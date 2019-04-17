---
title: Conception de mappage spatial
description: Utilisation efficace de mappage spatial dans HoloLens nécessite une attention particulière de nombreux facteurs.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Mappage de Windows Mixed Reality, conception, spatiale, HoloLens, surface reconstruction, maillage
ms.openlocfilehash: d2ddcbf9458769a60cd3ed2871c5f3405c75f10c
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593379"
---
# <a name="spatial-mapping-design"></a>Conception de mappage spatial

Utilisation efficace de mappage spatial dans HoloLens nécessite une attention particulière de nombreux facteurs.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> Mappage spatial</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

## <a name="why-is-spatial-mapping-important"></a>Pourquoi le mappage spatial est-elle importante ?

Mappage spatial rend possible de placer des objets sur des surfaces réels. Cela vous aide à des objets d’ancrage dans le monde de l’utilisateur et tire parti des signaux de profondeur de monde réel. OCCLUSION votre hologrammes selon d’autres hologrammes et les objets du monde réel, vous aide à convaincre l’utilisateur à qui ces hologrammes sont réellement dans leur espace. Hologrammes flottant dans l’espace ou à l’utilisateur ne se sentira pas est de type real. Dans la mesure du possible, les éléments de place pour plus de confort.

Visualiser les surfaces lors placement ou du déplacement hologrammes (utiliser une simple grille prévue). Cela vous aidera à l’utilisateur de savoir où ils peuvent placer mieux leurs hologrammes et indique l’utilisateur si la place, ils essaient de placer l’hologramme n’a pas encore été mappée. Vous pouvez « tableau éléments » vers l’utilisateur si elles se retrouvent au trop grand nombre d’un angle.

## <a name="what-influences-spatial-mapping-quality"></a>Élément qui influence la qualité de mappage spatial ?

Afin de fournir la meilleure expérience utilisateur, il est important de comprendre les facteurs qui affectent la qualité des données de mappage spatial collectées par HoloLens.

Erreurs dans les données de mappage spatial se répartissent en trois catégories :
* **Trous**: Surfaces du monde réel sont manquants dans les données de mappage spatial.
* **Délirante**: Surfaces existent dans les données de mappage spatial qui n’existent pas dans le monde réel.
* **Écart**: Surfaces dans les données de mappage spatial sont manière imparfaite alignées avec des surfaces de monde réel, soit envoyé ou extraites.

Plusieurs facteurs peuvent affecter la fréquence et la gravité de ces erreurs :

* **Mouvement de l’utilisateur**
   * Comment l’utilisateur progresse dans leur environnement détermine quelle mesure l’environnement sera analysé, afin de l’utilisateur peut nécessiter des conseils afin d’obtenir une bonne analyse.
   * L’appareil photo utilisé pour l’analyse fournit des données dans un cône 70 degrés, à partir d’un minimum de 0,8 mètres à un maximum de distance de compteurs 3.1 à partir de l’appareil photo. Surfaces du monde réel ne sera analysés que dans ce champ de vision. Notez que ces valeurs sont susceptibles de changer dans les futures versions.
   * Si l’utilisateur n’obtienne jamais dans 3.1 mètres d’un objet, il ne sera pas analysé.
   * Si l’utilisateur le consulte uniquement un objet à partir d’une distance inférieure à 0,8 mètres, il ne sera pas analysé (Cela évite de devoir analyser les mains de l’utilisateur).
   * Si l’utilisateur jamais recherche vers le haut (ce qui est assez normal), le plafond sera probablement pas analysé.
   * Si un utilisateur ne semble jamais derrière un meuble ou d’un mur, les objets bloqués par leur ne seront pas analysés.
   * Surfaces ont tendance à être analysés de meilleure qualité lorsqu’ils sont visualisés front plutôt que selon un angle superficiels.
   * Si le système de suivi de la tête de la HoloLens échoue momentanément (qui peut se produire en raison de mouvement de l’utilisateur rapide, d’éclairage faible, murs larges ou les caméras devenir couverte), cela peut introduire des erreurs dans les données de mappage spatial. De telles erreurs seront corrigées au fil du temps que l’utilisateur continue à se déplacer et de leur environnement d’analyse.

