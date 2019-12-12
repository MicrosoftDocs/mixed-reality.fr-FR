---
title: Utilisation de Vuforia avec Unity
description: Tirez parti de Vuforia pour créer des applications Windows Mixed Reality dans Unity.
author: thetuvix
ms.author: alexturn
ms.date: 01/28/2019
ms.topic: article
keywords: Vuforia, marqueurs, coordonnées, frame de référence, suivi
ms.openlocfilehash: bae5d0eb04ab9434dd3e72674686743779a8f70c
ms.sourcegitcommit: 9005b3fdfa87ac8fdc18a594a681e25c00ac5ce1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2019
ms.locfileid: "75003188"
---
# <a name="using-vuforia-engine-with-unity"></a>Utilisation du moteur Vuforia avec Unity

Le moteur Vuforia apporte une fonctionnalité importante à HoloLens, la puissance permettant de connecter les expériences AR à des images et objets spécifiques dans l’environnement. Vous pouvez utiliser cette fonctionnalité pour superposer des instructions pas à pas guidées par-dessus des machines pour l’entreprise industrielle ou ajouter des fonctionnalités et expériences numériques à un produit ou un jeu physique.

Pour une plus grande flexibilité lors du développement de l’expérience AR, le moteur Vuforia offre un large éventail de fonctionnalités et de cibles. L’une de nos fonctionnalités les plus récentes, Vuforia Model targets, est une fonctionnalité clé pour les utilisations commerciales et industrielles. Les cibles de modèle permettent aux applications de reconnaître des objets physiques tels que des machines, des automobiles ou des jouets et de les suivre en fonction d’un modèle de CAO ou d’un modèle 3D numérique. Pour les utilisations industrielles, cette fonctionnalité permet aux travailleurs d’assemblage et aux techniciens de service d’utiliser des instructions de travail et des instructions de procédure dans la fabrique ou dans le champ.

Les applications de moteur Vuforia existantes qui ont été générées pour les téléphones et les tablettes peuvent être facilement configurées dans Unity pour s’exécuter sur HoloLens. Vous pouvez même utiliser le moteur Vuforia pour placer votre nouvelle application HoloLens sur des tablettes Windows 10, telles que surface Pro et surface Book.


## <a name="get-the-tools"></a>Obtenir les outils

[Installez les versions recommandées](install-the-tools.md) de Visual Studio et Unity, puis configurez Unity pour utiliser Visual Studio et l’IDE et le compilateur préférés. 

Lors de l’installation d’Unity, veillez à installer le « backend de script IL2CPP Windows Store ».

