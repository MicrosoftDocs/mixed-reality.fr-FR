---
title: Entrée MR 212-voix
description: Suivez cette procédure pas à pas de codage avec Unity, Visual Studio et HoloLens pour apprendre les détails des concepts vocaux.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, vocal
ms.openlocfilehash: 9db503ea4c7db9a3eb272ad9663024ca3a407dda
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434598"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. [Une nouvelle série de didacticiels](mrlearning-base.md) a été publiée pour HoloLens 2.

<br>

# <a name="mr-input-212-voice"></a>Entrée MR 212 : voix

La [saisie vocale](voice-input.md) nous offre une autre manière d’interagir avec nos hologrammes. Les commandes vocales fonctionnent de manière très naturelle et simple. Concevez vos commandes vocales de sorte qu’elles soient :

* Parfois
* Facile à mémoriser
* Contexte approprié
* Suffisamment distinct des autres options dans le même contexte

>[!VIDEO https://www.youtube.com/embed/BYpYsVFYjdw]

Dans les [notions de base de m. 101](holograms-101.md), nous avons utilisé le KeywordRecognizer pour créer deux commandes vocales simples. Dans l’entrée d’Monsieur 212, nous allons approfondir et apprendre à :

* Concevez des commandes vocales optimisées pour le moteur de reconnaissance vocale HoloLens.
* Faites savoir aux utilisateurs quelles commandes vocales sont disponibles.
* Confirmez que nous avons entendu la commande vocale de l’utilisateur.
* Comprendre ce que l’utilisateur dit, à l’aide d’un module de reconnaissance de dictée.
* Utilisez un module de reconnaissance grammatical pour écouter les commandes basées sur un SRGS, ou sur la spécification de la grammaire de la reconnaissance vocale, file.

Dans ce cours, nous allons revisiter l’Explorateur de modèles, que nous avons créé dans l' [entrée 210](holograms-210.md) et l' [entrée Mr 211](holograms-211.md).

>[!IMPORTANT]
>Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrées à l’aide d’une version antérieure d’Unity et de la réalité mixte Toolkit. Alors que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des visuels dans les vidéos correspondantes qui sont obsolètes. Les vidéos restent incluses pour l’affiche et les concepts abordés s’appliquent toujours.


## <a name="device-support"></a>Périphériques pris en charge

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>Entrée MR 212 : voix</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Conditions préalables

* Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).
* Certaines fonctionnalités C# de programmation de base.
* Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).
* Vous devez avoir terminé l' [entrée 210](holograms-210.md).
* Vous devez avoir terminé l' [entrée 211](holograms-211.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-212-Voice.zip) requis par le projet. Requiert Unity 2017,2 ou une version ultérieure.
* Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-212-Voice).

### <a name="errata-and-notes"></a>Errata et notes

* L’option « Activer Uniquement mon code » doit être désactivée (*décochée*) dans Visual Studio sous outils-> Options-> le débogage pour atteindre les points d’arrêt dans votre code.

## <a name="unity-setup"></a>Configuration de Unity

### <a name="instructions"></a>Instructions

