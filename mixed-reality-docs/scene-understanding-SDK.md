---
title: Scène Understanding SDK
description: Guide de programmation du SDK Scene Understanding
author: szymons
ms.author: szymons
ms.date: 07/08/2019
ms.topic: article
keywords: Compréhension des scènes, mappage spatial, Windows Mixed Reality, Unity
ms.openlocfilehash: f293e779b041cdf4aa636cf317b7eaca70e16410
ms.sourcegitcommit: 37816514b8fe20669c487774b86e80ec08edcadf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/09/2020
ms.locfileid: "81003325"
---
# <a name="scene-understanding-sdk-overview"></a><span data-ttu-id="0ddd6-104">Présentation du SDK présentation de Scene</span><span class="sxs-lookup"><span data-stu-id="0ddd6-104">Scene understanding SDK overview</span></span>

<span data-ttu-id="0ddd6-105">L’objectif de la compréhension des scènes est de transformer les données de capteur d’environnement non structurées capturées par votre appareil de réalité mixte et de le convertir en une représentation puissante mais abstraite, intuitive et facile à développer pour.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-105">The goal of Scene understanding is to transform the un-structured environment sensor data that your Mixed Reality device captures and to convert it into a powerful but abstracted representation that is intuitive and easy to develop for.</span></span> <span data-ttu-id="0ddd6-106">Le kit de développement logiciel (SDK) joue le rôle de couche de communication entre votre application et le runtime Understanding.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-106">The SDK acts as the communication layer between your application and the Scene Understanding runtime.</span></span> <span data-ttu-id="0ddd6-107">Elle est destinée à imiter les constructions standard existantes, telles que les graphiques de scène 3D pour les représentations 3D et les rectangles 2D et les panneaux pour les applications 2D.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-107">It's aimed to mimic existing standard constructs such as 3D scene graphs for 3D representations and 2D rectangles and panels for 2D applications.</span></span> <span data-ttu-id="0ddd6-108">Tandis que la construction de scènes comprenant les imitations sera mappée aux frameworks concrets que vous pouvez utiliser, en général SceneUnderstanding est une infrastructure agnostique qui autorise l’interopérabilité entre des frameworks variés qui interagissent avec elle.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-108">While the constructs Scene Understanding mimics will map to concrete frameworks you may use, in general SceneUnderstanding is framework agnostic allowing for interop between varied frameworks that interact with it.</span></span> <span data-ttu-id="0ddd6-109">À mesure que la compréhension de la scène évolue, le rôle du kit de développement logiciel (SDK) consiste à s’assurer que de nouvelles représentations et fonctionnalités continuent à être exposées au sein d’une infrastructure unifiée.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-109">As Scene Understanding evolves the role of the SDK is to ensure new representations and capabilities continue to be exposed within a unified framework.</span></span> <span data-ttu-id="0ddd6-110">Dans ce document, nous allons commencer par introduire des concepts de haut niveau qui vous aideront à vous familiariser avec l’environnement de développement/l’utilisation, puis à fournir une documentation plus détaillée pour des classes et des constructions spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-110">In this document we will first introduce high level concepts that will help you get familiar with the development environment/usage and then provide more detailed documentation for specific classes and constructs.</span></span>

## <a name="where-do-i-get-the-sdk"></a><span data-ttu-id="0ddd6-111">Où puis-je me procurer le kit de développement logiciel ?</span><span class="sxs-lookup"><span data-stu-id="0ddd6-111">Where do I get the SDK?</span></span>

<span data-ttu-id="0ddd6-112">Le kit de développement logiciel (SDK) SceneUnderstanding peut être téléchargé via NuGet.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-112">The SceneUnderstanding SDK is downloadable via NuGet.</span></span>

