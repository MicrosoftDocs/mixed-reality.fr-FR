---
title: Pointage du regard
description: Le point de présence est la première forme d’entrée et est une forme principale de ciblage au sein de la réalité mixte.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: Réalité mixte, point de regard, interaction, conception
ms.openlocfilehash: 7e65d26d3e9edabbd01d35a887ffc8622a3c6337
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414369"
---
# <a name="gaze"></a>Pointage du regard

Le point de **présence est la** première forme d’entrée et est une forme principale de ciblage au sein de la réalité mixte. Le point de regard indique où l’utilisateur regarde dans le monde et vous permet de déterminer son intention. Dans le monde réel, vous examinez généralement un objet avec lequel vous souhaitez interagir. C’est le même avec le point de regard.

Les casques de réalité mixte utilisent la position et l’orientation de la tête de l’utilisateur pour déterminer le vecteur de regard de son en-tête. Vous pouvez considérer ce vecteur comme un pointeur laser directement entre les yeux de l’utilisateur. À mesure que l’utilisateur regarde dans la pièce, votre application peut croiser ce rayon, à la fois avec ses propres hologrammes et avec le maillage de [mappage spatial](spatial-mapping.md) pour déterminer l’objet virtuel ou réel que votre utilisateur peut consulter.

Sur HoloLens 2, les interactions peuvent être ciblées par les intersections du point de regard de l’utilisateur, du regard ou des interactions près ou Far.
Sur HoloLens (1ère génération), les interactions doivent généralement dériver leur ciblage du point de vue de l’utilisateur, au lieu d’essayer d’effectuer un rendu ou une interaction directement à l’emplacement de la main. Une fois qu’une interaction a démarré, les mouvements relatifs de la main peuvent être utilisés pour contrôler le [mouvement](gestures.md), comme avec la [manipulation ou](gestures.md#composite-gestures) le mouvement de navigation. Avec les casques immersifs, vous pouvez cibler à l’aide de contrôleurs de [mouvement](motion-controllers.md)de pointage de tête ou de pointage.

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
        <td>Point de tête</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
     <tr>
        <td>Point de regard</td>
        <td>❌</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

> [!NOTE]
> Plus d’instructions spécifiques à HoloLens 2 bientôt [disponible](index.md#news-and-notes).


## <a name="uses-of-gaze"></a>Utilisations du point de regard

En tant que développeur de réalité mixte, vous pouvez faire beaucoup de regard en tête ou en œil:
* Votre application peut faire une intersection avec le regard des hologrammes dans votre scène pour déterminer où se trouve l’attention de l’utilisateur.
* Votre application peut cibler les gestes et les presses du contrôleur en fonction du point de regard de l’utilisateur, ce qui permet à l’utilisateur de sélectionner, d’activer, de saisir, de faire défiler ou d’interagir de manière interactive avec ses hologrammes.
* Votre application peut permettre à l’utilisateur de placer des hologrammes sur des surfaces réelles, en croisant leur rayon de regard avec le maillage de mappage spatial.
* Votre application peut savoir quand l’utilisateur *ne cherche pas* dans la direction d’un objet important, ce qui peut amener votre application à donner des signaux visuels et audio pour tourner vers cet objet.

## <a name="cursor"></a>Curseur

Pour le point de vue de la tête, la plupart des applications doivent utiliser un [curseur](cursors.md) (ou une autre indication d’audit/visuel) pour donner à l’utilisateur la certitude de ce qu’ils sont sur le point d’interagir. En règle générale, vous positionnez ce curseur dans le monde où le rayon de regard de son en-tête croise d’abord un objet, qui peut être un hologramme ou une surface réaliste.

![Exemple de curseur visuel pour afficher le regard](images/cursor.jpg)<br>
*Exemple de curseur visuel pour afficher le regard*

Pour les yeux oculaires, nous vous recommandons généralement de *ne pas* afficher de curseur, car cela peut rapidement devenir gênant et ennuyeux pour l’utilisateur. À la place, mettez en surbrillance les cibles visuelles ou utilisez un curseur très pâle pour faire confiance à ce que l’utilisateur est sur le point d’interagir. Pour plus d’informations, consultez notre [Guide de conception pour une entrée basée](eye-tracking.md) sur l’œil sur HoloLens 2.

## <a name="giving-action-to-the-users-gaze"></a>Donner une action au point de vue de l’utilisateur

Une fois que l’utilisateur a ciblé un hologramme ou un objet réel à l’aide de son regard, l’étape suivante consiste à agir sur cet objet. Les principales méthodes permettant à un utilisateur de prendre des mesures sont les [gestes](gestures.md), les contrôleurs de [mouvement](motion-controllers.md) et la [voix](voice-input.md).

## <a name="see-also"></a>Voir aussi
* [Réalité mixte - Entrées - Cours 210 : Point de tête](holograms-210.md)
* [Suivre de la tête et du regard dans DirectX](gaze-in-directx.md)
* [Point de regard de l’en-tête dans Unity](gaze-in-unity.md)
* [Eye-point de regard sur HoloLens 2](eye-tracking.md)
* [Point de regard sur Unity avec la réalité mixte Toolkit](https://aka.ms/mrtk-eyes)
