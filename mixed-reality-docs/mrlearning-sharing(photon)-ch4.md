---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 4. Partage de mouvements d’objet avec plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: b0ddf0799fd94c29ce8f1221c55073cd77b63703
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031249"
---
# <a name="4-sharing-object-movements-with-multiple-users"></a><span data-ttu-id="5f32b-105">4. Partage de mouvements d’objet avec plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="5f32b-105">4. Sharing object movements with multiple users</span></span>

<span data-ttu-id="5f32b-106">Dans ce tutoriel, vous allez apprendre à partager les mouvements d’objet afin que tous les participants d’une session partagée puissent collaborer et voir les interactions des autres.</span><span class="sxs-lookup"><span data-stu-id="5f32b-106">In this Tutorial, you'll learn how to share the movements of objects so that all participants of a shared session can collaborate and view each others' interactions.</span></span> <span data-ttu-id="5f32b-107">Cette leçon s’appuie sur le lanceur lunaire créé dans le cadre des [tutoriels du module de base](mrlearning-base.md).</span><span class="sxs-lookup"><span data-stu-id="5f32b-107">This lesson builds upon the Lunar Launcher that was built as part of the [Base Module Tutorials](mrlearning-base.md).</span></span>

## <a name="objectives"></a><span data-ttu-id="5f32b-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="5f32b-108">Objectives</span></span>

- <span data-ttu-id="5f32b-109">Faire apparaître le lanceur lunaire en tant que modèle 3D à partager</span><span class="sxs-lookup"><span data-stu-id="5f32b-109">Bring in the lunar launcher as the 3D model to be shared</span></span>
- <span data-ttu-id="5f32b-110">Configurer votre projet pour partager les mouvements du modèle 3D</span><span class="sxs-lookup"><span data-stu-id="5f32b-110">Configure your project to share the movements of the 3D model</span></span>
- <span data-ttu-id="5f32b-111">Apprendre à créer une application collaborative multi-utilisateur de base</span><span class="sxs-lookup"><span data-stu-id="5f32b-111">Learn how to build a basic multi-user collaborative application</span></span>

## <a name="instructions"></a><span data-ttu-id="5f32b-112">Instructions</span><span class="sxs-lookup"><span data-stu-id="5f32b-112">Instructions</span></span>

1. <span data-ttu-id="5f32b-113">Enregistrez la scène de la leçon précédente (Ctrl+S).</span><span class="sxs-lookup"><span data-stu-id="5f32b-113">Save the scene from the previous lesson (Control+S).</span></span> <span data-ttu-id="5f32b-114">Vous pouvez la nommer HLSharedProjectMainPart4.unity pour la retrouver plus facilement quand vous en avez besoin.</span><span class="sxs-lookup"><span data-stu-id="5f32b-114">You can name it HLSharedProjectMainPart4.unity so it's easier to find when you need it.</span></span>

2. <span data-ttu-id="5f32b-115">Dans la fenêtre Project, dans le dossier Assets->Scripts, double-cliquez sur GenericNetSync pour l’ouvrir dans Visual Studio ou dans l’éditeur de code que vous utilisez, quel qu’il soit.</span><span class="sxs-lookup"><span data-stu-id="5f32b-115">From the Project window, in the Assets->Scripts folder, double-click GenericNetSync to open it in Visual Studio or which ever code editor you are using.</span></span>  

    ![module3chapter4updatestep2](images/module3chapter4updatestep2.png)

3. <span data-ttu-id="5f32b-117">Lignes 34 et 38, supprimez « // » pour activer le code pour la table que vous allez utiliser dans cette leçon.</span><span class="sxs-lookup"><span data-stu-id="5f32b-117">On Lines 34 and 38, remove "//" to activate the code for the table that you will use in this lesson.</span></span> <span data-ttu-id="5f32b-118">Enregistrez ensuite le fichier.</span><span class="sxs-lookup"><span data-stu-id="5f32b-118">Next, save the file.</span></span>

    ![module3chapter4updatestep3](images/module3chapter4updatestep3.png)

4. <span data-ttu-id="5f32b-120">Dans la fenêtre Project, double-cliquez sur le fichier PhotonRoom.cs dans le dossier Assets->Scripts pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5f32b-120">In the Project window, double-click the PhotonRoom.cs file in the Assets->Scripts folder to open it in Visual Studio.</span></span>

    ![module3chapter4updatestep4](images/module3chapter4updatestep4.png)

