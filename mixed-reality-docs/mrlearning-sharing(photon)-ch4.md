---
title: Module de partage d’apprentissage MR pour HoloLens 2
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 3e4be00ddeab6d91dbbc8226bfa3dc543cded095
ms.sourcegitcommit: 611af6ff7a2412abad80c0c7d4decfc0c3a0e8c8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/17/2019
ms.locfileid: "68293676"
---
# <a name="4-sharing-object-movements-with-multiple-users"></a><span data-ttu-id="371d5-104">4. Partage des mouvements d’objets avec plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="371d5-104">4. Sharing object movements with multiple users</span></span>

<span data-ttu-id="371d5-105">Dans ce didacticiel, nous apprenons à partager les mouvements d’objets afin que tous les participants d’une session partagée puissent collaborer et afficher les interactions entre eux.</span><span class="sxs-lookup"><span data-stu-id="371d5-105">In this Tutorial, we learn how to share the movements of objects so that all participants of a shared session can collaborate together and view each others' interactions.</span></span> <span data-ttu-id="371d5-106">Cette leçon s’appuie sur le lanceur lunaire créé dans le cadre des [didacticiels du module de base](mrlearning-base.md).</span><span class="sxs-lookup"><span data-stu-id="371d5-106">This lesson builds upon the Lunar Launcher that was built as part of the [Base Module Tutorials](mrlearning-base.md).</span></span>

<span data-ttu-id="371d5-107">Cherché</span><span class="sxs-lookup"><span data-stu-id="371d5-107">Objectives:</span></span>

- <span data-ttu-id="371d5-108">Amener le lanceur lunaire en tant que modèle 3D à partager</span><span class="sxs-lookup"><span data-stu-id="371d5-108">Bring in the lunar launcher as the 3D model to be shared</span></span>
- <span data-ttu-id="371d5-109">Configurez votre projet pour partager les mouvements du modèle 3D.</span><span class="sxs-lookup"><span data-stu-id="371d5-109">Configure your project to share the movements of the 3D model.</span></span>
- <span data-ttu-id="371d5-110">Découvrez comment créer une application collaborative multi-utilisateur de base</span><span class="sxs-lookup"><span data-stu-id="371d5-110">Learn how to build a basic multi-user collaborative application</span></span>

### <a name="instructions"></a><span data-ttu-id="371d5-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="371d5-111">Instructions</span></span>


1. <span data-ttu-id="371d5-112">Enregistrez la scène de la leçon précédente (contrôle + S).</span><span class="sxs-lookup"><span data-stu-id="371d5-112">Save the scene from the previous lesson (Control+S).</span></span> <span data-ttu-id="371d5-113">Vous pouvez le nommer, HLSharedProjectMainPart4. Unity, afin qu’il soit plus facile à trouver lorsque vous en avez besoin.</span><span class="sxs-lookup"><span data-stu-id="371d5-113">You can name it, HLSharedProjectMainPart4.unity, so that it's easier to find when you need it.</span></span>

2. <span data-ttu-id="371d5-114">Dans la fenêtre projet, dans le dossier Ressources-> scripts, double-cliquez sur GenericNetSync pour l’ouvrir dans Visual Studio ou dans l’éditeur de code que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="371d5-114">From the Project window, in the Assets->Scripts folder, double click on GenericNetSync to open it in Visual Studio or which ever code editor you are using.</span></span>  

![module3chapter4updatestep2](images/module3chapter4updatestep2.png)

3. <span data-ttu-id="371d5-116">Sur les lignes 34 et 38, supprimez le//pour activer le code de la table que nous allons utiliser dans cette leçon.</span><span class="sxs-lookup"><span data-stu-id="371d5-116">On Lines 34 and 38, remove the // to activate the code for the table that we will use in this lesson.</span></span> <span data-ttu-id="371d5-117">Ensuite, enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="371d5-117">next, Save the file.</span></span> 

![module3chapter4updatestep3](images/module3chapter4updatestep3.png)

4. <span data-ttu-id="371d5-119">Dans la fenêtre projet, double-cliquez sur le fichier PhotonRoom.cs dans le dossier Ressources-> scripts pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="371d5-119">In the Project window, double click on the PhotonRoom.cs file in the Assets->Scripts folder to open it in Visual Studio.</span></span> 

![module3chapter4updatestep4](images/module3chapter4updatestep4.png)

5. <span data-ttu-id="371d5-121">Comme à l’étape 3, vous devez supprimer le//pour activer le code aux lignes 25, 26 et 106.</span><span class="sxs-lookup"><span data-stu-id="371d5-121">Just like in Step 3, we need to remove the // to activate the code at Lines 25, 26, and 106.</span></span>

