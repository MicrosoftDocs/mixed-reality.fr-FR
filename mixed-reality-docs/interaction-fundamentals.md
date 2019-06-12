---
title: Vue d’ensemble de l’interaction multimodale
description: Vue d’ensemble de l’interaction multimodale
author: shengkait
ms.author: shengkait
ms.date: 04/11/2019
ms.topic: article
ms.localizationpriority: high
keywords: Mixed Reality, pointage du regard, ciblage avec le regard, interaction, conception, hololens, MMR, multimodal
ms.openlocfilehash: bea205edf484a55db701e8e0d1a233234882a272
ms.sourcegitcommit: 9b6949d7cd2e67e6bde9b32aebeaeea325baa6c4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66516019"
---
# <a name="introducing-instinctual-interactions"></a>Présentation des interactions instinctuelles

Les interactions simples et instinctuelles constituent la trame philosophique de la plateforme Microsoft Mixed Reality.  Nous avons suivi trois étapes pour que les développeurs et concepteurs d’applications puissent proposer des interactions faciles et intuitives à leurs clients. 

Tout d’abord, nous avons veillé à combiner en modèles d’interaction multimodale fluides nos capteurs et notre technologie d’entrée extraordinaires, notamment le suivi de la main, le suivi du regard et le langage naturel.  Selon nos recherches, la conception et le développement sous forme multimodale, plutôt qu’à partir d’entrées uniques, sont essentiels à la création d’expériences instinctuelles.

Deuxièmement, nous sommes conscients que de nombreux développeurs ciblent plusieurs appareils, que ce soit HoloLens 2 et HoloLens (1ère génération) ou HoloLens et VR.  Nous avons donc conçu nos modèles d’interaction pour qu’ils fonctionnent sur tous les appareils (même si la technologie d’entrée varie d’un appareil à l’autre).  Par exemple, une interaction de loin sur un casque immersif Windows avec un contrôleur 6DOF et une interaction de loin sur un appareil HoloLens 2 utilisent toutes deux des affordances et des schémas identiques, ce qui rend les choses plus faciles pour les applications multi-appareils. Cela est pratique pour les développeurs et les concepteurs et naturel pour les utilisateurs finaux. 

Enfin, face aux milliers d’interactions efficaces, attrayantes et magiques possibles qu’offre la réalité mixte, nous avons trouvé que l’utilisation intentionnelle d’un seul modèle d’interaction de bout en bout dans une application est le meilleur gage de réussite et d’expérience agréable pour les utilisateurs.  À cette fin, nous avons inclus trois choses dans ce guide d’interaction :
* Nous avons structuré ce guide autour des trois modèles d’interaction principaux et des composants et schémas requis pour chacun
* Nous avons inclus des conseils supplémentaires sur d’autres avantages qu’offre notre plateforme
* Nous avons inclus des conseils afin de vous aider à sélectionner le modèle d’interaction approprié pour votre scénario

## <a name="multimodal-interaction-models"></a>Modèles d’interaction multimodale

D’après nos recherches et la collaboration avec certains clients jusqu’à ce jour, trois modèles d’interaction principaux conviennent pour la majorité des expériences de réalité mixte.

Dans bien des égards, le modèle d’interaction est le modèle mental de l’utilisateur pour l’exécution de ses flux.  Chacun de ces modèles d’interaction est optimisé pour un ensemble de besoins des clients, et chacun est pratique, puissant et utilisable à part entière. 

Le tableau ci-dessous offre une vue d’ensemble simplifiée.  Vous pouvez cliquer sur les liens ci-après pour obtenir des informations détaillées sur l’utilisation de chaque modèle d’interaction, y compris des images et des exemples de code. 

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
        <td><strong>Exemples de scénario</strong></td>
        <td><strong>Cadre</strong></td>
        <td><strong>Matériel</strong></td>
    </tr>
    <tr>
        <td><a href="hands-and-tools.md">Mains et contrôleurs de mouvement</a></td>
        <td>Expériences 3D spatiales, par exemple conception et disposition spatiales, manipulation de contenu ou simulation.</td>
        <td>Idéal pour les nouveaux utilisateurs, couplé avec la voix, le suivi du regard ou le suivi de la tête. Courbe d’apprentissage basse. Expérience utilisateur cohérente entre le suivi de la main et les contrôleurs 6DOF.</td>
        <td>HoloLens 2<br>Casques immersifs</td>
    </tr>
    <tr>
        <td><a href="hands-free.md">Mains-libres</a></td>
        <td>Expériences contextuelles où les mains d’un utilisateur sont occupées, par exemple, dans le cadre d’un apprentissage « sur le tas » ou d’une maintenance.</td>
        <td>Un apprentissage est requis. Si les mains ne sont pas disponibles, peut être associé à la voix et au langage naturel.</td>
        <td>HoloLens 2<br>HoloLens (1ère génération)<br>Casques immersifs</td>
    </tr>
    <tr>
        <td><a href="gaze-and-commit.md">Suivre de la tête et valider</a></td>
        <td>Expériences au moyen de clics, par exemple, présentations 3D et démonstrations.</td>
        <td>Nécessite une formation sur les appareils HMD, mais pas sur mobile. Idéal pour les contrôleurs accessibles. Idéal pour HoloLens (1ère génération).</td>
        <td>HoloLens 2<br>HoloLens (1ère génération)<br>Casques immersifs<br>Réalité augmentée mobile</td>
    </tr>
