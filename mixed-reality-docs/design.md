---
layout: LandingPage
title: Commencer à concevoir et à créer des prototypes
description: Si vous êtes prêt à vous lancer, découvrez les concepts de base dont vous avez besoin pour commencer à concevoir et à créer des prototypes.
author: grbury
ms.author: grbury
ms.date: 08/24/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, découvrir, distribuer, index, page d’accueil, conception, développement, tutoriels, exemples d’applications, principes fondamentaux, études de cas, ressources, procédures HoloLens, projets open source, concepts principaux, interaction
ms.openlocfilehash: 708a6f83c2de149be9c221130b83f5d787f8f56a
ms.sourcegitcommit: 8daefb763d1f23fe02b95b766b00b373f04c5c2d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86447915"
---
# <a name="start-designing-and-prototyping"></a>Commencer à concevoir et à créer des prototypes


![résumé de la conception en réalité mixte](images/03_Design.png)

## <a name="expand-your-design-process"></a>[Développer votre processus de conception](case-study-expanding-the-design-process-for-mixed-reality.md)

Quand Microsoft a lancé l’appareil HoloLens auprès d’un public de développeurs enthousiastes en 2016, l’équipe s’était déjà associée à des studios à l’intérieur et à l’extérieur de Microsoft pour créer les expériences de lancement de l’appareil. Ces équipes ont appris sur le tas, trouvant des opportunités et des défis dans le nouveau domaine de la conception de réalité mixte. [En savoir plus](case-study-expanding-the-design-process-for-mixed-reality.md)

<br>

---

## <a name="what-are-the-core-concepts-of-an-experience"></a>Quels sont les principaux concepts d’une expérience ?

### <a name="keep-the-user-comfortable---comfort"></a>[Faire en sorte que l’utilisateur soit toujours à l’aise : confort](comfort.md)
Pour garantir un confort maximal sur les afficheurs placés sur la tête, il est important que les concepteurs et les développeurs créent du contenu et le présentent d’une manière qui imite le fonctionnement de ces indicateurs dans le monde naturel.

<br>

### <a name="consider-how-the-user-sees-the-world---holographic-frame"></a>[Réfléchir à la façon dont l’utilisateur voit le monde : image holographique](holographic-frame.md)
Les utilisateurs voient le monde de la réalité mixte par le biais d’une fenêtre d’affichage rectangulaire alimentée par leur casque. Sur l’appareil HoloLens, cette zone rectangulaire est appelée « image holographique » et permet aux utilisateurs de voir le contenu numérique superposé au monde réel qui les entoure.

<br>

### <a name="types-of-mixed-reality-apps"></a>[Types d’applications de réalité mixte](types-of-mixed-reality-apps.md)
L’un des avantages du développement d’applications pour la réalité mixte est qu’il existe un éventail d’expériences que la plateforme peut prendre en charge. Des environnements virtuels entièrement immersifs à la couche d’informations légère sur l’environnement actuel d’un utilisateur, la réalité mixte fournit un ensemble d’outils robustes pour donner vie à toute expérience.

<br>

### <a name="keeping-holograms-in-place---coordinate-systems"></a>[Maintenir les hologrammes en place : systèmes de coordonnées](coordinate-systems.md)
Les applications de réalité mixte placent essentiellement les hologrammes dans votre monde de sorte qu’ils ressemblent à des objets réels. Cela implique de positionner précisément ces hologrammes à des endroits significatifs pour l’utilisateur, qu’il s’agisse d’une salle physique ou d’un monde virtuel que vous avez créé.

<br>

### <a name="making-holographic-objects-feel-real---spatial-mapping"></a>[Faire en sorte que les objets holographiques semblent réels : mappage spatial](spatial-mapping.md)
Le mappage spatial permet de placer des objets sur des surfaces réelles. Cela permet d’ancrer les objets dans le monde de l’utilisateur et de tirer parti des indicateurs de profondeur dans le monde réel.

<br>


---

<br>

![Facteurs de conception des interactions](images/UX/UX_Hero_Manipulation.jpg)

## <a name="interaction-design-factors-to-consider"></a>Facteurs de conception des interactions à prendre en compte


### <a name="choose-an-interaction-model-for-your-customer"></a>[Choisir un modèle d’interaction pour votre client](interaction-fundamentals.md)
Les interactions simples et instinctuelles sont étroitement liées dans la plateforme Mixed Reality. Nous avons suivi trois étapes pour que les développeurs et concepteurs d’applications puissent proposer des interactions faciles et intuitives à leurs clients.

<br>

### <a name="hands-and-motion-controllers"></a>[Mains et contrôleurs de mouvement](hands-and-tools.md)
Les utilisateurs peuvent toucher et manipuler les hologrammes directement avec une ou deux mains comme ils le font avec des objets réels. Ou avec des contrôleurs de mouvement, vous pouvez étendre les capacités physiques de l’utilisateur en proposant des interactions précises sur un large éventail de distances.

<br>

### <a name="directly-commanding-objects-with-voice-input"></a>[Commande directe d’objets par entrée vocale](voice-input.md)
La voix est l’un des principaux types d’entrée sur HoloLens. Elle vous permet de commander directement un hologramme sans avoir à utiliser de gestes. Une entrée vocale peut être un moyen naturel de communiquer votre intention.

