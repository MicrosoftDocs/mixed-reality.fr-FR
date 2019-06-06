---
title: Typographie
description: Le texte est un élément important pour fournir des informations dans votre expérience d’application.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, style, de police, typographie, l’interface utilisateur, l’expérience utilisateur
ms.openlocfilehash: debf125a7f82ac79fe3ad776ba9c8c0b69396848
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66692371"
---
# <a name="typography"></a>Typographie

Le texte est un élément important pour fournir des informations dans votre expérience d’application. Tout comme la typographie sur les écrans 2D, vise à être clairs et lisible. Avec l’aspect en trois dimensions de réalité mixte, il existe une opportunité pour affecter le texte et l’utilisateur globale expérience de manière encore plus grande.

![Exemple de typographie dans HoloLens](images/typography-cover.png)<br>
*Exemple de typographie dans HoloLens*

Lorsque nous parlons de type en 3D, nous avons tendance à considérer extrudé, volumétrique texte 3D. À l’exception de certaines conceptions logotype et quelques autres applications limitées, texte extrudé a tendance à se dégrader la lisibilité du texte. Bien que nous allons concevoir des expériences pour 3D, nous utilisons 2D pour le type, car il est plus lisible et plus facile à lire.

Dans HoloLens, type est construit avec hologrammes à l’aide de la lumière basée sur le système de couleur additive. À l’instar des autres hologrammes, type peut être placé dans l’environnement réel où elle peut être world verrouillé et observé à partir de n’importe quel angle. Le [parallaxe](https://en.wikipedia.org/wiki/Parallax) effet entre le type et l’environnement ajoute également la profondeur à l’expérience.

## <a name="typography-in-mixed-reality"></a>Typographie dans la réalité mixte

Règles typographiques en réalité mixte diffèrent pas nulle part ailleurs. Le texte dans le monde physique et le monde virtuel doit être lisible et accessible en lecture. Texte peut se trouver sur un mur ou superposé à un objet physique. Il peut en virgule flottante, ainsi que d’une interface utilisateur numérique. Quel que soit le contexte, nous appliquons les mêmes règles typographiques pour la lecture et de reconnaissance.

### <a name="create-clear-hierarchy"></a>Créer une hiérarchie claire

Générer le contraste et la hiérarchie à l’aide de poids et tailles de type différent. Définition d’une rampe de type ou le suivant dans l’ensemble de l’expérience de l’application fournit une expérience utilisateur satisfaisante avec la hiérarchie de la cohérence des informations.

![Exemples de types de démarrage](images/typography-ramp-1000px.jpg)<br>
*Définir votre rampe de type et de suivre tout au long de l’expérience d’application*

### <a name="limit-your-fonts"></a>Limiter vos polices

Évitez d’utiliser plus de deux familles de polices différentes dans un contexte unique. Cela rompre l’harmonie et la cohérence de votre expérience et rendre plus difficile d’utiliser les informations. Dans HoloLens, étant donné que les informations sont superposées à l’environnement physique, à l’aide de styles de police trop réduit l’expérience. Segoe UI est la police pour toutes les conceptions numériques Microsoft. Il est utilisé de manière cohérente dans l’interpréteur de commandes Windows Mixed Reality. Vous pouvez télécharger le fichier de police Segoe UI à partir de la [page de boîte à outils de conception de Windows](https://docs.microsoft.com/windows/uwp/design-downloads/).

[Plus d’informations sur la police Segoe UI](https://docs.microsoft.com/windows/uwp/design/style/typography)

### <a name="avoid-thin-font-weights"></a>Éviter les poids de la police fine

Évitez d’utiliser le poids de police claire ou semilight pour les tailles de type sous 42pt dans la mesure où les traits verticaux minces seront vibration et dégrader une meilleure lisibilité. Polices modernes avec suffisamment épaisseur du trait fonctionnent bien. Par exemple, Helvetica et Arial sont très lisible en HoloLens à l’aide de pondérations réguliers ou en gras.

### <a name="color"></a>Color

Dans HoloLens, étant donné que les hologrammes sont construits avec un système de lumière additif, texte blanc est hautement lisible. Vous trouverez des exemples de texte blanc sur le menu Démarrer et la barre des applications. Même si le texte blanc fonctionne correctement sans une plaque arrière sur HoloLens, un arrière-plan physique complex peut rendre le type difficile à lire. Pour améliorer le focus de l’utilisateur et réduire l’encombrement physique univers, nous vous recommandons d’à l’aide du texte blanc sur une plaque sombre ou retour colorée.

<br>


![Nous recommandons à l’aide du texte blanc sur une plaque arrière sombre ou en couleur. ](images/typography-whiteonblack2-1000px.jpg)
 *Exemples de texte blanc sur une plaque arrière sombre ou en couleur.*
<br>

Pour utiliser le texte foncé, vous devez utiliser une plaque arrière brillant pour le rendre accessible en lecture. Dans les systèmes de couleurs additives, noir est affiché comme transparente. Cela signifie que vous ne serez pas en mesure de voir le texte sans une couleur noir plaque de sauvegarde.

![Exemples de texte noir](images/typography-whiteonblack.png)
<br>*Exemples de blanc DOS et noir sur blanc texte*


![Exemples de texte noir](images/640px-typography-blackonwhite.jpg)
<br>*Exemples de texte en noir dans les applications système - Store et les paramètres*

## <a name="recommended-font-size"></a>Taille de police recommandée

Comme vous pouvez l’imaginer, les tailles de type que nous utilisons sur un PC ou une tablette (en général entre 12 – 32 points) Examinez relativement petites une distance de 2 mètres. Il dépend des caractéristiques de chaque police, mais en général le minimum recommandé affichage angle et la hauteur de police pour une meilleure lisibilité concernent 0.35°-0.4°/12.21-13.97mm selon nos études de recherche utilisateur. Il s’agit 35-40pt avec le facteur d’échelle présentée ci-dessus. 

Pour l’interaction proche à 0.45m(45cm), angle de visualisation de la police lisibles minimale et la hauteur sont 0,4 °-0,5 ° / 3.14 – 3.9 mm. Il s’agit 9-12 pt avec le facteur d’échelle présentée ci-dessus.

![NEAR et far plage d’interaction](images/typography-distance-1000px.jpg)
*plage de contenu à proximité et lointain interaction*

### <a name="the-minimum-legible-font-size"></a>La taille de police lisibles minimale
| Distance | Angle de visualisation | Hauteur du texte | Taille de police ** |
|---------|---------|---------|---------|
| 45 centimètres (distance manipulation directe) | 0.4°-0.5° | 3.14 – 3.9 mm | 8.9 – 11.13pt |
| 2m | 0.35°-0.4° | 12.21 – 13.97 mm | 34.63-39.58pt |


### <a name="the-comfortably-legible-font-size"></a>La taille de police confortablement lisibles
| Distance | Angle de visualisation | Hauteur du texte | Taille de police ** |
|---------|---------|---------|---------|
| 45 centimètres (distance manipulation directe) | 0.65°-0.8° | 5.1-6.3 mm | 14.47-17.8pt |
| 2m | 0.6°-0.75° | 20,9-26,2 mm | 59.4-74.2pt |


Segoe UI (la police par défaut pour Windows) fonctionne bien dans la plupart des cas. Toutefois, évitez d’utiliser les familles de polices clair light ou semi de petite taille dans la mesure où les traits verticaux minces seront vibration et cela dégradera la lisibilité. Polices modernes avec suffisamment épaisseur du trait fonctionnent bien. Par exemple, Helvetica et Arial rechercher exceptionnelles et sont très lisible en HoloLens avec des poids réguliers ou en gras.

** Pour plus d’informations sur le calcul de taille de texte dans Unity, reportez-vous à la page [texte dans Unity](text-in-unity.md)

![Angle d’affichage](images/Text_In_Unity_ViewingAngle.jpg)
*affichage hauteur distance et angle de texte*

## <a name="resources"></a>Ressources
* [Polices Segoe](http://download.microsoft.com/download/1/B/C/1BCF071A-78EE-4968-ACBE-15461C274B61/Segoe%20fonts%20v1705.zip)
* [Police de HoloLens](http://download.microsoft.com/download/3/8/D/38D659E2-4B9C-413A-B2E7-1956181DC427/Hololens%20font.zip)

![La police HoloLens vous donne les glyphes de symbole utilisés dans Windows Mixed Reality](images/300px-hololensmdl2symbols.jpg)
<br>*La police HoloLens vous donne les glyphes de symbole utilisés dans la réalité mixte de Windows.*

## <a name="see-also"></a>Voir aussi
* [Texte dans Unity](text-in-unity.md)
* [Couleurs, éclairage et matériaux](color,-light-and-materials.md)
