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
# <a name="voice-input-in-directx"></a><span data-ttu-id="97e1d-104">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="97e1d-104">Voice input in DirectX</span></span>

<span data-ttu-id="97e1d-105">Cette rubrique explique comment implémenter [commandes vocales](voice-input.md)et de reconnaissance de phrase et la phrase petite dans une application DirectX pour Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="97e1d-105">This topic explains how to implement [voice commands](voice-input.md), and small phrase and sentence recognition in a DirectX app for Windows Mixed Reality.</span></span>

>[!NOTE]
><span data-ttu-id="97e1d-106">Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="97e1d-106">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="97e1d-107">Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="97e1d-107">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="use-a-speechrecognizer-for-continuous-recognition-of-voice-commands"></a><span data-ttu-id="97e1d-108">Utiliser un SpeechRecognizer pour la reconnaissance continue des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="97e1d-108">Use a SpeechRecognizer for continuous recognition of voice commands</span></span>

<span data-ttu-id="97e1d-109">Dans cette section, nous décrivons comment utiliser la reconnaissance vocale continue pour activer les commandes vocales dans votre application.</span><span class="sxs-lookup"><span data-stu-id="97e1d-109">In this section, we describe how to use continuous speech recognition to enable voice commands in your app.</span></span> <span data-ttu-id="97e1d-110">Cette procédure pas à pas utilise le code à partir de la [HolographicVoiceInput](http://go.microsoft.com/fwlink/p/?LinkId=844964) exemple.</span><span class="sxs-lookup"><span data-stu-id="97e1d-110">This walkthrough uses code from the [HolographicVoiceInput](http://go.microsoft.com/fwlink/p/?LinkId=844964) Sample.</span></span> <span data-ttu-id="97e1d-111">Lorsque l’exemple est exécuté, énonce le nom de l’une des commandes de couleur enregistrée pour modifier la couleur du cube en rotation.</span><span class="sxs-lookup"><span data-stu-id="97e1d-111">When the sample is running, speak the name of one of the registered color commands to change the color of the spinning cube.</span></span>

<span data-ttu-id="97e1d-112">Tout d’abord, créez un **Windows::Media::SpeechRecognition::SpeechRecognizer** instance.</span><span class="sxs-lookup"><span data-stu-id="97e1d-112">First, create a new **Windows::Media::SpeechRecognition::SpeechRecognizer** instance.</span></span>

<span data-ttu-id="97e1d-113">À partir de *HolographicVoiceInputSampleMain::CreateSpeechConstraintsForCurrentState*:</span><span class="sxs-lookup"><span data-stu-id="97e1d-113">From *HolographicVoiceInputSampleMain::CreateSpeechConstraintsForCurrentState*:</span></span>

```
m_speechRecognizer = ref new SpeechRecognizer();
```

<span data-ttu-id="97e1d-114">Vous aurez besoin créer une liste de commandes vocales pour le module de reconnaissance écouter.</span><span class="sxs-lookup"><span data-stu-id="97e1d-114">You'll need to create a list of speech commands for the recognizer to listen for.</span></span> <span data-ttu-id="97e1d-115">Nous construisons un ensemble de commandes pour modifier la couleur d’un hologramme.</span><span class="sxs-lookup"><span data-stu-id="97e1d-115">Here, we construct a set of commands to change the color of a hologram.</span></span> <span data-ttu-id="97e1d-116">Pour des raisons pratiques, nous créons également les données que nous allons utiliser pour les commandes par la suite.</span><span class="sxs-lookup"><span data-stu-id="97e1d-116">For the sake of convenience, we also create the data that we'll use for the commands later on.</span></span>

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

<span data-ttu-id="97e1d-117">Commandes peuvent être spécifiées à l’aide de mots phonétiques qui ne peuvent pas être dans un dictionnaire :</span><span class="sxs-lookup"><span data-stu-id="97e1d-117">Commands can be specified using phonetic words that might not be in a dictionary:</span></span>

```
m_speechCommandList->Append(StringReference(L"SpeechRecognizer"));
   m_speechCommandData.push_back(float4(0.5f, 0.1f, 1.f, 1.f));
```

<span data-ttu-id="97e1d-118">La liste des commandes est chargée dans la liste des contraintes pour le module de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="97e1d-118">The list of commands is loaded into the list of constraints for the speech recognizer.</span></span> <span data-ttu-id="97e1d-119">Cela en utilisant un [SpeechRecognitionListConstraint](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionlistconstraint.aspx) objet.</span><span class="sxs-lookup"><span data-stu-id="97e1d-119">This is done by using a [SpeechRecognitionListConstraint](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionlistconstraint.aspx) object.</span></span>

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

<span data-ttu-id="97e1d-120">S’abonner à la [ResultGenerated](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated.aspx) événement sur le module de reconnaissance vocale [SpeechContinuousRecognitionSession](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.aspx).</span><span class="sxs-lookup"><span data-stu-id="97e1d-120">Subscribe to the [ResultGenerated](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated.aspx) event on the speech recognizer's [SpeechContinuousRecognitionSession](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.aspx).</span></span> <span data-ttu-id="97e1d-121">Cet événement informe votre application lorsqu’un de vos commandes a été reconnu.</span><span class="sxs-lookup"><span data-stu-id="97e1d-121">This event notifies your app when one of your commands has been recognized.</span></span>

```
m_speechRecognizer->ContinuousRecognitionSession->ResultGenerated +=
       ref new TypedEventHandler<SpeechContinuousRecognitionSession^, SpeechContinuousRecognitionResultGeneratedEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnResultGenerated, this, _1, _2)
           );
```

<span data-ttu-id="97e1d-122">Votre **OnResultGenerated** Gestionnaire d’événements reçoit des données d’événement dans un [SpeechContinuousRecognitionResultGeneratedEventArgs](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.aspx) instance.</span><span class="sxs-lookup"><span data-stu-id="97e1d-122">Your **OnResultGenerated** event handler receives event data in a [SpeechContinuousRecognitionResultGeneratedEventArgs](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.aspx) instance.</span></span> <span data-ttu-id="97e1d-123">Si la confiance est supérieure au seuil que vous avez défini, votre application doit noter que l’événement s’est produit.</span><span class="sxs-lookup"><span data-stu-id="97e1d-123">If the confidence is greater than the threshold you have defined, your app should note that the event happened.</span></span> <span data-ttu-id="97e1d-124">Enregistrer les données d’événement afin de pouvoir l’utiliser dans une boucle de mise à jour ultérieure.</span><span class="sxs-lookup"><span data-stu-id="97e1d-124">Save the event data so that you can make use of it in a subsequent update loop.</span></span>

<span data-ttu-id="97e1d-125">À partir de *HolographicVoiceInputSampleMain.cpp*:</span><span class="sxs-lookup"><span data-stu-id="97e1d-125">From *HolographicVoiceInputSampleMain.cpp*:</span></span>

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

<span data-ttu-id="97e1d-126">Rendre utilisent les données toutefois applicables à votre scénario d’application.</span><span class="sxs-lookup"><span data-stu-id="97e1d-126">Make use of the data however applicable to your app scenario.</span></span> <span data-ttu-id="97e1d-127">Dans notre exemple de code, nous modifier la couleur du cube en rotation hologramme en fonction de la commande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="97e1d-127">In our example code, we change the color of the spinning hologram cube according to the user's command.</span></span>

<span data-ttu-id="97e1d-128">À partir de *HolographicVoiceInputSampleMain::Update*:</span><span class="sxs-lookup"><span data-stu-id="97e1d-128">From *HolographicVoiceInputSampleMain::Update*:</span></span>

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

## <a name="use-dictation-for-one-shot-recognition-of-speech-phrases-and-sentences"></a><span data-ttu-id="97e1d-129">Utiliser la dictée de reconnaissance One-Shot de phrases de reconnaissance vocale et des expressions</span><span class="sxs-lookup"><span data-stu-id="97e1d-129">Use dictation for one-shot recognition of speech phrases and sentences</span></span>

<span data-ttu-id="97e1d-130">Vous pouvez configurer un module de reconnaissance vocale pour écouter les expressions ou phrases parlées par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="97e1d-130">You can configure a speech recognizer to listen for phrases or sentences spoken by the user.</span></span> <span data-ttu-id="97e1d-131">Dans ce cas, nous appliquons un SpeechRecognitionTopicConstraint qui indique à la reconnaissance vocale de quel type d’entrée à attendre.</span><span class="sxs-lookup"><span data-stu-id="97e1d-131">In this case, we apply a SpeechRecognitionTopicConstraint that tells the speech recognizer what type of input to expect.</span></span> <span data-ttu-id="97e1d-132">Le flux de travail d’application est la suivante, pour ce type de cas d’usage :</span><span class="sxs-lookup"><span data-stu-id="97e1d-132">The app workflow is as follows, for this type of use case:</span></span>
1. <span data-ttu-id="97e1d-133">Votre application crée le SpeechRecognizer fournit des invites de l’interface utilisateur et commence à écouter pour une commande à énoncer immédiatement.</span><span class="sxs-lookup"><span data-stu-id="97e1d-133">Your app creates the SpeechRecognizer, provides UI prompts, and starts listening for a command to be spoken immediately.</span></span>
2. <span data-ttu-id="97e1d-134">L’utilisateur parle d’une expression ou une phrase.</span><span class="sxs-lookup"><span data-stu-id="97e1d-134">The user speaks a phrase, or sentence.</span></span>
3. <span data-ttu-id="97e1d-135">Reconnaissance de la voix de l’utilisateur est effectuée, et un résultat est retourné à l’application.</span><span class="sxs-lookup"><span data-stu-id="97e1d-135">Recognition of the user's speech is performed, and a result is returned to the app.</span></span> <span data-ttu-id="97e1d-136">À ce stade, votre application doit fournir une invite d’interface utilisateur indiquant que la reconnaissance s’est produite.</span><span class="sxs-lookup"><span data-stu-id="97e1d-136">At this point, your app should provide a UI prompt indicating that recognition has occurred.</span></span>
4. <span data-ttu-id="97e1d-137">Selon le niveau de confiance que vous souhaitez répondre et le niveau de confiance du résultat de reconnaissance vocale, votre application peut traiter le résultat et répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="97e1d-137">Depending on the confidence level you want to respond to and the confidence level of the speech recognition result, your app can process the result and respond as appropriate.</span></span>

<span data-ttu-id="97e1d-138">Cette section décrit comment créer un SpeechRecognizer, compilez la contrainte et écouter la saisie vocale.</span><span class="sxs-lookup"><span data-stu-id="97e1d-138">This section describes how to create a SpeechRecognizer, compile the constraint, and listen for speech input.</span></span>

<span data-ttu-id="97e1d-139">Le code suivant compile la contrainte de rubrique, qui dans ce cas est optimisée pour la recherche sur le Web.</span><span class="sxs-lookup"><span data-stu-id="97e1d-139">The following code compiles the topic constraint, which in this case is optimized for Web search.</span></span>

```
auto constraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, L"webSearch");
   m_speechRecognizer->Constraints->Clear();
   m_speechRecognizer->Constraints->Append(constraint);
   return create_task(m_speechRecognizer->CompileConstraintsAsync())
       .then([this](task<SpeechRecognitionCompilationResult^> previousTask)
   {
```

<span data-ttu-id="97e1d-140">Si la compilation réussit, nous pouvons poursuivre la reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="97e1d-140">If compilation succeeds, we can proceed with speech recognition.</span></span>

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

<span data-ttu-id="97e1d-141">Le résultat est ensuite renvoyé à l’application.</span><span class="sxs-lookup"><span data-stu-id="97e1d-141">The result is then returned to the app.</span></span> <span data-ttu-id="97e1d-142">Si nous sommes convaincus suffisamment dans le résultat, nous pouvons traiter la commande.</span><span class="sxs-lookup"><span data-stu-id="97e1d-142">If we are confident enough in the result, we can process the command.</span></span> <span data-ttu-id="97e1d-143">Cet exemple de code traite les résultats en toute confiance au moins à moyen.</span><span class="sxs-lookup"><span data-stu-id="97e1d-143">This code example processes results with at least Medium confidence.</span></span>

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

<span data-ttu-id="97e1d-144">Chaque fois que vous utilisez la reconnaissance vocale, il est conseillé pour les exceptions qui peut indiquer à que l’utilisateur a désactivé le microphone dans les paramètres de confidentialité du système.</span><span class="sxs-lookup"><span data-stu-id="97e1d-144">Whenever you use speech recognition, you should watch for exceptions that could indicate the user has turned off the microphone in the system privacy settings.</span></span> <span data-ttu-id="97e1d-145">Cela peut se produire pendant l’initialisation, ou lors de la reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="97e1d-145">This can happen during initialization, or during recognition.</span></span>

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

<span data-ttu-id="97e1d-146">**REMARQUE :** Il existe plusieurs prédéfinies [SpeechRecognitionScenarios](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionscenario.aspx) disponibles pour optimiser la reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="97e1d-146">**NOTE:** There are several predefined [SpeechRecognitionScenarios](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionscenario.aspx) available for optimizing speech recognition.</span></span>
* <span data-ttu-id="97e1d-147">Si vous souhaitez optimiser pour la dictée, utilisez le scénario de dictée :</span><span class="sxs-lookup"><span data-stu-id="97e1d-147">If you want to optimize for dictation, use the Dictation scenario:</span></span>

```
// Compile the dictation topic constraint, which optimizes for speech dictation.
   auto dictationConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::Dictation, "dictation");
   m_speechRecognizer->Constraints->Append(dictationConstraint);
```
* <span data-ttu-id="97e1d-148">Lorsque vous utilisez la reconnaissance vocale pour effectuer une recherche Web, vous pouvez utiliser une contrainte de scénario Web spécifiques comme suit :</span><span class="sxs-lookup"><span data-stu-id="97e1d-148">When using speech to perform a Web search, you can use a Web-specific scenario constraint as follows:</span></span>

```
// Add a web search topic constraint to the recognizer.
   auto webSearchConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, "webSearch");
   speechRecognizer->Constraints->Append(webSearchConstraint);
```
* <span data-ttu-id="97e1d-149">Utilisez la contrainte de formulaire pour remplir des formulaires.</span><span class="sxs-lookup"><span data-stu-id="97e1d-149">Use the form constraint to fill out forms.</span></span> <span data-ttu-id="97e1d-150">Dans ce cas, il est préférable d’appliquer votre propre syntaxe qui est optimisé pour remplir votre formulaire.</span><span class="sxs-lookup"><span data-stu-id="97e1d-150">In this case, it is best to apply your own grammar that is optimized for filling out your form.</span></span>

```
// Add a form constraint to the recognizer.
   auto formConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::FormFilling, "formFilling");
   speechRecognizer->Constraints->Append(formConstraint );
```
* <span data-ttu-id="97e1d-151">Vous pouvez fournir votre propre grammaire en utilisant le format SRGS.</span><span class="sxs-lookup"><span data-stu-id="97e1d-151">You can provide your own grammar using the SRGS format.</span></span>

## <a name="use-continuous-freeform-speech-dictation"></a><span data-ttu-id="97e1d-152">Utilisez la dictée vocale continu, de forme libre</span><span class="sxs-lookup"><span data-stu-id="97e1d-152">Use continuous, freeform speech dictation</span></span>

<span data-ttu-id="97e1d-153">Consultez l’exemple de code de reconnaissance vocale de Windows 10 UWP pour le scénario de dictée continue [ici.](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpeechRecognitionAndSynthesis/cpp/Scenario_ContinuousDictation.xaml.cpp)</span><span class="sxs-lookup"><span data-stu-id="97e1d-153">See the Windows 10 UWP speech code sample for the continuous dictation scenario [here.](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpeechRecognitionAndSynthesis/cpp/Scenario_ContinuousDictation.xaml.cpp)</span></span>

## <a name="handle-degradation-in-quality"></a><span data-ttu-id="97e1d-154">Dégradation de la poignée de qualité</span><span class="sxs-lookup"><span data-stu-id="97e1d-154">Handle degradation in quality</span></span>

<span data-ttu-id="97e1d-155">Conditions dans l’environnement peuvent parfois empêcher la reconnaissance vocale à partir de travail.</span><span class="sxs-lookup"><span data-stu-id="97e1d-155">Conditions in the environment can sometimes prevent speech recognition from working.</span></span> <span data-ttu-id="97e1d-156">Par exemple, l’espace est peut-être trop bruyante ou l’utilisateur peut énoncer au plus un volume trop élevé.</span><span class="sxs-lookup"><span data-stu-id="97e1d-156">For example, the room might be too noisy or the user might speak at too high a volume.</span></span> <span data-ttu-id="97e1d-157">L’API de reconnaissance vocale fournit des informations, si possible, sur les conditions qui ont provoqué une dégradation de la qualité.</span><span class="sxs-lookup"><span data-stu-id="97e1d-157">The speech recognition API provides info, where possible, about conditions that have caused a degradation in quality.</span></span>

<span data-ttu-id="97e1d-158">Ces informations sont envoyées à votre application à l’aide d’un événement WinRT.</span><span class="sxs-lookup"><span data-stu-id="97e1d-158">This information is pushed to your app using a WinRT event.</span></span> <span data-ttu-id="97e1d-159">Voici un exemple montrant comment s’abonner à cet événement.</span><span class="sxs-lookup"><span data-stu-id="97e1d-159">Here is an example of how to subscribe to this event.</span></span>

```
m_speechRecognizer->RecognitionQualityDegrading +=
       ref new TypedEventHandler<SpeechRecognizer^, SpeechRecognitionQualityDegradingEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnSpeechQualityDegraded, this, _1, _2)
           );
```

<span data-ttu-id="97e1d-160">Dans notre exemple de code, nous choisissons d’écrire les informations de conditions dans la console de débogage.</span><span class="sxs-lookup"><span data-stu-id="97e1d-160">In our code sample, we choose to write the conditions info to the debug console.</span></span> <span data-ttu-id="97e1d-161">Une application peut vouloir fournir des commentaires à l’utilisateur via l’interface utilisateur, la synthèse vocale et ainsi de suite, ou il faudra se comportent différemment lorsque vocale est interrompue par une réduction temporaire de qualité.</span><span class="sxs-lookup"><span data-stu-id="97e1d-161">An app might want to provide feedback to the user via UI, speech synthesis, and so on, or it might need to behave differently when speech is interrupted by a temporary reduction in quality.</span></span>

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

<span data-ttu-id="97e1d-162">Si vous n’utilisez pas les classes ref pour créer votre application DirectX, vous devez désabonner l’événement avant la libération ou à recréer votre module de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="97e1d-162">If you are not using ref classes to create your DirectX app, you must unsubscribe from the event before releasing or recreating your speech recognizer.</span></span> <span data-ttu-id="97e1d-163">Le HolographicSpeechPromptSample a une routine pour arrêter la reconnaissance et se désabonner d’événements comme suit :</span><span class="sxs-lookup"><span data-stu-id="97e1d-163">The HolographicSpeechPromptSample has a routine to stop recognition, and unsubscribe from events like so:</span></span>

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

## <a name="use-speech-synthesis-to-provide-audible-voice-prompts"></a><span data-ttu-id="97e1d-164">Utilisation de la synthèse vocale pour fournir des invites vocales sonores</span><span class="sxs-lookup"><span data-stu-id="97e1d-164">Use speech synthesis to provide audible voice prompts</span></span>

<span data-ttu-id="97e1d-165">Les exemples de reconnaissance vocale HOLOGRAPHIQUE utilisent la synthèse vocale pour fournir des instructions sonores à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="97e1d-165">The holographic speech samples use speech synthesis to provide audible instructions to the user.</span></span> <span data-ttu-id="97e1d-166">Cette rubrique décrit le processus de création d’un exemple de voix synthétisée et lire à l’aide de l’API audio HRTF.</span><span class="sxs-lookup"><span data-stu-id="97e1d-166">This topic walks through the process of creating a synthesized voice sample, and playing it back using the HRTF audio APIs.</span></span>

<span data-ttu-id="97e1d-167">Vous devez fournir que votre propre vocale vous invite à entrer lors de la demande de saisie du mot.</span><span class="sxs-lookup"><span data-stu-id="97e1d-167">You should provide your own speech prompts when requesting phrase input.</span></span> <span data-ttu-id="97e1d-168">Cela peut également être utile pour indiquer quand les commandes vocales peuvent être prononcés, pour un scénario de reconnaissance continue.</span><span class="sxs-lookup"><span data-stu-id="97e1d-168">This can also be helpful for indicating when speech commands can be spoken, for a continuous recognition scenario.</span></span> <span data-ttu-id="97e1d-169">Voici un exemple montrant comment procéder avec un synthétiseur vocal ; Notez que vous pouvez également utiliser un message vocal préenregistrées, une interface utilisateur visual ou autre indicateur des éléments à titre d’exemple dans les scénarios où l’invite n’est pas dynamique.</span><span class="sxs-lookup"><span data-stu-id="97e1d-169">Here is an example of how to do that with a speech synthesizer; note that you could also use a pre-recorded voice clip, a visual UI, or other indicator of what to say, for example in scenarios where the prompt is not dynamic.</span></span>

<span data-ttu-id="97e1d-170">Commencez par créer l’objet de SpeechSynthesizer :</span><span class="sxs-lookup"><span data-stu-id="97e1d-170">First, create the SpeechSynthesizer object:</span></span>

```
auto speechSynthesizer = ref new Windows::Media::SpeechSynthesis::SpeechSynthesizer();
```

<span data-ttu-id="97e1d-171">Vous devez également une chaîne avec le texte à être synthétisées :</span><span class="sxs-lookup"><span data-stu-id="97e1d-171">You also need a string with the text to be synthesized:</span></span>

```
// Phrase recognition works best when requesting a phrase or sentence.
   StringReference voicePrompt = L"At the prompt: Say a phrase, asking me to change the cube to a specific color.";
```

<span data-ttu-id="97e1d-172">Reconnaissance vocale est synthétisé à l’aide de façon asynchrone les SynthesizeTextToStreamAsync.</span><span class="sxs-lookup"><span data-stu-id="97e1d-172">Speech is synthesized asynchronously using SynthesizeTextToStreamAsync.</span></span> <span data-ttu-id="97e1d-173">Ici, nous démarrons une tâche asynchrone afin de synthétiser les paroles.</span><span class="sxs-lookup"><span data-stu-id="97e1d-173">Here, we kick off an async task to synthesize the speech.</span></span>

```
create_task(speechSynthesizer->SynthesizeTextToStreamAsync(voicePrompt), task_continuation_context::use_current())
       .then([this, speechSynthesizer](task<Windows::Media::SpeechSynthesis::SpeechSynthesisStream^> synthesisStreamTask)
   {
       try
       {
```

<span data-ttu-id="97e1d-174">La synthèse vocale est envoyée comme un flux d’octets.</span><span class="sxs-lookup"><span data-stu-id="97e1d-174">The speech synthesis is sent as a byte stream.</span></span> <span data-ttu-id="97e1d-175">Nous pouvons initialiser une voix XAudio2 à l’aide de ce flux d’octets ; pour nos exemples de code HOLOGRAPHIQUE, nous Lisez-le comme un effet audio HRTF.</span><span class="sxs-lookup"><span data-stu-id="97e1d-175">We can initialize an XAudio2 voice using that byte stream; for our holographic code samples, we play it back as an HRTF audio effect.</span></span>

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

<span data-ttu-id="97e1d-176">Comme avec la reconnaissance vocale, synthèse vocale lève une exception si une erreur survient.</span><span class="sxs-lookup"><span data-stu-id="97e1d-176">As with speech recognition, speech synthesis will throw an exception if something goes wrong.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="97e1d-177">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="97e1d-177">See also</span></span>
* [<span data-ttu-id="97e1d-178">Conception d’applications de reconnaissance vocale</span><span class="sxs-lookup"><span data-stu-id="97e1d-178">Speech app design</span></span>](https://msdn.microsoft.com/library/dn596121.aspx)
* [<span data-ttu-id="97e1d-179">Son spatial dans DirectX</span><span class="sxs-lookup"><span data-stu-id="97e1d-179">Spatial sound in DirectX</span></span>](spatial-sound-in-directx.md)
* [<span data-ttu-id="97e1d-180">Exemple de SpeechRecognitionAndSynthesis</span><span class="sxs-lookup"><span data-stu-id="97e1d-180">SpeechRecognitionAndSynthesis sample</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpeechRecognitionAndSynthesis)
