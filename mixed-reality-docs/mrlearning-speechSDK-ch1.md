---
title: Didacticiels Azure Speech services-1. Intégration et utilisation de la reconnaissance vocale et de la transcription
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 25e5aa05839845620a23c3dba6698ac7b5854d6d
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77553970"
---
# <a name="1-integrating-and-using-speech-recognition-and-transcription"></a>1. intégration et utilisation de la reconnaissance vocale et de la transcription

## <a name="overview"></a>Overview

Ce didacticiel crée une application de réalité mixte qui explore l’utilisation du kit de développement logiciel (SDK) Azure Cognitive Services Speech avec le HoloLens 2. À la fin de cette série de didacticiels, vous serez en mesure d’utiliser le microphone de votre appareil pour transcrire la parole en temps réel, traduire votre discours en d’autres langues et tirer parti de la fonctionnalité d’intention du kit de développement logiciel (SDK) Speech pour comprendre les commandes vocales à l’aide de artificiel audience.

## <a name="objectives"></a>Objectifs

* Découvrez comment intégrer le kit de développement logiciel (SDK) Azure Speech dans une application HoloLens 2
* En savoir plus sur l’utilisation des commandes vocales
* En savoir plus sur l’utilisation des fonctionnalités vocales en texte

## <a name="prerequisites"></a>Composants requis

>[!TIP]
>Si vous n’avez pas encore terminé la série des [didacticiels de mise](mrlearning-base.md) en route, nous vous recommandons d’effectuer d’abord ces didacticiels.

* PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Capacité de programmation C# de base
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)

>[!IMPORTANT]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X. Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.

## <a name="getting-started"></a>Mise en route

1. Démarrez Unity et créez un nouveau projet. Entrez le module d’apprentissage du kit de développement logiciel (SDK) Speech Name. Choisissez un emplacement pour l’emplacement où enregistrer votre projet. Cliquez sur créer un projet.

    ![Module2Chapter3step1im](images/module4chapter1step1im.PNG)

    >[!NOTE]
    >Assurez-vous que le modèle est défini sur 3D, comme indiqué dans l’image ci-dessus.

