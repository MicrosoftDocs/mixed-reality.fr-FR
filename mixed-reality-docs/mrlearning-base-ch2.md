---
title: Didacticiels de mise en route-3. Création d’une interface utilisateur et configuration d’une réalité mixte Toolkit
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: f1d042150d1c81940e672b174c6c02ac71e05883
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77554880"
---
# <a name="3-creating-user-interface-and-configure-mixed-reality-toolkit"></a>3. création d’une interface utilisateur et configuration d’une réalité mixte Toolkit
<!-- TODO: Consider renaming to 'Configuring Mixed Reality Toolkit profiles and creating user interfaces' -->

Dans le didacticiel précédent, vous avez appris certaines des possibilités offertes par le kit d’outils de réalité mixte (MRTK) en démarrant votre première application pour HoloLens 2. Dans ce didacticiel, vous allez apprendre à créer et à organiser des boutons avec des panneaux de texte d’interface utilisateur et à utiliser l’interaction par défaut (Touch) pour interagir avec chaque bouton. Vous allez également découvrir comment ajouter des actions et des effets simples, comme changer la taille, la sonorité et la couleur des objets. Ce module présente les concepts de base de la modification des profils MRTK, en commençant par la désactivation de la visualisation de maillage de [mappage spatial](spatial-mapping.md) .

## <a name="objectives"></a>Objectifs

* Personnaliser et configurer des profils MRTK
* Interagir avec des hologrammes à l’aide d’éléments d’interface utilisateur et de boutons
* Entrées et interactions de base pour le suivi de la main

## <a name="how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option"></a>Comment configurer les profils de la boîte à outils de la réalité mixte (modifier l’option d’affichage de sensibilisation spatiale)
<!-- TODO: Consider renaming to 'How to customize the MRTK profiles' -->

Dans cette section, vous allez apprendre à personnaliser et à configurer les profils MRTK par défaut.

Cet exemple indique comment masquer le maillage de la sensibilisation spatiale en modifiant les paramètres de l’observateur de maillage spatial. Toutefois, vous pouvez suivre ces mêmes principes pour personnaliser n’importe quel paramètre ou valeur dans les profils MRTK.

Les principales étapes à suivre pour masquer le maillage de la sensibilisation spatiale sont les suivantes :

1. Cloner le profil de configuration par défaut
2. Activer le système de sensibilisation spatiale
3. Cloner le profil système de sensibilisation spatiale par défaut
4. Cloner le profil d’observateur de maillage de sensibilisation spatiale par défaut
5. Modifier la visibilité du maillage de la sensibilisation spatiale

> [!NOTE]
> Par défaut, les profils MRTK ne sont pas modifiables. Il s’agit des modèles de profil par défaut que vous devez cloner avant de pouvoir les modifier. Il existe plusieurs couches imbriquées de profils. Par conséquent, il est courant de cloner et de modifier plusieurs profils lors de la configuration d’un ou plusieurs paramètres.

### <a name="1-clone-the-default-configuration-profile"></a>1. cloner le profil de configuration par défaut

> [!NOTE]
> Le profil de configuration est le profil de niveau supérieur. Par conséquent, pour pouvoir modifier d’autres profils, vous devez d’abord cloner le profil de configuration.

Lorsque l’objet **MixedRealityToolkit** est sélectionné dans la fenêtre hiérarchie, dans la fenêtre de l’inspecteur, modifiez le **profil de configuration** du Toolkit de réalité mixte en **DefaultHoloLens2ConfigurationProfile**:

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-1.png)

L’objet **MixedRealityToolkit** étant toujours sélectionné, dans la fenêtre de l’inspecteur, cliquez sur le bouton **Copier & personnaliser** pour ouvrir la fenêtre cloner le profil :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-2.png)

Dans la fenêtre cloner le profil, cliquez sur le bouton **cloner** pour créer une copie modifiable de l' **DefaultHololens2ConfigurationProfile**:

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-3.png)

Le profil de configuration que vous venez de créer est maintenant affecté comme profil de configuration pour votre scène :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-4.png)

Dans le menu Unity, sélectionnez **fichier** > **Enregistrer** pour enregistrer votre scène.

> [!TIP]
> N’oubliez pas d’enregistrer votre travail tout au long du didacticiel.

### <a name="2-enable-the-spatial-awareness-system"></a>2. activer le système de sensibilisation spatiale

