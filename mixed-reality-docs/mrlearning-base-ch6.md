---
title: Didacticiels de mise en route-7. Création d’un exemple d’application de module lunaire
description: Dans cette leçon, vous allez combiner plusieurs concepts appris dans les leçons précédentes pour créer un exemple d’expérience unique.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: b033e4f9a379fb1778da3d94da70262e073d141b
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926518"
---
# <a name="7-creating-a-lunar-module-sample-application"></a>7. création d’un exemple d’application de module lunaire

Dans ce didacticiel, plusieurs concepts sont combinés à partir de leçons précédentes pour créer un exemple d’expérience unique. Vous allez apprendre à créer une application d’assembly de module lunaire permettant à un utilisateur d’utiliser des mains suivies pour récupérer des parties du module lunaire et tenter d’assembler un module lunaire. Nous utilisons des boutons permettant de basculer les indicateurs de placement, de réinitialiser notre expérience et de lancer notre module lunaire dans l’espace ! Dans les prochains didacticiels, nous continuerons à développer cette expérience, qui comprend des cas d’utilisation multi-utilisateurs puissants qui tirent parti des ancres spatiales Azure pour l’alignement spatial.

## <a name="objectives"></a>Objectifs

- Combiner plusieurs concepts issus des leçons précédentes pour créer une même expérience
- Découvrir comment activer/désactiver des objets
- Déclencher des événements complexes en utilisant des boutons enfonçables
- Utiliser la physique et les forces des corps rigides
- Explorer l’utilisation d’info-bulles

## <a name="instructions"></a>Instructions

### <a name="configuring-the-lunar-module"></a>Configuration du module lunaire

Dans cette section, nous présentons les différents composants nécessaires pour créer notre exemple d’expérience.

1. Ajoutez l’assembly de module lunaire Prefab à votre scène de base. Pour ce faire, sous l’onglet projet, accédez à ressources > BaseModuleAssets > Prefabs. Vous verrez deux prefabs de lanceur fusée, faire glisser la Prefab Rocket Launcher_Tutorial dans votre scène et la positionner comme vous le souhaitez.

    >[!NOTE]
    >Le Prefab Rocket Launcher_Complete est le lanceur terminé, fourni à des fins de référence.

    ![Lesson6 Chapter1 Step1im](images/Lesson6_Chapter1_step1im.PNG)

    Si vous développez l’objet de jeu de fusée Launcher_Tutorial dans votre hiérarchie et que vous développez davantage l’objet de module lunaire, vous trouverez plusieurs objets enfants qui ont un matériau appelé « x-ray ». Le matériau « x-ray » autorise une couleur légèrement translucide qui sera utilisée comme indicateurs de placement pour l’utilisateur. 

    ![Lesson6 fichier chapter1 Noteaim](images/Lesson6_Chapter1_noteaim.PNG)

    Le module lunaire utilise cinq parties avec lesquelles l’utilisateur interagit, comme illustré dans l’image ci-dessous :

    1. Le boîtier du rover (Rover Enclosure)
    2. Le réservoir de carburant (Fuel Tank)
    3. La batterie (Energy Cell)
    4. Le portail d’accueil (Docking Portal)
    5. Le capteur externe (External sensor)

    ![Lesson6 Chapter1 Notebim](images/Lesson6_Chapter1_notebim.PNG)

    >[!NOTE]
    >Les noms des objets de jeu que vous voyez dans la hiérarchie de votre scène de base ne correspondent pas aux noms des objets dans la scène.

2. Ajoutez une source audio à l’objet de jeu LunarModule. Assurez-vous que LunarModule est sélectionné dans votre hiérarchie de scènes, puis cliquez sur Ajouter un composant. Recherchez la source audio et ajoutez-la à l’objet de jeu. Laissez le champ AudioClip vide pour le moment, mais changez le paramètre spécial Blend de 0 en 1 pour activer l’audio spatial. Vous allez utiliser cette source audio pour jouer un son de lancement plus tard.

    ![Lesson6 fichier chapter1 Step2im](images/Lesson6_Chapter1_step2im.PNG)

3. Ajoutez le script activer les indicateurs de positionnement. Cliquez sur Ajouter un composant et recherchez les indicateurs de positionnement bascule. Il s’agit d’un script personnalisé qui vous permet d’activer et de désactiver les indicateurs translucides (objets avec la matière de rayons x), comme mentionné précédemment.

    ![Lesson6 fichier chapter1 Step3im](images/Lesson6_Chapter1_step3im.PNG)

