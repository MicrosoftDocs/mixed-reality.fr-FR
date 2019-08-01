---
title: Vue d’ensemble de l’interaction multimodale
description: Vue d’ensemble de l’interaction multimodale
author: shengkait
ms.author: shengkait
ms.date: 04/11/2019
ms.topic: article
ms.localizationpriority: high
keywords: Mixed Reality, pointage du regard, ciblage avec le regard, interaction, conception, hololens, MMR, multimodal
ms.openlocfilehash: 3ba1a2fc46aa88c856e4cc9531382c479b3fb17a
ms.sourcegitcommit: 76a7aa6e64e114b63ace058dd6d6d662b3c9f09e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/26/2019
ms.locfileid: "68507899"
---
# <a name="introducing-instinctual-interactions"></a><span data-ttu-id="49442-104">Présentation des interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="49442-104">Introducing instinctual interactions</span></span>

<span data-ttu-id="49442-105">Les interactions simples et instinctuelles sont étroitement liées dans la plateforme Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="49442-105">The philosophy of simple, instinctual interactions is interwoven throughout the Mixed Reality platform.</span></span>  <span data-ttu-id="49442-106">Nous avons suivi trois étapes pour que les développeurs et concepteurs d’applications puissent proposer des interactions faciles et intuitives à leurs clients.</span><span class="sxs-lookup"><span data-stu-id="49442-106">We've taken three steps to ensure that application designers and developers can provide their customers with easy and intuitive interactions.</span></span> 

<span data-ttu-id="49442-107">Tout d’abord, nous avons veillé à combiner en modèles d’interaction multimodale fluides nos capteurs et nos technologies d’entrée (notamment le suivi de la main et oculaire, associé à l’entrée de langage naturel).</span><span class="sxs-lookup"><span data-stu-id="49442-107">First, we've made sure our sensors and input technologies (which includes hand and eye tracking along with natural language input) combine into seamless, multimodal interaction models.</span></span>  <span data-ttu-id="49442-108">Selon nos recherches, la conception et le développement au sein d’un framework multimodal, plutôt qu’à partir d’entrées uniques, sont essentiels à la création d’expériences instinctuelles.</span><span class="sxs-lookup"><span data-stu-id="49442-108">Based on our research, designing and developing within a multimodal framework, and not based on single inputs, is the key to creating instinctual experiences.</span></span>

<span data-ttu-id="49442-109">Deuxièmement, nous sommes conscients que de nombreux développeurs ciblent plusieurs appareils HoloLens tels qu’HoloLens 2 et HoloLens (1ère génération) ou HoloLens et VR.</span><span class="sxs-lookup"><span data-stu-id="49442-109">Second, we recognize that many developers target multiple HoloLens devices, such as HoloLens 2 and HoloLens (1st gen) or HoloLens and VR.</span></span>  <span data-ttu-id="49442-110">Nous avons donc conçu nos modèles d’interaction pour qu’ils fonctionnent sur tous les appareils, même si la technologie d’entrée varie d’un appareil à l’autre.</span><span class="sxs-lookup"><span data-stu-id="49442-110">So we've designed our interaction models to work across devices, even if the input technology varies on each device.</span></span>  <span data-ttu-id="49442-111">Par exemple, une interaction de loin sur un casque immersif Windows avec un contrôleur 6DoF et une interaction de loin sur un appareil HoloLens 2 utilisent toutes deux des affordances et des schémas identiques, ce qui facilite le développement d’applications multi-appareils donnant une sensation naturelle aux interactions des utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="49442-111">For example, far interaction on a Windows Immersive headset with a 6DoF controller and far interaction on a HoloLens 2 both use  identical affordances and patterns, making it easy for cross-device application development that provides a natural feel to end-user interactions.</span></span> 

