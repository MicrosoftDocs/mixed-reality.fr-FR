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
# <a name="gestures-and-motion-controllers-in-unity"></a>Mouvements et les contrôleurs de mouvement dans Unity

Il existe deux façons principales d’agir votre [regards dans Unity](gaze-in-unity.md), [main mouvements](gestures.md) et [contrôleurs de mouvement](motion-controllers.md). Vous accédez aux données pour les deux sources d’entrée spatiale via les mêmes API dans Unity.

Unity fournit deux méthodes principales pour accéder à des données spatiales d’entrée pour la réalité mixte Windows, courantes *Input.GetButton/Input.GetAxis* API capables de fonctionner sur plusieurs Unity XR kits de développement logiciel, et un *InteractionManager / GestureRecognizer* API spécifique à Windows Mixed Reality qui expose l’ensemble complet des données spatiales d’entrée disponibles.

## <a name="unity-buttonaxis-mapping-table"></a>Table de mappage de bouton/axe Unity

Les ID de bouton et d’axe dans le tableau ci-dessous sont prises en charge dans le Gestionnaire d’entrée de Unity pour les contrôleurs de mouvement de réalité mixte Windows par le biais du *Input.GetButton/GetAxis* API, tandis que la colonne « Windows MR spécifique » fait référence aux propriétés disponible issu de la *InteractionSourceState* type. Chacune de ces API sont décrites en détail dans les sections ci-dessous.

Les mappages d’ID de bouton/axe pour la réalité mixte Windows correspond généralement à l’ID Oculus bouton/axe.

Les mappages d’ID de bouton/axe pour la réalité mixte Windows diffèrent des mappages de OpenVR de deux manières :
1. Le mappage utilise des ID de pavé tactile qui diffèrent des stick analogique, pour prendre en charge des contrôleurs avec sticks analogiques et un pavé tactile.
2. Le mappage permet d’éviter la surcharge de l’ID pour les boutons de Menu, laisser celles disponibles pour les boutons ABXY physiques de boutons A et X.

<table>
<tr>
<th rowspan="2">Entrée </th><th colspan="2"><a href="gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis">API Unity courantes</a><br />(Input.GetButton/GetAxis) </th><th rowspan="2"><a href="gestures-and-motion-controllers-in-unity.md#windows-specific-apis-xr.wsa.input">API d’entrée spécifiques à Windows MR</a><br />(XR.WSA.Input)</th>
</tr><tr>
<th> Gauche </th><th> Droite</th>
</tr><tr>
<td> Sélectionnez le déclencheur enfoncé </td><td> Axe 9 = 1.0 </td><td> Axe 10 = 1.0 </td><td> selectPressed</td>
</tr><tr>
<td> Sélectionnez la valeur analogique du déclencheur </td><td> Axe 9 </td><td> Axe 10 </td><td> selectPressedAmount</td>
</tr><tr>
<td> Sélectionnez le déclencheur partiellement enfoncé </td><td> Bouton 14 <i>(gamepad compat)</i> </td><td> Bouton 15 <i>(gamepad compat)</i> </td><td> selectPressedAmount &gt; 0.0</td>
</tr><tr>
<td> Bouton de menu enfoncé </td><td> Bouton 6 * </td><td> Bouton 7 * </td><td> menuPressed</td>
</tr><tr>
<td> Bouton de poignée enfoncé </td><td> Axe 11 = 1.0 (aucune valeur analogique)<br />Bouton 4 <i>(gamepad compat)</i> </td><td> Axe 12 = 1.0 (aucune valeur analogique)<br />Bouton 5 <i>(gamepad compat)</i> </td><td> saisi</td>
</tr><tr>
<td> Stick analogique X <i>(gauche : -1,0, droite : 1.0)</i> </td><td> Axe 1 </td><td> Axe 4 </td><td> thumbstickPosition.x</td>
</tr><tr>
<td> Stick analogique Y <i>(haut : -1,0, bas : 1.0)</i> </td><td> Axe 2 </td><td> Axe 5 </td><td> thumbstickPosition.y</td>
</tr><tr>
<td> Stick analogique enfoncé </td><td> Bouton 8 </td><td> Bouton 9 </td><td> thumbstickPressed</td>
</tr><tr>
<td> Pavé tactile X <i>(gauche : -1,0, droite : 1.0)</i> </td><td> Axe 17 * </td><td> Axe 19 * </td><td> touchpadPosition.x</td>
</tr><tr>
<td> Pavé tactile Y <i>(haut : -1,0, bas : 1.0)</i> </td><td> Axe 18 * </td><td> Axe 20 * </td><td> touchpadPosition.y</td>
</tr><tr>
<td> Pavé tactile couvertes </td><td> Bouton 18 * </td><td> Bouton 19 * </td><td> touchpadTouched</td>
</tr><tr>
<td> Pavé tactile enfoncé </td><td> Bouton 16 * </td><td> Bouton 17 * </td><td> touchpadPressed</td>
</tr><tr>
<td> 6DoF poignée pose ou pose de pointeur </td><td colspan="2"> <i>Poignée</i> poser uniquement : <a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html">XR.InputTracking.GetLocalPosition</a><br /><a href="https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalRotation.html">XR.InputTracking.GetLocalRotation</a></td><td> Passer <i>poignée</i> ou <i>pointeur</i> en tant qu’argument : sourceState.sourcePose.TryGetPosition<br />sourceState.sourcePose.TryGetRotation<br /></td>
</tr><tr>
<td> Suivi de l’état </td><td colspan="2"> <i>Analyse de précision et de la source de perte risque de position disponible uniquement via les API spécifiques MR</i> </td><td> <a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourcePose-positionAccuracy.html">sourceState.sourcePose.positionAccuracy</a><br /><a href="https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionSourceProperties-sourceLossRisk.html">sourceState.properties.sourceLossRisk</a></td>
</tr>
</table>

