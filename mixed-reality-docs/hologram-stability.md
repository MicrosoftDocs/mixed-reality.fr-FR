---
title: Stabilité HOLOGRAMME
description: HoloLens automatiquement les hologrammes stabilise, mais les développeurs peuvent prendre pour améliorer la stabilité hologramme davantage des mesures.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: hologrammes, stabilité, hololens
ms.openlocfilehash: b35b904e3c662c5ebd0670a98044706fe208e348
ms.sourcegitcommit: c20563b8195c0c374a927b96708d958b127ffc8f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974937"
---
# <a name="hologram-stability"></a>Stabilité HOLOGRAMME

Pour obtenir les hologrammes stables, HoloLens dispose d’un pipeline de stabilisation d’image intégrée. Le pipeline de stabilisation fonctionne automatiquement en arrière-plan, il y a aucune étape supplémentaire requise pour l’activer. Toutefois, les développeurs doivent exercer techniques qui améliorent la stabilité hologramme et éviter les scénarios qui réduisent la stabilité.

## <a name="hologram-quality-terminology"></a>Terminologie de qualité HOLOGRAMME

La qualité de hologrammes est un résultat de bon environnement et du développement de la bonne application. Les applications qui atteint une constante 60 frames par seconde dans un environnement où HoloLens peut suivre environs garantit que l’hologramme et le système de coordonnées correspondant sont synchronisés. À partir d’un utilisateur, hologrammes destinés à être stationnaire déplacera pas par rapport à l’environnement.

