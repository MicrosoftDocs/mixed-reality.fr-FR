---
title: Tutoriels de démarrage - 8. Utilisation du suivi oculaire
description: Ce cours vous montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 31552cba9a68d1f1214395dbf4e4ed84ecd3f388
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376601"
---
# <a name="8-using-eye-tracking"></a>8. Utilisation du suivi oculaire

## <a name="overview"></a>Vue d’ensemble

Dans ce tutoriel, vous allez voir comment activer le suivi oculaire (eye-tracking) pour HoloLens 2 et comment l’ajouter aux objets en vue de déclencher des actions lorsque l’utilisateur regarde ces objets.

> [!NOTE]
> Si vous déployez également ce projet sur HoloLens (1re génération), notez que le suivi oculaire est pris en charge uniquement sur HoloLens 2.

## <a name="objectives"></a>Objectifs

* Apprendre à activer le suivi oculaire pour HoleLens 2
* Apprendre à utiliser le suivi oculaire pour déclencher une action

## <a name="ensuring-the-eye-gaze-input-capability-is-enabled"></a>Vérifier que la fonctionnalité d’entrée avec le pointage du regard est activée

Dans le menu Unity, sélectionnez Mixed Reality Toolkit > Utilities > **Configure Unity Project** pour ouvrir la fenêtre **MRTK Project Configurator** puis, dans la section **UWP Capabilities**, vérifiez que l’option **Enable Eye Gaze Input Capability** est grisée :

![mr-learning-base](images/mr-learning-base/base-08-section1-step1-1.png)

> [!NOTE]
> La fonctionnalité Gaze Input doit avoir été activée lors des instructions [Appliquer les paramètres de MRTK Project Configurator](mr-learning-base-02.md#1-apply-the-mrtk-project-configurator-settings) lorsque vous avez configuré le projet Unity au début de cette série de tutoriels. Toutefois, si elle n’est pas activée, activez-la maintenant.

## <a name="enabling-eye-based-gaze-in-the-gaze-provider"></a>Activation du pointage du regard dans le fournisseur de regard

Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit**. Ensuite, dans la fenêtre Inspector, sélectionnez l’onglet MixedRealityToolkit > **Input**, puis effectuez les étapes suivantes :

* Clonez **DefaultHoloLens2InputSystemProfile**, puis attribuez-lui un nom adapté, comme _GettingStarted_HoloLens2InputSystemProfile_.
* Développez la section **Pointers**.
* Clonez **DefaultMixedRealityPointerProfile**, puis attribuez-lui un nom adapté, comme _GettingStarted_MixedRealityPointerProfile_.
* Recherchez la section**Gaze Settings** (Paramètres du regard), puis cochez la case **Is Eye Tracking Enabled** (Activation du suivi oculaire).

![mr-learning-base](images/mr-learning-base/base-08-section2-step1-1.png)

> [!TIP]
> Pour obtenir un rappel de la façon de cloner des profils MRTK, vous pouvez consulter les instructions fournies dans [Configuration des profils MRTK](mr-learning-base-03.md).

## <a name="enabling-simulated-eye-tracking-for-the-unity-editor"></a>Activation du suivi oculaire simulé pour l’éditeur Unity

Dans la fenêtre Hierarchy, sélectionnez l’objet **MixedRealityToolkit**. Ensuite, dans la fenêtre Inspector, accédez à l’onglet **Input**, puis :

* Développez la section **Input Data Providers** > **Input Simulation Service**.
* Clonez **DefaultMixedRealityInputSimulationProfile**, puis attribuez-lui un nom adapté, comme _GettingStarted_MixedRealityInputSimulationProfile_.
* Localisez la section **Eye Simulation**, puis cochez la case **Simulate Eye Position**.

![mr-learning-base](images/mr-learning-base/base-08-section3-step1-1.png)

## <a name="adding-eye-tracking-to-objects"></a>Ajout du suivi oculaire aux objets

Dans la fenêtre Hierarchy, développez l’objet RoverExplorer > **Buttons**, puis, pour chacun des trois objets enfants Buttons, développez et sélectionnez l’objet SeeItSayItLabel > **TextMeshPro** :

![mr-learning-base](images/mr-learning-base/base-08-section4-step1-1.png)

Avec les trois objets TextMeshPro toujours sélectionnés, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter les composants suivants à tous les objets sélectionnés :

* Composant **Box Collider**
* Composant **EyeTrackingTarget**

![mr-learning-base](images/mr-learning-base/base-08-section4-step1-2.png)

Dans la fenêtre Hierarchy, sélectionnez l’objet **Hints** > SeeItSayItLabel > **TextMeshPro**, puis configurez le composant **EyeTrackingTarget** de la façon suivante :

* Dans la section d’événement **On Look At Start ()**
  * Cliquez sur la petite icône **+** pour ajouter un autre événement.
  * Affectez l’objet **TextMeshPro** au champ **None (Object)** .
  * Dans la liste déroulante **No Function**, sélectionnez **TextMeshPro** > **float fontSize** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
  * Définissez l’argument sur **0.06** pour augmenter la taille de police actuelle (0.04) de 50 %.
* Dans la section d’événement **On Look Away ()**
  * Cliquez sur la petite icône **+** pour ajouter un autre événement.
  * Affectez l’objet **TextMeshPro** au champ **None (Object)** .
  * Dans la liste déroulante **No Function**, sélectionnez **TextMeshPro** > **float fontSize** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
  * Définissez l’argument sur **0.04** pour rétablir la taille de la police à 0.04.

![mr-learning-base](images/mr-learning-base/base-08-section4-step1-3.png)

**Répétez** cette étape pour l’objet **Explode** > SeeItSayItLabel > **TextMeshPro** et pour l’objet **Reset** > SeeItSayItLabel > **TextMeshPro**.

Si vous passez maintenant en mode jeu, puis maintenez enfoncé le bouton droit de la souris tout en déplaçant la souris jusqu’à ce que le regard atteigne l’une des étiquettes, vous verrez que la taille de police augmente de 50 % et retourne à sa taille d’origine lorsque l’utilisateur regarde ailleurs :

![mr-learning-base](images/mr-learning-base/base-08-section4-step1-4.png)

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez vu comment activer le suivi oculaire pour HoloLens 2 et comment l’ajouter aux objets en vue de déclencher des actions lorsque l’utilisateur regarde ces objets.

[Tutoriel suivant : 9. Utilisation des commandes vocales](mr-learning-base-09.md)