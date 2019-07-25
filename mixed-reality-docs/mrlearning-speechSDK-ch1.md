---
title: Module d’apprentissage de SpeechSDK-reconnaissance vocale et transcription
description: Suivez ce cours pour apprendre à implémenter le kit de développement logiciel (SDK) Azure Speech dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: c1ca44ffcaa8dced988b829d9875ebe304f14a12
ms.sourcegitcommit: c7c7e3c836373b65e319609b4e8389dea6b081de
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68460355"
---
# <a name="1-integrating-and-using-speech-recognition-and-transcription"></a>1. Intégration et utilisation de la reconnaissance vocale et de la transcription

Ce didacticiel crée une application de réalité mixte qui explore l’utilisation du kit de développement logiciel (SDK) Azure Cognitive Services Speech avec le HoloLens 2. À la fin de cette série de didacticiels, vous serez en mesure d’utiliser le microphone de votre appareil pour transcrire la parole en temps réel, traduire votre discours en d’autres langues et tirer parti de la fonctionnalité d’intention du kit de développement logiciel (SDK) Speech pour comprendre les commandes vocales à l’aide de intelligence artificielle.

## <a name="objectives"></a>Objectifs

- Découvrez comment intégrer le kit de développement logiciel (SDK) Azure Speech dans une application HoloLens 2
- En savoir plus sur l’utilisation des commandes vocales
- En savoir plus sur l’utilisation des fonctionnalités vocales en texte

## <a name="instructions"></a>Instructions

### <a name="getting-started"></a>Prise en main

1. Démarrez Unity et créez un nouveau projet. Entrez le module d’apprentissage du kit de développement logiciel (SDK) Speech Name. Choisissez un emplacement pour l’emplacement où enregistrer votre projet. Cliquez ensuite sur créer un projet.

![Module2Chapter3step1im](images/module4chapter1step1im.PNG)

> Remarque : Assurez-vous que le modèle est défini sur 3D, comme indiqué dans l’image ci-dessus.

2. Téléchargez le package Unity du [Kit d’outils de réalité mixte](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC2/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC2.unitypackage) et enregistrez-le dans un dossier sur votre ordinateur. Importez le package dans votre projet Unity. Pour obtenir des instructions détaillées sur la procédure à suivre, consultez le [module de base leçon 1](mrlearning-base-ch1.md). 

