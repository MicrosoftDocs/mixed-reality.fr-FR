---
title: Entrée vocale dans DirectX
description: Explique comment implémenter des commandes vocales et une petite reconnaissance d’expressions et de phrases dans une application DirectX pour Windows Mixed Reality.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: procédure pas à pas, commande vocale, expression, reconnaissance, reconnaissance vocale, DirectX, plateforme, Cortana, Windows Mixed Reality
ms.openlocfilehash: 728457a495616e5f65ec3986dfb6ac60231f9e46
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63548660"
---
# <a name="voice-input-in-directx"></a>Entrée vocale dans DirectX

Cette rubrique explique comment implémenter des [commandes vocales](voice-input.md)et une petite reconnaissance d’expressions et de phrases dans une application DirectX pour Windows Mixed Reality.

>[!NOTE]
>Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).  Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.

## <a name="use-a-speechrecognizer-for-continuous-recognition-of-voice-commands"></a>Utiliser un SpeechRecognizer pour la reconnaissance continue des commandes vocales

Dans cette section, nous décrivons comment utiliser la reconnaissance vocale continue pour activer les commandes vocales dans votre application. Cette procédure pas à pas utilise le code de l’exemple [HolographicVoiceInput](http://go.microsoft.com/fwlink/p/?LinkId=844964) . Lorsque l’exemple est en cours d’exécution, parlez le nom de l’une des commandes de couleur inscrite pour modifier la couleur du cube en rotation.

Tout d’abord, créez une instance **Windows:: Media:: SpeechRecognition:: SpeechRecognizer** .

À partir de *HolographicVoiceInputSampleMain:: CreateSpeechConstraintsForCurrentState*:

```
m_speechRecognizer = ref new SpeechRecognizer();
```

Vous devez créer une liste de commandes vocales pour que le module de reconnaissance écoute. Ici, nous créons un ensemble de commandes pour modifier la couleur d’un hologramme. Par souci de commodité, nous créons également les données que nous utiliserons ultérieurement pour les commandes.

```
m_speechCommandList = ref new Platform::Collections::Vector<String^>();
   m_speechCommandData.clear();
   m_speechCommandList->Append(StringReference(L"white"));
   m_speechCommandData.push_back(float4(1.f, 1.f, 1.f, 1.f));
   m_speechCommandList->Append(StringReference(L"grey"));
   m_speechCommandData.push_back(float4(0.5f, 0.5f, 0.5f, 1.f));
   m_speechCommandList->Append(StringReference(L"green"));
   m_speechCommandData.push_back(float4(0.f, 1.f, 0.f, 1.f));
   m_speechCommandList->Append(StringReference(L"black"));
   m_speechCommandData.push_back(float4(0.1f, 0.1f, 0.1f, 1.f));
   m_speechCommandList->Append(StringReference(L"red"));
   m_speechCommandData.push_back(float4(1.f, 0.f, 0.f, 1.f));
   m_speechCommandList->Append(StringReference(L"yellow"));
   m_speechCommandData.push_back(float4(1.f, 1.f, 0.f, 1.f));
   m_speechCommandList->Append(StringReference(L"aquamarine"));
   m_speechCommandData.push_back(float4(0.f, 1.f, 1.f, 1.f));
   m_speechCommandList->Append(StringReference(L"blue"));
   m_speechCommandData.push_back(float4(0.f, 0.f, 1.f, 1.f));
   m_speechCommandList->Append(StringReference(L"purple"));
   m_speechCommandData.push_back(float4(1.f, 0.f, 1.f, 1.f));
```

Les commandes peuvent être spécifiées à l’aide de mots phonétiques qui ne se trouvent peut-être pas dans un dictionnaire:

```
m_speechCommandList->Append(StringReference(L"SpeechRecognizer"));
   m_speechCommandData.push_back(float4(0.5f, 0.1f, 1.f, 1.f));
```

La liste des commandes est chargée dans la liste des contraintes pour le module de reconnaissance vocale. Pour ce faire, utilisez un objet [SpeechRecognitionListConstraint](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionlistconstraint.aspx) .

```
SpeechRecognitionListConstraint^ spConstraint = ref new SpeechRecognitionListConstraint(m_speechCommandList);
   m_speechRecognizer->Constraints->Clear();
   m_speechRecognizer->Constraints->Append(spConstraint);
   create_task(m_speechRecognizer->CompileConstraintsAsync()).then([this](SpeechRecognitionCompilationResult^ compilationResult)
   {
       if (compilationResult->Status == SpeechRecognitionResultStatus::Success)
       {
           m_speechRecognizer->ContinuousRecognitionSession->StartAsync();
       }
       else
       {
           // Handle errors here.
       }
   });
```

Abonnez-vous à l’événement [ResultGenerated](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated.aspx) sur le [SpeechContinuousRecognitionSession](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.aspx)du module de reconnaissance vocale. Cet événement avertit votre application lorsque l’une de vos commandes a été reconnue.

```
m_speechRecognizer->ContinuousRecognitionSession->ResultGenerated +=
       ref new TypedEventHandler<SpeechContinuousRecognitionSession^, SpeechContinuousRecognitionResultGeneratedEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnResultGenerated, this, _1, _2)
           );
```

Votre gestionnaire d’événements **OnResultGenerated** reçoit les données d’événement dans une instance [SpeechContinuousRecognitionResultGeneratedEventArgs](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.aspx) . Si la confiance est supérieure au seuil que vous avez défini, votre application doit noter que l’événement s’est produit. Enregistrez les données d’événement afin de pouvoir les utiliser dans une boucle de mise à jour ultérieure.

À partir de *HolographicVoiceInputSampleMain. cpp*:

```
// Change the cube color, if we get a valid result.
   void HolographicVoiceInputSampleMain::OnResultGenerated(SpeechContinuousRecognitionSession ^sender, SpeechContinuousRecognitionResultGeneratedEventArgs ^args)
   {
       if (args->Result->RawConfidence > 0.5f)
       {
           m_lastCommand = args->Result->Text;
       }
   }
```

Utilisez les données toutefois applicables à votre scénario d’application. Dans notre exemple de code, nous modifions la couleur du cube d’hologramme en rotation en fonction de la commande de l’utilisateur.

À partir de *HolographicVoiceInputSampleMain:: Update*:

```
// Check for new speech input since the last frame.
   if (m_lastCommand != nullptr)
   {
       auto command = m_lastCommand;
       m_lastCommand = nullptr;

       int i = 0;
       for each (auto& iter in m_speechCommandList)
       {
           if (iter == command)
           {
               m_spinningCubeRenderer->SetColor(m_speechCommandData[i]);
               break;
           }

           ++i;
       }
   }
```

## <a name="use-dictation-for-one-shot-recognition-of-speech-phrases-and-sentences"></a>Utiliser la dictée pour la reconnaissance d’une seule capture d’expressions et de phrases vocales

Vous pouvez configurer un module de reconnaissance vocale pour écouter les expressions ou les phrases prononcées par l’utilisateur. Dans ce cas, nous appliquons un SpeechRecognitionTopicConstraint qui indique au module de reconnaissance vocale le type d’entrée à attendre. Le flux de travail de l’application est le suivant, pour ce type de cas d’usage:
1. Votre application crée le SpeechRecognizer, fournit des invites d’interface utilisateur et commence à écouter une commande qui est immédiatement parlée.
2. L’utilisateur parle une expression ou une phrase.
3. La reconnaissance de la parole de l’utilisateur est effectuée et un résultat est renvoyé à l’application. À ce stade, votre application doit fournir une invite d’interface utilisateur indiquant que la reconnaissance s’est produite.
4. Selon le niveau de confiance auquel vous souhaitez répondre et le niveau de confiance du résultat de la reconnaissance vocale, votre application peut traiter le résultat et répondre de manière appropriée.

Cette section décrit comment créer un SpeechRecognizer, compiler la contrainte et écouter les entrées vocales.

Le code suivant compile la contrainte de rubrique, qui, dans ce cas, est optimisée pour la recherche Web.

```
auto constraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, L"webSearch");
   m_speechRecognizer->Constraints->Clear();
   m_speechRecognizer->Constraints->Append(constraint);
   return create_task(m_speechRecognizer->CompileConstraintsAsync())
       .then([this](task<SpeechRecognitionCompilationResult^> previousTask)
   {
```

Si la compilation est réussie, nous pouvons continuer la reconnaissance vocale.

```
try
       {
           SpeechRecognitionCompilationResult^ compilationResult = previousTask.get();

           // Check to make sure that the constraints were in a proper format and the recognizer was able to compile it.
           if (compilationResult->Status == SpeechRecognitionResultStatus::Success)
           {
               // If the compilation succeeded, we can start listening for the user's spoken phrase or sentence.
               create_task(m_speechRecognizer->RecognizeAsync()).then([this](task<SpeechRecognitionResult^>& previousTask)
               {
```

Le résultat est ensuite renvoyé à l’application. Si nous sommes suffisamment sûrs dans le résultat, nous pouvons traiter la commande. Cet exemple de code traite les résultats avec au moins une confiance moyenne.

```
try
                   {
                       auto result = previousTask.get();

                       if (result->Status != SpeechRecognitionResultStatus::Success)
                       {
                           PrintWstringToDebugConsole(
                               std::wstring(L"Speech recognition was not successful: ") +
                               result->Status.ToString()->Data() +
                               L"\n"
                               );
                       }

                       // In this example, we look for at least medium confidence in the speech result.
                       if ((result->Confidence == SpeechRecognitionConfidence::High) ||
                           (result->Confidence == SpeechRecognitionConfidence::Medium))
                       {
                           // If the user said a color name anywhere in their phrase, it will be recognized in the
                           // Update loop; then, the cube will change color.
                           m_lastCommand = result->Text;

                           PrintWstringToDebugConsole(
                               std::wstring(L"Speech phrase was: ") +
                               m_lastCommand->Data() +
                               L"\n"
                               );
                       }
                       else
                       {
                           PrintWstringToDebugConsole(
                               std::wstring(L"Recognition confidence not high enough: ") +
                               result->Confidence.ToString()->Data() +
                               L"\n"
                               );
                       }
                   }
```

Chaque fois que vous utilisez la reconnaissance vocale, vous devez surveiller les exceptions qui peuvent indiquer que l’utilisateur a désactivé le microphone dans les paramètres de confidentialité du système. Cela peut se produire pendant l’initialisation ou pendant la reconnaissance.

```
catch (Exception^ exception)
                   {
                       // Note that if you get an "Access is denied" exception, you might need to enable the microphone
                       // privacy setting on the device and/or add the microphone capability to your app manifest.

                       PrintWstringToDebugConsole(
                           std::wstring(L"Speech recognizer error: ") +
                           exception->ToString()->Data() +
                           L"\n"
                           );
                   }
               });

               return true;
           }
           else
           {
               OutputDebugStringW(L"Could not initialize predefined grammar speech engine!\n");

               // Handle errors here.
               return false;
           }
       }
       catch (Exception^ exception)
       {
           // Note that if you get an "Access is denied" exception, you might need to enable the microphone
           // privacy setting on the device and/or add the microphone capability to your app manifest.

           PrintWstringToDebugConsole(
               std::wstring(L"Exception while trying to initialize predefined grammar speech engine:") +
               exception->Message->Data() +
               L"\n"
               );

           // Handle exceptions here.
           return false;
       }
   });
```

**REMARQUE :** Plusieurs [SpeechRecognitionScenarios](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionscenario.aspx) prédéfinis sont disponibles pour optimiser la reconnaissance vocale.
* Si vous souhaitez optimiser la dictée, utilisez le scénario de dictée:

```
// Compile the dictation topic constraint, which optimizes for speech dictation.
   auto dictationConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::Dictation, "dictation");
   m_speechRecognizer->Constraints->Append(dictationConstraint);
```
* Lorsque vous utilisez la reconnaissance vocale pour effectuer une recherche sur le Web, vous pouvez utiliser une contrainte de scénario spécifique au Web comme suit:

```
// Add a web search topic constraint to the recognizer.
   auto webSearchConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, "webSearch");
   speechRecognizer->Constraints->Append(webSearchConstraint);
```
* Utilisez la contrainte de formulaire pour remplir les formulaires. Dans ce cas, il est préférable d’appliquer votre propre grammaire qui est optimisée pour remplir votre formulaire.

```
// Add a form constraint to the recognizer.
   auto formConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::FormFilling, "formFilling");
   speechRecognizer->Constraints->Append(formConstraint );
```
* Vous pouvez fournir votre propre grammaire en utilisant le format SRGS.

## <a name="use-continuous-freeform-speech-dictation"></a>Utiliser la dictée continue et la reconnaissance vocale à main levée

Consultez l’exemple de code vocal Windows 10 UWP pour le scénario de dictée continue [ici.](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpeechRecognitionAndSynthesis/cpp/Scenario_ContinuousDictation.xaml.cpp)

## <a name="handle-degradation-in-quality"></a>Gérer la dégradation de la qualité

Les conditions de l’environnement peuvent parfois empêcher la reconnaissance vocale de fonctionner. Par exemple, la salle peut être trop bruyante ou l’utilisateur peut parler à un volume trop élevé. L’API reconnaissance vocale fournit des informations, dans la mesure du possible, sur les conditions qui ont provoqué une dégradation de la qualité.

Ces informations sont envoyées à votre application à l’aide d’un événement WinRT. Voici un exemple qui montre comment s’abonner à cet événement.

```
m_speechRecognizer->RecognitionQualityDegrading +=
       ref new TypedEventHandler<SpeechRecognizer^, SpeechRecognitionQualityDegradingEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnSpeechQualityDegraded, this, _1, _2)
           );
```

Dans notre exemple de code, nous choisissons d’écrire les informations sur les conditions dans la console de débogage. Une application peut souhaiter fournir des commentaires à l’utilisateur via l’interface utilisateur, la synthèse vocale, etc., ou il peut s’avérer nécessaire de se comporter différemment quand la reconnaissance vocale est interrompue par une réduction temporaire de la qualité.

```
void HolographicSpeechPromptSampleMain::OnSpeechQualityDegraded(SpeechRecognizer^ recognizer, SpeechRecognitionQualityDegradingEventArgs^ args)
   {
       switch (args->Problem)
       {
       case SpeechRecognitionAudioProblem::TooFast:
           OutputDebugStringW(L"The user spoke too quickly.\n");
           break;

       case SpeechRecognitionAudioProblem::TooSlow:
           OutputDebugStringW(L"The user spoke too slowly.\n");
           break;

       case SpeechRecognitionAudioProblem::TooQuiet:
           OutputDebugStringW(L"The user spoke too softly.\n");
           break;

       case SpeechRecognitionAudioProblem::TooLoud:
           OutputDebugStringW(L"The user spoke too loudly.\n");
           break;

       case SpeechRecognitionAudioProblem::TooNoisy:
           OutputDebugStringW(L"There is too much noise in the signal.\n");
           break;

       case SpeechRecognitionAudioProblem::NoSignal:
           OutputDebugStringW(L"There is no signal.\n");
           break;

       case SpeechRecognitionAudioProblem::None:
       default:
           OutputDebugStringW(L"An error was reported with no information.\n");
           break;
       }
   }
```

Si vous n’utilisez pas de classes Ref pour créer votre application DirectX, vous devez vous désabonner de l’événement avant de libérer ou de recréer votre reconnaissance vocale. Le HolographicSpeechPromptSample a une routine pour arrêter la reconnaissance et se désabonner des événements de la façon suivante:

```
Concurrency::task<void> HolographicSpeechPromptSampleMain::StopCurrentRecognizerIfExists()
   {
       return create_task([this]()
       {
           if (m_speechRecognizer != nullptr)
           {
               return create_task(m_speechRecognizer->StopRecognitionAsync()).then([this]()
               {
                   m_speechRecognizer->RecognitionQualityDegrading -= m_speechRecognitionQualityDegradedToken;

                   if (m_speechRecognizer->ContinuousRecognitionSession != nullptr)
                   {
                       m_speechRecognizer->ContinuousRecognitionSession->ResultGenerated -= m_speechRecognizerResultEventToken;
                   }
               });
           }
           else
           {
               return create_task([this]() { m_speechRecognizer = nullptr; });
           }
       });
   }
```

## <a name="use-speech-synthesis-to-provide-audible-voice-prompts"></a>Utiliser la synthèse vocale pour fournir des invites vocales audibles

Les exemples de reconnaissance vocale holographique utilisent la synthèse vocale pour fournir des instructions audibles à l’utilisateur. Cette rubrique décrit le processus de création d’un exemple de voix synthétisée et sa lecture à l’aide des API audio HRTF.

Vous devez fournir vos propres invites vocales lors de la demande d’entrée de phrase. Cela peut également être utile pour indiquer à quel moment les commandes vocales peuvent être parlées, pour un scénario de reconnaissance continue. Voici un exemple de la procédure à suivre avec un synthétiseur vocal; Notez que vous pouvez également utiliser un clip vocal pré-enregistré, une interface utilisateur visuelle ou tout autre indicateur de ce qu’il faut prononcer, par exemple dans les scénarios où l’invite n’est pas dynamique.

Tout d’abord, créez l’objet SpeechSynthesizer:

```
auto speechSynthesizer = ref new Windows::Media::SpeechSynthesis::SpeechSynthesizer();
```

Vous avez également besoin d’une chaîne avec le texte à synthétiser:

```
// Phrase recognition works best when requesting a phrase or sentence.
   StringReference voicePrompt = L"At the prompt: Say a phrase, asking me to change the cube to a specific color.";
```

La reconnaissance vocale est synthétisée de façon asynchrone à l’aide de SynthesizeTextToStreamAsync. Ici, nous lançons une tâche asynchrone pour synthétiser la parole.

```
create_task(speechSynthesizer->SynthesizeTextToStreamAsync(voicePrompt), task_continuation_context::use_current())
       .then([this, speechSynthesizer](task<Windows::Media::SpeechSynthesis::SpeechSynthesisStream^> synthesisStreamTask)
   {
       try
       {
```

La synthèse vocale est envoyée sous forme de flux d’octets. Nous pouvons initialiser une voix XAudio2 à l’aide de ce flux d’octets. pour nos exemples de code holographiques, nous les relireons en tant qu’effet audio HRTF.

```
Windows::Media::SpeechSynthesis::SpeechSynthesisStream^ stream = synthesisStreamTask.get();

           auto hr = m_speechSynthesisSound.Initialize(stream, 0);
           if (SUCCEEDED(hr))
           {
               m_speechSynthesisSound.SetEnvironment(HrtfEnvironment::Small);
               m_speechSynthesisSound.Start();

               // Amount of time to pause after the audio prompt is complete, before listening
               // for speech input.
               static const float bufferTime = 0.15f;

               // Wait until the prompt is done before listening.
               m_secondsUntilSoundIsComplete = m_speechSynthesisSound.GetDuration() + bufferTime;
               m_waitingForSpeechPrompt = true;
           }
       }
```

Comme avec la reconnaissance vocale, la synthèse vocale lève une exception en cas de problème.

```
catch (Exception^ exception)
       {
           PrintWstringToDebugConsole(
               std::wstring(L"Exception while trying to synthesize speech: ") +
               exception->Message->Data() +
               L"\n"
               );

           // Handle exceptions here.
       }
   });
```

## <a name="see-also"></a>Voir aussi
* [Conception d’applications vocales](https://msdn.microsoft.com/library/dn596121.aspx)
* [Son spatial dans DirectX](spatial-sound-in-directx.md)
* [Exemple SpeechRecognitionAndSynthesis](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpeechRecognitionAndSynthesis)
