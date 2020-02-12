---
title: Didacticiels de mise en route-3. Création d’une interface utilisateur et configuration d’une réalité mixte Toolkit
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 067832a130f130ffbaa8d455007b8e77e1b13671
ms.sourcegitcommit: cc61f7ac08f9ac2f2f04e8525c3260ea073e04a7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77130531"
---
# <a name="3-creating-user-interface-and-configure-mixed-reality-toolkit"></a><span data-ttu-id="2bc60-105">3. création d’une interface utilisateur et configuration d’une réalité mixte Toolkit</span><span class="sxs-lookup"><span data-stu-id="2bc60-105">3. Creating user interface and configure Mixed Reality Toolkit</span></span>
<!-- TODO: Consider renaming to 'Configuring Mixed Reality Toolkit profiles and creating user interfaces' -->

<span data-ttu-id="2bc60-106">Dans le didacticiel précédent, vous avez appris certaines des possibilités offertes par le kit d’outils de réalité mixte (MRTK) en démarrant votre première application pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="2bc60-106">In the previous tutorial, you learned about some of the capabilities the Mixed Reality Toolkit (MRTK) has to offer by starting your first application for the HoloLens 2.</span></span> <span data-ttu-id="2bc60-107">Dans ce didacticiel, vous allez apprendre à créer et à organiser des boutons avec des panneaux de texte d’interface utilisateur et à utiliser l’interaction par défaut (Touch) pour interagir avec chaque bouton.</span><span class="sxs-lookup"><span data-stu-id="2bc60-107">In this tutorial you will learn how to create and organize buttons along with UI text panels, and use default interaction (touch) to interact with each button.</span></span> <span data-ttu-id="2bc60-108">Vous allez également découvrir comment ajouter des actions et des effets simples, comme changer la taille, la sonorité et la couleur des objets.</span><span class="sxs-lookup"><span data-stu-id="2bc60-108">You will also explore the addition of simple actions and effects, such as changing the size, sound and color of objects.</span></span> <span data-ttu-id="2bc60-109">Ce module présente les concepts de base de la modification des profils MRTK, en commençant par la désactivation de la visualisation de maillage de [mappage spatial](spatial-mapping.md) .</span><span class="sxs-lookup"><span data-stu-id="2bc60-109">This module will introduce basic concepts about modifying MRTK profiles, starting with turning off the [spatial mapping](spatial-mapping.md) mesh visualization.</span></span>

## <a name="objectives"></a><span data-ttu-id="2bc60-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="2bc60-110">Objectives</span></span>

* <span data-ttu-id="2bc60-111">Personnaliser et configurer des profils MRTK</span><span class="sxs-lookup"><span data-stu-id="2bc60-111">Customize and configure Mixed Reality Toolkit profiles</span></span>
* <span data-ttu-id="2bc60-112">Interagir avec des hologrammes à l’aide d’éléments d’interface utilisateur et de boutons</span><span class="sxs-lookup"><span data-stu-id="2bc60-112">Interact with holograms using UI elements and buttons</span></span>
* <span data-ttu-id="2bc60-113">Entrées et interactions de base pour le suivi de la main</span><span class="sxs-lookup"><span data-stu-id="2bc60-113">Basic hand-tracking input and interactions</span></span>

## <a name="how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option"></a><span data-ttu-id="2bc60-114">Comment configurer les profils de la boîte à outils de la réalité mixte (modifier l’option d’affichage de sensibilisation spatiale)</span><span class="sxs-lookup"><span data-stu-id="2bc60-114">How to configure the Mixed Reality Toolkit Profiles (Change Spatial Awareness Display Option)</span></span>
<!-- TODO: Consider renaming to 'How to customize the MRTK profiles' -->

<span data-ttu-id="2bc60-115">Dans cette section, vous allez apprendre à personnaliser et à configurer les profils MRTK par défaut.</span><span class="sxs-lookup"><span data-stu-id="2bc60-115">In this section, you will learn how to customize and configure the default MRTK profiles.</span></span>

<span data-ttu-id="2bc60-116">Cet exemple indique comment masquer le maillage de la sensibilisation spatiale en modifiant les paramètres de l’observateur de maillage spatial.</span><span class="sxs-lookup"><span data-stu-id="2bc60-116">This particular example will show you how to hide the spatial awareness mesh by changing the settings of the Spatial Mesh Observer.</span></span> <span data-ttu-id="2bc60-117">Toutefois, vous pouvez suivre ces mêmes principes pour personnaliser n’importe quel paramètre ou valeur dans les profils MRTK.</span><span class="sxs-lookup"><span data-stu-id="2bc60-117">However, you may follow these same principles to customize any setting or value in the MRTK profiles.</span></span>

<span data-ttu-id="2bc60-118">Les principales étapes à suivre pour masquer le maillage de la sensibilisation spatiale sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2bc60-118">The main steps you will take to hide the spatial awareness mesh are:</span></span>

1. <span data-ttu-id="2bc60-119">Cloner le profil de configuration par défaut</span><span class="sxs-lookup"><span data-stu-id="2bc60-119">Clone the default Configuration Profile</span></span>
2. <span data-ttu-id="2bc60-120">Activer le système de sensibilisation spatiale</span><span class="sxs-lookup"><span data-stu-id="2bc60-120">Enable the Spatial Awareness System</span></span>
3. <span data-ttu-id="2bc60-121">Cloner le profil système de sensibilisation spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="2bc60-121">Clone the default Spatial Awareness System Profile</span></span>
4. <span data-ttu-id="2bc60-122">Cloner le profil d’observateur de maillage de sensibilisation spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="2bc60-122">Clone the default Spatial Awareness Mesh Observer Profile</span></span>
5. <span data-ttu-id="2bc60-123">Modifier la visibilité du maillage de la sensibilisation spatiale</span><span class="sxs-lookup"><span data-stu-id="2bc60-123">Change the visibility of the spatial awareness mesh</span></span>

