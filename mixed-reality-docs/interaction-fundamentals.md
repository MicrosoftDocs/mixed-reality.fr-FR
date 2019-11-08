---
title: Interactions instinctives
description: Découvrez que les interactions simples et instinctives sont étroitement liées dans la plateforme de réalité mixte.
author: shengkait
ms.author: shentan
ms.date: 04/11/2019
ms.topic: article
ms.localizationpriority: high
keywords: Mixed Reality, pointage du regard, ciblage avec le regard, interaction, conception, hololens, MMR, multimodal
ms.openlocfilehash: abd82947be08a2f6aecc4462abc34c4674abfb7a
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437977"
---
# <a name="introducing-instinctual-interactions"></a><span data-ttu-id="f59bd-104">Présentation des interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="f59bd-104">Introducing instinctual interactions</span></span>

<span data-ttu-id="f59bd-105">Les interactions simples et instinctuelles sont étroitement liées dans la plateforme de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="f59bd-105">The philosophy of simple, instinctual interactions is interwoven throughout the mixed reality (MR) platform.</span></span> <span data-ttu-id="f59bd-106">Nous avons suivi trois étapes pour que les développeurs et concepteurs d’applications puissent proposer des interactions faciles et intuitives à leurs clients.</span><span class="sxs-lookup"><span data-stu-id="f59bd-106">We've taken three steps to ensure that application designers and developers can provide their customers with easy and intuitive interactions.</span></span> 

<span data-ttu-id="f59bd-107">Tout d’abord, nous avons veillé à combiner en modèles d’interaction multimodale fluides nos capteurs et nos technologies d’entrée (notamment le suivi de la main et oculaire, associé à l’entrée de langage naturel).</span><span class="sxs-lookup"><span data-stu-id="f59bd-107">First, we've made sure our sensors and input technologies (which includes hand and eye tracking along with natural language input) combine into seamless, multimodal interaction models.</span></span>  
<span data-ttu-id="f59bd-108">Selon nos recherches, la conception et le développement au sein d’un framework multimodal (plutôt qu’à partir d’entrées individuelles) sont essentiels à la création d’expériences instinctives.</span><span class="sxs-lookup"><span data-stu-id="f59bd-108">Based on our research, designing and developing within a multimodal framework (and not based on individual inputs) is the key to creating instinctual experiences.</span></span>

<span data-ttu-id="f59bd-109">Deuxièmement, nous sommes conscients que de nombreux développeurs ciblent plusieurs appareils HoloLens tels qu’HoloLens 2 et HoloLens (1ère génération) ou HoloLens et VR.</span><span class="sxs-lookup"><span data-stu-id="f59bd-109">Second, we recognize that many developers target multiple HoloLens devices, such as HoloLens 2 and HoloLens (1st gen) or HoloLens and VR.</span></span>  
<span data-ttu-id="f59bd-110">Nous avons donc conçu nos modèles d’interaction pour qu’ils fonctionnent sur tous les appareils, même si la technologie d’entrée varie d’un appareil à l’autre.</span><span class="sxs-lookup"><span data-stu-id="f59bd-110">So we've designed our interaction models to work across devices, even if the input technology varies on each device.</span></span>  
<span data-ttu-id="f59bd-111">Par exemple, une interaction de loin sur un casque immersif Windows avec un contrôleur 6DoF et une interaction de loin sur un appareil HoloLens 2 utilisent toutes deux des affordances et des schémas identiques, ce qui facilite le développement d’applications multi-appareils et la proposition d’une sensation naturelle aux interactions des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f59bd-111">For example, far interaction on a Windows Immersive headset with a 6DoF controller and far interaction on a HoloLens 2 both use identical affordances and patterns, making it easy for cross-device application development and providing a natural feel to user interactions.</span></span> 