1. Démarrez Unity.
2. Sélectionnez **ouvrir**.
3. Accédez au dossier **HolographicAcademy-hologrammees-212-Voice** que vous avez précédemment désinstallé.
4. Recherchez et sélectionnez le dossier **démarrage**/**Explorateur de modèles** .
5. Cliquez sur le bouton **Sélectionner un dossier** .
6. Dans le panneau **projet** , développez le dossier **scenes** .
7. Double-cliquez sur **ModelExplorer** Scene pour le charger dans Unity.

### <a name="building"></a>Création

1. Dans Unity, sélectionnez **fichier > paramètres de build**.
2. Si **scenes/ModelExplorer** n’est pas listé dans **scenes dans Build**, cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.
3. Si vous développez spécifiquement pour HoloLens, définissez **appareil cible** sur **hololens**. Dans le cas contraire, laissez-le sur **un appareil**.
4. Vérifiez que le **type de build** est défini sur **D3D** et que le **Kit de développement logiciel (SDK** ) est défini sur le **dernier installé** (qui doit être le SDK 16299 ou une version ultérieure).
5. Cliquez sur **Build**.
6. Créez un **dossier** nommé « App ».
7. Cliquez sur le dossier de l' **application** .
8. Appuyez sur **Sélectionner un dossier** et Unity va commencer à générer le projet pour Visual Studio.

Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.

1. Ouvrez le dossier de l' **application** .
2. Ouvrez la **solution Visual Studio ModelExplorer**.

En cas de déploiement dans HoloLens :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.
2. Cliquez sur la flèche déroulante en regard du bouton ordinateur local, puis sélectionnez **ordinateur distant**.
3. Entrez **l’adresse IP de votre appareil HoloLens** et définissez le mode d’authentification sur **universel (protocole non chiffré)** . Cliquez sur **Sélectionner**. Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées**.
4. Dans la barre de menus supérieure, cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**. S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le [coupler à Visual Studio](using-visual-studio.md#pairing-your-device).
5. Une fois l’application déployée, ignorez le **Fitbox** avec un **mouvement Select**.

En cas de déploiement sur un casque immersif :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.
2. Assurez-vous que la cible de déploiement est définie sur **ordinateur local**.
3. Dans la barre de menus supérieure, cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
4. Une fois l’application déployée, Faites disparaître le **Fitbox** en tirant le déclencheur sur un contrôleur de mouvement.

>[!NOTE]
>Vous pouvez remarquer des erreurs rouges dans le panneau erreurs de Visual Studio. Vous pouvez les ignorer en toute sécurité. Basculez vers le panneau sortie pour afficher la progression réelle de la génération. Les erreurs dans le panneau sortie vous obligent à faire un correctif (le plus souvent, elles sont provoquées par une erreur dans un script).

## <a name="chapter-1---awareness"></a>Chapitre 1-sensibilisation

>[!VIDEO https://www.youtube.com/embed/fDwijJWuEc0]

### <a name="objectives"></a>Objectifs

* Découvrez les **dénis** de la conception des commandes vocales.
* Utilisez **KeywordRecognizer** pour ajouter des commandes vocales en regard.
* Faites savoir aux utilisateurs les commandes vocales à l’aide de **Commentaires**sur les curseurs.

### <a name="voice-command-design"></a>Conception de commande vocale

Dans ce chapitre, vous allez apprendre à concevoir des commandes vocales. Lors de la création de commandes vocales :

#### <a name="do"></a>DO

* Créer des commandes concises. Vous ne souhaitez pas utiliser *« Lire la vidéo actuellement sélectionnée »* , car cette commande n’est pas concise et peut facilement être oubliée par l’utilisateur. Au lieu de cela, vous devez utiliser : *« Lire la vidéo »* , car elle est concise et comporte plusieurs syllabes.
* Utilisez un vocabulaire simple. Essayez toujours d’utiliser des mots et des expressions courants qui sont faciles à découvrir et à mémoriser pour l’utilisateur. Par exemple, si votre application comporte un objet note qui peut être affiché ou masqué, vous n’utiliseriez pas la commande *« Show pancarte »* , car « pancarte » est un terme rarement utilisé. Au lieu de cela, vous devez utiliser la commande : *« Show note »* pour révéler la remarque dans votre application.
* Soyez cohérent. Les commandes vocales doivent rester cohérentes dans l’ensemble de votre application. Imaginez que vous avez deux scènes dans votre application et que les deux scènes contiennent un bouton pour fermer l’application. Si la première scène a utilisé la commande *« Exit »* pour déclencher le bouton, alors que la deuxième scène a utilisé la commande *« Close App »* , l’utilisateur va être très confus. Si la même fonctionnalité persiste sur plusieurs scènes, la même commande vocale doit être utilisée pour la déclencher.

#### <a name="dont"></a>Ne pas

* Utilisez des commandes d’une seule syllabe. Par exemple, si vous créez une commande vocale pour lire une vidéo, vous devez éviter d’utiliser la commande simple *« lecture »* , car il ne s’agit que d’une seule syllabe qui peut être facilement manquée par le système. Au lieu de cela, vous devez utiliser : *« Lire la vidéo »* , car elle est concise et comporte plusieurs syllabes.
* Utilisez les commandes système. La commande *« Select »* est réservée par le système pour déclencher un événement TAP pour l’objet actuellement actif. Ne réutilisez pas la commande *« Select »* dans un mot clé ou une expression, car elle risque de ne pas fonctionner comme prévu. Par exemple, si la commande de voix pour la sélection d’un cube dans votre application était *« Sélectionner un cube »* , mais que l’utilisateur regardait une sphère lorsqu’il a intégré la commande, la sphère serait sélectionnée à la place. De même, les commandes de la barre d’application sont activées pour la voix. N’utilisez pas les commandes vocales suivantes dans votre vue CoreWindow :
    1. Retour
    2. Outil de défilement
    3. Outil zoom
    4. Faire glisser l’outil
    5. Ajuster
    6. Remove
* Utilisez des sons similaires. Essayez d’éviter d’utiliser des commandes vocales qui agencement. Si vous aviez une application d’achat qui prenait en charge *« afficher le magasin »* et *« afficher plus »* en tant que commandes vocales, vous souhaiterez désactiver l’une des commandes pendant que l’autre était en cours d’utilisation. Par exemple, vous pouvez utiliser le bouton *« afficher le magasin »* pour ouvrir le magasin, puis désactiver cette commande lors de l’affichage de la Banque afin que la commande *« afficher plus »* puisse être utilisée pour la navigation.

### <a name="instructions"></a>Instructions

* Dans le panneau de la **hiérarchie** Unity, utilisez l’outil de recherche pour Rechercher l’objet **holoComm_screen_mesh** .
* Double-cliquez sur l’objet **holoComm_screen_mesh** pour l’afficher dans la **scène**. Il s’agit de la montre de astronautes, qui répondra à nos commandes vocales.
* Dans le volet de l' **inspecteur** , localisez le composant **source d’entrée vocale (script)** .
* Développez la section **Mots clés** pour voir la commande vocale prise en charge : **ouvrir Communicator**.
* Cliquez sur le roue dentée situé à droite, puis sélectionnez **modifier le script**.
* Explorez **SpeechInputSource.cs** pour comprendre comment il utilise **KeywordRecognizer** pour ajouter des commandes vocales.

### <a name="build-and-deploy"></a>Génération et déploiement

* Dans Unity, utilisez les **paramètres de build de > de fichiers** pour régénérer l’application.
* Ouvrez le dossier de l' **application** .
* Ouvrez la **solution Visual Studio ModelExplorer**.

(Si vous avez déjà généré/déployé ce projet dans Visual Studio au cours de la configuration, vous pouvez ouvrir cette instance de VS et cliquer sur « recharger tout » lorsque vous y êtes invité).

* Dans Visual Studio, cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
* Une fois que l’application a été déployée sur HoloLens, ignorez la zone d’ajustement à l’aide du mouvement d' [appui sur l’air](gaze-and-commit.md#composite-gestures) .
* Pointez le regard de la montre du astronautes.
* Lorsque la montre a le focus, vérifiez que le curseur se transforme en microphone. Cela fournit des commentaires que l’application écoute pour les commandes vocales.
* Vérifiez qu’une info-bulle apparaît sur la montre. Cela aide les utilisateurs à découvrir la commande *« Open Communicator »* .
* Si Gazing à la montre, dites *« ouvrir Communicator »* pour ouvrir le panneau Communicator.

## <a name="chapter-2---acknowledgement"></a>Chapitre 2-accusé de réception

>[!VIDEO https://www.youtube.com/embed/87ViteoPpyU]

### <a name="objectives"></a>Objectifs

* Enregistrez un message à l’aide de l’entrée microphone.
* Envoyer des commentaires à l’utilisateur que l’application écoute sur sa voix.

>[!NOTE]
>La fonctionnalité **microphone** doit être déclarée pour qu’une application soit enregistrée à partir du microphone. Cela est fait pour vous déjà dans une entrée de m. 212, mais gardez cela à l’esprit pour vos propres projets.
>
>1. Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à « modifier les paramètres du projet > > Player ».
>2. Cliquez sur l’onglet « plateforme Windows universelle »
>3. Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la fonctionnalité du **microphone** .

### <a name="instructions"></a>Instructions

* Dans le panneau de la **hiérarchie** Unity, vérifiez que l’objet **holoComm_screen_mesh** est sélectionné.
* Dans le volet de l' **inspecteur** , recherchez le composant **astronautes Watch (script)** .
* Cliquez sur le petit cube bleu défini comme valeur de la propriété **Communicator Prefab** .
* Dans le panneau **projet** , le Prefab **Communicator** doit maintenant avoir le focus.
* Cliquez sur le Prefab **Communicator** dans le panneau **projet** pour afficher ses composants dans l' **inspecteur**.
* Examinez le composant du **Gestionnaire de microphone (script)** , ceci nous permettra d’enregistrer la voix de l’utilisateur.
* Notez que l’objet **Communicator** possède un composant **Gestionnaire d’entrée vocale (script)** pour répondre à la commande **Envoyer un message** .
* Examinez le composant **Communicator (script)** et double-cliquez sur le script pour l’ouvrir dans Visual Studio.

Communicator.cs est chargé de définir les États de bouton appropriés sur le périphérique Communicator. Cela permet à nos utilisateurs d’enregistrer un message, de le lire et d’envoyer le message à astronautes. Il démarre et arrête également un formulaire d’onde animée, pour accuser réception à l’utilisateur que sa voix a été entendue.

* Dans **Communicator.cs**, supprimez les lignes suivantes (81 et 82) de la méthode **Start** . Cela active le bouton « enregistrer » sur le Communicator.

```cs
// TODO: 2.a Delete the following two lines:
RecordButton.SetActive(false);
MessageUIRenderer.gameObject.SetActive(false);
```

### <a name="build-and-deploy"></a>Génération et déploiement

* Dans Visual Studio, régénérez votre application et déployez-la sur l’appareil.
* Pointez le regard du astronautes et dites *« ouvrir Communicator »* pour afficher le Communicator.
* Appuyez sur le bouton d' **enregistrement** (microphone) pour démarrer l’enregistrement d’un message verbal pour le astronautes.
* Commencez à parler et vérifiez que l’animation Wave est jouée sur le Communicator, ce qui fournit des commentaires à l’utilisateur indiquant que sa voix est audible.
* Appuyez sur le bouton **arrêter** (carré gauche) et vérifiez que l’animation Wave cesse de s’exécuter.
* Appuyez sur le bouton de **lecture** (triangle rectangle) pour lire le message enregistré et l’écouter sur l’appareil.
* Appuyez sur le bouton **arrêter** (carré droit) pour arrêter la lecture du message enregistré.
* Dites *« Envoyer un message »* pour fermer le Communicator et recevoir une réponse « message received » de astronautes.

## <a name="chapter-3---understanding-and-the-dictation-recognizer"></a>Chapitre 3 : compréhension et le module de reconnaissance de la dictée

>[!VIDEO https://www.youtube.com/embed/TIMddr-HqEU]

### <a name="objectives"></a>Objectifs

* Utilisez le module de reconnaissance de dictée pour convertir la parole de l’utilisateur en texte.
* Affichez les résultats de l’hypothèse et du résultat final du module de reconnaissance de dictée dans Communicator.

Dans ce chapitre, nous allons utiliser le module de reconnaissance de dictée pour créer un message pour le astronautes. Lorsque vous utilisez le module de reconnaissance de dictée, gardez à l’esprit que :

* Vous devez être connecté à WiFi pour que le module de reconnaissance de dictée fonctionne.
* Les délais d’attente se produisent après un laps de temps défini. Deux délais d’attente doivent être pris en compte :
  * Si le module de reconnaissance démarre et n’entend aucun audio pendant les cinq premières secondes, il expire.
  * Si le module de reconnaissance a donné un résultat, mais émet un silence pendant vingt secondes, il expire.
* Un seul type de module de reconnaissance (mot clé ou dictée) peut s’exécuter à la fois.

>[!NOTE]
>La fonctionnalité **microphone** doit être déclarée pour qu’une application soit enregistrée à partir du microphone. Cela est fait pour vous déjà dans une entrée de m. 212, mais gardez cela à l’esprit pour vos propres projets.
>
>1. Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à « modifier les paramètres du projet > > Player ».
>2. Cliquez sur l’onglet « plateforme Windows universelle »
>3. Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la fonctionnalité du **microphone** .

### <a name="instructions"></a>Instructions

Nous allons modifier **MicrophoneManager.cs** pour utiliser le module de reconnaissance de dictée. Voici ce que nous allons ajouter :

1. Lorsque vous appuyez sur le **bouton d’enregistrement** , nous allons **Démarrer le DictationRecognizer**.
2. Montrez l' **hypothèse** de ce que le DictationRecognizer a compris.
3. Verrouillez les **résultats** de ce que le DictationRecognizer a compris.
4. Vérifiez les délais d’attente à partir du DictationRecognizer.
5. Lorsque vous appuyez sur le **bouton arrêter** ou que la session MIC expire, **Arrêtez le DictationRecognizer**.
6. Redémarrez **KeywordRecognizer**, qui écoutera la commande **Envoyer un message** .

Commençons. Terminez tous les exercices de codage pour 3. a dans **MicrophoneManager.cs**, ou copiez et collez le code final trouvé ci-dessous :

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

### <a name="build-and-deploy"></a>Génération et déploiement

* Régénérez dans Visual Studio et déployez sur votre appareil.
* Faites disparaître la zone d’ajustement avec un mouvement d’appui sur l’air.
* Pointez le regard du astronautes et dites *« ouvrir Communicator »* .
* Sélectionnez le bouton d' **enregistrement** (microphone) pour enregistrer votre message.
* Commencez à parler. Le module de **reconnaissance de dictée** interprètera votre discours et affichera le texte de l’hypothèse dans le Communicator.
* Essayez de dire *« Envoyer un message »* lors de l’enregistrement d’un message. Notez que le module de **reconnaissance de mot clé** ne répond pas, car le module de **reconnaissance de dictée** est toujours actif.
* Arrêtez de parler pendant quelques secondes. Regardez que le module de reconnaissance de dictée termine son hypothèse et montre le résultat final.
* Commencez à parler, puis suspendez pendant 20 secondes. Le module de **reconnaissance de dictée** est alors dépassé.
* Notez que le module de **reconnaissance de mot clé** est réactivé après l’expiration du délai d’attente. Communicator répond alors aux commandes vocales.
* Dites *« Envoyer un message »* pour envoyer le message à astronautes.

## <a name="chapter-4---grammar-recognizer"></a>Chapitre 4-module de reconnaissance de la grammaire

>[!VIDEO https://www.youtube.com/embed/J2dYJNSvv18]

### <a name="objectives"></a>Objectifs

* Utilisez le module de reconnaissance grammatical pour reconnaître la parole de l’utilisateur en fonction d’un SRGS, ou de la spécification de la grammaire de la reconnaissance vocale, fichier.

>[!NOTE]
>La fonctionnalité **microphone** doit être déclarée pour qu’une application soit enregistrée à partir du microphone. Cela est fait pour vous déjà dans une entrée de m. 212, mais gardez cela à l’esprit pour vos propres projets.
>
>1. Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à « modifier les paramètres du projet > > Player ».
>2. Cliquez sur l’onglet « plateforme Windows universelle »
>3. Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la fonctionnalité du **microphone** .

### <a name="instructions"></a>Instructions

1. Dans le volet **hiérarchie** , recherchez **Jetpack_Center** et sélectionnez-le.
2. Recherchez le script d' **action accompagnent** dans le panneau **inspecteur** .
3. Cliquez sur le petit cercle situé à droite de l' **objet à baliser** sur le champ.
4. Dans la fenêtre qui s’affiche, recherchez **SRGSToolbox** et sélectionnez-le dans la liste.
5. Jetez un coup d’œil au fichier **SRGSColor. xml** dans le dossier **StreamingAssets** .
    1. Les spécifications de conception SRGS se trouvent sur le site Web du W3C [ici](https://www.w3.org/TR/speech-grammar/).

Dans notre fichier SRGS, nous avons trois types de règles :

* Une règle qui vous permet d’indiquer une couleur dans une liste de douze couleurs.
* Trois règles qui écoutent une combinaison de la règle de couleur et l’une des trois formes.
* La règle racine, colorChooser, qui écoute toutes les combinaisons des trois règles de « couleur et de forme ». Les formes peuvent être déclarées dans n’importe quel ordre et dans n’importe quel montant, d’une seule à l’autre. Il s’agit de la seule règle écoutée pour, telle qu’elle est spécifiée en tant que règle racine en haut du fichier dans la balise de&gt; de grammaire initiale &lt;.

### <a name="build-and-deploy"></a>Génération et déploiement

* Régénérez l’application dans Unity, puis générez et déployez à partir de Visual Studio pour expérimenter l’application sur HoloLens.
* Faites disparaître la zone d’ajustement avec un mouvement d’appui sur l’air.
* Pointez le regard du astronautes et effectuez un mouvement d’appui sur l’air.
* Commencez à parler. Le module de reconnaissance de la **grammaire** interprète votre discours et modifie les couleurs des formes en fonction de la reconnaissance. Un exemple de commande est « cercle bleu, carré jaune ».
* Effectuez un autre mouvement d’appui sur l’air pour faire disparaître la boîte à outils.

## <a name="the-end"></a>La fin

Félicitations ! Vous avez maintenant terminé l' **entrée 212 : Voice**.

* Vous connaissez les dos et les absences de commandes vocales.
* Vous avez vu comment les info-bulles étaient utilisées pour que les utilisateurs soient informés des commandes vocales.
* Vous avez vu plusieurs types de commentaires utilisés pour accuser réception de la voix de l’utilisateur.
* Vous savez comment basculer entre le module de reconnaissance de mot clé et le module de reconnaissance de dictée, et comment ces deux fonctionnalités comprennent et interprètent votre voix.
* Vous avez appris à utiliser un fichier SRGS et le module de reconnaissance grammaticale pour la reconnaissance vocale dans votre application.
