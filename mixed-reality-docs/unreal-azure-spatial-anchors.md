---
title: Azure Spatial Anchors dans Unreal
description: Vue d’ensemble de la création d’ancres spatiales Azure dans un moteur Unreal.
author: hferrone
services: azure-spatial-anchors
ms.author: v-haferr
ms.date: 07/01/2020
ms.topic: tutorial
ms.service: azure-spatial-anchors
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens 2, azure, développement Azure, ancres spatiales, réalité mixte, développement, fonctionnalités, nouveau projet, émulateur, documentation, guides, hologrammes, développement de jeux
ms.openlocfilehash: c7189407bea4b38e7305f0dda7637b82d3325704
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87377282"
---
# <a name="azure-spatial-anchors-in-unreal"></a><span data-ttu-id="f998e-104">Azure Spatial Anchors dans Unreal</span><span class="sxs-lookup"><span data-stu-id="f998e-104">Azure Spatial Anchors in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="f998e-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="f998e-105">Overview</span></span>

<span data-ttu-id="f998e-106">Azure Spatial Anchors est un service de Réalité mixte Microsoft qui permet aux appareils de réalité augmentée de découvrir, de partager et de conserver des points d’ancrage dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="f998e-106">Azure Spatial Anchors is a Microsoft Mixed Reality service, allowing augmented reality devices to discover, share, and persist anchor points in the physical world.</span></span> <span data-ttu-id="f998e-107">La documentation ci-dessous fournit des instructions pour l’intégration du service Azure Spatial Anchors à un projet Unreal.</span><span class="sxs-lookup"><span data-stu-id="f998e-107">Documentation below provides instructions for integrating the Azure Spatial Anchors service into an Unreal project.</span></span> <span data-ttu-id="f998e-108">Si vous souhaitez obtenir plus d’informations, consultez la documentation sur le [service Azure Spatial Anchors](https://azure.microsoft.com/services/spatial-anchors/).</span><span class="sxs-lookup"><span data-stu-id="f998e-108">If you're looking for more information, check out the [Azure Spatial Anchors service](https://azure.microsoft.com/services/spatial-anchors/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f998e-109">Les ancres locales sont stockées sur l’appareil, alors que les ancres spatiales Azure sont stockées dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="f998e-109">Local anchors are stored on device, while Azure Spatial Anchors are stored in the cloud.</span></span> <span data-ttu-id="f998e-110">Si vous envisagez de stocker vos ancres localement sur un appareil, nous mettons à votre disposition un document sur les [ancres spatiales locales](unreal-spatial-anchors.md) qui peut vous guider tout au long du processus.</span><span class="sxs-lookup"><span data-stu-id="f998e-110">If you're looking to store your anchors locally on a device, we have a [Local Spatial Anchors](unreal-spatial-anchors.md) document that can walk you through the process.</span></span> <span data-ttu-id="f998e-111">Notez que vous pouvez avoir des ancres locales et Azure dans le même projet sans conflit.</span><span class="sxs-lookup"><span data-stu-id="f998e-111">Note that you can have local and Azure anchors in the same project without conflict.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f998e-112">Prérequis</span><span class="sxs-lookup"><span data-stu-id="f998e-112">Prerequisites</span></span>

<span data-ttu-id="f998e-113">Pour suivre ce guide, vous devez avoir :</span><span class="sxs-lookup"><span data-stu-id="f998e-113">To complete this guide, make sure you have:</span></span>

- <span data-ttu-id="f998e-114">Installé [Unreal version 4.25](https://www.unrealengine.com/get-now) ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f998e-114">Installed [Unreal version 4.25](https://www.unrealengine.com/get-now) or later</span></span>
- <span data-ttu-id="f998e-115">Un projet [HoloLens 2](unreal-uxt-ch1.md) configuré dans Unreal.</span><span class="sxs-lookup"><span data-stu-id="f998e-115">A [HoloLens 2 project](unreal-uxt-ch1.md) setup in Unreal</span></span> 
- <span data-ttu-id="f998e-116">Lu la [vue d’ensemble d’Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/overview).</span><span class="sxs-lookup"><span data-stu-id="f998e-116">Read through the [Azure Spatial Anchors overview](https://docs.microsoft.com/azure/spatial-anchors/overview)</span></span>
- <span data-ttu-id="f998e-117">Une connaissance de base de C++ et Unreal.</span><span class="sxs-lookup"><span data-stu-id="f998e-117">Basic knowledge on C++ and Unreal</span></span>

## <a name="getting-azure-spatial-anchors-account-info"></a><span data-ttu-id="f998e-118">Obtention d’informations sur le compte Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="f998e-118">Getting Azure Spatial Anchors account info</span></span>

<span data-ttu-id="f998e-119">Avant d’utiliser Azure Spatial Anchors dans votre projet, vous devez :</span><span class="sxs-lookup"><span data-stu-id="f998e-119">Before using Azure Spatial Anchors in your project, you need to:</span></span>
* <span data-ttu-id="f998e-120">[Créer une ressource d’ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens#create-a-spatial-anchors-resource) et copier les champs de compte listés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f998e-120">[Create a spatial anchors resource](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens#create-a-spatial-anchors-resource) and copy the account fields listed below.</span></span> <span data-ttu-id="f998e-121">Ces valeurs sont utilisées pour authentifier les utilisateurs auprès du compte de votre application :</span><span class="sxs-lookup"><span data-stu-id="f998e-121">These values are used to authenticate users with your application's account:</span></span>
    * <span data-ttu-id="f998e-122">**ID de compte**</span><span class="sxs-lookup"><span data-stu-id="f998e-122">**Account ID**</span></span>
    * <span data-ttu-id="f998e-123">**Clé de compte**</span><span class="sxs-lookup"><span data-stu-id="f998e-123">**Account Key**</span></span>

<span data-ttu-id="f998e-124">Pour plus d’informations, consultez la documentation sur l’[authentification Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/concepts/authentication?tabs=csharp).</span><span class="sxs-lookup"><span data-stu-id="f998e-124">Check out the [Azure Spatial Anchors authentication](https://docs.microsoft.com/azure/spatial-anchors/concepts/authentication?tabs=csharp) docs for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="f998e-125">Azure Spatial Anchors dans Unreal 4.25 ne prend pas en charge les jetons d’authentification Azure AD, mais la prise en charge de cette fonctionnalité sera disponible dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f998e-125">Azure Spatial Anchors in Unreal 4.25 does not support Azure AD authentication tokens, but support for this functionality will be coming in a later release.</span></span>

## <a name="adding-azure-spatial-anchors-plugins"></a><span data-ttu-id="f998e-126">Ajout des plug-ins Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="f998e-126">Adding Azure Spatial Anchors plugins</span></span>

<span data-ttu-id="f998e-127">Activez les plug-ins Azure Spatial Anchors dans l’éditeur Unreal en effectuant les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f998e-127">Enable the Azure Spatial Anchors plugins in the Unreal editor by:</span></span>
1. <span data-ttu-id="f998e-128">Cliquez sur **Edit > Plugins** et recherchez **AzureSpatialAnchors** et **AzureSpatialAnchorsForWMR**.</span><span class="sxs-lookup"><span data-stu-id="f998e-128">Clicking **Edit > Plugins** and searching for **AzureSpatialAnchors** and **AzureSpatialAnchorsForWMR**.</span></span>
2. <span data-ttu-id="f998e-129">Cochez la case **Enabled** dans les deux plug-ins pour autoriser l’accès aux bibliothèques de blueprints Azure Spatial Anchors dans votre application.</span><span class="sxs-lookup"><span data-stu-id="f998e-129">Select the **Enabled** checkbox in both plugins to allow access to the Azure Spatial Anchors blueprint libraries in your application.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-01.png)

<span data-ttu-id="f998e-131">Une fois cette opération terminée, redémarrez l’éditeur Unreal pour que les modifications apportées aux plug-ins prennent effet.</span><span class="sxs-lookup"><span data-stu-id="f998e-131">Once that's done, restart the Unreal Editor for the plugin changes to take effect.</span></span> <span data-ttu-id="f998e-132">Le projet est maintenant prêt à utiliser Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-132">The project is now ready to use Azure Spatial Anchors.</span></span>

## <a name="starting-a-spatial-anchors-session"></a><span data-ttu-id="f998e-133">Démarrage d’une session Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="f998e-133">Starting a Spatial Anchors session</span></span>
<span data-ttu-id="f998e-134">Une session Azure Spatial Anchors permet aux applications clientes de communiquer avec le service Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-134">An Azure Spatial Anchors session allows client applications to communicate with the Azure Spatial Anchors service.</span></span> <span data-ttu-id="f998e-135">Vous devez créer et démarrer une session Azure Spatial Anchors pour créer, conserver et partager des ancres spatiales Azure :</span><span class="sxs-lookup"><span data-stu-id="f998e-135">You'll need to create and start an Azure Spatial Anchors session to create, persist, and share Azure Spatial Anchors:</span></span>

1. <span data-ttu-id="f998e-136">Ouvrez le blueprint du Pawn que vous utilisez dans l’application.</span><span class="sxs-lookup"><span data-stu-id="f998e-136">Open the blueprint for the Pawn you're using in the application.</span></span>
2. <span data-ttu-id="f998e-137">Ajoutez deux variables de chaîne pour l’**ID de compte** et la **clé de compte**, puis affectez les valeurs correspondantes à partir de votre compte Azure Spatial Anchors pour authentifier la session.</span><span class="sxs-lookup"><span data-stu-id="f998e-137">Add two string variables for the **Account ID** and **Account Key**, then assign the corresponding values from your Azure Spatial Anchors account to authenticate the session.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-02.png)

<span data-ttu-id="f998e-139">Démarrez une session Azure Spatial Anchors en effectuant les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f998e-139">Start an Azure Spatial Anchors session by:</span></span>
1. <span data-ttu-id="f998e-140">Vérifiez qu’une **session RA** est en cours d’exécution dans l’application HoloLens, car la session Azure Spatial Anchors ne peut pas démarrer tant qu’une session RA n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f998e-140">Checking that an **AR Session** is running in the HoloLens application, as the Azure Spatial Anchors session can't start until an AR Session is running.</span></span> <span data-ttu-id="f998e-141">Si vous n’en avez pas configuré, [créez une ressource de session RA](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch3#adding-the-session-asset).</span><span class="sxs-lookup"><span data-stu-id="f998e-141">If you don't have one setup, [create an AR Session asset](https://docs.microsoft.com/windows/mixed-reality/unreal-uxt-ch3#adding-the-session-asset).</span></span>
2. <span data-ttu-id="f998e-142">Ajoutez l’événement personnalisé **Démarrer une session Azure Spatial Anchors** et configurez-le comme indiqué dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f998e-142">Adding the **Start Azure Spatial Anchors Session** custom event and configure it as shown in the screenshot below.</span></span>
    * <span data-ttu-id="f998e-143">La création d’une session ne provoque pas son démarrage par défaut, ce qui permet au développeur de configurer la session pour l’authentification auprès du service Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-143">Creating a session doesn't start the session by default, which allows the developer to configure the session for authentication with the Azure Spatial Anchors service.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-03.png)

3. <span data-ttu-id="f998e-145">Configurez la session Azure Spatial Anchors pour fournir l’**ID de compte** et la **clé de compte**.</span><span class="sxs-lookup"><span data-stu-id="f998e-145">Configure the Azure Spatial Anchors session to provide the **Account ID** and **Account Key**.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-04.png)

4. <span data-ttu-id="f998e-147">Démarrez la session Azure Spatial Anchors afin de permettre à l’application de créer et de localiser les ancres spatiales Azure.</span><span class="sxs-lookup"><span data-stu-id="f998e-147">Start the Azure Spatial Anchors session, allowing the application to create and locate Azure Spatial Anchors.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-05.png)

<span data-ttu-id="f998e-149">Nous vous recommandons de nettoyer les ressources Azure Spatial Anchors dans votre blueprint de graphe d’événements lorsque vous n’utilisez plus le service :</span><span class="sxs-lookup"><span data-stu-id="f998e-149">It's good practice to clean up Azure Spatial Anchors resources in your Event Graph blueprint when you're no longer using the service:</span></span>

1. <span data-ttu-id="f998e-150">Arrêtez la session Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-150">Stop the Azure Spatial Anchors session.</span></span> <span data-ttu-id="f998e-151">La session ne sera plus en cours d’exécution, mais ses ressources associées existeront toujours dans le plug-in Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-151">The session will no longer be running, but its associated resources will still exist in the Azure Spatial Anchors plugin.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-06.png)

