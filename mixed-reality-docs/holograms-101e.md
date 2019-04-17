---
title: Principes fondamentaux de M. 101E - projet complet avec l’émulateur
description: Suivez cette procédure pas à pas à l’aide de Unity, Visual Studio et HoloLens émulateur pour apprendre les notions d’une application holographique de codage.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: réalité mixte, réalité mixte Windows, HoloLens, HOLOGRAMME, émulateur didacticiel academy,
ms.openlocfilehash: 77f7d497396937bf471a69fa514cef84ab0b699d
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593987"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-basics-101e-complete-project-with-emulator"></a>Principes de base MR 101E : Projet complet avec l’émulateur

 >[!VIDEO https://www.youtube.com/embed/Xzm8_s05mm8]

Ce didacticiel vous guidera dans un projet complet, créé dans Unity, qui illustre les fonctionnalités de Windows Mixed Reality core, notamment HoloLens [les regards](gaze.md), [mouvements](gestures.md), [entréevoix](voice-input.md), [son spatial](spatial-sound.md) et [mappage spatial](spatial-mapping.md). Le didacticiel vous prendra environ une heure.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>Principes de base MR 101E : Projet complet avec l’émulateur</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).

### <a name="project-files"></a>Fichiers projet

* Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) requise par le projet. Nécessite Unity 2017.2 ou version ultérieure.
  * Si vous avez besoin de prise en charge de Unity 5.6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).
  * Si vous avez besoin de prise en charge de Unity 5.5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).
  * Si vous avez besoin de prise en charge de Unity 5.4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).
* Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement. Conservez le nom de dossier en tant que **Origami**.

>[!NOTE]
>Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).

## <a name="chapter-1---holo-world"></a>Chapitre 1 - « Holo » world

