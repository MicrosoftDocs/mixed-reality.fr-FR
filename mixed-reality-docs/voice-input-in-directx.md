---
title: Entrée vocale dans DirectX
description: Explique comment implémenter des commandes vocales et une petite reconnaissance d’expressions et de phrases dans une application DirectX pour Windows Mixed Reality.
author: mikeriches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: procédure pas à pas, commande vocale, expression, reconnaissance, reconnaissance vocale, DirectX, plateforme, Cortana, Windows Mixed Reality
ms.openlocfilehash: 2837a0fc42e8fdebb2e1facee118d20b5668cd43
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81277967"
---
# <a name="voice-input-in-directx"></a><span data-ttu-id="d5e6d-104">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="d5e6d-104">Voice input in DirectX</span></span>

<span data-ttu-id="d5e6d-105">Cet article explique comment implémenter des [commandes vocales](voice-input.md) , ainsi que la reconnaissance des phrases et des phrases de petite taille dans une application DirectX pour Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-105">This article explains how to implement [voice commands](voice-input.md) plus small-phrase and sentence recognition in a DirectX app for Windows Mixed Reality.</span></span>

>[!NOTE]
><span data-ttu-id="d5e6d-106">Les extraits de code de cet article utilisent C++/CX au lieu de C++/WinRT conforme à C + +17, qui est utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="d5e6d-106">The code snippets in this article use C++/CX rather than C++17-compliant C++/WinRT, which is used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="d5e6d-107">Les concepts sont équivalents pour C++un projet/WinRT, mais vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-107">The concepts are equivalent for a C++/WinRT project, but you need to translate the code.</span></span>

## <a name="use-speechrecognizer-for-continuous-speech-recognition"></a><span data-ttu-id="d5e6d-108">Utiliser SpeechRecognizer pour la reconnaissance vocale continue</span><span class="sxs-lookup"><span data-stu-id="d5e6d-108">Use SpeechRecognizer for continuous speech recognition</span></span>

<span data-ttu-id="d5e6d-109">Cette section décrit comment utiliser la reconnaissance vocale continue pour activer les commandes vocales dans votre application.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-109">This section describes how to use continuous speech recognition to enable voice commands in your app.</span></span> <span data-ttu-id="d5e6d-110">Cette procédure pas à pas utilise le code de l’exemple [HolographicVoiceInput](https://go.microsoft.com/fwlink/p/?LinkId=844964) .</span><span class="sxs-lookup"><span data-stu-id="d5e6d-110">This walk-through uses code from the [HolographicVoiceInput](https://go.microsoft.com/fwlink/p/?LinkId=844964) sample.</span></span> <span data-ttu-id="d5e6d-111">Lorsque l’exemple est en cours d’exécution, parlez le nom de l’une des commandes de couleur inscrite pour modifier la couleur du cube en rotation.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-111">When the sample is running, speak the name of one of the registered color commands to change the color of the spinning cube.</span></span>

<span data-ttu-id="d5e6d-112">Tout d’abord, créez une instance *Windows :: Media :: SpeechRecognition :: SpeechRecognizer* .</span><span class="sxs-lookup"><span data-stu-id="d5e6d-112">First, create a new *Windows::Media::SpeechRecognition::SpeechRecognizer* instance.</span></span>

<span data-ttu-id="d5e6d-113">À partir de *HolographicVoiceInputSampleMain :: CreateSpeechConstraintsForCurrentState*:</span><span class="sxs-lookup"><span data-stu-id="d5e6d-113">From *HolographicVoiceInputSampleMain::CreateSpeechConstraintsForCurrentState*:</span></span>

```
m_speechRecognizer = ref new SpeechRecognizer();
```

<span data-ttu-id="d5e6d-114">Créez une liste de commandes vocales pour le module de reconnaissance à écouter.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-114">Create a list of speech commands for the recognizer to listen for.</span></span> <span data-ttu-id="d5e6d-115">Ici, nous créons un ensemble de commandes pour modifier la couleur d’un hologramme.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-115">Here, we construct a set of commands to change the color of a hologram.</span></span> <span data-ttu-id="d5e6d-116">Pour plus de commodité, nous créons également les données que nous allons utiliser pour les commandes ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-116">For convenience, we also create the data that we'll use for the commands later.</span></span>

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

<span data-ttu-id="d5e6d-117">Vous pouvez utiliser des mots phonétiques qui peuvent ne pas figurer dans un dictionnaire pour spécifier des commandes.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-117">You can use phonetic words that might not be in a dictionary to specify commands.</span></span>

