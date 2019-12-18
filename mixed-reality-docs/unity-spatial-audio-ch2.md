---
title: Didacticiels audio spatiaux-2. Sons d’interaction du bouton d’aménagement
description: Ajoutez un bouton à votre projet et spatialez les sons d’interaction du bouton.
author: kegodin
ms.author: kegodin
ms.date: 12/01/2019
ms.topic: article
keywords: réalité mixte, Unity, tutorial, hololens2, audio spatial
ms.openlocfilehash: bd70e3bc88ee39b2c6257089ac3a2b93dfae0ad1
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75182776"
---
# <a name="spatializing-button-interaction-sounds"></a><span data-ttu-id="a9aed-105">Sons d’interaction du bouton d’aménagement</span><span class="sxs-lookup"><span data-stu-id="a9aed-105">Spatializing button interaction sounds</span></span>

## <a name="objectives"></a><span data-ttu-id="a9aed-106">Objectifs</span><span class="sxs-lookup"><span data-stu-id="a9aed-106">Objectives</span></span>
<span data-ttu-id="a9aed-107">Dans ce deuxième chapitre du module audio spatial des didacticiels HoloLens 2, vous allez :</span><span class="sxs-lookup"><span data-stu-id="a9aed-107">In this second chapter of the spatial audio module of the HoloLens 2 tutorials, you'll:</span></span>
* <span data-ttu-id="a9aed-108">Ajouter un bouton</span><span class="sxs-lookup"><span data-stu-id="a9aed-108">Add a button</span></span>
* <span data-ttu-id="a9aed-109">Spatialiser le clic sur le bouton</span><span class="sxs-lookup"><span data-stu-id="a9aed-109">Spatialize the button click sounds</span></span>

## <a name="add-a-button"></a><span data-ttu-id="a9aed-110">Ajouter un bouton</span><span class="sxs-lookup"><span data-stu-id="a9aed-110">Add a button</span></span>
<span data-ttu-id="a9aed-111">Dans le volet **projet** , sélectionnez **ressources** et tapez « PressableButtonHoloLens2 » dans la barre de recherche :</span><span class="sxs-lookup"><span data-stu-id="a9aed-111">In the **Project** pane, select **Assets** and type "PressableButtonHoloLens2" in the search bar:</span></span>

![Bouton Prefab dans les ressources](images/spatial-audio/button-prefab-in-assets.png)

<span data-ttu-id="a9aed-113">Le bouton Prefab est l’entrée représentée par une icône bleue, plutôt qu’une icône blanche.</span><span class="sxs-lookup"><span data-stu-id="a9aed-113">The button prefab is the entry represented by a blue icon, rather than a white icon.</span></span> <span data-ttu-id="a9aed-114">Faites glisser le Prefab nommé **PressableButtonHoloLens2** dans le volet **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="a9aed-114">Drag the prefab named **PressableButtonHoloLens2** into the **Hierarchy** pane.</span></span> <span data-ttu-id="a9aed-115">Dans le volet de l' **inspecteur** de votre nouveau bouton, définissez la propriété **position** sur (0,-0,4, 2) afin qu’elle s’affiche devant l’utilisateur au démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="a9aed-115">In the **Inspector** pane for your new button, set the **Position** property to (0, -0.4, 2) so that it will appear in front of the user when the application starts.</span></span> <span data-ttu-id="a9aed-116">Le composant **transformer** du bouton se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9aed-116">The **Transform** component of the button will look like this:</span></span>

![Transformation de bouton](images/spatial-audio/button-transform.png)

## <a name="spatialize-button-feedback"></a><span data-ttu-id="a9aed-118">Commentaires sur le bouton spatial</span><span class="sxs-lookup"><span data-stu-id="a9aed-118">Spatialize button feedback</span></span>
<span data-ttu-id="a9aed-119">Dans cette étape, vous allez spatialiser les commentaires audio pour le bouton.</span><span class="sxs-lookup"><span data-stu-id="a9aed-119">In this step, you'll spatialize the audio feedback for the button.</span></span> <span data-ttu-id="a9aed-120">Pour obtenir des suggestions de conception associées, consultez [conception de son spatial](spatial-sound-design.md).</span><span class="sxs-lookup"><span data-stu-id="a9aed-120">For related design suggestions, see [spatial sound design](spatial-sound-design.md).</span></span> 

