---
title: Didacticiels de mise en route-5. Interaction avec les objets 3D
description: ''
author: jessemcculloch
ms.author: jemccull
ms.date: 05/02/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: a1b26d56b4693ef23f2d77ba53e0961693489a3a
ms.sourcegitcommit: cc61f7ac08f9ac2f2f04e8525c3260ea073e04a7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77130262"
---
# <a name="5-interacting-with-3d-objects"></a>5. interaction avec les objets 3D

Dans ce didacticiel, vous allez découvrir le contenu 3D de base et l’expérience utilisateur, tels que l’Organisation des objets 3D dans le cadre d’une collection, des zones englobantes pour la manipulation de base, l’interaction proche et éloignée, et les gestes tactiles et de manipulation avec le suivi de la main.

## <a name="objectives"></a>Objectifs

* Créer un panneau d’objets 3D qui sera utilisé pour les autres objectifs de formation
* Implémenter des cadres englobants
* Configurer des objets 3D pour des manipulations de base telles que déplacer, faire pivoter et mettre à l’échelle
* Explorer l’interaction de près et de loin
* En savoir plus sur les gestes supplémentaires de suivi de la main, tels que la manipulation et la saisie tactile

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du didacticiel

Téléchargez et importez le package personnalisé Unity :

* [MRTK. HoloLens2. Unity. Tutorials. Assets. GettingStarted. 2.2.0.0. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.2.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.2.0.0.unitypackage)

Une fois que vous avez importé les ressources du didacticiel, votre fenêtre de projet doit ressembler à ceci :

![mrlearning-base](images/mrlearning-base/tutorial4-section1-step1-1.png)

> [!TIP]
> Pour obtenir un rappel sur l’importation d’un package personnalisé Unity, vous pouvez vous reporter aux instructions [importez les instructions de la réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) .

## <a name="decluttering-the-scene-view"></a>Désencombrement de la vue scène

Pour faciliter l’utilisation de votre scène, définissez la visibilité des **scènes** pour les objets cube et ButtonCollection sur désactivé en cliquant sur l’icône représentant un **œil** à gauche des objets. Cela masque l’objet dans la fenêtre de scène sans modifier sa visibilité dans le jeu :

![mrlearning-base](images/mrlearning-base/tutorial4-section2-step1-1.png)

> [!TIP]
> Pour en savoir plus sur les contrôles de visibilité des scènes et sur la façon dont vous pouvez les utiliser pour optimiser l’affichage et le flux de travail de votre scène, vous pouvez consulter la documentation sur la <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">visibilité des scènes</a> d’Unity.

## <a name="organizing-3d-objects-in-a-collection"></a>Organisation d’objets 3D dans une collection

Dans cette section, vous allez créer un panneau d’objets 3D que vous allez utiliser pour explorer les différentes façons d’interagir avec les objets 3D dans les sections suivantes de ce didacticiel. Plus précisément, vous configurez les objets 3D de manière à ce qu’ils soient positionnés sur une grille 3 x 3.

De la même façon que lorsque vous avez [créé un panneau de boutons](mrlearning-base-ch2.md#creating-a-panel-of-buttons-using-mrtks-grid-object-collection), les principales étapes à suivre pour y parvenir sont les suivantes :

1. Parent des objets 3D à un objet parent
2. Ajouter et configurer le composant de collection d’objets Grid (script)

### <a name="1-parent-the-3d-objects-to-a-parent-object"></a>1. parent des objets 3D à un objet parent

Dans la fenêtre hiérarchie, **créez un objet vide**, donnez-lui un nom approprié, par exemple, **3DObjectCollection**, et positionnez-le à un emplacement approprié, par exemple, X = 0, Y =-0,2, Z = 2.

Dans la fenêtre projet, accédez à **ressources** > **MRTK. Tutoriels. GettingStarted** > **Prefabs**, **puis le Prefabs suivant au** **3DObjectCollection**:

* Fromage
* CoffeeCup
* EarthCore
* Octa
* Platoniques
* TheModule

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-1.png)

Dans la fenêtre hiérarchie, **créez trois cubes** en tant qu’objets enfants du **3DObjectCollection** et définissez leur **échelle** de transformation sur X = 0,15, Y = 0,15, Z = 0,15 :

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-2.png)

<!-- TODO: Finish -->
> [!TIP]
> Pour obtenir un rappel sur la procédure à suivre pour effectuer les étapes décrites ci-dessus, vous pouvez consulter le didacticiel Création de l' [interface utilisateur et configuration de la réalité mixte](mrlearning-base-ch2.md) .

