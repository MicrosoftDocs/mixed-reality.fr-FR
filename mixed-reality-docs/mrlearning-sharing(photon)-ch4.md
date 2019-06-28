---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: d5bed61f5ffc1d3b4efed96f47c3568fbf3a2948
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67416010"
---
# <a name="synchronizing-the-movements-of-shared-objects"></a><span data-ttu-id="eceb7-104">Synchronisation des mouvements des objets partagés</span><span class="sxs-lookup"><span data-stu-id="eceb7-104">Synchronizing the Movements of Shared Objects</span></span>

<span data-ttu-id="eceb7-105">Dans cette leçon, nous allez apprendre à partager les mouvements des objets afin que tous les participants d’une session partagée peuvent collaborer et afficher leurs interactions.</span><span class="sxs-lookup"><span data-stu-id="eceb7-105">In this lesson, we will learn how to share the movements of objects so that all participants of a shared session can collaborate together and view each others' interactions.</span></span> <span data-ttu-id="eceb7-106">Cette leçon repose sur le Lanceur lunaire qui a été créé dans le cadre de la [didacticiels de Module de Base](mrlearning-base.md).</span><span class="sxs-lookup"><span data-stu-id="eceb7-106">This lesson builds upon the Lunar Launcher that was built as part of the [Base Module Tutorials](mrlearning-base.md).</span></span>

<span data-ttu-id="eceb7-107">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="eceb7-107">Objectives:</span></span>

- <span data-ttu-id="eceb7-108">Remettre dans le Lanceur lunaire que le modèle 3D à partager</span><span class="sxs-lookup"><span data-stu-id="eceb7-108">Bring in the Lunar Launcher as the 3D model to be shared</span></span>
- <span data-ttu-id="eceb7-109">Configurer votre projet pour partager les mouvements d’un modèle 3D.</span><span class="sxs-lookup"><span data-stu-id="eceb7-109">Configure your project to share the movements of the 3D model.</span></span>
- <span data-ttu-id="eceb7-110">Découvrez comment créer une application de collaboration multi-utilisateur base</span><span class="sxs-lookup"><span data-stu-id="eceb7-110">Learn how to build a basic multi-user collaborative application</span></span>

### <a name="instructions"></a><span data-ttu-id="eceb7-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="eceb7-111">Instructions</span></span>

1. <span data-ttu-id="eceb7-112">Enregistrer la scène à partir de la leçon précédente (CTRL + S).</span><span class="sxs-lookup"><span data-stu-id="eceb7-112">Save the scene from the previous lesson (control+S).</span></span> <span data-ttu-id="eceb7-113">Vous pouvez le nommer « HLSharedProjectMainPart4.unity » afin qu’il soit plus facile à trouver lorsque vous en avez besoin à nouveau.</span><span class="sxs-lookup"><span data-stu-id="eceb7-113">You may name it "HLSharedProjectMainPart4.unity" so that it's easier to find when you need it again.</span></span>

2. <span data-ttu-id="eceb7-114">Dans la fenêtre de projet, dans les ressources > dossier Scripts, double-cliquez sur GenericNetSync pour l’ouvrir dans Visual Studio ou qui vous sont à l’aide de l’éditeur de code jamais.</span><span class="sxs-lookup"><span data-stu-id="eceb7-114">In the Project window, in the Assets > Scripts folder, double click on GenericNetSync to open it in Visual Studio or which ever code editor you are using.</span></span>  ![](images/module3chapter4updatestep2.png)

3. <span data-ttu-id="eceb7-115">Sur les lignes 34 et 38, supprimez le « / / » pour activer le code pour la Table que nous utiliserons dans cette leçon.</span><span class="sxs-lookup"><span data-stu-id="eceb7-115">On lines 34 and 38, remove the "//" to activate the code for the Table that we will use in this lesson.</span></span>  <span data-ttu-id="eceb7-116">Puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="eceb7-116">Then Save the file.</span></span> ![](images/module3chapter4updatestep3.png)

4. <span data-ttu-id="eceb7-117">Dans la fenêtre projet, double-cliquez sur le fichier PhotonRoom.cs dans les ressources > dossier de Scripts pour l’ouvrir à nouveau dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eceb7-117">In the project window, double click on the PhotonRoom.cs file in the Assets > Scripts folder to again open it in Visual Studio.</span></span> ![](images/module3chapter4updatestep4.png)

5. <span data-ttu-id="eceb7-118">Comme à l’étape 3, nous devons supprimer le « / / » pour activer le code en lignes 25 et 26 106.![](images/module3chapter4updatestep5a.png)</span><span class="sxs-lookup"><span data-stu-id="eceb7-118">Just like in step 3 we need to remove the "//" to activate the code at lines 25, 26, and 106.![](images/module3chapter4updatestep5a.png)</span></span> ![](images/module3chapter4updatestep5b.png)