<span data-ttu-id="f59bd-112">Face aux milliers d’interactions efficaces, attrayantes et magiques possibles qu’offre la réalité mixte, nous avons trouvé que l’utilisation intentionnelle d’un seul modèle d’interaction de bout en bout dans une application est le meilleur gage de réussite et d’expérience agréable pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f59bd-112">While we recognize that there are thousands of effective, engaging, and magical interactions possible in MR, we've found that intentionally employing a single interaction model end-to-end in an application is the best way to ensure users are successful and have a great experience.</span></span> <span data-ttu-id="f59bd-113">À cette fin, nous avons inclus trois choses dans ce guide d’interaction :</span><span class="sxs-lookup"><span data-stu-id="f59bd-113">To that end, we've included three things in this interaction guidance:</span></span>
* <span data-ttu-id="f59bd-114">Des instructions spécifiques autour des trois modèles d’interaction principaux et des composants et schémas requis pour chacun.</span><span class="sxs-lookup"><span data-stu-id="f59bd-114">Specific guidance around the three primary interaction models and the components and patterns required for each.</span></span>
* <span data-ttu-id="f59bd-115">Des conseils supplémentaires sur d’autres avantages qu’offre notre plateforme.</span><span class="sxs-lookup"><span data-stu-id="f59bd-115">Supplemental guidance about other benefits that our platform provides.</span></span>
* <span data-ttu-id="f59bd-116">Des conseils d’ordre général pour vous aider à sélectionner le modèle d’interaction approprié pour votre scénario.</span><span class="sxs-lookup"><span data-stu-id="f59bd-116">General guidance to help select the appropriate interaction model for your development scenario.</span></span>

## <a name="multimodal-interaction-models"></a><span data-ttu-id="f59bd-117">Modèles d’interaction multimodale</span><span class="sxs-lookup"><span data-stu-id="f59bd-117">Multimodal interaction models</span></span>

<span data-ttu-id="f59bd-118">D’après nos recherches et les commentaires des clients, trois modèles d’interaction principaux conviennent pour la majorité des expériences de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="f59bd-118">Based on our research and feedback from customers, we've discovered that three primary interaction models suit the majority of mixed reality experiences.</span></span> <span data-ttu-id="f59bd-119">À bien des égards, le modèle d’interaction est le modèle mental de l’utilisateur pour l’exécution d’un workflow.</span><span class="sxs-lookup"><span data-stu-id="f59bd-119">In many ways, the interaction model is the user's mental model for how to complete a workflow.</span></span> <span data-ttu-id="f59bd-120">Chacun de ces modèles d’interaction est optimisé pour un ensemble de besoins des clients et s’avère pratique, puissant et exploitable dans le cadre d’une utilisation correcte.</span><span class="sxs-lookup"><span data-stu-id="f59bd-120">Each of these interaction models is optimized for a set of customer needs and is convenient, powerful, and usable when used correctly.</span></span> 

<span data-ttu-id="f59bd-121">Le tableau ci-dessous offre une vue d’ensemble simplifiée.</span><span class="sxs-lookup"><span data-stu-id="f59bd-121">The chart below is a simplified overview.</span></span> <span data-ttu-id="f59bd-122">Vous pouvez cliquer sur les liens ci-après pour obtenir des informations détaillées sur l’utilisation de chaque modèle d’interaction, y compris des images et des exemples de code.</span><span class="sxs-lookup"><span data-stu-id="f59bd-122">Detailed information for using each interaction model is linked in the pages below with images and code samples.</span></span> 