> [!NOTE]
> <span data-ttu-id="2bc60-124">Par défaut, les profils MRTK ne sont pas modifiables.</span><span class="sxs-lookup"><span data-stu-id="2bc60-124">By default, the MRTK profiles are not editable.</span></span> <span data-ttu-id="2bc60-125">Il s’agit des modèles de profil par défaut que vous devez cloner avant de pouvoir les modifier.</span><span class="sxs-lookup"><span data-stu-id="2bc60-125">These are default profile templates that you have to clone before they can be edited.</span></span> <span data-ttu-id="2bc60-126">Il existe plusieurs couches imbriquées de profils.</span><span class="sxs-lookup"><span data-stu-id="2bc60-126">There are several nested layers of profiles.</span></span> <span data-ttu-id="2bc60-127">Par conséquent, il est courant de cloner et de modifier plusieurs profils lors de la configuration d’un ou plusieurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="2bc60-127">Therefore, it is common to clone and edit several profiles when configuring one or more settings.</span></span>

### <a name="1-clone-the-default-configuration-profile"></a><span data-ttu-id="2bc60-128">1. cloner le profil de configuration par défaut</span><span class="sxs-lookup"><span data-stu-id="2bc60-128">1. Clone the default Configuration Profile</span></span>

> [!NOTE]
> <span data-ttu-id="2bc60-129">Le profil de configuration est le profil de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="2bc60-129">The Configuration Profile is the top level profile.</span></span> <span data-ttu-id="2bc60-130">Par conséquent, pour pouvoir modifier d’autres profils, vous devez d’abord cloner le profil de configuration.</span><span class="sxs-lookup"><span data-stu-id="2bc60-130">Consequently, to be able to edit any other profiles, you first have to clone the Configuration Profile.</span></span>

<span data-ttu-id="2bc60-131">Lorsque l’objet **MixedRealityToolkit** est sélectionné dans la fenêtre hiérarchie, dans la fenêtre Inspecteur, cliquez sur le bouton **Copier & personnaliser** pour ouvrir la fenêtre cloner le profil :</span><span class="sxs-lookup"><span data-stu-id="2bc60-131">With the **MixedRealityToolkit** object selected in the Hierarchy window, in the Inspector window, click the **Copy & Customize** button to open the Clone Profile window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-1.png)

<span data-ttu-id="2bc60-133">Dans la fenêtre cloner le profil, cliquez sur le bouton **cloner** pour créer une copie modifiable de l' **DefaultHololens2ConfigurationProfile**:</span><span class="sxs-lookup"><span data-stu-id="2bc60-133">In the Clone Profile window, click the **Clone** button to create an editable copy of the **DefaultHololens2ConfigurationProfile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-2.png)

<span data-ttu-id="2bc60-135">Le profil de configuration que vous venez de créer est maintenant affecté comme profil de configuration pour votre scène :</span><span class="sxs-lookup"><span data-stu-id="2bc60-135">The newly created Configuration Profile is now assigned as the Configuration Profile for your scene:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-3.png)

<span data-ttu-id="2bc60-137">Dans le menu Unity, sélectionnez **fichier** > **Enregistrer** pour enregistrer votre scène.</span><span class="sxs-lookup"><span data-stu-id="2bc60-137">In the Unity menu, select **File** > **Save** to save your scene.</span></span>

> [!TIP]
> <span data-ttu-id="2bc60-138">N’oubliez pas d’enregistrer votre travail tout au long du didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2bc60-138">Remember to save your work throughout the tutorial.</span></span>

### <a name="2-enable-the-spatial-awareness-system"></a><span data-ttu-id="2bc60-139">2. activer le système de sensibilisation spatiale</span><span class="sxs-lookup"><span data-stu-id="2bc60-139">2. Enable the Spatial Awareness System</span></span>

<span data-ttu-id="2bc60-140">Lorsque l’objet **MixedRealityToolkit** est toujours sélectionné dans la fenêtre hiérarchie, dans la fenêtre Inspecteur, sélectionnez l’onglet **détection spatiale** , puis activez la case à cocher **activer le système de sensibilisation spatiale** :</span><span class="sxs-lookup"><span data-stu-id="2bc60-140">With the **MixedRealityToolkit** object still selected in the Hierarchy window, in the Inspector window, select the **Spatial Awareness** tab, and then check the **Enable Spatial Awareness System** checkbox:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step2-1.png)

### <a name="3-clone-the-default-spatial-awareness-system-profile"></a><span data-ttu-id="2bc60-142">3. cloner le profil système de sensibilisation spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="2bc60-142">3. Clone the default Spatial Awareness System Profile</span></span>

<span data-ttu-id="2bc60-143">Dans l’onglet **sensibilisation spatiale** , cliquez sur le bouton **cloner** pour ouvrir la fenêtre cloner le profil :</span><span class="sxs-lookup"><span data-stu-id="2bc60-143">In the **Spatial Awareness** tab, click the **Clone** button to open the Clone Profile window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-1.png)

<span data-ttu-id="2bc60-145">Dans la fenêtre cloner le profil, cliquez sur le bouton **cloner** pour créer une copie modifiable de l' **DefaultMixedRealitySpatialAwarenessSystemProfile**:</span><span class="sxs-lookup"><span data-stu-id="2bc60-145">In the Clone Profile window, click the **Clone** button to create an editable copy of the **DefaultMixedRealitySpatialAwarenessSystemProfile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-2.png)

<span data-ttu-id="2bc60-147">Le profil de système de sensibilisation spatiale nouvellement créé est maintenant automatiquement affecté à votre profil de configuration :</span><span class="sxs-lookup"><span data-stu-id="2bc60-147">The newly created Spatial Awareness System Profile is now automatically assigned to your Configuration Profile:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-3.png)

### <a name="4-clone-the-default-spatial-awareness-mesh-observer-profile"></a><span data-ttu-id="2bc60-149">4. clonez le profil d’observateur de maillage de détection spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="2bc60-149">4. Clone the default Spatial Awareness Mesh Observer Profile</span></span>

<span data-ttu-id="2bc60-150">Avec l’onglet **sensibilisation spatiale** toujours sélectionné, développez la section **Observateur de maillage spatial Windows Mixed Reality** , puis cliquez sur le bouton **cloner** pour ouvrir la fenêtre cloner le profil :</span><span class="sxs-lookup"><span data-stu-id="2bc60-150">With the **Spatial Awareness** tab still selected, expand the **Windows Mixed Reality Spatial Mesh Observer** section, then click the **Clone** button to open the Clone Profile window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-1.png)

