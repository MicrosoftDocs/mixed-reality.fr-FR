---
title: Tutoriels de démarrage - 3. Création de l’interface utilisateur et configuration du Kit d’outils de réalité mixte
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: c389c7a3d16770dcbf57d9acdcfd81c6507f7cd6
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "79376136"
---
# <a name="3-creating-user-interface-and-configure-mixed-reality-toolkit"></a><span data-ttu-id="b36d6-105">3. Création de l’interface utilisateur et configuration du Kit d’outils de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="b36d6-105">3. Creating user interface and configure Mixed Reality Toolkit</span></span>
<!-- TODO: Consider renaming to 'Configuring Mixed Reality Toolkit profiles and creating user interfaces' -->

<span data-ttu-id="b36d6-106">Dans le tutoriel précédent, vous avez découvert certaines des fonctionnalités offertes par le Kit de ressources de réalité mixte (MRTK, Mixed Reality Toolkit) en commençant votre première application pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="b36d6-106">In the previous tutorial, you learned about some of the capabilities the Mixed Reality Toolkit (MRTK) has to offer by starting your first application for the HoloLens 2.</span></span> <span data-ttu-id="b36d6-107">Dans ce tutoriel, vous allez découvrir comment créer et organiser des boutons et des panneaux de texte de l’interface utilisateur, et comment utiliser l’interaction par défaut (tactile) pour interagir avec chaque bouton.</span><span class="sxs-lookup"><span data-stu-id="b36d6-107">In this tutorial you will learn how to create and organize buttons along with UI text panels, and use default interaction (touch) to interact with each button.</span></span> <span data-ttu-id="b36d6-108">Vous allez également découvrir comment ajouter des actions et des effets simples, comme changer la taille, la sonorité et la couleur des objets.</span><span class="sxs-lookup"><span data-stu-id="b36d6-108">You will also explore the addition of simple actions and effects, such as changing the size, sound and color of objects.</span></span> <span data-ttu-id="b36d6-109">Ce module présente des concepts de base sur la façon de modifier des profils MRTK, en commençant par la désactivation de la visualisation du maillage de [mappage spatial](spatial-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="b36d6-109">This module will introduce basic concepts about modifying MRTK profiles, starting with turning off the [spatial mapping](spatial-mapping.md) mesh visualization.</span></span>

## <a name="objectives"></a><span data-ttu-id="b36d6-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="b36d6-110">Objectives</span></span>

* <span data-ttu-id="b36d6-111">Personnaliser et configurer des profils MRTK</span><span class="sxs-lookup"><span data-stu-id="b36d6-111">Customize and configure Mixed Reality Toolkit profiles</span></span>
* <span data-ttu-id="b36d6-112">Interaction avec des hologrammes en utilisant des éléments d’interface utilisateur et des boutons</span><span class="sxs-lookup"><span data-stu-id="b36d6-112">Interact with holograms using UI elements and buttons</span></span>
* <span data-ttu-id="b36d6-113">Entrées et interactions de base pour le suivi de la main</span><span class="sxs-lookup"><span data-stu-id="b36d6-113">Basic hand-tracking input and interactions</span></span>

## <a name="how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option"></a><span data-ttu-id="b36d6-114">Comment configurer les profils du Kit de ressources de réalité mixte (Modifier l’option d’affichage de la reconnaissance spatiale)</span><span class="sxs-lookup"><span data-stu-id="b36d6-114">How to configure the Mixed Reality Toolkit Profiles (Change Spatial Awareness Display Option)</span></span>
<!-- TODO: Consider renaming to 'How to customize the MRTK profiles' -->

<span data-ttu-id="b36d6-115">Dans cette section, vous allez découvrir comment personnaliser et configurer les profils MRTK par défaut.</span><span class="sxs-lookup"><span data-stu-id="b36d6-115">In this section, you will learn how to customize and configure the default MRTK profiles.</span></span>

<span data-ttu-id="b36d6-116">Cet exemple va vous montrer comment masquer le maillage de la reconnaissance spatiale en modifiant les paramètres de l’observateur de maillage spatial.</span><span class="sxs-lookup"><span data-stu-id="b36d6-116">This particular example will show you how to hide the spatial awareness mesh by changing the settings of the Spatial Mesh Observer.</span></span> <span data-ttu-id="b36d6-117">Vous pouvez cependant suivre ces mêmes principes pour personnaliser des paramètres ou des valeurs dans les profils MRTK.</span><span class="sxs-lookup"><span data-stu-id="b36d6-117">However, you may follow these same principles to customize any setting or value in the MRTK profiles.</span></span>

<span data-ttu-id="b36d6-118">Les principales étapes à suivre pour masquer le maillage de la reconnaissance spatiale sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="b36d6-118">The main steps you will take to hide the spatial awareness mesh are:</span></span>

1. <span data-ttu-id="b36d6-119">Cloner le profil de configuration par défaut</span><span class="sxs-lookup"><span data-stu-id="b36d6-119">Clone the default Configuration Profile</span></span>
2. <span data-ttu-id="b36d6-120">Activer le système de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="b36d6-120">Enable the Spatial Awareness System</span></span>
3. <span data-ttu-id="b36d6-121">Cloner le profil système de reconnaissance spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="b36d6-121">Clone the default Spatial Awareness System Profile</span></span>
4. <span data-ttu-id="b36d6-122">Cloner le profil d’observateur de maillage de reconnaissance spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="b36d6-122">Clone the default Spatial Awareness Mesh Observer Profile</span></span>
5. <span data-ttu-id="b36d6-123">Changer la visibilité du maillage de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="b36d6-123">Change the visibility of the spatial awareness mesh</span></span>

> [!NOTE]
> <span data-ttu-id="b36d6-124">Par défaut, les profils MRTK ne sont pas modifiables.</span><span class="sxs-lookup"><span data-stu-id="b36d6-124">By default, the MRTK profiles are not editable.</span></span> <span data-ttu-id="b36d6-125">Il s’agit des modèles de profil par défaut que vous devez cloner avant de pouvoir les modifier.</span><span class="sxs-lookup"><span data-stu-id="b36d6-125">These are default profile templates that you have to clone before they can be edited.</span></span> <span data-ttu-id="b36d6-126">Il existe plusieurs couches de profils imbriquées.</span><span class="sxs-lookup"><span data-stu-id="b36d6-126">There are several nested layers of profiles.</span></span> <span data-ttu-id="b36d6-127">Par conséquent, il est courant de cloner et de modifier plusieurs profils lors de la configuration d’un ou plusieurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="b36d6-127">Therefore, it is common to clone and edit several profiles when configuring one or more settings.</span></span>

### <a name="1-clone-the-default-configuration-profile"></a><span data-ttu-id="b36d6-128">1. Cloner le profil de configuration par défaut</span><span class="sxs-lookup"><span data-stu-id="b36d6-128">1. Clone the default Configuration Profile</span></span>

> [!NOTE]
> <span data-ttu-id="b36d6-129">Le profil de configuration est le profil de plus haut niveau.</span><span class="sxs-lookup"><span data-stu-id="b36d6-129">The Configuration Profile is the top level profile.</span></span> <span data-ttu-id="b36d6-130">Par conséquent, pour pouvoir modifier d’autres profils, vous devez d’abord cloner le profil de configuration.</span><span class="sxs-lookup"><span data-stu-id="b36d6-130">Consequently, to be able to edit any other profiles, you first have to clone the Configuration Profile.</span></span>

<span data-ttu-id="b36d6-131">Avec l’objet **MixedRealityToolkit** sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, changez le **profil de configuration** Mixed Reality Toolkit en **DefaultHoloLens2ConfigurationProfile** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-131">With the **MixedRealityToolkit** object selected in the Hierarchy window, in the Inspector window, change the Mixed Reality Toolkit **Configuration Profile** to **DefaultHoloLens2ConfigurationProfile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-1.png)

<span data-ttu-id="b36d6-133">Avec l’objet **MixedRealityToolkit** sélectionné, dans la fenêtre Inspector, cliquez sur le bouton **Copy & Customize** pour ouvrir la fenêtre Clone Profile :</span><span class="sxs-lookup"><span data-stu-id="b36d6-133">With the **MixedRealityToolkit** object still selected, in the Inspector window, click the **Copy & Customize** button to open the Clone Profile window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-2.png)

