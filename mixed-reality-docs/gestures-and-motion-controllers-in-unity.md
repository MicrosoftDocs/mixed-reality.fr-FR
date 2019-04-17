---
title: Mouvements et les contrôleurs de mouvement dans Unity
description: Il existe deux façons principales d’agir sur votre regard dans Unity, les mouvements de main et les contrôleurs de mouvement.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: mouvements, contrôleurs de mouvement, unity, regards, entrée
ms.openlocfilehash: d98590f9a6c40336a13cb75e8050e13edfaa2a6c
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593287"
---
# <a name="gestures-and-motion-controllers-in-unity"></a><span data-ttu-id="269de-104">Mouvements et les contrôleurs de mouvement dans Unity</span><span class="sxs-lookup"><span data-stu-id="269de-104">Gestures and motion controllers in Unity</span></span>

<span data-ttu-id="269de-105">Il existe deux façons principales d’agir votre [regards dans Unity](gaze-in-unity.md), [main mouvements](gestures.md) et [contrôleurs de mouvement](motion-controllers.md).</span><span class="sxs-lookup"><span data-stu-id="269de-105">There are two key ways to take action on your [gaze in Unity](gaze-in-unity.md), [hand gestures](gestures.md) and [motion controllers](motion-controllers.md).</span></span> <span data-ttu-id="269de-106">Vous accédez aux données pour les deux sources d’entrée spatiale via les mêmes API dans Unity.</span><span class="sxs-lookup"><span data-stu-id="269de-106">You access the data for both sources of spatial input through the same APIs in Unity.</span></span>

<span data-ttu-id="269de-107">Unity fournit deux méthodes principales pour accéder à des données spatiales d’entrée pour la réalité mixte Windows, courantes *Input.GetButton/Input.GetAxis* API capables de fonctionner sur plusieurs Unity XR kits de développement logiciel, et un *InteractionManager / GestureRecognizer* API spécifique à Windows Mixed Reality qui expose l’ensemble complet des données spatiales d’entrée disponibles.</span><span class="sxs-lookup"><span data-stu-id="269de-107">Unity provides two primary ways to access spatial input data for Windows Mixed Reality, the common *Input.GetButton/Input.GetAxis* APIs that work across multiple Unity XR SDKs, and an *InteractionManager/GestureRecognizer* API specific to Windows Mixed Reality that exposes the full set of spatial input data available.</span></span>

## <a name="unity-buttonaxis-mapping-table"></a><span data-ttu-id="269de-108">Table de mappage de bouton/axe Unity</span><span class="sxs-lookup"><span data-stu-id="269de-108">Unity button/axis mapping table</span></span>

<span data-ttu-id="269de-109">Les ID de bouton et d’axe dans le tableau ci-dessous sont prises en charge dans le Gestionnaire d’entrée de Unity pour les contrôleurs de mouvement de réalité mixte Windows par le biais du *Input.GetButton/GetAxis* API, tandis que la colonne « Windows MR spécifique » fait référence aux propriétés disponible issu de la *InteractionSourceState* type.</span><span class="sxs-lookup"><span data-stu-id="269de-109">The button and axis IDs in the table below are supported in Unity's Input Manager for Windows Mixed Reality motion controllers through the *Input.GetButton/GetAxis* APIs, while the "Windows MR-specific" column refers to properties available off of the *InteractionSourceState* type.</span></span> <span data-ttu-id="269de-110">Chacune de ces API sont décrites en détail dans les sections ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="269de-110">Each of these APIs are described in detail in the sections below.</span></span>

<span data-ttu-id="269de-111">Les mappages d’ID de bouton/axe pour la réalité mixte Windows correspond généralement à l’ID Oculus bouton/axe.</span><span class="sxs-lookup"><span data-stu-id="269de-111">The button/axis ID mappings for Windows Mixed Reality generally match the Oculus button/axis IDs.</span></span>

<span data-ttu-id="269de-112">Les mappages d’ID de bouton/axe pour la réalité mixte Windows diffèrent des mappages de OpenVR de deux manières :</span><span class="sxs-lookup"><span data-stu-id="269de-112">The button/axis ID mappings for Windows Mixed Reality differ from OpenVR's mappings in two ways:</span></span>
1. <span data-ttu-id="269de-113">Le mappage utilise des ID de pavé tactile qui diffèrent des stick analogique, pour prendre en charge des contrôleurs avec sticks analogiques et un pavé tactile.</span><span class="sxs-lookup"><span data-stu-id="269de-113">The mapping uses touchpad IDs that are distinct from thumbstick, to support controllers with both thumbsticks and touchpads.</span></span>
2. <span data-ttu-id="269de-114">Le mappage permet d’éviter la surcharge de l’ID pour les boutons de Menu, laisser celles disponibles pour les boutons ABXY physiques de boutons A et X.</span><span class="sxs-lookup"><span data-stu-id="269de-114">The mapping avoids overloading the A and X button IDs for the Menu buttons, to leave those available for physical ABXY buttons.</span></span>

<table>
<tr>
<th rowspan="2"><span data-ttu-id="269de-115">Entrée</span><span class="sxs-lookup"><span data-stu-id="269de-115">Input</span></span> </th><th colspan="2"><span data-ttu-id="269de-116"><a href="gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis">API Unity courantes</a></span><span class="sxs-lookup"><span data-stu-id="269de-116"><a href="gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis">Common Unity APIs</a></span></span><br /><span data-ttu-id="269de-117">(Input.GetButton/GetAxis)</span><span class="sxs-lookup"><span data-stu-id="269de-117">(Input.GetButton/GetAxis)</span></span> </th><th rowspan="2"><span data-ttu-id="269de-118"><a href="gestures-and-motion-controllers-in-unity.md#windows-specific-apis-xr.wsa.input">API d’entrée spécifiques à Windows MR</a></span><span class="sxs-lookup"><span data-stu-id="269de-118"><a href="gestures-and-motion-controllers-in-unity.md#windows-specific-apis-xr.wsa.input">Windows MR-specific Input API</a></span></span><br /><span data-ttu-id="269de-119">(XR.WSA.Input)</span><span class="sxs-lookup"><span data-stu-id="269de-119">(XR.WSA.Input)</span></span></th>
</tr><tr>
<th> <span data-ttu-id="269de-120">Gauche</span><span class="sxs-lookup"><span data-stu-id="269de-120">Left hand</span></span> </th><th> <span data-ttu-id="269de-121">Droite</span><span class="sxs-lookup"><span data-stu-id="269de-121">Right hand</span></span></th>
</tr><tr>
<td> <span data-ttu-id="269de-122">Sélectionnez le déclencheur enfoncé</span><span class="sxs-lookup"><span data-stu-id="269de-122">Select trigger pressed</span></span> </td><td> <span data-ttu-id="269de-123">Axe 9 = 1.0</span><span class="sxs-lookup"><span data-stu-id="269de-123">Axis 9 = 1.0</span></span> </td><td> <span data-ttu-id="269de-124">Axe 10 = 1.0</span><span class="sxs-lookup"><span data-stu-id="269de-124">Axis 10 = 1.0</span></span> </td><td> <span data-ttu-id="269de-125">selectPressed</span><span class="sxs-lookup"><span data-stu-id="269de-125">selectPressed</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-126">Sélectionnez la valeur analogique du déclencheur</span><span class="sxs-lookup"><span data-stu-id="269de-126">Select trigger analog value</span></span> </td><td> <span data-ttu-id="269de-127">Axe 9</span><span class="sxs-lookup"><span data-stu-id="269de-127">Axis 9</span></span> </td><td> <span data-ttu-id="269de-128">Axe 10</span><span class="sxs-lookup"><span data-stu-id="269de-128">Axis 10</span></span> </td><td> <span data-ttu-id="269de-129">selectPressedAmount</span><span class="sxs-lookup"><span data-stu-id="269de-129">selectPressedAmount</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-130">Sélectionnez le déclencheur partiellement enfoncé</span><span class="sxs-lookup"><span data-stu-id="269de-130">Select trigger partially pressed</span></span> </td><td> <span data-ttu-id="269de-131">Bouton 14 <i>(gamepad compat)</i> </span><span class="sxs-lookup"><span data-stu-id="269de-131">Button 14 <i>(gamepad compat)</i> </span></span></td><td> <span data-ttu-id="269de-132">Bouton 15 <i>(gamepad compat)</i> </span><span class="sxs-lookup"><span data-stu-id="269de-132">Button 15 <i>(gamepad compat)</i> </span></span></td><td> <span data-ttu-id="269de-133">selectPressedAmount &gt; 0.0</span><span class="sxs-lookup"><span data-stu-id="269de-133">selectPressedAmount &gt; 0.0</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-134">Bouton de menu enfoncé</span><span class="sxs-lookup"><span data-stu-id="269de-134">Menu button pressed</span></span> </td><td> <span data-ttu-id="269de-135">Bouton 6 \*</span><span class="sxs-lookup"><span data-stu-id="269de-135">Button 6\*</span></span> </td><td> <span data-ttu-id="269de-136">Bouton 7 \*</span><span class="sxs-lookup"><span data-stu-id="269de-136">Button 7\*</span></span> </td><td> <span data-ttu-id="269de-137">menuPressed</span><span class="sxs-lookup"><span data-stu-id="269de-137">menuPressed</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-138">Bouton de poignée enfoncé</span><span class="sxs-lookup"><span data-stu-id="269de-138">Grip button pressed</span></span> </td><td> <span data-ttu-id="269de-139">Axe 11 = 1.0 (aucune valeur analogique)</span><span class="sxs-lookup"><span data-stu-id="269de-139">Axis 11 = 1.0 (no analog values)</span></span><br /><span data-ttu-id="269de-140">Bouton 4 <i>(gamepad compat)</i> </span><span class="sxs-lookup"><span data-stu-id="269de-140">Button 4 <i>(gamepad compat)</i> </span></span></td><td> <span data-ttu-id="269de-141">Axe 12 = 1.0 (aucune valeur analogique)</span><span class="sxs-lookup"><span data-stu-id="269de-141">Axis 12 = 1.0 (no analog values)</span></span><br /><span data-ttu-id="269de-142">Bouton 5 <i>(gamepad compat)</i> </span><span class="sxs-lookup"><span data-stu-id="269de-142">Button 5 <i>(gamepad compat)</i> </span></span></td><td> <span data-ttu-id="269de-143">saisi</span><span class="sxs-lookup"><span data-stu-id="269de-143">grasped</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-144">Stick analogique X <i>(gauche : -1,0, droite : 1.0)</i> </span><span class="sxs-lookup"><span data-stu-id="269de-144">Thumbstick X <i>(left: -1.0, right: 1.0)</i> </span></span></td><td> <span data-ttu-id="269de-145">Axe 1</span><span class="sxs-lookup"><span data-stu-id="269de-145">Axis 1</span></span> </td><td> <span data-ttu-id="269de-146">Axe 4</span><span class="sxs-lookup"><span data-stu-id="269de-146">Axis 4</span></span> </td><td> <span data-ttu-id="269de-147">thumbstickPosition.x</span><span class="sxs-lookup"><span data-stu-id="269de-147">thumbstickPosition.x</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-148">Stick analogique Y <i>(haut : -1,0, bas : 1.0)</i> </span><span class="sxs-lookup"><span data-stu-id="269de-148">Thumbstick Y <i>(top: -1.0, bottom: 1.0)</i> </span></span></td><td> <span data-ttu-id="269de-149">Axe 2</span><span class="sxs-lookup"><span data-stu-id="269de-149">Axis 2</span></span> </td><td> <span data-ttu-id="269de-150">Axe 5</span><span class="sxs-lookup"><span data-stu-id="269de-150">Axis 5</span></span> </td><td> <span data-ttu-id="269de-151">thumbstickPosition.y</span><span class="sxs-lookup"><span data-stu-id="269de-151">thumbstickPosition.y</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-152">Stick analogique enfoncé</span><span class="sxs-lookup"><span data-stu-id="269de-152">Thumbstick pressed</span></span> </td><td> <span data-ttu-id="269de-153">Bouton 8</span><span class="sxs-lookup"><span data-stu-id="269de-153">Button 8</span></span> </td><td> <span data-ttu-id="269de-154">Bouton 9</span><span class="sxs-lookup"><span data-stu-id="269de-154">Button 9</span></span> </td><td> <span data-ttu-id="269de-155">thumbstickPressed</span><span class="sxs-lookup"><span data-stu-id="269de-155">thumbstickPressed</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-156">Pavé tactile X <i>(gauche : -1,0, droite : 1.0)</i> </span><span class="sxs-lookup"><span data-stu-id="269de-156">Touchpad X <i>(left: -1.0, right: 1.0)</i> </span></span></td><td> <span data-ttu-id="269de-157">Axe 17 \*</span><span class="sxs-lookup"><span data-stu-id="269de-157">Axis 17\*</span></span> </td><td> <span data-ttu-id="269de-158">Axe 19 \*</span><span class="sxs-lookup"><span data-stu-id="269de-158">Axis 19\*</span></span> </td><td> <span data-ttu-id="269de-159">touchpadPosition.x</span><span class="sxs-lookup"><span data-stu-id="269de-159">touchpadPosition.x</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-160">Pavé tactile Y <i>(haut : -1,0, bas : 1.0)</i> </span><span class="sxs-lookup"><span data-stu-id="269de-160">Touchpad Y <i>(top: -1.0, bottom: 1.0)</i> </span></span></td><td> <span data-ttu-id="269de-161">Axe 18 \*</span><span class="sxs-lookup"><span data-stu-id="269de-161">Axis 18\*</span></span> </td><td> <span data-ttu-id="269de-162">Axe 20 \*</span><span class="sxs-lookup"><span data-stu-id="269de-162">Axis 20\*</span></span> </td><td> <span data-ttu-id="269de-163">touchpadPosition.y</span><span class="sxs-lookup"><span data-stu-id="269de-163">touchpadPosition.y</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-164">Pavé tactile couvertes</span><span class="sxs-lookup"><span data-stu-id="269de-164">Touchpad touched</span></span> </td><td> <span data-ttu-id="269de-165">Bouton 18 \*</span><span class="sxs-lookup"><span data-stu-id="269de-165">Button 18\*</span></span> </td><td> <span data-ttu-id="269de-166">Bouton 19 \*</span><span class="sxs-lookup"><span data-stu-id="269de-166">Button 19\*</span></span> </td><td> <span data-ttu-id="269de-167">touchpadTouched</span><span class="sxs-lookup"><span data-stu-id="269de-167">touchpadTouched</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-168">Pavé tactile enfoncé</span><span class="sxs-lookup"><span data-stu-id="269de-168">Touchpad pressed</span></span> </td><td> <span data-ttu-id="269de-169">Bouton 16 \*</span><span class="sxs-lookup"><span data-stu-id="269de-169">Button 16\*</span></span> </td><td> <span data-ttu-id="269de-170">Bouton 17 \*</span><span class="sxs-lookup"><span data-stu-id="269de-170">Button 17\*</span></span> </td><td> <span data-ttu-id="269de-171">touchpadPressed</span><span class="sxs-lookup"><span data-stu-id="269de-171">touchpadPressed</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-172">6DoF poignée pose ou pose de pointeur</span><span class="sxs-lookup"><span data-stu-id="269de-172">6DoF grip pose or pointer pose</span></span> </td><td colspan="2"> <span data-ttu-id="269de-173"><i>Poignée</i> poser uniquement : <a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html">XR.InputTracking.GetLocalPosition</a></span><span class="sxs-lookup"><span data-stu-id="269de-173"><i>Grip</i> pose only: <a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html">XR.InputTracking.GetLocalPosition</a></span></span><br /><span data-ttu-id="269de-174"><a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalRotation.html">XR.InputTracking.GetLocalRotation</a></span><span class="sxs-lookup"><span data-stu-id="269de-174"><a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalRotation.html">XR.InputTracking.GetLocalRotation</a></span></span></td><td> <span data-ttu-id="269de-175">Passer <i>poignée</i> ou <i>pointeur</i> en tant qu’argument : sourceState.sourcePose.TryGetPosition</span><span class="sxs-lookup"><span data-stu-id="269de-175">Pass <i>Grip</i> or <i>Pointer</i> as an argument: sourceState.sourcePose.TryGetPosition</span></span><br /><span data-ttu-id="269de-176">sourceState.sourcePose.TryGetRotation</span><span class="sxs-lookup"><span data-stu-id="269de-176">sourceState.sourcePose.TryGetRotation</span></span><br /></td>
</tr><tr>
<td> <span data-ttu-id="269de-177">Suivi de l’état</span><span class="sxs-lookup"><span data-stu-id="269de-177">Tracking state</span></span> </td><td colspan="2"> <span data-ttu-id="269de-178"><i>Analyse de précision et de la source de perte risque de position disponible uniquement via les API spécifiques MR</i> </span><span class="sxs-lookup"><span data-stu-id="269de-178"><i>Position accuracy and source loss risk only available through MR-specific API</i> </span></span></td><td> <span data-ttu-id="269de-179"><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourcePose-positionAccuracy.html">sourceState.sourcePose.positionAccuracy</a></span><span class="sxs-lookup"><span data-stu-id="269de-179"><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourcePose-positionAccuracy.html">sourceState.sourcePose.positionAccuracy</a></span></span><br /><span data-ttu-id="269de-180"><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourceProperties-sourceLossRisk.html">sourceState.properties.sourceLossRisk</a></span><span class="sxs-lookup"><span data-stu-id="269de-180"><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourceProperties-sourceLossRisk.html">sourceState.properties.sourceLossRisk</a></span></span></td>
</tr>
</table>

