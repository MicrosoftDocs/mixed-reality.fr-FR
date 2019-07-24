---
title: Implémenter des lanceurs d’applications en 3D (applications UWP)
description: Comment créer des programmes de lancement et des logos d’applications en 3D pour des applications et des jeux UWP Windows Mixed Reality (distribués via le Microsoft Store), à la fois sur des casques HoloLens et immersif (VR).
author: thmignon
ms.author: thmignon
ms.date: 07/12/2018
ms.topic: article
keywords: 3D, logo, icône, modélisation, lanceur, lanceur 3D, vignette, cube dynamique, lien profond, secondarytile, vignette secondaire, UWP
ms.openlocfilehash: 4a8d4a696ff6ef19d7332b20580f1f5ee67bf045
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63516743"
---
# <a name="implement-3d-app-launchers-uwp-apps"></a><span data-ttu-id="9af62-104">Implémenter des lanceurs d’applications en 3D (applications UWP)</span><span class="sxs-lookup"><span data-stu-id="9af62-104">Implement 3D app launchers (UWP apps)</span></span>

> [!NOTE]
> <span data-ttu-id="9af62-105">Cette fonctionnalité a été ajoutée dans le cadre de la mise à jour 2017 automne Creators (RS3) pour les casques immersifs et est prise en charge par HoloLens avec la mise à jour 2018 d’avril de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9af62-105">This feature was added as part of the 2017 Fall Creators Update (RS3) for immersive headsets and is supported by HoloLens with the  Windows 10 April 2018 Update.</span></span> <span data-ttu-id="9af62-106">Assurez-vous que votre application cible une version du SDK Windows supérieure ou égale à 10.0.16299 sur les casques immersifs et 10.0.17125 sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9af62-106">Make sure your application is targeting a version of the Windows SDK greater than or equal to 10.0.16299 on immersive Headsets and 10.0.17125 on HoloLens.</span></span> <span data-ttu-id="9af62-107">Vous trouverez les SDK Windows les plus récentes [ici](https://developer.microsoft.com/windows/downloads/windows-10-sdk).</span><span class="sxs-lookup"><span data-stu-id="9af62-107">You can find the latest Windows SDK [here](https://developer.microsoft.com/windows/downloads/windows-10-sdk).</span></span>

<span data-ttu-id="9af62-108">La [base de la réalité Windows Mixed](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs se trouvent avant de lancer des applications.</span><span class="sxs-lookup"><span data-stu-id="9af62-108">The [Windows Mixed Reality home](navigating-the-windows-mixed-reality-home.md) is the starting point where users land before launching applications.</span></span> <span data-ttu-id="9af62-109">Lors de la création d’une application UWP pour Windows Mixed Reality, par défaut, les applications sont lancées en tant qu’ardoise 2D avec le logo de leur application.</span><span class="sxs-lookup"><span data-stu-id="9af62-109">When creating a UWP application for Windows Mixed Reality, by default, apps are launched as 2D slates with their app's logo.</span></span> <span data-ttu-id="9af62-110">Lors du développement d’expériences pour Windows Mixed Reality, un lanceur 3D peut éventuellement être défini pour remplacer le lanceur 2D par défaut de votre application.</span><span class="sxs-lookup"><span data-stu-id="9af62-110">When developing experiences for Windows Mixed Reality, a 3D launcher can optionally be defined to override the default 2D launcher for your application.</span></span> <span data-ttu-id="9af62-111">En général, les lanceurs 3D sont recommandés pour lancer des applications immersifs qui utilisent les utilisateurs hors de Windows Mixed Reality, tandis que le lanceur 2D par défaut est préféré quand l’application est activée sur place.</span><span class="sxs-lookup"><span data-stu-id="9af62-111">In general, 3D launchers are recommended for launching immersive applications that take users out of the Windows Mixed Reality home whereas the default 2D launcher is preferred when the app is activated in place.</span></span> <span data-ttu-id="9af62-112">Vous pouvez également créer un [lien profond en 3D (secondaryTile)](#3d-deep-links-secondarytiles) en tant que lanceur en 3D pour le contenu d’une application UWP 2D.</span><span class="sxs-lookup"><span data-stu-id="9af62-112">You can also create a [3D deep link (secondaryTile)](#3d-deep-links-secondarytiles) as a 3D launcher to content within a 2D UWP app.</span></span>

>[!VIDEO https://www.youtube.com/embed/TxIslHsEXno]

## <a name="3d-app-launcher-creation-process"></a><span data-ttu-id="9af62-113">processus de création du lanceur d’applications 3D</span><span class="sxs-lookup"><span data-stu-id="9af62-113">3D app launcher creation process</span></span>

<span data-ttu-id="9af62-114">La création d’un lanceur d’applications 3D comporte trois étapes:</span><span class="sxs-lookup"><span data-stu-id="9af62-114">There are 3 steps to creating a 3D app launcher:</span></span>
1. [<span data-ttu-id="9af62-115">Conception et concept</span><span class="sxs-lookup"><span data-stu-id="9af62-115">Designing and concepting</span></span>](3d-app-launcher-design-guidance.md)
2. [<span data-ttu-id="9af62-116">Modélisation et exportation</span><span class="sxs-lookup"><span data-stu-id="9af62-116">Modeling and exporting</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. <span data-ttu-id="9af62-117">Intégration dans votre application (cet article)</span><span class="sxs-lookup"><span data-stu-id="9af62-117">Integrating it into your application (this article)</span></span>

<span data-ttu-id="9af62-118">les ressources 3D à utiliser comme lanceurs pour votre application doivent être créées à l’aide des [instructions de création Windows Mixed realisation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) pour garantir la compatibilité.</span><span class="sxs-lookup"><span data-stu-id="9af62-118">3D assets to be used as launchers for your application should be authored using the [Windows Mixed Reality authoring guidelines](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) to ensure compatibility.</span></span> <span data-ttu-id="9af62-119">Les ressources qui ne satisfont pas à cette spécification de création ne seront pas affichées dans la page d’hébergement de la réalité mixte Windows.</span><span class="sxs-lookup"><span data-stu-id="9af62-119">Assets that fail to meet this authoring specification will not be rendered in the Windows Mixed Reality home.</span></span>

## <a name="configuring-the-3d-launcher"></a><span data-ttu-id="9af62-120">Configuration du lanceur 3D</span><span class="sxs-lookup"><span data-stu-id="9af62-120">Configuring the 3D launcher</span></span>

<span data-ttu-id="9af62-121">Lorsque vous créez un projet dans Visual Studio, cela a pour effet de créer une vignette par défaut simple qui affiche le nom et le logo de votre application.</span><span class="sxs-lookup"><span data-stu-id="9af62-121">When you create a new project in Visual Studio, it creates a simple default tile that displays your app's name and logo.</span></span> <span data-ttu-id="9af62-122">Pour remplacer cette représentation 2D par un modèle 3D personnalisé, modifiez le manifeste d’application de votre application de manière à inclure l’élément «MixedRealityModel» dans le cadre de votre définition de vignette par défaut.</span><span class="sxs-lookup"><span data-stu-id="9af62-122">To replace this 2D representation with a custom 3D model edit the app manifest of your application to include the “MixedRealityModel” element as part of your default tile definition.</span></span> <span data-ttu-id="9af62-123">Pour revenir au lanceur 2D, supprimez simplement la définition MixedRealityModel du manifeste.</span><span class="sxs-lookup"><span data-stu-id="9af62-123">To revert to the 2D launcher just remove the MixedRealityModel definition from the manifest.</span></span>

### <a name="xml"></a><span data-ttu-id="9af62-124">XML</span><span class="sxs-lookup"><span data-stu-id="9af62-124">XML</span></span>

<span data-ttu-id="9af62-125">Tout d’abord, recherchez le manifeste du package d’application dans votre projet actuel.</span><span class="sxs-lookup"><span data-stu-id="9af62-125">First, locate the app package manifest in your current project.</span></span> <span data-ttu-id="9af62-126">Par défaut, le manifeste sera nommé Package. appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="9af62-126">By default, the manifest will be named Package.appxmanifest.</span></span> <span data-ttu-id="9af62-127">Si vous utilisez Visual Studio, cliquez avec le bouton droit sur le manifeste dans votre afficheur de solution, puis sélectionnez **afficher la source** pour ouvrir le fichier XML à modifier.</span><span class="sxs-lookup"><span data-stu-id="9af62-127">If you're using Visual Studio, then right-click the manifest in your solution viewer and select **View source** to open the xml for editing.</span></span> 

<span data-ttu-id="9af62-128">En haut du manifeste, ajoutez le schéma uap5 et incluez-le en tant qu’espace de noms pouvant être ignoré:</span><span class="sxs-lookup"><span data-stu-id="9af62-128">At the top of the manifest, add the uap5 schema and include it as an ignorable namespace:</span></span>

```xml
<Package xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2" 
         xmlns:uap5="http://schemas.microsoft.com/appx/manifest/uap/windows10/5"
         IgnorableNamespaces="uap uap2 uap5 mp"
         xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10">
```

<span data-ttu-id="9af62-129">Spécifiez ensuite la valeur «MixedRealityModel» dans la vignette par défaut de votre application:</span><span class="sxs-lookup"><span data-stu-id="9af62-129">Next specify the "MixedRealityModel" in the default tile for your application:</span></span>

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

<span data-ttu-id="9af62-130">Les éléments MixedRealityModel acceptent un chemin d’accès de fichier pointant vers une ressource 3D stockée dans votre package d’application.</span><span class="sxs-lookup"><span data-stu-id="9af62-130">The MixedRealityModel elements accepts a file path pointing to a 3D asset stored in your app package.</span></span> <span data-ttu-id="9af62-131">Actuellement, seuls les modèles 3D fournis à l’aide du format de fichier. GLB et créés par rapport aux [instructions de création de ressources 3D Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9af62-131">Currently only 3D models delivered using the .glb file format and authored against the [Windows Mixed Reality 3D asset authoring instructions](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) are supported.</span></span> <span data-ttu-id="9af62-132">Les ressources doivent être stockées dans le package d’application et l’animation n’est pas prise en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="9af62-132">Assets must be stored in the app package and animation is not currently supported.</span></span> <span data-ttu-id="9af62-133">Si le paramètre «Path» est laissé vide, Windows affiche la ardoise 2D au lieu du lanceur 3D.</span><span class="sxs-lookup"><span data-stu-id="9af62-133">If the “Path” parameter is left blank Windows will show the 2D slate instead of the 3D launcher.</span></span> <span data-ttu-id="9af62-134">**Remarque:** la ressource. GLB doit être marquée comme «contenu» dans vos paramètres de génération avant de générer et d’exécuter votre application.</span><span class="sxs-lookup"><span data-stu-id="9af62-134">**Note:** the .glb asset must be marked as "Content" in your build settings before building and running your app.</span></span>


<span data-ttu-id="9af62-135">![Sélectionnez le. GLB dans votre Explorateur de solutions et utilisez la section Propriétés pour le marquer comme «contenu» dans les paramètres de génération.](images/buildsetting-content-300px.png)</span><span class="sxs-lookup"><span data-stu-id="9af62-135">![Select the .glb in your solution explorer and use the properties section to mark it as "Content" in the build settings](images/buildsetting-content-300px.png)</span></span><br>
<span data-ttu-id="9af62-136">*Sélectionnez le. GLB dans votre Explorateur de solutions et utilisez la section Propriétés pour le marquer comme «contenu» dans les paramètres de génération.*</span><span class="sxs-lookup"><span data-stu-id="9af62-136">*Select the .glb in your solution explorer and use the properties section to mark it as "Content" in the build settings*</span></span>

### <a name="bounding-box"></a><span data-ttu-id="9af62-137">Cadre englobant</span><span class="sxs-lookup"><span data-stu-id="9af62-137">Bounding box</span></span>

<span data-ttu-id="9af62-138">Un cadre englobant peut être utilisé pour ajouter éventuellement une zone de mémoire tampon supplémentaire autour de l’objet.</span><span class="sxs-lookup"><span data-stu-id="9af62-138">A bounding box can be used to optionally add an additional buffer region around the object.</span></span> <span data-ttu-id="9af62-139">Le cadre englobant est spécifié à l’aide d’un point central et d’étendues qui indiquent la distance entre le centre du rectangle englobant et ses bords le long de chaque axe.</span><span class="sxs-lookup"><span data-stu-id="9af62-139">The bounding box is specified using a center point and extents which indicate the distance from the center of the bounding box to its edges along each axis.</span></span> <span data-ttu-id="9af62-140">Les unités du cadre englobant peuvent être mappées à 1 unité = 1 mètre.</span><span class="sxs-lookup"><span data-stu-id="9af62-140">Units for the bounding box can be mapped to 1 unit = 1 meter.</span></span> <span data-ttu-id="9af62-141">Si aucun cadre englobant n’est fourni, l’un d’eux est automatiquement ajusté à la maille de l’objet.</span><span class="sxs-lookup"><span data-stu-id="9af62-141">If a bounding box is not provided then one will be automatically fitted to the mesh of the object.</span></span> <span data-ttu-id="9af62-142">Si le cadre englobant fourni est plus petit que le modèle, il sera redimensionné pour s’ajuster à la maille.</span><span class="sxs-lookup"><span data-stu-id="9af62-142">If the provided bounding box is smaller than the model then it will be resized to fit the mesh.</span></span>

<span data-ttu-id="9af62-143">La prise en charge de l’attribut cadre englobant sera fournie avec la mise à jour Windows RS4 en tant que propriété sur l’élément MixedRealityModel.</span><span class="sxs-lookup"><span data-stu-id="9af62-143">Support for the bounding box attribute will come with the Windows RS4 update as a property on the MixedRealityModel element.</span></span> <span data-ttu-id="9af62-144">Pour définir un cadre englobant tout d’abord en haut du manifeste de l’application, ajoutez le schéma uap6 et incluez-le en tant qu’espaces de noms pouvant être ignorés:</span><span class="sxs-lookup"><span data-stu-id="9af62-144">To define a bounding box first at the top of the app manifest add the uap6 schema and include it them as ignorable namespaces:</span></span>

```xml
<Package xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2" 
         xmlns:uap5="http://schemas.microsoft.com/appx/manifest/uap/windows10/5"
         xmlns:uap6="http://schemas.microsoft.com/appx/manifest/uap/windows10/6"
         IgnorableNamespaces="uap uap2 uap5 uap6 mp"
         xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10">
```
<span data-ttu-id="9af62-145">Ensuite, sur le MixedRealityModel, définissez la propriété SpatialBoundingBox pour définir le cadre englobant:</span><span class="sxs-lookup"><span data-stu-id="9af62-145">Next, on the MixedRealityModel set the SpatialBoundingBox property to define the bounding box:</span></span> 

```xml
        <uap:DefaultTile Wide310x150Logo="Assets\WideLogo.png" >
          <uap5:MixedRealityModel Path="Assets\My3DTile.glb">
              <uap6:SpatialBoundingBox  Center=”1,-2,3” Extents=”1,2,3” />
          </uap5:MixedRealityModel>
        </uap:DefaultTile>
```

### <a name="using-unity"></a><span data-ttu-id="9af62-146">Utilisation d’Unity</span><span class="sxs-lookup"><span data-stu-id="9af62-146">Using Unity</span></span>

<span data-ttu-id="9af62-147">Lorsque vous utilisez Unity, le projet doit être généré et ouvert dans Visual Studio pour que le manifeste d’application puisse être modifié.</span><span class="sxs-lookup"><span data-stu-id="9af62-147">When working with Unity the project must be built and opened in Visual Studio before the App Manifest can be edited.</span></span> 

>[!NOTE]
><span data-ttu-id="9af62-148">Le lanceur 3D doit être redéfini dans le manifeste lors de la génération et du déploiement d’une nouvelle solution Visual Studio à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="9af62-148">The 3D launcher must be redefined in the manifest when building and deploying a new Visual Studio solution from Unity.</span></span>

## <a name="3d-deep-links-secondarytiles"></a><span data-ttu-id="9af62-149">Liens Deep 3D (secondaryTiles)</span><span class="sxs-lookup"><span data-stu-id="9af62-149">3D deep links (secondaryTiles)</span></span>

> [!NOTE]
> <span data-ttu-id="9af62-150">Cette fonctionnalité a été ajoutée dans le cadre de la mise à jour de 2017 automne Creators Update (RS3) pour les casques immersifs (VR) et dans le cadre de la mise à jour du 2018 d’avril (RS4) pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9af62-150">This feature was added as part of the 2017 Fall Creators Update (RS3) for immersive (VR) headsets and as part of the April 2018 Update (RS4) for HoloLens.</span></span> <span data-ttu-id="9af62-151">Assurez-vous que votre application cible une version du SDK Windows supérieure ou égale à 10.0.16299 sur les casques immersifs (VR) et 10.0.17125 sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9af62-151">Make sure your application is targeting a version of the Windows SDK greater than or equal to 10.0.16299 on immersive (VR) headsets and 10.0.17125 on HoloLens.</span></span> <span data-ttu-id="9af62-152">Vous trouverez les SDK Windows les plus récentes [ici](https://developer.microsoft.com/windows/downloads/windows-10-sdk).</span><span class="sxs-lookup"><span data-stu-id="9af62-152">You can find the latest Windows SDK [here](https://developer.microsoft.com/windows/downloads/windows-10-sdk).</span></span>

>[!IMPORTANT]
><span data-ttu-id="9af62-153">les liens secondaryTiles (3D Deep Links) fonctionnent uniquement avec les applications UWP 2D.</span><span class="sxs-lookup"><span data-stu-id="9af62-153">3D deep links (secondaryTiles) only work with 2D UWP apps.</span></span> <span data-ttu-id="9af62-154">Toutefois, vous pouvez créer un lanceur d' [applications en 3D](implementing-3d-app-launchers.md) pour lancer une application exclusive à partir de la page d’hébergement de Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="9af62-154">You can, however, create a [3D app launcher](implementing-3d-app-launchers.md) to launch an exclusive app from the Windows Mixed Reality home.</span></span>

<span data-ttu-id="9af62-155">Vos applications 2D peuvent être améliorées pour Windows Mixed Reality en ajoutant la possibilité de placer des modèles 3D à partir de votre application dans la [page d’accueil Windows Mixed Real](navigating-the-windows-mixed-reality-home.md) comme des liens détaillés vers le contenu de votre application 2D, comme des [vignettes secondaires 2D](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-secondary-tiles) sur le site de démarrage de Windows menus.</span><span class="sxs-lookup"><span data-stu-id="9af62-155">Your 2D applications can be enhanced for Windows Mixed Reality by adding the ability to place 3D models from your app into the [Windows Mixed Reality home](navigating-the-windows-mixed-reality-home.md) as deep links to content within your 2D app, just like [2D secondary tiles](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-secondary-tiles) on the Windows Start menu.</span></span> <span data-ttu-id="9af62-156">Par exemple, vous pouvez créer des photosphères de 360 ° qui se lient directement à une application de visionneuse de photos 360 °, ou permettre aux utilisateurs de placer du contenu 3D à partir d’une collection de ressources qui ouvre une page de détails à propos de l’auteur.</span><span class="sxs-lookup"><span data-stu-id="9af62-156">For example, you can create 360° photospheres that link directly into a 360° photo viewer app, or let users place 3D content from a collection of assets that opens a details page about the author.</span></span> <span data-ttu-id="9af62-157">Il s’agit simplement de quelques façons d’étendre les fonctionnalités de votre application 2D avec du contenu 3D.</span><span class="sxs-lookup"><span data-stu-id="9af62-157">These are just a couple ways to expand the functionality of your 2D application with 3D content.</span></span>

### <a name="creating-a-3d-secondarytile"></a><span data-ttu-id="9af62-158">Création d’un «secondaryTile» 3D</span><span class="sxs-lookup"><span data-stu-id="9af62-158">Creating a 3D “secondaryTile”</span></span>

<span data-ttu-id="9af62-159">Vous pouvez placer du contenu 3D à partir de votre application à l’aide de «secondaryTiles» en définissant un modèle de réalité mixte au moment de la création.</span><span class="sxs-lookup"><span data-stu-id="9af62-159">You can place 3D content from your application using “secondaryTiles” by defining a mixed reality model at creation time.</span></span> <span data-ttu-id="9af62-160">Les modèles de réalité mixte sont créés en référençant une ressource 3D dans votre package d’application et en définissant éventuellement un cadre englobant.</span><span class="sxs-lookup"><span data-stu-id="9af62-160">Mixed reality models are created by referencing a 3D asset in your app package and optionally defining a bounding box.</span></span> 

> [!NOTE]
> <span data-ttu-id="9af62-161">La création de «secondaryTiles» à partir d’une vue exclusive n’est pas prise en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="9af62-161">Creating “secondaryTiles” from within an exclusive view is not currently supported.</span></span>

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

### <a name="bounding-box"></a><span data-ttu-id="9af62-162">Cadre englobant</span><span class="sxs-lookup"><span data-stu-id="9af62-162">Bounding box</span></span>

<span data-ttu-id="9af62-163">Un cadre englobant peut être utilisé pour ajouter une zone de mémoire tampon supplémentaire autour de l’objet.</span><span class="sxs-lookup"><span data-stu-id="9af62-163">A bounding box can be used to add an additional buffer region around the object.</span></span> <span data-ttu-id="9af62-164">Le cadre englobant est spécifié à l’aide d’un point central et d’étendues qui indiquent la distance entre le centre du rectangle englobant et ses bords le long de chaque axe.</span><span class="sxs-lookup"><span data-stu-id="9af62-164">The bounding box is specified using a center point and extents which indicate the distance from the center of the bounding box to its edges along each axis.</span></span> <span data-ttu-id="9af62-165">Les unités du cadre englobant peuvent être mappées à 1 unité = 1 mètre.</span><span class="sxs-lookup"><span data-stu-id="9af62-165">Units for the bounding box can be mapped to 1 unit = 1 meter.</span></span> <span data-ttu-id="9af62-166">Si aucun cadre englobant n’est fourni, l’un d’eux est automatiquement ajusté à la maille de l’objet.</span><span class="sxs-lookup"><span data-stu-id="9af62-166">If a bounding box is not provided then one will be automatically fitted to the mesh of the object.</span></span> <span data-ttu-id="9af62-167">Si le cadre englobant fourni est plus petit que le modèle, il sera redimensionné pour s’ajuster à la maille.</span><span class="sxs-lookup"><span data-stu-id="9af62-167">If the provided bounding box is smaller than the model then it will be resized to fit the mesh.</span></span>

### <a name="activation-behavior"></a><span data-ttu-id="9af62-168">Comportement d’activation</span><span class="sxs-lookup"><span data-stu-id="9af62-168">Activation behavior</span></span>

> [!NOTE]
> <span data-ttu-id="9af62-169">Ce composant sera pris en charge à partir de la mise à jour de Windows RS4.</span><span class="sxs-lookup"><span data-stu-id="9af62-169">This feature will be supported as of the Windows RS4 update.</span></span> <span data-ttu-id="9af62-170">Assurez-vous que votre application cible une version du SDK Windows supérieure ou égale à 10.0.17125 si vous envisagez d’utiliser cette fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="9af62-170">Make sure your application is targeting a version of the Windows SDK greater than or equal to 10.0.17125 if you plan to use this feature</span></span>

<span data-ttu-id="9af62-171">Vous pouvez définir le comportement d’activation d’un secondaryTile 3D afin de contrôler la manière dont il réagit lorsqu’un utilisateur le sélectionne.</span><span class="sxs-lookup"><span data-stu-id="9af62-171">You can define the activation behavior for a 3D secondaryTile to control how it reacts when a user selects it.</span></span> <span data-ttu-id="9af62-172">Cela peut être utilisé pour placer des objets 3D dans la zone de vie de la réalité mixte qui sont informatifs ou décoratifs Purley.</span><span class="sxs-lookup"><span data-stu-id="9af62-172">This can be used to place 3D objects in the Mixed Reality home that are purley informative or decorative.</span></span> <span data-ttu-id="9af62-173">Les types de comportement d’activation suivants sont pris en charge:</span><span class="sxs-lookup"><span data-stu-id="9af62-173">The following activation behavior types are supported:</span></span>
1. <span data-ttu-id="9af62-174">Par défaut : Quand un utilisateur sélectionne l’secondaryTile 3D, l’application est activée</span><span class="sxs-lookup"><span data-stu-id="9af62-174">Default: When a user selects the 3D secondaryTile the app is activated</span></span>
2. <span data-ttu-id="9af62-175">None : Lorsque les utilisateurs sélectionnent l’secondaryTile 3D, rien ne se produit et l’application n’est pas activée.</span><span class="sxs-lookup"><span data-stu-id="9af62-175">None: When the users selects the 3D secondaryTile nothing happens and the app is not activated.</span></span>

### <a name="obtaining-and-updating-an-existing-secondarytile"></a><span data-ttu-id="9af62-176">Obtention et mise à jour d’un «secondaryTile» existant</span><span class="sxs-lookup"><span data-stu-id="9af62-176">Obtaining and updating an existing “secondaryTile”</span></span>

<span data-ttu-id="9af62-177">Les développeurs peuvent obtenir une liste de leurs vignettes secondaires existantes, y compris les propriétés qu’ils ont spécifiées précédemment.</span><span class="sxs-lookup"><span data-stu-id="9af62-177">Developers can get back a list of their existing secondary tiles, which includes the properties that they previously specified.</span></span> <span data-ttu-id="9af62-178">Ils peuvent également mettre à jour les propriétés en modifiant la valeur, puis en appelant UpdateAsync ().</span><span class="sxs-lookup"><span data-stu-id="9af62-178">They can also update the properties by changing the value and then calling UpdateAsync().</span></span>

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

### <a name="checking-that-the-user-is-in-windows-mixed-reality"></a><span data-ttu-id="9af62-179">Vérification de la présence de l’utilisateur dans Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="9af62-179">Checking that the user is in Windows Mixed Reality</span></span>

<span data-ttu-id="9af62-180">les liens en profondeur 3D (secondaryTiles) peuvent être créés uniquement lorsque la vue est affichée dans un casque Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="9af62-180">3D deep links (secondaryTiles) can only be created while the view is being displayed in a Windows Mixed Reality headset.</span></span> <span data-ttu-id="9af62-181">Lorsque votre affichage n’est pas présenté dans un casque Windows Mixed Reality, nous vous recommandons de le gérer en masquant le point d’entrée ou en indiquant un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="9af62-181">When your view isn't being presented in a Windows Mixed Reality headset we recommend gracefully handling this by either hiding the entry point or showing an error message.</span></span> <span data-ttu-id="9af62-182">Vous pouvez vérifier cela en interrogeant [IsCurrentViewPresentedOnHolographic ()](https://docs.microsoft.com/uwp/api/windows.applicationmodel.preview.holographic.holographicapplicationpreview#Windows_ApplicationModel_Preview_Holographic_HolographicApplicationPreview_IsCurrentViewPresentedOnHolographicDisplay_).</span><span class="sxs-lookup"><span data-stu-id="9af62-182">You can check this by querying [IsCurrentViewPresentedOnHolographic()](https://docs.microsoft.com/uwp/api/windows.applicationmodel.preview.holographic.holographicapplicationpreview#Windows_ApplicationModel_Preview_Holographic_HolographicApplicationPreview_IsCurrentViewPresentedOnHolographicDisplay_).</span></span>

## <a name="tile-notifications"></a><span data-ttu-id="9af62-183">Notifications par vignette</span><span class="sxs-lookup"><span data-stu-id="9af62-183">Tile notifications</span></span>

<span data-ttu-id="9af62-184">Les notifications par vignette ne prennent pas actuellement en charge l’envoi d’une mise à jour avec une ressource 3D.</span><span class="sxs-lookup"><span data-stu-id="9af62-184">Tile notifications do not currently support sending an update with a 3D asset.</span></span> <span data-ttu-id="9af62-185">Cela signifie que les développeurs ne seront pas en mesure d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="9af62-185">This means that developers will not be able to do the following</span></span>
* <span data-ttu-id="9af62-186">Notifications Push</span><span class="sxs-lookup"><span data-stu-id="9af62-186">Push Notifications</span></span>
* <span data-ttu-id="9af62-187">Interrogation périodique</span><span class="sxs-lookup"><span data-stu-id="9af62-187">Periodic Polling</span></span>
* <span data-ttu-id="9af62-188">Notifications planifiées</span><span class="sxs-lookup"><span data-stu-id="9af62-188">Scheduled Notifications</span></span>

<span data-ttu-id="9af62-189">Pour plus d’informations sur les autres fonctionnalités et attributs de vignettes et sur la façon dont ils sont utilisés pour les mosaïques 2D, consultez la [documentation vignettes pour les applications UWP](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-creating-tiles).</span><span class="sxs-lookup"><span data-stu-id="9af62-189">For more information on the other tiles features and attributes and how they are used for 2D tiles refer to the [Tiles for UWP Apps documentation](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-creating-tiles).</span></span>

## <a name="see-also"></a><span data-ttu-id="9af62-190">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9af62-190">See also</span></span>

* <span data-ttu-id="9af62-191">[Exemple de modèle de réalité mixte](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) contenant un lanceur d’application 3D.</span><span class="sxs-lookup"><span data-stu-id="9af62-191">[Mixed reality model sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) containing a 3D app launcher.</span></span>
* [<span data-ttu-id="9af62-192">Guide de conception du lanceur d’applications 3D</span><span class="sxs-lookup"><span data-stu-id="9af62-192">3D app launcher design guidance</span></span>](3d-app-launcher-design-guidance.md)
* [<span data-ttu-id="9af62-193">Création de modèles 3D à utiliser dans la page d’hébergement Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="9af62-193">Creating 3D models for use in the Windows Mixed Reality home</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [<span data-ttu-id="9af62-194">Implémentation de lanceurs d’applications en 3D (applications Win32)</span><span class="sxs-lookup"><span data-stu-id="9af62-194">Implementing 3D app launchers (Win32 apps)</span></span>](implementing-3d-app-launchers-win32.md)
* [<span data-ttu-id="9af62-195">Exploration de la page d’accueil Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="9af62-195">Navigating the Windows Mixed Reality home</span></span>](navigating-the-windows-mixed-reality-home.md)
