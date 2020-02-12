---
title: Didacticiels de mise en route-4. Placement de contenu dynamique et utilisation de solveurs
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 8275d5a97d7827d34ed3926cabe4032cc7f4cfac
ms.sourcegitcommit: cc61f7ac08f9ac2f2f04e8525c3260ea073e04a7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2020
ms.locfileid: "77129315"
---
# <a name="4-placing-dynamic-content-and-using-solvers"></a>4. placement de contenu dynamique et utilisation de solveurs
<!-- Consider renaming to 'Placing dynamic content using Solvers' -->

Les hologrammes arrivent à la vie dans HoloLens 2 lorsqu’ils suivent intuitivement l’utilisateur et sont placés dans l’environnement physique d’une manière qui rend l’interaction transparente et élégante. Dans ce didacticiel, nous explorons les façons de placer dynamiquement des hologrammes à l’aide des outils de positionnement disponibles de MRTK, appelés résolveurs, pour résoudre des scénarios de placement spatial complexes. Dans le MRTK, les solveurs sont un système de scripts et de comportements utilisés pour permettre aux éléments de l’interface utilisateur de suivre, de l’utilisateur ou d’autres objets de jeu dans la scène. Ils servent également à accélérer l’alignement sur certaines positions, rendant votre application plus intuitive.

## <a name="objectives"></a>Objectifs

* Introduire les solveurs de MRTK
* Utiliser des solveurs pour avoir une collection de boutons à la suite de l’utilisateur
* Utilisez les solveurs pour avoir un objet de jeu à la suite des mains suivies par l’utilisateur

## <a name="location-of-solvers-in-the-mrtk"></a>Emplacement des solveurs dans le MRTK

 Les solveurs de MRTK se trouvent dans le dossier du kit de développement logiciel (SDK) MRTK. Pour afficher les solveurs disponibles dans votre projet, dans la fenêtre projet, accédez à **ressources** > **MixedRealityToolkit. SDK** > **fonctionnalités** > **utilitaires** > **solveurs**:

![mrlearning-base](images/mrlearning-base/tutorial3-section1-step1-1.png)