<span data-ttu-id="2bc60-152">Dans la fenêtre cloner le profil, cliquez sur le bouton **cloner** pour créer une copie modifiable de l' **DefaultMixedRealitySpatialAwarenessMeshObserverProfile**:</span><span class="sxs-lookup"><span data-stu-id="2bc60-152">In the Clone Profile window, click the **Clone** button to create an editable copy of the **DefaultMixedRealitySpatialAwarenessMeshObserverProfile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-2.png)

<span data-ttu-id="2bc60-154">Le profil d’observateur de maillage de sensibilisation spatiale nouvellement créé est maintenant automatiquement affecté à votre profil système de sensibilisation spatiale :</span><span class="sxs-lookup"><span data-stu-id="2bc60-154">The newly created Spatial Awareness Mesh Observer Profile is now automatically assigned to your Spatial Awareness System Profile:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-3.png)

### <a name="5-change-the-visibility-of-the-spatial-awareness-mesh"></a><span data-ttu-id="2bc60-156">5. modifier la visibilité du maillage de la sensibilisation spatiale</span><span class="sxs-lookup"><span data-stu-id="2bc60-156">5. Change the visibility of the spatial awareness mesh</span></span>

<span data-ttu-id="2bc60-157">Dans les **paramètres d’observateur de maillage spatial**, définissez l' **option d’affichage** sur **occlusion** pour rendre le maillage de mappage spatial invisible alors qu’il est toujours fonctionnel :</span><span class="sxs-lookup"><span data-stu-id="2bc60-157">In the **Spatial Mesh Observer Settings**, change the **Display Option** to **Occlusion** to make the spatial mapping mesh invisible while still being functional:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step5-1.png)

> [!NOTE]
> <span data-ttu-id="2bc60-159">Bien que le maillage de mappage spatial ne soit pas visible, il est toujours présent et fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="2bc60-159">Although the spatial mapping mesh is not visible, it is still present and functional.</span></span> <span data-ttu-id="2bc60-160">Par exemple, tous les hologrammes derrière le maillage de mappage spatial, tels qu’un hologramme derrière un mur physique, ne sont pas visibles.</span><span class="sxs-lookup"><span data-stu-id="2bc60-160">For example, any holograms behind the spatial mapping mesh, such as a hologram behind a physical wall, will not be visible.</span></span>

<span data-ttu-id="2bc60-161">Vous venez de découvrir comment modifier un paramètre dans le profil MRTK.</span><span class="sxs-lookup"><span data-stu-id="2bc60-161">You just learned how to modify a setting in the MRTK profile.</span></span> <span data-ttu-id="2bc60-162">Comme vous pouvez le voir, pour personnaliser les paramètres MRTK, vous devez d’abord créer des copies des profils par défaut.</span><span class="sxs-lookup"><span data-stu-id="2bc60-162">As you can see, in order to customize the MRTK settings, you first need to create copies of the default profiles.</span></span> <span data-ttu-id="2bc60-163">Étant donné que les profils par défaut ne sont pas modifiables, vous les aurez toujours comme référence si vous souhaitez rétablir les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="2bc60-163">Because the default profiles are not editable, you will always have them as reference if you want revert back to the default settings.</span></span> <span data-ttu-id="2bc60-164">Pour en savoir plus sur les profils MRTK et leur architecture, vous pouvez consulter le [Guide de configuration du profil du Toolkit de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) dans le portail de [documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="2bc60-164">To learn more about MRTK profiles and their architecture, you can visit the [Mixed Reality Toolkit profile configuration guide](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="hand-tracking-gestures-and-interactable-buttons"></a><span data-ttu-id="2bc60-165">Mouvements de suivi de main et boutons interactifs</span><span class="sxs-lookup"><span data-stu-id="2bc60-165">Hand tracking gestures and interactable buttons</span></span>

<span data-ttu-id="2bc60-166">Dans cette section, vous allez apprendre à utiliser le suivi de la main pour appuyer sur un bouton et déclencher des événements pour déclencher une action lorsque le bouton est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="2bc60-166">In this section, you will learn how to use hand tracking to press a button and trigger events to cause an action when the button is pressed.</span></span>

<span data-ttu-id="2bc60-167">Cet exemple vous montre comment modifier la couleur d’un cube lorsque le bouton est enfoncé et rétablir sa couleur d’origine quand le bouton est relâché.</span><span class="sxs-lookup"><span data-stu-id="2bc60-167">This particular example will show you how to change the color of a cube when the button is pressed and change it back to it's original color when the button is released.</span></span> <span data-ttu-id="2bc60-168">Toutefois, vous pouvez suivre ces mêmes principes pour créer d’autres événements.</span><span class="sxs-lookup"><span data-stu-id="2bc60-168">However, you may follow these same principles to create other events.</span></span>

<span data-ttu-id="2bc60-169">Les principales étapes à suivre pour modifier la couleur du cube sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2bc60-169">The main steps you will take to change the color of the cube are:</span></span>

1. <span data-ttu-id="2bc60-170">Ajouter un bouton Prefab à la scène</span><span class="sxs-lookup"><span data-stu-id="2bc60-170">Add a pressable button prefab to the scene</span></span>
2. <span data-ttu-id="2bc60-171">Ajouter un cube à la scène</span><span class="sxs-lookup"><span data-stu-id="2bc60-171">Add a cube to the scene</span></span>
3. <span data-ttu-id="2bc60-172">Configurer le type d’événement InteractableOnPressReceiver</span><span class="sxs-lookup"><span data-stu-id="2bc60-172">Configure the InteractableOnPressReceiver event type</span></span>
4. <span data-ttu-id="2bc60-173">Configurer le cube pour recevoir l’événement on Press</span><span class="sxs-lookup"><span data-stu-id="2bc60-173">Configure the cube to receive the On Press event</span></span>
5. <span data-ttu-id="2bc60-174">Définir l’action qui doit être déclenchée par l’événement on Press</span><span class="sxs-lookup"><span data-stu-id="2bc60-174">Define the action to be triggered by the On Press event</span></span>
6. <span data-ttu-id="2bc60-175">Configurer le cube pour recevoir l’événement on release</span><span class="sxs-lookup"><span data-stu-id="2bc60-175">Configure the cube to receive the On Release event</span></span>
7. <span data-ttu-id="2bc60-176">Définir l’action qui doit être déclenchée par l’événement on release</span><span class="sxs-lookup"><span data-stu-id="2bc60-176">Define the action to be triggered by the On Release event</span></span>
8. <span data-ttu-id="2bc60-177">Tester le bouton à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="2bc60-177">Test the button using the in-editor simulation</span></span>

### <a name="1-add-a-pressable-button-prefab-to-the-scene"></a><span data-ttu-id="2bc60-178">1. Ajouter un bouton Prefab à la scène</span><span class="sxs-lookup"><span data-stu-id="2bc60-178">1. Add a pressable button prefab to the scene</span></span>

> [!TIP]
> <span data-ttu-id="2bc60-179">Un <a href="https://docs.unity3d.com/Manual/Prefabs.html" target="_blank">Prefab</a> est un gameobject préconfiguré stocké en tant que ressource Unity et peut être réutilisé dans tout le projet.</span><span class="sxs-lookup"><span data-stu-id="2bc60-179">A <a href="https://docs.unity3d.com/Manual/Prefabs.html" target="_blank">prefab</a> is a pre-configured GameObject stored as a Unity Asset and can be reused throughout your project.</span></span>

<span data-ttu-id="2bc60-180">Dans la **fenêtre projet**, recherchez **PressableButtonHoloLens2** pour trouver le Prefab que vous allez utiliser pour cet exemple :</span><span class="sxs-lookup"><span data-stu-id="2bc60-180">In the **Project window**, search for **PressableButtonHoloLens2** to locate the prefab you will use for this example:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-1.png)

<span data-ttu-id="2bc60-182">Dans les résultats de la **recherche** , sélectionnez le Prefab **PressableButtonHoloLens2** et faites-le **glisser** dans la fenêtre **hiérarchie** pour l’ajouter à votre scène :</span><span class="sxs-lookup"><span data-stu-id="2bc60-182">In the **Search** result, select the **PressableButtonHoloLens2** prefab and **drag** it into the **Hierarchy** window to add it to your scene:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-2.png)

