---
title: Didacticiels de mise en route-6. Exploration des options d’entrée avancées
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: aaa02ce118fd051d94311e837b143affc96ff72b
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77554259"
---
# <a name="6-exploring-advanced-input-options"></a>6. exploration des options d’entrée avancées

Dans ce didacticiel, vous allez explorer quelques options d’entrée avancées pour HoloLens 2, y compris l’utilisation de commandes vocales, le mouvement panoramique et le suivi oculaire.

## <a name="objectives"></a>Objectifs

* Déclencher des événements à l’aide de commandes et de mots clés vocaux
* Utilisez des mains suivies pour faire pivoter des textures et des objets 3D avec des mains suivies
* Tirez parti des fonctionnalités de suivi oculaire HoloLens 2 pour sélectionner des objets

## <a name="enabling-voice-commands"></a>Activation des commandes vocales
<!-- TODO: Consider changing to 'Enabling Speech Commands -->

Dans cette section, vous allez implémenter une commande vocale pour permettre à l’utilisateur de lire un son sur l’objet octa. Pour ce faire, vous allez créer une nouvelle commande vocale, puis configurer l’événement pour qu’il déclenche l’action souhaitée lorsque le mot clé de commande vocale est parlé.

Voici les principales étapes à suivre pour y parvenir :

1. Cloner le profil de système d’entrée par défaut
2. Cloner le profil de commandes vocales par défaut
3. Créer une nouvelle commande vocale
4. Ajouter et configurer le composant Gestionnaire d’entrée vocale (script)
5. Implémenter l’événement Response pour la commande Speech

### <a name="1-clone-the-default-input-system-profile"></a>1. cloner le profil de système d’entrée par défaut

Dans la fenêtre hiérarchie, sélectionnez l’objet **MixedRealityToolkit** , puis dans la fenêtre de l’inspecteur, sélectionnez l’onglet **entrée** , puis clonez le **DefaultHoloLens2InputSystemProfile** pour le remplacer par votre **profil de système d’entrée**personnalisable :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step1-1.png)

> [!TIP]
> Pour obtenir un rappel sur la façon de cloner des profils MRTK, vous pouvez consulter les instructions de [Configuration des profils de la boîte à outils de la réalité mixte](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) .

### <a name="2-clone-the-default-speech-commands-profile"></a>2. cloner le profil de commandes vocales par défaut

Développez la section **Speech** et clonez le **DefaultMixedRealitySpeechCommandsProfile** pour le remplacer par votre propre **profil de commandes vocales**personnalisables :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step2-1.png)

### <a name="3-create-a-new-speech-command"></a>3. créer une nouvelle commande vocale

Dans la section **commandes vocales** , cliquez sur le bouton **+ Ajouter une nouvelle commande vocale** pour ajouter une nouvelle commande vocale au bas de la liste des commandes vocales existantes, puis dans le champ **mot clé** , entrez un mot ou une expression appropriée, par exemple **Lire la musique**:

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step3-1.png)

> [!TIP]
> Si votre ordinateur ne dispose pas d’un microphone et que vous souhaitez tester la commande vocale à l’aide de la simulation dans l’éditeur, vous pouvez affecter un KeyCode à la commande vocale, ce qui vous permet de la déclencher quand vous appuyez sur la touche correspondante.

### <a name="4-add-and-configure-the-speech-input-handler-script-component"></a>4. Ajouter et configurer le composant Gestionnaire d’entrée vocale (script)

Dans la fenêtre hiérarchie, sélectionnez l’objet **octa** et ajoutez le composant **Gestionnaire d’entrée vocale (script)** à l’objet octa. Désactivez ensuite la case à cocher **is Focus required** afin que l’utilisateur n’ait pas besoin d’examiner l’objet octa pour déclencher la commande vocale :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step4-1.png)

### <a name="5-implement-the-response-event-for-the-speech-command"></a>5. implémentez l’événement Response pour la commande Speech

Sur le composant Gestionnaire d’entrée vocale (script), cliquez sur le petit bouton de **+** pour ajouter un élément de mot clé à la liste des mots clés :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-1.png)

Cliquez sur l’élément qui vient d’être créé **0** pour le développer, puis, dans la liste déroulante **mot clé** , choisissez le mot clé **Play Music** que vous avez créé précédemment :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-2.png)

> [!NOTE]
> Les mots clés dans la liste déroulante de mots clés sont renseignés en fonction des mots clés définis dans la liste commandes vocales du profil commandes vocales.

