---
title: Suivi des pertes dans Unity
description: Gestion des pertes de suivi dans une application Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, perte de suivi, image de perte de suivi
ms.openlocfilehash: eb675860d67e9cad0d1129b3a6f61343990a4179
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63548741"
---
# <a name="tracking-loss-in-unity"></a><span data-ttu-id="09aa2-104">Suivi des pertes dans Unity</span><span class="sxs-lookup"><span data-stu-id="09aa2-104">Tracking loss in Unity</span></span>

<span data-ttu-id="09aa2-105">Lorsque l’appareil ne peut pas se trouver dans le monde entier, l’application rencontre une «perte de suivi».</span><span class="sxs-lookup"><span data-stu-id="09aa2-105">When the device cannot locate itself in the world, the app experiences "tracking loss".</span></span> <span data-ttu-id="09aa2-106">Par défaut, Unity met en pause la boucle de mise à jour et affiche une image de démarrage pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="09aa2-106">By default, Unity will pause the update loop and display a splash image to the user.</span></span> <span data-ttu-id="09aa2-107">Lorsque le suivi est retrouvé, l’image de démarrage disparaît et la boucle de mise à jour se poursuit.</span><span class="sxs-lookup"><span data-stu-id="09aa2-107">When tracking is regained, the splash image goes away and the update loop continues.</span></span>

<span data-ttu-id="09aa2-108">En guise d’alternative, l’utilisateur peut gérer manuellement cette transition en désactivant le paramètre.</span><span class="sxs-lookup"><span data-stu-id="09aa2-108">As an alternative, the user can manually handle this transition by opting out of the setting.</span></span> <span data-ttu-id="09aa2-109">Tout le contenu semblera être verrouillé pendant le suivi de la perte si rien n’est fait pour le gérer.</span><span class="sxs-lookup"><span data-stu-id="09aa2-109">All content will seem to become body locked during tracking loss if nothing is done to handle it.</span></span>

## <a name="default-handling"></a><span data-ttu-id="09aa2-110">Gestion par défaut</span><span class="sxs-lookup"><span data-stu-id="09aa2-110">Default Handling</span></span>

<span data-ttu-id="09aa2-111">Par défaut, la boucle de mise à jour de l’application, ainsi que tous les messages et événements, s’arrête pendant la durée du suivi des pertes.</span><span class="sxs-lookup"><span data-stu-id="09aa2-111">By default, the update loop of the app as well as all messages and events will stop for the duration of tracking loss.</span></span> <span data-ttu-id="09aa2-112">En même temps, une image sera affichée à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="09aa2-112">At that same time, an image will be displayed to the user.</span></span> <span data-ttu-id="09aa2-113">Vous pouvez personnaliser cette image en accédant à modifier > Paramètres-> Player, en cliquant sur image de l’écran de démarrage et en définissant l’image de perte de suivi holographique.</span><span class="sxs-lookup"><span data-stu-id="09aa2-113">You can customize this image by going to Edit->Settings->Player, clicking Splash Image, and setting the Holographic Tracking Loss image.</span></span>

## <a name="manual-handling"></a><span data-ttu-id="09aa2-114">Gestion manuelle</span><span class="sxs-lookup"><span data-stu-id="09aa2-114">Manual Handling</span></span>

<span data-ttu-id="09aa2-115">Pour gérer manuellement le suivi des pertes, vous devez accéder à **modifier** > les**paramètres** > du projet**lecteur** > **plateforme Windows universelle onglet** > paramètres**image** dedémarrage >  **Windows holographique** et décochez «en cas de suspension du suivi et d’affichage de l’image».</span><span class="sxs-lookup"><span data-stu-id="09aa2-115">To manually handle tracking loss, you need to go to **Edit** > **Project Settings** > **Player** > **Universal Windows Platform settings tab** > **Splash Image** > **Windows Holographic** and uncheck "On Tracking Loss Pause and Show Image".</span></span> <span data-ttu-id="09aa2-116">Après quoi, vous devez gérer les modifications de suivi avec les API spécifiées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="09aa2-116">After which, you need to handle tracking changes with the APIs specified below.</span></span>

