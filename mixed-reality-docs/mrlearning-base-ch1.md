---
title: Didacticiels de mise en route-2. Initialisation de votre projet et de la première application
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 11/01/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 3bf218b42ea8abed45a80c0dd048e791cdd8372b
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926886"
---
# <a name="2-initializing-your-project-and-first-application"></a>2. initialisation de votre projet et de votre première application

Dans cette première leçon, vous découvrirez certaines des fonctionnalités que le [MRTK (Mixed Reality Toolkit)]() doit offrir, commencez votre première application pour HoloLens 2 et déployez-la sur l’appareil.

## <a name="objectives"></a>Objectifs

* Optimiser Unity pour le développement HoloLens.
* Importer les ressources et configurer la scène.
* Visualisation du maillage de mappage spatial, des maillages de main et du compteur de fréquence.

## <a name="instructions"></a>Instructions

### <a name="create-new-unity-project"></a>Créer un projet Unity

1. Démarrez Unity.
2. Sélectionnez **New**.
![Lesson1 Section1 étape 2](images/mrlearning-base-ch1-1-step2.JPG)

3. Entrez un nom de projet (par exemple, « MixedRealityBase »).
![Lesson1 Section1 step3](images/mrlearning-base-ch1-1-step3.JPG)
4. Entrez un emplacement auquel enregistrer votre projet.
![Lesson1 Section1 étape 4](images/mrlearning-base-ch1-1-step4.JPG)
5. Vérifiez que le projet est défini sur **3D**.
![Lesson1 Section1 étape 5](images/mrlearning-base-ch1-1-step5.JPG)
6. Cliquez sur **Create Project**.
![Lesson1 Section1 étape 6](images/mrlearning-base-ch1-1-step6.JPG)


### <a name="configure-the-unity-project-for-windows-mixed-reality"></a>Configurer le projet Unity pour Windows Mixed Reality

