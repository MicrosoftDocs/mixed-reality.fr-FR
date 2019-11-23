---
title: 'Étude de cas : création de HoloSketch, mise en page spatiale et application d’esquisse UX pour HoloLens'
description: HoloSketch est une disposition spatiale sur un appareil et un outil d’esquisse de l’expérience utilisateur pour HoloLens pour faciliter la génération d’expériences holographiques.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: HoloSketch, HoloLens, Windows Mixed Reality, ébauche, application
ms.openlocfilehash: d6d22aae7709bcc1a33b142a100d1a0f9645d3cc
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73436946"
---
# <a name="case-study---building-holosketch-a-spatial-layout-and-ux-sketching-app-for-hololens"></a><span data-ttu-id="0c1f0-104">Étude de cas : création de HoloSketch, mise en page spatiale et application d’esquisse UX pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="0c1f0-104">Case study - Building HoloSketch, a spatial layout and UX sketching app for HoloLens</span></span>

<span data-ttu-id="0c1f0-105">HoloSketch est une disposition spatiale sur un appareil et un outil d’esquisse de l’expérience utilisateur pour HoloLens pour faciliter la génération d’expériences holographiques.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-105">HoloSketch is an on-device spatial layout and UX sketching tool for HoloLens to help build holographic experiences.</span></span> <span data-ttu-id="0c1f0-106">HoloSketch fonctionne avec un clavier et une souris Bluetooth couplés, ainsi que des commandes vocales et de mouvement.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-106">HoloSketch works with a paired Bluetooth keyboard and mouse as well as gesture and voice commands.</span></span> <span data-ttu-id="0c1f0-107">L’objectif de HoloSketch est de fournir un outil de disposition d’expérience utilisateur simple pour une visualisation et une itération rapides.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-107">The purpose of HoloSketch is to provide a simple UX layout tool for quick visualization and iteration.</span></span>

<span data-ttu-id="0c1f0-108">![HoloSketch : présentation spatiale et application d’esquisse de l’expérience utilisateur pour HoloLens.](images/holosketch-image-01-640px.png)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-108">![HoloSketch: A spatial layout and UX sketching app for HoloLens.](images/holosketch-image-01-640px.png)</span></span><br>
<span data-ttu-id="0c1f0-109">*HoloSketch : présentation spatiale et application d’esquisse de l’expérience utilisateur pour HoloLens*</span><span class="sxs-lookup"><span data-stu-id="0c1f0-109">*HoloSketch: spatial layout and UX sketching app for HoloLens*</span></span>

<span data-ttu-id="0c1f0-110">![un outil simple d’expérience utilisateur pour une visualisation et une itération rapides.](images/holosketch-image-02.png)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-110">![A simple UX layout tool for quick visualization and iteration.](images/holosketch-image-02.png)</span></span><br>
<span data-ttu-id="0c1f0-111">*Outil de disposition d’expérience utilisateur simple pour une visualisation et une itération rapides*</span><span class="sxs-lookup"><span data-stu-id="0c1f0-111">*A simple UX layout tool for quick visualization and iteration*</span></span>

## <a name="features"></a><span data-ttu-id="0c1f0-112">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="0c1f0-112">Features</span></span>

### <a name="primitives-for-quick-studies-and-scale-prototyping"></a><span data-ttu-id="0c1f0-113">Primitives pour les études rapides et le prototypage à l’échelle</span><span class="sxs-lookup"><span data-stu-id="0c1f0-113">Primitives for quick studies and scale-prototyping</span></span>

![Utilisation de formes primitives](images/holosketch-primitives-giphy.gif)

<span data-ttu-id="0c1f0-115">Utilisez des formes primitives pour les études de masse rapide et le prototypage à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-115">Use primitive shapes for quick massing studies and scale-prototyping.</span></span>

### <a name="import-objects-through-onedrive"></a><span data-ttu-id="0c1f0-116">Importer des objets via OneDrive</span><span class="sxs-lookup"><span data-stu-id="0c1f0-116">Import objects through OneDrive</span></span>

![importation d’objets](images/holosketch-importobjects-giphy.gif)

<span data-ttu-id="0c1f0-118">Importez des images PNG/JPG ou des objets 3D FBX (nécessite un Packaging dans Unity) dans l’espace de la réalité mixte via OneDrive.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-118">Import PNG/JPG images or 3D FBX objects(requires packaging in Unity) into the mixed reality space through OneDrive.</span></span>