<span data-ttu-id="a9aed-121">Le volet **mixage audio** vous permet de définir des destinations, appelées **groupes de mixage**, pour la lecture audio à partir de composants **sources audio** .</span><span class="sxs-lookup"><span data-stu-id="a9aed-121">The **Audio Mixer** pane is where you'll define destinations, called **Mixer Groups**, for audio playback from **Audio Source** components.</span></span> 
* <span data-ttu-id="a9aed-122">Ouvrez le volet **mixage audio** à partir de la barre de menus à l’aide de la **fenêtre > Audio-> mixage audio**</span><span class="sxs-lookup"><span data-stu-id="a9aed-122">Open the **Audio Mixer** pane from the menu bar using **Window -> Audio -> Audio Mixer**</span></span>
* <span data-ttu-id="a9aed-123">Créez un **mélangeur** en cliquant sur le signe « + » en regard de **mixages**.</span><span class="sxs-lookup"><span data-stu-id="a9aed-123">Create a **Mixer** by clicking the '+' next to **Mixers**.</span></span> <span data-ttu-id="a9aed-124">Le nouveau mélangeur inclura un **groupe** par défaut nommé **maître**.</span><span class="sxs-lookup"><span data-stu-id="a9aed-124">The new mixer will include a default **Group** called **Master**.</span></span>

<span data-ttu-id="a9aed-125">Le volet de **mixage** ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a9aed-125">Your **Mixer** pane will now look like this:</span></span>

![Panneau de mixage avec le premier mélangeur](images/spatial-audio/mixer-panel-with-first-mixer.png)

> [!NOTE]
> <span data-ttu-id="a9aed-127">Jusqu’à ce que la réverbération soit activée dans le [Chapitre 5](unity-spatial-audio-ch5.md), le compteur de volume du mélangeur n’affiche pas l’activité des sons joués par Microsoft Spatializer</span><span class="sxs-lookup"><span data-stu-id="a9aed-127">Until reverb is enabled in [Chapter 5](unity-spatial-audio-ch5.md), the mixer's volume meter doesn't show activity for sounds played through the Microsoft Spatializer</span></span>

<span data-ttu-id="a9aed-128">Dans le volet **hiérarchie** , cliquez sur **PressableButtonHoloLens2** .</span><span class="sxs-lookup"><span data-stu-id="a9aed-128">Click the **PressableButtonHoloLens2** in the **Hierarchy** pane.</span></span> <span data-ttu-id="a9aed-129">Dans le volet **inspecteur** :</span><span class="sxs-lookup"><span data-stu-id="a9aed-129">In the **Inspector** pane:</span></span>
1. <span data-ttu-id="a9aed-130">Rechercher le composant **source audio**</span><span class="sxs-lookup"><span data-stu-id="a9aed-130">Find the **Audio Source** component</span></span>
2. <span data-ttu-id="a9aed-131">Pour la propriété **sortie** , cliquez sur le sélecteur et choisissez votre mélangeur</span><span class="sxs-lookup"><span data-stu-id="a9aed-131">For the **Output** property, click the selector and choose your mixer</span></span>
3. <span data-ttu-id="a9aed-132">Cochez la case **spatialiser**</span><span class="sxs-lookup"><span data-stu-id="a9aed-132">Check the **Spatialize** checkbox</span></span>
4. <span data-ttu-id="a9aed-133">Déplacez le curseur de **lissage spatial** vers 3D (1).</span><span class="sxs-lookup"><span data-stu-id="a9aed-133">Move the **Spatial Blend** slider to 3D (1).</span></span>

> [!NOTE]
> <span data-ttu-id="a9aed-134">Dans les versions de Unity antérieures à 2019, la case à cocher « spatialiser » se trouve en bas du volet de l' **inspecteur** pour la **source audio**.</span><span class="sxs-lookup"><span data-stu-id="a9aed-134">In versions of Unity prior to 2019, the 'Spatialize' checkbox is at the bottom of the **Inspector** pane for the **Audio Source**.</span></span>

<span data-ttu-id="a9aed-135">Une fois ces modifications effectuées, le composant **source audio** de votre **PressableButtonHoloLens2** se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9aed-135">After these changes, the **Audio Source** component of your **PressableButtonHoloLens2** will look like this:</span></span>

![Source audio du bouton](images/spatial-audio/button-audio-source.png)

> [!NOTE]
> <span data-ttu-id="a9aed-137">Si vous déplacez le **lissage spatial** sur 1 (3d) sans activer la case à cocher **spatialiser** , Unity utilise son Spatializer panoramique, au lieu du **Spatializer Microsoft** avec HRTFs.</span><span class="sxs-lookup"><span data-stu-id="a9aed-137">If you move **Spatial Blend** to 1 (3D) without checking the **Spatialize** checkbox, Unity will use its panning spatializer, instead of the **Microsoft Spatializer** with HRTFs.</span></span>

