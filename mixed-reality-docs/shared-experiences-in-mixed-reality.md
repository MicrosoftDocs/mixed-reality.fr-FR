---
title: Expériences partagées dans la réalité mixte
description: Les applications holographiques peuvent partager des ancres spatiales d’un HoloLens à un autre, ce qui permet aux utilisateurs d’afficher un hologramme au même endroit dans le monde réel, sur plusieurs appareils.
author: thetuvix
ms.author: grbury
ms.date: 02/10/2019
ms.topic: article
keywords: expérience partagée, réalité mixte, hologramme, ancrage spatial, multi-utilisateur, multi
ms.openlocfilehash: 4e71bdefa32d2f6cf3b85b074c3d9fcbdb6aa909
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437469"
---
# <a name="shared-experiences-in-mixed-reality"></a>Expériences partagées dans la réalité mixte

Les hologrammes n’ont pas besoin de rester privés pour un seul utilisateur. Les applications holographiques peuvent partager des [ancres spatiales](spatial-anchors.md) d’un appareil HoloLens, iOS ou Android à un autre, ce qui permet aux utilisateurs d’afficher un hologramme au même endroit dans le monde réel sur plusieurs appareils.

## <a name="six-questions-to-define-shared-scenarios"></a>Six questions pour définir des scénarios partagés

Avant de commencer à concevoir des expériences partagées, il est important de définir les scénarios cibles. Ces scénarios aident à clarifier ce que vous concevez et à mettre en place un vocabulaire commun pour vous aider à comparer et à opposer les fonctionnalités requises dans votre expérience. Le fait de comprendre le problème principal et les différentes voies pour les solutions est essentiel pour dévoiler les opportunités inhérentes à ce nouveau support.

Nous avons créé six questions pour vous aider à définir des scénarios partagés par le biais de prototypes internes et d’explorations de nos agences de partenaires HoloLens. Ces questions forment une infrastructure, non destinée à être exhaustive, pour aider à reconvertir les attributs importants de vos scénarios.

### <a name="1-how-are-they-sharing"></a>1. Comment sont-elles partagées ?

Une présentation peut être dirigée par un seul utilisateur virtuel, tandis que plusieurs utilisateurs peuvent collaborer, ou un enseignant peut fournir des conseils aux élèves virtuels qui utilisent des documents virtuels : la complexité des expériences augmente en fonction du niveau d’Agence dont dispose un utilisateur ou peut avoir dans un scénario.

![Homme et femmes avec holograph sur la table](images/man-and-women-with-holograph-on-table-500px.png)

Il existe de nombreuses façons de partager, mais nous avons constaté que la plupart d’entre elles se répartissent en trois catégories :

* **Présentation**: quand le même contenu est affiché à plusieurs utilisateurs. Par exemple : un professeur qui donne un cours à plusieurs élèves en utilisant les mêmes éléments holographiques présentés à tout le monde. Toutefois, le professeur peut avoir ses propres indications et notes qui peuvent ne pas être visibles par d’autres utilisateurs.
* **Collaboration**: lorsque des utilisateurs travaillent ensemble pour atteindre des objectifs courants. Par exemple : le professeur a donné un projet pour en savoir plus sur l’exécution d’une intervention cardiaque. Les étudiants s’associent et créent une expérience de laboratoire de compétences partagées qui permet aux étudiants médicaux de collaborer sur le modèle de cœur et d’apprendre.
* **Conseils**: quand une personne aide quelqu’un à résoudre un problème dans une interaction de style un-à-un plus grand. Par exemple, le professeur qui donne des conseils à un étudiant lorsqu’il est en mesure d’exécuter le laboratoire de compétences en chirurgie cardiaque dans l’expérience partagée.

### <a name="2-what-is-the-group-size"></a>2. quelle est la taille de groupe ?

