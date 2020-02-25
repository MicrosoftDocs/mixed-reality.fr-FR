---
title: Didacticiels de mise en route-7. Création d’un exemple d’application de module lunaire
description: Dans cette leçon, vous allez combiner plusieurs concepts appris dans les leçons précédentes pour créer un exemple d’expérience unique.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 3a557be91bee9b98e750ae1546ea1c4b3103298e
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77555257"
---
# <a name="7-creating-a-lunar-module-sample-application"></a>7. création d’un exemple d’application de module lunaire
<!-- TODO: Rename to 'Creating a Rocket Launcher sample application' -->

Dans ce didacticiel, plusieurs concepts sont combinés à partir de leçons précédentes pour créer un exemple d’expérience unique. Vous allez apprendre à créer une application d’assemblage de pièces dans laquelle un utilisateur doit utiliser des mains suivies pour récupérer des pièces et tenter d’assembler un module lunaire. Vous allez utiliser des boutons permettant d’activer et de désactiver les indicateurs de positionnement, de réinitialiser l’expérience et de lancer le module lunaire dans l’espace.

Dans les prochains didacticiels, vous continuerez à développer cette expérience, qui comprend des cas d’utilisation multi-utilisateurs puissants qui tirent parti des ancres spatiales Azure pour l’alignement spatial.

## <a name="objectives"></a>Objectifs

* Combiner plusieurs concepts issus des leçons précédentes pour créer une même expérience
* Découvrir comment activer/désactiver des objets
* Déclencher des événements complexes en utilisant des boutons enfonçables
* Utiliser la physique et les forces des corps rigides
* Explorer l’utilisation d’info-bulles

## <a name="lunar-module-parts-overview"></a>Vue d’ensemble des parties du module lunaire
<!-- TODO: Rename to 'Implementing the part assembly functionality' -->

Dans cette section, vous allez créer un simple défi d’assemblage de pièces où l’objectif de l’utilisateur est de placer cinq parties qui sont réparties sur la table à l’emplacement approprié sur le module lunaire.

Voici les principales étapes à suivre pour y parvenir :

1. Ajouter le Prefab du lanceur Rocket à la scène
2. Activer la manipulation d’objets pour toutes les parties
3. Ajouter et configurer le composant de démonstration d’assembly d’un composant (script)

> [!NOTE]
> Le composant de démonstration de l’assembly de composant (script) ne fait pas partie de MRTK. Il a été fourni avec les ressources de ce didacticiel.

### <a name="1-add-the-rocket-launcher-prefab-to-the-scene"></a>1. ajouter le Prefab du lanceur Rocket à la scène

Dans la fenêtre projet, accédez aux **ressources** > **MRTK. Tutoriels. GettingStarted** > **Prefabs** > dossier **RocketLauncher** , faites glisser le Prefab **RocketLauncher** dans la fenêtre hiérarchie pour l’ajouter à votre scène, puis placez-le à un emplacement approprié, par exemple :

* Transformer la position X = 1,5, Y =-0,4, Z = 0, afin qu’elle soit positionnée à droite de l’utilisateur à la hauteur de la taille
* Transform rotation X = 0, Y = 180, Z = 0, les principales fonctionnalités de l’expérience sont-elles l’utilisateur

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step1-1.png)

### <a name="2-enable-object-manipulation-for-all-the-parts"></a>2. activer la manipulation d’objets pour toutes les parties

Dans la fenêtre hiérarchie, localisez l’objet RocketLauncher > **LunarModuleParts** et sélectionnez tous les **objets enfants**, ajoutez le composant de **Gestionnaire de manipulation (script)** et le composant de script (script) à **proximité d’interaction** , puis configurez le gestionnaire de manipulation (script) comme suit :

* Désactivez la case à cocher **autoriser la manipulation Far** pour autoriser uniquement l’interaction proche.
* Modifier **deux types de manipulations de droitier** pour **déplacer la rotation** afin que la mise à l’échelle soit désactivée

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step1-2.png)

> [!TIP]
> Pour obtenir un rappel, avec des instructions pas à pas sur la façon d’implémenter la manipulation d’objets, vous pouvez consulter les instructions sur la [manipulation d’objets 3D](mrlearning-base-ch4.md#manipulating-3d-objects) .

### <a name="3-add-and-configure-the-part-assembly-demo-script-component"></a>3. Ajouter et configurer le composant de démonstration d’assembly d’un composant (script)

Avec tous les objets enfants LunarModuleParts toujours sélectionnés, ajoutez un composant **audio source** , puis configurez-le comme suit :

* Affectez un clip audio approprié au champ **Audioclip** , par exemple, MRKT_Scale_Start
* Désactivez la case à cocher **lire sur éveil** , afin que le clip audio ne soit pas automatiquement lu lors du chargement de la scène.
* Remplacez **spatial Blend** par 1 pour activer l’audio spatial

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-1.png)

