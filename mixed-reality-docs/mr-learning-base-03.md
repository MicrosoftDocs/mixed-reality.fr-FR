---
title: Tutoriels de démarrage - 3. Configuration des profils MRTK
description: Ce cours vous montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 2c413964a435814275a1b908770ca977412f92be
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86305772"
---
# <a name="3-configuring-the-mrtk-profiles"></a><span data-ttu-id="c865f-105">3. Configuration des profils MRTK</span><span class="sxs-lookup"><span data-stu-id="c865f-105">3. Configuring the MRTK profiles</span></span>

## <a name="overview"></a><span data-ttu-id="c865f-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="c865f-106">Overview</span></span>

<span data-ttu-id="c865f-107">Dans ce tutoriel, vous allez voir comment personnaliser et configurer les profils MRTK.</span><span class="sxs-lookup"><span data-stu-id="c865f-107">In this tutorial, you will learn how to customize and configure the MRTK profiles.</span></span>

<span data-ttu-id="c865f-108">Cet exemple va vous montrer comment masquer le maillage de la reconnaissance spatiale en modifiant les paramètres de l’observateur de maillage spatial.</span><span class="sxs-lookup"><span data-stu-id="c865f-108">This particular example will show you how to hide the spatial awareness mesh by changing the settings of the Spatial Mesh Observer.</span></span> <span data-ttu-id="c865f-109">Vous pouvez cependant suivre ces mêmes principes pour personnaliser des paramètres ou des valeurs dans les profils MRTK.</span><span class="sxs-lookup"><span data-stu-id="c865f-109">However, you may follow these same principles to customize any setting or value in the MRTK profiles.</span></span>

## <a name="objectives"></a><span data-ttu-id="c865f-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="c865f-110">Objectives</span></span>

* <span data-ttu-id="c865f-111">Apprendre à personnaliser et à configurer des profils MRTK</span><span class="sxs-lookup"><span data-stu-id="c865f-111">Learn how to customize and configure MRTK profiles</span></span>
* <span data-ttu-id="c865f-112">Apprendre à masquer le maillage de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="c865f-112">Hide the spatial awareness mesh</span></span>

## <a name="changing-the-spatial-awareness-display-option"></a><span data-ttu-id="c865f-113">Changement de l’option d’affichage de la reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="c865f-113">Changing the Spatial Awareness Display Option</span></span>

<span data-ttu-id="c865f-114">Les principales étapes à suivre pour masquer le maillage de la reconnaissance spatiale sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="c865f-114">The main steps you will take to hide the spatial awareness mesh are:</span></span>

1. <span data-ttu-id="c865f-115">Cloner le profil de configuration par défaut</span><span class="sxs-lookup"><span data-stu-id="c865f-115">Clone the default Configuration Profile</span></span>
2. <span data-ttu-id="c865f-116">Activer le système de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="c865f-116">Enable the Spatial Awareness System</span></span>
3. <span data-ttu-id="c865f-117">Cloner le profil système de reconnaissance spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="c865f-117">Clone the default Spatial Awareness System Profile</span></span>
4. <span data-ttu-id="c865f-118">Cloner le profil d’observateur de maillage de reconnaissance spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="c865f-118">Clone the default Spatial Awareness Mesh Observer Profile</span></span>
5. <span data-ttu-id="c865f-119">Changer la visibilité du maillage de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="c865f-119">Change the visibility of the spatial awareness mesh</span></span>

> [!NOTE]
> <span data-ttu-id="c865f-120">Par défaut, les profils MRTK ne sont pas modifiables.</span><span class="sxs-lookup"><span data-stu-id="c865f-120">By default, the MRTK profiles are not editable.</span></span> <span data-ttu-id="c865f-121">Il s’agit des modèles de profil par défaut que vous devez cloner avant de pouvoir les modifier.</span><span class="sxs-lookup"><span data-stu-id="c865f-121">These are default profile templates that you have to clone before they can be edited.</span></span> <span data-ttu-id="c865f-122">Il existe plusieurs couches de profils imbriquées.</span><span class="sxs-lookup"><span data-stu-id="c865f-122">There are several nested layers of profiles.</span></span> <span data-ttu-id="c865f-123">Par conséquent, il est courant de cloner et de modifier plusieurs profils lors de la configuration d’un ou plusieurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="c865f-123">Therefore, it is common to clone and edit several profiles when configuring one or more settings.</span></span>

### <a name="1-clone-the-default-configuration-profile"></a><span data-ttu-id="c865f-124">1. Cloner le profil de configuration par défaut</span><span class="sxs-lookup"><span data-stu-id="c865f-124">1. Clone the default Configuration Profile</span></span>

> [!NOTE]
> <span data-ttu-id="c865f-125">Le profil de configuration est le profil de plus haut niveau.</span><span class="sxs-lookup"><span data-stu-id="c865f-125">The Configuration Profile is the top-level profile.</span></span> <span data-ttu-id="c865f-126">Par conséquent, pour pouvoir modifier d’autres profils, vous devez d’abord cloner le profil de configuration.</span><span class="sxs-lookup"><span data-stu-id="c865f-126">Consequently, to be able to edit any other profiles, you first have to clone the Configuration Profile.</span></span>

