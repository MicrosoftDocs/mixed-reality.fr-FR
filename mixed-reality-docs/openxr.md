---
title: OpenXR
description: Générez un moteur à l’aide de la norme de l’API OpenXR portable et déployez-le sur des casques Windows mixtes et des casques HoloLens 2.
author: thetuvix
ms.author: alexturn
ms.date: 7/29/2019
ms.topic: article
keywords: OpenXR, Khronos, BasicXRApp, réalité mixte OpenXR portail des développeurs, DirectX, natif, moteur personnalisé d’application native, intergiciel
ms.openlocfilehash: cf8795e6fed7db9fd0743d0902ce1585d56fa5e0
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438137"
---
# <a name="openxr"></a>OpenXR

OpenXR est une norme d’API libre de redevance de <a href="https://www.khronos.org/" target="_blank">Khronos</a> qui fournit aux moteurs un accès natif à un large éventail d’appareils de nombreux fournisseurs qui s’étendent sur le spectre de la [réalité mixte](mixed-reality.md).

Vous pouvez développer à l’aide de OpenXR sur un casque de l’architecture HoloLens 2 ou Windows Mixed Reality sur le bureau.  Si vous n’avez pas accès à un casque, vous pouvez utiliser l’émulateur HoloLens 2 ou Windows Mixed Reality Simulator à la place.

## <a name="why-openxr"></a>Pourquoi OpenXR ?

Avec OpenXR, vous pouvez créer des moteurs qui ciblent les deux appareils holographiques (tels que HoloLens 2) qui placent le contenu numérique dans le monde réel comme s’il existait vraiment, ainsi que des appareils immersifs (tels que des casques Windows mixtes de réalité pour ordinateurs de bureau) qui masquent les et remplacez-le par un environnement numérique.  OpenXR vous permet d’écrire du code une fois qui est ensuite portable sur une large gamme de plateformes matérielles.

L’API OpenXR utilise un chargeur qui connecte votre application directement à la prise en charge native de la plateforme de votre casque.  Cela offre aux utilisateurs finaux des performances maximales et une latence minimale, qu’ils utilisent un casque Windows Mixed Reality ou tout autre casque.

## <a name="what-is-openxr"></a>Qu’est-ce que OpenXR ?

L’API Core OpenXR 1,0 fournit les fonctionnalités de base dont vous aurez besoin pour créer un moteur qui peut cibler des appareils holographiques comme HoloLens 2 et des appareils immersifs tels que les casques de la réalité mixte Windows :
* Systèmes et sessions
* Espaces de référence (vue, local, intermédiaire)
* Afficher les configurations (mono, stéréo)
* Chaînes d’échange + minutage des frames
* Couches de composition
* Entrée et haptique
* API Graphics + intégration de plateforme

Pour en savoir plus sur l’API OpenXR, consultez la <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">spécification</a>OpenXR 1,0, informations de <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/man/html/openxr.html" target="_blank">référence</a> sur les API et <a href="https://www.khronos.org/files/openxr-10-reference-guide.pdf" target="_blank">Guide de référence rapide</a>.  Pour plus d’informations, consultez la <a href="https://www.khronos.org/openxr/" target="_blank">page Khronos OpenXR</a>.

