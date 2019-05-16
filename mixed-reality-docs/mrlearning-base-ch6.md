---
title: Module MR Learning Base - lunaire Module Assembly exemple expérience
description: Dans cette leçon, nous combinera plusieurs concepts appris à partir des leçons précédentes pour créer une expérience unique d’exemple.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, hololens (didacticiel), unity,
ms.openlocfilehash: 8a2f388e842d521f991203916177e3dac15769eb
ms.sourcegitcommit: 1c0fbee8fa887525af6ed92174edc42c05b25f90
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65730846"
---
# <a name="mr-learning-base-module---lunar-module-assembly-sample-experience"></a>Module MR Learning Base - lunaire Module Assembly exemple expérience

Dans cette leçon, nous combinera plusieurs concepts appris à partir des leçons précédentes pour créer une expérience unique d’exemple. Nous allons créer une application d’assembly lunaire module par laquelle un utilisateur devra utiliser mains suivies à assimiler les parties lunaire module et tentez d’assembler un module lunaire. Nous allons utiliser les boutons PRESSEE pour activer/désactiver les indicateurs de sélection élective, à notre expérience de réinitialisation et pour lancer notre module lunaire dans l’espace ! Dans les futures didacticiels, nous continuerons à s’appuient sur cette expérience, y compris les puissants multi-utilisateur-cas d’usage qui tire parti des ancres Spatial Azure pour l’alignement spatiale.

## <a name="objectives"></a>Objectifs

- Combiner plusieurs concepts issus des leçons précédentes pour créer une expérience unique
- Découvrez comment activer/désactiver les objets
- Déclencher des événements complexes à l’aide des boutons PRESSEE
- Utilisez rigidbody physique et force
- Explorer l’utilisation d’info-bulles

## <a name="instructions"></a>Instructions

### <a name="configuring-the-lunar-module"></a>Configuration du Module lunaire

Dans ce chapitre, nous présentera les divers composants nécessaires pour créer notre expérience de l’exemple.

1. Ajoutez le préfabriqué assembly lunaire module à votre scène de Base. Pour ce faire, dans l’onglet de votre projet, recherchez « Launcher_Tutorial de fusée ». Vous pouvez également trouver le préfabriqué actifs > BaseModuleAssets > Prefabs. Vous pouvez voir deux prefabs de Lanceur de fusée ; un avec le nom « didacticiel » et l’autre avec le nom « terminent ». Faites glisser le préfabriqué « Rocket Launcher_Tutorial » à votre scène de Base. N’hésitez pas à positionner le placement de la préfabriqué dans votre scène.
   Remarque: Le préfabriqué « Rocket Launcher_Complete » est le Lanceur terminé, fourni à titre de référence. 

![Lesson6 Chapter1 Step1im](images/Lesson6_Chapter1_step1im.PNG)

Si vous développez l’objet de jeu de « Rocket Launcher_Tutorial » dans votre hiérarchie et développez davantage l’objet « Module lunaire », vous verrez plusieurs objets enfants qui ont un matériau appelé « radio ». Le matériel de « radio » permet une couleur légèrement translucide que nous allons utiliser en tant qu’indicateurs de sélection élective de l’utilisateur. 

![Lesson6 Chapter1 Noteaim](images/Lesson6_Chapter1_noteaim.PNG) il existe cinq parties au module lunaire que l’utilisateur va interagir, comme illustré dans l’image ci-dessous :

1.  Le boîtier du robot sur
2.  Le réservoir de carburant
3.  La cellule d’énergie
4.  Le portail d’accueil 
5.  Le capteur externe

![Lesson6 Chapter1 Notebim](images/Lesson6_Chapter1_notebim.PNG)

> Remarque: Les noms d’objet de jeu que vous voyez dans votre hiérarchie de la scène de base ne correspondent pas aux noms des objets dans la scène.

Étape 2 : Ajouter une source audio au module lunaire. Assurez-vous que le module lunaire est sélectionné dans votre hiérarchie de la scène de base et cliquez sur « Ajouter un composant ». Recherchez « Audio Source » et l’ajouter à l’objet. Laissez vide pour l’instant. Nous l’utiliserons pour lire le son lancement ultérieurement.
 ![Lesson6 Chapter1 Step2im](images/Lesson6_Chapter1_step2im.PNG) étape 3 : Ajoutez le script « activer/désactiver des indicateurs de sélection élective ». Cliquez sur « Ajouter un composant » et recherchez « Activer/désactiver des indicateurs de sélection élective ». Il s’agit d’un script personnalisé qui permet d’activer et désactiver les indicateurs translucides (objets avec le matériel de rayons x), mentionnés précédemment. 
