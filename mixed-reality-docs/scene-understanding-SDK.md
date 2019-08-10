---
title: Scène Understanding SDK
description: Guide de programmation du SDK Scene Understanding
author: szymons
ms.author: szymons
ms.date: 07/08/19
ms.topic: article
keywords: Compréhension des scènes, mappage spatial, Windows Mixed Reality, Unity
ms.openlocfilehash: 88138622987800ff86a24d05e1308e694e2dd2b1
ms.sourcegitcommit: c4c293971bb3205a82121bbfb40d1ac52b5cb38e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/10/2019
ms.locfileid: "68941236"
---
## <a name="scene-understanding-sdk-overview"></a><span data-ttu-id="8b182-104">Présentation du SDK présentation de Scene</span><span class="sxs-lookup"><span data-stu-id="8b182-104">Scene Understanding SDK Overview</span></span>

<span data-ttu-id="8b182-105">L’objectif de la compréhension des scènes est de transformer les données de capteur d’environnement non structurées capturées par votre appareil de réalité mixte et de le convertir en une représentation puissante mais abstraite, intuitive et facile à développer pour.</span><span class="sxs-lookup"><span data-stu-id="8b182-105">The goal of Scene Understanding is to transform the un-structured environment sensor data that your Mixed Reality device captures and to convert it into a powerful but abstracted representation that is intuitive and easy to develop for.</span></span> <span data-ttu-id="8b182-106">Le kit de développement logiciel (SDK) joue le rôle de couche de communication entre votre application et le runtime Understanding.</span><span class="sxs-lookup"><span data-stu-id="8b182-106">The SDK acts as the communication layer between your application and the Scene Understanding runtime.</span></span> <span data-ttu-id="8b182-107">Elle est destinée à imiter les constructions standard existantes, telles que les graphiques de scène 3D pour les représentations 3D et les rectangles/panneaux 2D pour les applications 2D.</span><span class="sxs-lookup"><span data-stu-id="8b182-107">It's aimed to mimic existing standard constructs such as 3d scene graphs for 3d representations and 2D rectangles/panels for 2d applications.</span></span> <span data-ttu-id="8b182-108">Tandis que la construction de scènes comprenant les imitations sera mappée aux frameworks concrets que vous pouvez utiliser, en général SceneUnderstanding est une infrastructure agnostique qui autorise l’interopérabilité entre des frameworks variés qui interagissent avec elle.</span><span class="sxs-lookup"><span data-stu-id="8b182-108">While the constructs Scene Understanding mimics will map to concrete frameworks you may use, in general SceneUnderstanding is framework agnostic allowing for interop between varied frameworks that interact with it.</span></span> <span data-ttu-id="8b182-109">À mesure que la compréhension de la scène évolue, le rôle du kit de développement logiciel (SDK) consiste à s’assurer que de nouvelles représentations et fonctionnalités continuent à être exposées au sein d’une infrastructure unifiée.</span><span class="sxs-lookup"><span data-stu-id="8b182-109">As Scene Understanding evolves the role of the SDK is to ensure new representations and capabilities continue to be exposed within a unified framework.</span></span> <span data-ttu-id="8b182-110">Dans ce document, nous allons commencer par introduire des concepts de haut niveau qui vous aideront à vous familiariser avec l’environnement de développement/l’utilisation, puis à fournir une documentation plus détaillée pour des classes et des constructions spécifiques.</span><span class="sxs-lookup"><span data-stu-id="8b182-110">In this document we will first introduce high level concepts that will help you get familiar with the development environment/usage and then provide more detailed documentation for specific classes and constructs.</span></span>

## <a name="where-do-i-get-the-sdk"></a><span data-ttu-id="8b182-111">Où puis-je me procurer le kit de développement logiciel?</span><span class="sxs-lookup"><span data-stu-id="8b182-111">Where do I get the SDK?</span></span>

<span data-ttu-id="8b182-112">Le kit de développement logiciel (SDK) SceneUnderstanding peut être téléchargé via NuGet.</span><span class="sxs-lookup"><span data-stu-id="8b182-112">The SceneUnderstanding SDK is downloadable via NuGet.</span></span>

