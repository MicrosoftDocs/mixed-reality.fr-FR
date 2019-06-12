---
title: Module d’apprentissage de base sur la réalité mixte - Initialisation du projet et première application
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: c5490e6a3b542a5ca677b309e5ed1171f8666fe7
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "65814012"
---
# <a name="mr-learning-base-module---project-initialization-and-first-application"></a>Module d’apprentissage de base sur la réalité mixte - Initialisation du projet et première application

Dans cette première leçon, vous allez apprendre certaines des fonctionnalités qu’offre le Kit de ressources de réalité mixte, démarrer votre première application pour HoloLens 2 et la déployer sur l’appareil.

## <a name="objectives"></a>Objectifs

* Optimiser Unity pour le développement HoloLens.
* Importer les ressources et configurer la scène.
* Visualiser le maillage spatial, les maillages de la main et le compteur de fréquence d’images.

## <a name="instructions"></a>Instructions

### <a name="create-new-unity-project"></a>Créer un projet Unity

1. Démarrez Unity.
2. Sélectionnez **New**.
![Leçon 1 Chapitre 1 Étape 2](images/Lesson1Chapter1Step2.JPG)
3. Entrez un nom de projet (par exemple, « MixedRealityBase »).
![Leçon 1 Chapitre 1 Étape 3](images/Lesson1Chapter1Step3.JPG)
4. Entrez un emplacement auquel enregistrer votre projet.
![Leçon 1 Chapitre 1 Étape 4](images/Lesson1Chapter1Step4.JPG)
5. Vérifiez que le projet est défini sur **3D**.
![Leçon 1 Chapitre 1 Étape 5](images/Lesson1Chapter1Step5.JPG)
6. Cliquez sur **Create Project**.
![Leçon 1 Chapitre 1 Étape 6](images/Lesson1Chapter1Step6.JPG)

### <a name="configure-the-unity-project-for-windows-mixed-reality"></a>Configurer le projet Unity pour Windows Mixed Reality

1. Ouvrez la fenêtre Build Settings (Paramètres de génération) en choisissant File>Build Settings.
![Leçon 1 Chapitre 4 Étape 1](images/Lesson1Chapter4Step1.JPG)
2. Basculez vers « Plateforme Windows universelle » en sélectionnant « Universal Windows Platform », puis en cliquant sur le bouton « Switch Platform » (Changer de plateforme). Les applications qui s’exécutent sur HoloLens 2 doivent être de type UWP (plateforme Windows universelle).
![Leçon 1 Chapitre 4 Étape 2](images/Lesson1Chapter4Step2.JPG)
3. Activez la réalité virtuelle en cliquant sur Player Settings (Paramètres du lecteur) dans la fenêtre Build (Générer) puis, dans le panneau de l’inspecteur, cochez la case « Virtual Reality Supported » (Prise en charge de la réalité virtuelle), sous XR Settings (Paramètres XR), comme indiqué dans l’image ci-dessous. Veuillez noter que vous devrez peut-être faire glisser la fenêtre « Build Settings » pour voir le panneau de l’inspecteur. La case à cocher « Virtual Reality Supported » s’applique également aux casques de réalité mixte/réalité augmentée, car elle fait référence à l’activation de la vision stéréoscopique (rendu d’images différentes pour chaque œil). ![Leçon 1 Chapitre 4 Étape 3](images/Lesson1Chapter4Step3.JPG)
4. Dans le même panneau de l’inspecteur, sous Publishing Settings (Paramètres de publication), dans la section des fonctionnalités, vérifiez que la case « Spatial Perception » (Perception spatiale) est cochée. La perception spatiale nous permettra de visualiser le maillage du mappage spatial sur un appareil de réalité mixte tel que HoloLens 2. Les paramètres de publication se trouvent dans le panneau Inspector, au-dessus de « XR Settings » et sous « Other Settings » (Autres paramètres).
![Leçon 1 Chapitre 4 Étape 4](images/Lesson1Chapter4Step4.JPG)

