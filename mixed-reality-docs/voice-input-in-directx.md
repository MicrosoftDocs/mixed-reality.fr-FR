---
title: Entrée vocale dans DirectX
description: Explique comment implémenter des commandes vocales et reconnaissance de phrase et la phrase petite dans une application DirectX pour Windows Mixed Reality.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: procédure pas à pas, commande vocale, une phrase, reconnaissance, speech, directx, plate-forme, cortana, réalité mixte windows
ms.openlocfilehash: 728457a495616e5f65ec3986dfb6ac60231f9e46
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597125"
---
# <a name="voice-input-in-directx"></a>Entrée vocale dans DirectX

Cette rubrique explique comment implémenter [commandes vocales](voice-input.md)et de reconnaissance de phrase et la phrase petite dans une application DirectX pour Windows Mixed Reality.

>[!NOTE]
>Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).  Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.

## <a name="use-a-speechrecognizer-for-continuous-recognition-of-voice-commands"></a>Utiliser un SpeechRecognizer pour la reconnaissance continue des commandes vocales

Dans cette section, nous décrivons comment utiliser la reconnaissance vocale continue pour activer les commandes vocales dans votre application. Cette procédure pas à pas utilise le code à partir de la [HolographicVoiceInput](http://go.microsoft.com/fwlink/p/?LinkId=844964) exemple. Lorsque l’exemple est exécuté, énonce le nom de l’une des commandes de couleur enregistrée pour modifier la couleur du cube en rotation.

Tout d’abord, créez un **Windows::Media::SpeechRecognition::SpeechRecognizer** instance.

À partir de *HolographicVoiceInputSampleMain::CreateSpeechConstraintsForCurrentState*:

```
m_speechRecognizer = ref new SpeechRecognizer();
```

Vous aurez besoin créer une liste de commandes vocales pour le module de reconnaissance écouter. Nous construisons un ensemble de commandes pour modifier la couleur d’un hologramme. Pour des raisons pratiques, nous créons également les données que nous allons utiliser pour les commandes par la suite.

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

Commandes peuvent être spécifiées à l’aide de mots phonétiques qui ne peuvent pas être dans un dictionnaire :

```
m_speechCommandList->Append(StringReference(L"SpeechRecognizer"));
   m_speechCommandData.push_back(float4(0.5f, 0.1f, 1.f, 1.f));
```

La liste des commandes est chargée dans la liste des contraintes pour le module de reconnaissance vocale. Cela en utilisant un [SpeechRecognitionListConstraint](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionlistconstraint.aspx) objet.

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

S’abonner à la [ResultGenerated](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated.aspx) événement sur le module de reconnaissance vocale [SpeechContinuousRecognitionSession](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.aspx). Cet événement informe votre application lorsqu’un de vos commandes a été reconnu.

```
m_speechRecognizer->ContinuousRecognitionSession->ResultGenerated +=
       ref new TypedEventHandler<SpeechContinuousRecognitionSession^, SpeechContinuousRecognitionResultGeneratedEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnResultGenerated, this, _1, _2)
           );
```

Votre **OnResultGenerated** Gestionnaire d’événements reçoit des données d’événement dans un [SpeechContinuousRecognitionResultGeneratedEventArgs](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.aspx) instance. Si la confiance est supérieure au seuil que vous avez défini, votre application doit noter que l’événement s’est produit. Enregistrer les données d’événement afin de pouvoir l’utiliser dans une boucle de mise à jour ultérieure.

À partir de *HolographicVoiceInputSampleMain.cpp*:

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

Rendre utilisent les données toutefois applicables à votre scénario d’application. Dans notre exemple de code, nous modifier la couleur du cube en rotation hologramme en fonction de la commande de l’utilisateur.

À partir de *HolographicVoiceInputSampleMain::Update*:

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

## <a name="use-dictation-for-one-shot-recognition-of-speech-phrases-and-sentences"></a>Utiliser la dictée de reconnaissance One-Shot de phrases de reconnaissance vocale et des expressions

Vous pouvez configurer un module de reconnaissance vocale pour écouter les expressions ou phrases parlées par l’utilisateur. Dans ce cas, nous appliquons un SpeechRecognitionTopicConstraint qui indique à la reconnaissance vocale de quel type d’entrée à attendre. Le flux de travail d’application est la suivante, pour ce type de cas d’usage :
1. Votre application crée le SpeechRecognizer fournit des invites de l’interface utilisateur et commence à écouter pour une commande à énoncer immédiatement.
2. L’utilisateur parle d’une expression ou une phrase.
3. Reconnaissance de la voix de l’utilisateur est effectuée, et un résultat est retourné à l’application. À ce stade, votre application doit fournir une invite d’interface utilisateur indiquant que la reconnaissance s’est produite.
4. Selon le niveau de confiance que vous souhaitez répondre et le niveau de confiance du résultat de reconnaissance vocale, votre application peut traiter le résultat et répondre de manière appropriée.

Cette section décrit comment créer un SpeechRecognizer, compilez la contrainte et écouter la saisie vocale.

Le code suivant compile la contrainte de rubrique, qui dans ce cas est optimisée pour la recherche sur le Web.

```
auto constraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, L"webSearch");
   m_speechRecognizer->Constraints->Clear();
   m_speechRecognizer->Constraints->Append(constraint);
   return create_task(m_speechRecognizer->CompileConstraintsAsync())
       .then([this](task<SpeechRecognitionCompilationResult^> previousTask)
   {
```

Si la compilation réussit, nous pouvons poursuivre la reconnaissance vocale.

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

Le résultat est ensuite renvoyé à l’application. Si nous sommes convaincus suffisamment dans le résultat, nous pouvons traiter la commande. Cet exemple de code traite les résultats en toute confiance au moins à moyen.

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

Chaque fois que vous utilisez la reconnaissance vocale, il est conseillé pour les exceptions qui peut indiquer à que l’utilisateur a désactivé le microphone dans les paramètres de confidentialité du système. Cela peut se produire pendant l’initialisation, ou lors de la reconnaissance.

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

**REMARQUE :** Il existe plusieurs prédéfinies [SpeechRecognitionScenarios](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionscenario.aspx) disponibles pour optimiser la reconnaissance vocale.
* Si vous souhaitez optimiser pour la dictée, utilisez le scénario de dictée :

```
// Compile the dictation topic constraint, which optimizes for speech dictation.
   auto dictationConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::Dictation, "dictation");
   m_speechRecognizer->Constraints->Append(dictationConstraint);
```
* Lorsque vous utilisez la reconnaissance vocale pour effectuer une recherche Web, vous pouvez utiliser une contrainte de scénario Web spécifiques comme suit :

```
// Add a web search topic constraint to the recognizer.
   auto webSearchConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, "webSearch");
   speechRecognizer->Constraints->Append(webSearchConstraint);
```
* Utilisez la contrainte de formulaire pour remplir des formulaires. Dans ce cas, il est préférable d’appliquer votre propre syntaxe qui est optimisé pour remplir votre formulaire.

```
// Add a form constraint to the recognizer.
   auto formConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::FormFilling, "formFilling");
   speechRecognizer->Constraints->Append(formConstraint );
```
* Vous pouvez fournir votre propre grammaire en utilisant le format SRGS.

## <a name="use-continuous-freeform-speech-dictation"></a>Utilisez la dictée vocale continu, de forme libre

Consultez l’exemple de code de reconnaissance vocale de Windows 10 UWP pour le scénario de dictée continue [ici.](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpeechRecognitionAndSynthesis/cpp/Scenario_ContinuousDictation.xaml.cpp)

## <a name="handle-degradation-in-quality"></a>Dégradation de la poignée de qualité

Conditions dans l’environnement peuvent parfois empêcher la reconnaissance vocale à partir de travail. Par exemple, l’espace est peut-être trop bruyante ou l’utilisateur peut énoncer au plus un volume trop élevé. L’API de reconnaissance vocale fournit des informations, si possible, sur les conditions qui ont provoqué une dégradation de la qualité.

Ces informations sont envoyées à votre application à l’aide d’un événement WinRT. Voici un exemple montrant comment s’abonner à cet événement.

```
m_speechRecognizer->RecognitionQualityDegrading +=
       ref new TypedEventHandler<SpeechRecognizer^, SpeechRecognitionQualityDegradingEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnSpeechQualityDegraded, this, _1, _2)
           );
```

Dans notre exemple de code, nous choisissons d’écrire les informations de conditions dans la console de débogage. Une application peut vouloir fournir des commentaires à l’utilisateur via l’interface utilisateur, la synthèse vocale et ainsi de suite, ou il faudra se comportent différemment lorsque vocale est interrompue par une réduction temporaire de qualité.

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

Si vous n’utilisez pas les classes ref pour créer votre application DirectX, vous devez désabonner l’événement avant la libération ou à recréer votre module de reconnaissance vocale. Le HolographicSpeechPromptSample a une routine pour arrêter la reconnaissance et se désabonner d’événements comme suit :

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

## <a name="use-speech-synthesis-to-provide-audible-voice-prompts"></a>Utilisation de la synthèse vocale pour fournir des invites vocales sonores

Les exemples de reconnaissance vocale HOLOGRAPHIQUE utilisent la synthèse vocale pour fournir des instructions sonores à l’utilisateur. Cette rubrique décrit le processus de création d’un exemple de voix synthétisée et lire à l’aide de l’API audio HRTF.

Vous devez fournir que votre propre vocale vous invite à entrer lors de la demande de saisie du mot. Cela peut également être utile pour indiquer quand les commandes vocales peuvent être prononcés, pour un scénario de reconnaissance continue. Voici un exemple montrant comment procéder avec un synthétiseur vocal ; Notez que vous pouvez également utiliser un message vocal préenregistrées, une interface utilisateur visual ou autre indicateur des éléments à titre d’exemple dans les scénarios où l’invite n’est pas dynamique.

Commencez par créer l’objet de SpeechSynthesizer :

```
auto speechSynthesizer = ref new Windows::Media::SpeechSynthesis::SpeechSynthesizer();
```

Vous devez également une chaîne avec le texte à être synthétisées :

```
// Phrase recognition works best when requesting a phrase or sentence.
   StringReference voicePrompt = L"At the prompt: Say a phrase, asking me to change the cube to a specific color.";
```

Reconnaissance vocale est synthétisé à l’aide de façon asynchrone les SynthesizeTextToStreamAsync. Ici, nous démarrons une tâche asynchrone afin de synthétiser les paroles.

```
create_task(speechSynthesizer->SynthesizeTextToStreamAsync(voicePrompt), task_continuation_context::use_current())
       .then([this, speechSynthesizer](task<Windows::Media::SpeechSynthesis::SpeechSynthesisStream^> synthesisStreamTask)
   {
       try
       {
```

La synthèse vocale est envoyée comme un flux d’octets. Nous pouvons initialiser une voix XAudio2 à l’aide de ce flux d’octets ; pour nos exemples de code HOLOGRAPHIQUE, nous Lisez-le comme un effet audio HRTF.

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

Comme avec la reconnaissance vocale, synthèse vocale lève une exception si une erreur survient.

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
* [Conception d’applications de reconnaissance vocale](https://msdn.microsoft.com/library/dn596121.aspx)
* [Son spatial dans DirectX](spatial-sound-in-directx.md)
* [Exemple de SpeechRecognitionAndSynthesis](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpeechRecognitionAndSynthesis)
