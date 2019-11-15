---
title: Didacticiels sur les fonctionnalités multi-utilisateur-4. Partage des mouvements d’objets avec plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 34b8165888c13b0c94be8951d5a4fdc07fab5308
ms.sourcegitcommit: 781e47db2ca2f2c792c95e76ac309b44b3535555
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74106034"
---
# <a name="4-sharing-object-movements-with-multiple-users"></a><span data-ttu-id="61a65-105">4. partage des mouvements d’objets avec plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="61a65-105">4. Sharing object movements with multiple users</span></span>

<span data-ttu-id="61a65-106">Dans ce didacticiel, vous allez apprendre à partager les mouvements d’objets afin que tous les participants d’une session partagée puissent collaborer et afficher les interactions entre eux.</span><span class="sxs-lookup"><span data-stu-id="61a65-106">In this Tutorial, you'll learn how to share the movements of objects so that all participants of a shared session can collaborate and view each others' interactions.</span></span> <span data-ttu-id="61a65-107">Cette leçon s’appuie sur le lanceur lunaire créé dans le cadre des [didacticiels du module de base](mrlearning-base.md).</span><span class="sxs-lookup"><span data-stu-id="61a65-107">This lesson builds upon the Lunar Launcher that was built as part of the [Base Module Tutorials](mrlearning-base.md).</span></span>

<span data-ttu-id="61a65-108">Cherché</span><span class="sxs-lookup"><span data-stu-id="61a65-108">Objectives:</span></span>

- <span data-ttu-id="61a65-109">Amener le lanceur lunaire en tant que modèle 3D à partager</span><span class="sxs-lookup"><span data-stu-id="61a65-109">Bring in the lunar launcher as the 3D model to be shared</span></span>
- <span data-ttu-id="61a65-110">Configurer votre projet pour partager les mouvements du modèle 3D</span><span class="sxs-lookup"><span data-stu-id="61a65-110">Configure your project to share the movements of the 3D model</span></span>
- <span data-ttu-id="61a65-111">Découvrez comment créer une application collaborative multi-utilisateur de base</span><span class="sxs-lookup"><span data-stu-id="61a65-111">Learn how to build a basic multi-user collaborative application</span></span>

## <a name="instructions"></a><span data-ttu-id="61a65-112">Instructions</span><span class="sxs-lookup"><span data-stu-id="61a65-112">Instructions</span></span>


1. <span data-ttu-id="61a65-113">Enregistrez la scène de la leçon précédente (contrôle + S).</span><span class="sxs-lookup"><span data-stu-id="61a65-113">Save the scene from the previous lesson (Control+S).</span></span> <span data-ttu-id="61a65-114">Vous pouvez le nommer HLSharedProjectMainPart4. Unity pour qu’il soit plus facile à trouver lorsque vous en avez besoin.</span><span class="sxs-lookup"><span data-stu-id="61a65-114">You can name it HLSharedProjectMainPart4.unity so it's easier to find when you need it.</span></span>

2. <span data-ttu-id="61a65-115">Dans la fenêtre projet, dans le dossier Ressources-> scripts, double-cliquez sur GenericNetSync pour l’ouvrir dans Visual Studio ou dans l’éditeur de code que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="61a65-115">From the Project window, in the Assets->Scripts folder, double-click GenericNetSync to open it in Visual Studio or which ever code editor you are using.</span></span>  

![module3chapter4updatestep2](images/module3chapter4updatestep2.png)

3. <span data-ttu-id="61a65-117">Sur les lignes 34 et 38, supprimez « // » pour activer le code de la table que vous allez utiliser dans cette leçon.</span><span class="sxs-lookup"><span data-stu-id="61a65-117">On Lines 34 and 38, remove "//" to activate the code for the table that you will use in this lesson.</span></span> <span data-ttu-id="61a65-118">Ensuite, enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="61a65-118">Next, save the file.</span></span> 

![module3chapter4updatestep3](images/module3chapter4updatestep3.png)

4. <span data-ttu-id="61a65-120">Dans la fenêtre projet, double-cliquez sur le fichier PhotonRoom.cs dans le dossier Ressources-> scripts pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61a65-120">In the Project window, double-click the PhotonRoom.cs file in the Assets->Scripts folder to open it in Visual Studio.</span></span> 

![module3chapter4updatestep4](images/module3chapter4updatestep4.png)

5. <span data-ttu-id="61a65-122">Comme à l’étape 3, vous devez supprimer « // » pour activer le code aux lignes 25, 26 et 106.</span><span class="sxs-lookup"><span data-stu-id="61a65-122">Just like in Step 3, we need to remove "//" to activate the code at Lines 25, 26, and 106.</span></span>