3. Téléchargez et importez le [Kit de développement logiciel (SDK) Azure Speech](https://aka.ms/csspeech/unitypackage) pour le package d’actifs Unity. Importez le package du kit de développement logiciel (SDK) Speech en cliquant sur actifs, en sélectionnant importer un package, puis en sélectionnant package personnalisé. Recherchez le package du kit de développement logiciel (SDK) Speech téléchargé précédemment et ouvrez-le pour commencer le processus d’importation. 

![Module4Chapter1step3ima](images/module4chapter1step3ima.PNG)

![Module4Chapter1step3im](images/module4chapter1step3im.PNG)

4. Dans la fenêtre contextuelle suivante, cliquez sur Importer pour commencer l’importation du package du kit de développement logiciel (SDK) Speech. Vérifiez que tous les éléments sont vérifiés comme indiqué dans l’image ci-dessous.

![Module4Chapter1step4im](images/module4chapter1step4im.PNG)

5. Téléchargez le module Asset SDK module Asset Pack, également appelé package Lunarcom en cliquant sur [ce lien](https://github.com/microsoft/MixedRealityLearning/releases/tag/Speech_2). Le package de ressources Lunarcom est un ensemble de ressources et de scripts développés pour cette série de leçons afin de présenter une utilisation pratique du kit de développement logiciel (SDK) Speech d’Azure. Il s’agit d’un terminal de commande vocale qui, au final, interviendra avec l’expérience d’assembly de module lunaire développée dans le [didacticiel du module de base.](mrlearning-base-ch6.md)

6. Importez le package de ressources Lunarcom dans votre projet Unity en suivant les étapes similaires que vous avez suivies pour importer le kit de ressources de réalité mixte et le SDK Speech.
7. Configurez la boîte à outils de réalité mixte (MRTK). Pour ce faire, cliquez sur le panneau du Toolkit de réalité mixte en haut de votre fenêtre, puis sélectionnez Ajouter à la scène et configurer.

![Module4Chapter1step7im](images/module4chapter1step7im.PNG)

![module4Chapter1step9ima](images/module4chapter1step9ima.PNG)

![module4Chapter1step9imb](images/module4chapter1step9imb.PNG)

8. Votre scène contient maintenant plusieurs nouveaux éléments à partir du MRTK. Enregistrez votre scène sous un nom différent en cliquant sur «fichier», puis sur «Enregistrer sous» et nommez votre scène SpeechScene. 

> Remarque : Si vous appuyez sur lire sur votre scène après avoir ajouté le MRTK à votre projet et qu’il n’entre pas en mode lecture, vous devrez peut-être redémarrer Unity. 

9. Avec l’objet MixedRealityToolkit sélectionné dans votre hiérarchie, cliquez sur copier et personnaliser dans le panneau Inspecteur.

![Module4Chapter1step9im](images/module4chapter1step9im.PNG)

10. De même, dans le panneau inspecteur (avec l’objet MixedRealityToolkit sélectionné dans votre hiérarchie), désactivez le système de diagnostic en désactivant la case à cocher située à droite de l’option Activer le système de diagnostic.

![Module4Chapter1step9imd](images/module4chapter1step9imd.PNG)

11. Pour activer les commandes vocales, sélectionnez le profil MRTK nouvellement créé à personnaliser. Dans ce didacticiel, nous utilisons les commandes vocales en entrée pour la reconnaissance vocale et la transcription. Permet de cloner le profil d’entrée pour apporter des modifications aux paramètres de reconnaissance vocale.

![Module4Chapter1step11imb](images/module4chapter1step11imb.PNG)

![Module4Chapter1step11imd](images/module4chapter1step11imd.PNG)

12. Une fois le profil d’entrée cloné, accédez à commandes vocales et Clonez les commandes vocales.

![Module4Chapter1step12imb](images/module4chapter1step12imb.PNG)

![Module4Chapter1step12imc](images/module4chapter1step12imc.PNG)

13. Maintenant, sous commandes vocales, accédez à «paramètres généraux» et définissez «comportement de démarrage» sur «démarrage manuel».

![Module4Chapter1step13imb](images/module4chapter1step13imb.PNG)

14. Dans le panneau projet, développez le dossier Lunarcom et faites glisser le Prefab Lunarcom_Base dans votre hiérarchie.

![Module4Chapter1step11im](images/module4chapter1step11im.PNG)

15. Sélectionnez l’objet Lunarcom_Base dans votre hiérarchie et assurez-vous que la position est définie sur x = 0, y = 0 et z = 0, ainsi que la rotation définie sur x = 0, y = 0 et z = 0. Définissez l’échelle sur lecture x = 0.008, y = 0.008 et z = 0,01.

![Module4Chapter1step12im](images/module4chapter1step12im.PNG)

16. Cliquez sur Ajouter un composant, puis recherchez et sélectionnez LunarcomController. Ce script est inclus dans le pack d’actifs Lunarcom que vous avez importé à l’étape 6.

![Module4Chapter1step13im](images/module4chapter1step13im.PNG)

17. Pour connecter notre application à Azure Cognitive Services, vous devez entrer une clé d’abonnement (également appelée clé API) pour le service vocal. Suivez les instructions [ici](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/get-started) pour obtenir une clé d’abonnement gratuite. Une fois que vous avez obtenu la clé d’abonnement, entrez-la dans le champ clé de l’API du service vocal du composant LunarcomController dans le panneau Inspecteur, comme indiqué dans l’image ci-dessous.

18. Entrez la région que vous avez choisie lorsque vous vous êtes inscrit à la clé d’abonnement dans le champ région du service vocal du composant LunarcomController dans le panneau Inspecteur. Par exemple, pour la région «ouest des États-Unis» dans «ouestr»

![Module4Chapter1step15im](images/module4chapter1step15im.PNG)

19. Dans votre hiérarchie, développez l’objet Lunarcom_Base en cliquant sur la flèche à gauche de celui-ci. Ensuite, faites de même pour son objet enfant, «terminal», comme indiqué dans l’image ci-dessous.

20. Tandis que Lunarcom_Base est sélectionné, cliquez et faites glisser Lunarcom Text de la hiérarchie vers l’emplacement du texte de sortie dans le composant LunarcomController du panneau Inspecteur, comme indiqué dans l’image ci-dessous.

21. Effectuez la même opération avec l’objet terminal dans l’emplacement terminal et l’objet de connexion Light à l’emplacement de contrôle Light de connexion.

![Module4Chapter1step18im](images/module4chapter1step18im.PNG)

22. Cliquez sur la flèche en regard de la section Lunarcom Buttons du script LunarcomController dans le panneau Inspector, puis définissez la taille sur 3. Appuyez sur entrée ou retour. Trois nouveaux champs d’élément apparaissent alors.

![Module4Chapter1step19im](images/module4chapter1step19im.PNG)

23. Développez les boutons Lunarcom en cliquant sur la flèche en regard de celle-ci dans votre hiérarchie et en utilisant le même processus que ci-dessus, faites glisser les Gameobjects MIC, satellite et Rocket vers les références des éléments 0, 1 et 2, respectivement, dans le composant LunarcomController de la Panneau de l’inspecteur. 

![Module4Chapter1step18im](images/module4chapter1step20im.PNG)

24. Sélectionnez l’objet Lunarcom_Base» dans votre hiérarchie. Cliquez sur Ajouter un composant dans le panneau Inspecteur, puis recherchez et sélectionnez LunarcomWakeWordRecognizer.

![Module4Chapter1step18im](images/module4chapter1step21im.PNG)

25. Dans l’emplacement de mise en éveil par mot, tapez activer terminal. Dans l’emplacement ignorer le mot, tapez rejeter le terminal.

![Module4Chapter1step18im](images/module4chapter1step22im.PNG)

### <a name="build-your-application-to-your-device"></a>Générer votre application sur votre appareil

1. Ouvrez à nouveau la fenêtre Paramètres de build en accédant à fichier > paramètres de Build.

![Lesson1 Chapter5 étape1](images/Lesson1Chapter5Step1.JPG)

2. Vérifiez que la scène que vous souhaitez essayer figure dans la liste « Scenes in Build » (Scènes dans la génération) en cliquant sur le bouton « Add Open Scenes » (Ajouter des scènes ouvertes).

3. Appuyez sur le bouton Build (Générer) pour commencer le processus de génération.

![Lesson1 Chapter5 step3](images/Lesson1Chapter5Step3.JPG)

4. Créez un dossier pour votre application et nommez-le. Dans l’image ci-dessous, un dossier portant le nom « App » a été créé pour contenir l’application. Cliquez sur « Select Folder » (Sélectionner le dossier) pour commencer la génération dans le dossier que vous venez de créer. Une fois la génération terminée, vous pouvez fermer la fenêtre « Build Settings » dans Unity. 

![Lesson1 Chapter5 étape 4](images/Lesson1Chapter5Step4.JPG)

> REMARQUE : Si la génération échoue, essayez de renouveler l’opération, éventuellement après avoir redémarré Unity. Si vous voyez une erreur comme « Error : CS0246 = The type or namespace name “XX” could not be found (are you missing a using directive or an assembly reference?) » (CS0246 = le type ou le nom de l’espace de noms « XX » est introuvable (une directive using ou une référence d’assembly est-elle manquante ?) », vous devrez peut-être installer [SDK Windows 10 (10.0.18362.0)](<https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk>)

5. Une fois la génération terminée, ouvrez le dossier créé qui contient vos fichiers d’application nouvellement générés. Double-cliquez sur le fichier solution «. sln» pour ouvrir le fichier solution dans Visual Studio.

> Remarque : Veillez à ouvrir le dossier créé (par exemple, le dossier « App », si vous avez suivi les conventions de nommage indiquées aux étapes précédentes), car il existe un fichier .sln portant le même nom en dehors de ce dossier qui ne doit pas être confondu avec le fichier .sln situé dans le dossier de génération. 

![Leçon 1 Chapitre 5 Étape 5](images/Lesson1Chapter5Step5.JPG)

> Remarque : Si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants requis sont installés comme spécifié dans la [page « Installer les outils »](install-the-tools.md).

6. Branchez l’appareil HoloLens 2 à votre PC avec le câble USB. Bien que les instructions de cette leçon supposent que vous déployez un test avec un appareil HoloLens 2, vous pouvez choisir d’effectuer le déploiement sur l’[émulateur HoloLens 2](using-the-hololens-emulator.md) ou de créer un [package d’application pour effectuer un chargement indépendant](<https://docs.microsoft.com/en-us/windows/uwp/packaging/packaging-uwp-apps>).

7. Avant d’effectuer la génération sur votre appareil, vérifiez que ce dernier est en mode développeur. S’il s’agit de votre premier déploiement sur l’appareil HoloLens 2, Visual Studio peut vous demander de l’associer à un code confidentiel. Veuillez suivre [ces instructions](https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio) si vous devez activer le mode développeur ou associer l’appareil à Visual Studio.

8. Configurez Visual Studio en vue d’effectuer la génération sur votre appareil HoloLens 2 en sélectionnant la configuration « Release » et l’architecture « ARM ».

![Lesson1 Chapter5 Step8](images/Lesson1Chapter5Step8.JPG)

9. L’étape finale consiste à effectuer la génération sur votre appareil en sélectionnant Déboguer > Démarrer sans débogage. Quand vous sélectionnez « Démarrer sans débogage », l’application démarre immédiatement sur votre appareil si la génération réussit, mais les informations de débogage n’apparaissent pas dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci. Vous pouvez également sélectionner Générer > Déployer la solution pour effectuer le déploiement sur votre appareil sans que l’application démarre automatiquement.

![Lesson1 Chapter5 Step9](images/Lesson1Chapter5Step9.JPG)

## <a name="congratulations"></a>Félicitations

Vous avez configuré la reconnaissance vocale dans votre application, optimisée par Azure. Exécutez l’application pour vous assurer que toutes les fonctions et fonctionnalités fonctionnent correctement. Commencez par dire le mot de mise en éveil que vous avez tapé à l’étape 22, activer terminal. Sélectionnez le bouton microphone pour démarrer la reconnaissance vocale. Commencez à parler. Vous verrez vos mots transcrits dans le terminal à mesure que vous parlez. Appuyez une deuxième fois sur le bouton microphone pour arrêter la reconnaissance vocale. Dites rejeter le terminal pour masquer le terminal Lunarcom. Dans la leçon suivante, nous allons apprendre à utiliser de manière dynamique la reconnaissance vocale de l’appareil pour les situations où le kit de développement logiciel (SDK) Speech d’Azure n’est pas disponible en raison de la déconnexion de HoloLens 2.

[Didacticiel suivant: 2. Ajout d’un mode hors connexion pour la traduction de parole en texte locale](mrlearning-speechSDK-ch2.md)

