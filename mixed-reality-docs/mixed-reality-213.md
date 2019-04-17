---
title: Entrée M. 213
description: Suivez ce didacticiel de codage à l’aide de Unity, Visual Studio et des casques IMMERSIFS pour connaître les détails de contrôleurs de mouvement.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, immersive, de mouvement contrôleur, academy, didacticiel
ms.openlocfilehash: 85449795a4fb3d182101cb5b4c4ce3fe85b009c0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596965"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-input-213-motion-controllers"></a>Entrée M. 213 : Contrôleurs de mouvement

Dans le monde de réalité mixte, les contrôleurs de mouvement ajoutent un autre niveau d’interactivité. Avec [contrôleurs de mouvement](motion-controllers.md), nous pouvons directement interagir avec des objets de façon plus naturelle, similaire à vos interactions physiques dans la vie réelle, augmentant immersion et raviront dans votre expérience d’application.

213 d’entrée M., nous allons explorer les événements d’entrée du contrôleur de mouvement en créant une expérience de peinture spatiale simple. Avec cette application, les utilisateurs peuvent peindre dans un espace tridimensionnel avec différents types de pinceaux et couleurs.

## <a name="topics-covered-in-this-tutorial"></a>Sujets abordés dans ce didacticiel

|![MixedReality213 Topic1](images/mr213-topic1.png)|![MixedReality213 Topic2](images/mr213-topic2.png)|![MixedReality213 Topic3](images/mr213-topic3.png)|
| :--- | :--- | :--- |
|**Visualisation du contrôleur**|**Événements d’entrée de contrôleur**|**Contrôleur personnalisé et l’interface utilisateur**|
|Découvrez comment afficher les modèles de contrôleur de mouvement dans le mode de jeu d’Unity et d’exécution.|Comprendre les différents types d’événements de bouton et de leurs applications.|Apprenez à superposer des éléments d’interface utilisateur sur le contrôleur ou de personnaliser entièrement.|

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>Entrée M. 213 : Contrôleurs de mouvement</td><td style="text-align: center;"> </td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

Consultez la liste de vérification d’installation pour des casques IMMERSIFS sur [cette page](install-the-tools.md).

