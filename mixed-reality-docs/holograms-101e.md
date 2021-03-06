---
title: Notions de base de 101E-projet complet avec l’émulateur
description: Suivez cette procédure pas à pas de codage à l’aide d’Unity, de Visual Studio et de l’émulateur HoloLens pour apprendre les principes de base d’une application holographique.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: réalité mixte, Windows Mixed Reality, HoloLens, hologramme, Academy, didacticiel, émulateur
ms.openlocfilehash: b1d8e1f3f272051bdd6f69ab88c3aef4f86f13ef
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434702"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. [Une nouvelle série de didacticiels](mrlearning-base.md) a été publiée pour HoloLens 2.

<br>

# <a name="mr-basics-101e-complete-project-with-emulator"></a>Notions de base de 101E : projet complet avec l’émulateur

 >[!VIDEO https://www.youtube.com/embed/Xzm8_s05mm8]

Ce didacticiel vous guide tout au long d’un projet complet, Unity, qui illustre les fonctionnalités de base de la réalité mixte Windows sur HoloLens [, y compris](gaze-and-commit.md)le point de présence, les [gestes](gaze-and-commit.md#composite-gestures), l' [entrée vocale](voice-input.md), le [son spatial](spatial-sound.md) et le [mappage spatial](spatial-mapping.md) . Le didacticiel prendra environ 1 heure.

## <a name="device-support"></a>Périphériques pris en charge

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>Notions de base de 101E : projet complet avec l’émulateur</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Conditions préalables

* Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).

### <a name="project-files"></a>Fichiers projet

* Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) requis par le projet. Requiert Unity 2017,2 ou une version ultérieure.
  * Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).
  * Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).
  * Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).
* Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre. Conservez le nom du dossier **origami**.

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).

## <a name="chapter-1---holo-world"></a>Chapitre 1-monde « Holo »

