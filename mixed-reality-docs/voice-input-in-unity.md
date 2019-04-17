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
# <a name="voice-input-in-unity"></a>Entrée vocale dans Unity

Unity expose trois façons d’ajouter [entrée voix](voice-input.md) à votre application Unity.

Avec KeywordRecognizer (un des deux types de PhraseRecognizers), votre application peut recevoir un tableau de commandes de chaîne pour écouter. Avec le GrammarRecognizer (l’autre type de PhraseRecognizer), votre application peut recevoir un fichier SRGS définissant une syntaxe spécifique pour écouter. Avec la DictationRecognizer, votre application peut écouter tout mot et permettre aux utilisateurs une note ou un autre écran de leur voix.

>[!NOTE]
>Uniquement la dictée ou la reconnaissance de phrase peut être gérée en même temps. Cela signifie que si le GrammarRecognizer ou KeywordRecognizer est active, un DictationRecognizer ne peut pas être active et vice versa.

## <a name="enabling-the-capability-for-voice"></a>L’activation de la fonctionnalité de voix

Le **Microphone** fonctionnalité doit être déclarée pour une application tirer parti d’entrée vocale.
1. Dans l’éditeur Unity, accédez aux paramètres player en accédant à « Modifier > projet Paramètres > Player »
2. Cliquez sur l’onglet « Windows Store »
3. Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **Microphone** fonctionnalité

## <a name="phrase-recognition"></a>Reconnaissance de phrase

Pour activer votre application écouter les spécifiques phrases prononcées par l’utilisateur, puis prennent des mesures, vous devez :
1. Spécifiez les expressions pour écouter à l’aide d’un KeywordRecognizer ou le GrammarRecognizer
2. Gérer l’événement OnPhraseRecognized et prendre des mesures correspondant à l’expression reconnue

### <a name="keywordrecognizer"></a>KeywordRecognizer

**Namespace :** *UnityEngine.Windows.Speech*<br>
**Types :** *KeywordRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*

Nous avons besoin de quelques instructions using pour enregistrer quelques séquences de touches :

```
using UnityEngine.Windows.Speech;
using System.Collections.Generic;
using System.Linq;
```

Puis nous allons ajouter quelques champs à votre classe pour stocker le mot clé et le module de reconnaissance -> dictionnaire de l’action :

```
KeywordRecognizer keywordRecognizer;
Dictionary<string, System.Action> keywords = new Dictionary<string, System.Action>();
```

Ajoutez maintenant un mot clé au dictionnaire (par exemple, à l’intérieur d’une méthode Start()). Nous ajoutons le mot clé « activer » dans cet exemple :

```
//Create keywords for keyword recognizer
keywords.Add("activate", () =>
{
    // action to be performed when this keyword is spoken
});
```

Créer le module de reconnaissance du mot clé et lui indiquer ce que nous souhaitons reconnaître :

```
keywordRecognizer = new KeywordRecognizer(keywords.Keys.ToArray());
```

Désormais s’inscrire pour l’événement OnPhraseRecognized

```
keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
```

Un exemple de gestionnaire est :

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

Enfin, commence la reconnaissance !

```
keywordRecognizer.Start();
```

### <a name="grammarrecognizer"></a>GrammarRecognizer

**Namespace :** *UnityEngine.Windows.Speech*<br>
**Types**: *GrammarRecognizer*, *PhraseRecognizedEventArgs*, *SpeechError*, *SpeechSystemStatus*

Le GrammarRecognizer est utilisé si vous spécifiez votre syntaxe de reconnaissance à l’aide de SRGS. Cela peut être utile si votre application possède plus de quelques mots clés, si vous souhaitez reconnaître des expressions plus complexes, ou si vous voulez facilement activer et désactiver les jeux de commandes. Consultez : [Créer du code XML SRGS à l’aide des grammaires](https://msdn.microsoft.com/library/hh378349(v=office.14).aspx) des informations de format de fichier.

Une fois que vous avez votre grammaire SRGS, et il se trouve dans votre projet dans un [StreamingAssets dossier](http://docs.unity3d.com/Manual/StreamingAssets.html):

```
<PROJECT_ROOT>/Assets/StreamingAssets/SRGS/myGrammar.xml
```

Créer un GrammarRecognizer et lui transmettre le chemin d’accès à votre fichier SRGS :

```
private GrammarRecognizer grammarRecognizer;
grammarRecognizer = new GrammarRecognizer(Application.streamingDataPath + "/SRGS/myGrammar.xml");
```

Désormais s’inscrire pour l’événement OnPhraseRecognized

```
grammarRecognizer.OnPhraseRecognized += grammarRecognizer_OnPhraseRecognized;
```

Vous obtiendrez un rappel contenant les informations spécifiées dans votre grammaire SRGS que vous pouvez gérer de manière appropriée. Vous trouverez la plupart des informations importantes dans le tableau semanticMeanings.

```
private void Grammar_OnPhraseRecognized(PhraseRecognizedEventArgs args)
{
    SemanticMeaning[] meanings = args.semanticMeanings;
    // do something
}
```

Enfin, commence la reconnaissance !

```
grammarRecognizer.Start();
```

## <a name="dictation"></a>Dictée

**Namespace :** *UnityEngine.Windows.Speech*<br>
**Types**: *DictationRecognizer*, *SpeechError*, *SpeechSystemStatus*

Utilisez le DictationRecognizer pour convertir les voix de l’utilisateur en texte. Expose le DictationRecognizer [dictée](voice-input.md#dictation) fonctionnalité et prend en charge l’inscription et à l’écoute pour hypothèse et une phrase terminée événements, vous pouvez donner à vos commentaires à votre utilisateur alors que leur manière de parler et par la suite. Méthodes Start() et Stop() respectivement activer et désactiver la reconnaissance de dictée. Une fois le module de reconnaissance, il doit être supprimé à l’aide de la méthode Dispose() pour libérer les ressources qu’il utilise. Il publiera ces ressources automatiquement pendant le garbage collection pour un coût de performances supplémentaires si elles ne sont pas libérées avant cela.

Il existe quelques étapes nécessaires pour la prise en main la dictée :
1. Créer un nouveau DictationRecognizer
2. Gérer les événements de la dictée
3. Démarrer le DictationRecognizer

### <a name="enabling-the-capability-for-dictation"></a>L’activation de la fonction pour la dictée

La fonctionnalité « Internet Client », ainsi que la fonction « Microphone » mentionnée ci-dessus, doit être déclarée pour une application tirer parti de la dictée.
1. Dans l’éditeur Unity, accédez aux paramètres de lecteur en accédant à la page « Modifier > projet Paramètres > lecteur »
2. Cliquez sur l’onglet « Windows Store »
3. Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **InternetClient** fonctionnalité

### <a name="dictationrecognizer"></a>DictationRecognizer

Créer un DictationRecognizer comme suit :

```
dictationRecognizer = new DictationRecognizer();
```

Il existe quatre événements dictée qui peuvent être abonnés à et gérés pour implémenter le comportement de dictée.
1. DictationResult
2. DictationComplete
3. DictationHypothesis
4. DictationError

**DictationResult**

Cet événement est déclenché lorsque l’utilisateur met en pause, généralement à la fin d’une phrase. La version complète reconnu la chaîne est retournée ici.

Tout d’abord, abonnez-vous à l’événement DictationResult :

```
dictationRecognizer.DictationResult += DictationRecognizer_DictationResult;
```

Ensuite gérer le rappel DictationResult :

```
private void DictationRecognizer_DictationResult(string text, ConfidenceLevel confidence)
{
    // do something
}
```

**DictationHypothesis**

Cet événement est déclenché en continu pendant communique avec l’utilisateur. Comme le module de reconnaissance est à l’écoute, il fournit le texte de ce qu’il est entendu jusqu'à présent.

Tout d’abord, abonnez-vous à l’événement DictationHypothesis :

```
dictationRecognizer.DictationHypothesis += DictationRecognizer_DictationHypothesis;
```

Ensuite gérer le rappel DictationHypothesis :

```
private void DictationRecognizer_DictationHypothesis(string text)
{
    // do something
}
```

**DictationComplete**

Cet événement est déclenché lorsque le module de reconnaissance s’arrête, à partir de Stop() est appelée, un délai d’expiration qui se produisent, ou une autre erreur.

Tout d’abord, abonnez-vous à l’événement DictationComplete :

```
dictationRecognizer.DictationComplete += DictationRecognizer_DictationComplete;
```

Ensuite gérer le rappel DictationComplete :

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

Ensuite gérer le rappel DictationError :

```
private void DictationRecognizer_DictationError(string error, int hresult)
{
    // do something
}
```

Une fois que vous avez inscrit et géré les événements de dictée qui vous intéressent, démarrez le module de reconnaissance de dictée pour commencer à recevoir des événements.

```
dictationRecognizer.Start();
```

Si vous souhaitez ne plus conserver le DictationRecognizer autour, vous devez annuler l’abonnement à partir des événements et de supprimer le DictationRecognizer.

```
dictationRecognizer.DictationResult -= DictationRecognizer_DictationResult;
dictationRecognizer.DictationComplete -= DictationRecognizer_DictationComplete ;
dictationRecognizer.DictationHypothesis -= DictationRecognizer_DictationHypothesis ;
dictationRecognizer.DictationError -= DictationRecognizer_DictationError ;
dictationRecognizer.Dispose();
```

**Conseils**
* Méthodes Start() et Stop() respectivement activer et désactiver la reconnaissance de dictée.
* Une fois le module de reconnaissance, il doit être supprimée à l’aide de la méthode Dispose() pour libérer les ressources qu’il utilise. Il publiera ces ressources automatiquement pendant le garbage collection pour un coût de performances supplémentaires si elles ne sont pas libérées avant cela.
* Dépassement du délai après un laps de temps défini. Vous pouvez vérifier ces délais d’expiration dans l’événement DictationComplete. Il existe deux délais d’expiration à connaître :
   1. Si le module de reconnaissance commence et n’entendre des données audio pour les cinq premières secondes, elle dépassera le délai d’attente.
   2. Si le module de reconnaissance a donné un résultat mais puis entend silence pendant 20 secondes, elle dépassera le délai d’attente.

## <a name="using-both-phrase-recognition-and-dictation"></a>À l’aide de la reconnaissance de Phrase et la dictée

Si vous souhaitez utiliser la reconnaissance de phrase et la dictée dans votre application, vous devrez complètement arrêtés un avant de commencer à l’autre. Si vous avez plusieurs KeywordRecognizers en cours d’exécution, vous pouvez les arrêter tout à la fois avec :

```
PhraseRecognitionSystem.Shutdown();
```

Pour restaurer tous les modules de reconnaissance à leur état précédent, une fois le DictationRecognizer arrêté, vous pouvez appeler :

```
PhraseRecognitionSystem.Restart();
```

Vous pouvez aussi simplement commencer KeywordRecognizer, ce qui redémarrera le PhraseRecognitionSystem également.

## <a name="using-the-microphone-helper"></a>À l’aide de l’application d’assistance du microphone

La boîte à outils de réalité mixte sur GitHub contient une classe d’assistance de microphone pour cacher des développeurs s’il existe un microphone utilisable sur le système. Une utilisation pour qu’il est lorsque un ne souhaitez pas vérifier si microphone est sur le système avant d’afficher des indicateurs de l’interaction de n’importe quel discours dans l’application.

Vous trouverez le script d’assistance de microphone dans le [dossier d’entrée/Scripts/utilitaires](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/Utilities/MicrophoneHelper.cs). Le référentiel GitHub contient également un [petit échantillon](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scripts/MicrophoneHelperSample.cs) qui montre comment utiliser l’application d’assistance.

## <a name="voice-input-in-mixed-reality-toolkit"></a>Entrée vocale dans le Kit de ressources de réalité mixte
Vous pouvez trouver les exemples de l’entrée de la voix dans cette scène.

- [HoloToolkit-Examples/Input/Scenes/SpeechInputSource.unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scenes/SpeechInputSource.unity)
