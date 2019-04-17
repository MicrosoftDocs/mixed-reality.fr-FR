---
title: Suivi de la perte dans Unity
description: Gestion du suivi de la perte d’une application Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, suivi de la perte, l’image de la perte de suivi
ms.openlocfilehash: eb675860d67e9cad0d1129b3a6f61343990a4179
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595716"
---
# <a name="tracking-loss-in-unity"></a><span data-ttu-id="92c38-104">Suivi de la perte dans Unity</span><span class="sxs-lookup"><span data-stu-id="92c38-104">Tracking loss in Unity</span></span>

<span data-ttu-id="92c38-105">Lorsque l’appareil ne peut pas localiser lui-même dans le monde, l’application rencontre « perte de suivi ».</span><span class="sxs-lookup"><span data-stu-id="92c38-105">When the device cannot locate itself in the world, the app experiences "tracking loss".</span></span> <span data-ttu-id="92c38-106">Par défaut, Unity s’interrompre la boucle de mise à jour et afficher une image de démarrage à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92c38-106">By default, Unity will pause the update loop and display a splash image to the user.</span></span> <span data-ttu-id="92c38-107">Lorsque le suivi est récupéré, l’image de démarrage disparaît et continue la boucle de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="92c38-107">When tracking is regained, the splash image goes away and the update loop continues.</span></span>

<span data-ttu-id="92c38-108">Comme alternative, l’utilisateur peut gérer manuellement cette transition en n’optant pas le paramètre.</span><span class="sxs-lookup"><span data-stu-id="92c38-108">As an alternative, the user can manually handle this transition by opting out of the setting.</span></span> <span data-ttu-id="92c38-109">Tout le contenu vous sembleront pour devenir corps verrouillés pendant le suivi de la perte si rien n’est fait pour le gérer.</span><span class="sxs-lookup"><span data-stu-id="92c38-109">All content will seem to become body locked during tracking loss if nothing is done to handle it.</span></span>

## <a name="default-handling"></a><span data-ttu-id="92c38-110">La gestion par défaut</span><span class="sxs-lookup"><span data-stu-id="92c38-110">Default Handling</span></span>

<span data-ttu-id="92c38-111">Par défaut, la boucle de mise à jour de l’application, ainsi que tous les messages et les événements s’arrête pendant la durée de suivi de la perte.</span><span class="sxs-lookup"><span data-stu-id="92c38-111">By default, the update loop of the app as well as all messages and events will stop for the duration of tracking loss.</span></span> <span data-ttu-id="92c38-112">À ce moment même, une image sera affichée à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92c38-112">At that same time, an image will be displayed to the user.</span></span> <span data-ttu-id="92c38-113">Vous pouvez personnaliser cette image en accédant à modifier -> Paramètres -> lecteur, en cliquant sur Image de démarrage et définition de l’image holographique suivi de la perte.</span><span class="sxs-lookup"><span data-stu-id="92c38-113">You can customize this image by going to Edit->Settings->Player, clicking Splash Image, and setting the Holographic Tracking Loss image.</span></span>

## <a name="manual-handling"></a><span data-ttu-id="92c38-114">Gestion manuelle</span><span class="sxs-lookup"><span data-stu-id="92c38-114">Manual Handling</span></span>

<span data-ttu-id="92c38-115">Pour gérer manuellement une perte de suivi, vous devez accéder à **modifier** > **paramètres du projet** > **Player**  >   **Onglet Paramètres de plateforme de Windows Universal** > **Image de démarrage** > **Windows HOLOGRAPHIQUE** et décochez la case « sur le suivi des pertes Pause et afficher l’Image ".</span><span class="sxs-lookup"><span data-stu-id="92c38-115">To manually handle tracking loss, you need to go to **Edit** > **Project Settings** > **Player** > **Universal Windows Platform settings tab** > **Splash Image** > **Windows Holographic** and uncheck "On Tracking Loss Pause and Show Image".</span></span> <span data-ttu-id="92c38-116">Après quoi, vous devez gérer le suivi des modifications avec les API spécifiées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="92c38-116">After which, you need to handle tracking changes with the APIs specified below.</span></span>

<span data-ttu-id="92c38-117">**Namespace :** *UnityEngine.XR.WSA*</span><span class="sxs-lookup"><span data-stu-id="92c38-117">**Namespace:** *UnityEngine.XR.WSA*</span></span><br>
<span data-ttu-id="92c38-118">**Type :** *WorldManager*</span><span class="sxs-lookup"><span data-stu-id="92c38-118">**Type:** *WorldManager*</span></span>