Pour cibler l’ensemble complet des fonctionnalités de HoloLens 2, vous utiliserez également des extensions OpenXR spécifiques à un fournisseur et à un fournisseur qui activent des fonctionnalités supplémentaires au-delà du OpenXR 1,0 cœurs, telles que le suivi articulé, le suivi oculaire, le mappage spatial et les ancrages spatiaux.  Pour plus d’informations sur les extensions arrivant plus tard cette année, consultez la section de la feuille de [route](openxr.md#roadmap) ci-dessous.

Notez que OpenXR n’est pas lui-même un moteur de réalité mixte.  Au lieu de cela, OpenXR permet aux moteurs comme Unity et Unreal d’écrire du code portable une seule fois qui peut ensuite accéder aux fonctionnalités natives de la plateforme de l’appareil holographique ou immersif de l’utilisateur, quel que soit le fournisseur qui a créé cette plateforme.

## <a name="getting-started-with-openxr-for-hololens-2"></a>Prise en main de OpenXR pour HoloLens 2

Pour commencer à développer des applications OpenXR pour HoloLens 2 :

1. Configurez un HoloLens 2 ou suivez les instructions pour [installer l’émulateur hololens 2](using-the-hololens-emulator.md).
1. Lancez l’application du Windows Store à partir de l’appareil ou de l’émulateur et assurez-vous que toutes les applications sont mises à jour.  Cela permet de s’assurer que le runtime OpenXR sur votre HoloLens est mis à jour vers OpenXR 1,0.  Si vous utilisez l’émulateur, vous souhaiterez consulter les [instructions d’entrée](using-the-hololens-emulator.md#basic-emulator-input) de l’émulateur pour vous aider à utiliser l’application du Windows Store dans l’émulateur.

## <a name="getting-started-with-openxr-for-windows-mixed-reality-headsets"></a>Prise en main de OpenXR pour les casques Windows Mixed Reality

Pour commencer à développer des applications OpenXR pour des casques Windows mixtes immersifs :

1. Assurez-vous que vous exécutez la mise à jour Windows 10 2019 (1903), qui est la configuration minimale requise pour que les utilisateurs finaux Windows Mixed realisation exécutent des applications OpenXR.  Si vous utilisez une version antérieure de Windows 10, vous pouvez effectuer la mise à niveau vers la mise à jour 2019 de mai à l’aide de l' <a href="https://www.microsoft.com//software-download/windows10" target="_blank">Assistant Mise à jour de Windows 10</a>.  Si vous n’êtes pas en mesure de mettre à jour votre PC, il est également possible de [développer votre application OpenXR à l’aide de la mise à jour 2018 (1809) de Windows 10 octobre](openxr.md#developing-on-windows-10-october-2018-update), bien que vous puissiez constater une baisse des performances ou d’autres problèmes.
2. Configurez un casque Windows Mixed Reality ou suivez les instructions pour [activer le simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md).  Après la configuration de Windows Mixed Reality, le portail de réalité mixte installe automatiquement le runtime OpenXR Windows Mixed Reality.  Le Microsoft Store garde alors le runtime à jour.
3. Rendez le runtime OpenXR Windows Mixed Reality actif en lançant le portail de réalité mixte à partir du menu Démarrer, en cliquant sur le bouton... dans l’angle inférieur gauche, puis en sélectionnant « Configurer OpenXR ».<br>
![la configuration de OpenXR dans le portail de réalité mixte](images/mixed-reality-portal-set-up-openxr.png)

Si vous devez faire en sorte que le runtime OpenXR Windows Mixed Reality soit à nouveau actif, répétez l’étape 3.

> [!NOTE]
> Le runtime Windows Mixed Reality OpenXR sera bientôt configuré automatiquement pour tous les utilisateurs finaux Windows Mixed Reality.

## <a name="getting-the-mixed-reality-openxr-developer-portal"></a>Obtention du portail des développeurs OpenXR de la réalité mixte

Pour tester le runtime OpenXR Windows Mixed Reality, vous pouvez installer l' <a href="https://www.microsoft.com/store/productId/9n5cvvl23qbt" target="_blank">application [Mixed Reality OpenXR Developer Portal</a>.  Cette application fournit une scène de démonstration qui exerce diverses fonctionnalités de OpenXR, ainsi qu’une page d’État du système qui fournit des informations clés sur le runtime actif et le casque actuel.

![Application du portail des développeurs OpenXR de la réalité mixte](images/mixed-reality-openxr-developer-portal.png)

## <a name="building-a-sample-openxr-app"></a>Création d’un exemple d’application OpenXR

Le projet <a href="https://github.com/Microsoft/OpenXR-SDK-VisualStudio/tree/master/samples/BasicXrApp" target="_blank">BasicXrApp</a> illustre un exemple OpenXR simple avec deux fichiers projet Visual Studio, un pour une application de bureau Win32 et un pour une application UWP 2 UWP.  Étant donné que la solution contient un projet UWP HoloLens, vous avez besoin de la [charge de travail de développement plateforme Windows universelle](install-the-tools.md#installation-checklist) installée dans Visual Studio pour l’ouvrir entièrement.

Notez que, bien que les fichiers de projet Win32 et UWP soient distincts en raison des différences d’empaquetage et de déploiement, le code de l’application à l’intérieur de chaque projet est de 100% le même !

## <a name="roadmap"></a>Feuille de route

La spécification OpenXR définit un mécanisme d’extension qui permet aux implémenteurs de runtime d’exposer des fonctionnalités supplémentaires au-delà des [fonctionnalités](openxr.md#what-is-openxr) de base définies dans la <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">spécification 1,0 de base OpenXR</a>.

Il existe trois types d’extensions OpenXR :
* **Extensions de fournisseur (par exemple, MSFT) :** Active l’innovation par fournisseur dans les fonctionnalités matérielles ou logicielles.  N’importe quel fournisseur de Runtime peut introduire et livrer une extension de fournisseur à tout moment.
* **Extensions ext :** Extensions inter-fournisseurs que plusieurs entreprises définissent et implémentent.  Les groupes de sociétés intéressées peuvent introduire des extensions EXT à tout moment.
* **Extensions KHR :** Extensions Khronos officielles ratifiées dans le cadre d’une version de base spec.  Les extensions KHR sont couvertes par la même licence que la spécification principale elle-même.

À la fin de l’année, le runtime OpenXR Windows Mixed Reality prendra en charge un ensemble d’extensions MSFT et EXT qui apportent l’ensemble complet des fonctionnalités HoloLens 2 aux applications OpenXR :
* [Espace de référence non lié (expériences à l’échelle mondiale)](coordinate-systems.md#building-a-world-scale-experience)
* [Ancres spatiales + stockage](spatial-anchors.md)
* [Articulation manuelle + maille](hands-and-tools.md)
* [Suivre du regard](eye-tracking.md)
* [Configurations d’affichage secondaire (capture de réalité mixte)](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in)
* [Mappage spatial](spatial-mapping.md)
* Interopérabilité avec les API SDK Windows

Bien que certaines de ces extensions puissent démarrer en tant qu’extensions MSFT spécifiques au fournisseur, Microsoft et d’autres fournisseurs de Runtime OpenXR travaillent ensemble pour concevoir des extensions EXT ou KHR inter-fournisseurs pour la plupart de ces fonctionnalités.  Cela permet au code que vous écrivez pour que ces fonctionnalités soient portables entre les fournisseurs de Runtime, tout comme avec la spécification principale.

## <a name="troubleshooting"></a>Dépannage

Voici quelques conseils de dépannage pour le runtime OpenXR Windows Mixed Reality.  Si vous avez d’autres questions sur la <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">spécification OpenXR 1,0</a>, visitez les <a href="https://community.khronos.org/c/openxr" target="_blank">Forums Khronos OpenXR</a> ou la <a href="https://khr.io/slack" target="_blank">marge #openxr canal</a>.

### <a name="developing-on-windows-10-october-2018-update"></a>Mise à jour du développement sur Windows 10 octobre 2018

Si vous n’êtes pas en mesure de [mettre à niveau votre PC de développement vers la mise à jour 2019 de mai](https://www.microsoft.com//software-download/windows10), vous pouvez configurer votre PC Windows 10 octobre 2018 update (1809) pour le développement en suivant une étape supplémentaire :

1. Suivez les étapes ci-dessus pour commencer à utiliser OpenXR sur votre ordinateur de bureau.
1. Pour définir le runtime Windows Mixed Reality OpenXR comme le runtime OpenXR actif de votre système, installez le [Pack de compatibilité des développeurs Windows Mixed Reality OpenXR](https://aka.ms/openxr-compat).

> [!NOTE]
> Bien que la mise à jour 2018 (1809) de Windows 10 octobre puisse être utilisée lors du développement de vos applications OpenXR, la mise à jour Windows 10 mai 2019 (1903) est la configuration minimale requise pour que les utilisateurs finaux utilisent OpenXR avec Windows Mixed Reality.  Vous pouvez constater une baisse des performances ou d’autres problèmes lors de l’exécution de votre application OpenXR sur la mise à jour d’octobre 2018.  Il est fortement recommandé de mettre à niveau votre PC de développement vers la mise à jour 2019 de Windows 10 (1903).

### <a name="openxr-app-not-starting-windows-mixed-reality"></a>Application OpenXR ne démarrant pas Windows Mixed Reality

Si votre application OpenXR ne démarre pas Windows Mixed Reality quand vous l’exécutez, le runtime Windows Mixed Reality OpenXR peut ne pas être défini comme le runtime actif.  Veillez à suivre les instructions ci-dessus pour bien [Démarrer avec OpenXR pour les casques Windows Mixed Reality](#getting-started-with-openxr-for-windows-mixed-reality-headsets) pour rendre le runtime actif.

Vous pouvez également exécuter le [portail des développeurs OpenXR de la réalité mixte](#getting-the-mixed-reality-openxr-developer-portal) pour obtenir une aide supplémentaire sur l’état du runtime Windows Mixed Reality OpenXR sur votre système.

### <a name="mixed-reality-portal-not-showing-set-up-openxr-menu-item"></a>Le portail de réalité mixte n’indique pas l’élément de menu « configurer OpenXR »

Assurez-vous que vous exécutez au moins la mise à jour 2018 de Windows 10 octobre (1809).  Si vous utilisez une version antérieure de Windows 10, vous pouvez effectuer la mise à niveau vers la mise à jour 2019 (1903) à l’aide de l' [Assistant Mise à jour de Windows 10](https://www.microsoft.com//software-download/windows10).

L’élément de menu « configurer OpenXR » peut ne pas être disponible si vous disposez d’une version antérieure de l’application portail de réalité mixte.  Recherchez une [mise à jour de l’application portail de réalité mixte](https://www.microsoft.com/p/mixed-reality-portal/9ng1h8b3zc7m) pour vous assurer que vous disposez de la dernière version.

Notez que l’élément de menu « configurer OpenXR » n’apparaît pas si le runtime Windows Mixed Reality OpenXR est déjà installé et actif.  Vous pouvez installer le [portail des développeurs OpenXR de la réalité mixte](#getting-the-mixed-reality-openxr-developer-portal) pour déterminer l’état actuel du runtime OpenXR sur votre système.

## <a name="see-also"></a>Articles associés

* <a href="https://www.khronos.org/openxr/" target="_blank">Plus d’informations sur OpenXR</a>
* <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">Spécification OpenXR 1,0</a>
* <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/man/html/openxr.html" target="_blank">Informations de référence sur l’API OpenXR 1,0</a>
* <a href="https://www.khronos.org/files/openxr-10-reference-guide.pdf" target="_blank">Guide de référence rapide de OpenXR 1,0</a>
