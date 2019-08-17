---
title: Didacticiels de mise en route-7. Création d’un exemple d’application de module lunaire
description: Dans cette leçon, nous allons combiner plusieurs concepts découverts dans les leçons précédentes pour créer un exemple d’expérience.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: f45aa7e2f07a8a67cd56f0aae140de3a68afc918
ms.sourcegitcommit: e9a55528965048ce34f8247ef6e544f9f432ee37
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69559891"
---
# <a name="7-creating-a-lunar-module-sample-application"></a>7. Création d’un exemple d’application de module lunaire

Dans ce didacticiel, nous combinons plusieurs concepts présentés dans les leçons précédentes pour créer un exemple d’expérience unique. Nous allons créer une application d’assembly de module lunaire dans laquelle un utilisateur doit utiliser des mains suivies pour capter les parties du module lunaire et tenter d’assembler un module lunaire. Nous utilisons des boutons permettant de basculer les indicateurs de placement, de réinitialiser notre expérience et de lancer notre module lunaire dans l’espace! Dans les prochains didacticiels, nous continuerons à développer cette expérience, qui comprend des cas d’utilisation multi-utilisateurs puissants qui tirent parti des ancres spatiales Azure pour l’alignement spatial.

## <a name="objectives"></a>Objectifs

- Combiner plusieurs concepts issus des leçons précédentes pour créer une même expérience
- Découvrir comment activer/désactiver des objets
- Déclencher des événements complexes en utilisant des boutons enfonçables
- Utiliser la physique et les forces des corps rigides
- Explorer l’utilisation d’info-bulles

## <a name="instructions"></a>Instructions

### <a name="configuring-the-lunar-module"></a>Configuration du module lunaire

Dans cette section, nous présentons les différents composants nécessaires pour créer notre exemple d’expérience.

1. Ajoutez l’assembly de module lunaire Prefab à votre scène de base. Pour ce faire, sous l’onglet projet, recherchez Rocket Launcher_Tutorial. 
Recherchez les Prefab dans Ressources-> BaseModuleAssets-> Prefabs. Vous verrez également deux prefabs de lanceur fusée. l’un portant le nom «Tutorial» et l’autre portant le nom «complete». Faites glisser le Prefab Rocket Launcher_Tutorial sur votre scène de base et positionnez-le comme vous le souhaitez.
   Remarque : Le Launcher_Complete Rocket Prefab est le lanceur terminé, fourni à des fins de référence. 

![Lesson6 Chapter1 Step1im](images/Lesson6_Chapter1_step1im.PNG)

Si vous développez l’objet de jeu Launcher_Tutorial Rocket dans votre hiérarchie et que vous développez davantage l’objet de module lunaire, vous trouvez plusieurs objets enfants qui ont un matériau appelé «x-ray». Le matériau «x-ray» autorise une couleur légèrement translucide que nous utiliserons comme indicateurs de placement pour l’utilisateur. 

![Lesson6 fichier chapter1 Noteaim](images/Lesson6_Chapter1_noteaim.PNG) il y a cinq parties au module lunaire avec lesquelles l’utilisateur interagit comme indiqué dans l’image ci-dessous:

1.  Le boîtier du rover (Rover Enclosure)
2.  Le réservoir de carburant (Fuel Tank)
3.  La batterie (Energy Cell)
4.  Le portail d’accueil (Docking Portal) 
5.  Le capteur externe (External sensor)

![Lesson6 Chapter1 Notebim](images/Lesson6_Chapter1_notebim.PNG)

> Remarque : Les noms d’objets de jeu que vous voyez dans votre hiérarchie de scène de base ne correspondent pas aux noms des objets dans la scène.

Étape 2 : Ajoutez une source audio au module lunaire. Assurez-vous que le module lunaire est sélectionné dans votre hiérarchie de scènes de base, puis cliquez sur Ajouter un composant. Recherchez source audio, puis ajoutez-le à l’objet. Laissez-le vide pour l’instant, mais veillez à activer la case à cocher «spatialiser» pour activer l’audio spatial. Nous allons l’utiliser plus tard pour jouer le son du lancement.

 ![Lesson6 fichier chapter1 Step2im](images/Lesson6_Chapter1_step2im.PNG)  
Étape 3 : Ajoutez le script, activez les indicateurs de positionnement. Cliquez sur Ajouter un composant, puis recherchez indicateurs de position de basculement. Il s’agit d’un script personnalisé qui vous permet d’activer et de désactiver les indicateurs translucides (objets avec les rayons x) mentionnés précédemment.  
![Lesson6 fichier chapter1 Step3im](images/Lesson6_Chapter1_step3im.PNG)  
Étape 4 : Étant donné que nous avons cinq objets, tapez «5» pour la taille du tableau d’objets de jeu. Vous verrez alors cinq nouveaux éléments s’affichent.  


