---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: f2e8cef618ea2fbee398ce19f1ba60b712b5fe3e
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67327666"
---
# <a name="connecting-multiple-users"></a><span data-ttu-id="dd25b-104">**Plusieurs utilisateurs qui se connectent**</span><span class="sxs-lookup"><span data-stu-id="dd25b-104">**Connecting Multiple Users**</span></span> 

<span data-ttu-id="dd25b-105">Dans cette leçon, nous allez apprendre à vous connecter de plusieurs utilisateurs dans le cadre de l’expérience partagée en direct.</span><span class="sxs-lookup"><span data-stu-id="dd25b-105">In this lesson, we will learn how to connect multiple users as part of a live shared experience.</span></span> <span data-ttu-id="dd25b-106">À la fin de cette leçon, vous serez en mesure d’ouvrir l’application sur plusieurs appareils et consultez les représentations sous forme de « avatar » de chaque personne qui joint (avatars représentés par une sphère).</span><span class="sxs-lookup"><span data-stu-id="dd25b-106">By the end of this lesson, you will be able to open the application on multiple devices, and see "avatar" representations of each person that joins (avatars represented by a sphere.)</span></span> 

<span data-ttu-id="dd25b-107">Objectifs :</span><span class="sxs-lookup"><span data-stu-id="dd25b-107">Objectives:</span></span>

- <span data-ttu-id="dd25b-108">Configurer le jeu de mots dans votre application</span><span class="sxs-lookup"><span data-stu-id="dd25b-108">Configure PUN within your application</span></span>
- <span data-ttu-id="dd25b-109">Configurer des joueurs</span><span class="sxs-lookup"><span data-stu-id="dd25b-109">Configure players</span></span>
- <span data-ttu-id="dd25b-110">Découvrez comment vous connecter à plusieurs utilisateurs dans une expérience partagée</span><span class="sxs-lookup"><span data-stu-id="dd25b-110">Learn how to connect multiple users in a shared experience</span></span>

### <a name="instructions"></a><span data-ttu-id="dd25b-111">Instructions</span><span class="sxs-lookup"><span data-stu-id="dd25b-111">Instructions</span></span>

1. <span data-ttu-id="dd25b-112">Dans les ressources > ressources > Prefabs dossier du Panneau de configuration de projet, glisser- déposer le « NetworkLobby » prefab dans à la hiérarchie, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="dd25b-112">In the Assets>Resources>Prefabs folder of the project panel, drag and drop the "NetworkLobby" prefab in to the hierarchy, as shown in the image below.</span></span>


![Module3Chapter3step1im](images/module3chapter3step1im.PNG)

2. <span data-ttu-id="dd25b-114">Lorsque vous développez le prefab « NetworkLobby », vous devez voir un objet enfant appelé « NetworkRoom ».</span><span class="sxs-lookup"><span data-stu-id="dd25b-114">When you expand the prefab "NetworkLobby," you should see a child object called "NetworkRoom."</span></span> <span data-ttu-id="dd25b-115">Avec qu’elle est sélectionnée, accédez au volet d’inspecteur, puis cliquez sur « Ajouter le composant ».</span><span class="sxs-lookup"><span data-stu-id="dd25b-115">With it selected, go into the inspector panel and click "Add Component."</span></span> <span data-ttu-id="dd25b-116">Recherchez « PhotonView » et ajouter le composant.</span><span class="sxs-lookup"><span data-stu-id="dd25b-116">Search for "PhotonView" and add the component.</span></span>

![Module3Chapter3tep2im](images/module3chapter3step2im.PNG)

3. <span data-ttu-id="dd25b-118">Créer un nouvel objet de jeu vide dans la hiérarchie (cliquez avec le bouton droit dans la hiérarchie et sélectionnez « Vide » dans le menu contextuel).</span><span class="sxs-lookup"><span data-stu-id="dd25b-118">Create a new empty game object in the hierarchy (right click in the hierarchy and select "Empty" from the context menu).</span></span> <span data-ttu-id="dd25b-119">Vérifiez le positionnement est défini sur x = 0, y = 0, z = 0 et nommer l’objet, « PhotonUser ».</span><span class="sxs-lookup"><span data-stu-id="dd25b-119">Ensure the positioning is set to x =0, y=0, z=0 and name the object, "PhotonUser."</span></span>

![Module3Chapter3step3im](images/module3chapter3step3im.PNG)

