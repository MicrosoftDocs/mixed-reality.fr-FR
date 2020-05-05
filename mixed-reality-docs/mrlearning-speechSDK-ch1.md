---
title: Tutoriels sur les services Azure Speech - 1. Intégration et utilisation de la reconnaissance vocale et de la transcription
description: Suivez ce cours pour découvrir comment implémenter le SDK Azure Speech au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 71a6c2124258f05e80e624b940386db72a36070b
ms.sourcegitcommit: 92ff5478a5c55b4e2c5cc2f44f1588702f4ec5d1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82604980"
---
# <a name="1-integrating-and-using-speech-recognition-and-transcription"></a>1. Intégration et utilisation de la reconnaissance vocale et de la transcription

## <a name="overview"></a>Vue d’ensemble


Dans cette série de tutoriels, vous allez créer une application de réalité mixte qui explore l’utilisation des services Azure Speech avec le HoloLens 2. À la fin de cette série de tutoriels, vous serez en mesure d’utiliser le microphone de votre appareil pour convertir la parole en texte en temps réel, traduire votre parole en d’autres langues et exploiter la fonctionnalité Reconnaissance de l’intention pour comprendre des commandes vocales à l’aide de l’intelligence artificielle.

## <a name="objectives"></a>Objectifs

* Apprendre à intégrer les services Azure Speech à une application HoloLens 2
* Apprendre à utiliser la reconnaissance vocale pour transcrire du texte

## <a name="prerequisites"></a>Prérequis

>[!TIP]
>Si vous n’avez pas encore terminé la série de [tutoriels de démarrage](mrlearning-base.md), nous vous conseillons de le faire avant d’aller plus loin.

* PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Capacité de programmation C# de base
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)
* <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté

> [!IMPORTANT]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X. Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.

## <a name="creating-and-preparing-the-unity-project"></a>Création et préparation du projet Unity

Dans cette section, vous allez créer un projet Unity et le préparer au développement avec MRTK.

Pour cela, suivez d’abord [Initialisation de votre projet et de votre première application](mrlearning-base-ch1.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device), ce qui inclut les étapes suivantes :

1. [Créer un projet Unity](mrlearning-base-ch1.md#create-new-unity-project) et lui donner un nom approprié, par exemple *MRTK Tutorials*

2. [Configurer le projet Unity pour Windows Mixed Reality](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality)

3. [Importer les ressources essentielles TextMeshPro](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources)

4. [Importer Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit)

5. [Configurer le projet Unity pour Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit)

6. [Ajouter Mixed Reality Toolkit à la scène Unity](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) et donner à la scène un nom approprié, par exemple *AzureSpeechServices*

Ensuite, suivez les instructions du [Guide pratique pour configurer les profils Mixed Reality Toolkit (Modifier l’option d’affichage de la sensibilisation spatiale)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) pour remplacer le profil de configuration MRTK de votre scène par **DefaultHoloLens2ConfigurationProfile** et pour remplacer les options d’affichage du maillage de la sensibilisation spatiale par **Occlusion**.

> [!CAUTION]
> Comme mentionné dans les instructions de l’étape [Configurer le projet Unity pour Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) dont le lien est disponible ci-dessus, il est fortement recommandé de ne pas activer MSBuild pour Unity.

## <a name="configuring-the-speech-commands-start-behavior"></a>Configuration du comportement de démarrage des commandes vocales

Étant donné que vous allez utiliser le SDK Speech pour la reconnaissance vocale et la transcription, vous avez besoin de configurer les commandes vocales MRTK se sorte qu’elles n’interfèrent pas avec la fonctionnalité du SDK Speech. Pour cela, vous pouvez modifier le comportement de démarrage des commandes vocales en passant d’un démarrage automatique à un démarrage manuel.

Avec l’objet **MixedRealityToolkit** sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, sélectionnez l’onglet **Input**, clonez **DefaultHoloLens2InputSystemProfile** et **DefaultMixedRealitySpeechCommandsProfile**, puis remplacez le comportement de démarrage (**Start Behavior**) des commandes vocales en choisissant **Manual Start** :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section2-step1-1.png)

> [!TIP]
> Pour obtenir un rappel sur la façon de cloner et de configurer des profils MRTK, vous pouvez vous reportez aux instructions données dans le [Guide pratique pour configurer les profils Mixed Reality Toolkit (Modifier l’option d’affichage de la sensibilisation spatiale)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option).

## <a name="configuring-the-capabilities"></a>Configuration des fonctionnalités

Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, puis recherchez la section **Player** >  **Publishing Settings** :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section3-step1-1.png)

Dans la section **Publishing Settings**, accédez à la section **Capabilities** et vérifiez que les fonctionnalités **InternetClient**, **Microphone** et **SpatialPerception**, que vous avez activées lors de la création du projet au début de ce tutoriel, sont cochées. Activez ensuite les fonctionnalités **InternetClientServer** et **PrivateNetworkClientServer** :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section3-step1-2.png)

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du tutoriel

Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre dans lequel ils sont listés** :

