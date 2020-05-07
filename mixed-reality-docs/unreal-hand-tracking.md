---
title: Suivi des mains dans des conditions non réelles
description: Explique comment utiliser le suivi des handles en mode inréel
author: AndreyChistyakov
ms.author: anchisty
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality, HoloLens, suivi de la main
ms.openlocfilehash: 3f7f4dd1eb62cb707eaaf8632a2ba3c280a4ac31
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82835415"
---
# <a name="hand-tracking"></a><span data-ttu-id="09a72-104">Suivi de la main</span><span class="sxs-lookup"><span data-stu-id="09a72-104">Hand Tracking</span></span>

<span data-ttu-id="09a72-105">Le système de suivi de la main utilise les paumes et les doigts d’une personne en tant qu’entrée dans un environnement inréel.</span><span class="sxs-lookup"><span data-stu-id="09a72-105">The hand tracking system uses a person’s palms and fingers as input to Unreal.</span></span> <span data-ttu-id="09a72-106">Un développeur peut obtenir la position et la rotation de chaque doigt, le Palm entier et même les gestes à utiliser dans leur propre code.</span><span class="sxs-lookup"><span data-stu-id="09a72-106">A developer can get every finger’s position and rotation, the entire palm, and even hand gestures to use in their own code.</span></span> 

## <a name="hand-pose"></a><span data-ttu-id="09a72-107">Poser à la main</span><span class="sxs-lookup"><span data-stu-id="09a72-107">Hand Pose</span></span>

