---
title: Tutoriels de démarrage - 5. Interaction avec les objets 3D
description: Découvrez plus d’informations sur le contenu 3D de base et les expériences utilisateur, comme l’organisation des objets 3D et des zones englobantes pour la manipulation de base.
author: jessemcculloch
ms.author: jemccull
ms.date: 05/02/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 65bcef6a7c10450816d7a928302b0b266b132f0f
ms.sourcegitcommit: 536fd45b48a70bbeca1454cef517ae007225e533
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80362072"
---
# <a name="5-interacting-with-3d-objects"></a>5. Interaction avec les objets 3D

Dans ce tutoriel, vous allez découvrir des informations sur les objets 3D de base et l’expérience utilisateur, comme l’organisation des objets 3D dans le cadre d’une collection, les cadres englobants pour la manipulation de base, l’interaction de près et de loin, les gestes tactiles et de préhension avec le suivi de la main.

## <a name="objectives"></a>Objectifs

* Créer un panneau d’objets 3D qui sera utilisé pour les autres objectifs d’apprentissage
* Implémenter des cadres englobants
* Configurer des objets 3D pour la manipulation de base, comme le déplacement, la rotation et la mise à l’échelle
* Explorer l’interaction de près et de loin
* Découvrir des informations sur les gestes de suivi de la main, comme la préhension et l’interaction tactile

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du tutoriel

Téléchargez et importez le package personnalisé Unity :

* [MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.2/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage)

Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :

![mrlearning-base](images/mrlearning-base/tutorial4-section1-step1-1.png)

> [!TIP]
> Pour un rappel de la façon d’importer un package personnalisé Unity, vous pouvez vous référer aux instructions de [Importer le Kit de ressources de réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit).

## <a name="decluttering-the-scene-view"></a>Désencombrement de la vue Scène

Pour faciliter l’utilisation de votre scène, définissez **Scene visibility** pour les objets **Cube** et **ButtonCollection** sur Off en cliquant sur l’icône d’**œil** à gauche des objets. Ceci masque l’objet dans la fenêtre Scene sans modifier sa visibilité dans le jeu :

![mrlearning-base](images/mrlearning-base/tutorial4-section2-step1-1.png)

> [!TIP]
> Pour en savoir plus sur les contrôles de visibilité de la scène et sur la façon dont vous pouvez les utiliser pour optimiser l’affichage et le workflow de votre scène, vous pouvez consulter la documentation <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> d’Unity.

## <a name="organizing-3d-objects-in-a-collection"></a>Organisation des objets 3D dans une collection

Dans cette section, vous allez créer un panneau d’objets 3D que vous allez utiliser pour explorer les différentes façons d’interagir avec les objets 3D dans les sections suivantes de ce tutoriel. Plus précisément, vous allez configurer les objets 3D de manière à ce qu’ils soient positionnés sur une grille 3 x 3.

De la même façon que quand vous avez [créé un panneau de boutons](mrlearning-base-ch2.md#creating-a-panel-of-buttons-using-mrtks-grid-object-collection), les principales étapes à suivre pour y parvenir sont les suivantes :

1. Rattacher les objets 3D à un objet parent
2. Ajouter et configurer le composant Grid Object Collection (Script)

### <a name="1-parent-the-3d-objects-to-a-parent-object"></a>1. Rattacher les objets 3D à un objet parent

Dans la fenêtre Hierarchy, **créez un objet vide**, donnez-lui un nom approprié, par exemple **3DObjectCollection** et le positionnez-le à un emplacement approprié, par exemple X = 0 ; Y = -0,2 ; Z = 2.

Dans la fenêtre Project, accédez à **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs**, puis **rattachez** les préfabriqués suivants à **3DObjectCollection** :

* Cheese
* CoffeeCup
* EarthCore
* Octa
* Platonic
* TheModule

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-1.png)

Dans la fenêtre Hierarchy, **créez trois cubes** en tant qu’objets enfants de **3DObjectCollection** et définissez la valeur **Scale** de leur transformation sur X = 0,15 ; Y = 0,15 ; Z = 0,15 :

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-2.png)

> [!TIP]
> Pour un rappel de la façon d’effectuer les étapes listées ci-dessus, vous pouvez vous référer au tutoriel [Création de l’interface utilisateur et configuration du kit d’outils de réalité mixte](mrlearning-base-ch2.md).

Repositionnez les cubes de façon à voir chaque cube :

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-3.png)