>[!VIDEO https://www.youtube.com/embed/qotpUpIQxVU]

Dans ce chapitre, nous le programme d’installation de notre premier projet Unity et les étapes à la build et processus de déploiement.

### <a name="objectives"></a>Objectifs

* Configurer Unity pour le développement HOLOGRAPHIQUE.
* Rendre un hologramme.
* Consultez un hologramme que vous avez apportées.

### <a name="instructions"></a>Instructions

* Démarrez Unity.
* Sélectionnez **Open**.
* Entrez l’emplacement que le **Origami** dossier vous précédemment non archivés.
* Sélectionnez **Origami** et cliquez sur **sélectionner le dossier**.
* Enregistrer la nouvelle scène : **Fichier** / **enregistrer la scène sous**.
* Nommez la scène **Origami** et appuyez sur la **enregistrer** bouton.

#### <a name="setup-the-main-camera"></a>Le programme d’installation de la caméra principale

* Dans le **hiérarchie panneau**, sélectionnez **Main Camera**.
* Dans le **inspecteur** positionnez sa transformation **0,0,0**.
* Rechercher la **effacer les indicateurs** propriété et modifier la liste déroulante à partir de **Skybox** à **couleur unie**.
* Cliquez sur le **arrière-plan** champ pour ouvrir un sélecteur de couleurs.
* Définissez **R, G, B et A** à **0**.

#### <a name="setup-the-scene"></a>Le programme d’installation de la scène

* Dans le **hiérarchie panneau**, cliquez sur **créer** et **créer vide**.
* Cliquez sur le nouveau **GameObject** et sélectionnez Renommer. Renommer le GameObject à **OrigamiCollection**.
* À partir de la **Vntana** dossier dans le **panneau projet**:
  * Faites glisser **étape** dans la hiérarchie soit un enfant de **OrigamiCollection**.
  * Faites glisser **Sphere1** dans la hiérarchie soit un enfant de **OrigamiCollection**.
  * Faites glisser **Sphere2** dans la hiérarchie soit un enfant de **OrigamiCollection**.
* Avec le bouton droit le **lumière directionnelle** de l’objet dans le **hiérarchie panneau** et sélectionnez **supprimer**.
* À partir de la **hologrammes** dossier, faites glisser **lumières** à la racine de la **hiérarchie panneau**.
* Dans le **hiérarchie**, sélectionnez le **OrigamiCollection**.
* Dans le **inspecteur**, positionnez la transformation **0, -0,5, 2.0**.
* Appuyez sur la **lire** bouton dans Unity pour afficher un aperçu votre hologrammes.
* Vous devez voir les objets Origami dans la fenêtre d’aperçu.
* Appuyez sur **lire** une deuxième fois pour arrêter le mode d’aperçu.

#### <a name="export-the-project-from-unity-to-visual-studio"></a>Exportez le projet à partir d’Unity pour Visual Studio

* Dans, sélectionnez Unity **fichier > Paramètres de Build**.
* Sélectionnez **Windows Store** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.
* Définissez **SDK** à **universelle 10** et **Type de Build** à **D3D**.
* Vérifiez **Unity C# projets**.
* Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.
* Cliquez sur **paramètres du lecteur...** .
* Dans l’instruction select panneau Inspecteur le **logo du Windows Store**. Puis sélectionnez **paramètres de publication**.
* Dans le **fonctionnalités** section, sélectionnez le **Microphone** et **SpatialPerception** fonctionnalités.
* Dans la fenêtre Paramètres de Build, cliquez sur **Build**.
* Créer un **nouveau dossier** nommé « Application ».
* Clic le **dossier application**.
* Appuyez sur **sélectionnez dossier**.
* Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.
* Ouvrez le **application** dossier.
* Ouvrez le **Origami Visual Studio Solution**.
* À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **X86**.
  * Cliquez sur la flèche en regard du bouton de l’appareil, puis sélectionnez **HoloLens émulateur**.
  * Cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.
  * Après un certain temps, l’émulateur démarre avec le projet Origami. Lors du lancement d’abord le [émulateur](using-the-hololens-emulator.md), il peut prendre jusqu'à 15 minutes pour l’émulateur démarre. Une fois qu’il démarre, ne la fermez pas.

## <a name="chapter-2---gaze"></a>Chapitre 2 - regards

>[!VIDEO https://www.youtube.com/embed/BPWTbAC210k]

Dans ce chapitre, nous allons introduire le premier des trois façons d’interagir avec votre hologrammes-- [les regards](gaze.md).

### <a name="objectives"></a>Objectifs

* Visualiser votre regard à l’aide d’un curseur verrouillé de monde.

### <a name="instructions"></a>Instructions

* Revenez à votre projet Unity et fermer la fenêtre Paramètres de Build si elle est toujours ouverte.
* Sélectionnez le **Vntana** dossier dans le **panneau projet**.
* Faites glisser le **curseur** de l’objet dans le **Panneau de la hiérarchie** au niveau racine.
* Double-cliquez sur le **curseur** objet effectue une examiner plus en détail.
* Avec le bouton droit sur le **Scripts** dossier dans le panneau de configuration de projet.
* Cliquez sur le **créer** sous-menu.
* Sélectionnez  **C# Script**.
* Nommez le script **WorldCursor**. Remarque: Le nom est sensible à la casse. Vous n’avez pas besoin ajouter l’extension .cs.
* Sélectionnez le **curseur** de l’objet dans le **Panneau de la hiérarchie**.
* Faites glisser et déposez le **WorldCursor** écrite dans le **panneau Inspecteur**.
* Double-cliquez sur le **WorldCursor** script pour l’ouvrir dans Visual Studio.
* Copiez et collez ce code dans **WorldCursor.cs** et **Enregistrer tout**.

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

* Régénérer l’application à partir de **fichier > Paramètres de Build**.
* Revenez à la solution Visual Studio utilisée précédemment pour déployer sur l’émulateur.
* Sélectionnez « Recharger All » lorsque vous y êtes invité.
* Cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.
* Utilisez la manette Xbox pour rechercher la scène. Notez la façon dont le curseur interagit avec la forme d’objets.

## <a name="chapter-3---gestures"></a>Chapitre 3 - mouvements

>[!VIDEO https://www.youtube.com/embed/6d-0RHeKHq4]

Dans ce chapitre, nous allons ajouter la prise en charge de [mouvements](gestures.md). Lorsque l’utilisateur sélectionne une sphère de papier, nous allons rendre la sphère se répartissent en activant la gravité, à l’aide du moteur de physique d’Unity.

### <a name="objectives"></a>Objectifs

* Contrôler votre hologrammes avec le mouvement de sélection.

### <a name="instructions"></a>Instructions

Nous allons commencer en créant un script que peut détecter le mouvement de sélection.

* Dans le **Scripts** dossier, créez un script nommé **GazeGestureManager**.
* Faites glisser le **GazeGestureManager** de script sur le **OrigamiCollection** objet dans la hiérarchie.
* Ouvrez le **GazeGestureManager** de script dans Visual Studio et ajoutez le code suivant :

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

* Créer un autre script dans le dossier Scripts, cette fois nommée **SphereCommands**.
* Développez le **OrigamiCollection** objet dans la vue de la hiérarchie.
* Faites glisser le **SphereCommands** de script sur le **Sphere1** objet dans le volet de la hiérarchie.
* Faites glisser le **SphereCommands** de script sur le **Sphere2** objet dans le volet de la hiérarchie.
* Ouvrez le script dans Visual Studio pour la modification et remplacez le code par défaut avec ce :

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

* Exporter, générer et déployer l’application sur l’émulateur de HoloLens.
* Regardez autour de la scène et centrer sur l’un de la couleur des sphères.
* Appuyez sur la **A** bouton sur le contrôleur Xbox ou appuyez sur la barre d’espace pour simuler le mouvement de sélection.

## <a name="chapter-4---voice"></a>Chapitre 4 - Voice

>[!VIDEO https://www.youtube.com/embed/LxbOhnd2_GM]

Dans ce chapitre, nous allons ajouter la prise en charge pour deux [commandes vocales](voice-input.md): « Réinitialisation world » pour retourne les sphères supprimés à leur emplacement d’origine et la « Sphère de dépôt » pour rendre la sphère appartiennent.

### <a name="objectives"></a>Objectifs

* Ajouter des commandes vocales qui écoutent toujours en arrière-plan.
* Créer un hologramme qui réagit à une commande vocale.

### <a name="instructions"></a>Instructions

* Dans le **Scripts** dossier, créez un script nommé **SpeechManager**.
* Faites glisser le **SpeechManager** de script sur le **OrigamiCollection** objet dans la hiérarchie
* Ouvrez le **SpeechManager** script dans Visual Studio.
* Copiez et collez ce code dans **SpeechManager.cs** et **Enregistrer tout**:

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

* Ouvrez le **SphereCommands** script dans Visual Studio.
* Mettre à jour le script comme suit :

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

* Exporter, générer et déployer l’application sur l’émulateur de HoloLens.
* L’émulateur prendra en charge microphone de votre PC et répondre à votre voix : ajuster la vue de sorte que le curseur se trouve sur l’un de la couleur des sphères et dire « Drop sphère ».
* Par exemple «**World réinitialiser**» pour les ramener dans leur position initiale.

## <a name="chapter-5---spatial-sound"></a>Chapitre 5 - son Spatial

>[!VIDEO https://www.youtube.com/embed/Xc3C4VA10w4]

Dans ce chapitre, nous allons ajouter de la musique à l’application et ensuite déclencher effets sonores sur certaines actions. Nous allons utiliser [son spatial](spatial-sound.md) afin de donner des sons à un emplacement spécifique dans l’espace 3D.

### <a name="objectives"></a>Objectifs

* Écoutez hologrammes dans votre monde.

### <a name="instructions"></a>Instructions

* Dans l’instruction select dans le menu supérieur Unity **Modifier > Paramètres du projet > Audio**
* Rechercher la **plug-in spatial** paramètre et sélectionnez **MS HRTF Spatializer**.
* À partir de la **hologrammes** dossier, faites glisser le **ambiance** de l’objet sur le **OrigamiCollection** objet dans le volet de la hiérarchie.
* Sélectionnez **OrigamiCollection** et recherchez le **Audio Source** composant. Modifier ces propriétés :
  * Vérifier le **Spatialize** propriété.
  * Vérifier le **jouer sur éveillés**.
  * Modification **Blend Spatial** à **3D** en faisant glisser le curseur complètement à droite.
  * Vérifier le **boucle** propriété.
  * Développez **les paramètres audio 3D**, puis entrez **0.1** pour **niveau Doppler**.
  * Définissez **Volume écrêtage** à **écrêtage logarithmique**.
  * Définissez **Max Distance** à **20**.
* Dans le **Scripts** dossier, créez un script nommé **SphereSounds**.
* Faites glisser **SphereSounds** à la **Sphere1** et **Sphere2** objets dans la hiérarchie.
* Ouvrez **SphereSounds** dans Visual Studio, mettre à jour le code suivant et **Enregistrer tout**.

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

* Enregistrer le script et revenir à Unity.
* Exporter, générer et déployer l’application sur l’émulateur de HoloLens.
* Porter un casque pour obtenir l’effet et déplacer le plus proche et plus éloigné de la phase d’entendre les sons à modifier.

## <a name="chapter-6---spatial-mapping"></a>Mappage du chapitre 6 – Spatial

>[!VIDEO https://www.youtube.com/embed/S-517Y63Cnk]

Maintenant nous allons utiliser [mappage spatial](spatial-mapping.md) pour placer le plateau de jeu sur un objet réel dans le monde réel.

### <a name="objectives"></a>Objectifs

* Placez votre monde réel dans le monde virtuel.
* Placez votre hologrammes où ils vous intéressent.

### <a name="instructions"></a>Instructions

* Cliquez sur le **hologrammes** dossier dans le panneau de configuration de projet.
* Faites glisser le **mappage Spatial** actif à la racine de la **hiérarchie**.
* Cliquez sur le **mappage Spatial** objet dans la hiérarchie.
* Dans le **panneau Inspecteur**, modifiez les propriétés suivantes :
  * Vérifier le **dessiner les maillages Visual** boîte.
  * Recherchez **dessiner un matériau** et cliquez sur le cercle sur la droite. Type «**filaire**» dans le champ de recherche en haut. Cliquez sur le résultat, puis fermez la fenêtre.
* Exporter, générer et déployer l’application sur l’émulateur de HoloLens.
* Lorsque l’application s’exécute, une maille d’un salon réalistes précédemment analysé s’affichera en filaire.
* Regardez comment une sphère propagée tombera hors de la scène et sur le sol !

Maintenant nous allons vous montrer comment déplacer la OrigamiCollection vers un nouvel emplacement :

* Dans le **Scripts** dossier, créez un script nommé **TapToPlaceParent**.
* Dans le **hiérarchie**, développez le **OrigamiCollection** et sélectionnez le **étape** objet.
* Faites glisser le **TapToPlaceParent** script sur l’objet de la scène.
* Ouvrez le **TapToPlaceParent** de script dans Visual Studio et mettre à jour pour être ce qui suit :

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

* Exporter, créer et déployer l’application.
* Vous devez désormais maintenant être en mesure de placer le jeu dans un emplacement spécifique par gazing à elle, à l’aide du mouvement sélectionnez (**A** ou espace) et déplacer vers un nouvel emplacement, puis à l’aide du mouvement sélectionnez à nouveau.

## <a name="the-end"></a>La fin

Et c’est la fin de ce didacticiel !

Vous avez appris :

* Comment créer une application HOLOGRAPHIQUE dans Unity.
* Comment rendre l’utilisation des regards, mouvement, voix, sons et mappage spatial.
* Comment créer et déployer une application à l’aide de Visual Studio.

Vous êtes maintenant prêt à commencer à créer vos propres applications HOLOGRAPHIQUE !

## <a name="see-also"></a>Voir aussi

* [Principes de base MR 101 : Projet complet avec l’appareil](holograms-101.md)
* [Gaze](gaze.md)
* [Mouvements](gestures.md)
* [Entrée vocale](voice-input.md)
* [Son spatial](spatial-sound.md)
* [Mappage spatial](spatial-mapping.md)
