---
title: Entrée MR 211-geste
description: Suivez cette procédure pas à pas de codage à l’aide de Unity, Visual Studio et HoloLens pour apprendre les concepts de mouvement.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, geste
ms.openlocfilehash: 76d2b4c0ac3d0a3783b091f7dc8c39548a18b548
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522452"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

# <a name="mr-input-211-gesture"></a>Monsieur 211: Mouvement

Les [gestes](gestures.md) transforment l’intention de l’utilisateur en action. Avec les gestes, les utilisateurs peuvent interagir avec des hologrammes. Dans ce cours, nous allons apprendre à suivre les mains de l’utilisateur, à répondre aux entrées de l’utilisateur et à envoyer des commentaires à l’utilisateur en fonction de l’État et de l’emplacement de la main.

>[!VIDEO https://www.youtube.com/embed/c9zlpfFeEtc]

Dans les [notions de base de m. 101](holograms-101.md), nous avons utilisé un simple geste d’appui sur l’air pour interagir avec nos hologrammes. À présent, nous allons aller au-delà du geste d’entrée aérienne et explorer de nouveaux concepts pour:

* Détectez le moment où l’utilisateur fait l’objet d’un suivi et fournissez des commentaires à l’utilisateur.
* Utilisez un mouvement de navigation pour faire pivoter nos hologrammes.
* Fournir des commentaires lorsque la main de l’utilisateur est sur le point de sortir de l’affichage.
* Utilisez des événements de manipulation pour permettre aux utilisateurs de déplacer des hologrammes.

Dans ce cours, nous allons revisiter l' **Explorateur de modèles**de projet Unity, que nous avons créé dans l' [entrée 210](holograms-210.md)de la m. Notre ami astronautes est en retour pour nous aider dans notre exploration de ces nouveaux concepts de mouvement.

>[!IMPORTANT]
>Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrées à l’aide d’une version antérieure d’Unity et de la réalité mixte Toolkit. Alors que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des visuels dans les vidéos correspondantes qui sont obsolètes. Les vidéos restent incluses pour l’affiche et les concepts abordés s’appliquent toujours.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>Monsieur 211: Mouvement</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).
* Certaines fonctionnalités C# de programmation de base.
* Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).
* Vous devez avoir terminé l' [entrée 210](holograms-210.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-211-Gesture.zip) requis par le projet. Requiert Unity 2017,2 ou une version ultérieure.
* Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-211-Gesture).

### <a name="errata-and-notes"></a>Errata et notes

* L’option «Activer Uniquement mon code» doit être désactivée (décochée) dans Visual Studio sous Outils-> Options-> le débogage pour atteindre les points d’arrêt dans votre code.

## <a name="chapter-0---unity-setup"></a>Chapitre 0-Configuration Unity

### <a name="instructions"></a>Instructions

1. Démarrez Unity.
2. Sélectionnez **ouvrir**.
3. Accédez au dossier de **mouvements** que vous avez préalablement désinstallé.
4. Recherchez et sélectionnez le dossier de **démarrage**/de l'**Explorateur de modèles** .
5. Cliquez sur le bouton **Sélectionner un dossier** .
6. Dans le panneau **projet** , développez le dossier **scenes** .
7. Double-cliquez sur **ModelExplorer** Scene pour le charger dans Unity.

### <a name="building"></a>Génération

1. Dans Unity, sélectionnez **fichier > paramètres de build**.
2. Si **scenes/ModelExplorer** n’est pas listé dans **scenes dans Build**, cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.
3. Si vous développez spécifiquement pour HoloLens, définissez **appareil cible** sur **hololens**. Dans le cas contraire, laissez-le sur **un appareil**.
4. Vérifiez que le **type de build** est défini sur **D3D** et que le **Kit de développement logiciel (SDK** ) est défini sur le **dernier installé** (qui doit être le SDK 16299 ou une version ultérieure).
5. Cliquez sur **Build**.
6. Créez un **dossier** nommé «App».
7. Cliquez sur le dossier de l' **application** .
8. Appuyez sur **Sélectionner un dossier** et Unity va commencer à générer le projet pour Visual Studio.

Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.

1. Ouvrez le dossier de l' **application** .
2. Ouvrez la **solution Visual Studio ModelExplorer**.

En cas de déploiement dans HoloLens:

1. À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.
2. Cliquez sur la flèche déroulante en regard du bouton ordinateur local, puis sélectionnez **ordinateur distant**.
3. Entrez **l’adresse IP de votre appareil HoloLens** et définissez le mode d’authentification sur **universel (protocole non chiffré)** . Cliquez sur **Sélectionner**. Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées**.
4. Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**. S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le coupler à [Visual Studio](using-visual-studio.md#pairing-your-device-hololens).
5. Une fois l’application déployée, ignorez le **Fitbox** avec un **mouvement Select**.

En cas de déploiement sur un casque immersif:

1. À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.
2. Assurez-vous que la cible de déploiement est définie sur **ordinateur local**.
3. Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
4. Une fois l’application déployée, Faites disparaître le **Fitbox** en tirant le déclencheur sur un contrôleur de mouvement.

>[!NOTE]
>Vous pouvez remarquer des erreurs rouges dans le panneau erreurs de Visual Studio. Vous pouvez les ignorer en toute sécurité. Basculez vers le panneau sortie pour afficher la progression réelle de la génération. Les erreurs dans le panneau sortie vous obligent à faire un correctif (le plus souvent, elles sont provoquées par une erreur dans un script).

## <a name="chapter-1---hand-detected-feedback"></a>Chapitre 1-commentaires sur la main détectés

>[!VIDEO https://www.youtube.com/embed/D1FcIyuFTZQ]

### <a name="objectives"></a>Objectifs

* S’abonner aux événements de suivi de la main.
* Utilisez les commentaires des curseurs pour montrer aux utilisateurs quand une main fait l’objet d’un suivi.

### <a name="instructions"></a>Instructions

* Dans le volet **hiérarchie** , développez l’objet **InputManager** .
* Recherchez et sélectionnez l’objet **GesturesInput** .

Le script **InteractionInputSource.cs** effectue les étapes suivantes:

1. S’abonne aux événements InteractionSourceDetected et InteractionSourceLost.
2. Définit l’État HandDetected.
3. Annule l’abonnement aux événements InteractionSourceDetected et InteractionSourceLost.

Ensuite, nous allons mettre à niveau notre curseur de l' [entrée 210](holograms-210.md) en une qui affiche les commentaires en fonction des actions de l’utilisateur.

1. Dans le volet **hiérarchie** , sélectionnez l’objet **curseur** et supprimez-le.
2. Dans le panneau **projet** , recherchez **CursorWithFeedback** et faites-le glisser dans le panneau **hiérarchie** .
3. Cliquez sur **InputManager** dans le panneau **hiérarchie** , puis faites glisser l’objet **CursorWithFeedback** de la **hiérarchie** vers le champ **curseur** du **SimpleSinglePointerSelector**du InputManager, en bas de l’onglet **Inspecteur**.
4. Cliquez sur **CursorWithFeedback** dans la **hiérarchie**.
5. Dans le volet de l' **inspecteur** , développez **données d’État du curseur** sur le script du curseur de l' **objet** .

Les **données d’État du curseur** fonctionnent de la manière suivante:

* Tout état d' **observation** signifie qu’aucune main n’est détectée et que l’utilisateur recherche simplement.
* Tout état d' **interaction** signifie qu’une main ou un contrôleur est détecté.
* Tout état de **survol** signifie que l’utilisateur Regarde un hologramme.

### <a name="build-and-deploy"></a>Génération et déploiement

* Dans Unity, utilisez les **paramètres de build de > de fichiers** pour régénérer l’application.
* Ouvrez le dossier de l' **application** .
* S’il n’est pas déjà ouvert, ouvrez la **solution Visual Studio ModelExplorer**.
  * (Si vous avez déjà généré/déployé ce projet dans Visual Studio au cours de la configuration, vous pouvez ouvrir cette instance de VS et cliquer sur «recharger tout» lorsque vous y êtes invité).
* Dans Visual Studio, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
* Une fois que l’application a été déployée sur HoloLens, Faites disparaître le fitbox à l’aide du geste d’appui sur l’air.
* Déplacez votre main en vue et pointez votre index vers le ciel pour démarrer le suivi.
* Déplacez votre main à gauche, à droite, en haut et en aval.
* Regardez comment le curseur change lorsque votre main est détectée, puis perdu de la vue.
* Si vous êtes sur un casque immersif, vous devez vous connecter et déconnecter votre contrôleur. Ces commentaires deviennent moins intéressants sur un appareil immersif, car un contrôleur connecté est toujours «disponible».

## <a name="chapter-2---navigation"></a>Chapitre 2-navigation

>[!VIDEO https://www.youtube.com/embed/sm-kxtKksSo]

### <a name="objectives"></a>Objectifs

* Utilisez les événements de mouvement de navigation pour faire pivoter le astronautes.

### <a name="instructions"></a>Instructions

Pour utiliser des mouvements de navigation dans notre application, nous allons modifier **GestureAction.cs** pour faire pivoter les objets lorsque le mouvement de navigation se produit. En outre, nous ajouterons des commentaires au curseur à afficher lorsque la navigation est disponible.

1. Dans le volet **hiérarchie** , développez **CursorWithFeedback**.
2. Dans le  dossier hologrammes, recherchez la ressource **ScrollFeedback** .
3. Glissez-déplacez le Prefab **ScrollFeedback** sur le gameobject **CursorWithFeedback** dans la **hiérarchie**.
4. Cliquez sur **CursorWithFeedback**.
5. Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
6. Dans le menu, tapez dans la zone de recherche **CursorFeedback**. Sélectionnez le résultat de la recherche.
7. Faites glisser et déposez l’objet **ScrollFeedback** à partir de la **hiérarchie** vers la propriété objet de jeu dans le **défilement détectée** dans le composant de **Commentaires de curseur** de l' **inspecteur**.
8. Dans le volet **hiérarchie** , sélectionnez l’objet **AstroMan** .
9. Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
10. Dans le menu, tapez dans l’action de **mouvement**de zone de recherche. Sélectionnez le résultat de la recherche.

Ensuite, ouvrez **GestureAction.cs** dans Visual Studio. Dans l’exercice de codage 2. c, modifiez le script pour effectuer les opérations suivantes:

1. **Faites pivoter l’objet AstroMan** chaque fois qu’un mouvement de navigation est effectué.
2. Calcule le **rotationFactor** pour contrôler la quantité de rotation appliquée à l’objet.
3. **Faire pivoter l’objet** autour de l’axe y lorsque l’utilisateur déplace sa main à gauche ou à droite.

Effectuez les exercices de codage 2. c dans le script ou remplacez le code par la solution terminée ci-dessous:

```cs
using HoloToolkit.Unity.InputModule;
using UnityEngine;

/// <summary>
/// GestureAction performs custom actions based on
/// which gesture is being performed.
/// </summary>
public class GestureAction : MonoBehaviour, INavigationHandler, IManipulationHandler, ISpeechHandler
{
    [Tooltip("Rotation max speed controls amount of rotation.")]
    [SerializeField]
    private float RotationSensitivity = 10.0f;

    private bool isNavigationEnabled = true;
    public bool IsNavigationEnabled
    {
        get { return isNavigationEnabled; }
        set { isNavigationEnabled = value; }
    }

    private Vector3 manipulationOriginalPosition = Vector3.zero;

    void INavigationHandler.OnNavigationStarted(NavigationEventData eventData)
    {
        InputManager.Instance.PushModalInputHandler(gameObject);
    }

    void INavigationHandler.OnNavigationUpdated(NavigationEventData eventData)
    {
        if (isNavigationEnabled)
        {
            /* TODO: DEVELOPER CODING EXERCISE 2.c */

            // 2.c: Calculate a float rotationFactor based on eventData's NormalizedOffset.x multiplied by RotationSensitivity.
            // This will help control the amount of rotation.
            float rotationFactor = eventData.NormalizedOffset.x * RotationSensitivity;

            // 2.c: transform.Rotate around the Y axis using rotationFactor.
            transform.Rotate(new Vector3(0, -1 * rotationFactor, 0));
        }
    }

    void INavigationHandler.OnNavigationCompleted(NavigationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void INavigationHandler.OnNavigationCanceled(NavigationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void IManipulationHandler.OnManipulationStarted(ManipulationEventData eventData)
    {
        if (!isNavigationEnabled)
        {
            InputManager.Instance.PushModalInputHandler(gameObject);

            manipulationOriginalPosition = transform.position;
        }
    }

    void IManipulationHandler.OnManipulationUpdated(ManipulationEventData eventData)
    {
        if (!isNavigationEnabled)
        {
            /* TODO: DEVELOPER CODING EXERCISE 4.a */

            // 4.a: Make this transform's position be the manipulationOriginalPosition + eventData.CumulativeDelta
        }
    }

    void IManipulationHandler.OnManipulationCompleted(ManipulationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void IManipulationHandler.OnManipulationCanceled(ManipulationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void ISpeechHandler.OnSpeechKeywordRecognized(SpeechEventData eventData)
    {
        if (eventData.RecognizedText.Equals("Move Astronaut"))
        {
            isNavigationEnabled = false;
        }
        else if (eventData.RecognizedText.Equals("Rotate Astronaut"))
        {
            isNavigationEnabled = true;
        }
        else
        {
            return;
        }

        eventData.Use();
    }
}
```

Vous remarquerez que les autres événements de navigation sont déjà renseignés avec des informations. Nous envoyons les GameObject dans la pile modale InputSystem’s de la boîte à outils, de sorte que l’utilisateur n’a pas à maintenir le focus sur le astronautes une fois la rotation commencée. En conséquence, nous dépilerons le GameObject de la pile une fois le mouvement terminé.

### <a name="build-and-deploy"></a>Génération et déploiement

1. Régénérez l’application dans Unity, puis générez et déployez à partir de Visual Studio pour l’exécuter dans HoloLens.
2. Pointez le curseur sur le astronautes, deux flèches doivent apparaître sur l’un ou l’autre côté du curseur. Ce nouvel visuel indique que le astronautes peut être pivoté.
3. Placez votre main à la position prête (index Finger pointant vers le ciel) pour que le HoloLens commence à suivre votre main.
4. Pour faire pivoter le astronautes, abaissez votre index à la position de pincement, puis déplacez votre main vers la gauche ou vers la droite pour déclencher le mouvement NavigationX.

## <a name="chapter-3---hand-guidance"></a>Chapitre 3-Guide de la main

>[!VIDEO https://www.youtube.com/embed/ULzlVw4e14I]

### <a name="objectives"></a>Objectifs

* Utilisez le score de l’aide à la **main** pour prédire quand le suivi de la main sera perdu.
* Fournissez **des commentaires sur le curseur** pour montrer quand l’utilisateur est près du bord de la vue de l’appareil photo.

### <a name="instructions"></a>Instructions

1. Dans le volet **hiérarchie** , sélectionnez l’objet **CursorWithFeedback** .
2. Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
3. Dans le menu, tapez dans la zone de recherche Guide de la **main**. Sélectionnez le résultat de la recherche.
4. Dans le dossier **hologrammes** du panneau **projet** , recherchez la ressource **HandGuidanceFeedback** .
5. Faites glisser et déposez la ressource **HandGuidanceFeedback** sur la propriété de l' **indicateur de guide main** dans le panneau **inspecteur** .

### <a name="build-and-deploy"></a>Génération et déploiement

* Régénérez l’application dans Unity, puis générez et déployez à partir de Visual Studio pour expérimenter l’application sur HoloLens.
* Affichez votre main et augmentez votre doigt d’index pour obtenir le suivi.
* Commencez à faire pivoter le astronautes avec le mouvement de navigation (pincez le doigt et le curseur de l’index).
* Déplacez votre main à gauche, à droite, en haut et en baisse.
* À mesure que votre main approche du bord du cadre de mouvement, une flèche doit apparaître en regard du curseur pour vous avertir que le suivi des mains sera perdu. La flèche indique la direction dans laquelle déplacer votre main afin d’empêcher la perte du suivi.

## <a name="chapter-4---manipulation"></a>Chapitre 4-manipulation

>[!VIDEO https://www.youtube.com/embed/f3m8MvU60-I]

### <a name="objectives"></a>Objectifs

* Utilisez des événements de manipulation pour déplacer le astronautes avec vos mains.
* Fournissez des commentaires sur le curseur pour permettre à l’utilisateur de savoir quand la manipulation peut être utilisée.

### <a name="instructions"></a>Instructions

GestureManager.cs et AstronautManager.cs nous permettront d’effectuer les opérations suivantes:

1. Utilisez le mot clé Speech «**Move astronautes**» pour activer les gestes de **manipulation** et «**Rotate astronautes**» pour les désactiver.
2. Passez à la réponse à la **reconnaissance de mouvement de manipulation**.

Commençons.

1. Dans le volet **hiérarchie** , créez un gameobject vide. Nommez-le «**AstronautManager**».
2. Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
3. Dans le menu, tapez dans la zone de recherche **astronautes Manager**. Sélectionnez le résultat de la recherche.
4. Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
5. Dans le menu, tapez la **source d’entrée vocale**de la zone de recherche. Sélectionnez le résultat de la recherche.

Nous allons maintenant ajouter les commandes vocales requises pour contrôler l’état d’interaction du astronautes.

1. Développez la section **Mots clés** dans l' **inspecteur**.
2. Cliquez sur **+** le côté droit pour ajouter un nouveau mot clé.
3. Tapez le mot clé en tant que **Move astronautes**. N’hésitez pas à ajouter un raccourci clavier si vous le souhaitez.
4. Cliquez sur **+** le côté droit pour ajouter un nouveau mot clé.
5. Tapez le mot clé **Rotate astronautes**. N’hésitez pas à ajouter un raccourci clavier si vous le souhaitez.
6. Le code du gestionnaire correspondant se trouve dans **GestureAction.cs**, dans le gestionnaire **ISpeechHandler. OnSpeechKeywordRecognized** .

![Comment configurer la source d’entrée vocale pour le chapitre 4](images/holograms211-speech.png)

Ensuite, nous allons configurer les commentaires de manipulation sur le curseur.

1. Dans le dossier **hologrammes** du panneau **projet** , recherchez la ressource **PathingFeedback** .
2. Glissez-déplacez le Prefab **PathingFeedback** vers l’objet **CursorWithFeedback** dans la **hiérarchie**.
3. Dans le volet **hiérarchie** , cliquez sur **CursorWithFeedback**.
4. Faites glisser et déposez l’objet **PathingFeedback** à partir de la **hiérarchie** vers la propriété **d’objet de jeu Pathing détectée** dans le composant de **retour de curseur** de l' **inspecteur**.

À présent, nous devons ajouter du code à **GestureAction.cs** pour activer les éléments suivants:

1. Ajoutez du code à la fonction **IManipulationHandler. OnManipulationUpdated** , qui déplacera le astronautes lorsqu’un mouvement de **manipulation** sera détecté.
2. Calculez le **vecteur de déplacement** pour déterminer où le astronautes doit être déplacé en fonction de la position de la main.
3. **Déplacez** le astronautes vers la nouvelle position.

Effectuez le codage de l’exercice 4. a dans **GestureAction.cs**ou utilisez notre solution complète ci-dessous:

```cs
using HoloToolkit.Unity.InputModule;
using UnityEngine;

/// <summary>
/// GestureAction performs custom actions based on
/// which gesture is being performed.
/// </summary>
public class GestureAction : MonoBehaviour, INavigationHandler, IManipulationHandler, ISpeechHandler
{
    [Tooltip("Rotation max speed controls amount of rotation.")]
    [SerializeField]
    private float RotationSensitivity = 10.0f;

    private bool isNavigationEnabled = true;
    public bool IsNavigationEnabled
    {
        get { return isNavigationEnabled; }
        set { isNavigationEnabled = value; }
    }

    private Vector3 manipulationOriginalPosition = Vector3.zero;

    void INavigationHandler.OnNavigationStarted(NavigationEventData eventData)
    {
        InputManager.Instance.PushModalInputHandler(gameObject);
    }

    void INavigationHandler.OnNavigationUpdated(NavigationEventData eventData)
    {
        if (isNavigationEnabled)
        {
            /* TODO: DEVELOPER CODING EXERCISE 2.c */

            // 2.c: Calculate a float rotationFactor based on eventData's NormalizedOffset.x multiplied by RotationSensitivity.
            // This will help control the amount of rotation.
            float rotationFactor = eventData.NormalizedOffset.x * RotationSensitivity;

            // 2.c: transform.Rotate around the Y axis using rotationFactor.
            transform.Rotate(new Vector3(0, -1 * rotationFactor, 0));
        }
    }

    void INavigationHandler.OnNavigationCompleted(NavigationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void INavigationHandler.OnNavigationCanceled(NavigationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void IManipulationHandler.OnManipulationStarted(ManipulationEventData eventData)
    {
        if (!isNavigationEnabled)
        {
            InputManager.Instance.PushModalInputHandler(gameObject);

            manipulationOriginalPosition = transform.position;
        }
    }

    void IManipulationHandler.OnManipulationUpdated(ManipulationEventData eventData)
    {
        if (!isNavigationEnabled)
        {
            /* TODO: DEVELOPER CODING EXERCISE 4.a */

            // 4.a: Make this transform's position be the manipulationOriginalPosition + eventData.CumulativeDelta
            transform.position = manipulationOriginalPosition + eventData.CumulativeDelta;
        }
    }

    void IManipulationHandler.OnManipulationCompleted(ManipulationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void IManipulationHandler.OnManipulationCanceled(ManipulationEventData eventData)
    {
        InputManager.Instance.PopModalInputHandler();
    }

    void ISpeechHandler.OnSpeechKeywordRecognized(SpeechEventData eventData)
    {
        if (eventData.RecognizedText.Equals("Move Astronaut"))
        {
            isNavigationEnabled = false;
        }
        else if (eventData.RecognizedText.Equals("Rotate Astronaut"))
        {
            isNavigationEnabled = true;
        }
        else
        {
            return;
        }

        eventData.Use();
    }
}
```

### <a name="build-and-deploy"></a>Génération et déploiement

* Régénérez dans Unity, puis générez et déployez à partir de Visual Studio pour exécuter l’application dans HoloLens.
* Déplacez votre main devant le HoloLens et augmentez le doigt de votre index afin qu’il puisse être suivi.
* Focus sur le curseur sur le astronautes.
* Dites «Move astronautes» pour déplacer le astronautes avec un mouvement de manipulation.
* Quatre flèches doivent apparaître autour du curseur pour indiquer que le programme va maintenant répondre aux événements de manipulation.
* Abaissez votre index au niveau de votre curseur et empêchez-vous de le pincer.
* À mesure que vous déplacez votre main, le astronautes se déplace également (manipulation).
* Augmentez le doigt de votre index pour arrêter la manipulation du astronautes.
* Remarque : Si vous n’indiquez pas «Move astronautes» avant de déplacer votre main, le mouvement de navigation sera utilisé à la place.
* Dites «Rotate astronautes» pour revenir à l’État rotatif.

## <a name="chapter-5---model-expansion"></a>Chapitre 5-développement d’un modèle

>[!VIDEO https://www.youtube.com/embed/dA11P4P0VO8]

### <a name="objectives"></a>Objectifs

* Développez le modèle astronautes en plusieurs éléments plus petits avec lesquels l’utilisateur peut interagir.
* Déplacez chaque élément individuellement à l’aide de mouvements de navigation et de manipulation.

### <a name="instructions"></a>Instructions

Dans cette section, nous allons effectuer les tâches suivantes:

1. Ajoutez un nouveau mot clé «**expand Model**» pour développer le modèle astronautes.
2. Ajoutez un nouveau mot clé «**Reset Model**» pour ramener le modèle à son formulaire d’origine.

Pour ce faire, nous allons ajouter deux mots clés supplémentaires à la source d’entrée vocale du chapitre précédent. Nous présenterons également une autre façon de gérer les événements de reconnaissance.

1. Cliquez sur **AstronautManager** dans l' **inspecteur** et développez la section **Mots clés** dans l' **inspecteur**.
2. Cliquez sur **+** le côté droit pour ajouter un nouveau mot clé.
3. Tapez le mot clé **expand Model**. N’hésitez pas à ajouter un raccourci clavier si vous le souhaitez.
4. Cliquez sur **+** le côté droit pour ajouter un nouveau mot clé.
5. Tapez le mot clé en tant que **modèle**de réinitialisation. N’hésitez pas à ajouter un raccourci clavier si vous le souhaitez.
6. Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
7. Dans le menu, tapez dans le **Gestionnaire d’entrée**de la zone de recherche. Sélectionnez le résultat de la recherche.
8. Check **est l’écouteur global**, puisque nous voulons que ces commandes fonctionnent, quel que soit le gameobject que nous allons concentrer.
9. Cliquez sur **+** le bouton et sélectionnez **développer le modèle** dans la liste déroulante mot clé.
10. Cliquez sur **+** le sous réponse, puis faites glisser le **AstronautManager** de la **hiérarchie** vers le champ **aucun (objet)** .
11. Maintenant, cliquez sur la liste déroulante **no Function** , sélectionnez **AstronautManager**, puis **ExpandModelCommand**.
12. Cliquez sur le bouton du **+** gestionnaire d’entrée vocale et sélectionnez Réinitialiser le **modèle** dans la liste déroulante mot clé.
13. Cliquez sur **+** le sous réponse, puis faites glisser le **AstronautManager** de la **hiérarchie** vers le champ **aucun (objet)** .
14. Maintenant, cliquez sur la liste déroulante **no Function** , sélectionnez **AstronautManager**, puis **ResetModelCommand**.

![Comment configurer la source et le gestionnaire de l’entrée vocale pour le chapitre 5](images/holograms211-speechhandler.png)

### <a name="build-and-deploy"></a>Génération et déploiement

* Essayez ! Générez et déployez l’application sur HoloLens.
* Par exemple, **développez modèle** pour voir le modèle astronautes développé.
* Utilisez la **navigation** pour faire pivoter des éléments individuels de la couleur astronautes.
* Par exemple, vous pouvez **déplacer astronautes** , puis utiliser la **manipulation** pour déplacer des éléments individuels de la couleur astronautes.
* Par exemple, **faites pivoter astronautes** pour faire pivoter les éclats.
* Par exemple, réinitialisez le **modèle** pour retourner le astronautes sous sa forme d’origine.

## <a name="the-end"></a>La fin

Félicitations ! Vous avez maintenant terminé **l’entrée 211: Mouvement**.

* Vous savez comment détecter et répondre aux événements de suivi de la main, de navigation et de manipulation.
* Vous comprenez la différence entre les gestes de navigation et de manipulation.
* Vous savez comment modifier le curseur pour fournir des commentaires visuels quand une main est détectée, quand une main est sur le point d’être perdue et quand un objet prend en charge différentes interactions (navigation et manipulation).