```
m_speechCommandList->Append(StringReference(L"SpeechRecognizer"));
   m_speechCommandData.push_back(float4(0.5f, 0.1f, 1.f, 1.f));
```

<span data-ttu-id="d5e6d-118">Pour charger la liste de commandes dans la liste des contraintes pour le module de reconnaissance vocale, utilisez un objet [SpeechRecognitionListConstraint](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionlistconstraint.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d5e6d-118">To load the commands list into the list of constraints for the speech recognizer use a [SpeechRecognitionListConstraint](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionlistconstraint.aspx) object.</span></span>

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

<span data-ttu-id="d5e6d-119">Abonnez-vous à l’événement [ResultGenerated](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated.aspx) sur le [SpeechContinuousRecognitionSession](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.aspx)du module de reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-119">Subscribe to the [ResultGenerated](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.resultgenerated.aspx) event on the speech recognizer's [SpeechContinuousRecognitionSession](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionsession.aspx).</span></span> <span data-ttu-id="d5e6d-120">Cet événement avertit votre application lorsque l’une de vos commandes a été reconnue.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-120">This event notifies your app when one of your commands has been recognized.</span></span>

```
m_speechRecognizer->ContinuousRecognitionSession->ResultGenerated +=
       ref new TypedEventHandler<SpeechContinuousRecognitionSession^, SpeechContinuousRecognitionResultGeneratedEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnResultGenerated, this, _1, _2)
           );
```

<span data-ttu-id="d5e6d-121">Votre gestionnaire d’événements *OnResultGenerated* reçoit les données d’événement dans une instance [SpeechContinuousRecognitionResultGeneratedEventArgs](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d5e6d-121">Your *OnResultGenerated* event handler receives event data in a [SpeechContinuousRecognitionResultGeneratedEventArgs](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechcontinuousrecognitionresultgeneratedeventargs.aspx) instance.</span></span> <span data-ttu-id="d5e6d-122">Si la confiance est supérieure au seuil que vous avez défini, votre application doit noter que l’événement s’est produit.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-122">If the confidence is greater than the threshold that you defined, your app should note that the event happened.</span></span> <span data-ttu-id="d5e6d-123">Enregistrez les données d’événement afin de pouvoir les utiliser dans une boucle de mise à jour ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-123">Save the event data so that you can use it in a subsequent update loop.</span></span>

<span data-ttu-id="d5e6d-124">À partir de *HolographicVoiceInputSampleMain. cpp*:</span><span class="sxs-lookup"><span data-stu-id="d5e6d-124">From *HolographicVoiceInputSampleMain.cpp*:</span></span>

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

<span data-ttu-id="d5e6d-125">Dans notre exemple de code, nous modifions la couleur du cube d’hologramme en rotation en fonction de la commande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-125">In our example code, we change the color of the spinning hologram cube according to the user's command.</span></span>

<span data-ttu-id="d5e6d-126">À partir de *HolographicVoiceInputSampleMain :: Update*:</span><span class="sxs-lookup"><span data-stu-id="d5e6d-126">From *HolographicVoiceInputSampleMain::Update*:</span></span>

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

## <a name="use-one-shot-recognition"></a><span data-ttu-id="d5e6d-127">Utilisez la reconnaissance « une seule capture »</span><span class="sxs-lookup"><span data-stu-id="d5e6d-127">Use "one-shot" recognition</span></span>

<span data-ttu-id="d5e6d-128">Vous pouvez configurer un module de reconnaissance vocale pour écouter les expressions ou les phrases que l’utilisateur parle.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-128">You can configure a speech recognizer to listen for phrases or sentences that the user speaks.</span></span> <span data-ttu-id="d5e6d-129">Dans ce cas, nous appliquons un *SpeechRecognitionTopicConstraint* qui indique au module de reconnaissance vocale le type d’entrée à attendre.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-129">In this case, we apply a *SpeechRecognitionTopicConstraint* that tells the speech recognizer what type of input to expect.</span></span> <span data-ttu-id="d5e6d-130">Voici un flux de travail d’application pour ce scénario :</span><span class="sxs-lookup"><span data-stu-id="d5e6d-130">Here's an app workflow for this scenario:</span></span>
1. <span data-ttu-id="d5e6d-131">Votre application crée le SpeechRecognizer, fournit des invites d’interface utilisateur et commence à écouter une commande parlée.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-131">Your app creates the SpeechRecognizer, provides UI prompts, and starts listening for a spoken command.</span></span>
2. <span data-ttu-id="d5e6d-132">L’utilisateur parle une expression ou une phrase.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-132">The user speaks a phrase or sentence.</span></span>
3. <span data-ttu-id="d5e6d-133">La reconnaissance de la parole de l’utilisateur se produit et un résultat est renvoyé à l’application.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-133">Recognition of the user's speech occurs, and a result is returned to the app.</span></span> <span data-ttu-id="d5e6d-134">À ce stade, votre application doit fournir une invite d’interface utilisateur pour indiquer que la reconnaissance s’est produite.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-134">At this point, your app should provide a UI prompt to indicate that recognition has occurred.</span></span>
4. <span data-ttu-id="d5e6d-135">Selon le niveau de confiance auquel vous souhaitez répondre et le niveau de confiance du résultat de la reconnaissance vocale, votre application peut traiter le résultat et répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-135">Depending on the confidence level that you want to respond to and the confidence level of the speech recognition result, your app can process the result and respond as appropriate.</span></span>

<span data-ttu-id="d5e6d-136">Cette section décrit comment créer un SpeechRecognizer, compiler la contrainte et écouter les entrées vocales.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-136">This section describes how to create a SpeechRecognizer, compile the constraint, and listen for speech input.</span></span>

<span data-ttu-id="d5e6d-137">Le code suivant compile la contrainte de rubrique, qui, dans ce cas, est optimisée pour la recherche Web.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-137">The following code compiles the topic constraint, which in this case is optimized for web search.</span></span>

```
auto constraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, L"webSearch");
   m_speechRecognizer->Constraints->Clear();
   m_speechRecognizer->Constraints->Append(constraint);
   return create_task(m_speechRecognizer->CompileConstraintsAsync())
       .then([this](task<SpeechRecognitionCompilationResult^> previousTask)
   {
```

<span data-ttu-id="d5e6d-138">Si la compilation est réussie, nous pouvons continuer la reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-138">If compilation succeeds, we can proceed with speech recognition.</span></span>

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

<span data-ttu-id="d5e6d-139">Le résultat est ensuite renvoyé à l’application.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-139">The result is then returned to the app.</span></span> <span data-ttu-id="d5e6d-140">Si nous sommes suffisamment sûrs dans le résultat, nous pouvons traiter la commande.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-140">If we're confident enough in the result, we can process the command.</span></span> <span data-ttu-id="d5e6d-141">Cet exemple de code traite les résultats avec au moins une confiance moyenne.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-141">This code example processes results with at least medium confidence.</span></span>

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

<span data-ttu-id="d5e6d-142">Chaque fois que vous utilisez la reconnaissance vocale, observez les exceptions qui peuvent indiquer que l’utilisateur a désactivé le microphone dans les paramètres de confidentialité du système.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-142">Whenever you use speech recognition, watch for exceptions that could indicate that the user has turned off the microphone in the system privacy settings.</span></span> <span data-ttu-id="d5e6d-143">Cela peut se produire pendant l’initialisation ou la reconnaissance.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-143">This can happen during initialization or recognition.</span></span>

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
> <span data-ttu-id="d5e6d-144">Il existe plusieurs [SpeechRecognitionScenarios](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionscenario.aspx) prédéfinis que vous pouvez utiliser pour optimiser la reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-144">There are several predefined [SpeechRecognitionScenarios](https://msdn.microsoft.com/library/windows/apps/windows.media.speechrecognition.speechrecognitionscenario.aspx) that you can use to optimize speech recognition.</span></span>

* <span data-ttu-id="d5e6d-145">Pour optimiser la dictée, utilisez le scénario de dictée.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-145">To optimize for dictation, use the dictation scenario.</span></span><br/>
   ```
   // Compile the dictation topic constraint, which optimizes for speech dictation.
   auto dictationConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::Dictation, "dictation");
   m_speechRecognizer->Constraints->Append(dictationConstraint);
   ```

* <span data-ttu-id="d5e6d-146">Pour les recherches Web vocales, utilisez la contrainte de scénario spécifique au Web suivante.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-146">For speech web searches, use the following web-specific scenario constraint.</span></span>

   ```
   // Add a web search topic constraint to the recognizer.
   auto webSearchConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::WebSearch, "webSearch");
   speechRecognizer->Constraints->Append(webSearchConstraint);
   ```

* <span data-ttu-id="d5e6d-147">Utilisez la contrainte de formulaire pour remplir les formulaires.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-147">Use the form constraint to fill out forms.</span></span> <span data-ttu-id="d5e6d-148">Dans ce cas, il est préférable d’appliquer votre propre grammaire qui est optimisée pour remplir le formulaire.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-148">In this case, it's best to apply your own grammar that's optimized for filling out the form.</span></span>

   ```
   // Add a form constraint to the recognizer.
   auto formConstraint = ref new SpeechRecognitionTopicConstraint(SpeechRecognitionScenario::FormFilling, "formFilling");
   speechRecognizer->Constraints->Append(formConstraint );
   ```
* <span data-ttu-id="d5e6d-149">Vous pouvez fournir votre propre grammaire au format SRGS.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-149">You can provide your own grammar in the SRGS format.</span></span>

## <a name="use-continuous-recognition"></a><span data-ttu-id="d5e6d-150">Utiliser la reconnaissance continue</span><span class="sxs-lookup"><span data-stu-id="d5e6d-150">Use continuous recognition</span></span>

<span data-ttu-id="d5e6d-151">Pour le scénario de dictée continue, consultez l' [exemple de code vocal Windows 10 UWP](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpeechRecognitionAndSynthesis/cpp/Scenario_ContinuousDictation.xaml.cpp).</span><span class="sxs-lookup"><span data-stu-id="d5e6d-151">For the continuous-dictation scenario, see the [Windows 10 UWP speech code sample](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpeechRecognitionAndSynthesis/cpp/Scenario_ContinuousDictation.xaml.cpp).</span></span>

## <a name="handle-quality-degradation"></a><span data-ttu-id="d5e6d-152">Gérer la dégradation de la qualité</span><span class="sxs-lookup"><span data-stu-id="d5e6d-152">Handle quality degradation</span></span>

<span data-ttu-id="d5e6d-153">Les conditions environnementales interfèrent parfois avec la reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-153">Environmental conditions sometimes interfere with speech recognition.</span></span> <span data-ttu-id="d5e6d-154">Par exemple, la salle peut être trop bruyante ou l’utilisateur peut parler trop fort.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-154">For example, the room might be too noisy, or the user might speak too loudly.</span></span> <span data-ttu-id="d5e6d-155">Dans la mesure du possible, l’API de reconnaissance vocale fournit des informations sur les conditions à l’origine de la dégradation de la qualité.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-155">Whenever possible, the speech recognition API provides information about the conditions that caused the quality degradation.</span></span> <span data-ttu-id="d5e6d-156">Ces informations sont envoyées à votre application par le biais d’un événement WinRT.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-156">This information is pushed to your app through a WinRT event.</span></span> <span data-ttu-id="d5e6d-157">L’exemple suivant montre comment s’abonner à cet événement.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-157">The following example shows  how to subscribe to this event.</span></span>

```
m_speechRecognizer->RecognitionQualityDegrading +=
       ref new TypedEventHandler<SpeechRecognizer^, SpeechRecognitionQualityDegradingEventArgs^>(
           std::bind(&HolographicVoiceInputSampleMain::OnSpeechQualityDegraded, this, _1, _2)
           );
```

<span data-ttu-id="d5e6d-158">Dans notre exemple de code, nous écrivons les informations sur les conditions dans la console de débogage.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-158">In our code sample, we write the conditions information to the debug console.</span></span> <span data-ttu-id="d5e6d-159">Une application peut souhaiter fournir des commentaires à l’utilisateur via l’interface utilisateur, la synthèse vocale et une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-159">An app might want to provide feedback to the user through the UI, speech synthesis, and another method.</span></span> <span data-ttu-id="d5e6d-160">Ou il peut s’avérer nécessaire de se comporter différemment lorsque la reconnaissance vocale est interrompue par une réduction temporaire de la qualité.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-160">Or it might need to behave differently when speech is interrupted by a temporary reduction in quality.</span></span>

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

<span data-ttu-id="d5e6d-161">Si vous n’utilisez pas de classes Ref pour créer votre application DirectX, vous devez vous désabonner de l’événement avant de libérer ou de recréer votre reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-161">If you're not using ref classes to create your DirectX app, you must unsubscribe from the event before you release or recreate your speech recognizer.</span></span> <span data-ttu-id="d5e6d-162">HolographicSpeechPromptSample a une routine pour arrêter la reconnaissance et annuler l’abonnement aux événements.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-162">The HolographicSpeechPromptSample has a routine to stop recognition and unsubscribe from events.</span></span>

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

## <a name="use-speech-synthesis-to-provide-audible-prompts"></a><span data-ttu-id="d5e6d-163">Utiliser la synthèse vocale pour fournir des invites sonores</span><span class="sxs-lookup"><span data-stu-id="d5e6d-163">Use speech synthesis to provide audible prompts</span></span>

<span data-ttu-id="d5e6d-164">Les exemples de reconnaissance vocale holographique utilisent la synthèse vocale pour fournir des instructions audibles à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-164">The holographic speech samples use speech synthesis to provide audible instructions to the user.</span></span> <span data-ttu-id="d5e6d-165">Cette section montre comment créer un exemple de voix synthétisée, puis le relire via les API audio HRTF.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-165">This section shows how to create a synthesized voice sample  and then play it back through the HRTF audio APIs.</span></span>

<span data-ttu-id="d5e6d-166">Vous devez fournir vos propres invites vocales lorsque vous demandez une entrée de phrase.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-166">You should provide your own speech prompts when you request phrase input.</span></span> <span data-ttu-id="d5e6d-167">Les invites permettent également d’indiquer à quel moment les commandes vocales peuvent être parlées pour un scénario de reconnaissance continue.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-167">Prompts can also help indicate when speech commands can be spoken for a continuous-recognition scenario.</span></span> <span data-ttu-id="d5e6d-168">L’exemple suivant montre comment utiliser un synthétiseur vocal pour effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-168">The following example demonstrates how to use a speech synthesizer to do this.</span></span> <span data-ttu-id="d5e6d-169">Vous pouvez également utiliser un clip vocal pré-enregistré, une interface utilisateur visuelle ou un autre indicateur de ce qui doit être dit, par exemple dans les scénarios où l’invite n’est pas dynamique.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-169">You could also use a pre-recorded voice clip, a visual UI, or another indicator of what to say, for example in scenarios where the prompt is not dynamic.</span></span>

<span data-ttu-id="d5e6d-170">Tout d’abord, créez l’objet SpeechSynthesizer.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-170">First, create the SpeechSynthesizer object.</span></span>

```
auto speechSynthesizer = ref new Windows::Media::SpeechSynthesis::SpeechSynthesizer();
```

<span data-ttu-id="d5e6d-171">Vous avez également besoin d’une chaîne qui contient le texte à synthétiser.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-171">You also need a string that includes the text to  synthesize.</span></span>

```
// Phrase recognition works best when requesting a phrase or sentence.
   StringReference voicePrompt = L"At the prompt: Say a phrase, asking me to change the cube to a specific color.";
```

<span data-ttu-id="d5e6d-172">La parole est synthétisée de façon asynchrone via SynthesizeTextToStreamAsync.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-172">Speech is synthesized asynchronously through SynthesizeTextToStreamAsync.</span></span> <span data-ttu-id="d5e6d-173">Ici, nous commençons une tâche asynchrone pour synthétiser la parole.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-173">Here, we start an async task to synthesize the speech.</span></span>

```
create_task(speechSynthesizer->SynthesizeTextToStreamAsync(voicePrompt), task_continuation_context::use_current())
       .then([this, speechSynthesizer](task<Windows::Media::SpeechSynthesis::SpeechSynthesisStream^> synthesisStreamTask)
   {
       try
       {
```

<span data-ttu-id="d5e6d-174">La synthèse vocale est envoyée sous forme de flux d’octets.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-174">The speech synthesis is sent as a byte stream.</span></span> <span data-ttu-id="d5e6d-175">Nous pouvons utiliser ce flux d’octets pour initialiser une voix XAudio2.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-175">We can use that byte stream to initialize an XAudio2 voice.</span></span> <span data-ttu-id="d5e6d-176">Pour nos exemples de code holographiques, nous les relireons en tant qu’effet audio HRTF.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-176">For our holographic code samples, we play it back as an HRTF audio effect.</span></span>

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

<span data-ttu-id="d5e6d-177">Comme avec la reconnaissance vocale, la synthèse vocale lève une exception en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="d5e6d-177">As with speech recognition, speech synthesis throws an exception if something goes wrong.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="d5e6d-178">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d5e6d-178">See also</span></span>
* [<span data-ttu-id="d5e6d-179">Conception d’applications vocales</span><span class="sxs-lookup"><span data-stu-id="d5e6d-179">Speech app design</span></span>](https://msdn.microsoft.com/library/dn596121.aspx)
* [<span data-ttu-id="d5e6d-180">Exemple SpeechRecognitionAndSynthesis</span><span class="sxs-lookup"><span data-stu-id="d5e6d-180">SpeechRecognitionAndSynthesis sample</span></span>](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpeechRecognitionAndSynthesis)
