---
title: Étude de cas - HoloSketch de génération, une disposition spatiale et un UX esquisse d’application pour HoloLens
description: HoloSketch est disposition spatiale sur l’appareil et l’expérience utilisateur esquisse outil pour HoloLens aider à créer des expériences HOLOGRAPHIQUE.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: HoloSketch, HoloLens, Windows Mixed Reality, esquisse, application
ms.openlocfilehash: d7f94a09bf4a8a16000c2345adf1a046dab4bd15
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594279"
---
# <a name="case-study---building-holosketch-a-spatial-layout-and-ux-sketching-app-for-hololens"></a><span data-ttu-id="b51c7-104">Étude de cas - HoloSketch de génération, une disposition spatiale et un UX esquisse d’application pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="b51c7-104">Case study - Building HoloSketch, a spatial layout and UX sketching app for HoloLens</span></span>

<span data-ttu-id="b51c7-105">HoloSketch est disposition spatiale sur l’appareil et l’expérience utilisateur esquisse outil pour HoloLens aider à créer des expériences HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="b51c7-105">HoloSketch is an on-device spatial layout and UX sketching tool for HoloLens to help build holographic experiences.</span></span> <span data-ttu-id="b51c7-106">HoloSketch fonctionne avec un commandes de clavier et souris ainsi que gestuelle et vocale Bluetooth couplé.</span><span class="sxs-lookup"><span data-stu-id="b51c7-106">HoloSketch works with a paired Bluetooth keyboard and mouse as well as gesture and voice commands.</span></span> <span data-ttu-id="b51c7-107">HoloSketch vise à fournir un outil de mise en page de l’expérience utilisateur simple pour l’itération et de visualisation rapide.</span><span class="sxs-lookup"><span data-stu-id="b51c7-107">The purpose of HoloSketch is to provide a simple UX layout tool for quick visualization and iteration.</span></span>

<span data-ttu-id="b51c7-108">![HoloSketch : Une disposition spatiale et un UX esquisse d’application pour HoloLens.](images/holosketch-image-01-640px.png)</span><span class="sxs-lookup"><span data-stu-id="b51c7-108">![HoloSketch: A spatial layout and UX sketching app for HoloLens.](images/holosketch-image-01-640px.png)</span></span><br>
<span data-ttu-id="b51c7-109">*HoloSketch : disposition spatiale et l’expérience utilisateur esquisse d’application pour HoloLens*</span><span class="sxs-lookup"><span data-stu-id="b51c7-109">*HoloSketch: spatial layout and UX sketching app for HoloLens*</span></span>

<span data-ttu-id="b51c7-110">![Un simple outil de disposition de l’expérience utilisateur visualisation rapide et une itération.](images/holosketch-image-02.png)</span><span class="sxs-lookup"><span data-stu-id="b51c7-110">![A simple UX layout tool for quick visualization and iteration.](images/holosketch-image-02.png)</span></span><br>
<span data-ttu-id="b51c7-111">*Un outil de mise en page de l’expérience utilisateur simple visualisation rapide et une itération*</span><span class="sxs-lookup"><span data-stu-id="b51c7-111">*A simple UX layout tool for quick visualization and iteration*</span></span>

## <a name="features"></a><span data-ttu-id="b51c7-112">Fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="b51c7-112">Features</span></span>

### <a name="primitives-for-quick-studies-and-scale-prototyping"></a><span data-ttu-id="b51c7-113">Primitives pour les études rapide et mise à l’échelle-prototypage</span><span class="sxs-lookup"><span data-stu-id="b51c7-113">Primitives for quick studies and scale-prototyping</span></span>

![À l’aide de formes primitifs](images/holosketch-primitives-giphy.gif)

<span data-ttu-id="b51c7-115">Utiliser des formes primitifs pour études massing rapides et mise à l’échelle-prototypage.</span><span class="sxs-lookup"><span data-stu-id="b51c7-115">Use primitive shapes for quick massing studies and scale-prototyping.</span></span>

### <a name="import-objects-through-onedrive"></a><span data-ttu-id="b51c7-116">Importer des objets via OneDrive</span><span class="sxs-lookup"><span data-stu-id="b51c7-116">Import objects through OneDrive</span></span>