2. <span data-ttu-id="f998e-153">Détruisez la session Azure Spatial Anchors pour nettoyer toutes les ressources de session Azure Spatial Anchors, toujours connues du plug-in Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-153">Destroy the Azure Spatial Anchors session to clean up any Azure Spatial Anchors session resources still known to the Azure Spatial Anchors plugin.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-07.png)

<span data-ttu-id="f998e-155">Votre blueprint de graphe d’événements doit ressembler à la capture d’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f998e-155">Your Event Graph blueprint should look like the screenshot below:</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-08.png)


## <a name="creating-an-anchor"></a><span data-ttu-id="f998e-157">Création d’une ancre</span><span class="sxs-lookup"><span data-stu-id="f998e-157">Creating an anchor</span></span>
<span data-ttu-id="f998e-158">Une ancre spatiale Azure représente un environnement physique dans l’espace de l’application de réalité augmentée, qui verrouille le contenu de réalité augmentée à des emplacements du monde physique.</span><span class="sxs-lookup"><span data-stu-id="f998e-158">An Azure Spatial Anchor represents a physical world pose in the augmented reality application space, which locks augmented reality content to locations in the physical world.</span></span> <span data-ttu-id="f998e-159">Les ancres spatiales Azure peuvent également être partagées par différents utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f998e-159">Azure Spatial Anchors can also be shared among different users.</span></span> <span data-ttu-id="f998e-160">Ce partage permet de placer du contenu de réalité augmenté sur différents appareils au même emplacement dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="f998e-160">This sharing allows augmented reality content drawn on different devices to be positioned in the same location in the physical world.</span></span> 

<span data-ttu-id="f998e-161">Pour créer une ancre spatiale Azure</span><span class="sxs-lookup"><span data-stu-id="f998e-161">To create a new Azure Spatial Anchor:</span></span>
1. <span data-ttu-id="f998e-162">Vérifiez qu’une session Azure Spatial Anchors est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f998e-162">Check that an Azure Spatial Anchors session is running.</span></span> <span data-ttu-id="f998e-163">L’application ne peut pas créer ou conserver une ancre spatiale Azure quand aucune session Azure Spatial Anchors n’est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f998e-163">The application can't create or persist an Azure Spatial Anchor when no Azure Spatial Anchors session is running.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-09.png)

2. <span data-ttu-id="f998e-165">Créez ou obtenez un **[composant de scène](https://docs.unrealengine.com/API/Runtime/Engine/Components/USceneComponent/index.html)** Unreal dont l’emplacement doit être conservé.</span><span class="sxs-lookup"><span data-stu-id="f998e-165">Create or obtain an Unreal **[Scene Component](https://docs.unrealengine.com/API/Runtime/Engine/Components/USceneComponent/index.html)** that should have its location persisted.</span></span> 
    * <span data-ttu-id="f998e-166">Dans l’image ci-dessous, le composant **Scene Component Needing Anchor** est utilisé comme variable.</span><span class="sxs-lookup"><span data-stu-id="f998e-166">In the below image, the **Scene Component Needing Anchor** component is used as a variable.</span></span> <span data-ttu-id="f998e-167">Un composant de scène Unreal est nécessaire pour établir une transformation universelle d’application pour une [épingle RA](https://docs.unrealengine.com/BlueprintAPI/HoloLensAR/ARPin/index.html) et une ancre spatiale Azure.</span><span class="sxs-lookup"><span data-stu-id="f998e-167">An Unreal Scene Component is needed to establish an application world transform for an [AR Pin](https://docs.unrealengine.com/BlueprintAPI/HoloLensAR/ARPin/index.html) and Azure Spatial Anchor.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-10.png)

<span data-ttu-id="f998e-169">Pour construire et enregistrer une ancre spatiale Azure pour un composant de scène Unreal</span><span class="sxs-lookup"><span data-stu-id="f998e-169">To construct and save an Azure Spatial Anchor for an Unreal Scene Component:</span></span>
1. <span data-ttu-id="f998e-170">Appelez le [composant d’épingle](https://docs.unrealengine.com/BlueprintAPI/ARAugmentedReality/Pin/PinComponent/index.html) pour le composant de scène Unreal et spécifiez la **transformation universelle** du composant de scène comme transformation universelle utilisée pour l’épingle RA.</span><span class="sxs-lookup"><span data-stu-id="f998e-170">Call the [Pin Component](https://docs.unrealengine.com/BlueprintAPI/ARAugmentedReality/Pin/PinComponent/index.html) for the Unreal Scene Component and specify the Scene Component's **World Transform** as the World Transform used for the AR Pin.</span></span>
    * <span data-ttu-id="f998e-171">Unreal effectue le suivi des points RA dans l’espace de l’application à l’aide d’épingles RA, qui sont utilisées pour créer une ancre spatiale Azure.</span><span class="sxs-lookup"><span data-stu-id="f998e-171">Unreal tracks AR points in the application space using AR Pins, which are used to create an Azure Spatial Anchor.</span></span> <span data-ttu-id="f998e-172">Dans Unreal, une épingle RA est analogue à un SpatialAnchor sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="f998e-172">In Unreal, an AR Pin is analogous to a SpatialAnchor on HoloLens.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-11.png)

2. <span data-ttu-id="f998e-174">Appelez **Create Cloud Anchor** à l’aide de l’épingle RA que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="f998e-174">Call **Create Cloud Anchor** using the newly created AR Pin.</span></span>
    * <span data-ttu-id="f998e-175">Create Cloud Anchor crée une ancre spatiale Azure localement mais pas dans le service Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-175">Create Cloud Anchor creates an Azure Spatial Anchor locally but not in the Azure Spatial Anchor service.</span></span> <span data-ttu-id="f998e-176">Les paramètres de l’ancre spatiale Azure, tels que la date d’expiration, peuvent être définis avant de créer l’ancre spatiale Azure avec le service.</span><span class="sxs-lookup"><span data-stu-id="f998e-176">Parameters for the Azure Spatial Anchor, such as an expiration date, can be set before creating the Azure Spatial Anchor with the service.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-12.png)

3. <span data-ttu-id="f998e-178">Définissez l’expiration de l’ancre spatiale Azure.</span><span class="sxs-lookup"><span data-stu-id="f998e-178">Set the Azure Spatial Anchor expiration.</span></span> <span data-ttu-id="f998e-179">Le paramètre Durée de vie de cette fonction permet au développeur de spécifier, en secondes, la durée pendant laquelle l’ancre doit être tenue à jour par le service.</span><span class="sxs-lookup"><span data-stu-id="f998e-179">This function's Lifetime parameter allows the developer to specify in seconds how long the anchor should be maintained by the service.</span></span>
    * <span data-ttu-id="f998e-180">Par exemple, un délai d’expiration d’une semaine prendrait une valeur de 60 secondes x 60 minutes x 24 heures x 7 jours = 604 800 secondes.</span><span class="sxs-lookup"><span data-stu-id="f998e-180">For example, a week long expiration would take a value of 60 seconds x 60 minutes x 24 hours x seven days = 604,800 seconds.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-13.png)

<span data-ttu-id="f998e-182">Après avoir défini les paramètres de l’ancre, déclarez-la comme prête à être enregistrée.</span><span class="sxs-lookup"><span data-stu-id="f998e-182">After setting anchor parameters, declare the anchor as ready to save.</span></span> <span data-ttu-id="f998e-183">Dans l’exemple ci-dessous, la nouvelle ancre spatiale Azure est ajoutée à un ensemble d’ancres spatiales Azure nécessitant un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="f998e-183">In the example below, the newly created Azure Spatial Anchor is added to a set of Azure Spatial Anchors needing saving.</span></span> <span data-ttu-id="f998e-184">Cet ensemble est déclaré en tant que variable pour le blueprint de Pawn.</span><span class="sxs-lookup"><span data-stu-id="f998e-184">This set is declared as a variable for the Pawn blueprint.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-14.png)