<span data-ttu-id="c865f-127">Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit**, puis, dans la fenêtre Inspector, remplacez le profil de configuration **MixedRealityToolkit** par **DefaultHoloLens2ConfigurationProfile** :</span><span class="sxs-lookup"><span data-stu-id="c865f-127">In the Hierarchy window, select the **MixedRealityToolkit** object, then in the Inspector window, change the **MixedRealityToolkit** Configuration Profile to the **DefaultHoloLens2ConfigurationProfile**:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step1-1.png)

<span data-ttu-id="c865f-129">Avec l’objet **MixedRealityToolkit** sélectionné, dans la fenêtre Inspector, cliquez sur le bouton **Copy & Customize** pour ouvrir la fenêtre Clone Profile :</span><span class="sxs-lookup"><span data-stu-id="c865f-129">With the **MixedRealityToolkit** object still selected, in the Inspector window, click the **Copy & Customize** button to open the Clone Profile window:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step1-2.png)

<span data-ttu-id="c865f-131">Dans la fenêtre Clone Profile, en regard de **Profile Name**, entrez un nom de profil adapté comme _GettingStarted_HoloLens2ConfigurationProfile_, puis cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultHololens2ConfigurationProfile** :</span><span class="sxs-lookup"><span data-stu-id="c865f-131">In the Clone Profile window, enter a suitable **Profile Name**, for example, _GettingStarted_HoloLens2ConfigurationProfile_, then click the **Clone** button to create an editable copy of the **DefaultHololens2ConfigurationProfile**:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step1-3.png)

<span data-ttu-id="c865f-133">Le profil de configuration que vous venez de créer est maintenant affecté comme profil de configuration pour votre scène :</span><span class="sxs-lookup"><span data-stu-id="c865f-133">The newly created Configuration Profile is now assigned as the Configuration Profile for your scene:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step1-4.png)

<span data-ttu-id="c865f-135">Dans le menu Unity, sélectionnez **File** > **Save** pour enregistrer votre scène.</span><span class="sxs-lookup"><span data-stu-id="c865f-135">In the Unity menu, select **File** > **Save** to save your scene.</span></span>

> [!TIP]
> <span data-ttu-id="c865f-136">N’oubliez pas d’enregistrer votre travail tout au long des tutoriels.</span><span class="sxs-lookup"><span data-stu-id="c865f-136">Remember to save your work throughout the tutorials.</span></span>

### <a name="2-enable-the-spatial-awareness-system"></a><span data-ttu-id="c865f-137">2. Activer le système de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="c865f-137">2. Enable the Spatial Awareness System</span></span>

<span data-ttu-id="c865f-138">Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit**. Ensuite, dans la fenêtre Inspector, sélectionnez l’onglet **Spatial Awareness**, puis cochez la case **Enable Spatial Awareness System** :</span><span class="sxs-lookup"><span data-stu-id="c865f-138">In the Hierarchy window, select the **MixedRealityToolkit** object, then in the Inspector window, select the **Spatial Awareness** tab, and then check the **Enable Spatial Awareness System** checkbox:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step2-1.png)

### <a name="3-clone-the-default-spatial-awareness-system-profile"></a><span data-ttu-id="c865f-140">3. Cloner le profil système de reconnaissance spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="c865f-140">3. Clone the default Spatial Awareness System Profile</span></span>

<span data-ttu-id="c865f-141">Sous l’onglet **Spatial Awareness**, cliquez sur le bouton **Clone** pour ouvrir la fenêtre Clone Profile :</span><span class="sxs-lookup"><span data-stu-id="c865f-141">In the **Spatial Awareness** tab, click the **Clone** button to open the Clone Profile window:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step3-1.png)

<span data-ttu-id="c865f-143">Dans la fenêtre Clone Profile, en regard de **Profile Name**, entrez un nom de profil adapté comme _GettingStarted_MixedRealitySpatialAwarenessSystemProfile_, puis cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultMixedRealitySpatialAwarenessSystemProfile** :</span><span class="sxs-lookup"><span data-stu-id="c865f-143">In the Clone Profile window, enter a suitable **Profile Name**, for example, _GettingStarted_MixedRealitySpatialAwarenessSystemProfile_, then click the **Clone** button to create an editable copy of the **DefaultMixedRealitySpatialAwarenessSystemProfile**:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step3-2.png)

<span data-ttu-id="c865f-145">Le profil Spatial Awareness System nouvellement créé est maintenant automatiquement affecté à votre profil de configuration :</span><span class="sxs-lookup"><span data-stu-id="c865f-145">The newly created Spatial Awareness System Profile is now automatically assigned to your Configuration Profile:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step3-3.png)

### <a name="4-clone-the-default-spatial-awareness-mesh-observer-profile"></a><span data-ttu-id="c865f-147">4. Cloner le profil d’observateur de maillage de reconnaissance spatiale par défaut</span><span class="sxs-lookup"><span data-stu-id="c865f-147">4. Clone the default Spatial Awareness Mesh Observer Profile</span></span>

