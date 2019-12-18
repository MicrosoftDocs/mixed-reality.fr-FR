---
title: Entrée vocale dans DirectX
description: Explique comment implémenter des commandes vocales et une petite reconnaissance d’expressions et de phrases dans une application DirectX pour Windows Mixed Reality.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: procédure pas à pas, commande vocale, expression, reconnaissance, reconnaissance vocale, DirectX, plateforme, Cortana, Windows Mixed Reality
ms.openlocfilehash: c0a7ca85c24147e607603e733c9d191c64cbd927
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75181819"
---
# <a name="voice-input-in-directx"></a>Entrée vocale dans DirectX

Cet article explique comment implémenter des [commandes vocales](voice-input.md) , ainsi que la reconnaissance des phrases et des phrases de petite taille dans une application DirectX pour Windows Mixed Reality.

>[!NOTE]
>Les extraits de code de cet article utilisent C++/CX au lieu de C++/WinRT conforme à C + +17, qui est utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).  Les concepts sont équivalents pour C++un projet/WinRT, mais vous devez traduire le code.

## <a name="use-speechrecognizer-for-continuous-speech-recognition"></a>Utiliser SpeechRecognizer pour la reconnaissance vocale continue

Cette section décrit comment utiliser la reconnaissance vocale continue pour activer les commandes vocales dans votre application. Cette procédure pas à pas utilise le code de l’exemple [HolographicVoiceInput](https://go.microsoft.com/fwlink/p/?LinkId=844964) . Lorsque l’exemple est en cours d’exécution, parlez le nom de l’une des commandes de couleur inscrite pour modifier la couleur du cube en rotation.

Tout d’abord, créez une instance *Windows :: Media :: SpeechRecognition :: SpeechRecognizer* .

À partir de *HolographicVoiceInputSampleMain :: CreateSpeechConstraintsForCurrentState*:

```
m_speechRecognizer = ref new SpeechRecognizer();
```

Créez une liste de commandes vocales pour le module de reconnaissance à écouter. Ici, nous créons un ensemble de commandes pour modifier la couleur d’un hologramme. Pour plus de commodité, nous créons également les données que nous allons utiliser pour les commandes ultérieurement.

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

Vous pouvez utiliser des mots phonétiques qui peuvent ne pas figurer dans un dictionnaire pour spécifier des commandes.

```
m_speechCommandList->Append(StringReference(L"SpeechRecognizer"));
   m_speechCommandData.push_back(float4(0.5f, 0.1f, 1.f, 1.f));
```

Pour charger la liste de commandes dans la liste des contraintes pour le module de reconnaissance vocale, utilisez un objet [SpeechRecognitionListConstraint](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionlistconstraint.aspx) .

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

Votre gestionnaire d’événements *OnResultGenerated* reçoit les données d’événement dans une instance [SpeechContinuousRecognitionResultGeneratedEventArgs](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.aspx) . Si la confiance est supérieure au seuil que vous avez défini, votre application doit noter que l’événement s’est produit. Enregistrez les données d’événement afin de pouvoir les utiliser dans une boucle de mise à jour ultérieure.

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

Dans notre exemple de code, nous modifions la couleur du cube d’hologramme en rotation en fonction de la commande de l’utilisateur.

À partir de *HolographicVoiceInputSampleMain :: Update*:

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

## <a name="use-one-shot-recognition"></a>Utilisez la reconnaissance « une seule capture »

Vous pouvez configurer un module de reconnaissance vocale pour écouter les expressions ou les phrases que l’utilisateur parle. Dans ce cas, nous appliquons un *SpeechRecognitionTopicConstraint* qui indique au module de reconnaissance vocale le type d’entrée à attendre. Voici un flux de travail d’application pour ce scénario :
1. Votre application crée le SpeechRecognizer, fournit des invites d’interface utilisateur et commence à écouter une commande parlée.
2. L’utilisateur parle une expression ou une phrase.
3. La reconnaissance de la parole de l’utilisateur se produit et un résultat est renvoyé à l’application. À ce stade, votre application doit fournir une invite d’interface utilisateur pour indiquer que la reconnaissance s’est produite.
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

Chaque fois que vous utilisez la reconnaissance vocale, observez les exceptions qui peuvent indiquer que l’utilisateur a désactivé le microphone dans les paramètres de confidentialité du système. Cela peut se produire pendant l’initialisation ou la reconnaissance.

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

> [!NOTE]
> Il existe plusieurs [SpeechRecognitionScenarios](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionscenario.aspx) prédéfinis que vous pouvez utiliser pour optimiser la reconnaissance vocale.

* Pour optimiser la dictée, utilisez le scénario de dictée.<br/>
   ```
   // Compile the dictation topic constraint, which optimizes for speech dictation.
   auto dictationConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::Dictation, "dictation");
   m_speechRecognizer->Constraints->Append(dictationConstraint);
   ```

* Pour les recherches Web vocales, utilisez la contrainte de scénario spécifique au Web suivante.

   ```
   // Add a web search topic constraint to the recognizer.
   auto webSearchConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, "webSearch");
   speechRecognizer->Constraints->Append(webSearchConstraint);
   ```

* Utilisez la contrainte de formulaire pour remplir les formulaires. Dans ce cas, il est préférable d’appliquer votre propre grammaire qui est optimisée pour remplir le formulaire.

   ```
   // Add a form constraint to the recognizer.
   auto formConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::FormFilling, "formFilling");
   speechRecognizer->Constraints->Append(formConstraint );
   ```
* Vous pouvez fournir votre propre grammaire au format SRGS.

## <a name="use-continuous-recognition"></a>Utiliser la reconnaissance continue

Pour le scénario de dictée continue, consultez l' [exemple de code vocal Windows 10 UWP](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpeechRecognitionAndSynthesis/cpp/Scenario_ContinuousDictation.xaml.cpp).

## <a name="handle-quality-degradation"></a>Gérer la dégradation de la qualité

Les conditions environnementales interfèrent parfois avec la reconnaissance vocale. Par exemple, la salle peut être trop bruyante ou l’utilisateur peut parler trop fort. Dans la mesure du possible, l’API de reconnaissance vocale fournit des informations sur les conditions à l’origine de la dégradation de la qualité. Ces informations sont envoyées à votre application par le biais d’un événement WinRT. L’exemple suivant montre comment s’abonner à cet événement.

```
m_speechRecognizer->RecognitionQualityDegrading +=
       ref new TypedEventHandler<SpeechRecognizer^, SpeechRecognitionQualityDegradingEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnSpeechQualityDegraded, this, _1, _2)
           );
```

Dans notre exemple de code, nous écrivons les informations sur les conditions dans la console de débogage. Une application peut souhaiter fournir des commentaires à l’utilisateur via l’interface utilisateur, la synthèse vocale et une autre méthode. Ou il peut s’avérer nécessaire de se comporter différemment lorsque la reconnaissance vocale est interrompue par une réduction temporaire de la qualité.

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

Si vous n’utilisez pas de classes Ref pour créer votre application DirectX, vous devez vous désabonner de l’événement avant de libérer ou de recréer votre reconnaissance vocale. HolographicSpeechPromptSample a une routine pour arrêter la reconnaissance et annuler l’abonnement aux événements.

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

## <a name="use-speech-synthesis-to-provide-audible-prompts"></a>Utiliser la synthèse vocale pour fournir des invites sonores

Les exemples de reconnaissance vocale holographique utilisent la synthèse vocale pour fournir des instructions audibles à l’utilisateur. Cette section montre comment créer un exemple de voix synthétisée, puis le relire via les API audio HRTF.

Vous devez fournir vos propres invites vocales lorsque vous demandez une entrée de phrase. Les invites permettent également d’indiquer à quel moment les commandes vocales peuvent être parlées pour un scénario de reconnaissance continue. L’exemple suivant montre comment utiliser un synthétiseur vocal pour effectuer cette opération. Vous pouvez également utiliser un clip vocal pré-enregistré, une interface utilisateur visuelle ou un autre indicateur de ce qui doit être dit, par exemple dans les scénarios où l’invite n’est pas dynamique.

Tout d’abord, créez l’objet SpeechSynthesizer.

```
auto speechSynthesizer = ref new Windows::Media::SpeechSynthesis::SpeechSynthesizer();
```

Vous avez également besoin d’une chaîne qui contient le texte à synthétiser.

```
// Phrase recognition works best when requesting a phrase or sentence.
   StringReference voicePrompt = L"At the prompt: Say a phrase, asking me to change the cube to a specific color.";
```

La parole est synthétisée de façon asynchrone via SynthesizeTextToStreamAsync. Ici, nous commençons une tâche asynchrone pour synthétiser la parole.

```
create_task(speechSynthesizer->SynthesizeTextToStreamAsync(voicePrompt), task_continuation_context::use_current())
       .then([this, speechSynthesizer](task<Windows::Media::SpeechSynthesis::SpeechSynthesisStream^> synthesisStreamTask)
   {
       try
       {
```

La synthèse vocale est envoyée sous forme de flux d’octets. Nous pouvons utiliser ce flux d’octets pour initialiser une voix XAudio2. Pour nos exemples de code holographiques, nous les relireons en tant qu’effet audio HRTF.

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

## <a name="see-also"></a>Articles associés
* [Conception d’applications vocales](https://msdn.microsoft.com/library/dn596121.aspx)
* [Exemple SpeechRecognitionAndSynthesis](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpeechRecognitionAndSynthesis)
