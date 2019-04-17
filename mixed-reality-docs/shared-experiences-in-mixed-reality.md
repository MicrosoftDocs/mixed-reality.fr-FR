---
title: Partage des expériences en réalité mixte
description: Applications HOLOGRAPHIQUE peuvent partager des ancres spatiales à partir d’un HoloLens vers un autre, en permettant aux utilisateurs d’afficher un hologramme au même endroit dans le monde réel sur plusieurs appareils.
author: thetuvix
ms.author: grbury
ms.date: 02/10/2019
ms.topic: article
keywords: expérience partagée, mixte réalité HOLOGRAMME, ancre spatiale, multi-utilisateur, plusieurs
ms.openlocfilehash: b27da1e73c927a26e33746cd2db08e67c6f70acc
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597137"
---
# <a name="shared-experiences-in-mixed-reality"></a>Partage des expériences en réalité mixte

Hologrammes n’avez pas besoin de rester privées pour un seul utilisateur. Partagent des applications HOLOGRAPHIQUE [ancres spatiales](coordinate-systems.md) à partir d’un HoloLens, appareil iOS ou Android vers un autre, permettant aux utilisateurs d’afficher un hologramme au même endroit dans le monde réel sur plusieurs appareils.

## <a name="six-questions-to-define-shared-scenarios"></a>Six questions pour définir des scénarios partagés

Avant de commencer la conception pour les expériences partagées, il est important de définir les scénarios cible. Ces scénarios vous aider à clarifier ce que vous êtes de conception et établissez un vocabulaire commun afin de comparer les fonctionnalités requises dans votre expérience. Compréhension le problème fondamental et les voies différentes pour les solutions, est essentielle aux opportunités découvrant inhérentes à ce nouveau support.

Grâce à des prototypes internes et explorations à partir de notre agences de partenaire HoloLens, nous avons créé des six questions pour vous aider à définir des scénarios partagés. Ces questions forment une infrastructure ne pas destinée à être exhaustive, pour aider à diffuser les attributs importants de vos scénarios.

### <a name="1-how-are-they-sharing"></a>1. Comment ils partage ?

Une présentation peut être conduite par un seul utilisateur virtuel, tandis que plusieurs utilisateurs peuvent collaborer, ou un enseignant peut fournir des conseils aux étudiants virtuels fonctionne avec les matériaux virtuel, la complexité du expériences augmente en fonction du niveau de l’agence qui a un utilisateur ou peut avoir dans un scénario.

![Homme et Femme avec holograph sur la table](images/man-and-women-with-holograph-on-table-500px.png)

Il existe plusieurs manières de partager, mais nous avons constaté que la plupart d'entre eux se répartissent en trois catégories :
* **Présentation**: Lorsque le même contenu est affiché à plusieurs utilisateurs. Exemple : Professeur est céder un discours à plusieurs étudiants à l’aide de la même sujet HOLOGRAPHIQUE présenté à tout le monde. Le professeur peut cependant avoir son propres indicateurs et les remarques qui ne sont peut-être pas visibles à d’autres personnes.
* **Collaboration**: Lorsque personnes collaborent pour atteindre des objectifs courants. Exemple : Le professeur a donné un projet pour en savoir plus sur l’exécution d’une CHIRURGIE CARDIAQUE. Les étudiants par deux et créer une expérience de laboratoire de compétences partagé qui permet des étudiants de collaborer sur le modèle de cœur et en savoir plus.
* **Conseils**: Quand une personne est d’aider quelqu'un à résoudre un problème dans une interaction de style d’un plus un. Exemple : Professeur offrant des conseils pour un étudiant lorsqu’il exécute le laboratoire de compétences de CHIRURGIE CARDIAQUE dans l’expérience partagée.

### <a name="2-what-is-the-group-size"></a>2. Quelle est la taille de groupe ?

**-À-un** partage des expériences peut fournir une référence forte et dans l’idéal, vos preuves de concept peuvent être créés à ce niveau. Sachez toutefois que partage avec des groupes importants (au-delà de 6 personnes) peut entraîner des difficultés à partir de la technique (données et mise en réseau) pour les réseaux sociaux (l’impact d’en cours dans une salle avec [avatars plusieurs](https://vimeo.com/160704056)). La complexité augmente de façon exponentielle comme vous accédez à partir de **petit** à **grands groupes**.

Nous avons découvert que les besoins de groupes peuvent être classées en trois catégories de taille :
* 1:1
* Petite < 7
* Grand > = 7

Augmente la taille de groupe pour une question importante, car son influence sur :
* Représentations sous forme de personnes dans l’espace HOLOGRAPHIQUE
* Mise à l’échelle d’objets
* Mise à l’échelle de l’environnement

### <a name="3-where-is-everyone"></a>3. Où se trouve tout le monde ?

La force de réalité mixte intervient quand une expérience partagée peut avoir lieu dans le même emplacement. Nous appelons qui **colocalisé**. À l’inverse, lorsque le groupe est distribué et au moins un participant n’est pas dans le même espace physique (comme c’est souvent le cas avec VR) nous appelons qui une expérience à distance. Il est souvent le cas où votre groupe a **à la fois** participants colocalisés et à distance (par exemple, deux groupes dans les salles de conférence).

![Trois personnes en situation de holograph sur la table](images/three-people-with-holograph-on-table-500px.png)

Les catégories suivantes aident à transmettre dans lequel se trouvent les utilisateurs :
* Colocalisée : Tous vos utilisateurs seront dans le même espace physique.
* À distance : Tous vos utilisateurs seront dans des espaces physiques distincts.
* Les deux : Vos utilisateurs seront un mélange d’espaces colocalisés et à distance.

Certaines raisons pour lesquelles cette question essentielle, car son influence sur :
* Modes de communication ?
* Exemple : Si, ils doivent avoir les avatars ?
* Les objets qu'ils voient. Tous les objets sont partagés ?
* Si nous avons besoin de s’adapter à leur environnement ?

### <a name="4-when-are-they-sharing"></a>4. Quand ils partagent ?

On parle généralement de **synchrone** rencontre lorsque les expériences partagées viennent à l’esprit : Tous nos il ensemble. Mais inclure un élément virtuel qui a été ajouté par quelqu'un d’autre et que vous avez un **asynchrone** scénario. Imaginez une note ou Mémo vocal, restant dans un environnement virtuel. Comment gérez-vous les mémos virtuels 100 restant sur votre conception ? Que se passe-t-il si elles sont parmi des dizaines de personnes avec différents niveaux de confidentialité ?

Prenez en compte vos expériences en tant qu’une de ces catégories de temps :
* **Mode synchrone**: Partage l’expérience HOLOGRAPHIQUE en même temps. Exemple : Deux stagiaires de la réalisation de l’atelier de compétences en même temps.
* **En mode asynchrone**: Partage l’expérience HOLOGRAPHIQUE à des moments différents. Exemple : Deux stagiaires de réalisation de l’atelier de compétences mais que sur des sections distinctes à des moments différents.
* **Les deux**: Vos utilisateurs sont parfois partage synchrone, mais d’autres fois en mode asynchrone. Exemple : Professeur de classement de l’assignation effectuée par les étudiants à une date ultérieure et quitter notes pour les étudiants pour le jour suivant.

Certaines raisons pour lesquelles cette question importante, car son influence sur :
* Objet de persistance et de l’environnement. Exemple : Stocker les États afin qu’ils peuvent être récupérées.
* Perspective de l’utilisateur. Exemple : Mémorisation peut-être ce que l’utilisateur a été consultant en quittant les notes de publication.

### <a name="5-how-similar-are-their-physical-environments"></a>5. Degré de similitude sont leurs environnements physiques ?

La probabilité de deux environnements réels identiques, en dehors des expériences COLOCALISÉES, est léger, sauf si ces environnements ont été conçus pour être identiques. Vous êtes plus susceptible d’avoir **similaire** environnements. Par exemple, les salles de conférence sont similaires, il a généralement une table centralisée entourée chaises. Salons, quant à eux, sont généralement **dissemblables** et peut inclure un nombre quelconque de meubles dans un tableau infini de dispositions.

![Holograph sur la table](images/holograph-on-table-500px.png)

Prenez en compte vos expériences de partage correspondant dans un de ces deux catégories :
* **Similaire**: Les environnements qui ont tendance à avoir des meubles similaire, la lumière ambiante et son, taille de l’espace physique. Exemple : Professeur est dans la salle de conférence A et les étudiants sont en cours hall hall B. conférence A peut-être moins chaises que B, mais ils ont tous deux peuvent un support physique pour placer hologrammes sur.
* **Dissemblables**: Environnements qui sont assez différentes dans les paramètres de mobilier, tailles de salle, considérations relatives à la lumière et robuste. Exemple : Professeur est dans une salle de focus, tandis que les étudiants sont dans une salle de conférence volumineux remplie d’étudiants / enseignants /.

Il est important de réfléchir à l’environnement comme il aura un impact sur :
* Comment les personnes verront ces objets. Exemple : Si votre expérience fonctionne mieux sur une table et que l’utilisateur ne dispose pas de table ? Ou sur une surface plate étage, mais l’utilisateur a un espace encombré.
* Mise à l’échelle des objets. Exemple : Placement d’un modèle de humaine de 6 pieds sur une table peut s’avérer difficile, mais un modèle de cœur fonctionnerait très bien.

### <a name="6-what-devices-are-they-using"></a>6. Quels sont les appareils qu’ils utilisent ?

Aujourd'hui vous verrez souvent probablement les expériences partagées entre deux **appareils immersives** (ces appareils peuvent différer légèrement en termes de boutons et de la fonctionnalité relative, mais pas considérablement) ou deux **HOLOGRAPHIQUE appareils** étant donné les solutions qui est ciblées sur ces appareils. Mais tenez compte des points **appareils 2D** (mobile/bureau participant ou Observateur) sera un facteur important nécessaire, en particulier dans les situations de **mixte appareils 2D et 3D**. Présentation des types d’appareils qui qu'utiliseront les participants est important, non seulement parce qu’ils sont fournis avec différents fidélité et des contraintes de données et des opportunités, mais étant donné que les utilisateurs ont des attentes uniques pour chaque plateforme.

## <a name="exploring-the-potential-of-shared-experiences"></a>Exploration des possibilités d’expériences partagées

Réponses aux questions ci-dessus peuvent être combinés pour mieux comprendre votre scénario partagé, CRISTALLISATION les défis que vous développez l’expérience. Pour l’équipe de Microsoft, il a participé à une feuille de route pour améliorer les expériences nous utilisons aujourd'hui, comprendre la nuance de ces problèmes complexes et comment tirer parti des expériences partagées dans la réalité mixte.

Par exemple, considérez un des scénarios de Skype depuis le lancement de HoloLens : un utilisateur passé [comment la corriger un commutateur lumineux rompu](https://www.youtube.com/watch?v=iBfzs3G8BEA) avec l’aide d’un expert situé à distance.

![Résolution d’un commutateur clair avec une assistance via Skype pour HoloLens](images/fix-a-broken-switch-with-hololens-640px.jpg)

<i>Fournit un expert <b>1:1</b> des conseils sur son <b>2D</b>, ordinateur de bureau à l’utilisateur d’un <b>3D, réalité mixte</b> appareil. Le <b>conseils</b> est <b>synchrone</b> et les environnements physiques sont <b>dissemblables</b>.</i>

Une telle expérience est une étape-modification à partir de notre expérience actuelle, appliquant le paradigme de voix et vidéo à un nouveau support. Mais nous sommes tournés vers l’avenir, nous devons mieux définir l’opportunité de nos scénarios et créer des expériences qui reflètent la force de réalité mixte.

Prendre en compte la [outil de collaboration OnSight](https://www.youtube.com/watch?v=ZOWQp0-Bkkw) développé par Jet Propulsion Laboratory la NASA. Scientifiques qui opèrent sur des données à partir de la mission du robot sur Mars peuvent collaborer avec des collègues dans en temps réel au sein des données à partir du paysage Martian.

![Collaboration entre collègues séparés à distance pour planifier le travail pour le robot sur Mars](images/onsight-nasa-jpl.gif)

<i>Un spécialiste des explore un environnement à l’aide un <b>3D, réalité mixte</b> appareil avec un <b>petit</b> groupe de <b>distant</b> collègues à l’aide <b>2D et 3D</b> appareils. Le <b>collaboration</b> est <b>synchrone</b> (mais vous pourrez en mode asynchrone) et les environnements physiques sont (presque) <b>similaire</b>.</i>

Expériences comme OnSight présentent de nouvelles opportunités pour collaborer. À partir de mentionner physiquement les éléments dans l’environnement virtuel et permanent en regard d’un collègue partage leur point de vue en expliquant leurs conclusions. OnSight utilise la glace immersion et à la présence de repenser les expériences de partage en réalité mixte.

Collaboration intuitive est la base de conversation et de collaboration, et il est essentiel de comprendre comment nous pouvons appliquer cette intuition à la complexité de la réalité mixte. Si nous pouvons non seulement recréer le partage des expériences dans la réalité mixte mais que vous surchargez les, il sera un changement de paradigme pour l’avenir de travail. Conception pour les expériences partagées en réalité mixte est nouvelle et passionnante de l’espace, et nous sommes uniquement au début.

## <a name="get-started-sharing-experiences"></a>Commencez à partager des expériences

En fonction de votre application et le scénario, il y aura des exigences différentes pour atteindre votre expérience souhaitée. Certaines d'entre elles incluent
* Fabrication de correspondance : Possibilité pour créer des sessions, de session, de publier et de découvrir et d’inviter des personnes spécifiques, à la fois localement et à distance pour joindre votre session.
* L’ancrage de partage : Possibilité d’aligner les coordonnées sur plusieurs appareils dans un espace local commun, donc vntana apparaître au même endroit pour toutes les personnes.
* Mise en réseau : Possibilité d’avoir positionne, interactions, et les mouvements de personnes et hologrammes synchronisées dans en temps réel dans tous les participants.
* Stockage de l’état : Possibilité de stocker des caractéristiques de hologramme et les emplacements dans l’espace pour la jonction de session intermédiaire, de rappeler à une heure ultérieure et la robustesse par rapport aux problèmes de réseau.


La clé pour les expériences partagées est plusieurs utilisateurs, voir les mêmes hologrammes dans le monde sur leur propre appareil fréquemment effectuée en partageant des points d’ancrage pour aligner les coordonnées sur des appareils.
Pour partager des points d’ancrage, utilisez le <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>:
* Tout d’abord l’utilisateur place le hologramme.
* Application crée un [ancre spatial](coordinate-systems.md) pour épingler ce hologramme précisément dans le monde.
* Les ancres peuvent être partagées pour HoloLens, appareils iOS et Android via le <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">ancres Spatial Azure</a>. 

Avec un point d’ancrage spatial partagé, l’application sur chaque appareil a maintenant un système de coordonnées courants dans lesquels ils peuvent placer le contenu. L’application peut maintenant assurer pour positionner et orienter l’hologramme au même emplacement.
Sur les appareils HoloLens, vous pouvez également partager des points d’ancrage en mode hors connexion d’un périphérique vers un autre.  Utilisez les liens ci-dessous pour déterminer ce qui convient le mieux à votre application.


## <a name="see-also"></a>Voir aussi
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Ancres Spatial Azure</a>
* [Partagé spatiales ancres dans DirectX](shared-spatial-anchors-in-directx.md)
* [Expériences partagées dans Unity](shared-experiences-in-unity.md)
* [Vue du spectateur](spectator-view.md)