<span data-ttu-id="b36d6-135">Dans la fenêtre Clone Profile, cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultHololens2ConfigurationProfile** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-135">In the Clone Profile window, click the **Clone** button to create an editable copy of the **DefaultHololens2ConfigurationProfile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-3.png)

<span data-ttu-id="b36d6-137">Le profil de configuration que vous venez de créer est maintenant affecté comme profil de configuration pour votre scène :</span><span class="sxs-lookup"><span data-stu-id="b36d6-137">The newly created Configuration Profile is now assigned as the Configuration Profile for your scene:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-4.png)

<span data-ttu-id="b36d6-139">Dans le menu Unity, sélectionnez **File** > **Save** pour enregistrer votre scène.</span><span class="sxs-lookup"><span data-stu-id="b36d6-139">In the Unity menu, select **File** > **Save** to save your scene.</span></span>

> [!TIP]
> <span data-ttu-id="b36d6-140">N’oubliez pas d’enregistrer votre travail tout au long du tutoriel.</span><span class="sxs-lookup"><span data-stu-id="b36d6-140">Remember to save your work throughout the tutorial.</span></span>

### <a name="2-enable-the-spatial-awareness-system"></a><span data-ttu-id="b36d6-141">2. Activer le système de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="b36d6-141">2. Enable the Spatial Awareness System</span></span>

<span data-ttu-id="b36d6-142">Avec l’objet **MixedRealityToolkit** sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, sélectionnez l’onglet **Spatial Awareness**, puis cochez la case **Enable Spatial Awareness System** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-142">With the **MixedRealityToolkit** object still selected in the Hierarchy window, in the Inspector window, select the **Spatial Awareness** tab, and then check the **Enable Spatial Awareness System** checkbox:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step2-1.png)

### <a name="3-clone-the-default-spatial-awareness-system-profile"></a><span data-ttu-id="b36d6-144">3. Cloner le profil système de reconnaissance spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="b36d6-144">3. Clone the default Spatial Awareness System Profile</span></span>

<span data-ttu-id="b36d6-145">Sous l’onglet **Spatial Awareness**, cliquez sur le bouton **Clone** pour ouvrir la fenêtre Clone Profile :</span><span class="sxs-lookup"><span data-stu-id="b36d6-145">In the **Spatial Awareness** tab, click the **Clone** button to open the Clone Profile window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-1.png)

<span data-ttu-id="b36d6-147">Dans la fenêtre Clone Profile, cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultMixedRealitySpatialAwarenessSystemProfile** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-147">In the Clone Profile window, click the **Clone** button to create an editable copy of the **DefaultMixedRealitySpatialAwarenessSystemProfile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-2.png)

<span data-ttu-id="b36d6-149">Le profil Spatial Awareness System nouvellement créé est maintenant automatiquement affecté à votre profil de configuration :</span><span class="sxs-lookup"><span data-stu-id="b36d6-149">The newly created Spatial Awareness System Profile is now automatically assigned to your Configuration Profile:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-3.png)

### <a name="4-clone-the-default-spatial-awareness-mesh-observer-profile"></a><span data-ttu-id="b36d6-151">4. Cloner le profil d’observateur de maillage de reconnaissance spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="b36d6-151">4. Clone the default Spatial Awareness Mesh Observer Profile</span></span>

<span data-ttu-id="b36d6-152">Avec l’onglet **Spatial Awareness** sélectionné, développez la section **Windows Mixed Reality Spatial Mesh Observer**, puis cliquez sur le bouton **Clone** pour ouvrir la fenêtre Clone Profile :</span><span class="sxs-lookup"><span data-stu-id="b36d6-152">With the **Spatial Awareness** tab still selected, expand the **Windows Mixed Reality Spatial Mesh Observer** section, then click the **Clone** button to open the Clone Profile window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-1.png)

