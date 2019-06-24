---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: a67eaef45582054b62198a563f0ee01724fd60db
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67327443"
---
# <a name="synchronizing-the-movements-of-shared-objects"></a><span data-ttu-id="e9ac2-104">Synchronisation des mouvements des objets partagés</span><span class="sxs-lookup"><span data-stu-id="e9ac2-104">Synchronizing the Movements of Shared Objects</span></span>

<span data-ttu-id="e9ac2-105">Dans cette leçon, nous allez apprendre à partager les mouvements des objets afin que tous les participants d’une session partagée peuvent collaborer et afficher leurs interactions.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-105">In this lesson, we will learn how to share the movements of objects so that all participants of a shared session can collaborate together and view each others' interactions.</span></span> <span data-ttu-id="e9ac2-106">Cette leçon repose sur le Lanceur lunaire qui a été créé dans le cadre de la [didacticiels de Module de Base](mrlearning-base.md).</span><span class="sxs-lookup"><span data-stu-id="e9ac2-106">This lesson builds upon the Lunar Launcher that was built as part of the [Base Module Tutorials](mrlearning-base.md).</span></span>

<span data-ttu-id="e9ac2-107">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="e9ac2-107">Objectives:</span></span>

- <span data-ttu-id="e9ac2-108">Importer le Lanceur lunaire terminé en tant que le modèle 3D à partager</span><span class="sxs-lookup"><span data-stu-id="e9ac2-108">Import the completed Lunar Launcher as the 3D model to be shared</span></span>
- <span data-ttu-id="e9ac2-109">Configurer votre projet pour partager les mouvements d’un modèle 3D.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-109">Configure your project to share the movements of the 3D model.</span></span>
- <span data-ttu-id="e9ac2-110">Découvrez comment créer une application de collaboration multi-utilisateur base</span><span class="sxs-lookup"><span data-stu-id="e9ac2-110">Learn how to build a basic multi-user collaborative application</span></span>

### <a name="instructions"></a><span data-ttu-id="e9ac2-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="e9ac2-111">Instructions</span></span>

1. <span data-ttu-id="e9ac2-112">Enregistrer la scène à partir de la leçon précédente (CTRL + S).</span><span class="sxs-lookup"><span data-stu-id="e9ac2-112">Save the scene from the previous lesson (control+S).</span></span> <span data-ttu-id="e9ac2-113">Vous pouvez le nommer « HLSharedProjectMainPart4.unity » afin qu’il soit plus facile à trouver lorsque vous en avez besoin à nouveau.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-113">You may name it "HLSharedProjectMainPart4.unity" so that it's easier to find when you need it again.</span></span>

2. <span data-ttu-id="e9ac2-114">Supprimer l’objet « NetworkLobby » (en le sélectionnant et en appuyant sur Supprimer).</span><span class="sxs-lookup"><span data-stu-id="e9ac2-114">Delete the "NetworkLobby" object (by selecting it and pressing delete).</span></span> <span data-ttu-id="e9ac2-115">En outre, accédez dans le dossier « prefabs » à partir de la leçon 2 et supprimer le préfabriqué « NetworkLobby » à partir de là aussi.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-115">Also, go into the "prefabs" folder from lesson 2 and delete the "NetworkLobby" prefab from there as well.</span></span>

![Module3Chapter4tep2im](images/module3chapter4step2im.PNG)

3. <span data-ttu-id="e9ac2-117">Importer un nouveau package personnalisé (par exemple, l’étape 2 de la leçon 2) et importer le [LunarModule.unitypackage](linkforModule1 lesson with the lunar module) et [NetworkLobbyReplacement.unitypackage.](linkforNetworklobbyreplacement package here)</span><span class="sxs-lookup"><span data-stu-id="e9ac2-117">Import a new custom package (like step 2 from the lesson 2) and import the [LunarModule.unitypackage](linkforModule1 lesson with the lunar module) and the [NetworkLobbyReplacement.unitypackage.](linkforNetworklobbyreplacement package here)</span></span>

