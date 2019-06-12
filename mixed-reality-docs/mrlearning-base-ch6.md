---
title: Module de base d’apprentissage de la réalité mixte - Exemple d’expérience d’assemblage de module lunaire
description: Dans cette leçon, nous allons combiner plusieurs concepts découverts dans les leçons précédentes pour créer un exemple d’expérience.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 8a2f388e842d521f991203916177e3dac15769eb
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "65730846"
---
# <a name="mr-learning-base-module---lunar-module-assembly-sample-experience"></a>Module de base d’apprentissage de la réalité mixte - Exemple d’expérience d’assemblage de module lunaire

Dans cette leçon, nous allons combiner plusieurs concepts découverts dans les leçons précédentes pour créer un exemple d’expérience. Nous allons créer une application d’assemblage de module lunaire où un utilisateur devra utiliser les mains suivies pour prendre des composants de module lunaire et tenter de les assembler. Nous allons utiliser des boutons enfonçables pour activer/désactiver des indicateurs d’emplacement, pour réinitialiser notre expérience et pour lancer notre module lunaire dans l’espace ! Dans des tutoriels à venir, nous continuerons de nous appuyer sur cette expérience, notamment avec des cas d’utilisation multi-utilisateurs complexes tirant parti d’Azure Spatial Anchors pour l’alignement spatial.

## <a name="objectives"></a>Objectifs

- Combiner plusieurs concepts issus des leçons précédentes pour créer une même expérience
- Découvrir comment activer/désactiver des objets
- Déclencher des événements complexes en utilisant des boutons enfonçables
- Utiliser la physique et les forces des corps rigides
- Explorer l’utilisation d’info-bulles

## <a name="instructions"></a>Instructions

### <a name="configuring-the-lunar-module"></a>Configuration du module lunaire

Dans ce chapitre, nous allons découvrir les différents composants nécessaires pour créer notre exemple d’expérience.

1. Ajoutez l’élément préfabriqué d’assemblage de module lunaire à votre scène de base. Pour cela, dans l’onglet de votre projet, recherchez « Rocket Launcher_Tutorial ». Vous pouvez également trouver l’élément préfabriqué dans Assets>BaseModuleAssets>Prefabs (Ressources>Ressources du module de base>Éléments préfabriqués). Vous pouvez voir deux éléments préfabriqués : un avec le nom « tutorial » et un autre avec le nom « complete ». Faites glisser l’élément préfabriqué « Rocket Launcher_Tutorial » vers votre scène de base. Vous pouvez positionner le placement de l’élément préfabriqué dans votre scène.
   Remarque: L’élément préfabriqué « Rocket Launcher_Complete » est le lanceur terminé, fourni à titre de référence. 

![Lesson6 Chapter1 Step1im](images/Lesson6_Chapter1_step1im.PNG)

Si vous développez l’objet de jeu « Rocket Launcher_Tutorial » dans votre hiérarchie et que vous développez ensuite l’objet « Lunar Module » (Module lunaire), vous voyez plusieurs objets enfants avec un matériau appelé « x-ray » (Rayon X). Le matériau « x-ray » permet une couleur légèrement translucide que nous allons utiliser comme indicateurs de placement pour l’utilisateur. 

![Lesson6 Chapter1 Noteaim](images/Lesson6_Chapter1_noteaim.PNG) Le module lunaire comprend cinq parties, avec lesquelles l’utilisateur va interagir, comme illustré dans l’image ci-dessous :

1.  Le boîtier du rover (Rover Enclosure)
2.  Le réservoir de carburant (Fuel Tank)
3.  La batterie (Energy Cell)
4.  Le portail d’accueil (Docking Portal) 
5.  Le capteur externe (External sensor)

![Lesson6 Chapter1 Notebim](images/Lesson6_Chapter1_notebim.PNG)

> Remarque: Les noms des objets de jeu que vous voyez dans la hiérarchie de votre scène de base ne correspondent pas aux noms des objets dans la scène.

Étape 2 : Ajoutez une source audio au module lunaire. Vérifiez que le module lunaire est sélectionné dans la hiérarchie de votre scène de base et cliquez sur « Add Component » (Ajouter un composant). Recherchez « Audio Source » et ajoutez-le à l’objet. Laissez-le vide pour l’instant. Nous allons l’utiliser plus tard pour jouer le son du lancement.
 ![Lesson6 Chapter1 Step2im](images/Lesson6_Chapter1_step2im.PNG) Étape 3 : Ajoutez le script « toggle placement hint ». Cliquez sur « Add Component » et recherchez « Toggle Placement Hints » (Activer/désactiver les indicateurs de placement). Il s’agit d’un script personnalisé qui vous permet d’activer et de désactiver les indicateurs translucides (objets avec le matériau « x-ray ») mentionnés précédemment. 
