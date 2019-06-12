---
title: Permettre le placement des modèles 3D dans la page d’accueil
description: Comment placer des modèles 3D à partir de votre site Web ou une application dans Windows Mixed Reality domestique
author: thmignon
ms.author: thmignon
ms.date: 05/04/2018
ms.topic: article
keywords: 3D, modèle, sur place à domicile, sur place, monde, modélisation, réalité mixte domestique, web, application
ms.openlocfilehash: 954086b79e3614e1b75ceb7560f9fc87435530fa
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829735"
---
# <a name="enable-placement-of-3d-models-in-the-mixed-reality-home"></a><span data-ttu-id="762b9-104">Permettre le placement des modèles 3D dans la réalité mixte domestique</span><span class="sxs-lookup"><span data-stu-id="762b9-104">Enable placement of 3D models in the mixed reality home</span></span>

> [!NOTE]
> <span data-ttu-id="762b9-105">Cette fonctionnalité a été ajoutée dans le cadre de la [mettre à jour du 10 avril 2018 Windows](release-notes-april-2018.md).</span><span class="sxs-lookup"><span data-stu-id="762b9-105">This feature was added as part of the [Windows 10 April 2018 Update](release-notes-april-2018.md).</span></span> <span data-ttu-id="762b9-106">Les versions antérieures de Windows ne sont pas compatibles avec cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="762b9-106">Older versions of Windows are not compatible with this feature.</span></span>

<span data-ttu-id="762b9-107">Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs arrivent avant de lancer des applications.</span><span class="sxs-lookup"><span data-stu-id="762b9-107">The [Windows Mixed Reality home](navigating-the-windows-mixed-reality-home.md) is the starting point where users land before launching applications.</span></span> <span data-ttu-id="762b9-108">Dans certains scénarios, les applications 2D (par exemple, l’application hologrammes) permettent le placement des modèles 3D directement dans la page d’accueil réalité mixte comme des ornements, ou pour une nouvelle inspection entièrement en 3D.</span><span class="sxs-lookup"><span data-stu-id="762b9-108">In some scenarios, 2D apps (like the Holograms app) enable placement of 3D models directly into the mixed reality home as decorations or for further inspection in full 3D.</span></span> <span data-ttu-id="762b9-109">Le *ajouter modèle protocole* vous permet d’envoyer un modèle 3D à partir de votre site Web ou une application directement dans la réalité mixte Windows domestique, où il est conservé comme [lanceurs d’applications 3D](3d-app-launcher-design-guidance.md), applications 2D et hologrammes.</span><span class="sxs-lookup"><span data-stu-id="762b9-109">The *add model protocol* allows you to send a 3D model from your website or application directly into the Windows Mixed Reality home, where it will persist like [3D app launchers](3d-app-launcher-design-guidance.md), 2D apps, and holograms.</span></span> 

<span data-ttu-id="762b9-110">Par exemple, si vous développez une application qui fait apparaître un catalogue de mobilier 3D pour la conception d’un espace, vous pouvez utiliser la *ajouter modèle protocole* pour permettre aux utilisateurs de placer ces modèles de mobilier 3D à partir du catalogue.</span><span class="sxs-lookup"><span data-stu-id="762b9-110">For example, if you're developing an application that surfaces a catalog of 3D furniture for designing a space, you can use the *add model protocol* to allow users to place those 3D furniture models from the catalog.</span></span> <span data-ttu-id="762b9-111">Une fois placés dans le monde, les utilisateurs peuvent déplacer, redimensionner et supprimer ces modèles 3D à l’instar des autres hologrammes dans la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="762b9-111">Once placed in the world, users can move, resize, and remove these 3D models just like other holograms in the home.</span></span> <span data-ttu-id="762b9-112">Cet article fournit une vue d’ensemble de l’implémentation de la *ajouter modèle protocole* afin que vous pouvez démarrer permettant aux utilisateurs de décorer la vie avec des objets 3D à partir de votre application ou le web.</span><span class="sxs-lookup"><span data-stu-id="762b9-112">This article provides an overview of implementing the *add model protocol* so that you can start enabling users to decorate their world with 3D objects from your app or the web.</span></span>

## <a name="device-support"></a><span data-ttu-id="762b9-113">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="762b9-113">Device support</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="762b9-114"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="762b9-114"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="762b9-115"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="762b9-115"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="762b9-116"><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></span><span class="sxs-lookup"><span data-stu-id="762b9-116"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="762b9-117">Ajouter le protocole de modèle</span><span class="sxs-lookup"><span data-stu-id="762b9-117">Add model protocol</span></span></td>
        <td><span data-ttu-id="762b9-118">✔️</span><span class="sxs-lookup"><span data-stu-id="762b9-118">✔️</span></span></td>
        <td><span data-ttu-id="762b9-119">✔️</span><span class="sxs-lookup"><span data-stu-id="762b9-119">✔️</span></span></td>
    </tr>
</table>

## <a name="overview"></a><span data-ttu-id="762b9-120">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="762b9-120">Overview</span></span>

<span data-ttu-id="762b9-121">Il existe 2 étapes de permettre à l’emplacement des modèles 3D dans Windows Mixed Reality domestique :</span><span class="sxs-lookup"><span data-stu-id="762b9-121">There are 2 steps to enabling the placement of 3D models in the Windows Mixed Reality home:</span></span>
1. <span data-ttu-id="762b9-122">[Vérifiez que votre modèle 3D est compatible avec Windows Mixed Reality accueil](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md).</span><span class="sxs-lookup"><span data-stu-id="762b9-122">[Ensure your 3D model is compatible with the Windows Mixed Reality home](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md).</span></span>
2. <span data-ttu-id="762b9-123">Implémentez le *ajouter le protocole de modèle* dans votre application ou d’une page Web (cet article).</span><span class="sxs-lookup"><span data-stu-id="762b9-123">Implement the *add model protocol* in your application or webpage (this article).</span></span>