<br>

### <a name="leveraging-the-users-eye-gaze"></a>[Tirer parti du pointage du regard de l’utilisateur](eye-tracking.md)
HoloLens 2 permet d’accéder à un nouveau niveau de compréhension contextuelle et humaine au sein de l’expérience holographique en offrant aux développeurs la capacité d’utiliser des informations sur ce que les utilisateurs regardent.

<br>


---

<br>


![Éléments de l’expérience utilisateur](images/UX/UX_Hero_BoundingBox.jpg)

## <a name="user-experience-elements-for-mixed-reality"></a>Éléments de l’expérience utilisateur pour la réalité mixte


### <a name="color-light-and-materials"></a>[Couleurs, éclairage et matériaux](color,-light-and-materials.md)
La conception de contenu pour la réalité mixte nécessite d’accorder une attention particulière à la couleur, à l’éclairage et aux matériaux de chacune des ressources visuelles utilisées dans votre expérience.

<br>

### <a name="suggesting-the-scale-of-an-object"></a>[Suggérer l’échelle d’un objet](scale.md)
L’une des clés pour afficher du contenu qui semble réaliste sous forme holographique est de simuler les caractéristiques visuelles du monde réel aussi fidèlement que possible. Cela consiste à incorporer autant d’indicateurs visuels que possible susceptibles de nous aider (dans le monde réel) à comprendre la position des objets, leur taille et leur composition.

<br>

### <a name="clear-and-readable-typography"></a>[Typographie claire et lisible](typography.md)
Tout comme la typographie sur les écrans 2D, l’objectif est d’être clair et lisible. Avec l’aspect tridimensionnel de la réalité mixte, il est possible d’affecter le texte et l’expérience utilisateur globale beaucoup mieux.

<br>

### <a name="common-controls-and-behaviors"></a>[Contrôles et comportements communs](app-patterns-landingpage.md)
Découvrez les modules d’interface utilisateur et les interactions spatiales courantes fréquemment utilisés pour les expériences de réalité mixte.



<br>


---

## <a name="choose-a-prototyping-option"></a>Choisir une option de prototypage  

:::row:::   
    :::column:::    
       [![Découvrir Unity](images/Final_unity_logo.png)](https://learn.unity.com/)<br>
        **[Découvrir Unity](https://learn.unity.com/)**<br>
        Découvrez comment créer des expériences interactives avec Unity. Apprenez par la pratique, du début à la fin.
    :::column-end:::    
    :::column:::    
        [![Mixed Reality Toolkit (MRTK)](images/Final_mrtk-small_logo.png)](https://github.com/Microsoft/MixedRealityToolkit-Unity)<br>
        **[Mixed Reality Toolkit (MRTK)](https://github.com/Microsoft/MixedRealityToolkit-Unity)**<br>  
        Avec l’interaction spatiale et les composants d’interface utilisateur, démarrez la conception et le développement de votre réalité mixte avec Unity.   
    :::column-end:::
    :::column:::    
        [![Mixed Reality Design Labs](images/Final_mrdl_logo.png)](https://github.com/Microsoft/MRDL_Unity_PeriodicTable)<br>
        **[Mixed Reality Design Labs](https://github.com/Microsoft/MRDL_Unity_PeriodicTable)**<br>  
        Obtenez des exemples d’applications qui vous montrent comment utiliser les composants de MRTK pour créer de superbes expériences de réalité mixte.
    :::column-end:::        
    :::column:::    
        [![Microsoft Maquette](images/Final_maquette_logo.png)](https://www.maquette.ms/)<br>
        **[Microsoft Maquette](https://www.maquette.ms/)**<br>  
        Conception de réalité virtuelle. Microsoft maquette rend le prototypage spatial facile, rapide et immersif. 
    :::column-end:::    
:::row-end:::

<br>

---



## <a name="what-would-you-like-to-do-next"></a>Que voulez-vous faire à présent ?

:::row:::
    :::column:::
       [![Comprendre les principes de base](images/icon-lightbulb.png)](get-started-with-mr.md#understand-the-basics)<br>
        **[Comprendre les principes de base](get-started-with-mr.md#understand-the-basics)**<br>
        Approfondissez votre compréhension de ce qui définit la réalité mixte et de la manière de l’utiliser.
    :::column-end:::
    :::column:::
        [![Participer à un événement](images/icon-calendar.jpg)](sf-academy-events.md)<br>
         **[Participer à un événement](sf-academy-events.md)**<br>
        Venez voir le matériel et participer à un atelier pratique pour créer votre première application HoloLens 2.
    :::column-end:::
    :::column:::
        [![Installer les outils](images/icon-design.jpg)](install-the-tools.md)<br>
         **[Installer les outils](install-the-tools.md)**<br>
        Utilisez la liste de vérification de l’installation pour obtenir les outils dont vous avez besoin pour créer des applications pour HoloLens et la réalité mixte.
    :::column-end:::
    :::column:::
        [![Commencer à développer](images/icon-developer.jpg)](development.md)<br>
        **[Commencer à développer](development.md)**<br>
        Choisissez un chemin de développement en fonction de votre niveau de compétence, de votre méthode de travail ou de la plateforme qui vous intéresse.
    :::column-end:::
:::row-end:::


<br>

<br>


