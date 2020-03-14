---
title: Systèmes de coordonnées
description: Les systèmes de coordonnées spatiales utilisés pour créer des expériences de réalité mixte assiste, debout, à l’échelle de la place et à l’échelle mondiale.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: système de coordonnées, système de coordonnées spatiales, orientation uniquement, à l’échelle assise, à l’échelle debout, à l’échelle de la pièce, à l’échelle mondiale, 360 de degrés, assis, debout, salle, monde, échelle, position, orientation, stationnaire, attaché, étage, Ancre, ancrage spatial, verrouillage universel, verrouillage universel, verrouillage du corps, verrouillage du corps, limites, persistance, partage, perte de suivi, ancrage spatial Cloud
ms.openlocfilehash: 228f46f1962c39012571234da47ccec07aa67118
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375636"
---
# <a name="coordinate-systems"></a>Systèmes de coordonnées

À leur cœur, les applications de réalité mixte placent des [hologrammes](hologram.md) dans votre monde qui ressemblent à des objets réels. Cela implique de positionner et d’orienter précisément ces hologrammes à des endroits du monde qui sont significatifs pour l’utilisateur, qu’il s’agisse de son espace physique ou d’un domaine virtuel que vous avez créé. Lorsque vous pensez à la position et à l’orientation de vos hologrammes, ou à toute autre géométrie telle que les positions [de rayons ou](gaze-and-commit.md) de [main](hands-and-tools.md), Windows fournit divers systèmes de coordonnées réalistes dans lesquels cette géométrie peut être exprimée, appelée **systèmes de coordonnées spatiales**.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/TneGSeqVAXQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

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
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td><a href="coordinate-systems.md#stationary-frame-of-reference">Cadre de référence stationnaire</a></td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td><a href="coordinate-systems.md#attached-frame-of-reference">Cadre de référence attaché</a></td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td><a href="coordinate-systems.md#stage-frame-of-reference">Cadre de la phase de référence</a></td>
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
    <tr>
        <td><a href="scene-understanding.md">Compréhension des scènes</a></td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="mixed-reality-experience-scales"></a>Évolution de l’expérience de réalité mixte

Les applications de réalité mixte peuvent concevoir une large gamme d’expériences utilisateur, à partir de visionneuses vidéo de 360 degrés qui ont juste besoin de l’orientation du casque, à des applications et des jeux à l’échelle mondiale, qui nécessitent un mappage spatial et des ancres spatiales :
<br>

