---
title: Entrée vocale
description: Didacticiel sur la configuration et l’utilisation de l’entrée vocale dans HoloLens 2 et le moteur inréel
author: hferrone
ms.author: v-haferr
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality, non réel, moteur 4, UE4, HoloLens 2, voix, entrée vocale, reconnaissance vocale, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, développement de jeux
ms.openlocfilehash: c5de0cd912674ccd681fd398fb6fe5fd345ab6f2
ms.sourcegitcommit: 1b8090ba6aed9ff128e4f32d40c96fac2e6a220b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/03/2020
ms.locfileid: "84330631"
---
# <a name="voice-input-in-unreal"></a><span data-ttu-id="84476-104">Entrée vocale en non réel</span><span class="sxs-lookup"><span data-stu-id="84476-104">Voice Input in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="84476-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="84476-105">Overview</span></span>
<span data-ttu-id="84476-106">L’entrée vocale vous permet d’interagir avec un hologramme sans avoir à utiliser des mouvements manuels et est pris en charge sur HoloLens (1re génération) et HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="84476-106">Voice input allows you to interact with a hologram without having to use hand gestures and is supported on HoloLens (1st Gen) and HoloLens 2.</span></span> <span data-ttu-id="84476-107">Il est alimenté par le même moteur qui prend en charge la reconnaissance vocale dans toutes les autres applications Windows universelles et peut ajouter une sensation naturelle à la façon dont vous interagissez en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="84476-107">It's powered by the same engine that supports speech in all other Universal Windows Apps and can add a natural feeling to the way you interact in mixed reality.</span></span> 

