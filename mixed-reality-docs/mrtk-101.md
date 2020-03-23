---
title: MRTK 101 - Guide pratique pour utiliser Mixed Reality Toolkit avec Unity pour les interactions de base (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)
description: Guide pratique pour utiliser Mixed Reality Toolkit avec Unity pour les interactions de base (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)
author: cre8ivepark
ms.author: dongpark
ms.date: 08/27/2019
ms.topic: article
keywords: HoloLens, MRTK, Mixed Reality Toolkit, Windows Mixed Reality, conception, exemple d’application, contrôles
ms.localizationpriority: high
ms.openlocfilehash: 4564e7a0c6a717452effacae2587461fe283cf0b
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79028311"
---
# <a name="mrtk-101-how-to-use-mixed-reality-toolkit-unity-for-basic-interactions-hololens-2-hololens-windows-mixed-reality-openvr"></a><span data-ttu-id="a113d-104">MRTK 101 : Guide pratique pour utiliser Mixed Reality Toolkit avec Unity pour les interactions de base (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)</span><span class="sxs-lookup"><span data-stu-id="a113d-104">MRTK 101: How to use Mixed Reality Toolkit Unity for Basic Interactions (HoloLens 2, HoloLens, Windows Mixed Reality, Open VR)</span></span>

![MRTK](images/MRTK101/MRTK101Cover.png)

<span data-ttu-id="a113d-106">Découvrez comment utiliser MRTK pour obtenir certains des modèles d’interaction les plus largement utilisés dans le domaine de la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="a113d-106">Learn about how to use MRTK to achieve some of the most widely used common interaction patterns in mixed reality.</span></span>

- <span data-ttu-id="a113d-107">Comment simuler des interactions d’entrée dans l’éditeur Unity ?</span><span class="sxs-lookup"><span data-stu-id="a113d-107">How to simulate input interactions in Unity editor?</span></span>
- <span data-ttu-id="a113d-108">Comment saisir et déplacer un objet ?</span><span class="sxs-lookup"><span data-stu-id="a113d-108">How to grab and move an object?</span></span>
- <span data-ttu-id="a113d-109">Comment redimensionner un objet ?</span><span class="sxs-lookup"><span data-stu-id="a113d-109">How to resize an object?</span></span>
- <span data-ttu-id="a113d-110">Comment déplacer ou faire pivoter un objet avec précision ?</span><span class="sxs-lookup"><span data-stu-id="a113d-110">How to move or rotate an object with precision?</span></span>
- <span data-ttu-id="a113d-111">Comment faire en sorte qu’un objet réponde à des événements d’entrée ?</span><span class="sxs-lookup"><span data-stu-id="a113d-111">How to make an object respond to input events?</span></span>
- <span data-ttu-id="a113d-112">Comment ajouter un retour visuel ?</span><span class="sxs-lookup"><span data-stu-id="a113d-112">How to add visual feedback?</span></span>
- <span data-ttu-id="a113d-113">Comment ajouter un retour audio ?</span><span class="sxs-lookup"><span data-stu-id="a113d-113">How to add audio feedback?</span></span>
- <span data-ttu-id="a113d-114">Comment utiliser des préfabriqués de bouton de style HoloLens 2 ?</span><span class="sxs-lookup"><span data-stu-id="a113d-114">How to use HoloLens 2 style button prefabs?</span></span>
- <span data-ttu-id="a113d-115">Comment faire en sorte qu’un objet vous suive ?</span><span class="sxs-lookup"><span data-stu-id="a113d-115">How to make an object follow you?</span></span>
- <span data-ttu-id="a113d-116">Comment faire en sorte qu’un objet se mette en face de vous ?</span><span class="sxs-lookup"><span data-stu-id="a113d-116">How to make an object face you?</span></span>

