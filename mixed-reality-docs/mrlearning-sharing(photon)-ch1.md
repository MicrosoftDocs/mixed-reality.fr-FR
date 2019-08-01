---
title: Didacticiels sur les fonctionnalités multi-utilisateur-1. Configuration de la mise en réseau photonique Unity
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: acb6966ace81180e95e6a0fe447d350572f7c0dd
ms.sourcegitcommit: af1602710c1ccb7ed870a491923350d387706129
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68701973"
---
#  <a name="1-setting-up-photon-unity-networking"></a>1. Configuration de la mise en réseau photonique Unity

Dans ce didacticiel, nous allons apprendre à vous préparer à la création d’une expérience partagée en important la mise en réseau de photons Unity (retentissante) dans votre projet Unity. Photons est l’une des nombreuses options de mise en réseau disponibles pour les développeurs de réalité mixte pour créer des expériences partagées. Nous allons apprendre à créer un compte de photons, à importer une photons et à créer un serveur local facultatif

## <a name="objectives"></a>Objectifs

* Découvrez comment créer un compte de photons

* Découvrez comment rechercher et importer une mise en réseau photonique Unity

* Configurer un serveur de photons local

  

## <a name="setting-up-photon"></a>Configuration de photons

1. Configurez un compte de [photons](https://dashboard.photonengine.com/en-US/Account/SignUp) . Accédez à la page d’inscription à photons en cliquant sur [ce lien](https://dashboard.photonengine.com/en-US/Account/SignUp). Suivez les instructions de la page d’inscription pour créer le compte. 
   

![Module3Chapter1step1im](images/module3chapter1step1im.PNG)

![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

2. Créez un ID d’application en cliquant sur le bouton créer une application.

![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

3. Sélectionnez photons retentissante dans le menu déroulant sous type de photons. Donnez-lui un nom. Dans cet exemple, nous avons nommé IT HoloLensPhotonProject. Une fois terminé, cliquez sur le bouton créer.

![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

4. Une fois cette opération effectuée, revenez à la page de votre application et vous devriez voir une image semblable à celle ci-dessous. Cliquez sur l’ID d’application et copiez-le. Collez-la quelque part pour y accéder facilement.  

![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

5. Créez un nouveau projet Unity et nommez-le HLSharingProject. Pour obtenir des instructions sur la création d’un nouveau projet Unity, reportez-vous à [la section «créer un projet Unity» du module de base](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project). 

6. Une fois le projet chargé, cliquez sur l’onglet stockage des ressources, comme indiqué dans l’image ci-dessous. Ensuite, dans la zone de recherche mise en surbrillance dans l’image ci-dessous, tapez retentissante, puis sélectionnez la ressource photon retentissante 2-FREE» dans les résultats de la recherche. 

![Module3Chapter1step10im](images/module3chapter1step10im.PNG)

7. Téléchargez et importez cette ressource en appuyant sur les boutons télécharger et importer.

![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

8. Une fois que photon a terminé le processus d’importation, l’Assistant retentissante s’affiche. Prenez l’ID d’application (qui doit se trouver dans le presse-papiers) de l’étape 4 et collez-le dans la zone AppID, puis appuyez sur le bouton du projet d’installation. 
![module3chapter1step12im](images/module3chapter1step12im.PNG)

9. Après avoir ajouté avec succès l’AppID, accédez à photons-> PhotonUnityNetworking-> Ressources-> PhotonServerSettings dans ressources. Sélectionnez l’option utiliser le serveur de noms, puis définissez la région fixe sur US ou votre région de service de photons.

![module3chapter1step13im](images/module3chapter1step13im.PNG)

## <a name="congratulations"></a>Félicitations

Vous venez de créer un compte de photons, de configurer un serveur de photons local et d’importer des retentissante dans Unity. L’étape suivante consiste à configurer le projet, puis à autoriser les connexions avec d’autres utilisateurs afin que plusieurs utilisateurs puissent voir votre travail. 

[Didacticiel suivant: 2. Préparation de Unity pour le développement](mrlearning-sharing(photon)-ch2.md)