> [!TIP]
> <span data-ttu-id="2bc60-184">Pour afficher votre scène comme indiqué dans l’image ci-dessous, double-cliquez sur l’objet PressableButtonHoloLens2 dans la fenêtre hiérarchie pour l’activer, puis utilisez la <a href="https://docs.unity3d.com/Manual/SceneViewNavigation.html" target="_blank">scène Gizmo</a>, située dans le coin supérieur droit de la fenêtre de scène, pour ajuster l’angle d’affichage sur l’axe Z de l’avant.</span><span class="sxs-lookup"><span data-stu-id="2bc60-184">To display your scene as shown in the image below, double-click the PressableButtonHoloLens2 object in the Hierarchy window to bring it into focus, then use the <a href="https://docs.unity3d.com/Manual/SceneViewNavigation.html" target="_blank">Scene Gizmo</a>, located in the top right corner of the Scene window, to adjust the viewing angle to be along the forward Z axis.</span></span>

<span data-ttu-id="2bc60-185">L’objet PressableButtonHoloLens2 étant toujours sélectionné, dans la fenêtre de l' **inspecteur** :</span><span class="sxs-lookup"><span data-stu-id="2bc60-185">With the PressableButtonHoloLens2 object still selected, in the **Inspector** window:</span></span>

* <span data-ttu-id="2bc60-186">Modifiez sa **position** de transformation pour qu’elle soit positionnée devant l’appareil photo, qui est positionné à l’origine, par exemple, x = 0, y = 0 et z = 0,5</span><span class="sxs-lookup"><span data-stu-id="2bc60-186">Change its Transform **Position** so it's positioned in front of the camera, which is positioned at origin, for example, x = 0, y = 0, and z = 0.5</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-3.png)

> [!NOTE]
> <span data-ttu-id="2bc60-188">En général, une unité de position dans Unity est à peu près équivalente à 1 mètre dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="2bc60-188">In general, 1 position unit in Unity is roughly equivalent to 1 meter in the physical world.</span></span> <span data-ttu-id="2bc60-189">Toutefois, il existe des exceptions à cela, par exemple lorsque des objets sont des enfants d’objets mis à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="2bc60-189">However, there are exceptions to this, for example, when objects are children of scaled objects.</span></span>

### <a name="2-add-a-cube-to-the-scene"></a><span data-ttu-id="2bc60-190">2. Ajouter un cube à la scène</span><span class="sxs-lookup"><span data-stu-id="2bc60-190">2. Add a cube to the scene</span></span>

<span data-ttu-id="2bc60-191">Cliquez avec le bouton droit sur une zone vide à l’intérieur de la fenêtre de hiérarchie et sélectionnez **objet 3d** > **cube** pour ajouter un cube à votre scène :</span><span class="sxs-lookup"><span data-stu-id="2bc60-191">Right-click on an empty spot inside the Hierarchy window and select **3D Object** > **Cube** to add a cube to your scene:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step2-1.png)

<span data-ttu-id="2bc60-193">Lorsque l’objet cube est toujours sélectionné, dans la fenêtre **Inspector** :</span><span class="sxs-lookup"><span data-stu-id="2bc60-193">With the Cube object still selected, in the **Inspector** window:</span></span>

* <span data-ttu-id="2bc60-194">Modifiez sa **position** de transformation de sorte qu’elle soit située près du bouton enfoncé, mais qu’elle ne se chevauche pas, par exemple x = 0, y = 0,04 et z = 0,5</span><span class="sxs-lookup"><span data-stu-id="2bc60-194">Change its Transform **Position** so its located near the pressable button, but not overlapping with it, for example, x = 0, y = 0.04, and z = 0.5</span></span>
* <span data-ttu-id="2bc60-195">Modifiez son **échelle** de transformation en lui attribuant une taille appropriée, par exemple, x = 0,02, y = 0,02 et z = 0,02</span><span class="sxs-lookup"><span data-stu-id="2bc60-195">Change its Transform **Scale** to a suitable size, for example, x = 0.02, y = 0.02, and z = 0.02</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step2-2.png)