<span data-ttu-id="b36d6-154">Dans la fenêtre Clone Profile, cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultMixedRealitySpatialAwarenessMeshObserverProfile** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-154">In the Clone Profile window, click the **Clone** button to create an editable copy of the **DefaultMixedRealitySpatialAwarenessMeshObserverProfile**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-2.png)

<span data-ttu-id="b36d6-156">Le profil Spatial Awareness Mesh Observer nouvellement créé est maintenant automatiquement affecté à votre profil Spatial Awareness System :</span><span class="sxs-lookup"><span data-stu-id="b36d6-156">The newly created Spatial Awareness Mesh Observer Profile is now automatically assigned to your Spatial Awareness System Profile:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-3.png)

### <a name="5-change-the-visibility-of-the-spatial-awareness-mesh"></a><span data-ttu-id="b36d6-158">5. Changer la visibilité du maillage de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="b36d6-158">5. Change the visibility of the spatial awareness mesh</span></span>

<span data-ttu-id="b36d6-159">Dans **Spatial Mesh Observer Settings**, changez **Display Option** en **Occlusion** pour rendre le maillage de mappage spatial invisible tout en le laissant fonctionnel :</span><span class="sxs-lookup"><span data-stu-id="b36d6-159">In the **Spatial Mesh Observer Settings**, change the **Display Option** to **Occlusion** to make the spatial mapping mesh invisible while still being functional:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step5-1.png)

> [!NOTE]
> <span data-ttu-id="b36d6-161">Bien que le maillage de mappage spatial ne soit pas visible, il est toujours présent et fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="b36d6-161">Although the spatial mapping mesh is not visible, it is still present and functional.</span></span> <span data-ttu-id="b36d6-162">Par exemple, les hologrammes qui sont derrière le maillage de mappage spatial, comme un hologramme derrière un mur physique, ne sont pas visibles.</span><span class="sxs-lookup"><span data-stu-id="b36d6-162">For example, any holograms behind the spatial mapping mesh, such as a hologram behind a physical wall, will not be visible.</span></span>

<span data-ttu-id="b36d6-163">Vous venez de découvrir comment modifier un paramètre dans le profil MRTK.</span><span class="sxs-lookup"><span data-stu-id="b36d6-163">You just learned how to modify a setting in the MRTK profile.</span></span> <span data-ttu-id="b36d6-164">Comme vous pouvez le voir, pour pouvoir personnaliser les paramètres du MRTK, vous devez d’abord créer des copies des profils par défaut.</span><span class="sxs-lookup"><span data-stu-id="b36d6-164">As you can see, in order to customize the MRTK settings, you first need to create copies of the default profiles.</span></span> <span data-ttu-id="b36d6-165">Étant donné que les profils par défaut ne sont pas modifiables, vous les aurez toujours comme référence si vous voulez rétablir les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="b36d6-165">Because the default profiles are not editable, you will always have them as reference if you want revert back to the default settings.</span></span> <span data-ttu-id="b36d6-166">Pour plus d’informations sur les profils MRTK et leur architecture, vous pouvez consulter le [Guide de configuration du profil Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="b36d6-166">To learn more about MRTK profiles and their architecture, you can visit the [Mixed Reality Toolkit profile configuration guide](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="hand-tracking-gestures-and-interactable-buttons"></a><span data-ttu-id="b36d6-167">Gestes de suivi de la main et boutons d’interaction</span><span class="sxs-lookup"><span data-stu-id="b36d6-167">Hand tracking gestures and interactable buttons</span></span>

<span data-ttu-id="b36d6-168">Dans cette section, vous allez découvrir comment utiliser le suivi de la main pour appuyer sur un bouton et déclencher des événements pour provoquer une action quand le bouton est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="b36d6-168">In this section, you will learn how to use hand tracking to press a button and trigger events to cause an action when the button is pressed.</span></span>

<span data-ttu-id="b36d6-169">Cet exemple vous montre comment changer la couleur d’un cube quand le bouton est enfoncé et rétablir sa couleur d’origine quand le bouton est relâché.</span><span class="sxs-lookup"><span data-stu-id="b36d6-169">This particular example will show you how to change the color of a cube when the button is pressed and change it back to it's original color when the button is released.</span></span> <span data-ttu-id="b36d6-170">Vous pouvez cependant suivre ces mêmes principes pour créer d’autres événements.</span><span class="sxs-lookup"><span data-stu-id="b36d6-170">However, you may follow these same principles to create other events.</span></span>

<span data-ttu-id="b36d6-171">Les principales étapes à suivre pour changer la couleur du cube sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="b36d6-171">The main steps you will take to change the color of the cube are:</span></span>

1. <span data-ttu-id="b36d6-172">Ajouter un préfabriqué de bouton enfonçable</span><span class="sxs-lookup"><span data-stu-id="b36d6-172">Add a pressable button prefab to the scene</span></span>
2. <span data-ttu-id="b36d6-173">Ajouter un cube à la scène</span><span class="sxs-lookup"><span data-stu-id="b36d6-173">Add a cube to the scene</span></span>
3. <span data-ttu-id="b36d6-174">Configurer le type d’événement InteractableOnPressReceiver</span><span class="sxs-lookup"><span data-stu-id="b36d6-174">Configure the InteractableOnPressReceiver event type</span></span>
4. <span data-ttu-id="b36d6-175">Configurer le cube pour recevoir l’événement On Press</span><span class="sxs-lookup"><span data-stu-id="b36d6-175">Configure the cube to receive the On Press event</span></span>
5. <span data-ttu-id="b36d6-176">Définir l’action à déclencher par l’événement On Press</span><span class="sxs-lookup"><span data-stu-id="b36d6-176">Define the action to be triggered by the On Press event</span></span>
6. <span data-ttu-id="b36d6-177">Configurer le cube pour recevoir l’événement On Release</span><span class="sxs-lookup"><span data-stu-id="b36d6-177">Configure the cube to receive the On Release event</span></span>
7. <span data-ttu-id="b36d6-178">Définir l’action à déclencher par l’événement On Release</span><span class="sxs-lookup"><span data-stu-id="b36d6-178">Define the action to be triggered by the On Release event</span></span>
8. <span data-ttu-id="b36d6-179">Tester le bouton en utilisant la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="b36d6-179">Test the button using the in-editor simulation</span></span>

### <a name="1-add-a-pressable-button-prefab-to-the-scene"></a><span data-ttu-id="b36d6-180">1. Ajouter un préfabriqué de bouton enfonçable</span><span class="sxs-lookup"><span data-stu-id="b36d6-180">1. Add a pressable button prefab to the scene</span></span>

> [!TIP]
> <span data-ttu-id="b36d6-181">Un <a href="https://docs.unity3d.com/Manual/Prefabs.html" target="_blank">préfabriqué</a> (Prefab) est un GameObject préconfiguré stocké en tant que ressource Unity et qui peut être réutilisé dans tout votre projet.</span><span class="sxs-lookup"><span data-stu-id="b36d6-181">A <a href="https://docs.unity3d.com/Manual/Prefabs.html" target="_blank">prefab</a> is a pre-configured GameObject stored as a Unity Asset and can be reused throughout your project.</span></span>

<span data-ttu-id="b36d6-182">Dans la **fenêtre Project**, recherchez **PressableButtonHoloLens2** pour localiser le préfabriqué que vous allez utiliser pour cet exemple :</span><span class="sxs-lookup"><span data-stu-id="b36d6-182">In the **Project window**, search for **PressableButtonHoloLens2** to locate the prefab you will use for this example:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-1.png)

<span data-ttu-id="b36d6-184">Dans le résultat de la **Recherche**, sélectionnez le préfabriqué **PressableButtonHoloLens2** et **faites-le glisser** dans la fenêtre **Hierarchy** pour l’ajouter à votre scène :</span><span class="sxs-lookup"><span data-stu-id="b36d6-184">In the **Search** result, select the **PressableButtonHoloLens2** prefab and **drag** it into the **Hierarchy** window to add it to your scene:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-2.png)