![Lesson6 Chapter1 Step4bim](images/Lesson6_Chapter1_step4bim.PNG)

Faites glisser chacun des objets translucides dans toutes les zones Nom (Game Explorateur).
Faites glisser les objets suivants depuis le module lunaire dans votre scène de base : 

•   Backpack

•   GasTank

•   Topleftbody

•   Nose

•   LeftTwirler

 ![Lesson6 Chapter1 Step4aim](images/Lesson6_Chapter1_step4aim.PNG)

Le script activer/désactiver les indicateurs de positionnement est maintenant configuré. Cela nous permet d’activer et de désactiver les indicateurs.

Étape 5 : Ajoutez le script Launch lunaire module. Cliquez sur le bouton Ajouter un composant, recherchez «lancer le module lunaire», puis sélectionnez-le. Ce script lance le module lunaire. Quand vous appuyez sur un bouton configuré, il ajoute une force vers le haut au composant du corps rigide du module lunaire et provoque le lancement du module vers le haut. Si vous êtes à l’intérieur, le module lunaire peut se crasher sur le maillage de votre plafond. Mais si vous êtes à l’extérieur, il va voler indéfiniment dans l’espace. 

![Lesson6 Chapter1 Step5im](images/Lesson6_Chapter1_step5im.PNG)

Étape 6 : Ajustez la poussée afin que le module lunaire vole de façon fluide. Essayez une valeur de 0,01. Laissez le champ « Rb » vide. Rb signifie « rigid body » (corps rigide), et ce champ est renseigné automatiquement lors de l’exécution.

![Lesson6 Chapter1 Step6im](images/Lesson6_Chapter1_step6im.PNG)

### <a name="lunar-module-parts-overview"></a>Vue d’ensemble des parties du module lunaire
L’objet parent des composants de module lunaire est la collection des objets avec lesquels l’utilisateur interagit. Les noms des objets de jeu, avec les noms de scène libellés dans paretheses, sont fournis dans la liste ci-dessous:

- Backpack (Fuel Tank)
- GasTank (Energy Cell)
- TopLeftBody (Rover Enclosure)
- Nose (Docking Portal)
- LeftTwirler (External Sensor)

Notez que chacun de ces objets a un gestionnaire de manipulation comme indiqué dans la leçon 4. Avec le gestionnaire de manipulation, les utilisateurs peuvent saisir et manipuler l’objet. Notez également que le paramètre, deux types de manipulations de type droitier est défini sur déplacer et faire pivoter. Ceci permet seulement à l’utilisateur de déplacer l’objet mais pas de changer sa taille, ce qui est la fonctionnalité souhaitée pour une application d’assemblage.
En outre, la manipulation Far n’est pas vérifiée pour autoriser uniquement l’interaction directe des parties de module.

![Lesson6 Chapter2im](images/Lesson6_Chapter2im.PNG)

Le script de démonstration d’assembly d’un composant (illustré ci-dessus) est le script qui gère les objets que l’utilisateur place sur le module lunaire par l’utilisateur. 

Le champ objet à placer est la transformation qui est sélectionnée, comme illustré dans l’image ci-dessus, le sac à dos/réservoir de carburant associé à l’objet auquel il se connecte. 

Les paramètres distance à distance et distance déterminent la proximité des composants qui sont en place ou peuvent être libérés. Par exemple, le réservoir de sacs/carburants doit se trouver à 0,1 unités à l’extérieur du module lunaire pour pouvoir être placé en place. Le paramètre distance définit l’emplacement où l’objet peut être avant de se détacher du module lunaire. Dans ce cas, la main de l’utilisateur doit saisir le sac à dos/réservoir et le tire à une distance de 0,2 unités du module lunaire pour le retirer de l’emplacement d’insertion et le remettre en place.

L’info-bulle est l’étiquette de l’info-bulle dans la scène. Lorsque les objets sont alignés sur place, l’étiquette est désactivée. 

La source audio est automatiquement saisie. 

### <a name="placement-hints-buttons"></a>Boutons d’indicateurs de positionnement
Dans la [leçon 2](mrlearning-base-ch2.md), vous avez découvert comment placer et configurer des boutons pour faire des choses comme changer la couleur d’un élément ou lui faire jouer un son quand l’utilisateur l’enfonce. Nous allons continuer à utiliser ces principes pour configurer nos boutons permettant d’activer et de désactiver les indicateurs de placement. 