![Lesson6 Chapter1 Step3im](images/Lesson6_Chapter1_step3im.PNG) étape 4 : Étant donné que nous avons 5 objets, tapez « 5 » pour la taille du tableau objet de jeu. Vous ne devriez voir 5 nouveaux éléments apparaissent. 

![Lesson6 Chapter1 Step4bim](images/Lesson6_Chapter1_step4bim.PNG)

Faites glisser chacun des objets translucides dans les zones qui indiquent « Aucun (objet de jeu). » Faites glisser les objets suivants à partir du module lunaire dans votre scène base : 

• Sac à DOS

•   GasTank

• Topleftbody

• Nez

•   LeftTwirler

 ![Lesson6 Chapter1 Step4aim](images/Lesson6_Chapter1_step4aim.PNG)

Le script « activer/désactiver les indicateurs de sélection élective » est maintenant configuré. Cela nous permettra à activer et désactiver la les indicateurs.

Étape 5 : Ajoutez le script « lancement lunaire module ». Cliquez sur le bouton « Ajouter un composant », recherchez « lancement lunaire module » et sélectionnez-le. Ce script sera chargé de lancer le module lunaire. Lorsque vous appuyez sur un bouton configuré, il ajoutera une force vers le haut au composant de corps rigide du module lunaire et entraîne le module lancer vers le haut. Si vous êtes à l’intérieur, le module lunaire peut se bloquer sur votre maillage plafond. Mais si vous êtes extérieur, il traverse dans espace indéfiniment. 

![Lesson6 Chapter1 Step5im](images/Lesson6_Chapter1_step5im.PNG)

Étape 6 : Ajustez la poussée afin que le module lunaire traverse des normalement. Essayez une valeur de 0,01. Laissez le champ « Rb » vide. RB signifie corps rigide, et ce champ est renseigné automatiquement lors de l’exécution.

![Lesson6 Chapter1 Step6im](images/Lesson6_Chapter1_step6im.PNG)

### <a name="lunar-module-parts-overview"></a>Vue d’ensemble des parties lunaire Module
L’objet parent de parties lunaire Module est la collection d’objets qui interagit avec l’utilisateur. Les noms d’objet de jeu (avec scène étiqueté noms dans paretheses) sont fournis dans la liste ci-dessous :

- Sac à DOS (réservoir)
- GasTank (cellule énergie)
- TopLeftBody (boîtier du robot sur)
- Nez (portail d’accueil)
- LeftTwirler (capteur externe)

Notez que chacun de ces objets le Gestionnaire de manipulation, comme indiqué dans la leçon 4. Avec le Gestionnaire de manipulation, les utilisateurs sont en mesure de récupérer et manipuler l’objet. Notez également que le paramètre « type de manipulation transmis deux » est défini à « déplacer et faire pivoter ». Cela autorise uniquement l’utilisateur de déplacer l’objet et ne modifie pas sa taille, c'est-à-dire les fonctionnalités souhaitées pour une application de l’assembly.
En outre, la manipulation lointain est désactivée pour autoriser uniquement l’interaction directe des parties de module.

![Lesson6 Chapter2im](images/Lesson6_Chapter2im.PNG)

Le script de démonstration d’assembly partie (illustré ci-dessus) est le script qui gère les objets à placer sur le module lunaire par l’utilisateur. 

Le champ « Objet à la Place » est la transformation qui est sélectionné (n le cas de l’image ci-dessus, le sac à DOS/réservoir) avec l’objet qu’il peut se connecter à. 

Les paramètres « Près de Distance » et « Distance beaucoup » sont chargés de déterminer la proximité à laquelle les parties seront aligne en place ou libérées. Par exemple, le sac à DOS/réservoir doit être 0,1 unité en dehors du module lunaire en place. Le « présent Distance » définit l’emplacement où l’objet doit être pour dissocier le module lunaire. Dans ce cas, main de l’utilisateur doit saisir le sac à DOS/réservoir et tirez-la 0,2 unités en dehors du module lunaire pour le supprimer de l’alignement arrière en place.

L’objet « info-bulle de l’outil » est l’étiquette d’info-bulle outil dans la scène. Lorsque les objets sont alignées en place, l’étiquette sera désactivé. 

La Source Audio sera automatiquement être saisie. 

### <a name="placement-hints-buttons"></a>Boutons d’indicateurs de sélection élective
Dans [leçon 2](mrlearning-base-ch2.md), vous avez appris comment placer et configurer les boutons pour effectuer des opérations comme modifier la couleur d’un élément ou en faire un signal sonore lorsqu’elle est poussée. Nous allons continuer à utiliser ces principes lorsque nous configurons nos boutons pour activer/désactiver les indicateurs de sélection élective. 

