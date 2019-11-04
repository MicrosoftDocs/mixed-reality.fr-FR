---
title: Recommandations en matière de performances pour Unity
description: Conseils spécifiques à Unity pour améliorer les performances avec des applications de réalité mixte.
author: Troy-Ferrell
ms.author: trferrel
ms.date: 03/26/2019
ms.topic: article
keywords: graphiques, UC, GPU, rendu, garbage collection, hololens
ms.openlocfilehash: 724ec24408e70360fda07c59a4ca2ffc30b49c1f
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438129"
---
# <a name="performance-recommendations-for-unity"></a>Recommandations en matière de performances pour Unity

Cet article s’appuie sur la discussion présentée dans [recommandations de performances pour la réalité mixte](understanding-performance-for-mixed-reality.md) , mais se concentre sur les apprentissages spécifiques à l’environnement du moteur Unity.

Il est également vivement conseillé aux développeurs de passer en revue les [paramètres d’environnement recommandés pour l’article Unity](Recommended-settings-for-unity.md). Cet article contient du contenu avec certaines des configurations de scène les plus importantes en ce qui concerne la création d’applications de réalité mixte performantes. Certains de ces paramètres recommandés sont également mis en surbrillance ci-dessous.

## <a name="how-to-profile-with-unity"></a>Profilage avec Unity

Unity fournit le **[profileur Unity](https://docs.unity3d.com/Manual/Profiler.html)** , qui est une excellente ressource permettant de recueillir des informations de performances précieuses pour votre application. Bien qu’il soit possible d’exécuter le profileur dans l’éditeur, ces mesures ne représentent pas l’environnement d’exécution réel et, par conséquent, les résultats de ce doivent être utilisés avec prudence. Nous vous recommandons de profiler à distance votre application en cours d’exécution sur l’appareil pour obtenir des informations plus précises et exploitables. En outre, le [débogueur de frames](https://docs.unity3d.com/Manual/FrameDebugger.html) Unity est également un outil très puissant et d’analyse à utiliser.

Unity fournit une documentation très utile pour :
1) Comment connecter le [profileur Unity aux applications UWP à distance](https://docs.unity3d.com/Manual/windowsstore-profiler.html)
2) Comment [diagnostiquer efficacement les problèmes de performances avec le profileur Unity](https://unity3d.com/learn/tutorials/temas/performance-optimization/diagnosing-performance-problems-using-profiler-window)

>[!NOTE]
> Lorsque le profileur Unity est connecté et après l’ajout du profileur GPU (voir *Ajouter le profileur* dans l’angle supérieur droit), vous pouvez voir le temps passé sur le processeur & GPU, respectivement au milieu du profileur. Cela permet au développeur d’obtenir une approximation rapide si son application est liée à l’UC ou au GPU.
>
> ![UC et GPU Unity](images/unity-profiler-cpu-gpu.png)

## <a name="cpu-performance-recommendations"></a>Recommandations relatives aux performances de l’UC

Le contenu ci-dessous couvre des pratiques de performances plus approfondies, en C# particulier destinées au développement & Unity.

#### <a name="cache-references"></a>Références du cache

Il est recommandé de mettre en cache les références à tous les composants et GameObjects pertinents lors de l’initialisation. Cela est dû au fait que les appels de fonction répétitifs, tels que *[GetComponent\<t > ()](https://docs.unity3d.com/ScriptReference/GameObject.GetComponent.html)* , sont beaucoup plus coûteux par rapport au coût de mémoire pour stocker un pointeur. Cela s’applique également à l' [appareil photo. main régulièrement utilisé. main](https://docs.unity3d.com/ScriptReference/Camera-main.html). *Camera. main* utilise en fait simplement *[FindGameObjectsWithTag ()](https://docs.unity3d.com/ScriptReference/GameObject.FindGameObjectsWithTag.html)* en dessous, qui effectue une recherche coûteuse dans votre graphique de scène pour un objet Camera avec la balise *« MainCamera »* .

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
> Évitez GetComponent (String) <br/>
> Lors de l’utilisation de *[GetComponent ()](https://docs.unity3d.com/ScriptReference/GameObject.GetComponent.html)* , il existe un certain nombre de surcharges différentes. Il est important de toujours utiliser les implémentations basées sur le type et jamais la surcharge de recherche basée sur chaîne. La recherche par chaîne dans votre scène est beaucoup plus coûteuse que la recherche par type. <br/>
> État GetComponent composant (type type) <br/>
> État T GetComponent\<T > () <br/>
> Incorrecte GetComponent du composant (chaîne) > <br/>

#### <a name="avoid-expensive-operations"></a>Évitez les opérations coûteuses

1) **Éviter l’utilisation de [LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/getting-started-with-linq)**

    Même si LINQ peut être très propre et facile à lire et à écrire, il requiert généralement beaucoup plus de calculs et plus particulièrement plus d’allocation de mémoire que l’écriture manuelle de l’algorithme.

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

    Certaines API Unity, bien qu’utiles, peuvent être très chères à s’exécuter. La plupart d’entre elles impliquent la recherche d’une liste de GameObjects correspondante dans l’ensemble du graphique de scène. Ces opérations peuvent généralement être évitées en mettant en cache des références ou en implémentant un composant de gestionnaire pour le GameObjects en question pour suivre les références au moment de l’exécution.

        GameObject.SendMessage()
        GameObject.BroadcastMessage()
        UnityEngine.Object.Find()
        UnityEngine.Object.FindWithTag()
        UnityEngine.Object.FindObjectOfType()
        UnityEngine.Object.FindObjectsOfType()
        UnityEngine.Object.FindGameObjectsWithTag()
        UnityEngine.Object.FindGameObjectsWithTag()

>[!NOTE]
> *[SendMessage ()](https://docs.unity3d.com/ScriptReference/GameObject.SendMessage.html)* et *[BroadcastMessage ()](https://docs.unity3d.com/ScriptReference/GameObject.BroadcastMessage.html)* doivent être éliminés à tout prix. Ces fonctions peuvent être dans l’ordre de 1 000 fois plus lentes que les appels de fonction directs.

3) **Méfiez-vous du Boxing**

    La C# [conversion boxing](https://docs.microsoft.com/dotnet/csharp/programming-guide/types/boxing-and-unboxing) est un concept fondamental du langage et du Runtime. C’est le processus qui consiste à encapsuler des variables de type valeur, telles que Char, int, bool, etc., dans des variables de type référence. Quand une variable de type valeur est « boxed », elle est encapsulée à l’intérieur d’un System. Object qui est stocké sur le tas managé. Par conséquent, la mémoire est allouée et, quand elle est supprimée, elle doit être traitée par le garbage collector. Ces allocations et désallocations entraînent un coût de performance et, dans de nombreux scénarios, sont inutiles ou peuvent être facilement remplacées par une alternative moins coûteuse.

    L’une des formes les plus courantes de boxing dans le développement est l’utilisation de [types valeur Nullable](https://docs.microsoft.com//dotnet/csharp/programming-guide/nullable-types/). Il est courant de vouloir retourner null pour un type valeur dans une fonction, en particulier lorsque l’opération peut échouer en tentant d’obtenir la valeur. Le problème potentiel de cette approche est que l’allocation se produit maintenant sur le tas et doit donc être récupérée par le garbage collector ultérieurement.

    **Exemple de boxing dansC#**

    ```csharp
    // boolean value type is boxed into object boxedMyVar on the heap
    bool myVar = true;
    object boxedMyVar = myVar;
    ```

    **Exemple de boxing problématique via les types valeur Nullable**

    Ce code illustre une classe de particule factice qu’il est possible de créer dans un projet Unity. Un appel à `TryGetSpeed()` entraîne l’allocation d’objets sur le tas qui devra être récupéré par le garbage collector ultérieurement. Cet exemple est particulièrement problématique, car il peut y avoir plus de 1000 particules dans une scène, chacune étant demandée pour la vitesse actuelle. Par conséquent, 1 000 d’objets seraient alloués et, par conséquent, désalloués à chaque trame, ce qui aurait beaucoup diminué les performances. La réécriture de la fonction pour retourner une valeur négative telle que-1 pour indiquer qu’un échec peut éviter ce problème et conserver la mémoire sur la pile.

    ```csharp
        public class MyParticle
        {
            // Example of function returning nullable value type
            public int? TryGetSpeed()
            {
                // Returns current speed int value or null if fails
            }
        }
    ```

#### <a name="repeating-code-paths"></a>Répéter les chemins de code

Toutes les fonctions de rappel Unity répétitives (c.-à-d. Update) qui sont exécutées plusieurs fois par seconde et/ou que le frame doit être écrit très attentivement. Toutes les opérations coûteuses ici auront un impact énorme et cohérent sur les performances.

1) **Fonctions de rappel vides**

    Bien que le code ci-dessous puisse paraître inoffensif dans votre application, en particulier puisque chaque script Unity s’initialise automatiquement avec ce bloc de code, ces rappels vides peuvent en fait devenir très coûteux. Unity fonctionne de façon alternée par rapport à une limite de code non managé/managé, entre le code UnityEngine et votre code d’application. Le changement de contexte sur ce pont est assez coûteux même s’il n’y a rien à exécuter. Cela devient particulièrement problématique si votre application a 100 GameObjects avec des composants qui ont des rappels Unity répétitifs vides.

    ```CS
    void Update()
    {
    }
    ```

>[!NOTE]
> Update () est la manifestation la plus courante de ce problème de performance, mais d’autres rappels Unity répétitifs, tels que les suivants, peuvent également être aussi mauvais si ce n’est pas pire : FixedUpdate (), LateUpdate (), OnPostRender», OnPreRender (), OnRenderImage (), etc. 

2) **Opérations à privilégier en cours d’exécution par frame**

    Les API Unity suivantes sont des opérations courantes pour de nombreuses applications holographiques. Bien que cela ne soit pas toujours possible, les résultats de ces fonctions peuvent être souvent calculés une fois et les résultats réutilisés dans l’application pour une trame donnée.

    r. en général, il est recommandé de disposer d’une classe ou d’un service Singleton dédié pour gérer votre Raycast de pointage dans la scène, puis de réutiliser ce résultat dans tous les autres composants de scène, au lieu d’effectuer des opérations Raycast répétées et fondamentalement identiques pour chaque -. Bien entendu, certaines applications peuvent nécessiter des raycasts provenant de différentes origines ou de différentes [LayerMasks](https://docs.unity3d.com/ScriptReference/LayerMask.html).

        UnityEngine.Physics.Raycast()
        UnityEngine.Physics.RaycastAll()

    b) Évitez les opérations GetComponent () dans les rappels Unity répétés tels que Update () en [mettant en cache les références](#cache-references) dans START () ou éveillé ()

        UnityEngine.Object.GetComponent()

    c) il est recommandé d’instancier tous les objets, si possible, lors de l’initialisation et utiliser le [pool d’objets](#object-pooling) pour recycler et réutiliser les GameObjects tout au long de l’exécution de votre application

        UnityEngine.Object.Instantiate()

3) **Évitez les interfaces et les constructions virtuelles**

    L’appel d’appels de fonction via des interfaces et des objets directs ou l’appel de fonctions virtuelles peut souvent être beaucoup plus coûteux que l’utilisation de constructions directes ou d’appels de fonction directs. Si la fonction ou l’interface virtuelle n’est pas nécessaire, elle doit être supprimée. Toutefois, l’impact sur les performances de ces approches est généralement plus intéressant si leur utilisation simplifie la collaboration au développement, la lisibilité du code et la maintenabilité du code.

    En règle générale, il est recommandé de ne pas marquer les champs et les fonctions comme virtuels, à moins qu’il y ait une attente claire que ce membre doive être remplacé. L’un d’eux doit être particulièrement attentif aux chemins de code à haute fréquence qui sont appelés plusieurs fois par trame, ou même une fois par Frame, par exemple une méthode de `UpdateUI()`.

4) **Évitez de passer des structs par valeur**

    Contrairement aux classes, les structs sont des types valeur et lorsqu’ils sont passés directement à une fonction, leur contenu est copié dans une instance nouvellement créée. Cette copie ajoute le coût de l’UC, ainsi que la mémoire supplémentaire sur la pile. Pour les petits structs, l’effet est généralement très minime et donc acceptable. Toutefois, pour les fonctions appelées à plusieurs reprises à chaque trame ainsi que les fonctions acceptant des structures volumineuses, si possible, modifiez la définition de fonction pour qu’elle passe par référence. [En savoir plus ici](https://docs.microsoft.com/dotnet/csharp/programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method)

#### <a name="miscellaneous"></a>Divers

1) **Physique**

    r) en général, le moyen le plus simple d’améliorer la physique consiste à limiter le temps consacré à la physique ou au nombre d’itérations par seconde. Bien entendu, cela permet de réduire la précision de la simulation. Voir [timemanager](https://docs.unity3d.com/Manual/class-TimeManager.html) dans Unity

    b) le type de conflits dans Unity a des caractéristiques de performances très différentes. L’ordre ci-dessous répertorie les conflits les plus performants pour les conflits les plus performants, de gauche à droite. Il est plus important d’éviter les conflits de maille qui sont beaucoup plus coûteux que les conflits primitifs.

        Sphere < Capsule < Box <<< Mesh (Convex) < Mesh (non-Convex)

    Pour plus d’informations, consultez [meilleures pratiques pour la physique Unity](https://unity3d.com/learn/tutorials/topics/physics/physics-best-practices)

2) **Animations**

    Désactivez les animations inactives en désactivant le composant d’animation (la désactivation de l’objet de jeu n’a pas le même effet). Évitez les modèles de conception où un animateur se trouve dans une boucle qui affecte une valeur à la même chose. Cette technique présente une surcharge considérable, sans effet sur l’application. [Pour en savoir plus, cliquez ici.](https://docs.unity3d.com/Manual/MecanimPeformanceandOptimization.html)

3) **Algorithmes complexes**

    Si votre application utilise des algorithmes complexes tels que des cinématiques inverses, des recherches de chemin, etc., recherchez une approche plus simple ou ajustez les paramètres pertinents pour leurs performances.