>[!NOTE]
>Ces ID de bouton/axe diffère de l’ID Unity utilise pour OpenVR en raison de collisions dans les mappages utilisés par les boîtiers de commande, Oculus tactile et OpenVR.

## <a name="grip-pose-vs-pointing-pose"></a>Pose de poignée et pose de pointage

Réalité mixte Windows prend en charge les contrôleurs de mouvements dans un large éventail de facteurs de forme, avec la conception de chaque contrôleur qui se différencie par sa relation entre la position des utilisateurs manuellement et naturel « transférer » direction que les applications doit utiliser pour le pointage lors du rendu de la contrôleur.

Pour mieux représenter ces contrôleurs, il existe deux types de risque de poser pour chaque source de l’interaction, vous pouvez passer en revue la **poignée pose** et **pose de pointeur**. Les deux les poignée pose et pointeur pose les coordonnées sont exprimées par toutes les API Unity dans les coordonnées de monde Unity globales.

### <a name="grip-pose"></a>Poignée pose

Le **poignée pose** représente l’emplacement de la portée de main détectée par un HoloLens ou palm contenant un contrôleur de mouvement.

Sur des casques IMMERSIFS, la pose de poignée mieux permet de restituer **main de l’utilisateur** ou **détenues par un objet à portée de main de l’utilisateur**, tel qu’un mot de passe ou les électrons. La pose de poignée est également utilisée lors de la visualisation d’un contrôleur de mouvements en tant que le **modèle pouvant être rendue** fourni par Windows pour un mouvement contrôleur utilise la pose de poignée que son origine et le centre de rotation.

La pose de poignée est définie spécifiquement comme suit :
* Le **Attrapez position**: Le centroïde de palm naturellement, tout en maintenant le contrôleur ajustée gauche ou droite pour centrer la position au sein de la poignée. Sur le contrôleur de mouvement Windows Mixed Reality, cette position aligne généralement avec le bouton de compréhension.
* Le **Attrapez axe de droite de l’orientation**: Lorsque vous ouvrez totalement la main pour former une pose plat 5-doigt, le rayon qui est normal pour votre palm (en avant à partir de la gauche palm, vers l’arrière de palm droite)
* Le **Attrapez axe vers l’avant de l’orientation**: Lorsque vous fermez votre main partiellement (comme le cas maintenant le contrôleur), le rayon pointe « forward » via le tube formé par vos doigts non curseur.
* Le **Attrapez orientation d’axe**: L’axe à distance impliqué par les définitions de droite, en avant.

Vous pouvez accéder à la pose de poignée via une entrée soit Unity entre fournisseurs API (*[XR. InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html). GetLocalPosition/Rotation*) ou via l’API Windows MR spécifiques (*sourceState.sourcePose.TryGetPosition/Rotation*, demande présentent des données pour le **poignée** nœud).

### <a name="pointer-pose"></a>Pose de pointeur

Le **pose de pointeur** représente l’info-bulle du contrôleur qui pointe vers l’avant.

La pose de pointeur fournie par le système qui convient pour raycast lorsque vous êtes **rendu le modèle de contrôleur lui-même**. Si vous restituez un autre objet virtuel à la place le contrôleur, par exemple un électrons virtuel, vous devez faire avec un rayon qui est plus naturel pour cet objet virtuel, comme un rayon qui transite le long de la gaine du modèle électrons définies par l’application. Étant donné que les utilisateurs peuvent voir l’objet virtuel et non du contrôleur physique, en pointant avec l’objet virtuel seront probablement plus naturel pour ceux qui utilisent votre application.

Actuellement, la pose de pointeur est disponible dans Unity uniquement par le biais de l’API Windows MR spécifiques, *sourceState.sourcePose.TryGetPosition/Rotation*, en passant dans *InteractionSourceNode.Pointer* comme le argument.

## <a name="controller-tracking-state"></a>État du contrôleur de suivi

Comme les casques, le contrôleur de mouvement de réalité mixte Windows ne requiert aucune configuration de capteurs de suivi externe. Au lieu de cela, les contrôleurs sont suivies par les capteurs dans le casque lui-même.

Si l’utilisateur déplace les contrôleurs de champ de vision du casque, dans la plupart des cas Windows continuera à déduire des positions de contrôleur et les fournir à l’application. Lorsque le contrôleur a perdu visual de suivi pour le temps, les positions du contrôleur supprimera les positions de précision approximative.

