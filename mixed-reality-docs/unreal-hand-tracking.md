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
# <a name="hand-tracking"></a>Suivi de la main

Le système de suivi de la main utilise les paumes et les doigts d’une personne en tant qu’entrée dans un environnement inréel. Un développeur peut obtenir la position et la rotation de chaque doigt, le Palm entier et même les gestes à utiliser dans leur propre code. 

## <a name="hand-pose"></a>Poser à la main

À l’aide de la pose, les développeurs peuvent suivre les mains et les doigts de l’utilisateur actif comme entrée. Ce système est exposé via les plans et C++. Les détails techniques se trouvent dans la classe WinRT correspondante [Windows. perception. People. HandPose](https://docs.microsoft.com/uwp/api/windows.perception.people.handpose) cette API inréelle fournit les données au format du système de coordonnées non réelles et les battements sont synchronisés avec le moteur inréel.

### <a name="enum"></a>Enum

EWMRHandKeypoint décrit la hiérarchie osseuse de la main. 

Blueprint

![Main KEYpoint BP](images/unreal/hand-keypoint-bp.png)
 
C++ :
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

Les valeurs numériques se trouvent dans la table [Windows. perception. People. HandJointKind](https://docs.microsoft.com/uwp/api/windows.perception.people.handjointkind)
 
### <a name="functions"></a>Fonctions

Pour utiliser des fonctions de suivi des handles dans des plans, ouvrez « suivi de la main/réalité mixte Windows »

![Suivi de main BP](images/unreal/hand-tracking-bp.png)

Pour les fonctions C++, incluez « WindowsMixedRealityHandTrackingFunctionLibrary. h »

BP

![Prend en charge le BP de suivi de main](images/unreal/supports-hand-tracking-bp.png)
 
C++ :
```cpp
static bool UWindowsMixedRealityHandTrackingFunctionLibrary::SupportsHandTracking()
```

Retourne la valeur true si le suivi des handles est pris en charge sur l’appareil, false si le suivi des mains n’est pas disponible.

BP

![Faire une transformation conjointe de la main](images/unreal/get-hand-joint-transform.png)
 
C++ :
```cpp
static bool UWindowsMixedRealityHandTrackingFunctionLibrary::GetHandJointTransform(EControllerHand Hand, EWMRHandKeypoint Keypoint, FTransform& OutTransform, float& OutRadius)
```

Cette fonction retourne les données spatiales de la main. Les données sont mises à jour chaque frame, à l’intérieur d’un frame, les valeurs retournées sont mises en cache. Il n’est pas recommandé d’avoir une logique importante sur cette fonction pour des raisons de performances. 

* À **la main de** l’utilisateur, peut être gauche ou droite
* **KEYpoint** : le segment de la main. 
* **Transform** : coordonnées et orientation de la base du segment. Pour obtenir les données de transformation pour la fin d’un segment, la base du segment suivant doit être demandée. Un segment de pourboire spécial offre une terminaison de distribution. 
* **Rayon** : rayon de la base du segment.
* **Valeur de retour** : true si le segment est suivi dans ce frame, false si le segment n’est pas suivi.

## <a name="hand-live-link-animation"></a>Animation de lien dynamique à la main
Les poses de main sont exposées à l’animation à l’aide du plug-in Live Link. La documentation du plug-in est [ici](https://docs.unrealengine.com/en-US/Engine/Animation/LiveLinkPlugin/index.html)

Si les plug-ins Windows Mixed Reality et Live Link sont activés, accédez à la **fenêtre > Live Link** pour ouvrir la fenêtre de l’éditeur de liens actifs. Cliquez sur le **bouton + source** et activez la source de suivi de la main Windows Mixed Reality.

![Source de la liaison dynamique](images/unreal/live-link-source.png)
 
Une fois que vous avez activé la source et ouvert une ressource d’animation, l’onglet Aperçu de la scène de l’animation présente les options supplémentaires suivantes (les détails se trouvent dans la documentation sur les liens dynamiques non réels, car le plug-in est en version bêta, le processus peut changer plus tard)

![Animation des liens dynamiques](images/unreal/live-link-animation.png)
 
La hiérarchie d’animation manuelle est la même que dans EWMRHandKeypoint. L’animation peut être reciblée à l’aide de WindowsMixedRealityHandTrackingLiveLinkRemapAsset. 

![Animation de lien dynamique 2](images/unreal/live-link-animation2.png)
 
Il peut être sous-classé dans l’éditeur.

![Remappage de liaison dynamique](images/unreal/live-link-remap.png)
 
## <a name="hand-mesh"></a>Maille manuelle
Maille représentant les mains de l’utilisateur. 

![Maille manuelle](images/unreal/hand-mesh.png)
 
### <a name="how-to-enable-and-configure"></a>Comment activer et configurer

Les développeurs peuvent obtenir un accès direct à des mailles à la main pour leurs propres besoins. Cet accès doit être activé dans ARSessionConfig : paramètres AR-> mappage universel-> générer des données de maillage à partir d’une géométrie suivie. 

Voici les paramètres par défaut des mailles :

1.  Utiliser les données de maillage pour l’occlusion
2.  Générer une collision pour les données de maillage
3.  Générer un maillage de navigation pour les données de maillage
4.  Rendu des données de maillage dans le paramètre filaire – débogage qui affiche le maillage généré

Pour les projets de réalité mixte, ces valeurs de paramètre sont utilisées comme maillage de mappage spatial et par défaut. Les développeurs peuvent les modifier dans BP ou dans le code d’une maille particulière.

### <a name="c-api-reference"></a>Informations de référence sur l’API C++ 
```cpp
enum class EARObjectClassification : uint8
{
// other types 
    HandMesh,
};
```

Cette valeur est le maillage à la main entre tous les objets suivis.

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

Ces délégués sont appelés lorsque le système détecte tout objet suivi, y compris un maillage à la main. 
```cpp
void UARHandMeshComponent::OnTrackableAdded(UARTrackedGeometry* Added)
```
Les gestionnaires des délégués doivent avoir la signature suivante :
```cpp
UMRMeshComponent* UARTrackedGeometry::GetUnderlyingMesh()
```

Les données de maillage sont accessibles par`UARTrackedGeometry::GetUnderlyingMesh`

### <a name="blueprint-api-reference"></a>Informations de référence sur l’API Blueprint

Les développeurs doivent ajouter un composant Notify suivi d’AR à un acteur Blueprint

![Notification ARTrackable](images/unreal/ar-trackable-notify.png)
 
Accédez ensuite aux détails du composant 

![ARTrackable Notify 2](images/unreal/ar-trackable-notify2.png)
 
Et remplacent sur Ajouter/mettre à jour/supprimer une géométrie suivie avec un code similaire à ce qui suit :

![Sur ARTrackable Notify](images/unreal/on-artrackable-notify.png)
 
## <a name="hand-rays"></a>Rayons de main

Les développeurs peuvent utiliser un rayon main comme dispositif de pointage. Le système est disponible en C++ et Blueprint. Techniquement, il expose [Windows. UI. Input. spatial. SpatialPointerInteractionSourcePose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerinteractionsourcepose)

Il est important de mentionner que, étant donné que les résultats de toutes les fonctions changent chaque image, elles sont toutes rendues accessibles. Pour plus d’informations sur les fonctions pures et impures [ou pouvant être](https://docs.unrealengine.com/en-US/Engine/Blueprints/UserGuide/Functions/index.html#purevs.impure) appelées, consultez

Pour Blueprint, ouvrez « Windows Mixed Reality HMD »

![Rayons main BP](images/unreal/hand-rays-bp.png)
 
Pour C++, incluez « WindowsMixedRealityFunctionLibrary. h »

### <a name="enum"></a>Enum

![Boutons du contrôleur d’entrée](images/unreal/input-controller-buttons.png)
```cpp
enum class EHMDInputControllerButtons : uint8
{
    Select,
    Grasp,
//......
};
```
* **Select** -– l’utilisateur a déclenché l’événement Select, qui peut être déclenché dans HoloLens 2 par airtap ou en regard de la validation. Une autre façon de déclencher cet événement est d’indiquer « Select ». 
* **Saisissez** -– événement de préhension déclenché par l’utilisateur, qui est déclenché dans HoloLens 2 en fermant les doigts de l’utilisateur sur un hologramme. 
```cpp
enum class EHMDTrackingStatus : uint8
{
    NotTracked,
    //......
    Tracked
};
```
* **NotTracked** – la main n’est pas visible
* **Suivi** : la main est entièrement suivie

### <a name="struct"></a>Struct

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
* **Origin** : origine de la main
* **Direction** : direction de la main
* **Haut** -vecteur de la main
* **Orientation** -Quaternion d’orientation 
* **État du suivi** – État du suivi actuel

### <a name="functions"></a>Fonctions

Toutes les fonctions doivent pouvoir être appelées sur chaque frame pour une surveillance continue. 

![Obtient les informations de pose du pointeur](images/unreal/get-pointer-pose-info.png)
```cpp
static FPointerPoseInfo UWindowsMixedRealityFunctionLibrary::GetPointerPoseInfo(EControllerHand hand);
```
La fonction retourne les informations complètes sur la direction du rayon de la main dans ce frame. 

![Est saisi BP](images/unreal/is-grasped-bp.png)
```cpp
static bool UWindowsMixedRealityFunctionLibrary::IsGrasped(EControllerHand hand);
```
Retourne la valeur true si la main est saisie dans ce frame. 

![Est sélectionner un fond de panier appuyé](images/unreal/is-select-pressed-bp.png)
```cpp
static bool UWindowsMixedRealityFunctionLibrary::IsSelectPressed(EControllerHand hand);
```
Retourne la valeur true si l’utilisateur a déclenché SELECT dans ce frame.

![Clic sur le bouton de la BP](images/unreal/is-button-clicked-bp.png)
```cpp
static bool UWindowsMixedRealityFunctionLibrary::IsButtonClicked(EControllerHand hand, EHMDInputControllerButtons button);
```
Retourne la valeur true si l’événement/le bouton est déclenché dans ce frame.

![Obtient l’état du suivi du contrôleur BP](images/unreal/get-controller-tracking-status-bp.png)
```cpp
static EHMDTrackingStatus UWindowsMixedRealityFunctionLibrary::GetControllerTrackingStatus(EControllerHand hand);
```
Retourne l’état de suivi dans ce frame.

## <a name="gestures"></a>Mouvements

Hololens 2 peut suivre les gestes spatiaux. Les détails de ces gestes sont [ici](https://docs.microsoft.com/hololens/hololens2-basic-usage) un développeur peut les capturer comme entrée dans leur application de réalité mixte. 

La fonction C++ est dans « WindowsMixedRealitySpatialInputFunctionLibrary. h »

La fonction Blueprint est dans une entrée spatiale Windows Mixed Reality

![Capturer les gestes](images/unreal/capture-gestures.png)

### <a name="enum"></a>Enum

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
Cette énumération décrit les mouvements d’axe spatial. Vous pouvez en savoir plus à [ce sujet ici](holograms-211.md)

### <a name="function"></a>Fonction

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
La fonction active et désactive la capture des mouvements. Les gestes activés déclenchent des événements d’entrée. Elle retourne la valeur true si l’activation de la capture de mouvement a réussi et false en cas d’erreur.
Événements clés

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
Si le mouvement est activé, les événements commencent à se déclencher. 

