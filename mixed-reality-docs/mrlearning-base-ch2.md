---
title: Tutoriels de démarrage - 3. Création de l’interface utilisateur et configuration du Kit d’outils de réalité mixte
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: c389c7a3d16770dcbf57d9acdcfd81c6507f7cd6
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79376136"
---
# <a name="3-creating-user-interface-and-configure-mixed-reality-toolkit"></a>3. Création de l’interface utilisateur et configuration du Kit d’outils de réalité mixte
<!-- TODO: Consider renaming to 'Configuring Mixed Reality Toolkit profiles and creating user interfaces' -->

Dans le tutoriel précédent, vous avez découvert certaines des fonctionnalités offertes par le Kit de ressources de réalité mixte (MRTK, Mixed Reality Toolkit) en commençant votre première application pour HoloLens 2. Dans ce tutoriel, vous allez découvrir comment créer et organiser des boutons et des panneaux de texte de l’interface utilisateur, et comment utiliser l’interaction par défaut (tactile) pour interagir avec chaque bouton. Vous allez également découvrir comment ajouter des actions et des effets simples, comme changer la taille, la sonorité et la couleur des objets. Ce module présente des concepts de base sur la façon de modifier des profils MRTK, en commençant par la désactivation de la visualisation du maillage de [mappage spatial](spatial-mapping.md).

## <a name="objectives"></a>Objectifs

* Personnaliser et configurer des profils MRTK
* Interaction avec des hologrammes en utilisant des éléments d’interface utilisateur et des boutons
* Entrées et interactions de base pour le suivi de la main

## <a name="how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option"></a>Comment configurer les profils du Kit de ressources de réalité mixte (Modifier l’option d’affichage de la reconnaissance spatiale)
<!-- TODO: Consider renaming to 'How to customize the MRTK profiles' -->

Dans cette section, vous allez découvrir comment personnaliser et configurer les profils MRTK par défaut.

Cet exemple va vous montrer comment masquer le maillage de la reconnaissance spatiale en modifiant les paramètres de l’observateur de maillage spatial. Vous pouvez cependant suivre ces mêmes principes pour personnaliser des paramètres ou des valeurs dans les profils MRTK.

Les principales étapes à suivre pour masquer le maillage de la reconnaissance spatiale sont les suivantes :

1. Cloner le profil de configuration par défaut
2. Activer le système de reconnaissance spatiale
3. Cloner le profil système de reconnaissance spatiale par défaut
4. Cloner le profil d’observateur de maillage de reconnaissance spatiale par défaut
5. Changer la visibilité du maillage de reconnaissance spatiale

> [!NOTE]
> Par défaut, les profils MRTK ne sont pas modifiables. Il s’agit des modèles de profil par défaut que vous devez cloner avant de pouvoir les modifier. Il existe plusieurs couches de profils imbriquées. Par conséquent, il est courant de cloner et de modifier plusieurs profils lors de la configuration d’un ou plusieurs paramètres.

### <a name="1-clone-the-default-configuration-profile"></a>1. Cloner le profil de configuration par défaut

> [!NOTE]
> Le profil de configuration est le profil de plus haut niveau. Par conséquent, pour pouvoir modifier d’autres profils, vous devez d’abord cloner le profil de configuration.

Avec l’objet **MixedRealityToolkit** sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, changez le **profil de configuration** Mixed Reality Toolkit en **DefaultHoloLens2ConfigurationProfile** :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-1.png)

Avec l’objet **MixedRealityToolkit** sélectionné, dans la fenêtre Inspector, cliquez sur le bouton **Copy & Customize** pour ouvrir la fenêtre Clone Profile :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-2.png)

Dans la fenêtre Clone Profile, cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultHololens2ConfigurationProfile** :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-3.png)

Le profil de configuration que vous venez de créer est maintenant affecté comme profil de configuration pour votre scène :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step1-4.png)

Dans le menu Unity, sélectionnez **File** > **Save** pour enregistrer votre scène.

> [!TIP]
> N’oubliez pas d’enregistrer votre travail tout au long du tutoriel.

### <a name="2-enable-the-spatial-awareness-system"></a>2. Activer le système de reconnaissance spatiale

Avec l’objet **MixedRealityToolkit** sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, sélectionnez l’onglet **Spatial Awareness**, puis cochez la case **Enable Spatial Awareness System** :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step2-1.png)

