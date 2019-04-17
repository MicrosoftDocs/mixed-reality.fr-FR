---
title: Implémenter des lanceurs d’applications 3D (applications UWP)
description: Comment créer des lanceurs d’applications 3D et les logos pour applications UWP de réalité mixte Windows et les jeux (distribués via le Microsoft Store), à la fois sur HoloLens et des casques IMMERSIFS (VR).
author: thmignon
ms.author: thmignon
ms.date: 07/12/2018
ms.topic: article
keywords: 3D, le logo, icône, modélisation, Lanceur, Lanceur 3D, vignette, cube en direct, lien profond, secondarytile, vignette secondaire, UWP
ms.openlocfilehash: 4a8d4a696ff6ef19d7332b20580f1f5ee67bf045
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597028"
---
# <a name="implement-3d-app-launchers-uwp-apps"></a><span data-ttu-id="03e58-104">Implémenter des lanceurs d’applications 3D (applications UWP)</span><span class="sxs-lookup"><span data-stu-id="03e58-104">Implement 3D app launchers (UWP apps)</span></span>

> [!NOTE]
> <span data-ttu-id="03e58-105">Cette fonctionnalité a été ajoutée dans le cadre de 2017 Fall Creators Update (RS3) pour des casques IMMERSIFS et est pris en charge par HoloLens avec les fenêtres de mettre à jour du 10 avril 2018.</span><span class="sxs-lookup"><span data-stu-id="03e58-105">This feature was added as part of the 2017 Fall Creators Update (RS3) for immersive headsets and is supported by HoloLens with the  Windows 10 April 2018 Update.</span></span> <span data-ttu-id="03e58-106">Assurez-vous que votre application cible une version du SDK Windows supérieur ou égal à 10.0.16299 sur des casques IMMERSIFS et 10.0.17125 sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="03e58-106">Make sure your application is targeting a version of the Windows SDK greater than or equal to 10.0.16299 on immersive Headsets and 10.0.17125 on HoloLens.</span></span> <span data-ttu-id="03e58-107">Vous trouverez la dernière version du SDK de Windows [ici](https://developer.microsoft.com/windows/downloads/windows-10-sdk).</span><span class="sxs-lookup"><span data-stu-id="03e58-107">You can find the latest Windows SDK [here](https://developer.microsoft.com/windows/downloads/windows-10-sdk).</span></span>

<span data-ttu-id="03e58-108">Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs arrivent avant de lancer des applications.</span><span class="sxs-lookup"><span data-stu-id="03e58-108">The [Windows Mixed Reality home](navigating-the-windows-mixed-reality-home.md) is the starting point where users land before launching applications.</span></span> <span data-ttu-id="03e58-109">Lorsque vous créez une application UWP pour Windows Mixed Reality, par défaut, les applications sont lancées en tant qu’ardoises 2D avec le logo de leur application.</span><span class="sxs-lookup"><span data-stu-id="03e58-109">When creating a UWP application for Windows Mixed Reality, by default, apps are launched as 2D slates with their app's logo.</span></span> <span data-ttu-id="03e58-110">Lorsque vous développez des expériences pour la réalité mixte Windows, un lanceur 3D peut éventuellement être défini pour remplacer le Lanceur 2D par défaut pour votre application.</span><span class="sxs-lookup"><span data-stu-id="03e58-110">When developing experiences for Windows Mixed Reality, a 3D launcher can optionally be defined to override the default 2D launcher for your application.</span></span> <span data-ttu-id="03e58-111">En règle générale, les lanceurs 3D sont recommandés pour le lancement des applications immersives qui acceptent les utilisateurs d’accéder à Windows Mixed Reality accueil tandis que le Lanceur 2D par défaut est préférable lorsque l’application est activée sur place.</span><span class="sxs-lookup"><span data-stu-id="03e58-111">In general, 3D launchers are recommended for launching immersive applications that take users out of the Windows Mixed Reality home whereas the default 2D launcher is preferred when the app is activated in place.</span></span> <span data-ttu-id="03e58-112">Vous pouvez également créer un [lien profond 3D (secondaryTile)](#3d-deep-links-secondarytiles) comme un lanceur 3D vers du contenu dans une application UWP 2D.</span><span class="sxs-lookup"><span data-stu-id="03e58-112">You can also create a [3D deep link (secondaryTile)](#3d-deep-links-secondarytiles) as a 3D launcher to content within a 2D UWP app.</span></span>

>[!VIDEO https://www.youtube.com/embed/TxIslHsEXno]

## <a name="3d-app-launcher-creation-process"></a><span data-ttu-id="03e58-113">Processus de création de lanceur application 3D</span><span class="sxs-lookup"><span data-stu-id="03e58-113">3D app launcher creation process</span></span>

<span data-ttu-id="03e58-114">Il existe 3 étapes à la création d’un lanceur d’applications 3D :</span><span class="sxs-lookup"><span data-stu-id="03e58-114">There are 3 steps to creating a 3D app launcher:</span></span>
1. [<span data-ttu-id="03e58-115">Conception et concepting</span><span class="sxs-lookup"><span data-stu-id="03e58-115">Designing and concepting</span></span>](3d-app-launcher-design-guidance.md)
2. [<span data-ttu-id="03e58-116">Modélisation et l’exportation</span><span class="sxs-lookup"><span data-stu-id="03e58-116">Modeling and exporting</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. <span data-ttu-id="03e58-117">L’intégration dans votre application (cet article)</span><span class="sxs-lookup"><span data-stu-id="03e58-117">Integrating it into your application (this article)</span></span>

<span data-ttu-id="03e58-118">Composants 3D à utiliser comme lanceurs pour votre application doivent être créés à l’aide de la [recommandations sur la programmation de Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) pour assurer la compatibilité.</span><span class="sxs-lookup"><span data-stu-id="03e58-118">3D assets to be used as launchers for your application should be authored using the [Windows Mixed Reality authoring guidelines](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) to ensure compatibility.</span></span> <span data-ttu-id="03e58-119">Actifs qui ne parviennent pas à répondre à cette spécification création seront affichera pas dans la réalité mixte Windows domestique.</span><span class="sxs-lookup"><span data-stu-id="03e58-119">Assets that fail to meet this authoring specification will not be rendered in the Windows Mixed Reality home.</span></span>

## <a name="configuring-the-3d-launcher"></a><span data-ttu-id="03e58-120">Configuration du Lanceur 3D</span><span class="sxs-lookup"><span data-stu-id="03e58-120">Configuring the 3D launcher</span></span>

<span data-ttu-id="03e58-121">Lorsque vous créez un projet dans Visual Studio, cela a pour effet de créer une vignette par défaut simple qui affiche le nom et le logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="03e58-121">When you create a new project in Visual Studio, it creates a simple default tile that displays your app's name and logo.</span></span> <span data-ttu-id="03e58-122">Pour remplacer cette 2D représentation avec un modèle 3D personnalisé modifier le manifeste d’application de votre application pour inclure l’élément « MixedRealityModel » dans le cadre de votre définition de la vignette par défaut.</span><span class="sxs-lookup"><span data-stu-id="03e58-122">To replace this 2D representation with a custom 3D model edit the app manifest of your application to include the “MixedRealityModel” element as part of your default tile definition.</span></span> <span data-ttu-id="03e58-123">Pour revenir à la 2D Lanceur simplement supprimer la définition de MixedRealityModel à partir du manifeste.</span><span class="sxs-lookup"><span data-stu-id="03e58-123">To revert to the 2D launcher just remove the MixedRealityModel definition from the manifest.</span></span>

### <a name="xml"></a><span data-ttu-id="03e58-124">XML</span><span class="sxs-lookup"><span data-stu-id="03e58-124">XML</span></span>

<span data-ttu-id="03e58-125">Tout d’abord, recherchez le manifeste de package d’application dans votre projet actuel.</span><span class="sxs-lookup"><span data-stu-id="03e58-125">First, locate the app package manifest in your current project.</span></span> <span data-ttu-id="03e58-126">Par défaut, le manifeste sera nommé Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="03e58-126">By default, the manifest will be named Package.appxmanifest.</span></span> <span data-ttu-id="03e58-127">Si vous utilisez Visual Studio, puis cliquez sur le manifeste dans l’Observateur de votre solution et sélectionnez **afficher la source** pour ouvrir le fichier xml pour la modification.</span><span class="sxs-lookup"><span data-stu-id="03e58-127">If you're using Visual Studio, then right-click the manifest in your solution viewer and select **View source** to open the xml for editing.</span></span> 

<span data-ttu-id="03e58-128">En haut du manifeste, ajoutez le schéma uap5 et incluez-le comme un espace de noms peut être ignoré :</span><span class="sxs-lookup"><span data-stu-id="03e58-128">At the top of the manifest, add the uap5 schema and include it as an ignorable namespace:</span></span>

```xml
<Package xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2" 
         xmlns:uap5="http://schemas.microsoft.com/appx/manifest/uap/windows10/5"
         IgnorableNamespaces="uap uap2 uap5 mp"
         xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10">
```

<span data-ttu-id="03e58-129">Ensuite, spécifiez le « MixedRealityModel » dans la mosaïque par défaut de votre application :</span><span class="sxs-lookup"><span data-stu-id="03e58-129">Next specify the "MixedRealityModel" in the default tile for your application:</span></span>

```xml
<Applications>
    <Application Id="App"
      Executable="$targetnametoken$.exe"
      EntryPoint="ExampleApp.App">
      <uap:VisualElements
        DisplayName="ExampleApp"
        Square150x150Logo="Assets\Logo.png"
        Square44x44Logo="Assets\SmallLogo.png"
        Description="ExampleApp"
        BackgroundColor="#464646">
        <uap:DefaultTile Wide310x150Logo="Assets\WideLogo.png" >
          <uap5:MixedRealityModel Path="Assets\My3DTile.glb" />
        </uap:DefaultTile>
        <uap:SplashScreen Image="Assets\SplashScreen.png" />
      </uap:VisualElements>
    </Application>
</Applications>
```

<span data-ttu-id="03e58-130">Les éléments MixedRealityModel accepte un chemin d’accès qui pointe vers une ressource 3D stockée dans votre package d’application.</span><span class="sxs-lookup"><span data-stu-id="03e58-130">The MixedRealityModel elements accepts a file path pointing to a 3D asset stored in your app package.</span></span> <span data-ttu-id="03e58-131">Actuellement des modèles 3D uniquement remis en utilisant le format de fichier .glb et créé sur le [asset 3D de Windows Mixed Reality création instructions](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="03e58-131">Currently only 3D models delivered using the .glb file format and authored against the [Windows Mixed Reality 3D asset authoring instructions](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) are supported.</span></span> <span data-ttu-id="03e58-132">Ressources doivent être stockées dans le package d’application et animation n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="03e58-132">Assets must be stored in the app package and animation is not currently supported.</span></span> <span data-ttu-id="03e58-133">Si le paramètre « Chemin » est vide, Windows affiche l’ardoise 2D au lieu du Lanceur 3D.</span><span class="sxs-lookup"><span data-stu-id="03e58-133">If the “Path” parameter is left blank Windows will show the 2D slate instead of the 3D launcher.</span></span> <span data-ttu-id="03e58-134">**Remarque :** la ressource .glb doit être marquée comme « Contenu » dans vos paramètres de build avant de générer et exécuter votre application.</span><span class="sxs-lookup"><span data-stu-id="03e58-134">**Note:** the .glb asset must be marked as "Content" in your build settings before building and running your app.</span></span>


<span data-ttu-id="03e58-135">![Sélectionnez le .glb dans l’Explorateur de solutions et utiliser la section des propriétés pour marquer en tant que « Contenu » dans les paramètres de build](images/buildsetting-content-300px.png)</span><span class="sxs-lookup"><span data-stu-id="03e58-135">![Select the .glb in your solution explorer and use the properties section to mark it as "Content" in the build settings](images/buildsetting-content-300px.png)</span></span><br>
<span data-ttu-id="03e58-136">*Sélectionnez le .glb dans l’Explorateur de solutions et utiliser la section des propriétés pour marquer en tant que « Contenu » dans les paramètres de build*</span><span class="sxs-lookup"><span data-stu-id="03e58-136">*Select the .glb in your solution explorer and use the properties section to mark it as "Content" in the build settings*</span></span>

### <a name="bounding-box"></a><span data-ttu-id="03e58-137">Cadre englobant</span><span class="sxs-lookup"><span data-stu-id="03e58-137">Bounding box</span></span>

<span data-ttu-id="03e58-138">Un rectangle englobant peut être utilisé pour éventuellement ajouter une région de mémoire tampon supplémentaire autour de l’objet.</span><span class="sxs-lookup"><span data-stu-id="03e58-138">A bounding box can be used to optionally add an additional buffer region around the object.</span></span> <span data-ttu-id="03e58-139">La zone englobante est spécifiée à l’aide d’un point central et les extensions qui indiquent la distance entre le centre du rectangle englobant et ses bords chaque axe.</span><span class="sxs-lookup"><span data-stu-id="03e58-139">The bounding box is specified using a center point and extents which indicate the distance from the center of the bounding box to its edges along each axis.</span></span> <span data-ttu-id="03e58-140">Unités pour la zone englobante peuvent être mappées à 1 unité = 1 mètre.</span><span class="sxs-lookup"><span data-stu-id="03e58-140">Units for the bounding box can be mapped to 1 unit = 1 meter.</span></span> <span data-ttu-id="03e58-141">Si un rectangle englobant n’est pas fourni puis une sera être ajustée automatiquement à la maille de l’objet.</span><span class="sxs-lookup"><span data-stu-id="03e58-141">If a bounding box is not provided then one will be automatically fitted to the mesh of the object.</span></span> <span data-ttu-id="03e58-142">Si la zone englobante fournie est plus petite que le modèle puis, il est redimensionné pour s’ajuster à la maille.</span><span class="sxs-lookup"><span data-stu-id="03e58-142">If the provided bounding box is smaller than the model then it will be resized to fit the mesh.</span></span>

<span data-ttu-id="03e58-143">Prise en charge pour l’attribut de zone englobante proviendront avec la mise à jour Windows RS4 en tant que propriété sur l’élément MixedRealityModel.</span><span class="sxs-lookup"><span data-stu-id="03e58-143">Support for the bounding box attribute will come with the Windows RS4 update as a property on the MixedRealityModel element.</span></span> <span data-ttu-id="03e58-144">Pour définir un rectangle englobant de tout d’abord en haut de l’application manifeste ajouter le schéma uap6 et l’inclure en tant que des espaces de noms peut être ignoré :</span><span class="sxs-lookup"><span data-stu-id="03e58-144">To define a bounding box first at the top of the app manifest add the uap6 schema and include it them as ignorable namespaces:</span></span>

```xml
<Package xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2" 
         xmlns:uap5="http://schemas.microsoft.com/appx/manifest/uap/windows10/5"
         xmlns:uap6="http://schemas.microsoft.com/appx/manifest/uap/windows10/6"
         IgnorableNamespaces="uap uap2 uap5 uap6 mp"
         xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10">
```
<span data-ttu-id="03e58-145">Ensuite, dans le MixedRealityModel définie la propriété SpatialBoundingBox pour définir la zone englobante :</span><span class="sxs-lookup"><span data-stu-id="03e58-145">Next, on the MixedRealityModel set the SpatialBoundingBox property to define the bounding box:</span></span> 

```xml
        <uap:DefaultTile Wide310x150Logo="Assets\WideLogo.png" >
          <uap5:MixedRealityModel Path="Assets\My3DTile.glb">
              <uap6:SpatialBoundingBox  Center=”1,-2,3” Extents=”1,2,3” />
          </uap5:MixedRealityModel>
        </uap:DefaultTile>
```

### <a name="using-unity"></a><span data-ttu-id="03e58-146">À l’aide de Unity</span><span class="sxs-lookup"><span data-stu-id="03e58-146">Using Unity</span></span>

<span data-ttu-id="03e58-147">Lorsque vous travaillez avec Unity, le projet doit être créé et ouvert dans Visual Studio avant de pouvoir modifier le manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="03e58-147">When working with Unity the project must be built and opened in Visual Studio before the App Manifest can be edited.</span></span> 

>[!NOTE]
><span data-ttu-id="03e58-148">Le Lanceur 3D doit être redéfini dans le manifeste pour créer et déployer une nouvelle solution Visual Studio à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="03e58-148">The 3D launcher must be redefined in the manifest when building and deploying a new Visual Studio solution from Unity.</span></span>

## <a name="3d-deep-links-secondarytiles"></a><span data-ttu-id="03e58-149">Profondeur 3D lie (secondaryTiles)</span><span class="sxs-lookup"><span data-stu-id="03e58-149">3D deep links (secondaryTiles)</span></span>

> [!NOTE]
> <span data-ttu-id="03e58-150">Cette fonctionnalité a été ajoutée dans le cadre de 2017 Fall Creators Update (RS3) pour des casques IMMERSIFS (VR) et dans le cadre de l’avril 2018 mise à jour (RS4) pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="03e58-150">This feature was added as part of the 2017 Fall Creators Update (RS3) for immersive (VR) headsets and as part of the April 2018 Update (RS4) for HoloLens.</span></span> <span data-ttu-id="03e58-151">Assurez-vous que votre application cible une version du SDK Windows supérieur ou égal à 10.0.16299 sur des casques IMMERSIFS (VR) et 10.0.17125 sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="03e58-151">Make sure your application is targeting a version of the Windows SDK greater than or equal to 10.0.16299 on immersive (VR) headsets and 10.0.17125 on HoloLens.</span></span> <span data-ttu-id="03e58-152">Vous trouverez la dernière version du SDK de Windows [ici](https://developer.microsoft.com/windows/downloads/windows-10-sdk).</span><span class="sxs-lookup"><span data-stu-id="03e58-152">You can find the latest Windows SDK [here](https://developer.microsoft.com/windows/downloads/windows-10-sdk).</span></span>

>[!IMPORTANT]
><span data-ttu-id="03e58-153">Liens ciblés 3D (secondaryTiles) fonctionnent uniquement avec les applications UWP 2D.</span><span class="sxs-lookup"><span data-stu-id="03e58-153">3D deep links (secondaryTiles) only work with 2D UWP apps.</span></span> <span data-ttu-id="03e58-154">Vous pouvez, cependant, créer un [Lanceur d’applications 3D](implementing-3d-app-launchers.md) pour lancer une application exclusive à partir de Windows Mixed Reality domestique.</span><span class="sxs-lookup"><span data-stu-id="03e58-154">You can, however, create a [3D app launcher](implementing-3d-app-launchers.md) to launch an exclusive app from the Windows Mixed Reality home.</span></span>

<span data-ttu-id="03e58-155">Vos applications 2D peuvent être améliorées pour la réalité mixte Windows en ajoutant la possibilité de placer des modèles 3D à partir de votre application dans le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) en tant que liens ciblés vers du contenu dans votre application 2D, tout comme [secondaire 2D vignettes](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-secondary-tiles) dans le menu Démarrer de Windows.</span><span class="sxs-lookup"><span data-stu-id="03e58-155">Your 2D applications can be enhanced for Windows Mixed Reality by adding the ability to place 3D models from your app into the [Windows Mixed Reality home](navigating-the-windows-mixed-reality-home.md) as deep links to content within your 2D app, just like [2D secondary tiles](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-secondary-tiles) on the Windows Start menu.</span></span> <span data-ttu-id="03e58-156">Par exemple, vous pouvez créer photospheres 360° lier directement dans une application de visionneuse de photos de 360°, ou permettent aux utilisateurs de placer du contenu 3D à partir d’une collection de ressources qui ouvre une page de détails à propos de l’auteur.</span><span class="sxs-lookup"><span data-stu-id="03e58-156">For example, you can create 360° photospheres that link directly into a 360° photo viewer app, or let users place 3D content from a collection of assets that opens a details page about the author.</span></span> <span data-ttu-id="03e58-157">Voici quelques façons d’étendre les fonctionnalités de votre application 2D avec du contenu 3D.</span><span class="sxs-lookup"><span data-stu-id="03e58-157">These are just a couple ways to expand the functionality of your 2D application with 3D content.</span></span>

### <a name="creating-a-3d-secondarytile"></a><span data-ttu-id="03e58-158">Création d’une « secondaryTile » 3D</span><span class="sxs-lookup"><span data-stu-id="03e58-158">Creating a 3D “secondaryTile”</span></span>

<span data-ttu-id="03e58-159">Vous pouvez placer du contenu 3D à partir de votre application à l’aide de « secondaryTiles » en définissant un modèle de réalité mixte lors de la création.</span><span class="sxs-lookup"><span data-stu-id="03e58-159">You can place 3D content from your application using “secondaryTiles” by defining a mixed reality model at creation time.</span></span> <span data-ttu-id="03e58-160">Modèles de réalité mixte sont créés en faisant référence à une ressource 3D dans votre package d’application et éventuellement définir un rectangle englobant.</span><span class="sxs-lookup"><span data-stu-id="03e58-160">Mixed reality models are created by referencing a 3D asset in your app package and optionally defining a bounding box.</span></span> 

> [!NOTE]
> <span data-ttu-id="03e58-161">Création de « secondaryTiles » à partir de dans une vue exclusive n’est pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="03e58-161">Creating “secondaryTiles” from within an exclusive view is not currently supported.</span></span>

```cs
using Windows.UI.StartScreen;
using Windows.Foundation.Numerics;
using Windows.Perception.Spatial;

// Initialize the tile
SecondaryTile tile = new SecondaryTile("myTileId")
{
    DisplayName = "My Tile",
    Arguments = "myArgs"
};

tile.VisualElements.Square150x150Logo = new Uri("ms-appx:///Assets/MyTile/Square150x150Logo.png");

//Assign 3D model (only ms-appx and ms-appdata are allowed)
TileMixedRealityModel model = tile.VisualElements.MixedRealityModel;
model.Uri = new Uri("ms-appx:///Assets/MyTile/MixedRealityModel.glb");
model.ActivationBehavior = TileMixedRealityModelActivationBehavior.Default;
model.BoundingBox = new SpatialBoundingBox
{
    Center = new Vector3 { X = 1, Y = 0, Z = 0 },
    Extents = new Vector3 { X = 3, Y = 5, Z = 4 }
};

// And place it
await tile.RequestCreateAsync();
```

### <a name="bounding-box"></a><span data-ttu-id="03e58-162">Cadre englobant</span><span class="sxs-lookup"><span data-stu-id="03e58-162">Bounding box</span></span>

<span data-ttu-id="03e58-163">Un rectangle englobant peut être utilisé pour ajouter une région de mémoire tampon supplémentaire autour de l’objet.</span><span class="sxs-lookup"><span data-stu-id="03e58-163">A bounding box can be used to add an additional buffer region around the object.</span></span> <span data-ttu-id="03e58-164">La zone englobante est spécifiée à l’aide d’un point central et les extensions qui indiquent la distance entre le centre du rectangle englobant et ses bords chaque axe.</span><span class="sxs-lookup"><span data-stu-id="03e58-164">The bounding box is specified using a center point and extents which indicate the distance from the center of the bounding box to its edges along each axis.</span></span> <span data-ttu-id="03e58-165">Unités pour la zone englobante peuvent être mappées à 1 unité = 1 mètre.</span><span class="sxs-lookup"><span data-stu-id="03e58-165">Units for the bounding box can be mapped to 1 unit = 1 meter.</span></span> <span data-ttu-id="03e58-166">Si un rectangle englobant n’est pas fourni puis une sera être ajustée automatiquement à la maille de l’objet.</span><span class="sxs-lookup"><span data-stu-id="03e58-166">If a bounding box is not provided then one will be automatically fitted to the mesh of the object.</span></span> <span data-ttu-id="03e58-167">Si la zone englobante fournie est plus petite que le modèle puis, il est redimensionné pour s’ajuster à la maille.</span><span class="sxs-lookup"><span data-stu-id="03e58-167">If the provided bounding box is smaller than the model then it will be resized to fit the mesh.</span></span>

### <a name="activation-behavior"></a><span data-ttu-id="03e58-168">Comportement d’activation</span><span class="sxs-lookup"><span data-stu-id="03e58-168">Activation behavior</span></span>

> [!NOTE]
> <span data-ttu-id="03e58-169">Cette fonctionnalité sera pris en charge à compter de la mise à jour Windows RS4.</span><span class="sxs-lookup"><span data-stu-id="03e58-169">This feature will be supported as of the Windows RS4 update.</span></span> <span data-ttu-id="03e58-170">Assurez-vous que votre application cible une version du SDK Windows supérieure ou égale à 10.0.17125 si vous envisagez d’utiliser cette fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="03e58-170">Make sure your application is targeting a version of the Windows SDK greater than or equal to 10.0.17125 if you plan to use this feature</span></span>

<span data-ttu-id="03e58-171">Vous pouvez définir le comportement d’activation pour une secondaryTile 3D contrôler comment il réagit lorsqu’un utilisateur le sélectionne.</span><span class="sxs-lookup"><span data-stu-id="03e58-171">You can define the activation behavior for a 3D secondaryTile to control how it reacts when a user selects it.</span></span> <span data-ttu-id="03e58-172">Cela permet de placer des objets 3D dans la réalité mixte domestique qui sont purley informative ou décoratif.</span><span class="sxs-lookup"><span data-stu-id="03e58-172">This can be used to place 3D objects in the Mixed Reality home that are purley informative or decorative.</span></span> <span data-ttu-id="03e58-173">Les types de comportement d’activation suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="03e58-173">The following activation behavior types are supported:</span></span>
1. <span data-ttu-id="03e58-174">Default : Lorsqu’un utilisateur sélectionne la secondaryTile 3D l’application est activée</span><span class="sxs-lookup"><span data-stu-id="03e58-174">Default: When a user selects the 3D secondaryTile the app is activated</span></span>
2. <span data-ttu-id="03e58-175">None : Lorsque l’utilisateur sélectionne la secondaryTile 3D, rien ne se produit et l’application n’est pas activé.</span><span class="sxs-lookup"><span data-stu-id="03e58-175">None: When the users selects the 3D secondaryTile nothing happens and the app is not activated.</span></span>

### <a name="obtaining-and-updating-an-existing-secondarytile"></a><span data-ttu-id="03e58-176">Obtention et la mise à jour une instance existante de « secondaryTile »</span><span class="sxs-lookup"><span data-stu-id="03e58-176">Obtaining and updating an existing “secondaryTile”</span></span>

<span data-ttu-id="03e58-177">Les développeurs peuvent obtenir une liste de leurs vignettes secondaires existantes, ce qui inclut les propriétés qui ont été spécifiées précédemment.</span><span class="sxs-lookup"><span data-stu-id="03e58-177">Developers can get back a list of their existing secondary tiles, which includes the properties that they previously specified.</span></span> <span data-ttu-id="03e58-178">Ils peuvent également mettre à jour les propriétés en modifiant la valeur, puis UpdateAsync().</span><span class="sxs-lookup"><span data-stu-id="03e58-178">They can also update the properties by changing the value and then calling UpdateAsync().</span></span>

```cs
// Grab the existing secondary tile
SecondaryTile tile = (await SecondaryTile.FindAllAsync()).First();

Uri updatedUri = new Uri("ms-appdata:///local/MixedRealityUpdated.glb");

// See if the model needs updating
if (!tile.VisualElements.MixedRealityModel.Uri.Equals(updatedUri))
{
    // Update it
    tile.VisualElements.MixedRealityModel.Uri = updatedUri;

    // And apply the changes
    await tile.UpdateAsync();
}
```

### <a name="checking-that-the-user-is-in-windows-mixed-reality"></a><span data-ttu-id="03e58-179">Vérification que l’utilisateur est en réalité mixte Windows</span><span class="sxs-lookup"><span data-stu-id="03e58-179">Checking that the user is in Windows Mixed Reality</span></span>

<span data-ttu-id="03e58-180">Liens ciblés 3D (secondaryTiles) peuvent uniquement être créés alors que la vue est affichée dans un casque Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="03e58-180">3D deep links (secondaryTiles) can only be created while the view is being displayed in a Windows Mixed Reality headset.</span></span> <span data-ttu-id="03e58-181">Lorsque votre vue n’est pas en cours de présentation dans un casque Windows Mixed Reality, nous vous recommandons d’envisageable normalement en masquant le point d’entrée ou en affichant un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="03e58-181">When your view isn't being presented in a Windows Mixed Reality headset we recommend gracefully handling this by either hiding the entry point or showing an error message.</span></span> <span data-ttu-id="03e58-182">Vous pouvez le vérifier en interrogeant [IsCurrentViewPresentedOnHolographic()](https://docs.microsoft.com/uwp/api/windows.applicationmodel.preview.holographic.holographicapplicationpreview#Windows_ApplicationModel_Preview_Holographic_HolographicApplicationPreview_IsCurrentViewPresentedOnHolographicDisplay_).</span><span class="sxs-lookup"><span data-stu-id="03e58-182">You can check this by querying [IsCurrentViewPresentedOnHolographic()](https://docs.microsoft.com/uwp/api/windows.applicationmodel.preview.holographic.holographicapplicationpreview#Windows_ApplicationModel_Preview_Holographic_HolographicApplicationPreview_IsCurrentViewPresentedOnHolographicDisplay_).</span></span>

## <a name="tile-notifications"></a><span data-ttu-id="03e58-183">Notifications par vignette</span><span class="sxs-lookup"><span data-stu-id="03e58-183">Tile notifications</span></span>

<span data-ttu-id="03e58-184">Notifications de vignette ne gèrent pas actuellement envoyer une mise à jour avec la ressource de 3D.</span><span class="sxs-lookup"><span data-stu-id="03e58-184">Tile notifications do not currently support sending an update with a 3D asset.</span></span> <span data-ttu-id="03e58-185">Cela signifie que les développeurs ne sera pas en mesure d’effectuer les opérations suivantes</span><span class="sxs-lookup"><span data-stu-id="03e58-185">This means that developers will not be able to do the following</span></span>
* <span data-ttu-id="03e58-186">Notifications push</span><span class="sxs-lookup"><span data-stu-id="03e58-186">Push Notifications</span></span>
* <span data-ttu-id="03e58-187">Interrogation périodique</span><span class="sxs-lookup"><span data-stu-id="03e58-187">Periodic Polling</span></span>
* <span data-ttu-id="03e58-188">Notifications planifiées</span><span class="sxs-lookup"><span data-stu-id="03e58-188">Scheduled Notifications</span></span>

<span data-ttu-id="03e58-189">Pour plus d’informations sur les autres vignettes de fonctionnalités et d’attributs et comment ils sont utilisés pour les vignettes 2D font référence à la [vignettes pour documentation UWP Apps](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-creating-tiles).</span><span class="sxs-lookup"><span data-stu-id="03e58-189">For more information on the other tiles features and attributes and how they are used for 2D tiles refer to the [Tiles for UWP Apps documentation](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-creating-tiles).</span></span>

## <a name="see-also"></a><span data-ttu-id="03e58-190">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="03e58-190">See also</span></span>

* <span data-ttu-id="03e58-191">[Exemple de modèle de réalité mixte](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) contenant un lanceur d’applications 3D.</span><span class="sxs-lookup"><span data-stu-id="03e58-191">[Mixed reality model sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) containing a 3D app launcher.</span></span>
* [<span data-ttu-id="03e58-192">Guide de conception du Lanceur d’application 3D</span><span class="sxs-lookup"><span data-stu-id="03e58-192">3D app launcher design guidance</span></span>](3d-app-launcher-design-guidance.md)
* [<span data-ttu-id="03e58-193">Création de modèles 3D pour une utilisation dans la page d’accueil Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="03e58-193">Creating 3D models for use in the Windows Mixed Reality home</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [<span data-ttu-id="03e58-194">Implémentation des lanceurs d’applications 3D (applications Win32)</span><span class="sxs-lookup"><span data-stu-id="03e58-194">Implementing 3D app launchers (Win32 apps)</span></span>](implementing-3d-app-launchers-win32.md)
* [<span data-ttu-id="03e58-195">Navigation dans Windows Mixed Reality domestique</span><span class="sxs-lookup"><span data-stu-id="03e58-195">Navigating the Windows Mixed Reality home</span></span>](navigating-the-windows-mixed-reality-home.md)
