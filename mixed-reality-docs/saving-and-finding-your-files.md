---
title: L’enregistrement et la recherche de vos fichiers
description: Comment rechercher, enregistrer et partager des fichiers sur HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 09/27/2018
ms.topic: article
keywords: savoir-faire, sélecteur de fichiers, fichiers, photos, vidéos, images, OneDrive, stockage, l’Explorateur de fichiers
ms.openlocfilehash: d539af29fc94fdbde0d2cf08157ae8b5ce8ad0a1
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595663"
---
# <a name="saving-and-finding-your-files"></a>L’enregistrement et la recherche de vos fichiers

Fichiers peuvent être enregistrées et gérées de manière similaire à d’autres Windows 10 Desktop et les appareils mobiles :
* À l’aide de l’application de l’Explorateur de fichiers pour accéder aux dossiers locaux
* Au sein d’un stockage de l’application
* Dans un dossier spécial connu (par exemple, la bibliothèque de musique ou de vidéo)
* À l’aide d’un service de stockage qui inclut un sélecteur d’application et de fichier (par exemple, OneDrive)
* À l’aide d’un PC de bureau connecté à votre HoloLens via une connexion USB, avec prise en charge du protocole MTP (Media Transfer Protocol)

## <a name="file-explorer"></a>Explorateur de fichiers

Vous pouvez utiliser l’application de l’Explorateur de fichiers pour déplacer et supprimer des fichiers à partir de HoloLens.

>[!NOTE]
>Si vous ne voyez pas tous les fichiers dans l’Explorateur de fichiers, le filtre « Récent » peut être actif (icône d’horloge est mise en surbrillance dans le volet gauche). Pour résoudre ce problème, sélectionnez le **ce périphérique** document icône dans le volet de gauche (sous l’icône d’horloge), ou ouvrez le menu et sélectionnez **ce périphérique**.

## <a name="files-within-an-app"></a>Fichiers au sein d’une application

Si une application enregistre les fichiers sur votre appareil, vous pouvez utiliser cette application pour y accéder.

### <a name="where-are-my-photosvideos"></a>Où sont mes photos/vidéos ?

[Capture de la réalité de mixte](mixed-reality-capture.md) photos et vidéos sont enregistrés dans le dossier pellicule de l’appareil. Elles sont accessibles le [application Photos](see-your-photos.md#photos-app). Vous pouvez utiliser l’application de Photos pour synchroniser vos photos et vidéos sur OneDrive. Vous pouvez également accéder à vos photos et vidéos via la page capturer de réalité mixte de le [Windows Device Portal](using-the-windows-device-portal.md#mixed-reality-capture).

### <a name="requesting-files-from-another-app"></a>Demandes de fichiers à partir d’une autre application

Une application peut demander à enregistrer un fichier ou d’ouvrir un fichier à partir d’une autre application via [fichier sélecteurs](app-model.md#file-pickers).

## <a name="known-folders"></a>Dossiers connus

HoloLens prend en charge un nombre de [connu les dossiers](app-model.md#known-folders) que les applications peuvent demander autorisé à y accéder.

## <a name="files-in-a-service"></a>Fichiers dans un service

Pour enregistrer un fichier (ou accéder aux fichiers à partir de) un service, l’application associée au service doit être installé. Pour enregistrer des fichiers et accéder aux fichiers à partir de OneDrive, vous devez installer le [application OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3).

## <a name="mtp-media-transfer-protocol"></a>Protocole MTP (Media Transfer Protocol)

Similaire à d’autres appareils mobiles, connectez-vous HoloLens sur votre PC de bureau et ouvrez l’Explorateur de fichiers sur le PC pour accéder à vos bibliothèques HoloLens (photos, vidéos, documents) pour faciliter le transfert.

## <a name="clarifications"></a>Clarifications

* HoloLens ne prend pas en charge la connexion à des disques durs externes ou des cartes SD.
* En tant que de la [Windows 10 avril 2018 mise à jour (RS4) pour HoloLens](release-notes-april-2018.md), HoloLens inclut un Explorateur de fichiers pour l’enregistrement et la gestion de fichiers sur l’appareil. L’ajout de l’Explorateur de fichiers vous donne également la possibilité de choisir votre sélecteur de fichier (par exemple, l’enregistrement d’un fichier sur votre appareil ou pour OneDrive).