Dans la fenêtre Project, accédez à **Assets** > **MixedRealityToolkit.SDK** > **StandardAssets** > **Materials** pour voir les matériaux fournis par le MRTK.

**Cliquez et faites glisser** un matériau approprié sur la propriété Mesh Renderer **Materials** Element 0 de chaque cube, par exemple :

* MRTK_Standard_GlowingCyan
* MRTK_Standard_GlowingOrange
* MRTK_Standard_Green

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-4.png)

### <a name="2-add-and-configure-the-grid-object-collection-script-component"></a>2. Ajouter et configurer le composant Grid Object Collection (Script)

Ajoutez un composant **Grid Object Collection (Script)** à l’objet **3DObjectCollection** et configurez-le comme suit :

* Changez **Sort Type** en **Child Order** pour que les objets enfants soient triés dans l’ordre où vous les avez placés sous l’objet parent.

Cliquez ensuite sur le bouton **Update Collection** pour appliquer la nouvelle configuration :

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step2-1.png)

## <a name="manipulating-3d-objects"></a>Manipulation d’objets 3D

Dans cette section, vous allez ajouter la possibilité de manipuler tous les objets 3D dans le panneau que vous avez créé dans la section précédente. En outre, pour les objets préfabriqués, vous allez permettre aux utilisateurs d’accéder à ces objets et de les saisir avec des mains suivies. Vous allez ensuite explorer quelques comportements de manipulation que vous pouvez appliquer à vos objets.

Voici les principales étapes à suivre pour y parvenir :

1. Ajouter le composant Manipulation Handler (Script) à tous les objets
2. Ajouter le composant Near Interaction Grabbable (Script) aux objets préfabriqués
3. Configurer le composant Manipulation Handler (Script)

> [!IMPORTANT]
> Pour pouvoir **manipuler un objet**, celui-ci doit avoir les composants suivants :
>
> * Le composant **Collider**, par exemple un Box Collider
> * Le composant **Manipulation Handler (Script)**
>
> Pour pouvoir **manipuler** et **saisir** un objet avec les mains suivies, celui-ci doit avoir les composants suivants :
>
> * Le composant **Collider**, par exemple un Box Collider
> * Le composant **Manipulation Handler (Script)**
> * Le composant **Near Interaction Grabbable (Script)**

### <a name="1-add-the-manipulation-handler-script-component-to-all-the-objects"></a>1. Ajouter le composant Manipulation Handler (Script) à tous les objets

Dans la fenêtre Hierarchy, sélectionnez l’objet **Cheese**, maintenez la touche **Maj** enfoncée, puis sélectionnez l’objet **Cube () 2** et ajoutez le composant **Manipulation Handler (Script)** à tous les objets :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step1-1.png)

> [!NOTE]
> Dans le cadre de ce tutoriel, les colliders ont déjà été ajoutés aux objets préfabriqués. Pour les primitives Unity, comme les objets Cube, le composant Collider est automatiquement ajouté lors de la création de l’objet. Dans l’image ci-dessus, les colliders sont représentés par les contours verts. Pour plus d’informations sur les colliders, vous pouvez consulter la documentation <a href="https://docs.unity3d.com/Manual/CollidersOverview.html" target="_blank">Collider</a> d’Unity.

### <a name="2-add-the-near-interaction-grabbable-script-component-to-the-prefab-objects"></a>2. Ajouter le composant Near Interaction Grabbable (Script) aux objets préfabriqués

Dans la fenêtre Hierarchy, sélectionnez l’objet **Cheese**, maintenez la touche **Maj** enfoncée, puis sélectionnez l’objet **TheModule** et ajoutez le composant **Near Interaction Grabbable (Script)** à tous les objets :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step2-1.png)

### <a name="3-configure-the-manipulation-handler-script-component"></a>3. Configurer le composant Manipulation Handler (Script)

#### <a name="default-manipulation"></a>Manipulation par défaut

Pour l’objet **Cube**, laissez toutes les propriétés à leurs valeurs par défaut pour expérimenter le comportement de manipulation par défaut :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-1.png)

> [!TIP]
> Pour rétablir les valeurs par défaut d’un composant, vous pouvez sélectionner l’icône Settings du composant, puis sélectionner Reset.

#### <a name="restrict-manipulation-to-scale-only"></a>Limiter la manipulation à la mise à l’échelle uniquement

Pour l’objet **Cube (1)** , changez **Two Handed Manipulation Type** en **Scale** pour autoriser l’utilisateur à seulement changer la taille de l’objet :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-2.png)

