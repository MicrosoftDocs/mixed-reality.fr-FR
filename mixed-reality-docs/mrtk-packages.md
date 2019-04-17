---
title: Packages MRTK
description: Cet article décrit les packages qui composent le Toollkit de réalité mixte de Microsoft.
author: davidkline-ms
ms.author: davidkl
ms.date: 02/12/19
ms.topic: article
keywords: Windows Mixed Reality, MRTK, composant, le package
ms.openlocfilehash: 7e44d75e1c267cff0ba67dd86dabfaa51bce659d
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596941"
---
# <a name="mrtk-packages"></a><span data-ttu-id="82b11-104">Packages MRTK</span><span class="sxs-lookup"><span data-stu-id="82b11-104">MRTK packages</span></span>

<span data-ttu-id="82b11-105">Le Kit de ressources de réalité mixte (MRTK) est une collection de packages qui permettent le développement d’applications inter-plateformes réalité mixte en fournissant la prise en charge pour les plateformes et de matériel de réalité mixte de manière modulaire.</span><span class="sxs-lookup"><span data-stu-id="82b11-105">The Mixed Reality Toolkit (MRTK) is a collection of packages that enable cross platform Mixed Reality application development by providing support for Mixed Reality hardware and platforms in a componentized manner.</span></span>

<span data-ttu-id="82b11-106">Il existe trois catégories de packages MRTK :</span><span class="sxs-lookup"><span data-stu-id="82b11-106">There are three categories of MRTK packages:</span></span> 