![module3chapter4updatestep5a](images/module3chapter4updatestep5a.png) 

![module3chapter4updatestep5b](images/module3chapter4updatestep5b.png)

6. <span data-ttu-id="61a65-125">Dans l’affichage des hiérarchies, sélectionnez l’objet NetworkRoom.</span><span class="sxs-lookup"><span data-stu-id="61a65-125">In the Hierarchy view, select the NetworkRoom object.</span></span>

![module3chapter4updatestep6](images/module3chapter4updatestep6.png)

7. <span data-ttu-id="61a65-127">Dans la vue de projet, accédez à ressources-> Ressources-> Prefabs.</span><span class="sxs-lookup"><span data-stu-id="61a65-127">In the Project view, navigate to Assets->Resources->Prefabs.</span></span> <span data-ttu-id="61a65-128">Tout d’abord, glissez-déplacez la table Prefab vers l’emplacement Tableprefab sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="61a65-128">First, drag and drop the Table prefab to the Tableprefab slot on the PhotonRoom class.</span></span> <span data-ttu-id="61a65-129">Ensuite, faites glisser et déposez RocketLauncherCompleteVariantprefab sur l’emplacement Prefab du module sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="61a65-129">Next, drag and drop the RocketLauncherCompleteVariantprefab to the Module Prefab slot on the PhotonRoom class.</span></span>

![module3chapter4updatestep7](images/module3chapter4updatestep7.png)

<span data-ttu-id="61a65-131">Remarque : Si vous cliquez sur l’un des objets Prefab et que vous la libérez, l’inspecteur bascule sur cet objet.</span><span class="sxs-lookup"><span data-stu-id="61a65-131">Note: If you click one of the prefab objects and release, the inspector will switch to that object.</span></span> <span data-ttu-id="61a65-132">Cliquez sur, faites glisser, déposez et relâchez chaque objet à l’emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="61a65-132">Click, drag, drop, and release each object to its appropriate slot.</span></span>

8. <span data-ttu-id="61a65-133">Cliquez sur la flèche à gauche de MixedRealityPlayspace et déplacez l’objet de jeu enfant MainCamera vers le bas dans le Prefab SharedPlayground.</span><span class="sxs-lookup"><span data-stu-id="61a65-133">Click the arrow to the left of MixedRealityPlayspace and move the child game object MainCamera down into the SharedPlayground prefab.</span></span> <span data-ttu-id="61a65-134">Ensuite, supprimez le Prefab, MixedRealityPlayspace en sélectionnant le Prefab et appuyez sur « supprimer » sur votre clavier).</span><span class="sxs-lookup"><span data-stu-id="61a65-134">Next, delete the prefab, MixedRealityPlayspace by selecting the prefab and tap "delete" on your keyboard).</span></span>
<span data-ttu-id="61a65-135">![Module3hapter4step5im](images/module3chapter4step5im.PNG)</span><span class="sxs-lookup"><span data-stu-id="61a65-135">![Module3hapter4step5im](images/module3chapter4step5im.PNG)</span></span>

><span data-ttu-id="61a65-136">Remarque : Assurez-vous que les positions caméra principale et SharedPlayground sont définies sur 0, 0, 0.</span><span class="sxs-lookup"><span data-stu-id="61a65-136">Note:  Make sure that both the Main Camera and SharedPlayground positions are set to 0,0,0.</span></span>
>

9. <span data-ttu-id="61a65-137">Sélectionnez l’objet « SharedPlayground » et cliquez avec le bouton droit sur la souris pour choisir l’option « créer vide » afin de créer un objet de jeu vide en tant qu’enfant de l’objet de jeu « SharedPlayground ».</span><span class="sxs-lookup"><span data-stu-id="61a65-137">Select "SharedPlayground" object and right click the mouse to choose "create empty" option to create an empty game object as a child of "SharedPlayground" game object.</span></span>

   ![Module3chapter4step6im](images/module3chapter4step6im.PNG)

10. <span data-ttu-id="61a65-139">Après avoir sélectionné le nouvel objet dans votre hiérarchie, remplacez le nom de l’objet par TableAnchor dans le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="61a65-139">With the new object selected in your hierarchy, change the name of the object to TableAnchor in the Inspector panel.</span></span> <span data-ttu-id="61a65-140">En outre, cliquez sur Ajouter un composant et recherchez le composant TableAnchor.</span><span class="sxs-lookup"><span data-stu-id="61a65-140">Also, click Add Component and search for the TableAnchor component.</span></span> <span data-ttu-id="61a65-141">Sélectionnez-le et ajoutez-le à l’objet.</span><span class="sxs-lookup"><span data-stu-id="61a65-141">Select it and add it to the object.</span></span> 