* **Supports de l’aire de conception**
   * Les documents trouvés sur les surfaces de réels varient considérablement. Impact sur la qualité de mappage spatial, données, car elles affectent la lumière infrarouge sont reflétées.
   * Surfaces foncées peut ne pas analyser jusqu'à ce qu’ils soient plus proches de l’appareil photo, car ils reflètent le moins de lumière.
   * Des surfaces peut-être donc foncées qu’ils reflètent trop peu clair pour être analysée à partir de n’importe quelle distance, afin qu’ils seront également introduire des erreurs de trou à l’emplacement de la surface et parfois derrière la surface.
   * Peuvent analyser uniquement les surfaces brillantes en particulier lorsqu’ils sont affichés front, mais ne pas affichés à partir d’un angle superficiels.
   * Miroirs, parce qu’elles créent des réflexions illusory des espaces réels et des surfaces, peuvent provoquer des erreurs de trou et les erreurs hallucination.

* **Mouvement de la scène**
   * Mappage spatial s’adapte rapidement aux changements dans l’environnement, telles que le déplacement de personnes ou d’ouverture et de fermeture des portes.
   * Toutefois, mappage spatial peut uniquement s’adapter aux modifications dans une zone lorsque cette zone est clairement visible à l’appareil photo qui est utilisé pour l’analyse.
   * Pour cette raison, il est possible pour cette adaptation rester derrière la réalité, ce qui peut entraîner des erreurs trou ou hallucination.
   * Par exemple, un utilisateur analyse un ami, puis met tandis que l’ami quitte la salle. Une représentation sous forme de « ghost » de l’ami (une erreur hallucination) persistera dans les données de mappage spatial, jusqu'à ce que l’utilisateur reprend et nouvelle analyse l’espace où l’ami a été permanent.

* **Interférence de l’éclairage**
   * La lumière ambiante infrarouge dans la scène peut-être interférer avec l’analyse, par exemple du soleil fort provenant d’une fenêtre.
   * Les surfaces brillantes en particulier peuvent interférer avec l’analyse des surfaces à proximité, la lumière rebondissements sur les erreurs de décalage à l’origine.
   * Les surfaces brillantes réflexion de lumière directement dans l’appareil photo peuvent interférer avec espace proche, en provoquant flottante délirante air en milieu ou en retardant l’adaptation de mouvement de la scène.
   * Deux appareils HoloLens dans la même salle ne doivent pas interférer avec l’autre, mais la présence de plus de cinq appareils HoloLens peut provoquer des interférences.

Il peut être possible d’éviter ou de corriger certains de ces erreurs. Toutefois, vous devez concevoir votre application afin que l’utilisateur est en mesure d’atteindre leurs objectifs même en présence d’erreurs dans les données de mappage spatial.

## <a name="the-environment-scanning-experience"></a>L’environnement d’expérience d’analyse

HoloLens apprend sur les surfaces de son environnement, comme l’utilisateur consulte. Au fil du temps, le HoloLens construit une analyse de toutes les parties de l’environnement qui ont été observés. Il met également à jour l’analyse comme les modifications de l’environnement sont observées. Cette analyse est automatiquement conservées entre lancements d’applications.

Chaque application qui utilise le mappage spatial doit prendre en compte prévisibilité « analyse » ; le processus par le biais duquel l’application guide l’utilisateur afin d’analyser les surfaces qui sont nécessaires pour l’application fonctionne correctement.

![Exemple d’analyse](images/sr-mixedworld-140429-8pm-00068-1000px.png)<br>
*Exemple d’analyse*

La nature de cette expérience d’analyse peut varier considérablement en fonction des besoins de chaque application, mais deux principes essentiels doivent guider sa conception.