<span data-ttu-id="c865f-148">Avec l’onglet **Spatial Awareness** sélectionné, développez la section **Windows Mixed Reality Spatial Mesh Observer**, puis cliquez sur le bouton **Clone** pour ouvrir la fenêtre Clone Profile :</span><span class="sxs-lookup"><span data-stu-id="c865f-148">With the **Spatial Awareness** tab still selected, expand the **Windows Mixed Reality Spatial Mesh Observer** section, then click the **Clone** button to open the Clone Profile window:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step4-1.png)

<span data-ttu-id="c865f-150">Dans la fenêtre Clone Profile, en regard de **Profile Name**, entrez un nom de profil adapté comme _GettingStarted_MixedRealitySpatialAwarenessMeshObserverProfile_, puis cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultMixedRealitySpatialAwarenessMeshObserverProfile** :</span><span class="sxs-lookup"><span data-stu-id="c865f-150">In the Clone Profile window, enter a suitable **Profile Name**, for example, _GettingStarted_MixedRealitySpatialAwarenessMeshObserverProfile_, then click the **Clone** button to create an editable copy of the **DefaultMixedRealitySpatialAwarenessMeshObserverProfile**:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step4-2.png)

<span data-ttu-id="c865f-152">Le profil Spatial Awareness Mesh Observer nouvellement créé est maintenant automatiquement affecté à votre profil Spatial Awareness System :</span><span class="sxs-lookup"><span data-stu-id="c865f-152">The newly created Spatial Awareness Mesh Observer Profile is now automatically assigned to your Spatial Awareness System Profile:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step4-3.png)

### <a name="5-change-the-visibility-of-the-spatial-awareness-mesh"></a><span data-ttu-id="c865f-154">5. Changer la visibilité du maillage de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="c865f-154">5. Change the visibility of the spatial awareness mesh</span></span>

<span data-ttu-id="c865f-155">Dans **Spatial Mesh Observer Settings**, configurez **Display Option** sur **Occlusion** pour rendre le maillage de mappage spatial invisible tout en le gardant fonctionnel :</span><span class="sxs-lookup"><span data-stu-id="c865f-155">In the **Spatial Mesh Observer Settings**, change the **Display Option** to **Occlusion** to make the spatial mapping mesh invisible while still functional:</span></span>

![mr-learning-base](images/mr-learning-base/base-03-section1-step5-1.png)

> [!NOTE]
> <span data-ttu-id="c865f-157">Bien que le maillage de mappage spatial ne soit pas visible, il est toujours présent et fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="c865f-157">Although the spatial mapping mesh is not visible, it is still present and functional.</span></span> <span data-ttu-id="c865f-158">Par exemple, les hologrammes qui sont derrière le maillage de mappage spatial, comme un hologramme derrière un mur physique, ne sont pas visibles.</span><span class="sxs-lookup"><span data-stu-id="c865f-158">For example, any holograms behind the spatial mapping mesh, such as a hologram behind a physical wall, will not be visible.</span></span>

<span data-ttu-id="c865f-159">Vous venez de découvrir comment modifier un paramètre dans le profil MRTK.</span><span class="sxs-lookup"><span data-stu-id="c865f-159">You just learned how to modify a setting in the MRTK profile.</span></span> <span data-ttu-id="c865f-160">Comme vous pouvez le voir, pour personnaliser les paramètres du MRTK, vous devez d’abord créer une copie des profils par défaut.</span><span class="sxs-lookup"><span data-stu-id="c865f-160">As you can see, to customize the MRTK settings, you first need to create copies of the default profiles.</span></span> <span data-ttu-id="c865f-161">Étant donné que les profils par défaut ne sont pas modifiables, vous les aurez toujours comme référence si vous voulez rétablir les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="c865f-161">Because the default profiles are not editable, you will always have them as references if you want to revert to the default settings.</span></span> <span data-ttu-id="c865f-162">Pour plus d’informations sur les profils MRTK et leur architecture, vous pouvez consulter le [Guide de configuration du profil MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span><span class="sxs-lookup"><span data-stu-id="c865f-162">To learn more about MRTK profiles and their architecture, you can refer to the [MRTK profile configuration guide](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) in the [MRTK Documentation Portal](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).</span></span>

## <a name="congratulations"></a><span data-ttu-id="c865f-163">Félicitations</span><span class="sxs-lookup"><span data-stu-id="c865f-163">Congratulations</span></span>

<span data-ttu-id="c865f-164">Dans ce tutoriel, vous avez vu comment cloner, personnaliser et configurer les profils et les paramètres MRTK.</span><span class="sxs-lookup"><span data-stu-id="c865f-164">In this tutorial, you learned how to clone, customize, and configure MRTK profiles and settings.</span></span>

[<span data-ttu-id="c865f-165">Tutoriel suivant : 4. Positionnement des objets dans la scène</span><span class="sxs-lookup"><span data-stu-id="c865f-165">Next Tutorial: 4. Positioning objects in the scene</span></span>](mr-learning-base-04.md)
