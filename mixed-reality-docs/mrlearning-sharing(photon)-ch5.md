---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 9f4a0c0cc37ab097a60c44891d56fa65f6032418
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67327598"
---
# <a name="azure-spatial-anchors-and-shared-experiences"></a><span data-ttu-id="51688-104">Azure ancres spatiales et les expériences partagées</span><span class="sxs-lookup"><span data-stu-id="51688-104">Azure Spatial Anchors and Shared Experiences</span></span>

<span data-ttu-id="51688-105">Dans cette leçon, nous allez apprendre à intégrer Azure Spatial ancres (ASA) dans notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="51688-105">In this lesson, we will learn how to integrate Azure Spatial Anchors (ASA) into our shared experience.</span></span> <span data-ttu-id="51688-106">ASA permet à plusieurs appareils colocalisés avoir une compréhension commune si leur environnement physique pour l’ancrage virtuel connaît tel que tous les participants de voir les objets dans le même emplacement physique.</span><span class="sxs-lookup"><span data-stu-id="51688-106">ASA allows multiple co-located devices to have a common understanding if their physical environment in order to anchor virtual experiences such that all participants see objects in the same physical place.</span></span>

<span data-ttu-id="51688-107">Avant de poursuivre cette leçon, nous devrons effectuer le Module de formation ASA, qui couvre les notions de base, compte Azure et la création de ressources et autres blocs de bâtiments fondamentaux qui sont nécessaires avant que nous pouvons intégrer ASA dans notre expérience partagée ASA.</span><span class="sxs-lookup"><span data-stu-id="51688-107">Before proceeding with this lesson, we will need to complete the ASA Learning Module, which will cover ASA basics, Azure account and resource creation, and other fundamental buildings blocks that are required before we can integrate ASA into our shared experience.</span></span>

<span data-ttu-id="51688-108">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="51688-108">Objectives:</span></span>

- <span data-ttu-id="51688-109">Intégrer ASA dans une expérience partagée pour l’alignement de multi-device</span><span class="sxs-lookup"><span data-stu-id="51688-109">Integrate ASA into a shared experience for multi-device alignment</span></span>
- <span data-ttu-id="51688-110">Découvrez les principes de base du fonctionne de ASA dans le contexte d’une expérience partagé local</span><span class="sxs-lookup"><span data-stu-id="51688-110">Learn the fundamentals of how ASA works in the context of a local shared experience</span></span>

### <a name="instructions"></a><span data-ttu-id="51688-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="51688-111">Instructions</span></span>

1. <span data-ttu-id="51688-112">Enregistrez le projet à partir de la leçon précédente (CTRL + S) et nommez-la « HLSharedProjectMainPart5.unity » afin qu’il soit plus facile à trouver lorsque vous avez besoin à nouveau.</span><span class="sxs-lookup"><span data-stu-id="51688-112">Save the project from the previous lesson (control+S) and name it "HLSharedProjectMainPart5.unity" so that it's easier to find when you need it again.</span></span>

2. <span data-ttu-id="51688-113">Sélectionnez le préfabriqué TableAnchor en dessous de l’objet parent de « MixedRealityPlayspace » et le supprimer.</span><span class="sxs-lookup"><span data-stu-id="51688-113">Select the TableAnchor prefab underneath  the "MixedRealityPlayspace" parent object, and delete it.</span></span>

![Module3Chapter5tep2im](images/module3chapter5step2im.PNG)

3. <span data-ttu-id="51688-115">Comme certaines des leçons précédentes, importer un nouveau package personnalisé que vous pouvez obtenir [ici.](placeholderlink)</span><span class="sxs-lookup"><span data-stu-id="51688-115">Just like some of the previous lessons, import a new custom package that you can get [here.](placeholderlink)</span></span>

![Module3Chapter5step3im](images/module3chapter5step3im.PNG)