## <a name="adjust-the-volume-curve"></a><span data-ttu-id="a9aed-138">Ajuster la courbe du volume</span><span class="sxs-lookup"><span data-stu-id="a9aed-138">Adjust the Volume curve</span></span>
<span data-ttu-id="a9aed-139">Par défaut, Unity atténue les sons spatiaux au fur et à mesure qu’ils s’éloignent de l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="a9aed-139">By default, Unity will attenuate spatialized sounds as they get farther from the listener.</span></span> <span data-ttu-id="a9aed-140">Lorsque cette atténuation est appliquée à des sons d’interaction, l’interface peut devenir plus difficile à utiliser.</span><span class="sxs-lookup"><span data-stu-id="a9aed-140">When this attenuation is applied to interaction feedback sounds, the interface can become more difficult to use.</span></span>

<span data-ttu-id="a9aed-141">Pour désactiver cette atténuation, ajustez la courbe du **volume** .</span><span class="sxs-lookup"><span data-stu-id="a9aed-141">To disable this attenuation, adjust the **Volume** curve.</span></span> <span data-ttu-id="a9aed-142">Dans le composant **source audio** du volet de l' **inspecteur** pour **PressableButtonHoloLens2**, il existe une section intitulée **paramètres audio 3D**.</span><span class="sxs-lookup"><span data-stu-id="a9aed-142">In the **Audio Source** component of the **Inspector** pane for the **PressableButtonHoloLens2**, there is a section called **3D Sound Settings**.</span></span> <span data-ttu-id="a9aed-143">Dans cette section :</span><span class="sxs-lookup"><span data-stu-id="a9aed-143">In that section:</span></span>
1. <span data-ttu-id="a9aed-144">Définir la propriété **volume Rolloff** sur Linear</span><span class="sxs-lookup"><span data-stu-id="a9aed-144">Set the **Volume Rolloff** property to Linear</span></span>
2. <span data-ttu-id="a9aed-145">Faites glisser le point de terminaison sur la courbe de **volume** (la courbe rouge) de « 0 » sur l’axe y jusqu’à « 1 »</span><span class="sxs-lookup"><span data-stu-id="a9aed-145">Drag the endpoint on the **Volume** curve (the red curve) from '0' on the y axis up to '1'</span></span>
3. <span data-ttu-id="a9aed-146">Pour ajuster la forme de la courbe de **volume** à plat, faites glisser le contrôle de forme de courbe blanche pour qu’il soit parallèle à l’axe X.</span><span class="sxs-lookup"><span data-stu-id="a9aed-146">To adjust the shape of the **Volume** curve to be flat, drag the white curve shape control to be parallel to the X axis</span></span>

<span data-ttu-id="a9aed-147">Une fois ces modifications effectuées, la section **paramètres audio 3D** des propriétés de la **source audio** de l' **PressableButtonHoloLens2** se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9aed-147">After these changes, the **3D Sound Settings** section of the **Audio Source** properties of the **PressableButtonHoloLens2** will look like this:</span></span>

![Paramètres audio de bouton 3D](images/spatial-audio/button-3d-sound-settings.png)

## <a name="next-steps"></a><span data-ttu-id="a9aed-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9aed-149">Next steps</span></span>

<span data-ttu-id="a9aed-150">Essayez votre application sur un HoloLens 2 ou dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="a9aed-150">Try out your app on a HoloLens 2, or in the Unity editor.</span></span> <span data-ttu-id="a9aed-151">Dans l’application, vous pouvez toucher le bouton et entendre les sons d’interaction du bouton spatial.</span><span class="sxs-lookup"><span data-stu-id="a9aed-151">In the app, you can touch the button and hear the spatialized button interaction sounds.</span></span>

<span data-ttu-id="a9aed-152">Lors du test dans l’éditeur Unity, appuyez sur la barre d’espace et faites défiler la molette pour activer la simulation manuelle.</span><span class="sxs-lookup"><span data-stu-id="a9aed-152">When testing in the Unity editor, press the space bar and scroll with the scroll wheel to activate hand simulation.</span></span> <span data-ttu-id="a9aed-153">Pour plus d’informations, consultez la [documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene).</span><span class="sxs-lookup"><span data-stu-id="a9aed-153">For more info, see the [MRTK documentation](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene).</span></span>

<span data-ttu-id="a9aed-154">Passez au [chapitre 3](unity-spatial-audio-ch3.md) pour ajouter une vidéo à votre application et spatialer l’audio de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="a9aed-154">Continue to [Chapter 3](unity-spatial-audio-ch3.md) to add a video to your app, and spatialize the audio from the video.</span></span>

