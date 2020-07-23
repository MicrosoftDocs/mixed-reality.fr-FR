---
title: Tutoriels sur les fonctionnalités multiutilisateurs - 1. Introduction
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: eff600ba6388732ab9aa200ce41494cac1dddf35
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86305826"
---
# <a name="1-introduction"></a><span data-ttu-id="ff3d5-105">1. Introduction</span><span class="sxs-lookup"><span data-stu-id="ff3d5-105">1. Introduction</span></span>

## <a name="overview"></a><span data-ttu-id="ff3d5-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="ff3d5-106">Overview</span></span>

<span data-ttu-id="ff3d5-107">Bienvenue dans les tutoriels sur les fonctionnalités multiutilisateurs !</span><span class="sxs-lookup"><span data-stu-id="ff3d5-107">Welcome to the Multi-User Capabilities tutorials!</span></span> <span data-ttu-id="ff3d5-108">Dans cette série de tutoriels, vous allez apprendre les bases de la création d’une expérience multiutilisateur à l’aide de <a href="https://www.photonengine.com/PUN" target="_blank">Photon Unity Networking</a> (PUN).</span><span class="sxs-lookup"><span data-stu-id="ff3d5-108">Through this tutorial series, you will learn the fundamentals of building a multi-user experience using <a href="https://www.photonengine.com/PUN" target="_blank">Photon Unity Networking</a> (PUN).</span></span> <span data-ttu-id="ff3d5-109">PUN est l’une des nombreuses options de réseau que peuvent utiliser les développeurs de réalité mixte pour créer des expériences partagées.</span><span class="sxs-lookup"><span data-stu-id="ff3d5-109">PUN is one of several networking options available to mixed reality developers to create shared experiences.</span></span>

<span data-ttu-id="ff3d5-110">Tutoriels de cette série :</span><span class="sxs-lookup"><span data-stu-id="ff3d5-110">Tutorials in this series:</span></span>

