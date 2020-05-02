---
title: Tutoriels de démarrage - 6. Exploration des options d’entrée avancées
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: ec078015304e1cddc9b042fb5e94cf1904a302cb
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "79376086"
---
# <a name="6-exploring-advanced-input-options"></a>6. Exploration des options d’entrée avancées

Dans ce tutoriel, vous allez examiner quelques options d’entrée avancée pour HoloLens 2, notamment l’utilisation de commandes vocales, le mouvement de panoramique et l’eye-tracking.

## <a name="objectives"></a>Objectifs

* Déclencher des événements en utilisant des commandes vocales et des mots clés
* Utiliser le suivi des mains pour faire un panoramique sur des textures et des objets 3D
* Tirer parti des fonctionnalités d’eye-tracking d’HoloLens 2 pour sélectionner des objets

## <a name="enabling-voice-commands"></a>Activation des commandes vocales
<!-- TODO: Consider changing to 'Enabling Speech Commands -->

Dans cette section, vous allez implémenter une commande vocale pour permettre à l’utilisateur de jouer un son sur l’objet Octa. Pour cela, vous allez créer une commande vocale, puis configurer l’événement pour qu’il déclenche l’action souhaitée quand le mot clé de la commande vocale est prononcé.

Voici les principales étapes à suivre pour y parvenir :

1. Cloner le Input System Profile par défaut
2. Cloner le Speech Commands Profile par défaut
3. Créer une commande vocale
4. Ajouter et configurer le composant Speech Input Handler (Script)
5. Implémenter l’événement Response pour la commande Speech

### <a name="1-clone-the-default-input-system-profile"></a>1. Cloner le Input System Profile par défaut

Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit** puis, dans la fenêtre Inspector, sélectionnez l’onglet **Input** et clonez le **DefaultHoloLens2InputSystemProfile** pour le remplacer par votre propre **Input System Profile** personnalisable :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step1-1.png)

> [!TIP]
> Pour un rappel de la façon de cloner des profils MRTK, vous pouvez consulter les instructions du [Guide pratique pour configurer les profils du Kit de ressources de réalité mixte](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option).

### <a name="2-clone-the-default-speech-commands-profile"></a>2. Cloner le Speech Commands Profile par défaut

Développez la section **Speech** et clonez le profil **DefaultMixedRealitySpeechCommandsProfile** pour le remplacer par votre propre **Speech Commands Profile** personnalisable :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step2-1.png)

### <a name="3-create-a-new-speech-command"></a>3. Créer une commande vocale

Dans la section **Speech Commands**, cliquez sur le bouton **+ Add a New Speech Command** pour ajouter une nouvelle commande vocale au bas de la liste des commandes vocales existantes puis, dans le champ **Keyword**, entrez un mot ou une expression appropriée, par exemple **Play Music** :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step3-1.png)

> [!TIP]
> Si votre ordinateur ne dispose pas d’un microphone et que vous souhaitez tester la commande vocale avec la simulation dans l’éditeur, vous pouvez affecter un KeyCode à la commande vocale, ce qui vous permet de la déclencher quand vous appuyez sur la touche correspondante.

### <a name="4-add-and-configure-the-speech-input-handler-script-component"></a>4. Ajouter et configurer le composant Speech Input Handler (Script)

Dans la fenêtre Hierarchy, sélectionnez l’objet **Octa** et ajoutez le composant **Speech Input Handler (Script)** à l’objet Octa. Décochez ensuite la case **Is Focus Required** pour que l’utilisateur ne soit pas obligé de regarder l’objet Octa pour déclencher la commande vocale :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step4-1.png)

### <a name="5-implement-the-response-event-for-the-speech-command"></a>5. Implémenter l’événement Response pour la commande Speech

Sur le composant Speech Input Handler (Script), cliquez sur le petit bouton **+** pour ajouter un élément de mot clé à la liste des mots clés :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-1.png)

Cliquez sur le **Element 0** que vous venez de créer pour le développer puis, dans la liste déroulante **Keyword**, choisissez le mot clé **Play Music** que vous avez créé précédemment :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-2.png)

> [!NOTE]
> Les mots clés de la liste déroulante Keyword sont renseignés en fonction des mots clés définis dans la liste Speech Commands du profil de commandes vocales.

