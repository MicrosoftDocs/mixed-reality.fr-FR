---
title: À propos de ce guide de conception
description: Cette aide a été écrite par des concepteurs, des développeurs, des responsables de programme et les chercheurs de Microsoft, dont les travaux couvrent les appareils holographiques (par exemple HoloLens) et les appareils immersifs (par exemple les casques Windows Mixed Reality Acer et HP).
author: MRWied
ms.author: jonwie
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, introduction, conseils
ms.openlocfilehash: 0e5601898c2b1f351b5ab2aaa491a7c64ae57f7e
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414161"
---
# <a name="about-this-design-guidance"></a>À propos de ce guide de conception

## <a name="introduction"></a>Présentation

**Bonjour et Bienvenue dans vos conseils de conception pour la réalité mixte.**

Ce guide est créé par les concepteurs, les développeurs, les responsables de programme et les chercheurs de Microsoft, dont le travail s’étend sur des appareils holographiques, en tant que HoloLens et périphériques immersifs, tels que les casques Windows de la réalité mixte Acer et HP. Considérez ce travail comme un ensemble de rubriques expliquant comment concevoir des affichages montés en tête Windows.

Avec vous, nous avons introduit une nouvelle ère remarquablement passionnante de l’informatique. Des innovations dans les affichages montés en tête, le son spatial, les capteurs, la sensibilisation de l’environnement, les entrées et les graphiques 3D nous mènent, et nous nous contenterons de définir de nouveaux types d’expériences: une nouvelle frontière est radicalement plus personnelle, intuitive, immersive et contextuelle.

Dans la mesure du possible, nous proposerons des conseils de conception actionnables avec le code associé sur GitHub. Cela dit, étant donné que nous nous familiarisons avec vous, nous ne serons pas toujours en mesure de proposer des conseils pratiques spécifiques. Une partie de ce que nous partagerons sera à l’esprit des «leçons que nous avons apprises» et «évitez de faire tourner ce chemin d’accès».

Et nous savons que de nombreuses innovations seront générées par la communauté de conception plus grande. Nous sommes donc impatients de vous faire part de vos commentaires, de vous apprendre et de travailler en étroite collaboration avec vous. Pour notre part, nous ferons de notre mieux pour partager nos Insights, même s’ils sont exploratoires et tôt avec l’intention de donner aux développeurs et aux concepteurs des conseils de conception, des pratiques recommandées et les contrôles, modèles et exemples d’applications open source associés que vous pouvez utiliser. directement dans votre propre travail.

## <a name="overview"></a>Vue d'ensemble

