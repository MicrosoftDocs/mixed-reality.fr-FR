---
title: Module MR Learning ASA Azure spatiale de point d’ancrage sur HoloLens 2
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 4dc36aec4d885fa75ea490446c2d682264049725
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67326774"
---
# <a name="persistence-and-sharing-of-azure-spatial-anchors"></a>Persistance et le partage des points d’ancrage Spatial Azure

Dans cette leçon, nous allez apprendre à conserver les notre ancres Spatial Azure entre plusieurs sessions d’application en enregistrant nos informations d’ancrage sur le disque de la HoloLens 2. Nous allez également apprendre à partager ces informations d’ancrage à d’autres périphériques pour un alignement d’ancrage sur plusieurs appareils.

## <a name="objectives"></a>Objectifs

* Découvrez comment enregistrer et récupérer les informations d’ancrage Spatial Azure à partir du disque local HoloLens 2, pour la persistance entre les sessions de l’application

* Découvrez comment partager des informations d’ancrage Spatial Azure entre les utilisateurs dans un scénario multi-device

  

## <a name="instructions"></a>Instructions

### <a name="persist-azure-anchors-between-app-sessions---save-anchor-id-to-disk"></a>Conserver les ancres Azure entre les Sessions de l’application - ID d’ancrage sur le disque de sauvegarde

1. Recherchez et ajoutez le préfabriqué « SaveAnchorToDisk » à votre scène. Ceux-ci incluent les deux boutons, un bouton pour l’enregistrement de n’importe quel ID de point d’ancrage Azure disponible sur le disque 2 de HoloLens et l’autre pour la récupération de n’importe quel ID à partir du disque.

   ![module2chapter2step1im](images/module2chapter2step1im.PNG)

2. Configurer chaque bouton en suivant les instructions ci-dessous
   - Pour le bouton « SaveToDisk », créez un nouvel événement sous le déclencheur d’événement « Bouton enfoncé », ainsi que le déclencheur d’événement « Sur Click ». Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode SaveAzureAnchorIDToDisk() à partir du composant de l’objet ParentAnchor ASAmoduleScript.
   
     > Remarque : certains boutons peuvent apparaître qui se chevauchent les autres boutons de la scène. N’hésitez pas à ajuster le positionnement du bouton.
   

  ![module2chapter2step2aim](images/module2chapter2step2aim.PNG)

![module2chapter2step2aim](images/module2chapter2step2bim.PNG)

![module2chapter2step2aim](images/module2chapter2step2cim.PNG)

   - Pour le bouton « GetFromDisk », créez un nouvel événement sous le déclencheur d’événement « Bouton enfoncé », ainsi que le déclencheur d’événement « Sur Click ». Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode LoadAzureAnchorIDsFromDisk() à partir du composant de l’objet ParentAnchor ASAmoduleScript.

3. Suivez les instructions de la leçon 1 pour générer l’application mis à jour sur votre appareil. Après avoir appuyé sur le bouton « Créer le point d’ancrage de Azure », comme vous l’avez fait dans la leçon précédente, vous pouvez maintenant enregistrer l’ID d’ancrage de Azure sur le disque en appuyant sur l’enregistrement au bouton du disque.

4. Redémarrer l’application, démarrer la Session d’Azure, appuyez sur le bouton « ID de point d’ancrage de charge », puis appuyez sur le bouton « Rechercher le point d’ancrage de Azure » pour localiser le point d’ancrage associé au code que nous avons enregistré sur le disque. La scène entière doit maintenant s’aligner dans sa position, à l’emplacement vous avez enregistré le point d’ancrage précédemment !

### <a name="share-azure-anchors-between-multiple-devices"></a>Partager des points d’ancrage Azure entre plusieurs appareils

Dans cette section, nous allez apprendre à partager l’ID d’ancrage de Azure entre plusieurs appareils. Ainsi, plusieurs périphériques interroger Azure pour le même ID d’ancrage, ce qui permet de notre hologrammes ancrés et des scènes SPATIALEMENT aligné. Alignement spatial (voir les mêmes hologrammes dans le même emplacement physique entre plusieurs appareils) est les expériences partagées clés en local dans les 2 HoloLens. Il existe plusieurs façons pour transférer des informations concernant les ID azure entre les appareils, y compris les méthodes décrites dans les expériences partagées ancres Spatial Azure didacticiels (TODO : ajouter un lien.) Cet exemple utilise un service web simple pour charger et télécharger des ID d’ancrage entre les appareils.

