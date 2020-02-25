---
title: Didacticiels sur les ancres spatiales Azure-1. Prise en main des ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 0163b61bfbf8bd583532092581d94f63e1c2a624
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77554654"
---
# <a name="1-getting-started-with-azure-spatial-anchors"></a>1. prise en main des ancres spatiales Azure

## <a name="overview"></a>Overview

Bienvenue dans la deuxième série des didacticiels HoloLens 2. Dans cette série de didacticiels en trois parties, vous allez apprendre les principes de base des ancres spatiales Azure.

Dans ce premier didacticiel, bien démarrer [avec les ancres spatiales Azure](mrlearning-asa-ch1.md), vous allez explorer les différentes étapes requises pour démarrer et arrêter une session Azure et créer, charger et télécharger des ancres Azure sur un seul appareil.

Dans le deuxième didacticiel, [l’enregistrement, la récupération et le partage d’ancres spatiales Azure](mrlearning-asa-ch2.md), vous apprendrez à enregistrer les ancres spatiales Azure dans plusieurs sessions d’application en enregistrant les informations d’ancrage dans le stockage de HoloLens 2 et en partageant ces informations d’ancre avec d’autres appareils pour un alignement d’ancrage sur plusieurs appareils.

Dans le troisième didacticiel, l’affichage de commentaires sur l' [ancrage spatial Azure](mrlearning-asa-ch3.md)vous apprendra à fournir aux utilisateurs des commentaires sur les événements d’ancrage et les États lors de l’utilisation d’ancres spatiales Azure.

## <a name="objectives"></a>Objectifs

* Découvrez les principes de base du développement avec les ancres spatiales Azure pour HoloLens 2
* Créer, charger et télécharger des ancres spatiales

## <a name="prerequisites"></a>Composants requis

>[!TIP]
>Si vous n’avez pas encore terminé la série des [didacticiels de mise](mrlearning-base.md) en route, nous vous recommandons d’effectuer d’abord ces didacticiels.

* PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md)
* SDK Windows 10 (10.0.18362.0 ou version ultérieure)
* Capacité de programmation C# de base
* Appareil HoloLens 2 [configuré pour le développement](using-visual-studio.md#enabling-developer-mode)
* <a href="https://docs.unity3d.com/Manual/GettingStartedInstallingHub.html" target="_blank">Unity Hub</a> avec Unity 2019.2.X installé et le module de prise en charge de la build d’applications de plateforme Windows universelle ajouté
* Complétez la section [créer une ressource d’ancrages spatiaux](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du Guide de [démarrage rapide : créer une application de l’unité HoloLens qui utilise des ancres spatiales Azure](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) .

> [!IMPORTANT]
> La version Unity recommandée pour cette série de tutoriels est Unity 2019.2.X. Cela remplace toute exigence ou recommandation de version Unity énoncée dans les prérequis indiqués ci-dessus.

## <a name="creating-the-unity-project"></a>Création du projet Unity
<!-- TODO: Consider renaming to 'Creating and preparing the Unity scene and project'-->

Dans cette section, vous allez créer un nouveau projet Unity et le préparer au développement MRTK.

Pour ce faire, commencez par suivre le processus [d’initialisation de votre projet et de votre première application](mrlearning-base-ch1.md), à l’exclusion de la [création de votre application dans](mrlearning-base-ch1.md#build-your-application-to-your-device) les instructions de votre appareil, notamment les étapes suivantes :

1. [Créez un nouveau projet Unity](mrlearning-base-ch1.md#create-new-unity-project) et donnez-lui un nom approprié, par exemple, des *didacticiels MRTK*.

2. [Configurer le projet Unity pour Windows Mixed Reality](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality)

3. [Importer des ressources TextMesh Pro Essential](mrlearning-base-ch1.md#import-textmesh-pro-essential-resources)

4. [Importer la boîte à outils de réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit)

5. [Configurer le projet Unity pour la réalité mixte Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit)

6. [Ajoutez la boîte à outils de réalité mixte à la scène Unity](mrlearning-base-ch1.md#configure-the-mixed-reality-toolkit) et donnez un nom approprié à la scène, par exemple *AzureSpatialAnchors*

Suivez ensuite les instructions [Comment configurer les profils de la boîte à outils de la réalité mixte (modifier l’option d’affichage de détection spatiale)](mrlearning-base-ch2.md#how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option) pour modifier le profil de configuration MRTK pour votre scène sur le **DefaultHoloLens2ConfigurationProfile** et modifier les options d’affichage du maillage de la sensibilisation spatiale à **occlusion**.

> [!CAUTION]
> Comme mentionné dans les instructions [configure the Unity for the Mixed Reality Toolkit](mrlearning-base-ch1.md#configure-the-unity-project-for-the-mixed-reality-toolkit) ci-dessus, il est fortement recommandé de ne pas activer MSBuild pour Unity.

## <a name="adding-inbuilt-unity-packages"></a>Ajout de packages Unity incorporés
<!-- TODO: Consider renaming to 'Installing AR Foundation' -->

Dans cette section, vous allez installer le package d’intégration de fondation d’Unity, car il est requis par le kit de développement logiciel (SDK) d’ancre spatiale Azure que vous allez importer dans la section suivante.

Dans le menu Unity, sélectionnez **fenêtre** > **Gestionnaire de package**:

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section2-step1-1.png)

> [!NOTE]
> Il peut s’avérer nécessaire de prendre quelques secondes avant que le package de fondation de base ne s’affiche dans la liste.

Dans la fenêtre du gestionnaire de package, sélectionnez **AR Foundation** et installez le package en cliquant sur le bouton **installer** :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section2-step1-2.png)

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du didacticiel

Téléchargez et **importez** les packages personnalisés Unity suivants **dans l’ordre dans lequel ils sont répertoriés**:

* [AzureSpatialAnchors. pour Unity](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)
* [MRTK. HoloLens2. Unity. Tutorials. Assets. GettingStarted. 2.3.0.2. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.2/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage)
* [MRTK. HoloLens2. Unity. Tutorials. Assets. AzureSpatialAnchors. 2.3.0.0. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.0.unitypackage)

> [!TIP]
> Pour obtenir un rappel sur l’importation d’un package personnalisé Unity, vous pouvez vous reporter aux instructions [importez les instructions de la réalité mixte](mrlearning-base-ch1.md#import-the-mixed-reality-toolkit) .

Une fois que vous avez importé les ressources du didacticiel, votre fenêtre de projet doit ressembler à ceci :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section3-step1-1.png)

## <a name="creating-and-preparing-the-scene"></a>Création et préparation de la scène
<!-- TODO: Consider renaming to 'Preparing the scene' -->

Dans cette section, vous allez préparer la scène en ajoutant une partie du didacticiel prefabs.

Dans la fenêtre projet, accédez à **ressources** > **MRTK. Tutoriels. AzureSpatialAnchors** > dossier **Prefabs** . Tout en maintenant enfoncé le bouton CTRL, cliquez sur **ButtonParent**, **DebugWindow**, **instructions**et **ParentAnchor** pour sélectionner les quatre prefabs :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section4-step1-1.png)

Les quatre prefabs étant toujours sélectionnés, faites-les glisser dans la fenêtre de hiérarchie pour les ajouter à la scène :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section4-step1-2.png)

Pour vous concentrer sur les objets de la scène, vous pouvez double-cliquer sur l’objet ParentAnchor, puis effectuer un zoom légèrement arrière :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section4-step1-3.png)

> [!TIP]
> Si vous trouvez les grandes icônes de votre scène, par exemple les icônes « t » de grande taille, vous pouvez les masquer en <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">basculant la gizmos</a> sur la position OFF.

## <a name="configuring-the-buttons-to-operate-the-scene"></a>Configuration des boutons pour faire fonctionner la scène

Dans cette section, vous allez ajouter des scripts dans la scène pour créer une série d’événements de bouton qui illustrent les principes de base de la façon dont les ancres locales et les ancres spatiales Azure se comportent dans une application.

### <a name="1-configure-the-pressable-button-holo-lens-2-script-component"></a>1. configurer le composant Holo lentille 2 (script) du bouton enfoncé

Dans la fenêtre hiérarchie, développez l’objet **ButtonParent** et sélectionnez le premier objet enfant nommé **StartAzureSession**:

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step1-1.png)

Dans la fenêtre de l’inspecteur, localisez le **bouton enfoncé Holo lentille 2 (script)** et ajoutez un nouvel écouteur d’événements à l’événement **bouton enfoncé ()** en cliquant sur l’icône **+** :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step1-2.png)

Lorsque l’objet StartAzureSession est toujours sélectionné dans la fenêtre hiérarchie, cliquez avec le bouton droit sur l’objet **ParentAnchor** de la fenêtre hiérarchie et faites-le glisser dans le champ **aucun (objet)** vide de l’écouteur d’événements que vous venez d’ajouter pour que l’objet ParentAnchor écoute les événements appuyés sur le bouton :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step1-3.png)