* <span data-ttu-id="92c38-119">World Manager expose un événement pour détecter le suivi perdu/acquise (*WorldManager.OnPositionalLocatorStateChanged*) et une propriété pour interroger l’état actuel (*WorldManager.state*)</span><span class="sxs-lookup"><span data-stu-id="92c38-119">World Manager exposes an event to detect tracking lost/gained (*WorldManager.OnPositionalLocatorStateChanged*) and a property to query the current state (*WorldManager.state*)</span></span>
* <span data-ttu-id="92c38-120">Lorsque l’état de suivi n’est pas actif, l’appareil photo n’apparaîtra pas traduire dans le monde virtuel, même si l’utilisateur est traduit.</span><span class="sxs-lookup"><span data-stu-id="92c38-120">When the tracking state is not active, the camera will not appear to translate in the virtual world even as the user translates.</span></span> <span data-ttu-id="92c38-121">Cela signifie que les objets ne sont plus correspond à n’importe quel emplacement physique et tous apparaissent corps verrouillé.</span><span class="sxs-lookup"><span data-stu-id="92c38-121">This means objects will no longer correspond to any physical location and all will appear body locked.</span></span>

<span data-ttu-id="92c38-122">Lors du traitement de suivi des modifications sur votre propre vous devez soit pour l’interrogation de la propriété state chaque frame ou la poignée de la *OnPositionalLocatorStateChanged* événement.</span><span class="sxs-lookup"><span data-stu-id="92c38-122">When handling tracking changes on your own you either need to poll for the state property each frame or handle the *OnPositionalLocatorStateChanged* event.</span></span>

### <a name="polling"></a><span data-ttu-id="92c38-123">Interrogation</span><span class="sxs-lookup"><span data-stu-id="92c38-123">Polling</span></span>

<span data-ttu-id="92c38-124">L’état plus importantes est *PositionalLocatorState.Active* ce qui signifie que le suivi est entièrement fonctionnels.</span><span class="sxs-lookup"><span data-stu-id="92c38-124">The most important state is *PositionalLocatorState.Active* which means tracking is fully functional.</span></span> <span data-ttu-id="92c38-125">N’importe quel autre état entraînent uniquement les deltas de rotation de la caméra principale.</span><span class="sxs-lookup"><span data-stu-id="92c38-125">Any other state will result in only rotational deltas to the main camera.</span></span> <span data-ttu-id="92c38-126">Exemple :</span><span class="sxs-lookup"><span data-stu-id="92c38-126">For example:</span></span>

```cs
void Update()
{
    switch (UnityEngine.XR.WSA.WorldManager.state)
    {
        case PositionalLocatorState.Active:
            // handle active
            break;
        case PositionalLocatorState.Activating:
        case PositionalLocatorState.Inhibited:
        case PositionalLocatorState.OrientationOnly:
        case PositionalLocatorState.Unavailable:
        default:
            // only rotational information is available
            break;
    }
}
```

### <a name="handling-the-onpositionallocatorstatechanged-event"></a><span data-ttu-id="92c38-127">Gestion de l’événement OnPositionalLocatorStateChanged</span><span class="sxs-lookup"><span data-stu-id="92c38-127">Handling the OnPositionalLocatorStateChanged event</span></span>

<span data-ttu-id="92c38-128">Vous pouvez également et plus facilement, vous pouvez également vous abonner à *OnPositionalLocatorStateChanged* pour gérer les transitions :</span><span class="sxs-lookup"><span data-stu-id="92c38-128">Alternatively and more conveniently, you can also subscribe to *OnPositionalLocatorStateChanged* to handle the transitions:</span></span>

```cs
void Start()
{
    UnityEngine.XR.WSA.WorldManager.OnPositionalLocatorStateChanged += WorldManager_OnPositionalLocatorStateChanged;
}

private void WorldManager_OnPositionalLocatorStateChanged(PositionalLocatorState oldState, PositionalLocatorState newState)
{
    if (newState == PositionalLocatorState.Active)
    {
        // Handle becoming active
    }
    else
    {
        // Handle becoming rotational only
    }
}
```

## <a name="see-also"></a><span data-ttu-id="92c38-129">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="92c38-129">See also</span></span>
* [<span data-ttu-id="92c38-130">Gérer le suivi de la perte dans DirectX</span><span class="sxs-lookup"><span data-stu-id="92c38-130">Handling tracking loss in DirectX</span></span>](coordinate-systems-in-directx.md#handling-tracking-loss)