## <a name="saving-an-anchor"></a><span data-ttu-id="f998e-186">Enregistrement d’une ancre</span><span class="sxs-lookup"><span data-stu-id="f998e-186">Saving an Anchor</span></span>

<span data-ttu-id="f998e-187">Après avoir configuré l’ancre spatiale Azure avec vos paramètres, appelez **Save Cloud Anchor**.</span><span class="sxs-lookup"><span data-stu-id="f998e-187">After configuring the Azure Spatial Anchor with your parameters, call **Save Cloud Anchor**.</span></span> <span data-ttu-id="f998e-188">Save Cloud Anchor déclare l’ancre auprès du service Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-188">Save Cloud Anchor declares the anchor to the Azure Spatial Anchors service.</span></span> <span data-ttu-id="f998e-189">Lorsque l’appel à Save Cloud Anchor s’effectue correctement, l’ancre spatiale Azure est disponible pour les autres utilisateurs du service Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-189">When the call to Save Cloud Anchor succeeds, the Azure Spatial Anchor is available to other users of the Azure Spatial Anchor service.</span></span>  

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-15.png)

> [!NOTE]
> <span data-ttu-id="f998e-191">Save Cloud Anchor est une fonction asynchrone qui peut être appelée uniquement sur un événement de thread de jeu, par exemple **EventTick**.</span><span class="sxs-lookup"><span data-stu-id="f998e-191">Save Cloud Anchor is an asynchronous function and can only be called on a game thread event such as **EventTick**.</span></span> <span data-ttu-id="f998e-192">Save Cloud Anchor peut ne pas apparaître en tant que fonction de blueprint disponible dans les fonctions de blueprint personnalisées.</span><span class="sxs-lookup"><span data-stu-id="f998e-192">Save Cloud Anchor may not appear as an available blueprint function in custom blueprint Functions.</span></span> <span data-ttu-id="f998e-193">Toutefois, elle devrait être disponible dans l’éditeur de blueprint de graphe d’événements de Pawn.</span><span class="sxs-lookup"><span data-stu-id="f998e-193">However, it should be available in the Pawn Event Graph blueprint editor.</span></span>

