---
title: À propos de ce guide de conception
description: Ce guide a été coécrit par les concepteurs, les développeurs, les responsables de programme et les chercheurs, dont les appareils HOLOGRAPHIQUE (par exemple, HoloLens) et immersive (par exemple, les casques Acer et HP Windows Mixed Reality) s’étend sur Microsoft.
author: MRWied
ms.author: jonwie
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, présentation de conception, des conseils
ms.openlocfilehash: b4f128c001a2fa6ed72e1548ef82693ad1488099
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593799"
---
# <a name="about-this-design-guidance"></a>À propos de ce guide de conception

## <a name="introduction"></a>Introduction

**Bonjour et Bienvenue dans votre Guide de conception pour la réalité mixte.**

Ce guide a été coécrit par les concepteurs, les développeurs, les responsables de programme et les chercheurs, dont les appareils HOLOGRAPHIQUE (par exemple, HoloLens) et immersive (par exemple, les casques Acer et HP Windows Mixed Reality) s’étend sur Microsoft. Par conséquent, envisagez ce travail comme un ensemble de rubriques « comment concevoir pour Windows afficheur tête haute ».

Avec vous, nous entrons dans une nouvelle ère de l’informatique extrêmement intéressant. Innovations dans head monté affiche, son spatial, de capteurs, la connaissance de l’environnement, d’entrée, et cela nous amène les graphiques 3D et nous, à définir de nouveaux types d’expériences Défiez... une nouvelle frontière qui est considérablement plus personnelles, intuitive, immersives et contextuelles.

Dans la mesure du possible, nous proposerons des conseils de conception exploitables, avec le code connexe sur GitHub. Cela étant dit, étant donné que nous avons learning droite en même temps que vous, nous ne pourrons toujours offre également des conseils spécifiques et exploitables ici. Certains de ce que nous partageons seront dans l’esprit de « nous avons enseignements » et « éviter ce chemin d’accès pour descendre ».

Et nous savons de que nombreuses innovations seront générées par la Communauté de conception plus volumineuse, donc nous attendons avec impatience vos commentaires à partir de vous, l’apprentissage de votre part et travailler en étroite collaboration avec vous. Pour notre part, nous allons faire tout notre possible pour partager notre, même si elles sont exploratoires et au plus tôt, dans le but d’encourageant les développeurs et concepteurs avec réflexion de conception, les meilleures pratiques et les informations associées pour ouvrir les contrôles de source, les modèles et les exemples d’applications que vous pouvez utiliser directement dans votre propre travail.

## <a name="overview"></a>Vue d'ensemble

