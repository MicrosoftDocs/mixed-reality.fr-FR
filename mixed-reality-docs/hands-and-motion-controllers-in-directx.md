---
title: Contrôleurs mains et motion dans DirectX
description: Guide du développeur pour utiliser le suivi des mains et les contrôleurs de mouvement dans les applications DirectX natives.
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/30/2019
ms.topic: article
keywords: mains, contrôleurs de mouvement, DirectX, entrée, hologrammes
ms.openlocfilehash: 08666c8c26cd4851c0c003a96a9e96d7a90228ac
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629642"
---
# <a name="hands-and-motion-controllers-in-directx"></a>Contrôleurs mains et motion dans DirectX

Dans Windows Mixed Reality, les entrées de la main et du [contrôleur de mouvement](motion-controllers.md) sont gérées via les API d’entrée spatiale, qui se trouvent dans l’espace de noms [Windows. UI. Input. spatial](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial) . Cela vous permet de gérer facilement des actions courantes telles que la **sélection** de la même façon sur les deux mains et les contrôleurs de mouvement.

## <a name="getting-started"></a>Prise en main

Pour accéder aux entrées spatiales dans Windows Mixed Reality, commencez par l’interface SpatialInteractionManager.  Vous pouvez accéder à cette interface en appelant [SpatialInteractionManager:: GetForCurrentView](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.getforcurrentview), généralement au cours du démarrage de l’application.

```cpp
using namespace winrt::Windows::UI::Input::Spatial;

SpatialInteractionManager interactionManager = SpatialInteractionManager::GetForCurrentView();
```

Le travail du SpatialInteractionManager consiste à fournir l’accès à [SpatialInteractionSources](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource), qui représente une source d’entrée.  Il existe trois types de SpatialInteractionSources disponibles dans le système.
* La **main** représente la main détectée d’un utilisateur. Les sources de main offrent différentes fonctionnalités basées sur l’appareil, allant des gestes de base sur HoloLens au suivi complet sur HoloLens 2. 
* Le **contrôleur** représente un contrôleur de mouvement jumelé. Les contrôleurs de mouvement peuvent offrir un large éventail de fonctionnalités.  Exemple : Sélectionnez les déclencheurs, les boutons de menu, les boutons de sélection, les pavés tactiles et Thumbsticks.
* La **voix** représente les mots-clés détectés par le système vocal de l’utilisateur. Par exemple, cette source injecte une pression SELECT et une mise en sortie chaque fois que l’utilisateur dit «Select».

Les données par trame pour une source sont représentées par l’interface [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) . Il existe deux façons d’accéder à ces données, selon que vous souhaitez utiliser un modèle piloté par des événements ou basé sur l’interrogation dans votre application.

### <a name="event-driven-input"></a>Entrée pilotée par les événements
SpatialInteractionManager fournit un certain nombre d’événements que votre application peut écouter.  Voici quelques exemples: [SourcePressed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed), [SourceReleased](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcereleased) et [SourceUpdated](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourceupdated).

Par exemple, le code suivant raccorde un gestionnaire d’événements appelé MyApp:: OnSourcePressed à l’événement SourcePressed.  Cela permet à votre application de détecter les presses sur n’importe quel type de source d’interaction.

```cpp
using namespace winrt::Windows::UI::Input::Spatial;

auto interactionManager = SpatialInteractionManager::GetForCurrentView();
interactionManager.SourcePressed({ this, &MyApp::OnSourcePressed });

```

Cet événement appuyé est envoyé à votre application de manière asynchrone, avec les SpatialInteractionSourceState correspondants au moment où la pression s’est produite. Votre application ou moteur de jeu peut effectuer un traitement immédiatement ou vous pouvez mettre en file d’attente les données d’événement dans votre routine de traitement d’entrée. Voici une fonction de gestionnaire d’événements pour l’événement SourcePressed, qui montre comment vérifier si l’utilisateur a cliqué sur le bouton de sélection.

```cpp
using namespace winrt::Windows::UI::Input::Spatial;

void MyApp::OnSourcePressed(SpatialInteractionManager const& sender, SpatialInteractionSourceEventArgs const& args)
{
    if (args.PressKind() == SpatialInteractionPressKind::Select)
    {
        // Select button was pressed, update app state
    }
}
```