| Mise à l’échelle | Configuration requise | Exemple d’expérience | 
|----------|----------|----------|
|  **Orientation uniquement** |  **Orientation du casque** (alignée en gravité) |  visionneuse vidéo 360 ° | 
|  **À l’échelle assise** |  Ci-dessus, plus la **position du casque** par rapport à la position zéro |  Jeu de course ou simulateur d’espace | 
|  **À l’échelle debout** |  Ci-dessus, plus l’origine de l' **étage** |  Jeu d’action dans lequel vous avez des canards et une densité  | 
|  **Mise à l’échelle de l’espace** |  Ci-dessus, plus les limites de la **phase Polygon** |  Jeu de puzzle dans lequel vous parcourez le puzzle | 
|  **À l’échelle mondiale** |  **Ancres spatiales** (et généralement le [mappage spatial](spatial-mapping.md)) |  Jeu avec des ennemis provenant de vos murs réels, tels que [RoboRaid](https://www.microsoft.com/p/roboraid/9nblggh5fv3j) | 

Ces possibilités de mise à l’échelle suivent un modèle d’imbrication de poupées. Le principal concept de conception pour Windows Mixed Reality est qu’un casque donné prend en charge les applications conçues pour une mise à l’échelle de l’expérience cible, ainsi que toutes les échelles les plus petites :
<br>

| suivi 6DOF | Défini par l’étage | suivi de 360 ° | Limites définies | Ancres spatiales | Expérience max. | 
|----------|----------|----------|----------|----------|----------|
|  Non |  - |  - |  - |  - |  **Orientation uniquement** | 
|  **Oui** |  Non |  - |  - |  - |  **Positionné** | 
|  **Oui** |  **Oui** |  Non |  - |  - |  **En aval** | 
|  **Oui** |  **Oui** |  **Oui** |  Non |  - |  **Debout-360 °** | 
|  **Oui** |  **Oui** |  **Oui** |  **Oui** |  Non |  **Divertissement** | 
|  **Oui** |  **Oui** |  **Oui** |  **Oui** |  **Oui** |  **Réelles** | 

Notez que le cadre de la phase de référence n’est pas encore pris en charge sur HoloLens. Une application de mise à l’échelle de la place sur HoloLens doit actuellement utiliser le [mappage spatial](spatial-mapping.md) ou la [compréhension des scènes](scene-understanding.md) pour rechercher le plancher et les murs de l’utilisateur.

## <a name="spatial-coordinate-systems"></a>Systèmes de coordonnées spatiales

Toutes les applications graphiques 3D utilisent des [systèmes de coordonnées cartésiens](https://docs.microsoft.com/windows/uwp/graphics-concepts/coordinate-systems) pour expliquer les positions et les orientations des objets dans les mondes virtuels qu’elles affichent. Ces systèmes de coordonnées établissent 3 axes perpendiculaires pour positionner les objets : un axe X, Y et Z.

En [réalité mixte](mixed-reality.md), vos applications ont une raison d’être des systèmes de coordonnées physiques et virtuels. Windows appelle un système de coordonnées qui a une signification réelle dans le système physique de **coordonnées spatiales**.

Les systèmes de coordonnées spatiales expriment leurs valeurs de coordonnées en mètres. Cela signifie que les objets placés 2 unités à l’écart de l’axe X, Y ou Z apparaîtront à 2 mètres l’un de l’autre lorsqu’ils sont rendus en réalité mixte. Cela vous permet de rendre facilement les objets et les environnements à l’échelle du monde réel.

En général, les systèmes de coordonnées cartésiennes peuvent être droitiers ou gauches. Les systèmes de coordonnées spatiales sur les fenêtres sont toujours droitiers, ce qui signifie que les points de l’axe des X positifs à droite, l’axe Y positif pointe vers le haut (aligné sur la gravité) et les points positifs de l’axe Z vers vous.

Dans les deux types de systèmes de coordonnées, l’axe X positif pointe vers la droite et l’axe Y positif pointe vers le haut. La différence est que l’axe Z positif pointe vers vous ou en éloigne. Vous pouvez vous souvenir de la direction vers laquelle pointe l’axe Z positif en pointant les doigts de votre gauche ou de la main droite dans la direction X positive et en les faisant passer à la direction Y positive. La direction vers laquelle votre Thumb pointe, que ce soit vers vous ou en dehors, est la direction dans laquelle les points positifs de l’axe Z pour ce système de coordonnées.

## <a name="building-an-orientation-only-or-seated-scale-experience"></a>Création d’une expérience d’orientation seule ou de mise à l’échelle installée

La clé du [rendu](rendering.md) holographique est la modification de la vue de l’application de ses hologrammes à mesure que l’utilisateur se déplace, afin de faire correspondre le mouvement de l’en-tête prédit. Vous pouvez créer des expériences à l' **échelle assises** qui respectent les modifications apportées à la position des têtes et à l’orientation des têtes de l’utilisateur à l’aide d’un **cadre stationnaire de référence**.

Une partie du contenu doit ignorer les mises à jour de position de l’en-tête, à tout moment résolu à un titre et à une distance choisis. L’exemple principal est la vidéo de 360 degrés : étant donné que la vidéo est capturée à partir d’une perspective fixe unique, l’illusion de la position de la vue doit être déplacée par rapport au contenu, même si l’orientation de la vue doit changer à mesure que l’utilisateur regarde. Vous pouvez générer une telle **expérience d’orientation uniquement** à l’aide d’un **cadre de référence attaché**.

### <a name="stationary-frame-of-reference"></a>Cadre de référence stationnaire

Le système de coordonnées fourni par un cadre stationnaire de référence permet de conserver les positions des objets près de l’utilisateur aussi stables que possible par rapport au monde, tout en respectant les modifications de la position de la tête de l’utilisateur.

Pour les expériences à l’échelle assises dans un moteur de jeu comme [Unity](https://unity3d.com/), une image fixe de référence est ce qui définit la « provenance mondiale » du moteur. Les objets placés à une coordonnée universelle spécifique utilisent le cadre stationnaire de référence pour définir leur position dans le monde réel à l’aide de ces mêmes coordonnées. Le contenu qui reste dans le monde, même au fur et à mesure que l’utilisateur se déplace, est connu sous le nom de contenu **à verrouillage universel** .

Une application crée généralement une image fixe de référence au démarrage et utilise son système de coordonnées tout au long de la durée de vie de l’application. En tant que développeur d’applications dans Unity, vous pouvez simplement commencer à placer du contenu par rapport à l’origine, qui sera à la position et à l’orientation initiales de l’utilisateur. Si l’utilisateur se déplace vers un nouvel emplacement et veut poursuivre son expérience à l’échelle assise, vous pouvez recentrer l’origine du monde à cet emplacement.

Au fil du temps, à mesure que le système apprend davantage sur l’environnement de l’utilisateur, il peut déterminer que les distances entre les différents points du monde réel sont plus courtes ou plus longues que le système n’était supposé. Si vous affichez des hologrammes dans une image de référence fixe pour une application sur HoloLens, où les utilisateurs se dépassent d’une zone d’environ 5 mètres de largeur, votre application peut observer une dérive à l’emplacement observé de ces hologrammes. Si votre expérience a des utilisateurs qui se dépassent de 5 mètres, vous créez une expérience à l' [échelle mondiale](#building-a-world-scale-experience), qui nécessitera des techniques supplémentaires pour garantir la stabilité des hologrammes, comme décrit ci-dessous.

### <a name="attached-frame-of-reference"></a>Cadre de référence attaché

Un cadre de référence attaché se déplace avec l’utilisateur lors de son parcours, avec un en-tête fixe défini lorsque l’application crée d’abord le frame. Cela permet à l’utilisateur de regarder confortablement le contenu placé dans ce cadre de référence. Le contenu rendu dans cette méthode relative à l’utilisateur est appelé contenu **verrouillé** .

Lorsque le casque ne peut pas déterminer où il se trouve dans le monde, un cadre de référence attaché fournit le seul système de coordonnées qui peut être utilisé pour le rendu des hologrammes. Cela permet d’afficher l’interface utilisateur de secours idéale pour indiquer à l’utilisateur que son appareil ne peut pas le trouver dans le monde. Les applications qui sont installées à l’échelle ou supérieures doivent inclure un secours en orientation seule pour aider l’utilisateur à se relancer, avec une interface utilisateur semblable à celle illustrée dans la page d’hébergement de la [réalité mixte](navigating-the-windows-mixed-reality-home.md).

## <a name="building-a-standing-scale-or-room-scale-experience"></a>Création d’une expérience de mise à l’échelle permanente ou à l’échelle de l’espace

Pour aller au-delà de la mise à l’échelle sur un casque immersif et créer une expérience à l' **échelle debout**, vous pouvez utiliser le **cadre de la phase de référence**.

Pour fournir une **expérience**de mise à l’échelle de l’espace, en permettant aux utilisateurs de se déplacer dans la limite de 5 mètres qu’ils prédéfinis, vous pouvez également vérifier les limites du niveau **intermédiaire** .

### <a name="stage-frame-of-reference"></a>Cadre de la phase de référence

Lors de la configuration initiale d’un casque immersif, l’utilisateur définit une **étape**, qui représente la salle dans laquelle il expérimentera la réalité mixte. L’étape définit au minimum un **État d’origine**, un système de coordonnées spatiales centré à la position de plancher choisie par l’utilisateur et l’orientation vers l’avant, où il envisage d’utiliser l’appareil. En plaçant le contenu dans ce système de coordonnées au niveau du plan de plancher Y = 0, vous pouvez vous assurer que vos hologrammes apparaissent confortablement à l’étage lorsque l’utilisateur est debout, ce qui permet aux utilisateurs de bénéficier d’une expérience à l' **échelle debout**.

### <a name="stage-bounds"></a>Limites de la phase

L’utilisateur peut également définir des limites au niveau de la **phase**, une zone de la pièce dans laquelle elles ont été désactivées pour se déplacer dans la réalité mixte. Dans ce cas, l’application peut créer une expérience de mise à l’échelle de l' **espace**, à l’aide de ces limites pour s’assurer que les hologrammes sont toujours placés là où l’utilisateur peut les joindre.

Étant donné que le cadre de la phase de référence fournit un système de coordonnées fixe unique dans lequel placer le contenu relatif à l’étage, il s’agit du chemin le plus simple pour le portage des applications à l’échelle du sol et à l’échelle de l’espace développée pour les casques de réalité virtuelle. Toutefois, comme pour ces plateformes VR, un seul système de coordonnées peut uniquement stabiliser le contenu dans environ un diamètre de 5 mètres (16 pieds de page), avant que les effets du bras de levier n’entraînent une évolution notable du contenu du centre. Pour aller au-delà de 5 mètres, les ancres spatiales sont nécessaires.

## <a name="building-a-world-scale-experience"></a>Création d’une expérience à l’échelle mondiale

HoloLens permet des expériences de mise à l' **échelle au monde** véritables qui permettent aux utilisateurs de dépasser 5 mètres. Pour créer une application à l’échelle mondiale, vous aurez besoin de nouvelles techniques au-delà de celles utilisées pour les expériences à l’échelle de la place.

### <a name="why-a-single-rigid-coordinate-system-cannot-be-used-beyond-5-meters"></a>Pourquoi un système de coordonnées rigides unique ne peut pas être utilisé au-delà de 5 mètres

Aujourd’hui, lors de l’écriture de jeux, d’applications de visualisation de données ou d’applications de réalité virtuelle, l’approche classique consiste à établir un système de coordonnées universel unique sur lequel toutes les autres coordonnées peuvent être mappées de manière fiable. Dans cet environnement, vous pouvez toujours trouver une transformation stable qui définit une relation entre deux objets dans ce monde. Si vous n’avez pas déplacé ces objets, leurs transformations relatives restent toujours les mêmes. Ce type de système de coordonnées global fonctionne bien lors du rendu d’un monde purement virtuel où vous connaissez toute la géométrie à l’avance. Aujourd’hui, les applications de la mise à l’échelle de la salle établissent généralement ce type de système de coordonnées à l’échelle de la pièce, avec son origine sur le plancher.

En revanche, un appareil de réalité mixte non attaché, tel que HoloLens, a une compréhension dynamique pilotée par les capteurs du monde, en ajustant en permanence ses connaissances dans le temps de l’environnement de l’utilisateur lorsqu’il parcourt de nombreux compteurs à travers l’ensemble d’un étage d’un bâtiment. Dans le cas d’une expérience à l’échelle mondiale, si vous avez placé tous vos hologrammes dans un système de coordonnées rigides unique, ces hologrammes se déplaceront nécessairement dans le temps, soit par rapport au monde ou entre eux.

Par exemple, le casque peut considérer deux endroits du monde comme étant séparés de 4 mètres, puis affiner cette compréhension, en sachant que les emplacements sont en fait de 3,9 mètres de distance. Si ces hologrammes avaient initialement été placés à 4 mètres en un seul système de coordonnées rigides, l’un d’eux présenterait toujours 0,1 mètres du monde réel.

### <a name="spatial-anchors"></a>Ancres spatiales

Windows Mixed Reality résout le problème décrit dans la section précédente en vous permettant de créer des [ancres spatiales](spatial-anchors.md) pour marquer des points importants dans le monde où l’utilisateur a placé des hologrammes. Une ancre spatiale représente dans le monde un point important dont le système doit effectuer le suivi au fil du temps.

À mesure que l’appareil apprend sur le monde, ces ancres spatiales peuvent ajuster leur position par rapport à l’autre en fonction des besoins pour s’assurer que chaque ancre reste précisément là où elle a été placée par rapport au monde réel. En plaçant un ancrage spatial à l’emplacement où l’utilisateur place un hologramme, puis en positionnant Cet hologramme par rapport à son ancrage spatial, vous pouvez vous assurer que l’hologramme maintient une stabilité optimale, même lorsque l’utilisateur se déplace sur des dizaines de mètres.

Ce réglage continu des ancrages spatiaux l’un de l’autre est la principale différence entre les systèmes de coordonnées des ancres spatiales et des images fixes de référence :

* Les hologrammes placés dans le cadre stationnaire de référence conservent une relation rigide les uns avec les autres. Toutefois, à mesure que l’utilisateur parcourt de longues distances, le système de coordonnées de ce frame peut dépasser par rapport au monde pour s’assurer que les hologrammes à côté de l’utilisateur semblent stables.

* Les hologrammes placés dans le cadre de la phase de référence conservent également une relation rigide les uns avec les autres. Contrairement à l’image stationnaire, le frame d’étape reste toujours fixe en place par rapport à son origine physique définie. Toutefois, le contenu rendu dans le système de coordonnées de l’étape au-delà de sa limite de 5 mètres n’apparaîtra stable que lorsque l’utilisateur se trouve dans cette limite.

* Les hologrammes placés à l’aide d’une ancre spatiale peuvent être dérives par rapport aux hologrammes placés à l’aide d’une autre ancre spatiale. Cela permet à Windows d’améliorer sa compréhension de la position de chaque ancrage spatial, même si, par exemple, une ancre doit s’ajuster elle-même à gauche et qu’une autre ancre doit s’ajuster à droite.

Contrairement à une image stationnaire de référence qui optimise toujours la stabilité près de l’utilisateur, le cadre de la phase de référence et les ancres spatiales garantissent une stabilité proche de leur origine. Cela permet aux hologrammes de rester précisément en place au fil du temps, mais cela signifie également que les hologrammes rendus trop loin de l’origine de leur système de coordonnées subiront des effets de leviers plus sérieux. Cela est dû au fait que les petits ajustements de la position et de l’orientation de la phase ou de l’ancrage sont agrandis proportionnellement à la distance par rapport à cette ancre. 

Une bonne règle empirique consiste à s’assurer que tout ce que vous restituez en fonction du système de coordonnées d’une ancre spatiale distante est situé à environ 3 mètres de son origine. Dans le cas d’une étape proche, le rendu du contenu distant est OK, car toute erreur de position plus importante affecte uniquement les petits hologrammes qui ne se déplacent pas dans l’affichage de l’utilisateur.

### <a name="spatial-anchor-persistence"></a>Persistance d’ancrage spatial

Les ancres spatiales peuvent également permettre à votre application de mémoriser un emplacement important même après l’interruption de votre application ou l’arrêt de l’appareil.

Vous pouvez enregistrer sur disque les ancres spatiales créées par votre application, puis les charger à nouveau ultérieurement en les rendant persistantes dans le **magasin d’ancrage spatial**de votre application. Lors de l’enregistrement ou du chargement d’une ancre, vous fournissez une clé de chaîne qui est significative pour votre application, afin d’identifier l’ancre ultérieurement. Considérez cette clé comme le nom de fichier de votre point d’ancrage. Si vous souhaitez associer d’autres données à cette ancre, par exemple un modèle 3D que l’utilisateur a placé à cet emplacement, enregistrez-le dans le stockage local de votre application et associez-le à la clé que vous avez choisie.

En conservant les ancres dans le magasin, vos utilisateurs peuvent placer des hologrammes individuels ou placer un espace de travail autour duquel une application place ses différents hologrammes, puis rechercher ces hologrammes plus tard là où ils l’attendent, sur de nombreuses utilisations de votre application.

Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> pour la persistance asynchrone des hologrammes sur les appareils HoloLens, iOS et Android.  En partageant une ancre spatiale cloud durable, plusieurs appareils peuvent observer le même hologramme conservé au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.

### <a name="spatial-anchor-sharing"></a>Partage d’ancrage spatial

Votre application peut également partager une ancre spatiale en temps réel avec d’autres appareils, ce qui permet d’obtenir des expériences partagées en temps réel.

En utilisant des <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres spatiales Azure</a>, votre application peut partager une ancre spatiale sur plusieurs appareils HoloLens, iOS et Android. Quand chaque appareil affiche un hologramme à l’aide de la même ancre spatiale, tous les utilisateurs voient l’hologramme au même endroit dans le monde réel.

## <a name="avoid-head-locked-content"></a>Éviter le contenu verrouillé

Nous vous déconseillons fortement de rendre le contenu verrouillé, qui reste à une position fixe dans l’affichage (par exemple, un HUD). En général, le contenu verrouillé est inconfortable pour les utilisateurs et ne ressemble pas à une partie naturelle de leur monde.

Le contenu verrouillé doit généralement être remplacé par des hologrammes attachés à l’utilisateur ou placés dans le monde lui-même. Par exemple, les [curseurs](cursors.md) doivent généralement être poussés dans le monde entier, avec une mise à l’échelle naturelle pour refléter la position et la distance de l’objet sous le regard de l’utilisateur.

## <a name="handling-tracking-errors"></a>Gestion des erreurs de suivi

Dans certains environnements tels que les couloirs sombres, il n’est pas possible pour un casque utilisant le suivi de l’extérieur de se localiser correctement dans le monde. Cela peut entraîner l’affichage des hologrammes qui ne s’affichent pas ou n’apparaissent pas aux endroits erronés si le traitement est incorrect. Nous évoquons maintenant les conditions dans lesquelles cela peut se produire, son impact sur l’expérience utilisateur et des conseils pour mieux gérer cette situation.

### <a name="headset-cannot-track-due-to-insufficient-sensor-data"></a>Impossible d’effectuer le suivi du casque en raison de données de capteur insuffisantes

Parfois, les capteurs du casque ne sont pas en mesure de déterminer où se trouve le casque. Cela peut se produire si la pièce est sombre, si les capteurs sont couverts par des cheveux ou des mains ou si l’environnement n’a pas suffisamment de texture.

Dans ce cas, le casque n’est pas en mesure d’effectuer le suivi de sa position avec suffisamment de précision pour le rendu des hologrammes à verrouillage universel. Vous ne serez pas en mesure de déterminer l’emplacement d’un point d’ancrage spatial, d’un cadre stationnaire ou d’un cadre intermédiaire par rapport à l’appareil, mais vous pouvez toujours restituer le contenu verrouillé dans le cadre de référence attaché.

Votre application doit indiquer à l’utilisateur comment obtenir le suivi positionnel, en rendant un contenu verrouillé verrouillé qui décrit certains conseils, tels que la récupération des capteurs et l’activation d’autres lumières.

### <a name="headset-tracks-incorrectly-due-to-dynamic-changes-in-the-environment"></a>Le casque suit de manière incorrecte en raison de modifications dynamiques dans l’environnement

Parfois, l’appareil ne peut pas suivre correctement s’il y a beaucoup de modifications dynamiques dans l’environnement, telles que de nombreuses personnes qui se déplacent dans la pièce. Dans ce cas, les hologrammes peuvent sembler sauter ou dérive lorsque l’appareil tente de se suivre dans cet environnement dynamique. Nous vous recommandons d’utiliser l’appareil dans un environnement moins dynamique si vous atteignez ce scénario.

### <a name="headset-tracks-incorrectly-because-the-environment-has-changed-significantly-over-time"></a>Le casque suit de manière incorrecte, car l’environnement a considérablement changé au fil du temps

Parfois, lorsque vous commencez à utiliser un casque dans un environnement qui a subi un grand nombre de modifications (par exemple, un déplacement important de meubles, de points de suspension, etc.), il est possible que certains hologrammes soient décalés de leur emplacement d’origine. Les hologrammes précédents peuvent également sauter au fur et à mesure que l’utilisateur se déplace dans ce nouvel espace. Cela est dû au fait que la compréhension du système de votre espace ne se débloque plus et tente de remapper l’environnement tout en essayant de rapprocher les fonctionnalités de la salle. Dans ce scénario, il est recommandé d’encourager les utilisateurs à réactiver les hologrammes qu’ils ont épinglés dans le monde s’ils n’apparaissent pas là où ils sont attendus.

### <a name="headset-tracks-incorrectly-due-to-identical-spaces-in-an-environment"></a>Le casque suit de manière incorrecte en raison d’espaces identiques dans un environnement

Parfois, un logement ou un autre espace peut avoir deux zones identiques. Par exemple, deux salles de conférence identiques, deux zones d’angle identiques, deux affiches identiques identiques qui couvrent le champ de vision de l’appareil. Dans de tels scénarios, l’appareil peut parfois être confondu entre les parties identiques et les marquer comme étant identiques dans sa représentation interne. Cela peut entraîner l’affichage des hologrammes de certaines zones dans d’autres emplacements. L’appareil peut commencer à perdre souvent le suivi, car sa représentation interne de l’environnement a été endommagée. Dans ce cas, il est recommandé de réinitialiser la compréhension de l’environnement du système. Notez que la réinitialisation de la carte provoque la perte de tous les placements d’ancrage spatial. Cela permet au casque de suivre correctement les zones uniques de l’environnement. Toutefois, le problème peut se produire si l’appareil est à nouveau confondu entre les zones identiques.

## <a name="see-also"></a>Voir aussi
* [Présentation GDC 2017 sur les systèmes de coordonnées spatiales et le rendu holographique](https://channel9.msdn.com/events/GDC/GDC-2017/GDC2017-008)
* [Systèmes de coordonnées dans Unity](coordinate-systems-in-unity.md)
* [Systèmes de coordonnées dans DirectX](coordinate-systems-in-directx.md)
* [Ancres spatiales](spatial-anchors.md)
* [Expériences partagées dans Mixed Reality](shared-experiences-in-mixed-reality.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>
* [Étude de cas - Voir à travers vos objets](case-study-looking-through-holes-in-your-reality.md)