Lorsque l’objet **MixedRealityToolkit** est toujours sélectionné dans la fenêtre hiérarchie, dans la fenêtre Inspecteur, sélectionnez l’onglet **détection spatiale** , puis activez la case à cocher **activer le système de sensibilisation spatiale** :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step2-1.png)

### <a name="3-clone-the-default-spatial-awareness-system-profile"></a>3. cloner le profil système de sensibilisation spatiale par défaut

Dans l’onglet **sensibilisation spatiale** , cliquez sur le bouton **cloner** pour ouvrir la fenêtre cloner le profil :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-1.png)

Dans la fenêtre cloner le profil, cliquez sur le bouton **cloner** pour créer une copie modifiable de l' **DefaultMixedRealitySpatialAwarenessSystemProfile**:

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-2.png)

Le profil de système de sensibilisation spatiale nouvellement créé est maintenant automatiquement affecté à votre profil de configuration :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-3.png)

### <a name="4-clone-the-default-spatial-awareness-mesh-observer-profile"></a>4. clonez le profil d’observateur de maillage de détection spatiale par défaut

Avec l’onglet **sensibilisation spatiale** toujours sélectionné, développez la section **Observateur de maillage spatial Windows Mixed Reality** , puis cliquez sur le bouton **cloner** pour ouvrir la fenêtre cloner le profil :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-1.png)

Dans la fenêtre cloner le profil, cliquez sur le bouton **cloner** pour créer une copie modifiable de l' **DefaultMixedRealitySpatialAwarenessMeshObserverProfile**:

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-2.png)

Le profil d’observateur de maillage de sensibilisation spatiale nouvellement créé est maintenant automatiquement affecté à votre profil système de sensibilisation spatiale :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-3.png)

### <a name="5-change-the-visibility-of-the-spatial-awareness-mesh"></a>5. modifier la visibilité du maillage de la sensibilisation spatiale

Dans les **paramètres d’observateur de maillage spatial**, définissez l' **option d’affichage** sur **occlusion** pour rendre le maillage de mappage spatial invisible alors qu’il est toujours fonctionnel :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step5-1.png)

> [!NOTE]
> Bien que le maillage de mappage spatial ne soit pas visible, il est toujours présent et fonctionnel. Par exemple, tous les hologrammes derrière le maillage de mappage spatial, tels qu’un hologramme derrière un mur physique, ne sont pas visibles.

Vous venez de découvrir comment modifier un paramètre dans le profil MRTK. Comme vous pouvez le voir, pour personnaliser les paramètres MRTK, vous devez d’abord créer des copies des profils par défaut. Étant donné que les profils par défaut ne sont pas modifiables, vous les aurez toujours comme référence si vous souhaitez rétablir les paramètres par défaut. Pour en savoir plus sur les profils MRTK et leur architecture, vous pouvez consulter le [Guide de configuration du profil du Toolkit de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) dans le portail de [documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="hand-tracking-gestures-and-interactable-buttons"></a>Mouvements de suivi de main et boutons interactifs

Dans cette section, vous allez apprendre à utiliser le suivi de la main pour appuyer sur un bouton et déclencher des événements pour déclencher une action lorsque le bouton est enfoncé.

Cet exemple vous montre comment modifier la couleur d’un cube lorsque le bouton est enfoncé et rétablir sa couleur d’origine quand le bouton est relâché. Toutefois, vous pouvez suivre ces mêmes principes pour créer d’autres événements.

Les principales étapes à suivre pour modifier la couleur du cube sont les suivantes :

1. Ajouter un bouton Prefab à la scène
2. Ajouter un cube à la scène
3. Configurer le type d’événement InteractableOnPressReceiver
4. Configurer le cube pour recevoir l’événement on Press
5. Définir l’action qui doit être déclenchée par l’événement on Press
6. Configurer le cube pour recevoir l’événement on release
7. Définir l’action qui doit être déclenchée par l’événement on release
8. Tester le bouton à l’aide de la simulation dans l’éditeur

### <a name="1-add-a-pressable-button-prefab-to-the-scene"></a>1. Ajouter un bouton Prefab à la scène

> [!TIP]
> Un <a href="https://docs.unity3d.com/Manual/Prefabs.html" target="_blank">Prefab</a> est un gameobject préconfiguré stocké en tant que ressource Unity et peut être réutilisé dans tout le projet.

Dans la **fenêtre projet**, recherchez **PressableButtonHoloLens2** pour trouver le Prefab que vous allez utiliser pour cet exemple :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-1.png)