> [!TIP]
> <span data-ttu-id="b36d6-186">Pour afficher votre scène comme dans l’image ci-dessous, double-cliquez sur l’objet PressableButtonHoloLens2 dans la fenêtre Hierarchy pour lui donner le focus, puis utilisez le <a href="https://docs.unity3d.com/Manual/SceneViewNavigation.html" target="_blank">gizmo Scene</a>, qui se trouve dans le coin supérieur droit de la fenêtre Scene, pour ajuster l’angle de visualisation sur l’axe Z vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="b36d6-186">To display your scene as shown in the image below, double-click the PressableButtonHoloLens2 object in the Hierarchy window to bring it into focus, then use the <a href="https://docs.unity3d.com/Manual/SceneViewNavigation.html" target="_blank">Scene Gizmo</a>, located in the top right corner of the Scene window, to adjust the viewing angle to be along the forward Z axis.</span></span>

<span data-ttu-id="b36d6-187">Avec l’objet **PressableButtonHoloLens2** sélectionné, dans la fenêtre **Inspector** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-187">With the **PressableButtonHoloLens2** object still selected, in the **Inspector** window:</span></span>

* <span data-ttu-id="b36d6-188">Changez la valeur **Position** de sa transformation de sorte qu’il soit positionné devant la caméra, elle-même positionnée à l’origine, par exemple x = 0, y = 0 et z = 0,5</span><span class="sxs-lookup"><span data-stu-id="b36d6-188">Change its Transform **Position** so it's positioned in front of the camera, which is positioned at origin, for example, x = 0, y = 0, and z = 0.5</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-3.png)

> [!NOTE]
> <span data-ttu-id="b36d6-190">En règle générale, 1 unité de position dans Unity est à peu près équivalente à 1 mètre dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="b36d6-190">In general, 1 position unit in Unity is roughly equivalent to 1 meter in the physical world.</span></span> <span data-ttu-id="b36d6-191">Il y a cependant des exceptions à cela, par exemple quand les objets sont des enfants d’objets mis à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="b36d6-191">However, there are exceptions to this, for example, when objects are children of scaled objects.</span></span>

### <a name="2-add-a-cube-to-the-scene"></a><span data-ttu-id="b36d6-192">2. Ajouter un cube à la scène</span><span class="sxs-lookup"><span data-stu-id="b36d6-192">2. Add a cube to the scene</span></span>

<span data-ttu-id="b36d6-193">Cliquez avec le bouton droit sur un emplacement vide dans la fenêtre Hierarchy et sélectionnez **3D Object** > **Cube** pour ajouter un cube à votre scène :</span><span class="sxs-lookup"><span data-stu-id="b36d6-193">Right-click on an empty spot inside the Hierarchy window and select **3D Object** > **Cube** to add a cube to your scene:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step2-1.png)

<span data-ttu-id="b36d6-195">Avec l’objet **Cube** sélectionné, dans la fenêtre **Inspector** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-195">With the **Cube** object still selected, in the **Inspector** window:</span></span>

* <span data-ttu-id="b36d6-196">Changez la valeur **Position** de sa transformation de sorte qu’il se trouve près du bouton enfonçable, mais sans le chevaucher, par exemple x = 0, y = 0,04 et z = 0,5</span><span class="sxs-lookup"><span data-stu-id="b36d6-196">Change its Transform **Position** so its located near the pressable button, but not overlapping with it, for example, x = 0, y = 0.04, and z = 0.5</span></span>
* <span data-ttu-id="b36d6-197">Changez la valeur **Scale** de sa transformation en une taille appropriée, par exemple x = 0,02, y = 0,02 et z = 0,02</span><span class="sxs-lookup"><span data-stu-id="b36d6-197">Change its Transform **Scale** to a suitable size, for example, x = 0.02, y = 0.02, and z = 0.02</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step2-2.png)

### <a name="3-configure-the-interactableonpressreceiver-event-type"></a><span data-ttu-id="b36d6-199">3. Configurer le type d’événement InteractableOnPressReceiver</span><span class="sxs-lookup"><span data-stu-id="b36d6-199">3. Configure the InteractableOnPressReceiver event type</span></span>

