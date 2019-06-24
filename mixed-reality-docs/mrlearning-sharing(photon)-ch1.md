---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 8940de029ef5c67c38f427a238f88fcab527d79d
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67327910"
---
# <a name="setting-up-photon"></a>Configuration de Photon

Dans cette leçon, nous allez apprendre à se préparer pour la création d’une expérience partagée par l’importation de la mise en réseau de Unity Photon (a) dans votre projet Unity. Photon est une des options de mise en réseau plusieurs qui permettent aux développeurs de réalité mixte pour créer des expériences partagées. Nous nous allez apprendre à créer un compte de Photon, importer Photon et créer un serveur local facultatif

Objectifs :

* Apprenez à créer le compte de Photon

* Découvrez comment rechercher et importer Unity de Photon mise en réseau

* Configurer un serveur local de Photon

  

### <a name="setting-up-photon"></a>Configuration de Photon

1. Configurer un [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) compte. Accédez à la page d’inscription Photon en cliquant sur [ce lien](https://dashboard.photonengine.com/en-US/Account/SignUp). Suivez les instructions sur la page d’inscription pour créer le compte. 
   

![Module3Chapter1step1im](images/module3chapter1step1im.PNG)

2. Une fois que vous êtes inscrit, cliquez sur les kits de développement logiciel. Une fois que vous êtes sur cette page, cliquez sur « server » et vous assurer de l’état est « auto-hébergé. » Puis faites défiler vers le bas et cliquez sur « server », comme indiqué dans la deuxième image ci-dessous.

   

   ![Module3Chapter1step2aim](images/module3chapter1step2aim.PNG)

   ![Module3Chapter1step2bim](images/module3chapter1step2bim.PNG)
   
   3. Si vous le faites étiqueté, une zone de texte « lire me. » Continuons et le lire. Une fois que vous avez terminé, cliquez sur le lien en regard de « downloadSDK » afin de le télécharger.


![Module3Chapter1step3im](images/module3chapter1step3im.PNG)

4. Sur le dossier une fois le téléchargement terminé.  Une fois que l’Explorateur de fichiers s’ouvre, révélant le dossier du Kit de développement logiciel, copiez le dossier SDK.
   
   - L’étape suivante consisterait à aller dans le lecteur C: windows et créez un dossier appelé « serveur ».
   
   ![Module3Chapter1step4aim](images/module3chapter1step4aim.PNG)
   
   - Ouvrez le dossier et coller le dossier SDK que vous avez copiée précédemment.
   
   ![Module3Chapter1step4bim](images/module3chapter1step4bim.PNG)
   
5. Une fois cette opération terminée, ouvrez le dossier SDK et accédez à « déployer », puis « bin_Win64 », et double-cliquez sur « contrôle photon ».


![Module3Chapter1step5im](images/module3chapter1step5im.PNG)

> Remarque: Si vous avez des questions sur l’adresse IP ou autres questions similaires, vous trouverez la plupart de vos informations dans la barre d’outils (comme indiqué dans l’image ci-dessous).
>
> ![Module3Chapter1noteim](images/module3chapter1noteim.PNG)

6. Maintenant que le serveur est configuré et lancé, revenez en arrière vers le site Web de Photon et vous assurer que vous êtes toujours connecté (ou vous reconnecter, si vous n’êtes pas). Cliquez sur l’icône de profil (converti (boxed) dans l’angle supérieur droit de l’image ci-dessous) et sélectionnez « vos applications. »
   

![Module3Chapter1step6im](images/module3chapter1step6im.PNG)

7. Créer un ID d’application en cliquant sur le bouton « Créer une nouvelle application ».

   ![Module3Chapter1step7aim](images/module3chapter1step7aim.PNG)

   - Sélectionnez « Photon a » dans le menu déroulant sous « type photon. » Puis donnez-lui un nom, dans cet exemple, nous l’avons appelé « HoloLensPhotonProject ». Une fois que vous avez terminé, cliquez sur le bouton « Créer ».

   ![Module3Chapter1step7bim](images/module3chapter1step7bim.PNG)

8. Une fois cette opération effectuée, revenez à la page de vos applications et vous devriez voir quelque chose de similaire à l’image ci-dessous. Cliquez sur l’ID d’application et copiez-la. Coller est dans un endroit que facilement accessible.  
   

![Module3Chapter1step8im](images/module3chapter1step8im.PNG)

9. Créez un projet unity et nommez-le « HLSharingProject. » Pour obtenir des instructions sur la création d’un projet Unity, reportez-vous à [section de « Créer un projet Unity » du Module de Base](https://docs.microsoft.com/en-us/windows/mixed-reality/mrlearning-base-ch1#create-new-unity-project). 


10. Une fois que le projet se charge, cliquez sur l’onglet « ressources store », comme illustré dans l’image ci-dessous. Puis, dans la zone de recherche en surbrillance dans l’image ci-dessous, tapez « A » et sélectionnez la ressource « Photon gratuit a-2 » dans les résultats de recherche. 

    ![Module3Chapter1step10im](images/module3chapter1step10im.PNG)
    
    11. Télécharger et importer cette ressource en appuyant sur les boutons « Télécharger » et « Importer ».
    
    ![Module3Chapter1step11im](images/module3chapter1step11im.PNG)

## <a name="congratulations"></a>Félicitations

Vous avez correctement créé un compte de Photon configurer un serveur local de Photon et importé ce jeu dans Unity. L’étape suivante consiste à configurer le projet et ensuite autoriser les connexions avec d’autres utilisateurs afin que plusieurs utilisateurs puissent voir votre travail. 

[Leçon suivante : Sharing(Photon) leçon 2](mrlearning-sharing(photon)-ch2.md)