<span data-ttu-id="49442-112">Face aux milliers d’interactions efficaces, attrayantes et magiques possibles qu’offre la réalité mixte (MR), nous avons trouvé que l’utilisation intentionnelle d’un seul modèle d’interaction de bout en bout dans une application est le meilleur gage de réussite et d’expérience agréable pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="49442-112">While we recognize that there are thousands of effective, engaging, and magical interactions possible in mixed reality (MR), we've found that intentionally employing a single interaction model, end-to-end, in an application is the best way to ensure users are successful and have a great experience.</span></span> <span data-ttu-id="49442-113">À cette fin, nous avons inclus trois choses dans ce guide d’interaction :</span><span class="sxs-lookup"><span data-stu-id="49442-113">To that end, we've included three things in this interaction guidance:</span></span>
* <span data-ttu-id="49442-114">Ce guide est structuré autour des trois modèles d’interaction principaux et des composants et schémas requis pour chacun.</span><span class="sxs-lookup"><span data-stu-id="49442-114">This guidance is structured around the three primary interaction models and the components and patterns required for each.</span></span>
* <span data-ttu-id="49442-115">Des conseils supplémentaires sur d’autres avantages qu’offre notre plateforme ont été inclus.</span><span class="sxs-lookup"><span data-stu-id="49442-115">Supplemental guidance has been included about other benefits that our platform provides.</span></span>
* <span data-ttu-id="49442-116">Des conseils pour vous aider à sélectionner le modèle d’interaction approprié pour votre scénario ont également été inclus.</span><span class="sxs-lookup"><span data-stu-id="49442-116">Guidance has also been included to help select the appropriate interaction model for your development scenario.</span></span>

## <a name="multimodal-interaction-models"></a><span data-ttu-id="49442-117">Modèles d’interaction multimodale</span><span class="sxs-lookup"><span data-stu-id="49442-117">Multimodal interaction models</span></span>

<span data-ttu-id="49442-118">D’après nos recherches et les commentaires des clients, trois modèles d’interaction principaux conviennent pour la majorité des expériences de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="49442-118">Based on our research as well as feedback from customers, we've discovered that three primary interaction models suit the majority of mixed reality experiences.</span></span>

<span data-ttu-id="49442-119">Dans bien des égards, le modèle d’interaction est le modèle mental de l’utilisateur pour l’exécution de ses flux.</span><span class="sxs-lookup"><span data-stu-id="49442-119">In many ways, the interaction model is the user's mental model for completing their flows.</span></span> <span data-ttu-id="49442-120">Chacun de ces modèles d’interaction est optimisé pour un ensemble de besoins du client.</span><span class="sxs-lookup"><span data-stu-id="49442-120">Each of these interaction models is optimized for a set of customer needs.</span></span> <span data-ttu-id="49442-121">Ils sont tous pratiques, puissants et utilisables indépendamment les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="49442-121">Each is convenient, powerful, and usable in its own right.</span></span> 

<span data-ttu-id="49442-122">Le tableau ci-dessous offre une vue d’ensemble simplifiée.</span><span class="sxs-lookup"><span data-stu-id="49442-122">The chart below is a simplified overview.</span></span> <span data-ttu-id="49442-123">Vous pouvez cliquer sur les liens ci-après pour obtenir des informations détaillées sur l’utilisation de chaque modèle d’interaction, y compris des images et des exemples de code.</span><span class="sxs-lookup"><span data-stu-id="49442-123">Detailed information for using each interaction model is linked in the pages below with images and code samples.</span></span> 

