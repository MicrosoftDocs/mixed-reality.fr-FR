---
title: Son spatial dans Unreal
description: Vue d’ensemble du plug-in d’audio spatial pour le moteur Unreal.
author: hferrone
ms.author: v-haferr
ms.date: 06/15/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, streaming, communication à distance, réalité mixte, développement, démarrage, fonctionnalités, nouveau projet, émulateur, documentation, guides, fonctionnalités, hologrammes, développement de jeux
ms.openlocfilehash: 404aaec7b618e951ad69c02e7aaef80e42d31dbd
ms.sourcegitcommit: 5612e8bfb9c548eac42182702cec87b160efbbfe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85446796"
---
# <a name="spatial-audio-in-unreal"></a><span data-ttu-id="ee508-104">Son spatial dans Unreal</span><span class="sxs-lookup"><span data-stu-id="ee508-104">Spatial Audio in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="ee508-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="ee508-105">Overview</span></span>

<span data-ttu-id="ee508-106">Contrairement à la vue, les êtres humains entendent en son surround à 360 degrés.</span><span class="sxs-lookup"><span data-stu-id="ee508-106">Unlike vision, humans hear in 360 degree surround sound.</span></span> <span data-ttu-id="ee508-107">Le son spatial émule le fonctionnement de l’audition humaine, en fournissant les signaux nécessaires pour identifier les emplacements sonores dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="ee508-107">Spatial sound emulates how human hearing works, providing the cues needed to identify sound locations in world-space.</span></span> <span data-ttu-id="ee508-108">Quand vous ajoutez un son spatial dans vos applications de réalité mixte, vous améliorez le niveau d’immersion de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ee508-108">When you add spatial sound in your mixed reality applications, you're enhancing the level of immersion your users experience.</span></span>  

<span data-ttu-id="ee508-109">Le traitement du son spatial de haute qualité est complexe ; HoloLens 2 est donc fourni avec un matériel dédié pour le traitement de ces objets audio.</span><span class="sxs-lookup"><span data-stu-id="ee508-109">High quality spatial sound processing is complex, so the HoloLens 2 comes with dedicated hardware for processing those sound objects.</span></span>  <span data-ttu-id="ee508-110">Pour pouvoir accéder à cette prise en charge du traitement matériel, vous devez installer le plug-in **MicrosoftSpatialSound** dans votre projet Unreal.</span><span class="sxs-lookup"><span data-stu-id="ee508-110">Before you can access this hardware processing support, you'll need to install the **MicrosoftSpatialSound** plugin in your Unreal project.</span></span> <span data-ttu-id="ee508-111">Cet article vous guide tout au long de l’installation et de la configuration de ce plug-in, et vous dirige vers des ressources plus approfondies sur l’utilisation du son spatial dans le moteur Unreal.</span><span class="sxs-lookup"><span data-stu-id="ee508-111">This article will walk you through the installation and configuration of that plugin and point you towards more in-depth resources for using spatial sound in the Unreal engine.</span></span> 

## <a name="installing-the-microsoft-spatial-sound-plugin"></a><span data-ttu-id="ee508-112">Installation du plug-in Microsoft Spatial Sound</span><span class="sxs-lookup"><span data-stu-id="ee508-112">Installing the Microsoft Spatial Sound plugin</span></span> 

<span data-ttu-id="ee508-113">La première étape pour ajouter un son spatial à votre projet consiste à installer le plug-in de son spatial Microsoft, que vous trouverez en :</span><span class="sxs-lookup"><span data-stu-id="ee508-113">The first step to adding spatial sound to your project is installing the Microsoft Spatial Sound plugin, which you can find by:</span></span> 

1. <span data-ttu-id="ee508-114">Cliquant sur **Modifier > Plug-ins** et en recherchant **MicrosoftSpatialSound** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="ee508-114">Clicking **Edit > Plugins** and searching for **MicrosoftSpatialSound** in the search box.</span></span> 
2. <span data-ttu-id="ee508-115">Cochant la case **Activé** dans le plug-in **MicrosoftSpatialSound**.</span><span class="sxs-lookup"><span data-stu-id="ee508-115">Selecting the **Enabled** checkbox in the **MicrosoftSpatialSound** plugin.</span></span> 
3. <span data-ttu-id="ee508-116">Redémarrant l’éditeur Unreal en sélectionnant **Redémarrer maintenant** à partir de la page de plug-ins.</span><span class="sxs-lookup"><span data-stu-id="ee508-116">Restarting the Unreal Editor by selecting **Restart Now** from the plugins page.</span></span> 

> [!NOTE]
> <span data-ttu-id="ee508-117">Si ce n’est déjà fait, vous devez installer les plug-ins **Microsoft Windows Mixed Reality** et **HoloLens** en suivant les instructions fournies dans la section **[Initialisation de votre projet](unreal-uxt-ch2.md)** de notre série de tutoriels Unreal.</span><span class="sxs-lookup"><span data-stu-id="ee508-117">If you haven't already, you'll need to install the **Microsoft Windows Mixed Reality** and **HoloLens** plugins by following the instructions in the **[Initializing your project](unreal-uxt-ch2.md)** section of our Unreal tutorial series.</span></span>

![Plug-in audio spatial Unreal](images/unreal-spatial-audio-img-01.png)

<span data-ttu-id="ee508-119">Une fois l’éditeur redémarré, vous pouvez commencer votre projet.</span><span class="sxs-lookup"><span data-stu-id="ee508-119">Once the editor restarts, your project is all set!</span></span>


## <a name="setting-the-spatialization-plugin-for-hololens-2-platform"></a><span data-ttu-id="ee508-120">Définition du plug-in de spatialisation pour la plateforme HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="ee508-120">Setting the spatialization plugin for HoloLens 2 platform</span></span>
<span data-ttu-id="ee508-121">La configuration du plug-in de spatialisation s’effectue sur la base de chaque plateforme.</span><span class="sxs-lookup"><span data-stu-id="ee508-121">Configuring the spatialization plugin is done on a per-platform basis.</span></span>  <span data-ttu-id="ee508-122">Pour activer le plug-in Microsoft Spatial Sound pour HoloLens 2, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ee508-122">You can enable the Microsoft Spatial Sound plugin for the HoloLens 2 by:</span></span>
1. <span data-ttu-id="ee508-123">Sélectionnez **Edit > Project Settings** (Modifier > Paramètres du projet), faites défiler jusque **Platforms**, puis cliquez sur **HoloLens**.</span><span class="sxs-lookup"><span data-stu-id="ee508-123">Selecting **Edit > Project Settings**, scrolling to **Platforms** and clicking **HoloLens**.</span></span>
2. <span data-ttu-id="ee508-124">Développez les propriétés **Audio** et affectez la valeur **Microsoft Spatial Sound** au champ **Spatialization Plugin**.</span><span class="sxs-lookup"><span data-stu-id="ee508-124">Expanding the **Audio** properties and setting the **Spatialization Plugin** field to **Microsoft Spatial Sound**.</span></span>

![Plug-in de spatialisation pour la plateforme HoloLens](images/unreal-spatial-audio-img-02.png)

<span data-ttu-id="ee508-126">Si vous prévoyez d’afficher un aperçu de votre application dans l’éditeur Unreal sur un PC de bureau, vous devez répéter les étapes ci-dessus pour la plateforme **Windows** :</span><span class="sxs-lookup"><span data-stu-id="ee508-126">If you're going to be previewing your application in the Unreal editor on a desktop PC, you'll need to repeat the above steps for the **Windows** platform:</span></span>

![Plug-in de spatialisation pour la plateforme Windows](images/unreal-spatial-audio-img-05.png)

## <a name="enabling-spatial-audio-on-your-workstation"></a><span data-ttu-id="ee508-128">Activation de l’audio spatial sur votre station de travail</span><span class="sxs-lookup"><span data-stu-id="ee508-128">Enabling spatial audio on your workstation</span></span>
<span data-ttu-id="ee508-129">L’audio spatial est désactivé par défaut sur les versions de bureau de Windows.</span><span class="sxs-lookup"><span data-stu-id="ee508-129">Spatial audio is disabled by default on desktop versions of Windows.</span></span> <span data-ttu-id="ee508-130">Pour l’activer, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ee508-130">You can enable it by:</span></span>
* <span data-ttu-id="ee508-131">Cliquez avec le bouton droit sur l’icône de **volume** dans la barre des tâches.</span><span class="sxs-lookup"><span data-stu-id="ee508-131">Right-clicking on the **volume** icon in the task bar.</span></span> 
    + <span data-ttu-id="ee508-132">Choisissez **Son spatial-> Windows Sonic pour casque** pour obtenir la meilleure représentation de ce que vous entendrez sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="ee508-132">Choose **Spatial sound -> Windows Sonic for Headphones** to get the best representation of what you'll hear on HoloLens 2.</span></span>

![Plug-in de spatialisation](images/unreal-spatial-audio-img-04.png)

> [!NOTE]
><span data-ttu-id="ee508-134">Ce paramètre est obligatoire uniquement si vous envisagez de tester votre projet dans l’éditeur Unreal.</span><span class="sxs-lookup"><span data-stu-id="ee508-134">This setting is only required if you plan to test your project in the Unreal editor.</span></span>

