---
title: Vue d’ensemble de l’interaction multimodale
description: Vue d’ensemble de l’interaction multimodale
author: shengkait
ms.author: shengkait
ms.date: 04/11/2019
ms.topic: article
keywords: Mixte réalité, regards, regards ciblant, interaction, concevoir
ms.openlocfilehash: 8c578d9a67f6809df69fb132f4c46a381726596e
ms.sourcegitcommit: d6d96d552ec10cd7e6502fbbc1905432e2878325
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2019
ms.locfileid: "65524336"
---
# <a name="introducing-instinctual-interactions"></a><span data-ttu-id="f713a-104">Présentation des interactions instinctual</span><span class="sxs-lookup"><span data-stu-id="f713a-104">Introducing instinctual interactions</span></span>
<span data-ttu-id="f713a-105">La philosophie d’interactions simples, instinctual nouée tout au long de la plateforme de réalité mixte de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f713a-105">The philosophy of simple, instinctual interactions is woven throughout the Microsoft Mixed Reality platform.</span></span>  <span data-ttu-id="f713a-106">Nous avons pris trois étapes pour vérifier que les développeurs et concepteurs d’applications peuvent fournir des interactions faciles et intuitives pour leurs clients.</span><span class="sxs-lookup"><span data-stu-id="f713a-106">We've taken three steps to ensure that application designers and developers can provide easy and intuitive interactions for their customers.</span></span> 

<span data-ttu-id="f713a-107">Tout d’abord, nous avons veillé à ce notre étonnant de capteurs et de la technologie d’entrée, notamment main suivi, suivi de le œil et langage naturel, combinent des modèles d’interaction multimodale transparente.</span><span class="sxs-lookup"><span data-stu-id="f713a-107">First, we've made sure our amazing sensors and input technology, including hand tracking, eye tracking, and natural language, combine into seamless multimodal interaction models.</span></span>  <span data-ttu-id="f713a-108">Selon nos recherches, conception et développement multi-modalement--et ne dépendent ne pas des entrées uniques--est essentiel à la création d’expériences instinctual.</span><span class="sxs-lookup"><span data-stu-id="f713a-108">Based on our research, designing and developing multimodally -- and not based on single inputs -- is the key to creating instinctual experiences.</span></span>

<span data-ttu-id="f713a-109">Deuxièmement, nous reconnaissons que de nombreux développeurs ciblent plusieurs appareils, que ce soit pour HoloLens 2 et HoloLens (1er gen) ou HoloLens et VR.</span><span class="sxs-lookup"><span data-stu-id="f713a-109">Secondly, we recognize that many developers target multiple devices, whether that means HoloLens 2 and HoloLens (1st gen) or HoloLens and VR.</span></span>  <span data-ttu-id="f713a-110">Par conséquent, nous avons conçu nos modèles d’interaction pour travailler sur des appareils (même si la technologie d’entrée varie sur chaque appareil).</span><span class="sxs-lookup"><span data-stu-id="f713a-110">So we've designed our interaction models to work across devices (even if the input technology varies on each device).</span></span>  <span data-ttu-id="f713a-111">Par exemple, interaction lointain sur casque Immersive de Windows avec un contrôleur 6DoF et lointain interaction sur les deux 2 HoloLens utiliser l’intuitivité identiques et les modèles, ce qui facilite pour les applications entre les périphériques.</span><span class="sxs-lookup"><span data-stu-id="f713a-111">For example, far interaction on a Windows Immersive headset with a 6DoF controller and far interaction on a HoloLens 2 both use the identical affordances and patterns, making it easy for cross-device applications.</span></span> <span data-ttu-id="f713a-112">Est non seulement ce pratique pour les développeurs et concepteurs, mais il a l’air normal pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="f713a-112">Not only is this convenient for developers and designers, but it feels natural to end users.</span></span> 