<br>
<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="49442-124"><strong>Modèle</strong></span><span class="sxs-lookup"><span data-stu-id="49442-124"><strong>Model</strong></span></span></td>
        <td><span data-ttu-id="49442-125"><strong>Exemples de scénario</strong></span><span class="sxs-lookup"><span data-stu-id="49442-125"><strong>Example scenarios</strong></span></span></td>
        <td><span data-ttu-id="49442-126"><strong>Cadre</strong></span><span class="sxs-lookup"><span data-stu-id="49442-126"><strong>Fit</strong></span></span></td>
        <td><span data-ttu-id="49442-127"><strong>Matériel</strong></span><span class="sxs-lookup"><span data-stu-id="49442-127"><strong>Hardware</strong></span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="49442-128"><a href="hands-and-tools.md">Mains et contrôleurs de mouvement</a></span><span class="sxs-lookup"><span data-stu-id="49442-128"><a href="hands-and-tools.md">Hands and motion controllers</a></span></span></td>
        <td><span data-ttu-id="49442-129">Expériences 3D spatiales telles que la conception et la disposition spatiales, la manipulation de contenu ou la simulation.</span><span class="sxs-lookup"><span data-stu-id="49442-129">3D spatial experiences, such as spatial layout and design, content manipulation, or simulation.</span></span></td>
        <td><span data-ttu-id="49442-130">Idéal pour les nouveaux utilisateurs en liaison avec la voix, le suivi oculaire ou le suivi de la tête.</span><span class="sxs-lookup"><span data-stu-id="49442-130">Great for new users coupled with voice, eye tracking or head gaze.</span></span> <span data-ttu-id="49442-131">Courbe d’apprentissage basse.</span><span class="sxs-lookup"><span data-stu-id="49442-131">Low learning curve.</span></span> <span data-ttu-id="49442-132">Expérience utilisateur cohérente entre le suivi de la main et les contrôleurs 6DoF.</span><span class="sxs-lookup"><span data-stu-id="49442-132">Consistent UX across hand tracking and 6DoF controllers.</span></span></td>
        <td><span data-ttu-id="49442-133">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="49442-133">HoloLens 2</span></span><br><span data-ttu-id="49442-134">Casques immersifs</span><span class="sxs-lookup"><span data-stu-id="49442-134">Immersive headsets</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="49442-135"><a href="hands-free.md">Mains-libres</a></span><span class="sxs-lookup"><span data-stu-id="49442-135"><a href="hands-free.md">Hands-free</a></span></span></td>
        <td><span data-ttu-id="49442-136">Expériences contextuelles où les mains d’un utilisateur sont occupées, par exemple dans le cadre d’un apprentissage « sur le tas » et d’une maintenance.</span><span class="sxs-lookup"><span data-stu-id="49442-136">Contextual experiences where a user's hands are occupied, such as on-the-job learning, and maintenance.</span></span></td>
        <td><span data-ttu-id="49442-137">Un apprentissage est requis.</span><span class="sxs-lookup"><span data-stu-id="49442-137">Some learning required.</span></span> <span data-ttu-id="49442-138">Si les mains ne sont pas disponibles, l’appareil peut être associé à la voix et au langage naturel.</span><span class="sxs-lookup"><span data-stu-id="49442-138">If hands are unavailable, the device pairs well with voice and natural language.</span></span></td>
        <td><span data-ttu-id="49442-139">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="49442-139">HoloLens 2</span></span><br><span data-ttu-id="49442-140">HoloLens (1ère génération)</span><span class="sxs-lookup"><span data-stu-id="49442-140">HoloLens (1st gen)</span></span><br><span data-ttu-id="49442-141">Casques immersifs</span><span class="sxs-lookup"><span data-stu-id="49442-141">Immersive headsets</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="49442-142"><a href="gaze-and-commit.md">Suivre de la tête et valider</a></span><span class="sxs-lookup"><span data-stu-id="49442-142"><a href="gaze-and-commit.md">Head-gaze and commit</a></span></span></td>
        <td><span data-ttu-id="49442-143">Expériences au moyen de clics, par exemple, présentations 3D et démonstrations.</span><span class="sxs-lookup"><span data-stu-id="49442-143">Click-through experiences, e.g. 3D presentations, demos.</span></span></td>
        <td><span data-ttu-id="49442-144">Nécessite une formation sur les appareils HMD, mais pas sur mobile.</span><span class="sxs-lookup"><span data-stu-id="49442-144">Requires training on HMDs but not on mobile.</span></span> <span data-ttu-id="49442-145">Idéal pour les contrôleurs accessibles.</span><span class="sxs-lookup"><span data-stu-id="49442-145">Best for accessible controllers.</span></span> <span data-ttu-id="49442-146">Idéal pour HoloLens (1ère génération).</span><span class="sxs-lookup"><span data-stu-id="49442-146">Best for HoloLens (1st gen).</span></span></td>
        <td><span data-ttu-id="49442-147">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="49442-147">HoloLens 2</span></span><br><span data-ttu-id="49442-148">HoloLens (1ère génération)</span><span class="sxs-lookup"><span data-stu-id="49442-148">HoloLens (1st gen)</span></span><br><span data-ttu-id="49442-149">Casques immersifs</span><span class="sxs-lookup"><span data-stu-id="49442-149">Immersive headsets</span></span><br><span data-ttu-id="49442-150">Réalité augmentée mobile</span><span class="sxs-lookup"><span data-stu-id="49442-150">Mobile AR</span></span></td>
    </tr>
</table>
<br>

<span data-ttu-id="49442-151">Pour qu’il n’y ait ni vides ni trous dans l’expérience d’interaction de l’utilisateur, le mieux est de suivre les conseils pour un modèle unique du début à la fin.</span><span class="sxs-lookup"><span data-stu-id="49442-151">To ensure that there are no gaps or holes in the user interaction experience, it is best to follow the guidance for a single model from beginning to end.</span></span> 