<br>
<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="f59bd-123"><strong>Modèle</strong></span><span class="sxs-lookup"><span data-stu-id="f59bd-123"><strong>Model</strong></span></span></td>
        <td><span data-ttu-id="f59bd-124"><strong>Exemples de scénario</strong></span><span class="sxs-lookup"><span data-stu-id="f59bd-124"><strong>Example scenarios</strong></span></span></td>
        <td><span data-ttu-id="f59bd-125"><strong>Cadre</strong></span><span class="sxs-lookup"><span data-stu-id="f59bd-125"><strong>Fit</strong></span></span></td>
        <td><span data-ttu-id="f59bd-126"><strong>Matériel</strong></span><span class="sxs-lookup"><span data-stu-id="f59bd-126"><strong>Hardware</strong></span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f59bd-127"><a href="hands-and-tools.md">Mains et contrôleurs de mouvement</a></span><span class="sxs-lookup"><span data-stu-id="f59bd-127"><a href="hands-and-tools.md">Hands and motion controllers</a></span></span></td>
        <td><span data-ttu-id="f59bd-128">Expériences 3D spatiales telles que la conception et la disposition spatiales, la manipulation de contenu ou la simulation.</span><span class="sxs-lookup"><span data-stu-id="f59bd-128">3D spatial experiences, such as spatial layout and design, content manipulation, or simulation.</span></span></td>
        <td><span data-ttu-id="f59bd-129">Idéal pour les nouveaux utilisateurs en liaison avec la voix, le suivi oculaire ou le suivi de la tête.</span><span class="sxs-lookup"><span data-stu-id="f59bd-129">Great for new users coupled with voice, eye tracking or head gaze.</span></span> <span data-ttu-id="f59bd-130">Courbe d’apprentissage basse.</span><span class="sxs-lookup"><span data-stu-id="f59bd-130">Low learning curve.</span></span> <span data-ttu-id="f59bd-131">Expérience utilisateur cohérente entre le suivi de la main et les contrôleurs 6DoF.</span><span class="sxs-lookup"><span data-stu-id="f59bd-131">Consistent UX across hand tracking and 6DoF controllers.</span></span></td>
        <td><span data-ttu-id="f59bd-132">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="f59bd-132">HoloLens 2</span></span><br><span data-ttu-id="f59bd-133">Casques immersifs</span><span class="sxs-lookup"><span data-stu-id="f59bd-133">Immersive headsets</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f59bd-134"><a href="hands-free.md">Mains-libres</a></span><span class="sxs-lookup"><span data-stu-id="f59bd-134"><a href="hands-free.md">Hands-free</a></span></span></td>
        <td><span data-ttu-id="f59bd-135">Expériences contextuelles où les mains d’un utilisateur sont occupées, par exemple dans le cadre d’un apprentissage « sur le tas » et d’une maintenance.</span><span class="sxs-lookup"><span data-stu-id="f59bd-135">Contextual experiences where a user's hands are occupied, such as on-the-job learning and maintenance.</span></span></td>
        <td><span data-ttu-id="f59bd-136">Un apprentissage est requis.</span><span class="sxs-lookup"><span data-stu-id="f59bd-136">Some learning required.</span></span> <span data-ttu-id="f59bd-137">Si les mains ne sont pas disponibles, l’appareil peut être associé à la voix et au langage naturel.</span><span class="sxs-lookup"><span data-stu-id="f59bd-137">If hands are unavailable, the device pairs well with voice and natural language.</span></span></td>
        <td><span data-ttu-id="f59bd-138">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="f59bd-138">HoloLens 2</span></span><br><span data-ttu-id="f59bd-139">HoloLens (1ère génération)</span><span class="sxs-lookup"><span data-stu-id="f59bd-139">HoloLens (1st gen)</span></span><br><span data-ttu-id="f59bd-140">Casques immersifs</span><span class="sxs-lookup"><span data-stu-id="f59bd-140">Immersive headsets</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f59bd-141"><a href="gaze-and-commit.md">Pointer et valider</a></span><span class="sxs-lookup"><span data-stu-id="f59bd-141"><a href="gaze-and-commit.md">Gaze and commit</a></span></span></td>
        <td><span data-ttu-id="f59bd-142">Expériences au moyen de clics, par exemple, présentations 3D et démonstrations.</span><span class="sxs-lookup"><span data-stu-id="f59bd-142">Click-through experiences, e.g. 3D presentations, demos.</span></span></td>
        <td><span data-ttu-id="f59bd-143">Nécessite une formation sur les appareils HMD, mais pas sur mobile.</span><span class="sxs-lookup"><span data-stu-id="f59bd-143">Requires training on HMDs but not on mobile.</span></span> <span data-ttu-id="f59bd-144">Idéal pour les contrôleurs accessibles.</span><span class="sxs-lookup"><span data-stu-id="f59bd-144">Best for accessible controllers.</span></span> <span data-ttu-id="f59bd-145">Idéal pour HoloLens (1ère génération).</span><span class="sxs-lookup"><span data-stu-id="f59bd-145">Best for HoloLens (1st gen).</span></span></td>
        <td><span data-ttu-id="f59bd-146">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="f59bd-146">HoloLens 2</span></span><br><span data-ttu-id="f59bd-147">HoloLens (1ère génération)</span><span class="sxs-lookup"><span data-stu-id="f59bd-147">HoloLens (1st gen)</span></span><br><span data-ttu-id="f59bd-148">Casques immersifs</span><span class="sxs-lookup"><span data-stu-id="f59bd-148">Immersive headsets</span></span><br><span data-ttu-id="f59bd-149">Réalité augmentée mobile</span><span class="sxs-lookup"><span data-stu-id="f59bd-149">Mobile AR</span></span></td>
    </tr>
</table>
<br>

<span data-ttu-id="f59bd-150">Pour qu’il n’y ait pas de vides dans l’expérience d’interaction de l’utilisateur, le mieux est de suivre les conseils pour un modèle unique du début à la fin.</span><span class="sxs-lookup"><span data-stu-id="f59bd-150">To ensure that there are no gaps in the user interaction experience, it is best to follow the guidance for a single model from beginning to end.</span></span>

<span data-ttu-id="f59bd-151">Les sections ci-dessous décrivent les étapes de sélection et d’implémentation de l’un de ces modèles d’interaction.</span><span class="sxs-lookup"><span data-stu-id="f59bd-151">The sections below walk through the steps for selecting and implementing one of these interaction models.</span></span>  
 
### <a name="by-the-end-of-this-page-you-will-understand-our-guidance-on"></a><span data-ttu-id="f59bd-152">Quand vous parviendrez à la fin de cette page, vous comprendrez nos conseils sur :</span><span class="sxs-lookup"><span data-stu-id="f59bd-152">By the end of this page, you will understand our guidance on:</span></span>
 
* <span data-ttu-id="f59bd-153">Le choix d’un modèle d’interaction pour votre client</span><span class="sxs-lookup"><span data-stu-id="f59bd-153">Choosing an interaction model for your customer</span></span>
* <span data-ttu-id="f59bd-154">Implémentation du modèle d’interaction</span><span class="sxs-lookup"><span data-stu-id="f59bd-154">Implementing the interaction model</span></span>
* <span data-ttu-id="f59bd-155">Le passage d’un modèle d’interaction à un autre</span><span class="sxs-lookup"><span data-stu-id="f59bd-155">Transitioning between interaction models</span></span>
* <span data-ttu-id="f59bd-156">Les étapes suivantes de la conception</span><span class="sxs-lookup"><span data-stu-id="f59bd-156">Design next steps</span></span>


## <a name="choose-an-interaction-model-for-your-customer"></a><span data-ttu-id="f59bd-157">Choisir un modèle d’interaction pour votre client</span><span class="sxs-lookup"><span data-stu-id="f59bd-157">Choose an interaction model for your customer</span></span>

<span data-ttu-id="f59bd-158">Généralement, les développeurs et les créateurs ont envisagé les types d’interactions que leurs clients peuvent avoir.</span><span class="sxs-lookup"><span data-stu-id="f59bd-158">Typically, developers and creators have thought through the types of interactions that their customers can have.</span></span> <span data-ttu-id="f59bd-159">Pour encourager une approche conceptuelle axée sur le client, nous vous recommandons de suivre les conseils suivants afin de sélectionner le modèle d’interaction qui est optimisé pour votre client.</span><span class="sxs-lookup"><span data-stu-id="f59bd-159">To encourage a customer-focused approach to design, we recommend the following guidance for selecting the interaction model that's optimized for your customer.</span></span>

### <a name="why-follow-this-guidance"></a><span data-ttu-id="f59bd-160">Pourquoi suivre ces conseils ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-160">Why follow this guidance?</span></span>

* <span data-ttu-id="f59bd-161">Nos modèles d’interaction sont testés en fonction de critères objectifs et subjectifs tels que les efforts physiques et cognitifs, l’intuitivité et la facilité d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="f59bd-161">Our interaction models are tested for objective and subjective criteria, such as physical and cognitive effort, intuitiveness, and learnability.</span></span> 
* <span data-ttu-id="f59bd-162">Tout comme les interactions, les affordances visuelles/audio et le comportement des objets peuvent varier d’un modèle d’interaction à l’autre.</span><span class="sxs-lookup"><span data-stu-id="f59bd-162">Because interactions differ, visual/audio affordances and object behavior might differ between interaction models.</span></span>  
* <span data-ttu-id="f59bd-163">La combinaison de parties de plusieurs modèles d’interaction crée le risque d’affordances concurrentes, à l’image de rayons émanant de la main et d’un curseur oculaire simultanés.</span><span class="sxs-lookup"><span data-stu-id="f59bd-163">Combining parts of multiple interaction models creates the risk of competing affordances, such as simultaneous hand rays and a head-gaze cursor.</span></span> <span data-ttu-id="f59bd-164">Cette expérience peut submerger et perturber les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f59bd-164">This can overwhelm and confuse users.</span></span>

<span data-ttu-id="f59bd-165">Voici quelques exemples d’optimisation des affordances et des comportements pour chaque modèle d’interaction.</span><span class="sxs-lookup"><span data-stu-id="f59bd-165">Here are some examples of how affordances and behaviors are optimized for each interaction model.</span></span> <span data-ttu-id="f59bd-166">Nous constatons souvent que les nouveaux utilisateurs ont des questions similaires, telles que _« comment savoir si le système fonctionne ? »_ , _« comment savoir ce que je peux faire ? »_ et _« comment savoir s’il a compris ce que je viens de faire ? »_ .</span><span class="sxs-lookup"><span data-stu-id="f59bd-166">We often see new users have similar questions, such as _"how do I know the system is working"_, _"how do I know what I can do"_, and _"how do I know if it understood what I just did?"_</span></span>

<br>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="f59bd-167"><strong>Modèle</strong></span><span class="sxs-lookup"><span data-stu-id="f59bd-167"><strong>Model</strong></span></span></td>
        <td><span data-ttu-id="f59bd-168"><strong>Comment savoir si ça fonctionne ?</strong></span><span class="sxs-lookup"><span data-stu-id="f59bd-168"><strong>How do I know it's working?</strong></span></span></td>
        <td><span data-ttu-id="f59bd-169"><strong>Comment savoir ce que je peux faire ?</strong></span><span class="sxs-lookup"><span data-stu-id="f59bd-169"><strong>How do I know what I can do?</strong></span></span></td>
        <td><span data-ttu-id="f59bd-170"><strong>Comment savoir ce que je viens de faire ?</strong></span><span class="sxs-lookup"><span data-stu-id="f59bd-170"><strong>How do I know what I just did?</strong></span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f59bd-171"><a href="hands-and-tools.md">Mains et contrôleurs de mouvement</a></span><span class="sxs-lookup"><span data-stu-id="f59bd-171"><a href="hands-and-tools.md">Hands and motion controllers</a></span></span></td>
        <td><span data-ttu-id="f59bd-172">Je vois un maillage de main, une affordance d’extrémité de doigt ou des rayons de contrôleur/sortant de la main.</span><span class="sxs-lookup"><span data-stu-id="f59bd-172">I see a hand mesh, a fingertip affordance, or hand/controller rays.</span></span></td>
        <td><span data-ttu-id="f59bd-173">Des poignées déplaçables ou un rectangle englobant apparaissent quand ma main est proche d’un objet.</span><span class="sxs-lookup"><span data-stu-id="f59bd-173">I see grabbable handles, or a bounding box appears when my hand is near an object.</span></span></td>
        <td><span data-ttu-id="f59bd-174">J’entends des tonalités et vois des animations quand je saisis ou libère un objet.</span><span class="sxs-lookup"><span data-stu-id="f59bd-174">I hear audible tones and see animations on grab and release.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f59bd-175"><a href="gaze-and-commit.md">Suivre de la tête et valider</a></span><span class="sxs-lookup"><span data-stu-id="f59bd-175"><a href="gaze-and-commit.md">Head-gaze and commit</a></span></span></td>
        <td><span data-ttu-id="f59bd-176">Je vois un curseur au centre de mon champ de vision.</span><span class="sxs-lookup"><span data-stu-id="f59bd-176">I see a cursor in the center of my field of view.</span></span></td>
        <td><span data-ttu-id="f59bd-177">Le curseur change d’état en fonction de l’objet au-dessus duquel il se trouve.</span><span class="sxs-lookup"><span data-stu-id="f59bd-177">The cursor changes state when it's over certain objects.</span></span></td>
        <td><span data-ttu-id="f59bd-178">Je vois/j’entends des confirmations visuelles et sonores quand j’effectue une action.</span><span class="sxs-lookup"><span data-stu-id="f59bd-178">I see/hear visual and audible confirmations when I take action.</span></span></td>
    </tr>   
    <tr>
        <td><span data-ttu-id="f59bd-179"><a href="hands-free.md">Mains-libres (Suivre de la tête et stabiliser)</a></span><span class="sxs-lookup"><span data-stu-id="f59bd-179"><a href="hands-free.md">Hands-free (Head-gaze and dwell)</a></span></span></td>
        <td><span data-ttu-id="f59bd-180">Je vois un curseur au centre de mon champ de vision.</span><span class="sxs-lookup"><span data-stu-id="f59bd-180">I see a cursor in the center of my field of view.</span></span></td>
        <td><span data-ttu-id="f59bd-181">Je vois un indicateur de progression quand je reste sur un objet avec interaction possible.</span><span class="sxs-lookup"><span data-stu-id="f59bd-181">I see a progress indicator when I dwell on an interactable object.</span></span></td>
        <td><span data-ttu-id="f59bd-182">Je vois/j’entends des confirmations visuelles et sonores quand j’effectue une action.</span><span class="sxs-lookup"><span data-stu-id="f59bd-182">I see/hear visual and audible confirmations when I take action.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f59bd-183"><a href="hands-free.md">Mains-libres (commander avec la voix)</a></span><span class="sxs-lookup"><span data-stu-id="f59bd-183"><a href="hands-free.md">Hands-free (Voice commanding)</a></span></span></td>
        <td><span data-ttu-id="f59bd-184">Je vois un indicateur à l’écoute et des légendes qui montrent ce que le système a entendu.</span><span class="sxs-lookup"><span data-stu-id="f59bd-184">I see a listening indicator and captions that show what the system heard.</span></span></td>
        <td><span data-ttu-id="f59bd-185">J’obtiens des indicateurs et des invites vocales.</span><span class="sxs-lookup"><span data-stu-id="f59bd-185">I get voice prompts and hints.</span></span> <span data-ttu-id="f59bd-186">Quand je dis : Qu’est-ce que je dis ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-186">When I say: "What can I say?"</span></span> <span data-ttu-id="f59bd-187">je vois un retour.</span><span class="sxs-lookup"><span data-stu-id="f59bd-187">I see feedback.</span></span></td>
        <td><span data-ttu-id="f59bd-188">Je vois/entends des confirmations visuelles et sonores quand je donne une commande ou obtiens une expérience utilisateur de levée d’ambiguïté si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f59bd-188">I see/hear visual and audible confirmations when I give a command, or get disambiguation UX when needed.</span></span></a></td>
    </tr>