<span data-ttu-id="f998e-194">Dans l’exemple ci-dessous, l’ancre spatiale Azure est stockée dans un ensemble pendant un rappel d’événement d’entrée.</span><span class="sxs-lookup"><span data-stu-id="f998e-194">In the example below, the Azure Spatial Anchor is stored in a set during an input event callback.</span></span> <span data-ttu-id="f998e-195">Elle est ensuite enregistrée sur l’EventTick.</span><span class="sxs-lookup"><span data-stu-id="f998e-195">The anchor is then saved on the EventTick.</span></span> <span data-ttu-id="f998e-196">L’enregistrement d’une ancre spatiale Azure peut nécessiter plusieurs tentatives, en fonction de la quantité de données spatiales créées par votre session Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-196">Saving an Azure Spatial Anchor may take multiple attempts depending on the amount of spatial data that your Azure Spatial Anchors session has created.</span></span> <span data-ttu-id="f998e-197">Il est donc préférable de vérifier si l’appel d’enregistrement a réussi.</span><span class="sxs-lookup"><span data-stu-id="f998e-197">That's why it's a good idea to check whether the save call succeeded.</span></span>

<span data-ttu-id="f998e-198">Si l’ancre n’est pas enregistrée, rajoutez-la à l’ensemble d’ancres à enregistrer.</span><span class="sxs-lookup"><span data-stu-id="f998e-198">If the anchor doesn't save, re-add it to the set of anchors still needing to be saved.</span></span> <span data-ttu-id="f998e-199">Les EventTicks ultérieurs essaieront d’enregistrer l’ancre jusqu’à ce qu’elle soit correctement stockée dans le service Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-199">Future EventTicks will try to save the anchor until it's successfully stored in the Azure Spatial Anchor service.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-16.png)