<span data-ttu-id="49442-152">Pour accélérer le développement et la conception, nous avons inclus des informations détaillées et des liens vers des images et des exemples de code dans la couverture de chaque modèle.</span><span class="sxs-lookup"><span data-stu-id="49442-152">To speed up design and development, we've included detailed information and links to images and code samples within our coverage of each model.</span></span>

<span data-ttu-id="49442-153">Les sections ci-dessous décrivent les étapes de sélection et d’implémentation de l’un de ces modèles d’interaction.</span><span class="sxs-lookup"><span data-stu-id="49442-153">The sections below walk through the steps for selecting and implementing one of these interaction models.</span></span>  
 
### <a name="by-the-end-of-this-page-you-will-understand-our-guidance-on"></a><span data-ttu-id="49442-154">Quand vous parviendrez à la fin de cette page, vous comprendrez nos conseils sur :</span><span class="sxs-lookup"><span data-stu-id="49442-154">By the end of this page, you will understand our guidance on:</span></span>
 
* <span data-ttu-id="49442-155">Le choix d’un modèle d’interaction pour votre client</span><span class="sxs-lookup"><span data-stu-id="49442-155">Choosing an interaction model for your customer</span></span>
* <span data-ttu-id="49442-156">L’utilisation du guide des modèles d’interaction</span><span class="sxs-lookup"><span data-stu-id="49442-156">Using the interaction model guidance</span></span>
* <span data-ttu-id="49442-157">Le passage d’un modèle d’interaction à un autre</span><span class="sxs-lookup"><span data-stu-id="49442-157">Transitioning between interaction models</span></span>
* <span data-ttu-id="49442-158">Les étapes suivantes de la conception</span><span class="sxs-lookup"><span data-stu-id="49442-158">Design next steps</span></span>


## <a name="choose-an-interaction-model-for-your-customer"></a><span data-ttu-id="49442-159">Choisir un modèle d’interaction pour votre client</span><span class="sxs-lookup"><span data-stu-id="49442-159">Choose an interaction model for your customer</span></span>


<span data-ttu-id="49442-160">Généralement, les développeurs et les créateurs ont envisagé les types d’interactions que leurs clients peuvent avoir.</span><span class="sxs-lookup"><span data-stu-id="49442-160">Typically, developers and creators have thought through the types of interactions that their customers can have.</span></span> <span data-ttu-id="49442-161">Pour encourager une approche conceptuelle axée sur le client, nous vous recommandons de suivre les conseils suivants afin de sélectionner le modèle d’interaction qui est optimisé pour votre client.</span><span class="sxs-lookup"><span data-stu-id="49442-161">To encourage a customer-focused approach to design, we recommend the following guidance for selecting the interaction model that's optimized for your customer.</span></span>

### <a name="why-follow-this-guidance"></a><span data-ttu-id="49442-162">Pourquoi suivre ces conseils ?</span><span class="sxs-lookup"><span data-stu-id="49442-162">Why follow this guidance?</span></span>

* <span data-ttu-id="49442-163">Nos modèles d’interaction sont testés en fonction de critères objectifs et subjectifs tels que les efforts physiques et cognitifs, l’intuitivité et la facilité d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="49442-163">Our interaction models are tested for objective and subjective criteria, such as physical and cognitive effort, intuitiveness, and learnability.</span></span> 
* <span data-ttu-id="49442-164">Tout comme les interaction, les affordances visuelles et audio et le comportement des objets peuvent varier d’un modèle d’interaction à l’autre.</span><span class="sxs-lookup"><span data-stu-id="49442-164">Because interactions differ, visual and audio affordances and object behavior might differ between interaction models.</span></span>  
* <span data-ttu-id="49442-165">La combinaison de parties de plusieurs modèles d’interaction crée le risque d’affordances concurrentes, à l’image de rayons émanant de la main et d’un curseur oculaire simultanés, qui peuvent submerger et perturber l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="49442-165">Combining parts of multiple interaction models creates the risk of competing affordances, such as simultaneous hand rays and a head-gaze cursor that can overwhelm and confuse users.</span></span>

