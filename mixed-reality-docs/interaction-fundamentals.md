---
title: Interactions instinctives
description: Découvrez que les interactions simples et instinctives sont étroitement liées dans la plateforme de réalité mixte.
author: shengkait
ms.author: shentan
ms.date: 04/11/2019
ms.topic: article
ms.localizationpriority: high
keywords: Mixed Reality, pointage du regard, ciblage avec le regard, interaction, conception, hololens, MMR, multimodal
ms.openlocfilehash: abd82947be08a2f6aecc4462abc34c4674abfb7a
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437977"
---
# <a name="introducing-instinctual-interactions"></a>Présentation des interactions instinctuelles

Les interactions simples et instinctuelles sont étroitement liées dans la plateforme de réalité mixte. Nous avons suivi trois étapes pour que les développeurs et concepteurs d’applications puissent proposer des interactions faciles et intuitives à leurs clients. 

Tout d’abord, nous avons veillé à combiner en modèles d’interaction multimodale fluides nos capteurs et nos technologies d’entrée (notamment le suivi de la main et oculaire, associé à l’entrée de langage naturel).  
Selon nos recherches, la conception et le développement au sein d’un framework multimodal (plutôt qu’à partir d’entrées individuelles) sont essentiels à la création d’expériences instinctives.

Deuxièmement, nous sommes conscients que de nombreux développeurs ciblent plusieurs appareils HoloLens tels qu’HoloLens 2 et HoloLens (1ère génération) ou HoloLens et VR.  
Nous avons donc conçu nos modèles d’interaction pour qu’ils fonctionnent sur tous les appareils, même si la technologie d’entrée varie d’un appareil à l’autre.  
Par exemple, une interaction de loin sur un casque immersif Windows avec un contrôleur 6DoF et une interaction de loin sur un appareil HoloLens 2 utilisent toutes deux des affordances et des schémas identiques, ce qui facilite le développement d’applications multi-appareils et la proposition d’une sensation naturelle aux interactions des utilisateurs. 

Face aux milliers d’interactions efficaces, attrayantes et magiques possibles qu’offre la réalité mixte, nous avons trouvé que l’utilisation intentionnelle d’un seul modèle d’interaction de bout en bout dans une application est le meilleur gage de réussite et d’expérience agréable pour les utilisateurs. À cette fin, nous avons inclus trois choses dans ce guide d’interaction :
* Des instructions spécifiques autour des trois modèles d’interaction principaux et des composants et schémas requis pour chacun.
* Des conseils supplémentaires sur d’autres avantages qu’offre notre plateforme.
* Des conseils d’ordre général pour vous aider à sélectionner le modèle d’interaction approprié pour votre scénario.

## <a name="multimodal-interaction-models"></a>Modèles d’interaction multimodale

D’après nos recherches et les commentaires des clients, trois modèles d’interaction principaux conviennent pour la majorité des expériences de réalité mixte. À bien des égards, le modèle d’interaction est le modèle mental de l’utilisateur pour l’exécution d’un workflow. Chacun de ces modèles d’interaction est optimisé pour un ensemble de besoins des clients et s’avère pratique, puissant et exploitable dans le cadre d’une utilisation correcte. 

Le tableau ci-dessous offre une vue d’ensemble simplifiée. Vous pouvez cliquer sur les liens ci-après pour obtenir des informations détaillées sur l’utilisation de chaque modèle d’interaction, y compris des images et des exemples de code. 

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
        <td>Expériences 3D spatiales telles que la conception et la disposition spatiales, la manipulation de contenu ou la simulation.</td>
        <td>Idéal pour les nouveaux utilisateurs en liaison avec la voix, le suivi oculaire ou le suivi de la tête. Courbe d’apprentissage basse. Expérience utilisateur cohérente entre le suivi de la main et les contrôleurs 6DoF.</td>
        <td>HoloLens 2<br>Casques immersifs</td>
    </tr>
    <tr>
        <td><a href="hands-free.md">Mains-libres</a></td>
        <td>Expériences contextuelles où les mains d’un utilisateur sont occupées, par exemple dans le cadre d’un apprentissage « sur le tas » et d’une maintenance.</td>
        <td>Un apprentissage est requis. Si les mains ne sont pas disponibles, l’appareil peut être associé à la voix et au langage naturel.</td>
        <td>HoloLens 2<br>HoloLens (1ère génération)<br>Casques immersifs</td>
    </tr>
    <tr>
        <td><a href="gaze-and-commit.md">Pointer et valider</a></td>
        <td>Expériences au moyen de clics, par exemple, présentations 3D et démonstrations.</td>
        <td>Nécessite une formation sur les appareils HMD, mais pas sur mobile. Idéal pour les contrôleurs accessibles. Idéal pour HoloLens (1ère génération).</td>
        <td>HoloLens 2<br>HoloLens (1ère génération)<br>Casques immersifs<br>Réalité augmentée mobile</td>
    </tr>
