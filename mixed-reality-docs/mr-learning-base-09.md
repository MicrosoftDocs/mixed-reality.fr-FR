---
title: Tutoriels de démarrage - 9. Utilisation des commandes vocales
description: Ce cours montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: b0b9771d9569d100a354af96a34cd20ef2a3d7c4
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376591"
---
# <a name="9-using-speech-commands"></a><span data-ttu-id="7248e-105">9. Utilisation des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="7248e-105">9. Using speech commands</span></span>

## <a name="overview"></a><span data-ttu-id="7248e-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="7248e-106">Overview</span></span>

<span data-ttu-id="7248e-107">Dans ce tutoriel, vous allez apprendre à créer des commandes vocales et à les contrôler globalement.</span><span class="sxs-lookup"><span data-stu-id="7248e-107">In this tutorial, you will learn how to create speech commands and how to control them globally.</span></span> <span data-ttu-id="7248e-108">Vous allez également apprendre à contrôler les commandes vocales locales qui demandent à l’utilisateur de regarder l’objet qui contrôle la commande vocale.</span><span class="sxs-lookup"><span data-stu-id="7248e-108">You will also learn how to control local speech commands that require the user to look at the object that controls the speech command.</span></span>

## <a name="objectives"></a><span data-ttu-id="7248e-109">Objectifs</span><span class="sxs-lookup"><span data-stu-id="7248e-109">Objectives</span></span>

* <span data-ttu-id="7248e-110">Apprendre à créer des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="7248e-110">Learn how to create speech commands</span></span>
* <span data-ttu-id="7248e-111">Apprendre à contrôler les commandes vocales globalement et localement</span><span class="sxs-lookup"><span data-stu-id="7248e-111">Learn how to control speech commands globally and locally</span></span>

## <a name="ensuring-the-microphone-capability-is-enabled"></a><span data-ttu-id="7248e-112">Vérification de l’activation de la fonctionnalité Microphone</span><span class="sxs-lookup"><span data-stu-id="7248e-112">Ensuring the Microphone capability is enabled</span></span>

<span data-ttu-id="7248e-113">Dans le menu Unity, sélectionnez Mixed Reality Toolkit > Utilities > **Configure Unity Project** pour ouvrir la fenêtre **MRTK Project Configurator** puis, dans la section **UWP Capabilities**, vérifiez que l’option **Enable Microphone Capability** est grisée :</span><span class="sxs-lookup"><span data-stu-id="7248e-113">In the Unity menu, select Mixed Reality Toolkit > Utilities > **Configure Unity Project** to open the **MRTK Project Configurator** window, then in the **UWP Capabilities** section, verify that **Enable Microphone Capability** is greyed out:</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section1-step1-1.png)

> [!NOTE]
> <span data-ttu-id="7248e-115">La fonctionnalité Microphone doit avoir été activée lors des instructions [Appliquer les paramètres de MRTK Project Configurator](mr-learning-base-02.md#1-apply-the-mrtk-project-configurator-settings) lorsque vous avez configuré le projet Unity au début de cette série de tutoriels.</span><span class="sxs-lookup"><span data-stu-id="7248e-115">The Microphone capability should have been enabled during the [Apply the MRTK Project Configurator settings](mr-learning-base-02.md#1-apply-the-mrtk-project-configurator-settings) instructions when you configured the Unity project at the beginning of this tutorial series.</span></span> <span data-ttu-id="7248e-116">Toutefois, si elle n’est pas activée, veillez à l’activer maintenant.</span><span class="sxs-lookup"><span data-stu-id="7248e-116">However, if it is not enabled, make sure you enable it now.</span></span>

## <a name="creating-speech-commands"></a><span data-ttu-id="7248e-117">Création de commandes vocales</span><span class="sxs-lookup"><span data-stu-id="7248e-117">Creating speech commands</span></span>

<span data-ttu-id="7248e-118">Dans la fenêtre de hiérarchie, sélectionnez l’objet **MixedRealityToolkit** puis, dans la fenêtre de l’inspecteur, sélectionnez l’onglet MixedRealityToolkit > **Input** et effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7248e-118">In the Hierarchy window, select the **MixedRealityToolkit** object, then in the Inspector window, select the MixedRealityToolkit > **Input** tab and take the following steps:</span></span>

* <span data-ttu-id="7248e-119">Développez la section **Speech**.</span><span class="sxs-lookup"><span data-stu-id="7248e-119">Expand the **Speech** section</span></span>
* <span data-ttu-id="7248e-120">Clonez le **DefaultMixedRealitySpeechCommandsProfile** et donnez-lui un nom approprié, par exemple _GettingStarted_MixedRealitySpeechCommandsProfile_.</span><span class="sxs-lookup"><span data-stu-id="7248e-120">Clone the **DefaultMixedRealitySpeechCommandsProfile** and give it a suitable name, for example, _GettingStarted_MixedRealitySpeechCommandsProfile_</span></span>
* <span data-ttu-id="7248e-121">Vérifiez que **Start Behaviour** (Comportement de démarrage) est défini sur **Auto Start** (Démarrage automatique).</span><span class="sxs-lookup"><span data-stu-id="7248e-121">Verify that **Start Behaviour** is set to **Auto Start**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section2-step1-1.png)

