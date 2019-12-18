---
title: Didacticiels audio spatiaux-3. L’aménagement de l’audio à partir d’une vidéo
description: Importez un élément multimédia vidéo dans votre projet Unity et spatialez l’audio de la vidéo.
author: kegodin
ms.author: kegodin
ms.date: 12/01/2019
ms.topic: article
keywords: réalité mixte, Unity, tutorial, hololens2, audio spatial
ms.openlocfilehash: 1e5c84fd7d14cc5edc78839bbdf91590cc7fd8e7
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75182746"
---
# <a name="spatializing-audio-from-a-video"></a><span data-ttu-id="4d4c1-105">L’aménagement de l’audio à partir d’une vidéo</span><span class="sxs-lookup"><span data-stu-id="4d4c1-105">Spatializing audio from a video</span></span>
<span data-ttu-id="4d4c1-106">Dans ce troisième chapitre du module audio spatial des didacticiels HoloLens 2 Unity, vous allez :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-106">In this 3rd chapter of the spatial audio module of the HoloLens 2 Unity tutorials, you'll:</span></span>
* <span data-ttu-id="4d4c1-107">Importer une vidéo et ajouter un lecteur vidéo</span><span class="sxs-lookup"><span data-stu-id="4d4c1-107">Import a video and add a Video Player</span></span>
* <span data-ttu-id="4d4c1-108">Lire la vidéo sur un Quadrangle</span><span class="sxs-lookup"><span data-stu-id="4d4c1-108">Play the video onto a quadrangle</span></span>
* <span data-ttu-id="4d4c1-109">Acheminer l’audio de la vidéo vers le Quadrangle et spatialiser l’audio</span><span class="sxs-lookup"><span data-stu-id="4d4c1-109">Route audio from the video to the quadrangle, and spatialize the audio</span></span>

## <a name="import-a-video-and-add-a-video-player"></a><span data-ttu-id="4d4c1-110">Importer une vidéo et ajouter un lecteur vidéo</span><span class="sxs-lookup"><span data-stu-id="4d4c1-110">Import a video and add a Video Player</span></span>

