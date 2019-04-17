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
# <a name="mrtk-packages"></a>Packages MRTK

Le Kit de ressources de réalité mixte (MRTK) est une collection de packages qui permettent le développement d’applications inter-plateformes réalité mixte en fournissant la prise en charge pour les plateformes et de matériel de réalité mixte de manière modulaire.

Il existe trois catégories de packages MRTK : 

* [Foundation](#foundation-packages)
* [Extension](#extension-packages)
* [Expérimental](#experimental-packages)

## <a name="foundation-packages"></a>Packages de base

La base de kit de ressources de réalité mixte est l’ensemble des packages qui permettent à votre application tirer parti des fonctionnalités communes entre des plateformes de réalité mixte. Ces packages sont publiés et pris en charge par Microsoft à partir du code source dans le [mrtk_release](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/mrtk_release) branche sur GitHub.

![Packages de base MRTK](images/mrtk-foundation.jpg)

*Packages de base de kit de ressources de réalité mixtes*

La Fondation MRTK se compose de :

* [Package de base](#core-package)
* [Fournisseurs de plateforme](#platform-providers)
* [Services système](#system-services)
* [Ressources de fonctionnalité](#feature-assets)

Les sections suivantes décrivent les types de packages dans chaque catégorie.

### <a name="core-package"></a>Package de base

Le package de base est un _requis_ composant et est considérée comme une dépendance par tous les packages de foundation MRTK.

Le package MRTK Core inclut :

* [Common interfaces, classes et types de données](#common-interfaces-clases-and-data-types)
* [Composant de scène MixedRealityToolkit](#mixedrealitytoolkit-scene-component)
* [Nuanceur Standard MRTK](#mrtk-standard-shader)
* [Fournisseur d’entrée Unity](#unity-input-provider)
* [Gestion des packages](#package-management)

#### <a name="common-interfaces-classes-and-data-types"></a>Common interfaces, classes et types de données

Le package de base de kit de ressources de réalité mixte contient les définitions pour toutes les interfaces courantes, classes et types de données qui sont utilisés par tous les autres composants. Il est vivement recommandé que les applications accéder aux composants MRTK exclusivement via les interfaces définies pour permettre le plus haut niveau de compatibilité entre plateformes.

#### <a name="mixedrealitytoolkit-scene-component"></a>Composant de scène MixedRealityToolkit

Le composant de la scène MixedRealityToolkit est le Gestionnaire de ressources unique, centralisée pour le Kit de ressources de réalité mixte. Ce composant charge et gère la durée de vie des modules de plateforme et de service et fournit des ressources pour les systèmes à accéder à leurs paramètres de configuration. 

#### <a name="mrtk-standard-shader"></a>Nuanceur Standard MRTK

Le nuanceur Standard MRTK fournit la base de presque tous les documents de fournie par le MRTK. Ce nuanceur est extrêmement flexible et optimisé pour les diverses plateformes sur lequel MRTK est pris en charge. Il est _hautement_ recommandé que les documents de votre application utilisent le nuanceur standard MRTK pour des performances optimales.

#### <a name="unity-input-provider"></a>Fournisseur d’entrée Unity

Le fournisseur d’entrées de Unity fournit l’accès à des périphériques d’entrée communs tels que les contrôleurs de jeu, les écrans tactiles et une souris spatiale 3D.

#### <a name="package-management"></a>Gestion des packages

_Bientôt disponible_

Le package de base de kit de ressources de réalité mixte prend en charge pour la découverte et la gestion de la foundation facultative, d’extension et les packages MRTK expérimentales.

### <a name="platform-providers"></a>Fournisseurs de plateforme

Les packages de fournisseur de plateforme MRTK sont les composants qui activent les fonctionnalités de plateforme et le Toolkit de réalité mixte pour cibler le matériel de réalité mixte.

Plateformes prises en charge sont les suivantes :

* [Windows Mixed Reality](#windows-mixed-reality)
* [OpenVR](#openvr)
* [Vocale de Windows](#windows-voice)

#### <a name="windows-mixed-reality"></a>Windows Mixed Reality

Le package Windows Mixed Reality prend en charge pour les appareils Microsoft HoloLens et Windows mixte réalité immersives. Le package contient le support de plate-forme complet, y compris :

* Ciblage des regards
* Mouvements
* Contrôleurs de mouvement de réalité mixte Windows
* Mappage spatial

#### <a name="openvr"></a>OpenVR

Le package OpenVR fournit la plate-forme matérielle et prendre en charge pour les appareils à l’aide de la plateforme OpenVR.

#### <a name="windows-voice"></a>Vocale de Windows

Le package vocale de Windows prend en charge pour la fonctionnalité de reconnaissance et la dictée de mot clé sur les périphériques Microsoft Windows 10.

### <a name="system-services"></a>Services système

Services de plateforme centraux sont fournis dans les packages de service système. Ces packages contiennent les implémentations par défaut du Toolkit de réalité mixte les système d’interfaces de service, définis dans le [core](#core-package) package.

La Fondation MRTK inclut les services système suivants :

* [Limite système](#boundary-system)
* [Système de diagnostic](#diagnostic-system)
* [Système d’entrée](#input-system)
* [Système de reconnaissance spatiale](#spatial-awareness-system)
* [Teleport système](#teleport-system)

#### <a name="boundary-system"></a>Limite système

Le système limite MRTK fournit des données sur la réalité en virtuel playspace. Sur les systèmes pour lesquels l’utilisateur a configuré la limite, le système peut fournir un plan d’étage, playspace rectangulaire, suivies de zone et bien plus encore.

#### <a name="diagnostic-system"></a>Système de diagnostic

Le système de Diagnostic MRTK fournit des données de performances en temps réel au sein de votre expérience de l’application. À un aperçu, vous serez en mesure d’afficher la fréquence d’images, de temps processeur et d’autres mesures de performances clés que vous utilisez votre application.

#### <a name="input-system"></a>Système d’entrée

Les systèmes d’entrée MRTK permet aux applications d’accéder à des entrées de manière inter-plateformes en spécifiant les actions de l’utilisateur et en affectant ces actions aux boutons plus appropriée et aux axes sur les contrôleurs de cible.

#### <a name="spatial-awareness-system"></a>Système de reconnaissance spatiale

Le système de reconnaissance spatiale MRTK permet d’accéder aux données de l’environnement réel à partir d’appareils tels que le Microsoft HoloLens.

#### <a name="teleport-system"></a>Teleport système

Le système de Teleport MRTK prend en charge de locomotion de réalité virtuelle.

### <a name="feature-assets"></a>Ressources de fonctionnalité

Ressources de fonctionnalité sont des collections de fonctionnalités connexes fournies sous forme de scripts et les ressources de Unity. Certaines de ces fonctionnalités sont les suivantes :

* Contrôles d’Interface utilisateur
* Ressources standard
* more

## <a name="extension-packages"></a>Packages d’extension

Packages d’Extension de MRTK sont une collection de packages écrite par Microsoft et la Communauté qui étendent et améliorent les fonctionnalités de la boîte à outils de réalité mixte. Auteurs de l’extension d’état les dépendances requises, marquer le package comme étant compatible avec le Kit de ressources de réalité mixte et fournir des licences et prennent en charge les instructions.

Packages d’extension peuvent fournir de nouvelles fonctionnalités et la nouvelle prise en charge de la plateforme. Au fil du temps, les extensions peuvent, avec l’assistance et l’approbation des auteurs, être migrées dans la base de MRTK, moment auquel elles seront publiées et prises en charge par Microsoft.

![Package d’Extension MRTK](images/mrtk-extensions.jpg)

*Packages d’Extension de kit de ressources de réalité mixtes*

## <a name="experimental-packages"></a>Packages expérimentales

Packages expérimentales offrent la possibilité aux fonctionnalités de prototype de vol, les versions préliminaires et les nouvelles idées intéressantes. L’objectif de packages plus expérimentales est d’essayer quelque chose de nouveau et à évaluer l’intérêt du client. Nombreuses, mais pas toutes, packages expérimentales sera republiés en tant qu’extensions une fois le prototypage et la phase de test se termine.

![Packages expérimentales MRTK](images/mrtk-experimental.jpg)

*Packages expérimentale du Kit de ressources réalité mixtes*

## <a name="conclusion"></a>Conclusion

Les packages du Kit de ressources de réalité mixte et le système de gestion de package sont conçus pour activer une méthode propre et simple de feu générer des fonctionnalités dans vos expériences sans nécessiter de composants inutiles à inclure dans le projet.

Au fil du temps, prise en charge de gestion de package est ajouté et amélioré dans la boîte à outils de réalité mixte. Si vous avez des commentaires ou que vous souhaitez participer, veuillez visiter le [projet du Kit de ressources de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity) sur GitHub. 

## <a name="see-also"></a>Voir aussi

* [MixedRealityToolkit-Unity (GitHub)](https://github.com/Microsoft/MixedRealityToolkit-Unity)

