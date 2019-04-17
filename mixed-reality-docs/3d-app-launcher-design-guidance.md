---
title: Guide de conception du Lanceur d’application 3D
description: Un lanceur d’applications 3D est un objet « physique » dans la maison de réalité mixte de l’utilisateur qu’ils peuvent sélectionner pour lancer une application.
author: thmignon
ms.author: thmignon
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, de lanceur d’applications 3D immersif casque, live cube
ms.openlocfilehash: 47db5bffa121c0cc11d246dc749c464e5f187270
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593646"
---
# <a name="3d-app-launcher-design-guidance"></a>Guide de conception du Lanceur d’application 3D

Quand vous placez sur un casque (VR) immersif de Windows Mixed Reality, vous entrez Windows Mixed Reality domestique, affichée sous la forme d’une maison sur une falaise entouré d’eau et Montagnes (bien que vous puissiez [choisissez autres environnements et même créer vos propres](add-custom-home-environments.md)). Dans l’espace de cette maison, un utilisateur est libre de réorganiser les objets 3D et les applications qui les intéressent tout comme ils le souhaitent. Un **Lanceur d’applications 3D** est un objet « physique » dans l’utilisateur mixte de maison réalité qu’ils peuvent sélectionner pour lancer une application.

![Exemple : Lanceur d’applications 3D Bird flottante](images/20171016-151526-mixedreality1-1200px-1000px.jpg)<br>
*Exemple de lanceur flottante application 3D d’imagerie Bird ' s (application fictive)*

## <a name="3d-app-launcher-creation-process"></a>Processus de création de lanceur application 3D