1. Ouvrez la fenêtre *paramètres de build* en accédant à **fichier** > paramètres de **Build**.
![Lesson1 section2 étape1](images/mrlearning-base-ch1-2-step1.JPG)
2. Sélectionnez le *plateforme Windows universelle* , puis cliquez sur le bouton **changer de plateforme** pour basculer entre les plateformes. Les applications qui s’exécutent sur HoloLens 2 doivent être compatibles plateforme Windows universelle (UWP).
![Lesson1 section2 étape 2](images/mrlearning-base-ch1-2-step2.JPG)
3. Activez la réalité virtuelle en cliquant sur le bouton **paramètres du lecteur** dans la fenêtre générer, puis activez la case à cocher de la *réalité virtuelle prise en charge* sous paramètres XR dans le panneau Inspecteur, comme indiqué dans l’image ci-dessous. Notez que vous devrez peut-être faire glisser la fenêtre *paramètres de build* pour voir le panneau Inspecteur. La case à cocher de *réalité virtuelle prise en charge* s’applique également à la réalité mixte et aux casques de la réalité augmentée, car elle fait référence à l’activation de la vision stéréoscopique (rendu de différentes images pour chaque oeil). ![Lesson1 Section2 step3](images/mrlearning-base-ch1-2-step3.JPG)
4. Également sous paramètres XR, définissez le *mode de rendu stéréo* sur *Single-instanced*. Ce [style de pipeline de rendu](https://docs.unity3d.com/Manual/SinglePassStereoRenderingHoloLens.html) est généralement le plus performant pour HoloLens 2. Si vous souhaitez obtenir d’autres configurations performantes pour votre environnement Unity, suivez [ces instructions](recommended-settings-for-unity.md).
![Lesson1 section2 étape 4](images/mrlearning-base-ch1-2-step4.jpg)
5. Dans le même volet de l’inspecteur, vérifiez que la case à cocher *perception spatiale* de la section fonctionnalités est activée sous *paramètres de publication*. La perception spatiale nous permet de visualiser le maillage de mappage spatial sur un appareil de réalité mixte, tel que HoloLens 2. Les paramètres de publication se trouvent dans le panneau Inspecteur, au-dessus des paramètres XR et sous autres paramètres.
![Lesson1 section2 étape 5](images/mrlearning-base-ch1-2-step5.JPG)

    > [!NOTE]
    > Bien qu’il ne soit pas utilisé dans cette section, d’autres fonctionnalités courantes que vous pouvez souhaiter activer incluent le *microphone* pour les commandes vocales et *internetclient* pour la connexion aux services qui requièrent une connexion réseau.

### <a name="import-the-mixed-reality-toolkit"></a>Importer le Kit de ressources de réalité mixte

1. Téléchargez la [version du package 2.1.0](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.1.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage) Unity de la [réalité mixte](https://github.com/microsoft/MixedRealityToolkit-Unity/releases) et enregistrez-la dans un dossier sur votre ordinateur.

2. Importez le package de la *boîte à outils de réalité mixte* que vous avez téléchargé à l’étape précédente. Commencez par cliquer sur **actifs** > **Importer** > **package personnalisé** et sélectionnez *Microsoft. MixedReality. Toolkit. Unity. Foundation. 2.1.0. pour Unity* et ouvrez-le pour commencer le processus d’importation. Veuillez patienter quelques minutes avant la fin du processus d’importation.
    ![Lesson1 section3 Step2a](images/mrlearning-base-ch1-3-step2a.JPG) ![Lesson1 section3 Step2b](images/mrlearning-base-ch1-3-step2b.JPG)

3. Dans la fenêtre contextuelle suivante, cliquez sur **Importer** pour commencer l’importation du package sélectionné dans le projet Unity. Vérifiez que tous les éléments sont vérifiés comme indiqué dans l’image.
    ![Lesson1 section3 step3](images/mrlearning-base-ch1-3-step3.JPG)

    > [!NOTE]
    > Si une boîte de dialogue contextuelle s’affiche et vous invite à appliquer les paramètres par défaut de la mise en page d’outils de la réalité mixte, cliquez sur **appliquer**. MRTK analyse votre projet pour déterminer s’il manque des paramètres recommandés lorsqu’il est importé pour une installation automatisée. Selon vos paramètres, la fenêtre contextuelle peut paraître différente, puis l’image ci-dessous.

    ![Lesson1 section3 étape 4 Note1](images/mrlearning-base-ch1-3-step4-note1.JPG)

### <a name="configure-the-mixed-reality-toolkit"></a>Configurer le Kit de ressources de réalité mixte

1. Ajoutez la *boîte à outils de réalité mixte* à votre scène actuelle en sélectionnant la **boîte à outils de réalité mixte** > **Ajouter à la scène et configurer.** à partir de la barre de menus. Si vous ne voyez pas cet élément de menu après avoir importé le Kit de ressources de réalité mixte, redémarrez Unity.
    ![Lesson1 Section4 étape1](images/mrlearning-base-ch1-4-step1.JPG)

    > [!NOTE]
    > Vous pouvez voir s’afficher une boîte de dialogue contextuelle permettant de sélectionner un [Profil pour la boîte à outils de la réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Profiles/Profiles.html). Choisissez le profil nommé *DefaultHoloLens2ConfigurationProfile* en double-cliquant dessus.

2. Votre scène aura plusieurs nouveaux éléments et modifications. Enregistrez votre scène sous un nom différent en cliquant sur **fichier** > **Enregistrer sous...** , puis donnez un nom à votre scène, par exemple *BaseScene*. Gardez votre scène organisée en l’enregistrant dans le dossier *scenes* du dossier de *ressources* de votre projet.
    ![Lesson1 Section4 Step2a](images/mrlearning-base-ch1-4-step2a.JPG) ![Lesson1 Section4 Step2b](images/mrlearning-base-ch1-4-step2b.JPG)

### <a name="build-your-application-to-your-device"></a>Générer votre application sur votre appareil

1. Si vous avez fermé la fenêtre *paramètres de génération* à partir des sections précédentes, ouvrez à nouveau la fenêtre *paramètres* de build en accédant à **fichier** > **paramètres de build**.
    ![Lesson1 Section5 étape1](images/mrlearning-base-ch1-5-step1.JPG)

2. Assurez-vous que la scène que vous venez de créer se trouve dans la liste *scènes dans* la liste Build en cliquant sur le bouton **Ajouter des scènes ouvertes** pendant que votre scène est ouverte dans Unity.

3. Appuyez sur le bouton **générer** pour commencer le processus de génération.
    ![Lesson1 Section5 step3](images/mrlearning-base-ch1-5-step3.JPG)

4. Créez un dossier pour votre application et nommez-le. Dans l’image ci-dessous, un dossier avec le nom de l’application a été créé pour contenir l’application. Cliquez sur **Sélectionner un dossier** pour commencer à créer le dossier nouvellement créé. Une fois la génération terminée, vous pouvez fermer la fenêtre *paramètres de build* dans Unity.
    ![Lesson1 Section5 étape 4](images/mrlearning-base-ch1-5-step4.JPG)

  > [!IMPORTANT]
  > Si la génération échoue, essayez de renouveler l’opération, éventuellement après avoir redémarré Unity. Si vous voyez une erreur, telle que « erreur : CS0246 = le type ou le nom d’espace de noms «XX » est introuvable (une directive using ou une référence d’assembly est-elle manquante ?). Si c’est le cas, vous devrez peut-être installer le [Kit de développement logiciel (SDK) Windows 10 (10.0.18362.0)](https://developer.microsoft.com//windows/downloads/windows-10-sdk)

5. Une fois la génération terminée, ouvrez le dossier créé qui contient vos fichiers d’application nouvellement générés. Double-cliquez sur la solution *MixedRealityBase. sln* , ou le nom correspondant, si vous avez utilisé un autre nom pour votre projet, pour ouvrir le fichier solution dans Visual Studio.

    > [!NOTE]
    > Veillez à ouvrir le dossier nouvellement créé (par exemple, le dossier de l' *application* , si vous respectez les conventions d’affectation des noms des étapes précédentes), dans la mesure où il y aura un fichier. sln portant le même nom en dehors de ce dossier, à ne pas confondre avec le fichier. sln dans le dossier Build. La structure de dossiers doit ressembler à l’image ci-dessous.
    >
    > Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants requis sont installés comme spécifié dans la [page « Installer les outils »](install-the-tools.md).

    ![Lesson1 Section5 étape 5](images/mrlearning-base-ch1-5-step5.JPG)

6. Connectez votre HoloLens 2 à votre PC. Bien que ces instructions partent du principe que vous allez déployer sur un appareil HoloLens 2, vous pouvez également choisir de déployer vers l' [émulateur hololens 2](using-the-hololens-emulator.md) ou de créer un [package d’application pour chargement](<https://docs.microsoft.com//windows/uwp/packaging/packaging-uwp-apps>)

    > [!IMPORTANT]
    > Avant de créer sur votre appareil, l’appareil doit être en *mode développeur* et associé à votre ordinateur de développement. Vous pouvez effectuer ces deux étapes en suivant [ces instructions](using-visual-studio.md) .

7. Configurez Visual Studio pour la création dans votre HoloLens 2 en sélectionnant la configuration *Release* ou *Master* , l’architecture *ARM* et l' *appareil* en tant que cible.
    ![Lesson1 Section5 Step8](images/mrlearning-base-ch1-5-step7.JPG)

8. La dernière étape consiste à générer et à déployer sur votre appareil en sélectionnant **Déboguer** > **exécuter sans débogage**. Si vous sélectionnez l’option *exécuter sans débogage* , l’application démarre immédiatement sur votre appareil lors d’une génération réussie, mais sans le débogueur et les informations s’affichent dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci.

    > [!NOTE]
    > Vous pouvez également sélectionner **générer** > **déployer la solution** pour déployer sur votre appareil sans démarrer automatiquement l’application.

    ![Lesson1 Section5 Step9](images/mrlearning-base-ch1-5-step8.JPG)

## <a name="congratulations"></a>Félicitations !

Vous avez maintenant déployé votre première application HoloLens 2. Au fur et à mesure que vous parcourez, vous devriez voir un maillage de mappage spatial couvrant toutes les surfaces qui ont été perçues par le HoloLens 2. En outre, vous devriez voir des indicateurs sur vos mains et vos doigts pour le suivi de la main et un compteur de fréquence d’images pour garder un œil sur les performances de l’application. Ce ne sont là que quelques-uns des éléments fondamentaux immédiatement disponibles dans le Kit de ressources de réalité mixte. Dans les leçons à venir, vous commencerez à ajouter du contenu et de l’interactivité à votre scène afin de pouvoir explorer pleinement les fonctionnalités de HoloLens 2 et de la boîte à outils de la réalité mixte.

> [!NOTE]
> Dans l’application, vous remarquerez peut-être le profileur Visual. Vous allez aborder la manière de basculer le compteur de fréquence d’images à l’aide d’une commande vocale dans la [leçon 5](mrlearning-base-ch5.md). Il est généralement recommandé de garder le générateur de profils visuel visible à tout moment pendant le développement pour comprendre quand les modifications du code peuvent avoir un impact sur les performances. L’application HoloLens 2 doit [s’exécuter en continu à 60 fps](understanding-performance-for-mixed-reality.md).

[Leçon suivante : 3. création d’une interface utilisateur et configuration d’un kit de tâches de réalité mixte](mrlearning-base-ch2.md)