</table>

### <a name="below-are-questions-that-weve-found-help-teams-select-an-interaction-model"></a><span data-ttu-id="f59bd-189">Voici les questions qui, d’après nous, aident les équipes à sélectionner un modèle d’interaction :</span><span class="sxs-lookup"><span data-stu-id="f59bd-189">Below are questions that we've found help teams select an interaction model:</span></span>
 
1.  <span data-ttu-id="f59bd-190">Q :  Les utilisateurs souhaitent-ils toucher des hologrammes et effectuer des manipulations holographiques de précision ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-190">Q:  Do my users want to touch holograms and perform precision holographic manipulations?</span></span><br><br>
<span data-ttu-id="f59bd-191">R :  Si tel est le cas, consultez le modèle d’interaction Mains et contrôleurs de mouvement pour un ciblage et une manipulation de précision.</span><span class="sxs-lookup"><span data-stu-id="f59bd-191">A:  If so, check out the Hands and motion controllers interaction model for precision targeting and manipulation.</span></span>
 
2.  <span data-ttu-id="f59bd-192">Q :  Les utilisateurs doivent-ils conserver leurs mains libres pour les tâches réelles ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-192">Q:  Do my users need to keep their hands free for real-world tasks?</span></span><br><br>
<span data-ttu-id="f59bd-193">R :  Si tel est le cas, examinez le modèle d’interaction sans les mains, qui fournit une excellente expérience sans les mains par le biais d’interactions vocales et par pointage du regard.</span><span class="sxs-lookup"><span data-stu-id="f59bd-193">A:  If so, take a look at the Hands-free interaction model, which provides a great hands-free experience through gaze and voice-based interactions.</span></span>
 
3.  <span data-ttu-id="f59bd-194">Q :  Les utilisateurs ont-ils le temps d’apprendre les interactions pour mon application de réalité mixte ou ont-ils besoin des interactions présentant la courbe d’apprentissage la plus basse possible ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-194">Q:  Do my users have time to learn interactions for my MR application or do they need the interactions with the lowest learning curve possible?</span></span><br><br>
<span data-ttu-id="f59bd-195">R :  Nous recommandons le modèle Mains et contrôleurs de mouvement pour la courbe d’apprentissage la plus basse et les interactions les plus intuitives, sous réserve que les utilisateurs puissent recourir à leurs mains pour les interactions.</span><span class="sxs-lookup"><span data-stu-id="f59bd-195">A:  For the lowest learning curve and most intuitive interactions, we recommend the Hands and motion controllers model, as long as users are able to use their hands for interaction.</span></span>
 
