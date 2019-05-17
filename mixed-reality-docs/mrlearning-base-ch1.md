---
title: Module de Base de formation de MR - l’initialisation de projets et de la première Application
description: Terminer ce cours pour apprendre à implémenter la reconnaissance faciale de Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, hololens (didacticiel), unity,
ms.openlocfilehash: c5490e6a3b542a5ca677b309e5ed1171f8666fe7
ms.sourcegitcommit: b5bad4eeb5cdd0c2a7b639442656c306e8b5853b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65814012"
---
# <a name="mr-learning-base-module---project-initialization-and-first-application"></a>Module de Base de formation de MR - l’initialisation de projets et de la première Application

Dans cette première leçon, vous apprendrez certaines des fonctionnalités de que la boîte à outils de réalité mixte peut vous offrir, démarrer votre première application pour HoloLens 2 et la déployer sur l’appareil.

## <a name="objectives"></a>Objectifs

* Optimiser Unity pour le développement de HoloLens.
* Importer les ressources et le programme d’installation de la scène.
* Visualisation de la maille spatiale, les mailles de main et le compteur de fréquence d’images.

## <a name="instructions"></a>Instructions

### <a name="create-new-unity-project"></a>Créer un projet Unity

1. Démarrez Unity.
2. Sélectionnez **New**.
![Leçon 1 Chapter1 Step2](images/Lesson1Chapter1Step2.JPG)
3. Entrez un nom de projet (par exemple) "MixedRealityBase").
![Leçon 1 Chapter1 Step3](images/Lesson1Chapter1Step3.JPG)
4. Entrez un emplacement pour enregistrer votre projet.
![Étape 4 de Chapter1 Lesson1](images/Lesson1Chapter1Step4.JPG)
5. Assurez-vous que le projet est défini sur **3D**.
![Étape 5 de Chapter1 Lesson1](images/Lesson1Chapter1Step5.JPG)
6. Cliquez sur **créer le projet**.
![Étape 6 de Chapter1 Lesson1](images/Lesson1Chapter1Step6.JPG)

### <a name="configure-the-unity-project-for-windows-mixed-reality"></a>Configurer le projet Unity pour Windows Mixed Reality

1. Ouvrez la fenêtre Paramètres de build en choisissant Fichier > Paramètres de Build.
![Leçon 1 chapitre4 Step1](images/Lesson1Chapter4Step1.JPG)
2. Basculez vers « Plateforme Windows universelle » en sélectionnant « Plateforme Windows universelle » et puis cliquez sur le bouton « Basculer la plateforme » pour changer de plate-forme. Applications qui s’exécutent sur HoloLens 2 doivent être Universal Windows Platform (UWP).
![Leçon 1 chapitre4 Step2](images/Lesson1Chapter4Step2.JPG)
3. Activer la réalité virtuelle en cliquant sur Paramètres du lecteur dans la fenêtre de génération et puis, dans le panneau Inspecteur activer la case à cocher « Virtuel réalité pris en charge », sous Paramètres XR, comme indiqué dans l’image ci-dessous. Veuillez noter que vous devrez peut-être faire glisser disparaître la fenêtre de « Paramètres de Build » pour afficher le panneau de l’inspecteur. La case à cocher « Virtuel réalité pris en charge » s’applique également à la réalité mixte / les casques AR, car il fait référence à l’activation de la vision stéréoscopique (rendu images différentes pour chaque œil.) ![Leçon 1 chapitre4 Step3](images/Lesson1Chapter4Step3.JPG)
4. Dans le même panneau d’inspecteur, vérifiez que la case à cocher « Perception spatiale » dans la section fonctionnalités est activé, sous paramètres de publication. Perception spatiale nous permettra de visualiser la maille de mappage spatial sur un appareil de réalité mixte tels que les 2 HoloLens. Paramètres de publication sont trouvent dans le panneau d’inspecteur, « Paramètres XR » ci-dessus et sous « Autres paramètres ».
![Étape 4 de chapitre4 leçon 1](images/Lesson1Chapter4Step4.JPG)