Voici un aperçu rapide de l’organisation de ce guide de conception. Vous trouverez des sections pour chacun de ces domaines, avec des liens vers plusieurs articles.
* **[Commencer à concevoir](mixed-reality.md)**  - lire nos pensées de haut niveau et comprendre les principes nous suivons.
* **[Conception de l’interaction](interaction-fundamentals.md)**  -en savoir plus sur l’entrée, des commandes, la navigation et d’autres principes de base d’interaction pour la conception de vos applications.
* **[Style](typography.md)**  -rendre votre application plaisante à l’aide de la couleur, la typographie et motion.
* **[Modèles d’application](types-of-mixed-reality-apps.md)**  -Découvrez comment les applications peuvent s’étendre sur des scénarios dans les environnements IMMERSIFS et réels.
* **[Contrôles](interactable-object.md)**  -utiliser des contrôles et modèles comme expérience de blocs de construction pour créer votre propre application.
* **[Exemples d’applications](design.md#sample-apps)**  -créez des expériences exceptionnelles à partir d’exemples conçu et créé par notre équipe.
* **[Concevoir des outils et ressources](design.md#design-tools)**  -lancer votre projet avec les outils et les modèles de conception.

Pour tous les éléments ci-dessus, nous voulons livrer la bonne combinaison de texte, les illustrations et les diagrammes et vidéos, donc, vous verrez nous expérimenter différents formats et techniques, tout dans le but de fournir ce que vous avez besoin. Et dans les prochains mois, nous développerons cette taxonomie afin d’inclure un ensemble plus large des rubriques de la conception. Si possible, que nous vous donnerons un frontal sur les futures fonctionnalités, par conséquent, conserver la vérification de retour.

## <a name="objectives"></a>Objectifs

Voici un aperçu des objectifs de haut niveau qui sont guidant ce travail pour vous pouvez de comprendre où nous venons de :

### <a name="help-solve-customer-challenges"></a>Aider à résoudre les défis du client

![Aider à résoudre les défis du client](images/500px-fix-a-broken-switch-with-hololens.jpg) <br>

Nous lutter contre la plupart des mêmes problèmes que vous effectuez, et nous savons comment difficile est de votre travail. Il est intéressant de les Explorer et définir une nouvelle frontière... et il peut également être décourageant. Pratiques et les paradigmes ancien doivent être considéré nouveau ; client besoin de nouvelles expériences ; et il est tellement potentiel d’innovation. Étant donné que, nous voulons que ce travail pour être aussi complète que possible, déplacement bien au-delà d’un guide de style. Notre objectif est de fournir un ensemble complet des conseils de conception qui couvre mixte d’interaction de la réalité, exécution de commandes, navigation, entrée et le style – toutes ancrée dans les scénarios et un comportement humain selon. 

### <a name="point-the-way-towards-a-new-more-human-way-of-computing"></a>Pointez la voie vers une nouvelle méthode plus humaine de l’informatique

![Pointez la voie vers une nouvelle méthode plus humaine de l’informatique](images/500px-man-and-women-with-holograph-on-table.png)<br>

S’il est important de se concentrer sur les problèmes des clients spécifiques, nous souhaitons également nous-mêmes considérer au-delà de celles et de distribuer plus poussée. Nous pensons que la conception n’est pas « simplement » résolution des problèmes, mais elles permettent également à activer concrètement évolution humaine. Nouvelles méthodes de comportement humain ; nouvelles façons de personnes relatives à eux-mêmes leurs activités et leurs environnements ; nouvelles façons de voir notre monde... Nous voulons que nos conseils afin de refléter toutes les manières suivantes plus formelle de penser en trop. 

### <a name="meet-creators-where-they-are"></a>Répondre aux créateurs où ils sont

![Répondre aux créateurs où ils sont](images/500px-creators.jpg) <br>

Nous espérons que de nombreux publics ce guide vous être utiles. Vous avez différentes compétences (début, intermédiaire, Avancé), que vous utilisez différents outils (Unity, DirectX, C++, C#, autres), sont familiarisés avec différentes plateformes (Windows, iOS, Android), proviennent de différents arrière-plans (mobile, enterprise, jeux ) et nous travaillons sur les équipes de taille différente (solo, petite, moyenne, grande). Par conséquent, ce guide sera consulté avec les besoins et différentes perspectives. Si possible, nous allons tenter cette diversité n’oubliez pas et rendent nos conseils aussi utile que possible aux personnes autant que possible. En outre, nous savons que beaucoup d'entre vous se trouvent déjà sur GitHub, donc nous allons associer directement vers les dépôts GitHub et des forums pour répondre aux vous où vous êtes déjà. 

### <a name="share-as-much-as-possible-from-experimental-to-explicit"></a>Partage autant que possible, à partir d’expérimentale en explicite

![Partage autant que possible, à partir d’expérimentale en explicite](images/500px-man-playinggame.jpg) <br>

Un des défis de l’offre des conseils de conception dans ce nouveau support 3D est que nous n’avons toujours pas guide définitif pour offrir. Comme vous, nous sommes en savoir plus, expérimentation, le prototypage, résolution des problèmes et l’ajustement alors que nous atteignons les obstacles. Au lieu d’attendre pour certains moment futures aux lorsque nous avons il deviné, notre objectif est de partager nos réflexions avec vous en temps réel, même si elle n’est pas concluant. Bien sûr, notre objectif final consiste à être indispensable dans la mesure du possible, en fournissant des conseils de conception claire et flexible liée au code open source et exploitables dans les outils de conception et de développement de Microsoft. Mais bien vers ce point de nombreux essais d’itération et de formation. Nous voulons prendre contact avec vous et découvrez avec vous, tout au long du processus, donc nous allons effectuer le mieux possible pour partager la mesure que nous, y compris notre, qui est expérimentale. 

### <a name="the-right-balance-of-global-and-local-design"></a>Le juste équilibre entre conception globale et locale

![Le juste équilibre entre conception globale et locale](images/500px-fluentdesign.jpg) <br>

Nous allons proposer deux niveaux de guide de conception : globaux et locaux. Notre Guide de conception 'global' est représentée dans le [Fluent Design System](http://fluent.microsoft.com). Détails de Fluent notre vision des notions de base comme light, profondeur, de mouvement, des documents et à l’échelle dans toutes les Microsoft design – nos périphériques, les produits, les outils et les services. Que ledit, importantes différences spécifiques à l’appareil existent sur ce système plus grand, donc notre 'local' conseils de conception pour afficheur tête haute décrira une conception pour appareils HOLOGRAPHIQUES et immersives possèdent souvent différentes d’entrée et les méthodes de sortie, et scénarios et besoins des utilisateurs différents. Par conséquent, les instructions de conception local couvre les sujets uniques à HMDs, par exemple 3D environnements et des objets ; environnements partagés ; l’utilisation de capteurs, suivi de le œil et mappage spatial ; et les opportunités de signal audio spatial. Dans l’ensemble de nos conseils vous verrez probablement nous font référence à ces global et les aspects locaux, et j’espère que cela vous aidera votre travail d’arrière-plan dans une plus grande base de conception tout en tirant parti des différences de conception des appareils spécifiques.

### <a name="have-a-discussion"></a>Avoir une discussion

![Avoir une discussion](images/500px-share.jpg) <br>

Peut-être plus important encore, nous voulons prendre contact avec vous, la Communauté des concepteurs HOLOGRAPHIQUES et IMMERSIFS et des développeurs, pour définir ce nouvel âge fabuleux de conception. Comme mentionné ci-dessus, nous savons nous n’avons pas toutes les réponses et nous pensons que de nombreuses solutions passionnantes et innovations proviendront de vous. Notre objectif est d’être ouverte et disponible à entendre les concernant et discuter avec vous en ligne et au cours des événements et ajouter la valeur dans la mesure du possible. Nous sommes heureux d’être une partie de cette Communauté de conception étonnantes, passer à une aventure ensemble. 

## <a name="please-dive-in"></a>Foncez.

Nous espérons que cet article bienvenu fournit un contexte significatif pendant que vous explorez notre Guide de conception. Veuillez foncez et faites-nous savoir vos réflexions sur les forums GitHub vous trouverez les liées dans nos articles, ou à Microsoft Design [Twitter](https://twitter.com/MicrosoftDesign) et [Facebook](https://www.facebook.com/microsoftdesign/). Nous allons concevoir des produits avec l’avenir ensemble !
