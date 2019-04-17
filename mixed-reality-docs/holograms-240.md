---
title: MR partage 240 - plusieurs appareils HoloLens
description: Suivez cette procédure pas à pas à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails du partage hologrammes de codage.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, sharing, networking, academy, tutorial
ms.openlocfilehash: 70a39a739d360a5032bc8df76b6f0bd57521d9ec
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594888"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-sharing-240-multiple-hololens-devices"></a>MR 240 de partage : Plusieurs appareils HoloLens

Hologrammes reçoivent présence dans notre monde par reste en place lorsque nous transférerons dans l’espace. HoloLens conserve hologrammes en place à l’aide de divers [systèmes de coordonnées](coordinate-systems.md) pour effectuer le suivi de l’emplacement et l’orientation des objets. Lorsque nous partageons ces systèmes de coordonnées entre les appareils, nous pouvons créer une expérience partagée qui permet de prendre part à un monde HOLOGRAPHIQUE partagé.

Dans ce didacticiel, nous allons :

* Configuration d’un réseau pour une expérience partagée.
* Partager hologrammes entre les appareils HoloLens.
* Découvrir d’autres personnes de notre monde HOLOGRAPHIQUE partagé.
* Créer une expérience interactive partagée où vous pouvez cibler d’autres joueurs - et lancer des projectiles sur leur !

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>MR 240 de partage : Plusieurs appareils HoloLens</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md) avec accès à Internet.
* Au moins deux appareils HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-240-SharedHolograms.zip) requise par le projet. Nécessite Unity 2017.2 ou version ultérieure.
  * Si vous avez besoin de prise en charge de Unity 5.6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-240.zip).
  * Si vous avez besoin de prise en charge de Unity 5.5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-240.zip).
  * Si vous avez besoin de prise en charge de Unity 5.4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-240.zip).
* Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement. Conservez le nom de dossier en tant que **SharedHolograms**.

>[!NOTE]
>Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-240-SharedHolograms).

## <a name="chapter-1---holo-world"></a>Chapitre 1 - Holo World

>[!VIDEO https://www.youtube.com/embed/c7qHYYW8rxQ]

Dans ce chapitre, nous le programme d’installation de notre premier projet Unity et les étapes à la build et processus de déploiement.

### <a name="objectives"></a>Objectifs

* Le programme d’installation Unity pour développer des applications HOLOGRAPHIQUE.
* Consultez votre HOLOGRAMME !

### <a name="instructions"></a>Instructions

* Démarrez Unity.
* Sélectionnez **Open**.
* Entrez l’emplacement que le **SharedHolograms** dossier vous non précédemment archivé.
* Sélectionnez **nom_projet** et cliquez sur **sélectionner le dossier**.
* Dans le **hiérarchie**, avec le bouton droit le **Main Camera** et sélectionnez **supprimer**.
* Dans le **HoloToolkit partage-240/Prefabs/caméra** dossier, recherchez le **Main Camera** prefab.
* Faites glisser et déposez le **Main Camera** dans le **hiérarchie**.
* Dans le **hiérarchie**, cliquez sur **créer** et **créer vide**.
* Cliquez sur le nouveau **GameObject** et sélectionnez **renommer**.
* Renommer le GameObject à **HologramCollection**.
* Sélectionnez le **HologramCollection** de l’objet dans le **hiérarchie**.
* Dans le **inspecteur** définir le **transformer position** à : **X : 0, Y : -0,25, Z : 2**.
* Dans le **Vntana** dossier dans le **panneau projet**, trouver la **EnergyHub** asset.
* Faites glisser et déposez le **EnergyHub** à partir de l’objet le **panneau projet** à la **hiérarchie** en tant qu’un **enfant de HologramCollection**.
* Sélectionnez **fichier > Enregistrer la scène sous...**
* Nommez la scène **SharedHolograms** et cliquez sur **enregistrer**.
* Appuyez sur la **lire** bouton dans Unity pour afficher un aperçu votre hologrammes.
* Appuyez sur **lire** une deuxième fois pour arrêter le mode d’aperçu.

**Exportez le projet à partir d’Unity pour Visual Studio**
* Dans, sélectionnez Unity **fichier > Paramètres de Build**.
* Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.
* Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.
* Définissez **SDK** à **10 universelle**.
* Définissez **appareil cible** à **HoloLens** et **Type de Build UWP** à **D3D**.
* Vérifiez **Unity C# projets**.
* Cliquez sur **Build**.
* Dans la fenêtre Explorateur de fichiers qui s’affiche, créez un **nouveau dossier** nommé « Application ».
* Clic le **application** dossier.
* Appuyez sur **sélectionnez dossier**.
* Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.
* Ouvrez le **application** dossier.
* Ouvrez **SharedHolograms.sln** pour lancer Visual Studio.
* À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **X86**.
* Cliquez sur la flèche déroulante en regard de l’ordinateur Local, puis sélectionnez **périphérique distant**.
    * Définir le **adresse** au nom ou adresse IP de votre HoloLens. Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées** ou demandez à Cortana **« Hey Cortana, quelle est mon adresse IP ? »**
    * Laissez le **Mode d’authentification** définie sur **universelle**.
    * Cliquez sur **sélectionnez**
* Cliquez sur **Déboguer > Démarrer sans débogage** ou appuyez sur **Ctrl + F5**. S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device-hololens).
* Placez sur votre HoloLens et trouver l’hologramme EnergyHub.

