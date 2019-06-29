---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: b729de818dfa21df8fbce782a24a611a365ac795
ms.sourcegitcommit: 78e21e887bf4357c96c9ab2164559d610e8c041e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67465224"
---
# <a name="synchronizing-shared-object-movements"></a><span data-ttu-id="bf407-104">Synchronisation des mouvements des objets partagés</span><span class="sxs-lookup"><span data-stu-id="bf407-104">Synchronizing shared object movements</span></span>

<span data-ttu-id="bf407-105">Dans cette leçon, nous allez apprendre à partager les mouvements des objets afin que tous les participants d’une session partagée peuvent collaborer et afficher leurs interactions.</span><span class="sxs-lookup"><span data-stu-id="bf407-105">In this lesson, we learn how to share the movements of objects so that all participants of a shared session can collaborate together and view each others' interactions.</span></span> <span data-ttu-id="bf407-106">Cette leçon repose sur le Lanceur lunaire qui a été créé dans le cadre de la [didacticiels de Module de Base](mrlearning-base.md).</span><span class="sxs-lookup"><span data-stu-id="bf407-106">This lesson builds upon the Lunar Launcher that was built as part of the [Base Module Tutorials](mrlearning-base.md).</span></span>

<span data-ttu-id="bf407-107">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="bf407-107">Objectives:</span></span>

- <span data-ttu-id="bf407-108">Remettre dans le Lanceur lunaire que le modèle 3D à partager</span><span class="sxs-lookup"><span data-stu-id="bf407-108">Bring in the lunar launcher as the 3D model to be shared</span></span>
- <span data-ttu-id="bf407-109">Configurer votre projet pour partager les mouvements d’un modèle 3D.</span><span class="sxs-lookup"><span data-stu-id="bf407-109">Configure your project to share the movements of the 3D model.</span></span>
- <span data-ttu-id="bf407-110">Découvrez comment créer une application de collaboration multi-utilisateur base</span><span class="sxs-lookup"><span data-stu-id="bf407-110">Learn how to build a basic multi-user collaborative application</span></span>

### <a name="instructions"></a><span data-ttu-id="bf407-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="bf407-111">Instructions</span></span>


1. <span data-ttu-id="bf407-112">Enregistrer la scène à partir de la leçon précédente (contrôle + S).</span><span class="sxs-lookup"><span data-stu-id="bf407-112">Save the scene from the previous lesson (Control+S).</span></span> <span data-ttu-id="bf407-113">Vous pouvez le nommer HLSharedProjectMainPart4.unity afin qu’il soit plus facile à trouver lorsque vous en avez besoin.</span><span class="sxs-lookup"><span data-stu-id="bf407-113">You can name it HLSharedProjectMainPart4.unity so that it's easier to find when you need it.</span></span>

2. <span data-ttu-id="bf407-114">À partir de la fenêtre projet, dans les ressources -> dossier Scripts, double-cliquez sur GenericNetSync pour l’ouvrir dans Visual Studio ou qui vous sont à l’aide de l’éditeur de code jamais.</span><span class="sxs-lookup"><span data-stu-id="bf407-114">From the Project window, in the Assets->Scripts folder, double click on GenericNetSync to open it in Visual Studio or which ever code editor you are using.</span></span>  ![](images/module3chapter4updatestep2.png)

3. <span data-ttu-id="bf407-115">Sur les lignes 34 et 38, supprimez les / / pour activer le code pour la table que nous utiliserons dans cette leçon.</span><span class="sxs-lookup"><span data-stu-id="bf407-115">On Lines 34 and 38, remove the // to activate the code for the table that we will use in this lesson.</span></span> <span data-ttu-id="bf407-116">Ensuite, enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="bf407-116">next, Save the file.</span></span> ![](images/module3chapter4updatestep3.png)

4. <span data-ttu-id="bf407-117">Dans la fenêtre projet, double-cliquez sur le fichier PhotonRoom.cs dans les ressources -> dossier de Scripts pour l’ouvrir dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf407-117">In the Project window, double click on the PhotonRoom.cs file in the Assets->Scripts folder to open it in Visual Studio.</span></span> ![](images/module3chapter4updatestep4.png)

5. <span data-ttu-id="bf407-118">Comme à l’étape 3, nous devons supprimer les / / pour activer le code en lignes 25 et 26 106.![](images/module3chapter4updatestep5a.png)</span><span class="sxs-lookup"><span data-stu-id="bf407-118">Just like in Step 3, we need to remove the // to activate the code at Lines 25, 26, and 106.![](images/module3chapter4updatestep5a.png)</span></span> ![](images/module3chapter4updatestep5b.png)

