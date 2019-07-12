---
title: Recommandations relatives aux performances pour Unity
description: Obtenir des conseils de Unity spécifiques pour améliorer les performances avec les applications de réalité mixte.
author: Troy-Ferrell
ms.author: trferrel
ms.date: 03/26/2019
ms.topic: article
keywords: graphiques, UC, gpu, de rendu, le garbage collection, hololens
ms.openlocfilehash: b0821f07184bff8630f6b6af0d0fc461f6fcd133
ms.sourcegitcommit: 8f3ff9738397d9b9fdf4703b14b89d416f0186a5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843335"
---
# <a name="performance-recommendations-for-unity"></a>Recommandations relatives aux performances pour Unity

Cet article s’appuie sur la discussion décrite dans [recommandations relatives aux performances pour la réalité mixte](understanding-performance-for-mixed-reality.md) mais se concentre sur les apprentissages spécifiques à l’environnement du moteur Unity.

Il est également vivement conseillé que les développeurs consulter le [environnement aux paramètres recommandés pour l’article Unity](Recommended-settings-for-unity.md). Cet article a contenu avec certaines configurations de scène plus importantes en ce qui concerne à la création d’applications de réalité mixte performante. Certains de ces paramètres recommandés sont également mis en surbrillance ci-dessous.

## <a name="how-to-profile-with-unity"></a>Comment Profiler avec Unity