<span data-ttu-id="f713a-113">Enfin, alors que nous reconnaissons qu’il existe des milliers d’effective, attrayantes et interactions magiques possibles dans MR, nous avons trouvé cette intentionnellement utilisant un modèle d’interaction unique bout en bout dans une application est la meilleure façon de garantir aux utilisateurs réussissent et offrir une bonne expérience.</span><span class="sxs-lookup"><span data-stu-id="f713a-113">Lastly, while we recognize that there are thousands of effective, engaging, and magical interactions possible in MR, we have found that intentionally employing a single interaction model end to end in an application is the best way to ensure users are successful and have a great experience.</span></span>  <span data-ttu-id="f713a-114">À cette fin, nous avons inclus les trois choses dans ce guide de l’interaction :</span><span class="sxs-lookup"><span data-stu-id="f713a-114">To that end, we've included three things in this interaction guidance:</span></span>
* <span data-ttu-id="f713a-115">Nous avons structuré ce guide autour de trois modèles d’interaction principal et les composants et les modèles requis pour chaque</span><span class="sxs-lookup"><span data-stu-id="f713a-115">We've structured this guidance around the three primary interaction models and the components and patterns required for each</span></span>
* <span data-ttu-id="f713a-116">Nous avons inclus des conseils supplémentaires sur les autres avantages offerts par notre plateforme</span><span class="sxs-lookup"><span data-stu-id="f713a-116">We've included supplemental guidance on other benefits that our platform provides</span></span>
* <span data-ttu-id="f713a-117">Nous avons inclus des conseils pour aider à sélectionner le modèle d’interaction approprié pour votre scénario</span><span class="sxs-lookup"><span data-stu-id="f713a-117">We've included guidance to help select the appropriate interaction model for your scenario</span></span>


## <a name="three-multimodal-interaction-models"></a><span data-ttu-id="f713a-118">Trois modèles d’interaction multimodale</span><span class="sxs-lookup"><span data-stu-id="f713a-118">Three multimodal interaction models</span></span>
<span data-ttu-id="f713a-119">Selon notre recherche et la collaboration avec les clients à ce jour, nous avons découvert que les trois modèles d’interaction principal adapter à la majorité des expériences de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="f713a-119">Based on our research and work with customers to date, we've discovered that three primary interaction models suit the majority of Mixed Reality experiences.</span></span>

<span data-ttu-id="f713a-120">Dans bien des égards, le modèle d’interaction est modèle mental de l’utilisateur pour l’exécution de leurs flux.</span><span class="sxs-lookup"><span data-stu-id="f713a-120">In many ways, the interaction model  is the user's mental model for completing their flows.</span></span>  <span data-ttu-id="f713a-121">Chacun de ces modèles d’interaction est optimisé pour un ensemble de besoins des clients, et chacun est utilisable à part entière, puissant et pratique.</span><span class="sxs-lookup"><span data-stu-id="f713a-121">Each of these interaction models is optimized for a set of customer needs, and each is convenient, powerful, and usable in its own right.</span></span> 

<span data-ttu-id="f713a-122">Le tableau ci-dessous est une vue d’ensemble simplifiée.</span><span class="sxs-lookup"><span data-stu-id="f713a-122">The chart below is a simplified overview.</span></span>  <span data-ttu-id="f713a-123">Des informations détaillées pour l’utilisation de chaque modèle d’interaction sont liées dans les pages ci-dessous avec des images et des exemples de code.</span><span class="sxs-lookup"><span data-stu-id="f713a-123">Detailed information for using each interaction model is linked in the pages below with images and code samples.</span></span>  

