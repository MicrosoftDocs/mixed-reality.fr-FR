---
title: Tutoriels de démarrage - 7. Interaction avec les objets 3D
description: Ce cours montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: f02780a1b9421b814242727ce92311d62b5e3461
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376421"
---
# <a name="7-interacting-with-3d-objects"></a>7. Interaction avec les objets 3D

Dans ce tutoriel, vous allez apprendre à activer la manipulation proche et lointaine des objets 3D et à limiter les types de manipulation autorisés. Vous apprendrez également à ajouter des cadres englobants autour des objets 3D afin de faciliter le contrôle de la manipulation des objets.

## <a name="objectives"></a>Objectifs

* Apprendre à configurer des objets 3D afin de pouvoir interagir avec
* Apprendre à ajouter des cadres englobants à des objets 3D

## <a name="manipulating-3d-objects"></a>Manipulation d’objets 3D

Dans cette section, vous allez ajouter la capacité à manipuler toutes les pièces du Rover que vous avez disposées sur la table durant le tutoriel [Positionnement des objets dans la scène](mr-learning-base-04.md).

Voici les principales étapes à suivre pour y parvenir :

1. Ajouter le composant Object Manipulator (Script) à tous les objets de la pièce
2. Ajouter le composant NearInteractionGrabbable à tous les objets de la pièce
3. Configurer le composant Object Manipulator (Script)

> [!NOTE]
> Pour pouvoir **manipuler un objet**, celui-ci doit avoir les composants suivants :
>
> * Le composant **Collider**, par exemple un Box Collider
> * Le composant **Object Manipulator (Script)**
>
> Pour pouvoir **manipuler** et **saisir** un objet avec les mains suivies, celui-ci doit avoir les composants suivants :
>
> * Le composant **Collider**, par exemple un Box Collider
> * Le composant **Object Manipulator (Script)**
> * Le composant **NearInteractionGrabbable**

De plus, vous configurerez le RoverExplorer afin de pouvoir placer les pièces du Rover sur le Rover pour en faire un assemblage complet.

Dans la fenêtre de hiérarchie, développez l’objet RoverExplorer > **RoverParts** et sélectionnez tous ses objets de pièces de Rover enfants et l’objet **RoverAssembly** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** (Ajouter un composant) pour ajouter les composants suivants à tous les objets sélectionnés :

* Le composant **Object Manipulator (Script)**
* Le composant **NearInteractionGrabbable**
* Le composant **Part Assembly Controller (Script)**

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-1.png)

> [!TIP]
> Pour sélectionner plusieurs objets qui ne sont pas les uns à côté des autres, appuyez sur la touche Ctrl et maintenez-la enfoncée pendant que vous utilisez la souris pour sélectionner un objet.

> [!NOTE]
> Dans le cadre de ce tutoriel, des colliders ont déjà été ajoutés aux pièces du Rover. Pour plus d’informations sur les colliders, vous pouvez consulter la documentation <a href="https://docs.unity3d.com/Manual/CollidersOverview.html" target="_blank">Collider</a> d’Unity.

> [!NOTE]
> Part Assembly Controller (Script) ne fait pas partie du MRTK, mais il a été inclus avec les ressources du tutoriel.

Toujours avec les objets de pièces de Rover et l’objet RoverAssembly sélectionnés, dans la fenêtre de l’inspecteur, configurez le composant **Object Manipulator (Script)** comme suit :

* Dans la liste déroulante **Two Handed Manipulation Type** (Type de manipulation à deux mains), décochez Scale (Mise à l’échelle) afin que seuls **Move** (Déplacer) et **Rotate** (Faire pivoter) soient activés.

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-2.png)

> [!NOTE]
> À ce stade, vous avez activé la manipulation d’objet pour tous les objets de pièces de Rover et l’objet RoverAssembly.

Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK** > **SDK** > **StandardAssets** > **Audio** pour localiser les clips audio :

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-3.png)

Dans la fenêtre de hiérarchie, resélectionnez tous les **objets de pièces de Rover** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** pour ajouter le composant **Audio Sources** et configurez-le comme suit :

* Affectez le clip audio **MRTK_Scale_Start** au champ **AudioClip**.
* Décochez la case **Play On Awake** (Lire en cas d’activité)
* Affectez la valeur 1 à **Spatial Blend**.

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-4.png)

Dans la fenêtre de hiérarchie, développez l’objet RoverAssembly > RoverModel_PlacementHints_XRay > **Parts_PlacementHints** pour révéler tous les objets d’indicateur de placement, puis sélectionnez la première pièce de Rover, RoverParts > **Camera_Part**, et configurez le composant **Part Assembly Controller (Script)** comme suit :

* Assignez l’objet **Camera_PlacementHint** au champ **Location To Place** (Emplacement).

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-5.png)

**Répétez** cette étape pour chacun des objets de pièces de Rover restants et l’objet RoverAssembly afin de configurer le composant **Part Assembly Controller (Script)** comme suit :

* Pour **Generator_Part**, assignez l’objet **Generator_PlacementHint** au champ **Location To Place**.
* Pour **Lights_Part**, assignez l’objet **Lights_PlacementHint** au champ **Location To Place**.
* Pour **UHFAntenna_Part**, assignez l’objet **UHFAntenna_PlacementHint** au champ **Location To Place**.
* Pour **Spectrometer_Part**, assignez l’objet **Spectrometer_PlacementHint** au champ **Location To Place**.
* Pour **RoverAssembly**, assignez l’objet lui-même (c’est-à-dire le même objet **RoverAssembly**), au champ **Location To Place**.

