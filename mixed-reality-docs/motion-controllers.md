---
title: Contrôleurs de mouvement
description: Détails sur les contrôleurs de mouvement de réalité mixte.
author: wguyman
ms.author: wguyman
ms.date: 03/21/2018
ms.topic: article
keywords: contrôleurs 6DOF, contrôleurs de mouvement
ms.openlocfilehash: 84ebc6c0d7c63e58346b6ee9e565811bc40571b5
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437853"
---
# <a name="motion-controllers"></a>Contrôleurs de mouvement

:::row:::
    :::column:::
        Les contrôleurs de mouvement sont des [accessoires matériels](hardware-accessories.md) qui permettent aux utilisateurs de prendre des mesures en réalité mixte. L’un des avantages des contrôleurs de mouvement par rapport aux [gestes](gaze-and-commit.md#composite-gestures) est que les contrôleurs ont une position précise dans l’espace, ce qui permet une interaction fine en grain avec les objets numériques. Pour les casques immersifs Windows Mixed Reality, les contrôleurs de mouvement constituent la principale façon dont les utilisateurs effectuent des actions dans leur environnement.<br>
        <br>
        *Image : contrôleur de mouvement Windows Mixed Reality*
    :::column-end:::
        :::column:::
       ![Contrôleurs de mouvement Windows Mixed Reality](images/winmr-ck-1080x1080-350px.jpg)<br> 
    :::column-end:::
:::row-end:::

<br>

---

## <a name="device-support"></a>Périphériques pris en charge

<table>
<colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
</colgroup>
<tr>
     <td><strong>Fonctionnalité</strong></td>
     <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
     <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
     <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
</tr>
<tr>
     <td>Contrôleurs de mouvement</td>
     <td>❌</td>
     <td>❌</td>
     <td>✔️</td>
</tr>
</table>

## <a name="hardware-details"></a>Détails du matériel

<iframe width="940" height="530" src="https://www.youtube.com/embed/1nlcdDNOdm8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Les contrôleurs de mouvement Windows Mixed Reality permettent un suivi précis et réactif des mouvements dans votre champ de vue à l’aide des capteurs du casque immersif, ce qui signifie qu’il n’est pas nécessaire d’installer le matériel sur les murs de votre espace. Ces contrôleurs de mouvement offriront la même facilité de configuration et de portabilité que les casques immersifs immersifs de Windows Mixed Reality. Nos partenaires d’appareils envisagent de commercialiser et de vendre ces contrôleurs sur les étagères de la vente au détail.

![connaître votre](images/controllerimage-750px.png) de contrôleur<br>
*Découverte de votre contrôleur*

**Éléments**
* Suivi optique
* Stead
* Bouton de manipulation
* Stick
* Pavé tactile

## <a name="setup"></a>Installation

### <a name="before-you-begin"></a>Avant de commencer

**Vous aurez besoin des éléments suivants :**
* Ensemble de deux contrôleurs de mouvement.
* Quatre piles AA.
* Un PC compatible Bluetooth 4,0.

**Rechercher les mises à jour de Windows, Unity et Driver**
* Consultez [installer les outils](install-the-tools.md) pour les versions préférées de Windows, Unity, etc. pour le développement de la réalité mixte.
* Veillez à disposer des [pilotes de contrôleur de mouvement et de casque](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/mixed-reality-software)les plus récents.

### <a name="pairing-controllers"></a>Contrôleurs associés

Les contrôleurs de mouvement peuvent être liés à un PC hôte à l’aide de paramètres Windows, comme tout autre appareil Bluetooth.

1. Insérez 2 piles AA à l’arrière du contrôleur. Laissez la couverture de la batterie désactivée pour le moment.
2. Si vous utilisez une carte Bluetooth USB externe au lieu d’une radio Bluetooth intégrée, passez en revue les [meilleures pratiques Bluetooth](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#bluetooth-best-practices) avant de continuer. Pour la configuration du bureau avec la radio intégrée, vérifiez que l’antenne est connectée.
3. Ouvrez **Paramètres Windows** -> **appareils** -> **Ajouter bluetooth ou un autre appareil** -> **Bluetooth** et supprimer toutes les instances antérieures de « pilote de mouvement – droite » et « contrôleur de mouvement – gauche ». Consultez également la catégorie autres périphériques au bas de la liste.
4. Sélectionnez **Ajouter un périphérique Bluetooth ou un autre appareil** pour voir comment détecter des appareils Bluetooth.
5. Appuyez sur le bouton Windows du contrôleur et maintenez-le enfoncé pour le mettre sous tension.
6. Appuyez sur le bouton d’appariement (onglet dans le compartiment batterie) et maintenez-le enfoncé jusqu’à ce que les LED commencent à clignoter.

:::row:::
    :::column:::
7. Attendez que « contrôleur de mouvement-gauche » ou « contrôleur de mouvement-droite » apparaisse au bas de la liste. Sélectionnez une paire. Le contrôleur vibrera une seule fois lors de la connexion.<br>
        <br>
        *Image : sélectionnez « contrôleur de mouvement » à coupler. s’il existe plusieurs instances, sélectionnez-en une en bas de la liste.*
    :::column-end:::
        :::column:::
       ![Sélectionnez contrôleur de mouvement à coupler, si plusieurs instances en sélectionnent une dans la partie inférieure de la liste.](images/450px-bluetooth-add-a-device-300px.png)<br> 
    :::column-end:::
:::row-end:::
   
8. Le contrôleur s’affiche dans les paramètres Bluetooth sous la **catégorie « souris, clavier & stylet »** comme **connecté**. À ce stade, vous pouvez obtenir une mise à jour du microprogramme, voir la [section suivante](motion-controllers.md#updating-controller-firmware).
9. Reconnectez la couverture de la batterie.
10. Répétez les étapes 1-9 pour le deuxième contrôleur.

<br>

:::row:::
    :::column:::
        Après avoir couplé avec succès les deux contrôleurs, vos paramètres doivent ressembler à ceci sous **la catégorie « souris, clavier, & stylet »** . <br>
        <br>
        *Image : contrôleurs de mouvement connectés*
    :::column-end:::
        :::column:::
       ![Contrôleurs de mouvement connectés](images/450px-motion-controller-connected-300px.png)<br>
    :::column-end:::
:::row-end:::

Si les contrôleurs sont désactivés après l’appariement, leur état s’affiche comme jumelé. Si les contrôleurs restent définitivement sous « autres périphériques », la combinaison de catégories n’a peut-être été que partiellement terminée et doit être réexécutée pour obtenir la fonctionnalité du contrôleur.

### <a name="updating-controller-firmware"></a>Mise à jour du microprogramme du contrôleur

* Si un casque immersif est connecté à votre PC et que le nouveau microprogramme du contrôleur est disponible, le microprogramme est automatiquement envoyé à vos contrôleurs de mouvement la prochaine fois qu’ils sont allumés. Les mises à jour du microprogramme du contrôleur sont indiquées par un modèle de quadrants lumineux lumineux dans un mouvement circulaire et prennent 1-2 minutes.


:::row:::
    :::column:::
* Une fois la mise à jour du microprogramme terminée, les contrôleurs redémarrent et se reconnectent. Les deux contrôleurs doivent être connectés maintenant. <br>
        <br>
        *Image : contrôleurs connectés dans les paramètres Bluetooth*
    :::column-end:::
        :::column:::
       ![Contrôleurs connectés](images/cyk-connected-300px.jpg)<br>
    :::column-end:::
:::row-end:::


* Vérifiez que vos contrôleurs fonctionnent correctement :
    1. Lancez le **portail de réalité mixte** et entrez votre page d’hébergement de la réalité mixte.
    2. Déplacez vos contrôleurs et vérifiez le suivi, les boutons de test et vérifiez que la [téléportage](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) fonctionne. Si ce n’est pas le cas, consultez [résolution des problèmes du contrôleur de mouvement](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#motion-controllers).

## <a name="gazing-and-pointing"></a>Gazing et pointage

Windows Mixed Reality prend en charge deux modèles clés pour l’interaction, le point de présence **et la validation** , ainsi que le **point et la validation**:
* Avec le point de suspension **et la validation**, les utilisateurs ciblent un objet avec le [regard](gaze-and-commit.md) , puis sélectionnent les objets avec des robinets à main, un boîtier de soucoursment, un clic ou leur voix.
* Avec **point et validation**, un utilisateur peut viser un contrôleur de mouvement de pointage sur l’objet cible, puis sélectionner des objets avec le déclencheur du contrôleur.

Les applications qui prennent en charge le pointage avec les contrôleurs de mouvement doivent également activer les interactions pilotées par le regard dans la mesure du possible, pour permettre aux utilisateurs de choisir les périphériques d’entrée qu’ils utilisent.

### <a name="managing-recoil-when-pointing"></a>Gestion de la réenroulement lors du pointage

Lorsque vous utilisez des contrôleurs de mouvement pour pointer et valider, vos utilisateurs utilisent le contrôleur pour cibler, puis agir en extrayant son déclencheur. Les utilisateurs qui extraient le déclencheur peuvent finir par faire en sorte que le contrôleur soit plus élevé à la fin de l’extraction du déclencheur que prévu.

Pour gérer ce type de réenroulement qui peut se produire lorsque les utilisateurs extraient le déclencheur, votre application peut aligner son cible sur Ray lorsque la valeur de l’axe analogique du déclencheur dépasse 0,0. Vous pouvez ensuite prendre une mesure à l’aide du ciblage de rayon de quelques frames plus tard, une fois que la valeur du déclencheur atteint 1,0, tant que la dernière pression se produit dans une fenêtre de temps abrégée. Lors de l’utilisation du [mouvement composite composite](gaze-and-commit.md#composite-gestures)de niveau supérieur, Windows gère cette capture et ce délai d’expiration pour le ciblage.

## <a name="grip-pose-vs-pointing-pose"></a>Poignée de pose et pose de pointage

Windows Mixed Reality prend en charge les contrôleurs de mouvement dans un large éventail de facteurs de forme, la conception de chaque contrôleur étant différente dans sa relation entre la position de l’utilisateur et la direction « avant » naturelle que les applications doivent utiliser pour pointer lors du rendu de la SideWinder.

Pour mieux représenter ces contrôleurs, il existe deux genres de poses que vous pouvez examiner pour chaque source d’interaction, le pose de la **poignée** et le **pointeur se posent**.

### <a name="grip-pose"></a>Poignée de pose

La **poignée** représente l’emplacement de la paume d’une main détectée par un HoloLens ou la poche qui détient un contrôleur de mouvement.

Sur les casques immersifs, le pose de la poignée est utilisé pour restituer **la main de l’utilisateur** ou **un objet détenu par l’utilisateur**, tel qu’un épée ou un pistolet. La poignée est également utilisée lors de la visualisation d’un contrôleur de mouvement, car le **modèle de rendu** fourni par Windows pour un contrôleur de mouvement utilise la poignée comme son origine et le centre de rotation.

La poignée est définie spécifiquement comme suit :
* Position de la **poignée**: le centre de la poche quand il maintient le contrôleur naturellement, ajusté à gauche ou à droite pour centrer la position au sein de la poignée. Sur le contrôleur de mouvement Windows Mixed Reality, cette position s’aligne généralement avec le bouton de saisie.
* **Axe droit de l’orientation de la poignée**: lorsque vous ouvrez complètement votre main pour former une pose plate à 5 doigts, le rayon normal à votre paume (en avant à partir de la poche de gauche, en arrière depuis la paume de droite)
* **Axe avant de l’orientation de la poignée**: quand vous fermez partiellement votre main (comme si vous détenir le contrôleur), le rayon qui pointe vers l’avant dans le tube formé par vos doigts non thumbs.
* **Axe vers le haut de l’orientation**: l’axe vers le haut, impliqué dans les définitions Right et Forward.

### <a name="pointer-pose"></a>Pose du pointeur

Le **pointeur de pose** représente l’extrémité du contrôleur pointant vers l’avant.

Le pointeur fourni par le système est le mieux utilisé pour raycast lorsque vous effectuez **le rendu du modèle de contrôleur lui-même**. Si vous effectuez le rendu d’un autre objet virtuel à la place du contrôleur, tel qu’un pistolet virtuel, vous devez pointer vers un rayon qui est le plus naturel pour cet objet virtuel, tel qu’un rayon qui traverse le canon du modèle de pistolet défini par l’application. Étant donné que les utilisateurs peuvent voir l’objet virtuel et non le contrôleur physique, le fait de pointer avec l’objet virtuel sera probablement plus naturel pour ceux qui utilisent votre application.

## <a name="controller-tracking-state"></a>État du suivi du contrôleur

À l’instar des casques, le contrôleur de mouvement Windows Mixed Reality ne nécessite pas de configuration de capteurs de suivi externe. Au lieu de cela, les contrôleurs sont suivis par des capteurs dans le casque lui-même.

Si l’utilisateur déplace les contrôleurs du champ de vue du casque, dans la plupart des cas, Windows continue à déduire les positions des contrôleurs et à les fournir à l’application. Lorsque le contrôleur a perdu le suivi visuel suffisamment longtemps, les positions du contrôleur sont découpées à des positions de précision approximatives.

À ce stade, le système va verrouiller le contrôleur à l’utilisateur, en effectuant le suivi de la position de l’utilisateur lors de son déplacement, tout en exposant l’orientation réelle du contrôleur à l’aide de ses capteurs d’orientation internes. De nombreuses applications qui utilisent des contrôleurs pour pointer et activer des éléments d’interface utilisateur peuvent fonctionner normalement avec une précision approximative sans que l’utilisateur ne remarque.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/rkDpRllbLII" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### <a name="reasoning-about-tracking-state-explicitly"></a>Raisonnement sur le suivi de l’État explicitement

Les applications qui souhaitent traiter différemment les positions en fonction de l’état de suivi peuvent aller plus loin et inspecter les propriétés de l’état du contrôleur, telles que SourceLossRisk et PositionAccuracy :

<table>
<tr>
<th> État du suivi </th><th> SourceLossRisk </th><th> PositionAccuracy </th><th> TryGetPosition</th>
</tr><tr>
<td>   de <b>haute précision</b></td><td style="background-color: green; color: white"> &lt; 1,0 </td><td style="background-color: green; color: white"> Élevé </td><td style="background-color: green; color: white"> true</td>
</tr><tr>
<td> <b>Haute précision (risque de perte)</b> </td><td style="background-color: orange"> = = 1,0 </td><td style="background-color: green; color: white"> Élevé </td><td style="background-color: green; color: white"> true</td>
</tr><tr>
<td> <b>Précision approximative</b> </td><td style="background-color: orange"> = = 1,0 </td><td style="background-color: orange"> Approximate </td><td style="background-color: green; color: white"> true</td>
</tr><tr>
<td> <b>Aucune position</b> </td><td style="background-color: orange"> = = 1,0 </td><td style="background-color: orange"> Approximate </td><td style="background-color: orange"> false</td>
</tr>
</table>



Ces États de suivi du contrôleur de mouvement sont définis comme suit :
* **Précision élevée :** Alors que le contrôleur de mouvement se trouve dans le champ de vision du casque, il fournit généralement des positions à grande précision, en fonction du suivi visuel. Notez qu’un contrôleur mobile qui laisse momentanément le champ de vue ou est momentanément masqué à partir des capteurs du casque (par exemple, par l’autre côté de l’utilisateur) continue à retourner des poses de grande précision pendant une brève période, en fonction du suivi inertiel du contrôleur. automatiquement.
* **Haute précision (risque de perte) :** Lorsque l’utilisateur déplace le contrôleur de mouvement au-delà du bord du champ de vue du casque, le casque ne pourra bientôt pas suivre la position du contrôleur. L’application sait quand le contrôleur a atteint cette limite d’aide en regardant le **SourceLossRisk** REACH 1,0. À ce stade, l’application peut choisir de suspendre les gestes de contrôleur qui nécessitent un flux constant de poses très haute qualité.
* **Précision approximative :** Lorsque le contrôleur a perdu le suivi visuel suffisamment longtemps, les positions du contrôleur sont découpées à des positions de précision approximatives. À ce stade, le système va verrouiller le contrôleur à l’utilisateur, en effectuant le suivi de la position de l’utilisateur lors de son déplacement, tout en exposant l’orientation réelle du contrôleur à l’aide de ses capteurs d’orientation internes. De nombreuses applications qui utilisent des contrôleurs pour pointer et activer des éléments d’interface utilisateur peuvent fonctionner normalement, tout en ayant une précision approximative, sans que l’utilisateur ne remarque. Les applications avec des exigences d’entrée plus lourdes peuvent choisir de déterminer ce déplacement de la **haute** précision à une précision **approximative** en inspectant la propriété **PositionAccuracy** , par exemple pour fournir à l’utilisateur un hitbox plus généreux sur les cibles hors écran pendant ce temps.
* **Aucune position :** Alors que le contrôleur peut fonctionner à des fins de précision approximative pendant une longue période, le système sait parfois que même une position verrouillée par le corps n’est pas significative pour le moment. Par exemple, un contrôleur qui vient d’être activé n’a peut-être jamais été observé visuellement, ou un utilisateur peut mettre un contrôleur qui est ensuite récupéré par une autre personne. À ce moment-là, le système ne fournit aucune position à l’application, et **TryGetPosition** retourne la valeur false.

## <a name="interactions-low-level-spatial-input"></a>Interactions : entrée spatiale de bas niveau

Les interactions de base entre les contrôleurs mains et Motion sont **Select**, **menu**, rescelle, **Touchpad** **,** **stick analogique**et **familial**.
* **Select** est l’interaction principale pour activer un hologramme, qui consiste en une pression suivie d’une mise en sortie. Pour les contrôleurs de mouvement, vous effectuez une pression Select à l’aide du déclencheur du contrôleur. D’autres façons d’effectuer une sélection sont en parlant la [commande vocale](voice-input.md) « Select ». La même interaction SELECT peut être utilisée dans n’importe quelle application. Pensez à sélectionner comme équivalent d’un clic de souris, une action universelle que vous découvrez une fois, puis appliquez-la à toutes vos applications.
* **Menu** est l’interaction secondaire pour agir sur un objet, utilisée pour extraire un menu contextuel ou effectuer une autre action secondaire. Avec les contrôleurs de mouvement, vous pouvez effectuer une action de menu à l’aide du bouton de *menu* du contrôleur. (c’est-à-dire le bouton avec l’icône « menu » du hamburger)
* **Saisissez** comment les utilisateurs peuvent directement agir sur les objets à leur disposition pour les manipuler. Avec les contrôleurs de mouvement, vous pouvez faire une action en appuyant sur votre avant-première. Un contrôleur de mouvement peut détecter une compréhension à l’aide d’un bouton de manipulation, d’un déclencheur Palm ou d’un autre capteur.
* Le **pavé tactile** permet à l’utilisateur d’ajuster une action en deux dimensions le long de la surface du pavé tactile d’un contrôleur de mouvement, en validant l’action en cliquant sur le bouton du pavé tactile. Les pavés tactiles fournissent un état appuyé, un État touché et des coordonnées XY normalisées. Plage X et Y comprise entre-1 et 1 dans la plage du pavé tactile circulaire, avec un centre à (0,0). Pour X,-1 est sur la gauche et 1 est sur la droite. Pour Y,-1 est en bas et 1 est en haut.
* Le **stick analogique** permet à l’utilisateur d’ajuster une action en deux dimensions en déplaçant le stick analogique d’un contrôleur de mouvement dans sa plage circulaire, en validant l’action en cliquant sur le stick analogique. Thumbsticks fournissent également un état appuyé et des coordonnées XY normalisées. Plage X et Y comprise entre-1 et 1 dans la plage du pavé tactile circulaire, avec un centre à (0,0). Pour X,-1 est sur la gauche et 1 est sur la droite. Pour Y,-1 est en bas et 1 est en haut.
* La **page d’accueil** est une action système spéciale qui est utilisée pour revenir au menu Démarrer. Cela revient à appuyer sur la touche Windows d’un clavier ou le bouton Xbox sur un contrôleur Xbox. Vous pouvez utiliser le bouton Windows d’un contrôleur de mouvement pour accéder à la page d’hébergement. Notez que vous pouvez toujours revenir au début en disant « Hey Cortana, Go Accueil ». Les applications ne peuvent pas réagir spécifiquement aux actions d’hébergement, car elles sont gérées par le système.

## <a name="composite-gestures-high-level-spatial-input"></a>Gestes composites : entrée spatiale de haut niveau

Les [gestes](gaze-and-commit.md#composite-gestures) à la main et les contrôleurs de mouvement peuvent être suivis au fil du temps pour détecter un ensemble commun de **[gestes composites](gaze-and-commit.md#composite-gestures)** de haut niveau. Cela permet à votre application de détecter les gestes d' **appui**, de **maintien**, de **manipulation** et de **navigation** de haut niveau, que les utilisateurs finissent par utiliser des mains ou des contrôleurs.

## <a name="rendering-the-motion-controller-model"></a>Rendu du modèle de contrôleur de mouvement

**modèles de contrôleur 3D** Windows met à la disposition des applications un modèle pouvant être rendu de chaque contrôleur de mouvement actuellement actif dans le système. En faisant en sorte que votre application charge et articule dynamiquement ces modèles de contrôleur fournis par le système lors de l’exécution, vous pouvez vous assurer que votre application est compatible avec les futures conceptions de contrôleur.

Ces modèles de rendu doivent tous être rendus au niveau de la **poignée** du contrôleur, car l’origine du modèle est alignée sur ce point dans le monde physique. Si vous affichez des modèles de contrôleur, vous souhaiterez peut-être raycast dans votre scène à partir du point de vue du **pointeur**, qui représente le rayon le long duquel les utilisateurs s’attendent naturellement à POINTER, étant donné la conception physique du contrôleur.

Pour plus d’informations sur la façon de charger dynamiquement des modèles de contrôleur dans Unity, consultez la section [rendu du modèle de contrôleur de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md#rendering-the-motion-controller-model-in-unity) .

**art de ligne de contrôleur 2D** Bien que nous vous recommandons de joindre des commandes et des conseils de contrôleur dans l’application aux modèles de contrôleur dans l’application eux-mêmes, certains développeurs peuvent souhaiter utiliser des représentations d’art de ligne 2D des contrôleurs de mouvement dans un « didacticiel » plat ou une interface utilisateur « How-to ». Pour ces développeurs, nous avons créé des fichiers d’art de ligne de contrôleur de mouvement. png disponibles dans le noir et le blanc ci-dessous (cliquez avec le bouton droit pour enregistrer).

![Aperçu des images de ligne des contrôleurs de mouvement](images/motioncontrollers-black-preview-300px.png)

[Image de ligne des contrôleurs de mouvement pleine résolution dans' ' 'White' ' '](images/motioncontrollers-white.png)
 
[Image de ligne des contrôleurs de mouvement pleine résolution dans' ' 'noir' ' '](images/motioncontrollers-black.png)

## <a name="faq"></a>Forum Aux Questions

### <a name="can-i-pair-motion-controllers-to-multiple-pcs"></a>Puis-je coupler des contrôleurs de mouvement à plusieurs PC ?

Les contrôleurs de mouvement prennent en charge le jumelage avec un seul PC. Suivez les instructions relatives à la [configuration du contrôleur de mouvement](motion-controllers.md#setup) pour coupler vos contrôleurs.

### <a name="how-do-i-update-motion-controller-firmware"></a>Comment faire mettre à jour le microprogramme du contrôleur de mouvement ?

Le microprogramme du contrôleur de mouvement fait partie du pilote du casque et sera mis à jour automatiquement à la connexion, si nécessaire. Les mises à jour de microprogramme prennent généralement 1-2 minutes en fonction de la radio Bluetooth et de la qualité de liaison. Dans de rares cas, les mises à jour du microprogramme du contrôleur peuvent prendre jusqu’à 10 minutes, ce qui peut indiquer une connectivité Bluetooth médiocre ou des interférences radio. Pour résoudre les problèmes de connectivité, consultez [meilleures pratiques pour Bluetooth dans le Guide du passionné](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#bluetooth-best-practices) . Après une mise à jour du microprogramme, les contrôleurs redémarrent et se reconnectent au PC hôte (vous remarquerez peut-être que les LED sont brillantes pour le suivi). Si une mise à jour du microprogramme est interrompue (par exemple, si les contrôleurs perdent de l’énergie), elle sera tentée à nouveau lors de la prochaine mise sous tension des contrôleurs.

### <a name="how-i-can-check-battery-level"></a>Comment vérifier le niveau de la batterie ?

Dans la [page d’hébergement de la réalité mixte Windows](navigating-the-windows-mixed-reality-home.md), vous pouvez transformer votre contrôleur pour voir son niveau de batterie du côté opposé du modèle virtuel. Il n’y a pas d’indicateur de niveau de batterie physique.

### <a name="can-you-use-these-controllers-without-a-headset-just-for-the-joysticktriggeretc-input"></a>Pouvez-vous utiliser ces contrôleurs sans casque ? Uniquement pour la manette de jeu/déclencheur/etc.

Pas pour les applications Windows universelles.

## <a name="troubleshooting"></a>Dépannage

Consultez [résolution des problèmes du contrôleur de mouvement](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#motion-controllers) dans le Guide du passionné.

## <a name="filing-motion-controller-feedbackbugs"></a>Profilage de commentaires/bogues du contrôleur de mouvement

[Faites-nous part](give-us-feedback.md) de vos commentaires dans le hub de commentaires à l’aide de la catégorie « > d’entrée de réalité mixte ».

## <a name="see-also"></a>Articles associés
* [Mouvements et contrôleurs de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Mouvements](gaze-and-commit.md#composite-gestures)
* [Entrée MR 213 : contrôleurs de mouvement](mixed-reality-213.md)
* [Guide de passionnés : votre page d’hébergement Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/your-mixed-reality-home)
* [Guide de passionnés : utilisation de jeux & des applications dans Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/using-games-and-apps-in-windows-mixed-reality)
* [Fonctionnement du suivi interne](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/tracking-system)