Repositionnez les cubes afin de voir chaque cube :

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-3.png)

Dans la fenêtre projet, accédez à **ressources** > **MixedRealityToolkit. SDK** > **StandardAssets** > **matériaux** pour voir les matériaux fournis avec MRTK.

**Cliquez et faites glisser** un matériau approprié sur la propriété de **l’élément 0** du convertisseur de maillage de chaque cube, par exemple :

* MRTK_Standard_GlowingCyan
* MRTK_Standard_GlowingOrange
* MRTK_Standard_Green :

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step1-4.png)

### <a name="2-add-and-configure-the-grid-object-collection-script-component"></a>2. Ajouter et configurer le composant collection d’objets Grid (script)

Ajoutez un composant de **collection d’objets Grid (script)** à l’objet 3DObjectCollection et configurez-le comme suit :

* Changez le **type de tri** en ordre enfant pour vous assurer que les objets enfants sont triés dans l’ordre dans lequel vous les avez placés sous l’objet parent

Cliquez ensuite sur le bouton **mettre à jour la collection** pour appliquer la nouvelle configuration :

![mrlearning-base](images/mrlearning-base/tutorial4-section3-step2-1.png)

## <a name="manipulating-3d-objects"></a>Manipulation d’objets 3D

Dans cette section, vous allez ajouter la possibilité de manipuler tous les objets 3D dans le panneau que vous avez créé dans la section précédente. En outre, pour les objets Prefab, vous permettez aux utilisateurs d’accéder à ces objets et de les saisir avec des mains suivies. Vous allez ensuite explorer quelques comportements de manipulation que vous pouvez appliquer à vos objets.

Voici les principales étapes à suivre pour y parvenir :

1. Ajouter le composant de gestionnaire de manipulation (script) à tous les objets
2. Ajouter le composant de script (script) à proximité des objets Prefab
3. Configurer le composant de gestionnaire de manipulation (script)

> [!IMPORTANT]
> Pour pouvoir **manipuler un objet**, l’objet doit avoir les composants suivants :
>
> * Composant de **collision** , par exemple, un conflit de boîte
> * Composant du **Gestionnaire de manipulation (script)**
>
> Pour pouvoir **manipuler** et **récupérer un objet avec des mains suivies**, l’objet doit avoir les composants suivants :
>
> * Composant de **collision** , par exemple, un conflit de boîte
> * Composant du **Gestionnaire de manipulation (script)**
> * Composant **de script (script) à proximité d’interaction**

### <a name="1-add-the-manipulation-handler-script-component-to-all-the-objects"></a>1. ajouter le composant de gestionnaire de manipulation (script) à tous les objets

Dans la fenêtre hiérarchie, sélectionnez l’objet **fromage** , maintenez la touche **MAJ** enfoncée, puis sélectionnez l’objet **cube ()** et ajoutez le composant **Gestionnaire de manipulation (script)** à tous les objets :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step1-1.png)

> [!NOTE]
> Dans le cadre de ce didacticiel, les conflits ont déjà été ajoutés à prefabs. Pour les primitives Unity, telles que les objets cube, le composant de conflit est automatiquement ajouté lors de la création de l’objet. Dans l’image ci-dessus, les conflits sont représentés par les contours verts. Pour en savoir plus sur les conflits, vous pouvez consulter la documentation sur les <a href="https://docs.unity3d.com/Manual/CollidersOverview.html" target="_blank">conflits</a> d’Unity.

### <a name="2-add-the-near-interaction-grabbable-script-component-to-the-prefab-objects"></a>2. ajouter le composant de script (script) à proximité des objets Prefab

Dans la fenêtre hiérarchie, sélectionnez l’objet **fromage** , maintenez la touche **MAJ** enfoncée, puis sélectionnez l’objet **TheModule** et ajoutez le composant de script à **proximité d’interaction** à tous les objets :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step2-1.png)

### <a name="3-configure-the-manipulation-handler-script-component"></a>3. configurer le composant Gestionnaire de manipulation (script)

#### <a name="default-manipulation"></a>Manipulation par défaut

Pour l’objet **cube** , laissez toutes les propriétés par défaut pour connaître le comportement de manipulation par défaut :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-1.png)

> [!TIP]
> Pour rétablir les valeurs par défaut d’un composant, vous pouvez sélectionner l’icône des paramètres du composant, puis sélectionner réinitialiser.

#### <a name="restrict-manipulation-to-scale-only"></a>Limiter la manipulation à l’échelle uniquement

Pour l’objet **cube (1)** , modifiez **deux types de manipulations de type droitier** pour que l’utilisateur n’autorise que la modification de la taille de l’objet :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-2.png)

