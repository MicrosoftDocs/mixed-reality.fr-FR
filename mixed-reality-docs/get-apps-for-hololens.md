---
title: Obtenez des applications pour HoloLens
description: Décrit l’installation d’applications pour HoloLens, à la fois via le Microsoft Store et le chargement indépendant.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: chargement de version test, chargement indépendant, chargement indépendant, store, uwp, application, installer
ms.openlocfilehash: 5042c380e3a548e5001e045676190c2349a835a0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593247"
---
# <a name="get-apps-for-hololens"></a>Obtenez des applications pour HoloLens

Un appareil Windows 10, HoloLens prend en charge de nombreuses applications UWP existantes à partir du magasin d’applications, ainsi que les nouvelles applications conçues spécialement pour HoloLens. Sur ces ressources, vous pouvez également [développer](development-overview.md) et installer vos propres applications ou ceux de vos amis !

## <a name="installing-apps"></a>Installation d’applications

Il existe trois façons d’installer de nouvelles applications sur votre HoloLens. La méthode principale sera d’installer de nouvelles applications à partir du Windows Store. Toutefois, vous pouvez également installer vos propres applications via le portail de l’appareil ou en les déployant à partir de Visual Studio.

### <a name="from-the-microsoft-store"></a>À partir du Microsoft Store
1. Effectuer un [bloom](gestures.md#bloom) mouvement pour ouvrir le [Menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu).
2. Sélectionnez l’application de Store, puis sur pour placer cette vignette dans votre monde.
3. Une fois que l’application de Store s’ouvre, utilisez la barre de recherche pour rechercher n’importe quelle application souhaitée.
4. Sélectionnez **obtenir** ou **installer** sur la page d’application (un achat peut être nécessaire).

### <a name="installing-an-application-package-with-the-device-portal"></a>L’installation d’un package d’application avec le portail de l’appareil
1. Établir une connexion à partir de [appareil portail](using-the-windows-device-portal.md) à la cible HoloLens.
2. Accédez à la **applications** page dans le volet de navigation gauche.
3. Sous **Package d’application** accédez au fichier .aspx associé à votre application.
  >[!IMPORTANT]
  >Veillez à référencer les fichiers de dépendance et les certificats associés.

4. Cliquez sur **accédez**.

![Installer le formulaire d’application dans Windows Device Portal sur Microsoft HoloLens](images/deviceportal-appmanager.jpg)<br>
À l’aide de Windows Device Portal pour installer une application sur HoloLens

### <a name="deploying-from-microsoft-visual-studio-2015"></a>Déploiement à partir de Microsoft Visual Studio 2015
1. Ouvrez la solution de Visual Studio de votre application (fichier .sln).
2. Ouvrez le projet **propriétés** .
3. Sélectionnez la configuration de build suivant : Ordinateur maître/x86/distant.
4. Lorsque vous sélectionnez la Machine distante :
   * Assurez-vous que les points d’adresse en adresse de WiFi IP des HoloLens.
   * Définir l’authentification sur universel (protocole non chiffré).
5. Générez votre solution.
6. Cliquez sur le **Machine distante** bouton pour déployer l’application à partir de votre PC de développement pour votre HoloLens. Si vous avez déjà une build existante sur le HoloLens, sélectionnez Oui pour réinstaller cette version plus récente.<br>
  ![Déploiement de Machine à distance pour les applications pour Microsoft HoloLens dans Visual Studio](images/vs2015-remotedeployment.jpg)<br>
7. L’application installera et auto lancement sur votre HoloLens.