L’ajout de la prise en charge du moteur Vuforia fonctionne différemment selon votre version d’Unity :
*   Unity 2018,4 : Télécharger le programme d’installation du moteur Vuforia pour Unity 2018,4 à partir du portail des développeurs Vuforia
*   Unity 2019,2 : Procurez-vous le dernier [package de moteur Vuforia](https://library.vuforia.com/content/vuforia-library/en/articles/Solution/vuforia-engine-package-hosting-for-unity.html) 

## <a name="getting-started-with-vuforia-engine"></a>Prise en main du moteur Vuforia

Le meilleur point de départ pour apprendre à utiliser le moteur Vuforia avec HoloLens est l' [exemple hololens du moteur Vuforia](https://assetstore.unity.com/packages/templates/packs/vuforia-hololens-sample-101553) (disponible dans le magasin d’actifs Unity). L’exemple fournit un projet HoloLens complet, y compris des scènes préconfigurées qui peuvent être déployées sur un HoloLens.

Les scènes montrent comment utiliser des cibles d’image Vuforia pour reconnaître une image et l’enrichir avec du contenu numérique dans une expérience HoloLens. L’exemple Hololens du moteur Vuforia comprend également une scène qui montre l’utilisation des cibles du modèle et VuMarks sur HoloLens. Vous pouvez facilement substituer votre propre contenu en coulisses pour expérimenter la création d’applications HoloLens qui utilisent le moteur Vuforia.



## <a name="configuring-a-vuforia-app-for-hololens"></a>Configuration d’une application Vuforia pour HoloLens

Le développement d’une application de moteur Vuforia pour HoloLens est fondamentalement identique au développement d’applications de moteur Vuforia pour d’autres appareils. Vous pouvez ensuite appliquer les paramètres de build et les configurations décrits dans la section ci-dessous. C’est tout ce qui est nécessaire pour permettre au moteur Vuforia de fonctionner avec les systèmes de mappage spatial et de suivi positionnel de HoloLens.

## <a name="build-and-run-the-vuforia-engine-sample-for-hololens"></a>Générer et exécuter l’exemple de moteur Vuforia pour HoloLens
1.  Télécharger l' [exemple de moteur Vuforia pour HoloLens](https://assetstore.unity.com/packages/templates/packs/vuforia-hololens-sample-101553) à partir du magasin d’actifs Unity
2.  Appliquer les [options de moteur Unity recommandées pour l’alimentation et les performances](performance-recommendations-for-unity.md)
3.  Ajoutez les exemples de scènes aux scènes dans la Build.
4.  Définissez votre cible de génération de plateforme pour « plateforme Windows universelle » dans les paramètres de génération > de fichiers.
5.  Sélectionnez les paramètres de configuration de build de la plateforme suivants : 
   * Appareil cible = HoloLens
   * Type de build = D3D
   * SDK = dernière version installée
   * Version de Visual Studio = dernière version installée
   * Générer et exécuter sur = ordinateur local
6.  Définissez un **nom de produit**unique, dans **paramètres du lecteur**, pour servir de nom à l’application lorsqu’elle est installée sur HoloLens.
7.  Vérifier la **réalité augmentée de Vuforia** et **la réalité virtuelle prise en charge** dans les **paramètres du lecteur > paramètres XR**
8.  En outre, sous **paramètres de XR**, assurez-vous que « Windows Mixed Reality » est ajouté à la liste des kits de développement logiciel (SDK) de **réalité virtuelle**
9.  Vérifiez les fonctionnalités suivantes dans les paramètres du lecteur > paramètres de publication 
   * InternetClient
   * WebCam
   * SpatialPerception : Si vous envisagez d’utiliser l’API observateur de surface
10. Sélectionnez générer pour générer un projet Visual Studio
11. Générer le fichier exécutable à partir de Visual Studio et l’installer sur votre HoloLens

Remarque : à compter de la version 7,2, l’exemple de moteur Vuforia pour HoloLens inclut un exemple de scène, y compris l’utilisation d’exemples de cibles de modèle

## <a name="the-vuforia-developer-portal"></a>Portail des développeurs Vuforia

Les développeurs qui cherchent à créer leurs propres expériences AR avec le moteur Vuforia et HoloLens doivent s’inscrire sur notre portail des développeurs Vuforia sur [Developer.vuforia.com](https://developer.vuforia.com/). Dans le portail, les développeurs ont accès aux [forums du moteur Vuforia](https://developer.vuforia.com/forum) où ils peuvent rejoindre les discussions de la Communauté, une [bibliothèque](https://library.vuforia.com/) avec une documentation détaillée sur toutes les fonctionnalités du moteur Vuforia, et le [Gestionnaire cible Vuforia](https://developer.vuforia.com/target-manager) où les utilisateurs peuvent créer leurs propres cibles personnalisées. Les développeurs peuvent également s’inscrire pour obtenir une licence de développeur gratuite à l’aide du [Gestionnaire de licences Vuforia](https://developer.vuforia.com/license-manager).

## <a name="extended-tracking-with-vuforia"></a>Suivi étendu avec Vuforia

Le [suivi étendu](https://library.vuforia.com/articles/Training/Extended-Tracking) gère le suivi, même lorsqu’une cible n’est plus en vue. Elle est automatiquement activée pour toutes les cibles lorsque le dispositif de suivi de périphérique positionnel est activé. Pour les applications HoloLens, le dispositif de suivi positionnel est démarré automatiquement dans Unity.

Le moteur Vuforia fusionne automatiquement les poses du suivi de l’appareil photo et du suivi spatial de HoloLens pour fournir des poses cibles stables, indépendamment du fait que la cible est ou non visible par l’appareil photo.

Étant donné que le processus est géré automatiquement, il ne nécessite pas de programmation par le développeur.


**Voici ce qui se produit...**
1. Le dispositif de suivi cible de Vuforia reconnaît la cible
2. Le suivi cible est ensuite initialisé
3. La position et la rotation de la cible sont analysées pour fournir une estimation de pose robuste pour HoloLens
4. Le moteur Vuforia transforme la pose de la cible dans l’espace de coordonnées de mappage spatial HoloLens
5. HoloLens prend le contrôle du suivi si la cible n’est plus dans la vue. À chaque fois que vous examinez à nouveau la cible, Vuforia continuera à suivre les images et les objets avec précision.

Les cibles qui sont détectées, mais qui ne sont plus en vue, sont signalées comme EXTENDED_TRACKED. Dans ce cas, le script DefaultTrackableEventHandler utilisé sur toutes les cibles continue d’afficher le contenu d’augmentation. Le développeur peut contrôler ce comportement en implémentant un script de gestionnaire d’événements suivi personnalisé.


## <a name="performance-mode-with-vuforia-engine"></a>Mode de performance avec moteur Vuforia 

Il est possible d’utiliser le moteur Vuforia pour gérer les performances de la gestion des ressources de l’unité (HoloLens) et réduire la charge de travail sur le processeur. Le moteur Vuforia offre trois modes qui peuvent être sélectionnés : par défaut, pour optimiser la vitesse et pour optimiser la qualité. 

*   MODE_OPTIMIZE_SPEED vous permet de réduire la charge de travail sur l’appareil HoloLens et est parfait pour l’extension des expériences de l’AR. Il est recommandé dans les situations où l’application effectue le suivi des objets/cibles statiques.
*   MODE_DEFAULT est le mode normal qui peut être utilisé dans la plupart des scénarios.
*   MODE_OPTIMIZE_QUALITY est mieux adapté au suivi des cibles mobiles ou des cibles de modèle que vous prévoyez de choisir.

**Définition du mode**

Pour modifier le mode de performance dans Unity, accédez à configuration de Vuforia (Ctrl + Maj + V/Cmd + Maj + V) qui se trouve en tant que composant dans le GameObject ARCamera. 
*   Sélectionnez le menu déroulant mode périphérique de l’appareil photo et sélectionnez l’une des trois options.


## <a name="see-also"></a>Articles associés
* [Installer les outils](install-the-tools.md)
* [Systèmes de coordonnées](coordinate-systems.md)
* [Mappage spatial](spatial-mapping.md)
* [Appareil photo dans Unity](camera-in-unity.md)
* [Exportation et création de solutions Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md)
* [Documentation Vuforia : développement pour Windows 10 dans Unity](https://library.vuforia.com/articles/Solution/Developing-for-Windows-10-in-Unity)
* [Documentation Vuforia : comment installer l’extension Vuforia Unity](https://library.vuforia.com/articles/Solution/Installing-the-Unity-Extension)
* [Documentation Vuforia : utilisation de l’exemple HoloLens dans Unity](https://library.vuforia.com/articles/Solution/Working-with-the-HoloLens-sample-in-Unity)
* [Documentation Vuforia : suivi étendu dans Vuforia](https://library.vuforia.com/articles/Training/Extended-Tracking)
