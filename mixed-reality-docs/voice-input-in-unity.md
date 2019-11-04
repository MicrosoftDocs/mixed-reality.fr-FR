---
title: Entrée vocale dans Unity
description: Unity expose trois façons d’ajouter une entrée vocale à votre application Windows Mixed Reality.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Entrée vocale, KeywordRecognizer, GrammarRecognizer, microphone, dictée, voix
ms.openlocfilehash: d1cd2a2b954a195bc3f2688d915965f89aa30f98
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438196"
---
# <a name="voice-input-in-unity"></a><span data-ttu-id="cc3f2-104">Entrée vocale dans Unity</span><span class="sxs-lookup"><span data-stu-id="cc3f2-104">Voice input in Unity</span></span>

>[!NOTE]
><span data-ttu-id="cc3f2-105">Au lieu d’utiliser les informations ci-dessous, envisagez d’utiliser le plug-in Unity pour le kit de développement logiciel (SDK) cognitive Speech services qui offre de meilleurs résultats de précision vocale et fournit un accès facile au décodage vocal en texte et à des fonctionnalités vocales avancées telles que la boîte de dialogue, intentionnellement interaction, traduction, synthèse vocale et reconnaissance vocale en langage naturel.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-105">Instead of the below information, consider using the Unity plug-in for the Cognitive Speech Services SDK which has much better Speech Accuracy results and provides easy access to speech-to-text decode and advanced speech features like dialog, intent based interaction, translation, text-to-speech synthesis and natural language speech recognition.</span></span> <span data-ttu-id="cc3f2-106">Recherchez l’exemple et documentation ici : https://docs.microsoft.com//azure/cognitive-services/speech-service/quickstart-csharp-unity</span><span class="sxs-lookup"><span data-stu-id="cc3f2-106">Find the sample and documentaion here: https://docs.microsoft.com//azure/cognitive-services/speech-service/quickstart-csharp-unity</span></span>   

<span data-ttu-id="cc3f2-107">Unity expose trois façons d’ajouter une [entrée vocale](voice-input.md) à votre application Unity.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-107">Unity exposes three ways to add [Voice input](voice-input.md) to your Unity application.</span></span>

<span data-ttu-id="cc3f2-108">Avec KeywordRecognizer (l’un des deux types de PhraseRecognizers), votre application peut recevoir un tableau de commandes de chaîne à écouter.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-108">With the KeywordRecognizer (one of two types of PhraseRecognizers), your app can be given an array of string commands to listen for.</span></span> <span data-ttu-id="cc3f2-109">Avec GrammarRecognizer (l’autre type de PhraseRecognizer), votre application peut recevoir un fichier SRGS définissant une grammaire spécifique à écouter.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-109">With the GrammarRecognizer (the other type of PhraseRecognizer), your app can be given an SRGS file defining a specific grammar to listen for.</span></span> <span data-ttu-id="cc3f2-110">Avec DictationRecognizer, votre application peut écouter tout mot et fournir à l’utilisateur une note ou un autre affichage de sa parole.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-110">With the DictationRecognizer, your app can listen for any word and provide the user with a note or other display of their speech.</span></span>

>[!NOTE]
><span data-ttu-id="cc3f2-111">Seule la reconnaissance de la dictée ou de l’expression peut être gérée à la fois.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-111">Only dictation or phrase recognition can be handled at once.</span></span> <span data-ttu-id="cc3f2-112">Cela signifie que si un GrammarRecognizer ou un KeywordRecognizer est actif, un DictationRecognizer ne peut pas être actif et vice versa.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-112">That means if a GrammarRecognizer or KeywordRecognizer is active, a DictationRecognizer can not be active and vice versa.</span></span>

## <a name="enabling-the-capability-for-voice"></a><span data-ttu-id="cc3f2-113">Activation de la fonctionnalité de voix</span><span class="sxs-lookup"><span data-stu-id="cc3f2-113">Enabling the capability for Voice</span></span>