> REMARQUE : Bien qu’elles ne soient pas utilisées dans cette section, certaines autres fonctionnalités courantes que vous pouvez être amené à activer incluent Microphone (pour les commandes vocales) et InternetClient (pour la connexion aux services qui requièrent une connexion réseau).

### <a name="import-the-mixed-reality-toolkit"></a>Importer le Kit de ressources de réalité mixte

1. Téléchargez le package Unity du [Kit de ressources de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC1.unitypackage) et enregistrez-le dans un dossier sur votre PC.

2. Importez le package du Kit de ressources de réalité mixte en cliquant sur Assets (Ressources)> Import > Custom Package (Package personnalisé). Recherchez le package du Kit de ressources de réalité mixte téléchargé à l’étape 1 et ouvrez-le pour commencer le processus d’importation. Patientez quelques minutes, le temps que le processus d’importation se termine.
    ![Leçon 1 Chapitre 2 Étape 2a](images/Lesson1Chapter2Step2a.JPG) ![Leçon 1 Chapitre 2 Étape 2b](images/Lesson1Chapter2Step2b.JPG)

3. Dans la fenêtre contextuelle suivante, cliquez sur « Import » pour commencer l’importation du Kit de ressources de réalité mixte. Vérifiez que tous les éléments sont cochés, comme illustré dans l’image. Si apparaît une boîte de dialogue contextuelle demandant s’il faut appliquer les paramètres par défaut du Kit de ressources de réalité mixte, cliquez sur « Apply ».
    ![Leçon 1 Chapitre 2 Étape 3](images/Lesson1Chapter2Step3.JPG) ![Leçon 1 Chapitre 2 Étape 3](images/Lesson1Chapter2Step3b.JPG)

### <a name="configure-the-mixed-reality-toolkit"></a>Configurer le Kit de ressources de réalité mixte

1. Configurez le Kit de ressources de réalité mixte en sélectionnant dans la barre de menus Mixed Reality Toolkit > Configure. Si vous ne voyez pas cet élément de menu après avoir importé le Kit de ressources de réalité mixte, redémarrez Unity.
![Leçon 1 Chapitre 3 Étape 1](images/Lesson1Chapter3Step1.JPG)
2. Votre scène contient maintenant plusieurs nouveaux éléments et modifications issus du Kit de ressources de réalité mixte. Enregistrez votre scène sous un autre nom en cliquant sur File>Save As (Fichier > Enregistrer sous) et donnez un nom à votre scène, par exemple BaseScene. Dans un souci d’organisation, enregistrez la scène dans le dossier « Scenes » du dossier Assets (Ressources) de votre projet.
![Leçon 1 Chapitre 3 Étape2a](images/Lesson1Chapter3Step2a.JPG)
![Leçon 1 Chapitre 3 Étape2b](images/Lesson1Chapter3Step2b.JPG)

### <a name="build-your-application-to-your-device"></a>Générer votre application sur votre appareil

1. Si vous avez fermé la fenêtre Build Settings dans les sections précédentes, rouvrez-la en choisissant File>Build Settings.
    ![Leçon 1 Chapitre 5 Étape 1](images/Lesson1Chapter5Step1.JPG)

2. Vérifiez que la scène que vous souhaitez essayer figure dans la liste « Scenes in Build » (Scènes dans la génération) en cliquant sur le bouton « Add Open Scenes » (Ajouter des scènes ouvertes).

3. Appuyez sur le bouton Build (Générer) pour commencer le processus de génération.
    ![Leçon 1 Chapitre 5 Étape 3](images/Lesson1Chapter5Step3.JPG)

