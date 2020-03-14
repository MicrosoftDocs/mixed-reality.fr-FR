---
title: Typographie
description: Le texte est un élément important pour la diffusion d’informations dans votre expérience d’application.
author: cre8ivepark
ms.author: dongpark
ms.date: 06/03/2019
ms.topic: article
keywords: Windows Mixed Reality, conception, style, police, typographie, UI, UX
ms.openlocfilehash: 9664d355e941d800ac1ac862860fc5889b6b7686
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375796"
---
# <a name="typography"></a>Typographie

![Exemple de typographie dans HoloLens](images/typography-cover.png)<br>


Le texte est un élément important pour la diffusion d’informations dans votre expérience d’application. Tout comme la typographie sur les écrans 2D, l’objectif est d’être clair et lisible. Avec l’aspect tridimensionnel de la réalité mixte, il est possible d’affecter le texte et l’expérience utilisateur globale beaucoup mieux.

Lorsque nous parlerons du type en 3D, nous avons tendance à penser que le texte 3D est extrudé et jaugé. À l’exception de certaines conceptions logotype et de quelques autres applications limitées, le texte extrudé a tendance à dégrader la lisibilité du texte. Même si nous concevons des expériences en 3D, nous utilisons 2D pour le type, car il est plus lisible et plus facile à lire.