> [!TIP]
> <span data-ttu-id="7248e-123">Pour vous rappeler comment cloner des profils MRTK, vous pouvez consulter les instructions fournies dans [Configuration des profils MRTK](mr-learning-base-03.md).</span><span class="sxs-lookup"><span data-stu-id="7248e-123">For a reminder on how to clone MRTK profiles, you can refer to the [Configuring the MRTK profiles](mr-learning-base-03.md) instructions.</span></span>

<span data-ttu-id="7248e-124">Dans la section Speech > **Speech Commands**, cliquez à quatre reprises sur le bouton **+ Add a New Speech Command** (Ajouter une commande vocale) pour ajouter quatre nouvelles commandes vocales à la liste des commandes vocales existantes puis, dans le champ **Keyword** (Mot clé), entrez les expressions suivantes :</span><span class="sxs-lookup"><span data-stu-id="7248e-124">In the Speech > **Speech Commands** section, click the **+ Add a New Speech Command** button four times to add four new speech commands to the list of the existing speech commands, then in the **Keyword** fields enter the following phrases:</span></span>

* <span data-ttu-id="7248e-125">Activer l’indicateur</span><span class="sxs-lookup"><span data-stu-id="7248e-125">Enable Indicator</span></span>
* <span data-ttu-id="7248e-126">Activer l’appui pour placement</span><span class="sxs-lookup"><span data-stu-id="7248e-126">Enable Tap to Place</span></span>
* <span data-ttu-id="7248e-127">Activer le cadre englobant</span><span class="sxs-lookup"><span data-stu-id="7248e-127">Enable Bounding Box</span></span>
* <span data-ttu-id="7248e-128">Désactiver le cadre englobant</span><span class="sxs-lookup"><span data-stu-id="7248e-128">Disable Bounding Box</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section2-step1-2.png)

> [!TIP]
> <span data-ttu-id="7248e-130">Si votre ordinateur ne dispose pas d’un microphone, vous pouvez affecter un code-clé aux commandes vocales, ce qui vous permettra de les déclencher lorsque vous appuierez sur la touche correspondante.</span><span class="sxs-lookup"><span data-stu-id="7248e-130">If your computer does not have a microphone you can assign a KeyCode to the speech commands, which will let you trigger them when the corresponding key is pressed.</span></span>

## <a name="controlling-speech-commands"></a><span data-ttu-id="7248e-131">Contrôle des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="7248e-131">Controlling speech commands</span></span>

<span data-ttu-id="7248e-132">Dans la Project projet, accédez au dossier **Assets** > **MRTK** > **SDK** > **Features** > **UX** > **Prefabs** > **ToolTip** pour localiser les préfabriqués d’info-bulle :</span><span class="sxs-lookup"><span data-stu-id="7248e-132">In the Project window, navigate to the **Assets** > **MRTK** > **SDK** > **Features** > **UX** > **Prefabs** > **ToolTip** folder to locate the tooltip prefabs:</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-1.png)

<span data-ttu-id="7248e-134">Dans la fenêtre de hiérarchie, cliquez avec le bouton droit sur une zone vide et sélectionnez **Create Empty** pour ajouter un objet vide à votre scène.</span><span class="sxs-lookup"><span data-stu-id="7248e-134">In the Hierarchy window, right-click on an empty spot and select **Create Empty** to add an empty object to your scene.</span></span>

