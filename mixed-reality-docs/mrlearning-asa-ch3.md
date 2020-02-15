---
title: Didacticiels sur les ancres spatiales Azure-3. Affichage des commentaires sur l’ancrage spatial Azure
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: f4f609a71b05a52e8761e282763a540b42e9f7f5
ms.sourcegitcommit: a580166a19294f835b8e09c780f663f228dd5de0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77250686"
---
# <a name="3-displaying-azure-spatial-anchor-feedback"></a>3. affichage des commentaires sur l’ancrage spatial Azure

Dans ce didacticiel, vous allez apprendre à fournir aux utilisateurs des commentaires sur la découverte d’ancrage, les événements et l’état lors de l’utilisation d’ancres spatiales Azure (ASA).

## <a name="objectives"></a>Objectifs

* Découvrez comment configurer un panneau d’interface utilisateur qui affiche des informations importantes sur la session ASA actuelle.
* Comprendre et explorer les éléments de commentaires que le kit de développement logiciel (SDK) ASA met à la disposition des utilisateurs

## <a name="set-up-asa-feedback-ui-panel"></a>Panneau de l’interface utilisateur de configuration des commentaires ASA

Dans la fenêtre hiérarchie, cliquez avec le bouton droit sur les **instructions** > objet **TextContent** et sélectionnez **objet 3D** > **texte-TextMeshPro** pour créer un objet de texte TextMeshPro en tant qu’enfant des instructions > objet TextContent et donnez-lui un nom approprié, par exemple, **Commentaires**:

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-1.png)

> [!TIP]
> Pour faciliter l’utilisation de votre scène, définissez l’option visibilité de la <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">scène</a> de l’objet ParentAnchor sur désactivé en cliquant sur l’icône représentant un œil à gauche de l’objet. Cela masque l’objet dans la fenêtre de scène sans modifier sa visibilité dans le jeu.

Lorsque l’objet de **Commentaires** est toujours sélectionné, dans la fenêtre de l’inspecteur, modifiez sa position et sa taille de manière à ce qu’il soit placé soigneusement sous le texte d’instruction, par exemple :

* Remplacez le POS transformation Rect **Y** par-0,24
* Modifiez la **largeur** de la transformation Rect en 0,555
* Modifier la **hauteur** de la transformation Rect en 0,1

Choisissez ensuite propriétés de police pour que le texte s’ajuste correctement dans la zone de texte, par exemple :

* Modifier le **style de police** du texte de maillage Pro (script) en gras
* Modifier la **taille de police** du texte de maille Pro (script) à 0,17
* Modifiez l' **alignement** du texte de maille Pro (script) en centre et au milieu

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-2.png)

Lorsque l’objet de **Commentaires** est toujours sélectionné, dans la fenêtre de l’inspecteur, utilisez le bouton **Ajouter un composant** pour ajouter le composant script d' **ancrage de commentaires (script)** à l’objet de commentaires :

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-3.png)

Assignez l’objet de **Commentaires** au champ de **texte de commentaire** du composant de script d' **ancrage de commentaires (script)** :

![mrlearning-base](images/mrlearning-asa/tutorial3-section1-step1-4.png)

## <a name="congratulations"></a>Félicitations !

Dans ce didacticiel, vous avez appris à créer un panneau d’interface utilisateur pour afficher l’état actuel de l’expérience d’ancrage spatial Azure pour fournir aux utilisateurs des commentaires en temps réel.