## <a name="creating-attenuation-objects"></a><span data-ttu-id="ee508-135">Création d’objets d’atténuation</span><span class="sxs-lookup"><span data-stu-id="ee508-135">Creating Attenuation objects</span></span>
<span data-ttu-id="ee508-136">Une fois que vous avez installé et configuré les plug-ins nécessaires :</span><span class="sxs-lookup"><span data-stu-id="ee508-136">After you've installed and configured the necessary plugins:</span></span>
1. <span data-ttu-id="ee508-137">Recherchez un acteur **Ambient Sound** (Son ambiant) dans la fenêtre **Place Actors** (Placer des acteurs), puis faites-le glisser dans la fenêtre **Scene**.</span><span class="sxs-lookup"><span data-stu-id="ee508-137">Search for an **Ambient Sound** actor in the **Place Actors** window and drag it into the **Scene** window.</span></span>

![Ajout d’un acteur de son ambiant](images/unreal-spatial-audio-img-07.png)

2. <span data-ttu-id="ee508-139">Faites de l’acteur **Ambient Sound** un enfant d’un visuel dans votre scène.</span><span class="sxs-lookup"><span data-stu-id="ee508-139">Make the **Ambient Sound** actor a child of a visual element in your scene.</span></span> 
    * <span data-ttu-id="ee508-140">Un acteur Ambient Sound n’a pas de représentation visuelle par défaut, donc vous n’entendrez un son que de sa position dans la scène.</span><span class="sxs-lookup"><span data-stu-id="ee508-140">An Ambient Sound actor doesn't have any visual representation by default, so you'll only hear a sound from its position in the scene.</span></span> <span data-ttu-id="ee508-141">Si vous l’attachez à un visuel, vous pouvez voir et déplacer l’acteur comme n’importe quel autre actif multimédia.</span><span class="sxs-lookup"><span data-stu-id="ee508-141">Attaching it to a visual element let's you see and move the actor like any other asset.</span></span>

3.  <span data-ttu-id="ee508-142">Cliquez avec le bouton droit sur **Content Browser** (Navigateur de contenu) et sélectionnez **Create Advanced Asset -> Sounds -> Sound Attenuation** (Créer un actif multimédia avancé -> Sons -> Atténuation du son) :</span><span class="sxs-lookup"><span data-stu-id="ee508-142">Right-click on the **Content Browser** and selecting **Create Advanced Asset -> Sounds -> Sound Attenuation**:</span></span>

![Création d’un actif multimédia d’atténuation du son](images/unreal-spatial-audio-img-06.png)

4. <span data-ttu-id="ee508-144">Cliquez avec le bouton droit sur l’élément **Sound Attenuation** dans la fenêtre **Content Browser** et sélectionnez l’option **Edit** pour afficher la fenêtre de propriétés.</span><span class="sxs-lookup"><span data-stu-id="ee508-144">Right-click on the **Sound Attenuation** asset in the **Content Browser** window and select the **Edit** option to bring up the properties window.</span></span>
    * <span data-ttu-id="ee508-145">Basculez l’option **Spatialization Method** sur **Binaural**.</span><span class="sxs-lookup"><span data-stu-id="ee508-145">Switch the **Spatialization Method** to **Binaural**.</span></span>

![Définir la méthode de spatialisation](images/unreal-spatial-audio-img-03.png)

5. <span data-ttu-id="ee508-147">Sélectionnez l’acteur **Ambient Sound** et faites défiler jusqu’à la section **Attenuation** dans le panneau **Details**.</span><span class="sxs-lookup"><span data-stu-id="ee508-147">Select the **Ambient Sound** actor and scroll down to the **Attenuation** section in the **Details** panel.</span></span> 
    * <span data-ttu-id="ee508-148">Affectez l’actif **Sound Attenuation** que vous avez créé comme valeur de la propriété **Attenuation Settings**.</span><span class="sxs-lookup"><span data-stu-id="ee508-148">Set the **Attenuation Settings** property to the **Sound Attenuation** asset you created.</span></span>

![Définir le paramètre d’atténuation](images/unreal-spatial-audio-img-08.png)

6. <span data-ttu-id="ee508-150">Définissez l’actif sonore (**Sound Asset**) que vous souhaitez attacher à l’acteur Ambient Sound en mettant à jour la propriété **Sound** de l’acteur Ambient Sound pour qu’elle spécifie le fichier SoundAsset à utiliser.</span><span class="sxs-lookup"><span data-stu-id="ee508-150">Set the **Sound Asset** you want to attach to the Ambient Sound actor by updating the **Sound** property of the Ambient Sound actor to specify the SoundAsset file to use.</span></span>

![Définir l’actif sonore](images/unreal-spatial-audio-img-09.png)