Unity fournit le **[Unity Profiler](https://docs.unity3d.com/Manual/Profiler.html)** intégré qui est une excellente ressource pour rassembler des informations de performances précieuses pour votre application. Bien que le profileur éditeur exécutable, ces mesures ne représentent pas l’environnement d’exécution true et par conséquent, les résultats à partir de ce doivent être utilisés avec précaution. Il est recommandé à profiler à distance à votre application pendant son exécution sur le périphérique pour des informations plus précises et exploitables. En outre, d’Unity [Frame débogueur](https://docs.unity3d.com/Manual/FrameDebugger.html) est également très puissante et outil d’analyse à utiliser.

Unity fournit une documentation exceptionnelle pour :
1) Comment connecter le [profileur Unity pour applications UWP à distance](https://docs.unity3d.com/Manual/windowsstore-profiler.html)
2) Comment efficacement [diagnostiquer les problèmes de performances avec le Profiler Unity](https://unity3d.com/learn/tutorials/temas/performance-optimization/diagnosing-performance-problems-using-profiler-window)

>[!NOTE]
> Avec le Profiler Unity connecté et après avoir ajouté le profileur GPU (consultez *Profiler ajouter* dans le coin supérieur droit), vous pouvez voir combien de temps sur l’UC et GPU respectivement au milieu du profileur. Cela permet au développeur obtenir une approximation rapide si leur application est l’UC ou GPU délimité.
>
> ![Plug-in unityvs processeur GPU](images/unity-profiler-cpu-gpu.png)

## <a name="cpu-performance-recommendations"></a>Recommandations relatives aux performances de processeur

Le contenu ci-dessous présente les plus pratiques de performances approfondies, particulièrement ciblés pour Unity & C# développement.

#### <a name="cache-references"></a>Références du cache

Il est recommandé de cache des références à tous les composants concernés et GameObjects lors de l’initialisation. Il s’agit, car la répétition des appels de fonction comme *[GetComponent\<T > ()](https://docs.unity3d.com/ScriptReference/GameObject.GetComponent.html)* nettement plus élevé par rapport à la mémoire pour stocker un pointeur de coût. Cela s’applique également à la très, régulièrement utilisée [Camera.main](https://docs.unity3d.com/ScriptReference/Camera-main.html). *Camera.main* utilise en fait juste *[FindGameObjectsWithTag()](https://docs.unity3d.com/ScriptReference/GameObject.FindGameObjectsWithTag.html)* en dessous, qui recherche coûteuse de votre graphique de scène pour un objet appareil photo avec la *« MainCamera »*  balise.

```CS
using UnityEngine;
using System.Collections;

public class ExampleClass : MonoBehaviour
{
    private Camera cam;
    private CustomComponent comp;

    void Start() 
    {
        cam = Camera.main;
        comp = GetComponent<CustomComponent>();
    }

    void Update()
    {
        // Good
        this.transform.position = cam.transform.position + cam.transform.forward * 10.0f;

        // Bad
        this.transform.position = Camera.main.transform.position + Camera.main.transform.forward * 10.0f;

        // Good
        comp.DoSomethingAwesome();

        // Bad
        GetComponent<CustomComponent>().DoSomethingAwesome();
    }
}
```

>[!NOTE] 
> Éviter GetComponent(string) <br/>
> Lorsque vous utilisez  *[GetComponent()](https://docs.unity3d.com/ScriptReference/GameObject.GetComponent.html)* , il existe un certain nombre de surcharges différentes. Il est important de toujours utiliser les implémentations de Type en fonction et jamais la surcharge de recherche basé sur chaîne. La recherche par la chaîne dans votre scène est considérablement plus coûteuse que la recherche par Type. <br/>
> (Bon) Composant GetComponent (Type type) <br/>
> (Bon) T GetComponent\<T > () <br/>
> (Incorrect) Composant GetComponent(string) > <br/>

#### <a name="avoid-expensive-operations"></a>Éviter les opérations coûteuses

1) **Évitez d’utiliser [LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/getting-started-with-linq)**

    Même si LINQ peut être très propre et facile à lire et écrire, elle nécessite généralement beaucoup plus de calcul et plus particulièrement l’allocation de mémoire que l’écriture de l’algorithme manuellement.

    ```CS
    // Example Code
    using System.Linq;

    List<int> data = new List<int>();
    data.Any(x => x > 10);

    var result = from x in data
                 where x > 10
                 select x;
    ```

2) **API Unity courantes**

    Certaines API Unity, bien qu’utile, peut être très coûteux à exécuter. La plupart d'entre eux implique la recherche de votre graphique de scène entière pour une liste des GameObjects correspondants. Ces opérations peuvent généralement être évitées en mise en cache des références ou en implémentant un composant de gestionnaire pour les GameObjects en question suivre les références lors de l’exécution.

        GameObject.SendMessage()
        GameObject.BroadcastMessage()
        UnityEngine.Object.Find()
        UnityEngine.Object.FindWithTag()
        UnityEngine.Object.FindObjectOfType()
        UnityEngine.Object.FindObjectsOfType()
        UnityEngine.Object.FindGameObjectsWithTag()
        UnityEngine.Object.FindGameObjectsWithTag()

>[!NOTE]
> *[SendMessage()](https://docs.unity3d.com/ScriptReference/GameObject.SendMessage.html)*  et *[BroadcastMessage()](https://docs.unity3d.com/ScriptReference/GameObject.BroadcastMessage.html)* doivent être supprimés à tout prix. Ces fonctions peuvent être l’ordre de 1 000 x plus lent que les appels de fonction direct.

3) **Méfiez-vous des conversions boxing**

    [Boxing](https://docs.microsoft.com/dotnet/csharp/programming-guide/types/boxing-and-unboxing) est un concept fondamental de la C# langage et exécution. Il est le processus d’encapsuler des valeurs de variables telles que char, int, bool, etc. dans des variables de référence typée. Quand une variable typée à la valeur est « boxed », il est encapsulé à l’intérieur d’un System.Object qui est stocké sur le tas managé. Par conséquent, la mémoire est allouée et finalement lorsque supprimé doit être traité par le garbage collector. Ces allocations et les désallocations entraînent une baisse des performances et dans de nombreux scénarios ne sont pas nécessaires ou peuvent être facilement remplacées par une alternative moins coûteuse.

#### <a name="repeating-code-paths"></a>Chemins de code extensible

Les fonctions de rappel Unity extensibles (ex.) Mise à jour) qui sont exécutées plusieurs fois par seconde et/ou de frame doit être écrits très soigneusement. Les opérations coûteuses ici a impact énorme et cohérente sur les performances.

1) **Fonctions de rappel vide**

    Bien que le code ci-dessous peut sembler inoffensif à laisser dans votre application, en particulier depuis chaque Unity script automatique initialise avec ce bloc de code, ces rappels vides peuvent en réalité devenir très coûteux. Unity fonctionne dans les deux sens sur une limite de code gérés/non gérés, entre le code de UnityEngine et de votre code d’application. Contexte de basculement de ce pont est relativement coûteuse même s’il n’a rien à exécuter. Cela devient particulièrement problématique si votre application comporte des centaines de GameObjects avec des composants qui ont des rappels Unity extensibles vides.

    ```CS
    void Update()
    {
    }
    ```