<span data-ttu-id="cc3f2-114">La fonctionnalité **microphone** doit être déclarée pour qu’une application tire parti de l’entrée vocale.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-114">The **Microphone** capability must be declared for an app to leverage Voice input.</span></span>
1. <span data-ttu-id="cc3f2-115">Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à « modifier les paramètres du projet > > Player ».</span><span class="sxs-lookup"><span data-stu-id="cc3f2-115">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
2. <span data-ttu-id="cc3f2-116">Cliquer sur l’onglet « Windows Store »</span><span class="sxs-lookup"><span data-stu-id="cc3f2-116">Click on the "Windows Store" tab</span></span>
3. <span data-ttu-id="cc3f2-117">Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la fonctionnalité du **microphone** .</span><span class="sxs-lookup"><span data-stu-id="cc3f2-117">In the "Publishing Settings > Capabilities" section, check the **Microphone** capability</span></span>

## <a name="phrase-recognition"></a><span data-ttu-id="cc3f2-118">Reconnaissance d’expressions</span><span class="sxs-lookup"><span data-stu-id="cc3f2-118">Phrase Recognition</span></span>

<span data-ttu-id="cc3f2-119">Pour permettre à votre application d’écouter des expressions spécifiques parlées par l’utilisateur, puis de prendre des mesures, vous devez :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-119">To enable your app to listen for specific phrases spoken by the user then take some action, you need to:</span></span>
1. <span data-ttu-id="cc3f2-120">Spécifier les expressions à écouter à l’aide d’un KeywordRecognizer ou d’un GrammarRecognizer</span><span class="sxs-lookup"><span data-stu-id="cc3f2-120">Specify which phrases to listen for using a KeywordRecognizer or GrammarRecognizer</span></span>
2. <span data-ttu-id="cc3f2-121">Gérer l’événement OnPhraseRecognized et entreprendre une action correspondant à l’expression reconnue</span><span class="sxs-lookup"><span data-stu-id="cc3f2-121">Handle the OnPhraseRecognized event and take action corresponding to the phrase recognized</span></span>

### <a name="keywordrecognizer"></a><span data-ttu-id="cc3f2-122">KeywordRecognizer</span><span class="sxs-lookup"><span data-stu-id="cc3f2-122">KeywordRecognizer</span></span>

<span data-ttu-id="cc3f2-123">**Espace de noms :** *UnityEngine. Windows. Speech*</span><span class="sxs-lookup"><span data-stu-id="cc3f2-123">**Namespace:** *UnityEngine.Windows.Speech*</span></span><br>
<span data-ttu-id="cc3f2-124">**Types :** *KeywordRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*</span><span class="sxs-lookup"><span data-stu-id="cc3f2-124">**Types:** *KeywordRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*</span></span>

<span data-ttu-id="cc3f2-125">Nous aurons besoin de quelques instructions d’utilisation pour enregistrer des séquences de touches :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-125">We'll need a few using statements to save some keystrokes:</span></span>

```
using UnityEngine.Windows.Speech;
using System.Collections.Generic;
using System.Linq;
```

<span data-ttu-id="cc3f2-126">Nous allons ensuite ajouter quelques champs à votre classe pour stocker le module de reconnaissance et de mot clé-> dictionnaire d’actions :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-126">Then let's add a few fields to your class to store the recognizer and keyword->action dictionary:</span></span>

```
KeywordRecognizer keywordRecognizer;
Dictionary<string, System.Action> keywords = new Dictionary<string, System.Action>();
```

<span data-ttu-id="cc3f2-127">Ajoutez maintenant un mot clé au dictionnaire (par exemple, à l’intérieur d’une méthode Start ()).</span><span class="sxs-lookup"><span data-stu-id="cc3f2-127">Now add a keyword to the dictionary (e.g. inside of a Start() method).</span></span> <span data-ttu-id="cc3f2-128">Nous ajoutons le mot clé « Activate » dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-128">We're adding the "activate" keyword in this example:</span></span>

```
//Create keywords for keyword recognizer
keywords.Add("activate", () =>
{
    // action to be performed when this keyword is spoken
});
```

<span data-ttu-id="cc3f2-129">Créez le module de reconnaissance de mot clé et dites-lui ce que nous souhaitons reconnaître :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-129">Create the keyword recognizer and tell it what we want to recognize:</span></span>

```
keywordRecognizer = new KeywordRecognizer(keywords.Keys.ToArray());
```

<span data-ttu-id="cc3f2-130">Inscrivez-vous maintenant à l’événement OnPhraseRecognized</span><span class="sxs-lookup"><span data-stu-id="cc3f2-130">Now register for the OnPhraseRecognized event</span></span>

```
keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
```