## <a name="cpu-to-gpu-performance-recommendations"></a>Recommandations relatives aux performances de l’UC vers GPU

En règle générale, les performances de l’UC vers le GPU baissent les **appels de dessin** soumis à la carte graphique. Pour améliorer les performances, les appels de dessin doivent être stratégiques, **réduits** ou **b) restructurés** pour obtenir des résultats optimaux. Étant donné que les appels de dessin eux-mêmes sont gourmands en ressources, leur réduction réduira le travail global requis. En outre, les changements d’État entre les appels de dessin nécessitent une validation et des étapes de traduction coûteuses dans le pilote graphique et, par conséquent, la restructuration des appels de dessin de votre application pour limiter les changements d’État (c.-à-d. les différents matériaux, etc.) peuvent améliorer les performances.

Unity est un excellent article qui donne une vue d’ensemble et explore le traitement par lot des appels de dessin pour sa plateforme.
- [Traitement par lot des appels Unity](https://docs.unity3d.com/Manual/DrawCallBatching.html)

#### <a name="single-pass-instanced-rendering"></a>Rendu d’instance à passe unique

Le rendu d’instance à passage unique dans Unity permet de réduire les appels de dessin pour chaque œil jusqu’à un appel de dessin instancié. En raison de la cohérence du cache entre deux appels de dessin, il y a également une amélioration des performances sur le GPU.

Pour activer cette fonctionnalité dans votre projet Unity
1)  Ouvrez **les paramètres du XR Player** (accédez à **modifier** > **paramètres du projet** > **lecteur** > **paramètres XR**)
2) Sélectionnez **une instance de passe unique** dans le menu déroulant **méthode de rendu stéréo** (la case à cocher de**la réalité virtuelle** doit être activée)

