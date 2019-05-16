---
title: Pointage du regard
description: Regards est la première forme d’entrée et un principal de ciblage dans la réalité mixte.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: Réalité mixte, regards, Interaction, concevoir
ms.openlocfilehash: 738ba9063a5d00f3bbedce989d93076d56ad1a44
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629108"
---
# <a name="gaze"></a>Pointage du regard

**Utilisation** est la première forme d’entrée et un principal de ciblage dans la réalité mixte. Regards vous indique où l’utilisateur recherche dans le monde et vous permet de déterminer leur intention. Dans le monde réel, vous ferez généralement à un objet que vous avez l’intention d’interagir avec. Il s’agit même avec les regards.

Casques de réalité mixte utilisent la position et l’orientation de tête de l’utilisateur pour déterminer leur vecteur regards principal. Vous pouvez considérer ce vecteur comme un pointeur laser directement à l’avance de directement entre les yeux de l’utilisateur. Comme l’utilisateur semble autour de la pièce, votre application peut se croisent ce rayon, avec son propre hologrammes et avec le [mappage spatial](spatial-mapping.md) maille pour déterminer quel objet virtuel ou réelles de votre utilisateur peut regarder.

Sur HoloLens 2, interactions peuvent être ciblées par les regards principal soit l’utilisateur par le biais de près ou présent distribuer interactions.  Sur HoloLens (1er gen), les interactions doivent dériver généralement leur ciblage à partir des regards principal de l’utilisateur, au lieu d’essayer restituer ou interagir directement à l’emplacement de la part. Une fois démarrée, une interaction des mouvements relatifs de la main peuvent être utilisé pour contrôle le [mouvement](gestures.md), comme avec la [manipulation ou navigation](gestures.md#composite-gestures) mouvement. Avec des casques IMMERSIFS, vous pouvez cibler à l’aide soit du pointage de regard ou pointant compatibles [contrôleurs de mouvement](motion-controllers.md).

<br>

>[!VIDEO https://www.youtube.com/embed/zCPiZlWdVws]

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1er gen)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> Utilisation de la tête</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr><tr>
<td> Regard de œil</td><td></td><td style="text-align: center;">✔️</td><td></td>
</tr>
</table>

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).


## <a name="uses-of-gaze"></a>Utilisations des regards

Un développeur de réalité mixte, vous pouvez faire beaucoup avec pointage de regard :
* Votre application peut se croisent regards avec les hologrammes dans votre scène pour déterminer où se trouve l’attention des utilisateurs.
* Votre application peut cibler des mouvements et appuie sur le contrôleur en fonction du pointage de regard de l’utilisateur, vous sélectionnez, activer, récupérer, faites défiler ou sinon interagir avec leurs hologrammes permettant de l’utilisateur.
* Votre application peut permettre à l’utilisateur de placer des hologrammes sur les surfaces du monde réel, par l’intersection de leur ray regards auprès de la maille de mappage spatial.
* Votre application peut savoir quand l’utilisateur est *pas* recherche dans la direction d’un objet important, ce qui peut conduire à votre application afin de donner des signaux visuels et audio pour activer vers cet objet.

## <a name="cursor"></a>Curseur

La plupart des applications doivent utiliser un [curseur](cursors.md) (ou autre indication AUDITIVE/visual) à attribuer à la confiance des utilisateurs de ce que, ils sont sur le point d’interagir avec. En général, vous positionnez ce curseur dans le monde où leur ray regards interagit tout d’abord un objet qui peut être un hologramme ou une surface du monde réel.

![Un exemple visuel du curseur pour afficher les regards](images/cursor.jpg)<br>
*Un exemple visuel du curseur pour afficher les regards*

## <a name="giving-action-to-the-users-gaze"></a>Donnant action au regard de l’utilisateur

Une fois que l’utilisateur a ciblé un hologramme ou un objet réel à l’aide de leurs regards, leur étape suivante consiste à prendre des mesures sur cet objet. Les méthodes principales pour un utilisateur de prendre des mesures sont effectuent via [mouvements](gestures.md), [contrôleurs de mouvement](motion-controllers.md) et [voix](voice-input.md).

## <a name="see-also"></a>Voir aussi
* [Réalité mixte - Entrées - Cours 210 : Pointage du regard](holograms-210.md)
* [HEAD et surveillez les regards dans DirectX](gaze-in-directx.md)
* [Pointage du regard dans Unity](gaze-in-unity.md)
