---
title: Recommandations sur les performances pour Unity
description: Conseils propres à Unity pour améliorer les performances avec les applications de réalité mixte.
author: troy-ferrell
ms.author: trferrel
ms.date: 03/26/2019
ms.topic: article
keywords: graphiques, UC, GPU, rendu, garbage collection, Hololens
ms.localizationpriority: high
ms.openlocfilehash: 28f09986cdb8c562aedfc9deae7b0369214ebc05
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "81277567"
---
# <a name="performance-recommendations-for-unity"></a>Recommandations sur les performances pour Unity

Cet article s’appuie sur les [recommandations sur les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md) mais il se concentre sur des informations propres à l’environnement du moteur Unity.

## <a name="use-recommended-unity-project-settings"></a>Utiliser les paramètres de projet Unity recommandés

Pour optimiser les performances des applications de réalité mixte dans Unity, la première étape, et la plus importante, consiste à utiliser les [paramètres d’environnement recommandés pour Unity](recommended-settings-for-unity.md). Le contenu de cet article s’intéresse à certaines des configurations de scène les plus importantes pour créer des applications Mixed Reality performantes. Certains de ces paramètres recommandés sont également soulignés ci-après.

## <a name="how-to-profile-with-unity"></a>Comment profiler avec Unity

Unity est fourni avec le profileur intégré **[Unity Profiler](https://docs.unity3d.com/Manual/Profiler.html)** , qui constitue une ressource intéressante pour recueillir de précieux insights sur les performances de votre application. Bien qu’il soit possible d’exécuter le profileur dans l’éditeur, ces métriques ne représentent pas l’environnement d’exécution réel et vous devez donc en utiliser les résultats avec prudence. Nous vous recommandons de profiler à distance votre application pendant son exécution sur un appareil pour obtenir des insights plus précis et exploitables. De plus, le débogueur [Frame Debugger](https://docs.unity3d.com/Manual/FrameDebugger.html) de Unity est également un outil très puissant.

Unity fournit une documentation très dense sur les thèmes suivants :
1) Comment connecter [à distance le profileur Unity à des applications UWP](https://docs.unity3d.com/Manual/windowsstore-profiler.html)
2) Comment [diagnostiquer efficacement les problèmes de performances avec Unity Profiler](https://unity3d.com/learn/tutorials/temas/performance-optimization/diagnosing-performance-problems-using-profiler-window)

>[!NOTE]
> Une fois Unity Profiler connecté et après avoir ajouté le profileur GPU (consultez *Ajouter un profileur* dans le coin supérieur droit), vous pouvez voir le temps passé sur le processeur et le GPU respectivement au milieu du profileur. Ainsi, le développeur détermine approximativement et rapidement si son application est liée au processeur ou au GPU.
>
> ![Processeur et GPU Unity](images/unity-profiler-cpu-gpu.png)

## <a name="cpu-performance-recommendations"></a>Recommandations sur les performances de processeur

Le contenu ci-dessous couvre des pratiques liées aux performances de manière plus approfondie, en ciblant particulièrement le développement en C# avec Unity.

#### <a name="cache-references"></a>Mettre en cache les références

Une bonne pratique consiste à mettre en cache les références à tous les composants et GameObjects pertinents au moment de l’initialisation. Cela est dû au fait que les appels de fonction répétitifs, comme *[GetComponent\<T>()](https://docs.unity3d.com/ScriptReference/GameObject.GetComponent.html)* sont beaucoup plus coûteux en termes de mémoire pour stocker un pointeur. Cela s’applique également au très régulièrement utilisé [Camera.main](https://docs.unity3d.com/ScriptReference/Camera-main.html). En fait, *Camera.main* utilise simplement *[FindGameObjectsWithTag ()](https://docs.unity3d.com/ScriptReference/GameObject.FindGameObjectsWithTag.html)* , qui recherche de façon coûteuse dans votre graphe de scène un objet caméra portant l’étiquette *« MainCamera »* .

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
> Quand vous utilisez *[GetComponent()](https://docs.unity3d.com/ScriptReference/GameObject.GetComponent.html)* , il existe plusieurs surcharges différentes. Il est important de toujours utiliser les implémentations basées sur le type et jamais la surcharge de recherche basée sur la chaîne. Une recherche par chaîne dans votre scène est beaucoup plus coûteuse qu’une recherche par type. <br/>
> (Correct) Component GetComponent(Type type) <br/>
> (Correct) T GetComponent\<T>() <br/>
> (Mauvais) Component GetComponent(string)> <br/>

#### <a name="avoid-expensive-operations"></a>Éviter les opérations coûteuses

1) **Éviter l’utilisation de [LINQ](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/getting-started-with-linq)**

    Même si LINQ est très propre et facile à lire et à écrire, cette technologie nécessite généralement beaucoup plus de calcul et notamment plus d’allocation de mémoire que l’écriture manuelle de l’algorithme.

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

    Certaines API Unity, bien qu’utiles, peuvent s’avérer très onéreuses à exécuter. La plupart d’entre elles impliquent la recherche d’une liste de GameObjects correspondante dans l’ensemble de votre graphe de scène. Ces opérations peuvent généralement être évitées en mettant en cache les références ou en implémentant un composant de gestionnaire pour les GameObjects en question afin de suivre les références au moment de l’exécution.

        GameObject.SendMessage()
        GameObject.BroadcastMessage()
        UnityEngine.Object.Find()
        UnityEngine.Object.FindWithTag()
        UnityEngine.Object.FindObjectOfType()
        UnityEngine.Object.FindObjectsOfType()
        UnityEngine.Object.FindGameObjectsWithTag()
        UnityEngine.Object.FindGameObjectsWithTag()

>[!NOTE]
> *[SendMessage()](https://docs.unity3d.com/ScriptReference/GameObject.SendMessage.html)* et *[BroadcastMessage()](https://docs.unity3d.com/ScriptReference/GameObject.BroadcastMessage.html)* doivent être éliminés à tout prix. Ces fonctions peuvent être de l’ordre de 1 000 fois plus lentes que les appels de fonction directs.

3) **Attention à Boxing**

    [Boxing](https://docs.microsoft.com/dotnet/csharp/programming-guide/types/boxing-and-unboxing) est un concept fondamental du langage et runtime C#. Il s’agit du processus qui consiste à wrapper des variables de type valeur, comme char, int, bool, etc., dans des variables de type référence. Quand une variable de type valeur est « boxed », elle est wrappée à l’intérieur d’un System.Object qui est stocké sur le tas managé. Ainsi, de la mémoire est allouée et, quand elle est supprimée, elle doit être traitée par le garbage collector. Ces allocations et désallocations entraînent un coût pour les performances et, dans de nombreux scénarios, s’avèrent inutiles ou peuvent être facilement remplacées par une alternative moins coûteuse.

    L’une des formes les plus courantes de boxing en développement est l’utilisation de [types valeur Nullable](https://docs.microsoft.com//dotnet/csharp/programming-guide/nullable-types/). Il est courant de vouloir retourner Null pour un type valeur dans une fonction, notamment quand l’opération risque de ne pas réussir à obtenir la valeur. L’éventuel problème avec cette approche est que l’allocation se produit maintenant sur le tas et doit donc être récupérée par le garbage collector ultérieurement.

    **Exemple de boxing en C#**

    ```csharp
    // boolean value type is boxed into object boxedMyVar on the heap
    bool myVar = true;
    object boxedMyVar = myVar;
    ```

    **Exemple de boxing problématique par le biais de types valeur Nullable**

    Ce code illustre une classe de particule factice qu’il est possible de créer dans un projet Unity. Un appel à `TryGetSpeed()` entraîne l’allocation d’objets sur le tas qui devront être récupérés par le garbage collector ultérieurement. Cet exemple s’avère particulièrement problématique, car il peut y avoir plus de 1000 particules dans une scène, chacune étant demandée pour sa vitesse actuelle. Par conséquent, des milliers d’objets sont alloués et, donc, désalloués à chaque frame, ce qui diminue considérablement les performances. La réécriture de la fonction pour retourner une valeur négative comme -1 pour indiquer qu’un échec permet d’éviter ce problème et de conserver la mémoire sur la pile.

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

#### <a name="repeating-code-paths"></a>Chemins de code répétitifs

Toutes les fonctions de rappel Unity répétitives (c.-à-d. Update) exécutées plusieurs fois par seconde et/ou frame doivent être écrites très soigneusement. Toutes les opérations coûteuses ont ici un impact énorme et constant sur les performances.

1) **Fonctions de rappel vides**

    Bien que le code ci-dessous puisse vous paraître inoffensif si vous le laissez dans votre application, notamment parce que chaque script Unity s’initialise automatiquement avec ce bloc de code, ces rappels vides peuvent en fait devenir très coûteux. Unity fonctionne en alternance sur une limite de code non managé/managé, entre le code UnityEngine et votre code d’application. Le changement de contexte sur ce pont est assez onéreux, même s’il n’y a rien à exécuter. Cela devient particulièrement problématique si votre application comporte des centaines de GameObjects avec des composants qui ont des rappels Unity répétitifs vides.

    ```CS
    void Update()
    {
    }
    ```

>[!NOTE]
> Update() est la manifestation la plus courante de ce problème de performances, mais d’autres rappels Unity répétitifs, comme les suivants peuvent s’avérer aussi mauvais, si ce n’est pire : FixedUpdate(), LateUpdate(), OnPostRender", OnPreRender(), OnRenderImage(), etc. 

2) **Opérations dont l’exécution une fois par frame est à privilégier**

    Les API Unity suivantes sont des opérations courantes pour de nombreuses applications holographiques. Bien que cela ne soit pas toujours possible, les résultats de ces fonctions peuvent être bien souvent calculés une seule fois et les résultats réutilisés dans l’application pour une frame donné.

    a) Une bonne pratique consiste généralement à avoir une classe ou un service Singleton dédié(e) pour gérer votre Raycast de pointage du regard dans la scène, puis à réutiliser ce résultat dans tous les autres composants de scène, au lieu d’effectuer des opérations Raycast répétées et fondamentalement identiques. Bien entendu, certaines applications peuvent nécessiter des raycasts provenant de différentes origines ou de différents [LayerMasks](https://docs.unity3d.com/ScriptReference/LayerMask.html).

        UnityEngine.Physics.Raycast()
        UnityEngine.Physics.RaycastAll()

    b) Évitez les opérations GetComponent() dans les rappels Unity répétés comme Update() en [mettant en cache les références](#cache-references) dans Start() ou Awake().

        UnityEngine.Object.GetComponent()

    c) Une bonne pratique consiste à instancier tous les objets, si possible, lors de l’initialisation et à utiliser la [mise en pool d’objets](#object-pooling) pour recycler et réutiliser les GameObjects tout au long de l’exécution de votre application.

        UnityEngine.Object.Instantiate()

3) **Éviter les interfaces et les constructions virtuelles**

    L’invocation d’appels de fonction par le biais d’interfaces plutôt que d’objets directs ou l’appel de fonctions virtuelles peuvent souvent s’avérer beaucoup plus coûteux que l’utilisation de constructions directes ou d’appels de fonction directs. Si la fonction virtuelle ou interface n’est pas nécessaire, elle doit être supprimée. Toutefois, la baisse de performances dans ces approches est généralement plus intéressante si leur utilisation simplifie la collaboration pour le développement, la lisibilité du code et la maintenabilité du code.

    En règle générale, il est recommandé de ne pas marquer des champs et des fonctions comme virtuels, sauf s’il est clairement attendu que ce membre a besoin d’être remplacé. Une attention particulière doit être portée aux chemins de code à haute fréquence qui sont appelés de nombreuses fois par frame, ou même une seule fois par frame, comme une méthode `UpdateUI()`.

4) **Éviter de passer des structs par valeur**

    Contrairement aux classes, les structs sont des types valeur et quand ils sont passés directement à une fonction, leur contenu est copié dans une instance nouvellement créée. Cette copie augmente le coût du processeur, ainsi que la mémoire supplémentaire sur la pile. Pour les petits structs, l’effet est généralement très minime et donc acceptable. En revanche, pour les fonctions appelées à plusieurs reprises, chaque frame ainsi que les fonctions acceptant des grands structs, modifiez si possible la définition de fonction pour qu’elle passe par référence. [En savoir plus ici](https://docs.microsoft.com/dotnet/csharp/programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method)

#### <a name="miscellaneous"></a>Divers

1) **Physique**

    a) En règle générale, le moyen le plus simple d’améliorer la physique consiste à limiter le temps dédié à la physique ou le nombre d’itérations par seconde. Bien entendu, la précision de la simulation s’en retrouve réduite. Consultez [TimeManager](https://docs.unity3d.com/Manual/class-TimeManager.html) dans Unity.

    b) Le type des colliders dans Unity possède des caractéristiques de performances très différentes. Les colliders ci-dessous sont listés du plus performant au moins performant, de gauche à droite. Il est plus important d’éviter les Mesh Colliders, qui sont beaucoup plus onéreux que les colliders primitifs.

        Sphere < Capsule < Box <<< Mesh (Convex) < Mesh (non-Convex)

    Pour plus d’informations, consultez [Bonnes pratiques pour la physique dans Unity](https://unity3d.com/learn/tutorials/topics/physics/physics-best-practices).

2) **Animations**

    Désactivez les animations inactives en désactivant le composant Animator (la désactivation de l’objet jeu n’a pas le même effet). Évitez les modèles de conception où un animateur se trouve dans une boucle qui affecte une valeur à la même chose. Cette technique présente une surcharge considérable, sans effet sur l’application. [En savoir plus ici.](https://docs.unity3d.com/Manual/MecanimPeformanceandOptimization.html)

3) **Algorithmes complexes**

    Si votre application utilise des algorithmes complexes comme des cinématiques inverses, des recherches de chemins, etc., recherchez une approche plus simple ou ajustez les paramètres pertinents pour leurs performances.