Créez un événement **Response ()** , configurez l’objet **Octa** pour recevoir l’événement, définissez **AudioSource.PlayOneShot** comme action à déclencher et affectez un clip audio approprié au champ **Audio Clip**, par exemple le clip audio MRTK_Gem :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-3.png)

> [!TIP]
> Pour un rappel de la façon d’implémenter des événements et d’affecter un clip audio, vous pouvez consulter les instructions de [Implémenter un événement On Touch Started](mrlearning-base-ch4.md#4-implement-the-on-touch-started-event).

## <a name="the-pan-gesture"></a>Le mouvement panoramique

Le mouvement panoramique est utile pour le défilement en utilisant votre doigt ou votre main pour faire défiler le contenu. Dans cet exemple, vous allez d’abord découvrir comment faire défiler une IU 2D, puis à développer à partir de là pour pouvoir faire défiler une collection d’objets 3D.

Voici les principales étapes à suivre pour y parvenir :

1. Créer un objet Quad qui peut être utilisé pour le panoramique
2. Ajouter le composant Near Interaction Touchable (Script)
3. Ajouter le composant Hand Interaction Pan Zoom (Script)
4. Ajouter du contenu 2D à faire défiler
5. Ajouter du contenu 3D à faire défiler
6. Ajouter le composant Move With Pan (Script)

> [!NOTE]
> Le composant Move With Pan (script) ne fait pas partie de MRTK. Il a été fourni avec les ressources de ce tutoriel.

### <a name="1-create-a-quad-object-that-can-be-used-for-panning"></a>1. Créer un objet Quad qui peut être utilisé pour le panoramique

Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur une zone vide, puis sélectionnez **3D Object** > **Quad** pour ajouter un quad à votre scène. Donnez-lui un nom approprié, par exemple **PanGesture**, et positionnez-le à un emplacement approprié, par exemple X = 0 ; Y = -0,2 ; Z = 2.

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-1.png)

> [!TIP]
> Pour un rappel de la façon d’ajouter à votre scène des primitives Unity, comme un quad 3D, vous pouvez vous reporter aux instructions de [Ajouter un cube à la scène](mrlearning-base-ch2.md#2-add-a-cube-to-the-scene).

Comme pour toute autre interaction, le mouvement panoramique nécessite également un collider. Par défaut, un quad a un mesh collider. Celui-ci n’est cependant pas idéal, car il est extrêmement fin. Pour faciliter l’interaction de l’utilisateur avec le collider, nous allons remplacer le collider de maillage par un box collider.

Avec l’objet PanGesture sélectionné, cliquez sur l’icône **Settings** du composant **Mesh Collider** et sélectionnez **Remove Component** pour supprimer le mesh collider :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-2.png)

Dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter un **Box Collider**, puis changez la taille (**Size**) de Z en 0,15 pour augmenter l’épaisseur du box collider :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-3.png)

### <a name="2-add-the-near-interaction-touchable-script-component"></a>2. Ajouter le composant Near Interaction Touchable (Script)

Avec l’objet **PanGesture** toujours sélectionné, ajoutez le composant **Near Interaction Touchable (Script)** à l’objet PanGesture, puis cliquez sur les boutons **Fix Bounds** et **Fix Center** pour mettre à jour les propriétés Center et Bounds de Near Interaction Touchable (Script) pour qu’elles correspondent au BoxCollider :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step2-1.png)

### <a name="3-add-the-hand-interaction-pan-zoom-script-component"></a>3. Ajouter le composant Hand Interaction Pan Zoom (Script)

Avec l’objet **PanGesture** sélectionné, ajoutez le composant **Hand Interaction Pan Zoom (Script)** à l’objet PanGesture, puis cochez la case **Lock Horizontal** pour autoriser seulement le défilement vertical :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step3-1.png)

### <a name="4-add-2d-content-to-be-scrolled"></a>4. Ajouter du contenu 2D à faire défiler

Dans le panneau Project, recherchez le matériau **PanContent**, puis cliquez sur celui-ci et faites-le glisser vers la propriété Mesh Renderer **Material** Element 0 de l’objet **PanGesture** :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-1.png)

Dans la fenêtre Inspector, développez le composant de matériau **PanContent** nouvellement ajouté, puis changez sa valeur Y de **Tiling** en 0,5 afin qu’elle corresponde à la valeur X et que les vignettes apparaissent sous forme de carré :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-2.png)