![l’importation d’objets](images/holosketch-importobjects-giphy.gif)

<span data-ttu-id="b51c7-118">Importer des images PNG/JPG ou objets FBX 3D (nécessite l’empaquetage dans Unity) dans l’espace de réalité mixte via OneDrive.</span><span class="sxs-lookup"><span data-stu-id="b51c7-118">Import PNG/JPG images or 3D FBX objects(requires packaging in Unity) into the mixed reality space through OneDrive.</span></span>

### <a name="manipulate-objects"></a><span data-ttu-id="b51c7-119">Manipuler des objets</span><span class="sxs-lookup"><span data-stu-id="b51c7-119">Manipulate objects</span></span>

![manipulation des objets](images/manipulate-objects-640px.jpg)

<span data-ttu-id="b51c7-121">Manipuler des objets (déplacement/faire pivoter/mise à l’échelle) avec une interface familière objet 3D.</span><span class="sxs-lookup"><span data-stu-id="b51c7-121">Manipulate objects (move/rotate/scale) with a familiar 3D object interface.</span></span>

### <a name="bluetooth-mousekeyboard-gestures-and-voice-commands"></a><span data-ttu-id="b51c7-122">Bluetooth, clavier/souris, mouvements et les commandes vocales</span><span class="sxs-lookup"><span data-stu-id="b51c7-122">Bluetooth, mouse/keyboard, gestures and voice commands</span></span>

![prend en charge de Bluetooth](images/supports-bluetooth-640px.jpg)

<span data-ttu-id="b51c7-124">HoloSketch prend en charge clavier/souris Bluetooth, les mouvements et les commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="b51c7-124">HoloSketch supports Bluetooth mouse/keyboard, gestures and voice commands.</span></span>

## <a name="background"></a><span data-ttu-id="b51c7-125">Arrière-plan</span><span class="sxs-lookup"><span data-stu-id="b51c7-125">Background</span></span>

### <a name="importance-of-experiencing-your-design-in-the-device"></a><span data-ttu-id="b51c7-126">Importance de rencontre votre conception de l’appareil</span><span class="sxs-lookup"><span data-stu-id="b51c7-126">Importance of experiencing your design in the device</span></span>

<span data-ttu-id="b51c7-127">Lorsque vous concevez quelque chose pour HoloLens, il est important profiter de votre conception de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="b51c7-127">When you design something for HoloLens, it is important to experience your design in the device.</span></span> <span data-ttu-id="b51c7-128">Un des plus grands défis dans la conception d’applications de réalité mixte est qu’il est difficile d’obtenir le sens de mise à l’échelle, de position et de profondeur, en particulier par le biais des croquis 2D traditionnels.</span><span class="sxs-lookup"><span data-stu-id="b51c7-128">One of the biggest challenges in mixed reality app design is that it is hard to get the sense of scale, position and depth, especially through traditional 2D sketches.</span></span>

### <a name="cost-of-2d-based-communication"></a><span data-ttu-id="b51c7-129">Communication basée sur le coût de 2D</span><span class="sxs-lookup"><span data-stu-id="b51c7-129">Cost of 2D based communication</span></span>

<span data-ttu-id="b51c7-130">Pour communiquer efficacement des flux de l’expérience utilisateur et des scénarios pour d’autres, un concepteur peut retrouver beaucoup de temps à créer des ressources à l’aide des outils traditionnels 2D comme Illustrator, Photoshop et PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="b51c7-130">To effectively communicate UX flows and scenarios to others, a designer may end up spending a lot of time creating assets using traditional 2D tools such as Illustrator, Photoshop and PowerPoint.</span></span> <span data-ttu-id="b51c7-131">Ces conceptions 2D nécessitent souvent un effort supplémentaire pour les convertir en 3D.</span><span class="sxs-lookup"><span data-stu-id="b51c7-131">These 2D designs often require additional effort to convert them it into 3D.</span></span> <span data-ttu-id="b51c7-132">Quelques idées sont perdues dans cette traduction à partir de 2D en 3D.</span><span class="sxs-lookup"><span data-stu-id="b51c7-132">Some ideas are lost in this translation from 2D to 3D.</span></span>