<span data-ttu-id="09a72-108">À l’aide de la pose, les développeurs peuvent suivre les mains et les doigts de l’utilisateur actif comme entrée.</span><span class="sxs-lookup"><span data-stu-id="09a72-108">Using the hand pose, developers can track the hands and fingers of the active user as input.</span></span> <span data-ttu-id="09a72-109">Ce système est exposé via les plans et C++.</span><span class="sxs-lookup"><span data-stu-id="09a72-109">This system is exposed through both Blueprints and C++.</span></span> <span data-ttu-id="09a72-110">Les détails techniques se trouvent dans la classe WinRT correspondante [Windows. perception. People. HandPose](https://docs.microsoft.com/uwp/api/windows.perception.people.handpose) cette API inréelle fournit les données au format du système de coordonnées non réelles et les battements sont synchronisés avec le moteur inréel.</span><span class="sxs-lookup"><span data-stu-id="09a72-110">Technical details are in the corresponding WinRT class [Windows.Perception.People.HandPose](https://docs.microsoft.com/uwp/api/windows.perception.people.handpose) This Unreal API provides the data in the format of Unreal’s coordinate system and ticks are synchronised with the Unreal Engine.</span></span>

### <a name="enum"></a><span data-ttu-id="09a72-111">Enum</span><span class="sxs-lookup"><span data-stu-id="09a72-111">Enum</span></span>

<span data-ttu-id="09a72-112">EWMRHandKeypoint décrit la hiérarchie osseuse de la main.</span><span class="sxs-lookup"><span data-stu-id="09a72-112">EWMRHandKeypoint describes the Hand’s bone hierarchy.</span></span> 

<span data-ttu-id="09a72-113">Blueprint</span><span class="sxs-lookup"><span data-stu-id="09a72-113">Blueprint:</span></span>

![Main KEYpoint BP](images/unreal/hand-keypoint-bp.png)
 
<span data-ttu-id="09a72-115">C++ :</span><span class="sxs-lookup"><span data-stu-id="09a72-115">C++:</span></span>
```cpp
enum class EWMRHandKeypoint : uint8
{
    Palm,
    Wrist,
    ThumbMetacarpal,
    ThumbProximal,
    ThumbDistal,
    ThumbTip,
    IndexMetacarpal,
    IndexProximal,
    IndexIntermediate,
    IndexDistal,
    IndexTip,
    MiddleMetacarpal,
    MiddleProximal,
    MiddleIntermediate,
    MiddleDistal,
    MiddleTip,
    RingMetacarpal,
    RingProximal,
    RingIntermediate,
    RingDistal,
    RingTip,
    LittleMetacarpal,
    LittleProximal,
    LittleIntermediate,
    LittleDistal,
    LittleTip
};
```

![Squelette de main](images/hand-skeleton.png)

<span data-ttu-id="09a72-117">Les valeurs numériques se trouvent dans la table [Windows. perception. People. HandJointKind](https://docs.microsoft.com/uwp/api/windows.perception.people.handjointkind)</span><span class="sxs-lookup"><span data-stu-id="09a72-117">The numerical values can be found in the table [Windows.Perception.People.HandJointKind](https://docs.microsoft.com/uwp/api/windows.perception.people.handjointkind)</span></span>
 
### <a name="functions"></a><span data-ttu-id="09a72-118">Fonctions</span><span class="sxs-lookup"><span data-stu-id="09a72-118">Functions</span></span>

<span data-ttu-id="09a72-119">Pour utiliser des fonctions de suivi des handles dans des plans, ouvrez « suivi de la main/réalité mixte Windows »</span><span class="sxs-lookup"><span data-stu-id="09a72-119">To use hand tracking functions in Blueprints, open "Hand Tracking/Windows Mixed Reality"</span></span>

![Suivi de main BP](images/unreal/hand-tracking-bp.png)

<span data-ttu-id="09a72-121">Pour les fonctions C++, incluez « WindowsMixedRealityHandTrackingFunctionLibrary. h »</span><span class="sxs-lookup"><span data-stu-id="09a72-121">For C++ functions, include "WindowsMixedRealityHandTrackingFunctionLibrary.h"</span></span>

<span data-ttu-id="09a72-122">BP</span><span class="sxs-lookup"><span data-stu-id="09a72-122">BP:</span></span>

![Prend en charge le BP de suivi de main](images/unreal/supports-hand-tracking-bp.png)
 
<span data-ttu-id="09a72-124">C++ :</span><span class="sxs-lookup"><span data-stu-id="09a72-124">C++:</span></span>
```cpp
static bool UWindowsMixedRealityHandTrackingFunctionLibrary::SupportsHandTracking()
```

<span data-ttu-id="09a72-125">Retourne la valeur true si le suivi des handles est pris en charge sur l’appareil, false si le suivi des mains n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="09a72-125">Returns true if hand tracking is supported on the device, false if hand tracking is not available.</span></span>

<span data-ttu-id="09a72-126">BP</span><span class="sxs-lookup"><span data-stu-id="09a72-126">BP:</span></span>

![Faire une transformation conjointe de la main](images/unreal/get-hand-joint-transform.png)
 
<span data-ttu-id="09a72-128">C++ :</span><span class="sxs-lookup"><span data-stu-id="09a72-128">C++:</span></span>
```cpp
static bool UWindowsMixedRealityHandTrackingFunctionLibrary::GetHandJointTransform(EControllerHand Hand, EWMRHandKeypoint Keypoint, FTransform& OutTransform, float& OutRadius)
```

<span data-ttu-id="09a72-129">Cette fonction retourne les données spatiales de la main.</span><span class="sxs-lookup"><span data-stu-id="09a72-129">This function returns spatial data of the hand.</span></span> <span data-ttu-id="09a72-130">Les données sont mises à jour chaque frame, à l’intérieur d’un frame, les valeurs retournées sont mises en cache.</span><span class="sxs-lookup"><span data-stu-id="09a72-130">The data updates every frame, inside a frame the returned values are cached.</span></span> <span data-ttu-id="09a72-131">Il n’est pas recommandé d’avoir une logique importante sur cette fonction pour des raisons de performances.</span><span class="sxs-lookup"><span data-stu-id="09a72-131">It is not recommended to have heavy logic on this function for performance reasons.</span></span> 

* <span data-ttu-id="09a72-132">À **la main de** l’utilisateur, peut être gauche ou droite</span><span class="sxs-lookup"><span data-stu-id="09a72-132">**Hand** – hand of the user, may be left or right</span></span>
* <span data-ttu-id="09a72-133">**KEYpoint** : le segment de la main.</span><span class="sxs-lookup"><span data-stu-id="09a72-133">**Keypoint** – the bone of the hand.</span></span> 
* <span data-ttu-id="09a72-134">**Transform** : coordonnées et orientation de la base du segment.</span><span class="sxs-lookup"><span data-stu-id="09a72-134">**Transform** – coordinates and orientation of bone’s base.</span></span> <span data-ttu-id="09a72-135">Pour obtenir les données de transformation pour la fin d’un segment, la base du segment suivant doit être demandée.</span><span class="sxs-lookup"><span data-stu-id="09a72-135">To get the transform data for the end of a bone, the base of the next bone should be requested.</span></span> <span data-ttu-id="09a72-136">Un segment de pourboire spécial offre une terminaison de distribution.</span><span class="sxs-lookup"><span data-stu-id="09a72-136">A special Tip bone gives end of distal.</span></span> 
* <span data-ttu-id="09a72-137">**Rayon** : rayon de la base du segment.</span><span class="sxs-lookup"><span data-stu-id="09a72-137">**Radius** — radius of the base of the bone.</span></span>
* <span data-ttu-id="09a72-138">**Valeur de retour** : true si le segment est suivi dans ce frame, false si le segment n’est pas suivi.</span><span class="sxs-lookup"><span data-stu-id="09a72-138">**Return Value** — true if the bone is tracked this frame, false if the bone is not tracked.</span></span>

## <a name="hand-live-link-animation"></a><span data-ttu-id="09a72-139">Animation de lien dynamique à la main</span><span class="sxs-lookup"><span data-stu-id="09a72-139">Hand Live Link Animation</span></span>
<span data-ttu-id="09a72-140">Les poses de main sont exposées à l’animation à l’aide du plug-in Live Link.</span><span class="sxs-lookup"><span data-stu-id="09a72-140">Hand poses are exposed to Animation using the Live Link plugin.</span></span> <span data-ttu-id="09a72-141">La documentation du plug-in est [ici](https://docs.unrealengine.com/en-US/Engine/Animation/LiveLinkPlugin/index.html)</span><span class="sxs-lookup"><span data-stu-id="09a72-141">The plugin documentation is [here](https://docs.unrealengine.com/en-US/Engine/Animation/LiveLinkPlugin/index.html)</span></span>

<span data-ttu-id="09a72-142">Si les plug-ins Windows Mixed Reality et Live Link sont activés, accédez à la **fenêtre > Live Link** pour ouvrir la fenêtre de l’éditeur de liens actifs.</span><span class="sxs-lookup"><span data-stu-id="09a72-142">If the Windows Mixed Reality and Live Link plugins are enabled, go to **Window > Live Link** to open the Live Link editor window.</span></span> <span data-ttu-id="09a72-143">Cliquez sur le **bouton + source** et activez la source de suivi de la main Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="09a72-143">Click the **+ Source button** and enable Windows Mixed Reality Hand Tracking Source</span></span>

![Source de la liaison dynamique](images/unreal/live-link-source.png)
 
<span data-ttu-id="09a72-145">Une fois que vous avez activé la source et ouvert une ressource d’animation, l’onglet Aperçu de la scène de l’animation présente les options supplémentaires suivantes (les détails se trouvent dans la documentation sur les liens dynamiques non réels, car le plug-in est en version bêta, le processus peut changer plus tard)</span><span class="sxs-lookup"><span data-stu-id="09a72-145">After you enable the source and open any animation asset, the Preview Scene tab of Animation will have the following additional options (the details are in Unreal’s Live Link documentation- as the plugin is in beta, the process may change later)</span></span>

![Animation des liens dynamiques](images/unreal/live-link-animation.png)
 
<span data-ttu-id="09a72-147">La hiérarchie d’animation manuelle est la même que dans EWMRHandKeypoint.</span><span class="sxs-lookup"><span data-stu-id="09a72-147">The hand animation hierarchy is the same as in EWMRHandKeypoint.</span></span> <span data-ttu-id="09a72-148">L’animation peut être reciblée à l’aide de WindowsMixedRealityHandTrackingLiveLinkRemapAsset.</span><span class="sxs-lookup"><span data-stu-id="09a72-148">Animation can be retargeted using WindowsMixedRealityHandTrackingLiveLinkRemapAsset.</span></span> 

![Animation de lien dynamique 2](images/unreal/live-link-animation2.png)
 
<span data-ttu-id="09a72-150">Il peut être sous-classé dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="09a72-150">It can be subclassed in the editor</span></span>

![Remappage de liaison dynamique](images/unreal/live-link-remap.png)
 
## <a name="hand-mesh"></a><span data-ttu-id="09a72-152">Maille manuelle</span><span class="sxs-lookup"><span data-stu-id="09a72-152">Hand Mesh</span></span>
<span data-ttu-id="09a72-153">Maille représentant les mains de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="09a72-153">Mesh representing the user hands.</span></span> 

![Maille manuelle](images/unreal/hand-mesh.png)
 
### <a name="how-to-enable-and-configure"></a><span data-ttu-id="09a72-155">Comment activer et configurer</span><span class="sxs-lookup"><span data-stu-id="09a72-155">How to enable and configure</span></span>

<span data-ttu-id="09a72-156">Les développeurs peuvent obtenir un accès direct à des mailles à la main pour leurs propres besoins.</span><span class="sxs-lookup"><span data-stu-id="09a72-156">Developers can get direct access to hand meshes for their own purposes.</span></span> <span data-ttu-id="09a72-157">Cet accès doit être activé dans ARSessionConfig : paramètres AR-> mappage universel-> générer des données de maillage à partir d’une géométrie suivie.</span><span class="sxs-lookup"><span data-stu-id="09a72-157">This access must be enabled in ARSessionConfig: AR Settings -> World Mapping -> Generate Mesh Data from Tracked Geometry.</span></span> 

<span data-ttu-id="09a72-158">Voici les paramètres par défaut des mailles :</span><span class="sxs-lookup"><span data-stu-id="09a72-158">Here are the default parameters for meshes:</span></span>

1.  <span data-ttu-id="09a72-159">Utiliser les données de maillage pour l’occlusion</span><span class="sxs-lookup"><span data-stu-id="09a72-159">Use Mesh Data for Occlusion</span></span>
2.  <span data-ttu-id="09a72-160">Générer une collision pour les données de maillage</span><span class="sxs-lookup"><span data-stu-id="09a72-160">Generate Collision for Mesh Data</span></span>
3.  <span data-ttu-id="09a72-161">Générer un maillage de navigation pour les données de maillage</span><span class="sxs-lookup"><span data-stu-id="09a72-161">Generate Nav Mesh for Mesh Data</span></span>
4.  <span data-ttu-id="09a72-162">Rendu des données de maillage dans le paramètre filaire – débogage qui affiche le maillage généré</span><span class="sxs-lookup"><span data-stu-id="09a72-162">Render Mesh Data in Wireframe – debug parameter that shows generated mesh</span></span>

<span data-ttu-id="09a72-163">Pour les projets de réalité mixte, ces valeurs de paramètre sont utilisées comme maillage de mappage spatial et par défaut.</span><span class="sxs-lookup"><span data-stu-id="09a72-163">For mixed reality projects, these parameter values will be used as the spatial mapping mesh and hand mesh defaults.</span></span> <span data-ttu-id="09a72-164">Les développeurs peuvent les modifier dans BP ou dans le code d’une maille particulière.</span><span class="sxs-lookup"><span data-stu-id="09a72-164">Developers can change them in BP or code for any particular mesh.</span></span>

### <a name="c-api-reference"></a><span data-ttu-id="09a72-165">Informations de référence sur l’API C++</span><span class="sxs-lookup"><span data-stu-id="09a72-165">C++ API Reference</span></span> 
```cpp
enum class EARObjectClassification : uint8
{
// other types 
    HandMesh,
};
```

<span data-ttu-id="09a72-166">Cette valeur est le maillage à la main entre tous les objets suivis.</span><span class="sxs-lookup"><span data-stu-id="09a72-166">This value is the hand mesh among all trackable objects.</span></span>

```cpp
class FARSupportInterface 
{
public:
// other params 
    DECLARE_AR_SI_DELEGATE_FUNCS(OnTrackableAdded)
    DECLARE_AR_SI_DELEGATE_FUNCS(OnTrackableUpdated)
    DECLARE_AR_SI_DELEGATE_FUNCS(OnTrackableRemoved)
};
```

<span data-ttu-id="09a72-167">Ces délégués sont appelés lorsque le système détecte tout objet suivi, y compris un maillage à la main.</span><span class="sxs-lookup"><span data-stu-id="09a72-167">These delegates are called when the system detects any trackable object, including a hand mesh.</span></span> 
```cpp
void UARHandMeshComponent::OnTrackableAdded(UARTrackedGeometry* Added)
```
<span data-ttu-id="09a72-168">Les gestionnaires des délégués doivent avoir la signature suivante :</span><span class="sxs-lookup"><span data-stu-id="09a72-168">Handlers to the delegates should have the following signature:</span></span>
```cpp
UMRMeshComponent* UARTrackedGeometry::GetUnderlyingMesh()
```

<span data-ttu-id="09a72-169">Les données de maillage sont accessibles par`UARTrackedGeometry::GetUnderlyingMesh`</span><span class="sxs-lookup"><span data-stu-id="09a72-169">Mesh data can be accessed by `UARTrackedGeometry::GetUnderlyingMesh`</span></span>

### <a name="blueprint-api-reference"></a><span data-ttu-id="09a72-170">Informations de référence sur l’API Blueprint</span><span class="sxs-lookup"><span data-stu-id="09a72-170">Blueprint API Reference</span></span>

<span data-ttu-id="09a72-171">Les développeurs doivent ajouter un composant Notify suivi d’AR à un acteur Blueprint</span><span class="sxs-lookup"><span data-stu-id="09a72-171">Developers should add an AR Trackable Notify Component to a Blueprint actor</span></span>

![Notification ARTrackable](images/unreal/ar-trackable-notify.png)
 
<span data-ttu-id="09a72-173">Accédez ensuite aux détails du composant</span><span class="sxs-lookup"><span data-stu-id="09a72-173">Then go to the component’s details</span></span> 

![ARTrackable Notify 2](images/unreal/ar-trackable-notify2.png)
 
<span data-ttu-id="09a72-175">Et remplacent sur Ajouter/mettre à jour/supprimer une géométrie suivie avec un code similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="09a72-175">And overwrite On Add/Update/Remove Tracked Geometry with code like the below:</span></span>

![Sur ARTrackable Notify](images/unreal/on-artrackable-notify.png)
 
## <a name="hand-rays"></a><span data-ttu-id="09a72-177">Rayons de main</span><span class="sxs-lookup"><span data-stu-id="09a72-177">Hand Rays</span></span>

<span data-ttu-id="09a72-178">Les développeurs peuvent utiliser un rayon main comme dispositif de pointage.</span><span class="sxs-lookup"><span data-stu-id="09a72-178">Developers can use a hand ray as a pointing device.</span></span> <span data-ttu-id="09a72-179">Le système est disponible en C++ et Blueprint.</span><span class="sxs-lookup"><span data-stu-id="09a72-179">The system is available in C++ and Blueprint.</span></span> <span data-ttu-id="09a72-180">Techniquement, il expose [Windows. UI. Input. spatial. SpatialPointerInteractionSourcePose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerinteractionsourcepose)</span><span class="sxs-lookup"><span data-stu-id="09a72-180">Technically it exposes [Windows.UI.Input.Spatial.SpatialPointerInteractionSourcePose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerinteractionsourcepose)</span></span>

<span data-ttu-id="09a72-181">Il est important de mentionner que, étant donné que les résultats de toutes les fonctions changent chaque image, elles sont toutes rendues accessibles.</span><span class="sxs-lookup"><span data-stu-id="09a72-181">It’s important to mention that since the results of all the functions changes every frame, they are all made callable.</span></span> <span data-ttu-id="09a72-182">Pour plus d’informations sur les fonctions pures et impures [ou pouvant être](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Functions/index.html#purevs.impure) appelées, consultez</span><span class="sxs-lookup"><span data-stu-id="09a72-182">For more information about pure vs impure or callable functions, see [that](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Functions/index.html#purevs.impure)</span></span>

<span data-ttu-id="09a72-183">Pour Blueprint, ouvrez « Windows Mixed Reality HMD »</span><span class="sxs-lookup"><span data-stu-id="09a72-183">For Blueprint open “Windows Mixed Reality HMD”</span></span>

![Rayons main BP](images/unreal/hand-rays-bp.png)
 
<span data-ttu-id="09a72-185">Pour C++, incluez « WindowsMixedRealityFunctionLibrary. h »</span><span class="sxs-lookup"><span data-stu-id="09a72-185">For C++ include "WindowsMixedRealityFunctionLibrary.h"</span></span>

### <a name="enum"></a><span data-ttu-id="09a72-186">Enum</span><span class="sxs-lookup"><span data-stu-id="09a72-186">Enum</span></span>

![Boutons du contrôleur d’entrée](images/unreal/input-controller-buttons.png)
```cpp
enum class EHMDInputControllerButtons : uint8
{
    Select,
    Grasp,
//......
};
```
* <span data-ttu-id="09a72-188">**Select** -– l’utilisateur a déclenché l’événement Select, qui peut être déclenché dans HoloLens 2 par airtap ou en regard de la validation.</span><span class="sxs-lookup"><span data-stu-id="09a72-188">**Select** -– User triggered Select event, which can be triggered in HoloLens 2 by airtap or gaze and commit.</span></span> <span data-ttu-id="09a72-189">Une autre façon de déclencher cet événement est d’indiquer « Select ».</span><span class="sxs-lookup"><span data-stu-id="09a72-189">Another way to trigger this event is to say “Select”.</span></span> 
* <span data-ttu-id="09a72-190">**Saisissez** -– événement de préhension déclenché par l’utilisateur, qui est déclenché dans HoloLens 2 en fermant les doigts de l’utilisateur sur un hologramme.</span><span class="sxs-lookup"><span data-stu-id="09a72-190">**Grasp** -– User triggered Grasp event, which is triggered in HoloLens 2 by closing the user’s fingers on a hologram.</span></span> 
```cpp
enum class EHMDTrackingStatus : uint8
{
    NotTracked,
    //......
    Tracked
};
```
* <span data-ttu-id="09a72-191">**NotTracked** – la main n’est pas visible</span><span class="sxs-lookup"><span data-stu-id="09a72-191">**NotTracked** –- the hand isn’t visible</span></span>
* <span data-ttu-id="09a72-192">**Suivi** : la main est entièrement suivie</span><span class="sxs-lookup"><span data-stu-id="09a72-192">**Tracked** –- the hand is fully tracked</span></span>

### <a name="struct"></a><span data-ttu-id="09a72-193">Struct</span><span class="sxs-lookup"><span data-stu-id="09a72-193">Struct</span></span>

![Informations de pose du pointeur BP](images/unreal/pointer-pose-info-bp.png)
```cpp
struct FPointerPoseInfo
{
    FVector Origin;
    FVector Direction;
    FVector Up;
    FQuat Orientation;
    EHMDTrackingStatus TrackingStatus;
};
```
* <span data-ttu-id="09a72-195">**Origin** : origine de la main</span><span class="sxs-lookup"><span data-stu-id="09a72-195">**Origin** – origin of the hand</span></span>
* <span data-ttu-id="09a72-196">**Direction** : direction de la main</span><span class="sxs-lookup"><span data-stu-id="09a72-196">**Direction** – direction of the hand</span></span>
* <span data-ttu-id="09a72-197">**Haut** -vecteur de la main</span><span class="sxs-lookup"><span data-stu-id="09a72-197">**Up** – up vector of the hand</span></span>
* <span data-ttu-id="09a72-198">**Orientation** -Quaternion d’orientation</span><span class="sxs-lookup"><span data-stu-id="09a72-198">**Orientation** – orientation quaternion</span></span> 
* <span data-ttu-id="09a72-199">**État du suivi** – État du suivi actuel</span><span class="sxs-lookup"><span data-stu-id="09a72-199">**Tracking Status** – current tracking status</span></span>

### <a name="functions"></a><span data-ttu-id="09a72-200">Fonctions</span><span class="sxs-lookup"><span data-stu-id="09a72-200">Functions</span></span>

<span data-ttu-id="09a72-201">Toutes les fonctions doivent pouvoir être appelées sur chaque frame pour une surveillance continue.</span><span class="sxs-lookup"><span data-stu-id="09a72-201">All the functions should be callable on every frame for continuous monitoring.</span></span> 

![Obtient les informations de pose du pointeur](images/unreal/get-pointer-pose-info.png)
```cpp
static FPointerPoseInfo UWindowsMixedRealityFunctionLibrary::GetPointerPoseInfo(EControllerHand hand);
```
<span data-ttu-id="09a72-203">La fonction retourne les informations complètes sur la direction du rayon de la main dans ce frame.</span><span class="sxs-lookup"><span data-stu-id="09a72-203">The function returns the full information about the hand ray direction in this frame.</span></span> 

![Est saisi BP](images/unreal/is-grasped-bp.png)
```cpp
static bool UWindowsMixedRealityFunctionLibrary::IsGrasped(EControllerHand hand);
```
<span data-ttu-id="09a72-205">Retourne la valeur true si la main est saisie dans ce frame.</span><span class="sxs-lookup"><span data-stu-id="09a72-205">Returns true if the hand is grasped in this frame.</span></span> 

![Est sélectionner un fond de panier appuyé](images/unreal/is-select-pressed-bp.png)
```cpp
static bool UWindowsMixedRealityFunctionLibrary::IsSelectPressed(EControllerHand hand);
```
<span data-ttu-id="09a72-207">Retourne la valeur true si l’utilisateur a déclenché SELECT dans ce frame.</span><span class="sxs-lookup"><span data-stu-id="09a72-207">Returns true if the user triggered Select in this frame.</span></span>

![Clic sur le bouton de la BP](images/unreal/is-button-clicked-bp.png)
```cpp
static bool UWindowsMixedRealityFunctionLibrary::IsButtonClicked(EControllerHand hand, EHMDInputControllerButtons button);
```
<span data-ttu-id="09a72-209">Retourne la valeur true si l’événement/le bouton est déclenché dans ce frame.</span><span class="sxs-lookup"><span data-stu-id="09a72-209">Returns true if the event/button is triggered in this frame.</span></span>

![Obtient l’état du suivi du contrôleur BP](images/unreal/get-controller-tracking-status-bp.png)
```cpp
static EHMDTrackingStatus UWindowsMixedRealityFunctionLibrary::GetControllerTrackingStatus(EControllerHand hand);
```
<span data-ttu-id="09a72-211">Retourne l’état de suivi dans ce frame.</span><span class="sxs-lookup"><span data-stu-id="09a72-211">Returns the tracking status in this frame.</span></span>

## <a name="gestures"></a><span data-ttu-id="09a72-212">Mouvements</span><span class="sxs-lookup"><span data-stu-id="09a72-212">Gestures</span></span>

<span data-ttu-id="09a72-213">Hololens 2 peut suivre les gestes spatiaux.</span><span class="sxs-lookup"><span data-stu-id="09a72-213">The Hololens 2 can track spatial gestures.</span></span> <span data-ttu-id="09a72-214">Les détails de ces gestes sont [ici](https://docs.microsoft.com/hololens/hololens2-basic-usage) un développeur peut les capturer comme entrée dans leur application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="09a72-214">Details about these gestures are [here](https://docs.microsoft.com/hololens/hololens2-basic-usage) A developer can capture them as input to their mixed reality application.</span></span> 

<span data-ttu-id="09a72-215">La fonction C++ est dans « WindowsMixedRealitySpatialInputFunctionLibrary. h »</span><span class="sxs-lookup"><span data-stu-id="09a72-215">The C++ function is in "WindowsMixedRealitySpatialInputFunctionLibrary.h"</span></span>

<span data-ttu-id="09a72-216">La fonction Blueprint est dans une entrée spatiale Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="09a72-216">The Blueprint function is in Windows Mixed Reality Spatial Input</span></span>

![Capturer les gestes](images/unreal/capture-gestures.png)

### <a name="enum"></a><span data-ttu-id="09a72-218">Enum</span><span class="sxs-lookup"><span data-stu-id="09a72-218">Enum</span></span>

![Type de mouvement](images/unreal/gesture-type.png)
```cpp
enum class ESpatialInputAxisGestureType : uint8
{
    None = 0,
    Manipulation = 1,
    Navigation = 2,
    NavigationRails = 3
};
```
<span data-ttu-id="09a72-220">Cette énumération décrit les mouvements d’axe spatial.</span><span class="sxs-lookup"><span data-stu-id="09a72-220">This enum describes spatial axis gestures.</span></span> <span data-ttu-id="09a72-221">Vous pouvez en savoir plus à [ce sujet ici](holograms-211.md)</span><span class="sxs-lookup"><span data-stu-id="09a72-221">You can read about them [here](holograms-211.md)</span></span>

### <a name="function"></a><span data-ttu-id="09a72-222">Fonction</span><span class="sxs-lookup"><span data-stu-id="09a72-222">Function</span></span>

![Capturer les gestes BP](images/unreal/capture-gestures-bp.png)
```cpp
static bool UWindowsMixedRealitySpatialInputFunctionLibrary::CaptureGestures(
    bool Tap = false, 
    bool Hold = false, 
    ESpatialInputAxisGestureType AxisGesture = ESpatialInputAxisGestureType::None, 
    bool NavigationAxisX = true, 
    bool NavigationAxisY = true, 
    bool NavigationAxisZ = true);
```
<span data-ttu-id="09a72-224">La fonction active et désactive la capture des mouvements.</span><span class="sxs-lookup"><span data-stu-id="09a72-224">The function enables and disables capturing of gestures.</span></span> <span data-ttu-id="09a72-225">Les gestes activés déclenchent des événements d’entrée.</span><span class="sxs-lookup"><span data-stu-id="09a72-225">The enabled gestures fire input events.</span></span> <span data-ttu-id="09a72-226">Elle retourne la valeur true si l’activation de la capture de mouvement a réussi et false en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="09a72-226">It returns true if enabling gesture capture succeeded and false if there's an error.</span></span>
<span data-ttu-id="09a72-227">Événements clés</span><span class="sxs-lookup"><span data-stu-id="09a72-227">Key Events</span></span>

![Événements clés](images/unreal/key-events.png)

![Événements clés 2](images/unreal/key-events2.png)
```cpp
const FKey FSpatialInputKeys::TapGesture(TapGestureName);
const FKey FSpatialInputKeys::DoubleTapGesture(DoubleTapGestureName);
const FKey FSpatialInputKeys::HoldGesture(HoldGestureName);

const FKey FSpatialInputKeys::LeftTapGesture(LeftTapGestureName);
const FKey FSpatialInputKeys::LeftDoubleTapGesture(LeftDoubleTapGestureName);
const FKey FSpatialInputKeys::LeftHoldGesture(LeftHoldGestureName);

const FKey FSpatialInputKeys::RightTapGesture(RightTapGestureName);
const FKey FSpatialInputKeys::RightDoubleTapGesture(RightDoubleTapGestureName);
const FKey FSpatialInputKeys::RightHoldGesture(RightHoldGestureName);

const FKey FSpatialInputKeys::LeftManipulationGesture(LeftManipulationGestureName);
const FKey FSpatialInputKeys::LeftManipulationXGesture(LeftManipulationXGestureName);
const FKey FSpatialInputKeys::LeftManipulationYGesture(LeftManipulationYGestureName);
const FKey FSpatialInputKeys::LeftManipulationZGesture(LeftManipulationZGestureName);

const FKey FSpatialInputKeys::LeftNavigationGesture(LeftNavigationGestureName);
const FKey FSpatialInputKeys::LeftNavigationXGesture(LeftNavigationXGestureName);
const FKey FSpatialInputKeys::LeftNavigationYGesture(LeftNavigationYGestureName);
const FKey FSpatialInputKeys::LeftNavigationZGesture(LeftNavigationZGestureName);


const FKey FSpatialInputKeys::RightManipulationGesture(RightManipulationGestureName);
const FKey FSpatialInputKeys::RightManipulationXGesture(RightManipulationXGestureName);
const FKey FSpatialInputKeys::RightManipulationYGesture(RightManipulationYGestureName);
const FKey FSpatialInputKeys::RightManipulationZGesture(RightManipulationZGestureName);

const FKey FSpatialInputKeys::RightNavigationGesture(RightNavigationGestureName);
const FKey FSpatialInputKeys::RightNavigationXGesture(RightNavigationXGestureName);
const FKey FSpatialInputKeys::RightNavigationYGesture(RightNavigationYGestureName);
const FKey FSpatialInputKeys::RightNavigationZGesture(RightNavigationZGestureName);
```
<span data-ttu-id="09a72-230">Si le mouvement est activé, les événements commencent à se déclencher.</span><span class="sxs-lookup"><span data-stu-id="09a72-230">If the gesture is enabled, the events begin firing.</span></span> 