<span data-ttu-id="f998e-201">Une fois l’ancre enregistrée, vous pouvez utiliser la transformation d’épingles RA en tant que transformation de référence pour placer du contenu dans l’application.</span><span class="sxs-lookup"><span data-stu-id="f998e-201">Once the anchor saves, you can use the AR Pins' transform as a reference transform for placing content in the application.</span></span> <span data-ttu-id="f998e-202">D’autres utilisateurs peuvent détecter cette ancre et aligner du contenu RA pour différents appareils dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="f998e-202">Other users can detect this anchor and align AR content for different devices in the physical world.</span></span>

## <a name="deleting-an-anchor"></a><span data-ttu-id="f998e-203">Suppression d’une ancre</span><span class="sxs-lookup"><span data-stu-id="f998e-203">Deleting an Anchor</span></span>

<span data-ttu-id="f998e-204">Vous pouvez supprimer des ancres du service Azure Spatial Anchors en appelant **Delete Cloud Anchor**.</span><span class="sxs-lookup"><span data-stu-id="f998e-204">You can delete anchors from the Azure Spatial Anchor service by calling **Delete Cloud Anchor**.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-17.png)

> [!NOTE]
> <span data-ttu-id="f998e-206">Delete Cloud Anchor est une fonction latente qui peut être appelée uniquement sur un événement de thread de jeu, tel qu’EventTick.</span><span class="sxs-lookup"><span data-stu-id="f998e-206">Delete Cloud Anchor is a latent function and can only be called on a game thread event, such as EventTick.</span></span> <span data-ttu-id="f998e-207">Delete Cloud Anchor peut ne pas apparaître en tant que fonction de blueprint disponible dans les fonctions de blueprint personnalisées.</span><span class="sxs-lookup"><span data-stu-id="f998e-207">Delete Cloud Anchor may not appear as an available blueprint function in custom blueprint Functions.</span></span> <span data-ttu-id="f998e-208">Elle devrait toutefois être disponible dans l’éditeur de blueprint de graphe d’événements de Pawn.</span><span class="sxs-lookup"><span data-stu-id="f998e-208">It should however be available in the Pawn Event Graph blueprint editor.</span></span>