### <a name="3-configure-the-interactableonpressreceiver-event-type"></a><span data-ttu-id="2bc60-197">3. configurer le type d’événement InteractableOnPressReceiver</span><span class="sxs-lookup"><span data-stu-id="2bc60-197">3. Configure the InteractableOnPressReceiver event type</span></span>

<span data-ttu-id="2bc60-198">Lorsque l’objet PressableButtonHoloLens2 est sélectionné dans la fenêtre hiérarchie, dans le **menu hamburger**de la fenêtre de l' **inspecteur** , sélectionnez **réduire tous les composants** pour avoir une vue d’ensemble de tous les composants de cet objet :</span><span class="sxs-lookup"><span data-stu-id="2bc60-198">With the PressableButtonHoloLens2 object selected in the Hierarchy window, in the **Inspector** window **hamburger menu**, select **Collaps All Components** to get an overview of all components on this object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-1.png)

<span data-ttu-id="2bc60-200">Développez le composant **(script)** pouvant être interagi, puis localisez et développez la section **événements** > les **destinataires** :</span><span class="sxs-lookup"><span data-stu-id="2bc60-200">Expand the **Interactable (Script)** component, then locate and expand the **Events** > **Receivers** section:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-2.png)

<span data-ttu-id="2bc60-202">Pour le type de récepteur d’événements **InteractableOnPressReceiver**, remplacez le **filtre d’interaction** par **near et Far**:</span><span class="sxs-lookup"><span data-stu-id="2bc60-202">For the Event Receiver Type **InteractableOnPressReceiver**, change the **Interaction Filter** to **Near and Far**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-3.png)

> [!NOTE]
> <span data-ttu-id="2bc60-204">Le type de récepteur d’événements nommé InteractableOnPressReceiver permet au bouton de répondre à un événement appuyé quand un suivi appuie sur le bouton.</span><span class="sxs-lookup"><span data-stu-id="2bc60-204">The Event Receiver Type named InteractableOnPressReceiver allows the button to respond to a pressed event when a tracked hand presses the button.</span></span>

### <a name="4-configure-the-cube-to-receive-the-on-press-event"></a><span data-ttu-id="2bc60-205">4. configurer le cube pour recevoir l’événement on Press</span><span class="sxs-lookup"><span data-stu-id="2bc60-205">4. Configure the cube to receive the On Press event</span></span>

<span data-ttu-id="2bc60-206">Dans la fenêtre hiérarchie, **cliquez et faites glisser** le **cube** dans le champ objet des **propriétés d’événement** pour l’événement **on Press ()** afin d’affecter le cube comme récepteur de l’événement on Press () :</span><span class="sxs-lookup"><span data-stu-id="2bc60-206">From the Hierarchy window, **click-and-drag** the **Cube** into the **Event Properties** object field for the **On Press ()** event to assign the Cube as a receiver of the On Press () event:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step4-1.png)

### <a name="5-define-the-action-to-be-triggered-by-the-on-press-event"></a><span data-ttu-id="2bc60-208">5. définir l’action qui doit être déclenchée par l’événement on Press</span><span class="sxs-lookup"><span data-stu-id="2bc60-208">5. Define the action to be triggered by the On Press event</span></span>

<span data-ttu-id="2bc60-209">Cliquez sur la liste déroulante action, **aucune fonction**actuellement affectée, puis sélectionnez **MeshRenderer** > **matériau** matériel pour définir la propriété Material du cube à modifier lorsque l’événement on Press () est déclenché :</span><span class="sxs-lookup"><span data-stu-id="2bc60-209">Click the action dropdown, currently assigned **No Function**, and select **MeshRenderer** > **Material material** to set the Cube's material property to be changed when the On Press () event is triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-1.png)

<span data-ttu-id="2bc60-211">Cliquez sur l’icône représentant un petit **cercle** en regard du champ matériel, actuellement remplie sans **aucun (matériau)** , pour ouvrir la fenêtre Sélectionner une matière :</span><span class="sxs-lookup"><span data-stu-id="2bc60-211">Click the small **circle** icon next to the material field, currently populated with **None (Material)**, to open the Select Material window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-2.png)

<span data-ttu-id="2bc60-213">Dans la fenêtre Sélectionner une matière , recherchez **MRTK_Standard** et sélectionnez un matériau approprié, par exemple, **MRTK_Standard_Cyan** pour que la couleur du cube change en cyan lorsque le bouton est enfoncé :</span><span class="sxs-lookup"><span data-stu-id="2bc60-213">In the Select Material window, **search** for **MRTK_Standard** and select a suitable material, for example, **MRTK_Standard_Cyan** so the Cube's color changes to cyan when the button is pressed:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-3.png)

### <a name="6-configure-the-cube-to-receive-the-on-release-event"></a><span data-ttu-id="2bc60-215">6. configurer le cube pour recevoir l’événement on release</span><span class="sxs-lookup"><span data-stu-id="2bc60-215">6. Configure the cube to receive the On Release event</span></span>

<span data-ttu-id="2bc60-216">**Répéter** Étape 4 pour l’événement on release afin d’affecter le cube comme récepteur de l’événement on release ().</span><span class="sxs-lookup"><span data-stu-id="2bc60-216">**Repeat** Step 4 for the On Release event to assign the Cube as a receiver of the On Release () event.</span></span>

### <a name="7-define-the-action-to-be-triggered-by-the-on-release-event"></a><span data-ttu-id="2bc60-217">7. définir l’action qui doit être déclenchée par l’événement on release</span><span class="sxs-lookup"><span data-stu-id="2bc60-217">7. Define the action to be triggered by the On Release event</span></span>

<span data-ttu-id="2bc60-218">**Répéter** Étape 5 pour l’événement on release, mais choisissez le matériel **MRTK_Standard_LightGray** pour que la couleur du cube retourne à sa couleur gris clair d’origine lorsque le bouton est relâché :</span><span class="sxs-lookup"><span data-stu-id="2bc60-218">**Repeat** Step 5 for the On Release event, but choose the **MRTK_Standard_LightGray** material so the Cube's color returns to its original light gray color when the button is released:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step7-1.png)