![module3chapter4updatestep5a](images/module3chapter4updatestep5a.png) 

![module3chapter4updatestep5b](images/module3chapter4updatestep5b.png)

6. <span data-ttu-id="371d5-124">Dans l’affichage des hiérarchies, sélectionnez l’objet NetworkRoom.</span><span class="sxs-lookup"><span data-stu-id="371d5-124">In the Hierarchy view, select the NetworkRoom object.</span></span>

![module3chapter4updatestep6](images/module3chapter4updatestep6.png)

7. <span data-ttu-id="371d5-126">Dans la vue de projet, accédez à ressources-> Ressources-> Prefabs.</span><span class="sxs-lookup"><span data-stu-id="371d5-126">In the Project view, navigate to Assets->Resources->Prefabs.</span></span> <span data-ttu-id="371d5-127">Tout d’abord, glissez-déplacez la table Prefab vers l’emplacement Tableprefab sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="371d5-127">First, drag and drop the Table prefab to the Tableprefab slot on the PhotonRoom class.</span></span> <span data-ttu-id="371d5-128">Ensuite, faites glisser et déposez le Prefab LunarModule vers l’emplacement Prefab de module sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="371d5-128">Next drag and drop the LunarModule prefab to the Module Prefab slot on the PhotonRoom class.</span></span>

![module3chapter4updatestep7](images/module3chapter4updatestep7.png)

   <span data-ttu-id="371d5-130">Remarque : Si vous cliquez sur l’un des objets Prefab et la version Release, l’inspecteur bascule sur cet objet.</span><span class="sxs-lookup"><span data-stu-id="371d5-130">Note: If you click on one of the prefab objects and release, the inspector will switch to that object.</span></span> <span data-ttu-id="371d5-131">Cliquez sur, faites glisser, déposez et relâchez chaque objet à l’emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="371d5-131">Click, drag, drop, and release each object to its appropriate slot.</span></span>

8. <span data-ttu-id="371d5-132">Cliquez sur la flèche à gauche de MixedRealityPlayspace et déplacez l’objet de jeu enfant, MainCamera vers le bas dans le Prefab SharedPlayground.</span><span class="sxs-lookup"><span data-stu-id="371d5-132">Click the arrow to the left of MixedRealityPlayspace, and move the child game object, MainCamera down into the SharedPlayground prefab.</span></span> <span data-ttu-id="371d5-133">Ensuite, supprimez le Prefab, MixedRealityPlayspace, à supprimer, sélectionnez le Prefab, puis appuyez sur «supprimer» sur votre clavier).</span><span class="sxs-lookup"><span data-stu-id="371d5-133">Next, delete the prefab, MixedRealityPlayspace, to delete, select the prefab, and tap "delete" on your keyboard).</span></span>
<span data-ttu-id="371d5-134">![Module3hapter4step5im](images/module3chapter4step5im.PNG)</span><span class="sxs-lookup"><span data-stu-id="371d5-134">![Module3hapter4step5im](images/module3chapter4step5im.PNG)</span></span>

><span data-ttu-id="371d5-135">Remarque :  Assurez-vous que les positions caméra principale et SharedPlayground sont définies sur 0, 0, 0.</span><span class="sxs-lookup"><span data-stu-id="371d5-135">Note:  Make sure that both the Main Camera and SharedPlayground positions are set to 0,0,0.</span></span>
>

9. <span data-ttu-id="371d5-136">Créez un nouvel objet de jeu défini en tant qu’objet enfant sur l’objet parent SharedPlayground pour créer un objet.</span><span class="sxs-lookup"><span data-stu-id="371d5-136">Create a new game object set as a child object to the SharedPlayground parent object to create a new object.</span></span> <span data-ttu-id="371d5-137">Cliquez avec le bouton droit sur l’objet parent, puis sélectionnez Créer vide.</span><span class="sxs-lookup"><span data-stu-id="371d5-137">Right click on the parent object, and select Create Empty.</span></span> 

10. <span data-ttu-id="371d5-138">Après avoir sélectionné le nouvel objet dans votre hiérarchie, remplacez le nom de l’objet par TableAnchor dans le panneau Inspecteur.</span><span class="sxs-lookup"><span data-stu-id="371d5-138">With the new object selected in your hierarchy, change the name of the object to TableAnchor in the Inspector panel.</span></span> <span data-ttu-id="371d5-139">En outre, cliquez sur Ajouter un composant, puis recherchez le composant TableAnchor.</span><span class="sxs-lookup"><span data-stu-id="371d5-139">Also, click Add Component, and search for the TableAnchor component.</span></span> <span data-ttu-id="371d5-140">Sélectionnez-le et ajoutez-le à l’objet.</span><span class="sxs-lookup"><span data-stu-id="371d5-140">Select it and add it to the object.</span></span> 