5. <span data-ttu-id="5f32b-122">Comme à l’étape 3, nous avons besoin de supprimer « // » pour activer le code aux lignes 25, 26 et 106.</span><span class="sxs-lookup"><span data-stu-id="5f32b-122">Just like in Step 3, we need to remove "//" to activate the code at Lines 25, 26, and 106.</span></span>

    ![module3chapter4updatestep5a](images/module3chapter4updatestep5a.png)

    ![module3chapter4updatestep5b](images/module3chapter4updatestep5b.png)

6. <span data-ttu-id="5f32b-125">Dans la vue Hierarchy, sélectionnez l’objet NetworkRoom.</span><span class="sxs-lookup"><span data-stu-id="5f32b-125">In the Hierarchy view, select the NetworkRoom object.</span></span>

    ![module3chapter4updatestep6](images/module3chapter4updatestep6.png)

7. <span data-ttu-id="5f32b-127">Dans la vue Project, accédez à Assets->Resources->Prefabs.</span><span class="sxs-lookup"><span data-stu-id="5f32b-127">In the Project view, navigate to Assets->Resources->Prefabs.</span></span> <span data-ttu-id="5f32b-128">Tout d’abord, glissez-déposez le préfabriqué Table vers l’emplacement Tableprefab sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="5f32b-128">First, drag and drop the Table prefab to the Tableprefab slot on the PhotonRoom class.</span></span> <span data-ttu-id="5f32b-129">Ensuite, glissez-déplacez RocketLauncherCompleteVariantprefab vers l’emplacement Module Prefab sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="5f32b-129">Next, drag and drop the RocketLauncherCompleteVariantprefab to the Module Prefab slot on the PhotonRoom class.</span></span>

    ![module3chapter4updatestep7](images/module3chapter4updatestep7.png)

    >[!NOTE]
    ><span data-ttu-id="5f32b-131">Si vous cliquez sur l’un des objets d’élément préfabriqué avant de relâcher le bouton de la souris, l’inspecteur bascule vers cet objet.</span><span class="sxs-lookup"><span data-stu-id="5f32b-131">If you click one of the prefab objects and release, the inspector will switch to that object.</span></span> <span data-ttu-id="5f32b-132">Cliquez sur chaque objet, faites-les glisser, déposez-les et relâchez-les à l’emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="5f32b-132">Click, drag, drop, and release each object to its appropriate slot.</span></span>

8. <span data-ttu-id="5f32b-133">Cliquez sur la flèche située à gauche de MixedRealityPlayspace pour déplacer l’objet jeu enfant MainCamera jusqu’au préfabriqué SharedPlayground.</span><span class="sxs-lookup"><span data-stu-id="5f32b-133">Click the arrow to the left of MixedRealityPlayspace and move the child game object MainCamera down into the SharedPlayground prefab.</span></span> <span data-ttu-id="5f32b-134">Ensuite, supprimez le préfabriqué MixedRealityPlayspace en le sélectionnant et en appuyant sur « suppr » sur votre clavier.</span><span class="sxs-lookup"><span data-stu-id="5f32b-134">Next, delete the prefab, MixedRealityPlayspace by selecting the prefab and tap "delete" on your keyboard).</span></span>

    ![Module3hapter4step5im](images/module3chapter4step5im.PNG)

    >[!NOTE]
    ><span data-ttu-id="5f32b-136">Assurez-vous que les positions de Main Camera et SharedPlayground sont définies sur 0, 0, 0.</span><span class="sxs-lookup"><span data-stu-id="5f32b-136">Make sure that both the Main Camera and SharedPlayground positions are set to 0,0,0.</span></span>

9. <span data-ttu-id="5f32b-137">Sélectionnez l’objet « SharedPlayground » et cliquez avec le bouton droit de la souris pour choisir l’option « create empty » afin de créer un objet jeu vide en tant qu’enfant de l’objet jeu « SharedPlayground ».</span><span class="sxs-lookup"><span data-stu-id="5f32b-137">Select "SharedPlayground" object and right click the mouse to choose "create empty" option to create an empty game object as a child of "SharedPlayground" game object.</span></span>

   ![Module3chapter4step6im](images/module3chapter4step6im.PNG)

