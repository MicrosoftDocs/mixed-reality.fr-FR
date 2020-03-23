---
title: Tutoriels sur les fonctionnalités multiutilisateurs - 3. Connexion de plusieurs utilisateurs
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multiutilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: cbe0d8d2db6c34ba262fe9c946b68366ed3dbb93
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031229"
---
# <a name="3-connecting-multiple-users"></a><span data-ttu-id="66fc4-105">3. Connexion de plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="66fc4-105">3. Connecting multiple users</span></span>

<span data-ttu-id="66fc4-106">Dans cette leçon, nous allons apprendre à connecter plusieurs utilisateurs dans le cadre d’une expérience partagée en direct.</span><span class="sxs-lookup"><span data-stu-id="66fc4-106">In this lesson, we learn how to connect multiple users as part of a live shared experience.</span></span> <span data-ttu-id="66fc4-107">À la fin de cette leçon, vous pourrez ouvrir l’application sur plusieurs appareils et voir l’avatar, représenté par une sphère, de chaque personne rejoignant l’expérience.</span><span class="sxs-lookup"><span data-stu-id="66fc4-107">By the end of this lesson, you'll be able to open the application on multiple devices and see the avatar, represented by a sphere for each person that joins.</span></span>

## <a name="objectives"></a><span data-ttu-id="66fc4-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="66fc4-108">Objectives</span></span>

* <span data-ttu-id="66fc4-109">Configurer PUN dans votre application</span><span class="sxs-lookup"><span data-stu-id="66fc4-109">Configure PUN within your application</span></span>
* <span data-ttu-id="66fc4-110">Configurer des joueurs</span><span class="sxs-lookup"><span data-stu-id="66fc4-110">Configure players</span></span>
* <span data-ttu-id="66fc4-111">Découvrir comment connecter plusieurs utilisateurs dans un environnement partagé</span><span class="sxs-lookup"><span data-stu-id="66fc4-111">Learn how to connect multiple users in a shared experience</span></span>

## <a name="instructions"></a><span data-ttu-id="66fc4-112">Instructions</span><span class="sxs-lookup"><span data-stu-id="66fc4-112">Instructions</span></span>

1. <span data-ttu-id="66fc4-113">Dans le dossier Assets > Resources > Prefabs du panneau Project, faites glisser-déposer le préfabriqué NetworkLobby dans la hiérarchie, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="66fc4-113">In the Assets->Resources->Prefabs folder of the Project panel, drag and drop the NetworkLobby prefab into the hierarchy as shown in the image below.</span></span>

    ![Module3Chapter3step1im](images/module3chapter3step1im.PNG)

2. <span data-ttu-id="66fc4-115">Quand vous développez NetworkLobby, vous voyez un objet enfant appelé NetworkRoom.</span><span class="sxs-lookup"><span data-stu-id="66fc4-115">When you expand NetworkLobby, you'll see a child object called NetworkRoom.</span></span> <span data-ttu-id="66fc4-116">NetworkRoom étant sélectionné, accédez au panneau Inspector, puis cliquez sur Add Component.</span><span class="sxs-lookup"><span data-stu-id="66fc4-116">With NetworkRoom selected, go into the Inspector panel and click Add Component.</span></span> <span data-ttu-id="66fc4-117">Recherchez PhotonView et ajoutez le composant.</span><span class="sxs-lookup"><span data-stu-id="66fc4-117">Search for PhotonView and add the component.</span></span>

    ![Module3Chapter3tep2im](images/module3chapter3step2im.PNG)

3. <span data-ttu-id="66fc4-119">Créez un objet de jeu vide dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="66fc4-119">Create a new empty game object in the hierarchy.</span></span> <span data-ttu-id="66fc4-120">Cliquez avec le bouton droit dans la hiérarchie et sélectionnez Empty dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="66fc4-120">Right-click in the hierarchy and select Empty from the Context menu.</span></span> <span data-ttu-id="66fc4-121">Vérifiez que le positionnement est défini avec les valeurs x=0, y=0 et z=0, puis nommez l’objet PhotonUser.</span><span class="sxs-lookup"><span data-stu-id="66fc4-121">Ensure the positioning is set to x =0, y=0, z=0 and name the object, PhotonUser.</span></span>

    ![Module3Chapter3step3im](images/module3chapter3step3im.PNG)

4. <span data-ttu-id="66fc4-123">Cliquez sur Add Component et tapez Generic Net Sync. Sélectionnez la classe Generic Net Sync.</span><span class="sxs-lookup"><span data-stu-id="66fc4-123">Click Add Component and type Generic Net Sync. Select the Generic Net Sync class.</span></span> <span data-ttu-id="66fc4-124">Quand la classe s’affiche, cochez la case User pour l’activer.</span><span class="sxs-lookup"><span data-stu-id="66fc4-124">When the class appears, click the User check box to turn it on.</span></span>

    ![module3chapter3updateStep4im](images/module3chapter3updateStep4im.png)

5. <span data-ttu-id="66fc4-126">Cliquez à nouveau sur Add Component, puis tapez Photon View.</span><span class="sxs-lookup"><span data-stu-id="66fc4-126">Click Add Component again, and type Photon View.</span></span> <span data-ttu-id="66fc4-127">Sélectionnez la classe Photon View qui apparaît dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="66fc4-127">Select the Photon View class that appears in the drop-down list.</span></span>

    ![module3chapter3updateStep5im](images/module3chapter3updateStep5im.png)

