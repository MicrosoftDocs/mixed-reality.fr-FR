---
title: Didacticiels sur les fonctionnalités multi-utilisateur-5. Intégration des ancres spatiales Azure dans un environnement partagé
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: c1b64b9d32409d61284f21ca216417ece4767d1b
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77553807"
---
# <a name="5-integrating-azure-spatial-anchors-into-a-shared-experience"></a>5. intégration des ancres spatiales Azure dans un environnement partagé

Dans cette leçon, vous allez apprendre à intégrer les ancres spatiales Azure (ASA) à notre expérience partagée. ASA permet à plusieurs appareils colocalisés d’avoir une référence commune si leur environnement physique est d’ancrer des expériences virtuelles, de sorte que tous les participants voient les objets dans le même emplacement physique.

## <a name="objectives"></a>Objectifs

* Intégrez ASA dans une expérience partagée pour l’alignement sur plusieurs appareils.
* Découvrez les principes de base du fonctionnement de ASA dans le contexte d’une expérience partagée locale.

## <a name="instructions"></a>Instructions

1. Sélectionnez le Prefab TableAnchor sous l’objet parent MixedRealityPlayspace et supprimez-le.

    ![Module3Chapter5tep2im](images/module3chapter5step2im.PNG)

2. Dans la vue projet, accédez à ressources-> Ressources-> Prefabs, puis faites glisser le Prefab TableAnchor sur l’objet SharedPlayground pour en faire un enfant.

3. Développez l’objet parent MixedRealityPlayspace, l’objet TableAnchor, puis développez également l’objet Buttons.

    ![Module3hapter5step5im](images/module3chapter5step5im.PNG)

4. À présent, dans la hiérarchie, sélectionnez ShareAzureAnchorButton et déplacez votre attention sur le panneau de l’inspecteur. Faites défiler vers le bas jusqu’au menu déroulant illustré dans l’image ci-dessous, sélectionnez AnchorModuleScript, puis cliquez sur ShareAnchorNetwork ().

    ![Module3hapter5step6im](images/module3chapter5step6im.PNG)

5. Sélectionnez GetAzureAnchorButton (Voir l’étape 4) et replacez votre attention sur le panneau Inspecteur. Faites défiler jusqu’au menu déroulant affiché dans l’image ci-dessous, sélectionnez AnchorModuleScript, cliquez sur GetSharedAnchorNetwork (), puis sur Enregistrer.

    ![Module3hapter5step7im](images/module3chapter5step7im.PNG)

6. Répétez l’étape 4 pour raccorder la fonction StartAzureSession () à StartAzureSessionButton.

7. Répétez l’étape 4 pour raccorder la fonction CreateAzureAnchor () à CreateAzureAnchorButton et vérifier que l’objet TableAnchor est assigné au champ paramètre « Game Object » du paramètre de la fonction.

8. Suivez les instructions de [connexion de la scène aux ressources Azure](mrlearning-asa-ch1.md#4-connect-the-scene-to-the-azure-resource) pour ajouter vos informations d’identification de service d’ancrage spatial Azure.

9. Pour tester le module de partage, cliquez sur le bouton « Démarrer une session ASA Azure », qui démarre la session d’ancrages spatiaux Azure, puis crée le point d’ancrage Azure en cliquant sur le bouton « créer un point d’ancrage Azure ». Attendez que le point d’ancrage Azure soit créé. Une fois l’ancre Azure créée, cliquez sur le bouton « partager l’ancre Azure » pour partager l’ancre Azure créée à partir du HoloLens.

10. Pour recevoir le point d’ancrage Azure partagé dans un autre HoloLens, cliquez sur « Démarrer la session ASA Azure » pour démarrer et accéder à la session ASA actuelle.

11. Cliquez sur le bouton « procurez-vous Azure Anchor » pour récupérer l’ancre Azure partagée à partir de l’autre HoloLens.

## <a name="congratulations"></a>Félicitations

Dans cette leçon, vous avez appris à intégrer les nouvelles ancres spatiales d’Azure pour aligner les appareils colocalisés dans un environnement partagé. Cela conclut également le module de partage. Nous avons appris à configurer un nouveau compte de photons, à intégrer photons et retentissante dans une nouvelle application Unity, à configurer des avatars et des objets partagés, puis à aligner plusieurs participants à l’aide de ASA.
