---
title: 6. Empaquetage et déploiement sur un appareil ou un émulateur
description: Partie 6 d’un tutoriel pour créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools du Mixed Reality Toolkit
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: 35b18e4bb289438f94433827846e94d1014385db
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840378"
---
# <a name="6-packaging--deploying-to-device-or-emulator"></a>6. Empaquetage et déploiement sur un appareil ou un émulateur

Cette section vous guide dans les étapes de préparation de votre application pour qu’elle s’exécute sur un appareil ou un émulateur HoloLens 2. Si vous disposez d’un appareil, vous pouvez effectuer un streaming depuis votre ordinateur vers le périphérique ou empaqueter l’application pour qu’elle s’exécute directement sur l’appareil. Si vous n’avez pas d’appareil, vous devez empaqueter l’application pour qu’elle s’exécute sur l’émulateur. 

## <a name="objectives"></a>Objectifs

* [Appareil uniquement] Streaming de votre application vers HoloLens 2 via l’exécution à distance d’une application holographique
* Empaqueter et déployer votre application sur un appareil ou un émulateur HoloLens 2

## <a name="device-only-stream"></a>[Appareil uniquement] Streaming

1.  Installez le **lecteur distant holographique** à partir du Microsoft Store sur votre HoloLens 2 et exécuter l’application

2.  Accédez à **Edit > Project Settings**. Dans la section Holographic Remoting, cochez la case pour activer la communication à distance, puis redémarrez l’éditeur.

3.  Entrez l’adresse IP de votre appareil, puis cliquez sur Connect.

4.  Une fois que vous êtes connecté, dans votre éditeur UE4, cliquez sur la flèche déroulante à droite du bouton Play et sélectionnez VR Preview.

## <a name="package-and-deploy-your-app"></a>Empaqueter et déployer votre application 

1.  Accédez à **Edit > Project Settings**. Sous **Project > Description > About > Project Name**, donnez un nom à votre projet. Sous **Project > Description > Publisher > Company Distinguished Name**, placez « CN={INSERT COMPANY NAME} ». Si vous laissez un de ces champs vide, vous recevrez une erreur. 

![Paramètres du projet - Description](images/unreal-uxt/6-cn.PNG)

2.  Sous **Platforms > HoloLens**, choisissez Emulation et/ou Device selon ce que vous voulez cibler.

3.  Dans la section **Packaging**, en regard de **Signing Certificate**, cliquez sur le bouton **Generate new** pour générer un nouveau certificat de signature. Revenez dans la fenêtre principale.

![Paramètres du projet - Plateformes - HoloLens](images/unreal-uxt/6-packaging.PNG)

4.  Accédez à **File > Package Project** et sélectionnez **HoloLens**. Créez un dossier où enregistrer votre package, puis cliquez sur **Select Folder**. 

5.  Une fois que l’application a été empaquetée correctement, ouvrez le **Windows Device Portal**, accédez à **Views > Apps** et recherchez la section **Deploy apps**.

6.  Cliquez sur **Browse...** et accédez à votre fichier **ChessApp.appxbundle**. Cliquez sur **Ouvrir**. 

    * Si c’est la première fois que vous installez l’application sur votre appareil, cochez la case en regard de **Allow me to select framework packages**. Dans la boîte de dialogue suivante, incluez le fichier appx VCLibs approprié (arm64 pour l’appareil, x64 pour l’émulateur). 

7.  Cliquez sur **Install**.

Félicitations, vous avez terminé ce tutoriel !  