---
title: Obtenir des applications pour HoloLens
description: Décrit l’installation d’applications pour HoloLens, à la fois via le Microsoft Store et le chargement par le côté.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: chargement, charge latérale, chargement secondaire, Store, UWP, application, installer
ms.openlocfilehash: 5042c380e3a548e5001e045676190c2349a835a0
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522566"
---
# <a name="get-apps-for-hololens"></a>Obtenir des applications pour HoloLens

En tant qu’appareil Windows 10, HoloLens prend en charge de nombreuses applications UWP existantes à partir de l’App Store, ainsi que de nouvelles applications conçues spécifiquement pour HoloLens. En plus de ceux-ci, vous souhaiterez peut-être même [développer](development-overview.md) et installer vos propres applications ou celles de vos amis!

## <a name="installing-apps"></a>Installation d’applications

Il existe trois façons d’installer de nouvelles applications sur votre HoloLens. La méthode principale consiste à installer de nouvelles applications à partir du Windows Store. Toutefois, vous pouvez également installer vos propres applications à l’aide du portail des appareils ou en les déployant à partir de Visual Studio.

### <a name="from-the-microsoft-store"></a>À partir de la Microsoft Store
1. Effectuez un mouvement de [floraison](gestures.md#bloom) pour ouvrir le [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu).
2. Sélectionnez l’application du Store, puis appuyez pour placer cette vignette dans votre monde.
3. Une fois l’application du Store ouverte, utilisez la barre de recherche pour rechercher les applications souhaitées.
4. Sélectionnez **obtenir** ou **installer** sur la page de l’application (un achat peut être nécessaire).

### <a name="installing-an-application-package-with-the-device-portal"></a>Installation d’un package d’application avec le portail de l’appareil
1. Établissez une connexion entre le portail de l' [appareil](using-the-windows-device-portal.md) et le HoloLens cible.
2. Accédez à la page **applications** dans le volet de navigation de gauche.
3. Sous **package d’application** , accédez au fichier. AppX associé à votre application.
  >[!IMPORTANT]
  >Veillez à référencer les fichiers de dépendance et de certificat associés.

4. Cliquez sur **OK**.

![Installer le formulaire d’application dans le portail de périphériques Windows sur Microsoft HoloLens](images/deviceportal-appmanager.jpg)<br>
Utilisation du portail d’appareils Windows pour installer une application sur HoloLens

### <a name="deploying-from-microsoft-visual-studio-2015"></a>Déploiement à partir de Microsoft Visual Studio 2015
1. Ouvrez la solution Visual Studio de votre application (fichier. sln).
2. Ouvrez les **Propriétés** du projet.
3. Sélectionnez la configuration de build suivante: Ordinateur maître/x86/distant.
4. Lorsque vous sélectionnez ordinateur distant:
   * Assurez-vous que l’adresse pointe vers l’adresse IP WiFi de l’HoloLens.
   * Définissez authentification sur universel (protocole non chiffré).
5. Générez votre solution.
6. Cliquez sur le bouton **ordinateur distant** pour déployer l’application à partir de votre PC de développement vers votre HoloLens. Si vous avez déjà une build existante sur HoloLens, sélectionnez Oui pour réinstaller cette version plus récente.<br>
  ![Déploiement d’ordinateurs distants pour des applications dans Microsoft HoloLens dans Visual Studio](images/vs2015-remotedeployment.jpg)<br>
7. L’application s’installe et se lance automatiquement sur votre HoloLens.
