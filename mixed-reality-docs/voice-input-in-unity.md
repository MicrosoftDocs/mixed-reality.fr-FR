---
title: Entrée vocale dans Unity
description: Unity expose trois façons d’ajouter l’entrée vocale à votre application Windows Mixed Reality.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Entrée vocale, KeywordRecognizer, GrammarRecognizer, microphone, la dictée, voix
ms.openlocfilehash: ef8114a1c877fe9b858122e0c64628d4b71a69cd
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597012"
---
# <a name="voice-input-in-unity"></a><span data-ttu-id="3ff08-104">Entrée vocale dans Unity</span><span class="sxs-lookup"><span data-stu-id="3ff08-104">Voice input in Unity</span></span>

<span data-ttu-id="3ff08-105">Unity expose trois façons d’ajouter [entrée voix](voice-input.md) à votre application Unity.</span><span class="sxs-lookup"><span data-stu-id="3ff08-105">Unity exposes three ways to add [Voice input](voice-input.md) to your Unity application.</span></span>

<span data-ttu-id="3ff08-106">Avec KeywordRecognizer (un des deux types de PhraseRecognizers), votre application peut recevoir un tableau de commandes de chaîne pour écouter.</span><span class="sxs-lookup"><span data-stu-id="3ff08-106">With the KeywordRecognizer (one of two types of PhraseRecognizers), your app can be given an array of string commands to listen for.</span></span> <span data-ttu-id="3ff08-107">Avec le GrammarRecognizer (l’autre type de PhraseRecognizer), votre application peut recevoir un fichier SRGS définissant une syntaxe spécifique pour écouter.</span><span class="sxs-lookup"><span data-stu-id="3ff08-107">With the GrammarRecognizer (the other type of PhraseRecognizer), your app can be given an SRGS file defining a specific grammar to listen for.</span></span> <span data-ttu-id="3ff08-108">Avec la DictationRecognizer, votre application peut écouter tout mot et permettre aux utilisateurs une note ou un autre écran de leur voix.</span><span class="sxs-lookup"><span data-stu-id="3ff08-108">With the DictationRecognizer, your app can listen for any word and provide the user with a note or other display of their speech.</span></span>

>[!NOTE]
><span data-ttu-id="3ff08-109">Uniquement la dictée ou la reconnaissance de phrase peut être gérée en même temps.</span><span class="sxs-lookup"><span data-stu-id="3ff08-109">Only dictation or phrase recognition can be handled at once.</span></span> <span data-ttu-id="3ff08-110">Cela signifie que si le GrammarRecognizer ou KeywordRecognizer est active, un DictationRecognizer ne peut pas être active et vice versa.</span><span class="sxs-lookup"><span data-stu-id="3ff08-110">That means if a GrammarRecognizer or KeywordRecognizer is active, a DictationRecognizer can not be active and vice versa.</span></span>

## <a name="enabling-the-capability-for-voice"></a><span data-ttu-id="3ff08-111">L’activation de la fonctionnalité de voix</span><span class="sxs-lookup"><span data-stu-id="3ff08-111">Enabling the capability for Voice</span></span>

<span data-ttu-id="3ff08-112">Le **Microphone** fonctionnalité doit être déclarée pour une application tirer parti d’entrée vocale.</span><span class="sxs-lookup"><span data-stu-id="3ff08-112">The **Microphone** capability must be declared for an app to leverage Voice input.</span></span>
1. <span data-ttu-id="3ff08-113">Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »</span><span class="sxs-lookup"><span data-stu-id="3ff08-113">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player"</span></span>
2. <span data-ttu-id="3ff08-114">Cliquez sur l’onglet « Windows Store »</span><span class="sxs-lookup"><span data-stu-id="3ff08-114">Click on the "Windows Store" tab</span></span>
3. <span data-ttu-id="3ff08-115">Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **Microphone** fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="3ff08-115">In the "Publishing Settings > Capabilities" section, check the **Microphone** capability</span></span>