## <a name="chapter-2---interaction"></a>Chapitre 2 - Interaction

>[!VIDEO https://www.youtube.com/embed/W60xG15a8gc]

Dans ce chapitre, nous permettra d’interagir avec notre hologrammes. Tout d’abord, nous allons ajouter un curseur pour visualiser notre [les regards](gaze.md). Ensuite, nous allons ajouter [mouvements](gestures.md) et utiliser notre main placer notre hologrammes dans l’espace.

### <a name="objectives"></a>Objectifs

* Utilisez les regards d’entrée pour contrôler un curseur.
* Utiliser le mouvement d’entrée pour interagir avec hologrammes.

### <a name="instructions"></a>Instructions

**Gaze**
* Dans le **Panneau de la hiérarchie** sélectionner le **HologramCollection** objet.
* Dans le **panneau Inspecteur** cliquez sur le **ajouter un composant** bouton.
* Dans le menu, tapez dans la zone de recherche **Manager les regards**. Sélectionnez le résultat de recherche.
* Dans le **HoloToolkit partage 240\Prefabs\Input** dossier, recherchez le **curseur** asset.
* Faites glisser et déposez le **curseur** actif sur le **hiérarchie**.

**Mouvement**
* Dans le **Panneau de la hiérarchie** sélectionner le **HologramCollection** objet.
* Cliquez sur **ajouter un composant** et type **Gestionnaire de mouvements** dans le champ de recherche. Sélectionnez le résultat de recherche.
* Dans le **Panneau de la hiérarchie**, développez **HologramCollection**.
* Sélectionnez l’enfant **EnergyHub** objet.
* Dans le **panneau Inspecteur** cliquez sur le **ajouter un composant** bouton.
* Dans le menu, tapez dans la zone de recherche **hologramme Placement**. Sélectionnez le résultat de recherche.
* Enregistrer la scène en sélectionnant **fichier > Enregistrer la scène**.

**Déployer et profitez de**
* Créer et déployer dans votre HoloLens, en suivant les instructions du chapitre précédent.
* Une fois que l’application démarre sur votre HoloLens, déplacer votre tête et notez comment le EnergyHub suit votre regard.
* Remarquez que le curseur s’affiche lorsque vous remplacez l’hologramme et devient une lumière point lorsque ne gazing pas à un hologramme.
* Effectuer un appui pour placer l’hologramme. À ce stade dans notre projet, vous pouvez uniquement placer une fois l’hologramme (redéploiement pour essayer à nouveau).

## <a name="chapter-3---shared-coordinates"></a>Chapitre 3 - partagé coordonne

>[!VIDEO https://www.youtube.com/embed/Ey8yBgWiqtg]

Il est amusant de voir et interagir avec hologrammes, mais allons plus loin. Nous allons configurer notre première expérience partagé - un hologramme tout le monde peut voir ensemble.

### <a name="objectives"></a>Objectifs

* Configuration d’un réseau pour une expérience partagée.
* Établir un point de référence commun.
* Partager des systèmes de coordonnées entre les appareils.
* Tout le monde voit le même HOLOGRAMME !

>[!NOTE]
>Le **InternetClientServer** et **PrivateNetworkClientServer** fonctionnalités doivent être déclarées pour une application à se connecter au serveur partage. Cela est fait pour vous déjà dans hologrammes 240, mais gardez cela à l’esprit pour vos propres projets.
>1. Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »
>2. Cliquez sur l’onglet « Windows Store »
>3. Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **InternetClientServer** fonctionnalité et la **PrivateNetworkClientServer** fonctionnalité

### <a name="instructions"></a>Instructions

* Dans le **panneau projet** accédez à la **HoloToolkit partage 240\Prefabs\Sharing** dossier.
* Faites glisser et déposez le **partage** prefab dans le **Panneau de la hiérarchie**.

Nous devons ensuite lancer le service de partage. Uniquement **un PC** dans le partage rencontrer les besoins d’effectuer cette étape.
* Dans Unity - dans le menu en haut la main, sélectionnez le **HoloToolkit partage 240 menu**.
* Sélectionnez le **lancer le Service de partage** élément dans la liste déroulante.
* Vérifier le **réseau privé** , cliquez sur **autoriser l’accès** lorsque l’invite de pare-feu s’affiche.
* Notez l’adresse IPv4 affichée dans la fenêtre de console de Service de partage. Il s’agit de la même adresse IP que l’ordinateur qu'est en cours d’exécution sur le service.

Suivez le reste des instructions **tous les PC** qui joindra l’expérience partagée.
* Dans le **hiérarchie**, sélectionnez le **partage** objet.
* Dans le **inspecteur**, dans le **étape partage** composant, modifier le **adresse du serveur** à partir de « localhost » à l’adresse IPv4 de l’ordinateur en cours d’exécution SharingService.exe.
* Dans le **hiérarchie** sélectionner le **HologramCollection** objet.
* Dans le **inspecteur** cliquez sur le **ajouter un composant** bouton.
* Dans la zone de recherche, tapez **importer exporter d’ancrage Manager**. Sélectionnez le résultat de recherche.
* Dans le **panneau projet** accédez à la **Scripts** dossier.
* Double-cliquez sur le **HologramPlacement** script pour l’ouvrir dans Visual Studio.
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

* Dans Unity, sélectionnez le **HologramCollection** dans le **Panneau de la hiérarchie**.
* Dans le **panneau Inspecteur** cliquez sur le **ajouter un composant** bouton.
* Dans le menu, tapez dans la zone de recherche **Gestionnaire d’état application**. Sélectionnez le résultat de recherche.

**Déployer et profitez de**
* Générez le projet pour vos appareils HoloLens.
* Désigner un HoloLens à déployer en premier. Vous devez attendre que le point d’ancrage être téléchargé vers le service avant de pouvoir placer le EnergyHub (cette opération peut prendre environ 30 à 60 secondes). Jusqu'à ce que le téléchargement est terminé, votre mouvements tap seront ignorés.
* Une fois le EnergyHub a été placé, son emplacement sera téléchargé vers le service et vous pouvez ensuite déployer sur tous les autres appareils HoloLens.
* Lorsqu’un nouveau HoloLens joint tout d’abord la session, l’emplacement de la EnergyHub n’est peut-être pas correct sur l’appareil. Toutefois, dès que l’ancre et les emplacements de EnergyHub ont été téléchargées à partir du service, le EnergyHub doit accéder à l’emplacement partagé, de nouveau. Si cela n’arrive pas dans environ 30 à 60 secondes, remonter où le HoloLens d’origine était lorsque vous définissez le point d’ancrage pour recueillir plusieurs indices d’environnement. Si l’emplacement ne verrouille pas toujours redéployer, à l’appareil.
* Lorsque les appareils sont prêts et exécution de l’application, recherchez le EnergyHub. Peuvent tous d’accord sur les emplacement de l’hologramme et le sens dans lequel le texte est face ?

## <a name="chapter-4---discovery"></a>Chapitre 4 - découverte

>[!VIDEO https://www.youtube.com/embed/5NxJWMV4BP8]

Tout le monde peut voir maintenant l’hologramme même ! Maintenant nous allons voir tout le monde else connecté à notre monde HOLOGRAPHIQUE partagé. Dans ce chapitre, nous allons saisir l’emplacement principal et la rotation de tous les autres appareils HoloLens dans la même session de partage.

### <a name="objectives"></a>Objectifs

* Découvrir les uns des autres dans notre expérience partagée.
* Choisissez et partager un avatar de lecteur.
* Attacher l’avatar de joueur en regard de têtes de tout le monde.

### <a name="instructions"></a>Instructions

* Dans le **panneau projet** accédez à la **hologrammes** dossier.
* Faites glisser et déposez le **PlayerAvatarStore** dans le **hiérarchie**.
* Dans le **panneau projet** accédez à la **Scripts** dossier.
* Double-cliquez sur le **AvatarSelector** script pour l’ouvrir dans Visual Studio.
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

* Dans le **hiérarchie** sélectionner le **HologramCollection** objet.
* Dans le **inspecteur** cliquez sur **ajouter un composant**.
* Dans la zone de recherche, tapez **Gestionnaire de lecteur Local**. Sélectionnez le résultat de recherche.
* Dans le **hiérarchie** sélectionner le **HologramCollection** objet.
* Dans le **inspecteur** cliquez sur **ajouter un composant**.
* Dans la zone de recherche, tapez **Gestionnaire de lecteur distant**. Sélectionnez le résultat de recherche.
* Ouvrez le **HologramPlacement** script dans Visual Studio.
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

* Ouvrez le **AppStateManager** script dans Visual Studio.
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

**Déployer et profitez de**
* Générer et déployer le projet sur vos appareils HoloLens.
* Lorsque vous entendez un test ping, recherchez le menu de sélection avatar, puis sélectionnez un avatar avec le mouvement d’appui en l’air.
* Si vous n’êtes pas dans n’importe quel hologrammes, le point de lumière autour de votre curseur activera une couleur différente lorsque votre HoloLens communique avec le service : l’initialisation (violet foncé), le téléchargement de point d’ancrage (vert), l’importation/exportation de données d’emplacement (jaune), charger le point d’ancrage (bleu). Si votre point clair autour de votre curseur est la couleur par défaut (Violet clair), vous êtes prêt à interagir avec d’autres joueurs dans votre session !
* Examinez les autres utilisateurs connectés à votre espace - il y aura un robot HOLOGRAPHIQUE flotte au-dessus de son épaule et celle de leurs mouvements principal !

## <a name="chapter-5---placement"></a>Chapitre 5 : Placement

>[!VIDEO https://www.youtube.com/embed/afFTwHQIw0s]

Dans ce chapitre, nous veillerons à ce point d’ancrage peuvent pas être placés sur des surfaces du monde réel. Nous allons utiliser des coordonnées partagées pour placer ce point d’ancrage dans le point médian entre tous les utilisateurs connectés à l’expérience partagée.

### <a name="objectives"></a>Objectifs

* Placez hologrammes sur la carte spatiale en fonction de la position de tête de joueurs.

### <a name="instructions"></a>Instructions

* Dans le **panneau projet** accédez à la **hologrammes** dossier.
* Faites glisser et déposez le **CustomSpatialMapping** prefab sur le **hiérarchie**.
* Dans le **panneau projet** accédez à la **Scripts** dossier.
* Double-cliquez sur le **AppStateManager** script pour l’ouvrir dans Visual Studio.
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

* Dans le **panneau projet** accédez à la **Scripts** dossier.
* Double-cliquez sur le **HologramPlacement** script pour l’ouvrir dans Visual Studio.
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

**Déployer et profitez de**
* Générer et déployer le projet sur vos appareils HoloLens.
* Lorsque l’application est prête, mettez au point dans un cercle et notez que le EnergyHub apparaît au centre de tout le monde.
* Cliquez pour placer le EnergyHub.
* Essayez la commande de voix 'Réinitialiser Target' et reprenez le EnergyHub fonctionnent ensemble en tant que groupe pour déplacer l’hologramme vers un nouvel emplacement.

## <a name="chapter-6---real-world-physics"></a>Chapitre 6 - réel physique

>[!VIDEO https://www.youtube.com/embed/XNpQVSyXwMo]

Dans ce chapitre, nous allons ajouter hologrammes rebondissent sur les surfaces du monde réel. Surveillez votre page se remplisse pas de projets lancés par vous et vos amis !

### <a name="objectives"></a>Objectifs

* Lance des projectiles qui rebondissent sur les surfaces du monde réel.
* Partager les projectiles afin d’autres joueurs puissent les voir.

### <a name="instructions"></a>Instructions

* Dans le **hiérarchie** sélectionner le **HologramCollection** objet.
* Dans le **inspecteur** cliquez sur **ajouter un composant**.
* Dans la zone de recherche, tapez **PROJECTILES Lanceur**. Sélectionnez le résultat de recherche.

**Déployer et profitez de**
* Générer et déployer sur vos appareils HoloLens.
* Lorsque l’application s’exécute sur tous les appareils, effectuez un appui pour lancer des projectiles sur les surfaces du monde réel.
* Découvrez ce qui se passe lorsque votre PROJECTILES est en conflit avec les avatar d’un autre lecteur.

## <a name="chapter-7---grand-finale"></a>Chapitre 7 - aborder

>[!VIDEO https://www.youtube.com/embed/kDUPUvZEqRg]

Dans ce chapitre, nous allons découvrir un portail qui ne peut être détecté à la collaboration.

### <a name="objectives"></a>Objectifs

* Œuvrent ensemble pour lancer suffisamment projectiles sur le point d’ancrage pour découvrir un portail secret !

### <a name="instructions"></a>Instructions

* Dans le **panneau projet** accédez à la **hologrammes** dossier.
* Faites glisser et déposez le **Underworld** actif comme un **enfant de HologramCollection**.
* Avec **HologramCollection** sélectionnée, cliquez sur le **ajouter un composant** situé dans le **inspecteur**.
* Dans le menu, tapez dans la zone de recherche **ExplodeTarget**. Sélectionnez le résultat de recherche.
* Avec **HologramCollection** sélectionné, à partir de la **hiérarchie** faites glisser le **EnergyHub** de l’objet à la **cible** champ dans le **Inspecteur**.
* Avec **HologramCollection** sélectionné, à partir de la **hiérarchie** faites glisser le **Underworld** de l’objet à la **Underworld** champ dans le  **Inspecteur de**.

**Déployer et profitez de**
* Générer et déployer sur vos appareils HoloLens.
* Lorsque l’application est lancée, collaborer pour lancer des projectiles sur le EnergyHub.
* Lorsque l’underworld s’affiche, lancer des projectiles sur les robots underworld (atteinte un robot trois fois pour le plaisir supplémentaire).
