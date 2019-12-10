---
title: Didacticiels sur les ancres spatiales Azure-1. Prise en main des ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 861c42f9449fcb3cf038258af91088fc927941e5
ms.sourcegitcommit: f4812e1312c4751a22a2de56771c475b22a4ba24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2019
ms.locfileid: "74940977"
---
# <a name="1-getting-started-with-azure-spatial-anchors"></a>1. prise en main des ancres spatiales Azure

## <a name="overview"></a>Vue d'ensemble

Bienvenue dans la deuxième série des didacticiels HoloLens 2. Dans cette série de didacticiels en trois parties, vous allez apprendre les principes de base des ancres spatiales Azure.

Dans ce premier didacticiel, bien démarrer [avec les ancres spatiales Azure](mrlearning-asa-ch1.md), vous allez explorer les différentes étapes requises pour démarrer et arrêter une session Azure et créer, charger et télécharger des ancres Azure sur un seul appareil.

Dans le deuxième didacticiel, [l’enregistrement, la récupération et le partage d’ancres spatiales Azure](mrlearning-asa-ch2.md), vous apprendrez à enregistrer les ancres spatiales Azure dans plusieurs sessions d’application en enregistrant les informations d’ancrage dans le stockage de HoloLens 2 et en partageant ces informations d’ancre avec d’autres appareils pour un alignement d’ancrage sur plusieurs appareils.

Dans le troisième didacticiel, l’affichage de commentaires sur l' [ancrage spatial Azure](mrlearning-asa-ch3.md)vous apprendra à fournir aux utilisateurs des commentaires sur les événements d’ancrage et les États lors de l’utilisation d’ancres spatiales Azure.

## <a name="objectives"></a>Objectifs

* Découvrez les principes de base du développement avec les ancres spatiales Azure pour HoloLens 2
* Créer, charger et télécharger des ancres spatiales

## <a name="prerequisites"></a>Conditions préalables

* Respectez la configuration requise indiquée dans la section [conditions préalables](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#prerequisites) du Guide de [démarrage rapide : créer une application de l’outil HoloLens Unity HoloLens qui utilise des ancres spatiales Azure](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) .
* Complétez la section [créer une ressource d’ancrages spatiaux](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens#create-a-spatial-anchors-resource) du Guide de [démarrage rapide : créer une application de l’unité HoloLens qui utilise des ancres spatiales Azure](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-unity-hololens) .
* Si vous n’avez pas encore terminé la série des [didacticiels de mise](mrlearning-base.md) en route, nous vous recommandons d’effectuer d’abord ces didacticiels.

## <a name="creating-the-unity-project"></a>Création du projet Unity

Dans cette section, vous allez créer un nouveau projet Unity et le configurer pour Windows Mixed Reality.

1. Créez un projet Unity et donnez-lui un nom approprié, par exemple le didacticiel sur les _ancres spatiales Azure_.

2. Configurez le projet Unity pour Windows Mixed Reality.

    >[!TIP]
    >Pour obtenir un rappel sur la façon de créer un projet Unity et de le configurer pour Windows Mixed Reality, vous pouvez consulter les sections créer un projet [Unity](mrlearning-base-ch1.md#create-new-unity-project) et [configurer le projet Unity pour Windows Mixed Reality](mrlearning-base-ch1.md#configure-the-unity-project-for-windows-mixed-reality) dans le didacticiel [initialiser votre projet et votre première application](https://docs.microsoft.com/windows/mixed-reality/mrlearning-base-ch1) , qui fait partie de la série de [didacticiels de mise](mrlearning-base.md) en route.

## <a name="adding-inbuilt-unity-packages"></a>Ajout de packages Unity incorporés

Dans cette section, vous allez ajouter des ressources Unity et des packages requis par les kits de ressources et les kits de développement logiciel (SDK) que vous utiliserez dans le projet.

1. Importez des ressources TMP essentielles.

    >[!NOTE]
    >Nous ajoutons ce package, car il est requis par le kit de la réalité mixte.

    Dans le menu Unity, sélectionnez **windows** > **TextMeshPro** > **importer des ressources tmp Essential**.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-2-1.1.png)

    Dans la fenêtre contextuelle importer un package d’Unity, commencez par vérifier que toutes les ressources sont sélectionnées en cliquant sur le bouton **tout** , puis importez les éléments multimédias en cliquant sur le bouton **Importer** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-2-1.2.png)

2. Installez AR Foundation.

    >[!NOTE]
    >Nous ajoutons ce package, car il est requis par le kit de développement logiciel (SDK) d’ancre spatiale Azure.

    Dans le menu Unity, sélectionnez **fenêtre** > **Gestionnaire de package**.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-2-2.1.png)

    Dans la fenêtre du gestionnaire de package, sélectionnez **AR Foundation** et installez le package en cliquant sur le bouton **installer** .

    >[!IMPORTANT]
    >Il peut s’avérer nécessaire de prendre quelques secondes avant que le package de fondation de base ne s’affiche dans la liste.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-2-2.2.png)