Cliquez sur la liste déroulante **no Function** du même écouteur d’événements, puis sélectionnez **AnchorModuleScript** > **StartAzureSession ()** pour définir la fonction StartAzureSession () comme l’action qui est déclenchée lorsque les événements activés du bouton sont déclenchés à partir de ce bouton :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step1-4.png)

### <a name="2-configure-the-interactable-script-component"></a>2. configurer le composant (script) pouvant être interagi

Lorsque l’objet StartAzureSession est toujours sélectionné dans la fenêtre hiérarchie, dans la fenêtre Inspecteur, localisez le composant **(script) pouvant être interagi** et répétez le même processus que à l’étape 1 ci-dessus pour l’événement **OnClick ()** :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step2-1.png)

### <a name="3-configure-the-remaining-buttons"></a>3. configurer les autres boutons

Pour chacun des autres boutons, effectuez le processus décrit aux étapes 1 et 2 ci-dessus pour affecter des fonctions aux événements **bouton appuyé ()** et **OnClick ()** :

* Pour l’objet **StopAzureSession** , assignez la fonction AnchorModuleScript > **StopAzureSession ()** .
* Pour l’objet **CreateAzureAnchor** , assignez la fonction AnchorModuleScript > **CreateAzureAnchor ()** ,
  * Faites ensuite glisser à nouveau le **ParentAnchor** dans le champ vide **aucun (objet de jeu)** .
* Pour l’objet **RemoveLocalAnchor** , assignez la fonction AnchorModuleScript > **RemoveLocalAnchor ()** ,
  * Faites ensuite glisser à nouveau le **ParentAnchor** dans le champ vide **aucun (objet de jeu)** .
* Pour l’objet **FindAzureAnchor** , assignez la fonction AnchorModuleScript > **FindAzureAnchor ()** .
* Pour l’objet **DeleteAzureAnchor** , assignez la fonction AnchorModuleScript > **DeleteAzureAnchor ()** .

### <a name="4-connect-the-scene-to-the-azure-resource"></a>4. Connectez la scène à la ressource Azure

Dans la fenêtre hiérarchie, sélectionnez l’objet **ParentAnchor** et, dans la fenêtre de l’inspecteur, faites défiler jusqu’au composant **Gestionnaire d’ancrage spatial (script)** .

Ensuite, dans la section **informations d’identification** , collez votre ID de compte et votre clé d’ancrage spatial, que vous avez créés dans le cadre des [conditions préalables](mrlearning-asa-ch1.md#prerequisites)de ce didacticiel, dans les champs de clé du compte d' **ancrage** spatial et des ancres **spatiales** correspondants :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section5-step4-1.png)

## <a name="trying-the-basic-behaviors-of-azure-spatial-anchors"></a>Essai des comportements de base des ancres spatiales Azure

Maintenant que votre scène est configurée pour illustrer les principes de base des ancres spatiales Azure, il est temps de déployer l’application afin de pouvoir expérimenter les ancres spatiales Azure.

### <a name="1-add-additional-required-capabilities"></a>1. ajouter des fonctionnalités supplémentaires requises

Dans le menu Unity, sélectionnez **modifier** > **paramètres du projet...** pour ouvrir la fenêtre Paramètres du lecteur :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section6-step1-1.png)

Dans la fenêtre Paramètres du lecteur, sélectionnez **lecteur** , puis **paramètres de publication**:

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section6-step1-2.png)

Dans les **paramètres de publication**, faites défiler jusqu’à la section **fonctionnalités** et vérifiez que les fonctionnalités **internetclient**, **microphone**et **SpatialPerception** , que vous avez activées lors de la création du projet au début du didacticiel, sont activées. Activez ensuite les fonctionnalités **InternetClientServer**, **PrivateNetworkClientServer**, **RemovableStorage**et **webcam** :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section6-step1-3.png)

