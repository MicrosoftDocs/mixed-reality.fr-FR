---
title: Tutoriels de démarrage - 2. Initialisation de votre projet et de votre première application
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 11/01/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: d4e58e2c9236ba35b4394fd80cde3843edaa6f57
ms.sourcegitcommit: 4d43a8f40e3132605cee9ece9229e67d985db645
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74491202"
---
# <a name="2-initializing-your-project-and-first-application"></a>2. Initialisation de votre projet et de votre première application

Dans cette première leçon, vous allez découvrir certaines fonctionnalités du [Mixed Reality Toolkit (MRTK)](). Vous verrez également comment démarrer votre première application pour HoloLens 2 et la déployer sur l’appareil.

## <a name="objectives"></a>Objectifs

* Optimiser Unity pour le développement HoloLens.
* Importer les ressources et configurer la scène.
* Visualiser le maillage spatial, les maillages de la main et le compteur de fréquence d’images.

## <a name="instructions"></a>Instructions

### <a name="create-new-unity-project"></a>Créer un projet Unity

1. Démarrez Unity.
2. Sélectionnez **New**.
![Leçon 1, section 1, étape 2](images/mrlearning-base-ch1-1-step2.JPG)

3. Entrez un nom de projet (par exemple, « MixedRealityBase »).
![Leçon 1, section 1, étape 3](images/mrlearning-base-ch1-1-step3.JPG)
4. Entrez un emplacement auquel enregistrer votre projet.
![Leçon 1, section 1, étape 4](images/mrlearning-base-ch1-1-step4.JPG)
5. Vérifiez que le projet est défini sur **3D**.
![Leçon 1, section 1, étape 5](images/mrlearning-base-ch1-1-step5.JPG)
6. Cliquez sur **Create Project**.
![Leçon 1, section 1, étape 6](images/mrlearning-base-ch1-1-step6.JPG)


### <a name="configure-the-unity-project-for-windows-mixed-reality"></a>Configurer le projet Unity pour Windows Mixed Reality