<span data-ttu-id="49442-166">Voici quelques exemples d’optimisation des affordances et des comportements pour chaque modèle d’interaction.</span><span class="sxs-lookup"><span data-stu-id="49442-166">Here are some examples of how affordances and behaviors are optimized for each interaction model.</span></span>  <span data-ttu-id="49442-167">Nous constatons souvent que les nouveaux utilisateurs ont des questions similaires, telles que « comment savoir si le système fonctionne ? », « comment savoir ce que je peux faire ? » et « comment savoir s’il a compris ce que je viens de faire ? ».</span><span class="sxs-lookup"><span data-stu-id="49442-167">We often see new users have similar questions, such as "how do I know the system is working, how do I know what I can do, and how do I know if it understood what I just did?"</span></span>

<br>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="49442-168"><strong>Modèle</strong></span><span class="sxs-lookup"><span data-stu-id="49442-168"><strong>Model</strong></span></span></td>
        <td><span data-ttu-id="49442-169"><strong>Comment savoir si ça fonctionne ?</strong></span><span class="sxs-lookup"><span data-stu-id="49442-169"><strong>How do I know it's working?</strong></span></span></td>
        <td><span data-ttu-id="49442-170"><strong>Comment savoir ce que je peux faire ?</strong></span><span class="sxs-lookup"><span data-stu-id="49442-170"><strong>How do I know what I can do?</strong></span></span></td>
        <td><span data-ttu-id="49442-171"><strong>Comment savoir ce que je viens de faire ?</strong></span><span class="sxs-lookup"><span data-stu-id="49442-171"><strong>How do I know what I just did?</strong></span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="49442-172"><a href="hands-and-tools.md">Mains et contrôleurs de mouvement</a></span><span class="sxs-lookup"><span data-stu-id="49442-172"><a href="hands-and-tools.md">Hands and motion controllers</a></span></span></td>
        <td><span data-ttu-id="49442-173">Je vois un maillage de main, je vois une affordance d’extrémité de doigt ou des rayons de contrôleur/sortant de la main.</span><span class="sxs-lookup"><span data-stu-id="49442-173">I see a hand mesh, I see a fingertip affordance or hand/controller rays.</span></span></td>
        <td><span data-ttu-id="49442-174">Des poignées déplaçables ou un rectangle englobant apparaissent quand ma main est proche d’un objet.</span><span class="sxs-lookup"><span data-stu-id="49442-174">I see grabbable handles or a bounding box appears when my hand is near an object.</span></span></td>
        <td><span data-ttu-id="49442-175">J’entends des tonalités et vois des animations quand je saisis ou libère un objet.</span><span class="sxs-lookup"><span data-stu-id="49442-175">I hear audible tones and see animations on grab and release.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="49442-176"><a href="gaze-and-commit.md">Suivre de la tête et valider</a></span><span class="sxs-lookup"><span data-stu-id="49442-176"><a href="gaze-and-commit.md">Head-gaze and commit</a></span></span></td>
        <td><span data-ttu-id="49442-177">Je vois un curseur au centre de mon champ de vision.</span><span class="sxs-lookup"><span data-stu-id="49442-177">I see a cursor in the center of my field of view.</span></span></td>
        <td><span data-ttu-id="49442-178">Le curseur oculaire de la tête change d’état en fonction de l’objet au-dessus duquel il se trouve.</span><span class="sxs-lookup"><span data-stu-id="49442-178">The head-gaze cursor changes state when it's over certain objects.</span></span></td>
        <td><span data-ttu-id="49442-179">Je vois/j’entends des confirmations visuelles et sonores quand j’effectue une action.</span><span class="sxs-lookup"><span data-stu-id="49442-179">I see/hear visual and audible confirmations when I take action.</span></span></td>
    </tr>   
    <tr>
        <td><span data-ttu-id="49442-180"><a href="hands-free.md">Mains-libres (Suivre de la tête et stabiliser)</a></span><span class="sxs-lookup"><span data-stu-id="49442-180"><a href="hands-free.md">Hands-free (Head-gaze and dwell)</a></span></span></td>
        <td><span data-ttu-id="49442-181">Je vois un curseur au centre de mon champ de vision.</span><span class="sxs-lookup"><span data-stu-id="49442-181">I see a cursor in the center of my field of view.</span></span></td>
        <td><span data-ttu-id="49442-182">Je vois un indicateur de progression quand je reste sur un objet avec interaction possible.</span><span class="sxs-lookup"><span data-stu-id="49442-182">I see a progress indicator when I dwell on an interactable object.</span></span></td>
        <td><span data-ttu-id="49442-183">Je vois/j’entends des confirmations visuelles et sonores quand j’effectue une action.</span><span class="sxs-lookup"><span data-stu-id="49442-183">I see/hear visual and audible confirmations when I take action.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="49442-184"><a href="hands-free.md">Mains-libres (commander avec la voix)</a></span><span class="sxs-lookup"><span data-stu-id="49442-184"><a href="hands-free.md">Hands-free (Voice commanding)</a></span></span></td>
        <td><span data-ttu-id="49442-185">Je vois un indicateur à l’écoute et des légendes qui montrent ce que le système a entendu.</span><span class="sxs-lookup"><span data-stu-id="49442-185">I see a listening indicator and captions that show what the system heard.</span></span></td>
        <td><span data-ttu-id="49442-186">J’obtiens des indicateurs et des invites vocales.</span><span class="sxs-lookup"><span data-stu-id="49442-186">I get voice prompts and hints.</span></span> <span data-ttu-id="49442-187">Quand je dis : Qu’est-ce que je dis ?</span><span class="sxs-lookup"><span data-stu-id="49442-187">When I say: "What can I say?"</span></span> <span data-ttu-id="49442-188">je vois un retour.</span><span class="sxs-lookup"><span data-stu-id="49442-188">I see feedback.</span></span></td>
        <td><span data-ttu-id="49442-189">Je vois/entends des confirmations visuelles et sonores quand je donne une commande ou obtiens une expérience utilisateur de levée d’ambiguïté si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="49442-189">I see/ hear visual and audible confirmations when I give a command, or get disambiguation UX when needed.</span></span></a></td>
    </tr>