Le code ci-dessus vérifie uniquement l’appui sur «Select», qui correspond à l’action principale sur l’appareil. Les exemples incluent la réalisation d’un AirTap sur HoloLens ou l’extraction du déclencheur sur un contrôleur de mouvement.  Les presses «Select» représentent l’intention de l’utilisateur d’activer l’hologramme qu’il cible.  L’événement SourcePressed se déclenche pour un certain nombre de boutons et de mouvements différents. vous pouvez inspecter les autres propriétés sur le SpatialInteractionSource pour tester ces cas-là.

### <a name="polling-based-input"></a>Entrée basée sur l’interrogation
Vous pouvez également utiliser SpatialInteractionManager pour interroger l’état actuel de l’entrée dans chaque cadre.  Pour ce faire, appelez simplement [GetDetectedSourcesAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.getdetectedsourcesattimestamp) chaque frame.  Cette fonction retourne un tableau contenant un [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) pour chaque [SpatialInteractionSource](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource)actif. Cela signifie un pour chaque contrôleur de mouvement actif, un pour chaque main suivie et un pour la parole si une commande «Select» a été récemment mise en circulation. Vous pouvez ensuite inspecter les propriétés sur chaque SpatialInteractionSourceState pour piloter l’entrée dans votre application. 

Voici un exemple de vérification de l’action «Select» à l’aide de la méthode d’interrogation. Notez que la  variable de prédiction représente un objet [HolographicFramePrediction](https://docs.microsoft.com/en-us/uwp/api/Windows.Graphics.Holographic.HolographicFramePrediction) , qui peut être obtenu à partir du [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe).

```cpp
using namespace winrt::Windows::UI::Input::Spatial;

auto interactionManager = SpatialInteractionManager::GetForCurrentView();
auto sourceStates = m_spatialInteractionManager.GetDetectedSourcesAtTimestamp(prediction.Timestamp());

for (auto& sourceState : sourceStates)
{
    if (sourceState.IsSelectPressed())
    {
        // Select button is down, update app state
    }
}
```

Chaque SpatialInteractionSource a un ID, que vous pouvez utiliser pour identifier les nouvelles sources et mettre en corrélation les sources existantes d’une image à l’autre.  Les mains reçoivent un nouvel ID à chaque fois qu’ils sortent et entrent dans l’angle de la connexion, mais les ID de contrôleur restent statiques pendant toute la durée de la session.  Vous pouvez utiliser les événements sur SpatialInteractionManager tels que [SourceDetected](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcedetected) et [SourceLost](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcelost), pour réagir quand les mains entrent ou quittent la vue de l’appareil, ou lorsque les contrôleurs de mouvement sont activés/désactivés ou sont jumelés/non couplés.

### <a name="predicted-vs-historical-poses"></a>Différences entre les poses prédites et l’historique
Notez que GetDetectedSourcesAtTimestamp a un paramètre timestamp. Cela vous permet de demander l’État et de créer des données qui sont prédites ou historiques, ce qui vous permet de mettre en corrélation les interactions spatiales avec d’autres sources d’entrée. Par exemple, lors du rendu de la position de la main dans le frame actuel, vous pouvez transmettre l’horodatage prédit fourni par [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe). Cela permet au système de prédire la position de la main pour s’aligner étroitement avec la sortie du frame rendu, réduisant ainsi la latence perçue.

Toutefois, une telle pose prédite ne produit pas de rayon de pointage idéal pour le ciblage avec une source d’interaction. Par exemple, quand vous appuyez sur un bouton de contrôleur de mouvement, il peut s’écouler jusqu’à 20 ms pour que cet événement se propage via Bluetooth au système d’exploitation. De même, une fois qu’un utilisateur a effectué un mouvement manuel, un certain laps de temps peut s’écouler avant que le système ne détecte le geste et que votre application l’interroge. Au moment où votre application interroge une modification d’État, les points de vue et de main sont utilisés pour cibler cette interaction qui s’est effectivement produite dans le passé. Si vous ciblez en passant l’horodatage de votre HolographicFrame actuel à GetDetectedSourcesAtTimestamp, le pose sera au contraire prévisible dans le rayon cible au moment de l’affichage de l’image, ce qui peut être supérieur à 20 ms dans le futur. Ce nouveau point est idéal pour le *rendu* de la source d’interaction, mais il compose notre problème de temps pour *cibler* l’interaction, car le ciblage de l’utilisateur s’est produit dans le passé.

Heureusement, les événements [SourcePressed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed), [SourceReleased](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcereleased) et [SourceUpdated](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourceupdated) fournissent l' [État](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourceeventargs.state) historique associé à chaque événement d’entrée.  Cela comprend directement les mises à disposition de l’historique et des handles disponibles via [TryGetPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose), ainsi qu’un [horodateur](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.timestamp) historique que vous pouvez transmettre à d’autres API pour établir une corrélation avec cet événement.

Cela entraîne les meilleures pratiques suivantes lors du rendu et du ciblage avec les mains et les contrôleurs de chaque cadre:
* Pour le rendu de la **main/du contrôleur** de chaque trame, votre application doit interroger la partie préprédite de chaque source d’interaction au moment de la photonique du frame actuel.  Vous pouvez interroger toutes les sources d’interaction en appelant [GetDetectedSourcesAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.getdetectedsourcesattimestamp) chaque frame, en transmettant l’horodatage prédit fourni par [HolographicFrame:: CurrentPrediction](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe.currentprediction).
* Pour le ciblage de la **main/du contrôleur** sur une presse ou une mise en version, votre application doit gérer les **événements**appuyés/libérés, Raycasting en fonction de la position de l' **historique** ou de la main pour cet événement. Pour ce faire, vous devez gérer l’événement [SourcePressed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed) ou [SourceReleased](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcereleased) , obtenir la propriété [State](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourceeventargs.state) à partir des arguments d’événement, puis appeler sa méthode [TryGetPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose) .

## <a name="cross-device-input-properties"></a>Propriétés d’entrée entre appareils
L’API SpatialInteractionSource prend en charge les contrôleurs et les systèmes de suivi de main avec un large éventail de fonctionnalités. Un certain nombre de ces fonctionnalités sont communes entre les types d’appareils. Par exemple, le suivi des mains et les contrôleurs de mouvement fournissent tous deux une action «sélectionner» et une position 3D. Dans la mesure du possible, l’API mappe ces fonctionnalités communes aux mêmes propriétés sur le SpatialInteractionSource.  Cela permet aux applications de prendre en charge plus facilement un large éventail de types d’entrée. Le tableau suivant décrit les propriétés prises en charge et leur comparaison entre les types d’entrée.

| Propriété | Description | Gestes HoloLens | Contrôleurs de mouvement | Mains articulées|
|--- |--- |--- |--- |--- |
| [SpatialInteractionSource::**main**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource.handedness) | La main droite ou gauche/le contrôleur. | Non pris en charge | Pris en charge | Pris en charge |
| [SpatialInteractionSourceState::**IsSelectPressed**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.isselectpressed) | État actuel du bouton principal. | Robinet d’air | Déclencheur | Robinet à air lâche (pincement vertical) |
| [SpatialInteractionSourceState::**IsGrasped**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.isgrasped) | État actuel du bouton de manipulation. | Non pris en charge | Bouton de manipulation | Pincer ou fermer la main |
| [SpatialInteractionSourceState::**IsMenuPressed**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.ismenupressed) | État actuel du bouton de menu.    | Non pris en charge | Bouton de menu | Non pris en charge |
| [SpatialInteractionSourceLocation::**position**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcelocation.position) | Emplacement XYZ de la main ou de la position de la poignée sur le contrôleur. | Emplacement Palm | Poignée de pose position | Emplacement Palm |
| [SpatialInteractionSourceLocation::**orientation**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcelocation.orientation) | Quaternion représentant l’orientation de la main ou de la poignée sur le contrôleur. | Non pris en charge | Poignée d’orientation de pose | Orientation Palm |
| [SpatialPointerInteractionSourcePose::**position**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerinteractionsourcepose.position#Windows_UI_Input_Spatial_SpatialPointerInteractionSourcePose_Position) | Origine du rayon de pointage. | Non pris en charge | Pris en charge | Pris en charge |
| [SpatialPointerInteractionSourcePose::**ForwardDirection**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerinteractionsourcepose.forwarddirection#Windows_UI_Input_Spatial_SpatialPointerInteractionSourcePose_ForwardDirection) | Direction du rayon de pointage. | Non pris en charge | Pris en charge | Pris en charge |

Certaines des propriétés ci-dessus ne sont pas disponibles sur tous les appareils, et l’API fournit un moyen de les tester. Par exemple, vous pouvez inspecter la propriété [SpatialInteractionSource:: IsGraspSupported](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource.isgraspsupported) pour déterminer si la source fournit une action saisissante.

### <a name="grip-pose-vs-pointing-pose"></a>Poignée de pose et pose de pointage

Windows Mixed Reality prend en charge les contrôleurs de mouvement dans un large éventail de facteurs de forme.  Il prend également en charge les systèmes de suivi articulés.  Tous ces systèmes ont des relations différentes entre la position de la main et la direction «avant» naturelle que les applications doivent utiliser pour pointer ou rendreing des objets dans la main de l’utilisateur.  Pour prendre en charge tout cela, il existe deux types de poses 3D fournis pour le suivi des mains et les contrôleurs de mouvement.  La première est la poignée, qui représente la position de l’utilisateur.  Le deuxième point de pose, qui représente un rayon de pointage provenant de la main ou du contrôleur de l’utilisateur. Par conséquent, si vous souhaitez afficher **la main de l’utilisateur** ou **un objet détenu par l’utilisateur**, tel qu’un épée ou un pistolet, utilisez la poignée. Si vous souhaitez raycast du contrôleur ou de la main, par exemple lorsque l’utilisateur **pointe sur l’interface utilisateur** , utilisez le point de pose.

Vous pouvez accéder à la **poignée** à l’aide de [SpatialInteractionSourceState::P ropriétés:: TryGetLocation (...)](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourceproperties.trygetlocation#Windows_UI_Input_Spatial_SpatialInteractionSourceProperties_TryGetLocation_Windows_Perception_Spatial_SpatialCoordinateSystem_).  Il est défini comme suit:
* Position de la **poignée**: Le centre de la poche quand il maintient le contrôleur naturellement, ajusté à gauche ou à droite pour centrer la position au sein de la poignée.
* **Axe droit de l’orientation de la poignée**: Lorsque vous ouvrez complètement votre main pour former une pose plate à 5 doigts, le rayon normal à votre Palm (à partir de la poche de gauche, en arrière depuis la paume de droite)
* **Axe vers l’avant de l’orientation de la poignée**: Lorsque vous fermez partiellement votre main (comme si vous détenir le contrôleur), le rayon qui pointe vers l’avant dans le tube formé par vos doigts non thumbs.
* **Axe vers le haut de l’orientation de la poignée**: Axe vers le haut impliqué par les définitions Right et Forward.

Vous pouvez accéder à la **pose du pointeur** par le biais de [SpatialInteractionSourceState::P ropriétés:: TryGetLocation (...):: SourcePointerPose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsourcelocation#Windows_UI_Input_Spatial_SpatialInteractionSourceLocation_SourcePointerPose) ou [SpatialInteractionSourceState:: TryGetPointerPose (...):: TryGetInteractionSourcePose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerpose#Windows_UI_Input_Spatial_SpatialPointerPose_TryGetInteractionSourcePose_Windows_UI_Input_Spatial_SpatialInteractionSource_) .

## <a name="controller-specific-input-properties"></a>Propriétés d’entrée spécifiques au contrôleur
Pour les contrôleurs, SpatialInteractionSource a une propriété de contrôleur avec des fonctionnalités supplémentaires.
* **HasThumbstick:** Si la valeur est true, le contrôleur a un stick analogique. Inspectez la propriété [ControllerProperties](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractioncontrollerproperties) de SpatialInteractionSourceState pour obtenir les valeurs de stick analogique x et y (ThumbstickX et ThumbstickY), ainsi que l’état enfoncé (IsThumbstickPressed).
* **HasTouchpad:** Si la valeur est true, le contrôleur a un pavé tactile. Inspectez la propriété ControllerProperties de SpatialInteractionSourceState pour obtenir les valeurs de pavé tactile x et y (TouchpadX et touchpad) et savoir si l’utilisateur touche le bloc (IsTouchpadTouched) et s’il appuie sur le pavé tactile ( IsTouchpadPressed).
* **SimpleHapticsController:** L’API SimpleHapticsController pour le contrôleur vous permet d’inspecter les fonctionnalités haptique du contrôleur et vous permet également de contrôler les commentaires haptique.

Notez que la plage du pavé tactile et du stick analogique est comprise entre-1 et 1 pour les deux axes (de bas en haut et de gauche à droite). La plage du déclencheur analogique, accessible à l’aide de la propriété SpatialInteractionSourceState:: SelectPressedValue, a une plage comprise entre 0 et 1. La valeur 1 est corrélée avec IsSelectPressed égal à true; toute autre valeur est corrélée avec IsSelectPressed égal à false.

## <a name="articulated-hand-tracking"></a>Suivi articulé
L’API Windows Mixed Reality assure une prise en charge complète du suivi articulé, par exemple sur HoloLens 2. Le suivi articulé peut être utilisé pour implémenter la manipulation directe et les modèles d’entrée de point et de validation dans vos applications. Il peut également être utilisé pour créer des interactions entièrement personnalisées.

### <a name="hand-skeleton"></a>Squelette de main
Le suivi articulé fournit un squelette de 25 jointures qui permet de nombreux types différents d’interactions.  La structure fournit 5 jointures pour l’index, le milieu/l’anneau, les 4 jointures pour le pouce et le poignet.  L’articulation du poignet sert de base de la hiérarchie. L’image suivante illustre la disposition du squelette.

![Squelette de main](images/hand-skeleton.png)

Dans la plupart des cas, chaque joint est nommé en fonction du segment qu’il représente.  Étant donné qu’il y a deux segments à chaque articulation, nous utilisons une convention pour nommer chaque jointure en fonction du segment enfant à cet emplacement.  Le segment enfant est défini comme le segment du poignet.  Par exemple, l’articulation «index proximal» contient la position de début de l’index de l’OS proximal et l’orientation de ce segment.  Il ne contient pas la position de fin du segment.  Si vous en avez besoin, vous pouvez le faire à partir de la jointure suivante dans la hiérarchie, l’articulation «index intermédiaire».

Outre les 25 articulations hiérarchiques, le système fournit un joint Palm.  Le Palm n’est généralement pas considéré comme faisant partie de la structure squelettique.  Elle est fournie uniquement comme un moyen pratique d’obtenir la position et l’orientation globales de la main.

Les informations suivantes sont fournies pour chaque jointure:

| Nom | Description |
|--- |--- |
|Position | position 3D de la jointure, disponible dans n’importe quel système de coordonnées demandé. |
|Orientation | orientation 3D du segment, disponible dans n’importe quel système de coordonnées demandé. |
|Rayon | Distance à la surface de l’apparence à la position conjointe. Utile pour le paramétrage des interactions directes ou des visualisations qui reposent sur la largeur du doigt. |
|Précision | Fournit une indication sur la confiance que le système estime sur les informations de cette articulation. |

Vous pouvez accéder aux données squelettes à l’aide d’une fonction sur le [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate).  La fonction est appelée [TryGetHandPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygethandpose#Windows_UI_Input_Spatial_SpatialInteractionSourceState_TryGetHandPose)et retourne un objet appelé [HandPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handpose).  Si la source ne prend pas en charge les mains articulées, cette fonction retournera la valeur null.  Une fois que vous disposez d’un HandPose, vous pouvez obtenir les données communes actuelles en appelant [TryGetJoint](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handpose.trygetjoint#Windows_Perception_People_HandPose_TryGetJoint_Windows_Perception_Spatial_SpatialCoordinateSystem_Windows_Perception_People_HandJointKind_Windows_Perception_People_JointPose__), avec le nom de la jointure qui vous intéresse.  Les données sont retournées sous la forme d’une structure [JointPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.jointpose) .  Le code suivant obtient la position de l’info-bulle de l’index. La variable *CurrentState* représente une instance de [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate).

```cpp
using namespace winrt::Windows::Perception::People;
using namespace winrt::Windows::Foundation::Numerics;

auto handPose = currentState.TryGetHandPose();
if (handPose)
{
    JointPose joint;
    if (handPose.TryGetJoint(desiredCoordinateSystem, HandJointKind::IndexTip, joint))
    {
        float3 indexTipPosition = joint.Position;

        // Do something with the index tip position
    }
}
```

### <a name="hand-mesh"></a>Maille manuelle

L’API de suivi articulé permet d’obtenir un maillage de handles de triangle entièrement déformable.  Ce maillage peut se déformer en temps réel, ainsi que le squelette de la main, et est utile pour la visualisation, ainsi que pour les techniques de physique avancées.  Pour accéder à la maille manuelle, vous devez d’abord créer un objet [HandMeshObserver](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handmeshobserver) en appelant [TryCreateHandMeshObserverAsync](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource.trycreatehandmeshobserverasync) sur [SpatialInteractionSource](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource).  Cette opération ne doit être effectuée qu’une seule fois par source, généralement la première fois que vous la voyez.  Cela signifie que vous appellerez cette fonction pour créer un objet HandMeshObserver chaque fois qu’une main entre dans l’angle de la montre.  Notez qu’il s’agit d’une fonction Async. vous devrez donc traiter un peu d’accès concurrentiel ici.  Une fois disponible, vous pouvez demander à l’objet HandMeshObserver pour la mémoire tampon d’index de triangle en appelant [GetTriangleIndices](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handmeshobserver.gettriangleindices#Windows_Perception_People_HandMeshObserver_GetTriangleIndices_System_UInt16___).  Les index ne changent pas le frame sur le frame, ce qui vous permet de les obtenir et de les mettre en cache pendant la durée de vie de la source.  Les index sont fournis dans l’ordre d’enroulement dans le sens des aiguilles d’une montre.

Le code suivant permet de tourner un std:: thread détaché pour créer l’observateur de maillage et d’extraire le tampon d’index une fois que l’observateur de maillage est disponible.  Il démarre à partir d’une variable appelée *CurrentState*, qui est une instance de [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) représentant une main.

```cpp
using namespace Windows::Perception::People;

std::thread createObserverThread([this, currentState]()
{
    HandMeshObserver newHandMeshObserver = currentState.Source().TryCreateHandMeshObserverAsync().get();
    if (newHandMeshObserver)
    {
        unsigned indexCount = newHandMeshObserver.TriangleIndexCount();
        vector<unsigned short> indices(indexCount);
        newHandMeshObserver.GetTriangleIndices(indices);

        // Save the indices and handMeshObserver for later use - and use a mutex to synchronize access if needed!
     }
});
createObserverThread.detach();
```
Le démarrage d’un thread détaché n’est qu’une option pour gérer les appels asynchrones.  Vous pouvez également utiliser la nouvelle fonctionnalité [co_await](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) prise en charge par C++/WinRT.

Une fois que vous avez un objet HandMeshObserver, vous devez le conserver pendant la durée pendant laquelle son SpatialInteractionSource correspondant est actif.  Ensuite, chaque frame, vous pouvez lui demander la dernière mémoire tampon de vertex qui représente la main en appelant [GetVertexStateForPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handmeshobserver.getvertexstateforpose) et en passant une instance [HandPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handpose) qui représente le pose pour lequel vous souhaitez obtenir des sommets.  Chaque vertex de la mémoire tampon a une position et un normal.  Voici un exemple d’obtention de l’ensemble actuel de vertex pour une maille.  Comme précédemment, la variable *CurrentState* représente une instance de [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate).

```cpp
using namespace winrt::Windows::Perception::People;

auto handPose = currentState.TryGetHandPose();
if (handPose)
{
    std::vector<HandMeshVertex> vertices(handMeshObserver.VertexCount());
    auto vertexState = handMeshObserver.GetVertexStateForPose(handPose);
    vertexState.GetVertices(vertices);

    auto meshTransform = vertexState.CoordinateSystem().TryGetTransformTo(desiredCoordinateSystem);
    if (meshTransform != nullptr)
    {
        // Do something with the vertices and mesh transform, along with the indices that you saved earlier
    }
}
```

Contrairement aux jointures squelettes, l’API de maillage de la main ne vous permet pas de spécifier un système de coordonnées pour les vertex.  Au lieu de cela, le [HandMeshVertexState](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handmeshvertexstate) spécifie le système de coordonnées dans lequel les vertex sont fournis.  Vous pouvez ensuite obtenir une transformation de maillage en appelant [TryGetTransformTo](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem.trygettransformto#Windows_Perception_Spatial_SpatialCoordinateSystem_TryGetTransformTo_Windows_Perception_Spatial_SpatialCoordinateSystem_) et en spécifiant le système de coordonnées souhaité.  Vous devez utiliser cette transformation de maille chaque fois que vous travaillez avec les vertex.  Cette approche réduit la surcharge du processeur, en particulier si vous utilisez uniquement la maille à des fins de rendu.

## <a name="gaze-and-commit-composite-gestures"></a>Mouvements composites de point de regard et de validation
Pour les applications utilisant le modèle d’entrée de point de vue et de validation, en particulier sur HoloLens (First Gen), l’API d’entrée spatiale fournit un [SpatialGestureRecognizer](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.aspx) facultatif qui peut être utilisé pour activer les gestes composites reposant sur l’événement «Select».  En acheminant les interactions entre le SpatialInteractionManager et le SpatialGestureRecognizer d’un hologramme, les applications peuvent détecter les événements de TAP, de maintien, de manipulation et de navigation uniformément entre les mains, les voix et les périphériques d’entrée spatiales, sans avoir à gérer les presses et les libère manuellement.

SpatialGestureRecognizer effectue uniquement la désambiguïsation minimale entre l’ensemble de mouvements que vous demandez. Par exemple, si vous demandez simplement TAP, l’utilisateur peut conserver son doigt tant qu’il le souhaite et un TAP continue à se produire. Si vous demandez un tap-and-hold, une fois que vous avez appuyé sur un second de son doigt, le geste passe à un blocage et un TAP ne se produit plus.

Pour utiliser SpatialGestureRecognizer, gérez l’événement [InteractionDetected](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialInteractionManager.InteractionDetected) de SpatialInteractionManager et récupérez le SpatialPointerPose qui y est exposé. Utilisez la tête de regard de l’utilisateur à partir de cette pose pour faire une intersection avec les hologrammes et les maillages de surface dans l’environnement de l’utilisateur, afin de déterminer ce que l’utilisateur a l’intention d’interagir avec. Ensuite, acheminez le SpatialInteraction dans les arguments d’événement vers le SpatialGestureRecognizer de l’hologramme cible, à l’aide de sa méthode [CaptureInteraction](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.CaptureInteraction) . Cela commence à interpréter cette interaction en fonction du [SpatialGestureSettings](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureSettings) défini sur ce module de reconnaissance au moment de la création, ou par [TrySetGestureSettings](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.TrySetGestureSettings).

Sur HoloLens (First Gen), les interactions et les gestes doivent généralement dériver leur ciblage du point de vue de l’utilisateur, au lieu d’essayer d’effectuer un rendu ou une interaction directement à l’emplacement de la main. Une fois qu’une interaction a démarré, les mouvements relatifs de la main peuvent être utilisés pour contrôler le mouvement, comme avec la manipulation ou le mouvement de navigation.

## <a name="see-also"></a>Voir aussi
* [Suivre de la tête et du regard dans DirectX](gaze-in-directx.md)
* [Modèle d’entrée de manipulation directe](direct-manipulation.md)
* [Modèle d’entrée de point et de validation](point-and-commit.md)
* [Modèle d’entrée de regard et de validation](gaze-and-commit.md)
* [Contrôleurs de mouvement](motion-controllers.md)
