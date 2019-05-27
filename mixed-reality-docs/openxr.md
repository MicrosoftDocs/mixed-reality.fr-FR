---
title: OpenXR
description: Essayer l’API OpenXR 0,90 provisoire avec l’aperçu pour développeurs OpenXR réalité mixte.
author: thetuvix
ms.author: alexturn
ms.date: 3/18/2019
ms.topic: article
keywords: Réalité mixte OpenXR Developer Preview
ms.openlocfilehash: 723b0b85785d4b6dd735430aa76a24b9ce05b5c7
ms.sourcegitcommit: 8d6e5723283c03f984f1fafef81afa5aab5d04bc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66039182"
---
# <a name="openxr"></a>OpenXR

OpenXR est une norme ouverte libres de [Khronos](https://www.khronos.org/) qui fournit l’accès natif à un large éventail d’appareils à partir de nombreux fournisseurs qui couvrent la [spectre de réalité mixte](mixed-reality.md).

Avec OpenXR, vous pouvez créer des applications qui ciblent les appareils HOLOGRAPHIQUE (par exemple, HoloLens, 2) qui placent un contenu numérique dans le monde réel comme s’il s’agissait vraiment ce, ainsi qu’immersives périphériques (tels que les casques de réalité mixte Windows pour les ordinateurs de bureau) qui masquent la monde physique et le remplacer par une expérience numérique.  OpenXR vous permet d’écrire du code une fois que c’est portable sur un large éventail de plateformes matérielles.

La norme OpenXR est en cours d’une phase provisoire, avec une spécification OpenXR 0,90 initiale publiée pour envoyer des commentaires.  Pour plus d’informations sur OpenXR, y compris l’accès à la [spec 0,90 provisoire](https://www.khronos.org/registry/OpenXR/specs/0.90/html/xrspec.html) et [en-têtes](https://github.com/KhronosGroup/OpenXR-Docs/tree/master/include/openxr), consultez le [Khronos OpenXR page](https://www.khronos.org/openxr/). 

Vous pouvez essayer l’API OpenXR 0,90 provisoire sur un 2 HoloLens ou un PC de bureau à l’aide de l’aperçu pour développeurs OpenXR réalité mixte.  Ce runtime anticipé permet aux applications ciblant l’API OpenXR 0,90 cibler HoloLens 2 ou des casques IMMERSIFS Windows Mixed Reality sur le bureau.

Si vous n’avez pas accès à un casque, vous pouvez utiliser l’émulateur de 2 HoloLens ou le simulateur de réalité mixte Windows à la place.

## <a name="setting-up-the-mixed-reality-openxr-developer-preview-for-hololens-2"></a>Configuration de l’aperçu pour développeurs OpenXR réalité mixte pour HoloLens 2

Prise en main l’aperçu pour développeurs OpenXR réalité mixte sur HoloLens 2 :

1. Configurer un 2 HoloLens ou suivez les instructions pour [installer l’émulateur HoloLens 2](using-the-hololens-emulator.md).
1. Lancer l’application Store à partir de l’appareil ou l’émulateur et vérifier que toutes les applications sont mises à jour.  Cela installera l’aperçu pour développeurs OpenXR réalité mixte pour une utilisation avec des applications sur l’appareil.  Si vous utilisez l’émulateur, vous voudrez consulter le [émulateur d’entrée des instructions](using-the-hololens-emulator.md#basic-emulator-input) pour vous aider à utiliser l’application de Store dans l’émulateur.

## <a name="setting-up-the-mixed-reality-openxr-developer-preview-for-immersive-desktop-headsets"></a>Configuration de l’aperçu pour développeurs OpenXR réalité mixte pour des casques IMMERSIFS de bureau

Prise en main l’aperçu pour développeurs OpenXR réalité mixte sur un PC de bureau :

1. Vérifiez que vous exécutez Windows 10 octobre 2018 mise à jour (1809) ou Windows 10 peut 2019 mettre à jour (1903).  Si vous êtes sur une version antérieure de Windows 10, vous pouvez mettre à niveau vers le mai 2019 mettre à jour à l’aide de la [l’Assistant Mise à jour de Windows 10](https://www.microsoft.com/en-us/software-download/windows10).
1. Configurer un casque Windows Mixed Reality ou suivez les instructions pour [activer le simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md).
1. Installer le [Mixed Reality OpenXR Developer Preview, application](https://www.microsoft.com/store/productId/9n5cvvl23qbt).  Cette application vous permet de configurer avec la version préliminaire du runtime de OpenXR sur Windows 10 octobre 2018 mise à jour (1809) ou version ultérieure.  Après avoir installé cette application, le Windows Store conserve le runtime à jour.
1. Exécutez l’application mixte réalité OpenXR Developer Preview dans le menu Démarrer et suivez les instructions pour rendre le runtime actif.  Bientôt, cette application vous permet d’Explorer les autres informations de débogage OpenXR également.

![Réalité mixte OpenXR Developer Preview, application](images/mixed-reality-openxr-developer-preview.png)

### <a name="support-for-windows-10-october-2018-update"></a>Prise en charge de la mise à jour de Windows 10 octobre 2018

Si vous exécutez Windows 10 mai 2019 (1903) de mettre à jour et suivi les étapes ci-dessus, vous devez être prêt à utiliser l’aperçu pour développeurs OpenXR réalité mixte !

Si vous n’êtes pas prêt à [mise à niveau de votre ordinateur de bureau vers le mai 2019 mise à jour](https://www.microsoft.com/en-us/software-download/windows10), vous pouvez adopter Windows 10 octobre 2018 mettre à jour (1809) en suivant une étape supplémentaire :

1. Suivez les étapes ci-dessus pour installer l’aperçu pour développeurs OpenXR réalité mixte.
1. Pour définir l’aperçu pour développeurs OpenXR réalité mixte comme runtime de OpenXR actif de votre système, vous devez installer le [Pack de compatibilité mixte réalité OpenXR Developer Preview](https://aka.ms/openxr-compat).

## <a name="building-a-sample-openxr-app"></a>Création d’un exemple d’application OpenXR

Le [BasicXrApp](https://github.com/Microsoft/OpenXR-SDK-VisualStudio/tree/master/samples/BasicXrApp) projet illustre un exemple de OpenXR simple avec deux fichiers de projet Visual Studio, un pour à la fois une application de bureau Win32 et un pour une application UWP HoloLens 2.  Étant donné que la solution contient un projet UWP de HoloLens, vous devez le [charge de travail de développement plateforme Windows universelle](install-the-tools.md#installation-checklist) installé dans Visual Studio pour l’ouvrir entièrement.

Notez que, si les fichiers de projet Win32 et UWP sont séparés en raison des différences dans l’empaquetage et déploiement, le code d’application à l’intérieur de chaque projet est 100 % le même !

## <a name="feedback"></a>Commentaires

Pour envoyer des commentaires sur le [spécification de OpenXR provisoires 0,90](https://www.khronos.org/registry/OpenXR/specs/0.90/html/xrspec.html), visitez le [Khronos OpenXR Forums](https://community.khronos.org/c/openxr), [les canaux Slack #openxr](https://khr.io/slack) et le [spec suivi des problèmes](https://github.com/KhronosGroup/OpenXR-Docs/issues).

## <a name="troubleshooting"></a>Résolution des problèmes

Voici quelques conseils de dépannage pour l’aperçu pour développeurs OpenXR réalité mixte.  Si vous rencontrez d’autres problèmes, visitez le [Khronos OpenXR Forums](https://community.khronos.org/c/openxr) ou [les canaux Slack #openxr](https://khr.io/slack).

### <a name="openxr-app-not-starting-windows-mixed-reality"></a>Application OpenXR ne démarre ne pas Windows Mixed Reality

Si votre application OpenXR ne démarre pas Windows Mixed Reality lors de son exécution, l’aperçu pour développeurs OpenXR réalité mixte ne peuvent pas être définie en tant que le runtime actif.  Veillez à exécuter l’application mixte réalité OpenXR Developer Preview et suivez les instructions pour rendre le runtime actif.

### <a name="mixed-reality-openxr-developer-preview-app-cannot-be-installed"></a>Application de réalité OpenXR Developer Preview mixte ne peut pas être installée 

Vérifiez que vous exécutez au moins Windows 10 octobre 2018 mettre à jour (1809).  Si vous êtes sur une version antérieure de Windows 10, vous pouvez mettre à niveau vers le mai 2019 mettre à jour (1903) à l’aide de la [l’Assistant Mise à jour de Windows 10](https://www.microsoft.com/en-us/software-download/windows10).

Si l’installation de bouton sur l’application mixte réalité OpenXR Developer Preview ne rien sur Windows 10 octobre 2018 met à jour, votre système ont mis en cache obsolète configuration requise pour l’application.  Vous pouvez exécuter la commande `wsreset.exe` à partir d’une invite de commandes pour effacer le cache.

## <a name="see-also"></a>Voir aussi

* [Plus d’informations sur OpenXR](https://www.khronos.org/openxr/)
* [Spécification de OpenXR provisoires 0,90](https://www.khronos.org/registry/OpenXR/specs/0.90/html/xrspec.html)
* [Référence de l’API OpenXR provisoires 0,90](https://www.khronos.org/registry/OpenXR/specs/0.90/man/html/)
* [En-têtes de OpenXR provisoires 0,90](https://github.com/KhronosGroup/OpenXR-Docs/tree/master/include/openxr)
* [Guide de référence rapide OpenXR provisoires 0,90](https://www.khronos.org/registry/OpenXR/specs/0.90/refguide/OpenXR-0.90-web.pdf)