4.  <span data-ttu-id="f59bd-196">Q :  Les utilisateurs utilisent-ils des contrôleurs de mouvement pour les opérations de pointage et de manipulation ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-196">Q:  Do my users use motion controllers for pointing and manipulation?</span></span><br><br>
<span data-ttu-id="f59bd-197">R :  Le modèle Mains et contrôleurs de mouvement inclut tous les conseils pour une bonne expérience des contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="f59bd-197">A:  The Hands and motion controllers model includes all guidance for a great experience with motion controllers.</span></span>
 
5.  <span data-ttu-id="f59bd-198">Q :  Les utilisateurs se servent-ils d’un contrôleur d’accessibilité ou d’un contrôleur Bluetooth courant, tel qu’un dispositif de clic ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-198">Q:  Do my users use an accessibility controller or a common Bluetooth controller, such as a clicker?</span></span><br><br>
<span data-ttu-id="f59bd-199">R :  Nous recommandons le modèle Suivre de la tête et valider pour tous les contrôleurs non suivis.</span><span class="sxs-lookup"><span data-stu-id="f59bd-199">A:  We recommend the Head-gaze and commit model for all non-tracked controllers.</span></span> <span data-ttu-id="f59bd-200">Il est conçu pour permettre à un utilisateur de parcourir une expérience entière avec un simple mécanisme de type « ciblage et validation ».</span><span class="sxs-lookup"><span data-stu-id="f59bd-200">It's designed to allow a user to traverse an entire experience with a simple "target and commit" mechanism.</span></span> 
 
6.  <span data-ttu-id="f59bd-201">Q : Les utilisateurs progressent-ils dans une expérience uniquement par le biais de clics (comme dans un environnement de type diaporama 3D), par opposition à la navigation dans des dispositions denses de contrôles d’interface utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-201">Q: Do my users only progress through an experience by "clicking through" (for example in a 3D slideshow-like environment), as opposed to navigating dense layouts of UI controls?</span></span><br><br>
<span data-ttu-id="f59bd-202">R :  Si les utilisateurs n’ont pas besoin de contrôler une interface utilisateur conséquente, le modèle Suivre de la tête et valider offre une option accessible où ils n’ont pas besoin de se soucier du ciblage.</span><span class="sxs-lookup"><span data-stu-id="f59bd-202">A:  If users do not need to control a lot of UI, Head-gaze and commit offers a learnable option where users do not have to worry about targeting.</span></span> 
 
7.  <span data-ttu-id="f59bd-203">Q :  Les utilisateurs utilisent-ils à la fois des casques immersifs appareil HoloLens (1ère génération) et HoloLens 2/Windows Mixed Reality (VR) ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-203">Q:  Do my users use both HoloLens (1st gen) and HoloLens 2/Windows Mixed Reality immersive headsets (VR)?</span></span><br><br>
<span data-ttu-id="f59bd-204">R :  Dans la mesure où le modèle Suivre de la tête et valider est le modèle d’interaction pour HoloLens (1ère génération), nous recommandons aux créateurs qui prennent en charge HoloLens (1ère génération) d’utiliser ce modèle pour les fonctionnalités ou les modes que les utilisateurs vivront sur un casque HoloLens (1ère génération).</span><span class="sxs-lookup"><span data-stu-id="f59bd-204">A:  Since Head-gaze and commit is the interaction model for HoloLens (1st gen), we recommend that creators who support HoloLens (1st gen) use Head-gaze and commit for any features or modes that users will experience on a HoloLens (1st gen) headset.</span></span> <span data-ttu-id="f59bd-205">Consultez la section ci-dessous *Passage d’un modèle d’interaction à un autre* pour plus d’informations sur la création d’une expérience optimale pour plusieurs générations de dispositifs HoloLens.</span><span class="sxs-lookup"><span data-stu-id="f59bd-205">Please see the next section below on *Transitioning interaction models* for details on making a great experience for multiple HoloLens generations.</span></span>
 
8.  <span data-ttu-id="f59bd-206">Q : Qu’en est-il des utilisateurs qui sont généralement mobiles, dans un large espace ou en raison de déplacements entre des espaces, et des utilisateurs qui ont tendance à travailler dans un seul espace ?</span><span class="sxs-lookup"><span data-stu-id="f59bd-206">Q: What about users who are generally mobile, covering a large space or moving between spaces, versus users who tend to work in a single space?</span></span><br><br>
<span data-ttu-id="f59bd-207">R :  Tous les modèles d’interaction fonctionnent pour ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f59bd-207">A:  Any of the interaction models will work for these users.</span></span>  