4. Étant donné que nous avons cinq objets, tapez « 5 » pour la taille du tableau d’objets de jeu. Vous verrez alors cinq nouveaux éléments s’affichent.

    ![Lesson6 Chapter1 Step4bim](images/Lesson6_Chapter1_step4bim.PNG)

    Faites glisser chacun des objets translucides dans toutes les zones Nom (objet de jeu). Faites glisser les objets suivants du module lunaire de votre scène vers les champs du tableau d’objets, comme indiqué dans l’image ci-dessus :

    ![Lesson6 Chapter1 Step4aim](images/Lesson6_Chapter1_step4aim.PNG)

    Le script activer/désactiver les indicateurs de positionnement est maintenant configuré, ce qui nous permet d’activer et de désactiver les indicateurs.

5. Ajoutez le script Launch lunaire module. Cliquez sur le bouton Ajouter un composant, recherchez « lancer le module lunaire » et sélectionnez-le. Ce script lance le module lunaire. Quand vous appuyez sur un bouton configuré, il ajoute une force vers le haut au composant de corps rigide du module lunaire et provoque le lancement du module vers le haut. Si vous êtes à l’intérieur, le module lunaire peut se crasher sur le maillage de votre plafond. Si vous vous trouvez dans une zone avec des plafonds élevés ou aucun plafond, le module lunaire se déplacera indéfiniment dans l’espace.

    ![Lesson6 Chapter1 Step5im](images/Lesson6_Chapter1_step5im.PNG)

6. Ajustez la poussée afin que le module lunaire vole de façon fluide. Essayez une valeur de 0,01. Laissez le champ « Rb » vide. RB représente le corps rigide et ce champ est automatiquement rempli lors de l’exécution.

    ![Lesson6 Chapter1 Step6im](images/Lesson6_Chapter1_step6im.PNG)

### <a name="lunar-module-parts-overview"></a>Vue d’ensemble des parties du module lunaire

L’objet parent des composants de module lunaire est la collection des objets avec lesquels l’utilisateur interagit. Les noms des objets de jeu avec des noms de scènes libellés entre parenthèses, sont fournis dans la liste ci-dessous :

- Sac à dos (cellule Energy)
- GasTank (réservoir de carburant)
- TopLeftBody (Rover Enclosure)
- Nose (Docking Portal)
- LeftTwirler (External Sensor)

Notez que chacun de ces objets a un gestionnaire de manipulation, comme expliqué dans la leçon 4. Cette fonctionnalité permet aux utilisateurs de saisir et de manipuler l’objet. Notez également que le paramètre, deux types de manipulation de la main, est défini sur déplacer et faire pivoter. Cette option permet uniquement à l’utilisateur de déplacer l’objet sans modifier sa taille, ce qui est la fonctionnalité souhaitée pour une application d’assembly.
En outre, la manipulation Far n’est pas vérifiée pour autoriser uniquement l’interaction directe des parties de module.

![Lesson6 Chapter2im](images/Lesson6_Chapter2im.PNG)

Le script de démonstration d’assembly d’un composant (illustré ci-dessus) est le script qui gère les objets que l’utilisateur place sur le module lunaire par l’utilisateur.

Le champ objet à placer est la transformation qui est sélectionnée, comme illustré dans l’image ci-dessus, le sac à dos/réservoir de carburant associé à l’objet auquel il se connecte.

Les paramètres distance à distance et distance déterminent la proximité des composants qui sont en place ou peuvent être libérés. Par exemple, le réservoir de sacs/carburants doit se trouver à 0,1 unités à l’extérieur du module lunaire pour pouvoir être placé en place. Le paramètre distance définit l’emplacement où l’objet peut être avant de se détacher du module lunaire. Dans ce cas, la main de l’utilisateur doit saisir le sac à dos/réservoir et le tire à une distance de 0,2 unités du module lunaire pour le retirer de l’emplacement d’insertion et le remettre en place.

L’info-bulle est l’étiquette de l’info-bulle dans la scène. Lorsque les objets sont alignés sur place, l’étiquette est désactivée.

La source audio est automatiquement saisie.

### <a name="configuring-the-placement-hints-button"></a>Configuration du bouton indicateurs de positionnement

Dans la [leçon 2](mrlearning-base-ch2.md), vous avez appris à placer et configurer des boutons permettant d’effectuer des opérations telles que modifier la couleur d’un élément ou faire en sorte qu’il émette un signal sonore lorsqu’il est poussé. Nous allons continuer à utiliser ces principes pour configurer nos boutons permettant d’activer et de désactiver les indicateurs de placement.