>[!NOTE]
><span data-ttu-id="269de-181">Ces ID de bouton/axe diffère de l’ID Unity utilise pour OpenVR en raison de collisions dans les mappages utilisés par les boîtiers de commande, Oculus tactile et OpenVR.</span><span class="sxs-lookup"><span data-stu-id="269de-181">These button/axis IDs differ from the IDs that Unity uses for OpenVR due to collisions in the mappings used by gamepads, Oculus Touch and OpenVR.</span></span>

## <a name="grip-pose-vs-pointing-pose"></a><span data-ttu-id="269de-182">Pose de poignée et pose de pointage</span><span class="sxs-lookup"><span data-stu-id="269de-182">Grip pose vs. pointing pose</span></span>

<span data-ttu-id="269de-183">Réalité mixte Windows prend en charge les contrôleurs de mouvements dans un large éventail de facteurs de forme, avec la conception de chaque contrôleur qui se différencie par sa relation entre la position des utilisateurs manuellement et naturel « transférer » direction que les applications doit utiliser pour le pointage lors du rendu de la contrôleur.</span><span class="sxs-lookup"><span data-stu-id="269de-183">Windows Mixed Reality supports motion controllers in a variety of form factors, with each controller's design differing in its relationship between the user's hand position and the natural "forward" direction that apps should use for pointing when rendering the controller.</span></span>

<span data-ttu-id="269de-184">Pour mieux représenter ces contrôleurs, il existe deux types de risque de poser pour chaque source de l’interaction, vous pouvez passer en revue la **poignée pose** et **pose de pointeur**.</span><span class="sxs-lookup"><span data-stu-id="269de-184">To better represent these controllers, there are two kinds of poses you can investigate for each interaction source, the **grip pose** and the **pointer pose**.</span></span> <span data-ttu-id="269de-185">Les deux les poignée pose et pointeur pose les coordonnées sont exprimées par toutes les API Unity dans les coordonnées de monde Unity globales.</span><span class="sxs-lookup"><span data-stu-id="269de-185">Both the grip pose and pointer pose coordinates are expressed by all Unity APIs in global Unity world coordinates.</span></span>

### <a name="grip-pose"></a><span data-ttu-id="269de-186">Poignée pose</span><span class="sxs-lookup"><span data-stu-id="269de-186">Grip pose</span></span>

<span data-ttu-id="269de-187">Le **poignée pose** représente l’emplacement de la portée de main détectée par un HoloLens ou palm contenant un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="269de-187">The **grip pose** represents the location of either the palm of a hand detected by a HoloLens, or the palm holding a motion controller.</span></span>

<span data-ttu-id="269de-188">Sur des casques IMMERSIFS, la pose de poignée mieux permet de restituer **main de l’utilisateur** ou **détenues par un objet à portée de main de l’utilisateur**, tel qu’un mot de passe ou les électrons.</span><span class="sxs-lookup"><span data-stu-id="269de-188">On immersive headsets, the grip pose is best used to render **the user's hand** or **an object held in the user's hand**, such as a sword or gun.</span></span> <span data-ttu-id="269de-189">La pose de poignée est également utilisée lors de la visualisation d’un contrôleur de mouvements en tant que le **modèle pouvant être rendue** fourni par Windows pour un mouvement contrôleur utilise la pose de poignée que son origine et le centre de rotation.</span><span class="sxs-lookup"><span data-stu-id="269de-189">The grip pose is also used when visualizing a motion controller, as the **renderable model** provided by Windows for a motion controller uses the grip pose as its origin and center of rotation.</span></span>

<span data-ttu-id="269de-190">La pose de poignée est définie spécifiquement comme suit :</span><span class="sxs-lookup"><span data-stu-id="269de-190">The grip pose is defined specifically as follows:</span></span>
* <span data-ttu-id="269de-191">Le **Attrapez position**: Le centroïde de palm naturellement, tout en maintenant le contrôleur ajustée gauche ou droite pour centrer la position au sein de la poignée.</span><span class="sxs-lookup"><span data-stu-id="269de-191">The **grip position**: The palm centroid when holding the controller naturally, adjusted left or right to center the position within the grip.</span></span> <span data-ttu-id="269de-192">Sur le contrôleur de mouvement Windows Mixed Reality, cette position aligne généralement avec le bouton de compréhension.</span><span class="sxs-lookup"><span data-stu-id="269de-192">On the Windows Mixed Reality motion controller, this position generally aligns with the Grasp button.</span></span>
* <span data-ttu-id="269de-193">Le **Attrapez axe de droite de l’orientation**: Lorsque vous ouvrez totalement la main pour former une pose plat 5-doigt, le rayon qui est normal pour votre palm (en avant à partir de la gauche palm, vers l’arrière de palm droite)</span><span class="sxs-lookup"><span data-stu-id="269de-193">The **grip orientation's Right axis**: When you completely open your hand to form a flat 5-finger pose, the ray that is normal to your palm (forward from left palm, backward from right palm)</span></span>
* <span data-ttu-id="269de-194">Le **Attrapez axe vers l’avant de l’orientation**: Lorsque vous fermez votre main partiellement (comme le cas maintenant le contrôleur), le rayon pointe « forward » via le tube formé par vos doigts non curseur.</span><span class="sxs-lookup"><span data-stu-id="269de-194">The **grip orientation's Forward axis**: When you close your hand partially (as if holding the controller), the ray that points "forward" through the tube formed by your non-thumb fingers.</span></span>
* <span data-ttu-id="269de-195">Le **Attrapez orientation d’axe**: L’axe à distance impliqué par les définitions de droite, en avant.</span><span class="sxs-lookup"><span data-stu-id="269de-195">The **grip orientation's Up axis**: The Up axis implied by the Right and Forward definitions.</span></span>

<span data-ttu-id="269de-196">Vous pouvez accéder à la pose de poignée via une entrée soit Unity entre fournisseurs API (*[XR. InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html). GetLocalPosition/Rotation*) ou via l’API Windows MR spécifiques (*sourceState.sourcePose.TryGetPosition/Rotation*, demande présentent des données pour le **poignée** nœud).</span><span class="sxs-lookup"><span data-stu-id="269de-196">You can access the grip pose through either Unity's cross-vendor input API (*[XR.InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html).GetLocalPosition/Rotation*) or through the Windows MR-specific API (*sourceState.sourcePose.TryGetPosition/Rotation*, requesting pose data for the **Grip** node).</span></span>

### <a name="pointer-pose"></a><span data-ttu-id="269de-197">Pose de pointeur</span><span class="sxs-lookup"><span data-stu-id="269de-197">Pointer pose</span></span>

<span data-ttu-id="269de-198">Le **pose de pointeur** représente l’info-bulle du contrôleur qui pointe vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="269de-198">The **pointer pose** represents the tip of the controller pointing forward.</span></span>

