---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 2a16d318c6d749bcbf6ed9db0d6cd2228a6ea06e
ms.sourcegitcommit: 78e21e887bf4357c96c9ab2164559d610e8c041e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67465201"
---
# <a name="azure-spatial-anchors-and-shared-experiences"></a><span data-ttu-id="9c302-104">Azure ancres spatiales et les expériences partagées</span><span class="sxs-lookup"><span data-stu-id="9c302-104">Azure Spatial Anchors and shared experiences</span></span>

<span data-ttu-id="9c302-105">Dans cette leçon, nous Découvrez comment intégrer Azure Spatial ancres (ASA) dans notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="9c302-105">In this lesson, we learn how to integrate Azure Spatial Anchors (ASA) into our shared experience.</span></span> <span data-ttu-id="9c302-106">ASA permet à plusieurs appareils colocalisés avoir une référence commune si leur environnement physique consiste aux expériences virtuel d’ancrage sorte que tous les participants de voir les objets dans le même emplacement physique.</span><span class="sxs-lookup"><span data-stu-id="9c302-106">ASA allows multiple co-located devices to have a common reference if their physical environment is to anchor virtual experiences such that all participants see objects in the same physical place.</span></span>

<span data-ttu-id="9c302-107">Avant de poursuivre cette leçon, nous allons devoir effectuer le module de formation ASA, qui couvre les notions de base, compte Azure et la création de ressources et autres blocs de bâtiments fondamentaux qui sont nécessaires avant que nous pouvons intégrer ASA dans notre expérience partagée ASA.</span><span class="sxs-lookup"><span data-stu-id="9c302-107">Before proceeding with this lesson, we'll need to complete the ASA learning module, which will cover ASA basics, Azure account and resource creation, and other fundamental buildings blocks that are required before we can integrate ASA into our shared experience.</span></span>

<span data-ttu-id="9c302-108">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="9c302-108">Objectives:</span></span>

- <span data-ttu-id="9c302-109">Intégrer ASA dans une expérience partagée pour l’alignement de multi-device</span><span class="sxs-lookup"><span data-stu-id="9c302-109">Integrate ASA into a shared experience for multi-device alignment</span></span>
- <span data-ttu-id="9c302-110">Découvrez les principes de base du fonctionne de ASA dans le contexte d’une expérience partagé local</span><span class="sxs-lookup"><span data-stu-id="9c302-110">Learn the fundamentals of how ASA works in the context of a local shared experience</span></span>

### <a name="instructions"></a><span data-ttu-id="9c302-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="9c302-111">Instructions</span></span>

1. <span data-ttu-id="9c302-112">Enregistrez le projet à partir de la leçon précédente (CTRL + S) et nommez-la « HLSharedProjectMainPart5.unity » afin qu’il soit plus facile à trouver lorsque vous avez besoin à nouveau.</span><span class="sxs-lookup"><span data-stu-id="9c302-112">Save the project from the previous lesson (control+S) and name it "HLSharedProjectMainPart5.unity" so that it's easier to find when you need it again.</span></span>

2. <span data-ttu-id="9c302-113">Sélectionnez le préfabriqué TableAnchor en dessous de l’objet parent de MixedRealityPlayspace et supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="9c302-113">Select the TableAnchor prefab underneath the MixedRealityPlayspace parent object, and delete it.</span></span>

![Module3Chapter5tep2im](images/module3chapter5step2im.PNG)



3.  <span data-ttu-id="9c302-115">Dans la vue du projet, accédez aux ressources -> ressources -> Prefabs, puis faites glisser le préfabriqué TableAnchor en haut de l’objet SharedPlayground pour le rendre un enfant.</span><span class="sxs-lookup"><span data-stu-id="9c302-115">In the Project view go to Assets->Resources->Prefabs, and drag the TableAnchor prefab on top of the SharedPlayground object to make it a child.</span></span>
4.  <span data-ttu-id="9c302-116">Développez l’objet parent de MixedRealityPlayspace, TableAnchor objet et l’objet de boutons.</span><span class="sxs-lookup"><span data-stu-id="9c302-116">Expand the MixedRealityPlayspace parent object, TableAnchor object, and expand the Buttons object as well.</span></span> 

![Module3hapter5step5im](images/module3chapter5step5im.PNG)

4. <span data-ttu-id="9c302-118">Maintenant dans la hiérarchie, sélectionnez ShareAzureAnchorButton et déplacer votre attention sur le panneau Inaspector.</span><span class="sxs-lookup"><span data-stu-id="9c302-118">Now in the hierarchy, select ShareAzureAnchorButton, and move your attention to the Inaspector panel.</span></span> <span data-ttu-id="9c302-119">Faites défiler vers le menu déroulant illustré dans l’image ci-dessous et sélectionnez AnchorModuleScript et cliquez sur ShareAnchorNetework().</span><span class="sxs-lookup"><span data-stu-id="9c302-119">Scroll down to the drop-down menu shown in the image below, and select AnchorModuleScript and click ShareAnchorNetework().</span></span>

![Module3hapter5step6im](images/module3chapter5step6im.PNG)

5. <span data-ttu-id="9c302-121">Sélectionnez GetAzureAnchorButton (voir l’étape 4), et déplacer votre attention à ce panneau.</span><span class="sxs-lookup"><span data-stu-id="9c302-121">Select GetAzureAnchorButton (see Step 4), and move your attention back to the Inspector panel.</span></span> <span data-ttu-id="9c302-122">Faites défiler vers le menu déroulant illustré dans l’image ci-dessous, AnchorModuleScript et cliquez sur GetSharedAnchorNetwork() et sélectionnez Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="9c302-122">Scroll down to the drop-down menu shown in the image below, and select AnchorModuleScript, and click GetSharedAnchorNetwork(), and save.</span></span>

![Module3hapter5step7im](images/module3chapter5step7im.PNG)




## <a name="congratulations"></a><span data-ttu-id="9c302-124">Félicitations</span><span class="sxs-lookup"><span data-stu-id="9c302-124">Congratulations</span></span>

<span data-ttu-id="9c302-125">Dans cette leçon, vous avez appris comment intégrer puissantes nouvelles Spatial ancres d’Azure pour aligner les appareils colocalisés dans une expérience partagée !</span><span class="sxs-lookup"><span data-stu-id="9c302-125">In this Lesson you learned how to integrate Azure's powerful new Spatial Anchors to align co-located devices in a shared experience!</span></span> <span data-ttu-id="9c302-126">Cette leçon conclut également le Module de partage.</span><span class="sxs-lookup"><span data-stu-id="9c302-126">This lesson also concludes the Sharing Module.</span></span> <span data-ttu-id="9c302-127">Nous avons appris à configurer un nouveau compte Photon, intégrer Photon et jeu de mots dans une application Unity, configuration avatars et des objets partagés et enfin en alignant plusieurs participants à l’aide de ASA.</span><span class="sxs-lookup"><span data-stu-id="9c302-127">We learned how to set up a new Photon account, integrate Photon and PUN into a new Unity application, configuring avatars and shared objects, and finally aligning multiple participants using ASA.</span></span> 

