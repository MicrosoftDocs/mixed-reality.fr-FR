---
title: Contrôleurs mains et motion
description: Vue d’ensemble de l’interaction des contrôleurs mains et motion
author: shengkait
ms.author: shentan
ms.date: 04/26/2019
ms.topic: article
keywords: La réalité mixte, les mains, les contrôleurs de mouvement, l’interaction et la conception
ms.openlocfilehash: 27d13316bbc4b3b40a1e617d73dd5487c05cb347
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334447"
---
# <a name="hands-and-motion-controllers"></a><span data-ttu-id="bbc44-104">Contrôleurs mains et motion</span><span class="sxs-lookup"><span data-stu-id="bbc44-104">Hands and motion controllers</span></span>
## <a name="scenarios"></a><span data-ttu-id="bbc44-105">Scénarios</span><span class="sxs-lookup"><span data-stu-id="bbc44-105">Scenarios</span></span>
<span data-ttu-id="bbc44-106">Si vous choisissez d’adopter ce modèle d’interaction après avoir lu la [vue d’ensemble](interaction-fundamentals.md)de l’interaction, cela signifie que vous développez une application nécessitant que les utilisateurs utilisent deux mains pour interagir avec le monde holographique.</span><span class="sxs-lookup"><span data-stu-id="bbc44-106">If you choose to adopt this interaction model after reading the [interaction overview](interaction-fundamentals.md), it means that you are developing an application requiring users to use two hands to interact with the holographic world.</span></span> <span data-ttu-id="bbc44-107">Votre application va atteindre l’objectif de supprimer la limite entre les serveurs virtuel et physique.</span><span class="sxs-lookup"><span data-stu-id="bbc44-107">Your application is going to achieve the goal of removing the boundary between virtual and physical.</span></span>

<span data-ttu-id="bbc44-108">Certains scénarios spécifiques peuvent être :</span><span class="sxs-lookup"><span data-stu-id="bbc44-108">Some specific scenarios might be:</span></span>
* <span data-ttu-id="bbc44-109">Fournir aux travailleurs de l’information des écrans virtuels 2D avec l’interface utilisateur intuitivité pour afficher et contrôler le contenu</span><span class="sxs-lookup"><span data-stu-id="bbc44-109">Providing information workers 2D virtual screens with UI affordances to display and control content</span></span>
* <span data-ttu-id="bbc44-110">Mise à disposition des didacticiels et des guides des travailleurs de première ligne pour les lignes d’assemblage usine</span><span class="sxs-lookup"><span data-stu-id="bbc44-110">Providing first line workers tutorials and guides for factory assembly lines</span></span>
* <span data-ttu-id="bbc44-111">Développement d’outils professionnels pour assister et former des professionnels de la santé</span><span class="sxs-lookup"><span data-stu-id="bbc44-111">Developing professional tools for assisting and educating medical professionals</span></span>  
* <span data-ttu-id="bbc44-112">Utilisation d’objets virtuels 3D pour décorer le monde réel ou créer un second monde</span><span class="sxs-lookup"><span data-stu-id="bbc44-112">Using 3D virtual objects to decorate the real world or to create a second world</span></span> 
* <span data-ttu-id="bbc44-113">Création de services et de jeux basés sur l’emplacement en utilisant le monde réel comme arrière-plan</span><span class="sxs-lookup"><span data-stu-id="bbc44-113">Creating location-based services and games using the real world as a background</span></span>

<br>

---