<span data-ttu-id="4d4c1-111">Faites glisser un fichier vidéo dans le volet **projet** de votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-111">Drag a video file into the **Project** pane in your Unity project.</span></span> <span data-ttu-id="4d4c1-112">Vous pouvez utiliser [cette vidéo](https://github.com/microsoft/spatialaudio-unity/blob/develop/Samples/MicrosoftSpatializerSample/Assets/Microsoft%20HoloLens%20-%20Spatial%20Sound-PTPvx7mDon4.mp4?raw=true) à partir de l’exemple de projet de son spatial.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-112">You can use [this video](https://github.com/microsoft/spatialaudio-unity/blob/develop/Samples/MicrosoftSpatializerSample/Assets/Microsoft%20HoloLens%20-%20Spatial%20Sound-PTPvx7mDon4.mp4?raw=true) from the spatial audio sample project.</span></span>

![Dossier des ressources avec une vidéo](images/spatial-audio/assets-folder-with-video.png)

<span data-ttu-id="4d4c1-114">L’ajustement des paramètres de qualité sur le clip vidéo peut garantir une lecture douce sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-114">Adjusting the quality settings on the video clip can ensure smooth playback on HoloLens 2.</span></span> <span data-ttu-id="4d4c1-115">Cliquez sur le fichier vidéo dans le volet **projet** .</span><span class="sxs-lookup"><span data-stu-id="4d4c1-115">Click on the video file in the **Project** pane.</span></span> <span data-ttu-id="4d4c1-116">Ensuite, dans le volet de l' **inspecteur** du fichier vidéo, substituez les paramètres pour les applications du Windows Store et :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-116">Then in the **Inspector** pane for the video file, override the settings for Windows Store Apps, and:</span></span>
* <span data-ttu-id="4d4c1-117">Activer le **transcodage**</span><span class="sxs-lookup"><span data-stu-id="4d4c1-117">Enable **Transcode**</span></span>
* <span data-ttu-id="4d4c1-118">Définir le **codec** sur H264 –</span><span class="sxs-lookup"><span data-stu-id="4d4c1-118">Set **Codec** to H264</span></span>
* <span data-ttu-id="4d4c1-119">Définir le **Mode débit** sur faible</span><span class="sxs-lookup"><span data-stu-id="4d4c1-119">Set **Bitrate Mode** to Low</span></span>
* <span data-ttu-id="4d4c1-120">Définir la **qualité spatiale** sur une qualité spatiale moyenne</span><span class="sxs-lookup"><span data-stu-id="4d4c1-120">Set **Spatial Quality** to Medium Spatial Quality</span></span>

<span data-ttu-id="4d4c1-121">Après ces ajustements, le volet de l' **inspecteur** du fichier vidéo se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-121">After these adjustments, the **Inspector** pane for the video file will look like this:</span></span>

![Volet de propriétés vidéo](images/spatial-audio/video-property-pane.png)

<span data-ttu-id="4d4c1-123">Ensuite, ajoutez un objet **lecteur vidéo** à la **hiérarchie** en cliquant avec le bouton droit sur le volet **hiérarchie** et en choisissant **vidéo-> lecteur vidéo**:</span><span class="sxs-lookup"><span data-stu-id="4d4c1-123">Next, add a **Video Player** object to the **Hierarchy** by right-clicking on the **Hierarchy** pane and choosing **Video -> Video Player**:</span></span>

![Lecteur vidéo dans la hiérarchie](images/spatial-audio/video-player-in-hierarchy.png)

## <a name="play-video-onto-a-quadrangle"></a><span data-ttu-id="4d4c1-125">Lire une vidéo sur un Quadrangle</span><span class="sxs-lookup"><span data-stu-id="4d4c1-125">Play video onto a quadrangle</span></span>
<span data-ttu-id="4d4c1-126">L’objet **lecteur vidéo** a besoin d’un objet de jeu texturé sur lequel afficher la vidéo.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-126">The **Video Player** object needs a textured game object on which to render the video.</span></span> <span data-ttu-id="4d4c1-127">Tout d’abord, ajoutez un **quadruple** à votre **hiérarchie** en cliquant avec le bouton droit sur le volet **hiérarchie** et en choisissant **objet 3D-> Quad**:</span><span class="sxs-lookup"><span data-stu-id="4d4c1-127">First, add a **Quad** to your **Hierarchy** by right-clicking on the **Hierarchy** pane and choosing **3D Object -> Quad**:</span></span>

![Ajouter le Quad à la hiérarchie](images/spatial-audio/add-quad-to-hierarchy.png)

<span data-ttu-id="4d4c1-129">Pour vous assurer que le **Quad** s’affiche devant l’utilisateur au démarrage de l’application, définissez la propriété **position** du **quadruple** sur (0, 0, 2) et la propriété **Scale** sur (1,28, 0,72, 1).</span><span class="sxs-lookup"><span data-stu-id="4d4c1-129">To ensure the **Quad** appears in front of the user when the application starts, set the **Position** property of the **Quad** to (0, 0, 2), and the **Scale** property to (1.28, 0.72, 1).</span></span> <span data-ttu-id="4d4c1-130">Une fois ces modifications effectuées, le composant de **transformation** sur le volet de l' **inspecteur** pour le **Quad** ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-130">After these changes, the **Transform** component on the **Inspector** pane for the **Quad** will look like this:</span></span>

![Quadruple transformation](images/spatial-audio/quad-transform.png)

<span data-ttu-id="4d4c1-132">Pour texturer le **Quad** avec une vidéo, créez une **texture de rendu**.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-132">To texture the **Quad** with video, create a new **Render Texture**.</span></span> <span data-ttu-id="4d4c1-133">Dans le volet **projet** , cliquez avec le bouton droit et choisissez **créer-> texture de rendu**:</span><span class="sxs-lookup"><span data-stu-id="4d4c1-133">In the **Project** pane, right-click and choose **Create -> Render Texture**:</span></span>

![Créer une texture de rendu](images/spatial-audio/create-render-texture.png)

<span data-ttu-id="4d4c1-135">Dans le volet de l' **inspecteur** de la **texture de rendu**, définissez la propriété **Size** pour qu’elle corresponde à la résolution native de la vidéo de 1280 x 720.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-135">On the **Inspector** pane of the **Render Texture**, set the **Size** property to match the video's native resolution of 1280x720.</span></span> <span data-ttu-id="4d4c1-136">Ensuite, pour garantir de bonnes performances de rendu sur HoloLens 2, affectez à la propriété de la **mémoire tampon de profondeur** une **profondeur d’au moins 16 bits**.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-136">Then, to ensure good rendering performance on HoloLens 2, set the **Depth Buffer** property to **At least 16 bits depth**.</span></span> <span data-ttu-id="4d4c1-137">Après ces paramètres, le volet de l' **inspecteur** pour la **texture de rendu** se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-137">After these settings, the **Inspector** pane for the **Render Texture** will look like this:</span></span>

![Propriétés de texture de rendu](images/spatial-audio/render-texture-properties.png)

<span data-ttu-id="4d4c1-139">Ensuite, utilisez votre nouvelle **texture de rendu** comme texture pour le **Quad**:</span><span class="sxs-lookup"><span data-stu-id="4d4c1-139">Next, use your new **Render Texture** as the texture for the **Quad**:</span></span>
1. <span data-ttu-id="4d4c1-140">Faites glisser la **texture rendu** du volet **projet** sur le **quadruple** dans la **hiérarchie** .</span><span class="sxs-lookup"><span data-stu-id="4d4c1-140">Drag the **Render Texture** from the **Project** pane onto the **Quad** in the **Hierarchy**</span></span>
2. <span data-ttu-id="4d4c1-141">Pour garantir de bonnes performances sur HoloLens 2, dans le volet de l' **inspecteur** pour le **Quad**, sélectionnez le **nuanceur standard Mixed Reality Toolkit**.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-141">To ensure good performance on HoloLens 2, on the **Inspector** pane for the **Quad**, select the **Mixed Reality Toolkit Standard Shader**.</span></span>

<span data-ttu-id="4d4c1-142">Avec ces paramètres, le composant de **texture** du volet de l' **inspecteur** pour le **Quad** ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-142">With these settings, the **Texture** component on the **Inspector** pane for the **Quad** will look like this:</span></span>

![Propriétés de texture Quad](images/spatial-audio/quad-texture-properties.png)

<span data-ttu-id="4d4c1-144">Pour définir votre nouveau **lecteur vidéo** et **afficher la texture** pour lire votre clip vidéo, ouvrez le volet de l' **inspecteur** pour le **lecteur vidéo** et :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-144">To set your new **Video Player** and **Render Texture** to play your video clip, open the **Inspector** pane for the **Video Player** and:</span></span>
* <span data-ttu-id="4d4c1-145">Définir la propriété **clip vidéo** sur votre fichier vidéo</span><span class="sxs-lookup"><span data-stu-id="4d4c1-145">Set the **Video Clip** property to your video file</span></span>
* <span data-ttu-id="4d4c1-146">Cochez la case **boucle**</span><span class="sxs-lookup"><span data-stu-id="4d4c1-146">Check the **Loop** checkbox</span></span>
* <span data-ttu-id="4d4c1-147">Définir la **texture cible** sur votre nouvelle texture de rendu</span><span class="sxs-lookup"><span data-stu-id="4d4c1-147">Set **Target Texture** to your new render texture</span></span>

<span data-ttu-id="4d4c1-148">Le volet de l' **inspecteur** pour le **lecteur vidéo** ressemble maintenant à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-148">The **Inspector** pane for the **Video Player** will now look like this:</span></span>

![Propriétés du lecteur vidéo](images/spatial-audio/video-player-properties.png)

## <a name="spatialize-the-audio-from-the-video"></a><span data-ttu-id="4d4c1-150">Spatialiser l’audio à partir de la vidéo</span><span class="sxs-lookup"><span data-stu-id="4d4c1-150">Spatialize the audio from the video</span></span>
<span data-ttu-id="4d4c1-151">Dans le volet de l' **inspecteur** pour le **Quad**, créez une **source audio** dans laquelle vous allez acheminer l’audio à partir de la vidéo :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-151">In the **Inspector** pane for the **Quad**, create an **Audio Source** to which you'll route the audio from the video:</span></span>
* <span data-ttu-id="4d4c1-152">Cliquez sur **Ajouter un composant** en bas du volet.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-152">Click **Add Component** at the bottom of the pane</span></span>
* <span data-ttu-id="4d4c1-153">Ajouter une **source audio**</span><span class="sxs-lookup"><span data-stu-id="4d4c1-153">Add an **Audio Source**</span></span>

<span data-ttu-id="4d4c1-154">Ensuite, sur la **source audio**:</span><span class="sxs-lookup"><span data-stu-id="4d4c1-154">Then, on the **Audio Source**:</span></span>
* <span data-ttu-id="4d4c1-155">Définir la **sortie** dans votre mélangeur</span><span class="sxs-lookup"><span data-stu-id="4d4c1-155">Set **Output** to your mixer</span></span>
* <span data-ttu-id="4d4c1-156">Vérifier la zone **spatiale**</span><span class="sxs-lookup"><span data-stu-id="4d4c1-156">Check the **Spatialize** box</span></span>
* <span data-ttu-id="4d4c1-157">Déplacez le curseur de **lissage spatial** sur 1 (3d)</span><span class="sxs-lookup"><span data-stu-id="4d4c1-157">Move the **Spatial Blend** slider to 1 (3D)</span></span>

<span data-ttu-id="4d4c1-158">Une fois ces modifications effectuées, le composant **source audio** sur le volet de l' **inspecteur** pour le **Quad** ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-158">After these changes, the **Audio Source** component on the **Inspector** pane for the **Quad** will look like this:</span></span>

![Inspecteur de source audio quadruple](images/spatial-audio/quad-audio-source-inspector.png)

<span data-ttu-id="4d4c1-160">Pour configurer le **lecteur vidéo** de façon à acheminer son audio vers la **source audio** sur le **Quad**, ouvrez le volet de l' **inspecteur** pour le **lecteur vidéo** et :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-160">To set the **Video Player** to route its audio to the **Audio Source** on the **Quad**, open the **Inspector** pane for the **Video Player** and:</span></span>
* <span data-ttu-id="4d4c1-161">Définir le **mode de sortie audio** sur « audio source »</span><span class="sxs-lookup"><span data-stu-id="4d4c1-161">Set the **Audio Output Mode** to 'Audio Source'</span></span>
* <span data-ttu-id="4d4c1-162">Définissez la propriété **source audio** sur votre quadruple</span><span class="sxs-lookup"><span data-stu-id="4d4c1-162">Set the **Audio Source** property to your Quad</span></span>

<span data-ttu-id="4d4c1-163">Une fois ces modifications effectuées, le volet de l' **inspecteur** pour le **lecteur vidéo** ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="4d4c1-163">After these changes, the **Inspector** pane for the **Video Player** will look like this:</span></span>

![Source du jeu de lecteurs vidéo](images/spatial-audio/video-player-set-audio-source.png)

## <a name="next-steps"></a><span data-ttu-id="4d4c1-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d4c1-165">Next steps</span></span>
<span data-ttu-id="4d4c1-166">Essayez votre application sur un HoloLens 2 ou dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-166">Try out your app on a HoloLens 2 or in the Unity editor.</span></span> <span data-ttu-id="4d4c1-167">Vous verrez et entendez la vidéo, et l’audio de la vidéo sera spatial.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-167">You'll see and hear the video, and the audio from the video will be spatialized.</span></span>

<span data-ttu-id="4d4c1-168">Passez au [Chapitre 4](unity-spatial-audio-ch4.md) pour utiliser le bouton permettant d’activer et de désactiver les Spatialization au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="4d4c1-168">Continue to [Chapter 4](unity-spatial-audio-ch4.md) to use the button to enable and disable spatialization at run time.</span></span>

