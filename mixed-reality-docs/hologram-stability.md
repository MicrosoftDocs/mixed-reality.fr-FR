---
title: Stabilité des hologrammes
description: Le HoloLens stabilise automatiquement les hologrammes, mais il existe des étapes que les développeurs peuvent prendre pour améliorer davantage la stabilité des hologrammes.
author: thetuvix
ms.author: alexturn
ms.date: 07/08/2020
ms.topic: article
keywords: hologrammes, stabilité, hololens
appliesto:
- HoloLens
ms.openlocfilehash: 4a489c923138808e3afb545097c314f354b5ad2a
ms.sourcegitcommit: 2813f5b3027d47f7c6e9772338935eeccfa2aaec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86408207"
---
# <a name="hologram-stability"></a>Stabilité des hologrammes

## <a name="overview"></a>Vue d’ensemble

Pour obtenir des hologrammes stables, HoloLens dispose d’un pipeline de stabilisation d’image intégré. Le pipeline de stabilisation fonctionne automatiquement en arrière-plan. vous n’avez donc pas besoin d’effectuer des étapes supplémentaires pour l’activer. Toutefois, vous devez exercer des techniques qui améliorent la stabilité des hologrammes et évitez les scénarios qui réduisent la stabilité.

## <a name="hologram-quality-terminology"></a>Terminologie de la qualité des hologrammes

La qualité des hologrammes est un résultat d’un bon environnement et d’un développement d’applications correct. Les applications qui s’exécutent à une constante 60 images par seconde dans un environnement où HoloLens peut suivre l’environnement garantissent la synchronisation de l’hologramme et du système de coordonnées correspondant. Du point de vue de l’utilisateur, les hologrammes destinés à être stationnaires ne seront pas déplacés par rapport à l’environnement.

