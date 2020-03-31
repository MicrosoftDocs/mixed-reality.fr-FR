---
title: Tutoriels de démarrage - 4. Placement de contenu dynamique et utilisation de solveurs
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 8a85ab560d0e6b36b589970b4d5b8a441ed2bbe2
ms.sourcegitcommit: 536fd45b48a70bbeca1454cef517ae007225e533
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80362040"
---
# <a name="4-placing-dynamic-content-and-using-solvers"></a>4. Placement de contenu dynamique et utilisation de solveurs
<!-- Consider renaming to 'Placing dynamic content using Solvers' -->

Les hologrammes prennent vie dans HoloLens 2 quand ils suivent intuitivement l’utilisateur et sont placés dans l’environnement physique de manière à rendre l’interaction fluide et élégante. Dans ce tutoriel, nous allons étudier différentes manières de placer dynamiquement des hologrammes à l’aide des outils de placement fournis dans le MRTK, appelés « solveurs », pour résoudre des scénarios de placement spatial complexes. Dans le MRTK, les solveurs sont un système de scripts et de comportements utilisés pour permettre aux éléments de l’interface utilisateur de suivre l’utilisateur (vous) ou d’autres objets de jeu dans la scène. Ils servent également à accélérer l’alignement sur certaines positions, rendant votre application plus intuitive.

## <a name="objectives"></a>Objectifs

* Introduire les solveurs du MRTK
* Utiliser des solveurs pour qu’une collection de boutons suive l’utilisateur
* Utiliser des solveurs pour qu’un objet de jeu suive les mouvements captés des mains de l’utilisateur

## <a name="location-of-solvers-in-the-mrtk"></a>Emplacement des solveurs dans le MRTK

 Les solveurs du MRTK se trouvent dans le dossier du SDK MRTK. Pour voir les solveurs disponibles dans votre projet, dans la fenêtre Project, accédez à **Assets** > **MixedRealityToolkit.SDK** > **Features** > **Utilities** > **Solvers** :

![mrlearning-base](images/mrlearning-base/tutorial3-section1-step1-1.png)