<br>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="f713a-124"><strong>Modèle</strong></span><span class="sxs-lookup"><span data-stu-id="f713a-124"><strong>Model</strong></span></span></td>
        <td><span data-ttu-id="f713a-125"><strong>Exemples de scénarios</strong></span><span class="sxs-lookup"><span data-stu-id="f713a-125"><strong>Example scenarios</strong></span></span></td>
        <td><span data-ttu-id="f713a-126"><strong>Fit</strong></span><span class="sxs-lookup"><span data-stu-id="f713a-126"><strong>Fit</strong></span></span></td>
        <td><span data-ttu-id="f713a-127"><strong>Matériel</strong></span><span class="sxs-lookup"><span data-stu-id="f713a-127"><strong>Hardware</strong></span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f713a-128"><a href="hands-and-tools.md">Mains et outils</a></span><span class="sxs-lookup"><span data-stu-id="f713a-128"><a href="hands-and-tools.md">Hands and tools</a></span></span></td>
        <td><span data-ttu-id="f713a-129">Expériences spatiales 3D</span><span class="sxs-lookup"><span data-stu-id="f713a-129">3D spatial experiences</span></span><br><span data-ttu-id="f713a-130">par exemple, spatiale disposition et conception, manipulation de contenu ou simulation</span><span class="sxs-lookup"><span data-stu-id="f713a-130">e.g. spatial layout and design, content manipulation, or simulation</span></span></td>
        <td><span data-ttu-id="f713a-131">Idéal pour les nouveaux utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f713a-131">Great for new users</span></span><br><span data-ttu-id="f713a-132">Courbe d’apprentissage basse</span><span class="sxs-lookup"><span data-stu-id="f713a-132">Low learning curve</span></span><br><span data-ttu-id="f713a-133">Ancrée dans intuitivité visual facile</span><span class="sxs-lookup"><span data-stu-id="f713a-133">Grounded in easy visual affordances</span></span><br><span data-ttu-id="f713a-134">Expérience utilisateur cohérente entre main suivi et 6DoF contrôleurs</span><span class="sxs-lookup"><span data-stu-id="f713a-134">Consistent UX across hand tracking and 6DoF controllers</span></span><br><span data-ttu-id="f713a-135">Très bien associée à la voix, suivi de le œil ou head les regards</span><span class="sxs-lookup"><span data-stu-id="f713a-135">Great when coupled with voice, eye tracking, or head gaze</span></span></td>
        <td><span data-ttu-id="f713a-136">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="f713a-136">HoloLens 2</span></span><br><span data-ttu-id="f713a-137">Windows immersives avec 6DoF contrôleurs</span><span class="sxs-lookup"><span data-stu-id="f713a-137">Windows Immersive w/ 6DoF Controllers</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f713a-138"><a href="hands-free.md">Mains-libres</a></span><span class="sxs-lookup"><span data-stu-id="f713a-138"><a href="hands-free.md">Hands-free</a></span></span></td>
        <td><span data-ttu-id="f713a-139">Expériences contextuelles, où les mains d’un utilisateur sont occupés par exemple, sur le travail d’apprentissage, de maintenance</span><span class="sxs-lookup"><span data-stu-id="f713a-139">Contextual experiences where a user's hands are occupied e.g. on the-job learning, maintenance</span></span></td>
        <td><span data-ttu-id="f713a-140">Certaines de formation requise</span><span class="sxs-lookup"><span data-stu-id="f713a-140">Some learning required</span></span><br><span data-ttu-id="f713a-141">Si les mains ne sont pas disponibles</span><span class="sxs-lookup"><span data-stu-id="f713a-141">If hands are unavailable</span></span><br><span data-ttu-id="f713a-142">paires bien avec la voix et de langage naturel</span><span class="sxs-lookup"><span data-stu-id="f713a-142">pairs well with voice and natural language</span></span></td>
        <td><span data-ttu-id="f713a-143">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="f713a-143">HoloLens 2</span></span><br><span data-ttu-id="f713a-144">HoloLens (1er gen)</span><span class="sxs-lookup"><span data-stu-id="f713a-144">HoloLens (1st gen)</span></span><br> <span data-ttu-id="f713a-145">Immersive de Windows</span><span class="sxs-lookup"><span data-stu-id="f713a-145">Windows Immersive</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f713a-146"><a href="gaze-and-commit.md">Pointer du regard vers l’avant et valider</a></span><span class="sxs-lookup"><span data-stu-id="f713a-146"><a href="gaze-and-commit.md">Head-gaze and commit</a></span></span></td>
        <td><span data-ttu-id="f713a-147">Par exemple, 3D des présentations, démos des expériences clic</span><span class="sxs-lookup"><span data-stu-id="f713a-147">Click-through experiences e.g. 3D presentations, demos</span></span></td>
        <td><span data-ttu-id="f713a-148">Nécessite une formation sur HMDs, mais pas sur mobile</span><span class="sxs-lookup"><span data-stu-id="f713a-148">Requires training on HMDs but not on mobile</span></span><br><span data-ttu-id="f713a-149">Idéal pour les contrôleurs accessibles</span><span class="sxs-lookup"><span data-stu-id="f713a-149">Best for accessible controllers</span></span><br><span data-ttu-id="f713a-150">Idéal pour HoloLens (1er gen)</span><span class="sxs-lookup"><span data-stu-id="f713a-150">Best for HoloLens (1st gen)</span></span></td>
        <td><span data-ttu-id="f713a-151">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="f713a-151">HoloLens 2</span></span><br><span data-ttu-id="f713a-152">HoloLens (1er gen)</span><span class="sxs-lookup"><span data-stu-id="f713a-152">HoloLens (1st gen)</span></span><br> <span data-ttu-id="f713a-153">Immersive de Windows</span><span class="sxs-lookup"><span data-stu-id="f713a-153">Windows Immersive</span></span><br> <span data-ttu-id="f713a-154">Mobile AR</span><span class="sxs-lookup"><span data-stu-id="f713a-154">Mobile AR</span></span></td>
    </tr>
