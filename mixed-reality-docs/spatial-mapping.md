---
title: Mappage spatial
description: Mappage spatial fournit une représentation détaillée des surfaces réels dans l’environnement autour de la HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: mappage spatial, HoloLens, réalité mixte, reconstruction de l’aire de conception, maillage, sr
ms.openlocfilehash: 31abeca624512f1d5e721dbe879ca2243cf41345
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597101"
---
# <a name="spatial-mapping"></a>Mappage spatial

Mappage spatial fournit une représentation détaillée des surfaces du monde réel dans l’environnement autour de la HoloLens, ce qui permet aux développeurs de créer une expérience de réalité mixte convaincante. En fusionnant le monde réel avec le monde virtuel, une application peut faire hologrammes semblent réel. Applications peuvent également plus naturellement aligner avec les attentes des utilisateurs en fournissant des interactions et des comportements réalistes familiers.

<br>

>[!VIDEO https://www.youtube.com/embed/zff2aQ1RaVo]

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1er gen)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> Mappage spatial</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>



## <a name="conceptual-overview"></a>Vue d’ensemble conceptuelle

![Les surfaces qui couvrent une salle de maillage](images/SurfaceReconstruction.jpg)<br>
*Un exemple d’une maille de mappage spatial couvrant une salle*

Les deux types d’objet principal utilisés pour le mappage spatial sont l’Observateur Spatial' aire et la « Surface spatiale ».

L’application fournit l’Observateur de Surface spatiale avec un ou plusieurs volumes englobants, pour définir les régions d’espace dans lequel l’application souhaite recevoir des données de mappage spatial. Pour chacun de ces volumes, mappage spatial fournira à l’application avec un ensemble de Surfaces spatiale.

Ces volumes peuvent être STATIONNAIRES (dans un emplacement fixe en ce qui concerne le monde réel), ou elles peuvent être attachées à la HoloLens (ils déplacent, mais ne tournent pas, avec la HoloLens lorsqu’elles circulent dans l’environnement). Chaque surface spatiale décrit surfaces réels dans un petit volume d’espace, représenté sous la forme d’un maillage de triangles attaché à un monde-verrouillé [système de coordonnées spatial](coordinate-systems.md).

Comme le HoloLens rassemble des nouvelles données sur l’environnement, et lorsque des modifications à l’environnement sont, les surfaces spatiales apparaîtra, disparaissent et le modifier.

## <a name="common-usage-scenarios"></a>Scénarios d’utilisation courants

![Illustrations de scénarios d’utilisation courants de mappage Spatial : Positionnement, Occlusion, physique et la Navigation](images/sm-concepts-1000px.png)

### <a name="placement"></a>Sélection élective

Mappage spatial fournit aux applications la possibilité de présenter des formes naturelles et familière d’interaction à l’utilisateur ; ce qui pourrait être plus naturel que celle de placer votre téléphone vers le bas sur le support ?

Limiter le placement de hologrammes (ou plus généralement, une sélection des emplacements spatiaux) de reposer sur des surfaces fournit un mappage naturel à partir de 3D (point dans l’espace) en 2D (point sur la surface). Cela réduit la quantité d’informations de l’utilisateur doit fournir à l’application et permet ainsi des interactions de l’utilisateur plus rapide, plus facile et plus précis. Cela est particulièrement vrai, car « distance » n’est pas quelque chose que nous avons l’habitude de communication physiquement à d’autres personnes ou aux ordinateurs. Lorsque nous indiquons avec notre doigt, nous spécifions une direction, mais pas une distance.

Un inconvénient important ici est que lorsqu’une application déduit la distance à partir de la direction (par exemple en effectuant un raycast le long de la direction du regard de l’utilisateur pour rechercher le plus proche surface spatiale), il doit produire des résultats dont l’utilisateur est en mesure de manière fiable. Sinon, l’utilisateur va perdre leur logique de contrôle, et cela peut rapidement devenir frustrante. Une méthode qui permet cela consiste à effectuer plusieurs raycasts au lieu d’un. Les résultats d’agrégation doivent être plus lisse et plus prévisible, moins susceptibles d’influencer dans les résultats temporaires « valeurs hors norme » (comme peut être dû à des rayons en passant par les failles minuscules ou en appuyant sur petits extraits de la géométrie de l’utilisateur ne connaît pas). Agrégation ou lissage peut également être effectué au fil du temps ; par exemple, vous pouvez limiter la vitesse maximale à laquelle un hologramme peut varier dans la distance à partir de l’utilisateur. Limitation simplement la valeur de distance minimale et maximale peut également aider, donc l’hologramme en cours de déplacement ne pas soudainement voler absent dans la distance ou un plantage en face de l’utilisateur.