## <a name="how-to-simulate-input-interactions-in-unityeditor"></a><span data-ttu-id="a113d-117">Comment simuler des interactions d’entrée dans l’éditeur Unity ?</span><span class="sxs-lookup"><span data-stu-id="a113d-117">How to simulate input interactions in Unity editor?</span></span>
<span data-ttu-id="a113d-118">MRTK prend en charge la simulation d’une entrée dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="a113d-118">MRTK supports in-editor input simulation.</span></span> <span data-ttu-id="a113d-119">Exécutez simplement votre scène en cliquant sur le bouton de lecture dans Unity.</span><span class="sxs-lookup"><span data-stu-id="a113d-119">Simply run your scene by clicking Unity's play button.</span></span> <span data-ttu-id="a113d-120">Utilisez ces touches pour simuler une entrée.</span><span class="sxs-lookup"><span data-stu-id="a113d-120">Use these keys to simulate input.</span></span>
<span data-ttu-id="a113d-121">Appuyez sur les touches W, A, S, D pour déplacer la caméra.</span><span class="sxs-lookup"><span data-stu-id="a113d-121">Press W, A, S, D keys to move the camera.</span></span>
<span data-ttu-id="a113d-122">Maintenez le bouton droit de la souris enfoncé et déplacez la souris pour regarder autour de vous.</span><span class="sxs-lookup"><span data-stu-id="a113d-122">Hold the right mouse button and move the mouse to look around.</span></span>
<span data-ttu-id="a113d-123">Pour faire apparaître les mains simulées, appuyez sur la barre d’espace (avec la main droite) ou sur la touche Maj gauche (avec la main gauche). Pour garder les mains simulées dans la vue, appuyez sur la touche T ou Y. Pour faire pivoter les mains simulées, appuyez sur Q ou E (horizontal)/R ou F (vertical).</span><span class="sxs-lookup"><span data-stu-id="a113d-123">To bring up the simulated hands, press Space bar(Right hand) or left Shift key(Left hand) To keep simulated hands in the view, press T or Y key To rotate simulated hands, press Q or E(horizontal) / R or F(vertical)</span></span>