> REMARQUE : Bien que ne pas utilisé dans cette section, certaines autres fonctionnalités courantes, il pouvez que vous souhaitez activer incluent Microphone (pour les commandes vocales) et InternetClient (pour la connexion aux services qui requièrent une connexion réseau)

### <a name="import-the-mixed-reality-toolkit"></a>Importation du Kit de ressources de réalité mixte

1. Téléchargez le [Toolkit de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC1.unitypackage) unity empaqueter et enregistrez-la dans un dossier sur votre PC.

2. Importer le package du Kit de ressources de réalité mixte en cliquant sur les ressources > Importer > Package personnalisé. Trouver le package du Kit de ressources de réalité mixte téléchargé à l’étape 1 et l’ouvrir pour commencer le processus d’importation. Patientez quelques minutes pour le processus d’importation.
    ![Leçon 1 Chapter2 Step2a](images/Lesson1Chapter2Step2a.JPG) ![Lesson1 Chapter2 Step2b](images/Lesson1Chapter2Step2b.JPG)

3. Dans la fenêtre contextuelle suivante, cliquez sur « Importer » pour commencer l’importation de la boîte à outils de réalité mixte. Vérifiez tous les éléments sont activés, comme illustré dans l’image. Si vous voyez une boîte de dialogue contextuelle demandant à appliquer les paramètres par défaut de boîte à outils de réalité mixte, cliquez sur « Appliquer ».
    ![Leçon 1 Chapter2 Step3](images/Lesson1Chapter2Step3.JPG) ![Lesson1 Chapter2 Step3](images/Lesson1Chapter2Step3b.JPG)

### <a name="configure-the-mixed-reality-toolkit"></a>Configurer le Kit de ressources de réalité mixte

1. Configurer le Kit de ressources mixte en sélectionnant dans le menu de barre de boîte à outils de réalité mixte > configurer. Si vous ne voyez pas cet élément de menu après l’importation du Kit de ressources de réalité mixte, veuillez redémarrer Unity.
![Leçon 1 chapitre3 Step1](images/Lesson1Chapter3Step1.JPG)
2. Votre scène aura maintenant plusieurs nouveaux éléments et les modifications qu’il contient à partir de la boîte à outils de réalité mixte. Enregistrez votre scène sous un autre nom en cliquant sur fichier > Enregistrer sous et donnez un nom, par exemple, BaseScene à votre scène. Gardez votre scène organisée en les enregistrant dans le dossier « En coulisses » dans le dossier de ressources de votre projet.
![Leçon 1 chapitre3 Step2a](images/Lesson1Chapter3Step2a.JPG)
![Lesson1 chapitre3 Step2b](images/Lesson1Chapter3Step2b.JPG)

### <a name="build-your-application-to-your-device"></a>Générez votre application pour votre appareil

1. Si vous avez fermé la fenêtre Paramètres de génération des sections précédentes, rouvrez la fenêtre de paramètres de build en choisissant Fichier > Paramètres de Build.
    ![Leçon 1 Chapter5 Step1](images/Lesson1Chapter5Step1.JPG)

2. Vérifiez que la scène que vous souhaitez essayer figure dans la liste « Scènes dans la Build » en cliquant sur le bouton « Ajouter un arrière-plan Open ».

3. Appuyez sur le bouton Générer pour commencer le processus de génération.
    ![Leçon 1 Chapter5 Step3](images/Lesson1Chapter5Step3.JPG)

4. Créez et nommez un nouveau dossier pour votre application. Dans l’image ci-dessous, un dossier portant le nom « Application » a été créée pour contenir l’application. Cliquez sur « Sélectionner le dossier » pour commencer à créer dans le dossier nouvellement créé. Une fois la build terminée, vous pouvez fermer la fenêtre « Paramètres de Build » dans Unity. 
    ![Étape 4 de Chapter5 Lesson1](images/Lesson1Chapter5Step4.JPG)

  > REMARQUE : Si la build échoue, tentez une génération à nouveau ou redémarrer Unity et créer à nouveau. Si vous voyez une erreur comme « erreur : CS0246 = le nom du type ou espace de noms « XX » est introuvable (ne manque-t-il pas une à l’aide de la directive ou une référence d’assembly ?) », puis vous devrez peut-être installer [SDK Windows 10 (10.0.18362.0)](<https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk>)
  >

