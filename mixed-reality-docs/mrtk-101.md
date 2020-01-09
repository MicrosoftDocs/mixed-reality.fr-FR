---
title: MRTK 101-utilisation de Mixed Reality Toolkit Unity pour les interactions de base (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)
description: Comment utiliser le kit de procédures pratiques de réalité mixte pour les interactions de base (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)
author: cre8ivepark
ms.author: dongpark
ms.date: 08/27/2019
ms.topic: article
keywords: HoloLens, MRTK, kit d’outils de réalité mixte, Windows Mixed Reality, conception, exemple d’application, contrôles
ms.openlocfilehash: ad9d2755522c2610ae051fa61f96605e49404d2d
ms.sourcegitcommit: 5054f5c23965ce56599cb29ac9d9c6e48812dabd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2020
ms.locfileid: "75623496"
---
# <a name="mrtk-101-how-to-use-mixed-reality-toolkit-unity-for-basic-interactions-hololens-2-hololens-windows-mixed-reality-openvr"></a><span data-ttu-id="815a3-104">MRTK 101 : comment utiliser le kit de tâches de la réalité mixte pour les interactions de base (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)</span><span class="sxs-lookup"><span data-stu-id="815a3-104">MRTK 101: How to use Mixed Reality Toolkit Unity for Basic Interactions (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)</span></span>

![MRTK](images/MRTK101/MRTK101Cover.png)

<span data-ttu-id="815a3-106">Découvrez comment utiliser MRTK pour obtenir certains des modèles d’interaction les plus couramment utilisés dans la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="815a3-106">Learn about how to use MRTK to achieve some of the most widely used common interaction patterns in mixed reality.</span></span>

- <span data-ttu-id="815a3-107">Comment simuler des interactions d’entrée dans l’éditeur Unity ?</span><span class="sxs-lookup"><span data-stu-id="815a3-107">How to simulate input interactions in Unity editor?</span></span>
- <span data-ttu-id="815a3-108">Comment récupérer et déplacer un objet ?</span><span class="sxs-lookup"><span data-stu-id="815a3-108">How to grab and move an object?</span></span>
- <span data-ttu-id="815a3-109">Comment redimensionner un objet ?</span><span class="sxs-lookup"><span data-stu-id="815a3-109">How to resize an object?</span></span>
- <span data-ttu-id="815a3-110">Comment déplacer ou faire pivoter un objet avec une précision ?</span><span class="sxs-lookup"><span data-stu-id="815a3-110">How to move or rotate an object with precision?</span></span>
- <span data-ttu-id="815a3-111">Comment faire en sorte qu’un objet réponde aux événements d’entrée ?</span><span class="sxs-lookup"><span data-stu-id="815a3-111">How to make an object respond to input events?</span></span>
- <span data-ttu-id="815a3-112">Comment ajouter des commentaires visuels ?</span><span class="sxs-lookup"><span data-stu-id="815a3-112">How to add visual feedback?</span></span>
- <span data-ttu-id="815a3-113">Comment ajouter des commentaires audio ?</span><span class="sxs-lookup"><span data-stu-id="815a3-113">How to add audio feedback?</span></span>
- <span data-ttu-id="815a3-114">Comment utiliser le bouton de style HoloLens 2 prefabs ?</span><span class="sxs-lookup"><span data-stu-id="815a3-114">How to use HoloLens 2 style button prefabs?</span></span>
- <span data-ttu-id="815a3-115">Comment faire en sorte qu’un objet suive votre propos ?</span><span class="sxs-lookup"><span data-stu-id="815a3-115">How to make an object follow you?</span></span>
- <span data-ttu-id="815a3-116">Comment faire face à un objet ?</span><span class="sxs-lookup"><span data-stu-id="815a3-116">How to make an object face you?</span></span>