Après avoir sélectionné tous les objets enfants LunarModuleParts, ajoutez le composant de **démonstration de l’assembly de composant (script)** :

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-2.png)

Dans la fenêtre hiérarchie, sélectionnez l’objet **RoverEnclosure** et configurez son composant de **démonstration d’assembly (script)** comme suit :

* Pour le champ **objet à placer** , assignez l’objet **lui-même**, dans ce cas, l’objet RoverEnclosure
* Dans le champ **emplacement à placer** , assignez l’objet **PlacementHints** correspondant, dans ce cas, l’objet RoverEnclosure_PlacementHint
* Dans le champ **objet d’info-bulle** , assignez l' **info-bulle**correspondante, dans ce cas, l’objet RoverEnclosure_ToolTip
* Dans le champ **source audio** , assignez l’objet **lui-même**, dans ce cas, l’objet RoverEnclosure

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-3.png)

**Répétez cette opération** pour chacun des autres objets enfants LunarModuleParts, C.-à-d. FuelTank, EnergyCell, DockingPortal et ExternalSensor.

Si vous passez maintenant en mode jeu et que vous déplacez un « objet à placer » proche de son emplacement correspondant à l’emplacement de destination, vous remarquerez que :

* L’objet sera mis en place et sera apparenté sous l’objet LunarModule afin qu’il fasse partie du module lunaire
* La source audio sur l’objet lira le clip audio affecté à l’emplacement de l’objet.
* L’objet d’info-bulle correspondant sera masqué

![mrlearning-base](images/mrlearning-base/tutorial6-section1-step2-4.png)

> [!TIP]
> Pour obtenir un rappel sur l’utilisation de la simulation d’entrée dans l’éditeur, vous pouvez vous reporter au [à l’aide de la simulation d’entrée de l’éditeur pour tester un](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) Guide de scène dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="configuring-the-lunar-module"></a>Configuration du module lunaire

Dans cette section, vous allez ajouter des fonctionnalités supplémentaires à l’application du lanceur Rocket afin que l’utilisateur puisse :

* Interagir avec le module lunaire
* Lancer le module lunaire dans l’espace et émettre un signal sonore lorsqu’il est lancé
* Réinitialisation de l’application pour que le module lunaire et toutes les parties soient remis à leur position d’origine
* Masquez les indicateurs de placement pour compliquer le défi de l’assembly du composant.

Voici les principales étapes à suivre pour y parvenir :

1. Activer la manipulation d’objets
2. Activer la physique
3. Ajouter un composant source audio
4. Ajouter et configurer le composant Launch lunaire module (script)
5. Ajouter et configurer le composant activer/désactiver les indicateurs de positionnement (script)

> [!NOTE]
> Le composant Launch lunaire module (script) et le composant indicateurs de positionnement Toggle (script) ne font pas partie de MRTK. Ils ont été fournis avec les ressources de ce didacticiel.

### <a name="1-enable-object-manipulation"></a>1. activer la manipulation d’objets

Dans la fenêtre hiérarchie, sélectionnez l’objet RocketLauncher > **LunarModule** , ajoutez le composant de **Gestionnaire de manipulation (script)** et le composant de script (script) à proximité de l' **interaction** , puis configurez le gestionnaire de manipulation (script) comme suit :

* Désactivez la case à cocher **autoriser la manipulation Far** pour autoriser uniquement l’interaction proche.
* Modifier **deux types de manipulations de droitier** pour déplacer la rotation afin que la mise à l’échelle soit désactivée

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step1-1.png)

### <a name="2-enable-physics"></a>2. activer la physique

Avec l’objet RocketLauncher > **LunarModule** toujours sélectionné, ajoutez un composant **RigidBody** , puis configurez-le comme suit :

* Désactivez la case à cocher **utiliser la gravité** pour que le module lunaire ne soit pas affecté par la gravité
* Cochez la case **est cinématique** pour que le module lunaire ne soit pas affecté initialement par les forces physico-

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step2-1.png)

### <a name="3-add-an-audio-source-component"></a>3. Ajouter un composant source audio

Avec l’objet RocketLauncher > **LunarModule** toujours sélectionné, ajoutez un composant **audio source** , puis configurez-le comme suit :

* Remplacez **spatial Blend** par 1 pour activer l’audio spatial

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step3-1.png)

### <a name="4-add-and-configure-the-launch-lunar-module-script-component"></a>4. Ajouter et configurer le composant Launch lunaire module (script)

Avec l’objet RocketLauncher > **LunarModule** toujours sélectionné, ajoutez le composant **Launch lunaire module (script)** , puis configurez-le comme suit :

* Modifiez la valeur de **Poussée** afin que le module lunaire se déplacera correctement au lancement, par exemple, à 0,01

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step4-1.png)

