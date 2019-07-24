---
title: Notions de base de m. 101-finaliser le projet avec l’appareil
description: Suivez cette procédure pas à pas de codage à l’aide d’Unity, Visual Studio et HoloLens pour apprendre les principes fondamentaux de Windows Mixed Reality.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: réalité mixte, Windows Mixed Reality, HoloLens, hologramme, Academy, didacticiel
ms.openlocfilehash: 043ffac8f30a4e29586478b5dca6ecccc2b5afd3
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524030"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br>

# <a name="mr-basics-101-complete-project-with-device"></a>Notions de base de m. 101: Terminer le projet avec l’appareil

<br>

>[!VIDEO https://www.youtube.com/embed/XKIIEC5BMWg]

Ce didacticiel vous guide tout au long d’un projet complet, Unity, qui illustre les fonctionnalités de base de la réalité mixte Windows sur HoloLens [, y compris](gaze.md)le point de présence, les [gestes](gestures.md), l' [entrée vocale](voice-input.md), le [son spatial](spatial-sound.md) et le [mappage spatial](spatial-mapping.md) .

Le didacticiel prendra environ 1 heure.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>Notions de base de m. 101: Terminer le projet avec l’appareil</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-101.zip) requis par le projet. Requiert Unity 2017,2 ou une version ultérieure.
  * Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-101.zip).
  * Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-101.zip).
  * Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-101.zip).
* Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre. Conservez le nom du dossier **origami**.

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-101).

## <a name="chapter-1---holo-world"></a>Chapitre 1-monde «Holo»