> [!NOTE]
> <span data-ttu-id="f59bd-208">Des conseils spécifiques à la conception d’applications seront [bientôt](news.md) disponibles.</span><span class="sxs-lookup"><span data-stu-id="f59bd-208">More guidance specific to app design [coming soon](news.md).</span></span>


## <a name="transitioning-interaction-models"></a><span data-ttu-id="f59bd-209">Passage d’un modèle d’interaction à un autre</span><span class="sxs-lookup"><span data-stu-id="f59bd-209">Transitioning interaction models</span></span>
<span data-ttu-id="f59bd-210">Certains cas d’usage peuvent nécessiter l’utilisation de plusieurs modèles d’interaction.</span><span class="sxs-lookup"><span data-stu-id="f59bd-210">There are also use cases that might require utilizing more than one interaction model.</span></span> <span data-ttu-id="f59bd-211">Par exemple, le flux de création de votre application utilise le modèle d’interaction _« Mains et contrôleurs de mouvement »_ , mais vous souhaitez employer un mode sans mains pour les techniciens de terrain.</span><span class="sxs-lookup"><span data-stu-id="f59bd-211">For example, your application's creation flow utilizes the _"hands and motion controllers"_ interaction model, but you want to employ a hands-free mode for field technicians.</span></span>
<span data-ttu-id="f59bd-212">Si votre expérience requiert plusieurs modèles d’interaction, n’oubliez pas que de nombreux utilisateurs peuvent rencontrer des difficultés pour passer d’un modèle à un autre, en particulier les utilisateurs pour lesquels la réalité mixte est une nouveauté.</span><span class="sxs-lookup"><span data-stu-id="f59bd-212">If your experience does require multiple interaction models, please keep in mind that many users might encounter difficulty when transitioning from one model to another, especially users who are new to mixed reality.</span></span>

> [!Note]
> <span data-ttu-id="f59bd-213">Nous travaillons en permanence sur des conseils supplémentaires qui seront mis à la disposition des développeurs et des concepteurs et les informeront de la manière, du moment et de la raison de l’utilisation de plusieurs modèles d’interaction RM.</span><span class="sxs-lookup"><span data-stu-id="f59bd-213">We're constantly working on more guidance that will be available to developers and designers, informing them about the how, when, and why for using multiple MR interaction models.</span></span>
 

## <a name="see-also"></a><span data-ttu-id="f59bd-214">Voir également</span><span class="sxs-lookup"><span data-stu-id="f59bd-214">See also</span></span>
* [<span data-ttu-id="f59bd-215">Confort</span><span class="sxs-lookup"><span data-stu-id="f59bd-215">Comfort</span></span>](comfort.md)
* [<span data-ttu-id="f59bd-216">Interaction basée sur le regard</span><span class="sxs-lookup"><span data-stu-id="f59bd-216">Eye-based interaction</span></span>](eye-gaze-interaction.md)
* [<span data-ttu-id="f59bd-217">Suivi oculaire sur HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="f59bd-217">Eye tracking on HoloLens 2</span></span>](eye-tracking.md)
* [<span data-ttu-id="f59bd-218">Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="f59bd-218">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="f59bd-219">Pointer du regard et fixer</span><span class="sxs-lookup"><span data-stu-id="f59bd-219">Gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="f59bd-220">Mains : Manipulation directe</span><span class="sxs-lookup"><span data-stu-id="f59bd-220">Hands - Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="f59bd-221">Mains : Mouvements</span><span class="sxs-lookup"><span data-stu-id="f59bd-221">Hands - Gestures</span></span>](gaze-and-commit.md#composite-gestures)
* [<span data-ttu-id="f59bd-222">Mains : Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="f59bd-222">Hands - Point and commit</span></span>](point-and-commit.md)
* [<span data-ttu-id="f59bd-223">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="f59bd-223">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="f59bd-224">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="f59bd-224">Motion controllers</span></span>](motion-controllers.md)
* [<span data-ttu-id="f59bd-225">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="f59bd-225">Spatial mapping</span></span>](spatial-mapping.md)
* [<span data-ttu-id="f59bd-226">Conception du son spatial</span><span class="sxs-lookup"><span data-stu-id="f59bd-226">Spatial sound design</span></span>](spatial-sound-design.md)
* [<span data-ttu-id="f59bd-227">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="f59bd-227">Voice input</span></span>](voice-input.md)


