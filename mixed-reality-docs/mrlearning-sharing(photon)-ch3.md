---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 4625acfcb3353e9537961a444012452139705359
ms.sourcegitcommit: 78e21e887bf4357c96c9ab2164559d610e8c041e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67465216"
---
# <a name="connecting-multiple-users"></a><span data-ttu-id="d72d9-104">**Plusieurs utilisateurs qui se connectent**</span><span class="sxs-lookup"><span data-stu-id="d72d9-104">**Connecting multiple users**</span></span> 

<span data-ttu-id="d72d9-105">Dans cette leçon, nous Découvrez comment connecter plusieurs utilisateurs dans le cadre de l’expérience partagée en direct.</span><span class="sxs-lookup"><span data-stu-id="d72d9-105">In this lesson, we learn how to connect multiple users as part of a live shared experience.</span></span> <span data-ttu-id="d72d9-106">À la fin de cette leçon, vous serez en mesure d’ouvrir l’application sur plusieurs appareils et consultez avatar, représenté par une sphère, les représentations sous forme de chaque personne qui joint.</span><span class="sxs-lookup"><span data-stu-id="d72d9-106">By the end of this lesson, you'll be able to open the application on multiple devices, and see avatar, represented by a sphere, representations of each person that joins.</span></span> 

<span data-ttu-id="d72d9-107">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="d72d9-107">Objectives:</span></span>

- <span data-ttu-id="d72d9-108">Configurer le jeu de mots dans votre application</span><span class="sxs-lookup"><span data-stu-id="d72d9-108">Configure PUN within your application</span></span>
- <span data-ttu-id="d72d9-109">Configurer des joueurs</span><span class="sxs-lookup"><span data-stu-id="d72d9-109">Configure players</span></span>
- <span data-ttu-id="d72d9-110">Découvrez comment vous connecter à plusieurs utilisateurs dans une expérience partagée</span><span class="sxs-lookup"><span data-stu-id="d72d9-110">Learn how to connect multiple users in a shared experience</span></span>

### <a name="instructions"></a><span data-ttu-id="d72d9-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="d72d9-111">Instructions</span></span>

1. <span data-ttu-id="d72d9-112">Dans les ressources -> ressources -> dossier Prefabs dans le panneau de configuration de projet, faites glisser le préfabriqué NetworkLobby dans à la hiérarchie comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d72d9-112">In the Assets->Resources->Prefabs folder in the Project panel, drag and drop the NetworkLobby prefab in to the hierarchy as shown in the image below.</span></span>


   ![Module3Chapter3step1im](images/module3chapter3step1im.PNG)

2. <span data-ttu-id="d72d9-114">Lorsque vous développez NetworkLobby, vous verrez un objet enfant appelé NetworkRoom.</span><span class="sxs-lookup"><span data-stu-id="d72d9-114">When you expand NetworkLobby, you'll see a child object called NetworkRoom.</span></span> <span data-ttu-id="d72d9-115">Avec NetworkRoom sélectionné, accédez au volet d’inspecteur, puis cliquez sur Ajouter un composant.</span><span class="sxs-lookup"><span data-stu-id="d72d9-115">With NetworkRoom selected, go into the Inspector panel, and click Add Component.</span></span> <span data-ttu-id="d72d9-116">Recherchez PhotonView et ajouter le composant.</span><span class="sxs-lookup"><span data-stu-id="d72d9-116">Search for PhotonView and add the component.</span></span>

   ![Module3Chapter3tep2im](images/module3chapter3step2im.PNG)

3. <span data-ttu-id="d72d9-118">Créer un nouvel objet de jeu vide dans la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="d72d9-118">Create a new empty game object in the hierarchy.</span></span> <span data-ttu-id="d72d9-119">Cliquez avec le bouton droit dans la hiérarchie, puis sélectionnez vide dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="d72d9-119">Right click in the hierarchy, and select Empty from the Context menu.</span></span> <span data-ttu-id="d72d9-120">Vérifiez le positionnement est défini sur x = 0, y = 0, z = 0 et nommer l’objet, PhotonUser.</span><span class="sxs-lookup"><span data-stu-id="d72d9-120">Ensure the positioning is set to x =0, y=0, z=0 and name the object, PhotonUser.</span></span>

   ![Module3Chapter3step3im](images/module3chapter3step3im.PNG)

4. <span data-ttu-id="d72d9-122">Cliquez sur Ajouter un composant, puis tapez synchronisation Net générique. Sélectionnez la classe générique synchronisation Net.</span><span class="sxs-lookup"><span data-stu-id="d72d9-122">Click Add Component, and type Generic Net Sync. Select the Generic Net Sync class.</span></span> <span data-ttu-id="d72d9-123">Lorsque la classe s’affiche, cliquez sur la case à cocher pour l’activer.</span><span class="sxs-lookup"><span data-stu-id="d72d9-123">When the class appears, click on the User check box to turn it on.</span></span> 

   ![module3chapter3updateStep4im](images/module3chapter3updateStep4im.png)

5. <span data-ttu-id="d72d9-125">Cliquez sur Ajouter un composant à nouveau et tapez Photon View.</span><span class="sxs-lookup"><span data-stu-id="d72d9-125">Click on Add Component again, and type Photon View.</span></span> <span data-ttu-id="d72d9-126">Sélectionnez la classe d’affichage de Photon qui s’affiche dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="d72d9-126">Select the Photon View class that appears in the drop-down list.</span></span>

   ![module3chapter3updateStep5im](images/module3chapter3updateStep5im.png)

