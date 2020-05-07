---
title: Entrée vocale
description: Explique comment utiliser l’entrée vocale
author: AndreyChistyakov
ms.author: anchisty
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality, HoloLens
ms.openlocfilehash: d61a9f9d40c76c8872ff0a1b39d65f95ae88d2b7
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82835307"
---
# <a name="voice-input"></a><span data-ttu-id="24cd3-104">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="24cd3-104">Voice Input</span></span>

<span data-ttu-id="24cd3-105">Pour activer la reconnaissance vocale sur HoloLens, le développeur doit activer « microphone » dans l’éditeur non réel sous paramètres du projet > fonctionnalités de la plateforme > HoloLens >.</span><span class="sxs-lookup"><span data-stu-id="24cd3-105">To enable speech recognition on HoloLens, the developer needs to enable “Microphone” in the Unreal editor under Project Settings > Platform > HoloLens > Capabilities.</span></span> <span data-ttu-id="24cd3-106">La reconnaissance vocale de l’appareil doit également être activée dans paramètres > confidentialité > vocale et utilisez la langue anglaise.</span><span class="sxs-lookup"><span data-stu-id="24cd3-106">The device must also have Speech recognition enabled in Settings > Privacy > Speech and use the English language.</span></span>

![Paramètres de reconnaissance vocale Windows](images/unreal/speech-recognition-settings.png)

<span data-ttu-id="24cd3-108">Il est recommandé d’activer la reconnaissance vocale en ligne pour la meilleure qualité possible du service.</span><span class="sxs-lookup"><span data-stu-id="24cd3-108">It’s recommended to enable Online speech recognition too for the best possible quality of the service.</span></span> <span data-ttu-id="24cd3-109">Vous trouverez des détails techniques sur la reconnaissance vocale sur HoloLens [ici](voice-input.md) .</span><span class="sxs-lookup"><span data-stu-id="24cd3-109">Technical details for speech recognition on HoloLens can be found [here](voice-input.md)</span></span>

<span data-ttu-id="24cd3-110">L’utilisateur verra alors s’afficher une boîte de dialogue sur l’activation du microphone lors du premier démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="24cd3-110">Then user will see a dialog about enabling the microphone when the application first starts.</span></span> <span data-ttu-id="24cd3-111">Si un utilisateur sélectionne Oui, l’application commence à obtenir une entrée vocale.</span><span class="sxs-lookup"><span data-stu-id="24cd3-111">If a user selects Yes, the application will begin getting voice input.</span></span>

<span data-ttu-id="24cd3-112">L’entrée vocale ne nécessite pas d’API de réalité mixte Windows spéciale et s’appuie plutôt sur l’API existante de mappage d’entrée de moteur non réel.</span><span class="sxs-lookup"><span data-stu-id="24cd3-112">Speech input doesn’t require a special Windows Mixed Reality API and is instead built upon the existing Unreal Engine 4 Input mapping API.</span></span> <span data-ttu-id="24cd3-113">Pour plus d’informations sur l’utilisation de l' [here](https://docs.unrealengine.com/en-US/Gameplay/Input/index.html) API d’entrée, consultez</span><span class="sxs-lookup"><span data-stu-id="24cd3-113">Details on how to use the Input API are [here](https://docs.unrealengine.com/en-US/Gameplay/Input/index.html)</span></span>

<span data-ttu-id="24cd3-114">Les mappages de reconnaissance vocale ont été ajoutés à la section liaisons du moteur – entrée sous les mappages action et axe.</span><span class="sxs-lookup"><span data-stu-id="24cd3-114">Speech Mappings have been added to the Bindings section of Engine – Input below Action and Axis Mappings.</span></span> 

![Positions d’entrée du moteur UE4](images/unreal/engine-input.png)
 
<span data-ttu-id="24cd3-116">Voici un exemple de la surveillance ajoutée pour le « Jump » universel.</span><span class="sxs-lookup"><span data-stu-id="24cd3-116">Here is an example of added monitoring for the world “jump”.</span></span> <span data-ttu-id="24cd3-117">Vous pouvez utiliser n’importe quel mot ou phrase en anglais.</span><span class="sxs-lookup"><span data-stu-id="24cd3-117">Any English word(s) or short sentences can be used.</span></span> 

<span data-ttu-id="24cd3-118">Après l’ajout d’un mappage vocal via les paramètres du projet, un développeur peut alors utiliser une logique inhabituelle standard pour gérer l’entrée, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="24cd3-118">After a Speech Mapping is added via Project Settings, a developer can then use standard Unreal logic to handle the input, as in the following example:</span></span> 
 
![Action simple pour la voix](images/unreal/input-action-bp.png)