### <a name="manipulate-objects"></a><span data-ttu-id="0c1f0-119">Manipuler des objets</span><span class="sxs-lookup"><span data-stu-id="0c1f0-119">Manipulate objects</span></span>

![manipulation d’objets](images/manipulate-objects-640px.jpg)

<span data-ttu-id="0c1f0-121">Manipuler des objets (déplacer/faire pivoter/mettre à l’échelle) avec une interface d’objet 3D familière.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-121">Manipulate objects (move/rotate/scale) with a familiar 3D object interface.</span></span>

### <a name="bluetooth-mousekeyboard-gestures-and-voice-commands"></a><span data-ttu-id="0c1f0-122">Bluetooth, souris/clavier, mouvements et commandes vocales</span><span class="sxs-lookup"><span data-stu-id="0c1f0-122">Bluetooth, mouse/keyboard, gestures and voice commands</span></span>

![prend en charge Bluetooth](images/supports-bluetooth-640px.jpg)

<span data-ttu-id="0c1f0-124">HoloSketch prend en charge la souris, le clavier, les gestes et les commandes vocales Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-124">HoloSketch supports Bluetooth mouse/keyboard, gestures and voice commands.</span></span>

## <a name="background"></a><span data-ttu-id="0c1f0-125">Présentation</span><span class="sxs-lookup"><span data-stu-id="0c1f0-125">Background</span></span>

### <a name="importance-of-experiencing-your-design-in-the-device"></a><span data-ttu-id="0c1f0-126">Importance de la conception de l’appareil</span><span class="sxs-lookup"><span data-stu-id="0c1f0-126">Importance of experiencing your design in the device</span></span>

<span data-ttu-id="0c1f0-127">Quand vous concevez un élément pour HoloLens, il est important d’expérimenter votre conception dans l’appareil.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-127">When you design something for HoloLens, it is important to experience your design in the device.</span></span> <span data-ttu-id="0c1f0-128">L’un des plus grands défis de la conception d’applications de réalité mixte est qu’il est difficile d’avoir une idée de la mise à l’échelle, de la position et de la profondeur, en particulier par le biais des croquis 2D traditionnels.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-128">One of the biggest challenges in mixed reality app design is that it is hard to get the sense of scale, position and depth, especially through traditional 2D sketches.</span></span>

### <a name="cost-of-2d-based-communication"></a><span data-ttu-id="0c1f0-129">Coût de la communication en 2D</span><span class="sxs-lookup"><span data-stu-id="0c1f0-129">Cost of 2D based communication</span></span>

<span data-ttu-id="0c1f0-130">Pour communiquer efficacement des flux et des scénarios d’expérience utilisateur à d’autres utilisateurs, un concepteur peut finir par consacrer beaucoup de temps à la création de ressources à l’aide d’outils 2D traditionnels tels qu’Illustrator, Photoshop et PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-130">To effectively communicate UX flows and scenarios to others, a designer may end up spending a lot of time creating assets using traditional 2D tools such as Illustrator, Photoshop and PowerPoint.</span></span> <span data-ttu-id="0c1f0-131">Ces conceptions 2D nécessitent souvent des efforts supplémentaires pour les convertir en 3D.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-131">These 2D designs often require additional effort to convert them it into 3D.</span></span> <span data-ttu-id="0c1f0-132">Certaines idées sont perdues dans cette traduction de 2D en 3D.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-132">Some ideas are lost in this translation from 2D to 3D.</span></span>

### <a name="complex-deployment-process"></a><span data-ttu-id="0c1f0-133">Processus de déploiement complexe</span><span class="sxs-lookup"><span data-stu-id="0c1f0-133">Complex deployment process</span></span>

<span data-ttu-id="0c1f0-134">Étant donné que la réalité mixte est un nouveau canevas pour nous, elle implique un grand nombre d’itérations de conception et d’essais et d’erreurs par nature.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-134">Since mixed reality is a new canvas for us, it involves a lot of design iteration and trial and error by its nature.</span></span> <span data-ttu-id="0c1f0-135">Pour les concepteurs qui ne sont pas familiarisés avec les outils tels que Unity et Visual Studio, il n’est pas facile de rassembler des éléments dans HoloLens.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-135">For designer who are not familiar with tools such as Unity and Visual Studio, it is not easy to put something together in HoloLens.</span></span> <span data-ttu-id="0c1f0-136">En général, vous devez suivre le processus ci-dessous pour voir votre illustration 2D/3D dans l’appareil.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-136">Typically you have to go through the process below to see your 2D/3D artwork in the device.</span></span> <span data-ttu-id="0c1f0-137">C’était un grand obstacle pour les concepteurs qui itèrent rapidement sur les idées et les scénarios.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-137">This was a big barrier for designers iterating on ideas and scenarios quickly.</span></span>