>[!VIDEO https://www.youtube.com/embed/PmtZGjYFroY]

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
* Étant donné que le projet **origami** ne contient pas de scène, enregistrez la scène vide par défaut dans un nouveau fichier à l’aide de: Fichier / **enregistrer la scène sous**.
* Nommez le nouvel **origami** de scène et appuyez sur le bouton **Enregistrer** .

#### <a name="setup-the-main-virtual-camera"></a>Configurer la caméra virtuelle principale

* Dans le **panneau hiérarchie**, sélectionnez **caméra principale**.
* Dans l' **inspecteur** , définissez sa position de transformation sur **0, 0,** 0.
* Recherchez la propriété **effacer les indicateurs** et remplacez la liste déroulante **skybox** par **couleur unie**.
* Cliquez sur le champ **arrière-plan** pour ouvrir un sélecteur de couleurs.
* Affectez **R, G, B et A** à **0**.

#### <a name="setup-the-scene"></a>Configurer la scène

* Dans le **volet hiérarchie**, cliquez sur **créer** et **créez un vide**.
* Cliquez avec le bouton droit sur le nouveau **gameobject** , puis sélectionnez Renommer. Renommez GameObject en **OrigamiCollection**.
* Dans le  dossier hologrammes du panneau projet (développez actifs et sélectionnez hologrammes ou double-cliquez sur le dossier hologrammes dans le panneau projet):
  * Faites glisser **étape** dans la hiérarchie pour être un enfant de **OrigamiCollection**.
  * Faites glisser **Sphere1** dans la hiérarchie pour être un enfant de **OrigamiCollection**.
  * Faites glisser **Sphere2** dans la hiérarchie pour être un enfant de **OrigamiCollection**.
* Cliquez avec le bouton droit sur l’objet **Light directionnel** dans le **panneau hiérarchie** , puis sélectionnez **supprimer**.
* À partir  du dossier hologrammes, faites glisser Lights à la racine du **panneau de hiérarchie**.
* Dans la **hiérarchie**, sélectionnez **OrigamiCollection**.
* Dans l' **inspecteur**, définissez la position de la transformation sur **0,-0,5, 2,0**.
* Appuyez sur le bouton de **lecture** dans Unity pour afficher un aperçu de vos hologrammes.
* Les objets origami doivent apparaître dans la fenêtre d’aperçu.
* Appuyez sur **lecture** une deuxième fois pour arrêter le mode aperçu.

#### <a name="export-the-project-from-unity-to-visual-studio"></a>Exporter le projet d’Unity vers Visual Studio

* Dans Unity, sélectionnez **fichier > paramètres de build**.
* Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur basculer la **plateforme**.
* Affectez à **SDK** la valeur **Universal 10** et **type de build** la valeur **D3D**.
* Vérifiez **les C# projets Unity**.
* Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.
* Cliquez sur **Build**.
* Dans la fenêtre de l’Explorateur de fichiers qui s’affiche, créez un **nouveau dossier** nommé «App».
* Cliquez sur le **dossier**de l’application.
* Appuyez sur **Sélectionner un dossier**.
* Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.
* Ouvrez le dossier de l' **application** .
* Ouvrez (double-clic) **origami. sln**.
* À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.
* Cliquez sur la flèche en regard du bouton périphérique, puis sélectionnez **machine** distante à déployer sur Wi-Fi.
  * Définissez l' **adresse** sur le nom ou l’adresse IP de votre HoloLens. Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées** ou demandez à Cortana **«Hey Cortana, qu’est-ce que mon adresse IP?»**
  * Si HoloLens est attaché sur USB, vous pouvez sélectionner l' **appareil** à déployer sur USB.
  * Laissez le **mode d’authentification** défini sur **universel**.
  * Cliquez sur **Sélectionner**

* Cliquez sur déboguer **> exécuter sans débogage** ou appuyez sur **CTRL + F5**. S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le coupler à [Visual Studio](using-visual-studio.md#pairing-your-device-hololens-(1st-gen)).

* Le projet Origami va maintenant générer, déployer sur votre HoloLens, puis exécuter.
* Placez-vous sur HoloLens et recherchez vos nouveaux hologrammes.

## <a name="chapter-2---gaze"></a>Chapitre 2-point de regard

>[!VIDEO https://www.youtube.com/embed/MSO2BoFSQbM]

Dans ce chapitre, nous allons présenter la première des trois façons d’interagir avec vos hologrammes, en pointant le [regard](gaze.md).

### <a name="objectives"></a>Objectifs

* Visualisez votre point de regard à l’aide d’un curseur verrouillé.

### <a name="instructions"></a>Instructions

* Revenez à votre projet Unity et fermez la fenêtre Paramètres de build si elle est toujours ouverte.
* Sélectionnez le  dossier hologrammes dans le **panneau Projet**.
* Faites glisser l’objet **curseur** dans le volet de la **hiérarchie** au niveau de la racine.
* Double-cliquez sur l’objet **curseur** pour l’examiner en détail.
* Cliquez avec le bouton droit sur le dossier **scripts** dans le panneau projet.
* Cliquez sur le sous-menu **créer** .
* Sélectionnez  **C# script**.
* Nommez le script **WorldCursor**. Remarque : Le nom est sensible à la casse. Vous n’avez pas besoin d’ajouter l’extension. cs.
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

            // Move the cursor to the point where the raycast hit.
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
* Revenez à la solution Visual Studio utilisée précédemment pour le déploiement dans votre HoloLens.
* Lorsque vous y êtes invité, sélectionnez «recharger tout».
* Cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
* Examinez maintenant la scène et observez comment le curseur interagit avec la forme d’objets.

## <a name="chapter-3---gestures"></a>Chapitre 3-mouvements

>[!VIDEO https://www.youtube.com/embed/kW3ThJ2MbvQ]

Dans ce chapitre, nous allons ajouter la prise en charge des [gestes](gestures.md). Lorsque l’utilisateur sélectionne une sphère papier, nous allons faire tomber la sphère en activant la gravité en utilisant le moteur physique Unity.

### <a name="objectives"></a>Objectifs

* Contrôlez vos hologrammes avec le geste Select.

### <a name="instructions"></a>Instructions

Nous allons commencer par créer un script, puis détecter le mouvement Select.

* Dans le dossier **scripts** , créez un script nommé **GazeGestureManager**.
* Faites glisser le script **GazeGestureManager** sur l’objet **OrigamiCollection** dans la hiérarchie.
* Ouvrez le script **GazeGestureManager** dans Visual Studio et ajoutez le code suivant:

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
    void Awake()
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
* Ouvrez le script dans Visual Studio pour le modifier, puis remplacez le code par défaut par ce qui suit:

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

* Exportez, générez et déployez l’application dans votre HoloLens.
* Examinez l’une des sphères.
* Effectuez le mouvement SELECT et regardez la sphère de la sphère sur l’aire ci-dessous.

## <a name="chapter-4---voice"></a>Chapitre 4-voix

>[!VIDEO https://www.youtube.com/embed/1-Aq0VVtHM8]

Dans ce chapitre, nous allons ajouter la prise en charge de deux [commandes vocales](voice-input.md): «Réinitialiser le monde» pour ramener les sphères déplacées à leur emplacement d’origine et «déposer la sphère» pour faire tomber la sphère.

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
* Mettez à jour le script pour le lire comme suit:

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

* Exportez, générez et déployez l’application dans votre HoloLens.
* Examinez l’une des sphères et dites «**Drop Sphere**».
* Dites «**Réinitialiser le monde**» pour ramener les positions initiales.

## <a name="chapter-5---spatial-sound"></a>Chapitre 5-sons spatiaux

>[!VIDEO https://www.youtube.com/embed/Aj4de5Ncbfo]

Dans ce chapitre, nous allons ajouter de la musique à l’application, puis déclencher des effets sonores sur certaines actions. Nous utiliserons le [son spatial](spatial-sound.md) pour fournir des sons à un emplacement spécifique dans l’espace 3D.

### <a name="objectives"></a>Objectifs

* Écoutez des hologrammes dans votre monde.

### <a name="instructions"></a>Instructions

* Dans Unity, sélectionnez dans le menu supérieur **modifier > paramètres du projet > audio**
* Dans le volet de l’inspecteur situé sur le côté droit, recherchez le paramètre de **plug-in Spatializer** , puis sélectionnez **MS HRTF Spatializer**.
* À partir  du dossier hologrammes du panneau projet, faites glisser l’objet **ambiance** sur l’objet **OrigamiCollection** dans le panneau hiérarchie.
* Sélectionnez **OrigamiCollection** et recherchez le composant **audio source** dans le panneau Inspecteur. Modifiez les propriétés suivantes:
  * Vérifiez la propriété **spatial** .
  * Vérifiez la **lecture sur éveillé**.
  * Remplacez **spatial Blend** par **3D** en faisant glisser le curseur vers la droite. La valeur doit passer de 0 à 1 lorsque vous déplacez le curseur.
  * Vérifiez la propriété **Loop** .
  * Développez **paramètres audio 3D**, puis entrez **0,1** pour le **niveau Doppler**.
  * Définissez **volume Rolloff** sur **Rolloff logarithmique**.
  * Définissez **distance maximale** sur **20**.
* Dans le dossier **scripts** , créez un script nommé **SphereSounds**.
* Glissez-déplacez **SphereSounds** vers les objets **Sphere1** et **Sphere2** dans la hiérarchie.
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
* Exportez, générez et déployez l’application dans votre HoloLens.
* Rapprochez-vous de l’étape et transformez-la en côte à côte pour entendre la modification des sons.

## <a name="chapter-6---spatial-mapping"></a>Chapitre 6-mappage spatial

>[!VIDEO https://www.youtube.com/embed/Pkt1_wNLLXY]

Nous allons maintenant utiliser le [mappage spatial](spatial-mapping.md) pour placer la grille de jeux sur un objet réel dans le monde réel.

### <a name="objectives"></a>Objectifs

* Intégrez votre monde réel dans le monde virtuel.
* Placez vos hologrammes là où ils vous intéressent le plus.

### <a name="instructions"></a>Instructions

* Dans Unity, cliquez sur  le dossier hologrammes dans le panneau projet.
* Faites glisser la ressource de **mappage spatial** à la racine de la **hiérarchie**.
* Cliquez sur l’objet **mappage spatial** dans la hiérarchie.
* Dans le **panneau Inspecteur**, modifiez les propriétés suivantes:
  * Cochez la case **dessiner des panneaux visuels** .
  * Recherchez **matériel de dessin** , puis cliquez sur le cercle à droite. Tapez «**Wireframe**» dans le champ de recherche en haut. Cliquez sur le résultat, puis fermez la fenêtre. Lorsque vous effectuez cette opération, la valeur de Draw Material doit être définie sur Wireframe.
* Exportez, générez et déployez l’application dans votre HoloLens.
* Lorsque l’application s’exécute, un maillage filaire se superpose à votre monde réel.
* Regardez comment une sphère enchaînée va tomber à l’étage, et à l’étage!

Nous allons maintenant vous montrer comment déplacer le OrigamiCollection vers un nouvel emplacement:

* Dans le dossier **scripts** , créez un script nommé **TapToPlaceParent**.
* Dans la **hiérarchie**, développez le **OrigamiCollection** et sélectionnez l’objet **stage** .
* Faites glisser le script **TapToPlaceParent** sur l’objet stage.
* Ouvrez le script **TapToPlaceParent** dans Visual Studio et mettez-le à jour comme suit:

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
* Vous devez maintenant être en mesure de placer le jeu à un emplacement spécifique par gazing, à l’aide du geste Select, puis en le déplaçant vers un nouvel emplacement et en réutilisant le geste Select.

## <a name="chapter-7---holographic-fun"></a>Chapitre 7-divertissement holographique

### <a name="objectives"></a>Objectifs

* Révélez l’entrée à un sous-monde holographique.

### <a name="instructions"></a>Instructions

Nous allons maintenant vous montrer comment dévoiler le sous-monde holographique:

* Dans le  dossier hologrammes du panneau projet:
  * Faites glisser le sous- **monde** dans la hiérarchie pour être un enfant de **OrigamiCollection**.
* Dans le dossier **scripts** , créez un script nommé **HitTarget**.
* Dans la **hiérarchie**, développez **OrigamiCollection**.
* Développez l’objet **stage** et sélectionnez l’objet **cible** (ventilateur bleu).
* Faites glisser le script **HitTarget** sur l’objet **cible** .
* Ouvrez le script **HitTarget** dans Visual Studio et mettez-le à jour comme suit:

```cs
using UnityEngine;

public class HitTarget : MonoBehaviour
{
    // These public fields become settable properties in the Unity editor.
    public GameObject underworld;
    public GameObject objectToHide;

    // Occurs when this object starts colliding with another object
    void OnCollisionEnter(Collision collision)
    {
        // Hide the stage and show the underworld.
        objectToHide.SetActive(false);
        underworld.SetActive(true);

        // Disable Spatial Mapping to let the spheres enter the underworld.
        SpatialMapping.Instance.MappingEnabled = false;
    }
}
```

* Dans Unity, sélectionnez l’objet **cible** .
* Deux propriétés publiques sont désormais visibles sur le composant **cible d’accès** et doivent référencer des objets dans notre scène:
  * Faites glisser le sous- **monde** du volet de la **hiérarchie** vers **la propriété sous** le composant cible d' **accès** .
  * Faites glisser **étape** du volet **hiérarchie** vers l' **objet pour masquer** la propriété sur le composant cible d' **accès** .
* Exporter, générer et déployer l’application.
* Placez la collection d’origamis à l’étage, puis utilisez le mouvement SELECT pour faire glisser une sphère.
* Lorsque la sphère atteint la cible (ventilateur bleu), une explosion se produit. Le regroupement sera masqué et un trou au sous-monde s’affichera.

## <a name="the-end"></a>La fin

Et c’est la fin de ce didacticiel.

Vous avez appris à:

* Comment créer une application holographique dans Unity.
* Comment utiliser le point de vue du regard, du geste, de la voix, du son et du mappage spatial.
* Comment générer et déployer une application à l’aide de Visual Studio.

Vous êtes maintenant prêt à commencer à créer votre propre expérience holographique!

## <a name="see-also"></a>Voir aussi

* [Réalité mixte - Principes fondamentaux - Cours 101E : Projet complet avec émulateur](holograms-101e.md)
* [Pointage du regard](gaze.md)
* [Mouvements](gestures.md)
* [Entrée vocale](voice-input.md)
* [Son spatial](spatial-sound.md)
* [Mappage spatial](spatial-mapping.md)
