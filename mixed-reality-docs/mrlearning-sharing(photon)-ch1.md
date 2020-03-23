---
title: Tutoriels sur les fonctionnalités multiutilisateurs - 1. Configuration de Photon Unity Networking
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multiutilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 94068ff706e0e56ca8ec0f23beaed3a34159b777
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031328"
---
# <a name="1-setting-up-photon-unity-networking"></a>1. Configuration de Photon Unity Networking

## <a name="overview"></a>Vue d’ensemble

Dans ce tutoriel, vous allez découvrir comment préparer la création d’une expérience partagée en important Photon Unity Networking (PUN) dans votre projet Unity. Photon est l’une des nombreuses options de mise en réseau accessibles aux développeurs de réalité mixte pour créer des expériences partagées. Vous allez découvrir comment créer un compte Photon, importer Photon et créer un serveur local facultatif.

## <a name="objectives"></a>Objectifs

* Découvrir comment créer un compte Photon
* Découvrir comment trouver et importer Photon Unity Networking
* Configurer un serveur Photon local

## <a name="prerequisites"></a>Prérequis

>[!TIP]
>Si vous n’avez pas encore effectué les [tutoriels de démarrage](mrlearning-base.md) et les [tutoriels sur les ancres spatiales Azure](mrlearning-asa-ch1.md), nous vous conseillons de le faire avant d’aller plus loin.

* PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Capacité de programmation C# de base
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)

>[!IMPORTANT]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X. Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.

## <a name="setting-up-photon"></a>Configuration de Photon

1. Configurez un compte [Photon](https://dashboard.photonengine.com//Account/SignUp). Cliquez sur [ce lien](https://dashboard.photonengine.com//Account/SignUp) pour accéder à la page d’inscription à Photon. Suivez les instructions de la page d’inscription pour créer le compte.

    ![Module3Chapter1step1im](images/module3chapter1step1im.PNG)

    ![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

2. Cliquez sur le bouton Create a New App pour créer un ID d’application.

    ![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

3. Sélectionnez Photon PUN dans le menu déroulant sous Photon Type. Nommez ensuite l’application. Dans cet exemple, nous la nommons HoloLensPhotonProject. Quand vous avez terminé, cliquez sur le bouton Create.

    ![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

4. Revenez à la page des applications. Vous devriez voir quelque chose de semblable à l’image ci-dessous. Cliquez sur l’ID d’application et copiez-le. Collez-le dans un endroit facilement accessible.  

    ![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

5. Créez un projet Unity et nommez-le HLSharingProject. Pour obtenir des instructions sur la création d’un projet Unity, consultez la [section « Créer un projet Unity » du module de base](https://docs.microsoft.com//windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project). 

6. Une fois le projet chargé, cliquez sur l’onglet Assets Store, comme illustré dans l’image ci-dessous. Ensuite, dans la zone de recherche mise en évidence dans l’image ci-dessous, tapez PUN, puis sélectionnez la ressource Photon « PUN 2 - FREE » dans les résultats de la recherche.

    ![Module3Chapter1step10im](images/module3chapter1step10im.PNG)

7. Téléchargez et importez cette ressource en appuyant sur les boutons Download et Import.

    ![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

8. Une fois que Photon a terminé le processus d’importation, l’Assistant PUN apparaît. Collez l’ID d’application (que vous avez copié dans votre Presse-papiers à l’étape 4) dans la zone AppID, puis appuyez sur le bouton Setup Project.

    ![module3chapter1step12im](images/module3chapter1step12im.PNG)

9. Une fois l’AppID ajouté, accédez à Photon > PhotonUnityNetworking > Resources > PhotonServerSettings dans Assets. Sélectionnez l’option Use Name Server, puis sélectionnez US ou la région de votre service Photon en regard de Fixed Region.

    ![module3chapter1step13im](images/module3chapter1step13im.PNG)

## <a name="congratulations"></a>Félicitations

Vous venez de créer un compte Photon, de configurer un serveur Photon local et d’importer PUN dans Unity. Vous allez à présent configurer le projet et autoriser les connexions avec d’autres utilisateurs pour qu’ils puissent voir votre travail.

[Tutoriel suivant : 2. Préparation de Unity pour le développement](mrlearning-sharing(photon)-ch2.md)
