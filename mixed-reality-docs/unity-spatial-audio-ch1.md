---
title: Didacticiels audio spatial-1. Ajout de données audio spatiales à votre projet
description: Ajoutez le plug-in Microsoft Spatializer à votre projet Unity pour accéder au déchargement matériel HoloLens 2 HRTF.
author: kegodin
ms.author: kegodin
ms.date: 12/01/2019
ms.topic: article
keywords: réalité mixte, Unity, tutorial, hololens2, audio spatial
ms.openlocfilehash: 8978017b3ce6c49a81b3eee2fe21e9234f4e71f0
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75182796"
---
# <a name="adding-spatial-audio-to-your-unity-project"></a>Ajout de données audio spatiales à votre projet Unity

Bienvenue dans le tutioral de l’audio spatial pour Unity sur HoloLens2. Cette séquence de didacticiel présente les éléments suivants :
* Utilisation du déchargement de HRTF sur HoloLens 2 dans Unity
* Comment activer le réverbe lors de l’utilisation du déchargement HRTF

Le [dépôt github Microsoft Spatializer](https://github.com/microsoft/spatialaudio-unity) a un projet Unity terminé de cette séquence de didacticiels. 

Pour obtenir des recommandations sur le moment où il peut être utile d’les sons, consultez [conception de son spatial](https://docs.microsoft.com/windows/mixed-reality/spatial-sound-design).

## <a name="objectives"></a>Objectifs
Dans ce premier chapitre, vous allez :
* Créer un projet Unity et importer MRTK
* Importer le plug-in Microsoft Spatializer
* Activer le plug-in Microsoft Spatializer
* Activer l’audio spatial sur votre station de travail de développeur

## <a name="create-a-project-and-add-nuget-for-unity"></a>Créer un projet et ajouter NuGet pour Unity
Commencez avec un projet Unity vide, puis ajoutez et configurez NuGet pour Unity :
1. Téléchargez la dernière version de [NuGetForUnity. pour Unity](https://github.com/GlitchEnzo/NuGetForUnity/releases/latest)
2. Dans la barre de menus Unity, cliquez sur **ressources-> importer un package-> package personnalisé...** et installer le package NuGetForUnity :

![Importer un package personnalisé](images/spatial-audio/import-custom-package.png)

## <a name="add-the-windows-mixed-reality-package"></a>Ajouter le package Windows Mixed Reality
La prise en charge de Windows Mixed Reality dans Unity 2019 et versions ultérieures est contenue dans un package facultatif. Pour l’ajouter à votre projet, ouvrez la **fenêtre > gestionnaire de package** à partir de la barre de menus Unity :

![Menu du gestionnaire de package](images/spatial-audio/package-manager-menu.png)

Recherchez et installez le package **Windows Mixed Reality** :

![Fenêtre du gestionnaire de package](images/spatial-audio/package-manager-window.png)

## <a name="install-mrtk-and-microsoft-spatializer"></a>Installer MRTK et Microsoft Spatializer
À l’aide de NuGet pour Unity, installez les plug-ins MRTK et Microsoft Spatializer :
1. Dans la barre de menus de Unity, cliquez sur **NuGet-> gérer les packages NuGet**.

![Gérer des packages NuGet](images/spatial-audio/manage-nuget-packages.png)

2. Dans la zone de **recherche** , entrez « Microsoft. MixedReality. Toolkit » et installez le package MRTK Core : **Microsoft. MixedReality. Toolkit. Foundation**

![Package NuGet MRTK](images/spatial-audio/mrtk-nuget-package.png)

Le [package NuGet MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MRTKNuGetPackage.html) contient un contexte et des détails supplémentaires.

4. Dans la zone de **recherche** , entrez « Microsoft. SpatialAudio » et installez le package Microsoft Spatializer : **Microsoft. SpatialAudio. Spatializer. Unity**

![Plug-in Spatializer NuGet](images/spatial-audio/spatializer-plugin-nuget.png)

## <a name="set-up-mrtk-in-your-project"></a>Configurer MRTK dans votre projet

1. Ouvrez la fenêtre Paramètres de build en accédant à **fichiers-> paramètres de build**.

2. Sélectionnez le _plateforme Windows universelle_ , puis cliquez sur **basculer la plateforme**.

3. Cliquez sur **paramètres du lecteur** dans la **fenêtre générer** pour ouvrir les propriétés des **paramètres du lecteur** dans le volet **inspecteur** .
    * Sous **paramètres de XR**, activez la case à cocher **réalité virtuelle prise en charge**
    * Sous **paramètres XR**, définissez le **mode de rendu stéréo** sur **Single-instanced**.
    * Sous **paramètres de publication**, activez la case à cocher **perception spatiale** dans la section **fonctionnalités** .

4. Dans la barre de menus, cliquez sur **Kit de pratiques de réalité mixte-> ajouter à la scène et configurer.** pour ajouter MRTK à votre scène.

Pour obtenir des conseils supplémentaires, notamment la façon de créer votre application et de la déployer sur un HoloLens 2, consultez [le chapitre 1 du module de base de l’apprentissage de RM](mrlearning-base-ch1.md).

## <a name="enable-the-microsoft-spatializer-plugin"></a>Activer le plug-in Microsoft Spatializer
Activez le plug-in **Microsoft Spatializer** . Ouvrez les **paramètres de projet Edit->-> audio**, puis remplacez le **plug-in Spatializer** par "Microsoft Spatializer". La section **audio** des **paramètres du projet** doit maintenant ressembler à ceci :

![Paramètres du projet présentant le plug-in Spatializer](images/spatial-audio/project-settings.png)

## <a name="enable-spatial-audio-on-your-workstation"></a>Activer l’audio spatial sur votre station de travail
Sur les versions de bureau de Windows, l’audio spatial est désactivé par défaut. Pour l’activer, cliquez avec le bouton droit sur l’icône de volume dans la barre des tâches. Pour obtenir la meilleure représentation de ce que vous entendez sur HoloLens 2, choisissez **son Spatial > Windows Sonic pour casque**.

![Paramètres audio spatiaux du Bureau](images/spatial-audio/desktop-audio-settings.png)

> [!NOTE]
> Ce paramètre est requis uniquement si vous envisagez de tester votre projet dans l’éditeur Unity.

## <a name="next-steps"></a>Étapes suivantes
Passez à [Unity audio spatial chapitre 2](unity-spatial-audio-ch2.md) pour effectuer l’spatiale des sons d’interaction du bouton.

