---
title: Entrée vocale
description: Didacticiel sur la configuration et l’utilisation de l’entrée vocale dans HoloLens 2 et le moteur inréel
author: hferrone
ms.author: v-haferr
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality, non réel, moteur 4, UE4, HoloLens 2, voix, entrée vocale, reconnaissance vocale, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, développement de jeux
ms.openlocfilehash: 134a8c5bbeb700a973d3732d24fa9078feb568ef
ms.sourcegitcommit: 7f50210b71a65631fd1bc3fdb215064e0db34333
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84551785"
---
# <a name="voice-input-in-unreal"></a><span data-ttu-id="6c57e-104">Entrée vocale en non réel</span><span class="sxs-lookup"><span data-stu-id="6c57e-104">Voice Input in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="6c57e-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="6c57e-105">Overview</span></span>
<span data-ttu-id="6c57e-106">Les entrées vocales en temps réel vous permettent d’interagir avec un hologramme sans avoir à utiliser des mouvements manuels et n’est pris en charge que pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="6c57e-106">Voice input in Unreal allows you to interact with a hologram without having to use hand gestures and is only supported HoloLens 2.</span></span> <span data-ttu-id="6c57e-107">Même si l’entrée vocale sur HoloLens 2 est alimentée par le même moteur qui prend en charge la reconnaissance vocale dans toutes les autres applications Windows universelles, inréel utilise un moteur plus limité qui lui est propre pour traiter l’entrée vocale.</span><span class="sxs-lookup"><span data-stu-id="6c57e-107">Even though voice input on HoloLens 2 is powered by the same engine that supports speech in all other Universal Windows Apps, Unreal uses a more limited engine of its own to process voice input.</span></span> <span data-ttu-id="6c57e-108">Cela limite les fonctionnalités d’entrée vocales dans des mappages de reconnaissance vocale non réels, qui sont traités dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="6c57e-108">This limits voice input features in Unreal to predefined speech mappings, which is covered in the following sections.</span></span> 

## <a name="enabling-speech-recognition"></a><span data-ttu-id="6c57e-109">Activation de la reconnaissance vocale</span><span class="sxs-lookup"><span data-stu-id="6c57e-109">Enabling Speech Recognition</span></span>

<span data-ttu-id="6c57e-110">Pour activer la reconnaissance vocale sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="6c57e-110">To enable speech recognition on HoloLens:</span></span>
1. <span data-ttu-id="6c57e-111">Sélectionnez **paramètres du projet > plateforme > HoloLens > fonctionnalités** et activer le **microphone**.</span><span class="sxs-lookup"><span data-stu-id="6c57e-111">Select **Project Settings > Platform > HoloLens > Capabilities** and enable **Microphone**.</span></span> 
2. <span data-ttu-id="6c57e-112">Activez la reconnaissance vocale dans **paramètres > confidentialité > voix** et sélectionnez **anglais**.</span><span class="sxs-lookup"><span data-stu-id="6c57e-112">Enabled speech recognition in **Settings > Privacy > Speech** and select **English**.</span></span>

> [!NOTE]
> <span data-ttu-id="6c57e-113">La reconnaissance vocale fonctionne toujours dans la langue d’affichage Windows configurée dans l’application **paramètres** .</span><span class="sxs-lookup"><span data-stu-id="6c57e-113">Speech recognition always functions in the Windows display language configured in the **Settings** app.</span></span> <span data-ttu-id="6c57e-114">Il est recommandé d’activer également la **reconnaissance vocale en ligne** pour une qualité de service optimale.</span><span class="sxs-lookup"><span data-stu-id="6c57e-114">It’s recommended that you also enable **Online speech recognition** for the best service quality.</span></span>

![Paramètres de reconnaissance vocale Windows](images/unreal/speech-recognition-settings.png)

3. <span data-ttu-id="6c57e-116">Une boîte de dialogue s’affiche lorsque l’application commence par vous demander si vous souhaitez activer le microphone.</span><span class="sxs-lookup"><span data-stu-id="6c57e-116">A dialog will show up when the application first starts to ask if you want to enable the microphone.</span></span> <span data-ttu-id="6c57e-117">Si vous sélectionnez **Oui** , l’entrée vocale démarre dans l’application.</span><span class="sxs-lookup"><span data-stu-id="6c57e-117">Selecting **Yes** starts voice input in the app.</span></span>

