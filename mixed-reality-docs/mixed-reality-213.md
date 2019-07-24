---
title: Entrée MR 213
description: Suivez ce didacticiel de codage avec Unity, Visual Studio et les casques immersifs pour apprendre les détails des contrôleurs de mouvement.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, immersion, contrôleur de mouvement, Academy, didacticiel
ms.openlocfilehash: 85449795a4fb3d182101cb5b4c4ce3fe85b009c0
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63516417"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br>

# <a name="mr-input-213-motion-controllers"></a>Monsieur 213: Contrôleurs de mouvement

Les contrôleurs de mouvement dans le monde de la réalité mixte ajoutent un autre niveau d’interactivité. Avec les contrôleurs de [mouvement](motion-controllers.md), nous pouvons interagir directement avec les objets de manière plus naturelle, de la même façon que nos interactions physiques en réel, en renforçant l’immersion et le plaisir de l’expérience de votre application.

Dans l’entrée 213, nous explorerons les événements d’entrée du contrôleur de mouvement en créant une expérience de peinture spatiale simple. Avec cette application, les utilisateurs peuvent peindre dans un espace tridimensionnel avec différents types de pinceaux et de couleurs.

## <a name="topics-covered-in-this-tutorial"></a>Rubriques traitées dans ce didacticiel

|![MixedReality213 Topic1](images/mr213-topic1.png)|![MixedReality213 Topic2](images/mr213-topic2.png)|![MixedReality213 Topic3](images/mr213-topic3.png)|
| :--- | :--- | :--- |
|**Visualisation du contrôleur**|**Événements d’entrée du contrôleur**|**Contrôleur personnalisé et interface utilisateur**|
|Découvrez comment restituer les modèles de contrôleur de mouvement dans le mode jeu et le runtime d’Unity.|Comprenez les différents types d’événements de bouton et leurs applications.|Découvrez comment superposer des éléments d’interface utilisateur en plus du contrôleur ou le personnaliser entièrement.|

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>Monsieur 213: Contrôleurs de mouvement</td><td style="text-align: center;"> </td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

Consultez la liste de vérification de l’installation des casques immersifs sur [cette page](install-the-tools.md).