### <a name="8-test-the-button-using-the-in-editor-simulation"></a><span data-ttu-id="2bc60-220">8. Testez le bouton à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="2bc60-220">8. Test the button using the in-editor simulation</span></span>

<span data-ttu-id="2bc60-221">Appuyez sur le bouton **lecture** pour entrer en mode jeu et utilisez la simulation d’entrée de l’éditeur pour tester le bouton que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="2bc60-221">Press the **Play** button to enter Game mode and use the in-editor input simulation to test your newly configured button.</span></span>

<span data-ttu-id="2bc60-222">Bouton non enfoncé (espace + molette de défilement de la souris vers l’arrière) :</span><span class="sxs-lookup"><span data-stu-id="2bc60-222">Button not pressed (spacebar + mouse scroll wheel backward):</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step8-1.png)

<span data-ttu-id="2bc60-224">Bouton enfoncé (espace + molette de défilement de la souris vers l’avant) :</span><span class="sxs-lookup"><span data-stu-id="2bc60-224">Button pressed (spacebar + mouse scroll wheel forward):</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step8-2.png)

> [!TIP]
> <span data-ttu-id="2bc60-226">Pour savoir comment utiliser la simulation d’entrée dans l’éditeur, vous pouvez vous reporter au [à l’aide de la simulation d’entrée de l’éditeur pour tester un](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) Guide de scène dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="2bc60-226">To learn how to use the in-editor input simulation, you can refer to the [Using the In-Editor Hand Input Simulation to test a scene](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="creating-a-panel-of-buttons-using-mrtks-grid-object-collection"></a><span data-ttu-id="2bc60-227">Création d’un panneau de boutons avec la collection d’objets de grille du MRTK</span><span class="sxs-lookup"><span data-stu-id="2bc60-227">Creating a panel of buttons using MRTK’s Grid Object Collection</span></span>

<span data-ttu-id="2bc60-228">Dans cette section, vous allez apprendre à aligner automatiquement plusieurs boutons dans une interface utilisateur claire à l’aide de l’outil de collection d’objets Grid de MRTK.</span><span class="sxs-lookup"><span data-stu-id="2bc60-228">In this section, you will learn how to automatically align multiple buttons into a neat user interface by using the MRTK’s Grid Object Collection tool.</span></span>

<span data-ttu-id="2bc60-229">Cet exemple indique comment créer un panneau avec cinq boutons alignés horizontalement.</span><span class="sxs-lookup"><span data-stu-id="2bc60-229">This particular example will show you how to a create a panel with five buttons aligned horizontally.</span></span> <span data-ttu-id="2bc60-230">Toutefois, vous pouvez suivre ces mêmes principes pour créer d’autres dispositions.</span><span class="sxs-lookup"><span data-stu-id="2bc60-230">However, you may follow these same principles to create other layouts.</span></span>

<span data-ttu-id="2bc60-231">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="2bc60-231">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="2bc60-232">Parent des objets bouton à un objet parent</span><span class="sxs-lookup"><span data-stu-id="2bc60-232">Parent the button objects to a parent object</span></span>
2. <span data-ttu-id="2bc60-233">Ajouter et configurer le composant de collection d’objets Grid (script)</span><span class="sxs-lookup"><span data-stu-id="2bc60-233">Add and configure the Grid Object Collection (Script) component</span></span>
3. <span data-ttu-id="2bc60-234">Tester les boutons à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="2bc60-234">Test the buttons using the in-editor simulation</span></span>

### <a name="1-parent-the-button-objects-to-a-parent-object"></a><span data-ttu-id="2bc60-235">1. parent des objets bouton à un objet parent</span><span class="sxs-lookup"><span data-stu-id="2bc60-235">1. Parent the button objects to a parent object</span></span>

<span data-ttu-id="2bc60-236">Cliquez avec le bouton droit sur une zone vide à l’intérieur de la fenêtre de hiérarchie et sélectionnez **créer un vide**:</span><span class="sxs-lookup"><span data-stu-id="2bc60-236">Right-click on an empty spot inside the Hierarchy window and select **Create Empty**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-1.png)

<span data-ttu-id="2bc60-238">Cliquez avec le bouton droit sur l’objet nouvellement créé, sélectionnez **Renommer**, puis attribuez-lui un nom approprié, par exemple, **ButtonCollection**:</span><span class="sxs-lookup"><span data-stu-id="2bc60-238">Right-click on the newly created object, select **Rename**, and give it a suitable name, for example, **ButtonCollection**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-2.png)

<span data-ttu-id="2bc60-240">Sélectionnez l’objet **PressableButtonHoloLens2** et **faites** -le glisser sur l’objet **ButtonCollection** pour en faire un enfant de l’objet ButtonCollection :</span><span class="sxs-lookup"><span data-stu-id="2bc60-240">Select the **PressableButtonHoloLens2** object and **drag** it on top of the **ButtonCollection** object to make it a child of the ButtonCollection object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-3.png)

<span data-ttu-id="2bc60-242">Cliquez avec le bouton droit sur l’objet **PressableButtonHoloLens2** et sélectionnez **dupliquer** pour en créer une copie :</span><span class="sxs-lookup"><span data-stu-id="2bc60-242">Right-click the **PressableButtonHoloLens2** object and select **Duplicate** to create a copy of it:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-4.png)

<span data-ttu-id="2bc60-244">**Répétez** cette étape quatre fois, jusqu’à ce que vous ayez un total de cinq objets PressableButtonHoloLens2.</span><span class="sxs-lookup"><span data-stu-id="2bc60-244">**Repeat** this step four more times until you have a total of five PressableButtonHoloLens2 objects.</span></span>

### <a name="2-add-and-configure-the-grid-object-collection-script-component"></a><span data-ttu-id="2bc60-245">2. Ajouter et configurer le composant collection d’objets Grid (script)</span><span class="sxs-lookup"><span data-stu-id="2bc60-245">2. Add and configure the Grid Object Collection (Script) component</span></span>

