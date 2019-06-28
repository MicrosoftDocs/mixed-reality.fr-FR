---
title: Pointage du regard
description: Regards est la première forme d’entrée et un principal de ciblage dans la réalité mixte.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: Mixte réalité, regards, interaction, concevoir
ms.openlocfilehash: 7e65d26d3e9edabbd01d35a887ffc8622a3c6337
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414369"
---
# <a name="gaze"></a>Pointage du regard

**Utilisation** est la première forme d’entrée et un principal de ciblage dans la réalité mixte. Regards vous indique où l’utilisateur recherche dans le monde et vous permet de déterminer leur intention. Dans le monde réel, vous ferez généralement à un objet que vous avez l’intention d’interagir avec. Il s’agit même avec les regards.

Casques de réalité mixte utilisent la position et l’orientation de tête de l’utilisateur pour déterminer leur vecteur regards principal. Vous pouvez considérer ce vecteur comme un pointeur laser directement à l’avance de directement entre les yeux de l’utilisateur. Comme l’utilisateur semble autour de la pièce, votre application peut se croisent ce rayon, avec son propre hologrammes et avec le [mappage spatial](spatial-mapping.md) maille pour déterminer quel objet virtuel ou réelles de votre utilisateur peut regarder.

Sur HoloLens 2, interactions peuvent être ciblées par principal du pointage de regard soit l’utilisateur, les regards yeux via près ou présent distribuer les interactions.
Sur HoloLens (1er gen), les interactions doivent dériver généralement leur ciblage à partir des regards principal de l’utilisateur, au lieu d’essayer restituer ou interagir directement à l’emplacement de la part. Une fois démarrée, une interaction des mouvements relatifs de la main peuvent être utilisé pour contrôle le [mouvement](gestures.md), comme avec la [manipulation ou navigation](gestures.md#composite-gestures) mouvement. Avec des casques IMMERSIFS, vous pouvez cibler à l’aide soit du pointage de regard principal ou de pointage compatible [contrôleurs de mouvement](motion-controllers.md).

<br>

>[!VIDEO https://www.youtube.com/embed/zCPiZlWdVws]

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Utilisation de la tête</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
     <tr>
        <td>Regard de œil</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).


## <a name="uses-of-gaze"></a>Utilisations des regards

Un développeur de réalité mixte, vous pouvez faire beaucoup avec regards head ou des yeux :
* Votre application peut se croisent regards avec les hologrammes dans votre scène pour déterminer où se trouve l’attention des utilisateurs.
* Votre application peut cibler des mouvements et appuie sur le contrôleur en fonction du pointage de regard de l’utilisateur, vous sélectionnez, activer, récupérer, faites défiler ou sinon interagir avec leurs hologrammes permettant de l’utilisateur.
* Votre application peut permettre à l’utilisateur de placer des hologrammes sur les surfaces du monde réel, par l’intersection de leur ray regards auprès de la maille de mappage spatial.
* Votre application peut savoir quand l’utilisateur est *pas* recherche dans la direction d’un objet important, ce qui peut conduire à votre application afin de donner des signaux visuels et audio pour activer vers cet objet.

## <a name="cursor"></a>Curseur

Pour des regards principal, la plupart des applications doivent utiliser un [curseur](cursors.md) (ou autre indication AUDITIVE/visual) à attribuer à la confiance des utilisateurs de ce que, ils sont sur le point d’interagir avec. En général, vous positionnez ce curseur dans le monde où leur ray regards principal tout d’abord entre en intersection avec un objet qui peut être un hologramme ou une surface du monde réel.

![Un exemple visuel du curseur pour afficher les regards](images/cursor.jpg)<br>
*Un exemple visuel du curseur pour afficher les regards*

Pour les regards yeux, nous recommandons généralement *pas* pour afficher un curseur, comme cela peut rapidement devenir parasites et agaçante de l’utilisateur. Au lieu de cela légèrement visual cibles de mettre en surbrillance ou un curseur yeux très faible pour assurent sur les nouveautés de l’utilisateur sur le point d’interagir avec. Pour plus d’informations, consultez notre [Guide de conception pour l’entrée basée sur les yeux](eye-tracking.md) sur HoloLens 2.

## <a name="giving-action-to-the-users-gaze"></a>Donnant action au regard de l’utilisateur

Une fois que l’utilisateur a ciblé un hologramme ou un objet réel à l’aide de leurs regards, leur étape suivante consiste à prendre des mesures sur cet objet. Les méthodes principales pour un utilisateur de prendre des mesures sont effectuent via [mouvements](gestures.md), [contrôleurs de mouvement](motion-controllers.md) et [voix](voice-input.md).

## <a name="see-also"></a>Voir aussi
* [Réalité mixte - Entrées - Cours 210 : Utilisation de la tête](holograms-210.md)
* [Suivre de la tête et du regard dans DirectX](gaze-in-directx.md)
* [Head regards dans Unity](gaze-in-unity.md)
* [OCULAIRE sur HoloLens 2](eye-tracking.md)
* [Surveillez les regards dans Unity à l’aide du Kit de ressources de réalité mixte](https://aka.ms/mrtk-eyes)
