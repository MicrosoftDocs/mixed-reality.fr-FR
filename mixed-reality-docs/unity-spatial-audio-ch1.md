---
title: Didacticiels audio spatial-1. Ajout de données audio spatiales à votre projet
description: Ajoutez le plug-in Microsoft Spatializer à votre projet Unity pour accéder au déchargement matériel HoloLens 2 HRTF.
author: kegodin
ms.author: kegodin
ms.date: 12/01/2019
ms.topic: article
keywords: réalité mixte, Unity, tutorial, hololens2, audio spatial
ms.openlocfilehash: 8978017b3ce6c49a81b3eee2fe21e9234f4e71f0
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75182796"
---
# <a name="adding-spatial-audio-to-your-unity-project"></a><span data-ttu-id="10dad-105">Ajout de données audio spatiales à votre projet Unity</span><span class="sxs-lookup"><span data-stu-id="10dad-105">Adding spatial audio to your Unity project</span></span>

<span data-ttu-id="10dad-106">Bienvenue dans le tutioral de l’audio spatial pour Unity sur HoloLens2.</span><span class="sxs-lookup"><span data-stu-id="10dad-106">Welcome to the spatial audio tutioral for Unity on HoloLens2.</span></span> <span data-ttu-id="10dad-107">Cette séquence de didacticiel présente les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="10dad-107">This tutorial sequence shows:</span></span>
* <span data-ttu-id="10dad-108">Utilisation du déchargement de HRTF sur HoloLens 2 dans Unity</span><span class="sxs-lookup"><span data-stu-id="10dad-108">How to use HRTF offload on HoloLens 2 in Unity</span></span>
* <span data-ttu-id="10dad-109">Comment activer le réverbe lors de l’utilisation du déchargement HRTF</span><span class="sxs-lookup"><span data-stu-id="10dad-109">How to enable reverb when using HRTF offload</span></span>

