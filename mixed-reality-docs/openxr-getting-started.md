---
title: Prise en main de OpenXR
description: Prise en main de l’API OpenXR portable standard sur Windows Mixed Reality et les casques HoloLens 2.
author: thetuvix
ms.author: alexturn
ms.date: 2/28/2020
ms.topic: article
keywords: OpenXR, Khronos, BasicXRApp, Windows Mixed Reality OpenXR portail des développeurs, DirectX, native, application native, moteur personnalisé, intergiciel, prise en main, 101, extensions préliminaires
ms.openlocfilehash: db45308834f920413420f080a35b378f6a55fa49
ms.sourcegitcommit: 536fd45b48a70bbeca1454cef517ae007225e533
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2020
ms.locfileid: "80362032"
---
# <a name="getting-started-with-openxr"></a>Prise en main de OpenXR

Vous pouvez développer à l’aide de OpenXR sur un casque de l’architecture HoloLens 2 ou Windows Mixed Reality sur le bureau.  Si vous n’avez pas accès à un casque, vous pouvez utiliser l’émulateur HoloLens 2 ou Windows Mixed Reality Simulator à la place.

## <a name="getting-started-with-openxr-for-hololens-2"></a>Prise en main de OpenXR pour HoloLens 2

Pour commencer à développer des applications OpenXR pour HoloLens 2 :