### <a name="complex-deployment-process"></a><span data-ttu-id="b51c7-133">Processus de déploiement complexes</span><span class="sxs-lookup"><span data-stu-id="b51c7-133">Complex deployment process</span></span>

<span data-ttu-id="b51c7-134">Étant donné que la réalité mixte est un nouveau canevas pour nous, elle implique un grand nombre d’itération de conception et d’essais et erreurs par sa nature.</span><span class="sxs-lookup"><span data-stu-id="b51c7-134">Since mixed reality is a new canvas for us, it involves a lot of design iteration and trial and error by its nature.</span></span> <span data-ttu-id="b51c7-135">Concepteur qui ne sont pas familiers avec les outils tels que Unity et Visual Studio, il n’est pas simple de créer quelque chose dans HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b51c7-135">For designer who are not familiar with tools such as Unity and Visual Studio, it is not easy to put something together in HoloLens.</span></span> <span data-ttu-id="b51c7-136">En général, vous devez passer par le processus ci-dessous pour voir votre illustration 2D/3D dans l’appareil.</span><span class="sxs-lookup"><span data-stu-id="b51c7-136">Typically you have to go through the process below to see your 2D/3D artwork in the device.</span></span> <span data-ttu-id="b51c7-137">Il s’agissait d’une barrière big pour itérer rapidement sur des idées et des scénarios de concepteurs.</span><span class="sxs-lookup"><span data-stu-id="b51c7-137">This was a big barrier for designers iterating on ideas and scenarios quickly.</span></span>