À ce stade, le système sera verrouillage de corps le contrôleur à l’utilisateur, suivi de position de l’utilisateur comme ils sont en déplacement, tout en exposant toujours l’orientation true du contrôleur à l’aide de ses capteurs orientation interne. De nombreuses applications qui utilisent des contrôleurs pour pointer vers et activer des éléments d’interface utilisateur peuvent fonctionner normalement en précision approximative sans le remarquer utilisateur.

La meilleure façon de faire une idée pour cela consiste à essayer vous-même. Regardez cette vidéo avec des exemples de contenu immersive qui fonctionne avec les contrôleurs de mouvement entre les différents États de suivi :

<br>

 >[!VIDEO https://www.youtube.com/embed/QK_fOFDHj0g]

### <a name="reasoning-about-tracking-state-explicitly"></a>Un peu de suivi de l’état explicitement

Les applications que vous souhaitent traiter les positions différemment en fonction de suivi de l’état peuvent aller plus loin et inspecter les propriétés sur l’état du contrôleur, tel que *SourceLossRisk* et *PositionAccuracy*:

<table>
<tr>
<th> Suivi de l’état </th><th> SourceLossRisk </th><th> PositionAccuracy </th><th> TryGetPosition</th>
</tr><tr>
<td> <b>Haute précision</b> </td><td style="background-color: green; color: white"> &lt; 1.0 </td><td style="background-color: green; color: white"> Élevée </td><td style="background-color: green; color: white"> true</td>
</tr><tr>
<td> <b>Haute précision (courant un risque de perte)</b> </td><td style="background-color: orange"> == 1.0 </td><td style="background-color: green; color: white"> Élevée </td><td style="background-color: green; color: white"> true</td>
</tr><tr>
<td> <b>Précision approximative</b> </td><td style="background-color: orange"> == 1.0 </td><td style="background-color: orange"> Approximate </td><td style="background-color: green; color: white"> true</td>
</tr><tr>
<td> <b>Aucune position</b> </td><td style="background-color: orange"> == 1.0 </td><td style="background-color: orange"> Approximate </td><td style="background-color: orange"> false</td>
</tr>
</table>

Ces États de suivi de contrôleur de mouvement sont définis comme suit :
* **Haute précision :** Pendant que le contrôleur de mouvement se trouve dans le champ de vision du casque, il fournira généralement positions extrêmement précise, en fonction de suivi visuel. Remarque qu’un contrôleur de déplacement qui momentanément quitte le champ de vision ou est momentanément masqué à partir des capteurs casque (par exemple, en revanche de l’utilisateur) continue à renvoyer pose analyse de haute précision pour une courte période, en fonction de l’inertie suivi du contrôleur lui-même.
* **Analyse de précision élevé (au risque de perdre) :** Lorsque l’utilisateur déplace le contrôleur de mouvement au-delà du bord du champ de vision du casque, le casque sera bientôt ne peut pas suivre visuellement position de contrôleur. L’application sait quand le contrôleur a atteint cette limite de l’angle d’ouverture en visualisant le **SourceLossRisk** atteindre 1.0. À ce stade, l’application peut choisir de les suspendre les mouvements de contrôleur qui nécessitent un flux régulier de risque de poser de haute qualité.
* **Précision approximative :** Lorsque le contrôleur a perdu visual de suivi pour le temps, les positions du contrôleur supprimera les positions de précision approximative. À ce stade, le système sera verrouillage de corps le contrôleur à l’utilisateur, suivi de position de l’utilisateur comme ils sont en déplacement, tout en exposant toujours l’orientation true du contrôleur à l’aide de ses capteurs orientation interne. De nombreuses applications qui utilisent des contrôleurs pour pointer vers et activer des éléments d’interface utilisateur peuvent fonctionner en temps normal, en précision approximative, sans le remarquer utilisateur. Applications plus lourd en termes d’entrée peuvent choisir de détecter cette liste à partir de **haute** précision à **approximatif** précision en inspectant le **PositionAccuracy** propriété, pour exemple pour donner à l’utilisateur un hitbox plus importante sur les cibles hors écran pendant ce temps.
* **Aucune position :** Alors que le contrôleur peut fonctionner à précision approximative pendant une longue période, parfois le système sache que même une position verrouillée de corps n’est pas significative pour le moment. Par exemple, un contrôleur qui a été activé simplement peut n’ont jamais été observé visuellement, ou un utilisateur peut placer un contrôleur qui est ensuite récupéré par quelqu'un d’autre vers le bas. À l’heure, le système ne fournira pas n’importe quelle position à l’application, et *TryGetPosition* retournera la valeur false.

## <a name="common-unity-apis-inputgetbuttongetaxis"></a>API Unity commune (Input.GetButton/GetAxis)

**Namespace :** *UnityEngine*, *UnityEngine.XR*<br>
**Types**: *Input*, *XR.InputTracking*

Unity utilise actuellement son général *Input.GetButton/Input.GetAxis* API pour exposer une entrée pour [le SDK Oculus](https://docs.unity3d.com/Manual/OculusControllers.html), [le SDK OpenVR](https://docs.unity3d.com/Manual/OpenVRControllers.html) et la réalité mixte Windows, y compris mains et contrôleurs de mouvement. Si votre application utilise ces API pour l’entrée, il peut facilement prendre en charge les contrôleurs de mouvement entre plusieurs XR kits de développement logiciel, y compris Windows Mixed Reality.

### <a name="getting-a-logical-buttons-pressed-state"></a>Obtention de l’état enfoncé d’un bouton logique

Pour utiliser l’entrée Unity générale API, vous commencerez généralement en organisant les boutons et les axes à des noms logiques dans le [Unity entrée Manager](https://docs.unity3d.com/Manual/ConventionalGameInput.html), liaison d’un bouton ou un axe ID à chaque nom. Vous pouvez ensuite écrire du code qui fait référence à ce nom de bouton/axe logique.

Par exemple, pour mapper le bouton de déclencheur du contrôleur de mouvement de gauche à l’action d’envoi, accédez à **Modifier > Paramètres du projet > entrée** dans Unity et développez les propriétés de la section d’envoi sous Axes. Modifier le **bouton positif** ou **bouton positif Alt** propriété à lire **bouton joystick 14**, comme suit :

![InputManager de Unity](images/unity-input-manager.png)<br>
*Unity InputManager*

Votre script peut ensuite vérifier pour l’action Envoyer à l’aide *Input.GetButton*:

```cs
if (Input.GetButton("Submit"))
{
  // ...
}
```
Vous pouvez ajouter des boutons plus logiques en modifiant le **taille** propriété sous **Axes**.

### <a name="getting-a-physical-buttons-pressed-state-directly"></a>L’obtention d’un état appuyé d’un bouton physique directement

Vous pouvez également accéder à boutons manuellement par leurs complet nom, en utilisant *Input.GetKey*:

```cs
if (Input.GetKey("joystick button 8"))
{
  // ...
}
```

### <a name="getting-a-hand-or-motion-controllers-pose"></a>Obtention d’une main ou pose du contrôleur de mouvement

Vous pouvez accéder à la position et la rotation du contrôleur, à l’aide de *XR. InputTracking*:

```cs
Vector3 leftPosition = InputTracking.GetLocalPosition(XRNode.LeftHand);
Quaternion leftRotation = InputTracking.GetLocalRotation(XRNode.LeftHand);
```

Notez que cela représente pose de poignée du contrôleur (où l’utilisateur appuie sur le contrôleur), ce qui est utile pour le rendu d’un à double tranchant ou électrons dans main de l’utilisateur ou un modèle du contrôleur lui-même.

Notez que la relation entre cette pose poignée et la pose de pointeur (où l’info-bulle du contrôleur de pointe) peut-être différer entre les contrôleurs. À ce stade, l’accès à la pose de pointeur du contrôleur n’est possible via l’entrée M. propres API, décrite dans les sections ci-dessous.

## <a name="windows-specific-apis-xrwsainput"></a>API Windows spécifique (XR. WSA. Entrée)

**Namespace :** *UnityEngine.XR.WSA.Input*<br>
**Types**: *InteractionManager*, *InteractionSourceState*, *InteractionSource*, *InteractionSourceProperties*, *InteractionSourceKind*, *InteractionSourceLocation*

Pour accéder à des informations plus détaillées sur l’entrée de main Windows Mixed Reality (pour HoloLens) et les contrôleurs de mouvement, vous pouvez choisir d’utiliser les API d’entrée spatiales spécifiques à Windows sous la *UnityEngine.XR.WSA.Input* espace de noms. Cela vous permet d’accéder à des informations supplémentaires, telles que de la précision de la position ou le type de source, ce qui vous permet d’indiquer les mains et les uns des autres contrôleurs de.

### <a name="polling-for-the-state-of-hands-and-motion-controllers"></a>Interrogation de l’état de mains et contrôleurs de mouvement

Vous pouvez interroger à l’état de cette image pour chaque source (contrôleur main ou de mouvement) d’interaction à l’aide de la *GetCurrentReading* (méthode).

```cs
var interactionSourceStates = InteractionManager.GetCurrentReading();
foreach (var interactionSourceState in interactionSourceStates) {
    // ...
}
```

Chaque *InteractionSourceState* vous obtenez précédent représente une source de l’interaction au moment actuel dans le temps. Le *InteractionSourceState* expose des informations telles que :
* Qui [types d’activations](motion-controllers.md) se produisent (sélectionnez/Menu/appréhendé/pavé tactile/stick analogique)

   ```cs
   if (interactionSourceState.selectPressed) {
       // ...
   }
   ```
* Autres données spécifiques aux contrôleurs de mouvement, tel le pavé tactile et/ou de stick analogique coordonnées XY et état touché

   ```cs
   if (interactionSourceState.touchpadTouched && interactionSourceState.touchpadPosition.x > 0.5) {
       // ...
   }
   ```
   
* Le InteractionSourceKind pour savoir si la source est une main ou un contrôleur de mouvement

   ```cs
   if (interactionSourceState.source.kind == InteractionSourceKind.Hand) {
       // ...
   }
   ```

### <a name="polling-for-forward-predicted-rendering-poses"></a>Interrogation de risque de poser prédit avant le rendu

* Lors de l’interrogation pour les données d’interaction de source des mains et les contrôleurs, vous obtenez le risque de poser est prédit avant le risque de poser pour le moment dans le temps lorsque photons de cette image seront atteignent les yeux de l’utilisateur.  Il est préférable d’utiliser ces risque de poser avant prédit pour **rendu** le contrôleur ou un détenu chaque image de l’objet.  Si vous êtes ciblant l’appui sur une donnée ou mise en production avec le contrôleur, il s’agit plus précis si vous utilisez l’événement d’historique API décrites ci-dessous.

   ```cs
   var sourcePose = interactionSourceState.sourcePose;
   Vector3 sourceGripPosition;
   Quaternion sourceGripRotation;
   if ((sourcePose.TryGetPosition(out sourceGripPosition, InteractionSourceNode.Grip)) &&
       (sourcePose.TryGetRotation(out sourceGripRotation, InteractionSourceNode.Grip))) {
       // ...
   }
   ```

* Vous pouvez également obtenir la pose principale a prédit l’avant pour ce frame actuel.  Comme avec la pose de la source, cela est utile pour **rendu** un curseur, bien que ciblant un press donné ou la mise en production sera plus précis si vous utilisez l’événement d’historique API décrites ci-dessous.

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

Pour gérer les événements d’entrée qu’elles se produisent avec leurs données pose historique précis, vous pouvez gérer les événements de source d’interaction au lieu d’interrogation.

Pour gérer les événements de source d’interaction :
* Inscrivez-vous à un *InteractionManager* événement d’entrée. Pour chaque type d’événement d’interaction qui vous intéresse, vous devez vous abonner à ce dernier.

   ```cs
   InteractionManager.InteractionSourcePressed += InteractionManager_InteractionSourcePressed;
   ```
   
* Gérer l’événement. Une fois que vous êtes abonné à un événement d’interaction, vous obtiendrez le rappel lorsque cela est approprié. Dans le *SourcePressed* exemple, il s’agit une fois que la source a été détectée et avant qu’il est publié ou perdue.

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

Vous devez arrêter la gestion d’un événement lorsque vous n’êtes plus intéressé par l’événement ou de détruire l’objet qui s’est abonnée à l’événement. Pour arrêter la gestion de l’événement, vous désabonner l’événement.

```cs
InteractionManager.InteractionSourcePressed -= InteractionManager_InteractionSourcePressed;
```

### <a name="list-of-interaction-source-events"></a>Liste des événements de source d’interaction

Les événements de source d’interaction disponibles sont :
* *InteractionSourceDetected* (source devient active)
* *InteractionSourceLost* (devient inactif)
* *InteractionSourcePressed* (tap, appuyez sur le bouton ou « Select » prononcés)
* *InteractionSourceReleased* (fin de drainage, du bouton ou fin de « Select » a été exprimée)
* *InteractionSourceUpdated* (déplace ou bien modifie un état)

### <a name="events-for-historical-targeting-poses-that-most-accurately-match-a-press-or-release"></a>Événements pour le ciblage historiques qui pose plus de précision correspondent à un press ou la mise en production

Les API d’interrogation décrits précédemment donner à votre application risque de poser avant prédit.  Alors que ces pose prédite conviennent le mieux pour le rendu le contrôleur ou un objet virtuel de poche, pose futures n’est pas optimales pour le ciblage, pour deux raisons principales :
* Lorsque l’utilisateur appuie sur un bouton sur un contrôleur, il peut y avoir environ 20 ms de latence sans fil via Bluetooth avant que le système ne reçoive la presse.
* Ensuite, si vous utilisez une pose prédite de transfert, il y aurait un autre 10-20 ms de prédiction directe appliquée pour cibler le temps lorsque les photons du frame actif seront atteignent les yeux de l’utilisateur.

Cela signifie que l’interrogation vous donne une pose source ou head poser c'est-à-dire 30-40 MS avant à partir de l’où l’utilisateur head et mains réellement étaient lors de la presse ou la version s’est produit.  Pour l’entrée de main HoloLens, il n’existe aucun délai de transmission sans fil, il existe un délai de traitement similaire pour détecter la presse.

Pour cible précisément en fonction de l’intention d’origine de l’utilisateur pour un press main ou de contrôleur, vous devez utiliser la source historiques pose ou principal pose de celui *InteractionSourcePressed* ou *InteractionSourceReleased* événement d’entrée.

Vous pouvez cibler un press ou libérer avec des données historiques pose de tête de l’utilisateur ou de leur contrôleur :
* La pose principale pour le moment dans le temps lorsque appuyez sur un contrôleur ou mouvement s’est produite, qui peuvent être utilisées pour **ciblant** pour déterminer ce que l’utilisateur a été [gazing](gaze.md) à :

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

* La pose de source pour le moment dans le temps lorsque appuyez sur un contrôleur de mouvement s’est produite, qui peuvent être utilisées pour **ciblant** pour déterminer ce que l’utilisateur a été pointant vers le contrôleur d’à.  Il s’agit de l’état du contrôleur qui a rencontré la presse.  Si vous restituez le contrôleur lui-même, vous pouvez demander la pose de pointeur plutôt que la pose de poignée pour dépanner le ciblage rayon à partir de ce que l’utilisateur prend en compte le Conseil naturels de qui a rendu le contrôleur :

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

## <a name="high-level-composite-gesture-apis-gesturerecognizer"></a>Mouvement de haut niveau composite API (GestureRecognizer)

**Namespace :** *UnityEngine.XR.WSA.Input*<br>
**Types**: *GestureRecognizer*, *GestureSettings*, *InteractionSourceKind*

Votre application peut aussi reconnaître des gestes composites de haut niveau pour les gestes de suspension, de Manipulation et de Navigation spatiale sources d’entrée, Tap. Vous pouvez reconnaître ces mouvements composites à la fois sur [mains](gestures.md) et [contrôleurs de mouvement](motion-controllers.md) à l’aide de la GestureRecognizer.

Chaque événement de mouvement sur le GestureRecognizer fournit le SourceKind pour l’entrée, ainsi que le ciblage rayon principal au moment de l’événement. Certains événements fournissent des informations de contexte supplémentaires spécifiques.

Il existe quelques étapes nécessaires pour capturer des mouvements à l’aide d’un module de reconnaissance de mouvement :
1. Créer un nouveau module de reconnaissance de mouvement
2. Spécifiez les gestes à surveiller
3. S’abonner aux événements pour ces mouvements
4. Démarrer la capture de mouvements

### <a name="create-a-new-gesture-recognizer"></a>Créer un nouveau module de reconnaissance de mouvement

Pour utiliser le *GestureRecognizer*, vous devez avoir créé un *GestureRecognizer*:

```cs
GestureRecognizer recognizer = new GestureRecognizer();
```

### <a name="specify-which-gestures-to-watch-for"></a>Spécifiez les gestes à surveiller

Spécifiez les gestes, vous êtes intéressé par le biais de *SetRecognizableGestures()*:

```cs
recognizer.SetRecognizableGestures(GestureSettings.Tap | GestureSettings.Hold);
```

### <a name="subscribe-to-events-for-those-gestures"></a>S’abonner aux événements pour ces mouvements

S’abonner aux événements pour les gestes que vous intéresse.

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
>Les mouvements de navigation et de Manipulation sont mutuellement exclusifs sur une instance d’un *GestureRecognizer*.

### <a name="start-capturing-gestures"></a>Démarrer la capture de mouvements

Par défaut, un *GestureRecognizer* ne surveille pas d’entrée jusqu'à ce que *StartCapturingGestures()* est appelée. Il est possible qu’un événement de mouvement peut être généré après *StopCapturingGestures()* est appelée si l’entrée a été effectuée avant l’image où *StopCapturingGestures()* a été traité. Le *GestureRecognizer* mémorisent s’il a été activé ou désactivé durant le frame Evaluation dans lequel le mouvement ayant réellement eu lieu et par conséquent, il est fiable pour démarrer et arrêter le suivi de mouvement basé sur le ciblage du pointage de regard de cette image.

```cs
recognizer.StartCapturingGestures();
```

### <a name="stop-capturing-gestures"></a>Arrêter la capture de mouvements

Pour arrêter la reconnaissance du mouvement :

```cs
recognizer.StopCapturingGestures();
```

### <a name="removing-a-gesture-recognizer"></a>Suppression d’un module de reconnaissance de mouvement

N’oubliez pas de se désabonner d’événements auxquels vous êtes abonnés à l’avant de détruire un *GestureRecognizer* objet.

```cs
void OnDestroy()
{
    recognizer.Tapped -= GestureRecognizer_Tapped;
    recognizer.HoldStarted -= GestureRecognizer_HoldStarted;
    recognizer.HoldCompleted -= GestureRecognizer_HoldCompleted;
    recognizer.HoldCanceled -= GestureRecognizer_HoldCanceled;
}
```

## <a name="rendering-the-motion-controller-model-in-unity"></a>Le modèle de contrôleur de mouvement dans Unity de rendu

![Téléportation et modèle de contrôleur de mouvement](images/motioncontrollertest-teleport-1000px.png)<br>
*Téléportation et modèle de contrôleur de mouvement*

Pour afficher les contrôleurs de mouvement dans votre application qui correspondent à vos utilisateurs sont maintenant et expliquer que différents boutons sont enfoncés les contrôleurs de physiques, vous pouvez utiliser la **MotionController préfabriqué** dans le [Toolkit de réalité mixte ](https://github.com/Microsoft/MixedRealityToolkit-Unity/).  Cette préfabriqué charge dynamiquement le modèle glTF correct lors de l’exécution à partir du pilote de contrôleur installé mouvement du système.  Il est important de charger ces modèles de manière dynamique plutôt que de les importer manuellement dans l’éditeur, afin que votre application n’affiche des modèles 3D physiquement précis pour des contrôleurs actuels et futurs de vos utilisateurs peuvent avoir.

1. Suivez le [mise en route](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/GettingStarted.md) instructions pour télécharger le Toolkit de réalité mixte et ajoutez-le à votre projet Unity.
2. Si vous avez remplacé votre appareil photo avec la *MixedRealityCameraParent* prefab en tant que partie de la procédure de mise en route, vous êtes fin prêt !  Ce préfabriqué inclut le rendu de contrôleur de mouvement.  Sinon, ajoutez *Assets/HoloToolkit/Input/Prefabs/MotionControllers.prefab* dans votre scène à partir du volet de projet.  Vous souhaiterez ajouter que prefab en tant qu’enfant de l’objet parent vous permet de déplacer la caméra autour lorsque l’utilisateur teleports dans votre scène, afin que les contrôleurs sont fournis, ainsi que l’utilisateur.  Si votre application n’implique pas teleporting, ajoutez simplement le préfabriqué à la racine de votre scène.

## <a name="throwing-objects"></a>Levée d’objets

Levée d’objets dans la réalité virtuelle est un problème difficile, puis il peut à première vue sembler. Comme avec les interactions en plus physiquement, lors de la levée de jeu jouent le rôle de manière inattendue, il est immédiatement évident et s’arrête en immersion. Nous avons passé des temps de réfléchir profondément sur la façon de représenter un comportement levant physiquement correct et ont développé quelques recommandations, activées par le biais des mises à jour sur notre plateforme, que nous souhaitons partager avec vous.

Vous trouverez un exemple de comment nous vous recommandons d’implémenter lever [ici](https://github.com/keluecke/MixedRealityToolkit-Unity/blob/master/External/Unitypackages/ThrowingStarter.unitypackage). Cet exemple suit ces quatre instructions :
* **Utiliser le contrôleur *velocity* au lieu de la position**. Dans la mise à jour de novembre de Windows, nous avons introduit un changement de comportement dans le ['' approximatif '' positionnels suivi de l’état](motion-controllers.md#controller-tracking-state). Dans cet état, rapidité plus d’informations sur le contrôleur de continuera à déclarer pour tant que nous pensons qu’il s’agit de haute précision, ce qui est souvent plus de temps que la position reste haute précision.
* **Incorporer le *vitesse angulaire* du contrôleur**. Cette logique est contenue dans le `throwing.cs` de fichiers dans le `GetThrownObjectVelAngVel` méthode statique, dans le package lié ci-dessus :
   1. Comme la vitesse angulaire est conservée, l’objet levé doit conserver la même vitesse angulaire telle qu’elle avait au moment de la levée : `objectAngularVelocity = throwingControllerAngularVelocity;`
   2. Comme le centre de gravité de l’objet levé est probablement que pas à l’origine de la poignée de pose, il comporte sûrement une rapidité différentes, puis au contrôleur de dans le cadre de référence de l’utilisateur. La partie de la vitesse de l’objet a contribué de cette façon est la rapidité de tangente instantanée du centre de gravité de l’objet levé autour de l’origine du contrôleur. Cette vitesse tangent est le produit croisé de la vitesse angulaire du contrôleur avec le vecteur qui représente la distance entre l’origine de contrôleur et le centre de gravité de l’objet levé.
    
      ```cs
      Vector3 radialVec = thrownObjectCenterOfMass - throwingControllerPos;
      Vector3 tangentialVelocity = Vector3.Cross(throwingControllerAngularVelocity, radialVec);
      ```
   
   3. La rapidité totale de l’objet levé est par conséquent, la somme de vitesse du contrôleur et cette rapidité tangente : `objectVelocity = throwingControllerVelocity + tangentialVelocity;`

* **Prêtez attention à la *temps* auquel nous appliquons la rapidité**. Lorsqu’un bouton est enfoncé, il peut prendre jusqu'à 20 ms pour cet événement à se propager via Bluetooth au système d’exploitation. Cela signifie que si vous interrogez un changement d’état de contrôleur à partir d’appuyé ne pas enfoncé ou vice versa, les informations de pose de contrôleur que vous obtenez avec lui sera avant cette modification dans un état. En outre, la pose de contrôleur présentée par notre API d’interrogation est transférer prédite afin de refléter une pose probablement au moment que le frame s’affichera, qui peut être plus de 20 ms puis à l’avenir. Cette fonction est utile pour *rendu* stockés les objets, mais composés de notre problème de temps pour *ciblant* l’objet que nous calculons la trajectoire pour le moment l’utilisateur a relâché leur throw. Heureusement, avec la mise à jour de novembre, lorsqu’un événement Unity comme *InteractionSourcePressed* ou *InteractionSourceReleased* est envoyé, l’état inclut les données historiques pose à partir du serveur lorsque le bouton a été effectivement appuyé ou publiées.  Pour obtenir le rendu de contrôleur plus précis et le contrôleur ciblant pendant lève, vous devez correctement utiliser l’interrogation et la gestion des événements, comme il convient :
   * Pour **rendu de contrôleur** chaque trame, votre application doit positionner du contrôleur *GameObject* au niveau du contrôleur avant prédit poser pour des temps de photon du frame actif.  Vous obtenez ces données à partir d’Unity comme API d’interrogation *[XR. InputTracking.GetLocalPosition](https://docs.unity3d.com/ScriptReference/XR.InputTracking.GetLocalPosition.html)* ou  *[XR. WSA. Input.InteractionManager.GetCurrentReading](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.GetCurrentReading.html)*.
   * Pour **contrôleur ciblant** selon une press ou une mise en production, votre application doit raycast et calculer des trajectoires selon la pose de contrôleur historiques pour cet événement press ou de mise en production.  Vous obtenez ces données à partir de l’API, d’événements Unity comme  *[InteractionManager.InteractionSourcePressed](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.InteractionSourcePressed.html)*.
* **Utilisez la pose de poignée**. Vitesse angulaire et la vélocité sont signalés par rapport à la pose de poignée, pas de pointeur pose.

Lever continuera à améliorer les futures mises à jour de Windows, et vous pouvez vous attendre à trouver plus d’informations sur ce dernier ici.

## <a name="accelerate-development-with-mixed-reality-toolkit"></a>Accélérez le développement avec le Kit de ressources de réalité mixte

Il existe deux scènes exemple sur InputManager et MotionController dans Unity. Au moyen de ces séquences, vous pouvez apprendre à utiliser InputManager de MRTK et accéder aux données gèrent les événements à partir des boutons du contrôleur de mouvement.

- [HoloToolkit-Examples/Input/Scenes/InputManagerTest.unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scenes/InputManagerTest.unity)
- [HoloToolkit-Examples/Input/Scenes/MotionControllerTest.unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/Input/Scenes/MotionControllerTest.unity)
- [Fichier Lisez-moi des détails techniques](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input)

![Exemple d’entrée des scènes dans MRTK](images/MRTK_ExampleScene_Input.png)<br>
*Exemple d’entrée des scènes dans MRTK*

### <a name="automatic-scene-setup"></a>Programme d’installation automatique de scène

Lorsque vous importez [MRTK publie des packages de Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases) ou cloner le projet à partir de la [référentiel GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity), vous vous apprêtez à trouver un nouveau menu « Toolkit de réalité mixte » dans Unity. Sous le menu « Configurer », vous verrez le menu « Application des paramètres de scène réalité mixte ». Lorsque vous cliquez dessus, il supprime l’appareil photo par défaut et ajoute les composants fondamentaux - [InputManager](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/InputManager.prefab), [MixedRealityCameraParent](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/MixedRealityCameraParent.prefab), et [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab).

![Menu MRTK pour le programme d’installation de scène](images/MRTK_Input_Menu.png)<br>
*Menu MRTK pour le programme d’installation de scène*

![Programme d’installation automatique de scène dans MRTK](images/MRTK_HowTo_Input1.png)<br>
*Programme d’installation automatique de scène dans MRTK*

### <a name="mixedrealitycamera-prefab"></a>MixedRealityCamera prefab

Vous pouvez également ajouter manuellement à partir du panneau projet. Vous pouvez trouver ces composants en tant que prefabs. Si vous effectuez une recherche **MixedRealityCamera**, vous serez en mesure de voir les deux prefabs caméra différente. La différence est, **MixedRealityCamera** est l’appareil photo uniquement prefab tandis que **MixedRealityCameraParent** inclut des composants supplémentaires pour les casques IMMERSIFS telles que téléportation, Motion Contrôleur et limites.

![Prefabs caméra dans MRTK](images/MRTK_HowTo_Input2.png)<br>
*Prefabs caméra dans MRTK*

**MixedRealtyCamera** prend en charge HoloLens et immersif casque. Il détecte le type d’appareil et optimise les propriétés telles que d’effacer les indicateurs et Skybox. Vous trouverez ci-dessous certaines des propriétés utiles, vous pouvez personnaliser comme curseur personnalisé, les modèles de contrôleur de mouvement et Floor.

![Propriétés pour le contrôleur de mouvement, curseur et étage](images/MRTK_HowTo_Input3.png)<br>
*Propriétés pour le contrôleur de mouvement, curseur et étage*

## <a name="follow-along-with-tutorials"></a>Suivre des didacticiels

Didacticiels pas à pas, avec des exemples de personnalisation plus détaillées, sont disponibles dans l’Académie de réalité mixte :

- [Entrée M. 211 : Gesture](holograms-211.md)
- [Entrée M. 213 : Contrôleurs de mouvement](mixed-reality-213.md)

[![Entrée M. 213 - contrôleur de mouvement](images/mr213-main-600px.jpg)](https://docs.microsoft.com/windows/mixed-reality/mixed-reality-213)<br>
*Entrée M. 213 - contrôleur de mouvement*

## <a name="see-also"></a>Voir aussi

* [Mouvements](gestures.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [UnityEngine.XR.WSA.Input](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.html)
* [UnityEngine.XR.InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html)
* [InteractionInputSource.cs dans MixedRealityToolkit-Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Scripts/InputSources/InteractionInputSource.cs)
