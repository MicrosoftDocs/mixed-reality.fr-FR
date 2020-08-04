---
title: Tutoriels de démarrage - 7. Interaction avec les objets 3D
description: Ce cours montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: f02780a1b9421b814242727ce92311d62b5e3461
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376421"
---
# <a name="7-interacting-with-3d-objects"></a><span data-ttu-id="dc2dc-105">7. Interaction avec les objets 3D</span><span class="sxs-lookup"><span data-stu-id="dc2dc-105">7. Interacting with 3D objects</span></span>

<span data-ttu-id="dc2dc-106">Dans ce tutoriel, vous allez apprendre à activer la manipulation proche et lointaine des objets 3D et à limiter les types de manipulation autorisés.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-106">In this tutorial, you will learn how to enable near and far manipulation of 3D objects and limit the allowed types of manipulation.</span></span> <span data-ttu-id="dc2dc-107">Vous apprendrez également à ajouter des cadres englobants autour des objets 3D afin de faciliter le contrôle de la manipulation des objets.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-107">You will also learn how to add bounding boxes around 3D objects to make it easier to control the object manipulation.</span></span>

## <a name="objectives"></a><span data-ttu-id="dc2dc-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="dc2dc-108">Objectives</span></span>

* <span data-ttu-id="dc2dc-109">Apprendre à configurer des objets 3D afin de pouvoir interagir avec</span><span class="sxs-lookup"><span data-stu-id="dc2dc-109">Learn how to configure 3D objects so they can be interacted with</span></span>
* <span data-ttu-id="dc2dc-110">Apprendre à ajouter des cadres englobants à des objets 3D</span><span class="sxs-lookup"><span data-stu-id="dc2dc-110">Learn how to add bounding boxes to 3D objects</span></span>

## <a name="manipulating-3d-objects"></a><span data-ttu-id="dc2dc-111">Manipulation d’objets 3D</span><span class="sxs-lookup"><span data-stu-id="dc2dc-111">Manipulating 3D objects</span></span>

<span data-ttu-id="dc2dc-112">Dans cette section, vous allez ajouter la capacité à manipuler toutes les pièces du Rover que vous avez disposées sur la table durant le tutoriel [Positionnement des objets dans la scène](mr-learning-base-04.md).</span><span class="sxs-lookup"><span data-stu-id="dc2dc-112">In this section, you will add the ability to manipulate all the Rover parts you organized on the table during the [Positioning objects in the scene](mr-learning-base-04.md) tutorial.</span></span>

<span data-ttu-id="dc2dc-113">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-113">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="dc2dc-114">Ajouter le composant Object Manipulator (Script) à tous les objets de la pièce</span><span class="sxs-lookup"><span data-stu-id="dc2dc-114">Add the Object Manipulator (Script) component to all the part objects</span></span>
2. <span data-ttu-id="dc2dc-115">Ajouter le composant NearInteractionGrabbable à tous les objets de la pièce</span><span class="sxs-lookup"><span data-stu-id="dc2dc-115">Add the NearInteractionGrabbable component to all the part objects</span></span>
3. <span data-ttu-id="dc2dc-116">Configurer le composant Object Manipulator (Script)</span><span class="sxs-lookup"><span data-stu-id="dc2dc-116">Configure the Object Manipulator (Script) component</span></span>

