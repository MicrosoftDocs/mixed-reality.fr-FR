---
title: Optimal
description: Pendant l’affichage naturel, le système visuel humain s’appuie sur plusieurs sources d’informations, ou «signaux», pour interpréter les formes 3D et la position relative des objets.
author: erickjpaul
ms.author: erpau
ms.date: 04/5/2019
ms.topic: article
keywords: Réalité mixte, conception, confort, HoloLens 2, HoloLens (1ère génération)
ms.openlocfilehash: e3a78e9a990d207b19b287e1897897a5d6dee3ca
ms.sourcegitcommit: 150d258a23130026c8792da383a3993657841fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/12/2019
ms.locfileid: "67024444"
---
# <a name="comfort"></a>Optimal

Pendant l’affichage naturel, le système visuel humain s’appuie sur plusieurs sources d’informations, ou «signaux», pour interpréter les formes 3D et les positions relatives des objets. Certaines signaux reposent uniquement sur un seul oeil (signaux monoculaires), y compris une [perspective linéaire](https://en.wikipedia.org/wiki/Perspective_(graphical)), une [taille familière](https://en.wikipedia.org/wiki/Size#Perception_of_size), une occlusion, [un flou de profondeur de champ](https://en.wikipedia.org/wiki/Depth_of_field)et un [logement](https://en.wikipedia.org/wiki/Accommodation_(eye)). Les autres signaux reposent sur les deux yeux (indications binoculaires) et incluent les [vergence](https://en.wikipedia.org/wiki/Vergence) (essentiellement les rotations relatives des yeux nécessaires à l’examen d’un objet) et la [disparité binoculaire](https://en.wikipedia.org/wiki/Stereopsis) (le modèle de différences entre les projections de la scène sur le arrière des deux yeux). Pour garantir un confort maximal sur les affichages montés en tête, il est important pour les concepteurs et les développeurs de créer et présenter du contenu d’une manière qui imite la manière dont ces signaux fonctionnent dans le monde naturel. D’un point de vue physique, il est également important de concevoir du contenu qui ne nécessite pas de mouvements fatiguing du cou ou des bras. Dans cet article, nous allons examiner les points clés à prendre en compte pour atteindre ces objectifs.

## <a name="vergence-accommodation-conflict"></a>Vergence-conflit d’hébergement

Pour afficher les objets clairement, l’homme doit [prendre en charge](https://en.wikipedia.org/wiki/Accommodation_%28eye%29)ou ajuster son focus à la distance de l’objet. En même temps, la rotation des deux yeux doit [converger](https://en.wikipedia.org/wiki/Convergence_(eye)) vers la distance de l’objet pour éviter de voir les images en double. En vue naturelle, vergence et hébergement sont liés. Lorsque vous affichez un peu près (par exemple, un housefly proche de votre nez), vos yeux se croisent et s’adaptent à un point proche. Inversement, si vous affichez des éléments à l’infini optique (à partir de 6 m ou plus pour une vision normale), les lignes de visibilité de vos yeux deviennent parallèles et vos objectifs s’adaptent à l’infini. 

Dans la plupart des affichages montés en tête, les utilisateurs s’appuient toujours sur la distance focale de l’écran (pour obtenir une image nette), mais convergent sur la distance de l’objet qui vous intéresse (pour obtenir une image unique). Lorsque les utilisateurs s’accommodent de différentes distances, le lien naturel entre les deux signaux doit être cassé et cela peut entraîner une gêne visuelle ou une fatigue.

<br>

>[!VIDEO https://www.youtube.com/embed/-606oZKLa_s]

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils holographiques

Les affichages HoloLens sont fixés à une distance optique d’environ 2,0 mètres de l’utilisateur. Ainsi, les utilisateurs doivent toujours prendre en charge près de 2.0 m pour maintenir une image claire dans l’appareil. Les développeurs d’applications peuvent guider les yeux des utilisateurs en plaçant le contenu et les hologrammes à différents niveaux. La gêne du conflit vergence-hébergement peut être évitée ou réduite en conservant le contenu sur lequel les utilisateurs convergent le plus près de 2.0 m (par exemple, dans une scène avec beaucoup de profondeur, placez les zones d’intérêt près de 2.0 m de l’utilisateur si possible). Lorsque le contenu ne peut pas être placé près de 2.0 m, le conflit entre les logements vergence est plus grand lorsque le point d’arrêt de l’utilisateur passe d’une distance à l’autre. En d’autres termes, il est bien plus facile de regarder un hologramme stationnaire qui reste 50cm que d’examiner un hologramme 50cm qui se déplace vers et à partir de vous dans le temps.

![Distance optimale pour le placement des hologrammes de l’utilisateur.](images/distanceguiderendering-950px.png)<br>
*Distance optimale pour le placement des hologrammes de l’utilisateur*

### <a name="best-practices-for-hololens-1st-gen-and-hololens-2"></a>Meilleures pratiques pour HoloLens (1re génération) et HoloLens 2

Pour un maximum de confort, **la zone optimale pour le placement de l’hologramme est comprise entre 1,25 m et 5m**. Dans tous les cas, les concepteurs doivent tenter de structurer le contenu pour encourager les utilisateurs à interagir 1m ou plus loin du contenu (par exemple, ajuster la [taille du contenu et les paramètres de positionnement par défaut](gaze-targeting.md)). 

Bien que le contenu doive parfois être affiché plus près de 1m, nous vous recommandons de ne jamais présenter des hologrammes plus proches que les 40cm. Par conséquent, nous vous recommandons de commencer à faire **disparaître le contenu sur 40cm et de placer un plan de découpage de rendu sur 30cm** pour éviter tout objet plus proche.

Les objets qui se déplacent en profondeur sont plus susceptibles d’avoir des objets stationnaires pour produire une gêne en raison du conflit vergence-hébergement. De même, le fait de demander aux utilisateurs de basculer rapidement entre le focus vers le bas et le focus (par exemple, en raison d’un hologramme contextuel nécessitant une interaction directe) peut provoquer une gêne visuelle et une fatigue. Par conséquent, **une attention particulière doit être prise pour réduire la fréquence d’utilisation des utilisateurs: afficher le contenu qui se déplace en profondeur, ou basculer rapidement le focus entre des hologrammes proches et éloignés**. 

### <a name="additional-considerations-for-hololens-2-and-near-interaction-distances"></a>Considérations supplémentaires concernant les distances HoloLens 2 et near interaction

Lors de la conception de contenu pour une interaction directe (proche) dans HoloLens 2, ou **dans toute application où le contenu doit être placé plus près de 1m, une attention supplémentaire doit être prise pour garantir le confort de l’utilisateur**. Les risques de gêne dus au conflit d’hébergement vergence augmentent de façon exponentielle avec une distance d’affichage décroissante. En outre, les utilisateurs peuvent être confrontés à une augmentation des bluriness lors de l’affichage du contenu à proximité des distances. nous vous recommandons donc de tester le contenu rendu à la fois dans la zone de positionnement optimal des hologrammes et plus près (moins de 1,0 m vers le plan de découpage) vers Assurez-vous qu’il reste clair et agréable à consulter. 

**Nous vous recommandons de créer un «budget détaillé» pour les applications en fonction de la durée pendant laquelle un utilisateur est censé afficher le contenu proche de (moins de 1,0 m) et de se déplacer en profondeur**. Un exemple consiste à éviter de placer l’utilisateur dans ces situations plus de 25% du temps. Si le budget détaillé est dépassé, nous vous recommandons de tester minutieusement les utilisateurs pour s’assurer qu’il reste une expérience confortable. 

En général, nous recommandons également un test minutieux pour garantir que les exigences d’interaction (par exemple, la vélocité du mouvement, l’accessibilité, etc.) à proximité des distances restent confortables pour les utilisateurs. 


### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersifs

Pour les appareils immersifs, l’aide et les meilleures pratiques pour HoloLens s’appliquent toujours, mais les valeurs spécifiques pour la zone de confort sont déplacées en fonction de la distance focale jusqu’à l’affichage. En général, les distances focale à ces écrans sont comprises entre 1,25 m-2,5 m. En cas de doute, évitez de rendre les objets d’intérêt trop proches des utilisateurs et essayez plutôt de conserver la plus grande partie du contenu.

## <a name="interpupillary-distance-and-vertical-offset"></a>Interpupillary distance et décalage vertical

Lorsque vous affichez du contenu numérique sur des écrans montés en tête (HMD), la position des yeux d’une visionneuse par rapport à la position d’affichage du contenu numérique est essentielle. Plus précisément, les deux distances interpupillary ([IPD](https://en.wikipedia.org/wiki/Pupillary_distance)) et verticale offset (VO) sont importantes pour une vue confortable du contenu numérique dans HMDs. 

L’IPD fait référence à la distance entre les élèves, ou les centres, des yeux d’un individu. La fonction VO fait référence au décalage vertical potentiel du contenu numérique présenté à chaque œil par rapport à l’axe horizontal des yeux de la visionneuse (en particulier, il ne s’agit pas du même décalage horizontal, ni de la disparité binoculaire). Le fait de ne pas faire correspondre un ou plusieurs de ces facteurs à un utilisateur individuel peut aggraver les effets de la gêne causée par le conflit de vergence, mais cela peut même causer une gêne quand V-A est réduit (par exemple, pour le contenu affiché au niveau de la station focale 2.0 m). distance du HoloLens). 

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils holographiques

#### <a name="hololens-1st-gen"></a>HoloLens (1ère génération)

Pour HoloLens (1re génération), l’IPD est estimée et définie pendant l' [étalonnage](calibration.md)de l’appareil. Pour les nouveaux utilisateurs sur un appareil déjà configuré, l’étalonnage doit être exécuté ou l’IPD doit être défini manuellement. La fonction VO dépend entièrement de l’appareil. Plus précisément, pour réduire la valeur de VO, l’appareil doit être placé sur la tête de l’utilisateur, de telle sorte que les affichages soient de niveau avec l’axe de ses yeux. 

#### <a name="hololens-2"></a>HoloLens 2

Pour HoloLens 2, l’IPD est estimée et définie pendant l' [étalonnage](calibration.md)oculaire/appareil. Pour les nouveaux utilisateurs sur un appareil déjà configuré, l’étalonnage doit être exécuté pour garantir que l’IPD est correctement défini. Le VO est comptabilisé automatiquement dans HoloLens 2. 

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersifs

Les HMDs immersifs Windows Mixed Reality n’ont pas d’étalonnage automatique pour IPD ou VO. L’IPD peut être définie manuellement dans le logiciel (sous paramètres du portail de réalité mixte, voir [étalonnage](calibration.md)), ou certains HMDs ont un curseur mécanique qui permet à l’utilisateur d’ajuster l’espacement des lentilles à une position confortable (c’est-à-dire, qui correspond approximativement à leur IPD). 

## <a name="rendering-rates"></a>Taux de rendu

Les applications de réalité mixte sont uniques, car les utilisateurs peuvent se déplacer librement dans le monde et interagir avec du contenu virtuel comme s’ils étaient des objets réels. Pour maintenir cette impression, il est essentiel de rendre les hologrammes de sorte qu’ils apparaissent stables dans le monde et s’animent facilement. Le rendu à un [minimum de 60 images par seconde (FPS)](understanding-performance-for-mixed-reality.md) aide à atteindre cet objectif. Certains appareils de réalité mixte prennent en charge le rendu à trames plus de 60 FPS et pour ces appareils, il est vivement recommandé de les rendre au trames supérieur pour offrir une expérience utilisateur optimale.

**Approfondissement**

Pour dessiner des hologrammes pour [qu’ils soient stables dans le monde réel ou virtuel, les](hologram-stability.md)applications doivent restituer des images à partir de la position de l’utilisateur. Étant donné que le rendu d’image prend du temps, HoloLens et d’autres appareils Windows Mixed Reality prévoient où la tête d’un utilisateur sera affichée lorsque les images seront affichées dans les affichages. Cet algorithme de prédiction est une approximation. Les algorithmes et le matériel Windows Mixed Reality ajustent l’image rendue pour tenir compte de l’écart entre la position de la tête prédite et la position réelle de la tête. Ce processus rend l’image visible par l’utilisateur comme si elle était affichée à partir de l’emplacement approprié, et les hologrammes semblent stables. Les mises à jour fonctionnent mieux pour les modifications mineures de la position de la tête, et elles ne peuvent pas complètement tenir compte des différences d’images rendues, comme celles provoquées par motion-parallaxe.

**En procédant à un rendu d’une cadence minimale de 60 FPS, vous effectuez deux opérations pour vous aider à créer des hologrammes stables:**
1. Réduction de l’apparence de Judder, qui est caractérisée par des images inégales et des images doubles. Un mouvement d’hologramme plus rapide et des taux de rendu inférieurs sont associés à des Judder plus prononcées. Par conséquent, si vous vous efforcez toujours de conserver 60 FPS (ou le taux de rendu maximal de votre appareil), vous pouvez éviter Judder pour déplacer des hologrammes.
2. Minimisation de la latence globale. Dans un moteur avec un thread de jeu et un thread de rendu s’exécutant dans échelons, l’exécution de sur 30FPS peut ajouter 33,3 ms de latence supplémentaire. En diminuant la latence, cela réduit l’erreur de prédiction et augmente la stabilité de l’hologramme.

**Analyse des performances**

Il existe un large éventail d’outils qui peuvent être utilisés pour évaluer la fréquence d’images de votre application, par exemple:
* GPUView
* Débogueur graphique Visual Studio
* Profileurs intégrés à des moteurs 3D tels que le débogueur de frame dans Unity

## <a name="self-motion-and-user-locomotion"></a>Automotion et utilisateur locomotion

La seule limitation est la taille de votre espace physique; Si vous souhaitez permettre aux utilisateurs de se déplacer plus loin dans l’environnement virtuel que dans leurs véritables salles, une forme de mouvement purement virtuel doit être implémentée. Toutefois, un mouvement virtuel soutenu qui ne correspond pas au mouvement physique réel de l’utilisateur peut parfois provoquer des mouvements de maladie. Ce résultat est dû aux *signaux visuels* pour l’auto-déplacement du *monde virtuel* en conflit avec les [signaux Vestibular](https://en.wikipedia.org/wiki/Vestibular_system) pour l’auto-Motion provenant du *monde réel*.

Heureusement, il existe des conseils pour l’implémentation de locomotion utilisateur qui peuvent aider à éviter ce problème:
* Mettez toujours l’utilisateur au contrôle de ses mouvements; l’auto-déplacement inattendu est particulièrement problématique
* Les êtres humains sont très sensibles à la direction de la gravité. Par conséquent, les mouvements verticaux non initiés par l’utilisateur doivent être évités.

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils holographiques

Une méthode pour permettre à l’utilisateur de passer à un autre emplacement dans un grand environnement virtuel consiste à donner l’impression qu’il déplace un petit objet dans la scène. Cet effet peut être obtenu comme suit:
   1. Fournissez une interface dans laquelle l’utilisateur peut sélectionner un emplacement dans l’environnement virtuel où il souhaite se déplacer.
   2. Une fois la sélection effectuée, réduisez le rendu de la scène sur un disque autour de l’emplacement souhaité.
   3. Tout en conservant l’emplacement sélectionné, autorisez l’utilisateur à le déplacer comme s’il s’agissait d’un petit objet. L’utilisateur peut ensuite déplacer la sélection à proximité de ses pieds.
   4. Lors de la désélection, reprendre le rendu de la scène entière.

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersifs

L’approche d’appareil holographique précédente ne fonctionne pas aussi bien sur un appareil immersif, car elle nécessite que l’application affiche un grand noir ou un autre environnement par défaut tout en déplaçant le disque. Ce traitement interrompt le sens de l’immersion. Une astuce pour l’utilisateur locomotion dans un casque immersif est l’approche de «clignotement». Cette implémentation permet à l’utilisateur de contrôler son mouvement et donne un bref aperçu du mouvement, mais il est tellement bref que l’utilisateur est moins enclin à être déorienté par le libre-mouvement purement virtuel:
   1. Fournissez une interface dans laquelle l’utilisateur peut sélectionner un emplacement dans l’environnement virtuel où il souhaite se déplacer.
   2. Lors de la sélection, commencez un mouvement très rapide simulé (100 m/s) vers cet emplacement tout en découpant rapidement le rendu.
   3. Rétrécit le rendu en arrière après avoir terminé la traduction.

## <a name="heads-up-displays"></a>Affichages des têtes

Dans First-Person-Shooter videogames, Head-Up affiche (HUDs) des informations persistantes telles que l’intégrité du joueur, les mini-cartes et les inventaires directement à l’écran. HUDs fonctionne bien pour rester informé du joueur sans être confronté à l’expérience de jeu. Dans les expériences de réalité mixte, les HUDs ont le potentiel de provoquer une gêne importante et doivent être adaptés au contexte plus immersif. Plus précisément, les HUDs qui sont verrouillés de manière rigide sur l’orientation des têtes de l’utilisateur sont susceptibles de produire une gêne. Si une application requiert un HUD, nous vous recommandons de verrouiller le *corps* plutôt que le verrouillage de la tête. Ce traitement peut être implémenté sous la forme d’un ensemble d’affichages qui se traduisent immédiatement avec l’utilisateur, mais ne pivotent pas avec la tête de l’utilisateur jusqu’à ce qu’un seuil de rotation soit atteint. Une fois cette rotation effectuée, le HUD peut se réorienter pour présenter les informations dans le champ de vue de l’utilisateur. L’implémentation de la rotation et de la translation HUD 1:1 par rapport aux mouvements de l’en-tête de l’utilisateur doit toujours être évitée.

## <a name="text-legibility"></a>Lisibilité du texte

La lisibilité optimale du texte peut aider à réduire les fatigues oculaires et à maintenir le confort des utilisateurs, en particulier dans les applications ou les scénarios qui obligent les utilisateurs à lire dans un HMD. La lisibilité du texte dépend de divers facteurs, notamment des propriétés d’affichage (par exemple, densité de pixels, luminosité, contraste), des propriétés d’objectif (par exemple, une aberration chromatique) et des propriétés de texte/police (par exemple, la police spécifique). caractéristiques telles que le poids, l’espacement, les Serif, etc., la couleur de police, la couleur d’arrière-plan).  

En général, nous vous recommandons de tester la lisibilité d’applications spécifiques et de faire en sorte que les tailles de police soient aussi importantes que possible pour une expérience confortable. Ci-dessous, nous proposons des recommandations générales comme point de départ pour le développement. Notez que toutes les tailles de police sont signalées en degrés d' [angle visuel](https://en.wikipedia.org/wiki/Visual_angle) plutôt qu’en tant que tailles physiques spécifiques, ce qui fournit des conseils pour toute distance au sein de la zone de positionnement optimal des hologrammes, car il tient compte de la taille du texte et de la distance qu’il apparaît dans la visionneuse. 

Pour obtenir des instructions plus détaillées, consultez [typographie](typography.md) et [texte dans](text-in-unity.md) les pages Unity.

### <a name="guidance-for-holographic-devices"></a>Conseils pour les appareils holographiques

Pour les appareils holographiques, le rendu de texte noir/foncé sur un arrière-plan blanc/clair fournit le rapport de contraste le plus cohérent, car l’arrière-plan occultait les interférences du monde réel derrière le rendu. Le rendu de texte blanc/clair sur un arrière-plan noir/foncé permet à un plus grand nombre d’environnements réels de s’afficher, ce qui peut interférer avec la lisibilité du texte. 

#### <a name="hololens-1st-gen"></a>HoloLens (1ère génération)

La taille de police minimale lisible (mesurée à partir de la ligne de base de police à ascendeur) est d’environ 0,35 ° et la taille de police confortable est d’au moins 0,5 ° pour la lecture du contenu présenté à une distance de 2 m à l’utilisateur. 

#### <a name="hololens-2"></a>HoloLens 2

La taille de police minimale lisible (mesurée à partir de la ligne de base de la police à la version ascendante) est au moins égale à environ: 
   - 0,4 °-0,5 ° à 45cm (distance de manipulation directe) 
   - 0.35 °-0,4 ° à 2,0 m
   
La taille de police lisible (mesurée à partir de la ligne de base de la police à l’ascendeur) est au moins égale à environ: 
   - 0,65 °-0,8 ° à 45cm (distance de manipulation directe)
   - 0,6 °-0,75 ° à 2,0 m

Notez que les tailles de police doivent être légèrement supérieures pour le texte aux distances de manipulation directe en raison du conflit d’hébergement vergence décrit ci-dessus (les yeux des utilisateurs s’adaptent à une distance de 2,0 m sur l’affichage HoloLens, afin que le contenu soit rendu, par exemple, 45cm peut paraître plus flou pour les utilisateurs). 

### <a name="guidance-for-immersive-devices"></a>Conseils pour les appareils immersifs

Les appareils immersifs présentent généralement des taux de contraste plus élevés en raison de l’occlusion complète de l’environnement extérieur, mais peuvent avoir une densité de pixels plus faible en partie en raison de l’agrandissement des lentilles devant les écrans. 

Pour les HMDs immersifs Windows Mixed Reality, la taille de police verticale minimale (mesurée à partir de la ligne de base de la police à Ascender) est approximativement de 0,7-0,9 ° et la taille de police verticale confortable est d’environ 1,0 ° pour la lecture du contenu présenté à une distance de 2m à la utilisateur.

## <a name="gaze-direction"></a>Sens du regard

Pour éviter les variations oculaires et cervicales, le contenu doit être conçu de manière à éviter les mouvements d’oeil excessif et de cou.
* **Évitez** les angles de regard de plus de 10 degrés au-dessus de l’horizon (déplacement vertical)
* **Évitez** les angles de regard de plus de 60 degrés en dessous de l’horizon (déplacement vertical)
* **Évitez** les rotations du cou de plus de 45 degrés hors Centre (déplacement horizontal)

L’angle de regard optimal (repos) est considéré entre 10-20 degrés au-dessous de l’horizontale, car l’en-tête tend à pivoter légèrement vers le bas, en particulier pendant les activités.

![Champ de vision (angle de vue) autorisé, tel que déterminé par la plage de cou](images/optimal-field-of-view-2-750px.png)<br>
*Champ de vision (angle de vue) autorisé, tel que déterminé par la plage de cou*

## <a name="arm-positions"></a>Positions ARM

La fatigue musculaire peut s’accumuler lorsque les utilisateurs sont censés conserver une main tout au long de la durée d’une expérience. Il peut également être fatiguing pour obliger l’utilisateur à effectuer des mouvements de pression d’air à plusieurs reprises sur de longues durées. Nous vous recommandons donc d’éviter d’avoir à utiliser des entrées de mouvement constantes et répétées. Cet objectif peut être atteint en incorporant des sauts courts ou en proposant une combinaison de saisie de mouvement et de voix pour interagir avec l’application.

## <a name="see-also"></a>Voir aussi
* [Pointage du regard](gaze.md)
* [Stabilité des hologrammes](hologram-stability.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Image holographique](holographic-frame.md)
* [Étalonnage](calibration.md)