2. Téléchargez la [version du package 2.3.0](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.3.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage) Unity de la [réalité mixte](https://github.com/microsoft/MixedRealityToolkit-Unity/releases) et enregistrez-la dans un dossier sur votre ordinateur. Importez le package dans votre projet Unity. Pour obtenir des instructions détaillées sur la procédure à suivre, consultez les [didacticiels de mise en route-leçon 2. Initialisation de votre projet et de votre première application](mrlearning-base-ch1.md).

3. Téléchargez et importez le [Kit de développement logiciel (SDK) Azure Speech](https://aka.ms/csspeech/unitypackage) pour le package d’actifs Unity. Importez le package du kit de développement logiciel (SDK) Speech en cliquant sur actifs, en sélectionnant importer un package, puis en sélectionnant package personnalisé. Recherchez le package du kit de développement logiciel (SDK) Speech téléchargé précédemment et ouvrez-le pour commencer le processus d’importation.

    ![mrlearning-Speech-CH1-1-step3a. png](images/mrlearning-speech-ch1-1-step3a.png)

    ![mrlearning-Speech-CH1-1-step3b. png](images/mrlearning-speech-ch1-1-step3b.png)

4. Dans la fenêtre contextuelle suivante, cliquez sur Importer pour commencer l’importation du package du kit de développement logiciel (SDK) Speech. Vérifiez que tous les éléments sont cochés, comme indiqué dans l’image ci-dessous.

    ![mrlearning-Speech-CH1-1-step4. png](images/mrlearning-speech-ch1-1-step4.png)

5. Téléchargez les ressources du didacticiel :
    * [MRTK. HoloLens2. Unity. Tutorials. Assets. GettingStarted. 2.3.0.2. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.2/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage)
    * [SpeechSDKAssets. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/Speech_2/SpeechSDKAssets.unitypackage) (version 1,2)

    Le package de ressources SpeechSDKAssets est un ensemble de ressources et de scripts développés pour cette série de didacticiels afin d’illustrer l’utilisation pratique du kit de développement logiciel (SDK) Speech d’Azure. Il s’agit d’un terminal de commande vocale qui, au final, interviendra avec l’expérience d’assembly du lanceur Rocket développée dans les [didacticiels de prise en main-leçon 7. Création d’un exemple d’application de module lunaire](mrlearning-base-ch6.md).

6. Importez les deux packages de ressources du didacticiel dans votre projet Unity en suivant les étapes similaires que vous avez suivies pour importer le kit de ressources de réalité mixte et le SDK Speech.

7. Configurez la boîte à outils de réalité mixte (MRTK).

    Pour ce faire, cliquez sur le panneau du Toolkit de réalité mixte en haut de votre fenêtre, puis sélectionnez Ajouter à la scène et configurer.

    ![mrlearning-Speech-CH1-1-step7a. png](images/mrlearning-speech-ch1-1-step7a.png)

    Une fois l’objet MixedRealityToolkit sélectionné dans votre hiérarchie de scènes, dans la fenêtre de l’inspecteur, sélectionnez DefaultHoloLens2ConfigurationProfile pour en faire le profil actif de la boîte à outils de la réalité mixte.

    ![mrlearning-Speech-CH1-1-step7b. png](images/mrlearning-speech-ch1-1-step7b.png)

8. Votre scène contient maintenant plusieurs nouveaux éléments à partir du MRTK. Enregistrez votre scène sous un nom différent en cliquant sur « fichier », puis sur « Enregistrer sous » et nommez votre scène SpeechScene.

    >[!NOTE]
    >Si vous appuyez sur lire sur votre scène après avoir ajouté le MRTK à votre projet et qu’il n’entre pas en mode lecture, vous devrez peut-être redémarrer Unity.

9. Une fois l’objet MixedRealityToolkit sélectionné dans votre hiérarchie de scènes, cliquez sur Copier & Personnaliser dans le panneau Inspecteur pour ouvrir la fenêtre contextuelle cloner le profil. Dans la fenêtre contextuelle cloner un profil, entrez un nom approprié pour votre profil personnalisé, par exemple HoloLens2ConfigurationProfile personnalisé. Cliquez sur Cloner pour créer votre profil de configuration personnalisé et le définir comme profil actif.

    ![mrlearning-Speech-CH1-1-step9. png](images/mrlearning-speech-ch1-1-step9.png)

10. De même, dans le panneau inspecteur (avec l’objet MixedRealityToolkit sélectionné dans votre hiérarchie), désactivez le système de diagnostic en désactivant la case à cocher située à droite de l’option Activer le système de diagnostic.

    ![mrlearning-Speech-CH1-1-step10. png](images/mrlearning-speech-ch1-1-step10.png)

11. Dans ce didacticiel, nous utilisons les commandes vocales en entrée pour la reconnaissance vocale et la transcription. Nous allons cloner le profil d’entrée pour apporter des modifications aux paramètres de reconnaissance vocale.

    Lorsque l’objet MixedRealityToolkit est toujours sélectionné dans votre hiérarchie de scènes, cliquez sur le petit bouton cloner dans le panneau Inspecteur pour ouvrir la fenêtre contextuelle clone Profile. Dans la fenêtre contextuelle cloner un profil, entrez un nom approprié pour votre profil personnalisé, par exemple HoloLens2InputSystemProfile personnalisé, puis cliquez sur Cloner pour créer votre profil de système d’entrée personnalisé et le définir comme profil actif.

    ![mrlearning-Speech-CH1-1-step11. png](images/mrlearning-speech-ch1-1-step11.png)

12. Une fois le profil d’entrée cloné, développez la section Speech et suivez le même processus que dans l’étape précédente pour cloner le profil des commandes vocales.

    ![mrlearning-Speech-CH1-1-step12. png](images/mrlearning-speech-ch1-1-step12.png)

13. Sous la section Speech, accédez à paramètres généraux et remplacez comportement de démarrage par démarrage manuel.

    ![mrlearning-Speech-CH1-1-step13. png](images/mrlearning-speech-ch1-1-step13.png)

14. Dans le panneau projet, développez le dossier Lunarcom et faites glisser le Prefab Lunarcom_Base dans votre hiérarchie de scènes.

    ![mrlearning-Speech-CH1-1-STEP14. png](images/mrlearning-speech-ch1-1-step14.png)

15. Sélectionnez l’objet Lunarcom_Base dans votre hiérarchie, assurez-vous que la position est définie sur x = 0, y = 0 et z = 0, ainsi que la rotation définie sur x = 0, y = 0 et z = 0. Définissez l’échelle sur lecture x = 0.008, y = 0.008 et z = 0,01.

    ![Module4Chapter1step12im](images/module4chapter1step12im.PNG)

16. Cliquez sur Ajouter un composant, puis recherchez et sélectionnez contrôleur Lunarcom. Ce script est inclus dans le pack d’actifs Lunarcom que vous avez importé à l’étape 6.

    ![Module4Chapter1step13im](images/module4chapter1step13im.PNG)

17. Pour connecter notre application à Azure Cognitive Services, vous devez entrer une clé d’abonnement (également appelée clé API) pour le service vocal. Suivez les instructions [ici](https://docs.microsoft.com/azure/cognitive-services/speech-service/get-started) pour obtenir une clé d’abonnement gratuite. Une fois que vous avez obtenu la clé d’abonnement, entrez-la dans le champ clé de l’API du service vocal du composant LunarcomController dans le panneau Inspecteur, comme indiqué dans l’image ci-dessous.

18. Entrez la région que vous avez choisie lorsque vous vous êtes inscrit à la clé d’abonnement dans le champ région du service vocal du composant LunarcomController dans le panneau Inspecteur. Par exemple, pour la région ouest des États-Unis dans « ouestr ».

    ![Module4Chapter1step15im](images/module4chapter1step15im.PNG)

19. Dans votre hiérarchie, développez l’objet Lunarcom_Base en cliquant sur la flèche à gauche de celui-ci. Ensuite, faites de même pour son objet enfant, « terminal », comme indiqué dans l’image ci-dessous.

20. Si Lunarcom_Base est sélectionné, cliquez et faites glisser Lunarcom Text de la hiérarchie vers l’emplacement du texte de sortie dans le composant LunarcomController du panneau Inspecteur, comme indiqué dans l’image ci-dessous.

21. Effectuez la même opération avec l’objet terminal dans l’emplacement terminal et l’objet de connexion Light à l’emplacement de contrôle Light de connexion.

    ![Module4Chapter1step18im](images/module4chapter1step18im.PNG)

22. Cliquez sur la flèche en regard de la section Lunarcom Buttons du script LunarcomController dans le panneau Inspector, puis définissez la taille sur 3. Appuyez sur entrée ou retour. Trois nouveaux champs d’élément apparaissent alors.

    ![Module4Chapter1step19im](images/module4chapter1step19im.PNG)

23. Développez les boutons Lunarcom en cliquant sur la flèche en regard de celle-ci dans votre hiérarchie et en utilisant le même processus que ci-dessus, faites glisser les Gameobjects MIC, satellite et Rocket vers les références des éléments 0, 1 et 2, respectivement, dans le composant LunarcomController de la Panneau de l’inspecteur.

    ![Module4Chapter1step18im](images/module4chapter1step20im.PNG)

24. Sélectionnez l’objet Lunarcom_Base» dans votre hiérarchie. Cliquez sur Ajouter un composant dans le panneau Inspecteur, puis recherchez et sélectionnez Lunarcom Speech Recognizer. Répétez les mêmes étapes pour ajouter Lunarcom de mise en éveil par mot.

    ![Module4Chapter1step18im](images/module4chapter1step21im.PNG)

25. Dans l’emplacement de mise en éveil par mot, tapez activer terminal. Dans l’emplacement ignorer le mot, tapez rejeter le terminal.

    ![Module4Chapter1step18im](images/module4chapter1step22im.PNG)

## <a name="build-your-application-to-your-device"></a>Générer votre application sur votre appareil

1. Ouvrez à nouveau la fenêtre Paramètres de build en accédant à fichier > paramètres de Build.

    ![images/mrlearning-Speech-CH1-2-étape1](images/mrlearning-speach-ch1-2-step1.jpg)

2. Vérifiez que la scène que vous souhaitez essayer figure dans la liste « Scenes in Build » (Scènes dans la génération) en cliquant sur le bouton « Add Open Scenes » (Ajouter des scènes ouvertes).

3. Appuyez sur le bouton Paramètres du lecteur et accédez à paramètres de publication. Sous fonctionnalités, activez : Internet, serveur client Internet, serveur client de réseau privé, microphone et perception spatiale.

4. Dans les mêmes paramètres de lecteur, accédez à paramètres XR et sélectionnez la réalité virtuelle prise en charge sur activé.

5. Appuyez sur le bouton Build (Générer) pour commencer le processus de génération.

    ![mrlearning-Speech-CH1-2-étape 5](images/mrlearning-speach-ch1-2-step5.jpg)

6. Créez un dossier pour votre application et nommez-le. Dans l’image ci-dessous, un dossier portant le nom « App » a été créé pour contenir l’application. Cliquez sur « Select Folder » (Sélectionner le dossier) pour commencer la génération dans le dossier que vous venez de créer. Une fois la génération terminée, vous pouvez fermer la fenêtre « Build Settings » dans Unity.

    ![mrlearning-Speech-CH1-2-étape 6](images/mrlearning-speach-ch1-2-step6.jpg)

    >[!NOTE]
    >Si la génération échoue, essayez de renouveler l’opération, éventuellement après avoir redémarré Unity. Si vous voyez une erreur telle que « erreur : CS0246 = le type ou le nom d’espace de noms «XX » est introuvable (vous manque-t-il une directive using ou une référence d’assembly ?)», vous devrez peut-être installer le [Kit de développement logiciel (SDK) Windows 10 (10.0.18362.0)](<https://developer.microsoft.com//windows/downloads/windows-10-sdk>)

7. Une fois la génération terminée, ouvrez le dossier créé qui contient vos fichiers d’application nouvellement générés. Double-cliquez sur le fichier solution « . sln » pour ouvrir le fichier solution dans Visual Studio.

    >[!NOTE]
    >Veillez à ouvrir le dossier nouvellement créé (par exemple, le dossier « application », si vous suivez les conventions d’affectation des noms des étapes précédentes), car il y aura un fichier. sln de même nom en dehors de ce dossier qui est différent du fichier. sln dans le dossier Build. 

    ![mrlearning-Speech-CH1-2-step7](images/mrlearning-speach-ch1-2-step7.jpg)

    >[!NOTE]
    >Si Visual Studio vous invite à installer de nouveaux composants, assurez-vous que tous les composants requis sont installés comme indiqué dans [la page « installer les outils »](install-the-tools.md) .

8. Branchez l’appareil HoloLens 2 à votre PC avec le câble USB. Bien que les instructions de cette leçon supposent que vous déployez un test avec un appareil HoloLens 2, vous pouvez choisir d’effectuer le déploiement sur l’[émulateur HoloLens 2](using-the-hololens-emulator.md) ou de créer un [package d’application pour effectuer un chargement indépendant](<https://docs.microsoft.com//windows/uwp/packaging/packaging-uwp-apps>).

9. Avant d’effectuer la génération sur votre appareil, vérifiez que ce dernier est en mode développeur. S’il s’agit de votre premier déploiement sur l’appareil HoloLens 2, Visual Studio peut vous demander de l’associer à un code confidentiel. Veuillez suivre [ces instructions](https://docs.microsoft.com//windows/mixed-reality/using-visual-studio) si vous devez activer le mode développeur ou associer l’appareil à Visual Studio.

10. Configurez Visual Studio en vue d’effectuer la génération sur votre appareil HoloLens 2 en sélectionnant la configuration « Release » et l’architecture « ARM ».

    ![mrlearning-Speech-CH1-2-step10](images/mrlearning-speach-ch1-2-step10.jpg)

11. L’étape finale consiste à effectuer la génération sur votre appareil en sélectionnant Déboguer > Démarrer sans débogage. Quand vous sélectionnez « Démarrer sans débogage », l’application démarre immédiatement sur votre appareil si la génération réussit, mais les informations de débogage n’apparaissent pas dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci. Vous pouvez également sélectionner Générer > Déployer la solution pour effectuer le déploiement sur votre appareil sans que l’application démarre automatiquement.

    ![mrlearning-Speech-CH1-2-step11. SITUÉE](images/mrlearning-speach-ch1-2-step11.jpg)

## <a name="congratulations"></a>Félicitations

Vous avez configuré la reconnaissance vocale dans votre application, optimisée par Azure. Exécutez l’application pour vous assurer que toutes les fonctions et fonctionnalités fonctionnent correctement. Commencez par dire le mot de mise en éveil que vous avez tapé à l’étape 25, activer terminal. Sélectionnez le bouton microphone pour démarrer la reconnaissance vocale. Commencez à parler. Vous verrez vos mots transcrits dans le terminal à mesure que vous parlez. Appuyez une deuxième fois sur le bouton microphone pour arrêter la reconnaissance vocale. Dites rejeter le terminal pour masquer le terminal Lunarcom. Dans la leçon suivante, vous apprendrez à basculer dynamiquement vers à l’aide de la reconnaissance vocale de l’appareil pour les situations où le kit de développement logiciel (SDK) Speech d’Azure n’est pas disponible en raison de la déconnexion de HoloLens 2.

[Didacticiel suivant : 2. Ajout d’un mode hors connexion pour la traduction vocale locale en texte](mrlearning-speechSDK-ch2.md)