>[!VIDEO https://www.youtube.com/embed/qotpUpIQxVU]

Dans ce chapitre, nous allons configurer notre premier projet Unity et effectuer un pas à pas détaillé dans le processus de création et de déploiement.

### <a name="objectives"></a>Objectifs

* Configurez Unity pour le développement holographique.
* Créez un hologramme.
* Consultez un hologramme que vous avez créé.

### <a name="instructions"></a>Instructions

* Démarrez Unity.
* Sélectionnez **ouvrir**.
* Entrez l’emplacement du dossier **origami** que vous avez précédemment désinstallé.
* Sélectionnez **origami** , puis cliquez sur **Sélectionner un dossier**.
* Enregistrez la nouvelle scène : **fichier** / **enregistrer la scène sous**.
* Nommez la scène **origami** et appuyez sur le bouton **Enregistrer** .

#### <a name="setup-the-main-camera"></a>Configurer la caméra principale

* Dans le **panneau hiérarchie**, sélectionnez **caméra principale**.
* Dans l' **inspecteur** , définissez sa position de transformation sur **0, 0,** 0.
* Recherchez la propriété **effacer les indicateurs** et remplacez la liste déroulante **skybox** par **couleur unie**.
* Cliquez sur le champ **arrière-plan** pour ouvrir un sélecteur de couleurs.
* Affectez **R, G, B et A** à **0**.

#### <a name="setup-the-scene"></a>Configurer la scène

* Dans le **volet hiérarchie**, cliquez sur **créer** et **créez un vide**.
* Cliquez avec le bouton droit sur le nouveau **gameobject** , puis sélectionnez Renommer. Renommez GameObject en **OrigamiCollection**.
* Dans le dossier **hologrammes** du **panneau Projet**:
  * Faites glisser **étape** dans la hiérarchie pour être un enfant de **OrigamiCollection**.
  * Faites glisser **Sphere1** dans la hiérarchie pour être un enfant de **OrigamiCollection**.
  * Faites glisser **Sphere2** dans la hiérarchie pour être un enfant de **OrigamiCollection**.
* Cliquez avec le bouton droit sur l’objet **Light directionnel** dans le **panneau hiérarchie** , puis sélectionnez **supprimer**.
* À partir du dossier **hologrammes** , faites glisser **Lights** à la racine du **panneau de hiérarchie**.
* Dans la **hiérarchie**, sélectionnez **OrigamiCollection**.
* Dans l' **inspecteur**, définissez la position de la transformation sur **0,-0,5, 2,0**.
* Appuyez sur le bouton de **lecture** dans Unity pour afficher un aperçu de vos hologrammes.
* Les objets origami doivent apparaître dans la fenêtre d’aperçu.
* Appuyez sur **lecture** une deuxième fois pour arrêter le mode aperçu.

#### <a name="export-the-project-from-unity-to-visual-studio"></a>Exporter le projet d’Unity vers Visual Studio

* Dans Unity, sélectionnez **fichier > paramètres de build**.
* Sélectionnez **Windows Store** dans la liste **plateforme** , puis cliquez sur **basculer la plateforme**.
* Affectez à **SDK** la valeur **Universal 10** et **type de build** la valeur **D3D**.
* Vérifiez **les C# projets Unity**.
* Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.
* Cliquez sur **paramètres du lecteur...** .
* Dans le panneau de l’inspecteur, sélectionnez le **logo du Windows Store**. Sélectionnez ensuite **paramètres de publication**.
* Dans la section **fonctionnalités** , sélectionnez les fonctionnalités **microphone** et **SpatialPerception** .
* De retour dans la fenêtre Paramètres de build, cliquez sur **générer**.
* Créez un **dossier** nommé « App ».
* Cliquez sur le **dossier**de l’application.
* Appuyez sur **Sélectionner un dossier**.
* Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.
* Ouvrez le dossier de l' **application** .
* Ouvrez la **solution Visual Studio origami**.
* À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.
  * Cliquez sur la flèche en regard du bouton périphérique, puis sélectionnez **émulateur HoloLens**.
  * Cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
  * Après un certain temps, l’émulateur démarrera avec le projet origami. Lors du premier lancement de l' [émulateur](using-the-hololens-emulator.md), le démarrage de l’émulateur peut prendre jusqu’à 15 minutes. Une fois qu’il a démarré, ne le fermez pas.

## <a name="chapter-2---gaze"></a>Chapitre 2-point de regard

>[!VIDEO https://www.youtube.com/embed/BPWTbAC210k]

Dans ce chapitre, nous allons présenter la première des trois façons d’interagir avec vos hologrammes, en pointant le [regard](gaze-and-commit.md).

### <a name="objectives"></a>Objectifs

* Visualisez votre point de regard à l’aide d’un curseur verrouillé.

### <a name="instructions"></a>Instructions

* Revenez à votre projet Unity et fermez la fenêtre Paramètres de build si elle est toujours ouverte.
* Sélectionnez le dossier **hologrammes** dans le **panneau Projet**.
* Faites glisser l’objet **curseur** dans le volet de la **hiérarchie** au niveau de la racine.
* Double-cliquez sur l’objet **curseur** pour l’examiner en détail.
* Cliquez avec le bouton droit sur le dossier **scripts** dans le panneau projet.
* Cliquez sur le sous-menu **créer** .
* Sélectionnez  **C# script**.
* Nommez le script **WorldCursor**. Remarque : le nom respecte la casse. Vous n’avez pas besoin d’ajouter l’extension. cs.
* Sélectionnez l’objet **curseur** dans le **panneau hiérarchie**.
* Glissez-déplacez le script **WorldCursor** dans le panneau de l' **inspecteur**.
* Double-cliquez sur le script **WorldCursor** pour l’ouvrir dans Visual Studio.
* Copiez et collez ce code dans **WorldCursor.cs** et **Enregistrez All**.

```cs
using UnityEngine;

public class WorldCursor : MonoBehaviour
{
    private MeshRenderer meshRenderer;

    // Use this for initialization
    void Start()
    {
        // Grab the mesh renderer that's on the same object as this script.
        meshRenderer = this.gameObject.GetComponentInChildren<MeshRenderer>();
    }

    // Update is called once per frame
    void Update()
    {
        // Do a raycast into the world based on the user's
        // head position and orientation.
        var headPosition = Camera.main.transform.position;
        var gazeDirection = Camera.main.transform.forward;

        RaycastHit hitInfo;

        if (Physics.Raycast(headPosition, gazeDirection, out hitInfo))
        {
            // If the raycast hit a hologram...
            // Display the cursor mesh.
            meshRenderer.enabled = true;

            // Move thecursor to the point where the raycast hit.
            this.transform.position = hitInfo.point;

            // Rotate the cursor to hug the surface of the hologram.
            this.transform.rotation = Quaternion.FromToRotation(Vector3.up, hitInfo.normal);
        }
        else
        {
            // If the raycast did not hit a hologram, hide the cursor mesh.
            meshRenderer.enabled = false;
        }
    }
}
```

* Régénérez l’application à partir du **fichier > paramètres de build**.
* Revenez à la solution Visual Studio utilisée précédemment pour le déploiement sur l’émulateur.
* Lorsque vous y êtes invité, sélectionnez « recharger tout ».
* Cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
* Utilisez le contrôleur Xbox pour parcourir la scène. Notez que le curseur interagit avec la forme d’objets.

## <a name="chapter-3---gestures"></a>Chapitre 3-mouvements

>[!VIDEO https://www.youtube.com/embed/6d-0RHeKHq4]

Dans ce chapitre, nous allons ajouter la prise en charge des [gestes](gaze-and-commit.md#composite-gestures). Lorsque l’utilisateur sélectionne une sphère papier, nous allons faire tomber la sphère en activant la gravité en utilisant le moteur physique Unity.

### <a name="objectives"></a>Objectifs

* Contrôlez vos hologrammes avec le geste Select.

### <a name="instructions"></a>Instructions

Nous allons commencer par créer un script que peut détecter le mouvement Select.

* Dans le dossier **scripts** , créez un script nommé **GazeGestureManager**.
* Faites glisser le script **GazeGestureManager** sur l’objet **OrigamiCollection** dans la hiérarchie.
* Ouvrez le script **GazeGestureManager** dans Visual Studio et ajoutez le code suivant :

```cs
using UnityEngine;
using UnityEngine.XR.WSA.Input;

public class GazeGestureManager : MonoBehaviour
{
    public static GazeGestureManager Instance { get; private set; }

    // Represents the hologram that is currently being gazed at.
    public GameObject FocusedObject { get; private set; }

    GestureRecognizer recognizer;

    // Use this for initialization
    void Start()
    {
        Instance = this;

        // Set up a GestureRecognizer to detect Select gestures.
        recognizer = new GestureRecognizer();
        recognizer.Tapped += (args) =>
        {
            // Send an OnSelect message to the focused object and its ancestors.
            if (FocusedObject != null)
            {
                FocusedObject.SendMessageUpwards("OnSelect", SendMessageOptions.DontRequireReceiver);
            }
        };
        recognizer.StartCapturingGestures();
    }

    // Update is called once per frame
    void Update()
    {
        // Figure out which hologram is focused this frame.
        GameObject oldFocusObject = FocusedObject;

        // Do a raycast into the world based on the user's
        // head position and orientation.
        var headPosition = Camera.main.transform.position;
        var gazeDirection = Camera.main.transform.forward;

        RaycastHit hitInfo;
        if (Physics.Raycast(headPosition, gazeDirection, out hitInfo))
        {
            // If the raycast hit a hologram, use that as the focused object.
            FocusedObject = hitInfo.collider.gameObject;
        }
        else
        {
            // If the raycast did not hit a hologram, clear the focused object.
            FocusedObject = null;
        }

        // If the focused object changed this frame,
        // start detecting fresh gestures again.
        if (FocusedObject != oldFocusObject)
        {
            recognizer.CancelGestures();
            recognizer.StartCapturingGestures();
        }
    }
}
```

* Créez un autre script dans le dossier scripts, cette fois nommé **SphereCommands**.
* Développez l’objet **OrigamiCollection** dans l’affichage des hiérarchies.
* Faites glisser le script **SphereCommands** sur l’objet **Sphere1** dans le panneau hiérarchie.
* Faites glisser le script **SphereCommands** sur l’objet **Sphere2** dans le panneau hiérarchie.
* Ouvrez le script dans Visual Studio pour le modifier, puis remplacez le code par défaut par ce qui suit :

```cs
using UnityEngine;

public class SphereCommands : MonoBehaviour
{
    // Called by GazeGestureManager when the user performs a Select gesture
    void OnSelect()
    {
        // If the sphere has no Rigidbody component, add one to enable physics.
        if (!this.GetComponent<Rigidbody>())
        {
            var rigidbody = this.gameObject.AddComponent<Rigidbody>();
            rigidbody.collisionDetectionMode = CollisionDetectionMode.Continuous;
        }
    }
}
```

* Exportez, générez et déployez l’application sur l’émulateur HoloLens.
* Parcourez la scène et centrez-la sur l’un des sphères.
* Appuyez sur le bouton **A** du contrôleur Xbox ou appuyez sur la barre d’espace pour simuler le mouvement Select.

## <a name="chapter-4---voice"></a>Chapitre 4-voix

>[!VIDEO https://www.youtube.com/embed/LxbOhnd2_GM]

Dans ce chapitre, nous allons ajouter la prise en charge de deux [commandes vocales](voice-input.md): « réinitialiser le monde » pour revenir à leur emplacement d’origine, puis « déposer la sphère » pour faire tomber la sphère.

### <a name="objectives"></a>Objectifs

* Ajoutez des commandes vocales qui écoutent toujours en arrière-plan.
* Créez un hologramme qui réagit à une commande vocale.

### <a name="instructions"></a>Instructions

* Dans le dossier **scripts** , créez un script nommé **SpeechManager**.
* Faites glisser le script **SpeechManager** sur l’objet **OrigamiCollection** dans la hiérarchie.
* Ouvrez le script **SpeechManager** dans Visual Studio.
* Copiez et collez ce code dans **SpeechManager.cs** et **Enregistrez All**:

```cs
using System.Collections.Generic;
using System.Linq;
using UnityEngine;
using UnityEngine.Windows.Speech;

public class SpeechManager : MonoBehaviour
{
    KeywordRecognizer keywordRecognizer = null;
    Dictionary<string, System.Action> keywords = new Dictionary<string, System.Action>();

    // Use this for initialization
    void Start()
    {
        keywords.Add("Reset world", () =>
        {
            // Call the OnReset method on every descendant object.
            this.BroadcastMessage("OnReset");
        });

        keywords.Add("Drop Sphere", () =>
        {
            var focusObject = GazeGestureManager.Instance.FocusedObject;
            if (focusObject != null)
            {
                // Call the OnDrop method on just the focused object.
                focusObject.SendMessage("OnDrop", SendMessageOptions.DontRequireReceiver);
            }
        });

        // Tell the KeywordRecognizer about our keywords.
        keywordRecognizer = new KeywordRecognizer(keywords.Keys.ToArray());

        // Register a callback for the KeywordRecognizer and start recognizing!
        keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
        keywordRecognizer.Start();
    }

    private void KeywordRecognizer_OnPhraseRecognized(PhraseRecognizedEventArgs args)
    {
        System.Action keywordAction;
        if (keywords.TryGetValue(args.text, out keywordAction))
        {
            keywordAction.Invoke();
        }
    }
}
```

* Ouvrez le script **SphereCommands** dans Visual Studio.
* Mettez à jour le script pour le lire comme suit :

```cs
using UnityEngine;

public class SphereCommands : MonoBehaviour
{
    Vector3 originalPosition;

    // Use this for initialization
    void Start()
    {
        // Grab the original local position of the sphere when the app starts.
        originalPosition = this.transform.localPosition;
    }

    // Called by GazeGestureManager when the user performs a Select gesture
    void OnSelect()
    {
        // If the sphere has no Rigidbody component, add one to enable physics.
        if (!this.GetComponent<Rigidbody>())
        {
            var rigidbody = this.gameObject.AddComponent<Rigidbody>();
            rigidbody.collisionDetectionMode = CollisionDetectionMode.Continuous;
        }
    }

    // Called by SpeechManager when the user says the "Reset world" command
    void OnReset()
    {
        // If the sphere has a Rigidbody component, remove it to disable physics.
        var rigidbody = this.GetComponent<Rigidbody>();
        if (rigidbody != null)
        {
            rigidbody.isKinematic = true;
            Destroy(rigidbody);
        }

        // Put the sphere back into its original local position.
        this.transform.localPosition = originalPosition;
    }

    // Called by SpeechManager when the user says the "Drop sphere" command
    void OnDrop()
    {
        // Just do the same logic as a Select gesture.
        OnSelect();
    }
}
```

* Exportez, générez et déployez l’application sur l’émulateur HoloLens.
* L’émulateur prend en charge le microphone de votre PC et répond à votre voix : Ajustez l’affichage afin que le curseur se trouve sur l’un des deux, et dites « déposer la sphère ».
* Dites «**Réinitialiser le monde**» pour ramener les positions initiales.

## <a name="chapter-5---spatial-sound"></a>Chapitre 5-sons spatiaux

>[!VIDEO https://www.youtube.com/embed/Xc3C4VA10w4]

Dans ce chapitre, nous allons ajouter de la musique à l’application, puis déclencher des effets sonores sur certaines actions. Nous utiliserons le [son spatial](spatial-sound.md) pour fournir des sons à un emplacement spécifique dans l’espace 3D.

### <a name="objectives"></a>Objectifs

* Écoutez des hologrammes dans votre monde.

### <a name="instructions"></a>Instructions

* Dans Unity, sélectionnez dans le menu supérieur **modifier > paramètres du projet > audio**
* Recherchez le paramètre de **plug-in Spatializer** et sélectionnez **MS HRTF Spatializer**.
* À partir du dossier **hologrammes** , faites glisser l’objet **ambiance** sur l’objet **OrigamiCollection** dans le panneau hiérarchie.
* Sélectionnez **OrigamiCollection** et recherchez le composant **audio source** . Modifiez les propriétés suivantes :
  * Vérifiez la propriété **spatial** .
  * Vérifiez la **lecture sur éveillé**.
  * Remplacez **spatial Blend** par **3D** en faisant glisser le curseur vers la droite.
  * Vérifiez la propriété **Loop** .
  * Développez **paramètres audio 3D**, puis entrez **0,1** pour le **niveau Doppler**.
  * Définissez **volume Rolloff** sur **Rolloff logarithmique**.
  * Définissez **distance maximale** sur **20**.
* Dans le dossier **scripts** , créez un script nommé **SphereSounds**.
* Faites glisser **SphereSounds** vers les objets **Sphere1** et **Sphere2** dans la hiérarchie.
* Ouvrez **SphereSounds** dans Visual Studio, mettez à jour le code suivant et **Enregistrez All**.

```cs
using UnityEngine;

public class SphereSounds : MonoBehaviour
{
    AudioSource impactAudioSource = null;
    AudioSource rollingAudioSource = null;

    bool rolling = false;

    void Start()
    {
        // Add an AudioSource component and set up some defaults
        impactAudioSource = gameObject.AddComponent<AudioSource>();
        impactAudioSource.playOnAwake = false;
        impactAudioSource.spatialize = true;
        impactAudioSource.spatialBlend = 1.0f;
        impactAudioSource.dopplerLevel = 0.0f;
        impactAudioSource.rolloffMode = AudioRolloffMode.Logarithmic;
        impactAudioSource.maxDistance = 20f;

        rollingAudioSource = gameObject.AddComponent<AudioSource>();
        rollingAudioSource.playOnAwake = false;
        rollingAudioSource.spatialize = true;
        rollingAudioSource.spatialBlend = 1.0f;
        rollingAudioSource.dopplerLevel = 0.0f;
        rollingAudioSource.rolloffMode = AudioRolloffMode.Logarithmic;
        rollingAudioSource.maxDistance = 20f;
        rollingAudioSource.loop = true;

        // Load the Sphere sounds from the Resources folder
        impactAudioSource.clip = Resources.Load<AudioClip>("Impact");
        rollingAudioSource.clip = Resources.Load<AudioClip>("Rolling");
    }

    // Occurs when this object starts colliding with another object
    void OnCollisionEnter(Collision collision)
    {
        // Play an impact sound if the sphere impacts strongly enough.
        if (collision.relativeVelocity.magnitude >= 0.1f)
        {
            impactAudioSource.Play();
        }
    }

    // Occurs each frame that this object continues to collide with another object
    void OnCollisionStay(Collision collision)
    {
        Rigidbody rigid = gameObject.GetComponent<Rigidbody>();

        // Play a rolling sound if the sphere is rolling fast enough.
        if (!rolling && rigid.velocity.magnitude >= 0.01f)
        {
            rolling = true;
            rollingAudioSource.Play();
        }
        // Stop the rolling sound if rolling slows down.
        else if (rolling && rigid.velocity.magnitude < 0.01f)
        {
            rolling = false;
            rollingAudioSource.Stop();
        }
    }

    // Occurs when this object stops colliding with another object
    void OnCollisionExit(Collision collision)
    {
        // Stop the rolling sound if the object falls off and stops colliding.
        if (rolling)
        {
            rolling = false;
            impactAudioSource.Stop();
            rollingAudioSource.Stop();
        }
    }
}
```

* Enregistrez le script et revenez à Unity.
* Exportez, générez et déployez l’application sur l’émulateur HoloLens.
* Portez du casque pour obtenir un effet complet, et rapprochez-vous de la phase pour écouter les sons.

## <a name="chapter-6---spatial-mapping"></a>Chapitre 6-mappage spatial

>[!VIDEO https://www.youtube.com/embed/S-517Y63Cnk]

Nous allons maintenant utiliser le [mappage spatial](spatial-mapping.md) pour placer la grille de jeux sur un objet réel dans le monde réel.

### <a name="objectives"></a>Objectifs

* Intégrez votre monde réel dans le monde virtuel.
* Placez vos hologrammes là où ils vous intéressent le plus.

### <a name="instructions"></a>Instructions

* Cliquez sur le dossier **hologrammes** dans le panneau projet.
* Faites glisser la ressource de **mappage spatial** à la racine de la **hiérarchie**.
* Cliquez sur l’objet **mappage spatial** dans la hiérarchie.
* Dans le **panneau Inspecteur**, modifiez les propriétés suivantes :
  * Cochez la case **dessiner des panneaux visuels** .
  * Recherchez **matériel de dessin** , puis cliquez sur le cercle à droite. Tapez «**Wireframe**» dans le champ de recherche en haut. Cliquez sur le résultat, puis fermez la fenêtre.
* Exportez, générez et déployez l’application sur l’émulateur HoloLens.
* Lorsque l’application s’exécute, une maille d’une salle de vie réelle scannée précédemment est rendue en filaire.
* Regardez comment une sphère enchaînée va tomber à l’étage, et à l’étage !

Nous allons maintenant vous montrer comment déplacer le OrigamiCollection vers un nouvel emplacement :

* Dans le dossier **scripts** , créez un script nommé **TapToPlaceParent**.
* Dans la **hiérarchie**, développez le **OrigamiCollection** et sélectionnez l’objet **stage** .
* Faites glisser le script **TapToPlaceParent** sur l’objet stage.
* Ouvrez le script **TapToPlaceParent** dans Visual Studio et mettez-le à jour comme suit :

```cs
using UnityEngine;

public class TapToPlaceParent : MonoBehaviour
{
    bool placing = false;

    // Called by GazeGestureManager when the user performs a Select gesture
    void OnSelect()
    {
        // On each Select gesture, toggle whether the user is in placing mode.
        placing = !placing;

        // If the user is in placing mode, display the spatial mapping mesh.
        if (placing)
        {
            SpatialMapping.Instance.DrawVisualMeshes = true;
        }
        // If the user is not in placing mode, hide the spatial mapping mesh.
        else
        {
            SpatialMapping.Instance.DrawVisualMeshes = false;
        }
    }

    // Update is called once per frame
    void Update()
    {
        // If the user is in placing mode,
        // update the placement to match the user's gaze.

        if (placing)
        {
            // Do a raycast into the world that will only hit the Spatial Mapping mesh.
            var headPosition = Camera.main.transform.position;
            var gazeDirection = Camera.main.transform.forward;

            RaycastHit hitInfo;
            if (Physics.Raycast(headPosition, gazeDirection, out hitInfo,
                30.0f, SpatialMapping.PhysicsRaycastMask))
            {
                // Move this object's parent object to
                // where the raycast hit the Spatial Mapping mesh.
                this.transform.parent.position = hitInfo.point;

                // Rotate this object's parent object to face the user.
                Quaternion toQuat = Camera.main.transform.localRotation;
                toQuat.x = 0;
                toQuat.z = 0;
                this.transform.parent.rotation = toQuat;
            }
        }
    }
}
```

* Exporter, générer et déployer l’application.
* Vous devez maintenant être en mesure de placer le jeu à un emplacement spécifique par gazing, à l’aide du geste Select (**a ou de** l’espace), puis en le déplaçant vers un nouvel emplacement et en réutilisant le geste Select.

## <a name="the-end"></a>La fin

Et c’est la fin de ce didacticiel.

Vous avez appris à :

* Comment créer une application holographique dans Unity.
* Comment utiliser le point de vue du regard, du mouvement, de la voix, des sons et du mappage spatial.
* Comment générer et déployer une application à l’aide de Visual Studio.

Vous êtes maintenant prêt à commencer à créer vos propres applications holographiques !

## <a name="see-also"></a>Articles associés

* [MR Basics 101 : finaliser le projet avec l’appareil](holograms-101.md)
* [Pointage du regard](gaze-and-commit.md)
* [Pointer du regard vers l’avant et valider](gaze-and-commit.md)
* [Entrée vocale](voice-input.md)
* [Son spatial](spatial-sound.md)
* [Mappage spatial](spatial-mapping.md)