</table>
<br>

Pour qu’il n’y ait pas de vides dans l’expérience d’interaction de l’utilisateur, le mieux est de suivre les conseils pour un modèle unique du début à la fin.

Les sections ci-dessous décrivent les étapes de sélection et d’implémentation de l’un de ces modèles d’interaction.  
 
### <a name="by-the-end-of-this-page-you-will-understand-our-guidance-on"></a>Quand vous parviendrez à la fin de cette page, vous comprendrez nos conseils sur :
 
* Le choix d’un modèle d’interaction pour votre client
* Implémentation du modèle d’interaction
* Le passage d’un modèle d’interaction à un autre
* Les étapes suivantes de la conception


## <a name="choose-an-interaction-model-for-your-customer"></a>Choisir un modèle d’interaction pour votre client

Généralement, les développeurs et les créateurs ont envisagé les types d’interactions que leurs clients peuvent avoir. Pour encourager une approche conceptuelle axée sur le client, nous vous recommandons de suivre les conseils suivants afin de sélectionner le modèle d’interaction qui est optimisé pour votre client.

### <a name="why-follow-this-guidance"></a>Pourquoi suivre ces conseils ?

* Nos modèles d’interaction sont testés en fonction de critères objectifs et subjectifs tels que les efforts physiques et cognitifs, l’intuitivité et la facilité d’apprentissage. 
* Tout comme les interactions, les affordances visuelles/audio et le comportement des objets peuvent varier d’un modèle d’interaction à l’autre.  
* La combinaison de parties de plusieurs modèles d’interaction crée le risque d’affordances concurrentes, à l’image de rayons émanant de la main et d’un curseur oculaire simultanés. Cette expérience peut submerger et perturber les utilisateurs.

Voici quelques exemples d’optimisation des affordances et des comportements pour chaque modèle d’interaction. Nous constatons souvent que les nouveaux utilisateurs ont des questions similaires, telles que _« comment savoir si le système fonctionne ? »_ , _« comment savoir ce que je peux faire ? »_ et _« comment savoir s’il a compris ce que je viens de faire ? »_ .

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
        <td>Je vois un maillage de main, une affordance d’extrémité de doigt ou des rayons de contrôleur/sortant de la main.</td>
        <td>Des poignées déplaçables ou un rectangle englobant apparaissent quand ma main est proche d’un objet.</td>
        <td>J’entends des tonalités et vois des animations quand je saisis ou libère un objet.</td>
    </tr>
    <tr>
        <td><a href="gaze-and-commit.md">Suivre de la tête et valider</a></td>
        <td>Je vois un curseur au centre de mon champ de vision.</td>
        <td>Le curseur change d’état en fonction de l’objet au-dessus duquel il se trouve.</td>
        <td>Je vois/j’entends des confirmations visuelles et sonores quand j’effectue une action.</td>
    </tr>   
    <tr>
        <td><a href="hands-free.md">Mains-libres (Suivre de la tête et stabiliser)</a></td>
        <td>Je vois un curseur au centre de mon champ de vision.</td>
        <td>Je vois un indicateur de progression quand je reste sur un objet avec interaction possible.</td>
        <td>Je vois/j’entends des confirmations visuelles et sonores quand j’effectue une action.</td>
    </tr>
    <tr>
        <td><a href="hands-free.md">Mains-libres (commander avec la voix)</a></td>
        <td>Je vois un indicateur à l’écoute et des légendes qui montrent ce que le système a entendu.</td>
        <td>J’obtiens des indicateurs et des invites vocales. Quand je dis : Qu’est-ce que je dis ? je vois un retour.</td>
        <td>Je vois/entends des confirmations visuelles et sonores quand je donne une commande ou obtiens une expérience utilisateur de levée d’ambiguïté si nécessaire.</a></td>
    </tr>
</table>

### <a name="below-are-questions-that-weve-found-help-teams-select-an-interaction-model"></a>Voici les questions qui, d’après nous, aident les équipes à sélectionner un modèle d’interaction :
 
1.  Q :  Les utilisateurs souhaitent-ils toucher des hologrammes et effectuer des manipulations holographiques de précision ?<br><br>
R :  Si tel est le cas, consultez le modèle d’interaction Mains et contrôleurs de mouvement pour un ciblage et une manipulation de précision.
 