<span data-ttu-id="b36d6-200">Dans la fenêtre Hierarchy, sélectionnez l’objet **PressableButtonHoloLens2** puis, dans le **menu hamburger** de la fenêtre **Inspector**, sélectionnez **Collapse All Components** pour avoir une vue d’ensemble de tous les composants sur cet objet :</span><span class="sxs-lookup"><span data-stu-id="b36d6-200">In the Hierarchy window, select the **PressableButtonHoloLens2** object, then in the **Inspector** window **hamburger menu**, select **Collapse All Components** to get an overview of all components on this object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-1.png)

<span data-ttu-id="b36d6-202">Développez le composant **Interactable (Script)** , puis localisez et développez la section **Events** > **Receivers** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-202">Expand the **Interactable (Script)** component, then locate and expand the **Events** > **Receivers** section:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-2.png)

<span data-ttu-id="b36d6-204">Cliquez sur le bouton **Add Event** pour créer un récepteur d’événements avec **InteractableOnPressReceiver** comme Event Receiver Type :</span><span class="sxs-lookup"><span data-stu-id="b36d6-204">Click the **Add Event** button, to create a new event receiver of Event Receiver Type **InteractableOnPressReceiver**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-3.png)

> [!NOTE]
> <span data-ttu-id="b36d6-206">Le Event Receiver Type nommé InteractableOnPressReceiver permet au bouton de répondre à un événement d’appui quand une main suivie appuie sur le bouton.</span><span class="sxs-lookup"><span data-stu-id="b36d6-206">The Event Receiver Type named InteractableOnPressReceiver allows the button to respond to a pressed event when a tracked hand presses the button.</span></span>

<span data-ttu-id="b36d6-207">Pour le récepteur d’événements nouvellement créé, changez **Interaction Filter** en **Near and Far** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-207">For the newly created event receiver, change the **Interaction Filter** to **Near and Far**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-4.png)

### <a name="4-configure-the-cube-to-receive-the-on-press-event"></a><span data-ttu-id="b36d6-209">4. Configurer le cube pour recevoir l’événement On Press</span><span class="sxs-lookup"><span data-stu-id="b36d6-209">4. Configure the cube to receive the On Press event</span></span>

<span data-ttu-id="b36d6-210">Dans la fenêtre Hierarchy, **cliquez et faites glisser** le **Cube** dans le champ de l’objet **Event Properties** pour l’événement **On Press ()** pour affecter le Cube comme récepteur de l’événement On Press () :</span><span class="sxs-lookup"><span data-stu-id="b36d6-210">From the Hierarchy window, **click-and-drag** the **Cube** into the **Event Properties** object field for the **On Press ()** event to assign the Cube as a receiver of the On Press () event:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step4-1.png)

### <a name="5-define-the-action-to-be-triggered-by-the-on-press-event"></a><span data-ttu-id="b36d6-212">5. Définir l’action à déclencher par l’événement On Press</span><span class="sxs-lookup"><span data-stu-id="b36d6-212">5. Define the action to be triggered by the On Press event</span></span>

<span data-ttu-id="b36d6-213">Cliquez sur la liste déroulante des actions, actuellement définie sur **No Function**, puis sélectionnez **MeshRenderer** > **Material material** pour définir la propriété Material du cube comme devant changer quand l’événement On Press () est déclenché :</span><span class="sxs-lookup"><span data-stu-id="b36d6-213">Click the action dropdown, currently assigned **No Function**, and select **MeshRenderer** > **Material material** to set the Cube's material property to be changed when the On Press () event is triggered:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-1.png)

<span data-ttu-id="b36d6-215">Cliquez sur la petite icône de **cercle** en regard du champ Material, actuellement défini sur **None (Material)** , pour ouvrir la fenêtre Select Material :</span><span class="sxs-lookup"><span data-stu-id="b36d6-215">Click the small **circle** icon next to the material field, currently populated with **None (Material)**, to open the Select Material window:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-2.png)

<span data-ttu-id="b36d6-217">Dans la fenêtre Select Material, **recherchez** **MRTK_Standard** et sélectionnez un matériau approprié, par exemple **MRTK_Standard_Cyan**, pour que la couleur du cube change en cyan quand le bouton est enfoncé :</span><span class="sxs-lookup"><span data-stu-id="b36d6-217">In the Select Material window, **search** for **MRTK_Standard** and select a suitable material, for example, **MRTK_Standard_Cyan** so the Cube's color changes to cyan when the button is pressed:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-3.png)

### <a name="6-configure-the-cube-to-receive-the-on-release-event"></a><span data-ttu-id="b36d6-219">6. Configurer le cube pour recevoir l’événement On Release</span><span class="sxs-lookup"><span data-stu-id="b36d6-219">6. Configure the cube to receive the On Release event</span></span>

<span data-ttu-id="b36d6-220">**Répétez** l’étape 4 pour l’événement On Release afin d’affecter le **Cube**  comme récepteur de l’événement **On Release ()** .</span><span class="sxs-lookup"><span data-stu-id="b36d6-220">**Repeat** Step 4 for the On Release event to assign the **Cube** as a receiver of the **On Release ()** event.</span></span>

### <a name="7-define-the-action-to-be-triggered-by-the-on-release-event"></a><span data-ttu-id="b36d6-221">7. Définir l’action à déclencher par l’événement On Release</span><span class="sxs-lookup"><span data-stu-id="b36d6-221">7. Define the action to be triggered by the On Release event</span></span>

<span data-ttu-id="b36d6-222">**Répétez** l’étape 5 pour l’événement On Release, mais choisissez le matériau **MRTK_Standard_LightGray** pour que la couleur du cube retourne à sa couleur gris clair d’origine quand le bouton est relâché :</span><span class="sxs-lookup"><span data-stu-id="b36d6-222">**Repeat** Step 5 for the On Release event, but choose the **MRTK_Standard_LightGray** material so the Cube's color returns to its original light gray color when the button is released:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step7-1.png)

### <a name="8-test-the-button-using-the-in-editor-simulation"></a><span data-ttu-id="b36d6-224">8. Tester le bouton en utilisant la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="b36d6-224">8. Test the button using the in-editor simulation</span></span>

