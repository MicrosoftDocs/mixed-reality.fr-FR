---
title: Didacticiels sur les ancres spatiales Azure-2. Enregistrement, récupération et partage d’ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: d03579bf04081f3729baa7d8d76d92586a416184
ms.sourcegitcommit: 83698638b93c5ba77b3ffc399f1706482539f27b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74539712"
---
# <a name="2-saving-retrieving-and-sharing-azure-spatial-anchors"></a>2. enregistrement, récupération et partage d’ancres spatiales Azure

Dans ce didacticiel, vous allez apprendre à enregistrer nos ancres spatiales Azure sur plusieurs sessions d’application en enregistrant les informations d’ancrage dans le stockage de HoloLens 2. Vous allez également apprendre à partager ces informations d’ancrage avec d’autres appareils pour un alignement d’ancrage sur plusieurs appareils.

## <a name="objectives"></a>Objectifs

* Découvrez comment enregistrer et récupérer les informations d’ancre spatiale Azure à partir du disque local HoloLens 2, pour la persistance entre les sessions d’application

* Découvrez comment partager des informations d’ancrage spatial Azure entre les utilisateurs dans un scénario multi-appareil

## <a name="instructions"></a>Instructions

### <a name="persist-azure-anchors-between-app-sessions---save-anchor-id-to-disk"></a>Conserver les ancres Azure entre les sessions d’application-enregistrer l’ID d’ancrage sur le disque

1. Recherchez et ajoutez le Prefab SaveAnchorToDisk à votre scène. Ces deux boutons sont les suivants : un bouton permettant d’enregistrer les ID d’ancrage Azure disponibles dans le stockage HoloLens 2, et un autre pour la récupération des ID du disque.

![module2chapter2step1im](images/module2chapter2step1im.PNG)

2. Configurez chaque bouton en suivant les instructions ci-dessous.

   - Pour le bouton nommé SaveToDisk, créez un événement sous le déclencheur d’événements appuyé sur le bouton, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode SaveAzureAnchorIDToDisk () à partir du composant ASAmoduleScript de l’objet ParentAnchor.
   
     > Remarque : certains boutons peuvent apparaître qui chevauchent les autres boutons de la scène. N’hésitez pas à ajuster le positionnement du bouton.

![module2chapter2step2aim](images/module2chapter2step2aim.PNG)

![module2chapter2step2aim](images/module2chapter2step2bim.PNG)

![module2chapter2step2aim](images/module2chapter2step2cim.PNG)


   - Pour le bouton nommé GetFromDisk, créez un événement sous le déclencheur d’événements appuyé sur le bouton, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode LoadAzureAnchorIDsFromDisk () à partir du composant ASAmoduleScript de l’objet ParentAnchor.

3. Suivez les instructions du didacticiel 1 pour créer l’application mise à jour sur votre appareil. Après avoir appuyé sur le bouton créer une ancre Azure, comme vous l’avez fait dans la leçon précédente, vous pouvez maintenant enregistrer l’ID d’ancrage Azure sur le disque en appuyant sur le bouton enregistrer sur le disque.

4. Redémarrez l’application, démarrez la session Azure, appuyez sur charger l’ID d’ancrage, puis appuyez sur localiser Azure Anchor pour localiser l’ancre associée à l’ID que nous avons enregistré sur le disque. L’ensemble de la scène doit maintenant s’aligner sur la position, à l’emplacement où vous avez précédemment enregistré l’ancre !

### <a name="share-azure-anchors-between-multiple-devices"></a>Partager des ancres Azure entre plusieurs appareils

Dans cette section, nous allons apprendre à partager l’ID d’ancre Azure entre plusieurs appareils. Cela permet à plusieurs appareils d’interroger Azure pour obtenir le même ID d’ancrage, ce qui permet l’alignement spatial de nos hologrammes et scènes ancrés. L’alignement spatial (voir les mêmes hologrammes dans le même emplacement physique entre plusieurs appareils) est essentiel pour les expériences partagées locales dans le HoloLens 2. Il existe de nombreuses façons de transférer des informations concernant les identifiants Azure entre les appareils, notamment les méthodes décrites dans les [didacticiels](mrlearning-sharing(photon)-ch1.md)sur les expériences partagées d’ancrage spatial Azure. Cet exemple utilise un service Web simple pour charger et télécharger des ID d’ancrage entre les appareils.

1. Ajoutez le Prefab ShareAnchor à votre hiérarchie. Ce Prefab ajoute deux nouveaux boutons à votre scène. une pour le chargement des informations d’ID d’ancrage et une autre pour le téléchargement des informations d’ID d’ancrage. 