Lisez les articles suivants sur Unity pour plus d’informations sur cette approche de rendu.
- [Optimisation des performances de l’AR et du VR avec un rendu stéréo avancé](https://blogs.unity3d.com/2017/11/21/how-to-maximize-ar-and-vr-performance-with-advanced-stereo-rendering/)
- [Instanciation à passage unique](https://docs.unity3d.com/Manual/SinglePassInstancing.html) 

>[!NOTE]
> Un problème courant avec un rendu d’instance à passage unique se produit si les développeurs possèdent déjà des nuanceurs personnalisés existants non écrits pour l’instanciation. Une fois cette fonctionnalité activée, les développeurs peuvent remarquer que certains GameObjects ne s’affichent qu’en un seul œil. Cela est dû au fait que les nuanceurs personnalisés associés n’ont pas les propriétés appropriées pour l’instanciation.
>
> Consultez [rendu stéréo à passage unique pour HoloLens](https://docs.unity3d.com/Manual/SinglePassStereoRenderingHoloLens.html) à partir d’Unity pour savoir comment résoudre ce problème

#### <a name="static-batching"></a>Traitement par lot statique

Unity peut traiter par lot de nombreux objets statiques pour réduire les appels de dessin au GPU. Le traitement par lots statique fonctionne pour la plupart des objets de [convertisseur](https://docs.unity3d.com/ScriptReference/Renderer.html) dans Unity qui **1) partagent le même matériau** et **2) sont tous marqués comme *statiques***  (sélectionnez un objet dans Unity et cliquez sur la case à cocher en haut à droite de l’inspecteur). Les GameObjects marqués comme *static* ne peuvent pas être déplacés tout au long de l’exécution de votre application. Par conséquent, le traitement par lot statique peut être difficile à exploiter sur HoloLens, où pratiquement tous les objets doivent être placés, déplacés, mis à l’échelle, etc. Pour les casques immersifs, le traitement par lot statique peut réduire considérablement les appels de dessin et donc améliorer les performances.

Pour plus d’informations, consultez *traitement par lot statique* sous [créer un traitement par lot dans Unity](https://docs.unity3d.com/Manual/DrawCallBatching.html) .

#### <a name="dynamic-batching"></a>Traitement par lot dynamique

Étant donné qu’il est difficile de marquer les objets comme *statiques* pour le développement HoloLens, le traitement par lot dynamique peut être un excellent outil pour compenser cette fonctionnalité non compensée. Bien entendu, il peut également être utile sur les casques immersifs. Le traitement par lots dynamique dans Unity peut être difficile à activer, car GameObjects doit **partager les mêmes documents** et **b) répondre à une longue liste d’autres critères**.

Pour obtenir la liste complète, lisez *traitement dynamique par lot* sous l' [appel de dessin](https://docs.unity3d.com/Manual/DrawCallBatching.html) . En règle générale, les GameObjects ne sont plus valides pour être regroupés de manière dynamique, car les données de maillage associées ne peuvent pas dépasser 300 sommets.

#### <a name="other-techniques"></a>Autres techniques

Le traitement par lot ne peut se produire que si plusieurs GameObjects sont en mesure de partager le même document. En général, cette opération est bloquée par la nécessité pour GameObjects d’avoir une texture unique pour leur matériau respectif. Il est courant de combiner les textures en une seule grande texture, une méthode appelée « [Atlas des textures](https://en.wikipedia.org/wiki/Texture_atlas)».

En outre, il est généralement préférable de combiner les mailles en un seul GameObject, lorsque cela est possible et raisonnable. Chaque convertisseur dans Unity a des appels de dessin associés et envoie un maillage combiné sous un convertisseur.

>[!NOTE]
> Modification des propriétés du convertisseur. la documentation au moment de l’exécution crée une copie du matériau et, par conséquent, interrompt le traitement par lot. Utilisez Renderr. sharedMaterial pour modifier les propriétés des matériaux partagés entre les GameObjects.

## <a name="gpu-performance-recommendations"></a>Recommandations relatives aux performances GPU

En savoir plus sur [l’optimisation du rendu graphique dans Unity](https://unity3d.com/learn/tutorials/temas/performance-optimization/optimizing-graphics-rendering-unity-games)

### <a name="optimize-depth-buffer-sharing"></a>Optimiser le partage du tampon de profondeur

Il est généralement recommandé d’activer le **partage de mémoire tampon de profondeur** sous les paramètres de **XR Player** pour optimiser la stabilité de l' [hologramme](Hologram-stability.md). Lors de l’activation de la reprojection à l’étape à base de la profondeur avec ce paramètre, il est recommandé de sélectionner le **format de profondeur 16** bits au lieu du **format de profondeur 24 bits**. Les mémoires tampons de profondeur 16 bits réduisent considérablement la bande passante (et donc la puissance) associée au trafic de mémoire tampon de profondeur. Il peut s’agir d’un grand succès en matière de réduction de l’alimentation et d’amélioration des performances. Toutefois, il existe deux résultats négatifs possibles en utilisant *le format de profondeur 16 bits*.

**Z-combat**

La fidélité de la plage de profondeur réduite rend la [lutte z](https://en.wikipedia.org/wiki/Z-fighting) plus susceptible de se produire avec 16 bits que 24 bits. Pour éviter ces artefacts, modifiez les plans de clip proches/Far de l' [appareil photo Unity](https://docs.unity3d.com/Manual/class-Camera.html) afin de réduire la précision. Pour les applications basées sur HoloLens, un plan de découpage de 50 millions à la place de l’unité par défaut de l’unité de mesure peut généralement éliminer toute lutte z.

**Tampon de stencil désactivé**

Quand Unity crée une [texture de rendu avec une profondeur de 16 bits](https://docs.unity3d.com/ScriptReference/RenderTexture-depth.html), aucune mémoire tampon de stencil n’est créée. La sélection du format de profondeur 24 bits, par documentation Unity, créera une mémoire tampon z de 24 bits ainsi qu’une [mémoire tampon de stencil de 8 bits](https://docs.unity3d.com/Manual/SL-Stencil.html) (si 32 bits est applicable sur l’appareil, ce qui est généralement le cas, par exemple, HoloLens).

### <a name="avoid-full-screen-effects"></a>Éviter les effets plein écran

Les techniques qui fonctionnent en mode plein écran peuvent être assez onéreuses, car leur ordre de grandeur est de millions d’opérations chaque trame. Par conséquent, il est recommandé d’éviter les effets de la [publication](https://docs.unity3d.com/Manual/PostProcessingOverview.html) , tels que l’anticrénelage, les fleurs et bien plus encore.

### <a name="optimal-lighting-settings"></a>Paramètres d’éclairage optimaux

L' [éclairage global](https://docs.unity3d.com/Manual/GIIntro.html) en temps réel dans Unity peut fournir des résultats visuels nombre, mais implique des calculs d’éclairage très coûteux. Il est recommandé de désactiver l’éclairage global en temps réel pour chaque fichier de scène Unity via la **fenêtre** > le **rendu** > **paramètres d’éclairage** > de décocher l' **éclairage global en temps réel**.

En outre, il est recommandé de désactiver toutes les captures instantanées, car celles-ci ajoutent des passes GPU coûteuses à une scène Unity. Les ombres peuvent être désactivées par lumière, mais peuvent également être contrôlées de façon holistique via des paramètres de qualité.

**Modifiez** > **paramètres du projet**, puis sélectionnez la catégorie **qualité** > sélectionnez **faible qualité** pour la plateforme UWP. Il est également possible de définir simplement la propriété **Shadows** pour **Désactiver les ombres**.

### <a name="reduce-poly-count"></a>Réduire le nombre de poly

Le nombre de polygones est généralement réduit par
1) Suppression d’objets d’une scène
2) Décimalisation de la ressource qui réduit le nombre de polygones pour un filet donné
3) Implémentation d’un [système de niveau de détail (LOD)](https://docs.unity3d.com/Manual/LevelOfDetail.html) dans votre application qui restitue des objets éloignés avec une version de polygone plus faible de la même géométrie

### <a name="understanding-shaders-in-unity"></a>Fonctionnement des nuanceurs dans Unity

Une approximation facile pour comparer les nuanceurs en matière de performances consiste à identifier le nombre moyen d’opérations qui s’exécutent chaque fois au moment de l’exécution. Cela peut être fait facilement dans Unity.

1) Sélectionnez votre élément de nuanceur ou sélectionnez un matériau, puis dans le coin supérieur droit de la fenêtre de l’inspecteur, sélectionnez l’icône d’engrenage, puis **sélectionnez le nuanceur** .

    ![Sélectionner le nuanceur dans Unity](images/Select-shader-unity.png)
2) Une fois l’élément de nuanceur sélectionné, cliquez sur le bouton **« compiler et afficher le code »** sous la fenêtre de l’inspecteur.

    ![Compiler le code du nuanceur dans Unity](images/compile-shader-code-unity.PNG)

3) Après la compilation, recherchez la section des statistiques dans les résultats avec le nombre d’opérations différentes pour le vertex shader et le nuanceur de pixels (Remarque : les nuanceurs de pixels sont souvent également appelés nuanceurs de fragments)

    ![Opérations de nuanceur standard Unity](images/unity-standard-shader-compilation.png)

#### <a name="optmize-pixel-shaders"></a>Nuanceurs de pixels Optmize

Si vous examinez les résultats des statistiques compilées à l’aide de la méthode ci-dessus, le [nuanceur de fragments](https://en.wikipedia.org/wiki/Shader#Pixel_shaders) exécutera généralement plus d’opérations que le [nuanceur de sommets](https://en.wikipedia.org/wiki/Shader#Vertex_shaders) en moyenne. Le nuanceur de fragments, également connu sous le nom de nuanceur de pixels, est exécuté par pixel sur la sortie de l’écran, tandis que le nuanceur de sommets est exécuté uniquement par sommet de tous les maillages dessinés à l’écran. 

Par conséquent, les nuanceurs de fragments ont plus d’instructions que les nuanceurs vertex en raison de tous les calculs d’éclairage, les nuanceurs de fragments sont presque toujours exécutés sur un jeu de données plus volumineux. Par exemple, si la sortie d’écran est une image de 2k Ko, le nuanceur de fragments peut être exécuté 2000 * 2000 = 4 millions fois. En cas de rendu de deux yeux, ce nombre est doublé puisqu’il y a deux écrans. Si une application de réalité mixte a plusieurs passes, des effets de la publication plein écran ou un rendu de plusieurs mailles sur le même pixel, ce nombre augmente considérablement. 

Par conséquent, la réduction du nombre d’opérations dans le nuanceur de fragments peut entraîner des gains de performances bien supérieurs par rapport aux optimisations dans le nuanceur de sommets.

#### <a name="unity-standard-shader-alternatives"></a>Alternatives de nuanceur standard Unity

Au lieu d’utiliser un rendu physique (PBR) ou un autre nuanceur de haute qualité, examinez l’utilisation d’un nuanceur plus performant et moins onéreux. La [boîte à outils de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity) fournit le [nuanceur standard MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_MRTKStandardShader.html) qui a été optimisé pour les projets de réalité mixte.

Unity fournit également un non éclairé, un sommet éclairé, une diffusion et d’autres options de nuanceur simplifiées qui sont nettement plus rapides par rapport au nuanceur standard Unity. Pour plus d’informations, consultez [utilisation et performances des nuanceurs intégrés](https://docs.unity3d.com/Manual/shader-Performance.html) .

#### <a name="shader-preloading"></a>Préchargement de nuanceur

Utilisez le *préchargement des nuanceurs* et d’autres astuces pour optimiser le [temps de chargement des nuanceurs](https://docs.unity3d.com/Manual/OptimizingShaderLoadTime.html). En particulier, le préchargement des nuanceurs signifie que vous ne verrez aucun crochet en raison de la compilation du nuanceur d’exécution.

### <a name="limit-overdraw"></a>Limiter le surdessin

Dans Unity, vous pouvez afficher le surdessin pour leur scène, en basculant sur le [**menu mode dessin**](https://docs.unity3d.com/Manual/ViewModes.html) dans l’angle supérieur gauche de la **vue scène** et en sélectionnant **surdraw**.

En règle générale, le surdessin peut être atténué en éliminant les objets à l’avance avant leur envoi au GPU. Unity fournit des détails sur l’implémentation de l' [élimination des occlusions](https://docs.unity3d.com/Manual/OcclusionCulling.html) pour son moteur.

## <a name="memory-recommendations"></a>Recommandations de mémoire

L’allocation de mémoire excessive & les opérations de désallocation peuvent avoir des effets négatifs sur votre application holographique, ce qui se traduit par des performances incohérentes, des trames figées et d’autres comportements nuisibles. Il est particulièrement important de comprendre les considérations relatives à la mémoire lors du développement dans Unity, car la gestion de la mémoire est contrôlée par le garbage collector.

#### <a name="garbage-collection"></a>Garbage collection

Les applications holographiques vont perdre le temps de calcul au garbage collector (GC) quand le GC est activé pour analyser les objets qui ne sont plus dans l’étendue lors de l’exécution et où leur mémoire doit être libérée pour pouvoir être réutilisée. Les allocations constantes et les désallocations requièrent généralement que le garbage collector s’exécute plus fréquemment, ce qui nuit aux performances et à l’expérience de l’utilisateur.

Unity a fourni une excellente page qui explique en détail comment le garbage collector fonctionne et des conseils pour écrire du code plus efficace en ce qui concerne la gestion de la mémoire.
- [Optimisation des garbage collection dans les jeux Unity](https://unity3d.com/learn/tutorials/topics/performance-optimization/optimizing-garbage-collection-unity-games?playlist=44069)

L’une des pratiques les plus courantes qui conduisent à une garbage collection excessive ne consiste pas à mettre en cache des références à des composants et des classes dans le développement Unity. Toutes les références doivent être capturées pendant Start () ou éveillé () et réutilisées dans des fonctions ultérieures telles que Update () ou LateUpdate ().

Autres conseils rapides :
- Utiliser la classe [StringBuilder](https://docs.microsoft.com/dotnet/api/system.text.stringbuilder?view=netframework-4.7.2) C# pour créer dynamiquement des chaînes complexes au moment de l’exécution
- Supprimer les appels à Debug. log () quand vous n’en avez plus besoin, car ils s’exécutent toujours dans toutes les versions de build d’une application
- Si votre application holographique requiert généralement beaucoup de mémoire, envisagez d’appeler [ _**System. gc. Collect ()**_ ](https://docs.microsoft.com/dotnet/api/system.gc.collect?view=netframework-4.7.2) pendant les phases de chargement, par exemple lors de la présentation d’un écran de chargement ou de transition.

#### <a name="object-pooling"></a>Mise en pool d’objets

Le mise en pool d’objets est une technique populaire pour réduire le coût des allocations continues & des désallocations d’objets. Pour ce faire, vous devez allouer un grand pool d’objets identiques et réutiliser les instances inactives de ce pool au lieu de générer et de détruire constamment des objets dans le temps. Les pools d’objets sont idéaux pour les composants réutilisables qui ont une durée de vie variable pendant une application.

- [Didacticiel de mise en pool d’objets dans Unity](https://unity3d.com/learn/tutorials/topics/scripting/object-pooling) 

## <a name="startup-performance"></a>Performances de démarrage

Vous devez envisager de démarrer votre application avec une plus petite scène, puis d’utiliser *[SceneManager. LoadSceneAsync](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.LoadSceneAsync.html)* pour charger le reste de la scène. Cela permet à votre application d’accéder à un État interactif aussi rapide que possible. N’oubliez pas qu’il peut y avoir un pic d’UC important pendant l’activation de la nouvelle scène et que tout contenu rendu peut être saccadé ou déposé. Pour contourner ce cas, vous pouvez affecter la valeur false à la propriété AsyncOperation. allowSceneActivation sur la scène en cours de chargement, attendre le chargement de la scène, effacer l’écran en noir, puis rétablir la valeur true pour terminer l’activation de la scène.

N’oubliez pas que pendant le chargement, l’écran de démarrage holographique s’affiche à l’attention de l’utilisateur.

## <a name="see-also"></a>Articles associés
- [Optimisation du rendu graphique dans les jeux Unity](https://unity3d.com/learn/tutorials/temas/performance-optimization/optimizing-graphics-rendering-unity-games?playlist=44069)
- [Optimisation des garbage collection dans les jeux Unity](https://unity3d.com/learn/tutorials/topics/performance-optimization/optimizing-garbage-collection-unity-games?playlist=44069)
- [Meilleures pratiques en matière de physique [Unity]](https://unity3d.com/learn/tutorials/topics/physics/physics-best-practices)
- [Optimisation des scripts [Unity]](https://docs.unity3d.com/Manual/MobileOptimizationPracticalScriptingOptimizations.html)
