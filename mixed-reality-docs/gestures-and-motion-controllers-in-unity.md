---
title: Mouvements et contrôleurs de mouvement dans Unity
description: Il existe deux façons principales d’agir sur votre point d’intergression, les gestes manuels et les contrôleurs de mouvement.
author: thetuvix
ms.author: yoyoz
ms.date: 03/21/2018
ms.topic: article
keywords: mouvements, contrôleurs de mouvement, Unity, point de regard, entrée
ms.openlocfilehash: f0d2835a08ef534af1310db35ccb81888e49aeb8
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63525757"
---
# <a name="gestures-and-motion-controllers-in-unity"></a>Mouvements et contrôleurs de mouvement dans Unity

Il existe deux façons principales d’agir sur votre point [de regard](gaze-in-unity.md), les [gestes manuels](gestures.md) et les [contrôleurs de mouvement](motion-controllers.md) dans HoloLens et les HMD immersifs. Vous accédez aux données des deux sources d’entrée spatiale via les mêmes API dans Unity.

Unity fournit deux méthodes principales pour accéder aux données d’entrée spatiale pour Windows Mixed Reality, les API common *Input. GetButton/Input. GetAxis* qui fonctionnent sur plusieurs SDK XR Unity et une API *InteractionManager/GestureRecognizer* spécifique à Windows Mixed Reality qui expose l’ensemble complet des données d’entrée spatiale disponibles.

## <a name="unity-buttonaxis-mapping-table"></a>Bouton Unity/table de mappage des axes

Les ID de bouton et d’axe dans le tableau ci-dessous sont pris en charge dans le gestionnaire d’entrée d’Unity Manager pour les contrôleurs de mouvement Windows Mixed Reality via les API *Input. GetButton/GetAxis* , tandis que la colonne «propre à Windows Mr» fait référence aux propriétés disponibles sur le Type de *InteractionSourceState* . Chacune de ces API est décrite en détail dans les sections ci-dessous.

Les mappages de bouton/ID d’axe pour Windows Mixed Reality correspondent généralement aux ID d’axe/bouton Oculus.

Les mappages de bouton/ID d’axe pour Windows Mixed Reality diffèrent des mappages de OpenVR de deux façons:
1. Le mappage utilise des ID de pavé tactile distincts du stick analogique, pour prendre en charge des contrôleurs avec Thumbsticks et des pavés tactiles.
2. Le mappage évite de surcharger les ID de bouton A et X pour les boutons de menu, afin de conserver ceux disponibles pour les boutons ABXY physiques.

<table>
<tr>
<th rowspan="2">Entrée </th><th colspan="2"><a href="gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis">API Unity courantes</a><br />(Input. GetButton/GetAxis) </th><th rowspan="2"><a href="gestures-and-motion-controllers-in-unity.md#">API d’entrée spécifique à Windows MR</a><br />XR. WSA. Entrée</th>
</tr><tr>
<th> Main gauche </th><th> À droite</th>
</tr><tr>
<td> Sélectionner le déclencheur enfoncé </td><td> Axe 9 = 1,0 </td><td> Axe 10 = 1,0 </td><td> selectPressed</td>
</tr><tr>
<td> Sélectionner la valeur analogique du déclencheur </td><td> Axe 9 </td><td> Axe 10 </td><td> selectPressedAmount</td>
</tr><tr>
<td> Sélectionner le déclencheur partiellement enfoncé </td><td> Bouton 14 <i>(compatibilité du boîtier de</i> l’option) </td><td> Bouton 15 <i>(compatibilité du boîtier de</i> l’option) </td><td> selectPressedAmount &gt; 0,0</td>
</tr><tr>
<td> Bouton de menu enfoncé </td><td> Bouton 6 * </td><td> Bouton 7 * </td><td> menuPressed</td>
</tr><tr>
<td> Bouton de préhension enfoncé </td><td> Axe 11 = 1,0 (aucune valeur analogique)<br />Bouton 4 <i>(compatibilité du boîtier de</i> l’option) </td><td> Axe 12 = 1,0 (aucune valeur analogique)<br />Bouton 5 <i>(compatibilité du boîtier de</i> l’option) </td><td> saisi</td>
</tr><tr>
<td> Stick analogique <i>X (gauche:-1,0, droite: 1,0)</i> </td><td> Axe 1 </td><td> Axe 4 </td><td> thumbstickPosition. x</td>
</tr><tr>
<td> Joystick Y <i>(haut:-1,0, bas: 1,0)</i> </td><td> Axe 2 </td><td> Axe 5 </td><td> thumbstickPosition. y</td>
</tr><tr>
<td> Stick analogique appuyé </td><td> Bouton 8 </td><td> Bouton 9 </td><td> thumbstickPressed</td>
</tr><tr>
<td> Pavé tactile <i>X (à gauche:-1,0, droite: 1,0)</i> </td><td> Axe 17 * </td><td> Axe 19 * </td><td> touchpadPosition. x</td>
</tr><tr>
<td> Pavé tactile <i>Y (haut:-1,0, bas: 1,0)</i> </td><td> Axe 18 * </td><td> Axe 20 * </td><td> touchpadPosition. y</td>
</tr><tr>
<td> Pavé tactile touché </td><td> Bouton 18 * </td><td> Bouton 19 * </td><td> touchpadTouched</td>
</tr><tr>
<td> Pavé tactile enfoncé </td><td> Bouton 16 * </td><td> Bouton 17 * </td><td> touchpadPressed</td>
</tr><tr>
<td> pose de la poignée ou du pointeur 6DoF </td><td colspan="2"> <i>Poignée</i> de pose uniquement: <a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html">XR. InputTracking.GetLocalPosition</a><br /><a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalRotation.html">XR. InputTracking.GetLocalRotation</a></td><td> <i>Poignée</i> ou <i>pointeur</i> en tant qu’argument: SourceState. sourcePose. TryGetPosition<br />sourceState.sourcePose.TryGetRotation<br /></td>
</tr><tr>
<td> État du suivi </td><td colspan="2"> <i>Précision de la position et risque de perte de source uniquement disponible via une API spécifique à MR</i> </td><td> <a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourcePose-positionAccuracy.html">sourceState.sourcePose.positionAccuracy</a><br /><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourceProperties-sourceLossRisk.html">sourceState. Properties. sourceLossRisk</a></td>
</tr>
</table>