## <a name="phrase-recognition"></a><span data-ttu-id="3ff08-116">Reconnaissance de phrase</span><span class="sxs-lookup"><span data-stu-id="3ff08-116">Phrase Recognition</span></span>

<span data-ttu-id="3ff08-117">Pour activer votre application écouter les spécifiques phrases prononcées par l’utilisateur, puis prennent des mesures, vous devez :</span><span class="sxs-lookup"><span data-stu-id="3ff08-117">To enable your app to listen for specific phrases spoken by the user then take some action, you need to:</span></span>
1. <span data-ttu-id="3ff08-118">Spécifiez les expressions pour écouter à l’aide d’un KeywordRecognizer ou le GrammarRecognizer</span><span class="sxs-lookup"><span data-stu-id="3ff08-118">Specify which phrases to listen for using a KeywordRecognizer or GrammarRecognizer</span></span>
2. <span data-ttu-id="3ff08-119">Gérer l’événement OnPhraseRecognized et prendre des mesures correspondant à l’expression reconnue</span><span class="sxs-lookup"><span data-stu-id="3ff08-119">Handle the OnPhraseRecognized event and take action corresponding to the phrase recognized</span></span>

### <a name="keywordrecognizer"></a><span data-ttu-id="3ff08-120">KeywordRecognizer</span><span class="sxs-lookup"><span data-stu-id="3ff08-120">KeywordRecognizer</span></span>

<span data-ttu-id="3ff08-121">**Namespace :** *UnityEngine.Windows.Speech*</span><span class="sxs-lookup"><span data-stu-id="3ff08-121">**Namespace:** *UnityEngine.Windows.Speech*</span></span><br>
<span data-ttu-id="3ff08-122">**Types :** *KeywordRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*</span><span class="sxs-lookup"><span data-stu-id="3ff08-122">**Types:** *KeywordRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*</span></span>

<span data-ttu-id="3ff08-123">Nous avons besoin de quelques instructions using pour enregistrer quelques séquences de touches :</span><span class="sxs-lookup"><span data-stu-id="3ff08-123">We'll need a few using statements to save some keystrokes:</span></span>

```
using UnityEngine.Windows.Speech;
using System.Collections.Generic;
using System.Linq;
```

<span data-ttu-id="3ff08-124">Puis nous allons ajouter quelques champs à votre classe pour stocker le mot clé et le module de reconnaissance -> dictionnaire de l’action :</span><span class="sxs-lookup"><span data-stu-id="3ff08-124">Then let's add a few fields to your class to store the recognizer and keyword->action dictionary:</span></span>

```
KeywordRecognizer keywordRecognizer;
Dictionary<string, System.Action> keywords = new Dictionary<string, System.Action>();
```

<span data-ttu-id="3ff08-125">Ajoutez maintenant un mot clé au dictionnaire (par exemple, à l’intérieur d’une méthode Start()).</span><span class="sxs-lookup"><span data-stu-id="3ff08-125">Now add a keyword to the dictionary (e.g. inside of a Start() method).</span></span> <span data-ttu-id="3ff08-126">Nous ajoutons le mot clé « activer » dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="3ff08-126">We're adding the "activate" keyword in this example:</span></span>

```
//Create keywords for keyword recognizer
keywords.Add("activate", () =>
{
    // action to be performed when this keyword is spoken
});
```

<span data-ttu-id="3ff08-127">Créer le module de reconnaissance du mot clé et lui indiquer ce que nous souhaitons reconnaître :</span><span class="sxs-lookup"><span data-stu-id="3ff08-127">Create the keyword recognizer and tell it what we want to recognize:</span></span>

```
keywordRecognizer = new KeywordRecognizer(keywords.Keys.ToArray());
```

<span data-ttu-id="3ff08-128">Désormais s’inscrire pour l’événement OnPhraseRecognized</span><span class="sxs-lookup"><span data-stu-id="3ff08-128">Now register for the OnPhraseRecognized event</span></span>

```
keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
```