### <a name="5-add-and-configure-the-toggle-placement-hints-script-component"></a>5. Ajouter et configurer le composant activer/désactiver les indicateurs de positionnement (script)

Avec l’objet RocketLauncher > **LunarModule** toujours sélectionné, ajoutez le composant **activer/désactiver les indicateurs de positionnement (script)** , puis configurez-le comme suit :

* Affectez à la propriété **taille** du tableau d’objets de jeu la valeur 5
* Affectez chacun des **objets enfants** RocketLauncher > LunarModule > **PlacementHints** à un champ d' **élément** dans le tableau d’objets de jeu :

![mrlearning-base](images/mrlearning-base/tutorial6-section2-step5-1.png)

## <a name="configuring-the-launch-button"></a>Configuration du bouton de lancement

Dans la fenêtre hiérarchie, sélectionnez les boutons de > RocketLauncher > objet **LaunchButton** , puis sur le composant **bouton enfoncé (script)** , créez un événement **bouton appuyé ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule. StartThruster** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-1.png)

> [!TIP]
> Pour obtenir un rappel sur la façon d’implémenter des événements, vous pouvez consulter les instructions de suivi de la [main et les boutons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) interactifs.

À l’aide des boutons de > RocketLauncher > objet **LaunchButton** toujours sélectionné, sur le composant **bouton appuyé (script)** , créez un événement **bouton enfoncé ()** , configurez l’objet **LunarModule** pour recevoir l’événement, définissez **audiosource. PlayOneShot** comme action à déclencher et affectez un clip audio approprié au champ de **clip** audio, par exemple, le clip audio MRTK_Gem :

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-2.png)

À l’aide des boutons de > RocketLauncher > objet **LaunchButton** toujours sélectionné, sur le composant **bouton (script) pouvant être appuyé** , créez un événement **Touch end ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule. StopThruster** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-3.png)

Si vous entrez maintenant le mode jeu et que vous appuyez sur le bouton de lancement, vous entendez le clip audio, et si vous maintenez le bouton de lancement enfoncé pendant environ une seconde ou plus, vous verrez le lancement du module lunaire dans l’espace :

![mrlearning-base](images/mrlearning-base/tutorial6-section3-step1-4.png)

## <a name="configuring-the-reset-button"></a>Configuration du bouton de réinitialisation

Dans la fenêtre hiérarchie, sélectionnez les boutons de > RocketLauncher > objet **ResetButton** , puis sur le composant **bouton enfoncé (script)** , créez un événement **bouton appuyé ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **LaunchLunarModule. ResetModule** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-1.png)

À l’aide des boutons de > RocketLauncher > objet **ResetButton** toujours sélectionné, sur le composant **bouton appuyé (script)** , créez un événement **bouton enfoncé ()** , configurez l’objet **RocketLauncher** pour recevoir l’événement, définissez **GameObject. BroadcastMessage** comme action à déclencher, puis entrez **ResetPlacement** dans le champ message :

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-2.png)

> [!TIP]
> L’action GameObject. BroadcastMessage envoie le message ResetPlacement de l’objet RocketLauncher à tous ses objets enfants. Tout objet enfant qui a la fonction ResetPlacement, qui est définie dans le composant de démonstration d’assembly d’élément (script) que vous avez ajouté à tous les objets enfants LunarModuleParts, appellera la fonction ResetPlacement qui réinitialise le placement de cet objet enfant.

Si vous passez maintenant en mode jeu, déplacez certaines parties et/ou lancez le module lunaire, puis appuyez sur le bouton Réinitialiser pour voir les parties et/ou le module lunaire être réinitialisés à leur position d’origine :

![mrlearning-base](images/mrlearning-base/tutorial6-section4-step1-3.png)

## <a name="configuring-the-placement-hints-button"></a>Configuration du bouton indicateurs de positionnement
<!-- TODO: Rename to 'Configuring the Hints button'-->

Dans la fenêtre hiérarchie, sélectionnez les boutons de > RocketLauncher > objet **HintsButton** , puis sur le composant **bouton enfoncé (script)** , créez un événement **bouton appuyé ()** , configurez l’objet **LunarModule** pour recevoir l’événement et définissez **TogglePlacementHints. ToggleGameObjects** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial6-section5-step1-1.png)

Si vous passez maintenant en mode jeu, vous remarquerez que les indicateurs d’emplacement translucides sont désactivés par défaut, mais que vous pouvez les activer et les désactiver en appuyant sur le bouton indicateurs :

![mrlearning-base](images/mrlearning-base/tutorial6-section5-step1-2.png)

## <a name="congratulations"></a>Félicitations

Vous avez entièrement configuré cette application. Désormais, votre application permet aux utilisateurs d’assembler entièrement le module lunaire, de lancer le module lunaire, de basculer les indicateurs et de réinitialiser l’application pour redémarrer.