</table>
<br>

Pour que l’interaction de votre expérience soit dépourvue de vides ou de trous, la meilleure approche consiste à suivre le guide pour un modèle unique du début à la fin. 

Pour accélérer le développement et la conception, nous avons inclus des informations détaillées et des liens vers des images et des exemples de code dans la couverture de chaque modèle.

Mais tout d’abord, les sections ci-dessous décrivent les étapes de sélection et d’implémentation de l’un de ces modèles d’interaction.  
 
### <a name="by-the-end-of-this-page-you-will-understand-our-guidance-on"></a>Quand vous parviendrez à la fin de cette page, vous comprendrez nos conseils sur :
 
* Le choix d’un modèle d’interaction pour votre client
* L’utilisation du guide des modèles d’interaction
* Le passage d’un modèle d’interaction à un autre
* Les étapes suivantes de la conception


## <a name="choose-an-interaction-model-for-your-customer"></a>Choisir un modèle d’interaction pour votre client


Les développeurs et les créateurs ont déjà probablement une idée des types d’expérience d’interaction qu’ils souhaitent proposer à l’utilisateur.
Pour encourager une approche conceptuelle axée sur le client, nous vous recommandons de suivre les conseils ci-dessous afin de sélectionner le modèle d’interaction qui est optimisé pour votre client.

### <a name="why-follow-this-guidance"></a>Pourquoi suivre ces conseils ?

* Nos modèles d’interaction sont testés en fonction de critères objectifs et subjectifs, tels que les efforts physiques et cognitifs, l’intuitivité et la facilité d’apprentissage. 
* L’interaction pouvant varier, les affordances visuelles et audio et le comportement des objets peuvent également différer d’un modèle d’interaction à l’autre.  
* La combinaison de parties de plusieurs modèles d’interaction crée le risque d’affordances concurrentes, à l’image de rayons sortant de la main et d’un curseur de suivi de la tête simultanés, qui peuvent submerger et perturber l’utilisateur.

Voici quelques exemples d’optimisation des affordances et des comportements pour chaque modèle d’interaction.  Nous constatons souvent que les nouveaux utilisateurs ont des questions similaires, telles que « comment savoir si le système fonctionne ? », « comment savoir ce que je peux faire ? » et « comment savoir s’il a compris ce que je viens de faire ? ».

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
        <td><strong>Comment savoir si ça fonctionne ?</strong></td>
        <td><strong>Comment savoir ce que je peux faire ?</strong></td>
        <td><strong>Comment savoir ce que je viens de faire ?</strong></td>
    </tr>
    <tr>
        <td><a href="hands-and-tools.md">Mains et contrôleurs de mouvement</a></td>
        <td>Je vois un maillage de main, je vois une affordance d’extrémité de doigt ou des rayons de contrôleur ou sortant de la main.</td>
        <td>Des poignées déplaçables ou un rectangle englobant apparaissent quand ma main est proche.</td>
        <td>J’entends des tonalités et vois des animations quand je saisis ou libère un objet.</td>
    </tr>
    <tr>
        <td><a href="gaze-and-commit.md">Suivre de la tête et valider</a></td>
        <td>Je vois un curseur au centre de mon champ de vision.</td>
        <td>Le curseur de suivi de la tête change d’état en fonction de l’objet au-dessus duquel il se trouve.</td>
        <td>Je vois/entends des confirmations visuelles et sonores quand j’effectue une action.</td>
    </tr>   
    <tr>
        <td><a href="hands-free.md">Mains-libres (Suivre de la tête et stabiliser)</a></td>
        <td>Je vois un curseur au centre de mon champ de vision.</td>
        <td>Je vois un indicateur de progression quand je reste sur un objet avec interaction possible.</td>
        <td>Je vois/entends des confirmations visuelles et sonores quand j’effectue une action.</td>
    </tr>
    <tr>
        <td><a href="hands-free.md">Mains-libres (commander avec la voix)</a></td>
        <td>Je vois un indicateur à l’écoute et des légendes qui montrent ce que le système a entendu.</td>
        <td>J’obtiens des indicateurs et des invites vocales.  Quand je dis « what can I say ? », je vois un retour.</td>
        <td>Je vois/entends des confirmations visuelles et sonores quand je donne une commande ou obtiens une expérience utilisateur de levée d’ambiguïté si nécessaire.</a></td>
    </tr>
</table>

### <a name="below-are-the-questions-that-weve-found-help-teams-select-an-interaction-model"></a>Voici les questions qui, d’après nous, aident les équipes à sélectionner un modèle d’interaction :
 
1.  Q :  Les utilisateurs souhaitent-ils toucher des hologrammes et effectuer des manipulations holographiques de précision ?<br><br>
R :  Si tel est le cas, consultez le modèle d’interaction Mains et outils pour le ciblage et la manipulation de précision avec les mains ou des contrôleurs de mouvement.
 
2.  Q :  Les utilisateurs doivent-ils conserver leurs mains libres pour les tâches réelles ?<br><br>
R :  Si tel est le cas, examinez le modèle d’interaction Mains-libres, qui fournit une excellente expérience mains-libres par le biais d’interactions vocales et par pointage du regard.
 
3.  Q :  Les utilisateurs ont-ils le temps d’apprendre les interactions pour mon application de réalité mixte ou ont-ils besoin des interactions présentant la courbe d’apprentissage la plus basse possible ?<br><br>
R :  Nous recommandons le modèle Mains et outils pour la courbe d’apprentissage la plus basse et les interactions les plus intuitives, sous réserve que les utilisateurs puissent recourir à leurs mains pour les interactions.
 
4.  Q :  Les utilisateurs utilisent-ils des contrôleurs de mouvement pour les opérations de pointage et de manipulation ?<br><br>
R :  Le modèle Mains et outils inclut tous les conseils pour une bonne expérience des contrôleurs de mouvement.
 
5.  Q :  Les utilisateurs se servent-ils d’un contrôleur d’accessibilité ou d’un contrôleur Bluetooth courant, tel qu’un dispositif de clic ?<br><br>
R :  Nous recommandons le modèle Suivre de la tête et valider pour tous les contrôleurs non suivis.  Il est conçu pour permettre à un utilisateur de parcourir une expérience entière avec un simple mécanisme de type « ciblage et validation ». 
 
6.  Q : Les utilisateurs progressent-ils dans une expérience uniquement par le biais de clics (comme dans un environnement de type diaporama 3D), par opposition à la navigation dans des dispositions denses de contrôles d’interface utilisateur ?<br><br>
R :  Si les utilisateurs n’ont pas besoin de contrôler une interface utilisateur conséquente, le modèle Suivre de la tête et valider offre une option accessible où ils n’ont pas besoin de se soucier du ciblage. 
 
7.  Q :  Les utilisateurs utilisent-ils à la fois un appareil HoloLens (1ère génération) et un appareil immersif Windows/HoloLens 2 (casques VR) ?<br><br>
R :  Dans la mesure où le modèle Suivre de la tête et valider est le modèle d’interaction pour HoloLens (1ère génération), nous recommandons aux créateurs qui prennent en charge HoloLens (1ère génération) d’utiliser ce modèle pour les fonctionnalités ou les modes que les utilisateurs sont susceptibles d’expérimenter sur un casque HoloLens (1ère génération).  Consultez la section ci-dessous *Passage d’un modèle d’interaction à un autre* pour plus d’informations sur la création d’une expérience optimale pour plusieurs générations de dispositifs HoloLens.
 
8.  Q : Qu’en est-il des utilisateurs qui sont généralement mobiles (dans un large espace ou se déplaçant entre des espaces) et des utilisateurs qui ont tendance à travailler dans un seul espace ?<br><br>
R :  Tous les modèles d’interaction fonctionnent pour ces utilisateurs.  

> [!NOTE]
> Des conseils spécifiques à la conception d’applications seront [bientôt](index.md#news-and-notes) disponibles.


## <a name="transition-interaction-models"></a>Passage d’un modèle d’interaction à un autre
Il peut également arriver que vos cas d’usage nécessitent l’utilisation de plusieurs modèles d’interaction.  Par exemple, le « flux de création » de votre application utilise le modèle d’interaction Mains et contrôleurs de mouvement, mais vous souhaitez employer un mode mains-libres pour les techniciens de terrain.  

Si votre expérience requiert plusieurs modèles d’interaction, nous avons constaté que de nombreux utilisateurs finaux peuvent rencontrer des difficultés pour passer d’un modèle à un autre, en particulier les utilisateurs pour lesquels la réalité mixte est une nouveauté.

> [!Note]
> Pour guider les concepteurs et les développeurs dans les choix éventuellement difficiles dans le domaine de la réalité mixte, nous travaillons à l’approfondissement de l’aide sur l’utilisation de plusieurs modèles d’interaction.
 

## <a name="see-also"></a>Voir également
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