<span data-ttu-id="3ff08-129">Un exemple de gestionnaire est :</span><span class="sxs-lookup"><span data-stu-id="3ff08-129">An example handler is:</span></span>

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

<span data-ttu-id="3ff08-130">Enfin, commence la reconnaissance !</span><span class="sxs-lookup"><span data-stu-id="3ff08-130">Finally, start recognizing!</span></span>

```
keywordRecognizer.Start();
```

### <a name="grammarrecognizer"></a><span data-ttu-id="3ff08-131">GrammarRecognizer</span><span class="sxs-lookup"><span data-stu-id="3ff08-131">GrammarRecognizer</span></span>

<span data-ttu-id="3ff08-132">**Namespace :** *UnityEngine.Windows.Speech*</span><span class="sxs-lookup"><span data-stu-id="3ff08-132">**Namespace:** *UnityEngine.Windows.Speech*</span></span><br>
<span data-ttu-id="3ff08-133">**Types**: *GrammarRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*</span><span class="sxs-lookup"><span data-stu-id="3ff08-133">**Types**: *GrammarRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*</span></span>

<span data-ttu-id="3ff08-134">Le GrammarRecognizer est utilisé si vous spécifiez votre syntaxe de reconnaissance à l’aide de SRGS.</span><span class="sxs-lookup"><span data-stu-id="3ff08-134">The GrammarRecognizer is used if you're specifying your recognition grammar using SRGS.</span></span> <span data-ttu-id="3ff08-135">Cela peut être utile si votre application possède plus de quelques mots clés, si vous souhaitez reconnaître des expressions plus complexes, ou si vous voulez facilement activer et désactiver les jeux de commandes.</span><span class="sxs-lookup"><span data-stu-id="3ff08-135">This can be useful if your app has more than just a few keywords, if you want to recognize more complex phrases, or if you want to easily turn on and off sets of commands.</span></span> <span data-ttu-id="3ff08-136">Consultez : [Créer du code XML SRGS à l’aide des grammaires](https://msdn.microsoft.com/library/hh378349(v=office.14).aspx) des informations de format de fichier.</span><span class="sxs-lookup"><span data-stu-id="3ff08-136">See: [Create Grammars Using SRGS XML](https://msdn.microsoft.com/library/hh378349(v=office.14).aspx) for file format information.</span></span>