1. Configurez un HoloLens 2 ou suivez les instructions pour [installer une version récente de l’émulateur hololens 2](using-the-hololens-emulator.md).  Si votre appareil a récemment mis à jour son système d’exploitation ou si vous utilisez une image d’émulateur récente, OpenXR 1,0 doit déjà être prêt à l’emploi.
1. Pour vous assurer que vous disposez de la dernière version du runtime OpenXR avec toutes les [Extensions](openxr.md#roadmap) présentes, lancez l’application du Windows Store à partir de l’appareil ou de l’émulateur, ouvrez le menu en haut à droite, cliquez sur **téléchargements et mises à jour** , puis cliquez sur **récupérer les mises à jour**.  Cela garantit que le runtime OpenXR sur votre HoloLens est à jour.  Notez que si vous utilisez l’émulateur, l’image de l’émulateur est réinitialisée chaque fois que vous le démarrez. votre meilleur résultat est de vous assurer que vous disposez [de la dernière version de l’image de l’émulateur HoloLens 2](using-the-hololens-emulator.md).

## <a name="getting-started-with-openxr-for-windows-mixed-reality-headsets"></a>Prise en main de OpenXR pour les casques Windows Mixed Reality

Pour commencer à développer des applications OpenXR pour des casques Windows mixtes immersifs :

1. Assurez-vous que vous exécutez au moins la mise à jour Windows 10 2019 (1903), qui est la configuration minimale requise pour que les utilisateurs finaux Windows Mixed realisation exécutent des applications OpenXR.  Si vous utilisez une version antérieure de Windows 10, vous pouvez procéder à une mise à niveau à l’aide de l' <a href="https://www.microsoft.com/software-download/windows10" target="_blank">Assistant Mise à jour de Windows 10</a>.
2. Configurez un casque Windows Mixed Reality ou suivez les instructions pour [activer le simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md).  Quand vous configurez Windows Mixed Reality, le portail de réalité mixte installe automatiquement le runtime OpenXR Windows Mixed Reality.  Le Microsoft Store garde alors le runtime à jour.
3. Rendez le runtime OpenXR Windows Mixed Reality actif en lançant le portail de réalité mixte à partir du menu Démarrer, en cliquant sur le bouton... dans l’angle inférieur gauche, puis en sélectionnant « Configurer OpenXR ».<br>
![la configuration de OpenXR dans le portail de réalité mixte](images/mixed-reality-portal-set-up-openxr.png)

Si vous devez faire en sorte que le runtime OpenXR Windows Mixed Reality soit à nouveau actif, répétez l’étape 3.

> [!NOTE]
> Le runtime Windows Mixed Reality OpenXR sera bientôt activé automatiquement pour tous les utilisateurs finaux de Windows Mixed Reality.

## <a name="getting-the-windows-mixed-reality-openxr-developer-portal"></a>Obtention du portail des développeurs OpenXR Windows Mixed Reality

Pour tester le runtime OpenXR Windows Mixed Reality, vous pouvez installer l' <a href="https://www.microsoft.com/store/productId/9n5cvvl23qbt" target="_blank">application de portail de développement OpenXR de la réalité mixte</a>.  Cette application fournit une scène de démonstration qui exerce diverses fonctionnalités de OpenXR, ainsi qu’une page d’État du système qui fournit des informations clés sur le runtime actif et le casque actuel.

Si vous utilisez l’émulateur, le moyen le plus simple d’installer le portail de développement OpenXR de la réalité mixte consiste à utiliser le [portail des appareils Windows](using-the-windows-device-portal.md), en accédant à la page « OpenXR », puis en cliquant sur le bouton « installer » sous « fonctionnalités pour les développeurs ». (cela fonctionne également sur un appareil HoloLens 2 physique)

![Application du portail des développeurs OpenXR de la réalité mixte](images/mixed-reality-openxr-developer-portal.png)

## <a name="building-a-sample-openxr-app"></a>Création d’un exemple d’application OpenXR

Veillez à [installer les outils](install-the-tools.md) dont vous aurez besoin pour le développement OpenXR si vous ne l’avez pas déjà fait.

Le projet <a href="https://github.com/microsoft/OpenXR-MixedReality/tree/master/samples/BasicXrApp" target="_blank">BasicXrApp</a> illustre un exemple OpenXR simple avec deux fichiers projet Visual Studio, un pour une application de bureau Win32 et un pour une application UWP 2 UWP.  Étant donné que la solution contient un projet UWP HoloLens, vous avez besoin de la [charge de travail de développement plateforme Windows universelle](install-the-tools.md#installation-checklist) installée dans Visual Studio pour l’ouvrir entièrement.

Notez que, bien que les fichiers de projet Win32 et UWP soient distincts en raison des différences d’empaquetage et de déploiement, le code de l’application à l’intérieur de chaque projet est de 100% le même !

Après la génération d’un bureau OpenXR Win32. EXE, vous pouvez l’utiliser avec un casque VR sur toute plateforme Desktop VR qui prend en charge OpenXR, qu’il s’agisse d’un casque Windows Mixed Reality ou de tout autre casque.

Après avoir créé un package d’application OpenXR UWP, vous pouvez [déployer ce package](using-visual-studio.md) sur un appareil hololens 2 ou sur l’émulateur hololens 2.

## <a name="integrate-the-openxr-loader-into-a-project"></a>Intégrer le chargeur OpenXR dans un projet

Pour commencer à utiliser OpenXR dans un projet existant, vous devez inclure le chargeur OpenXR.  Le chargeur Découvre le runtime OpenXR actif sur l’appareil et donne accès aux fonctions de base et aux fonctions d’extension qu’il implémente.

Vous pouvez soit [référencer le package NuGet officiel OpenXR](#reference-official-openxr-nuget-package) à partir de votre projet Visual Studio, soit [inclure la source officielle OpenXR Loader](#include-official-openxr-loader-source) à partir du Khronos GitHub référentiel.  Les deux approches vous permettront d’accéder aux fonctionnalités principales de OpenXR 1,0, ainsi qu’aux extensions `KHR`, `EXT` et `MSFT` publiées.

Si vous souhaitez faire des essais avec les extensions de `MSFT_preview` également, vous pouvez copier les en [-têtes OpenXR en](#using-preview-extensions) préversion à partir du GitHub référentiel de la réalité mixte.

### <a name="reference-official-openxr-nuget-package"></a>Référencer le package NuGet officiel OpenXR

Le <a href="https://www.nuget.org/packages/OpenXR.Loader/" target="_blank">package NuGet **OpenXR. Loader** </a> est le moyen le plus simple de référencer un chargeur OpenXR prédéfini. DLL dans votre solution Visual C++ Studio.  Cela vous permet d’accéder aux fonctionnalités principales de OpenXR 1,0, ainsi qu’aux extensions `KHR`, `EXT` et `MSFT` publiées.

Pour ajouter une référence de package NuGet OpenXR. Loader à votre solution Visual C++ Studio :
1. Dans **Explorateur de solutions**, cliquez avec le bouton droit sur le projet qui utilisera OpenXR et sélectionnez **gérer les packages NuGet...** .
1. Basculez vers l’onglet **Parcourir** et recherchez **OpenXR. Loader**.
1. Sélectionnez le package **OpenXR. Loader** , puis cliquez sur installer dans le volet des détails à droite.
1. Cliquez sur OK pour accepter les modifications apportées à votre projet.
1. Ajoutez `#include <openxr/openxr.h>` à un fichier source pour commencer à utiliser l’API OpenXR.

Pour voir un exemple de l’API OpenXR en action, consultez l’exemple d’application <a href="https://github.com/microsoft/OpenXR-MixedReality/tree/master/samples/BasicXrApp" target="_blank">BasicXrApp</a> .

### <a name="include-official-openxr-loader-source"></a>Inclure la source de chargeur OpenXR officielle

Si vous souhaitez créer vous-même le chargeur, par exemple pour éviter le chargeur supplémentaire. DLL, vous pouvez extraire les sources officielles Khronos OpenXR Loader dans votre projet.  Cela vous permet d’accéder aux fonctionnalités principales de OpenXR 1,0, ainsi qu’aux extensions `KHR`, `EXT` et `MSFT` publiées.

Pour commencer, suivez les instructions de la <a href="https://github.com/KhronosGroup/OpenXR-SDK" target="_blank">Khronos OpenXR-SDK référentiel sur GitHub</a>.  Le projet est configuré pour être généré avec CMake : Si vous utilisez MSBuild, vous devrez copier vers le code dans votre propre projet.

## <a name="using-preview-extensions"></a>Utilisation des extensions d’aperçu

Les extensions de `MSFT_preview` répertoriées dans la feuille de [route d’extension](openxr.md#roadmap) sont des extensions de fournisseur expérimentales prévisualisées pour recueillir des commentaires.  Ces extensions sont destinées aux appareils de développement uniquement et seront supprimées lors de la livraison de l’extension réelle.

Si vous souhaitez essayer les extensions de `MSFT_preview` disponibles, suivez les étapes ci-dessous pour mettre à jour votre projet :
1. Suivez l’une des approches ci-dessus pour intégrer un chargeur OpenXR à votre projet.
1. Remplacez les en-têtes OpenXR standard de votre projet par les <a href="https://github.com/microsoft/OpenXR-MixedReality/tree/master/openxr_preview/include/openxr" target="_blank">en-têtes d’aperçu de la OpenXR de la réalité mixte référentiel sur GitHub</a>.

Pour activer les extensions de préversion sur votre ordinateur de bureau ou HoloLens 2 cible :
  1. Activer le portail d’appareils Windows sur l’appareil cible :
     * Si votre appareil cible est un appareil HoloLens 2, [suivez ces instructions](using-the-windows-device-portal.md) sur l’appareil cible.  Notez que cela nécessite un casque physique, comme un problème connu dans l’émulateur HoloLens 2 empêche l’interface utilisateur dans l’étape suivante de s’afficher dans l’émulateur.
     * Si votre appareil cible est un PC de bureau équipé d’un périphérique de casque immersif, <a href="https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-desktop#set-up-device-portal-on-windows-desktop" target="_blank">suivez ces instructions</a> sur le PC de bureau cible.
  1. Accédez à l’onglet **OpenXR** dans le volet gauche et activez **utiliser la dernière version d’évaluation de OpenXR Runtime**.  Cela active le runtime Preview sur votre appareil, pour lequel les extensions d’aperçu sont activées.

Pour obtenir de la documentation sur ces extensions préliminaires et des exemples d’utilisation, consultez le <a href="https://github.com/microsoft/OpenXR-MixedReality#openxr-preview-extensions" target="_blank">référentiel OpenXR de la réalité mixte</a> .

## <a name="troubleshooting"></a>Résolution des problèmes

Si vous ne parvenez pas à vous lancer avec le développement OpenXR, consultez nos [conseils de dépannage](openxr-troubleshooting.md).