---
title: Didacticiels audio spatiaux-2. Sons d’interaction du bouton d’aménagement
description: Ajoutez un bouton à votre projet et spatialez les sons d’interaction du bouton.
author: kegodin
ms.author: kegodin
ms.date: 12/01/2019
ms.topic: article
keywords: réalité mixte, Unity, tutorial, hololens2, audio spatial
ms.openlocfilehash: bd70e3bc88ee39b2c6257089ac3a2b93dfae0ad1
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75182776"
---
# <a name="spatializing-button-interaction-sounds"></a>Sons d’interaction du bouton d’aménagement

## <a name="objectives"></a>Objectifs
Dans ce deuxième chapitre du module audio spatial des didacticiels HoloLens 2, vous allez :
* Ajouter un bouton
* Spatialiser le clic sur le bouton

## <a name="add-a-button"></a>Ajouter un bouton
Dans le volet **projet** , sélectionnez **ressources** et tapez « PressableButtonHoloLens2 » dans la barre de recherche :

![Bouton Prefab dans les ressources](images/spatial-audio/button-prefab-in-assets.png)

Le bouton Prefab est l’entrée représentée par une icône bleue, plutôt qu’une icône blanche. Faites glisser le Prefab nommé **PressableButtonHoloLens2** dans le volet **hiérarchie** . Dans le volet de l' **inspecteur** de votre nouveau bouton, définissez la propriété **position** sur (0,-0,4, 2) afin qu’elle s’affiche devant l’utilisateur au démarrage de l’application. Le composant **transformer** du bouton se présente comme suit :

![Transformation de bouton](images/spatial-audio/button-transform.png)

## <a name="spatialize-button-feedback"></a>Commentaires sur le bouton spatial
Dans cette étape, vous allez spatialiser les commentaires audio pour le bouton. Pour obtenir des suggestions de conception associées, consultez [conception de son spatial](spatial-sound-design.md). 

Le volet **mixage audio** vous permet de définir des destinations, appelées **groupes de mixage**, pour la lecture audio à partir de composants **sources audio** . 
* Ouvrez le volet **mixage audio** à partir de la barre de menus à l’aide de la **fenêtre > Audio-> mixage audio**
* Créez un **mélangeur** en cliquant sur le signe « + » en regard de **mixages**. Le nouveau mélangeur inclura un **groupe** par défaut nommé **maître**.

Le volet de **mixage** ressemble à ce qui suit :

![Panneau de mixage avec le premier mélangeur](images/spatial-audio/mixer-panel-with-first-mixer.png)

> [!NOTE]
> Jusqu’à ce que la réverbération soit activée dans le [Chapitre 5](unity-spatial-audio-ch5.md), le compteur de volume du mélangeur n’affiche pas l’activité des sons joués par Microsoft Spatializer

Dans le volet **hiérarchie** , cliquez sur **PressableButtonHoloLens2** . Dans le volet **inspecteur** :
1. Rechercher le composant **source audio**
2. Pour la propriété **sortie** , cliquez sur le sélecteur et choisissez votre mélangeur
3. Cochez la case **spatialiser**
4. Déplacez le curseur de **lissage spatial** vers 3D (1).

> [!NOTE]
> Dans les versions de Unity antérieures à 2019, la case à cocher « spatialiser » se trouve en bas du volet de l' **inspecteur** pour la **source audio**.

Une fois ces modifications effectuées, le composant **source audio** de votre **PressableButtonHoloLens2** se présente comme suit :

![Source audio du bouton](images/spatial-audio/button-audio-source.png)

> [!NOTE]
> Si vous déplacez le **lissage spatial** sur 1 (3d) sans activer la case à cocher **spatialiser** , Unity utilise son Spatializer panoramique, au lieu du **Spatializer Microsoft** avec HRTFs.

## <a name="adjust-the-volume-curve"></a>Ajuster la courbe du volume
Par défaut, Unity atténue les sons spatiaux au fur et à mesure qu’ils s’éloignent de l’écouteur. Lorsque cette atténuation est appliquée à des sons d’interaction, l’interface peut devenir plus difficile à utiliser.

Pour désactiver cette atténuation, ajustez la courbe du **volume** . Dans le composant **source audio** du volet de l' **inspecteur** pour **PressableButtonHoloLens2**, il existe une section intitulée **paramètres audio 3D**. Dans cette section :
1. Définir la propriété **volume Rolloff** sur Linear
2. Faites glisser le point de terminaison sur la courbe de **volume** (la courbe rouge) de « 0 » sur l’axe y jusqu’à « 1 »
3. Pour ajuster la forme de la courbe de **volume** à plat, faites glisser le contrôle de forme de courbe blanche pour qu’il soit parallèle à l’axe X.

Une fois ces modifications effectuées, la section **paramètres audio 3D** des propriétés de la **source audio** de l' **PressableButtonHoloLens2** se présente comme suit :

![Paramètres audio de bouton 3D](images/spatial-audio/button-3d-sound-settings.png)

## <a name="next-steps"></a>Étapes suivantes

Essayez votre application sur un HoloLens 2 ou dans l’éditeur Unity. Dans l’application, vous pouvez toucher le bouton et entendre les sons d’interaction du bouton spatial.

Lors du test dans l’éditeur Unity, appuyez sur la barre d’espace et faites défiler la molette pour activer la simulation manuelle. Pour plus d’informations, consultez la [documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene).

Passez au [chapitre 3](unity-spatial-audio-ch3.md) pour ajouter une vidéo à votre application et spatialer l’audio de la vidéo.

