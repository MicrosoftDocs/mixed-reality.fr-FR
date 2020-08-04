---
title: Tutoriels de démarrage - 4. Positionnement des objets dans la scène
description: Ce cours vous montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: 71990db23b5154de916f0eda86a978885ab53547
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376631"
---
# <a name="4-positioning-objects-in-the-scene"></a>4. Positionnement des objets dans la scène

## <a name="overview"></a>Vue d’ensemble

Dans ce tutoriel, vous allez importer les ressources du tutoriel et positionner les objets fournis dans la scène.

## <a name="objectives"></a>Objectifs

* Apprendre à positionner des objets dans la scène
* Apprendre à utiliser la fonctionnalité Grid Object Collection du MRTK

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du tutoriel

Téléchargez et importez le package personnalisé Unity suivant :

* [MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.4.0/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.4.0.unitypackage)

Une fois que vous avez importé les ressources du tutoriel, votre fenêtre Project doit ressembler à ceci :

![mr-learning-base](images/mr-learning-base/base-04-section1-step1-1.png)

> [!TIP]
> Pour vous rappeler comment importer un package personnalisé Unity, reportez-vous aux instructions fournies dans [Importation du MRTK](mr-learning-base-02.md#importing-the-mixed-reality-toolkit).

## <a name="creating-the-parent-object"></a>Création de l’objet parent

Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur une zone vide et sélectionnez **Create Empty** pour ajouter un objet vide à votre scène :

![mr-learning-base](images/mr-learning-base/base-04-section2-step1-1.png)

> [!TIP]
> Pour afficher côte à côte les fenêtres Scene et Game comme dans l’image ci-dessus, faites glisser la fenêtre Game à droite de la fenêtre Scene. Pour en savoir plus, consultez la page consacrée à la <a href="https://docs.unity3d.com/Manual/CustomizingYourWorkspace.html" target="_blank">personnalisation de votre espace de travail</a> dans la documentation Unity.

Cliquez avec le bouton droit sur l’objet que vous venez de créer, sélectionnez **Rename**, puis remplacez le nom par **RoverExplorer** :

![mr-learning-base](images/mr-learning-base/base-04-section2-step1-2.png)

L’objet RoverExplorer étant toujours sélectionné, dans la fenêtre Inspector, configurez le composant **Transform** comme ceci :

* **Position** : X = 0, Y = -0.6, Z = 2
* **Rotation** : X = 0, Y = 0, Z = 0
* **Scale** : X = 1, Y = 1, Z = 1

![mr-learning-base](images/mr-learning-base/base-04-section2-step1-3.png)

> [!NOTE]
> L’appareil photo, qui représente la tête de l’utilisateur, est positionné à l’origine (X = 0, Y = 0, Z = 0). En règle générale, 1 unité dans Unity correspond à peu près à 1 mètre dans le monde physique. Il y a cependant des exceptions à cela, par exemple quand les objets sont des enfants d’objets mis à l’échelle. Dans le scénario ci-dessus, l’objet RoverExplorer est positionné 2 mètres devant la tête de l’utilisateur et 0,6 mètre en dessous.

## <a name="adding-the-tutorial-prefabs"></a>Ajout des préfabriqués du tutoriel

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.GettingStarted** > **Prefabs** :

![mr-learning-base](images/mr-learning-base/base-04-section3-step1-1.png)

> [!TIP]
> Un <a href="https://docs.unity3d.com/Manual/Prefabs.html" target="_blank">préfabriqué</a> (Prefab) est un GameObject préconfiguré stocké en tant que ressource Unity et qui peut être réutilisé dans tout votre projet.

Dans la fenêtre Project, cliquez sur le préfabriqué **Table** et faites-le glisser sur l’objet **RoverExplorer** pour en faire un enfant de cet objet, puis dans la fenêtre Inspector, configurez le composant **Transform** comme ceci :

* **Position** : X = 0, Y = -0.005, Z = 0
* **Rotation** : X = 0, Y = 0, Z = 0
* **Scale** : X = 1.2, Y = 0.01, Z = 1.2

![mr-learning-base](images/mr-learning-base/base-04-section3-step1-2.png)

> [!TIP]
> Pour afficher votre scène comme dans l’image ci-dessus, utilisez le <a href="https://docs.unity3d.com/Manual/SceneViewNavigation.html" target="_blank">gizmo Scene</a> en haut à droite de la fenêtre Scene pour ajuster l’angle de visualisation sur l’axe Z vers l’avant, double-cliquez sur l’objet MixedRealityPlayspace dans la fenêtre Hierarchy pour avoir le focus sur l’appareil photo, puis faites un zoom avant si nécessaire.

Dans la fenêtre Project, cliquez sur le préfabriqué **RoverAssembly** et faites-le glisser sur l’objet **RoverExplorer** pour en faire un enfant de cet objet, puis dans la fenêtre Inspector, configurez le composant **Transform** comme ceci :

* **Position** : X = -0.1, Y = 0, Z = 0
* **Rotation** : X = 0, Y = -135, Z = 0
* **Scale** : X = 1, Y = 1, Z = 1

![mr-learning-base](images/mr-learning-base/base-04-section3-step1-3.png)

## <a name="organizing-objects-in-a-collection"></a>Organisation des objets dans une collection

Dans la fenêtre Hierarchy, cliquez avec le bouton droit sur l’objet **RoverExplorer**, puis sélectionnez **Create Empty** pour ajouter un objet vide en tant qu’enfant de RoverExplorer. Nommez l’objet **RoverParts**, puis configurez le composant **Transform** comme ceci :

* **Position** : X = 0, Y = 0.06, Z = 0
* **Rotation** : X = 0, Y = 90, Z = 0
* **Scale** : X = 1, Y = 1, Z = 1

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-1.png)