<span data-ttu-id="10dad-110">Le [dépôt github Microsoft Spatializer](https://github.com/microsoft/spatialaudio-unity) a un projet Unity terminé de cette séquence de didacticiels.</span><span class="sxs-lookup"><span data-stu-id="10dad-110">The [Microsoft Spatializer GitHub repository](https://github.com/microsoft/spatialaudio-unity) has a completed Unity project of this tutorial sequence.</span></span> 

<span data-ttu-id="10dad-111">Pour obtenir des recommandations sur le moment où il peut être utile d’les sons, consultez [conception de son spatial](https://docs.microsoft.com/windows/mixed-reality/spatial-sound-design).</span><span class="sxs-lookup"><span data-stu-id="10dad-111">For our recommendations on when it can be helpful to spatialize sounds, see [spatial sound design](https://docs.microsoft.com/windows/mixed-reality/spatial-sound-design).</span></span>

## <a name="objectives"></a><span data-ttu-id="10dad-112">Objectifs</span><span class="sxs-lookup"><span data-stu-id="10dad-112">Objectives</span></span>
<span data-ttu-id="10dad-113">Dans ce premier chapitre, vous allez :</span><span class="sxs-lookup"><span data-stu-id="10dad-113">In this first chapter, you'll:</span></span>
* <span data-ttu-id="10dad-114">Créer un projet Unity et importer MRTK</span><span class="sxs-lookup"><span data-stu-id="10dad-114">Create a Unity project and import MRTK</span></span>
* <span data-ttu-id="10dad-115">Importer le plug-in Microsoft Spatializer</span><span class="sxs-lookup"><span data-stu-id="10dad-115">Import the Microsoft spatializer plugin</span></span>
* <span data-ttu-id="10dad-116">Activer le plug-in Microsoft Spatializer</span><span class="sxs-lookup"><span data-stu-id="10dad-116">Enable the Microsoft spatializer plugin</span></span>
* <span data-ttu-id="10dad-117">Activer l’audio spatial sur votre station de travail de développeur</span><span class="sxs-lookup"><span data-stu-id="10dad-117">Enable spatial audio on your developer workstation</span></span>

## <a name="create-a-project-and-add-nuget-for-unity"></a><span data-ttu-id="10dad-118">Créer un projet et ajouter NuGet pour Unity</span><span class="sxs-lookup"><span data-stu-id="10dad-118">Create a project and add NuGet for Unity</span></span>
<span data-ttu-id="10dad-119">Commencez avec un projet Unity vide, puis ajoutez et configurez NuGet pour Unity :</span><span class="sxs-lookup"><span data-stu-id="10dad-119">Start with an empty Unity project, then add and configure NuGet for Unity:</span></span>
1. <span data-ttu-id="10dad-120">Téléchargez la dernière version de [NuGetForUnity. pour Unity](https://github.com/GlitchEnzo/NuGetForUnity/releases/latest)</span><span class="sxs-lookup"><span data-stu-id="10dad-120">Download the latest [NuGetForUnity .unitypackage](https://github.com/GlitchEnzo/NuGetForUnity/releases/latest)</span></span>
2. <span data-ttu-id="10dad-121">Dans la barre de menus Unity, cliquez sur **ressources-> importer un package-> package personnalisé...** et installer le package NuGetForUnity :</span><span class="sxs-lookup"><span data-stu-id="10dad-121">In the Unity menu bar, click **Assets -> Import Package -> Custom Package...** and install the NuGetForUnity package:</span></span>

![Importer un package personnalisé](images/spatial-audio/import-custom-package.png)

## <a name="add-the-windows-mixed-reality-package"></a><span data-ttu-id="10dad-123">Ajouter le package Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="10dad-123">Add the Windows Mixed Reality package</span></span>
<span data-ttu-id="10dad-124">La prise en charge de Windows Mixed Reality dans Unity 2019 et versions ultérieures est contenue dans un package facultatif.</span><span class="sxs-lookup"><span data-stu-id="10dad-124">Windows Mixed Reality support in Unity 2019 and later is contained in an optional package.</span></span> <span data-ttu-id="10dad-125">Pour l’ajouter à votre projet, ouvrez la **fenêtre > gestionnaire de package** à partir de la barre de menus Unity :</span><span class="sxs-lookup"><span data-stu-id="10dad-125">To add it to your project, open **Window -> Package Manager** from the Unity menu bar:</span></span>

![Menu du gestionnaire de package](images/spatial-audio/package-manager-menu.png)

<span data-ttu-id="10dad-127">Recherchez et installez le package **Windows Mixed Reality** :</span><span class="sxs-lookup"><span data-stu-id="10dad-127">Then find and install the **Windows Mixed Reality** package:</span></span>

![Fenêtre du gestionnaire de package](images/spatial-audio/package-manager-window.png)

## <a name="install-mrtk-and-microsoft-spatializer"></a><span data-ttu-id="10dad-129">Installer MRTK et Microsoft Spatializer</span><span class="sxs-lookup"><span data-stu-id="10dad-129">Install MRTK and Microsoft Spatializer</span></span>
<span data-ttu-id="10dad-130">À l’aide de NuGet pour Unity, installez les plug-ins MRTK et Microsoft Spatializer :</span><span class="sxs-lookup"><span data-stu-id="10dad-130">Using NuGet for Unity, install the MRTK and Microsoft Spatializer plugins:</span></span>
1. <span data-ttu-id="10dad-131">Dans la barre de menus de Unity, cliquez sur **NuGet-> gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="10dad-131">In the Unity menu bar, click on **NuGet -> Manage NuGet Packages**.</span></span>

![Gérer des packages NuGet](images/spatial-audio/manage-nuget-packages.png)

2. <span data-ttu-id="10dad-133">Dans la zone de **recherche** , entrez « Microsoft. MixedReality. Toolkit » et installez le package MRTK Core : **Microsoft. MixedReality. Toolkit. Foundation**</span><span class="sxs-lookup"><span data-stu-id="10dad-133">In the **Search** box, enter "Microsoft.MixedReality.Toolkit" and install the MRTK core package: **Microsoft.MixedReality.Toolkit.Foundation**</span></span>

![Package NuGet MRTK](images/spatial-audio/mrtk-nuget-package.png)

<span data-ttu-id="10dad-135">Le [package NuGet MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MRTKNuGetPackage.html) contient un contexte et des détails supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="10dad-135">[MRTK NuGet Package](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MRTKNuGetPackage.html) has additional context and details.</span></span>

4. <span data-ttu-id="10dad-136">Dans la zone de **recherche** , entrez « Microsoft. SpatialAudio » et installez le package Microsoft Spatializer : **Microsoft. SpatialAudio. Spatializer. Unity**</span><span class="sxs-lookup"><span data-stu-id="10dad-136">In the **Search** box, enter "Microsoft.SpatialAudio" and install the Microsoft Spatializer package: **Microsoft.SpatialAudio.Spatializer.Unity**</span></span>

![Plug-in Spatializer NuGet](images/spatial-audio/spatializer-plugin-nuget.png)

## <a name="set-up-mrtk-in-your-project"></a><span data-ttu-id="10dad-138">Configurer MRTK dans votre projet</span><span class="sxs-lookup"><span data-stu-id="10dad-138">Set up MRTK in your project</span></span>

1. <span data-ttu-id="10dad-139">Ouvrez la fenêtre Paramètres de build en accédant à **fichiers-> paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="10dad-139">Open the Build Settings window by going to **File -> Build Settings**.</span></span>

2. <span data-ttu-id="10dad-140">Sélectionnez le _plateforme Windows universelle_ , puis cliquez sur **basculer la plateforme**.</span><span class="sxs-lookup"><span data-stu-id="10dad-140">Select the _Universal Windows Platform_ and click **Switch Platform**.</span></span>

3. <span data-ttu-id="10dad-141">Cliquez sur **paramètres du lecteur** dans la **fenêtre générer** pour ouvrir les propriétés des **paramètres du lecteur** dans le volet **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="10dad-141">Click **Player Settings** in the **Build Window** to open the **Player Settings** properties in the **Inspector** pane.</span></span>
    * <span data-ttu-id="10dad-142">Sous **paramètres de XR**, activez la case à cocher **réalité virtuelle prise en charge**</span><span class="sxs-lookup"><span data-stu-id="10dad-142">Under **XR Settings**, check the **Virtual Reality Supported** checkbox</span></span>
    * <span data-ttu-id="10dad-143">Sous **paramètres XR**, définissez le **mode de rendu stéréo** sur **Single-instanced**.</span><span class="sxs-lookup"><span data-stu-id="10dad-143">Under **XR Settings**, change the **Stereo Rendering Mode** to **Single Pass Instanced**.</span></span>
    * <span data-ttu-id="10dad-144">Sous **paramètres de publication**, activez la case à cocher **perception spatiale** dans la section **fonctionnalités** .</span><span class="sxs-lookup"><span data-stu-id="10dad-144">Under **Publishing Settings**, check the **Spatial Perception** checkbox in the **Capabilities** section</span></span>

4. <span data-ttu-id="10dad-145">Dans la barre de menus, cliquez sur **Kit de pratiques de réalité mixte-> ajouter à la scène et configurer.**</span><span class="sxs-lookup"><span data-stu-id="10dad-145">On the menu bar, click **Mixed Reality Toolkit -> Add to Scene and Configure..**</span></span> <span data-ttu-id="10dad-146">pour ajouter MRTK à votre scène.</span><span class="sxs-lookup"><span data-stu-id="10dad-146">to add MRTK to your scene.</span></span>

<span data-ttu-id="10dad-147">Pour obtenir des conseils supplémentaires, notamment la façon de créer votre application et de la déployer sur un HoloLens 2, consultez [le chapitre 1 du module de base de l’apprentissage de RM](mrlearning-base-ch1.md).</span><span class="sxs-lookup"><span data-stu-id="10dad-147">For additional guidance, including how to build your app and deploy to a HoloLens 2, see [Chapter 1 of the MR Learning Base Module](mrlearning-base-ch1.md).</span></span>

## <a name="enable-the-microsoft-spatializer-plugin"></a><span data-ttu-id="10dad-148">Activer le plug-in Microsoft Spatializer</span><span class="sxs-lookup"><span data-stu-id="10dad-148">Enable the Microsoft Spatializer plugin</span></span>
<span data-ttu-id="10dad-149">Activez le plug-in **Microsoft Spatializer** .</span><span class="sxs-lookup"><span data-stu-id="10dad-149">Enable the **Microsoft Spatializer** plugin.</span></span> <span data-ttu-id="10dad-150">Ouvrez les **paramètres de projet Edit->-> audio**, puis remplacez le **plug-in Spatializer** par "Microsoft Spatializer".</span><span class="sxs-lookup"><span data-stu-id="10dad-150">Open **Edit -> Project Settings -> Audio**, and change **Spatializer Plugin** to "Microsoft Spatializer".</span></span> <span data-ttu-id="10dad-151">La section **audio** des **paramètres du projet** doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="10dad-151">The **Audio** section of the **Project Settings** will now look like this:</span></span>

![Paramètres du projet présentant le plug-in Spatializer](images/spatial-audio/project-settings.png)

## <a name="enable-spatial-audio-on-your-workstation"></a><span data-ttu-id="10dad-153">Activer l’audio spatial sur votre station de travail</span><span class="sxs-lookup"><span data-stu-id="10dad-153">Enable spatial audio on your workstation</span></span>
<span data-ttu-id="10dad-154">Sur les versions de bureau de Windows, l’audio spatial est désactivé par défaut.</span><span class="sxs-lookup"><span data-stu-id="10dad-154">On desktop versions of Windows, spatial audio is disabled by default.</span></span> <span data-ttu-id="10dad-155">Pour l’activer, cliquez avec le bouton droit sur l’icône de volume dans la barre des tâches.</span><span class="sxs-lookup"><span data-stu-id="10dad-155">Enable it by right-clicking on the volume icon in the task bar.</span></span> <span data-ttu-id="10dad-156">Pour obtenir la meilleure représentation de ce que vous entendez sur HoloLens 2, choisissez **son Spatial > Windows Sonic pour casque**.</span><span class="sxs-lookup"><span data-stu-id="10dad-156">To get the best representation of what you'll hear on HoloLens 2, choose **Spatial sound -> Windows Sonic for Headphones**.</span></span>

![Paramètres audio spatiaux du Bureau](images/spatial-audio/desktop-audio-settings.png)

> [!NOTE]
> <span data-ttu-id="10dad-158">Ce paramètre est requis uniquement si vous envisagez de tester votre projet dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="10dad-158">This setting is only required if you plan to test your project in the Unity editor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10dad-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10dad-159">Next steps</span></span>
<span data-ttu-id="10dad-160">Passez à [Unity audio spatial chapitre 2](unity-spatial-audio-ch2.md) pour effectuer l’spatiale des sons d’interaction du bouton.</span><span class="sxs-lookup"><span data-stu-id="10dad-160">Continue on to [Unity spatial audio chapter 2](unity-spatial-audio-ch2.md) to spatialize button interaction sounds.</span></span>