> [!NOTE]
> <span data-ttu-id="dc2dc-117">Pour pouvoir **manipuler un objet**, celui-ci doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-117">To be able to **manipulate an object**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="dc2dc-118">Le composant **Collider**, par exemple un Box Collider</span><span class="sxs-lookup"><span data-stu-id="dc2dc-118">**Collider** component, for example, a Box Collider</span></span>
> * <span data-ttu-id="dc2dc-119">Le composant **Object Manipulator (Script)**</span><span class="sxs-lookup"><span data-stu-id="dc2dc-119">**Object Manipulator (Script)** component</span></span>
>
> <span data-ttu-id="dc2dc-120">Pour pouvoir **manipuler** et **saisir** un objet avec les mains suivies, celui-ci doit avoir les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-120">To be able to **manipulate** and **grab an object with tracked hands**, the object must have the following components:</span></span>
>
> * <span data-ttu-id="dc2dc-121">Le composant **Collider**, par exemple un Box Collider</span><span class="sxs-lookup"><span data-stu-id="dc2dc-121">**Collider** component, for example, a Box Collider</span></span>
> * <span data-ttu-id="dc2dc-122">Le composant **Object Manipulator (Script)**</span><span class="sxs-lookup"><span data-stu-id="dc2dc-122">**Object Manipulator (Script)** component</span></span>
> * <span data-ttu-id="dc2dc-123">Le composant **NearInteractionGrabbable**</span><span class="sxs-lookup"><span data-stu-id="dc2dc-123">**NearInteractionGrabbable** component</span></span>

<span data-ttu-id="dc2dc-124">De plus, vous configurerez le RoverExplorer afin de pouvoir placer les pièces du Rover sur le Rover pour en faire un assemblage complet.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-124">Additionally, you will configure the Rover Explorer so that you can place the rover parts on to the Rover to make it a complete rover assembly.</span></span>

<span data-ttu-id="dc2dc-125">Dans la fenêtre de hiérarchie, développez l’objet RoverExplorer > **RoverParts** et sélectionnez tous ses objets de pièces de Rover enfants et l’objet **RoverAssembly** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** (Ajouter un composant) pour ajouter les composants suivants à tous les objets sélectionnés :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-125">In the Hierarchy window, expand the RoverExplorer > **RoverParts** object and select all its child rover part objects and the **RoverAssembly** object, then in the Inspector window, use the **Add Component** button to add the following components to all the selected objects:</span></span>

* <span data-ttu-id="dc2dc-126">Le composant **Object Manipulator (Script)**</span><span class="sxs-lookup"><span data-stu-id="dc2dc-126">**Object Manipulator (Script)** component</span></span>
* <span data-ttu-id="dc2dc-127">Le composant **NearInteractionGrabbable**</span><span class="sxs-lookup"><span data-stu-id="dc2dc-127">**NearInteractionGrabbable** component</span></span>
* <span data-ttu-id="dc2dc-128">Le composant **Part Assembly Controller (Script)**</span><span class="sxs-lookup"><span data-stu-id="dc2dc-128">**Part Assembly Controller (Script)** component</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-1.png)

> [!TIP]
> <span data-ttu-id="dc2dc-130">Pour sélectionner plusieurs objets qui ne sont pas les uns à côté des autres, appuyez sur la touche Ctrl et maintenez-la enfoncée pendant que vous utilisez la souris pour sélectionner un objet.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-130">To select multiple objects that are not next to each other, press-and-hold the CTRL key while using the mouse to select any object.</span></span>

> [!NOTE]
> <span data-ttu-id="dc2dc-131">Dans le cadre de ce tutoriel, des colliders ont déjà été ajoutés aux pièces du Rover.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-131">For the purpose of this tutorial, colliders have already been added to the rover parts.</span></span> <span data-ttu-id="dc2dc-132">Pour plus d’informations sur les colliders, vous pouvez consulter la documentation <a href="https://docs.unity3d.com/Manual/CollidersOverview.html" target="_blank">Collider</a> d’Unity.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-132">To learn more about colliders, you can visit Unity's <a href="https://docs.unity3d.com/Manual/CollidersOverview.html" target="_blank">Collider</a> documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="dc2dc-133">Part Assembly Controller (Script) ne fait pas partie du MRTK, mais il a été inclus avec les ressources du tutoriel.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-133">The Part Assembly Controller (Script) is not part of the MRTK but was included with the tutorial assets.</span></span>

<span data-ttu-id="dc2dc-134">Toujours avec les objets de pièces de Rover et l’objet RoverAssembly sélectionnés, dans la fenêtre de l’inspecteur, configurez le composant **Object Manipulator (Script)** comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-134">With all the rover part objects and the RoverAssembly object still selected, in the Inspector window, configure the **Object Manipulator (Script)** component as follows:</span></span>

