---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 5. Intégration d’Azure Spatial Anchors dans une expérience partagée
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 7fb8cd03b2f3739037dee38786493bfd9012f6ce
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031689"
---
# <a name="5-integrating-azure-spatial-anchors-into-a-shared-experience"></a>5. Intégration d’Azure Spatial Anchors dans une expérience partagée

Dans cette leçon, vous allez apprendre à intégrer Azure Spatial Anchors (ASA) à notre expérience partagée. ASA permet à plusieurs appareils colocalisés d’avoir une référence commune si leur environnement physique a vocation à ancrer des expériences virtuelles, de sorte que tous les participants voient les objets dans le même emplacement physique.

## <a name="objectives"></a>Objectifs

* Intégrez ASA à une expérience partagée pour l’alignement de plusieurs appareils.
* Découvrez les principes de base du fonctionnement d’ASA dans le contexte d’une expérience partagée locale.

## <a name="instructions"></a>Instructions

1. Sélectionnez le préfabriqué TableAnchor sous l’objet parent MixedRealityPlayspace et supprimez-le.

    ![Module3Chapter5tep2im](images/module3chapter5step2im.PNG)

2. Dans la vue Project, accédez à Assets->Resources->Prefabs, puis faites glisser le préfabriqué TableAnchor sur l’objet SharedPlayground pour en faire un objet enfant.

3. Développez l’objet parent MixedRealityPlayspace, l’objet TableAnchor, puis développez également l’objet Buttons.

    ![Module3hapter5step5im](images/module3chapter5step5im.PNG)

4. À présent, dans la hiérarchie, sélectionnez ShareAzureAnchorButton et portez votre attention sur le panneau Inspector. Faites défiler l’écran vers le bas jusqu’au menu déroulant illustré dans l’image ci-dessous, sélectionnez AnchorModuleScript, puis cliquez sur ShareAnchorNetwork().

    ![Module3hapter5step6im](images/module3chapter5step6im.PNG)

5. Sélectionnez GetAzureAnchorButton (consultez l’étape 4) et reportez votre attention sur le panneau Inspector. Faites défiler l’écran vers le bas jusqu’au menu déroulant présenté dans l’image ci-dessous, sélectionnez AnchorModuleScript, cliquez sur GetSharedAnchorNetwork(), puis enregistrez.

    ![Module3hapter5step7im](images/module3chapter5step7im.PNG)

6. Répétez l’étape 4 pour raccorder la fonction StartAzureSession () à StartAzureSessionButton.

7. Répétez l’étape 4 pour raccorder la fonction CreateAzureAnchor () à CreateAzureAnchorButton et vérifiez que l’objet TableAnchor est affecté au champ « Game Object » du paramètre de la fonction.

8. Suivez les instructions données dans [Connecter la scène à la ressource Azure](mrlearning-asa-ch1.md#4-connect-the-scene-to-the-azure-resource) pour ajouter les informations d’identification de votre service Azure Spatial Anchors.

9. Pour tester le module de partage, cliquez sur le bouton « Start Azure ASA Session », qui démarre la session Azure Spatial Anchors, puis créez l’ancre Azure en cliquant sur le bouton « Create Azure Anchor ». Attendez que l’ancre Azure soit créée. Une fois l’ancre Azure créée, cliquez sur le bouton « Share Azure Anchor » pour la partager à partir du HoloLens.

10. Pour recevoir l’ancre Azure partagée dans un autre HoloLens, cliquez sur « Start Azure ASA Session » pour démarrer et accéder à la session ASA en cours.

11. Cliquez sur le bouton « Get Azure Anchor » pour obtenir l’ancre Azure partagée à partir de l’autre HoloLens.

## <a name="congratulations"></a>Félicitations

Dans cette leçon, vous avez appris à intégrer les nouvelles ancres spatiales d’Azure pour aligner des appareils colocalisés dans une expérience partagée. Cette leçon conclut également le module de partage. Nous avons appris à configurer un nouveau compte Photon, à intégrer Photon et PUN dans une nouvelle application Unity, à configurer des avatars et des objets partagés, puis à aligner plusieurs participants à l’aide d’ASA.
