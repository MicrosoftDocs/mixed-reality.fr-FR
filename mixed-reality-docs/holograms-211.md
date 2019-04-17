---
title: Entrée M. 211 - mouvement
description: Suivez cette procédure pas à pas codage à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des concepts de mouvement.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, tutorial, gesture
ms.openlocfilehash: 76d2b4c0ac3d0a3783b091f7dc8c39548a18b548
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596148"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

# <a name="mr-input-211-gesture"></a>Entrée M. 211 : Mouvement

[Mouvements](gestures.md) transformer d’intention de l’utilisateur en action. Les gestes, les utilisateurs peuvent interagir avec hologrammes. Dans ce cours, nous allons apprendre à effectuer le suivi des mains de l’utilisateur, répondre aux entrées d’utilisateur, et envoyez vos commentaires à l’utilisateur quant à état et l’emplacement.

>[!VIDEO https://www.youtube.com/embed/c9zlpfFeEtc]

Dans [101 des principes fondamentaux de M.](holograms-101.md), nous avons utilisé un mouvement d’appui simple d’interagir avec notre hologrammes. Maintenant, nous le mouvement d’appui en l’air au-delà des concepts et explorez les nouveaux concepts à :

* Détecter lorsque le suivi de main de l’utilisateur et fournir des commentaires à l’utilisateur.
* Utilisez un mouvement de navigation pour faire pivoter notre hologrammes.
* Fournir des commentaires lors de la part de l’utilisateur est sur le point de sortir de la vue.
* Utilisez les événements de manipulation pour permettre aux utilisateurs de déplacer hologrammes avec leurs mains.

Dans ce cours, nous y reviendrons le projet Unity **l’Explorateur de modèles**, que nous avons construit dans [210 d’entrée M.](holograms-210.md). Notre ami astronautes est à nous assister dans notre exploration de ces nouveaux concepts de mouvement.

>[!IMPORTANT]
>Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrés à l’aide d’une version antérieure de Unity et le Kit de ressources de réalité mixte. Tandis que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des éléments visuels dans les vidéos correspondantes qui sont obsolètes. Les vidéos restent inclus éternellement et car couvert les concepts s’appliquent toujours.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>Entrée M. 211 : Mouvement</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).
* Base C# possibilité de programmation.
* Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).
* Vous devez avoir terminé [210 d’entrée M.](holograms-210.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-211-Gesture.zip) requise par le projet. Nécessite Unity 2017.2 ou version ultérieure.
* Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.

>[!NOTE]
>Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-211-Gesture).

### <a name="errata-and-notes"></a>Errata et remarques

* « Activer uniquement mon Code » doit être désactivé (*unchecked*) dans Visual Studio sous Outils -> Options -> débogage afin d’atteindre des points d’arrêt dans votre code.

## <a name="chapter-0---unity-setup"></a>Chapitre 0 - le programme d’installation Unity

### <a name="instructions"></a>Instructions