>[!NOTE]
> Update() est la manifestation la plus commune de ce problème de performances, mais d’autres rappels Unity extensibles semblable à celui-ci peuvent être tout aussi mauvais si pas pire : FixedUpdate(), LateUpdate(), OnPostRender", OnPreRender(), OnRenderImage(), etc. 

2) **Opérations de favoriser en cours d’exécution une fois par frame**

    Les API Unity suivantes sont des opérations courantes pour de nombreuses applications HOLOGRAPHIQUE. Bien que pas toujours possible, les résultats de ces fonctions peuvent être très couramment calculées une fois et les résultats de nouveau utilisé à travers l’application pour une trame donnée.

    (a) en général il est conseillé de disposer d’une classe Singleton dédié ou un service pour gérer votre regard Raycast dans la scène et de réutiliser ensuite ce résultat dans tous les autres composants de la scène, au lieu d’effectuer des opérations Raycast répétées et fondamentalement identiques par chaque composant. Bien entendu, certaines applications peuvent nécessiter raycasts à partir de différentes origines ou par rapport à différents [LayerMasks](https://docs.unity3d.com/ScriptReference/LayerMask.html).

        UnityEngine.Physics.Raycast()
        UnityEngine.Physics.RaycastAll()

    (b) éviter les opérations de GetComponent() dans les rappels Unity répétées comme Update() par [mise en cache des références](#cache-references) dans Start() ou Awake()

        UnityEngine.Object.GetComponent()

    (c) il est conseillé à instancier tous les objets, si possible, à l’initialisation et l’utilisation [le pool d’objets](#object-pooling) à recycler et réutiliser les GameObjects tout au long de l’exécution de votre application

        UnityEngine.Object.Instantiate()

3) **Éviter les interfaces et les constructions virtuelles**

    Appels de fonction via des interfaces vs direct objets ou de l’appel de fonctions virtuelles peuvent souvent être beaucoup plus onéreux que l’utilisation de constructions directe ou des appels de fonction direct. Si la fonction virtuelle ou l’interface n’est pas nécessaire, elle doit être supprimée. Toutefois, les performances de ces approches d’accès valent généralement le compromis si leur utilisation simplifie la collaboration de développement, la lisibilité du code et la maintenabilité du code. 

4) **Éviter les structures de passage par valeur**

    Contrairement aux classes, structs sont des types de valeur, et quand il est passé directement à une fonction, leur contenu est copié dans une instance nouvellement créée. Cette copie ajoute le coût, ainsi que la mémoire supplémentaire sur la pile de l’UC. Pour les petits structs, l’effet est généralement très minimes et par conséquent acceptable. Toutefois, pour les fonctions appelées plusieurs fois chaque trame ainsi que des fonctions en prenant les structures de grande taille, si possible modifier la définition de fonction pour passer par référence. [En savoir plus ici](https://docs.microsoft.com/dotnet/csharp/programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method)

#### <a name="miscellaneous"></a>Divers

1) **Physique**

    (a) en règle générale, le plus simple pour améliorer physique consiste à limiter la quantité de temps passé sur physique ou le nombre d’itérations par seconde. Bien sûr, cela réduira la précision de la simulation. Consultez [TimeManager](https://docs.unity3d.com/Manual/class-TimeManager.html) dans Unity

    (b) le type de colliders dans Unity présentent des caractéristiques de performances très différents. L’ordre ci-dessous répertorie les plupart des colliders performante au moins performante colliders de gauche à droite. Il est plus important d’éviter Colliders maillage qui sont beaucoup plus cher que les colliders primitifs.

        Sphere < Capsule < Box <<< Mesh (Convex) < Mesh (non-Convex)

    Consultez [Unity physique meilleures pratiques](https://unity3d.com/learn/tutorials/topics/physics/physics-best-practices) pour plus d’informations

2) **Animations**

    Désactiver les animations inactives en désactivant le composant d’animation (la désactivation de l’objet de jeu ne sont pas avoir le même effet). Évitez les modèles de conception où un animateur se trouve dans une boucle de définition d’une valeur à la même chose. Il existe une charge considérable pour cette technique, sans aucune incidence sur l’application. [En savoir plus ici.](https://docs.unity3d.com/Manual/MecanimPeformanceandOptimization.html)

3) **Algorithmes complexes**

    Si votre application utilise des algorithmes complexes telles que la cinématique inverse, la recherche de chemin d’accès, etc., cherchez à une approche plus simple de trouver ou d’ajuster les paramètres appropriés pour leurs performances

## <a name="cpu-to-gpu-performance-recommendations"></a>Recommandations relatives aux performances de l’UC à GPU

En règle générale, les performances de l’UC à GPU est fourni jusqu'à la **les appels de dessin** soumis à la carte graphique. Pour améliorer les performances, appels de dessin doivent être programmées de façon stratégique **a) réduit** ou **b) restructuré** pour des résultats optimaux. Étant donné que les appels de dessin eux-mêmes sont gourmandes en ressources, ce qui réduit les réduira travail global requis. En outre, les modifications entre les appels de dessin requiert la validation coûteux et étapes de traduction dans le pilote graphique d’état et par conséquent, la restructuration de votre application appels de dessin pour limiter les changements d’état (ex.) différents, etc.) peut améliorer les performances.

Unity possède un excellent article qui donne une vue d’ensemble et explore le traitement par lot des appels de dessin pour leur plateforme.
- [Unity dessiner le traitement par lot des appels](https://docs.unity3d.com/Manual/DrawCallBatching.html)

#### <a name="single-pass-instanced-rendering"></a>Rendu instanciées passe unique

Rendu Instanced unique dans Unity permet les appels de dessin pour chaque œil être réduit à l’appel de dessin instancié une seule. En raison de la cohérence du cache entre les deux appels de dessin, il existe également une amélioration des performances sur le GPU également.

Pour activer cette fonctionnalité dans votre projet Unity
1)  Ouvrez **paramètres du lecteur XR** (accédez à **modifier** > **paramètres du projet** > **Player**  >  **XR paramètres**)
2) Sélectionnez **unique passer une instance créée** à partir de la **méthode de rendu stéréo** menu déroulant (**virtuel pris en charge de réalité** case doit être cochée)

Pour plus d’informations avec cette approche de rendu, lisez les articles suivants à partir d’Unity.
- [Comment optimiser les performances des AR et VR avec rendu stéréo avancé](https://blogs.unity3d.com/2017/11/21/how-to-maximize-ar-and-vr-performance-with-advanced-stereo-rendering/)
- [L’instanciation unique Pass](https://docs.unity3d.com/Manual/SinglePassInstancing.html) 

>[!NOTE]
> Un problème courant avec unique passer instancié rendu se produit si les développeurs ont déjà des nuanceurs personnalisés existants non écrits pour l’instanciation. Après avoir activé cette fonctionnalité, les développeurs remarquerez certains rendu uniquement GameObjects d’un oeil. Il s’agit comme les nuanceurs personnalisés associés n’ont pas les propriétés appropriées pour l’instanciation.
>
> Consultez [unique passer stéréo rendu pour HoloLens](https://docs.unity3d.com/Manual/SinglePassStereoRenderingHoloLens.html) à partir d’Unity pour savoir comment résoudre le problème

#### <a name="static-batching"></a>Le traitement par lots statique

Unity est en mesure de nombreux objets statiques afin de réduire les appels de dessin au GPU du lot. Le traitement par lots statique fonctionne pour la plupart des [convertisseur](https://docs.unity3d.com/ScriptReference/Renderer.html) objets dans Unity qui **1) partagent le même matériel** et **2) sont toutes marquées en tant que *statique***  () Sélectionnez un objet dans Unity et cliquez sur la case à cocher dans le coin supérieur droit de l’inspecteur). La mention GameObjects *statique* ne peut pas être déplacé dans l’ensemble du runtime de votre application. Par conséquent, le traitement par lots statique peut être difficile de tirer parti de HoloLens où pratiquement chaque objet doit être placé, déplacées, à l’échelle, etc. Pour des casques IMMERSIFS, le traitement par lots statique peut considérablement réduire les appels de dessin et améliore donc les performances.

Lecture *le traitement par lots statique* sous [dessiner appeler le traitement par lots dans Unity](https://docs.unity3d.com/Manual/DrawCallBatching.html) pour plus d’informations.

#### <a name="dynamic-batching"></a>Le traitement par lots dynamique

Dans la mesure où il est problématique pour marquer des objets en tant que *statique* pour le développement HoloLens, dynamique de traitement par lot peut être un excellent outil pour pallier cette absence de fonctionnalité. Bien sûr, il est peut également être utile dans des casques IMMERSIFS. Traitement par lot de manière dynamique dans Unity peut être difficile cependant activer car doit GameObjects **a) partage le même document** et **b) répondent à une longue liste d’autres critères**.

Lecture *le traitement par lots dynamique* sous [dessiner appeler le traitement par lots dans Unity](https://docs.unity3d.com/Manual/DrawCallBatching.html) pour obtenir la liste complète. En règle générale, GameObjects deviennent non valides pour être traités par lot dynamiquement, car les données de maillage associé peuvent être pas plus de 300 vertex.

#### <a name="other-techniques"></a>autres techniques

Le traitement par lots peut uniquement se produire si plusieurs GameObjects sont en mesure de partager le même matériel. En général, cela sera bloquée par la nécessité de GameObjects avoir une texture unique pour leurs documents respectifs. Il est courant de combiner des Textures dans une Texture volumineuse, une méthode appelée [Texture Atlasing](https://en.wikipedia.org/wiki/Texture_atlas).

En outre, il est généralement préférable de combiner les mailles en un GameObject si possible et raisonnable. Chaque convertisseur dans Unity aura il est associé à dessin appel (s) par rapport à l’envoi d’une maille combinée sous un convertisseur. 

>[!NOTE]
> Modification des propriétés de Renderer.material lors de l’exécution pour créer une copie de la matière et par conséquent susceptibles d’interrompre le traitement par lots. Utilisez Renderer.sharedMaterial pour modifier les propriétés de matériel partagées entre les GameObjects.

## <a name="gpu-performance-recommendations"></a>Recommandations relatives aux performances de GPU

En savoir plus sur [optimisation de rendu de graphiques dans Unity](https://unity3d.com/learn/tutorials/temas/performance-optimization/optimizing-graphics-rendering-unity-games) 

### <a name="optimize-depth-buffer-sharing"></a>Optimiser le partage de mémoire tampon de profondeur

Il est généralement recommandé d’activer **partage de mémoire tampon de profondeur** sous **paramètres du lecteur XR** afin d’optimiser [la stabilité hologramme](Hologram-stability.md). Lors de l’activation basée sur une profondeur de reprojection minute avec ce paramètre Toutefois, il est recommandé de sélectionner **format de la profondeur de 16 bits** au lieu de **format de 24 bits profondeur**. La volonté de mémoires tampons de profondeur de 16 bits réduit considérablement la bande passante (et par conséquent, l’alimentation) associé au trafic de mémoire tampon de profondeur. Cela peut s’avérer efficace en puissance, mais il est uniquement applicable pour les expériences avec une plage de profondeur petit comme [z lutte](https://en.wikipedia.org/wiki/Z-fighting) est susceptible de se produire avec 16 bits à 24 bits. Pour éviter ces artefacts, modifier les plans de découpage près/lointain de le [appareil photo Unity](https://docs.unity3d.com/Manual/class-Camera.html) pour prendre en compte pour la précision inférieure. Pour les applications basées sur HoloLens, un plan de découpage lointain de 50 millions au lieu de la valeur par défaut de Unity 1000 m peut éliminer généralement un z fighting.

### <a name="reduce-poly-count"></a>Réduire le nombre de poly

Nombre de polygone est généralement réduite à l’aide
1) Suppression d’objets dans une scène
2) Décimalisation Asset ce qui réduit le nombre de polygones pour une maille donnée
3) Implémentation d’un [système de niveau de détail (LOD)](https://docs.unity3d.com/Manual/LevelOfDetail.html) dans votre application qui restitue éloigné des objets avec une version inférieure-polygone de la même géométrie

### <a name="understanding-shaders-in-unity"></a>Nuanceurs de présentation dans Unity

Une approximation facile à comparer les nuanceurs de performances est d’identifier le nombre moyen d’opérations chaque s’exécute lors de l’exécution. Cela est possible facilement dans Unity.

1) Sélectionnez votre ressource de nuanceur ou sélectionnez un matériau, puis dans le coin supérieur droit de la fenêtre Inspecteur, sélectionnez l’icône d’engrenage, puis **« Sélectionnez nuanceur »**

    ![Sélectionnez le nuanceur dans Unity](images/Select-shader-unity.png)
2) La ressource de nuanceur sélectionnée, puis cliquez sur le **« Compilation et l’affichage de code »** bouton sous la fenêtre Inspecteur

    ![Compiler le Code de nuanceur dans Unity](images/compile-shader-code-unity.PNG)

3) Après la compilation, recherchez la section des statistiques dans les résultats avec le nombre d’opérations différents pour le nuanceur de sommets et de pixels (Remarque : des nuanceurs de pixels sont souvent également appelés des nuanceurs de fragment)

    ![Opérations Standard de nuanceur Unity](images/unity-standard-shader-compilation.png)

#### <a name="optmize-pixel-shaders"></a>Optimisation des nuanceurs

Regarder les résultats statistiques compilées à l’aide de la méthode ci-dessus, le [fragment shader](https://en.wikipedia.org/wiki/Shader#Pixel_shaders) exécutera généralement des opérations plus que le [nuanceur de sommets](https://en.wikipedia.org/wiki/Shader#Vertex_shaders) en moyenne. Le nuanceur de fragment, également connu sous le nuanceur de pixels est exécuté par pixel sur l’écran pendant que le nuanceur de sommets est uniquement exécutée par vertex de toutes les mailles dessinés à l’écran de sortie. 

Par conséquent, non seulement les nuanceurs de fragment ont plus d’instructions que des nuanceurs de sommets en raison de tous les calculs d’éclairage, les nuanceurs de fragment sont presque toujours exécutés dans un dataset plus volumineux. Par exemple, si la sortie de l’écran est un 2k par 2 image k, le nuanceur de fragment peut obtenir exécutée 2 000 * 2, = 4,000,000 000 fois. Si deux yeux de rendu, ce nombre double dans la mesure où il existe deux écrans. Si une application de réalité mixte a plusieurs passes, plein écran post-traitement effets ou rendre plusieurs mailles au même pixel, ce nombre augmente considérablement. 

Par conséquent, ce qui réduit le nombre d’opérations dans le nuanceur de fragment généralement permettent bien plus des gains de performances sur les optimisations dans le nuanceur de sommets.

#### <a name="unity-standard-shader-alternatives"></a>Alternatives de nuanceur Standard Unity

Au lieu d’utiliser un rendu physiquement en (PBR) ou autres nuanceur de haute qualité, rechercher l’utilisation d’un plus performant et plus économique nuanceur. Le [Toolkit de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity) fournit le [nuanceur standard MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_MRTKStandardShader.html) qui a été optimisé pour les projets de réalité mixte.

Unity fournit également un éteint, vertex allumée et les options de nuanceur simplifiée diffuse et d’autres qui sont considérablement plus rapide que le nuanceur Unity Standard. Consultez [l’utilisation et les performances de nuanceurs intégrés](https://docs.unity3d.com/Manual/shader-Performance.html) pour des informations plus détaillées.

#### <a name="shader-preloading"></a>Le préchargement de nuanceur

Utilisez *nuanceur préchargement* et autres astuces pour optimiser [temps de chargement du nuanceur](http://docs.unity3d.com/Manual/OptimizingShaderLoadTime.html). En particulier, le préchargement de nuanceur signifie que vous ne voyez pas toutes eu de problèmes en raison de la compilation de nuanceur de runtime.

### <a name="limit-overdraw"></a>Limite de superposition

Dans Unity, un peut afficher superposition pour leur scène, en basculant le [ **dessiner menu mode** ](https://docs.unity3d.com/Manual/ViewModes.html) dans le coin supérieur gauche de la **vue de la scène** et en sélectionnant **superpositions** .

En règle générale, la superposition peut être atténuée à l’élimination des objets à l’avance avant leur envoi vers le GPU. Unity fournit des détails sur l’implémentation de [coupe d’Occlusion](https://docs.unity3d.com/Manual/OcclusionCulling.html) pour leur moteur.

## <a name="memory-recommendations"></a>Recommandations de mémoire

Opérations d’allocation et désallocation de mémoire excessive peuvent avoir des effets négatifs sur votre application holographique avec performances incohérent, cadres figés et autres comportements nuisibles. Il est particulièrement important de comprendre les considérations relatives à la mémoire lors du développement dans Unity, étant donné que la gestion de la mémoire est contrôlée par le garbage collector.

#### <a name="garbage-collection"></a>Le garbage collection

Applications HOLOGRAPHIQUE perdent leur temps de calcul de traitement pour le garbage collector (GC) quand le GC est activé pour analyser les objets qui ne sont plus dans la portée lors de l’exécution et leur mémoire doit être libéré peut être rendue disponible pour une réutilisation. Allocations de déduplication et constante nécessitera généralement le garbage collector s’exécute plus fréquemment par conséquent promu de performances et l’expérience utilisateur.

Unity a fourni une excellente page qui explique en détail comment le garbage collector fonctionne et conseils pour écrire du code plus efficace en ce qui concerne à la gestion de la mémoire.
- [Optimiser le garbage collection de jeux Unity](https://unity3d.com/learn/tutorials/topics/performance-optimization/optimizing-garbage-collection-unity-games?playlist=44069)

Parmi les pratiques les plus courantes qui conduit au garbage collection excessif n'est pas mise en cache des références aux composants et les classes de développement Unity. Toutes les références doivent être capturées pendant Start() ou Awake() et réutilisés dans les fonctions ultérieures telles que Update() ou LateUpdate().

Autres conseils rapides :
- Utilisez le [StringBuilder](https://docs.microsoft.com/dotnet/api/system.text.stringbuilder?view=netframework-4.7.2) C# classe pour générer dynamiquement des chaînes complexes lors de l’exécution
- Supprimez les appels à Debug.Log() lorsqu’inutile car ils s’exécutent toujours dans toutes les versions de génération d’une application
- Si votre application HOLOGRAPHIQUE nécessite généralement beaucoup de mémoire, envisagez d’appeler [ _**System.GC.Collect()**_ ](https://docs.microsoft.com/dotnet/api/system.gc.collect?view=netframework-4.7.2) pendant le chargement des phases telles que lors de la présentation d’un chargement ou écran de transition

#### <a name="object-pooling"></a>Pool d’objets

Le pool d’objets est une technique répandue qui permet de réduire le coût des allocations continues & désallocations d’objets. Pour cela, en allouant un grand nombre d’objets identiques et en réutilisant les instances inactives, disponibles à partir de ce pool au lieu de constamment lors de la génération et la destruction d’objets au fil du temps. Les pools d’objet sont idéales pour des composants réutilisables qui possèdent la durée de vie des variable au cours d’une application.

- [Objet de regroupement de didacticiel dans Unity](https://unity3d.com/learn/tutorials/topics/scripting/object-pooling) 

## <a name="startup-performance"></a>Performances de démarrage

Vous devez envisager de démarrage de votre application avec une scène plus petits, puis à l’aide de *[SceneManager.LoadSceneAsync](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.LoadSceneAsync.html)* pour charger le reste de la scène. Cela permet à votre application accéder à un état interactif aussi rapidement que possible. Être prenant en charge qui peut contenir un grand pic d’UC pendant que la nouvelle scène est activée et que n’importe quel contenu rendu peut être perturbée ou aucune difficulté. Une façon de contourner ce problème consiste à définir la propriété AsyncOperation.allowSceneActivation sur false sur la scène en cours de chargement, d’attente de la scène charger, désactivez l’écran noir et puis rétabli sur true pour effectuer l’activation de la scène.

N’oubliez pas que, pendant le chargement de la scène de démarrage, l’écran de démarrage holographique est affiché à l’utilisateur.

## <a name="see-also"></a>Voir aussi
- [Optimisation de rendu de graphiques dans des jeux Unity](https://unity3d.com/learn/tutorials/temas/performance-optimization/optimizing-graphics-rendering-unity-games?playlist=44069)
- [Optimiser le garbage collection de jeux Unity](https://unity3d.com/learn/tutorials/topics/performance-optimization/optimizing-garbage-collection-unity-games?playlist=44069)
- [Physique meilleures pratiques [Unity]](https://unity3d.com/learn/tutorials/topics/physics/physics-best-practices)
- [Optimisation des Scripts [Unity]](https://docs.unity3d.com/Manual/MobileOptimizationPracticalScriptingOptimizations.html)