### <a name="3-clone-the-default-spatial-awareness-system-profile"></a>3. Cloner le profil système de reconnaissance spatiale par défaut

Sous l’onglet **Spatial Awareness**, cliquez sur le bouton **Clone** pour ouvrir la fenêtre Clone Profile :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-1.png)

Dans la fenêtre Clone Profile, cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultMixedRealitySpatialAwarenessSystemProfile** :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-2.png)

Le profil Spatial Awareness System nouvellement créé est maintenant automatiquement affecté à votre profil de configuration :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step3-3.png)

### <a name="4-clone-the-default-spatial-awareness-mesh-observer-profile"></a>4. Cloner le profil d’observateur de maillage de reconnaissance spatiale par défaut

Avec l’onglet **Spatial Awareness** sélectionné, développez la section **Windows Mixed Reality Spatial Mesh Observer**, puis cliquez sur le bouton **Clone** pour ouvrir la fenêtre Clone Profile :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-1.png)

Dans la fenêtre Clone Profile, cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultMixedRealitySpatialAwarenessMeshObserverProfile** :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-2.png)

Le profil Spatial Awareness Mesh Observer nouvellement créé est maintenant automatiquement affecté à votre profil Spatial Awareness System :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step4-3.png)

### <a name="5-change-the-visibility-of-the-spatial-awareness-mesh"></a>5. Changer la visibilité du maillage de reconnaissance spatiale

Dans **Spatial Mesh Observer Settings**, changez **Display Option** en **Occlusion** pour rendre le maillage de mappage spatial invisible tout en le laissant fonctionnel :

![mrlearning-base](images/mrlearning-base/tutorial2-section1-step5-1.png)

> [!NOTE]
> Bien que le maillage de mappage spatial ne soit pas visible, il est toujours présent et fonctionnel. Par exemple, les hologrammes qui sont derrière le maillage de mappage spatial, comme un hologramme derrière un mur physique, ne sont pas visibles.

Vous venez de découvrir comment modifier un paramètre dans le profil MRTK. Comme vous pouvez le voir, pour pouvoir personnaliser les paramètres du MRTK, vous devez d’abord créer des copies des profils par défaut. Étant donné que les profils par défaut ne sont pas modifiables, vous les aurez toujours comme référence si vous voulez rétablir les paramètres par défaut. Pour plus d’informations sur les profils MRTK et leur architecture, vous pouvez consulter le [Guide de configuration du profil Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="hand-tracking-gestures-and-interactable-buttons"></a>Gestes de suivi de la main et boutons d’interaction

Dans cette section, vous allez découvrir comment utiliser le suivi de la main pour appuyer sur un bouton et déclencher des événements pour provoquer une action quand le bouton est enfoncé.

Cet exemple vous montre comment changer la couleur d’un cube quand le bouton est enfoncé et rétablir sa couleur d’origine quand le bouton est relâché. Vous pouvez cependant suivre ces mêmes principes pour créer d’autres événements.

Les principales étapes à suivre pour changer la couleur du cube sont les suivantes :

1. Ajouter un préfabriqué de bouton enfonçable
2. Ajouter un cube à la scène
3. Configurer le type d’événement InteractableOnPressReceiver
4. Configurer le cube pour recevoir l’événement On Press
5. Définir l’action à déclencher par l’événement On Press
6. Configurer le cube pour recevoir l’événement On Release
7. Définir l’action à déclencher par l’événement On Release
8. Tester le bouton en utilisant la simulation dans l’éditeur

### <a name="1-add-a-pressable-button-prefab-to-the-scene"></a>1. Ajouter un préfabriqué de bouton enfonçable

> [!TIP]
> Un <a href="https://docs.unity3d.com/Manual/Prefabs.html" target="_blank">préfabriqué</a> (Prefab) est un GameObject préconfiguré stocké en tant que ressource Unity et qui peut être réutilisé dans tout votre projet.

Dans la **fenêtre Project**, recherchez **PressableButtonHoloLens2** pour localiser le préfabriqué que vous allez utiliser pour cet exemple :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-1.png)

Dans le résultat de la **Recherche**, sélectionnez le préfabriqué **PressableButtonHoloLens2** et **faites-le glisser** dans la fenêtre **Hierarchy** pour l’ajouter à votre scène :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-2.png)