* <span data-ttu-id="dc2dc-135">Dans la liste déroulante **Two Handed Manipulation Type** (Type de manipulation à deux mains), décochez Scale (Mise à l’échelle) afin que seuls **Move** (Déplacer) et **Rotate** (Faire pivoter) soient activés.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-135">From the **Two Handed Manipulation Type** dropdown, uncheck the Scale, so only **Move** and **Rotate** is enabled</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-2.png)

> [!NOTE]
> <span data-ttu-id="dc2dc-137">À ce stade, vous avez activé la manipulation d’objet pour tous les objets de pièces de Rover et l’objet RoverAssembly.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-137">At this point, you have enabled object manipulation for all the rover part objects and the RoverAssembly object.</span></span>

<span data-ttu-id="dc2dc-138">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK** > **SDK** > **StandardAssets** > **Audio** pour localiser les clips audio :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-138">In the Project window, navigate to the **Assets** > **MRTK** > **SDK** > **StandardAssets** > **Audio** folder to locate the audio clips:</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-3.png)

<span data-ttu-id="dc2dc-140">Dans la fenêtre de hiérarchie, resélectionnez tous les **objets de pièces de Rover** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** pour ajouter le composant **Audio Sources** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-140">In the Hierarchy window, reselect all the **rover part objects**, then in the Inspector window, use the **Add Component** button to add the **Audio Sources** component and configure it as follows:</span></span>

* <span data-ttu-id="dc2dc-141">Affectez le clip audio **MRTK_Scale_Start** au champ **AudioClip**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-141">Assign the **MRTK_Scale_Start** audio clip to the **AudioClip** field</span></span>
* <span data-ttu-id="dc2dc-142">Décochez la case **Play On Awake** (Lire en cas d’activité)</span><span class="sxs-lookup"><span data-stu-id="dc2dc-142">Uncheck the **Play On Awake** checkbox</span></span>
* <span data-ttu-id="dc2dc-143">Affectez la valeur 1 à **Spatial Blend**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-143">Change **Spatial Blend** to 1</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-4.png)

<span data-ttu-id="dc2dc-145">Dans la fenêtre de hiérarchie, développez l’objet RoverAssembly > RoverModel_PlacementHints_XRay > **Parts_PlacementHints** pour révéler tous les objets d’indicateur de placement, puis sélectionnez la première pièce de Rover, RoverParts > **Camera_Part**, et configurez le composant **Part Assembly Controller (Script)** comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-145">In the Hierarchy window, expand the RoverAssembly > RoverModel_PlacementHints_XRay > **Parts_PlacementHints** object to reveal all of the placement hint objects, then select the first rover part, RoverParts > **Camera_Part**, and configure the **Part Assembly Controller (Script)** component as follows:</span></span>

* <span data-ttu-id="dc2dc-146">Assignez l’objet **Camera_PlacementHint** au champ **Location To Place** (Emplacement).</span><span class="sxs-lookup"><span data-stu-id="dc2dc-146">Assign the **Camera_PlacementHint** object to the **Location To Place** field</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-5.png)

<span data-ttu-id="dc2dc-148">**Répétez** cette étape pour chacun des objets de pièces de Rover restants et l’objet RoverAssembly afin de configurer le composant **Part Assembly Controller (Script)** comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-148">**Repeat** this step for each of the remaining rover part objects and the RoverAssembly object to configure the **Part Assembly Controller (Script)** component as follows:</span></span>