>[!NOTE]
>Ces ID de bouton/axe diffèrent des ID utilisés par Unity pour les OpenVR en raison de collisions dans les mappages utilisés par les boîtiers de soucodeurs, Oculus touch et OpenVR.

## <a name="grip-pose-vs-pointing-pose"></a>Poignée de pose et pose de pointage

Windows Mixed Reality prend en charge les contrôleurs de mouvement dans un large éventail de facteurs de forme, la conception de chaque contrôleur étant différente dans sa relation entre la position de l’utilisateur et la direction «avant» naturelle que les applications doivent utiliser pour pointer lors du rendu de la SideWinder.

Pour mieux représenter ces contrôleurs, il existe deux genres de poses que vous pouvez examiner pour chaque source d’interaction, le pose de la **poignée** et le **pointeur se posent**. Les coordonnées de pose de la poignée et du pointeur sont exprimées par toutes les API Unity dans les coordonnées universelles Unity universel.

### <a name="grip-pose"></a>Poignée de pose

La **poignée** représente l’emplacement de la paume d’une main détectée par un HoloLens ou la poche qui détient un contrôleur de mouvement.

Sur les casques immersifs, le pose de la poignée est utilisé pour restituer **la main de l’utilisateur** ou **un objet détenu par l’utilisateur**, tel qu’un épée ou un pistolet. La poignée est également utilisée lors de la visualisation d’un contrôleur de mouvement, car le **modèle de rendu** fourni par Windows pour un contrôleur de mouvement utilise la poignée comme son origine et le centre de rotation.

La poignée est définie spécifiquement comme suit:
* Position de la **poignée**: Le centre de la poche quand il maintient le contrôleur naturellement, ajusté à gauche ou à droite pour centrer la position au sein de la poignée. Sur le contrôleur de mouvement Windows Mixed Reality, cette position s’aligne généralement avec le bouton de saisie.
* **Axe droit de l’orientation de la poignée**: Lorsque vous ouvrez complètement votre main pour former une pose plate à 5 doigts, le rayon normal à votre Palm (à partir de la poche de gauche, en arrière depuis la paume de droite)
* **Axe vers l’avant de l’orientation de la poignée**: Lorsque vous fermez partiellement votre main (comme si vous détenir le contrôleur), le rayon qui pointe vers l’avant dans le tube formé par vos doigts non thumbs.
* **Axe vers le haut de l’orientation de la poignée**: Axe vers le haut impliqué par les définitions Right et Forward.

Vous pouvez accéder à la poignée à l’aide de l’API d’entrée entre fournisseurs de l’unité Unity ( *[XR. InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html). GetLocalPosition/rotation*) ou via l’API propre à Windows Mr (*SourceState. SourcePose. TryGetPosition/rotation*, en demandant des données de pose pour le nœud de **poignée** ).

### <a name="pointer-pose"></a>Pose du pointeur

Le **pointeur de pose** représente l’extrémité du contrôleur pointant vers l’avant.

Le pointeur fourni par le système est le mieux utilisé pour raycast lorsque vous effectuez **le rendu du modèle de contrôleur lui-même**. Si vous effectuez le rendu d’un autre objet virtuel à la place du contrôleur, tel qu’un pistolet virtuel, vous devez pointer vers un rayon qui est le plus naturel pour cet objet virtuel, tel qu’un rayon qui traverse le canon du modèle de pistolet défini par l’application. Étant donné que les utilisateurs peuvent voir l’objet virtuel et non le contrôleur physique, le fait de pointer avec l’objet virtuel sera probablement plus naturel pour ceux qui utilisent votre application.