> [!TIP]
> Pour afficher votre scène comme dans l’image ci-dessous, double-cliquez sur l’objet PressableButtonHoloLens2 dans la fenêtre Hierarchy pour lui donner le focus, puis utilisez le <a href="https://docs.unity3d.com/Manual/SceneViewNavigation.html" target="_blank">gizmo Scene</a>, qui se trouve dans le coin supérieur droit de la fenêtre Scene, pour ajuster l’angle de visualisation sur l’axe Z vers l’avant.

Avec l’objet **PressableButtonHoloLens2** sélectionné, dans la fenêtre **Inspector** :

* Changez la valeur **Position** de sa transformation de sorte qu’il soit positionné devant la caméra, elle-même positionnée à l’origine, par exemple x = 0, y = 0 et z = 0,5

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step1-3.png)

> [!NOTE]
> En règle générale, 1 unité de position dans Unity est à peu près équivalente à 1 mètre dans le monde physique. Il y a cependant des exceptions à cela, par exemple quand les objets sont des enfants d’objets mis à l’échelle.

### <a name="2-add-a-cube-to-the-scene"></a>2. Ajouter un cube à la scène

Cliquez avec le bouton droit sur un emplacement vide dans la fenêtre Hierarchy et sélectionnez **3D Object** > **Cube** pour ajouter un cube à votre scène :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step2-1.png)

Avec l’objet **Cube** sélectionné, dans la fenêtre **Inspector** :

* Changez la valeur **Position** de sa transformation de sorte qu’il se trouve près du bouton enfonçable, mais sans le chevaucher, par exemple x = 0, y = 0,04 et z = 0,5
* Changez la valeur **Scale** de sa transformation en une taille appropriée, par exemple x = 0,02, y = 0,02 et z = 0,02

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step2-2.png)

### <a name="3-configure-the-interactableonpressreceiver-event-type"></a>3. Configurer le type d’événement InteractableOnPressReceiver

Dans la fenêtre Hierarchy, sélectionnez l’objet **PressableButtonHoloLens2** puis, dans le **menu hamburger** de la fenêtre **Inspector**, sélectionnez **Collapse All Components** pour avoir une vue d’ensemble de tous les composants sur cet objet :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-1.png)

Développez le composant **Interactable (Script)** , puis localisez et développez la section **Events** > **Receivers** :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-2.png)

Cliquez sur le bouton **Add Event** pour créer un récepteur d’événements avec **InteractableOnPressReceiver** comme Event Receiver Type :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-3.png)

> [!NOTE]
> Le Event Receiver Type nommé InteractableOnPressReceiver permet au bouton de répondre à un événement d’appui quand une main suivie appuie sur le bouton.

Pour le récepteur d’événements nouvellement créé, changez **Interaction Filter** en **Near and Far** :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step3-4.png)

### <a name="4-configure-the-cube-to-receive-the-on-press-event"></a>4. Configurer le cube pour recevoir l’événement On Press

Dans la fenêtre Hierarchy, **cliquez et faites glisser** le **Cube** dans le champ de l’objet **Event Properties** pour l’événement **On Press ()** pour affecter le Cube comme récepteur de l’événement On Press () :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step4-1.png)

### <a name="5-define-the-action-to-be-triggered-by-the-on-press-event"></a>5. Définir l’action à déclencher par l’événement On Press

Cliquez sur la liste déroulante des actions, actuellement définie sur **No Function**, puis sélectionnez **MeshRenderer** > **Material material** pour définir la propriété Material du cube comme devant changer quand l’événement On Press () est déclenché :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-1.png)

Cliquez sur la petite icône de **cercle** en regard du champ Material, actuellement défini sur **None (Material)** , pour ouvrir la fenêtre Select Material :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-2.png)

Dans la fenêtre Select Material, **recherchez** **MRTK_Standard** et sélectionnez un matériau approprié, par exemple **MRTK_Standard_Cyan**, pour que la couleur du cube change en cyan quand le bouton est enfoncé :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step5-3.png)

### <a name="6-configure-the-cube-to-receive-the-on-release-event"></a>6. Configurer le cube pour recevoir l’événement On Release

