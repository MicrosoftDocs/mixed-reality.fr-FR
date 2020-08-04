---
title: Tutoriels de démarrage - 3. Configuration des profils MRTK
description: Ce cours vous montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: d3381241bb1418fb0e1fb7e5d29d552a533faa32
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376641"
---
# <a name="3-configuring-the-mrtk-profiles"></a>3. Configuration des profils MRTK

## <a name="overview"></a>Vue d’ensemble

Dans ce tutoriel, vous allez voir comment personnaliser et configurer les profils MRTK.

Cet exemple va vous montrer comment masquer le maillage de la reconnaissance spatiale en modifiant les paramètres de l’observateur de maillage spatial. Vous pouvez cependant suivre ces mêmes principes pour personnaliser des paramètres ou des valeurs dans les profils MRTK.

## <a name="objectives"></a>Objectifs

* Apprendre à personnaliser et à configurer des profils MRTK
* Apprendre à masquer le maillage de reconnaissance spatiale

## <a name="changing-the-spatial-awareness-display-option"></a>Changement de l’option d’affichage de la reconnaissance spatiale

Les principales étapes à suivre pour masquer le maillage de la reconnaissance spatiale sont les suivantes :

1. Cloner le profil de configuration par défaut
2. Activer le système de reconnaissance spatiale
3. Cloner le profil système de reconnaissance spatiale par défaut
4. Cloner le profil d’observateur de maillage de reconnaissance spatiale par défaut
5. Changer la visibilité du maillage de reconnaissance spatiale

> [!NOTE]
> Par défaut, les profils MRTK ne sont pas modifiables. Il s’agit des modèles de profil par défaut que vous devez cloner avant de pouvoir les modifier. Il existe plusieurs couches de profils imbriquées. Par conséquent, il est courant de cloner et de modifier plusieurs profils lors de la configuration d’un ou plusieurs paramètres.

### <a name="1-clone-the-default-configuration-profile"></a>1. Cloner le profil de configuration par défaut

> [!NOTE]
> Le profil de configuration est le profil de plus haut niveau. Par conséquent, pour pouvoir modifier d’autres profils, vous devez d’abord cloner le profil de configuration.

Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit**, puis, dans la fenêtre Inspector, remplacez le profil de configuration **MixedRealityToolkit** par **DefaultHoloLens2ConfigurationProfile** :

![mr-learning-base](images/mr-learning-base/base-03-section1-step1-1.png)

Avec l’objet **MixedRealityToolkit** sélectionné, dans la fenêtre Inspector, cliquez sur le bouton **Copy & Customize** pour ouvrir la fenêtre Clone Profile :

![mr-learning-base](images/mr-learning-base/base-03-section1-step1-2.png)

Dans la fenêtre Clone Profile, en regard de **Profile Name**, entrez un nom de profil adapté comme _GettingStarted_HoloLens2ConfigurationProfile_, puis cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultHololens2ConfigurationProfile** :

![mr-learning-base](images/mr-learning-base/base-03-section1-step1-3.png)

Le profil de configuration que vous venez de créer est maintenant affecté comme profil de configuration pour votre scène :

![mr-learning-base](images/mr-learning-base/base-03-section1-step1-4.png)

Dans le menu Unity, sélectionnez **File** > **Save** pour enregistrer votre scène.

> [!TIP]
> N’oubliez pas d’enregistrer votre travail tout au long des tutoriels.

### <a name="2-enable-the-spatial-awareness-system"></a>2. Activer le système de reconnaissance spatiale

Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit**. Ensuite, dans la fenêtre Inspector, sélectionnez l’onglet **Spatial Awareness**, puis cochez la case **Enable Spatial Awareness System** :

![mr-learning-base](images/mr-learning-base/base-03-section1-step2-1.png)

### <a name="3-clone-the-default-spatial-awareness-system-profile"></a>3. Cloner le profil système de reconnaissance spatiale par défaut

Sous l’onglet **Spatial Awareness**, cliquez sur le bouton **Clone** pour ouvrir la fenêtre Clone Profile :

![mr-learning-base](images/mr-learning-base/base-03-section1-step3-1.png)

Dans la fenêtre Clone Profile, en regard de **Profile Name**, entrez un nom de profil adapté comme _GettingStarted_MixedRealitySpatialAwarenessSystemProfile_, puis cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultMixedRealitySpatialAwarenessSystemProfile** :

![mr-learning-base](images/mr-learning-base/base-03-section1-step3-2.png)

Le profil Spatial Awareness System nouvellement créé est maintenant automatiquement affecté à votre profil de configuration :

![mr-learning-base](images/mr-learning-base/base-03-section1-step3-3.png)

### <a name="4-clone-the-default-spatial-awareness-mesh-observer-profile"></a>4. Cloner le profil d’observateur de maillage de reconnaissance spatiale par défaut

Avec l’onglet **Spatial Awareness** sélectionné, développez la section **Windows Mixed Reality Spatial Mesh Observer**, puis cliquez sur le bouton **Clone** pour ouvrir la fenêtre Clone Profile :

![mr-learning-base](images/mr-learning-base/base-03-section1-step4-1.png)

Dans la fenêtre Clone Profile, en regard de **Profile Name**, entrez un nom de profil adapté comme _GettingStarted_MixedRealitySpatialAwarenessMeshObserverProfile_, puis cliquez sur le bouton **Clone** pour créer une copie modifiable de **DefaultMixedRealitySpatialAwarenessMeshObserverProfile** :

![mr-learning-base](images/mr-learning-base/base-03-section1-step4-2.png)

Le profil Spatial Awareness Mesh Observer nouvellement créé est maintenant automatiquement affecté à votre profil Spatial Awareness System :

![mr-learning-base](images/mr-learning-base/base-03-section1-step4-3.png)

### <a name="5-change-the-visibility-of-the-spatial-awareness-mesh"></a>5. Changer la visibilité du maillage de reconnaissance spatiale

Dans **Spatial Mesh Observer Settings**, configurez **Display Option** sur **Occlusion** pour rendre le maillage de mappage spatial invisible tout en le gardant fonctionnel :

![mr-learning-base](images/mr-learning-base/base-03-section1-step5-1.png)

> [!NOTE]
> Bien que le maillage de mappage spatial ne soit pas visible, il est toujours présent et fonctionnel. Par exemple, les hologrammes qui sont derrière le maillage de mappage spatial, comme un hologramme derrière un mur physique, ne sont pas visibles.

Vous venez de découvrir comment modifier un paramètre dans le profil MRTK. Comme vous pouvez le voir, pour personnaliser les paramètres du MRTK, vous devez d’abord créer une copie des profils par défaut. Étant donné que les profils par défaut ne sont pas modifiables, vous les aurez toujours comme référence si vous voulez rétablir les paramètres par défaut. Pour plus d’informations sur les profils MRTK et leur architecture, vous pouvez consulter le [Guide de configuration du profil MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez vu comment cloner, personnaliser et configurer les profils et les paramètres MRTK.

[Tutoriel suivant : 4. Positionnement des objets dans la scène](mr-learning-base-04.md)