1. Ouvrez la fenêtre *Build Settings* (Paramètres de génération) en choisissant **File** > **Build Settings**.
![Leçon 1, section 2, étape 1](images/mrlearning-base-ch1-2-step1.JPG)
2. Sélectionnez *Universal Windows Platform* (Plateforme Windows universelle), puis cliquez sur le bouton **Switch Platform** (Changer de plateforme). Les applications qui s’exécutent sur HoloLens 2 doivent être compatibles avec la plateforme Windows universelle (UWP).
![Leçon 1, section 2, étape 2](images/mrlearning-base-ch1-2-step2.JPG)
3. Activez la réalité virtuelle en cliquant sur **Player Settings** (Paramètres du lecteur) dans la fenêtre Build (Générer), puis cochez la case *Virtual Reality Supported* (Prise en charge de la réalité virtuelle), sous XR Settings (Paramètres XR) dans le panneau Inspector (Inspecteur), comme le montre l’image ci-dessous. Notez que vous devrez peut-être faire glisser la fenêtre *Build Settings* pour voir le panneau Inspector. La case à cocher *Virtual Reality Supported* s’applique également aux casques de réalité mixte et de réalité augmentée, car elle fait référence à l’activation de la vision stéréoscopique (rendu d’images différentes pour chaque œil). ![Leçon 1, section 2, étape 3](images/mrlearning-base-ch1-2-step3.JPG)
4. Sous XR Settings, choisissez *Single Pass Instanced* (Instanciation en un seul passage) comme *Stereo Rendering Mode* (Mode de rendu stéréo). Ce [style de pipeline de rendu](https://docs.unity3d.com/Manual/SinglePassStereoRenderingHoloLens.html) donne généralement de meilleurs résultats avec HoloLens 2. Si vous souhaitez obtenir d’autres configurations performantes pour votre environnement Unity, suivez [ces instructions](recommended-settings-for-unity.md).
![Leçon 1, section 2, étape 4](images/mrlearning-base-ch1-2-step4.jpg)
5. Dans le même panneau Inspector, sous *Publishing Settings* (Paramètres de publication), dans la section des fonctionnalités, vérifiez que la case *Spatial Perception* (Perception spatiale) est cochée. La perception spatiale nous permet de visualiser le maillage du mappage spatial sur un appareil de réalité mixte comme HoloLens 2. Les paramètres de publication se trouvent dans le panneau Inspector, au-dessus de XR Settings et sous Other Settings (Autres paramètres).
![Leçon 1, section 2, étape 5](images/mrlearning-base-ch1-2-step5.JPG)

    > [!NOTE]
    > Vous pouvez également activer d’autres fonctionnalités courantes comme *Microphone* (pour les commandes vocales) et *InternetClient* (pour la connexion à des services nécessitant une connexion réseau), même si elles ne sont pas utilisées dans cette section.

### <a name="import-the-mixed-reality-toolkit"></a>Importer le Kit de ressources de réalité mixte

1. Téléchargez le [package de base version 2.1.0](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.1.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage) de [Mixed Reality Toolkit](https://github.com/microsoft/MixedRealityToolkit-Unity/releases) pour Unity et enregistrez-le dans un dossier sur votre PC.

2. Importez le package *Mixed Reality Toolkit* que vous avez téléchargé à l’étape précédente. Commencez par cliquer sur **Assets** (Ressources) > **Import** (Importer) > **Custom Package** (Package personnalisé). Ensuite, sélectionnez *Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage* et ouvrez-le pour lancer le processus d’importation. Patientez quelques minutes, le temps que le processus d’importation se termine.
    ![Leçon 1, section 3, étape 2a](images/mrlearning-base-ch1-3-step2a.JPG) ![Leçon 1, section 3, étape 2b](images/mrlearning-base-ch1-3-step2b.JPG)

3. Dans la fenêtre contextuelle suivante, cliquez sur **Import** pour commencer l’importation du package sélectionné dans le projet Unity. Vérifiez que tous les éléments sont cochés, comme illustré dans l’image.
    ![Leçon 1, section 3, étape 3](images/mrlearning-base-ch1-3-step3.JPG)

    > [!NOTE]
    > Si une boîte de dialogue contextuelle s’affiche pour vous inviter à appliquer les paramètres par défaut de Mixed Reality Toolkit, cliquez sur **Apply** (Appliquer). MRTK analyse votre projet à la recherche de paramètres recommandés manquants si vous l’importez pour une installation automatisée. Selon vos paramètres, la fenêtre contextuelle peut être différente de l’image ci-dessous.

    ![Leçon 1, section 3, étape 4, remarque 1](images/mrlearning-base-ch1-3-step4-note1.JPG)

### <a name="configure-the-mixed-reality-toolkit"></a>Configurer le Kit de ressources de réalité mixte

1. Ajoutez le *Mixed Reality Toolkit* à votre scène actuelle. Pour cela, sélectionnez **Mixed Reality Toolkit** > **Add to Scene and Configure** (Ajouter à la scène et configurer) à partir de la barre de menus. Si vous ne voyez pas cet élément de menu après avoir importé le Kit de ressources de réalité mixte, redémarrez Unity.
    ![Leçon 1, section 4, étape 1](images/mrlearning-base-ch1-4-step1.JPG)

    > [!NOTE]
    > Une boîte de dialogue contextuelle peut s’afficher pour vous demander de sélectionner un [profil Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Profiles/Profiles.html). Double-cliquez sur le profil nommé *DefaultHoloLens2ConfigurationProfile* pour le choisir.

2. Votre scène comprend de nouveaux éléments et des modifications. Enregistrez votre scène sous un autre nom. Pour cela, cliquez sur **File** (Fichier) > **Save As...** (Enregistrer sous) et donnez un nom à votre scène, par exemple *BaseScene*. Dans un souci d’organisation, enregistrez la scène dans le dossier *Scenes* du dossier *Assets* de votre projet.
    ![Leçon 1, section 4, étape 2a](images/mrlearning-base-ch1-4-step2a.JPG) ![Leçon 1, section 4, étape 2b](images/mrlearning-base-ch1-4-step2b.JPG)

### <a name="build-your-application-to-your-device"></a>Générer votre application sur votre appareil

1. Si vous avez fermé la fenêtre *Build Settings* dans les sections précédentes, rouvrez-la ** en choisissant **File** > **Build Settings**.
    ![Leçon 1, section 5, étape 1](images/mrlearning-base-ch1-5-step1.JPG)

2. Vérifiez que la scène que vous venez de créer figure dans la liste *Scenes in Build* (Scènes dans la génération). Pour cela, cliquez sur le bouton **Add Open Scenes** (Ajouter des scènes ouvertes) quand votre scène est ouverte dans Unity.

3. Appuyez sur le bouton **Build** (Générer) pour commencer le processus de génération.
    ![Leçon 1, section 5, étape 3](images/mrlearning-base-ch1-5-step3.JPG)

4. Créez un dossier pour votre application et nommez-le. Dans l’image ci-dessous, un dossier portant le nom App a été créé pour contenir l’application. Cliquez sur **Select Folder** (Sélectionner le dossier) pour commencer la génération dans le dossier que vous venez de créer. Une fois la génération terminée, vous pouvez fermer la fenêtre *Build Settings* dans Unity.
    ![Leçon 1, section 5, étape 4](images/mrlearning-base-ch1-5-step4.JPG)

  > [!IMPORTANT]
  > Si la génération échoue, essayez de renouveler l’opération, éventuellement après avoir redémarré Unity. Si vous voyez une erreur du type « Error: CS0246 = The type or namespace name “XX” could not be found (are you missing a using directive or an assembly reference?) » (Erreur : CS0246 = Le type ou le nom de l’espace de noms XX est introuvable [une directive using ou une référence d’assembly est-elle manquante ?]), vous devrez peut-être installer le [SDK Windows 10 (10.0.18362.0)](https://developer.microsoft.com//windows/downloads/windows-10-sdk).

5. Une fois la génération terminée, ouvrez le dossier créé qui contient vos fichiers d’application nouvellement générés. Double-cliquez sur la solution *MixedRealityBase.sln* (ou le nom correspondant si vous avez utilisé un autre nom pour votre projet) pour ouvrir le fichier solution dans Visual Studio.

    > [!NOTE]
    > Veillez à ouvrir le dossier créé (par exemple, le dossier *App* si vous avez suivi les conventions de nommage indiquées aux étapes précédentes), car il existe un fichier .sln portant le même nom en dehors de ce dossier qui ne doit pas être confondu avec le fichier .sln situé dans le dossier de génération. La structure de dossiers doit ressembler à celle de l’image ci-dessous.
    >
    > Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants requis sont installés comme spécifié dans la [page « Installer les outils »](install-the-tools.md).

    ![Leçon 1, section 5, étape 5](images/mrlearning-base-ch1-5-step5.JPG)

6. Connectez votre HoloLens 2 à votre PC. Bien que ces instructions supposent que vous déployez sur un appareil HoloLens 2, vous pouvez choisir de déployer sur l’[émulateur HoloLens 2](using-the-hololens-emulator.md) ou de créer un [package d’application pour effectuer un chargement indépendant](<https://docs.microsoft.com//windows/uwp/packaging/packaging-uwp-apps>).

    > [!IMPORTANT]
    > Avant d’effectuer la génération sur votre appareil, celui-ci doit être en *Mode développeur* et associé à votre ordinateur de développement. Vous pouvez effectuer ces deux étapes en suivant [ces instructions](using-visual-studio.md).

7. Configurez Visual Studio pour effectuer la génération sur votre HoloLens 2. Pour cela, sélectionnez la configuration *Release* ou *Master*, l’architecture *ARM* et *Device* comme cible.
    ![Leçon 1, section 5, étape 8](images/mrlearning-base-ch1-5-step7.JPG)

8. L’étape finale consiste à effectuer la génération et le déploiement sur votre appareil. Pour cela, sélectionnez **Déboguer** > **Démarrer sans débogage**. Quand vous sélectionnez *Démarrer sans débogage*, l’application démarre immédiatement sur votre appareil si la génération réussit, mais le débogueur attaché et les informations de débogage n’apparaissent pas dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci.

    > [!NOTE]
    > Vous pouvez également sélectionner **Générer** > **Déployer la solution** pour effectuer le déploiement sur votre appareil sans que l’application démarre automatiquement.

    ![Leçon 1, section 5, étape 9](images/mrlearning-base-ch1-5-step8.JPG)

## <a name="congratulations"></a>Félicitations

Vous venez de déployer votre première application HoloLens 2. À mesure que vous vous déplacez, vous devez voir un maillage de mappage spatial couvrant toutes les surfaces qui ont été perçues par HoloLens 2. En outre, vous devez voir des indicateurs sur vos mains et doigts pour le suivi de la main et un compteur de fréquence d’images pour vous tenir informé des performances de l’application. Ce ne sont là que quelques-uns des éléments fondamentaux immédiatement disponibles dans le Kit de ressources de réalité mixte. Au cours des leçons à venir, vous commencerez à ajouter du contenu et une interactivité à votre scène afin de pouvoir explorer pleinement les fonctionnalités d’HoloLens 2 et de Mixed Reality Toolkit.

> [!NOTE]
> Dans l’application, vous remarquerez peut-être le profileur visuel. Vous découvrirez comment afficher/masquer le compteur de fréquence d’images à l’aide d’une commande vocale dans la [leçon 5](mrlearning-base-ch5.md). Il est généralement recommandé d’afficher le profileur visuel pendant toute la durée du développement pour que vous puissiez voir si des modifications apportées au code impactent les performances. L’application HoloLens 2 doit [s’exécuter en continu à 60 images par seconde](understanding-performance-for-mixed-reality.md).

[Leçon suivante : 3. Création de l’interface utilisateur et configuration du kit d’outils de réalité mixte](mrlearning-base-ch2.md)