<span data-ttu-id="84476-108">Les fonctionnalités vocales prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="84476-108">Supported voice features include:</span></span>
- <span data-ttu-id="84476-109">[Commande SELECT](https://docs.microsoft.com/windows/mixed-reality/voice-input#the-select-command)</span><span class="sxs-lookup"><span data-stu-id="84476-109">The [Select command](https://docs.microsoft.com/windows/mixed-reality/voice-input#the-select-command)</span></span>
- [<span data-ttu-id="84476-110">Bonjour Cortana</span><span class="sxs-lookup"><span data-stu-id="84476-110">Hey, Cortana</span></span>](https://docs.microsoft.com/windows/mixed-reality/voice-input#hey-cortana)
- <span data-ttu-id="84476-111">« Regardez-le, dites-le » pour l’interaction avec les boutons et les étiquettes</span><span class="sxs-lookup"><span data-stu-id="84476-111">"See it, say it" for button and label interaction</span></span>
- <span data-ttu-id="84476-112">Dictation</span><span class="sxs-lookup"><span data-stu-id="84476-112">Dictation</span></span>

<span data-ttu-id="84476-113">Pour plus d’informations, consultez la documentation [d’entrée vocale](voice-input.md) principale.</span><span class="sxs-lookup"><span data-stu-id="84476-113">For more information, check out the main [Voice Input](voice-input.md) documentation.</span></span>

## <a name="enabling-speech-recognition"></a><span data-ttu-id="84476-114">Activation de la reconnaissance vocale</span><span class="sxs-lookup"><span data-stu-id="84476-114">Enabling Speech Recognition</span></span>

<span data-ttu-id="84476-115">Pour activer la reconnaissance vocale sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="84476-115">To enable speech recognition on HoloLens:</span></span>
1. <span data-ttu-id="84476-116">Sélectionnez **paramètres du projet > plateforme > HoloLens > fonctionnalités** et activer le **microphone**.</span><span class="sxs-lookup"><span data-stu-id="84476-116">Select **Project Settings > Platform > HoloLens > Capabilities** and enable **Microphone**.</span></span> 
2. <span data-ttu-id="84476-117">Activation de la Recogniztion vocale dans **paramètres > confidentialité > voix** et sélectionnez **anglais**.</span><span class="sxs-lookup"><span data-stu-id="84476-117">Enabled speech recogniztion in **Settings > Privacy > Speech** and select **English**.</span></span>

> [!NOTE]
> <span data-ttu-id="84476-118">La reconnaissance vocale fonctionne toujours dans la langue d’affichage Windows configurée dans l’application **paramètres** .</span><span class="sxs-lookup"><span data-stu-id="84476-118">Speech recognition always functions in the Windows display language configured in the **Settings** app.</span></span> <span data-ttu-id="84476-119">Il est recommandé d’activer également la **reconnaissance vocale en ligne** pour une qualité de service optimale.</span><span class="sxs-lookup"><span data-stu-id="84476-119">It’s recommended that you also enable **Online speech recognition** for the best service quality.</span></span>

![Paramètres de reconnaissance vocale Windows](images/unreal/speech-recognition-settings.png)

3. <span data-ttu-id="84476-121">Une boîte de dialogue s’affiche lorsque l’application commence par vous demander si vous souhaitez activer le microphone.</span><span class="sxs-lookup"><span data-stu-id="84476-121">A dialog will show up when the application first starts to ask if you want to enable the microphone.</span></span> <span data-ttu-id="84476-122">Si vous sélectionnez **Oui** , l’entrée vocale démarre dans l’application.</span><span class="sxs-lookup"><span data-stu-id="84476-122">Selecting **Yes** starts voice input in the app.</span></span>

<span data-ttu-id="84476-123">L’entrée vocale ne nécessite pas d’API Windows Mixed Reality spéciales. Il repose sur l’API existante de mappage [d’entrée](https://docs.unrealengine.com/Gameplay/Input/index.html) de moteur non réel.</span><span class="sxs-lookup"><span data-stu-id="84476-123">Voice input doesn’t require any special Windows Mixed Reality APIs; it's built on the existing Unreal Engine 4 [Input](https://docs.unrealengine.com/Gameplay/Input/index.html) mapping API.</span></span> 

## <a name="adding-speech-mappings"></a><span data-ttu-id="84476-124">Ajout de mappages vocaux</span><span class="sxs-lookup"><span data-stu-id="84476-124">Adding Speech Mappings</span></span>
<span data-ttu-id="84476-125">La connexion vocale à l’action est une étape importante lors de l’utilisation de l’entrée vocale.</span><span class="sxs-lookup"><span data-stu-id="84476-125">Connecting speech to action is an important step when using voice input.</span></span> <span data-ttu-id="84476-126">Ces mappages surveillent l’application pour les mots clés vocaux qu’un utilisateur peut prononcer, puis déclenchent une action liée.</span><span class="sxs-lookup"><span data-stu-id="84476-126">These mappings monitor the app for speech keywords that a user might say, then fire off a linked action.</span></span> <span data-ttu-id="84476-127">Vous pouvez trouver des mappages de reconnaissance vocale en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="84476-127">You can find Speech Mappings by:</span></span>
1. <span data-ttu-id="84476-128">Sélectionnez **modifier > paramètres du projet**, faites défiler jusqu’à la section **moteur** , puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="84476-128">Selecting **Edit > Project Settings**, scrolling to the **Engine** section, and clicking **Input**.</span></span>

<span data-ttu-id="84476-129">Pour ajouter un nouveau mappage de reconnaissance vocale pour une commande de saut :</span><span class="sxs-lookup"><span data-stu-id="84476-129">To add a new Speech Mapping for a jump command:</span></span>
1. <span data-ttu-id="84476-130">Cliquez sur l' **+** icône en regard d' **éléments de tableau** et remplissez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="84476-130">Click the **+** icon next to **Array elements** and fill out the following values:</span></span>
    * <span data-ttu-id="84476-131">**jumpWord** pour le nom de l' **action**</span><span class="sxs-lookup"><span data-stu-id="84476-131">**jumpWord** for **Action Name**</span></span>
    * <span data-ttu-id="84476-132">**raccourci** pour le **mot clé Speech**</span><span class="sxs-lookup"><span data-stu-id="84476-132">**jump** for **Speech Keyword**</span></span>

> [!NOTE]
> <span data-ttu-id="84476-133">Vous pouvez utiliser n’importe quel mot ou phrase (s) en anglais comme mot clé.</span><span class="sxs-lookup"><span data-stu-id="84476-133">Any English word(s) or short sentence(s) can be used as a keyword.</span></span> 

![Positions d’entrée du moteur UE4](images/unreal/engine-input.png)

<span data-ttu-id="84476-135">Les mappages vocaux peuvent être utilisés en tant que composants d’entrée comme les mappages d’action ou d’axe ou en tant que nœuds de plan dans le graphique d’événements.</span><span class="sxs-lookup"><span data-stu-id="84476-135">Speech Mappings can be used as Input components like Action or Axis Mappings or as blueprint nodes in the Event Graph.</span></span> <span data-ttu-id="84476-136">Par exemple, vous pouvez lier la commande Jump pour imprimer deux journaux différents selon le moment où le mot est parlé :</span><span class="sxs-lookup"><span data-stu-id="84476-136">For example, you could link the jump command to print out two different logs depending on when the word is spoken:</span></span>

1. <span data-ttu-id="84476-137">Double-cliquez sur un plan pour l’ouvrir dans le **graphique des événements**.</span><span class="sxs-lookup"><span data-stu-id="84476-137">Double-click a blueprint to open it in the **Event Graph**.</span></span>
2. <span data-ttu-id="84476-138">**Cliquez avec le bouton droit** et recherchez le **nom d’action** de votre mappage de reconnaissance vocale (dans le cas présent **jumpWord**), puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="84476-138">**Right-click** and search for the **Action Name** of your speech mapping (in this case **jumpWord**), then hit **Enter**.</span></span> <span data-ttu-id="84476-139">Cela ajoute un nœud **d’action d’entrée** au graphique.</span><span class="sxs-lookup"><span data-stu-id="84476-139">This adds an **Input Action** node to the graph.</span></span>
3. <span data-ttu-id="84476-140">Faites glisser et déposez le code PIN **appuyé** pour imprimer le nœud de **chaîne** comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="84476-140">Drag and drop the **Pressed** pin to **Print String** node as shown in the image below.</span></span> <span data-ttu-id="84476-141">Vous pouvez faire en sorte que le code confidentiel **libéré** soit vide. il n’exécutera rien pour les mappages vocaux.</span><span class="sxs-lookup"><span data-stu-id="84476-141">You can leave the **Released** pin empty, it won't execute anything for speech mappings.</span></span>
 
![Action simple pour la voix](images/unreal/voice-input-img-03.png)

4. <span data-ttu-id="84476-143">Lisez l’application, disons le mot **Jump** et regardez la console imprimer les journaux !</span><span class="sxs-lookup"><span data-stu-id="84476-143">Play the app, say the word **jump** and watch the console print out the logs!</span></span>

<span data-ttu-id="84476-144">C’est tout ce dont vous avez besoin pour commencer à ajouter des entrées vocales à vos applications HoloLens en toute situation.</span><span class="sxs-lookup"><span data-stu-id="84476-144">That's all the setup you'll need to start adding voice input to your HoloLens apps in Unreal.</span></span> <span data-ttu-id="84476-145">Vous trouverez plus d’informations sur la voix et l’interactivité dans les liens ci-dessous, et veillez à réfléchir à l’expérience que vous créez pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="84476-145">You can find more information on speech and interactivity can be found at the links below, and be sure to think about the experience you're creating for your users.</span></span>

## <a name="see-also"></a><span data-ttu-id="84476-146">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="84476-146">See also</span></span>
* [<span data-ttu-id="84476-147">Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="84476-147">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="84476-148">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="84476-148">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="84476-149">Réalité mixte - Entrées - Cours 212 : Voix</span><span class="sxs-lookup"><span data-stu-id="84476-149">MR Input 212: Voice</span></span>](holograms-212.md)
