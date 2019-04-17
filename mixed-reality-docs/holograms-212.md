---
title: Entrée M. 212 - Voice
description: Suivez cette procédure pas à pas codage à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des concepts de voix.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, tutorial, voice
ms.openlocfilehash: 7e792bf40c47d4e1d57898fbe75ad050a030b7e3
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593795"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-input-212-voice"></a>Entrée M. 212 : Voix

[Entrée voix](voice-input.md) nous donne une autre façon d’interagir avec notre hologrammes. Les commandes vocales fonctionnent de manière très naturelle et facile. Concevez vos commandes vocales afin qu’elles soient :

* Natural
* Facile à retenir
* Contexte approprié
* Suffisamment distinctes à partir d’autres options dans le même contexte

>[!VIDEO https://www.youtube.com/embed/BYpYsVFYjdw]

Dans [101 des principes fondamentaux de M.](holograms-101.md), nous avons utilisé le KeywordRecognizer pour générer les deux commandes vocales simples. Dans 212 d’entrée M., nous allons Approfondissez vos connaissances et découvrez comment :

* Concevoir des commandes vocales qui sont optimisés pour le moteur de reconnaissance vocale HoloLens.
* Informer l’utilisateur du voix des commandes sont disponibles.
* Reconnaissez que nous avons entendu commande vocale de l’utilisateur.
* Comprendre ce qui est l’utilisateur indiquant que, à l’aide d’un module de reconnaissance de dictée.
* Utiliser une grammaire de reconnaissance pour écouter les commandes basées sur un fichier SRGS ou spécification de grammaire de reconnaissance vocale.

Dans ce cours, nous y reviendrons Explorateur de modèles, nous avons créé dans [210 d’entrée M.](holograms-210.md) et [211 d’entrée M.](holograms-211.md).

>[!IMPORTANT]
>Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrés à l’aide d’une version antérieure de Unity et le Kit de ressources de réalité mixte. Tandis que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des éléments visuels dans les vidéos correspondantes qui sont obsolètes. Les vidéos restent inclus éternellement et car couvert les concepts s’appliquent toujours.


## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>Entrée M. 212 : Voix</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).
* Base C# possibilité de programmation.
* Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).
* Vous devez avoir terminé [210 d’entrée M.](holograms-210.md).
* Vous devez avoir terminé [211 d’entrée M.](holograms-211.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-212-Voice.zip) requise par le projet. Nécessite Unity 2017.2 ou version ultérieure.
* Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.

>[!NOTE]
>Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-212-Voice).

### <a name="errata-and-notes"></a>Errata et remarques

* « Activer uniquement mon Code » doit être désactivé (*unchecked*) dans Visual Studio sous Outils -> Options -> débogage afin d’atteindre des points d’arrêt dans votre code.

## <a name="unity-setup"></a>Programme d’installation Unity

### <a name="instructions"></a>Instructions

1. Démarrez Unity.
2. Sélectionnez **Open**.
3. Accédez à la **HolographicAcademy hologrammes 212 vocaux** dossier vous précédemment non archivés.
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

## <a name="chapter-1---awareness"></a>Chapitre 1 - sensibilisation

>[!VIDEO https://www.youtube.com/embed/fDwijJWuEc0]

### <a name="objectives"></a>Objectifs

* Découvrez le **choses à faire et** de conception d’une commande vocale.
* Utilisez **KeywordRecognizer** pour ajouter des regards en fonction des commandes vocales.
* Informer les utilisateurs des commandes vocales à l’aide du curseur **commentaires**.

### <a name="voice-command-design"></a>Conception d’une commande vocale

Dans ce chapitre, vous allez découvrir les commandes vocales de conception. Lorsque vous créez des commandes vocales :

#### <a name="do"></a>DO

* Créer des commandes concis. Vous ne souhaitez pas utiliser *« Lire la vidéo actuellement sélectionnée »*, car cette commande n’est pas concise et serait oubliée par l’utilisateur. Au lieu de cela, vous devez utiliser : *« Lire la vidéo »*, car il est concis et a plusieurs syllabes.
* Utiliser un vocabulaire simple. Toujours essayer d’utiliser des mots et des expressions qui sont faciles à l’utilisateur de découvrir et n’oubliez pas courants. Par exemple, si votre application avait une remarque de l’objet qui peut être affiché ou masqué à partir de la vue, vous ne serez pas utiliser la commande *« Afficher le panneau »*, car le panneau « des » sont un terme rarement utilisé. Au lieu de cela, vous devez utiliser la commande : *« Afficher la Remarque »*, pour afficher la note dans votre application.
* Soyez cohérent. Les commandes vocales doivent être cohérente dans votre application. Imaginez que vous avez deux scènes dans votre application et les deux scènes contiennent un bouton pour fermer l’application. Si la première scène utilisé la commande *« Exit »* pour déclencher le bouton, mais la deuxième scène utilisé la commande *« Fermer l’application »*, puis l’utilisateur va peu trouble. Si les mêmes fonctionnalités sont conservées dans plusieurs scènes, la même commande voix doit être utilisée pour déclencher l’il.

#### <a name="dont"></a>NE PAS

* Utilisez les commandes SYLLABE unique. Par exemple, si vous avez créé une commande vocale pour lire une vidéo, vous évitez d’utiliser la commande simple *« Lecture »*, car elle est uniquement un SYLLABE unique et peut facilement être omis par le système. Au lieu de cela, vous devez utiliser : *« Lire la vidéo »*, car il est concis et a plusieurs syllabes.
* Utilisez les commandes du système. Le *« Select »* commande est réservée par le système à déclencher un événement de clic pour l’objet ayant actuellement le focus. Ne réutilisez pas le *« Select »* commande dans un mot clé ou une expression, comme il peut ne pas fonctionne comme prévu. Par exemple, si la commande de la voix pour la sélection d’un cube dans votre application a été *« Sélectionnez cube »*, mais l’utilisateur a été de consulter une sphère lorsqu’ils prononcés la commande, puis la sphère est sélectionnée à la place. De même, la barre de commandes application est voix activée. N’utilisez pas les commandes suivantes de la reconnaissance vocale dans votre affichage CoreWindow :
    1. Retour
    2. Outil de défilement
    3. Outil zoom
    4. Outil de glisser
    5. Réglage
    6. Supprimer
* Utilisez les sons similaire. Essayez d’éviter d’utiliser les commandes vocales entraîner. Si vous aviez une application d’achat qui pris en charge *« Store afficher »* et *« Afficher plus »* comme vocal de commandes, puis désactivez l’une des commandes alors que l’autre était en cours d’utilisation souhaité. Par exemple, vous pouvez utiliser la *« Afficher Store »* bouton pour ouvrir le magasin et désactivez cette commande lors de l’affichage de la banque afin que le *« Afficher plus »* commande peut être utilisée pour la navigation.

### <a name="instructions"></a>Instructions

* Dans Unity **hiérarchie** du panneau, utilisez l’outil de recherche pour trouver la **holoComm_screen_mesh** objet.
* Double-cliquez sur le **holoComm_screen_mesh** objet pour l’afficher dans le **scène**. Il s’agit d’espion de l’astronaut, qui répond à nos commandes vocales.
* Dans le **inspecteur** panneau, recherchez le **Source d’entrée vocale (Script)** composant.
* Développez le **mots clés** section pour afficher les commandes vocales prises en charge : **Ouvrez Communicator**.
* Cliquez sur la roue dentée à droite, puis sélectionnez **modifier le Script**.
* Explorer **SpeechInputSource.cs** de comprendre comment il utilise le **KeywordRecognizer** pour ajouter des commandes vocales.

### <a name="build-and-deploy"></a>Générer et déployer

* Dans Unity, utilisez **fichier > Paramètres de Build** pour régénérer l’application.
* Ouvrez le **application** dossier.
* Ouvrez le **ModelExplorer Visual Studio Solution**.

(Si vous avez déjà créé/déployé ce projet dans Visual Studio pendant l’installation, puis vous pouvez ouvrir qu’une instance de Visual Studio et cliquez sur « Recharger All » lorsque vous y êtes invité).

* Dans Visual Studio, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.
* Une fois que l’application se déploie sur le HoloLens, faire disparaître la boîte adaptée à l’aide de la [-appui en l’air](gestures.md#air-tap) mouvement.
* Fixez du espion de l’astronaut regard.
* Lors de la surveillance a le focus, vérifiez que le curseur se transforme en un microphone. Cela fournit des commentaires qui l’application est à l’écoute des commandes vocales.
* Vérifiez qu’une info-bulle s’affiche sur la surveillance. Cela permet aux utilisateurs de découvrir le *« Open Communicator »* commande.
* Lors de la gazing à la surveillance, par exemple *« Ouvrir Communicator »* pour ouvrir le panneau de communicator.

## <a name="chapter-2---acknowledgement"></a>Chapitre 2 - accusé de réception

>[!VIDEO https://www.youtube.com/embed/87ViteoPpyU]

### <a name="objectives"></a>Objectifs

* Enregistrer un message à l’aide de la saisie par Microphone.
* Envoyer des commentaires à l’utilisateur que l’application est à l’écoute à leur voix.

>[!NOTE]
>Le **Microphone** fonctionnalité doit être déclarée pour une application enregistrer à l’aide du microphone. Cela est fait pour vous déjà dans 212 d’entrée M., mais gardez cela à l’esprit pour vos propres projets.
>
>1. Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »
>2. Cliquez sur l’onglet « Plateforme Windows universelle »
>3. Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **Microphone** fonctionnalité

### <a name="instructions"></a>Instructions

* Dans Unity **hiérarchie** panneau, vérifiez que le **holoComm_screen_mesh** objet est sélectionné.
* Dans le **inspecteur** panneau, recherchez le **Astronaut espion (Script)** composant.
* Cliquez sur le cube petit, bleu, qui est défini comme valeur de la **Prefab Communicator** propriété.
* Dans le **projet** Panneau de configuration, le **Communicator** préfabriqué doit maintenant avoir le focus.
* Cliquez sur le **Communicator** prefab dans le **projet** Panneau de configuration pour afficher ses composants dans le **inspecteur**.
* Examinez le **Manager Microphone (Script)** composant, cela nous permettra d’enregistrement vocal de l’utilisateur.
* Notez que le **Communicator** objet possède un **Gestionnaire d’entrée vocale (Script)** composant pour répondre à la **envoyer un Message** commande.
* Examinez le **Communicator (Script)** composant et double-cliquez sur le script pour l’ouvrir dans Visual Studio.

Communicator.cs est chargé de définir les États de bouton appropriées sur l’appareil de communicator. Cela permettra à nos utilisateurs d’enregistrer un message, lire et envoyer le message au astronautes !. Il sera également commencer et arrêter une forme d’onde animée, pour accuser réception à l’utilisateur qu’il a été entendre leur voix.

* Dans **Communicator.cs**, supprimez les lignes suivantes (81 et 82) de la **Démarrer** (méthode). Cela active le bouton 'Record' sur le communicator.

```cs
// TODO: 2.a Delete the following two lines:
RecordButton.SetActive(false);
MessageUIRenderer.gameObject.SetActive(false);
```

### <a name="build-and-deploy"></a>Générer et déployer

* Dans Visual Studio, régénérez votre application et les déployer sur l’appareil.
* Fixez du espion de l’astronaut regard et dire *« Open Communicator »* pour afficher le communicator.
* Appuyez sur la **enregistrement** bouton (microphone) pour commencer l’enregistrement d’un message verbaux pour l’astronautes !.
* Commencez à parler et vérifiez que l’animation de wave est lue sur communicator, qui fournit des commentaires à l’utilisateur que d’entendre leur voix.
* Appuyez sur la **arrêter** bouton (carré gauche), puis vérifiez que l’animation wave cesse de s’exécuter.
* Appuyez sur la **lire** bouton (triangle rectangle) permettant de lire le message enregistré et avoir votre avis sur l’appareil.
* Appuyez sur la **arrêter** bouton (carré de droite) pour arrêter la lecture du message enregistré.
* Par exemple *« Envoyer un Message »* pour fermer le communicator et de recevoir une réponse « Message reçu » de l’astronaut.

## <a name="chapter-3---understanding-and-the-dictation-recognizer"></a>Chapitre 3 - présentation et le module de reconnaissance de dictée

>[!VIDEO https://www.youtube.com/embed/TIMddr-HqEU]

### <a name="objectives"></a>Objectifs

* Utilisez le module de reconnaissance de dictée pour convertir les voix de l’utilisateur en texte.
* Afficher les résultats de test d’hypothèse sur et dernière du module de reconnaissance dictée dans l’Office communicator.

Dans ce chapitre, nous allons utiliser le module de reconnaissance de dictée pour créer un message pour l’astronautes !. Lorsque vous utilisez le module de reconnaissance de dictée, sachez que :

* Vous devez être connecté au réseau sans fil pour le module de reconnaissance de dictée fonctionne.
* Dépassement du délai après un laps de temps défini. Il existe deux délais d’expiration à connaître :
  * Si le module de reconnaissance commence et n’entendre des données audio pour les cinq premières secondes, elle dépassera le délai d’attente.
  * Si le module de reconnaissance a donné un résultat mais puis entend silence pendant 20 secondes, elle dépassera le délai d’attente.
* Seul un type de module de reconnaissance (mot clé ou dictée) permettre exécuter à la fois.

>[!NOTE]
>Le **Microphone** fonctionnalité doit être déclarée pour une application enregistrer à l’aide du microphone. Cela est fait pour vous déjà dans 212 d’entrée M., mais gardez cela à l’esprit pour vos propres projets.
>
>1. Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »
>2. Cliquez sur l’onglet « Plateforme Windows universelle »
>3. Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **Microphone** fonctionnalité

### <a name="instructions"></a>Instructions

Nous allons modifier **MicrophoneManager.cs** à utiliser le module de reconnaissance de dictée. C’est ce que nous allons ajouter :

1. Lorsque le **bouton d’enregistrement** est enfoncé, nous allons **démarrer le DictationRecognizer**.
2. Afficher le **hypothèse** de ce que le DictationRecognizer compris.
3. Verrouiller le **résultats** de ce que le DictationRecognizer compris.
4. Recherchez les délais d’attente à partir de la DictationRecognizer.
5. Lorsque le **bouton Arrêter** est enfoncé, ou la session de mic arrive à expiration, **arrêter le DictationRecognizer**.
6. Redémarrez le **KeywordRecognizer**, qui écoutera les le **envoyer un Message** commande.

Commençons. Terminer tous les exercices de codage pour 3.a dans **MicrophoneManager.cs**, ou copiez et collez le code de fin figurant ci-dessous :

```cs
// Copyright (c) Microsoft Corporation. All rights reserved.
// Licensed under the MIT License. See LICENSE in the project root for license information.

using System.Collections;
using System.Text;
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.Windows.Speech;

namespace Academy
{
    public class MicrophoneManager : MonoBehaviour
    {
        [Tooltip("A text area for the recognizer to display the recognized strings.")]
        [SerializeField]
        private Text dictationDisplay;

        private DictationRecognizer dictationRecognizer;

        // Use this string to cache the text currently displayed in the text box.
        private StringBuilder textSoFar;

        // Using an empty string specifies the default microphone. 
        private static string deviceName = string.Empty;
        private int samplingRate;
        private const int messageLength = 10;

        // Use this to reset the UI once the Microphone is done recording after it was started.
        private bool hasRecordingStarted;

        void Awake()
        {
            /* TODO: DEVELOPER CODING EXERCISE 3.a */

            // 3.a: Create a new DictationRecognizer and assign it to dictationRecognizer variable.
            dictationRecognizer = new DictationRecognizer();

            // 3.a: Register for dictationRecognizer.DictationHypothesis and implement DictationHypothesis below
            // This event is fired while the user is talking. As the recognizer listens, it provides text of what it's heard so far.
            dictationRecognizer.DictationHypothesis += DictationRecognizer_DictationHypothesis;

            // 3.a: Register for dictationRecognizer.DictationResult and implement DictationResult below
            // This event is fired after the user pauses, typically at the end of a sentence. The full recognized string is returned here.
            dictationRecognizer.DictationResult += DictationRecognizer_DictationResult;

            // 3.a: Register for dictationRecognizer.DictationComplete and implement DictationComplete below
            // This event is fired when the recognizer stops, whether from Stop() being called, a timeout occurring, or some other error.
            dictationRecognizer.DictationComplete += DictationRecognizer_DictationComplete;

            // 3.a: Register for dictationRecognizer.DictationError and implement DictationError below
            // This event is fired when an error occurs.
            dictationRecognizer.DictationError += DictationRecognizer_DictationError;

            // Query the maximum frequency of the default microphone. Use 'unused' to ignore the minimum frequency.
            int unused;
            Microphone.GetDeviceCaps(deviceName, out unused, out samplingRate);

            // Use this string to cache the text currently displayed in the text box.
            textSoFar = new StringBuilder();

            // Use this to reset the UI once the Microphone is done recording after it was started.
            hasRecordingStarted = false;
        }

        void Update()
        {
            // 3.a: Add condition to check if dictationRecognizer.Status is Running
            if (hasRecordingStarted && !Microphone.IsRecording(deviceName) && dictationRecognizer.Status == SpeechSystemStatus.Running)
            {
                // Reset the flag now that we're cleaning up the UI.
                hasRecordingStarted = false;

                // This acts like pressing the Stop button and sends the message to the Communicator.
                // If the microphone stops as a result of timing out, make sure to manually stop the dictation recognizer.
                // Look at the StopRecording function.
                SendMessage("RecordStop");
            }
        }

        /// <summary>
        /// Turns on the dictation recognizer and begins recording audio from the default microphone.
        /// </summary>
        /// <returns>The audio clip recorded from the microphone.</returns>
        public AudioClip StartRecording()
        {
            // 3.a Shutdown the PhraseRecognitionSystem. This controls the KeywordRecognizers
            PhraseRecognitionSystem.Shutdown();

            // 3.a: Start dictationRecognizer
            dictationRecognizer.Start();

            // 3.a Uncomment this line
            dictationDisplay.text = "Dictation is starting. It may take time to display your text the first time, but begin speaking now...";

            // Set the flag that we've started recording.
            hasRecordingStarted = true;

            // Start recording from the microphone for 10 seconds.
            return Microphone.Start(deviceName, false, messageLength, samplingRate);
        }

        /// <summary>
        /// Ends the recording session.
        /// </summary>
        public void StopRecording()
        {
            // 3.a: Check if dictationRecognizer.Status is Running and stop it if so
            if (dictationRecognizer.Status == SpeechSystemStatus.Running)
            {
                dictationRecognizer.Stop();
            }

            Microphone.End(deviceName);
        }

        /// <summary>
        /// This event is fired while the user is talking. As the recognizer listens, it provides text of what it's heard so far.
        /// </summary>
        /// <param name="text">The currently hypothesized recognition.</param>
        private void DictationRecognizer_DictationHypothesis(string text)
        {
            // 3.a: Set DictationDisplay text to be textSoFar and new hypothesized text
            // We don't want to append to textSoFar yet, because the hypothesis may have changed on the next event
            dictationDisplay.text = textSoFar.ToString() + " " + text + "...";
        }

        /// <summary>
        /// This event is fired after the user pauses, typically at the end of a sentence. The full recognized string is returned here.
        /// </summary>
        /// <param name="text">The text that was heard by the recognizer.</param>
        /// <param name="confidence">A representation of how confident (rejected, low, medium, high) the recognizer is of this recognition.</param>
        private void DictationRecognizer_DictationResult(string text, ConfidenceLevel confidence)
        {
            // 3.a: Append textSoFar with latest text
            textSoFar.Append(text + ". ");

            // 3.a: Set DictationDisplay text to be textSoFar
            dictationDisplay.text = textSoFar.ToString();
        }

        /// <summary>
        /// This event is fired when the recognizer stops, whether from Stop() being called, a timeout occurring, or some other error.
        /// Typically, this will simply return "Complete". In this case, we check to see if the recognizer timed out.
        /// </summary>
        /// <param name="cause">An enumerated reason for the session completing.</param>
        private void DictationRecognizer_DictationComplete(DictationCompletionCause cause)
        {
            // If Timeout occurs, the user has been silent for too long.
            // With dictation, the default timeout after a recognition is 20 seconds.
            // The default timeout with initial silence is 5 seconds.
            if (cause == DictationCompletionCause.TimeoutExceeded)
            {
                Microphone.End(deviceName);

                dictationDisplay.text = "Dictation has timed out. Please press the record button again.";
                SendMessage("ResetAfterTimeout");
            }
        }

        /// <summary>
        /// This event is fired when an error occurs.
        /// </summary>
        /// <param name="error">The string representation of the error reason.</param>
        /// <param name="hresult">The int representation of the hresult.</param>
        private void DictationRecognizer_DictationError(string error, int hresult)
        {
            // 3.a: Set DictationDisplay text to be the error string
            dictationDisplay.text = error + "\nHRESULT: " + hresult;
        }

        /// <summary>
        /// The dictation recognizer may not turn off immediately, so this call blocks on
        /// the recognizer reporting that it has actually stopped.
        /// </summary>
        public IEnumerator WaitForDictationToStop()
        {
            while (dictationRecognizer != null && dictationRecognizer.Status == SpeechSystemStatus.Running)
            {
                yield return null;
            }
        }
    }
}
```

### <a name="build-and-deploy"></a>Générer et déployer

* Régénérez dans Visual Studio et les déployer sur votre appareil.
* Fermez l’adapté avec un mouvement d’appui en l’air.
* Fixez du espion de l’astronaut regard et dire *« Open Communicator »*.
* Sélectionnez le **enregistrement** bouton (microphone) pour enregistrer votre message.
* Commencez à parler. Le **module de reconnaissance de dictée** interprétera votre enregistrement vocal et afficher le test d’hypothèse sur texte dans l’Office communicator.
* Essayez de dire *« Envoyer un Message »* pendant que vous enregistrez un message. Notez que le **mot clé de module de reconnaissance** ne répond pas, car le **module de reconnaissance de dictée** est toujours actif.
* Arrêter de parler de quelques secondes. Écoutez le module de reconnaissance de dictée se termine son hypothèse et affiche le résultat final.
* Commencez à parler et puis de s’interrompre pendant 20 secondes. Cela entraîne le **module de reconnaissance de dictée** au délai d’attente.
* Notez que le **module de reconnaissance de mot clé** est réactivé après le délai d’attente ci-dessus. Le communicator est maintenant répondre aux commandes vocales.
* Par exemple *« Envoyer un Message »* pour envoyer le message au astronautes !.

## <a name="chapter-4---grammar-recognizer"></a>Chapitre 4 - module de reconnaissance de grammaire

>[!VIDEO https://www.youtube.com/embed/J2dYJNSvv18]

### <a name="objectives"></a>Objectifs

* Utilisez le module de reconnaissance de grammaire voix de l’utilisateur en fonction d’un fichier SRGS ou spécification de grammaire de reconnaissance vocale.

>[!NOTE]
>Le **Microphone** fonctionnalité doit être déclarée pour une application enregistrer à l’aide du microphone. Cela est fait pour vous déjà dans 212 d’entrée M., mais gardez cela à l’esprit pour vos propres projets.
>
>1. Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »
>2. Cliquez sur l’onglet « Plateforme Windows universelle »
>3. Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **Microphone** fonctionnalité

### <a name="instructions"></a>Instructions

1. Dans le **hiérarchie** du panneau, recherchez **Jetpack_Center** et sélectionnez-le.
2. Recherchez le **accompagnent Action** de script dans le **inspecteur** Panneau de configuration.
3. Cliquez sur le petit cercle à droite de la **objet de balise le long** champ.
4. Dans la fenêtre qui s’affiche, recherchez **SRGSToolbox** et sélectionnez-le dans la liste.
5. Jetez un coup de œil à la **SRGSColor.xml** de fichiers dans le **StreamingAssets** dossier.
* La spécification de conception SRGS sont accessibles sur le site Web W3C [ici](https://www.w3.org/TR/speech-grammar/).
* Dans notre fichier SRGS, nous avons trois types de règles :
  * Une règle qui vous permet d’indiquer une couleur à partir d’une liste de douze couleurs.
  * Trois règles qui écoutent une combinaison de la règle de couleur et l’une des trois formes.
  * La règle racine, colorChooser d’écoute de n’importe quelle combinaison des trois règles « couleur + mettre en forme ». Les formes peuvent être désignées dans n’importe quel ordre et dans n’importe quel volume depuis un seul pour les trois. Ceci est la seule règle qui est écoutée, tel qu’il est spécifié comme règle racine en haut du fichier initial &lt;grammaire&gt; balise.

### <a name="build-and-deploy"></a>Générer et déployer

* Régénérez l’application dans Unity, puis générez et déployez à partir de Visual Studio pour profiter de l’application sur HoloLens.
* Fermez l’adapté avec un mouvement d’appui en l’air.
* Fixez du jetpack de l’astronaut regard et effectuez un mouvement d’appui en l’air.
* Commencez à parler. Le **module de reconnaissance de grammaire** interpréter votre voix et de modifier les couleurs des formes en fonction de la reconnaissance. Un exemple de commande est « cercle bleu, jaune carré ».
* Effectuez une autre-appui en l’air pour faire disparaître la boîte à outils.

## <a name="the-end"></a>La fin

Félicitations ! Vous avez maintenant terminé **212 d’entrée M. : Voix**.

* Vous connaissez les choses à faire et des commandes vocales.
* Vous avez vu comment les info-bulles ont été utilisés pour informer les utilisateurs des commandes vocales.
* Vous avez vu plusieurs types de commentaires permet de confirmer que la voix de l’utilisateur a été émises.
* Vous savez comment basculer entre le module de reconnaissance du mot clé et le module de reconnaissance de dictée, et comment ces deux fonctionnalités comprennent et interprètent votre voix.
* Vous avez appris comment utiliser un fichier SRGS et le module de reconnaissance de grammaire de reconnaissance vocale dans votre application.