<span data-ttu-id="f998e-209">Dans l’exemple ci-dessous, l’ancre est marquée pour suppression sur un événement d’entrée personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f998e-209">In the example below, the anchor is flagged for deletion on a custom input event.</span></span> <span data-ttu-id="f998e-210">La suppression est ensuite tentée sur l’EventTick.</span><span class="sxs-lookup"><span data-stu-id="f998e-210">The deletion is then attempted on the EventTick.</span></span> <span data-ttu-id="f998e-211">En cas d’échec de la suppression de l’ancre spatiale Azure, ajoutez-la à l’ensemble d’ancres marquées pour suppression. La suppression sera retentée lors des EventTicks ultérieurs.</span><span class="sxs-lookup"><span data-stu-id="f998e-211">If the anchor deletion fails, add the Azure Spatial Anchor to the set of anchors flagged for deletion and tries again on later EventTicks.</span></span>

<span data-ttu-id="f998e-212">Votre blueprint de graphe d’événements doit maintenant ressembler à la capture d’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f998e-212">Your Event Graph blueprint should now look like the screenshot below:</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-18.png)


## <a name="locating-pre-existing-anchors"></a><span data-ttu-id="f998e-214">Recherche d’ancres préexistantes</span><span class="sxs-lookup"><span data-stu-id="f998e-214">Locating pre-existing anchors</span></span>

<span data-ttu-id="f998e-215">En plus de créer des ancres spatiales Azure, vous pouvez détecter les ancres créées par des homologues avec le service Azure Spatial Anchors :</span><span class="sxs-lookup"><span data-stu-id="f998e-215">In addition to creating Azure Spatial Anchors, you can detect anchors created by peers with the Azure Spatial Anchors service:</span></span>

1. <span data-ttu-id="f998e-216">Obtenez un identificateur Azure Spatial Anchors pour l’ancre que vous souhaitez détecter.</span><span class="sxs-lookup"><span data-stu-id="f998e-216">Obtain an Azure Spatial Anchor identifier for the anchor that you would like to detect.</span></span>
    * <span data-ttu-id="f998e-217">Un identificateur d’ancre peut être obtenu pour une ancre créée par le même appareil lors d’une session Azure Spatial Anchors précédente.</span><span class="sxs-lookup"><span data-stu-id="f998e-217">An anchor identifier can be obtained for an anchor created by the same device in a previous Azure Spatial Anchors session.</span></span> <span data-ttu-id="f998e-218">Il peut également être créé et partagé par des appareils homologues qui interagissent avec le service Azure Spatial Anchors.</span><span class="sxs-lookup"><span data-stu-id="f998e-218">It can also be created and shared by peer devices interacting with the Azure Spatial Anchors service.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-24.png)

2. <span data-ttu-id="f998e-220">Ajoutez un composant **AzureSpatialAnchorsEvent** à votre blueprint de Pawn.</span><span class="sxs-lookup"><span data-stu-id="f998e-220">Add an **AzureSpatialAnchorsEvent** component to your Pawn blueprint.</span></span>
    * <span data-ttu-id="f998e-221">Ce composant vous permet de vous abonner à différents événements Azure Spatial Anchors, tels que des événements appelés quand des ancres spatiales Azure sont localisées.</span><span class="sxs-lookup"><span data-stu-id="f998e-221">This component allows you to subscribe to various Azure Spatial Anchors events, such as events called when Azure Spatial Anchors are located.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-19.png)

3. <span data-ttu-id="f998e-223">Abonnez-vous à l’**ASAAnchor Located Delegate** pour le composant **AzureSpatialAnchorsEvent**.</span><span class="sxs-lookup"><span data-stu-id="f998e-223">Subscribe to the **ASAAnchor Located Delegate** for the **AzureSpatialAnchorsEvent** component.</span></span>
    * <span data-ttu-id="f998e-224">Le délégué permet à l’application de savoir quand de nouvelles ancres associées au compte Azure Spatial Anchors ont été localisées.</span><span class="sxs-lookup"><span data-stu-id="f998e-224">The delegate lets the application know when new anchors associated with the Azure Spatial Anchors account have been located.</span></span>
    * <span data-ttu-id="f998e-225">Avec le rappel d’événement, les ancres spatiales Azure créées par les homologues à l’aide de la session Azure Spatial Anchors n’auront pas d’épingles RA créées par défaut.</span><span class="sxs-lookup"><span data-stu-id="f998e-225">With the event callback, Azure Spatial Anchors created by peers using the Azure Spatial Anchors session won't have AR Pins created by default.</span></span> <span data-ttu-id="f998e-226">Pour créer une épingle RA pour l’ancre spatiale Azure détectée, les développeurs peuvent appeler **Create ARPin Around Azure Cloud Spatial Anchor**.</span><span class="sxs-lookup"><span data-stu-id="f998e-226">To create an AR Pin for the detected Azure Spatial Anchor, developers can call **Create ARPin Around Azure Cloud Spatial Anchor**.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-20.png)