![module2chapter2step5im](images/module2chapter2step5im.PNG)

2. Configurez chaque bouton en suivant les instructions ci-dessous.

   - Pour le bouton nommé SendSharedAnchor, créez un événement sous le déclencheur d’événements appuyé sur le bouton, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode ShareAnchor () à partir du composant ASAmoduleScript de l’objet ParentAnchor.

![module2chapter2step6aim](images/module2chapter2step6aim.PNG)

![module2chapter2step6bim](images/module2chapter2step6bim.PNG)

   - Pour le bouton nommé GetSharedAnchor, créez un événement sous le déclencheur d’événements appuyé sur le bouton, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode GetSharedAzureAnchor () à partir du composant ASAmoduleScript de l’objet ParentAnchor.

3. Suivez les instructions du [didacticiel 1](mrlearning-base-ch1.md) pour créer l’application mise à jour sur votre appareil. Après avoir appuyé sur le bouton créer une ancre Azure, comme vous l’avez fait dans la leçon précédente, vous pouvez désormais partager l’ID d’ancrage Azure avec d’autres appareils en appuyant sur le bouton partager sur un autre appareil.

   > Remarque : sélectionnez l’ancre parente et faites défiler jusqu’au script d’ancrage parent. Assurez-vous que votre code confidentiel de partage public est unique (vous pouvez le remplacer par un autre nombre). ainsi, lorsque vous le partagez, vous savez que vous partagez. Il peut y avoir des milliers d’utilisateurs qui partagent leurs points d’ancrage Azure, ce qui vous permet de vous assurer que vous partagez les ancres Azure appropriées.
   > 

![module2chapter2step7bim](images/module2chapter2step7bim.PNG)

4. Si vous avez un autre périphérique HoloLens 2, démarrez l’application, puis démarrez la session Azure. Appuyez sur le bouton obtenir l’ID d’ancrage partagé, puis sur le bouton localiser Azure Anchor pour localiser l’ancre associée à l’ID que nous avons partagé à l’aide du service Web. L’intégralité de la scène doit maintenant s’aligner sur la position, à l’emplacement où elle a été placée sur l’autre appareil HoloLens 2 ! Si vous disposez d’un seul HoloLens 2, vous pouvez toujours tester la fonctionnalité en redémarrant l’application, en démarrant la session Azure, puis en appuyant sur le bouton « obtenir un ID d’ancrage partagé », suivi du bouton « localiser le point d’ancrage Azure » pour localiser l’ancre associée à l’ID que nous avons enregistré sur le disque. L’ensemble de la scène doit maintenant s’aligner sur la position, à l’emplacement où vous avez précédemment enregistré l’ancre !

## <a name="congratulations"></a>Félicitations !
Dans cette leçon, vous avez appris à conserver les ancres spatiales Azure entre les sessions d’application et les redémarrages d’application en enregistrant l’ID d’ancrage spatial Azure sur le disque local sur HoloLens 2. Vous avez également appris comment partager des ancres spatiales Azure entre plusieurs appareils pour une expérience de base multi-utilisateur et une expérience partagée d’hologramme statique.

Nous apprenons à implémenter des ancres spatiales Azure dans le cadre d’une expérience partagée locale entièrement interactive au cours de la dernière leçon du module de partage. Une expérience de partage local peut inclure des fonctionnalités telles que la position, la rotation et l’échelle des objets 3D synchronisés, les identificateurs pour chaque utilisateur et les États des applications partagées. Les ancres spatiales Azure améliorent ces scénarios partagés en fournissant à chaque participant un point d’ancrage commun qui permet à tous les utilisateurs de voir les objets virtuels dans le même emplacement physique. Cela s’applique à toute une gamme de plateformes d’appareils, y compris les appareils HoloLens, Android et iOS. Pour apprendre à développer une expérience partagée, effectuez toutes les leçons du module de partage.

Dans la leçon suivante, vous allez apprendre à fournir aux utilisateurs des commentaires en temps réel. Ces commentaires incluent des informations sur la création d’ancres, la qualité de la compréhension de l’environnement et l’état de la session Azure. Sans commentaires, les utilisateurs peuvent ne pas savoir si un point d’ancrage a été chargé avec succès sur Azure, que la qualité de l’environnement soit suffisante pour la création de l’ancre ou pour l’état actuel.

[Leçon suivante : 3. affichage des commentaires sur l’ancrage spatial Azure](mrlearning-asa-ch3.md)

