---
title: Tutoriels de démarrage - 7. Création d’un exemple d’application Module lunaire
description: Dans cette leçon, vous allez combiner plusieurs concepts tirés des leçons précédentes pour créer un exemple d’expérience unique.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 7b432c5ba0ebee5199f5abb1c26715185fc0d70d
ms.sourcegitcommit: 9df82dba06a91a8d2cedbe38a4328f8b86bb2146
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2020
ms.locfileid: "79031566"
---
# <a name="7-creating-a-lunar-module-sample-application"></a>7. Création d’un exemple d’application Module lunaire
<!-- TODO: Rename to 'Creating a Rocket Launcher sample application' -->

Dans ce tutoriel, plusieurs concepts issus des leçons précédentes sont combinés pour créer un exemple d’expérience unique. Vous allez apprendre à créer une application d’assemblage de composants dans laquelle un utilisateur doit utiliser ses mains, dont les mouvements sont captés, pour saisir des composants et tenter d’assembler un module lunaire. Vous utiliserez des boutons enfonçables pour activer/désactiver des indicateurs d’emplacement, réinitialiser l’expérience et lancer le module lunaire dans l’espace.

Vous continuerez à développer cette expérience dans les tutoriels à venir, notamment avec des cas d’usage multiutilisateurs complexes qui tirent parti d’Azure Spatial Anchors pour l’alignement spatial.

## <a name="objectives"></a>Objectifs

* Combiner plusieurs concepts issus des leçons précédentes pour créer une même expérience
* Découvrir comment activer/désactiver des objets
* Déclencher des événements complexes en utilisant des boutons enfonçables
* Utiliser la physique et les forces des corps rigides
* Explorer l’utilisation d’info-bulles

## <a name="lunar-module-parts-overview"></a>Vue d’ensemble des composants du module lunaire
<!-- TODO: Rename to 'Implementing the part assembly functionality' -->

Dans cette section, vous allez créer une tâche simple d’assemblage où l’objectif de l’utilisateur est de placer cinq composants répartis sur une table au bon endroit sur le module lunaire.

Voici les principales étapes à suivre pour y parvenir :

1. Ajouter le préfabriqué RocketLauncher à la scène
2. Activer la manipulation d’objets pour tous les composants
3. Ajouter et configurer le composant Part Assembly Demo (Script)

> [!NOTE]
> Le composant Part Assembly Demo (Script) ne fait pas partie du MRTK. Il a été fourni avec les ressources de ce tutoriel.

### <a name="1-add-the-rocket-launcher-prefab-to-the-scene"></a>1. Ajouter le préfabriqué RocketLauncher à la scène

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** > **RocketLauncher**, faites glisser le préfabriqué **RocketLauncher** dans la fenêtre Hierarchy pour l’ajouter à votre scène, puis positionnez-le à un emplacement approprié. Par exemple :

* Sous Transform, définissez Position avec les valeurs X = 1,5, Y =-0,4 et Z = 0 pour le positionner à droite de l’utilisateur à hauteur de taille.
* Sous Transform, définissez Rotation avec les valeurs X = 0, Y = 180 et Z = 0 pour que les principales fonctionnalités de l’expérience soient face à l’utilisateur.

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step1-1.png)

### <a name="2-enable-object-manipulation-for-all-the-parts"></a>2. Activer la manipulation d’objets pour tous les composants

Dans la fenêtre Hierarchy, localisez l’objet RocketLauncher > **LunarModuleParts** et sélectionnez tous les **objets enfants**. Ajoutez les composants **Manipulation Handler (Script)** et **Near Interaction Grabbable (Script)** , puis configurez Manipulation Handler (Script) comme suit :

* Décochez la case **Allow Far Manipulation** pour autoriser uniquement l’interaction proche.
* En regard de **Two Handed Manipulation Type**, sélectionnez **Move Rotate** pour désactiver la mise à l’échelle.

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step1-2.png)

> [!TIP]
> Si vous avez besoin d’un rappel et d’instructions pas à pas sur la façon d’implémenter la manipulation d’objets, consultez [Manipulation des objets 3D](mrlearning-base-ch4.md#manipulating-3d-objects).

### <a name="3-add-and-configure-the-part-assembly-demo-script-component"></a>3. Ajouter et configurer le composant Part Assembly Demo (Script)

Tous les objets enfants de LunarModuleParts étant encore sélectionnés, ajoutez un composant **Audio Source** et configurez-le comme suit :

* Affectez un clip audio approprié au champ **AudioClip**, par exemple, MRKT_Scale_Start.
* Décochez la case **Play On Awake** pour ne pas lire automatiquement le clip audio quand la scène se charge.
* Définissez **Spatial Blend** avec la valeur 1 pour activer l’audio spatial.

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-1.png)