Tout d’abord, **effacer la communication avec l’utilisateur est la principale préoccupation**. L’utilisateur doit toujours être conscient de si les exigences de l’application sont respectés. Quand ils ne sont pas respectées, il doit être immédiatement claire pour l’utilisateur pourquoi c’est le cas, et ils doivent être rapidement a conduit à prendre les mesures appropriées.

Deuxièmement, **applications doivent tenter de trouver un équilibre entre l’efficacité et la fiabilité**. Quand il est possible de faire **fiable**, les applications doivent analyser automatiquement les données de mappage spatial pour gagner du temps de l’utilisateur. Lorsqu’il n’est pas possible de faire de manière fiable, applications doivent activer l’utilisateur à fournir rapidement l’application avec les informations supplémentaires que nécessaires à la place.

Pour aider à concevoir l’expérience d’analyse de droite, tenez compte parmi les possibilités suivantes s’appliquent à votre application :

* **Aucune expérience d’analyse**
   * Une application peut fonctionner parfaitement sans aucune expérience d’analyse interactive ; Il sera en savoir plus sur les surfaces qui sont observés au cours de déplacement de l’utilisateur naturelle.
   * Par exemple une application qui permet à l’utilisateur de dessiner sur les surfaces avec spraypaint HOLOGRAPHIQUE requiert des connaissances uniquement des surfaces actuellement visibles par l’utilisateur.
   * L’environnement peut être complètement analysé déjà s’il s’agit d’un dans lequel l’utilisateur a déjà passé beaucoup de temps à l’aide de la HoloLens.
   * N’oubliez pas cependant que l’appareil photo utilisé par le mappage spatial ne peut voir 3,1 m devant l’utilisateur, par conséquent, mappage spatial ne saurez pas sur des surfaces plus éloignées, sauf si l’utilisateur a les observé à partir d’une distance plus en détail dans le passé.
   * L’utilisateur comprenne bien les surfaces ont été analysés, l’application doit fournir des commentaires visuels à cet effet, par exemple le cast shadows virtuels sur les surfaces numérisés peut aider l’utilisateur placer hologrammes sur ces surfaces.
   * Dans ce cas, les volumes englobant de l’Observateur de surface spatiale doivent être mis à jour de chaque image à un verrouillage de corps [système de coordonnées spatial](coordinate-systems.md), afin qu’elles suivent l’utilisateur.

* **Recherchez un emplacement approprié**
   * Une application peut être conçue pour une utilisation dans un emplacement avec des exigences spécifiques.
   * Par exemple, l’application peut nécessiter une zone vide autour de l’utilisateur afin qu’ils peuvent exercer en toute sécurité karateka HOLOGRAPHIQUE.
   * Les applications doivent communiquer des exigences spécifiques à l’utilisateur initial et renforcer les commentaires visuelle claire.
   * Dans cet exemple, l’application doit visualiser l’étendue de la zone vide requise et mettre en évidence visuellement de la présence de tous les objets indésirables dans cette zone.
   * Dans ce cas, les volumes englobant de l’Observateur de surface spatiale doivent utiliser verrouillé par un monde [système de coordonnées spatial](coordinate-systems.md) dans l’emplacement choisi.

* **Rechercher une configuration appropriée des surfaces**
   * Une application peut nécessiter une configuration spécifique des surfaces, par exemple deux grandes, plate, opposées murs pour créer un hall holographique de miroirs.
   * Dans ce cas, l’application devra analyser les surfaces fournies par le mappage spatial pour détecter les surfaces adaptées et diriger l’utilisateur vers eux.
   * L’utilisateur doit avoir une option de secours si l’analyse de la surface de l’application n’est pas entièrement fiable. Par exemple, si l’application identifie incorrectement une voie d’accès comme un mur plat, l’utilisateur a besoin d’un moyen simple pour corriger cette erreur.

