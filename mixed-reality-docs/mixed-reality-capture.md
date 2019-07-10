---
title: MRC (Mixed Reality Capture)
description: Informations sur l’utilisation de capture de réalité mixte.
author: wguyman
ms.author: wguyman
ms.date: 10/02/2018
ms.topic: article
keywords: option, mixte de capture de la réalité, photos, vidéo, appareil photo, capture, l’utilisation, flux, retransmission en direct, démonstration
ms.openlocfilehash: 7af60682f78f624e6b41ded88c8a77e70d40194c
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694484"
---
# <a name="mixed-reality-capture"></a>MRC (Mixed Reality Capture)

HoloLens offre aux utilisateurs l’expérience de mélange du monde réel avec le monde numérique. Capture de réalité mixte (MRC) vous permettre de capturer cette expérience en tant qu’une photo ou une vidéo. Cela vous permet de partager l’expérience avec d’autres utilisateurs en les autorisant à voir les hologrammes comme vous les voyez. Ces photos et vidéos sont à partir du point de vue de la première personne. Pour le point de vue de la troisième personne, utiliser [vue du spectateur](spectator-view.md).

Cas d’usage pour la capture de réalité mixte aller au-delà de partage de vidéos entre un cercle de réseaux sociaux. Vidéos peuvent être utilisés pour indiquer à d’autres utilisateurs sur l’utilisation d’une application. Les développeurs peuvent utiliser des vidéos ou des images fixes pour améliorer les étapes de reproduction et déboguer des expériences d’application.

## <a name="live-streaming-from-hololens"></a>Vidéo en flux continu à partir de HoloLens

Le [Windows 10 octobre 2018 Update](release-notes-october-2018.md) prend désormais en charge Miracast HoloLens. Sélectionnez le **Connect** bouton en bas du menu Démarrer pour afficher un sélecteur pour les périphériques prenant en charge les Miracast et les cartes. Sélectionnez l’appareil auquel vous voulez commencer la diffusion en continu. Lorsque vous avez terminé, sélectionnez le **déconnexion** bouton en bas du menu Démarrer.  **Se connecter** et **déconnexion** sont également disponibles dans le menu actions rapides.