![Module3Chapter4step3im](images/module3chapter4step3im.PNG)

4. <span data-ttu-id="e9ac2-119">Maintenant, dans le dossier « prefabs », faites glisser la nouvelle préfabriqué « NetworkLobby » dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-119">Now, in the "prefabs" folder, drag the new "NetworkLobby" prefab into the hierarchy .</span></span> 

![Module3hapter4step4im](images/module3chapter4step4im.PNG)

> <span data-ttu-id="e9ac2-121">Remarque : les deux packages, nous avons importé dans les étapes précédentes mises à jour le préfabriqué « NetworkLobby ».</span><span class="sxs-lookup"><span data-stu-id="e9ac2-121">note: the two packages we imported in the previous steps updated the "NetworkLobby" prefab.</span></span> <span data-ttu-id="e9ac2-122">Il vous évite beaucoup de saisie !</span><span class="sxs-lookup"><span data-stu-id="e9ac2-122">It saves you from a lot of typing!</span></span>

5. <span data-ttu-id="e9ac2-123">Maintenant, cliquez sur la flèche à gauche de « MixedRealityPlayspace » et déplacer l’objet de jeu d’enfant, « MainCamera » vers le bas dans le préfabriqué « SharedPlayground ».</span><span class="sxs-lookup"><span data-stu-id="e9ac2-123">Now, click the arrow to the left of "MixedRealityPlayspace" and move the child game object, "MainCamera" down into the "SharedPlayground" prefab.</span></span> <span data-ttu-id="e9ac2-124">Ensuite, supprimez le prefab « MixedRealityPlayspace » (pour les supprimer, sélectionnez le préfabriqué et appuyez sur « Supprimer » de votre clavier).</span><span class="sxs-lookup"><span data-stu-id="e9ac2-124">Then, delete the prefab "MixedRealityPlayspace" (to delete, select the prefab and tap "delete" on your keyboard).</span></span>

![Module3hapter4step5im](images/module3chapter4step5im.PNG)

6. <span data-ttu-id="e9ac2-126">Créer un nouvel objet de jeu définie en tant qu’objet enfant à l’objet parent de « SharedPlayground » (pour créer un nouvel objet, cliquez avec le bouton droit sur l’objet parent et sélectionnez « Créer vide »).</span><span class="sxs-lookup"><span data-stu-id="e9ac2-126">Create a new game object set as a child object to the "SharedPlayground" parent object (to create a new object, right click on the parent object, and select "create  empty").</span></span>
7. <span data-ttu-id="e9ac2-127">Avec le nouvel objet sélectionné dans votre hiérarchie, modifier le nom de l’objet à « TableAnchor » dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-127">With the new object selected in your hierarchy, change the name of the object to "TableAnchor" in the inspector panel.</span></span> <span data-ttu-id="e9ac2-128">En outre, cliquez sur « Ajouter un composant » et recherchez le composant « TableAnchor ».</span><span class="sxs-lookup"><span data-stu-id="e9ac2-128">Also, click "add component" and search for the "TableAnchor" component.</span></span> <span data-ttu-id="e9ac2-129">Sélectionnez-le et ajoutez-le à l’objet.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-129">Select it and add it to the object.</span></span>

![Module3Chapter4step6im](images/module3chapter4step7im.PNG)

> <span data-ttu-id="e9ac2-131">Remarque : définir le positionnement à x = 1, y =-0,55 et z = 2.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-131">note: set the positioning to x=1, y=-0.55, and z=2.</span></span> <span data-ttu-id="e9ac2-132">En outre, la valeur est la rotation y = 90.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-132">Also, set the rotation to y=90.</span></span> 
>
> ![Module3Chapter4step6im](images/module3chapter4noteim.PNG)

8. <span data-ttu-id="e9ac2-134">Maintenant dans le volet de projet, dans le dossier « prefabs », faites glisser le préfabriqué « table » dans l’objet enfant de « TableAnchor » vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-134">Now in the project panel, in the "prefabs" folder, drag the "table" prefab into the "TableAnchor" child object you just created.</span></span>

   ![Module3Chapter4step8im](images/module3chapter4step8im.PNG)