Dans les résultats de la **recherche** , sélectionnez le Prefab **PressableButtonHoloLens2** et faites-le **glisser** dans la fenêtre **hiérarchie** pour l’ajouter à votre scène :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-2.png)

> [!TIP]
> Pour afficher votre scène comme indiqué dans l’image ci-dessous, double-cliquez sur l’objet PressableButtonHoloLens2 dans la fenêtre hiérarchie pour l’activer, puis utilisez la <a href="https://docs.unity3d.com/Manual/SceneViewNavigation.html" target="_blank">scène Gizmo</a>, située dans le coin supérieur droit de la fenêtre de scène, pour ajuster l’angle d’affichage sur l’axe Z de l’avant.

L’objet **PressableButtonHoloLens2** étant toujours sélectionné, dans la fenêtre de l' **inspecteur** :

* Modifiez sa **position** de transformation pour qu’elle soit positionnée devant l’appareil photo, qui est positionné à l’origine, par exemple, x = 0, y = 0 et z = 0,5

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-3.png)

> [!NOTE]
> En général, une unité de position dans Unity est à peu près équivalente à 1 mètre dans le monde physique. Toutefois, il existe des exceptions à cela, par exemple lorsque des objets sont des enfants d’objets mis à l’échelle.

### <a name="2-add-a-cube-to-the-scene"></a>2. Ajouter un cube à la scène

Cliquez avec le bouton droit sur une zone vide à l’intérieur de la fenêtre de hiérarchie et sélectionnez **objet 3d** > **cube** pour ajouter un cube à votre scène :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step2-1.png)

Lorsque l’objet **cube** est toujours sélectionné, dans la fenêtre **Inspector** :

* Modifiez sa **position** de transformation de sorte qu’elle soit située près du bouton enfoncé, mais qu’elle ne se chevauche pas, par exemple x = 0, y = 0,04 et z = 0,5
* Modifiez son **échelle** de transformation en lui attribuant une taille appropriée, par exemple, x = 0,02, y = 0,02 et z = 0,02

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step2-2.png)

### <a name="3-configure-the-interactableonpressreceiver-event-type"></a>3. configurer le type d’événement InteractableOnPressReceiver

Dans la fenêtre hiérarchie, sélectionnez l’objet **PressableButtonHoloLens2** , puis dans le **menu hamburger**de la fenêtre de l' **inspecteur** , sélectionnez **réduire tous les composants** pour avoir une vue d’ensemble de tous les composants de cet objet :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-1.png)

Développez le composant **(script)** pouvant être interagi, puis localisez et développez la section **événements** > les **destinataires** :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-2.png)

Cliquez sur le bouton **Ajouter un événement** pour créer un récepteur d’événements de type récepteur d’événements **InteractableOnPressReceiver**:

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-3.png)

> [!NOTE]
> Le type de récepteur d’événements nommé InteractableOnPressReceiver permet au bouton de répondre à un événement appuyé quand un suivi appuie sur le bouton.

Pour le récepteur d’événements nouvellement créé, remplacez le **filtre d’interaction** par **near et Far**:

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-4.png)

### <a name="4-configure-the-cube-to-receive-the-on-press-event"></a>4. configurer le cube pour recevoir l’événement on Press

Dans la fenêtre hiérarchie, **cliquez et faites glisser** le **cube** dans le champ objet des **propriétés d’événement** pour l’événement **on Press ()** afin d’affecter le cube comme récepteur de l’événement on Press () :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step4-1.png)

### <a name="5-define-the-action-to-be-triggered-by-the-on-press-event"></a>5. définir l’action qui doit être déclenchée par l’événement on Press

Cliquez sur la liste déroulante action, **aucune fonction**actuellement affectée, puis sélectionnez **MeshRenderer** > **matériau** matériel pour définir la propriété Material du cube à modifier lorsque l’événement on Press () est déclenché :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-1.png)

Cliquez sur l’icône représentant un petit **cercle** en regard du champ matériel, actuellement remplie sans **aucun (matériau)** , pour ouvrir la fenêtre Sélectionner une matière :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-2.png)

Dans la fenêtre Sélectionner une matière , recherchez **MRTK_Standard** et sélectionnez un matériau approprié, par exemple, **MRTK_Standard_Cyan** pour que la couleur du cube change en cyan lorsque le bouton est enfoncé :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-3.png)

