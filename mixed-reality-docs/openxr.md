---
title: OpenXR
description: Générez un moteur à l’aide de la norme de l’API OpenXR portable et déployez-le sur des casques Windows mixtes et des casques HoloLens 2.
author: thetuvix
ms.author: alexturn
ms.date: 7/29/2019
ms.topic: article
keywords: OpenXR, Khronos, BasicXRApp, réalité mixte OpenXR portail des développeurs, DirectX, natif, moteur personnalisé d’application native, intergiciel
ms.openlocfilehash: 057d01527163f2ffcfe10d2e105592f07ff9e9e2
ms.sourcegitcommit: 23e172664c2ee1220fe3b4468c104b37ef3ceda9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2019
ms.locfileid: "68601598"
---
# <a name="openxr"></a>OpenXR

OpenXR est une norme d’API libre de redevance de [Khronos](https://www.khronos.org/) qui fournit aux moteurs un accès natif à un large éventail d’appareils de nombreux fournisseurs qui s’étendent sur le spectre de la [réalité mixte](mixed-reality.md).

Vous pouvez développer à l’aide de OpenXR sur un casque de l’architecture HoloLens 2 ou Windows Mixed Reality sur le bureau.  Si vous n’avez pas accès à un casque, vous pouvez utiliser l’émulateur HoloLens 2 ou Windows Mixed Reality Simulator à la place.

## <a name="why-openxr"></a>Pourquoi OpenXR?

Avec OpenXR, vous pouvez créer des moteurs qui ciblent les deux appareils holographiques (tels que HoloLens 2) qui placent le contenu numérique dans le monde réel comme s’il existait vraiment, ainsi que des appareils immersifs (tels que des casques Windows mixtes de réalité pour ordinateurs de bureau) qui masquent les et remplacez-le par un environnement numérique.  OpenXR vous permet d’écrire du code une fois qui est ensuite portable sur une large gamme de plateformes matérielles.

L’API OpenXR utilise un chargeur qui connecte votre application directement à la prise en charge native de la plateforme de votre casque.  Cela offre aux utilisateurs finaux des performances maximales et une latence minimale, qu’ils utilisent un casque Windows Mixed Reality ou tout autre casque.

## <a name="what-is-openxr"></a>Qu’est-ce que OpenXR?

L’API Core OpenXR 1,0 fournit les fonctionnalités de base dont vous aurez besoin pour créer un moteur qui peut cibler des appareils holographiques comme HoloLens 2 et des appareils immersifs tels que les casques de la réalité mixte Windows:
* Systèmes et sessions
* Espaces de référence (vue, local, intermédiaire)
* Afficher les configurations (mono, stéréo)
* Chaînes d’échange + minutage des frames
* Couches de composition
* Entrée et haptique
* API Graphics + intégration de plateforme

Pour en savoir plus sur l’API OpenXR, consultez la [spécification OpenXR 1,0](https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html) et informations de référence sur l' [API OpenXR 1,0](https://www.khronos.org/registry/OpenXR/specs/1.0/man/html/).  Pour plus d’informations, consultez la [page Khronos OpenXR](https://www.khronos.org/openxr/).

Pour cibler l’ensemble complet des fonctionnalités de HoloLens 2, vous utiliserez également des extensions OpenXR spécifiques à un fournisseur et à un fournisseur qui activent des fonctionnalités supplémentaires au-delà du OpenXR 1,0 cœurs, telles que le suivi articulé, le suivi oculaire, le mappage spatial et les ancrages spatiaux.  Pour plus d’informations sur les extensions arrivant plus tard cette année, consultez la section de la feuille de [route](openxr.md#roadmap) ci-dessous.

Notez que OpenXR n’est pas lui-même un moteur de réalité mixte.  Au lieu de cela, OpenXR permet aux moteurs comme Unity et Unreal d’écrire du code portable une seule fois qui peut ensuite accéder aux fonctionnalités natives de la plateforme de l’appareil holographique ou immersif de l’utilisateur, quel que soit le fournisseur qui a créé cette plateforme.

## <a name="getting-started-with-openxr-for-hololens-2"></a>Prise en main de OpenXR pour HoloLens 2

Pour commencer à développer des applications OpenXR pour HoloLens 2:

1. Configurez un HoloLens 2 ou suivez les instructions pour [installer l’émulateur hololens 2](using-the-hololens-emulator.md).
1. Lancez l’application du Windows Store à partir de l’appareil ou de l’émulateur et assurez-vous que toutes les applications sont mises à jour.  Cela permet de s’assurer que le runtime OpenXR sur votre HoloLens est mis à jour vers OpenXR 1,0.  Si vous utilisez l’émulateur, vous souhaiterez consulter les [instructions d’entrée](using-the-hololens-emulator.md#basic-emulator-input) de l’émulateur pour vous aider à utiliser l’application du Windows Store dans l’émulateur.

## <a name="getting-started-with-openxr-for-windows-mixed-reality-headsets"></a>Prise en main de OpenXR pour les casques Windows Mixed Reality

Pour commencer à développer des applications OpenXR pour des casques Windows mixtes immersifs:

1. Assurez-vous que vous exécutez la mise à jour Windows 10 2019 (1903), qui est la configuration minimale requise pour que les utilisateurs finaux Windows Mixed realisation exécutent des applications OpenXR.  Si vous utilisez une version antérieure de Windows 10, vous pouvez effectuer la mise à niveau vers la mise à jour 2019 de mai à l’aide de l' [Assistant Mise à jour de Windows 10](https://www.microsoft.com/en-us/software-download/windows10).  Si vous n’êtes pas en mesure de mettre à jour votre PC, il est également possible de [développer votre application OpenXR à l’aide de la mise à jour 2018 (1809) de Windows 10 octobre](openxr.md#developing-on-windows-10-october-2018-update), bien que vous puissiez constater une baisse des performances ou d’autres problèmes.
1. Configurez un casque Windows Mixed Reality ou suivez les instructions pour [activer le simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md).
1. Installez l' [application du portail des développeurs OpenXR de la réalité mixte](https://www.microsoft.com/store/productId/9n5cvvl23qbt).  L’installation de cette application installera automatiquement le runtime OpenXR de la réalité mixte.  Une fois le runtime OpenXR installé, le Microsoft Store garde le runtime à jour.
1. Exécutez l’application portail de développement OpenXR en réalité mixte à partir du menu Démarrer et suivez les instructions pour rendre le runtime actif.

![Application du portail des développeurs OpenXR de la réalité mixte](images/mixed-reality-openxr-developer-portal.png)

> [!NOTE]
> Le runtime OpenXR de la réalité mixte sera bientôt disponible pour tous les utilisateurs finaux Windows Mixed Reality via l’application de portail de réalité mixte.

## <a name="building-a-sample-openxr-app"></a>Création d’un exemple d’application OpenXR

Le projet [BasicXrApp](https://github.com/Microsoft/OpenXR-SDK-VisualStudio/tree/master/samples/BasicXrApp) illustre un exemple OpenXR simple avec deux fichiers projet Visual Studio, un pour une application de bureau Win32 et un pour une application UWP 2 UWP.  Étant donné que la solution contient un projet UWP HoloLens, vous avez besoin de la [charge de travail de développement plateforme Windows universelle](install-the-tools.md#installation-checklist) installée dans Visual Studio pour l’ouvrir entièrement.

Notez que, bien que les fichiers de projet Win32 et UWP soient distincts en raison des différences d’empaquetage et de déploiement, le code de l’application à l’intérieur de chaque projet est de 100% le même!

## <a name="roadmap"></a>Feuille de route

La spécification OpenXR définit un mécanisme d’extension qui permet aux implémenteurs de runtime d’exposer des fonctionnalités supplémentaires au-delà des [fonctionnalités](openxr.md#what-is-openxr) de base définies dans la [spécification 1,0 de base OpenXR](https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html).

Il existe trois types d’extensions OpenXR:
* **Extensions de fournisseur (par exemple, MSFT):** Active l’innovation par fournisseur dans les fonctionnalités matérielles ou logicielles.  N’importe quel fournisseur de Runtime peut introduire et livrer une extension de fournisseur à tout moment.
* **Extensions EXT:** Extensions inter-fournisseurs que plusieurs entreprises définissent et implémentent.  Les groupes de sociétés intéressées peuvent introduire des extensions EXT à tout moment.
* **Extensions KHR:** Extensions Khronos officielles ratifiées dans le cadre d’une version de base spec.  Les extensions KHR sont couvertes par la même licence que la spécification principale elle-même.

À la fin de l’année, le runtime OpenXR en réalité mixte prendra en charge un ensemble d’extensions MSFT et EXT qui apportent l’ensemble complet des fonctionnalités HoloLens 2 aux applications OpenXR:
* [Espace de référence non lié (expériences à l’échelle mondiale)](coordinate-systems.md#building-a-world-scale-experience)
* [Ancres spatiales + stockage](spatial-anchors.md)
* [Articulation manuelle + maille](hands-and-tools.md)
* [Suivre du regard](eye-tracking.md)
* [Configurations d’affichage secondaire (capture de réalité mixte)](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in)
* [Mappage spatial](spatial-mapping.md)
* Interopérabilité avec les API SDK Windows

Bien que certaines de ces extensions puissent démarrer en tant qu’extensions MSFT spécifiques au fournisseur, Microsoft et d’autres fournisseurs de Runtime OpenXR travaillent ensemble pour concevoir des extensions EXT ou KHR inter-fournisseurs pour la plupart de ces fonctionnalités.  Cela permet au code que vous écrivez pour que ces fonctionnalités soient portables entre les fournisseurs de Runtime, tout comme avec la spécification principale.

## <a name="troubleshooting"></a>Résolution des problèmes

Voici quelques conseils de dépannage pour le runtime OpenXR de la réalité mixte.  Si vous avez d’autres questions sur la [spécification OpenXR 1,0](https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html), visitez les [Forums Khronos OpenXR](https://community.khronos.org/c/openxr) ou la [marge #openxr canal](https://khr.io/slack).

### <a name="developing-on-windows-10-october-2018-update"></a>Mise à jour du développement sur Windows 10 octobre 2018

Si vous n’êtes pas en mesure de [mettre à niveau votre PC de développement vers la mise à jour 2019 de mai](https://www.microsoft.com/en-us/software-download/windows10), vous pouvez configurer votre PC Windows 10 octobre 2018 update (1809) pour le développement en suivant une étape supplémentaire:

1. Suivez les étapes ci-dessus pour commencer à utiliser OpenXR sur votre ordinateur de bureau.
1. Pour définir le runtime OpenXR en réalité mixte comme Runtime OpenXR actif de votre système, installez le [Pack de compatibilité de développeur OpenXR de la réalité mixte](https://aka.ms/openxr-compat).

> [!NOTE]
> Bien que la mise à jour 2018 (1809) de Windows 10 octobre puisse être utilisée lors du développement de vos applications OpenXR, la mise à jour Windows 10 mai 2019 (1903) est la configuration minimale requise pour que les utilisateurs finaux utilisent OpenXR avec Windows Mixed Reality.  Vous pouvez constater une baisse des performances ou d’autres problèmes lors de l’exécution de votre application OpenXR sur la mise à jour d’octobre 2018.  Il est fortement recommandé de mettre à niveau votre PC de développement vers la mise à jour 2019 de Windows 10 (1903).

### <a name="openxr-app-not-starting-windows-mixed-reality"></a>Application OpenXR ne démarrant pas Windows Mixed Reality

Si votre application OpenXR ne démarre pas Windows Mixed Reality quand vous l’exécutez, le runtime OpenXR de la réalité mixte ne peut pas être défini en tant que Runtime actif.  Veillez à exécuter l’application portail de développement OpenXR en réalité mixte et suivez les instructions pour activer le Runtime.

### <a name="mixed-reality-openxr-developer-portal-app-cannot-be-installed"></a>Impossible d’installer l’application du portail des développeurs OpenXR de la réalité mixte 

Assurez-vous que vous exécutez au moins la mise à jour 2018 de Windows 10 octobre (1809).  Si vous utilisez une version antérieure de Windows 10, vous pouvez effectuer la mise à niveau vers la mise à jour 2019 (1903) à l’aide de l' [Assistant Mise à jour de Windows 10](https://www.microsoft.com/en-us/software-download/windows10).

Si le bouton installer de l’application OpenXR Developer de la réalité mixte ne fait rien sur la mise à jour 2018 d’octobre de Windows 10, votre système peut avoir mis en cache une configuration système périmée pour l’application.  Vous pouvez exécuter la commande `wsreset.exe` à partir d’une invite de commandes pour effacer le cache.

## <a name="see-also"></a>Voir aussi

* [Plus d’informations sur OpenXR](https://www.khronos.org/openxr/)
* [Spécification OpenXR 1,0](https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html)
* [Informations de référence sur l’API OpenXR 1,0](https://www.khronos.org/registry/OpenXR/specs/1.0/man/html/)
* [Guide de référence rapide de OpenXR 1,0](https://www.khronos.org/registry/OpenXR/specs/1.0/refguide/OpenXR-1.0-web.pdf)