## <a name="how-to-simulate-input-interactions-in-unityeditor"></a><span data-ttu-id="815a3-117">Comment simuler des interactions d’entrée dans l’éditeur Unity ?</span><span class="sxs-lookup"><span data-stu-id="815a3-117">How to simulate input interactions in Unity editor?</span></span>
<span data-ttu-id="815a3-118">MRTK prend en charge la simulation d’entrée dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="815a3-118">MRTK supports in-editor input simulation.</span></span> <span data-ttu-id="815a3-119">Exécutez simplement votre scène en cliquant sur le bouton de lecture d’Unity.</span><span class="sxs-lookup"><span data-stu-id="815a3-119">Simply run your scene by clicking Unity's play button.</span></span> <span data-ttu-id="815a3-120">Utilisez ces clés pour simuler l’entrée.</span><span class="sxs-lookup"><span data-stu-id="815a3-120">Use these keys to simulate input.</span></span>
<span data-ttu-id="815a3-121">Appuyez sur les touches W, A, S, D pour déplacer l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="815a3-121">Press W, A, S, D keys to move the camera.</span></span>
<span data-ttu-id="815a3-122">Maintenez le bouton droit de la souris et déplacez la souris pour regarder.</span><span class="sxs-lookup"><span data-stu-id="815a3-122">Hold the right mouse button and move the mouse to look around.</span></span>
<span data-ttu-id="815a3-123">Pour faire apparaître les mains simulées, appuyez sur la barre d’espace (droite) ou sur la touche gauche (gauche) pour conserver les mains simulées dans la vue, appuyez sur la touche T ou Y pour faire pivoter les mains simulées, appuyez sur Q ou E (horizontal)/R ou F (vertical)</span><span class="sxs-lookup"><span data-stu-id="815a3-123">To bring up the simulated hands, press Space bar(Right hand) or left Shift key(Left hand) To keep simulated hands in the view, press T or Y key To rotate simulated hands, press Q or E(horizontal) / R or F(vertical)</span></span>