### <a name="6-configure-the-cube-to-receive-the-on-release-event"></a>6. configurer le cube pour recevoir l’événement on release

**Répéter** Étape 4 pour l’événement on release afin d’affecter le **cube** comme récepteur de l’événement **on release ()** .

### <a name="7-define-the-action-to-be-triggered-by-the-on-release-event"></a>7. définir l’action qui doit être déclenchée par l’événement on release

**Répéter** Étape 5 pour l’événement on release, mais choisissez le matériel **MRTK_Standard_LightGray** pour que la couleur du cube retourne à sa couleur gris clair d’origine lorsque le bouton est relâché :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step7-1.png)

### <a name="8-test-the-button-using-the-in-editor-simulation"></a>8. Testez le bouton à l’aide de la simulation dans l’éditeur

Appuyez sur le bouton **lecture** pour entrer en mode jeu et utilisez la simulation d’entrée de l’éditeur pour tester le bouton que vous venez de configurer.

Bouton non enfoncé (espace + molette de défilement de la souris vers l’arrière) :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step8-1.png)

Bouton enfoncé (espace + molette de défilement de la souris vers l’avant) :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step8-2.png)

> [!TIP]
> Pour savoir comment utiliser la simulation d’entrée dans l’éditeur, vous pouvez vous reporter au [à l’aide de la simulation d’entrée de l’éditeur pour tester un](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) Guide de scène dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="creating-a-panel-of-buttons-using-mrtks-grid-object-collection"></a>Création d’un panneau de boutons avec la collection d’objets de grille du MRTK

Dans cette section, vous allez apprendre à aligner automatiquement plusieurs boutons dans une interface utilisateur claire à l’aide de l’outil de collection d’objets Grid de MRTK.

Cet exemple indique comment créer un panneau avec cinq boutons alignés horizontalement. Toutefois, vous pouvez suivre ces mêmes principes pour créer d’autres dispositions.

Voici les principales étapes à suivre pour y parvenir :

1. Parent des objets bouton à un objet parent
2. Ajouter et configurer le composant de collection d’objets Grid (script)
3. Tester les boutons à l’aide de la simulation dans l’éditeur

### <a name="1-parent-the-button-objects-to-a-parent-object"></a>1. parent des objets bouton à un objet parent

Cliquez avec le bouton droit sur une zone vide à l’intérieur de la fenêtre de hiérarchie et sélectionnez **créer un vide**:

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-1.png)

Cliquez avec le bouton droit sur l’objet nouvellement créé, sélectionnez **Renommer**, puis attribuez-lui un nom approprié, par exemple, **ButtonCollection**:

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-2.png)

Sélectionnez l’objet **PressableButtonHoloLens2** et **faites** -le glisser sur l’objet **ButtonCollection** pour en faire un enfant de l’objet ButtonCollection :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-3.png)

Cliquez avec le bouton droit sur l’objet **PressableButtonHoloLens2** et sélectionnez **dupliquer** pour en créer une copie :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-4.png)

**Répétez** cette étape quatre fois, jusqu’à ce que vous ayez un total de cinq objets PressableButtonHoloLens2.

### <a name="2-add-and-configure-the-grid-object-collection-script-component"></a>2. Ajouter et configurer le composant collection d’objets Grid (script)

Lorsque l’objet ButtonCollection est sélectionné dans la fenêtre hiérarchie, dans la fenêtre Inspecteur, cliquez sur le bouton **Ajouter un composant** , puis recherchez et sélectionnez **collection d’objets Grid** pour ajouter un composant de collection d’objets Grid (script) à l’objet ButtonCollection :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-1.png)

Configurez la collection d’objets Grid (script) comme suit :

* Remplacez le **nombre de lignes** par 1 pour que tous les boutons soient alignés sur une seule ligne
* Modifiez la **largeur de cellule** sur 0,05 pour espacer les boutons dans la ligne

Cliquez ensuite sur le bouton **mettre à jour la collection** pour appliquer la nouvelle configuration :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-2.png)