Voici une vue d’ensemble rapide de l’organisation de ce guide de conception. Vous trouverez des sections pour chacun de ces domaines avec des liens vers plusieurs articles.
* **[Prise en main de la conception](mixed-reality.md)** : Lisez nos pensées de haut niveau et comprenez les principes que nous suivons.
* **[Interactions instinctual](interaction-fundamentals.md)** : en savoir plus sur les entrées, les commandes, la navigation et d’autres notions de base sur l’interaction pour la conception de vos applications.
* **[Style](typography.md)** : rendez votre application délicieuse en utilisant la couleur, la typographie et le mouvement.
* **[Modèles d’application](types-of-mixed-reality-apps.md)** : Découvrez comment les applications peuvent couvrir des scénarios dans les environnements immersifs et dans le monde réel.
* **[Contrôles](interactable-object.md)** : utilisez des contrôles et des modèles comme blocs de construction pour créer votre propre expérience d’application.
* **[Exemples d’applications](design.md#sample-apps)** : créez de superbes expériences à partir d’exemples conçus et créés par notre équipe.
* **[Concevoir des outils et des ressources](design.md#design-tools)** -démarrez votre projet avec des modèles et des outils de conception.

Pour tous les éléments ci-dessus, nous avons l’intention de fournir la bonne combinaison de texte, d’illustrations et de diagrammes, ainsi que de vidéos. vous verrez donc que nous expérimentons des formats et des techniques différents, avec l’intention de fournir ce dont vous avez besoin. Et dans les mois à venir, nous développerons cette taxonomie pour inclure un ensemble plus large de rubriques de conception. Dans la mesure du possible, nous vous ferons découvrir ce qui se passe à l’étape suivante. par conséquent, continuez à vérifier.

## <a name="objectives"></a>Objectifs

Voici un aperçu rapide de certains objectifs de haut niveau qui guident ce travail pour vous permettre de comprendre où nous sommes issus

### <a name="help-solve-customer-challenges"></a>Aider à résoudre les problèmes des clients

![Aider à résoudre les problèmes des clients](images/500px-fix-a-broken-switch-with-hololens.jpg) <br>

Nous prenons en charge un grand nombre des problèmes que vous rencontrez et nous comprenons la difficulté de votre travail. Il est intéressant d’explorer et de définir une nouvelle frontière... et il peut également s’avérer décourageant. Les anciens paradigmes et pratiques doivent être repensés. les clients ont besoin de nouvelles expériences; et le potentiel d’innovation est tellement grand. Étant donné que nous souhaitons que ce travail soit aussi complet que possible, en passant au-delà d’un guide de style. Nous avons l’intention de fournir un ensemble complet de conseils de conception qui traitent de l’interaction de la réalité mixte, de l’action, de la navigation, de l’entrée et du style, tout cela dans le comportement humain et les scénarios. 

### <a name="point-the-way-towards-a-new-more-human-way-of-computing"></a>Pointez vers un nouveau moyen de calcul plus humain

![Pointez vers un nouveau moyen de calcul plus humain](images/500px-man-and-women-with-holograph-on-table.png)<br>

Bien qu’il soit important de se concentrer sur des problèmes spécifiques aux clients, nous souhaitons également nous faire part de vos commentaires et pour en faire plus. Nous pensons que la conception n’est pas «juste», mais également un moyen d’activer l’évolution humaine de manière significative. Nouvelles méthodes de comportement humain; nouvelles méthodes de personnes liées à elles-mêmes, à leurs activités et à leurs environnements; de nouvelles façons de voir notre monde... Nous souhaitons que nos conseils reflètent l’ensemble de ces méthodes de réflexion. 

### <a name="meet-creators-where-they-are"></a>Rencontrez les créateurs où ils sont

![Rencontrez les créateurs où ils sont](images/500px-creators.jpg) <br>

Nous espérons que de nombreux publics trouvent ces conseils pour être utiles. Vous avez différentes compétences (début, intermédiaire, avancé), utilisez différents outils (Unity, DirectX, C++, C#, etc.), vous êtes familiarisé avec les différentes plateformes (Windows, iOS, Android), issues de différents horizons (mobiles, entreprise, jeux ) et travaillent sur différentes équipes de taille (solo, petite, moyenne, grande). Ce guide peut donc être consulté avec différentes perspectives et besoins. Dans la mesure du possible, nous essaierons de garder cette diversité à l’esprit et de faire en sorte que nos conseils soient les plus pertinents possible pour autant de personnes que possible. En outre, nous savons que beaucoup d’entre vous sont déjà sur GitHub. Nous allons donc nous lier directement à des GitHubs et à des forums pour vous répondre là où vous êtes déjà. 

### <a name="share-as-much-as-possible-from-experimental-to-explicit"></a>Partager le plus possible, de l’expérimentation à la valeur explicite

![Partager le plus possible, de l’expérimentation à la valeur explicite](images/500px-man-playinggame.jpg) <br>

L’un des défis liés à l’offre de conseils en matière de conception dans ce nouveau support 3D est que nous n’avons pas toujours de conseils définitifs à proposer. Comme vous le feriez, nous envoyons, expérimentons, prototypages, résolution des problèmes et ajustons à mesure que nous heurtons les obstacles. Au lieu d’attendre un futur moment où nous l’avons fait, nous souhaitons partager notre pensée avec vous en temps réel, même s’il n’est pas concluant. Bien entendu, notre objectif final est de clarifier partout où nous pouvons, en fournissant des conseils de conception clairs et flexibles, liés au code open source et actionnables dans les outils de développement et de conception Microsoft. Toutefois, l’accès à ce point prend de nombreuses séries d’itérations et d’apprentissage. Nous souhaitons vous contacter et vous apprendre avec vous, en cours de route. Tout cela à l’esprit, nous allons faire de notre mieux pour le partager au fur et à mesure, même avec nos produits expérimentaux. 

### <a name="the-right-balance-of-global-and-local-design"></a>Le juste équilibre entre la conception globale et la conception locale

![Le juste équilibre entre la conception globale et la conception locale](images/500px-fluentdesign.jpg) <br>

Nous proposons deux niveaux de conseils de conception: global et local. Notre guide de conception «global» est incorporé dans le [système de conception Fluent](http://fluent.microsoft.com). Fluent explique en détail comment nous pensons aux notions de base, telles que la lumière, la profondeur, le mouvement, le matériau et la mise à l’échelle dans l’ensemble de la conception Microsoft, nos appareils, produits, outils et services. Cela dit, des différences significatives spécifiques aux appareils existent sur ce système plus volumineux. Ainsi, notre guide de conception «local» pour les affichages montés en tête décrivent la conception d’appareils holographiques et immersifs qui ont souvent des méthodes d’entrée et de sortie différentes, ainsi que des besoins et des scénarios d’utilisateur différents. Le Guide de conception local couvre les rubriques propres à HMDs. Exemple : environnements et objets 3D; environnements partagés; l’utilisation de capteurs, le suivi oculaire et le mappage spatial; et les opportunités de l’audio spatial. Tout au long de nos conseils, nous verrons que nous nous référons à la fois à ces aspects globaux et locaux. Nous espérons que cela vous aidera à mettre votre travail en œuvre dans un grand nombre de conceptions tout en tirant parti des différences de conception entre les appareils spécifiques.

### <a name="have-a-discussion"></a>Avoir une discussion

![Avoir une discussion](images/500px-share.jpg) <br>

Plus important encore, nous souhaitons vous contacter, la communauté de concepteurs et de développeurs de systèmes holographiques et immersifs, afin de définir cette nouvelle ère passionnante de conception. Comme indiqué ci-dessus, nous savons que nous n’avons pas toutes les réponses. C’est la raison pour laquelle nous pensons que de nombreuses solutions et innovations passionnantes vous seront fournies. Nous souhaitons être ouverts et disponibles pour en savoir plus à leur sujet, et discuter avec vous en ligne et aux événements, et ajouter de la valeur partout où nous le pouvons. Nous sommes ravis de faire partie de cette communauté de conception incroyable, en vous regroupant sur une aventure. 

## <a name="please-dive-in"></a>Plongez-vous

Nous espérons que cet article de présentation fournit un contexte explicite lorsque vous explorez nos conseils de conception. Plongez-vous et faites-nous part de vos commentaires sur les forums GitHub que vous trouverez dans nos articles, ou sur le lien Microsoft sur [Twitter](https://twitter.com/MicrosoftDesign) et [Facebook](https://www.facebook.com/microsoftdesign/). Nous allons concevoir l’avenir en collaboration.
