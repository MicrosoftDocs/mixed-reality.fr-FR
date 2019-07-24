---
title: MRC (Mixed Reality Capture)
description: Informations sur l’utilisation de la capture de la réalité mixte.
author: wguyman
ms.author: wguyman
ms.date: 10/02/2018
ms.topic: article
keywords: MRC, capture de la réalité mixte, photos, vidéo, appareil photo, capture, utilisation, flux, diffusion en continu, démo
ms.openlocfilehash: 7af60682f78f624e6b41ded88c8a77e70d40194c
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694484"
---
# <a name="mixed-reality-capture"></a>MRC (Mixed Reality Capture)

HoloLens offre aux utilisateurs l’expérience de combiner le monde réel avec le monde numérique. La capture de réalité mixte (MRC) vous permet de capturer cette expérience en tant que photographie ou vidéo. Cela vous permet de partager l’expérience avec d’autres utilisateurs en leur permettant de voir les hologrammes tels que vous les voyez. Ces vidéos et photos proviennent du point de vue de la première personne. Pour un point de vue tiers, utilisez la [vue spectateur](spectator-view.md).

Les cas d’usage pour la capture de réalité mixte vont au-delà du partage de vidéos dans un cercle social. Les vidéos peuvent être utilisées pour indiquer aux autres utilisateurs comment utiliser une application. Les développeurs peuvent utiliser des vidéos ou toujours pour améliorer les étapes de reproduction et déboguer les expériences d’application.

## <a name="live-streaming-from-hololens"></a>Streaming en direct à partir de HoloLens

La [mise à jour 2018 de Windows 10 octobre](release-notes-october-2018.md) ajoute la prise en charge Miracast à HoloLens. Sélectionnez le bouton **se connecter** au bas du menu Démarrer pour afficher un sélecteur pour les appareils et les adaptateurs compatibles Miracast. Sélectionnez l’appareil sur lequel vous souhaitez commencer la diffusion en continu. Lorsque vous avez terminé,  sélectionnez le bouton déconnecter en bas du menu Démarrer.  **Connexion** et **déconnexion** sont également disponibles dans le menu actions rapides.

Le [portail d’appareils Windows](using-the-windows-device-portal.md) et l' [application auxiliaire Microsoft HoloLens](https://www.microsoft.com/store/productId/9NBLGGH4QWNX) exposent les options de diffusion en continu pour les appareils en mode développeur.

L' [assistance à distance Dynamics 365](https://dynamics.microsoft.com/en-us/mixed-reality/remote-assist) prend en charge la diffusion en continu en direct à partir de HoloLens vers des employés distants.

## <a name="taking-mixed-reality-captures"></a>Captures de la réalité mixte

![Cliquez sur l’icône de l’appareil photo en bas du menu Démarrer.](images/cameraiconinpins-300px.png)<br>
*Cliquez sur l’icône de l’appareil photo en bas du menu Démarrer.*

