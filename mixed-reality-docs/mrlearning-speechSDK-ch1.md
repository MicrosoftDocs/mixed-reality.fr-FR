---
title: Tutoriels sur les services Azure Speech - 1. Intégration et utilisation de la reconnaissance vocale et de la transcription
description: Suivez ce cours pour découvrir comment implémenter le SDK Azure Speech au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: f376ab268e9c2869e48b325fa728672a16ee6d32
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86303680"
---
# <a name="1-integrating-and-using-speech-recognition-and-transcription"></a>1. Intégration et utilisation de la reconnaissance vocale et de la transcription

## <a name="overview"></a>Vue d’ensemble


Dans cette série de tutoriels, vous allez créer une application de réalité mixte qui explore l’utilisation des services Azure Speech avec le HoloLens 2. À la fin de cette série de tutoriels, vous serez en mesure d’utiliser le microphone de votre appareil pour convertir la parole en texte en temps réel, traduire votre parole en d’autres langues et exploiter la fonctionnalité Reconnaissance de l’intention pour comprendre des commandes vocales à l’aide de l’intelligence artificielle.

## <a name="objectives"></a>Objectifs

* Apprendre à intégrer les services Azure Speech à une application HoloLens 2
* Apprendre à utiliser la reconnaissance vocale pour transcrire du texte

## <a name="prerequisites"></a>Prérequis

>[!TIP]
>Si vous n’avez pas encore terminé la série de [tutoriels de démarrage](mr-learning-base-01.md), nous vous conseillons de le faire avant d’aller plus loin.

* PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Capacité de programmation C# de base
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)
* <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté

> [!IMPORTANT]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X. Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.

## <a name="creating-and-preparing-the-unity-project"></a>Création et préparation du projet Unity

Dans cette section, vous allez créer un projet Unity et le préparer au développement avec MRTK.

Pour cela, suivez d’abord [Initialisation de votre projet et de votre première application](mr-learning-base-02.md), en excluant les instructions données dans [Générer votre application sur votre appareil](mr-learning-base-02.md#building-your-application-to-your-hololens-2), ce qui inclut les étapes suivantes :

1. [Création du projet Unity](mr-learning-base-02.md#creating-the-unity-project) et affectation d’un nom pertinent, par exemple *MRTK Tutorials*
2. [Changement de plateforme de génération](mr-learning-base-02.md#configuring-the-unity-project)
3. [Importation des ressources TextMeshPro Essential](mr-learning-base-02.md#importing-the-textmeshpro-essential-resources)
4. [Importation du Mixed Reality Toolkit](mr-learning-base-02.md#importing-the-mixed-reality-toolkit)
5. [Configuration du projet Unity](mr-learning-base-02.md#configuring-the-unity-project)
6. [Création et configuration de la scène](mr-learning-base-02.md#creating-and-configuring-the-scene), et affectation d’un nom pertinent à la scène, par exemple *AzureSpeechServices*

Ensuite, suivez les instructions de [Modification de l’option d’affichage de la reconnaissance spatiale](mr-learning-base-03.md#changing-the-spatial-awareness-display-option) pour remplacer le profil de configuration MRTK de votre scène par **DefaultHoloLens2ConfigurationProfile** et remplacer les options d’affichage du maillage de la reconnaissance spatiale par **Occlusion**.

## <a name="configuring-the-speech-commands-start-behavior"></a>Configuration du comportement de démarrage des commandes vocales

Étant donné que vous allez utiliser le SDK Speech pour la reconnaissance vocale et la transcription, vous avez besoin de configurer les commandes vocales MRTK se sorte qu’elles n’interfèrent pas avec la fonctionnalité du SDK Speech. Pour cela, vous pouvez modifier le comportement de démarrage des commandes vocales en passant d’un démarrage automatique à un démarrage manuel.

Avec l’objet **MixedRealityToolkit** sélectionné dans la fenêtre Hierarchy, dans la fenêtre Inspector, sélectionnez l’onglet **Input**, clonez **DefaultHoloLens2InputSystemProfile** et **DefaultMixedRealitySpeechCommandsProfile**, puis remplacez le comportement de démarrage (**Start Behavior**) des commandes vocales en choisissant **Manual Start** :

![mrlearning-speech](images/mrlearning-speech/tutorial1-section2-step1-1.png)

> [!TIP]
> Pour vous rappeler comment cloner et configurer des profils MRTK, reportez-vous aux instructions fournies dans [Configuration des profils Mixed Reality Toolkit](mr-learning-base-03.md).

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
> Pour vous rappeler comment importer un package personnalisé Unity, reportez-vous aux instructions fournies dans [Importation du Mixed Reality Toolkit](mr-learning-base-02.md#importing-the-mixed-reality-toolkit).

Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :

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
