---
title: Didacticiels sur les fonctionnalités multi-utilisateur-5. Intégration des ancres spatiales Azure dans un environnement partagé
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: a3b136023b0beea7cf6eecd52a9a21447576d482
ms.sourcegitcommit: 2bfe9b1af4ee2cc0d668caeccb8ebc3137cbc20b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2020
ms.locfileid: "75901468"
---
# <a name="5-integrating-azure-spatial-anchors-into-a-shared-experience"></a><span data-ttu-id="a7351-105">5. intégration des ancres spatiales Azure dans un environnement partagé</span><span class="sxs-lookup"><span data-stu-id="a7351-105">5. Integrating Azure Spatial Anchors into a shared experience</span></span>

<span data-ttu-id="a7351-106">Dans cette leçon, vous allez apprendre à intégrer les ancres spatiales Azure (ASA) à notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="a7351-106">In this lesson, you'll learn how to integrate Azure Spatial Anchors (ASA) into our shared experience.</span></span> <span data-ttu-id="a7351-107">ASA permet à plusieurs appareils colocalisés d’avoir une référence commune si leur environnement physique est d’ancrer des expériences virtuelles, de sorte que tous les participants voient les objets dans le même emplacement physique.</span><span class="sxs-lookup"><span data-stu-id="a7351-107">ASA allows multiple co-located devices to have a common reference if their physical environment is to anchor virtual experiences such that all participants see objects in the same physical place.</span></span>

## <a name="objectives"></a><span data-ttu-id="a7351-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="a7351-108">Objectives</span></span>

* <span data-ttu-id="a7351-109">Intégrez ASA dans une expérience partagée pour l’alignement sur plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="a7351-109">Integrate ASA into a shared experience for multi-device alignment.</span></span>
* <span data-ttu-id="a7351-110">Découvrez les principes de base du fonctionnement de ASA dans le contexte d’une expérience partagée locale.</span><span class="sxs-lookup"><span data-stu-id="a7351-110">Learn the fundamentals of how ASA works in the context of a local shared experience.</span></span>

## <a name="instructions"></a><span data-ttu-id="a7351-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="a7351-111">Instructions</span></span>

1. <span data-ttu-id="a7351-112">Sélectionnez le Prefab TableAnchor sous l’objet parent MixedRealityPlayspace et supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="a7351-112">Select the TableAnchor prefab underneath the MixedRealityPlayspace parent object, and delete it.</span></span>

    ![Module3Chapter5tep2im](images/module3chapter5step2im.PNG)

2. <span data-ttu-id="a7351-114">Dans la vue projet, accédez à ressources-> Ressources-> Prefabs, puis faites glisser le Prefab TableAnchor sur l’objet SharedPlayground pour en faire un enfant.</span><span class="sxs-lookup"><span data-stu-id="a7351-114">In the Project view, go to Assets->Resources->Prefabs, and drag the TableAnchor prefab on top of the SharedPlayground object to make it a child.</span></span>

3. <span data-ttu-id="a7351-115">Développez l’objet parent MixedRealityPlayspace, l’objet TableAnchor, puis développez également l’objet Buttons.</span><span class="sxs-lookup"><span data-stu-id="a7351-115">Expand the MixedRealityPlayspace parent object, TableAnchor object, and expand the Buttons object as well.</span></span>

    ![Module3hapter5step5im](images/module3chapter5step5im.PNG)

4. <span data-ttu-id="a7351-117">À présent, dans la hiérarchie, sélectionnez ShareAzureAnchorButton et déplacez votre attention sur le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="a7351-117">Now in the hierarchy, select ShareAzureAnchorButton and move your attention to the Inspector panel.</span></span> <span data-ttu-id="a7351-118">Faites défiler vers le bas jusqu’au menu déroulant illustré dans l’image ci-dessous, sélectionnez AnchorModuleScript, puis cliquez sur ShareAnchorNetwork ().</span><span class="sxs-lookup"><span data-stu-id="a7351-118">Scroll down to the drop-down menu shown in the image below, select AnchorModuleScript and click ShareAnchorNetwork().</span></span>

    ![Module3hapter5step6im](images/module3chapter5step6im.PNG)