- [<span data-ttu-id="a113d-124">En savoir plus sur la simulation d’entrée dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-124">Learn more about Input Simulation in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/InputSimulation/InputSimulationService.html)


## <a name="how-to-grab-and-move-anobject"></a><span data-ttu-id="a113d-125">Comment saisir et déplacer un objet ?</span><span class="sxs-lookup"><span data-stu-id="a113d-125">How to grab and move an object?</span></span>
<span data-ttu-id="a113d-126">Pour rendre un objet saisissable, affectez ces deux scripts : ManipulationHandler.cs et NearInteractionGrabbable.cs (pour une entrée par saisie directe avec de suivi de la main articulée). ManipulationHandler prend à la fois en charge les interactions proches et éloignées.</span><span class="sxs-lookup"><span data-stu-id="a113d-126">To make an object grabbable, assign these two scripts: ManipulationHandler.cs and NearInteractionGrabbable.cs(for direct grab with articulated hand tracking input) ManipulationHandler supports both near and far interactions.</span></span> <span data-ttu-id="a113d-127">Avec Hololens 2, vous pouvez saisir et déplacer un objet avec une entrée par suivi de la main articulée (interaction proche), avec un rayon émanant de la main (interaction éloignée), avec le faisceau du contrôleur de mouvement (interaction éloignée), avec le curseur oculaire HoloLens et le clic aérien (interaction éloignée).</span><span class="sxs-lookup"><span data-stu-id="a113d-127">You can grab and move an object with HoloLens 2's articulated hand tracking input(near), hand ray(far), motion controller's beam(far), HoloLens gaze cursor & air-tap(far).</span></span>

<img alt="NearInteractionGrabbable and ManipulationHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_ManipulationHandler.png">

<img alt="NearInteractionGrabbable and ManipulationHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_GrabMove.gif">


## <a name="how-to-resize-anobject"></a><span data-ttu-id="a113d-128">Comment redimensionner un objet ?</span><span class="sxs-lookup"><span data-stu-id="a113d-128">How to resize an object?</span></span>
<span data-ttu-id="a113d-129">ManipulationHandler.cs prend en charge la rotation/la mise à l’échelle à deux mains.</span><span class="sxs-lookup"><span data-stu-id="a113d-129">ManipulationHandler.cs supports two-handed scale/rotation.</span></span> <span data-ttu-id="a113d-130">Cela fonctionne avec divers types d’entrée : suivi de la main articulée avec HoloLens 2, pointage du regard + mouvement avec HoloLens 1 et contrôleur de mouvement du casque immersif de Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="a113d-130">This works with various input types such as HoloLens 2's articulated hand input, HoloLens 1's gaze + gesture input, and Windows Mixed Reality immersive headset's motion controller input.</span></span>

- [<span data-ttu-id="a113d-131">En savoir plus sur le gestionnaire de manipulation dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-131">Learn more about Manipulation Handler in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html)

<img alt="NearInteractionGrabbable and ManipulationHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_ManipulationHandler.gif">

## <a name="how-to-move-or-rotate-an-object-with-precision"></a><span data-ttu-id="a113d-132">Comment déplacer ou faire pivoter un objet avec précision ?</span><span class="sxs-lookup"><span data-stu-id="a113d-132">How to move or rotate an object with precision?</span></span>
<span data-ttu-id="a113d-133">Affectez BoundingBox.cs à un objet pour utiliser un cadre englobant qui constitue l’interface pour la mise à l’échelle et la rotation d’un objet.</span><span class="sxs-lookup"><span data-stu-id="a113d-133">Assign BoundingBox.cs to an object to use Bounding Box which is the interface for scaling and rotating an object.</span></span> <span data-ttu-id="a113d-134">Par défaut, il présente les poignées et les lignes bleues de style HoloLens 1.</span><span class="sxs-lookup"><span data-stu-id="a113d-134">By default, it shows HoloLens 1 style blue handles and wires.</span></span> <span data-ttu-id="a113d-135">Pour utiliser des poignées animées de proximité de style HoloLens 2, vous devez affecter des préfabriqués et des matériaux.</span><span class="sxs-lookup"><span data-stu-id="a113d-135">To use HoloLens 2 style proximity-based animated handles, you need to assign prefabs and materials.</span></span> <span data-ttu-id="a113d-136">Pour plus d’informations sur la configuration, reportez-vous à la [ documentation sur le cadre englobant](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) et à la scène BoundingBoxExamples.unity.</span><span class="sxs-lookup"><span data-stu-id="a113d-136">Please refer to [Bounding Box documentation](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) and the BoundingBoxExamples.unity scene for the configuration details.</span></span>

<img alt="BoundingBox.cs assigned to an object" width="800" src="images/MRTK101/MRTK_BoundingBox.png">

<img alt="BoundingBox.cs assigned to an object" width="800" src="images/MRTK101/MRTK_BoundingBox.gif">


- [<span data-ttu-id="a113d-137">En savoir plus sur le cadre englobant dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-137">Learn more about Bounding Box in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html)

## <a name="how-to-make-an-object-respond-to-inputevents"></a><span data-ttu-id="a113d-138">Comment faire en sorte qu’un objet réponde à des événements d’entrée ?</span><span class="sxs-lookup"><span data-stu-id="a113d-138">How to make an object respond to input events?</span></span>
<span data-ttu-id="a113d-139">Affectez PointerHandler.cs à un objet.</span><span class="sxs-lookup"><span data-stu-id="a113d-139">Assign PointerHandler.cs to an object.</span></span> <span data-ttu-id="a113d-140">Dans l’inspecteur, vous allez pouvoir utiliser des événements OnPointerDown(), OnPointerUp(), OnPointerClicked(), OnPointerDragged(). Pour utiliser ces événements dans un script, implémentez IMixedRealityPointerHandler.</span><span class="sxs-lookup"><span data-stu-id="a113d-140">In the inspector, you will be able to use events OnPointerDown(), OnPointerUp(), OnPointerClicked(), OnPointerDragged() To use these events in a script, implement IMixedRealityPointerHandler.</span></span>

<img alt="PointerHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_PointerHandler.png">

- [<span data-ttu-id="a113d-141">En savoir plus sur le système d’entrée dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-141">Learn more about Input System in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html)

## <a name="how-to-add-visual-feedback"></a><span data-ttu-id="a113d-142">Comment ajouter un retour visuel ?</span><span class="sxs-lookup"><span data-stu-id="a113d-142">How to add visual feedback?</span></span>
<span data-ttu-id="a113d-143">Affectez Interactable.cs à un objet.</span><span class="sxs-lookup"><span data-stu-id="a113d-143">Assign Interactable.cs to an object.</span></span> <span data-ttu-id="a113d-144">Dans l’inspecteur, créez un thème.</span><span class="sxs-lookup"><span data-stu-id="a113d-144">In the inspector, create a new theme.</span></span> <span data-ttu-id="a113d-145">À l’aide des profils de thème d’Interactable, vous pouvez facilement ajouter un retour visuel à tous les états d’interaction d’entrée disponibles.</span><span class="sxs-lookup"><span data-stu-id="a113d-145">Using Interactable's theme profiles, you can easily add visual feedback to all available input interaction states.</span></span>

<img alt="PointerHandler.cs assigned to an object" width="800" src="images/MRTK101/MRTK_Interactable.png">

<img alt="Interactable" width="800" src="images/MRTK101/MRTK_Interactable.gif">


<span data-ttu-id="a113d-146">Interactable fournit divers types de thèmes, notamment le thème du nuanceur, qui vous permet de contrôler les propriétés du nuanceur par état d’interaction.</span><span class="sxs-lookup"><span data-stu-id="a113d-146">Interactable provides various types of themes including the shader theme which allows you to control properties of the shader per interaction state.</span></span>

- [<span data-ttu-id="a113d-147">En savoir plus sur Interactable dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-147">Learn more about Interactable in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Interactable.html)

<span data-ttu-id="a113d-148">Un autre module important pour le retour visuel est le nuanceur MRTK standard.</span><span class="sxs-lookup"><span data-stu-id="a113d-148">Another important building block for visual feedback is the MRTK Standard Shader.</span></span> <span data-ttu-id="a113d-149">Avec le nuanceur MRTK standard, vous pouvez facilement ajouter des effets de retour visuel comme une lumière de survol et une lumière de proximité.</span><span class="sxs-lookup"><span data-stu-id="a113d-149">With MRTK Standard Shader, you can easily add visual feedback effects such as hover light and proximity light.</span></span> <span data-ttu-id="a113d-150">Étant donné que le nuanceur MRTK standard effectue beaucoup moins de calcul que le nuanceur Unity standard, vous pouvez ainsi créer une expérience performante.</span><span class="sxs-lookup"><span data-stu-id="a113d-150">Since MRTK Standard shader performs significantly less computation than the Unity Standard shader, you can create a performant experience.</span></span>

<span data-ttu-id="a113d-151">Créez un matériau et sélectionnez le nuanceur « Mixed Reality Toolkit > Standard ».</span><span class="sxs-lookup"><span data-stu-id="a113d-151">Create a new material and select the Shader 'Mixed Reality Toolkit > Standard'.</span></span> <span data-ttu-id="a113d-152">Ou vous pouvez choisir l’un des matériaux existants qui utilisent le nuanceur MRTK standard.</span><span class="sxs-lookup"><span data-stu-id="a113d-152">Or you can pick one of the existing materials that use MRTK Standard Shader.</span></span>

<img alt="MRTK Standard Shader" width="400" src="images/MRTK101/MRTK_Shader0.png">
<br/><br/>
<img alt="MRTK Standard Shader" width="800" src="images/MRTK101/MRTK_Shader1.png">

<img alt="MRTK Standard Shader" width="800" src="images/MRTK101/MRTK_Shader.gif">


- [<span data-ttu-id="a113d-153">En savoir plus sur le nuanceur MRTK standard dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-153">Learn more about MRTK Standard Shader in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_MRTKStandardShader.html)

## <a name="how-to-add-audio-feedback"></a><span data-ttu-id="a113d-154">Comment ajouter un retour audio ?</span><span class="sxs-lookup"><span data-stu-id="a113d-154">How to add audio feedback?</span></span>
<span data-ttu-id="a113d-155">Ajoutez AudioSource à un objet.</span><span class="sxs-lookup"><span data-stu-id="a113d-155">Add AudioSource to an object.</span></span> <span data-ttu-id="a113d-156">Ensuite, dans les scripts qui exposent des événements d’entrée (par exemple, Interactable.cs ou PointerHandler.cs), affectez l’objet à l’événement et sélectionnez AudioSource.PlayOneShot().</span><span class="sxs-lookup"><span data-stu-id="a113d-156">Then, in the scripts that exposes input events(e.g. Interactable.cs or PointerHandler.cs), assign the object to the event and select AudioSource.PlayOneShot().</span></span> <span data-ttu-id="a113d-157">Vous pouvez utiliser vos clips audio ou en choisir un à partir des ressources audio de MRTK.</span><span class="sxs-lookup"><span data-stu-id="a113d-157">You can use your audio clips or choose one from MRTK's audio assets.</span></span>

<img alt="Audio Source assigned to an object. AudioSource.PlayOneShot configured in the Interactable's OnPress() and OnRelease() events." width="800" src="images/MRTK101/MRTK_Audio.png">

## <a name="how-to-use-hololens-2-style-buttonprefabs"></a><span data-ttu-id="a113d-158">Comment utiliser des préfabriqués de bouton de style HoloLens 2 ?</span><span class="sxs-lookup"><span data-stu-id="a113d-158">How to use HoloLens 2 style button prefabs?</span></span>
<span data-ttu-id="a113d-159">MRTK fournit divers types de boutons de style shell (système d’exploitation) HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="a113d-159">MRTK provides various types of HoloLens 2's shell(OS) style buttons.</span></span> <span data-ttu-id="a113d-160">Il propose des retours visuels sophistiqués, comme la lumière de proximité, le cadre de compression et un effet d’ondulation à la surface du bouton.</span><span class="sxs-lookup"><span data-stu-id="a113d-160">It provides sophisticated visual feedbacks such as proximity light, compressing box, and a ripple effect on the button surface.</span></span>

<img alt="Interactable" width="800" src="images/MRTK101/MRTK_Button.gif">

<span data-ttu-id="a113d-161">Il vous suffit de glisser-déposer l’un des préfabriqués de boutons sur lequel appuyer de style HoloLens 2 dans votre scène.</span><span class="sxs-lookup"><span data-stu-id="a113d-161">Simply drag and drop one of the HoloLens 2 style pressable button prefab into your scene.</span></span> <span data-ttu-id="a113d-162">Le préfabriqué utilise Interactable.cs, décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a113d-162">The prefab uses Interactable.cs which is introduced above.</span></span> <span data-ttu-id="a113d-163">Vous pouvez utiliser des événements exposés comme OnClick() dans Interactable pour déclencher des actions.</span><span class="sxs-lookup"><span data-stu-id="a113d-163">You can use exposed events such as OnClick() in the Interactable to trigger actions.</span></span>

<img alt="HoloLens 2 Button Prefab" width="800" src="images/MRTK101/MRTK_Button.png">

- [<span data-ttu-id="a113d-164">En savoir plus sur les préfabriqués de bouton dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-164">Learn more about Button prefabs in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Button.html)

## <a name="how-to-make-an-object-followyou"></a><span data-ttu-id="a113d-165">Comment faire en sorte qu’un objet vous suive ?</span><span class="sxs-lookup"><span data-stu-id="a113d-165">How to make an object follow you?</span></span>
<span data-ttu-id="a113d-166">Affectez le script RadialView.cs à un objet.</span><span class="sxs-lookup"><span data-stu-id="a113d-166">Assign RadialView.cs script to an object.</span></span> <span data-ttu-id="a113d-167">Il fait partie de la série de scripts Solver qui vous permet d’obtenir divers types de positionnement des objets dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="a113d-167">It is part of the Solver script series that allows you to achieve various types of object positioning in 3D space.</span></span> <span data-ttu-id="a113d-168">SolverHandler.cs est automatiquement ajouté.</span><span class="sxs-lookup"><span data-stu-id="a113d-168">SolverHandler.cs will be automatically added.</span></span>
<span data-ttu-id="a113d-169">Voici un exemple de configuration de RadialView pour obtenir un comportement de suivi tardif, à l’instar du menu Démarrer dans le shell HoloLens.</span><span class="sxs-lookup"><span data-stu-id="a113d-169">Below is an example of RadialView configuration to achieve 'lazy follow' tag-along behavior just like the Start menu in the HoloLens shell.</span></span> <span data-ttu-id="a113d-170">Vous pouvez spécifier la distance minimale/maximale et les degrés d’affichage minimaux/maximaux.</span><span class="sxs-lookup"><span data-stu-id="a113d-170">You can specify the minimum/maximum distance and minimum/maximum view degrees.</span></span> <span data-ttu-id="a113d-171">L’exemple ci-dessous montre le positionnement de l’objet dans une plage comprise entre 0,4 et 0,8 mètre à 15 °.</span><span class="sxs-lookup"><span data-stu-id="a113d-171">The example below shows positioning the object between 0.4m and 0.8m range within 15°.</span></span> <span data-ttu-id="a113d-172">Ajustez les valeurs de délai Lerp pour accélérer ou ralentir la mise à jour de la position.</span><span class="sxs-lookup"><span data-stu-id="a113d-172">Adjust Lerp Time values to make the positional update faster or slower.</span></span>

<img alt="MRTK Standard Shader" width="400" src="images/MRTK101/MRTK_SolverRadialView.png">

<img alt="Interactable" width="800" src="images/MRTK101/MRTK_RadialViewSolver.gif">

- [<span data-ttu-id="a113d-173">En savoir plus sur Solver dans la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-173">Learn more about Solvers in the MRTK documentation</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html)

## <a name="how-to-make-an-object-faceyou"></a><span data-ttu-id="a113d-174">Comment faire en sorte qu’un objet se mette en face de vous ?</span><span class="sxs-lookup"><span data-stu-id="a113d-174">How to make an object face you?</span></span>
<span data-ttu-id="a113d-175">Affectez le script Billboard.cs à un objet.</span><span class="sxs-lookup"><span data-stu-id="a113d-175">Assign Billboard.cs script to an object.</span></span> <span data-ttu-id="a113d-176">L’objet vous fera toujours face, quelle que soit votre position.</span><span class="sxs-lookup"><span data-stu-id="a113d-176">It will always face you, regardless of your position.</span></span> <span data-ttu-id="a113d-177">Vous pouvez spécifier l’option d’axe pivot.</span><span class="sxs-lookup"><span data-stu-id="a113d-177">You can specify the pivot axis option.</span></span>

<img alt="Billboard.cs script assigned to an object with Pivot Axis option Y" width="800" src="images/MRTK101/MRTK_Billboard.png">

<img alt="Billboard.cs script assigned to an object with Pivot Axis option Y" width="800" src="images/MRTK101/MRTK_Billboard.gif">


<span data-ttu-id="a113d-178">Vous êtes prêt à créer des expériences étonnantes pour la réalité mixte ?</span><span class="sxs-lookup"><span data-stu-id="a113d-178">Ready to create amazing experiences for mixed reality?</span></span> <span data-ttu-id="a113d-179">Consultez les pages ci-dessous pour en savoir plus sur MRTK et la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="a113d-179">Visit the pages below and learn more about MRTK and mixed reality.</span></span>

## <a name="about-the-author"></a><span data-ttu-id="a113d-180">À propos de l’auteur</span><span class="sxs-lookup"><span data-stu-id="a113d-180">About the author</span></span>

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><span data-ttu-id="a113d-181"><b>Dong Yoon Park</b></span><span class="sxs-lookup"><span data-stu-id="a113d-181"><b>Dong Yoon Park</b></span></span><br><span data-ttu-id="a113d-182">Concepteur d’expérience utilisateur @Microsoft</span><span class="sxs-lookup"><span data-stu-id="a113d-182">UX Designer @Microsoft</span></span></td>
</tr>
</table>

## <a name="see-also"></a><span data-ttu-id="a113d-183">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a113d-183">See also</span></span>

* [<span data-ttu-id="a113d-184">Mixed Reality Toolkit - Unity (MRTK) GitHub</span><span class="sxs-lookup"><span data-stu-id="a113d-184">Mixed Reality Toolkit-Unity (MRTK) GitHub</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity)
* [<span data-ttu-id="a113d-185">Portail de la documentation MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-185">MRTK Documentation Portal</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html)
* [<span data-ttu-id="a113d-186">Bien démarrer avec MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-186">Getting Started with MRTK</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)
* [<span data-ttu-id="a113d-187">Instructions de portage de HoloToolkit vers MRTK</span><span class="sxs-lookup"><span data-stu-id="a113d-187">HoloToolkit to MRTK Porting Guideline</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html)