### <a name="2-deploy-the-app-to-your-hololens-2"></a>2. Déployez l’application sur votre HoloLens 2

Les ancres spatiales Azure ne peuvent pas s’exécuter dans Unity. pour tester la fonctionnalité d’ancrages spatiaux Azure, vous devez déployer le projet sur votre appareil.

> [!TIP]
> Pour obtenir un rappel sur la création et le déploiement de votre projet Unity dans HoloLens 2, vous pouvez vous reporter à la rubrique [créer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device) .

### <a name="3-run-the-app-on-your-hololens-2-and-follow-the-in-app-instructions"></a>3. Exécutez l’application sur votre HoloLens 2 et suivez les instructions de l’application

> [!CAUTION]
> Les ancres spatiales Azure utilisent Internet pour enregistrer et charger les données d’ancrage. Assurez-vous que votre appareil est connecté à Internet.

Lorsque l’application est en cours d’exécution sur votre appareil, suivez les instructions à l’écran affichées dans le panneau d’instructions du didacticiel d’ancrage spatial Azure :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section6-step3-1.png)

## <a name="anchoring-an-experience"></a>Ancrage d’une expérience

Dans les sections précédentes, vous avez appris les principes de base des ancres spatiales Azure. Nous avons utilisé un cube pour représenter et visualiser l’objet de jeu parent avec l’ancre attachée. Dans cette section, vous allez apprendre à ancrer une expérience complète en la plaçant en tant qu’enfant de l’objet ParentAnchor.

### <a name="1-add-the-rocket-launcher-experience"></a>1. ajouter l’expérience du lanceur Rocket

Dans la fenêtre projet, accédez aux **ressources** > **MRTK. Tutoriels. GettingStarted** > **Prefabs** > dossier **RocketLauncher** et sélectionnez le **RocketLauncher_Complete** Prefab :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section7-step1-1.png)

Avec la RocketLauncher_Complete Prefab toujours sélectionnée, faites-la glisser sur l’objet **ParentAnchor** dans la fenêtre hiérarchie pour en faire un enfant de l’objet ParentAnchor :

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section7-step1-2.png)

### <a name="2-reposition-the-rocket-launcher-experience"></a>2. repositionner l’expérience du lanceur Rocket

Positionner, faire pivoter et mettre à l’échelle l’objet **RocketLauncher_Complete** avec une mise à l’échelle et une orientation appropriées, tout en veillant à ce que l’objet **ParentAnchor** soit toujours exposé, par exemple :

* Transformer la **position** X = 0, Y = 0, Z = 3,75
* Transformation de **rotation** X = 0, Y = 90, Z = 0
* Transformation **Scale** X = 10, Y = 10, Z = 10

![mrlearning-ASA](images/mrlearning-asa/tutorial1-section7-step2-1.png)

Dans l’application, les utilisateurs peuvent maintenant repositionner l’intégralité de l’expérience du lanceur Rocket en déplaçant le cube.

> [!TIP]
> Il existe un grand nombre d’expériences utilisateur pour repositionner les expériences, y compris l’utilisation d’un objet de repositionnement (tel que le cube utilisé dans ce didacticiel), l’utilisation d’un bouton pour basculer un cadre englobant qui entoure l’expérience, l’utilisation de la position et de la rotation. gizmos, et bien plus encore.

## <a name="congratulations"></a>Félicitations

Dans ce didacticiel, vous avez appris les principes de base des ancres spatiales Azure. Ce didacticiel vous a fourni plusieurs boutons qui vous permettent d’explorer les différentes étapes requises pour démarrer et arrêter une session d’ancre spatiale Azure et créer, charger et télécharger des ancres spatiales Azure sur un seul appareil.

Dans la leçon suivante, vous apprendrez comment enregistrer des ID d’ancrage Azure dans votre HoloLens 2 pour la récupération, même après le redémarrage de l’application, et comment transférer des ID d’ancrage entre plusieurs appareils pour obtenir un alignement spatial.

[Leçon suivante : 2. enregistrement, récupération et partage d’ancres spatiales Azure](mrlearning-asa-ch2.md)