* **Partie de l’environnement d’analyse**
   * Une application peut souhaiter capturer uniquement la partie de l’environnement, comme indiqué par l’utilisateur.
   * Par exemple, l’application balaie partie d’un espace pour l’utilisateur peut publier une annonce classique HOLOGRAPHIQUE pour meuble qu’ils souhaitent vendre.
   * Dans ce cas, l’application doit capturer les données de mappage spatial dans les régions observées par l’utilisateur lors de leur analyse.

* **Analyse de la salle d’ensemble**
   * Une application peut nécessiter une analyse de toutes les surfaces dans la salle, y compris ceux derrière l’utilisateur.
   * Par exemple, un jeu peut affecter l’utilisateur au rôle de Gulliver, sous siege parmi des centaines de minuscules Lilliputians approche à partir de toutes les directions.
   * Dans ce cas, l’application devra déterminer combien des surfaces en cours de l’espace ont déjà été analysés et diriger les regards de l’utilisateur pour combler les lacunes significatives.
   * La clé pour ce processus fournit des commentaires visuels qui rend clairement à l’utilisateur les surfaces qui n’ont pas encore été analysés. L’application peut par exemple utiliser [brouillard basé sur une distance](https://msdn.microsoft.com/library/windows/desktop/bb173401%28v=vs.85%29.aspx) pour mettre en évidence visuellement des régions qui ne sont pas couverts par les surfaces de mappage spatial.

* **Prenez un instantané de l’environnement**
   * Une application peut souhaiter ignorer toutes les modifications dans l’environnement après réception d’un « instantané » initial.
   * Cela peut être appropriée pour éviter toute interruption de données créés par l’utilisateur qui sont étroitement liées à l’état initial de l’environnement.
   * Dans ce cas, l’application doit faire une copie des données de mappage spatial dans son état initial une fois que l’analyse est terminée.
   * Les applications doivent continuer à recevoir des mises à jour les données de mappage spatial si hologrammes doivent toujours être correctement bloqués par l’environnement.
   * Mises à jour continues des données de mappage spatial permettent également de visualiser toutes les modifications qui se sont produites, clarifier les différences entre les états antérieurs et présentes de l’environnement à l’utilisateur.

* **Prendre des instantanés initiée par l’utilisateur de l’environnement**
   * Une application peut souhaiter uniquement répondre aux modifications d’ordre environnemental lorsqu’il par l’utilisateur.
   * Par exemple, l’utilisateur peut créer plusieurs 3D 'statues » d’un ami en capturant leurs risque de poser à des moments différents.

* **Autoriser l’utilisateur à modifier l’environnement**
   * Une application peut être conçue pour répondre en temps réel pour toutes les modifications apportées dans l’environnement utilisateur.
   * Par exemple, l’utilisateur un rideau de dessin peut déclencher de changement de scène pour une lecture HOLOGRAPHIQUE ayant lieu sur l’autre côté.

* **Guide de l’utilisateur pour éviter les erreurs dans les données de mappage spatial**
   * Une application peut souhaiter fournissent des instructions à l’utilisateur pendant qu’ils sont analyse leur environnement.
   * Cela peut aider à l’utilisateur afin d’éviter certains types de [erreurs dans les données de mappage spatial](spatial-mapping-design.md#what-influences-spatial-mapping-quality), par exemple en restant en dehors de windows sunlit ou miroirs.

Un détail supplémentaire à connaître est que la plage de données de mappage spatial n’est pas un nombre illimitée. Tandis que le mappage spatial génère une base de données permanente de grands espaces, il établit uniquement ces données disponibles pour les applications dans une bulle de taille limitée autour de l’utilisateur. Par conséquent, si vous commencez au début d’un couloir long et le parcours assez loin de début, puis finalement les surfaces spatiales au début disparaît. Vous pouvez bien sûr atténuer ce risque en mettant en cache ces surfaces dans votre application une fois qu’ils ont disparu à partir des données de mappage spatial disponible.

## <a name="mesh-processing"></a>Traitement de maillage

Il peut être utile pour détecter les types courants d’erreurs dans les surfaces et à filtrer, supprimer ou modifier les données de mappage spatial comme il convient.

N’oubliez pas que le mappage spatial données sont destinées à être aussi fidèle que possible aux surfaces du monde réel, par conséquent, tout traitement vous appliquez les risques de décalage de vos surfaces plus éloigné de la vérité »'.

Voici quelques exemples de différents types de maillage de traitement que vous pouvez trouver utiles :

* **Remplissage des trous**
   * Si un petit objet constitué d’un matériau foncé ne parvient pas à analyser, il laissera une faille dans la surface environnante.
   * Trous affectent occlusion : hologrammes sont consultables « par « un trou dans une surface réalistes soi-disant opaque.
   * Trous affectent raycasts : Si vous utilisez raycasts pour aider les utilisateurs à interagir avec des surfaces, il est peut-être pas souhaitable pour ces des rayons à passer par les failles. Une atténuation consiste à utiliser un ensemble de plusieurs raycasts couvrant une zone de taille appropriée. Cela vous permettra de filtrer les résultats de la « valeur hors norme », afin que même si un raycast traverse un petit trou, le résultat du regroupement sera toujours valide. Toutefois, n’oubliez pas que cette approche a un coût de calcul.
   * Trous affectent les collisions physique : un objet contrôlé par simulation physique peut supprimer par un trou de l’étage et se perdent.
   * Il est possible de façon algorithmique remplir ces trous dans la maille superficielle. Toutefois, vous devrez régler votre algorithme afin que les trous réels telles que windows et les guichets ne pas remplis. Il peut être difficile de différencier fiable des trous réels à partir de « trous imaginaires », vous devrez faire des essais avec différents paramètres heuristiques tels que « size » et « forme limite ».

* **Suppression de hallucination**
   * Réflexions, des lumières et déplacement d’objets peut laisser des petites en attente 'délirante' flottante en l’air.
   * Délirante affecte occlusion : délirante peut-être devenir visibles en tant que formes foncées déplacement devant et OCCLUSION autres hologrammes.
   * Délirante affecte raycasts : Si vous utilisez raycasts pour aider les utilisateurs à interagir avec des surfaces, ces rayons pouvaient atteindre une hallucination au lieu de la surface derrière lui. Comme avec les trous, une atténuation consiste à utiliser les nombreuses raycasts au lieu d’un raycast unique, mais là encore cela se fera à un coût de calcul.
   * Délirante affectent physique collisions : un objet contrôlé par simulation physique peut se bloquer sur une hallucination et son incapacité à déplacer dans une zone apparemment claire d’espace.
   * Il est possible de filtrer ces délirante à partir de la maille superficielle. Toutefois, comme avec les trous, vous devez régler votre algorithme afin que les petites réel objets tels que lamp-stands et poignées des portes ne sont pas supprimées.

* **Lissage**
   * Mappage spatial peut retourner les surfaces qui semblent être approximative ou bruyant par rapport à leurs équivalents du monde réel.
   * Lissage affecte les collisions physique : si la valeur plancher est approximatif, une balle de golf physiquement simulé peuvent se pas déployer sans heurts entre il dans une ligne droite.
   * Lissage affecte le rendu : si une surface est visualisée directement, les normales de surface rugueuses peuvent affecter son apparence et interrompre un coup de œil « nettoyage ». Il est possible de ce problème en utilisant un éclairage approprié et les textures dans le nuanceur est utilisé pour restituer la surface.
   * Il est possible de lisser irrégularité dans une maille superficielle. Toutefois, cela peut pousser la surface davantage la surface réel correspondant. Maintenir une correspondance étroite est important pour produire d’occlusion hologramme précis et permet aux utilisateurs d’obtenir des interactions précises et prévisibles avec des surfaces HOLOGRAPHIQUE.
   * Si seule une modification cosmétique est nécessaire, il peut être suffisant lisser les normales des sommets sans modifier les positions de vertex.

* **Recherche de plan**
   * Il existe de nombreux formulaires d’analyse une application pouvez souhaiter effectuer sur les surfaces de mappage spatial.
   * Constitue un exemple simple « du plan de recherche » ; identification des régions délimitées, principalement PLANAIRE des surfaces.
   * Régions planaires peuvent servir de HOLOGRAPHIQUE-surfaces de travail, les régions où HOLOGRAPHIQUE contenu peut être placé automatiquement par l’application.
   * Régions planaires peuvent contraindre l’interface utilisateur, pour guider les utilisateurs pour interagir avec les surfaces de leurs besoins.
   * Régions planaires utilisable comme dans le monde réel, pour HOLOGRAPHIQUE équivalents à des objets fonctionnelles tels que les écrans LCD, des tables ou des tableaux blancs.
   * Régions planaires peuvent définir des zones de play, qui forment la base de niveaux de jeu vidéo.
   * Planaires régions peuvent aider les agents virtuels pour naviguer le monde réel, en identifiant les zones de l’étage que des personnes réelles sont susceptibles de remonter sur.

## <a name="prototyping-and-debugging"></a>Prototypage et débogage

### <a name="useful-tools"></a>Outils utiles
* Le [HoloLens émulateur](using-the-hololens-emulator.md) peut être utilisé pour développer des applications à l’aide du mappage spatial sans accès à un HoloLens physique. Il vous permet de simuler une session en direct sur un HoloLens dans un environnement réaliste, avec toutes les données de votre application serait normalement consommer, notamment HoloLens motion, systèmes de coordonnées spatiales et les mailles de mappage spatial. Cela peut servir à fournir l’entrée fiable et renouvelable, ce qui peut être utile pour le débogage des problèmes et d’évaluer les modifications apportées à votre code.
* Pour reproduire des scénarios, capturer des données de mappage spatial sur le réseau à partir d’un HoloLens en direct, puis enregistrez-le disque et le réutiliser dans des sessions de débogage suivantes.
* Le [vue 3D portail des appareils Windows](using-the-windows-device-portal.md#3d-view) fournit un moyen de voir toutes les surfaces spatiales actuellement disponibles via le système de mappage spatial. Cela fournit une base de comparaison pour les surfaces spatiales à l’intérieur de votre application ; par exemple vous pouvez facilement vérifier si toutes les surfaces spatiales manquent ou sont affichés au mauvais endroit.

### <a name="general-prototyping-guidance"></a>Conseils de création de prototypes général
* Étant donné que [erreurs](spatial-mapping-design.md#what-influences-spatial-mapping-quality) dans le mappage spatial data peut fortement affectent l’expérience utilisateur, nous vous recommandons de tester votre application dans une grande variété d’environnements.
* Ne pas obtenir interceptées l’habitude de toujours tester dans le même emplacement, par exemple à votre bureau. Veillez à tester sur différentes surfaces des positions différentes, les formes, les tailles et les documents.
* De même, tandis que les données synthétiques ou enregistrées peuvent être utiles pour le débogage, ne deviennent trop dépend de même les rares cas de test. Cela peut retarder la recherche des problèmes importants qui aurait détecté plus variées test précédemment.
* Il est judicieux d’effectuer des tests avec des utilisateurs réels (et dans l’idéal, non surveillées), car ils ne peuvent pas utiliser le HoloLens ou votre application dans la même façon que vous effectuez. En fait, il peut vous surprendre comportement de comment divergente populaire, base de connaissances et les hypothèses peuvent être !

## <a name="see-also"></a>Voir aussi
* [Visualisation d’analyse de salle](room-scan-visualization.md)
* [Sonorisation spatiale](spatial-sound-design.md)
* [Persistance dans Unity](persistence-in-unity.md)