![Module3Chapter4step6im](images/module3chapter4step7im.PNG)

> <span data-ttu-id="371d5-142">Remarque : Définissez le positionnement sur x = 1, y =-0,55 et z = 2.</span><span class="sxs-lookup"><span data-stu-id="371d5-142">Note: Set the positioning to x=1, y=-0.55, and z=2.</span></span> <span data-ttu-id="371d5-143">En outre, définissez la rotation sur y = 90.</span><span class="sxs-lookup"><span data-stu-id="371d5-143">Also, set the rotation to y=90.</span></span> 
>
> ![Module3Chapter4step6im](images/module3chapter4noteim.PNG)

11. <span data-ttu-id="371d5-145">À présent, à partir du panneau projet dans le dossier Prefabs, faites glisser la table Prefab dans l’objet enfant «TableAnchor» que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="371d5-145">Now from the Project panel in the Prefabs folder, drag the Table prefab into the "TableAnchor" child object you just created.</span></span>

![Module3Chapter4step8im](images/module3chapter4step8im.PNG)

12. <span data-ttu-id="371d5-147">Enfin, dans l’objet DebugWindow, remplacez la largeur par 50 et la hauteur par 20.</span><span class="sxs-lookup"><span data-stu-id="371d5-147">Finally, in the DebugWindow object, change the width to 50 and the height to 20.</span></span>

![Module3Chapter4step9im](images/module3chapter4step11im.PNG)

## <a name="congratulations"></a><span data-ttu-id="371d5-149">Félicitations</span><span class="sxs-lookup"><span data-stu-id="371d5-149">Congratulations</span></span>


<span data-ttu-id="371d5-150">Une fois cette opération terminée, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le lanceur lunaire.</span><span class="sxs-lookup"><span data-stu-id="371d5-150">Once this is complete, all users that join your Unity project can move the lunar launcher around.</span></span> <span data-ttu-id="371d5-151">Tous les mouvements sont synchronisés afin que chaque utilisateur puisse voir les interactions entre eux.</span><span class="sxs-lookup"><span data-stu-id="371d5-151">All movements are synchronized so that each user can see each others' interactions.</span></span> <span data-ttu-id="371d5-152">Ces concepts constituent les blocs de construction fondamentaux pour les expériences de collaboration complètes et partagées.</span><span class="sxs-lookup"><span data-stu-id="371d5-152">These concepts serve as the fundamental building blocks for full-featured, shared collaboration experiences.</span></span> 

<span data-ttu-id="371d5-153">Bien que tous les utilisateurs soient connectés dans le cadre d’une expérience partagée et puissent voir les mouvements relatifs des objets, l’application n’est toujours pas en mesure d’aligner avec précision les avatars et les objets afin que les utilisateurs locaux puissent voir les objets et les objets dans le même emplacement au sein du réelles.</span><span class="sxs-lookup"><span data-stu-id="371d5-153">Although all users are connected as part of a shared experience, and can see the relative movements of objects, the application is still unable to accurately align avatars and objects so that local users see each other and objects in the same place within the physical world.</span></span> <span data-ttu-id="371d5-154">Pour pouvoir ancrer des expériences partagées locales, chaque appareil doit avoir une compréhension commune de l’environnement physique.</span><span class="sxs-lookup"><span data-stu-id="371d5-154">In order to anchor a local shared experiences, every device requires a common understanding of the physical environment.</span></span> <span data-ttu-id="371d5-155">Dans ce module, nous allons y parvenir en utilisant les [ancres spatiales Azure](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA) qui seront implémentées dans la prochaine leçon.</span><span class="sxs-lookup"><span data-stu-id="371d5-155">In this module, we'll achieve this by using [Azure Spatial Anchors](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA) that will be implemented in the next lesson.</span></span>

<span data-ttu-id="371d5-156">Avant de passer à la leçon suivante, nous devrons suivre le module ASA Learning qui traite des principes fondamentaux de ASA, de la création de comptes et de ressources Azure, ainsi que d’autres blocs de construction fondamentaux nécessaires avant de pouvoir les intégrer dans notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="371d5-156">Before proceeding to the next lesson, we'll need to complete the ASA Learning Module that covers ASA basics, Azure account and resource creation, and other fundamental buildings blocks required before we can integrate this into our shared experience.</span></span>

<span data-ttu-id="371d5-157">[Leçon suivante : Leçon 5 sur le partage (photon)](mrlearning-sharing(photon)-ch5.md)</span><span class="sxs-lookup"><span data-stu-id="371d5-157">[Next Lesson: Sharing(Photon) Lesson 5](mrlearning-sharing(photon)-ch5.md)</span></span>

