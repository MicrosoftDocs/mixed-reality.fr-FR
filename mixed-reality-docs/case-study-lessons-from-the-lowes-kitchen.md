---
title: Étude de cas-leçons de la cuisine de Lowe
description: L’équipe HoloLens souhaite partager certaines des meilleures pratiques qui ont été dérivées du projet HoloLens de Lowe.
author: BrandonBray
ms.author: kevincol
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, Lowe, HoloLens, cuisine, étude de cas
ms.openlocfilehash: 24759f90b8b84ec19e644fb8dff44f64c3ab81d2
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522345"
---
# <a name="case-study---lessons-from-the-lowes-kitchen"></a><span data-ttu-id="9632f-104">Étude de cas-leçons de la cuisine de Lowe</span><span class="sxs-lookup"><span data-stu-id="9632f-104">Case study - Lessons from the Lowe's kitchen</span></span>

<span data-ttu-id="9632f-105">L’équipe HoloLens souhaite partager certaines des meilleures pratiques qui ont été dérivées du projet HoloLens de Lowe.</span><span class="sxs-lookup"><span data-stu-id="9632f-105">The HoloLens team wants to share some of the best practices that were derived from the Lowe's HoloLens project.</span></span> <span data-ttu-id="9632f-106">Vous trouverez ci-dessous une vidéo de l’Lowe HoloLens projeté présentée dans le discours de Satya 2016.</span><span class="sxs-lookup"><span data-stu-id="9632f-106">Below is a video of the Lowe's HoloLens projected demonstrated at Satya's 2016 Ignite keynote.</span></span>
<br>
>[!VIDEO https://www.youtube.com/embed/gC_4JxF0e_k]

## <a name="lowes-hololens-best-practices"></a><span data-ttu-id="9632f-107">Meilleures pratiques de Lowe HoloLens</span><span class="sxs-lookup"><span data-stu-id="9632f-107">Lowe's HoloLens Best Practices</span></span>

<span data-ttu-id="9632f-108">Les deux vidéos couvrent les meilleures pratiques qui ont été dérivées du pilote HoloLens de Lowe, qui se trouvait dans deux magasins Lowe depuis avril 2016.</span><span class="sxs-lookup"><span data-stu-id="9632f-108">The two videos cover best practices that were derived from the Lowe's HoloLens Pilot that has been in two Lowe's stores since April 2016.</span></span> <span data-ttu-id="9632f-109">Les principales rubriques sont les suivantes:</span><span class="sxs-lookup"><span data-stu-id="9632f-109">The key topics are:</span></span>
* <span data-ttu-id="9632f-110">Optimiser les performances d’un appareil mobile</span><span class="sxs-lookup"><span data-stu-id="9632f-110">Maximize performance for a mobile device</span></span>
* <span data-ttu-id="9632f-111">Créer des méthodes d’expérience utilisateur avec une image holographique complète (2e contact)</span><span class="sxs-lookup"><span data-stu-id="9632f-111">Create UX methods with a full holographic frame (2nd talk)</span></span>
* <span data-ttu-id="9632f-112">Alignement de précision (2e contact)</span><span class="sxs-lookup"><span data-stu-id="9632f-112">Precision alignment (2nd talk)</span></span>
* <span data-ttu-id="9632f-113">Expériences holographiques partagées (2e contact)</span><span class="sxs-lookup"><span data-stu-id="9632f-113">Shared holographic experiences (2nd talk)</span></span>
* <span data-ttu-id="9632f-114">Interaction avec les clients (2e Conférence)</span><span class="sxs-lookup"><span data-stu-id="9632f-114">Interacting with customers (2nd talk)</span></span>

## <a name="video-1"></a><span data-ttu-id="9632f-115">Vidéo 1</span><span class="sxs-lookup"><span data-stu-id="9632f-115">Video 1</span></span>

<span data-ttu-id="9632f-116">**Optimiser les performances d’un appareil mobile** HoloLens est un appareil non attaché avec tout le traitement effectué sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="9632f-116">**Maximize performance for a mobile device** HoloLens is an untethered device with all the processing taking place in the device.</span></span> <span data-ttu-id="9632f-117">Cela nécessite une plate-forme mobile et requiert un mentalités similaire à la création d’applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="9632f-117">This requires a mobile platform and requires a mindset similar to creating mobile applications.</span></span> <span data-ttu-id="9632f-118">Microsoft recommande que votre application HoloLens maintienne 60FPS pour fournir une expérience délicieuse à vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9632f-118">Microsoft recommends that your HoloLens application maintain 60FPS to provide a delicious experience for your users.</span></span> <span data-ttu-id="9632f-119">Une faible FPS peut entraîner des hologrammes instables.</span><span class="sxs-lookup"><span data-stu-id="9632f-119">Having low FPS can result in unstable holograms.</span></span>

<span data-ttu-id="9632f-120">Voici quelques-uns des éléments les plus importants à examiner lorsque le développement sur HoloLens est l’optimisation/la décimalisation des ressources, à l’aide de nuanceurs personnalisés (disponibles gratuitement dans la [boîte à outils HoloLens](https://github.com/Microsoft/HoloToolkit-Unity)).</span><span class="sxs-lookup"><span data-stu-id="9632f-120">Some of the most important things to look at when developing on HoloLens is asset optimization/decimation, using custom shaders (available for free in the [HoloLens Toolkit](https://github.com/Microsoft/HoloToolkit-Unity)).</span></span> <span data-ttu-id="9632f-121">Une autre considération importante consiste à mesurer la fréquence d’images à partir du début de votre projet.</span><span class="sxs-lookup"><span data-stu-id="9632f-121">Another important consideration is to measure the frame rate from the very beginning of your project.</span></span> <span data-ttu-id="9632f-122">Selon le projet, l’ordre d’affichage de vos ressources peut également être un grand contributeur</span><span class="sxs-lookup"><span data-stu-id="9632f-122">Depending on the project, the order of displaying your assets can also be a big contributor</span></span>
<br>
>[!VIDEO https://www.youtube.com/embed/o0QIPwgiP9A]

## <a name="video-2"></a><span data-ttu-id="9632f-123">Vidéo 2</span><span class="sxs-lookup"><span data-stu-id="9632f-123">Video 2</span></span>

<span data-ttu-id="9632f-124">**Créer des méthodes d’expérience utilisateur avec une image holographique complète** Il est important de comprendre le positionnement des hologrammes dans un monde physique.</span><span class="sxs-lookup"><span data-stu-id="9632f-124">**Create UX methods with a full holographic frame** It's important to understand the placement of holograms in a physical world.</span></span> <span data-ttu-id="9632f-125">Avec Lowe, nous parlerons des différentes méthodes d’expérience utilisateur qui permettent aux utilisateurs d’expérimenter leurs hologrammes tout en continuant à voir l’environnement plus grand des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="9632f-125">With Lowe's we talk about different UX methods that help users experience holograms up close while still seeing the larger environment of holograms.</span></span>

<span data-ttu-id="9632f-126">**Alignement de précision** Pour le scénario de Lowe, il était primordial d’avoir un alignement précis des hologrammes sur la cuisine physique.</span><span class="sxs-lookup"><span data-stu-id="9632f-126">**Precision alignment** For the Lowe's scenario, it was paramount to the experience to have precision alignment of the holograms to the physical kitchen.</span></span> <span data-ttu-id="9632f-127">Nous nous penchons sur les techniques pour garantir une expérience qui convainc les utilisateurs que leur environnement physique a changé.</span><span class="sxs-lookup"><span data-stu-id="9632f-127">We discuss techniques helps ensure an experience that convinces users that their physical environment has changed.</span></span>

<span data-ttu-id="9632f-128">**Expériences holographiques partagées** Les couples sont le principal moyen de consommer l’expérience du Lowe.</span><span class="sxs-lookup"><span data-stu-id="9632f-128">**Shared holographic experiences** Couples are the primary way that the Lowe's experience is consumed.</span></span> <span data-ttu-id="9632f-129">Une personne peut modifier le plan de plan et l’autre personne verra les modifications.</span><span class="sxs-lookup"><span data-stu-id="9632f-129">One person can change the countertop and the other person will see the changes.</span></span> <span data-ttu-id="9632f-130">Nous avons appelé «expériences partagées».</span><span class="sxs-lookup"><span data-stu-id="9632f-130">We called this "shared experiences".</span></span>

<span data-ttu-id="9632f-131">**Interaction avec les clients** Les concepteurs de Lowe n’utilisent pas un HoloLens, mais ils ont besoin de voir ce que les clients voient.</span><span class="sxs-lookup"><span data-stu-id="9632f-131">**Interacting with customers** Lowe's designers are not using a HoloLens, but they need to see what the customers are seeing.</span></span> <span data-ttu-id="9632f-132">Nous montrons comment capturer ce que le client voit sur une application UWP.</span><span class="sxs-lookup"><span data-stu-id="9632f-132">We show how to capture what the customer is seeing on a UWP application.</span></span>
<br>
>[!VIDEO https://www.youtube.com/embed/LceMdyKZ4PI]