#### <a name="constrain-the-movement-to-a-fixed-distance-from-the-user"></a>Contraindre le mouvement à une distance fixe de l’utilisateur

Pour l’objet **cube (2)** , modifiez la **contrainte de déplacement** pour corriger distance à partir de Head afin que, lorsque l’objet est déplacé, il reste à la même distance de l’utilisateur :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-3.png)

#### <a name="default-grabbable-manipulation"></a>Manipulation par défaut de l’option d’accrochage

Pour les objets **fromage**, **CoffeCup**et **EarthCore** , laissez toutes les propriétés par défaut pour connaître le comportement de manipulation par défaut :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-4.png)

#### <a name="remove-the-ability-of-far-manipulation"></a>Supprimer la capacité de manipulation lointaine

Pour l’objet **octa** , désactivez la case à cocher **autoriser la manipulation lointaine** pour que l’utilisateur puisse interagir uniquement avec l’objet directement à l’aide des mains suivies :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-5.png)

#### <a name="make-an-object-rotate-around-its-center"></a>Faire pivoter un objet autour de son centre

Pour l’objet **platoniques** , modifiez le **mode de rotation d’un côté** vers le bas et le mode de rotation d' **un seul** côté pour faire pivoter le centre d’objets pour le faire ainsi lorsque l’utilisateur fait pivoter l’objet d’une main, il pivote autour du centre de l’objet :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-6.png)

#### <a name="prevent-movement-after-object-is-released"></a>Empêcher le déplacement après la libération de l’objet

Pour l’objet **TheModule** , remplacez le **comportement Release** par Nothing afin qu’une fois que l’objet est libéré de la main de l’utilisateur, il ne continue pas à se déplacer :

![mrlearning-base](images/mrlearning-base/tutorial4-section4-step3-7.png)

Pour en savoir plus sur le composant de gestionnaire de manipulation et ses propriétés associées, vous pouvez consulter le Guide du [Gestionnaire de manipulation](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html) dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="adding-bounding-boxes"></a>Ajouter des zones englobantes

Les rectangles englobants facilitent et simplifient la manipulation d’objets avec une main pour une interaction proche et éloignée en fournissant des poignées qui peuvent être utilisées pour la mise à l’échelle et la rotation.

Dans cet exemple, vous allez ajouter un cadre englobant à l’objet EarthCore pour que cet objet puisse être manipulé avec l’utilisation de la manipulation d’objets que vous avez configurée dans la section précédente, ainsi que pour la mise à l’échelle et la rotation à l’aide des poignées de cadre englobant.

> [!IMPORTANT]
> Pour pouvoir utiliser un **cadre englobant**, l’objet doit avoir les composants suivants :
>
> * Composant de **collision** , par exemple, un conflit de boîte
> * Composant **de cadre englobant (script)**

### <a name="1-add-the-bounding-box-script-component-to-the-earthcore-object"></a>1. ajouter le composant de cadre englobant (script) à l’objet EarthCore

Dans la fenêtre de l’inspecteur, sélectionnez l’objet **EarthCore** et ajoutez le composant de cadre **englobant (script)** à l’objet EarthCore :

![mrlearning-base](images/mrlearning-base/tutorial4-section5-step1-1.png)

> [!NOTE]
> Les visualisations de cadre englobant sont créées au moment de l’exécution et ne sont donc pas visibles avant l’entrée en mode jeu.

### <a name="2-visualize-and-test-the-bounding-box-using-the-in-editor-simulation"></a>2. Visualisez et testez le cadre englobant à l’aide de la simulation dans l’éditeur

Appuyez sur le bouton lecture pour passer en mode jeu. Appuyez sur la barre d’espace et maintenez-la enfoncée pour afficher la main et utilisez la souris pour interagir avec le cadre englobant :

![mrlearning-base](images/mrlearning-base/tutorial4-section5-step2-1.png)

