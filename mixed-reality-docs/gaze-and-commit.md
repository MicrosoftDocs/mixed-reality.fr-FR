---
title: Point de regard et validation
description: Vue d’ensemble générale du modèle d’entrée « point d’entrée et de validation », à l’aide d’une entrée d’œil ou de tête.
author: sostel
ms.author: sostel
ms.date: 10/31/2019
ms.topic: article
keywords: La réalité mixte, le point de présence, le regard, l’interaction, la conception, le suivi des yeux, le suivi des têtes
ms.openlocfilehash: df152f6a3a6e4ae2d6c32a0c56fbb615bcfa7aa8
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375846"
---
# <a name="gaze-and-commit"></a><span data-ttu-id="c8460-104">Point de regard et validation</span><span class="sxs-lookup"><span data-stu-id="c8460-104">Gaze and commit</span></span>

<span data-ttu-id="c8460-105">Le point de _regard et la validation_ est un modèle d’entrée fondamental étroitement lié à la façon dont nous interagissons avec nos ordinateurs à l’aide de la souris : _point & cliquez_.</span><span class="sxs-lookup"><span data-stu-id="c8460-105">_Gaze and commit_ is a fundamental input model that is closely related with the way we're interacting with our computers using the mouse: _Point & click_.</span></span>
<span data-ttu-id="c8460-106">Sur cette page, nous présentons deux types d’entrées de regard (pointer et Eye-regard) et différents types d’actions de validation.</span><span class="sxs-lookup"><span data-stu-id="c8460-106">On this page, we introduce two types of gaze input (head- and eye-gaze) and different types of commit actions.</span></span> 
<span data-ttu-id="c8460-107">Le point de _regard et la validation_ sont considérés comme un modèle d’entrée lointain avec manipulation indirecte.</span><span class="sxs-lookup"><span data-stu-id="c8460-107">_Gaze and commit_ is considered a far input model with indirect manipulation.</span></span>
<span data-ttu-id="c8460-108">Cela signifie qu’il est préférable d’utiliser le contenu holographique qui est hors de portée.</span><span class="sxs-lookup"><span data-stu-id="c8460-108">This means it is best used for interacting with holographic content that is out of reach.</span></span>

<span data-ttu-id="c8460-109">Les casques de réalité mixte peuvent utiliser la position et l’orientation de la tête de l’utilisateur pour déterminer le vecteur de direction de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="c8460-109">Mixed reality headsets can use the position and orientation of the user's head to determine their head direction vector.</span></span> <span data-ttu-id="c8460-110">Vous pouvez l’assimiler à un rayon laser qui prend son origine entre les yeux de l’utilisateur et pointe droit devant.</span><span class="sxs-lookup"><span data-stu-id="c8460-110">You can think of this as a laser that points straight ahead from directly between the user's eyes.</span></span> <span data-ttu-id="c8460-111">C’est une approximation assez grossière de la zone vers laquelle se porte le regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8460-111">This is a fairly coarse approximation of where the user is looking.</span></span> <span data-ttu-id="c8460-112">Votre application peut croiser ce rayon avec des objets virtuels ou réels, et dessiner un curseur à cet emplacement pour permettre à l’utilisateur de savoir ce qu’il cible actuellement.</span><span class="sxs-lookup"><span data-stu-id="c8460-112">Your application can intersect this ray with virtual or real-world objects, and draw a cursor at that location to let the user know what they are currently targeting.</span></span>

<span data-ttu-id="c8460-113">En plus de la tête de regard, certains casques de réalité mixte, tels que HoloLens 2, incluent des systèmes de suivi oculaire qui produisent un vecteur point-Orient.</span><span class="sxs-lookup"><span data-stu-id="c8460-113">In addition to head gaze, some mixed reality headsets, such as HoloLens 2, include eye tracking systems that produce an eye-gaze vector.</span></span> <span data-ttu-id="c8460-114">Ces dispositifs fournissent une mesure précise de la zone vers laquelle se porte le regard de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8460-114">This provides a fine-grained measurement of where the user is looking.</span></span> <span data-ttu-id="c8460-115">Dans les deux cas, le point de regard représente un signal important pour l’intention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8460-115">In both cases, the gaze represents an important signal for the user's intent.</span></span> <span data-ttu-id="c8460-116">Mieux le système peut interpréter et prédire les actions prévues de l’utilisateur, l’augmentation de la satisfaction des utilisateurs et l’amélioration des performances.</span><span class="sxs-lookup"><span data-stu-id="c8460-116">The better the system can interpret and predict the user's intended actions, user satisfaction increases and performance improves.</span></span>

<span data-ttu-id="c8460-117">Voici quelques exemples de la façon dont vous êtes un développeur de réalité mixte qui peut tirer parti de la tête ou du regard :</span><span class="sxs-lookup"><span data-stu-id="c8460-117">Below are a few examples for how you as a mixed reality developer can benefit from head- or eye-gaze:</span></span>
* <span data-ttu-id="c8460-118">Votre application peut faire une intersection avec le regard des hologrammes dans votre scène pour déterminer où l’attention de l’utilisateur est (plus précise avec le regard de l’oeil).</span><span class="sxs-lookup"><span data-stu-id="c8460-118">Your app can intersect gaze with the holograms in your scene to determine where the user's attention is (more precise with eye-gaze).</span></span>
* <span data-ttu-id="c8460-119">Votre application peut canaliser les gestes et les presses des contrôleurs en fonction du point de regard de l’utilisateur, ce qui permet à l’utilisateur de sélectionner, d’activer, de saisir, de faire défiler ou d’interagir de manière transparente avec ses hologrammes.</span><span class="sxs-lookup"><span data-stu-id="c8460-119">Your app can channel gestures and controller presses based on the user's gaze, letting the user seamlessly select, activate, grab, scroll, or otherwise interact with their holograms.</span></span>
* <span data-ttu-id="c8460-120">Votre application peut permettre à l’utilisateur de placer des hologrammes sur des surfaces réelles en croisant leur rayon de regard avec le maillage de mappage spatial.</span><span class="sxs-lookup"><span data-stu-id="c8460-120">Your app can let the user place holograms on real-world surfaces by intersecting their gaze ray with the spatial mapping mesh.</span></span>
* <span data-ttu-id="c8460-121">Votre application peut savoir quand l’utilisateur *ne cherche pas* dans la direction d’un objet important, ce qui peut amener votre application à donner des signaux visuels et audio pour tourner vers cet objet.</span><span class="sxs-lookup"><span data-stu-id="c8460-121">Your app can know when the user is *not* looking in the direction of an important object, which can lead your app to give visual and audio cues to turn towards that object.</span></span>

<br>


