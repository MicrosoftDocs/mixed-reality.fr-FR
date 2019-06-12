---
title: Systèmes de coordonnées
description: Les systèmes de coordonnées spatiales permet de générer assis, debout, salle à l’échelle et à l’échelle du monde mixte réalité expériences.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: système de coordonnées, système de coordonnées spatial, orientation, à l’échelle en place et seule permanent à l’échelle, salle-échelle, mise à l’échelle mondiale, assis à 360 degrés, debout, salle, monde, mise à l’échelle, position, orientation, fixe, attaché, étape, ancre, ancre spatiale, World-verrouillé, verrouillage world, body-verrouillée, verrouillage de corps, limites, persistance, partage, suivi de la perte, cloud spatiale d’ancrage
ms.openlocfilehash: f4b945a3ffb83b9ac0a94e0d793a19939aece3bb
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829863"
---
# <a name="coordinate-systems"></a>Systèmes de coordonnées

En son cœur, mixte sur place les applications de réalité [hologrammes](hologram.md) dans votre monde dont l’apparence et des objets réels vous semble. Cela implique le positionnement et l’orientation des ces hologrammes dans des lieux dans le monde qui sont significatives pour l’utilisateur, si le monde est leur espace physique ou un domaine virtuel que vous avez créé avec précision. Quand un peu de la position et l’orientation de votre hologrammes ou n’importe quelle autre géométrie comme le [les regards](gaze.md) ray ou [main positions](gestures.md), Windows fournit divers systèmes de coordonnées réels dans laquelle géométrie peut être exprimée, connu sous le nom **des systèmes de coordonnées spatiales**.

<br>

