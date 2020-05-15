---
title: Codes QR dans Unreal
description: Guide d’utilisation des codes QR dans Unreal
author: sw5813
ms.author: jacksonf
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, codes qr
ms.openlocfilehash: 67a3a8092ab908cba6768e92ed6a0e7bd2737275
ms.sourcegitcommit: 5b802078090700e06630c8fc665fedeaa0a16eb7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83342657"
---
# <a name="qr-codes-in-unreal"></a><span data-ttu-id="3b737-104">Codes QR dans Unreal</span><span class="sxs-lookup"><span data-stu-id="3b737-104">QR codes in Unreal</span></span>

<span data-ttu-id="3b737-105">HoloLens peut localiser les codes QR dans l’espace universel afin d’afficher des hologrammes à des positions connues dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="3b737-105">HoloLens can locate QR codes in world space to render holograms at known positions in the real world.</span></span>  <span data-ttu-id="3b737-106">Cela permet également d’afficher des hologrammes sur plusieurs appareils à la même position pour créer une expérience partagée.</span><span class="sxs-lookup"><span data-stu-id="3b737-106">This can also be used to render holograms on multiple devices in the same location to create a shared experience.</span></span> 

<span data-ttu-id="3b737-107">Pour activer la détection QR sur HoloLens, vérifiez que la fonctionnalité « Webcam » est cochée dans l’éditeur Unreal sous Project Settings > Platform > HoloLens > Capabilities.</span><span class="sxs-lookup"><span data-stu-id="3b737-107">To enable QR detection on HoloLens, ensure the “Webcam” capability is checked in the Unreal editor under Project Settings > Platform > HoloLens > Capabilities.</span></span>  

<span data-ttu-id="3b737-108">Acceptez l’utilisation du suivi des codes QR dans Unreal en démarrant une ARSession avec la fonction StartARSession.</span><span class="sxs-lookup"><span data-stu-id="3b737-108">Opt into using QR code tracking in Unreal by starting an ARSession with the StartARSession function.</span></span> 

<span data-ttu-id="3b737-109">Les codes QR sont exposés sous forme d’image suivie par le biais du système de géométrie suivie AR dans Unreal.</span><span class="sxs-lookup"><span data-stu-id="3b737-109">QR Codes are surfaced through Unreal’s AR tracked geometry system as a tracked image.</span></span>  <span data-ttu-id="3b737-110">Pour utiliser cette fonctionnalité, ajoutez un composant ARTrackableNotify à un acteur Blueprint :</span><span class="sxs-lookup"><span data-stu-id="3b737-110">To use this, add an AR Trackable Notify component to a Blueprint actor:</span></span> 

![Composant ARTrackableNotify QR](images/unreal-spatialmapping-artrackablenotify.PNG)

<span data-ttu-id="3b737-112">Ensuite, accédez aux détails du composant et cliquez sur le bouton « + » vert dans les événements à surveiller.</span><span class="sxs-lookup"><span data-stu-id="3b737-112">Then go to the component’s details and click on the green “+” button on the events to monitor.</span></span>  

![Événements QR](images/unreal-spatialmapping-events.PNG)

<span data-ttu-id="3b737-114">Ici, nous avons un abonnement à OnUpdateTrackedImage pour afficher un point au centre d’un code QR et imprimer les données encodées du code QR.</span><span class="sxs-lookup"><span data-stu-id="3b737-114">Here, we have subscribed to OnUpdateTrackedImage to render a point in the center of a QR Code and print the QR code’s encoded data.</span></span> 

![Exemple d’affichage QR](images/unreal-qr-render.PNG)

<span data-ttu-id="3b737-116">Tout d’abord, convertissez l’image suivie en ARTrackedQRCode pour vérifier que l’image mise à jour actuelle est un code QR.</span><span class="sxs-lookup"><span data-stu-id="3b737-116">First cast the tracked image to an ARTrackedQRCode to verify that the current updated image is a QR code.</span></span>  <span data-ttu-id="3b737-117">Les données encodées peuvent ensuite être récupérées avec la variable QRCode.</span><span class="sxs-lookup"><span data-stu-id="3b737-117">Then the encoded data can be retrieved with the QRCode variable.</span></span>  <span data-ttu-id="3b737-118">La partie en haut à gauche du code QR peut être récupérée de la position de GetLocalToWorldTransform.</span><span class="sxs-lookup"><span data-stu-id="3b737-118">The top-left of the QR code can be retrieved from the location of GetLocalToWorldTransform.</span></span>  <span data-ttu-id="3b737-119">Les dimensions peuvent être récupérées avec GetEstimateSize.</span><span class="sxs-lookup"><span data-stu-id="3b737-119">The dimensions can be retrieved with GetEstimateSize.</span></span> 

<span data-ttu-id="3b737-120">Par ailleurs, chaque code QR a un identificateur GUID unique :</span><span class="sxs-lookup"><span data-stu-id="3b737-120">Every QR code also has a unique guid ID:</span></span> 

![GUID QR](images/unreal-qr-guid.PNG)

## <a name="see-also"></a><span data-ttu-id="3b737-122">Voir également</span><span class="sxs-lookup"><span data-stu-id="3b737-122">See also</span></span>
* [<span data-ttu-id="3b737-123">Suivi des codes QR</span><span class="sxs-lookup"><span data-stu-id="3b737-123">QR code tracking</span></span>](qr-code-tracking.md)