<span data-ttu-id="09aa2-117">**Espace de noms :** *UnityEngine. XR. WSA*</span><span class="sxs-lookup"><span data-stu-id="09aa2-117">**Namespace:** *UnityEngine.XR.WSA*</span></span><br>
<span data-ttu-id="09aa2-118">**Type :** *WorldManager*</span><span class="sxs-lookup"><span data-stu-id="09aa2-118">**Type:** *WorldManager*</span></span>

* <span data-ttu-id="09aa2-119">World Manager expose un événement pour détecter le suivi des pertes/gains (*WorldManager. OnPositionalLocatorStateChanged*) et une propriété pour interroger l’état actuel (*WorldManager. State*)</span><span class="sxs-lookup"><span data-stu-id="09aa2-119">World Manager exposes an event to detect tracking lost/gained (*WorldManager.OnPositionalLocatorStateChanged*) and a property to query the current state (*WorldManager.state*)</span></span>
* <span data-ttu-id="09aa2-120">Lorsque l’état de suivi n’est pas actif, l’appareil photo n’apparaît pas dans le monde virtuel, même lorsque l’utilisateur se traduit.</span><span class="sxs-lookup"><span data-stu-id="09aa2-120">When the tracking state is not active, the camera will not appear to translate in the virtual world even as the user translates.</span></span> <span data-ttu-id="09aa2-121">Cela signifie que les objets ne correspondent plus à aucun emplacement physique et que tous les corps sont verrouillés.</span><span class="sxs-lookup"><span data-stu-id="09aa2-121">This means objects will no longer correspond to any physical location and all will appear body locked.</span></span>

<span data-ttu-id="09aa2-122">Lors du traitement des modifications de suivi, vous devez interroger la propriété d’état de chaque trame ou gérer l’événement *OnPositionalLocatorStateChanged* .</span><span class="sxs-lookup"><span data-stu-id="09aa2-122">When handling tracking changes on your own you either need to poll for the state property each frame or handle the *OnPositionalLocatorStateChanged* event.</span></span>

### <a name="polling"></a><span data-ttu-id="09aa2-123">Interrogation</span><span class="sxs-lookup"><span data-stu-id="09aa2-123">Polling</span></span>

<span data-ttu-id="09aa2-124">L’état le plus important est *PositionalLocatorState. active* , ce qui signifie que le suivi est entièrement fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="09aa2-124">The most important state is *PositionalLocatorState.Active* which means tracking is fully functional.</span></span> <span data-ttu-id="09aa2-125">Tous les autres États entraînent uniquement des deltas de rotation vers la caméra principale.</span><span class="sxs-lookup"><span data-stu-id="09aa2-125">Any other state will result in only rotational deltas to the main camera.</span></span> <span data-ttu-id="09aa2-126">Exemple :</span><span class="sxs-lookup"><span data-stu-id="09aa2-126">For example:</span></span>

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

### <a name="handling-the-onpositionallocatorstatechanged-event"></a><span data-ttu-id="09aa2-127">Gestion de l’événement OnPositionalLocatorStateChanged</span><span class="sxs-lookup"><span data-stu-id="09aa2-127">Handling the OnPositionalLocatorStateChanged event</span></span>

<span data-ttu-id="09aa2-128">En guise d’alternative et de commodité, vous pouvez également vous abonner à *OnPositionalLocatorStateChanged* pour gérer les transitions:</span><span class="sxs-lookup"><span data-stu-id="09aa2-128">Alternatively and more conveniently, you can also subscribe to *OnPositionalLocatorStateChanged* to handle the transitions:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="09aa2-129">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="09aa2-129">See also</span></span>
* [<span data-ttu-id="09aa2-130">Gestion des pertes de suivi dans DirectX</span><span class="sxs-lookup"><span data-stu-id="09aa2-130">Handling tracking loss in DirectX</span></span>](coordinate-systems-in-directx.md#handling-tracking-loss)