## <a name="device-support"></a><span data-ttu-id="c8460-122">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="c8460-122">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="c8460-123"><strong>Modèle d’entrée</strong></span><span class="sxs-lookup"><span data-stu-id="c8460-123"><strong>Input model</strong></span></span></td>
        <td><span data-ttu-id="c8460-124"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="c8460-124"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="c8460-125"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="c8460-125"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="c8460-126"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="c8460-126"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="c8460-127">Suivre de la tête et valider</span><span class="sxs-lookup"><span data-stu-id="c8460-127">Head-gaze and commit</span></span></td>
        <td><span data-ttu-id="c8460-128">✔️ Recommandé</span><span class="sxs-lookup"><span data-stu-id="c8460-128">✔️ Recommended</span></span></td>
        <td><span data-ttu-id="c8460-129">✔️ Recommandé (troisième choix ; <a href="interaction-fundamentals.md">voir les autres options</a>)</span><span class="sxs-lookup"><span data-stu-id="c8460-129">✔️ Recommended (third choice - <a href="interaction-fundamentals.md">See the other options</a>)</span></span></td>
        <td><span data-ttu-id="c8460-130">➕ Autre option</span><span class="sxs-lookup"><span data-stu-id="c8460-130">➕ Alternate option</span></span></td>
    </tr>
         <tr>
        <td><span data-ttu-id="c8460-131">Suivre du regard et valider</span><span class="sxs-lookup"><span data-stu-id="c8460-131">Eye-gaze and commit</span></span></td>
        <td><span data-ttu-id="c8460-132">❌ non disponible</span><span class="sxs-lookup"><span data-stu-id="c8460-132">❌ Not available</span></span></td>
        <td><span data-ttu-id="c8460-133">✔️ Recommandé (troisième choix ; <a href="interaction-fundamentals.md">voir les autres options</a>)</span><span class="sxs-lookup"><span data-stu-id="c8460-133">✔️ Recommended (third choice - <a href="interaction-fundamentals.md">See the other options</a>)</span></span></td>
        <td><span data-ttu-id="c8460-134">❌ non disponible</span><span class="sxs-lookup"><span data-stu-id="c8460-134">❌ Not available</span></span></td>
    </tr>
</table>


## <a name="gaze"></a><span data-ttu-id="c8460-135">Pointage du regard</span><span class="sxs-lookup"><span data-stu-id="c8460-135">Gaze</span></span>

### <a name="eye--or-head-gaze"></a><span data-ttu-id="c8460-136">Le regard de l’œil ou de la tête ?</span><span class="sxs-lookup"><span data-stu-id="c8460-136">Eye- or head-gaze?</span></span>
<span data-ttu-id="c8460-137">Il y a plusieurs points à prendre en compte lorsque vous êtes confronté à la question de savoir si vous devez utiliser le modèle d’entrée « Eye-regard and Commit » ou « Head-Pointing and commit ».</span><span class="sxs-lookup"><span data-stu-id="c8460-137">There are several considerations to take into account when faced with the question whether you should use the "eye-gaze and commit" or "head-gaze and commit" input model.</span></span> <span data-ttu-id="c8460-138">Si vous développez pour un casque immersif ou pour HoloLens (1re génération), le choix est simple : début et validation.</span><span class="sxs-lookup"><span data-stu-id="c8460-138">If you're developing for an immersive headset or for HoloLens (1st gen) then the choice is simple: Head-gaze and commit.</span></span> <span data-ttu-id="c8460-139">Si vous développez pour HoloLens 2, le choix devient un peu plus difficile, c’est pourquoi il est important de comprendre les avantages et les défis inhérents à chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="c8460-139">If you're developing for HoloLens 2, the choice becomes a little harder which is why it's important to understand the advantages and challenges that come with each of them.</span></span>
<span data-ttu-id="c8460-140">Nous avons compilé un grand nombre de professionnels et de conversions dans le tableau ci-dessous pour contraster en tête et en regard.</span><span class="sxs-lookup"><span data-stu-id="c8460-140">We compiled some broad pro's and con's in the table below to contrast head- vs. eye-gaze targeting.</span></span> <span data-ttu-id="c8460-141">Ceci est loin d’être terminé et nous vous suggérons d’en apprendre davantage sur le ciblage des regards dans la réalité mixte ici :</span><span class="sxs-lookup"><span data-stu-id="c8460-141">This is far from complete and we suggest learning more about eye-gaze targeting in mixed reality here:</span></span>
* <span data-ttu-id="c8460-142">[Suivi oculaire sur hololens 2](eye-tracking.md): présentation générale de notre nouvelle fonctionnalité de suivi oculaire sur hololens 2, avec quelques conseils pour les développeurs.</span><span class="sxs-lookup"><span data-stu-id="c8460-142">[Eye tracking on HoloLens 2](eye-tracking.md): General introduction of our new eye tracking capability on HoloLens 2 including some developer guidance.</span></span> 
* <span data-ttu-id="c8460-143">[Œil-regard](eye-gaze-interaction.md): considérations de conception et recommandations lors de la planification de l’utilisation du suivi oculaire comme entrée.</span><span class="sxs-lookup"><span data-stu-id="c8460-143">[Eye-gaze interaction](eye-gaze-interaction.md): Design considerations and recommendations when planning to use eye tracking as an input.</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
   <tr>
        <td><span data-ttu-id="c8460-144"><strong>Regard sur les yeux</strong></span><span class="sxs-lookup"><span data-stu-id="c8460-144"><strong>Eye-gaze targeting</strong></span></span></td>
        <td><span data-ttu-id="c8460-145"><strong>Cible du regard</strong></span><span class="sxs-lookup"><span data-stu-id="c8460-145"><strong>Head-gaze targeting</strong></span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="c8460-146">Expédition!</span><span class="sxs-lookup"><span data-stu-id="c8460-146">Fast!</span></span></td>
        <td><span data-ttu-id="c8460-147">Élevé</span><span class="sxs-lookup"><span data-stu-id="c8460-147">Slower</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="c8460-148">Faible effort (à peine les mouvements de corps nécessaires)</span><span class="sxs-lookup"><span data-stu-id="c8460-148">Low effort (barely any body movements necessary)</span></span></td>
        <td><span data-ttu-id="c8460-149">Peut être fatiguing-une gêne possible (par exemple, une fatigue du cou)</span><span class="sxs-lookup"><span data-stu-id="c8460-149">Can be fatiguing - Possible discomfort (e.g., neck strain)</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="c8460-150">Ne nécessite pas de curseur, mais les commentaires subtils sont recommandés</span><span class="sxs-lookup"><span data-stu-id="c8460-150">Does not require a cursor, but subtle feedback is recommended</span></span></td>
        <td><span data-ttu-id="c8460-151">Requiert l’affichage d’un curseur</span><span class="sxs-lookup"><span data-stu-id="c8460-151">Requires to show a cursor</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="c8460-152">Aucun mouvement d’œil lisse, par exemple, non adapté au dessin</span><span class="sxs-lookup"><span data-stu-id="c8460-152">No smooth eye movements – e.g., not good for drawing</span></span></td>
        <td><span data-ttu-id="c8460-153">Plus contrôlé et plus explicite</span><span class="sxs-lookup"><span data-stu-id="c8460-153">More controlled and explicit</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="c8460-154">Difficile pour les très petites cibles (par exemple, des boutons minuscules ou des liens weblink)</span><span class="sxs-lookup"><span data-stu-id="c8460-154">Difficult for very small targets (e.g., tiny buttons or weblinks)</span></span></td>
        <td><span data-ttu-id="c8460-155">Fidèles!</span><span class="sxs-lookup"><span data-stu-id="c8460-155">Reliable!</span></span> <span data-ttu-id="c8460-156">Parfait !</span><span class="sxs-lookup"><span data-stu-id="c8460-156">Great fallback!</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="c8460-157">...</span><span class="sxs-lookup"><span data-stu-id="c8460-157">...</span></span></td>
        <td><span data-ttu-id="c8460-158">...</span><span class="sxs-lookup"><span data-stu-id="c8460-158">...</span></span></td>
    </tr>