[<span data-ttu-id="8b182-113">SDK SceneUnderstanding</span><span class="sxs-lookup"><span data-stu-id="8b182-113">SceneUnderstanding SDK</span></span>](https://www.nuget.org/packages/Microsoft.MixedReality.SceneUnderstanding/)

<span data-ttu-id="8b182-114">Avant de commencer, Notez que le kit de développement logiciel (SDK) s’exécute par-dessus la série UWP et nécessite SDK Windows version 18362 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8b182-114">Before you begin please note that the SDK runs on top of the UWP, and requires Windows SDK version 18362 or higher.</span></span> 

### <a name="the-scene"></a><span data-ttu-id="8b182-115">La scène</span><span class="sxs-lookup"><span data-stu-id="8b182-115">The Scene</span></span>

<span data-ttu-id="8b182-116">Votre appareil de réalité mixte intègre constamment des informations sur ce qu’il voit dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="8b182-116">Your mixed reality device is constantly integrating information about what it sees in your environment.</span></span> <span data-ttu-id="8b182-117">La compréhension de la scène entonnoir toutes ces sources de données et produit une seule abstraction cohésive.</span><span class="sxs-lookup"><span data-stu-id="8b182-117">Scene Understanding funnels all of these data sources and produces one single cohesive abstraction.</span></span> <span data-ttu-id="8b182-118">La compréhension des scènes génère des scènes qui constituent une composition de [SceneObjects](scene-understanding-SDK.md#sceneobjects) représentant une instance d’une seule chose (par exemple, un mur/un plafond/étage). Les objets de scène sont eux-mêmes une composition de [SceneComponents](scene-understanding-SDK.md#scenecomponents) qui représentent des éléments plus granulaires qui composent ce SceneObject.</span><span class="sxs-lookup"><span data-stu-id="8b182-118">Scene Understanding generates Scenes which are a composition of [SceneObjects](scene-understanding-SDK.md#sceneobjects) that represent an instance of a single thing, (e.g. a wall/ceiling/floor.) Scene Objects themselves are a composition of [SceneComponents](scene-understanding-SDK.md#scenecomponents) which represent more granular pieces that make up this SceneObject.</span></span> <span data-ttu-id="8b182-119">Les exemples de composants sont les Quad et les maillages, mais à l’avenir, ils peuvent représenter des zones englobantes, des mehses de collision, des métadonnées, etc.</span><span class="sxs-lookup"><span data-stu-id="8b182-119">Examples of components are quads and meshes, but in the future could represent bounding boxes, collision mehses, metadata etc...</span></span>

<span data-ttu-id="8b182-120">Le processus de conversion des données de capteur brutes en scène est une opération potentiellement coûteuse qui peut prendre des secondes pour les espaces moyens (~ 10x10m) à minutes pour les espaces de très grande taille (~ 50x50m). par conséquent, il ne s’agit pas d’un objet qui est calculé par l’appareil sans demande de l’application.</span><span class="sxs-lookup"><span data-stu-id="8b182-120">The process of converting the raw sensor data into a Scene is a potentially expensive operation that could take seconds for medium spaces (~10x10m) to minutes for very large spaces (~50x50m) and therefore it is not something that is being computed by the device without application request.</span></span> <span data-ttu-id="8b182-121">Au lieu de cela, la génération de scènes est déclenchée par votre application à la demande.</span><span class="sxs-lookup"><span data-stu-id="8b182-121">Instead, Scene generation is triggered by your application on demand.</span></span> <span data-ttu-id="8b182-122">La classe SceneObserver a des méthodes statiques qui peuvent calculer ou désérialiser une scène, que vous pouvez ensuite énumérer/interagir avec.</span><span class="sxs-lookup"><span data-stu-id="8b182-122">The SceneObserver class has static methods that can Compute or Deserialize a scene, which you can then enumerate/interact with.</span></span> <span data-ttu-id="8b182-123">L’action «Compute» est exécutée à la demande et s’exécute sur l’UC, mais dans un processus séparé (le pilote de réalité mixte).</span><span class="sxs-lookup"><span data-stu-id="8b182-123">The "Compute" action is executed on-demand and executes on the CPU but in a seperate process (the Mixed Reality Driver).</span></span> <span data-ttu-id="8b182-124">Toutefois, pendant que nous effectuons le calcul dans un autre processus, les données de scène obtenues sont stockées et conservées dans votre application dans l’objet de scène.</span><span class="sxs-lookup"><span data-stu-id="8b182-124">However, while we do compute in another process the resulting Scene data is stored and maintained in your application in the Scene object.</span></span> 

<span data-ttu-id="8b182-125">Vous trouverez ci-dessous un diagramme qui illustre ce processus et montre des exemples de deux applications interagissant avec le runtime de la vision de la scène.</span><span class="sxs-lookup"><span data-stu-id="8b182-125">Below is a diagram that illustrates this process flow and shows examples of two applications interfacing with the Scene Understanding runtime.</span></span> 

![Diagramme de processus](images/SU-ProcessFlow.png)

<span data-ttu-id="8b182-127">La partie gauche est un diagramme du runtime de réalité mixte qui est toujours actif et s’exécute dans son propre processus.</span><span class="sxs-lookup"><span data-stu-id="8b182-127">On the left hand side is a diagram of the mixed reality runtime which is always on and running in its own process.</span></span> <span data-ttu-id="8b182-128">Ce Runtime est chargé de l’exécution du suivi des appareils, de la reconstruction de la surface et d’autres opérations que la présentation de Scene utilise pour comprendre et expliquer le monde autour de vous.</span><span class="sxs-lookup"><span data-stu-id="8b182-128">This runtime is responsible for performing device tracking, surface reconstruction, and other operations that Scene Understanding uses to understand and reason about the world around you.</span></span> <span data-ttu-id="8b182-129">Sur le côté droit du diagramme, nous présentons deux applications théoriques qui utilisent la compréhension des scènes.</span><span class="sxs-lookup"><span data-stu-id="8b182-129">On the right side of the diagram, we show two theoretical applications that make use of Scene Understanding.</span></span> <span data-ttu-id="8b182-130">La première application interface avec MRTK, qui utilise le kit de développement logiciel (SDK) de scène en interne, la deuxième application calcule et utilise deux instances de scène sepereate.</span><span class="sxs-lookup"><span data-stu-id="8b182-130">The first application interfaces with MRTK which uses the Scene Understanding SDK internally, the second app computes and uses two sepereate scene instances.</span></span> <span data-ttu-id="8b182-131">Les trois scènes dans ce diagramme génèrent des instances distinctes des scènes, le pilote ne suit pas l’état global qui est partagé entre les applications et les objets de scène dans une scène ne sont pas trouvés dans un autre.</span><span class="sxs-lookup"><span data-stu-id="8b182-131">All 3 Scenes in this diagram generate distinct instances of the scenes, the driver is not tracking global state that is shared between applications and Scene Objects in one scene are not found in another.</span></span> <span data-ttu-id="8b182-132">La compréhension de la scène fournit un mécanisme de suivi au fil du temps, mais cette opération s’effectue à l’aide du kit de développement logiciel (SDK) et du code, le code qui effectue ce suivi s’exécute dans le kit de développement logiciel (SDK) du processus de votre application</span><span class="sxs-lookup"><span data-stu-id="8b182-132">Scene Understanding does provide a mechanism to track over time, but this is done using the SDK and code the code that performs this tracking is running in the SDK in your app's process.</span></span>

<span data-ttu-id="8b182-133">Étant donné que chaque scène stocke ses données dans l’espace mémoire de votre application, vous pouvez supposer que toutes les fonctions de l’objet de la scène ou de ses données internes sont toujours exécutées dans le processus de votre application.</span><span class="sxs-lookup"><span data-stu-id="8b182-133">Because each Scene stores it's data in your application's memory space, you can assume that all function of the Scene object or it's internal data is always executed in your application's process.</span></span>

#### <a name="layout"></a><span data-ttu-id="8b182-134">Mise en page</span><span class="sxs-lookup"><span data-stu-id="8b182-134">Layout</span></span>

<span data-ttu-id="8b182-135">Pour travailler avec la compréhension des scènes, il peut être utile de savoir et de comprendre comment le runtime représente des composants logiquement et physiquement.</span><span class="sxs-lookup"><span data-stu-id="8b182-135">To work with Scene Understanding it may be valuable to know and understand how the runtime represents components logically and physically.</span></span> <span data-ttu-id="8b182-136">La scène représente des données avec une disposition spécifique qui a été choisie comme simple tout en conservant une structure sous-jacente qui est pliable pour répondre aux exigences futures sans avoir besoin de révisions majeures.</span><span class="sxs-lookup"><span data-stu-id="8b182-136">The Scene represents data with a specific layout that was chosen to be simple while maintaining an underlying structure that is pliable to meet future requirements without needing major revisions.</span></span> <span data-ttu-id="8b182-137">Pour ce faire, la scène stocke tous les composants (blocs de construction pour tous les objets de scène) dans une liste plate et définit la hiérarchie et la composition par le biais de références où des composants spécifiques référencent d’autres.</span><span class="sxs-lookup"><span data-stu-id="8b182-137">The Scene does this by storing all Components (building blocks for all Scene Objects) in a flat list and defining hierarchy and composition through references where specific components reference others.</span></span>

<span data-ttu-id="8b182-138">Ci-dessous, nous présentons un exemple de structure dans sa forme plate et logique.</span><span class="sxs-lookup"><span data-stu-id="8b182-138">Below we present an example of a structure in both its flat and logical form.</span></span>

<table>
<tr><th><span data-ttu-id="8b182-139">Disposition logique</span><span class="sxs-lookup"><span data-stu-id="8b182-139">Logical Layout</span></span></th><th><span data-ttu-id="8b182-140">Disposition physique</span><span class="sxs-lookup"><span data-stu-id="8b182-140">Physical Layout</span></span></th></tr>
<tr>
<td>
<ul>
  <span data-ttu-id="8b182-141">Écran</span><span class="sxs-lookup"><span data-stu-id="8b182-141">Scene</span></span>
  <ul>
  <li><span data-ttu-id="8b182-142">SceneObject_1</span><span class="sxs-lookup"><span data-stu-id="8b182-142">SceneObject_1</span></span>
    <ul>
      <li><span data-ttu-id="8b182-143">Mesh_1</span><span class="sxs-lookup"><span data-stu-id="8b182-143">Mesh_1</span></span></li>
      <li><span data-ttu-id="8b182-144">Quad_1</span><span class="sxs-lookup"><span data-stu-id="8b182-144">Quad_1</span></span></li>
      <li><span data-ttu-id="8b182-145">Quad_2</span><span class="sxs-lookup"><span data-stu-id="8b182-145">Quad_2</span></span></li>
    </ul>
  </li>
  <li><span data-ttu-id="8b182-146">SceneObject_2</span><span class="sxs-lookup"><span data-stu-id="8b182-146">SceneObject_2</span></span>
    <ul>
      <li><span data-ttu-id="8b182-147">Quad_1</span><span class="sxs-lookup"><span data-stu-id="8b182-147">Quad_1</span></span></li>
      <li><span data-ttu-id="8b182-148">Quad_3</span><span class="sxs-lookup"><span data-stu-id="8b182-148">Quad_3</span></span></li>
      </li></ul>
  </li>
  <li><span data-ttu-id="8b182-149">SceneObject_3</span><span class="sxs-lookup"><span data-stu-id="8b182-149">SceneObject_3</span></span>
    <ul>
      <li><span data-ttu-id="8b182-150">Mesh_3</span><span class="sxs-lookup"><span data-stu-id="8b182-150">Mesh_3</span></span></li>
    </ul>
  </ul>
</ul>
</td>
<td>
<ul>
  <li><span data-ttu-id="8b182-151">SceneObject_1</span><span class="sxs-lookup"><span data-stu-id="8b182-151">SceneObject_1</span></span></li>
  <li><span data-ttu-id="8b182-152">SceneObject_2</span><span class="sxs-lookup"><span data-stu-id="8b182-152">SceneObject_2</span></span></li>
  <li><span data-ttu-id="8b182-153">SceneObject_3</span><span class="sxs-lookup"><span data-stu-id="8b182-153">SceneObject_3</span></span></li>
  <li><span data-ttu-id="8b182-154">Quad_1</span><span class="sxs-lookup"><span data-stu-id="8b182-154">Quad_1</span></span></li>
  <li><span data-ttu-id="8b182-155">Quad_2</span><span class="sxs-lookup"><span data-stu-id="8b182-155">Quad_2</span></span></li>
  <li><span data-ttu-id="8b182-156">Quad_3</span><span class="sxs-lookup"><span data-stu-id="8b182-156">Quad_3</span></span></li>
  <li><span data-ttu-id="8b182-157">Mesh_1</span><span class="sxs-lookup"><span data-stu-id="8b182-157">Mesh_1</span></span></li>
  <li><span data-ttu-id="8b182-158">Mesh_2</span><span class="sxs-lookup"><span data-stu-id="8b182-158">Mesh_2</span></span></li>
</ul>
</td>
</tr>
</table>

<span data-ttu-id="8b182-159">Cette illustration met en évidence la différence entre la disposition physique et logique de la scène.</span><span class="sxs-lookup"><span data-stu-id="8b182-159">This illustration highlights the difference between the physical and logical layout of the Scene.</span></span> <span data-ttu-id="8b182-160">À droite, nous voyons la disposition hiérarchique des données que votre application voit lors de l’énumération de la scène.</span><span class="sxs-lookup"><span data-stu-id="8b182-160">On the right we see the hierarchical layout of the data that your application sees when enumerating the scene.</span></span> <span data-ttu-id="8b182-161">À gauche, nous voyons que la scène est en fait composée de 12 composants distincts qui sont accessibles individuellement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8b182-161">On the left we see that the scene is actually comprised of 12 distinct components that are accessible individually if necessary.</span></span> <span data-ttu-id="8b182-162">Lors du traitement d’une nouvelle scène, nous pensons que les applications parcourent cette hiérarchie logiquement, toutefois, lors du suivi entre les mises à jour de la scène, certaines applications peuvent uniquement être intéressées à cibler des composants spécifiques qui sont partagés entre deux scènes.</span><span class="sxs-lookup"><span data-stu-id="8b182-162">When processing a new scene, we expect applications to walk this hierarchy logically, however when tracking between scene updates, some applications may only be interested in targeting specific components that are shared between two scenes.</span></span>

### <a name="high-level-overview"></a><span data-ttu-id="8b182-163">Vue d’ensemble de haut niveau</span><span class="sxs-lookup"><span data-stu-id="8b182-163">High-level Overview</span></span>

<span data-ttu-id="8b182-164">La section suivante fournit une vue d’ensemble des constructions de la présentation des scènes.</span><span class="sxs-lookup"><span data-stu-id="8b182-164">The following section provides a high-level overview of the constructs in Scene Understanding.</span></span> <span data-ttu-id="8b182-165">La lecture de cette section vous donne une idée de la façon dont les scènes sont représentées, ainsi que de l’utilisation des différents composants.</span><span class="sxs-lookup"><span data-stu-id="8b182-165">Reading this section will give you an  understanding of how scenes are represented, and what the various components do/are used for.</span></span> <span data-ttu-id="8b182-166">La section suivante fournit des exemples de code concrets et des détails supplémentaires qui sont brillants dans cette vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="8b182-166">The next section will provide concrete code examples and additional details that are glossed over in this overview.</span></span>

#### <a name="scenecomponents"></a><span data-ttu-id="8b182-167">SceneComponents</span><span class="sxs-lookup"><span data-stu-id="8b182-167">SceneComponents</span></span>

<span data-ttu-id="8b182-168">Maintenant que vous comprenez la disposition logique des scènes, nous pouvons maintenant présenter le concept de SceneComponents et la façon dont ils sont utilisés pour composer la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="8b182-168">Now that you understand the logical layout of scenes we can now present the concept of SceneComponents and how they are used to compose hierarchy.</span></span> <span data-ttu-id="8b182-169">SceneComponents sont les décompositions les plus granulaires de SceneUnderstanding qui représentent une seule base, par exemple une maille ou un quadruple-Box ou un cadre englobant.</span><span class="sxs-lookup"><span data-stu-id="8b182-169">SceneComponents are the most granular decompositions in SceneUnderstanding representing a single core thing, e.g. a mesh or a quad or a bounding box.</span></span> <span data-ttu-id="8b182-170">Les SceneComponents sont des éléments qui peuvent être mis à jour de manière indépendante et peuvent être référencés par d’autres SceneComponents, de sorte qu’ils disposent d’un ID unique de propriété globale unique, qui autorise ce type de mécanisme de suivi/référencement.</span><span class="sxs-lookup"><span data-stu-id="8b182-170">SceneComponents are things that can update independently and can be referenced by other SceneComponents, hence they have a single global property a unique Id, that allow for this type of tracking/referencing mechanism.</span></span> <span data-ttu-id="8b182-171">Les ID sont utilisés pour la composition logique de la hiérarchie des scènes, ainsi que pour la persistance des objets (opération consistant à mettre à jour une scène par rapport à une autre.)</span><span class="sxs-lookup"><span data-stu-id="8b182-171">Ids are used for the logical composition of scene hierarchy as well as object persistence (the act of updating one scene relative to another.)</span></span> 

<span data-ttu-id="8b182-172">Si vous traitez toutes les scènes nouvellement calculées comme étant distinctes et que vous énumérez simplement toutes les données qu’elle contient, les ID sont en grande partie transparents pour vous.</span><span class="sxs-lookup"><span data-stu-id="8b182-172">If you are treating every newly computed scene as being distinct, and simply enumerating all data within it then Ids are largely transparent to you.</span></span> <span data-ttu-id="8b182-173">Toutefois, si vous envisagez de suivre des composants sur plusieurs mises à jour, vous allez utiliser les ID pour indexer et Rechercher des SceneComponents entre les objets de scène.</span><span class="sxs-lookup"><span data-stu-id="8b182-173">However, if you are planning to track components over several updates you will use the Ids to index and find SceneComponents between Scene objects.</span></span>

#### <a name="sceneobjects"></a><span data-ttu-id="8b182-174">SceneObjects</span><span class="sxs-lookup"><span data-stu-id="8b182-174">SceneObjects</span></span>

<span data-ttu-id="8b182-175">Un SceneObject est un SceneComponent qui représente une instance d’un «élément», par exemple un mur, un étage, un plafond, etc. exprimé par leur propriété Kind.</span><span class="sxs-lookup"><span data-stu-id="8b182-175">A SceneObject is a SceneComponent that represents an instance of a "thing" e.g. a wall, a floor, a ceiling, etc... expressed by their Kind property.</span></span> <span data-ttu-id="8b182-176">Les SceneObjects sont géométriques et, par conséquent, ont des fonctions et des propriétés qui représentent leur emplacement dans l’espace, mais elles ne contiennent pas de structure géométrique ou logique.</span><span class="sxs-lookup"><span data-stu-id="8b182-176">SceneObjects are geometric, and therefore have functions and properties that represent their location in space, however they don't contain any geometric or logical structure.</span></span> <span data-ttu-id="8b182-177">Au lieu de cela, SceneObjects référence d’autres SceneComponents, en particulier SceneQuads et SceneMeshes, qui fournissent les représentations variées prises en charge par le système.</span><span class="sxs-lookup"><span data-stu-id="8b182-177">Instead, SceneObjects reference other SceneComponents, specifically SceneQuads and SceneMeshes which provide the varied representations that are supported by the system.</span></span> <span data-ttu-id="8b182-178">Quand une nouvelle scène est calculée, votre application va probablement énumérer le SceneObjects de la scène pour traiter ce qui l’intéresse.</span><span class="sxs-lookup"><span data-stu-id="8b182-178">When a new scene is computed, your application will most likely enumerate the Scene's SceneObjects to process what it's interested in.</span></span>

<span data-ttu-id="8b182-179">SceneObjects peut avoir l’un des éléments suivants:</span><span class="sxs-lookup"><span data-stu-id="8b182-179">SceneObjects can have any one of the following:</span></span>

<table>
<tr>
<th><span data-ttu-id="8b182-180">SceneObjectKind</span><span class="sxs-lookup"><span data-stu-id="8b182-180">SceneObjectKind</span></span></th> <th><span data-ttu-id="8b182-181">Description</span><span class="sxs-lookup"><span data-stu-id="8b182-181">Description</span></span></th>
</tr>
<tr><td><span data-ttu-id="8b182-182">Présentation</span><span class="sxs-lookup"><span data-stu-id="8b182-182">Background</span></span></td><td><span data-ttu-id="8b182-183">Le SceneObject est connu pour <b>ne pas</b> être l’un des autres types d’objets de scène reconnus.</span><span class="sxs-lookup"><span data-stu-id="8b182-183">The SceneObject is known to be <b>not</b> one of the other recognized kinds of scene object.</span></span> <span data-ttu-id="8b182-184">Cette classe ne doit pas être confondue avec Unknown, où l’arrière-plan est connu comme étant un mur/plancher/plafond, etc... alors que inconnu n’est pas encore catégorisé.</span><span class="sxs-lookup"><span data-stu-id="8b182-184">This class should not be confused with Unknown where Background is known not to be wall/floor/ceiling etc... while unknown is not yet categorized.</span></span></b></td></tr>
<tr><td><span data-ttu-id="8b182-185">Encastre</span><span class="sxs-lookup"><span data-stu-id="8b182-185">Wall</span></span></td><td><span data-ttu-id="8b182-186">Un mur physique.</span><span class="sxs-lookup"><span data-stu-id="8b182-186">A physical wall.</span></span> <span data-ttu-id="8b182-187">Les murs sont supposés être des structures environnementales immobilières.</span><span class="sxs-lookup"><span data-stu-id="8b182-187">Walls are assumed to be immovable environmental structures.</span></span></td></tr>
<tr><td><span data-ttu-id="8b182-188">Floor</span><span class="sxs-lookup"><span data-stu-id="8b182-188">Floor</span></span></td><td><span data-ttu-id="8b182-189">Les étages sont des surfaces sur lesquelles il est possible de parcourir.</span><span class="sxs-lookup"><span data-stu-id="8b182-189">Floors are any surfaces on which one can walk.</span></span> <span data-ttu-id="8b182-190">Remarque: les escaliers ne sont pas des étages.</span><span class="sxs-lookup"><span data-stu-id="8b182-190">Note: stairs are not floors.</span></span> <span data-ttu-id="8b182-191">Notez également que les étages supposent une surface pouvant être guidée et qu’il n’y a donc pas d’hypothèse explicite d’un étage singulier.</span><span class="sxs-lookup"><span data-stu-id="8b182-191">Also note, that floors assume any walkable surface and therefore there is no explicit assumption of a singular floor.</span></span> <span data-ttu-id="8b182-192">Structures à plusieurs niveaux, rampes, etc... doit tous être classifiés en tant que plancher.</span><span class="sxs-lookup"><span data-stu-id="8b182-192">Multi-level structures, ramps etc... should all classify as floor.</span></span></td></tr>
<tr><td><span data-ttu-id="8b182-193">Plafond</span><span class="sxs-lookup"><span data-stu-id="8b182-193">Ceiling</span></span></td><td><span data-ttu-id="8b182-194">Surface supérieure d’une salle.</span><span class="sxs-lookup"><span data-stu-id="8b182-194">The upper surface of a room.</span></span></td></tr>
<tr><td><span data-ttu-id="8b182-195">Plateforme</span><span class="sxs-lookup"><span data-stu-id="8b182-195">Platform</span></span></td><td><span data-ttu-id="8b182-196">Grande surface plate sur laquelle vous pouvez placer des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="8b182-196">A large flat surface on which you could place holograms.</span></span> <span data-ttu-id="8b182-197">Elles ont tendance à représenter des tables, des plans de plan et d’autres grandes surfaces horizontales.</span><span class="sxs-lookup"><span data-stu-id="8b182-197">These tend to represent tables, countertops and other large horizontal surfaces.</span></span></td></tr>
<tr><td><span data-ttu-id="8b182-198">World</span><span class="sxs-lookup"><span data-stu-id="8b182-198">World</span></span></td><td><span data-ttu-id="8b182-199">Étiquette réservée pour les données géométriques indépendantes de l’étiquetage.</span><span class="sxs-lookup"><span data-stu-id="8b182-199">A reserved label for geometric data that is agnostic to labeling.</span></span> <span data-ttu-id="8b182-200">La maille générée par la définition de l’indicateur de mise à jour EnableWorldMesh est classée comme monde.</span><span class="sxs-lookup"><span data-stu-id="8b182-200">The mesh generated by setting the EnableWorldMesh update flag would be classified as world.</span></span></td></tr>
<tr><td><span data-ttu-id="8b182-201">Inconnu</span><span class="sxs-lookup"><span data-stu-id="8b182-201">Unknown</span></span></td><td><span data-ttu-id="8b182-202">Cet objet de scène n’a pas encore été classé et affecté un genre.</span><span class="sxs-lookup"><span data-stu-id="8b182-202">This scene object has yet to be classified and assigned a kind.</span></span> <span data-ttu-id="8b182-203">Cela ne doit pas être confondu avec l’arrière-plan, car cet objet peut être n’importe quoi, le système n’a pas encore pu trouver une classification suffisamment importante pour l’informatique.</span><span class="sxs-lookup"><span data-stu-id="8b182-203">This should not be confused with Background, as this object could be anything, the system has just not come up with a strong enough classification for it yet.</span></span></td></tr>
</tr>
</table>

#### <a name="scenemesh"></a><span data-ttu-id="8b182-204">SceneMesh</span><span class="sxs-lookup"><span data-stu-id="8b182-204">SceneMesh</span></span>

<span data-ttu-id="8b182-205">Un SceneMesh est un SceneComponent qui se rapproche de la géométrie des objets géométriques arbitraires à l’aide d’une liste de triangles.</span><span class="sxs-lookup"><span data-stu-id="8b182-205">A SceneMesh is a SceneComponent that approximates the geometry of arbitrary geometric objects using a triangle list.</span></span> <span data-ttu-id="8b182-206">Les SceneMeshes sont utilisés dans plusieurs contextes différents, ils peuvent représenter des composants de la structure de cellules étanches ou en tant que WorldMesh qui représente la reconstruction de la surface indépendante associée à la scène.</span><span class="sxs-lookup"><span data-stu-id="8b182-206">SceneMeshes are used in several different contexts, they can represent components of the watertight cell structure or as the WorldMesh which represents the unbounded Surface Reconstruction associated with the Scene.</span></span> <span data-ttu-id="8b182-207">Les données d’index et de vertex fournies avec chaque maille utilisent la même disposition familière que les [mémoires tampons de vertex et d’index](https://msdn.microsoft.com/library/windows/desktop/bb147325%28v=vs.85%29.aspx) utilisées pour le rendu des maillages de triangle dans toutes les API de rendu modernes.</span><span class="sxs-lookup"><span data-stu-id="8b182-207">The index and vertex data provided with each mesh uses the same familiar layout as the [vertex and index buffers](https://msdn.microsoft.com/library/windows/desktop/bb147325%28v=vs.85%29.aspx) that are used for rendering triangle meshes in all modern rendering APIs.</span></span> <span data-ttu-id="8b182-208">Notez que, dans la compréhension de la scène, les maillages utilisent des index 32 bits et peuvent avoir besoin d’être décomposés en segments pour certains moteurs de rendu.</span><span class="sxs-lookup"><span data-stu-id="8b182-208">Note that in Scene Understanding, meshes use 32-bit indices and may need to be broken up into chunks for certain rendering engines.</span></span>

#### <a name="scenequad"></a><span data-ttu-id="8b182-209">SceneQuad</span><span class="sxs-lookup"><span data-stu-id="8b182-209">SceneQuad</span></span>

<span data-ttu-id="8b182-210">Un SceneQuad est un SceneComponent qui représente des surfaces 2D qui occupent le monde 3D.</span><span class="sxs-lookup"><span data-stu-id="8b182-210">A SceneQuad is a SceneComponent that represents 2d surfaces that occupy the 3d world.</span></span> <span data-ttu-id="8b182-211">SceneQuads peut être utilisé de la même façon que les plans ARKit ARPlaneAnchor ou ARCore, mais ils offrent des fonctionnalités de haut niveau comme des canevas 2D à utiliser par les applications plates, ou une expérience utilisateur améliorée.</span><span class="sxs-lookup"><span data-stu-id="8b182-211">SceneQuads can be used similarly to ARKit ARPlaneAnchor or ARCore Planes but they offer more high level functionality as 2d canvases to be used by flat apps, or augmented UX.</span></span> <span data-ttu-id="8b182-212">des API spécifiques 2D sont fournies pour les quatre cœurs qui facilitent l’utilisation de l’emplacement et de la disposition, et le développement (à l’exception du rendu) avec quatre cœurs doit avoir un sens plus semblable à l’utilisation de canevas 2D que les maillages 3D.</span><span class="sxs-lookup"><span data-stu-id="8b182-212">2D specific APIs are provided for quads that make placement and layout simple to use, and developing (with the exception of rendering) with quads should feel more akin to working with 2d canvases than 3d meshes.</span></span>

### <a name="scene-understanding-sdk-details-and-reference"></a><span data-ttu-id="8b182-213">Description et informations de référence du SDK</span><span class="sxs-lookup"><span data-stu-id="8b182-213">Scene Understanding SDK Details and Reference</span></span>

#### <a name="sdk"></a><span data-ttu-id="8b182-214">SDK</span><span class="sxs-lookup"><span data-stu-id="8b182-214">SDK</span></span>

<span data-ttu-id="8b182-215">La section suivante vous aidera à vous familiariser avec les principes fondamentaux de SceneUnderstanding.</span><span class="sxs-lookup"><span data-stu-id="8b182-215">The following section will help get you familiar with the basics of SceneUnderstanding.</span></span> <span data-ttu-id="8b182-216">Cette section doit vous fournir les principes de base, à partir desquels vous devez disposer d’un contexte suffisant pour parcourir les exemples d’applications et voir comment SceneUnderstanding est utilisé de manière holistique.</span><span class="sxs-lookup"><span data-stu-id="8b182-216">This section should provide you with the basics, at which point you should have enough context to browse through the sample applications to see how SceneUnderstanding is used holistically.</span></span>

#### <a name="initialization"></a><span data-ttu-id="8b182-217">Initialisation</span><span class="sxs-lookup"><span data-stu-id="8b182-217">Initialization</span></span>

<span data-ttu-id="8b182-218">La première étape de l’utilisation de SceneUnderstanding est de permettre à votre application d’obtenir une référence à un objet de scène.</span><span class="sxs-lookup"><span data-stu-id="8b182-218">The first step to working with SceneUnderstanding is for your application to gain reference to a Scene object.</span></span> <span data-ttu-id="8b182-219">Cette opération peut être effectuée de deux manières: une scène peut être calculée par le pilote, ou une scène existante qui a été calculée dans le passé peut être désérialisée.</span><span class="sxs-lookup"><span data-stu-id="8b182-219">This can be done in one of two ways, a Scene can either be computed by the driver, or an existing Scene that was computed in the past can be de-serialized.</span></span> <span data-ttu-id="8b182-220">Ce dernier est particulièrement utile pour travailler avec SceneUnderstanding pendant le développement, où les applications et les expériences peuvent être rapidement prototypées sans appareil de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="8b182-220">The latter is particularly useful for working with SceneUnderstanding during development, where applications and experiences can be prototyped quickly without a mixed reality device.</span></span>

<span data-ttu-id="8b182-221">Les scènes sont calculées à l’aide d’un SceneObserver.</span><span class="sxs-lookup"><span data-stu-id="8b182-221">Scenes are computed using a SceneObserver.</span></span> <span data-ttu-id="8b182-222">Avant de créer une scène, votre application doit interroger votre appareil pour s’assurer qu’il prend en charge SceneUnderstanding, ainsi que pour demander l’accès utilisateur aux informations dont SceneUnderstanding a besoin.</span><span class="sxs-lookup"><span data-stu-id="8b182-222">Before creating a Scene, your application should query your device to ensure that it supports SceneUnderstanding, as well as to request user access for information that SceneUnderstanding needs.</span></span>

```cs
if (SceneObserver.IsSupported())
{
    // Handle the error
}

// This call should grant the access we need.
await SceneObserver.RequestAccessAsync();
```

<span data-ttu-id="8b182-223">Si RequestAccessAsync () n’est pas appelé, le calcul d’une nouvelle scène échoue.</span><span class="sxs-lookup"><span data-stu-id="8b182-223">If RequestAccessAsync() is not called, computing a new Scene will fail.</span></span> <span data-ttu-id="8b182-224">Ensuite, nous allons calculer une nouvelle scène enracinée autour du casque de la réalité mixte et ayant un rayon de 10 mètres.</span><span class="sxs-lookup"><span data-stu-id="8b182-224">Next we will compute a new scene that's rooted around the Mixed Reality headset and has a 10 meter radius.</span></span>

```cs
// Create Query settings for the scene update
SceneQuerySettings querySettings;

querySettings.EnableSceneObjectQuads = true;                                       // Requests that the scene updates quads.
querySettings.EnableSceneObjectMeshes = true;                                      // Requests that the scene updates watertight mesh data.
querySettings.EnableOnlyObservedSceneObjects = false;                              // Do not explicitly turn off quad inference.
querySettings.EnableWorldMesh = true;                                              // Requests a static version of the spatial mapping mesh.
querySettings.RequestedMeshLevelOfDetail = SceneMeshLevelOfDetail.Fine;            // Requests the finest LOD of the static spatial mapping mesh.

// Initialize a new Scene
Scene myScene = SceneObserver.Compute(querySettings, 10.0f);
```

#### <a name="initialization-from-data-aka-the-pc-path"></a><span data-ttu-id="8b182-225">Initialisation à partir des données (alias.</span><span class="sxs-lookup"><span data-stu-id="8b182-225">Initialization from Data (aka.</span></span> <span data-ttu-id="8b182-226">le chemin d’accès du PC)</span><span class="sxs-lookup"><span data-stu-id="8b182-226">the PC Path)</span></span>

<span data-ttu-id="8b182-227">Si les scènes peuvent être calculées pour une consommation directe, elles peuvent également être calculées sous forme sérialisée pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8b182-227">While Scenes can be computed for direct consumption, they can also be computed in serialized form for later use.</span></span> <span data-ttu-id="8b182-228">Cela s’est avéré très utile pour le développement, car il permet aux développeurs de travailler dans et de tester la compréhension des scènes sans avoir besoin d’un appareil.</span><span class="sxs-lookup"><span data-stu-id="8b182-228">This has proven to be very useful for development as it allows developers to work in and test Scene Understanding without the need for a device.</span></span> <span data-ttu-id="8b182-229">L’acte de sérialisation d’une scène est quasiment identique à son calcul, les données sont retournées à votre application au lieu d’être désérialisées localement par le kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="8b182-229">The act of serializing a scene is nearly identical to computing it, the data is returned to your application instead of being deserialized locally by the SDK.</span></span> <span data-ttu-id="8b182-230">Vous pouvez ensuite le désérialiser vous-même ou l’enregistrer pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8b182-230">You may then deserialize it yourself or save it for future use.</span></span>

```cs
// Create Query settings for the scene update
SceneUnderstanding.QuerySettings querySettings;

// Compute a scene but serialized as a byte array
byte[] newSceneBlob = SceneObserver.ComputeSerialized(querySettings, 10.0f);

// If we want to use it immediatley we can de-serialize the scene ourselves
Scene mySceneDeSerialized = Scene.Deserialize(newSceneBlob);

// Save newSceneBlob for later
```

#### <a name="sceneobject-enumeration"></a><span data-ttu-id="8b182-231">Énumération SceneObject</span><span class="sxs-lookup"><span data-stu-id="8b182-231">SceneObject Enumeration</span></span>

<span data-ttu-id="8b182-232">Maintenant que votre application a une scène, votre application va regarder et interagir avec SceneObjects.</span><span class="sxs-lookup"><span data-stu-id="8b182-232">Now that your application has a scene, your application will be looking at and interacting with SceneObjects.</span></span> <span data-ttu-id="8b182-233">Pour ce faire, accédez à la propriété **SceneObjects** :</span><span class="sxs-lookup"><span data-stu-id="8b182-233">This is done by accessing the **SceneObjects** property:</span></span>

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

#### <a name="component-update-and-re-finding-components"></a><span data-ttu-id="8b182-234">Mise à jour des composants et rerecherche de composants</span><span class="sxs-lookup"><span data-stu-id="8b182-234">Component update and re-finding components</span></span>

<span data-ttu-id="8b182-235">Une autre fonction récupère les composants de la scène appelée ***FindComponent***.</span><span class="sxs-lookup"><span data-stu-id="8b182-235">There is another function that retrieves components in the Scene called ***FindComponent***.</span></span> <span data-ttu-id="8b182-236">Cette fonction est utile lors de la mise à jour des objets de suivi et de leur recherche dans des scènes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="8b182-236">This function is useful when updating tracking objects and finding them in subsequent scenes.</span></span> <span data-ttu-id="8b182-237">Le code suivant calcule une nouvelle scène par rapport à une scène précédente, puis trouve le plancher dans la nouvelle scène.</span><span class="sxs-lookup"><span data-stu-id="8b182-237">The following code will compute a new scene relative to a previous scene and then find the floor in the new scene.</span></span>

```cs
// Compute a new scene, but tell the system that we want to compute relative to the previous scene
Scene myNextScene = SceneObserver.Compute(querySettings, 10.0f, myScene);

// Use the Id for the floor we found last time, and find it again
firstFloor = (SceneObject)myNextScene.FindComponent(firstFloor.Id);

if (firstFloor != null)
{
    // We found it again, we can now update the transforms of all objects we attatched to this floor transform
}
```

### <a name="accessing-meshes-and-quads-from-scene-objects"></a><span data-ttu-id="8b182-238">Accès aux maillages et aux quads à partir d’objets de scène</span><span class="sxs-lookup"><span data-stu-id="8b182-238">Accessing Meshes and Quads from Scene Objects</span></span>

<span data-ttu-id="8b182-239">Une fois les SceneObjects trouvés, votre application souhaitera probablement accéder aux données contenues dans n cœurs/maillages dont elle est composée.</span><span class="sxs-lookup"><span data-stu-id="8b182-239">Once SceneObjects have been found your application will most likely want to access the data that is contained n the quads/meshes that it is comprised of.</span></span> <span data-ttu-id="8b182-240">Ces données sont accessibles avec les propriétés quads et meshes.</span><span class="sxs-lookup"><span data-stu-id="8b182-240">This data is accessed with the ***Quads*** and ***Meshes*** properties.</span></span> <span data-ttu-id="8b182-241">Le code suivant énumère tous les Quad et les maillages de notre objet Floor.</span><span class="sxs-lookup"><span data-stu-id="8b182-241">The following code will enumerate all quads and meshes of our floor object.</span></span>

```cs

// Get the matrix for the SceneObject
System.Numerics.Matrix4x4 floorTransform = firstFloor.LocationAsMatrix();

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

<span data-ttu-id="8b182-242">Notez qu’il s’agit du SceneObject qui a la transformation par rapport à l’origine de la scène.</span><span class="sxs-lookup"><span data-stu-id="8b182-242">Notice that it is the SceneObject that has the transform that is relative to the Scene origin.</span></span> <span data-ttu-id="8b182-243">Cela est dû au fait que SceneObject représente une instance d’un «élément» et qu’il est localisable dans l’espace, les Quad et les maillages représentent une géométrie transformée par rapport à leur parent.</span><span class="sxs-lookup"><span data-stu-id="8b182-243">This is because the SceneObject represents an instance of a "thing" and is locatable in space, the quads and meshes represent geometry that is transformed relative to their parent.</span></span> <span data-ttu-id="8b182-244">Il est possible pour des SceneObjects distincts de référencer le même SceneComponewnts SceneMesh/SceneQuad, et il est également possible qu’un SceneObject ait plus d’un SceneMesh/SceneQuad.</span><span class="sxs-lookup"><span data-stu-id="8b182-244">It is possible for separate SceneObjects to reference the same SceneMesh/SceneQuad SceneComponewnts, and it is also possible that a SceneObject has more than one SceneMesh/SceneQuad.</span></span>

### <a name="dealing-with-transforms"></a><span data-ttu-id="8b182-245">Traitement des transformations</span><span class="sxs-lookup"><span data-stu-id="8b182-245">Dealing with Transforms</span></span>

<span data-ttu-id="8b182-246">La compréhension des scènes a fait une tentative délibérée d’alignement avec les représentations de scène 3D traditionnelles lors du traitement des transformations.</span><span class="sxs-lookup"><span data-stu-id="8b182-246">Scene Understanding has made a deliberate attempt to align with traditional 3D scene representations when dealing with transforms.</span></span> <span data-ttu-id="8b182-247">Chaque scène est donc confinée à un système de coordonnées unique, à l’instar des représentations environnementales 3D les plus courantes.</span><span class="sxs-lookup"><span data-stu-id="8b182-247">Each Scene is therefore confined to a single coordinate system much like most common 3D environmental representations.</span></span> <span data-ttu-id="8b182-248">Si votre application traite des scènes qui étendent la limite de ce qu’une origine unique fournit peut ancrer SceneObjects à SpatialAnchors, ou générer plusieurs scènes et les fusionner, mais pour des raisons de simplicité, nous supposons que des scènes étanches existent dans leur propre origine localisée par un NodeId défini par scene:: OriginSpatialGraphNodeId.</span><span class="sxs-lookup"><span data-stu-id="8b182-248">If your application is dealing with Scenes that stretch the limit of what a single origin provides it can anchor SceneObjects to SpatialAnchors, or generate several scenes and merge them together, but for simplicity we assume that watertight scenes exist in their own origin that's localized by one NodeId defined by Scene::OriginSpatialGraphNodeId.</span></span>

<span data-ttu-id="8b182-249">Le code Unity suivant, par exemple, montre comment utiliser la perception Windows et les API Unity pour aligner les systèmes de coordonnées:</span><span class="sxs-lookup"><span data-stu-id="8b182-249">The following unity code, for example, shows how to use windows perception and Unity APIs to align coordinate systems together:</span></span>


```cs
    public static System.Numerics.Matrix4x4? GetSceneToUnityTransform(Guid nodeId)
    {
        System.Numerics.Matrix4x4? sceneToUnityTransform; 
       
        SpatialCoordinateSystem sceneSpatialCoordinateSystem = Windows.Perception.Spatial.Preview.SpatialGraphInteropPreview.CreateCoordinateSystemForNode(nodeId);
        SpatialCoordinateSystem unitySpatialCoordinateSystem = (SpatialCoordinateSystem)System.Runtime.InteropServices.Marshal.GetObjectForIUnknown(UnityEngine.XR.WSA.WorldManager.GetNativeISpatialCoordinateSystemPtr());

        sceneToUnityTransform = sceneSpatialCoordinateSystem.TryGetTransformTo(unitySpatialCoordinateSystem);

        if (sceneToUnityTransform != null)
        {
            sceneToUnityTransform = TransformUtils.ConvertRightHandedMatrix4x4ToLeftHanded(sceneToUnityTransform.Value);
        }
        
        return sceneToUnityTransform;
    }

    // Converts from right-handed to left handed coordinates
    public System.Numerics.Matrix4x4 ConvertRightHandedMatrix4x4ToLeftHanded(System.Numerics.Matrix4x4 transformationMatrix)
    {
        transformationMatrix.M13 = -transformationMatrix.M13;
        transformationMatrix.M23 = -transformationMatrix.M23;
        transformationMatrix.M43 = -transformationMatrix.M43;

        transformationMatrix.M31 = -transformationMatrix.M31;
        transformationMatrix.M32 = -transformationMatrix.M32;
        transformationMatrix.M34 = -transformationMatrix.M34;

        return transformationMatrix;
    }
```

<span data-ttu-id="8b182-250">Et le code suivant appelle cette fonction:</span><span class="sxs-lookup"><span data-stu-id="8b182-250">And the following code calls this function:</span></span>

```cs
System.Numerics.Matrix4x4? sceneToUnityTransform = TransformUtils.GetSceneToUnityTransform(scene.OriginSpatialGraphNodeId);

// Set the root transform
Vector3 t;
Quaternion r;
Vector3 s;

System.Numerics.Matrix4x4.Decompose(sceneToUnityTransform, out s, out r, out t);
SceneRoot.Transform.SetPositionAndRotation(t, r);
```

### <a name="quad"></a><span data-ttu-id="8b182-251">Quadruple</span><span class="sxs-lookup"><span data-stu-id="8b182-251">Quad</span></span>

<span data-ttu-id="8b182-252">Les Quad sont conçus pour faciliter les scénarios de positionnement 2D et doivent être considérés comme des extensions aux éléments d’expérience utilisateur 2D Canvas.</span><span class="sxs-lookup"><span data-stu-id="8b182-252">Quads were designed to facilitate 2D placement scenarios and should be thought of as extensions to 2D canvas UX elements.</span></span> <span data-ttu-id="8b182-253">Alors que les Quad sont des composants de SceneObjects et peuvent être rendus en 3D, les API Quad elles-mêmes partent du principe que les quatre cœurs sont des structures 2D.</span><span class="sxs-lookup"><span data-stu-id="8b182-253">While Quads are components of SceneObjects and can be rendered in 3D, the Quad APIs themselves assume Quads are 2D structures.</span></span> <span data-ttu-id="8b182-254">Elles offrent des informations telles que l’étendue, la forme et fournissent des API pour le positionnement.</span><span class="sxs-lookup"><span data-stu-id="8b182-254">They offer information such as extent, shape, and provide APIs for placement.</span></span>

<span data-ttu-id="8b182-255">Les Quad présentent des étendues rectangulaires, mais elles représentent des surfaces 2D de forme arbitraire.</span><span class="sxs-lookup"><span data-stu-id="8b182-255">Quads have rectangular extents, but they represent arbitrarily shaped 2d surfaces.</span></span> <span data-ttu-id="8b182-256">Pour activer la position sur ces surfaces 2D qui interagissent avec les utilitaires de l’environnement 3D quads, vous pouvez faire en sorte que cette interaction soit possible.</span><span class="sxs-lookup"><span data-stu-id="8b182-256">To enable placement on these 2D surfaces that interact with the 3D environment quads offer utilities to make this interaction possible.</span></span> <span data-ttu-id="8b182-257">Actuellement, la compréhension des scènes fournit deux fonctions telles que **FindCentermostPlacement** et **GetOcclusionMask**.</span><span class="sxs-lookup"><span data-stu-id="8b182-257">Currently Scene Understanding provides two such functions, **FindCentermostPlacement** and **GetOcclusionMask**.</span></span> <span data-ttu-id="8b182-258">FindCentermostPlacement est une API de haut niveau qui localise une position sur le quadruple dans laquelle un objet peut être placé et tente de trouver le meilleur emplacement pour votre objet, garantissant que le cadre englobant que vous fournissez se trouvera sur la surface sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="8b182-258">FindCentermostPlacement is a high level API that locates a position on the quad where an object can be placed and will try to find the best location for your object guaranteeing that the bounding box you provide will reside on the underlying surface.</span></span>

<span data-ttu-id="8b182-259">L’exemple suivant montre comment Rechercher l’emplacement positionnable centermost et ancrer un hologramme au quadruple.</span><span class="sxs-lookup"><span data-stu-id="8b182-259">The following example shows how to find the centermost placeable location and anchor a hologram to the quad.</span></span>

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
                // Step 1: Create a new node QuadTransformNode as a child of Root, and set the transform from quad[0].Transform
                // Step 2: Create your hologram and set it as a child of QuadTransformNode
                // Step 3: Set the QuadTransformNode tranform to a translation (location.x, location.y, 0)
            }
        }
    }
}
```

<span data-ttu-id="8b182-260">Les étapes 1-3 sont fortement dépendantes de votre infrastructure/implémentation particulière, mais les thèmes doivent être similaires.</span><span class="sxs-lookup"><span data-stu-id="8b182-260">Steps 1-3 are highly dependent on your particular framework/implementation, but the themes should be similar.</span></span> <span data-ttu-id="8b182-261">Il est important de noter que le quad n’est généralement pas destiné à être, qu’il représente simplement un plan 2D limité localisé dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="8b182-261">It is important to note that the Quad is not usually intended to be, is just represents a bounded 2D plane that is localized in space.</span></span> <span data-ttu-id="8b182-262">En faisant savoir au moteur/à l’infrastructure où se trouve le quad et en rootant vos objets par rapport au Quad, vos hologrammes se trouveront correctement.</span><span class="sxs-lookup"><span data-stu-id="8b182-262">By having your engine/framework know where the quad is and rooting your objects relative to the quad, your holograms will be located correctly.</span></span> <span data-ttu-id="8b182-263">Pour obtenir des informations plus détaillées, consultez nos exemples sur les quatre cœurs qui présentent des implémentations spécifiques.</span><span class="sxs-lookup"><span data-stu-id="8b182-263">For more detailed information please see our samples on quads which show specific implementations.</span></span>

### <a name="mesh"></a><span data-ttu-id="8b182-264">Déjà</span><span class="sxs-lookup"><span data-stu-id="8b182-264">Mesh</span></span>

<span data-ttu-id="8b182-265">Les maillages représentent les représentations géométriques des objets ou des environnements.</span><span class="sxs-lookup"><span data-stu-id="8b182-265">Meshes represent geometric representations of objects or environments.</span></span> <span data-ttu-id="8b182-266">À l’instar du [mappage spatial](spatial-mapping.md), les données de vertex et d’index de maillage fournies avec chaque maillage de surface spatiale utilisent la même disposition familière que les mémoires tampons de vertex et d’index utilisées pour le rendu des maillages de triangle dans toutes les API de rendu modernes.</span><span class="sxs-lookup"><span data-stu-id="8b182-266">Much like [spatial mapping](spatial-mapping.md), mesh index and vertex data provided with each spatial surface mesh uses the same familiar layout as the vertex and index buffers that are used for rendering triangle meshes in all modern rendering APIs.</span></span> <span data-ttu-id="8b182-267">Les API spécifiques utilisées pour référencer ces données sont les suivantes:</span><span class="sxs-lookup"><span data-stu-id="8b182-267">The specific APIs used to reference this data are as follows:</span></span>

```cs
void GetTriangleIndices(int[] indices);
void GetVertices(float[] vertices);
```

<span data-ttu-id="8b182-268">\* \* Remarque: GetVertices retourne une liste de vertex où chaque 3 tuple de valeurs à virgule flottante représente une coordonnée unique dans l’espace cartésien x, y et z.</span><span class="sxs-lookup"><span data-stu-id="8b182-268">\*\*Note: GetVertices returns a list of vertices where every 3-tuple of floating point values represents a single coordinate in cartesian x,y and z space.</span></span>

<span data-ttu-id="8b182-269">Le code suivant fournit un exemple de génération d’une liste de triangles à partir de la structure de maillage:</span><span class="sxs-lookup"><span data-stu-id="8b182-269">The following code provides an example of generating a triangle list from the mesh structure:</span></span>

```cs
uint[] indices = new uint[mesh.TriangleIndexCount];
float[] positions = new float[mesh.VertexCount * 3];

mesh.GetTriangleIndices(indices);
mesh.GetVertexPositions(positions);
```

<span data-ttu-id="8b182-270">Les mémoires tampons d’index/vertex doivent être > = nombre d’index/vertex, mais peuvent être de taille arbitraire, ce qui permet une réutilisation efficace de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="8b182-270">The index/vertex buffers must be >= the index/vertex counts, but otherwise can be arbitrarily sized allowing for efficient memory re-use.</span></span>

### <a name="developing-with-scene-understandings"></a><span data-ttu-id="8b182-271">Développement avec présentation des scènes</span><span class="sxs-lookup"><span data-stu-id="8b182-271">Developing with Scene Understandings</span></span>

<span data-ttu-id="8b182-272">À ce stade, vous devez comprendre les principaux blocs de construction de la scène présentation du runtime et du kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="8b182-272">At this point you should understand the core building blocks of the Scene Understanding runtime and SDK.</span></span> <span data-ttu-id="8b182-273">La majeure partie de la puissance et de la complexité se trouve dans les modèles d’accès, l’interaction avec les frameworks 3D et les outils qui peuvent être écrits sur ces API pour effectuer des tâches plus avancées, telles que la planification spatiale, l’analyse de la salle, la navigation, la physique, etc. Nous espérons capturer ces exemples dans des exemples qui devraient vous guider dans la bonne direction pour que vos scénarios brillent.</span><span class="sxs-lookup"><span data-stu-id="8b182-273">The bulk of the power and complexity lies in access patterns, interaction with 3d frameworks, and tools that can be written on top of these APIs to perform more advanced tasks like spatial planning, room analysis, navigation, physics etc... We hope to capture these in samples that should hopefully guide you in the proper direction to make your scenarios shine.</span></span> <span data-ttu-id="8b182-274">S’il existe des exemples ou des scénarios que nous n’adressons pas, faites-le nous savoir et nous essaierons de documenter/prototyper ce dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="8b182-274">If there are samples/scenarios we are not addressing, please let us know and we will try to document/prototype what you need.</span></span>

## <a name="see-also"></a><span data-ttu-id="8b182-275">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8b182-275">See also</span></span>

* [<span data-ttu-id="8b182-276">mappage spatial</span><span class="sxs-lookup"><span data-stu-id="8b182-276">spatial mapping</span></span>](spatial-mapping.md)