<span data-ttu-id="0c1f0-138">![processus de déploiement complexe](images/holosketch-image-03-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-138">![Complex deployment process](images/holosketch-image-03-1000px.png)</span></span><br>
<span data-ttu-id="0c1f0-139">*Processus de déploiement*</span><span class="sxs-lookup"><span data-stu-id="0c1f0-139">*Deployment process*</span></span>

### <a name="simplified-process-with-holosketch"></a><span data-ttu-id="0c1f0-140">Processus simplifié avec HoloSketch</span><span class="sxs-lookup"><span data-stu-id="0c1f0-140">Simplified process with HoloSketch</span></span>

<span data-ttu-id="0c1f0-141">Avec HoloSketch, nous souhaitons simplifier ce processus sans impliquer les outils de développement et le jumelage des portails de périphériques.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-141">With HoloSketch, we wanted to simplify this process without involving development tools and device portal pairing.</span></span> <span data-ttu-id="0c1f0-142">À l’aide de OneDrive, les utilisateurs peuvent facilement placer des ressources 2D/3D dans HoloLens.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-142">Using OneDrive, users can easily put 2D/3D assets into HoloLens.</span></span>

<span data-ttu-id="0c1f0-143">![processus simplifié avec HoloSketch](images/holosketch-image-04-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-143">![Simplified process with HoloSketch](images/holosketch-image-04-1000px.png)</span></span><br>
<span data-ttu-id="0c1f0-144">*Processus simplifié avec HoloSketch*</span><span class="sxs-lookup"><span data-stu-id="0c1f0-144">*Simplified process with HoloSketch*</span></span>

### <a name="encouraging-three-dimensional-design-thinking-and-solutions"></a><span data-ttu-id="0c1f0-145">Encourager la pensée et les solutions de conception à trois dimensions</span><span class="sxs-lookup"><span data-stu-id="0c1f0-145">Encouraging three-dimensional design thinking and solutions</span></span>

<span data-ttu-id="0c1f0-146">Nous avons pensé que cet outil donne aux concepteurs la possibilité d’explorer les solutions dans un espace véritablement tridimensionnel et de ne pas être coincé en 2D.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-146">We thought this tool would give designers an opportunity to explore solutions in a truly three-dimensional space and not be stuck in 2D.</span></span> <span data-ttu-id="0c1f0-147">Ils n’ont pas à se soucier de la création d’un arrière-plan 3D pour leur interface utilisateur, car l’arrière-plan est le monde réel dans le cas de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-147">They don’t have to think about creating a 3D background for their UI since the background is the real world in the case of HoloLens.</span></span> <span data-ttu-id="0c1f0-148">HoloSketch permet aux concepteurs d’explorer facilement la conception 3D sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-148">HoloSketch opens up a way for designers to easily explore 3D design on HoloLens.</span></span>

## <a name="get-started"></a><span data-ttu-id="0c1f0-149">Prise en main</span><span class="sxs-lookup"><span data-stu-id="0c1f0-149">Get Started</span></span>

### <a name="how-to-import-2d-images-jpgpng-into-holosketch"></a><span data-ttu-id="0c1f0-150">Comment importer des images 2D (JPG/PNG) dans HoloSketch</span><span class="sxs-lookup"><span data-stu-id="0c1f0-150">How to import 2D images (JPG/PNG) into HoloSketch</span></span>

* <span data-ttu-id="0c1f0-151">Chargez des images JPG/PNG dans votre dossier OneDrive « documents/HoloSketch ».</span><span class="sxs-lookup"><span data-stu-id="0c1f0-151">Upload JPG/PNG images to your OneDrive folder ‘Documents/HoloSketch’.</span></span>
* <span data-ttu-id="0c1f0-152">Dans le menu OneDrive de HoloSketch, vous pourrez sélectionner et placer l’image dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-152">From the OneDrive menu in HoloSketch, you will be able to select and place the image in the environment.</span></span>

<span data-ttu-id="0c1f0-153">![l’importation d’images 2D](images/import-2d-images-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-153">![Importing 2D images](images/import-2d-images-1000px.jpg)</span></span><br>
<span data-ttu-id="0c1f0-154">*Importation d’images et d’objets 3D via OneDrive*</span><span class="sxs-lookup"><span data-stu-id="0c1f0-154">*Importing images and 3D objects through OneDrive*</span></span>

### <a name="how-to-import-3d-objects-into-holosketch"></a><span data-ttu-id="0c1f0-155">Comment importer des objets 3D dans HoloSketch</span><span class="sxs-lookup"><span data-stu-id="0c1f0-155">How to import 3D objects into HoloSketch</span></span>

<span data-ttu-id="0c1f0-156">Avant de télécharger vers votre dossier OneDrive, suivez les étapes ci-dessous pour empaqueter vos objets 3D dans un bundle d’actifs Unity.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-156">Before uploading to your OneDrive folder, please follow the steps below to package your 3D objects into a Unity asset bundle.</span></span> <span data-ttu-id="0c1f0-157">À l’aide de ce processus, vous pouvez importer vos fichiers FBX/OBJ à partir de logiciels 3D tels que Maya, Cinema 4D et Microsoft Paint 3D.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-157">Using this process you can import your FBX/OBJ files from 3D software such as Maya, Cinema 4D and Microsoft Paint 3D.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0c1f0-158">Actuellement, la création d’un groupe de ressources est prise en charge avec Unity version 5.4.5 F1.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-158">Currently, asset bundle creation is supported with Unity version 5.4.5f1.</span></span>

1. <span data-ttu-id="0c1f0-159">Téléchargez et ouvrez le projet Unity ['AssetBunlder_Unity'](https://github.com/Microsoft/MRDesignLabs/tree/master/ReleasedApps/HoloSketch/AssetBundler_Unity).</span><span class="sxs-lookup"><span data-stu-id="0c1f0-159">Download and open the Unity project ['AssetBunlder_Unity'](https://github.com/Microsoft/MRDesignLabs/tree/master/ReleasedApps/HoloSketch/AssetBundler_Unity).</span></span> <span data-ttu-id="0c1f0-160">Ce projet Unity comprend le script pour la génération de la ressource bundle.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-160">This Unity project includes the script for the bundle asset generation.</span></span>
2. <span data-ttu-id="0c1f0-161">Créez un nouveau GameObject.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-161">Create a new GameObject.</span></span>
3. <span data-ttu-id="0c1f0-162">Nommez le GameObject en fonction du contenu.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-162">Name the GameObject based on the contents.</span></span>
4. <span data-ttu-id="0c1f0-163">Dans le panneau de l’inspecteur, cliquez sur « Ajouter un composant » et ajoutez « conflit de boîte ».</span><span class="sxs-lookup"><span data-stu-id="0c1f0-163">In the Inspector panel, click ‘Add Component’ and add ‘Box Collider’.</span></span> 

   ![Dans le panneau de l’inspecteur, cliquez sur « Ajouter un composant » et ajoutez « conflit de boîte »](images/holosketch-10a-assetbundles-1000px.png)
   
   ![Dans le panneau de l’inspecteur, cliquez sur « Ajouter un composant » et ajoutez le #2 « Box de collision »](images/holosketch-10b-assetbundles-1000px.png)

5. <span data-ttu-id="0c1f0-166">Importez le fichier 3D FBX en le faisant glisser dans le panneau projet.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-166">Import the 3D FBX file by dragging it into the project panel.</span></span>
6. <span data-ttu-id="0c1f0-167">Faites glisser l’objet dans le volet de la hiérarchie **sous votre nouvelle gameobject**.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-167">Drag the object into the Hierarchy panel **under your new GameObject**.</span></span>

   ![Faites glisser l’objet dans le volet de la hiérarchie sous votre nouvelle GameObject](images/holosketch-12-assetbundles-1000px.png)

7. <span data-ttu-id="0c1f0-169">Ajustez la dimension de conflit si elle ne correspond pas à l’objet.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-169">Adjust the collider dimension if it does not match the object.</span></span> <span data-ttu-id="0c1f0-170">Faites pivoter l’objet en face **Z-AXIS**.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-170">Rotate the object to face **Z-axis**.</span></span>

   ![Ajustez la dimension de conflit si elle ne correspond pas à l’objet.](images/holosketch-13-assetbundles-1000px.png)

8. <span data-ttu-id="0c1f0-172">Faites glisser l’objet du panneau de la hiérarchie vers le panneau projet pour le **rendre Prefab**.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-172">Drag the object from the Hierarchy panel to the Project panel to **make it prefab**.</span></span>
9. <span data-ttu-id="0c1f0-173">En bas du panneau de l’inspecteur, cliquez sur la liste déroulante, créez et attribuez un nouveau nom unique.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-173">On the bottom of the inspector panel, click the dropdown, create and assign a new unique name.</span></span> <span data-ttu-id="0c1f0-174">L’exemple ci-dessous montre comment ajouter et assigner « brownchair » pour le nom de AssetBundle.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-174">Below example shows adding and assigning 'brownchair' for the AssetBundle Name.</span></span> 

   ![En bas du panneau de l’inspecteur, cliquez sur la liste déroulante et attribuez un nouveau nom unique.](images/holosketch-14-assetbundles-1000px.png)

10. <span data-ttu-id="0c1f0-176">Préparez une image miniature pour l’objet de modèle.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-176">Prepare a thumbnail image for the model object.</span></span> 
   <span data-ttu-id="0c1f0-177">![faites glisser une image dans le panneau projet et attribuez le nom utilisé pour l’objet.](images/holosketch-15-assetbundles-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-177">![Drag an image into the project panel and assign the name used for the object.](images/holosketch-15-assetbundles-1000px.png)</span></span>

11. <span data-ttu-id="0c1f0-178">Créez un dossier nommé « Assetbundles » sous le dossier « Asset » du projet Unity.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-178">Create a folder named ‘Assetbundles’ under the Unity project’s ‘Asset’ folder.</span></span>

12. <span data-ttu-id="0c1f0-179">Dans le menu ressources, sélectionnez « Générer AssetBundles » pour générer le fichier.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-179">From the Assets menu, select ‘Build AssetBundles’ to generate file.</span></span> 
   <span data-ttu-id="0c1f0-180">![dans le menu ressources, sélectionnez « Générer AssetBundles » pour générer le fichier.](images/holosketch-15a-assetbundles.png)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-180">![From the Assets menu, select ‘Build AssetBundles’ to generate file.](images/holosketch-15a-assetbundles.png)</span></span>


13. <span data-ttu-id="0c1f0-181">**Téléchargez le fichier généré dans le dossier/Files/Documents/HoloSketch sur OneDrive.**</span><span class="sxs-lookup"><span data-stu-id="0c1f0-181">**Upload the generated file to the /Files/Documents/HoloSketch folder on OneDrive.**</span></span> <span data-ttu-id="0c1f0-182">Charge uniquement le fichier asset_unique_name.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-182">Upload the asset_unique_name file only.</span></span> <span data-ttu-id="0c1f0-183">Vous n’avez pas besoin de charger des fichiers manifeste ou un fichier AssetBundles.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-183">You don’t need to upload manifest files or AssetBundles file.</span></span> <br>
<span data-ttu-id="0c1f0-184">![ajouter des fichiers à des fichiers/documents/HoloSketch/dossier](images/holosketch-onedriveupload-1000px.png)
![vous verrez ajouter un objet 3D dans le menu OneDrive de HoloSketch](images/holosketch-14-onedriveexample-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-184">![Add files to Files/Documents/HoloSketch/ folder](images/holosketch-onedriveupload-1000px.png)
![You will see added 3D object in HoloSketch's OneDrive menu](images/holosketch-14-onedriveexample-1000px.jpg)</span></span>

## <a name="how-to-manipulate-the-objects"></a><span data-ttu-id="0c1f0-185">Comment manipuler les objets</span><span class="sxs-lookup"><span data-stu-id="0c1f0-185">How to manipulate the objects</span></span>

<span data-ttu-id="0c1f0-186">HoloSketch prend en charge l’interface traditionnelle couramment utilisée dans les logiciels 3D.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-186">HoloSketch supports the traditional interface that is widely used in 3D software.</span></span> <span data-ttu-id="0c1f0-187">Vous pouvez utiliser déplacer, faire pivoter, mettre à l’échelle les objets avec des gestes et une souris.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-187">You can use move, rotate, scale the objects with gestures and a mouse.</span></span> <span data-ttu-id="0c1f0-188">Vous pouvez rapidement basculer entre les différents modes avec la voix ou le clavier.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-188">You can quickly switch between different modes with voice or keyboard.</span></span>

### <a name="object-manipulation-modes"></a><span data-ttu-id="0c1f0-189">Modes de manipulation d’objets</span><span class="sxs-lookup"><span data-stu-id="0c1f0-189">Object manipulation modes</span></span>

<span data-ttu-id="0c1f0-190">![comment manipuler les objets](images/holosketch-image-06-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-190">![How to manipulate the objects](images/holosketch-image-06-1000px.png)</span></span><br>
<span data-ttu-id="0c1f0-191">*Comment manipuler les objets*</span><span class="sxs-lookup"><span data-stu-id="0c1f0-191">*How to manipulate the objects*</span></span>

### <a name="contextual-and-tool-belt-menus"></a><span data-ttu-id="0c1f0-192">Menus contextuels et de la ceinture d’outils</span><span class="sxs-lookup"><span data-stu-id="0c1f0-192">Contextual and Tool Belt menus</span></span>

<span data-ttu-id="0c1f0-193">**Utilisation du menu contextuel**</span><span class="sxs-lookup"><span data-stu-id="0c1f0-193">**Using the Contextual Menu**</span></span>

<span data-ttu-id="0c1f0-194">Appuyez deux fois sur air pour ouvrir le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-194">Double air tap to open the Contextual Menu.</span></span> 

<span data-ttu-id="0c1f0-195">Éléments de menu :</span><span class="sxs-lookup"><span data-stu-id="0c1f0-195">Menu items:</span></span>
* <span data-ttu-id="0c1f0-196">**Surface de disposition :** Il s’agit d’un système de grille 3D dans lequel vous pouvez mettre en page plusieurs objets et les gérer en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-196">**Layout Surface:** This is a 3D grid system where you can layout multiple objects and manage them as a group.</span></span> <span data-ttu-id="0c1f0-197">Appuyez deux fois sur l’aire de disposition pour y ajouter des objets.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-197">Double air-tap on the Layout Surface to add objects to it.</span></span>
* <span data-ttu-id="0c1f0-198">**Primitives :** Utilisez des cubes, des sphères, des cylindres et des cônes pour les études de masse.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-198">**Primitives:** Use cubes, spheres, cylinders and cones for massing studies.</span></span>
* <span data-ttu-id="0c1f0-199">**OneDrive :** Ouvrez le menu OneDrive pour importer des objets.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-199">**OneDrive:** Open the OneDrive menu to import objects.</span></span>
* <span data-ttu-id="0c1f0-200">**Aide :** Affiche l’écran d’aide.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-200">**Help:** Displays help screen.</span></span>

<span data-ttu-id="0c1f0-201">menu contextuel ![](images/holosketch-image-07.png)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-201">![Contextual menu](images/holosketch-image-07.png)</span></span><br>
<span data-ttu-id="0c1f0-202">*Menu contextuel*</span><span class="sxs-lookup"><span data-stu-id="0c1f0-202">*Contextual menu*</span></span>

<span data-ttu-id="0c1f0-203">**Utilisation du menu de la ceinture d’outils**</span><span class="sxs-lookup"><span data-stu-id="0c1f0-203">**Using the Tool Belt Menu**</span></span>

<span data-ttu-id="0c1f0-204">Déplacer, faire pivoter, mettre à l’échelle, enregistrer et charger la scène sont disponibles dans le menu de la ceinture d’outils.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-204">Move, Rotate, Scale, Save, and Load Scene are available from the Tool Belt Menu.</span></span> 

## <a name="using-keyboard-gestures-and-voice-commands"></a><span data-ttu-id="0c1f0-205">Utilisation du clavier, des mouvements et des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="0c1f0-205">Using keyboard, gestures and voice commands</span></span>

<span data-ttu-id="0c1f0-206">![le clavier, les gestes et les commandes vocales](images/holosketch-image-08-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="0c1f0-206">![Keyboard, Gestures and Voice Commands](images/holosketch-image-08-1000px.png)</span></span><br>
<span data-ttu-id="0c1f0-207">*Clavier, mouvements et commandes vocales*</span><span class="sxs-lookup"><span data-stu-id="0c1f0-207">*Keyboard, gestures, and voice commands*</span></span>

## <a name="download-the-app"></a><span data-ttu-id="0c1f0-208">Télécharger l’application</span><span class="sxs-lookup"><span data-stu-id="0c1f0-208">Download the app</span></span>

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="HoloSketch app icon" width="60" height="60" src="images/holosketch-app-icon.png">
</td>
<td style="border-style: none"><span data-ttu-id="0c1f0-209"><a href="https://www.microsoft.com/store/p/holosketch/9p3br4t5m4tv">Téléchargez et installez l’application HoloSketch gratuitement à partir du Microsoft Store</a>
</span><span class="sxs-lookup"><span data-stu-id="0c1f0-209"><a href="https://www.microsoft.com/store/p/holosketch/9p3br4t5m4tv">Download and install the HoloSketch app for free from the Microsoft Store</a>
</span></span></td>
</tr>
</table>

## <a name="known-issues"></a><span data-ttu-id="0c1f0-210">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="0c1f0-210">Known issues</span></span>
* <span data-ttu-id="0c1f0-211">La création du groupement d’actifs est prise en charge avec **Unity version 5.4.5 F1.**</span><span class="sxs-lookup"><span data-stu-id="0c1f0-211">Currently asset bundle creation is supported with **Unity version 5.4.5f1.**</span></span>
* <span data-ttu-id="0c1f0-212">Selon la quantité de données de votre OneDrive, l’application peut apparaître comme si elle s’était arrêtée lors du chargement du contenu OneDrive</span><span class="sxs-lookup"><span data-stu-id="0c1f0-212">Depending on the amount of data in your OneDrive, the app might appear as if it has stopped while loading OneDrive contents</span></span>
* <span data-ttu-id="0c1f0-213">Actuellement, la fonctionnalité d’enregistrement et de chargement ne prend en charge que les objets primitifs</span><span class="sxs-lookup"><span data-stu-id="0c1f0-213">Currently, Save and Load feature only supports primitive objects</span></span>
* <span data-ttu-id="0c1f0-214">Les menus texte, audio, vidéo et photo sont désactivés dans le menu contextuel</span><span class="sxs-lookup"><span data-stu-id="0c1f0-214">Text, Sound, Video and Photo menus are disabled on the contextual menu</span></span>
* <span data-ttu-id="0c1f0-215">Le bouton de lecture du menu de la ceinture d’outils efface le gizmos de manipulation.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-215">The Play button on the Tool Belt menu clears the manipulation gizmos</span></span>

## <a name="sharing-your-sketches"></a><span data-ttu-id="0c1f0-216">Partage de vos croquis</span><span class="sxs-lookup"><span data-stu-id="0c1f0-216">Sharing your sketches</span></span>

<span data-ttu-id="0c1f0-217">Vous pouvez utiliser la fonctionnalité d’enregistrement vidéo dans HoloLens en indiquant « Hey Cortana, Start/Stop Recording ».</span><span class="sxs-lookup"><span data-stu-id="0c1f0-217">You can use the video recording feature in HoloLens by saying 'Hey Cortana, Start/Stop recording'.</span></span> <span data-ttu-id="0c1f0-218">Appuyez sur la touche haut/flèche du volume pour prendre une photo de votre croquis.</span><span class="sxs-lookup"><span data-stu-id="0c1f0-218">Press the volume up/down key together to take a picture of your sketch.</span></span>

## <a name="about-the-authors"></a><span data-ttu-id="0c1f0-219">À propos des auteurs</span><span class="sxs-lookup"><span data-stu-id="0c1f0-219">About the authors</span></span>

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><span data-ttu-id="0c1f0-220"><b>Dong Yoon Park</b></span><span class="sxs-lookup"><span data-stu-id="0c1f0-220"><b>Dong Yoon Park</b></span></span><br><span data-ttu-id="0c1f0-221">@Microsoft du concepteur UX</span><span class="sxs-lookup"><span data-stu-id="0c1f0-221">UX Designer @Microsoft</span></span></td>
</tr>
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Patrick Sebring" width="60" height="60" src="images/paseb-60px.jpg"></td>
<td style="border-style: none"><span data-ttu-id="0c1f0-222"><b>Patrick</b></span><span class="sxs-lookup"><span data-stu-id="0c1f0-222"><b>Patrick Sebring</b></span></span><br><span data-ttu-id="0c1f0-223">@Microsoft de développement</span><span class="sxs-lookup"><span data-stu-id="0c1f0-223">Developer @Microsoft</span></span></td>
</tr>
</table> 