Les expériences de partage **un-à-un** peuvent fournir une base forte et, idéalement, vous pouvez créer vos preuves de concept à ce niveau. Toutefois, sachez que le partage avec de grands groupes (au-delà de 6 personnes) peut entraîner des difficultés à la fois techniques (données et mise en réseau) et sociales (l’impact d’être dans une salle avec [plusieurs avatars](https://vimeo.com/160704056)). La complexité augmente de façon exponentielle au fur et à mesure que vous passez de **petits** à **grands groupes**.

Nous avons constaté que les besoins des groupes peuvent être répartis en trois catégories :
* 1:1
* Petit < 7
* Grand > = 7

La taille de groupe fait une question importante car elle influence :

* Représentations des personnes dans l’espace holographique
* Échelle des objets
* Mise à l’échelle de l’environnement

### <a name="3-where-is-everyone"></a>3. où est-ce que tout le monde ?

La force de la réalité mixte entre en interaction quand une expérience partagée peut avoir lieu au même emplacement. Nous **appelons ce colocalisation**. Inversement, lorsque le groupe est distribué et qu’au moins un participant n’est pas dans le même espace physique (comme c’est souvent le cas avec VR), nous appelons cette **expérience à distance**. Souvent, il s’agit du cas où votre groupe a des participants colocalisés et distants (par exemple, deux groupes dans **les** salles de conférence).

![Trois personnes avec holograph sur la table](images/three-people-with-holograph-on-table-500px.png)

Les catégories suivantes vous aident à communiquer où se trouvent les utilisateurs :

* Colocalisé : tous vos utilisateurs se **trouvent**dans le même espace physique.
* **À distance**: tous vos utilisateurs se trouvent dans des espaces physiques distincts.
* **Les deux**: vos utilisateurs sont un mélange d’espaces colocalisés et distants.

Cette question est cruciale, car elle influence :

* Comment les gens communiquent-ils ?
    * Par exemple : s’ils doivent avoir des avatars ?
* Les objets qu’ils voient. Tous les objets sont-ils partagés ?
* Si nous avons besoin de s’adapter à leur environnement ?

### <a name="4-when-are-they-sharing"></a>4. quand sont-ils partagés ?

En général, nous considérons les expériences **synchrones** quand les expériences partagées sont à l’esprit : nous travaillons tous ensemble. Toutefois, si nous incluons un seul élément virtuel qui a été ajouté par quelqu’un d’autre, nous avons un scénario **asynchrone** . Imaginez une note, ou un mémo vocal, laissé dans un environnement virtuel. Comment gérer les mémos virtuels 100 sur votre conception ? Que se passe-t-il s’il s’agit de dizaines de personnes avec des niveaux de confidentialité différents ?

Considérez vos expériences comme l’une des catégories de temps suivantes :

* En mode **synchrone**: partage de l’expérience holographique en même temps. Par exemple, deux élèves effectuant le laboratoire de compétences en même temps.
* De **manière asynchrone**: le partage de l’expérience holographique à des moments différents. Par exemple, deux élèves effectuant le laboratoire de compétences, mais travaillant sur des sections distinctes à des moments différents.
* **Les deux**: vos utilisateurs partageront parfois de façon synchrone, mais d’autres fois de façon asynchrone. Par exemple, un professeur qui dégrade l’attribution effectuée par les étudiants ultérieurement et qui laisse des notes aux élèves pour la journée suivante.

Cette question est importante car elle influence :

* Persistance des objets et de l’environnement. Par exemple : stockage des États afin qu’ils puissent être récupérés.
* Point de vue de l’utilisateur. Par exemple, vous avez peut-être besoin de mémoriser ce que l’utilisateur a fait lors de la sortie des notes.

### <a name="5-how-similar-are-their-physical-environments"></a>5. quelle est la similarité de leurs environnements physiques ?

La probabilité de deux environnements réels identiques, en dehors des expériences colocalisées, est mince, à moins que ces environnements aient été conçus pour être identiques. Vous êtes plus susceptible d’avoir des environnements **similaires** . Par exemple, les salles de conférence sont similaires. elles ont généralement une table située à l’emplacement central, entourée de chaises. Les salles vivantes, en revanche, sont généralement **dissemblables** et peuvent inclure un nombre quelconque de meubles dans un tableau infini de dispositions.

![Holograph sur la table](images/holograph-on-table-500px.png)

Imaginez que vos expériences de partage s’adaptent à l’une de ces deux catégories :

* **Similaire**: environnements qui ont tendance à avoir des meubles similaires, un éclairage ambiant et un son, la taille de la salle physique. Par exemple, le professeur est dans la salle de conférence A et les étudiants se trouvent dans la salle de conférence B. la salle de conférence A peut avoir moins de chaises que B, mais les deux peuvent avoir un bureau physique sur lequel placer des hologrammes.
* **Différent : environnements**qui sont très différents dans les paramètres de mobilier, les tailles de salle, les considérations claires et sonores. Par exemple, un professeur est dans une salle de focalisation, tandis que les étudiants sont dans une grande salle de conférence, remplis avec des étudiants et des enseignants.

Il est important de [réfléchir à l’environnement](environment-considerations-for-hololens.md), car il aura une incidence sur les éléments suivants :

* La manière dont les utilisateurs auront connaissance de ces objets. Par exemple : Si votre expérience fonctionne mieux sur une table et si l’utilisateur n’a pas de table ? Ou sur une surface plate, mais l’utilisateur a un espace encombré.
* Échelle des objets. Par exemple, le fait de placer un modèle humain de 6 mètres sur une table peut être difficile, mais un modèle cardiaque fonctionnerait bien.

### <a name="6-what-devices-are-they-using"></a>6. Quels appareils utilisent-ils ?

Aujourd’hui, vous êtes souvent amené à voir des expériences partagées entre deux [**appareils immersifs**](immersive-headset-hardware-details.md) (ces appareils peuvent différer légèrement en termes de boutons et de fonctionnalités relatives, mais pas beaucoup) ou de deux **appareils holographiques** étant donné les solutions ciblées sur ces appareils. Toutefois, si les **appareils 2D** (un participant ou un observateur mobile/Desktop) sont nécessaires, en particulier dans les situations des **appareils 2D et 3D mélangés**. Il est important de comprendre les types d’appareils que vos participants vont utiliser, non seulement parce qu’ils sont fournis avec des opportunités et des contraintes de fidélité et de données différentes, mais parce que les utilisateurs ont des attentes uniques pour chaque plateforme.

## <a name="exploring-the-potential-of-shared-experiences"></a>Exploration du potentiel des expériences partagées

Les réponses aux questions ci-dessus peuvent être combinées pour mieux comprendre votre scénario partagé, en déformant les défis au fur et à mesure que vous développez l’expérience. Pour l’équipe chez Microsoft, cela nous a aidé à établir un plan de route pour améliorer les expériences que nous utilisons aujourd’hui, à comprendre la nuance de ces problèmes complexes et à tirer parti des expériences partagées dans la réalité mixte.

Par exemple, considérez l’un des scénarios Skype du lancement de HoloLens : un utilisateur a travaillé sur [la résolution d’un commutateur lumineux défectueux](https://www.youtube.com/watch?v=iBfzs3G8BEA) avec l’aide d’un expert à distance.

![Résolution d’un commutateur léger avec assistance via Skype pour HoloLens](images/fix-a-broken-switch-with-hololens-640px.jpg)

*Un expert fournit des conseils **1:1** de son ordinateur de bureau **2D**à un utilisateur d’un appareil en **réalité mixte en 3D** . L' **aide** est **synchrone** et les environnements physiques sont **différents**.*

Une expérience comme celle-ci est un changement pas à pas de notre expérience actuelle, en appliquant le paradigme de la vidéo et de la voix à un nouveau support. Mais à l’avenir, nous devons mieux définir l’opportunité de nos scénarios et créer des expériences qui reflètent la force de la réalité mixte.

Prenons l' [outil de collaboration OnSight](https://www.youtube.com/watch?v=XtUyUJAVQ6w), développé par le laboratoire de propulsion jet de la NASA. Les scientifiques qui travaillent sur les données des missions de mars Rover peuvent collaborer avec des collègues en temps réel dans les données du paysage Martian.

![Collaboration entre collègues séparés à distance pour planifier le travail pour Mars Rover](images/onsight-nasa-jpl.gif)

*Un scientifique explore un environnement à l’aide d’un appareil 3D et en **réalité mixte** avec un **petit** groupe de collègues **distants** utilisant des appareils **3D et 2D** . La **collaboration** est **synchrone** (mais peut être revisitée de manière asynchrone) et les environnements physiques sont (pratiquement) **similaires**.*

Des expériences comme OnSight présentent de nouvelles opportunités de collaboration. Du point de vue physique des éléments de l’environnement virtuel à la position à côté d’un collègue et au partage de leur perspective lorsqu’ils expliquent leurs résultats. OnSight utilise l’objectif de l’immersion et de la présence pour repenser les expériences de partage dans la réalité mixte.

La collaboration intuitive est le socle de conversation, le travail et la compréhension de la façon dont nous pouvons appliquer cette intuition à la complexité de la réalité mixte est cruciale. Si nous pouvons non seulement recréer les expériences de partage dans la réalité mixte, mais les surcharger, il s’agit d’un changement de paradigme pour l’avenir du travail. La conception d’expériences partagées en réalité mixte est une nouveauté et une expérience passionnante, et nous ne sommes qu’au début.

## <a name="get-started-building-shared-experiences"></a>Commencez à créer des expériences partagées

En fonction de votre application et de votre scénario, il y aura plusieurs exigences pour atteindre votre expérience souhaitée. Parmi ceux-ci, citons notamment :

* **Correspondance**: possibilité de créer des sessions, de publier des sessions, de découvrir et d’inviter des personnes spécifiques, localement et à distance, pour rejoindre votre session.
* **Partage d’ancrage**: possibilité d’aligner les coordonnées sur plusieurs appareils dans un espace local commun, de sorte que les hologrammes s’affichent dans le même emplacement pour tous les utilisateurs.
* **Mise en réseau**: possibilité d’avoir des positions, des interactions et des mouvements de personnes et d’hologrammes synchronisés en temps réel pour tous les participants.
* **Stockage d’État**: capacité à stocker les caractéristiques et emplacements de l’hologramme dans l’espace pour la jonction au milieu des sessions, à rappeler ultérieurement et à renforcer les problèmes réseau.

La clé de l’expérience partagée consiste à faire en sorte que plusieurs utilisateurs voient les mêmes hologrammes dans le monde sur leur propre appareil, souvent en partageant des points d’ancrage pour aligner les coordonnées entre les appareils.

Pour partager des ancres, utilisez les [ancres spatiales Azure](https://docs.microsoft.com/azure/spatial-anchors):

* Tout d’abord, l’utilisateur place l’hologramme.
* L’application crée une [ancre spatiale](spatial-anchors.md), pour épingler précisément cet hologramme dans le monde.
* Les ancres peuvent être partagées avec des appareils HoloLens, iOS et Android via des [ancres spatiales Azure](https://docs.microsoft.com/azure/spatial-anchors/).

Avec une ancre spatiale partagée, l’application sur chaque appareil dispose désormais d’un [système de coordonnées commun](coordinate-systems.md) dans lequel elles peuvent placer du contenu. L’application peut maintenant garantir la position et l’orientation de l’hologramme au même emplacement.

Sur les appareils HoloLens, vous pouvez également partager des ancres hors connexion d’un appareil à un autre.  Utilisez les liens ci-dessous pour déterminer ce qui convient le mieux à votre application.

## <a name="evaluating-tech-options"></a>Évaluation des options techniques

Différentes options de service et de technologie sont disponibles pour vous aider à créer des expériences de réalité mixte multi-utilisateur.  Il peut être difficile de choisir un chemin d’accès. par conséquent, si vous prenez une perspective axée sur les scénarios, certaines options sont détaillées ci-dessous.

## <a name="shared-static-holograms-no-interactions"></a>Hologrammes statiques partagés (aucune interaction)

Tirez parti des [ancres spatiales Azure](https://docs.microsoft.com/azure/spatial-anchors/) dans votre application.  L’activation et le partage d’ancres spatiales sur plusieurs appareils vous permettent de créer une application dans laquelle les utilisateurs voient les hologrammes dans le même emplacement en même temps.  La synchronisation supplémentaire entre les appareils est nécessaire pour permettre aux utilisateurs d’interagir avec les hologrammes et voir les mouvements ou les mises à jour d’état des hologrammes.

## <a name="share-1st-person-perspective"></a>Perspective partager la première personne

Tirez parti de la prise en charge de Miracast intégrée, pour les utilisateurs locaux lorsque vous avez un récepteur Miracast pris en charge, tel qu’un PC ou une télévision, aucun code d’application supplémentaire n’est nécessaire.

Tirez parti de [MixedReality-WebRTC](https://github.com/microsoft/mixedreality-webrtc) dans votre application, pour les utilisateurs distants ou lorsque vous avez des appareils non Miracast que vous souhaitez partager.  L’activation d’une connexion WebRTC active des flux audio/vidéo de 1:1 entre les utilisateurs, avec un canal de données pour la messagerie sur les appareils.  L’implémentation de la réalité mixte optimise pour HoloLens, en fournissant un flux vidéo de capture de la réalité mixte de la vue de l’utilisateur HoloLens à d’autres utilisateurs.  Si vous souhaitez mettre à l’échelle la diffusion vidéo en continu vers plusieurs clients distants, un [fournisseur de services MCU](https://webrtcglossary.com/mcu/) (multipoint Conferencing Unit) est généralement utilisé, tel que [SignalWire](https://signalwire.com/).  Un déploiement SignalWire sur Azure est disponible via [FreeSwitch](https://github.com/andywolk/azure-freeswitch-gpu-windows).

> [!NOTE]
> Notez que SignalWire est un service payant et qu’il n’est pas détenu/affilié à Microsoft.

## <a name="presenter-spectator-applications-and-demos"></a>Présentateur-applications et démonstrations pour spectateur

Tirez parti de [MixedReality-SpectatorView](https://github.com/microsoft/MixedReality-SpectatorView) pour intégrer les [fonctionnalités de vue de specator](spectator-view.md) à votre application.  Activez les autres appareils (HL, Android, iOS et les caméras vidéo) pour voir ce que l’HoloLens voit d’une perspective différente au même emplacement, et recevoir des mises à jour sur les interactions de l’utilisateur de l’ordinateur hôte HoloLens qui interagit avec les hologrammes.  Regardez, prenez des photos et enregistrez une vidéo de ce que fait l’hôte avec les hologrammes de l’application, de votre propre perspective spatiale avec l’accompagnement spectateur de la même application.

**Remarque :** Les images sont prises via la capture d’écran sur les appareils iOS/Android.

## <a name="multi-user-collaborative-experience"></a>Expérience collaborative multi-utilisateur

Commencez avec notre [didacticiel d’apprentissage multi-utilisateur](mrlearning-sharing(photon)-ch1.md), qui tire parti des [ancres spatiales Azure](https://docs.microsoft.com/azure/spatial-anchors/) pour les utilisateurs locaux et le [Kit de développement logiciel (SDK) de photons](https://www.photonengine.com/PUN) pour synchroniser le contenu/l’État dans la scène. Créez des applications de collaboration localement, où chaque utilisateur a sa propre perspective sur les hologrammes de la scène et peut interagir entièrement avec les hologrammes.  Les mises à jour sont fournies sur tous les appareils et la gestion des conflits d’interaction est gérée par la photonique.

> [!NOTE]
> Notez que la [photon](https://www.photonengine.com/) est un produit non-Microsoft. une relation de facturation avec photons peut donc être nécessaire pour la reproduction et la mise à l’échelle pour une utilisation plus élevée.

## <a name="future-work"></a>Travail à venir

Les fonctionnalités et les interfaces des composants vous aideront à fournir une cohérence commune et une prise en charge robuste dans les différents scénarios et technologies sous-jacentes.  À ce moment-là, choisissez le chemin le mieux adapté au scénario que vous essayez d’atteindre dans votre application.

Autre scénario ou souhait d’utiliser une autre technique/service ? Fournissez des commentaires sous forme de problèmes GitHub dans le référentiel correspondant, en bas de cette page, ou accédez à la [marge HoloDevelopers](https://holodevelopers.slack.com/).

## <a name="see-also"></a>Articles associés

* [Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors)
* [Ancres spatiales partagées dans DirectX](shared-spatial-anchors-in-directx.md)
* [Expériences partagées dans Unity](shared-experiences-in-unity.md)
* [Vue Spectateur](spectator-view.md)
