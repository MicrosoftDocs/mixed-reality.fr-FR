---
title: RM partageant 240-plusieurs appareils HoloLens
description: Suivez cette procédure pas à pas de codage avec Unity, Visual Studio et HoloLens pour apprendre les détails du partage d’hologrammes.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, partage, mise en réseau, Academy, didacticiel
ms.openlocfilehash: 70a39a739d360a5032bc8df76b6f0bd57521d9ec
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522330"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br>

# <a name="mr-sharing-240-multiple-hololens-devices"></a>RM partageant 240: Plusieurs appareils HoloLens

Les hologrammes sont présents dans notre monde en restant en place au fur et à mesure que nous nous déplacerons dans l’espace. HoloLens conserve les hologrammes en place à l’aide de différents [systèmes de coordonnées](coordinate-systems.md) pour effectuer le suivi de l’emplacement et de l’orientation des objets. Lorsque nous partageons ces systèmes de coordonnées entre les appareils, nous pouvons créer une expérience partagée qui nous permet de participer à un monde holographique partagé.

Dans ce didacticiel, nous allons:

* Configurez un réseau pour une expérience partagée.
* Partager des hologrammes sur des appareils HoloLens.
* Découvrez d’autres personnes dans notre monde holographique partagé.
* Créez une expérience interactive partagée où vous pouvez cibler d’autres joueurs et lancer des projectiles!

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>RM partageant 240: Plusieurs appareils HoloLens</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md) avec l’accès à Internet.
* Au moins deux appareils HoloLens [configurés pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-240-SharedHolograms.zip) requis par le projet. Requiert Unity 2017,2 ou une version ultérieure.
  * Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-240.zip).
  * Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-240.zip).
  * Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-240.zip).
* Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre. Conservez le nom du dossier en tant que **SharedHolograms**.

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-240-SharedHolograms).

## <a name="chapter-1---holo-world"></a>Chapitre 1-Holo World