Il existe 3 étapes à la création d’un lanceur d’applications 3D :
1. Conception et concepting (cet article)
2. [Modélisation et l’exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. Intégration dans votre application :
    * [Applications UWP](implementing-3d-app-launchers.md)
    * [Applications Win32](implementing-3d-app-launchers-win32.md)

## <a name="design-concepts"></a>Principes de conception

### <a name="fantastic-yet-familiar"></a>Tout simplement fantastique encore familier

L’environnement Windows Mixed Reality dans que Lanceur d’applications se trouve est partie familière, partie fantastiques/sci-fi. Les lanceurs meilleures suivent les règles de ce monde. Imaginez comment vous pouvez prendre un objet familière et représentatif de votre application, mais certaines des règles de réalité réelle de pliage. Magic entraîne.

### <a name="intuitive"></a>Intuitive

Lorsque vous examinez le Lanceur d’applications, son objectif - pour lancer votre application - devrait être évident et ne devrait pas causer de toute confusion. Par exemple, n’oubliez pas que votre Lanceur est un évident suffisamment représentative de votre application qu’elle ne sont pas confondue pour un élément de décor dans le Cliff House. Lanceur d’applications doit inviter des personnes à tactile/sélectionner il.

![Exemple : Lanceur d’applications 3D Remarque fraîche](images/20171016-152145-mixedreality1-1200px-1000px.jpg)<br>
*Exemple de Lanceur d’application 3D Remarque fraîche (application fictive)*

### <a name="home-scale"></a>Accueil mise à l’échelle

Lanceurs d’applications 3D live dans le Cliff House et leur taille par défaut vous semblera logique avec les autres objets « physiques » dans l’espace. Si vous placez votre Lanceur beside, par exemple, une usine de la maison ou certains meubles, cela vous à la maison, size-wise. Un bon point de départ consiste à voir à quoi il ressemble à 30 centimètres cubes, mais n’oubliez pas que les utilisateurs mettre à l’échelle vers le haut ou vers le bas s’ils le souhaitent.

### <a name="own-able"></a>Peut être propriétaire

Le Lanceur d’applications doit sembler un objet, une personne serait ravie d’accueillir dans leur espace. Ils amèneront être pratiquement entourant eux-mêmes avec ces éléments, donc le Lanceur doit s’apparentent à quelque chose l’idée de l’utilisateur a été suffisamment souhaitable pour débusquer et conserver à proximité.

![Exemple : Lanceur d’applications 3D de astro Warp](images/20171016-132936-mixedreality-1200px-1000px.jpg)<br>
*Exemple de lanceur d’application 3D astro Warp (application fictive)*

### <a name="recognizable"></a>Reconnaissable

Le Lanceur d’applications 3D doit instantanément express « marque de votre application » aux personnes il. Si vous avez un caractère en étoile ou un objet en particulier identifiable dans votre application, nous vous recommandons de l’utiliser comme une grande partie de votre conception. Dans un monde de réalité mixte, un objet sera susciter l’intérêt du plus à partir d’utilisateurs que simplement un logo autonome. Objets reconnaissables communiquent marque rapidement et de manière claire.

### <a name="volumetric"></a>Volumétriques

Votre application mérite plus que placer votre logo sur un plan plat et appel de journée. Votre Lanceur devriez vous sentir comme un objet physique, 3D et intéressant dans l’espace de l’utilisateur. Une bonne approche est d’imaginer que votre application s’apprêtait à avoir une info-bulle dans jour de Thanksgiving YCbCr de le Macy. Posez-vous, ce qui serait vraiment épater personnes tel qu’indiqué dans la rue ? Ce qui aurait l’aspect souhaité à partir de tous les angles d’affichage ?


:::row:::
    :::column:::
        ![Logo only](images/20171016-140436-mixedreality-640px.jpg)
        *Logo only*
    :::column-end:::
    :::column:::
        ![More recognizable with a character](images/20171016-140557-mixedreality-640px.jpg)
        *More recognizable with a character*
    :::column-end:::
:::row-end:::


:::row:::
    :::column:::
        ![Flat approach, not surprisingly, feels flat](images/20171016-155101-mixedreality-640px.jpg)
        *Flat approach, not surprisingly, feels flat*
    :::column-end:::
    :::column:::
        ![Volumetric approach better showcases your app](images/20171016-161407-mixedreality-640px.jpg)
        *Volumetric approach better showcases your app*
    :::column-end:::
:::row-end:::


## <a name="tips-for-good-3d-models"></a>Conseils pour les bons modèles 3D

### <a name="best-practices"></a>Meilleures pratiques
* Lorsque vous planifiez des dimensions du Lanceur de votre application, viser à peu près d’un cube de 30 centimètres. Par conséquent, 1 : rapport de taille de 1:1.
* Modèles doivent être des polygones moins de 10 000. [En savoir plus sur les nombres de triangle et les niveaux de détails (degrés)](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#triangle-counts-and-levels-of-detail-lods)
* Tester sur un casque immersif lorsque cela est possible.
* Détails de la build dans la géométrie de votre modèle lorsque cela est possible, ne vous fiez textures pour les détails.
* Construire une géométrie de « eau étroite » fermé. Aucune faille qui n’est pas modélisés.
* Utiliser des matériaux naturelles dans votre objet. Imaginez qu’il créant dans le monde réel.
* Assurez-vous que votre modèle lit bien avec les dimensions et les distances différents.
* Lorsque votre modèle est prêt à commencer, lisez le [exportation des indications de ressources](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#asset-requirements-overview).

![Modèle avec des détails subtils dans la texture](images/20171013-143334-mixedreality-640px.jpg)<br>
*Modèle avec des détails subtils dans la texture*

### <a name="what-to-avoid"></a>Pratiques à éviter
* N’utilisez pas les détails de contraste élevé ou modèles de petite taille, occupés et des textures.
* N’utilisez pas geometry mince : il ne fonctionne bien à distance et sera alias mal.
* Ne laissez pas les parties de votre modèle étendre trop au-delà de 1 : rapport de taille de 1:1. Il crée des problèmes de mise à l’échelle.

![Éviter le contraste élevé, de petits modèles occupés](images/20171013-143603-mixedreality-640px.jpg)<br>
*Éviter les modèles de contraste élevé, petite, occupés*

## <a name="how-to-handle-type"></a>Comment gérer le type

### <a name="best-practices"></a>Meilleures pratiques
* Nous vous recommandons de que votre type se compose d’environ 1/3 du Lanceur d’applications (ou plus). Le type est la principale chose qui fournit aux personnes une idée votre Lanceur est, en fait, un lanceur afin qu’il est intéressant si elle est assez importante.
* Évitez de faire très large de type – essayez de conserver dans les limites des lanceurs d’applications des dimensions de base (plus ou moins).
* Type plat, vous pouvez travailler, mais n’oubliez pas qu’il peut être difficile à afficher à partir de certains angles et dans certains environnements. Vous pouvez envisager de placer un objet solid ou l’arrière-plan derrière lui pour aider à ce sujet.
* Ajout de dimension à votre type semble intéressante en 3D. Les côtés du type d’ombrage une couleur différente, plus sombre peut faciliter la lisibilité.


:::row:::
    :::column:::
        ![Flat type without a backdrop can be hard to view from certain angles and in certain environments](images/flattype-640px.png)
        *Flat type without a backdrop can be hard to view from certain angles and in certain environments*
    :::column-end:::
    :::column:::
        ![Type with a built-in backdrop can work well](images/flattypeandbkg-640px.png)
        *Type with a built-in backdrop can work well*
    :::column-end:::
    :::column:::
        ![Extruded type can work well if you shade the sides](images/20171016-160221-mixedreality-640px.jpg)
        *Extruded type can work well if you shade the sides*
    :::column-end:::
:::row-end:::


**Couleurs de type qui fonctionnent**
* Blanc
* Noir
* Vif semi-structurées saturée

![Type des couleurs qui fonctionnent.](images/20171016-112111-mixedreality-640px.jpg)<br>
*Couleurs de type qui fonctionnent*

### <a name="what-to-avoid"></a>Pratiques à éviter

**Couleurs de type qui entraînent des problèmes**
* Demi-teintes
* Gris
* Excessif saturation des couleurs ou couleurs désaturées

![Type des couleurs qui entraînent des problèmes.](images/20171016-112246-mixedreality-640px.jpg)<br>
*Couleurs de type qui entraînent des problèmes*

## <a name="lighting"></a>Éclairage

L’éclairage du Lanceur de votre application provient de l’environnement Cliff House. Veillez à tester votre Lanceur à plusieurs endroits de la maison afin qu’il vous semble correct dans la lumière et les ombres. La bonne nouvelle, c’est, si vous avez suivi les conseils de conception dans ce document, votre Lanceur doit être assez bien établies pour la plupart des éclairage dans la Cliff House.

Bon pour tester la manière dont votre Lanceur apparence dans les différents voyants dans l’environnement est le Studio, la salle de média, n’importe où à l’extérieur et dans le Patio précédent (la zone concrète avec la pelouse). Un autre bon test consiste à placer dans la moitié de lumière et la moitié de clichés instantanés et voir à quoi elle ressemble.

![Assurez-vous que votre Lanceur semble correct dans la lumière et les ombres.](images/20171013-145523-mixedreality-1200px-1000px.jpg)<br>
*Assurez-vous que votre Lanceur semble correct dans la lumière et les ombres*

## <a name="texturing"></a>Texture

### <a name="authoring-your-textures"></a>Création de vos textures

Le format de la fin de votre Lanceur d’applications 3D sera un fichier .glb, qui est effectué à l’aide du pipeline PBR (physiquement en fonction de rendu). Cela peut être un processus difficile, est maintenant temps d’employer un artiste technique si vous n’avez pas déjà. Si vous êtes un courageux soi-même-er, prendre le temps de [effectuer des recherches et découvrez la terminologie PBR](http://wiki.polycount.com/wiki/PBR) et ce qui se passe sous le capot avant de commencer, vous éviterez les erreurs courantes. 

![Exemple : Application de Note de frais](images/pbr-freshnote1-640px-500px.png)<br>
*Exemple de Lanceur d’application 3D Remarque fraîche (application fictive)*

**Outil de création recommandé**

Nous vous recommandons d’utiliser [reproduire la mise en Substance](https://www.allegorithmic.com/products/substance-painter) par Allegorithmic pour créer votre fichier finale. Si vous n’êtes pas familiarisé avec la création de nuanceurs PBR en Substance, ici du peintre un [didacticiel](https://docs.allegorithmic.com/documentation/display/SPDOC/Tutorials).

(Vous pouvez également cliquer [3D-Coat](https://3dcoat.com/home/), [Quixel Suite 2](https://quixel.se/suite2/), ou [Marmoset Toolbag](https://www.marmoset.co/toolbag/) fonctionne également si vous êtes familiarisé avec un d’eux.)

### <a name="best-practices"></a>Meilleures pratiques

* Si votre objet de lanceur d’application a été créé pour PBR, il doit être relativement simple pour le convertir pour l’environnement Cliff House.
* Notre nuanceur attend un flux de travail complète/irrégularité : nuanceur de PBR Unreal l’est une télécopie ferme.
* Lorsque l’exportation de vos textures de conserver le [texture tailles recommandées](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#material-guidelines) à l’esprit.
* Veillez à créer vos objets d’éclairage en temps réel, cela signifie que :
    * Éviter les ombres cuites – ou shadows peintes
    * Éviter la boulangerie d’éclairage dans les textures
    * Utilisez une de l’objet material PBR création de packages pour obtenir les mappages de droit générés pour notre nuanceur de

## <a name="see-also"></a>Voir aussi

* [Créer des modèles 3D pour une utilisation dans la réalité mixte domestique](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [Implémenter des lanceurs d’applications 3D (applications UWP)](implementing-3d-app-launchers.md)
* [Implémenter des lanceurs d’applications 3D (applications Win32)](implementing-3d-app-launchers-win32.md)
