---
title: Tutoriels Azure Spatial Anchors - 4. Azure Spatial Anchors pour Android et iOS
description: Suivez ce tutoriel pour découvrir comment implémenter Azure Spatial Anchors au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 05/18/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, cours, hololens, azure, spatial anchors
ms.localizationpriority: high
ms.openlocfilehash: a35f73ae5aee493182f0f4990aa345d990c3f513
ms.sourcegitcommit: e65f1463aec3c040a1cd042e61fc2bd156a42ff8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83867621"
---
# <a name="4-azure-spatial-anchors-for-android-and-ios"></a>4. Azure Spatial Anchors pour Android et iOS

Dans ce tutoriel, vous allez découvrir comment créer votre projet pour des appareils Android et iOS à l’aide des packages AR Foundation, ARCore XR Plugin et ARKit XR Plugin.

## <a name="objectives"></a>Objectifs

* Découvrir comment créer votre projet pour un appareil Android à l’aide des packages Unity AR Foundation et ARCore XR Plugin
* Découvrir comment créer votre projet pour un appareil iOS à l’aide des packages Unity AR Foundation et ARKit XR Plugin

[!NOTE] Pour suivre ce tutoriel, veillez d’abord à effectuer les étapes des tutoriels Azure Spatial Anchors -> [Bien démarrer avec Azure Spatial Anchors](mrlearning-asa-ch1.md).

## <a name="adding-inbuilt-unity-packages"></a>Ajout de packages Unity intégrés

Dans cette section, vous allez installer les packages intégrés AR Foundation, ARCore XR Plugin et ARKit XR Plugin d’Unity nécessaires à la prise en charge des appareils Android et iOS.

Veillez à installer les versions listées ci-dessous de ces packages Unity :

* **AR Foundation 2.1.4**
* **ARCore XR Plugin 2.2.0 Preview 2**
* **ARKit XR Plugin 2.1.1**

[!NOTE] Si vous développez ce projet pour Android, il est inutile d’installer le package ARKit XR Plugin. De même, si vous développez ce projet pour iOS, il est inutile d’installer le package ARCore XR Plugin.

Dans le menu Unity, sélectionnez **Window** > **Package Manager** :

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-1.png)

L’affichage de tous les packages dans la liste peut prendre quelques secondes. Pour voir les packages en préversion, cliquez sur l’option Advanced, puis sélectionnez **Show preview packages**.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-2.png)

Dans la fenêtre Package Manager, sélectionnez **AR Foundation**. Sélectionnez la version 2.1.4 dans la liste, puis mettez à jour le package en cliquant sur le bouton **Update to 2.1.4** :

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-3.png)

Pour prendre en charge les appareils Android, importez le package ARCore XR Plugin 2.2.0 Preview 2 en suivant le même processus.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-4.png)

Pour prendre en charge les appareils iOS, vous devez importer le package Unity **ARKit XR Plugin 2.1.1** dans Package Manager.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section1-step1-5.png)

## <a name="customize-mrtk-to-support-ar-foundation-camera"></a>Personnaliser MRTK pour prendre en charge la caméra AR Foundation

Pour prendre en charge AR Foundation, vous devez personnaliser les paramètres de MRTK. Sélectionnez MixedRealityToolKit dans la fenêtre Hierarchy, puis cliquez sur le bouton **Clone** dans la fenêtre Inspector sous Mixed Reality ToolKit.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section2-step1-1.png)

Quand vous cliquez sur le bouton **Clone**, une fenêtre Clone Profile s’ouvre. Cliquez une nouvelle fois sur le bouton Clone pour cloner DefaultMixedRealityToolkitProfile.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section2-step1-2.png)

De même, clonez le profil de la caméra dans la fenêtre Inspector, renommez le profil en « UnityARConfigurationProfile », puis cliquez sur le bouton **Clone**. Dans la fenêtre Inspector, localisez MixedReality et sélectionnez l’onglet Camera. Ensuite, développez Camera Settings Providers dans la fenêtre Inspector, puis cliquez sur **+Add Camera Setting Provider** > développez **New data provider 1** > sélectionnez **None** comme Type > sélectionnez **Microsoft.MixedReality.Toolkit.Experimental.UnityAR** > sélectionnez **UnityARCameraSettings**.