* [Microsoft.CognitiveServices.Speech.N.N.N.unitypackage](https://aka.ms/csspeech/unitypackage) (dernière version)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.3/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.3.unitypackage)
* [MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpeechServices.2.3.0.0.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-speech-services-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpeechServices.2.3.0.0.unitypackage)

> [!TIP]
> Pour obtenir un rappel sur la façon d’importer un package personnalisé Unity, vous pouvez vous reporter aux instructions données dans [Importer Mixed Reality Toolkit](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit).

Une fois que vous avez importé les ressources du tutoriel, votre fenêtre de projet doit ressembler à ceci :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section4-step1-1.png)

## <a name="preparing-the-scene"></a>Préparation de la scène

Dans cette section, vous allez préparer la scène en ajoutant le préfabriqué du tutoriel et configurer le composant Lunarcom Controller (Script) pour contrôler votre scène.

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureSpeechServices** > **Prefabs** et faites glisser le préfabriqué **Lunarcom** dans la fenêtre Hierarchy pour l’ajouter à votre scène :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-1.png)

Avec l’objet **Lunarcom** toujours sélectionné dans la fenêtre Hierachy, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Controller (Script)** à l’objet Lunarcom :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-2.png)

> [!NOTE]
> Le composant Lunarcom Controller (Script) ne fait pas partie de MRTK. Il a été fourni avec les ressources de ce tutoriel.

L’objet **Lunarcom** étant toujours sélectionné, développez-le pour révéler ses objets enfants, puis faites glisser l’objet **Terminal** dans le champ **Terminal** du composant Lunarcom Controller (Script) :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-3.png)

Avec l’objet **Lunarcom** toujours sélectionné, développez l’objet Terminal pour révéler ses objets enfants, puis faites glisser l’objet **ConnectionLight** dans le champ **Connection Light** du composant Lunarcom Controller (Script) et l’objet **OutputText** dans le champ **Output Text** :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-4.png)

Avec l’objet **Lunarcom** toujours sélectionné, développez l’objet Buttons pour révéler ses objets enfants, puis, dans la fenêtre Inspector, développez la liste **Buttons**, définissez **Size** sur 3, puis faites glisser les objets **MicButton**, **SatelliteButton** et **RocketButton** dans les champs **Element** 0, 1 et 2 respectivement :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section5-step1-5.png)

## <a name="connecting-the-unity-project-to-the-azure-resource"></a>Connexion du projet Unity à la ressource Azure

Pour utiliser les services Azure Speech, vous devez créer une ressource Azure et obtenir une clé API pour le service Speech. Suivez les instructions données dans [Essayer le service Speech gratuitement](https://docs.microsoft.com/azure/cognitive-services/speech-service/get-started) et notez votre région de service (également appelée Emplacement) ainsi que votre clé API (également appelée Key1 ou Key2).

Dans la fenêtre Hierarchy, sélectionnez l’objet **Lunarcom**, puis dans la fenêtre Inspector, localisez la section **Speech SDK Credentials** du composant **Lunarcom Controller (Script)** et configurez-la de la façon suivante :

* Dans le champ **Speech Service API Key**, entrez votre clé API (Key1 or Key2).
* Dans le champ **Speech Service Region**, entrez votre région de service (Emplacement) en utilisant des lettres minuscules et en supprimant les espaces.

![mrlearning-speech](images/mrlearning-speech/tutorial1-section6-step1-1.png)

## <a name="using-speech-recognition-to-transcribe-speech"></a>Utilisation de la reconnaissance vocale pour transcrire la parole

Dans la fenêtre Hierachy, sélectionnez l’objet **Lunarcom** puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Lunarcom Speech Recognizer (Script)** à l’objet Lunarcom :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section7-step1-1.png)

> [!NOTE]
> Le composant Lunarcom Speech Recognizer (Script) ne fait pas partie de MRTK. Il a été fourni avec les ressources de ce tutoriel.

Si vous entrez maintenant en mode Game, vous pouvez tester la reconnaissance vocale en commençant par appuyer sur le bouton du microphone :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section7-step1-2.png)

Ensuite, en supposant que votre ordinateur est doté d’un microphone, quand vous dites quelque chose, votre parole est transcrite sur le panneau du terminal :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section7-step1-3.png)


> [!CAUTION]
> L’application a besoin de se connecter à Azure, donc vérifiez que votre ordinateur/appareil est connecté à Internet.

## <a name="congratulations"></a>Félicitations

Vous avez implémenté la technologie Azure de reconnaissance vocale. Exécutez l’application sur votre appareil pour vérifier que tout fonctionne bien.

Dans le tutoriel suivant, vous allez apprendre à exécuter des commandes à l’aide de la reconnaissance vocale Azure.

[Tutoriel suivant : 2. Utilisation de la reconnaissance vocale pour exécuter des commandes](mrlearning-speechSDK-ch2.md)
