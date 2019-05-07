---
title: Vue d’ensemble de l’interaction multimodale
description: Vue d’ensemble de l’interaction multimodale
author: shengkait
ms.author: shengkait
ms.date: 04/11/2019
ms.topic: article
keywords: Mixte réalité, regards, regards ciblant, interaction, concevoir
ms.openlocfilehash: f52a0cd8ec53bfe0f4c5da2c054c538eda1c93ca
ms.sourcegitcommit: aa88f6b42aa8d83e43104b78964afb506a368fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/02/2019
ms.locfileid: "64993601"
---
# <a name="introducing-instinctual-interactions"></a>Présentation des interactions instinctual
La philosophie d’interactions simples, instinctual nouée tout au long de la plateforme de réalité mixte de Microsoft.  Nous avons pris trois étapes pour vérifier que les développeurs et concepteurs d’applications peuvent fournir des interactions faciles et intuitives pour leurs clients. 

Tout d’abord, nous avons veillé à ce notre étonnant de capteurs et de la technologie d’entrée, notamment main suivi, suivi de le œil et langage naturel, combinent des modèles d’interaction multimodale transparente.  Selon nos recherches, conception et développement multi-modalement--et ne dépendent ne pas des entrées uniques--est essentiel à la création d’expériences instinctual.

Deuxièmement, nous reconnaissons que de nombreux développeurs ciblent plusieurs appareils, que ce soit pour HoloLens 2 et HoloLens (1er gen) ou HoloLens et VR.  Par conséquent, nous avons conçu nos modèles d’interaction pour travailler sur des appareils (même si la technologie d’entrée varie sur chaque appareil).  Par exemple, interaction lointain sur casque Immersive de Windows avec un contrôleur 6DOF et lointain interaction sur les deux 2 HoloLens utiliser l’intuitivité identiques et les modèles, ce qui facilite pour les applications entre les périphériques. Est non seulement ce pratique pour les développeurs et concepteurs, mais il a l’air normal pour les utilisateurs finaux. 

Enfin, alors que nous reconnaissons qu’il existe des milliers d’effective, attrayantes et interactions magiques possibles dans MR, nous avons trouvé cette intentionnellement utilisant un modèle d’interaction unique bout en bout dans une application est la meilleure façon de garantir aux utilisateurs réussissent et offrir une bonne expérience.  À cette fin, nous avons inclus les trois choses dans ce guide de l’interaction :
* Nous avons structuré ce guide autour de trois modèles d’interaction principal et les composants et les modèles requis pour chaque
* Nous avons inclus des conseils supplémentaires sur les autres avantages offerts par notre plateforme
* Nous avons inclus des conseils pour aider à sélectionner le modèle d’interaction approprié pour votre scénario


## <a name="three-multimodal-interaction-models"></a>Trois modèles d’interaction multimodale
Selon notre recherche et la collaboration avec les clients à ce jour, nous avons découvert que les trois modèles d’interaction principal adapter à la majorité des expériences de réalité mixte.

Dans bien des égards, le modèle d’interaction est modèle mental de l’utilisateur pour l’exécution de leurs flux.  Chacun de ces modèles d’interaction est optimisé pour un ensemble de besoins des clients, et chacun est utilisable à part entière, puissant et pratique. 

Le tableau ci-dessous est une vue d’ensemble simplifiée.  Des informations détaillées pour l’utilisation de chaque modèle d’interaction sont liées dans les pages ci-dessous avec des images et des exemples de code.  

<br>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Modèle</strong></td>
        <td><strong>Exemples de scénarios</strong></td>
        <td><strong>Fit</strong></td>
        <td><strong>Matériel</strong></td>
    </tr>
    <tr>
        <td><a href="hands-and-tools.md">Mains et outils</a></td>
        <td>Expériences spatiales 3D<br>par exemple, spatiale disposition et conception, manipulation de contenu ou simulation</td>
        <td>Idéal pour les nouveaux utilisateurs<br>Courbe d’apprentissage basse<br>Ancrée dans intuitivité visual facile<br>Expérience utilisateur cohérente entre main suivi et les contrôleurs de DDL 6<br>Très bien associée à la voix, suivi de le œil ou head les regards</td>
        <td>HoloLens 2<br>Windows immersives avec 6DOF contrôleurs</td>
    </tr>
    <tr>
        <td><a href="hands-free.md">Mains libres</a></td>
        <td>Expériences contextuelles, où les mains d’un utilisateur sont occupés par exemple, sur le travail d’apprentissage, de maintenance</td>
        <td>Certaines de formation requise<br>Si les mains ne sont pas disponibles<br>paires bien avec la voix et de langage naturel</td>
        <td>HoloLens 2<br>HoloLens (1er gen)<br> Immersive de Windows</td>
    </tr>
    <tr>
        <td><a href="gaze-and-commit.md">Regards de tête et de validation</a></td>
        <td>Par exemple, 3D des présentations, démos des expériences clic</td>
        <td>Nécessite une formation sur HMDs, mais pas sur mobile<br>Idéal pour les contrôleurs accessibles<br>Idéal pour HoloLens (1er gen)</td>
        <td>HoloLens 2<br>HoloLens (1er gen)<br> Immersive de Windows<br> Mobile AR</td>
    </tr>