<span data-ttu-id="7248e-135">Nommez l’objet **SpeechInputHandler_Global** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** pour ajouter le composant **SpeechInputHandler** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="7248e-135">Name the object **SpeechInputHandler_Global**, then in the Inspector window, use the **Add Component** button to add the **SpeechInputHandler** component and configure it as follows:</span></span>

* <span data-ttu-id="7248e-136">**Décochez** la case **Is Focus Required** afin que l’utilisateur ne soit pas obligé de regarder l’objet avec le composant SpeechInputHandler pour déclencher la commande vocale.</span><span class="sxs-lookup"><span data-stu-id="7248e-136">**Uncheck** the **Is Focus Required** checkbox, so the user is not required to look at the object with the SpeechInputHandler component to trigger the speech command</span></span>
* <span data-ttu-id="7248e-137">À partir de la fenêtre Project, affectez le préfabriqué **SpeechConfirmation Tooltip** au champ **Speech Confirmation Tooltip Prefab** (Préfabriqué d’info-bulle de confirmation vocale) afin que ce préfabriqué s’affiche quand une commande vocale est reconnue.</span><span class="sxs-lookup"><span data-stu-id="7248e-137">From the Project window, assign the **SpeechConfirmation Tooltip** prefab to the **Speech Confirmation Tooltip Prefab** field, to have this prefab appear when a speech command is recognized</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-2.png)

<span data-ttu-id="7248e-139">Sur le composant SpeechInputHandler, cliquez trois fois sur la petite icône **+** pour ajouter trois éléments de mot clé :</span><span class="sxs-lookup"><span data-stu-id="7248e-139">On the SpeechInputHandler component, click the small **+** icon three times to add three keyword elements:</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-3.png)

<span data-ttu-id="7248e-141">Développez **Element 0** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="7248e-141">Expand **Element 0** and configure it as follows:</span></span>

* <span data-ttu-id="7248e-142">Dans le champ **Keyword**, entrez **Activer l’indicateur** afin de référencer la commande vocale Activer l’indicateur que vous avez créée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="7248e-142">In the **Keyword** field, enter **Enable Indicator**, to reference the Enable Indicator speech command you created in the previous section</span></span>
* <span data-ttu-id="7248e-143">Cliquez sur la petite icône **+** pour ajouter un événement.</span><span class="sxs-lookup"><span data-stu-id="7248e-143">Click the small **+** icon to add an event</span></span>
* <span data-ttu-id="7248e-144">Dans la fenêtre de hiérarchie, affectez l’objet **Indicator** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="7248e-144">From the Hierarchy window, assign the **Indicator** object to the **None (Object)** field</span></span>
* <span data-ttu-id="7248e-145">Dans la liste déroulante **No Function**, sélectionnez **GameObject** > **SetActive (bool)** pour définir cette fonction en tant qu’action à exécuter lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="7248e-145">From the **No Function** dropdown, select **GameObject** > **SetActive (bool)** to set this function as the action to be executed when the event is triggered</span></span>
* <span data-ttu-id="7248e-146">**Cochez** la case de l’argument.</span><span class="sxs-lookup"><span data-stu-id="7248e-146">Check the argument checkbox, so it is **checked**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-4.png)

<span data-ttu-id="7248e-148">Développez **Element 1** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="7248e-148">Expand **Element 1** and configure it as follows:</span></span>

* <span data-ttu-id="7248e-149">Dans le champ **Keyword**, entrez **Activer le cadre englobant** afin de référencer la commande vocale Activer le cadre englobant que vous avez créée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="7248e-149">In the **Keyword** field, enter **Enable Bounding Box**, to reference the Enable Bounding Box command you created in the previous section</span></span>
* <span data-ttu-id="7248e-150">Cliquez sur la petite icône **+** pour ajouter un événement.</span><span class="sxs-lookup"><span data-stu-id="7248e-150">Click the small **+** icon to add an event</span></span>
* <span data-ttu-id="7248e-151">Dans la fenêtre de hiérarchie, affectez l’objet **RoverExplorer** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="7248e-151">From the Hierarchy window, assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="7248e-152">Dans la liste déroulante **No Function**, sélectionnez **BoundingBox** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="7248e-152">From the **No Function** dropdown, select **BoundingBox** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="7248e-153">**Cochez** la case de l’argument.</span><span class="sxs-lookup"><span data-stu-id="7248e-153">Check the argument checkbox, so it is **checked**</span></span>
* <span data-ttu-id="7248e-154">Cliquez sur la petite icône **+** pour ajouter un autre événement.</span><span class="sxs-lookup"><span data-stu-id="7248e-154">Click the small **+** icon to add another event</span></span>
* <span data-ttu-id="7248e-155">Dans la fenêtre de hiérarchie, affectez l’objet **RoverExplorer** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="7248e-155">From the Hierarchy window, assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="7248e-156">Dans la liste déroulante **No Function**, sélectionnez **ObjectManipulator** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="7248e-156">From the **No Function** dropdown, select **ObjectManipulator** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="7248e-157">**Cochez** la case de l’argument.</span><span class="sxs-lookup"><span data-stu-id="7248e-157">Check the argument checkbox, so it is **checked**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-5.png)