## <a name="cpu-to-gpu-performance-recommendations"></a>Recommandations sur les performances de processeur à GPU

En règle générale, les performances de processeur à GPU diminuent jusqu’aux **appels de dessin** soumis à la carte graphique. Pour améliorer les performances, les appels de dessin doivent être stratégiquement **a) réduits** ou **b) restructurés** afin d’obtenir des résultats optimaux. Étant donné que les appels de dessin eux-mêmes sont gourmands en ressources, leur réduction réduira le travail global nécessaire. De plus, les changements d’état entre les appels de dessin nécessitent des étapes de validation et de traduction coûteuses dans le pilote graphique et, par conséquent, la restructuration des appels de dessin de votre application pour limiter les changements d’état (c.-à-d. les différents matériaux, etc.) peuvent améliorer les performances.

Unity dispose d’un excellent article qui donne une vue d’ensemble descriptive du traitement par lot des appels de dessin pour sa plateforme.
- [Traitement par lot des appels de dessin Unity](https://docs.unity3d.com/Manual/DrawCallBatching.html)

#### <a name="single-pass-instanced-rendering"></a>Rendu d’instance à passage unique

Le rendu d’instance à passage unique dans Unity permet de réduire les appels de dessin pour chaque œil à un seul appel de dessin instancié. En raison de la cohérence du cache entre deux appels de dessin, les performances sont également améliorées sur le GPU.

Pour activer cette fonctionnalité dans votre projet Unity
1)  Ouvrez **Player XR Settings** (accédez à **Edit** > **Project Settings** > **Player** > **XR Settings**).
2) Sélectionnez **Single Pass Instanced** dans le menu déroulant **Stereo Rendering Method** (la case **Virtual Reality Supported** doit être cochée).

