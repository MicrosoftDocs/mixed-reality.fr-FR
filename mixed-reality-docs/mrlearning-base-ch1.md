---
title: Module d’apprentissage de base sur la réalité mixte - Initialisation du projet et première application
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: e79c3ea719a71d6df8ffd9e2be009d14a846a16a
ms.sourcegitcommit: b086d7a62ee0c7913aa8f66c90e9d2527f270264
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68485723"
---
# <a name="2-initializing-your-project-and-first-application"></a>2. Initialisation de votre projet et de la première application

Dans cette première leçon, vous découvrirez certaines des fonctionnalités que le MRTK (Mixed Reality Toolkit) doit offrir, commencez votre première application pour HoloLens 2 et déployez-la sur l’appareil.

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

1. Ouvrez la fenêtre Paramètres de build en accédant à fichier > paramètres de Build.
![Leçon 1 Chapitre 4 Étape 1](images/Lesson1Chapter4Step1.JPG)
2. Basculez vers plateforme Windows universelle en sélectionnant plateforme Windows universelle. Cliquez sur le bouton changer de plateforme pour basculer entre les plateformes. Les applications qui s’exécutent sur HoloLens 2 doivent être compatibles plateforme Windows universelle (UWP).
![Leçon 1 Chapitre 4 Étape 2](images/Lesson1Chapter4Step2.JPG)
3. Activez la réalité virtuelle en cliquant sur paramètres du lecteur dans la fenêtre générer, puis activez la case à cocher réalité virtuelle prise en charge sous paramètres XR dans le panneau Inspecteur, comme indiqué dans l’image ci-dessous. Notez que vous devrez peut-être faire glisser la fenêtre Paramètres de build pour voir le panneau Inspecteur. La case à cocher de réalité virtuelle prise en charge s’applique également à la réalité mixte et aux casques de la réalité augmentée, car elle fait référence à l’activation de la vision stéréoscopique (rendu de différentes images pour chaque oeil). ![Leçon 1 Chapitre 4 Étape 3](images/Lesson1Chapter4Step3.JPG)
4. Dans le même volet de l’inspecteur, vérifiez que la case à cocher perception spatiale de la section fonctionnalités est activée sous paramètres de publication. La perception spatiale nous permet de visualiser le maillage de mappage spatial sur un appareil de réalité mixte, tel que HoloLens 2. Les paramètres de publication se trouvent dans le panneau Inspecteur, au-dessus des paramètres XR et sous autres paramètres.
![Leçon 1 Chapitre 4 Étape 4](images/Lesson1Chapter4Step4.JPG)

> REMARQUE : Bien qu’il ne soit pas utilisé dans cette section, d’autres fonctionnalités courantes que vous pouvez souhaiter activer incluent le microphone pour les commandes vocales et InternetClient pour la connexion aux services qui requièrent une connexion réseau.

### <a name="import-the-mixed-reality-toolkit"></a>Importer le Kit de ressources de réalité mixte

1. Téléchargez le package Unity du [Kit d’outils de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC1.unitypackage) et enregistrez-le dans un dossier sur votre ordinateur.

2. Importez le package du Kit de ressources de réalité mixte en cliquant sur Assets (Ressources)> Import > Custom Package (Package personnalisé). Recherchez le package du Kit de ressources de réalité mixte téléchargé à l’étape 1 et ouvrez-le pour commencer le processus d’importation. Patientez quelques minutes, le temps que le processus d’importation se termine.
    ![Leçon 1 Chapitre 2 Étape 2a](images/Lesson1Chapter2Step2a.JPG) ![Leçon 1 Chapitre 2 Étape 2b](images/Lesson1Chapter2Step2b.JPG)

3. Dans la fenêtre contextuelle suivante, cliquez sur Importer pour commencer l’importation de la boîte à outils de la réalité mixte. Vérifiez que tous les éléments sont vérifiés comme indiqué dans l’image. Si une boîte de dialogue contextuelle s’affiche et vous invite à appliquer les paramètres par défaut de la mise en page d’outils de la réalité mixte, cliquez sur appliquer.
    ![Leçon 1 Chapitre 2 Étape 3](images/Lesson1Chapter2Step3.JPG) ![Leçon 1 Chapitre 2 Étape 3](images/Lesson1Chapter2Step3b.JPG)

### <a name="configure-the-mixed-reality-toolkit"></a>Configurer le Kit de ressources de réalité mixte

1. Configurez le MRTK en sélectionnant la boîte à outils de réalité mixte > configurer à partir de la barre de menus. Si vous ne voyez pas cet élément de menu après avoir importé le Kit de ressources de réalité mixte, redémarrez Unity.
  ![Leçon 1 Chapitre 3 Étape 1](images/Lesson1Chapter3Step1.JPG)

  > Remarque : Une boîte de dialogue contextuelle peut s’afficher pour vous demander de sélectionner un profil pour la boîte à outils de la réalité mixte. Si c’est le cas, sélectionnez OK, puis choisissez le profil nommé «DefaultMixedRealityToolkitConfigurationProfile».

2. Votre scène aura plusieurs nouveaux éléments et modifications dans le MRTK. Enregistrez votre scène sous un nom différent en cliquant sur fichier > Enregistrer sous et donnez un nom à votre scène, par exemple BaseScene. Gardez votre scène organisée en l’enregistrant dans le dossier scenes du dossier de ressources de votre projet.
  ![Leçon 1 Chapitre 3 Étape2a](images/Lesson1Chapter3Step2a.JPG)
  ![Leçon 1 Chapitre 3 Étape2b](images/Lesson1Chapter3Step2b.JPG)