1. Démarrez Unity.
2. Sélectionnez **Open**.
3. Accédez à la **mouvement** dossier vous précédemment non archivés.
4. Recherchez et sélectionnez le **démarrage**/**l’Explorateur de modèles** dossier.
5. Cliquez sur le **sélectionner le dossier** bouton.
6. Dans le **projet** volet, développez le **scènes** dossier.
7. Double-cliquez sur **ModelExplorer** scène à le charger dans Unity.

### <a name="building"></a>Génération

1. Dans Unity, sélectionnez **fichier > Paramètres de Build**.
2. Si **arrière-plan/ModelExplorer** n’est pas répertorié dans **scènes dans Build**, cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.
3. Si vous développez en particulier pour HoloLens, définissez **appareil cible** à **HoloLens**. Dans le cas contraire, laissez-le sur **n’importe quel appareil**.
4. Vérifiez **Type Build** a la valeur **D3D** et **SDK** a la valeur **dernière installé** (qui doit être SDK 16299 ou une version ultérieure).
5. Cliquez sur **Build**.
6. Créer un **nouveau dossier** nommé « Application ».
7. Clic le **application** dossier.
8. Appuyez sur **sélectionner le dossier** et Unity commence à générer le projet pour Visual Studio.

Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.

1. Ouvrez le **application** dossier.
2. Ouvrez le **ModelExplorer Visual Studio Solution**.

Si le déploiement sur HoloLens :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x86**.
2. Cliquez sur la flèche déroulante en regard du bouton de l’ordinateur Local, puis sélectionnez **Machine distante**.
3. Entrez **votre adresse IP du périphérique HoloLens** et définir le Mode d’authentification **universel (protocole non chiffré)**. Cliquez sur **Sélectionner**. Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées**.
4. Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**. S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device-hololens).
5. Lorsque l’application a été déployée, faire disparaître le **Fitbox** avec un **sélectionnez mouvement**.

Si le déploiement sur un casque immersif :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x64**.
2. Assurez-vous que la cible de déploiement est définie sur **ordinateur Local**.
3. Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.
4. Lorsque l’application a été déployée, faire disparaître le **Fitbox** en extrayant le déclencheur sur un contrôleur de mouvement.

>[!NOTE]
>Vous remarquerez peut-être des erreurs rouge dans le panneau erreurs de Visual Studio. Il est possible de les ignorer. Basculer vers le volet de sortie pour afficher les réelle progression de la build. Erreurs dans le volet de sortie vous obligera à effectuer un correctif (la plus souvent qu’ils sont provoquées par une erreur dans un script).

## <a name="chapter-1---hand-detected-feedback"></a>Chapitre 1 - main a détecté des commentaires

>[!VIDEO https://www.youtube.com/embed/D1FcIyuFTZQ]

### <a name="objectives"></a>Objectifs

* S’abonner pour transmettre des événements de suivi.
* Utilisez le curseur pour afficher les utilisateurs lors de la main est suivie.

### <a name="instructions"></a>Instructions

* Dans le **hiérarchie** volet, développez le **InputManager** objet.
* Recherchez et sélectionnez le **GesturesInput** objet.

Le **InteractionInputSource.cs** script effectue ces étapes :

1. S’abonne aux événements InteractionSourceDetected et InteractionSourceLost.
2. Définit l’état HandDetected.
3. Annule l’abonnement à partir des événements InteractionSourceDetected et InteractionSourceLost.

Ensuite, nous allons mettre à niveau notre curseur à partir [210 d’entrée M.](holograms-210.md) en une seule qui affiche des commentaires en fonction des actions de l’utilisateur.

1. Dans le **hiérarchie** Panneau de configuration, sélectionnez le **curseur** de l’objet et supprimez-le.
2. Dans le **projet** du panneau, recherchez **CursorWithFeedback** et faites-le glisser vers le **hiérarchie** Panneau de configuration.
3. Cliquez sur **InputManager** dans le **hiérarchie** panneau, puis faites glisser le **CursorWithFeedback** de l’objet à partir de la **hiérarchie** dans le De InputManager **SimpleSinglePointerSelector**de **curseur** champ, en bas de la **inspecteur**.
4. Cliquez sur le **CursorWithFeedback** dans le **hiérarchie**.
5. Dans le **inspecteur** volet, développez **données d’état de curseur** sur le **objet curseur** script.

Le **données d’état de curseur** fonctionne comme suit :

* N’importe quel **observer** état signifie qu’aucun main n’est détecté et que l’utilisateur est simplement chercher.
* N’importe quel **Interact** état signifie qu’une main ou le contrôleur a été détecté.
* N’importe quel **pointez** état signifie que l’utilisateur consulte un hologramme.

### <a name="build-and-deploy"></a>Générer et déployer

* Dans Unity, utilisez **fichier > Paramètres de Build** pour régénérer l’application.
* Ouvrez le **application** dossier.
* Si elle n’est pas déjà ouverte, ouvrez le **ModelExplorer Visual Studio Solution**.
  * (Si vous avez déjà créé/déployé ce projet dans Visual Studio pendant l’installation, puis vous pouvez ouvrir qu’une instance de Visual Studio et cliquez sur « Recharger All » lorsque vous y êtes invité).
* Dans Visual Studio, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.
* Une fois que l’application se déploie sur le HoloLens, faire disparaître le fitbox à l’aide du mouvement d’appui en l’air.
* Déplacer votre main dans la vue et pointer votre doigt de l’index vers le ciel pour démarrer manuellement le suivi des.
* Déplacer votre main gauche, droite, haut et bas.
* Regardez comment quand le curseur prend la main est détectée et puis perdue à partir de la vue.
* Si vous êtes sur un casque immersif, vous devrez vous connecter et déconnecter votre contrôleur. Ces commentaires devient moins intéressants sur un appareil immersif, comme un contrôleur connecté sera toujours « disponible ».

## <a name="chapter-2---navigation"></a>Chapitre 2 - Navigation

>[!VIDEO https://www.youtube.com/embed/sm-kxtKksSo]

### <a name="objectives"></a>Objectifs

* Utilisez les événements de mouvement de Navigation pour faire pivoter l’astronautes !.

### <a name="instructions"></a>Instructions

Pour utiliser des gestes de Navigation dans notre application, nous allons modifier **GestureAction.cs** faire pivoter des objets quand le mouvement de Navigation se produit. En outre, nous allons ajouter des commentaires pour le curseur à afficher lorsque la Navigation est disponible.

1. Dans le **hiérarchie** volet, développez **CursorWithFeedback**.
2. Dans le **hologrammes** dossier, recherchez le **ScrollFeedback** actif.
3. Faites glisser et déposez le **ScrollFeedback** prefab sur le **CursorWithFeedback** GameObject dans le **hiérarchie**.
4. Cliquez sur **CursorWithFeedback**.
5. Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.
6. Dans le menu, tapez dans la zone de recherche **CursorFeedback**. Sélectionnez le résultat de recherche.
7. Faites glisser et déposez le **ScrollFeedback** à partir de l’objet le **hiérarchie** sur le **défilement détecté Game Object** propriété dans le **commentaire du curseur**composant dans le **inspecteur**.
8. Dans le **hiérarchie** Panneau de configuration, sélectionnez le **AstroMan** objet.
9. Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.
10. Dans le menu, tapez dans la zone de recherche **mouvement Action**. Sélectionnez le résultat de recherche.

Ensuite, ouvrez **GestureAction.cs** dans Visual Studio. De codage dans l’exercice 2.c, modifiez le script pour effectuer les opérations suivantes :

1. **Faire pivoter le AstroMan** objet chaque fois qu’un mouvement de Navigation est effectué.
2. Calculer le **rotationFactor** pour contrôler la quantité de rotation appliquée à l’objet.
3. **Faire pivoter l’objet** autour de l’axe des ordonnées lorsque l’utilisateur déplace la main gauche ou droite.

Codage complète exerce 2.c du script, ou remplacez le code par la solution terminée ci-dessous :

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

Vous remarquerez que les autres événements de navigation sont déjà renseignés avec des informations. Nous envoyons le GameObject sur le Kit de ressources pile modale de InputSystem, afin de l’utilisateur n’a pas à conserver le focus sur l’astronautes une fois la rotation a commencé. En conséquence, nous pop le GameObject la pile une fois que le geste est terminé.

### <a name="build-and-deploy"></a>Générer et déployer

1. Régénérez l’application dans Unity puis créer et déployer à partir de Visual Studio pour l’exécuter dans le HoloLens.
2. Fixez du regard l’astronaut, deux flèches doivent apparaître sur chaque côté du curseur. Ce nouvel élément visuel indique que l’astronautes peut être pivoté.
3. Placez votre main dans la position de prête (votre index pointé vers le ciel) pour que la HoloLens puisse démarrer le suivi de votre main.
4. Pour faire pivoter l’astronaut, réduire votre doigt de l’index à une position de pincement et puis déplacez la main gauche ou droite pour déclencher le mouvement NavigationX.

## <a name="chapter-3---hand-guidance"></a>Chapitre 3 - conseils de main

>[!VIDEO https://www.youtube.com/embed/ULzlVw4e14I]

### <a name="objectives"></a>Objectifs

* Utilisez **remettez le score de conseils** pour aider à prédire lorsque main suivi seront perdue.
* Fournir **des commentaires sur le curseur** à afficher lorsque l’approche de bord de la caméra de vue main de l’utilisateur.

### <a name="instructions"></a>Instructions

1. Dans le **hiérarchie** Panneau de configuration, sélectionnez le **CursorWithFeedback** objet.
2. Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.
3. Dans le menu, tapez dans la zone de recherche **main conseils**. Sélectionnez le résultat de recherche.
4. Dans le **projet** panneau **hologrammes** dossier, recherchez le **HandGuidanceFeedback** asset.
5. Faites glisser et déposez le **HandGuidanceFeedback** actif sur le **main conseils indicateur** propriété dans le **inspecteur** panneau.

### <a name="build-and-deploy"></a>Générer et déployer

* Régénérez l’application dans Unity puis créer et déployer à partir de Visual Studio pour profiter de l’application sur HoloLens.
* Afficher votre main dans la vue et déclencher votre doigt de l’index pour obtenir l’objet d’un suivi.
* Démarrer la rotation du astronautes avec le mouvement de Navigation (pincement votre doigt de l’index et ensemble de curseur de défilement).
* Déplacer votre main gauche, droite, haut et bas.
* Lorsque votre main arrive à une flèche doit apparaître à côté du bord de l’image de mouvement, le curseur pour vous avertir que disponible de suivi seront perdu. La flèche indique la direction pour déplacer votre main afin d’éviter de suivi à partir de la perte.

## <a name="chapter-4---manipulation"></a>Chapitre 4 - Manipulation

>[!VIDEO https://www.youtube.com/embed/f3m8MvU60-I]

### <a name="objectives"></a>Objectifs

* Utiliser des événements de Manipulation pour déplacer l’astronaut avec vos mains.
* Fournir des commentaires sur le curseur pour informer l’utilisateur lors de la Manipulation peut être utilisée.

### <a name="instructions"></a>Instructions

GestureManager.cs et AstronautManager.cs nous permettra d’effectuer les opérations suivantes :

1. Utilisez le mot clé vocale »**Astronaut déplacer**» pour activer **Manipulation** mouvements et «**Astronaut faire pivoter**» pour les désactiver.
2. Basculez vers la réponse à la **reconnaissance de mouvement de Manipulation**.

Commençons.

1. Dans le **hiérarchie** panel, créer un nouveau GameObject vide. Nommez-le «**AstronautManager**».
2. Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.
3. Dans le menu, tapez dans la zone de recherche **Astronaut Manager**. Sélectionnez le résultat de recherche.
4. Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.
5. Dans le menu, tapez dans la zone de recherche **Source d’entrée vocale**. Sélectionnez le résultat de recherche.

Nous allons maintenant ajouter les commandes vocales nécessaires pour contrôler l’état de l’interaction de l’astronaut.

1. Développez le **mots clés** section dans le **inspecteur**.
2. Cliquez sur le **+** sur le côté droit pour ajouter un nouveau mot clé.
3. Tapez le mot clé en tant que **déplacer astronautes**. N’hésitez pas à ajouter un raccourci de la clé si vous le souhaitez.
4. Cliquez sur le **+** sur le côté droit pour ajouter un nouveau mot clé.
5. Tapez le mot clé en tant que **pivoter astronautes**. N’hésitez pas à ajouter un raccourci de la clé si vous le souhaitez.
6. Vous trouverez le code de gestionnaire correspondant dans **GestureAction.cs**, dans le **ISpeechHandler.OnSpeechKeywordRecognized** gestionnaire.

![Comment configurer la Source d’entrée vocale pour chapitre 4](images/holograms211-speech.png)

Ensuite, nous allons configurer les commentaires de manipulation sur le curseur.

1. Dans le **projet** panneau **hologrammes** dossier, recherchez le **PathingFeedback** asset.
2. Faites glisser et déposez le **PathingFeedback** prefab sur le **CursorWithFeedback** de l’objet dans le **hiérarchie**.
3. Dans le **hiérarchie** du panneau, cliquez sur **CursorWithFeedback**.
4. Faites glisser et déposez le **PathingFeedback** à partir de l’objet le **hiérarchie** sur le **chemins détecté Game Object** propriété dans le **commentaire du curseur**composant dans le **inspecteur**.

Nous devons à présent ajouter de code **GestureAction.cs** pour activer les éléments suivants :

1. Ajouter du code pour le **IManipulationHandler.OnManipulationUpdated** (fonction), qui déplacera l’astronautes lorsqu’un **Manipulation** mouvement est détecté.
2. Calculer le **vecteur de mouvement** pour déterminer où l’astronautes doit être déplacé vers position de base disponible.
3. **Déplacer** l’astronautes vers la nouvelle position.

Codage complète exercice 4.a dans **GestureAction.cs**, ou utiliser notre solution terminée ci-dessous :

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

### <a name="build-and-deploy"></a>Générer et déployer

* Reconstruire dans Unity puis créer et déployer à partir de Visual Studio pour exécuter l’application dans HoloLens.
* Déplacer votre main devant le HoloLens et déclencher votre doigt de l’index afin qu’il peut être suivi.
* Concentrer le curseur sur l’astronautes !.
* Par exemple « Déplacer Astronaut » pour déplacer l’astronaut avec un mouvement de Manipulation.
* Quatre flèches doivent apparaître autour du curseur pour indiquer que le programme maintenant répondront aux événements de Manipulation.
* Réduire votre doigt index jusqu'à votre curseur et de les pincés ensemble.
* Lorsque vous déplacez votre main sur, l’astronaut déplacera trop (il s’agit de Manipulation).
* Déclencher votre doigt de l’index pour arrêter de manipuler l’astronautes !.
* Remarque: Si vous ne dites pas « Déplacer astronautes ! » avant de passer votre main, le mouvement de Navigation sera utilisé à la place.
* Par exemple « Faire pivoter des Astronaut » pour revenir à l’état rotatif.

## <a name="chapter-5---model-expansion"></a>Chapitre 5 - expansion de modèle

>[!VIDEO https://www.youtube.com/embed/dA11P4P0VO8]

### <a name="objectives"></a>Objectifs

* Développez le modèle astronautes en plusieurs, en plus petits éléments que l’utilisateur peut interagir avec.
* Déplacez chaque élément individuellement à l’aide de la Navigation et Manipulation de mouvements.

### <a name="instructions"></a>Instructions

Dans cette section, nous allez effectuer les tâches suivantes :

1. Ajouter un nouveau mot clé «**modèle développez**» pour développer le modèle astronautes !.
2. Ajouter un nouveau mot clé «**modèle réinitialiser**» pour renvoyer le modèle dans sa forme d’origine.

Pour ce faire, nous allons ajouter deux autres mots clés à la Source d’entrée vocale dans le chapitre précédent. Nous illustrerons également une autre façon de gérer les événements de reconnaissance.

1. Cliquez sur précédent dans **AstronautManager** dans le **inspecteur** et développez le **mots clés** section dans le **inspecteur**.
2. Cliquez sur le **+** sur le côté droit pour ajouter un nouveau mot clé.
3. Tapez le mot clé en tant que **développez modèle**. N’hésitez pas à ajouter un raccourci de la clé si vous le souhaitez.
4. Cliquez sur le **+** sur le côté droit pour ajouter un nouveau mot clé.
5. Tapez le mot clé en tant que **réinitialiser modèle**. N’hésitez pas à ajouter un raccourci de la clé si vous le souhaitez.
6. Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.
7. Dans le menu, tapez dans la zone de recherche **Gestionnaire d’entrée vocale**. Sélectionnez le résultat de recherche.
8. Vérifiez **est un écouteur Global**, étant donné que nous voulons que ces commandes fonctionnent, quel que soit le GameObject, nous allons aborder.
9. Cliquez sur le **+** bouton et sélectionnez **développez un modèle** dans la liste déroulante de mot clé.
10. Cliquez sur le **+** sous réponse, puis faites glisser le **AstronautManager** à partir de la **hiérarchie** dans le **None (objet)** champ.
11. Maintenant, cliquez sur le **aucune fonction** liste déroulante, sélectionnez **AstronautManager**, puis **ExpandModelCommand**.
12. Cliquez sur le Gestionnaire d’entrée vocale **+** bouton et sélectionnez **modèle réinitialiser** dans la liste déroulante de mot clé.
13. Cliquez sur le **+** sous réponse, puis faites glisser le **AstronautManager** à partir de la **hiérarchie** dans le **None (objet)** champ.
14. Maintenant, cliquez sur le **aucune fonction** liste déroulante, sélectionnez **AstronautManager**, puis **ResetModelCommand**.

![Comment configurer la Source d’entrée vocale et de gestionnaire pour le chapitre 5](images/holograms211-speechhandler.png)

### <a name="build-and-deploy"></a>Générer et déployer

* Essayez ! Générer et déployer l’application sur le HoloLens.
* Par exemple **modèle développez** pour voir le modèle astronaut développée.
* Utilisez **Navigation** pour faire pivoter des éléments individuels de la couleur astronautes !.
* Par exemple **Astronaut déplacer** , puis utilisez **Manipulation** pour déplacer des éléments individuels de la couleur astronautes !.
* Par exemple **Astronaut pivoter** pour faire pivoter les éléments à nouveau.
* Par exemple **modèle réinitialiser** pour retourner l’astronaut à sa forme d’origine.

## <a name="the-end"></a>La fin

Félicitations ! Vous avez maintenant terminé **211 d’entrée M. : Mouvement**.

* Vous savez comment détecter et répondre pour transmettre les événements de suivi, de navigation et de manipulation.
* Vous comprenez la différence entre les mouvements de Navigation et de Manipulation.
* Vous savez comment modifier le curseur pour fournir des commentaires visuels quand une main est détectée, quand une main est sur le point d’être perdus et lorsqu’un objet prend en charge des interactions (Navigation vs Manipulation).