4. <span data-ttu-id="dd25b-121">Ensuite, nous voulons créer des sphères pour représenter chaque personne qui rejoint une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="dd25b-121">Next, we want to create spheres to represent each person that joins a shared experience.</span></span> <span data-ttu-id="dd25b-122">Cliquez avec le bouton droit sur l’objet « PhotonUser » que vous venez de créer, descend jusqu’aux « objet 3D » et cliquez sur la « Sphère ».</span><span class="sxs-lookup"><span data-stu-id="dd25b-122">Right click the "PhotonUser" object you just created, go down to "3D Object" and click "Sphere."</span></span> <span data-ttu-id="dd25b-123">Cela créera un objet de jeu sphère en tant qu’enfant de l’objet PhotonUser.</span><span class="sxs-lookup"><span data-stu-id="dd25b-123">This will create a sphere game object as a child of the PhotonUser object.</span></span>

![Module3Chapter3step4im](images/module3chapter3step4im.PNG)

5. <span data-ttu-id="dd25b-125">Mettre à l’échelle de la sphère à x = 0,06, y = 0,06, ad z = 0,06.</span><span class="sxs-lookup"><span data-stu-id="dd25b-125">Scale the sphere down to x=0.06, y=0.06, ad z=0.06.</span></span>

![Module3hapter3step5im](images/module3chapter3step5im.PNG)

6. <span data-ttu-id="dd25b-127">Faites glisser l’objet de jeu de « PhotonUser » dans le dossier « prefabs » dans le panneau de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="dd25b-127">Drag the "PhotonUser" game object into the "prefabs" folder in the project panel.</span></span> <span data-ttu-id="dd25b-128">Ensuite, le supprimer à partir de la scène.</span><span class="sxs-lookup"><span data-stu-id="dd25b-128">Then, delete it from the scene.</span></span> <span data-ttu-id="dd25b-129">Nous avons maintenant créé un préfabriqué qui sera utilisé lors de la génération dynamique ou instanciation de nouveaux lecteurs dans un environnement partagé.</span><span class="sxs-lookup"><span data-stu-id="dd25b-129">We have now created a prefab that will be used when spawning or instantiating new players in a shared experience.</span></span>

![Module3Chapter3step6im](images/module3chapter3step6im.PNG)

> <span data-ttu-id="dd25b-131">Remarque : Assurez-vous que l’objet de jeu a copiée dans le dossier « prefabs » avant de le supprimer à partir de votre hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="dd25b-131">Note: ensure that the game object has successfully copied into the "prefabs" folder before deleting it from your hierarchy.</span></span>

7. <span data-ttu-id="dd25b-132">Créez un nouvel objet dans la hiérarchie (à l’aide des instructions similaires à celle de l’étape 3) et nommez-le « SharedPlayground. »</span><span class="sxs-lookup"><span data-stu-id="dd25b-132">Create a new object in the hierarchy (using similar instructions to that of Step 3), and name it "SharedPlayground."</span></span> <span data-ttu-id="dd25b-133">Ensuite, cliquez sur « Ajouter un composant » et recherchez « gestionnaire réseau générique » et cliquez dessus pour ajouter le composant Gestionnaire de réseau générique.</span><span class="sxs-lookup"><span data-stu-id="dd25b-133">Then, click "Add Component" and search for "generic network manager" and click it to add the Generic Network Manager component.</span></span> <span data-ttu-id="dd25b-134">Modifier la position de l’objet à x = 0, y = 0 et z = 0.</span><span class="sxs-lookup"><span data-stu-id="dd25b-134">Change the position of the object to x=0, y=0, and z =0.</span></span>

![Module3Chapter3step7im](images/module3chapter3step7im.PNG)


## <a name="congratulations"></a><span data-ttu-id="dd25b-136">Félicitations</span><span class="sxs-lookup"><span data-stu-id="dd25b-136">Congratulations</span></span>

<span data-ttu-id="dd25b-137">Une fois que toutes les étapes ci-dessus sont terminées, et le processus de génération est terminé, lorsque vous appuyez sur le bouton de lecture et que vous vous connectez votre 2 HoloLens, vous devez voir une sphère déplaçant à mesure que vous déplacez votre tête !</span><span class="sxs-lookup"><span data-stu-id="dd25b-137">Once all the steps above are complete, and the build process is complete, when you press the play button and connect your HoloLens 2, you should see a sphere moving around as you move your head!</span></span> <span data-ttu-id="dd25b-138">Elle sera visible pour tous les utilisateurs qui se joint à votre projet Unity !</span><span class="sxs-lookup"><span data-stu-id="dd25b-138">This will be shown for any user that joins your Unity project!</span></span>

<span data-ttu-id="dd25b-139">[Leçon suivante : Sharing(Photon) leçon 4](mrlearning-sharing(photon)-ch4.md)</span><span class="sxs-lookup"><span data-stu-id="dd25b-139">[Next Lesson: Sharing(Photon) Lesson 4](mrlearning-sharing(photon)-ch4.md)</span></span>