<span data-ttu-id="f998e-228">Pour localiser les ancres spatiales Azure créées par des homologues à l’aide du service Azure Spatial Anchors, l’application doit créer un **observateur Azure Spatial Anchors** :</span><span class="sxs-lookup"><span data-stu-id="f998e-228">In order to locate Azure Spatial Anchors created by peers using the Azure Spatial Anchor service, the application will have to create an **Azure Spatial Anchors Watcher**:</span></span>
1. <span data-ttu-id="f998e-229">Vérifiez qu’une session Azure Spatial Anchors est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f998e-229">Check that an Azure Spatial Anchors session is running.</span></span>
2. <span data-ttu-id="f998e-230">Créez un **AzureSpatialAnchorsLocateCriteria**.</span><span class="sxs-lookup"><span data-stu-id="f998e-230">Create an **AzureSpatialAnchorsLocateCriteria**.</span></span>
    * <span data-ttu-id="f998e-231">Vous pouvez spécifier différents paramètres d’emplacement tels que la distance par rapport à l’utilisateur ou la distance par rapport à une autre ancre.</span><span class="sxs-lookup"><span data-stu-id="f998e-231">You can specify various location parameters like distance from the user or distance from another anchor.</span></span>
3. <span data-ttu-id="f998e-232">Déclarez l’identificateur Azure Spatial Anchors souhaité dans l’**AzureSpatialAnchorsLocateCritieria**.</span><span class="sxs-lookup"><span data-stu-id="f998e-232">Declare your desired Azure Spatial Anchor identifier in the **AzureSpatialAnchorsLocateCritieria**.</span></span>
4. <span data-ttu-id="f998e-233">Appelez **Create Watcher**.</span><span class="sxs-lookup"><span data-stu-id="f998e-233">Call **Create Watcher**.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-21.png)

<span data-ttu-id="f998e-235">L’application commence maintenant à rechercher les ancres spatiales Azure connues du service Azure Spatial Anchors, ce qui signifie que les utilisateurs peuvent localiser les ancres spatiales Azure créées par leurs homologues.</span><span class="sxs-lookup"><span data-stu-id="f998e-235">The application now begins looking for Azure Spatial Anchors known to the Azure Spatial Anchors service, meaning that users can locate Azure Spatial Anchors created by their peers.</span></span>

<span data-ttu-id="f998e-236">Après avoir localisé l’ancre spatiale Azure, appelez **Stop Watcher** pour arrêter l’observateur Azure Spatial Anchors et nettoyer ses ressources.</span><span class="sxs-lookup"><span data-stu-id="f998e-236">After locating the Azure Spatial Anchor, call **Stop Watcher** to stop the Azure Spatial Anchors Watcher and clean up watcher resources.</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-22.png)

<span data-ttu-id="f998e-238">Votre blueprint de graphe d’événements final doit maintenant ressembler à la capture d’écran ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f998e-238">Your final Event Graph blueprint should now look like the screenshot below:</span></span>

![Plug-ins Spatial Anchors](images/asa-unreal/unreal-spatial-anchors-img-23.png)


## <a name="next-steps"></a><span data-ttu-id="f998e-240">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f998e-240">Next steps</span></span>
* [<span data-ttu-id="f998e-241">Ancres spatiales locales</span><span class="sxs-lookup"><span data-stu-id="f998e-241">Local Spatial Anchors</span></span>](unreal-spatial-anchors.md)
* [<span data-ttu-id="f998e-242">Documentation sur les ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="f998e-242">Spatial Anchors documentation</span></span>](https://docs.microsoft.com/azure/spatial-anchors/)
* [<span data-ttu-id="f998e-243">Fonctionnalités des ancres spatiales</span><span class="sxs-lookup"><span data-stu-id="f998e-243">Spatial Anchor features</span></span>](https://azure.microsoft.com/services/spatial-anchors/#features)
* [<span data-ttu-id="f998e-244">Recommandations pour une expérience d’ancrage efficace</span><span class="sxs-lookup"><span data-stu-id="f998e-244">Effective anchor experience guidelines</span></span>](https://docs.microsoft.com/azure/spatial-anchors/concepts/guidelines-effective-anchor-experiences)