**Répétez** l’étape 4 pour l’événement On Release afin d’affecter le **Cube**  comme récepteur de l’événement **On Release ()** .

### <a name="7-define-the-action-to-be-triggered-by-the-on-release-event"></a>7. Définir l’action à déclencher par l’événement On Release

**Répétez** l’étape 5 pour l’événement On Release, mais choisissez le matériau **MRTK_Standard_LightGray** pour que la couleur du cube retourne à sa couleur gris clair d’origine quand le bouton est relâché :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step7-1.png)

### <a name="8-test-the-button-using-the-in-editor-simulation"></a>8. Tester le bouton en utilisant la simulation dans l’éditeur

Appuyez sur le bouton **Play** pour entrer en mode Game et utilisez la simulation d’entrée de l’éditeur pour tester le bouton nouvellement configuré.

Bouton non enfoncé (barre d’espace + molette de défilement de la souris vers l’arrière) :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step8-1.png)

Bouton enfoncé (barre d’espace + molette de défilement de la souris vers l’avant) :

![mrlearning-base](images/mrlearning-base/tutorial2-section2-step8-2.png)

> [!TIP]
> Pour découvrir comment utiliser la simulation d’entrée dans l’éditeur, consultez le guide [Utilisation de la simulation d’entrée avec les mains dans l’éditeur pour tester une scène](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html#using-the-in-editor-hand-input-simulation-to-test-a-scene) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="creating-a-panel-of-buttons-using-mrtks-grid-object-collection"></a>Création d’un panneau de boutons avec l’outil Grid Object Collection du MRTK

Dans cette section, vous allez découvrir comment aligner automatiquement plusieurs boutons dans une interface utilisateur bien ordonnée en utilisant l’outil Grid Object Collection du MRTK.

Cet exemple vous montre comment créer un panneau avec cinq boutons alignés horizontalement. Vous pouvez cependant suivre ces mêmes principes pour créer d’autres dispositions.

Voici les principales étapes à suivre pour y parvenir :

1. Rattacher les objets Button à un objet parent
2. Ajouter et configurer le composant Grid Object Collection (Script)
3. Tester les boutons en utilisant la simulation dans l’éditeur

### <a name="1-parent-the-button-objects-to-a-parent-object"></a>1. Rattacher les objets Button à un objet parent

Cliquez avec le bouton droit sur un emplacement vide dans la fenêtre Hierarchy et sélectionnez **Create Empty** :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-1.png)

Cliquez avec le bouton droit sur l’objet nouvellement créé, sélectionnez **Rename**et donnez-lui un nom approprié, par exemple **ButtonCollection** :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-2.png)

Sélectionnez l’objet **PressableButtonHoloLens2** et **faites-le glisser** au-dessus de l’objet **ButtonCollection** pour en faire un enfant de l’objet ButtonCollection :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-3.png)

Cliquez avec le bouton droit sur l’objet **PressableButtonHoloLens2** et sélectionnez **Duplicate** pour en créer une copie :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step1-4.png)

**Répétez** cette étape quatre fois, jusqu’à avoir un total de cinq objets PressableButtonHoloLens2.

### <a name="2-add-and-configure-the-grid-object-collection-script-component"></a>2. Ajouter et configurer le composant Grid Object Collection (Script)

Avec l’objet ButtonCollection sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, cliquez sur le bouton **Add Component**, puis recherchez et sélectionnez **Grid Object Collection** pour ajouter un composant Grid Object Collection (Script) à l’objet ButtonCollection :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-1.png)

Configurez le composant Grid Object Collection (Script) comme suit :

* Changez **Num Rows** en 1 pour que tous les boutons soient alignés sur une même ligne
* Changez **Cell Width** en 0,05 pour espacer les boutons dans la ligne

Cliquez ensuite sur le bouton **Update Collection** pour appliquer la nouvelle configuration :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-2.png)

> [!NOTE]
> Les modifications de configuration que vous venez d’appliquer représentent les modifications minimales nécessaires pour atteindre l’objectif de placer les boutons sur une même ligne. Cependant, dans les projets futurs, en fonction de facteurs tels que par exemple l’orientation des objets parents et enfants, vous devrez peut-être ajuster d’autres paramètres, comme par exemple le type d’orientation. Pour plus d’informations sur le composant Grid Object Collection de MRTK, vous pouvez consulter le guide [Object collection scripts](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html#object-collection-scripts) dans le [portail de documentation de MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

Avec l’objet ButtonCollection sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, changez la valeur **Position** de la transformation de l’objet ButtonCollection de sorte que ses objets de boutons enfants soient positionnés devant la caméra, qui est elle-même positionnée à l’origine, par exemple x = 0, y = 0 et z = 0,5 :

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step2-3.png)