<span data-ttu-id="7248e-159">Développez **Element 2** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="7248e-159">Expand **Element 2** and configure it as follows:</span></span>

* <span data-ttu-id="7248e-160">Dans le champ **Keyword**, entrez **Désactiver le cadre englobant** afin de référencer la commande vocale Désactiver le cadre englobant que vous avez créée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="7248e-160">In the **Keyword** field, enter **Disable Bounding Box**, to reference the Disable Bounding Box command you created in the previous section</span></span>
* <span data-ttu-id="7248e-161">Cliquez sur la petite icône **+** pour ajouter un événement.</span><span class="sxs-lookup"><span data-stu-id="7248e-161">Click the small **+** icon to add an event</span></span>
* <span data-ttu-id="7248e-162">Dans la fenêtre de hiérarchie, affectez l’objet **RoverExplorer** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="7248e-162">From the Hierarchy window, assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="7248e-163">Dans la liste déroulante **No Function**, sélectionnez **BoundingBox** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="7248e-163">From the **No Function** dropdown, select **BoundingBox** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="7248e-164">Vérifiez que la case de l’argument est **décochée**.</span><span class="sxs-lookup"><span data-stu-id="7248e-164">Verify that the argument checkbox is **unchecked**</span></span>
* <span data-ttu-id="7248e-165">Cliquez sur la petite icône **+** pour ajouter un autre événement.</span><span class="sxs-lookup"><span data-stu-id="7248e-165">Click the small **+** icon to add another event</span></span>
* <span data-ttu-id="7248e-166">Dans la fenêtre de hiérarchie, affectez l’objet **RoverExplorer** au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="7248e-166">From the Hierarchy window, assign the **RoverExplorer** object to the **None (Object)** field</span></span>
* <span data-ttu-id="7248e-167">Dans la liste déroulante **No Function**, sélectionnez **ObjectManipulator** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="7248e-167">From the **No Function** dropdown, select **ObjectManipulator** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="7248e-168">Vérifiez que la case de l’argument est **décochée**.</span><span class="sxs-lookup"><span data-stu-id="7248e-168">Verify that the argument checkbox is **unchecked**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-6.png)

<span data-ttu-id="7248e-170">Dans la fenêtre de hiérarchie, sélectionnez l’objet RoverExplorer > **RoverAssembly** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** pour ajouter le composant **SpeechInputHandler** et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="7248e-170">In the Hierarchy window, select the RoverExplorer > **RoverAssembly** object, then in the Inspector window, use the **Add Component** button to add the **SpeechInputHandler** component and configure it as follows:</span></span>

* <span data-ttu-id="7248e-171">Vérifiez que la case **Is Focus Required** est **cochée** afin que l’utilisateur ne soit pas obligé de regarder l’objet avec le composant SpeechInputHandler (autrement dit, RoverAssembly) pour déclencher la commande vocale.</span><span class="sxs-lookup"><span data-stu-id="7248e-171">Verify that the **Is Focus Required** checkbox is **check**, so the user is required to look at the object with the SpeechInputHandler component, i.e., the RoverAssembly, to trigger the speech command</span></span>
* <span data-ttu-id="7248e-172">À partir de la fenêtre Project, affectez le préfabriqué **SpeechConfirmation Tooltip** au champ **Speech Confirmation Tooltip Prefab** (Préfabriqué d’info-bulle de confirmation vocale) afin que ce préfabriqué s’affiche quand une commande vocale est reconnue.</span><span class="sxs-lookup"><span data-stu-id="7248e-172">From the Project window, assign the **SpeechConfirmation Tooltip** prefab to the **Speech Confirmation Tooltip Prefab** field, to have this prefab appear when a speech command is recognized</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-7.png)

