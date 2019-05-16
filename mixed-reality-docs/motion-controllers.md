---
title: Contrôleurs de mouvement
description: Plus d’informations sur les contrôleurs de mouvement de réalité mixte.
author: wguyman
ms.author: wguyman
ms.date: 03/21/2018
ms.topic: article
keywords: contrôleurs 6DOF, contrôleurs de mouvement
ms.openlocfilehash: 7db1c16f8243081dc8f53e8722391f102c38e0d3
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629111"
---
# <a name="motion-controllers"></a>Contrôleurs de mouvement

Contrôleurs de mouvement sont [Accessoires matériels](hardware-accessories.md) qui permettent aux utilisateurs de prendre des mesures en réalité mixte. L’avantage de contrôleurs de mouvement sur [mouvements](gestures.md) est que les contrôleurs ont une position précise dans l’espace, ce qui permet une interaction affinée avec des objets numériques. Pour des casques IMMERSIFS Windows Mixed Reality, contrôleurs de mouvement sont le principal moyen que les utilisateurs effectuera action dans leur environnement.

![Contrôleurs de mouvement Windows Mixed Reality](images/winmr-ck-1080x1080-350px.jpg)


## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1er gen)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> Contrôleurs de mouvement</td><td style="text-align: center;"></td><td style="text-align: center;"></td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="hardware-details"></a>Détails sur le matériel

