---
title: Tableau périodique des éléments
description: La table périodique des éléments est un exemple d’application open source des laboratoires de conception de la réalité mixte de Microsoft, où vous pouvez apprendre à disposer un tableau d’objets dans l’espace 3D avec différents types de surface à l’aide d’une collection d’objets.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, exemple d’application, contrôles
ms.openlocfilehash: ad95d2bcfd1b70d805adcceb36be0c6c29b838f0
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63525367"
---
# <a name="periodic-table-of-the-elements"></a>Tableau périodique des éléments

>[!NOTE]
>Cet article présente un exemple exploratoire que nous avons créé dans les [laboratoires de conception de réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity), un endroit où nous partageons nos connaissances et des suggestions concernant le développement d’applications de réalité mixte. Nos articles et code liés à la conception évoluent à mesure que nous effectuons de nouvelles découvertes.

[La table périodique des éléments](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable) est un exemple d’application open source des laboratoires de conception de la réalité mixte de Microsoft. Avec ce projet, vous pouvez apprendre à disposer un tableau d’objets dans l’espace 3D avec différents types de surface à l’aide d’une **[collection d’objets](object-collection.md)** . Découvrez également comment créer des objets interactifs qui répondent aux entrées standard de HoloLens. Vous pouvez utiliser les composants de ce projet pour créer votre propre expérience d’application de réalité mixte.

![Table period de l’application Elements](images/640px-periodictable-hero.jpg)

## <a name="about-the-app"></a>À propos de l’application

La table périodique des éléments visualise les éléments chimiques et chacune de leurs propriétés dans un espace 3D. Il intègre les interactions de base de HoloLens, telles que le toucher et l’air. Les utilisateurs peuvent en savoir plus sur les éléments avec des modèles 3D animés. Ils peuvent comprendre visuellement le shell électron d’un élément et son noyau, qui est composé de protons et de neutrons.

## <a name="background"></a>Présentation

Une fois que j’ai expérimenté le langage HoloLens, une application de table périodique était une idée que je souhaitais expérimenter en réalité mixte. Étant donné que chaque élément a de nombreux points de données qui s’affichent avec du texte, j’ai pensé qu’il serait intéressant d’explorer la composition typographique dans un espace 3D. La possibilité de visualiser le modèle d’électrons de l’élément était une autre partie intéressante de ce projet.

## <a name="design"></a>Concevoir

Pour la vue par défaut de la table périodique, j’ai imaginé des cases tridimensionnelles qui contiennent le modèle d’électrons de chaque élément. La surface de chaque zone est translucide afin que l’utilisateur puisse obtenir une idée approximative du volume de l’élément. Lorsque vous appuyez sur le regard et l’air, l’utilisateur peut ouvrir une vue détaillée de chaque élément. Pour effectuer la transition entre la vue de table et l’affichage détaillé en douceur et en naturel, j’ai fait de la même façon que l’interaction physique d’une ouverture de Box dans la vie réelle.

![Concevoir l’esquisse](images/640px-sketch20170406.jpg)<br>
*Concevoir des croquis*

En mode Détails, je voulais visualiser les informations de chaque élément avec un rendu impeccable du texte dans l’espace 3D. Le modèle d’électrons 3D animé est affiché dans la zone centrale et peut être affiché à partir de différents angles.

![Interaction](images/640px-periodictable-interaction.jpg)

![Prototypes](images/640px-periodictable-prototypes.jpg)<br>
*Prototypes d’interaction*

L’utilisateur peut modifier le type de surface par air en appuyant sur les boutons situés en bas du tableau: il peut basculer entre le plan, le cylindre, la sphère et le nuage de points.

## <a name="common-controls-and-patterns-used-in-this-app"></a>Contrôles et modèles communs utilisés dans cette application

### <a name="interactable-object-button"></a>Objet interagiable (bouton)

L’objet pouvant être [interagi](interactable-object.md) est un objet qui peut répondre aux entrées HoloLens de base. Il est fourni en tant que Prefab/script que vous pouvez facilement appliquer à n’importe quel objet. Par exemple, vous pouvez faire en sorte qu’une tasse de café dans votre scène puisse être manipulée et répondre à des entrées telles que le pointage, le toucher en air, les mouvements de navigation et de manipulation. [En savoir plus](interactable-object.md)

![objet nteractable](images/640px-periodictable-interactableobject.jpg)

### <a name="object-collection"></a>Collection d’objets

La [collection d’objets](object-collection.md) est un objet qui vous permet de disposer plusieurs objets dans différentes formes. Il prend en charge les plans, les cylindres, les sphères et les nuages de points. Vous pouvez configurer des propriétés supplémentaires telles que le rayon, le nombre de lignes et l’espacement. [En savoir plus](object-collection.md)

![Collection d’objets](images/640px-periodictable-collections.jpg)

### <a name="fitbox"></a>Fitbox

Par défaut, les hologrammes sont placés à l’emplacement où l’utilisateur est Gazing au moment où l’application est lancée. Cela entraîne parfois des résultats indésirables, tels que des hologrammes placés derrière un mur ou au milieu d’une table. Un fitbox permet à un utilisateur d’utiliser du regard pour déterminer l’emplacement où l’hologramme sera placé. Il est créé avec une texture d’image PNG simple qui peut être facilement personnalisée avec vos propres images ou objets 3D.

![Fitbox](images/450px-periodictable-fitbox.jpg)

## <a name="technical-details"></a>Détails techniques

Vous trouverez scripts and prefabs pour la table Periodic de l’application Elements sur le GitHub de conception de la [réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable).

## <a name="application-examples"></a>Exemples d’applications

Voici quelques idées de ce que vous pouvez créer en tirant parti des composants de ce projet.

### <a name="stock-data-visualization-app"></a>Application de visualisation des données boursières

En utilisant les mêmes contrôles et le même modèle d’interaction que la table périodique de l’exemple d’éléments, vous pouvez créer une application qui visualise les données boursières. Cet exemple utilise le contrôle de collection d’objets pour présenter les données boursières dans une forme sphérique. Vous pouvez imaginer un affichage détaillé où des informations supplémentaires sur chaque stock peuvent être affichées d’une manière intéressante.

![Exemple d’application: Finance (1 sur 3)](images/640px-periodictable-applicationexamples-finance1.jpg)

![Exemple d’application: Finance (2 sur 3)](images/640px-periodictable-applicationexamples-finance2.jpg)

![Exemple d’application: Finance (3 sur 3)](images/640px-periodictable-applicationexamples-finance3.jpg)<br>
*Exemple de la façon dont la collection d’objets utilisée dans la table périodique de l’exemple d’application Elements peut être utilisée dans une application finance*

### <a name="sports-app"></a>Application sportive

Voici un exemple de visualisation de données sportives à l’aide de la collection d’objets et d’autres composants de la table périodique de l’exemple d’application d’éléments.

![Exemple d’application: Sports (1 sur 3)](images/640px-periodictable-applicationexamples-sports0.jpg)

![Exemple d’application: Sports (2 sur 3)](images/640px-periodictable-applicationexamples-sports1.jpg)

![Exemple d’application: Sports (3 sur 3)](images/640px-periodictable-applicationexamples-sports3.jpg)<br>
*Exemple de la façon dont la collection d’objets utilisée dans la table périodique de l’exemple d’éléments appcould doit être utilisée dans une application sportive*

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><b>Dong Yoon Park</b><br>Concepteur UX@Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi

* [Objet avec interaction possible](interactable-object.md)
* [Collection d’objets](object-collection.md)