>[!VIDEO https://www.youtube.com/embed/c7qHYYW8rxQ]

Dans ce chapitre, nous allons configurer notre premier projet Unity et effectuer un pas à pas détaillé dans le processus de création et de déploiement.

### <a name="objectives"></a>Objectifs

* Configurer Unity pour développer des applications holographiques.
* Consultez votre hologramme!

### <a name="instructions"></a>Instructions

* Démarrez Unity.
* Sélectionnez **ouvrir**.
* Entrez l’emplacement du dossier **SharedHolograms** que vous avez précédemment désarchivé.
* Sélectionnez le **nom du projet** , puis cliquez sur Sélectionner un **dossier**.
* Dans la **hiérarchie**, cliquez avec le bouton droit sur l' **appareil photo principal** et sélectionnez **supprimer**.
* Dans le dossier **HoloToolkit-partage-240/Prefabs/Camera** , recherchez la **caméra principale** Prefab.
* Glissez-déposez la **caméra principale** dans la **hiérarchie**.
* Dans la **hiérarchie**, cliquez sur **créer** et **créez un vide**.
* Cliquez avec le bouton droit sur le nouveau **gameobject** , puis sélectionnez Renommer.
* Renommez GameObject en **HologramCollection**.
* Sélectionnez l’objet **HologramCollection** dans la **hiérarchie**.
* Dans l' **inspecteur** , définissez la position de la **transformation** sur: **X 0, Y:-0,25, Z: 2**.
* Dans le  dossier hologrammes du **panneau Projet**, recherchez la ressource **EnergyHub** .
* Glissez-déplacez l’objet **EnergyHub** du **panneau Projet** vers la **hiérarchie** en tant qu' **enfant de HologramCollection**.
* Sélectionnez le **fichier > enregistrer la scène sous...**
* Nommez la scène **SharedHolograms** , puis cliquez sur **Enregistrer**.
* Appuyez sur le bouton de **lecture** dans Unity pour afficher un aperçu de vos hologrammes.
* Appuyez sur **lecture** une deuxième fois pour arrêter le mode aperçu.

**Exporter le projet d’Unity vers Visual Studio**
* Dans Unity, sélectionnez **fichier > paramètres de build**.
* Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.
* Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur basculer la **plateforme**.
* Affectez à **SDK** la valeur **Universal 10**.
* Définissez le **périphérique cible** sur **HoloLens** et le **type de build UWP** sur **D3D**.
* Vérifiez **les C# projets Unity**.
* Cliquez sur **Build**.
* Dans la fenêtre de l’Explorateur de fichiers qui s’affiche, créez un **nouveau dossier** nommé «App».
* Cliquez sur le dossier de l' **application** .
* Appuyez sur **Sélectionner un dossier**.
* Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.
* Ouvrez le dossier de l' **application** .
* Ouvrez **SharedHolograms. sln** pour lancer Visual Studio.
* À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.
* Cliquez sur la flèche déroulante en regard de ordinateur local, puis sélectionnez **périphérique distant**.
    * Définissez l' **adresse** sur le nom ou l’adresse IP de votre HoloLens. Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées** ou demandez à Cortana **«Hey Cortana, qu’est-ce que mon adresse IP?»**
    * Laissez le **mode d’authentification** défini sur **universel**.
    * Cliquez sur **Sélectionner**
* Cliquez sur déboguer **> exécuter sans débogage** ou appuyez sur **CTRL + F5**. S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le coupler à [Visual Studio](using-visual-studio.md#pairing-your-device-hololens).
* Placez sur HoloLens et recherchez l’hologramme EnergyHub.

## <a name="chapter-2---interaction"></a>Chapitre 2-interaction

>[!VIDEO https://www.youtube.com/embed/W60xG15a8gc]

Dans ce chapitre, nous interagissons avec nos hologrammes. Tout d’abord, nous allons ajouter un curseur pour visualiser notre point de [regard](gaze.md). Ensuite, nous ajouterons des [gestes](gestures.md) et utilisons notre main pour placer nos hologrammes dans l’espace.

### <a name="objectives"></a>Objectifs

* Utilisez l’entrée de regard pour contrôler un curseur.
* Utilisez l’entrée de mouvement pour interagir avec des hologrammes.

### <a name="instructions"></a>Instructions

**Pointage du regard**
* Dans le **volet de hiérarchie** , sélectionnez l’objet **HologramCollection** .
* Dans le **volet** de l’inspecteur, cliquez sur le bouton **Ajouter un composant** .
* Dans le menu, tapez dans la zone de recherche **Gestionnaire de regard**. Sélectionnez le résultat de la recherche.
* Dans le dossier **HoloToolkit-Sharing-240\Prefabs\Input** , recherchez la ressource **curseur** .
* Faites glisser et déposez la ressource **curseur** dans la **hiérarchie**.

**Mouvement**
* Dans le **volet de hiérarchie** , sélectionnez l’objet **HologramCollection** .
* Cliquez sur **Ajouter un composant** et tapez gestionnaire de **mouvements** dans le champ de recherche. Sélectionnez le résultat de la recherche.
* Dans le **volet hiérarchie**, développez **HologramCollection**.
* Sélectionnez l’objet **EnergyHub** enfant.
* Dans le **volet** de l’inspecteur, cliquez sur le bouton **Ajouter un composant** .
* Dans le menu, tapez dans la zone de recherche placement de l' **hologramme**. Sélectionnez le résultat de la recherche.
* Enregistrez la scène en sélectionnant **fichier > enregistrer la scène**.

**Déployer et apprécier**
* Créez et déployez sur votre HoloLens, en suivant les instructions du chapitre précédent.
* Une fois l’application lancée sur votre HoloLens, déplacez votre tête et notez la façon dont la EnergyHub suit votre point de regard.
* Notez que le curseur s’affiche lorsque vous pointez sur l’hologramme et qu’il passe à une lumière de point lorsque vous n’êtes pas Gazing à un hologramme.
* Effectuez un TAP-Air pour placer l’hologramme. À ce stade de notre projet, vous ne pouvez placer l’hologramme qu’une seule fois (redéployer pour réessayer).

## <a name="chapter-3---shared-coordinates"></a>Chapitre 3-coordonnées partagées

>[!VIDEO https://www.youtube.com/embed/Ey8yBgWiqtg]

Il est amusant de voir et d’interagir avec les hologrammes, mais nous allons aller plus loin. Nous allons configurer notre première expérience partagée: un hologramme tout le monde peut le voir ensemble.

### <a name="objectives"></a>Objectifs

* Configurez un réseau pour une expérience partagée.
* Établissez un point de référence commun.
* Partager des systèmes de coordonnées entre les appareils.
* Tout le monde voit le même hologramme!

>[!NOTE]
>Les fonctionnalités **InternetClientServer** et **PrivateNetworkClientServer** doivent être déclarées pour qu’une application se connecte au serveur de partage. Cela est fait pour vous déjà dans les hologrammes 240, mais gardez cela à l’esprit pour vos propres projets.
>1. Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à «modifier les paramètres du projet > > Player».
>2. Cliquer sur l’onglet «Windows Store»
>3. Dans la section «fonctionnalités de > des paramètres de publication», vérifiez la capacité de **InternetClientServer** et la capacité de **PrivateNetworkClientServer**

### <a name="instructions"></a>Instructions

* Dans le **panneau Projet** , accédez au dossier **HoloToolkit-Sharing-240\Prefabs\Sharing** .
* Faites glisser et déposez le Prefab de **partage** dans le **panneau de hiérarchie**.

Nous devons ensuite lancer le service de partage. **Un seul ordinateur** de l’expérience partagée doit effectuer cette étape.
* Dans Unity, dans le menu de niveau supérieur, sélectionnez le **menu HoloToolkit-Sharing-240**.
* Sélectionnez l’élément **Démarrer le partage de service** dans la liste déroulante.
* Cochez l’option **réseau privé** , puis cliquez sur **autoriser l’accès** lorsque l’invite de pare-feu s’affiche.
* Notez l’adresse IPv4 affichée dans la fenêtre de console du service de partage. Il s’agit de la même adresse IP que la machine sur laquelle le service est en cours d’exécution.

Suivez le reste des instructions sur **tous les PC** qui vont rejoindre l’expérience partagée.
* Dans la **hiérarchie**, sélectionnez l’objet de **partage** .
* Dans l' **inspecteur**, sur le composant **étape de partage** , remplacez l’adresse du **serveur** «localhost» par l’adresse IPv4 de l’ordinateur exécutant SharingService. exe.
* Dans la **hiérarchie** , sélectionnez l’objet **HologramCollection** .
* Dans l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
* Dans la zone de recherche, tapez **Import exporter Anchor Manager**. Sélectionnez le résultat de la recherche.
* Dans le **panneau Projet** , accédez au dossier **scripts** .
* Double-cliquez sur le script **HologramPlacement** pour l’ouvrir dans Visual Studio.
* Remplacez le contenu par le code ci-dessous.

```cs
using UnityEngine;
using System.Collections.Generic;
using UnityEngine.Windows.Speech;
using Academy.HoloToolkit.Unity;
using Academy.HoloToolkit.Sharing;

public class HologramPlacement : Singleton<HologramPlacement>
{
    /// <summary>
    /// Tracks if we have been sent a transform for the anchor model.
    /// The anchor model is rendered relative to the actual anchor.
    /// </summary>
    public bool GotTransform { get; private set; }

    private bool animationPlayed = false;

    void Start()
    {
        // We care about getting updates for the anchor transform.
        CustomMessages.Instance.MessageHandlers[CustomMessages.TestMessageID.StageTransform] = this.OnStageTransform;

        // And when a new user join we will send the anchor transform we have.
        SharingSessionTracker.Instance.SessionJoined += Instance_SessionJoined;
    }

    /// <summary>
    /// When a new user joins we want to send them the relative transform for the anchor if we have it.
    /// </summary>
    /// <param name="sender"></param>
    /// <param name="e"></param>
    private void Instance_SessionJoined(object sender, SharingSessionTracker.SessionJoinedEventArgs e)
    {
        if (GotTransform)
        {
            CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
        }
    }

    void Update()
    {
        if (GotTransform)
        {
            if (ImportExportAnchorManager.Instance.AnchorEstablished &&
                animationPlayed == false)
            {
                // This triggers the animation sequence for the anchor model and 
                // puts the cool materials on the model.
                GetComponent<EnergyHubBase>().SendMessage("OnSelect");
                animationPlayed = true;
            }
        }
        else
        {
            transform.position = Vector3.Lerp(transform.position, ProposeTransformPosition(), 0.2f);
        }
    }

    Vector3 ProposeTransformPosition()
    {
        // Put the anchor 2m in front of the user.
        Vector3 retval = Camera.main.transform.position + Camera.main.transform.forward * 2;

        return retval;
    }

    public void OnSelect()
    {
        // Note that we have a transform.
        GotTransform = true;
        
        // And send it to our friends.
        CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
    }

    /// <summary>
    /// When a remote system has a transform for us, we'll get it here.
    /// </summary>
    /// <param name="msg"></param>
    void OnStageTransform(NetworkInMessage msg)
    {
        // We read the user ID but we don't use it here.
        msg.ReadInt64();

        transform.localPosition = CustomMessages.Instance.ReadVector3(msg);
        transform.localRotation = CustomMessages.Instance.ReadQuaternion(msg);

        // The first time, we'll want to send the message to the anchor to do its animation and
        // swap its materials.
        if (GotTransform == false)
        {
            GetComponent<EnergyHubBase>().SendMessage("OnSelect");
        }

        GotTransform = true;
    }

    public void ResetStage()
    {
        // We'll use this later.
    }
}
```

* De retour dans Unity, sélectionnez le **HologramCollection** dans le panneau de la **hiérarchie**.
* Dans le **volet** de l’inspecteur, cliquez sur le bouton **Ajouter un composant** .
* Dans le menu, tapez dans la zone de recherche **Gestionnaire d’état des applications**. Sélectionnez le résultat de la recherche.

**Déployer et apprécier**
* Générez le projet pour vos appareils HoloLens.
* Désignez un HoloLens à déployer au préalable. Vous devez attendre que le point d’ancrage soit téléchargé vers le service avant de pouvoir placer le EnergyHub (cette opération peut prendre environ 30-60 secondes). Tant que le téléchargement n’est pas terminé, vos gestes TAP seront ignorés.
* Une fois que le EnergyHub a été placé, son emplacement est chargé sur le service et vous pouvez le déployer sur tous les autres appareils HoloLens.
* Quand un nouveau HoloLens rejoint pour la première fois dans la session, l’emplacement du EnergyHub peut ne pas être correct sur cet appareil. Toutefois, dès que les emplacements d’ancrage et de EnergyHub ont été téléchargés à partir du service, le EnergyHub doit accéder au nouvel emplacement partagé. Si cela ne se produit pas dans un délai de environ 30-60 secondes, passez à l’emplacement de l’HoloLens d’origine lors de la définition de l’ancre pour obtenir davantage d’indices d’environnement. Si l’emplacement ne verrouille toujours pas, redéployez sur l’appareil.
* Une fois que les appareils sont prêts et que vous exécutez l’application, recherchez EnergyHub. Pouvez-vous tous les accepter sur l’emplacement de l’hologramme et la direction dans laquelle le texte est dirigé?

## <a name="chapter-4---discovery"></a>Chapitre 4-détection

>[!VIDEO https://www.youtube.com/embed/5NxJWMV4BP8]

Tout le monde peut désormais Voir le même hologramme! Voyons à présent tous les autres utilisateurs connectés à notre environnement holographique partagé. Dans ce chapitre, nous allons récupérer l’emplacement et la rotation de tous les autres appareils HoloLens dans la même session de partage.

### <a name="objectives"></a>Objectifs

* Découvrez les autres dans notre expérience partagée.
* Choisissez et partagez un avatar de joueur.
* Attachez l’avatar du joueur à côté de tout le monde.

### <a name="instructions"></a>Instructions

* Dans le **panneau Projet** , accédez au  dossier hologrammes.
* Glissez-déplacez le **PlayerAvatarStore** dans la **hiérarchie**.
* Dans le **panneau Projet** , accédez au dossier **scripts** .
* Double-cliquez sur le script **AvatarSelector** pour l’ouvrir dans Visual Studio.
* Remplacez le contenu par le code ci-dessous.

```cs
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Script to handle the user selecting the avatar.
/// </summary>
public class AvatarSelector : MonoBehaviour
{
    /// <summary>
    /// This is the index set by the PlayerAvatarStore for the avatar.
    /// </summary>
    public int AvatarIndex { get; set; }

    /// <summary>
    /// Called when the user is gazing at this avatar and air-taps it.
    /// This sends the user's selection to the rest of the devices in the experience.
    /// </summary>
    void OnSelect()
    {
        PlayerAvatarStore.Instance.DismissAvatarPicker();

        LocalPlayerManager.Instance.SetUserAvatar(AvatarIndex);        
    }

    void Start()
    {
        // Add Billboard component so the avatar always faces the user.
        Billboard billboard = gameObject.GetComponent<Billboard>();
        if (billboard == null)
        {
            billboard = gameObject.AddComponent<Billboard>();
        }

        // Lock rotation along the Y axis.
        billboard.PivotAxis = PivotAxis.Y;
    }
}
```

* Dans la **hiérarchie** , sélectionnez l’objet **HologramCollection** .
* Dans l' **inspecteur** , cliquez sur **Ajouter un composant**.
* Dans la zone de recherche, tapez **Gestionnaire de lecteur local**. Sélectionnez le résultat de la recherche.
* Dans la **hiérarchie** , sélectionnez l’objet **HologramCollection** .
* Dans l' **inspecteur** , cliquez sur **Ajouter un composant**.
* Dans la zone de recherche, tapez **Gestionnaire de lecteur distant**. Sélectionnez le résultat de la recherche.
* Ouvrez le script **HologramPlacement** dans Visual Studio.
* Remplacez le contenu par le code ci-dessous.

```cs
using UnityEngine;
using System.Collections.Generic;
using UnityEngine.Windows.Speech;
using Academy.HoloToolkit.Unity;
using Academy.HoloToolkit.Sharing;

public class HologramPlacement : Singleton<HologramPlacement>
{
    /// <summary>
    /// Tracks if we have been sent a transform for the model.
    /// The model is rendered relative to the actual anchor.
    /// </summary>
    public bool GotTransform { get; private set; }

    /// <summary>
    /// When the experience starts, we disable all of the rendering of the model.
    /// </summary>
    List<MeshRenderer> disabledRenderers = new List<MeshRenderer>();

    void Start()
    {
        // When we first start, we need to disable the model to avoid it obstructing the user picking a hat.
        DisableModel();

        // We care about getting updates for the model transform.
        CustomMessages.Instance.MessageHandlers[CustomMessages.TestMessageID.StageTransform] = this.OnStageTransform;

        // And when a new user join we will send the model transform we have.
        SharingSessionTracker.Instance.SessionJoined += Instance_SessionJoined;
    }

    /// <summary>
    /// When a new user joins we want to send them the relative transform for the model if we have it.
    /// </summary>
    /// <param name="sender"></param>
    /// <param name="e"></param>
    private void Instance_SessionJoined(object sender, SharingSessionTracker.SessionJoinedEventArgs e)
    {
        if (GotTransform)
        {
            CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
        }
    }

    /// <summary>
    /// Turns off all renderers for the model.
    /// </summary>
    void DisableModel()
    {
        foreach (MeshRenderer renderer in gameObject.GetComponentsInChildren<MeshRenderer>())
        {
            if (renderer.enabled)
            {
                renderer.enabled = false;
                disabledRenderers.Add(renderer);
            }
        }

        foreach (MeshCollider collider in gameObject.GetComponentsInChildren<MeshCollider>())
        {
            collider.enabled = false;
        }
    }

    /// <summary>
    /// Turns on all renderers that were disabled.
    /// </summary>
    void EnableModel()
    {
        foreach (MeshRenderer renderer in disabledRenderers)
        {
            renderer.enabled = true;
        }

        foreach (MeshCollider collider in gameObject.GetComponentsInChildren<MeshCollider>())
        {
            collider.enabled = true;
        }

        disabledRenderers.Clear();
    }


    void Update()
    {
        // Wait till users pick an avatar to enable renderers.
        if (disabledRenderers.Count > 0)
        {
            if (!PlayerAvatarStore.Instance.PickerActive &&
            ImportExportAnchorManager.Instance.AnchorEstablished)
            {
                // After which we want to start rendering.
                EnableModel();

                // And if we've already been sent the relative transform, we will use it.
                if (GotTransform)
                {
                    // This triggers the animation sequence for the model and 
                    // puts the cool materials on the model.
                    GetComponent<EnergyHubBase>().SendMessage("OnSelect");
                }
            }
        }
        else if (GotTransform == false)
        {
            transform.position = Vector3.Lerp(transform.position, ProposeTransformPosition(), 0.2f);
        }
    }

    Vector3 ProposeTransformPosition()
    {
        // Put the model 2m in front of the user.
        Vector3 retval = Camera.main.transform.position + Camera.main.transform.forward * 2;

        return retval;
    }

    public void OnSelect()
    {
        // Note that we have a transform.
        GotTransform = true;

        // And send it to our friends.
        CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
    }

    /// <summary>
    /// When a remote system has a transform for us, we'll get it here.
    /// </summary>
    /// <param name="msg"></param>
    void OnStageTransform(NetworkInMessage msg)
    {
        // We read the user ID but we don't use it here.
        msg.ReadInt64();

        transform.localPosition = CustomMessages.Instance.ReadVector3(msg);
        transform.localRotation = CustomMessages.Instance.ReadQuaternion(msg);

        // The first time, we'll want to send the message to the model to do its animation and
        // swap its materials.
        if (disabledRenderers.Count == 0 && GotTransform == false)
        {
            GetComponent<EnergyHubBase>().SendMessage("OnSelect");
        }

        GotTransform = true;
    }

    public void ResetStage()
    {
        // We'll use this later.
    }
}
```

* Ouvrez le script **AppStateManager** dans Visual Studio.
* Remplacez le contenu par le code ci-dessous.

```cs
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Keeps track of the current state of the experience.
/// </summary>
public class AppStateManager : Singleton<AppStateManager>
{
    /// <summary>
    /// Enum to track progress through the experience.
    /// </summary>
    public enum AppState
    {
        Starting = 0,
        WaitingForAnchor,
        WaitingForStageTransform,
        PickingAvatar,
        Ready
    }

    /// <summary>
    /// Tracks the current state in the experience.
    /// </summary>
    public AppState CurrentAppState { get; set; }

    void Start()
    {
        // We start in the 'picking avatar' mode.
        CurrentAppState = AppState.PickingAvatar;

        // We start by showing the avatar picker.
        PlayerAvatarStore.Instance.SpawnAvatarPicker();
    }

    void Update()
    {
        switch (CurrentAppState)
        {
            case AppState.PickingAvatar:
                // Avatar picking is done when the avatar picker has been dismissed.
                if (PlayerAvatarStore.Instance.PickerActive == false)
                {
                    CurrentAppState = AppState.WaitingForAnchor;
                }
                break;
            case AppState.WaitingForAnchor:
                if (ImportExportAnchorManager.Instance.AnchorEstablished)
                {
                    CurrentAppState = AppState.WaitingForStageTransform;
                    GestureManager.Instance.OverrideFocusedObject = HologramPlacement.Instance.gameObject;
                }
                break;
            case AppState.WaitingForStageTransform:
                // Now if we have the stage transform we are ready to go.
                if (HologramPlacement.Instance.GotTransform)
                {
                    CurrentAppState = AppState.Ready;
                    GestureManager.Instance.OverrideFocusedObject = null;
                }
                break;
        }
    }
}
```

**Déployer et apprécier**
* Générez et déployez le projet sur vos appareils HoloLens.
* Quand vous entendez un son de ping, recherchez le menu de sélection d’avatar et sélectionnez un avatar avec le geste de pression d’air.
* Si vous n’êtes pas en train de regarder des hologrammes, la lumière du point autour de votre curseur permet de changer de couleur quand votre HoloLens communique avec le service: initialisation (violet foncé), téléchargement de l’ancre (vert), importation/exportation des données d’emplacement (jaune), chargement de l’ancre (bleu). Si votre lumière de point autour de votre curseur est la couleur par défaut (violet clair), vous êtes prêt à interagir avec les autres joueurs de votre session.
* Regardez les autres personnes connectées à votre espace-un robot holographique flotte au-dessus de son épaule et imitant ses mouvements de tête!

## <a name="chapter-5---placement"></a>Chapitre 5-placement

>[!VIDEO https://www.youtube.com/embed/afFTwHQIw0s]

Dans ce chapitre, nous allons faire en sorte que l’ancre puisse être placée sur des surfaces réelles. Nous allons utiliser des coordonnées partagées pour placer cette ancre dans le point central entre tout le monde connecté à l’expérience partagée.

### <a name="objectives"></a>Objectifs

* Placez les hologrammes sur la carte spatiale en fonction de la position de tête des joueurs.

### <a name="instructions"></a>Instructions

* Dans le **panneau Projet** , accédez au  dossier hologrammes.
* Glissez-déplacez le Prefab **CustomSpatialMapping** sur la **hiérarchie**.
* Dans le **panneau Projet** , accédez au dossier **scripts** .
* Double-cliquez sur le script **AppStateManager** pour l’ouvrir dans Visual Studio.
* Remplacez le contenu par le code ci-dessous.

```cs
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Keeps track of the current state of the experience.
/// </summary>
public class AppStateManager : Singleton<AppStateManager>
{
    /// <summary>
    /// Enum to track progress through the experience.
    /// </summary>
    public enum AppState
    {
        Starting = 0,
        PickingAvatar,
        WaitingForAnchor,
        WaitingForStageTransform,
        Ready
    }

    // The object to call to make a projectile.
    GameObject shootHandler = null;

    /// <summary>
    /// Tracks the current state in the experience.
    /// </summary>
    public AppState CurrentAppState { get; set; }

    void Start()
    {
        // The shootHandler shoots projectiles.
        if (GetComponent<ProjectileLauncher>() != null)
        {
            shootHandler = GetComponent<ProjectileLauncher>().gameObject;
        }

        // We start in the 'picking avatar' mode.
        CurrentAppState = AppState.PickingAvatar;

        // Spatial mapping should be disabled when we start up so as not
        // to distract from the avatar picking.
        SpatialMappingManager.Instance.StopObserver();
        SpatialMappingManager.Instance.gameObject.SetActive(false);

        // On device we start by showing the avatar picker.
        PlayerAvatarStore.Instance.SpawnAvatarPicker();
    }

    public void ResetStage()
    {
        // If we fall back to waiting for anchor, everything needed to 
        // get us into setting the target transform state will be setup.
        if (CurrentAppState != AppState.PickingAvatar)
        {
            CurrentAppState = AppState.WaitingForAnchor;
        }

        // Reset the underworld.
        if (UnderworldBase.Instance)
        {
            UnderworldBase.Instance.ResetUnderworld();
        }
    }

    void Update()
    {
        switch (CurrentAppState)
        {
            case AppState.PickingAvatar:
                // Avatar picking is done when the avatar picker has been dismissed.
                if (PlayerAvatarStore.Instance.PickerActive == false)
                {
                    CurrentAppState = AppState.WaitingForAnchor;
                }
                break;
            case AppState.WaitingForAnchor:
                // Once the anchor is established we need to run spatial mapping for a 
                // little while to build up some meshes.
                if (ImportExportAnchorManager.Instance.AnchorEstablished)
                {
                    CurrentAppState = AppState.WaitingForStageTransform;
                    GestureManager.Instance.OverrideFocusedObject = HologramPlacement.Instance.gameObject;

                    SpatialMappingManager.Instance.gameObject.SetActive(true);
                    SpatialMappingManager.Instance.DrawVisualMeshes = true;
                    SpatialMappingDeformation.Instance.ResetGlobalRendering();
                    SpatialMappingManager.Instance.StartObserver();
                }
                break;
            case AppState.WaitingForStageTransform:
                // Now if we have the stage transform we are ready to go.
                if (HologramPlacement.Instance.GotTransform)
                {
                    CurrentAppState = AppState.Ready;
                    GestureManager.Instance.OverrideFocusedObject = shootHandler;
                }
                break;
        }
    }
}
```

* Dans le **panneau Projet** , accédez au dossier **scripts** .
* Double-cliquez sur le script **HologramPlacement** pour l’ouvrir dans Visual Studio.
* Remplacez le contenu par le code ci-dessous.

```cs
using UnityEngine;
using System.Collections.Generic;
using UnityEngine.Windows.Speech;
using Academy.HoloToolkit.Unity;
using Academy.HoloToolkit.Sharing;

public class HologramPlacement : Singleton<HologramPlacement>
{
    /// <summary>
    /// Tracks if we have been sent a transform for the model.
    /// The model is rendered relative to the actual anchor.
    /// </summary>
    public bool GotTransform { get; private set; }

    /// <summary>
    /// When the experience starts, we disable all of the rendering of the model.
    /// </summary>
    List<MeshRenderer> disabledRenderers = new List<MeshRenderer>();

    /// <summary>
    /// We use a voice command to enable moving the target.
    /// </summary>
    KeywordRecognizer keywordRecognizer;

    void Start()
    {
        // When we first start, we need to disable the model to avoid it obstructing the user picking a hat.
        DisableModel();

        // We care about getting updates for the model transform.
        CustomMessages.Instance.MessageHandlers[CustomMessages.TestMessageID.StageTransform] = this.OnStageTransform;

        // And when a new user join we will send the model transform we have.
        SharingSessionTracker.Instance.SessionJoined += Instance_SessionJoined;

        // And if the users want to reset the stage transform.
        CustomMessages.Instance.MessageHandlers[CustomMessages.TestMessageID.ResetStage] = this.OnResetStage;

        // Setup a keyword recognizer to enable resetting the target location.
        List<string> keywords = new List<string>();
        keywords.Add("Reset Target");
        keywordRecognizer = new KeywordRecognizer(keywords.ToArray());
        keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
        keywordRecognizer.Start();
    }

    /// <summary>
    /// When the keyword recognizer hears a command this will be called.  
    /// In this case we only have one keyword, which will re-enable moving the 
    /// target.
    /// </summary>
    /// <param name="args">information to help route the voice command.</param>
    private void KeywordRecognizer_OnPhraseRecognized(PhraseRecognizedEventArgs args)
    {
        ResetStage();
    }

    /// <summary>
    /// Resets the stage transform, so users can place the target again.
    /// </summary>
    public void ResetStage()
    {
        GotTransform = false;

        // AppStateManager needs to know about this so that
        // the right objects get input routed to them.
        AppStateManager.Instance.ResetStage();

        // Other devices in the experience need to know about this as well.
        CustomMessages.Instance.SendResetStage();

        // And we need to reset the object to its start animation state.
        GetComponent<EnergyHubBase>().ResetAnimation();
    }

    /// <summary>
    /// When a new user joins we want to send them the relative transform for the model if we have it.
    /// </summary>
    /// <param name="sender"></param>
    /// <param name="e"></param>
    private void Instance_SessionJoined(object sender, SharingSessionTracker.SessionJoinedEventArgs e)
    {
        if (GotTransform)
        {
            CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
        }
    }

    /// <summary>
    /// Turns off all renderers for the model.
    /// </summary>
    void DisableModel()
    {
        foreach (MeshRenderer renderer in gameObject.GetComponentsInChildren<MeshRenderer>())
        {
            if (renderer.enabled)
            {
                renderer.enabled = false;
                disabledRenderers.Add(renderer);
            }
        }

        foreach (MeshCollider collider in gameObject.GetComponentsInChildren<MeshCollider>())
        {
            collider.enabled = false;
        }
    }

    /// <summary>
    /// Turns on all renderers that were disabled.
    /// </summary>
    void EnableModel()
    {
        foreach (MeshRenderer renderer in disabledRenderers)
        {
            renderer.enabled = true;
        }

        foreach (MeshCollider collider in gameObject.GetComponentsInChildren<MeshCollider>())
        {
            collider.enabled = true;
        }

        disabledRenderers.Clear();
    }


    void Update()
    {
        // Wait till users pick an avatar to enable renderers.
        if (disabledRenderers.Count > 0)
        {
            if (!PlayerAvatarStore.Instance.PickerActive &&
            ImportExportAnchorManager.Instance.AnchorEstablished)
            {
                // After which we want to start rendering.
                EnableModel();

                // And if we've already been sent the relative transform, we will use it.
                if (GotTransform)
                {
                    // This triggers the animation sequence for the model and 
                    // puts the cool materials on the model.
                    GetComponent<EnergyHubBase>().SendMessage("OnSelect");
                }
            }
        }
        else if (GotTransform == false)
        {
            transform.position = Vector3.Lerp(transform.position, ProposeTransformPosition(), 0.2f);
        }
    }

    Vector3 ProposeTransformPosition()
    {
        Vector3 retval;
        // We need to know how many users are in the experience with good transforms.
        Vector3 cumulatedPosition = Camera.main.transform.position;
        int playerCount = 1;
        foreach (RemotePlayerManager.RemoteHeadInfo remoteHead in RemotePlayerManager.Instance.remoteHeadInfos)
        {
            if (remoteHead.Anchored && remoteHead.Active)
            {
                playerCount++;
                cumulatedPosition += remoteHead.HeadObject.transform.position;
            }
        }

        // If we have more than one player ...
        if (playerCount > 1)
        {
            // Put the transform in between the players.
            retval = cumulatedPosition / playerCount;
            RaycastHit hitInfo;

            // And try to put the transform on a surface below the midpoint of the players.
            if (Physics.Raycast(retval, Vector3.down, out hitInfo, 5, SpatialMappingManager.Instance.LayerMask))
            {
                retval = hitInfo.point;
            }
        }
        // If we are the only player, have the model act as the 'cursor' ...
        else
        {
            // We prefer to put the model on a real world surface.
            RaycastHit hitInfo;

            if (Physics.Raycast(Camera.main.transform.position, Camera.main.transform.forward, out hitInfo, 30, SpatialMappingManager.Instance.LayerMask))
            {
                retval = hitInfo.point;
            }
            else
            {
                // But if we don't have a ray that intersects the real world, just put the model 2m in
                // front of the user.
                retval = Camera.main.transform.position + Camera.main.transform.forward * 2;
            }
        }
        return retval;
    }

    public void OnSelect()
    {
        // Note that we have a transform.
        GotTransform = true;

        // And send it to our friends.
        CustomMessages.Instance.SendStageTransform(transform.localPosition, transform.localRotation);
    }

    /// <summary>
    /// When a remote system has a transform for us, we'll get it here.
    /// </summary>
    /// <param name="msg"></param>
    void OnStageTransform(NetworkInMessage msg)
    {
        // We read the user ID but we don't use it here.
        msg.ReadInt64();

        transform.localPosition = CustomMessages.Instance.ReadVector3(msg);
        transform.localRotation = CustomMessages.Instance.ReadQuaternion(msg);

        // The first time, we'll want to send the message to the model to do its animation and
        // swap its materials.
        if (disabledRenderers.Count == 0 && GotTransform == false)
        {
            GetComponent<EnergyHubBase>().SendMessage("OnSelect");
        }

        GotTransform = true;
    }

    /// <summary>
    /// When a remote system has a transform for us, we'll get it here.
    /// </summary>
    void OnResetStage(NetworkInMessage msg)
    {
        GotTransform = false;

        GetComponent<EnergyHubBase>().ResetAnimation();
        AppStateManager.Instance.ResetStage();
    }
}
```

**Déployer et apprécier**
* Générez et déployez le projet sur vos appareils HoloLens.
* Lorsque l’application est prête, mettez-la dans un cercle et observez la façon dont le EnergyHub apparaît au centre de tout le monde.
* Appuyez pour placer le EnergyHub.
* Essayez la commande vocale «réinitialiser la cible» pour sélectionner le EnergyHub de sauvegarde et travailler ensemble en tant que groupe pour déplacer l’hologramme vers un nouvel emplacement.

## <a name="chapter-6---real-world-physics"></a>Chapitre 6-physique réel

>[!VIDEO https://www.youtube.com/embed/XNpQVSyXwMo]

Dans ce chapitre, nous allons ajouter des hologrammes qui rebondissent sur des surfaces réelles. Regardez votre espace plein avec les projets lancés par vous et vos amis!

### <a name="objectives"></a>Objectifs

* Lancez des projectiles qui rebondissent sur des surfaces réelles.
* Partagez les projectiles afin que d’autres joueurs puissent les voir.

### <a name="instructions"></a>Instructions

* Dans la **hiérarchie** , sélectionnez l’objet **HologramCollection** .
* Dans l' **inspecteur** , cliquez sur **Ajouter un composant**.
* Dans la zone de recherche, tapez lanceur de projectiles. Sélectionnez le résultat de la recherche.

**Déployer et apprécier**
* Créez et déployez sur vos appareils HoloLens.
* Lorsque l’application est en cours d’exécution sur tous les appareils, effectuez un taraudage pour lancer un projectile à des surfaces réelles.
* Voyez ce qui se passe lorsque votre projectile entre en conflit avec un avatar d’un joueur!

## <a name="chapter-7---grand-finale"></a>Chapitre 7-finalisation général

>[!VIDEO https://www.youtube.com/embed/kDUPUvZEqRg]

Dans ce chapitre, nous allons découvrir un portail qui peut être découvert uniquement avec la collaboration.

### <a name="objectives"></a>Objectifs

* Collaborez pour lancer suffisamment de projectiles à l’ancre pour découvrir un portail de secret.

### <a name="instructions"></a>Instructions

* Dans le **panneau Projet** , accédez au  dossier hologrammes.
* Faites glisser et déposez la ressource de sous- **monde** en tant qu' **enfant de HologramCollection**.
* Avec **HologramCollection** sélectionné, cliquez sur le bouton **Ajouter un composant** dans l' **inspecteur**.
* Dans le menu, tapez dans la zone de recherche **ExplodeTarget**. Sélectionnez le résultat de la recherche.
* Avec **HologramCollection** sélectionné, dans la **hiérarchie** , faites glisser l’objet **EnergyHub** vers le champ **cible** de l' **inspecteur**.
* Lorsque **HologramCollection** est sélectionné, dans la **hiérarchie** , faites glisser l’objet «sous- **monde** » vers le champ «sous- **monde** » de l' **inspecteur**.

**Déployer et apprécier**
* Créez et déployez sur vos appareils HoloLens.
* Lorsque l’application a démarré, collaborez pour lancer des projectiles au EnergyHub.
* Quand le sous-monde s’affiche, lancez des projectiles chez les robots du sous-monde (un robot se trouve trois fois plus amusant).
