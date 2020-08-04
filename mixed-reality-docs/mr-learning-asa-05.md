---
title: Tutoriels Azure Spatial Anchors - 5. Azure Spatial Anchors pour Android et iOS
description: Suivez ce cours pour découvrir comment déployer un projet Unity avec Mixed Reality Toolkit et Azure Spatial Anchors sur Android et iOS.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens, android, ios
ms.localizationpriority: high
ms.openlocfilehash: 8c63204948b3e4aa3d25e5b2ca948798726f0838
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376541"
---
# <a name="5-azure-spatial-anchors-for-android-and-ios"></a>5. Azure Spatial Anchors pour Android et iOS

Dans ce tutoriel, vous allez découvrir comment créer votre projet pour des appareils Android et iOS à l’aide des packages AR Foundation, ARCore XR Plugin et ARKit XR Plugin.

## <a name="objectives"></a>Objectifs

* Apprendre à générer votre projet sur votre appareil Android à l’aide des packages AR Foundation et ARCore XR Plugin de Unity
* Apprendre à générer votre projet sur votre appareil iOS à l’aide des packages AR Foundation et ARKit XR Plugin de Unity

## <a name="installing-inbuilt-unity-packages"></a>Installation de packages Unity intégrés

Dans cette section, vous allez mettre à niveau et installer les packages intégrés suivants :

* AR Foundation 3.1.3
* Legacy Input Helpers 2.1.4
* ARCore XR Plugin 3.1.3 pour la prise en charge d’Android
* ARKit XR plugin 3.1.3 pour la prise en charge d’iOS

> [!CAUTION]
> Toutes les versions ne sont pas compatibles avec MRTK et seules certaines versions fonctionnent ensemble ; veillez donc à installer précisément les versions listées ci-dessus.

Dans le menu Unity, sélectionnez **Window** > **Package Manager** pour ouvrir la fenêtre Package Manager, sélectionnez **AR Foundation** > **3.1.3**, puis cliquez sur le bouton **Update to 3.1.3** pour mettre à jour le package :

![mr-learning-asa](images/mr-learning-asa/asa-05-section1-step1-1.png)

Suivez le même processus pour importer les packages restants en fonction des besoins.

> [!NOTE]
> Si vous développez ce projet pour Android, il est inutile d’installer le package ARKit XR Plugin. De même, si vous développez ce projet pour iOS, il est inutile d’installer le package ARCore XR Plugin.

## <a name="configure-mrtk-for-ar-foundation-camera"></a>Configurer MRTK pour l’appareil photo AR Foundation

Dans cette section, vous allez découvrir comment configurer MRTK pour le déploiement sur un appareil mobile.

Dans la fenêtre de hiérarchie, sélectionnez l’objet **MixedRealityToolkit**. Ensuite, dans la fenêtre de l’inspecteur, sélectionnez l’onglet **Camera**, clonez le profil de la caméra et attribuez-lui un nom pertinent, par exemple **AzureSpatialAnchors_ARCameraProfile** :

![mr-learning-asa](images/mr-learning-asa/asa-05-section2-step1-1.png)

> [!TIP]
> Pour vous rappeler comment cloner des profils MRTK, vous pouvez consulter les instructions fournies dans [Configuration des profils Mixed Reality Toolkit](mr-learning-base-03.md).

Avec l’onglet **Camera** toujours sélectionné dans la fenêtre de l’inspecteur, développez **Camera Setting Providers** (Fournisseurs de paramètres d’appareil photo), cliquez sur le bouton **+ Add Camera Setting Provider** (Ajouter un fournisseur de paramètres d’appareil photo), puis développez le **New data provider 1** qui vient d’être ajouté :

![mr-learning-asa](images/mr-learning-asa/asa-05-section2-step1-2.png)

À l’aide de la liste déroulante **Type**, sélectionnez le type **Microsoft.MixedReality.Toolkit.Experimental.UnityAR** > **UnityARCameraSettings** :

![mr-learning-asa](images/mr-learning-asa/asa-05-section2-step1-3.png)

Avec l’objet **MixedRealityToolkit** toujours sélectionné dans la fenêtre de hiérarchie, utilisez le bouton **Add Component** dans la fenêtre de l’inspecteur pour ajouter les composants suivants :

* AR Anchor Manager (Script)
* DisableDiagnosticsSystem (Script)

![mr-learning-asa](images/mr-learning-asa/asa-05-section2-step1-4.png)

> [!NOTE]
> Lorsque vous ajoutez le composant AR Reference Point Manager (Script), le composant AR Session Origin (Script) est ajouté automatiquement, car il est demandé par le composant AR Reference Point Manager (Script).

## <a name="building-your-application-to-your-android-device"></a>Génération de votre application sur votre appareil Android