Tous les objets enfants de LunarModuleParts étant encore sélectionnés, ajoutez le composant **Part Assembly Demo (Script)**  :

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-2.png)

Dans la fenêtre Hierarchy, sélectionnez l’objet **RoverEnclosure** et configurez son composant **Part Assembly Demo (Script)** comme suit :

* Affectez au champ **Object To Place** l’objet **lui-même**, dans ce cas RoverEnclosure.
* Affectez au champ **Location To Place** l’objet **PlacementHints** correspondant, dans ce cas RoverEnclosure_PlacementHint.
* Affectez au champ **Tool Tip Object** l’objet **ToolTip** correspondant, dans ce cas RoverEnclosure_ToolTip.
* Affectez au champ **Audio Source** l’objet **lui-même**, dans ce cas RoverEnclosure.

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-3.png)

**Répétez** ces opérations pour chaque objet enfant de LunarModuleParts, comme FuelTank, EnergyCell, DockingPortal et ExternalSensor.

Si vous passez maintenant en mode Game et déplacez un « Object To Place » à proximité de son « Location To Place » correspondant, voilà ce qui se passe :

* L’objet est ancré et apparenté à l’objet LunarModule. Il fait donc partie du module lunaire.
* La source audio sur l’objet lit le clip audio affecté à l’emplacement de l’objet.
* L’objet Tool Tip correspondant est masqué.

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-4.png)

> [!TIP]
> Si vous avez besoin d’un rappel sur la façon d’utiliser la simulation d’entrée dans l’éditeur, consultez le [guide d’utilisation de la simulation d’entrée avec les mains dans l’éditeur pour tester une scène](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="configuring-the-lunar-module"></a>Configuration du module lunaire

Dans cette section, vous allez ajouter des fonctionnalités à l’application RocketLauncher pour que l’utilisateur puisse effectuer les tâches suivantes :

* Interagir avec le module lunaire
* Lancer le module lunaire dans l’espace et émettre un signal sonore quand il est lancé
* Réinitialiser l’application pour faire revenir le module lunaire et tous les composants à leur position d’origine
* Masquer les indicateurs de placement pour rendre le test d’assemblage de composants plus difficile

Voici les principales étapes à suivre pour y parvenir :

1. Activer la manipulation d’objets
2. Activer les propriétés physiques
3. Ajouter un composant Audio Source
4. Ajouter et configurer le composant Launch Lunar Module (Script)
5. Ajouter et configurer le composant Toggle Placement Hints (Script)

> [!NOTE]
> Les composants Launch Lunar Module (Script) et Toggle Placement Hints (Script) ne font pas partie du MRTK. Ils ont été fournis avec les ressources de ce tutoriel.

### <a name="1-enable-object-manipulation"></a>1. Activer la manipulation d’objets

Dans la fenêtre Hierarchy, sélectionnez l’objet RocketLauncher > **LunarModuleParts**, ajoutez les composants **Manipulation Handler (Script)** et **Near Interaction Grabbable (Script)** , puis configurez Manipulation Handler (Script) comme suit :

* Décochez la case **Allow Far Manipulation** pour autoriser uniquement l’interaction proche.
* En regard de **Two Handed Manipulation Type**, sélectionnez Move Rotate pour désactiver la mise à l’échelle.

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step1-1.png)

### <a name="2-enable-physics"></a>2. Activer les propriétés physiques

L’objet RocketLauncher > **LunarModule** étant encore sélectionné, ajoutez un composant **RigidBody**, puis configurez-le comme suit :

* Décochez la case **Use Gravity** pour que le module lunaire ne soit pas affecté par la gravité.
* Cochez la case **Is Kinematic** pour que le module lunaire ne soit pas initialement affecté par les forces physiques.

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step2-1.png)

### <a name="3-add-an-audio-source-component"></a>3. Ajouter un composant Audio Source

L’objet RocketLauncher > **LunarModule** étant encore sélectionné, ajoutez un composant **Audio Source**, puis configurez-le comme suit :

* Définissez **Spatial Blend** avec la valeur 1 pour activer l’audio spatial.

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step3-1.png)

### <a name="4-add-and-configure-the-launch-lunar-module-script-component"></a>4. Ajouter et configurer le composant Launch Lunar Module (Script)

