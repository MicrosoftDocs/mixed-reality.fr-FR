---
title: Didacticiels sur les fonctionnalités multi-utilisateur-5. Intégration des ancres spatiales Azure dans un environnement partagé
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: b83c7ac39d522fc2b799591fa02608d5fc5cc930
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437568"
---
# <a name="5-integrating-azure-spatial-anchors-into-a-shared-experience"></a>5. intégration des ancres spatiales Azure dans un environnement partagé

Dans cette leçon, nous apprenons à intégrer les ancres spatiales Azure (ASA) dans notre expérience partagée. ASA permet à plusieurs appareils colocalisés d’avoir une référence commune si leur environnement physique est d’ancrer des expériences virtuelles, de sorte que tous les participants voient les objets dans le même emplacement physique.

Avant de poursuivre cette leçon, nous devrons suivre le module ASA Learning, qui aborde les principes fondamentaux de ASA, la création de comptes et de ressources Azure, ainsi que d’autres blocs de construction fondamentaux nécessaires avant de pouvoir intégrer ASA à notre expérience partagée.

Cherché

- Intégrez ASA dans une expérience partagée pour l’alignement sur plusieurs appareils.
- Découvrez les principes de base du fonctionnement de ASA dans le contexte d’une expérience partagée locale.

### <a name="instructions"></a>Instructions

1. Enregistrez le projet de la leçon précédente (contrôle + S) et nommez-le « HLSharedProjectMainPart5. Unity » afin qu’il soit plus facile à trouver lorsque vous en avez besoin à nouveau.

2. Sélectionnez le Prefab TableAnchor sous l’objet parent MixedRealityPlayspace et supprimez-le.

![Module3Chapter5tep2im](images/module3chapter5step2im.PNG)

3.  Dans la vue projet, accédez à ressources-> Ressources-> Prefabs, puis faites glisser le Prefab TableAnchor sur l’objet SharedPlayground pour en faire un enfant.
4.  Développez l’objet parent MixedRealityPlayspace, l’objet TableAnchor, puis développez également l’objet Buttons. 

![Module3hapter5step5im](images/module3chapter5step5im.PNG)

4. À présent, dans la hiérarchie, sélectionnez ShareAzureAnchorButton et déplacez votre attention sur le panneau de l’informat. Faites défiler vers le bas jusqu’au menu déroulant illustré dans l’image ci-dessous, sélectionnez AnchorModuleScript, puis cliquez sur ShareAnchorNetework ().

![Module3hapter5step6im](images/module3chapter5step6im.PNG)

5. Sélectionnez GetAzureAnchorButton (Voir l’étape 4) et replacez votre attention sur le panneau Inspecteur. Faites défiler vers le bas jusqu’au menu déroulant illustré dans l’image ci-dessous, puis sélectionnez AnchorModuleScript, puis cliquez sur GetSharedAnchorNetwork () et Save.

![Module3hapter5step7im](images/module3chapter5step7im.PNG)

6. Pour tester le module de partage, cliquez sur le bouton « Démarrer une session ASA Azure », qui démarre la session d’ancrages spatiaux Azure, puis crée le point d’ancrage Azure en cliquant sur le bouton « créer un point d’ancrage Azure ». Attendez que le point d’ancrage Azure soit créé. Une fois l’ancre Azure créée, cliquez sur le bouton « partager l’ancre Azure » pour partager l’ancre Azure créée à partir du HoloLens.

7. Pour recevoir le point d’ancrage Azure partagé dans un autre HoloLens, cliquez sur « Démarrer la session ASA Azure » pour démarrer et accéder à la session ASA actuelle.

8. Cliquez sur le bouton « procurez-vous Azure Anchor » pour récupérer l’ancre Azure partagée à partir de l’autre HoloLens.

   > Remarque : tous les détails des actions correspondantes sur les boutons individuels s’affichent dans la fenêtre de débogage.

## <a name="congratulations"></a>Félicitations !

Dans cette leçon, vous avez appris à intégrer les nouvelles ancres spatiales d’Azure pour aligner les appareils colocalisés dans un environnement partagé. Cela conclut également le module de partage. Nous avons appris à configurer un nouveau compte de photons, à intégrer photons et retentissante dans une nouvelle application Unity, à configurer des avatars et des objets partagés, puis à aligner plusieurs participants à l’aide de ASA. 