5. Une fois la build terminée, ouvrez le dossier nouvellement créé qui contient vos fichiers d’application nouvellement créée. Double-cliquez sur la solution « MixedRealityBase.sln » (ou le nom correspondant, si vous avez utilisé un autre nom pour votre projet) pour ouvrir le fichier de solution dans Visual Studio.

  > Remarque: Veillez à ouvrir le dossier nouvellement créé (par exemple, le « Application » dossier, si suit les conventions d’affectation de noms des étapes précédentes), comme il y aura un fichier .sln portant le même nom en dehors de ce dossier ne doit ne pas être confondue avec le fichier .sln dans le dossier de génération. 

![Étape 5 de Chapter5 Lesson1](images/Lesson1Chapter5Step5.JPG)

  > Remarque: Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants requis sont installés comme spécifié dans [la page « Installer les outils »](install-the-tools.md)

6. Branchez votre 2 HoloLens sur votre PC avec le câble USB. Ces instructions de la leçon suppose que vous déployez un test avec un appareil HoloLens 2, vous pouvez également choisir de déployer à la [HoloLens 2 émulateur](using-the-hololens-emulator.md) ou choisissez de créer un [package d’application pour le chargement de version test](<https://docs.microsoft.com/en-us/windows/uwp/packaging/packaging-uwp-apps>)

7. Avant la génération de votre appareil, vérifiez que l’appareil est en Mode développeur. S’il s’agit de votre premier déploiement sur le 2 HoloLens, Visual Studio peut vous demander d’associer votre 2 HoloLens avec un code confidentiel. Veuillez suivre [ces instructions](https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio) si vous devez activer le mode développeur ou couplé à Visual Studio.

8. Configurer Visual Studio pour la création de votre 2 HoloLens en sélectionnant la configuration « Release » et l’architecture « ARM ».
    ![Leçon 1 Chapter5 Step8](images/Lesson1Chapter5Step8.JPG)

9. L’étape finale consiste à créer pour votre appareil en sélectionnant le débogage > Démarrer sans débogage. La sélection de « Démarrer sans débogage » entraîne l’application à démarrer immédiatement sur votre appareil sur une build réussie, mais sans les informations de débogage qui apparaissent dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre 2 HoloLens sans arrêter l’application. Vous pouvez également sélectionner la Build > déployer la Solution pour déployer sur votre appareil sans avoir à l’application de démarrer automatiquement.
    ![Leçon 1 Chapter5 Step9](images/Lesson1Chapter5Step9.JPG)

## <a name="congratulations"></a>Félicitations !

Vous avez déployé votre première application HoloLens 2 maintenant. Comme vous le déplacer, vous devez voir une maille spatiale couvrent toutes les surfaces qui ont été perçues par la version 2 HoloLens. En outre, vous devez voir des indicateurs sur vos mains et les doigts pour la main de suivi et un compteur de taux de trames pour vous tenir informé sur les performances de l’application. Voici quelques éléments fondamentaux, incluses dès le départ, avec le Kit de ressources de réalité mixte. Au cours des leçons à venir, vous commencerez à ajouter plus de contenu et de l’interactivité à votre scène, vous pouvez explorer pleinement les capacités de la version 2 HoloLens et le Kit de ressources de réalité mixte.

>Remarque: Décrivez comment afficher/masquer le compteur de taux de trame à l’aide d’une commande vocale dans [leçon 5](mrlearning-base-ch5.md)

[Leçon suivante : Interface utilisateur, main suivi et mixte de Configuration du Kit de ressources réalité](mrlearning-base-ch2.md)