* Ce didacticiel requiert [Unity 2017.2.1p2](https://beta.unity3d.com/download/1dc514532f08/UnityDownloadAssistant-2017.2.1p2.exe)

### <a name="project-files"></a>Fichiers projet

* [Télécharger les fichiers](https://github.com/Microsoft/MixedReality213/archive/master.zip) requise par le projet et extrayez les fichiers sur le bureau.

>[!NOTE]
>Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/MixedReality213).

## <a name="unity-setup"></a>Programme d’installation Unity

>[!VIDEO https://www.youtube.com/embed/cBAOALaHys4]

### <a name="objectives"></a>Objectifs

* Optimiser le développement de Unity pour Windows Mixed Reality
* Le programme d’installation de caméra de réalité mixte
* Environnement de configuration

### <a name="instructions"></a>Instructions

* Démarrez Unity.
* Sélectionnez **Open**.
* Accédez à votre bureau et de rechercher le **MixedReality213-master** dossier vous non précédemment archivé.
* Cliquez sur **Sélectionner un dossier**.
* Une fois que Unity a terminé le chargement des fichiers de projet, vous serez en mesure de voir éditeur Unity.
* Dans Unity, sélectionnez **fichier > Paramètres de Build**.

![MR213_BuildSettings](images/mr213-buildsettings-450px.png)
* Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur le **plateforme de commutation** bouton.
* Appareil cible la valeur **n’importe quel appareil**
* Définissez le Type de Build sur **D3D**
* Définissez le SDK **dernière installé**
* Vérifiez **Unity C# projets**
    * Cela vous permet de que modifier les fichiers de script dans le projet Visual Studio sans régénération du projet Unity.
* Cliquez sur **paramètres du lecteur**.
* Dans le **inspecteur** Panneau de configuration, faites défiler vers le bas
* Dans paramètres XR, vérifiez **virtuel pris en charge de réalité**
* Sous SDK de réalité virtuelle, sélectionnez **Windows Mixed Reality**

![MR213_XRSettings](images/mr213-xrsettings-500px.png)
* Fermer **paramètres de Build** fenêtre.

### <a name="project-structure"></a>Structure de projet

Ce didacticiel utilise  **[Toolkit de réalité mixte - Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity)**. Vous pouvez trouver les versions sur [cette page](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases).

![ProjectStructure](images/mr213-projectstructure-650px.png)

**Arrière-plan terminé pour votre référence**
* Vous trouverez deux scènes Unity terminées sous **scènes** dossier.
    * **MixedReality213**: Scène terminée avec un pinceau unique
    * **MixedReality213Advanced**: Fin de scène pour conception avancée avec plusieurs pinceaux

**Nouvelle installation de scène pour le didacticiel**
* Dans Unity, cliquez sur **fichier > nouvelle scène**
* Supprimer **caméra principale** et **lumière directionnelle**
* À partir de la **panneau projet**, recherchez et faites glisser les prefabs suivants dans le **hiérarchie** panneau :
    * Assets/HoloToolkit/Input/Prefabs/**MixedRealityCamera**
    * Assets/AppPrefabs/**Environment**

![Appareil photo et l’environnement](images/mr213-cameraenvironment-300px.jpg)
* Il existe deux prefabs appareil photo dans la boîte à outils de réalité mixte :
    * **MixedRealityCamera.prefab**: Caméra uniquement
    * **MixedRealityCameraParent.prefab**: Appareil photo + téléportation + limite
    * Dans ce didacticiel, nous allons utiliser **MixedRealityCamera** sans téléportation fonctionnalité. Pour cette raison, nous avons ajouté simple **environnement** préfabriqué qui contient un étage de base pour rendre l’utilisateur se sentent la terre.
    * Pour en savoir plus sur la téléportation avec **MixedRealityCameraParent**, consultez [conception - téléportation et locomotion avancée](#advanced-design---teleportation-and-locomotion)

**Programme d’installation skybox**
* Cliquez sur **fenêtre > éclairage > Paramètres**
* Cliquez sur le cercle sur le côté droit de la **champ de Skybox matériau**
* Tapez « gris » et sélectionnez **SkyboxGray**

(Assets/AppPrefabs/Support/Materials/SkyboxGray.mat)

![Paramètre skybox](images/mr123-skyboxsetting-400px.jpg)
* Vérifiez **Skybox** option pour être en mesure de voir affecté skybox dégradé gris

![Activer/désactiver skybox option](images/mr213-skyboxcheck-400px.jpg)
* La scène avec MixedRealityCamera, environnement et gris skybox se présentera comme suit.

![Environnement de MixedReality213](images/mr213-environment-600px.jpg)
* Cliquez sur **fichier > Enregistrer la scène en tant que**
* **Enregistrer** votre scène sous le dossier de scènes avec n’importe quel nom

## <a name="chapter-1---controller-visualization"></a>Chapitre 1 - visualisation du contrôleur

>[!VIDEO https://www.youtube.com/embed/Kw0bf5NqyRg]

### <a name="objectives"></a>Objectifs

* Découvrez comment restituer des modèles de contrôleur en mode de jeu d’Unity et de l’exécution de mouvement.

Réalité mixte Windows fournit un modèle de contrôleur animée pour la visualisation de contrôleur. Il existe plusieurs approches que possibles pour la visualisation de contrôleur dans votre application :
* Par défaut, à l’aide de contrôleur par défaut sans aucune modification
* Hybride - à l’aide de contrôleur par défaut, mais certains de ses éléments personnalisation ou recouvrir des composants d’interface utilisateur
* Remplacement - à l’aide de votre propre personnalisé à un modèle 3D pour le contrôleur

Dans ce chapitre, vous allez apprendre sur les exemples de ces personnalisations de contrôleur.

### <a name="instructions"></a>Instructions

* Dans le **projet** panneau, tapez **MotionControllers** dans la zone de recherche. Vous pouvez également le trouver sous ressources/HoloToolkit/Input/Prefabs /.
* Faites glisser le **MotionControllers** prefab dans le **hiérarchie** Panneau de configuration.
* Cliquez sur le **MotionControllers** prefab dans le **hiérarchie** Panneau de configuration.

**MotionControllers préfabriqué**

**MotionControllers** préfabriqué a un **MotionControllerVisualizer** script qui fournit les emplacements pour les modèles de l’autre contrôleur. Si vous attribuez vos propres modèles 3D personnalisées telles que main ou un mot de passe et que vous vérifiez « Toujours modèle l’utilisation autre gauche/droite », vous les voyez au lieu du modèle par défaut. Nous allons utiliser cet emplacement dans le chapitre 4 pour remplacer le modèle de contrôleur avec un pinceau.

![MR213_ControllerVisualizer](images/mr213-controllervisualizer-600px.png)

**Instructions**
* Dans le **inspecteur** , double-cliquez sur le panneau **MotionControllerVisualizer** script pour afficher le code dans Visual Studio

**Script de MotionControllerVisualizer**

Le **MotionControllerVisualizer** et **MotionControllerInfo** classes fournissent les moyens d’accéder aux & modifier les modèles de contrôleur par défaut. **MotionControllerVisualizer** s’abonne à Unity **InteractionSourceDetected** événement et instancie automatiquement des modèles de contrôleur quand ils sont trouvent.

```cs
protected override void Awake()
{
    ...
    InteractionManager.InteractionSourceDetected += InteractionManager_InteractionSourceDetected;
    InteractionManager.InteractionSourceLost += InteractionManager_InteractionSourceLost;
    ...
}
```

Les modèles de contrôleur sont remis en fonction de [la spécification glTF](https://github.com/KhronosGroup/glTF). Ce format a été créé pour fournir un format commun, tout en améliorant le processus derrière la transmission et la décompression des composants 3D. Dans ce cas, nous devons récupérer et charger les modèles de contrôleur lors de l’exécution, comme nous voulons que l’utilisateur expérience aussi transparente que possible, et il n’a pas garanti quelle version des contrôleurs de mouvement de l’utilisateur peut utiliser. Ce cours, par le biais de la boîte à outils de réalité mixte, utilise une version du groupe Khronos [UnityGLTF projet](https://github.com/KhronosGroup/UnityGLTF).

Une fois que le contrôleur a été remis, les scripts peuvent utiliser **MotionControllerInfo** pour rechercher les transformations pour les éléments d’un contrôleur spécifique afin qu’ils peuvent se positionner correctement.

Dans un chapitre ultérieur, nous allez apprendre à utiliser ces scripts pour joindre des éléments d’interface utilisateur pour les contrôleurs.

*Dans certains scripts, vous trouverez des blocs de code avec **#if ! UNITY_EDITOR** ou **UNITY_WSA**. Ces blocs de code exécutent uniquement sur le runtime UWP lorsque vous déployez pour Windows. Il s’agit, car le jeu d’API utilisées par l’éditeur Unity et le runtime d’application UWP sont différents.*
* **Enregistrer** la scène et cliquez sur le **lire** bouton.

Vous serez en mesure de voir la scène avec des contrôleurs de mouvement dans votre casque. Vous pouvez voir les animations détaillées pour les clics de bouton, de déplacement de stick analogique et mise en surbrillance du tactile pavé tactile.

![Par défaut de visualisation MR213_Controller](images/mr213-controllervisualizationdefault-500px.jpg)

## <a name="chapter-2---attaching-ui-elements-to-the-controller"></a>Chapitre 2 : attacher des éléments d’interface utilisateur pour le contrôleur

>[!VIDEO https://www.youtube.com/embed/e-mLlwmTzJo]

### <a name="objectives"></a>Objectifs

* En savoir plus sur les éléments des contrôleurs de mouvement
* Découvrez comment attacher des objets à des parties spécifiques des contrôleurs

Dans ce chapitre, vous allez apprendre à ajouter des éléments d’interface utilisateur pour le contrôleur sur lequel l’utilisateur peut facilement accéder et manipuler à tout moment au. Vous allez également apprendre à ajouter un sélecteur de couleurs simple interface utilisateur en utilisant le pavé tactile d’entrée.

### <a name="instructions"></a>Instructions

* Dans le **projet** du panneau, recherchez **MotionControllerInfo** script.
* À partir du résultat de recherche, double-cliquez sur **MotionControllerInfo** script pour afficher le code dans Visual Studio.

**Script de MotionControllerInfo**

La première étape consiste à décider quel élément du contrôleur de l’interface utilisateur à joindre à. Ces éléments sont définis dans **ControllerElementEnum** dans **MotionControllerInfo.cs**.

![MR213 MotionControllerElements](images/mr213-motioncontrollerelements-1000px.jpg)
* **Accueil**
* **Menu**
* **Comprendre**
* **Stick analogique**
* **Select**
* **Pavé tactile**
* **Pointage pose** : cet élément représente l’info-bulle du contrôleur qui pointe vers l’avant.

**Instructions**
* Dans le **projet** du panneau, recherchez **AttachToController** script.
* À partir du résultat de recherche, double-cliquez sur **AttachToController** script pour afficher le code dans Visual Studio.

**Script de AttachToController**

Le **AttachToController** script fournit un moyen simple d’attacher des objets à un caractère gaucher ou droitier de contrôleur spécifié et l’élément.

Dans **AttachElementToController()**,
* Vérifier à l’aide du caractère gaucher ou droitier **MotionControllerInfo.Handedness**
* Obtenir un élément spécifique du contrôleur en utilisant **MotionControllerInfo.TryGetElement()**
* Après avoir récupéré l’élément transformer du modèle de contrôleur, le parent de l’objet dans cette section et définir la position locale et la rotation de l’objet à zéro.

```cs
public MotionControllerInfo.ControllerElementEnum Element { get { return element; } }

private void AttachElementToController(MotionControllerInfo newController)
{
     if (!IsAttached && newController.Handedness == handedness)
     {
          if (!newController.TryGetElement(element, out elementTransform))
          {
               Debug.LogError("Unable to find element of type " + element + " under controller " + newController.ControllerParent.name + "; not attaching.");
               return;
          }

          controller = newController;

          SetChildrenActive(true);

          // Parent ourselves under the element and set our offsets
          transform.parent = elementTransform;
          transform.localPosition = positionOffset;
          transform.localEulerAngles = rotationOffset;
          if (setScaleOnAttach)
          {
               transform.localScale = scale;
          }

          // Announce that we're attached
          OnAttachToController();
          IsAttached = true;
     }
}
```

La façon la plus simple d’utiliser **AttachToController** script consiste à hériter de celui-ci, comme nous l’avons fait dans le cas de **ColorPickerWheel.** Il vous suffit de remplacer le **OnAttachToController** et **OnDetatchFromController** fonctions pour effectuer votre installation / répartition lorsque le contrôleur est détecté ou déconnecté.

**Instructions**
* Dans le **projet** panneau, tapez dans la zone de recherche **ColorPickerWheel**. Vous pouvez également le trouver sous ressources/AppPrefabs /.
* Faites glisser **ColorPickerWheel** prefab dans le **hiérarchie** Panneau de configuration.
* Cliquez sur le **ColorPickerWheel** prefab dans le **hiérarchie** Panneau de configuration.
* Dans le **inspecteur** , double-cliquez sur le panneau **ColorPickerWheel** Script pour afficher le code dans Visual Studio.

![ColorPickerWheel préfabriqué](images/mr213-colorpickerwheel-1000px.jpg)

**Script de ColorPickerWheel**

Dans la mesure où **ColorPickerWheel** hérite **AttachToController**, il montre **gaucher/droitier** et **élément** dans le  **Inspecteur** Panneau de configuration. Nous allons attacher l’interface utilisateur à l’élément du pavé tactile sur le contrôleur de gauche.

![Script de ColorPickerWheel](images/mr213-attachtocontroller-300px.jpg)

**ColorPickerWheel** remplace le **OnAttachToController** et **OnDetatchFromController** pour vous abonner à l’événement d’entrée qui sera utilisé dans le chapitre suivant pour la sélection de couleur avec pavé tactile d’entrée.

```cs
public class ColorPickerWheel : AttachToController, IPointerTarget
{
    protected override void OnAttachToController()
    {
        // Subscribe to input now that we're parented under the controller
        InteractionManager.InteractionSourceUpdated += InteractionSourceUpdated;
    }

    protected override void OnDetachFromController()
    {
        Visible = false;

        // Unsubscribe from input now that we've detached from the controller
        InteractionManager.InteractionSourceUpdated -= InteractionSourceUpdated;
    }
    ...
}
```
* **Enregistrer** la scène et cliquez sur le **lire** bouton.

**Autre méthode d’attachement d’objets pour les contrôleurs**

Nous recommandons que vos scripts héritent **AttachToController** et remplacer **OnAttachToController**. Toutefois, cela n'est pas toujours possible. Une alternative l’utilise en tant que composant autonome. Cela peut être utile lorsque vous souhaitez associer un préfabriqué existant à un contrôleur sans refactorisation vos scripts. Simplement que votre classe attendre IsAttached être définie sur true avant d’effectuer tout le programme d’installation. Le plus simple pour ce faire consiste à l’aide d’une coroutine pour 'Start'.

```cs
private IEnumerator Start() {
    AttachToController attach = gameObject.GetComponent<AttachToController>();

    while (!attach.IsAttached) {
        yield return null;
    }

    // Perform setup here
}
```

## <a name="chapter-3---working-with-touchpad-input"></a>Chapitre 3 - utilisation de l’entrée du pavé tactile

>[!VIDEO https://www.youtube.com/embed/SUyw0kxZPFw]

### <a name="objectives"></a>Objectifs

* Découvrez comment obtenir les événements de données d’entrée du pavé tactile
* Découvrez comment utiliser les informations de position de l’axe du pavé tactile pour votre expérience d’application

### <a name="instructions"></a>Instructions

* Dans le **hiérarchie** du panneau, cliquez sur **ColorPickerWheel**
* Dans le **inspecteur** panneau, sous **Animatior**, double-cliquez sur **ColorPickerWheelController**
* Vous serez en mesure de voir **animation** onglet ouvert

**Interface utilisateur de l’affichage/masquage avec le contrôleur de l’Animation d’Unity**

Pour afficher et masquer le **ColorPickerWheel** l’interface utilisateur avec l’animation, nous utilisons [système d’animation d’Unity](https://docs.unity3d.com/Manual/AnimationOverview.html). Définition de la **ColorPickerWheel**de **Visible** propriété aux déclencheurs true ou false **afficher** et **masquer** les déclencheurs d’animations. **Afficher** et **masquer** paramètres sont définis dans le **ColorPickerWheelController** contrôleur de l’animation.

![Contrôleur de l’Animation Unity](images/mr123-animationcontroller-550px.jpg)

**Instructions**
* Dans le **hiérarchie** panneau, sélectionnez **ColorPickerWheel** prefab
* Dans le **inspecteur** , double-cliquez sur le panneau **ColorPickerWheel** script pour afficher le code dans Visual Studio

**Script de ColorPickerWheel**

**ColorPickerWheel** s’abonne à Unity **InteractionSourceUpdated** événements pour écouter les événements du pavé tactile.

Dans **InteractionSourceUpdated()**, le script vérifie d’abord pour vous assurer qu’elles :
* est en fait un événement tactile (obj.state. **touchpadTouched**)
* origine à partir du contrôleur de gauche (obj.state.source. **gaucher/droitier**)

Si les deux sont true, le pavé tactile positionner (obj.state. **touchpadPosition**) est affectée à **selectorPosition**.

```cs
private void InteractionSourceUpdated(InteractionSourceUpdatedEventArgs obj)
{
    if (obj.state.source.handedness == handedness && obj.state.touchpadTouched)
    {
        Visible = true;
        selectorPosition = obj.state.touchpadPosition;
    }
}
```

Dans **Update()**, en fonction de **visible** propriété, il déclenche l’affichage et le masquage des déclencheurs d’animation dans le composant d’animation du sélecteur de couleurs

```cs
if (visible != visibleLastFrame)
{
    if (visible)
    {
        animator.SetTrigger("Show");
    }
    else
    {
        animator.SetTrigger("Hide");
    }
}
```

Dans **Update()**, **selectorPosition** est utilisé pour effectuer un cast d’un rayon à collider de maillage de la roulette de la couleur, qui retourne une position UV. Cette position peut ensuite servir à trouver les coordonnées de pixel et de couleur de texture de la roue couleur. Cette valeur est accessible aux autres scripts via la **SelectedColor** propriété.

![Raycasting de roulette de sélecteur de couleurs](images/mr213-colorpickerwheel-raycast-700px.png)

```cs
...
    // Clamp selector position to a radius of 1
    Vector3 localPosition = new Vector3(selectorPosition.x * inputScale, 0.15f, selectorPosition.y * inputScale);
    if (localPosition.magnitude > 1)
    {
        localPosition = localPosition.normalized;
    }
    selectorTransform.localPosition = localPosition;

    // Raycast the wheel mesh and get its UV coordinates
    Vector3 raycastStart = selectorTransform.position + selectorTransform.up * 0.15f;
    RaycastHit hit;
    Debug.DrawLine(raycastStart, raycastStart - (selectorTransform.up * 0.25f));

    if (Physics.Raycast(raycastStart, -selectorTransform.up, out hit, 0.25f, 1 << colorWheelObject.layer, QueryTriggerInteraction.Ignore))
    {
        // Get pixel from the color wheel texture using UV coordinates
        Vector2 uv = hit.textureCoord;
        int pixelX = Mathf.FloorToInt(colorWheelTexture.width * uv.x);
        int pixelY = Mathf.FloorToInt(colorWheelTexture.height * uv.y);
        selectedColor = colorWheelTexture.GetPixel(pixelX, pixelY);
        selectedColor.a = 1f;
    }
    // Set the selector's color and blend it with white to make it visible on top of the wheel
    selectorRenderer.material.color = Color.Lerp (selectedColor, Color.white, 0.5f);
}
```

## <a name="chapter-4---overriding-controller-model"></a>Chapitre 4 - modèle de contrôleur de remplacement

>[!VIDEO https://www.youtube.com/embed/8gBFqA_DZ_U]

### <a name="objectives"></a>Objectifs

* Découvrez comment remplacer le modèle de contrôleur avec un modèle 3D personnalisé.

![MR213_BrushToolOverride](images/mr213-brushtooloverride-500px.jpg)

### <a name="instructions"></a>Instructions

* Cliquez sur **MotionControllers** dans le **hiérarchie** Panneau de configuration.
* Cliquez sur le cercle sur le côté droit de la **autre contrôleur droite** champ.
* Tapez dans **' BrushController**» et sélectionnez le préfabriqué à partir du résultat. Vous pouvez le trouver sous ressources/AppPrefabs/**BrushController**.
* Vérifiez **toujours utiliser le modèle approprié autre**

![MR213_BrushToolOverrideSlot](images/mr213-motioncontrollersoverride-700px.jpg)

Le **BrushController** préfabriqué ne devra pas être inclus dans le **hiérarchie** Panneau de configuration. Toutefois, à consulter ses composants enfants :
* Dans le **projet** panneau, tapez **BrushController** et faites glisser **BrushController** prefab dans le **hiérarchie** Panneau de configuration.

![MR213_BrushTool_Prefab2](images/mr213-brushtool-prefab-1000px.jpg)

Vous trouverez le **Conseil** composant dans **BrushController**. Nous allons utiliser sa transformation pour tracer des lignes de démarrage/arrêt.
* Supprimer le **BrushController** à partir de la **hiérarchie** Panneau de configuration.
* **Enregistrer** la scène et cliquez sur le **lire** bouton. Vous serez en mesure de voir que le modèle de pinceau remplacé le contrôleur de mouvement de droite.

## <a name="chapter-5---painting-with-select-input"></a>Chapitre 5 - entrée de peinture avec Select

>[!VIDEO https://www.youtube.com/embed/QTrYaMHIs7w]

### <a name="objectives"></a>Objectifs

* Découvrez comment utiliser l’événement de bouton Sélectionner pour démarrer et arrêter un dessin au trait

### <a name="instructions"></a>Instructions

* Recherche **BrushController** prefab dans le **projet** Panneau de configuration.
* Dans le **inspecteur** , double-cliquez sur le panneau **BrushController** Script pour afficher le code dans Visual Studio

**Script de BrushController**

**BrushController** s’abonne à la InteractionManager **InteractionSourcePressed** et **InteractionSourceReleased** événements. Lorsque **InteractionSourcePressed** événement est déclenché, le pinceau **dessiner** propriété est définie sur true ; lorsque **InteractionSourceReleased** événement est déclenché, le pinceau **Dessiner** propriété est définie sur false.

```cs
private void InteractionSourcePressed(InteractionSourcePressedEventArgs obj)
{
    if (obj.state.source.handedness == InteractionSourceHandedness.Right && obj.pressType == InteractionSourcePressType.Select)
    {
        Draw = true;
    }
}

private void InteractionSourceReleased(InteractionSourceReleasedEventArgs obj)
{
    if (obj.state.source.handedness == InteractionSourceHandedness.Right && obj.pressType == InteractionSourcePressType.Select)
    {
        Draw = false;
    }
}
```

Bien que **dessiner** est définie sur true, le pinceau généreront les points dans un Unity instancié **LineRenderer**. Une référence à cette préfabriqué est conservée dans le pinceau **Prefab Stroke** champ.

```cs
private IEnumerator DrawOverTime()
{
    // Get the position of the tip
    Vector3 lastPointPosition = tip.position;

    ...

    // Create a new brush stroke
    GameObject newStroke = Instantiate(strokePrefab);
    LineRenderer line = newStroke.GetComponent<LineRenderer>();
    newStroke.transform.position = startPosition;
    line.SetPosition(0, tip.position);
    float initialWidth = line.widthMultiplier;

    // Generate points in an instantiated Unity LineRenderer
    while (draw)
    {
        // Move the last point to the draw point position
        line.SetPosition(line.positionCount - 1, tip.position);
        line.material.color = colorPicker.SelectedColor;
        brushRenderer.material.color = colorPicker.SelectedColor;
        lastPointAddedTime = Time.unscaledTime;
        // Adjust the width between 1x and 2x width based on strength of trigger pull
        line.widthMultiplier = Mathf.Lerp(initialWidth, initialWidth * 2, width);

        if (Vector3.Distance(lastPointPosition, tip.position) > minPositionDelta || Time.unscaledTime > lastPointAddedTime + maxTimeDelta)
        {
            // Spawn a new point
            lastPointAddedTime = Time.unscaledTime;
            lastPointPosition = tip.position;
            line.positionCount += 1;
            line.SetPosition(line.positionCount - 1, lastPointPosition);
        }
        yield return null;
    }
}
```

Pour utiliser la couleur actuellement sélectionnée à partir de la roulette de sélecteur de couleurs interface utilisateur, **BrushController** doit avoir une référence à la **ColorPickerWheel** objet. Étant donné que le **BrushController** préfabriqué est instancié lors de l’exécution en tant qu’un contrôleur de remplacement, toutes les références aux objets dans la scène aura à définir lors de l’exécution. Dans ce cas, nous utilisons **GameObject.FindObjectOfType** pour localiser le **ColorPickerWheel**:

```cs
private void OnEnable()
{
    // Locate the ColorPickerWheel
    colorPicker = FindObjectOfType<ColorPickerWheel>();

    // Assign currently selected color to the brush’s material color
    brushRenderer.material.color = colorPicker.SelectedColor;
    ...
}
```
* **Enregistrer** la scène et cliquez sur le **lire** bouton. Vous ne pourrez pas dessiner les lignes et peindre à l’aide du bouton de sélection sur le contrôleur de droite.

## <a name="chapter-6---object-spawning-with-select-input"></a>Chapitre 6 - objet lors de la génération avec Select d’entrée

>[!VIDEO https://www.youtube.com/embed/z4IxyzFHP0U]

### <a name="objectives"></a>Objectifs

* Découvrez comment utiliser Select et comprendre les événements d’entrée de bouton
* Découvrez comment instancier des objets

### <a name="instructions"></a>Instructions

* Dans le **projet** panneau, tapez **ObjectSpawner** dans la zone de recherche. Vous pouvez également le trouver sous ressources/AppPrefabs /
* Faites glisser le **ObjectSpawner** prefab dans le **hiérarchie** Panneau de configuration.
* Cliquez sur **ObjectSpawner** dans le **hiérarchie** Panneau de configuration.
* **ObjectSpawner** possède un champ nommé **couleur Source**.
* À partir de la **hiérarchie** volet, faites glisser le **ColorPickerWheel** référence dans ce champ.

![Objet Spawner inspecteur](images/mr213-objectspawnercolorpickerwheel-650px.jpg)
* Cliquez sur le **ObjectSpawner** prefab dans le **hiérarchie** Panneau de configuration.
* Dans le **inspecteur** , double-cliquez sur le panneau **ObjectSpawner** Script pour afficher le code dans Visual Studio.

**Script de ObjectSpawner**

Le **ObjectSpawner** instancie des copies d’une maille primitifs (cube, sphère, cylindre) dans l’espace. Quand un **InteractionSourcePressed** est détecté qu’il vérifie le caractère gaucher ou droitier et s’il est un **InteractionSourcePressType.Grasp** ou **InteractionSourcePressType.Select** événement.

Pour un **saisir** événement, il incrémente l’index de type maille actuel (sphère, cube, cylindre)

```cs
private void InteractionSourcePressed(InteractionSourcePressedEventArgs obj)
{
    // Check handedness, see if it is left controller
    if (obj.state.source.handedness == handedness)
    {
        switch (obj.pressType)
        {
            // If it is Select button event, spawn object
            case InteractionSourcePressType.Select:
                if (state == StateEnum.Idle)
                {
                    // We've pressed the grasp - enter spawning state
                    state = StateEnum.Spawning;
                    SpawnObject();
                }
                break;

            // If it is Grasp button event
            case InteractionSourcePressType.Grasp:

                // Increment the index of current mesh type (sphere, cube, cylinder)
                meshIndex++;
                if (meshIndex >= NumAvailableMeshes)
                {
                    meshIndex = 0;
                }
                break;

            default:
                break;
        }
    }
}
```

Pour un **sélectionnez** événement, dans **SpawnObject()**, un nouvel objet est instancié, non apparentée et publiées dans le monde entier.

```cs
private void SpawnObject()
{
    // Instantiate the spawned object
    GameObject newObject = Instantiate(displayObject.gameObject, spawnParent);
    // Detatch the newly spawned object
    newObject.transform.parent = null;
    // Reset the scale transform to 1
    scaleParent.localScale = Vector3.one;
    // Set its material color so its material gets instantiated
    newObject.GetComponent<Renderer>().material.color = colorSource.SelectedColor;
}
```

Le **ObjectSpawner** utilise le **ColorPickerWheel** pour définir la couleur des éléments de l’objet d’affichage. Objets engendrés bénéficient d’une instance de ce document afin qu’ils conserveront leur couleur.
* **Enregistrer** la scène et cliquez sur le **lire** bouton.

Vous ne pourrez pas modifier les objets avec le bouton de comprendre et de générer dynamiquement des objets avec le bouton de sélection.

## <a name="build-and-deploy-app-to-mixed-reality-portal"></a>Créer et déployer l’application au portail de réalité mixte
* Dans Unity, sélectionnez **fichier > Paramètres de Build**.
* Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène actuelle pour le **scènes dans Build**.
* Cliquez sur **Build**.
* Créer un **nouveau dossier** nommé « Application ».
* Clic le **application** dossier.
* Cliquez sur **Sélectionner un dossier**.
* Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.
* Ouvrez le **application** dossier.
* Double-cliquez sur **YourSceneName.sln** fichier de Solution Visual Studio.
* À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **X64**.
* Cliquez sur la flèche déroulante en regard du bouton de l’appareil, puis sélectionnez **ordinateur Local**.
* Cliquez sur **Déboguer -> Démarrer sans débogage** dans le menu ou appuyez sur **Ctrl + F5**.

Maintenant, l’application est créée et installée dans le portail de réalité mixte. Vous pouvez le lancer à nouveau via le menu Démarrer dans le portail de réalité mixte.

## <a name="advanced-design---brush-tools-with-radial-layout"></a>Conception avancée - outils de pinceau avec disposition radial

![MixedReality213 Main](images/mr213-main-600px.jpg)

Dans ce chapitre, vous allez apprendre à remplacer le modèle de contrôleur de mouvement par défaut par une collection d’outil Pinceau personnalisé. À titre de référence, vous pouvez trouver la scène terminée **MixedReality213Advanced** sous **scènes** dossier.

### <a name="instructions"></a>Instructions

* Dans le **projet** panneau, tapez **BrushSelector** dans la zone de recherche. Vous pouvez également le trouver sous ressources/AppPrefabs /
* Faites glisser le **BrushSelector** prefab dans le **hiérarchie** Panneau de configuration.
* Pour l’organisation, créer un GameObject vide appelé **pinceaux**
* Faites glisser suivantes prefabs à partir de la **projet** panneau dans **pinceaux**
    * Assets/AppPrefabs/**BrushFat**
    * Assets/AppPrefabs/**BrushThin**
    * Assets/AppPrefabs/**Eraser**
    * Assets/AppPrefabs/**MarkerFat**
    * Assets/AppPrefabs/**MarkerThin**
    * Assets/AppPrefabs/**Pencil**

![Pinceaux](images/mixedreality213-brushes-250px.png)
* Cliquez sur **MotionControllers** prefab dans le **hiérarchie** Panneau de configuration.
* Dans le **inspecteur** panneau, décochez la case **toujours modèle l’utilisation autre droit** sur la **visualiseur de contrôleur de mouvement**
* Dans le **hiérarchie** du panneau, cliquez sur **BrushSelector**
* **BrushSelector** possède un champ nommé **ColorPicker**
* À partir de la **hiérarchie** volet, faites glisser le **ColorPickerWheel** dans **ColorPicker** champ dans le **inspecteur** Panneau de configuration.

![Affecter ColorPickerWheel de sélecteur de pinceau](images/mr213-brushselector-500px.jpg)
* Dans le **hiérarchie** panneau, sous **BrushSelector** prefab, sélectionnez le **Menu** objet.
* Dans le **inspecteur** panneau, sous la **LineObjectCollection** composant, ouvrez le **objets** tableau dropdown. Vous verrez les emplacements vides 6.
* À partir de la **hiérarchie** volet, faites glisser chacune des prefabs apparentés sous le **pinceaux** GameObject dans ces emplacements dans n’importe quel ordre. (Assurez-vous que vous faites glisser les prefabs à partir de la scène, pas les préfabriqués dans le dossier du projet.)

![Sélecteur de pinceau](images/mr213-brushselectorbrushes-700px.jpg)

**BrushSelector préfabriqué**

Dans la mesure où le **BrushSelector** hérite **AttachToController**, il montre **gaucher/droitier** et **élément** options dans le  **Inspecteur** Panneau de configuration. Nous avons sélectionné **droite** et **pointant poser** pour attacher les outils de pinceau pour le contrôleur de droite avec la direction vers l’avant.

Le **BrushSelector** utilise deux utilitaires :
* **Ellipse**: permet de générer des points dans l’espace le long d’une forme d’ellipse.
* **LineObjectCollection**: distribue les objets à l’aide de points générés par n’importe quelle classe de ligne (par exemple, Ellipse). C’est ce que nous allons utiliser pour placer notre pinceaux le long de la forme d’Ellipse.

Lorsqu’elles sont combinées, ces utilitaires peuvent être utilisés pour créer un menu radial.

**Script de LineObjectCollection**

**LineObjectCollection** dispose de contrôles pour la taille, la position et la rotation d’objets distribués selon sa ligne. Cela est utile pour la création de menus radiales telles que le sélecteur de pinceau. Pour créer l’apparence de pinceaux cette mise à l’échelle à partir de rien que qu’ils approchent de la position du centre sélectionné, le **ObjectScale** courbe pics dans le centre et le se désactivé à la périphérie.

**Script de BrushSelector**

Dans le cas de la **BrushSelector**, nous avons choisi d’utiliser une animation procédurale. Tout d’abord, les modèles de pinceau sont distribués dans une ellipse par le **LineObjectCollection** script. Ensuite, chaque pinceau est responsable du maintien de sa position en main de l’utilisateur selon son **DisplayMode** valeur, en fonction de la sélection. Nous avons choisi une approche procédurale en raison de la forte probabilité de transitions de position de pinceau interrompue lorsque l’utilisateur sélectionne des pinceaux. Les animations Mecanim peuvent gérer correctement les interruptions, mais il a tendance à être plus compliquée qu’une simple opération Lerp.

**BrushSelector** utilise une combinaison des deux. Lors de l’entrée du pavé tactile est détectée, les options de pinceau deviennent visibles et monter le long du menu radial. Après une période de délai d’attente (ce qui indique que l’utilisateur a effectué une sélection) le pinceau des options de mise à l’échelle vers le bas, en laissant uniquement le pinceau sélectionné.

**Visualisation d’entrée du pavé tactile**

Même dans les cas où le modèle de contrôleur a été entièrement remplacé, il peut être utile afficher d’entrée sur les entrées de modèle d’origine. Cela permet à la pour terre des actions de l’utilisateur en réalité. Pour le **BrushSelector** que nous avons choisi rendre le pavé tactile brièvement visibles lorsque l’entrée est reçue. Cela a été effectuée en récupérant l’élément pavé tactile à partir du contrôleur, en remplaçant son matériel avec un matériel personnalisé, puis appliquer un dégradé de couleur de ce matériel basé sur le pavé tactile de heure dernière entrée a été reçue.

```cs
protected override void OnAttachToController()
{
    // Turn off the default controller's renderers
    controller.SetRenderersVisible(false);

    // Get the touchpad and assign our custom material to it
    Transform touchpad;
    if (controller.TryGetElement(MotionControllerInfo.ControllerElementEnum.Touchpad, out touchpad))
    {
        touchpadRenderer = touchpad.GetComponentInChildren<MeshRenderer>();
        originalTouchpadMaterial = touchpadRenderer.material;
        touchpadRenderer.material = touchpadMaterial;
        touchpadRenderer.enabled = true;
    }
            
    // Subscribe to input now that we're parented under the controller
    InteractionManager.InteractionSourceUpdated += InteractionSourceUpdated;
}

private void Update()
{
    ...
    // Update our touchpad material
    Color glowColor = touchpadColor.Evaluate((Time.unscaledTime - touchpadTouchTime) / touchpadGlowLossTime);
    touchpadMaterial.SetColor("_EmissionColor", glowColor);
    touchpadMaterial.SetColor("_Color", glowColor);
    ...
}
```

**Sélection de l’outil Pinceau avec une entrée tactile**

Lorsque le sélecteur de pinceau détecte l’entrée appuyé du pavé tactile, il vérifie la position de l’entrée pour déterminer si elle a été vers la gauche ou droite.

**Épaisseur du trait avec selectPressedAmount**

Au lieu du **InteractionSourcePressType.Select** événement dans le **InteractionSourcePressed()**, vous pouvez obtenir la valeur analogique du montant appuyé via **selectPressedAmount**. Cette valeur peut être récupérée dans **InteractionSourceUpdated()**.

```cs
private void InteractionSourceUpdated(InteractionSourceUpdatedEventArgs obj)
{
    if (obj.state.source.handedness == handedness)
    {
        if (obj.state.touchpadPressed)
        {
            // Check which side we clicked
            if (obj.state.touchpadPosition.x < 0)
            {
                currentAction = SwipeEnum.Left;
            }
            else
            {
                currentAction = SwipeEnum.Right;
            }

            // Ping the touchpad material so it gets bright
            touchpadTouchTime = Time.unscaledTime;
        }

        if (activeBrush != null)
        {
            // If the pressed amount is greater than our threshold, draw
            if (obj.state.selectPressedAmount >= selectPressedDrawThreshold)
            {
                activeBrush.Draw = true;
                activeBrush.Width = ProcessSelectPressedAmount(obj.state.selectPressedAmount);
            }
            else
            {
                // Otherwise, stop drawing
                activeBrush.Draw = false;
                selectPressedSmooth = 0f;
            }
        }
    }
}
```

**Script de la gomme**

**Gomme** est un type spécial de pinceau qui remplace la base de **pinceau**de **DrawOverTime()** (fonction). Bien que le dessin est true, la gomme vérifie si son info-bulle se croise avec des traits de pinceau existant. Dans l’affirmative, ils sont ajoutés à une file d’attente pour être réduit vers le bas et supprimées.

## <a name="advanced-design---teleportation-and-locomotion"></a>Conception avancée - téléportation et locomotion

Si vous souhaitez autoriser l’utilisateur à déplacer la scène avec téléportation à l’aide de stick analogique, utilisez **MixedRealityCameraParent** au lieu de **MixedRealityCamera**. Vous devez également ajouter **InputManager** et **DefaultCusor**. Dans la mesure où **MixedRealityCameraParent** inclut déjà **MotionControllers** et **limite** en tant que composants enfants, vous devez supprimer existant  **MotionControllers** et **environnement** prefab.

### <a name="instructions"></a>Instructions

* Dans le **hiérarchie** panel, supprimer **MixedRealityCamera**, **environnement** et **MotionControllers**
* À partir de la **panneau projet**, recherchez et faites glisser les prefabs suivants dans le **hiérarchie** panneau :
    * Assets/AppPrefabs/Input/Prefabs/**MixedRealityCameraParent**
    * Assets/AppPrefabs/Input/Prefabs/**InputManager**
    * Assets/AppPrefabs/Input/Prefabs/Cursor/**DefaultCursor**

![Parent de la caméra de réalité mixte](images/mr213-cameraparent-300px.png)
* Dans le **hiérarchie** du panneau, cliquez sur **Gestionnaire d’entrée**
* Dans le **inspecteur** du panneau, faites défiler jusqu'à la **Simple sélecteur de pointeur unique** section
* À partir de la **hiérarchie** volet, faites glisser **DefaultCursor** dans **curseur** champ

![Affectation de DefaultCursor](images/mr213-defaultcursor-500px.png)
* **Enregistrer** la scène et cliquez sur le **lire** bouton. Vous serez en mesure d’utiliser le stick analogique gauche/droite ou teleport.

## <a name="the-end"></a>La fin

Et c’est la fin de ce didacticiel ! Vous avez appris :
* Comment travailler avec des modèles de contrôleur de mouvement dans le mode de jeu d’Unity et d’exécution.
* Comment utiliser différents types d’événements de bouton et de leurs applications.
* Guide pratique pour superposer des éléments d’interface utilisateur sur le contrôleur ou de personnaliser entièrement.

Vous êtes maintenant prêt à commencer à créer votre propre expérience d’immersion avec des contrôleurs de motion !

## <a name="completed-scenes"></a>Arrière-plan terminée

* Dans Unity **projet** panneau, cliquez sur le **scènes** dossier.
* Vous trouverez deux écrans Unity **MixedReality213** et **MixedReality213Advanced**.
    * **MixedReality213**: Scène terminée avec un pinceau unique
    * **MixedReality213Advanced**: Scène terminé avec plusieurs pinceau avec exemple de quantité appuyez sur bouton sélection

## <a name="see-also"></a>Voir aussi

* [Fichiers de projet 213 d’entrée M.](https://github.com/Microsoft/MixedReality213)
* [Toolkit de réalité mixte - scène de Test de contrôleur de mouvement](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/Input/Scenes)
* [Réalité mixte Toolkit - mécanique de manipulation](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/MotionControllers-GrabMechanics)
* [Directives de développement de contrôleur de mouvement](motion-controllers.md)
