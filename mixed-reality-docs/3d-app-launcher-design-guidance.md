---
title: Guide de conception du lanceur d’applications 3D
description: Un lanceur d’applications 3D est un objet « physique » dans la maison de réalité mixte de l’utilisateur qu’il peut sélectionner pour lancer une application.
author: thmignon
ms.author: thmignon
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, mode de lancement d’application 3D, casque immersif, cube actif
ms.openlocfilehash: ce9d242e26d67c8fe5af7ac32f4e910a15715d25
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437223"
---
# <a name="3d-app-launcher-design-guidance"></a>Guide de conception du lanceur d’applications 3D

Lorsque vous placez un casque Windows Mixed Reality (VR), vous accédez à la page d’hébergement de Windows Mixed Reality, visualisée en tant que maison sur une falaise placée par des montagnes et de l’eau (vous pouvez toutefois [choisir d’autres environnements et même créer votre propre environnement](add-custom-home-environments.md)). Dans l’espace de cette page d’hébergement, un utilisateur est libre de réorganiser et d’organiser les objets et applications 3D dont il se soucie. Un **lanceur d’applications 3D** est un objet « physique » dans la maison de réalité mixte de l’utilisateur qu’il peut sélectionner pour lancer une application.

Exemple de ![: le lanceur d’applications 3D à effet flottant](images/20171016-151526-mixedreality1-1200px-1000px.jpg)<br>
*Exemple de lanceur d’application 3D d’oiseau flottant (application fictive)*

## <a name="3d-app-launcher-creation-process"></a>processus de création du lanceur d’applications 3D