6. <span data-ttu-id="66fc4-129">Cliquez sur l’icône File de la classe Generic Net Sync.</span><span class="sxs-lookup"><span data-stu-id="66fc4-129">Click the File icon for the Generic Net Sync class.</span></span> <span data-ttu-id="66fc4-130">Faites-le glisser-déposer dans le champ Observed Components de Photon View.</span><span class="sxs-lookup"><span data-stu-id="66fc4-130">Drag and drop it in the Photon View's Observed Components field.</span></span>

    ![module3chapter3updateStep6im.png](images/module3chapter3updateStep6im.png)

7. <span data-ttu-id="66fc4-132">Nous allons à présent créer des sphères pour représenter chaque personne rejoignant une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="66fc4-132">Next, we create spheres to represent each person that joins a shared experience.</span></span> <span data-ttu-id="66fc4-133">Cliquez avec le bouton droit sur l’objet PhotonUser que vous venez de créer, faites défiler jusqu’à 3D Object et cliquez sur Sphere.</span><span class="sxs-lookup"><span data-stu-id="66fc4-133">Right-click the PhotonUser object you just created, scroll-down to "3D Object and click Sphere.</span></span> <span data-ttu-id="66fc4-134">Un objet de jeu Sphere est créé en tant qu’enfant de l’objet PhotonUser.</span><span class="sxs-lookup"><span data-stu-id="66fc4-134">This will create a sphere game object as a child of the PhotonUser object.</span></span>

    ![Module3Chapter3step4im](images/module3chapter3step4im.PNG)

8. <span data-ttu-id="66fc4-136">Mettez à l’échelle la sphère avec les valeurs x=0,06, y=0,06 et z=0,06.</span><span class="sxs-lookup"><span data-stu-id="66fc4-136">Scale the sphere down to x=0.06, y=0.06, ad z=0.06.</span></span>

    ![Module3hapter3step5im](images/module3chapter3step5im.PNG)

9. <span data-ttu-id="66fc4-138">Faites glisser l’objet de jeu PhotonUser dans le dossier Prefabs du panneau Project, puis supprimez-le de la scène.</span><span class="sxs-lookup"><span data-stu-id="66fc4-138">Drag the PhotonUser game object into the Prefabs folder in the Project panel and then delete it from the scene.</span></span> <span data-ttu-id="66fc4-139">Vous disposez maintenant d’un élément fabriqué que vous pouvez utiliser lors de la génération ou de l’instanciation de nouveaux joueurs dans une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="66fc4-139">You have now created a prefab that can be used when spawning or instantiating new players in a shared experience.</span></span>

    ![Module3Chapter3step6im](images/module3chapter3step6im.PNG)

    >[!NOTE]
    ><span data-ttu-id="66fc4-141">Vérifiez que l’objet de jeu a bien été copié dans le dossier Prefabs avant de le supprimer de votre hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="66fc4-141">Ensure that the game object has successfully copied into the Prefabs folder before deleting it from your hierarchy.</span></span>

10. <span data-ttu-id="66fc4-142">Créez un objet dans la hiérarchie en suivant les instructions de l’étape 3 et nommez-le SharedPlayground.</span><span class="sxs-lookup"><span data-stu-id="66fc4-142">Create a new object in the hierarchy by following the instructions in Step 3 and name it SharedPlayground.</span></span> <span data-ttu-id="66fc4-143">Ensuite, cliquez sur Add Component et recherchez Generic Network Manager.</span><span class="sxs-lookup"><span data-stu-id="66fc4-143">Then, click Add Component and search for generic network manager.</span></span>  <span data-ttu-id="66fc4-144">Cliquez à nouveau dessus pour ajouter le composant Generic Network Manager.</span><span class="sxs-lookup"><span data-stu-id="66fc4-144">Click it again to add the Generic Network Manager component.</span></span> <span data-ttu-id="66fc4-145">Définissez la position de l’objet avec les valeurs x=0, y=0 et z=0.</span><span class="sxs-lookup"><span data-stu-id="66fc4-145">Change the position of the object to x=0, y=0, and z =0.</span></span>

    ![Module3Chapter3step7im](images/module3chapter3step7im.PNG)

## <a name="congratulations"></a><span data-ttu-id="66fc4-147">Félicitations</span><span class="sxs-lookup"><span data-stu-id="66fc4-147">Congratulations</span></span>

<span data-ttu-id="66fc4-148">Au terme des étapes ci-dessus et du processus de génération, appuyez sur le bouton de lecture et connectez votre HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="66fc4-148">Once all the steps above are complete and the build process is also complete, press the Play button and connect your HoloLens 2.</span></span> <span data-ttu-id="66fc4-149">Vous devriez voir une sphère qui se déplace à mesure que vous bougez la tête.</span><span class="sxs-lookup"><span data-stu-id="66fc4-149">You should see a sphere moving around as you move your head.</span></span> <span data-ttu-id="66fc4-150">Tout utilisateur qui rejoint votre projet Unity peut la voir.</span><span class="sxs-lookup"><span data-stu-id="66fc4-150">This will be shown for any user that joins your Unity project!</span></span>

<span data-ttu-id="66fc4-151">[Leçon suivante : 4. Partage de mouvements d’objet avec plusieurs utilisateurs](mrlearning-sharing(photon)-ch4.md)</span><span class="sxs-lookup"><span data-stu-id="66fc4-151">[Next Lesson: 4. Sharing object movements with multiple users](mrlearning-sharing(photon)-ch4.md)</span></span>