<span data-ttu-id="b36d6-225">Appuyez sur le bouton **Play** pour entrer en mode Game et utilisez la simulation d’entrée de l’éditeur pour tester le bouton nouvellement configuré.</span><span class="sxs-lookup"><span data-stu-id="b36d6-225">Press the **Play** button to enter Game mode and use the in-editor input simulation to test your newly configured button.</span></span>

<span data-ttu-id="b36d6-226">Bouton non enfoncé (barre d’espace + molette de défilement de la souris vers l’arrière) :</span><span class="sxs-lookup"><span data-stu-id="b36d6-226">Button not pressed (spacebar + mouse scroll wheel backward):</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step8-1.png)

<span data-ttu-id="b36d6-228">Bouton enfoncé (barre d’espace + molette de défilement de la souris vers l’avant) :</span><span class="sxs-lookup"><span data-stu-id="b36d6-228">Button pressed (spacebar + mouse scroll wheel forward):</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step8-2.png)

> [!TIP]
> <span data-ttu-id="b36d6-230">Pour découvrir comment utiliser la simulation d’entrée dans l’éditeur, consultez le guide [Utilisation de la simulation d’entrée avec les mains dans l’éditeur pour tester une scène](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="b36d6-230">To learn how to use the in-editor input simulation, you can refer to the [Using the In-Editor Hand Input Simulation to test a scene](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="creating-a-panel-of-buttons-using-mrtks-grid-object-collection"></a><span data-ttu-id="b36d6-231">Création d’un panneau de boutons avec l’outil Grid Object Collection du MRTK</span><span class="sxs-lookup"><span data-stu-id="b36d6-231">Creating a panel of buttons using MRTK's Grid Object Collection</span></span>

<span data-ttu-id="b36d6-232">Dans cette section, vous allez découvrir comment aligner automatiquement plusieurs boutons dans une interface utilisateur bien ordonnée en utilisant l’outil Grid Object Collection du MRTK.</span><span class="sxs-lookup"><span data-stu-id="b36d6-232">In this section, you will learn how to automatically align multiple buttons into a neat user interface by using the MRTK's Grid Object Collection tool.</span></span>

<span data-ttu-id="b36d6-233">Cet exemple vous montre comment créer un panneau avec cinq boutons alignés horizontalement.</span><span class="sxs-lookup"><span data-stu-id="b36d6-233">This particular example will show you how to a create a panel with five buttons aligned horizontally.</span></span> <span data-ttu-id="b36d6-234">Vous pouvez cependant suivre ces mêmes principes pour créer d’autres dispositions.</span><span class="sxs-lookup"><span data-stu-id="b36d6-234">However, you may follow these same principles to create other layouts.</span></span>

<span data-ttu-id="b36d6-235">Voici les principales étapes à suivre pour y parvenir :</span><span class="sxs-lookup"><span data-stu-id="b36d6-235">The main steps you will take to achieve this are:</span></span>

1. <span data-ttu-id="b36d6-236">Rattacher les objets Button à un objet parent</span><span class="sxs-lookup"><span data-stu-id="b36d6-236">Parent the button objects to a parent object</span></span>
2. <span data-ttu-id="b36d6-237">Ajouter et configurer le composant Grid Object Collection (Script)</span><span class="sxs-lookup"><span data-stu-id="b36d6-237">Add and configure the Grid Object Collection (Script) component</span></span>
3. <span data-ttu-id="b36d6-238">Tester les boutons en utilisant la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="b36d6-238">Test the buttons using the in-editor simulation</span></span>

### <a name="1-parent-the-button-objects-to-a-parent-object"></a><span data-ttu-id="b36d6-239">1. Rattacher les objets Button à un objet parent</span><span class="sxs-lookup"><span data-stu-id="b36d6-239">1. Parent the button objects to a parent object</span></span>

<span data-ttu-id="b36d6-240">Cliquez avec le bouton droit sur un emplacement vide dans la fenêtre Hierarchy et sélectionnez **Create Empty** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-240">Right-click on an empty spot inside the Hierarchy window and select **Create Empty**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-1.png)

<span data-ttu-id="b36d6-242">Cliquez avec le bouton droit sur l’objet nouvellement créé, sélectionnez **Rename**et donnez-lui un nom approprié, par exemple **ButtonCollection** :</span><span class="sxs-lookup"><span data-stu-id="b36d6-242">Right-click on the newly created object, select **Rename**, and give it a suitable name, for example, **ButtonCollection**:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-2.png)

<span data-ttu-id="b36d6-244">Sélectionnez l’objet **PressableButtonHoloLens2** et **faites-le glisser** au-dessus de l’objet **ButtonCollection** pour en faire un enfant de l’objet ButtonCollection :</span><span class="sxs-lookup"><span data-stu-id="b36d6-244">Select the **PressableButtonHoloLens2** object and **drag** it on top of the **ButtonCollection** object to make it a child of the ButtonCollection object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-3.png)

<span data-ttu-id="b36d6-246">Cliquez avec le bouton droit sur l’objet **PressableButtonHoloLens2** et sélectionnez **Duplicate** pour en créer une copie :</span><span class="sxs-lookup"><span data-stu-id="b36d6-246">Right-click the **PressableButtonHoloLens2** object and select **Duplicate** to create a copy of it:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-4.png)

<span data-ttu-id="b36d6-248">**Répétez** cette étape quatre fois, jusqu’à avoir un total de cinq objets PressableButtonHoloLens2.</span><span class="sxs-lookup"><span data-stu-id="b36d6-248">**Repeat** this step four more times until you have a total of five PressableButtonHoloLens2 objects.</span></span>

### <a name="2-add-and-configure-the-grid-object-collection-script-component"></a><span data-ttu-id="b36d6-249">2. Ajouter et configurer le composant Grid Object Collection (Script)</span><span class="sxs-lookup"><span data-stu-id="b36d6-249">2. Add and configure the Grid Object Collection (Script) component</span></span>