Actuellement, le pointeur de pose est disponible dans Unity uniquement par le biais de l’API propre à Windows MR, *sourceState. sourcePose. TryGetPosition/rotation*, en passant *InteractionSourceNode. pointeur* comme argument.

## <a name="controller-tracking-state"></a>État du suivi du contrôleur

À l’instar des casques, le contrôleur de mouvement Windows Mixed Reality ne nécessite pas de configuration de capteurs de suivi externe. Au lieu de cela, les contrôleurs sont suivis par des capteurs dans le casque lui-même.

Si l’utilisateur déplace les contrôleurs du champ de vue du casque, dans la plupart des cas, Windows continue à déduire les positions des contrôleurs et à les fournir à l’application. Lorsque le contrôleur a perdu le suivi visuel suffisamment longtemps, les positions du contrôleur sont découpées à des positions de précision approximatives.

À ce stade, le système va verrouiller le contrôleur à l’utilisateur, en effectuant le suivi de la position de l’utilisateur lors de son déplacement, tout en exposant l’orientation réelle du contrôleur à l’aide de ses capteurs d’orientation internes. De nombreuses applications qui utilisent des contrôleurs pour pointer et activer des éléments d’interface utilisateur peuvent fonctionner normalement avec une précision approximative sans que l’utilisateur ne remarque.

La meilleure façon de vous en faire une idée est de l’essayer vous-même. Consultez cette vidéo avec des exemples de contenu immersif qui fonctionne avec les contrôleurs de mouvement dans différents États de suivi:

<br>

 >[!VIDEO https://www.youtube.com/embed/QK_fOFDHj0g]

### <a name="reasoning-about-tracking-state-explicitly"></a>Raisonnement sur le suivi de l’État explicitement

Les applications qui souhaitent traiter différemment les positions en fonction de l’état de suivi peuvent aller plus loin et inspecter les propriétés de l’état du contrôleur, telles que *SourceLossRisk* et *PositionAccuracy*:

<table>
<tr>
<th> État du suivi </th><th> SourceLossRisk </th><th> PositionAccuracy </th><th> TryGetPosition</th>
</tr><tr>
<td> <b>Haute précision</b> </td><td style="background-color: green; color: white"> &lt;1,0 </td><td style="background-color: green; color: white"> Élevé </td><td style="background-color: green; color: white"> true</td>
</tr><tr>
<td> <b>Haute précision (risque de perte)</b> </td><td style="background-color: orange"> = = 1,0 </td><td style="background-color: green; color: white"> Élevé </td><td style="background-color: green; color: white"> true</td>
</tr><tr>
<td> <b>Précision approximative</b> </td><td style="background-color: orange"> = = 1,0 </td><td style="background-color: orange"> Approximate </td><td style="background-color: green; color: white"> true</td>
</tr><tr>
<td> <b>Aucune position</b> </td><td style="background-color: orange"> = = 1,0 </td><td style="background-color: orange"> Approximate </td><td style="background-color: orange"> false</td>
</tr>
</table>

Ces États de suivi du contrôleur de mouvement sont définis comme suit:
* **Précision élevée:** Alors que le contrôleur de mouvement se trouve dans le champ de vision du casque, il fournit généralement des positions à grande précision, en fonction du suivi visuel. Notez qu’un contrôleur mobile qui laisse momentanément le champ de vue ou est momentanément masqué à partir des capteurs du casque (par exemple, par l’autre côté de l’utilisateur) continue à retourner des poses de grande précision pendant une brève période, en fonction du suivi inertiel du contrôleur. automatiquement.
* **Haute précision (risque de perte):** Lorsque l’utilisateur déplace le contrôleur de mouvement au-delà du bord du champ de vue du casque, le casque ne pourra bientôt pas suivre la position du contrôleur. L’application sait quand le contrôleur a atteint cette limite d’aide en regardant le **SourceLossRisk** REACH 1,0. À ce stade, l’application peut choisir de suspendre les gestes de contrôleur qui nécessitent un flux constant de poses très haute qualité.
* **Précision approximative:** Lorsque le contrôleur a perdu le suivi visuel suffisamment longtemps, les positions du contrôleur sont découpées à des positions de précision approximatives. À ce stade, le système va verrouiller le contrôleur à l’utilisateur, en effectuant le suivi de la position de l’utilisateur lors de son déplacement, tout en exposant l’orientation réelle du contrôleur à l’aide de ses capteurs d’orientation internes. De nombreuses applications qui utilisent des contrôleurs pour pointer et activer des éléments d’interface utilisateur peuvent fonctionner normalement, tout en ayant une précision approximative, sans que l’utilisateur ne remarque. Les applications avec des exigences d’entrée plus lourdes peuvent choisir de déterminer ce déplacement de la **haute** précision à une précision **approximative** en inspectant la propriété **PositionAccuracy** , par exemple pour fournir à l’utilisateur un hitbox plus généreux sur les cibles hors écran pendant ce temps.
* **Aucune position:** Alors que le contrôleur peut fonctionner à des fins de précision approximative pendant une longue période, le système sait parfois que même une position verrouillée par le corps n’est pas significative pour le moment. Par exemple, un contrôleur qui vient d’être activé n’a peut-être jamais été observé visuellement, ou un utilisateur peut mettre un contrôleur qui est ensuite récupéré par une autre personne. À ce moment-là, le système ne fournit aucune position à l’application, et *TryGetPosition* retourne la valeur false.

## <a name="common-unity-apis-inputgetbuttongetaxis"></a>API Unity courantes (Input. GetButton/GetAxis)

**Espace de noms :** *UnityEngine*, *UnityEngine. XR*<br>
**Types**: *Entrée*, *XR. InputTracking*

Unity utilise actuellement ses API *d’entrée. GetButton/Input. GetAxis* pour exposer l’entrée pour [le kit de développement logiciel (SDK) Oculus](https://docs.unity3d.com/Manual/OculusControllers.html), [le kit de développement logiciel (SDK) OpenVR et la](https://docs.unity3d.com/Manual/OpenVRControllers.html) réalité mixte Windows, y compris les contrôleurs mains et motion. Si votre application utilise ces API pour l’entrée, elle peut facilement prendre en charge des contrôleurs de mouvement sur plusieurs kits de développement logiciel (SDK) XR, y compris Windows Mixed Reality.

### <a name="getting-a-logical-buttons-pressed-state"></a>Obtention de l’état enfoncé d’un bouton logique

Pour utiliser les API d’entrée Unity générales, vous commencez généralement par associer des boutons et des axes aux noms logiques dans le [Gestionnaire d’entrée Unity](https://docs.unity3d.com/Manual/ConventionalGameInput.html), en liant un bouton ou des ID d’axe à chaque nom. Vous pouvez ensuite écrire du code qui fait référence à ce nom d’axe/bouton logique.

Par exemple, pour mapper le bouton de déclenchement du contrôleur de mouvement gauche à l’action envoyer, accédez à **modifier > paramètres du projet > entrée** dans Unity, puis développez les propriétés de la section envoyer sous axes. Modifiez le **bouton** ou la propriété du **bouton Alt positif** pour lire le bouton de la manette de jeu **14**, comme suit:

![InputManager d’Unity](images/unity-input-manager.png)<br>
*InputManager Unity*

Votre script peut ensuite Rechercher l’action envoyer à l’aide de *Input. GetButton*:

```cs
if (Input.GetButton("Submit"))
{
  // ...
}
```
Vous pouvez ajouter des boutons logiques en modifiant la propriété **taille** sous **axes**.

### <a name="getting-a-physical-buttons-pressed-state-directly"></a>Obtention directe d’un état enfoncé d’un bouton physique

Vous pouvez également accéder manuellement aux boutons à l’aide de leur nom complet, en utilisant *Input. GetKey*:

```cs
if (Input.GetKey("joystick button 8"))
{
  // ...
}
```

### <a name="getting-a-hand-or-motion-controllers-pose"></a>Obtention d’une main ou d’une pose de contrôleur de mouvement

Vous pouvez accéder à la position et à la rotation du contrôleur, à l’aide de *XR. InputTracking*:

```cs
Vector3 leftPosition = InputTracking.GetLocalPosition(XRNode.LeftHand);
Quaternion leftRotation = InputTracking.GetLocalRotation(XRNode.LeftHand);
```

Notez que cela représente la poignée de préhension du contrôleur (où l’utilisateur détient le contrôleur), qui est utile pour le rendu d’une arme ou d’un pistolet dans la main de l’utilisateur, ou un modèle du contrôleur lui-même.

Notez que la relation entre cette poignée pose et que le pointeur pose (où l’extrémité du contrôleur pointe) peut différer d’un contrôle à l’autre. À ce stade, l’accès au pointeur du contrôleur est possible uniquement via l’API d’entrée spécifique à MR, décrite dans les sections ci-dessous.

## <a name="windows-specific-apis-xrwsainput"></a>API spécifiques à Windows (XR. WSA. Entrée

**Espace de noms :** *UnityEngine. XR. WSA. Input*<br>
**Types**: *InteractionManager*, *InteractionSourceState*, *InteractionSource*, *InteractionSourceProperties*, *InteractionSourceKind*, *InteractionSourceLocation*

Pour obtenir des informations plus détaillées sur l’entrée manuelle de Windows Mixed Reality (pour HoloLens) et les contrôleurs de mouvement, vous pouvez choisir d’utiliser les API d’entrée spatiale spécifiques à Windows sous l’espace de noms *UnityEngine. XR. WSA. Input* . Cela vous permet d’accéder à des informations supplémentaires, telles que la précision de la position ou le genre de source, vous permettant de distinguer les mains et les contrôleurs.

### <a name="polling-for-the-state-of-hands-and-motion-controllers"></a>Interrogation de l’état des contrôleurs mains et motion

Vous pouvez interroger l’état de ce frame pour chaque source d’interaction (contrôleur de main ou de mouvement) à l’aide de la méthode *GetCurrentReading* .

```cs
var interactionSourceStates = InteractionManager.GetCurrentReading();
foreach (var interactionSourceState in interactionSourceStates) {
    // ...
}
```

Chaque *InteractionSourceState* que vous récupérez représente une source d’interaction à l’instant courant. *InteractionSourceState* expose des informations telles que:
* Quels sont les [types d’enfoncement](motion-controllers.md) (Select/menu///-pavé/Stick)

   ```cs
   if (interactionSourceState.selectPressed) {
       // ...
   }
   ```
* Autres données spécifiques aux contrôleurs de mouvement, telles que le pavé tactile et/ou les coordonnées XY et l’État touché

   ```cs
   if (interactionSourceState.touchpadTouched && interactionSourceState.touchpadPosition.x > 0.5) {
       // ...
   }
   ```
   
* InteractionSourceKind à savoir si la source est une main ou un contrôleur de mouvement

   ```cs
   if (interactionSourceState.source.kind == InteractionSourceKind.Hand) {
       // ...
   }
   ```

### <a name="polling-for-forward-predicted-rendering-poses"></a>Interrogation pour les poses de rendu prédits par progression

* Lors de l’interrogation des données sources d’interaction à partir de mains et de contrôleurs, les poses que vous recevez sont des poses prédites pour le moment où les photons de ce frame atteindront les yeux de l’utilisateur.  Ces poses préprédits sont préférables pour le **rendu** du contrôleur ou d’un objet détenu dans chaque frame.  Si vous ciblez une pression ou une mise en route donnée avec le contrôleur, celles-ci seront plus précises si vous utilisez les API d’événements historiques décrites ci-dessous.

   ```cs
   var sourcePose = interactionSourceState.sourcePose;
   Vector3 sourceGripPosition;
   Quaternion sourceGripRotation;
   if ((sourcePose.TryGetPosition(out sourceGripPosition, InteractionSourceNode.Grip)) &&
       (sourcePose.TryGetRotation(out sourceGripRotation, InteractionSourceNode.Grip))) {
       // ...
   }
   ```

* Vous pouvez également obtenir la pose de tête préprédite pour ce frame actuel.  Comme avec la source, cela est utile pour le **rendu** d’un curseur, bien que le ciblage d’une presse ou d’une version donnée soit plus précis si vous utilisez les API d’événements historiques décrites ci-dessous.

   ```cs
   var headPose = interactionSourceState.headPose;
   var headRay = new Ray(headPose.position, headPose.forward);
   RaycastHit raycastHit;
   if (Physics.Raycast(headPose.position, headPose.forward, out raycastHit, 10)) {
       var cursorPos = raycastHit.point;
       // ...
   }
   ```

### <a name="handling-interaction-source-events"></a>Gestion des événements de source d’interaction

Pour gérer les événements d’entrée à mesure qu’ils se produisent avec leurs données d’historique exactes, vous pouvez gérer les événements de source d’interaction au lieu d’interroger.

Pour gérer les événements de source d’interaction:
* Inscrivez-vous pour un événement d’entrée *InteractionManager* . Pour chaque type d’événement d’interaction qui vous intéresse, vous devez vous y abonner.

   ```cs
   InteractionManager.InteractionSourcePressed += InteractionManager_InteractionSourcePressed;
   ```
   
* Gérez l’événement. Une fois que vous êtes abonné à un événement d’interaction, vous obtiendrez le rappel le cas échéant. Dans l’exemple *SourcePressed* , c’est une fois que la source a été détectée et avant qu’elle soit libérée ou perdue.

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

### <a name="how-to-stop-handling-an-event"></a>Comment arrêter la gestion d’un événement

Vous devez arrêter la gestion d’un événement lorsque vous n’êtes plus intéressé par l’événement ou si vous détruisez l’objet qui s’est abonné à l’événement. Pour arrêter la gestion de l’événement, vous devez vous désabonner de l’événement.

```cs
InteractionManager.InteractionSourcePressed -= InteractionManager_InteractionSourcePressed;
```

### <a name="list-of-interaction-source-events"></a>Liste des événements de source d’interaction

Les événements de la source d’interaction disponibles sont les suivants:
* *InteractionSourceDetected* (la source devient active)
* *InteractionSourceLost* (devient inactif)
* *InteractionSourcePressed* (appuyez sur, appuyez sur le bouton ou sélectionnez «Sélectionner»)
* *InteractionSourceReleased* (fin d’un TAP, d’un bouton relâché ou d’une fin de «SELECT»)
* *InteractionSourceUpdated* (déplace ou modifie un État quelconque)

### <a name="events-for-historical-targeting-poses-that-most-accurately-match-a-press-or-release"></a>Les événements pour le ciblage historique posent qui correspondent le plus précisément à une pression ou à une mise en sortie

Les API d’interrogation décrites précédemment fournissent à votre application des poses préprédits.  Bien que ces éléments prédits soient les plus adaptés pour le rendu du contrôleur ou d’un objet de poche virtuel, les nouvelles poses ne sont pas optimales pour le ciblage, pour deux raisons principales:
* Quand l’utilisateur appuie sur un bouton sur un contrôleur, il peut y avoir environ 20 ms de latence sans fil sur Bluetooth avant que le système ne reçoive la presse.
* Ensuite, si vous utilisez une pose préprédite, il y aura une autre 20 ms de prédiction directe appliquée pour cibler le moment où les photons du frame actuel atteindront les yeux de l’utilisateur.

Cela signifie que l’interrogation vous donne une source de pose ou de tête qui est de 30-40ms à partir de là où la tête et la mains de l’utilisateur ont été retirées lorsque l’appui ou la mise en place a eu lieu.  Pour l’entrée de la main HoloLens, bien qu’il n’y ait pas de délai de transmission sans fil, il existe un délai de traitement similaire pour détecter la presse.

Pour cibler avec précision en fonction de l’intention initiale de l’utilisateur pour une presse ou un contrôleur, vous devez utiliser la base de l’historique de la source ou de l’en-tête à partir de cet événement d’entrée *InteractionSourcePressed* ou *InteractionSourceReleased* .

Vous pouvez cibler une presse ou une mise en route avec des données de pose historiques à partir de la tête de l’utilisateur ou de son contrôleur:
* L’en-tête pose au moment où un mouvement ou un contrôleur s’est produit, ce qui peut être utilisé pour **cibler** pour déterminer à quoi l’utilisateur a [Gazing](gaze.md) :

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

* La source pose au moment où une pression du contrôleur de mouvement s’est produite, qui peut être utilisée pour le **ciblage** afin de déterminer le point de contrôle de l’utilisateur sur le contrôleur.  Il s’agit de l’état du contrôleur qui a rencontré la presse.  Si vous effectuez le rendu du contrôleur lui-même, vous pouvez demander le point de pose plutôt que le pose de la poignée pour faire tourner le ciblage de la cible à partir de ce que l’utilisateur prendra en compte l’astuce naturelle de ce contrôleur rendu:

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

### <a name="event-handlers-example"></a>Exemple de gestionnaires d’événements

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

## <a name="high-level-composite-gesture-apis-gesturerecognizer"></a>API de mouvement composite de haut niveau (GestureRecognizer)

**Espace de noms :** *UnityEngine. XR. WSA. Input*<br>
**Types**: *GestureRecognizer*, *GestureSettings*, *InteractionSourceKind*

Votre application peut également reconnaître les gestes composites de niveau supérieur pour les sources d’entrée spatiale, le TAP, le maintien, la manipulation et les gestes de navigation. Vous pouvez reconnaître ces gestes composites sur les [mains](gestures.md) et les contrôleurs de [mouvement](motion-controllers.md) à l’aide de GestureRecognizer.

Chaque événement de mouvement sur le GestureRecognizer fournit le SourceKind pour l’entrée, ainsi que le rayon de l’en-tête de ciblage au moment de l’événement. Certains événements fournissent des informations spécifiques au contexte.

Seules quelques étapes sont requises pour capturer des mouvements à l’aide d’un module de reconnaissance de mouvement:
1. Créer un module de reconnaissance de mouvement
2. Spécifier les gestes à surveiller
3. S’abonner à des événements pour ces mouvements
4. Démarrer la capture des mouvements

### <a name="create-a-new-gesture-recognizer"></a>Créer un module de reconnaissance de mouvement

Pour utiliser *GestureRecognizer*, vous devez avoir créé un *GestureRecognizer*:

```cs
GestureRecognizer recognizer = new GestureRecognizer();
```

### <a name="specify-which-gestures-to-watch-for"></a>Spécifier les gestes à surveiller

Spécifiez les gestes qui vous intéressent via *SetRecognizableGestures ()* :

```cs
recognizer.SetRecognizableGestures(GestureSettings.Tap | GestureSettings.Hold);
```

### <a name="subscribe-to-events-for-those-gestures"></a>S’abonner à des événements pour ces mouvements

Abonnez-vous aux événements pour les mouvements qui vous intéressent.

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
>Les mouvements de navigation et de manipulation s’excluent mutuellement sur une instance d’un *GestureRecognizer*.

### <a name="start-capturing-gestures"></a>Démarrer la capture des mouvements

Par défaut, un *GestureRecognizer* ne surveille pas l’entrée tant que *StartCapturingGestures ()* n’est pas appelé. Il est possible qu’un événement de mouvement soit généré après l’appel de *StopCapturingGestures ()* si l’entrée a été effectuée avant le frame dans lequel *StopCapturingGestures ()* a été traité. Le *GestureRecognizer* se souvient s’il était activé ou désactivé pendant la trame Previou dans laquelle le mouvement s’est réellement produit. il est donc fiable pour démarrer et arrêter la surveillance des mouvements en fonction du point de vue du regard de ce frame.

```cs
recognizer.StartCapturingGestures();
```

### <a name="stop-capturing-gestures"></a>Arrêter la capture des mouvements

Pour arrêter la reconnaissance des mouvements:

```cs
recognizer.StopCapturingGestures();
```

### <a name="removing-a-gesture-recognizer"></a>Suppression d’un module de reconnaissance de mouvement

N’oubliez pas de vous désabonner des événements souscrits avant de détruire un objet *GestureRecognizer* .

```cs
void OnDestroy()
{
    recognizer.Tapped -= GestureRecognizer_Tapped;
    recognizer.HoldStarted -= GestureRecognizer_HoldStarted;
    recognizer.HoldCompleted -= GestureRecognizer_HoldCompleted;
    recognizer.HoldCanceled -= GestureRecognizer_HoldCanceled;
}
```

## <a name="rendering-the-motion-controller-model-in-unity"></a>Rendu du modèle de contrôleur de mouvement dans Unity

![Modèle de contrôleur de mouvement et téléportage](images/motioncontrollertest-teleport-1000px.png)<br>
*Modèle de contrôleur de mouvement et téléportage*

Pour afficher les contrôleurs de mouvement de votre application qui correspondent aux contrôleurs physiques que vos utilisateurs détiennent et qui s’articulent à mesure que les différents boutons sont enfoncés, vous pouvez utiliser la **Prefab MotionController** dans le [Toolkit de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity/).  Ce Prefab charge dynamiquement le modèle glTF correct au moment de l’exécution à partir du pilote du contrôleur de mouvement installé du système.  Il est important de charger ces modèles de manière dynamique plutôt que de les importer manuellement dans l’éditeur, afin que votre application affiche des modèles 3D physiquement précis pour tous les contrôleurs actuels et futurs que vos utilisateurs peuvent avoir.

1. Suivez les instructions [prise en main](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/GettingStarted.md) pour télécharger la boîte à outils de réalité mixte et l’ajouter à votre projet Unity.
2. Si vous avez remplacé votre appareil photo par le *MixedRealityCameraParent* Prefab dans le cadre des étapes de prise en main, vous êtes en déplacement.  Prefab comprend le rendu du contrôleur de mouvement.  Sinon, ajoutez *Assets/HoloToolkit/Input/Prefabs/MotionControllers. Prefab* à votre scène à partir du volet de projet.  Vous pouvez ajouter ce Prefab en tant qu’enfant de n’importe quel objet parent que vous utilisez pour déplacer la caméra lorsque l’utilisateur téléporte dans votre scène, afin que les contrôleurs soient fournis avec l’utilisateur.  Si votre application n’implique pas de téléportage, ajoutez simplement le Prefab à la racine de votre scène.

## <a name="throwing-objects"></a>Lever des objets

La levée d’objets dans la réalité virtuelle est un problème plus difficile, alors il peut sembler évident. Comme avec la plupart des interactions basées physiquement, lorsque la levée dans le jeu se fait de manière inattendue, elle est immédiatement évidente et s’arrête à l’immersion. Nous avons passé un peu de temps à réfléchir à la façon de représenter un comportement de levée de manière physique et à rencontrer quelques recommandations, activées par le biais de mises à jour de notre plateforme, que nous aimerions partager avec vous.

Vous trouverez un exemple de la façon dont nous vous recommandons d’implémenter la levée [ici](https://github.com/keluecke/MixedRealityToolkit-Unity/blob/master/External/Unitypackages/ThrowingStarter.unitypackage). Cet exemple suit les quatre instructions suivantes:
* **Utilisez la *vélocité* du contrôleur au lieu de la position**. Dans la mise à jour de novembre de Windows, nous avons introduit un changement de comportement dans l' [État de suivi positionnel «approximatif](motion-controllers.md#controller-tracking-state)». Dans cet État, les informations de vélocité sur le contrôleur continuent d’être signalées aussi longtemps que nous pensons qu’il s’agit d’une précision élevée, qui est souvent plus longue que la position reste une précision élevée.
* **Incorporez la *vélocité angulaire* du contrôleur**. Cette logique est contenue `throwing.cs` dans le fichier de la `GetThrownObjectVelAngVel` méthode statique, dans le package lié ci-dessus:
   1. Comme la vélocité angulaire est conservée, l’objet levé doit conserver la même vélocité angulaire qu’au moment de la levée:`objectAngularVelocity = throwingControllerAngularVelocity;`
   2. Comme le centre de la masse de l’objet levé n’est probablement pas à l’origine de la poignée, il a probablement une vélocité différente de celle du contrôleur dans le cadre de référence de l’utilisateur. La partie de la rapidité de l’objet utilisée de cette façon est la vélocité tangentielle instantanée du centre de la masse de l’objet levé autour de l’origine du contrôleur. Cette vélocité tangentielle est le produit croisé de la vélocité angulaire du contrôleur avec le vecteur représentant la distance entre l’origine du contrôleur et le centre de la masse de l’objet levé.
    
      ```cs
      Vector3 radialVec = thrownObjectCenterOfMass - throwingControllerPos;
      Vector3 tangentialVelocity = Vector3.Cross(throwingControllerAngularVelocity, radialVec);
      ```
   
   3. La rapidité totale de l’objet levé est donc la somme de la vélocité du contrôleur et de cette vélocité tangentielle:`objectVelocity = throwingControllerVelocity + tangentialVelocity;`

* **Portez une attention particulière à l' *heure* à laquelle nous appliquons la vélocité**. Quand vous appuyez sur un bouton, il peut s’écouler jusqu’à 20 ms pour que cet événement se propage via Bluetooth au système d’exploitation. Cela signifie que si vous interrogez le changement d’état d’un contrôleur en l’appuyant sur non enfoncé, ou vice versa, le contrôleur vous pose les informations dont vous bénéficiez en effet. En outre, le contrôleur présenté par notre API d’interrogation est Forward prédit pour refléter une situation probable au moment où l’image sera affichée, ce qui pourrait être plus 20 ms à l’avenir. Cela est idéal pour le *rendu* des objets maintenus, mais il compose notre problème de temps pour *cibler* l’objet à mesure que nous calculons la trajectoire pour le moment où l’utilisateur a relâché sa levée. Heureusement, avec la mise à jour de novembre, lors de l’envoi d’un événement Unity comme *InteractionSourcePressed* ou *InteractionSourceReleased* , l’État comprend les données d’historique de la pose lorsque le bouton a été enfoncé ou relâché.  Pour optimiser le rendu du contrôleur et le ciblage du contrôleur lors des levées, vous devez utiliser correctement l’interrogation et l’événement, selon le cas:
   * Pour le rendu de chaque trame par le **contrôleur** , votre application doit positionner les *gameobject* du contrôleur au niveau du contrôleur avant prédiction pour le temps des photons du frame actuel.  Vous recevez ces données à partir d’API d’interrogation Unity, telles que *[XR. InputTracking. GetLocalPosition](https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html)* ou *[XR. WSA. Entrez. InteractionManager. GetCurrentReading](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.GetCurrentReading.html)* .
   * Pour le **ciblage du contrôleur** sur une presse ou une mise en sortie, votre application doit raycast et calculer des trajectoires en fonction de la pose du contrôleur historique pour cet événement Press ou Release.  Vous recevez ces données à partir d’API d’événements Unity, telles que *[InteractionManager. InteractionSourcePressed](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.InteractionSourcePressed.html)* .
* **Utilisez la poignée**. La rapidité et la vélocité angulaires sont rapportées par rapport à la pose de la poignée, et non à la pose du pointeur.

La génération continuera à s’améliorer avec les futures mises à jour de Windows, et vous pouvez vous attendre à trouver plus d’informations ici.

## <a name="gesture-and-motion-controllers-in-mrtk-v2"></a>Contrôleurs de mouvement et de mouvement dans MRTK v2

Vous pouvez accéder au contrôleur de mouvement et de mouvement à partir du gestionnaire d’entrée. 
* [Mouvement dans MRTK v2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Gestures.html)
* [Contrôleur de mouvement dans MRTK v2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Controllers.html)


## <a name="follow-along-with-tutorials"></a>Suivre les didacticiels

Des didacticiels pas à pas, avec des exemples de personnalisation plus détaillés, sont disponibles dans Mixed Reality Academy:

- [Réalité mixte - Entrées - Cours 211 : Mouvement](holograms-211.md)
- [Réalité mixte - Entrées - Cours 213 : Contrôleurs de mouvement](mixed-reality-213.md)

[![Entrée MR 213-contrôleur de mouvement](images/mr213-main-600px.jpg)](https://docs.microsoft.com/windows/mixed-reality/mixed-reality-213)<br>
*Entrée MR 213-contrôleur de mouvement*

## <a name="see-also"></a>Voir aussi

* [Mouvements](gestures.md)
* [Contrôleurs de mouvement](motion-controllers.md)