>[!VIDEO https://www.youtube.com/embed/1nlcdDNOdm8]

Contrôleurs de mouvement Windows Mixed Reality offrent précis et réactif suivi du mouvement dans votre champ de vue à l’aide des capteurs dans le casque immersif, ce qui signifie qu’il est inutile d’installer le matériel sur les murs dans votre espace. Ces contrôleurs de mouvement offre la même facilité d’installation et la portabilité comme des casques IMMERSIFS Windows Mixed Reality. Nos partenaires appareil planifier commercialiser et vendre ces contrôleurs de vente au détail rayons ces vacances.

![Familiarisez-vous avec votre contrôleur](images/controllerimage-750px.png)<br>
*Familiarisez-vous avec votre contrôleur*

**fonctionnalités :**
* Suivi optique
* déclencheur
* Bouton de manipulation
* Stick analogique
* Pavé tactile

## <a name="setup"></a>Installation

### <a name="before-you-begin"></a>Avant de commencer

**Vous aurez besoin :**
* Un ensemble de deux contrôleurs de mouvement.
* Quatre piles AA.
* Un PC capable de Bluetooth 4.0.

**Recherchez les mises à jour Windows, Unity et pilote**
* Visitez [installer les outils](install-the-tools.md) pour les versions par défaut de Windows, Unity, etc. pour le développement de réalité mixte.
* Vérifiez que vous avez les plus récentes [casque et le mouvement des pilotes de contrôleur](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/mixed-reality-software).

### <a name="pairing-controllers"></a>Appariement des contrôleurs

Contrôleurs de mouvement peuvent être liés avec l’ordinateur hôte à l’aide des paramètres de Windows comme tout autre appareil Bluetooth.

1. Insérer des piles AA 2 à l’arrière du contrôleur. Laissez le cache de la batterie pour l’instant.
2. Si vous utilisez un adaptateur de Bluetooth USB externe au lieu d’une case d’option Bluetooth intégré, passez en revue la [Bluetooth meilleures pratiques](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#bluetooth-best-practices) avant de continuer. Pour la configuration du bureau intégré radio, vérifiez que l’antenne est connecté.
3. Ouvrez **les paramètres Windows** -> **appareils** -> **Bluetooth ajouter ou tout autre périphérique** -> **Bluetooth** et supprimez toutes les instances précédentes de mouvement « controller » – droite et le mouvement « controller » – gauche. Recherchez également autres appareils dans la catégorie en bas de la liste.
4. Sélectionnez **Bluetooth ajouter ou tout autre périphérique** et qu’elle commence à découvrir des périphériques Bluetooth.
5. Appuyez et maintenez le bouton de Windows du contrôleur pour activer le contrôleur, publiez-la une fois bourdonnements.
6. Maintenez le bouton de jumelage (onglet dans le compartiment de batterie) jusqu'à ce que les voyants commencent à impulsion.
7. Attendez le mouvement « controller » - gauche ou le mouvement « controller » - droite apparaissent au bas de la liste. Sélectionnez cette option pour la paire. Contrôleur sera vibrer qu’une seule fois lors de la connexion.

   ![Sélectionnez le contrôleur de mouvement paire, si plusieurs instances sélectionnez-en un dans qui apparaît en bas de la liste](images/450px-bluetooth-add-a-device-300px.png)<br>
   *Sélectionnez « Contrôleur de mouvement « paire ; s’il existe plusieurs instances, sélectionnez-en un dans le bas de la liste*
   
8. Vous verrez le contrôleur s’affichent dans les paramètres Bluetooth sous **« Avec la souris, clavier et stylet » catégorie** comme **connecté**. À ce stade, vous risquez d’obtenir une mise à jour du microprogramme – consultez [section suivante](motion-controllers.md#updating-controller-firmware).
9. Rattacher le cache de la batterie.
10. Répétez les étapes 1 à 9 pour le second contrôleur.

Après l’appairage avec succès les deux contrôleurs, vos paramètres doivent ressembler à ceci sous **« Avec la souris, clavier et stylet » catégorie** 

   ![Contrôleurs de mouvement connectés](images/450px-motion-controller-connected-300px.png)<br>
   *Contrôleurs de mouvement connectés*

Si les contrôleurs sont désactivés après l’appairage, leur état s’afficheront en tant qu’appariés. Si les contrôleurs de restent définitivement sous « Autres périphériques » catégorie association peut avoir ne été que partiellement effectué et devoir être effectuée de nouveau pour obtenir le contrôleur fonctionnel.

### <a name="updating-controller-firmware"></a>Mise à jour du microprogramme du contrôleur

* Si un casque immersif est connecté à votre PC et nouveau microprogramme du contrôleur est disponible, le microprogramme est adressée à vos contrôleurs de mouvement automatiquement la prochaine fois qu’ils sont activés. Mises à jour du microprogramme de contrôleur sont indiquées par un modèle d’éclairage LED quadrants dans un mouvement circulaire et prennent 1 à 2 minutes.
* Une fois la mise à jour du microprogramme terminée, les contrôleurs redémarre et se reconnecter. Les deux contrôleurs doivent être connectés maintenant. 
    
    ![Contrôleurs connectés](images/cyk-connected-300px.jpg)<br>
    *Contrôleurs connectées dans Paramètres Bluetooth*

* Vérifier votre travail de contrôleurs correctement :
    1. Lancez **Portal de réalité mixte** et entrez votre maison de réalité mixte.
    2. Déplacer vos contrôleurs et vérifier le suivi des modifications, les boutons de test, puis vérifier que [teleportation](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) fonctionne. Si elles ne, Froideur automnale des [la résolution des problèmes de contrôleur de mouvement](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#motion-controllers).

## <a name="gazing-and-pointing"></a>Gazing et en pointant

Réalité mixte Windows prend en charge deux modèles de clé pour l’interaction, **les regards et validez** et **pointez et validez**:
* Avec **les regards et valider**, les utilisateurs ciblent un objet avec leurs [les regards](gaze.md) , puis sélectionnez les objets avec air-drainages de main, un boîtier de commande, un clicker ou de leur voix.
* Avec **pointez et validez**, un utilisateur peut viser un contrôleur de mouvement compatible pointant à l’objet cible, puis sélectionnez les objets avec un déclencheur du contrôleur.

Applications prise en charge de pointe avec des contrôleurs de mouvement doit également activent des interactions pilotées par des regards lorsque cela est possible, pour permettre aux utilisateurs choix dans les périphériques d’entrée qu’ils utilisent.

### <a name="managing-recoil-when-pointing"></a>La gestion de recul lorsque pointe

Lorsque vous utilisez des contrôleurs de mouvement pour pointer et valider, vos utilisateurs utiliseront le contrôleur pour cibler et agir en conséquence en tirant son déclencheur. Les utilisateurs qui partagent le déclencheur vigoureusement peuvent retrouver visant le plus élevé à la fin de leur extraction de déclencheur de contrôleur que qu’ils avaient prévu.

Pour gérer toutes Ce recul peut se produire lorsque les utilisateurs à retirer le déclencheur, votre application peut aligner ses ray ciblage lors de la valeur d’axe analogique du déclencheur s’élève au-dessus 0.0. Vous pouvez ensuite en action à l’aide de ce ciblage ray quelques images ultérieurement une fois que la valeur du déclencheur atteint 1.0, tant que la presse finale se produit dans une fenêtre d’heure courte. Lors de l’utilisation de kits [composite geste d’appui](gestures.md#composite-gestures), Windows gèreront cette ciblant le délai d’attente et de capture de ray pour vous.

## <a name="grip-pose-vs-pointing-pose"></a>Pose de poignée et pose de pointage

Réalité mixte Windows prend en charge les contrôleurs de mouvements dans un large éventail de facteurs de forme, avec la conception de chaque contrôleur qui se différencie par sa relation entre la position des utilisateurs manuellement et naturel « transférer » direction que les applications doit utiliser pour le pointage lors du rendu de la contrôleur.

Pour mieux représenter ces contrôleurs, il existe deux types de risque de poser pour chaque source de l’interaction, vous pouvez passer en revue la **poignée pose** et **pose de pointeur**.

### <a name="grip-pose"></a>Poignée pose

Le **poignée pose** représente l’emplacement de la portée de main détectée par un HoloLens ou palm contenant un contrôleur de mouvement.

Sur des casques IMMERSIFS, la pose de poignée mieux permet de restituer **main de l’utilisateur** ou **détenues par un objet à portée de main de l’utilisateur**, tel qu’un mot de passe ou les électrons. La pose de poignée est également utilisée lors de la visualisation d’un contrôleur de mouvements en tant que le **modèle pouvant être rendue** fourni par Windows pour un mouvement contrôleur utilise la pose de poignée que son origine et le centre de rotation.

La pose de poignée est définie spécifiquement comme suit :
* Le **Attrapez position**: Le centroïde de palm naturellement, tout en maintenant le contrôleur ajustée gauche ou droite pour centrer la position au sein de la poignée. Sur le contrôleur de mouvement Windows Mixed Reality, cette position aligne généralement avec le bouton de compréhension.
* Le **Attrapez axe de droite de l’orientation**: Lorsque vous ouvrez totalement la main pour former une pose plat 5-doigt, le rayon qui est normal pour votre palm (en avant à partir de la gauche palm, vers l’arrière de palm droite)
* Le **Attrapez axe vers l’avant de l’orientation**: Lorsque vous fermez votre main partiellement (comme le cas maintenant le contrôleur), le rayon pointe « forward » via le tube formé par vos doigts non curseur.
* Le **Attrapez orientation d’axe**: L’axe à distance impliqué par les définitions de droite, en avant.

### <a name="pointer-pose"></a>Pose de pointeur

Le **pose de pointeur** représente l’info-bulle du contrôleur qui pointe vers l’avant.

La pose de pointeur fournie par le système qui convient pour raycast lorsque vous êtes **rendu le modèle de contrôleur lui-même**. Si vous restituez un autre objet virtuel à la place le contrôleur, par exemple un électrons virtuel, vous devez faire avec un rayon qui est plus naturel pour cet objet virtuel, comme un rayon qui transite le long de la gaine du modèle électrons définies par l’application. Étant donné que les utilisateurs peuvent voir l’objet virtuel et non du contrôleur physique, en pointant avec l’objet virtuel seront probablement plus naturel pour ceux qui utilisent votre application.

## <a name="controller-tracking-state"></a>État du contrôleur de suivi

Comme les casques, le contrôleur de mouvement de réalité mixte Windows ne requiert aucune configuration de capteurs de suivi externe. Au lieu de cela, les contrôleurs sont suivies par les capteurs dans le casque lui-même.

Si l’utilisateur déplace les contrôleurs de champ de vision du casque, dans la plupart des cas Windows continuera à déduire des positions de contrôleur et les fournir à l’application. Lorsque le contrôleur a perdu visual de suivi pour le temps, les positions du contrôleur supprimera les positions de précision approximative.

À ce stade, le système sera verrouillage de corps le contrôleur à l’utilisateur, suivi de position de l’utilisateur comme ils sont en déplacement, tout en exposant toujours l’orientation true du contrôleur à l’aide de ses capteurs orientation interne. De nombreuses applications qui utilisent des contrôleurs pour pointer vers et activer des éléments d’interface utilisateur peuvent fonctionner normalement en précision approximative sans le remarquer utilisateur.

&nbsp;

>[!VIDEO https://www.youtube.com/embed/rkDpRllbLII]

### <a name="reasoning-about-tracking-state-explicitly"></a>Un peu de suivi de l’état explicitement

Les applications que vous souhaitent traiter les positions différemment en fonction de suivi de l’état peuvent aller plus loin et inspecter les propriétés sur l’état du contrôleur, telles que SourceLossRisk et PositionAccuracy :

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
* **Aucune position :** Alors que le contrôleur peut fonctionner à précision approximative pendant une longue période, parfois le système sache que même une position verrouillée de corps n’est pas significative pour le moment. Par exemple, un contrôleur qui a été activé simplement peut n’ont jamais été observé visuellement, ou un utilisateur peut placer un contrôleur qui est ensuite récupéré par quelqu'un d’autre vers le bas. À l’heure, le système ne fournira pas n’importe quelle position à l’application, et **TryGetPosition** retournera la valeur false.

## <a name="interactions-low-level-spatial-input"></a>Interactions : Entrée spatiale bas niveau

Les interactions principales entre les mains et les contrôleurs de mouvement sont **sélectionnez**, **Menu**, **saisir**, **pavé tactile**,  **Stick analogique**, et **accueil**.
* **Sélectionnez** est l’interaction principale pour activer un hologramme, consistant en un press suivie d’une mise en production. Pour les contrôleurs de mouvement, vous effectuer un cliquer à l’aide de déclencheur du contrôleur. Autres façons d’exécuter une instruction Select sont en parlant la [commande vocale](voice-input.md) « Select ». L’interaction sélectionnez même peut être utilisée dans n’importe quelle application. Considérer sélectionnez comme l’équivalent de la souris cliquez sur une action universelle que vous découvrez qu’une seule fois et que vous appliquerez toutes vos applications.
* **Menu** est l’interaction secondaire permettant d’agir sur un objet utilisé pour extraire un menu contextuel ou exécute une autre action secondaire. Avec les contrôleurs de mouvement, vous pouvez entreprendre une action de menu à l’aide du contrôleur *menu* bouton. (par exemple, le bouton avec l’icône de « menu » hamburger dessus)
* **Saisissez** est comment peuvent directement prendre des mesures sur les objets à leur portée de main pour les manipuler. Avec les contrôleurs de mouvement, faire une action de comprendre en appuyant sur votre première étroitement. Un contrôleur de mouvement peut détecter appréhendé avec un bouton de la manipulation, le déclencheur de palm ou autre capteur.
* **Pavé tactile** permet à l’utilisateur d’ajuster une action en deux dimensions le long de la surface du pavé tactile d’un contrôleur de mouvement, de valider l’action en cliquant sur vers le bas sur le pavé tactile. Pavés tactiles fournissent un état enfoncé, État touché et normalisées coordonnées XY. X et Y une plage comprise entre -1 à 1 entre la plage du pavé tactile circulaire, avec un centre à (0, 0). Pour X, -1 est sur la gauche et 1 se trouve à droite. Pour Y, -1 est sur le bas et 1 est situé en haut.
* **Stick analogique** permet à l’utilisateur d’ajuster une action en deux dimensions en déplaçant le stick analogique d’un contrôleur de mouvement dans sa plage circulaire, valider l’action en cliquant sur vers le bas sur le stick analogique. En outre, sticks analogiques fournissent un état appuyé et normalisée des coordonnées XY. X et Y une plage comprise entre -1 à 1 entre la plage du pavé tactile circulaire, avec un centre à (0, 0). Pour X, -1 est sur la gauche et 1 se trouve à droite. Pour Y, -1 est sur le bas et 1 est situé en haut.
* **Accueil** est une action système spécial qui permet de revenir en arrière dans le Menu Démarrer. Il est similaire à la touche Windows sur un clavier ou le bouton Xbox sur une manette Xbox. Vous pouvez rentrer chez soi en appuyant sur le bouton Windows sur un contrôleur de mouvement. Notez que vous pouvez également toujours revenir à démarrer en disant « Hey Cortana, Go Home ». Les applications ne peut pas réagir spécifiquement pour les actions de base, car celles-ci sont gérées par le système.

## <a name="composite-gestures-high-level-spatial-input"></a>Mouvements composite : Entrée spatiale haut niveau

Les deux [main mouvements](gestures.md) et contrôleurs de mouvement peuvent être suivis au fil du temps pour détecter un ensemble commun de haut niveau  **[mouvements composites](gestures.md#composite-gestures)**. Cela permet à votre application détecter de haut niveau **appuyez sur**, **contenir**, **manipulation** et **navigation** mouvements, si les utilisateurs se retrouvent à l’aide de mains ou les contrôleurs.

## <a name="rendering-the-motion-controller-model"></a>Le modèle de contrôleur de mouvement de rendu

**Modèles 3D contrôleur** Windows rend disponible pour les applications un modèle pouvant être rendue de chaque contrôleur de mouvement actuellement actif dans le système. En demandant à votre application charger dynamiquement et d’expliquer ces modèles de contrôleur fourni par le système lors de l’exécution, vous pouvez garantir votre application les conceptions de compatibilité ascendante pour toute autre contrôleur.

Ces modèles pouvant être rendues doivent tous être rendus au **poignée pose** du contrôleur, comme l’origine du modèle s’aligne sur ce point dans le monde physique. Si vous restituez les modèles de contrôleur, vous pouvez ensuite souhaiter raycast dans votre scène à partir de la **pose de pointeur**, qui représente le rayon le long duquel les utilisateurs se naturellement attendent pointer, étant donné la conception physique de ce contrôleur.

Pour plus d’informations sur la façon de charger les modèles de contrôleur dynamiquement dans Unity, consultez le [rendu le modèle de contrôleur de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md#rendering-the-motion-controller-model-in-unity) section.

**Dessin au trait 2D contrôleur** pendant que nous vous recommandons de joindre des conseils de contrôleur de dans l’application et des commandes pour les modèles dans l’application contrôleur eux-mêmes, certains développeurs voudront à utiliser des représentations sous forme de ligne 2D art des contrôleurs de mouvement dans plat « didacticiel » ou « procédures » INTERFACE UTILISATEUR. Pour les développeurs, nous avons apporté .png mouvement contrôleur ligne art fichiers disponibles dans les deux ci-dessous noir et blanc (clic droit pour enregistrer).

![Aperçu du trait de contrôleurs de mouvement](images/motioncontrollers-black-preview-300px.png)

 [Contrôleurs de mouvement de haute résolution trait dans ''' blanc '''](images/motioncontrollers-white.png)
 
 [Contrôleurs de mouvement de haute résolution trait dans ''' noir '''](images/motioncontrollers-black.png)

## <a name="faq"></a>Forum Aux Questions

### <a name="can-i-pair-motion-controllers-to-multiple-pcs"></a>J’ai paire puis-je de mouvement contrôleurs à plusieurs ordinateurs ?

Contrôleurs de mouvement prend en charge un appariement avec un PC unique. Suivez les instructions [le programme d’installation du contrôleur de mouvement](motion-controllers.md#setup) d’associer vos contrôleurs.

### <a name="how-do-i-update-motion-controller-firmware"></a>Comment mettre à jour le microprogramme du contrôleur de mouvement ?

Microprogramme du contrôleur de mouvement fait partie du pilote casque et est actualisé automatiquement sur la connexion si nécessaire. Mises à jour du microprogramme prennent généralement 1 à 2 minutes en fonction de la qualité de cases d’option et lien Bluetooth. Dans de rares cas, les mises à jour du microprogramme de contrôleur peuvent prendre jusqu'à 10 minutes, ce qui peut indiquer une connectivité Bluetooth médiocre ou des interférences radio. Consultez [Bluetooth de meilleures pratiques dans le Guide de passionnés](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#bluetooth-best-practices) pour résoudre les problèmes de connectivité. Après une mise à jour du microprogramme, contrôleurs redémarre et se reconnecter à l’ordinateur (vous pouvez remarquer les LED accédez clair pour le suivi) hôte. Si une mise à jour du microprogramme est interrompue (par exemple, les contrôleurs de coupure), elle sera tentée à nouveau la prochaine fois que les contrôleurs sont sous tension.

### <a name="how-i-can-check-battery-level"></a>Comment puis-je vérifier le niveau de batterie ?

Dans le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md), vous pouvez activer votre contrôleur pour voir son niveau de batterie sur le côté inverse du modèle virtuel. Il n’existe aucun indicateur de niveau de batterie physique.

### <a name="can-you-use-these-controllers-without-a-headset-just-for-the-joysticktriggeretc-input"></a>Vous pouvez utiliser ces contrôleurs sans un casque ? Uniquement pour l’entrée de la manette de jeu/déclencheur/etc. ?

Pas pour les Applications Windows universelles.

## <a name="troubleshooting"></a>Résolution des problèmes

Consultez [la résolution des problèmes de contrôleur de mouvement](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#motion-controllers) dans le Guide enthousiaste.

## <a name="filing-motion-controller-feedbackbugs"></a>Contrôleur de mouvement dépôt commentaires/bogues

[Envoyez-nous vos commentaires](give-us-feedback.md) dans le Hub de commentaires, à l’aide de la catégorie « Mixed Reality -> entrée ».

## <a name="see-also"></a>Voir aussi
* [Mouvements et contrôleurs de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Mouvements](gestures.md)
* [Réalité mixte - Entrées - Cours 213 : Contrôleurs de mouvement](mixed-reality-213.md)
* [Guide de fans : Votre Windows Mixed Reality domestique](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/your-mixed-reality-home)
* [Guide de fans : À l’aide de jeux et applications en réalité mixte Windows](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/using-games-and-apps-in-windows-mixed-reality)
* [Fonctionne de l’intérieur à la sortie de suivi](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/tracking-system)