>[!VIDEO https://www.youtube.com/embed/TneGSeqVAXQ]

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="40%" />
    <col width="20%" />
    <col width="20%" />
    <col width="20%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1er gen)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td><a href="coordinate-systems.md#stationary-frame-of-reference">Système de référence stationnaire</a></td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td><a href="coordinate-systems.md#attached-frame-of-reference">Jointe de référence</a></td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td><a href="coordinate-systems.md#stage-frame-of-reference">Phase de référence</a></td>
        <td>Pas encore pris en charge</td>
        <td>Pas encore pris en charge</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td><a href="coordinate-systems.md#spatial-anchors">Ancres spatiales</a></td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td><a href="spatial-mapping.md">Mappage spatial</a></td>
        <td>✔️</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="mixed-reality-experience-scales"></a>Échelles d’expérience de réalité mixte

Applications de réalité mixte peuvent concevoir d’une large gamme d’expériences utilisateur, à partir des visionneuses de vidéo à 360 degrés juste besoin orientation du casque, à complète world-applications à l’échelle et de jeux, qui doivent mappage spatial et ancres spatiales :
<br>

| Expérience mise à l’échelle | Configuration requise | Expérience de l’exemple | 
|----------|----------|----------|
|  **Orientation-only** |  **Orientation de casque** (gravité aligné) |  Visionneuse de vidéo à 360° | 
|  **Seated-scale** |  Ci-dessus, plus **position casque** par rapport à la position zéro |  Simulateur de jeu ou votre espace de course | 
|  **Permanent à l’échelle** |  Ci-dessus, plus **étape d’origine de l’étage** |  Jeu d’action où vous volante des fous et d’en place  | 
|  **Échelle de la salle** |  Ci-dessus, plus **polygone de limites de phase** |  Jeu de puzzle où vous partez du puzzle | 
|  **À l’échelle mondiale** |  **Ancres spatiales** (en général [mappage spatial](spatial-mapping.md)) |  Jeu avec ennemis provenant de votre murs réels, tel que [RoboRaid](https://www.microsoft.com/p/roboraid/9nblggh5fv3j) | 

Ces expérience échelles suivent un modèle « imbrication poupées ». Le principe de conception clés ici pour la réalité mixte Windows est qu’un casque donné prend en charge les applications conçues pour une expérience de mise à l’échelle les cible, ainsi que tout moindre échelles :
<br>

| Suivi de 6DOF | Floor défini | 360° de suivi | Limites définies | Ancres spatiales | Expérience de max | 
|----------|----------|----------|----------|----------|----------|
|  Non |  - |  - |  - |  - |  **Orientation-only** | 
|  **Oui** |  Non |  - |  - |  - |  **En place** | 
|  **Oui** |  **Oui** |  Non |  - |  - |  **Permanent - progression** | 
|  **Oui** |  **Oui** |  **Oui** |  Non |  - |  **Debout - 360°** | 
|  **Oui** |  **Oui** |  **Oui** |  **Oui** |  Non |  **Salle** | 
|  **Oui** |  **Oui** |  **Oui** |  **Oui** |  **Oui** |  **World** | 

Notez que la phase de référence n’est pas encore possible sur HoloLens. Une application de l’échelle de l’espace sur HoloLens doit actuellement utiliser [mappage spatial](spatial-mapping.md) pour trouver l’utilisateur floor et walls.

## <a name="spatial-coordinate-systems"></a>Systèmes de coordonnées spatiales

Utilisent toutes les applications graphiques 3D [systèmes de coordonnées cartésiennes](https://docs.microsoft.com/windows/uwp/graphics-concepts/coordinate-systems) de raisonner sur les positions et les orientations d’objets dans les mondes virtuels leur rendu. Ces systèmes de coordonnées établir 3 axes perpendiculaires le long duquel positionner les objets : un axe X, Y et Z.

Dans [une réalité mixte](mixed-reality.md), vos applications seront analyser les systèmes de coordonnées physiques et virtuels. Windows appelle un système de coordonnées ayant une signification réelle dans le monde physique un **système de coordonnées spatial**.

Les systèmes de coordonnées spatiales exprimer leurs valeurs de coordonnées en mètres. Cela signifie que les objets placés 2 unités distantes soit x, l’axe Y ou Z apparaîtra 2 mètres indépendamment les uns des autres lors du rendu en réalité mixte. Cela vous permet de restituer facilement des objets et des environnements à grande échelle du monde réel.

En règle générale, les systèmes de coordonnées cartésiennes peuvent être droitier ou gaucher. Les systèmes de coordonnées spatiales sur Windows sont toujours droitiers, ce qui signifie que la valeur positive l’axe des x pointant vers la droite, l’axe y positif pointe vers le haut (aligné sur la gravité) et la valeur positive z pointant vers vous.

Dans les deux types de systèmes de coordonnées, la valeur positive l’axe des x pointant vers la droite et l’axe y positif pointe vers le haut. La différence est que l’axe z positif pointe vers ou à vous. Vous pouvez mémoriser la direction dans laquelle l’axe z positif pointe en pointant les doigts d’un de votre gauche ou la droite dans la valeur positive X direction et les utiliser curl pour l’axe Y positif. La direction de votre curseur pointe, rapprochez ou éloignez vous, est la direction dans laquelle les points de l’axe z positif pour ce système de coordonnées.

## <a name="building-an-orientation-only-or-seated-scale-experience"></a>Création d’une expérience de l’orientation uniquement ou à l’échelle en place

La clé au holographic [rendu](rendering.md) évolue de vue de votre application de son hologrammes chaque frame comme l’utilisateur se déplace, pour correspondre à leur déplacement de la tête prédite. Vous pouvez générer **à l’échelle en place des expériences** qu’égard change à la position de tête de l’utilisateur et l’orientation principale à l’aide un **de référence stationnaire**.

Certains contenus doit ignorer les mises à jour de la position de tête, rester fixe à un en-tête choisi et la distance à partir de l’utilisateur à tout moment. L’exemple principal est à 360 degrés vidéo : étant donné que la vidéo est capturée à partir d’une seule perspective fixe, il serait endommager l’illusion de la position de la vue déplacer relative au contenu, même si l’orientation de la vue doit changer comme l’utilisateur recherche. Vous pouvez générer ces **expériences orientation seule** à l’aide un **attaché de référence**.

### <a name="stationary-frame-of-reference"></a>Système de référence stationnaire

Le système de coordonnées fourni par un système de référence stationnaire s’efforce de maintenir les positions des objets à proximité de l’utilisateur comme stable que possible par rapport à l’environnement, tout en respectant les modifications apportées à la position de tête de l’utilisateur.

Pour des expériences de l’échelle en place dans un moteur de jeu comme [Unity](https://unity3d.com/), un système de référence stationnaire est ce qui définit « monde l’origine. » du moteur Les objets qui sont placés en une coordonnée du monde spécifique utilisent le système de référence stationnaire pour définir leur position dans le monde réel à l’aide de ces mêmes coordonnées. Contenu qui reste placé dans le monde, même lorsque l’utilisateur, est appelé **verrouillé de monde** contenu.

Une application crée généralement un système de référence stationnaire au démarrage et utilise son système de coordonnées tout au long de durée de vie de l’application. En tant que développeur d’applications dans Unity, vous êtes prêt à placer le contenu relatif à l’origine, ce qui sera à la position principale initiale et l’orientation de l’utilisateur. Si l’utilisateur se déplace vers un nouvel emplacement et souhaite continuer leur expérience à l’échelle en place, vous pouvez recentrer l’origine du monde entier à cet emplacement.

Au fil du temps, comme le système apprend plus sur l’environnement utilisateur, il peut déterminer que les distances entre les différents points dans le monde réel sont plus court ou plus longue que le système de croire précédemment. Si vous effectuez le rendu hologrammes dans un système de référence stationnaire pour une application sur HoloLens où les utilisateurs divaguer au-delà de la zone large d’environ 5 mètres, votre application peut observer une dérive dans l’emplacement observée de ces hologrammes. Si votre expérience a des utilisateurs dont y au-delà de 5 mètres, vous créez un [à l’échelle du monde expérience](#building-a-world-scale-experience), ce qui nécessitera des techniques supplémentaires pour conserver les hologrammes stable, comme décrit ci-dessous.

### <a name="attached-frame-of-reference"></a>Jointe de référence

Un cadre de référence jointe se déplace avec l’utilisateur tandis qu’ils autour, avec un titre fixe défini lors de l’application crée d’abord le frame. Cela permet à l’utilisateur confortablement regardez autour de contenu placé dans ce cadre de référence. Le contenu restitué de cette façon relatifs à un utilisateur est appelé **body-verrouillée** contenu.

Lorsque le casque ne peut pas déterminer où il est dans le monde, un cadre de référence jointe fournit le seul système de coordonnées qui peut être utilisé pour restituer hologrammes. Cette solution est idéale pour l’affichage de l’interface utilisateur de secours pour indiquer à l’utilisateur que son appareil ne peut pas se retrouver dans le monde. Les applications qui sont en place à l’échelle ou une version ultérieure doivent inclure un secours orientation uniquement pour aider l’utilisateur à commencer à nouveau, avec l’interface utilisateur similaire à celle illustrée à la [Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md).

## <a name="building-a-standing-scale-or-room-scale-experience"></a>Création d’une expérience permanent à l’échelle ou d’échelle de la salle

Pour aller au-delà d’assis-mise à l’échelle sur un casque immersif et générer un **permanent à l’échelle expérience**, vous pouvez utiliser la **phase de référence**.

Pour fournir un **expérience de l’échelle de la salle**, ce qui permet les utilisateurs Parcourir dans la limite de 5-compteur ils prédéfinis, vous pouvez vérifier **limites à l’étape** ainsi.

### <a name="stage-frame-of-reference"></a>Phase de référence

Lorsque vous configurez tout d’abord un casque immersif, l’utilisateur définit un **étape**, qui représente l’espace dans lequel ils seront confrontés une réalité mixte. L’étape définit au minimum un **origine à l’étape**, un système de coordonnées spatial centré à l’utilisateur de choisi position d’étage et orientation vers l’avant, où il a l’intention d’utiliser l’appareil. En plaçant le contenu dans ce système de coordonnées étape au niveau du plan d’étage Y = 0, vous pouvez Vérifiez votre hologrammes apparaissent confortablement sur le sol lorsque l’utilisateur est permanent, offrant aux utilisateurs un **permanent à l’échelle expérience**.

### <a name="stage-bounds"></a>Limites de la scène

L’utilisateur peut également définir **limites à l’étape**, une zone dans l’espace qui leur ont effacées meuble où ils souhaitent déplacer dans une réalité mixte. Si, par conséquent, l’application peut générer un **expérience de l’échelle de la salle**, à l’aide de ces limites pour vous assurer que hologrammes sont toujours placées dans lequel l’utilisateur peut y accéder.

Étant donné que la phase de référence fournit la que correction d’un seul système de coordonnées dans lequel placer le contenu de l’étage relatif, il est le chemin le plus simple pour portage permanent à l’échelle et des applications à l’échelle de la salle développées pour les casques de réalité virtuelle. Toutefois, comme avec ces plateformes de réalité virtuelle, un seul système de coordonnées peut uniquement se stabiliser contenu dans sur un diamètre égal à 5 mètres (16 pied), avant les bras de levier entraîner l’échec contenu loin d’être le centre de décalage sensiblement comme ajuste le système. Pour aller au-delà de 5 mètres, ancres spatiales sont nécessaires.

## <a name="building-a-world-scale-experience"></a>Création d’une expérience à l’échelle mondiale

True permet de HoloLens **expériences à l’échelle du monde** qui permettent aux utilisateurs divaguer au-delà de 5 mètres. Pour générer une application à l’échelle mondiale, vous aurez besoin de nouvelles techniques plus de ceux utilisés pour des expériences de l’échelle de la salle.

### <a name="why-a-single-rigid-coordinate-system-cannot-be-used-beyond-5-meters"></a>Pourquoi un système de coordonnées rigid unique ne peut pas être utilisé au-delà de 5 mètres

Aujourd'hui, lorsque vous écrivez des jeux, des applications de visualisation de données ou des applications de réalité virtuelle, la classique consiste à établir un système de coordonnées universelles absolues toutes les autres coordonnées peuvent mapper fiable vers. Dans cet environnement, vous pouvez toujours trouver une transformation stable qui définit une relation entre deux objets dans ce monde. Si vous n’avez pas déplacer ces objets, leurs transformations relatives toujours reste le même. Ce système de coordonnées de global fonctionne correctement lors du rendu d’un monde purement virtuel où vous connaissez tous de la géométrie à l’avance. Aujourd'hui, salle à l’échelle des applications VR établissent généralement ce type de système de coordonnées absolu salle à l’échelle avec son origine sur le sol.

En revanche, un appareil de réalité mixte librement telles que HoloLens a une compréhension piloté par les capteurs dynamique du monde, ajuster en permanence ses connaissances au fil du temps de l’environnement de l’utilisateur tandis qu’ils mètres nombreuses entre un étage d’un bâtiment entier. Dans une expérience à l’échelle mondiale, si vous avez placé tous vos hologrammes dans un système de coordonnées rigid unique, ces hologrammes seraient nécessairement dérives au fil du temps, par rapport au monde ou entre eux.

Par exemple, le casque peut croire actuellement deux emplacements dans le monde entier pour être 4 mètres uns des autres et ensuite affiner ultérieurement cette compréhension, que les emplacements sont en fait des compteurs 3.9 éloignés de formation. Si ces hologrammes étaient initialement placées 4 mètres uns des autres dans un système de coordonnées rigid unique, un d’eux puis toujours apparaîtrait 0,1 mètres du monde réel.

### <a name="spatial-anchors"></a>Ancres spatiales

Réalité mixte Windows résout le problème décrit dans la section précédente, en vous permettant de créer [ancres spatiales](spatial-anchors.md) pour marquer des points importants dans le monde où l’utilisateur a placé hologrammes. Un point d’ancrage spatial représente un point important dans le monde que le système doit effectuer le suivi au fil du temps.

Comme l’appareil s’informe sur le monde, ces points d’ancrage spatiales peuvent ajustent leur position par rapport à l’autre en fonction des besoins pour vous assurer que chaque point d’ancrage reste précisément où il a été placé par rapport au monde réel. En plaçant une ancre de spatial à l’emplacement où l’utilisateur place un hologramme et puis en positionnant ce hologramme par rapport à son ancre spatiale, vous pouvez vous assurer que l’hologramme conserve une stabilité optimale, même lorsque l’utilisateur se déplace sur des dizaines de mètres.

Cet ajustement continu d’ancres spatiales par rapport à l’autre est la principale différence entre coordinate systems à partir de points d’ancrage spatiales et images de référence STATIONNAIRES :

* Hologrammes placés dans le système de référence stationnaire tous les conservent une relation rigide entre eux. Toutefois, lorsque l’utilisateur longues distances, système de coordonnées de celle de l’image peut dérives par rapport au monde pour vous assurer que hologrammes en regard de l’utilisateur apparaissent stables.

* Hologrammes placés dans la phase de référence également conservent une relation rigide entre eux. Contrairement à l’image fixe, le frame de la phase toujours reste fixe par rapport à son origine physique défini. Toutefois, le contenu restitué dans le système de coordonnées de la scène au-delà de sa limite de 5-compteur apparaîtra seulement stable alors que l’utilisateur est permanent au sein de cette limite.

* Hologrammes placées à l’aide d’une ancre spatial peut dérives par rapport à hologrammes placé à l’aide d’un autre point d’ancrage spatiale. Cela permet à Windows améliorer la compréhension de la position de chaque point d’ancrage spatiale, même si, par exemple, un point d’ancrage doit ajuster lui-même gauche et un autre point d’ancrage doit ajuster vers la droite.

Contrairement à un système de référence stationnaire, qui optimise toujours de stabilité près de l’utilisateur, la phase de référence et les ancres spatiales garantissent la stabilité près de leurs origines. Cela permet à ces hologrammes demeurer précisément en place au fil du temps, mais cela signifie également que hologrammes rendus trop loin à partir de l’origine de leur système coordonnées seront confrontés à des effets de plus en plus graves levier-arm. Il s’agit, car de légères modifications à la position et l’orientation de la scène ou d’un point d’ancrage sont amplifient encore proportionnelle à la distance à partir de ce point d’ancrage. 

Une règle empirique consiste à vous assurer que quoi que ce soit rendu selon le système de coordonnées de l’une ancre spatial éloigné se trouve dans environ 3 mètres de son origine. Pour une origine de scène à proximité, rendre le contenu distant est OK, car toute erreur positionnelle accrue affecte seulement les petites hologrammes qui ne sont pas décalés une grande partie de la vue.

### <a name="spatial-anchor-persistence"></a>Persistance de l’ancre spatial

Ancres spatiales peuvent permettent également de votre application à mémoriser un emplacement important même après que votre application s’interrompt ou de l’appareil est arrêté.

Vous pouvez enregistrer les ancres spatiales crée votre application de disque et puis chargez-les revenir plus tard, en rendant persistant vers votre application **Boutique spatial**. Lors de l’enregistrement ou du chargement d’un point d’ancrage, vous fournissez une clé de chaîne qui est significative pour votre application, afin d’identifier le point d’ancrage plus tard. Considérez cette clé comme le nom de fichier pour votre point d’ancrage. Si vous souhaitez associer les autres données qui sont ancrés, tels qu’un modèle 3D placé par l’utilisateur à cet emplacement, enregistre dans le stockage local de votre application et l’associer à la clé que vous avez choisi.

Par ancres persistantes dans le magasin, vos utilisateurs peuvent placer hologrammes individuels ou placer un espace de travail autour de laquelle une application placer ses hologrammes différents et recherchez ces hologrammes ultérieurement où ils attendent, au fil de nombreuses utilisations de votre application.

Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour la persistance hologramme asynchrone sur HoloLens, appareils iOS et Android.  En partageant une ancre spatial cloud durable, plusieurs périphériques peuvent observer l’hologramme persistante même au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.

### <a name="spatial-anchor-sharing"></a>Partage d’ancrage spatial

Votre application peut également partager un point d’ancrage spatiale en temps réel avec d’autres appareils, ce qui permet en temps réel partagé des expériences.

À l’aide de <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a>, votre application peut partager un point d’ancrage spatial entre plusieurs HoloLens, appareils iOS et Android. En demandant à chaque appareil de restituer un hologramme à l’aide de l’ancre spatial même, tous les utilisateurs voient l’hologramme apparaissent au même endroit dans le monde réel.

## <a name="avoid-head-locked-content"></a>Éviter la tête verrouillée de contenu

Nous vous déconseillons fortement de restituer le contenu de tête verrouillée, ce qui reste à un point fixe dans l’affichage (par exemple, un HUD). En règle générale, contenu de tête verrouillée est désagréable pour les utilisateurs et ne pas semble un dans le cadre de leur univers.

Contenu de tête verrouillée doit généralement être remplacé par hologrammes qui sont attachés à l’utilisateur ou placés dans le monde lui-même. Par exemple, [curseurs](cursors.md) doit généralement être transférée dans le monde, mise à l’échelle naturellement pour refléter la position et la distance de l’objet sous le regard de l’utilisateur.

## <a name="handling-tracking-errors"></a>Gestion des erreurs de suivi

Dans certains environnements tels que des couloirs foncées, il peut-être pas possible pour un casque à l’aide de suivi intégrale lui-même localiser correctement dans le monde. Cela peut entraîner des hologrammes apparaître ou apparaître dans des lieux incorrect si pas correctement traités. Nous abordons maintenant les conditions dans lesquelles cela peut se produire, son impact sur l’expérience utilisateur, et des conseils pour mieux gérant cette situation.

### <a name="headset-cannot-track-due-to-insufficient-sensor-data"></a>Casque ne peut pas effectuer le suivi en raison de données de capteur insuffisant

Parfois, les capteurs du casque ne sont pas en mesure de déterminer où le casque est. Cela peut se produire si la pièce est sombre, si les capteurs sont couverts par les cheveux ou mains, ou si l’environnement n’ont pas de suffisamment de texture.

Dans ce cas, le casque ne pourront pas être effectuer le suivi de sa position avec suffisamment de précision pour restituer hologrammes verrouillé de monde. Vous ne pourrez pas déterminer où une ancre spatiale, un frame stationnaire ou un cadre de l’étape est relatif à l’appareil, mais vous pouvez toujours afficher verrouillé de corps de contenu dans le cadre de référence jointe.

Votre application doit indiquer à l’utilisateur comment obtenir la position de suivi, rendu du contenu verrouillé de corps de secours qui présente des conseils, telles que dévoilant les capteurs et en activant les lumières plus.

### <a name="headset-tracks-incorrectly-due-to-dynamic-changes-in-the-environment"></a>Casque effectue le suivi de manière incorrecte en raison de modifications dynamiques dans l’environnement

Parfois, l’appareil ne peut pas suivre correctement s’il existe un grand nombre de modifications dynamiques dans l’environnement, telles que de nombreuses personnes vous épargne dans la salle. Dans ce cas, les hologrammes semblent accéder ou dérive car l’appareil tente d’effectuer le suivi de lui-même dans cet environnement dynamique. Nous recommandons à l’aide de l’appareil dans un environnement moins dynamique si vous rencontrez ce scénario.

### <a name="headset-tracks-incorrectly-because-the-environment-has-changed-significantly-over-time"></a>Casque effectue le suivi de manière incorrecte, car l’environnement a changé considérablement au fil du temps

Parfois, lorsque vous démarrez à l’aide d’un casque dans un environnement ayant subi beaucoup de modifications (par exemple le mouvement significatif de mobilier, porte-manteaux etc.), il est possible que certains hologrammes peuvent apparaître décalées depuis leur emplacement d’origine. Les hologrammes antérieures peuvent également passez à une autre que l’utilisateur se déplace dans ce nouvel espace. Il s’agit, car compréhension du système de votre espace ne conserve plus et il essaie de remapper l’environnement lorsqu’il tente de réconcilier les fonctionnalités de la salle. Dans ce scénario, il est conseillé d’encourager les utilisateurs à ré-placer hologrammes, qu’ils épinglées dans le monde si elles ne s’affichent pas emplacement attendu.

### <a name="headset-tracks-incorrectly-due-to-identical-spaces-in-an-environment"></a>Casque effectue le suivi de manière incorrecte en raison des espaces identiques dans un environnement

Parfois, une maison ou autres espace peut avoir deux domaines identiques. Par exemple, deux salles de conférence identiques, deux identiques coin inférieur droit des zones, deux schémas identiques de grande taille qui couvrent le champ de vision de l’appareil. Dans de tels scénarios, l’appareil peut, dans certains cas, perturbés entre les parties identiques et marquez-les comme étant le même que dans sa représentation interne. Cela peut entraîner les hologrammes à partir de certaines zones à apparaître dans d’autres emplacements. L’appareil peut commencer à perdre suivi souvent dans la mesure où sa représentation interne de l’environnement a été endommagée. Dans ce cas, il est conseillé de réinitialiser la compréhension de l’environnement du système. Veuillez noter que la réinitialisation de la carte entraîne une perte de tous les emplacements spatiale d’ancrage. Cela entraîne le casque suivre correctement dans les domaines uniques de l’environnement. Toutefois, le problème peut se ré-produire si l’appareil obtient confondu entre les zones d’identiques.

## <a name="see-also"></a>Voir aussi
* [Présentation de GDC 2017 sur les systèmes de coordonnées spatiales et rendu HOLOGRAPHIQUE](https://channel9.msdn.com/events/GDC/GDC-2017/GDC2017-008)
* [Systèmes de coordonnées dans Unity](coordinate-systems-in-unity.md)
* [Systèmes de coordonnées dans DirectX](coordinate-systems-in-directx.md)
* [Ancres spatiales](spatial-anchors.md)
* [Expériences partagées dans Mixed Reality](shared-experiences-in-mixed-reality.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>
* [Étude de cas - parcourant des trous dans la réalité](case-study-looking-through-holes-in-your-reality.md)