Créez un événement de **réponse ()** , configurez l’objet **octa** pour recevoir l’événement, définissez **audiosource. PlayOneShot** comme action à déclencher et affectez un clip audio approprié au champ **clip** audio, par exemple, le clip audio MRTK_Gem :

![mrlearning-base](images/mrlearning-base/tutorial5-section1-step5-3.png)

> [!TIP]
> Pour obtenir un rappel sur la façon d’implémenter des événements et d’assigner un clip audio, vous pouvez consulter les instructions relatives à l' [implémentation de l’événement at Touch Started](mrlearning-base-ch4.md#4-implement-the-on-touch-started-event) .

## <a name="the-pan-gesture"></a>Le mouvement panoramique

Le mouvement panoramique est utile pour faire défiler le contenu à l’aide de votre doigt ou main. Dans cet exemple, vous allez d’abord apprendre à faire défiler une IU 2D, puis à développer sur cela pour pouvoir faire défiler une collection d’objets 3D.

Voici les principales étapes à suivre pour y parvenir :

1. Créer un objet quadruple qui peut être utilisé pour le panoramique
2. Ajouter le composant touchable (script) near interaction
3. Ajouter le composant de zoom (script) d’interaction manuelle
4. Ajouter du contenu 2D à faire défiler
5. Ajouter du contenu 3D à faire défiler
6. Ajouter le composant déplacer avec le panoramique (script)

> [!NOTE]
> Le composant Move with Pan (script) ne fait pas partie de MRTK. Il a été fourni avec les ressources de ce didacticiel.

### <a name="1-create-a-quad-object-that-can-be-used-for-panning"></a>1. créer un objet quadruple qui peut être utilisé pour le panoramique

Dans la fenêtre hiérarchie, cliquez avec le bouton droit sur une zone vide et sélectionnez **objet 3d** > **quadruple** pour ajouter un quadruple à votre scène. Donnez-lui un nom approprié, par exemple, **PanGesture**, et positionnez-le à un emplacement approprié, par exemple, X = 0, Y =-0,2, Z = 2.

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-1.png)

> [!TIP]
> Pour obtenir un rappel sur la façon d’ajouter des primitives Unity, telles qu’un quadruple 3D, à votre scène, vous pouvez consulter les instructions [Ajouter un cube aux scènes](mrlearning-base-ch2.md#2-add-a-cube-to-the-scene) .

Comme pour toute autre interaction, le geste panoramique requiert également un conflit. Par défaut, un quadruple a un conflit de maille. Toutefois, le conflit de maille n’est pas idéal, car il est extrêmement léger. Pour faciliter l’interaction de l’utilisateur avec le conflit, nous allons remplacer le conflit de maille par un conflit de Box.

Avec l’objet PanGesture toujours sélectionné, cliquez sur l’icône des **paramètres** du composant de **conflit de maillage** et sélectionnez **supprimer le composant** pour supprimer le conflit de maille :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-2.png)

Dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter un **conflit de cases**, puis modifiez la **taille** de la zone de conflit Z à 0,15 pour augmenter l’épaisseur du conflit de boîte :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step1-3.png)

### <a name="2-add-the-near-interaction-touchable-script-component"></a>2. ajouter le composant touchable (script) near interaction

L’objet **PanGesture** étant toujours sélectionné, ajoutez le composant **touchable (script) near-interaction** à l’objet PanGesture, puis cliquez sur les boutons **corriger les limites** et le centre de **Correction** pour mettre à jour les propriétés du centre local et des limites du touchable d’interaction Near (script) pour qu’elles correspondent à la BoxCollider :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step2-1.png)

### <a name="3-add-the-hand-interaction-pan-zoom-script-component"></a>3. Ajoutez le composant zoom (script) d’interaction manuelle

Lorsque l’objet **PanGesture** est toujours sélectionné, ajoutez le composant **Zoom (script) d’interaction manuelle** à l’objet PanGesture, puis activez la case à cocher **Verrouiller horizontal** pour autoriser le défilement vertical uniquement :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step3-1.png)

### <a name="4-add-2d-content-to-be-scrolled"></a>4. ajouter le contenu 2D à faire défiler

Dans le panneau projet, recherchez la documentation **PanContent** , puis cliquez dessus et faites-la glisser vers la propriété élément 0 de la **matière** du convertisseur de maillage de l’objet **PanGesture** :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-1.png)

Dans la fenêtre de l’inspecteur, développez le composant de matériau **PanContent** que vous venez d’ajouter, puis remplacez la valeur Y de la **mosaïque** par 0,5 afin qu’il corresponde à la valeur X et que les vignettes apparaissent carré :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-2.png)