* [<span data-ttu-id="ff3d5-111">Configuration de Photon Unity Networking</span><span class="sxs-lookup"><span data-stu-id="ff3d5-111">Setting up Photon Unity Networking</span></span>](mr-learning-sharing-02.md)
* [<span data-ttu-id="ff3d5-112">Connexion de plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ff3d5-112">Connecting multiple users</span></span>](mr-learning-sharing-03.md)
* [<span data-ttu-id="ff3d5-113">Partage de mouvements d’objet avec plusieurs utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ff3d5-113">Sharing object movements with multiple users</span></span>](mr-learning-sharing-04.md)
* [<span data-ttu-id="ff3d5-114">Intégration d’Azure Spatial Anchors dans une expérience partagée</span><span class="sxs-lookup"><span data-stu-id="ff3d5-114">Integrating Azure Spatial Anchors into a shared experience</span></span>](mr-learning-sharing-05.md)

## <a name="objectives"></a><span data-ttu-id="ff3d5-115">Objectifs</span><span class="sxs-lookup"><span data-stu-id="ff3d5-115">Objectives</span></span>

* <span data-ttu-id="ff3d5-116">Apprendre à créer une application PUN et y connecter votre projet Unity</span><span class="sxs-lookup"><span data-stu-id="ff3d5-116">Learn how to create a PUN app and connect your Unity project to it</span></span>
* <span data-ttu-id="ff3d5-117">Apprendre à connecter plusieurs utilisateurs dans un environnement partagé</span><span class="sxs-lookup"><span data-stu-id="ff3d5-117">Learn how to connect multiple users in a shared experience</span></span>
* <span data-ttu-id="ff3d5-118">Apprendre à partager les mouvements d’objets avec d’autres utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ff3d5-118">Learn how to share the object movements with other users</span></span>
* <span data-ttu-id="ff3d5-119">Apprendre à obtenir un alignement spatial entre plusieurs appareils</span><span class="sxs-lookup"><span data-stu-id="ff3d5-119">Learn how to achieve spatial alignment between multiple devices</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff3d5-120">Prérequis</span><span class="sxs-lookup"><span data-stu-id="ff3d5-120">Prerequisites</span></span>

* <span data-ttu-id="ff3d5-121">Ordinateur Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)</span><span class="sxs-lookup"><span data-stu-id="ff3d5-121">A Windows 10 computer configured with the correct [tools installed](install-the-tools.md)</span></span>
* <span data-ttu-id="ff3d5-122">SDK Windows 10 (10.0.18362.0 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="ff3d5-122">Windows 10 SDK 10.0.18362.0 or later</span></span>
* <span data-ttu-id="ff3d5-123">Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)</span><span class="sxs-lookup"><span data-stu-id="ff3d5-123">A HoloLens 2 device [configured for development](using-visual-studio.md#enabling-developer-mode)</span></span>
* <span data-ttu-id="ff3d5-124"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.3.15 installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté</span><span class="sxs-lookup"><span data-stu-id="ff3d5-124"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the Universal Windows Platform Build Support module added</span></span>
* <span data-ttu-id="ff3d5-125">Avoir suivi la section [Créer une ressource d’ancres spatiales](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du tutoriel [Démarrage rapide : Créer une application HoloLens Unity qui utilise Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens).</span><span class="sxs-lookup"><span data-stu-id="ff3d5-125">Completed the [Create a Spatial Anchors resource](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) section of the [Quickstart: Create a Unity HoloLens app that uses Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) tutorial</span></span>
* <span data-ttu-id="ff3d5-126">Avoir suivi la série de [tutoriels de démarrage](mr-learning-base-01.md) ou connaître les fondamentaux d’Unity et de MRTK</span><span class="sxs-lookup"><span data-stu-id="ff3d5-126">Completed the [Getting started tutorials](mr-learning-base-01.md) series or some basic prior experience with Unity and MRTK</span></span>
* <span data-ttu-id="ff3d5-127">Avoir suivi la série de [tutoriels sur Azure Spatial Anchors](mr-learning-asa-01.md) ou avoir déjà créé des comptes Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="ff3d5-127">Completed the [Azure Spatial Anchors tutorials](mr-learning-asa-01.md) series or prior experience creating an Azure Spatial Anchors Account</span></span>
* <span data-ttu-id="ff3d5-128">Si vous envisagez d’effectuer un déploiement à la fois sur Android et sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="ff3d5-128">If you intend to deploy to Android as well as HoloLens</span></span>
  * <span data-ttu-id="ff3d5-129">Appareil Android <a href="https://developer.android.com/studio/debug/dev-options" target="_blank">en mode développeur</a> et <a href="https://developers.google.com/ar/discover/supported-devices" target="_blank">compatible avec ARCore</a> disposant d’une connexion USB à votre ordinateur Windows ou macOS</span><span class="sxs-lookup"><span data-stu-id="ff3d5-129">A <a href="https://developer.android.com/studio/debug/dev-options" target="_blank">developer enabled</a> and <a href="https://developers.google.com/ar/discover/supported-devices" target="_blank">ARCore capable</a> Android device with USB connection to your Windows or macOS computer</span></span>
  * <span data-ttu-id="ff3d5-130"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.3.15 installé et le module Android Build Support ajouté</span><span class="sxs-lookup"><span data-stu-id="ff3d5-130"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the Android Build Support module added</span></span>
* <span data-ttu-id="ff3d5-131">Si vous envisagez d’effectuer un déploiement à la fois sur iOS et sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="ff3d5-131">If you intend to deploy to iOS as well as HoloLens</span></span>
  * <span data-ttu-id="ff3d5-132">Ordinateur macOS avec les dernières versions de <a href="https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12" target="_blank">Xcode</a> et de <a href="https://cocoapods.org" target="_blank">CocoaPods</a> installées</span><span class="sxs-lookup"><span data-stu-id="ff3d5-132">A macOS computer with the latest version of <a href="https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12" target="_blank">Xcode</a> and <a href="https://cocoapods.org" target="_blank">CocoaPods</a> installed</span></span>
  * <span data-ttu-id="ff3d5-133">Appareil iOS <a href="https://developer.apple.com/documentation/arkit/verifying_device_support_and_user_permission" target="_blank">compatible avec ARKit</a> disposant d’une connexion USB à votre ordinateur macOS</span><span class="sxs-lookup"><span data-stu-id="ff3d5-133">An <a href="https://developer.apple.com/documentation/arkit/verifying_device_support_and_user_permission" target="_blank">ARKit compatible</a> iOS device with USB connection to your macOS computer</span></span>
  * <span data-ttu-id="ff3d5-134"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.3.15 installé et le module iOS Build Support ajouté</span><span class="sxs-lookup"><span data-stu-id="ff3d5-134"><a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> with Unity 2019.3.15 installed and the iOS Build Support module added</span></span>

> [!CAUTION]
> <span data-ttu-id="ff3d5-135">La version de Mixed Reality Toolkit qui est recommandée pour cette série de tutoriels est MRTK 2.4.0.</span><span class="sxs-lookup"><span data-stu-id="ff3d5-135">The recommended Mixed Reality Toolkit version for this tutorial series is MRTK 2.4.0.</span></span>

> [!CAUTION]
> <span data-ttu-id="ff3d5-136">La version Unity recommandée pour cette série de tutoriels est Unity 2019.3.15.</span><span class="sxs-lookup"><span data-stu-id="ff3d5-136">The recommended Unity version for this tutorial series is Unity 2019.3.15.</span></span> <span data-ttu-id="ff3d5-137">Cela remplace toutes les exigences de version Unity énoncées dans les prérequis indiqués ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ff3d5-137">This supersedes any Unity version requirements stated in the prerequisites linked above.</span></span>

[<span data-ttu-id="ff3d5-138">Tutoriel suivant : 2. Configuration du réseau Photon Unity</span><span class="sxs-lookup"><span data-stu-id="ff3d5-138">Next Tutorial: 2. Setting up Photon Unity Networking</span></span>](mr-learning-sharing-02.md)