* Ce didacticiel nécessite [Unity 2017.2.1 P2](https://beta.unity3d.com/download/1dc514532f08/UnityDownloadAssistant-2017.2.1p2.exe)

### <a name="project-files"></a>Fichiers projet

* [Téléchargez les fichiers](https://github.com/Microsoft/MixedReality213/archive/master.zip) requis par le projet et extrayez les fichiers sur le bureau.

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/MixedReality213).

## <a name="unity-setup"></a>Configuration de Unity

>[!VIDEO https://www.youtube.com/embed/cBAOALaHys4]

### <a name="objectives"></a>Objectifs

* Optimiser Unity pour le développement Windows Mixed Reality
* Configurer une caméra de réalité mixte
* Environnement d’installation

### <a name="instructions"></a>Instructions

* Démarrez Unity.
* Sélectionnez **ouvrir**.
* Accédez à votre bureau et recherchez le dossier **MixedReality213-Master** que vous avez précédemment non archivé.
* Cliquez sur **Sélectionner un dossier**.
* Une fois que Unity a fini de charger les fichiers projet, vous pouvez voir l’éditeur Unity.
* Dans Unity, sélectionnez **fichier > paramètres de build**.

![MR213_BuildSettings](images/mr213-buildsettings-450px.png)
* Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur le bouton **changer de plateforme** .
* Définir un appareil cible sur **un appareil**
* Définir le type de build sur **D3D**
* Installer le SDK sur le **dernier installé**
* Vérifier **les C# projets Unity**
    * Cela vous permet de modifier les fichiers de script dans le projet Visual Studio sans reconstruire le projet Unity.
* Cliquez sur **paramètres du lecteur**.
* Dans le volet de l' **inspecteur** , faites défiler l’écran vers le bas
* Dans les paramètres XR, vérifiez **la réalité virtuelle prise en charge**
* Sous kits de développement logiciel (SDK) Virtual Reality, sélectionnez **Windows Mixed Reality** .

![MR213_XRSettings](images/mr213-xrsettings-500px.png)
* Fermez la fenêtre **paramètres de build** .

### <a name="project-structure"></a>Structure de projet

Ce didacticiel utilise la **[réalité mixte Toolkit-Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity)** . Vous pouvez trouver les versions dans [cette page](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases).

![ProjectStructure](images/mr213-projectstructure-650px.png)

**Scènes terminées pour votre référence**
* Deux scènes Unity terminées s’affichent sous le dossier **scenes** .
    * **MixedReality213**: Scène terminée avec un seul pinceau
    * **MixedReality213Advanced**: Scène terminée pour une conception avancée avec plusieurs pinceaux

**Nouvelle configuration de scène pour le didacticiel**
* Dans Unity, cliquez sur **fichier > nouvelle scène**
* Supprimer la **caméra principale** et la **lumière directionnelle**
* Dans le **volet de projet**, recherchez et faites glisser le prefabs suivant dans le volet de **hiérarchie** :
    * Ressources/HoloToolkit/entrée/Prefabs/**MixedRealityCamera**
    * Ressources/AppPrefabs/**environnement**

![Appareil photo et environnement](images/mr213-cameraenvironment-300px.jpg)
* Il existe deux prefabs d’appareil photo dans Mixed Reality Toolkit:
    * **MixedRealityCamera. Prefab**: Appareil photo uniquement
    * **MixedRealityCameraParent. Prefab**: Appareil photo + téléportage + limite
    * Dans ce didacticiel, nous allons utiliser **MixedRealityCamera** sans la fonctionnalité de téléportage. Pour cette raison, nous avons ajouté un Prefab d' **environnement** simple qui contient un étage de base pour que l’utilisateur ait le sentiment de la terre.
    * Pour en savoir plus sur la téléportage avec **MixedRealityCameraParent**, consultez [conception avancée-téléportage et locomotion](#advanced-design---teleportation-and-locomotion)

**Installation de skybox**
* Cliquez sur **fenêtre > éclairage > paramètres**
* Cliquez sur le cercle sur le côté droit du **champ de matériau skybox** .
* Tapez «Gray» et sélectionnez **SkyboxGray**

(Ressources/AppPrefabs/support/Materials/SkyboxGray. mat)

![Définition de skybox](images/mr123-skyboxsetting-400px.jpg)
* Cochez l’option **skybox** pour afficher le dégradé gris affecté skybox

![Activer/désactiver l’option skybox](images/mr213-skyboxcheck-400px.jpg)
* La scène avec MixedRealityCamera, Environment et Gray skybox ressemblera à ce qui suit.

![Environnement MixedReality213](images/mr213-environment-600px.jpg)
* Cliquez sur **fichier > enregistrer la scène sous**
* **Enregistrez** votre scène sous le dossier scenes avec n’importe quel nom

## <a name="chapter-1---controller-visualization"></a>Chapitre 1-visualisation du contrôleur

>[!VIDEO https://www.youtube.com/embed/Kw0bf5NqyRg]

### <a name="objectives"></a>Objectifs

* Découvrez comment restituer les modèles de contrôleur de mouvement en mode jeu Unity et au moment de l’exécution.

Windows Mixed Reality fournit un modèle de contrôleur animé pour la visualisation du contrôleur. Vous pouvez prendre plusieurs approches pour la visualisation du contrôleur dans votre application:
* Par défaut-utilisation du contrôleur par défaut sans modification
* Hybride: à l’aide du contrôleur par défaut, mais en personnalisant certains de ses éléments ou en superposant des composants d’interface utilisateur
* Remplacement: utilisation de votre propre modèle 3D personnalisé pour le contrôleur

Dans ce chapitre, nous allons découvrir les exemples de ces personnalisations de contrôleur.

### <a name="instructions"></a>Instructions

* Dans le panneau **projet** , tapez **MotionControllers** dans la zone de recherche. Vous pouvez également le trouver sous ressources/HoloToolkit/entrée/Prefabs/.
* Faites glisser le Prefab **MotionControllers** dans le panneau de la **hiérarchie** .
* Cliquez sur le Prefab **MotionControllers** dans le panneau **hiérarchie** .

**MotionControllers Prefab**

**MotionControllers** Prefab a un script **MotionControllerVisualizer** qui fournit les emplacements pour les autres modèles de contrôleur. Si vous affectez vos propres modèles 3D personnalisés, tels qu’une main ou un épée, et que vous activez la case à cocher «toujours utiliser le modèle de remplacement gauche/droit», vous les verrez à la place du modèle par défaut. Nous allons utiliser cet emplacement dans le chapitre 4 pour remplacer le modèle de contrôleur par un pinceau.

![MR213_ControllerVisualizer](images/mr213-controllervisualizer-600px.png)

**Instructions**
* Dans le panneau **inspecteur** , double-cliquez sur **MotionControllerVisualizer** script pour afficher le code dans Visual Studio.

**Script MotionControllerVisualizer**

Les classes **MotionControllerVisualizer** et **MotionControllerInfo** fournissent les moyens d’accéder à & de modifier les modèles de contrôleur par défaut. **MotionControllerVisualizer** s’abonne à l’événement **InteractionSourceDetected** de Unity et instancie automatiquement les modèles de contrôleur lorsqu’ils sont trouvés.

```cs
protected override void Awake()
{
    ...
    InteractionManager.InteractionSourceDetected += InteractionManager_InteractionSourceDetected;
    InteractionManager.InteractionSourceLost += InteractionManager_InteractionSourceLost;
    ...
}
```

Les modèles de contrôleur sont fournis conformément à [la spécification glTF](https://github.com/KhronosGroup/glTF). Ce format a été créé pour fournir un format commun, tout en améliorant le processus de transmission et de décompression des ressources 3D. Dans ce cas, nous devons récupérer et charger les modèles de contrôleur lors de l’exécution, car nous souhaitons que l’expérience de l’utilisateur soit aussi transparente que possible, et il n’est pas garanti que la version des contrôleurs de mouvement que l’utilisateur utilise. Ce cours, via le kit d’outils de réalité mixte, utilise une version du [projet UnityGLTF](https://github.com/KhronosGroup/UnityGLTF)du groupe Khronos.

Une fois le contrôleur remis, les scripts peuvent utiliser **MotionControllerInfo** pour rechercher les transformations pour des éléments de contrôleur spécifiques afin qu’ils puissent se positionner correctement.

Dans un chapitre ultérieur, nous allons apprendre à utiliser ces scripts pour attacher des éléments d’interface utilisateur aux contrôleurs.

*Dans certains scripts, vous trouverez des blocs de code avec **#if! UNITY_EDITOR** ou **UNITY_WSA**. Ces blocs de code s’exécutent uniquement sur le runtime UWP quand vous déployez sur Windows. Cela est dû au fait que l’ensemble d’API utilisé par l’éditeur Unity et le runtime d’application UWP sont différents.*
* **Enregistrez** la scène, puis cliquez sur le bouton **lecture** .

Vous pourrez voir la scène avec des contrôleurs de mouvement dans votre casque. Vous pouvez voir des animations détaillées pour les clics de bouton, le mouvement du joystick et la mise en surbrillance des touches tactiles.

![MR213_Controller visualisation par défaut](images/mr213-controllervisualizationdefault-500px.jpg)

## <a name="chapter-2---attaching-ui-elements-to-the-controller"></a>Chapitre 2-attachement des éléments d’interface utilisateur au contrôleur

>[!VIDEO https://www.youtube.com/embed/e-mLlwmTzJo]

### <a name="objectives"></a>Objectifs

* En savoir plus sur les éléments des contrôleurs de mouvement
* Découvrez comment attacher des objets à des parties spécifiques des contrôleurs

Dans ce chapitre, vous allez apprendre à ajouter des éléments d’interface utilisateur au contrôleur que l’utilisateur peut facilement accéder et manipuler à tout moment. Vous allez également apprendre à ajouter une interface utilisateur de sélecteur de couleurs simple à l’aide de l’entrée du pavé tactile.

### <a name="instructions"></a>Instructions

* Dans le panneau **projet** , recherchez script **MotionControllerInfo** .
* Dans le résultat de la recherche, double-cliquez sur le script **MotionControllerInfo** pour afficher le code dans Visual Studio.

**Script MotionControllerInfo**

La première étape consiste à choisir l’élément du contrôleur auquel vous souhaitez attacher l’interface utilisateur. Ces éléments sont définis dans **ControllerElementEnum** dans **MotionControllerInfo.cs**.

![MR213 MotionControllerElements](images/mr213-motioncontrollerelements-1000px.jpg)
* **Accueil**
* **Menu**
* **Maîtriser**
* **Stick**
* **Sélectionné**
* **Pavé tactile**
* **Pose** de pointage: cet élément représente l’extrémité du point de contrôle de direction vers l’avant.

**Instructions**
* Dans le panneau **projet** , recherchez script **AttachToController** .
* Dans le résultat de la recherche, double-cliquez sur le script **AttachToController** pour afficher le code dans Visual Studio.

**Script AttachToController**

Le script **AttachToController** offre un moyen simple d’attacher des objets à un élément et un élément de contrôle.

Dans **AttachElementToController ()** ,
* Vérifier la main à l’aide de **MotionControllerInfo. main**
* Obtient un élément spécifique du contrôleur à l’aide de **MotionControllerInfo. TryGetElement ()**
* Après avoir récupéré la transformation de l’élément à partir du modèle de contrôleur, mettez-y le parent de l’objet et définissez position locale de l’objet & la rotation sur zéro.

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

La façon la plus simple d’utiliser le script **AttachToController** est d’en hériter, comme nous l’avons fait dans le cas de **ColorPickerWheel.** Remplacez simplement les fonctions **OnAttachToController** et **OnDetatchFromController** pour effectuer votre configuration/répartition lorsque le contrôleur est détecté/déconnecté.

**Instructions**
* Dans le panneau **projet** , tapez dans la zone de recherche **ColorPickerWheel**. Vous pouvez également le trouver sous ressources/AppPrefabs/.
* Faites glisser **ColorPickerWheel** Prefab dans le panneau de **hiérarchie** .
* Cliquez sur le Prefab **ColorPickerWheel** dans le panneau **hiérarchie** .
* Dans le panneau **inspecteur** , double-cliquez sur **ColorPickerWheel** script pour afficher le code dans Visual Studio.

![ColorPickerWheel Prefab](images/mr213-colorpickerwheel-1000px.jpg)

**Script ColorPickerWheel**

Étant donné que **ColorPickerWheel** hérite de **AttachToController**, il affiche la **main** et l' **élément** dans le panneau de l' **inspecteur** . Nous allons attacher l’interface utilisateur à l’élément Touchpad sur le contrôleur de gauche.

![Script ColorPickerWheel](images/mr213-attachtocontroller-300px.jpg)

**ColorPickerWheel** remplace les **OnAttachToController** et **OnDetatchFromController** pour s’abonner à l’événement d’entrée qui sera utilisé dans le chapitre suivant pour la sélection des couleurs avec l’entrée du pavé tactile.

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
* **Enregistrez** la scène, puis cliquez sur le bouton **lecture** .

**Autre méthode pour attacher des objets aux contrôleurs**

Nous recommandons que vos scripts héritent de **AttachToController** et remplacent **OnAttachToController**. Toutefois, cela n’est pas toujours possible. Une alternative consiste à l’utiliser comme un composant autonome. Cela peut être utile lorsque vous souhaitez attacher un Prefab existant à un contrôleur sans Refactoriser vos scripts. Faites simplement en sorte que votre classe attende que IsAttached, soit défini sur true avant d’effectuer une installation. Pour ce faire, la méthode la plus simple consiste à utiliser une Coroutine pour «Start».

```cs
private IEnumerator Start() {
    AttachToController attach = gameObject.GetComponent<AttachToController>();

    while (!attach.IsAttached) {
        yield return null;
    }

    // Perform setup here
}
```

## <a name="chapter-3---working-with-touchpad-input"></a>Chapitre 3-utilisation de l’entrée du pavé tactile

>[!VIDEO https://www.youtube.com/embed/SUyw0kxZPFw]

### <a name="objectives"></a>Objectifs

* Découvrez comment obtenir des événements de données d’entrée dans le pavé tactile
* Découvrez comment utiliser les informations de position de l’axe du pavé tactile pour votre expérience d’application

### <a name="instructions"></a>Instructions

* Dans le volet **hiérarchie** , cliquez sur **ColorPickerWheel**
* Dans le panneau **inspecteur** , sous **Animatior**, double-cliquez sur **ColorPickerWheelController**
* Vous pourrez voir l’onglet **animation** ouvert

**Montrer/masquer l’interface utilisateur avec le contrôleur d’animation Unity**

Pour afficher et masquer l’interface utilisateur **ColorPickerWheel** avec l’animation, nous utilisons le [système d’animation Unity](https://docs.unity3d.com/Manual/AnimationOverview.html). L’affectation de la valeur true ou false aux déclencheurs de la propriété **visible** de **ColorPickerWheel** **affiche** et **masque** les déclencheurs d’animation. Les paramètres d' **affichage** et de **masquage** sont définis dans le contrôleur d’animation **ColorPickerWheelController** .

![Contrôleur d’animation Unity](images/mr123-animationcontroller-550px.jpg)

**Instructions**
* Dans le volet **hiérarchie** , sélectionnez **ColorPickerWheel** Prefab
* Dans le panneau **inspecteur** , double-cliquez sur **ColorPickerWheel** script pour afficher le code dans Visual Studio.

**Script ColorPickerWheel**

**ColorPickerWheel** s’abonne à l’événement **InteractionSourceUpdated** d’Unity pour écouter les événements du pavé tactile.

Dans **InteractionSourceUpdated ()** , le script commence par vérifier qu’il:
* est en fait un événement de pavé tactile (obj. State). **touchpadTouched**)
* provient du contrôleur gauche (obj. State. source). **droitier**)

Si les deux ont la valeur true, la position du pavé tactile (obj. State. **touchpadPosition**) est assignée à **selectorPosition**.

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

Dans **Update ()** , en fonction de la propriété **visible** , elle déclenche les déclencheurs d’animation afficher et masquer dans le composant d’animation du sélecteur de couleurs

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

Dans **Update ()** , **selectorPosition** est utilisé pour effectuer un cast d’un rayon au niveau du conflit de maillage de la roue de couleur, qui retourne une position UV. Cette position peut ensuite être utilisée pour rechercher la coordonnée de pixels et la valeur de couleur de la texture de la roue chromatique. Cette valeur est accessible aux autres scripts via la propriété **SelectedColor** .

![Roulette du sélecteur de couleurs Raycasting](images/mr213-colorpickerwheel-raycast-700px.png)

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

## <a name="chapter-4---overriding-controller-model"></a>Chapitre 4-remplacement du modèle de contrôleur

>[!VIDEO https://www.youtube.com/embed/8gBFqA_DZ_U]

### <a name="objectives"></a>Objectifs

* Découvrez comment remplacer le modèle de contrôleur par un modèle 3D personnalisé.

![MR213_BrushToolOverride](images/mr213-brushtooloverride-500px.jpg)

### <a name="instructions"></a>Instructions

* Dans le volet **hiérarchie** , cliquez sur **MotionControllers** .
* Cliquez sur le cercle sur le côté droit du champ **autre contrôleur de droite** .
* Tapez **«BrushController**» et sélectionnez Prefab dans le résultat. Vous pouvez le trouver sous actifs/AppPrefabs/**BrushController**.
* Cochez **toujours utiliser le modèle de remplacement à droite**

![MR213_BrushToolOverrideSlot](images/mr213-motioncontrollersoverride-700px.jpg)

Le Prefab **BrushController** ne doit pas être inclus dans le panneau de **hiérarchie** . Toutefois, pour extraire ses composants enfants:
* Dans le panneau **projet** , tapez **BrushController** et faites glisser **BrushController** Prefab dans le volet **hiérarchie** .

![MR213_BrushTool_Prefab2](images/mr213-brushtool-prefab-1000px.jpg)

Vous trouverez le composant **Tip** dans **BrushController**. Nous allons utiliser sa transformation pour démarrer/arrêter le dessin de lignes.
* Supprimez le **BrushController** du panneau de la **hiérarchie** .
* **Enregistrez** la scène, puis cliquez sur le bouton **lecture** . Vous serez en mesure de voir que le modèle de pinceau a remplacé le contrôleur de mouvement de droite.

## <a name="chapter-5---painting-with-select-input"></a>Chapitre 5-peinture avec l’entrée Select

>[!VIDEO https://www.youtube.com/embed/QTrYaMHIs7w]

### <a name="objectives"></a>Objectifs

* Découvrez comment utiliser l’événement bouton Sélectionner pour démarrer et arrêter un dessin de ligne

### <a name="instructions"></a>Instructions

* Recherchez **BrushController** Prefab dans le panneau **projet** .
* Dans le panneau **inspecteur** , double-cliquez sur **BrushController** script pour afficher le code dans Visual Studio

**Script BrushController**

**BrushController** s’abonne aux événements **InteractionSourcePressed** et **InteractionSourceReleased** du InteractionManager. Lorsque l’événement **InteractionSourcePressed** est déclenché, la propriété **Draw** du pinceau est définie sur true; Lorsque l’événement **InteractionSourceReleased** est déclenché, la propriété **Draw** du pinceau est définie sur false.

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

Bien que **Draw** ait la valeur true, le pinceau génère des points dans une Unity **LineRenderer**instanciée. Une référence à ce Prefab est conservée dans le champ **Stroke Prefab** du pinceau.

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

Pour utiliser la couleur actuellement sélectionnée à partir de l’interface utilisateur de la roue du sélecteur de couleurs, **BrushController** doit avoir une référence à l’objet **ColorPickerWheel** . Étant donné que le Prefab **BrushController** est instancié au moment de l’exécution en tant que contrôleur de remplacement, toutes les références aux objets de la scène doivent être définies au moment de l’exécution. Dans ce cas, nous utilisons **GameObject. FindObjectOfType** pour localiser le **ColorPickerWheel**:

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
* **Enregistrez** la scène, puis cliquez sur le bouton **lecture** . Vous pourrez dessiner les lignes et peindre à l’aide du bouton Sélectionner sur le contrôleur de droite.

## <a name="chapter-6---object-spawning-with-select-input"></a>Chapitre 6-génération d’objets avec sélection d’entrée

>[!VIDEO https://www.youtube.com/embed/z4IxyzFHP0U]

### <a name="objectives"></a>Objectifs

* Découvrez comment utiliser les événements d’entrée de bouton Sélectionner et ressaisir
* Apprendre à instancier des objets

### <a name="instructions"></a>Instructions

* Dans le panneau **projet** , tapez **ObjectSpawner** dans la zone de recherche. Vous pouvez également le trouver sous ressources/AppPrefabs/
* Faites glisser le Prefab **ObjectSpawner** dans le panneau de la **hiérarchie** .
* Dans le volet **hiérarchie** , cliquez sur **ObjectSpawner** .
* **ObjectSpawner** a un champ nommé **Color source**.
* À partir du panneau **hiérarchie** , faites glisser la référence **ColorPickerWheel** dans ce champ.

![Inspecteur du Spawn d’objets](images/mr213-objectspawnercolorpickerwheel-650px.jpg)
* Cliquez sur le Prefab **ObjectSpawner** dans le panneau **hiérarchie** .
* Dans le panneau **inspecteur** , double-cliquez sur **ObjectSpawner** script pour afficher le code dans Visual Studio.

**Script ObjectSpawner**

Le **ObjectSpawner** instancie des copies d’un maillage primitif (cube, sphère, cylindre) dans l’espace. Lorsqu’un **InteractionSourcePressed** est détecté, il vérifie la main et s’il s’agit d’un événement **InteractionSourcePressType.** dispose ou **InteractionSourcePressType. Select** .

Pour un événement **saisissant** , il incrémente l’index du type de maillage actuel (Sphere, cube, Cylinder)

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

Dans le cas d’un événement **Select** , dans **SpawnObject ()** , un nouvel objet est instancié, non apparenté et libéré dans le monde.

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

**ObjectSpawner** utilise **ColorPickerWheel** pour définir la couleur du matériau de l’objet d’affichage. Les objets générés reçoivent une instance de ce document, de sorte qu’ils conservent leur couleur.
* **Enregistrez** la scène, puis cliquez sur le bouton **lecture** .

Vous pouvez modifier les objets avec le bouton de sélection et générer des objets à l’aide du bouton Sélectionner.

## <a name="build-and-deploy-app-to-mixed-reality-portal"></a>Créer et déployer une application sur un portail de réalité mixte
* Dans Unity, sélectionnez **fichier > paramètres de build**.
* Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène actuelle aux **scènes dans la build**.
* Cliquez sur **Build**.
* Créez un **dossier** nommé «App».
* Cliquez sur le dossier de l' **application** .
* Cliquez sur **Sélectionner un dossier**.
* Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.
* Ouvrez le dossier de l' **application** .
* Double-cliquez sur le fichier solution Visual Studio **YourSceneName. sln** .
* À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.
* Cliquez sur la flèche déroulante en regard du bouton périphérique, puis sélectionnez **ordinateur local**.
* Cliquez sur déboguer **-> exécuter sans débogage** dans le menu ou appuyez sur **CTRL + F5**.

L’application est désormais générée et installée dans le portail de réalité mixte. Vous pouvez le relancer par le biais du menu Démarrer dans le portail de réalité mixte.

## <a name="advanced-design---brush-tools-with-radial-layout"></a>Outils de conception avancée avec disposition radiale

![Main MixedReality213](images/mr213-main-600px.jpg)

Dans ce chapitre, vous allez apprendre à remplacer le modèle de contrôleur de mouvement par défaut par une collection d’outils de pinceau personnalisée. Pour référence, vous pouvez trouver la scène terminée **MixedReality213Advanced** sous le  dossier Scenes.

### <a name="instructions"></a>Instructions

* Dans le panneau **projet** , tapez **BrushSelector** dans la zone de recherche. Vous pouvez également le trouver sous ressources/AppPrefabs/
* Faites glisser le Prefab **BrushSelector** dans le panneau de la **hiérarchie** .
* Pour l’organisation, créez un GameObject vide  appelé pinceaux
* Faites glisser les prefabs suivants du panneau **projet** vers les **pinceaux**
    * Ressources/AppPrefabs/**BrushFat**
    * Ressources/AppPrefabs/**BrushThin**
    * Ressources/AppPrefabs/**gomme**
    * Ressources/AppPrefabs/**MarkerFat**
    * Ressources/AppPrefabs/**MarkerThin**
    * Ressources/AppPrefabs/**crayon**

![Pinceaux](images/mixedreality213-brushes-250px.png)
* Dans le volet **hiérarchie** , cliquez sur **MotionControllers** Prefab.
* Dans le panneau de l' **inspecteur** , décochez **toujours utiliser le modèle de remplacement à droite** sur le visualiseur du contrôleur de **mouvement** .
* Dans le volet **hiérarchie** , cliquez sur **BrushSelector**
* **BrushSelector** a un champ nommé **ColorPicker**
* À partir du panneau **hiérarchie** , faites glisser le champ **ColorPickerWheel** dans **ColorPicker** dans le panneau **inspecteur** .

![Assigner ColorPickerWheel à un sélecteur de pinceau](images/mr213-brushselector-500px.jpg)
* Dans le panneau **hiérarchie** , sous **BrushSelector** Prefab, sélectionnez l’objet **menu** .
* Dans le volet de l' **inspecteur** , sous le composant **LineObjectCollection** , ouvrez la liste déroulante tableau d' **objets** . Vous verrez 6 emplacements vides.
* Dans le volet **hiérarchie** , faites glisser chaque prefabs apparenté sous les pinceaux  gameobject dans n’importe quel ordre. (Assurez-vous de faire glisser le prefabs à partir de la scène, et non prefabs dans le dossier du projet.)

![Sélecteur de pinceau](images/mr213-brushselectorbrushes-700px.jpg)

**BrushSelector Prefab**

Étant donné que **BrushSelector** hérite de **AttachToController**, il affiche les options de **remise** et d' **élément** dans le panneau **inspecteur** . Nous avons sélectionné la **pose** de **droite** et de pointage pour attacher les outils de pinceau au contrôleur de droite avec la direction vers l’avant.

Le **BrushSelector** utilise deux utilitaires:
* **Ellipse**: utilisée pour générer des points dans l’espace le long d’une forme d’ellipse.
* **LineObjectCollection**: distribue les objets à l’aide des points générés par n’importe quelle classe de lignes (par ex., ellipse). C’est ce que nous allons utiliser pour placer nos pinceaux le long de la forme d’ellipse.

Lorsqu’ils sont combinés, ces utilitaires peuvent être utilisés pour créer un menu radial.

**Script LineObjectCollection**

**LineObjectCollection** possède des contrôles pour la taille, la position et la rotation des objets distribués le long de la ligne. Cela est utile pour créer des menus radiaux tels que le sélecteur de pinceau. Pour créer l’apparence des pinceaux qui s’ajustent à partir de rien, car ils approchent la position sélectionnée au centre, les pics de la courbe **ObjectScale** dans les bords du centre et des bandes.

**Script BrushSelector**

Dans le cas de **BrushSelector**, nous avons choisi d’utiliser l’animation procédurale. Tout d’abord, les modèles de pinceau sont distribués dans une ellipse par le script **LineObjectCollection** . Ensuite, chaque pinceau est chargé de conserver sa position dans la main de l’utilisateur en fonction de sa valeur **DisplayMode** , qui change en fonction de la sélection. Nous avons choisi une approche procédurale en raison de la probabilité élevée que les transitions de position de pinceau soient interrompues lorsque l’utilisateur sélectionne des pinceaux. Les animations Mecanim peuvent gérer les interruptions de manière appropriée, mais elles ont tendance à être plus compliquées qu’une simple opération Lerp.

**BrushSelector** utilise une combinaison des deux. Lorsque l’entrée de pavé tactile est détectée, les options de pinceau deviennent visibles et évoluent le long du menu radial. Après un délai d’expiration (qui indique que l’utilisateur a effectué une sélection), les options de pinceau remontent d’une nouvelle échelle, en laissant uniquement le pinceau sélectionné.

**Visualisation de l’entrée du pavé tactile**

Même dans les cas où le modèle de contrôleur a été complètement remplacé, il peut être utile d’afficher l’entrée sur les entrées du modèle d’origine. Cela permet de reconstituer les actions de l’utilisateur en réalité. Pour le **BrushSelector** , nous avons choisi de rendre le pavé tactile brièvement visible lors de la réception de l’entrée. Pour ce faire, récupérez l’élément de pavé tactile à partir du contrôleur, en remplaçant son matériau par un matériau personnalisé, puis en appliquant un dégradé à la couleur de ce matériau en fonction de la dernière entrée de pavé tactile reçue.

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

**Sélection de l’outil pinceau avec entrée de pavé tactile**

Lorsque le sélecteur de pinceau détecte l’entrée appuyée du pavé tactile, il vérifie la position de l’entrée pour déterminer si elle se trouvait à gauche ou à droite.

**Épaisseur du trait avec selectPressedAmount**

Au lieu de l’événement **InteractionSourcePressType. Select** dans le **InteractionSourcePressed ()** , vous pouvez récupérer la valeur analogique du montant appuyé par le biais de **selectPressedAmount**. Cette valeur peut être extraite dans **InteractionSourceUpdated ()** .

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

**Gomme** est un type spécial de pinceau qui remplace la fonction **DrawOverTime ()** du **pinceau**de base. Bien que Draw ait la valeur true, la gomme vérifie si son info-bulle croise les traits de pinceau existants. Si c’est le cas, ils sont ajoutés à une file d’attente pour être réduits et supprimés.

## <a name="advanced-design---teleportation-and-locomotion"></a>Conception avancée-téléportage et locomotion

Si vous souhaitez autoriser l’utilisateur à se déplacer dans la scène avec la téléportage à l’aide du stick analogique, utilisez **MixedRealityCameraParent** au lieu de **MixedRealityCamera**. Vous devez également ajouter **InputManager** et **DefaultCusor**. Étant donné que **MixedRealityCameraParent** contient déjà des **MotionControllers** et des **limites** en tant que composants enfants, vous devez supprimer les Prefab de **MotionControllers** et d' **environnement** existants.

### <a name="instructions"></a>Instructions

* Dans le volet **hiérarchie** , supprimez **MixedRealityCamera**, **Environment** et **MotionControllers**
* Dans le **volet de projet**, recherchez et faites glisser le prefabs suivant dans le volet de **hiérarchie** :
    * Ressources/AppPrefabs/entrée/Prefabs/**MixedRealityCameraParent**
    * Ressources/AppPrefabs/entrée/Prefabs/**InputManager**
    * Ressources/AppPrefabs/entrée/Prefabs/Cursor/**DefaultCursor**

![Parent de la caméra de réalité mixte](images/mr213-cameraparent-300px.png)
* Dans le volet **hiérarchie** , cliquez sur **Gestionnaire d’entrée** .
* Dans le volet de l' **inspecteur** , faites défiler jusqu’à la section du **Sélecteur de pointeur simple simple**
* À partir du panneau **hiérarchie** , faites glisser **DefaultCursor** dans le champ **Cursor**

![Attribution de DefaultCursor](images/mr213-defaultcursor-500px.png)
* **Enregistrez** la scène, puis cliquez sur le bouton **lecture** . Vous serez en mesure d’utiliser le stick analogique pour faire pivoter vers la gauche/droite ou la téléporter.

## <a name="the-end"></a>La fin

Et c’est la fin de ce didacticiel. Vous avez appris à:
* Comment utiliser les modèles de contrôleur de mouvement dans le mode jeu et le runtime d’Unity.
* Comment utiliser différents types d’événements de bouton et leurs applications.
* Comment superposer des éléments d’interface utilisateur en plus du contrôleur ou le personnaliser entièrement.

Vous êtes maintenant prêt à commencer à créer votre propre expérience immersive avec les contrôleurs motion.

## <a name="completed-scenes"></a>Scènes terminées

* Dans le panneau **projet** d’Unity,  cliquez sur le dossier Scenes.
* Vous trouverez deux Unity Sceens **MixedReality213** et **MixedReality213Advanced**.
    * **MixedReality213**: Scène terminée avec un seul pinceau
    * **MixedReality213Advanced**: Scène terminée avec un pinceau multiple avec l’exemple de montant de pression du bouton Sélectionner

## <a name="see-also"></a>Voir aussi

* [Fichiers projet d’entrée 213](https://github.com/Microsoft/MixedReality213)
* [Boîte à outils de réalité mixte-scène de test du contrôleur de mouvement](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/Input/Scenes)
* [Kit de pratiques de réalité mixte-mécanisme de manipulation](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/MotionControllers-GrabMechanics)
* [Instructions de développement du contrôleur motion](motion-controllers.md)
