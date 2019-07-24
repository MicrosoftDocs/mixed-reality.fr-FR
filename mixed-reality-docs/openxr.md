---
title: OpenXR
description: Essayez l’API OpenXR 0,90 provisoire avec la préversion de la réalité mixte OpenXR developer preview.
author: thetuvix
ms.author: alexturn
ms.date: 3/18/2019
ms.topic: article
keywords: Version préliminaire du développeur OpenXR pour la réalité mixte
ms.openlocfilehash: 723b0b85785d4b6dd735430aa76a24b9ce05b5c7
ms.sourcegitcommit: 8d6e5723283c03f984f1fafef81afa5aab5d04bc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66039182"
---
# <a name="openxr"></a>OpenXR

OpenXR est une norme ouverte gratuite de [Khronos](https://www.khronos.org/) qui fournit un accès natif à un large éventail d’appareils de nombreux fournisseurs qui s’étendent sur le spectre de la [réalité mixte](mixed-reality.md).

Avec OpenXR, vous pouvez créer des applications qui ciblent les deux appareils holographiques (tels que HoloLens 2) qui placent du contenu numérique dans le monde réel comme s’il existait vraiment, ainsi que des appareils immersifs (tels que des casques Windows mixtes de réalité pour ordinateurs de bureau) qui masquent les le monde physique et remplacez-le par une expérience numérique.  OpenXR vous permet d’écrire du code une fois qui est ensuite portable sur une large gamme de plateformes matérielles.

La norme OpenXR est actuellement en phase provisoire, avec une spécification initiale de OpenXR 0,90 publiée pour les commentaires.  Pour plus d’informations sur OpenXR, y compris l’accès aux spécifications et [en-têtes](https://github.com/KhronosGroup/OpenXR-Docs/tree/master/include/openxr) [0,90 provisoires](https://www.khronos.org/registry/OpenXR/specs/0.90/html/xrspec.html) , consultez la [page Khronos OpenXR](https://www.khronos.org/openxr/). 

Vous pouvez essayer l’API OpenXR 0,90 provisoire sur un HoloLens 2 ou un ordinateur de bureau à l’aide de la préversion de la réalité mixte OpenXR developer preview.  Ce Runtime précoce permet aux applications ciblant l’API OpenXR 0,90 de cibler des casques Windows HoloLens 2 ou Windows Mixed Reality sur le bureau.

Si vous n’avez pas accès à un casque, vous pouvez utiliser l’émulateur HoloLens 2 ou Windows Mixed Reality Simulator à la place.

## <a name="setting-up-the-mixed-reality-openxr-developer-preview-for-hololens-2"></a>Configuration de la version d’évaluation de la réalité mixte OpenXR pour les développeurs pour HoloLens 2

Pour commencer à utiliser la version mixte OpenXR developer preview sur HoloLens 2:

1. Configurez un HoloLens 2 ou suivez les instructions pour [installer l’émulateur hololens 2](using-the-hololens-emulator.md).
1. Lancez l’application du Windows Store à partir de l’appareil ou de l’émulateur et assurez-vous que toutes les applications sont mises à jour.  Cette opération installe la version préliminaire du développeur OpenXR en réalité mixte pour une utilisation avec les applications sur cet appareil.  Si vous utilisez l’émulateur, vous souhaiterez consulter les [instructions d’entrée](using-the-hololens-emulator.md#basic-emulator-input) de l’émulateur pour vous aider à utiliser l’application du Windows Store dans l’émulateur.

## <a name="setting-up-the-mixed-reality-openxr-developer-preview-for-immersive-desktop-headsets"></a>Configuration de la version d’évaluation de la réalité mixte OpenXR developer preview pour les casques de bureau immersifs

Pour commencer à utiliser la version d’évaluation OpenXR Developer de la réalité mixte sur un PC de bureau:

1. Vérifiez que vous exécutez la mise à jour 2018 de Windows 10 octobre (1809) ou la mise à jour de Windows 10 mai 2019 (1903).  Si vous utilisez une version antérieure de Windows 10, vous pouvez effectuer la mise à niveau vers la mise à jour 2019 de mai à l’aide de l' [Assistant Mise à jour de Windows 10](https://www.microsoft.com/en-us/software-download/windows10).
1. Configurez un casque Windows Mixed Reality ou suivez les instructions pour [activer le simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md).
1. Installez l' [Application Developer OpenXR developer preview](https://www.microsoft.com/store/productId/9n5cvvl23qbt).  Cette application vous permet de configurer avec la version préliminaire de OpenXR Runtime sur Windows 10 octobre 2018 Update (1809) ou version ultérieure.  Après l’installation de cette application, le Windows Store garde le runtime à jour.
1. Exécutez l’application OpenXR Developer de la réalité mixte à partir du menu Démarrer et suivez les instructions pour rendre le runtime actif.  Bientôt, cette application vous permet d’explorer d’autres informations de débogage OpenXR également.

![Application en version préliminaire développeur OpenXR en réalité mixte](images/mixed-reality-openxr-developer-preview.png)

### <a name="support-for-windows-10-october-2018-update"></a>Prise en charge de Windows 10 octobre 2018 mise à jour

Si vous exécutez la mise à jour de Windows 10 2019 (1903) et que vous avez suivi les étapes ci-dessus, vous devez être prêt à utiliser la version préliminaire OpenXR Developer de la réalité mixte.

Si vous n’êtes pas prêt à [mettre à niveau votre PC de bureau vers la mise à jour 2019 de mai](https://www.microsoft.com/en-us/software-download/windows10), vous pouvez vous rendre sur la mise à jour de Windows 10 octobre 2018 (1809) en suivant une étape supplémentaire:

1. Suivez les étapes ci-dessus pour installer la version d’évaluation du développeur OpenXR en réalité mixte.
1. Pour définir la version d’évaluation du développeur OpenXR en réalité mixte comme le runtime OpenXR actif de votre système, installez le Pack de compatibilité de l’aperçu de la [réalité mixte OpenXR developer preview](https://aka.ms/openxr-compat).

## <a name="building-a-sample-openxr-app"></a>Création d’un exemple d’application OpenXR

Le projet [BasicXrApp](https://github.com/Microsoft/OpenXR-SDK-VisualStudio/tree/master/samples/BasicXrApp) illustre un exemple OpenXR simple avec deux fichiers projet Visual Studio, un pour une application de bureau Win32 et un pour une application UWP 2 UWP.  Étant donné que la solution contient un projet UWP HoloLens, vous avez besoin de la [charge de travail de développement plateforme Windows universelle](install-the-tools.md#installation-checklist) installée dans Visual Studio pour l’ouvrir entièrement.

Notez que, bien que les fichiers de projet Win32 et UWP soient distincts en raison des différences d’empaquetage et de déploiement, le code de l’application à l’intérieur de chaque projet est de 100% le même!

## <a name="feedback"></a>Commentaires

Pour nous faire part de vos commentaires sur la [spécification OpenXR provisoire 0,90](https://www.khronos.org/registry/OpenXR/specs/0.90/html/xrspec.html), visitez les [Forums Khronos OpenXR](https://community.khronos.org/c/openxr), la [marge #openxr canal](https://khr.io/slack) et le [suivi des problèmes des spécifications](https://github.com/KhronosGroup/OpenXR-Docs/issues).

## <a name="troubleshooting"></a>Résolution des problèmes

Voici quelques conseils de dépannage pour la préversion de la réalité mixte OpenXR developer preview.  Si vous rencontrez d’autres problèmes, consultez les [Forums Khronos OpenXR](https://community.khronos.org/c/openxr) ou la [marge #openxr canal](https://khr.io/slack).

### <a name="openxr-app-not-starting-windows-mixed-reality"></a>Application OpenXR ne démarrant pas Windows Mixed Reality

Si votre application OpenXR ne démarre pas Windows Mixed Reality quand vous l’exécutez, la préversion de la réalité mixte OpenXR Developer ne peut pas être définie comme étant active Runtime.  Veillez à exécuter l’application OpenXR Developer de la réalité mixte et suivez les instructions pour activer le Runtime.

### <a name="mixed-reality-openxr-developer-preview-app-cannot-be-installed"></a>Impossible d’installer l’application Developer OpenXR developer preview 

Assurez-vous que vous exécutez au moins la mise à jour 2018 de Windows 10 octobre (1809).  Si vous utilisez une version antérieure de Windows 10, vous pouvez effectuer la mise à niveau vers la mise à jour 2019 (1903) à l’aide de l' [Assistant Mise à jour de Windows 10](https://www.microsoft.com/en-us/software-download/windows10).

Si le bouton installer de l’application Developer OpenXR developer preview ne fait rien sur la mise à jour 2018 d’octobre de Windows 10, votre système peut avoir mis en cache une configuration système périmée pour l’application.  Vous pouvez exécuter la commande `wsreset.exe` à partir d’une invite de commandes pour effacer le cache.

## <a name="see-also"></a>Voir aussi

* [Plus d’informations sur OpenXR](https://www.khronos.org/openxr/)
* [OpenXR spécification 0,90 provisoire](https://www.khronos.org/registry/OpenXR/specs/0.90/html/xrspec.html)
* [Référence de l’API 0,90 provisoire OpenXR](https://www.khronos.org/registry/OpenXR/specs/0.90/man/html/)
* [OpenXR les en-têtes 0,90 provisoires](https://github.com/KhronosGroup/OpenXR-Docs/tree/master/include/openxr)
* [Guide de référence rapide 0,90 provisoire](https://www.khronos.org/registry/OpenXR/specs/0.90/refguide/OpenXR-0.90-web.pdf)