## <a name="importing-the-tutorial-assets"></a>Importation des ressources du didacticiel

Dans cette section, vous allez télécharger et importer toutes les ressources du didacticiel.

1. Téléchargez les ressources.

    * [AzureSpatialAnchors. pour Unity](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.0.0/AzureSpatialAnchors.unitypackage) (version 2.0.0)
    * [Microsoft. MixedReality. Toolkit. Unity. Foundation. 2.1.0. pour Unity](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.1.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage)
    * [MRTK. HoloLens2. Unity. Tutorials. Assets. GettingStarted. 2.1.0.1. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.1.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.1.0.1.unitypackage)
    * [MRTK. HoloLens2. Unity. Tutorials. Assets. AzureSpatialAnchors. 2.1.0.1. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.1.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.1.0.1.unitypackage)

2. Importez les ressources.

    Dans le menu Unity, sélectionnez **actifs** > **importer un package** > **package personnalisé...** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-3-2.1.png)

    Dans le package d’importation... dans la fenêtre indépendante, sélectionnez **AzureSpatialAnchors. pour Unity** , puis cliquez sur le bouton **ouvrir** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-3-2.2.png)

    Dans la fenêtre contextuelle importer un package d’Unity, commencez par vérifier que toutes les ressources sont sélectionnées en cliquant sur le bouton **tout** , puis importez les éléments multimédias en cliquant sur le bouton **Importer** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-3-2.3.png)

    Répétez ces étapes pour importer les packages de ressources restants. Une fois l’opération terminée, le dossier des **ressources** de votre projet Unity doit contenir ces sous-dossiers.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-3-2.4.png)

## <a name="creating-and-preparing-the-scene"></a>Création et préparation de la scène

Dans cette section, vous allez créer et préparer la scène en ajoutant la boîte à outils de la réalité mixte et une partie du didacticiel prefabs.

1. Créez une nouvelle scène.

    Dans le menu Unity, sélectionnez **fichier** > **nouvelle scène**.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-1.1.png)

    Dans le menu Unity, sélectionnez **fichier** > **Enregistrer sous...** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-1.2.png)

    Dans la fenêtre contextuelle enregistrer la scène, accédez au dossier **scenes** de votre projet, donnez à votre scène un nom approprié, par exemple, _ASATutorialScene_, puis enregistrez la scène en cliquant sur le bouton **Enregistrer** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-1.3.png)

    >[!TIP]
    >Vous pouvez enregistrer la scène à l’emplacement de votre choix, à condition qu’elle se trouve dans le dossier ressources du projet. Toutefois, pour que votre projet reste organisé, il est généralement recommandé de l’enregistrer dans le dossier scenes du projet.

2. Ajoutez la boîte à outils de réalité mixte.

    Dans le menu Unity, sélectionnez **Mixed Reality Toolkit** > **Ajouter à la scène et configurer..** ..

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-2.1.png)

    Dans la fenêtre contextuelle sélectionner MixedRealityToolkitConfigurationProfile, cliquez sur **DefaultHoloLens2ConfigurationProfile** pour le définir comme profil de configuration MRTK de la scène.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-2.2.png)

    Dans le menu Unity, sélectionnez **File** > **Save** pour enregistrer la scène.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-2.3.png)

    >[!TIP]
    >Vous pouvez utiliser le raccourci clavier CTRL + S (commande + S sur macOS) pour enregistrer rapidement votre scène au cours de ce didacticiel.