### <a name="build-your-application-to-your-device"></a>Générer votre application sur votre appareil

1. Si vous avez fermé la fenêtre Paramètres de génération à partir des sections précédentes, ouvrez à nouveau la fenêtre Paramètres de build en accédant à fichier > paramètres de Build.
    ![Leçon 1 Chapitre 5 Étape 1](images/Lesson1Chapter5Step1.JPG)

2. Vérifiez que la scène que vous souhaitez essayer se trouve dans la liste scenes dans la build, en cliquant sur le bouton Ajouter des scènes en cours.

3. Appuyez sur le bouton Build (Générer) pour commencer le processus de génération.
    ![Leçon 1 Chapitre 5 Étape 3](images/Lesson1Chapter5Step3.JPG)

4. Créez un dossier pour votre application et nommez-le. Dans l’image ci-dessous, un dossier avec le nom de l’application a été créé pour contenir l’application. Cliquez sur Sélectionner un dossier pour commencer à créer le dossier nouvellement créé. Une fois la génération terminée, vous pouvez fermer la fenêtre Paramètres de build dans Unity. 
    ![Leçon 1 Chapitre 5 Étape 4](images/Lesson1Chapter5Step4.JPG)

  > REMARQUE : Si la génération échoue, essayez de renouveler l’opération, éventuellement après avoir redémarré Unity. Si une erreur s’affiche, telle que «erreur: CS0246 = le type ou le nom d’espace de noms «XX» est introuvable (vous manque-t-il une directive using ou une référence d’assembly?). Si c’est le cas, vous devrez peut-être installer le [Kit de développement logiciel (SDK) Windows 10 (10.0.18362.0)](<https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk>)
  >

5. Une fois la génération terminée, ouvrez le dossier créé qui contient vos fichiers d’application nouvellement générés. Double-cliquez sur la solution MixedRealityBase. sln, ou le nom correspondant, si vous avez utilisé un autre nom pour votre projet, pour ouvrir le fichier solution dans Visual Studio.

  > Remarque : Veillez à ouvrir le dossier nouvellement créé (c’est-à-dire, le dossier de l’application, si vous respectez les conventions d’affectation des noms des étapes précédentes), dans la mesure où il y aura un fichier. sln portant le même nom en dehors de ce dossier, à ne pas confondre avec le fichier. sln dans le dossier Build. 

![Leçon 1 Chapitre 5 Étape 5](images/Lesson1Chapter5Step5.JPG)

  > Remarque : Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants requis sont installés comme spécifié dans la [page « Installer les outils »](install-the-tools.md).

6. Connectez votre HoloLens 2 à votre PC. Bien que ces instructions partent du principe que vous allez déployer un test avec un appareil HoloLens 2, vous pouvez également choisir de déployer vers l' [émulateur hololens 2](using-the-hololens-emulator.md) ou de créer un [package d’application pour chargement](<https://docs.microsoft.com/en-us/windows/uwp/packaging/packaging-uwp-apps>)

7. Avant d’effectuer la génération sur votre appareil, vérifiez que ce dernier est en mode développeur. Si c’est la première fois que vous déployez sur le HoloLens 2, Visual Studio peut vous demander d’associer votre HoloLens 2 avec un code confidentiel. Veuillez suivre [ces instructions](https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio) si vous devez activer le mode développeur ou associer l’appareil à Visual Studio.

8. Configurez Visual Studio pour la création dans votre HoloLens 2 en sélectionnant la configuration Release et l’architecture ARM.
    ![Leçon 1 Chapitre 5 Étape 8](images/Lesson1Chapter5Step8.JPG)

9. La dernière étape consiste à créer sur votre appareil en sélectionnant Déboguer > Exécuter sans débogage. Si vous sélectionnez l’option Exécuter sans débogage, l’application démarre immédiatement sur votre appareil lors d’une génération réussie, mais sans informations de débogage dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci. Vous pouvez également sélectionner générer > déployer la solution pour déployer sur votre appareil sans démarrer automatiquement l’application.
    ![Leçon 1 Chapitre 5 Étape 9](images/Lesson1Chapter5Step9.JPG)

## <a name="congratulations"></a>Félicitations

Vous avez maintenant déployé votre première application HoloLens 2. Au fur et à mesure que vous parcourez, vous devriez voir un maillage spatial couvrant toutes les surfaces qui ont été perçues par le HoloLens 2. En outre, vous devriez voir des indicateurs sur vos mains et vos doigts pour le suivi de la main et un compteur de fréquence d’images pour garder un œil sur les performances de l’application. Ce ne sont là que quelques-uns des éléments fondamentaux immédiatement disponibles dans le Kit de ressources de réalité mixte. Dans les leçons à venir, vous commencerez à ajouter du contenu et de l’interactivité à votre scène afin de pouvoir explorer pleinement les fonctionnalités de HoloLens 2 et de la boîte à outils de la réalité mixte.

>Remarque : Vous découvrirez comment afficher/masquer le compteur de fréquence d’images à l’aide d’une commande vocale dans la [Leçon 5](mrlearning-base-ch5.md).

[Leçon suivante : 3. Création d’une interface utilisateur et configuration d’une réalité mixte Toolkit](mrlearning-base-ch2.md)