6. <span data-ttu-id="bf407-119">Dans la vue de la hiérarchie, sélectionnez l’objet NetworkRoom.![](images/module3chapter4updatestep6.png)</span><span class="sxs-lookup"><span data-stu-id="bf407-119">In the Hierarchy view, select the NetworkRoom object.![](images/module3chapter4updatestep6.png)</span></span>

7. <span data-ttu-id="bf407-120">Dans la vue du projet, accédez à ressources -> ressources -> Prefabs.</span><span class="sxs-lookup"><span data-stu-id="bf407-120">In the Project view, navigate to Assets->Resources->Prefabs.</span></span> <span data-ttu-id="bf407-121">Tout d’abord, faites glisser le préfabriqué de Table vers l’emplacement de Tableprefab sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="bf407-121">First, drag and drop the Table prefab to the Tableprefab slot on the PhotonRoom class.</span></span> <span data-ttu-id="bf407-122">Ensuite glisser -déplacer le préfabriqué LunarModule vers l’emplacement de Module Prefab sur la classe PhotonRoom.</span><span class="sxs-lookup"><span data-stu-id="bf407-122">Next drag and drop the LunarModule prefab to the Module Prefab slot on the PhotonRoom class.</span></span> ![](images/module3chapter4updatestep7.png)

   <span data-ttu-id="bf407-123">Remarque: Si vous cliquez sur l’un des objets prefab et mise en production, l’inspecteur passe à cet objet.</span><span class="sxs-lookup"><span data-stu-id="bf407-123">Note: If you click on one of the prefab objects and release, the inspector will switch to that object.</span></span> <span data-ttu-id="bf407-124">Cliquez sur, faites glisser, déposer et libérer chaque objet de l’emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="bf407-124">Click, drag, drop, and release each object to its appropriate slot.</span></span>



8. <span data-ttu-id="bf407-125">Cliquez sur la flèche à gauche de MixedRealityPlayspace et déplacer l’objet de jeu d’enfant, MainCamera vers le bas dans le préfabriqué SharedPlayground.</span><span class="sxs-lookup"><span data-stu-id="bf407-125">Click the arrow to the left of MixedRealityPlayspace, and move the child game object, MainCamera down into the SharedPlayground prefab.</span></span> <span data-ttu-id="bf407-126">Ensuite, supprimez le préfabriqué, MixedRealityPlayspace, à supprimer, sélectionnez le préfabriqué, appuyez sur « delete » sur votre clavier).</span><span class="sxs-lookup"><span data-stu-id="bf407-126">Next, delete the prefab, MixedRealityPlayspace, to delete, select the prefab, and tap "delete" on your keyboard).</span></span>
<span data-ttu-id="bf407-127">![Module3hapter4step5im](images/module3chapter4step5im.PNG)</span><span class="sxs-lookup"><span data-stu-id="bf407-127">![Module3hapter4step5im](images/module3chapter4step5im.PNG)</span></span>

<span data-ttu-id="bf407-128">Remarque:  Assurez-vous que les positions de la Main Camera et SharedPlayground sont définies sur 0,0,0.</span><span class="sxs-lookup"><span data-stu-id="bf407-128">Note:  Make sure that both the Main Camera and SharedPlayground positions are set to 0,0,0.</span></span>

9. <span data-ttu-id="bf407-129">Créer un nouvel objet de jeu défini comme un objet enfant à l’objet parent de SharedPlayground pour créer un nouvel objet.</span><span class="sxs-lookup"><span data-stu-id="bf407-129">Create a new game object set as a child object to the SharedPlayground parent object to create a new object.</span></span> <span data-ttu-id="bf407-130">Cliquez avec le bouton droit sur l’objet parent, puis sélectionnez Créer vide.</span><span class="sxs-lookup"><span data-stu-id="bf407-130">Right click on the parent object, and select Create Empty.</span></span> 

10. <span data-ttu-id="bf407-131">Avec le nouvel objet sélectionné dans votre hiérarchie, modifier le nom de l’objet à TableAnchor dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="bf407-131">With the new object selected in your hierarchy, change the name of the object to TableAnchor in the Inspector panel.</span></span> <span data-ttu-id="bf407-132">En outre, cliquez sur Ajouter un composant et recherchez le composant TableAnchor.</span><span class="sxs-lookup"><span data-stu-id="bf407-132">Also, click Add Component, and search for the TableAnchor component.</span></span> <span data-ttu-id="bf407-133">Sélectionnez-le et ajoutez-le à l’objet.</span><span class="sxs-lookup"><span data-stu-id="bf407-133">Select it and add it to the object.</span></span> 

![Module3Chapter4step6im](images/module3chapter4step7im.PNG)