6. <span data-ttu-id="eceb7-119">Dans la vue de la hiérarchie, sélectionnez l’objet NetworkRoom.![](images/module3chapter4updatestep6.png)</span><span class="sxs-lookup"><span data-stu-id="eceb7-119">In the Hierarchy view, select the NetworkRoom object.![](images/module3chapter4updatestep6.png)</span></span>

7. <span data-ttu-id="eceb7-120">Dans la vue du projet, accédez aux ressources > ressources > Prefabs.</span><span class="sxs-lookup"><span data-stu-id="eceb7-120">In the project view, navigate to Assets > Resources > Prefabs.</span></span> <span data-ttu-id="eceb7-121">Tout d’abord, faites glisser le préfabriqué de Table à l’emplacement « Tableprefab » sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="eceb7-121">First, drag and drop the Table prefab to the "Tableprefab" slot on the PhotonRoom class.</span></span> <span data-ttu-id="eceb7-122">Ensuite glisser -déplacer le préfabriqué LunarModule vers l’emplacement « Module Prefab » sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="eceb7-122">Next drag and drop the LunarModule prefab to the "Module Prefab" slot on the PhotonRoom class.</span></span> ![](images/module3chapter4updatestep7.png)

   <span data-ttu-id="eceb7-123">Remarque: Si vous cliquez sur l’un des objets prefab et mise en production, l’inspecteur passe à cet objet.</span><span class="sxs-lookup"><span data-stu-id="eceb7-123">Note: If you click on one of the prefab objects and release, the inspector will switch to that object.</span></span> <span data-ttu-id="eceb7-124">Cliquez sur, faites glisser, déposer et libérer chaque objet de l’emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="eceb7-124">Click, drag, drop and release each object to its appropriate slot.</span></span>



8. <span data-ttu-id="eceb7-125">Maintenant, cliquez sur la flèche à gauche de « MixedRealityPlayspace » et déplacer l’objet de jeu d’enfant, « MainCamera » vers le bas dans le préfabriqué « SharedPlayground ».</span><span class="sxs-lookup"><span data-stu-id="eceb7-125">Now, click the arrow to the left of "MixedRealityPlayspace" and move the child game object, "MainCamera" down into the "SharedPlayground" prefab.</span></span> <span data-ttu-id="eceb7-126">Ensuite, supprimez le prefab « MixedRealityPlayspace » (pour les supprimer, sélectionnez le préfabriqué et appuyez sur « Supprimer » de votre clavier).</span><span class="sxs-lookup"><span data-stu-id="eceb7-126">Then, delete the prefab "MixedRealityPlayspace" (to delete, select the prefab and tap "delete" on your keyboard).</span></span>

![Module3hapter4step5im](images/module3chapter4step5im.PNG)

<span data-ttu-id="eceb7-128">Remarque :  Assurez-vous que les positions de la Main Camera et SharedPlayground sont définies sur 0,0,0.</span><span class="sxs-lookup"><span data-stu-id="eceb7-128">note:  Make sure that both the Main Camera and SharedPlayground positions are set to 0,0,0.</span></span>

9. <span data-ttu-id="eceb7-129">Créer un nouvel objet de jeu définie en tant qu’objet enfant à l’objet parent de « SharedPlayground » (pour créer un nouvel objet, cliquez avec le bouton droit sur l’objet parent et sélectionnez « Créer vide »).</span><span class="sxs-lookup"><span data-stu-id="eceb7-129">Create a new game object set as a child object to the "SharedPlayground" parent object (to create a new object, right click on the parent object, and select "create  empty").</span></span> 

10. <span data-ttu-id="eceb7-130">Avec le nouvel objet sélectionné dans votre hiérarchie, modifier le nom de l’objet à « TableAnchor » dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="eceb7-130">With the new object selected in your hierarchy, change the name of the object to "TableAnchor" in the inspector panel.</span></span> <span data-ttu-id="eceb7-131">En outre, cliquez sur « Ajouter un composant » et recherchez le composant « TableAnchor ».</span><span class="sxs-lookup"><span data-stu-id="eceb7-131">Also, click "add component" and search for the "TableAnchor" component.</span></span> <span data-ttu-id="eceb7-132">Sélectionnez-le et ajoutez-le à l’objet.</span><span class="sxs-lookup"><span data-stu-id="eceb7-132">Select it and add it to the object.</span></span> 