<span data-ttu-id="2bc60-246">Lorsque l’objet ButtonCollection est sélectionné dans la fenêtre hiérarchie, dans la fenêtre Inspecteur, cliquez sur le bouton **Ajouter un composant** , puis recherchez et sélectionnez **collection d’objets Grid** pour ajouter un composant de collection d’objets Grid (script) à l’objet ButtonCollection :</span><span class="sxs-lookup"><span data-stu-id="2bc60-246">With the ButtonCollection object selected in the Hierarchy window, in the Inspector window, click the **Add Component** button, then search for and select **Grid Object Collection** to add a Grid Object Collection (Script) component to the ButtonCollection object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-1.png)

<span data-ttu-id="2bc60-248">Configurez la collection d’objets Grid (script) comme suit :</span><span class="sxs-lookup"><span data-stu-id="2bc60-248">Configure the Grid Object Collection (Script) as follows:</span></span>

* <span data-ttu-id="2bc60-249">Remplacez le **nombre de lignes** par 1 pour que tous les boutons soient alignés sur une seule ligne</span><span class="sxs-lookup"><span data-stu-id="2bc60-249">Change **Num Rows** to 1 to have all buttons aligned on one single row</span></span>
* <span data-ttu-id="2bc60-250">Modifiez la **largeur de cellule** sur 0,05 pour espacer les boutons dans la ligne</span><span class="sxs-lookup"><span data-stu-id="2bc60-250">Change **Cell Width** to 0.05 to space out the buttons within the row</span></span>

<span data-ttu-id="2bc60-251">Cliquez ensuite sur le bouton **mettre à jour la collection** pour appliquer la nouvelle configuration :</span><span class="sxs-lookup"><span data-stu-id="2bc60-251">Then click the **Update Collection** button to apply the new configuration:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-2.png)

> [!NOTE]
> <span data-ttu-id="2bc60-253">Les modifications de configuration que vous venez d’appliquer représentent les modifications minimales requises pour atteindre l’objectif de placer les boutons sur une seule ligne.</span><span class="sxs-lookup"><span data-stu-id="2bc60-253">The configuration changes you just applied represent the minimum changes required to achieve the objective of placing the buttons in a single row.</span></span> <span data-ttu-id="2bc60-254">Toutefois, dans les projets futurs, en fonction de facteurs tels que, par exemple, l’orientation des objets parents et enfants, vous devrez peut-être ajuster d’autres paramètres tels que, par exemple, le type d’orientation.</span><span class="sxs-lookup"><span data-stu-id="2bc60-254">However, in future projects, depending on factors such as, for example, the orientation of the parent and child objects, you might need to adjust other settings such as, for example, the Orient Type.</span></span> <span data-ttu-id="2bc60-255">Pour en savoir plus sur la collection d’objets Grid de MRTK, vous pouvez consulter le guide des [scripts de collection d’objets](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html#object-collection-scripts) dans le portail de [documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="2bc60-255">To learn more about MRTK's Grid Object Collection, you can visit the [Object collection scripts](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html#object-collection-scripts) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

<span data-ttu-id="2bc60-256">Lorsque l’objet ButtonCollection est toujours sélectionné dans la fenêtre hiérarchie, dans la fenêtre de l’inspecteur, modifiez la **position** de la transformation de l’objet ButtonCollection de sorte que ses objets bouton enfant soient positionnés devant l’appareil photo, qui est positionné à l’origine, par exemple, x = 0, y = 0 et z = 0,5 :</span><span class="sxs-lookup"><span data-stu-id="2bc60-256">With the ButtonCollection object still selected in the Hierarchy window, in the Inspector window, change the ButtonCollection object's Transform **Position** so its child button objects are positioned in front of the camera, which is positioned at origin, for example, x = 0, y = 0, and z = 0.5:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-3.png)

> [!NOTE]
> <span data-ttu-id="2bc60-258">Lorsque vous avez ajouté pour la première fois le Prefab PressableButtonHoloLens2 à la scène dans la section [gestes de suivi de main et boutons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) interactifs ci-dessus, vous l’avez positionné devant l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="2bc60-258">When you first added the PressableButtonHoloLens2 prefab to the scene in the [Hand tracking gestures and interactable buttons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) section above, you positioned it in front of the camera.</span></span> <span data-ttu-id="2bc60-259">Toutefois, étant donné que la collection d’objets Grid contrôle ses objets enfants immédiats, la position Z des objets enfants PressableButtonHoloLens2 est réinitialisée à 0 en fonction de la distance par défaut de la collection d’objets Grid par rapport à la valeur parente de 0.</span><span class="sxs-lookup"><span data-stu-id="2bc60-259">However, because the Grid Object Collection controls its immediate child objects' position, the PressableButtonHoloLens2 child objects' Z Position were reset to 0 according to the Grid Object Collection's default Distance from parent value of 0.</span></span> <span data-ttu-id="2bc60-260">C’est pourquoi, et pour que la relation de position parent/enfant est organisée, c’est pourquoi nous avons déplacé la position de l’objet ButtonCollection parent au lieu de configurer la distance à partir de la valeur parente pour déplacer les objets enfants PressableButtonHoloLens2 vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="2bc60-260">This, and to keep the parent/child positional relationship organized, is why we moved the parent ButtonCollection object's position forward instead of configuring the Distance from parent value to move the PressableButtonHoloLens2 child objects forward.</span></span>

### <a name="3-test-the-buttons-using-the-in-editor-simulation"></a><span data-ttu-id="2bc60-261">3. Testez les boutons à l’aide de la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="2bc60-261">3. Test the buttons using the in-editor simulation</span></span>

<span data-ttu-id="2bc60-262">Appuyez sur le bouton lecture pour entrer en mode jeu et utilisez la simulation d’entrée de l’éditeur pour tester chacun des boutons dans le nouveau panneau de boutons :</span><span class="sxs-lookup"><span data-stu-id="2bc60-262">Press the Play button to enter Game mode and use the in-editor input simulation to test each of the buttons in in your newly created panel of buttons:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step3-1.png)