#### <a name="constrain-the-movement-to-a-fixed-distance-from-the-user"></a>Contraindre le mouvement à une distance fixe de l’utilisateur

Pour l’objet **Cube (2)** , changez **Constraint On Movement** en **Fix Distance From Head** pour que, quand l’objet est déplacé, il reste à la même distance de l’utilisateur :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-3.png)

#### <a name="default-grabbable-manipulation"></a>Manipulation de préhension par défaut

Pour les objets **Cheese**, **CoffeCup** et **EarthCore**, laissez toutes les propriétés à leurs valeurs par défaut pour expérimenter le comportement de manipulation de préhension par défaut :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-4.png)

#### <a name="remove-the-ability-of-far-manipulation"></a>Supprimer la possibilité de manipulation de loin

Pour l’objet **Octa**, décochez la case **Allow Far Manipulation** pour que l’utilisateur puisse interagir avec l’objet seulement en utilisant les mains suivies :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-5.png)

#### <a name="make-an-object-rotate-around-its-center"></a>Faire pivoter un objet autour de son centre

Pour l’objet **Platonic**, changez **One Hand Rotation Mode Near** et **One Hand Rotation Mode Far** en **Rotate About Object Center** pour que, quand l’utilisateur fait pivoter l’objet avec une main, il pivote autour de son centre :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-6.png)

#### <a name="keep-movement-after-object-is-released"></a>Conserver le mouvement après que l’objet soit relâché

Pour l’objet **TheModule**, ajoutez un composant **Rigidbody** pour activer les lois de la physique, puis décochez **Use Gravity** pour que l’objet ne soit pas affecté par la gravité :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-7.png)

De retour dans le composant Manipulation Handler (Script), vérifiez que **Release Behavior** est défini à la fois sur **Keep Velocity** et **Keep Angular Velocity** afin qu’une fois que l’objet est relâché par la main de l’utilisateur, il continue à se déplacer :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-8.png)

Pour en savoir plus sur le composant Manipulation Handler et ses propriétés associées, vous pouvez consulter le guide [Manipulation handler](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="adding-bounding-boxes"></a>Ajout de cadres englobants

Les cadres englobants facilitent et rendent plus intuitive la manipulation d’objets avec une main pour l’interaction proche et de loin en fournissant des poignées qui peuvent être utilisées pour la mise à l’échelle et la rotation.

Dans cet exemple, vous allez ajouter un cadre englobant à l’objet EarthCore pour permettre l’interaction avec cet objet en utilisant la manipulation d’objet que vous avez configurée dans la section précédente ainsi que la mise à l’échelle et la rotation, avec les poignées du cadre englobant.

> [!IMPORTANT]
> Pour pouvoir utiliser un **cadre englobant**, l’objet doit avoir les composants suivants :
>
> * Le composant **Collider**, par exemple un Box Collider
> * Le composant **Bounding Box (Script)**

### <a name="1-add-the-bounding-box-script-component-to-the-earthcore-object"></a>1. Ajouter le composant Bounding Box (Script) à l’objet EarthCore

Dans la fenêtre Inspector, sélectionnez l’objet **EarthCore** et ajoutez le composant **Bounding Box (Script)** à l’objet EarthCore :

![mrlearning-base](images/mrlearning-base/tutorial4-section5-step1-1.png)

> [!NOTE]
> La visualisation des cadres englobants est créée au moment de l’exécution et n’est donc pas visible avant l’entrée en mode Game.

### <a name="2-visualize-and-test-the-bounding-box-using-the-in-editor-simulation"></a>2. Visualiser et tester le cadre englobant en utilisant la simulation dans l’éditeur

Appuyez sur le bouton Play pour entrer en mode Game. Appuyez ensuite sur la barre d’espace pour faire apparaître la main et utilisez la souris pour interagir avec le cadre englobant :

![mrlearning-base](images/mrlearning-base/tutorial4-section5-step2-1.png)

Pour plus d’informations sur le composant Bounding Box et ses propriétés associées, vous pouvez consulter le guide [Bounding Box](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="adding-touch-effects"></a>Ajout d’effets tactiles

Dans cet exemple, vous allez activer des événements à déclencher quand vous touchez un objet avec votre main. Plus précisément, vous allez configurer l’objet Octa pour qu’il émette un son quand l’utilisateur le touche.

Voici les principales étapes à suivre pour y parvenir :

1. Ajouter un composant Audio Source à l’objet
2. Ajouter le composant Near Interaction Touchable (Script) à l’objet
3. Ajouter le composant Hand Interaction Touch (Script) à l’objet
4. Implémenter l’événement On Touch Started
5. Tester l’interaction tactile en utilisant la simulation dans l’éditeur

> [!IMPORTANT]
> Pour pouvoir **déclencher des événements tactiles**, l’objet doit avoir les composants suivants :
>
> * Le composant **Collider**, de préférence un Box Collider
> * Le composant **Near Interaction Touchable (Script)**
> * Le composant **Hand Interaction Touch (Script)**

> [!NOTE]
> Le composant Hand Interaction Touch (Script) ne fait pas partie de MRTK. Il a été importé avec les ressources de ce tutoriel et faisait partie à l’origine des exemples de Unity MixedReality Toolkit.

### <a name="1-add-an-audio-source-component-to-the-object"></a>1. Ajouter un composant Audio Source à l’objet

Dans la fenêtre Hierarchy, sélectionnez l’objet **Octa**, ajoutez un composant **Audio Source** à l’objet Octa, puis définissez **Spatial Blend** sur 1 pour activer l’audio spatial :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step1-1.png)

### <a name="2-add-the-near-interaction-touchable-script-component-to-the-object"></a>2. Ajouter le composant Near Interaction Touchable (Script) à l’objet

Avec l’objet **Octa** sélectionné, ajoutez le composant **Near Interaction Touchable (Script)** à l’objet Octa, puis cliquez sur les boutons **Fix Bounds** et **Fix Center** pour mettre à jour les propriétés Center et Bounds de Near Interaction Touchable (Script) pour qu’elles correspondent au BoxCollider :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step2-1.png)