<span data-ttu-id="cc3f2-131">Voici un exemple de gestionnaire :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-131">An example handler is:</span></span>

```
private void KeywordRecognizer_OnPhraseRecognized(PhraseRecognizedEventArgs args)
{
    System.Action keywordAction;
    // if the keyword recognized is in our dictionary, call that Action.
    if (keywords.TryGetValue(args.text, out keywordAction))
    {
        keywordAction.Invoke();
    }
}
```

<span data-ttu-id="cc3f2-132">Enfin, commencez à reconnaître !</span><span class="sxs-lookup"><span data-stu-id="cc3f2-132">Finally, start recognizing!</span></span>

```
keywordRecognizer.Start();
```

### <a name="grammarrecognizer"></a><span data-ttu-id="cc3f2-133">GrammarRecognizer</span><span class="sxs-lookup"><span data-stu-id="cc3f2-133">GrammarRecognizer</span></span>

<span data-ttu-id="cc3f2-134">**Espace de noms :** *UnityEngine. Windows. Speech*</span><span class="sxs-lookup"><span data-stu-id="cc3f2-134">**Namespace:** *UnityEngine.Windows.Speech*</span></span><br>
<span data-ttu-id="cc3f2-135">**Types**: *GrammarRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*</span><span class="sxs-lookup"><span data-stu-id="cc3f2-135">**Types**: *GrammarRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*</span></span>