1. Ajoutez le préfabriqué « ShareAnchor » dans votre hiérarchie. Cette préfabriqué ajoute deux nouveaux boutons à votre scène ; un pour le chargement des informations sur l’ID d’ancrage et l’autre pour le téléchargement des informations d’ID de l’ancrage. 

   ![module2chapter2step5im](images/module2chapter2step5im.PNG)

2. Configurer chaque bouton en suivant les instructions ci-dessous

   - Pour le bouton « SendSharedAnchor », créez un nouvel événement sous le déclencheur d’événement « Bouton enfoncé », ainsi que le déclencheur d’événement « Sur Click ». Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode ShareAnchor() à partir du composant de l’objet ParentAnchor ASAmoduleScript.

     ![module2chapter2step6aim](images/module2chapter2step6aim.PNG)

     ![module2chapter2step6bim](images/module2chapter2step6bim.PNG)

     

   - Pour le bouton « GetSharedAnchor », créez un nouvel événement sous le déclencheur d’événement « Bouton enfoncé », ainsi que le déclencheur d’événement « Sur Click ». Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode GetSharedAzureAnchor() à partir du composant de l’objet ParentAnchor ASAmoduleScript.

3. Suivez les instructions à partir de [leçon 1](mrlearning-base-ch1.md). pour générer l’application mis à jour sur votre appareil. Après avoir appuyé sur le bouton « Créer le point d’ancrage de Azure », comme vous l’avez fait dans la leçon précédente, vous pouvez désormais partager l’ID d’ancrage de Azure à d’autres appareils en appuyant sur le bouton partager à un autre appareil.

   > Remarque: Sélectionnez le point d’ancrage du parent et faites défiler jusqu'à le script de point d’ancrage du parent. Assurez-vous que votre partage épingler « public » est unique, afin que lorsque vous le partagez, vous savez que vous partagez. Il existe peut-être des milliers d’utilisateurs partage de point d’ancrage de Azure, donc cela vous permettra d’afin de que vous partagez les ancres Azure correct.

4. Si vous avez un autre appareil HoloLens 2, démarrez l’application, puis démarrez la Session Azure. Appuyez sur le bouton « Obtenir l’ID d’ancrage partagés », puis appuyez sur le bouton « Rechercher le point d’ancrage de Azure » pour localiser le point d’ancrage associé au code que nous avons enregistré sur le disque. La scène entière doit maintenant s’aligner dans sa position, à l’emplacement où il a été placé sur un autre appareil de HoloLens 2 ! Si vous avez uniquement un HoloLens 2, vous pourrez toujours tester des fonctionnalités en redémarrant l’application, à partir de la Session d’Azure, puis appuyez sur le bouton « Obtenir l’ID d’ancrage partagés » et puis appuyez sur le bouton « Rechercher le point d’ancrage de Azure » pour localiser le point d’ancrage associé l’ID que nous avons enregistré sur le disque. La scène entière doit maintenant s’aligner dans sa position, à l’emplacement vous avez enregistré le point d’ancrage précédemment !

## <a name="congratulations"></a>Félicitations
Dans cette leçon, vous avez appris comment conserver les ancres Spatial Azure entre les sessions d’application et les redémarrages d’application en enregistrant l’ID d’ancrage spatiale de Azure sur le disque local de 2 HoloLens. Vous avez également appris comment partager des ancres Spatial Azure entre plusieurs appareils pour une expérience de base hologramme multi-utilisateur, statiques partagée !

Nous allez apprendre à implémenter des ancres Spatial Azure en tant que partie d’une expérience partagée locale entièrement interactive au cours de la dernière leçon du Module de partage. Une expérience de partage locale peut inclure des fonctionnalités telles que des identificateurs de position, de rotation et de mise à l’échelle, un objet 3D synchronisé pour chaque utilisateur et partagés des États de l’application. Ancres Spatial Azure améliore ces scénarios partagés en fournissant de chaque participant avec un point d’ancrage commun qui permet à tous les utilisateurs à voir des objets virtuels dans le même emplacement physique. Cela est vrai pour un éventail de plateformes d’appareils, y compris les appareils HoloLens, Android et iOS. Pour savoir comment développer une expérience partagée, veuillez remplir toutes les leçons dans le module de partage.

Dans la leçon suivante, nous allez apprendre à fournir aux utilisateurs avec des commentaires en temps réel. Ces commentaires incluent des informations sur la création d’ancrage, de la qualité de compréhension de l’environnement et de l’état de la session Azure. Sans commentaires, les utilisateurs ne sait pas si un point d’ancrage a été correctement charger vers Azure, si la qualité de l’environnement est suffisante pour la création de point d’ancrage, ou l’état actuel.

[Leçon suivante : ASA leçon 3](mrlearning-asa-ch3.md)