10. <span data-ttu-id="5f32b-139">Après avoir sélectionné le nouvel objet dans votre hiérarchie, remplacez son nom par TableAnchor dans le panneau Inspector.</span><span class="sxs-lookup"><span data-stu-id="5f32b-139">With the new object selected in your hierarchy, change the name of the object to TableAnchor in the Inspector panel.</span></span> <span data-ttu-id="5f32b-140">De plus, cliquez sur Ajouter un composant et recherchez le composant TableAnchor.</span><span class="sxs-lookup"><span data-stu-id="5f32b-140">Also, click Add Component and search for the TableAnchor component.</span></span> <span data-ttu-id="5f32b-141">Sélectionnez-le et ajoutez-le à l’objet.</span><span class="sxs-lookup"><span data-stu-id="5f32b-141">Select it and add it to the object.</span></span>

    ![Module3Chapter4step7im](images/module3chapter4step7im.PNG)

11. <span data-ttu-id="5f32b-143">À partir du panneau Project dans le dossier Prefabs, faites glisser le préfabriqué Table dans l’objet enfant « TableAnchor » que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="5f32b-143">From the Project panel in the Prefabs folder, drag the Table prefab into the "TableAnchor" child object that you just created.</span></span>

    ![Module3Chapter4step8im](images/module3chapter4step8im.PNG)

## <a name="congratulations"></a><span data-ttu-id="5f32b-145">Félicitations</span><span class="sxs-lookup"><span data-stu-id="5f32b-145">Congratulations</span></span>

<span data-ttu-id="5f32b-146">Une fois cette opération terminée, recherchez le module lunaire.</span><span class="sxs-lookup"><span data-stu-id="5f32b-146">Once this is complete, look around to find the lunar module.</span></span> <span data-ttu-id="5f32b-147">À présent, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le lanceur lunaire.</span><span class="sxs-lookup"><span data-stu-id="5f32b-147">After this, all users that join your Unity project can move the lunar launcher around.</span></span>  <span data-ttu-id="5f32b-148">Tous les mouvements sont synchronisés afin que chaque utilisateur puisse voir les interactions des autres.</span><span class="sxs-lookup"><span data-stu-id="5f32b-148">All movements are synchronized so that each user can see each others' interactions.</span></span> <span data-ttu-id="5f32b-149">Ces concepts servent de composants fondamentaux aux expériences de collaboration complètes et partagées.</span><span class="sxs-lookup"><span data-stu-id="5f32b-149">These concepts serve as the fundamental building blocks for full-featured, shared collaboration experiences.</span></span>

<span data-ttu-id="5f32b-150">Bien que tous les utilisateurs soient connectés dans le cadre d’une expérience partagée et puissent voir les mouvements relatifs des objets, l’application n’est toujours pas en mesure d’aligner correctement les avatars et les objets, de sorte que les utilisateurs locaux ne peuvent pas se voir les uns les autres ni voir les objets situés au même endroit dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="5f32b-150">Although all users are connected as part of a shared experience and can see the relative movements of objects, the application is still unable to accurately align avatars and objects so that local users were not able see each other and objects in the same place within the physical world.</span></span> <span data-ttu-id="5f32b-151">Pour ancrer des expériences partagées locales, chaque appareil nécessite une compréhension commune de l’environnement physique.</span><span class="sxs-lookup"><span data-stu-id="5f32b-151">In order to anchor a local shared experiences, every device requires a common understanding of the physical environment.</span></span> <span data-ttu-id="5f32b-152">Dans ce module, nous allons nous atteler à ce problème en utilisant [Azure Spatial Anchors](<https://azure.microsoft.com//services/spatial-anchors/>) (ASA) que nous allons implémenter dans la prochaine leçon.</span><span class="sxs-lookup"><span data-stu-id="5f32b-152">In this module, we'll achieve this by using [Azure Spatial Anchors](<https://azure.microsoft.com//services/spatial-anchors/>) (ASA) which will be implemented in the next lesson.</span></span>

<span data-ttu-id="5f32b-153">Avant de passer à la leçon suivante, nous allons devoir suivre le module d’apprentissage ASA qui traite des principes fondamentaux d’ASA, de la création de comptes et de ressources Azure, ainsi que d’autres composants fondamentaux nécessaires avant de pouvoir intégrer ASA à notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="5f32b-153">Before proceeding to the next lesson, we'll need to complete the ASA Learning Module that covers ASA basics, Azure account and resource creation, as well as other fundamental buildings blocks required before we can integrate this into our shared experience.</span></span>

<span data-ttu-id="5f32b-154">[Leçon suivante : 5. Intégration d’ancres spatiales Azure dans une expérience partagée](mrlearning-sharing(photon)-ch5.md)</span><span class="sxs-lookup"><span data-stu-id="5f32b-154">[Next Lesson: 5. Integration Azure Spatial Anchors into a shared experience](mrlearning-sharing(photon)-ch5.md)</span></span>
