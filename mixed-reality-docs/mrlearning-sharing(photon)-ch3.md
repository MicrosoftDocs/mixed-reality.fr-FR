---
title: Module de partage d’apprentissage MR pour HoloLens 2
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 53519d7bb2832fe8ce500f1ee146c91488b09366
ms.sourcegitcommit: b086d7a62ee0c7913aa8f66c90e9d2527f270264
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68485660"
---
# <a name="3-connecting-multiple-users"></a><span data-ttu-id="69883-104">3. Connexion de plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="69883-104">3. Connecting multiple users</span></span>

<span data-ttu-id="69883-105">Dans cette leçon, nous allons apprendre à connecter plusieurs utilisateurs dans le cadre d’une expérience partagée en direct.</span><span class="sxs-lookup"><span data-stu-id="69883-105">In this lesson, we learn how to connect multiple users as part of a live shared experience.</span></span> <span data-ttu-id="69883-106">À la fin de cette leçon, vous serez en mesure d’ouvrir l’application sur plusieurs appareils, et de voir un avatar, représenté par une sphère, des représentations de chaque personne qui rejoint.</span><span class="sxs-lookup"><span data-stu-id="69883-106">By the end of this lesson, you'll be able to open the application on multiple devices, and see avatar, represented by a sphere, representations of each person that joins.</span></span> 

<span data-ttu-id="69883-107">Cherché</span><span class="sxs-lookup"><span data-stu-id="69883-107">Objectives:</span></span>

- <span data-ttu-id="69883-108">Configurer retentissante dans votre application</span><span class="sxs-lookup"><span data-stu-id="69883-108">Configure PUN within your application</span></span>
- <span data-ttu-id="69883-109">Configurer les joueurs</span><span class="sxs-lookup"><span data-stu-id="69883-109">Configure players</span></span>
- <span data-ttu-id="69883-110">Découvrez comment connecter plusieurs utilisateurs dans un environnement partagé</span><span class="sxs-lookup"><span data-stu-id="69883-110">Learn how to connect multiple users in a shared experience</span></span>

## <a name="instructions"></a><span data-ttu-id="69883-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="69883-111">Instructions</span></span>

1. <span data-ttu-id="69883-112">Dans le dossier Ressources-> Ressources-> Prefabs dans le panneau projet, glissez-déposez le Prefab NetworkLobby dans la hiérarchie, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="69883-112">In the Assets->Resources->Prefabs folder in the Project panel, drag and drop the NetworkLobby prefab in to the hierarchy as shown in the image below.</span></span>

![Module3Chapter3step1im](images/module3chapter3step1im.PNG)

2. <span data-ttu-id="69883-114">Lorsque vous développez NetworkLobby, vous voyez un objet enfant appelé NetworkRoom.</span><span class="sxs-lookup"><span data-stu-id="69883-114">When you expand NetworkLobby, you'll see a child object called NetworkRoom.</span></span> <span data-ttu-id="69883-115">Avec NetworkRoom sélectionné, accédez au panneau de l’inspecteur, puis cliquez sur Ajouter un composant.</span><span class="sxs-lookup"><span data-stu-id="69883-115">With NetworkRoom selected, go into the Inspector panel, and click Add Component.</span></span> <span data-ttu-id="69883-116">Recherchez PhotonView et ajoutez le composant.</span><span class="sxs-lookup"><span data-stu-id="69883-116">Search for PhotonView and add the component.</span></span>

![Module3Chapter3tep2im](images/module3chapter3step2im.PNG)

3. <span data-ttu-id="69883-118">Créez un nouvel objet de jeu vide dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="69883-118">Create a new empty game object in the hierarchy.</span></span> <span data-ttu-id="69883-119">Cliquez avec le bouton droit dans la hiérarchie, puis sélectionnez vide dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="69883-119">Right click in the hierarchy, and select Empty from the Context menu.</span></span> <span data-ttu-id="69883-120">Assurez-vous que le positionnement est défini sur x = 0, y = 0, z = 0 et nommez l’objet, PhotonUser.</span><span class="sxs-lookup"><span data-stu-id="69883-120">Ensure the positioning is set to x =0, y=0, z=0 and name the object, PhotonUser.</span></span>

![Module3Chapter3step3im](images/module3chapter3step3im.PNG)

4. <span data-ttu-id="69883-122">Cliquez sur Ajouter un composant, puis tapez Generic net Sync. Sélectionnez la classe Generic net Sync.</span><span class="sxs-lookup"><span data-stu-id="69883-122">Click Add Component, and type Generic Net Sync. Select the Generic Net Sync class.</span></span> <span data-ttu-id="69883-123">Lorsque la classe s’affiche, cliquez sur la case à cocher utilisateur pour l’activer.</span><span class="sxs-lookup"><span data-stu-id="69883-123">When the class appears, click on the User check box to turn it on.</span></span> 

![module3chapter3updateStep4im](images/module3chapter3updateStep4im.png)

5. <span data-ttu-id="69883-125">Cliquez à nouveau sur Ajouter un composant, puis tapez vue photon.</span><span class="sxs-lookup"><span data-stu-id="69883-125">Click on Add Component again, and type Photon View.</span></span> <span data-ttu-id="69883-126">Sélectionnez la classe de vue photons qui apparaît dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="69883-126">Select the Photon View class that appears in the drop-down list.</span></span>

