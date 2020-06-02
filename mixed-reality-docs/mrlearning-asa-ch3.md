---
title: Tutoriels Azure Spatial Anchors - 3. Affichage du feedback sur les ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 62ce1151837a345dea1bea4a8bea275cc851b9bd
ms.sourcegitcommit: e65f1463aec3c040a1cd042e61fc2bd156a42ff8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83866899"
---
# <a name="3-displaying-azure-spatial-anchor-feedback"></a>3. Affichage du feedback sur les ancres spatiales Azure

Dans ce tutoriel, vous allez apprendre à fournir aux utilisateurs un feedback sur la découverte des ancres, leurs événements et leur état quand vous utilisez Azure Spatial Anchors (ASA).

## <a name="objectives"></a>Objectifs

* Apprendre à configurer un panneau d’interface utilisateur qui affiche des informations importantes sur la session ASA en cours
* Comprendre et explorer les éléments de feedback que le SDK ASA met à la disposition des utilisateurs

## <a name="set-up-asa-feedback-ui-panel"></a>Configurer un panneau d’interface utilisateur pour le feedback ASA

Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **Instructions** > **TextContent** et sélectionnez **3D Object** > **Text - TextMeshPro** pour créer un objet texte TextMeshPro en tant qu’enfant de l’objet Instructions > TextContent et donnez-lui un nom approprié, par exemple **Feedback** :

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-1.png)

> [!TIP]
> Pour faciliter l’utilisation de votre scène, désactivez <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> pour l’objet ParentAnchor en cliquant sur l’icône œil à gauche de l’objet. Ceci masque l’objet dans la fenêtre Scene sans changer sa visibilité dans le jeu.

L’objet **Feedback** étant toujours sélectionné, dans la fenêtre Inspector, modifiez sa position et sa taille de manière à ce qu’il soit placé bien en dessous du texte d’instruction, par exemple :

* Remplacez la valeur **Pos Y** de Rect Transform par -0,24.
* Remplacez la valeur **Width** de Rect Transform par 0,555.
* Remplacez la valeur **Height** de Rect Transform par 0,1.

Choisissez ensuite les propriétés de police de sorte que le texte s’ajuste correctement dans la zone de texte, par exemple :

* Remplacez la valeur **Font Style** de Text Mesh Pro (Script) par Bold.
* Remplacez la valeur **Font Size** de Text Mesh Pro (Script) par 0,17.
* Remplacez la valeur **Alignment** de Text Mesh Pro (Script) par Center and Middle.

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-2.png)

L’objet **Feedback** étant toujours sélectionné, dans la fenêtre Inspector, utilisez le bouton **Add Component** pour ajouter le composant **Anchor Feedback Script (Script)** à l’objet Feedback :

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-3.png)

Affectez l’objet **Feedback** lui-même au champ **Feedback Text** du composant **Anchor Feedback Script (Script)**  :

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-4.png)

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à créer un panneau d’interface utilisateur pour afficher l’état actuel de l’expérience Azure Spatial Anchors visant à fournir aux utilisateurs un feedback en temps réel.

[Leçon suivante : 4. Azure Spatial Anchors pour Android et iOS](mrlearning-asa-ch4.md)