La terminologie suivante peut vous aider lorsque vous identifiez des problèmes liés à l’environnement, à des taux de rendu incohérents ou peu élevés, ou à tout autre.
* **Précision.** Une fois que l’hologramme est verrouillé et placé dans le monde réel, il doit rester à l’endroit où il est placé par rapport à l’environnement environnant et indépendamment du mouvement de l’utilisateur ou des modifications de l’environnement faible et épars. Si un hologramme s’affiche plus tard dans un emplacement inattendu, il s’agit d’un problème de *précision* . De tels scénarios peuvent se produire si deux salles distinctes paraissent identiques.
* **Instabilité.** Les utilisateurs observent le bougé comme un tremblement haute fréquence d’un hologramme, ce qui peut se produire lorsque le suivi de l’environnement se dégrade. Pour les utilisateurs, la solution exécute le [Paramétrage du capteur](sensor-tuning.md).
* **Judder.** Une faible fréquence de rendu entraîne des mouvements inégaux et des images double d’hologrammes. Judder est particulièrement visible dans les hologrammes avec motion. Les développeurs doivent conserver une [constante de 60 fps](hologram-stability.md#frame-rate).
* **Cession.** Les utilisateurs voient la dérive lorsqu’un hologramme s’éloigne de l’endroit où il a été placé à l’origine. La dérive se produit lorsque les hologrammes sont placés loin des [ancres spatiales](spatial-anchors.md), en particulier dans les parties de l’environnement qui ne sont pas entièrement mappées. La création d’hologrammes proches des ancres spatiales réduit la probabilité de dérive.
* **Jumpiness.** Quand un hologramme « sort » ou « saute » à son emplacement, parfois. Jumpiness peut se produire lorsque le suivi ajuste les hologrammes pour correspondre à la compréhension mise à jour de votre environnement.
* **Jeter.** Lorsqu’un hologramme apparaît sur le Sway correspondant au mouvement de la tête de l’utilisateur. Cet événement se produit lorsque l’application n’a pas été [entièrement implémentée et que](hologram-stability.md#reprojection)la vue HoloLens n’est pas [étalonnée](calibration.md) pour l’utilisateur actuel. L’utilisateur peut réexécuter l’application d' [étalonnage](calibration.md) pour résoudre le problème. Les développeurs peuvent mettre à jour le plan de stabilisation pour améliorer la stabilité.
* **Séparation des couleurs.** Les affichages dans HoloLens sont des affichages séquentiels de couleur, qui sont des canaux de couleur Flash rouge-vert-bleu-vert à 60 Hz (les champs de couleur individuels sont affichés à 240 Hz). Chaque fois qu’un utilisateur effectue le suivi d’un hologramme mobile avec ses yeux, les bords de début et de fin de l’hologramme sont séparés dans leurs couleurs constitutives, ce qui produit un effet arc-en-ciel. Le degré de séparation dépend de la vitesse de l’hologramme. Dans certains cas plus rares, le déplacement des têtes s’effectue rapidement tout en regardant un hologramme stationnaire, ce qui se traduit par une *[séparation des couleurs](hologram-stability.md#color-separation)*.

## <a name="frame-rate"></a>Fréquence d’images

La fréquence d’images est le premier pilier de la stabilité de l’hologramme. Pour que les hologrammes apparaissent stables dans le monde, chaque image présentée à l’utilisateur doit avoir des hologrammes dessinés à l’endroit approprié. Le s’affiche sur HoloLens Refresh 240 fois par seconde, affichant quatre champs de couleur distincts pour chaque image nouvellement rendue, ce qui aboutit à une expérience utilisateur de 60 FPS (images par seconde). Pour offrir la meilleure expérience possible, les développeurs d’applications doivent gérer 60 images/s, ce qui se traduit par la fourniture cohérente d’une nouvelle image au système d’exploitation toutes les 16 millisecondes.

**60 fps** Pour dessiner des hologrammes pour qu’ils se trouvent dans le monde réel, HoloLens doit afficher les images à partir de la position de l’utilisateur. Étant donné que le rendu d’image prend du temps, HoloLens prédit l’emplacement où se trouve l’utilisateur lorsque les images sont affichées dans l’affichage. Toutefois, cet algorithme de prédiction est une approximation. HoloLens possède un matériel qui ajuste l’image rendue pour tenir compte de l’écart entre la position de la tête prédite et la position réelle de la tête. L’ajustement rend l’image visible par l’utilisateur comme si elle était affichée à partir de l’emplacement approprié, et les hologrammes semblent stables. Les mises à jour de l’image fonctionnent mieux avec les petites modifications, et elles ne peuvent pas entièrement résoudre certains éléments dans l’image rendue, par exemple Motion-parallaxe.

En procédant à un rendu à 60 FPS, vous effectuez trois opérations pour vous aider à créer des hologrammes stables :
1. Minimisation de la latence globale entre le rendu d’une image et cette image qui est visible par l’utilisateur. Dans un moteur avec un jeu et un thread de rendu s’exécutant dans échelons, l’exécution sur 30FPS peut ajouter 33,3 ms de latence supplémentaire. La réduction de la latence diminue l’erreur de prédiction et augmente la stabilité de l’hologramme.
2. En faisant en sorte que chaque image atteignant les yeux de l’utilisateur a une latence cohérente. Si vous le rendez à 30 i/s, l’affichage affiche toujours les images à 60 FPS, ce qui signifie que la même image s’affiche deux fois dans une ligne. Le deuxième Frame aura une latence de 16,6 ms supérieure à celle du premier frame et devra corriger une plus grande quantité d’erreur. Cette incohérence dans l’amplitude des erreurs peut entraîner des judders de 60 Hz indésirables.
3. Vous réduisez l’impression de vibration, qui se caractérise par des mouvements irréguliers et des images dédoublées. Les mouvements rapides des hologrammes et les fréquences d’images peu élevées provoquent une impression de vibration plus prononcée. Le maintien de la maintenance de 60 FPS à tout moment permet d’éviter Judder pour un hologramme mobile donné.

**Cohérence du taux de trames** La cohérence de la fréquence d’images est aussi importante qu’un nombre élevé d’images par seconde. Parfois, les trames supprimées sont inévitables pour toute application riche en contenu, et le HoloLens implémente des algorithmes sophistiqués pour effectuer une récupération suite à des erreurs occasionnelles. Toutefois, une fréquence d’images fluctuante est beaucoup plus perceptible pour un utilisateur que de s’exécuter régulièrement à des fréquences d’images inférieures. Par exemple, une application qui s’affiche en douceur pour cinq images (60 FPS pour la durée de ces cinq frames), puis supprime toutes les autres images pour les 10 images suivantes (30 i/s pour la durée de ces 10 images) apparaîtra plus instable qu’une application qui s’affiche régulièrement à 30 i/s.

Sur une note connexe, le système d’exploitation limite les applications à 30 FPS lorsque la capture de la [réalité mixte](mixed-reality-capture.md) est en cours d’exécution.

**Analyse des performances** Il existe différents types d’outils qui peuvent être utilisés pour évaluer la fréquence d’images de votre application, par exemple :
* GPUView
* Le débogueur de graphiques Visual Studio
* Profileurs intégrés à des moteurs 3D tels qu’Unity

## <a name="hologram-render-distances"></a>Distances de rendu d’hologramme

>[!VIDEO https://www.youtube.com/embed/-606oZKLa_s]

Le système visuel humain intègre plusieurs signaux dépendant des distances lorsqu’il fixates et se concentre sur un objet.
* [Hébergement](https://en.wikipedia.org/wiki/Accommodation_%28eye%29) : la focalisation d’un oeil individuel.
* [Convergence](https://en.wikipedia.org/wiki/Convergence_(eye)) : deux yeux se déplacent vers l’intérieur ou vers l’extérieur sur un objet.
* [Vision binoculaire](https://en.wikipedia.org/wiki/Stereopsis) : disparités entre les images de gauche et de droite qui dépendent de la distance d’un objet par rapport à votre point de fixation.
* Ombrage, taille angulaire relative et autres signaux monoculaire (simple oeil).

La convergence et l’hébergement sont uniques, car leurs signaux extra-rétinienne liés à la façon dont les yeux changent pour percevoir des objets à des distances différentes. Dans un affichage naturel, la convergence et l’hébergement sont liés. Lorsque la vue des yeux est proche (par exemple, votre nez), les yeux se croisent et s’adaptent à un point proche. Lorsque la vue des yeux est infinie, les yeux deviennent parallèles et l’œil s’ajuste à l’infini. 

Les utilisateurs qui ont le port HoloLens s’adapteront toujours à 2,0 m pour maintenir une image claire, car les affichages HoloLens sont fixés à une distance optique d’environ 2,0 mètres de l’utilisateur. Les développeurs d’applications contrôlent l’emplacement des yeux des utilisateurs en plaçant le contenu et les hologrammes à différents niveaux. Lorsque les utilisateurs s’accommodent de différentes distances, le lien naturel entre les deux signaux est cassé, ce qui peut entraîner une gêne visuelle ou une fatigue, en particulier lorsque l’ampleur du conflit est importante. 

Il est possible d’éviter ou de minimiser le conflit entre le vergence et l’hébergement en conservant un contenu convergé aussi proche que possible de 2,0 m (autrement dit, dans une scène avec un grand nombre de points d’intérêt près de 2,0 m, si possible). Lorsque le contenu ne peut pas être placé près de 2,0 m, le conflit entre le vergence et l’hébergement est plus grand lorsque l’utilisateur se déplace entre les différentes distances. En d’autres termes, il est bien plus facile de regarder un hologramme stationnaire qui reste 50 cm de plus que d’examiner un hologramme de 50 cm qui se déplace vers et à partir de vous dans le temps.

Il est également avantageux de placer du contenu à 2,0 m, car les deux écrans sont conçus pour se chevaucher entièrement à cette distance. Pour les images placées en dehors de ce plan, lorsqu’elles se déplacent du côté du cadre holographique, elles apparaissent d’un affichage à l’autre, tout en étant toujours visibles. Cette rivalisation binoculaire peut perturber le sentiment de profondeur du holorgam.

**Distance optimale pour le placement des hologrammes par rapport à l’utilisateur**

![Distance optimale pour le placement des hologrammes par rapport à l’utilisateur](images/distanceguiderendering-750px.png)

**Plans de coupe** Pour un maximum de confort, nous vous recommandons de découper la distance de rendu à 85 cm avec disparition en fondu du contenu à partir de 1 m. Dans les applications où les hologrammes et les utilisateurs sont à la fois stationnaires, les hologrammes peuvent être visualisés confortablement aussi près de 50 cm. Dans ces cas, les applications doivent placer un plan de découpage inférieur à 30 cm et la disparition en fondu doit commencer au moins 10 cm du plan de découpage. Chaque fois que le contenu est plus proche de 85 cm, il est important de s’assurer que les utilisateurs ne se déplacent pas souvent de manière plus proche ou plus éloignée des hologrammes, ou qu’ils ne se déplacent pas souvent plus près ou plus loin de l’utilisateur, car ces situations sont susceptibles de provoquer une gêne à cause du conflit d’hébergement vergence. Le contenu doit être conçu pour réduire le besoin d’interaction plus proche que 85 cm de l’utilisateur, mais quand le contenu doit être rendu plus proche que 85 cm, une bonne règle empirique pour les développeurs consiste à concevoir des scénarios dans lesquels les utilisateurs et/ou les hologrammes ne se déplacent pas plus de 25% du temps.

**Meilleures pratiques** Lorsque les hologrammes ne peuvent pas être placés à 2 m et que les conflits entre la convergence et l’hébergement ne peuvent pas être évités, la zone optimale pour le placement de l’hologramme est comprise entre 1,25 m et 5 mètres. Dans tous les cas, les concepteurs doivent structurer le contenu pour encourager les utilisateurs à interagir à 1 + m de distance (par exemple, ajuster la taille du contenu et les paramètres de positionnement par défaut).

## <a name="reprojection"></a>Reprojection
HoloLens effectue une technique de stabilisation holographique à assistance matérielle sophistiquée appelée reprojection. La reprojection prend en compte le mouvement et la modification du point de vue (CameraPose) à mesure que la scène s’anime et que l’utilisateur déplace sa tête.  Les applications doivent prendre des mesures spécifiques pour utiliser au mieux la reprojection.


Il existe quatre types principaux de reprojection
* **Reprojection de profondeur :**  Produit les meilleurs résultats avec le moins d’effort possible de l’application.  Toutes les parties de la scène rendue sont stabilisées indépendamment en fonction de leur distance par rapport à l’utilisateur.  Certains artefacts de rendu peuvent être visibles lorsqu’il y a des modifications nettes en profondeur.  Cette option est uniquement disponible sur HoloLens 2 et les casques immersifs.
* **Reprojection planaire :**  Permet à l’application de contrôler précisément la stabilisation.  Un plan est défini par l’application et tout ce qui se trouve sur ce plan est la partie la plus stable de la scène.  Plus un hologramme est éloigné du plan, moins il sera stable.  Cette option est disponible sur toutes les plateformes Windows MR.
* **Reprojection plan automatique :**  Le système définit un plan de stabilisation à l’aide des informations contenues dans le tampon de profondeur.  Cette option est disponible sur HoloLens Generation 1 et HoloLens 2.
* **Aucun :** Si l’application n’a aucun effet, la reprojection planaire est utilisée avec le plan de stabilisation fixe à 2 mètres dans la direction du point de regard de l’utilisateur, ce qui produit généralement des résultats sous-standard.

Les applications doivent prendre des mesures spécifiques pour activer les différents types de reprojection
* **Reprojection de profondeur :** L’application soumet son tampon de profondeur au système pour chaque frame rendu.  Sur Unity, la reprojection de profondeur s’effectue à l’aide de l’option de **mémoire tampon de profondeur partagée** dans le volet **Windows Mixed Reality Settings** sous **gestion du plug-in XR**.  Les applications DirectX appellent CommitDirect3D11DepthBuffer.  L’application ne doit pas appeler SetFocusPoint.
* **Reprojection planaire :** Sur chaque image, les applications indiquent au système l’emplacement d’un plan à stabiliser.  Les applications Unity appellent SetFocusPointForFrame et doivent avoir une **mémoire tampon de profondeur partagée** désactivée.  Les applications DirectX appellent SetFocusPoint et ne doivent pas appeler CommitDirect3D11DepthBuffer.
* **Reprojection plan automatique :** Pour activer, l’application doit envoyer son tampon de profondeur au système comme pour la reprojection de profondeur.  Sur HoloLens 2, l’application doit ensuite SetFocusPoint avec un point de 0, 0 pour chaque trame.  Pour la génération de HoloLens 1, l’application ne doit pas appeler SetFocusPoint.

### <a name="choosing-reprojection-technique"></a>Choix de la technique de reprojection

Type de stabilisation |    Casques immersifs |    Génération HoloLens 1 | HoloLens 2
--- | --- | --- | ---
Reprojection de profondeur |    Recommandé |   N/A |   Recommandé<br/><br/>Les applications Unity doivent utiliser Unity 2018.4.12 ou version ultérieure ou Unity 2019,3 ou une version ultérieure. Sinon, utilisez la reprojection automatique planaire.
Reprojection plan automatique | N/A |   Valeur par défaut recommandée |   Recommandé si la reprojection de profondeur ne donne pas les meilleurs résultats<br/><br/>Les applications Unity sont recommandées pour utiliser Unity 2018.4.12 ou version ultérieure ou Unity 2019,3 ou une version ultérieure.  Les versions d’Unity précédentes fonctionnent avec des résultats de reprojection légèrement dégradés.
Reprojection planaire |   Non recommandé |   Recommandé si le plan automatique ne donne pas les meilleurs résultats | Utilisez si aucune des options de profondeur ne donne les résultats souhaités    

### <a name="verifying-depth-is-set-correctly"></a>La précision de la vérification est définie correctement
            
Lorsqu’une méthode de reprojection utilise la mémoire tampon de profondeur, il est important de vérifier que le contenu de la mémoire tampon de profondeur représente la scène rendue de l’application.  Un certain nombre de facteurs peuvent entraîner des problèmes. Si un deuxième appareil photo est utilisé pour afficher les superpositions de l’interface utilisateur, par exemple, il est probable qu’il remplace toutes les informations de profondeur de la vue réelle.  Les objets transparents ne définissent souvent pas la profondeur.  Une partie du rendu du texte ne définit pas la profondeur par défaut.  Il y aura des problèmes visibles dans le rendu lorsque la profondeur ne correspondra pas aux hologrammes rendus.
            
HoloLens 2 a un visualiseur qui indique où la profondeur est et n’est pas définie, ce qui peut être activé à partir du portail de l’appareil.  Dans l’onglet **vues**  >  de**stabilité d’hologramme** , activez la case à cocher Afficher la **visualisation de profondeur dans le casque** .  Les zones dont la profondeur est définie correctement sont bleues.  Les éléments rendus qui n’ont pas d’ensemble de profondeur sont marqués en rouge et doivent être corrigés.  

> [!NOTE]
> La visualisation de la profondeur n’apparaît pas dans la capture de la réalité mixte.  Il n’est visible que par l’intermédiaire de l’appareil.
            
Certains outils d’affichage GPU permettent de visualiser le tampon de profondeur.  Les développeurs d’applications peuvent utiliser ces outils pour s’assurer que la profondeur est correctement définie.  Consultez la documentation pour les outils de l’application.

### <a name="using-planar-reprojection"></a>Utilisation de la reprojection planaire
> [!NOTE]
> Pour les casques immersifs sur les ordinateurs de bureau, la définition d’un plan de stabilisation est généralement moins productive, car elle offre moins de qualité visuelle que le fait de fournir le tampon de profondeur de votre application au système pour permettre une reprojection basée sur la profondeur par pixel. À moins d’être exécuté sur un HoloLens, vous devez généralement éviter de définir le plan de stabilisation.

![Plan de stabilisation pour les objets 3D](images/stab-plane-500px.jpg)

L’appareil tente automatiquement de choisir ce plan, mais l’application doit vous aider en sélectionnant le point de focus dans la scène. Les applications Unity qui s’exécutent sur un HoloLens doivent choisir le meilleur point de focalisation en fonction de votre scène et la passer dans [SetFocusPoint ()](focus-point-in-unity.md). Un exemple de définition du point de focus dans DirectX est inclus dans le modèle de cube à rotation par défaut.

Unity envoie votre tampon de profondeur à Windows pour permettre une reprojection par pixel quand vous exécutez votre application sur un casque immersif connecté à un PC de bureau, ce qui offre une meilleure qualité d’image sans un travail explicite par l’application. Vous ne devez fournir un point de focus que lorsque votre application s’exécute sur un HoloLens ou que la reprojection par pixel sera remplacée.


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

Le positionnement du point de concentration dépend en grande partie de ce que l’hologramme examine. L’application a le vecteur de pointage pour référence et le concepteur d’applications sait à quel contenu il souhaite que l’utilisateur observe.

La seule chose la plus importante qu’un développeur puisse faire pour stabiliser des hologrammes est son rendu à 60 FPS. La chute inférieure à 60 FPS réduit considérablement la stabilité des hologrammes, quelle que soit l’optimisation du plan de stabilisation.

**Meilleures pratiques** Il n’existe pas de méthode universelle pour configurer le plan de stabilisation et il est spécifique à l’application. Notre recommandation principale est d’expérimenter et de voir ce qui convient le mieux à votre scénario. Toutefois, essayez d’aligner le plan de stabilisation avec autant de contenu que possible, car tout le contenu de ce plan est parfaitement stabilisé.

Par exemple :
* Si vous disposez uniquement d’un contenu planaire (lecture de l’application de lecture vidéo), alignez le plan de stabilisation avec le plan qui contient votre contenu.
* Si trois petites sphères sont verrouillées dans le monde, faites en sorte que le plan de stabilisation soit « coupé » par le biais des centres de tous les sphères actuellement dans la vue de l’utilisateur.
* Si votre scène a du contenu à des profondeurs sensiblement différentes, privilégiez les autres objets.
* Veillez à ajuster le point de stabilisation chaque cadre pour qu’il coïncide avec l’hologramme que l’utilisateur regarde.

**Éléments à éviter** Le plan de stabilisation est un outil formidable pour obtenir des hologrammes stables, mais en cas d’utilisation inutilisée, cela peut entraîner une sérieuse instabilité de l’image.
* Ne pas « déclencher et oublier ». Vous pouvez vous retrouver avec le plan de stabilisation derrière l’utilisateur ou attaché à un objet qui n’est plus dans la vue de l’utilisateur. Assurez-vous que le plan de stabilisation normal est défini en regard de caméra-Forward (par exemple,-Camera. Forward).
* Ne modifiez pas rapidement le plan de stabilisation entre les extrêmes
* Ne laissez pas le plan de stabilisation défini sur une distance/orientation fixe
* Ne laissez pas le plan de stabilisation passer par l’utilisateur
* Ne définissez pas le point de focus lorsqu’il s’exécute sur un PC de bureau plutôt qu’un HoloLens, et recourez plutôt à une reprojection basée sur la profondeur par pixel.

## <a name="color-separation"></a>Séparation des couleurs 

En raison de la nature des affichages HoloLens, un artefact appelé « séparation des couleurs » peut parfois être perçu. Il se manifeste en tant qu’image séparant les couleurs de base individuelles (rouge, vert et bleu). L’artefact peut être particulièrement visible quand vous affichez des objets blancs, car ils ont de grandes quantités de rouge, de vert et de bleu. Elle est la plus prononcée lorsqu’un utilisateur effectue un suivi visuel d’un hologramme qui se déplace sur l’image holographique à grande vitesse. Une autre façon dont l’artefact peut manifester est la déformation/déformation des objets. Si un objet a un contraste élevé et/ou des couleurs pures, comme le rouge, le vert, le bleu, la séparation des couleurs sera perçue comme déviation des différentes parties de l’objet.

**Exemple de ce à quoi peut ressembler la séparation des couleurs d’un curseur blanc en tête verrouillé à mesure qu’un utilisateur fait pivoter son en-tête sur le côté :**

![Exemple de ce à quoi peut ressembler la séparation des couleurs d’un curseur blanc en tête verrouillé à mesure qu’un utilisateur fait pivoter son en-tête sur le côté.](images/colorseparationofroundwhitecursor-300px.png)

Bien qu’il soit difficile d’éviter complètement la séparation des couleurs, plusieurs techniques sont disponibles pour y remédier.

**La séparation des couleurs peut être observée sur :**
* Objets qui se déplacent rapidement, y compris les objets verrouillés en tête tels que le [curseur](cursors.md).
* Objets qui sont largement éloignés du [plan de stabilisation](hologram-stability.md#reprojection).

**Pour atténuer les effets de la séparation des couleurs :**
* Faites en sorte que l’objet retarde le regard de l’utilisateur. Elle doit apparaître comme si elle avait une certaine inertie et est attachée au point de regard « sur les ressorts ». Cette approche ralentit le curseur (ce qui réduit la distance de séparation) et le met derrière le point de regard probable de l’utilisateur. Tant qu’il rattrape rapidement l’utilisateur lorsque l’utilisateur cesse de décaler le regard, il pense naturellement.
* Si vous ne souhaitez pas déplacer un hologramme, essayez de conserver sa vitesse de mouvement en dessous de 5 degrés/seconde si vous pensez que l’utilisateur la suivra avec ses yeux.
* Utilisez *Light* au lieu de *Geometry* pour le curseur. Une source d’éclairage virtuel attachée au point de regard est perçue comme un pointeur interactif, mais n’entraîne pas de séparation des couleurs.
* Ajustez le plan de stabilisation pour qu’il corresponde aux hologrammes auxquels l’utilisateur est Gazing.
* Rendez l’objet rouge, vert ou bleu.
* Basculez vers une version floue du contenu. Par exemple, un curseur blanc rond peut être remplacé par une ligne légèrement floue dans le sens du mouvement.

Comme précédemment, le rendu à 60 FPS et la définition du plan de stabilisation sont les techniques les plus importantes pour la stabilité des hologrammes. En cas de séparation sensible des couleurs, vérifiez d’abord que la fréquence d’images répond aux attentes.

## <a name="see-also"></a>Voir aussi
* [Comprendre les performances de la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Couleurs, éclairage et matériaux](color,-light-and-materials.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Stabilisation de l’hologramme MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/hologram-stabilization.html)