3. Ajoutez le didacticiel prefabs.

    Dans le panneau projet, accédez à **ressources** > **MRTK. Tutoriels. AzureSpatialAnchors** > dossier **Prefabs** . Tout en maintenant enfoncé le bouton CTRL (commande sur macOS), cliquez sur **ButtonParent**, **DebugWindow**et **ParentAnchor** pour sélectionner les trois prefabs.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-3.1.png)

    Les trois prefabs étant toujours sélectionnés, faites-les glisser dans le panneau de la hiérarchie pour les ajouter à la scène.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-3.2.png)

    Pour vous concentrer sur les objets de la scène, vous pouvez double-cliquer sur l’objet ParentAnchor, puis effectuer un zoom légèrement arrière.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-4-3.3.png)

    >[!TIP]
    >Si vous trouvez les grandes icônes de votre scène, par exemple les icônes « t » de grande taille, vous pouvez les masquer en <a href="https://docs.unity3d.com/2019.1/Documentation/Manual/GizmosMenu.html" target="_blank">basculant la gizmos</a> sur la position OFF.

## <a name="configuring-the-buttons-to-operate-the-scene"></a>Configuration des boutons pour faire fonctionner la scène

Dans cette section, vous allez ajouter des prefabs et des scripts dans la scène pour créer une série de boutons qui illustrent les principes de base de la façon dont les ancres locales et les ancres spatiales Azure se comportent dans une application.

1. Configurez le composant Holo lentille 2 (script) du bouton enfoncé.

    Dans le volet hiérarchie, développez l’objet **ButtonParent** et sélectionnez le premier objet enfant nommé **StartAzureSession**.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-1.1.png)

    Dans le volet de l’inspecteur, faites défiler l’écran jusqu’au **bouton enfoncé Holo objectif 2 (script)** et ajoutez un nouvel écouteur d’événements à l’événement **bouton enfoncé ()** en cliquant sur l’icône **+** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-1.2.png)

    Lorsque l’objet StartAzureSession est toujours sélectionné dans le panneau hiérarchie, cliquez et faites glisser l’objet **ParentAnchor** à partir du volet hiérarchie vers le champ **aucun (objet)** vide de l’écouteur d’événements que vous venez d’ajouter pour que l’objet ParentAnchor écoute les événements appuyés sur le bouton à partir de ce bouton.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-1.3.png)

    Cliquez sur la liste déroulante **no Function** du même écouteur d’événements, puis sélectionnez **AnchorModuleScript** > **StartAzureSession ()** pour définir la fonction StartAzureSession () comme l’action qui est déclenchée lorsque les événements activés du bouton sont déclenchés à partir de ce bouton.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-1.4.png)

2. Configurez le composant (script) pouvant être interagi.

    Avec l’objet StartAzureSession toujours sélectionné dans le panneau hiérarchie, dans le panneau Inspecteur, faites défiler l’écran jusqu’au composant **(script) pouvant être interagi** et répétez le même processus qu’à l’étape 1 ci-dessus pour l’événement **OnClick ()** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-2.1.png)

3. Configurer les autres boutons

    Pour chacun des autres boutons, terminez le processus décrit aux étapes 1 et 2 ci-dessus pour affecter des fonctions aux événements bouton appuyé () et OnClick () suivants :

    * Pour l’objet **StopAzureSession** , assignez la fonction **StopAzureSession ()** .
    * Pour l’objet **CreateAnchor** , assignez la fonction **CreateAzureAnchor ()** , puis faites glisser à nouveau le **ParentAnchor** dans le champ vide **aucun (objet de jeu)** .
    * Pour le **début de la recherche de l’objet d’ancrage** , assignez la fonction **FindAzureAnchor ()** .
    * Pour l’objet de **Suppression d’Azure Anchor** , assignez la fonction **DeleteAzureAnchor ()** .
    * Pour l' **objet supprimer l’ancre locale** , assignez la fonction **RemoveLocalAnchor ()** , puis faites glisser à nouveau le **ParentAnchor** dans le champ vide **aucun (objet de jeu)** .

4. Connecter la scène à la ressource Azure

    Dans le panneau hiérarchie, sélectionnez l’objet **ParentAnchor** et, dans le panneau Inspecteur, faites défiler jusqu’au composant **Gestionnaire d’ancrage spatial (script)** .

    Ensuite, dans la section **informations d’identification** , collez votre ID de compte et votre clé d’ancrage spatial dans les champs **ID de compte d’ancrage** spatial et **ancres spatiales** correspondants.

    >[!NOTE]
    >Vous avez créé votre ID de compte et votre clé d’ancrage spatial dans le cadre des [conditions préalables](mrlearning-asa-ch1.md#prerequisites)de ce didacticiel.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-5-4.1.png)

    >[!CAUTION]
    >Veillez à enregistrer votre scène.

## <a name="trying-the-basic-behaviors-of-azure-spatial-anchors"></a>Essai des comportements de base des ancres spatiales Azure

Maintenant que votre scène est configurée pour illustrer les principes de base des ancres spatiales Azure, il est temps de déployer l’application afin de pouvoir expérimenter les ancres spatiales Azure.

1. Ajoutez des fonctionnalités supplémentaires requises.

    Dans le menu Unity, sélectionnez **modifier** > **paramètres du projet...** pour ouvrir le panneau Paramètres du lecteur.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-6-1.1.png)

    Dans le panneau Paramètres du lecteur, sélectionnez **lecteur** , puis **paramètres de publication**.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-6-1.2.png)

    Dans les **paramètres de publication**, faites défiler jusqu’à la section **fonctionnalités** et vérifiez que **SpatialPerception**, que vous avez activé lors de la création du projet au début du didacticiel, est activé. Ensuite, activez les fonctionnalités **internetclient**, **InternetClientServer**, **PrivateNetworkClientServer**, **RemovableStorage**, **webcam**et **microphone** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-6-1.3.png)