</table>

<span data-ttu-id="c8460-159">Que vous utilisiez le point de regard ou le regard de votre modèle d’entrée de point de présence et de validation, il est fourni avec différents jeux de contraintes de conception, qui seront couverts séparément dans [les Articles de](gaze-and-commit-head.md) [regard et](gaze-and-commit-eyes.md) de validation.</span><span class="sxs-lookup"><span data-stu-id="c8460-159">Whether you use head-gaze or eye-gaze for your gaze-and-commit input model comes with different sets of design constraints, which will be covered separately in the [eye-gaze and commit](gaze-and-commit-eyes.md) and [head-gaze and commit](gaze-and-commit-head.md) articles.</span></span>

<br>

---

### <a name="cursor"></a><span data-ttu-id="c8460-160">Curseur</span><span class="sxs-lookup"><span data-stu-id="c8460-160">Cursor</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="c8460-161">Pour le point de vue de la tête, la plupart des applications doivent utiliser un [curseur](cursors.md) (ou une autre indication d’audit/visuel) pour donner à l’utilisateur la certitude de ce qu’ils sont sur le point d’interagir.</span><span class="sxs-lookup"><span data-stu-id="c8460-161">For head gaze, most apps should use a [cursor](cursors.md) (or other auditory/visual indication) to give the user confidence in what they're about to interact with.</span></span> <span data-ttu-id="c8460-162">En règle générale, vous positionnez ce curseur dans le monde où le rayon de regard de son en-tête croise d’abord un objet, qui peut être un hologramme ou une surface réaliste.</span><span class="sxs-lookup"><span data-stu-id="c8460-162">You typically position this cursor in the world where their head gaze ray first intersects an object, which may be a hologram or a real-world surface.</span></span><br>
        <br>
        <span data-ttu-id="c8460-163">Pour les yeux oculaires, nous vous recommandons généralement de *ne pas* afficher de curseur, car cela peut rapidement devenir gênant et ennuyeux pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8460-163">For eye gaze, we generally recommend *not* to show a cursor, as this can quickly become distracting and annoying for the user.</span></span> <span data-ttu-id="c8460-164">À la place, mettez en surbrillance les cibles visuelles ou utilisez un curseur très pâle pour faire confiance à ce que l’utilisateur est sur le point d’interagir.</span><span class="sxs-lookup"><span data-stu-id="c8460-164">Instead subtly highlight visual targets or use a very faint eye cursor to provide confidence about what the user is about to interact with.</span></span> <span data-ttu-id="c8460-165">Pour plus d’informations, consultez notre [Guide de conception pour une entrée basée](eye-tracking.md) sur l’œil sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="c8460-165">For more information, please check out our [design guidance for eye-based input](eye-tracking.md) on HoloLens 2.</span></span>
    :::column-end:::
        :::column:::
       <span data-ttu-id="c8460-166">![un exemple de curseur visuel pour afficher le regard](images/cursor.jpg)</span><span class="sxs-lookup"><span data-stu-id="c8460-166">![An example visual cursor to show gaze](images/cursor.jpg)</span></span><br>
       <span data-ttu-id="c8460-167">*Image : un exemple de curseur visuel pour afficher le regard*</span><span class="sxs-lookup"><span data-stu-id="c8460-167">*Image: An example visual cursor to show gaze*</span></span>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="commit"></a><span data-ttu-id="c8460-168">Validation</span><span class="sxs-lookup"><span data-stu-id="c8460-168">Commit</span></span>
<span data-ttu-id="c8460-169">Après avoir parlé des différentes façons de pointer vers une cible, nous _allons en parler_ plus sur la partie _validation_ dans le point de vue _et la validation_.</span><span class="sxs-lookup"><span data-stu-id="c8460-169">After talking about different ways to _gaze_ at a target, let's talk a bit more about the _commit_ part in _gaze and commit_.</span></span>
<span data-ttu-id="c8460-170">Après avoir ciblé un objet ou un élément d’interface utilisateur, l’utilisateur peut interagir ou cliquer dessus à l’aide d’une entrée secondaire.</span><span class="sxs-lookup"><span data-stu-id="c8460-170">After targeting an object or UI element, the user can interact or click on it using a secondary input.</span></span> <span data-ttu-id="c8460-171">C’est ce que l’on appelle l’étape de validation du modèle d’entrée.</span><span class="sxs-lookup"><span data-stu-id="c8460-171">This is known as the commit step of the input model.</span></span> 