[<span data-ttu-id="0ddd6-113">SDK SceneUnderstanding</span><span class="sxs-lookup"><span data-stu-id="0ddd6-113">SceneUnderstanding SDK</span></span>](https://www.nuget.org/packages/Microsoft.MixedReality.SceneUnderstanding/)

<span data-ttu-id="0ddd6-114">**Remarque :** la version la plus récente dépend des packages de préversion et vous devrez activer les packages de préversions pour les afficher.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-114">**Note:** the latest release depends on preview packages and you will need to enable pre-release packages to see it.</span></span>

<span data-ttu-id="0ddd6-115">Depuis la version 0.5.2022-RC, Scene Understanding prend en charge les C# projections de langage pour et C++ permettant aux applications de développer des applications pour les plateformes Win32 ou UWP.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-115">As of version 0.5.2022-rc, Scene Understanding supports language projections for C# and C++ allowing applications to develop applications for Win32 or UWP platforms.</span></span> <span data-ttu-id="0ddd6-116">À compter de cette version, SceneUnderstanding prend en charge Unity dans le cadre de la prise en charge de l’éditeur, avec la SceneObserver qui est utilisée uniquement pour communiquer avec HoloLens2.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-116">As of this version, SceneUnderstanding supports unity in-editor support barring the SceneObserver which is used solely for communicating with HoloLens2.</span></span> 

<span data-ttu-id="0ddd6-117">SceneUnderstanding requiert SDK Windows version 18362 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-117">SceneUnderstanding requires Windows SDK version 18362 or higher.</span></span> 

<span data-ttu-id="0ddd6-118">Si vous utilisez le kit de développement logiciel (SDK) dans un projet Unity, utilisez [NuGet pour Unity](https://github.com/GlitchEnzo/NuGetForUnity) pour installer le package dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-118">If you are using the SDK in a Unity project, please use [NuGet for Unity](https://github.com/GlitchEnzo/NuGetForUnity) to install the package into your project.</span></span>

## <a name="conceptual-overview"></a><span data-ttu-id="0ddd6-119">Vue d'ensemble conceptuelle</span><span class="sxs-lookup"><span data-stu-id="0ddd6-119">Conceptual Overview</span></span>

### <a name="the-scene"></a><span data-ttu-id="0ddd6-120">La scène</span><span class="sxs-lookup"><span data-stu-id="0ddd6-120">The Scene</span></span>

<span data-ttu-id="0ddd6-121">Votre appareil de réalité mixte intègre constamment des informations sur ce qu’il voit dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-121">Your mixed reality device is constantly integrating information about what it sees in your environment.</span></span> <span data-ttu-id="0ddd6-122">La compréhension de la scène entonnoir toutes ces sources de données et produit une seule abstraction cohésive.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-122">Scene Understanding funnels all of these data sources and produces one single cohesive abstraction.</span></span> <span data-ttu-id="0ddd6-123">La compréhension des scènes génère des scènes qui constituent une composition de [SceneObjects](scene-understanding-SDK.md#sceneobjects) représentant une instance d’une seule chose (par exemple, un mur/un plafond/étage). Les objets de scène sont eux-mêmes une composition de [SceneComponents](scene-understanding-SDK.md#scenecomponents) qui représentent des éléments plus granulaires qui composent ce SceneObject.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-123">Scene Understanding generates Scenes which are a composition of [SceneObjects](scene-understanding-SDK.md#sceneobjects) that represent an instance of a single thing, (e.g. a wall/ceiling/floor.) Scene Objects themselves are a composition of [SceneComponents](scene-understanding-SDK.md#scenecomponents) which represent more granular pieces that make up this SceneObject.</span></span> <span data-ttu-id="0ddd6-124">Les exemples de composants sont les quadruples et les maillages, mais à l’avenir, ils pourraient représenter des zones englobantes, des maillages de collision, des métadonnées, etc.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-124">Examples of components are quads and meshes, but in the future could represent bounding boxes, collision meshes, metadata etc...</span></span>

<span data-ttu-id="0ddd6-125">Le processus de conversion des données de capteur brutes en scène est une opération potentiellement coûteuse qui peut prendre des secondes pour les espaces moyens (~ 10x10m) à des minutes pour les espaces de très grande taille (~ 50x50m). par conséquent, il ne s’agit pas d’un objet qui est calculé par l’appareil sans demande d’application.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-125">The process of converting the raw sensor data into a Scene is a potentially expensive operation that could take seconds for medium spaces (~10x10m) to minutes for very large spaces (~50x50m) and therefore it is not something that is being computed by the device without application request.</span></span> <span data-ttu-id="0ddd6-126">Au lieu de cela, la génération de scènes est déclenchée par votre application à la demande.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-126">Instead, Scene generation is triggered by your application on demand.</span></span> <span data-ttu-id="0ddd6-127">La classe SceneObserver a des méthodes statiques qui peuvent calculer ou désérialiser une scène, que vous pouvez ensuite énumérer/interagir avec.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-127">The SceneObserver class has static methods that can Compute or Deserialize a scene, which you can then enumerate/interact with.</span></span> <span data-ttu-id="0ddd6-128">L’action « Compute » est exécutée à la demande et s’exécute sur l’UC, mais dans un processus séparé (le pilote de réalité mixte).</span><span class="sxs-lookup"><span data-stu-id="0ddd6-128">The "Compute" action is executed on-demand and executes on the CPU but in a separate process (the Mixed Reality Driver).</span></span> <span data-ttu-id="0ddd6-129">Toutefois, pendant que nous effectuons le calcul dans un autre processus, les données de scène obtenues sont stockées et conservées dans votre application dans l’objet de scène.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-129">However, while we do compute in another process the resulting Scene data is stored and maintained in your application in the Scene object.</span></span> 

<span data-ttu-id="0ddd6-130">Vous trouverez ci-dessous un diagramme qui illustre ce processus et montre des exemples de deux applications interagissant avec le runtime de la vision de la scène.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-130">Below is a diagram that illustrates this process flow and shows examples of two applications interfacing with the Scene Understanding runtime.</span></span> 

![Diagramme de processus](images/SU-ProcessFlow.png)

<span data-ttu-id="0ddd6-132">La partie gauche est un diagramme du runtime de réalité mixte qui est toujours actif et s’exécute dans son propre processus.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-132">On the left hand side is a diagram of the mixed reality runtime which is always on and running in its own process.</span></span> <span data-ttu-id="0ddd6-133">Ce Runtime est chargé d’effectuer le suivi des appareils, le mappage spatial et d’autres opérations que la présentation de Scene utilise pour comprendre et expliquer le monde autour de vous.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-133">This runtime is responsible for performing device tracking, spatial mapping, and other operations that Scene Understanding uses to understand and reason about the world around you.</span></span> <span data-ttu-id="0ddd6-134">Sur le côté droit du diagramme, nous présentons deux applications théoriques qui utilisent la compréhension des scènes.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-134">On the right side of the diagram, we show two theoretical applications that make use of Scene Understanding.</span></span> <span data-ttu-id="0ddd6-135">La première application interface avec MRTK, qui utilise le kit de développement logiciel (SDK) de scène en interne, la deuxième application calcule et utilise deux instances de scène distinctes.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-135">The first application interfaces with MRTK which uses the Scene Understanding SDK internally, the second app computes and uses two separate scene instances.</span></span> <span data-ttu-id="0ddd6-136">Les trois scènes dans ce diagramme génèrent des instances distinctes des scènes, le pilote ne suit pas l’état global qui est partagé entre les applications et les objets de scène dans une scène ne sont pas trouvés dans un autre.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-136">All 3 Scenes in this diagram generate distinct instances of the scenes, the driver is not tracking global state that is shared between applications and Scene Objects in one scene are not found in another.</span></span> <span data-ttu-id="0ddd6-137">La compréhension de la scène fournit un mécanisme de suivi au fil du temps, mais cette opération s’effectue à l’aide du kit de développement logiciel (SDK) et le code qui effectue ce suivi s’exécute dans le kit de développement logiciel (SDK) dans le processus de votre application.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-137">Scene Understanding does provide a mechanism to track over time, but this is done using the SDK and the code that performs this tracking is running in the SDK in your app's process.</span></span>

<span data-ttu-id="0ddd6-138">Étant donné que chaque scène stocke ses données dans l’espace mémoire de votre application, vous pouvez supposer que toutes les fonctions de l’objet de la scène ou de ses données internes sont toujours exécutées dans le processus de votre application.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-138">Because each Scene stores it's data in your application's memory space, you can assume that all function of the Scene object or it's internal data is always executed in your application's process.</span></span>

### <a name="layout"></a><span data-ttu-id="0ddd6-139">Disposition</span><span class="sxs-lookup"><span data-stu-id="0ddd6-139">Layout</span></span>

<span data-ttu-id="0ddd6-140">Pour travailler avec la compréhension des scènes, il peut être utile de savoir et de comprendre comment le runtime représente des composants logiquement et physiquement.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-140">To work with Scene Understanding it may be valuable to know and understand how the runtime represents components logically and physically.</span></span> <span data-ttu-id="0ddd6-141">La scène représente des données avec une disposition spécifique qui a été choisie comme simple tout en conservant une structure sous-jacente qui est pliable pour répondre aux exigences futures sans avoir besoin de révisions majeures.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-141">The Scene represents data with a specific layout that was chosen to be simple while maintaining an underlying structure that is pliable to meet future requirements without needing major revisions.</span></span> <span data-ttu-id="0ddd6-142">Pour ce faire, la scène stocke tous les composants (blocs de construction pour tous les objets de scène) dans une liste plate et définit la hiérarchie et la composition par le biais de références où des composants spécifiques référencent d’autres.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-142">The Scene does this by storing all Components (building blocks for all Scene Objects) in a flat list and defining hierarchy and composition through references where specific components reference others.</span></span>

<span data-ttu-id="0ddd6-143">Ci-dessous, nous présentons un exemple de structure dans sa forme plate et logique.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-143">Below we present an example of a structure in both its flat and logical form.</span></span>

<table>
<tr><th><span data-ttu-id="0ddd6-144">Disposition logique</span><span class="sxs-lookup"><span data-stu-id="0ddd6-144">Logical Layout</span></span></th><th><span data-ttu-id="0ddd6-145">Disposition physique</span><span class="sxs-lookup"><span data-stu-id="0ddd6-145">Physical Layout</span></span></th></tr>
<tr>
<td>
<ul>
  <span data-ttu-id="0ddd6-146">Scene</span><span class="sxs-lookup"><span data-stu-id="0ddd6-146">Scene</span></span>
  <ul>
  <li><span data-ttu-id="0ddd6-147">SceneObject_1</span><span class="sxs-lookup"><span data-stu-id="0ddd6-147">SceneObject_1</span></span>
    <ul>
      <li><span data-ttu-id="0ddd6-148">SceneMesh_1</span><span class="sxs-lookup"><span data-stu-id="0ddd6-148">SceneMesh_1</span></span></li>
      <li><span data-ttu-id="0ddd6-149">SceneQuad_1</span><span class="sxs-lookup"><span data-stu-id="0ddd6-149">SceneQuad_1</span></span></li>
      <li><span data-ttu-id="0ddd6-150">SceneQuad_2</span><span class="sxs-lookup"><span data-stu-id="0ddd6-150">SceneQuad_2</span></span></li>
    </ul>
  </li>
  <li><span data-ttu-id="0ddd6-151">SceneObject_2</span><span class="sxs-lookup"><span data-stu-id="0ddd6-151">SceneObject_2</span></span>
    <ul>
      <li><span data-ttu-id="0ddd6-152">SceneQuad_1</span><span class="sxs-lookup"><span data-stu-id="0ddd6-152">SceneQuad_1</span></span></li>
      <li><span data-ttu-id="0ddd6-153">SceneQuad_3</span><span class="sxs-lookup"><span data-stu-id="0ddd6-153">SceneQuad_3</span></span></li>
      </li></ul>
  </li>
  <li><span data-ttu-id="0ddd6-154">SceneObject_3</span><span class="sxs-lookup"><span data-stu-id="0ddd6-154">SceneObject_3</span></span>
    <ul>
      <li><span data-ttu-id="0ddd6-155">SceneMesh_3</span><span class="sxs-lookup"><span data-stu-id="0ddd6-155">SceneMesh_3</span></span></li>
    </ul>
  </ul>
</ul>
</td>
<td>
<ul>
  <li><span data-ttu-id="0ddd6-156">SceneObject_1</span><span class="sxs-lookup"><span data-stu-id="0ddd6-156">SceneObject_1</span></span></li>
  <li><span data-ttu-id="0ddd6-157">SceneObject_2</span><span class="sxs-lookup"><span data-stu-id="0ddd6-157">SceneObject_2</span></span></li>
  <li><span data-ttu-id="0ddd6-158">SceneObject_3</span><span class="sxs-lookup"><span data-stu-id="0ddd6-158">SceneObject_3</span></span></li>
  <li><span data-ttu-id="0ddd6-159">SceneQuad_1</span><span class="sxs-lookup"><span data-stu-id="0ddd6-159">SceneQuad_1</span></span></li>
  <li><span data-ttu-id="0ddd6-160">SceneQuad_2</span><span class="sxs-lookup"><span data-stu-id="0ddd6-160">SceneQuad_2</span></span></li>
  <li><span data-ttu-id="0ddd6-161">SceneQuad_3</span><span class="sxs-lookup"><span data-stu-id="0ddd6-161">SceneQuad_3</span></span></li>
  <li><span data-ttu-id="0ddd6-162">SceneMesh_1</span><span class="sxs-lookup"><span data-stu-id="0ddd6-162">SceneMesh_1</span></span></li>
  <li><span data-ttu-id="0ddd6-163">SceneMesh_2</span><span class="sxs-lookup"><span data-stu-id="0ddd6-163">SceneMesh_2</span></span></li>
</ul>
</td>
</tr>
</table>

<span data-ttu-id="0ddd6-164">Cette illustration met en évidence la différence entre la disposition physique et logique de la scène.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-164">This illustration highlights the difference between the physical and logical layout of the Scene.</span></span> <span data-ttu-id="0ddd6-165">À gauche, nous voyons la disposition hiérarchique des données que votre application voit lors de l’énumération de la scène.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-165">On the left we see the hierarchical layout of the data that your application sees when enumerating the scene.</span></span> <span data-ttu-id="0ddd6-166">À droite, nous voyons que la scène est en fait composée de 12 composants distincts qui sont accessibles individuellement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-166">On the right we see that the scene is actually comprised of 12 distinct components that are accessible individually if necessary.</span></span> <span data-ttu-id="0ddd6-167">Lors du traitement d’une nouvelle scène, nous pensons que les applications parcourent cette hiérarchie logiquement, toutefois, lors du suivi entre les mises à jour de la scène, certaines applications peuvent uniquement être intéressées à cibler des composants spécifiques qui sont partagés entre deux scènes.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-167">When processing a new scene, we expect applications to walk this hierarchy logically, however when tracking between scene updates, some applications may only be interested in targeting specific components that are shared between two scenes.</span></span>

## <a name="api-overview"></a><span data-ttu-id="0ddd6-168">Vue d’ensemble des API</span><span class="sxs-lookup"><span data-stu-id="0ddd6-168">API overview</span></span>

<span data-ttu-id="0ddd6-169">La section suivante fournit une vue d’ensemble des constructions de la présentation des scènes.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-169">The following section provides a high-level overview of the constructs in Scene Understanding.</span></span> <span data-ttu-id="0ddd6-170">La lecture de cette section vous donne une idée de la façon dont les scènes sont représentées, ainsi que de l’utilisation des différents composants.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-170">Reading this section will give you an  understanding of how scenes are represented, and what the various components do/are used for.</span></span> <span data-ttu-id="0ddd6-171">La section suivante fournit des exemples de code concrets et des détails supplémentaires qui sont brillants dans cette vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-171">The next section will provide concrete code examples and additional details that are glossed over in this overview.</span></span>

<span data-ttu-id="0ddd6-172">Tous les types décrits ci-dessous résident dans l’espace de noms `Microsoft.MixedReality.SceneUnderstanding`.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-172">All of the types described below reside in the `Microsoft.MixedReality.SceneUnderstanding` namespace.</span></span>

### <a name="scenecomponents"></a><span data-ttu-id="0ddd6-173">SceneComponents</span><span class="sxs-lookup"><span data-stu-id="0ddd6-173">SceneComponents</span></span>

<span data-ttu-id="0ddd6-174">Maintenant que vous comprenez la disposition logique des scènes, nous pouvons maintenant présenter le concept de SceneComponents et la façon dont ils sont utilisés pour composer la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-174">Now that you understand the logical layout of scenes we can now present the concept of SceneComponents and how they are used to compose hierarchy.</span></span> <span data-ttu-id="0ddd6-175">SceneComponents sont les décompositions les plus granulaires de SceneUnderstanding qui représentent une seule base, par exemple une maille ou un quadruple-Box ou un cadre englobant.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-175">SceneComponents are the most granular decompositions in SceneUnderstanding representing a single core thing, e.g. a mesh or a quad or a bounding box.</span></span> <span data-ttu-id="0ddd6-176">Les SceneComponents sont des éléments qui peuvent être mis à jour de manière indépendante et peuvent être référencés par d’autres SceneComponents, de sorte qu’ils disposent d’un ID unique de propriété globale unique, qui autorise ce type de mécanisme de suivi/référencement.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-176">SceneComponents are things that can update independently and can be referenced by other SceneComponents, hence they have a single global property a unique Id, that allow for this type of tracking/referencing mechanism.</span></span> <span data-ttu-id="0ddd6-177">Les ID sont utilisés pour la composition logique de la hiérarchie des scènes, ainsi que pour la persistance des objets (opération consistant à mettre à jour une scène par rapport à une autre.)</span><span class="sxs-lookup"><span data-stu-id="0ddd6-177">Ids are used for the logical composition of scene hierarchy as well as object persistence (the act of updating one scene relative to another.)</span></span> 

<span data-ttu-id="0ddd6-178">Si vous traitez toutes les scènes nouvellement calculées comme étant distinctes et que vous énumérez simplement toutes les données qu’elle contient, les ID sont en grande partie transparents pour vous.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-178">If you are treating every newly computed scene as being distinct, and simply enumerating all data within it then Ids are largely transparent to you.</span></span> <span data-ttu-id="0ddd6-179">Toutefois, si vous envisagez de suivre des composants sur plusieurs mises à jour, vous allez utiliser les ID pour indexer et Rechercher des SceneComponents entre les objets de scène.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-179">However, if you are planning to track components over several updates you will use the Ids to index and find SceneComponents between Scene objects.</span></span>

### <a name="sceneobjects"></a><span data-ttu-id="0ddd6-180">SceneObjects</span><span class="sxs-lookup"><span data-stu-id="0ddd6-180">SceneObjects</span></span>

<span data-ttu-id="0ddd6-181">Un SceneObject est un SceneComponent qui représente une instance d’un « élément », par exemple un mur, un étage, un plafond, etc. exprimé par leur propriété Kind.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-181">A SceneObject is a SceneComponent that represents an instance of a "thing" e.g. a wall, a floor, a ceiling, etc... expressed by their Kind property.</span></span> <span data-ttu-id="0ddd6-182">Les SceneObjects sont géométriques et, par conséquent, ont des fonctions et des propriétés qui représentent leur emplacement dans l’espace, mais elles ne contiennent pas de structure géométrique ou logique.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-182">SceneObjects are geometric, and therefore have functions and properties that represent their location in space, however they don't contain any geometric or logical structure.</span></span> <span data-ttu-id="0ddd6-183">Au lieu de cela, SceneObjects référence d’autres SceneComponents, en particulier SceneQuads et SceneMeshes, qui fournissent les représentations variées prises en charge par le système.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-183">Instead, SceneObjects reference other SceneComponents, specifically SceneQuads and SceneMeshes which provide the varied representations that are supported by the system.</span></span> <span data-ttu-id="0ddd6-184">Quand une nouvelle scène est calculée, votre application va probablement énumérer le SceneObjects de la scène pour traiter ce qui l’intéresse.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-184">When a new scene is computed, your application will most likely enumerate the Scene's SceneObjects to process what it's interested in.</span></span>

<span data-ttu-id="0ddd6-185">SceneObjects peut avoir l’un des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0ddd6-185">SceneObjects can have any one of the following:</span></span>

<table>
<tr>
<th><span data-ttu-id="0ddd6-186">SceneObjectKind</span><span class="sxs-lookup"><span data-stu-id="0ddd6-186">SceneObjectKind</span></span></th> <th><span data-ttu-id="0ddd6-187">Description</span><span class="sxs-lookup"><span data-stu-id="0ddd6-187">Description</span></span></th>
</tr>
<tr><td><span data-ttu-id="0ddd6-188">Arrière-plan</span><span class="sxs-lookup"><span data-stu-id="0ddd6-188">Background</span></span></td><td><span data-ttu-id="0ddd6-189">Le SceneObject est connu pour <b>ne pas</b> être l’un des autres types d’objets de scène reconnus.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-189">The SceneObject is known to be <b>not</b> one of the other recognized kinds of scene object.</span></span> <span data-ttu-id="0ddd6-190">Cette classe ne doit pas être confondue avec Unknown, où l’arrière-plan est connu comme étant un mur/plancher/plafond, etc... alors que inconnu n’est pas encore catégorisé.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-190">This class should not be confused with Unknown where Background is known not to be wall/floor/ceiling etc... while unknown is not yet categorized.</span></span></b></td></tr>
<tr><td><span data-ttu-id="0ddd6-191">Encastre</span><span class="sxs-lookup"><span data-stu-id="0ddd6-191">Wall</span></span></td><td><span data-ttu-id="0ddd6-192">Un mur physique.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-192">A physical wall.</span></span> <span data-ttu-id="0ddd6-193">Les murs sont supposés être des structures environnementales immobilières.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-193">Walls are assumed to be immovable environmental structures.</span></span></td></tr>
<tr><td><span data-ttu-id="0ddd6-194">Floor</span><span class="sxs-lookup"><span data-stu-id="0ddd6-194">Floor</span></span></td><td><span data-ttu-id="0ddd6-195">Les étages sont des surfaces sur lesquelles il est possible de parcourir.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-195">Floors are any surfaces on which one can walk.</span></span> <span data-ttu-id="0ddd6-196">Remarque : les escaliers ne sont pas des étages.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-196">Note: stairs are not floors.</span></span> <span data-ttu-id="0ddd6-197">Notez également que les étages supposent une surface pouvant être guidée et qu’il n’y a donc pas d’hypothèse explicite d’un étage singulier.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-197">Also note, that floors assume any walkable surface and therefore there is no explicit assumption of a singular floor.</span></span> <span data-ttu-id="0ddd6-198">Structures à plusieurs niveaux, rampes, etc... doit tous être classifiés en tant que plancher.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-198">Multi-level structures, ramps etc... should all classify as floor.</span></span></td></tr>
<tr><td><span data-ttu-id="0ddd6-199">Ceiling</span><span class="sxs-lookup"><span data-stu-id="0ddd6-199">Ceiling</span></span></td><td><span data-ttu-id="0ddd6-200">Surface supérieure d’une salle.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-200">The upper surface of a room.</span></span></td></tr>
<tr><td><span data-ttu-id="0ddd6-201">Plateforme</span><span class="sxs-lookup"><span data-stu-id="0ddd6-201">Platform</span></span></td><td><span data-ttu-id="0ddd6-202">Grande surface plate sur laquelle vous pouvez placer des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-202">A large flat surface on which you could place holograms.</span></span> <span data-ttu-id="0ddd6-203">Elles ont tendance à représenter des tables, des plans de plan et d’autres grandes surfaces horizontales.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-203">These tend to represent tables, countertops and other large horizontal surfaces.</span></span></td></tr>
<tr><td><span data-ttu-id="0ddd6-204">World</span><span class="sxs-lookup"><span data-stu-id="0ddd6-204">World</span></span></td><td><span data-ttu-id="0ddd6-205">Étiquette réservée pour les données géométriques indépendantes de l’étiquetage.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-205">A reserved label for geometric data that is agnostic to labeling.</span></span> <span data-ttu-id="0ddd6-206">La maille générée par la définition de l’indicateur de mise à jour EnableWorldMesh est classée comme monde.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-206">The mesh generated by setting the EnableWorldMesh update flag would be classified as world.</span></span></td></tr>
<tr><td><span data-ttu-id="0ddd6-207">Inconnu.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-207">Unknown</span></span></td><td><span data-ttu-id="0ddd6-208">Cet objet de scène n’a pas encore été classé et affecté un genre.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-208">This scene object has yet to be classified and assigned a kind.</span></span> <span data-ttu-id="0ddd6-209">Cela ne doit pas être confondu avec l’arrière-plan, car cet objet peut être n’importe quoi, le système n’a pas encore pu trouver une classification suffisamment importante pour l’informatique.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-209">This should not be confused with Background, as this object could be anything, the system has just not come up with a strong enough classification for it yet.</span></span></td></tr>
</tr>
</table>

### <a name="scenemesh"></a><span data-ttu-id="0ddd6-210">SceneMesh</span><span class="sxs-lookup"><span data-stu-id="0ddd6-210">SceneMesh</span></span>

<span data-ttu-id="0ddd6-211">Un SceneMesh est un SceneComponent qui se rapproche de la géométrie des objets géométriques arbitraires à l’aide d’une liste de triangles.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-211">A SceneMesh is a SceneComponent that approximates the geometry of arbitrary geometric objects using a triangle list.</span></span> <span data-ttu-id="0ddd6-212">Les SceneMeshes sont utilisés dans plusieurs contextes différents, ils peuvent représenter des composants de la structure de cellules étanches ou en tant que WorldMesh qui représente le maillage de mappage spatial non lié à la scène.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-212">SceneMeshes are used in several different contexts, they can represent components of the watertight cell structure or as the WorldMesh which represents the unbounded spatial mapping mesh associated with the Scene.</span></span> <span data-ttu-id="0ddd6-213">Les données d’index et de vertex fournies avec chaque maille utilisent la même disposition familière que les [mémoires tampons de vertex et d’index](https://msdn.microsoft.com/library/windows/desktop/bb147325%28v=vs.85%29.aspx) utilisées pour le rendu des maillages de triangle dans toutes les API de rendu modernes.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-213">The index and vertex data provided with each mesh uses the same familiar layout as the [vertex and index buffers](https://msdn.microsoft.com/library/windows/desktop/bb147325%28v=vs.85%29.aspx) that are used for rendering triangle meshes in all modern rendering APIs.</span></span> <span data-ttu-id="0ddd6-214">Notez que, dans la compréhension de la scène, les maillages utilisent des index 32 bits et peuvent avoir besoin d’être décomposés en segments pour certains moteurs de rendu.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-214">Note that in Scene Understanding, meshes use 32-bit indices and may need to be broken up into chunks for certain rendering engines.</span></span>

#### <a name="winding-order-and-coordinate-systems"></a><span data-ttu-id="0ddd6-215">Ordre d’enroulement et systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="0ddd6-215">Winding Order and Coordinate Systems</span></span>

<span data-ttu-id="0ddd6-216">Toutes les mailles produites par la compréhension des scènes sont supposées retourner des maillages dans un système de coordonnées droitiers à l’aide de l’ordre de séquencement des aiguilles d’une montre.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-216">All meshes produced by Scene Understanding are expected to return meshes in a Right-Handed coordinate system using clockwise winding order.</span></span> 

<span data-ttu-id="0ddd6-217">Remarque : les builds du système d’exploitation antérieures à. 191105 peuvent présenter un bogue connu dans lequel les maillages « universels » renvoient dans l’ordre de sortie dans le sens inverse des aiguilles d’une montre, qui a été résolu par la suite.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-217">Note: OS builds prior to .191105 may have a known bug where "World" meshes were returning in Counter-Clockwise winding order, which has subsequently been fixed.</span></span>

### <a name="scenequad"></a><span data-ttu-id="0ddd6-218">SceneQuad</span><span class="sxs-lookup"><span data-stu-id="0ddd6-218">SceneQuad</span></span>

<span data-ttu-id="0ddd6-219">Un SceneQuad est un SceneComponent qui représente des surfaces 2D qui occupent le monde 3D.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-219">A SceneQuad is a SceneComponent that represents 2d surfaces that occupy the 3d world.</span></span> <span data-ttu-id="0ddd6-220">SceneQuads peut être utilisé de la même façon que les plans ARKit ARPlaneAnchor ou ARCore, mais ils offrent des fonctionnalités de haut niveau comme des canevas 2D à utiliser par les applications plates, ou une expérience utilisateur améliorée.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-220">SceneQuads can be used similarly to ARKit ARPlaneAnchor or ARCore Planes but they offer more high level functionality as 2d canvases to be used by flat apps, or augmented UX.</span></span> <span data-ttu-id="0ddd6-221">des API spécifiques 2D sont fournies pour les quatre cœurs qui facilitent l’utilisation de l’emplacement et de la disposition, et le développement (à l’exception du rendu) avec quatre cœurs doit avoir un sens plus semblable à l’utilisation de canevas 2D que les maillages 3D.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-221">2D specific APIs are provided for quads that make placement and layout simple to use, and developing (with the exception of rendering) with quads should feel more akin to working with 2d canvases than 3d meshes.</span></span>

#### <a name="scenequad-shape"></a><span data-ttu-id="0ddd6-222">Forme SceneQuad</span><span class="sxs-lookup"><span data-stu-id="0ddd6-222">SceneQuad shape</span></span>

<span data-ttu-id="0ddd6-223">SceneQuads définit une surface rectangulaire délimitée en 2D.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-223">SceneQuads define a bounded rectangular surface in 2d.</span></span> <span data-ttu-id="0ddd6-224">Toutefois, les SceneQuads représentent des surfaces avec des formes arbitraires et potentiellement complexes (par exemple, une table en forme de bouée). Pour représenter la forme complexe de la surface d’un quadruple, vous pouvez utiliser l’API GetSurfaceMask pour afficher la forme de la surface dans une mémoire tampon d’image que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-224">However, SceneQuads are representing surfaces with arbitrary and potentially complex shapes (e.g. a donut shaped table.) To represent the complex shape of the surface of a quad you may use the GetSurfaceMask API to render the shape of the surface onto an image buffer you provide.</span></span> <span data-ttu-id="0ddd6-225">Si le SceneObject qui a le quad a également une maille, les triangles de maillage doivent être équivalents à cette image rendue, ils représentent tous les deux une géométrie réelle de la surface, juste en coordonnées 2D ou 3D.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-225">If the SceneObject that has the quad also has a mesh, the mesh triangles should be equivalent to this rendered image, they both represent real geometry of the surface, just either in 2d or 3d coordinates.</span></span>

## <a name="scene-understanding-sdk-details-and-reference"></a><span data-ttu-id="0ddd6-226">Description et informations de référence du SDK</span><span class="sxs-lookup"><span data-stu-id="0ddd6-226">Scene understanding SDK details and reference</span></span>

<span data-ttu-id="0ddd6-227">La section suivante vous aidera à vous familiariser avec les principes fondamentaux de SceneUnderstanding.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-227">The following section will help get you familiar with the basics of SceneUnderstanding.</span></span> <span data-ttu-id="0ddd6-228">Cette section doit vous fournir les principes de base, à partir desquels vous devez disposer d’un contexte suffisant pour parcourir les exemples d’applications et voir comment SceneUnderstanding est utilisé de manière holistique.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-228">This section should provide you with the basics, at which point you should have enough context to browse through the sample applications to see how SceneUnderstanding is used holistically.</span></span>

### <a name="initialization"></a><span data-ttu-id="0ddd6-229">Initialisation</span><span class="sxs-lookup"><span data-stu-id="0ddd6-229">Initialization</span></span>

<span data-ttu-id="0ddd6-230">La première étape de l’utilisation de SceneUnderstanding est de permettre à votre application d’obtenir une référence à un objet de scène.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-230">The first step to working with SceneUnderstanding is for your application to gain reference to a Scene object.</span></span> <span data-ttu-id="0ddd6-231">Cette opération peut être effectuée de deux manières : une scène peut être calculée par le pilote, ou une scène existante qui a été calculée dans le passé peut être désérialisée.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-231">This can be done in one of two ways, a Scene can either be computed by the driver, or an existing Scene that was computed in the past can be de-serialized.</span></span> <span data-ttu-id="0ddd6-232">Ce dernier est particulièrement utile pour travailler avec SceneUnderstanding pendant le développement, où les applications et les expériences peuvent être rapidement prototypées sans appareil de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-232">The latter is particularly useful for working with SceneUnderstanding during development, where applications and experiences can be prototyped quickly without a mixed reality device.</span></span>

<span data-ttu-id="0ddd6-233">Les scènes sont calculées à l’aide d’un SceneObserver.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-233">Scenes are computed using a SceneObserver.</span></span> <span data-ttu-id="0ddd6-234">Avant de créer une scène, votre application doit interroger votre appareil pour s’assurer qu’il prend en charge SceneUnderstanding, ainsi que pour demander l’accès utilisateur aux informations dont SceneUnderstanding a besoin.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-234">Before creating a Scene, your application should query your device to ensure that it supports SceneUnderstanding, as well as to request user access for information that SceneUnderstanding needs.</span></span>

```cs
if (SceneObserver.IsSupported())
{
    // Handle the error
}

// This call should grant the access we need.
await SceneObserver.RequestAccessAsync();
```

<span data-ttu-id="0ddd6-235">Si RequestAccessAsync () n’est pas appelé, le calcul d’une nouvelle scène échoue.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-235">If RequestAccessAsync() is not called, computing a new Scene will fail.</span></span> <span data-ttu-id="0ddd6-236">Ensuite, nous allons calculer une nouvelle scène enracinée autour du casque de la réalité mixte et ayant un rayon de 10 mètres.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-236">Next we will compute a new scene that's rooted around the Mixed Reality headset and has a 10 meter radius.</span></span>

```cs
// Create Query settings for the scene update
SceneQuerySettings querySettings;

querySettings.EnableSceneObjectQuads = true;                                       // Requests that the scene updates quads.
querySettings.EnableSceneObjectMeshes = true;                                      // Requests that the scene updates watertight mesh data.
querySettings.EnableOnlyObservedSceneObjects = false;                              // Do not explicitly turn off quad inference.
querySettings.EnableWorldMesh = true;                                              // Requests a static version of the spatial mapping mesh.
querySettings.RequestedMeshLevelOfDetail = SceneMeshLevelOfDetail.Fine;            // Requests the finest LOD of the static spatial mapping mesh.

// Initialize a new Scene
Scene myScene = SceneObserver.ComputeAsync(querySettings, 10.0f).GetAwaiter().GetResult();
```

### <a name="initialization-from-data-aka-the-pc-path"></a><span data-ttu-id="0ddd6-237">Initialisation à partir des données (alias.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-237">Initialization from Data (aka.</span></span> <span data-ttu-id="0ddd6-238">le chemin d’accès du PC)</span><span class="sxs-lookup"><span data-stu-id="0ddd6-238">the PC Path)</span></span>

<span data-ttu-id="0ddd6-239">Si les scènes peuvent être calculées pour une consommation directe, elles peuvent également être calculées sous forme sérialisée pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-239">While Scenes can be computed for direct consumption, they can also be computed in serialized form for later use.</span></span> <span data-ttu-id="0ddd6-240">Cela s’est avéré très utile pour le développement, car il permet aux développeurs de travailler dans et de tester la compréhension des scènes sans avoir besoin d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-240">This has proven to be very useful for development as it allows developers to work in and test Scene Understanding without the need for a device.</span></span> <span data-ttu-id="0ddd6-241">L’acte de sérialisation d’une scène est quasiment identique à son calcul, les données sont retournées à votre application au lieu d’être désérialisées localement par le kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="0ddd6-241">The act of serializing a scene is nearly identical to computing it, the data is returned to your application instead of being deserialized locally by the SDK.</span></span> <span data-ttu-id="0ddd6-242">Vous pouvez ensuite le désérialiser vous-même ou l’enregistrer pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-242">You may then deserialize it yourself or save it for future use.</span></span>

```cs
// Create Query settings for the scene update
SceneQuerySettings querySettings;

// Compute a scene but serialized as a byte array
SceneBuffer newSceneBuffer = SceneObserver.ComputeSerializedAsync(querySettings, 10.0f).GetAwaiter().GetResult();

// If we want to use it immediately we can de-serialize the scene ourselves
byte[] newSceneData = new byte[newSceneBuffer.Size];
newSceneBuffer.GetData(newSceneData);
Scene mySceneDeSerialized = Scene.Deserialize(newSceneData);

// Save newSceneBlob for later
```

### <a name="sceneobject-enumeration"></a><span data-ttu-id="0ddd6-243">Énumération SceneObject</span><span class="sxs-lookup"><span data-stu-id="0ddd6-243">SceneObject Enumeration</span></span>

<span data-ttu-id="0ddd6-244">Maintenant que votre application a une scène, votre application va regarder et interagir avec SceneObjects.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-244">Now that your application has a scene, your application will be looking at and interacting with SceneObjects.</span></span> <span data-ttu-id="0ddd6-245">Pour ce faire, accédez à la propriété **SceneObjects** :</span><span class="sxs-lookup"><span data-stu-id="0ddd6-245">This is done by accessing the **SceneObjects** property:</span></span>

```cs
SceneObject firstFloor = null;

// Find the first floor object
foreach (var sceneObject in myScene.SceneObjects)
{
    if (sceneObject.Kind == SceneObjectKind.Floor)
    {
        firstFloor = sceneObject;
        break;
    }
}
```

### <a name="component-update-and-re-finding-components"></a><span data-ttu-id="0ddd6-246">Mise à jour des composants et rerecherche de composants</span><span class="sxs-lookup"><span data-stu-id="0ddd6-246">Component update and re-finding components</span></span>

<span data-ttu-id="0ddd6-247">Une autre fonction récupère les composants de la scène appelée ***FindComponent***.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-247">There is another function that retrieves components in the Scene called ***FindComponent***.</span></span> <span data-ttu-id="0ddd6-248">Cette fonction est utile lors de la mise à jour des objets de suivi et de leur recherche dans des scènes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-248">This function is useful when updating tracking objects and finding them in subsequent scenes.</span></span> <span data-ttu-id="0ddd6-249">Le code suivant calcule une nouvelle scène par rapport à une scène précédente, puis trouve le plancher dans la nouvelle scène.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-249">The following code will compute a new scene relative to a previous scene and then find the floor in the new scene.</span></span>

```cs
// Compute a new scene, and tell the system that we want to compute relative to the previous scene
Scene myNextScene = SceneObserver.ComputeAsync(querySettings, 10.0f, myScene).GetAwaiter().GetResult();

// Use the Id for the floor we found last time, and find it again
firstFloor = (SceneObject)myNextScene.FindComponent(firstFloor.Id);

if (firstFloor != null)
{
    // We found it again, we can now update the transforms of all objects we attached to this floor transform
}
```

## <a name="accessing-meshes-and-quads-from-scene-objects"></a><span data-ttu-id="0ddd6-250">Accès aux maillages et aux quads à partir d’objets de scène</span><span class="sxs-lookup"><span data-stu-id="0ddd6-250">Accessing Meshes and Quads from Scene Objects</span></span>

<span data-ttu-id="0ddd6-251">Une fois les SceneObjects trouvés, votre application souhaitera probablement accéder aux données contenues dans les quadruples/les maillages dont elle est composée.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-251">Once SceneObjects have been found your application will most likely want to access the data that is contained in the quads/meshes that it is comprised of.</span></span> <span data-ttu-id="0ddd6-252">Ces données sont accessibles avec les propriétés ***quads*** et ***meshes*** .</span><span class="sxs-lookup"><span data-stu-id="0ddd6-252">This data is accessed with the ***Quads*** and ***Meshes*** properties.</span></span> <span data-ttu-id="0ddd6-253">Le code suivant énumère tous les Quad et les maillages de notre objet Floor.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-253">The following code will enumerate all quads and meshes of our floor object.</span></span>

```cs

// Get the transform for the SceneObject
System.Numerics.Matrix4x4 objectToSceneOrigin = firstFloor.GetLocationAsMatrix();

// Enumerate quads
foreach (var quad in firstFloor.Quads)
{
    // Process quads
}

// Enumerate meshes
foreach (var mesh in firstFloor.Meshes)
{
    // Process meshes
}
```

<span data-ttu-id="0ddd6-254">Notez qu’il s’agit du SceneObject qui a la transformation par rapport à l’origine de la scène.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-254">Notice that it is the SceneObject that has the transform that is relative to the Scene origin.</span></span> <span data-ttu-id="0ddd6-255">Cela est dû au fait que SceneObject représente une instance d’un « élément » et qu’il est localisable dans l’espace, les Quad et les maillages représentent une géométrie transformée par rapport à leur parent.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-255">This is because the SceneObject represents an instance of a "thing" and is locatable in space, the quads and meshes represent geometry that is transformed relative to their parent.</span></span> <span data-ttu-id="0ddd6-256">Il est possible pour des SceneObjects distincts de référencer le même SceneComponents SceneMesh/SceneQuad, et il est également possible qu’un SceneObject ait plus d’un SceneMesh/SceneQuad.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-256">It is possible for separate SceneObjects to reference the same SceneMesh/SceneQuad SceneComponents, and it is also possible that a SceneObject has more than one SceneMesh/SceneQuad.</span></span>

### <a name="dealing-with-transforms"></a><span data-ttu-id="0ddd6-257">Traitement des transformations</span><span class="sxs-lookup"><span data-stu-id="0ddd6-257">Dealing with Transforms</span></span>

<span data-ttu-id="0ddd6-258">La compréhension des scènes a fait une tentative délibérée d’alignement avec les représentations de scène 3D traditionnelles lors du traitement des transformations.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-258">Scene Understanding has made a deliberate attempt to align with traditional 3D scene representations when dealing with transforms.</span></span> <span data-ttu-id="0ddd6-259">Chaque scène est donc confinée à un système de coordonnées unique, à l’instar des représentations environnementales 3D les plus courantes.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-259">Each Scene is therefore confined to a single coordinate system much like most common 3D environmental representations.</span></span> <span data-ttu-id="0ddd6-260">Les SceneObjects fournissent chacun leur emplacement sous la forme d’une position et d’une orientation au sein de ce système de coordonnées.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-260">SceneObjects each provide their location as a position and orientation within that coordinate system.</span></span> <span data-ttu-id="0ddd6-261">Si votre application traite des scènes qui étendent la limite de ce qu’une origine unique fournit peut ancrer SceneObjects à SpatialAnchors, ou générer plusieurs scènes et les fusionner, mais pour des raisons de simplicité, nous supposons que des scènes étanches existent dans leur propre origine et sont localisées par un NodeId défini par Scene. OriginSpatialGraphNodeId.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-261">If your application is dealing with Scenes that stretch the limit of what a single origin provides it can anchor SceneObjects to SpatialAnchors, or generate several scenes and merge them together, but for simplicity we assume that watertight scenes exist in their own origin that's localized by one NodeId defined by Scene.OriginSpatialGraphNodeId.</span></span>

<span data-ttu-id="0ddd6-262">Le code Unity suivant, par exemple, montre comment utiliser la perception de Windows et les API Unity pour aligner les systèmes de coordonnées ensemble.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-262">The following Unity code, for example, shows how to use Windows Perception and Unity APIs to align coordinate systems together.</span></span> <span data-ttu-id="0ddd6-263">Pour plus d’informations sur les API de perception de Windows et sur les [objets natifs de réalité mixte en Unity](https://docs.microsoft.com//windows/mixed-reality/unity-xrdevice-advanced) , consultez [SpatialCoordinateSystem](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialcoordinatesystem) et [SpatialGraphInteropPreview](https://docs.microsoft.com//uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview) pour plus d’informations sur l’obtention d’un SpatialCoordinateSystem qui correspond à l’origine universelle de Unity, ainsi que sur la méthode d’extension `.ToUnity()` pour la conversion entre `System.Numerics.Matrix4x4` et `UnityEngine.Matrix4x4`.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-263">See [SpatialCoordinateSystem](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialcoordinatesystem) and [SpatialGraphInteropPreview](https://docs.microsoft.com//uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview) for details on the Windows Perception APIs, and [Mixed Reality native objects in Unity](https://docs.microsoft.com//windows/mixed-reality/unity-xrdevice-advanced) for details on obtaining a SpatialCoordinateSystem that corresponds to Unity's world origin, as well as the `.ToUnity()` extension method for converting between `System.Numerics.Matrix4x4` and `UnityEngine.Matrix4x4`.</span></span>

```cs
public class SceneRootComponent : MonoBehavior
{
    public SpatialCoordinateSystem worldOrigin;
    public Scene scene;
    SpatialCoordinateSystem sceneOrigin;
    
    void Start()
    {
        // Initialize a SpatialCoordinateSystem for the scene's node in the system's Spatial Graph.
        scene.origin = SpatialGraphInteropPreview.CreateCoordinateSystemForNode(scene.OriginSpatialGraphNodeId);
    }
    
    void Update()
    {
        // Try to get the current transform of the scene's spatial graph node.
        // This may not be available, e.g. when tracking has been lost.
        var sceneToWorld = sceneOrigin.TryGetTransformTo(worldOrigin);
        if (sceneToWorld.HasValue)
        {
            // Convert the transform to Unity numerics and update the game object.
            var sceneToWorldUnity = sceneToWorld.Value.ToUnity();
            this.gameObject.transform.SetPositionAndRotation(sceneToWorldUnity.GetColumn(3), sceneToWorldUnity.rotation);
        }
    }
}
```

<span data-ttu-id="0ddd6-264">Chaque `SceneObject` a une propriété `Position` et `Orientation` qui peut être utilisée pour positionner le contenu correspondant par rapport à l’origine du `Scene`contenant.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-264">Each `SceneObject` has a `Position` and `Orientation` property which can be used to position corresponding content relative to the origin of the containing `Scene`.</span></span> <span data-ttu-id="0ddd6-265">Par exemple, l’exemple suivant suppose que le jeu est un enfant de la racine de la scène et affecte sa position et sa rotation locales pour qu’il s’aligne sur un `SceneObject`donné :</span><span class="sxs-lookup"><span data-stu-id="0ddd6-265">For example, the following example assumes that the game is a child of the scene root, and assigns its local position and rotation to align to a given `SceneObject`:</span></span>

```cs
void SetLocalTransformFromSceneObject(GameObject gameObject, SceneObject sceneObject)
{
    gameObject.transform.localPosition = sceneObject.Position.ToUnity();
    gameObject.transform.localRotation = sceneObject.Orientation.ToUnity());
}
```

### <a name="quad"></a><span data-ttu-id="0ddd6-266">Quadruple</span><span class="sxs-lookup"><span data-stu-id="0ddd6-266">Quad</span></span>

<span data-ttu-id="0ddd6-267">Les Quad sont conçus pour faciliter les scénarios de positionnement 2D et doivent être considérés comme des extensions aux éléments d’expérience utilisateur 2D Canvas.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-267">Quads were designed to facilitate 2D placement scenarios and should be thought of as extensions to 2D canvas UX elements.</span></span> <span data-ttu-id="0ddd6-268">Alors que les Quad sont des composants de SceneObjects et peuvent être rendus en 3D, les API Quad elles-mêmes partent du principe que les quatre cœurs sont des structures 2D.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-268">While Quads are components of SceneObjects and can be rendered in 3D, the Quad APIs themselves assume Quads are 2D structures.</span></span> <span data-ttu-id="0ddd6-269">Elles offrent des informations telles que l’étendue, la forme et fournissent des API pour le positionnement.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-269">They offer information such as extent, shape, and provide APIs for placement.</span></span>

<span data-ttu-id="0ddd6-270">Les Quad présentent des étendues rectangulaires, mais elles représentent des surfaces 2D de forme arbitraire.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-270">Quads have rectangular extents, but they represent arbitrarily shaped 2D surfaces.</span></span> <span data-ttu-id="0ddd6-271">Pour activer la position sur ces surfaces 2D qui interagissent avec les utilitaires de l’environnement 3D quads, vous pouvez faire en sorte que cette interaction soit possible.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-271">To enable placement on these 2D surfaces that interact with the 3D environment quads offer utilities to make this interaction possible.</span></span> <span data-ttu-id="0ddd6-272">Actuellement, la compréhension des scènes fournit deux fonctions telles que **FindCentermostPlacement** et **GetOcclusionMask**.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-272">Currently Scene Understanding provides two such functions, **FindCentermostPlacement** and **GetOcclusionMask**.</span></span> <span data-ttu-id="0ddd6-273">FindCentermostPlacement est une API de haut niveau qui localise une position sur le quadruple dans laquelle un objet peut être placé et tente de trouver le meilleur emplacement pour votre objet, garantissant que le cadre englobant que vous fournissez se trouvera sur la surface sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-273">FindCentermostPlacement is a high level API that locates a position on the quad where an object can be placed and will try to find the best location for your object guaranteeing that the bounding box you provide will reside on the underlying surface.</span></span>

<span data-ttu-id="0ddd6-274">L’exemple suivant montre comment Rechercher l’emplacement positionnable centermost et ancrer un hologramme au quadruple.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-274">The following example shows how to find the centermost placeable location and anchor a hologram to the quad.</span></span>

```cs
// This code assumes you already have a "Root" object that attaches the Scene's Origin.

// Find the first quad
foreach (var sceneObject in myScene.SceneObjects)
{
    // Find a wall
    if (sceneObject.Kind == SceneObjectKind.Wall)
    {
        // Get the quad
        var quads = sceneObject.Quads;
        if (quads.Count > 0)
        {
            // Find a good location for a 1mx1m object  
            System.Numerics.Vector2 location;
            if (quads[0].FindCentermostPlacement(new System.Numerics.Vector2(1.0f, 1.0f), out location))
            {
                // We found one, anchor something to the transform
                // Step 1: Create a new game object for the quad itself as a child of the scene root
                // Step 2: Set the local transform from quads[0].Position and quads[0].Orientation
                // Step 3: Create your hologram and set it as a child of the quad's game object
                // Step 4: Set the hologram's local transform to a translation (location.x, location.y, 0)
            }
        }
    }
}
```

<span data-ttu-id="0ddd6-275">Les étapes 1-4 sont fortement dépendantes de votre infrastructure/implémentation particulière, mais les thèmes doivent être similaires.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-275">Steps 1-4 are highly dependent on your particular framework/implementation, but the themes should be similar.</span></span> <span data-ttu-id="0ddd6-276">Il est important de noter que le quad représente simplement un plan 2D limité qui est localisé dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-276">It is important to note that the Quad simply represents a bounded 2D plane that is localized in space.</span></span> <span data-ttu-id="0ddd6-277">En faisant savoir à votre moteur/infrastructure où se trouve le quad et la racine de vos objets par rapport au Quad, vos hologrammes se trouveront correctement en ce qui concerne le monde réel.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-277">By having your engine/framework know where the quad is and rooting your objects relative to the quad, your holograms will be located correctly with respect to the real world.</span></span> <span data-ttu-id="0ddd6-278">Pour obtenir des informations plus détaillées, consultez nos exemples sur les quatre cœurs qui présentent des implémentations spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-278">For more detailed information please see our samples on quads which show specific implementations.</span></span>

### <a name="mesh"></a><span data-ttu-id="0ddd6-279">Déjà</span><span class="sxs-lookup"><span data-stu-id="0ddd6-279">Mesh</span></span>

<span data-ttu-id="0ddd6-280">Les maillages représentent les représentations géométriques des objets ou des environnements.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-280">Meshes represent geometric representations of objects or environments.</span></span> <span data-ttu-id="0ddd6-281">À l’instar du [mappage spatial](spatial-mapping.md), les données de vertex et d’index de maillage fournies avec chaque maillage de surface spatiale utilisent la même disposition familière que les mémoires tampons de vertex et d’index utilisées pour le rendu des maillages de triangle dans toutes les API de rendu modernes.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-281">Much like [spatial mapping](spatial-mapping.md), mesh index and vertex data provided with each spatial surface mesh uses the same familiar layout as the vertex and index buffers that are used for rendering triangle meshes in all modern rendering APIs.</span></span> <span data-ttu-id="0ddd6-282">Les positions de vertex sont fournies dans le système de coordonnées du `Scene`.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-282">Vertex positions are provided in the coordinate system of the `Scene`.</span></span> <span data-ttu-id="0ddd6-283">Les API spécifiques utilisées pour référencer ces données sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ddd6-283">The specific APIs used to reference this data are as follows:</span></span>

```cs
void GetTriangleIndices(int[] indices);
void GetVertices(System.Numerics.Vector3[] vertices);
```

<span data-ttu-id="0ddd6-284">Le code suivant fournit un exemple de génération d’une liste de triangles à partir de la structure de maillage :</span><span class="sxs-lookup"><span data-stu-id="0ddd6-284">The following code provides an example of generating a triangle list from the mesh structure:</span></span>

```cs
uint[] indices = new uint[mesh.TriangleIndexCount];
System.Numerics.Vector3[] positions = new System.Numerics.Vector3[mesh.VertexCount];

mesh.GetTriangleIndices(indices);
mesh.GetVertexPositions(positions);
```

<span data-ttu-id="0ddd6-285">Les mémoires tampons d’index/vertex doivent être > = nombre d’index/vertex, mais peuvent être de taille arbitraire, ce qui permet une réutilisation efficace de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-285">The index/vertex buffers must be >= the index/vertex counts, but otherwise can be arbitrarily sized allowing for efficient memory re-use.</span></span>

## <a name="developing-with-scene-understandings"></a><span data-ttu-id="0ddd6-286">Développement avec présentation des scènes</span><span class="sxs-lookup"><span data-stu-id="0ddd6-286">Developing with scene understandings</span></span>

<span data-ttu-id="0ddd6-287">À ce stade, vous devez comprendre les principaux blocs de construction de la scène présentation du runtime et du kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="0ddd6-287">At this point you should understand the core building blocks of the scene understanding runtime and SDK.</span></span> <span data-ttu-id="0ddd6-288">La majeure partie de la puissance et de la complexité se trouve dans les modèles d’accès, l’interaction avec les frameworks 3D et les outils qui peuvent être écrits sur ces API pour effectuer des tâches plus avancées telles que la planification spatiale, l’analyse de la salle, la navigation, la physique, etc. Nous espérons capturer ces exemples dans des exemples qui devraient vous guider dans la bonne direction pour que vos scénarios brillent.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-288">The bulk of the power and complexity lies in access patterns, interaction with 3D frameworks, and tools that can be written on top of these APIs to perform more advanced tasks like spatial planning, room analysis, navigation, physics etc. We hope to capture these in samples that should hopefully guide you in the proper direction to make your scenarios shine.</span></span> <span data-ttu-id="0ddd6-289">S’il existe des exemples ou des scénarios que nous n’adressons pas, faites-le nous savoir et nous essaierons de documenter/prototyper ce dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-289">If there are samples/scenarios we are not addressing, please let us know and we will try to document/prototype what you need.</span></span>

### <a name="where-can-i-get-sample-code"></a><span data-ttu-id="0ddd6-290">Où puis-je recevoir un exemple de code ?</span><span class="sxs-lookup"><span data-stu-id="0ddd6-290">Where can I get sample code?</span></span>

<span data-ttu-id="0ddd6-291">Vous trouverez des exemples de code pour Unity dans notre page d' [exemple Unity](https://github.com/sceneunderstanding-microsoft/unitysample) .</span><span class="sxs-lookup"><span data-stu-id="0ddd6-291">Scene Understanding sample code for Unity can be found on our [Unity Sample Page](https://github.com/sceneunderstanding-microsoft/unitysample) page.</span></span> <span data-ttu-id="0ddd6-292">Cette application vous permet de communiquer avec votre appareil et de restituer les différents objets de scène, ou vous permet de charger une scène sérialisée sur votre ordinateur et de vous permettre de découvrir la scène sans appareil.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-292">This application will allow you to communicate with your device and render the various scene objects, or, it will allow you to load a serialized scene on your PC and allow you to experience Scene Understanding without a device.</span></span>

### <a name="where-can-i-get-sample-scenes"></a><span data-ttu-id="0ddd6-293">Où puis-je me procurer des exemples de scènes ?</span><span class="sxs-lookup"><span data-stu-id="0ddd6-293">Where can I get sample scenes?</span></span>

<span data-ttu-id="0ddd6-294">Si vous avez un HoloLens2, vous pouvez enregistrer toute scène que vous avez capturée en enregistrant la sortie de ComputeSerializedAsync dans un fichier et en la désérialisant à votre convenance.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-294">If you have a HoloLens2 you can save any scene you've captured by saving the output of ComputeSerializedAsync to file and deserializing it at your own convenience.</span></span> 

<span data-ttu-id="0ddd6-295">Si vous ne disposez pas d’un appareil HoloLens2, mais que vous souhaitez vous amuser avec la compréhension de la scène, vous devez télécharger une scène précapturée.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-295">If you do not have a HoloLens2 device but want to play with Scene Understanding you will need to download a pre-captured scene.</span></span> <span data-ttu-id="0ddd6-296">L’exemple Scene Understanding est actuellement fourni avec des scènes sérialisées qui peuvent être téléchargées et utilisées à votre convenance.</span><span class="sxs-lookup"><span data-stu-id="0ddd6-296">The Scene Understanding sample currently ships with serialized scenes that can be downloaded and used at your own convenience.</span></span> <span data-ttu-id="0ddd6-297">Vous pouvez les trouver ici :</span><span class="sxs-lookup"><span data-stu-id="0ddd6-297">You can find them here:</span></span>

[<span data-ttu-id="0ddd6-298">Exemples de scènes de vision</span><span class="sxs-lookup"><span data-stu-id="0ddd6-298">Scene Understanding Sample Scenes</span></span>](https://github.com/sceneunderstanding-microsoft/unitysample/tree/master/Assets/Resources/SerializedScenesForPCPath)

## <a name="see-also"></a><span data-ttu-id="0ddd6-299">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0ddd6-299">See also</span></span>

* [<span data-ttu-id="0ddd6-300">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="0ddd6-300">Spatial mapping</span></span>](spatial-mapping.md)
* [<span data-ttu-id="0ddd6-301">Compréhension des scènes</span><span class="sxs-lookup"><span data-stu-id="0ddd6-301">Scene understanding</span></span>](scene-understanding.md)
* [<span data-ttu-id="0ddd6-302">Exemple Unity</span><span class="sxs-lookup"><span data-stu-id="0ddd6-302">Unity Sample</span></span>](https://github.com/sceneunderstanding-microsoft/unitysample)
