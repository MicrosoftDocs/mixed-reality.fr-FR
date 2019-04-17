---
title: Typographie
description: Le texte est un élément important pour fournir des informations dans votre expérience d’application.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, style, de police, typographie, l’interface utilisateur, l’expérience utilisateur
ms.openlocfilehash: b4bac35cbc412ec7102748350c2f5c1e236c2f7d
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596046"
---
# <a name="typography"></a>Typographie

Le texte est un élément important pour fournir des informations dans votre expérience d’application. Tout comme la typographie sur les écrans 2D, vise à être clairs et lisible. Avec l’aspect en trois dimensions de réalité mixte, il existe une opportunité pour affecter le texte et l’utilisateur globale expérience de manière encore plus grande.

![Exemple de typographie dans HoloLens](images/640px-typography-hero2.jpg)<br>
*Exemple de typographie dans HoloLens*

Lorsque nous parlons de type en 3D, nous avons tendance à considérer extrudé, volumétrique texte 3D. À l’exception de certaines conceptions logotype et quelques autres applications limitées, texte extrudé a tendance à se dégrader la lisibilité du texte. Bien que nous allons concevoir des expériences pour 3D, nous utilisons 2D pour le type, car il est plus lisible et plus facile à lire.

Dans HoloLens, type est construit avec hologrammes à l’aide de la lumière basée sur le système de couleur additive. À l’instar des autres hologrammes, type peut être placé dans l’environnement réel où elle peut être world verrouillé et observé à partir de n’importe quel angle. Le [parallaxe](https://en.wikipedia.org/wiki/Parallax) effet entre le type et l’environnement ajoute également la profondeur à l’expérience.

## <a name="typography-in-mixed-reality"></a>Typographie dans la réalité mixte

Règles typographiques en réalité mixte diffèrent pas nulle part ailleurs. Le texte dans le monde physique et le monde virtuel doit être lisible et accessible en lecture. Texte peut se trouver sur un mur ou superposé à un objet physique. Il peut en virgule flottante, ainsi que d’une interface utilisateur numérique. Quel que soit le contexte, nous appliquons les mêmes règles typographiques pour la lecture et de reconnaissance.

### <a name="create-clear-hierarchy"></a>Créer une hiérarchie claire

Générer le contraste et la hiérarchie à l’aide de poids et tailles de type différent. Définition d’une rampe de type ou le suivant dans l’ensemble de l’expérience de l’application fournit une expérience utilisateur satisfaisante avec la hiérarchie de la cohérence des informations.

![Exemples de types de démarrage](images/typography-ramp-1000px.jpg)<br>
*Exemples de types de démarrage*

### <a name="limit-your-fonts"></a>Limiter vos polices

Évitez d’utiliser plus de deux familles de polices différentes dans un contexte unique. Cela rompre l’harmonie et la cohérence de votre expérience et rendre plus difficile d’utiliser les informations. Dans HoloLens, étant donné que les informations sont superposées à l’environnement physique, à l’aide de styles de police trop réduit l’expérience. Segoe UI est la police pour toutes les conceptions numériques Microsoft. Il est utilisé de manière cohérente dans l’interpréteur de commandes Windows Mixed Reality. Vous pouvez télécharger le fichier de police Segoe UI à partir de la [page de boîte à outils de conception de Windows](https://docs.microsoft.com/windows/uwp/design-downloads/).

[Plus d’informations sur la police Segoe UI](https://docs.microsoft.com/windows/uwp/design/style/typography)

### <a name="avoid-thin-font-weights"></a>Éviter les poids de la police fine

Évitez d’utiliser le poids de police claire ou semilight pour les tailles de type sous 42pt dans la mesure où les traits verticaux minces seront vibration et dégrader une meilleure lisibilité. Polices modernes avec suffisamment épaisseur du trait fonctionnent bien. Par exemple, Helvetica et Arial sont très lisible en HoloLens à l’aide de pondérations réguliers ou en gras.

### <a name="color"></a>Color

Dans HoloLens, étant donné que les hologrammes sont construits avec un système de lumière additif, texte blanc est hautement lisible. Vous trouverez des exemples de texte blanc sur le menu Démarrer et la barre des applications. Même si le texte blanc fonctionne correctement sans une plaque arrière sur HoloLens, un arrière-plan physique complex peut rendre le type difficile à lire. Pour améliorer le focus de l’utilisateur et réduire l’encombrement physique univers, nous vous recommandons d’à l’aide du texte blanc sur une plaque sombre ou retour colorée.

<br>


![Nous recommandons à l’aide du texte blanc sur une plaque arrière sombre ou en couleur.](images/typography-whiteonblack2-1000px.jpg)

Nous recommandons à l’aide du texte blanc sur une plaque arrière sombre ou en couleur.

<br>


![Exemples de texte noir](images/640px-typography-textcolors.jpg)

Pour utiliser le texte foncé, vous devez utiliser une plaque arrière brillant pour le rendre accessible en lecture. Dans les systèmes de couleurs additives, noir est affiché comme transparente. Cela signifie que vous ne serez pas en mesure de voir le texte sans une couleur noir plaque de sauvegarde.

<br>


![Exemples de texte noir](images/640px-typography-blackonwhite.jpg)

Vous trouverez des exemples de texte en noir dans les applications UWP tels que le Store ou les paramètres.

## <a name="recommended-font-size"></a>Taille de police recommandée

![Deux compteurs est la distance optimale pour l’affichage de texte.](images/typography-distance-1000px.jpg)

Deux compteurs est la distance optimale pour l’affichage de texte.

Étant donné que la réalité mixte implique la profondeur en trois dimensions, il n’est pas toujours facile de communiquer la taille de la police. Pour plus de confort de l’utilisateur, deux compteurs est la distance optimale pour placer hologrammes. Nous pouvons utiliser cette distance comme base pour rechercher la taille de police optimal.

Comme vous pouvez l’imaginer, les tailles de type que nous utilisons sur un PC ou une tablette (en général entre 12 – 32 points) Examinez relativement petites une distance de 2 mètres. Il dépend des caractéristiques de chaque police, mais en général, la taille minimale recommandée pour une meilleure lisibilité sans vibration de trait est environ 30pt. Si votre application est censée être utilisée à distance plus proche, plus petites tailles de type peut être utilisés. **La taille du point repose sur le maillage de texte 3D d’Unity et le texte de l’interface utilisateur. Pour les métriques détaillées et les facteurs d’échelle, reportez-vous à [texte dans Unity](text-in-unity.md).**

## <a name="resources"></a>Ressources
* [Polices Segoe](http://download.microsoft.com/download/1/B/C/1BCF071A-78EE-4968-ACBE-15461C274B61/Segoe%20fonts%20v1705.zip)
* [Police de HoloLens](http://download.microsoft.com/download/3/8/D/38D659E2-4B9C-413A-B2E7-1956181DC427/Hololens%20font.zip)

![La police HoloLens vous donne les glyphes de symbole utilisés dans Windows Mixed Reality](images/300px-hololensmdl2symbols.jpg)

La police HoloLens vous donne les glyphes de symbole utilisés dans la réalité mixte de Windows.

## <a name="see-also"></a>Voir aussi
* [Texte dans Unity](http://holodocsfuture/index.php?title=Text_in_Unity&action=edit&redlink=1)
* [Couleur, clair et supports](color,-light-and-materials.md)