* <span data-ttu-id="dc2dc-149">Pour **Generator_Part**, assignez l’objet **Generator_PlacementHint** au champ **Location To Place**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-149">For the **Generator_Part**, assign the **Generator_PlacementHint** object to the **Location To Place** field</span></span>
* <span data-ttu-id="dc2dc-150">Pour **Lights_Part**, assignez l’objet **Lights_PlacementHint** au champ **Location To Place**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-150">For the **Lights_Part**, assign the **Lights_PlacementHint** object to the **Location To Place** field</span></span>
* <span data-ttu-id="dc2dc-151">Pour **UHFAntenna_Part**, assignez l’objet **UHFAntenna_PlacementHint** au champ **Location To Place**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-151">For the **UHFAntenna_Part**, assign the **UHFAntenna_PlacementHint** object to the **Location To Place** field</span></span>
* <span data-ttu-id="dc2dc-152">Pour **Spectrometer_Part**, assignez l’objet **Spectrometer_PlacementHint** au champ **Location To Place**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-152">For the **Spectrometer_Part**, assign the **Spectrometer_PlacementHint** object to the **Location To Place** field</span></span>
* <span data-ttu-id="dc2dc-153">Pour **RoverAssembly**, assignez l’objet lui-même (c’est-à-dire le même objet **RoverAssembly**), au champ **Location To Place**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-153">For the **RoverAssembly**, assign the object itself, i.e. the same **RoverAssembly** object, to the **Location To Place** field</span></span>

<span data-ttu-id="dc2dc-154">Dans la fenêtre de hiérarchie, sélectionnez l’objet de bouton RoverExplorer > Buttons > **Reset** puis, dans la fenêtre de l’inspecteur, configurez l’événement **OnClick ()** comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-154">In the Hierarchy window, select the RoverExplorer > Buttons > **Reset** button object, then in the Inspector window, configure the Interactable **OnClick ()** event as follows:</span></span>

* <span data-ttu-id="dc2dc-155">Assignez l’objet **RoverAssembly** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="dc2dc-155">Assign the **RoverAssembly** object to the **None (Object)** field</span></span>
* <span data-ttu-id="dc2dc-156">Dans la liste déroulante **No Function**, sélectionnez **PartAssemblyController** > **ResetPlacement ()** pour définir cette fonction en tant qu’action à exécuter lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-156">From the **No Function** dropdown, select **PartAssemblyController** > **ResetPlacement ()** to set this function as the action to be executed when the event is triggered</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-6.png)

<span data-ttu-id="dc2dc-158">Si vous basculez maintenant en mode Game, vous pouvez utiliser l’interaction proche ou lointaine pour placer les pièces sur le Rover.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-158">If you now enter Game mode, you can use near or far interaction to place the rover parts on to the Rover.</span></span> <span data-ttu-id="dc2dc-159">Une fois que la pièce est proche de l’indicateur de placement correspondant, elle s’imbrique en place et devient partie intégrante du Rover.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-159">Once the part is close to the corresponding placement hint, it will snap into place and become part of the Rover.</span></span> <span data-ttu-id="dc2dc-160">Pour réinitialiser les placements, vous pouvez appuyer sur le bouton Reset :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-160">To reset the placements, you can press the Reset button:</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-7.png)

