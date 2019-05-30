---
title: Vue d’ensemble de l’interaction multimodale
description: Vue d’ensemble de l’interaction multimodale
author: shengkait
ms.author: shengkait
ms.date: 04/11/2019
ms.topic: article
ms.localizationpriority: high
keywords: Mixte réalité, les regards, les regards ciblant, interaction, concevez, hololens, MMR, multimodale
ms.openlocfilehash: d018179e20d26ee8b7b24bc74d7c1711bc788282
ms.sourcegitcommit: aba33a8ad1416f7598048ac35ae9ab1734bd5c37
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270385"
---
# <a name="introducing-instinctual-interactions"></a>Présentation des interactions instinctual

La philosophie d’interactions simples, instinctual nouée tout au long de la plateforme Microsoft mixte réalité (MMR), du matériel au logiciel.

Ces interactions instinctual utilisent toutes les technologies de d’entrée disponibles, y compris à l’intérieur de suivi main suivi, suivi de le œil et d’extraction du langage naturel, dans les modèles d’interaction multimodale transparente. Selon nos recherches, conception et développement multimodals et non pas sur les entrées uniques, sont essentiel lors de la création d’expériences instinctive.

Les modèles d’Interaction Instinctual alignent également naturellement dans les types d’appareils.  Par exemple, une interaction lointain sur un casque immersive avec un 6 degrés de contrôleur de liberté (DDL) et l’interaction lointain 2 HoloLens utiliser l’intuitivité de même, les modèles et les comportements.  Est non seulement ce pratique pour les développeurs et concepteurs, mais il a l’air normal pour les utilisateurs finaux.


Enfin, alors que nous reconnaissons qu’il existe des milliers d’effective, attrayantes et interactions magiques possibles dans MR, nous avons trouvé cette intentionnellement utilisant un modèle d’interaction unique bout en bout dans une application est la meilleure façon de garantir aux utilisateurs réussissent et offrir une bonne expérience.  À cette fin, nous avons inclus les trois choses dans ce guide de l’interaction :
* Nous avons structuré ce guide autour de trois modèles d’interaction principal et les composants et les modèles requis pour chaque
* Nous avons inclus des conseils supplémentaires sur les autres avantages offerts par notre plateforme
* Nous avons inclus des conseils pour aider à sélectionner le modèle d’interaction approprié pour votre scénario

## <a name="multimodal-interaction-models"></a>Modèles d’interaction multimodale

Selon notre recherche et la collaboration avec les clients à ce jour, nous avons découvert les trois modèles d’interaction principal qui convient à la majorité des expériences de réalité mixte.  

Considérez ces modèles d’interaction comme modèle mental de l’utilisateur pour l’exécution de leurs flux.

Chacun de ces modèles d’interaction est pratique, puissant et utilisable à part entière, et tous sont optimisés pour un ensemble de besoins des clients. Afficher le graphique ci-dessous, pour des scénarios, des exemples et des avantages de chaque modèle d’interaction.  

**Modèle** | **[Mains et contrôleurs de mouvement](hands-and-tools.md)** | **[Mains libres](hands-free.md)** | **[Regards de tête et de validation](gaze-and-commit.md)**
|--------- | --------------| ------------| ---------|
**Exemples de scénarios** | Du contenu 3D expériences spatiales, par exemple spatiale disposition et conception, de manipulation ou de simulation | Expériences contextuelles, où les mains d’un utilisateur sont occupés, par exemple, sur le travail d’apprentissage, de maintenance| Clic des expériences, par exemple, des présentations 3D, des démonstrations
**Fit** | Idéal pour les nouveaux utilisateurs, voix couplée wit, des yeux regards suivi ou principal. Courbe d’apprentissage basse. Expérience utilisateur cohérente entre main suivi et 6 contrôleurs DDL. | Certains d’apprentissage nécessaire. Si les mains sont des paires indisponibles bien avec la voix et de langage naturel | Nécessite une formation sur HMDs, mais pas sur mobile. Idéal pour les contrôleurs accessibles. Idéal pour HoloLens (1er gen). |
**Matériel** | HoloLens 2 <br>Casques immersifs | HoloLens 2 <br>HoloLens (1er gen) <br>Casques immersifs | HoloLens 2 <br>Casques immersifs | HoloLens 2 <br>HoloLens (1er gen) <br>Casques immersifs <br>Mobile AR |

Des informations détaillées pour l’utilisation de toutes les entrées disponibles dans chaque modèle d’interaction entre eux se trouve sur les pages qui suivent, ainsi que les illustrations et les liens vers du contenu de l’exemple à partir de notre MRTK Unity.


## <a name="choose-an-interaction-model-for-your-customer"></a>Choisir un modèle d’interaction pour votre client


Les développeurs et les créateurs d’également disposent déjà probablement quelques idées à l’esprit des types d’expérience d’interaction qu’ils souhaitent leurs utilisateurs d’avoir.
Pour encourager une approche axée sur le client pour concevoir, nous vous recommandons de suivre les instructions ci-dessous pour sélectionner le modèle d’interaction qui est optimisé pour votre client.

### <a name="why-follow-this-guidance"></a>Pourquoi suivre ce guide ?