</table>
<br>

Pour vous assurer qu’aucun vides ou les trous dans l’interaction de votre expérience, la meilleure consiste à suivre les recommandations pour un seul modèle à partir du début à la fin. 

Pour accélérer le développement et conception, nous avons inclus des informations détaillées et des liens vers des images et des exemples de code au sein de notre couverture de chaque modèle.

Mais tout d’abord, les sections ci-dessous décrivent les étapes de sélection et d’implémentation de l’un de ces modèles d’interaction.  
 
### <a name="by-the-end-of-this-page-you-will-understand-our-guidance-on"></a>À la fin de cette page, vous comprendrez nos conseils sur :
 
* Choix d’un modèle d’interaction pour votre client
* En utilisant les instructions de modèle d’interaction
* Transition entre les modèles d’interaction
* Étapes de conception

## <a name="choosing-an-interaction-model-for-your-customer"></a>Choix d’un modèle d’interaction pour votre client

Les développeurs et les créateurs de disposent déjà probablement quelques idées à l’esprit des types d’expérience d’interaction qu’ils souhaitent pour leurs utilisateurs.
Pour encourager une approche axée sur le client pour concevoir, nous vous recommandons de suivre les instructions ci-dessous pour sélectionner le modèle d’interaction qui est optimisé pour votre client.

### <a name="why-follow-this-guidance"></a>Pourquoi suivre ce guide ?

* Nos modèles d’interaction sont testés pour les objectifs et critères subjectifs tels que des efforts physiques et cognitive, intuitiveness et learnability. 
* Car diffère de l’interaction, intuitivité audio et visuelles et comportement des objets peuvent également différer entre les modèles d’interaction.  
* Combinant des parties de plusieurs modèles d’interaction crée le risque de concurrents intuitivité, telles que des rayons main simultanées et un curseur en regard, qui submerger et la confusion chez les utilisateurs.

Voici quelques exemples de la façon dont les intuitivité et comportements sont optimisés pour chaque modèle d’interaction.  Nous le constatons souvent nouveaux utilisateurs en tant que des questions similaires, tels que « comment savoir si le système fonctionne, comment savoir ce que je peux faire, et comment savoir si elle compris ce que je viens de faire ? »

<br>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Modèle</strong></td>
        <td><strong>Comment savoir qu’il fonctionne ?</strong></td>
        <td><strong>Comment savoir ce que puis-je faire ?</strong></td>
        <td><strong>Comment savoir ce que je viens de faire ?</strong></td>
    </tr>
    <tr>
        <td><a href="hands-and-tools.md">Mains et outils</a></td>
        <td>Je vois une main de maillage, je vois un intuitif du bout des doigts ou une main / contrôleur de rayons.</td>
        <td>Je vois des handles grabbable ou un rectangle englobant s’affichent lorsque ma main est proche.</td>
        <td>J’ai entendre des tonalités sonores et voir les animations sur la manipulation et la mise en production.</td>
    </tr>
    <tr>
        <td><a href="gaze-and-commit.md">Regards de tête et de validation</a></td>
        <td>Je vois un curseur dans le centre de mon champ de vision.</td>
        <td>Le curseur du pointage de regard modifie l’état lorsque sur certains objets.</td>
        <td>J’ai consultez / entendre les confirmations et sonores quand prendre des mesures.</td>
    </tr>   
    <tr>
        <td><a href="hands-free.md">Mains libres (regards et durée d’affichage)</a></td>
        <td>Je vois un curseur dans le centre de mon champ de vision.</td>
        <td>Je vois un indicateur de progression lorsque je m’attarderai pas sur un objet sur.</td>
        <td>J’ai consultez / entendre les confirmations et sonores quand prendre des mesures.</td>
    </tr>
    <tr>
        <td><a href="hands-free.md">Mains libres (exécution des commandes vocales)</a></td>
        <td>Je vois un indicateur à l’écoute et sous-titres codés qui montrent ce que le système entendu parler.</td>
        <td>J’obtiens des indicateurs et des invites vocales.  Lorsque je dis « que puis-je dire ? » Je vois des commentaires.</td>
        <td>J’ai consultez / entendre les confirmations et sonores lorsque j’ai une commande ou obtenir de levée d’ambiguïté l’expérience utilisateur si nécessaire.</a></td>
    </tr>