Lors de l’environnement émet, taux de rendu incohérent ou faible ou d’autres problèmes de l’application s’affichent, la terminologie suivante est utile pour identifier le problème.
* **Analyse de précision.** Une fois que l’hologramme est verrouillé de monde et placé dans le monde réel, il doit rester où il a été placé, par rapport à l’environnement ambiant, indépendamment de mouvement de l’utilisateur ou de modifications de l’environnement de petite et partiellement alloué. Si un hologramme apparaît ultérieurement dans un emplacement inattendu, c’est un *précision* problème. Scénarios de ce type peuvent se produire si deux pièces distinctes semblent identiques.
* **Jitter.** Les utilisateurs observer ce phénomène en tant que fréquence élevée faire bouger un hologramme. Cela peut se produire lorsque le suivi de l’environnement se dégrade. Pour les utilisateurs, la solution est en cours d’exécution [capteur réglage](sensor-tuning.md).
* **Judder.** Les fréquences de rendu de basse entraînent mouvement inégale et images double de hologrammes. Cela est particulièrement notable dans hologrammes avec motion. Les développeurs doivent maintenir un [constante 60 FPS](hologram-stability.md#frame-rate).
* **Dérive.** Les utilisateurs voient ceci comme hologramme apparaît à s’éloigner d’où il a été placé à l’origine. Cela se produit lorsque hologrammes sont placés loin de [ancres spatiales](spatial-anchors.md), en particulier dans les parties de l’environnement qui n’ont pas été entièrement mappés. Création hologrammes proche ancres spatiales réduit la probabilité d’une dérive.
* **Jumpiness.** Quand un hologramme « POP » ou « passe » en dehors de son emplacement occasionnellement. Cela peut se produire comme suivi ajuste hologrammes pour correspondre à la mise à jour de compréhension de votre environnement.
* **Swim.** Quand un hologramme semble sway correspondant pour le mouvement de tête de l’utilisateur. Cela se produit lorsque hologrammes ne sont pas sur le [plan de stabilisation](hologram-stability.md#stabilization-plane), et si le HoloLens n’est pas [étalonnés](calibration.md) pour l’utilisateur actuel. L’utilisateur peut réexécuter la [étalonnage](calibration.md) application pour résoudre ce problème. Les développeurs peuvent mettre à jour le plan de stabilisation pour améliorer la stabilité.
* **Séparation des couleurs.** L’affiche dans HoloLens est un affichage séquentiel de couleur, qui flash des canaux de couleur du rouge-vert-bleu-vert à 60Hz (couleur individuelle champs sont affichés à 240Hz). Chaque fois qu’un utilisateur effectue le suivi d’un déplacement hologramme avec ses propres yeux, de ce hologramme bords de tête et fin séparer dans leurs couleurs constitutifs, produisant un effet arc-en-ciel. Le degré de séparation dépend de la vitesse de l’hologramme. Dans certains cas rares, un déplacement de celles head rapidement lorsque vous examinez un hologramme stationnaire peut également entraîner un effet arc-en-ciel. Il s’agit  *[séparation des couleurs](hologram-stability.md#color-separation)*.

## <a name="frame-rate"></a>Fréquence d’images

Fréquence d’images est le premier pilier de la stabilité hologramme. Pour hologrammes apparaissent stable dans le monde, chaque image présentée à l’utilisateur doit avoir les hologrammes dessinés à l’endroit correct. Affiche lors de l’actualisation de HoloLens 240 fois par seconde, montrant quatre champs de couleur distinct pour chaque qui vient d’être rendu image, ce qui entraîne une expérience utilisateur de 60 i/s (images par seconde). Pour fournir la meilleure expérience possible, les développeurs d’applications doivent maintenir 60 i/s, ce qui se traduit par manière cohérente en fournissant une nouvelle image du système d’exploitation à toutes les 16 millisecondes.

**60 FPS** pour dessiner hologrammes s’affichent comme ils étaient assis dans le monde réel, HoloLens doit restituer des images à partir de la position de l’utilisateur. Étant donné que le rendu d’image prend de temps, HoloLens prédit où tête de l’utilisateur est quand les images sont affichés dans les affichages. Cet algorithme de prédiction est une approximation. HoloLens possède un matériel qui ajuste l’image rendue au compte pour l’écart entre la position de tête prédite et la position réelle principale. Cela rend l’image de l’utilisateur voit s’affichent comme si elle a été restituée à partir de l’emplacement approprié et hologrammes sentent stables. L’image des mises à jour mieux avec de petits changements, et il ne peut pas résoudre complètement certaines choses dans l’image rendue comme parallaxe de mouvement.

Par rendu à 60 FPS, vous effectuez trois choses pour aider à tirer hologrammes stables :
1. Pour réduire la latence globale entre le rendu d’une image et cette image qui est vu par l’utilisateur. Dans un moteur avec un thread de jeu et un thread de rendu en cours d’exécution par échelons, en cours d’exécution à 30 i/s peut ajouter des 33.3ms de latence supplémentaire. En réduisant la latence, cela diminue l’erreur de prédiction et augmente la stabilité hologramme.
2. Rend donc chaque image atteindre les yeux de l’utilisateur ont un degré de cohérence de latence. Si vous effectuez le rendu à 30 i/s, l’affichage affiche toujours les images à 60 FPS. Cela signifie que la même image s’affichera deux fois dans une ligne. La deuxième image aura 16.6ms latence plus que la première trame et devrez corriger une quantité plus prononcée d’erreurs. Cette incohérence dans la magnitude d’erreur peut entraîner indésirables SEQUENCES 60hz.
3. En réduisant l’apparence de SEQUENCES, qui se caractérise par motion inégale et images double. Mouvement de hologramme plus rapide et le rendu inférieure tarifs associés à plus prononcé judder. Par conséquent, effort pour assurer 60 FPS carrément fois permettra d’éviter SEQUENCES pour un hologramme déplacement donné.

**Cohérence de la fréquence d’images** cohérence de taux de Frame est tout aussi importante que les images par seconde élevé. Supprimait parfois les trames sont inévitables pour toutes les applications riches en contenu, et le HoloLens implémente certains algorithmes sophistiqués pour récupérer à partir de problèmes occasionnels. Toutefois, une fréquence d’images constamment fluctuante est beaucoup plus perceptible par un utilisateur que l’exécution de manière cohérente à des fréquences d’images plus faibles. Par exemple, une application qui effectue le rendu sans heurts pour les 5 cadres (60 i/s pendant la durée de ces 5 images), puis supprime autres cadres pour les frames ensuite 10 (30 i/s pendant la durée de ces 10 images) apparaîtront plus instable qu’une application constamment génère le rendu à 30 i/s.

Par ailleurs, le système d’exploitation limitera les applications jusqu'à 30 i/s lorsque [mixte de capture de la réalité](mixed-reality-capture.md) est en cours d’exécution.

**Analyse des performances** il existe un large éventail d’outils qui peut être utilisé pour évaluer votre taux de frame d’application telles que :
* GPUView
* Débogueur de Visual Studio Graphics
* Profileurs intégrées à des moteurs 3D tels que Unity

## <a name="hologram-render-distances"></a>Distances de rendu HOLOGRAMME

>[!VIDEO https://www.youtube.com/embed/-606oZKLa_s]

Le système visual humain s’intègre plusieurs signaux distance dépendant lorsqu’il fixates et se concentre sur un objet.
* [Hébergement](https://en.wikipedia.org/wiki/Accommodation_%28eye%29) -le focus d’un œil individuel.
* [Convergence](https://en.wikipedia.org/wiki/Convergence_(eye)) - deux yeux déplacement vers l’intérieur ou vers l’extérieur vers le centre sur un objet.
* [Vision (jumelles)](https://en.wikipedia.org/wiki/Stereopsis) -disparités entre les images de gauche et de droite noir qui dépendent de la distance d’un objet en dehors de votre point de fixation.
* Ombrage, taille angular relative et autres signaux monoculaire (yeux unique).

Convergence et hébergement sont uniques, car elles sont très rétiniens signaux liés à l’évolution des yeux pour percevoir les objets à des distances différentes. Dans l’affichage naturelle, convergence et hébergement sont liés. Lorsque les yeux afficher quelque chose près (par exemple, votre nez) les yeux croisent et prendre en charge à un point de near. Lorsque les yeux afficher quelque chose à l’infini que les yeux deviennent parallèle et le œil prend en charge à l’infini. Les utilisateurs qui HoloLens inclura toujours à m 2.0 pour maintenir une image claire, car le HoloLens affiche sont fixés à une distance optique environ 2.0m éloignée de l’utilisateur. Contrôle les développeurs d’applications où les yeux des utilisateurs convergent en plaçant le contenu et hologrammes à des profondeurs différents. Lorsque les utilisateurs prendre en charge et convergent vers différentes distances, le lien physique entre les deux signaux sont interrompues, et cela peut entraîner une gêne visual ou fatigue, en particulier lorsque l’amplitude du conflit est volumineux. Maux de conflit vergence-hébergement peut être évitée ou réduite en conservant le contenu que les utilisateurs convergent vers aussi proches m 2.0 que possible (par exemple, dans une scène avec un grand nombre de profondeur placer les zones d’intérêt près 2.0 m lorsque cela est possible). Lorsque le contenu ne peut pas être placé quasi m 2.0 maux de conflit vergence-hébergement est plus grande lorsque l’utilisateur de l’utilisation des allers et retours entre différentes distances. En d’autres termes, il est beaucoup plus à l’aise examiner un hologramme stationnaire qui reste 50cm qu’aux examiner un hologramme 50cm suite qui déplace les vers et à vous au fil du temps.

Placer le contenu à m 2.0 est également avantageux parce que les deux écrans sont conçus pour se chevauchent entièrement à cette distance. Pour les images placées hors de ce plan, lorsqu’ils passent du côté du frame HOLOGRAPHIQUE, elles seront disparaissent à partir d’un seul affichage tout en étant visible sur l’autre. Cette rivalité (jumelles) peut être perturbante pour l’impression de profondeur l’hologramme.

**Distance optimale pour placer hologrammes à partir de l’utilisateur**

![Distance optimale pour placer hologrammes à partir de l’utilisateur](images/distanceguiderendering-750px.png)

**Plans de coupe** pour un maximum de confort, nous recommandons distance de rendu de découpage à 85 cm avec fadeout du contenu, en commençant à 1 million. Dans les applications où hologrammes et les utilisateurs sont les deux hologrammes STATIONNAIRES sont consultables confortablement aussi près que 50cm. Dans ce cas, les applications doivent placer un plan de découpage ne moins de 30 centimètres de fondu doit au moins 10cm en dehors du plan de découpage. Chaque fois que le contenu est plus proche que cm 85, il est important de s’assurer que les utilisateurs ne se déplacent pas fréquemment ou se rapprocher loin hologrammes ou que hologrammes ne pas fréquemment se rapprocher ou plus loin de l’utilisateur car ces situations sont plus susceptibles de provoquer des maux de la conflit de vergence-hébergement. Contenu doit être conçu pour minimiser la nécessité d’interaction de moins de 85cm à partir de l’utilisateur, mais lorsque le contenu doit être restitué proche que 85cm une règle empirique pour les développeurs consiste à concevoir des scénarios où les utilisateurs et/ou hologrammes ne déplacent pas en profondeur plus de 25 % de t Il est temps.

**Meilleures pratiques** lorsque hologrammes ne peut pas être placés au 2 m et les conflits entre convergence et d’hébergement ne peut pas être évitées, la zone optimale pour la sélection élective hologramme est entre 1,25 m et 5 m. Dans tous les cas, les concepteurs doivent structurer le contenu à encourager les utilisateurs à interagir 1 + m (par exemple, ajuster la taille du contenu et les paramètres de sélection élective par défaut).

## <a name="stabilization-plane"></a>Plan de stabilisation
> [!NOTE]
> Pour des casques IMMERSIFS bureau, la définition d’un plan de stabilisation est généralement contre-productive, car elle offre moins qualité visuelle que fournissant la mémoire tampon de profondeur de votre application pour le système pour activer reprojection en fonction de profondeur de par pixel. Sauf en cours d’exécution sur un HoloLens, vous devez généralement éviter de définir le plan de stabilisation.

HoloLens effectue une technique sophistiquées HOLOGRAPHIQUE stabilisation assistée par matériel. Cela est en grande partie automatique et a trait à motion et modification du point de vue (CameraPose) comme anime la scène et l’utilisateur déplace leur tête. Un plan unique, appelé le plan de stabilisation, est choisi pour optimiser cette stabilisation. Alors que tous les hologrammes dans la scène recevoir certains stabilisation, hologrammes dans le plan de stabilisation reçoivent la stabilisation matérielles maximales.

![Plan de stabilisation pour les objets 3D](images/stab-plane-500px.jpg)

L’appareil va automatiquement essayer de choisir ce plan, mais l’application peut faciliter ce processus en sélectionnant le point de focus dans la scène. Les applications Unity en cours d’exécution sur un HoloLens doivent choisir le meilleur concentrer point en fonction de votre scène et le transmettre dans [SetFocusPoint()](focus-point-in-unity.md). Un exemple de définition du point de focus dans DirectX est inclus dans le modèle de cube en rotation par défaut.

Notez que lorsque votre application Unity s’exécute sur un casque immersif connecté à un PC de bureau, Unity soumettre votre mémoire tampon de profondeur à Windows pour activer reprojection par pixel, ce qui vous fournira généralement de meilleure qualité d’image sans travail explicite par l’application. Si vous fournissez un Point de Focus, qui remplacent la reprojection par pixel, donc vous devez uniquement faire quand votre application s’exécute sur un HoloLens.




```cs
// SetFocusPoint informs the system about a specific point in your scene to
// prioritize for image stabilization. The focus point is set independently
// for each holographic camera.
// You should set the focus point near the content that the user is looking at.
// In this example, we put the focus point at the center of the sample hologram,
// since that is the only hologram available for the user to focus on.
// You can also set the relative velocity and facing of that content; the sample
// hologram is at a fixed point so we only need to indicate its position.
renderingParameters.SetFocusPoint(
    currentCoordinateSystem,
    spinningCubeRenderer.Position
    );
```

Positionnement du point de focus dépend en grande partie l’hologramme consulte. L’application a le vecteur du pointage de regard pour référence et le Concepteur d’application sait quel contenu ils veulent l’utilisateur à observer.

Le seul qu'un développeur peut faire pour stabiliser hologrammes est essentiel pour restituer à 60 FPS. Le déplacement sous 60 i/s permet de réduire considérablement la stabilité de HOLOGRAMME, quel que soit l’optimisation de plan de stabilisation.

**Meilleures pratiques** il n’existe aucun moyen universel pour définir le plan de stabilisation et il est spécifique à l’application, la principale recommandation consiste donc à faire des essais et voir ce qui convient le mieux à vos scénarios. Toutefois, essayez d’aligner le plan de stabilisation avec autant de contenu que possible, car tout le contenu de ce plan est stabilisé parfaitement.

Exemple :
* Si vous avez du contenu uniquement PLANAIRE (application de lecture, application de lecture vidéo), aligner le plan de stabilisation avec le plan ayant votre contenu.
* S’il existe 3 petites sphères qui sont verrouillés au monde, rendre le plan de stabilisation « Couper » bien que les centres de tous les domaines qui se trouvent actuellement dans la vue.
* Si votre scène a du contenu à des profondeurs substantiellement différents, favoriser davantage les objets.
* Veillez à ajuster le point de stabilisation consulte chaque trame pour coïncider avec l’hologramme l’utilisateur

**Choses à éviter** le plan de la stabilisation est un très bon outil pour atteindre hologrammes stables, mais si utilisés à mauvais escient il peut entraîner une instabilité image graves.
* Ne « fire and forget », dans la mesure où vous pouvez vous retrouver avec la stabilisation du plan de derrière l’utilisateur ou attaché à un objet qui n’est plus dans la vue de l’utilisateur. Vérifiez que le plan de stabilisation normal est défini opposé caméra-forward (par exemple, - camera.forward)
* Ne pas modifier rapidement le plan de stabilisation dans les deux sens entre extrêmes
* Ne laissez pas le plan de stabilisation défini sur une distance fixe/orientation
* Ne laissez pas le plan de stabilisation Couper par l’utilisateur
* Ne définir le point de focus lors de l’exécution sur un ordinateur de bureau, PC, et non un HoloLens et à la place reposent sur reprojection en fonction de profondeur de par pixel.

## <a name="color-separation"></a>Séparation des couleurs 

En raison de la nature des écrans de HoloLens, un artefact appelé « séparation de couleur » peut parfois être perçu. Il se manifeste en tant que l’image de la séparation en couleurs de base individuelles - rouge, verts et bleus. L’artefact peut être particulièrement visible lors de l’affichage des objets blancs, dans la mesure où ils ont de grandes quantités de rouge, vert et bleu. Il est encore plus prononcée lorsqu’un utilisateur effectue le suivi de visuellement un hologramme qui a parcouru le frame HOLOGRAPHIQUE à vitesse élevée. Une autre façon que peut se manifester par l’artefact est déformation/déplacements d’objets. Si un objet possède le contraste élevé et/ou couleurs pures séparation des couleurs (rouge, verte et bleue), sera perçue comme déformation de différentes parties de l’objet.

**Exemple de quelles la séparation de couleur d’un curseur round blanc tête verrouillée pourrait ressembler comme un utilisateur fait pivoter leur tête sur le côté :**

![Exemple de quelles la séparation de couleur d’un curseur round blanc tête verrouillée pourrait ressembler comme un utilisateur fait pivoter leur tête sur le côté.](images/colorseparationofroundwhitecursor-300px.png)

S’il est difficile d’éviter complètement la séparation des couleurs, il existe plusieurs techniques disponibles pour les atténuer.

**Séparation des couleurs peut être consultée sur :**
* Les objets que déplacement rapidement, y compris les objets verrouillés en tête le [curseur](cursors.md).
* Les objets qui sont essentiellement loin de la [plan de stabilisation](hologram-stability.md#stabilization-plane).

**Pour atténuer les effets de la séparation des couleurs :**
* Rendre l’objet de retard du pointage de regard de l’utilisateur. Il doit apparaître comme si elle a certaines l’inertie et est attaché à la regards « sur springs ». Cela ralentit le curseur (ce qui réduit la distance de séparation) et le place derrière le point de regards probable de l’utilisateur. Dans la mesure où il rapidement rattrape lorsque l’utilisateur arrête leur regards le décalage il a l’air tout à fait normal.
* Si vous ne souhaitez pas déplacer un hologramme, essayez de garder sa vitesse de déplacement ci-dessous 5 degrés par seconde si vous pensez que l’utilisateur suit ce texte avec leurs yeux.
* Utilisez *light* au lieu de *geometry* pour le curseur. Une source d’éclairage virtuel attaché à la regards sera perçue comme un pointeur interactif, mais ne génère pas de séparation des couleurs.
* Ajustez le plan de stabilisation pour faire correspondre les hologrammes à que l’utilisateur est gazing.
* Vérifiez le rouge de l’objet, le vert ou le bleu.
* Basculer vers une version de floue du contenu. Par exemple, un curseur blanc arrondi peut être modification apportée à une ligne légèrement floue orientée dans la direction du mouvement.

Comme avant, le rendu à 60 i/s et en définissant le plan de stabilisation sont les techniques plus importants pour la stabilité hologramme. Tout d’abord accessible sur la séparation des couleurs notable, assurez-vous que la fréquence d’images répond aux attentes.

## <a name="see-also"></a>Voir aussi
* [Comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Couleurs, éclairage et matériaux](color,-light-and-materials.md)
* [Interactions instinctuelles](interaction-fundamentals.md)