Dans cette section, vous allez découvrir comment configurer votre projet pour le générer et le déployer sur un appareil Android.

Dans le menu Unity, sélectionnez **File** > **Build Settings...** pour ouvrir la fenêtre Build Settings, puis basculez vers la plateforme Android :

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-1.png)

> [!TIP]
> Pour vous rappeler comment changer de plateforme de génération, consultez les instructions fournies dans [Changement de la plateforme de génération](mr-learning-base-02.md#switching-the-build-platform).

Fermez la fenêtre Build Settings.

Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** pour ouvrir la fenêtre **MRTK Project Configurator**, vérifiez que toutes les options sont sélectionnées, puis cliquez sur le bouton **Apply** pour appliquer les paramètres :

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-2.png)

Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, recherchez la section **Player** >  **Other Settings**, sélectionnez **Vulkan** et supprimez-le en cliquant sur le symbole **« - »**  :

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-3.png)

Fermez la fenêtre Player Settings et rouvrez la fenêtre Build Settings.

Dans la fenêtre Build Settings, cliquez sur le bouton **Add Open Scenes** (Ajouter des scènes ouvertes) pour ajouter votre scène actuelle à la liste des scènes de la build (**Scenes In Build**). Ensuite, utilisez un câble USB pour connecter votre appareil Android à votre ordinateur et sélectionnez-le dans la liste déroulante **Run Device** :

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-4.png)

>[!NOTE]
> Si votre appareil n’apparaît pas dans la liste déroulante Run Device, vous devrez peut-être appuyer sur le bouton Refresh à côté de la liste déroulante.

Dans la fenêtre Build Settings, cliquez sur le bouton **Build And Run** (Générer et exécuter) pour ouvrir la fenêtre Build Android.

Choisissez un emplacement approprié où stocker votre build, par exemple _D:\MixedRealityLearning\Builds_, attribuez un nom pertinent à l’apk, par exemple _MRTKTutorials-AzureSpatialAnchors_, puis cliquez sur le bouton **Save** pour démarrer le processus de génération :

![mr-learning-asa](images/mr-learning-asa/asa-05-section3-step1-5.png)

> [!NOTE]
Si vous recevez une erreur dans la fenêtre Unity Console relative aux modules Android SDK, NDK ou JDK, vous devez ouvrir Unity Hub et installer les modules Android Build Support associés.

Une fois le processus de génération terminé, vos applications doivent se charger automatiquement sur votre appareil Android.

## <a name="building-your-application-to-your-ios-device"></a>Génération de votre application sur votre appareil iOS

Dans cette section, vous allez découvrir comment configurer votre projet pour le générer et le déployer sur votre appareil iOS.

Dans le menu Unity, sélectionnez **File** > **Build Settings...** pour ouvrir la fenêtre Build Settings et basculez vers la plateforme iOS :

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-1.png)

> [!TIP]
> Pour vous rappeler comment changer de plateforme de génération, consultez les instructions fournies dans [Changement de la plateforme de génération](mr-learning-base-02.md#switching-the-build-platform).

Fermez la fenêtre Build Settings.

Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project** pour ouvrir la fenêtre **MRTK Project Configurator**, vérifiez que toutes les options sont sélectionnées, puis cliquez sur le bouton **Apply** pour appliquer les paramètres :

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-2.png)

Dans le menu Unity, sélectionnez **Edit** > **Project Settings...** pour ouvrir la fenêtre Player Settings, recherchez la section **Player** >  **Other Settings**, et décochez la case **Strip Engine Code** (Supprimer le code du moteur) :

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-3.png)

Fermez la fenêtre Player Settings et rouvrez la fenêtre **Build Settings**.

Dans la fenêtre Build Settings, cliquez sur le bouton **Add Open Scenes** (Ajouter des scènes ouvertes) pour ajouter votre scène actuelle à la liste des scènes de la build (**Scenes In Build**) :

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-4.png)

Dans la fenêtre Build Settings, cliquez sur le bouton **Build** pour ouvrir la fenêtre Build iOS.

Choisissez un emplacement approprié où stocker votre projet Xcode, par exemple _D:\MixedRealityLearning\Builds_, créez un dossier et attribuez-lui un nom pertinent, par exemple _MRTKTutorials-AzureSpatialAnchors_, puis cliquez sur le bouton **Select Folder** pour démarrer le processus de génération :

![mr-learning-asa](images/mr-learning-asa/asa-05-section4-step1-5.png)

Une fois le processus de génération terminé, suivez les instructions fournies dans [Exporter le projet Xcode](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-ios#export-the-xcode-project) pour découvrir comment déployer votre projet Xcode sur votre appareil iOS.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à générer votre projet pour des appareils Android et iOS à l’aide des packages AR Foundation, ARCore XR Plugin et ARKit XR Plugin.