Si vous passez maintenant en mode Game, vous pouvez tester le défilement de contenu 2D avec le mouvement panoramique de la simulation dans l’éditeur :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-3.png)

### <a name="5-add-3d-content-to-be-scrolled"></a>5. Ajouter du contenu 3D à faire défiler

Dans la fenêtre Hierarchy, **créez quatre cubes** en tant qu’objets enfants de l’objet **PanGesture** et définissez la valeur **Scale** de leur transformation sur X = 0,15 ; Y = 0,15 ; Z = 0,15 :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step5-1.png)

Pour espacer uniformément les cubes et gagner du temps, ajoutez le composant **Grid Object Collection (Script)** à l’objet parent des cubes, c’est-à-dire à l’objet **PanGesture**, et configurez Grid Object Collection (Script) comme suit :

* Changez **Num Rows** en 1 pour que tous les cubes soient alignés sur une même ligne
* Changez **Cell Width** en 0,25 pour espacer les cubes dans la ligne

Cliquez ensuite sur le bouton **Update Collection** pour appliquer la nouvelle configuration :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step5-2.png)

### <a name="6-add-the-move-with-pan-script-component"></a>6. Ajouter le composant Move With Pan (Script)

Dans la fenêtre Hierarchy, sélectionnez tous les **objets enfants du cube** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Move With Pan (Script)** à tous les cubes :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-1.png)

> [!TIP]
> Pour un rappel de la façon de sélectionner plusieurs objets dans la fenêtre Hierarchy, vous pouvez vous référer aux instructions de [Ajouter le composant Manipulation Handler (Script) à tous les objets](mrlearning-base-ch4.md#1-add-the-manipulation-handler-script-component-to-all-the-objects).

Avec tous les cubes sélectionnés, cliquez et faites glisser l’objet **PanGesture** vers le champ**Pan Input Source** :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-2.png)

> [!TIP]
> Le composant Move with Pan (Script) sur chaque cube est à l’écoute de l’événement Pan Updated envoyé par le composant HandInteractionPanZoom (Script) sur l’objet PanGesture, que vous avez affecté comme Pan Input Source à l’étape ci-dessus, et il met à jour la position de chaque cube en conséquence.

Dans la fenêtre Hierarchy, sélectionnez l’objet **PanGesture** puis, dans l’inspecteur, **décochez** la case **Mesh Renderer** pour désactiver le composant Mesh Renderer :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-3.png)

Si vous passez maintenant en mode Game, vous pouvez tester le défilement de contenu 3D avec le mouvement panoramique de la simulation dans l’éditeur :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-4.png)

## <a name="eye-tracking"></a>Eye-tracking

Dans cette section, nous allons examiner comment activer l’eye-tracking dans votre projet. Pour cet exemple, vous allez implémenter une fonctionnalité permettant de faire en sorte que chaque objet de la 3DObjectCollection tourne lentement tout en faisant l’objet d’un pointage du regard de l’utilisateur, ainsi que de déclencher un effet de spot quand l’objet regardé est sélectionné par un toucher en l’air ou une commande vocale.

Voici les principales étapes à suivre pour y parvenir :

1. Ajouter le composant Eye Tracking Target (Script) à tous les objets cibles.
2. Ajouter le composant Eye Tracking Tutorial Demo (Script) à tous les objets cibles
3. Implémenter l’événement While Looking At Target
4. Implémenter l’événement On Selected
5. Activer l’eye-tracking simulé pour les simulations dans l’éditeur
6. Activer l’entrée par pointage du regard dans les fonctionnalités de l’application du projet Visual Studio

### <a name="1-add-the-eye-tracking-target-script-component-to-all-target-objects"></a>1. Ajouter le composant Eye Tracking Target (Script) à tous les objets cibles.

Dans la fenêtre Hierarchy, développez l’objet **3DObjectCollection** et sélectionnez tous les **objets enfants** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Eye Tracking Target (Script)** à tous les objets enfants :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step1-1.png)

Avec tous les **objets enfants** sélectionnés, configurez le composant **Eye Tracking Target (Script)** comme suit :

* Changez **Select Action** en **Select** pour définir l’action de toucher en l’air pour cet objet comme étant Select
* Développez **Voice Select** et définissez la taille (**Size**) de la liste des commandes vocales sur 1 puis, dans la nouvelle liste d’éléments qui apparaît, changez **Element 0** en **Select** pour définir l’action de commande vocale pour cet objet comme étant Select

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step1-2.png)