## <a name="hands-and-motion-controllers-modalities"></a><span data-ttu-id="bbc44-114">Modalités de contrôle des mains et des contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="bbc44-114">Hands and motion controllers modalities</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="bbc44-115">[![manipulation directe avec les mains](images/hands-and-controllers-direct-manipulation.jpg)](direct-manipulation.md)</span><span class="sxs-lookup"><span data-stu-id="bbc44-115">[![Direct manipulation with hands](images/hands-and-controllers-direct-manipulation.jpg)](direct-manipulation.md)</span></span><br>
       ### <a name="direct-manipulation-with-handsdirect-manipulationmdbr"></a>[<span data-ttu-id="bbc44-116">Manipulation directe avec les mains</span><span class="sxs-lookup"><span data-stu-id="bbc44-116">Direct manipulation with hands</span></span>](direct-manipulation.md)<br>
       <span data-ttu-id="bbc44-117">Il s’agit d’une modalité tirant parti de la puissance des mains, avec laquelle les utilisateurs peuvent toucher et manipuler les hologrammes directement.</span><span class="sxs-lookup"><span data-stu-id="bbc44-117">This is a modality leveraging the power of hands, with which users are capable of touching and manipulating the holograms directly.</span></span> <span data-ttu-id="bbc44-118">En tirant parti de l’expérience de vie quotidienne et en fournissant un intuitivité visuel approprié, les utilisateurs peuvent utiliser la même méthode de manipulation d’objets réels pour interagir avec des objets virtuels.</span><span class="sxs-lookup"><span data-stu-id="bbc44-118">By leveraging daily life experiences and providing proper visual affordances, users are able to use the same way of manipulating real world objects to interact with virtual ones.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="bbc44-119">[Point de ![et validation avec mains](images/hands-and-controllers-point-and-commit.jpg)](point-and-commit.md)</span><span class="sxs-lookup"><span data-stu-id="bbc44-119">[![Point and commit with hands](images/hands-and-controllers-point-and-commit.jpg)](point-and-commit.md)</span></span><br>
        ### <a name="point-and-commit-with-handspoint-and-commitmdbr"></a>[<span data-ttu-id="bbc44-120">Pointer et valider avec les mains</span><span class="sxs-lookup"><span data-stu-id="bbc44-120">Point and commit with hands</span></span>](point-and-commit.md)<br>
        <span data-ttu-id="bbc44-121">Cette modalité permet aux utilisateurs d’interagir avec des hologrammes à distance.</span><span class="sxs-lookup"><span data-stu-id="bbc44-121">This modality empowers users to interact with holograms in a distance.</span></span> <span data-ttu-id="bbc44-122">Il permet aux utilisateurs de tirer le meilleur parti de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="bbc44-122">It enables users to make the best use of surroundings.</span></span> <span data-ttu-id="bbc44-123">Les utilisateurs peuvent placer des hologrammes n’importe où et toujours y accéder à partir de n’importe quelle distance.</span><span class="sxs-lookup"><span data-stu-id="bbc44-123">Users can place holograms anywhere and still access them from any distance.</span></span> <span data-ttu-id="bbc44-124">Les modèles et les gestes mentals pour le contrôle et la manipulation des hologrammes 2D et 3D sont hautement synchronisés avec ceux de manipulation directe.</span><span class="sxs-lookup"><span data-stu-id="bbc44-124">The mental models and gestures for controlling and manipulating 2D and 3D holograms are highly in sync with those of direct manipulation.</span></span>
    :::column-end:::
    :::column:::
       <span data-ttu-id="bbc44-125">[contrôleurs de mouvement ![](images/hands-and-controllers-motion-controllers.jpg)](motion-controllers.md)</span><span class="sxs-lookup"><span data-stu-id="bbc44-125">[![Motion controllers](images/hands-and-controllers-motion-controllers.jpg)](motion-controllers.md)</span></span><br>
       ### <a name="motion-controllersmotion-controllersmdbr"></a>[<span data-ttu-id="bbc44-126">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="bbc44-126">Motion controllers</span></span>](motion-controllers.md)<br>
       <span data-ttu-id="bbc44-127">Les contrôleurs de mouvement sont des outils qui étendent les capacités physiques de l’utilisateur en fournissant des interactions précises sur une grande variété de distances tout en utilisant l’une ou l’autre des mains.</span><span class="sxs-lookup"><span data-stu-id="bbc44-127">Motion controllers are tools that extend the user's physical capabilities by providing precise interactions across a large range of distances while using one or both hands.</span></span> <span data-ttu-id="bbc44-128">Ces accessoires de matériel fournissent des raccourcis vers de nombreuses interactions couramment utilisées et fournissent des commentaires surefooted et tactiles pour diverses actions.</span><span class="sxs-lookup"><span data-stu-id="bbc44-128">These hardware accessories provide shortcuts to many commonly-used interactions and provide surefooted, tactile feedback for a variety of actions.</span></span> <span data-ttu-id="bbc44-129">Actuellement, les contrôleurs de mouvement sont uniquement disponibles pour les scénarios Windows Mixed Reality (WMR).</span><span class="sxs-lookup"><span data-stu-id="bbc44-129">Currently, motion controllers are only available for Windows Mixed Reality (WMR) scenarios.</span></span> 
    :::column-end:::
:::row-end:::

<br>

---

## <a name="see-also"></a><span data-ttu-id="bbc44-130">Articles associés</span><span class="sxs-lookup"><span data-stu-id="bbc44-130">See also</span></span>
* [<span data-ttu-id="bbc44-131">Pointer du regard vers l’avant et valider</span><span class="sxs-lookup"><span data-stu-id="bbc44-131">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="bbc44-132">Suivre de la tête et stabiliser</span><span class="sxs-lookup"><span data-stu-id="bbc44-132">Head-gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="bbc44-133">Manipulation directe avec les mains</span><span class="sxs-lookup"><span data-stu-id="bbc44-133">Direct manipulation with hands</span></span>](direct-manipulation.md)
* [<span data-ttu-id="bbc44-134">Pointer et valider avec les mains</span><span class="sxs-lookup"><span data-stu-id="bbc44-134">Point and commit with hands</span></span>](point-and-commit.md)
* [<span data-ttu-id="bbc44-135">Mains-libres</span><span class="sxs-lookup"><span data-stu-id="bbc44-135">Hands-free</span></span>](hands-free.md)
