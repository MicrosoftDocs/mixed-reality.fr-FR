---
title: Utilisation de Vuforia avec Unity
description: Tirez parti de Vuforia pour créer des applications Windows Mixed Reality dans Unity.
author: thetuvix
ms.author: alexturn
ms.date: 01/28/2019
ms.topic: article
keywords: Vuforia, marqueurs, coordonnées, frame de référence, suivi
ms.openlocfilehash: 0ab87a6262cbe74fd116fdc0a7045961bf8695d9
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437137"
---
# <a name="using-vuforia-engine-with-unity"></a>Utilisation du moteur Vuforia avec Unity

Le moteur Vuforia apporte une fonctionnalité importante à HoloLens, la puissance permettant de connecter les expériences AR à des images et objets spécifiques dans l’environnement. Vous pouvez utiliser cette fonctionnalité pour superposer des instructions pas à pas guidées par-dessus des machines pour l’entreprise industrielle ou ajouter des fonctionnalités et expériences numériques à un produit ou un jeu physique. 

Pour une plus grande flexibilité lors du développement de l’expérience AR, le moteur Vuforia offre un large éventail de fonctionnalités et de cibles. L’une de nos fonctionnalités les plus récentes, Vuforia Model targets, est une fonctionnalité clé pour les utilisations commerciales et industrielles. Les cibles de modèle permettent aux applications de reconnaître des objets physiques tels que des machines, des automobiles ou des jouets et de les suivre en fonction d’un modèle de CAO ou d’un modèle 3D numérique. Pour les utilisations industrielles, cette fonctionnalité permet aux travailleurs d’assemblage et aux techniciens de service d’utiliser des instructions de travail et des instructions de procédure dans la fabrique ou dans le champ. 

Les applications de moteur Vuforia existantes qui ont été générées pour les téléphones et les tablettes peuvent être facilement configurées dans Unity pour s’exécuter sur HoloLens. Vous pouvez même utiliser le moteur Vuforia pour placer votre nouvelle application HoloLens sur des tablettes Windows 10, telles que surface Pro 4 et surface Book.

## <a name="get-the-tools"></a>Obtenir les outils

[Installez les versions recommandées](install-the-tools.md) de Visual Studio et Unity, puis configurez Unity pour utiliser Visual Studio et l’IDE et le compilateur préférés. 

Lors de l’installation d’Unity, veillez à installer le « serveur principal de scripts .NET Windows Store » ou le « backend de script IL2CPP Windows Store ». En outre, veillez à sélectionner « prise en charge de la réalité augmentée Vuforia » pour activer le moteur Vuforia dans Unity.


## <a name="getting-started-with-vuforia-engine"></a>Prise en main du moteur Vuforia

Étant donné que le moteur Vuforia est intégré à Unity, les développeurs n’ont pas besoin de télécharger ni d’installer d’outils supplémentaires. La version recommandée d’Unity est le flux LTS qui est actuellement 2017,3 et comprend le moteur Vuforia 7.0.57. Le meilleur point de départ pour apprendre à utiliser le moteur Vuforia avec HoloLens est l' [exemple hololens du moteur Vuforia](https://assetstore.unity.com/packages/templates/packs/vuforia-hololens-sample-101553) (disponible dans le magasin d’actifs Unity). L’exemple fournit un projet HoloLens complet, y compris des scènes préconfigurées qui peuvent être déployées sur un HoloLens.

Les scènes montrent comment utiliser des cibles d’image Vuforia pour reconnaître une image et l’enrichir avec du contenu numérique dans une expérience HoloLens. Les développeurs qui utilisent des versions plus récentes d’Unity et Vuforia ont accès à des exemples mis à jour qui incluent une scène indiquant l’utilisation de cibles de modèle sur HoloLens. Vous pouvez facilement substituer votre propre contenu en coulisses pour expérimenter la création d’applications HoloLens qui utilisent le moteur Vuforia.


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

Les développeurs qui cherchent à créer leurs propres expériences AR avec le moteur Vuforia et HoloLens doivent s’inscrire sur notre portail des développeurs Vuforia sur [Developer.vuforia.com](https://developer.vuforia.com/). Dans le portail, les développeurs ont accès aux [forums du moteur Vuforia](https://developer.vuforia.com/forum) où ils peuvent rejoindre les discussions de la Communauté, une [bibliothèque](https://library.vuforia.com/) avec une documentation détaillée sur toutes les fonctionnalités du moteur Vuforia et le [Gestionnaire cible Vuforia](https://developer.vuforia.com/target-manager) où les utilisateurs peuvent Créez leurs propres cibles personnalisées. Les développeurs peuvent également s’inscrire pour obtenir une licence de développeur gratuite à l’aide du [Gestionnaire de licences Vuforia](https://developer.vuforia.com/license-manager).

## <a name="extended-tracking-with-vuforia"></a>Suivi étendu avec Vuforia

Le [suivi étendu](https://library.vuforia.com/articles/Training/Extended-Tracking) crée une carte de l’environnement pour maintenir le suivi, même lorsqu’une cible n’est plus en vue. Il s’agit de l’équivalent Vuforia Engines du mappage spatial effectué par HoloLens. Lorsque vous activez le suivi étendu sur une cible, vous permettez à la pose de cette cible d’être passée au système de mappage spatial. De cette façon, les cibles peuvent exister à la fois dans les systèmes de coordonnées spatiales du moteur Vuforia et HoloLens, mais pas simultanément.

![fenêtre Paramètres Unity](images/vuforia-extendedtracking.png)<br>
*Fenêtre Paramètres Unity*

**Activation du suivi étendu sur une cible**

Le moteur Vuforia transforme automatiquement la pose d’une cible qui utilise le suivi étendu dans le système de coordonnées spatiales HoloLens. Cela permet à HoloLens de prendre le suivi et d’intégrer tout contenu qui augmente dans le mappage spatial de l’environnement de la cible. Ce processus intervient entre le moteur Vuforia et les API de réalité mixte dans Unity et ne nécessite pas de programmation par le développeur ; il est géré automatiquement.

**Voici ce qui se produit...**
1. Le dispositif de suivi cible de Vuforia reconnaît la cible
2. Le suivi cible est ensuite initialisé
3. La position et la rotation de la cible sont analysées pour fournir une estimation de pose robuste à utiliser par HoloLens
4. Vuforia transforme la pose de la cible dans l’espace de coordonnées de mappage spatial HoloLens
5. HoloLens prend le relais et le dispositif de suivi Vuforia est désactivé

Le développeur peut contrôler ce processus, pour retourner le contrôle à Vuforia, en désactivant le suivi étendu sur le TargetBehaviour.

**Remarque :** À compter de Vuforia 7,2, le suivi étendu n’est plus activé sur une base par cible. Au lieu de cela, les développeurs peuvent activer le suivi des appareils pour activer des fonctionnalités similaires sur toutes les cibles de la scène.


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