6. <span data-ttu-id="d72d9-128">Cliquez sur l’icône de fichier pour la classe générique synchronisation Net.</span><span class="sxs-lookup"><span data-stu-id="d72d9-128">Click the File icon for the Generic Net Sync class.</span></span> <span data-ttu-id="d72d9-129">Faites glisser dans le champ d’observé les composants de la vue Photon.</span><span class="sxs-lookup"><span data-stu-id="d72d9-129">Drag and drop it in the Photon View's Observed Components field.</span></span> ![module3chapter3updateStep6im.png](images/module3chapter3updateStep6im.png) 

7. <span data-ttu-id="d72d9-131">Ensuite, nous créer sphères pour représenter chaque personne qui rejoint une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="d72d9-131">Next, we create spheres to represent each person that joins a shared experience.</span></span> <span data-ttu-id="d72d9-132">Avec le bouton droit sur l’objet de PhotonUser que vous venez de créer et scrolldown à « sphère objet 3D, puis cliquez sur.</span><span class="sxs-lookup"><span data-stu-id="d72d9-132">Right click the PhotonUser object you just created, and scrolldown to "3D Object, and click Sphere.</span></span> <span data-ttu-id="d72d9-133">Cela créera un objet de jeu sphère en tant qu’enfant de l’objet PhotonUser.</span><span class="sxs-lookup"><span data-stu-id="d72d9-133">This will create a sphere game object as a child of the PhotonUser object.</span></span>

   ![Module3Chapter3step4im](images/module3chapter3step4im.PNG)

8. <span data-ttu-id="d72d9-135">Mettre à l’échelle de la sphère à x = 0,06, y = 0,06, ad z = 0,06.</span><span class="sxs-lookup"><span data-stu-id="d72d9-135">Scale the sphere down to x=0.06, y=0.06, ad z=0.06.</span></span>

   ![Module3hapter3step5im](images/module3chapter3step5im.PNG)

9. <span data-ttu-id="d72d9-137">Faites glisser l’objet de jeu PhotonUser dans le dossier Prefabs dans le panneau de configuration de projet, puis supprimez-le de la scène.</span><span class="sxs-lookup"><span data-stu-id="d72d9-137">Drag the PhotonUser game object into the Prefabs folder in the Project panel, and then delete it from the scene.</span></span> <span data-ttu-id="d72d9-138">Nous avons maintenant créé un préfabriqué qui peut être utilisé lors de la génération dynamique ou instanciation de nouveaux lecteurs dans un environnement partagé.</span><span class="sxs-lookup"><span data-stu-id="d72d9-138">We have now created a prefab that can be used when spawning or instantiating new players in a shared experience.</span></span>

   ![Module3Chapter3step6im](images/module3chapter3step6im.PNG)

> <span data-ttu-id="d72d9-140">Remarque : Assurez-vous que l’objet de jeu a correctement copié dans le dossier Prefabs avant de le supprimer à partir de votre hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="d72d9-140">Note: ensure that the game object has successfully copied into the Prefabs folder before deleting it from your hierarchy.</span></span>

10. <span data-ttu-id="d72d9-141">Créer un nouvel objet dans la hiérarchie en suivant les instructions à l’étape 3 et nommez-le SharedPlayground.</span><span class="sxs-lookup"><span data-stu-id="d72d9-141">Create a new object in the hierarchy by following the instructions in Step 3, and name it SharedPlayground.</span></span> <span data-ttu-id="d72d9-142">Ensuite, cliquez sur Ajouter un composant, recherchez le Gestionnaire de réseau générique et cliquez dessus pour ajouter le composant Gestionnaire de réseau générique.</span><span class="sxs-lookup"><span data-stu-id="d72d9-142">Then, click Add Component, and search for generic network manager, and click it to add the Generic Network Manager component.</span></span> <span data-ttu-id="d72d9-143">Modifier la position de l’objet à x = 0, y = 0 et z = 0.</span><span class="sxs-lookup"><span data-stu-id="d72d9-143">Change the position of the object to x=0, y=0, and z =0.</span></span>

    ![Module3Chapter3step7im](images/module3chapter3step7im.PNG)


## <a name="congratulations"></a><span data-ttu-id="d72d9-145">Félicitations</span><span class="sxs-lookup"><span data-stu-id="d72d9-145">Congratulations</span></span>

<span data-ttu-id="d72d9-146">Une fois toutes les étapes ci-dessus sont terminées, et le processus de génération est également terminé, appuyez sur le bouton de lecture et connecter votre 2 HoloLens.</span><span class="sxs-lookup"><span data-stu-id="d72d9-146">Once all the steps above are complete, and the build process is also complete, press the play button and connect your HoloLens 2.</span></span> <span data-ttu-id="d72d9-147">Vous devez voir une sphère déplaçant à mesure que vous déplacez votre tête.</span><span class="sxs-lookup"><span data-stu-id="d72d9-147">You should see a sphere moving around as you move your head.</span></span> <span data-ttu-id="d72d9-148">Elle sera visible pour tous les utilisateurs qui se joint à votre projet Unity !</span><span class="sxs-lookup"><span data-stu-id="d72d9-148">This will be shown for any user that joins your Unity project!</span></span>

<span data-ttu-id="d72d9-149">[Leçon suivante : Sharing(Photon) leçon 4](mrlearning-sharing(photon)-ch4.md)</span><span class="sxs-lookup"><span data-stu-id="d72d9-149">[Next Lesson: Sharing(Photon) Lesson 4](mrlearning-sharing(photon)-ch4.md)</span></span>