* Nos modèles d’interaction sont testés pour les objectifs et critères subjectifs tels que des efforts physiques et cognitive, intuitiveness et learnability. 
* Car diffère de l’interaction, intuitivité audio et visuelles et comportement des objets peuvent également différer entre les modèles d’interaction.  
* Combinant des parties de plusieurs modèles d’interaction crée le risque de concurrents intuitivité, telles que des rayons main simultanées et un curseur regards de tête, qui submerger et la confusion chez les utilisateurs.

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
        <td><strong>Comment savoir que puis-je faire ?</strong></td>
        <td><strong>Comment savoir ce que je viens de faire ?</strong></td>
    </tr>
    <tr>
        <td><a href="hands-and-tools.md">Mains et contrôleurs de mouvement</a></td>
        <td>Je vois une main de maillage, je vois un intuitif du bout des doigts ou une main / contrôleur de rayons.</td>
        <td>Je vois des handles grabbable ou un rectangle englobant s’affichent lorsque ma main est proche.</td>
        <td>J’ai entendre des tonalités sonores et voir les animations sur la manipulation et la mise en production.</td>
    </tr>
    <tr>
        <td><a href="gaze-and-commit.md">Suivre de la tête et valider</a></td>
        <td>Je vois un curseur dans le centre de mon champ de vision.</td>
        <td>Le curseur de tête-regards change d’état lorsque sur certains objets.</td>
        <td>J’ai consultez / entendre les confirmations et sonores quand prendre des mesures.</td>
    </tr>   
    <tr>
        <td><a href="hands-free.md">Mains libres (Head-regards et durée d’affichage)</a></td>
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
 
1.  Q :  Mes utilisateurs voulez-vous touch hologrammes et effectuer des manipulations de précision HOLOGRAPHIQUE ?<br><br>
R :  Dans ce cas, consultez le modèle d’interaction des mains et pour le ciblage de précision et de manipulation avec mains ou contrôleurs de mouvement.
 
2.  Q :  Mes utilisateurs doivent-ils conserver leurs mains gratuits pour les tâches réelles ?<br><br>
R :  Dans ce cas, examinons le modèle d’interaction mains-libres, qui fournit une excellente expérience mains libres par le biais du pointage de regard et vocale basée sur les interactions.
 
3.  Q :  Mes utilisateurs doivent-ils disposer les temps d’apprendre les interactions pour mon application de réalité mixte, ou doivent-elles les interactions avec la courbe d’apprentissage la plus basse possible ?<br><br>
R :  Nous recommandons le modèle des mains et pour la courbe d’apprentissage la plus faible et des interactions plus intuitives, tant que les utilisateurs sont en mesure d’utiliser leurs mains pour l’interaction.
 
4.  Q :  Mes utilisateurs utilisent des contrôleurs de mouvement pour pointant et manipulation ?<br><br>
R :  Le modèle de mains et inclut tous les conseils pour une bonne expérience des contrôleurs de mouvement.
 
5.  Q :  Mes utilisateurs utilisent-elles un contrôleur d’accessibilité ou un contrôleur Bluetooth courantes, comme un clicker ?<br><br>
R :  Nous recommandons le modèle regards de tête et de validation pour tous les contrôleurs non suivies.  Il est conçu pour autoriser un utilisateur à parcourir une expérience entière avec une simple garagiste « cible et validation ». 
 
6.  Q : Mes utilisateurs uniquement la progression via une expérience cliquant « via » (par exemple dans un environnement semblable à diaporama 3d), par opposition à la navigation dans les dispositions denses de contrôles d’interface utilisateur ?<br><br>
R :  Si les utilisateurs n’ont pas besoin de contrôler un grand nombre de l’interface utilisateur, Head-regards et validation offre une option de demande où les utilisateurs n’ont pas à vous soucier de ciblage. 
 
7.  Q :  Mes utilisateurs utilisent-ils les deux HoloLens (1er gen) et HoloLens 2 / Immersive de Windows (casques VR)<br><br>
R :  Dans la mesure où les regards de tête et de validation est le modèle d’interaction pour HoloLens (1er gen), nous vous recommandons créateurs qui prennent en charge de HoloLens (1er gen) utiliser regards de tête et de validation pour les fonctionnalités ou les modes d’utilisateurs peut se produire sur un HoloLens (1er gen) casque.  Consultez la section suivante ci-dessous sur *transition des modèles d’interaction* pour plus d’informations sur la création d’une expérience optimale pour plusieurs générations de HoloLens.
 
8.  Q : Qu’en est-il pour les utilisateurs qui sont généralement mobiles (couvrant un large espace ou de déplacement entre des espaces), et les utilisateurs qui ont tendance à fonctionner dans un seul espace ?<br><br>
R :  Les modèles d’interaction de fonctionnera pour ces utilisateurs.  

> [!NOTE]
> Obtenir des instructions spécifiques à la conception d’applications [bientôt](index.md#news-and-notes).


## <a name="transition-interaction-models"></a>Modèles d’interaction de transition
Il existe également des cas où vos cas d’usage peuvent nécessiter qu’utilisant plus d’un modèle d’interaction.  Par exemple, votre flux d’application « création » utilise le modèle d’interaction des mains et, mais que vous souhaitez employer un mode mains libres pour les techniciens du terrain.  

Si votre expérience requiert plusieurs modèles d’interaction, nous avons constaté que nombreux utilisateurs finaux peuvent rencontrer des difficultés de transition d’un modèle à un autre, en particulier les utilisateurs finaux qui débutent avec MR.

> [!Note]
> Pour aider les concepteurs de guide et les développeurs à travers les choix qui peut s’avérer difficile dans MR, nous travaillons sur plus de conseils pour l’utilisation de plusieurs modèles d’interaction.
 

## <a name="see-also"></a>Voir aussi
* [Suivre de la tête et valider](gaze-and-commit.md)
* [Suivre de la tête et stabiliser](gaze-and-dwell.md)
* [Manipulation directe avec les mains](direct-manipulation.md)
* [Pointer et valider avec les mains](point-and-commit.md)
* [Mouvements](gestures.md)
* [Commander avec la voix](voice-design.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Conception du son spatial](spatial-sound-design.md)
* [Conception du mappage spatial](spatial-mapping-design.md)
* [Confort](comfort.md)