![Lesson6 Chapter1 Step3im](images/Lesson6_Chapter1_step3im.PNG) Étape 4 : Comme nous avons 5 objets, tapez « 5 » pour la taille du tableau d’objets de jeu. Vous devez alors voir apparaître 5 nouveaux éléments. 

![Lesson6 Chapter1 Step4bim](images/Lesson6_Chapter1_step4bim.PNG)

Faites glisser chacun des objets translucides dans les cadres indiquant « None (Game Object) » (Aucun (objet de jeu)). Faites glisser les objets suivants depuis le module lunaire dans votre scène de base : 

•   Backpack

•   GasTank

•   Topleftbody

•   Nose

•   LeftTwirler

 ![Lesson6 Chapter1 Step4aim](images/Lesson6_Chapter1_step4aim.PNG)

Le script « toggle placement hints » est maintenant configuré. Ceci nous permet d’activer et de désactiver les indicateurs.

Étape 5 : Ajoutez le script « launch lunar module ». Cliquez sur le bouton « Add Component », recherchez « launch lunar module » et sélectionnez-le. Ce script sera responsable du lancement du module lunaire. Quand nous appuyons sur un bouton configuré, il ajoute une force vers le haut au composant de corps rigide du module lunaire et provoque le lancement du module vers le haut. Si vous êtes à l’intérieur, le module lunaire peut se crasher sur le maillage de votre plafond. Mais si vous êtes à l’extérieur, il va voler indéfiniment dans l’espace. 

![Lesson6 Chapter1 Step5im](images/Lesson6_Chapter1_step5im.PNG)

Étape 6 : Ajustez la poussée afin que le module lunaire vole de façon fluide. Essayez une valeur de 0,01. Laissez le champ « Rb » vide. Rb signifie « rigid body » (corps rigide), et ce champ est renseigné automatiquement lors de l’exécution.

![Lesson6 Chapter1 Step6im](images/Lesson6_Chapter1_step6im.PNG)

### <a name="lunar-module-parts-overview"></a>Vue d’ensemble des composants du module lunaire
L’objet parent des composants du module lunaire est la collection des objets avec lesquels l’utilisateur va interagir. Les noms des objets de jeu (avec les noms étiquetés pour la scène entre parenthèses) sont fournis dans la liste ci-dessous :

- Backpack (Fuel Tank)
- GasTank (Energy Cell)
- TopLeftBody (Rover Enclosure)
- Nose (Docking Portal)
- LeftTwirler (External Sensor)

Notez que chacun de ces objets a un gestionnaire de manipulation, comme indiqué dans la leçon 4. Avec le gestionnaire de manipulation, les utilisateurs peuvent se saisir des objets et les manipuler. Notez aussi que le paramètre « two handed manipulation type » (Type de manipulation à deux mains) est défini sur « move and rotate » (Déplacer et faire pivoter). Ceci permet seulement à l’utilisateur de déplacer l’objet mais pas de changer sa taille, ce qui est la fonctionnalité souhaitée pour une application d’assemblage.
En outre, la manipulation de loin est désactivée, de façon à permettre seulement l’interaction directe avec les composants du module.

![Lesson6 Chapter2im](images/Lesson6_Chapter2im.PNG)

Le script de démonstration d’assemblage des parties (montré ci-dessus) est le script qui gère les objets à placer sur le module lunaire par l’utilisateur. 

Le champ « Object To Place » (Objet à placer) est la transformation qui est sélectionnée (dans le cas de l’image ci-dessus, sac à dos/réservoir) avec l’objet auquel elle peut se connecter. 

Les paramètres « Near Distance » (Distance proche) et « Far Distance » (Distance lointaine) sont chargés de déterminer la proximité à laquelle les composants sont insérés à l’emplacement ou relâchés. Par exemple, le sac à dos/réservoir doit être à une distance de 0,1 unité du module lunaire pour être inséré à l’emplacement. « Far Distance » définit l’emplacement où l’objet doit être détaché du module lunaire. Dans ce cas, la main de l’utilisateur doit saisir le sac à dos/réservoir et le tire à une distance de 0,2 unités du module lunaire pour le retirer de l’emplacement d’insertion et le remettre en place.

« Tool Tip Object » est l’étiquette d’info-bulle dans la scène. Quand les objets sont insérés à leur emplacement, l’étiquette est désactivée. 

La source audio sera automatiquement saisie. 

### <a name="placement-hints-buttons"></a>Boutons d’indicateurs de placement
Dans la [leçon 2](mrlearning-base-ch2.md), vous avez découvert comment placer et configurer des boutons pour faire des choses comme changer la couleur d’un élément ou lui faire jouer un son quand l’utilisateur l’enfonce. Nous allons continuer à utiliser ces principes pour configurer nos boutons permettant d’activer et de désactiver les indicateurs de placement. 

L’objectif est de configurer notre bouton pour que, chaque fois que l’utilisateur appuie sur le bouton d’indicateur de placement, il active/désactive la visibilité des indicateurs de placements translucides. 

Étape 1 : Déplacez le module lunaire vers l’emplacement vide « runtime only » (Exécution uniquement) dans le panneau de l’inspecteur avec l’objet Placement Hints (Indicateurs de placement) sélectionné dans la hiérarchie de votre scène de base. 
 ![Lesson6 Chapter3 Step1im](images/Lesson6_Chapter3_step1im.PNG) Étape 2 : Cliquez maintenant sur la liste déroulante indiquant « No Function » (Pas de fonction). Accédez à « TogglePlacementHints » et sous ce menu, sélectionnez « ToggleGameObjects() ». ToggleGameObjects() va activer et désactiver les indicateurs de placement afin qu’ils soient visibles ou invisibles chaque fois que le bouton est enfoncé.
 ![Lesson6 Chapter3 Step2im](images/Lesson6_Chapter3_step2im.PNG)

### <a name="configuring-the-reset-button"></a>Configuration du bouton de réinitialisation

Des situations peuvent se produire où l’utilisateur fait une erreur ou jette accidentellement l’objet, ou bien où il veut simplement réinitialiser l’expérience. Le bouton de réinitialisation va ajouter la possibilité de redémarrer l’expérience. 

Étape 1 : Sélectionnez le bouton de réinitialisation. Dans la scène de base, il est nommé « ResetRoundButton ». 

Étape 2 : Faites glisser le module lunaire depuis la hiérarchie de la scène de base vers l’emplacement vide sous « button pressed» (Bouton enfoncé ) dans le panneau de l’inspecteur.
 ![Lesson6 Chapter4 Step2im](images/Lesson6_Chapter4_step2im.PNG)

Étape 3 : Sélectionnez le menu déroulant qui indique « no function » et placez le curseur sur « LaunchLunarModule ». Sélectionnez maintenant « resetModule() ».

![Lesson6 Chapter4 Step3im](images/Lesson6_Chapter4_step3im.PNG)

> Remarque: Notez que par défaut, « GameObject.BroadcastMessage » est configuré en « ResetPlacement ». Ceci va diffuser un message appelé « ResetPlacement » pour tous les objets enfants de RocketLauncher_Tutorial. Tout objet ayant une méthode pour « ResetPlacement() » répond à ce message en réinitialisant sa position. 

### <a name="launching-the-lunar-module"></a>Lancement du module lunaire
Dans ce chapitre, nous allons configurer le bouton de lancement. Il va permettre à l’utilisateur d’appuyer sur le bouton et de lancer le module lunaire dans l’espace.

Étape 1 : Sélectionnez le bouton de lancement (dans la scène de base, il est nommé « LaunchRoundButton »). Faites glisser le module lunaire vers l’emplacement vide sous « Touch End » (Fin de l’interaction tactile) dans le panneau de l’inspecteur.
 ![Lesson6 Chapter5 Step1im](images/Lesson6_Chapter5_step1im.PNG) Étape 2 : Sélectionnez la liste déroulante indiquant « No Function » (Pas de fonction). Placez le curseur sur « LaunchLunarModule » et sélectionnez « StopThruster() ». Ceci va déterminer la quantité de poussée que l’utilisateur veut donner au module lunaire. 
 ![Lesson6 Chapter5 Step2im](images/Lesson6_Chapter5_step2im.PNG) Étape 3 : Sous « ButtonPressed() », ajoutez le module lunaire (cliquez, maintenez enfoncé et faites glisser) à l’emplacement vide. 

Étape 4 : Sélectionnez le menu déroulant qui indique « no function », placez le curseur sur « LaunchLunarModule » et sélectionnez « StartThruster () ». 
 ![Lesson6 Chapter5 Step4im](images/Lesson6_Chapter5_step4im.PNG) Étape 5 : Ajoutez de la musique au module lunaire pour que, quand la fusée décolle, la musique soit jouée. Pour cela, faites glisser le module lunaire à l’emplacement vide suivant sous « Bouton Pressed() ».

Étape 6 : Sélectionnez le menu déroulant « no function », placez le curseur sur « AudioSource », puis sélectionnez « PlayOneShot (AudioClip) ». Vous pouvez explorer les différents sons fournis avec le MRTK. Pour cet exemple, nous allons choisir « MRTK_Gem ».
 ![Lesson6 Chapter5 Step6im](images/Lesson6_Chapter5_step6im.PNG)


### <a name="congratulations"></a>Félicitations ! 
Vous avez entièrement configuré cette application ! Maintenant, quand vous appuyez sur Lecture, vous pouvez assembler entièrement le module lunaire, activer/désactiver les indicateurs, lancer le module lunaire et le réinitialiser pour le refaire entièrement.
