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
# <a name="spatializing-audio-from-a-video"></a>L’aménagement de l’audio à partir d’une vidéo
Dans ce troisième chapitre du module audio spatial des didacticiels HoloLens 2 Unity, vous allez :
* Importer une vidéo et ajouter un lecteur vidéo
* Lire la vidéo sur un Quadrangle
* Acheminer l’audio de la vidéo vers le Quadrangle et spatialiser l’audio

## <a name="import-a-video-and-add-a-video-player"></a>Importer une vidéo et ajouter un lecteur vidéo

Faites glisser un fichier vidéo dans le volet **projet** de votre projet Unity. Vous pouvez utiliser [cette vidéo](https://github.com/microsoft/spatialaudio-unity/blob/develop/Samples/MicrosoftSpatializerSample/Assets/Microsoft%20HoloLens%20-%20Spatial%20Sound-PTPvx7mDon4.mp4?raw=true) à partir de l’exemple de projet de son spatial.

![Dossier des ressources avec une vidéo](images/spatial-audio/assets-folder-with-video.png)

L’ajustement des paramètres de qualité sur le clip vidéo peut garantir une lecture douce sur HoloLens 2. Cliquez sur le fichier vidéo dans le volet **projet** . Ensuite, dans le volet de l' **inspecteur** du fichier vidéo, substituez les paramètres pour les applications du Windows Store et :
* Activer le **transcodage**
* Définir le **codec** sur H264 –
* Définir le **Mode débit** sur faible
* Définir la **qualité spatiale** sur une qualité spatiale moyenne

Après ces ajustements, le volet de l' **inspecteur** du fichier vidéo se présente comme suit :

![Volet de propriétés vidéo](images/spatial-audio/video-property-pane.png)

Ensuite, ajoutez un objet **lecteur vidéo** à la **hiérarchie** en cliquant avec le bouton droit sur le volet **hiérarchie** et en choisissant **vidéo-> lecteur vidéo**:

![Lecteur vidéo dans la hiérarchie](images/spatial-audio/video-player-in-hierarchy.png)

## <a name="play-video-onto-a-quadrangle"></a>Lire une vidéo sur un Quadrangle
L’objet **lecteur vidéo** a besoin d’un objet de jeu texturé sur lequel afficher la vidéo. Tout d’abord, ajoutez un **quadruple** à votre **hiérarchie** en cliquant avec le bouton droit sur le volet **hiérarchie** et en choisissant **objet 3D-> Quad**:

![Ajouter le Quad à la hiérarchie](images/spatial-audio/add-quad-to-hierarchy.png)

Pour vous assurer que le **Quad** s’affiche devant l’utilisateur au démarrage de l’application, définissez la propriété **position** du **quadruple** sur (0, 0, 2) et la propriété **Scale** sur (1,28, 0,72, 1). Une fois ces modifications effectuées, le composant de **transformation** sur le volet de l' **inspecteur** pour le **Quad** ressemble à ce qui suit :

![Quadruple transformation](images/spatial-audio/quad-transform.png)

Pour texturer le **Quad** avec une vidéo, créez une **texture de rendu**. Dans le volet **projet** , cliquez avec le bouton droit et choisissez **créer-> texture de rendu**:

![Créer une texture de rendu](images/spatial-audio/create-render-texture.png)

Dans le volet de l' **inspecteur** de la **texture de rendu**, définissez la propriété **Size** pour qu’elle corresponde à la résolution native de la vidéo de 1280 x 720. Ensuite, pour garantir de bonnes performances de rendu sur HoloLens 2, affectez à la propriété de la **mémoire tampon de profondeur** une **profondeur d’au moins 16 bits**. Après ces paramètres, le volet de l' **inspecteur** pour la **texture de rendu** se présente comme suit :

![Propriétés de texture de rendu](images/spatial-audio/render-texture-properties.png)

Ensuite, utilisez votre nouvelle **texture de rendu** comme texture pour le **Quad**:
1. Faites glisser la **texture rendu** du volet **projet** sur le **quadruple** dans la **hiérarchie** .
2. Pour garantir de bonnes performances sur HoloLens 2, dans le volet de l' **inspecteur** pour le **Quad**, sélectionnez le **nuanceur standard Mixed Reality Toolkit**.

Avec ces paramètres, le composant de **texture** du volet de l' **inspecteur** pour le **Quad** ressemble à ce qui suit :

![Propriétés de texture Quad](images/spatial-audio/quad-texture-properties.png)

Pour définir votre nouveau **lecteur vidéo** et **afficher la texture** pour lire votre clip vidéo, ouvrez le volet de l' **inspecteur** pour le **lecteur vidéo** et :
* Définir la propriété **clip vidéo** sur votre fichier vidéo
* Cochez la case **boucle**
* Définir la **texture cible** sur votre nouvelle texture de rendu

Le volet de l' **inspecteur** pour le **lecteur vidéo** ressemble maintenant à ce qui suit :

![Propriétés du lecteur vidéo](images/spatial-audio/video-player-properties.png)

## <a name="spatialize-the-audio-from-the-video"></a>Spatialiser l’audio à partir de la vidéo
Dans le volet de l' **inspecteur** pour le **Quad**, créez une **source audio** dans laquelle vous allez acheminer l’audio à partir de la vidéo :
* Cliquez sur **Ajouter un composant** en bas du volet.
* Ajouter une **source audio**

Ensuite, sur la **source audio**:
* Définir la **sortie** dans votre mélangeur
* Vérifier la zone **spatiale**
* Déplacez le curseur de **lissage spatial** sur 1 (3d)

Une fois ces modifications effectuées, le composant **source audio** sur le volet de l' **inspecteur** pour le **Quad** ressemble à ce qui suit :

![Inspecteur de source audio quadruple](images/spatial-audio/quad-audio-source-inspector.png)

Pour configurer le **lecteur vidéo** de façon à acheminer son audio vers la **source audio** sur le **Quad**, ouvrez le volet de l' **inspecteur** pour le **lecteur vidéo** et :
* Définir le **mode de sortie audio** sur « audio source »
* Définissez la propriété **source audio** sur votre quadruple

Une fois ces modifications effectuées, le volet de l' **inspecteur** pour le **lecteur vidéo** ressemble à ce qui suit :

![Source du jeu de lecteurs vidéo](images/spatial-audio/video-player-set-audio-source.png)

## <a name="next-steps"></a>Étapes suivantes
Essayez votre application sur un HoloLens 2 ou dans l’éditeur Unity. Vous verrez et entendez la vidéo, et l’audio de la vidéo sera spatial.

Passez au [Chapitre 4](unity-spatial-audio-ch4.md) pour utiliser le bouton permettant d’activer et de désactiver les Spatialization au moment de l’exécution.

