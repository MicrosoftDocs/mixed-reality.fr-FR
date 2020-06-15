---
title: 6. Empaquetage et déploiement sur un appareil ou un émulateur
description: Sixième tutoriel d’une série de six visant à créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in Mixed Reality Toolkit UX Tools
author: hferrone
ms.author: v-haferr
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: 99c431920c72cf85fed5a0eec6fc72ddf9fb112c
ms.sourcegitcommit: 1b8090ba6aed9ff128e4f32d40c96fac2e6a220b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330232"
---
# <a name="6-packaging--deploying-to-device-or-emulator"></a>6. Empaquetage et déploiement sur un appareil ou un émulateur

## <a name="overview"></a>Vue d’ensemble

Dans le tutoriel précédent, vous avez ajouté un bouton simple qui rétablit la pièce de jeu d’échecs à sa position d’origine. Dans cette section finale, vous allez préparer l’application à être exécutée sur un appareil ou un émulateur HoloLens 2. Si vous disposez d’un appareil HoloLens 2, vous pouvez effectuer un streaming depuis votre ordinateur ou empaqueter l’application pour qu’elle s’exécute directement sur l’appareil. Si vous n’avez pas d’appareil, vous allez empaqueter l’application pour qu’elle s’exécute sur l’émulateur. À la fin de cette section, vous aurez une application de réalité mixte déployée que vous pourrez lire, complète avec des interactions et une interface utilisateur.

## <a name="objectives"></a>Objectifs

* [Appareil uniquement] Streaming sur HoloLens 2 avec communication à distance de l’application holographique
* Empaquetage et déploiement de l’application sur un appareil ou émulateur HoloLens 2

## <a name="device-only-streaming"></a>[Appareil uniquement] Streaming
La [communication à distance holographique](https://docs.microsoft.com/windows/mixed-reality/add-holographic-remoting) dans cet exemple signifie le streaming des données à partir d’un PC ou d’un appareil UWP autonome vers l’appareil HoloLens 2, sans basculer le canal. Son fonctionnement repose sur une application hôte de communication à distance qui reçoit un flux de données d’entrée de la part d’un appareil HoloLens, restitue le contenu dans une vue immersive virtuelle et rediffuse en streaming les images de contenu à l’appareil HoloLens par Wi-Fi. Le streaming vous permet d’ajouter des vues immersives distantes à des logiciels de PC de bureau existants et d’accéder à plus de ressources système. 

Si vous suivez ce chemin avec l’application de jeu d’échecs, vous aurez besoin de quelques éléments :

1.  Installez **Holographic Remoting Player** à partir du Microsoft Store sur votre HoloLens 2 et exécutez l’application.

2.  Accédez à **Edit > Project Settings** et cochez la case **enable remoting** dans **Holographic Remoting**.

3.  Redémarrez l’éditeur, [recherchez l’adresse IP de votre appareil](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens#connect-over-wi-fi), puis entrez-la et cliquez sur **Connect**.

Une fois que vous êtes connecté, cliquez sur la flèche déroulante à droite du bouton **Play** et sélectionnez **VR Preview**. L’application est alors exécutée dans la fenêtre VR Preview, qui est diffusée en streaming vers le casque HoloLens. 

## <a name="packaging-and-deploying-the-app"></a>Empaquetage et déploiement de l’application 

>[!NOTE]
>S’il s’agit de la première fois que vous empaquetez une application Unreal pour HoloLens, vous devrez télécharger les fichiers de prise en charge à partir de l’Epic Launcher. 
>- Accédez à l’onglet **Library** dans Epic Games Launcher, sélectionnez la flèche déroulante à côté de **Launch**, puis cliquez sur **Options**. 
>- Sous **Target Platforms**, sélectionnez **HoloLens 2** et cliquez sur **Apply**. 
>![Paramètres du projet - Description](images/unreal-uxt/6-installationoptions.PNG)

1.  Accédez à **Edit > Project Settings**. 
    * Ajoutez un nom de projet sous **Project > Description > About > Project Name**. 
    * Ajoutez **CN={INSERT COMPANY NAME}** sous **Project > Description > Publisher > Company Distinguished Name**.

> [!IMPORTANT]
> Si vous laissez un de ces champs vide, vous recevrez une erreur. 

![Paramètres du projet - Description](images/unreal-uxt/6-cn.PNG)

2.  Cochez les cases **Build for HoloLens Emulation** et/ou **Build for HoloLens Device** sous **Platforms > HoloLens**.

3.  Cliquez sur **Generate new** dans la section **Packaging** (en regard de **Signing Certificate**), puis revenez à la fenêtre Main.

![Paramètres du projet - Plateformes - HoloLens](images/unreal-uxt/6-packaging.PNG)

4.  Accédez à **File > Package Project** et sélectionnez **HoloLens**. 
    * Créez un dossier où enregistrer votre package, puis cliquez sur **Select Folder**. 

5.  Ouvrez le [Portail d’appareil Windows](https://docs.microsoft.com/windows/mixed-reality/using-the-windows-device-portal) une fois l’application empaquetée, accédez à **Views > Apps** et recherchez la section **Deploy apps**.

6.  Cliquez sur **Browse...** , accédez à votre fichier **ChessApp.appxbundle**, puis cliquez sur **Open**. 

    * Cochez la case **Allow me to select framework packages** si c’est la première fois que vous installez l’application sur votre appareil. 
    * Dans le dialogue suivant, incluez les fichiers **VCLibs** et **appx** appropriés (arm64 pour l’appareil, x64 pour l’émulateur). Vous les trouverez sous **HoloLens** dans le dossier où vous avez enregistré votre package.

7.  Cliquez sur **Install**.
    * Vous pouvez maintenant accéder à **All Apps** et appuyer sur l’application que vous venez d’installer pour l’exécuter, ou vous pouvez démarrer l’application directement à partir du **Portail d’appareil Windows**. 

Félicitations ! Votre application de réalité mixte HoloLens est terminée et prête à l’emploi. En revanche, vous n’avez pas encore tout vu. MRTK comporte un grand nombre de fonctionnalités autonomes que vous pouvez ajouter à vos projets, notamment le mappage spatial, le pointage du regard et l’entrée vocale, voire même les codes QR. Pour plus d’informations sur ces fonctionnalités, consultez la [vue d’ensemble du développement Unreal](https://docs.microsoft.com/windows/mixed-reality/unreal-development-overview).