</table>
<br>

<span data-ttu-id="f713a-155">Pour vous assurer qu’aucun vides ou les trous dans l’interaction de votre expérience, la meilleure consiste à suivre les recommandations pour un seul modèle à partir du début à la fin.</span><span class="sxs-lookup"><span data-stu-id="f713a-155">The best way to ensure there are no gaps or holes in the interaction for your experience is to follow the guidance for a single model from beginning to end.</span></span> 

<span data-ttu-id="f713a-156">Pour accélérer le développement et conception, nous avons inclus des informations détaillées et des liens vers des images et des exemples de code au sein de notre couverture de chaque modèle.</span><span class="sxs-lookup"><span data-stu-id="f713a-156">To speed design and development, we've included detailed information and links to images and code samples within our coverage of each model.</span></span>

<span data-ttu-id="f713a-157">Mais tout d’abord, les sections ci-dessous décrivent les étapes de sélection et d’implémentation de l’un de ces modèles d’interaction.</span><span class="sxs-lookup"><span data-stu-id="f713a-157">But first, the sections below walk through the steps of selecting and implementing one of these interaction models.</span></span>  
 
### <a name="by-the-end-of-this-page-you-will-understand-our-guidance-on"></a><span data-ttu-id="f713a-158">À la fin de cette page, vous comprendrez nos conseils sur :</span><span class="sxs-lookup"><span data-stu-id="f713a-158">By the end of this page, you will understand our guidance on:</span></span>
 
* <span data-ttu-id="f713a-159">Choix d’un modèle d’interaction pour votre client</span><span class="sxs-lookup"><span data-stu-id="f713a-159">Choosing an interaction model for your customer</span></span>
* <span data-ttu-id="f713a-160">En utilisant les instructions de modèle d’interaction</span><span class="sxs-lookup"><span data-stu-id="f713a-160">Using the interaction model guidance</span></span>
* <span data-ttu-id="f713a-161">Transition entre les modèles d’interaction</span><span class="sxs-lookup"><span data-stu-id="f713a-161">Transitioning between interaction models</span></span>
* <span data-ttu-id="f713a-162">Étapes de conception</span><span class="sxs-lookup"><span data-stu-id="f713a-162">Design next steps</span></span>

## <a name="choosing-an-interaction-model-for-your-customer"></a><span data-ttu-id="f713a-163">Choix d’un modèle d’interaction pour votre client</span><span class="sxs-lookup"><span data-stu-id="f713a-163">Choosing an interaction model for your customer</span></span>

<span data-ttu-id="f713a-164">Les développeurs et les créateurs de disposent déjà probablement quelques idées à l’esprit des types d’expérience d’interaction qu’ils souhaitent pour leurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f713a-164">Most likely, developers and creators already have some ideas in mind of the kinds of interaction experience they want for their users.</span></span>
<span data-ttu-id="f713a-165">Pour encourager une approche axée sur le client pour concevoir, nous vous recommandons de suivre les instructions ci-dessous pour sélectionner le modèle d’interaction qui est optimisé pour votre client.</span><span class="sxs-lookup"><span data-stu-id="f713a-165">To encourage a customer-focused approach to design, we recommend following the guidance below to select the interaction model that's optimized for your customer.</span></span>

### <a name="why-follow-this-guidance"></a><span data-ttu-id="f713a-166">Pourquoi suivre ce guide ?</span><span class="sxs-lookup"><span data-stu-id="f713a-166">Why follow this guidance?</span></span>

* <span data-ttu-id="f713a-167">Nos modèles d’interaction sont testés pour les objectifs et critères subjectifs tels que des efforts physiques et cognitive, intuitiveness et learnability.</span><span class="sxs-lookup"><span data-stu-id="f713a-167">Our interaction models are tested for objective and subjective criteria such as physical and cognitive effort, intuitiveness, and learnability.</span></span> 
* <span data-ttu-id="f713a-168">Car diffère de l’interaction, intuitivité audio et visuelles et comportement des objets peuvent également différer entre les modèles d’interaction.</span><span class="sxs-lookup"><span data-stu-id="f713a-168">Because interaction differs, visual and audio affordances and object behavior may also differ between the interaction models.</span></span>  
* <span data-ttu-id="f713a-169">Combinant des parties de plusieurs modèles d’interaction crée le risque de concurrents intuitivité, telles que des rayons main simultanées et un curseur en regard, qui submerger et la confusion chez les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f713a-169">Combining parts of multiple interaction models together creates the risk of competing affordances, such as simultaneous hand rays and a gaze cursor, which overwhelm and confuse users.</span></span>