<span data-ttu-id="3ff08-137">Une fois que vous avez votre grammaire SRGS, et il se trouve dans votre projet dans un [StreamingAssets dossier](http://docs.unity3d.com/Manual/StreamingAssets.html):</span><span class="sxs-lookup"><span data-stu-id="3ff08-137">Once you have your SRGS grammar, and it is in your project in a [StreamingAssets folder](http://docs.unity3d.com/Manual/StreamingAssets.html):</span></span>

```
<PROJECT_ROOT>/Assets/StreamingAssets/SRGS/myGrammar.xml
```

<span data-ttu-id="3ff08-138">Créer un GrammarRecognizer et lui transmettre le chemin d’accès à votre fichier SRGS :</span><span class="sxs-lookup"><span data-stu-id="3ff08-138">Create a GrammarRecognizer and pass it the path to your SRGS file:</span></span>

```
private GrammarRecognizer grammarRecognizer;
grammarRecognizer = new GrammarRecognizer(Application.streamingDataPath + "/SRGS/myGrammar.xml");
```

<span data-ttu-id="3ff08-139">Désormais s’inscrire pour l’événement OnPhraseRecognized</span><span class="sxs-lookup"><span data-stu-id="3ff08-139">Now register for the OnPhraseRecognized event</span></span>

```
grammarRecognizer.OnPhraseRecognized += grammarRecognizer_OnPhraseRecognized;
```

<span data-ttu-id="3ff08-140">Vous obtiendrez un rappel contenant les informations spécifiées dans votre grammaire SRGS que vous pouvez gérer de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="3ff08-140">You will get a callback containing information specified in your SRGS grammar which you can handle appropriately.</span></span> <span data-ttu-id="3ff08-141">Vous trouverez la plupart des informations importantes dans le tableau semanticMeanings.</span><span class="sxs-lookup"><span data-stu-id="3ff08-141">Most of the important information will be provided in the semanticMeanings array.</span></span>

```
private void Grammar_OnPhraseRecognized(PhraseRecognizedEventArgs args)
{
    SemanticMeaning[] meanings = args.semanticMeanings;
    // do something
}
```

<span data-ttu-id="3ff08-142">Enfin, commence la reconnaissance !</span><span class="sxs-lookup"><span data-stu-id="3ff08-142">Finally, start recognizing!</span></span>

```
grammarRecognizer.Start();
```

## <a name="dictation"></a><span data-ttu-id="3ff08-143">Dictée</span><span class="sxs-lookup"><span data-stu-id="3ff08-143">Dictation</span></span>

<span data-ttu-id="3ff08-144">**Namespace :** *UnityEngine.Windows.Speech*</span><span class="sxs-lookup"><span data-stu-id="3ff08-144">**Namespace:** *UnityEngine.Windows.Speech*</span></span><br>
<span data-ttu-id="3ff08-145">**Types**: *DictationRecognizer*, *SpeechError*, *SpeechSystemStatus*</span><span class="sxs-lookup"><span data-stu-id="3ff08-145">**Types**: *DictationRecognizer*, *SpeechError*, *SpeechSystemStatus*</span></span>

<span data-ttu-id="3ff08-146">Utilisez le DictationRecognizer pour convertir les voix de l’utilisateur en texte.</span><span class="sxs-lookup"><span data-stu-id="3ff08-146">Use the DictationRecognizer to convert the user's speech to text.</span></span> <span data-ttu-id="3ff08-147">Expose le DictationRecognizer [dictée](voice-input.md#dictation) fonctionnalité et prend en charge l’inscription et à l’écoute pour hypothèse et une phrase terminée événements, vous pouvez donner à vos commentaires à votre utilisateur alors que leur manière de parler et par la suite.</span><span class="sxs-lookup"><span data-stu-id="3ff08-147">The DictationRecognizer exposes [dictation](voice-input.md#dictation) functionality and supports registering and listening for hypothesis and phrase completed events, so you can give feedback to your user both while they speak and afterwards.</span></span> <span data-ttu-id="3ff08-148">Méthodes Start() et Stop() respectivement activer et désactiver la reconnaissance de dictée.</span><span class="sxs-lookup"><span data-stu-id="3ff08-148">Start() and Stop() methods respectively enable and disable dictation recognition.</span></span> <span data-ttu-id="3ff08-149">Une fois le module de reconnaissance, il doit être supprimé à l’aide de la méthode Dispose() pour libérer les ressources qu’il utilise.</span><span class="sxs-lookup"><span data-stu-id="3ff08-149">Once done with the recognizer, it should be disposed using Dispose() method to release the resources it uses.</span></span> <span data-ttu-id="3ff08-150">Il publiera ces ressources automatiquement pendant le garbage collection pour un coût de performances supplémentaires si elles ne sont pas libérées avant cela.</span><span class="sxs-lookup"><span data-stu-id="3ff08-150">It will release these resources automatically during garbage collection at an additional performance cost if they are not released prior to that.</span></span>

<span data-ttu-id="3ff08-151">Il existe quelques étapes nécessaires pour la prise en main la dictée :</span><span class="sxs-lookup"><span data-stu-id="3ff08-151">There are only a few steps needed to get started with dictation:</span></span>
1. <span data-ttu-id="3ff08-152">Créer un nouveau DictationRecognizer</span><span class="sxs-lookup"><span data-stu-id="3ff08-152">Create a new DictationRecognizer</span></span>
2. <span data-ttu-id="3ff08-153">Gérer les événements de la dictée</span><span class="sxs-lookup"><span data-stu-id="3ff08-153">Handle Dictation events</span></span>
3. <span data-ttu-id="3ff08-154">Démarrer le DictationRecognizer</span><span class="sxs-lookup"><span data-stu-id="3ff08-154">Start the DictationRecognizer</span></span>

### <a name="enabling-the-capability-for-dictation"></a><span data-ttu-id="3ff08-155">L’activation de la fonction pour la dictée</span><span class="sxs-lookup"><span data-stu-id="3ff08-155">Enabling the capability for dictation</span></span>

<span data-ttu-id="3ff08-156">La fonctionnalité « Internet Client », ainsi que la fonction « Microphone » mentionnée ci-dessus, doit être déclarée pour une application tirer parti de la dictée.</span><span class="sxs-lookup"><span data-stu-id="3ff08-156">The "Internet Client" capability, in addition to the "Microphone" capability mentioned above, must be declared for an app to leverage dictation.</span></span>
1. <span data-ttu-id="3ff08-157">Dans l’éditeur Unity, accédez aux paramètres de lecteur en accédant à la page « Modifier > projet Paramètres > lecteur »</span><span class="sxs-lookup"><span data-stu-id="3ff08-157">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player" page</span></span>
2. <span data-ttu-id="3ff08-158">Cliquez sur l’onglet « Windows Store »</span><span class="sxs-lookup"><span data-stu-id="3ff08-158">Click on the "Windows Store" tab</span></span>
3. <span data-ttu-id="3ff08-159">Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **InternetClient** fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="3ff08-159">In the "Publishing Settings > Capabilities" section, check the **InternetClient** capability</span></span>

### <a name="dictationrecognizer"></a><span data-ttu-id="3ff08-160">DictationRecognizer</span><span class="sxs-lookup"><span data-stu-id="3ff08-160">DictationRecognizer</span></span>

<span data-ttu-id="3ff08-161">Créer un DictationRecognizer comme suit :</span><span class="sxs-lookup"><span data-stu-id="3ff08-161">Create a DictationRecognizer like so:</span></span>

```
dictationRecognizer = new DictationRecognizer();
```

<span data-ttu-id="3ff08-162">Il existe quatre événements dictée qui peuvent être abonnés à et gérés pour implémenter le comportement de dictée.</span><span class="sxs-lookup"><span data-stu-id="3ff08-162">There are four dictation events that can be subscribed to and handled to implement dictation behavior.</span></span>
1. <span data-ttu-id="3ff08-163">DictationResult</span><span class="sxs-lookup"><span data-stu-id="3ff08-163">DictationResult</span></span>
2. <span data-ttu-id="3ff08-164">DictationComplete</span><span class="sxs-lookup"><span data-stu-id="3ff08-164">DictationComplete</span></span>
3. <span data-ttu-id="3ff08-165">DictationHypothesis</span><span class="sxs-lookup"><span data-stu-id="3ff08-165">DictationHypothesis</span></span>
4. <span data-ttu-id="3ff08-166">DictationError</span><span class="sxs-lookup"><span data-stu-id="3ff08-166">DictationError</span></span>

<span data-ttu-id="3ff08-167">**DictationResult**</span><span class="sxs-lookup"><span data-stu-id="3ff08-167">**DictationResult**</span></span>

<span data-ttu-id="3ff08-168">Cet événement est déclenché lorsque l’utilisateur met en pause, généralement à la fin d’une phrase.</span><span class="sxs-lookup"><span data-stu-id="3ff08-168">This event is fired after the user pauses, typically at the end of a sentence.</span></span> <span data-ttu-id="3ff08-169">La version complète reconnu la chaîne est retournée ici.</span><span class="sxs-lookup"><span data-stu-id="3ff08-169">The full recognized string is returned here.</span></span>

<span data-ttu-id="3ff08-170">Tout d’abord, abonnez-vous à l’événement DictationResult :</span><span class="sxs-lookup"><span data-stu-id="3ff08-170">First, subscribe to the DictationResult event:</span></span>

```
dictationRecognizer.DictationResult += DictationRecognizer_DictationResult;
```

<span data-ttu-id="3ff08-171">Ensuite gérer le rappel DictationResult :</span><span class="sxs-lookup"><span data-stu-id="3ff08-171">Then handle the DictationResult callback:</span></span>

```
private void DictationRecognizer_DictationResult(string text, ConfidenceLevel confidence)
{
    // do something
}
```

<span data-ttu-id="3ff08-172">**DictationHypothesis**</span><span class="sxs-lookup"><span data-stu-id="3ff08-172">**DictationHypothesis**</span></span>

<span data-ttu-id="3ff08-173">Cet événement est déclenché en continu pendant communique avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3ff08-173">This event is fired continuously while the user is talking.</span></span> <span data-ttu-id="3ff08-174">Comme le module de reconnaissance est à l’écoute, il fournit le texte de ce qu’il est entendu jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="3ff08-174">As the recognizer listens, it provides text of what it's heard so far.</span></span>

<span data-ttu-id="3ff08-175">Tout d’abord, abonnez-vous à l’événement DictationHypothesis :</span><span class="sxs-lookup"><span data-stu-id="3ff08-175">First, subscribe to the DictationHypothesis event:</span></span>

```
dictationRecognizer.DictationHypothesis += DictationRecognizer_DictationHypothesis;
```

<span data-ttu-id="3ff08-176">Ensuite gérer le rappel DictationHypothesis :</span><span class="sxs-lookup"><span data-stu-id="3ff08-176">Then handle the DictationHypothesis callback:</span></span>

```
private void DictationRecognizer_DictationHypothesis(string text)
{
    // do something
}
```

<span data-ttu-id="3ff08-177">**DictationComplete**</span><span class="sxs-lookup"><span data-stu-id="3ff08-177">**DictationComplete**</span></span>

<span data-ttu-id="3ff08-178">Cet événement est déclenché lorsque le module de reconnaissance s’arrête, à partir de Stop() est appelée, un délai d’expiration qui se produisent, ou une autre erreur.</span><span class="sxs-lookup"><span data-stu-id="3ff08-178">This event is fired when the recognizer stops, whether from Stop() being called, a timeout occurring, or some other error.</span></span>

<span data-ttu-id="3ff08-179">Tout d’abord, abonnez-vous à l’événement DictationComplete :</span><span class="sxs-lookup"><span data-stu-id="3ff08-179">First, subscribe to the DictationComplete event:</span></span>

```
dictationRecognizer.DictationComplete += DictationRecognizer_DictationComplete;
```

<span data-ttu-id="3ff08-180">Ensuite gérer le rappel DictationComplete :</span><span class="sxs-lookup"><span data-stu-id="3ff08-180">Then handle the DictationComplete callback:</span></span>

```
private void DictationRecognizer_DictationComplete(DictationCompletionCause cause)
{
   // do something
}
```

<span data-ttu-id="3ff08-181">**DictationError**</span><span class="sxs-lookup"><span data-stu-id="3ff08-181">**DictationError**</span></span>

<span data-ttu-id="3ff08-182">Cet événement est déclenché lorsqu’une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="3ff08-182">This event is fired when an error occurs.</span></span>

<span data-ttu-id="3ff08-183">Tout d’abord, abonnez-vous à l’événement DictationError :</span><span class="sxs-lookup"><span data-stu-id="3ff08-183">First, subscribe to the DictationError event:</span></span>

```
dictationRecognizer.DictationError += DictationRecognizer_DictationError;
```

<span data-ttu-id="3ff08-184">Ensuite gérer le rappel DictationError :</span><span class="sxs-lookup"><span data-stu-id="3ff08-184">Then handle the DictationError callback:</span></span>

```
private void DictationRecognizer_DictationError(string error, int hresult)
{
    // do something
}
```

<span data-ttu-id="3ff08-185">Une fois que vous avez inscrit et géré les événements de dictée qui vous intéressent, démarrez le module de reconnaissance de dictée pour commencer à recevoir des événements.</span><span class="sxs-lookup"><span data-stu-id="3ff08-185">Once you have subscribed and handled the dictation events that you care about, start the dictation recognizer to begin receiving events.</span></span>

```
dictationRecognizer.Start();
```

<span data-ttu-id="3ff08-186">Si vous souhaitez ne plus conserver le DictationRecognizer autour, vous devez annuler l’abonnement à partir des événements et de supprimer le DictationRecognizer.</span><span class="sxs-lookup"><span data-stu-id="3ff08-186">If you no longer want to keep the DictationRecognizer around, you need to unsubscribe from the events and Dispose the DictationRecognizer.</span></span>

```
dictationRecognizer.DictationResult -= DictationRecognizer_DictationResult;
dictationRecognizer.DictationComplete -= DictationRecognizer_DictationComplete ;
dictationRecognizer.DictationHypothesis -= DictationRecognizer_DictationHypothesis ;
dictationRecognizer.DictationError -= DictationRecognizer_DictationError ;
dictationRecognizer.Dispose();
```

<span data-ttu-id="3ff08-187">**Conseils**</span><span class="sxs-lookup"><span data-stu-id="3ff08-187">**Tips**</span></span>
* <span data-ttu-id="3ff08-188">Méthodes Start() et Stop() respectivement activer et désactiver la reconnaissance de dictée.</span><span class="sxs-lookup"><span data-stu-id="3ff08-188">Start() and Stop() methods respectively enable and disable dictation recognition.</span></span>
* <span data-ttu-id="3ff08-189">Une fois le module de reconnaissance, il doit être supprimée à l’aide de la méthode Dispose() pour libérer les ressources qu’il utilise.</span><span class="sxs-lookup"><span data-stu-id="3ff08-189">Once done with the recognizer, it must be disposed using Dispose() method to release the resources it uses.</span></span> <span data-ttu-id="3ff08-190">Il publiera ces ressources automatiquement pendant le garbage collection pour un coût de performances supplémentaires si elles ne sont pas libérées avant cela.</span><span class="sxs-lookup"><span data-stu-id="3ff08-190">It will release these resources automatically during garbage collection at an additional performance cost if they are not released prior to that.</span></span>
* <span data-ttu-id="3ff08-191">Dépassement du délai après un laps de temps défini.</span><span class="sxs-lookup"><span data-stu-id="3ff08-191">Timeouts occur after a set period of time.</span></span> <span data-ttu-id="3ff08-192">Vous pouvez vérifier ces délais d’expiration dans l’événement DictationComplete.</span><span class="sxs-lookup"><span data-stu-id="3ff08-192">You can check for these timeouts in the DictationComplete event.</span></span> <span data-ttu-id="3ff08-193">Il existe deux délais d’expiration à connaître :</span><span class="sxs-lookup"><span data-stu-id="3ff08-193">There are two timeouts to be aware of:</span></span>
   1. <span data-ttu-id="3ff08-194">Si le module de reconnaissance commence et n’entendre des données audio pour les cinq premières secondes, elle dépassera le délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="3ff08-194">If the recognizer starts and doesn't hear any audio for the first five seconds, it will timeout.</span></span>
   2. <span data-ttu-id="3ff08-195">Si le module de reconnaissance a donné un résultat mais puis entend silence pendant 20 secondes, elle dépassera le délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="3ff08-195">If the recognizer has given a result but then hears silence for twenty seconds, it will timeout.</span></span>

## <a name="using-both-phrase-recognition-and-dictation"></a><span data-ttu-id="3ff08-196">À l’aide de la reconnaissance de Phrase et la dictée</span><span class="sxs-lookup"><span data-stu-id="3ff08-196">Using both Phrase Recognition and Dictation</span></span>

<span data-ttu-id="3ff08-197">Si vous souhaitez utiliser la reconnaissance de phrase et la dictée dans votre application, vous devrez complètement arrêtés un avant de commencer à l’autre.</span><span class="sxs-lookup"><span data-stu-id="3ff08-197">If you want to use both phrase recognition and dictation in your app, you'll need to fully shut one down before you can start the other.</span></span> <span data-ttu-id="3ff08-198">Si vous avez plusieurs KeywordRecognizers en cours d’exécution, vous pouvez les arrêter tout à la fois avec :</span><span class="sxs-lookup"><span data-stu-id="3ff08-198">If you have multiple KeywordRecognizers running, you can shut them all down at once with:</span></span>

```
PhraseRecognitionSystem.Shutdown();
```

<span data-ttu-id="3ff08-199">Pour restaurer tous les modules de reconnaissance à leur état précédent, une fois le DictationRecognizer arrêté, vous pouvez appeler :</span><span class="sxs-lookup"><span data-stu-id="3ff08-199">In order to restore all recognizers to their previous state, after the DictationRecognizer has stopped, you can call:</span></span>

```
PhraseRecognitionSystem.Restart();
```

<span data-ttu-id="3ff08-200">Vous pouvez aussi simplement commencer KeywordRecognizer, ce qui redémarrera le PhraseRecognitionSystem également.</span><span class="sxs-lookup"><span data-stu-id="3ff08-200">You could also just start a KeywordRecognizer, which will restart the PhraseRecognitionSystem as well.</span></span>

## <a name="using-the-microphone-helper"></a><span data-ttu-id="3ff08-201">À l’aide de l’application d’assistance du microphone</span><span class="sxs-lookup"><span data-stu-id="3ff08-201">Using the microphone helper</span></span>

<span data-ttu-id="3ff08-202">La boîte à outils de réalité mixte sur GitHub contient une classe d’assistance de microphone pour cacher des développeurs s’il existe un microphone utilisable sur le système.</span><span class="sxs-lookup"><span data-stu-id="3ff08-202">The Mixed Reality Toolkit on GitHub contains a microphone helper class to hint at developers if there is a usable microphone on the system.</span></span> <span data-ttu-id="3ff08-203">Une utilisation pour qu’il est lorsque un ne souhaitez pas vérifier si microphone est sur le système avant d’afficher des indicateurs de l’interaction de n’importe quel discours dans l’application.</span><span class="sxs-lookup"><span data-stu-id="3ff08-203">One use for it is where one would want to check if there is microphone on system before showing any speech interaction hints in the application.</span></span>

<span data-ttu-id="3ff08-204">Vous trouverez le script d’assistance de microphone dans le [dossier d’entrée/Scripts/utilitaires](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Utilities/MicrophoneHelper.cs).</span><span class="sxs-lookup"><span data-stu-id="3ff08-204">The microphone helper script can be found in the [Input/Scripts/Utilities folder](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Utilities/MicrophoneHelper.cs).</span></span> <span data-ttu-id="3ff08-205">Le référentiel GitHub contient également un [petit échantillon](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scripts/MicrophoneHelperSample.cs) qui montre comment utiliser l’application d’assistance.</span><span class="sxs-lookup"><span data-stu-id="3ff08-205">The GitHub repo also contains a [small sample](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scripts/MicrophoneHelperSample.cs) demonstrating how to use the helper.</span></span>

## <a name="voice-input-in-mixed-reality-toolkit"></a><span data-ttu-id="3ff08-206">Entrée vocale dans le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="3ff08-206">Voice input in Mixed Reality Toolkit</span></span>
<span data-ttu-id="3ff08-207">Vous pouvez trouver les exemples de l’entrée de la voix dans cette scène.</span><span class="sxs-lookup"><span data-stu-id="3ff08-207">You can find the examples of the voice input in this scene.</span></span>

- [<span data-ttu-id="3ff08-208">HoloToolkit-Examples/Input/Scenes/SpeechInputSource.unity</span><span class="sxs-lookup"><span data-stu-id="3ff08-208">HoloToolkit-Examples/Input/Scenes/SpeechInputSource.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scenes/SpeechInputSource.unity)
