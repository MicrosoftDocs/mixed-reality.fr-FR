---
title: Mains et contrôleurs de mouvement dans DirectX
description: Guide du développeur pour l’utilisation du suivi de la main et les contrôleurs de mouvement dans les applications DirectX natives.
author: caseymeekhof
ms.author: cmeekhof
ms.date: 04/30/2019
ms.topic: article
keywords: mains, contrôleurs de mouvement, directx, entrée, hologrammes
ms.openlocfilehash: 08666c8c26cd4851c0c003a96a9e96d7a90228ac
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629642"
---
# <a name="hands-and-motion-controllers-in-directx"></a>Mains et contrôleurs de mouvement dans DirectX

En réalité mixte de Windows, les deux main et [contrôleur de mouvement](motion-controllers.md) l’entrée est gérée via l’API, une entrée spatiale trouvée dans le [Windows.UI.Input.Spatial](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial) espace de noms. Cela vous permet de gérer facilement des actions courantes telles que **sélectionnez** appuie sur la même façon entre les mains et contrôleurs de mouvement.

## <a name="getting-started"></a>Prise en main

Pour accéder à spatiale d’entrée en réalité mixte Windows, démarrez avec l’interface SpatialInteractionManager.  Vous pouvez accéder à cette interface en appelant [SpatialInteractionManager::GetForCurrentView](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.getforcurrentview), généralement occasionnellement lors du démarrage de l’application.

```cpp
using namespace winrt::Windows::UI::Input::Spatial;

SpatialInteractionManager interactionManager = SpatialInteractionManager::GetForCurrentView();
```

Les travaux de le SpatialInteractionManager consiste à fournir un accès aux [SpatialInteractionSources](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource), qui représentent une source d’entrée.  Il existe trois types de SpatialInteractionSources disponibles dans le système.
* **Main** représente main détectés d’un utilisateur. Sources de main offrent des fonctionnalités différentes en fonction de l’appareil, allant des gestes de base sur HoloLens main entièrement articulés suivi sur HoloLens 2. 
* **Contrôleur** représente un contrôleur de mouvement associé. Contrôleurs de mouvement peuvent offrir un éventail de fonctionnalités.  Exemple : Sélectionnez les déclencheurs, les boutons de Menu, des boutons de compréhension, pavés tactiles et sticks analogiques.
* **Voix** représente la voix de l’utilisateur à propos du système a détecté les mots clés. Par exemple, cette source est injecter l’appui sur une sélection et mise en production chaque fois que l’utilisateur dit « Select ».

Par image données pour une source est représentée par le [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) interface. Il existe deux façons différentes d’accéder à ces données, selon que vous souhaitez utiliser un modèle événementiel ou reposant sur l’interrogation dans votre application.

### <a name="event-driven-input"></a>Entrée pilotée par événements
Le SpatialInteractionManager fournit un nombre d’événements que votre application peut écouter.  Sont des exemples [SourcePressed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed), [SourceReleased](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcereleased) et [SourceUpdated](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourceupdated).

Par exemple, le code suivant connecte un gestionnaire d’événements appelé MyApp::OnSourcePressed à l’événement SourcePressed.  Cela permet à votre application détecter les appuis sur n’importe quel type de source de l’interaction.

```cpp
using namespace winrt::Windows::UI::Input::Spatial;

auto interactionManager = SpatialInteractionManager::GetForCurrentView();
interactionManager.SourcePressed({ this, &MyApp::OnSourcePressed });

```

Cet événement appuyé est envoyé à votre application de façon asynchrone, ainsi que la SpatialInteractionSourceState correspondant au moment où que la presse s’est produite. Votre application ou le moteur de jeu souhaitez peut-être effectuer un traitement immédiatement, ou vous souhaiterez peut-être les données d’événement dans votre routine de traitement des entrées de file d’attente. Voici une fonction de gestionnaire d’événements pour l’événement SourcePressed, qui montre comment vérifier si le bouton de sélection a été enfoncé.

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

Le code ci-dessus vérifie uniquement la presse 'Select', qui correspond à l’action principale sur l’appareil. Effectuer un AirTap sur HoloLens ou exemples tirant le déclencheur sur un contrôleur de mouvement.  Presses 'Select' représentent l’intention de l’utilisateur pour activer l’hologramme que cibler.  L’événement SourcePressed se déclenche pendant un nombre de boutons différents et des mouvements, et vous pouvez inspecter les autres propriétés sur le SpatialInteractionSource à tester pour ces cas.