Dans la fenêtre de hiérarchie, sélectionnez l’objet de bouton RoverExplorer > Buttons > **Reset** puis, dans la fenêtre de l’inspecteur, configurez l’événement **OnClick ()** comme suit :

* Assignez l’objet **RoverAssembly** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **PartAssemblyController** > **ResetPlacement ()** pour définir cette fonction en tant qu’action à exécuter lorsque l’événement est déclenché.

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-6.png)

Si vous basculez maintenant en mode Game, vous pouvez utiliser l’interaction proche ou lointaine pour placer les pièces sur le Rover. Une fois que la pièce est proche de l’indicateur de placement correspondant, elle s’imbrique en place et devient partie intégrante du Rover. Pour réinitialiser les placements, vous pouvez appuyer sur le bouton Reset :

![mr-learning-base](images/mr-learning-base/base-07-section1-step1-7.png)

Pour en savoir plus sur le composant Object Manipulator et ses propriétés associées, vous pouvez consulter le guide [Object Manipulator](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectManipulator.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="adding-bounding-boxes"></a>Ajout de cadres englobants

Les cadres englobants facilitent et rendent plus intuitive la manipulation d’objets avec une main pour l’interaction proche et de loin en fournissant des poignées qui peuvent être utilisées pour la mise à l’échelle et la rotation.

Dans cet exemple, vous allez ajouter un cadre englobant à l’objet RoverExplorer afin de pouvoir effectuer facilement un déplacement, une rotation et une mise à l’échelle. Vous allez également configurer le menu afin de pouvoir activer ou désactiver le cadre englobant.

Dans la fenêtre de hiérarchie, sélectionnez l’objet **RoverExplorer** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** pour ajouter les composants suivants :

* Le composant **BoundingBox**
* Le composant **Object Manipulator (Script)**

Ensuite, **décochez** la case à côté des deux composants afin qu’ils soient **désactivés** par défaut :

![mr-learning-base](images/mr-learning-base/base-07-section2-step1-1.png)

> [!NOTE]
> La visualisation des cadres englobants est créée au moment de l’exécution, et n’est donc pas visible avant l’entrée en mode Game.

> [!NOTE]
> Le composant BoundingBox ajoutera automatiquement le composant NearInteractionGrabbable au moment de l’exécution. Par conséquent, nous n’avons pas besoin d’ajouter ce composant pour saisir les objets englobés avec les mouvements captés des mains.

Dans la fenêtre de hiérarchie, développez l’objet Menu > **ButtonCollection** pour afficher les quatre boutons et renommez le troisième bouton **BoundingBox_Enable** puis, dans la fenêtre de l’inspecteur, configurez le composant **Button Config Helper (Script)** comme suit :

* Affectez la valeur **Enable** à **Main Label Text** (Texte de l'étiquette principale).
* Assignez l’objet **RoverExplorer** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **BoundingBox** > **bool Enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
* Vérifiez que la case de l’argument est **cochée**.
* Cliquez sur la petite icône **+** pour ajouter un autre événement.
* Assignez l’objet **RoverExplorer** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **ObjectManipulator** > **bool Enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
* Vérifiez que la case de l’argument est **cochée**.
* Conservez « cube avec cadre englobant » comme **icône**.

![mr-learning-base](images/mr-learning-base/base-07-section2-step1-2.png)

Renommez **BoundingBox_Disable** les quatrième et dernier bouton puis, dans la fenêtre de l’inspecteur, configurez le composant **Button Config Helper (Script)** comme suit :

* Affectez la valeur **Disable** à **Main Label Text**.
* Assignez l’objet **RoverExplorer** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **BoundingBox** > **bool Enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
* Vérifiez que la case de l’argument est **décochée**.
* Cliquez sur la petite icône **+** pour ajouter un autre événement.
* Assignez l’objet **RoverExplorer** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **ObjectManipulator** > **bool Enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
* Vérifiez que la case de l’argument est **décochée**.
* Remplacez l’**icône** par « cube avec cadre englobant ».

![mr-learning-base](images/mr-learning-base/base-07-section2-step1-3.png)

Si vous basculez maintenant en mode Game et que vous activez le cadre englobant en cliquant sur le bouton Enable, vous pouvez utiliser l’interaction proche ou lointaine pour déplacer, faire pivoter et mettre à l’échelle le cadre englobant, et utiliser le bouton Disable pour désactiver le cadre englobant :

![mr-learning-base](images/mr-learning-base/base-07-section2-step1-4.png)

Pour plus d’informations sur le composant Bounding Box et ses propriétés associées, vous pouvez consulter le guide [Bounding Box](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html) dans le [portail de la documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html).

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à activer la manipulation proche et lointaine pour les objets 3D et comment limiter les types de manipulation autorisés. Vous avez également appris à ajouter des cadres englobants autour des objets 3D afin de faciliter le contrôle de la manipulation des objets.

[Tutoriel suivant : 8. Utilisation du suivi oculaire](mr-learning-base-08.md)