Si vous passez maintenant en mode jeu, vous pouvez tester le contenu 2D à l’aide du mouvement panoramique de la simulation dans l’éditeur :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step4-3.png)

### <a name="5-add-3d-content-to-be-scrolled"></a>5. ajouter du contenu 3D à faire défiler

Dans la fenêtre hiérarchie, **créez quatre cubes** en tant qu’objets enfants de l’objet **PanGesture** et définissez leur **échelle** de transformation sur X = 0,15, Y = 0,15, Z = 0,15 :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step5-1.png)

Pour espacer uniformément les cubes et gagner du temps, ajoutez le composant de **collection d’objets Grid (script)** à l’objet parent des cubes, c’est-à-dire l’objet **PanGesture** , puis configurez la collection d’objets Grid (script) comme suit :

* Remplacez le **nombre de lignes** par 1 pour que tous les cubes soient alignés sur une seule ligne
* Modifier la **largeur de cellule** à 0,25 pour espacer les cubes dans la ligne

Cliquez ensuite sur le bouton **mettre à jour la collection** pour appliquer la nouvelle configuration :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step5-2.png)

### <a name="6-add-the-move-with-pan-script-component"></a>6. ajouter le composant déplacer avec le panoramique (script)

Dans la fenêtre hiérarchie, sélectionnez tous les **objets enfants du cube**, puis dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter le composant **déplacer avec le panoramique (script)** à tous les cubes :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-1.png)

> [!TIP]
> Pour obtenir un rappel sur la sélection de plusieurs objets dans la fenêtre hiérarchie, les conditions d’utilisation peuvent faire référence au [composant Ajouter le gestionnaire de manipulation (script) à toutes les instructions d’objets](mrlearning-base-ch4.md#1-add-the-manipulation-handler-script-component-to-all-the-objects) .

Avec tous les cubes toujours sélectionnés, cliquez sur l’objet **PanGesture** et faites-le glisser vers le champ **source d’entrée de panoramique** :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-2.png)

> [!TIP]
> Le composant Move with Pan (script) sur chaque cube écoute l’événement Pan updated envoyé par le composant HandInteractionPanZoom (script) sur l’objet PanGesture, que vous avez affecté comme source d’entrée Pan à l’étape ci-dessus et met à jour la position de chaque cube en conséquence.

Dans la fenêtre hiérarchie, sélectionnez l’objet **PanGesture** , puis dans l’inspecteur désactivez la case à **cocher** **convertisseur de maillage** pour désactiver le composant de rendu de maille :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-3.png)

Si vous passez maintenant en mode jeu, vous pouvez tester le défilement du contenu 3D à l’aide du mouvement panoramique de la simulation dans l’éditeur :

![mrlearning-base](images/mrlearning-base/tutorial5-section2-step6-4.png)

## <a name="eye-tracking"></a>Eye-tracking

Dans cette section, vous allez découvrir comment activer le suivi visuel dans votre projet. Pour cet exemple, vous allez implémenter une fonctionnalité permettant de faire en sorte que chaque objet de la 3DObjectCollection tourne lentement tout en étant examiné par le point de vue des yeux de l’utilisateur, ainsi que de déclencher un effet de spot lorsque l’objet examiné est sélectionné par un TAP ou une commande vocale.

Voici les principales étapes à suivre pour y parvenir :

1. Ajouter le composant de cible de suivi oculaire (script) à tous les objets cibles
2. Ajouter le composant de démonstration du didacticiel de suivi oculaire (script) à tous les objets cibles
3. Implémenter le tout en examinant l’événement cible
4. Implémenter l’événement sur sélectionné
5. Activer le suivi oculaire simulé pour les simulations dans l’éditeur
6. Activer l’entrée de regard dans les fonctionnalités de l’application du projet Visual Studio

### <a name="1-add-the-eye-tracking-target-script-component-to-all-target-objects"></a>1. ajouter le composant cible de suivi des yeux (script) à tous les objets cibles

Dans la fenêtre hiérarchie, développez l’objet **3DObjectCollection** et sélectionnez tous les **objets enfants**, puis dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter le composant de cible de **suivi oculaire (script)** à tous les objets enfants :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step1-1.png)

Lorsque tous les **objets enfants** sont toujours sélectionnés, configurez le composant **cible de suivi oculaire (script)** comme suit :

* Modifiez **Sélectionner l’action** à **Sélectionner**pour définir l’action d’appui à l’air pour cet objet comme SELECT
* Développez **Voice Select** et définissez la **taille** de la liste de commandes vocale sur 1, puis, dans la nouvelle liste d’éléments qui s’affiche, remplacez l' **élément 0** par **Select**, afin de définir l’action de commande vocale pour cet objet comme SELECT

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step1-2.png)

