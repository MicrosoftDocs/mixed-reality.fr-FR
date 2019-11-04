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
# <a name="voice-input-in-unity"></a>Entrée vocale dans Unity

>[!NOTE]
>Au lieu d’utiliser les informations ci-dessous, envisagez d’utiliser le plug-in Unity pour le kit de développement logiciel (SDK) cognitive Speech services qui offre de meilleurs résultats de précision vocale et fournit un accès facile au décodage vocal en texte et à des fonctionnalités vocales avancées telles que la boîte de dialogue, intentionnellement interaction, traduction, synthèse vocale et reconnaissance vocale en langage naturel. Recherchez l’exemple et documentation ici : https://docs.microsoft.com//azure/cognitive-services/speech-service/quickstart-csharp-unity   

Unity expose trois façons d’ajouter une [entrée vocale](voice-input.md) à votre application Unity.

Avec KeywordRecognizer (l’un des deux types de PhraseRecognizers), votre application peut recevoir un tableau de commandes de chaîne à écouter. Avec GrammarRecognizer (l’autre type de PhraseRecognizer), votre application peut recevoir un fichier SRGS définissant une grammaire spécifique à écouter. Avec DictationRecognizer, votre application peut écouter tout mot et fournir à l’utilisateur une note ou un autre affichage de sa parole.

>[!NOTE]
>Seule la reconnaissance de la dictée ou de l’expression peut être gérée à la fois. Cela signifie que si un GrammarRecognizer ou un KeywordRecognizer est actif, un DictationRecognizer ne peut pas être actif et vice versa.

## <a name="enabling-the-capability-for-voice"></a>Activation de la fonctionnalité de voix

La fonctionnalité **microphone** doit être déclarée pour qu’une application tire parti de l’entrée vocale.
1. Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à « modifier les paramètres du projet > > Player ».
2. Cliquer sur l’onglet « Windows Store »
3. Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la fonctionnalité du **microphone** .

## <a name="phrase-recognition"></a>Reconnaissance d’expressions

Pour permettre à votre application d’écouter des expressions spécifiques parlées par l’utilisateur, puis de prendre des mesures, vous devez :
1. Spécifier les expressions à écouter à l’aide d’un KeywordRecognizer ou d’un GrammarRecognizer
2. Gérer l’événement OnPhraseRecognized et entreprendre une action correspondant à l’expression reconnue

### <a name="keywordrecognizer"></a>KeywordRecognizer

**Espace de noms :** *UnityEngine. Windows. Speech*<br>
**Types :** *KeywordRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*

Nous aurons besoin de quelques instructions d’utilisation pour enregistrer des séquences de touches :

```
using UnityEngine.Windows.Speech;
using System.Collections.Generic;
using System.Linq;
```

Nous allons ensuite ajouter quelques champs à votre classe pour stocker le module de reconnaissance et de mot clé-> dictionnaire d’actions :

```
KeywordRecognizer keywordRecognizer;
Dictionary<string, System.Action> keywords = new Dictionary<string, System.Action>();
```

Ajoutez maintenant un mot clé au dictionnaire (par exemple, à l’intérieur d’une méthode Start ()). Nous ajoutons le mot clé « Activate » dans cet exemple :

```
//Create keywords for keyword recognizer
keywords.Add("activate", () =>
{
    // action to be performed when this keyword is spoken
});
```

Créez le module de reconnaissance de mot clé et dites-lui ce que nous souhaitons reconnaître :

```
keywordRecognizer = new KeywordRecognizer(keywords.Keys.ToArray());
```

Inscrivez-vous maintenant à l’événement OnPhraseRecognized

```
keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
```

Voici un exemple de gestionnaire :

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

Enfin, commencez à reconnaître !

```
keywordRecognizer.Start();
```

### <a name="grammarrecognizer"></a>GrammarRecognizer

**Espace de noms :** *UnityEngine. Windows. Speech*<br>
**Types**: *GrammarRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*

