---
title: Mappage spatial
description: Le mappage spatial fournit une représentation détaillée des surfaces réelles dans l’environnement autour du HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: mappage spatial, HoloLens, réalité mixte, reconstruction de surface, maille
ms.openlocfilehash: 2988056b5caf50a4428d39c725bfe5432867a9c0
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437455"
---
# <a name="spatial-mapping"></a>Mappage spatial

Le mappage spatial fournit une représentation détaillée des surfaces réelles dans l’environnement autour du HoloLens, ce qui permet aux développeurs de créer une expérience de réalité mixte convaincante. En fusionnant le monde réel avec le monde virtuel, une application peut faire paraître des hologrammes réels. Les applications peuvent également être plus naturellement alignées sur les attentes des utilisateurs en fournissant des comportements et des interactions réels et familiers.

<br>

>[!VIDEO https://www.youtube.com/embed/zff2aQ1RaVo]

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
        <td>Mappage spatial</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>


## <a name="why-is-spatial-mapping-important"></a>Pourquoi le mappage spatial est-il important ?

Le mappage spatial permet de placer des objets sur des surfaces réelles. Cela permet d’ancrer les objets dans le monde de l’utilisateur et de tirer parti des indications de profondeur dans le monde réel. Boucher vos hologrammes en fonction d’autres hologrammes et des objets réels vous aide à convaincre l’utilisateur que ces hologrammes sont en fait dans leur espace. Les hologrammes flottants en espace ou en mouvement avec l’utilisateur ne seront pas aussi réels. Lorsque cela est possible, placez les éléments pour plus de confort.

Visualisez les surfaces lors du placement ou du déplacement d’hologrammes (utilisez une grille projetée simple). Cela permet à l’utilisateur de savoir où il peut placer ses hologrammes et montre l’utilisateur si l’endroit où il tente de placer l’hologramme n’a pas encore été mappé. Vous pouvez « encadrer des éléments » pour l’utilisateur s’ils finissent à un trop grand angle.

## <a name="conceptual-overview"></a>Vue d’ensemble conceptuelle

![surfaces de filet couvrant une salle](images/SurfaceReconstruction.jpg)<br>
*Exemple de maillage de mappage spatial couvrant une salle*

Les deux principaux types d’objets utilisés pour le mappage spatial sont l' « observateur de surface spatiale » et la « surface spatiale ».

L’application fournit l’observateur de surface spatiale avec un ou plusieurs volumes englobants, pour définir les régions d’espace dans lesquelles l’application souhaite recevoir des données de mappage spatiale. Pour chacun de ces volumes, le mappage spatial fournira à l’application un ensemble de surfaces spatiales.

Ces volumes peuvent être fixes (à un emplacement fixe par rapport au monde réel) ou ils peuvent être attachés au HoloLens (ils se déplacent, mais ne pivotent pas avec le HoloLens à mesure qu’il progresse dans l’environnement). Chaque surface spatiale décrit des surfaces réelles dans un petit volume d’espace, représentée sous la forme d’un maillage de triangles attaché à un [système de coordonnées spatiales](coordinate-systems.md)verrouillé.

À mesure que le HoloLens recueille de nouvelles données sur l’environnement et que les modifications apportées à l’environnement se produisent, les surfaces spatiales s’affichent, disparaissent et changent.

## <a name="spatial-mapping-vs-scene-undesranding-worldmesh"></a>Mappage spatial et scène Undesranding WorldMesh
Pour HoloLens 2, il est possible d’interroger une version statique des données de mappage spatiale à l’aide de [Scene Understanding SDK](scene-understanding-SDK.md) (paramètre EnableWorldMesh). Voici les différences entre deux méthodes d’accès aux données de mappage spatiale :
* API de mappage spatial :
   * Plage limitée : les données de mappage spatiale disponibles pour les applications dans une taille limitée mise en cache pour l’utilisateur.
   * Fournit des mises à jour à faible latence des régions de maillage modifiées par le biais d’événements SurfacesChanged.
   * Niveau variable de détails contrôlés par des triangles par paramètre de compteur cubique.
* SDK Scene compris :
   * Plage illimitée : fournit toutes les données de mappage spatiale analysées dans le rayon de la requête.
   * Fournit un instantané statique des données de mappage spatiale. L’obtention des données de mappage spatiale mises à jour requiert l’exécution d’une nouvelle requête pour l’ensemble du maillage.
   * Niveau de détail cohérent des détails contrôlés par le paramètre RequestedMeshLevelOfDetail.

## <a name="what-influences-spatial-mapping-quality"></a>Qu’est-ce qui influence la qualité du mappage spatial ?

Plusieurs facteurs, détaillés [ici](environment-considerations-for-hololens.md), peuvent affecter la fréquence et la gravité de ces erreurs.  Toutefois, vous devez concevoir votre application afin que l’utilisateur puisse atteindre ses objectifs même en présence d’erreurs dans les données de mappage spatiale.

## <a name="common-usage-scenarios"></a>Scénarios d’utilisation courants

![Illustrations de scénarios courants d’utilisation de mappages spatiaux : placement, occlusion, physique et navigation](images/sm-concepts-1000px.png)

### <a name="placement"></a>Sélection élective

Le mappage spatial offre aux applications la possibilité de présenter des formes d’interaction naturelles et familières à l’utilisateur. qu’est-ce qui pourrait être plus naturel que de placer votre téléphone sur le Bureau ?

La limitation de l’emplacement des hologrammes (ou plus généralement, toute sélection d’emplacements spatiaux) à placer sur des surfaces fournit un mappage naturel entre le langage 3D (point dans l’espace) et le 2D (point sur la surface). Cela réduit la quantité d’informations que l’utilisateur doit fournir à l’application et rend donc les interactions de l’utilisateur plus rapides, plus simples et plus précises. Cela est particulièrement vrai, car la « distance » n’est pas une opération qui permet de communiquer physiquement avec d’autres personnes ou sur des ordinateurs. Lorsque nous utilisons notre doigt, nous spécifions une direction, mais pas une distance.

Il est important de noter que lorsqu’une application déduit la distance par rapport à la direction (par exemple en effectuant un raycast le long de la direction du regard de l’utilisateur pour trouver la surface spatiale la plus proche), cela doit donner des résultats que l’utilisateur est en mesure de prédire de manière fiable. Dans le cas contraire, l’utilisateur perd sa logique de contrôle, ce qui peut rapidement devenir frustrant. Une méthode qui permet d’effectuer cette opération consiste à exécuter plusieurs raycasts au lieu d’un seul. Les résultats de l’agrégat doivent être plus lisses et plus prévisibles, moins susceptibles d’influencer les résultats « non-aberrants » temporaires (comme le peuvent être causés par des rayons passant par des trous minuscules ou des petits bits de géométrie dont l’utilisateur n’a pas conscience). L’agrégation ou le lissage peuvent également être effectués au fil du temps. par exemple, vous pouvez limiter la vitesse maximale à laquelle un hologramme peut varier de distance par rapport à l’utilisateur. Le simple fait de limiter la valeur de distance minimale et maximale peut également être utile, de sorte que l’hologramme qui est déplacé ne se déplace pas soudainement à la distance ou ne s’arrête pas dans le visage de l’utilisateur.

Les applications peuvent également utiliser la forme et la direction des surfaces pour guider le placement de l’hologramme. Une chaise holographique ne doit pas pénétrer dans les murs et doit être vidée avec le plancher même si elle est légèrement inégale. Ce genre de fonctionnalité s’appuie probablement sur l’utilisation de collisions physiques plutôt que simplement sur raycasts, mais des préoccupations similaires s’appliquent. Si l’hologramme est placé dans de nombreux petits polygones, comme les jambes d’un fauteuil, il peut être judicieux d’étendre la représentation physique de ces polygones à un autre plus large et plus lisse afin qu’ils soient plus en mesure de glisser-déplacer des surfaces spatiales sans avec SnagIt.

À l’extrême, l’entrée de l’utilisateur peut être simplifiée entièrement et les surfaces spatiales peuvent être utilisées pour effectuer un placement d’hologramme entièrement automatique. Par exemple, l’application peut placer un commutateur lumineux holographique quelque part sur le mur pour que l’utilisateur appuie sur. Les mêmes avertissements sur la prévisibilité s’appliquent doublement. Si l’utilisateur est en mesure de contrôler le placement des hologrammes, mais que l’application ne place pas toujours les hologrammes à l’endroit où ils s’attendent (si le commutateur lumineux apparaît quelque part que l’utilisateur ne peut pas atteindre), cette expérience est frustrante. Il peut s’avérer plus difficile d’effectuer un placement automatique nécessitant une correction utilisateur, plutôt que de demander simplement à l’utilisateur de toujours se positionner. étant donné que le positionnement automatique réussi est *attendu*, la correction manuelle semble être une charge !

Notez également que la capacité d’une application à utiliser des surfaces spatiales pour le placement dépend largement de l' [expérience d’analyse](spatial-mapping.md#the-environment-scanning-experience)de l’application. Si une surface n’a pas été analysée, elle ne peut pas être utilisée pour le placement. Il revient à l’application de rendre cette opération claire pour l’utilisateur, afin de pouvoir analyser les nouvelles surfaces ou sélectionner un nouvel emplacement.

Le retour visuel à l’utilisateur revêt une importance primordiale pendant le positionnement. L’utilisateur doit savoir où l’hologramme est lié à la surface la plus proche avec des [effets de terre](spatial-mapping.md#visualization). Ils doivent comprendre pourquoi le mouvement de leur hologramme est restreint (par exemple, en raison d’une collision avec une autre surface proche). S’ils ne peuvent pas placer un hologramme à l’emplacement actuel, la rétroaction visuelle doit le faire clairement. Par exemple, si l’utilisateur tente de placer un canapé dans le mur, les parties du canapé qui se trouvent derrière le mur doivent s’dans une couleur en colère. À l’inverse, si l’application ne parvient pas à trouver une surface spatiale dans un emplacement où l’utilisateur peut voir une surface réelle, l’application doit le faire clairement. L’absence évidente d’un effet de terre dans ce domaine peut atteindre cet objectif.

### <a name="occlusion"></a>Occlusion

L’une des principales utilisations des surfaces de mappage spatiales est simplement de occultait hologrammes. Ce comportement simple a un impact énorme sur le réalisme perçu des hologrammes, ce qui permet de créer un sens de Visceral qui occupe vraiment le même espace physique que l’utilisateur.

L’occlusion fournit également des informations à l’utilisateur. Lorsqu’un hologramme semble être bloqués par une surface réaliste, cela fournit des commentaires visuels supplémentaires sur l’emplacement spatial de cet hologramme dans le monde. À l’inverse, l’occlusion peut également *Masquer* de façon utile les informations de l’utilisateur ; l’occlusion des hologrammes derrière les murs peut réduire l’encombrement visuel de façon intuitive. Pour masquer ou afficher un hologramme, l’utilisateur doit simplement déplacer son chef.

L’occlusion peut également être utilisée pour répondre aux attentes d’une interface utilisateur naturelle basée sur des interactions physiques familières ; Si un hologramme est bloqués par une surface, c’est parce que cette surface est pleine, de sorte que l’utilisateur doit s’attendre à ce que l’hologramme entre en *conflit* avec cette surface et non simplement le traverser.

Parfois, l’occlusion des hologrammes n’est pas souhaitable. Si un utilisateur doit être en mesure d’interagir avec un hologramme, il doit être en mesure de le voir, même s’il se trouve derrière une surface réaliste. Dans ce cas, il est généralement judicieux d’afficher un tel hologramme différemment lorsqu’il est bloqués (par exemple, en réduisant sa luminosité). De cette façon, l’utilisateur est en mesure de localiser visuellement l’hologramme, mais il est toujours conscient qu’il se trouve derrière un point.

### <a name="physics"></a>Physique

L’utilisation de la simulation physique est une autre façon d’utiliser le mappage spatial pour renforcer la *présence* d’hologrammes dans l’espace physique de l’utilisateur. Lorsque ma boule de caoutchouc holographique s’arrête de façon réaliste sur mon bureau, rebondit sur le sol et disparaît sous le canapé, il peut être difficile de croire qu’elle n’est pas vraiment là.

La simulation physique offre également la possibilité pour une application d’utiliser des interactions naturelles et familières basées sur la physique. Le déplacement d’un morceau de mobilier holographique sur le plancher sera probablement plus facile pour l’utilisateur si le meuble répond comme s’il avait été déplacé sur le sol avec l’inertie et la friction appropriées.

Pour générer des comportements physiques réalistes, vous devrez probablement effectuer un [traitement par maillage](spatial-mapping.md#mesh-processing) , tel que le remplissage des trous, la suppression des hallucinations flottants et le lissage des surfaces approximatives.

Vous devrez également réfléchir à la façon dont l' [expérience d’analyse](spatial-mapping.md#the-environment-scanning-experience) de votre application influence sa simulation physique. Tout d’abord, les surfaces manquantes ne sont pas en conflit avec quoi que ce soit ; que se passe-t-il lorsque la balle en caoutchouc s’arrête au couloir et à la fin du monde connu ? Deuxièmement, vous devez décider si vous souhaitez continuer à répondre aux modifications de l’environnement dans le temps. Dans certains cas, vous souhaiterez peut-être répondre le plus rapidement possible. Imaginons que l’utilisateur utilise des portes et des meubles comme barricadesables dans la défense contre un TEMPEST de flèches latines entrantes. Dans d’autres cas, vous souhaiterez peut-être ignorer les nouvelles mises à jour ; la conduite de votre voiture de sport holographique autour de la Racetrack à votre étage peut ne pas être si amusante si votre chien décide de se asseoir au milieu de la piste.

### <a name="navigation"></a>Navigation

Les applications peuvent utiliser des données de mappage spatiale pour accorder aux caractères holographiques (ou agents) la possibilité de naviguer dans le monde réel de la même manière qu’une personne réelle. Cela peut aider à renforcer la présence de caractères holographiques en les limitant au même ensemble de comportements naturels et familiers que ceux de l’utilisateur et de leurs amis.

Les fonctionnalités de navigation peuvent également être utiles aux utilisateurs. Une fois qu’une carte de navigation a été créée dans une zone donnée, elle peut être partagée pour fournir des directions holographiques pour les nouveaux utilisateurs qui ne sont pas familiarisés avec cet emplacement. Cette carte peut être conçue pour garantir le bon déroulement du trafic « piéton », ou pour éviter les accidents dans des lieux dangereux tels que des sites de construction.

Les principaux défis techniques liés à la mise en œuvre de la fonctionnalité de navigation sont la détection fiable des surfaces guidées (les êtres humains ne se déplacent pas sur les tables !) et l’adaptation progressive aux changements de l’environnement (les êtres humains ne parcourent pas les portes fermées !). La maille peut nécessiter un [traitement](spatial-mapping.md#mesh-processing) avant de pouvoir être utilisée pour la planification des chemins d’accès et la navigation par un caractère virtuel. Le lissage de la maille et la suppression des hallucinations peuvent aider à éviter que des caractères soient bloqués. Vous pouvez également souhaiter simplifier considérablement la maille afin d’accélérer les calculs de la planification et de la navigation de vos caractères. Ces défis ont bien fait l’affaire d’une grande attention dans le développement de la technologie Videogame et il existe une multitude de documents de recherche disponibles sur ces sujets.

Notez que la fonctionnalité intégrée NavMesh dans Unity ne peut pas être utilisée avec des surfaces de mappage spatiale. En effet, les surfaces de mappage spatiale ne sont pas connues jusqu’au démarrage de l’application, tandis que les fichiers de données NavMesh doivent être générés à partir des ressources sources à l’avance. Notez également que le système de mappage spatial ne fournit pas d' [informations sur les surfaces très loin](spatial-mapping.md#the-environment-scanning-experience) de l’emplacement actuel de l’utilisateur. Par conséquent, l’application doit se déconnecter de lui-même s’il s’agit de créer une carte d’une très grande zone.

### <a name="visualization"></a>Sessions

La plupart du temps, il convient que les surfaces spatiales soient invisibles ; pour réduire l’encombrement visuel et laisser le monde réel parler de lui-même. Toutefois, il est parfois utile de visualiser les surfaces de mappage spatiales directement, malgré le fait que leurs équivalents réels sont déjà visibles.

Par exemple, lorsque l’utilisateur tente de placer un hologramme sur une surface (en plaçant une armoire holographique sur le mur, par exemple), il peut être utile d’utiliser l’hologramme en convertissant une ombre sur l’aire. Cela donne à l’utilisateur un sens nettement plus clair de la proximité physique exacte entre l’hologramme et la surface. Il s’agit également d’un exemple de la pratique plus générale de l’aperçu visuel d’une modification avant que l’utilisateur ne la valide.

Grâce à la visualisation des surfaces, l’application peut partager avec l’utilisateur sa compréhension de l’environnement. Par exemple, un jeu de cartes holographiques peut visualiser les surfaces horizontales qu’il a identifiées comme « tables », afin que l’utilisateur sache où il doit accéder à l’interaction.

La visualisation des surfaces peut être un moyen utile pour montrer à l’utilisateur des espaces qui sont masqués dans l’affichage. Cela peut fournir un moyen simple de donner à l’utilisateur l’accès à sa cuisine (et à tous ses hologrammes contenus) à partir de son salon.

Les maillages de surface fournis par le mappage spatial peuvent ne pas être particulièrement « nettoyés ». Il est donc important de les visualiser de manière appropriée. Les calculs d’éclairage traditionnels peuvent mettre en évidence les erreurs dans les normales de surface de manière visuellement gênante, tandis que les textures « propres » projetées sur l’aire peuvent aider à lui attribuer une apparence de plus propre. Il est également possible d’effectuer un [traitement de maillage](spatial-mapping.md#mesh-processing) pour améliorer les propriétés de maillage, avant le rendu des surfaces.

> [!NOTE]
> HoloLens 2 implémente un nouveau [Runtime de présentation de scène](scene-understanding.md), qui fournit aux développeurs de réalité mixte une représentation environnementale structurée, conçue pour simplifier l’implémentation du placement, de l’occlusion, de la physique et de la navigation.

## <a name="using-the-surface-observer"></a>Utilisation de l’observateur de surface

Le point de départ pour le mappage spatial est l’observateur de surface. Le déroulement du programme est le suivant :
* Créer un objet d’observateur de surface
   * Fournissez un ou plusieurs volumes spatiaux pour définir les régions d’intérêt pour lesquelles l’application souhaite recevoir des données de mappage spatiale. Un volume spatial est simplement une forme définissant une zone d’espace, telle qu’une sphère ou une zone.
   * Utilisez un volume spatial avec un système de coordonnées spatiales verrouillé pour identifier une région fixe du monde physique.
   * Utilisez un volume spatial, mettez à jour chaque cadre avec un système de coordonnées spatiales verrouillées pour identifier une région d’espace qui se déplace (mais ne pivote pas) avec l’utilisateur.
   * Ces volumes spatiaux peuvent être modifiés ultérieurement à tout moment, à mesure que l’état de l’application ou de l’utilisateur change.
* Utiliser l’interrogation ou la notification pour extraire des informations sur les surfaces spatiales
   * Vous pouvez interroger l’observateur de surface pour l’état de surface spatiale à tout moment. Vous pouvez également vous inscrire à l’événement « surfaces modifiées » de l’observateur de surface, qui notifie l’application quand des surfaces spatiales ont changé.
   * Pour un volume spatial dynamique, tel que la vue frustum, ou un volume verrouillé par le corps, les applications doivent interroger les modifications de chaque image en définissant la région d’intérêt, puis en obtenant l’ensemble actuel de surfaces spatiales.
   * Pour un volume statique, tel qu’un cube verrouillé couvrant une seule pièce, les applications peuvent s’inscrire à l’événement « surfaces modifiées » pour être averti lorsque des surfaces spatiales à l’intérieur de ce volume peuvent avoir changé.
* Modifications des surfaces de processus
   * Itérez l’ensemble de surfaces spatiales fourni.
   * Classer les surfaces spatiales comme ajoutées, modifiées ou supprimées.
   * Pour chaque surface spatiale ajoutée ou modifiée, si nécessaire, envoyez une demande asynchrone pour recevoir la maille mise à jour représentant l’état actuel de la surface au niveau de détail souhaité.
* Traiter la requête de maillage asynchrone (plus de détails dans les sections suivantes).

## <a name="mesh-caching"></a>Mise en cache de maillage

Les surfaces spatiales sont représentées par des maillages à angle dense. Le stockage, le rendu et le traitement de ces mailles peuvent consommer des ressources de calcul et de stockage significatives. Par conséquent, chaque application doit adopter un schéma de mise en cache de maillage adapté à ses besoins, afin de réduire les ressources utilisées pour le traitement et le stockage du maillage. Ce schéma doit déterminer les maillages à conserver et les à ignorer, ainsi que la mise à jour de la maille pour chaque surface spatiale.

La plupart des considérations abordées expliquent directement comment votre application doit utiliser la mise en cache de maille. Vous devez réfléchir à la façon dont l’utilisateur se déplace dans l’environnement, quelles sont les surfaces nécessaires, lorsque différentes surfaces sont observées et lorsque les modifications de l’environnement doivent être capturées.

Lors de l’interprétation de l’événement « surfaces modifiées » fourni par l’observateur de surface, la logique de mise en cache du maillage de base est la suivante :
* Si l’application voit un ID de surface spatiale qu’elle n’a pas déjà vu, elle doit la traiter en tant que nouvelle surface spatiale.
* Si l’application voit une surface spatiale avec un ID connu mais avec une nouvelle heure de mise à jour, elle doit considérer cela comme une surface spatiale mise à jour.
* Si l’application ne voit plus une surface spatiale avec un ID connu, elle doit la traiter comme une surface spatiale supprimée.

Chaque application peut ensuite effectuer les choix suivants :
* Pour les nouvelles surfaces spatiales, le maillage doit-il être demandé ?
   * En général, la maille doit être demandée immédiatement pour les nouvelles surfaces spatiales, ce qui peut fournir de nouvelles informations utiles à l’utilisateur.
   * Toutefois, les nouvelles surfaces spatiales près et avant de l’utilisateur doivent être prioritaires et leur maillage doit être demandé en premier.
   * Si le nouveau maillage n’est pas nécessaire, si, par exemple, l’application a, de manière permanente ou provisoire, son modèle d’environnement, elle ne doit pas être demandée.
* Pour les surfaces spatiales mises à jour, le maillage doit-il être demandé ?
   * Les surfaces spatiales mises à jour à proximité et devant l’utilisateur doivent être prioritaires et leur maillage doit être demandé en premier.
   * Il peut également être utile d’attribuer aux nouvelles surfaces une priorité plus élevée que celle des surfaces mises à jour, en particulier lors de l’analyse.
   * Pour limiter les coûts de traitement, les applications peuvent souhaiter limiter la vitesse à laquelle elles traitent les mises à jour des surfaces spatiales.
   * Il peut être possible de déduire que les modifications apportées à une surface spatiale sont mineures, par exemple si les limites de la surface sont petites, auquel cas la mise à jour peut ne pas être suffisamment importante pour le traitement.
   * Les mises à jour apportées aux surfaces spatiales en dehors de la région actuelle de l’utilisateur peuvent être ignorées entièrement, mais dans ce cas, il peut être plus efficace de modifier les volumes de limite spatiale en cours d’utilisation par l’observateur de surface.
* Pour les surfaces spatiales supprimées, le maillage doit-il être abandonné ?
   * Généralement, la maille doit être ignorée immédiatement pour les surfaces spatiales supprimées, afin que l’occlusion d’hologramme reste correcte.
   * Toutefois, si l’application a du mal à penser qu’une surface spatiale réapparaîtra bientôt (peut-être en raison de la conception de l’expérience utilisateur), il peut être plus efficace de la conserver que d’ignorer son maillage et de la recréer ultérieurement.
   * Si l’application crée un modèle à grande échelle de l’environnement de l’utilisateur, il se peut qu’elle ne souhaite pas supprimer les mailles. Toutefois, il est nécessaire de limiter l’utilisation des ressources, éventuellement en spoulés les maillages sur le disque en tant que surfaces spatiales disparaissent.
   * Notez que certains événements relativement rares pendant la génération de la surface spatiale peuvent entraîner le remplacement des surfaces spatiales par de nouvelles surfaces spatiales dans un emplacement similaire, mais avec des ID différents. Par conséquent, les applications qui choisissent de ne pas ignorer une surface supprimée doivent veiller à ne pas se retrouver avec plusieurs maillages de surface spatiales très superposés couvrant le même emplacement.
* Le maillage doit-il être ignoré pour toutes les autres surfaces spatiales ?
   * Même s’il existe une surface spatiale, si elle n’est plus utile à l’expérience de l’utilisateur, elle doit être ignorée. Par exemple, si l’application « remplace » la salle de l’autre côté d’une porte avec un espace virtuel alternatif, les surfaces spatiales de cette salle n’ont plus d’importance.

Voici un exemple de stratégie de mise en cache de maillage, utilisant des hystérésis spatiales et temporelles :
* Prenons l’exemple d’une application qui souhaite utiliser un volume spatial d’intérêt en forme de frustum qui suit le regard de l’utilisateur à mesure qu’ils regardent et détaillent.
* Une surface spatiale peut disparaître temporairement sur ce volume simplement parce que l’utilisateur regarde à l’extérieur de la surface ou des étapes... seulement pour revenir en arrière ou se déplacer à nouveau un instant plus tard. Dans ce cas, l’abandon et la recréation du maillage pour cette surface représentent un traitement redondant important.
* Pour réduire le nombre de modifications traitées, l’application utilise deux observateurs de surface spatiale, l’un contenu dans l’autre. Le plus grand volume est sphérique et suit l’utilisateur « paresseuse ». Il se déplace uniquement lorsque cela est nécessaire pour s’assurer que son centre se trouve dans 2,0 mètres de l’utilisateur.
* Les maillages de surface spatiale nouveaux et mis à jour sont toujours traités à partir de l’observateur de surface interne plus petite, mais les maillages sont mis en cache jusqu’à ce qu’ils disparaissent de l’observateur de surface externe plus large. Cela permet à l’application d’éviter le traitement de nombreuses modifications redondantes en raison du déplacement de l’utilisateur local.
* Comme une surface spatiale peut également disparaître temporairement en raison de la perte de suivi, l’application diffère également l’abandon des surfaces spatiales supprimées pendant le suivi de la perte.
* En général, une application doit évaluer le compromis entre le traitement des mises à jour réduites et l’augmentation de l’utilisation de la mémoire pour déterminer sa stratégie de mise en cache idéale.

## <a name="rendering"></a>Rendu

Il existe trois façons principales pour lesquelles les maillages de mappage spatial ont tendance à être utilisés pour le rendu :
* Pour la visualisation des surfaces
   * Il est souvent utile de visualiser directement les surfaces spatiales. Par exemple, le cast de « Shadows » d’objets en surfaces spatiales peut fournir des commentaires visuels utiles à l’utilisateur pendant qu’ils placent des hologrammes sur des surfaces.
   * Une chose à garder à l’esprit est que les maillages spatiaux sont différents du type de maille qu’un artiste 3D peut créer. La topologie triangulaire n’est pas aussi « propre » que la topologie créée par l’utilisateur, et la maille est sujette à de [nombreuses erreurs](spatial-mapping.md#what-influences-spatial-mapping-quality).
   * Pour créer un visuel agréable, vous pouvez effectuer un [traitement de maillage](spatial-mapping.md#mesh-processing), par exemple pour remplir des trous ou normaliser les normales de surface. Vous pouvez également utiliser un nuanceur pour projeter des textures conçues pour les artistes sur votre maille au lieu de visualiser directement la topologie de maillage et les normales.
* Pour boucher les hologrammes derrière des surfaces réelles
   * Les surfaces spatiales peuvent être rendues dans une passe de profondeur uniquement qui affecte uniquement la [mémoire tampon de profondeur](https://msdn.microsoft.com/library/windows/desktop/bb219616(v=vs.85).aspx) et n’affecte pas les cibles de rendu des couleurs.
   * Cela fait passer la mémoire tampon de profondeur aux hologrammes occultait par la suite sous-tendant des surfaces spatiales. L’occlusion précise des hologrammes améliore le sens dans lequel les hologrammes se trouvent vraiment dans l’espace physique de l’utilisateur.
   * Pour activer le rendu de profondeur uniquement, mettez à jour votre état de fusion pour affecter à [RenderTargetWriteMask](https://msdn.microsoft.com/library/windows/desktop/hh404492(v=vs.85).aspx) la valeur zéro pour toutes les cibles de rendu des couleurs.
* Pour modifier l’apparence des bloqués hologrammes par surfaces réelles
   * Normalement, la géométrie rendue est masquée lorsqu’elle est bloqués. Pour ce faire, définissez la fonction Depth dans votre [État Depth-stencil](https://msdn.microsoft.com/library/windows/desktop/ff476110(v=vs.85).aspx) sur « inférieur ou égal à », ce qui entraîne la visibilité de la géométrie uniquement lorsque celle-ci est plus **proche** de l’appareil photo que toutes les géométries affichées précédemment.
   * Toutefois, il peut être utile de garder une certaine géométrie visible même quand elle est bloqués et de modifier son apparence lorsque bloqués est un moyen de fournir des commentaires visuels à l’utilisateur. Par exemple, cela permet à l’application de montrer à l’utilisateur l’emplacement d’un objet tout en le rendant clair, derrière une surface réelle.
   * Pour ce faire, restituez la géométrie une seconde fois avec un nuanceur différent qui crée l’apparence « bloqués » souhaitée. Avant de restituer la géométrie pour la deuxième fois, apportez deux modifications à l’état de votre [gabarit de profondeur](https://msdn.microsoft.com/library/windows/desktop/ff476110(v=vs.85).aspx). Tout d’abord, définissez la fonction Depth sur « supérieur ou égal à », de façon à ce que la géométrie ne soit visible qu’à partir de l’appareil photo, par **rapport à toute** la géométrie précédemment rendue. Ensuite, définissez DepthWriteMask sur zéro, afin que la mémoire tampon de profondeur ne soit pas modifiée (le tampon de profondeur doit continuer à représenter la profondeur de la géométrie la **plus proche** de l’appareil photo).

Les [performances](understanding-performance-for-mixed-reality.md) sont une préoccupation importante lors du rendu de maillages de mappages spatiaux. Voici quelques techniques de performances de rendu spécifiques au rendu des maillages de mappage spatial :
* Ajuster la densité du triangle
   * Lors de la demande de maillages de surfaces spatiales à partir de votre observateur de surface, demandez la densité la plus faible des maillages de triangle qui suffira à vos besoins.
   * Il peut être judicieux de modifier la densité des triangles sur une surface par surface, en fonction de la distance de la surface de l’utilisateur et de sa pertinence pour l’expérience utilisateur.
   * La réduction du nombre de triangles réduira les coûts d’utilisation de la mémoire et de traitement des vertex sur le GPU, bien qu’il n’affecte pas les coûts de traitement des pixels.
* Effectuer une élimination frustum
   * L’élimination de frustum ignore les objets de dessin qui ne peuvent pas être vus, car ils se trouvent en dehors du frustum d’affichage actuel. Cela réduit les coûts de traitement du processeur et du GPU.
   * Étant donné que l’élimination est effectuée au niveau de chaque maillage et que les surfaces spatiales peuvent être volumineuses, le fait de diviser chaque maillage de surface spatiale en plus petits blocs peut entraîner une élimination plus efficace (dans le cas où un nombre réduit de triangles hors écran sont rendus). Toutefois, il existe un compromis. plus vous avez de maillages, plus les appels de dessin que vous devez effectuer, ce qui peut augmenter les coûts de l’UC. Dans un cas extrême, les calculs d’élimination des frustum peuvent même avoir un coût d’UC mesurable.
* Ajuster l’ordre de rendu
   * Les surfaces spatiales ont tendance à être volumineuses, car elles représentent l’environnement entier de l’utilisateur qui les entoure. Les coûts de traitement des pixels sur le GPU peuvent donc être élevés, en particulier dans les cas où il y a plus d’une couche de géométrie visible (y compris des surfaces spatiales et d’autres hologrammes). Dans ce cas, la couche la plus proche de l’utilisateur va abandonner toutes les couches, de sorte que tout temps GPU consacré au rendu de ces autres couches distantes est gaspillé.
   * Pour réduire ce travail redondant sur le GPU, il est utile de restituer les surfaces opaques dans l’ordre avant-arrière (les plus proches en premier, les plus éloignées en dernier). Par « opaque », nous entendons les surfaces pour lesquelles le DepthWriteMask est défini sur un dans l’état de votre [gabarit de profondeur](https://msdn.microsoft.com/library/windows/desktop/ff476110(v=vs.85).aspx). Lorsque les surfaces les plus proches sont rendues, elles priment le tampon de profondeur afin que davantage de surfaces distantes soient correctement ignorées par le processeur de pixels sur le GPU.

## <a name="mesh-processing"></a>Traitement de maillage

Une application peut souhaiter effectuer [diverses opérations](spatial-mapping.md#mesh-processing) sur les maillages de surface spatiale en fonction de ses besoins. Les données d’index et de vertex fournies avec chaque maillage de surface spatiale utilisent la même disposition familière que les [mémoires tampons de vertex et d’index](https://msdn.microsoft.com/library/windows/desktop/bb147325%28v=vs.85%29.aspx) utilisées pour le rendu des maillages de triangle dans toutes les API de rendu modernes. Toutefois, l’un des principaux faits à connaître est que les triangles de mappage spatial ont un **ordre de déroulement dans le sens inverse des aiguilles**d’une montre. Chaque triangle est représenté par trois index de vertex dans le tampon d’index de la maille et ces index identifient les vertex du triangle dans le **sens des aiguilles** d’une montre, lorsque le triangle est affiché du côté **frontal** . Le côté avant (ou à l’extérieur) des maillages de surface spatiales correspond au côté de l’avant (visible) des surfaces universelles réelles.

Les applications doivent uniquement effectuer une simplification de la maille si la densité de triangle la plus grossière fournie par l’observateur de surface est toujours insuffisante. ce travail est coûteux en termes de calcul et est déjà effectué par le runtime pour générer les différentes niveaux de détail fournis.

Étant donné que chaque observateur de surface peut fournir plusieurs surfaces spatiales non connectées, certaines applications peuvent souhaiter découper ces maillages de surface spatiale entre eux, puis les éclairer ensemble. En général, l’étape de découpage est nécessaire, car les maillages de surface spatiale avoisinants se chevauchent souvent légèrement.

## <a name="raycasting-and-collision"></a>Raycasting et collision

Pour qu’une API physique (telle que [Havok](https://www.havok.com/)) fournisse une application avec des fonctionnalités de Raycasting et de collision pour les surfaces spatiales, l’application doit fournir des maillages de surface spatiale à l’API physique. Les maillages utilisés pour la physique ont souvent les propriétés suivantes :
* Ils ne contiennent qu’un petit nombre de triangles. Les opérations physiques sont plus gourmandes en calcul que les opérations de rendu.
* Ils sont serrés. Les surfaces destinées à être solides ne doivent pas avoir de petits trous ; même les trous trop petits pour être visibles peuvent entraîner des problèmes.
* Ils sont convertis en coques convexes. Les coques convexes comportent peu de polygones et sont exemptes de trous, et elles sont beaucoup plus efficaces en termes de calculs que de maillages de triangles bruts.

Lorsque vous effectuez des raycasts sur des surfaces spatiales, gardez à l’esprit que ces surfaces sont souvent complexes, des formes encombrées de petits détails, tout comme votre bureau ! Cela signifie qu’un seul raycast est souvent insuffisant pour vous fournir suffisamment d’informations sur la forme de la surface et la forme de l’espace vide près de celui-ci. Il est donc généralement judicieux d’effectuer de nombreux raycasts dans une petite zone et d’utiliser les résultats d’agrégation pour obtenir une compréhension plus fiable de la surface. Par exemple, l’utilisation de la moyenne de 10 raycasts pour guider le placement de l’hologramme sur une surface produit un résultat beaucoup plus lisse et moins instable qui utilise simplement un raycast unique.

Toutefois, gardez à l’esprit que chaque raycast peut avoir un coût de calcul élevé. Par conséquent, en fonction de votre scénario d’utilisation, vous devez compenser le coût de calcul des raycasts supplémentaires (effectuées à chaque trame) par rapport au coût de calcul du [traitement des maillages](spatial-mapping.md#mesh-processing) pour lisser et supprimer des trous dans les surfaces spatiales (effectuée quand spatial les mailles sont mises à jour).

## <a name="the-environment-scanning-experience"></a>Expérience d’analyse de l’environnement

Chaque application qui utilise le mappage spatial doit envisager de fournir une « expérience d’analyse »; processus par lequel l’application guide l’utilisateur pour analyser les surfaces nécessaires au bon fonctionnement de l’application.

![exemple d’analyse](images/sr-mixedworld-140429-8pm-00068-1000px.png)<br>
*Exemple d’analyse*

La nature de cette expérience d’analyse peut varier considérablement en fonction des besoins de chaque application, mais deux principes principaux doivent guider sa conception.

Tout d’abord, une **communication claire avec l’utilisateur est la préoccupation principale**. L’utilisateur doit toujours savoir si les exigences de l’application sont respectées. Lorsqu’ils ne sont pas satisfaits, l’utilisateur doit immédiatement savoir pourquoi c’est le cas et il doit être rapidement dirigé pour prendre les mesures appropriées.

Deuxièmement, **les applications doivent tenter d’équilibrer l’efficacité et la fiabilité**. Lorsqu’il est possible de le faire de façon **fiable**, les applications doivent analyser automatiquement les données de mappage spatiale pour économiser le temps utilisateur. Lorsqu’il n’est pas possible de le faire de manière fiable, les applications doivent à la place permettre à l’utilisateur de fournir rapidement à l’application les informations supplémentaires dont il a besoin.

Pour faciliter la conception de l’expérience d’analyse, prenez en compte les possibilités suivantes applicables à votre application :

* **Aucune expérience d’analyse**
   * Une application peut fonctionner parfaitement sans aucune expérience d’analyse guidée. elle présente des informations sur les surfaces observées au cours du déplacement des utilisateurs naturels.
   * Par exemple, une application qui permet à l’utilisateur de dessiner sur des surfaces avec la peinture de pulvérisation holographique ne nécessite que les connaissances des surfaces actuellement visibles pour l’utilisateur.
   * L’environnement peut être complètement analysé s’il s’agit d’un environnement dans lequel l’utilisateur a déjà passé beaucoup de temps à l’aide de HoloLens.
   * Gardez à l’esprit que l’appareil photo utilisé par le mappage spatial ne peut voir que 3,1 m devant l’utilisateur ; par conséquent, le mappage spatial ne connaîtra pas d’autres surfaces distantes, sauf si l’utilisateur les a observées à partir d’une distance plus proche dans le passé.
   * L’utilisateur comprend donc les surfaces qui ont été analysées, l’application doit fournir un retour visuel à cet effet. par exemple, le cast d’ombres virtuelles sur des surfaces numérisées peut aider l’utilisateur à placer des hologrammes sur ces surfaces.
   * Dans ce cas, les volumes limites de l’observateur de surface spatiale doivent être mis à jour sur chaque cadre pour obtenir un [système de coordonnées spatiales](coordinate-systems.md)verrouillé, afin qu’ils suivent l’utilisateur.

* **Trouver un emplacement approprié**
   * Une application peut être conçue pour être utilisée dans un emplacement avec des exigences spécifiques.
   * Par exemple, l’application peut nécessiter une zone vide autour de l’utilisateur afin qu’elle puisse s’assurer en toute sécurité le kung-fou holographique.
   * Les applications doivent communiquer toutes les exigences spécifiques à l’utilisateur au préalable et les renforcer avec des commentaires visuels clairs.
   * Dans cet exemple, l’application doit visualiser l’étendue de la zone vide requise et mettre visuellement en évidence la présence d’objets non désirés dans cette zone.
   * Dans ce cas, les volumes limites de l’observateur de surface spatiale doivent utiliser un système de [coordonnées spatiales](coordinate-systems.md) verrouillé à l’emplacement choisi.

* **Rechercher une configuration appropriée des surfaces**
   * Une application peut nécessiter une configuration spécifique de surfaces, par exemple deux parois larges, plates et opposées pour créer un couloir holographique de miroirs.
   * Dans ce cas, l’application doit analyser les surfaces fournies par le mappage spatial pour détecter les surfaces appropriées et diriger l’utilisateur vers ces surfaces.
   * L’utilisateur doit avoir une option de secours si l’analyse des surfaces de l’application n’est pas complètement fiable. Par exemple, si l’application identifie de manière incorrecte une porte comme un mur plat, l’utilisateur a besoin d’un moyen simple de corriger cette erreur.

* **Analyser une partie de l’environnement**
   * Une application peut souhaiter uniquement capturer une partie de l’environnement, comme indiqué par l’utilisateur.
   * Par exemple, l’application analyse une partie d’une salle afin que l’utilisateur puisse poster une publicité classée holographique pour le mobilier qu’elle souhaite vendre.
   * Dans ce cas, l’application doit capturer les données de mappage spatiale dans les régions observées par l’utilisateur lors de son analyse.

* **Analyser la totalité de la salle**
   * Une application peut nécessiter une analyse de toutes les surfaces dans la salle actuelle, y compris celles qui se trouvent derrière l’utilisateur.
   * Par exemple, un jeu peut mettre l’utilisateur dans le rôle de Gulliver, sous siege à partir de centaines de petites Lilliputians approchant de toutes les directions.
   * Dans ce cas, l’application doit déterminer le nombre de surfaces de la salle active qui ont déjà été analysées et diriger le point de regard de l’utilisateur pour combler les lacunes significatives.
   * La clé de ce processus consiste à fournir des commentaires visuels qui démontrent à l’utilisateur que les surfaces n’ont pas encore été analysées. L’application peut, par exemple, utiliser [un brouillard basé](https://msdn.microsoft.com/library/windows/desktop/bb173401%28v=vs.85%29.aspx) sur la distance pour mettre visuellement en surbrillance des zones qui ne sont pas couvertes par des surfaces de mappage spatiale.

* **Prendre un instantané initial de l’environnement**
   * Une application peut souhaiter ignorer toutes les modifications apportées à l’environnement après avoir effectué un « instantané » initial.
   * Cela peut être utile pour éviter toute interruption des données créées par l’utilisateur qui est étroitement couplée à l’état initial de l’environnement.
   * Dans ce cas, l’application doit faire une copie des données de mappage spatiale dans son état initial une fois l’analyse terminée.
   * Les applications doivent continuer à recevoir des mises à jour des données de mappage spatiale si les hologrammes continuent d’être correctement bloquéss par l’environnement.
   * Les mises à jour continues des données de mappage spatiale permettent également de visualiser les modifications qui se sont produites, en clarifiant l’utilisateur les différences entre les États antérieur et présent de l’environnement.

* **Prendre des instantanés initiés par l’utilisateur de l’environnement**
   * Une application ne souhaite peut-être répondre aux modifications environnementales que lorsqu’il est demandé par l’utilisateur.
   * Par exemple, l’utilisateur peut créer plusieurs « statues » en 3D d’un ami en capturant ses poses à des moments différents.

* **Autoriser l’utilisateur à modifier l’environnement**
   * Une application peut être conçue pour répondre en temps réel à toute modification apportée à l’environnement de l’utilisateur.
   * Par exemple, l’utilisateur qui dessine un rideau peut déclencher une « modification de la scène » pour qu’une lecture holographique se déroule de l’autre côté.

* **Guide de l’utilisateur pour éviter les erreurs dans les données de mappage spatiale**
   * Une application peut souhaiter fournir des conseils à l’utilisateur pendant qu’il analyse son environnement.
   * Cela peut aider l’utilisateur à éviter certains types d' [Erreurs dans les données de mappage spatiale](spatial-mapping.md#what-influences-spatial-mapping-quality), par exemple en restant à l’écart des fenêtres ou miroirs Sunlit.

L’un des détails supplémentaires à prendre en compte est que la « plage » de données de mappage spatiale n’est pas illimitée. Tandis que le mappage spatial crée une base de données permanente d’espaces de grande taille, il ne rend ces données disponibles qu’aux applications dont la taille est limitée à l’utilisateur. Par conséquent, si vous commencez au début d’un couloir long et que vous vous éloignez suffisamment du début, les surfaces spatiales finissent par disparaître. Vous pouvez bien sûr atténuer cela en mettant en cache ces surfaces dans votre application une fois qu’elles ont disparu des données de mappage spatiale disponibles.

## <a name="mesh-processing"></a>Traitement de maillage

Il peut être utile de détecter les types courants d’erreurs dans les surfaces et de filtrer, supprimer ou modifier les données de mappage spatiale comme il convient.

Gardez à l’esprit que les données de mappage spatiale sont destinées à être aussi fidèles que possible pour les surfaces réelles, de sorte que tout traitement que vous appliquez risque de faire passer vos surfaces plus loin de la « vérité ».

Voici quelques exemples de différents types de traitement de maillage qui peuvent s’avérer utiles :

* **Remplissage de trous**
   * Si un petit objet constitué d’un matériau sombre ne parvient pas à être analysé, il laisse un trou dans la surface environnante.
   * Les trous affectent l’occlusion : les hologrammes peuvent être vus « jusqu’à » un trou dans une surface réaliste opaque.
   * Les trous affectent raycasts : Si vous utilisez raycasts pour aider les utilisateurs à interagir avec les surfaces, il peut être indésirable que ces rayons passent par des trous. Une solution de contournement consiste à utiliser un groupe de plusieurs raycasts couvrant une région de taille appropriée. Cela vous permettra de filtrer les résultats « aberrants », de sorte que même si un raycast traverse un petit trou, le résultat de l’agrégat restera valide. Toutefois, gardez à l’esprit que cette approche est un coût de calcul.
   * Les trous affectent les collisions physiques : un objet contrôlé par la simulation physique peut déplacer un trou à l’étage et être perdu.
   * Il est possible d’effectuer un remplissage algorithmique de ces trous dans le maillage des surfaces. Toutefois, vous devrez régler votre algorithme pour que les « véritables trous », tels que les fenêtres et les portes, ne soient pas remplis. Il peut être difficile de distinguer de manière fiable les « véritables trous » de « trous imaginaires ». vous devrez donc faire des essais avec différents heuristiques, tels que « taille » et « forme limite ».

* **Suppression de hallucination**
   * Les réflexions, les lumières brillantes et les objets mobiles peuvent rendre le petit « hallucinations » en attente flottant dans le milieu de l’air.
   * Hallucinations affecte l’occlusion : les hallucinations peuvent devenir visibles en tant que formes sombres se déplaçant devant et obturant d’autres hologrammes.
   * Hallucinations affecte raycasts : Si vous utilisez raycasts pour aider les utilisateurs à interagir avec les surfaces, ces rayons peuvent toucher un hallucination au lieu de la surface derrière. Comme avec les trous, une atténuation consiste à utiliser un grand nombre de raycasts au lieu d’un raycast unique, mais à nouveau cela aura un coût de calcul.
   * Les hallucinations affectent les collisions physiques : un objet contrôlé par la simulation physique peut être bloqué contre un hallucination et ne peut pas se déplacer dans une zone d’espace apparemment claire.
   * Il est possible de filtrer ce hallucinations à partir de la maille de surface. Toutefois, comme pour les trous, vous devez régler votre algorithme pour que les petits objets tels que les poignées de la porte et les béquilles ne soient pas supprimés.

* **Lissage**
   * Le mappage spatial peut retourner des surfaces qui semblent être rugueuses ou bruyantes par rapport à leurs équivalents réels.
   * Le lissage affecte les collisions physiques : si le plancher est grossier, une boule de golf simulée physiquement peut ne pas s’effectuer correctement sur une ligne droite.
   * Le lissage affecte le rendu : si une surface est visualisée directement, les normales des surfaces approximatives peuvent avoir une incidence sur l’apparence et perturber l’apparence d’un « nettoyage ». Il est possible de réduire cela en utilisant l’éclairage et les textures appropriés dans le nuanceur qui est utilisé pour afficher l’aire.
   * Il est possible de lisser l’irrégularité dans un maillage de surface. Toutefois, cela peut éloigner la surface de la surface réelle correspondante. Il est important de maintenir une correspondance étroite pour produire une occlusion d’hologramme précise et permettre aux utilisateurs d’effectuer des interactions précises et prévisibles avec des surfaces holographiques.
   * Si seule une modification cosmétique est nécessaire, elle peut suffire à lisser les normales des sommets sans modifier les positions des sommets.

* **Recherche de plan**
   * Il existe de nombreuses formes d’analyse qu’une application peut souhaiter effectuer sur les surfaces fournies par le mappage spatial.
   * Un exemple simple consiste à « rechercher dans le plan ». identification des régions délimitées, principalement planaires des surfaces.
   * Les régions planaires peuvent être utilisées comme des surfaces de travail holographiques, des régions où le contenu holographique peut être automatiquement placé par l’application.
   * Les régions planaires peuvent contraindre l’interface utilisateur, afin de guider les utilisateurs afin qu’ils puissent interagir avec les surfaces qui répondent le mieux à leurs besoins.
   * Les régions planaires peuvent être utilisées comme dans le monde réel, pour les équivalents holographiques aux objets fonctionnels, tels que les écrans LCD, les tables ou les tableaux blancs.
   * Les régions planaires peuvent définir des zones de lecture, formant ainsi la base des niveaux Videogame.
   * Les régions planaires peuvent aider les agents virtuels à naviguer dans le monde réel, en identifiant les zones d’étage que les gens sont susceptibles de parcourir.

## <a name="prototyping-and-debugging"></a>Prototypage et débogage

### <a name="useful-tools"></a>Outils utiles
* L' [émulateur hololens](using-the-hololens-emulator.md) peut être utilisé pour développer des applications à l’aide du mappage spatial sans accès à un HoloLens physique. Elle vous permet de simuler une session active sur un HoloLens dans un environnement réaliste, avec toutes les données que votre application consomme normalement, y compris le mouvement HoloLens, les systèmes de coordonnées spatiales et les maillages de mappage spatial. Cela peut être utilisé pour fournir des entrées fiables et reproductibles, ce qui peut être utile pour déboguer des problèmes et évaluer des modifications apportées à votre code.
* Pour reproduire un scénario, capturez les données de mappage spatiale sur le réseau à partir d’un HoloLens actif, puis enregistrez-les sur le disque et réutilisez-les dans les sessions de débogage suivantes.
* La [vue 3D du portail d’appareils Windows](using-the-windows-device-portal.md#3d-view) fournit un moyen de voir toutes les surfaces spatiales actuellement disponibles via le système de mappage spatial. Cela fournit une base de comparaison pour les surfaces spatiales à l’intérieur de votre application. par exemple, vous pouvez facilement savoir si des surfaces spatiales sont manquantes ou affichées au mauvais endroit.

### <a name="general-prototyping-guidance"></a>Conseils généraux sur le prototypage
* Étant donné que les [Erreurs](spatial-mapping.md#what-influences-spatial-mapping-quality) dans les données de mappage spatiale peuvent affecter fortement l’expérience de votre utilisateur, nous vous recommandons de tester votre application dans un large éventail d’environnements.
* Ne vous retrouvez pas à l’habitude de toujours tester dans le même emplacement, par exemple au niveau de votre bureau. Veillez à effectuer des tests sur différentes surfaces de différentes positions, formes, tailles et matériaux.
* De même, si les données synthétiques ou enregistrées peuvent être utiles pour le débogage, ne vous inquiétez pas trop sur les mêmes cas de test. Cela peut retarder la recherche de problèmes importants que des tests plus variés auraient été détectés précédemment.
* Il est judicieux d’effectuer des tests avec des utilisateurs réels (et idéalement non-surveillés), car ils ne peuvent pas utiliser le HoloLens ou votre application exactement de la même façon que vous le faites. En fait, il peut être surpris de savoir comment le comportement, les connaissances et les hypothèses de personnes divergentes peuvent être !

## <a name="troubleshooting"></a>Dépannage
* Pour que les maillages de surface soient correctement orientés, chaque GameObject doit être actif avant d’être envoyé à SurfaceObeserver pour que sa maille soit construite. Dans le cas contraire, les mailles s’affichent dans votre espace mais subissent une rotation à des angles inhabituels.
* Le GameObject qui exécute le script qui communique avec le SurfaceObserver doit être défini sur l’origine. Dans le cas contraire, tous les GameObjects que vous créez et envoyez au SurfaceObserver pour que leurs maillages soient construits auront un décalage égal au décalage de l’objet de jeu parent. Cela peut faire apparaître plusieurs mètres dans vos mails, ce qui rend très difficile le débogage de ce qui se passe.

## <a name="see-also"></a>Articles associés
* [Systèmes de coordonnées](coordinate-systems.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)
* [Mappage spatial dans Unity](spatial-mapping-in-unity.md)
* [Compréhension des scènes](scene-understanding.md)
* [Visualisation du balayage d’une pièce](room-scan-visualization.md)
* [Conception du son spatial](spatial-sound-design.md)
* [Étude de cas - Voir à travers vos objets](case-study-looking-through-holes-in-your-reality.md)