Dans HoloLens, le type est construit avec des hologrammes à l’aide de la lumière basée sur le système de couleurs additif. Tout comme les autres hologrammes, le type peut être placé dans l’environnement réel où il peut être verrouillé et observé à partir de n’importe quel angle. L’effet de [parallaxe](https://en.wikipedia.org/wiki/Parallax) entre le type et l’environnement ajoute également une profondeur à l’expérience.

## <a name="typography-in-mixed-reality"></a>Typographie dans une réalité mixte

Les règles typographiques en réalité mixte ne sont pas différentes de n’importe où ailleurs. Le texte à la fois dans le monde physique et dans le monde virtuel doit être lisible et lisible. Le texte peut être situé sur un mur ou superposé sur un objet physique. Il peut être flottant avec une interface utilisateur numérique. Quel que soit le contexte, nous appliquons les mêmes règles typographiques pour la lecture et la reconnaissance.

### <a name="create-clear-hierarchy"></a>Créer une hiérarchie claire

Générez le contraste et la hiérarchie en utilisant des tailles et des poids différents. Le fait de définir une rampe de type et de la suivre tout au long de l’expérience de l’application offre une expérience utilisateur exceptionnelle avec une hiérarchie d’informations cohérente.

exemples de rampe de type ![](images/typography-ramp-1000px.jpg)<br>
*Définir votre rampe de type et la suivre tout au long de l’expérience de l’application*

### <a name="limit-your-fonts"></a>Limiter vos polices

Évitez d’utiliser plus de deux familles de polices différentes dans un seul contexte. Cela rompt l’harmonie et la cohérence de votre expérience et complique la consommation d’informations. Dans HoloLens, étant donné que les informations sont superposées en plus de l’environnement physique, l’utilisation d’un trop grand nombre de styles de police dégradera l’expérience. Segoe UI est la police de toutes les conceptions numériques Microsoft. Il est utilisé de manière cohérente dans le shell Windows Mixed Reality. Vous pouvez télécharger le fichier de police Segoe UI à partir de la page de la [boîte à outils de conception Windows](https://docs.microsoft.com/windows/uwp/design-downloads/).

[Plus d’informations sur la police Segoe UI](https://docs.microsoft.com/windows/uwp/design/style/typography)

### <a name="avoid-thin-font-weights"></a>Évitez les poids des polices fines

Évitez d’utiliser des épaisseurs de police Light ou semilight pour les tailles de type sous est, car les traits verticaux fins vibreront et dégradent la lisibilité. Les polices modernes avec suffisamment d’épaisseur de trait fonctionnent bien. Par exemple, Helvetica et Arial sont très lisibles dans HoloLens en utilisant des pondérations standard ou en gras.

### <a name="color"></a>Couleur

Dans HoloLens, étant donné que les hologrammes sont construits avec un système d’éclairage additif, le texte blanc est très lisible. Vous trouverez des exemples de texte blanc dans le menu Démarrer et la barre des applications. Même si le texte blanc fonctionne bien sans une plaque arrière sur HoloLens, un arrière-plan physique complexe peut rendre le type difficile à lire. Pour améliorer le focus de l’utilisateur et réduire la distraction d’un arrière-plan physique, nous vous recommandons d’utiliser du texte blanc sur une plaque d’arrière-plan sombre ou colorée.

<br>


![nous vous recommandons d’utiliser du texte blanc sur une plaque d’arrière-plan foncée ou colorée.](images/typography-whiteonblack2-1000px.jpg)
*des exemples de texte blanc sur une plaque d’arrière-plan foncée ou colorée.*
<br>

Pour utiliser du texte foncé, vous devez utiliser une plaque de retour brillant pour la rendre lisible. Dans les systèmes de couleurs additives, le noir est affiché comme transparent. Cela signifie que vous ne pourrez pas voir le texte noir sans plaque arrière colorée.

:::row:::
    :::column:::
        ![des exemples de texte noir](images/typography-whiteonblack.png)<br>
        *Exemples de blanc sur noir et noir sur du texte blanc*<br>
    :::column-end:::
    :::column:::
        ![des exemples de texte noir](images/640px-typography-blackonwhite.jpg)<br>
        *Exemples de texte noir dans les applications système-magasin et paramètres*<br>
    :::column-end:::
:::row-end:::

<br>

---

## <a name="recommended-font-size"></a>Taille de police recommandée

Comme vous pouvez vous y attendre, les tailles de type que nous utilisons sur un PC ou un appareil tablette (généralement entre 12 et 32 points) semblent très petites à une distance de 2 mètres. Elle dépend des caractéristiques de chaque police, mais en général, l’angle de visualisation minimal recommandé et la hauteur de police pour la lisibilité sont autour de 0.35 °-0,4 °/12.21-13.97mm en fonction des études de recherche des utilisateurs. Elle est d’environ 35 40pt avec le facteur de mise à l’échelle introduit dans le [texte de la page Unity](text-in-unity.md) . 

Pour l’approche near interaction à 0.45 m (45cm), l’angle d’affichage de la police à la hauteur minimale et la hauteur sont de 0,4 °-0,5 °/3.14 – 3,9 mm. Elle est d’environ 9-12 PT avec le facteur de mise à l’échelle introduit dans le [texte de Unity](text-in-unity.md).

![plage d’interaction near et Far](images/typography-distance-1000px.jpg)
*contenu à une plage d’interaction proche et éloignée*

### <a name="the-minimum-legible-font-size"></a>Taille de police minimale lisible
| Distance | Angle d’affichage | Hauteur du texte | Taille de police * * |
|---------|---------|---------|---------|
| 45cm (distance de manipulation directe) | 0,4 °-0,5 ° | 3.14 – 3,9 mm | 8,9 – 11.13 PT |
| dollars | 0.35 °-0,4 ° | 12.21 – 13.97 mm | 34.63-39.58 PT |


### <a name="the-comfortably-legible-font-size"></a>Taille de police lisible
| Distance | Angle d’affichage | Hauteur du texte | Taille de police * * |
|---------|---------|---------|---------|
| 45cm (distance de manipulation directe) | 0,65 °-0,8 ° | 5.1-6.3 mm | 14.47-17.8 PT |
| dollars | 0,6 °-0,75 ° | 20.9-26.2 mm | 59.4-74.2 PT |


Segoe UI (police par défaut pour Windows) fonctionne bien dans la plupart des cas. Toutefois, évitez d’utiliser des familles de polices légères ou semi-claires en petite taille, car les traits verticaux fins vibreront et la lisibilité sera dégradée. Les polices modernes avec suffisamment d’épaisseur de trait fonctionnent bien. Par exemple, Helvetica et Arial semblent exceptionnels et sont très lisibles dans HoloLens avec des pondérations standard ou en gras.

**Pour plus d’informations sur le calcul de la taille du texte dans Unity, consultez le [texte dans Unity](text-in-unity.md)**

![angle de visualisation](images/Text_In_Unity_ViewingAngle.jpg)
*distance d’affichage, angle et hauteur du texte*

<br>

---

## <a name="resources"></a>Ressources

:::row:::
    :::column:::
    ### <a name="segoe-fontsbr"></a>[Polices Segoe](https://download.microsoft.com/download/1/B/C/1BCF071A-78EE-4968-ACBE-15461C274B61/Segoe%20fonts%20v1705.zip)<br>
    (Fichier zip)<br>
    ### <a name="hololens-fontbr"></a>[Police HoloLens](https://download.microsoft.com/download/3/8/D/38D659E2-4B9C-413A-B2E7-1956181DC427/Hololens%20font.zip)<br>
    (Fichier zip)<br>
    <br>
    *Image : la police HoloLens vous donne les glyphes de symboles utilisés dans Windows Mixed Reality.*
    :::column-end:::
        :::column:::
        ![La police HoloLens vous donne les glyphes de symboles utilisés dans Windows Mixed Reality](images/hololensmdl2symbols.jpg)<br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="see-also"></a>Voir aussi
* [Texte dans Unity](text-in-unity.md)
* [Couleurs, éclairage et matériaux](color,-light-and-materials.md)