<span data-ttu-id="f713a-170">Voici quelques exemples de la façon dont les intuitivité et comportements sont optimisés pour chaque modèle d’interaction.</span><span class="sxs-lookup"><span data-stu-id="f713a-170">Here are some examples of how affordances and behaviors are optimized for each interaction model.</span></span>  <span data-ttu-id="f713a-171">Nous le constatons souvent nouveaux utilisateurs en tant que des questions similaires, tels que « comment savoir si le système fonctionne, comment savoir ce que je peux faire, et comment savoir si elle compris ce que je viens de faire ? »</span><span class="sxs-lookup"><span data-stu-id="f713a-171">We often see new users as similar questions, such as "how do I know the system is working, how do I know what I can do, and how do I know if it understood what I just did?"</span></span>

<br>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="f713a-172"><strong>Modèle</strong></span><span class="sxs-lookup"><span data-stu-id="f713a-172"><strong>Model</strong></span></span></td>
        <td><span data-ttu-id="f713a-173"><strong>Comment savoir qu’il fonctionne ?</strong></span><span class="sxs-lookup"><span data-stu-id="f713a-173"><strong>How do I know it's working?</strong></span></span></td>
        <td><span data-ttu-id="f713a-174"><strong>Comment savoir que puis-je faire ?</strong></span><span class="sxs-lookup"><span data-stu-id="f713a-174"><strong>How do I know what I can do?</strong></span></span></td>
        <td><span data-ttu-id="f713a-175"><strong>Comment savoir ce que je viens de faire ?</strong></span><span class="sxs-lookup"><span data-stu-id="f713a-175"><strong>How do I know what I just did?</strong></span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f713a-176"><a href="hands-and-tools.md">Mains et outils</a></span><span class="sxs-lookup"><span data-stu-id="f713a-176"><a href="hands-and-tools.md">Hands and tools</a></span></span></td>
        <td><span data-ttu-id="f713a-177">Je vois une main de maillage, je vois un intuitif du bout des doigts ou une main / contrôleur de rayons.</span><span class="sxs-lookup"><span data-stu-id="f713a-177">I see a hand mesh, I see a fingertip affordance or hand/ controller rays.</span></span></td>
        <td><span data-ttu-id="f713a-178">Je vois des handles grabbable ou un rectangle englobant s’affichent lorsque ma main est proche.</span><span class="sxs-lookup"><span data-stu-id="f713a-178">I see grabbable handles or a bounding box appear when my hand is near.</span></span></td>
        <td><span data-ttu-id="f713a-179">J’ai entendre des tonalités sonores et voir les animations sur la manipulation et la mise en production.</span><span class="sxs-lookup"><span data-stu-id="f713a-179">I hear audible tones and see animations on grab and release.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f713a-180"><a href="gaze-and-commit.md">Pointer du regard vers l’avant et valider</a></span><span class="sxs-lookup"><span data-stu-id="f713a-180"><a href="gaze-and-commit.md">Head-gaze and commit</a></span></span></td>
        <td><span data-ttu-id="f713a-181">Je vois un curseur dans le centre de mon champ de vision.</span><span class="sxs-lookup"><span data-stu-id="f713a-181">I see a cursor in the center of my field of view.</span></span></td>
        <td><span data-ttu-id="f713a-182">Le curseur du pointage de regard modifie l’état lorsque sur certains objets.</span><span class="sxs-lookup"><span data-stu-id="f713a-182">The gaze cursor changes state when over certain objects.</span></span></td>
        <td><span data-ttu-id="f713a-183">J’ai consultez / entendre les confirmations et sonores quand prendre des mesures.</span><span class="sxs-lookup"><span data-stu-id="f713a-183">I see/ hear visual and audible confirmations when I take action.</span></span></td>
    </tr>   
    <tr>
        <td><span data-ttu-id="f713a-184"><a href="hands-free.md">Mains libres (regards et durée d’affichage)</a></span><span class="sxs-lookup"><span data-stu-id="f713a-184"><a href="hands-free.md">Hands-free (Gaze and dwell)</a></span></span></td>
        <td><span data-ttu-id="f713a-185">Je vois un curseur dans le centre de mon champ de vision.</span><span class="sxs-lookup"><span data-stu-id="f713a-185">I see a cursor in the center of my field of view.</span></span></td>
        <td><span data-ttu-id="f713a-186">Je vois un indicateur de progression lorsque je m’attarderai pas sur un objet sur.</span><span class="sxs-lookup"><span data-stu-id="f713a-186">I see a progress indicator when I dwell on an interactable object.</span></span></td>
        <td><span data-ttu-id="f713a-187">J’ai consultez / entendre les confirmations et sonores quand prendre des mesures.</span><span class="sxs-lookup"><span data-stu-id="f713a-187">I see/ hear visual and audible confirmations when I take action.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="f713a-188"><a href="hands-free.md">Mains libres (exécution des commandes vocales)</a></span><span class="sxs-lookup"><span data-stu-id="f713a-188"><a href="hands-free.md">Hands-free (Voice commanding)</a></span></span></td>
        <td><span data-ttu-id="f713a-189">Je vois un indicateur à l’écoute et sous-titres codés qui montrent ce que le système entendu parler.</span><span class="sxs-lookup"><span data-stu-id="f713a-189">I see a listening indicator and captions that show what the system heard.</span></span></td>
        <td><span data-ttu-id="f713a-190">J’obtiens des indicateurs et des invites vocales.</span><span class="sxs-lookup"><span data-stu-id="f713a-190">I get voice prompts and hints.</span></span>  <span data-ttu-id="f713a-191">Lorsque je dis « que puis-je dire ? »</span><span class="sxs-lookup"><span data-stu-id="f713a-191">When I say "what can I say?"</span></span> <span data-ttu-id="f713a-192">Je vois des commentaires.</span><span class="sxs-lookup"><span data-stu-id="f713a-192">I see feedback.</span></span></td>
        <td><span data-ttu-id="f713a-193">J’ai consultez / entendre les confirmations et sonores lorsque j’ai une commande ou obtenir de levée d’ambiguïté l’expérience utilisateur si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f713a-193">I see/ hear visual and audible confirmations when I give a command, or get disambiguation UX when needed.</span></span></a></td>
    </tr>