<span data-ttu-id="b51c7-138">![Processus de déploiement complexes](images/holosketch-image-03-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="b51c7-138">![Complex deployment process](images/holosketch-image-03-1000px.png)</span></span><br>
<span data-ttu-id="b51c7-139">*Processus de déploiement*</span><span class="sxs-lookup"><span data-stu-id="b51c7-139">*Deployment process*</span></span>

### <a name="simplified-process-with-holosketch"></a><span data-ttu-id="b51c7-140">Processus simplifié avec HoloSketch</span><span class="sxs-lookup"><span data-stu-id="b51c7-140">Simplified process with HoloSketch</span></span>

<span data-ttu-id="b51c7-141">Avec HoloSketch, nous souhaitons sans impliquer des outils de développement et le périphérique portail jumelage de simplifier ce processus.</span><span class="sxs-lookup"><span data-stu-id="b51c7-141">With HoloSketch, we wanted to simplify this process without involving development tools and device portal pairing.</span></span> <span data-ttu-id="b51c7-142">L’utilisation de OneDrive, les utilisateurs peuvent placer facilement les éléments multimédias en 2D/3D dans HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b51c7-142">Using OneDrive, users can easily put 2D/3D assets into HoloLens.</span></span>

<span data-ttu-id="b51c7-143">![Processus simplifié avec HoloSketch](images/holosketch-image-04-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="b51c7-143">![Simplified process with HoloSketch](images/holosketch-image-04-1000px.png)</span></span><br>
<span data-ttu-id="b51c7-144">*Processus simplifié avec HoloSketch*</span><span class="sxs-lookup"><span data-stu-id="b51c7-144">*Simplified process with HoloSketch*</span></span>

### <a name="encouraging-three-dimensional-design-thinking-and-solutions"></a><span data-ttu-id="b51c7-145">Encourager la pensée de conception en trois dimensions et des solutions</span><span class="sxs-lookup"><span data-stu-id="b51c7-145">Encouraging three-dimensional design thinking and solutions</span></span>

<span data-ttu-id="b51c7-146">Nous avons pensé que cet outil donnerait concepteurs une opportunité pour Explorer les solutions dans un espace tridimensionnel véritablement et ne pas être bloqué en 2D.</span><span class="sxs-lookup"><span data-stu-id="b51c7-146">We thought this tool would give designers an opportunity to explore solutions in a truly three-dimensional space and not be stuck in 2D.</span></span> <span data-ttu-id="b51c7-147">Ils n’ont pas de réfléchir à la création d’un arrière-plan 3D pour leur interface utilisateur dans la mesure où l’arrière-plan est le monde réel dans le cas de Hololens.</span><span class="sxs-lookup"><span data-stu-id="b51c7-147">They don’t have to think about creating a 3D background for their UI since the background is the real world in the case of Hololens.</span></span> <span data-ttu-id="b51c7-148">HoloSketch ouvre un moyen pour les concepteurs d’Explorer facilement conception 3D sur Hololens.</span><span class="sxs-lookup"><span data-stu-id="b51c7-148">HoloSketch opens up a way for designers to easily explore 3D design on Hololens.</span></span>

## <a name="get-started"></a><span data-ttu-id="b51c7-149">Prise en main</span><span class="sxs-lookup"><span data-stu-id="b51c7-149">Get Started</span></span>

### <a name="how-to-import-2d-images-jpgpng-into-holosketch"></a><span data-ttu-id="b51c7-150">Comment importer des images 2D (JPG/PNG) dans HoloSketch</span><span class="sxs-lookup"><span data-stu-id="b51c7-150">How to import 2D images (JPG/PNG) into HoloSketch</span></span>

* <span data-ttu-id="b51c7-151">Charger des images JPG/PNG dans votre dossier OneDrive « Documents/HoloSketch ».</span><span class="sxs-lookup"><span data-stu-id="b51c7-151">Upload JPG/PNG images to your OneDrive folder ‘Documents/HoloSketch’.</span></span>
* <span data-ttu-id="b51c7-152">Dans le menu OneDrive HoloSketch, vous serez en mesure de sélectionner et de placer l’image dans l’environnement.</span><span class="sxs-lookup"><span data-stu-id="b51c7-152">From the OneDrive menu in HoloSketch, you will be able to select and place the image in the environment.</span></span>

<span data-ttu-id="b51c7-153">![L’importation d’images 2D](images/import-2d-images-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="b51c7-153">![Importing 2D images](images/import-2d-images-1000px.jpg)</span></span><br>
<span data-ttu-id="b51c7-154">*L’importation d’images et des objets 3D via OneDrive*</span><span class="sxs-lookup"><span data-stu-id="b51c7-154">*Importing images and 3D objects through OneDrive*</span></span>

### <a name="how-to-import-3d-objects-into-holosketch"></a><span data-ttu-id="b51c7-155">Comment importer des objets 3D dans HoloSketch</span><span class="sxs-lookup"><span data-stu-id="b51c7-155">How to import 3D objects into HoloSketch</span></span>

<span data-ttu-id="b51c7-156">Avant de charger dans votre dossier OneDrive, suivez les étapes ci-dessous pour empaqueter vos objets 3D dans un groupe de ressources Unity.</span><span class="sxs-lookup"><span data-stu-id="b51c7-156">Before uploading to your OneDrive folder, please follow the steps below to package your 3D objects into a Unity asset bundle.</span></span> <span data-ttu-id="b51c7-157">À l’aide de ce processus vous pouvez importer vos fichiers FBX/OBJ contre les logiciels 3D telles que Maya, cinéma 4D et Microsoft Paint 3D.</span><span class="sxs-lookup"><span data-stu-id="b51c7-157">Using this process you can import your FBX/OBJ files from 3D software such as Maya, Cinema 4D and Microsoft Paint 3D.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b51c7-158">Actuellement, la création du regroupement actif est pris en charge avec Unity version 5.4.5f1.</span><span class="sxs-lookup"><span data-stu-id="b51c7-158">Currently, asset bundle creation is supported with Unity version 5.4.5f1.</span></span>

1. <span data-ttu-id="b51c7-159">Téléchargez et ouvrez le projet Unity ['AssetBunlder_Unity'](https://github.com/Microsoft/MRDesignLabs/tree/master/ReleasedApps/HoloSketch/AssetBundler_Unity).</span><span class="sxs-lookup"><span data-stu-id="b51c7-159">Download and open the Unity project ['AssetBunlder_Unity'](https://github.com/Microsoft/MRDesignLabs/tree/master/ReleasedApps/HoloSketch/AssetBundler_Unity).</span></span> <span data-ttu-id="b51c7-160">Ce projet Unity inclut le script pour la génération de la ressource offre groupée.</span><span class="sxs-lookup"><span data-stu-id="b51c7-160">This Unity project includes the script for the bundle asset generation.</span></span>
2. <span data-ttu-id="b51c7-161">Créer un nouveau GameObject.</span><span class="sxs-lookup"><span data-stu-id="b51c7-161">Create a new GameObject.</span></span>
3. <span data-ttu-id="b51c7-162">Nommez le GameObject en fonction du contenu.</span><span class="sxs-lookup"><span data-stu-id="b51c7-162">Name the GameObject based on the contents.</span></span>
4. <span data-ttu-id="b51c7-163">Dans ce panneau, cliquez sur Ajouter un composant et ajouter « Boîte Collider ».</span><span class="sxs-lookup"><span data-stu-id="b51c7-163">In the Inspector panel, click ‘Add Component’ and add ‘Box Collider’.</span></span> 

   ![Dans ce panneau, cliquez sur Ajouter un composant et ajoutez « Collider case »](images/holosketch-10a-assetbundles-1000px.png)
   
   ![Dans ce panneau, cliquez sur Ajouter un composant et ajoutez « boîte Collider' #2](images/holosketch-10b-assetbundles-1000px.png)

5. <span data-ttu-id="b51c7-166">Importer le fichier FBX 3D en le faisant glisser dans le panneau de configuration de projet.</span><span class="sxs-lookup"><span data-stu-id="b51c7-166">Import the 3D FBX file by dragging it into the project panel.</span></span>
6. <span data-ttu-id="b51c7-167">Faites glisser l’objet dans le volet hiérarchie **sous votre nouveau GameObject**.</span><span class="sxs-lookup"><span data-stu-id="b51c7-167">Drag the object into the Hierarchy panel **under your new GameObject**.</span></span>

   ![Faites glisser l’objet dans le volet de la hiérarchie sous votre nouveau GameObject](images/holosketch-12-assetbundles-1000px.png)

7. <span data-ttu-id="b51c7-169">Ajustez la dimension collider si elle ne correspond pas à l’objet.</span><span class="sxs-lookup"><span data-stu-id="b51c7-169">Adjust the collider dimension if it does not match the object.</span></span> <span data-ttu-id="b51c7-170">Faire pivoter l’objet pour faire face à **z**.</span><span class="sxs-lookup"><span data-stu-id="b51c7-170">Rotate the object to face **Z-axis**.</span></span>

   ![Ajustez la dimension de collider si elle ne correspond pas à l’objet.](images/holosketch-13-assetbundles-1000px.png)

8. <span data-ttu-id="b51c7-172">Faites glisser l’objet à partir du Panneau de la hiérarchie vers le panneau de projet pour **rendent prefab**.</span><span class="sxs-lookup"><span data-stu-id="b51c7-172">Drag the object from the Hierarchy panel to the Project panel to **make it prefab**.</span></span>
9. <span data-ttu-id="b51c7-173">Au bas de ce panneau, cliquez sur la liste déroulante, créer et affecter un nouveau nom unique.</span><span class="sxs-lookup"><span data-stu-id="b51c7-173">On the bottom of the inspector panel, click the dropdown, create and assign a new unique name.</span></span> <span data-ttu-id="b51c7-174">Exemple ci-dessous illustre l’ajout et l’affectation de « brownchair » pour le nom AssetBundle.</span><span class="sxs-lookup"><span data-stu-id="b51c7-174">Below example shows adding and assigning 'brownchair' for the AssetBundle Name.</span></span> 

   ![Au bas de ce panneau, cliquez sur la liste déroulante et affecter un nouveau nom unique.](images/holosketch-14-assetbundles-1000px.png)

10. <span data-ttu-id="b51c7-176">Préparer une image miniature de l’objet de modèle.</span><span class="sxs-lookup"><span data-stu-id="b51c7-176">Prepare a thumbnail image for the model object.</span></span> 
   <span data-ttu-id="b51c7-177">![Faites glisser une image dans le panneau de configuration de projet, puis attribuez le nom utilisé pour l’objet.](images/holosketch-15-assetbundles-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="b51c7-177">![Drag an image into the project panel and assign the name used for the object.](images/holosketch-15-assetbundles-1000px.png)</span></span>

11. <span data-ttu-id="b51c7-178">Créez un dossier nommé « Assetbundles » sous le dossier de « Actifs » du projet Unity.</span><span class="sxs-lookup"><span data-stu-id="b51c7-178">Create a folder named ‘Assetbundles’ under the Unity project’s ‘Asset’ folder.</span></span>

12. <span data-ttu-id="b51c7-179">Dans le menu de ressources, sélectionnez « Build AssetBundles' pour générer le fichier.</span><span class="sxs-lookup"><span data-stu-id="b51c7-179">From the Assets menu, select ‘Build AssetBundles’ to generate file.</span></span> 
   <span data-ttu-id="b51c7-180">![Dans le menu de ressources, sélectionnez « Build AssetBundles' pour générer le fichier.](images/holosketch-15a-assetbundles.png)</span><span class="sxs-lookup"><span data-stu-id="b51c7-180">![From the Assets menu, select ‘Build AssetBundles’ to generate file.](images/holosketch-15a-assetbundles.png)</span></span>


13. <span data-ttu-id="b51c7-181">**Chargez le fichier généré dans le dossier /Files/Documents/HoloSketch sur OneDrive.**</span><span class="sxs-lookup"><span data-stu-id="b51c7-181">**Upload the generated file to the /Files/Documents/HoloSketch folder on OneDrive.**</span></span> <span data-ttu-id="b51c7-182">Téléchargez le fichier asset_unique_name uniquement.</span><span class="sxs-lookup"><span data-stu-id="b51c7-182">Upload the asset_unique_name file only.</span></span> <span data-ttu-id="b51c7-183">Vous n’avez pas besoin de télécharger des fichiers manifeste ou AssetBundles fichier.</span><span class="sxs-lookup"><span data-stu-id="b51c7-183">You don’t need to upload manifest files or AssetBundles file.</span></span> <br>
<span data-ttu-id="b51c7-184">![Ajouter des fichiers à des fichiers/Documents/HoloSketch/dossier](images/holosketch-onedriveupload-1000px.png)
![vous verrez un objet 3D ajouté dans le menu de OneDrive de HoloSketch](images/holosketch-14-onedriveexample-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="b51c7-184">![Add files to Files/Documents/HoloSketch/ folder](images/holosketch-onedriveupload-1000px.png)
![You will see added 3D object in HoloSketch's OneDrive menu](images/holosketch-14-onedriveexample-1000px.jpg)</span></span>

## <a name="how-to-manipulate-the-objects"></a><span data-ttu-id="b51c7-185">Comment manipuler les objets</span><span class="sxs-lookup"><span data-stu-id="b51c7-185">How to manipulate the objects</span></span>

<span data-ttu-id="b51c7-186">HoloSketch prend en charge l’interface traditionnelle est largement utilisé dans les logiciels 3D.</span><span class="sxs-lookup"><span data-stu-id="b51c7-186">HoloSketch supports the traditional interface that is widely used in 3D software.</span></span> <span data-ttu-id="b51c7-187">Vous pouvez utiliser le déplacement, faire pivoter, mettre à l’échelle les objets avec des mouvements et une souris.</span><span class="sxs-lookup"><span data-stu-id="b51c7-187">You can use move, rotate, scale the objects with gestures and a mouse.</span></span> <span data-ttu-id="b51c7-188">Vous pouvez rapidement basculer entre différents modes avec voix ou du clavier.</span><span class="sxs-lookup"><span data-stu-id="b51c7-188">You can quickly switch between different modes with voice or keyboard.</span></span>

### <a name="object-manipulation-modes"></a><span data-ttu-id="b51c7-189">Modes de manipulation d’objet</span><span class="sxs-lookup"><span data-stu-id="b51c7-189">Object manipulation modes</span></span>

<span data-ttu-id="b51c7-190">![Comment manipuler les objets](images/holosketch-image-06-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="b51c7-190">![How to manipulate the objects](images/holosketch-image-06-1000px.png)</span></span><br>
<span data-ttu-id="b51c7-191">*Comment manipuler les objets*</span><span class="sxs-lookup"><span data-stu-id="b51c7-191">*How to manipulate the objects*</span></span>

### <a name="contextual-and-tool-belt-menus"></a><span data-ttu-id="b51c7-192">Menus contextuelles et ' s Tool Belt</span><span class="sxs-lookup"><span data-stu-id="b51c7-192">Contextual and Tool Belt menus</span></span>

<span data-ttu-id="b51c7-193">**Utilisez le Menu contextuel**</span><span class="sxs-lookup"><span data-stu-id="b51c7-193">**Using the Contextual Menu**</span></span>

<span data-ttu-id="b51c7-194">Double appui pour ouvrir le Menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="b51c7-194">Double air tap to open the Contextual Menu.</span></span> 

<span data-ttu-id="b51c7-195">Éléments de menu :</span><span class="sxs-lookup"><span data-stu-id="b51c7-195">Menu items:</span></span>
* <span data-ttu-id="b51c7-196">**Surface de disposition :** Ceci est un système de grille 3D dans lequel vous pouvez disposer plusieurs objets et les gérer en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="b51c7-196">**Layout Surface:** This is a 3D grid system where you can layout multiple objects and manage them as a group.</span></span> <span data-ttu-id="b51c7-197">Double-appui sur la Surface de disposition pour ajouter des objets.</span><span class="sxs-lookup"><span data-stu-id="b51c7-197">Double air-tap on the Layout Surface to add objects to it.</span></span>
* <span data-ttu-id="b51c7-198">**Primitives :** Utilisez des cubes, de domaines, de cylindre et de cône pour massing études.</span><span class="sxs-lookup"><span data-stu-id="b51c7-198">**Primitives:** Use cubes, spheres, cylinders and cones for massing studies.</span></span>
* <span data-ttu-id="b51c7-199">**OneDrive :** Ouvrez le menu OneDrive pour importer des objets.</span><span class="sxs-lookup"><span data-stu-id="b51c7-199">**OneDrive:** Open the OneDrive menu to import objects.</span></span>
* <span data-ttu-id="b51c7-200">**Aide :** Affiche l’écran d’aide.</span><span class="sxs-lookup"><span data-stu-id="b51c7-200">**Help:** Displays help screen.</span></span>

<span data-ttu-id="b51c7-201">![Menu contextuel](images/holosketch-image-07.png)</span><span class="sxs-lookup"><span data-stu-id="b51c7-201">![Contextual menu](images/holosketch-image-07.png)</span></span><br>
<span data-ttu-id="b51c7-202">*Menu contextuel*</span><span class="sxs-lookup"><span data-stu-id="b51c7-202">*Contextual menu*</span></span>

<span data-ttu-id="b51c7-203">**L’aide du Menu de la ceinture outil**</span><span class="sxs-lookup"><span data-stu-id="b51c7-203">**Using the Tool Belt Menu**</span></span>

<span data-ttu-id="b51c7-204">Déplacer, faire pivoter, mettre à l’échelle, enregistrer et la scène de charge sont disponibles dans le Menu de la ceinture outil.</span><span class="sxs-lookup"><span data-stu-id="b51c7-204">Move, Rotate, Scale, Save, and Load Scene are available from the Tool Belt Menu.</span></span> 

## <a name="using-keyboard-gestures-and-voice-commands"></a><span data-ttu-id="b51c7-205">À l’aide du clavier, les mouvements et les commandes vocales</span><span class="sxs-lookup"><span data-stu-id="b51c7-205">Using keyboard, gestures and voice commands</span></span>

<span data-ttu-id="b51c7-206">![Clavier, les mouvements et les commandes vocales](images/holosketch-image-08-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="b51c7-206">![Keyboard, Gestures and Voice Commands](images/holosketch-image-08-1000px.png)</span></span><br>
<span data-ttu-id="b51c7-207">*Clavier, les mouvements et les commandes vocales*</span><span class="sxs-lookup"><span data-stu-id="b51c7-207">*Keyboard, gestures, and voice commands*</span></span>

## <a name="download-the-app"></a><span data-ttu-id="b51c7-208">Télécharger l’application</span><span class="sxs-lookup"><span data-stu-id="b51c7-208">Download the app</span></span>

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="HoloSketch app icon" width="60" height="60" src="images/holosketch-app-icon.png">
</td>
<td style="border-style: none"><span data-ttu-id="b51c7-209"><a href="https://www.microsoft.com/store/p/holosketch/9p3br4t5m4tv">Téléchargez et installez l’application HoloSketch gratuitement à partir du Microsoft Store</a>
</span><span class="sxs-lookup"><span data-stu-id="b51c7-209"><a href="https://www.microsoft.com/store/p/holosketch/9p3br4t5m4tv">Download and install the HoloSketch app for free from the Microsoft Store</a>
</span></span></td>
</tr>
</table>

## <a name="known-issues"></a><span data-ttu-id="b51c7-210">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="b51c7-210">Known issues</span></span>
* <span data-ttu-id="b51c7-211">Actuellement pris en charge de la création de regroupement des éléments multimédias avec **Unity version 5.4.5f1.**</span><span class="sxs-lookup"><span data-stu-id="b51c7-211">Currently asset bundle creation is supported with **Unity version 5.4.5f1.**</span></span>
* <span data-ttu-id="b51c7-212">Selon la quantité de données dans votre OneDrive, l’application peut apparaître comme s’il s’est arrêté lors du chargement du contenu de OneDrive</span><span class="sxs-lookup"><span data-stu-id="b51c7-212">Depending on the amount of data in your OneDrive, the app might appear as if it has stopped while loading OneDrive contents</span></span>
* <span data-ttu-id="b51c7-213">Actuellement, enregistrer et la fonctionnalité de chargement prend uniquement en charge les objets de type primitif</span><span class="sxs-lookup"><span data-stu-id="b51c7-213">Currently, Save and Load feature only supports primitive objects</span></span>
* <span data-ttu-id="b51c7-214">Texte, audio, vidéo et Photo menus sont désactivés dans le menu contextuel</span><span class="sxs-lookup"><span data-stu-id="b51c7-214">Text, Sound, Video and Photo menus are disabled on the contextual menu</span></span>
* <span data-ttu-id="b51c7-215">Le bouton lecture dans le menu's Tool Belt efface les gizmos de manipulation</span><span class="sxs-lookup"><span data-stu-id="b51c7-215">The Play button on the Tool Belt menu clears the manipulation gizmos</span></span>

## <a name="sharing-your-sketches"></a><span data-ttu-id="b51c7-216">Partage de votre croquis</span><span class="sxs-lookup"><span data-stu-id="b51c7-216">Sharing your sketches</span></span>

<span data-ttu-id="b51c7-217">Vous pouvez utiliser la fonctionnalité d’enregistrement vidéo dans HoloLens en disant « Hey Cortana, l’enregistrement de démarrage/arrêt ».</span><span class="sxs-lookup"><span data-stu-id="b51c7-217">You can use the video recording feature in HoloLens by saying 'Hey Cortana, Start/Stop recording'.</span></span> <span data-ttu-id="b51c7-218">Appuyez sur le volume haut/bas clé ensemble pour prendre une photo de votre ébauche de projet.</span><span class="sxs-lookup"><span data-stu-id="b51c7-218">Press the volume up/down key together to take a picture of your sketch.</span></span>

## <a name="about-the-authors"></a><span data-ttu-id="b51c7-219">À propos des auteurs</span><span class="sxs-lookup"><span data-stu-id="b51c7-219">About the authors</span></span>

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><span data-ttu-id="b51c7-220"><b>Dong Yoon Park</b></span><span class="sxs-lookup"><span data-stu-id="b51c7-220"><b>Dong Yoon Park</b></span></span><br><span data-ttu-id="b51c7-221">Concepteur UX @Microsoft</span><span class="sxs-lookup"><span data-stu-id="b51c7-221">UX Designer @Microsoft</span></span></td>
</tr>
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Patrick Sebring" width="60" height="60" src="images/paseb-60px.jpg"></td>
<td style="border-style: none"><span data-ttu-id="b51c7-222"><b>Patrick Sebring</b></span><span class="sxs-lookup"><span data-stu-id="b51c7-222"><b>Patrick Sebring</b></span></span><br><span data-ttu-id="b51c7-223">Développeur @Microsoft</span><span class="sxs-lookup"><span data-stu-id="b51c7-223">Developer @Microsoft</span></span></td>
</tr>
</table> 