* [<span data-ttu-id="82b11-107">Foundation</span><span class="sxs-lookup"><span data-stu-id="82b11-107">Foundation</span></span>](#foundation-packages)
* [<span data-ttu-id="82b11-108">Extension</span><span class="sxs-lookup"><span data-stu-id="82b11-108">Extension</span></span>](#extension-packages)
* [<span data-ttu-id="82b11-109">Expérimental</span><span class="sxs-lookup"><span data-stu-id="82b11-109">Experimental</span></span>](#experimental-packages)

## <a name="foundation-packages"></a><span data-ttu-id="82b11-110">Packages de base</span><span class="sxs-lookup"><span data-stu-id="82b11-110">Foundation Packages</span></span>

<span data-ttu-id="82b11-111">La base de kit de ressources de réalité mixte est l’ensemble des packages qui permettent à votre application tirer parti des fonctionnalités communes entre des plateformes de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="82b11-111">The Mixed Reality Toolkit Foundation is the set of packages that enable your application to leverage common functionality across Mixed Reality Platforms.</span></span> <span data-ttu-id="82b11-112">Ces packages sont publiés et pris en charge par Microsoft à partir du code source dans le [mrtk_release](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/mrtk_release) branche sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="82b11-112">These packages are released and supported by Microsoft from source code in the [mrtk_release](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/mrtk_release) branch on GitHub.</span></span>

![Packages de base MRTK](images/mrtk-foundation.jpg)

<span data-ttu-id="82b11-114">*Packages de base de kit de ressources de réalité mixtes*</span><span class="sxs-lookup"><span data-stu-id="82b11-114">*Mixed Reality Toolkit Foundation packages*</span></span>

<span data-ttu-id="82b11-115">La Fondation MRTK se compose de :</span><span class="sxs-lookup"><span data-stu-id="82b11-115">The MRTK Foundation is comprised of:</span></span>

* [<span data-ttu-id="82b11-116">Package de base</span><span class="sxs-lookup"><span data-stu-id="82b11-116">Core Package</span></span>](#core-package)
* [<span data-ttu-id="82b11-117">Fournisseurs de plateforme</span><span class="sxs-lookup"><span data-stu-id="82b11-117">Platform Providers</span></span>](#platform-providers)
* [<span data-ttu-id="82b11-118">Services système</span><span class="sxs-lookup"><span data-stu-id="82b11-118">System Services</span></span>](#system-services)
* [<span data-ttu-id="82b11-119">Ressources de fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="82b11-119">Feature Assets</span></span>](#feature-assets)

<span data-ttu-id="82b11-120">Les sections suivantes décrivent les types de packages dans chaque catégorie.</span><span class="sxs-lookup"><span data-stu-id="82b11-120">The following sections describe the types of packages in each category.</span></span>

### <a name="core-package"></a><span data-ttu-id="82b11-121">Package de base</span><span class="sxs-lookup"><span data-stu-id="82b11-121">Core Package</span></span>

<span data-ttu-id="82b11-122">Le package de base est un _requis_ composant et est considérée comme une dépendance par tous les packages de foundation MRTK.</span><span class="sxs-lookup"><span data-stu-id="82b11-122">The core package is a _required_ component and is taken as a dependency by all MRTK foundation packages.</span></span>

<span data-ttu-id="82b11-123">Le package MRTK Core inclut :</span><span class="sxs-lookup"><span data-stu-id="82b11-123">The MRTK Core package includes:</span></span>

* [<span data-ttu-id="82b11-124">Common interfaces, classes et types de données</span><span class="sxs-lookup"><span data-stu-id="82b11-124">Common interfaces, classes and data types</span></span>](#common-interfaces-clases-and-data-types)
* [<span data-ttu-id="82b11-125">Composant de scène MixedRealityToolkit</span><span class="sxs-lookup"><span data-stu-id="82b11-125">MixedRealityToolkit scene component</span></span>](#mixedrealitytoolkit-scene-component)
* [<span data-ttu-id="82b11-126">Nuanceur Standard MRTK</span><span class="sxs-lookup"><span data-stu-id="82b11-126">MRTK Standard Shader</span></span>](#mrtk-standard-shader)
* [<span data-ttu-id="82b11-127">Fournisseur d’entrée Unity</span><span class="sxs-lookup"><span data-stu-id="82b11-127">Unity Input Provider</span></span>](#unity-input-provider)
* [<span data-ttu-id="82b11-128">Gestion des packages</span><span class="sxs-lookup"><span data-stu-id="82b11-128">Package Management</span></span>](#package-management)

#### <a name="common-interfaces-classes-and-data-types"></a><span data-ttu-id="82b11-129">Common interfaces, classes et types de données</span><span class="sxs-lookup"><span data-stu-id="82b11-129">Common interfaces, classes and data types</span></span>

<span data-ttu-id="82b11-130">Le package de base de kit de ressources de réalité mixte contient les définitions pour toutes les interfaces courantes, classes et types de données qui sont utilisés par tous les autres composants.</span><span class="sxs-lookup"><span data-stu-id="82b11-130">The Mixed Reality Toolkit Core package contains the definitions for all of the common interfaces, classes and data types that are used by all other components.</span></span> <span data-ttu-id="82b11-131">Il est vivement recommandé que les applications accéder aux composants MRTK exclusivement via les interfaces définies pour permettre le plus haut niveau de compatibilité entre plateformes.</span><span class="sxs-lookup"><span data-stu-id="82b11-131">It is highly recommended that applications access MRTK components exclusively through the defined interfaces to enable the highest level of compatibility across platforms.</span></span>

#### <a name="mixedrealitytoolkit-scene-component"></a><span data-ttu-id="82b11-132">Composant de scène MixedRealityToolkit</span><span class="sxs-lookup"><span data-stu-id="82b11-132">MixedRealityToolkit scene component</span></span>

<span data-ttu-id="82b11-133">Le composant de la scène MixedRealityToolkit est le Gestionnaire de ressources unique, centralisée pour le Kit de ressources de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="82b11-133">The MixedRealityToolkit scene component is the single, centralized resource manager for the Mixed Reality Toolkit.</span></span> <span data-ttu-id="82b11-134">Ce composant charge et gère la durée de vie des modules de plateforme et de service et fournit des ressources pour les systèmes à accéder à leurs paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="82b11-134">This component loads and manages the lifespan of the platform and service modules and provides resources for the systems to access their configuration settings.</span></span> 

#### <a name="mrtk-standard-shader"></a><span data-ttu-id="82b11-135">Nuanceur Standard MRTK</span><span class="sxs-lookup"><span data-stu-id="82b11-135">MRTK Standard Shader</span></span>

<span data-ttu-id="82b11-136">Le nuanceur Standard MRTK fournit la base de presque tous les documents de fournie par le MRTK.</span><span class="sxs-lookup"><span data-stu-id="82b11-136">The MRTK Standard Shader provides the basis for virtually all of the materials provided by the MRTK.</span></span> <span data-ttu-id="82b11-137">Ce nuanceur est extrêmement flexible et optimisé pour les diverses plateformes sur lequel MRTK est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="82b11-137">This shader is extremely flexible and optimized for the variety of platforms on which MRTK is supported.</span></span> <span data-ttu-id="82b11-138">Il est _hautement_ recommandé que les documents de votre application utilisent le nuanceur standard MRTK pour des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="82b11-138">It is _highly_ recommended that your application's materials use the MRTK standard shader for optimal performance.</span></span>

#### <a name="unity-input-provider"></a><span data-ttu-id="82b11-139">Fournisseur d’entrée Unity</span><span class="sxs-lookup"><span data-stu-id="82b11-139">Unity Input Provider</span></span>

<span data-ttu-id="82b11-140">Le fournisseur d’entrées de Unity fournit l’accès à des périphériques d’entrée communs tels que les contrôleurs de jeu, les écrans tactiles et une souris spatiale 3D.</span><span class="sxs-lookup"><span data-stu-id="82b11-140">The Unity Input Provider provides access to common input devices such as game controllers, touch screens and a 3D spatial mouse.</span></span>

#### <a name="package-management"></a><span data-ttu-id="82b11-141">Gestion des packages</span><span class="sxs-lookup"><span data-stu-id="82b11-141">Package Management</span></span>

<span data-ttu-id="82b11-142">_Bientôt disponible_</span><span class="sxs-lookup"><span data-stu-id="82b11-142">_Coming soon_</span></span>

<span data-ttu-id="82b11-143">Le package de base de kit de ressources de réalité mixte prend en charge pour la découverte et la gestion de la foundation facultative, d’extension et les packages MRTK expérimentales.</span><span class="sxs-lookup"><span data-stu-id="82b11-143">The Mixed Reality Toolkit Core package provides support for discovering and managing the optional foundation, extension and experimental MRTK packages.</span></span>

### <a name="platform-providers"></a><span data-ttu-id="82b11-144">Fournisseurs de plateforme</span><span class="sxs-lookup"><span data-stu-id="82b11-144">Platform Providers</span></span>

<span data-ttu-id="82b11-145">Les packages de fournisseur de plateforme MRTK sont les composants qui activent les fonctionnalités de plateforme et le Toolkit de réalité mixte pour cibler le matériel de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="82b11-145">The MRTK Platform Provider packages are the components that enable the Mixed Reality Toolkit to target Mixed Reality hardware and platform functionality.</span></span>

<span data-ttu-id="82b11-146">Plateformes prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="82b11-146">Supported platforms include:</span></span>

* [<span data-ttu-id="82b11-147">Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="82b11-147">Windows Mixed Reality</span></span>](#windows-mixed-reality)
* [<span data-ttu-id="82b11-148">OpenVR</span><span class="sxs-lookup"><span data-stu-id="82b11-148">OpenVR</span></span>](#openvr)
* [<span data-ttu-id="82b11-149">Vocale de Windows</span><span class="sxs-lookup"><span data-stu-id="82b11-149">Windows Voice</span></span>](#windows-voice)

#### <a name="windows-mixed-reality"></a><span data-ttu-id="82b11-150">Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="82b11-150">Windows Mixed Reality</span></span>

<span data-ttu-id="82b11-151">Le package Windows Mixed Reality prend en charge pour les appareils Microsoft HoloLens et Windows mixte réalité immersives.</span><span class="sxs-lookup"><span data-stu-id="82b11-151">The Windows Mixed Reality package provides support for Microsoft HoloLens and Windows Mixed Reality Immersive devices.</span></span> <span data-ttu-id="82b11-152">Le package contient le support de plate-forme complet, y compris :</span><span class="sxs-lookup"><span data-stu-id="82b11-152">The package contains full platform support, including:</span></span>

* <span data-ttu-id="82b11-153">Ciblage des regards</span><span class="sxs-lookup"><span data-stu-id="82b11-153">Gaze targeting</span></span>
* <span data-ttu-id="82b11-154">Mouvements</span><span class="sxs-lookup"><span data-stu-id="82b11-154">Gestures</span></span>
* <span data-ttu-id="82b11-155">Contrôleurs de mouvement de réalité mixte Windows</span><span class="sxs-lookup"><span data-stu-id="82b11-155">Windows Mixed Reality Motion controllers</span></span>
* <span data-ttu-id="82b11-156">Mappage spatial</span><span class="sxs-lookup"><span data-stu-id="82b11-156">Spatial Mapping</span></span>

#### <a name="openvr"></a><span data-ttu-id="82b11-157">OpenVR</span><span class="sxs-lookup"><span data-stu-id="82b11-157">OpenVR</span></span>

<span data-ttu-id="82b11-158">Le package OpenVR fournit la plate-forme matérielle et prendre en charge pour les appareils à l’aide de la plateforme OpenVR.</span><span class="sxs-lookup"><span data-stu-id="82b11-158">The OpenVR package provides hardware and platform support for devices using the OpenVR platform.</span></span>

#### <a name="windows-voice"></a><span data-ttu-id="82b11-159">Vocale de Windows</span><span class="sxs-lookup"><span data-stu-id="82b11-159">Windows Voice</span></span>

<span data-ttu-id="82b11-160">Le package vocale de Windows prend en charge pour la fonctionnalité de reconnaissance et la dictée de mot clé sur les périphériques Microsoft Windows 10.</span><span class="sxs-lookup"><span data-stu-id="82b11-160">The Windows Voice package provides support for keyword recognition and dictation functionality on Microsoft Windows 10 devices.</span></span>

### <a name="system-services"></a><span data-ttu-id="82b11-161">Services système</span><span class="sxs-lookup"><span data-stu-id="82b11-161">System Services</span></span>

<span data-ttu-id="82b11-162">Services de plateforme centraux sont fournis dans les packages de service système.</span><span class="sxs-lookup"><span data-stu-id="82b11-162">Core platform services are provided in system service packages.</span></span> <span data-ttu-id="82b11-163">Ces packages contiennent les implémentations par défaut du Toolkit de réalité mixte les système d’interfaces de service, définis dans le [core](#core-package) package.</span><span class="sxs-lookup"><span data-stu-id="82b11-163">These packages contain the Mixed Reality Toolkit's default implementations of the system service interfaces, defined in the [core](#core-package) package.</span></span>

<span data-ttu-id="82b11-164">La Fondation MRTK inclut les services système suivants :</span><span class="sxs-lookup"><span data-stu-id="82b11-164">The MRTK foundation includes the following system services:</span></span>

* [<span data-ttu-id="82b11-165">Limite système</span><span class="sxs-lookup"><span data-stu-id="82b11-165">Boundary System</span></span>](#boundary-system)
* [<span data-ttu-id="82b11-166">Système de diagnostic</span><span class="sxs-lookup"><span data-stu-id="82b11-166">Diagnostic System</span></span>](#diagnostic-system)
* [<span data-ttu-id="82b11-167">Système d’entrée</span><span class="sxs-lookup"><span data-stu-id="82b11-167">Input System</span></span>](#input-system)
* [<span data-ttu-id="82b11-168">Système de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="82b11-168">Spatial Awareness System</span></span>](#spatial-awareness-system)
* [<span data-ttu-id="82b11-169">Teleport système</span><span class="sxs-lookup"><span data-stu-id="82b11-169">Teleport System</span></span>](#teleport-system)

#### <a name="boundary-system"></a><span data-ttu-id="82b11-170">Limite système</span><span class="sxs-lookup"><span data-stu-id="82b11-170">Boundary System</span></span>

<span data-ttu-id="82b11-171">Le système limite MRTK fournit des données sur la réalité en virtuel playspace.</span><span class="sxs-lookup"><span data-stu-id="82b11-171">The MRTK Boundary System provides data about the to virtual reality playspace.</span></span> <span data-ttu-id="82b11-172">Sur les systèmes pour lesquels l’utilisateur a configuré la limite, le système peut fournir un plan d’étage, playspace rectangulaire, suivies de zone et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="82b11-172">On systems for which the user has configured the boundary, the system can provide a floor plane, rectangular playspace, tracked area, and more.</span></span>

#### <a name="diagnostic-system"></a><span data-ttu-id="82b11-173">Système de diagnostic</span><span class="sxs-lookup"><span data-stu-id="82b11-173">Diagnostic System</span></span>

<span data-ttu-id="82b11-174">Le système de Diagnostic MRTK fournit des données de performances en temps réel au sein de votre expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="82b11-174">The MRTK Diagnostic System provides real-time performance data within your application experience.</span></span> <span data-ttu-id="82b11-175">À un aperçu, vous serez en mesure d’afficher la fréquence d’images, de temps processeur et d’autres mesures de performances clés que vous utilisez votre application.</span><span class="sxs-lookup"><span data-stu-id="82b11-175">At a glace, you will be able to view frame rate, processor time and other key performance metrics as you use your application.</span></span>

#### <a name="input-system"></a><span data-ttu-id="82b11-176">Système d’entrée</span><span class="sxs-lookup"><span data-stu-id="82b11-176">Input System</span></span>

<span data-ttu-id="82b11-177">Les systèmes d’entrée MRTK permet aux applications d’accéder à des entrées de manière inter-plateformes en spécifiant les actions de l’utilisateur et en affectant ces actions aux boutons plus appropriée et aux axes sur les contrôleurs de cible.</span><span class="sxs-lookup"><span data-stu-id="82b11-177">The MRTK Input Systems enables applications to access input in a cross platform manner by specifying user actions and assigning those actions to the most appropriate buttons and axes on target controllers.</span></span>

#### <a name="spatial-awareness-system"></a><span data-ttu-id="82b11-178">Système de reconnaissance spatiale</span><span class="sxs-lookup"><span data-stu-id="82b11-178">Spatial Awareness System</span></span>

<span data-ttu-id="82b11-179">Le système de reconnaissance spatiale MRTK permet d’accéder aux données de l’environnement réel à partir d’appareils tels que le Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="82b11-179">The MRTK Spatial Awareness System enables access to real-world environmental data from devices such as the Microsoft HoloLens.</span></span>

#### <a name="teleport-system"></a><span data-ttu-id="82b11-180">Teleport système</span><span class="sxs-lookup"><span data-stu-id="82b11-180">Teleport System</span></span>

<span data-ttu-id="82b11-181">Le système de Teleport MRTK prend en charge de locomotion de réalité virtuelle.</span><span class="sxs-lookup"><span data-stu-id="82b11-181">The MRTK Teleport System provides virtual reality locomotion support.</span></span>

### <a name="feature-assets"></a><span data-ttu-id="82b11-182">Ressources de fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="82b11-182">Feature Assets</span></span>

<span data-ttu-id="82b11-183">Ressources de fonctionnalité sont des collections de fonctionnalités connexes fournies sous forme de scripts et les ressources de Unity.</span><span class="sxs-lookup"><span data-stu-id="82b11-183">Feature Assets are collections of related functionality delivered as Unity assets and scripts.</span></span> <span data-ttu-id="82b11-184">Certaines de ces fonctionnalités sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="82b11-184">Some of these features include:</span></span>

* <span data-ttu-id="82b11-185">Contrôles d’Interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="82b11-185">User Interface Controls</span></span>
* <span data-ttu-id="82b11-186">Ressources standard</span><span class="sxs-lookup"><span data-stu-id="82b11-186">Standard Assets</span></span>
* <span data-ttu-id="82b11-187">more</span><span class="sxs-lookup"><span data-stu-id="82b11-187">more</span></span>

## <a name="extension-packages"></a><span data-ttu-id="82b11-188">Packages d’extension</span><span class="sxs-lookup"><span data-stu-id="82b11-188">Extension Packages</span></span>

<span data-ttu-id="82b11-189">Packages d’Extension de MRTK sont une collection de packages écrite par Microsoft et la Communauté qui étendent et améliorent les fonctionnalités de la boîte à outils de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="82b11-189">MRTK Extension packages are a collection of packages written by Microsoft and the Community that extend and enhance the functionality of the Mixed Reality Toolkit.</span></span> <span data-ttu-id="82b11-190">Auteurs de l’extension d’état les dépendances requises, marquer le package comme étant compatible avec le Kit de ressources de réalité mixte et fournir des licences et prennent en charge les instructions.</span><span class="sxs-lookup"><span data-stu-id="82b11-190">Extension authors will state any required dependencies, mark the package as compatible with the Mixed Reality Toolkit and provide licensing and support statements.</span></span>

<span data-ttu-id="82b11-191">Packages d’extension peuvent fournir de nouvelles fonctionnalités et la nouvelle prise en charge de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="82b11-191">Extension packages may provide new features and new platform support.</span></span> <span data-ttu-id="82b11-192">Au fil du temps, les extensions peuvent, avec l’assistance et l’approbation des auteurs, être migrées dans la base de MRTK, moment auquel elles seront publiées et prises en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="82b11-192">Over time, extensions may, with the assistance and approval of the authors, be migrated into the MRTK Foundation at which time they will be released and supported by Microsoft.</span></span>

![Package d’Extension MRTK](images/mrtk-extensions.jpg)

<span data-ttu-id="82b11-194">*Packages d’Extension de kit de ressources de réalité mixtes*</span><span class="sxs-lookup"><span data-stu-id="82b11-194">*Mixed Reality Toolkit Extension packages*</span></span>

## <a name="experimental-packages"></a><span data-ttu-id="82b11-195">Packages expérimentales</span><span class="sxs-lookup"><span data-stu-id="82b11-195">Experimental Packages</span></span>

<span data-ttu-id="82b11-196">Packages expérimentales offrent la possibilité aux fonctionnalités de prototype de vol, les versions préliminaires et les nouvelles idées intéressantes.</span><span class="sxs-lookup"><span data-stu-id="82b11-196">Experimental packages provide the ability to flight prototype features, pre-releases and exciting new ideas.</span></span> <span data-ttu-id="82b11-197">L’objectif de packages plus expérimentales est d’essayer quelque chose de nouveau et à évaluer l’intérêt du client.</span><span class="sxs-lookup"><span data-stu-id="82b11-197">The goal of most experimental packages is to try something new and to gauge customer interest.</span></span> <span data-ttu-id="82b11-198">Nombreuses, mais pas toutes, packages expérimentales sera republiés en tant qu’extensions une fois le prototypage et la phase de test se termine.</span><span class="sxs-lookup"><span data-stu-id="82b11-198">Many, though not all, experimental packages will be re-released as extensions once the prototyping and testing phase completes.</span></span>

![Packages expérimentales MRTK](images/mrtk-experimental.jpg)

<span data-ttu-id="82b11-200">*Packages expérimentale du Kit de ressources réalité mixtes*</span><span class="sxs-lookup"><span data-stu-id="82b11-200">*Mixed Reality Toolkit Experimental packages*</span></span>

## <a name="conclusion"></a><span data-ttu-id="82b11-201">Conclusion</span><span class="sxs-lookup"><span data-stu-id="82b11-201">Conclusion</span></span>

<span data-ttu-id="82b11-202">Les packages du Kit de ressources de réalité mixte et le système de gestion de package sont conçus pour activer une méthode propre et simple de feu générer des fonctionnalités dans vos expériences sans nécessiter de composants inutiles à inclure dans le projet.</span><span class="sxs-lookup"><span data-stu-id="82b11-202">The Mixed Reality Toolkit packages and package management system are designed to enable a clean and simple method for you to additively build features into your experiences without requiring unnecessary components to be included into the project.</span></span>

<span data-ttu-id="82b11-203">Au fil du temps, prise en charge de gestion de package est ajouté et amélioré dans la boîte à outils de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="82b11-203">Over time, package management support will be added and enhanced within the Mixed Reality Toolkit.</span></span> <span data-ttu-id="82b11-204">Si vous avez des commentaires ou que vous souhaitez participer, veuillez visiter le [projet du Kit de ressources de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="82b11-204">If you have feedback or wish to get involved, please visit the [Mixed Reality Toolkit project](https://github.com/Microsoft/MixedRealityToolkit-Unity) on GitHub.</span></span> 

## <a name="see-also"></a><span data-ttu-id="82b11-205">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="82b11-205">See also</span></span>

* [<span data-ttu-id="82b11-206">MixedRealityToolkit-Unity (GitHub)</span><span class="sxs-lookup"><span data-stu-id="82b11-206">MixedRealityToolkit-Unity (GitHub)</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity)