</table>

### <a name="below-are-the-questions-that-weve-found-help-teams-select-an-interaction-model"></a><span data-ttu-id="f713a-194">Voici les questions que nous avons constaté aide les équipes sélectionnez un modèle d’interaction :</span><span class="sxs-lookup"><span data-stu-id="f713a-194">Below are the questions that we've found help teams select an interaction model:</span></span>
 
1.  <span data-ttu-id="f713a-195">Q :  Mes utilisateurs voulez-vous touch hologrammes et effectuer des manipulations de précision HOLOGRAPHIQUE ?</span><span class="sxs-lookup"><span data-stu-id="f713a-195">Q:  Do my users want to touch holograms and perform precision holographic manipulations?</span></span>
<span data-ttu-id="f713a-196">R :  Dans ce cas, consultez le modèle d’interaction des mains et pour le ciblage de précision et de manipulation avec mains ou contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="f713a-196">A:  If so, check out the Hands and Tools interaction model for precision targeting and manipulation with hands or motion controllers.</span></span>
 
2.  <span data-ttu-id="f713a-197">Q :  Mes utilisateurs doivent-ils conserver leurs mains gratuits pour les tâches réelles ?</span><span class="sxs-lookup"><span data-stu-id="f713a-197">Q:  Do my users need to keep their hands free, for real-world tasks?</span></span>
<span data-ttu-id="f713a-198">R :  Dans ce cas, examinons le modèle d’interaction mains-libres, qui fournit une excellente expérience mains libres par le biais du pointage de regard et vocale basée sur les interactions.</span><span class="sxs-lookup"><span data-stu-id="f713a-198">A:  If so, take a look at the Hands-Free interaction model, which provides a great hands-free experience through gaze- and voice-based interactions.</span></span>
 
