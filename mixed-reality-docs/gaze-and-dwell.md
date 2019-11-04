---
title: Point de regard
description: Présentation générale du modèle d’entrée (œil/tête) du regard et du point d’entrée
author: sostel
ms.author: sostel
ms.date: 10/31/2019
ms.topic: article
keywords: La réalité mixte, le regard, le point de présence, l’interaction, la conception, le suivi des yeux, le suivi des têtes
ms.openlocfilehash: d87406d0b2695cd86c40f27cb132af54ed525b25
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73435355"
---
# <a name="gaze-and-dwell"></a>Point de regard

Quand les mains sont occupées avec des outils et des pièces, les mouvements peuvent être fastidieux, voire impossibles. Les commandes vocales peuvent également être peu fiables dans certains contextes, par exemple dans des conditions excessivement intenses. Le point de regard et le point de vue offre un mécanisme familier et facile à maîtriser pour le fonctionnement des têtes et des mains libres sur HoloLens. En outre, le point de regard et le bruit est un excellent secours, qui est indépendant des contraintes de bruit ou de silence dans l’environnement d’exploitation.
Nous distingueons deux variantes de point de _regard_et de [tête : le point](gaze-and-dwell-head.md) de regard et le point d’appui [.](gaze-and-dwell-eyes.md)

## <a name="scenarios"></a>Scénarios

Le point de vue et le point de vue dans les scénarios où les mains d’une personne sont occupés avec d’autres tâches, et la voix n’est pas 100% fiable ou disponible en raison de contraintes environnementales ou sociales. Un bon exemple est une personne portant un appareil HoloLens pour superposer des informations de référence tout en réparant un moteur de voiture. Ses mains sont occupées par des outils ou supportent son corps quand elle se penche dans le compartiment du moteur. L’espace du garage est bruyant, les coups et bourdonnement constants des outils rendant difficile l’utilisation de commandes vocales. Le point de regard permet à la personne utilisant HoloLens de parcourir en toute confiance son document de référence sans interrompre son flux de travail. 

## <a name="device-support"></a>Périphériques pris en charge

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Modèle d’entrée</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Suivre de la tête et stabiliser</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé</td>
        <td>✔️ Recommandé</td>
    </tr>
     <tr>
        <td>Œil-point de regard</td>
        <td>❌ non disponible</td>
        <td>✔️ Recommandé</td>
        <td>❌ non disponible</td>
    </tr>
</table>


<br>

---
 
 ## <a name="see-also"></a>Articles associés
* [Interaction basée sur les yeux](eye-gaze-interaction.md)
* [Suivi des yeux sur HoloLens 2](eye-tracking.md)
* [Point de regard et validation](gaze-and-commit.md)
* [Manipulation directe](direct-manipulation.md)
* [Mouvements pratiques](gaze-and-commit.md#composite-gestures)
* [Mains et validation](point-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Entrée vocale](voice-input.md)