5. <span data-ttu-id="a7351-120">Sélectionnez GetAzureAnchorButton (Voir l’étape 4) et replacez votre attention sur le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="a7351-120">Select GetAzureAnchorButton (see Step 4) and move your attention back to the Inspector panel.</span></span> <span data-ttu-id="a7351-121">Faites défiler jusqu’au menu déroulant affiché dans l’image ci-dessous, sélectionnez AnchorModuleScript, cliquez sur GetSharedAnchorNetwork (), puis sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="a7351-121">Scroll down to the drop-down menu displayed in the image below, select AnchorModuleScript, click GetSharedAnchorNetwork(), and save.</span></span>

    ![Module3hapter5step7im](images/module3chapter5step7im.PNG)

6. <span data-ttu-id="a7351-123">Pour tester le module de partage, cliquez sur le bouton « Démarrer une session ASA Azure », qui démarre la session d’ancrages spatiaux Azure, puis crée le point d’ancrage Azure en cliquant sur le bouton « créer un point d’ancrage Azure ».</span><span class="sxs-lookup"><span data-stu-id="a7351-123">To test the sharing module, click the "Start Azure ASA Session" button which will start the azure spatial anchors session and then create the azure anchor by clicking the "Create Azure Anchor" button.</span></span> <span data-ttu-id="a7351-124">Attendez que le point d’ancrage Azure soit créé.</span><span class="sxs-lookup"><span data-stu-id="a7351-124">Wait for the azure anchor to get created.</span></span> <span data-ttu-id="a7351-125">Une fois l’ancre Azure créée, cliquez sur le bouton « partager l’ancre Azure » pour partager l’ancre Azure créée à partir du HoloLens.</span><span class="sxs-lookup"><span data-stu-id="a7351-125">Once the azure anchor is created, click the "Share Azure Anchor" button to share the created azure anchor from the HoloLens.</span></span>

7. <span data-ttu-id="a7351-126">Pour recevoir le point d’ancrage Azure partagé dans un autre HoloLens, cliquez sur « Démarrer la session ASA Azure » pour démarrer et accéder à la session ASA actuelle.</span><span class="sxs-lookup"><span data-stu-id="a7351-126">To receive the shared azure anchor in another HoloLens, click the "Start Azure ASA Session" to start and get in to the current ASA session</span></span>

8. <span data-ttu-id="a7351-127">Cliquez sur le bouton « procurez-vous Azure Anchor » pour récupérer l’ancre Azure partagée à partir de l’autre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="a7351-127">Click the "Get Azure Anchor" button to get the shared azure anchor from the other HoloLens.</span></span>

## <a name="congratulations"></a><span data-ttu-id="a7351-128">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="a7351-128">Congratulations</span></span>

<span data-ttu-id="a7351-129">Dans cette leçon, vous avez appris à intégrer les nouvelles ancres spatiales d’Azure pour aligner les appareils colocalisés dans un environnement partagé.</span><span class="sxs-lookup"><span data-stu-id="a7351-129">In this lesson, you learned how to integrate Azure's powerful new Spatial Anchors to align co-located devices in a shared experience!</span></span> <span data-ttu-id="a7351-130">Cela conclut également le module de partage.</span><span class="sxs-lookup"><span data-stu-id="a7351-130">This also concludes the Sharing Module.</span></span> <span data-ttu-id="a7351-131">Nous avons appris à configurer un nouveau compte de photons, à intégrer photons et retentissante dans une nouvelle application Unity, à configurer des avatars et des objets partagés, puis à aligner plusieurs participants à l’aide de ASA.</span><span class="sxs-lookup"><span data-stu-id="a7351-131">We learned how to set up a new Photon account, integrate Photon and PUN into a new Unity application, configure avatars and shared objects, and finally align multiple participants using ASA.</span></span>
