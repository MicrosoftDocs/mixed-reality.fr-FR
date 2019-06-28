---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 941bdc64ed614d5ce71f58f05585d0dfc86c3bb7
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67415930"
---
# <a name="azure-spatial-anchors-and-shared-experiences"></a>Azure ancres spatiales et les expériences partagées

Dans cette leçon, nous allez apprendre à intégrer Azure Spatial ancres (ASA) dans notre expérience partagée. ASA permet à plusieurs appareils colocalisés avoir une compréhension commune si leur environnement physique pour l’ancrage virtuel connaît tel que tous les participants de voir les objets dans le même emplacement physique.

Avant de poursuivre cette leçon, nous devrons effectuer le Module de formation ASA, qui couvre les notions de base, compte Azure et la création de ressources et autres blocs de bâtiments fondamentaux qui sont nécessaires avant que nous pouvons intégrer ASA dans notre expérience partagée ASA.

Objectifs :

- Intégrer ASA dans une expérience partagée pour l’alignement de multi-device
- Découvrez les principes de base du fonctionne de ASA dans le contexte d’une expérience partagé local

### <a name="instructions"></a>Instructions

1. Enregistrez le projet à partir de la leçon précédente (CTRL + S) et nommez-la « HLSharedProjectMainPart5.unity » afin qu’il soit plus facile à trouver lorsque vous avez besoin à nouveau.

2. Sélectionnez le préfabriqué TableAnchor en dessous de l’objet parent de « MixedRealityPlayspace » et le supprimer.

![Module3Chapter5tep2im](images/module3chapter5step2im.PNG)



3.  Dans la vue du projet, accédez aux ressources > ressources > Prefabs et faites glisser le TableAnchor prefab en haut de l’objet SharedPlayground pour le rendre un enfant.
4.  Développez l’objet parent de « MixedRealityPlayspace », puis l’objet « TableAnchor » et ainsi l’objet « boutons ». 

![Module3hapter5step5im](images/module3chapter5step5im.PNG)

4. Maintenant, dans la hiérarchie, sélectionnez le « ShareAzureAnchorButton » et déplacer votre attention sur le panneau de l’inspecteur. Faites défiler vers le menu déroulant illustré dans l’image ci-dessous et sélectionnez « AnchorModuleScript » et cliquez sur « ShareAnchorNetework() ».

![Module3hapter5step6im](images/module3chapter5step6im.PNG)

5. Comme étape 4, sélectionnez la « GetAzureAnchorButton » et déplacer votre attention à ce panneau. Faites défiler vers le menu déroulant illustré dans l’image ci-dessous et sélectionnez « AnchorModuleScript » et cliquez sur « GetSharedAnchorNetwork() ». Puis enregistrez.

![Module3hapter5step7im](images/module3chapter5step7im.PNG)




## <a name="congratulations"></a>Félicitations

Dans cette leçon, vous avez appris comment intégrer puissantes nouvelles Spatial ancres d’Azure pour aligner les appareils colocalisés dans une expérience partagée ! Cette leçon conclut également le Module de partage. Nous avons appris à configurer un nouveau compte Photon, intégrer Photon et jeu de mots dans une application Unity, configuration avatars et des objets partagés et enfin en alignant plusieurs participants à l’aide de ASA. 