2. Déployez l’application sur votre HoloLens 2.

    >[!TIP]
    >Pour obtenir un rappel sur la création et le déploiement de votre projet Unity dans HoloLens 2, vous pouvez consulter les sections [créer votre application sur votre appareil](mrlearning-base-ch1.md#build-your-application-to-your-device) dans le didacticiel [initialiser votre projet et votre première application](https://docs.microsoft.com/windows/mixed-reality/mrlearning-base-ch1) , qui fait partie de la série de [didacticiels de mise](mrlearning-base.md) en route.

3. Exécutez l’application et suivez les instructions de l’application.

    >[!CAUTION]
    >Les ancres spatiales Azure utilisent Internet pour enregistrer et charger les données d’ancrage. Assurez-vous que votre appareil est connecté à Internet.

    Lorsque l’application s’exécute sur votre appareil, suivez les instructions à l’écran affichées dans le panneau **instructions du module d’ancrage spatial Azure** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-6-3.1.png)

## <a name="anchoring-an-experience"></a>Ancrage d’une expérience

Dans les sections précédentes, vous avez appris les principes de base des ancres spatiales Azure. Nous avons utilisé un cube pour représenter et visualiser l’objet de jeu parent avec l’ancre attachée. Dans cette section, vous allez apprendre à ancrer une expérience complète en la plaçant en tant qu’enfant de l’objet ParentAnchor.

1. Ajoutez l’expérience du lanceur Rocket.

    Dans le panneau projet, accédez à **ressources** > **MRTK. Tutoriels. GettingStarted** > dossier **Prefabs** et sélectionnez le Prefab **Rocket Launcher_Complete** .

    ![mrlearning-ASA](images/mrlearning-asa-ch1-7-1.1.png)

    Avec la Prefab Rocket Launcher_Complete toujours sélectionnée, faites-la glisser sur l’objet **ParentAnchor** dans le panneau de la hiérarchie pour en faire un enfant de l’objet ParentAnchor.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-7-1.2.png)

2. Repositionnez l’expérience du lanceur Rocket.

    Déplacez le module **Rocket Launcher_Complete** objet afin que le **ParentAnchor** (le cube) soit toujours exposé.

    ![mrlearning-ASA](images/mrlearning-asa-ch1-7-2.1.png)

    Dans l’application, les utilisateurs peuvent maintenant repositionner l’intégralité de l’expérience du lanceur Rocket en déplaçant le cube.

    >[!TIP]
    >Il existe un grand nombre d’expériences utilisateur pour repositionner les expériences, y compris l’utilisation d’un objet de repositionnement (tel que le cube utilisé dans ce didacticiel), l’utilisation d’un bouton pour basculer un cadre englobant qui entoure l’expérience, l’utilisation de la position et de la rotation. gizmos, et bien plus encore.

## <a name="congratulations"></a>Félicitations !

Dans ce didacticiel, vous avez appris les principes de base des ancres spatiales Azure. Cette leçon vous a fourni plusieurs boutons qui vous permettent d’explorer les différentes étapes nécessaires au démarrage et à l’arrêt d’une session Azure et à la création, le chargement et le téléchargement d’ancres Azure sur un seul appareil.

Dans la leçon suivante, vous apprendrez comment enregistrer des ID d’ancrage Azure dans votre HoloLens 2 pour la récupération, même après le redémarrage de l’application, et comment transférer des ID d’ancrage entre plusieurs appareils pour obtenir un alignement spatial.

[Leçon suivante : 2. enregistrement, récupération et partage d’ancres spatiales Azure](mrlearning-asa-ch2.md)
