---
title: Tableau périodique des éléments
description: Tableau périodique des éléments est un exemple de l’open source d’application à partir mixte réalité conception Labs de Microsoft, où vous pouvez apprendre à disposer d’un tableau d’objets dans l’espace 3D avec différents types de surface à l’aide d’une collection d’objets.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, exemple d’application, contrôles
ms.openlocfilehash: ad95d2bcfd1b70d805adcceb36be0c6c29b838f0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596694"
---
# <a name="periodic-table-of-the-elements"></a>Tableau périodique des éléments

>[!NOTE]
>Cet article présente un exemple exploratoire, nous avons créé dans le [laboratoires de conception de réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity), un emplacement où nous partageons nos connaissances acquises sur et des suggestions pour développement d’applications de réalité mixte. Nos articles relatifs à la conception et le code évoluera lors de nos nouvelles découvertes.

[Tableau périodique des éléments](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable) est un exemple de l’open source d’application à partir de laboratoires de conception réalité mixte de Microsoft. Avec ce projet, vous pouvez apprendre à disposer d’un tableau d’objets dans l’espace 3D avec différents types de surface à l’aide un  **[collection d’objets](object-collection.md)**. Découvrez également comment créer des objets sur qui répondent aux entrées standards à partir de HoloLens. Vous pouvez utiliser les composants de ce projet pour créer vos propres mixte d’expérience d’application de réalité.

![Table des périodes de l’application d’éléments](images/640px-periodictable-hero.jpg)

## <a name="about-the-app"></a>À propos de l’application

Tableau périodique des éléments permet de visualiser les éléments sur les produits chimiques et chacune de leurs propriétés dans un espace 3D. Il intègre les interactions de base de HoloLens tels que des regards et air tap. Les utilisateurs peuvent en savoir plus sur les éléments avec des modèles 3D animés. Ils comprennent visuellement interpréteur de commandes d’un élément d’électrons et son noyau - composé de protons et neutrons.

## <a name="background"></a>Arrière-plan

Une fois que j’ai rencontré tout d’abord HoloLens, une application de tableau périodique était une idée, que je savais que je souhaitais faire des essais avec en réalité mixte. Étant donné que chaque élément a plusieurs points de données qui sont affichées en texte, j’ai pensé qu’il serait très sujet pour l’exploration de composition typographique dans un espace 3D. La possibilité de visualiser le modèle de l’élément d’électrons était une autre partie intéressante de ce projet.

## <a name="design"></a>Concevoir

Pour l’affichage par défaut de la table périodique, j’ai imaginé boîtes à trois dimensions qui contient le modèle d’électrons de chaque élément. La surface de chaque zone serait translucide afin que l’utilisateur peut obtenir une idée approximative du volume de l’élément. Un appui sur regards et air, l’utilisateur peut ouvrir une vue détaillée de chaque élément. Pour rendre la transition entre la vue de table et affichage des détails sans heurts et naturelle, je me suis semblable à l’interaction physique d’une zone d’ouverture dans la vie réelle.

![Ébauche de projet de conception](images/640px-sketch20170406.jpg)<br>
*Conception des croquis*

Dans la vue de détail, je voulais visualiser les informations de chaque élément avec le texte rendu impeccable et dans l’espace 3D. Le modèle d’électrons 3D animés s’affiche dans la zone centrale et sont consultables sous différents angles.

![Interaction](images/640px-periodictable-interaction.jpg)

![Prototypes](images/640px-periodictable-prototypes.jpg)<br>
*Prototypes d’interaction*

L’utilisateur peut modifier le type de surface par voie aérienne en appuyant sur les boutons en bas de la table, ils peuvent basculer entre un plan, cylindre, sphère et à nuages de points.

## <a name="common-controls-and-patterns-used-in-this-app"></a>Contrôles et modèles utilisés dans cette application courants

### <a name="interactable-object-button"></a>Objet sur (bouton)

[Objet sur](interactable-object.md) est un objet qui peut répondre aux entrées de base HoloLens. Il est fourni en tant que préfabriqué/script que vous pouvez facilement appliquer à n’importe quel objet. Par exemple, vous pouvez rendre une tasse de café dans votre scène sur et répondre aux entrées telles que des regards, appui, les mouvements de navigation et de manipulation. [En savoir plus](interactable-object.md)

![objet de nteractable](images/640px-periodictable-interactableobject.jpg)

### <a name="object-collection"></a>Collection d’objets

[Collection d’objets](object-collection.md) est un objet qui permet de disposer de plusieurs objets dans différentes formes. Il prend en charge le plan, cylindre, sphère et à nuages de points. Vous pouvez configurer des propriétés supplémentaires telles que le rayon, le nombre de lignes et l’espacement. [En savoir plus](object-collection.md)

![Collection d’objets](images/640px-periodictable-collections.jpg)

### <a name="fitbox"></a>Fitbox

Par défaut, hologrammes seront placés dans l’emplacement où l’utilisateur est gazing au moment où l’application est lancée. Cela entraîne parfois des résultats indésirables tels que hologrammes placées derrière un mur ou au milieu d’une table. Un fitbox permet à un utilisateur à utiliser des regards pour déterminer l’emplacement où l’hologramme sera placé. Il est effectué avec une texture d’image PNG simple qui peut être personnalisée facilement avec vos propres images ou des objets 3D.

![Fitbox](images/450px-periodictable-fitbox.jpg)

## <a name="technical-details"></a>Détails techniques

Vous pouvez trouver des scripts et prefabs pour la Table périodique de l’application d’éléments sur le [GitHub de laboratoires de conception réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable).

## <a name="application-examples"></a>Exemples d’applications

Voici quelques idées pour ce que vous pouvez créer en exploitant les composants dans ce projet.

### <a name="stock-data-visualization-app"></a>Application de visualisation des données boursières

Que la Table périodique de l’exemple d’éléments, utilisez les mêmes contrôles et le modèle d’interaction, vous pouvez générer une application qui visualise les données boursières. Cet exemple utilise le contrôle de collection d’objets pour présenter les données de stock dans une forme sphérique. Vous pouvez l’imaginer une vue de détail où des informations supplémentaires sur chaque action pouvant être affichées dans une façon intéressante.

![Exemple d’application : Finance (1 sur 3)](images/640px-periodictable-applicationexamples-finance1.jpg)

![Exemple d’application : Finance (2 sur 3)](images/640px-periodictable-applicationexamples-finance2.jpg)

![Exemple d’application : Finance (3 sur 3)](images/640px-periodictable-applicationexamples-finance3.jpg)<br>
*Un exemple d’utilisation de la collection d’objets utilisée dans la Table périodique de l’exemple d’application éléments peut être dans une application de finance*

### <a name="sports-app"></a>Application de sport

Il s’agit d’un exemple de visualisation des données de sports à l’aide de la collection d’objets et d’autres composants de la Table périodique de l’exemple d’application éléments.

![Exemple d’application : Sports (1 sur 3)](images/640px-periodictable-applicationexamples-sports0.jpg)

![Exemple d’application : Sports (2 sur 3)](images/640px-periodictable-applicationexamples-sports1.jpg)

![Exemple d’application : Sports (3 sur 3)](images/640px-periodictable-applicationexamples-sports3.jpg)<br>
*Un exemple d’utilisation de la collection d’objets dans la Table périodique de l’appcould exemple éléments être utilisé dans une application de sports*

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><b>Dong Yoon Park</b><br>Concepteur UX @Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi

* [Objet sur](interactable-object.md)
* [Collection d’objets](object-collection.md)