</table>

### <a name="below-are-the-questions-that-weve-found-help-teams-select-an-interaction-model"></a><span data-ttu-id="49442-190">Voici les questions qui, d’après nous, aident les équipes à sélectionner un modèle d’interaction :</span><span class="sxs-lookup"><span data-stu-id="49442-190">Below are the questions that we've found help teams select an interaction model:</span></span>
 
1.  <span data-ttu-id="49442-191">Q :  Les utilisateurs souhaitent-ils toucher des hologrammes et effectuer des manipulations holographiques de précision ?</span><span class="sxs-lookup"><span data-stu-id="49442-191">Q:  Do my users want to touch holograms and perform precision holographic manipulations?</span></span><br><br>
<span data-ttu-id="49442-192">R :  Si tel est le cas, consultez le modèle d’interaction Mains et contrôleurs de mouvement pour le ciblage et la manipulation de précision avec les mains ou des contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="49442-192">A:  If so, check out the Hands and motion controllers interaction model for precision targeting and manipulation with hands or motion controllers.</span></span>
 
2.  <span data-ttu-id="49442-193">Q :  Les utilisateurs doivent-ils conserver leurs mains libres pour les tâches réelles ?</span><span class="sxs-lookup"><span data-stu-id="49442-193">Q:  Do my users need to keep their hands free for real-world tasks?</span></span><br><br>
<span data-ttu-id="49442-194">R :  Si tel est le cas, examinez le modèle d’interaction sans les mains, qui fournit une excellente expérience sans les mains par le biais d’interactions vocales et par pointage du regard.</span><span class="sxs-lookup"><span data-stu-id="49442-194">A:  If so, take a look at the Hands-free interaction model, which provides a great hands-free experience through gaze and voice-based interactions.</span></span>
 
3.  <span data-ttu-id="49442-195">Q :  Les utilisateurs ont-ils le temps d’apprendre les interactions pour mon application de réalité mixte ou ont-ils besoin des interactions présentant la courbe d’apprentissage la plus basse possible ?</span><span class="sxs-lookup"><span data-stu-id="49442-195">Q:  Do my users have time to learn interactions for my MR application or do they need the interactions with the lowest learning curve possible?</span></span><br><br>
<span data-ttu-id="49442-196">R :  Nous recommandons le modèle Mains et contrôleurs de mouvement pour la courbe d’apprentissage la plus basse et les interactions les plus intuitives, sous réserve que les utilisateurs puissent recourir à leurs mains pour les interactions.</span><span class="sxs-lookup"><span data-stu-id="49442-196">A:  We recommend the Hands and motion controllers model for the lowest learning curve and most intuitive interactions, as long as users are able to use their hands for interaction.</span></span>
 
