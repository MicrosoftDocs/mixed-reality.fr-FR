---
title: Tutoriels Azure Spatial Anchors - 4. Affichage du feedback Azure Spatial Anchors
description: Suivez ce cours pour découvrir comment implémenter Azure Spatial Anchors dans une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: afcd7753fb2296503e67a1977b183df951124560
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376521"
---
# <a name="4-displaying-feedback-from-azure-spatial-anchors"></a>4. Affichage du feedback Azure Spatial Anchors

Dans ce tutoriel, vous allez voir comment fournir aux utilisateurs un feedback sur la découverte des ancres, leurs événements et leur état à l’aide d’Azure Spatial Anchors (ASA).

## <a name="objectives"></a>Objectifs

* Apprendre à configurer un panneau d’interface utilisateur qui affiche des informations essentielles sur la session ASA en cours
* Connaître les éléments de feedback que le SDK ASA met à la disposition des utilisateurs

## <a name="setting-up-asa-feedback-panel"></a>Apprendre à configurer un panneau de feedback ASA

Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **Instructions** > **TextContent**. Sélectionnez **3D Object** > **Text - TextMeshPro** pour créer un objet de texte TextMeshPro en tant qu’enfant de l’objet Instructions > TextContent :

![mr-learning-asa](images/mr-learning-asa/asa-04-section1-step1-1.png)

> [!TIP]
> Pour faciliter l’utilisation de votre scène, désactivez <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> pour l’objet ParentAnchor en cliquant sur l’icône œil à gauche de l’objet. Ceci masque l’objet dans la fenêtre Scene sans changer sa visibilité dans le jeu.

Attribuez à l’objet Text (TMP) que vous venez de créer le nom de **Feedback**, puis, dans la fenêtre Inspector, modifiez sa position et sa taille de manière à ce qu’il soit placé bien en dessous du texte d’instruction, par exemple :

* Remplacez la valeur **Pos Y** du composant Rect Transform par -0.24.
* Remplacez la valeur **Width** du composant Rect Transform par 0.555.
* Remplacez la valeur **Height** du composant Rect Transform par 0.1.

Choisissez ensuite les propriétés de police de sorte que le texte s’ajuste correctement dans la zone de texte, par exemple :

* Pour le composant TextMeshPro - Text, configurez la valeur de **Font Style** sur Bold.
* Pour le composant TextMeshPro - Text, configurez la valeur de **Font Size** sur 0.17.
* Pour le composant TextMeshPro - Text, configurez la valeur de **Alignment** sur Center et Middle.

![mr-learning-asa](images/mr-learning-asa/asa-04-section1-step1-2.png)

Dans la fenêtre Hierarchy, sélectionnez l’objet **Feedback**, puis, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Anchor Feedback Script (Script)** et le configurer de la façon suivante :

* Affectez l’objet **Feedback** au champ **Feedback Text** du composant **Anchor Feedback Script (Script)** .

![mr-learning-asa](images/mr-learning-asa/asa-04-section1-step1-3.png)

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez vu comment créer un panneau d’interface utilisateur. Celui-ci affiche l’état actuel de l’expérience Azure Spatial Anchors pour fournir aux utilisateurs du feedback en temps réel.

[Tutoriel suivant : 5. Azure Spatial Anchors pour Android et iOS](mr-learning-asa-05.md)