> [!TIP]
> <span data-ttu-id="2bc60-264">Actuellement, lorsque vous appuyez sur l’un des cinq boutons, la couleur du cube devient cyan.</span><span class="sxs-lookup"><span data-stu-id="2bc60-264">Currently, when your press any of the five buttons, the cube color changes to cyan.</span></span> <span data-ttu-id="2bc60-265">Pour rendre l’expérience plus intéressante, utilisez ce que vous venez d’apprendre pour configurer chaque bouton afin de remplacer le cube par une autre couleur.</span><span class="sxs-lookup"><span data-stu-id="2bc60-265">To make the experience more interesting, use what you just learn to configure each button to change the cube to a different color.</span></span>

## <a name="adding-text-into-your-scene"></a><span data-ttu-id="2bc60-266">Ajout de texte dans votre scène</span><span class="sxs-lookup"><span data-stu-id="2bc60-266">Adding text into your scene</span></span>

<span data-ttu-id="2bc60-267">Dans cette section, vous allez apprendre à ajouter du texte à vos expériences de réalité mixte à l’aide de TextMesh Pro de Unity, que vous avez préparé dans la section [importer des ressources TextMesh Pro Essential](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources) du didacticiel précédent.</span><span class="sxs-lookup"><span data-stu-id="2bc60-267">In this section, you will learn how to add text to your mixed reality experiences using Unity's TextMesh Pro, which you prepared in the [Import TextMesh Pro Essential Resources](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources) section of the previous tutorial.</span></span>

<span data-ttu-id="2bc60-268">Dans cet exemple, vous allez ajouter une étiquette simple sous la collection de boutons que vous avez créée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="2bc60-268">In this particular example, you will add a simple label underneath the button collection you created in the previous section.</span></span>

<span data-ttu-id="2bc60-269">Cliquez avec le bouton droit sur l’objet ButtonCollection, puis sélectionnez **objet 3d** > **Text-TextMeshPro** pour créer un objet TextMeshPro en tant qu’enfant de l’objet ButtonCollection :</span><span class="sxs-lookup"><span data-stu-id="2bc60-269">Right-click on the ButtonCollection object and select **3D Object** > **Text - TextMeshPro** to create a TextMeshPro object as a child of the ButtonCollection object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section4-step1-1.png)

<span data-ttu-id="2bc60-271">Avec l’objet TextMeshPro nouvellement créé, nommé Text (TMP), toujours sélectionné, dans la fenêtre Inspector, modifiez sa position et sa taille pour que l’étiquette soit placée clairement sous la collection de boutons, par exemple :</span><span class="sxs-lookup"><span data-stu-id="2bc60-271">With the newly created TextMeshPro object, named Text (TMP), still selected, in the Inspector window change its position and size so the label is placed neatly underneath the button collection, for example:</span></span>

* <span data-ttu-id="2bc60-272">Remplacez le POS transformation Rect **Y** par-0,0425</span><span class="sxs-lookup"><span data-stu-id="2bc60-272">Change the Rect Transform **Pos Y** to -0.0425</span></span>
* <span data-ttu-id="2bc60-273">Modifiez la **largeur** de la transformation Rect en 0,24</span><span class="sxs-lookup"><span data-stu-id="2bc60-273">Change the Rect Transform **Width** to 0.24</span></span>
* <span data-ttu-id="2bc60-274">Modifier la **hauteur** de la transformation Rect en 0,024</span><span class="sxs-lookup"><span data-stu-id="2bc60-274">Change the Rect Transform **Height** to 0.024</span></span>

<span data-ttu-id="2bc60-275">Ensuite, mettez à jour le texte pour refléter l’étiquette et choisissez les propriétés de police pour que le texte tienne dans l’étiquette, par exemple :</span><span class="sxs-lookup"><span data-stu-id="2bc60-275">Then update the text to reflect what the label is for and choose font properties so the text fits within the label, for example:</span></span>

* <span data-ttu-id="2bc60-276">Remplacer le texte de maille Pro (script **) par** la collection de boutons</span><span class="sxs-lookup"><span data-stu-id="2bc60-276">Change the Text Mesh Pro (Script) **Text** to Button Collection</span></span>
* <span data-ttu-id="2bc60-277">Modifier le **style de police** du texte de maillage Pro (script) en gras</span><span class="sxs-lookup"><span data-stu-id="2bc60-277">Change the Text Mesh Pro (Script) **Font Style** to Bold</span></span>
* <span data-ttu-id="2bc60-278">Modifier la **taille de police** du texte de maille Pro (script) à 0,2</span><span class="sxs-lookup"><span data-stu-id="2bc60-278">Change the Text Mesh Pro (Script) **Font Size** to 0.2</span></span>
* <span data-ttu-id="2bc60-279">Modifiez l' **alignement** du texte de maille Pro (script) en centre et au milieu</span><span class="sxs-lookup"><span data-stu-id="2bc60-279">Change the Text Mesh Pro (Script) **Alignment** to Center and Middle</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section4-step1-2.png)

## <a name="congratulations"></a><span data-ttu-id="2bc60-281">Félicitations</span><span class="sxs-lookup"><span data-stu-id="2bc60-281">Congratulations</span></span>

<span data-ttu-id="2bc60-282">Dans ce didacticiel, vous avez appris à cloner, personnaliser et configurer un paramètre de profil MRTK.</span><span class="sxs-lookup"><span data-stu-id="2bc60-282">In this tutorial, you learned how to clone, customize, and configure an MRTK profile setting.</span></span> <span data-ttu-id="2bc60-283">Vous avez également appris à interagir avec les boutons pour déclencher des événements à l’aide d’un suivi sur le HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="2bc60-283">You also learned how to interact with buttons to trigger events using tracked hands on the HoloLens 2.</span></span> <span data-ttu-id="2bc60-284">Enfin, vous avez appris à créer une interface d’interface utilisateur simple à l’aide du composant de collection d’objets Grid de MRTK et du texte Pro de l’Unity.</span><span class="sxs-lookup"><span data-stu-id="2bc60-284">Finally, you learned how to create a simple UI interface using the MRTK's Grid Object Collection component and Unity's Text Mesh Pro.</span></span>

[<span data-ttu-id="2bc60-285">Didacticiel suivant : 4. placement de contenu dynamique et utilisation de solveurs</span><span class="sxs-lookup"><span data-stu-id="2bc60-285">Next Tutorial: 4. Placing dynamic content and using solvers</span></span>](mrlearning-base-ch3.md)