### <a name="3-add-the-hand-interaction-touch-script-component-to-the-object"></a>3. Ajouter le composant Hand Interaction Touch (Script) à l’objet

Avec l’objet **Octa** sélectionné, ajoutez le composant **Hand Interaction Touch (Script)** à l’objet Octa :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step3-1.png)

### <a name="4-implement-the-on-touch-started-event"></a>4. Implémenter l’événement On Touch Started

Sur le composant **Hand Interaction Touch (Script)** , cliquez sur la petite icône **+** pour créer un événement **On Touch Started ()** . Configurez ensuite l’objet **Octa** pour recevoir l’événement et définissez **AudioSource.PlayOneShot** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step4-1.png)

Accédez à **Assets** > **MixedRealityToolkit.SDK** > **StandardAssets** > **Audio** pour voir les clips audio fournis avec le MRTK, puis affectez un clip audio approprié au champ **Audio Clip**, par exemple le clip audio MRTK_Gem :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step4-2.png)

> [!TIP]
> Pour un rappel de la façon d’implémenter des événements, vous pouvez vous référer aux instructions de [Gestes de suivi de la main et boutons d’interaction](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons).

### <a name="5-test-the-touch-interaction-using-the-in-editor-simulation"></a>5. Tester l’interaction tactile en utilisant la simulation dans l’éditeur

Appuyez sur le bouton Play pour entrer en mode Game. Appuyez ensuite sur la barre d’espace et maintenez-la enfoncée pour faire apparaître la main, et utilisez la souris pour toucher l’objet Octa et déclencher l’effet sonore :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step5-1.png)

> [!NOTE]
> Comme vous l’avez vu lors du test de l’interaction tactile et comme illustré dans l’image ci-dessus, la couleur de l’objet Octa a subi un effet de pulsations alors qu’il était touché. Cet effet est codé en dur dans le composant Hand Interaction Touch (Script) et ne résulte pas de la configuration des événements que vous avez effectuée dans les étapes ci-dessus.
>
> Si vous voulez désactiver cet effet, vous pouvez par exemple mettre en commentaire la ligne 32 « TargetRenderer = GetComponentInChildren<Renderer>(); », ce qui fait que le TargetRenderer reste null et que la couleur ne subit pas l’effet de pulsations.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez découvert comment organiser des objets 3D dans une collection de grille et comment manipuler ces objets (mise à l’échelle, rotation et déplacement) en utilisant l’interaction de près (en saisissant directement avec les mains suivies) et l’interaction de loin (en utilisant des rayons de pointage du regard ou des rayons de main). Vous avez aussi découvert comment placer des cadres englobants autour des objets 3D, et comment utiliser et personnaliser les poignées sur les cadres englobants. Enfin, vous avez découvert comment déclencher des événements quand l’utilisateur touche un objet.

[Leçon suivante : 6. Exploration des options d’entrée avancées](mrlearning-base-ch5.md)
