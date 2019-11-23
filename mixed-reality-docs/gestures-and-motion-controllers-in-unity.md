---
title: Mouvements et contrôleurs de mouvement dans Unity
description: Il existe deux façons principales d’agir sur votre point d’intergression, les gestes manuels et les contrôleurs de mouvement.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: mouvements, contrôleurs de mouvement, Unity, point de regard, entrée
ms.openlocfilehash: a85797bfb443f33147c116e90a02c88abda63c67
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926571"
---
# <a name="gestures-and-motion-controllers-in-unity"></a><span data-ttu-id="2adf1-104">Mouvements et contrôleurs de mouvement dans Unity</span><span class="sxs-lookup"><span data-stu-id="2adf1-104">Gestures and motion controllers in Unity</span></span>

<span data-ttu-id="2adf1-105">Il existe deux façons principales d’agir sur votre point [de regard](gaze-in-unity.md), les [gestes manuels](gaze-and-commit.md#composite-gestures) et les [contrôleurs de mouvement](motion-controllers.md) dans HoloLens et les HMD immersifs.</span><span class="sxs-lookup"><span data-stu-id="2adf1-105">There are two key ways to take action on your [gaze in Unity](gaze-in-unity.md), [hand gestures](gaze-and-commit.md#composite-gestures) and [motion controllers](motion-controllers.md) in HoloLens and Immersive HMD.</span></span> <span data-ttu-id="2adf1-106">Vous accédez aux données des deux sources d’entrée spatiale via les mêmes API dans Unity.</span><span class="sxs-lookup"><span data-stu-id="2adf1-106">You access the data for both sources of spatial input through the same APIs in Unity.</span></span>

<span data-ttu-id="2adf1-107">Unity fournit deux méthodes principales pour accéder aux données d’entrée spatiale pour Windows Mixed Reality, les API common *Input. GetButton/Input. GetAxis* qui fonctionnent sur plusieurs SDK XR Unity, et une API *InteractionManager/GestureRecognizer* propre à Windows Mixed Reality qui expose l’ensemble complet des données d’entrée spatiale disponibles.</span><span class="sxs-lookup"><span data-stu-id="2adf1-107">Unity provides two primary ways to access spatial input data for Windows Mixed Reality, the common *Input.GetButton/Input.GetAxis* APIs that work across multiple Unity XR SDKs, and an *InteractionManager/GestureRecognizer* API specific to Windows Mixed Reality that exposes the full set of spatial input data available.</span></span>

## <a name="unity-buttonaxis-mapping-table"></a><span data-ttu-id="2adf1-108">Bouton Unity/table de mappage des axes</span><span class="sxs-lookup"><span data-stu-id="2adf1-108">Unity button/axis mapping table</span></span>

<span data-ttu-id="2adf1-109">Les ID de bouton et d’axe dans le tableau ci-dessous sont pris en charge dans le gestionnaire d’entrée d’Unity Manager pour les contrôleurs de mouvement Windows Mixed Real via les API *Input. GetButton/GetAxis* , tandis que la colonne « propre à Windows Mr » fait référence aux propriétés disponibles sur le type *InteractionSourceState* .</span><span class="sxs-lookup"><span data-stu-id="2adf1-109">The button and axis IDs in the table below are supported in Unity's Input Manager for Windows Mixed Reality motion controllers through the *Input.GetButton/GetAxis* APIs, while the "Windows MR-specific" column refers to properties available off of the *InteractionSourceState* type.</span></span> <span data-ttu-id="2adf1-110">Chacune de ces API est décrite en détail dans les sections ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2adf1-110">Each of these APIs are described in detail in the sections below.</span></span>

<span data-ttu-id="2adf1-111">Les mappages de bouton/ID d’axe pour Windows Mixed Reality correspondent généralement aux ID d’axe/bouton Oculus.</span><span class="sxs-lookup"><span data-stu-id="2adf1-111">The button/axis ID mappings for Windows Mixed Reality generally match the Oculus button/axis IDs.</span></span>

<span data-ttu-id="2adf1-112">Les mappages de bouton/ID d’axe pour Windows Mixed Reality diffèrent des mappages de OpenVR de deux façons :</span><span class="sxs-lookup"><span data-stu-id="2adf1-112">The button/axis ID mappings for Windows Mixed Reality differ from OpenVR's mappings in two ways:</span></span>
1. <span data-ttu-id="2adf1-113">Le mappage utilise des ID de pavé tactile distincts du stick analogique, pour prendre en charge des contrôleurs avec Thumbsticks et des pavés tactiles.</span><span class="sxs-lookup"><span data-stu-id="2adf1-113">The mapping uses touchpad IDs that are distinct from thumbstick, to support controllers with both thumbsticks and touchpads.</span></span>
2. <span data-ttu-id="2adf1-114">Le mappage évite de surcharger les ID de bouton A et X pour les boutons de menu, afin de conserver ceux disponibles pour les boutons ABXY physiques.</span><span class="sxs-lookup"><span data-stu-id="2adf1-114">The mapping avoids overloading the A and X button IDs for the Menu buttons, to leave those available for physical ABXY buttons.</span></span>

<table>
<tr>
<th rowspan="2"><span data-ttu-id="2adf1-115">Entrée</span><span class="sxs-lookup"><span data-stu-id="2adf1-115">Input</span></span> </th><th colspan="2"><span data-ttu-id="2adf1-116"><a href="gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis">API Unity courantes</a></span><span class="sxs-lookup"><span data-stu-id="2adf1-116"><a href="gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis">Common Unity APIs</a></span></span><br /><span data-ttu-id="2adf1-117">(Input. GetButton/GetAxis)</span><span class="sxs-lookup"><span data-stu-id="2adf1-117">(Input.GetButton/GetAxis)</span></span> </th><th rowspan="2"><span data-ttu-id="2adf1-118"><a href="gestures-and-motion-controllers-in-unity.md#">API d’entrée spécifique à Windows MR</a></span><span class="sxs-lookup"><span data-stu-id="2adf1-118"><a href="gestures-and-motion-controllers-in-unity.md#">Windows MR-specific Input API</a></span></span><br /><span data-ttu-id="2adf1-119">XR. WSA. Entrée</span><span class="sxs-lookup"><span data-stu-id="2adf1-119">(XR.WSA.Input)</span></span></th>
</tr><tr>
<th> <span data-ttu-id="2adf1-120">Main gauche</span><span class="sxs-lookup"><span data-stu-id="2adf1-120">Left hand</span></span> </th><th> <span data-ttu-id="2adf1-121">À droite</span><span class="sxs-lookup"><span data-stu-id="2adf1-121">Right hand</span></span></th>
</tr><tr>
<td> <span data-ttu-id="2adf1-122">Sélectionner le déclencheur enfoncé</span><span class="sxs-lookup"><span data-stu-id="2adf1-122">Select trigger pressed</span></span> </td><td> <span data-ttu-id="2adf1-123">Axe 9 = 1,0</span><span class="sxs-lookup"><span data-stu-id="2adf1-123">Axis 9 = 1.0</span></span> </td><td> <span data-ttu-id="2adf1-124">Axe 10 = 1,0</span><span class="sxs-lookup"><span data-stu-id="2adf1-124">Axis 10 = 1.0</span></span> </td><td> <span data-ttu-id="2adf1-125">selectPressed</span><span class="sxs-lookup"><span data-stu-id="2adf1-125">selectPressed</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-126">Sélectionner la valeur analogique du déclencheur</span><span class="sxs-lookup"><span data-stu-id="2adf1-126">Select trigger analog value</span></span> </td><td> <span data-ttu-id="2adf1-127">Axe 9</span><span class="sxs-lookup"><span data-stu-id="2adf1-127">Axis 9</span></span> </td><td> <span data-ttu-id="2adf1-128">Axe 10</span><span class="sxs-lookup"><span data-stu-id="2adf1-128">Axis 10</span></span> </td><td> <span data-ttu-id="2adf1-129">selectPressedAmount</span><span class="sxs-lookup"><span data-stu-id="2adf1-129">selectPressedAmount</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-130">Sélectionner le déclencheur partiellement enfoncé</span><span class="sxs-lookup"><span data-stu-id="2adf1-130">Select trigger partially pressed</span></span> </td><td> <span data-ttu-id="2adf1-131">Bouton 14 <i>(compatibilité du boîtier de</i> l’option) </span><span class="sxs-lookup"><span data-stu-id="2adf1-131">Button 14 <i>(gamepad compat)</i> </span></span></td><td> <span data-ttu-id="2adf1-132">Bouton 15 <i>(compatibilité du boîtier de</i> l’option) </span><span class="sxs-lookup"><span data-stu-id="2adf1-132">Button 15 <i>(gamepad compat)</i> </span></span></td><td> <span data-ttu-id="2adf1-133">selectPressedAmount &gt; 0,0</span><span class="sxs-lookup"><span data-stu-id="2adf1-133">selectPressedAmount &gt; 0.0</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-134">Bouton de menu enfoncé</span><span class="sxs-lookup"><span data-stu-id="2adf1-134">Menu button pressed</span></span> </td><td> <span data-ttu-id="2adf1-135">Bouton 6 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-135">Button 6\*</span></span> </td><td> <span data-ttu-id="2adf1-136">Bouton 7 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-136">Button 7\*</span></span> </td><td> <span data-ttu-id="2adf1-137">menuPressed</span><span class="sxs-lookup"><span data-stu-id="2adf1-137">menuPressed</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-138">Bouton de préhension enfoncé</span><span class="sxs-lookup"><span data-stu-id="2adf1-138">Grip button pressed</span></span> </td><td> <span data-ttu-id="2adf1-139">Axe 11 = 1,0 (aucune valeur analogique)</span><span class="sxs-lookup"><span data-stu-id="2adf1-139">Axis 11 = 1.0 (no analog values)</span></span><br /><span data-ttu-id="2adf1-140">Bouton 4 <i>(compatibilité du boîtier de</i> l’option) </span><span class="sxs-lookup"><span data-stu-id="2adf1-140">Button 4 <i>(gamepad compat)</i> </span></span></td><td> <span data-ttu-id="2adf1-141">Axe 12 = 1,0 (aucune valeur analogique)</span><span class="sxs-lookup"><span data-stu-id="2adf1-141">Axis 12 = 1.0 (no analog values)</span></span><br /><span data-ttu-id="2adf1-142">Bouton 5 <i>(compatibilité du boîtier de</i> l’option) </span><span class="sxs-lookup"><span data-stu-id="2adf1-142">Button 5 <i>(gamepad compat)</i> </span></span></td><td> <span data-ttu-id="2adf1-143">saisi</span><span class="sxs-lookup"><span data-stu-id="2adf1-143">grasped</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-144">Stick analogique X <i>(gauche :-1,0, droite : 1,0)</i> </span><span class="sxs-lookup"><span data-stu-id="2adf1-144">Thumbstick X <i>(left: -1.0, right: 1.0)</i> </span></span></td><td> <span data-ttu-id="2adf1-145">Axe 1</span><span class="sxs-lookup"><span data-stu-id="2adf1-145">Axis 1</span></span> </td><td> <span data-ttu-id="2adf1-146">Axe 4</span><span class="sxs-lookup"><span data-stu-id="2adf1-146">Axis 4</span></span> </td><td> <span data-ttu-id="2adf1-147">thumbstickPosition. x</span><span class="sxs-lookup"><span data-stu-id="2adf1-147">thumbstickPosition.x</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-148">Joystick Y <i>(haut :-1,0, bas : 1,0)</i> </span><span class="sxs-lookup"><span data-stu-id="2adf1-148">Thumbstick Y <i>(top: -1.0, bottom: 1.0)</i> </span></span></td><td> <span data-ttu-id="2adf1-149">Axe 2</span><span class="sxs-lookup"><span data-stu-id="2adf1-149">Axis 2</span></span> </td><td> <span data-ttu-id="2adf1-150">Axe 5</span><span class="sxs-lookup"><span data-stu-id="2adf1-150">Axis 5</span></span> </td><td> <span data-ttu-id="2adf1-151">thumbstickPosition. y</span><span class="sxs-lookup"><span data-stu-id="2adf1-151">thumbstickPosition.y</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-152">Stick analogique appuyé</span><span class="sxs-lookup"><span data-stu-id="2adf1-152">Thumbstick pressed</span></span> </td><td> <span data-ttu-id="2adf1-153">Bouton 8</span><span class="sxs-lookup"><span data-stu-id="2adf1-153">Button 8</span></span> </td><td> <span data-ttu-id="2adf1-154">Bouton 9</span><span class="sxs-lookup"><span data-stu-id="2adf1-154">Button 9</span></span> </td><td> <span data-ttu-id="2adf1-155">thumbstickPressed</span><span class="sxs-lookup"><span data-stu-id="2adf1-155">thumbstickPressed</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-156">Pavé tactile X <i>(à gauche :-1,0, droite : 1,0)</i> </span><span class="sxs-lookup"><span data-stu-id="2adf1-156">Touchpad X <i>(left: -1.0, right: 1.0)</i> </span></span></td><td> <span data-ttu-id="2adf1-157">Axe 17 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-157">Axis 17\*</span></span> </td><td> <span data-ttu-id="2adf1-158">Axe 19 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-158">Axis 19\*</span></span> </td><td> <span data-ttu-id="2adf1-159">touchpadPosition. x</span><span class="sxs-lookup"><span data-stu-id="2adf1-159">touchpadPosition.x</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-160">Pavé tactile Y <i>(haut :-1,0, bas : 1,0)</i> </span><span class="sxs-lookup"><span data-stu-id="2adf1-160">Touchpad Y <i>(top: -1.0, bottom: 1.0)</i> </span></span></td><td> <span data-ttu-id="2adf1-161">Axe 18 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-161">Axis 18\*</span></span> </td><td> <span data-ttu-id="2adf1-162">Axe 20 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-162">Axis 20\*</span></span> </td><td> <span data-ttu-id="2adf1-163">touchpadPosition. y</span><span class="sxs-lookup"><span data-stu-id="2adf1-163">touchpadPosition.y</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-164">Pavé tactile touché</span><span class="sxs-lookup"><span data-stu-id="2adf1-164">Touchpad touched</span></span> </td><td> <span data-ttu-id="2adf1-165">Bouton 18 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-165">Button 18\*</span></span> </td><td> <span data-ttu-id="2adf1-166">Bouton 19 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-166">Button 19\*</span></span> </td><td> <span data-ttu-id="2adf1-167">touchpadTouched</span><span class="sxs-lookup"><span data-stu-id="2adf1-167">touchpadTouched</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-168">Pavé tactile enfoncé</span><span class="sxs-lookup"><span data-stu-id="2adf1-168">Touchpad pressed</span></span> </td><td> <span data-ttu-id="2adf1-169">Bouton 16 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-169">Button 16\*</span></span> </td><td> <span data-ttu-id="2adf1-170">Bouton 17 \*</span><span class="sxs-lookup"><span data-stu-id="2adf1-170">Button 17\*</span></span> </td><td> <span data-ttu-id="2adf1-171">touchpadPressed</span><span class="sxs-lookup"><span data-stu-id="2adf1-171">touchpadPressed</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-172">pose de la poignée ou du pointeur 6DoF</span><span class="sxs-lookup"><span data-stu-id="2adf1-172">6DoF grip pose or pointer pose</span></span> </td><td colspan="2"> <span data-ttu-id="2adf1-173"><i>Poignée</i> de pose uniquement : <a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html">XR. InputTracking. GetLocalPosition</a></span><span class="sxs-lookup"><span data-stu-id="2adf1-173"><i>Grip</i> pose only: <a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html">XR.InputTracking.GetLocalPosition</a></span></span><br /><span data-ttu-id="2adf1-174"><a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalRotation.html">XR. InputTracking.GetLocalRotation</a></span><span class="sxs-lookup"><span data-stu-id="2adf1-174"><a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalRotation.html">XR.InputTracking.GetLocalRotation</a></span></span></td><td> <span data-ttu-id="2adf1-175"><i>Poignée</i> ou <i>pointeur</i> en tant qu’argument : SourceState. sourcePose. TryGetPosition</span><span class="sxs-lookup"><span data-stu-id="2adf1-175">Pass <i>Grip</i> or <i>Pointer</i> as an argument: sourceState.sourcePose.TryGetPosition</span></span><br /><span data-ttu-id="2adf1-176">sourceState.sourcePose.TryGetRotation</span><span class="sxs-lookup"><span data-stu-id="2adf1-176">sourceState.sourcePose.TryGetRotation</span></span><br /></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-177">État du suivi</span><span class="sxs-lookup"><span data-stu-id="2adf1-177">Tracking state</span></span> </td><td colspan="2"> <span data-ttu-id="2adf1-178"><i>Précision de la position et risque de perte de source uniquement disponible via une API spécifique à MR</i> </span><span class="sxs-lookup"><span data-stu-id="2adf1-178"><i>Position accuracy and source loss risk only available through MR-specific API</i> </span></span></td><td> <span data-ttu-id="2adf1-179"><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourcePose-positionAccuracy.html">sourceState.sourcePose.positionAccuracy</a></span><span class="sxs-lookup"><span data-stu-id="2adf1-179"><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourcePose-positionAccuracy.html">sourceState.sourcePose.positionAccuracy</a></span></span><br /><span data-ttu-id="2adf1-180"><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourceProperties-sourceLossRisk.html">sourceState. Properties. sourceLossRisk</a></span><span class="sxs-lookup"><span data-stu-id="2adf1-180"><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourceProperties-sourceLossRisk.html">sourceState.properties.sourceLossRisk</a></span></span></td>
</tr>
</table>

>[!NOTE]
><span data-ttu-id="2adf1-181">Ces ID de bouton/axe diffèrent des ID utilisés par Unity pour les OpenVR en raison de collisions dans les mappages utilisés par les boîtiers de soucodeurs, Oculus touch et OpenVR.</span><span class="sxs-lookup"><span data-stu-id="2adf1-181">These button/axis IDs differ from the IDs that Unity uses for OpenVR due to collisions in the mappings used by gamepads, Oculus Touch and OpenVR.</span></span>

## <a name="grip-pose-vs-pointing-pose"></a><span data-ttu-id="2adf1-182">Poignée de pose et pose de pointage</span><span class="sxs-lookup"><span data-stu-id="2adf1-182">Grip pose vs. pointing pose</span></span>

<span data-ttu-id="2adf1-183">Windows Mixed Reality prend en charge les contrôleurs de mouvement dans un large éventail de facteurs de forme, la conception de chaque contrôleur étant différente dans sa relation entre la position de l’utilisateur et la direction « avant » naturelle que les applications doivent utiliser pour pointer lors du rendu de la SideWinder.</span><span class="sxs-lookup"><span data-stu-id="2adf1-183">Windows Mixed Reality supports motion controllers in a variety of form factors, with each controller's design differing in its relationship between the user's hand position and the natural "forward" direction that apps should use for pointing when rendering the controller.</span></span>

<span data-ttu-id="2adf1-184">Pour mieux représenter ces contrôleurs, il existe deux genres de poses que vous pouvez examiner pour chaque source d’interaction, le pose de la **poignée** et le **pointeur se posent**.</span><span class="sxs-lookup"><span data-stu-id="2adf1-184">To better represent these controllers, there are two kinds of poses you can investigate for each interaction source, the **grip pose** and the **pointer pose**.</span></span> <span data-ttu-id="2adf1-185">Les coordonnées de pose de la poignée et du pointeur sont exprimées par toutes les API Unity dans les coordonnées universelles Unity universel.</span><span class="sxs-lookup"><span data-stu-id="2adf1-185">Both the grip pose and pointer pose coordinates are expressed by all Unity APIs in global Unity world coordinates.</span></span>

### <a name="grip-pose"></a><span data-ttu-id="2adf1-186">Poignée de pose</span><span class="sxs-lookup"><span data-stu-id="2adf1-186">Grip pose</span></span>

<span data-ttu-id="2adf1-187">La **poignée** représente l’emplacement de la paume d’une main détectée par un HoloLens ou la poche qui détient un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="2adf1-187">The **grip pose** represents the location of either the palm of a hand detected by a HoloLens, or the palm holding a motion controller.</span></span>

<span data-ttu-id="2adf1-188">Sur les casques immersifs, le pose de la poignée est utilisé pour restituer **la main de l’utilisateur** ou **un objet détenu par l’utilisateur**, tel qu’un épée ou un pistolet.</span><span class="sxs-lookup"><span data-stu-id="2adf1-188">On immersive headsets, the grip pose is best used to render **the user's hand** or **an object held in the user's hand**, such as a sword or gun.</span></span> <span data-ttu-id="2adf1-189">La poignée est également utilisée lors de la visualisation d’un contrôleur de mouvement, car le **modèle de rendu** fourni par Windows pour un contrôleur de mouvement utilise la poignée comme son origine et le centre de rotation.</span><span class="sxs-lookup"><span data-stu-id="2adf1-189">The grip pose is also used when visualizing a motion controller, as the **renderable model** provided by Windows for a motion controller uses the grip pose as its origin and center of rotation.</span></span>

<span data-ttu-id="2adf1-190">La poignée est définie spécifiquement comme suit :</span><span class="sxs-lookup"><span data-stu-id="2adf1-190">The grip pose is defined specifically as follows:</span></span>
* <span data-ttu-id="2adf1-191">Position de la **poignée**: le centre de la poche quand il maintient le contrôleur naturellement, ajusté à gauche ou à droite pour centrer la position au sein de la poignée.</span><span class="sxs-lookup"><span data-stu-id="2adf1-191">The **grip position**: The palm centroid when holding the controller naturally, adjusted left or right to center the position within the grip.</span></span> <span data-ttu-id="2adf1-192">Sur le contrôleur de mouvement Windows Mixed Reality, cette position s’aligne généralement avec le bouton de saisie.</span><span class="sxs-lookup"><span data-stu-id="2adf1-192">On the Windows Mixed Reality motion controller, this position generally aligns with the Grasp button.</span></span>
* <span data-ttu-id="2adf1-193">**Axe droit de l’orientation de la poignée**: lorsque vous ouvrez complètement votre main pour former une pose plate à 5 doigts, le rayon normal à votre paume (en avant à partir de la poche de gauche, en arrière depuis la paume de droite)</span><span class="sxs-lookup"><span data-stu-id="2adf1-193">The **grip orientation's Right axis**: When you completely open your hand to form a flat 5-finger pose, the ray that is normal to your palm (forward from left palm, backward from right palm)</span></span>
* <span data-ttu-id="2adf1-194">**Axe avant de l’orientation de la poignée**: quand vous fermez partiellement votre main (comme si vous détenir le contrôleur), le rayon qui pointe vers l’avant dans le tube formé par vos doigts non thumbs.</span><span class="sxs-lookup"><span data-stu-id="2adf1-194">The **grip orientation's Forward axis**: When you close your hand partially (as if holding the controller), the ray that points "forward" through the tube formed by your non-thumb fingers.</span></span>
* <span data-ttu-id="2adf1-195">**Axe vers le haut de l’orientation**: l’axe vers le haut, impliqué dans les définitions Right et Forward.</span><span class="sxs-lookup"><span data-stu-id="2adf1-195">The **grip orientation's Up axis**: The Up axis implied by the Right and Forward definitions.</span></span>

<span data-ttu-id="2adf1-196">Vous pouvez accéder à la poignée à l’aide de l’API d’entrée entre fournisseurs de l’unité Unity ( *[XR. InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html). GetLocalPosition/rotation*) ou via l’API propre à Windows Mr (*SourceState. SourcePose. TryGetPosition/rotation*, en demandant des données de pose pour le nœud de **poignée** ).</span><span class="sxs-lookup"><span data-stu-id="2adf1-196">You can access the grip pose through either Unity's cross-vendor input API (*[XR.InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html).GetLocalPosition/Rotation*) or through the Windows MR-specific API (*sourceState.sourcePose.TryGetPosition/Rotation*, requesting pose data for the **Grip** node).</span></span>

### <a name="pointer-pose"></a><span data-ttu-id="2adf1-197">Pose du pointeur</span><span class="sxs-lookup"><span data-stu-id="2adf1-197">Pointer pose</span></span>

<span data-ttu-id="2adf1-198">Le **pointeur de pose** représente l’extrémité du contrôleur pointant vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="2adf1-198">The **pointer pose** represents the tip of the controller pointing forward.</span></span>

<span data-ttu-id="2adf1-199">Le pointeur fourni par le système est le mieux utilisé pour raycast lorsque vous effectuez **le rendu du modèle de contrôleur lui-même**.</span><span class="sxs-lookup"><span data-stu-id="2adf1-199">The system-provided pointer pose is best used to raycast when you are **rendering the controller model itself**.</span></span> <span data-ttu-id="2adf1-200">Si vous effectuez le rendu d’un autre objet virtuel à la place du contrôleur, tel qu’un pistolet virtuel, vous devez pointer vers un rayon qui est le plus naturel pour cet objet virtuel, tel qu’un rayon qui traverse le canon du modèle de pistolet défini par l’application.</span><span class="sxs-lookup"><span data-stu-id="2adf1-200">If you are rendering some other virtual object in place of the controller, such as a virtual gun, you should point with a ray that is most natural for that virtual object, such as a ray that travels along the barrel of the app-defined gun model.</span></span> <span data-ttu-id="2adf1-201">Étant donné que les utilisateurs peuvent voir l’objet virtuel et non le contrôleur physique, le fait de pointer avec l’objet virtuel sera probablement plus naturel pour ceux qui utilisent votre application.</span><span class="sxs-lookup"><span data-stu-id="2adf1-201">Because users can see the virtual object and not the physical controller, pointing with the virtual object will likely be more natural for those using your app.</span></span>

<span data-ttu-id="2adf1-202">Actuellement, le pointeur de pose est disponible dans Unity uniquement par le biais de l’API propre à Windows MR, *sourceState. sourcePose. TryGetPosition/rotation*, en passant *InteractionSourceNode. pointeur* comme argument.</span><span class="sxs-lookup"><span data-stu-id="2adf1-202">Currently, the pointer pose is available in Unity only through the Windows MR-specific API, *sourceState.sourcePose.TryGetPosition/Rotation*, passing in *InteractionSourceNode.Pointer* as the argument.</span></span>

## <a name="controller-tracking-state"></a><span data-ttu-id="2adf1-203">État du suivi du contrôleur</span><span class="sxs-lookup"><span data-stu-id="2adf1-203">Controller tracking state</span></span>

<span data-ttu-id="2adf1-204">À l’instar des casques, le contrôleur de mouvement Windows Mixed Reality ne nécessite pas de configuration de capteurs de suivi externe.</span><span class="sxs-lookup"><span data-stu-id="2adf1-204">Like the headsets, the Windows Mixed Reality motion controller requires no setup of external tracking sensors.</span></span> <span data-ttu-id="2adf1-205">Au lieu de cela, les contrôleurs sont suivis par des capteurs dans le casque lui-même.</span><span class="sxs-lookup"><span data-stu-id="2adf1-205">Instead, the controllers are tracked by sensors in the headset itself.</span></span>

<span data-ttu-id="2adf1-206">Si l’utilisateur déplace les contrôleurs du champ de vue du casque, dans la plupart des cas, Windows continue à déduire les positions des contrôleurs et à les fournir à l’application.</span><span class="sxs-lookup"><span data-stu-id="2adf1-206">If the user moves the controllers out of the headset's field of view, in most cases Windows will continue to infer controller positions and provide them to the app.</span></span> <span data-ttu-id="2adf1-207">Lorsque le contrôleur a perdu le suivi visuel suffisamment longtemps, les positions du contrôleur sont découpées à des positions de précision approximatives.</span><span class="sxs-lookup"><span data-stu-id="2adf1-207">When the controller has lost visual tracking for long enough, the controller's positions will drop to approximate-accuracy positions.</span></span>

<span data-ttu-id="2adf1-208">À ce stade, le système va verrouiller le contrôleur à l’utilisateur, en effectuant le suivi de la position de l’utilisateur lors de son déplacement, tout en exposant l’orientation réelle du contrôleur à l’aide de ses capteurs d’orientation internes.</span><span class="sxs-lookup"><span data-stu-id="2adf1-208">At this point, the system will body-lock the controller to the user, tracking the user's position as they move around, while still exposing the controller's true orientation using its internal orientation sensors.</span></span> <span data-ttu-id="2adf1-209">De nombreuses applications qui utilisent des contrôleurs pour pointer et activer des éléments d’interface utilisateur peuvent fonctionner normalement avec une précision approximative sans que l’utilisateur ne remarque.</span><span class="sxs-lookup"><span data-stu-id="2adf1-209">Many apps that use controllers to point at and activate UI elements can operate normally while in approximate accuracy without the user noticing.</span></span>

<span data-ttu-id="2adf1-210">La meilleure façon de vous en faire une idée est de l’essayer vous-même.</span><span class="sxs-lookup"><span data-stu-id="2adf1-210">The best way to get a feel for this is to try it yourself.</span></span> <span data-ttu-id="2adf1-211">Consultez cette vidéo avec des exemples de contenu immersif qui fonctionne avec les contrôleurs de mouvement dans différents États de suivi :</span><span class="sxs-lookup"><span data-stu-id="2adf1-211">Check out this video with examples of immersive content that works with motion controllers across various tracking states:</span></span>

<br>

 >[!VIDEO https://www.youtube.com/embed/QK_fOFDHj0g]

### <a name="reasoning-about-tracking-state-explicitly"></a><span data-ttu-id="2adf1-212">Raisonnement sur le suivi de l’État explicitement</span><span class="sxs-lookup"><span data-stu-id="2adf1-212">Reasoning about tracking state explicitly</span></span>

<span data-ttu-id="2adf1-213">Les applications qui souhaitent traiter différemment les positions en fonction de l’état de suivi peuvent aller plus loin et inspecter les propriétés de l’état du contrôleur, telles que *SourceLossRisk* et *PositionAccuracy*:</span><span class="sxs-lookup"><span data-stu-id="2adf1-213">Apps that wish to treat positions differently based on tracking state may go further and inspect properties on the controller's state, such as *SourceLossRisk* and *PositionAccuracy*:</span></span>

<table>
<tr>
<th> <span data-ttu-id="2adf1-214">État du suivi</span><span class="sxs-lookup"><span data-stu-id="2adf1-214">Tracking state</span></span> </th><th> <span data-ttu-id="2adf1-215">SourceLossRisk</span><span class="sxs-lookup"><span data-stu-id="2adf1-215">SourceLossRisk</span></span> </th><th> <span data-ttu-id="2adf1-216">PositionAccuracy</span><span class="sxs-lookup"><span data-stu-id="2adf1-216">PositionAccuracy</span></span> </th><th> <span data-ttu-id="2adf1-217">TryGetPosition</span><span class="sxs-lookup"><span data-stu-id="2adf1-217">TryGetPosition</span></span></th>
</tr><tr>
<td> <span data-ttu-id="2adf1-218">  de <b>haute précision</b></span><span class="sxs-lookup"><span data-stu-id="2adf1-218"><b>High accuracy</b> </span></span></td><td style="background-color: green; color: white"> <span data-ttu-id="2adf1-219">&lt; 1,0</span><span class="sxs-lookup"><span data-stu-id="2adf1-219">&lt; 1.0</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="2adf1-220">Élevé</span><span class="sxs-lookup"><span data-stu-id="2adf1-220">High</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="2adf1-221">true</span><span class="sxs-lookup"><span data-stu-id="2adf1-221">true</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-222"><b>Haute précision (risque de perte)</b> </span><span class="sxs-lookup"><span data-stu-id="2adf1-222"><b>High accuracy (at risk of losing)</b> </span></span></td><td style="background-color: orange"> <span data-ttu-id="2adf1-223">= = 1,0</span><span class="sxs-lookup"><span data-stu-id="2adf1-223">== 1.0</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="2adf1-224">Élevé</span><span class="sxs-lookup"><span data-stu-id="2adf1-224">High</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="2adf1-225">true</span><span class="sxs-lookup"><span data-stu-id="2adf1-225">true</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-226"><b>Précision approximative</b> </span><span class="sxs-lookup"><span data-stu-id="2adf1-226"><b>Approximate accuracy</b> </span></span></td><td style="background-color: orange"> <span data-ttu-id="2adf1-227">= = 1,0</span><span class="sxs-lookup"><span data-stu-id="2adf1-227">== 1.0</span></span> </td><td style="background-color: orange"> <span data-ttu-id="2adf1-228">Approximate</span><span class="sxs-lookup"><span data-stu-id="2adf1-228">Approximate</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="2adf1-229">true</span><span class="sxs-lookup"><span data-stu-id="2adf1-229">true</span></span></td>
</tr><tr>
<td> <span data-ttu-id="2adf1-230"><b>Aucune position</b> </span><span class="sxs-lookup"><span data-stu-id="2adf1-230"><b>No position</b> </span></span></td><td style="background-color: orange"> <span data-ttu-id="2adf1-231">= = 1,0</span><span class="sxs-lookup"><span data-stu-id="2adf1-231">== 1.0</span></span> </td><td style="background-color: orange"> <span data-ttu-id="2adf1-232">Approximate</span><span class="sxs-lookup"><span data-stu-id="2adf1-232">Approximate</span></span> </td><td style="background-color: orange"> <span data-ttu-id="2adf1-233">false</span><span class="sxs-lookup"><span data-stu-id="2adf1-233">false</span></span></td>
</tr>
</table>

<span data-ttu-id="2adf1-234">Ces États de suivi du contrôleur de mouvement sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="2adf1-234">These motion controller tracking states are defined as follows:</span></span>
* <span data-ttu-id="2adf1-235">**Précision élevée :** Alors que le contrôleur de mouvement se trouve dans le champ de vision du casque, il fournit généralement des positions à grande précision, en fonction du suivi visuel.</span><span class="sxs-lookup"><span data-stu-id="2adf1-235">**High accuracy:** While the motion controller is within the headset's field of view, it will generally provide high-accuracy positions, based on visual tracking.</span></span> <span data-ttu-id="2adf1-236">Notez qu’un contrôleur mobile qui laisse momentanément le champ de vue ou est momentanément masqué à partir des capteurs du casque (par exemple, par l’autre côté de l’utilisateur) continue à retourner des poses de grande précision pendant une brève période, en fonction du suivi inertiel du contrôleur. automatiquement.</span><span class="sxs-lookup"><span data-stu-id="2adf1-236">Note that a moving controller that momentarily leaves the field of view or is momentarily obscured from the headset sensors (e.g. by the user's other hand) will continue to return high-accuracy poses for a short time, based on inertial tracking of the controller itself.</span></span>
* <span data-ttu-id="2adf1-237">**Haute précision (risque de perte) :** Lorsque l’utilisateur déplace le contrôleur de mouvement au-delà du bord du champ de vue du casque, le casque ne pourra bientôt pas suivre la position du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="2adf1-237">**High accuracy (at risk of losing):** When the user moves the motion controller past the edge of the headset's field of view, the headset will soon be unable to visually track the controller's position.</span></span> <span data-ttu-id="2adf1-238">L’application sait quand le contrôleur a atteint cette limite d’aide en regardant le **SourceLossRisk** REACH 1,0.</span><span class="sxs-lookup"><span data-stu-id="2adf1-238">The app knows when the controller has reached this FOV boundary by seeing the **SourceLossRisk** reach 1.0.</span></span> <span data-ttu-id="2adf1-239">À ce stade, l’application peut choisir de suspendre les gestes de contrôleur qui nécessitent un flux constant de poses très haute qualité.</span><span class="sxs-lookup"><span data-stu-id="2adf1-239">At that point, the app may choose to pause controller gestures that require a steady stream of very high-quality poses.</span></span>
* <span data-ttu-id="2adf1-240">**Précision approximative :** Lorsque le contrôleur a perdu le suivi visuel suffisamment longtemps, les positions du contrôleur sont découpées à des positions de précision approximatives.</span><span class="sxs-lookup"><span data-stu-id="2adf1-240">**Approximate accuracy:** When the controller has lost visual tracking for long enough, the controller's positions will drop to approximate-accuracy positions.</span></span> <span data-ttu-id="2adf1-241">À ce stade, le système va verrouiller le contrôleur à l’utilisateur, en effectuant le suivi de la position de l’utilisateur lors de son déplacement, tout en exposant l’orientation réelle du contrôleur à l’aide de ses capteurs d’orientation internes.</span><span class="sxs-lookup"><span data-stu-id="2adf1-241">At this point, the system will body-lock the controller to the user, tracking the user's position as they move around, while still exposing the controller's true orientation using its internal orientation sensors.</span></span> <span data-ttu-id="2adf1-242">De nombreuses applications qui utilisent des contrôleurs pour pointer et activer des éléments d’interface utilisateur peuvent fonctionner normalement, tout en ayant une précision approximative, sans que l’utilisateur ne remarque.</span><span class="sxs-lookup"><span data-stu-id="2adf1-242">Many apps that use controllers to point at and activate UI elements can operate as normal while in approximate accuracy without the user noticing.</span></span> <span data-ttu-id="2adf1-243">Les applications avec des exigences d’entrée plus lourdes peuvent choisir de déterminer ce déplacement de la **haute** précision à une précision **approximative** en inspectant la propriété **PositionAccuracy** , par exemple pour accorder à l’utilisateur un hitbox plus généreux sur les cibles hors écran pendant cette période.</span><span class="sxs-lookup"><span data-stu-id="2adf1-243">Apps with heavier input requirements may choose to sense this drop from **High** accuracy to **Approximate** accuracy by inspecting the **PositionAccuracy** property, for example to give the user a more generous hitbox on off-screen targets during this time.</span></span>
* <span data-ttu-id="2adf1-244">**Aucune position :** Alors que le contrôleur peut fonctionner à des fins de précision approximative pendant une longue période, le système sait parfois que même une position verrouillée par le corps n’est pas significative pour le moment.</span><span class="sxs-lookup"><span data-stu-id="2adf1-244">**No position:** While the controller can operate at approximate accuracy for a long time, sometimes the system knows that even a body-locked position is not meaningful at the moment.</span></span> <span data-ttu-id="2adf1-245">Par exemple, un contrôleur qui vient d’être activé n’a peut-être jamais été observé visuellement, ou un utilisateur peut mettre un contrôleur qui est ensuite récupéré par une autre personne.</span><span class="sxs-lookup"><span data-stu-id="2adf1-245">For example, a controller that was just turned on may have never been observed visually, or a user may put down a controller that's then picked up by someone else.</span></span> <span data-ttu-id="2adf1-246">À ce moment-là, le système ne fournit aucune position à l’application, et *TryGetPosition* retourne la valeur false.</span><span class="sxs-lookup"><span data-stu-id="2adf1-246">At those times, the system will not provide any position to the app, and *TryGetPosition* will return false.</span></span>

## <a name="common-unity-apis-inputgetbuttongetaxis"></a><span data-ttu-id="2adf1-247">API Unity courantes (Input. GetButton/GetAxis)</span><span class="sxs-lookup"><span data-stu-id="2adf1-247">Common Unity APIs (Input.GetButton/GetAxis)</span></span>

<span data-ttu-id="2adf1-248">**Espace de noms :** *UnityEngine*, *UnityEngine. XR*</span><span class="sxs-lookup"><span data-stu-id="2adf1-248">**Namespace:** *UnityEngine*, *UnityEngine.XR*</span></span><br>
<span data-ttu-id="2adf1-249">**Types**: *Input*, *XR. InputTracking*</span><span class="sxs-lookup"><span data-stu-id="2adf1-249">**Types**: *Input*, *XR.InputTracking*</span></span>

<span data-ttu-id="2adf1-250">Unity utilise actuellement ses API *d’entrée. GetButton/Input. GetAxis* pour exposer l’entrée pour [le kit de développement logiciel (SDK) Oculus](https://docs.unity3d.com/Manual/OculusControllers.html), [le kit de développement logiciel (SDK) OpenVR et la](https://docs.unity3d.com/Manual/OpenVRControllers.html) réalité mixte Windows, y compris les contrôleurs mains et motion.</span><span class="sxs-lookup"><span data-stu-id="2adf1-250">Unity currently uses its general *Input.GetButton/Input.GetAxis* APIs to expose input for [the Oculus SDK](https://docs.unity3d.com/Manual/OculusControllers.html), [the OpenVR SDK](https://docs.unity3d.com/Manual/OpenVRControllers.html) and Windows Mixed Reality, including hands and motion controllers.</span></span> <span data-ttu-id="2adf1-251">Si votre application utilise ces API pour l’entrée, elle peut facilement prendre en charge des contrôleurs de mouvement sur plusieurs kits de développement logiciel (SDK) XR, y compris Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="2adf1-251">If your app uses these APIs for input, it can easily support motion controllers across multiple XR SDKs, including Windows Mixed Reality.</span></span>

### <a name="getting-a-logical-buttons-pressed-state"></a><span data-ttu-id="2adf1-252">Obtention de l’état enfoncé d’un bouton logique</span><span class="sxs-lookup"><span data-stu-id="2adf1-252">Getting a logical button's pressed state</span></span>

<span data-ttu-id="2adf1-253">Pour utiliser les API d’entrée Unity générales, vous commencez généralement par associer des boutons et des axes aux noms logiques dans le [Gestionnaire d’entrée Unity](https://docs.unity3d.com/Manual/ConventionalGameInput.html), en liant un bouton ou des ID d’axe à chaque nom.</span><span class="sxs-lookup"><span data-stu-id="2adf1-253">To use the general Unity input APIs, you'll typically start by wiring up buttons and axes to logical names in the [Unity Input Manager](https://docs.unity3d.com/Manual/ConventionalGameInput.html), binding a button or axis IDs to each name.</span></span> <span data-ttu-id="2adf1-254">Vous pouvez ensuite écrire du code qui fait référence à ce nom d’axe/bouton logique.</span><span class="sxs-lookup"><span data-stu-id="2adf1-254">You can then write code that refers to that logical button/axis name.</span></span>

<span data-ttu-id="2adf1-255">Par exemple, pour mapper le bouton de déclenchement du contrôleur de mouvement gauche à l’action envoyer, accédez à **modifier > paramètres du projet > entrée** dans Unity, puis développez les propriétés de la section envoyer sous axes.</span><span class="sxs-lookup"><span data-stu-id="2adf1-255">For example, to map the left motion controller's trigger button to the Submit action, go to **Edit > Project Settings > Input** within Unity, and expand the properties of the Submit section under Axes.</span></span> <span data-ttu-id="2adf1-256">Modifiez le bouton **positif** ou la propriété **ALT positive du bouton** pour lire le bouton de la manette de jeu **14**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="2adf1-256">Change the **Positive Button** or **Alt Positive Button** property to read **joystick button 14**, like this:</span></span>

<span data-ttu-id="2adf1-257">![](images/unity-input-manager.png) InputManager Unity</span><span class="sxs-lookup"><span data-stu-id="2adf1-257">![Unity's InputManager](images/unity-input-manager.png)</span></span><br>
<span data-ttu-id="2adf1-258">*InputManager Unity*</span><span class="sxs-lookup"><span data-stu-id="2adf1-258">*Unity InputManager*</span></span>

<span data-ttu-id="2adf1-259">Votre script peut ensuite Rechercher l’action envoyer à l’aide de *Input. GetButton*:</span><span class="sxs-lookup"><span data-stu-id="2adf1-259">Your script can then check for the Submit action using *Input.GetButton*:</span></span>

```cs
if (Input.GetButton("Submit"))
{
  // ...
}
```
<span data-ttu-id="2adf1-260">Vous pouvez ajouter des boutons logiques en modifiant la propriété **taille** sous **axes**.</span><span class="sxs-lookup"><span data-stu-id="2adf1-260">You can add more logical buttons by changing the **Size** property under **Axes**.</span></span>

### <a name="getting-a-physical-buttons-pressed-state-directly"></a><span data-ttu-id="2adf1-261">Obtention directe d’un état enfoncé d’un bouton physique</span><span class="sxs-lookup"><span data-stu-id="2adf1-261">Getting a physical button's pressed state directly</span></span>

<span data-ttu-id="2adf1-262">Vous pouvez également accéder manuellement aux boutons à l’aide de leur nom complet, en utilisant *Input. GetKey*:</span><span class="sxs-lookup"><span data-stu-id="2adf1-262">You can also access buttons manually by their fully-qualified name, using *Input.GetKey*:</span></span>

```cs
if (Input.GetKey("joystick button 8"))
{
  // ...
}
```

### <a name="getting-a-hand-or-motion-controllers-pose"></a><span data-ttu-id="2adf1-263">Obtention d’une main ou d’une pose de contrôleur de mouvement</span><span class="sxs-lookup"><span data-stu-id="2adf1-263">Getting a hand or motion controller's pose</span></span>

<span data-ttu-id="2adf1-264">Vous pouvez accéder à la position et à la rotation du contrôleur, à l’aide de *XR. InputTracking*:</span><span class="sxs-lookup"><span data-stu-id="2adf1-264">You can access the position and rotation of the controller, using *XR.InputTracking*:</span></span>

```cs
Vector3 leftPosition = InputTracking.GetLocalPosition(XRNode.LeftHand);
Quaternion leftRotation = InputTracking.GetLocalRotation(XRNode.LeftHand);
```

<span data-ttu-id="2adf1-265">Notez que cela représente la poignée de préhension du contrôleur (où l’utilisateur détient le contrôleur), qui est utile pour le rendu d’une arme ou d’un pistolet dans la main de l’utilisateur, ou un modèle du contrôleur lui-même.</span><span class="sxs-lookup"><span data-stu-id="2adf1-265">Note that this represents the controller's grip pose (where the user holds the controller), which is useful for rendering a sword or gun in the user's hand, or a model of the controller itself.</span></span>

<span data-ttu-id="2adf1-266">Notez que la relation entre cette poignée pose et que le pointeur pose (où l’extrémité du contrôleur pointe) peut différer d’un contrôle à l’autre.</span><span class="sxs-lookup"><span data-stu-id="2adf1-266">Note that the relationship between this grip pose and the pointer pose (where the tip of the controller is pointing) may differ across controllers.</span></span> <span data-ttu-id="2adf1-267">À ce stade, l’accès au pointeur du contrôleur est possible uniquement via l’API d’entrée spécifique à MR, décrite dans les sections ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2adf1-267">At this moment, accessing the controller's pointer pose is only possible through the MR-specific input API, described in the sections below.</span></span>

## <a name="windows-specific-apis-xrwsainput"></a><span data-ttu-id="2adf1-268">API spécifiques à Windows (XR. WSA. Entrée</span><span class="sxs-lookup"><span data-stu-id="2adf1-268">Windows-specific APIs (XR.WSA.Input)</span></span>

<span data-ttu-id="2adf1-269">**Espace de noms :** *UnityEngine. XR. WSA. Input*</span><span class="sxs-lookup"><span data-stu-id="2adf1-269">**Namespace:** *UnityEngine.XR.WSA.Input*</span></span><br>
<span data-ttu-id="2adf1-270">**Types**: *InteractionManager*, *InteractionSourceState*, *InteractionSource*, *InteractionSourceProperties*, *InteractionSourceKind*, *InteractionSourceLocation*</span><span class="sxs-lookup"><span data-stu-id="2adf1-270">**Types**: *InteractionManager*, *InteractionSourceState*, *InteractionSource*, *InteractionSourceProperties*, *InteractionSourceKind*, *InteractionSourceLocation*</span></span>

<span data-ttu-id="2adf1-271">Pour obtenir des informations plus détaillées sur l’entrée manuelle de Windows Mixed Reality (pour HoloLens) et les contrôleurs de mouvement, vous pouvez choisir d’utiliser les API d’entrée spatiale spécifiques à Windows sous l’espace de noms *UnityEngine. XR. WSA. Input* .</span><span class="sxs-lookup"><span data-stu-id="2adf1-271">To get at more detailed information about Windows Mixed Reality hand input (for HoloLens) and motion controllers, you can choose to use the Windows-specific spatial input APIs under the *UnityEngine.XR.WSA.Input* namespace.</span></span> <span data-ttu-id="2adf1-272">Cela vous permet d’accéder à des informations supplémentaires, telles que la précision de la position ou le genre de source, vous permettant de distinguer les mains et les contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="2adf1-272">This lets you access additional information, such as position accuracy or the source kind, letting you tell hands and controllers apart.</span></span>

### <a name="polling-for-the-state-of-hands-and-motion-controllers"></a><span data-ttu-id="2adf1-273">Interrogation de l’état des contrôleurs mains et motion</span><span class="sxs-lookup"><span data-stu-id="2adf1-273">Polling for the state of hands and motion controllers</span></span>

<span data-ttu-id="2adf1-274">Vous pouvez interroger l’état de ce frame pour chaque source d’interaction (contrôleur de main ou de mouvement) à l’aide de la méthode *GetCurrentReading* .</span><span class="sxs-lookup"><span data-stu-id="2adf1-274">You can poll for this frame's state for each interaction source (hand or motion controller) using the *GetCurrentReading* method.</span></span>

```cs
var interactionSourceStates = InteractionManager.GetCurrentReading();
foreach (var interactionSourceState in interactionSourceStates) {
    // ...
}
```

<span data-ttu-id="2adf1-275">Chaque *InteractionSourceState* que vous récupérez représente une source d’interaction à l’instant courant.</span><span class="sxs-lookup"><span data-stu-id="2adf1-275">Each *InteractionSourceState* you get back represents an interaction source at the current moment in time.</span></span> <span data-ttu-id="2adf1-276">*InteractionSourceState* expose des informations telles que :</span><span class="sxs-lookup"><span data-stu-id="2adf1-276">The *InteractionSourceState* exposes info such as:</span></span>
* <span data-ttu-id="2adf1-277">Quels sont les [types d’enfoncement](motion-controllers.md) (Select/menu///-pavé/Stick)</span><span class="sxs-lookup"><span data-stu-id="2adf1-277">Which [kinds of presses](motion-controllers.md) are occurring (Select/Menu/Grasp/Touchpad/Thumbstick)</span></span>

   ```cs
   if (interactionSourceState.selectPressed) {
       // ...
   }
   ```
* <span data-ttu-id="2adf1-278">Autres données spécifiques aux contrôleurs de mouvement, telles que le pavé tactile et/ou les coordonnées XY et l’État touché</span><span class="sxs-lookup"><span data-stu-id="2adf1-278">Other data specific to motion controllers, such the touchpad and/or thumbstick's XY coordinates and touched state</span></span>

   ```cs
   if (interactionSourceState.touchpadTouched && interactionSourceState.touchpadPosition.x > 0.5) {
       // ...
   }
   ```
   
* <span data-ttu-id="2adf1-279">InteractionSourceKind à savoir si la source est une main ou un contrôleur de mouvement</span><span class="sxs-lookup"><span data-stu-id="2adf1-279">The InteractionSourceKind to know if the source is a hand or a motion controller</span></span>

   ```cs
   if (interactionSourceState.source.kind == InteractionSourceKind.Hand) {
       // ...
   }
   ```

### <a name="polling-for-forward-predicted-rendering-poses"></a><span data-ttu-id="2adf1-280">Interrogation pour les poses de rendu prédits par progression</span><span class="sxs-lookup"><span data-stu-id="2adf1-280">Polling for forward-predicted rendering poses</span></span>

* <span data-ttu-id="2adf1-281">Lors de l’interrogation des données sources d’interaction à partir de mains et de contrôleurs, les poses que vous recevez sont des poses prédites pour le moment où les photons de ce frame atteindront les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2adf1-281">When polling for interaction source data from hands and controllers, the poses you get are forward-predicted poses for the moment in time when this frame's photons will reach the user's eyes.</span></span>  <span data-ttu-id="2adf1-282">Ces poses préprédits sont préférables pour le **rendu** du contrôleur ou d’un objet détenu dans chaque frame.</span><span class="sxs-lookup"><span data-stu-id="2adf1-282">These forward-predicted poses are best used for **rendering** the controller or a held object each frame.</span></span>  <span data-ttu-id="2adf1-283">Si vous ciblez une pression ou une mise en route donnée avec le contrôleur, celles-ci seront plus précises si vous utilisez les API d’événements historiques décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2adf1-283">If you are targeting a given press or release with the controller, that will be most accurate if you use the historical event APIs described below.</span></span>

   ```cs
   var sourcePose = interactionSourceState.sourcePose;
   Vector3 sourceGripPosition;
   Quaternion sourceGripRotation;
   if ((sourcePose.TryGetPosition(out sourceGripPosition, InteractionSourceNode.Grip)) &&
       (sourcePose.TryGetRotation(out sourceGripRotation, InteractionSourceNode.Grip))) {
       // ...
   }
   ```

* <span data-ttu-id="2adf1-284">Vous pouvez également obtenir la pose de tête préprédite pour ce frame actuel.</span><span class="sxs-lookup"><span data-stu-id="2adf1-284">You can also get the forward-predicted head pose for this current frame.</span></span>  <span data-ttu-id="2adf1-285">Comme avec la source, cela est utile pour le **rendu** d’un curseur, bien que le ciblage d’une presse ou d’une version donnée soit plus précis si vous utilisez les API d’événements historiques décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2adf1-285">As with the source pose, this is useful for **rendering** a cursor, although targeting a given press or release will be most accurate if you use the historical event APIs described below.</span></span>

   ```cs
   var headPose = interactionSourceState.headPose;
   var headRay = new Ray(headPose.position, headPose.forward);
   RaycastHit raycastHit;
   if (Physics.Raycast(headPose.position, headPose.forward, out raycastHit, 10)) {
       var cursorPos = raycastHit.point;
       // ...
   }
   ```

### <a name="handling-interaction-source-events"></a><span data-ttu-id="2adf1-286">Gestion des événements de source d’interaction</span><span class="sxs-lookup"><span data-stu-id="2adf1-286">Handling interaction source events</span></span>

<span data-ttu-id="2adf1-287">Pour gérer les événements d’entrée à mesure qu’ils se produisent avec leurs données d’historique exactes, vous pouvez gérer les événements de source d’interaction au lieu d’interroger.</span><span class="sxs-lookup"><span data-stu-id="2adf1-287">To handle input events as they happen with their accurate historical pose data, you can handle interaction source events instead of polling.</span></span>

<span data-ttu-id="2adf1-288">Pour gérer les événements de source d’interaction :</span><span class="sxs-lookup"><span data-stu-id="2adf1-288">To handle interaction source events:</span></span>
* <span data-ttu-id="2adf1-289">Inscrivez-vous pour un événement d’entrée *InteractionManager* .</span><span class="sxs-lookup"><span data-stu-id="2adf1-289">Register for a *InteractionManager* input event.</span></span> <span data-ttu-id="2adf1-290">Pour chaque type d’événement d’interaction qui vous intéresse, vous devez vous y abonner.</span><span class="sxs-lookup"><span data-stu-id="2adf1-290">For each type of interaction event that you are interested in, you need to subscribe to it.</span></span>

   ```cs
   InteractionManager.InteractionSourcePressed += InteractionManager_InteractionSourcePressed;
   ```
   
* <span data-ttu-id="2adf1-291">Gérez l’événement.</span><span class="sxs-lookup"><span data-stu-id="2adf1-291">Handle the event.</span></span> <span data-ttu-id="2adf1-292">Une fois que vous êtes abonné à un événement d’interaction, vous obtiendrez le rappel le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="2adf1-292">Once you have subscribed to an interaction event, you will get the callback when appropriate.</span></span> <span data-ttu-id="2adf1-293">Dans l’exemple *SourcePressed* , c’est une fois que la source a été détectée et avant qu’elle soit libérée ou perdue.</span><span class="sxs-lookup"><span data-stu-id="2adf1-293">In the *SourcePressed* example, this will be after the source was detected and before it is released or lost.</span></span>

   ```cs
   void InteractionManager_InteractionSourceDetected(InteractionSourceDetectedEventArgs args)
       var interactionSourceState = args.state;
       
       // args.state has information about:
          // targeting head ray at the time when the event was triggered
          // whether the source is pressed or not
          // properties like position, velocity, source loss risk
          // source id (which hand id for example) and source kind like hand, voice, controller or other
   }
   ```

### <a name="how-to-stop-handling-an-event"></a><span data-ttu-id="2adf1-294">Comment arrêter la gestion d’un événement</span><span class="sxs-lookup"><span data-stu-id="2adf1-294">How to stop handling an event</span></span>

<span data-ttu-id="2adf1-295">Vous devez arrêter la gestion d’un événement lorsque vous n’êtes plus intéressé par l’événement ou si vous détruisez l’objet qui s’est abonné à l’événement.</span><span class="sxs-lookup"><span data-stu-id="2adf1-295">You need to stop handling an event when you are no longer interested in the event or you are destroying the object that has subscribed to the event.</span></span> <span data-ttu-id="2adf1-296">Pour arrêter la gestion de l’événement, vous devez vous désabonner de l’événement.</span><span class="sxs-lookup"><span data-stu-id="2adf1-296">To stop handling the event, you unsubscribe from the event.</span></span>

```cs
InteractionManager.InteractionSourcePressed -= InteractionManager_InteractionSourcePressed;
```

### <a name="list-of-interaction-source-events"></a><span data-ttu-id="2adf1-297">Liste des événements de source d’interaction</span><span class="sxs-lookup"><span data-stu-id="2adf1-297">List of interaction source events</span></span>

<span data-ttu-id="2adf1-298">Les événements de la source d’interaction disponibles sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="2adf1-298">The available interaction source events are:</span></span>
* <span data-ttu-id="2adf1-299">*InteractionSourceDetected* (la source devient active)</span><span class="sxs-lookup"><span data-stu-id="2adf1-299">*InteractionSourceDetected* (source becomes active)</span></span>
* <span data-ttu-id="2adf1-300">*InteractionSourceLost* (devient inactif)</span><span class="sxs-lookup"><span data-stu-id="2adf1-300">*InteractionSourceLost* (becomes inactive)</span></span>
* <span data-ttu-id="2adf1-301">*InteractionSourcePressed* (appuyez sur, appuyez sur le bouton ou sélectionnez « Sélectionner »)</span><span class="sxs-lookup"><span data-stu-id="2adf1-301">*InteractionSourcePressed* (tap, button press, or "Select" uttered)</span></span>
* <span data-ttu-id="2adf1-302">*InteractionSourceReleased* (fin d’un TAP, d’un bouton relâché ou d’une fin de « SELECT »)</span><span class="sxs-lookup"><span data-stu-id="2adf1-302">*InteractionSourceReleased* (end of a tap, button released, or end of "Select" uttered)</span></span>
* <span data-ttu-id="2adf1-303">*InteractionSourceUpdated* (déplace ou change un État)</span><span class="sxs-lookup"><span data-stu-id="2adf1-303">*InteractionSourceUpdated* (moves or otherwise changes some state)</span></span>

### <a name="events-for-historical-targeting-poses-that-most-accurately-match-a-press-or-release"></a><span data-ttu-id="2adf1-304">Les événements pour le ciblage historique posent qui correspondent le plus précisément à une pression ou à une mise en sortie</span><span class="sxs-lookup"><span data-stu-id="2adf1-304">Events for historical targeting poses that most accurately match a press or release</span></span>

<span data-ttu-id="2adf1-305">Les API d’interrogation décrites précédemment fournissent à votre application des poses préprédits.</span><span class="sxs-lookup"><span data-stu-id="2adf1-305">The polling APIs described earlier give your app forward-predicted poses.</span></span>  <span data-ttu-id="2adf1-306">Bien que ces éléments prédits soient les plus adaptés pour le rendu du contrôleur ou d’un objet de poche virtuel, les nouvelles poses ne sont pas optimales pour le ciblage, pour deux raisons principales :</span><span class="sxs-lookup"><span data-stu-id="2adf1-306">While those predicted poses are best for rendering the controller or a virtual handheld object, future poses are not optimal for targeting, for two key reasons:</span></span>
* <span data-ttu-id="2adf1-307">Quand l’utilisateur appuie sur un bouton sur un contrôleur, il peut y avoir environ 20 ms de latence sans fil sur Bluetooth avant que le système ne reçoive la presse.</span><span class="sxs-lookup"><span data-stu-id="2adf1-307">When the user presses a button on a controller, there can be about 20ms of wireless latency over Bluetooth before the system receives the press.</span></span>
* <span data-ttu-id="2adf1-308">Ensuite, si vous utilisez une pose préprédite, il y aura une autre 20 ms de prédiction directe appliquée pour cibler le moment où les photons du frame actuel atteindront les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2adf1-308">Then, if you are using a forward-predicted pose, there would be another 10-20ms of forward prediction applied to target the time when the current frame's photons will reach the user's eyes.</span></span>

<span data-ttu-id="2adf1-309">Cela signifie que l’interrogation vous donne une source de pose ou de tête qui est de 30-40ms à partir de là où la tête et la mains de l’utilisateur ont été retirées lorsque l’appui ou la mise en place a eu lieu.</span><span class="sxs-lookup"><span data-stu-id="2adf1-309">This means that polling gives you a source pose or head pose that is 30-40ms forward from where the user's head and hands actually were back when the press or release happened.</span></span>  <span data-ttu-id="2adf1-310">Pour l’entrée de la main HoloLens, bien qu’il n’y ait pas de délai de transmission sans fil, il existe un délai de traitement similaire pour détecter la presse.</span><span class="sxs-lookup"><span data-stu-id="2adf1-310">For HoloLens hand input, while there's no wireless transmission delay, there is a similar processing delay to detect the press.</span></span>

<span data-ttu-id="2adf1-311">Pour cibler avec précision en fonction de l’intention initiale de l’utilisateur pour une presse ou un contrôleur, vous devez utiliser la base de l’historique de la source ou de l’en-tête à partir de cet événement d’entrée *InteractionSourcePressed* ou *InteractionSourceReleased* .</span><span class="sxs-lookup"><span data-stu-id="2adf1-311">To accurately target based on the user's original intent for a hand or controller press, you should use the historical source pose or head pose from that *InteractionSourcePressed* or *InteractionSourceReleased* input event.</span></span>

<span data-ttu-id="2adf1-312">Vous pouvez cibler une presse ou une mise en route avec des données de pose historiques à partir de la tête de l’utilisateur ou de son contrôleur :</span><span class="sxs-lookup"><span data-stu-id="2adf1-312">You can target a press or release with historical pose data from the user's head or their controller:</span></span>
* <span data-ttu-id="2adf1-313">L’en-tête pose au moment où un mouvement ou un contrôleur s’est produit, ce qui peut être utilisé pour **cibler** pour déterminer à quoi l’utilisateur a [Gazing](gaze-and-commit.md) :</span><span class="sxs-lookup"><span data-stu-id="2adf1-313">The head pose at the moment in time when a gesture or controller press occurred, which can be used for **targeting** to determine what the user was [gazing](gaze-and-commit.md) at:</span></span>

   ```cs
   void InteractionManager_InteractionSourcePressed(InteractionSourcePressedEventArgs args) {
       var interactionSourceState = args.state;
       var headPose = interactionSourceState.headPose;
       RaycastHit raycastHit;
       if (Physics.Raycast(headPose.position, headPose.forward, out raycastHit, 10)) {
           var targetObject = raycastHit.collider.gameObject;
           // ...
       }
   }
   ```

* <span data-ttu-id="2adf1-314">La source pose au moment où une pression du contrôleur de mouvement s’est produite, qui peut être utilisée pour le **ciblage** afin de déterminer le point de contrôle de l’utilisateur sur le contrôleur.</span><span class="sxs-lookup"><span data-stu-id="2adf1-314">The source pose at the moment in time when a motion controller press occurred, which can be used for **targeting** to determine what the user was pointing the controller at.</span></span>  <span data-ttu-id="2adf1-315">Il s’agit de l’état du contrôleur qui a rencontré la presse.</span><span class="sxs-lookup"><span data-stu-id="2adf1-315">This will be the state of the controller that experienced the press.</span></span>  <span data-ttu-id="2adf1-316">Si vous effectuez le rendu du contrôleur lui-même, vous pouvez demander le point de pose plutôt que le pose de la poignée pour faire tourner le ciblage de la cible à partir de ce que l’utilisateur prendra en compte l’astuce naturelle de ce contrôleur rendu :</span><span class="sxs-lookup"><span data-stu-id="2adf1-316">If you are rendering the controller itself, you can request the pointer pose rather than the grip pose, to shoot the targeting ray from what the user will consider the natural tip of that rendered controller:</span></span>

   ```cs
   void InteractionManager_InteractionSourcePressed(InteractionSourcePressedEventArgs args)
   {
       var interactionSourceState = args.state;
       var sourcePose = interactionSourceState.sourcePose;
       Vector3 sourceGripPosition;
       Quaternion sourceGripRotation;
       if ((sourcePose.TryGetPosition(out sourceGripPosition, InteractionSourceNode.Pointer)) &&
           (sourcePose.TryGetRotation(out sourceGripRotation, InteractionSourceNode.Pointer))) {
           RaycastHit raycastHit;
           if (Physics.Raycast(sourceGripPosition, sourceGripRotation * Vector3.forward, out raycastHit, 10)) {
               var targetObject = raycastHit.collider.gameObject;
               // ...
           }
       }
   }
   ```

### <a name="event-handlers-example"></a><span data-ttu-id="2adf1-317">Exemple de gestionnaires d’événements</span><span class="sxs-lookup"><span data-stu-id="2adf1-317">Event handlers example</span></span>

```cs
using UnityEngine.XR.WSA.Input;

void Start()
{
    InteractionManager.InteractionSourceDetected += InteractionManager_InteractionSourceDetected;
    InteractionManager.InteractionSourceLost += InteractionManager_InteractionSourceLost;
    InteractionManager.InteractionSourcePressed += InteractionManager_InteractionSourcePressed;
    InteractionManager.InteractionSourceReleased += InteractionManager_InteractionSourceReleased;
    InteractionManager.InteractionSourceUpdated += InteractionManager_InteractionSourceUpdated;
}

void OnDestroy()
{
    InteractionManager.InteractionSourceDetected -= InteractionManager_InteractionSourceDetected;
    InteractionManager.InteractionSourceLost -= InteractionManager_InteractionSourceLost;
    InteractionManager.InteractionSourcePressed -= InteractionManager_InteractionSourcePressed;
    InteractionManager.InteractionSourceReleased -= InteractionManager_InteractionSourceReleased;
    InteractionManager.InteractionSourceUpdated -= InteractionManager_InteractionSourceUpdated;
}

void InteractionManager_InteractionSourceDetected(InteractionSourceDetectedEventArgs args)
{
    // Source was detected
    // args.state has the current state of the source including id, position, kind, etc.
}

void InteractionManager_InteractionSourceLost(InteractionSourceLostEventArgs state)
{
    // Source was lost. This will be after a SourceDetected event and no other events for this
    // source id will occur until it is Detected again
    // args.state has the current state of the source including id, position, kind, etc.
}

void InteractionManager_InteractionSourcePressed(InteractionSourcePressedEventArgs state)
{
    // Source was pressed. This will be after the source was detected and before it is 
    // released or lost
    // args.state has the current state of the source including id, position, kind, etc.
}

void InteractionManager_InteractionSourceReleased(InteractionSourceReleasedEventArgs state)
{
    // Source was released. The source would have been detected and pressed before this point. 
    // This event will not fire if the source is lost
    // args.state has the current state of the source including id, position, kind, etc.
}

void InteractionManager_InteractionSourceUpdated(InteractionSourceUpdatedEventArgs state)
{
    // Source was updated. The source would have been detected before this point
    // args.state has the current state of the source including id, position, kind, etc.
}
```

## <a name="high-level-composite-gesture-apis-gesturerecognizer"></a><span data-ttu-id="2adf1-318">API de mouvement composite de haut niveau (GestureRecognizer)</span><span class="sxs-lookup"><span data-stu-id="2adf1-318">High-level composite gesture APIs (GestureRecognizer)</span></span>

<span data-ttu-id="2adf1-319">**Espace de noms :** *UnityEngine. XR. WSA. Input*</span><span class="sxs-lookup"><span data-stu-id="2adf1-319">**Namespace:** *UnityEngine.XR.WSA.Input*</span></span><br>
<span data-ttu-id="2adf1-320">**Types**: *GestureRecognizer*, *GestureSettings*, *InteractionSourceKind*</span><span class="sxs-lookup"><span data-stu-id="2adf1-320">**Types**: *GestureRecognizer*, *GestureSettings*, *InteractionSourceKind*</span></span>

<span data-ttu-id="2adf1-321">Votre application peut également reconnaître les gestes composites de niveau supérieur pour les sources d’entrée spatiale, le TAP, le maintien, la manipulation et les gestes de navigation.</span><span class="sxs-lookup"><span data-stu-id="2adf1-321">Your app can also recognize higher-level composite gestures for spatial input sources, Tap, Hold, Manipulation and Navigation gestures.</span></span> <span data-ttu-id="2adf1-322">Vous pouvez reconnaître ces gestes composites sur les [mains](gaze-and-commit.md#composite-gestures) et les [contrôleurs de mouvement](motion-controllers.md) à l’aide de GestureRecognizer.</span><span class="sxs-lookup"><span data-stu-id="2adf1-322">You can recognize these composite gestures across both [hands](gaze-and-commit.md#composite-gestures) and [motion controllers](motion-controllers.md) using the GestureRecognizer.</span></span>

<span data-ttu-id="2adf1-323">Chaque événement de mouvement sur le GestureRecognizer fournit le SourceKind pour l’entrée, ainsi que le rayon de l’en-tête de ciblage au moment de l’événement.</span><span class="sxs-lookup"><span data-stu-id="2adf1-323">Each Gesture event on the GestureRecognizer provides the SourceKind for the input as well as the targeting head ray at the time of the event.</span></span> <span data-ttu-id="2adf1-324">Certains événements fournissent des informations spécifiques au contexte.</span><span class="sxs-lookup"><span data-stu-id="2adf1-324">Some events provide additional context specific information.</span></span>

<span data-ttu-id="2adf1-325">Seules quelques étapes sont requises pour capturer des mouvements à l’aide d’un module de reconnaissance de mouvement :</span><span class="sxs-lookup"><span data-stu-id="2adf1-325">There are only a few steps required to capture gestures using a Gesture Recognizer:</span></span>
1. <span data-ttu-id="2adf1-326">Créer un module de reconnaissance de mouvement</span><span class="sxs-lookup"><span data-stu-id="2adf1-326">Create a new Gesture Recognizer</span></span>
2. <span data-ttu-id="2adf1-327">Spécifier les gestes à surveiller</span><span class="sxs-lookup"><span data-stu-id="2adf1-327">Specify which gestures to watch for</span></span>
3. <span data-ttu-id="2adf1-328">S’abonner à des événements pour ces mouvements</span><span class="sxs-lookup"><span data-stu-id="2adf1-328">Subscribe to events for those gestures</span></span>
4. <span data-ttu-id="2adf1-329">Démarrer la capture des mouvements</span><span class="sxs-lookup"><span data-stu-id="2adf1-329">Start capturing gestures</span></span>

### <a name="create-a-new-gesture-recognizer"></a><span data-ttu-id="2adf1-330">Créer un module de reconnaissance de mouvement</span><span class="sxs-lookup"><span data-stu-id="2adf1-330">Create a new Gesture Recognizer</span></span>

<span data-ttu-id="2adf1-331">Pour utiliser *GestureRecognizer*, vous devez avoir créé un *GestureRecognizer*:</span><span class="sxs-lookup"><span data-stu-id="2adf1-331">To use the *GestureRecognizer*, you must have created a *GestureRecognizer*:</span></span>

```cs
GestureRecognizer recognizer = new GestureRecognizer();
```

### <a name="specify-which-gestures-to-watch-for"></a><span data-ttu-id="2adf1-332">Spécifier les gestes à surveiller</span><span class="sxs-lookup"><span data-stu-id="2adf1-332">Specify which gestures to watch for</span></span>

<span data-ttu-id="2adf1-333">Spécifiez les gestes qui vous intéressent via *SetRecognizableGestures ()* :</span><span class="sxs-lookup"><span data-stu-id="2adf1-333">Specify which gestures you are interested in via *SetRecognizableGestures()*:</span></span>

```cs
recognizer.SetRecognizableGestures(GestureSettings.Tap | GestureSettings.Hold);
```

### <a name="subscribe-to-events-for-those-gestures"></a><span data-ttu-id="2adf1-334">S’abonner à des événements pour ces mouvements</span><span class="sxs-lookup"><span data-stu-id="2adf1-334">Subscribe to events for those gestures</span></span>

<span data-ttu-id="2adf1-335">Abonnez-vous aux événements pour les mouvements qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="2adf1-335">Subscribe to events for the gestures you are interested in.</span></span>

```cs
void Start()
{
    recognizer.Tapped += GestureRecognizer_Tapped;
    recognizer.HoldStarted += GestureRecognizer_HoldStarted;
    recognizer.HoldCompleted += GestureRecognizer_HoldCompleted;
    recognizer.HoldCanceled += GestureRecognizer_HoldCanceled;
}
```

>[!NOTE]
><span data-ttu-id="2adf1-336">Les mouvements de navigation et de manipulation s’excluent mutuellement sur une instance d’un *GestureRecognizer*.</span><span class="sxs-lookup"><span data-stu-id="2adf1-336">Navigation and Manipulation gestures are mutually exclusive on an instance of a *GestureRecognizer*.</span></span>

### <a name="start-capturing-gestures"></a><span data-ttu-id="2adf1-337">Démarrer la capture des mouvements</span><span class="sxs-lookup"><span data-stu-id="2adf1-337">Start capturing gestures</span></span>

<span data-ttu-id="2adf1-338">Par défaut, un *GestureRecognizer* ne surveille pas l’entrée tant que *StartCapturingGestures ()* n’est pas appelé.</span><span class="sxs-lookup"><span data-stu-id="2adf1-338">By default, a *GestureRecognizer* does not monitor input until *StartCapturingGestures()* is called.</span></span> <span data-ttu-id="2adf1-339">Il est possible qu’un événement de mouvement soit généré après l’appel de *StopCapturingGestures ()* si l’entrée a été effectuée avant le frame dans lequel *StopCapturingGestures ()* a été traité.</span><span class="sxs-lookup"><span data-stu-id="2adf1-339">It is possible that a gesture event may be generated after *StopCapturingGestures()* is called if input was performed before the frame where *StopCapturingGestures()* was processed.</span></span> <span data-ttu-id="2adf1-340">Le *GestureRecognizer* se souvient s’il était activé ou désactivé pendant l’image précédente dans laquelle le mouvement s’est réellement produit. il est donc fiable pour démarrer et arrêter la surveillance des mouvements en fonction du point de vue du regard de ce frame.</span><span class="sxs-lookup"><span data-stu-id="2adf1-340">The *GestureRecognizer* will remember whether it was on or off during the previous frame in which the gesture actually occurred, and so it is reliable to start and stop gesture monitoring based on this frame's gaze targeting.</span></span>

```cs
recognizer.StartCapturingGestures();
```

### <a name="stop-capturing-gestures"></a><span data-ttu-id="2adf1-341">Arrêter la capture des mouvements</span><span class="sxs-lookup"><span data-stu-id="2adf1-341">Stop capturing gestures</span></span>

<span data-ttu-id="2adf1-342">Pour arrêter la reconnaissance des mouvements :</span><span class="sxs-lookup"><span data-stu-id="2adf1-342">To stop gesture recognition:</span></span>

```cs
recognizer.StopCapturingGestures();
```

### <a name="removing-a-gesture-recognizer"></a><span data-ttu-id="2adf1-343">Suppression d’un module de reconnaissance de mouvement</span><span class="sxs-lookup"><span data-stu-id="2adf1-343">Removing a gesture recognizer</span></span>

<span data-ttu-id="2adf1-344">N’oubliez pas de vous désabonner des événements souscrits avant de détruire un objet *GestureRecognizer* .</span><span class="sxs-lookup"><span data-stu-id="2adf1-344">Remember to unsubscribe from subscribed events before destroying a *GestureRecognizer* object.</span></span>

```cs
void OnDestroy()
{
    recognizer.Tapped -= GestureRecognizer_Tapped;
    recognizer.HoldStarted -= GestureRecognizer_HoldStarted;
    recognizer.HoldCompleted -= GestureRecognizer_HoldCompleted;
    recognizer.HoldCanceled -= GestureRecognizer_HoldCanceled;
}
```

## <a name="rendering-the-motion-controller-model-in-unity"></a><span data-ttu-id="2adf1-345">Rendu du modèle de contrôleur de mouvement dans Unity</span><span class="sxs-lookup"><span data-stu-id="2adf1-345">Rendering the motion controller model in Unity</span></span>

<span data-ttu-id="2adf1-346">![modèle de contrôleur de mouvement et](images/motioncontrollertest-teleport-1000px.png) de téléportage</span><span class="sxs-lookup"><span data-stu-id="2adf1-346">![Motion Controller model and teleportation](images/motioncontrollertest-teleport-1000px.png)</span></span><br>
<span data-ttu-id="2adf1-347">*Modèle de contrôleur de mouvement et téléportage*</span><span class="sxs-lookup"><span data-stu-id="2adf1-347">*Motion controller model and teleportation*</span></span>

<span data-ttu-id="2adf1-348">Pour afficher les contrôleurs de mouvement de votre application qui correspondent aux contrôleurs physiques que vos utilisateurs détiennent et qui s’articulent à mesure que les différents boutons sont enfoncés, vous pouvez utiliser la **Prefab MotionController** dans le [Toolkit de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity/).</span><span class="sxs-lookup"><span data-stu-id="2adf1-348">To render motion controllers in your app that match the physical controllers your users are holding and articulate as various buttons are pressed, you can use the **MotionController prefab** in the [Mixed Reality Toolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/).</span></span>  <span data-ttu-id="2adf1-349">Ce Prefab charge dynamiquement le modèle glTF correct au moment de l’exécution à partir du pilote du contrôleur de mouvement installé du système.</span><span class="sxs-lookup"><span data-stu-id="2adf1-349">This prefab dynamically loads the correct glTF model at runtime from the system's installed motion controller driver.</span></span>  <span data-ttu-id="2adf1-350">Il est important de charger ces modèles de manière dynamique plutôt que de les importer manuellement dans l’éditeur, afin que votre application affiche des modèles 3D physiquement précis pour tous les contrôleurs actuels et futurs que vos utilisateurs peuvent avoir.</span><span class="sxs-lookup"><span data-stu-id="2adf1-350">It's important to load these models dynamically rather than importing them manually in the editor, so that your app will show physically accurate 3D models for any current and future controllers your users may have.</span></span>

1. <span data-ttu-id="2adf1-351">Suivez les instructions [prise en main](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/GettingStarted.md) pour télécharger la boîte à outils de réalité mixte et l’ajouter à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="2adf1-351">Follow the [Getting Started](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/GettingStarted.md) instructions to download the Mixed Reality Toolkit and add it to your Unity project.</span></span>
2. <span data-ttu-id="2adf1-352">Si vous avez remplacé votre appareil photo par le *MixedRealityCameraParent* Prefab dans le cadre des étapes de prise en main, vous êtes en déplacement.</span><span class="sxs-lookup"><span data-stu-id="2adf1-352">If you replaced your camera with the *MixedRealityCameraParent* prefab as part of the Getting Started steps, you're good to go!</span></span>  <span data-ttu-id="2adf1-353">Prefab comprend le rendu du contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="2adf1-353">That prefab includes motion controller rendering.</span></span>  <span data-ttu-id="2adf1-354">Sinon, ajoutez *Assets/HoloToolkit/Input/Prefabs/MotionControllers. Prefab* à votre scène à partir du volet de projet.</span><span class="sxs-lookup"><span data-stu-id="2adf1-354">Otherwise, add *Assets/HoloToolkit/Input/Prefabs/MotionControllers.prefab* into your scene from the Project pane.</span></span>  <span data-ttu-id="2adf1-355">Vous pouvez ajouter ce Prefab en tant qu’enfant de n’importe quel objet parent que vous utilisez pour déplacer la caméra lorsque l’utilisateur téléporte dans votre scène, afin que les contrôleurs soient fournis avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2adf1-355">You'll want to add that prefab as a child of whatever parent object you use to move the camera around when the user teleports within your scene, so that the controllers come along with the user.</span></span>  <span data-ttu-id="2adf1-356">Si votre application n’implique pas de téléportage, ajoutez simplement le Prefab à la racine de votre scène.</span><span class="sxs-lookup"><span data-stu-id="2adf1-356">If your app does not involve teleporting, just add the prefab at the root of your scene.</span></span>

## <a name="throwing-objects"></a><span data-ttu-id="2adf1-357">Lever des objets</span><span class="sxs-lookup"><span data-stu-id="2adf1-357">Throwing objects</span></span>

<span data-ttu-id="2adf1-358">La levée d’objets dans la réalité virtuelle est un problème plus difficile, alors il peut sembler évident.</span><span class="sxs-lookup"><span data-stu-id="2adf1-358">Throwing objects in virtual reality is a harder problem then it may at first seem.</span></span> <span data-ttu-id="2adf1-359">Comme avec la plupart des interactions basées physiquement, lorsque la levée dans le jeu se fait de manière inattendue, elle est immédiatement évidente et s’arrête à l’immersion.</span><span class="sxs-lookup"><span data-stu-id="2adf1-359">As with most physically based interactions, when throwing in game acts in an unexpected way, it is immediately obvious and breaks immersion.</span></span> <span data-ttu-id="2adf1-360">Nous avons passé un peu de temps à réfléchir à la façon de représenter un comportement de levée de manière physique et à rencontrer quelques recommandations, activées par le biais de mises à jour de notre plateforme, que nous aimerions partager avec vous.</span><span class="sxs-lookup"><span data-stu-id="2adf1-360">We have spent some time thinking deeply about how to represent a physically correct throwing behavior, and have come up with a few guidelines, enabled through updates to our platform, that we would like to share with you.</span></span>

<span data-ttu-id="2adf1-361">Vous trouverez un exemple de la façon dont nous vous recommandons d’implémenter la levée [ici](https://github.com/keluecke/MixedRealityToolkit-Unity/blob/master/External/Unitypackages/ThrowingStarter.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="2adf1-361">You can find an example of how we recommend to implement throwing [here](https://github.com/keluecke/MixedRealityToolkit-Unity/blob/master/External/Unitypackages/ThrowingStarter.unitypackage).</span></span> <span data-ttu-id="2adf1-362">Cet exemple suit les quatre instructions suivantes :</span><span class="sxs-lookup"><span data-stu-id="2adf1-362">This sample follows these four guidelines:</span></span>
* <span data-ttu-id="2adf1-363">**Utilisez la *vélocité* du contrôleur au lieu de la position**.</span><span class="sxs-lookup"><span data-stu-id="2adf1-363">**Use the controller’s *velocity* instead of position**.</span></span> <span data-ttu-id="2adf1-364">Dans la mise à jour de novembre de Windows, nous avons introduit un changement de comportement dans l' [État de suivi positionnel « approximatif](motion-controllers.md#controller-tracking-state)».</span><span class="sxs-lookup"><span data-stu-id="2adf1-364">In the November update to Windows, we introduced a change in behavior when in the [''Approximate'' positional tracking state](motion-controllers.md#controller-tracking-state).</span></span> <span data-ttu-id="2adf1-365">Dans cet État, les informations de vélocité sur le contrôleur continuent d’être signalées aussi longtemps que nous pensons qu’il s’agit d’une précision élevée, qui est souvent plus longue que la position reste une précision élevée.</span><span class="sxs-lookup"><span data-stu-id="2adf1-365">When in this state, velocity information about the controller will continue to be reported for as long as we believe it is high accuracy, which is often longer than position remains high accuracy.</span></span>
* <span data-ttu-id="2adf1-366">**Incorporez la *vélocité angulaire* du contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="2adf1-366">**Incorporate the *angular velocity* of the controller**.</span></span> <span data-ttu-id="2adf1-367">Cette logique est contenue dans le fichier `throwing.cs` de la méthode statique `GetThrownObjectVelAngVel`, au sein du package lié ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="2adf1-367">This logic is all contained in the `throwing.cs` file in the `GetThrownObjectVelAngVel` static method, within the package linked above:</span></span>
   1. <span data-ttu-id="2adf1-368">Comme la vélocité angulaire est conservée, l’objet levé doit conserver la même vélocité angulaire qu’au moment de la levée : `objectAngularVelocity = throwingControllerAngularVelocity;`</span><span class="sxs-lookup"><span data-stu-id="2adf1-368">As angular velocity is conserved, the thrown object must maintain the same angular velocity as it had at the moment of the throw: `objectAngularVelocity = throwingControllerAngularVelocity;`</span></span>
   2. <span data-ttu-id="2adf1-369">Comme le centre de la masse de l’objet levé n’est probablement pas à l’origine de la poignée, il a probablement une vélocité différente de celle du contrôleur dans le cadre de référence de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2adf1-369">As the center of mass of the thrown object is likely not at the origin of the grip pose, it likely has a different velocity then that of the controller in the frame of reference of the user.</span></span> <span data-ttu-id="2adf1-370">La partie de la rapidité de l’objet utilisée de cette façon est la vélocité tangentielle instantanée du centre de la masse de l’objet levé autour de l’origine du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="2adf1-370">The portion of the object’s velocity contributed in this way is the instantaneous tangential velocity of the center of mass of the thrown object around the controller origin.</span></span> <span data-ttu-id="2adf1-371">Cette vélocité tangentielle est le produit croisé de la vélocité angulaire du contrôleur avec le vecteur représentant la distance entre l’origine du contrôleur et le centre de la masse de l’objet levé.</span><span class="sxs-lookup"><span data-stu-id="2adf1-371">This tangential velocity is the cross product of the angular velocity of the controller with the vector representing the distance between the controller origin and the center of mass of the thrown object.</span></span>
    
      ```cs
      Vector3 radialVec = thrownObjectCenterOfMass - throwingControllerPos;
      Vector3 tangentialVelocity = Vector3.Cross(throwingControllerAngularVelocity, radialVec);
      ```
   
   3. <span data-ttu-id="2adf1-372">La rapidité totale de l’objet levé est donc la somme de la vélocité du contrôleur et de cette vélocité tangentielle : `objectVelocity = throwingControllerVelocity + tangentialVelocity;`</span><span class="sxs-lookup"><span data-stu-id="2adf1-372">The total velocity of the thrown object is thus the sum of velocity of the controller and this tangential velocity: `objectVelocity = throwingControllerVelocity + tangentialVelocity;`</span></span>

* <span data-ttu-id="2adf1-373">**Portez une attention particulière à l' *heure* à laquelle nous appliquons la vélocité**.</span><span class="sxs-lookup"><span data-stu-id="2adf1-373">**Pay close attention to the *time* at which we apply the velocity**.</span></span> <span data-ttu-id="2adf1-374">Quand vous appuyez sur un bouton, il peut s’écouler jusqu’à 20 ms pour que cet événement se propage via Bluetooth au système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="2adf1-374">When a button is pressed, it can take up to 20ms for that event to bubble up through Bluetooth to the operating system.</span></span> <span data-ttu-id="2adf1-375">Cela signifie que si vous interrogez le changement d’état d’un contrôleur en l’appuyant sur non enfoncé, ou vice versa, le contrôleur vous pose les informations dont vous bénéficiez en effet.</span><span class="sxs-lookup"><span data-stu-id="2adf1-375">This means that if you poll for a controller state change from pressed to not pressed or vice versa, the controller pose information you get with it will actually be ahead of this change in state.</span></span> <span data-ttu-id="2adf1-376">En outre, le contrôleur présenté par notre API d’interrogation est Forward prédit pour refléter une situation probable au moment où l’image sera affichée, ce qui pourrait être plus 20 ms à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="2adf1-376">Further, the controller pose presented by our polling API is forward predicted to reflect a likely pose at the time the frame will be displayed which could be more then 20ms in the future.</span></span> <span data-ttu-id="2adf1-377">Cela est idéal pour le *rendu* des objets maintenus, mais il compose notre problème de temps pour *cibler* l’objet à mesure que nous calculons la trajectoire pour le moment où l’utilisateur a relâché sa levée.</span><span class="sxs-lookup"><span data-stu-id="2adf1-377">This is good for *rendering* held objects, but compounds our time problem for *targeting* the object as we calculate the trajectory for the moment the user released their throw.</span></span> <span data-ttu-id="2adf1-378">Heureusement, avec la mise à jour de novembre, lors de l’envoi d’un événement Unity comme *InteractionSourcePressed* ou *InteractionSourceReleased* , l’État comprend les données d’historique de la pose lorsque le bouton a été enfoncé ou relâché.</span><span class="sxs-lookup"><span data-stu-id="2adf1-378">Fortunately, with the November update, when a Unity event like *InteractionSourcePressed* or *InteractionSourceReleased* is sent, the state includes the historical pose data from back when the button was actually pressed or released.</span></span>  <span data-ttu-id="2adf1-379">Pour optimiser le rendu du contrôleur et le ciblage du contrôleur lors des levées, vous devez utiliser correctement l’interrogation et l’événement, selon le cas :</span><span class="sxs-lookup"><span data-stu-id="2adf1-379">To get the most accurate controller rendering and controller targeting during throws, you must correctly use polling and eventing, as appropriate:</span></span>
   * <span data-ttu-id="2adf1-380">Pour le rendu de chaque trame par le **contrôleur** , votre application doit positionner les *gameobject* du contrôleur au niveau du contrôleur avant prédiction pour le temps des photons du frame actuel.</span><span class="sxs-lookup"><span data-stu-id="2adf1-380">For **controller rendering** each frame, your app should position the controller's *GameObject* at the forward-predicted controller pose for the current frame’s photon time.</span></span>  <span data-ttu-id="2adf1-381">Vous recevez ces données à partir d’API d’interrogation Unity, telles que *[XR. InputTracking. GetLocalPosition](https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html)* ou *[XR. WSA. Entrez. InteractionManager. GetCurrentReading](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.GetCurrentReading.html)* .</span><span class="sxs-lookup"><span data-stu-id="2adf1-381">You get this data from Unity polling APIs like *[XR.InputTracking.GetLocalPosition](https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html)* or *[XR.WSA.Input.InteractionManager.GetCurrentReading](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.GetCurrentReading.html)*.</span></span>
   * <span data-ttu-id="2adf1-382">Pour le **ciblage du contrôleur** sur une presse ou une mise en sortie, votre application doit raycast et calculer des trajectoires en fonction de la pose du contrôleur historique pour cet événement Press ou Release.</span><span class="sxs-lookup"><span data-stu-id="2adf1-382">For **controller targeting** upon a press or release, your app should raycast and calculate trajectories based on the historical controller pose for that press or release event.</span></span>  <span data-ttu-id="2adf1-383">Vous recevez ces données à partir d’API d’événements Unity, telles que *[InteractionManager. InteractionSourcePressed](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.InteractionSourcePressed.html)* .</span><span class="sxs-lookup"><span data-stu-id="2adf1-383">You get this data from Unity eventing APIs, like *[InteractionManager.InteractionSourcePressed](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.InteractionSourcePressed.html)*.</span></span>
* <span data-ttu-id="2adf1-384">**Utilisez la poignée**.</span><span class="sxs-lookup"><span data-stu-id="2adf1-384">**Use the grip pose**.</span></span> <span data-ttu-id="2adf1-385">La rapidité et la vélocité angulaires sont rapportées par rapport à la pose de la poignée, et non à la pose du pointeur.</span><span class="sxs-lookup"><span data-stu-id="2adf1-385">Angular velocity and velocity are reported relative to the grip pose, not pointer pose.</span></span>

<span data-ttu-id="2adf1-386">La génération continuera à s’améliorer avec les futures mises à jour de Windows, et vous pouvez vous attendre à trouver plus d’informations ici.</span><span class="sxs-lookup"><span data-stu-id="2adf1-386">Throwing will continue to improve with future Windows updates, and you can expect to find more information on it here.</span></span>

## <a name="gesture-and-motion-controllers-in-mrtk-v2"></a><span data-ttu-id="2adf1-387">Contrôleurs de mouvement et de mouvement dans MRTK v2</span><span class="sxs-lookup"><span data-stu-id="2adf1-387">Gesture and Motion Controllers in MRTK v2</span></span>

<span data-ttu-id="2adf1-388">Vous pouvez accéder au contrôleur de mouvement et de mouvement à partir du gestionnaire d’entrée.</span><span class="sxs-lookup"><span data-stu-id="2adf1-388">You can access gesture and motion controller from the input Manager.</span></span> 
* [<span data-ttu-id="2adf1-389">Mouvement dans MRTK v2</span><span class="sxs-lookup"><span data-stu-id="2adf1-389">Gesture in MRTK v2</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Gestures.html)
* [<span data-ttu-id="2adf1-390">Contrôleur de mouvement dans MRTK v2</span><span class="sxs-lookup"><span data-stu-id="2adf1-390">Motion Controller in MRTK v2</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Controllers.html)


## <a name="follow-along-with-tutorials"></a><span data-ttu-id="2adf1-391">Suivre les didacticiels</span><span class="sxs-lookup"><span data-stu-id="2adf1-391">Follow along with tutorials</span></span>

<span data-ttu-id="2adf1-392">Des didacticiels pas à pas, avec des exemples de personnalisation plus détaillés, sont disponibles dans Mixed Reality Academy :</span><span class="sxs-lookup"><span data-stu-id="2adf1-392">Step-by-step tutorials, with more detailed customization examples, are available in the Mixed Reality Academy:</span></span>

- [<span data-ttu-id="2adf1-393">Entrée MR 211 : geste</span><span class="sxs-lookup"><span data-stu-id="2adf1-393">MR Input 211: Gesture</span></span>](holograms-211.md)
- [<span data-ttu-id="2adf1-394">Entrée MR 213 : contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="2adf1-394">MR Input 213: Motion controllers</span></span>](mixed-reality-213.md)

<span data-ttu-id="2adf1-395">[![MR entrée 213-contrôleur de mouvement](images/mr213-main-600px.jpg)](https://docs.microsoft.com/windows/mixed-reality/mixed-reality-213)</span><span class="sxs-lookup"><span data-stu-id="2adf1-395">[![MR Input 213 - Motion controller](images/mr213-main-600px.jpg)](https://docs.microsoft.com/windows/mixed-reality/mixed-reality-213)</span></span><br>
<span data-ttu-id="2adf1-396">*Entrée MR 213-contrôleur de mouvement*</span><span class="sxs-lookup"><span data-stu-id="2adf1-396">*MR Input 213 - Motion controller*</span></span>

## <a name="see-also"></a><span data-ttu-id="2adf1-397">Voir également</span><span class="sxs-lookup"><span data-stu-id="2adf1-397">See also</span></span>

* [<span data-ttu-id="2adf1-398">Pointer du regard vers l’avant et valider</span><span class="sxs-lookup"><span data-stu-id="2adf1-398">Head-gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="2adf1-399">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="2adf1-399">Motion controllers</span></span>](motion-controllers.md)