L’objectif est de configurer notre bouton afin que chaque fois que l’utilisateur appuie sur le bouton d’indication de placement, il active ou désactive la visibilité des indicateurs de placement translucides. 

Étape 1 : Déplacez le module lunaire vers l’emplacement vide du runtime uniquement dans le panneau Inspecteur, tandis que l’objet indicateur de positionnement est sélectionné dans votre hiérarchie de scènes de base. 
 ![Lesson6 Chapter3 Step1im](images/Lesson6_Chapter3_step1im.PNG) Étape 2 : Cliquez maintenant sur la liste déroulante aucune fonction. Accédez à TogglePlacementHints, puis sous ce menu, sélectionnez ToggleGameObjects (). ToggleGameObjects () active ou désactive les indicateurs de positionnement afin qu’ils soient visibles ou invisibles à chaque fois que le bouton est enfoncé.  
 ![Lesson6 Chapter3 Step2im](images/Lesson6_Chapter3_step2im.PNG)

### <a name="configuring-the-reset-button"></a>Configuration du bouton de réinitialisation

Il y aura des situations où l’utilisateur fait une erreur ou lève accidentellement l’objet, ou simplement souhaite réinitialiser l’expérience. Le bouton Réinitialiser permet de relancer l’expérience. 

Étape 1 : Sélectionnez le bouton Réinitialiser. Dans la scène de base, elle est nommée, ResetRoundButton. 

Étape 2 : Faites glisser le module lunaire de la hiérarchie de scènes de base vers l’emplacement vide sous le bouton en appuyant sur le panneau de l’inspecteur.
 ![Lesson6 Chapter4 Step2im](images/Lesson6_Chapter4_step2im.PNG)

Étape 3 : Sélectionnez le menu déroulant aucune fonction, puis pointez sur LaunchLunarModule, sélectionnez resetModule ().

![Lesson6 Chapter4 Step3im](images/Lesson6_Chapter4_step3im.PNG)

> Remarque : Notez que, par défaut, GameObject. BroadcastMessage est configuré sur ResetPlacement. Cela diffuse un message appelé, ResetPlacement pour chaque objet enfant du RocketLauncher_Tutorial. Tout objet ayant une méthode pour ResetPlacement () répond à ce message en réinitialisant sa position. 

### <a name="launching-the-lunar-module"></a>Lancement du module lunaire
Cette section explaings comment configurer le bouton lancer. Cela permet à l’utilisateur d’appuyer sur le bouton et de lancer le module lunaire dans l’espace.

Étape 1 : Sélectionnez le bouton lancer. Dans la scène de base, elle est appelée, LaunchRoundButton. Faites glisser le module lunaire dans l’emplacement vide sous Touch end dans le panneau de l’inspecteur.
 ![Lesson6 Chapter5 Step1im](images/Lesson6_Chapter5_step1im.PNG) Étape 2 : Sélectionnez le menu déroulant aucune fonction, pointez sur LaunchLunarModule, puis sélectionnez StopThruster (). Cela permet de contrôler le niveau de Poussée que l’utilisateur souhaite attribuer au module lunaire. 
 ![Lesson6 Chapter5 Step2im](images/Lesson6_Chapter5_step2im.PNG)  
Étape 3 : Sous ButtonPressed (), ajoutez le module lunaire (cliquez, maintenez-le enfoncé, puis faites-le glisser) vers l’emplacement vide. 

Étape 4 : Cliquez sur le menu déroulant aucune fonction, pointez sur LaunchLunarModule, puis sélectionnez StartThruster (). 
 ![Lesson6 Chapter5 Step4im](images/Lesson6_Chapter5_step4im.PNG)  
Étape 5 : Ajoutez de la musique au module lunaire pour que la musique soit lue lorsque la fusée est désactivée. Pour ce faire, faites glisser le module lunaire vers l’emplacement vide suivant sous le bouton enfoncé ().

Étape 6 : Sélectionnez le menu déroulant aucune fonction, pointez sur AudioSource, puis sélectionnez PlayOneShot (AudioClip). Vous pouvez explorer les différents sons fournis avec le MRTK. Pour cet exemple, nous allons utiliser «MRTK_Gem».
 ![Lesson6 Chapter5 Step6im](images/Lesson6_Chapter5_step6im.PNG)


### <a name="congratulations"></a>Félicitations 
Vous avez entièrement configuré cette application. Maintenant, lorsque vous appuyez sur lire, vous pouvez assembler complètement le module lunaire, activer/désactiver les indicateurs, lancer le module lunaire et le réinitialiser pour recommencer.