<span data-ttu-id="cc3f2-136">Le GrammarRecognizer est utilisé si vous spécifiez votre grammaire de reconnaissance à l’aide de SRGS.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-136">The GrammarRecognizer is used if you're specifying your recognition grammar using SRGS.</span></span> <span data-ttu-id="cc3f2-137">Cela peut être utile si votre application contient plus de seulement quelques mots-clés, si vous souhaitez reconnaître des expressions plus complexes ou si vous souhaitez facilement activer et désactiver des ensembles de commandes.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-137">This can be useful if your app has more than just a few keywords, if you want to recognize more complex phrases, or if you want to easily turn on and off sets of commands.</span></span> <span data-ttu-id="cc3f2-138">Voir : [créer des grammaires à l’aide de SRGS XML](https://msdn.microsoft.com/library/hh378349(v=office.14).aspx) pour les informations de format de fichier.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-138">See: [Create Grammars Using SRGS XML](https://msdn.microsoft.com/library/hh378349(v=office.14).aspx) for file format information.</span></span>

<span data-ttu-id="cc3f2-139">Une fois que vous disposez de la grammaire SRGS et que celle-ci se trouve dans votre projet dans un [dossier StreamingAssets](https://docs.unity3d.com/Manual/StreamingAssets.html):</span><span class="sxs-lookup"><span data-stu-id="cc3f2-139">Once you have your SRGS grammar, and it is in your project in a [StreamingAssets folder](https://docs.unity3d.com/Manual/StreamingAssets.html):</span></span>

```
<PROJECT_ROOT>/Assets/StreamingAssets/SRGS/myGrammar.xml
```

<span data-ttu-id="cc3f2-140">Créez un GrammarRecognizer et transmettez-lui le chemin d’accès à votre fichier SRGS :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-140">Create a GrammarRecognizer and pass it the path to your SRGS file:</span></span>

```
private GrammarRecognizer grammarRecognizer;
grammarRecognizer = new GrammarRecognizer(Application.streamingDataPath + "/SRGS/myGrammar.xml");
```

<span data-ttu-id="cc3f2-141">Inscrivez-vous maintenant à l’événement OnPhraseRecognized</span><span class="sxs-lookup"><span data-stu-id="cc3f2-141">Now register for the OnPhraseRecognized event</span></span>

```
grammarRecognizer.OnPhraseRecognized += grammarRecognizer_OnPhraseRecognized;
```

<span data-ttu-id="cc3f2-142">Vous recevrez un rappel contenant les informations spécifiées dans votre grammaire SRGS que vous pouvez gérer de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-142">You will get a callback containing information specified in your SRGS grammar which you can handle appropriately.</span></span> <span data-ttu-id="cc3f2-143">La plupart des informations importantes seront fournies dans le tableau semanticMeanings.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-143">Most of the important information will be provided in the semanticMeanings array.</span></span>

```
private void Grammar_OnPhraseRecognized(PhraseRecognizedEventArgs args)
{
    SemanticMeaning[] meanings = args.semanticMeanings;
    // do something
}
```

<span data-ttu-id="cc3f2-144">Enfin, commencez à reconnaître !</span><span class="sxs-lookup"><span data-stu-id="cc3f2-144">Finally, start recognizing!</span></span>

```
grammarRecognizer.Start();
```

## <a name="dictation"></a><span data-ttu-id="cc3f2-145">Dictée</span><span class="sxs-lookup"><span data-stu-id="cc3f2-145">Dictation</span></span>

<span data-ttu-id="cc3f2-146">**Espace de noms :** *UnityEngine. Windows. Speech*</span><span class="sxs-lookup"><span data-stu-id="cc3f2-146">**Namespace:** *UnityEngine.Windows.Speech*</span></span><br>
<span data-ttu-id="cc3f2-147">**Types**: *DictationRecognizer*, *SpeechError*, *SpeechSystemStatus*</span><span class="sxs-lookup"><span data-stu-id="cc3f2-147">**Types**: *DictationRecognizer*, *SpeechError*, *SpeechSystemStatus*</span></span>

<span data-ttu-id="cc3f2-148">Utilisez DictationRecognizer pour convertir la parole de l’utilisateur en texte.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-148">Use the DictationRecognizer to convert the user's speech to text.</span></span> <span data-ttu-id="cc3f2-149">Le DictationRecognizer expose les fonctionnalités de [dictée](voice-input.md#dictation) et prend en charge l’inscription et l’écoute des événements d’hypothèse et d’expression terminés, ce qui vous permet de fournir des commentaires à l’utilisateur pendant qu’il parle et par la suite.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-149">The DictationRecognizer exposes [dictation](voice-input.md#dictation) functionality and supports registering and listening for hypothesis and phrase completed events, so you can give feedback to your user both while they speak and afterwards.</span></span> <span data-ttu-id="cc3f2-150">Les méthodes Start () et Stop () respectivement activent et désactivent la reconnaissance de la dictée.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-150">Start() and Stop() methods respectively enable and disable dictation recognition.</span></span> <span data-ttu-id="cc3f2-151">Une fois le module de reconnaissance terminé, il doit être supprimé à l’aide de la méthode Dispose () pour libérer les ressources qu’il utilise.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-151">Once done with the recognizer, it should be disposed using Dispose() method to release the resources it uses.</span></span> <span data-ttu-id="cc3f2-152">Les ressources seront libérées automatiquement pendant la garbage collection à un coût de performances supplémentaire si elles ne sont pas libérées avant cela.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-152">It will release these resources automatically during garbage collection at an additional performance cost if they are not released prior to that.</span></span>

<span data-ttu-id="cc3f2-153">Il n’y a que quelques étapes nécessaires pour commencer à utiliser la dictée :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-153">There are only a few steps needed to get started with dictation:</span></span>
1. <span data-ttu-id="cc3f2-154">Créer un nouveau DictationRecognizer</span><span class="sxs-lookup"><span data-stu-id="cc3f2-154">Create a new DictationRecognizer</span></span>
2. <span data-ttu-id="cc3f2-155">Gérer les événements de dictée</span><span class="sxs-lookup"><span data-stu-id="cc3f2-155">Handle Dictation events</span></span>
3. <span data-ttu-id="cc3f2-156">Démarrer le DictationRecognizer</span><span class="sxs-lookup"><span data-stu-id="cc3f2-156">Start the DictationRecognizer</span></span>

### <a name="enabling-the-capability-for-dictation"></a><span data-ttu-id="cc3f2-157">Activation de la fonctionnalité de dictée</span><span class="sxs-lookup"><span data-stu-id="cc3f2-157">Enabling the capability for dictation</span></span>

<span data-ttu-id="cc3f2-158">La fonctionnalité « client Internet », en plus de la fonctionnalité « microphone » mentionnée ci-dessus, doit être déclarée pour qu’une application tire parti de la dictée.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-158">The "Internet Client" capability, in addition to the "Microphone" capability mentioned above, must be declared for an app to leverage dictation.</span></span>
1. <span data-ttu-id="cc3f2-159">Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à la page « modifier les paramètres du projet > > Player ».</span><span class="sxs-lookup"><span data-stu-id="cc3f2-159">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player" page</span></span>
2. <span data-ttu-id="cc3f2-160">Cliquer sur l’onglet « Windows Store »</span><span class="sxs-lookup"><span data-stu-id="cc3f2-160">Click on the "Windows Store" tab</span></span>
3. <span data-ttu-id="cc3f2-161">Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la capacité de **internetclient**</span><span class="sxs-lookup"><span data-stu-id="cc3f2-161">In the "Publishing Settings > Capabilities" section, check the **InternetClient** capability</span></span>

### <a name="dictationrecognizer"></a><span data-ttu-id="cc3f2-162">DictationRecognizer</span><span class="sxs-lookup"><span data-stu-id="cc3f2-162">DictationRecognizer</span></span>

<span data-ttu-id="cc3f2-163">Créez un DictationRecognizer de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-163">Create a DictationRecognizer like so:</span></span>

```
dictationRecognizer = new DictationRecognizer();
```

<span data-ttu-id="cc3f2-164">Quatre événements de dictée peuvent être souscrits et gérés pour implémenter le comportement de la dictée.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-164">There are four dictation events that can be subscribed to and handled to implement dictation behavior.</span></span>
1. <span data-ttu-id="cc3f2-165">DictationResult</span><span class="sxs-lookup"><span data-stu-id="cc3f2-165">DictationResult</span></span>
2. <span data-ttu-id="cc3f2-166">DictationComplete</span><span class="sxs-lookup"><span data-stu-id="cc3f2-166">DictationComplete</span></span>
3. <span data-ttu-id="cc3f2-167">DictationHypothesis</span><span class="sxs-lookup"><span data-stu-id="cc3f2-167">DictationHypothesis</span></span>
4. <span data-ttu-id="cc3f2-168">DictationError</span><span class="sxs-lookup"><span data-stu-id="cc3f2-168">DictationError</span></span>

<span data-ttu-id="cc3f2-169">**DictationResult**</span><span class="sxs-lookup"><span data-stu-id="cc3f2-169">**DictationResult**</span></span>

<span data-ttu-id="cc3f2-170">Cet événement est déclenché après la suspension de l’utilisateur, généralement à la fin d’une phrase.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-170">This event is fired after the user pauses, typically at the end of a sentence.</span></span> <span data-ttu-id="cc3f2-171">La chaîne complète reconnue est retournée ici.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-171">The full recognized string is returned here.</span></span>

<span data-ttu-id="cc3f2-172">Tout d’abord, abonnez-vous à l’événement DictationResult :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-172">First, subscribe to the DictationResult event:</span></span>

```
dictationRecognizer.DictationResult += DictationRecognizer_DictationResult;
```

<span data-ttu-id="cc3f2-173">Gérez ensuite le rappel DictationResult :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-173">Then handle the DictationResult callback:</span></span>

```
private void DictationRecognizer_DictationResult(string text, ConfidenceLevel confidence)
{
    // do something
}
```

<span data-ttu-id="cc3f2-174">**DictationHypothesis**</span><span class="sxs-lookup"><span data-stu-id="cc3f2-174">**DictationHypothesis**</span></span>

<span data-ttu-id="cc3f2-175">Cet événement est déclenché en continu pendant que l’utilisateur parle.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-175">This event is fired continuously while the user is talking.</span></span> <span data-ttu-id="cc3f2-176">À mesure que le module de reconnaissance écoute, il fournit du texte sur ce qu’il est entendu jusqu’à présent.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-176">As the recognizer listens, it provides text of what it's heard so far.</span></span>

<span data-ttu-id="cc3f2-177">Tout d’abord, abonnez-vous à l’événement DictationHypothesis :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-177">First, subscribe to the DictationHypothesis event:</span></span>

```
dictationRecognizer.DictationHypothesis += DictationRecognizer_DictationHypothesis;
```

<span data-ttu-id="cc3f2-178">Gérez ensuite le rappel DictationHypothesis :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-178">Then handle the DictationHypothesis callback:</span></span>

```
private void DictationRecognizer_DictationHypothesis(string text)
{
    // do something
}
```

<span data-ttu-id="cc3f2-179">**DictationComplete**</span><span class="sxs-lookup"><span data-stu-id="cc3f2-179">**DictationComplete**</span></span>

<span data-ttu-id="cc3f2-180">Cet événement est déclenché lorsque le module de reconnaissance s’arrête, qu’il s’agisse de l’appel de Stop (), d’un délai d’attente ou d’une autre erreur.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-180">This event is fired when the recognizer stops, whether from Stop() being called, a timeout occurring, or some other error.</span></span>

<span data-ttu-id="cc3f2-181">Tout d’abord, abonnez-vous à l’événement DictationComplete :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-181">First, subscribe to the DictationComplete event:</span></span>

```
dictationRecognizer.DictationComplete += DictationRecognizer_DictationComplete;
```

<span data-ttu-id="cc3f2-182">Gérez ensuite le rappel DictationComplete :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-182">Then handle the DictationComplete callback:</span></span>

```
private void DictationRecognizer_DictationComplete(DictationCompletionCause cause)
{
   // do something
}
```

<span data-ttu-id="cc3f2-183">**DictationError**</span><span class="sxs-lookup"><span data-stu-id="cc3f2-183">**DictationError**</span></span>

<span data-ttu-id="cc3f2-184">Cet événement est déclenché lorsqu’une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-184">This event is fired when an error occurs.</span></span>

<span data-ttu-id="cc3f2-185">Tout d’abord, abonnez-vous à l’événement DictationError :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-185">First, subscribe to the DictationError event:</span></span>

```
dictationRecognizer.DictationError += DictationRecognizer_DictationError;
```

<span data-ttu-id="cc3f2-186">Gérez ensuite le rappel DictationError :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-186">Then handle the DictationError callback:</span></span>

```
private void DictationRecognizer_DictationError(string error, int hresult)
{
    // do something
}
```

<span data-ttu-id="cc3f2-187">Une fois que vous avez souscrit et géré les événements de dictée qui vous intéressent, démarrez le module de reconnaissance de dictée pour commencer à recevoir des événements.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-187">Once you have subscribed and handled the dictation events that you care about, start the dictation recognizer to begin receiving events.</span></span>

```
dictationRecognizer.Start();
```

<span data-ttu-id="cc3f2-188">Si vous ne souhaitez plus conserver les DictationRecognizer, vous devez vous désabonner des événements et supprimer le DictationRecognizer.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-188">If you no longer want to keep the DictationRecognizer around, you need to unsubscribe from the events and Dispose the DictationRecognizer.</span></span>

```
dictationRecognizer.DictationResult -= DictationRecognizer_DictationResult;
dictationRecognizer.DictationComplete -= DictationRecognizer_DictationComplete ;
dictationRecognizer.DictationHypothesis -= DictationRecognizer_DictationHypothesis ;
dictationRecognizer.DictationError -= DictationRecognizer_DictationError ;
dictationRecognizer.Dispose();
```

<span data-ttu-id="cc3f2-189">**Conseil**</span><span class="sxs-lookup"><span data-stu-id="cc3f2-189">**Tips**</span></span>
* <span data-ttu-id="cc3f2-190">Les méthodes Start () et Stop () respectivement activent et désactivent la reconnaissance de la dictée.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-190">Start() and Stop() methods respectively enable and disable dictation recognition.</span></span>
* <span data-ttu-id="cc3f2-191">Une fois le module de reconnaissance terminé, il doit être supprimé à l’aide de la méthode Dispose () pour libérer les ressources qu’il utilise.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-191">Once done with the recognizer, it must be disposed using Dispose() method to release the resources it uses.</span></span> <span data-ttu-id="cc3f2-192">Les ressources seront libérées automatiquement pendant la garbage collection à un coût de performances supplémentaire si elles ne sont pas libérées avant cela.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-192">It will release these resources automatically during garbage collection at an additional performance cost if they are not released prior to that.</span></span>
* <span data-ttu-id="cc3f2-193">Les délais d’attente se produisent après un laps de temps défini.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-193">Timeouts occur after a set period of time.</span></span> <span data-ttu-id="cc3f2-194">Vous pouvez vérifier ces délais d’attente dans l’événement DictationComplete.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-194">You can check for these timeouts in the DictationComplete event.</span></span> <span data-ttu-id="cc3f2-195">Deux délais d’attente doivent être pris en compte :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-195">There are two timeouts to be aware of:</span></span>
   1. <span data-ttu-id="cc3f2-196">Si le module de reconnaissance démarre et n’entend aucun audio pendant les cinq premières secondes, il expire.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-196">If the recognizer starts and doesn't hear any audio for the first five seconds, it will timeout.</span></span>
   2. <span data-ttu-id="cc3f2-197">Si le module de reconnaissance a donné un résultat, mais émet un silence pendant vingt secondes, il expire.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-197">If the recognizer has given a result but then hears silence for twenty seconds, it will timeout.</span></span>

## <a name="using-both-phrase-recognition-and-dictation"></a><span data-ttu-id="cc3f2-198">Utilisation de la reconnaissance et de la dictée des expressions</span><span class="sxs-lookup"><span data-stu-id="cc3f2-198">Using both Phrase Recognition and Dictation</span></span>

<span data-ttu-id="cc3f2-199">Si vous souhaitez utiliser la reconnaissance d’expression et la dictée dans votre application, vous devez l’arrêter complètement avant de pouvoir démarrer l’autre.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-199">If you want to use both phrase recognition and dictation in your app, you'll need to fully shut one down before you can start the other.</span></span> <span data-ttu-id="cc3f2-200">Si vous avez plusieurs KeywordRecognizers en cours d’exécution, vous pouvez les arrêter en même temps avec :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-200">If you have multiple KeywordRecognizers running, you can shut them all down at once with:</span></span>

```
PhraseRecognitionSystem.Shutdown();
```

<span data-ttu-id="cc3f2-201">Pour restaurer tous les reconnaisseurs à leur état précédent, après l’arrêt du DictationRecognizer, vous pouvez appeler :</span><span class="sxs-lookup"><span data-stu-id="cc3f2-201">In order to restore all recognizers to their previous state, after the DictationRecognizer has stopped, you can call:</span></span>

```
PhraseRecognitionSystem.Restart();
```

<span data-ttu-id="cc3f2-202">Vous pouvez aussi simplement démarrer un KeywordRecognizer, qui redémarrera également le PhraseRecognitionSystem.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-202">You could also just start a KeywordRecognizer, which will restart the PhraseRecognitionSystem as well.</span></span>

## <a name="using-the-microphone-helper"></a><span data-ttu-id="cc3f2-203">Utilisation du programme d’assistance du microphone</span><span class="sxs-lookup"><span data-stu-id="cc3f2-203">Using the microphone helper</span></span>

<span data-ttu-id="cc3f2-204">La boîte à outils de réalité mixte sur GitHub contient une classe d’assistance de microphone qui permet aux développeurs de savoir s’il existe un microphone utilisable sur le système.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-204">The Mixed Reality Toolkit on GitHub contains a microphone helper class to hint at developers if there is a usable microphone on the system.</span></span> <span data-ttu-id="cc3f2-205">Pour ce faire, il convient de vérifier s’il existe un microphone sur le système avant d’illustrer des indicateurs d’interaction vocale dans l’application.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-205">One use for it is where one would want to check if there is microphone on system before showing any speech interaction hints in the application.</span></span>

<span data-ttu-id="cc3f2-206">Le script d’assistance du microphone se trouve dans le [dossier entrées/scripts/utilitaires](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Utilities/MicrophoneHelper.cs).</span><span class="sxs-lookup"><span data-stu-id="cc3f2-206">The microphone helper script can be found in the [Input/Scripts/Utilities folder](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Utilities/MicrophoneHelper.cs).</span></span> <span data-ttu-id="cc3f2-207">Le référentiel GitHub contient également un [petit exemple](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scripts/MicrophoneHelperSample.cs) illustrant l’utilisation de l’application auxiliaire.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-207">The GitHub repo also contains a [small sample](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scripts/MicrophoneHelperSample.cs) demonstrating how to use the helper.</span></span>

## <a name="voice-input-in-mixed-reality-toolkit"></a><span data-ttu-id="cc3f2-208">Entrée vocale dans le Toolkit de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="cc3f2-208">Voice input in Mixed Reality Toolkit</span></span>
<span data-ttu-id="cc3f2-209">Vous trouverez les exemples de l’entrée vocale dans cette scène.</span><span class="sxs-lookup"><span data-stu-id="cc3f2-209">You can find the examples of the voice input in this scene.</span></span>

- [<span data-ttu-id="cc3f2-210">HoloToolkit-Examples/entrée/scènes/SpeechInputSource. Unity</span><span class="sxs-lookup"><span data-stu-id="cc3f2-210">HoloToolkit-Examples/Input/Scenes/SpeechInputSource.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scenes/SpeechInputSource.unity)