- [<span data-ttu-id="815a3-124">En savoir plus sur la simulation d’entrée dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-124">Learn more about Input Simulation in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/InputSimulation/InputSimulationService.html)


## <a name="how-to-grab-and-move-anobject"></a><span data-ttu-id="815a3-125">Comment récupérer et déplacer un objet ?</span><span class="sxs-lookup"><span data-stu-id="815a3-125">How to grab and move an object?</span></span>
<span data-ttu-id="815a3-126">Pour rendre un objet pouvant être extrait, assignez ces deux scripts : ManipulationHandler.cs et NearInteractionGrabbable. cs (pour la saisie directe avec l’entrée de suivi articulé) ManipulationHandler prend en charge les interactions près et éloignées.</span><span class="sxs-lookup"><span data-stu-id="815a3-126">To make an object grabbable, assign these two scripts: ManipulationHandler.cs and NearInteractionGrabbable.cs(for direct grab with articulated hand tracking input) ManipulationHandler supports both near and far interactions.</span></span> <span data-ttu-id="815a3-127">Vous pouvez saisir et déplacer un objet avec l’entrée de suivi articulé de HoloLens 2 (Near), le rayon de main (FAR), le faisceau de contrôle de mouvement (FAR), le curseur de pointeur HoloLens & le robinet d’air (FAR).</span><span class="sxs-lookup"><span data-stu-id="815a3-127">You can grab and move an object with HoloLens 2's articulated hand tracking input(near), hand ray(far), motion controller's beam(far), HoloLens gaze cursor & air-tap(far).</span></span>

<img alt="NearInteractionGrabbable and ManipulationHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_ManipulationHandler.png">

<img alt="NearInteractionGrabbable and ManipulationHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_GrabMove.gif">


## <a name="how-to-resize-anobject"></a><span data-ttu-id="815a3-128">Comment redimensionner un objet ?</span><span class="sxs-lookup"><span data-stu-id="815a3-128">How to resize an object?</span></span>
<span data-ttu-id="815a3-129">ManipulationHandler.cs prend en charge la rotation/la mise à l’échelle à deux mains.</span><span class="sxs-lookup"><span data-stu-id="815a3-129">ManipulationHandler.cs supports two-handed scale/rotation.</span></span> <span data-ttu-id="815a3-130">Cela fonctionne avec différents types d’entrée tels que l’entrée articulée du langage HoloLens 2, le point de contrôle du point d’entrée du regard et du point de présence du point de contrôle de l’entrée de commande du casque Windows Mixed Realing.</span><span class="sxs-lookup"><span data-stu-id="815a3-130">This works with various input types such as HoloLens 2's articulated hand input, HoloLens 1's gaze + gesture input, and Windows Mixed Reality immersive headset's motion controller input.</span></span>

- [<span data-ttu-id="815a3-131">En savoir plus sur le gestionnaire de manipulation dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-131">Learn more about Manipulation Handler in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html)

<img alt="NearInteractionGrabbable and ManipulationHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_ManipulationHandler.gif">

## <a name="how-to-move-or-rotate-an-object-with-precision"></a><span data-ttu-id="815a3-132">Comment déplacer ou faire pivoter un objet avec une précision ?</span><span class="sxs-lookup"><span data-stu-id="815a3-132">How to move or rotate an object with precision?</span></span>
<span data-ttu-id="815a3-133">Assignez BoundingBox.cs à un objet pour utiliser le cadre englobant qui est l’interface pour la mise à l’échelle et la rotation d’un objet.</span><span class="sxs-lookup"><span data-stu-id="815a3-133">Assign BoundingBox.cs to an object to use Bounding Box which is the interface for scaling and rotating an object.</span></span> <span data-ttu-id="815a3-134">Par défaut, il affiche les handles et les câbles bleus de style HoloLens 1.</span><span class="sxs-lookup"><span data-stu-id="815a3-134">By default, it shows HoloLens 1 style blue handles and wires.</span></span> <span data-ttu-id="815a3-135">Pour utiliser des handles animés basés sur le style HoloLens 2, vous devez assigner des prefabs et des matériaux.</span><span class="sxs-lookup"><span data-stu-id="815a3-135">To use HoloLens 2 style proximity-based animated handles, you need to assign prefabs and materials.</span></span> <span data-ttu-id="815a3-136">Pour plus d’informations sur la configuration, reportez-vous à la [documentation du cadre englobant](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) et à la scène BoundingBoxExamples. Unity.</span><span class="sxs-lookup"><span data-stu-id="815a3-136">Please refer to [Bounding Box documentation](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) and the BoundingBoxExamples.unity scene for the configuration details.</span></span>

<img alt="BoundingBox.cs assigned to an object" width="800" src="images/MRTK101/MRTK_BoundingBox.png">

<img alt="BoundingBox.cs assigned to an object" width="800" src="images/MRTK101/MRTK_BoundingBox.gif">


- [<span data-ttu-id="815a3-137">En savoir plus sur le cadre englobant dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-137">Learn more about Bounding Box in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)

## <a name="how-to-make-an-object-respond-to-inputevents"></a><span data-ttu-id="815a3-138">Comment faire en sorte qu’un objet réponde aux événements d’entrée ?</span><span class="sxs-lookup"><span data-stu-id="815a3-138">How to make an object respond to input events?</span></span>
<span data-ttu-id="815a3-139">Assignez PointerHandler.cs à un objet.</span><span class="sxs-lookup"><span data-stu-id="815a3-139">Assign PointerHandler.cs to an object.</span></span> <span data-ttu-id="815a3-140">Dans l’inspecteur, vous serez en mesure d’utiliser les événements OnPointerDown (), OnPointerUp (), OnPointerClicked (), OnPointerDragged () pour utiliser ces événements dans un script, implémentez IMixedRealityPointerHandler.</span><span class="sxs-lookup"><span data-stu-id="815a3-140">In the inspector, you will be able to use events OnPointerDown(), OnPointerUp(), OnPointerClicked(), OnPointerDragged() To use these events in a script, implement IMixedRealityPointerHandler.</span></span>

<img alt="PointerHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_PointerHandler.png">

- [<span data-ttu-id="815a3-141">En savoir plus sur le système d’entrée dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-141">Learn more about Input System in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html)

## <a name="how-to-add-visual-feedback"></a><span data-ttu-id="815a3-142">Comment ajouter des commentaires visuels ?</span><span class="sxs-lookup"><span data-stu-id="815a3-142">How to add visual feedback?</span></span>
<span data-ttu-id="815a3-143">Assignez Interactable.cs à un objet.</span><span class="sxs-lookup"><span data-stu-id="815a3-143">Assign Interactable.cs to an object.</span></span> <span data-ttu-id="815a3-144">Dans l’inspecteur, créez un nouveau thème.</span><span class="sxs-lookup"><span data-stu-id="815a3-144">In the inspector, create a new theme.</span></span> <span data-ttu-id="815a3-145">À l’aide des profils de thème interactifs, vous pouvez facilement ajouter des commentaires visuels à tous les États d’interaction d’entrée disponibles.</span><span class="sxs-lookup"><span data-stu-id="815a3-145">Using Interactable's theme profiles, you can easily add visual feedback to all available input interaction states.</span></span>

<img alt="PointerHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_Interactable.png">

<img alt="Interactable" width="800" src="images/MRTK101/MRTK_Interactable.gif">


<span data-ttu-id="815a3-146">L’interaction interactive fournit différents types de thèmes, y compris le thème du nuanceur, qui vous permet de contrôler les propriétés de l’état du nuanceur par interaction.</span><span class="sxs-lookup"><span data-stu-id="815a3-146">Interactable provides various types of themes including the shader theme which allows you to control properties of the shader per interaction state.</span></span>

- [<span data-ttu-id="815a3-147">En savoir plus sur les informations d’interaction dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-147">Learn more about Interactable in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)

<span data-ttu-id="815a3-148">Un autre bloc de construction important pour les commentaires visuels est le nuanceur standard MRTK.</span><span class="sxs-lookup"><span data-stu-id="815a3-148">Another important building block for visual feedback is the MRTK Standard Shader.</span></span> <span data-ttu-id="815a3-149">Avec le nuanceur standard MRTK, vous pouvez facilement ajouter des effets de commentaires visuels tels que la lumière de survol et la lumière de proximité.</span><span class="sxs-lookup"><span data-stu-id="815a3-149">With MRTK Standard Shader, you can easily add visual feedback effects such as hover light and proximity light.</span></span> <span data-ttu-id="815a3-150">Étant donné que le nuanceur standard MRTK effectue un calcul beaucoup moins important que le nuanceur standard Unity, vous pouvez créer une expérience performante.</span><span class="sxs-lookup"><span data-stu-id="815a3-150">Since MRTK Standard shader performs significantly less computation than the Unity Standard shader, you can create a performant experience.</span></span>

<span data-ttu-id="815a3-151">Créez un nouveau matériau et sélectionnez le nuanceur « Mixed Reality Toolkit > standard ».</span><span class="sxs-lookup"><span data-stu-id="815a3-151">Create a new material and select the Shader 'Mixed Reality Toolkit > Standard'.</span></span> <span data-ttu-id="815a3-152">Ou vous pouvez choisir l’un des matériaux existants qui utilisent le nuanceur standard MRTK.</span><span class="sxs-lookup"><span data-stu-id="815a3-152">Or you can pick one of the existing materials that use MRTK Standard Shader.</span></span>

<img alt="MRTK Standard Shader" width="400" src="images/MRTK101/MRTK_Shader0.png">
<br/><br/>
<img alt="MRTK Standard Shader" width="800" src="images/MRTK101/MRTK_Shader1.png">

<img alt="MRTK Standard Shader" width="800" src="images/MRTK101/MRTK_Shader.gif">


- [<span data-ttu-id="815a3-153">En savoir plus sur le nuanceur MRTK standard dans la documentation de MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-153">Learn more about MRTK Standard Shader in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_MRTKStandardShader.html)

## <a name="how-to-add-audio-feedback"></a><span data-ttu-id="815a3-154">Comment ajouter des commentaires audio ?</span><span class="sxs-lookup"><span data-stu-id="815a3-154">How to add audio feedback?</span></span>
<span data-ttu-id="815a3-155">Ajoutez AudioSource à un objet.</span><span class="sxs-lookup"><span data-stu-id="815a3-155">Add AudioSource to an object.</span></span> <span data-ttu-id="815a3-156">Ensuite, dans les scripts qui exposent des événements d’entrée (par exemple, Interactable.cs ou PointerHandler.cs), assignez l’objet à l’événement et sélectionnez AudioSource. PlayOneShot ().</span><span class="sxs-lookup"><span data-stu-id="815a3-156">Then, in the scripts that exposes input events(e.g. Interactable.cs or PointerHandler.cs), assign the object to the event and select AudioSource.PlayOneShot().</span></span> <span data-ttu-id="815a3-157">Vous pouvez utiliser vos clips audio ou en choisir un à partir des ressources audio de MRTK.</span><span class="sxs-lookup"><span data-stu-id="815a3-157">You can use your audio clips or choose one from MRTK's audio assets.</span></span>

<img alt="Audio Source assigned to an object. AudioSource.PlayOneShot configured in the Interactable's OnPress() and OnRelease() events." width="800" src="images/MRTK101/MRTK_Audio.png">

## <a name="how-to-use-hololens-2-style-buttonprefabs"></a><span data-ttu-id="815a3-158">Comment utiliser le bouton de style HoloLens 2 prefabs ?</span><span class="sxs-lookup"><span data-stu-id="815a3-158">How to use HoloLens 2 style button prefabs?</span></span>
<span data-ttu-id="815a3-159">MRTK fournit différents types de boutons de style de Shell (système d’exploitation) HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="815a3-159">MRTK provides various types of HoloLens 2's shell(OS) style buttons.</span></span> <span data-ttu-id="815a3-160">Il fournit des commentaires visuels sophistiqués, tels que la lumière de proximité, la zone de compression et un effet de ondulation sur l’aire du bouton.</span><span class="sxs-lookup"><span data-stu-id="815a3-160">It provides sophisticated visual feedbacks such as proximity light, compressing box, and a ripple effect on the button surface.</span></span>

<img alt="Interactable" width="800" src="images/MRTK101/MRTK_Button.gif">

<span data-ttu-id="815a3-161">Il vous suffit de faire glisser et déposer l’un des boutons Prefab de style HoloLens 2 sur votre scène.</span><span class="sxs-lookup"><span data-stu-id="815a3-161">Simply drag and drop one of the HoloLens 2 style pressable button prefab into your scene.</span></span> <span data-ttu-id="815a3-162">Prefab utilise Interactable.cs, qui est présenté ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="815a3-162">The prefab uses Interactable.cs which is introduced above.</span></span> <span data-ttu-id="815a3-163">Vous pouvez utiliser des événements exposés tels que OnClick () dans le pour déclencher des actions.</span><span class="sxs-lookup"><span data-stu-id="815a3-163">You can use exposed events such as OnClick() in the Interactable to trigger actions.</span></span>

<img alt="HoloLens 2 Button Prefab" width="800" src="images/MRTK101/MRTK_Button.png">

- [<span data-ttu-id="815a3-164">En savoir plus sur le bouton prefabs dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-164">Learn more about Button prefabs in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)

## <a name="how-to-make-an-object-followyou"></a><span data-ttu-id="815a3-165">Comment faire en sorte qu’un objet suive votre propos ?</span><span class="sxs-lookup"><span data-stu-id="815a3-165">How to make an object follow you?</span></span>
<span data-ttu-id="815a3-166">Assignez le script RadialView.cs à un objet.</span><span class="sxs-lookup"><span data-stu-id="815a3-166">Assign RadialView.cs script to an object.</span></span> <span data-ttu-id="815a3-167">Il fait partie de la série de scripts du solveur qui vous permet d’obtenir divers types de positionnement des objets dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="815a3-167">It is part of the Solver script series that allows you to achieve various types of object positioning in 3D space.</span></span> <span data-ttu-id="815a3-168">SolverHandler.cs sera automatiquement ajouté.</span><span class="sxs-lookup"><span data-stu-id="815a3-168">SolverHandler.cs will be automatically added.</span></span>
<span data-ttu-id="815a3-169">Vous trouverez ci-dessous un exemple de configuration de RadialView pour obtenir une balise de suivi tardif, tout comme le menu Démarrer dans l’interpréteur de commandes HoloLens.</span><span class="sxs-lookup"><span data-stu-id="815a3-169">Below is an example of RadialView configuration to achieve 'lazy follow' tag-along behavior just like the Start menu in the HoloLens shell.</span></span> <span data-ttu-id="815a3-170">Vous pouvez spécifier la distance minimale/maximale et les niveaux d’affichage minimal/maximal.</span><span class="sxs-lookup"><span data-stu-id="815a3-170">You can specify the minimum/maximum distance and minimum/maximum view degrees.</span></span> <span data-ttu-id="815a3-171">L’exemple ci-dessous montre le positionnement de l’objet entre 0,4 mètre et 0,8 m dans la plage de 15 °.</span><span class="sxs-lookup"><span data-stu-id="815a3-171">The example below shows positioning the object between 0.4m and 0.8m range within 15°.</span></span> <span data-ttu-id="815a3-172">Ajustez les valeurs de temps Lerp pour accélérer ou ralentir la mise à jour de position.</span><span class="sxs-lookup"><span data-stu-id="815a3-172">Adjust Lerp Time values to make the positional update faster or slower.</span></span>

<img alt="MRTK Standard Shader" width="400" src="images/MRTK101/MRTK_SolverRadialView.png">

<img alt="Interactable" width="800" src="images/MRTK101/MRTK_RadialViewSolver.gif">

- [<span data-ttu-id="815a3-173">En savoir plus sur les programmes de résolution dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-173">Learn more about Solvers in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html)

## <a name="how-to-make-an-object-faceyou"></a><span data-ttu-id="815a3-174">Comment faire face à un objet ?</span><span class="sxs-lookup"><span data-stu-id="815a3-174">How to make an object face you?</span></span>
<span data-ttu-id="815a3-175">Assignez le script Billboard.cs à un objet.</span><span class="sxs-lookup"><span data-stu-id="815a3-175">Assign Billboard.cs script to an object.</span></span> <span data-ttu-id="815a3-176">Elle sera toujours face à vous, quelle que soit votre position.</span><span class="sxs-lookup"><span data-stu-id="815a3-176">It will always face you, regardless of your position.</span></span> <span data-ttu-id="815a3-177">Vous pouvez spécifier l’option d’axe pivot.</span><span class="sxs-lookup"><span data-stu-id="815a3-177">You can specify the pivot axis option.</span></span>

<img alt="Billboard.cs script assigned to an object with Pivot Axis option Y" width="800" src="images/MRTK101/MRTK_Billboard.png">

<img alt="Billboard.cs script assigned to an object with Pivot Axis option Y" width="800" src="images/MRTK101/MRTK_Billboard.gif">


<span data-ttu-id="815a3-178">Vous êtes prêt à créer des expériences étonnantes pour la réalité mixte ?</span><span class="sxs-lookup"><span data-stu-id="815a3-178">Ready to create amazing experiences for mixed reality?</span></span> <span data-ttu-id="815a3-179">Visitez les pages ci-dessous et apprenez-en davantage sur MRTK et la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="815a3-179">Visit the pages below and learn more about MRTK and mixed reality.</span></span>

## <a name="about-the-author"></a><span data-ttu-id="815a3-180">À propos de l'auteur</span><span class="sxs-lookup"><span data-stu-id="815a3-180">About the author</span></span>

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><span data-ttu-id="815a3-181"><b>Dong Yoon Park</b></span><span class="sxs-lookup"><span data-stu-id="815a3-181"><b>Dong Yoon Park</b></span></span><br><span data-ttu-id="815a3-182">@Microsoft du concepteur UX</span><span class="sxs-lookup"><span data-stu-id="815a3-182">UX Designer @Microsoft</span></span></td>
</tr>
</table>

## <a name="see-also"></a><span data-ttu-id="815a3-183">Articles associés</span><span class="sxs-lookup"><span data-stu-id="815a3-183">See also</span></span>

* [<span data-ttu-id="815a3-184">Boîte à outils de réalité mixte-Unity (MRTK) GitHub</span><span class="sxs-lookup"><span data-stu-id="815a3-184">Mixed Reality Toolkit-Unity (MRTK) GitHub</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity)
* [<span data-ttu-id="815a3-185">Portail de documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-185">MRTK Documentation Portal</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)
* [<span data-ttu-id="815a3-186">Prise en main avec MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-186">Getting Started with MRTK</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
* [<span data-ttu-id="815a3-187">Indications sur le portage de HoloToolkit à MRTK</span><span class="sxs-lookup"><span data-stu-id="815a3-187">HoloToolkit to MRTK Porting Guideline</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html)