4.  <span data-ttu-id="49442-197">Q :  Les utilisateurs utilisent-ils des contrôleurs de mouvement pour les opérations de pointage et de manipulation ?</span><span class="sxs-lookup"><span data-stu-id="49442-197">Q:  Do my users use motion controllers for pointing and manipulation?</span></span><br><br>
<span data-ttu-id="49442-198">R :  Le modèle Mains et contrôleurs de mouvement inclut tous les conseils pour une bonne expérience des contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="49442-198">A:  The Hands and motion controllers model includes all guidance for a great experience with motion controllers.</span></span>
 
5.  <span data-ttu-id="49442-199">Q :  Les utilisateurs se servent-ils d’un contrôleur d’accessibilité ou d’un contrôleur Bluetooth courant, tel qu’un dispositif de clic ?</span><span class="sxs-lookup"><span data-stu-id="49442-199">Q:  Do my users use an accessibility controller or a common Bluetooth controller, such as a clicker?</span></span><br><br>
<span data-ttu-id="49442-200">R :  Nous recommandons le modèle Suivre de la tête et valider pour tous les contrôleurs non suivis.</span><span class="sxs-lookup"><span data-stu-id="49442-200">A:  We recommend the Head-gaze and commit model for all non-tracked controllers.</span></span> <span data-ttu-id="49442-201">Il est conçu pour permettre à un utilisateur de parcourir une expérience entière avec un simple mécanisme de type « ciblage et validation ».</span><span class="sxs-lookup"><span data-stu-id="49442-201">It's designed to allow a user to traverse an entire experience with a simple "target and commit" mechanism.</span></span> 
 
6.  <span data-ttu-id="49442-202">Q : Les utilisateurs progressent-ils dans une expérience uniquement par le biais de clics (comme dans un environnement de type diaporama 3D), par opposition à la navigation dans des dispositions denses de contrôles d’interface utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="49442-202">Q: Do my users only progress through an experience by "clicking through" (for example in a 3D slideshow-like environment), as opposed to navigating dense layouts of UI controls?</span></span><br><br>
<span data-ttu-id="49442-203">R :  Si les utilisateurs n’ont pas besoin de contrôler une interface utilisateur conséquente, le modèle Suivre de la tête et valider offre une option accessible où ils n’ont pas besoin de se soucier du ciblage.</span><span class="sxs-lookup"><span data-stu-id="49442-203">A:  If users do not need to control a lot of UI, Head-gaze and commit offers a learnable option where users do not have to worry about targeting.</span></span> 
 
7.  <span data-ttu-id="49442-204">Q :  Les utilisateurs utilisent-ils à la fois des casques immersifs appareil HoloLens (1ère génération) et HoloLens 2/Windows Mixed Reality (VR) ?</span><span class="sxs-lookup"><span data-stu-id="49442-204">Q:  Do my users use both HoloLens (1st gen) and HoloLens 2/Windows Mixed Reality immersive headsets (VR)?</span></span><br><br>
<span data-ttu-id="49442-205">R :  Dans la mesure où le modèle Suivre de la tête et valider est le modèle d’interaction pour HoloLens (1ère génération), nous recommandons aux créateurs qui prennent en charge HoloLens (1ère génération) d’utiliser ce modèle pour les fonctionnalités ou les modes que les utilisateurs vivront sur un casque HoloLens (1ère génération).</span><span class="sxs-lookup"><span data-stu-id="49442-205">A:  Since Head-gaze and commit is the interaction model for HoloLens (1st gen), we recommend that creators who support HoloLens (1st gen) use Head-gaze and commit for any features or modes that users will experience on a HoloLens (1st gen) headset.</span></span> <span data-ttu-id="49442-206">Consultez la section ci-dessous *Passage d’un modèle d’interaction à un autre* pour plus d’informations sur la création d’une expérience optimale pour plusieurs générations de dispositifs HoloLens.</span><span class="sxs-lookup"><span data-stu-id="49442-206">Please see the next section below on *Transitioning interaction models* for details on making a great experience for multiple HoloLens generations.</span></span>
 
8.  <span data-ttu-id="49442-207">Q : Qu’en est-il des utilisateurs qui sont généralement mobiles, dans un large espace ou en raison de déplacements entre des espaces, et des utilisateurs qui ont tendance à travailler dans un seul espace ?</span><span class="sxs-lookup"><span data-stu-id="49442-207">Q: What about users who are generally mobile, covering a large space or moving between spaces, versus users who tend to work in a single space?</span></span><br><br>
<span data-ttu-id="49442-208">R :  Tous les modèles d’interaction fonctionnent pour ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="49442-208">A:  Any of the interaction models will work for these users.</span></span>  