Lisez les articles suivants sur Unity pour plus d’informations sur l’approche de ce rendu.
- [How to maximize AR and VR performance with advanced stereo rendering](https://blogs.unity3d.com/2017/11/21/how-to-maximize-ar-and-vr-performance-with-advanced-stereo-rendering/)
- [Single Pass Instancing](https://docs.unity3d.com/Manual/SinglePassInstancing.html) 

>[!NOTE]
> Un problème courant avec le rendu d’instance à passage unique se produit si les développeurs ont déjà des nuanceurs personnalisés existants non écrits pour l’instanciation. Une fois cette fonctionnalité activée, les développeurs peuvent remarquer que certains GameObjects ne sont rendus que dans un seul œil. Cela est dû au fait que les nuanceurs personnalisés associés n’ont pas les propriétés appropriées pour l’instanciation.
>
> Consultez [Single Pass Stereo Rendering for HoloLens](https://docs.unity3d.com/Manual/SinglePassStereoRenderingHoloLens.html) sur Unity pour savoir comment résoudre ce problème.

#### <a name="static-batching"></a>Traitement par lot statique

Unity est capable de traiter par lot de nombreux objets statiques pour réduire les appels de dessin au GPU. Le traitement par lot statique fonctionne pour la plupart des objets [Renderer](https://docs.unity3d.com/ScriptReference/Renderer.html) dans Unity qui **1) partagent le même matériau** et **2) sont tous marqués comme *statiques*** (sélectionnez un objet dans Unity et cochez la case en haut à droite de l’inspecteur). Les GameObjects marqués comme *statiques* ne peuvent pas être déplacés dans le runtime de votre application. Ainsi, le traitement par lot statique peut s’avérer difficile à exploiter sur HoloLens, où pratiquement tous les objets ont besoin d’être placés, déplacés, mis à l’échelle, etc. Pour les casques immersifs, le traitement par lot statique peut réduire considérablement les appels de dessin et donc améliorer les performances.

Pour plus d’informations, consultez *Traitement par lot statique* sous [Traitement par lot des appels de dessin dans Unity](https://docs.unity3d.com/Manual/DrawCallBatching.html).

#### <a name="dynamic-batching"></a>Traitement par lot dynamique

Étant donné qu’il est difficile de marquer des objets comme *statiques* pour le développement HoloLens, le traitement par lot dynamique peut s’avérer un excellent outil pour compenser cette fonctionnalité manquante. Bien entendu, il peut également s’avérer utile sur les casques immersifs. Toutefois, le traitement par lot dynamique dans Unity peut être difficile à activer car les GameObjects doivent **a) partager le même matériau** et **b) remplir une longue liste d’autres critères**.

Lisez *Traitement par lot dynamique* sous [Traitement par lot des appels de dessin dans Unity](https://docs.unity3d.com/Manual/DrawCallBatching.html) pour obtenir la liste complète. En règle générale, les GameObjects deviennent non valides pour le traitement par lot dynamique, car les données de maillage associées ne peuvent pas dépasser 300 vertex.

#### <a name="other-techniques"></a>Autres techniques

Le traitement par lot ne peut se produire que si plusieurs GameObjects sont en mesure de partager le même matériau. En règle générale, il est bloqué par la nécessité pour les GameObjects d’avoir une texture unique pour leur matériau respectif. Il est courant de combiner des textures en une seule texture globale, une méthode appelée [création d’un atlas de textures](https://en.wikipedia.org/wiki/Texture_atlas).

En outre, il est généralement préférable de combiner les maillages en un seul GameObject, lorsque cela est possible et raisonnable. Chaque convertisseur dans Unity a ses appels de dessin associés au lieu d’envoyer un maillage combiné sous un seul convertisseur.

>[!NOTE]
> La modification des propriétés de Renderer.material au moment de l’exécution crée une copie du matériau et, par conséquent, interrompt éventuellement le traitement par lot. Utilisez Renderer.sharedMaterial pour modifier les propriétés des matériaux partagés entre les GameObjects.

## <a name="gpu-performance-recommendations"></a>Recommandations sur les performances de GPU

Découvrez-en plus sur l’[optimisation du rendu graphique dans Unity](https://unity3d.com/learn/tutorials/temas/performance-optimization/optimizing-graphics-rendering-unity-games).

### <a name="optimize-depth-buffer-sharing"></a>Optimiser le partage du tampon de profondeur

Il est généralement recommandé d’activer **Depth buffer sharing** sous **Player XR Settings** pour optimiser la [stabilité des hologrammes](Hologram-stability.md). En revanche, quand vous activez la reprojection au stade tardif basée sur la profondeur avec ce paramètre, il est recommandé de sélectionner le **format de profondeur 16 bits** au lieu du **format de profondeur 24 bits**. Les tampons de profondeur 16 bits réduisent considérablement la bande passante (et donc la puissance) associée au trafic du tampon de profondeur. Cela peut s’avérer avantageux à la fois en termes de réduction de puissance et d’amélioration des performances. Toutefois, il existe deux résultats négatifs possibles avec l’utilisation du *format de profondeur 16 bits*.

**Z-Fighting**

La fidélité à une plage de profondeur réduite rend le [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) plus susceptible de se produire avec 16 bits qu’avec 24 bits. Pour éviter ces artefacts, modifiez les plans de découpage proche/lointain de la [caméra Unity](https://docs.unity3d.com/Manual/class-Camera.html) pour tenir compte de cette moindre précision. Pour les applications HoloLens, un plan de découpage lointain de 50 m au lieu des 1 000 m par défaut de Unity peut en général éliminer tout z-fighting.

**Tampon de gabarit désactivé**

Quand Unity crée une [texture de rendu avec une profondeur de 16 bits](https://docs.unity3d.com/ScriptReference/RenderTexture-depth.html), aucun tampon de gabarit n’est créé. La sélection du format de profondeur 24 bits, conformément à la documentation Unity, va créer un tampon z-buffer de 24 bits, ainsi qu’un [tampon de gabarit de 8 bits] (https://docs.unity3d.com/Manual/SL-Stencil.html) (si 32 bits sont applicables sur un appareil, ce qui est généralement le cas, notamment pour HoloLens).

### <a name="avoid-full-screen-effects"></a>Éviter les effets plein écran

Les techniques qui fonctionnent en mode plein écran peuvent être assez coûteuses, car leur ordre de grandeur s’élève à des millions d’opérations pour chaque frame. Ainsi, il est recommandé d’éviter les [effets de post-traitement](https://docs.unity3d.com/Manual/PostProcessingOverview.html), comme l’anticrénelage, un écart des doigts paume vers le haut, etc.

### <a name="optimal-lighting-settings"></a>Paramètres d’éclairage optimaux

L’[illumination globale en temps réel](https://docs.unity3d.com/Manual/GIIntro.html) dans Unity peut donner des résultats visuels époustouflants, mais implique des calculs d’éclairage relativement coûteux. Il est recommandé de désactiver l’illumination globale en temps réel pour chaque fichier de scène Unity par le biais de **Window** > **Rendering** > **Lighting Settings** > Décochez **Real-time Global Illumination**.

En outre, il est recommandé de désactiver la projection d’ombres, car elle ajoute également des passes de GPU coûteuses à une scène Unity. Les ombres peuvent être désactivées par lumière, mais également contrôlées de façon holistique par le biais des paramètres de qualité.

Sélectionnez **Edit** > **Project Settings**, puis la catégorie **Quality** et **Low Quality** pour la plateforme UWP. Vous pouvez également affecter simplement à la propriété **Shadows** la valeur **Disable Shadows**.

### <a name="reduce-poly-count"></a>Réduire le nombre de polygones

Le nombre de polygones est généralement réduit par les opérations suivantes :
1) Suppression d’objets dans une scène
2) Décimation des ressources qui réduit le nombre de polygones pour un maillage donné
3) Implémentation d’un [système de niveau de détail (LOD)](https://docs.unity3d.com/Manual/LevelOfDetail.html) dans votre application qui restitue des objets lointains avec une version polygonale moindre de la même géométrie

### <a name="understanding-shaders-in-unity"></a>Présentation des nuanceurs dans Unity

Une approximation facile pour comparer les performances des nuanceurs consiste à identifier le nombre moyen d’opérations que chacun exécute au moment de l’exécution. Cette opération est simple dans Unity.

1) Sélectionnez votre ressource de nuanceur ou sélectionnez un matériau, puis dans le coin supérieur droit de la fenêtre de l’inspecteur, sélectionnez l’icône en forme d’engrenage, puis **« Select Shader »** .

    ![Select Shader dans Unity](images/Select-shader-unity.png)
2) Une fois la ressource de nuanceur sélectionnée, cliquez sur le bouton **« Compile and show code »** sous la fenêtre de l’inspecteur.

    ![Compile Shader Code dans Unity](images/compile-shader-code-unity.PNG)

3) Après la compilation, recherchez dans la section des statistiques des résultats le nombre d’opérations différentes pour le nuanceur de vertex et de pixels (remarque : les nuanceurs de pixels sont souvent également appelés nuanceurs de fragments).

    ![Opérations des nuanceurs standard Unity](images/unity-standard-shader-compilation.png)

#### <a name="optimize-pixel-shaders"></a>Optimiser les nuanceurs de pixels

En examinant les résultats des statistiques compilés à l’aide de la méthode ci-dessus, le [nuanceur de fragments](https://en.wikipedia.org/wiki/Shader#Pixel_shaders) exécute généralement plus d’opérations que le [nuanceur de vertex](https://en.wikipedia.org/wiki/Shader#Vertex_shaders), en moyenne. Le nuanceur de fragments, également connu sous le nom de nuanceur de pixels, est exécuté par pixel sur la sortie d’écran, tandis que le nuanceur de vertex est exécuté uniquement par vertex de tous les maillages dessinés à l’écran. 

Ainsi, non seulement les nuanceurs de fragments ont plus d’instructions que les nuanceurs de vertex en raison de tous les calculs d’éclairage, mais les nuanceurs de fragments sont aussi presque toujours exécutés sur un jeu de données plus volumineux. Par exemple, si la sortie d’écran est une image 2k par 2k, alors le nuanceur de fragments peut être exécuté 2 000 * 2 000 = 4 millions de fois. En cas de rendu de deux yeux, ce nombre double puisqu’il y a deux écrans. Si une application de réalité mixte a plusieurs passes, des effets de post-traitement plein écran ou un rendu de plusieurs maillages sur le même pixel, ce nombre augmente considérablement. 

Par conséquent, la réduction du nombre d’opérations dans le nuanceur de fragments peut entraîner des gains de performance bien supérieurs aux optimisations dans le nuanceur de vertex.

#### <a name="unity-standard-shader-alternatives"></a>Alternatives aux nuanceurs standard Unity

Au lieu d’utiliser un rendu physique ou un autre nuanceur haute qualité, envisagez d’utiliser un nuanceur plus performant et moins onéreux. [Mixed Reality Toolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity) fournit le [nuanceur standard MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_MRTKStandardShader.html) optimisé pour les projets de réalité mixte.

Unity fournit également des options de nuanceur simplifiées, comme l’absence d’éclairage, l’éclairage des vertex et la lumière diffuse, qui sont nettement plus rapides par rapport au nuanceur standard Unity. Pour plus d’informations, consultez [Utilisation et performances des nuanceurs intégrés](https://docs.unity3d.com/Manual/shader-Performance.html).

#### <a name="shader-preloading"></a>Préchargement des nuanceurs

Utilisez le *préchargement des nuanceurs* et d’autres astuces pour optimiser le [temps de chargement des nuanceurs](https://docs.unity3d.com/Manual/OptimizingShaderLoadTime.html). Plus particulièrement, le préchargement des nuanceurs signifie que vous ne rencontrerez aucune anicroche en raison de la compilation des nuanceurs au moment de l’exécution.

### <a name="limit-overdraw"></a>Limiter le surdessin

Dans Unity, vous pouvez afficher le surdessin pour votre scène, en utilisant le [**menu du mode dessin**](https://docs.unity3d.com/Manual/ViewModes.html) dans le coin supérieur gauche de la **vue de la scène** et en sélectionnant **Overdraw**.

En règle générale, le surdessin peut être atténué en éliminant les objets à l’avance avant leur envoi au GPU. Unity fournit des détails sur l’implémentation de l’[élimination des occlusions](https://docs.unity3d.com/Manual/OcclusionCulling.html) pour son moteur.

## <a name="memory-recommendations"></a>Recommandations sur la mémoire

Les opérations d’allocation et de désallocation de mémoire excessives peuvent avoir des effets négatifs sur votre application holographique, entraînant des performances irrégulières, des frames figées et d’autres comportements néfastes. Il est particulièrement important de bien comprendre les considérations relatives à la mémoire pour développer dans Unity, car la gestion de la mémoire est contrôlée par le garbage collector.

#### <a name="garbage-collection"></a>Garbage collection

Les applications holographiques perdent du temps de calcul de traitement dans le garbage collector (GC) quand le GC est activé pour analyser des objets qui ne sont plus dans la portée pendant l’exécution et quand leur mémoire doit être libérée, de sorte à être rendue disponible à des fins de réutilisation. Les allocations et désallocations constantes nécessitent généralement que le garbage collector s’exécute plus fréquemment, ce qui nuit aux performances et à l’expérience utilisateur.

Unity propose une excellente page qui explique précisément comment le garbage collector fonctionne et donne des conseils pour écrire du code plus efficace en termes de gestion de la mémoire.
- [Optimisation de garbage collection dans les jeux Unity](https://unity3d.com/learn/tutorials/topics/performance-optimization/optimizing-garbage-collection-unity-games?playlist=44069)

L’une des pratiques les plus courantes qui conduisent à un garbage collection excessif consiste à ne pas mettre en cache les références aux composants et aux classes dans le développement Unity. Toutes les références doivent être capturées pendant Start() ou Awake() et réutilisées dans des fonctions ultérieures comme Update() ou LateUpdate().

Autres conseils rapides :
- Utilisez la classe C# [StringBuilder](https://docs.microsoft.com/dotnet/api/system.text.stringbuilder?view=netframework-4.7.2) pour créer dynamiquement des chaînes complexes au moment de l’exécution.
- Supprimez les appels à Debug.log() quand vous n’en avez plus besoin, car ils s’exécutent encore dans toutes les versions de build d’une application.
- Si votre application holographique nécessite généralement beaucoup de mémoire, envisagez d’appeler [ _**System.GC.Collect()**_ ](https://docs.microsoft.com/dotnet/api/system.gc.collect?view=netframework-4.7.2) pendant les phases de chargement, par exemple lors de la présentation d’un écran de chargement ou de transition.

#### <a name="object-pooling"></a>Mise en pool d’objets

Le mise en pool d’objets est une technique connue pour réduire le coût des allocations et désallocations continues d’objets. Pour la réaliser, vous devez allouer un grand pool d’objets identiques et réutiliser des instances inactives disponibles de ce pool au lieu de générer et détruire constamment des objets au fil du temps. Les pools d’objets conviennent parfaitement aux composants réutilisables qui ont une durée de vie variable pendant une application.

- [Tutoriel sur la mise en pool d’objets dans Unity](https://unity3d.com/learn/tutorials/topics/scripting/object-pooling) 

## <a name="startup-performance"></a>Performances de démarrage

Vous devez envisager de démarrer votre application avec une scène plus petite, puis d’utiliser *[SceneManager.LoadSceneAsync](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.LoadSceneAsync.html)* pour charger le reste de la scène. Cela permet à votre application d’accéder à un état interactif aussi rapidement que possible. N’oubliez pas qu’il peut y avoir un pic consommation de processeur important pendant l’activation de la nouvelle scène et que tout contenu rendu peut être saccadé ou figé. Pour contourner ce problème, vous pouvez affecter à la propriété AsyncOperation.allowSceneActivation la valeur « false » sur la scène en cours de chargement, attendre que la scène se charge, effacer l’écran de sorte à ce qu’il soit noir, puis affecter la valeur « true » pour terminer l’activation de la scène.

N’oubliez pas que pendant le chargement de la scène de démarrage, l’écran de démarrage holographique est présenté à l’utilisateur.

## <a name="see-also"></a>Voir aussi
- [Optimisation du rendu graphique dans les jeux Unity](https://unity3d.com/learn/tutorials/temas/performance-optimization/optimizing-graphics-rendering-unity-games?playlist=44069)
- [Optimisation de garbage collection dans les jeux Unity](https://unity3d.com/learn/tutorials/topics/performance-optimization/optimizing-garbage-collection-unity-games?playlist=44069)
- [Bonnes pratiques pour la physique [Unity]](https://unity3d.com/learn/tutorials/topics/physics/physics-best-practices)
- [Optimisation des scripts [Unity]](https://docs.unity3d.com/Manual/MobileOptimizationPracticalScriptingOptimizations.html)