<span data-ttu-id="7248e-174">Sur le composant SpeechInputHandler, cliquez sur la petite icône **+** pour ajouter un élément Keyword, développez l’élément qui vient d’être créé, puis configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="7248e-174">On the SpeechInputHandler component, click the small **+** icon to add a keyword element, expand the newly created element, then configure it as follows:</span></span>

* <span data-ttu-id="7248e-175">Dans le champ **Keyword**, entrez **Activer l’appui pour placement** afin de référencer la commande vocale Activer l’appui pour placement que vous avez créée dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="7248e-175">In the **Keyword** field, enter **Enable Tap to Place**, to reference the Enable Tap to Place command you created in the previous section</span></span>
* <span data-ttu-id="7248e-176">Cliquez sur la petite icône **+** pour ajouter un événement.</span><span class="sxs-lookup"><span data-stu-id="7248e-176">Click the small **+** icon to add an event</span></span>
* <span data-ttu-id="7248e-177">Dans la fenêtre de hiérarchie, assignez l’objet lui-même, c’est-à-dire le même objet **RoverAssembly**, au champ **None (Object)** .</span><span class="sxs-lookup"><span data-stu-id="7248e-177">From the Hierarchy window, assign the object itself, i.e., the same **RoverAssembly** object, to the **None (Object)** field</span></span>
* <span data-ttu-id="7248e-178">Dans la liste déroulante **No Function**, sélectionnez **TapToPlace** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="7248e-178">From the **No Function** dropdown, select **TapToPlace** > **bool enabled** to update this property value when the event is triggered</span></span>
* <span data-ttu-id="7248e-179">**Cochez** la case de l’argument.</span><span class="sxs-lookup"><span data-stu-id="7248e-179">Check the argument checkbox, so it is **checked**</span></span>

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-8.png)

## <a name="congratulations"></a><span data-ttu-id="7248e-181">Félicitations</span><span class="sxs-lookup"><span data-stu-id="7248e-181">Congratulations</span></span>

<span data-ttu-id="7248e-182">Dans ce tutoriel, vous avez appris à créer des commandes vocales et à les contrôler globalement.</span><span class="sxs-lookup"><span data-stu-id="7248e-182">In this tutorial, you learned how to create speech commands and how to control them globally.</span></span> <span data-ttu-id="7248e-183">Vous avez également appris à contrôler les commandes vocales locales qui demandent à l’utilisateur de regarder l’objet qui contrôle la commande vocale.</span><span class="sxs-lookup"><span data-stu-id="7248e-183">You also learned how to control local speech commands that require the user to look at the object that controls the speech command.</span></span>

<span data-ttu-id="7248e-184">Cela conclut également la série de [Tutoriels de démarrage](mr-learning-base-01.md).</span><span class="sxs-lookup"><span data-stu-id="7248e-184">This also concludes the [Getting started tutorials](mr-learning-base-01.md) series.</span></span> <span data-ttu-id="7248e-185">En suivant ces tutoriels, vous avez réussi à créer une expérience de réalité mixte complète à l’aide de MRTK.</span><span class="sxs-lookup"><span data-stu-id="7248e-185">Through these tutorials, you have successfully built a complete mixed reality experience from scratch using the MRTK.</span></span>

<span data-ttu-id="7248e-186">Dans les deux prochaines séries de tutoriels, [Tutoriels Azure Spatial Anchors](mr-learning-asa-01.md) et [Tutoriels sur les fonctionnalités multiutilisateurs](mr-learning-sharing-01.md), vous allez d’abord apprendre à intégrer Azure Spatial Anchors dans votre projet afin d’ancrer l’expérience Rover Explorer que vous avez créée dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="7248e-186">In the next two tutorial series, [Azure Spatial Anchors tutorials](mr-learning-asa-01.md) and [Multi-user capabilities tutorials](mr-learning-sharing-01.md), you will first learn how to integrate Azure Spatial Anchors into your project to anchor the Rover Explorer experience you created in the real world.</span></span> <span data-ttu-id="7248e-187">Ensuite, vous apprendrez à ajouter des fonctionnalités multiutilisateurs à votre projet afin de partager des mouvements d’utilisateur et d’objet en temps réel.</span><span class="sxs-lookup"><span data-stu-id="7248e-187">Then, you will learn how to add multi-user capabilities to your project to share user and object movements in real-time.</span></span>