Applications permet également la forme et la direction des surfaces guide hologramme placement. Une chaise HOLOGRAPHIQUE ne doit pas pénétrer à travers les murs et doit se trouvent vidage avec la valeur plancher même si elle est légèrement inégale. Ce type de fonctionnalité serait probablement reposent sur l’utilisation de collisions de physique plutôt que simplement raycasts, autres soucis similaires cependant seront applique. Si l’hologramme placée a plusieurs polygones petits qui se borner out, comme les jambes sur une chaise, il peut être judicieux d’étendre la représentation physique de ces polygones à quelque chose de plus larges et plus lisse afin qu’ils soient plus en mesure de faire disparaître sur des surfaces spatiales sans avec SnagIt.

À son extrême, l’entrée d’utilisateur peut être simplifiée suite entièrement et surfaces spatiales peuvent être utilisées pour effectuer la sélection élective hologramme entièrement automatique. Par exemple, l’application peut placer un commutateur de lumière holographique de quelque part sur le mur de l’utilisateur appuie sur. La même restriction sur la prévisibilité applique doublement ici ; Si l’utilisateur s’attend à contrôler hologramme placement, mais l’application ne place pas de toujours hologrammes où qu’elles attendent (si le commutateur de lumière apparaît dans un endroit que l’utilisateur ne peut pas atteindre), ce sera une expérience frustrante. Il peut en fait être pire effectuer la sélection élective automatique nécessitant une correction de l’utilisateur du temps, aux simplement oblige l’utilisateur à procèdent toujours à une sélection élective elles-mêmes. Étant donné que la sélection élective automatique réussie est *attendu*, correction manuelle semble un fardeau !