> [!NOTE]
> Quand vous avez ajouté pour la première fois le préfabriqué PressableButtonHoloLens2 à la scène dans la section [Gestes de suivi de la main et boutons d’interaction](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) ci-dessus, vous l’avez positionné devant la caméra. Cependant, comme Grid Object Collection contrôle la position de ses objets enfants immédiats, la position Z des objets enfants de PressableButtonHoloLens2 est réinitialisée à 0 en fonction de la distance par défaut de Grid Object Collection par rapport à la valeur 0 du parent. C’est la raison pour laquelle, en plus de conserver la relation de position parent/enfants organisée, nous avons déplacé la position de l’objet ButtonCollection parent vers l’avant, au lieu de configurer la distance à partir de la valeur du parent pour déplacer les objets enfants PressableButtonHoloLens2 vers l’avant.

### <a name="3-test-the-buttons-using-the-in-editor-simulation"></a>3. Tester les boutons en utilisant la simulation dans l’éditeur

Appuyez sur le bouton Play pour entrer en mode Game et utilisez la simulation d’entrée de l’éditeur pour tester chacun des boutons de votre panneau de boutons nouvellement créé.

![mrlearning-base](images/mrlearning-base/tutorial2-section3-step3-1.png)

> [!TIP]
> Actuellement, quand vous appuyez sur un des cinq boutons, la couleur du cube devient cyan. Pour rendre l’expérience plus intéressante, utilisez ce que vous venez d’apprendre pour configurer chaque bouton pour que le cube soit affiché dans une autre différente.

## <a name="adding-text-into-your-scene"></a>Ajout de texte dans votre scène

Dans cette section, vous allez découvrir comment ajouter du texte à vos expériences de réalité mixte en utilisant TextMesh Pro d’Unity, que vous avez préparé dans la section [Importer les ressources essentielles TextMesh Pro](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources) du tutoriel précédent.

Dans cet exemple, vous allez ajouter une étiquette simple sous la collection de boutons que vous avez créée dans la section précédente.

Cliquez avec le bouton droit sur l’objet ButtonCollection, puis sélectionnez **3D Object** > **Text - TextMeshPro** pour créer un objet TextMeshPro en tant qu’enfant de l’objet ButtonCollection :

![mrlearning-base](images/mrlearning-base/tutorial2-section4-step1-1.png)

Sélectionnez l’objet TextMeshPro nommé Text (TMP) que vous venez de créer puis, dans la fenêtre Inspector, changez sa position et sa taille pour que l’étiquette soit placée sous la collection de boutons, par exemple :

* Changez la valeur **Pos Y** de Rect Transform en -0,0425.
* Changez la valeur **Width** de Rect Transform en 0,24.
* Changez la valeur **Height** de Rect Transform en 0,024.

Ensuite, changez le texte de façon à refléter l’objectif de l’étiquette et choisissez les propriétés de la police pour que le texte tienne dans l’étiquette, par exemple :

* Changez la valeur **Text** de Text Mesh Pro (Script) en Button Collection
* Changez la valeur **Font Style** de Text Mesh Pro (Script) en Bold.
* Changez la valeur **Font Size** de Text Mesh Pro (Script) en 0,2.
* Changez la valeur **Alignment** de Text Mesh Pro (Script) en Center and Middle.

![mrlearning-base](images/mrlearning-base/tutorial2-section4-step1-2.png)

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez découvert comment cloner, personnaliser et configurer un paramètre de profil MRTK. Vous avez également découvert comment interagir avec des boutons pour déclencher des événements en utilisant des mains suivies sur HoloLens 2. Enfin, vous avez découvert comment créer une interface utilisateur simple avec le composant Grid Object Collection du MRTK et le Text Mesh Pro d’Unity.

[Tutoriel suivant : 4. Placement du contenu dynamique et utilisation de solveurs](mrlearning-base-ch3.md)
