---
title: Étude de cas - leçons de cuisine de la Lowe
description: L’équipe de HoloLens veut partager certaines des meilleures pratiques qui ont été dérivées de projet de HoloLens de le Lowe.
author: BrandonBray
ms.author: kevincol
ms.date: 03/21/2018
ms.topic: article
keywords: Réalité mixte Windows, de Lowe, HoloLens, cuisine, étude de cas
ms.openlocfilehash: 24759f90b8b84ec19e644fb8dff44f64c3ab81d2
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594163"
---
# <a name="case-study---lessons-from-the-lowes-kitchen"></a><span data-ttu-id="6f56c-104">Étude de cas - leçons de cuisine de la Lowe</span><span class="sxs-lookup"><span data-stu-id="6f56c-104">Case study - Lessons from the Lowe's kitchen</span></span>

<span data-ttu-id="6f56c-105">L’équipe de HoloLens veut partager certaines des meilleures pratiques qui ont été dérivées de projet de HoloLens de le Lowe.</span><span class="sxs-lookup"><span data-stu-id="6f56c-105">The HoloLens team wants to share some of the best practices that were derived from the Lowe's HoloLens project.</span></span> <span data-ttu-id="6f56c-106">Ci-dessous est une vidéo de HoloLens de le Lowe projeté a montré au discours d’ouverture de Satya 2016 Ignite.</span><span class="sxs-lookup"><span data-stu-id="6f56c-106">Below is a video of the Lowe's HoloLens projected demonstrated at Satya's 2016 Ignite keynote.</span></span>
<br>
>[!VIDEO https://www.youtube.com/embed/gC_4JxF0e_k]

## <a name="lowes-hololens-best-practices"></a><span data-ttu-id="6f56c-107">HoloLens Best de Lowe Practices</span><span class="sxs-lookup"><span data-stu-id="6f56c-107">Lowe's HoloLens Best Practices</span></span>

<span data-ttu-id="6f56c-108">Les deux vidéos couvrent les meilleures pratiques qui ont été dérivés HoloLens pilote de la Lowe qui est présent dans les magasins de deux Lowe depuis avril 2016.</span><span class="sxs-lookup"><span data-stu-id="6f56c-108">The two videos cover best practices that were derived from the Lowe's HoloLens Pilot that has been in two Lowe's stores since April 2016.</span></span> <span data-ttu-id="6f56c-109">Les rubriques principales sont :</span><span class="sxs-lookup"><span data-stu-id="6f56c-109">The key topics are:</span></span>
* <span data-ttu-id="6f56c-110">Optimiser les performances pour un appareil mobile</span><span class="sxs-lookup"><span data-stu-id="6f56c-110">Maximize performance for a mobile device</span></span>
* <span data-ttu-id="6f56c-111">Créer des méthodes de l’expérience utilisateur avec un cadre complet HOLOGRAPHIQUE (2nd talk)</span><span class="sxs-lookup"><span data-stu-id="6f56c-111">Create UX methods with a full holographic frame (2nd talk)</span></span>
* <span data-ttu-id="6f56c-112">Alignement de précision (2nd talk)</span><span class="sxs-lookup"><span data-stu-id="6f56c-112">Precision alignment (2nd talk)</span></span>
* <span data-ttu-id="6f56c-113">Partage des expériences HOLOGRAPHIQUE (2nd talk)</span><span class="sxs-lookup"><span data-stu-id="6f56c-113">Shared holographic experiences (2nd talk)</span></span>
* <span data-ttu-id="6f56c-114">Interaction avec les clients (2e talk)</span><span class="sxs-lookup"><span data-stu-id="6f56c-114">Interacting with customers (2nd talk)</span></span>

## <a name="video-1"></a><span data-ttu-id="6f56c-115">Vidéo 1</span><span class="sxs-lookup"><span data-stu-id="6f56c-115">Video 1</span></span>

<span data-ttu-id="6f56c-116">**Optimiser les performances pour un appareil mobile** HoloLens est un appareil librement avec tout le traitement en cours dans l’appareil.</span><span class="sxs-lookup"><span data-stu-id="6f56c-116">**Maximize performance for a mobile device** HoloLens is an untethered device with all the processing taking place in the device.</span></span> <span data-ttu-id="6f56c-117">Cela nécessite une plate-forme mobile et nécessite un état d’esprit similaire à la création d’applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="6f56c-117">This requires a mobile platform and requires a mindset similar to creating mobile applications.</span></span> <span data-ttu-id="6f56c-118">Microsoft recommande que votre application HoloLens maintenir 60 i/s pour fournir une expérience délicieuse pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6f56c-118">Microsoft recommends that your HoloLens application maintain 60FPS to provide a delicious experience for your users.</span></span> <span data-ttu-id="6f56c-119">I/s faible peut entraîner de hologrammes instables.</span><span class="sxs-lookup"><span data-stu-id="6f56c-119">Having low FPS can result in unstable holograms.</span></span>

<span data-ttu-id="6f56c-120">Certaines des choses plus importantes à prendre en compte pour le développement sur HoloLens est actif optimisation/décimalisation, à l’aide des nuanceurs personnalisés (disponible gratuitement dans le [HoloLens Toolkit](https://github.com/Microsoft/HoloToolkit-Unity)).</span><span class="sxs-lookup"><span data-stu-id="6f56c-120">Some of the most important things to look at when developing on HoloLens is asset optimization/decimation, using custom shaders (available for free in the [HoloLens Toolkit](https://github.com/Microsoft/HoloToolkit-Unity)).</span></span> <span data-ttu-id="6f56c-121">Un autre élément important consiste à mesurer la fréquence d’images depuis le début de votre projet.</span><span class="sxs-lookup"><span data-stu-id="6f56c-121">Another important consideration is to measure the frame rate from the very beginning of your project.</span></span> <span data-ttu-id="6f56c-122">Selon le projet, l’ordre d’affichage de vos éléments multimédias permettre également être un très grand contributeur</span><span class="sxs-lookup"><span data-stu-id="6f56c-122">Depending on the project, the order of displaying your assets can also be a big contributor</span></span>
<br>
>[!VIDEO https://www.youtube.com/embed/o0QIPwgiP9A]

## <a name="video-2"></a><span data-ttu-id="6f56c-123">Vidéo 2</span><span class="sxs-lookup"><span data-stu-id="6f56c-123">Video 2</span></span>

<span data-ttu-id="6f56c-124">**Créer des méthodes de l’expérience utilisateur avec un cadre complet HOLOGRAPHIQUE** il est important de comprendre le positionnement des hologrammes dans un monde physique.</span><span class="sxs-lookup"><span data-stu-id="6f56c-124">**Create UX methods with a full holographic frame** It's important to understand the placement of holograms in a physical world.</span></span> <span data-ttu-id="6f56c-125">Avec Lowe nous parler de différentes méthodes de l’expérience utilisateur qui permettent aux utilisateurs hologrammes expérience de fermer tout en profitant de l’environnement de hologrammes.</span><span class="sxs-lookup"><span data-stu-id="6f56c-125">With Lowe's we talk about different UX methods that help users experience holograms up close while still seeing the larger environment of holograms.</span></span>

<span data-ttu-id="6f56c-126">**Alignement de précision** scénario pour le Lowe, il était plus haute importance pour l’expérience pour avoir un alignement de précision des hologrammes à la cuisine physique.</span><span class="sxs-lookup"><span data-stu-id="6f56c-126">**Precision alignment** For the Lowe's scenario, it was paramount to the experience to have precision alignment of the holograms to the physical kitchen.</span></span> <span data-ttu-id="6f56c-127">Nous abordons les techniques qui vous aide à garantir une expérience qui convainc les utilisateurs que leur environnement physique a changé.</span><span class="sxs-lookup"><span data-stu-id="6f56c-127">We discuss techniques helps ensure an experience that convinces users that their physical environment has changed.</span></span>

<span data-ttu-id="6f56c-128">**Partage des expériences HOLOGRAPHIQUE** Couples sont le principal moyen de que l’expérience de la Lowe est consommé.</span><span class="sxs-lookup"><span data-stu-id="6f56c-128">**Shared holographic experiences** Couples are the primary way that the Lowe's experience is consumed.</span></span> <span data-ttu-id="6f56c-129">Une personne peut changer le plan de travail et l’autre personne puisse voir les modifications.</span><span class="sxs-lookup"><span data-stu-id="6f56c-129">One person can change the countertop and the other person will see the changes.</span></span> <span data-ttu-id="6f56c-130">Nous avons appelé ce « expériences partagées ».</span><span class="sxs-lookup"><span data-stu-id="6f56c-130">We called this "shared experiences".</span></span>

<span data-ttu-id="6f56c-131">**Interaction avec les clients** les concepteurs de Lowe n’utilisent pas un HoloLens, mais dont ils ont besoin voir ce que rencontrent les clients.</span><span class="sxs-lookup"><span data-stu-id="6f56c-131">**Interacting with customers** Lowe's designers are not using a HoloLens, but they need to see what the customers are seeing.</span></span> <span data-ttu-id="6f56c-132">Nous montrons comment capturer ce que le client voit sur une application UWP.</span><span class="sxs-lookup"><span data-stu-id="6f56c-132">We show how to capture what the customer is seeing on a UWP application.</span></span>
<br>
>[!VIDEO https://www.youtube.com/embed/LceMdyKZ4PI]