2.  Q :  Les utilisateurs doivent-ils conserver leurs mains libres pour les tâches réelles ?<br><br>
R :  Si tel est le cas, examinez le modèle d’interaction sans les mains, qui fournit une excellente expérience sans les mains par le biais d’interactions vocales et par pointage du regard.
 
3.  Q :  Les utilisateurs ont-ils le temps d’apprendre les interactions pour mon application de réalité mixte ou ont-ils besoin des interactions présentant la courbe d’apprentissage la plus basse possible ?<br><br>
R :  Nous recommandons le modèle Mains et contrôleurs de mouvement pour la courbe d’apprentissage la plus basse et les interactions les plus intuitives, sous réserve que les utilisateurs puissent recourir à leurs mains pour les interactions.
 
4.  Q :  Les utilisateurs utilisent-ils des contrôleurs de mouvement pour les opérations de pointage et de manipulation ?<br><br>
R :  Le modèle Mains et contrôleurs de mouvement inclut tous les conseils pour une bonne expérience des contrôleurs de mouvement.
 
5.  Q :  Les utilisateurs se servent-ils d’un contrôleur d’accessibilité ou d’un contrôleur Bluetooth courant, tel qu’un dispositif de clic ?<br><br>
R :  Nous recommandons le modèle Suivre de la tête et valider pour tous les contrôleurs non suivis. Il est conçu pour permettre à un utilisateur de parcourir une expérience entière avec un simple mécanisme de type « ciblage et validation ». 
 
6.  Q : Les utilisateurs progressent-ils dans une expérience uniquement par le biais de clics (comme dans un environnement de type diaporama 3D), par opposition à la navigation dans des dispositions denses de contrôles d’interface utilisateur ?<br><br>
R :  Si les utilisateurs n’ont pas besoin de contrôler une interface utilisateur conséquente, le modèle Suivre de la tête et valider offre une option accessible où ils n’ont pas besoin de se soucier du ciblage. 
 
7.  Q :  Les utilisateurs utilisent-ils à la fois des casques immersifs appareil HoloLens (1ère génération) et HoloLens 2/Windows Mixed Reality (VR) ?<br><br>
R :  Dans la mesure où le modèle Suivre de la tête et valider est le modèle d’interaction pour HoloLens (1ère génération), nous recommandons aux créateurs qui prennent en charge HoloLens (1ère génération) d’utiliser ce modèle pour les fonctionnalités ou les modes que les utilisateurs vivront sur un casque HoloLens (1ère génération). Consultez la section ci-dessous *Passage d’un modèle d’interaction à un autre* pour plus d’informations sur la création d’une expérience optimale pour plusieurs générations de dispositifs HoloLens.
 
8.  Q : Qu’en est-il des utilisateurs qui sont généralement mobiles, dans un large espace ou en raison de déplacements entre des espaces, et des utilisateurs qui ont tendance à travailler dans un seul espace ?<br><br>
R :  Tous les modèles d’interaction fonctionnent pour ces utilisateurs.  

> [!NOTE]
> Des conseils spécifiques à la conception d’applications seront [bientôt](news.md) disponibles.


## <a name="transitioning-interaction-models"></a>Passage d’un modèle d’interaction à un autre
Certains cas d’usage peuvent nécessiter l’utilisation de plusieurs modèles d’interaction. Par exemple, le flux de création de votre application utilise le modèle d’interaction _« Mains et contrôleurs de mouvement »_ , mais vous souhaitez employer un mode sans mains pour les techniciens de terrain.
Si votre expérience requiert plusieurs modèles d’interaction, n’oubliez pas que de nombreux utilisateurs peuvent rencontrer des difficultés pour passer d’un modèle à un autre, en particulier les utilisateurs pour lesquels la réalité mixte est une nouveauté.

> [!Note]
> Nous travaillons en permanence sur des conseils supplémentaires qui seront mis à la disposition des développeurs et des concepteurs et les informeront de la manière, du moment et de la raison de l’utilisation de plusieurs modèles d’interaction RM.
 

## <a name="see-also"></a>Voir également
* [Confort](comfort.md)
* [Interaction basée sur le regard](eye-gaze-interaction.md)
* [Suivi oculaire sur HoloLens 2](eye-tracking.md)
* [Pointer et valider](gaze-and-commit.md)
* [Pointer du regard et fixer](gaze-and-dwell.md)
* [Mains : Manipulation directe](direct-manipulation.md)
* [Mains : Mouvements](gaze-and-commit.md#composite-gestures)
* [Mains : Pointer et valider](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Mappage spatial](spatial-mapping.md)
* [Conception du son spatial](spatial-sound-design.md)
* [Entrée vocale](voice-input.md)


