---
title: Notions de base de m. 100-prise en main d’Unity
description: Apprenez à créer votre première application de réalité mixte « Hello World ».
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: la réalité mixte, Windows Mixed Reality, HoloLens, immersif, VR, Mr, prise en main, hologramme, Academy, didacticiel
ms.openlocfilehash: 58a1785ef74872c633cf65d6a32e24d517367359
ms.sourcegitcommit: f523b74a549721b6bec69cb5d2eca5b7673a793c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85570303"
---
# <a name="mr-basics-100-getting-started-with-unity"></a><span data-ttu-id="040ad-104">Réalité mixte - Principes fondamentaux - Cours 100 : Bien démarrer avec Unity</span><span class="sxs-lookup"><span data-stu-id="040ad-104">MR Basics 100: Getting started with Unity</span></span>

>[!IMPORTANT]
><span data-ttu-id="040ad-105">Les tutoriels Mixed Reality Academy ont été conçus pour les appareils HoloLens (1re génération) et les casques immersifs de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="040ad-105">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="040ad-106">Nous estimons qu’il est important de laisser ces tutoriels à la disposition des développeurs qui recherchent encore des conseils pour développer des applications sur ces appareils.</span><span class="sxs-lookup"><span data-stu-id="040ad-106">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="040ad-107">Notez que ces tutoriels **_ne sont pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="040ad-107">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="040ad-108">Ils sont fournis dans le but de fonctionner sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="040ad-108">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="040ad-109">Une [nouvelle série de tutoriels](mrlearning-base.md) a été publiée pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="040ad-109">[A new series of tutorials](mrlearning-base.md) has been posted for HoloLens 2.</span></span>

<span data-ttu-id="040ad-110">Ce didacticiel vous guide dans la création d’une application de réalité mixte de base créée avec Unity.</span><span class="sxs-lookup"><span data-stu-id="040ad-110">This tutorial will walk you through creating a basic mixed reality app built with Unity.</span></span>

## <a name="device-support"></a><span data-ttu-id="040ad-111">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="040ad-111">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="040ad-112">Cours</span><span class="sxs-lookup"><span data-stu-id="040ad-112">Course</span></span></th><th style="width:150px"> <span data-ttu-id="040ad-113"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="040ad-113"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="040ad-114"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="040ad-114"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td><span data-ttu-id="040ad-115">Réalité mixte - Principes fondamentaux - Cours 100 : Bien démarrer avec Unity</span><span class="sxs-lookup"><span data-stu-id="040ad-115">MR Basics 100: Getting started with Unity</span></span></td><td style="text-align: center;"> <span data-ttu-id="040ad-116">✔️</span><span class="sxs-lookup"><span data-stu-id="040ad-116">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="040ad-117">✔️</span><span class="sxs-lookup"><span data-stu-id="040ad-117">✔️</span></span></td>
</tr>
</table>

## <a name="prerequisites"></a><span data-ttu-id="040ad-118">Prérequis</span><span class="sxs-lookup"><span data-stu-id="040ad-118">Prerequisites</span></span>

* <span data-ttu-id="040ad-119">Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).</span><span class="sxs-lookup"><span data-stu-id="040ad-119">A Windows 10 PC configured with the correct [tools installed](install-the-tools.md).</span></span>

## <a name="chapter-1---create-a-new-project"></a><span data-ttu-id="040ad-120">Chapitre 1-créer un nouveau projet</span><span class="sxs-lookup"><span data-stu-id="040ad-120">Chapter 1 - Create a New Project</span></span>

