---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 80cefb36ec1944ec6f537aafcbf4b63f7f812d26
ms.sourcegitcommit: cf9f8ebbca0301e9d277853771ff6e47701ba1c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67523300"
---
#  <a name="setting-up-photon-unity-networking"></a>Configuration de mise en réseau de Unity Photon

Dans ce didacticiel, nous comment se préparer pour la création d’une expérience partagée par l’importation de la mise en réseau de Unity Photon (a) dans votre projet Unity. Photon est une des options de mise en réseau plusieurs qui permettent aux développeurs de réalité mixte pour créer des expériences partagées. Nous nous allez apprendre à créer un compte de Photon, importer Photon et créer un serveur local facultatif

Objectifs :

* Découvrez comment créer un compte de Photon

* Découvrez comment rechercher et importer Unity de Photon mise en réseau

* Configurer un serveur local de Photon

  

### <a name="setting-up-photon"></a>Configuration de Photon

1. Configurer un [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) compte. Accédez à la page d’inscription Photon en cliquant sur [ce lien](https://dashboard.photonengine.com/en-US/Account/SignUp). Suivez les instructions sur la page d’inscription pour créer le compte. 
   

![Module3Chapter1step1im](images/module3chapter1step1im.PNG)



![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

2. Créer un ID d’application en cliquant sur Créer un bouton de la nouvelle application.

![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

3. Sélectionnez ce jeu de Photon dans le menu déroulant sous Type de Photon. Ensuite, donnez-lui un nom. Dans cet exemple, nous l’avons appelé HoloLensPhotonProject. Une fois que vous avez terminé, cliquez sur le bouton Créer.

![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

4. Une fois cette opération effectuée, revenez à la page de vos applications et vous devriez voir quelque chose de similaire à l’image ci-dessous. Cliquez sur l’ID d’application et copiez-la. Coller est dans un endroit que facilement accessible.  

![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

5. Créez un projet unity et nommez-le HLSharingProject. Pour obtenir des instructions sur la création d’un projet Unity, reportez-vous à [section de « Créer un projet Unity » du Module de Base](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project). 

6. Une fois que le projet se charge, cliquez sur l’onglet ressources Store, comme illustré dans l’image ci-dessous. Ressource puis, dans la zone de recherche en surbrillance dans l’image ci-dessous, tapez dans le jeu de mots, sélectionnez le 2 de ce jeu de Photon - FRE » dans les résultats de recherche. 

![Module3Chapter1step10im](images/module3chapter1step10im.PNG)

7. Télécharger et importer cette ressource en appuyant sur les boutons de téléchargement et importation.

![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

8. Une fois Photon a terminé le processus d’importation, l’Assistant a s’affiche. Prend l’ID d’application (qui doit être dans le Presse-papiers) à partir de l’étape 4 et collez-la dans la zone AppID, appuyez sur le bouton de projet d’installation. 
![module3chapter1step12im](images/module3chapter1step12im.PNG)

9. Après avoir ajouté avec succès l’AppID, accédez à Photon -> PhotonUnityNetworking -> ressources -> PhotonServerSettings d’actifs. Sélectionnez l’option utiliser le nom du serveur et définir la région fixe nous ou service yourPphoton.

   ![module3chapter1step13im](images/module3chapter1step13im.PNG)

## <a name="congratulations"></a>Félicitations

Vous avez correctement créé un compte de Photon configurer un serveur local de Photon et importé ce jeu dans Unity. L’étape suivante consiste à configurer le projet et ensuite autoriser les connexions avec d’autres utilisateurs afin que plusieurs utilisateurs puissent voir votre travail. 

[Didacticiel suivant : Préparation de Unity pour le développement](mrlearning-sharing(photon)-ch2.md)