Dans ce didacticiel, nous allons examiner l’implémentation du solveur orbital et du solveur de la vue radiale. Pour en savoir plus sur l’ensemble des programmes de résolution disponibles dans le MRTK, vous pouvez consulter le guide des [solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="use-a-solver-to-follow-the-user"></a>Utiliser un solveur pour suivre l’utilisateur
<!-- Consider renaming to 'Use a Solver to have an object follow the user' -->

Dans cette section, vous allez améliorer la collection de boutons que vous avez créée dans le didacticiel précédent afin qu’elle suive la direction du regard de l’utilisateur. En outre, vous allez également configurer le solveur pour que la collection de boutons soit toujours :

* Pivoté parallèlement au sens de lecture de l’utilisateur, pour une lecture naturelle de gauche à droite
* Positionné légèrement sous la direction du point d’interposition horizontal de l’utilisateur, il n’obstrue pas les autres objets que vous ajouterez plus loin dans ce didacticiel.
* Positionnée approximativement sur la longueur d’un demi-bras de l’utilisateur, les boutons peuvent être facilement enfoncés

Pour ce faire, vous allez utiliser le **Solveur orbital** qui verrouille l’objet à une position et à un décalage spécifiés à partir de l’objet référencé.

### <a name="1-add-the-orbital-solver"></a>1. ajouter le solveur orbital

Dans la fenêtre hiérarchie, sélectionnez l’objet **ButtonCollection** , puis dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter le composant **orbital (script)** à l’objet ButtonCollection.

> [!NOTE]
> Lorsque vous ajoutez un solveur, dans ce cas le composant orbital (script), le composant du gestionnaire de solveur (script) est automatiquement ajouté, car il est requis par le solveur.

### <a name="2-configure-the-orbital-solver"></a>2. configurer le solveur orbital

Configurez le composant du **Gestionnaire de solveur (script)** :

* Vérifier que **le type de cible suivi** est défini sur **Head**

Configurez le composant **orbital (script)** :

* Modifier le **type d’orientation** pour suivre l' **objet suivi**
* Réinitialiser le **décalage local** à X = 0, Y = 0, Z = 0
* Remplacez le **décalage universel** par X = 0, Y =-0,4, Z = 0,3

![mrlearning-base](images/mrlearning-base/tutorial3-section2-step2-1.png)

### <a name="3-test-the-orbital-solver-using-the-in-editor-simulation"></a>3. tester le solveur orbital à l’aide de la simulation dans l’éditeur

Appuyez sur le bouton lecture pour passer en mode jeu, puis appuyez et maintenez enfoncé le bouton droit de la souris pour faire pivoter la direction du regard et notez les points suivants :

* La position de la transformation de ButtonCollection est maintenant pilotée par les paramètres du solveur
* Le cube, qui n’est pas affecté par le solveur, reste à la même position

![mrlearning-base](images/mrlearning-base/tutorial3-section2-step3-1.png)

> [!TIP]
> Si vous ne voyez pas le rayon de l’appareil photo dans la fenêtre de votre scène, vérifiez que votre menu gizmos est activé. Pour en savoir plus sur le menu gizmos et sur la façon dont vous pouvez l’utiliser pour optimiser votre vue scène, vous pouvez consulter la documentation du <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">menu gizmos</a> d’Unity.
>
> Pour afficher côte à côte votre scène et votre fenêtre de jeu, comme indiqué dans l’image ci-dessus, faites simplement glisser la fenêtre du jeu vers le côté droit de la fenêtre de la scène. Pour en savoir plus sur la personnalisation de votre espace de travail, vous pouvez consulter la documentation sur la personnalisation de l' <a href="https://docs.unity3d.com/Manual/CustomizingYourWorkspace.html" target="_blank">espace de travail</a> .

## <a name="enabling-objects-to-follow-tracked-hands"></a>Activation d’objets pour suivre les mains suivies

Dans cette section, vous allez configurer l’objet de cube que vous avez créé dans le didacticiel précédent afin qu’il suive les mains suivies par l’utilisateur, en particulier le poignet de la main droite. En outre, vous allez également configurer le solveur pour que le cube :

* Change son orientation avec la rotation manuelle de l’utilisateur
* Positionné sur le poignet de l’utilisateur

Pour ce faire, vous allez utiliser le **Solveur vue radiale** qui conserve l’objet dans un cône de vue converti par l’objet référencé.

### <a name="1-add-the-radial-view-solver"></a>1. ajouter le solveur vue radiale

Dans la fenêtre hiérarchie, sélectionnez l’objet **cube** , puis dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter l’objet de cube du composant **vue transversale (script)** .

### <a name="2-configure-the-radial-view-solver"></a>2. configurer le solveur vue radiale

Configurez le composant du **Gestionnaire de solveur (script)** :

* Modifier **le type de cible suivi** pour la **jointure manuelle**
* Modifier la **main suivie** vers la **droite**
* Modifier l' **articulation du suivi sur le** **poignet**

Configurez le composant **vue transversale (script)** :

* Changez le **sens de référence** en **orienté objet**, puis activez la case à cocher **orienter vers la direction de référence**
* Modifier la **distance minimale** et la **distance maximale** à 0

![mrlearning-base](images/mrlearning-base/tutorial3-section3-step2-1.png)

### <a name="3-test-the-radial-view-solver-using-the-in-editor-simulation"></a>3. tester le solveur de la vue radiale à l’aide de la simulation dans l’éditeur

Appuyez sur le bouton lecture pour entrer en mode jeu, puis appuyez sur la barre d’espace et maintenez-la enfoncée pour afficher la main. Déplacez le curseur de la souris pour déplacer la main, puis cliquez et maintenez enfoncé le bouton gauche de la souris pour faire pivoter la main :

![mrlearning-base](images/mrlearning-base/tutorial3-section3-step3-1.png)

## <a name="congratulations"></a>Félicitations

Dans ce didacticiel, vous avez appris à utiliser les solveurs de MRTK pour qu’une interface utilisateur suive intuitivement l’utilisateur. Vous avez également appris à attacher un solveur à un objet (par exemple, cube) pour suivre les mains suivies par l’utilisateur. Pour en savoir plus sur ces autres programmes de résolution inclus dans le MRTK, vous pouvez consulter le guide des [solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

[Didacticiel suivant : 5. interaction avec les objets 3D](mrlearning-base-ch4.md)