![Module3Chapter4step6im](images/module3chapter4step7im.PNG)

> <span data-ttu-id="eceb7-134">Remarque : définir le positionnement à x = 1, y =-0,55 et z = 2.</span><span class="sxs-lookup"><span data-stu-id="eceb7-134">note: set the positioning to x=1, y=-0.55, and z=2.</span></span> <span data-ttu-id="eceb7-135">En outre, la valeur est la rotation y = 90.</span><span class="sxs-lookup"><span data-stu-id="eceb7-135">Also, set the rotation to y=90.</span></span> 
>
> ![Module3Chapter4step6im](images/module3chapter4noteim.PNG)

11. <span data-ttu-id="eceb7-137">Maintenant dans le volet de projet, dans le dossier « prefabs », faites glisser le préfabriqué « table » dans l’objet enfant de « TableAnchor » vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="eceb7-137">Now in the project panel, in the "prefabs" folder, drag the "table" prefab into the "TableAnchor" child object you just created.</span></span>

![Module3Chapter4step8im](images/module3chapter4step8im.PNG)



12. <span data-ttu-id="eceb7-139">Enfin, dans l’objet « DebugWindow », modifiez la largeur à 80 et la hauteur de 10.</span><span class="sxs-lookup"><span data-stu-id="eceb7-139">Finally, in the "DebugWindow" object, change the width to 80 and the height to 10.</span></span>

![Module3Chapter4step9im](images/module3chapter4step11im.PNG)




## <a name="congratulations"></a><span data-ttu-id="eceb7-141">Félicitations</span><span class="sxs-lookup"><span data-stu-id="eceb7-141">Congratulations</span></span>

<span data-ttu-id="eceb7-142">Une fois cette opération terminée, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le Lanceur lunaire.</span><span class="sxs-lookup"><span data-stu-id="eceb7-142">Once this is complete, all users that join your Unity project can move the Lunar Launcher around.</span></span> <span data-ttu-id="eceb7-143">Tous les mouvements sont synchronisés afin que chaque utilisateur peut voir les uns des autres interactions.</span><span class="sxs-lookup"><span data-stu-id="eceb7-143">All movements are synchronized so that each user can see each others' interactions.</span></span> <span data-ttu-id="eceb7-144">Ces concepts servent comme blocs de construction fondamentaux pour des expériences complètes de collaboration partagées.</span><span class="sxs-lookup"><span data-stu-id="eceb7-144">These concepts serve as the foundational building blocks for full-featured shared collaboration experiences.</span></span> 

<span data-ttu-id="eceb7-145">Bien que tous les utilisateurs sont connectés dans le cadre de l’expérience partagée et voyez les mouvements relatifs des objets, l’application est toujours Impossible d’aligner précisément les objets et les avatars afin que les utilisateurs locaux voient les uns des autres et les objets au même endroit dans physique World.</span><span class="sxs-lookup"><span data-stu-id="eceb7-145">Although all users are connected as part of a shared experience and can see the relative movements of objects, the application is still unable to accurately align avatars and objects so that local users see each other and objects in the same place within the physical world.</span></span> <span data-ttu-id="eceb7-146">Pour ancrer un expériences partagées local, chaque appareil nécessite une compréhension commune de l’environnement physique.</span><span class="sxs-lookup"><span data-stu-id="eceb7-146">In order to anchor a local shared experiences, every device requires a common understanding of the physical environment.</span></span> <span data-ttu-id="eceb7-147">Dans ce module, il peut y parvenir à l’aide de [ancres Spatial Azure](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA), qui seront implémenté dans la leçon suivante.</span><span class="sxs-lookup"><span data-stu-id="eceb7-147">In this module, we will achieve this using [Azure Spatial Anchors](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA), which will be implemented in the next lesson.</span></span>

<span data-ttu-id="eceb7-148">Avant de passer à la leçon suivante, nous devrons effectuer le Module de formation ASA, qui couvre principes de base ASA, compte Azure et la création de ressources et d’autres blocs de bâtiments fondamentales nécessaires avant que nous pouvons intégrer cela dans notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="eceb7-148">Before proceeding to the next lesson, we will need to complete the ASA Learning Module, which will cover ASA basics, Azure account and resource creation, and other fundamental buildings blocks required before we can integrate this into our shared experience.</span></span>

<span data-ttu-id="eceb7-149">[Leçon suivante : Sharing(Photon) leçon 5](mrlearning-sharing(photon)-ch5.md)</span><span class="sxs-lookup"><span data-stu-id="eceb7-149">[Next Lesson: Sharing(Photon) Lesson 5](mrlearning-sharing(photon)-ch5.md)</span></span>