Notez également que la capacité d’une application pour utiliser des surfaces spatiales pour sélection élective dépend fortement de l’application [analyse expérience](spatial-mapping-design.md#the-environment-scanning-experience). Si une surface n’a pas été analysée, il ne peut pas être utilisé pour la sélection élective. C’est à l’application pour être plus clair à l’utilisateur, afin qu’ils peuvent contribuer à analyser des nouvelles surfaces ou sélectionnez un nouvel emplacement.

Des commentaires visuels à l’utilisateur sont d’une importance primordiale pendant la sélection élective. L’utilisateur a besoin de savoir où l’hologramme est par rapport à la surface le plus proche avec [mise à la terre des effets](spatial-mapping.md#visualization). Ils doivent comprendre pourquoi le déplacement de leur hologramme est actuellement limité (par exemple, en raison d’un conflit avec un autre à proximité de la surface). Si elles ne peuvent pas placer un hologramme dans l’emplacement actuel, puis retour visuel doit indiquer clairement pourquoi ne pas. Par exemple, si l’utilisateur tente de placer un canapé HOLOGRAPHIQUE bloqué moitié sur la prise murale, puis les parties du canapé qui sont trouvent derrière le mur doivent pulsate dans une couleur en colère. Ou, à l’inverse, si l’application ne peut pas trouver une surface spatiale dans un emplacement où l’utilisateur peut voir une surface du monde réel, puis l’application doit indiquer cela clairement. L’absence d’évident d’un effet de la masse dans cette zone peut atteindre ce but.

### <a name="occlusion"></a>Occlusion

Une des principales utilisations des surfaces de mappage spatial doit simplement occlude hologrammes. Ce comportement simple a un impact important sur le réalisme perçu de hologrammes, vous aider à créer une idée viscérale qui vraiment occupent le même espace physique que l’utilisateur.

OCCLUSION fournit également des informations à l’utilisateur. Quand un hologramme semble être bloqués par une surface du monde réel, il offre des indications visuelles supplémentaires quant à l’emplacement spatial de ce hologramme dans le monde. À l’inverse, occlusion peut également utilement *masquer* plus d’informations à partir de l’utilisateur ; hologrammes OCCLUSION derrière les murs peut réduire l’encombrement visuel d’une manière intuitive. Pour masquer ou afficher un hologramme, l’utilisateur doit simplement déplacer leur tête.

OCCLUSION peut également servir d’amorcer des attentes en relation avec une interface utilisateur naturelle en fonction des interactions physiques familiers ; Si un hologramme est bloqué par une surface, c’est parce que cette surface est solide, par conséquent, l’utilisateur doit attendre que l’hologramme sera *entrent en collision* avec celui de surface et pas simplement passer au travers.

Parfois, occlusion d’hologrammes n’est pas souhaitable. Si un utilisateur doit être en mesure d’interagir avec un hologramme, ils doivent être en mesure de voir, même s’il se trouve derrière une surface du monde réel. Dans ce cas, il est généralement judicieux rendu tel un hologramme différemment lorsqu’il est bloqué (par exemple, en réduisant sa luminosité). De cette façon, l’utilisateur sera en mesure de localiser visuellement l’hologramme, mais ils seront toujours conscients qu’il se trouve derrière de quelque chose.

### <a name="physics"></a>Physique

L’utilisation de simulation physique est une autre manière que le mappage spatial peut être utilisé pour renforcer la *présence* de hologrammes dans un espace physique de l’utilisateur. Lorsque mon balle en caoutchouc HOLOGRAPHIQUE désactiver mon bureau se déroule dans la pratique, rebondit sur le sol et disparaît sous le canapé, il peut être difficile pour moi de croire qu’il n’est pas vraiment ce.

Simulation physique offre également la possibilité pour une application d’utiliser des interactions de physique naturelles et familière. Déplacement de HOLOGRAPHIQUE meuble autour de l’étage seront probablement plus facile pour l’utilisateur si mobilier réagit comme si elle ont été décalée sur le sol avec l’inertie appropriée et des frictions.

Pour générer des comportements physiques réalistes, vous aurez probablement besoin d’effectuer certaines [mesh traitement](spatial-mapping.md#mesh-processing) telles que de combler les lacunes, suppression flottante délirante et lissage approximatif des surfaces.

Vous devez également prendre en compte comment votre application [analyse expérience](spatial-mapping-design.md#the-environment-scanning-experience) influence son simulation physique. Tout d’abord, manquant surfaces n’entre en conflit avec n’importe quoi : que se passe-t-il lorsque la balle en caoutchouc génère le couloir et la fin du monde connu ? Deuxièmement, vous devez décider si vous continuez à répondre aux modifications de l’environnement au fil du temps. Dans certains cas, vous souhaitez répondre aussi rapidement que possible ; par exemple si l’utilisateur est à l’aide de portes et meubles comme barricades déplaçable dans défense contre un tempest de flèches Roman entrants. Dans d’autres cas cependant, vous souhaiterez ignorer les nouvelles mises à jour ; pilotent votre voiture de sport HOLOGRAPHIQUE autour de l’ovale sur votre plancher soudainement ne peut-être donc amusant si votre chien décide de se trouvent au milieu de la piste.

### <a name="navigation"></a>Navigation

Applications peuvent utiliser les données de mappage spatial pour accorder HOLOGRAPHIQUE caractères (ou les agents) permet de naviguer le monde réel dans la même façon une personne réelle. Cela peut aider à renforcer la présence de caractères HOLOGRAPHIQUE en les limitant au même jeu de comportements de naturels et familiers que celles de l’utilisateur et de ses amis.

Fonctionnalités de navigation peut être utiles aux utilisateurs également. Une fois qu’une carte de navigation a été créée dans une zone donnée, il peut être partagé pour fournir des directions HOLOGRAPHIQUE pour les nouveaux utilisateurs êtes pas familiarisés avec cet emplacement. Cette carte peut être conçue pour aider à maintenir le passage » « échange de données, ou pour éviter des accidents dans des emplacements dangereux tels que les sites de construction.

Principaux défis techniques liés à l’implémentation des fonctionnalités de navigation sera la détection fiable des surfaces opérationnel (l’homme allure tables !) et sans perte de données adaptation aux modifications de l’environnement (l’homme ne guide les portes fermés !). La maille peut nécessiter certaines [traitement](spatial-mapping.md#mesh-processing) avant qu’il soit utilisable pour la planification de chemin d’accès et la navigation par un caractère virtuel. Lissage du maillage et de suppression délirante peuvent aider à éviter les caractères devient bloqués. Vous pouvez également simplifier considérablement la maille afin d’accélérer son chemin d’accès-planification et les calculs de navigation. Ces défis ont reçu beaucoup d’attention dans le développement de la technologie de jeu vidéo, et constitue une mine de littérature de recherche disponibles sur ces sujets.

Notez que la fonctionnalité intégrée de NavMesh dans Unity ne peut pas être utilisée avec des surfaces de mappage spatial. Il s’agit, car les surfaces de mappage spatial ne sont pas connues avant l’application démarre, tandis que les fichiers de données NavMesh doivent être générés à partir de ressources source avance. Notez également que, le système de mappage spatial ne fournira pas [plus d’informations sur les surfaces de très loin](spatial-mapping-design.md#the-environment-scanning-experience) à partir de l’emplacement actuel de l’utilisateur. Par conséquent, l’application doit « n’oubliez pas' surfaces lui-même s’il doit générer une carte d’une zone de très grande taille.

### <a name="visualization"></a>visualisation

La plupart du temps, il est approprié pour les surfaces spatiales soit invisible ; Pour réduire l’encombrement visuel et de laisser le réel world parler d’elles-mêmes. Toutefois, il est parfois utile de visualiser les surfaces de mappage spatial directement, en dépit du fait que leurs équivalents du monde réel sont déjà visibles.

Par exemple, lorsque l’utilisateur tente de placer un hologramme sur une surface (en plaçant un fichier CAB HOLOGRAPHIQUE sur un mur, par exemple) il peut être utile de « d’arrière-plan » l’hologramme en effectuant un cast d’un cliché instantané sur la surface. Cela donne à l’utilisateur beaucoup plus claire de la proximité physique exacte entre la hologramme et la surface. Il s’agit également un exemple de la plus pratique visuellement « aperçu » une modification avant que l’utilisateur valide lui.

En visualisant les surfaces, l’application peut partager avec l’utilisateur sa compréhension de l’environnement. Par exemple, un jeu de plateau HOLOGRAPHIQUE peut visualiser les surfaces horizontales qu’il a identifié comme « tables », pour que l’utilisateur sache où ils vont interagir.

Visualisation des surfaces peut être un moyen utile pour afficher l’utilisateur à proximité des espaces qui sont masquées. Cela peut fournir un moyen simple de donner à l’utilisateur d’accéder à leur cuisine (et tous ses hologrammes de relation contenant-contenus) à partir de leur salon.

Les panneaux d’aire de conception fournies par le mappage spatial ne peuvent pas être particulièrement « nettoyage ». Par conséquent, il est important de les visualiser de façon appropriée. Calculs d’éclairage traditionnel peuvent Surligner les erreurs dans les normales de surface d’une manière visuellement gênant, tandis que les textures de « nettoyage » projetés sur la surface peuvent vous aider à lui donner une apparence plus propre. Il est également possible d’effectuer [mesh traitement](spatial-mapping.md#mesh-processing) pour améliorer les propriétés de la maille, avant que les surfaces sont rendus.

## <a name="using-the-surface-observer"></a>À l’aide de l’aire de conception observateur

Le point de départ pour le mappage spatial est l’aire de conception observateur. Flux de programme est comme suit :
* Créer un objet de l’aire de conception observateur
   * Fournir un ou plusieurs volumes spatiales, pour définir les régions d’intérêt dans lequel l’application souhaite recevoir des données de mappage spatial. Un volume spatial est simplement une forme définissant une zone d’espace, par exemple une sphère ou une zone.
   * Utiliser un volume spatial avec un système de coordonnées spatial world-verrouillé pour identifier une région fixe du monde physique.
   * Utilisez un volume spatial, mis à jour avec chaque image avec un verrouillage de corps spatial système de coordonnées, pour identifier une région d’espace qui déplace (mais ne pivote pas) avec l’utilisateur.
   * Ces volumes spatiales peuvent être modifiées ultérieurement à tout moment, en tant que l’état de l’application ou l’utilisateur change.
* Utiliser l’interrogation ou notification à récupérer des informations sur les surfaces spatiales
   * Vous pouvez 'interroger' l’aire de conception observateur pour l’état de surface spatiale à tout moment. Vous pouvez également vous pouvez enregistrer pour ' surfaces' événement modifié l’aire de conception observateur, notifie l’application lorsque les surfaces spatiales ont changé.
   * Pour un volume dynamique spatiaux, tels que le frustum vue, ou un volume verrouillé de corps, les applications devront interroge les modifications de chaque trame en affectant à la région d’intérêt et obtention de l’ensemble actuel des surfaces spatiales.
   * Pour un volume statique, par exemple un cube verrouillé de monde couvrant une salle unique, les applications peuvent enregistrer pour l’événement « surfaces modifié » être averti lorsque des surfaces spatiales à l’intérieur de ce volume a peut-être changé.
* Modifications des surfaces de processus
   * Itérer au sein de l’ensemble fourni des surfaces spatiales.
   * Classer les surfaces spatiales comme ajouté, modifié ou supprimé.
   * Pour chaque surface spatiale ajouté ou modifié, le cas échéant, soumettre une demande asynchrone pour recevoir des mises à jour de maillage représentant l’état actuel de l’aire au niveau de détail souhaité.
* Traiter la demande asynchrone maille (plus de détails dans les sections suivantes).

## <a name="mesh-caching"></a>La mise en cache de maillage

Surfaces spatiales sont représentées par des maillages de triangle dense. Stockage, de rendu et le traitement de ces panneaux peuvent consommer des ressources de calcul et de stockage importantes. Par conséquent, chaque application doit adopter une maille de la mise en cache de schéma appropriée à ses besoins, afin de réduire les ressources utilisées pour le stockage et traitement de la maille. Ce schéma doit déterminer des maillages à conserver et à ignorer, ainsi que quand mettre à jour de la maille de chaque surface spatiale.

La plupart des considérations abordées ici informe directement comment votre application doit être proche de la mise en cache d’une maille. Vous devez envisager comment l’utilisateur parcourt l’environnement, les surfaces sont nécessaires, lorsque les différentes surfaces seront arrêtées et lorsque les modifications dans l’environnement doivent être capturées.

Lors de l’interprétation de l’événement 'surfaces modifié' fourni par l’aire de conception observateur, la maille base logique de la mise en cache est la suivante :
* Si l’application voit un ID de surface spatial qui n’a pas vu avant, il doit le traiter comme une surface spatiale.
* Si l’application voit une surface spatiale avec un ID connu, mais avec une nouvelle heure de mise à jour, il doit traiter ceci comme une surface spatiale mis à jour.
* Si l’application ne détecte plus une surface spatiale avec un ID connu, il doit le traiter comme une surface spatiale supprimée.

C’est à chaque application à puis choisissez les options suivantes :
* Pour les nouvelles surfaces spatiales, maille doit être demandée ?
   * En règle générale maille doit être demandée immédiatement pour les nouvelles surfaces spatiales, qui peuvent fournir de nouvelles informations utiles à l’utilisateur.
   * Toutefois, les nouvelles surfaces spatiales près et devant l’utilisateur doivent être prioritaires et leur maille doit être demandée tout d’abord.
   * Si le nouveau maillage n’est pas nécessaire, si par exemple l’application a définitivement ou temporairement « figée » son modèle de l’environnement, puis il ne doit pas être demandée.
* Pour les surfaces spatiales mis à jour, maille doit être demandée ?
   * Mise à jour de surfaces spatiales près et devant l’utilisateur doivent être prioritaires et leur maille doit être demandée tout d’abord.
   * Il peut également être appropriée donner une priorité plus élevée aux surfaces de nouveau qu’à la mise à jour de surfaces, en particulier au cours de l’expérience d’analyse.
   * Pour limiter les coûts de traitement, les applications peuvent souhaiter limiter la fréquence à laquelle ils traitent les mises à jour aux surfaces spatiales.
   * Il peut être possible de déduire que les modifications apportées à une surface spatiale sont mineures, par exemple si les limites de la surface sont petits, auquel cas la mise à jour ne peut pas être suffisamment important pour les processus.
   * Mises à jour aux surfaces spatiales en dehors de la zone d’intérêt de l’utilisateur en cours peuvent être ignorés entièrement, bien que dans ce cas, il peut être plus efficace pour modifier les volumes englobants spatiales en cours d’utilisation par l’aire de conception observateur.
* Pour les surfaces spatiales supprimés, maille doit être supprimé ?
   * En règle générale maille doit être ignoré en immédiatement pour les surfaces spatiales supprimés, afin que les occlusion hologramme reste correcte.
   * Toutefois, si l’application a des raisons de croire qu’une surface spatiale s’affiche à nouveau peu de temps (peut-être en fonction de la conception de l’expérience utilisateur), il peut être plus efficace pour être conservé que to ignorer son maillage et le recréer ultérieurement.
   * Si un modèle à grande échelle de l’environnement utilisateur est créée à l’application puis elle pas souhaitera peut-être ignorer les mailles du tout. Il sera toujours besoin de limiter l’utilisation des ressources, éventuellement en mailles de mise en attente sur le disque comme surfaces spatiales disparaissent.
   * Notez que certains événements relativement rares lors de la génération de surface spatiale peuvent entraîner des surfaces spatiales à remplacer par les nouvelles surfaces spatiales dans un emplacement similaire, mais avec des ID différents. Par conséquent, les applications que vous choisissez de ne pas ignorer une surface supprimée votre attention pas à la fin de plusieurs hautement overlapped spatial surface maillages couvrant le même emplacement.
* Maillage doit être ignoré pour d’autres surfaces spatiales ?
   * Même lorsqu’il existe une surface spatiale, si elle n’est plus utile de l’expérience utilisateur puis, il doit être ignoré. Par exemple, si l’application 'remplace' la salle de l’autre côté d’une porte ouverte par un autre espace virtuel puis les surfaces spatiales dans cet espace n’est plus important.

Voici une stratégie exemple maille mise en cache, à l’aide des hystérésis spatiales et temporelles :
* Considérez une application qui souhaite utiliser un volume spatial en forme frustum d’intérêt qui suit le regard de l’utilisateur car elles observer cet onglet et Parcourir.
* Une surface spatiale peut-être disparaître temporairement de ce volume simplement parce que l’utilisateur recherche la surface ou étapes supplémentaires depuis celle-ci... à l’examen ou se rapproche de nouveau un peu plus tard. Dans ce cas, en supprimant et en recréer la maille pour cette aire représente beaucoup de traitement redondant.
* Pour réduire le nombre de modifications traitées, l’application utilise deux observateurs surfaces spatiales, un contenu dans l’autre. Le plus grand volume est sphérique et suit l’utilisateur tardivement ; Il déplace uniquement lorsque cela est nécessaire pour vous assurer que son centre se trouve dans 2.0 mètres de l’utilisateur.
* Les mailles surfaces spatiales nouveaux et mis à jour sont toujours traitées à partir de l’Observateur surface interne le plus petit, mais les mailles sont mis en cache jusqu'à ce qu’elles disparaissent de l’Observateur de surface externe plus grande. Cela permet à l’application éviter le traitement de nombreuses modifications redondantes due au déplacement des utilisateurs locaux.
* Dans la mesure où une surface spatiale peut également disparaître temporairement en raison de suivi de la perte, l’application diffère également rejet surfaces spatiales supprimés au cours de suivi de la perte.
* En général, une application doit évaluer le compromis entre la mise à jour réduit le traitement et l’utilisation accrue de la mémoire afin de déterminer sa stratégie de mise en cache idéale.

## <a name="rendering"></a>Rendu

Il existe trois méthodes principales dans lequel les mailles de mappage spatial ont tendance à être utilisée pour le rendu :
* Pour la visualisation de l’aire de conception
   * Il est souvent utile de visualiser les surfaces spatiales directement. Par exemple, 'shadows de conversion' à partir d’objets sur les surfaces spatiales peuvent fournir visuelles utiles à l’utilisateur pendant qu’ils sont mise hologrammes sur les surfaces.
   * Une chose à l’esprit est que mailles spatiales sont différents pour le genre de mailles un artiste 3D peut créer. La topologie de triangle ne sera pas aussi « propre » que topologie créés par l’homme et la maille subira des [diverses erreurs](spatial-mapping-design.md#what-influences-spatial-mapping-quality).
   * Pour créer une esthétique visual agréable, vous pouvez souhaiter donc effectuer certaines [mesh traitement](spatial-mapping.md#mesh-processing), par exemple pour les trous de remplissage ou de normales de surface lisses. Vous pouvez également utiliser un nuanceur à textures conçues par l’artiste de projet sur votre maillage au lieu de la visualisation directement la topologie de maille et normales.
* D’occlusion hologrammes derrière les surfaces du monde réel
   * Surfaces spatiaux peuvent être rendus dans un test de profondeur qui affecte uniquement le [tampon de profondeur](https://msdn.microsoft.com/library/windows/desktop/bb219616(v=vs.85).aspx) et n’affecte pas les cibles de rendu de couleur.
   * Cela prépare la mémoire tampon de profondeur pour occlude restitué par la suite les hologrammes derrière les surfaces spatiales. Occlusion précise de hologrammes améliore le sens que hologrammes existent réellement dans l’espace physique de l’utilisateur.
   * Pour activer le rendu de profondeur uniquement, mettre à jour votre état de fusion pour définir le [RenderTargetWriteMask](https://msdn.microsoft.com/library/windows/desktop/hh404492(v=vs.85).aspx) à zéro pour la couleur de toutes les cibles de rendu.
* Pour modifier l’apparence de hologrammes bloqués par les surfaces du monde réel
   * Géométrie normalement rendu est masqué quand il est bloqué. Pour cela en définissant la fonction de profondeur dans votre [état du stencil de profondeur](https://msdn.microsoft.com/library/windows/desktop/ff476110(v=vs.85).aspx) à « inférieur ou égal », ce qui entraîne la géométrie à être visible que s’il est **plus en détail** à l’appareil photo que tous les rendus précédemment géométrie.
   * Toutefois, il peut être utile de conserver certains géométrie visible même quand il est bloqué et modifier son apparence lorsque bloqués comme un moyen de fournir des commentaires visuels à l’utilisateur. Par exemple, cela permet à l’application afficher l’utilisateur de l’emplacement d’un objet tout en rendant plus clair que se trouve derrière une surface du monde réel.
   * Pour ce faire, afficher la géométrie une deuxième fois avec un nuanceur de différentes qui crée l’apparence souhaitée « bouché ». Avant le rendu de la géométrie pour la deuxième fois, apporter deux modifications à votre [état du stencil de profondeur](https://msdn.microsoft.com/library/windows/desktop/ff476110(v=vs.85).aspx). Tout d’abord, la valeur est la fonction de profondeur « supérieur ou égal à » afin que la géométrie sera visible uniquement lorsqu’il est **plus** à partir de l’appareil photo à toute la géométrie précédemment rendue. Ensuite, définissez le DepthWriteMask à zéro, afin que la mémoire tampon de profondeur ne sera pas modifié (le tampon de profondeur doit continuer représenter la profondeur de la géométrie **le plus proche** à l’appareil photo).

[Performances](understanding-performance-for-mixed-reality.md) est une préoccupation importante lors du rendu des mailles de mappage spatial. Voici quelques techniques de performances de rendu spécifiques au rendu des mailles de mappage spatial :
* Ajuster la densité de triangle
   * Lors de la surface spatiale demandeur maille à partir de votre aire de conception observateur, demander la densité la plus basse des maillages de triangle est suffisante pour vos besoins.
   * Il peut être judicieux pour faire varier la densité de triangle sur une base de la surface en surface, en fonction de la distance de la surface de l’utilisateur et sa pertinence dans l’expérience utilisateur.
   * Nombres de triangle réduire permet de réduire l’utilisation de mémoire et les coûts de traitement de vertex sur le GPU, bien que cela n’affectera pas les coûts de traitement de pixels.
* Effectue l’élimination de frustum
   * Élimination de frustum ignore les objets de dessin qui ne sont pas visibles, car elles sont en dehors de la frustum affichage actuel. Cela réduit les coûts de traitement CPU et GPU.
   * Dans la mesure où l’élimination est effectuée sur une base par maille et surfaces spatiaux peuvent être volumineux, avec rupture chaque maillage de surface spatiale en segments plus petits peut entraîner l’élimination plus efficace (où moins triangles hors écran sont rendus). Il existe un compromis, toutefois ; les mailles plus que vous avez, les appels de dessin plus que vous devez vous, ce qui peuvent augmenter les coûts de processeur. Dans un cas extrême, le frustum élimination de calculs eux-mêmes peut même avoir un coût UC mesurable.
* Ajuster l’ordre de rendu
   * Surfaces spatiales ont tendance à être volumineuses, car ils représentent un environnement de l’utilisateur qui les entoure. Les coûts sur le GPU de traitement de pixels peut être élevée, en particulier dans les cas où il existe plusieurs couches de géométrie visible (y compris les surfaces spatiales et autres hologrammes). Dans ce cas, la couche plus proche de l’utilisateur sera être OCCLUSION des couches plus tout de suite, afin de n’importe quel GPU temps ces couches plus éloignées de rendu est gaspillée.
   * Pour réduire ce travail redondant sur le GPU, il est utile de surfaces opaques s’affichent dans l’ordre de l’avant vers l’arrière (ceux qui sont plus en détail tout d’abord, plus éloignées de celles de la dernière). Par « opaque » nous entendons les surfaces pour lequel le DepthWriteMask est défini sur 1 dans votre [état du stencil de profondeur](https://msdn.microsoft.com/library/windows/desktop/ff476110(v=vs.85).aspx). Lorsque les surfaces le plus proche sont restitués, ils seront amorcer le tampon de profondeur afin que les surfaces plus longues sont efficacement ignorés par le processeur de pixels sur le GPU.

## <a name="mesh-processing"></a>Traitement de maillage

Une application peut souhaiter effectuer [diverses opérations](spatial-mapping.md#mesh-processing) sur des mailles surfaces spatiales en fonction de ses besoins. Les données d’index et de sommet fournies avec chaque maillage de surface spatiale utilisent la même disposition familier comme le [mémoires tampons de vertex et d’index](https://msdn.microsoft.com/library/windows/desktop/bb147325%28v=vs.85%29.aspx) qui sont utilisés pour le rendu des maillages de triangle dans le rendu moderne toutes les API. Toutefois, les faits clés à connaître est que les triangles mappage spatial ont un **front-dans le sens horaire ordre d’enroulement**. Chaque triangle est représenté par trois index de vertex dans la mémoire tampon d’index de la maille et ces index identifiera les vertex du triangle dans un **dans le sens horaire** ordre, le triangle est affiché dans le **front** côté. Début côté (ou de l’extérieur) des maillages de surface spatiales correspond évidemment à la face avant (visible) des surfaces du monde réel.

Les applications doivent réaliser uniquement simplification de maille si la densité de triangle plus grossière fournie par l’aire de conception observateur est toujours insuffisamment grossier, ce travail calculs est onéreux et déjà en cours d’exécution par le runtime pour générer les différents fourni des niveaux de détail.

Étant donné que chaque aire de conception observateur puisse fournir plusieurs surfaces spatiales non connectés, certaines applications souhaiterez peut-être ajuster ces données spatiales surface maillages contre chaque glissière autre, puis à leur ensemble. En règle générale, l’étape de découpage est nécessaire, comme les plus proches des maillages de surface spatiales souvent se chevauchent légèrement.

## <a name="raycasting-and-collision"></a>Raycasting et Collision

Dans l’ordre pour un API physique (tel que [Havok](http://www.havok.com/)) pour fournir une application avec des fonctionnalités raycasting et de collision pour les surfaces spatiales, l’application doit fournir la surface spatiale maillages à l’API physique. Les mailles souvent utilisées pour physique ont les propriétés suivantes :
* Elles contiennent uniquement de petits nombres de triangles. Opérations de physique sont plus intensifs que les opérations de rendu.
* Ils sont « eau étroite ». Surfaces destinées à être solid ne doivent pas avoir de petits trous dans mêmes trous trop petits pour être visible peuvent entraîner des problèmes.
* Ils sont convertis en balles convexes. Convexe ont plusieurs polygones issues et sont libres de trous, et ils sont beaucoup plus de calculs efficaces pour traiter que les maillages de triangle brutes.

Lorsque raycasts performantes par rapport à surfaces spatiales, n’oubliez pas que ces surfaces sont souvent complexes, formes encombrés complètes des détails peu confuses - simples comme votre bureau ! Cela signifie qu’un seul raycast est souvent insuffisant pour vous donner suffisamment d’informations sur la forme de la surface et la forme de l’espace vide de proximité. Il est donc généralement une bonne idée pour effectuer de nombreuses raycasts au sein d’une petite zone et à utiliser les résultats d’agrégation pour dériver une compréhension plus fiable de la surface. Par exemple, à l’aide de la moyenne des 10 raycasts guide hologramme placement sur une aire de produira un résultat beaucoup plus lisse et moins instable qui utilise simplement un raycast unique.

Toutefois, n’oubliez pas que chaque raycast peut avoir un coût élevé de calcul. Par conséquent, en fonction de votre scénario d’utilisation vous devez compenser le coût de calcul de raycasts supplémentaires (effectuée chaque trame) sur le coût de calcul [mesh traitement](spatial-mapping.md#mesh-processing) lisse et de supprimer des trous dans les surfaces spatial ( effectuée lorsque les mailles spatiales sont mis à jour).

## <a name="troubleshooting"></a>Résolution des problèmes
* Dans l’ordre pour les panneaux de surface d’exposition être correctement orienté, chaque GameObject doit être active avant d’être envoyé à la SurfaceObeserver d’avoir son maillage construit. Sinon, les panneaux seront afficheront dans votre espace mais paysage en bizarres angles.
* Le GameObject qui exécute le script qui communique avec le SurfaceObserver doit être définie à l’origine. Sinon, tous les GameObjects que vous créez et envoyez à la SurfaceObserver pour avoir leurs mailles construits comporte un décalage égal au décalage de l’objet de jeu de Parent. Cela peut rendre votre mailles affichent plusieurs mètres ce qui le rend très difficile de déboguer ce qui se passait.

## <a name="see-also"></a>Voir aussi
* [Systèmes de coordonnées](coordinate-systems.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)
* [Mappage spatial dans Unity](spatial-mapping-in-unity.md)
* [Conception de mappage spatial](spatial-mapping-design.md)
* [Étude de cas - parcourant des trous dans la réalité](case-study-looking-through-holes-in-your-reality.md)