Pour en savoir plus sur le composant de cadre englobant et ses propriétés associées, vous pouvez consulter le Guide du cadre [englobant](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="adding-touch-effects"></a>Ajout d’effets tactiles

Dans cet exemple, vous allez activer les événements à déclencher lorsque vous touchez un objet à votre main. Plus précisément, vous allez configurer l’objet octa pour qu’il émette un effet sonore lorsque l’utilisateur le touche.

Voici les principales étapes à suivre pour y parvenir :

1. Ajouter un composant source audio à l’objet
2. Ajouter le composant touchable (script) near interaction à l’objet
3. Ajouter le composant tactile d’interaction manuelle (script) à l’objet
4. Implémenter l’événement on Touch Started
5. Tester l’interaction tactile à l’aide de la simulation dans l’éditeur

> [!IMPORTANT]
> Pour pouvoir déclencher des **événements tactiles**, l’objet doit avoir les composants suivants :
>
> * Composant de **collision** , de préférence un conflit de Box
> * Composant **touchable (script) near interaction**
> * Composant **Touch interaction tactile (script)**

> [!NOTE]
> Le composant Touch interaction tactile (script) ne fait pas partie de MRTK. Il a été importé avec les ressources de ce didacticiel et faisait partie à l’origine des exemples d’Unity MixedReality Toolkit.

### <a name="1-add-an-audio-source-component-to-the-object"></a>1. Ajouter un composant audio source à l’objet

Dans la fenêtre hiérarchie, sélectionnez l’objet **octa** , ajoutez un composant **audio source** à l’objet octa, puis remplacez **spatial Blend** par 1 pour activer l’audio spatial :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step1-1.png)

### <a name="2-add-the-near-interaction-touchable-script-component-to-the-object"></a>2. ajouter le composant touchable (script) near-interaction à l’objet

L’objet **octa** étant toujours sélectionné, ajoutez le composant **touchable (script) near-interaction** à l’objet octa, puis cliquez sur les boutons **corriger les limites** et le centre de **Correction** pour mettre à jour les propriétés du centre local et des limites du touchable d’interaction Near (script) pour qu’elles correspondent à la BoxCollider :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step2-1.png)

### <a name="3-add-the-hand-interaction-touch-script-component-to-the-object"></a>3. ajouter le composant tactile d’interaction manuelle (script) à l’objet

Avec l’objet **octa** toujours sélectionné, ajoutez le composant **Touch interaction tactile (script)** à l’objet octa :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step3-1.png)

### <a name="4-implement-the-on-touch-started-event"></a>4. implémenter l’événement on Touch Started

Sur le composant Touch interaction tactile (script), cliquez sur l’icône de petite **+** pour créer un événement **on Touch Started ()** . Configurez ensuite l’objet **octa** pour recevoir l’événement et définissez **audiosource. PlayOneShot** comme action à déclencher :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step4-1.png)

Accédez à **ressources** > **MixedRealityToolkit. SDK** > **StandardAssets** > matériaux pour voir les clips audio fournis avec le MRTK, puis attribuez un clip audio approprié au champ de **clip audio** , par exemple, le clip audio MRTK_Gem :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step4-2.png)

> [!TIP]
> Pour obtenir un rappel sur la façon d’implémenter des événements, vous pouvez consulter les instructions de suivi de la [main et les boutons](mrlearning-base-ch2.md#hand-tracking-gestures-and-interactable-buttons) interactifs.

### <a name="5-test-the-touch-interaction-using-the-in-editor-simulation"></a>5. test de l’interaction tactile à l’aide de la simulation dans l’éditeur

Appuyez sur le bouton lecture pour passer en mode jeu. Appuyez sur la barre d’espace et maintenez-la enfoncée pour afficher la main et utilisez la souris pour toucher l’objet octa et déclencher l’effet sonore :

![mrlearning-base](images/mrlearning-base/tutorial4-section6-step5-1.png)

> [!NOTE]
> Comme vous l’avez vu lors du test de l’interaction tactile, et comme indiqué dans l’image ci-dessus, l’objet octa Color pulsated alors qu’il a été touché. Cet effet est codé en dur dans le composant Touch interaction tactile (script) et non pas dans la configuration d’événement que vous avez effectuée dans les étapes ci-dessus.
>
> Si vous souhaitez désactiver cet effet, vous pouvez, par exemple, mettre en commentaire ou ligne 32 « TargetRenderer = GetComponentInChildren<Renderer>(); », ce qui a pour effet que le TargetRenderer reste null et que la couleur n’est pas Pulsating.

## <a name="congratulations"></a>Félicitations

Dans ce didacticiel, vous avez appris à organiser les objets 3D dans une collection de grilles et à manipuler ces objets (mise à l’échelle, rotation et déplacement) à l’aide de Near interaction (saisie directe des mains) et de l’interaction lointaine (à l’aide de rayons ou de rayons main). Vous avez également appris à placer des zones englobantes autour des objets 3D et appris à utiliser et à personnaliser les poignées sur les zones englobantes. Enfin, vous avez découvert comment déclencher des événements quand l’utilisateur touche un objet.

[Leçon suivante : 6. exploration des options d’entrée avancées](mrlearning-base-ch5.md)