3.  <span data-ttu-id="f713a-199">Q :  Mes utilisateurs doivent-ils disposer les temps d’apprendre les interactions pour mon application de réalité mixte, ou doivent-elles les interactions avec la courbe d’apprentissage la plus basse possible ?</span><span class="sxs-lookup"><span data-stu-id="f713a-199">Q:  Do my users have time to learn interactions for my mixed reality application, or do they need the interactions with the lowest learning curve possible?</span></span>
<span data-ttu-id="f713a-200">R :  Nous recommandons le modèle des mains et pour la courbe d’apprentissage la plus faible et des interactions plus intuitives, tant que les utilisateurs sont en mesure d’utiliser leurs mains pour l’interaction.</span><span class="sxs-lookup"><span data-stu-id="f713a-200">A:  We recommend the Hands and Tools model for the lowest learning curve and most intuitive interactions, as long as users are able to use their hands for interaction.</span></span>
 
4.  <span data-ttu-id="f713a-201">Q :  Mes utilisateurs utilisent des contrôleurs de mouvement pour pointant et manipulation ?</span><span class="sxs-lookup"><span data-stu-id="f713a-201">Q:  Do my users use motion controllers for pointing and manipulation?</span></span>
<span data-ttu-id="f713a-202">R :  Le modèle de mains et inclut tous les conseils pour une bonne expérience des contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="f713a-202">A:  The Hands and Tools model includes all guidance for a great experience with motion controllers.</span></span>
 
5.  <span data-ttu-id="f713a-203">Q :  Mes utilisateurs utilisent-elles un contrôleur d’accessibilité ou un contrôleur Bluetooth courantes, comme un clicker ?</span><span class="sxs-lookup"><span data-stu-id="f713a-203">Q:  Do my users use an accessibility controller or a common Bluetooth controller, such as a clicker?</span></span>
<span data-ttu-id="f713a-204">R :  Nous recommandons le modèle regards de tête et de validation pour tous les contrôleurs non suivies.</span><span class="sxs-lookup"><span data-stu-id="f713a-204">A:  We recommend the Head-gaze and commit model for all non-tracked controllers.</span></span>  <span data-ttu-id="f713a-205">Il est conçu pour autoriser un utilisateur à parcourir une expérience entière avec une simple garagiste « cible et validation ».</span><span class="sxs-lookup"><span data-stu-id="f713a-205">It's designed to allow a user to traverse an entire experience with a simple "target and commit" mechanic.</span></span> 
 
6.  <span data-ttu-id="f713a-206">Q : Mes utilisateurs uniquement la progression via une expérience cliquant « via » (par exemple dans un environnement semblable à diaporama 3d), par opposition à la navigation dans les dispositions denses de contrôles d’interface utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="f713a-206">Q: Do my users only progress through an experience by "clicking through" (for example in a 3d slideshow-like environment), as opposed to navigating dense layouts of UI controls?</span></span>
<span data-ttu-id="f713a-207">R :  Si les utilisateurs n’ont pas besoin de contrôler un grand nombre de l’interface utilisateur, Head-regards et validation offre une option de demande où les utilisateurs n’ont pas à vous soucier de ciblage.</span><span class="sxs-lookup"><span data-stu-id="f713a-207">A:  If users do not need to control a lot of UI, Head-gaze and commit offers a learnable option where users do not have to worry about targeting.</span></span> 
 
7.  <span data-ttu-id="f713a-208">Q :  Mes utilisateurs utilisent-ils les deux HoloLens (1er gen) et HoloLens 2 / A: Immersive de Windows (casques VR)  Dans la mesure où les regards de tête et de validation est le modèle d’interaction pour HoloLens (1er gen), nous vous recommandons créateurs qui prennent en charge de HoloLens (1er gen) utiliser regards de tête et de validation pour les fonctionnalités ou les modes d’utilisateurs peut se produire sur un HoloLens (1er gen) casque.</span><span class="sxs-lookup"><span data-stu-id="f713a-208">Q:  Do my users use both HoloLens (1st gen) and HoloLens 2/ Windows Immersive (VR headsets) A:  Since Head-gaze and commit is the interaction model for HoloLens (1st gen), we recommend that creators who support HoloLens (1st gen) use Head-gaze and commit for any features or modes that users may experience on a HoloLens (1st gen) headset.</span></span>  <span data-ttu-id="f713a-209">Consultez la section suivante ci-dessous sur *transition des modèles d’interaction* pour plus d’informations sur la création d’une expérience optimale pour plusieurs générations de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="f713a-209">Please see the next section below on *Transitioning interaction models* for details on making a great experience for multiple HoloLens generations.</span></span>
 
