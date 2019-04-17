---
title: Livre blanc sur la caméra profondeur - ISSCC 2018
description: Livre blanc technique traitant de l’appareil photo de profondeur à être utilisé dans le projet Kinect pour Azure et la prochaine version de HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 7/5/2018
ms.topic: article
keywords: événement, iscc, vision par ordinateur, les recherches, kinect, hololens, profondeur, tof
ms.openlocfilehash: b692f9deeb7768e57ab6161b2c356a6610f18ed9
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594703"
---
# <a name="depth-camera-whitepaper---isscc-2018"></a><span data-ttu-id="5bb0f-104">Livre blanc sur la caméra profondeur - ISSCC 2018</span><span class="sxs-lookup"><span data-stu-id="5bb0f-104">Depth camera whitepaper - ISSCC 2018</span></span>

<span data-ttu-id="5bb0f-105">**titre :** BILAN de gravure 65 1Mpixel 320MHz démodulé TOF capteur d’Image avec 3.5μm obturateur Global Pixels et le compartimentage analogique</span><span class="sxs-lookup"><span data-stu-id="5bb0f-105">**Title:** 1Mpixel 65nm BSI 320MHz Demodulated TOF Image Sensor with 3.5μm Global Shutter Pixels and Analog Binning</span></span>

<span data-ttu-id="5bb0f-106">**Collaborateurs :** Cyrus S Bamji, Swati Mehta, Barry Thompson, Elkhatib Tamer, Stefan Wurster, Onur Akkaya, Andrew Payne, John Godbaz, Mike Fenton, Vijay Rajasekaran, Larry Prather, Satya Nagaraja, Vishali Mogallapu, Dane Snow, Rich McCauley, Mustansir Mukadam, Iskender Agi, Shaun McCarthy, Zhanping Xu, Travis Perry, William Qian, Vei-Han Chan, Prabhu Adepu, Gazi Ali, Muneeb Ahmed, Aditya Mukherjee, Sheethal Nayak, Dave Gampell, Sunil Acharya, Lou Kordus, Pat o ' Connor</span><span class="sxs-lookup"><span data-stu-id="5bb0f-106">**Contributors:** Cyrus S Bamji, Swati Mehta, Barry Thompson, Tamer Elkhatib, Stefan Wurster, Onur Akkaya, Andrew Payne, John Godbaz, Mike Fenton, Vijay Rajasekaran, Larry Prather, Satya Nagaraja, Vishali Mogallapu, Dane Snow, Rich McCauley, Mustansir Mukadam, Iskender Agi, Shaun McCarthy, Zhanping Xu, Travis Perry, William Qian, Vei-Han Chan, Prabhu Adepu, Gazi Ali, Muneeb Ahmed, Aditya Mukherjee, Sheethal Nayak, Dave Gampell, Sunil Acharya, Lou Kordus, Pat O'Connor</span></span>

<span data-ttu-id="5bb0f-107">**Présentées à ISSCC 2018 et publié dans ISSCC Deg. Tech. Livres, février 2018.**</span><span class="sxs-lookup"><span data-stu-id="5bb0f-107">**Presented at ISSCC 2018 and published in ISSCC Deg. Tech. Papers, Feb 2018.**</span></span>

<span data-ttu-id="5bb0f-108">C.</span><span class="sxs-lookup"><span data-stu-id="5bb0f-108">C.</span></span> <span data-ttu-id="5bb0f-109">Bamji et al., « 1Mpixel gravure 65 BSI 320MHz démodulé TOF capteur d’Image avec 3.5μm obturateur Global Pixels et le compartimentage analogique, « ISSCC Deg.</span><span class="sxs-lookup"><span data-stu-id="5bb0f-109">Bamji et al., “1Mpixel 65nm BSI 320MHz Demodulated TOF Image Sensor with 3.5μm Global Shutter Pixels and Analog Binning,” ISSCC Deg.</span></span> <span data-ttu-id="5bb0f-110">Tech.</span><span class="sxs-lookup"><span data-stu-id="5bb0f-110">Tech.</span></span> <span data-ttu-id="5bb0f-111">Livres blancs, pp. 94-95, février 2018.</span><span class="sxs-lookup"><span data-stu-id="5bb0f-111">Papers, pp. 94-95, Feb 2018.</span></span> <span data-ttu-id="5bb0f-112">IEEE Explorer lien : https://ieeexplore.ieee.org/document/8310200/</span><span class="sxs-lookup"><span data-stu-id="5bb0f-112">IEEE Explore Link: https://ieeexplore.ieee.org/document/8310200/</span></span>

<span data-ttu-id="5bb0f-113">© 2018 IEEE.</span><span class="sxs-lookup"><span data-stu-id="5bb0f-113">© 2018 IEEE.</span></span> <span data-ttu-id="5bb0f-114">Utilisation personnelle de ce matériel est autorisée.</span><span class="sxs-lookup"><span data-stu-id="5bb0f-114">Personal use of this material is permitted.</span></span> <span data-ttu-id="5bb0f-115">Autorisation de la norme IEEE doit être obtenue pour toutes les autres utilisations, dans n’importe quel support actuelles ou futures, y compris la réimprimé/réédition de ce document à des fins publicitaires ou promotionnelles, création de nouveaux travaux collective, pour les revendre ou de redistribution pour les serveurs ou les listes, ou réutilisation de n’importe quel composant les droits d’auteur de ce travail dans les autres travaux.</span><span class="sxs-lookup"><span data-stu-id="5bb0f-115">Permission from IEEE must be obtained for all other uses, in any current or future media, including reprinting/republishing this material for advertising or promotional purposes, creating new collective works, for resale or redistribution to servers or lists, or reuse of any copyrighted component of this work in other works.</span></span>

<span data-ttu-id="5bb0f-116">**Livre blanc :**</span><span class="sxs-lookup"><span data-stu-id="5bb0f-116">**Whitepaper:**</span></span><br>
<span data-ttu-id="5bb0f-117">![Aperçu du livre blanc](images/depth-camera-isscc.PNG)</span><span class="sxs-lookup"><span data-stu-id="5bb0f-117">![Preview of whitepaper](images/depth-camera-isscc.PNG)</span></span><br>
[<span data-ttu-id="5bb0f-118">Téléchargez le livre blanc de caméra de profondeur</span><span class="sxs-lookup"><span data-stu-id="5bb0f-118">Download depth camera whitepaper</span></span>](images/Depth-Camera-ISSCC-2018.pdf)