> <span data-ttu-id="bf407-135">Remarque: Définir le positionnement à x = 1, y =-0,55 et z = 2.</span><span class="sxs-lookup"><span data-stu-id="bf407-135">Note: Set the positioning to x=1, y=-0.55, and z=2.</span></span> <span data-ttu-id="bf407-136">En outre, la valeur est la rotation y = 90.</span><span class="sxs-lookup"><span data-stu-id="bf407-136">Also, set the rotation to y=90.</span></span> 
>
> ![Module3Chapter4step6im](images/module3chapter4noteim.PNG)

11. <span data-ttu-id="bf407-138">Maintenant dans le volet de projet dans le dossier Prefabs, faites glisser le préfabriqué de Table dans l’objet enfant de « TableAnchor » vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="bf407-138">Now from the Project panel in the Prefabs folder, drag the Table prefab into the "TableAnchor" child object you just created.</span></span>

![Module3Chapter4step8im](images/module3chapter4step8im.PNG)



12. <span data-ttu-id="bf407-140">Enfin, dans l’objet DebugWindow, modifiez la largeur à 80 et la hauteur de 10.</span><span class="sxs-lookup"><span data-stu-id="bf407-140">Finally, in the DebugWindow object, change the width to 80 and the height to 10.</span></span>

![Module3Chapter4step9im](images/module3chapter4step11im.PNG)




## <a name="congratulations"></a><span data-ttu-id="bf407-142">Félicitations</span><span class="sxs-lookup"><span data-stu-id="bf407-142">Congratulations</span></span>


<span data-ttu-id="bf407-143">Une fois cette opération terminée, tous les utilisateurs qui rejoignent votre projet Unity peuvent déplacer le Lanceur lunaire.</span><span class="sxs-lookup"><span data-stu-id="bf407-143">Once this is complete, all users that join your Unity project can move the lunar launcher around.</span></span> <span data-ttu-id="bf407-144">Tous les mouvements sont synchronisés afin que chaque utilisateur peut voir les uns des autres interactions.</span><span class="sxs-lookup"><span data-stu-id="bf407-144">All movements are synchronized so that each user can see each others' interactions.</span></span> <span data-ttu-id="bf407-145">Ces concepts servent comme blocs de construction fondamentaux pour des expériences de collaboration complète, partagé.</span><span class="sxs-lookup"><span data-stu-id="bf407-145">These concepts serve as the foundational building blocks for full-featured, shared collaboration experiences.</span></span> 

<span data-ttu-id="bf407-146">Bien que tous les utilisateurs sont connectés dans le cadre de l’expérience partagée et voyez les mouvements relatifs des objets, l’application est toujours Impossible d’aligner précisément les objets et les avatars afin que les utilisateurs locaux voient les uns des autres et les objets au même endroit dans physique World.</span><span class="sxs-lookup"><span data-stu-id="bf407-146">Although all users are connected as part of a shared experience, and can see the relative movements of objects, the application is still unable to accurately align avatars and objects so that local users see each other and objects in the same place within the physical world.</span></span> <span data-ttu-id="bf407-147">Pour ancrer un expériences partagées local, chaque appareil nécessite une compréhension commune de l’environnement physique.</span><span class="sxs-lookup"><span data-stu-id="bf407-147">In order to anchor a local shared experiences, every device requires a common understanding of the physical environment.</span></span> <span data-ttu-id="bf407-148">Dans ce module, nous allons y parvenir en utilisant [ancres Spatial Azure](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA) qui seront implémentés dans la leçon suivante.</span><span class="sxs-lookup"><span data-stu-id="bf407-148">In this module, we'll achieve this by using [Azure Spatial Anchors](<https://azure.microsoft.com/en-us/services/spatial-anchors/>) (ASA) that will be implemented in the next lesson.</span></span>

<span data-ttu-id="bf407-149">Avant de passer à la leçon suivante, nous allons devoir effectuer le Module d’apprentissage ASA qui couvre des notions de base ASA, compte Azure et la création de ressources et d’autres blocs de bâtiments fondamentales nécessaires avant que nous pouvons intégrer cela dans notre expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="bf407-149">Before proceeding to the next lesson, we'll need to complete the ASA Learning Module that covers ASA basics, Azure account and resource creation, and other fundamental buildings blocks required before we can integrate this into our shared experience.</span></span>

<span data-ttu-id="bf407-150">[Leçon suivante : Sharing(Photon) leçon 5](mrlearning-sharing(photon)-ch5.md)</span><span class="sxs-lookup"><span data-stu-id="bf407-150">[Next Lesson: Sharing(Photon) Lesson 5](mrlearning-sharing(photon)-ch5.md)</span></span>