L’objet RocketLauncher > **LunarModule** étant encore sélectionné, ajoutez le composant **Launch Lunar Module (Script)** , puis configurez-le comme suit :

* Définissez **Thrust** pour que le module lunaire décolle correctement au lancement, par exemple avec la valeur 0,01.

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step4-1.png)

### <a name="5-add-and-configure-the-toggle-placement-hints-script-component"></a>5. Ajouter et configurer le composant Toggle Placement Hints (Script)

L’objet RocketLauncher > **LunarModule** étant encore sélectionné, ajoutez le composant **Toggle Placement Hints (Script)** , puis configurez-le comme suit :

* Définissez la propriété **Size** de Game Object Array avec la valeur 5.
* Affectez chaque **objet enfant** de l’objet RocketLauncher > LunarModule > **PlacementHints** à un champ **Element** de Game Object Array :

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step5-1.png)

## <a name="configuring-the-launch-button"></a>Configuration du bouton de lancement

Dans la fenêtre Hierarchy, sélectionnez l’objet RocketLauncher > Buttons > **LaunchButton**, puis dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule.StartThruster** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-1.png)

> [!TIP]
> Si vous avez besoin d’un rappel sur la façon d’implémenter des événements, consultez les instructions dans [Gestes de suivi de la main et boutons d’interaction](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons).

L’objet RocketLauncher > Buttons > **LaunchButton** étant encore sélectionné, dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **LunarModule** pour recevoir l’événement, définissez **AudioSource.PlayOneShot** comme action à déclencher, puis affectez un clip audio approprié au champ **Audio Clip**, par exemple le clip audio MRTK_Gem :

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-2.png)

L’objet RocketLauncher > Buttons > **LaunchButton** étant encore sélectionné, dans le composant **Pressable Button (Script)** , créez un événement **Touch End ()** , configurez l’objet **LunarModule** pour recevoir l’événement, puis définissez **LaunchLunarModule.StopThruster** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-3.png)

Si vous passez maintenant en mode Game et que vous appuyez sur le bouton de lancement, vous entendez le clip audio. Si vous maintenez le bouton de lancement enfoncé pendant au moins une seconde, le module lunaire est lancé dans l’espace :

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-4.png)

## <a name="configuring-the-reset-button"></a>Configuration du bouton de réinitialisation

Dans la fenêtre Hierarchy, sélectionnez l’objet RocketLauncher > Buttons > **ResetButton**, puis dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule.ResetModule** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-1.png)

L’objet RocketLauncher > Buttons > **ResetButton** étant encore sélectionné, dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **RocketLauncher** pour recevoir l’événement, définissez **GameObject.BroadcastMessage** comme action à déclencher, puis entrez **ResetPlacement** dans le champ du message :

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-2.png)

> [!TIP]
> L’action GameObject.BroadcastMessage envoie le message ResetPlacement de l’objet RocketLauncher à tous ses objets enfants. Tout objet enfant ayant la fonction ResetPlacement, qui est définie dans le composant Part Assembly Demo (Script) que vous avez ajouté à tous les objets enfants de LunarModuleParts, appelle la fonction ResetPlacement qui réinitialise le placement de l’objet enfant.

Si vous passez maintenant en mode Game, déplacez certains composants et/ou lancez le module lunaire, puis appuyez sur le bouton Reset, la position d’origine des composants et/ou du module lunaire est rétablie :

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-3.png)

## <a name="configuring-the-placement-hints-button"></a>Configuration du bouton d’indicateurs de placement
<!-- TODO: Rename to 'Configuring the Hints button'-->

Dans la fenêtre Hierarchy, sélectionnez l’objet RocketLauncher > Buttons > **HintsButton**, puis dans le composant **Pressable Button (Script)** , créez un événement **Button Pressed ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **TogglePlacementHints.ToggleGameObjects** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial6-section5-step1-1.png)

Si vous passez maintenant en mode Game, vous pouvez constater que les indicateurs d’emplacement translucides sont désactivés par défaut. Vous pouvez toutefois les activer et les désactiver en appuyant sur le bouton d’indicateurs de placement :

![mrlearning-base](images/mrlearning-base/tutorial6-section5-step1-2.png)

## <a name="congratulations"></a>Félicitations

Vous avez entièrement configuré cette application. Les utilisateurs peuvent désormais assembler entièrement le module lunaire, le lancer, activer/désactiver les indicateurs et réinitialiser l’application pour recommencer.