![module3chapter3updateStep5im](images/module3chapter3updateStep5im.png)

6. <span data-ttu-id="69883-128">Cliquez sur l’icône de fichier de la classe Generic net Sync.</span><span class="sxs-lookup"><span data-stu-id="69883-128">Click the File icon for the Generic Net Sync class.</span></span> <span data-ttu-id="69883-129">Faites-le glisser et déposez-le dans le champ composants observés de la vue photons.</span><span class="sxs-lookup"><span data-stu-id="69883-129">Drag and drop it in the Photon View's Observed Components field.</span></span> 

![module3chapter3updateStep6im. png](images/module3chapter3updateStep6im.png) 

7. <span data-ttu-id="69883-131">Ensuite, nous créons des sphères pour représenter chaque personne qui rejoint une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="69883-131">Next, we create spheres to represent each person that joins a shared experience.</span></span> <span data-ttu-id="69883-132">Cliquez avec le bouton droit sur l’objet PhotonUser que vous venez de créer et scrolldown sur «objet 3D», puis cliquez sur sphère.</span><span class="sxs-lookup"><span data-stu-id="69883-132">Right click the PhotonUser object you just created, and scrolldown to "3D Object, and click Sphere.</span></span> <span data-ttu-id="69883-133">Cela permet de créer un objet de jeu Sphere en tant qu’enfant de l’objet PhotonUser.</span><span class="sxs-lookup"><span data-stu-id="69883-133">This will create a sphere game object as a child of the PhotonUser object.</span></span>

![Module3Chapter3step4im](images/module3chapter3step4im.PNG)

8. <span data-ttu-id="69883-135">Mettez à l’échelle la sphère jusqu’à x = 0.06, y = 0.06, ad z = 0.06.</span><span class="sxs-lookup"><span data-stu-id="69883-135">Scale the sphere down to x=0.06, y=0.06, ad z=0.06.</span></span>

![Module3hapter3step5im](images/module3chapter3step5im.PNG)

9. <span data-ttu-id="69883-137">Faites glisser l’objet de jeu PhotonUser dans le dossier Prefabs du panneau projet, puis supprimez-le de la scène.</span><span class="sxs-lookup"><span data-stu-id="69883-137">Drag the PhotonUser game object into the Prefabs folder in the Project panel, and then delete it from the scene.</span></span> <span data-ttu-id="69883-138">Nous avons maintenant créé un Prefab qui peut être utilisé lors de la génération ou de l’instanciation de nouveaux joueurs dans un environnement partagé.</span><span class="sxs-lookup"><span data-stu-id="69883-138">We have now created a prefab that can be used when spawning or instantiating new players in a shared experience.</span></span>

![Module3Chapter3step6im](images/module3chapter3step6im.PNG)

> <span data-ttu-id="69883-140">Remarque: Assurez-vous que l’objet de jeu a été copié dans le dossier Prefabs avant de le supprimer de votre hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="69883-140">Note: ensure that the game object has successfully copied into the Prefabs folder before deleting it from your hierarchy.</span></span>

10. <span data-ttu-id="69883-141">Créez un nouvel objet dans la hiérarchie en suivant les instructions de l’étape 3, puis nommez-le SharedPlayground.</span><span class="sxs-lookup"><span data-stu-id="69883-141">Create a new object in the hierarchy by following the instructions in Step 3, and name it SharedPlayground.</span></span> <span data-ttu-id="69883-142">Ensuite, cliquez sur Ajouter un composant et recherchez gestionnaire de réseau générique, puis cliquez dessus pour ajouter le composant Generic Network Manager.</span><span class="sxs-lookup"><span data-stu-id="69883-142">Then, click Add Component, and search for generic network manager, and click it to add the Generic Network Manager component.</span></span> <span data-ttu-id="69883-143">Remplacez la position de l’objet par x = 0, y = 0 et z = 0.</span><span class="sxs-lookup"><span data-stu-id="69883-143">Change the position of the object to x=0, y=0, and z =0.</span></span>

![Module3Chapter3step7im](images/module3chapter3step7im.PNG)


## <a name="congratulations"></a><span data-ttu-id="69883-145">Félicitations</span><span class="sxs-lookup"><span data-stu-id="69883-145">Congratulations</span></span>

<span data-ttu-id="69883-146">Une fois que toutes les étapes ci-dessus sont terminées et que le processus de génération est également terminé, appuyez sur le bouton de lecture et connectez votre HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="69883-146">Once all the steps above are complete, and the build process is also complete, press the play button and connect your HoloLens 2.</span></span> <span data-ttu-id="69883-147">Vous devriez voir une sphère se déplaçant au fur et à mesure que vous déplacez votre tête.</span><span class="sxs-lookup"><span data-stu-id="69883-147">You should see a sphere moving around as you move your head.</span></span> <span data-ttu-id="69883-148">Celui-ci s’affiche pour tout utilisateur qui rejoint votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="69883-148">This will be shown for any user that joins your Unity project!</span></span>

<span data-ttu-id="69883-149">[Leçon suivante : 4. Partage de mouvements d’objet avec plusieurs utilisateurs](mrlearning-sharing(photon)-ch4.md)</span><span class="sxs-lookup"><span data-stu-id="69883-149">[Next Lesson: 4. Sharing object movements with multiple users](mrlearning-sharing(photon)-ch4.md)</span></span>