4. <span data-ttu-id="51688-117">Une fois qu’il est importé, saisissez le point d’ancrage de la table qui vient d’être mise à jour (à partir du package unity importé à l’étape précédente) à partir du dossier « prefabs » dans le panneau de configuration de projet et déposez-le dans l’objet parent « MixedRealityPlayspace ».</span><span class="sxs-lookup"><span data-stu-id="51688-117">Once it's imported, grab the newly updated table anchor (from the unity package imported in the previous step) from the "prefabs" folder in the project panel and drop it into the parent object "MixedRealityPlayspace."</span></span>

![Module3hapter5step4im](images/module3chapter5step4im.PNG)

5. <span data-ttu-id="51688-119">Développez l’objet parent de « MixedRealityPlayspace », puis l’objet « TableAnchor » et ainsi l’objet « boutons ».</span><span class="sxs-lookup"><span data-stu-id="51688-119">Expand the "MixedRealityPlayspace" parent object, then the "TableAnchor" object, and expand the "buttons" object as well.</span></span> 

![Module3hapter5step5im](images/module3chapter5step5im.PNG)

6. <span data-ttu-id="51688-121">Maintenant, dans la hiérarchie, sélectionnez le « ShareAzureAnchorButton » et déplacer votre attention sur le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="51688-121">Now in the hierarchy, select the "ShareAzureAnchorButton" and move your attention to the inspector panel.</span></span> <span data-ttu-id="51688-122">Faites défiler vers le menu déroulant illustré dans l’image ci-dessous et sélectionnez « AnchorModuleScript » et cliquez sur « ShareAnchorNetework() ».</span><span class="sxs-lookup"><span data-stu-id="51688-122">Scroll down to the dropdown menu shown in the image below, and select "AnchorModuleScript" and click on "ShareAnchorNetework()."</span></span>

![Module3hapter5step6im](images/module3chapter5step6im.PNG)

7. <span data-ttu-id="51688-124">Comme étape 6, sélectionnez la « GetAzureAnchorButton » et déplacer votre attention à ce panneau.</span><span class="sxs-lookup"><span data-stu-id="51688-124">Much like step 6, select the "GetAzureAnchorButton" and move your attention back to the inspector panel.</span></span> <span data-ttu-id="51688-125">Faites défiler vers le menu déroulant illustré dans l’image ci-dessous et sélectionnez « AnchorModuleScript » et cliquez sur « GetSharedAnchorNetwork() ».</span><span class="sxs-lookup"><span data-stu-id="51688-125">Scroll down to the dropdown menu shown in the image below, and select "AnchorModuleScript" and click on "GetSharedAnchorNetwork()."</span></span> <span data-ttu-id="51688-126">Puis enregistrez.</span><span class="sxs-lookup"><span data-stu-id="51688-126">Then save.</span></span>

![Module3hapter5step7im](images/module3chapter5step7im.PNG)




## <a name="congratulations"></a><span data-ttu-id="51688-128">Félicitations</span><span class="sxs-lookup"><span data-stu-id="51688-128">Congratulations</span></span>

<span data-ttu-id="51688-129">Dans cette leçon, vous avez appris comment intégrer puissantes nouvelles Spatial ancres d’Azure pour aligner les appareils colocalisés dans une expérience partagée !</span><span class="sxs-lookup"><span data-stu-id="51688-129">In this Lesson you learned how to integrate Azure's powerful new Spatial Anchors to align co-located devices in a shared experience!</span></span> <span data-ttu-id="51688-130">Cette leçon conclut également le Module de partage.</span><span class="sxs-lookup"><span data-stu-id="51688-130">This lesson also concludes the Sharing Module.</span></span> <span data-ttu-id="51688-131">Nous avons appris à configurer un nouveau compte Photon, intégrer Photon et jeu de mots dans une application Unity, configuration avatars et des objets partagés et enfin en alignant plusieurs participants à l’aide de ASA.</span><span class="sxs-lookup"><span data-stu-id="51688-131">We learned how to set up a new Photon account, integrate Photon and PUN into a new Unity application, configuring avatars and shared objects, and finally aligning multiple participants using ASA.</span></span> 