La création d’un lanceur d’applications 3D comporte trois étapes :
1. Conception et concept (cet article)
2. [Modélisation et exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. Intégration dans votre application :
    * [Applications UWP](implementing-3d-app-launchers.md)
    * [Applications Win32](implementing-3d-app-launchers-win32.md)

## <a name="design-concepts"></a>Concepts de conception

### <a name="fantastic-yet-familiar"></a>Fantastique, encore familier

L’environnement Windows Mixed Reality dans lequel se trouve votre lanceur d’applications est une partie familière, une partie fantastique/science-fi. Les meilleurs lanceurs suivent les règles de ce monde. Pensez à la façon dont vous pouvez prendre un objet représentatif familier de votre application, mais pliez certaines règles de réalité réelle. La magie se produira.

### <a name="intuitive"></a>Peu

Lorsque vous examinez le lanceur d’applications, son objectif est de lancer votre application. il doit être évident et ne devrait pas provoquer de confusion. Par exemple, assurez-vous que votre lanceur est un représentant évident et évident de votre application qu’il ne sera pas confondu avec un morceau de décor dans la maison de la falaise. Votre lanceur d’applications doit inviter des personnes à les toucher/sélectionner.

Exemple de ![: nouveau lanceur d’applications de note 3D](images/20171016-152145-mixedreality1-1200px-1000px.jpg)<br>
*Exemple de lanceur d’application 3D note (application fictive)*

### <a name="home-scale"></a>Échelle personnelle

les lanceurs d’applications 3D qui vivent dans la maison de la falaise et leur taille par défaut doivent avoir un sens avec les autres objets « physiques » de l’espace. Si vous placez votre lanceur à côté, par exemple, d’une usine de maison ou de meubles, vous devez vous sentir à la maison, à la taille. Un bon point de départ consiste à voir comment il s’agit de 30 centimètres cubes, mais n’oubliez pas que les utilisateurs peuvent le mettre à l’échelle s’ils le souhaitent.

### <a name="own-able"></a>En toute possession

Le lanceur d’application doit ressembler à un objet qu’une personne peut avoir dans son espace. Elles seront virtuellement entourées de ces éléments, de sorte que le lanceur doit avoir le même aspect que quelque chose que l’utilisateur a été jugé suffisamment souhaitable pour se rendre à la recherche et rester à proximité.

Exemple de ![: lanceur d’application Astro Warp 3D](images/20171016-132936-mixedreality-1200px-1000px.jpg)<br>
*Exemple de lanceur d’application Astro Warp 3D (application fictive)*

### <a name="recognizable"></a>Reconnaissable

Votre lanceur d’applications 3D doit instantanément exprimer « la personnalisation de votre application » aux personnes qui l’affichent. Si votre application contient un caractère en étoile ou un objet particulièrement identifiable, nous vous recommandons de l’utiliser comme une partie importante de votre conception. Dans un monde de réalité mixte, un objet attire davantage l’intérêt des utilisateurs qu’un seul logo. Les objets reconnaissables communiquent la personnalisation rapidement et clairement.

### <a name="volumetric"></a>Dosage

Votre application mérite plus que simplement placer votre logo sur un plan plat et l’appeler une journée. Votre lanceur doit ressembler à un objet physique passionnant et 3D dans l’espace de l’utilisateur. Une bonne approche consiste à imaginer que votre application allait avoir une info-bulle dans la parade du jour de Thanksgiving de Macy. Demandez-vous ce que les gens étaient vraiment en mesure de tomber dans la rue ? Que feriez-vous de tous les angles d’affichage ?


:::row:::
    :::column:::
        Logo ![uniquement](images/20171016-140436-mixedreality-640px.jpg) *logo*
    :::column-end:::
    :::column:::
        ![plus reconnaissable avec un caractère](images/20171016-140557-mixedreality-640px.jpg) *plus reconnaissable avec un caractère*
    :::column-end:::
:::row-end:::


:::row:::
    :::column:::
        ![approche plate, pas surprenant, vous semble plat](images/20171016-155101-mixedreality-640px.jpg) une *approche plate, pas étonnamment surprenant,*
    :::column-end:::
    :::column:::
        ![approche volumétrique illustre mieux votre application](images/20171016-161407-mixedreality-640px.jpg) *approche volumétrique présente mieux votre application*
    :::column-end:::
:::row-end:::


## <a name="tips-for-good-3d-models"></a>Conseils pour les bons modèles 3D

### <a name="best-practices"></a>Meilleures pratiques
* Lors de la planification de dimensions pour votre lanceur d’applications, prenez des 30cm à peu près un cube. Par conséquent, un ratio de taille de 1:1:1.
* Les modèles doivent être sous les polygones 10 000. [En savoir plus sur le nombre de triangles et les niveaux de détail (LODs)](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#triangle-counts-and-levels-of-detail-lods)
* Testez sur un casque immersif lorsque cela est possible.
* Créez des détails dans la géométrie de votre modèle, dans la mesure du possible, ne vous fiez pas aux textures pour des détails.
* Créez une géométrie fermée « eau serrée ». Aucun trou n’est modélisé dans.
* Utilisez des matériaux naturels dans votre objet. Imaginez que vous le concevez dans le monde réel.
* Assurez-vous que votre modèle lit bien des distances et des tailles différentes.
* Lorsque votre modèle est prêt à l’emploi, lisez les [instructions relatives](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#asset-requirements-overview)à l’exportation de ressources.

![modèle avec des détails subtils dans la texture](images/20171013-143334-mixedreality-640px.jpg)<br>
*Modèle avec des détails subtils dans la texture*

### <a name="what-to-avoid"></a>Éléments à éviter
* N’utilisez pas de détails à contraste élevé ni de modèles et de textures de petite taille, occupés.
* N’utilisez pas de géométrie fine : elle ne fonctionne pas bien à distance et fera mal l’alias.
* Ne laissez pas les parties de votre modèle s’étendre trop au-delà du ratio de taille de 1:1:1. Il va créer des problèmes de mise à l’échelle.

![éviter les modèles à contraste élevé, à faible occupation](images/20171013-143603-mixedreality-640px.jpg)<br>
*Évitez les modèles à contraste élevé, les petits et les plus occupés*

## <a name="how-to-handle-type"></a>Comment gérer le type

### <a name="best-practices"></a>Meilleures pratiques
* Nous vous recommandons de faire en sorte que votre type comporte environ 1/3 de votre lanceur d’applications (ou plus). Le type est l’élément principal qui donne aux gens une idée que votre lanceur est, en fait, un lanceur, ce qui est intéressant s’il est assez important.
* Évitez de rendre le type Super étendu : essayez de le conserver dans les limites des dimensions principales des lanceurs d’applications (plus ou moins).
* Le type plat peut fonctionner, mais sachez qu’il peut être difficile à afficher à partir de certains angles et dans certains environnements. Vous pouvez envisager de placer un objet solide ou un fond en arrière-plan pour faciliter cette opération.
* L’ajout d’une dimension à votre type semble agréable en 3D. L’ombrage des côtés du type d’une couleur plus sombre peut contribuer à la lisibilité.


:::row:::
    :::column:::
        ![type plat sans fond peut être difficile à afficher à partir de certains angles et dans certains environnements,](images/flattype-640px.png) *type plat sans fond peut être difficile à afficher à partir de certains angles et dans certains environnements*
    :::column-end:::
    :::column:::
        ![type avec une zone de fond intégrée peut fonctionner correctement](images/flattypeandbkg-640px.png) *type avec un fond intégré peut fonctionner correctement*
    :::column-end:::
    :::column:::
        ![type extrudé peut fonctionner correctement si vous Nuancez les côtés](images/20171016-160221-mixedreality-640px.jpg) *type extrudé peut fonctionner correctement si vous Nuancez les côtés*
    :::column-end:::
:::row-end:::


**Tapez les couleurs qui fonctionnent**
* ajourée
* fond
* Couleur semi-saturée vive

![les couleurs de type qui fonctionnent.](images/20171016-112111-mixedreality-640px.jpg)<br>
*Tapez les couleurs qui fonctionnent*

### <a name="what-to-avoid"></a>Éléments à éviter

**Couleurs de type qui provoquent des problèmes**
* Mi-tons
* coché
* Couleurs sursaturées ou couleurs désaturées

![des couleurs de type qui provoquent des problèmes.](images/20171016-112246-mixedreality-640px.jpg)<br>
*Couleurs de type qui provoquent des problèmes*

## <a name="lighting"></a>Éclairage

L’éclairage de votre lanceur d’applications provient de l’environnement de la maison de la falaise. Veillez à tester votre lanceur à plusieurs endroits de la maison, afin qu’il soit parfait dans le ciel et dans les ombres. La bonne nouvelle, c’est que si vous avez suivi les autres conseils de conception de ce document, votre lanceur doit être de forme assez bonne pour la plupart des éclairages de la maison de la falaise.

Les bonnes places pour tester la manière dont votre lanceur regarde dans les différentes lumières de l’environnement sont le Studio, la salle de support, n’importe où et sur le patio Back (la zone concrète avec la pelouse). Un autre bon test consiste à le placer en demi-feu et demi-ombre et à voir à quoi il ressemble.

![Assurez-vous que votre lanceur semble parfait en clair et dans les ombres.](images/20171013-145523-mixedreality-1200px-1000px.jpg)<br>
*Assurez-vous que votre lanceur semble parfait dans le ciel et dans les ombres*

## <a name="texturing"></a>Texturation

### <a name="authoring-your-textures"></a>Création de vos Textures

Le format de fin de votre lanceur d’application 3D est un fichier. GLB, qui est créé à l’aide du pipeline PBR (rendu physique). Il peut s’agir d’un processus délicat. à présent, nous vous conseillons d’employer un artiste technique si vous ne l’avez pas déjà fait. Si vous êtes un peu vos propres méthodes-er, prenez le temps de [Rechercher et d’apprendre la terminologie du PBR](https://wiki.polycount.com/wiki/PBR) et ce qui se passe en coulisse avant de commencer vous aidera à éviter les erreurs courantes. 

Exemple de ![: nouvelle note d’application](images/pbr-freshnote1-640px-500px.png)<br>
*Exemple de lanceur d’application 3D note (application fictive)*

**Outil de création recommandé**

Nous vous recommandons d’utiliser l’outil de création de [substance](https://www.allegorithmic.com/products/substance-painter) par Allegorithmic pour créer votre fichier final. Si vous n’êtes pas familiarisé avec la création de nuanceurs PBR dans l’outil de création de substance, voici un [didacticiel](https://docs.allegorithmic.com/documentation/display/SPDOC/Tutorials).

(Vous pouvez également utiliser la [couche 3D](https://3dcoat.com/home/), [Quixel suite 2](https://quixel.se/suite2/)ou [marmoset Toolbag](https://www.marmoset.co/toolbag/) si vous êtes plus familiarisé avec l’un d’eux).

### <a name="best-practices"></a>Meilleures pratiques

* Si votre objet de lanceur d’application a été créé pour le PBR, il doit être assez simple de le convertir pour l’environnement de la maison de la falaise.
* Notre nuanceur attend un flot de travail Metal/grossiste : le nuanceur PBR non réel est une fac-similé de fermeture.
* Lorsque vous exportez vos Textures, gardez les [tailles de texture recommandées](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#material-guidelines) à l’esprit.
* Veillez à créer vos objets pour l’éclairage en temps réel, à savoir :
    * Évitez les ombres cuites, ou les ombres peintes
    * Éviter l’éclairage cuit dans les textures
    * Utilisez l’un des packages de création de matériel PBR pour obtenir les mappages appropriés générés pour notre nuanceur

## <a name="see-also"></a>Articles associés

* [Créer des modèles 3D à utiliser dans la réalité mixte](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [Implémenter des lanceurs d’applications 3D (applications UWP)](implementing-3d-app-launchers.md)
* [Implémenter des lanceurs d’applications 3D (applications Win32)](implementing-3d-app-launchers-win32.md)