8.  <span data-ttu-id="f713a-210">Q : Qu’en est-il pour les utilisateurs qui sont généralement mobiles (couvrant un large espace ou de déplacement entre des espaces), et les utilisateurs qui ont tendance à fonctionner dans un seul espace ?</span><span class="sxs-lookup"><span data-stu-id="f713a-210">Q: What about for users who are generally mobile (covering a large space or moving between spaces), versus users who tend to work in a single space?</span></span>  
<span data-ttu-id="f713a-211">R :  Les modèles d’interaction de fonctionnera pour ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f713a-211">A:  Any of the interaction models will work for these users.</span></span>  

> [!NOTE]
> <span data-ttu-id="f713a-212">Obtenir des instructions spécifiques à la conception d’applications [bientôt](index.md#news-and-notes).</span><span class="sxs-lookup"><span data-stu-id="f713a-212">More guidance specific to app design [coming soon](index.md#news-and-notes).</span></span>


## <a name="transition-interaction-models"></a><span data-ttu-id="f713a-213">Modèles d’interaction de transition</span><span class="sxs-lookup"><span data-stu-id="f713a-213">Transition interaction models</span></span>
<span data-ttu-id="f713a-214">Il existe également des cas où vos cas d’usage peuvent nécessiter qu’utilisant plus d’un modèle d’interaction.</span><span class="sxs-lookup"><span data-stu-id="f713a-214">There are also cases where your use cases may require that utilizing more than one interaction model.</span></span>  <span data-ttu-id="f713a-215">Par exemple, votre flux d’application « création » utilise le modèle d’interaction des mains et, mais que vous souhaitez employer un mode mains libres pour les techniciens du terrain.</span><span class="sxs-lookup"><span data-stu-id="f713a-215">For example, your app's "creation flow" utilizes the Hands and tools interaction model, but you want to employ a Hands-free mode for field technicians.</span></span>  

<span data-ttu-id="f713a-216">Si votre expérience requiert plusieurs modèles d’interaction, nous avons constaté que nombreux utilisateurs finaux peuvent rencontrer des difficultés de transition d’un modèle à un autre, en particulier les utilisateurs finaux qui débutent avec MR.</span><span class="sxs-lookup"><span data-stu-id="f713a-216">If your experience does require multiple interaction models, we've found that many end users may encounter difficulty transitioning from one model to another -- especially end users who are new to MR.</span></span>

> [!Note]
> <span data-ttu-id="f713a-217">Pour aider les concepteurs de guide et les développeurs à travers les choix qui peut s’avérer difficile dans MR, nous travaillons sur plus de conseils pour l’utilisation de plusieurs modèles d’interaction.</span><span class="sxs-lookup"><span data-stu-id="f713a-217">To help guide designers and developers through choices that can be difficult in MR, we're working on more guidance for using multiple interaction models.</span></span>
 

## <a name="see-also"></a><span data-ttu-id="f713a-218">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f713a-218">See also</span></span>
* [<span data-ttu-id="f713a-219">Pointer du regard vers l’avant et valider</span><span class="sxs-lookup"><span data-stu-id="f713a-219">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="f713a-220">Manipulation directe</span><span class="sxs-lookup"><span data-stu-id="f713a-220">Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="f713a-221">Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="f713a-221">Point and commit</span></span>](point-and-commit.md)
* [<span data-ttu-id="f713a-222">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="f713a-222">Gaze targeting</span></span>](gaze-targeting.md)
* [<span data-ttu-id="f713a-223">Mouvements</span><span class="sxs-lookup"><span data-stu-id="f713a-223">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="f713a-224">Conception de la voix</span><span class="sxs-lookup"><span data-stu-id="f713a-224">Voice design</span></span>](voice-design.md)
* [<span data-ttu-id="f713a-225">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="f713a-225">Motion controllers</span></span>](motion-controllers.md)
* [<span data-ttu-id="f713a-226">Conception du son spatial</span><span class="sxs-lookup"><span data-stu-id="f713a-226">Spatial sound design</span></span>](spatial-sound-design.md)
* [<span data-ttu-id="f713a-227">Conception du mappage spatial</span><span class="sxs-lookup"><span data-stu-id="f713a-227">Spatial mapping design</span></span>](spatial-mapping-design.md)
* [<span data-ttu-id="f713a-228">Confort</span><span class="sxs-lookup"><span data-stu-id="f713a-228">Comfort</span></span>](comfort.md)