<span data-ttu-id="269de-199">La pose de pointeur fournie par le système qui convient pour raycast lorsque vous êtes **rendu le modèle de contrôleur lui-même**.</span><span class="sxs-lookup"><span data-stu-id="269de-199">The system-provided pointer pose is best used to raycast when you are **rendering the controller model itself**.</span></span> <span data-ttu-id="269de-200">Si vous restituez un autre objet virtuel à la place le contrôleur, par exemple un électrons virtuel, vous devez faire avec un rayon qui est plus naturel pour cet objet virtuel, comme un rayon qui transite le long de la gaine du modèle électrons définies par l’application.</span><span class="sxs-lookup"><span data-stu-id="269de-200">If you are rendering some other virtual object in place of the controller, such as a virtual gun, you should point with a ray that is most natural for that virtual object, such as a ray that travels along the barrel of the app-defined gun model.</span></span> <span data-ttu-id="269de-201">Étant donné que les utilisateurs peuvent voir l’objet virtuel et non du contrôleur physique, en pointant avec l’objet virtuel seront probablement plus naturel pour ceux qui utilisent votre application.</span><span class="sxs-lookup"><span data-stu-id="269de-201">Because users can see the virtual object and not the physical controller, pointing with the virtual object will likely be more natural for those using your app.</span></span>

<span data-ttu-id="269de-202">Actuellement, la pose de pointeur est disponible dans Unity uniquement par le biais de l’API Windows MR spécifiques, *sourceState.sourcePose.TryGetPosition/Rotation*, en passant dans *InteractionSourceNode.Pointer* comme le argument.</span><span class="sxs-lookup"><span data-stu-id="269de-202">Currently, the pointer pose is available in Unity only through the Windows MR-specific API, *sourceState.sourcePose.TryGetPosition/Rotation*, passing in *InteractionSourceNode.Pointer* as the argument.</span></span>

## <a name="controller-tracking-state"></a><span data-ttu-id="269de-203">État du contrôleur de suivi</span><span class="sxs-lookup"><span data-stu-id="269de-203">Controller tracking state</span></span>

<span data-ttu-id="269de-204">Comme les casques, le contrôleur de mouvement de réalité mixte Windows ne requiert aucune configuration de capteurs de suivi externe.</span><span class="sxs-lookup"><span data-stu-id="269de-204">Like the headsets, the Windows Mixed Reality motion controller requires no setup of external tracking sensors.</span></span> <span data-ttu-id="269de-205">Au lieu de cela, les contrôleurs sont suivies par les capteurs dans le casque lui-même.</span><span class="sxs-lookup"><span data-stu-id="269de-205">Instead, the controllers are tracked by sensors in the headset itself.</span></span>

<span data-ttu-id="269de-206">Si l’utilisateur déplace les contrôleurs de champ de vision du casque, dans la plupart des cas Windows continuera à déduire des positions de contrôleur et les fournir à l’application.</span><span class="sxs-lookup"><span data-stu-id="269de-206">If the user moves the controllers out of the headset's field of view, in most cases Windows will continue to infer controller positions and provide them to the app.</span></span> <span data-ttu-id="269de-207">Lorsque le contrôleur a perdu visual de suivi pour le temps, les positions du contrôleur supprimera les positions de précision approximative.</span><span class="sxs-lookup"><span data-stu-id="269de-207">When the controller has lost visual tracking for long enough, the controller's positions will drop to approximate-accuracy positions.</span></span>

<span data-ttu-id="269de-208">À ce stade, le système sera verrouillage de corps le contrôleur à l’utilisateur, suivi de position de l’utilisateur comme ils sont en déplacement, tout en exposant toujours l’orientation true du contrôleur à l’aide de ses capteurs orientation interne.</span><span class="sxs-lookup"><span data-stu-id="269de-208">At this point, the system will body-lock the controller to the user, tracking the user's position as they move around, while still exposing the controller's true orientation using its internal orientation sensors.</span></span> <span data-ttu-id="269de-209">De nombreuses applications qui utilisent des contrôleurs pour pointer vers et activer des éléments d’interface utilisateur peuvent fonctionner normalement en précision approximative sans le remarquer utilisateur.</span><span class="sxs-lookup"><span data-stu-id="269de-209">Many apps that use controllers to point at and activate UI elements can operate normally while in approximate accuracy without the user noticing.</span></span>

<span data-ttu-id="269de-210">La meilleure façon de faire une idée pour cela consiste à essayer vous-même.</span><span class="sxs-lookup"><span data-stu-id="269de-210">The best way to get a feel for this is to try it yourself.</span></span> <span data-ttu-id="269de-211">Regardez cette vidéo avec des exemples de contenu immersive qui fonctionne avec les contrôleurs de mouvement entre les différents États de suivi :</span><span class="sxs-lookup"><span data-stu-id="269de-211">Check out this video with examples of immersive content that works with motion controllers across various tracking states:</span></span>

<br>

 >[!VIDEO https://www.youtube.com/embed/QK_fOFDHj0g]

### <a name="reasoning-about-tracking-state-explicitly"></a><span data-ttu-id="269de-212">Un peu de suivi de l’état explicitement</span><span class="sxs-lookup"><span data-stu-id="269de-212">Reasoning about tracking state explicitly</span></span>

<span data-ttu-id="269de-213">Les applications que vous souhaitent traiter les positions différemment en fonction de suivi de l’état peuvent aller plus loin et inspecter les propriétés sur l’état du contrôleur, tel que *SourceLossRisk* et *PositionAccuracy*:</span><span class="sxs-lookup"><span data-stu-id="269de-213">Apps that wish to treat positions differently based on tracking state may go further and inspect properties on the controller's state, such as *SourceLossRisk* and *PositionAccuracy*:</span></span>

<table>
<tr>
<th> <span data-ttu-id="269de-214">Suivi de l’état</span><span class="sxs-lookup"><span data-stu-id="269de-214">Tracking state</span></span> </th><th> <span data-ttu-id="269de-215">SourceLossRisk</span><span class="sxs-lookup"><span data-stu-id="269de-215">SourceLossRisk</span></span> </th><th> <span data-ttu-id="269de-216">PositionAccuracy</span><span class="sxs-lookup"><span data-stu-id="269de-216">PositionAccuracy</span></span> </th><th> <span data-ttu-id="269de-217">TryGetPosition</span><span class="sxs-lookup"><span data-stu-id="269de-217">TryGetPosition</span></span></th>
</tr><tr>
<td> <span data-ttu-id="269de-218"><b>Haute précision</b> </span><span class="sxs-lookup"><span data-stu-id="269de-218"><b>High accuracy</b> </span></span></td><td style="background-color: green; color: white"> <span data-ttu-id="269de-219">&lt; 1.0</span><span class="sxs-lookup"><span data-stu-id="269de-219">&lt; 1.0</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="269de-220">Élevée</span><span class="sxs-lookup"><span data-stu-id="269de-220">High</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="269de-221">true</span><span class="sxs-lookup"><span data-stu-id="269de-221">true</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-222"><b>Haute précision (courant un risque de perte)</b> </span><span class="sxs-lookup"><span data-stu-id="269de-222"><b>High accuracy (at risk of losing)</b> </span></span></td><td style="background-color: orange"> <span data-ttu-id="269de-223">== 1.0</span><span class="sxs-lookup"><span data-stu-id="269de-223">== 1.0</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="269de-224">Élevée</span><span class="sxs-lookup"><span data-stu-id="269de-224">High</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="269de-225">true</span><span class="sxs-lookup"><span data-stu-id="269de-225">true</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-226"><b>Précision approximative</b> </span><span class="sxs-lookup"><span data-stu-id="269de-226"><b>Approximate accuracy</b> </span></span></td><td style="background-color: orange"> <span data-ttu-id="269de-227">== 1.0</span><span class="sxs-lookup"><span data-stu-id="269de-227">== 1.0</span></span> </td><td style="background-color: orange"> <span data-ttu-id="269de-228">Approximate</span><span class="sxs-lookup"><span data-stu-id="269de-228">Approximate</span></span> </td><td style="background-color: green; color: white"> <span data-ttu-id="269de-229">true</span><span class="sxs-lookup"><span data-stu-id="269de-229">true</span></span></td>
</tr><tr>
<td> <span data-ttu-id="269de-230"><b>Aucune position</b> </span><span class="sxs-lookup"><span data-stu-id="269de-230"><b>No position</b> </span></span></td><td style="background-color: orange"> <span data-ttu-id="269de-231">== 1.0</span><span class="sxs-lookup"><span data-stu-id="269de-231">== 1.0</span></span> </td><td style="background-color: orange"> <span data-ttu-id="269de-232">Approximate</span><span class="sxs-lookup"><span data-stu-id="269de-232">Approximate</span></span> </td><td style="background-color: orange"> <span data-ttu-id="269de-233">false</span><span class="sxs-lookup"><span data-stu-id="269de-233">false</span></span></td>
</tr>
</table>

<span data-ttu-id="269de-234">Ces États de suivi de contrôleur de mouvement sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="269de-234">These motion controller tracking states are defined as follows:</span></span>
* <span data-ttu-id="269de-235">**Haute précision :** Pendant que le contrôleur de mouvement se trouve dans le champ de vision du casque, il fournira généralement positions extrêmement précise, en fonction de suivi visuel.</span><span class="sxs-lookup"><span data-stu-id="269de-235">**High accuracy:** While the motion controller is within the headset's field of view, it will generally provide high-accuracy positions, based on visual tracking.</span></span> <span data-ttu-id="269de-236">Remarque qu’un contrôleur de déplacement qui momentanément quitte le champ de vision ou est momentanément masqué à partir des capteurs casque (par exemple, en revanche de l’utilisateur) continue à renvoyer pose analyse de haute précision pour une courte période, en fonction de l’inertie suivi du contrôleur lui-même.</span><span class="sxs-lookup"><span data-stu-id="269de-236">Note that a moving controller that momentarily leaves the field of view or is momentarily obscured from the headset sensors (e.g. by the user's other hand) will continue to return high-accuracy poses for a short time, based on inertial tracking of the controller itself.</span></span>
* <span data-ttu-id="269de-237">**Analyse de précision élevé (au risque de perdre) :** Lorsque l’utilisateur déplace le contrôleur de mouvement au-delà du bord du champ de vision du casque, le casque sera bientôt ne peut pas suivre visuellement position de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="269de-237">**High accuracy (at risk of losing):** When the user moves the motion controller past the edge of the headset's field of view, the headset will soon be unable to visually track the controller's position.</span></span> <span data-ttu-id="269de-238">L’application sait quand le contrôleur a atteint cette limite de l’angle d’ouverture en visualisant le **SourceLossRisk** atteindre 1.0.</span><span class="sxs-lookup"><span data-stu-id="269de-238">The app knows when the controller has reached this FOV boundary by seeing the **SourceLossRisk** reach 1.0.</span></span> <span data-ttu-id="269de-239">À ce stade, l’application peut choisir de les suspendre les mouvements de contrôleur qui nécessitent un flux régulier de risque de poser de haute qualité.</span><span class="sxs-lookup"><span data-stu-id="269de-239">At that point, the app may choose to pause controller gestures that require a steady stream of very high-quality poses.</span></span>
* <span data-ttu-id="269de-240">**Précision approximative :** Lorsque le contrôleur a perdu visual de suivi pour le temps, les positions du contrôleur supprimera les positions de précision approximative.</span><span class="sxs-lookup"><span data-stu-id="269de-240">**Approximate accuracy:** When the controller has lost visual tracking for long enough, the controller's positions will drop to approximate-accuracy positions.</span></span> <span data-ttu-id="269de-241">À ce stade, le système sera verrouillage de corps le contrôleur à l’utilisateur, suivi de position de l’utilisateur comme ils sont en déplacement, tout en exposant toujours l’orientation true du contrôleur à l’aide de ses capteurs orientation interne.</span><span class="sxs-lookup"><span data-stu-id="269de-241">At this point, the system will body-lock the controller to the user, tracking the user's position as they move around, while still exposing the controller's true orientation using its internal orientation sensors.</span></span> <span data-ttu-id="269de-242">De nombreuses applications qui utilisent des contrôleurs pour pointer vers et activer des éléments d’interface utilisateur peuvent fonctionner en temps normal, en précision approximative, sans le remarquer utilisateur.</span><span class="sxs-lookup"><span data-stu-id="269de-242">Many apps that use controllers to point at and activate UI elements can operate as normal while in approximate accuracy without the user noticing.</span></span> <span data-ttu-id="269de-243">Applications plus lourd en termes d’entrée peuvent choisir de détecter cette liste à partir de **haute** précision à **approximatif** précision en inspectant le **PositionAccuracy** propriété, pour exemple pour donner à l’utilisateur un hitbox plus importante sur les cibles hors écran pendant ce temps.</span><span class="sxs-lookup"><span data-stu-id="269de-243">Apps with heavier input requirements may choose to sense this drop from **High** accuracy to **Approximate** accuracy by inspecting the **PositionAccuracy** property, for example to give the user a more generous hitbox on off-screen targets during this time.</span></span>
* <span data-ttu-id="269de-244">**Aucune position :** Alors que le contrôleur peut fonctionner à précision approximative pendant une longue période, parfois le système sache que même une position verrouillée de corps n’est pas significative pour le moment.</span><span class="sxs-lookup"><span data-stu-id="269de-244">**No position:** While the controller can operate at approximate accuracy for a long time, sometimes the system knows that even a body-locked position is not meaningful at the moment.</span></span> <span data-ttu-id="269de-245">Par exemple, un contrôleur qui a été activé simplement peut n’ont jamais été observé visuellement, ou un utilisateur peut placer un contrôleur qui est ensuite récupéré par quelqu'un d’autre vers le bas.</span><span class="sxs-lookup"><span data-stu-id="269de-245">For example, a controller that was just turned on may have never been observed visually, or a user may put down a controller that's then picked up by someone else.</span></span> <span data-ttu-id="269de-246">À l’heure, le système ne fournira pas n’importe quelle position à l’application, et *TryGetPosition* retournera la valeur false.</span><span class="sxs-lookup"><span data-stu-id="269de-246">At those times, the system will not provide any position to the app, and *TryGetPosition* will return false.</span></span>