Il existe plusieurs façons de lancer une capture de réalité mixte:
* Cortana peut être utilisée à tout moment, quelle que soit l’application en cours d’exécution. Disons «Bonjour Cortana, prendre une photo» ou «Hey Cortana, démarrer l’enregistrement». Pour arrêter une vidéo, dites «Hey Cortana, arrêter l’enregistrement».
* Dans le menu Démarrer, sélectionnez **caméra** ou **vidéo**. Utilisez [air-TAP](gestures.md#air-tap) pour ouvrir l’interface utilisateur de la caméra MRC intégrée.
* Dans le menu actions rapides, sélectionnez **caméra** ou **vidéo** pour ouvrir l’interface utilisateur de l’appareil photo MRC intégré.
* Les applications sont en mesure d’exposer leur propre interface utilisateur pour la capture de réalité mixte à l’aide d’un personnalisé ou, à partir de la [mise à jour 2018 d’octobre de Windows 10](release-notes-october-2018.md), l' [interface utilisateur de l’appareil photo MRC intégrée](mixed-reality-capture-for-developers.md).
* Propre à HoloLens: 
    * Le [portail de périphériques Windows](using-the-windows-device-portal.md) dispose d’une page de capture de réalité mixte qui peut être utilisée pour prendre des photos, des vidéos, des flux en direct et afficher des captures.
    * Appuyez simultanément sur les boutons **monter le volume** et **baisser le volume** pour prendre une photo, quelle que soit l’application en cours d’exécution.
    * Maintenez les boutons **monter le volume** et baisser le **volume** pendant trois secondes pour démarrer l’enregistrement d’une vidéo. Pour arrêter une vidéo, appuyez simultanément sur les boutons **monter** le volume et **baisser le volume** .
* Propres aux casques immersifs: 
    * À l’aide d’un contrôleur de mouvement, maintenez le bouton **Windows** enfoncé, puis appuyez sur le **déclencheur** pour prendre une photo. 
    * À l’aide d’un contrôleur de mouvement, maintenez le bouton **Windows** enfoncé, puis appuyez sur le bouton de **menu** pour démarrer l’enregistrement vidéo. Maintenez le bouton **Windows** enfoncé, puis appuyez sur le **déclencheur** pour arrêter l’enregistrement de la vidéo.
    
>[!NOTE]
>La [mise à jour 2018 de Windows 10 octobre](release-notes-october-2018.md) modifie le comportement de la touche et du bouton Windows. Avant la mise à jour, le geste ou le bouton Windows arrête l’enregistrement. Après la mise à jour, le geste ou le bouton Windows ouvre le menu Démarrer (ou le menu actions rapides si vous êtes dans une application). Dans le menu, sélectionnez **arrêter la vidéo** pour arrêter l’enregistrement.

### <a name="limitations-of-mixed-reality-capture"></a>Limitations de la capture de la réalité mixte

Sur HoloLens, le système limite le taux de rendu à 30Hz. Cela permet de libérer de l’espace pour l’exécution de la MRC afin que l’application n’ait pas besoin de conserver une réserve de budget constante et corresponde à la fréquence d’enregistrement de la vidéo MRC (jusqu’à) 30fps.

Les vidéos ont une longueur maximale de cinq minutes.

L’interface utilisateur de l’appareil photo MRC intégrée ne prend en charge qu’une seule opération MRC à la fois (la prise d’une photo s’exclut mutuellement de l’enregistrement d’une vidéo).

### <a name="file-formats"></a>Formats de fichiers

La réalité mixte capture les commandes vocales Cortana et les outils du menu Démarrer pour créer des fichiers aux formats suivants:

|  type  |  Format  |  Extension  |  Résolution :  |  Audio | 
|----------|----------|----------|----------|----------|
|  Photo  |  [GIF](https://en.wikipedia.org/wiki/JPEG)  |  .jpg  |  3904x2196px (HoloLens 2)<br> 1408x792px (HoloLens)<br> 1920x1080px (casques immersifs) |  N/A | 
|  Vidéo  |  [MPEG-4](https://en.wikipedia.org/wiki/MPEG-4)  |  .mp4  |  1920x1080px à 30fps (HoloLens 2)<br> 1216x684px à 24fps (HoloLens)<br> 1632x918px sur 30fps (casques immersifs) |  Stéréo 48 kHz | 

>[!NOTE]
>La résolution des photos et des vidéos peut être plus petite si la caméra photo/vidéo est déjà utilisée par une autre application, pendant la diffusion en continu ou lorsque les ressources système sont insuffisantes.

### <a name="video-stabilization"></a>Stabilisation vidéo

Par défaut:
* La stabilisation vidéo à latence nulle est appliquée lors de la diffusion en continu sur Miracast.
* La stabilisation vidéo à latence longue est appliquée aux vidéos capturées à l’aide de l’interface utilisateur de l’appareil photo MRC, des commandes vocales Cortana et du portail d’appareils Windows.

## <a name="viewing-mixed-reality-captures"></a>Affichage des captures de réalité mixte

La réalité mixte capture des photos et des vidéos sont enregistrées dans le dossier «pellicule» de l’appareil. Vous pouvez y accéder via l' [application photos](see-your-photos.md#photos-app) ou l’Explorateur de fichiers.

Sur un PC connecté à HoloLens, vous pouvez également utiliser le [portail de périphériques Windows](using-the-windows-device-portal.md#mixed-reality-capture) ou l’Explorateur de fichiers de votre PC ([via MTP](release-notes-april-2018.md#new-features-for-hololens)).

Si vous installez l' [application OneDrive](https://www.microsoft.com/p/onedrive/9wzdncrfj1p3), vous pouvez activer le **chargement de l’appareil photo** et vos photos et vidéos MRC seront synchronisées avec onedrive et vos autres appareils à l’aide de onedrive.

>[!NOTE]
>À compter de la mise à jour 2018 de Windows 10 avril, l’application photos ne chargera plus vos photos et vidéos sur OneDrive.

## <a name="see-also"></a>Voir aussi
* [Vue Spectateur](spectator-view.md)
* [Appareil photo localisable](locatable-camera.md)
* [Capture de Réalité Mixte pour les développeurs](mixed-reality-capture-for-developers.md)
* [Voir vos photos](see-your-photos.md)
* [Utilisation du portail d’appareil Windows](using-the-windows-device-portal.md)