>[!VIDEO https://www.youtube.com/embed/2L5IFO0hnYA]

<span data-ttu-id="040ad-121">Pour générer une application avec Unity, vous devez d’abord créer un projet.</span><span class="sxs-lookup"><span data-stu-id="040ad-121">To build an app with Unity, you first need to create a project.</span></span> <span data-ttu-id="040ad-122">Ce projet est organisé en quelques dossiers, dont le plus important est votre dossier de ressources.</span><span class="sxs-lookup"><span data-stu-id="040ad-122">This project is organized into a few folders, the most important of which is your Assets folder.</span></span> <span data-ttu-id="040ad-123">Il s’agit du dossier qui contient toutes les ressources que vous importez à partir d’outils de création de contenu numérique tels que Maya, Max Cinema 4D ou Photoshop, tout le code que vous créez avec Visual Studio ou votre éditeur de code favori, et tout autre fichier de contenu créé par Unity lorsque vous composez des scènes, animations et autres types de ressources Unity dans l’éditeur</span><span class="sxs-lookup"><span data-stu-id="040ad-123">This is the folder that holds all assets you import from digital content creation tools such as Maya, Max Cinema 4D or Photoshop, all code you create with Visual Studio or your favorite code editor, and any number of content files that Unity creates as you compose scenes, animations and other Unity asset types in the editor.</span></span>

<span data-ttu-id="040ad-124">Pour générer et déployer des applications UWP, Unity peut exporter le projet en tant que solution Visual Studio qui contient tous les fichiers de ressources et de code nécessaires.</span><span class="sxs-lookup"><span data-stu-id="040ad-124">To build and deploy UWP apps, Unity can export the project as a Visual Studio solution that will contain all necessary asset and code files.</span></span>

1. <span data-ttu-id="040ad-125">Démarrer Unity</span><span class="sxs-lookup"><span data-stu-id="040ad-125">Start Unity</span></span>
2. <span data-ttu-id="040ad-126">Sélectionner **nouveau**</span><span class="sxs-lookup"><span data-stu-id="040ad-126">Select **New**</span></span>
3. <span data-ttu-id="040ad-127">Entrez un nom de projet (par exemple, « MixedRealityIntroduction »)</span><span class="sxs-lookup"><span data-stu-id="040ad-127">Enter a project name (e.g. "MixedRealityIntroduction")</span></span>
4. <span data-ttu-id="040ad-128">Entrez un emplacement pour enregistrer votre projet</span><span class="sxs-lookup"><span data-stu-id="040ad-128">Enter a location to save your project</span></span>
5. <span data-ttu-id="040ad-129">Vérifier que le bouton bascule **3D** est sélectionné</span><span class="sxs-lookup"><span data-stu-id="040ad-129">Ensure the **3D** toggle is selected</span></span>
6. <span data-ttu-id="040ad-130">Sélectionner **créer un projet**</span><span class="sxs-lookup"><span data-stu-id="040ad-130">Select **Create project**</span></span>

<span data-ttu-id="040ad-131">Contentes, vous êtes prêt pour la prise en main de vos personnalisations de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="040ad-131">Congrats, you are all setup to get started with your mixed reality customizations now.</span></span>

## <a name="chapter-2---setup-the-camera"></a><span data-ttu-id="040ad-132">Chapitre 2-configurer l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="040ad-132">Chapter 2 - Setup the Camera</span></span>

>[!VIDEO https://www.youtube.com/embed/eP1ZwB4wSNA]

<span data-ttu-id="040ad-133">La caméra principale Unity gère le suivi des têtes et le rendu stéréoscopique.</span><span class="sxs-lookup"><span data-stu-id="040ad-133">The Unity Main Camera handles head tracking and stereoscopic rendering.</span></span> <span data-ttu-id="040ad-134">Il y a quelques modifications à apporter à la caméra principale pour l’utiliser avec la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="040ad-134">There are a few changes to make to the Main Camera to use it with mixed reality.</span></span>

1. <span data-ttu-id="040ad-135">Sélectionner un fichier > nouvelle scène</span><span class="sxs-lookup"><span data-stu-id="040ad-135">Select File > New Scene</span></span>

<span data-ttu-id="040ad-136">Tout d’abord, il sera plus facile de présenter votre application si vous imaginez la position de départ de l’utilisateur comme (**X**: 0, **Y**: 0, **Z**: 0).</span><span class="sxs-lookup"><span data-stu-id="040ad-136">First, it will be easier to lay out your app if you imagine the starting position of the user as (**X**: 0, **Y**: 0, **Z**: 0).</span></span> <span data-ttu-id="040ad-137">Étant donné que la caméra principale effectue le suivi du mouvement de la tête de l’utilisateur, la position de départ de l’utilisateur peut être définie en définissant la position de départ de l’appareil photo principal.</span><span class="sxs-lookup"><span data-stu-id="040ad-137">Since the Main Camera is tracking movement of the user's head, the starting position of the user can be set by setting the starting position of the Main Camera.</span></span>

1. <span data-ttu-id="040ad-138">Sélectionner la **caméra principale** dans le volet de la **hiérarchie**</span><span class="sxs-lookup"><span data-stu-id="040ad-138">Select **Main Camera** in the **Hierarchy** panel</span></span>
2. <span data-ttu-id="040ad-139">Dans le volet de l' **inspecteur** , recherchez le composant **transformer** et remplacez la **position** (**x**: 0, **y**: 1, **z**:-10) par (**x**: 0, **y**: 0, **z**: 0)</span><span class="sxs-lookup"><span data-stu-id="040ad-139">In the **Inspector** panel, find the **Transform** component and change the **Position** from (**X**: 0, **Y**: 1, **Z**: -10) to (**X**: 0, **Y**: 0, **Z**: 0)</span></span>

<span data-ttu-id="040ad-140">Deuxièmement, l’arrière-plan de la caméra par défaut a besoin d’une pensée.</span><span class="sxs-lookup"><span data-stu-id="040ad-140">Second, the default Camera background needs some thought.</span></span>

<span data-ttu-id="040ad-141">**Pour les applications HoloLens**, le monde réel doit apparaître derrière tout ce que l’appareil photo rend, et non une texture skybox.</span><span class="sxs-lookup"><span data-stu-id="040ad-141">**For HoloLens applications**, the real world should appear behind everything the camera renders, not a Skybox texture.</span></span>

1. <span data-ttu-id="040ad-142">Avec la **caméra principale** toujours sélectionnée dans le **panneau hiérarchie** , recherchez le composant **Camera** dans le panneau **inspecteur** et remplacez la liste déroulante **Clear Flags** de **skybox** par **couleur unie**.</span><span class="sxs-lookup"><span data-stu-id="040ad-142">With the **Main Camera** still selected in the **Hierarchy** panel, find the **Camera** component in the **Inspector** panel and change the **Clear Flags** dropdown from **Skybox** to **Solid Color**.</span></span>
2. <span data-ttu-id="040ad-143">Sélectionnez le sélecteur de couleur d' **arrière-plan** et modifiez les valeurs **RVBA** en (0, 0, 0, 0)</span><span class="sxs-lookup"><span data-stu-id="040ad-143">Select the **Background** color picker and change the **RGBA** values to (0, 0, 0, 0)</span></span>

<span data-ttu-id="040ad-144">**Pour les applications de réalité mixte ciblant des casques immersifs**, nous pouvons utiliser la texture skybox par défaut fournie par Unity.</span><span class="sxs-lookup"><span data-stu-id="040ad-144">**For mixed reality applications targeted to immersive headsets**, we can use the default Skybox texture that Unity provides.</span></span>

1. <span data-ttu-id="040ad-145">Avec la **caméra principale** toujours sélectionnée dans le panneau **hiérarchie** , recherchez le composant **Camera** dans le panneau **inspecteur** et conservez la liste déroulante **indicateurs clairs** pour **skybox**.</span><span class="sxs-lookup"><span data-stu-id="040ad-145">With the **Main Camera** still selected in the **Hierarchy** panel, find the **Camera** component in the **Inspector** panel and keep the **Clear Flags** dropdown to **Skybox**.</span></span>

<span data-ttu-id="040ad-146">Troisièmement, examinons le plan near clip dans Unity et empêchez les objets d’être rendus trop près des yeux des utilisateurs, car un utilisateur approche un objet ou un objet s’approche d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="040ad-146">Third, let us consider the near clip plane in Unity and prevent objects from being rendered too close to the users eyes as a user approaches an object or an object approaches a user.</span></span>

<span data-ttu-id="040ad-147">**Pour les applications HoloLens**, le plan near clip peut être défini sur les 0,85 compteurs [recommandés pour hololens](camera-in-unity.md#clip-planes) .</span><span class="sxs-lookup"><span data-stu-id="040ad-147">**For HoloLens applications**, the near clip plane can be set to the [HoloLens recommended](camera-in-unity.md#clip-planes) 0.85 meters.</span></span>

1. <span data-ttu-id="040ad-148">Avec la **caméra principale** toujours sélectionnée dans le volet de **hiérarchie** , recherchez le composant **Camera** dans le panneau **inspecteur** , puis modifiez le champ **near clip plan** de la valeur par défaut **0,3** en HoloLens Recommended **0,85**.</span><span class="sxs-lookup"><span data-stu-id="040ad-148">With the **Main Camera** still selected in the **Hierarchy** panel, find the **Camera** component in the **Inspector** panel and change the **Near Clip Plane** field from the default **0.3** to the HoloLens recommended **0.85**.</span></span>

<span data-ttu-id="040ad-149">**Pour les applications de réalité mixte ciblant des casques immersifs**, nous pouvons utiliser le paramètre par défaut fourni par Unity.</span><span class="sxs-lookup"><span data-stu-id="040ad-149">**For mixed reality applications targeted to immersive headsets**, we can use the default setting that Unity provides.</span></span>

1. <span data-ttu-id="040ad-150">Avec la **caméra principale** toujours sélectionnée dans le panneau **hiérarchie** , recherchez le composant **Camera** dans le panneau **inspecteur** , puis conservez le champ du **plan near clip** à la valeur par défaut **0,3**.</span><span class="sxs-lookup"><span data-stu-id="040ad-150">With the **Main Camera** still selected in the **Hierarchy** panel, find the **Camera** component in the **Inspector** panel and keep the **Near Clip Plane** field to the default **0.3**.</span></span>

<span data-ttu-id="040ad-151">Enfin, laissez-nous enregistrer notre progression jusqu’à présent.</span><span class="sxs-lookup"><span data-stu-id="040ad-151">Finally, let us save our progress so far.</span></span> <span data-ttu-id="040ad-152">Pour enregistrer les modifications de la scène, sélectionnez **fichier > enregistrer la scène sous**, nommez la scène **main**, puis sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="040ad-152">To save the scene changes, select **File > Save Scene As**, name the scene **Main**, and select **Save**.</span></span>

## <a name="chapter-3---setup-the-project-settings"></a><span data-ttu-id="040ad-153">Chapitre 3-configurer les paramètres du projet</span><span class="sxs-lookup"><span data-stu-id="040ad-153">Chapter 3 - Setup the Project Settings</span></span>

>[!VIDEO https://www.youtube.com/embed/ItRoiXccC0g]

<span data-ttu-id="040ad-154">Dans ce chapitre, nous allons définir des paramètres de projet Unity qui nous aident à cibler le kit de développement logiciel (SDK) Windows holographique pour le développement.</span><span class="sxs-lookup"><span data-stu-id="040ad-154">In this chapter, we will set some Unity project settings that help us target the Windows Holographic SDK for development.</span></span> <span data-ttu-id="040ad-155">Nous allons également définir des paramètres de qualité pour notre application.</span><span class="sxs-lookup"><span data-stu-id="040ad-155">We will also set some quality settings for our application.</span></span> <span data-ttu-id="040ad-156">Enfin, nous nous assurons que nos cibles de génération sont définies sur plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="040ad-156">Finally, we will ensure our build targets are set to Universal Windows Platform.</span></span>

### <a name="unity-performance-and-quality-settings"></a><span data-ttu-id="040ad-157">Paramètres de performance et de qualité Unity</span><span class="sxs-lookup"><span data-stu-id="040ad-157">Unity performance and quality settings</span></span>

<span data-ttu-id="040ad-158">**Paramètres de qualité Unity pour HoloLens**</span><span class="sxs-lookup"><span data-stu-id="040ad-158">**Unity quality settings for HoloLens**</span></span>

![Paramètres de qualité Unity pour HoloLens](images/qualitysettings.png)

<span data-ttu-id="040ad-160">Étant donné que la gestion de la fréquence élevée sur HoloLens est si importante, nous souhaitons que les paramètres de qualité soient réglés pour des performances plus rapides.</span><span class="sxs-lookup"><span data-stu-id="040ad-160">Since maintaining high framerate on HoloLens is so important, we want the quality settings tuned for fastest performance.</span></span> <span data-ttu-id="040ad-161">Pour plus d’informations sur les performances, sur [les recommandations en matière de performances pour Unity](performance-recommendations-for-unity.md).</span><span class="sxs-lookup"><span data-stu-id="040ad-161">For more detailed performance information, [Performance recommendations for Unity](performance-recommendations-for-unity.md).</span></span>

1. <span data-ttu-id="040ad-162">Sélectionnez **modifier > paramètres du projet > qualité**</span><span class="sxs-lookup"><span data-stu-id="040ad-162">Select **Edit > Project Settings > Quality**</span></span>
2. <span data-ttu-id="040ad-163">Sélectionnez la **liste déroulante** sous le logo de **plateforme Windows universelle** et sélectionnez **très faible**.</span><span class="sxs-lookup"><span data-stu-id="040ad-163">Select the **dropdown** under the **Universal Windows Platform** logo and select **Very Low**.</span></span> <span data-ttu-id="040ad-164">Vous saurez que le paramètre est appliqué correctement lorsque la zone de la plateforme Windows universelle colonne et la ligne **très basse** est verte.</span><span class="sxs-lookup"><span data-stu-id="040ad-164">You'll know the setting is applied correctly when the box in the Universal Windows Platform column and **Very Low** row is green.</span></span>

<span data-ttu-id="040ad-165">**Pour les applications de réalité mixte ciblant bloqués**, vous pouvez conserver les valeurs par défaut des paramètres de qualité.</span><span class="sxs-lookup"><span data-stu-id="040ad-165">**For mixed reality applications targeted to occluded displays**, you can leave the quality settings to its default values.</span></span>

### <a name="target-windows-10-sdk"></a><span data-ttu-id="040ad-166">SDK Windows 10 cible</span><span class="sxs-lookup"><span data-stu-id="040ad-166">Target Windows 10 SDK</span></span>

<span data-ttu-id="040ad-167">**KIT SDK Windows holographique cible**</span><span class="sxs-lookup"><span data-stu-id="040ad-167">**Target Windows Holographic SDK**</span></span>

![KIT SDK Windows holographique cible](images/xrsettings.png)

<span data-ttu-id="040ad-169">Nous devons permettre à Unity de savoir que l’application que nous essayons d’exporter doit créer une [vue immersive](app-views.md) au lieu d’une vue 2D.</span><span class="sxs-lookup"><span data-stu-id="040ad-169">We need to let Unity know that the app we are trying to export should create an [immersive view](app-views.md) instead of a 2D view.</span></span> <span data-ttu-id="040ad-170">Pour ce faire, nous allons activer la prise en charge de la réalité virtuelle sur Unity ciblant le SDK Windows 10.</span><span class="sxs-lookup"><span data-stu-id="040ad-170">We do this by enabling Virtual Reality support on Unity targeting the Windows 10 SDK.</span></span>

1. <span data-ttu-id="040ad-171">Accédez à **modifier > paramètres du projet > Player**.</span><span class="sxs-lookup"><span data-stu-id="040ad-171">Go to **Edit > Project Settings > Player**.</span></span>
2. <span data-ttu-id="040ad-172">Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez l’icône **plateforme Windows universelle** .</span><span class="sxs-lookup"><span data-stu-id="040ad-172">In the **Inspector Panel** for Player Settings, select the **Universal Windows Platform** icon.</span></span>
3. <span data-ttu-id="040ad-173">Développez le groupe **XR Settings**.</span><span class="sxs-lookup"><span data-stu-id="040ad-173">Expand the **XR Settings** group.</span></span>
4. <span data-ttu-id="040ad-174">Dans la section **rendu** , activez la case à cocher **réalité virtuelle prise en charge** pour ajouter une nouvelle liste de **SDK de réalité virtuelle** .</span><span class="sxs-lookup"><span data-stu-id="040ad-174">In the **Rendering** section, check the **Virtual Reality Supported** checkbox to add a new **Virtual Reality SDKs** list.</span></span>
5. <span data-ttu-id="040ad-175">Vérifiez que **Windows Mixed Reality** apparaît dans la liste.</span><span class="sxs-lookup"><span data-stu-id="040ad-175">Verify that **Windows Mixed Reality** appears in the list.</span></span> <span data-ttu-id="040ad-176">Dans le cas contraire, sélectionnez le bouton **+** en bas de la liste et choisissez **Windows Mixed Reality**.</span><span class="sxs-lookup"><span data-stu-id="040ad-176">If not, select the **+** button at the bottom of the list and choose **Windows Mixed Reality**.</span></span>

>[!NOTE]
><span data-ttu-id="040ad-177">Si vous ne voyez pas l’icône **plateforme Windows universelle** , vérifiez que vous avez sélectionné plateforme Windows universelle prise en charge de la génération pendant l’installation.</span><span class="sxs-lookup"><span data-stu-id="040ad-177">If you do not see the **Universal Windows Platform** icon, double check to make sure you selected Universal Windows Platform Build Support during installation.</span></span> <span data-ttu-id="040ad-178">Si ce n’est pas le cas, vous devrez peut-être réinstaller Unity avec l’installation de Windows appropriée.</span><span class="sxs-lookup"><span data-stu-id="040ad-178">If not, you may need to reinstall Unity with the correct Windows installation.</span></span>

<span data-ttu-id="040ad-179">Travail étonnant d’obtenir tous les paramètres de projet appliqués.</span><span class="sxs-lookup"><span data-stu-id="040ad-179">Awesome job on getting all the project settings applied.</span></span> <span data-ttu-id="040ad-180">Nous allons ensuite ajouter un hologramme !</span><span class="sxs-lookup"><span data-stu-id="040ad-180">Next, let us add a hologram!</span></span>

## <a name="chapter-4---create-a-cube"></a><span data-ttu-id="040ad-181">Chapitre 4-créer un cube</span><span class="sxs-lookup"><span data-stu-id="040ad-181">Chapter 4 - Create a cube</span></span>

>[!VIDEO https://www.youtube.com/embed/qKcK1Yuj-HQ]

<span data-ttu-id="040ad-182">La création d’un cube dans votre projet Unity est identique à la création d’un autre objet dans Unity.</span><span class="sxs-lookup"><span data-stu-id="040ad-182">Creating a cube in your Unity project is just like creating any other object in Unity.</span></span> <span data-ttu-id="040ad-183">Le fait de placer un cube devant l’utilisateur est simple, car le système de coordonnées de Unity est mis en correspondance avec le monde réel, où un compteur dans Unity est approximativement un compteur dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="040ad-183">Placing a cube in front of the user is easy because Unity's coordinate system is mapped to the real world - where one meter in Unity is approximately one meter in the real world.</span></span>

1. <span data-ttu-id="040ad-184">Dans le coin supérieur gauche du panneau de **hiérarchie** , sélectionnez la liste déroulante **créer** , puis choisissez **objet 3D > cube**.</span><span class="sxs-lookup"><span data-stu-id="040ad-184">In the top left corner of the **Hierarchy** panel, select the **Create** dropdown and choose **3D Object > Cube**.</span></span>
2. <span data-ttu-id="040ad-185">Sélectionner le **cube** nouvellement créé dans le volet de **hiérarchie**</span><span class="sxs-lookup"><span data-stu-id="040ad-185">Select the newly created **Cube** in the **Hierarchy** panel</span></span>
3. <span data-ttu-id="040ad-186">Dans l' **inspecteur** , recherchez le composant **transformer** et changez **position** en (**X**: 0, **Y**: 0, **Z**: 2).</span><span class="sxs-lookup"><span data-stu-id="040ad-186">In the **Inspector** find the **Transform** component and change **Position** to (**X**: 0, **Y**: 0, **Z**: 2).</span></span> <span data-ttu-id="040ad-187">*Cela positionne le cube 2 mètres devant la position de départ de l’utilisateur.*</span><span class="sxs-lookup"><span data-stu-id="040ad-187">*This positions the cube 2 meters in front of the user's starting position.*</span></span>
4. <span data-ttu-id="040ad-188">Dans le composant **transformer** , remplacez **rotation** par (**x**: 45, **Y**: 45, **z**: 45) et remplacez **adapter** par (**x**: 0,25, **y**: 0,25, **z**: 0,25).</span><span class="sxs-lookup"><span data-stu-id="040ad-188">In the **Transform** component, change **Rotation** to (**X**: 45, **Y**: 45, **Z**: 45) and change **Scale** to (**X**: 0.25, **Y**: 0.25, **Z**: 0.25).</span></span> <span data-ttu-id="040ad-189">*Le cube est mis à l’échelle sur 0,25 mètres.*</span><span class="sxs-lookup"><span data-stu-id="040ad-189">*This scales the cube to 0.25 meters.*</span></span>
5. <span data-ttu-id="040ad-190">Pour enregistrer les modifications de la scène, sélectionnez **fichier > enregistrer la scène**.</span><span class="sxs-lookup"><span data-stu-id="040ad-190">To save the scene changes, select **File > Save Scene**.</span></span>

## <a name="chapter-5---verify-on-device-from-unity-editor"></a><span data-ttu-id="040ad-191">Chapitre 5-vérification sur l’appareil à partir de l’éditeur Unity</span><span class="sxs-lookup"><span data-stu-id="040ad-191">Chapter 5 - Verify on device from Unity editor</span></span>

>[!VIDEO https://www.youtube.com/embed/vmCfiIdRb6Q]

<span data-ttu-id="040ad-192">Maintenant que nous avons créé notre cube, il est temps d’effectuer une vérification rapide de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="040ad-192">Now that we have created our cube, it is time to do a quick check in device.</span></span> <span data-ttu-id="040ad-193">Vous pouvez le faire directement à partir de l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="040ad-193">You can do this directly from within the Unity editor.</span></span>

### <a name="initial-setup"></a><span data-ttu-id="040ad-194">Configuration initiale</span><span class="sxs-lookup"><span data-stu-id="040ad-194">Initial setup</span></span>

1. <span data-ttu-id="040ad-195">Sur votre PC de développement, dans Unity, ouvrez le **fichier >** la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="040ad-195">On your development PC, in Unity, open **File > Build Settings** window.</span></span>
2. <span data-ttu-id="040ad-196">Remplacez **Platform** par **plateforme Windows universelle** , puis cliquez sur **switch Platform** .</span><span class="sxs-lookup"><span data-stu-id="040ad-196">Change **Platform** to **Universal Windows Platform** and click **Switch Platform**</span></span>

### <a name="for-hololens-use-unity-remoting"></a><span data-ttu-id="040ad-197">Pour utiliser la communication à distance Unity pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="040ad-197">For HoloLens use Unity Remoting</span></span>

1. <span data-ttu-id="040ad-198">Sur votre HoloLens, installez et exécutez le [lecteur de communication à distance holographique](holographic-remoting-player.md), disponible à partir du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="040ad-198">On your HoloLens, install and run the [Holographic Remoting Player](holographic-remoting-player.md), available from the Windows Store.</span></span> <span data-ttu-id="040ad-199">Lancez l’application sur l’appareil. elle entrera en état d’attente et affichera l’adresse IP de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="040ad-199">Launch the application on the device, and it will enter a waiting state and show the IP address of the device.</span></span> <span data-ttu-id="040ad-200">Notez l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="040ad-200">Note down the IP.</span></span>
2. <span data-ttu-id="040ad-201">Ouvrez **windows > XR > émulation holographique**.</span><span class="sxs-lookup"><span data-stu-id="040ad-201">Open **Window > XR > Holographic Emulation**.</span></span>
3. <span data-ttu-id="040ad-202">Remplacez le **mode** d’émulation **aucun** par **distant par appareil**.</span><span class="sxs-lookup"><span data-stu-id="040ad-202">Change **Emulation Mode** from **None** to **Remote to Device**.</span></span>
4. <span data-ttu-id="040ad-203">Dans **ordinateur distant**, entrez l’adresse IP de votre HoloLens indiquée précédemment.</span><span class="sxs-lookup"><span data-stu-id="040ad-203">In **Remote Machine**, enter the IP address of your HoloLens noted earlier.</span></span>
5. <span data-ttu-id="040ad-204">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="040ad-204">Click **Connect**.</span></span>
6. <span data-ttu-id="040ad-205">Vérifiez que l’état de la **connexion** devient vert **connecté**.</span><span class="sxs-lookup"><span data-stu-id="040ad-205">Ensure the **Connection Status** changes to green **Connected**.</span></span>
7. <span data-ttu-id="040ad-206">Vous pouvez maintenant cliquer sur **lire** dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="040ad-206">Now you can now click **Play** in the Unity editor.</span></span>

<span data-ttu-id="040ad-207">Vous pouvez maintenant voir le cube dans l’appareil et dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="040ad-207">You will now be able to see the cube in device and in the editor.</span></span> <span data-ttu-id="040ad-208">Vous pouvez suspendre, inspecter des objets et effectuer un débogage comme s’il s’agissait d’une application dans l’éditeur, car c’est essentiellement ce qui se passe, mais avec les données vidéo, audio et d’appareil transmises sur le réseau entre l’ordinateur hôte et l’appareil.</span><span class="sxs-lookup"><span data-stu-id="040ad-208">You can pause, inspect objects, and debug just like you are running an app in the editor, because that's essentially what's happening, but with video, audio, and device input transmitted back and forth across the network between the host machine and the device.</span></span>

### <a name="for-other-mixed-reality-supported-headsets"></a><span data-ttu-id="040ad-209">Pour les autres casques pris en charge par la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="040ad-209">For other mixed reality supported headsets</span></span>

1. <span data-ttu-id="040ad-210">Connectez le casque à votre PC de développement à l’aide du câble USB et du câble HDMI ou du port d’affichage.</span><span class="sxs-lookup"><span data-stu-id="040ad-210">Connect the headset to your development PC using the USB cable and the HDMI or display port cable.</span></span>
2. <span data-ttu-id="040ad-211">Lancez le **portail de réalité mixte** et assurez-vous que vous avez effectué la première expérience d’exécution.</span><span class="sxs-lookup"><span data-stu-id="040ad-211">Launch the **Mixed Reality Portal** and ensure you have completed the first run experience.</span></span>
3. <span data-ttu-id="040ad-212">À partir de Unity, vous pouvez maintenant appuyer sur le bouton de lecture.</span><span class="sxs-lookup"><span data-stu-id="040ad-212">From Unity, you can now press the Play button.</span></span>

<span data-ttu-id="040ad-213">Vous pouvez maintenant voir le rendu du cube dans votre casque de réalité mixte et dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="040ad-213">You will now be able to see the cube rendering in your mixed reality headset and in the editor.</span></span>

## <a name="chapter-6---build-and-deploy-to-device-from-visual-studio"></a><span data-ttu-id="040ad-214">Chapitre 6-générer et déployer sur un appareil à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="040ad-214">Chapter 6 - Build and deploy to device from Visual Studio</span></span>

>[!VIDEO https://www.youtube.com/embed/USSu8yHUdbk]

<span data-ttu-id="040ad-215">Nous sommes maintenant prêts à compiler notre projet dans Visual Studio et à le déployer sur notre appareil cible.</span><span class="sxs-lookup"><span data-stu-id="040ad-215">We are now ready to compile our project to Visual Studio and deploy to our target device.</span></span>

### <a name="export-to-the-visual-studio-solution"></a><span data-ttu-id="040ad-216">Exporter vers la solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="040ad-216">Export to the Visual Studio solution</span></span>

1. <span data-ttu-id="040ad-217">Ouvrez le **fichier >** la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="040ad-217">Open **File > Build Settings** window.</span></span>
1. <span data-ttu-id="040ad-218">Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.</span><span class="sxs-lookup"><span data-stu-id="040ad-218">Click **Add Open Scenes** to add the scene.</span></span>
1. <span data-ttu-id="040ad-219">Remplacez **Platform** par **plateforme Windows universelle** , puis cliquez sur **switch Platform**.</span><span class="sxs-lookup"><span data-stu-id="040ad-219">Change **Platform** to **Universal Windows Platform** and click **Switch Platform**.</span></span>
1. <span data-ttu-id="040ad-220">Dans **plateforme Windows universelle** paramètres, assurez-vous que le **Kit SDK** est **Universal 10**.</span><span class="sxs-lookup"><span data-stu-id="040ad-220">In **Universal Windows Platform** settings, ensure **SDK** is **Universal 10**.</span></span>
1. <span data-ttu-id="040ad-221">Pour appareil cible, laissez **un appareil** pour bloqués afficher ou basculer vers **HoloLens**.</span><span class="sxs-lookup"><span data-stu-id="040ad-221">For Target device, leave to **Any Device** for occluded displays or switch to **HoloLens**.</span></span>
1. <span data-ttu-id="040ad-222">Le **type de build UWP** doit être **D3D**.</span><span class="sxs-lookup"><span data-stu-id="040ad-222">**UWP Build Type** should be **D3D**.</span></span>
1. <span data-ttu-id="040ad-223">Le **Kit de développement logiciel (SDK) UWP** peut être laissé sur le **dernier installé**.</span><span class="sxs-lookup"><span data-stu-id="040ad-223">**UWP SDK** could be left at **Latest installed**.</span></span>
1. <span data-ttu-id="040ad-224">Cliquez sur **Générer**.</span><span class="sxs-lookup"><span data-stu-id="040ad-224">Click **Build**.</span></span>
1. <span data-ttu-id="040ad-225">Dans l’Explorateur de fichiers, cliquez sur **nouveau dossier** et nommez le dossier **« app »**.</span><span class="sxs-lookup"><span data-stu-id="040ad-225">In the file explorer, click **New Folder** and name the folder **"App"**.</span></span>
1. <span data-ttu-id="040ad-226">Après avoir sélectionné le dossier de l' **application** , cliquez sur le bouton **Sélectionner un dossier** .</span><span class="sxs-lookup"><span data-stu-id="040ad-226">With the **App** folder selected, click the **Select Folder** button.</span></span>
1. <span data-ttu-id="040ad-227">Une fois la création d’Unity terminée, une fenêtre de l’Explorateur de fichiers Windows s’affiche.</span><span class="sxs-lookup"><span data-stu-id="040ad-227">When Unity is done building, a Windows File Explorer window will appear.</span></span>
1. <span data-ttu-id="040ad-228">Ouvrez le dossier de l' **application** dans l’Explorateur de fichiers.</span><span class="sxs-lookup"><span data-stu-id="040ad-228">Open the **App** folder in file explorer.</span></span>
1. <span data-ttu-id="040ad-229">Ouvrez la solution Visual Studio générée (MixedRealityIntroduction. sln dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="040ad-229">Open the generated Visual Studio solution (MixedRealityIntroduction.sln in this example)</span></span>

### <a name="compile-the-visual-studio-solution"></a><span data-ttu-id="040ad-230">Compiler la solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="040ad-230">Compile the Visual Studio solution</span></span>

<span data-ttu-id="040ad-231">Enfin, nous allons compiler la solution Visual Studio exportée, la déployer et l’essayer sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="040ad-231">Finally, we will compile the exported Visual Studio solution, deploy it, and try it out on the device.</span></span>

1. <span data-ttu-id="040ad-232">À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible **Debug** par **Release** et de **ARM** par **x86**.</span><span class="sxs-lookup"><span data-stu-id="040ad-232">Using the top toolbar in Visual Studio, change the target from **Debug** to **Release** and from **ARM** to **X86**.</span></span>

<span data-ttu-id="040ad-233">Les instructions diffèrent pour le déploiement sur un appareil et sur l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="040ad-233">The instructions differ for deploying to a device versus the emulator.</span></span> <span data-ttu-id="040ad-234">Suivez les instructions qui correspondent à votre configuration.</span><span class="sxs-lookup"><span data-stu-id="040ad-234">Follow the instructions that match your setup.</span></span>

### <a name="deploy-to-mixed-reality-device-over-wi-fi"></a><span data-ttu-id="040ad-235">Déployer sur un appareil de réalité mixte via Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="040ad-235">Deploy to mixed reality device over Wi-Fi</span></span>

1. <span data-ttu-id="040ad-236">Cliquez sur la flèche en regard du bouton **ordinateur local** , puis remplacez la cible de déploiement par **ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="040ad-236">Click on the arrow next to the **Local Machine** button, and change the deployment target to **Remote Machine**.</span></span>
2. <span data-ttu-id="040ad-237">Entrez l’adresse IP de votre appareil de réalité mixte et changez le **mode d’authentification en mode** universel (protocole non chiffré) pour HoloLens et **Windows** pour les autres appareils.</span><span class="sxs-lookup"><span data-stu-id="040ad-237">Enter the IP address of your mixed reality device and change **Authentication Mode** to Universal (Unencrypted Protocol) for HoloLens and **Windows** for other devices.</span></span>
3. <span data-ttu-id="040ad-238">Cliquez sur **Déboguer > exécuter sans débogage**.</span><span class="sxs-lookup"><span data-stu-id="040ad-238">Click **Debug > Start without debugging**.</span></span>

<span data-ttu-id="040ad-239">**Pour HoloLens**, s’il s’agit de la première fois que vous déployez sur votre appareil, vous devez effectuer un jumelage [à l’aide de Visual Studio](using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="040ad-239">**For HoloLens**, If this is the first time deploying to your device, you will need to pair [using Visual Studio](using-visual-studio.md).</span></span>

### <a name="deploy-to-mixed-reality-device-over-usb"></a><span data-ttu-id="040ad-240">Déployer sur un appareil de réalité mixte sur USB</span><span class="sxs-lookup"><span data-stu-id="040ad-240">Deploy to mixed reality device over USB</span></span>

<span data-ttu-id="040ad-241">Assurez-vous que l’appareil est branché via le câble USB.</span><span class="sxs-lookup"><span data-stu-id="040ad-241">Ensure you device is plugged in via the USB cable.</span></span>

1. <span data-ttu-id="040ad-242">**Pour HoloLens**, cliquez sur la flèche en regard du bouton **ordinateur local** , puis remplacez la cible de déploiement par **appareil**.</span><span class="sxs-lookup"><span data-stu-id="040ad-242">**For HoloLens**, click on the arrow next to the **Local Machine** button, and change the deployment target to **Device**.</span></span>
2. <span data-ttu-id="040ad-243">**Pour cibler des appareils bloqués connectés à votre PC**, conservez le paramètre sur la machine locale.</span><span class="sxs-lookup"><span data-stu-id="040ad-243">**For targeting occluded devices attached to your PC**, keep the setting to Local Machine.</span></span> <span data-ttu-id="040ad-244">Assurez-vous que le portail de la **réalité mixte** est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="040ad-244">Ensure you have the **Mixed Reality Portal** running.</span></span>
3. <span data-ttu-id="040ad-245">Cliquez sur **Déboguer > exécuter sans débogage**.</span><span class="sxs-lookup"><span data-stu-id="040ad-245">Click **Debug > Start without debugging**.</span></span>

### <a name="deploy-to-emulator"></a><span data-ttu-id="040ad-246">Déployer sur l’émulateur</span><span class="sxs-lookup"><span data-stu-id="040ad-246">Deploy to Emulator</span></span>

1. <span data-ttu-id="040ad-247">Cliquez sur la flèche en regard du bouton **périphérique** , puis dans la liste déroulante, sélectionnez **émulateur HoloLens**.</span><span class="sxs-lookup"><span data-stu-id="040ad-247">Click on the arrow next to the **Device** button, and from drop down select **HoloLens Emulator**.</span></span>
2. <span data-ttu-id="040ad-248">Cliquez sur **Déboguer > exécuter sans débogage**.</span><span class="sxs-lookup"><span data-stu-id="040ad-248">Click **Debug > Start without debugging**.</span></span>

### <a name="try-out-your-app"></a><span data-ttu-id="040ad-249">Essayer votre application</span><span class="sxs-lookup"><span data-stu-id="040ad-249">Try out your app</span></span>

<span data-ttu-id="040ad-250">Maintenant que votre application est déployée, essayez de déplacer tout autour du cube et observez qu’il reste dans le monde.</span><span class="sxs-lookup"><span data-stu-id="040ad-250">Now that your app is deployed, try moving all around the cube and observe that it stays in the world in front of you.</span></span>

## <a name="see-also"></a><span data-ttu-id="040ad-251">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="040ad-251">See also</span></span>

* [<span data-ttu-id="040ad-252">Vue d’ensemble du développement Unity</span><span class="sxs-lookup"><span data-stu-id="040ad-252">Unity development overview</span></span>](unity-development-overview.md)
* [<span data-ttu-id="040ad-253">Bonnes pratiques sur l’utilisation d’Unity et de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="040ad-253">Best practices for working with Unity and Visual Studio</span></span>](best-practices-for-working-with-unity-and-visual-studio.md)
* [<span data-ttu-id="040ad-254">Réalité mixte - Principes fondamentaux - Cours 101</span><span class="sxs-lookup"><span data-stu-id="040ad-254">MR Basics 101</span></span>](holograms-101.md)
* [<span data-ttu-id="040ad-255">Réalité mixte - Principes fondamentaux - Cours 101E</span><span class="sxs-lookup"><span data-stu-id="040ad-255">MR Basics 101E</span></span>](holograms-101e.md)