> [!NOTE] 
> <span data-ttu-id="ee508-152">Le fichier SoundAsset doit être mono pour être spatialisé avec le plug-in Microsoft Spatial Sound.</span><span class="sxs-lookup"><span data-stu-id="ee508-152">The SoundAsset file needs to be mono to be spatialized with the Microsoft Spatial Sound plug-in.</span></span> <span data-ttu-id="ee508-153">Vous trouverez les propriétés du fichier son en pointant sur l’actif multimédia dans la fenêtre Content Browser, comme indiqué dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ee508-153">You can find the sound file properties by hovering over the asset in the Content Browser window as shown in the screenshot below.</span></span>

![Nouvel actif multimédia d’atténuation du son](images/unreal-spatial-audio-img-10.png)

<span data-ttu-id="ee508-155">Une fois tous ces éléments configurés, le son ambiant peut être spatialisé à l’aide de la prise en charge du déchargement matériel dédié sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="ee508-155">Once all of this is configured the ambient sound can be spatialized using the dedicated hardware offload support on HoloLens 2.</span></span>

## <a name="configuring-objects-for-spatialization"></a><span data-ttu-id="ee508-156">Configuration des objets pour la spatialisation</span><span class="sxs-lookup"><span data-stu-id="ee508-156">Configuring objects for spatialization</span></span>
<span data-ttu-id="ee508-157">L’utilisation de l’audio spatial signifie que vous responsable de la gestion du comportement sonore dans un environnement virtuel.</span><span class="sxs-lookup"><span data-stu-id="ee508-157">Working with spatial audio means you're in charge of managing how sound behaves in a virtual environment.</span></span> <span data-ttu-id="ee508-158">Votre objectif principal est de créer des objets sonores qui semblent plus bruyants quand l’utilisateur est proche, et moins bruyants quand l’utilisateur est éloigné.</span><span class="sxs-lookup"><span data-stu-id="ee508-158">Your main focus is creating sound objects that appear louder when the user is close, and quieter when the user is far away.</span></span> <span data-ttu-id="ee508-159">C’est ce que l’on appelle l’atténuation sonore : faire en sorte que les sons semblent positionnés à un endroit fixe.</span><span class="sxs-lookup"><span data-stu-id="ee508-159">This is referred to as sound attenuation, making sounds appear as if they are positioned in a fixed spot.</span></span>

<span data-ttu-id="ee508-160">Tous les objets d’atténuation sont fournis avec des paramètres modifiables de :</span><span class="sxs-lookup"><span data-stu-id="ee508-160">All attenuation objects come with modifiable settings for:</span></span>
* <span data-ttu-id="ee508-161">Distance</span><span class="sxs-lookup"><span data-stu-id="ee508-161">Distance</span></span>
* <span data-ttu-id="ee508-162">Spatialisation</span><span class="sxs-lookup"><span data-stu-id="ee508-162">Spatialization</span></span>
* <span data-ttu-id="ee508-163">Absorption de l’air</span><span class="sxs-lookup"><span data-stu-id="ee508-163">Air Absorption</span></span>
* <span data-ttu-id="ee508-164">Focus de l’auditeur</span><span class="sxs-lookup"><span data-stu-id="ee508-164">Listener Focus</span></span>
* <span data-ttu-id="ee508-165">Envoi de réverbération</span><span class="sxs-lookup"><span data-stu-id="ee508-165">Reverb Send</span></span>
* <span data-ttu-id="ee508-166">Occlusion</span><span class="sxs-lookup"><span data-stu-id="ee508-166">Occlusion</span></span>

<span data-ttu-id="ee508-167">L’article [Sound attenuation in Unreal](https://docs.unrealengine.com/Engine/Audio/DistanceModelAttenuation/index.html) fournit des détails et des informations sur l’implémentation de chacun de ces aspects.</span><span class="sxs-lookup"><span data-stu-id="ee508-167">[Sound attenuation in Unreal](https://docs.unrealengine.com/Engine/Audio/DistanceModelAttenuation/index.html) has details and implementation specifics on each of these topics.</span></span>


## <a name="see-also"></a><span data-ttu-id="ee508-168">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ee508-168">See also</span></span>
* [<span data-ttu-id="ee508-169">Son spatial</span><span class="sxs-lookup"><span data-stu-id="ee508-169">Spatial Sound</span></span>](https://docs.microsoft.com/windows/mixed-reality/spatial-sound)
* [<span data-ttu-id="ee508-170">Conception du son spatial</span><span class="sxs-lookup"><span data-stu-id="ee508-170">Spatial Sound Design</span></span>](https://docs.microsoft.com/windows/mixed-reality/spatial-sound-design)
* [<span data-ttu-id="ee508-171">Réalité mixte - Fonctionnalités spatiales - Cours 220 : Son spatial</span><span class="sxs-lookup"><span data-stu-id="ee508-171">MR Spatial 220: Spatial sound</span></span>](https://docs.microsoft.com/windows/mixed-reality/holograms-220)