### <a name="2-add-the-eye-tracking-tutorial-demo-script-component--to-all-target-objects"></a>2. ajouter le composant de démonstration du didacticiel de suivi oculaire (script) à tous les objets cibles

Lorsque tous les **objets enfants** sont toujours sélectionnés, utilisez le bouton **Ajouter un composant** pour ajouter le composant démonstration du **didacticiel de suivi oculaire (script)** à tous les objets enfants :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step2-1.png)

> [!NOTE]
> Le composant cible de suivi oculaire (script) ne fait pas partie de MRTK. Il a été fourni avec les ressources de ce didacticiel.

### <a name="3-implement-the-while-looking-at-target-event"></a>3. implémentez le tout en examinant l’événement cible

Dans la fenêtre hiérarchie, sélectionnez l’objet **fromage** , puis créez un événement **tout en regardant à la cible ()** , configurez l’objet **fromage** pour recevoir l’événement et définissez **EyeTrackingTutorialDemo. RotateTarget** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step3-1.png)

**Répétez cette opération** pour chacun des objets enfants du 3DObjectCollection.

> [!TIP]
> Pour obtenir un rappel sur la façon d’implémenter des événements, vous pouvez consulter les instructions de suivi de la [main et les boutons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) interactifs.

### <a name="4-implement-the-on-selected-event"></a>4. implémentez l’événement sur sélectionné

Dans la fenêtre hiérarchie, sélectionnez l’objet **fromage** , puis créer un événement **sur sélectionné ()** , configurez l’objet **fromage** pour recevoir l’événement et définissez **EyeTrackingTutorialDemo. BlipTarget** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step4-1.png)

**Répétez cette opération** pour chacun des objets enfants du 3DObjectCollection.

### <a name="5-enable-simulated-eye-tracking-for-in-editor-simulations"></a>5. activer le suivi oculaire simulé pour les simulations dans l’éditeur

Dans la fenêtre hiérarchie, sélectionnez l’objet **MixedRealityToolkit** , puis dans la fenêtre de l’inspecteur, sélectionnez l’onglet **entrée** , développez la section **fournisseurs de données d’entrée** , puis la section **service de simulation d’entrée** , puis clonez le **DefaultMixedRealityInputSimulationProfile** pour le remplacer par votre **profil de simulation d’entrée**personnalisable :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-1.png)

> [!TIP]
> Pour obtenir un rappel sur la façon de cloner des profils MRTK, vous pouvez consulter les instructions de [Configuration des profils de la boîte à outils de la réalité mixte](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) .

Dans la section **simulation oculaire** , activez la case à cocher **simuler la position des yeux** pour activer la simulation du suivi oculaire :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-2.png)

Si vous entrez maintenant le mode jeu, vous pouvez tester les effets de spin et de spot que vous avez implémentés en ajustant la vue afin que le curseur atteigne l’un des objets et en utilisant une interaction manuelle ou une commande vocale pour sélectionner l’objet :

![mrlearning-base](images/mrlearning-base/tutorial5-section3-step5-3.png)

> [!NOTE]
> Si vous n’avez pas utilisé DefaultHoloLens2ConfigurationProfile pour cloner votre profil de configuration MRTK personnalisable, comme indiqué dans les instructions [configurer les outils de réalité mixte](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) , le suivi des yeux peut ne pas être activé dans votre projet et doit être activé. Pour cela, vous pouvez vous reporter au [Guide de prise en main du suivi oculaire dans MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html) .

### <a name="6-enable-gaze-input-in-the-visual-studio-projects-app-capabilities"></a>6. activer l’entrée de regard dans les fonctionnalités de l’application du projet Visual Studio

Avant de générer et de déployer votre application à partir de Visual Studio sur votre appareil, le point d’entrée de regard doit être activé dans les fonctionnalités de l’application du projet. Pour ce faire, vous pouvez suivre le [test de votre application Unity sur les instructions HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2) .

## <a name="congratulations"></a>Félicitations

Vous avez ajouté avec succès des fonctionnalités de suivi des yeux de base à votre application. Ces premiers pas vous ouvrent la voie vers tout un monde de possibilités avec l’eye-tracking. Dans ce didacticiel, vous avez également appris les autres fonctionnalités d’entrée avancées, telles que les commandes vocales et les gestes de panoramique.

[Leçon suivante : 7. création d’un exemple d’application de module lunaire](mrlearning-base-ch6.md)