Dans ce tutoriel, nous allons passer en revue l’implémentation des solveurs Orbital et Radial View. Pour en savoir plus sur l’ensemble des solveurs disponibles dans le MRTK, consultez le [guide des solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="use-a-solver-to-follow-the-user"></a>Utiliser un solveur pour suivre l’utilisateur
<!-- Consider renaming to 'Use a Solver to have an object follow the user' -->

Dans cette section, vous allez améliorer la collection de boutons que vous avez créée dans le didacticiel précédent afin qu’elle suive le regard de l’utilisateur. Vous allez également configurer le solveur pour que la collection de boutons :

* pivote parallèlement au sens de lecture de l’utilisateur, pour une lecture naturelle de gauche à droite ;
* soit positionnée sous la ligne horizontale du regard de l’utilisateur, de manière à ce qu’elle n’obstrue pas les autres objets que vous ajouterez par la suite dans ce tutoriel ;
* soit positionnée à environ un demi-bras de l’utilisateur, de manière à ce qu’il puisse appuyer facilement sur les boutons.

Pour ce faire, vous allez utiliser le solveur **Orbital** qui verrouille l’objet à une position et à un décalage spécifiés par rapport à l’objet référencé.

### <a name="1-add-the-orbital-solver"></a>1. Ajouter le solveur Orbital

Dans la fenêtre Hierarchy, sélectionnez l’objet **ButtonCollection** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Orbital (Script)** à l’objet ButtonCollection :

> [!NOTE]
> Quand vous ajoutez un solveur, dans ce cas le composant Orbital (Script), le composant Solver Handler (Script) est automatiquement ajouté car le solveur en a besoin.

### <a name="2-configure-the-orbital-solver"></a>2. Configurer le solveur Orbital

Configurez le composant **Solver Handler (Script)**  :

* Vérifiez que **Tracked Target Type** indique **Head**.

Configurez le composant **Orbital (Script)**  :

* Vérifiez que **Orientation Type** indique **Follow Tracked Object**.
* Réinitialisez **Local Offset** avec les valeurs X = 0, Y = 0, Z = 0.
* Définissez **World Offset** avec les valeurs X = 0, Y = -0,4 et Z = 0,3.

![mrlearning-base](images/mrlearning-base/tutorial3-section2-step2-1.png)

### <a name="3-test-the-orbital-solver-using-the-in-editor-simulation"></a>3. Tester le solveur Orbital à l’aide de la simulation dans l’éditeur

Appuyez sur le bouton de lecture pour passer en mode Game, puis appuyez sur le bouton droit de la souris et maintenez-le enfoncé pour faire pivoter la direction de votre regard. Notez les points suivants :

* Les valeurs Position du paramètre Transform de ButtonCollection sont maintenant pilotées par les paramètres du solveur.
* La position de l’objet Cube, qui n’est pas affecté par le solveur, est inchangée.

![mrlearning-base](images/mrlearning-base/tutorial3-section2-step3-1.png)

> [!TIP]
> Si vous ne voyez pas le rayon de l’appareil photo dans votre fenêtre Scene, vérifiez que votre menu Gizmos est activé. Pour en savoir plus sur le menu Gizmos et sur la façon dont vous pouvez l’utiliser pour optimiser votre vue Scene, consultez la page consacrée au <a href="https://docs.unity3d.com/Manual/GizmosMenu.html" target="_blank">menu Gizmos</a> dans la documentation Unity.
>
> Pour afficher côte à côte les fenêtres Scene et Game comme dans l’image ci-dessus, faites simplement glisser la fenêtre Game à droite de la fenêtre Scene. Pour en savoir plus, consultez la page consacrée à la <a href="https://docs.unity3d.com/Manual/CustomizingYourWorkspace.html" target="_blank">personnalisation de votre espace de travail</a> dans la documentation Unity.

## <a name="enabling-objects-to-follow-tracked-hands"></a>Faire en sorte que les objets suivent les mouvements captés des mains

Dans cette section, vous allez configurer l’objet Cube que vous avez créé dans le tutoriel précédent afin qu’il suive les mouvements captés des mains de l’utilisateur, en particulier le poignet droit. Vous allez également configurer le solveur pour que l’objet Cube :

* change son orientation en fonction de la rotation de la main de l’utilisateur ;
* soit positionné sur le poignet de l’utilisateur.

Pour cela, vous allez utiliser le solveur **Radial View** qui maintient l’objet dans un cône de vue projeté par l’objet référencé.

### <a name="1-add-the-radial-view-solver"></a>1. Ajouter le solveur Radial View

Dans la fenêtre Hierarchy, sélectionnez l’objet **Cube** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter l’objet Cube du composant **Radial View (Script)** .

### <a name="2-configure-the-radial-view-solver"></a>2. Ajouter le solveur Radial View

Configurez le composant **Solver Handler (Script)**  :

* En regard de **Tracked Target Type**, sélectionnez **Hand Joint**.
* En regard de **Tracked Handness**, sélectionnez **Right**.
* En regard de **Tracked Hand Joint**, sélectionnez **Wrist**.

Configurez le composant **Radial View (Script)**  :

* En regard de **Reference Direction**, sélectionnez **Object Oriented**, puis cochez la case **Orient To Reference Direction**.
* Définissez **Min Distance** et **Max Distance** avec la valeur 0.

![mrlearning-base](images/mrlearning-base/tutorial3-section3-step2-1.png)

### <a name="3-test-the-radial-view-solver-using-the-in-editor-simulation"></a>3. Tester le solveur Radial View à l’aide de la simulation dans l’éditeur

Appuyez sur le bouton de lecture pour passer en mode Game, puis appuyez sur la barre d’espace et maintenez-la enfoncée pour faire apparaître la main. Déplacez le curseur de la souris pour déplacer la main, puis cliquez sur le bouton gauche de la souris et maintenez-le enfoncé pour faire pivoter la main :

![mrlearning-base](images/mrlearning-base/tutorial3-section3-step3-1.png)

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à utiliser les solveurs du MRTK pour que l’interface utilisateur suive intuitivement l’utilisateur. Vous avez également vu comment attacher un solveur à un objet (par exemple, un cube) pour suivre les mouvements captés des mains de l’utilisateur. Pour en savoir plus sur ces solveurs et d’autres fournis avec le MRTK, consultez le [guide des solveurs](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_Solver.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

[Tutoriel suivant : 5. Interaction avec les objets 3D](mrlearning-base-ch4.md)
