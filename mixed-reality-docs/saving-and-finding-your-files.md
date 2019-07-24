---
title: Enregistrement et recherche de vos fichiers
description: Comment rechercher, enregistrer et partager des fichiers sur HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 09/27/2018
ms.topic: article
keywords: procédures, sélecteur de fichiers, fichiers, photos, vidéos, images, OneDrive, stockage, Explorateur de fichiers
ms.openlocfilehash: d539af29fc94fdbde0d2cf08157ae8b5ce8ad0a1
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524601"
---
# <a name="saving-and-finding-your-files"></a>Enregistrement et recherche de vos fichiers

Les fichiers peuvent être enregistrés et gérés de la même façon que les autres appareils Windows 10 Desktop et mobile:
* Utilisation de l’application Explorateur de fichiers pour accéder aux dossiers locaux
* Dans le propre stockage d’une application
* Dans un dossier connu spécial (tel que la bibliothèque vidéo ou musique)
* Utilisation d’un service de stockage qui comprend un sélecteur d’application et de fichier (par exemple, OneDrive)
* Utilisation d’un PC de bureau connecté à votre HoloLens via USB via la prise en charge du protocole MTP (Media Transfer Protocol)

## <a name="file-explorer"></a>Explorateur de fichiers

Vous pouvez utiliser l’application Explorateur de fichiers pour déplacer et supprimer des fichiers à partir de HoloLens.

>[!NOTE]
>Si vous ne voyez aucun fichier dans l’Explorateur de fichiers, le filtre «récent» peut être actif (l’icône d’horloge est mise en surbrillance dans le volet gauche). Pour résoudre ce problème, sélectionnez l’icône de document de **ce périphérique** dans le volet gauche (sous l’icône d’horloge) ou ouvrez le menu et sélectionnez **cet appareil**.

## <a name="files-within-an-app"></a>Fichiers dans une application

Si une application enregistre des fichiers sur votre appareil, vous pouvez utiliser cette application pour y accéder.

### <a name="where-are-my-photosvideos"></a>Où se trouvent mes photos/vidéos?

La [réalité mixte capture](mixed-reality-capture.md) des photos et des vidéos sont enregistrées dans le dossier pellicule de l’appareil. Vous pouvez y accéder via l' [application photos](see-your-photos.md#photos-app). Vous pouvez utiliser l’application photos pour synchroniser vos photos et vidéos sur OneDrive. Vous pouvez également accéder à vos photos et vidéos via la page de capture de la réalité mixte du [portail d’appareils Windows](using-the-windows-device-portal.md#mixed-reality-capture).

### <a name="requesting-files-from-another-app"></a>Demande de fichiers à partir d’une autre application

Une application peut demander l’enregistrement d’un fichier ou l’ouverture d’un fichier à partir d’une autre application via des sélecteurs de [fichiers](app-model.md#file-pickers).

## <a name="known-folders"></a>Dossiers connus

HoloLens prend en charge un certain nombre de [dossiers connus](app-model.md#known-folders) auxquels les applications peuvent demander une autorisation d’accès.

## <a name="files-in-a-service"></a>Fichiers dans un service

Pour enregistrer un fichier dans (ou accéder aux fichiers à partir de) un service, l’application associée au service doit être installée. Pour pouvoir enregistrer des fichiers dans et accéder à des fichiers à partir de OneDrive, vous devez installer l' [application onedrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3).

## <a name="mtp-media-transfer-protocol"></a>MTP (Media Transfer Protocol)

À l’instar des autres appareils mobiles, connectez HoloLens à votre ordinateur de bureau et ouvrez l’Explorateur de fichiers sur le PC pour accéder à vos bibliothèques HoloLens (photos, vidéos, documents) en vue de les transférer facilement.

## <a name="clarifications"></a>Éclaircissements

* HoloLens ne prend pas en charge la connexion à des disques durs externes ou à des cartes SD.
* À compter de la [mise à jour 2018 de Windows 10 avril (RS4) pour HoloLens](release-notes-april-2018.md), hololens comprend l’Explorateur de fichiers pour l’enregistrement et la gestion des fichiers sur-appareil. L’ajout de l’Explorateur de fichiers vous donne également la possibilité de choisir votre sélecteur de fichiers (par exemple, l’enregistrement d’un fichier sur votre appareil ou sur OneDrive).