<span data-ttu-id="b36d6-250">Avec l’objet ButtonCollection sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, cliquez sur le bouton **Add Component**, puis recherchez et sélectionnez **Grid Object Collection** pour ajouter un composant Grid Object Collection (Script) à l’objet ButtonCollection :</span><span class="sxs-lookup"><span data-stu-id="b36d6-250">With the ButtonCollection object selected in the Hierarchy window, in the Inspector window, click the **Add Component** button, then search for and select **Grid Object Collection** to add a Grid Object Collection (Script) component to the ButtonCollection object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-1.png)

<span data-ttu-id="b36d6-252">Configurez le composant Grid Object Collection (Script) comme suit :</span><span class="sxs-lookup"><span data-stu-id="b36d6-252">Configure the Grid Object Collection (Script) as follows:</span></span>

* <span data-ttu-id="b36d6-253">Changez **Num Rows** en 1 pour que tous les boutons soient alignés sur une même ligne</span><span class="sxs-lookup"><span data-stu-id="b36d6-253">Change **Num Rows** to 1 to have all buttons aligned on one single row</span></span>
* <span data-ttu-id="b36d6-254">Changez **Cell Width** en 0,05 pour espacer les boutons dans la ligne</span><span class="sxs-lookup"><span data-stu-id="b36d6-254">Change **Cell Width** to 0.05 to space out the buttons within the row</span></span>

<span data-ttu-id="b36d6-255">Cliquez ensuite sur le bouton **Update Collection** pour appliquer la nouvelle configuration :</span><span class="sxs-lookup"><span data-stu-id="b36d6-255">Then click the **Update Collection** button to apply the new configuration:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-2.png)

> [!NOTE]
> <span data-ttu-id="b36d6-257">Les modifications de configuration que vous venez d’appliquer représentent les modifications minimales nécessaires pour atteindre l’objectif de placer les boutons sur une même ligne.</span><span class="sxs-lookup"><span data-stu-id="b36d6-257">The configuration changes you just applied represent the minimum changes required to achieve the objective of placing the buttons in a single row.</span></span> <span data-ttu-id="b36d6-258">Cependant, dans les projets futurs, en fonction de facteurs tels que par exemple l’orientation des objets parents et enfants, vous devrez peut-être ajuster d’autres paramètres, comme par exemple le type d’orientation.</span><span class="sxs-lookup"><span data-stu-id="b36d6-258">However, in future projects, depending on factors such as, for example, the orientation of the parent and child objects, you might need to adjust other settings such as, for example, the Orient Type.</span></span> <span data-ttu-id="b36d6-259">Pour plus d’informations sur le composant Grid Object Collection de MRTK, vous pouvez consulter le guide [Object collection scripts](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html#object-collection-scripts) dans le [portail de documentation de MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="b36d6-259">To learn more about MRTK's Grid Object Collection, you can visit the [Object collection scripts](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html#object-collection-scripts) guide in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

<span data-ttu-id="b36d6-260">Avec l’objet ButtonCollection sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, changez la valeur **Position** de la transformation de l’objet ButtonCollection de sorte que ses objets de boutons enfants soient positionnés devant la caméra, qui est elle-même positionnée à l’origine, par exemple x = 0, y = 0 et z = 0,5 :</span><span class="sxs-lookup"><span data-stu-id="b36d6-260">With the ButtonCollection object still selected in the Hierarchy window, in the Inspector window, change the ButtonCollection object's Transform **Position** so its child button objects are positioned in front of the camera, which is positioned at origin, for example, x = 0, y = 0, and z = 0.5:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-3.png)

> [!NOTE]
> <span data-ttu-id="b36d6-262">Quand vous avez ajouté pour la première fois le préfabriqué PressableButtonHoloLens2 à la scène dans la section [Gestes de suivi de la main et boutons d’interaction](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) ci-dessus, vous l’avez positionné devant la caméra.</span><span class="sxs-lookup"><span data-stu-id="b36d6-262">When you first added the PressableButtonHoloLens2 prefab to the scene in the [Hand tracking gestures and interactable buttons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) section above, you positioned it in front of the camera.</span></span> <span data-ttu-id="b36d6-263">Cependant, comme Grid Object Collection contrôle la position de ses objets enfants immédiats, la position Z des objets enfants de PressableButtonHoloLens2 est réinitialisée à 0 en fonction de la distance par défaut de Grid Object Collection par rapport à la valeur 0 du parent.</span><span class="sxs-lookup"><span data-stu-id="b36d6-263">However, because the Grid Object Collection controls its immediate child objects' position, the PressableButtonHoloLens2 child objects' Z Position were reset to 0 according to the Grid Object Collection's default Distance from parent value of 0.</span></span> <span data-ttu-id="b36d6-264">C’est la raison pour laquelle, en plus de conserver la relation de position parent/enfants organisée, nous avons déplacé la position de l’objet ButtonCollection parent vers l’avant, au lieu de configurer la distance à partir de la valeur du parent pour déplacer les objets enfants PressableButtonHoloLens2 vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="b36d6-264">This, and to keep the parent/child positional relationship organized, is why we moved the parent ButtonCollection object's position forward instead of configuring the Distance from parent value to move the PressableButtonHoloLens2 child objects forward.</span></span>

### <a name="3-test-the-buttons-using-the-in-editor-simulation"></a><span data-ttu-id="b36d6-265">3. Tester les boutons en utilisant la simulation dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="b36d6-265">3. Test the buttons using the in-editor simulation</span></span>

<span data-ttu-id="b36d6-266">Appuyez sur le bouton Play pour entrer en mode Game et utilisez la simulation d’entrée de l’éditeur pour tester chacun des boutons de votre panneau de boutons nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="b36d6-266">Press the Play button to enter Game mode and use the in-editor input simulation to test each of the buttons in in your newly created panel of buttons:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step3-1.png)

> [!TIP]
> <span data-ttu-id="b36d6-268">Actuellement, quand vous appuyez sur un des cinq boutons, la couleur du cube devient cyan.</span><span class="sxs-lookup"><span data-stu-id="b36d6-268">Currently, when your press any of the five buttons, the cube color changes to cyan.</span></span> <span data-ttu-id="b36d6-269">Pour rendre l’expérience plus intéressante, utilisez ce que vous venez d’apprendre pour configurer chaque bouton pour que le cube soit affiché dans une autre différente.</span><span class="sxs-lookup"><span data-stu-id="b36d6-269">To make the experience more interesting, use what you just learn to configure each button to change the cube to a different color.</span></span>