### <a name="polling-based-input"></a>Entrée d’interrogation.
Vous pouvez également utiliser SpatialInteractionManager pour interroger l’état actuel de l’entrée chaque trame.  Pour ce faire, appelez simplement [GetDetectedSourcesAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.getdetectedsourcesattimestamp) chaque trame.  Cette fonction retourne un tableau contenant une [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) pour chaque actif [SpatialInteractionSource](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource). Cela signifie une pour chaque contrôleur de mouvement active, une pour chaque aiguille suivie et une pour la reconnaissance vocale si une commande 'select' a été récemment prononcée. Vous pouvez ensuite inspecter les propriétés sur chaque SpatialInteractionSourceState à entrée du lecteur dans votre application. 

Voici un exemple montrant comment vérifier l’action « select » à l’aide de la méthode d’interrogation. Notez que le *prédiction* variable représente un [HolographicFramePrediction](https://docs.microsoft.com/en-us/uwp/api/Windows.Graphics.Holographic.HolographicFramePrediction) objet, ce qui peut être obtenu à partir de la [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe).

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

Chaque SpatialInteractionSource a un ID, vous pouvez utiliser pour identifier les nouvelles sources et de mettre en corrélation les sources existantes à partir d’une image à l’autre.  Mains sont affectés à un nouvel ID chaque fois qu’ils laissez, puis entrez l’angle d’ouverture, mais les ID de contrôleur restent statiques pendant la durée de la session.  Vous pouvez utiliser les événements sur SpatialInteractionManager comme [SourceDetected](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcedetected) et [SourceLost](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcelost), pour réagir quand mains ou à destination de l’appareil de l’afficher, ou lorsque les contrôleurs de mouvement sont activés/désactivé ou sont couplé/apparié.

### <a name="predicted-vs-historical-poses"></a>Prédite et risque de poser historiques
Notez que GetDetectedSourcesAtTimestamp a un paramètre de timestamp. Cela vous permet de demander l’état et présentent des données qui sont soit prédite ou historiques et ainsi vous mettre en corrélation spatiales interactions avec d’autres sources d’entrée. Par exemple, lors du rendu de position de la main dans le frame actuel, vous pouvez passer dans l’horodatage prédite fournie par le [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe). Cela permet au système de prédire-avant la position de la main pour s’aligner sur la sortie de l’image rendue, en réduisant la latence perçue.

Toutefois, telle une pose prédite ne produit pas un rayon de pointage idéale pour le ciblage avec une source de l’interaction. Par exemple, lorsqu’un bouton de contrôleur de mouvement est enfoncé, il peut prendre jusqu'à 20 ms pour cet événement à se propager via Bluetooth au système d’exploitation. De même, une fois un utilisateur effectue un mouvement de la main, une certaine quantité de temps peut passer avant que le système détecte le mouvement et votre application, puis interroge pour lui. Au moment où votre application interroge pour un changement d’état, le risque de poser head et main utilisé pour cible interaction s’est passée dans le passé. Si vous ciblez en passant d’horodatage de votre HolographicFrame actuel à GetDetectedSourcesAtTimestamp, la pose sera à la place par progression prédit pour le ciblage rayon au moment où que le frame s’affichera, qui pourrait être plus de 20 ms à l’avenir. Cette pose futures est valable pour *rendu* la source de l’interaction, composés, mais notre problème de temps pour *ciblant* l’interaction, comme l’utilisateur du ciblage s’est produite dans le passé.

Heureusement, le [SourcePressed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed), [SourceReleased](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcereleased) et [SourceUpdated](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourceupdated) événements fournissent l’historique [état](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourceeventargs.state) associé chaque événement d’entrée.  Cela inclut directement pose de tête et main historiques disponibles via [TryGetPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose), ainsi que d’un historique [Timestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.timestamp) que vous pouvez passer aux autres API pour mettre en corrélation avec cet événement.

Ceci nous mène aux meilleures pratiques suivantes lors de rendu et de ciblage avec mains et les contrôleurs de chaque image :
* Pour **rendu de main/contrôleur** chaque trame, votre application doit **interrogation** pour le **prédit avant** poser de chaque source de l’interaction au moment de photon du frame actif.  Vous pouvez interroger pour toutes les sources d’interaction en appelant [GetDetectedSourcesAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.getdetectedsourcesattimestamp) chaque trame, en passant l’horodatage prédite fourni par [HolographicFrame::CurrentPrediction](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe.currentprediction).
* Pour **main/contrôleur ciblant** selon une press ou une mise en production, votre application doit gérer enfoncé/publié **événements**, raycasting selon le **historique** pose de tête ou de la main pour Cet événement. Vous obtenez ce ciblage ray en gérant la [SourcePressed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed) ou [SourceReleased](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcereleased) événement, bien le [état](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourceeventargs.state) propriété à partir des arguments d’événement avant d’appeler ses [ TryGetPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose) (méthode).

## <a name="cross-device-input-properties"></a>Propriétés d’entrée entre les périphériques
L’API SpatialInteractionSource prend en charge les contrôleurs et les systèmes avec un large éventail de fonctionnalités de suivi de main. Un certain nombre de ces fonctionnalités est commun aux types d’appareils. Par exemple, main suivi mouvement contrôleurs et les deux fournissent une action « sélectionner » et une position 3D. Dans la mesure du possible, l’API mappe ces fonctionnalités courantes pour les mêmes propriétés sur le SpatialInteractionSource.  Cela permet aux applications plus facilement prendre en charge un large éventail de types d’entrée. Le tableau suivant décrit les propriétés qui sont prises en charge, et les comparer entre les types d’entrée.

| Propriété | Description | Mouvements de HoloLens | Contrôleurs de mouvement | Mains articulés|
|--- |--- |--- |--- |--- |
| [SpatialInteractionSource ::**gaucher/droitier**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource.handedness) | Droite ou gauche / contrôleur. | Non prise en charge | Prise en charge | Prise en charge |
| [SpatialInteractionSourceState::**IsSelectPressed**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.isselectpressed) | État actuel du bouton principal. | Appui | déclencheur | Souple Air appuyez sur (pincement vertical) |
| [SpatialInteractionSourceState::**IsGrasped**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.isgrasped) | État actuel du bouton de manipulation. | Non prise en charge | Bouton de manipulation | Main pincement ou fermé |
| [SpatialInteractionSourceState::**IsMenuPressed**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.ismenupressed) | État actuel du bouton de menu.    | Non prise en charge | Bouton de menu | Non prise en charge |
| [SpatialInteractionSourceLocation ::**Position**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcelocation.position) | Emplacement XYZ de la position main ou la poignée sur le contrôleur. | Emplacement de Palm | Poignée pose position | Emplacement de Palm |
| [SpatialInteractionSourceLocation ::**Orientation**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcelocation.orientation) | Quaternion qui représente l’orientation de la main ou la poignée de poser sur le contrôleur. | Non prise en charge | Poignée pose orientation | Orientation de Palm |
| [SpatialPointerInteractionSourcePose ::**Position**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerinteractionsourcepose.position#Windows_UI_Input_Spatial_SpatialPointerInteractionSourcePose_Position) | Origine du rayon de pointage. | Non prise en charge | Prise en charge | Prise en charge |
| [SpatialPointerInteractionSourcePose::**ForwardDirection**](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerinteractionsourcepose.forwarddirection#Windows_UI_Input_Spatial_SpatialPointerInteractionSourcePose_ForwardDirection) | Direction du rayon pointage. | Non prise en charge | Prise en charge | Prise en charge |

Certaines des propriétés ci-dessus ne sont pas disponibles sur tous les appareils, et l’API fournit un moyen de tester cela. Par exemple, vous pouvez inspecter les [SpatialInteractionSource::IsGraspSupported](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource.isgraspsupported) propriété pour déterminer si la source fournit une action de compréhension.

### <a name="grip-pose-vs-pointing-pose"></a>Pose de poignée et pose de pointage

Réalité mixte Windows prend en charge les contrôleurs de mouvements dans un large éventail de facteurs de forme.  Il prend également en charge les bras main des systèmes de suivi.  Tous ces systèmes ont différentes relations entre la position de la main et le sens de « avant » naturels que les applications doivent utiliser pour les objets pointant ou rendreing à portée de main de l’utilisateur.  Pour prendre en charge tout ceci, il existe deux types de risque de poser 3D fourni pour les deux contrôleurs de suivi et des mouvements de main.  La première est pose de poignée, qui représente la position de main de l’utilisateur.  La deuxième pointe pose, qui représente un rayon de pointage provenant de la main ou contrôleur de l’utilisateur. Par conséquent, si vous souhaitez restituer **main de l’utilisateur** ou **détenues par un objet à portée de main de l’utilisateur**, tel qu’un mot de passe ou d’un électrons, utilisez la pose de poignée. Si vous souhaitez raycast à partir du contrôleur ou d’une part, par exemple lorsque l’utilisateur est **vers l’interface utilisateur** , utilisez la pose de pointage.

Vous pouvez accéder à la **poignée pose** via [SpatialInteractionSourceState::Properties::TryGetLocation(...) ](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourceproperties.trygetlocation#Windows_UI_Input_Spatial_SpatialInteractionSourceProperties_TryGetLocation_Windows_Perception_Spatial_SpatialCoordinateSystem_).  Il est défini comme suit :
* Le **Attrapez position**: Le centroïde de palm naturellement, tout en maintenant le contrôleur ajustée gauche ou droite pour centrer la position au sein de la poignée.
* Le **Attrapez axe de droite de l’orientation**: Lorsque vous ouvrez totalement la main pour former une pose plat 5-doigt, le rayon qui est normal pour votre palm (en avant à partir de la gauche palm, vers l’arrière de palm droite)
* Le **Attrapez axe vers l’avant de l’orientation**: Lorsque vous fermez votre main partiellement (comme le cas maintenant le contrôleur), le rayon pointe « forward » via le tube formé par vos doigts non curseur.
* Le **Attrapez orientation d’axe**: L’axe à distance impliqué par les définitions de droite, en avant.

Vous pouvez accéder à la **pose de pointeur** via [SpatialInteractionSourceState::Properties::TryGetLocation (...) :: SourcePointerPose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsourcelocation#Windows_UI_Input_Spatial_SpatialInteractionSourceLocation_SourcePointerPose) ou [SpatialInteractionSourceState :: TryGetPointerPose (...) :: TryGetInteractionSourcePose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerpose#Windows_UI_Input_Spatial_SpatialPointerPose_TryGetInteractionSourcePose_Windows_UI_Input_Spatial_SpatialInteractionSource_).

## <a name="controller-specific-input-properties"></a>Propriétés d’entrée spécifique du contrôleur
Pour les contrôleurs, le SpatialInteractionSource a une propriété de contrôleur avec des fonctionnalités supplémentaires.
* **HasThumbstick :** Si la valeur est true, le contrôleur a un stick analogique. Inspecter le [ControllerProperties](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractioncontrollerproperties) propriété de la SpatialInteractionSourceState pour acquérir le stick analogique x et les valeurs y (ThumbstickX et ThumbstickY), ainsi que son état enfoncé (IsThumbstickPressed).
* **HasTouchpad :** Si la valeur est true, le contrôleur a un pavé tactile. Inspecter la propriété ControllerProperties de la SpatialInteractionSourceState pour acquérir le pavé tactile x et y valeurs (TouchpadX et TouchpadY) et pour savoir si l’utilisateur touche le panneau (IsTouchpadTouched) et si elles sont en appuyant sur le pavé tactile vers le bas () IsTouchpadPressed).
* **SimpleHapticsController :** L’API SimpleHapticsController pour le contrôleur vous permet d’inspecter les fonctionnalités HAPTIQUES du contrôleur de, et il vous permet également de contrôler le retour haptique.

Notez que la plage pour le pavé tactile et stick analogique est -1 et 1 pour les deux axes (de bas en haut et de gauche à droite). La plage pour le déclencheur analogique, qui est accessible à l’aide de la propriété SpatialInteractionSourceState::SelectPressedValue, a une plage de 0 à 1. Une valeur de 1 met en corrélation avec IsSelectPressed étant égal à true ; toute autre valeur met en corrélation avec IsSelectPressed étant égal à false.

## <a name="articulated-hand-tracking"></a>Main bras de suivi
L’API de réalité mixte Windows prend en charge pour la main articulé de suivi, par exemple sur HoloLens 2. Main bras de suivi peut servir à implémenter la manipulation directe et des modèles d’entrée de point et de validation dans vos applications. Il peut également servir à créer des interactions entièrement personnalisées.

### <a name="hand-skeleton"></a>Structure de main
Main articulé de suivi fournit une structure commune 25 qui permet de nombreux types d’interactions.  La structure fournit 5 joints pour les doigts index/intermédiaire/en anneau/peu, 4 joints pour le curseur et 1 poignet mixte.  La jointure de poignet sert de la base de la hiérarchie. L’image suivante illustre la disposition de la structure.

![Structure de main](images/hand-skeleton.png)

Dans la plupart des cas, chaque commune est nommé en fonction de l’OS qu’il représente.  Dans la mesure où il n’y a deux segments à chaque commune, nous utilisons une convention de nommage chaque joint en fonction de l’OS enfant à cet emplacement.  Le segment de l’enfant est défini comme l’OS plus éloigné du poignet.  Par exemple, le « Index PROXIMALE « mixte contient la position de début de l’OS PROXIMALE index et l’orientation de ce segment.  Il ne contient pas la position de fin du segment.  Si vous avez besoin que, vous obtiendriez il à partir de la prochaine mixte dans la hiérarchie, le « Index intermédiaires » commun.

En plus de 25 articulations hiérarchiques, le système fournit un joint palm.  Le palm n’est pas généralement considéré partie de la structure du squelette.  Il est fourni uniquement comme un moyen pratique pour obtenir la position et l’orientation globale de la main.

Les informations suivantes sont fournies pour chaque jointure :

| Nom | Description |
|--- |--- |
|Position | Position 3D de la jointure, disponible dans n’importe quel système de coordonnées demandée. |
|Orientation | Orientation 3D de l’OS, disponible dans aucun demandé de système de coordonnées. |
|Rayon | Distance à la surface de l’apparence à la position commune. Utile pour le réglage des interactions directes ou des visualisations qui s’appuient sur la largeur du doigt. |
|Précision | Fournit une indication sur la certitude comment le système semble sur les informations de cette jointure. |

Vous pouvez accéder à des données squelette disponible via une fonction sur le [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate).  La fonction est appelée [TryGetHandPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygethandpose#Windows_UI_Input_Spatial_SpatialInteractionSourceState_TryGetHandPose), et elle retourne un objet appelé [HandPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handpose).  Si la source ne prend pas en charge les mains articulés, cette fonction retourne null.  Une fois que vous avez un HandPose, vous pouvez obtenir des données mixte actuelles en appelant [TryGetJoint](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handpose.trygetjoint#Windows_Perception_People_HandPose_TryGetJoint_Windows_Perception_Spatial_SpatialCoordinateSystem_Windows_Perception_People_HandJointKind_Windows_Perception_People_JointPose__), avec le nom de la jointure, vous êtes intéressé.  Les données sont retournées en tant qu’un [JointPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.jointpose) structure.  Le code suivant obtient la position de l’info-bulle de votre index. La variable *currentState* représente une instance de [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate).

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

### <a name="hand-mesh"></a>Maillage de main

L’aiguille articulé de l’API de suivi permet une maille de main entièrement déformable triangle.  Ce maillage peut déformer en temps réel, ainsi que la structure de la main et est utile pour la visualisation, ainsi que des techniques de physique avancé.  Pour accéder à la maille de main, vous devez d’abord créer un [HandMeshObserver](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handmeshobserver) objet en appelant [TryCreateHandMeshObserverAsync](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource.trycreatehandmeshobserverasync) sur le [SpatialInteractionSource](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsource).  Cette opération ne doit être effectuée qu’une fois par source, généralement la première fois que vous le voyez.  Cela signifie que vous devez appeler cette fonction pour créer un objet HandMeshObserver chaque fois qu’une main passe à l’angle d’ouverture.  Notez qu’il s’agit d’une fonction async, vous devez donc gérer avec un peu de concurrence ici.  Une fois disponible, vous pouvez demander à l’objet HandMeshObserver de la mémoire tampon d’index triangle, en appelant [GetTriangleIndices](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handmeshobserver.gettriangleindices#Windows_Perception_People_HandMeshObserver_GetTriangleIndices_System_UInt16___).  Indices ne modifiez pas frame par frame, afin de pouvoir les obtenir qu’une seule fois et les mettre en cache pour la durée de vie de la source.  Indices sont fournies dans l’ordre d’enroulement dans le sens horaire.

Le code suivant tourne un std::thread détaché pour créer l’Observateur de maillage et extrait la mémoire tampon d’index une fois que l’Observateur de maille est disponible.  Il démarre à partir d’une variable appelée *currentState*, qui est une instance de [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) représentant une main suivie.

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
À partir d’un thread détaché est qu’une seule option pour la gestion des appels asynchrones.  Vous pouvez également utiliser la nouvelle [co_await](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) fonctionnalités prises en charge par C++/WinRT.

Une fois que vous avez un objet HandMeshObserver, vous ne devriez conserver il pendant la durée de son SpatialInteractionSource correspondant est actif.  Puis chaque cadre, vous pouvez le demander de la dernière mémoire tampon vertex qui représente la main en appelant [GetVertexStateForPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handmeshobserver.getvertexstateforpose) et en passant un [HandPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handpose) instance qui représente la pose que vous souhaitez les sommets pour.  Chaque vertex dans la mémoire tampon a une position et un élément normal.  Voici un exemple illustrant comment obtenir l’ensemble actuel des sommets d’un maillage de main.  Comme auparavant, le *currentState* variable représente une instance de [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate).

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

Contrairement à squelettes joints, l’API de maille main n’autorise pas vous permettent de spécifier un système de coordonnées pour les vertex.  Au lieu de cela, le [HandMeshVertexState](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.handmeshvertexstate) Spécifie le système de coordonnées qui les sommets sont fournies dans.  Vous pouvez ensuite obtenir une transformation de maille en appelant [TryGetTransformTo](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem.trygettransformto#Windows_Perception_Spatial_SpatialCoordinateSystem_TryGetTransformTo_Windows_Perception_Spatial_SpatialCoordinateSystem_) et en spécifiant votre système de coordonnées de votre choix.  Vous devez utiliser cette transformation maillage chaque fois que vous travaillez avec les sommets.  Cette approche réduit la surcharge du processeur, en particulier si vous utilisez uniquement la maille à des fins de rendu.

## <a name="gaze-and-commit-composite-gestures"></a>Utilisation et validez les mouvements composites
Pour les applications utilisant le modèle d’entrée du pointage de regard-validation, en particulier sur HoloLens (première génération), l’API d’entrée Spatial fournit facultative [SpatialGestureRecognizer](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.aspx) qui peut être utilisé à pour activer les mouvements composites, construits sur le 'select' événement.  En routage d’interactions à partir de la SpatialInteractionManager à SpatialGestureRecognizer d’un hologramme, applications peuvent détecter les événements Tap, blocage, la Manipulation et Navigation uniformément entre les mains, voix et périphériques d’entrée spatiales, sans avoir à gérer les activations et libère manuellement.

SpatialGestureRecognizer effectue uniquement la levée d’ambiguïté minimale entre l’ensemble des gestes que vous demandez. Par exemple, si vous demandez simplement Tap, l’utilisateur peut maintenez son doigt en tant qu’ils le souhaitent et un drainage se produira toujours. Si vous demandez à la fois maintenez sur, après environ une seconde d’enfoncée son doigt, promeut le mouvement à une suspension et un drainage ne se produit plus.

Pour utiliser SpatialGestureRecognizer, gérer la SpatialInteractionManager [InteractionDetected](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialInteractionManager.InteractionDetected) événements et capture le SpatialPointerPose exposée il. Utilisez ray regards principal de l’utilisateur à partir de cette pose à croiser avec l’hologrammes et surface mailles dans son environnement de l’utilisateur, afin de déterminer ce que l’utilisateur a l’intention d’interagir avec. Ensuite, acheminer la SpatialInteraction dans les arguments d’événement pour SpatialGestureRecognizer de hologramme de cible, à l’aide de son [CaptureInteraction](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.CaptureInteraction) (méthode). Cela démarre l’interprétation de cette interaction conformément à la [SpatialGestureSettings](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureSettings) définies sur ce module de reconnaissance à l’heure de création - ou en [TrySetGestureSettings](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.TrySetGestureSettings).

Sur HoloLens (tout d’abord de la génération), interactions et des mouvements doivent dériver généralement leur ciblage à partir des regards principal de l’utilisateur, au lieu d’essayer restituer ou interagir directement à l’emplacement de la main. Une fois démarrée, une interaction des mouvements relatifs de la main peuvent servir à contrôler le mouvement, comme avec le mouvement de Manipulation ou de Navigation.

## <a name="see-also"></a>Voir aussi
* [HEAD et surveillez les regards dans DirectX](gaze-in-directx.md)
* [Modèle d’entrée de manipulation directe](direct-manipulation.md)
* [Modèle d’entrée de point et validation](point-and-commit.md)
* [Modèle d’entrée du pointage de regard et validation](gaze-and-commit.md)
* [Contrôleurs de mouvement](motion-controllers.md)
