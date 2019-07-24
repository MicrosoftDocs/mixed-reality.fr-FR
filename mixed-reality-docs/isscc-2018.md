---
title: Livre blanc profondeur de l’appareil photo-ISSCC 2018
description: Livre blanc technique traitant de la caméra de profondeur à utiliser dans Project Kinect pour Azure et la prochaine version de HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 7/5/2018
ms.topic: article
keywords: événement, ISCC, vision par ordinateur, recherche, Kinect, hololens, Depth, tof
ms.openlocfilehash: b692f9deeb7768e57ab6161b2c356a6610f18ed9
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63516899"
---
# <a name="depth-camera-whitepaper---isscc-2018"></a><span data-ttu-id="a1dda-104">Livre blanc profondeur de l’appareil photo-ISSCC 2018</span><span class="sxs-lookup"><span data-stu-id="a1dda-104">Depth camera whitepaper - ISSCC 2018</span></span>

<span data-ttu-id="a1dda-105">**Bonhomme** 1Mpixel 65nm BSI 320MHz a démodulé le capteur d’images TOF avec des pixels d’obturateur global 3,5 μm et des compartimentage analogiques</span><span class="sxs-lookup"><span data-stu-id="a1dda-105">**Title:** 1Mpixel 65nm BSI 320MHz Demodulated TOF Image Sensor with 3.5μm Global Shutter Pixels and Analog Binning</span></span>

<span data-ttu-id="a1dda-106">**Contributeurs** Cyrus S Bamji, swati Mehta, Barry Thompson, Tamer elkhatib, Stefan Wurster, Onur Akkaya, Andrew Payne, John Godbaz, Mike Fenton, Vijay Rajasekaran, Larry Prather, Satya Nagaraja, Vishali Mogallapu, de la neige, Rich McCauley, Mustansir mukadam, Iskender agi, Shaun McCarthy, Zhanping Xu, Travis Perry, William Qian, VEI-Han Chan, Prabhu Adepu, Gazi Ali, Muneeb Ahmed, Aditya Mukherjee, Sheethal Nayak, Dave Gampell, Sunil Acharya, Lou Kordus, Pat O’Connor</span><span class="sxs-lookup"><span data-stu-id="a1dda-106">**Contributors:** Cyrus S Bamji, Swati Mehta, Barry Thompson, Tamer Elkhatib, Stefan Wurster, Onur Akkaya, Andrew Payne, John Godbaz, Mike Fenton, Vijay Rajasekaran, Larry Prather, Satya Nagaraja, Vishali Mogallapu, Dane Snow, Rich McCauley, Mustansir Mukadam, Iskender Agi, Shaun McCarthy, Zhanping Xu, Travis Perry, William Qian, Vei-Han Chan, Prabhu Adepu, Gazi Ali, Muneeb Ahmed, Aditya Mukherjee, Sheethal Nayak, Dave Gampell, Sunil Acharya, Lou Kordus, Pat O'Connor</span></span>

<span data-ttu-id="a1dda-107">**Présenté à ISSCC 2018 et publié dans ISSCC deg. Amateurs. Documents, février 2018.**</span><span class="sxs-lookup"><span data-stu-id="a1dda-107">**Presented at ISSCC 2018 and published in ISSCC Deg. Tech. Papers, Feb 2018.**</span></span>

<span data-ttu-id="a1dda-108">C.</span><span class="sxs-lookup"><span data-stu-id="a1dda-108">C.</span></span> <span data-ttu-id="a1dda-109">Bamji et al., «1Mpixel 65nm BSI 320MHz a démodulé le capteur d’images TOF avec 3,5 μm de pixels d’obturation globaux et compartimentage analogiques, «ISSCC deg.</span><span class="sxs-lookup"><span data-stu-id="a1dda-109">Bamji et al., “1Mpixel 65nm BSI 320MHz Demodulated TOF Image Sensor with 3.5μm Global Shutter Pixels and Analog Binning,” ISSCC Deg.</span></span> <span data-ttu-id="a1dda-110">Amateurs.</span><span class="sxs-lookup"><span data-stu-id="a1dda-110">Tech.</span></span> <span data-ttu-id="a1dda-111">Documents, pp. 94-95, février 2018.</span><span class="sxs-lookup"><span data-stu-id="a1dda-111">Papers, pp. 94-95, Feb 2018.</span></span> <span data-ttu-id="a1dda-112">Lien IEEE Explor: https://ieeexplore.ieee.org/document/8310200/</span><span class="sxs-lookup"><span data-stu-id="a1dda-112">IEEE Explore Link: https://ieeexplore.ieee.org/document/8310200/</span></span>

<span data-ttu-id="a1dda-113">© IEEE 2018.</span><span class="sxs-lookup"><span data-stu-id="a1dda-113">© 2018 IEEE.</span></span> <span data-ttu-id="a1dda-114">L’utilisation personnelle de ce document est autorisée.</span><span class="sxs-lookup"><span data-stu-id="a1dda-114">Personal use of this material is permitted.</span></span> <span data-ttu-id="a1dda-115">L’autorisation d’IEEE doit être obtenue pour toutes les autres utilisations, sur un support en cours ou futur, y compris la réimpression ou la republication de ce matériel à des fins de publicité ou de promotion, la création de nouveaux travaux collectifs, la revente ou la redistribution à des serveurs ou des listes, ou réutilisation de tout composant protégé de ce travail dans d’autres travaux.</span><span class="sxs-lookup"><span data-stu-id="a1dda-115">Permission from IEEE must be obtained for all other uses, in any current or future media, including reprinting/republishing this material for advertising or promotional purposes, creating new collective works, for resale or redistribution to servers or lists, or reuse of any copyrighted component of this work in other works.</span></span>

<span data-ttu-id="a1dda-116">**Intitulé**</span><span class="sxs-lookup"><span data-stu-id="a1dda-116">**Whitepaper:**</span></span><br>
<span data-ttu-id="a1dda-117">![Aperçu du livre blanc](images/depth-camera-isscc.PNG)</span><span class="sxs-lookup"><span data-stu-id="a1dda-117">![Preview of whitepaper](images/depth-camera-isscc.PNG)</span></span><br>
[<span data-ttu-id="a1dda-118">Télécharger le livre blanc de profondeur de l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="a1dda-118">Download depth camera whitepaper</span></span>](images/Depth-Camera-ISSCC-2018.pdf)