## <a name="common-unity-apis-inputgetbuttongetaxis"></a><span data-ttu-id="269de-247">API Unity commune (Input.GetButton/GetAxis)</span><span class="sxs-lookup"><span data-stu-id="269de-247">Common Unity APIs (Input.GetButton/GetAxis)</span></span>

<span data-ttu-id="269de-248">**Namespace :** *UnityEngine*, *UnityEngine.XR*</span><span class="sxs-lookup"><span data-stu-id="269de-248">**Namespace:** *UnityEngine*, *UnityEngine.XR*</span></span><br>
<span data-ttu-id="269de-249">**Types**: *Input*, *XR.InputTracking*</span><span class="sxs-lookup"><span data-stu-id="269de-249">**Types**: *Input*, *XR.InputTracking*</span></span>

<span data-ttu-id="269de-250">Unity utilise actuellement son général *Input.GetButton/Input.GetAxis* API pour exposer une entrée pour [le SDK Oculus](https://docs.unity3d.com/Manual/OculusControllers.html), [le SDK OpenVR](https://docs.unity3d.com/Manual/OpenVRControllers.html) et la réalité mixte Windows, y compris mains et contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="269de-250">Unity currently uses its general *Input.GetButton/Input.GetAxis* APIs to expose input for [the Oculus SDK](https://docs.unity3d.com/Manual/OculusControllers.html), [the OpenVR SDK](https://docs.unity3d.com/Manual/OpenVRControllers.html) and Windows Mixed Reality, including hands and motion controllers.</span></span> <span data-ttu-id="269de-251">Si votre application utilise ces API pour l’entrée, il peut facilement prendre en charge les contrôleurs de mouvement entre plusieurs XR kits de développement logiciel, y compris Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="269de-251">If your app uses these APIs for input, it can easily support motion controllers across multiple XR SDKs, including Windows Mixed Reality.</span></span>

### <a name="getting-a-logical-buttons-pressed-state"></a><span data-ttu-id="269de-252">Obtention de l’état enfoncé d’un bouton logique</span><span class="sxs-lookup"><span data-stu-id="269de-252">Getting a logical button's pressed state</span></span>

<span data-ttu-id="269de-253">Pour utiliser l’entrée Unity générale API, vous commencerez généralement en organisant les boutons et les axes à des noms logiques dans le [Unity entrée Manager](https://docs.unity3d.com/Manual/ConventionalGameInput.html), liaison d’un bouton ou un axe ID à chaque nom.</span><span class="sxs-lookup"><span data-stu-id="269de-253">To use the general Unity input APIs, you'll typically start by wiring up buttons and axes to logical names in the [Unity Input Manager](https://docs.unity3d.com/Manual/ConventionalGameInput.html), binding a button or axis IDs to each name.</span></span> <span data-ttu-id="269de-254">Vous pouvez ensuite écrire du code qui fait référence à ce nom de bouton/axe logique.</span><span class="sxs-lookup"><span data-stu-id="269de-254">You can then write code that refers to that logical button/axis name.</span></span>

<span data-ttu-id="269de-255">Par exemple, pour mapper le bouton de déclencheur du contrôleur de mouvement de gauche à l’action d’envoi, accédez à **Modifier > Paramètres du projet > entrée** dans Unity et développez les propriétés de la section d’envoi sous Axes.</span><span class="sxs-lookup"><span data-stu-id="269de-255">For example, to map the left motion controller's trigger button to the Submit action, go to **Edit > Project Settings > Input** within Unity, and expand the properties of the Submit section under Axes.</span></span> <span data-ttu-id="269de-256">Modifier le **bouton positif** ou **bouton positif Alt** propriété à lire **bouton joystick 14**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="269de-256">Change the **Postive Button** or **Alt Positive Button** property to read **joystick button 14**, like this:</span></span>

<span data-ttu-id="269de-257">![InputManager de Unity](images/unity-input-manager.png)</span><span class="sxs-lookup"><span data-stu-id="269de-257">![Unity's InputManager](images/unity-input-manager.png)</span></span><br>
<span data-ttu-id="269de-258">*Unity InputManager*</span><span class="sxs-lookup"><span data-stu-id="269de-258">*Unity InputManager*</span></span>

<span data-ttu-id="269de-259">Votre script peut ensuite vérifier pour l’action Envoyer à l’aide *Input.GetButton*:</span><span class="sxs-lookup"><span data-stu-id="269de-259">Your script can then check for the Submit action using *Input.GetButton*:</span></span>

```cs
if (Input.GetButton("Submit"))
{
  // ...
}
```
<span data-ttu-id="269de-260">Vous pouvez ajouter des boutons plus logiques en modifiant le **taille** propriété sous **Axes**.</span><span class="sxs-lookup"><span data-stu-id="269de-260">You can add more logical buttons by changing the **Size** property under **Axes**.</span></span>

### <a name="getting-a-physical-buttons-pressed-state-directly"></a><span data-ttu-id="269de-261">L’obtention d’un état appuyé d’un bouton physique directement</span><span class="sxs-lookup"><span data-stu-id="269de-261">Getting a physical button's pressed state directly</span></span>

<span data-ttu-id="269de-262">Vous pouvez également accéder à boutons manuellement par leurs complet nom, en utilisant *Input.GetKey*:</span><span class="sxs-lookup"><span data-stu-id="269de-262">You can also access buttons manually by their fully-qualified name, using *Input.GetKey*:</span></span>

```cs
if (Input.GetKey("joystick button 8"))
{
  // ...
}
```

### <a name="getting-a-hand-or-motion-controllers-pose"></a><span data-ttu-id="269de-263">Obtention d’une main ou pose du contrôleur de mouvement</span><span class="sxs-lookup"><span data-stu-id="269de-263">Getting a hand or motion controller's pose</span></span>

<span data-ttu-id="269de-264">Vous pouvez accéder à la position et la rotation du contrôleur, à l’aide de *XR. InputTracking*:</span><span class="sxs-lookup"><span data-stu-id="269de-264">You can access the position and rotation of the controller, using *XR.InputTracking*:</span></span>

```cs
Vector3 leftPosition = InputTracking.GetLocalPosition(XRNode.LeftHand);
Quaternion leftRotation = InputTracking.GetLocalRotation(XRNode.LeftHand);
```

<span data-ttu-id="269de-265">Notez que cela représente pose de poignée du contrôleur (où l’utilisateur appuie sur le contrôleur), ce qui est utile pour le rendu d’un à double tranchant ou électrons dans main de l’utilisateur ou un modèle du contrôleur lui-même.</span><span class="sxs-lookup"><span data-stu-id="269de-265">Note that this represents the controller's grip pose (where the user holds the controller), which is useful for rendering a sword or gun in the user's hand, or a model of the controller itself.</span></span>

<span data-ttu-id="269de-266">Notez que la relation entre cette pose poignée et la pose de pointeur (où l’info-bulle du contrôleur de pointe) peut-être différer entre les contrôleurs.</span><span class="sxs-lookup"><span data-stu-id="269de-266">Note that the relationship between this grip pose and the pointer pose (where the tip of the controller is pointing) may differ across controllers.</span></span> <span data-ttu-id="269de-267">À ce stade, l’accès à la pose de pointeur du contrôleur n’est possible via l’entrée M. propres API, décrite dans les sections ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="269de-267">At this moment, accessing the controller's pointer pose is only possible through the MR-specific input API, described in the sections below.</span></span>

## <a name="windows-specific-apis-xrwsainput"></a><span data-ttu-id="269de-268">API Windows spécifique (XR. WSA. Entrée)</span><span class="sxs-lookup"><span data-stu-id="269de-268">Windows-specific APIs (XR.WSA.Input)</span></span>

<span data-ttu-id="269de-269">**Namespace :** *UnityEngine.XR.WSA.Input*</span><span class="sxs-lookup"><span data-stu-id="269de-269">**Namespace:** *UnityEngine.XR.WSA.Input*</span></span><br>
<span data-ttu-id="269de-270">**Types**: *InteractionManager*, *InteractionSourceState*, *InteractionSource*, *InteractionSourceProperties*, *InteractionSourceKind*, *InteractionSourceLocation*</span><span class="sxs-lookup"><span data-stu-id="269de-270">**Types**: *InteractionManager*, *InteractionSourceState*, *InteractionSource*, *InteractionSourceProperties*, *InteractionSourceKind*, *InteractionSourceLocation*</span></span>

<span data-ttu-id="269de-271">Pour accéder à des informations plus détaillées sur l’entrée de main Windows Mixed Reality (pour HoloLens) et les contrôleurs de mouvement, vous pouvez choisir d’utiliser les API d’entrée spatiales spécifiques à Windows sous la *UnityEngine.XR.WSA.Input* espace de noms.</span><span class="sxs-lookup"><span data-stu-id="269de-271">To get at more detailed information about Windows Mixed Reality hand input (for HoloLens) and motion controllers, you can choose to use the Windows-specific spatial input APIs under the *UnityEngine.XR.WSA.Input* namespace.</span></span> <span data-ttu-id="269de-272">Cela vous permet d’accéder à des informations supplémentaires, telles que de la précision de la position ou le type de source, ce qui vous permet d’indiquer les mains et les uns des autres contrôleurs de.</span><span class="sxs-lookup"><span data-stu-id="269de-272">This lets you access additional information, such as position accuracy or the source kind, letting you tell hands and controllers apart.</span></span>

### <a name="polling-for-the-state-of-hands-and-motion-controllers"></a><span data-ttu-id="269de-273">Interrogation de l’état de mains et contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="269de-273">Polling for the state of hands and motion controllers</span></span>

<span data-ttu-id="269de-274">Vous pouvez interroger à l’état de cette image pour chaque source (contrôleur main ou de mouvement) d’interaction à l’aide de la *GetCurrentReading* (méthode).</span><span class="sxs-lookup"><span data-stu-id="269de-274">You can poll for this frame's state for each interaction source (hand or motion controller) using the *GetCurrentReading* method.</span></span>

```cs
var interactionSourceStates = InteractionManager.GetCurrentReading();
foreach (var interactionSourceState in interactionSourceStates) {
    // ...
}
```

<span data-ttu-id="269de-275">Chaque *InteractionSourceState* vous obtenez précédent représente une source de l’interaction au moment actuel dans le temps.</span><span class="sxs-lookup"><span data-stu-id="269de-275">Each *InteractionSourceState* you get back represents an interaction source at the current moment in time.</span></span> <span data-ttu-id="269de-276">Le *InteractionSourceState* expose des informations telles que :</span><span class="sxs-lookup"><span data-stu-id="269de-276">The *InteractionSourceState* exposes info such as:</span></span>
* <span data-ttu-id="269de-277">Qui [types d’activations](motion-controllers.md) se produisent (sélectionnez/Menu/appréhendé/pavé tactile/stick analogique)</span><span class="sxs-lookup"><span data-stu-id="269de-277">Which [kinds of presses](motion-controllers.md) are occurring (Select/Menu/Grasp/Touchpad/Thumbstick)</span></span>

   ```cs
   if (interactionSourceState.selectPressed) {
       // ...
   }
   ```
* <span data-ttu-id="269de-278">Autres données spécifiques aux contrôleurs de mouvement, tel le pavé tactile et/ou de stick analogique coordonnées XY et état touché</span><span class="sxs-lookup"><span data-stu-id="269de-278">Other data specific to motion controllers, such the touchpad and/or thumbstick's XY coordinates and touched state</span></span>

   ```cs
   if (interactionSourceState.touchpadTouched && interactionSourceState.touchpadPosition.x > 0.5) {
       // ...
   }
   ```
   
* <span data-ttu-id="269de-279">Le InteractionSourceKind pour savoir si la source est une main ou un contrôleur de mouvement</span><span class="sxs-lookup"><span data-stu-id="269de-279">The InteractionSourceKind to know if the source is a hand or a motion controller</span></span>

   ```cs
   if (interactionSourceState.source.kind == InteractionSourceKind.Hand) {
       // ...
   }
   ```

### <a name="polling-for-forward-predicted-rendering-poses"></a><span data-ttu-id="269de-280">Interrogation de risque de poser prédit avant le rendu</span><span class="sxs-lookup"><span data-stu-id="269de-280">Polling for forward-predicted rendering poses</span></span>

* <span data-ttu-id="269de-281">Lors de l’interrogation pour les données d’interaction de source des mains et les contrôleurs, vous obtenez le risque de poser est prédit avant le risque de poser pour le moment dans le temps lorsque photons de cette image seront atteignent les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="269de-281">When polling for interaction source data from hands and controllers, the poses you get are forward-predicted poses for the moment in time when this frame's photons will reach the user's eyes.</span></span>  <span data-ttu-id="269de-282">Il est préférable d’utiliser ces risque de poser avant prédit pour **rendu** le contrôleur ou un détenu chaque image de l’objet.</span><span class="sxs-lookup"><span data-stu-id="269de-282">These forward-predicted poses are best used for **rendering** the controller or a held object each frame.</span></span>  <span data-ttu-id="269de-283">Si vous êtes ciblant l’appui sur une donnée ou mise en production avec le contrôleur, il s’agit plus précis si vous utilisez l’événement d’historique API décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="269de-283">If you are targeting a given press or release with the controller, that will be most accurate if you use the historical event APIs described below.</span></span>

   ```cs
   var sourcePose = interactionSourceState.sourcePose;
   Vector3 sourceGripPosition;
   Quaternion sourceGripRotation;
   if ((sourcePose.TryGetPosition(out sourceGripPosition, InteractionSourceNode.Grip)) &&
       (sourcePose.TryGetRotation(out sourceGripRotation, InteractionSourceNode.Grip))) {
       // ...
   }
   ```

* <span data-ttu-id="269de-284">Vous pouvez également obtenir la pose principale a prédit l’avant pour ce frame actuel.</span><span class="sxs-lookup"><span data-stu-id="269de-284">You can also get the forward-predicted head pose for this current frame.</span></span>  <span data-ttu-id="269de-285">Comme avec la pose de la source, cela est utile pour **rendu** un curseur, bien que ciblant un press donné ou la mise en production sera plus précis si vous utilisez l’événement d’historique API décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="269de-285">As with the source pose, this is useful for **rendering** a cursor, although targeting a given press or release will be most accurate if you use the historical event APIs described below.</span></span>

   ```cs
   var headPose = interactionSourceState.headPose;
   var headRay = new Ray(headPose.position, headPose.forward);
   RaycastHit raycastHit;
   if (Physics.Raycast(headPose.position, headPose.forward, out raycastHit, 10)) {
       var cursorPos = raycastHit.point;
       // ...
   }
   ```

### <a name="handling-interaction-source-events"></a><span data-ttu-id="269de-286">Gestion des événements de source d’interaction</span><span class="sxs-lookup"><span data-stu-id="269de-286">Handling interaction source events</span></span>

<span data-ttu-id="269de-287">Pour gérer les événements d’entrée qu’elles se produisent avec leurs données pose historique précis, vous pouvez gérer les événements de source d’interaction au lieu d’interrogation.</span><span class="sxs-lookup"><span data-stu-id="269de-287">To handle input events as they happen with their accurate historical pose data, you can handle interaction source events instead of polling.</span></span>

<span data-ttu-id="269de-288">Pour gérer les événements de source d’interaction :</span><span class="sxs-lookup"><span data-stu-id="269de-288">To handle interaction source events:</span></span>
* <span data-ttu-id="269de-289">Inscrivez-vous à un *InteractionManager* événement d’entrée.</span><span class="sxs-lookup"><span data-stu-id="269de-289">Register for a *InteractionManager* input event.</span></span> <span data-ttu-id="269de-290">Pour chaque type d’événement d’interaction qui vous intéresse, vous devez vous abonner à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="269de-290">For each type of interaction event that you are interested in, you need to subscribe to it.</span></span>

   ```cs
   InteractionManager.InteractionSourcePressed += InteractionManager_InteractionSourcePressed;
   ```
   
* <span data-ttu-id="269de-291">Gérer l’événement.</span><span class="sxs-lookup"><span data-stu-id="269de-291">Handle the event.</span></span> <span data-ttu-id="269de-292">Une fois que vous êtes abonné à un événement d’interaction, vous obtiendrez le rappel lorsque cela est approprié.</span><span class="sxs-lookup"><span data-stu-id="269de-292">Once you have subscribed to an interaction event, you will get the callback when appropriate.</span></span> <span data-ttu-id="269de-293">Dans le *SourcePressed* exemple, il s’agit une fois que la source a été détectée et avant qu’il est publié ou perdue.</span><span class="sxs-lookup"><span data-stu-id="269de-293">In the *SourcePressed* example, this will be after the source was detected and before it is released or lost.</span></span>

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

### <a name="how-to-stop-handling-an-event"></a><span data-ttu-id="269de-294">Comment arrêter la gestion d’un événement</span><span class="sxs-lookup"><span data-stu-id="269de-294">How to stop handling an event</span></span>

<span data-ttu-id="269de-295">Vous devez arrêter la gestion d’un événement lorsque vous n’êtes plus intéressé par l’événement ou de détruire l’objet qui s’est abonnée à l’événement.</span><span class="sxs-lookup"><span data-stu-id="269de-295">You need to stop handling an event when you are no longer interested in the event or you are destroying the object that has subscribed to the event.</span></span> <span data-ttu-id="269de-296">Pour arrêter la gestion de l’événement, vous désabonner l’événement.</span><span class="sxs-lookup"><span data-stu-id="269de-296">To stop handling the event, you unsubscribe from the event.</span></span>

```cs
InteractionManager.InteractionSourcePressed -= InteractionManager_InteractionSourcePressed;
```

### <a name="list-of-interaction-source-events"></a><span data-ttu-id="269de-297">Liste des événements de source d’interaction</span><span class="sxs-lookup"><span data-stu-id="269de-297">List of interaction source events</span></span>

<span data-ttu-id="269de-298">Les événements de source d’interaction disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="269de-298">The available interaction source events are:</span></span>
* <span data-ttu-id="269de-299">*InteractionSourceDetected* (source devient active)</span><span class="sxs-lookup"><span data-stu-id="269de-299">*InteractionSourceDetected* (source becomes active)</span></span>
* <span data-ttu-id="269de-300">*InteractionSourceLost* (devient inactif)</span><span class="sxs-lookup"><span data-stu-id="269de-300">*InteractionSourceLost* (becomes inactive)</span></span>
* <span data-ttu-id="269de-301">*InteractionSourcePressed* (tap, appuyez sur le bouton ou « Select » prononcés)</span><span class="sxs-lookup"><span data-stu-id="269de-301">*InteractionSourcePressed* (tap, button press, or "Select" uttered)</span></span>
* <span data-ttu-id="269de-302">*InteractionSourceReleased* (fin de drainage, du bouton ou fin de « Select » a été exprimée)</span><span class="sxs-lookup"><span data-stu-id="269de-302">*InteractionSourceReleased* (end of a tap, button released, or end of "Select" uttered)</span></span>
* <span data-ttu-id="269de-303">*InteractionSourceUpdated* (déplace ou bien modifie un état)</span><span class="sxs-lookup"><span data-stu-id="269de-303">*InteractionSourceUpdated* (moves or otherwise changes some state)</span></span>

### <a name="events-for-historical-targeting-poses-that-most-accurately-match-a-press-or-release"></a><span data-ttu-id="269de-304">Événements pour le ciblage historiques qui pose plus de précision correspondent à un press ou la mise en production</span><span class="sxs-lookup"><span data-stu-id="269de-304">Events for historical targeting poses that most accurately match a press or release</span></span>

<span data-ttu-id="269de-305">Les API d’interrogation décrits précédemment donner à votre application risque de poser avant prédit.</span><span class="sxs-lookup"><span data-stu-id="269de-305">The polling APIs described earlier give your app forward-predicted poses.</span></span>  <span data-ttu-id="269de-306">Alors que ces pose prédite conviennent le mieux pour le rendu le contrôleur ou un objet virtuel de poche, pose futures n’est pas optimales pour le ciblage, pour deux raisons principales :</span><span class="sxs-lookup"><span data-stu-id="269de-306">While those predicted poses are best for rendering the controller or a virtual handheld object, future poses are not optimal for targeting, for two key reasons:</span></span>
* <span data-ttu-id="269de-307">Lorsque l’utilisateur appuie sur un bouton sur un contrôleur, il peut y avoir environ 20 ms de latence sans fil via Bluetooth avant que le système ne reçoive la presse.</span><span class="sxs-lookup"><span data-stu-id="269de-307">When the user presses a button on a controller, there can be about 20ms of wireless latency over Bluetooth before the system receives the press.</span></span>
* <span data-ttu-id="269de-308">Ensuite, si vous utilisez une pose prédite de transfert, il y aurait un autre 10-20 ms de prédiction directe appliquée pour cibler le temps lorsque les photons du frame actif seront atteignent les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="269de-308">Then, if you are using a forward-predicted pose, there would be another 10-20ms of forward prediction applied to target the time when the current frame's photons will reach the user's eyes.</span></span>

<span data-ttu-id="269de-309">Cela signifie que l’interrogation vous donne une pose source ou head poser c'est-à-dire 30-40 MS avant à partir de l’où l’utilisateur head et mains réellement étaient lors de la presse ou la version s’est produit.</span><span class="sxs-lookup"><span data-stu-id="269de-309">This means that polling gives you a source pose or head pose that is 30-40ms forward from where the user's head and hands actually were back when the press or release happened.</span></span>  <span data-ttu-id="269de-310">Pour l’entrée de main HoloLens, il n’existe aucun délai de transmission sans fil, il existe un délai de traitement similaire pour détecter la presse.</span><span class="sxs-lookup"><span data-stu-id="269de-310">For HoloLens hand input, while there's no wireless transmission delay, there is a similar processing delay to detect the press.</span></span>

<span data-ttu-id="269de-311">Pour cible précisément en fonction de l’intention d’origine de l’utilisateur pour un press main ou de contrôleur, vous devez utiliser la source historiques pose ou principal pose de celui *InteractionSourcePressed* ou *InteractionSourceReleased* événement d’entrée.</span><span class="sxs-lookup"><span data-stu-id="269de-311">To accurately target based on the user's original intent for a hand or controller press, you should use the historical source pose or head pose from that *InteractionSourcePressed* or *InteractionSourceReleased* input event.</span></span>

<span data-ttu-id="269de-312">Vous pouvez cibler un press ou libérer avec des données historiques pose de tête de l’utilisateur ou de leur contrôleur :</span><span class="sxs-lookup"><span data-stu-id="269de-312">You can target a press or release with historical pose data from the user's head or their controller:</span></span>
* <span data-ttu-id="269de-313">La pose principale pour le moment dans le temps lorsque appuyez sur un contrôleur ou mouvement s’est produite, qui peuvent être utilisées pour **ciblant** pour déterminer ce que l’utilisateur a été [gazing](gaze.md) à :</span><span class="sxs-lookup"><span data-stu-id="269de-313">The head pose at the moment in time when a gesture or controller press occurred, which can be used for **targeting** to determine what the user was [gazing](gaze.md) at:</span></span>

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

* <span data-ttu-id="269de-314">La pose de source pour le moment dans le temps lorsque appuyez sur un contrôleur de mouvement s’est produite, qui peuvent être utilisées pour **ciblant** pour déterminer ce que l’utilisateur a été pointant vers le contrôleur d’à.</span><span class="sxs-lookup"><span data-stu-id="269de-314">The source pose at the moment in time when a motion controller press occurred, which can be used for **targeting** to determine what the user was pointing the controller at.</span></span>  <span data-ttu-id="269de-315">Il s’agit de l’état du contrôleur qui a rencontré la presse.</span><span class="sxs-lookup"><span data-stu-id="269de-315">This will be the state of the controller that experienced the press.</span></span>  <span data-ttu-id="269de-316">Si vous restituez le contrôleur lui-même, vous pouvez demander la pose de pointeur plutôt que la pose de poignée pour dépanner le ciblage rayon à partir de ce que l’utilisateur prend en compte le Conseil naturels de qui a rendu le contrôleur :</span><span class="sxs-lookup"><span data-stu-id="269de-316">If you are rendering the controller itself, you can request the pointer pose rather than the grip pose, to shoot the targeting ray from what the user will consider the natural tip of that rendered controller:</span></span>

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

### <a name="event-handlers-example"></a><span data-ttu-id="269de-317">Exemple de gestionnaires d’événements</span><span class="sxs-lookup"><span data-stu-id="269de-317">Event handlers example</span></span>

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

## <a name="high-level-composite-gesture-apis-gesturerecognizer"></a><span data-ttu-id="269de-318">Mouvement de haut niveau composite API (GestureRecognizer)</span><span class="sxs-lookup"><span data-stu-id="269de-318">High-level composite gesture APIs (GestureRecognizer)</span></span>

<span data-ttu-id="269de-319">**Namespace :** *UnityEngine.XR.WSA.Input*</span><span class="sxs-lookup"><span data-stu-id="269de-319">**Namespace:** *UnityEngine.XR.WSA.Input*</span></span><br>
<span data-ttu-id="269de-320">**Types**: *GestureRecognizer*, *GestureSettings*, *InteractionSourceKind*</span><span class="sxs-lookup"><span data-stu-id="269de-320">**Types**: *GestureRecognizer*, *GestureSettings*, *InteractionSourceKind*</span></span>

<span data-ttu-id="269de-321">Votre application peut aussi reconnaître des gestes composites de haut niveau pour les gestes de suspension, de Manipulation et de Navigation spatiale sources d’entrée, Tap.</span><span class="sxs-lookup"><span data-stu-id="269de-321">Your app can also recognize higher-level composite gestures for spatial input sources, Tap, Hold, Manipulation and Navigation gestures.</span></span> <span data-ttu-id="269de-322">Vous pouvez reconnaître ces mouvements composites à la fois sur [mains](gestures.md) et [contrôleurs de mouvement](motion-controllers.md) à l’aide de la GestureRecognizer.</span><span class="sxs-lookup"><span data-stu-id="269de-322">You can recognize these composite gestures across both [hands](gestures.md) and [motion controllers](motion-controllers.md) using the GestureRecognizer.</span></span>

<span data-ttu-id="269de-323">Chaque événement de mouvement sur le GestureRecognizer fournit le SourceKind pour l’entrée, ainsi que le ciblage rayon principal au moment de l’événement.</span><span class="sxs-lookup"><span data-stu-id="269de-323">Each Gesture event on the GestureRecognizer provides the SourceKind for the input as well as the targeting head ray at the time of the event.</span></span> <span data-ttu-id="269de-324">Certains événements fournissent des informations de contexte supplémentaires spécifiques.</span><span class="sxs-lookup"><span data-stu-id="269de-324">Some events provide additional context specific information.</span></span>

<span data-ttu-id="269de-325">Il existe quelques étapes nécessaires pour capturer des mouvements à l’aide d’un module de reconnaissance de mouvement :</span><span class="sxs-lookup"><span data-stu-id="269de-325">There are only a few steps required to capture gestures using a Gesture Recognizer:</span></span>
1. <span data-ttu-id="269de-326">Créer un nouveau module de reconnaissance de mouvement</span><span class="sxs-lookup"><span data-stu-id="269de-326">Create a new Gesture Recognizer</span></span>
2. <span data-ttu-id="269de-327">Spécifiez les gestes à surveiller</span><span class="sxs-lookup"><span data-stu-id="269de-327">Specify which gestures to watch for</span></span>
3. <span data-ttu-id="269de-328">S’abonner aux événements pour ces mouvements</span><span class="sxs-lookup"><span data-stu-id="269de-328">Subscribe to events for those gestures</span></span>
4. <span data-ttu-id="269de-329">Démarrer la capture de mouvements</span><span class="sxs-lookup"><span data-stu-id="269de-329">Start capturing gestures</span></span>

### <a name="create-a-new-gesture-recognizer"></a><span data-ttu-id="269de-330">Créer un nouveau module de reconnaissance de mouvement</span><span class="sxs-lookup"><span data-stu-id="269de-330">Create a new Gesture Recognizer</span></span>

<span data-ttu-id="269de-331">Pour utiliser le *GestureRecognizer*, vous devez avoir créé un *GestureRecognizer*:</span><span class="sxs-lookup"><span data-stu-id="269de-331">To use the *GestureRecognizer*, you must have created a *GestureRecognizer*:</span></span>

```cs
GestureRecognizer recognizer = new GestureRecognizer();
```

### <a name="specify-which-gestures-to-watch-for"></a><span data-ttu-id="269de-332">Spécifiez les gestes à surveiller</span><span class="sxs-lookup"><span data-stu-id="269de-332">Specify which gestures to watch for</span></span>

<span data-ttu-id="269de-333">Spécifiez les gestes, vous êtes intéressé par le biais de *SetRecognizableGestures()*:</span><span class="sxs-lookup"><span data-stu-id="269de-333">Specify which gestures you are interested in via *SetRecognizableGestures()*:</span></span>

```cs
recognizer.SetRecognizableGestures(GestureSettings.Tap | GestureSettings.Hold);
```

### <a name="subscribe-to-events-for-those-gestures"></a><span data-ttu-id="269de-334">S’abonner aux événements pour ces mouvements</span><span class="sxs-lookup"><span data-stu-id="269de-334">Subscribe to events for those gestures</span></span>

<span data-ttu-id="269de-335">S’abonner aux événements pour les gestes que vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="269de-335">Subscribe to events for the gestures you are interested in.</span></span>

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
><span data-ttu-id="269de-336">Les mouvements de navigation et de Manipulation sont mutuellement exclusifs sur une instance d’un *GestureRecognizer*.</span><span class="sxs-lookup"><span data-stu-id="269de-336">Navigation and Manipulation gestures are mutually exclusive on an instance of a *GestureRecognizer*.</span></span>

### <a name="start-capturing-gestures"></a><span data-ttu-id="269de-337">Démarrer la capture de mouvements</span><span class="sxs-lookup"><span data-stu-id="269de-337">Start capturing gestures</span></span>

<span data-ttu-id="269de-338">Par défaut, un *GestureRecognizer* ne surveille pas d’entrée jusqu'à ce que *StartCapturingGestures()* est appelée.</span><span class="sxs-lookup"><span data-stu-id="269de-338">By default, a *GestureRecognizer* does not monitor input until *StartCapturingGestures()* is called.</span></span> <span data-ttu-id="269de-339">Il est possible qu’un événement de mouvement peut être généré après *StopCapturingGestures()* est appelée si l’entrée a été effectuée avant l’image où *StopCapturingGestures()* a été traité.</span><span class="sxs-lookup"><span data-stu-id="269de-339">It is possible that a gesture event may be generated after *StopCapturingGestures()* is called if input was performed before the frame where *StopCapturingGestures()* was processed.</span></span> <span data-ttu-id="269de-340">Le *GestureRecognizer* mémorisent s’il a été activé ou désactivé durant le frame Evaluation dans lequel le mouvement ayant réellement eu lieu et par conséquent, il est fiable pour démarrer et arrêter le suivi de mouvement basé sur le ciblage du pointage de regard de cette image.</span><span class="sxs-lookup"><span data-stu-id="269de-340">The *GestureRecognizer* will remember whether it was on or off during the previou frame in which the gesture actually occurred, and so it is reliable to start and stop gesture monitoring based on this frame's gaze targeting.</span></span>

```cs
recognizer.StartCapturingGestures();
```

### <a name="stop-capturing-gestures"></a><span data-ttu-id="269de-341">Arrêter la capture de mouvements</span><span class="sxs-lookup"><span data-stu-id="269de-341">Stop capturing gestures</span></span>

<span data-ttu-id="269de-342">Pour arrêter la reconnaissance du mouvement :</span><span class="sxs-lookup"><span data-stu-id="269de-342">To stop gesture recognition:</span></span>

```cs
recognizer.StopCapturingGestures();
```

### <a name="removing-a-gesture-recognizer"></a><span data-ttu-id="269de-343">Suppression d’un module de reconnaissance de mouvement</span><span class="sxs-lookup"><span data-stu-id="269de-343">Removing a gesture recognizer</span></span>

<span data-ttu-id="269de-344">N’oubliez pas de se désabonner d’événements auxquels vous êtes abonnés à l’avant de détruire un *GestureRecognizer* objet.</span><span class="sxs-lookup"><span data-stu-id="269de-344">Remember to unsubscribe from subscribed events before destroying a *GestureRecognizer* object.</span></span>

```cs
void OnDestroy()
{
    recognizer.Tapped -= GestureRecognizer_Tapped;
    recognizer.HoldStarted -= GestureRecognizer_HoldStarted;
    recognizer.HoldCompleted -= GestureRecognizer_HoldCompleted;
    recognizer.HoldCanceled -= GestureRecognizer_HoldCanceled;
}
```

## <a name="rendering-the-motion-controller-model-in-unity"></a><span data-ttu-id="269de-345">Le modèle de contrôleur de mouvement dans Unity de rendu</span><span class="sxs-lookup"><span data-stu-id="269de-345">Rendering the motion controller model in Unity</span></span>

<span data-ttu-id="269de-346">![Téléportation et modèle de contrôleur de mouvement](images/motioncontrollertest-teleport-1000px.png)</span><span class="sxs-lookup"><span data-stu-id="269de-346">![Motion Controller model and teleportation](images/motioncontrollertest-teleport-1000px.png)</span></span><br>
<span data-ttu-id="269de-347">*Téléportation et modèle de contrôleur de mouvement*</span><span class="sxs-lookup"><span data-stu-id="269de-347">*Motion controller model and teleportation*</span></span>

<span data-ttu-id="269de-348">Pour afficher les contrôleurs de mouvement dans votre application qui correspondent à vos utilisateurs sont maintenant et expliquer que différents boutons sont enfoncés les contrôleurs de physiques, vous pouvez utiliser la **MotionController préfabriqué** dans le [Toolkit de réalité mixte ](https://github.com/Microsoft/MixedRealityToolkit-Unity/).</span><span class="sxs-lookup"><span data-stu-id="269de-348">To render motion controllers in your app that match the physical controllers your users are holding and articulate as various buttons are pressed, you can use the **MotionController prefab** in the [Mixed Reality Toolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/).</span></span>  <span data-ttu-id="269de-349">Cette préfabriqué charge dynamiquement le modèle glTF correct lors de l’exécution à partir du pilote de contrôleur installé mouvement du système.</span><span class="sxs-lookup"><span data-stu-id="269de-349">This prefab dynamically loads the correct glTF model at runtime from the system's installed motion controller driver.</span></span>  <span data-ttu-id="269de-350">Il est important de charger ces modèles de manière dynamique plutôt que de les importer manuellement dans l’éditeur, afin que votre application n’affiche des modèles 3D physiquement précis pour des contrôleurs actuels et futurs de vos utilisateurs peuvent avoir.</span><span class="sxs-lookup"><span data-stu-id="269de-350">It's important to load these models dynamically rather than importing them manually in the editor, so that your app will show physically accurate 3D models for any current and future controllers your users may have.</span></span>

1. <span data-ttu-id="269de-351">Suivez le [mise en route](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/GettingStarted.md) instructions pour télécharger le Toolkit de réalité mixte et ajoutez-le à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="269de-351">Follow the [Getting Started](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/GettingStarted.md) instructions to download the Mixed Reality Toolkit and add it to your Unity project.</span></span>
2. <span data-ttu-id="269de-352">Si vous avez remplacé votre appareil photo avec la *MixedRealityCameraParent* prefab en tant que partie de la procédure de mise en route, vous êtes fin prêt !</span><span class="sxs-lookup"><span data-stu-id="269de-352">If you replaced your camera with the *MixedRealityCameraParent* prefab as part of the Getting Started steps, you're good to go!</span></span>  <span data-ttu-id="269de-353">Ce préfabriqué inclut le rendu de contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="269de-353">That prefab includes motion controller rendering.</span></span>  <span data-ttu-id="269de-354">Sinon, ajoutez *Assets/HoloToolkit/Input/Prefabs/MotionControllers.prefab* dans votre scène à partir du volet de projet.</span><span class="sxs-lookup"><span data-stu-id="269de-354">Otherwise, add *Assets/HoloToolkit/Input/Prefabs/MotionControllers.prefab* into your scene from the Project pane.</span></span>  <span data-ttu-id="269de-355">Vous souhaiterez ajouter que prefab en tant qu’enfant de l’objet parent vous permet de déplacer la caméra autour lorsque l’utilisateur teleports dans votre scène, afin que les contrôleurs sont fournis, ainsi que l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="269de-355">You'll want to add that prefab as a child of whatever parent object you use to move the camera around when the user teleports within your scene, so that the controllers come along with the user.</span></span>  <span data-ttu-id="269de-356">Si votre application n’implique pas teleporting, ajoutez simplement le préfabriqué à la racine de votre scène.</span><span class="sxs-lookup"><span data-stu-id="269de-356">If your app does not involve teleporting, just add the prefab at the root of your scene.</span></span>

## <a name="throwing-objects"></a><span data-ttu-id="269de-357">Levée d’objets</span><span class="sxs-lookup"><span data-stu-id="269de-357">Throwing objects</span></span>

<span data-ttu-id="269de-358">Levée d’objets dans la réalité virtuelle est un problème difficile, puis il peut à première vue sembler.</span><span class="sxs-lookup"><span data-stu-id="269de-358">Throwing objects in virtual reality is a harder problem then it may at first seem.</span></span> <span data-ttu-id="269de-359">Comme avec les interactions en plus physiquement, lors de la levée de jeu jouent le rôle de manière inattendue, il est immédiatement évident et s’arrête en immersion.</span><span class="sxs-lookup"><span data-stu-id="269de-359">As with most physically based interactions, when throwing in game acts in an unexpected way, it is immediately obvious and breaks immersion.</span></span> <span data-ttu-id="269de-360">Nous avons passé des temps de réfléchir profondément sur la façon de représenter un comportement levant physiquement correct et ont développé quelques recommandations, activées par le biais des mises à jour sur notre plateforme, que nous souhaitons partager avec vous.</span><span class="sxs-lookup"><span data-stu-id="269de-360">We have spent some time thinking deeply about how to represent a physically correct throwing behavior, and have come up with a few guidelines, enabled through updates to our platform, that we would like to share with you.</span></span>

<span data-ttu-id="269de-361">Vous trouverez un exemple de comment nous vous recommandons d’implémenter lever [ici](https://github.com/keluecke/MixedRealityToolkit-Unity/blob/master/External/Unitypackages/ThrowingStarter.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="269de-361">You can find an example of how we recommend to implement throwing [here](https://github.com/keluecke/MixedRealityToolkit-Unity/blob/master/External/Unitypackages/ThrowingStarter.unitypackage).</span></span> <span data-ttu-id="269de-362">Cet exemple suit ces quatre instructions :</span><span class="sxs-lookup"><span data-stu-id="269de-362">This sample follows these four guidelines:</span></span>
* <span data-ttu-id="269de-363">**Utiliser le contrôleur *velocity* au lieu de la position**.</span><span class="sxs-lookup"><span data-stu-id="269de-363">**Use the controller’s *velocity* instead of position**.</span></span> <span data-ttu-id="269de-364">Dans la mise à jour de novembre de Windows, nous avons introduit un changement de comportement dans le ['' approximatif '' positionnels suivi de l’état](motion-controllers.md#controller-tracking-state).</span><span class="sxs-lookup"><span data-stu-id="269de-364">In the November update to Windows, we introduced a change in behavior when in the [''Approximate'' positional tracking state](motion-controllers.md#controller-tracking-state).</span></span> <span data-ttu-id="269de-365">Dans cet état, rapidité plus d’informations sur le contrôleur de continuera à déclarer pour tant que nous pensons qu’il s’agit de haute précision, ce qui est souvent plus de temps que la position reste haute précision.</span><span class="sxs-lookup"><span data-stu-id="269de-365">When in this state, velocity information about the controller will continue to be reported for as long as we believe it is high accuracy, which is often longer than position remains high accuracy.</span></span>
* <span data-ttu-id="269de-366">**Incorporer le *vitesse angulaire* du contrôleur**.</span><span class="sxs-lookup"><span data-stu-id="269de-366">**Incorporate the *angular velocity* of the controller**.</span></span> <span data-ttu-id="269de-367">Cette logique est contenue dans le `throwing.cs` de fichiers dans le `GetThrownObjectVelAngVel` méthode statique, dans le package lié ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="269de-367">This logic is all contained in the `throwing.cs` file in the `GetThrownObjectVelAngVel` static method, within the package linked above:</span></span>
   1. <span data-ttu-id="269de-368">Comme la vitesse angulaire est conservée, l’objet levé doit conserver la même vitesse angulaire telle qu’elle avait au moment de la levée : `objectAngularVelocity = throwingControllerAngularVelocity;`</span><span class="sxs-lookup"><span data-stu-id="269de-368">As angular velocity is conserved, the thrown object must maintain the same angular velocity as it had at the moment of the throw: `objectAngularVelocity = throwingControllerAngularVelocity;`</span></span>
   2. <span data-ttu-id="269de-369">Comme le centre de gravité de l’objet levé est probablement que pas à l’origine de la poignée de pose, il comporte sûrement une rapidité différentes, puis au contrôleur de dans le cadre de référence de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="269de-369">As the center of mass of the thrown object is likely not at the origin of the grip pose, it likely has a different velocity then that of the controller in the frame of reference of the user.</span></span> <span data-ttu-id="269de-370">La partie de la vitesse de l’objet a contribué de cette façon est la rapidité de tangente instantanée du centre de gravité de l’objet levé autour de l’origine du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="269de-370">The portion of the object’s velocity contributed in this way is the instantaneous tangential velocity of the center of mass of the thrown object around the controller origin.</span></span> <span data-ttu-id="269de-371">Cette vitesse tangent est le produit croisé de la vitesse angulaire du contrôleur avec le vecteur qui représente la distance entre l’origine de contrôleur et le centre de gravité de l’objet levé.</span><span class="sxs-lookup"><span data-stu-id="269de-371">This tangential velocity is the cross product of the angular velocity of the controller with the vector representing the distance between the controller origin and the center of mass of the thrown object.</span></span>
    
      ```cs
      Vector3 radialVec = thrownObjectCenterOfMass - throwingControllerPos;
      Vector3 tangentialVelocity = Vector3.Cross(throwingControllerAngularVelocity, radialVec);
      ```
   
   3. <span data-ttu-id="269de-372">La rapidité totale de l’objet levé est par conséquent, la somme de vitesse du contrôleur et cette rapidité tangente : `objectVelocity = throwingControllerVelocity + tangentialVelocity;`</span><span class="sxs-lookup"><span data-stu-id="269de-372">The total velocity of the thrown object is thus the sum of velocity of the controller and this tangential velocity: `objectVelocity = throwingControllerVelocity + tangentialVelocity;`</span></span>

* <span data-ttu-id="269de-373">**Prêtez attention à la *temps* auquel nous appliquons la rapidité**.</span><span class="sxs-lookup"><span data-stu-id="269de-373">**Pay close attention to the *time* at which we apply the velocity**.</span></span> <span data-ttu-id="269de-374">Lorsqu’un bouton est enfoncé, il peut prendre jusqu'à 20 ms pour cet événement à se propager via Bluetooth au système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="269de-374">When a button is pressed, it can take up to 20ms for that event to bubble up through Bluetooth to the operating system.</span></span> <span data-ttu-id="269de-375">Cela signifie que si vous interrogez un changement d’état de contrôleur à partir d’appuyé ne pas enfoncé ou vice versa, les informations de pose de contrôleur que vous obtenez avec lui sera avant cette modification dans un état.</span><span class="sxs-lookup"><span data-stu-id="269de-375">This means that if you poll for a controller state change from pressed to not pressed or vice versa, the controller pose information you get with it will actually be ahead of this change in state.</span></span> <span data-ttu-id="269de-376">En outre, la pose de contrôleur présentée par notre API d’interrogation est transférer prédite afin de refléter une pose probablement au moment que le frame s’affichera, qui peut être plus de 20 ms puis à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="269de-376">Further, the controller pose presented by our polling API is forward predicted to reflect a likely pose at the time the frame will be displayed which could be more then 20ms in the future.</span></span> <span data-ttu-id="269de-377">Cette fonction est utile pour *rendu* stockés les objets, mais composés de notre problème de temps pour *ciblant* l’objet que nous calculons la trajectoire pour le moment l’utilisateur a relâché leur throw.</span><span class="sxs-lookup"><span data-stu-id="269de-377">This is good for *rendering* held objects, but compounds our time problem for *targeting* the object as we calculate the trajectory for the moment the user released their throw.</span></span> <span data-ttu-id="269de-378">Heureusement, avec la mise à jour de novembre, lorsqu’un événement Unity comme *InteractionSourcePressed* ou *InteractionSourceReleased* est envoyé, l’état inclut les données historiques pose à partir du serveur lorsque le bouton a été effectivement appuyé ou publiées.</span><span class="sxs-lookup"><span data-stu-id="269de-378">Fortunately, with the November update, when a Unity event like *InteractionSourcePressed* or *InteractionSourceReleased* is sent, the state includes the historical pose data from back when the button was actually pressed or released.</span></span>  <span data-ttu-id="269de-379">Pour obtenir le rendu de contrôleur plus précis et le contrôleur ciblant pendant lève, vous devez correctement utiliser l’interrogation et la gestion des événements, comme il convient :</span><span class="sxs-lookup"><span data-stu-id="269de-379">To get the most accurate controller rendering and controller targeting during throws, you must correctly use polling and eventing, as appropriate:</span></span>
   * <span data-ttu-id="269de-380">Pour **rendu de contrôleur** chaque trame, votre application doit positionner du contrôleur *GameObject* au niveau du contrôleur avant prédit poser pour des temps de photon du frame actif.</span><span class="sxs-lookup"><span data-stu-id="269de-380">For **controller rendering** each frame, your app should position the controller's *GameObject* at the forward-predicted controller pose for the current frame’s photon time.</span></span>  <span data-ttu-id="269de-381">Vous obtenez ces données à partir d’Unity comme API d’interrogation *[XR. InputTracking.GetLocalPosition](https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html)* ou  *[XR. WSA. Input.InteractionManager.GetCurrentReading](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.GetCurrentReading.html)*.</span><span class="sxs-lookup"><span data-stu-id="269de-381">You get this data from Unity polling APIs like *[XR.InputTracking.GetLocalPosition](https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html)* or *[XR.WSA.Input.InteractionManager.GetCurrentReading](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.GetCurrentReading.html)*.</span></span>
   * <span data-ttu-id="269de-382">Pour **contrôleur ciblant** selon une press ou une mise en production, votre application doit raycast et calculer des trajectoires selon la pose de contrôleur historiques pour cet événement press ou de mise en production.</span><span class="sxs-lookup"><span data-stu-id="269de-382">For **controller targeting** upon a press or release, your app should raycast and calculate trajectories based on the historical controller pose for that press or release event.</span></span>  <span data-ttu-id="269de-383">Vous obtenez ces données à partir de l’API, d’événements Unity comme  *[InteractionManager.InteractionSourcePressed](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.InteractionSourcePressed.html)*.</span><span class="sxs-lookup"><span data-stu-id="269de-383">You get this data from Unity eventing APIs, like *[InteractionManager.InteractionSourcePressed](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.InteractionSourcePressed.html)*.</span></span>
* <span data-ttu-id="269de-384">**Utilisez la pose de poignée**.</span><span class="sxs-lookup"><span data-stu-id="269de-384">**Use the grip pose**.</span></span> <span data-ttu-id="269de-385">Vitesse angulaire et la vélocité sont signalés par rapport à la pose de poignée, pas de pointeur pose.</span><span class="sxs-lookup"><span data-stu-id="269de-385">Angular velocity and velocity are reported relative to the grip pose, not pointer pose.</span></span>

<span data-ttu-id="269de-386">Lever continuera à améliorer les futures mises à jour de Windows, et vous pouvez vous attendre à trouver plus d’informations sur ce dernier ici.</span><span class="sxs-lookup"><span data-stu-id="269de-386">Throwing will continue to improve with future Windows updates, and you can expect to find more information on it here.</span></span>

## <a name="accelerate-development-with-mixed-reality-toolkit"></a><span data-ttu-id="269de-387">Accélérez le développement avec le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="269de-387">Accelerate development with Mixed Reality Toolkit</span></span>

<span data-ttu-id="269de-388">Il existe deux scènes exemple sur InputManager et MotionController dans Unity.</span><span class="sxs-lookup"><span data-stu-id="269de-388">There are two example scenes about InputManager and MotionController in Unity.</span></span> <span data-ttu-id="269de-389">Au moyen de ces séquences, vous pouvez apprendre à utiliser InputManager de MRTK et accéder aux données gèrent les événements à partir des boutons du contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="269de-389">Through these scenes, you can learn how to use MRTK's InputManager and access data handle events from the motion controller buttons.</span></span>

- [<span data-ttu-id="269de-390">HoloToolkit-Examples/Input/Scenes/InputManagerTest.unity</span><span class="sxs-lookup"><span data-stu-id="269de-390">HoloToolkit-Examples/Input/Scenes/InputManagerTest.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scenes/InputManagerTest.unity)
- [<span data-ttu-id="269de-391">HoloToolkit-Examples/Input/Scenes/MotionControllerTest.unity</span><span class="sxs-lookup"><span data-stu-id="269de-391">HoloToolkit-Examples/Input/Scenes/MotionControllerTest.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scenes/MotionControllerTest.unity)
- [<span data-ttu-id="269de-392">Fichier Lisez-moi des détails techniques</span><span class="sxs-lookup"><span data-stu-id="269de-392">Technical details README File</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input)

<span data-ttu-id="269de-393">![Exemple d’entrée des scènes dans MRTK](images/MRTK_ExampleScene_Input.png)</span><span class="sxs-lookup"><span data-stu-id="269de-393">![Input example scenes in MRTK](images/MRTK_ExampleScene_Input.png)</span></span><br>
<span data-ttu-id="269de-394">*Exemple d’entrée des scènes dans MRTK*</span><span class="sxs-lookup"><span data-stu-id="269de-394">*Input example scenes in MRTK*</span></span>

### <a name="automatic-scene-setup"></a><span data-ttu-id="269de-395">Programme d’installation automatique de scène</span><span class="sxs-lookup"><span data-stu-id="269de-395">Automatic scene setup</span></span>

<span data-ttu-id="269de-396">Lorsque vous importez [MRTK publie des packages de Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases) ou cloner le projet à partir de la [référentiel GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity), vous vous apprêtez à trouver un nouveau menu « Toolkit de réalité mixte » dans Unity.</span><span class="sxs-lookup"><span data-stu-id="269de-396">When you import [MRTK release Unity packages](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases) or clone the project from the [GitHub repository](https://github.com/Microsoft/MixedRealityToolkit-Unity), you are going to find a new menu 'Mixed Reality Toolkit' in Unity.</span></span> <span data-ttu-id="269de-397">Sous le menu « Configurer », vous verrez le menu « Application des paramètres de scène réalité mixte ».</span><span class="sxs-lookup"><span data-stu-id="269de-397">Under 'Configure' menu, you will see the menu 'Apply Mixed Reality Scene Settings'.</span></span> <span data-ttu-id="269de-398">Lorsque vous cliquez dessus, il supprime l’appareil photo par défaut et ajoute les composants fondamentaux - [InputManager](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/InputManager.prefab), [MixedRealityCameraParent](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/MixedRealityCameraParent.prefab), et [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab).</span><span class="sxs-lookup"><span data-stu-id="269de-398">When you click it, it removes the default camera and adds foundational components - [InputManager](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/InputManager.prefab), [MixedRealityCameraParent](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/MixedRealityCameraParent.prefab), and [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab).</span></span>

<span data-ttu-id="269de-399">![Menu MRTK pour le programme d’installation de scène](images/MRTK_Input_Menu.png)</span><span class="sxs-lookup"><span data-stu-id="269de-399">![MRTK Menu for scene setup](images/MRTK_Input_Menu.png)</span></span><br>
<span data-ttu-id="269de-400">*Menu MRTK pour le programme d’installation de scène*</span><span class="sxs-lookup"><span data-stu-id="269de-400">*MRTK Menu for scene setup*</span></span>

<span data-ttu-id="269de-401">![Programme d’installation automatique de scène dans MRTK](images/MRTK_HowTo_Input1.png)</span><span class="sxs-lookup"><span data-stu-id="269de-401">![Automatic scene setup in MRTK](images/MRTK_HowTo_Input1.png)</span></span><br>
<span data-ttu-id="269de-402">*Programme d’installation automatique de scène dans MRTK*</span><span class="sxs-lookup"><span data-stu-id="269de-402">*Automatic scene setup in MRTK*</span></span>

### <a name="mixedrealitycamera-prefab"></a><span data-ttu-id="269de-403">MixedRealityCamera prefab</span><span class="sxs-lookup"><span data-stu-id="269de-403">MixedRealityCamera prefab</span></span>

<span data-ttu-id="269de-404">Vous pouvez également ajouter manuellement à partir du panneau projet.</span><span class="sxs-lookup"><span data-stu-id="269de-404">You can also manually add these from the project panel.</span></span> <span data-ttu-id="269de-405">Vous pouvez trouver ces composants en tant que prefabs.</span><span class="sxs-lookup"><span data-stu-id="269de-405">You can find these components as prefabs.</span></span> <span data-ttu-id="269de-406">Si vous effectuez une recherche **MixedRealityCamera**, vous serez en mesure de voir les deux prefabs caméra différente.</span><span class="sxs-lookup"><span data-stu-id="269de-406">When you search **MixedRealityCamera**, you will be able to see two different camera prefabs.</span></span> <span data-ttu-id="269de-407">La différence est, **MixedRealityCamera** est l’appareil photo uniquement prefab tandis que **MixedRealityCameraParent** inclut des composants supplémentaires pour les casques IMMERSIFS telles que téléportation, Motion Contrôleur et limites.</span><span class="sxs-lookup"><span data-stu-id="269de-407">The difference is, **MixedRealityCamera** is the camera only prefab whereas, **MixedRealityCameraParent** includes additional components for the immersive headsets such as Teleportation, Motion Controller and, Boundary.</span></span>

<span data-ttu-id="269de-408">![Prefabs caméra dans MRTK](images/MRTK_HowTo_Input2.png)</span><span class="sxs-lookup"><span data-stu-id="269de-408">![Camera prefabs in MRTK](images/MRTK_HowTo_Input2.png)</span></span><br>
<span data-ttu-id="269de-409">*Prefabs caméra dans MRTK*</span><span class="sxs-lookup"><span data-stu-id="269de-409">*Camera prefabs in MRTK*</span></span>

<span data-ttu-id="269de-410">**MixedRealtyCamera** prend en charge HoloLens et immersif casque.</span><span class="sxs-lookup"><span data-stu-id="269de-410">**MixedRealtyCamera** supports both HoloLens and immersive headset.</span></span> <span data-ttu-id="269de-411">Il détecte le type d’appareil et optimise les propriétés telles que d’effacer les indicateurs et Skybox.</span><span class="sxs-lookup"><span data-stu-id="269de-411">It detects the device type and optimizes the properties such as clear flags and Skybox.</span></span> <span data-ttu-id="269de-412">Vous trouverez ci-dessous certaines des propriétés utiles, vous pouvez personnaliser comme curseur personnalisé, les modèles de contrôleur de mouvement et Floor.</span><span class="sxs-lookup"><span data-stu-id="269de-412">Below you can find some of the useful properties you can customize such as custom Cursor, Motion Controller models, and Floor.</span></span>

<span data-ttu-id="269de-413">![Propriétés pour le contrôleur de mouvement, curseur et étage](images/MRTK_HowTo_Input3.png)</span><span class="sxs-lookup"><span data-stu-id="269de-413">![Properties for the Motion controller, Cursor and Floor](images/MRTK_HowTo_Input3.png)</span></span><br>
<span data-ttu-id="269de-414">*Propriétés pour le contrôleur de mouvement, curseur et étage*</span><span class="sxs-lookup"><span data-stu-id="269de-414">*Properties for the Motion controller, Cursor and Floor*</span></span>

## <a name="follow-along-with-tutorials"></a><span data-ttu-id="269de-415">Suivre des didacticiels</span><span class="sxs-lookup"><span data-stu-id="269de-415">Follow along with tutorials</span></span>

<span data-ttu-id="269de-416">Didacticiels pas à pas, avec des exemples de personnalisation plus détaillées, sont disponibles dans l’Académie de réalité mixte :</span><span class="sxs-lookup"><span data-stu-id="269de-416">Step-by-step tutorials, with more detailed customization examples, are available in the Mixed Reality Academy:</span></span>

- [<span data-ttu-id="269de-417">Entrée M. 211 : Gesture</span><span class="sxs-lookup"><span data-stu-id="269de-417">MR Input 211: Gesture</span></span>](holograms-211.md)
- [<span data-ttu-id="269de-418">Entrée M. 213 : Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="269de-418">MR Input 213: Motion controllers</span></span>](mixed-reality-213.md)

<span data-ttu-id="269de-419">[![Entrée M. 213 - contrôleur de mouvement](images/mr213-main-600px.jpg)](https://docs.microsoft.com/windows/mixed-reality/mixed-reality-213)</span><span class="sxs-lookup"><span data-stu-id="269de-419">[![MR Input 213 - Motion controller](images/mr213-main-600px.jpg)](https://docs.microsoft.com/windows/mixed-reality/mixed-reality-213)</span></span><br>
<span data-ttu-id="269de-420">*Entrée M. 213 - contrôleur de mouvement*</span><span class="sxs-lookup"><span data-stu-id="269de-420">*MR Input 213 - Motion controller*</span></span>

## <a name="see-also"></a><span data-ttu-id="269de-421">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="269de-421">See also</span></span>

* [<span data-ttu-id="269de-422">Mouvements</span><span class="sxs-lookup"><span data-stu-id="269de-422">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="269de-423">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="269de-423">Motion controllers</span></span>](motion-controllers.md)
* [<span data-ttu-id="269de-424">UnityEngine.XR.WSA.Input</span><span class="sxs-lookup"><span data-stu-id="269de-424">UnityEngine.XR.WSA.Input</span></span>](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.html)
* [<span data-ttu-id="269de-425">UnityEngine.XR.InputTracking</span><span class="sxs-lookup"><span data-stu-id="269de-425">UnityEngine.XR.InputTracking</span></span>](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html)
* [<span data-ttu-id="269de-426">InteractionInputSource.cs dans MixedRealityToolkit-Unity</span><span class="sxs-lookup"><span data-stu-id="269de-426">InteractionInputSource.cs in MixedRealityToolkit-Unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/InputSources/InteractionInputSource.cs)