## <a name="implementing-the-add-model-protocol"></a><span data-ttu-id="762b9-124">Mise en œuvre le *ajouter le protocole de modèle*</span><span class="sxs-lookup"><span data-stu-id="762b9-124">Implementing the *add model protocol*</span></span>

<span data-ttu-id="762b9-125">Une fois que vous avez un [modèle 3D compatible](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md), vous pouvez implémenter la *ajouter modèle protocole* en activant l’URI suivant d’une page Web ou d’application :</span><span class="sxs-lookup"><span data-stu-id="762b9-125">Once you have a [compatible 3D model](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md), you can implement the *add model protocol* by activating the following URI from any webpage or application:</span></span>

```
ms-mixedreality:addmodel?uri=<Path to a .glb 3D model either local or remote>
```

<span data-ttu-id="762b9-126">Si l’URI pointe vers une ressource distante, puis il est automatiquement téléchargé et placé dans la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="762b9-126">If the URI points to a remote resource, then it will automatically be downloaded and placed in the home.</span></span> <span data-ttu-id="762b9-127">Ressources locales seront copiés au dossier de données de la page d’accueil réalité mixte application avant d’être placé dans la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="762b9-127">Local resources will be copied to the mixed reality home's app data folder before being placed in the home.</span></span> <span data-ttu-id="762b9-128">Nous vous recommandons de conception de votre expérience compte pour les scénarios où l’utilisateur peut exécuter une version antérieure de Windows qui ne prennent pas en charge cette fonctionnalité en masquant le bouton ou de la désactivation de la mesure du possible.</span><span class="sxs-lookup"><span data-stu-id="762b9-128">We recommend designing your experience to account for scenarios where the user might be running an older version of Windows that doesn't support this feature by hiding the button or disabling it if possible.</span></span> 

### <a name="invoking-the-add-model-protocol-from-a-universal-windows-platform-app"></a><span data-ttu-id="762b9-129">Appel de la *ajouter modèle protocole* à partir d’une application de plateforme Windows universelle :</span><span class="sxs-lookup"><span data-stu-id="762b9-129">Invoking the *add model protocol* from a Universal Windows Platform app:</span></span>

```C#
private async void launchURI_Click(object sender, RoutedEventArgs e)
{
   // Define the add model URI
   var uriAddModel = new Uri(@"ms-mixedreality:addModel?uri=sample.glb");

   // Launch the URI to invoke the placement
   var success = await Windows.System.Launcher.LaunchUriAsync(uriAddModel);

   if (success)
   {
      // URI launched
   }
   else
   {
      // URI launch failed
   }
}
```

### <a name="invoking-the-add-model-protocol-from-a-webpage"></a><span data-ttu-id="762b9-130">Appel de la *ajouter modèle protocole* à partir d’une page Web :</span><span class="sxs-lookup"><span data-stu-id="762b9-130">Invoking the *add model protocol* from a webpage:</span></span>

```html
<a class="btn btn-default" href="ms-mixedreality:addModel?uri=sample.glb"> Place 3D Model </a>
```

## <a name="considerations-for-immersive-vr-headsets"></a><span data-ttu-id="762b9-131">Considérations pour des casques IMMERSIFS (VR)</span><span class="sxs-lookup"><span data-stu-id="762b9-131">Considerations for immersive (VR) headsets</span></span>

* <span data-ttu-id="762b9-132">Pour des casques IMMERSIFS (VR), le portail de réalité mixte ne devra pas être en cours d’exécution avant d’appeler le *ajouter le protocole de modèle*.</span><span class="sxs-lookup"><span data-stu-id="762b9-132">For immersive (VR) headsets, the Mixed Reality Portal does not have to be running before invoking the *add model protocol*.</span></span> <span data-ttu-id="762b9-133">Dans ce cas, le *ajouter modèle protocole* lance le portail de réalité mixte et placer l’objet directement où le casque recherche une fois que vous arrivez dans la réalité mixte domestique.</span><span class="sxs-lookup"><span data-stu-id="762b9-133">In this case, the *add model protocol* will launch the Mixed Reality Portal and place the object directly where the headset is looking once you arrive in the mixed reality home.</span></span> 
* <span data-ttu-id="762b9-134">Lors de l’appel le *ajouter modèle protocole* à partir du bureau avec le portail de réalité mixte déjà en cours d’exécution, vérifiez que le casque est « éveillé ».</span><span class="sxs-lookup"><span data-stu-id="762b9-134">When invoking the *add model protocol* from the desktop with the Mixed Reality Portal already running, ensure that the headset is "awake".</span></span> <span data-ttu-id="762b9-135">Si ce n’est pas le cas, le placement ne réussira pas.</span><span class="sxs-lookup"><span data-stu-id="762b9-135">If not, the placement will not succeed.</span></span> 

## <a name="see-also"></a><span data-ttu-id="762b9-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="762b9-136">See also</span></span>

* [<span data-ttu-id="762b9-137">Création de modèles 3D pour une utilisation dans la page d’accueil Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="762b9-137">Creating 3D models for use in the Windows Mixed Reality home</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [<span data-ttu-id="762b9-138">Exploration de la page d’accueil Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="762b9-138">Navigating the Windows Mixed Reality home</span></span>](navigating-the-windows-mixed-reality-home.md)