<span data-ttu-id="6c57e-118">L’entrée vocale ne nécessite pas d’API Windows Mixed Reality spéciales. Il repose sur l’API existante de mappage [d’entrée](https://docs.unrealengine.com/Gameplay/Input/index.html) de moteur non réel.</span><span class="sxs-lookup"><span data-stu-id="6c57e-118">Voice input doesn’t require any special Windows Mixed Reality APIs; it's built on the existing Unreal Engine 4 [Input](https://docs.unrealengine.com/Gameplay/Input/index.html) mapping API.</span></span> 

## <a name="adding-speech-mappings"></a><span data-ttu-id="6c57e-119">Ajout de mappages vocaux</span><span class="sxs-lookup"><span data-stu-id="6c57e-119">Adding Speech Mappings</span></span>
<span data-ttu-id="6c57e-120">La connexion vocale à l’action est une étape importante lors de l’utilisation de l’entrée vocale.</span><span class="sxs-lookup"><span data-stu-id="6c57e-120">Connecting speech to action is an important step when using voice input.</span></span> <span data-ttu-id="6c57e-121">Ces mappages surveillent l’application pour les mots clés vocaux qu’un utilisateur peut prononcer, puis déclenchent une action liée.</span><span class="sxs-lookup"><span data-stu-id="6c57e-121">These mappings monitor the app for speech keywords that a user might say, then fire off a linked action.</span></span> <span data-ttu-id="6c57e-122">Vous pouvez trouver des mappages de reconnaissance vocale en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c57e-122">You can find Speech Mappings by:</span></span>
1. <span data-ttu-id="6c57e-123">Sélectionnez **modifier > paramètres du projet**, faites défiler jusqu’à la section **moteur** , puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="6c57e-123">Selecting **Edit > Project Settings**, scrolling to the **Engine** section, and clicking **Input**.</span></span>

<span data-ttu-id="6c57e-124">Pour ajouter un nouveau mappage de reconnaissance vocale pour une commande de saut :</span><span class="sxs-lookup"><span data-stu-id="6c57e-124">To add a new Speech Mapping for a jump command:</span></span>
1. <span data-ttu-id="6c57e-125">Cliquez sur l' **+** icône en regard d' **éléments de tableau** et remplissez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c57e-125">Click the **+** icon next to **Array elements** and fill out the following values:</span></span>
    * <span data-ttu-id="6c57e-126">**jumpWord** pour le nom de l' **action**</span><span class="sxs-lookup"><span data-stu-id="6c57e-126">**jumpWord** for **Action Name**</span></span>
    * <span data-ttu-id="6c57e-127">**raccourci** pour le **mot clé Speech**</span><span class="sxs-lookup"><span data-stu-id="6c57e-127">**jump** for **Speech Keyword**</span></span>

> [!NOTE]
> <span data-ttu-id="6c57e-128">Vous pouvez utiliser n’importe quel mot ou phrase (s) en anglais comme mot clé.</span><span class="sxs-lookup"><span data-stu-id="6c57e-128">Any English word(s) or short sentence(s) can be used as a keyword.</span></span> 

![Paramètres d’entrée du moteur UE4](images/unreal/engine-input.png)

<span data-ttu-id="6c57e-130">Les mappages vocaux peuvent être utilisés en tant que composants d’entrée comme les mappages d’action ou d’axe ou en tant que nœuds de plan dans le graphique d’événements.</span><span class="sxs-lookup"><span data-stu-id="6c57e-130">Speech Mappings can be used as Input components like Action or Axis Mappings or as blueprint nodes in the Event Graph.</span></span> <span data-ttu-id="6c57e-131">Par exemple, vous pouvez lier la commande Jump pour imprimer deux journaux différents selon le moment où le mot est parlé :</span><span class="sxs-lookup"><span data-stu-id="6c57e-131">For example, you could link the jump command to print out two different logs depending on when the word is spoken:</span></span>

1. <span data-ttu-id="6c57e-132">Double-cliquez sur un plan pour l’ouvrir dans le **graphique des événements**.</span><span class="sxs-lookup"><span data-stu-id="6c57e-132">Double-click a blueprint to open it in the **Event Graph**.</span></span>
2. <span data-ttu-id="6c57e-133">**Cliquez avec le bouton droit** et recherchez le **nom d’action** de votre mappage de reconnaissance vocale (dans le cas présent **jumpWord**), puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="6c57e-133">**Right-click** and search for the **Action Name** of your speech mapping (in this case **jumpWord**), then hit **Enter**.</span></span> <span data-ttu-id="6c57e-134">Cela ajoute un nœud **d’action d’entrée** au graphique.</span><span class="sxs-lookup"><span data-stu-id="6c57e-134">This adds an **Input Action** node to the graph.</span></span>
3. <span data-ttu-id="6c57e-135">Faites glisser et déposez le code PIN **appuyé** pour imprimer le nœud de **chaîne** comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6c57e-135">Drag and drop the **Pressed** pin to **Print String** node as shown in the image below.</span></span> <span data-ttu-id="6c57e-136">Vous pouvez faire en sorte que le code confidentiel **libéré** soit vide. il n’exécutera rien pour les mappages vocaux.</span><span class="sxs-lookup"><span data-stu-id="6c57e-136">You can leave the **Released** pin empty, it won't execute anything for speech mappings.</span></span>
 
![Action simple pour la voix](images/unreal/voice-input-img-03.png)

4. <span data-ttu-id="6c57e-138">Lisez l’application, disons le mot **Jump** et regardez la console imprimer les journaux !</span><span class="sxs-lookup"><span data-stu-id="6c57e-138">Play the app, say the word **jump** and watch the console print out the logs!</span></span>

<span data-ttu-id="6c57e-139">C’est tout ce dont vous avez besoin pour commencer à ajouter des entrées vocales à vos applications HoloLens en toute situation.</span><span class="sxs-lookup"><span data-stu-id="6c57e-139">That's all the setup you'll need to start adding voice input to your HoloLens apps in Unreal.</span></span> <span data-ttu-id="6c57e-140">Vous trouverez plus d’informations sur la voix et l’interactivité dans les liens ci-dessous, et veillez à réfléchir à l’expérience que vous créez pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6c57e-140">You can find more information on speech and interactivity can be found at the links below, and be sure to think about the experience you're creating for your users.</span></span>

## <a name="see-also"></a><span data-ttu-id="6c57e-141">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6c57e-141">See also</span></span>
* [<span data-ttu-id="6c57e-142">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="6c57e-142">Voice Input</span></span>](voice-input.md)
* [<span data-ttu-id="6c57e-143">Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="6c57e-143">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="6c57e-144">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="6c57e-144">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="6c57e-145">Réalité mixte - Entrées - Cours 212 : Voix</span><span class="sxs-lookup"><span data-stu-id="6c57e-145">MR Input 212: Voice</span></span>](holograms-212.md)