4. Créez un dossier pour votre application et nommez-le. Dans l’image ci-dessous, un dossier portant le nom « App » a été créé pour contenir l’application. Cliquez sur « Select Folder » (Sélectionner le dossier) pour commencer la génération dans le dossier que vous venez de créer. Une fois la génération terminée, vous pouvez fermer la fenêtre « Build Settings » dans Unity. 
    ![Leçon 1 Chapitre 5 Étape 4](images/Lesson1Chapter5Step4.JPG)

  > REMARQUE : Si la génération échoue, essayez de renouveler l’opération, éventuellement après avoir redémarré Unity. Si vous voyez une erreur comme « Error : CS0246 = The type or namespace name “XX” could not be found (are you missing a using directive or an assembly reference?) » (CS0246 = le type ou le nom de l’espace de noms « XX » est introuvable (une directive using ou une référence d’assembly est-elle manquante ?) », vous devrez peut-être installer [SDK Windows 10 (10.0.18362.0)](<https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk>)
  >

5. Une fois la génération terminée, ouvrez le dossier créé qui contient vos fichiers d’application nouvellement générés. Double-cliquez sur la solution « MixedRealityBase.sln » (ou le nom correspondant, si vous avez utilisé un autre nom pour votre projet) pour ouvrir le fichier solution dans Visual Studio.

  > Remarque: Veillez à ouvrir le dossier créé (par exemple, le dossier « App », si vous avez suivi les conventions de nommage indiquées aux étapes précédentes), car il existe un fichier .sln portant le même nom en dehors de ce dossier qui ne doit pas être confondu avec le fichier .sln situé dans le dossier de génération. 

![Leçon 1 Chapitre 5 Étape 5](images/Lesson1Chapter5Step5.JPG)

  > Remarque: Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants requis sont installés comme spécifié dans la [page « Installer les outils »](install-the-tools.md).

6. Branchez l’appareil HoloLens 2 à votre PC avec le câble USB. Bien que les instructions de cette leçon supposent que vous déployez un test avec un appareil HoloLens 2, vous pouvez choisir d’effectuer le déploiement sur l’[émulateur HoloLens 2](using-the-hololens-emulator.md) ou de créer un [package d’application pour effectuer un chargement indépendant](<https://docs.microsoft.com/en-us/windows/uwp/packaging/packaging-uwp-apps>).

7. Avant d’effectuer la génération sur votre appareil, vérifiez que ce dernier est en mode développeur. S’il s’agit de votre premier déploiement sur l’appareil HoloLens 2, Visual Studio peut vous demander de l’associer à un code confidentiel. Veuillez suivre [ces instructions](https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio) si vous devez activer le mode développeur ou associer l’appareil à Visual Studio.

8. Configurez Visual Studio en vue d’effectuer la génération sur votre appareil HoloLens 2 en sélectionnant la configuration « Release » et l’architecture « ARM ».
    ![Leçon 1 Chapitre 5 Étape 8](images/Lesson1Chapter5Step8.JPG)

9. L’étape finale consiste à effectuer la génération sur votre appareil en sélectionnant Déboguer > Démarrer sans débogage. Quand vous sélectionnez « Démarrer sans débogage », l’application démarre immédiatement sur votre appareil si la génération réussit, mais les informations de débogage n’apparaissent pas dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci. Vous pouvez également sélectionner Générer > Déployer la solution pour effectuer le déploiement sur votre appareil sans que l’application démarre automatiquement.
    ![Leçon 1 Chapitre 5 Étape 9](images/Lesson1Chapter5Step9.JPG)

## <a name="congratulations"></a>Félicitations

Vous venez de déployer votre première application HoloLens 2. À mesure que vous vous déplacez, vous devez voir un maillage spatial couvrir toutes les surfaces qui ont été perçues par l’appareil HoloLens 2. En outre, vous devez voir des indicateurs sur vos mains et doigts pour le suivi de la main et un compteur de fréquence d’images pour vous tenir informé des performances de l’application. Ce ne sont là que quelques-uns des éléments fondamentaux immédiatement disponibles dans le Kit de ressources de réalité mixte. Au cours des leçons à venir, vous commencerez à ajouter du contenu et une interactivité à votre scène afin de pouvoir explorer pleinement les fonctionnalités de l’appareil HoloLens 2 et du Kit de ressources de réalité mixte.

>Remarque: Vous découvrirez comment afficher/masquer le compteur de fréquence d’images à l’aide d’une commande vocale dans la [Leçon 5](mrlearning-base-ch5.md).

[Leçon suivante : Interface utilisateur, suivi manuel et configuration du Kit de ressources de réalité mixte](mrlearning-base-ch2.md)