9. <span data-ttu-id="e9ac2-136">Sélectionnez « NetworkRoom », un objet enfant sous « NetworkLobby » dans la hiérarchie et cliquez sur « Ajouter un composant » dans le panneau Inspecteur et recherchez « PhotonView » et ajoutez le script à la «*NetworkRoom*« objet.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-136">Select "NetworkRoom," a child object under "NetworkLobby" in the hierachy, and click "add component" in the inspector panel and search for "PhotonView" and add the script to the "*NetworkRoom*" object.</span></span>

![Module3Chapter4step9im](images/module3chapter4step9im.PNG)

11. <span data-ttu-id="e9ac2-138">Enfin, dans l’objet « DebugWindow », modifiez la largeur à 80 et la hauteur de 10.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-138">Finally, in the "DebugWindow" object, change the width to 80 and the height to 10.</span></span>

![Module3Chapter4step9im](images/module3chapter4step11im.PNG)




## <a name="congratulations"></a><span data-ttu-id="e9ac2-140">Félicitations</span><span class="sxs-lookup"><span data-stu-id="e9ac2-140">Congratulations</span></span>

<span data-ttu-id="e9ac2-141">Une fois cette opération terminée, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le Lanceur lunaire.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-141">Once this is complete, all users that join your Unity project can move the Lunar Launcher around.</span></span> <span data-ttu-id="e9ac2-142">Tous les mouvements sont synchronisés afin que chaque utilisateur peut voir les uns des autres interactions.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-142">All movements are synchronized so that each user can see each others' interactions.</span></span> <span data-ttu-id="e9ac2-143">Ces concepts servent comme blocs de construction fondamentaux pour des expériences complètes de collaboration partagées.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-143">These concepts serve as the foundational building blocks for full-featured shared collaboration experiences.</span></span> 

<span data-ttu-id="e9ac2-144">Bien que tous les utilisateurs sont connectés dans le cadre de l’expérience partagée et voyez les mouvements relatifs des objets, l’application est toujours Impossible d’aligner précisément les objets et les avatars afin que les utilisateurs locaux voient les uns des autres et les objets au même endroit dans physique World.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-144">Although all users are connected as part of a shared experience and can see the relative movements of objects, the application is still unable to accurately align avatars and objects so that local users see each other and objects in the same place within the physical world.</span></span> <span data-ttu-id="e9ac2-145">Pour ancrer un expériences partagées local, chaque appareil nécessite une compréhension commune de l’environnement physique.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-145">In order to anchor a local shared experiences, every device requires a common understanding of the physical environment.</span></span> <span data-ttu-id="e9ac2-146">Dans ce module, il peut y parvenir à l’aide de [ancres Spatial Azure](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA), qui seront implémenté dans la leçon suivante.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-146">In this module, we will achieve this using [Azure Spatial Anchors](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA), which will be implemented in the next lesson.</span></span>

<span data-ttu-id="e9ac2-147">Avant de passer à la leçon suivante, nous devrons effectuer le Module de formation ASA, qui couvre principes de base ASA, compte Azure et la création de ressources et d’autres blocs de bâtiments fondamentales nécessaires avant que nous pouvons intégrer cela dans notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="e9ac2-147">Before proceeding to the next lesson, we will need to complete the ASA Learning Module, which will cover ASA basics, Azure account and resource creation, and other fundamental buildings blocks required before we can integrate this into our shared experience.</span></span>

<span data-ttu-id="e9ac2-148">[Leçon suivante : Sharing(Photon) leçon 5](mrlearning-sharing(photon)-ch5.md)</span><span class="sxs-lookup"><span data-stu-id="e9ac2-148">[Next Lesson: Sharing(Photon) Lesson 5](mrlearning-sharing(photon)-ch5.md)</span></span>

