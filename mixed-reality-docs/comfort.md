---
title: Confort
description: Au cours de l’affichage physique, le système visual humain s’appuie sur plusieurs sources d’informations, ou « piles » pour interpréter des formes 3D et la position relative des objets.
author: erickjpaul
ms.author: erpau
ms.date: 02/13/2019
ms.topic: article
keywords: Réalité mixte, conception, confort
ms.openlocfilehash: dbf7080f5b9a2ebafdbd06fca79fae717b3207ed
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597057"
---
# <a name="comfort"></a>Confort

Au cours de l’affichage physique, le système visual humain s’appuie sur plusieurs sources d’informations, ou « piles » pour interpréter des formes 3D et la position relative des objets. Certains signaux s’appuient uniquement sur un œil unique (signaux monoculaires), y compris [perspective linéaire](https://en.wikipedia.org/wiki/Perspective_(graphical)), [taille familier](https://en.wikipedia.org/wiki/Size#Perception_of_size), occlusion, [flou de profondeur de champ](https://en.wikipedia.org/wiki/Depth_of_field), et [ hébergement](https://en.wikipedia.org/wiki/Accommodation_(eye)). Autres signaux s’appuient sur les deux yeux (signaux (jumelles)) et inclure [vergence](https://en.wikipedia.org/wiki/Vergence) (essentiellement les rotations relatifs des yeux nécessaires pour examiner un objet) et [disparité (jumelles)](https://en.wikipedia.org/wiki/Stereopsis) (le modèle de différences entre les projections de la scène à l’arrière des deux yeux). Pour garantir un maximum de confort sur les écrans de lunettes, il est important pour les concepteurs et développeurs de créer et de présenter du contenu d’une manière qui imite le fonctionnement de ces files d’attente dans le monde physique. À partir d’un point de vue physique, il est également important de concevoir le contenu qui ne nécessite pas de mouvements fatigante du cou ou armements. Dans cet article, nous aborderons les points clés à prendre en compte pour atteindre ces objectifs.

## <a name="vergence-accommodation-conflict"></a>Conflit de vergence-hébergement

Pour afficher les objets clairement, doivent êtres humains [prendre en charge](https://en.wikipedia.org/wiki/Accommodation_%28eye%29), ou ajuster le focus à la distance de l’objet des leurs yeux. En même temps, la rotation de deux yeux doit [converger](https://en.wikipedia.org/wiki/Convergence_(eye)) à distance de l’objet pour éviter l’affichage des images double. Dans l’affichage naturelle, vergence et hébergement sont liés. Lorsque vous affichez un élément (par exemple, un housefly proche de votre nez) près de vos yeux croisent et prendre en charge à un point de near. À l’inverse, si vous affichez un élément à l’infini optique (en commençant à peu près au 6m ou éloignez de vision normale), directe des yeux lignes deviennent parallèles et les objectifs des vos yeux s’adapter à l’infini. 

Dans les affichages plus LUNETTES utilisateurs inclura toujours à la distance focale de l’affichage (pour obtenir une image précise), mais convergent vers la distance de l’objet d’intérêt (pour obtenir une image unique). Lorsque les utilisateurs prendre en charge et convergent vers différentes distances, le lien physique entre les deux signaux doit être interrompu, et cela peut entraîner une gêne visual ou fatigue.

<br>

>[!VIDEO https://www.youtube.com/embed/-606oZKLa_s]

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils HOLOGRAPHIQUE

HoloLens affiche est fixés à une distance optique environ 2.0m éloignée de l’utilisateur. Par conséquent, les utilisateurs doivent s’adapter toujours près 2.0m pour maintenir une image claire dans l’appareil. Les développeurs d’applications peuvent guider où les yeux des utilisateurs convergent en plaçant le contenu et hologrammes à des profondeurs différents. Maux de conflit vergence-hébergement peut être évitée ou réduite en conservant le contenu auquel les utilisateurs convergent plus près m 2.0 que possible (par exemple, dans une scène avec un grand nombre de profondeur, placez les zones d’intérêt près m 2.0 à partir de l’utilisateur lorsque cela est possible). Lorsque le contenu ne peut pas être placé près 2.0 m, maux de conflit vergence-hébergement est plus grande lorsque regards de l’utilisateur bascule dans les deux sens entre différentes distances. En d’autres termes, il est beaucoup plus à l’aise examiner un hologramme stationnaire qui reste 50cm qu’aux examiner un hologramme 50cm suite qui déplace les vers et à vous au fil du temps.

![Distance optimale pour placer hologrammes à partir de l’utilisateur.](images/distanceguiderendering-950px.png)<br>
*Distance optimale pour placer hologrammes à partir de l’utilisateur*

#### <a name="best-practices-for-hololens-1st-gen-and-hololens-2"></a>Meilleures pratiques pour HoloLens (1er gen) et 2 de HoloLens

Pour plus de confort maximal, **la zone optimale pour la sélection élective hologramme est comprise entre 1,25 m et 5m**. Dans tous les cas, les concepteurs doivent tenter d’arrière-plan de contenu de structure pour encourager les utilisateurs à interagir 1 million ou plus éloignés du contenu (par exemple, ajuster [taille du contenu et par défaut des paramètres de positionnement](gaze-targeting.md)). 

Bien que le contenu peut parfois besoin d’afficher moins de 1 million, nous vous déconseillons jamais présentant moins de 40cm hologrammes. Par conséquent, nous vous recommandons de commencer à **fondu de contenu à 40cm et placer un plan de découpage de rendu à 30cm** afin d’éviter les plus proches des objets.

Objets déplacement en profondeur sont plus susceptibles que les objets STATIONNAIRES pour produire de gêne en raison du conflit vergence-hébergement. De même, que les utilisateurs doivent rapidement passer de près de focus lointain focus (par exemple, en raison d’un hologramme contextuels nécessitant une interaction directe) risque de fatigue et gêne visual. Par conséquent, **supplémentaire doit veiller à réduire la fréquence à laquelle les utilisateurs sont : affichage de contenu qui se déplacent en profondeur ; ou rapidement ramener le focus entre hologrammes proches**. 

Lors de la conception de contenu pour direct (near) interaction dans 2 HoloLens, ou **dans toutes les applications où le contenu doit être placé à moins de 1m, une attention particulière à entreprendre pour garantir le confort de l’utilisateur**. Les probabilités de gêne en raison du conflit vergence-hébergement augmenter de façon exponentielle avec diminution de distance de visualisation. **Nous vous recommandons de créer un budget « profondeur » pour les applications basées sur la durée pendant laquelle un utilisateur est censé afficher le contenu qui est proche de (< 1m) et le déplacement en profondeur**. Un exemple consiste à éviter de placer l’utilisateur dans ces situations plus de 25 % du temps. Si le budget de profondeur est dépassé, nous vous recommandons d’attention utilisateur de test pour vous assurer qu’il reste une expérience à l’aise.

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersives

Pour les appareils immersives, les instructions et les meilleures pratiques pour HoloLens s’applique toujours, mais les valeurs spécifiques de la Zone de confort sont décalés en fonction de la distance focale de l’affichage. En règle générale, les distances focal à ces écrans sont entre 1,25 à 2,5 millions. En cas de doute, éviter le rendu d’objets d’intérêt trop près aux utilisateurs et à la place d’essaie de garder la majorité du contenu 1m ou éloignés.

## <a name="interpupillary-distance-and-vertical-offset"></a>Distance interpupillary et le décalage vertical

Lorsque l’affichage de contenu numérique sur head monté s’affiche (HMD), la position des yeux d’un utilisateur donné par rapport à la position d’affichage de contenu numérique est critique. Plus précisément, les deux distance interpupillary ([IPD](https://en.wikipedia.org/wiki/Pupillary_distance)) et le décalage vertical (VO) sont importantes pour le confort de visualisation de contenu numérique dans HMDs. 

IPD fait référence à la distance entre les élèves ou les centres, des yeux d’un individu. VO fait référence à potentiel décalage vertical du contenu numérique indiqué pour chaque œil par rapport aux yeux de l’axe horizontal (notamment, cela n’est pas le même décalage horizontal ou disparité (jumelles)). Mal mise en correspondance une ou les deux de ces facteurs à un utilisateur individuel peut aggraver les effets de gêne provoqué par un conflit de vergence-hébergement, mais il peut même cause gêne lorsque des conflits de V-A sont réduite (par exemple, pour le contenu affiché sur le m 2.0 focal distance de la HoloLens). 

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils HOLOGRAPHIQUE

#### <a name="hololens-1st-gen"></a>HoloLens (1er gen)

Pour HoloLens (1er gen), IPD est estimé et au cours de l’appareil [étalonnage](calibration.md). Pour les nouveaux utilisateurs à un déjà définie d’appareil, étalonnage doit être exécuté ou IPD doit être défini manuellement. VO dépend entièrement du périphérique ajuster. Plus précisément, pour réduire VO, l’appareil doit être positionné sur la tête de l’utilisateur telles que les affichages sont au niveau de l’axe de ses yeux. 

#### <a name="hololens-2"></a>HoloLens 2

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersives

HMDs immersives Windows Mixed Reality n’ont aucune étalonnage automatique pour IPD ou VO. IPD peut être défini manuellement dans les logiciels (sous Paramètres du portail de réalité mixte, consultez [étalonnage](calibration.md)), ou certains HMDs ont un curseur de la mécanique qui permet à l’utilisateur d’ajuster l’espacement des lentilles à une position à l’aise (c'est-à-dire, qui à peu près correspond à leur infrastructure ou IPD). 

## <a name="rendering-rates"></a>Taux de rendu

Applications de réalité mixte sont uniques, car les utilisateurs peuvent se déplacer librement dans le monde et interagir avec le contenu virtuel comme comme s’ils étaient des objets réels. Pour maintenir cette impression, il est essentiel pour restituer hologrammes afin qu’ils apparaissent stables dans le monde et animer sans heurts. Rendu à un [minimum de 60 images par seconde (FPS)](understanding-performance-for-mixed-reality.md) vous aide à atteindre cet objectif. Il existe certains appareils de réalité mixte qui prennent en charge le rendu les vitesses supérieurs à 60 i/s et pour ces appareils il est fortement recommandé à restituer aux vitesses plus élevées pour fournir une expérience utilisateur optimale.

**Approfondissez vos connaissances**

Pour dessiner hologrammes ressemble [elles sont stables dans le monde réel ou virtuel](hologram-stability.md), les applications doivent rendre des images à partir de la position de l’utilisateur. Étant donné que le rendu d’image prend de temps, HoloLens et autres appareils Windows Mixed Reality prédire où tête de l’utilisateur lorsque les images sont affichés dans les affichages. Cet algorithme de prédiction est une approximation. Matériel et les algorithmes de Windows Mixed Reality ajuster l’image rendue pour prendre en compte l’écart entre la position de tête prédite et la position réelle principale. Ce processus rend l’image visible par l’utilisateur apparaissent comme si elle était rendue à partir de l’emplacement approprié et hologrammes sentent stables. Les mises à jour fonctionnent le mieux pour les petites modifications dans la position de tête et qu’ils ne peuvent pas complètement représentent des différences de rendu d’image, tels que ceux provoqués par parallax de mouvement.

**Par rendu à une fréquence minimale de 60 i/s, vous effectuez deux opérations permettant de lever hologrammes stables :**
1. En réduisant l’apparence de SEQUENCES, qui se caractérise par motion inégale et images double. Mouvement de hologramme plus rapide et le rendu inférieure tarifs associés à plus prononcé judder. Par conséquent, s’efforçant de toujours maintenir 60 i/s (ou le taux de rendu maximale de votre appareil) permettra d’éviter SEQUENCES de déplacement hologrammes.
2. Pour réduire la latence globale. Dans un moteur avec un thread de jeu et un thread de rendu en cours d’exécution par échelons, en cours d’exécution à 30 i/s peut ajouter des 33.3ms de latence supplémentaire. En réduisant la latence, cela diminue l’erreur de prédiction et augmente la stabilité hologramme.

**Analyse des performances**

Il existe un large éventail d’outils qui peut être utilisé pour évaluer la fréquence d’images de votre application comme :
* GPUView
* Débogueur de Visual Studio Graphics
* Profileurs intégrées à des moteurs 3D telle que le débogueur de Frame dans Unity

## <a name="self-motion-and-user-locomotion"></a>Automatique de mouvement et locomotion de l’utilisateur

La seule limite concerne la taille de votre espace physique ; Si vous souhaitez autoriser les utilisateurs à s’éloigner de l’environnement virtuel qu’ils le feraient dans leurs salles réelles, un formulaire de mouvement purement virtuel doit être implémenté. Toutefois, soutenue mouvement virtuel qui ne correspond pas au mouvement réel, physique de l’utilisateur peut amener souvent maladie de mouvement. Ce résultat est dû à la *signaux visuels* pour automatique de mouvement à partir de la *monde virtuel* en conflit avec le [signaux VESTIBULAIRE](https://en.wikipedia.org/wiki/Vestibular_system) pour automatique de mouvement peuvent provenir les *réels*.

Heureusement, il existe des conseils pour l’implémentation locomotion utilisateur pouvant aider à éviter le problème :
* Toujours placer l’utilisateur dans le contrôle de leurs mouvements ; inattendue de mouvement automatique est particulièrement problématique
* L’homme est très sensibles à la direction de gravité. Par conséquent, les mouvements verticales non initiées par l’utilisateur en particulier doivent être évitées.

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils HOLOGRAPHIQUE

Une méthode pour autoriser l’utilisateur à déplacer vers un autre emplacement dans un environnement virtuel de grande taille consiste à donner l’impression, qu'elles se déplacent un petit objet dans la scène. Cet effet peut être obtenu comme suit :
   1. Fournissent une interface où l’utilisateur peut sélectionner une place dans l’environnement virtuel où elles souhaitent déplacer.
   2. Fonction de sélection, de réduire le rendu de scène à un disque autour de l’endroit souhaité.
   3. Tout en conservant l’endroit sélectionné, autoriser l’utilisateur à déplacer comme s’il s’agissait d’un petit objet. L’utilisateur peut déplacer puis la sélection de près les pieds.
   4. Fonction désélection, reprendre le rendu de la scène entière.

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersives

L’approche d’appareil HOLOGRAPHIQUE précédent ne fonctionne pas aussi dans un appareil immersif, car elle requiert l’application pour restituer un grand void noir ou un autre environnement par défaut lors du déplacement de la « disque ». Ce traitement perturbe de sens d’immersion. Une astuce pour locomotion utilisateur dans un casque immersive est l’approche de « clignotement ». Cette implémentation fournit à l’utilisateur de contrôler leur mouvement et donne une brève impression de mouvement, mais rend donc brève que l’utilisateur est moins susceptible de se sentir disoriented par purement virtuel mouvement automatique :
   1. Fournissent une interface où l’utilisateur peut sélectionner une place dans l’environnement virtuel où elles souhaitent déplacer.
   2. Dès que vous sélectionnez, commencez un mouvement très rapide simulé (100 Mo/s) vers cet emplacement lors de fondu rapidement le rendu.
   3. Fondu le rendu différé dans après avoir terminé la traduction.

## <a name="heads-up-displays"></a>Affiche de tête haute

Dans les dernières premier-TIR, affichages tête haute (HUDs) présentent manière permanente des informations telles que l’état du joueur, mini-maps et inventaires directement sur l’écran. HUDs fonctionnent bien pour maintenir le joueur informé sans y converser sur l’expérience de jeu. Dans les expériences de réalité mixte, HUDs susceptibles d’entraîner une gêne importante et doivent être adaptées au contexte plus riche. Plus précisément, HUDs sont verrouillés de façon rigide à l’orientation de la principal de l’utilisateur sont susceptibles de produire une gêne. Si une application requiert un HUD, nous vous recommandons de *corps* verrouillage plutôt que de verrouillage principal. Ce traitement peut être implémenté en tant qu’ensemble d’affichage qui immédiatement traduire avec l’utilisateur, mais ne sont pas en rotation avec tête de l’utilisateur jusqu'à ce qu’un seuil de rotation est atteint. Une fois cette rotation est atteinte, le HUD peut-être réorienter pour présenter les informations dans le champ de vue utilisateur. Implémentation de rotation de HUD 1:1 et de traduction par rapport à la tête de l’utilisateur les mouvements doivent toujours être évitées.

## <a name="text-legibility"></a>Meilleure lisibilité du texte

Une meilleure lisibilité du texte optimal peut aider à alléger la charge de surveiller et maintenir le confort de l’utilisateur, en particulier dans les applications ou des scénarios qui requièrent des utilisateurs à lire dans un HMD. Une meilleure lisibilité du texte dépend de divers facteurs, notamment diverses propriétés d’affichage (par exemple, une densité de pixels, luminosité, contraste), propriétés de filtre (par exemple, les aberrations chromatique) et propriétés de police du texte / (par exemple, la police spécifique caractéristiques telles qu’épaisseur, empattements, etc., couleur de police, couleur d’arrière-plan).  

En règle générale, nous vous recommandons de tester des applications spécifiques pour une meilleure lisibilité et de rendre les tailles de police aussi grand que possible pour une expérience à l’aise. Ci-dessous, nous proposons des conseils généraux comme point de départ pour le développement. Notez que toutes les tailles de police sont signalés en degrés de [angle visual](https://en.wikipedia.org/wiki/Visual_angle) au lieu de tailles physiques spécifiques, qui fournit des conseils pour n’importe quelle distance dans la zone de sélection élective hologramme optimale, car elle prend en compte la taille de la texte et la distance, il apparaît dans l’Observateur. 

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils HOLOGRAPHIQUE

Pour les appareils HOLOGRAPHIQUE, rendu du texte noir/sombre sur un arrière-plan blanc/light fournit le niveau de contraste plus cohérente, car l’arrière-plan sera occlude interférence provenant du monde réel derrière le rendu. Rendu de texte/light blanc sur fond noir/sombre permet plus de l’environnement réel de transparaître à travers, qui peut-être interférer avec la lisibilité du texte. 

#### <a name="hololens-1st-gen"></a>HoloLens (1er gen)

La taille de police verticale lisibles minimale est environ 0,35 ° et une taille de police verticale à l’aise est au moins environ 0,5 ° pour lire le contenu présenté à une distance de 2m à l’utilisateur. 

#### <a name="hololens-2"></a>HoloLens 2

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersives

Appareils immersives généralement ont un taux de contraste plus élevé en raison de l’occlusion complète de l’environnement extérieur, mais ont une densité de pixels effectif inférieur en partie en raison de l’agrandissement des lentilles devant l’affiche. 

Pour HMDs immersives de Windows Mixed Reality, la taille de police verticale lisibles minimale est environ 0,7-0,9 ° et une taille de police verticale à l’aise est environ 1.0° pour lire le contenu présenté à une distance de 2m à l’utilisateur.

## <a name="gaze-direction"></a>Direction du regard

Pour éviter les yeux et le cou contenu doit être conçu afin que les mouvements yeux et le cou excessive sont évités.
* **Éviter** regards angles de plus de 10 degrés au-dessus de l’horizon (déplacement vertical)
* **Éviter** regards angles de plus de 60 degrés ci-dessous l’horizon (déplacement vertical)
* **Éviter** rotations cou plus de 45 degrés excentré (déplacement horizontal)

L’angle du pointage de regard (repos) optimal est considéré comme entre les degrés de 10 à 20 ci-dessous à l’horizontale, comme la tête a tendance à pivoter vers le bas légèrement, en particulier au cours des activités.

![Champ de vision autorisée (angle d’ouverture) tel que déterminé par la plage du goulot du mouvement](images/optimal-field-of-view-2-750px.png)<br>
*Champ de vision autorisée (angle d’ouverture) tel que déterminé par la plage du goulot du mouvement*

## <a name="arm-positions"></a>Positions ARM

Fatigue de muscle peut s’accumuler lorsque les utilisateurs sont censées conserver une main déclenchée pendant toute la durée d’une expérience. Il peut également être fatiguing pour obliger l’utilisateur à plusieurs reprises apporter air appuyez sur les mouvements sur de longues périodes. Nous recommandons donc d’expériences évitent exigeant une saisie de mouvement de constante, répétées. Cet objectif peut être obtenu en incorporant des pauses ou offre un mélange de gestes et paroles d’entrée pour interagir avec l’application.

## <a name="see-also"></a>Voir aussi
* [Gaze](gaze.md)
* [Stabilité HOLOGRAMME](hologram-stability.md)
* [Notions fondamentales d’interaction](interaction-fundamentals.md)
* [Frame HOLOGRAPHIQUE](holographic-frame.md)
* [Calibration](calibration.md)