Le [Windows Device Portal](using-the-windows-device-portal.md) et [application Compagnon de Microsoft HoloLens](https://www.microsoft.com/store/productId/9NBLGGH4QWNX) exposent en direct de diffusion en continu des options pour les appareils qui sont en mode développeur.

[Aider à distance de Dynamics 365](https://dynamics.microsoft.com/en-us/mixed-reality/remote-assist) prend en charge la diffusion en continu à partir de HoloLens aux employés distants.

## <a name="taking-mixed-reality-captures"></a>En prenant la réalité mixte de capture

![Cliquez sur l’icône de l’appareil photo en bas du menu Démarrer](images/cameraiconinpins-300px.png)<br>
*Cliquez sur l’icône de l’appareil photo en bas du menu Démarrer*

Il existe plusieurs façons de lancer une capture de réalité mixte :
* Cortana peut servir à tout moment, quel que soit l’application en cours d’exécution. Simplement par exemple, « Hey Cortana, prendre une photo » ou « Hey Cortana, démarrer l’enregistrement. » Pour arrêter une vidéo, dites « Hey Cortana, arrêter l’enregistrement. »
* Dans le menu Démarrer, sélectionnez **caméra** ou **vidéo**. Utilisez [-appui en l’air](gestures.md#air-tap) pour ouvrir la photo MRC intégré l’interface utilisateur.
* Dans le menu actions rapides, sélectionnez **caméra** ou **vidéo** pour ouvrir la photo MRC intégré l’interface utilisateur.
* Les applications sont en mesure d’exposer leur propre interface utilisateur pour la capture de réalité mixte à l’aide personnalisée, ou à partir de la [Windows 10 octobre 2018 Update](release-notes-october-2018.md), [photo MRC intégré l’interface utilisateur](mixed-reality-capture-for-developers.md).
* Unique pour HoloLens : 
    * [Windows Device Portal](using-the-windows-device-portal.md) comporte une page de capture de réalité mixte qui peut être utilisée pour prendre des photos, des vidéos, des flux en direct et afficher des captures.
    * Appuyez sur les deux le **monter le volume** et **baisser le volume** boutons simultanément pour prendre une photo, quel que soit l’application en cours d’exécution.
    * Maintenez la **monter le volume** et **baisser le volume** boutons pendant trois secondes commencer l’enregistrement d’une vidéo. Pour arrêter une vidéo, appuyez sur **monter le volume** et **baisser le volume** boutons simultanément.
* Casques uniques à immersives : 
    * À l’aide d’un contrôleur de mouvement, maintenez la **Windows** bouton, puis appuyez sur la **déclencheur** pour prendre une photo. 
    * À l’aide d’un contrôleur de mouvement, maintenez la **Windows** bouton, puis appuyez sur la **menu** bouton pour démarrer l’enregistrement vidéo. Maintenez la **Windows** bouton, puis appuyez sur la **déclencheur** pour arrêter l’enregistrement vidéo.
    
>[!NOTE]
>Le [Windows 10 octobre 2018 Update](release-notes-october-2018.md) modifie le comportement bloom et bouton de Windows. Avant la mise à jour, le bouton de Windows ou un mouvement de bloom voulez-vous arrêter l’enregistrement. Après la mise à jour, le mouvement de bloom ou sur le bouton Windows s’ouvre le menu Démarrer (ou le menu actions rapides si vous êtes dans une application). Dans le menu, sélectionnez **Stop vidéo** pour arrêter l’enregistrement.

### <a name="limitations-of-mixed-reality-capture"></a>Limitations de la capture de réalité mixte

Sur HoloLens, le système limite la vitesse de rendu à 30Hz. Cela crée pour cette option exécuter afin de l’application n’a pas besoin de conserver une réserve de budget constante certains accueillir et correspond également à la fréquence d’images vidéo enregistrement MRC de 30 i/s (au maximum).

Vidéos ont une longueur maximale de cinq minutes.

L’appareil photo intégré de MRC l’interface utilisateur prend uniquement en charge une seule opération MRC à la fois (une photo est mutuellement exclusive à partir de l’enregistrement d’une vidéo).

### <a name="file-formats"></a>Formats de fichier

Réalité mixte capture à partir des commandes vocales de Cortana et outils du Menu Démarrer créent des fichiers dans les formats suivants :

|  type  |  Format  |  Extension  |  Résolution  |  Audio | 
|----------|----------|----------|----------|----------|
|  Photo  |  [JPEG](https://en.wikipedia.org/wiki/JPEG)  |  .jpg  |  3904x2196px (HoloLens 2)<br> 1408x792px (HoloLens)<br> 1920 x 1080 px (des casques IMMERSIFS) |  N/A | 
|  Vidéo  |  [MPEG-4](https://en.wikipedia.org/wiki/MPEG-4)  |  .mp4  |  1920 x 1080 px à 30 i/s (HoloLens 2)<br> 1216x684px à 24 images par seconde (HoloLens)<br> 1632x918px à 30 i/s (des casques IMMERSIFS) |  48kHz stéréo | 

>[!NOTE]
>La résolution des photos et vidéos peut être inférieure si la caméra vidéo/photo est déjà en cours d’utilisation par une autre application, lors de la diffusion en continu, ou lorsque les ressources système sont insuffisantes.

### <a name="video-stabilization"></a>Stabilisation vidéo

Par défaut :
* Stabilisation vidéo sans aucune latence est appliquée lors de la diffusion continue sur Miracast.
* Stabilisation vidéo longue latence est appliquée aux vidéos capturées à l’aide de l’appareil photo intégré MRC UI, Cortana commandes vocales et Windows Device Portal.

## <a name="viewing-mixed-reality-captures"></a>Affichage de réalité mixte de capture

Réalité mixte capture de photos et vidéos sont enregistrées au dossier « Pellicule » de l’appareil. Elles sont accessibles le [application Photos](see-your-photos.md#photos-app) ou l’Explorateur de fichiers.

Sur un PC connecté à HoloLens, vous pouvez également utiliser [Windows Device Portal](using-the-windows-device-portal.md#mixed-reality-capture) ou l’Explorateur de fichiers de votre PC ([via MTP](release-notes-april-2018.md#new-features-for-hololens)).

Si vous installez le [application OneDrive](https://www.microsoft.com/p/onedrive/9wzdncrfj1p3), vous pouvez activer **chargement de l’appareil photo,** et vos MRC photos et vidéos seront synchronisés à OneDrive et à vos autres périphériques à l’aide de OneDrive.

>[!NOTE]
>À compter de Windows 10 avril 2018 mise à jour, l’application de Photos n’est plus téléchargerez vos photos et vidéos sur OneDrive.

## <a name="see-also"></a>Voir aussi
* [Vue Spectateur](spectator-view.md)
* [Appareil photo localisable](locatable-camera.md)
* [Capture de Réalité Mixte pour les développeurs](mixed-reality-capture-for-developers.md)
* [Voir vos photos](see-your-photos.md)
* [Utilisation du portail d’appareil Windows](using-the-windows-device-portal.md)