<span data-ttu-id="dc2dc-162">Pour en savoir plus sur le composant Object Manipulator et ses propriétés associées, vous pouvez consulter le guide [Object Manipulator](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectManipulator.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="dc2dc-162">To learn more about the Object Manipulator component and its associated properties, you can visit the [Object Manipulator](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectManipulator.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="adding-bounding-boxes"></a><span data-ttu-id="dc2dc-163">Ajout de cadres englobants</span><span class="sxs-lookup"><span data-stu-id="dc2dc-163">Adding bounding boxes</span></span>

<span data-ttu-id="dc2dc-164">Les cadres englobants facilitent et rendent plus intuitive la manipulation d’objets avec une main pour l’interaction proche et de loin en fournissant des poignées qui peuvent être utilisées pour la mise à l’échelle et la rotation.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-164">Bounding boxes make it easier and more intuitive to manipulate objects with one hand for both near and far interaction by providing handles that can be used for scaling and rotating.</span></span>

<span data-ttu-id="dc2dc-165">Dans cet exemple, vous allez ajouter un cadre englobant à l’objet RoverExplorer afin de pouvoir effectuer facilement un déplacement, une rotation et une mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-165">In this example, you will add a bounding box to the RoverExplorer object so the whole experience can easily be moved, rotated, and scaled.</span></span> <span data-ttu-id="dc2dc-166">Vous allez également configurer le menu afin de pouvoir activer ou désactiver le cadre englobant.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-166">Additionally, you will configure the Menu so you can turn the Bounding Box on and off.</span></span>

<span data-ttu-id="dc2dc-167">Dans la fenêtre de hiérarchie, sélectionnez l’objet **RoverExplorer** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** pour ajouter les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-167">In the Hierarchy window, select the **RoverExplorer** object, then in the Inspector window, use the **Add Component** button to add the following components:</span></span>

* <span data-ttu-id="dc2dc-168">Le composant **BoundingBox**</span><span class="sxs-lookup"><span data-stu-id="dc2dc-168">**BoundingBox** component</span></span>
* <span data-ttu-id="dc2dc-169">Le composant **Object Manipulator (Script)**</span><span class="sxs-lookup"><span data-stu-id="dc2dc-169">**Object Manipulator (Script)** component</span></span>

<span data-ttu-id="dc2dc-170">Ensuite, **décochez** la case à côté des deux composants afin qu’ils soient **désactivés** par défaut :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-170">Then **uncheck** the checkbox next to both components to make them **disabled** by default:</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section2-step1-1.png)

> [!NOTE]
> <span data-ttu-id="dc2dc-172">La visualisation des cadres englobants est créée au moment de l’exécution, et n’est donc pas visible avant l’entrée en mode Game.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-172">The Bounding Box visualization is created at runtime and, therefore, not visible before you enter Game mode.</span></span>

> [!NOTE]
> <span data-ttu-id="dc2dc-173">Le composant BoundingBox ajoutera automatiquement le composant NearInteractionGrabbable au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-173">The BoundingBox component will automatically add the NearInteractionGrabbable component at runtime.</span></span> <span data-ttu-id="dc2dc-174">Par conséquent, nous n’avons pas besoin d’ajouter ce composant pour saisir les objets englobés avec les mouvements captés des mains.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-174">Therefore, we do not need to add this component to grab the enclosed objects with tracked hands.</span></span>

<span data-ttu-id="dc2dc-175">Dans la fenêtre de hiérarchie, développez l’objet Menu > **ButtonCollection** pour afficher les quatre boutons et renommez le troisième bouton **BoundingBox_Enable** puis, dans la fenêtre de l’inspecteur, configurez le composant **Button Config Helper (Script)** comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-175">In the Hierarchy window, expand the Menu > **ButtonCollection** object to reveal the four buttons and rename the third button to **BoundingBox_Enable**, then in the Inspector window, configure the **Button Config Helper (Script)** component as follows:</span></span>

* <span data-ttu-id="dc2dc-176">Affectez la valeur **Enable** à **Main Label Text** (Texte de l'étiquette principale).</span><span class="sxs-lookup"><span data-stu-id="dc2dc-176">Change the **Main Label Text** to **Enable**</span></span>
* <span data-ttu-id="dc2dc-177">Assignez l’objet **RoverExplorer** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="dc2dc-177">Assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="dc2dc-178">Dans la liste déroulante **No Function**, sélectionnez **BoundingBox** > **bool Enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-178">From the **No Function** dropdown, select **BoundingBox** > **bool Enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="dc2dc-179">Vérifiez que la case de l’argument est **cochée**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-179">Verify that the argument checkbox is **checked**</span></span>
* <span data-ttu-id="dc2dc-180">Cliquez sur la petite icône **+** pour ajouter un autre événement.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-180">Click the small **+** icon to add another event</span></span>
* <span data-ttu-id="dc2dc-181">Assignez l’objet **RoverExplorer** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="dc2dc-181">Assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="dc2dc-182">Dans la liste déroulante **No Function**, sélectionnez **ObjectManipulator** > **bool Enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-182">From the **No Function** dropdown, select **ObjectManipulator** > **bool Enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="dc2dc-183">Vérifiez que la case de l’argument est **cochée**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-183">Verify that the argument checkbox is **checked**</span></span>
* <span data-ttu-id="dc2dc-184">Conservez « cube avec cadre englobant » comme **icône**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-184">Leave the **Icon** as the 'cube with bounding box' icon</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section2-step1-2.png)

<span data-ttu-id="dc2dc-186">Renommez **BoundingBox_Disable** les quatrième et dernier bouton puis, dans la fenêtre de l’inspecteur, configurez le composant **Button Config Helper (Script)** comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-186">Rename the forth and last button to **BoundingBox_Disable**, then in the Inspector window, configure the **Button Config Helper (Script)** component as follows:</span></span>

* <span data-ttu-id="dc2dc-187">Affectez la valeur **Disable** à **Main Label Text**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-187">Change the **Main Label Text** to **Disable**</span></span>
* <span data-ttu-id="dc2dc-188">Assignez l’objet **RoverExplorer** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="dc2dc-188">Assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="dc2dc-189">Dans la liste déroulante **No Function**, sélectionnez **BoundingBox** > **bool Enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-189">From the **No Function** dropdown, select **BoundingBox** > **bool Enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="dc2dc-190">Vérifiez que la case de l’argument est **décochée**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-190">Verify that the argument checkbox is **unchecked**</span></span>
* <span data-ttu-id="dc2dc-191">Cliquez sur la petite icône **+** pour ajouter un autre événement.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-191">Click the small **+** icon to add another event</span></span>
* <span data-ttu-id="dc2dc-192">Assignez l’objet **RoverExplorer** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="dc2dc-192">Assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="dc2dc-193">Dans la liste déroulante **No Function**, sélectionnez **ObjectManipulator** > **bool Enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-193">From the **No Function** dropdown, select **ObjectManipulator** > **bool Enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="dc2dc-194">Vérifiez que la case de l’argument est **décochée**.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-194">Verify that the argument checkbox is **unchecked**</span></span>
* <span data-ttu-id="dc2dc-195">Remplacez l’**icône** par « cube avec cadre englobant ».</span><span class="sxs-lookup"><span data-stu-id="dc2dc-195">Change the **Icon** to the 'cube with bounding box" icon</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section2-step1-3.png)

<span data-ttu-id="dc2dc-197">Si vous basculez maintenant en mode Game et que vous activez le cadre englobant en cliquant sur le bouton Enable, vous pouvez utiliser l’interaction proche ou lointaine pour déplacer, faire pivoter et mettre à l’échelle le cadre englobant, et utiliser le bouton Disable pour désactiver le cadre englobant :</span><span class="sxs-lookup"><span data-stu-id="dc2dc-197">If you now enter Game mode and enable the Bounding Box by clicking the Enable button, you can use near or far interaction to move, rotate, and scale the Bounding Box, and use the Disable button to disable the Bounding Box again:</span></span>

![mr-learning-base](images/mr-learning-base/base-07-section2-step1-4.png)

<span data-ttu-id="dc2dc-199">Pour plus d’informations sur le composant Bounding Box et ses propriétés associées, vous pouvez consulter le guide [Bounding Box](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="dc2dc-199">To learn more about the Bounding Box component and its associated properties, you can visit the [Bounding box](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="congratulations"></a><span data-ttu-id="dc2dc-200">Félicitations</span><span class="sxs-lookup"><span data-stu-id="dc2dc-200">Congratulations</span></span>

<span data-ttu-id="dc2dc-201">Dans ce tutoriel, vous avez appris à activer la manipulation proche et lointaine pour les objets 3D et comment limiter les types de manipulation autorisés.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-201">In this tutorial, you learned how to enable near and far manipulation for 3D objects and how to limit the allowed types of manipulation.</span></span> <span data-ttu-id="dc2dc-202">Vous avez également appris à ajouter des cadres englobants autour des objets 3D afin de faciliter le contrôle de la manipulation des objets.</span><span class="sxs-lookup"><span data-stu-id="dc2dc-202">You also learned how to add bounding boxes around 3D objects to make it easier to control the object manipulation.</span></span>

[<span data-ttu-id="dc2dc-203">Tutoriel suivant : 8. Utilisation du suivi oculaire</span><span class="sxs-lookup"><span data-stu-id="dc2dc-203">Next Tutorial: 8. Using eye-tracking</span></span>](mr-learning-base-08.md)