![Module3Chapter4step7im](images/module3chapter4step7im.PNG)

11. <span data-ttu-id="61a65-143">À partir du panneau projet dans le dossier Prefabs, faites glisser la table Prefab dans l’objet enfant « TableAnchor » que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="61a65-143">From the Project panel in the Prefabs folder, drag the Table prefab into the "TableAnchor" child object that you just created.</span></span>

![Module3Chapter4step8im](images/module3chapter4step8im.PNG)

12. <span data-ttu-id="61a65-145">Dans l’objet DebugWindow, remplacez la largeur par 50 et la hauteur par 20.</span><span class="sxs-lookup"><span data-stu-id="61a65-145">In the DebugWindow object, change the width to 50 and the height to 20.</span></span>

![Module3Chapter4step9im](images/module3chapter4step11im.PNG)

## <a name="congratulations"></a><span data-ttu-id="61a65-147">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="61a65-147">Congratulations</span></span>


<span data-ttu-id="61a65-148">Une fois cette opération terminée, recherchez le module lunaire.</span><span class="sxs-lookup"><span data-stu-id="61a65-148">Once this is complete, look around to find the lunar module.</span></span> <span data-ttu-id="61a65-149">Après cela, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le lanceur lunaire.</span><span class="sxs-lookup"><span data-stu-id="61a65-149">After this, all users that join your Unity project can move the lunar launcher around.</span></span>  <span data-ttu-id="61a65-150">Tous les mouvements sont synchronisés afin que chaque utilisateur puisse voir les interactions entre eux.</span><span class="sxs-lookup"><span data-stu-id="61a65-150">All movements are synchronized so that each user can see each others' interactions.</span></span> <span data-ttu-id="61a65-151">Ces concepts constituent les blocs de construction fondamentaux pour les expériences de collaboration complètes et partagées.</span><span class="sxs-lookup"><span data-stu-id="61a65-151">These concepts serve as the fundamental building blocks for full-featured, shared collaboration experiences.</span></span> 

<span data-ttu-id="61a65-152">Bien que tous les utilisateurs soient connectés dans le cadre d’une expérience partagée et puissent voir les mouvements relatifs des objets, l’application n’est toujours pas en mesure d’aligner correctement les avatars et les objets, de sorte que les utilisateurs locaux n’ont pas pu voir les autres et les objets dans le même emplacement dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="61a65-152">Although all users are connected as part of a shared experience and can see the relative movements of objects, the application is still unable to accurately align avatars and objects so that local users were not able see each other and objects in the same place within the physical world.</span></span> <span data-ttu-id="61a65-153">Pour pouvoir ancrer des expériences partagées locales, chaque appareil doit avoir une compréhension commune de l’environnement physique.</span><span class="sxs-lookup"><span data-stu-id="61a65-153">In order to anchor a local shared experiences, every device requires a common understanding of the physical environment.</span></span> <span data-ttu-id="61a65-154">Dans ce module, nous allons y parvenir en utilisant les [ancres spatiales Azure](<https://azure.microsoft.com//services/spatial-anchors/>) (ASA) qui seront implémentées dans la prochaine leçon.</span><span class="sxs-lookup"><span data-stu-id="61a65-154">In this module, we'll achieve this by using [Azure Spatial Anchors](<https://azure.microsoft.com//services/spatial-anchors/>) (ASA) which will be implemented in the next lesson.</span></span>

<span data-ttu-id="61a65-155">Avant de passer à la leçon suivante, nous devrons suivre le module ASA Learning qui traite des principes fondamentaux de ASA, de la création de comptes et de ressources Azure, ainsi que d’autres blocs de construction fondamentaux nécessaires avant de pouvoir intégrer cela dans notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="61a65-155">Before proceeding to the next lesson, we'll need to complete the ASA Learning Module that covers ASA basics, Azure account and resource creation, as well as other fundamental buildings blocks required before we can integrate this into our shared experience.</span></span>

<span data-ttu-id="61a65-156">[Leçon suivante : 5. intégration des ancres spatiales Azure dans une expérience partagée](mrlearning-sharing(photon)-ch5.md)</span><span class="sxs-lookup"><span data-stu-id="61a65-156">[Next Lesson: 5. Integration Azure Spatial Anchors into a shared experience](mrlearning-sharing(photon)-ch5.md)</span></span>