L’objectif est de configurer notre bouton afin que chaque fois que l’utilisateur appuie sur le bouton d’indication de placement, il active ou désactive la visibilité des indicateurs de placement translucides.

1. Déplacez le module lunaire vers l’emplacement vide du runtime uniquement dans le panneau Inspecteur, tandis que l’objet indicateur de positionnement est sélectionné dans votre hiérarchie de scènes de base.

    ![Lesson6 Chapter3 Step1im](images/Lesson6_Chapter3_step1im.PNG)

2. Cliquez sur la liste déroulante aucune fonction. Accédez à TogglePlacementHints et sélectionnez ToggleGameObjects () sous ce menu. ToggleGameObjects () active ou désactive les indicateurs de positionnement afin qu’ils soient visibles ou invisibles à chaque fois que le bouton est enfoncé.

    ![Lesson6 Chapter3 Step2im](images/Lesson6_Chapter3_step2im.PNG)

### <a name="configuring-the-reset-button"></a>Configuration du bouton de réinitialisation

Il y aura des situations où l’utilisateur fait une erreur, lève accidentellement l’objet à l’écart ou souhaite simplement réinitialiser l’expérience. Le bouton Réinitialiser permet de relancer l’expérience.

1. Sélectionnez le bouton Réinitialiser. Dans la scène de base, elle est nommée ResetRoundButton.

2. Faites glisser le module lunaire de la hiérarchie de la scène de base dans l’emplacement vide sous le bouton enfoncé dans le panneau de l’inspecteur.

    ![Lesson6 Chapter4 Step2im](images/Lesson6_Chapter4_step2im.PNG)

3. Sélectionnez le menu déroulant aucune fonction et pointez sur LaunchLunarModule, puis sélectionnez resetModule ().

    ![Lesson6 Chapter4 Step3im](images/Lesson6_Chapter4_step3im.PNG)

    >[!NOTE]
    >Notez que, par défaut, GameObject. BroadcastMessage est configuré sur ResetPlacement. Cela diffuse un message nommé ResetPlacement pour chaque objet enfant du RocketLauncher_Tutorial. Tout objet ayant une méthode pour ResetPlacement () répond à ce message en réinitialisant sa position.

### <a name="configuring-the-launch-button"></a>Configuration du bouton de lancement

Cette section explique comment configurer le bouton de lancement, qui permet à l’utilisateur d’appuyer sur le bouton et de lancer le module lunaire dans l’espace.

1. Sélectionnez le bouton lancer. Dans la scène de base, il s’agit de LaunchRoundButton. Faites glisser le module lunaire dans l’emplacement vide sous Touch end dans le panneau de l’inspecteur.

    ![Lesson6 Chapter5 Step1im](images/Lesson6_Chapter5_step1im.PNG)

2. Sélectionnez le menu déroulant no Function et pointez sur LaunchLunarModule, puis sélectionnez StopThruster (). Cela permet de contrôler le niveau de Poussée que l’utilisateur souhaite attribuer au module lunaire.

    ![Lesson6 Chapter5 Step2im](images/Lesson6_Chapter5_step2im.PNG)

3. Faites glisser le module lunaire de la hiérarchie de la scène de base dans l’emplacement vide sous le bouton enfoncé dans le panneau de l’inspecteur.

4. Cliquez sur le menu déroulant aucune fonction, puis sur LaunchLunarModule et sélectionnez StartThruster ().

    ![Lesson6 Chapter5 Step4im](images/Lesson6_Chapter5_step4im.PNG)

5. Ajoutez de la musique au module lunaire pour que la musique soit lue lorsque la fusée est désactivée. Pour ce faire, faites glisser le module lunaire vers l’emplacement vide suivant sous le bouton enfoncé ().

6. Sélectionnez le menu déroulant aucune fonction, pointez sur AudioSource, puis sélectionnez PlayOneShot (AudioClip). Vous pouvez explorer les différents sons fournis avec le MRTK. Dans cet exemple, nous allons utiliser « MRTK_Gem ».

    ![Lesson6 Chapter5 Step6im](images/Lesson6_Chapter5_step6im.PNG)

### <a name="congratulations"></a>Félicitations !

Vous avez entièrement configuré cette application. Maintenant, lorsque vous appuyez sur lire, vous pouvez assembler complètement le module lunaire, activer/désactiver les indicateurs, lancer le module lunaire et le réinitialiser pour redémarrer.