## <a name="adding-text-into-your-scene"></a><span data-ttu-id="b36d6-270">Ajout de texte dans votre scène</span><span class="sxs-lookup"><span data-stu-id="b36d6-270">Adding text into your scene</span></span>

<span data-ttu-id="b36d6-271">Dans cette section, vous allez découvrir comment ajouter du texte à vos expériences de réalité mixte en utilisant TextMesh Pro d’Unity, que vous avez préparé dans la section [Importer les ressources essentielles TextMesh Pro](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources) du tutoriel précédent.</span><span class="sxs-lookup"><span data-stu-id="b36d6-271">In this section, you will learn how to add text to your mixed reality experiences using Unity's TextMesh Pro, which you prepared in the [Import TextMesh Pro Essential Resources](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources) section of the previous tutorial.</span></span>

<span data-ttu-id="b36d6-272">Dans cet exemple, vous allez ajouter une étiquette simple sous la collection de boutons que vous avez créée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="b36d6-272">In this particular example, you will add a simple label underneath the button collection you created in the previous section.</span></span>

<span data-ttu-id="b36d6-273">Cliquez avec le bouton droit sur l’objet ButtonCollection, puis sélectionnez **3D Object** > **Text - TextMeshPro** pour créer un objet TextMeshPro en tant qu’enfant de l’objet ButtonCollection :</span><span class="sxs-lookup"><span data-stu-id="b36d6-273">Right-click on the ButtonCollection object and select **3D Object** > **Text - TextMeshPro** to create a TextMeshPro object as a child of the ButtonCollection object:</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section4-step1-1.png)

<span data-ttu-id="b36d6-275">Sélectionnez l’objet TextMeshPro nommé Text (TMP) que vous venez de créer puis, dans la fenêtre Inspector, changez sa position et sa taille pour que l’étiquette soit placée sous la collection de boutons, par exemple :</span><span class="sxs-lookup"><span data-stu-id="b36d6-275">With the newly created TextMeshPro object, named Text (TMP), still selected, in the Inspector window change its position and size so the label is placed neatly underneath the button collection, for example:</span></span>

* <span data-ttu-id="b36d6-276">Changez la valeur **Pos Y** de Rect Transform en -0,0425.</span><span class="sxs-lookup"><span data-stu-id="b36d6-276">Change the Rect Transform **Pos Y** to -0.0425</span></span>
* <span data-ttu-id="b36d6-277">Changez la valeur **Width** de Rect Transform en 0,24.</span><span class="sxs-lookup"><span data-stu-id="b36d6-277">Change the Rect Transform **Width** to 0.24</span></span>
* <span data-ttu-id="b36d6-278">Changez la valeur **Height** de Rect Transform en 0,024.</span><span class="sxs-lookup"><span data-stu-id="b36d6-278">Change the Rect Transform **Height** to 0.024</span></span>

<span data-ttu-id="b36d6-279">Ensuite, changez le texte de façon à refléter l’objectif de l’étiquette et choisissez les propriétés de la police pour que le texte tienne dans l’étiquette, par exemple :</span><span class="sxs-lookup"><span data-stu-id="b36d6-279">Then update the text to reflect what the label is for and choose font properties so the text fits within the label, for example:</span></span>

* <span data-ttu-id="b36d6-280">Changez la valeur **Text** de Text Mesh Pro (Script) en Button Collection</span><span class="sxs-lookup"><span data-stu-id="b36d6-280">Change the Text Mesh Pro (Script) **Text** to Button Collection</span></span>
* <span data-ttu-id="b36d6-281">Changez la valeur **Font Style** de Text Mesh Pro (Script) en Bold.</span><span class="sxs-lookup"><span data-stu-id="b36d6-281">Change the Text Mesh Pro (Script) **Font Style** to Bold</span></span>
* <span data-ttu-id="b36d6-282">Changez la valeur **Font Size** de Text Mesh Pro (Script) en 0,2.</span><span class="sxs-lookup"><span data-stu-id="b36d6-282">Change the Text Mesh Pro (Script) **Font Size** to 0.2</span></span>
* <span data-ttu-id="b36d6-283">Changez la valeur **Alignment** de Text Mesh Pro (Script) en Center and Middle.</span><span class="sxs-lookup"><span data-stu-id="b36d6-283">Change the Text Mesh Pro (Script) **Alignment** to Center and Middle</span></span>

![mrlearning-base](images/mrlearning-base/tutorial2-section4-step1-2.png)

## <a name="congratulations"></a><span data-ttu-id="b36d6-285">Félicitations</span><span class="sxs-lookup"><span data-stu-id="b36d6-285">Congratulations</span></span>

<span data-ttu-id="b36d6-286">Dans ce tutoriel, vous avez découvert comment cloner, personnaliser et configurer un paramètre de profil MRTK.</span><span class="sxs-lookup"><span data-stu-id="b36d6-286">In this tutorial, you learned how to clone, customize, and configure an MRTK profile setting.</span></span> <span data-ttu-id="b36d6-287">Vous avez également découvert comment interagir avec des boutons pour déclencher des événements en utilisant des mains suivies sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="b36d6-287">You also learned how to interact with buttons to trigger events using tracked hands on the HoloLens 2.</span></span> <span data-ttu-id="b36d6-288">Enfin, vous avez découvert comment créer une interface utilisateur simple avec le composant Grid Object Collection du MRTK et le Text Mesh Pro d’Unity.</span><span class="sxs-lookup"><span data-stu-id="b36d6-288">Finally, you learned how to create a simple UI interface using the MRTK's Grid Object Collection component and Unity's Text Mesh Pro.</span></span>

[<span data-ttu-id="b36d6-289">Tutoriel suivant : 4. Placement du contenu dynamique et utilisation de solveurs</span><span class="sxs-lookup"><span data-stu-id="b36d6-289">Next Tutorial: 4. Placing dynamic content and using solvers</span></span>](mrlearning-base-ch3.md)