L’objectif consiste à configurer notre bouton afin que chaque fois que l’utilisateur appuie sur le bouton d’indicateur de sélection élective, il sera afficher ou masquer les indicateurs de sélection élective translucide. 

Étape 1 : Déplacer le Module lunaire vers l’emplacement vide « runtime » uniquement dans le panneau Inspecteur pendant que l’objet d’indicateurs de sélection élective est sélectionné dans votre hiérarchie de la scène de base. 
 ![Lesson6 chapitre3 Step1im](images/Lesson6_Chapter3_step1im.PNG) étape 2 : Cliquez maintenant sur la liste déroulante n’intitulée, « aucune fonction ». Accédez à « TogglePlacementHints » et sous ce menu Sélectionner « ToggleGameObjects (). » ToggleGameObjects() activer les indicateurs de sélection élective et désactiver afin qu’ils soient visible ou invisible chaque fois que le bouton est enfoncé.
 ![Lesson6 chapitre3 Step2im](images/Lesson6_Chapter3_step2im.PNG)

### <a name="configuring-the-reset-button"></a>Configurer le bouton de réinitialisation

Il y aura des situations où l’utilisateur fait une erreur ou accidentellement lève que l’objet de suite, ou simplement souhaite rest l’expérience. Le bouton de réinitialisation ajoutera la possibilité de redémarrer l’expérience. 

Étape 1 : Sélectionnez le bouton de réinitialisation. Dans la scène de base, il est nommé « ResetRoundButton ». 

Étape 2 : Faites glisser le module lunaire à partir de la hiérarchie de la scène de base dans l’emplacement vide sous « bouton enfoncé » du Panneau de l’inspecteur.
 ![Lesson6 chapitre4 Step2im](images/Lesson6_Chapter4_step2im.PNG)

Étape 3 : Sélectionnez le menu déroulant qui est affiché le message « aucune fonction » et placez le curseur sur « LaunchLunarModule ». Sélectionnez maintenant « resetModule (). »

![Lesson6 chapitre4 Step3im](images/Lesson6_Chapter4_step3im.PNG)

> Remarque: Vous remarquerez que, par défaut, le « GameObject.BroadcastMessage » est configuré pour « ResetPlacement ». Cela va diffuser un message appelé « ResetPlacement » pour tous les objets enfants de RocketLauncher_Tutorial. N’importe quel objet qui a une méthode pour « ResetPlacement() » répond à ce message en redéfinissant sa position. 

### <a name="launching-the-lunar-module"></a>Lancement du Module lunaire
Ce chapitre, nous allons configurer le bouton de lancement. Cela autorise l’utilisateur à appuyer sur le bouton et lancer le Module lunaire dans l’espace.

Étape 1 : Sélectionnez le bouton de lancement (dans la scène de base est intitulée « LaunchRoundButton »). Faites glisser le Module de lunaire vers l’emplacement vide sous « End Touch » dans le panneau de l’inspecteur.
 ![Lesson6 Chapter5 Step1im](images/Lesson6_Chapter5_step1im.PNG) étape 2 : Sélectionnez le menu déroulant qui est affiché le message « aucune fonction ». Placez le curseur sur « LaunchLunarModule » et sélectionnez « StopThruster (). » Cette option détermine la quantité poussée de l’utilisateur veut donner au Module lunaire. 
 ![Lesson6 Chapter5 Step2im](images/Lesson6_Chapter5_step2im.PNG) étape 3 : Sous « ButtonPressed() », ajoutez le Module de lunaire (clic, maintenez et faites glisser) à l’emplacement vide. 

Étape 4 : Cliquez sur le menu déroulant qui est affiché le message « aucune fonction » et placez le curseur sur « LaunchLunarModule » et sélectionnez « StartThruster (). » 
 ![Lesson6 Chapter5 Step4im](images/Lesson6_Chapter5_step4im.PNG) étape 5 : Ajoutez de la musique au Module lunaire afin que lorsque le rocket décolle, la musique sera lu. Pour ce faire, faites glisser le Module lunaire à l’emplacement vide suivante sous « Bouton Pressed() ».

Étape 6 : Sélectionnez le menu déroulant qui est affiché le message « aucune fonction » et placez le curseur sur « AudioSource » puis « PlayOneShot (AudioClip) ». N’hésitez pas à découvrir la variété de sons inclus avec le MRTK. Pour cet exemple, nous allons se cantonner à « MRTK_Gem ».
 ![Lesson6 Chapter5 Step6im](images/Lesson6_Chapter5_step6im.PNG)


### <a name="congratulations"></a>Félicitations ! 
Vous avez entièrement configuré cette application ! Maintenant lorsque vous appuyez sur play, vous pouvez entièrement assembler le Module lunaire, activer/désactiver les indicateurs, lancez le Module lunaire et réinitialisez-le refaire tout.