> [!NOTE]
> Les modifications de configuration que vous venez d’appliquer représentent les modifications minimales requises pour atteindre l’objectif de placer les boutons sur une seule ligne. Toutefois, dans les projets futurs, en fonction de facteurs tels que, par exemple, l’orientation des objets parents et enfants, vous devrez peut-être ajuster d’autres paramètres tels que, par exemple, le type d’orientation. Pour en savoir plus sur la collection d’objets Grid de MRTK, vous pouvez consulter le guide des [scripts de collection d’objets](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html#object-collection-scripts) dans le portail de [documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

Lorsque l’objet ButtonCollection est toujours sélectionné dans la fenêtre hiérarchie, dans la fenêtre de l’inspecteur, modifiez la **position** de la transformation de l’objet ButtonCollection de sorte que ses objets bouton enfant soient positionnés devant l’appareil photo, qui est positionné à l’origine, par exemple, x = 0, y = 0 et z = 0,5 :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-3.png)

> [!NOTE]
> Lorsque vous avez ajouté pour la première fois le Prefab PressableButtonHoloLens2 à la scène dans la section [gestes de suivi de main et boutons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) interactifs ci-dessus, vous l’avez positionné devant l’appareil photo. Toutefois, étant donné que la collection d’objets Grid contrôle ses objets enfants immédiats, la position Z des objets enfants PressableButtonHoloLens2 est réinitialisée à 0 en fonction de la distance par défaut de la collection d’objets Grid par rapport à la valeur parente de 0. C’est pourquoi, et pour que la relation de position parent/enfant est organisée, c’est pourquoi nous avons déplacé la position de l’objet ButtonCollection parent au lieu de configurer la distance à partir de la valeur parente pour déplacer les objets enfants PressableButtonHoloLens2 vers l’avant.

### <a name="3-test-the-buttons-using-the-in-editor-simulation"></a>3. Testez les boutons à l’aide de la simulation dans l’éditeur

Appuyez sur le bouton lecture pour entrer en mode jeu et utilisez la simulation d’entrée de l’éditeur pour tester chacun des boutons dans le nouveau panneau de boutons :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step3-1.png)

> [!TIP]
> Actuellement, lorsque vous appuyez sur l’un des cinq boutons, la couleur du cube devient cyan. Pour rendre l’expérience plus intéressante, utilisez ce que vous venez d’apprendre pour configurer chaque bouton afin de remplacer le cube par une autre couleur.

## <a name="adding-text-into-your-scene"></a>Ajout de texte dans votre scène

Dans cette section, vous allez apprendre à ajouter du texte à vos expériences de réalité mixte à l’aide de TextMesh Pro de Unity, que vous avez préparé dans la section [importer des ressources TextMesh Pro Essential](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources) du didacticiel précédent.

Dans cet exemple, vous allez ajouter une étiquette simple sous la collection de boutons que vous avez créée dans la section précédente.

Cliquez avec le bouton droit sur l’objet ButtonCollection, puis sélectionnez **objet 3d** > **Text-TextMeshPro** pour créer un objet TextMeshPro en tant qu’enfant de l’objet ButtonCollection :

![mrlearning-base](images/mrlearning-base/tutorial2-section4-step1-1.png)

Avec l’objet TextMeshPro nouvellement créé, nommé Text (TMP), toujours sélectionné, dans la fenêtre Inspector, modifiez sa position et sa taille pour que l’étiquette soit placée clairement sous la collection de boutons, par exemple :

* Remplacez le POS transformation Rect **Y** par-0,0425
* Modifiez la **largeur** de la transformation Rect en 0,24
* Modifier la **hauteur** de la transformation Rect en 0,024

Ensuite, mettez à jour le texte pour refléter l’étiquette et choisissez les propriétés de police pour que le texte tienne dans l’étiquette, par exemple :

* Remplacer le texte de maille Pro (script **) par** la collection de boutons
* Modifier le **style de police** du texte de maillage Pro (script) en gras
* Modifier la **taille de police** du texte de maille Pro (script) à 0,2
* Modifiez l' **alignement** du texte de maille Pro (script) en centre et au milieu

![mrlearning-base](images/mrlearning-base/tutorial2-section4-step1-2.png)

## <a name="congratulations"></a>Félicitations

Dans ce didacticiel, vous avez appris à cloner, personnaliser et configurer un paramètre de profil MRTK. Vous avez également appris à interagir avec les boutons pour déclencher des événements à l’aide d’un suivi sur le HoloLens 2. Enfin, vous avez appris à créer une interface d’interface utilisateur simple à l’aide du composant de collection d’objets Grid de MRTK et du texte Pro de l’Unity.

[Didacticiel suivant : 4. placement de contenu dynamique et utilisation de solveurs](mrlearning-base-ch3.md)