### <a name="2-add-the-eye-tracking-tutorial-demo-script-component--to-all-target-objects"></a>2. Ajouter le composant Eye Tracking Tutorial Demo (Script) à tous les objets cibles

Avec tous les **objets enfants** sélectionnés, utilisez le bouton **Add Component** pour ajouter le composant **Eye Tracking Tutorial Demo (Script)** à tous les objets enfants :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step2-1.png)

> [!NOTE]
> Le composant Eye Tracking Target (Script) ne fait pas partie de MRTK. Il a été fourni avec les ressources de ce tutoriel.

### <a name="3-implement-the-while-looking-at-target-event"></a>3. Implémenter l’événement While Looking At Target

Dans la fenêtre Hierarchy, sélectionnez l’objet **Cheese**, puis créez un événement **While Looking At Target ()** , configurez l’objet **Cheese** pour recevoir l’événement et définissez **EyeTrackingTutorialDemo.RotateTarget** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step3-1.png)

**Répétez** pour chacun des objets enfants dans la 3DObjectCollection.

> [!TIP]
> Pour un rappel de la façon d’implémenter des événements, vous pouvez vous référer aux instructions de [Gestes de suivi de la main et boutons d’interaction](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons).

### <a name="4-implement-the-on-selected-event"></a>4. Implémenter l’événement On Selected

Dans la fenêtre Hierarchy, sélectionnez l’objet **Cheese**, puis créez un événement **On Selected ()** , configurez l’objet **Cheese** pour recevoir l’événement et définissez **EyeTrackingTutorialDemo.BlipTarget** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step4-1.png)

**Répétez** pour chacun des objets enfants dans la 3DObjectCollection.

### <a name="5-enable-simulated-eye-tracking-for-in-editor-simulations"></a>5. Activer l’eye-tracking simulé pour les simulations dans l’éditeur

Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit** puis, dans la fenêtre Inspector, sélectionnez l’onglet **Input**, développez la section **Input Data Providers**, puis la section **Input Simulation Service**, puis clonez le **DefaultMixedRealityInputSimulationProfile** pour le remplacer par votre **Input Simulation Profile** personnalisable :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-1.png)

> [!TIP]
> Pour un rappel de la façon de cloner des profils MRTK, vous pouvez consulter les instructions du [Guide pratique pour configurer les profils du Kit de ressources de réalité mixte](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option).

Dans la section **Eye Simulation**, cochez la case **Simulate Eye Position** pour activer la simulation de l’eye-tracking :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-2.png)

Si vous entrez maintenant dans le mode Game, vous pouvez tester les effets de rotation et de spot que vous avez implémentés en ajustant la vue afin que le curseur atteigne l’un des objets, et en utilisant une interaction manuelle ou une commande vocale pour sélectionner l’objet :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-3.png)

> [!NOTE]
> Si vous n’avez pas utilisé le DefaultHoloLens2ConfigurationProfile pour cloner votre profil de configuration MRTK personnalisable, comme indiqué dans les instructions de [Configurer le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit), l’eye-tracking peut ne pas être activé dans votre projet et vous devrez l’activer. Pour cela, vous pouvez vous reporter aux instructions de [Bien démarrer avec l’eye-tracking dans MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html).

### <a name="6-enable-gaze-input-in-the-visual-studio-projects-app-capabilities"></a>6. Activer l’entrée par pointage du regard dans les fonctionnalités de l’application du projet Visual Studio

Avant de générer et de déployer votre application à partir de Visual Studio sur votre appareil, l’entrée par pointage du regard doit être activée dans les fonctionnalités de l’application du projet. Pour cela, vous pouvez suivre les instructions de [Test de votre application Unity sur HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2).

## <a name="congratulations"></a>Félicitations

Vous avez réussi à ajouter des fonctionnalités d’eye-tracking de base à votre application. Ces premiers pas vous ouvrent la voie vers tout un monde de possibilités avec l’eye-tracking. Dans ce tutoriel, vous avez également découvert d’autres fonctionnalités d’entrée avancées, comme les commandes vocales et les mouvements de panoramique.

[Leçon suivante : 7. Création d’un exemple d’application Module lunaire](mrlearning-base-ch6.md)