<span data-ttu-id="c8460-172">Les méthodes de validation suivantes sont prises en charge :</span><span class="sxs-lookup"><span data-stu-id="c8460-172">The following commit methods are supported:</span></span>
- <span data-ttu-id="c8460-173">Mouvement d’appui sur la main (par exemple, augmentez votre main en avant et regroupez le doigt et le curseur de votre index)</span><span class="sxs-lookup"><span data-stu-id="c8460-173">Air tap hand gesture (i.e., raise your hand in front of you and bring together your index finger and thumb)</span></span>
- <span data-ttu-id="c8460-174">Dites _« Sélectionner »_ ou l’une des commandes vocales ciblées</span><span class="sxs-lookup"><span data-stu-id="c8460-174">Say _"select"_ or one of the targeted voice commands</span></span>
- <span data-ttu-id="c8460-175">Appuyer sur un bouton unique sur un [Clicker HoloLens](hardware-accessories.md#hololens-clicker)</span><span class="sxs-lookup"><span data-stu-id="c8460-175">Press a single button on a [HoloLens Clicker](hardware-accessories.md#hololens-clicker)</span></span>
- <span data-ttu-id="c8460-176">Appuyez sur le bouton « A » sur un boîtier de manette Xbox</span><span class="sxs-lookup"><span data-stu-id="c8460-176">Press the 'A' button on an Xbox gamepad</span></span>
- <span data-ttu-id="c8460-177">Appuyez sur le bouton « A » sur un contrôleur d’adaptateur Xbox</span><span class="sxs-lookup"><span data-stu-id="c8460-177">Press the 'A' button on an Xbox adaptive controller</span></span>

### <a name="gaze-and-air-tap-gesture"></a><span data-ttu-id="c8460-178">Mouvement du toucher et de l’air</span><span class="sxs-lookup"><span data-stu-id="c8460-178">Gaze and air tap gesture</span></span>
<span data-ttu-id="c8460-179">Le clic aérien est une action d’appui avec la main levée.</span><span class="sxs-lookup"><span data-stu-id="c8460-179">Air tap is a tapping gesture with the hand held upright.</span></span> <span data-ttu-id="c8460-180">Pour effectuer un TAP Air, soulevez le doigt de votre index jusqu’à la position prête, puis pincez-le avec votre curseur et augmentez la sauvegarde du doigt de l’index jusqu’à la version finale.</span><span class="sxs-lookup"><span data-stu-id="c8460-180">To perform an air tap, raise your index finger to the ready position, then pinch with your thumb, and raise your index finger back up to release.</span></span> <span data-ttu-id="c8460-181">Sur HoloLens (1ère génération), le robinet air est l’entrée secondaire la plus courante.</span><span class="sxs-lookup"><span data-stu-id="c8460-181">On HoloLens (1st gen), air tap is the most common secondary input.</span></span>


:::row:::
    :::column:::
       <span data-ttu-id="c8460-182">![doigt en position prête](images/readyandpress-ready.jpg)</span><span class="sxs-lookup"><span data-stu-id="c8460-182">![Finger in the ready position](images/readyandpress-ready.jpg)</span></span><br>
       <span data-ttu-id="c8460-183">**Doigt en position prête**</span><span class="sxs-lookup"><span data-stu-id="c8460-183">**Finger in the ready position**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="c8460-184">![Appuyez sur le doigt pour appuyer ou sur](images/readyandpress-press.jpg)</span><span class="sxs-lookup"><span data-stu-id="c8460-184">![Press finger down to tap or click](images/readyandpress-press.jpg)</span></span><br>
        <span data-ttu-id="c8460-185">**Appuyez sur le doigt pour appuyer ou sur**</span><span class="sxs-lookup"><span data-stu-id="c8460-185">**Press finger down to tap or click**</span></span><br>
    :::column-end:::
:::row-end:::


<span data-ttu-id="c8460-186">Le TAP Air est également disponible sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="c8460-186">Air tap is also available on HoloLens 2.</span></span> <span data-ttu-id="c8460-187">Elle a été allégée de la version d’origine.</span><span class="sxs-lookup"><span data-stu-id="c8460-187">It has been relaxed from the original version.</span></span> <span data-ttu-id="c8460-188">Presque tous les types de pincements sont maintenant pris en charge tant que la main est debout et qu’elles sont conservées.</span><span class="sxs-lookup"><span data-stu-id="c8460-188">Nearly all types of pinches are now supported as long as the hand is upright and holding still.</span></span> <span data-ttu-id="c8460-189">Ainsi, les utilisateurs peuvent apprendre et effectuer le mouvement beaucoup plus facilement.</span><span class="sxs-lookup"><span data-stu-id="c8460-189">This makes it much easier for users to learn and perform the gesture.</span></span> <span data-ttu-id="c8460-190">Ce nouveau robinet d’air remplace l’ancien par la même API. par conséquent, les applications existantes auront le nouveau comportement automatiquement après la recompilation pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="c8460-190">This new air tap replaces the old one through the same API, so existing applications will have the new behavior automatically after recompiling for HoloLens 2.</span></span>

<br>

---

### <a name="gaze-and-select-voice-command"></a><span data-ttu-id="c8460-191">Commande vocale en regard de « sélectionner »</span><span class="sxs-lookup"><span data-stu-id="c8460-191">Gaze and "Select" voice command</span></span>
<span data-ttu-id="c8460-192">Les commandes vocales sont l’une des principales méthodes d’interaction dans la réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="c8460-192">Voice commanding is one of the primary interaction methods in mixed reality.</span></span> <span data-ttu-id="c8460-193">Il fournit un mécanisme pratique et gratuit pour contrôler le système.</span><span class="sxs-lookup"><span data-stu-id="c8460-193">It provides a very powerful hands-free mechanism to control the system.</span></span> <span data-ttu-id="c8460-194">Il existe différents types de modèles d’interactions vocales :</span><span class="sxs-lookup"><span data-stu-id="c8460-194">There are different types of voice interaction models:</span></span>

- <span data-ttu-id="c8460-195">Commande « SELECT » générique qui effectue une activation de clic ou une validation en tant qu’entrée secondaire.</span><span class="sxs-lookup"><span data-stu-id="c8460-195">The generic "Select" command that performs a click actuation or commit as a secondary input.</span></span>
- <span data-ttu-id="c8460-196">Les commandes d’objet (par exemple, « fermer » ou « agrandir ») effectuent et valident une action en tant qu’entrée secondaire.</span><span class="sxs-lookup"><span data-stu-id="c8460-196">Object commands (e.g., "Close" or "Make it bigger") perform and commit to an action as a secondary input.</span></span>
- <span data-ttu-id="c8460-197">Les commandes globales (par exemple, « atteindre le début ») ne nécessitent pas de cible.</span><span class="sxs-lookup"><span data-stu-id="c8460-197">Global commands (e.g., "Go to start") don't require a target.</span></span>
- <span data-ttu-id="c8460-198">Les interfaces utilisateur ou les entités de conversation comme Cortana disposent d’une fonctionnalité de langage naturel AI.</span><span class="sxs-lookup"><span data-stu-id="c8460-198">Conversation user interfaces or entities like Cortana have an AI natural language capability.</span></span>
- <span data-ttu-id="c8460-199">Commandes vocales personnalisées</span><span class="sxs-lookup"><span data-stu-id="c8460-199">Custom voice commands</span></span>

<span data-ttu-id="c8460-200">Pour obtenir plus de détails, ainsi qu’une liste complète des commandes vocales disponibles et comment les utiliser, consultez notre guide de [commande vocale](voice-design.md) .</span><span class="sxs-lookup"><span data-stu-id="c8460-200">To find out more details as well as a comprehensive list of available voice commands and how to use them, check out our [voice commanding](voice-design.md) guidance.</span></span>

<br>

---


### <a name="gaze-and-hololens-clicker"></a><span data-ttu-id="c8460-201">Clic de la même façon</span><span class="sxs-lookup"><span data-stu-id="c8460-201">Gaze and HoloLens Clicker</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="c8460-202">L’interutilisateur HoloLens est le premier périphérique périphérique créé spécifiquement pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="c8460-202">The HoloLens Clicker is the first peripheral device built specifically for HoloLens.</span></span> <span data-ttu-id="c8460-203">Elle est incluse dans la version développement de HoloLens (1re génération).</span><span class="sxs-lookup"><span data-stu-id="c8460-203">It is included with HoloLens (1st gen) Development Edition.</span></span> <span data-ttu-id="c8460-204">L’utilisateur de l’un des clickers HoloLens permet à un utilisateur de cliquer avec un mouvement de main minimal et de valider comme entrée secondaire.</span><span class="sxs-lookup"><span data-stu-id="c8460-204">The HoloLens Clicker lets a user click with minimal hand motion, and commit as a secondary input.</span></span> <span data-ttu-id="c8460-205">L’utilisateur de l’un des clickers HoloLens se connecte à HoloLens (1re génération) ou à HoloLens 2 à l’aide de la BTLE (Bluetooth Low Energy).</span><span class="sxs-lookup"><span data-stu-id="c8460-205">The HoloLens Clicker connects to HoloLens (1st gen) or HoloLens 2 using Bluetooth Low Energy (BTLE).</span></span><br>
        <br>
        [<span data-ttu-id="c8460-206">Plus d’informations et d’instructions pour coupler l’appareil</span><span class="sxs-lookup"><span data-stu-id="c8460-206">More information and instructions to pair the device</span></span>](hardware-accessories.md#pairing-bluetooth-accessories)<br>
        <br>
        <span data-ttu-id="c8460-207">*Image : Clicker de HoloLens*</span><span class="sxs-lookup"><span data-stu-id="c8460-207">*Image: HoloLens Clicker*</span></span>
    :::column-end:::
        :::column:::
       ![Clicker de HoloLens](images/hololens-clicker-500px.jpg)<br>
    :::column-end:::
:::row-end:::

<br>

---


### <a name="gaze-and-xbox-wireless-controller"></a><span data-ttu-id="c8460-209">Contrôleur de réseau sans fil en regard</span><span class="sxs-lookup"><span data-stu-id="c8460-209">Gaze and Xbox Wireless Controller</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="c8460-210">Le contrôleur Xbox Wireless effectue une activation de clic comme entrée secondaire à l’aide du bouton « A ».</span><span class="sxs-lookup"><span data-stu-id="c8460-210">The Xbox Wireless Controller performs a click actuation as a secondary input by using the 'A' button.</span></span> <span data-ttu-id="c8460-211">L’appareil est mappé à un ensemble d’actions par défaut qui facilitent la navigation et le contrôle du système.</span><span class="sxs-lookup"><span data-stu-id="c8460-211">The device is mapped to a default set of actions that help navigate and control the system.</span></span> <span data-ttu-id="c8460-212">Si vous souhaitez personnaliser le contrôleur, utilisez l’application Accessoires Xbox pour configurer votre contrôleur Xbox Wireless.</span><span class="sxs-lookup"><span data-stu-id="c8460-212">If you want to customize the controller, use the Xbox Accessories application to configure your Xbox Wireless Controller.</span></span><br>
        <br>
        [<span data-ttu-id="c8460-213">Comment associer un contrôleur Xbox à votre PC</span><span class="sxs-lookup"><span data-stu-id="c8460-213">How to pair an Xbox controller with your PC</span></span>](hardware-accessories.md#pairing-bluetooth-accessories)<br>
        <br>
        <span data-ttu-id="c8460-214">*Image : contrôleur sans fil Xbox*</span><span class="sxs-lookup"><span data-stu-id="c8460-214">*Image: Xbox Wireless Controller*</span></span>
    :::column-end:::
        :::column:::
       ![Contrôleur Xbox Wireless](images/xboxcontroller.jpg)<br>
    :::column-end:::
:::row-end:::



<br>

---


### <a name="gaze-and-xbox-adaptive-controller"></a><span data-ttu-id="c8460-216">Contrôleur adaptatif du point de regard et de Xbox</span><span class="sxs-lookup"><span data-stu-id="c8460-216">Gaze and Xbox Adaptive Controller</span></span>
<span data-ttu-id="c8460-217">Conçu principalement pour répondre aux besoins des joueurs avec une mobilité limitée, le contrôleur d’adaptateur Xbox est un concentrateur unifié pour les appareils qui permet de rendre la réalité mixte plus accessible.</span><span class="sxs-lookup"><span data-stu-id="c8460-217">Designed primarily to meet the needs of gamers with limited mobility, the Xbox Adaptive Controller is a unified hub for devices that helps make mixed reality more accessible.</span></span>

<span data-ttu-id="c8460-218">Le contrôleur d’adaptateur Xbox effectue une action de clic comme entrée secondaire à l’aide du bouton « A ».</span><span class="sxs-lookup"><span data-stu-id="c8460-218">The Xbox Adaptive Controller performs a click actuation as a secondary input by using the 'A' button.</span></span> <span data-ttu-id="c8460-219">L’appareil est mappé à un ensemble d’actions par défaut qui facilitent la navigation et le contrôle du système.</span><span class="sxs-lookup"><span data-stu-id="c8460-219">The device is mapped to a default set of actions that help navigate and control the system.</span></span> <span data-ttu-id="c8460-220">Si vous souhaitez personnaliser le contrôleur, utilisez l’application Accessoires Xbox pour configurer votre contrôleur d’adaptateur Xbox.</span><span class="sxs-lookup"><span data-stu-id="c8460-220">If you want to customize the controller, use the Xbox Accessories application to configure your Xbox Adaptive Controller.</span></span>

<span data-ttu-id="c8460-221">![Manette Xbox Adaptive Controller](images/xbox-adaptive-controller-devices.jpg)</span><span class="sxs-lookup"><span data-stu-id="c8460-221">![Xbox Adaptive Controller](images/xbox-adaptive-controller-devices.jpg)</span></span><br>
<span data-ttu-id="c8460-222">*Manette Xbox Adaptive Controller*</span><span class="sxs-lookup"><span data-stu-id="c8460-222">*Xbox Adaptive Controller*</span></span>

<span data-ttu-id="c8460-223">Connectez des appareils externes, tels que des commutateurs, des boutons, des montages et des joysticks, afin de créer une expérience de contrôleur personnalisée unique.</span><span class="sxs-lookup"><span data-stu-id="c8460-223">Connect external devices such as switches, buttons, mounts, and joysticks to create a custom controller experience that is uniquely yours.</span></span> <span data-ttu-id="c8460-224">Les entrées de bouton, de Stick et de déclencheur sont contrôlées à l’aide d’appareils d’assistance connectés par des connecteurs 3,5 mm et des ports USB.</span><span class="sxs-lookup"><span data-stu-id="c8460-224">Button, thumbstick, and trigger inputs are controlled with assistive devices connected through 3.5mm jacks and USB ports.</span></span>

<span data-ttu-id="c8460-225">![Ports de la manette Xbox Adaptive Controller](images/xbox-adaptive-controller-ports.jpg)</span><span class="sxs-lookup"><span data-stu-id="c8460-225">![Xbox Adaptive Controller ports](images/xbox-adaptive-controller-ports.jpg)</span></span><br>
<span data-ttu-id="c8460-226">*Ports de la manette Xbox Adaptive Controller*</span><span class="sxs-lookup"><span data-stu-id="c8460-226">*Xbox Adaptive Controller ports*</span></span>

[<span data-ttu-id="c8460-227">Instructions pour coupler l’appareil</span><span class="sxs-lookup"><span data-stu-id="c8460-227">Instructions to pair the device</span></span>](hardware-accessories.md#pairing-bluetooth-accessories)

<span data-ttu-id="c8460-228"><a href=https://www.xbox.com/xbox-one/accessories/controllers/xbox-adaptive-controller>Plus d’informations sur le site Xbox</a></span><span class="sxs-lookup"><span data-stu-id="c8460-228"><a href=https://www.xbox.com/xbox-one/accessories/controllers/xbox-adaptive-controller>More info available on the Xbox site</a></span></span>

<br>

---

## <a name="composite-gestures"></a><span data-ttu-id="c8460-229">Mouvements composites</span><span class="sxs-lookup"><span data-stu-id="c8460-229">Composite gestures</span></span>

### <a name="air-tap"></a><span data-ttu-id="c8460-230">Clic aérien</span><span class="sxs-lookup"><span data-stu-id="c8460-230">Air tap</span></span>
<span data-ttu-id="c8460-231">Le mouvement d’appui sur l’air (ainsi que les autres mouvements ci-dessous) réagit uniquement à un TAP spécifique.</span><span class="sxs-lookup"><span data-stu-id="c8460-231">The air tap gesture (as well as the other gestures below) reacts only to a specific tap.</span></span> <span data-ttu-id="c8460-232">Pour détecter d’autres pressions, telles que menu ou saisis, votre application doit utiliser directement les interactions de niveau inférieur décrites dans la section relative aux mouvements de composants clés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c8460-232">To detect other taps, such as Menu or Grasp, your application must directly use the lower-level interactions described in the two key component gestures section above.</span></span>

### <a name="tap-and-hold"></a><span data-ttu-id="c8460-233">Appui de longue durée</span><span class="sxs-lookup"><span data-stu-id="c8460-233">Tap and hold</span></span>
<span data-ttu-id="c8460-234">L’appui prolongé consiste simplement à maintenir la position du doigt vers le bas pendant le clic aérien.</span><span class="sxs-lookup"><span data-stu-id="c8460-234">Hold is simply maintaining the downward finger position of the air tap.</span></span> <span data-ttu-id="c8460-235">La combinaison du robinet et du maintien de l’air permet d’obtenir une série d’interactions plus complexes de type « glisser-déplacer » lorsqu’elles sont combinées à des mouvements ARM tels que la sélection d’un objet au lieu de l’activer ou des interactions secondaires MouseDown, telles que l’émission d’un menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="c8460-235">The combination of air tap and hold allows for a variety of more complex "click and drag" interactions when combined with arm movement such as picking up an object instead of activating it or mousedown secondary interactions such as showing a context menu.</span></span>
<span data-ttu-id="c8460-236">Toutefois, vous devez faire preuve de vigilance lors de la conception de ce mouvement, car l’utilisateur peut être sujet à relâcher ses postures de la main pendant un mouvement étendu.</span><span class="sxs-lookup"><span data-stu-id="c8460-236">Caution should be used when designing for this gesture however, as users can be prone to relaxing their hand postures during the course of any extended gesture.</span></span>

### <a name="manipulation"></a><span data-ttu-id="c8460-237">Manipulation</span><span class="sxs-lookup"><span data-stu-id="c8460-237">Manipulation</span></span>
<span data-ttu-id="c8460-238">Les mouvements de manipulation peuvent être utilisés pour déplacer, redimensionner ou faire pivoter un hologramme lorsque vous souhaitez que l’hologramme réagisse 1:1 aux mouvements manuels de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c8460-238">Manipulation gestures can be used to move, resize, or rotate a hologram when you want the hologram to react 1:1 to the user's hand movements.</span></span> <span data-ttu-id="c8460-239">La possibilité pour l’utilisateur de dessiner ou de peindre dans le monde illustre l’utilisation de ce type de mouvement.</span><span class="sxs-lookup"><span data-stu-id="c8460-239">One use for such 1:1 movements is to let the user draw or paint in the world.</span></span>
<span data-ttu-id="c8460-240">Le ciblage initial pour un mouvement de manipulation doit être effectué au moyen d’un pointage du regard ou d’un pointage.</span><span class="sxs-lookup"><span data-stu-id="c8460-240">The initial targeting for a manipulation gesture should be done by gaze or pointing.</span></span> <span data-ttu-id="c8460-241">Une fois le TAP et le Hold démarré, toute manipulation de l’objet est gérée par des mouvements manuels, ce qui permet à l’utilisateur d’effectuer des recherches lors de la manipulation.</span><span class="sxs-lookup"><span data-stu-id="c8460-241">Once the tap and hold starts, any manipulation of the object is handled by hand movements, freeing the user to look around while they manipulate.</span></span>

### <a name="navigation"></a><span data-ttu-id="c8460-242">Navigation</span><span class="sxs-lookup"><span data-stu-id="c8460-242">Navigation</span></span>
<span data-ttu-id="c8460-243">Les mouvements de navigation fonctionnent comme une manette de jeu virtuelle et peuvent être utilisés pour parcourir des widgets d’interface utilisateur, tels que des menus circulaires.</span><span class="sxs-lookup"><span data-stu-id="c8460-243">Navigation gestures operate like a virtual joystick, and can be used to navigate UI widgets, such as radial menus.</span></span> <span data-ttu-id="c8460-244">Vous appuyez longuement pour démarrer le mouvement, puis déplacez votre main dans un cube 3D normalisé, centré sur l’appui initial.</span><span class="sxs-lookup"><span data-stu-id="c8460-244">You tap and hold to start the gesture and then move your hand within a normalized 3D cube, centered around the initial press.</span></span> <span data-ttu-id="c8460-245">Vous pouvez déplacer votre main sur l’axe des X, Y ou Z à partir d’une valeur comprise entre -1 et 1, 0 étant le point de départ.</span><span class="sxs-lookup"><span data-stu-id="c8460-245">You can move your hand along the X, Y or Z axis from a value of -1 to 1, with 0 being the starting point.</span></span>
<span data-ttu-id="c8460-246">La navigation peut servir à générer des mouvements de zoom ou de défilement continus basés sur la vitesse, à l’image du défilement d’une interface utilisateur 2D que vous pouvez obtenir en cliquant sur le bouton central de la souris, puis en déplaçant le pointeur de la souris vers le haut ou le bas.</span><span class="sxs-lookup"><span data-stu-id="c8460-246">Navigation can be used to build velocity-based continuous scrolling or zooming gestures, similar to scrolling a 2D UI by clicking the middle mouse button and then moving the mouse up and down.</span></span>

<span data-ttu-id="c8460-247">La navigation avec rails fait référence à la possibilité de reconnaître des mouvements dans certains axes jusqu’à ce qu’un certain seuil soit atteint sur cet axe.</span><span class="sxs-lookup"><span data-stu-id="c8460-247">Navigation with rails refers to the ability of recognizing movements in certain axis until a certain threshold is reached on that axis.</span></span> <span data-ttu-id="c8460-248">Cela est utile uniquement lorsque le déplacement dans plus d’un axe est activé dans une application par le développeur, par exemple si une application est configurée pour reconnaître les gestes de navigation sur l’axe des X, Y, mais également dans l’axe des X avec rails.</span><span class="sxs-lookup"><span data-stu-id="c8460-248">This is only useful when movement in more than one axis is enabled in an application by the developer, such as if an application is configured to recognize navigation gestures across X, Y axis but also specified X axis with rails.</span></span> <span data-ttu-id="c8460-249">Dans ce cas, le système reconnaît les mouvements de main sur l’axe des X tant qu’ils restent dans des rails imaginaires (repère) sur l’axe des X, si le mouvement des mains se produit également sur l’axe des Y.</span><span class="sxs-lookup"><span data-stu-id="c8460-249">In this case the system will recognize hand movements across X axis as long as they remain within an imaginary rails (guide) on the X axis, if hand movement also occurs on the Y axis.</span></span>

<span data-ttu-id="c8460-250">Dans les applications 2D, l’utilisateur peut se servir de mouvements de navigation verticaux pour faire défiler l’écran, effectuer un zoom ou faire glisser un élément à l’intérieur de l’application.</span><span class="sxs-lookup"><span data-stu-id="c8460-250">Within 2D apps, users can use vertical navigation gestures to scroll, zoom, or drag inside the app.</span></span> <span data-ttu-id="c8460-251">Des interactions tactiles virtuelles sont ainsi injectées dans l’application pour simuler des mouvements tactiles du même type.</span><span class="sxs-lookup"><span data-stu-id="c8460-251">This injects virtual finger touches to the app to simulate touch gestures of the same type.</span></span> <span data-ttu-id="c8460-252">Les utilisateurs peuvent sélectionner les actions à effectuer en basculant entre les outils de la barre au-dessus de l’application, soit en sélectionnant le bouton, soit en disant « < défilement/glissement/Zoom > outil ».</span><span class="sxs-lookup"><span data-stu-id="c8460-252">Users can select which of these actions take place by toggling between the tools on the bar above the application, either by selecting the button or saying '<Scroll/Drag/Zoom> Tool'.</span></span>

[<span data-ttu-id="c8460-253">Plus d’informations sur les mouvements composites</span><span class="sxs-lookup"><span data-stu-id="c8460-253">More info on composite gestures</span></span>](gaze-and-commit.md#composite-gestures)

## <a name="gesture-recognizers"></a><span data-ttu-id="c8460-254">Modules de reconnaissance des mouvements</span><span class="sxs-lookup"><span data-stu-id="c8460-254">Gesture recognizers</span></span>

<span data-ttu-id="c8460-255">L’un des avantages de l’utilisation de la reconnaissance des mouvements est que vous pouvez configurer un module de reconnaissance de mouvement uniquement pour les mouvements que l’hologramme actuellement ciblé peut accepter.</span><span class="sxs-lookup"><span data-stu-id="c8460-255">One benefit of using gesture recognition is that you can configure a gesture recognizer only for the gestures the currently targeted hologram can accept.</span></span> <span data-ttu-id="c8460-256">La plateforme ne fait que lever l’ambiguïté nécessaire pour distinguer les gestes pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c8460-256">The platform only does disambiguation as necessary to distinguish those particular supported gestures.</span></span> <span data-ttu-id="c8460-257">De cette façon, un hologramme qui prend uniquement en charge le TAP-Air peut accepter n’importe quel laps de temps entre une pression et une mise en route, tandis qu’un hologramme qui prend en charge les deux robinets peut promouvoir le robinet en attente après le seuil de temps de maintien.</span><span class="sxs-lookup"><span data-stu-id="c8460-257">In this way, a hologram that just supports air tap can accept any length of time between press and release, while a hologram that supports both tap and hold can promote the tap to a hold after the hold time threshold.</span></span>

## <a name="hand-recognition"></a><span data-ttu-id="c8460-258">Reconnaissance des mouvements de la main</span><span class="sxs-lookup"><span data-stu-id="c8460-258">Hand recognition</span></span>
<span data-ttu-id="c8460-259">HoloLens reconnaît les mouvements de la main en effectuant le suivi de la position de la main, ou des mains, que l’appareil peut voir.</span><span class="sxs-lookup"><span data-stu-id="c8460-259">HoloLens recognizes hand gestures by tracking the position of either or both hands that are visible to the device.</span></span> <span data-ttu-id="c8460-260">HoloLens voit les mains quand elles sont dans l’état « prêt » (dos de la main face à vous, index dressé) ou « enfoncé » (dos de la main face à vous, index abaissé).</span><span class="sxs-lookup"><span data-stu-id="c8460-260">HoloLens sees hands when they are in either the ready state (back of the hand facing you with index finger up) or the pressed state (back of the hand facing you with the index finger down).</span></span> <span data-ttu-id="c8460-261">Lorsque les mains sont dans d’autres poses, HoloLens les ignore.</span><span class="sxs-lookup"><span data-stu-id="c8460-261">When hands are in other poses, HoloLens ignores them.</span></span>
<span data-ttu-id="c8460-262">Pour chaque main détectée par HoloLens, vous pouvez accéder à sa position sans orientation et à son état appuyé.</span><span class="sxs-lookup"><span data-stu-id="c8460-262">For each hand that HoloLens detects, you can access its position without orientation and its pressed state.</span></span> <span data-ttu-id="c8460-263">Quand la main s’approche du bord du cadre de mouvement, vous disposez également d’un vecteur de direction, que vous pouvez présenter à l’utilisateur afin qu’il sache comment déplacer sa main de manière à ce que HoloLens puisse la voir.</span><span class="sxs-lookup"><span data-stu-id="c8460-263">As the hand nears the edge of the gesture frame, you're also provided with a direction vector, which you can show to the user so they know how to move their hand to get it back where HoloLens can see it.</span></span>

## <a name="gesture-frame"></a><span data-ttu-id="c8460-264">Cadre de mouvement</span><span class="sxs-lookup"><span data-stu-id="c8460-264">Gesture frame</span></span>
<span data-ttu-id="c8460-265">Pour les gestes sur HoloLens, la main doit se trouver dans un cadre de mouvement, dans une plage que les caméras de détection de mouvement peuvent voir de manière appropriée, d’un nez à l’autre et entre les épaules.</span><span class="sxs-lookup"><span data-stu-id="c8460-265">For gestures on HoloLens, the hand must be within a gesture frame, in a range that the gesture-sensing cameras can see appropriately,  from nose to waist and between the shoulders.</span></span> <span data-ttu-id="c8460-266">Les utilisateurs doivent être formés dans ce domaine de reconnaissance pour la réussite de l’action et pour leur propre confort.</span><span class="sxs-lookup"><span data-stu-id="c8460-266">Users need to be trained on this area of recognition both for success of action and for their own comfort.</span></span> <span data-ttu-id="c8460-267">Un grand nombre d’utilisateurs partent initialement du principe que le cadre de mouvement doit se trouver dans leur vue par le biais de HoloLens et que leurs bras ne sont pas plus confortables pour interagir.</span><span class="sxs-lookup"><span data-stu-id="c8460-267">Many users will initially assume that the gesture frame must be within their view through HoloLens, and hold their arms up uncomfortably in order to interact.</span></span> <span data-ttu-id="c8460-268">Lorsque vous utilisez le clicker HoloLens, il n’est pas nécessaire que les mains soient dans le cadre de mouvement.</span><span class="sxs-lookup"><span data-stu-id="c8460-268">When using the HoloLens Clicker, it's not necessary for hands to be within the gesture frame.</span></span>

<span data-ttu-id="c8460-269">En particulier, dans le cas de mouvements continus, il existe un risque que les utilisateurs se déplacent en dehors du cadre du geste pendant le déplacement d’un objet holographique, par exemple, et perdent leur résultat prévu.</span><span class="sxs-lookup"><span data-stu-id="c8460-269">In the case of continuous gestures in particular, there is some risk of users moving their hands outside of the gesture frame while in mid-gesture when moving a holographic object, for example, and losing their intended outcome.</span></span>

<span data-ttu-id="c8460-270">Voici trois choses que vous devez envisager :</span><span class="sxs-lookup"><span data-stu-id="c8460-270">There are three things that you should consider:</span></span>

- <span data-ttu-id="c8460-271">Éducation de l’utilisateur sur l’existence du cadre de mouvement et les limites approximatives.</span><span class="sxs-lookup"><span data-stu-id="c8460-271">User education on the gesture frame's existence and approximate boundaries.</span></span> <span data-ttu-id="c8460-272">Ce processus est enseigné au cours de la configuration de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="c8460-272">This is taught during HoloLens setup.</span></span>

- <span data-ttu-id="c8460-273">Notifier les utilisateurs lorsque leurs gestes approchent ou rompent les limites du cadre de mouvement au sein d’une application jusqu’à ce qu’un geste perdu aboutisse à des résultats indésirables.</span><span class="sxs-lookup"><span data-stu-id="c8460-273">Notifying users when their gestures are nearing or breaking the gesture frame boundaries within an application to the degree that a lost gesture leads to undesired outcomes.</span></span> <span data-ttu-id="c8460-274">La recherche a montré les qualités clés d’un tel système de notification.</span><span class="sxs-lookup"><span data-stu-id="c8460-274">Research has shown the key qualities of such a notification system.</span></span> <span data-ttu-id="c8460-275">L’interpréteur de commandes HoloLens fournit un bon exemple de ce type de notification, visuel, sur le curseur central, indiquant la direction dans laquelle le franchissement des limites est effectué.</span><span class="sxs-lookup"><span data-stu-id="c8460-275">The HoloLens shell provides a good example of this type of notification--visual, on the central cursor, indicating the direction in which boundary crossing is taking place.</span></span>

- <span data-ttu-id="c8460-276">Réduire au minimum les conséquences d’un franchissement des limites du cadre de mouvement.</span><span class="sxs-lookup"><span data-stu-id="c8460-276">Consequences of breaking the gesture frame boundaries should be minimized.</span></span> <span data-ttu-id="c8460-277">En général, cela signifie que le résultat d’un mouvement doit être arrêté à la limite et non inversé.</span><span class="sxs-lookup"><span data-stu-id="c8460-277">In general, this means that the outcome of a gesture should be stopped at the boundary, and not reversed.</span></span> <span data-ttu-id="c8460-278">Par exemple, si un utilisateur déplace un objet holographique dans une salle, le mouvement doit s’arrêter lorsque le cadre de mouvement est violé, et n’est pas retourné au point de départ.</span><span class="sxs-lookup"><span data-stu-id="c8460-278">For example, if a user is moving some holographic object across a room, the movement should stop when the gesture frame is breached, and not returned to the starting point.</span></span> <span data-ttu-id="c8460-279">L’utilisateur peut faire des frustrations, mais il peut comprendre plus rapidement les limites et ne pas avoir à redémarrer ses actions complètes à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="c8460-279">The user might experience some frustration, but might more quickly understand the boundaries, and not have to restart their full intended actions each time.</span></span>



## <a name="see-also"></a><span data-ttu-id="c8460-280">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c8460-280">See also</span></span>
* [<span data-ttu-id="c8460-281">Interaction basée sur le regard</span><span class="sxs-lookup"><span data-stu-id="c8460-281">Eye-based interaction</span></span>](eye-gaze-interaction.md)
* [<span data-ttu-id="c8460-282">Suivi oculaire sur HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="c8460-282">Eye tracking on HoloLens 2</span></span>](eye-tracking.md)
* [<span data-ttu-id="c8460-283">Pointer du regard et fixer</span><span class="sxs-lookup"><span data-stu-id="c8460-283">Gaze and dwell</span></span>](gaze-and-dwell.md)
* [<span data-ttu-id="c8460-284">Mains : Manipulation directe</span><span class="sxs-lookup"><span data-stu-id="c8460-284">Hands - Direct manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="c8460-285">Mains : Mouvements</span><span class="sxs-lookup"><span data-stu-id="c8460-285">Hands - Gestures</span></span>](gaze-and-commit.md#composite-gestures)
* [<span data-ttu-id="c8460-286">Mains : Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="c8460-286">Hands - Point and commit</span></span>](point-and-commit.md)
* [<span data-ttu-id="c8460-287">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="c8460-287">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="c8460-288">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="c8460-288">Voice input</span></span>](voice-input.md)

