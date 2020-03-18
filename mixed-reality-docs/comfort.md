---
title: Confort
description: Dans le processus de vision naturelle, le système visuel humain s’appuie sur plusieurs sources d’informations, ou « signaux », pour interpréter les formes 3D et la position relative des objets.
author: erickjpaul
ms.author: erpau
ms.date: 04/5/2019
ms.topic: article
ms.localizationpriority: high
keywords: Réalité mixte, conception, confort, HoloLens 2, HoloLens (1ère génération)
ms.openlocfilehash: 178044ce8c76de75b7cce5e10664ce65d108f0f8
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79376066"
---
# <a name="comfort"></a>Confort

Dans le processus de vision naturelle, le système visuel humain s’appuie sur plusieurs sources d’informations, ou « signaux », pour interpréter les formes 3D et la position relative des objets. Certains signaux ne reposent que sur un œil (signaux monoculaires). C’est le cas de la [perspective linéaire](https://en.wikipedia.org/wiki/Perspective_(graphical)), de la [taille familière](https://en.wikipedia.org/wiki/Size#Perception_of_size), de l’occlusion, du [flou de profondeur de champ](https://en.wikipedia.org/wiki/Depth_of_field) et de l’[accommodation](https://en.wikipedia.org/wiki/Accommodation_(eye)). D’autres signaux reposent sur les deux yeux (signaux binoculaires). Il s’agit notamment de la [vergence](https://en.wikipedia.org/wiki/Vergence) (rotations oculaires relatives qui sont nécessaires pour regarder un objet) et de la [disparité binoculaire](https://en.wikipedia.org/wiki/Stereopsis) (différences entre les projections de la scène sur la rétine de chaque œil). Pour garantir un confort maximal sur les afficheurs placés sur la tête, il est important que les concepteurs et les développeurs créent du contenu et le présentent d’une manière qui imite le fonctionnement de ces indicateurs dans le monde naturel. D’un point de vue physique, il est également important de concevoir du contenu qui ne nécessite pas de mouvements fatigants du cou ou des bras. Dans cet article, nous allons voir comment atteindre ces objectifs.

## <a name="vergence-accommodation-conflict"></a>Conflit entre la vergence et l’accommodation

Pour voir clairement les objets, l’homme doit procéder à une [accommodation](https://en.wikipedia.org/wiki/Accommodation_%28eye%29), c’est-à-dire qu’il doit ajuster son focus par rapport à la distance de l’objet. En même temps, la rotation des deux yeux doit [converger](https://en.wikipedia.org/wiki/Convergence_(eye)) au niveau de l’objet afin d’éviter de voir double. Dans le processus de vision naturelle, la vergence et l’accommodation sont liées. Lorsque vous regardez un objet de près (par exemple, une mouche sur votre nez), vos yeux se croisent et s’accommodent sur un point proche. Inversement, si vous regardez un objet avec une optique infinie (à partir de 6 mètres pour une vision normale), vos lignes de regard deviennent parallèles et votre cristallin s’accommode à l’infini. 

Avec la plupart des casques audiovisuels, les utilisateurs ajustent (accommodent) toujours leur vision à la distance focale de l’écran (pour obtenir une image nette), mais ils convergent au niveau de l’objet qui les intéresse (pour obtenir une seule image). Lorsque l’accommodation et la convergence se font à des distances différentes, la liaison naturelle entre ces deux signaux doit être brisée, ce qui peut entraîner une gêne visuelle ou une fatigue.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/-606oZKLa_s" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils holographiques

L’affichage des casques HoloLens est configuré sur une distance optique d’environ 2 mètres de l’utilisateur. Par conséquent, les utilisateurs doivent toujours ajuster leur vision sur environ 2 mètres pour avoir une image nette. Les développeurs d’applications peuvent guider l’endroit de convergence des yeux en plaçant du contenu et des hologrammes à différents niveaux de profondeur. La gêne due au conflit vergence-accommodation peut être évitée ou réduite en gardant le contenu sur lequel les yeux convergent à une distance la plus proche possible de 2 mètres (par exemple, dans une scène avec une grande profondeur, placez les zones d’intérêt à une distance de 2 mètres de l’utilisateur si possible). Lorsque le contenu ne peut pas être placé à une distance proche de 2 mètres, le conflit vergence-accommodation est accentué lorsque le regard de l’utilisateur passe à un objet situé à une distance différente. En d’autres termes, il est bien plus confortable de regarder un hologramme stationnaire situé à 50 cm que de regarder un hologramme situé à 50 cm qui passe son temps à se rapprocher et à s’éloigner de vous.

![Distance optimale pour le placement des hologrammes par rapport à l’utilisateur](images/distanceguiderendering-950px.png)<br>
*Distance optimale pour le placement des hologrammes par rapport à l’utilisateur*

### <a name="best-practices-for-hololens-1st-gen-and-hololens-2"></a>Bonnes pratiques pour HoloLens (1re génération) et HoloLens 2

Pour un confort optimal, **l’hologramme doit être placé à une distance comprise entre 1,25 m et 5 m**. Dans tous les cas, les concepteurs doivent tenter de structurer les scènes de contenu en vue d’encourager les utilisateurs à interagir à 1 m ou plus du contenu (par exemple, en ajustant les [paramètres de taille du contenu et de positionnement par défaut](gaze-and-commit.md)). 

Même si le contenu doit parfois être affiché à une distance inférieure à 1 m, nous vous déconseillons de présenter les hologrammes à une distance inférieure à 40 cm. Par conséquent, nous vous recommandons de commencer à **faire disparaître le contenu situé à 40 cm et à placer un plan de découpage du rendu à 30 cm** pour éviter que des objets ne soient plus proches.

Les objets qui changent de profondeur sont plus susceptibles d’entraîner une gêne que les objets stationnaires, en raison du conflit vergence-accommodation. De même, le fait de demander aux utilisateurs de changer rapidement de focus (par exemple, en raison d’un hologramme qui nécessite une interaction directe) peut provoquer une gêne visuelle et une fatigue. Par conséquent, **il est important de réduire la fréquence à laquelle les utilisateurs voient du contenu qui change de profondeur ou à laquelle ils doivent changer rapidement de focus entre un hologramme proche et un hologramme éloigné**. 

### <a name="additional-considerations-for-hololens-2-and-near-interaction-distances"></a>Autres considérations sur HoloLens 2 et les distances d’interaction proches

Lorsque vous concevez du contenu pour une interaction directe (proche) dans HoloLens 2, ou **dans des applications où le contenu doit être placé à une distance inférieure à 1 mètre, il est important de garantir le confort visuel de l’utilisateur**. Les risques de gêne dus au conflit vergence-accommodation augmentent de façon exponentielle lorsque la distance d’affichage diminue. De plus, l’utilisateur peut constater que l’image devient plus floue à mesure que le contenu avec lequel il interagit se rapproche. Il est donc recommandé de tester l’affichage du contenu dans la zone de positionnement optimal des hologrammes, mais également à une distance plus proche (inférieure à 1 mètre du plan de découpage) afin de garantir un affichage net et confortable. 

**Nous vous recommandons de créer un « budget profondeur » pour les applications, dans lequel vous évaluerez le nombre de fois qu’un utilisateur doit s’attendre à voir du contenu proche (à une distance inférieure à 1 mètre) et à voir des changements de profondeur**. Par exemple, vous pouvez limiter ces situations à 25 % du temps. Si le budget profondeur est dépassé, nous vous recommandons de procéder à de nombreux tests utilisateur pour garantir une utilisation confortable. 

En général, nous recommandons également de procéder à de nombreux tests pour garantir que les demandes d’interaction (rapidité de mouvement, accessibilité, etc.) restent confortables pour les utilisateurs à des distances d’interaction plus proches. 


### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersifs

Les instructions et les bonnes pratiques relatives à HoloLens s’appliquent également aux appareils immersifs. Toutefois, les valeurs de la zone de confort changent en fonction de la distance focale de l’écran. En général, les distances focales de ces écrans sont comprises entre 1,25 m et 2,5 m. En cas de doute, évitez d’afficher les objets d’intérêt trop près de l’utilisateur et essayez plutôt de conserver une distance minimale de 1 mètre.

## <a name="interpupillary-distance-and-vertical-offset"></a>Écart pupillaire et décalage vertical

Lorsque vous affichez du contenu numérique sur des casques audiovisuels, la position des yeux de l’utilisateur par rapport à la position d’affichage du contenu numérique est essentielle. Plus précisément, l’écart pupillaire ([IPD](https://en.wikipedia.org/wiki/Pupillary_distance)) et le décalage vertical (VO) sont importants pour garantir un confort de lecture du contenu numérique sur les casques audiovisuels. 

L’écart pupillaire fait référence à la distance qui sépare les deux pupilles, c’est-à-dire le centre des yeux de l’utilisateur. Le décalage vertical fait référence au décalage vertical potentiel du contenu numérique qui est présenté à chaque œil par rapport à l’axe horizontal des yeux de l’utilisateur (important : ce n’est pas la même chose que le décalage horizontal ou que la disparité binoculaire). Si l’un de ces facteurs, voire les deux, ne sont pas respectés, cela peut augmenter la gêne causée par le conflit vergence-accommodation, même après réduction de celui-ci (par exemple, en affichant du contenu à une distance focale de 2 mètres du casque HoloLens). 

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils holographiques

#### <a name="hololens-1st-gen"></a>HoloLens (1ère génération)

Pour HoloLens (1ère génération), l’écart pupillaire est estimé et défini lors de l’[étalonnage](calibration.md) de l’appareil. Les nouveaux utilisateurs qui disposent d’un appareil déjà configuré doivent effectuer l’étalonnage ou définir manuellement l’écart pupillaire. Le décalage vertical dépend entièrement de la manière dont l’appareil est ajusté. En effet, pour réduire la valeur du décalage vertical, l’utilisateur doit placer le casque sur sa tête de telle sorte que l’écran soit au niveau de l’axe de ses yeux. 

#### <a name="hololens-2"></a>HoloLens 2

Pour HoloLens 2, l’écart pupillaire est estimé et défini au cours de l’[étalonnage](calibration.md) du regard ou de l’appareil. Les nouveaux utilisateurs qui disposent d’un appareil déjà configuré doivent effectuer l’étalonnage ou vérifier que l’écart pupillaire est correctement défini. Le décalage vertical est pris en compte automatiquement dans HoloLens 2. 

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersifs

Les casques audiovisuels immersifs Windows Mixed Reality ne permettent pas d’étalonner automatiquement l’écart pupillaire et le décalage vertical. L’écart pupillaire peut être défini manuellement dans le logiciel (dans les paramètres du portail de réalité mixte, sous [Étalonnage](calibration.md)). Certains casques audiovisuels comprennent un curseur mécanique qui permet à l’utilisateur d’ajuster l’espacement des verres sur une position confortable (c’est-à-dire qui correspond approximativement à son écart pupillaire). 

## <a name="rendering-rates"></a>Fréquences d’images

Les applications de réalité mixte sont uniques, dans le sens où les utilisateurs peuvent se déplacer librement dans le monde réel tout en interagissant avec du contenu virtuel, comme s’ils s’agissait d’objets réels. Pour maintenir cette impression, il est essentiel d’afficher les hologrammes pour qu’ils paraissent stables dans le monde réel et s’animent progressivement. Un rendu avec un [minimum de 60 images par seconde (FPS)](understanding-performance-for-mixed-reality.md) permet d’atteindre cet objectif. Certains appareils de réalité mixte prennent en charge le rendu à des fréquences d’images de plus de 60 FPS. Pour ces appareils, il est vivement recommandé d’augmenter la fréquence d’images afin d’offrir une expérience utilisateur optimale.

**Pour aller plus loin**

Pour créer des hologrammes qui paraissent [stables aussi bien dans le monde réel que dans le monde virtuel](hologram-stability.md), les applications doivent afficher les images en se basant sur la position de l’utilisateur. Étant donné que le rendu d’images prend du temps, HoloLens et les autres appareils Windows Mixed Reality doivent prédire à quel endroit sera la tête de l’utilisateur lorsque les images seront affichées sur l’écran. Cet algorithme de prédiction permet d’obtenir une approximation. Les algorithmes et le matériel Windows Mixed Reality ajustent l’image affichée en tenant compte de l’écart entre la position prédite de la tête et sa position réelle. Avec ce processus, l’image que voit l’utilisateur paraît s’afficher au bon endroit et les hologrammes semblent stables. Les mises à jour fonctionnent mieux pour les légers changements de position de la tête et elles ne peuvent pas entièrement tenir compte des différences entre les images affichées, comme celles provoquées par la parallaxe de mouvement.

**En utilisant un rendu d’une fréquence d’images minimale de 60 FPS, vous effectuez deux opérations qui permettent de stabiliser les hologrammes :**
1. Vous réduisez l’impression de vibration, qui se caractérise par des mouvements irréguliers et des images dédoublées. Les mouvements rapides des hologrammes et les fréquences d’images peu élevées provoquent une impression de vibration plus prononcée. Par conséquent, en gardant une fréquence d’images de 60 FPS (ou la fréquence d’images maximale de votre appareil), vous pouvez éviter l’impression de vibration qui est associée au mouvement des hologrammes.
2. Vous réduisez la latence globale. Dans un moteur où sont exécutés conjointement un thread de jeu et un thread de rendu, l’utilisation d’une fréquence d’images de 30 IPS peut ajouter une latence supplémentaire de 33,3 ms. En réduisant la latence, vous diminuez le risque d’erreur de prédiction et vous augmentez la stabilité des hologrammes.

**Analyse des performances**

Il existe un large éventail d’outils qui peuvent être utilisés pour évaluer la fréquence d’images de votre application. En voici quelques exemples :
* GPUView
* Le débogueur de graphiques Visual Studio
* Les profileurs intégrés aux moteurs 3D, tels que Frame Debugger dans Unity

## <a name="self-motion-and-user-locomotion"></a>Mouvement propre et locomotion utilisateur

La seule limitation est liée à la taille de votre espace physique. Si vous souhaitez permettre aux utilisateurs d’aller plus loin dans l’environnement virtuel qu’ils ne le peuvent dans l’espace physique où ils se trouvent, vous devez implémenter une forme de mouvement purement virtuel. Toutefois, un mouvement virtuel prolongé qui ne correspond pas au mouvement physique réel de l’utilisateur peut parfois provoquer des vertiges et des nausées. Ceci est dû au fait que les *signaux visuels* obtenus par les mouvements propres effectués dans le *monde virtuel* sont en conflit avec les [signaux vestibulaires](https://en.wikipedia.org/wiki/Vestibular_system) obtenus par les mouvements propres effectués dans le *monde réel*.

Heureusement, il existe des astuces d’implémentation de la locomotion utilisateur qui permettent d’éviter ce problème :
* Permettez toujours à l’utilisateur de contrôler ses mouvements. Les mouvements propres inattendus sont particulièrement problématiques.
* Les êtres humains sont très sensibles au sens de la gravité. Par conséquent, il faut éviter les mouvements verticaux dont l’utilisateur n’est pas à l’initiative.

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils holographiques

L’une des méthodes possibles pour permettre à l’utilisateur de se déplacer dans un grand environnement virtuel consiste à lui donner l’impression qu’il déplace un petit objet dans la scène. Cet effet peut être obtenu de la façon suivante :
   1. Fournissez une interface dans laquelle l’utilisateur peut sélectionner un endroit de l’environnement virtuel vers lequel il souhaite se déplacer.
   2. Une fois la sélection effectuée, réduisez le rendu de la scène à un disque entourant l’endroit souhaité.
   3. Tout en maintenant la sélection de l’endroit, permettez à l’utilisateur de le déplacer comme s’il s’agissait d’un petit objet. L’utilisateur peut alors déplacer la sélection à proximité de ses pieds.
   4. Lorsque vous désélectionnez l’endroit, vous revenez au rendu intégral de la scène.

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersifs

La méthode précédente qui s’applique aux appareils holographiques ne fonctionne pas très bien sur les appareils immersifs, car elle nécessite que l’application affiche un grand écran noir ou un autre environnement par défaut lors du déplacement du disque de sélection. De cette façon, l’utilisateur perd la sensation d’immersion. Pour la locomotion utilisateur avec un casque immersif, il existe une astuce appelée la méthode « blink ». Cette implémentation permet à l’utilisateur de contrôler ses mouvements et donne une brève impression de mouvement. Cependant, cette impression est si brève que l’utilisateur est moins susceptible d’être désorienté par ses mouvements propres purement virtuels :
   1. Fournissez une interface dans laquelle l’utilisateur peut sélectionner un endroit de l’environnement virtuel vers lequel il souhaite se déplacer.
   2. Lors de la sélection, commencez par simuler un mouvement très rapide (100 m/s) vers cet endroit tout en faisant disparaître rapidement le rendu.
   3. Une fois la translation terminée, affichez de nouveau le rendu.

## <a name="heads-up-displays"></a>Affichage tête haute

Dans les jeux vidéos de tir à la première personne, l’affichage tête haute présente des informations persistantes, telles que la santé du joueur, des mini-cartes ou des inventaires, directement sur l’écran. L’affichage tête haute permet de tenir le joueur informé sans perturber le jeu. Dans les expériences de réalité mixte, l’affichage tête haute peut provoquer une gêne importante et doit être adapté aux contextes les plus immersifs. Plus particulièrement, les affichages tête haute qui sont verrouillés sur l’orientation de la tête de l’utilisateur sont susceptibles d’entraîner une gêne. Si une application nécessite un affichage tête haute, nous vous recommandons de choisir un verrouillage du *corps* plutôt qu’un verrouillage de la tête. Ceci peut être implémenté sous la forme d’un ensemble d’affichages immédiatement translatés pour l’utilisateur, mais qui ne pivoteront pas avec la tête de l’utilisateur tant qu’un certain seuil de rotation n’aura pas été atteint. Une fois la rotation effectuée, l’affichage tête haute peut se réorienter pour présenter les informations dans le champ visuel de l’utilisateur. L’implémentation « 1:1 » de la rotation et de la translation de l’affichage tête haute pour les mouvements de tête de l’utilisateur est à éviter absolument.

## <a name="text-legibility"></a>Lisibilité du texte

Une lisibilité optimale du texte peut réduire la fatigue oculaire et assurer le confort visuel des utilisateurs, en particulier dans les applications ou les scénarios qui obligent les utilisateurs à lire dans un casque audiovisuel. La lisibilité du texte dépend de divers facteurs, notamment des propriétés d’affichage (par exemple, la densité de pixels, la luminosité, le contraste), des propriétés des verres (aberration chromatique, etc.), ainsi que des propriétés du texte et de la police (par exemple, les caractéristiques de police telles que l’épaisseur, l’espacement des caractères, les sérifs, la couleur de la police, la couleur de l’arrière-plan, etc.).  

En général, nous vous recommandons de tester la lisibilité sur certaines applications et d’agrandir autant que possible les tailles de police pour un confort visuel maximal. Vous trouverez ci-dessous des recommandations générales qui vous serviront de point de départ pour le développement. Notez que toutes les tailles de police sont indiquées comme des degrés d’[angle visuel](https://en.wikipedia.org/wiki/Visual_angle) plutôt que comme des tailles physiques. Cela fournit des indications de distance au sein de la zone de positionnement optimal des hologrammes, car cela tient compte à la fois de la taille du texte et de la distance à laquelle il s’affiche pour l’utilisateur. 

Pour obtenir des instructions plus détaillées, consultez [Typographie](typography.md) et [Texte dans Unity](text-in-unity.md).

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils holographiques

Pour les appareils holographiques, l’affichage de texte noir/foncé sur un arrière-plan blanc/clair fournit le rapport de contraste le plus cohérent, car l’arrière-plan va occulter les interférences du monde réel à l’arrière de l’affichage. L’affichage de texte blanc/clair sur un arrière-plan noir/foncé permet davantage à l’environnement réel de transparaître, ce qui peut interférer avec la lisibilité du texte. 

#### <a name="hololens-1st-gen"></a>HoloLens (1ère génération)

La taille de police minimale pour la lisibilité (mesurée de la ligne de base au jambage ascendant) est d’environ 0,35 °, et une taille de police confortable doit être d’au moins 0,5 ° pour permettre la lecture d’un contenu présenté à une distance de 2 mètres de l’utilisateur. 

#### <a name="hololens-2"></a>HoloLens 2

La taille de police minimale pour la lisibilité (mesurée de la ligne de base au jambage ascendant) doit être au moins égale à environ : 
   - 0,4 °-0,5 ° à 45 cm (distance de manipulation directe) 
   - 0,35 °-0,4 ° à 2 mètres
   
La taille de police confortable pour la lisibilité (mesurée de la ligne de base au jambage ascendant) doit être au moins égale à environ : 
   - 0,65 °-0,8 ° à 45 cm (distance de manipulation directe)
   - 0,6 °-0,75 ° à 2 mètres

Notez que les tailles de police doivent être légèrement supérieures pour le texte présenté à des distances de manipulation directe en raison du conflit vergence-accommodation décrit plus haut (les yeux de l’utilisateur s’accommodent à une distance de 2 mètres sur l’écran HoloLens, ce qui fait que le contenu affiché à 45 cm, par exemple, peut paraître plus flou). 

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersifs

Les appareils immersifs présentent généralement des taux de contraste plus élevés en raison de l’occlusion complète de l’environnement extérieur. Toutefois, ils peuvent avoir une densité plus faible de pixels effectifs, en raison notamment de l’effet de loupe des verres placés devant l’écran. 

Pour les casques audiovisuels immersifs Windows Mixed Reality, la taille de police verticale minimale pour la lisibilité (mesurée de la ligne de base au jambage ascendant) est d’environ 0,7-0,9 °, et une taille de police confortable doit être d’au moins 1 ° pour permettre la lecture d’un contenu présenté à une distance de 2 mètres de l’utilisateur.

## <a name="gaze-direction"></a>Direction du regard

Pour éviter la fatigue oculaire et les douleurs cervicales, le contenu doit être conçu de manière à éviter de trop nombreux mouvements des yeux et du cou.
* **Évitez** les angles de regard de plus de 10 degrés au-dessus de l’horizon (mouvement vertical)
* **Évitez** les angles de regard de plus de 60 degrés en dessous de l’horizon (mouvement vertical)
* **Évitez** les rotations du cou de plus de 45 degrés par rapport au centre (mouvement horizontal)

L’angle de regard optimal (de repos) est situé entre 10 et 20 degrés en dessous de l’horizon, car la tête tend à pencher légèrement vers le bas, en particulier pendant les activités.

![Champ de vision possible, tel que déterminé par l’amplitude de mouvement du cou](images/optimal-field-of-view-2.png)<br>
*Champ de vision possible, tel que déterminé par l’amplitude de mouvement du cou*

## <a name="arm-positions"></a>Positions des bras

Une fatigue musculaire peut s’installer si les utilisateurs sont censés garder une main levée pendant toute la durée de l’expérience. Les clics aériens répétés peuvent également se révéler fatigants s’ils doivent être effectués sur une longue période. Nous vous recommandons donc d’éviter les expériences qui exigent des gestes répétés ou maintenus. Pour cela, vous pouvez intégrer de courtes pauses ou proposer une combinaison de saisies gestuelles et vocales pour interagir avec l’application.

## <a name="see-also"></a>Voir aussi
* [Pointage du regard](gaze-and-commit.md)
* [Stabilité des hologrammes](hologram-stability.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Image holographique](holographic-frame.md)
* [Étalonnage](calibration.md)