Le GrammarRecognizer est utilisé si vous spécifiez votre grammaire de reconnaissance à l’aide de SRGS. Cela peut être utile si votre application contient plus de seulement quelques mots-clés, si vous souhaitez reconnaître des expressions plus complexes ou si vous souhaitez facilement activer et désactiver des ensembles de commandes. Voir : [créer des grammaires à l’aide de SRGS XML](https://msdn.microsoft.com/library/hh378349(v=office.14).aspx) pour les informations de format de fichier.

Une fois que vous disposez de la grammaire SRGS et que celle-ci se trouve dans votre projet dans un [dossier StreamingAssets](https://docs.unity3d.com/Manual/StreamingAssets.html):

```
<PROJECT_ROOT>/Assets/StreamingAssets/SRGS/myGrammar.xml
```

Créez un GrammarRecognizer et transmettez-lui le chemin d’accès à votre fichier SRGS :

```
private GrammarRecognizer grammarRecognizer;
grammarRecognizer = new GrammarRecognizer(Application.streamingDataPath + "/SRGS/myGrammar.xml");
```

Inscrivez-vous maintenant à l’événement OnPhraseRecognized

```
grammarRecognizer.OnPhraseRecognized += grammarRecognizer_OnPhraseRecognized;
```

Vous recevrez un rappel contenant les informations spécifiées dans votre grammaire SRGS que vous pouvez gérer de manière appropriée. La plupart des informations importantes seront fournies dans le tableau semanticMeanings.

```
private void Grammar_OnPhraseRecognized(PhraseRecognizedEventArgs args)
{
    SemanticMeaning[] meanings = args.semanticMeanings;
    // do something
}
```

Enfin, commencez à reconnaître !

```
grammarRecognizer.Start();
```

## <a name="dictation"></a>Dictée

**Espace de noms :** *UnityEngine. Windows. Speech*<br>
**Types**: *DictationRecognizer*, *SpeechError*, *SpeechSystemStatus*

Utilisez DictationRecognizer pour convertir la parole de l’utilisateur en texte. Le DictationRecognizer expose les fonctionnalités de [dictée](voice-input.md#dictation) et prend en charge l’inscription et l’écoute des événements d’hypothèse et d’expression terminés, ce qui vous permet de fournir des commentaires à l’utilisateur pendant qu’il parle et par la suite. Les méthodes Start () et Stop () respectivement activent et désactivent la reconnaissance de la dictée. Une fois le module de reconnaissance terminé, il doit être supprimé à l’aide de la méthode Dispose () pour libérer les ressources qu’il utilise. Les ressources seront libérées automatiquement pendant la garbage collection à un coût de performances supplémentaire si elles ne sont pas libérées avant cela.

Il n’y a que quelques étapes nécessaires pour commencer à utiliser la dictée :
1. Créer un nouveau DictationRecognizer
2. Gérer les événements de dictée
3. Démarrer le DictationRecognizer

### <a name="enabling-the-capability-for-dictation"></a>Activation de la fonctionnalité de dictée

La fonctionnalité « client Internet », en plus de la fonctionnalité « microphone » mentionnée ci-dessus, doit être déclarée pour qu’une application tire parti de la dictée.
1. Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à la page « modifier les paramètres du projet > > Player ».
2. Cliquer sur l’onglet « Windows Store »
3. Dans la section « fonctionnalités de > des paramètres de publication », vérifiez la capacité de **internetclient**

### <a name="dictationrecognizer"></a>DictationRecognizer

Créez un DictationRecognizer de la manière suivante :

```
dictationRecognizer = new DictationRecognizer();
```

Quatre événements de dictée peuvent être souscrits et gérés pour implémenter le comportement de la dictée.
1. DictationResult
2. DictationComplete
3. DictationHypothesis
4. DictationError

**DictationResult**

Cet événement est déclenché après la suspension de l’utilisateur, généralement à la fin d’une phrase. La chaîne complète reconnue est retournée ici.

Tout d’abord, abonnez-vous à l’événement DictationResult :

```
dictationRecognizer.DictationResult += DictationRecognizer_DictationResult;
```

Gérez ensuite le rappel DictationResult :

```
private void DictationRecognizer_DictationResult(string text, ConfidenceLevel confidence)
{
    // do something
}
```

**DictationHypothesis**

Cet événement est déclenché en continu pendant que l’utilisateur parle. À mesure que le module de reconnaissance écoute, il fournit du texte sur ce qu’il est entendu jusqu’à présent.

Tout d’abord, abonnez-vous à l’événement DictationHypothesis :

```
dictationRecognizer.DictationHypothesis += DictationRecognizer_DictationHypothesis;
```

Gérez ensuite le rappel DictationHypothesis :

```
private void DictationRecognizer_DictationHypothesis(string text)
{
    // do something
}
```

**DictationComplete**

Cet événement est déclenché lorsque le module de reconnaissance s’arrête, qu’il s’agisse de l’appel de Stop (), d’un délai d’attente ou d’une autre erreur.

Tout d’abord, abonnez-vous à l’événement DictationComplete :

```
dictationRecognizer.DictationComplete += DictationRecognizer_DictationComplete;
```

Gérez ensuite le rappel DictationComplete :

```
private void DictationRecognizer_DictationComplete(DictationCompletionCause cause)
{
   // do something
}
```

**DictationError**

Cet événement est déclenché lorsqu’une erreur se produit.

Tout d’abord, abonnez-vous à l’événement DictationError :

```
dictationRecognizer.DictationError += DictationRecognizer_DictationError;
```

Gérez ensuite le rappel DictationError :

```
private void DictationRecognizer_DictationError(string error, int hresult)
{
    // do something
}
```

Une fois que vous avez souscrit et géré les événements de dictée qui vous intéressent, démarrez le module de reconnaissance de dictée pour commencer à recevoir des événements.

```
dictationRecognizer.Start();
```

Si vous ne souhaitez plus conserver les DictationRecognizer, vous devez vous désabonner des événements et supprimer le DictationRecognizer.

```
dictationRecognizer.DictationResult -= DictationRecognizer_DictationResult;
dictationRecognizer.DictationComplete -= DictationRecognizer_DictationComplete ;
dictationRecognizer.DictationHypothesis -= DictationRecognizer_DictationHypothesis ;
dictationRecognizer.DictationError -= DictationRecognizer_DictationError ;
dictationRecognizer.Dispose();
```

**Conseil**
* Les méthodes Start () et Stop () respectivement activent et désactivent la reconnaissance de la dictée.
* Une fois le module de reconnaissance terminé, il doit être supprimé à l’aide de la méthode Dispose () pour libérer les ressources qu’il utilise. Les ressources seront libérées automatiquement pendant la garbage collection à un coût de performances supplémentaire si elles ne sont pas libérées avant cela.
* Les délais d’attente se produisent après un laps de temps défini. Vous pouvez vérifier ces délais d’attente dans l’événement DictationComplete. Deux délais d’attente doivent être pris en compte :
   1. Si le module de reconnaissance démarre et n’entend aucun audio pendant les cinq premières secondes, il expire.
   2. Si le module de reconnaissance a donné un résultat, mais émet un silence pendant vingt secondes, il expire.

## <a name="using-both-phrase-recognition-and-dictation"></a>Utilisation de la reconnaissance et de la dictée des expressions

Si vous souhaitez utiliser la reconnaissance d’expression et la dictée dans votre application, vous devez l’arrêter complètement avant de pouvoir démarrer l’autre. Si vous avez plusieurs KeywordRecognizers en cours d’exécution, vous pouvez les arrêter en même temps avec :

```
PhraseRecognitionSystem.Shutdown();
```

Pour restaurer tous les reconnaisseurs à leur état précédent, après l’arrêt du DictationRecognizer, vous pouvez appeler :

```
PhraseRecognitionSystem.Restart();
```

Vous pouvez aussi simplement démarrer un KeywordRecognizer, qui redémarrera également le PhraseRecognitionSystem.

## <a name="using-the-microphone-helper"></a>Utilisation du programme d’assistance du microphone

La boîte à outils de réalité mixte sur GitHub contient une classe d’assistance de microphone qui permet aux développeurs de savoir s’il existe un microphone utilisable sur le système. Pour ce faire, il convient de vérifier s’il existe un microphone sur le système avant d’illustrer des indicateurs d’interaction vocale dans l’application.

Le script d’assistance du microphone se trouve dans le [dossier entrées/scripts/utilitaires](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Utilities/MicrophoneHelper.cs). Le référentiel GitHub contient également un [petit exemple](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scripts/MicrophoneHelperSample.cs) illustrant l’utilisation de l’application auxiliaire.

## <a name="voice-input-in-mixed-reality-toolkit"></a>Entrée vocale dans le Toolkit de réalité mixte
Vous trouverez les exemples de l’entrée vocale dans cette scène.

- [HoloToolkit-Examples/entrée/scènes/SpeechInputSource. Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scenes/SpeechInputSource.unity)