</table>

### <a name="below-are-the-questions-that-weve-found-help-teams-select-an-interaction-model"></a>Voici les questions que nous avons constaté aide les équipes sélectionnez un modèle d’interaction :
 
1.  Q :  Mes utilisateurs voulez-vous touch hologrammes et effectuer des manipulations de précision HOLOGRAPHIQUE ?
R :  Dans ce cas, consultez le modèle d’interaction des mains et pour le ciblage de précision et de manipulation avec mains ou contrôleurs de mouvement.
 
2.  Q :  Mes utilisateurs doivent-ils conserver leurs mains gratuits pour les tâches réelles ?
R :  Dans ce cas, examinons le modèle d’interaction mains-libres, qui fournit une excellente expérience mains libres par le biais du pointage de regard et vocale basée sur les interactions.
 
3.  Q :  Mes utilisateurs doivent-ils disposer les temps d’apprendre les interactions pour mon application de réalité mixte, ou doivent-elles les interactions avec la courbe d’apprentissage la plus basse possible ?
R :  Nous recommandons le modèle des mains et pour la courbe d’apprentissage la plus faible et des interactions plus intuitives, tant que les utilisateurs sont en mesure d’utiliser leurs mains pour l’interaction.
 
4.  Q :  Mes utilisateurs utilisent des contrôleurs de mouvement pour pointant et manipulation ?
R :  Le modèle de mains et inclut tous les conseils pour une bonne expérience des contrôleurs de mouvement.
 
5.  Q :  Mes utilisateurs utilisent-elles un contrôleur d’accessibilité ou un contrôleur Bluetooth courantes, comme un clicker ?
R :  Nous recommandons le modèle regards de tête et de validation pour tous les contrôleurs non suivies.  Il est conçu pour autoriser un utilisateur à parcourir une expérience entière avec une simple garagiste « cible et validation ». 
 
6.  Q : Mes utilisateurs uniquement la progression via une expérience cliquant « via » (par exemple dans un environnement semblable à diaporama 3d), par opposition à la navigation dans les dispositions denses de contrôles d’interface utilisateur ?
R :  Si les utilisateurs n’ont pas besoin de contrôler un grand nombre de l’interface utilisateur, Head-regards et validation offre une option de demande où les utilisateurs n’ont pas à vous soucier de ciblage. 
 
7.  Q :  Mes utilisateurs utilisent-ils les deux HoloLens (1er gen) et HoloLens 2 / A: Immersive de Windows (casques VR)  Dans la mesure où les regards de tête et de validation est le modèle d’interaction pour HoloLens (1er gen), nous vous recommandons créateurs qui prennent en charge de HoloLens (1er gen) utiliser regards de tête et de validation pour les fonctionnalités ou les modes d’utilisateurs peut se produire sur un HoloLens (1er gen) casque.  Consultez la section suivante ci-dessous sur *transition des modèles d’interaction* pour plus d’informations sur la création d’une expérience optimale pour plusieurs générations de HoloLens.
 
8.  Q : Qu’en est-il pour les utilisateurs qui sont généralement mobiles (couvrant un large espace ou de déplacement entre des espaces), et les utilisateurs qui ont tendance à fonctionner dans un seul espace ?  
R :  Les modèles d’interaction de fonctionnera pour ces utilisateurs.  

> [!NOTE]
> Obtenir des instructions spécifiques à la conception d’applications [bientôt](index.md#news-and-notes).


## <a name="transition-interaction-models"></a>Modèles d’interaction de transition
Il existe également des cas où vos cas d’usage peuvent nécessiter qu’utilisant plus d’un modèle d’interaction.  Par exemple, votre flux d’application « création » utilise le modèle d’interaction des mains et, mais que vous souhaitez employer un mode mains libres pour les techniciens du terrain.  

Si votre expérience requiert plusieurs modèles d’interaction, nous avons constaté que nombreux utilisateurs finaux peuvent rencontrer des difficultés de transition d’un modèle à un autre, en particulier les utilisateurs finaux qui débutent avec MR.

> [!Note]
> Pour aider les concepteurs de guide et les développeurs à travers les choix qui peut s’avérer difficile dans MR, nous travaillons sur plus de conseils pour l’utilisation de plusieurs modèles d’interaction.
 

## <a name="see-also"></a>Voir aussi
* [Regards de tête et de validation](gaze-and-commit.md)
* [Manipulation directe](direct-manipulation.md)
* [Point et validation](point-and-commit.md)
* [Pointage du regard](gaze-targeting.md)
* [Mouvements](gestures.md)
* [Conception de la voix](voice-design.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Conception du son spatial](spatial-sound-design.md)
* [Conception du mappage spatial](spatial-mapping-design.md)
* [Confort](comfort.md)