![mrlearning-asa](images/mrlearning-asa/tutorial4-section2-step1-3.png)

L’objet MixedRealityToolKit étant sélectionné dans la fenêtre Hierarchy, passez à la fenêtre Inspector pour attacher les scripts de prise en charge. Pour cela, cliquez sur le bouton **Add Component**, tapez AR Reference Point Manager et sélectionnez le script.

L’ajout du script « AR Reference Point Manager » ajoute automatiquement « AR Session Origin » dans la fenêtre Inspector. Une fois les scripts de prise en charge ajoutés, la fenêtre Inspector doit ressembler à ceci.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section2-step1-4.png)

## <a name="build-application-to-android-device"></a>Créer une application pour un appareil Android

Pour créer cette application pour votre appareil Android, cliquez sur **File** en haut de la fenêtre, puis sélectionnez **Build Settings**. Dans la fenêtre qui s’ouvre, sélectionnez **Android**, puis cliquez sur **Switch Platform**. Le changement de plateforme prend quelques minutes. Après avoir basculé vers la plateforme Android, cliquez sur **Add Open Scenes** et vérifiez que votre scène actuelle est la seule sélectionnée dans la liste **Scenes In Build**.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section3-step1-1.png)

Fermez la fenêtre **Build Settings**. Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project**, puis cliquez sur **Apply** pour configurer le projet Unity pour la plateforme Android.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section3-step1-2.png)

Dans le menu Unity, sélectionnez **Edit** > **Project Settings** pour ouvrir la fenêtre Project Settings. Dans la fenêtre Project Settings, sélectionnez l’onglet **Player**, développez la section Other Settings, sélectionnez **Vulkan**, puis supprimez-le en cliquant sur le symbole « - ».

![mrlearning-asa](images/mrlearning-asa/tutorial4-section3-step1-3.png)

Fermez la fenêtre Player Settings et rouvrez la fenêtre Build Settings. Ensuite, à l’aide d’un câble USB, connectez votre appareil Android à votre ordinateur, sélectionnez votre appareil dans la liste déroulante **Build and Run on**, puis cliquez sur **Build And Run**. Vous êtes alors invité à enregistrer un fichier .apk avec le nom de votre choix.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section3-step1-4.png)

> [!NOTE]
> Si vous recevez une erreur dans la fenêtre Unity Console relative aux modules Android SDK, NDK et/ou JDK, vous devez ouvrir Unity Hub et installer les modules SDK, NDK et JDK associés pour le module Android Build Support.

Une fois le processus de génération terminé, vos applications doivent se charger automatiquement sur votre appareil Android.

## <a name="build-application-to-ios-device"></a>Créer une application pour un appareil iOS

Pour créer cette application pour votre appareil iOS, cliquez sur **File** en haut de la fenêtre, puis sélectionnez **Build Settings**. Dans la fenêtre qui s’ouvre, sélectionnez **iOS**, puis cliquez sur **Switch Platform**.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section4-step1-1.png)

Fermez la fenêtre **Build Settings**. Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Utilities** > **Configure Unity Project**, puis cliquez sur **Apply** pour configurer le projet Unity pour la plateforme iOS.

![mrlearning-asa](images/mrlearning-asa/tutorial4-section4-step1-2.png)

Pour générer le projet XCode iOS, accédez à Build Settings, puis cliquez sur **Build**.

Suivez [ce guide](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-ios#export-the-xcode-project) pour découvrir comment déployer ce projet sur votre appareil iOS.

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez vu comment créer votre projet pour des appareils Android et iOS. Vous avez également appris à utiliser les packages AR Foundation, ARCore XR Plugin et ARKit XR Plugin pour faire fonctionner votre projet sur des appareils Android et iOS.