> [!NOTE]
> <span data-ttu-id="49442-209">Des conseils spécifiques à la conception d’applications seront [bientôt](index.md#news-and-notes) disponibles.</span><span class="sxs-lookup"><span data-stu-id="49442-209">More guidance specific to app design [coming soon](index.md#news-and-notes).</span></span>


## <a name="transitioning-interaction-models"></a><span data-ttu-id="49442-210">Passage d’un modèle d’interaction à un autre</span><span class="sxs-lookup"><span data-stu-id="49442-210">Transitioning interaction models</span></span>
<span data-ttu-id="49442-211">Certains cas d’usage peuvent nécessiter l’utilisation de plusieurs modèles d’interaction.</span><span class="sxs-lookup"><span data-stu-id="49442-211">There are also use cases that might require utilizing more than one interaction model.</span></span> <span data-ttu-id="49442-212">Par exemple, le flux de création de votre application utilise le modèle d’interaction Mains et contrôleurs de mouvement, mais vous souhaitez employer un mode sans mains pour les techniciens de terrain.</span><span class="sxs-lookup"><span data-stu-id="49442-212">For example, your application's creation flow utilizes the Hands and motion controllers interaction model, but you want to employ a hands-free mode for field technicians.</span></span>  

<span data-ttu-id="49442-213">Si votre expérience requiert plusieurs modèles d’interaction, n’oubliez pas que de nombreux utilisateurs finaux peuvent rencontrer des difficultés pour passer d’un modèle à un autre, en particulier les utilisateurs pour lesquels la réalité mixte est une nouveauté.</span><span class="sxs-lookup"><span data-stu-id="49442-213">If your experience does require multiple interaction models, keep in mind that many end users might encounter difficulty when transitioning from one model to another--especially for users who are new to mixed reality.</span></span>

> [!Note]
> <span data-ttu-id="49442-214">Nous travaillons en permanence sur des conseils supplémentaires qui seront mis à la disposition des développeurs et des concepteurs et les informeront de la manière, du moment et de la raison de l’utilisation de plusieurs modèles d’interaction RM.</span><span class="sxs-lookup"><span data-stu-id="49442-214">We're constantly working on more guidance that will be available to developers and designers, informing them about the how, when, and why for using multiple MR interaction models.</span></span>
 

## <a name="see-also"></a><span data-ttu-id="49442-215">Voir également</span><span class="sxs-lookup"><span data-stu-id="49442-215">See also</span></span>
* [<span data-ttu-id="49442-216">Suivre de la tête et valider</span><span class="sxs-lookup"><span data-stu-id="49442-216">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="49442-217">Suivre de la tête et stabiliser</span><span class="sxs-lookup"><span data-stu-id="49442-217">Head-gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="49442-218">Manipulation directe avec les mains</span><span class="sxs-lookup"><span data-stu-id="49442-218">Direct manipulation with hands</span></span>](direct-manipulation.md)
* [<span data-ttu-id="49442-219">Pointer et valider avec les mains</span><span class="sxs-lookup"><span data-stu-id="49442-219">Point and commit with hands</span></span>](point-and-commit.md)
* [<span data-ttu-id="49442-220">Mouvements</span><span class="sxs-lookup"><span data-stu-id="49442-220">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="49442-221">Commander avec la voix</span><span class="sxs-lookup"><span data-stu-id="49442-221">Voice commanding</span></span>](voice-design.md)
* [<span data-ttu-id="49442-222">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="49442-222">Motion controllers</span></span>](motion-controllers.md)
* [<span data-ttu-id="49442-223">Conception du son spatial</span><span class="sxs-lookup"><span data-stu-id="49442-223">Spatial sound design</span></span>](spatial-sound-design.md)
* [<span data-ttu-id="49442-224">Conception du mappage spatial</span><span class="sxs-lookup"><span data-stu-id="49442-224">Spatial mapping design</span></span>](spatial-mapping-design.md)
* [<span data-ttu-id="49442-225">Confort</span><span class="sxs-lookup"><span data-stu-id="49442-225">Comfort</span></span>](comfort.md)