Dans la fenêtre Hierarchy, sélectionnez tous les objets enfants RoverExplorer > RoverAssembly > RoverModel > **Parts**, cliquez dessus avec le bouton droit, puis sélectionnez **Duplicate** pour créer une copie de chaque élément :

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-2.png)

> [!TIP]
> Pour sélectionner plusieurs objets adjacents, maintenez la touche Maj enfoncée tout en utilisant la souris pour sélectionner le premier et le dernier objet.

Les objets enfants Parts que vous venez de dupliquer étant toujours sélectionnés, cliquez dessus et faites-les glisser sur l’objet **RoverParts** pour en faire des objets enfants de cet objet :

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-3.png)

Pour faciliter l’utilisation de votre scène, dans la fenêtre Hierarchy, cliquez sur l’icône **œil** à gauche de l’objet pour désactiver la **visibilité de la scène** pour l’objet **RoverExplorer**. Cette opération masque l’objet dans la fenêtre Scene sans changer sa visibilité dans le jeu :

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-4.png)

> [!TIP]
> Pour en savoir plus sur les contrôles de visibilité de la scène et sur la façon dont vous pouvez les utiliser pour optimiser l’affichage et le workflow de votre scène, reportez-vous à la documentation <a href="https://docs.unity3d.com/Manual/SceneVisibility.html" target="_blank">Scene Visibility</a> d’Unity.

Dans la fenêtre Hierarchy, nettoyez les noms des objets enfants RoverParts en remplaçant le suffixe **(1)** par **_Part** :

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-5.png)

Dans la fenêtre Hierarchy, sélectionnez l’objet **RoverParts**. Dans la fenêtre Inspector, cliquez sur le bouton **Add Component**, puis recherchez et sélectionnez **GridObjectCollection** pour ajouter le composant GridObjectCollection à l’objet RoverParts :

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-6.png)

Configurez les valeurs du composant **GridObjectCollection** comme ceci :

* **Sort Type** : Alphabetic
* **Layout** : Horizontale
* **Cell Width** : 0.25
* **Distance from parent** : 0.38

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-7.png)

Cliquez ensuite sur le bouton **Update Collection** pour mettre à jour la position des objets enfants de RoverParts :

![mr-learning-base](images/mr-learning-base/base-04-section4-step1-8.png)

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à positionner des objets dans la scène par rapport à l’utilisateur et à utiliser la fonctionnalité Grid Object Collection du MRTK pour organiser les objets dans une collection.

[Tutoriel suivant : 5. Création de contenu dynamique avec des solveurs](mr-learning-base-05.md)
