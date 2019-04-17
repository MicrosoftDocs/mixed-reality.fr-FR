---
title: OpenXR
description: Essayer l’API OpenXR 0,90 provisoire avec l’aperçu pour développeurs OpenXR réalité mixte.
author: thetuvix
ms.author: alexturn
ms.date: 3/18/2019
ms.topic: article
keywords: Réalité mixte OpenXR Developer Preview
ms.openlocfilehash: 0d8debf5c12cb88aaba402145c6a597f761491ee
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596353"
---
# <a name="openxr"></a>OpenXR

OpenXR est une norme ouverte libres de [Khronos](https://www.khronos.org/) qui fournit l’accès natif à un large éventail d’appareils à partir de nombreux fournisseurs qui couvrent la [spectre de réalité mixte](mixed-reality.md).

Avec OpenXR, vous pouvez créer des applications qui ciblent les appareils HOLOGRAPHIQUE (par exemple, HoloLens, 2) qui placent un contenu numérique dans le monde réel comme s’il s’agissait vraiment ce, ainsi qu’immersives périphériques (tels que les casques de réalité mixte Windows pour les ordinateurs de bureau) qui masquent la monde physique et le remplacer par une expérience numérique.  OpenXR vous permet d’écrire du code une fois que c’est portable sur un large éventail de plateformes matérielles.

La norme OpenXR est en cours d’une phase provisoire, avec une spécification OpenXR 0,90 initiale publiée pour envoyer des commentaires.  Pour plus d’informations sur OpenXR, y compris l’accès à la [spec 0,90 provisoire](https://www.khronos.org/registry/OpenXR/specs/0.90/html/xrspec.html) et [en-têtes](https://github.com/KhronosGroup/OpenXR-Docs/tree/master/include/openxr), consultez le [Khronos OpenXR page](https://www.khronos.org/openxr/).

## <a name="setting-up-the-mixed-reality-openxr-developer-preview"></a>Configuration de l’aperçu pour développeurs OpenXR réalité mixte

Vous pouvez essayer l’API OpenXR 0,90 provisoire dès aujourd'hui à l’aide de l’aperçu pour développeurs OpenXR réalité mixte.  Ce runtime anticipé permet aux applications ciblant l’API OpenXR 0,90 pour cible Windows Mixed Reality des casques IMMERSIFS sur le bureau.  Si vous n’avez pas accès à un casque, vous pouvez utiliser le simulateur de réalité mixte Windows à la place.

Prise en main l’aperçu pour développeurs OpenXR réalité mixte :

1. Vérifiez que vous exécutez au moins les fenêtres de mise à jour 10 octobre 2018.  Si vous êtes sur une version antérieure de Windows 10, vous pouvez mettre à niveau vers l’octobre 2018 mettre à jour à l’aide de la [l’Assistant Mise à jour de Windows 10](https://www.microsoft.com/en-us/software-download/windows10).  Si vous vous sentez aventureux, vous pouvez installer un [build de Windows 10 Insider Preview](https://insider.windows.com).
1. Configurer un casque Windows Mixed Reality ou suivez les instructions pour [activer le simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md).
1. Installer le [Mixed Reality OpenXR Developer Preview, application](https://www.microsoft.com/store/productId/9n5cvvl23qbt).  Cette application vous permet de configurer avec la version préliminaire du runtime de OpenXR sur Windows mise à jour 10 octobre 2018 ou version ultérieure.  Après avoir installé cette application, le Windows Store conserve le runtime à jour.
1. Exécutez l’application mixte réalité OpenXR Developer Preview dans le menu Démarrer et suivez les instructions pour rendre le runtime actif.  Bientôt, cette application vous permet d’Explorer les autres informations de débogage OpenXR également.

![Réalité mixte OpenXR Developer Preview, application](images/mixed-reality-openxr-developer-preview.png)

## <a name="support-for-windows-10-october-2018-update"></a>Prise en charge de la mise à jour de Windows 10 octobre 2018

Pour commencer avec l’aperçu pour développeurs OpenXR réalité mixte sur Windows 10 octobre 2018 mettre à jour (la version actuelle de Windows), vous devez suivre quelques étapes supplémentaires :

1. Suivez les étapes ci-dessus pour installer l’aperçu pour développeurs OpenXR réalité mixte.
1. Pour définir l’aperçu pour développeurs OpenXR réalité mixte comme runtime de OpenXR actif de votre système, vous devez installer le [Pack de compatibilité mixte réalité OpenXR Developer Preview](https://aka.ms/openxr-compat).

## <a name="building-a-test-openxr-app"></a>Création d’un test OpenXR application

Le [hello_xr](https://github.com/KhronosGroup/OpenXR-SDK/tree/master/src/tests/hello_xr) OpenXR test application illustre l’utilisation de différentes parties de l’API.  Vous pouvez suivre ces [instructions de génération](https://github.com/KhronosGroup/OpenXR-SDK/blob/master/BUILDING.md), ce qui génère l’application de test et les en-têtes OpenXR eux-mêmes.

## <a name="feedback"></a>Commentaires

Pour envoyer des commentaires sur le [spécification de OpenXR provisoires 0,90](https://www.khronos.org/registry/OpenXR/specs/0.90/html/xrspec.html), visitez le [Khronos OpenXR Forums](https://community.khronos.org/c/openxr), [les canaux Slack #openxr](https://khr.io/slack) et le [spec suivi des problèmes](https://github.com/KhronosGroup/OpenXR-Docs/issues).

## <a name="troubleshooting"></a>Résolution des problèmes

Voici quelques conseils de dépannage pour l’aperçu pour développeurs OpenXR réalité mixte.  Si vous rencontrez d’autres problèmes, visitez le [Khronos OpenXR Forums](https://community.khronos.org/c/openxr) ou [les canaux Slack #openxr](https://khr.io/slack).

### <a name="openxr-app-not-starting-windows-mixed-reality"></a>Application OpenXR ne démarre ne pas Windows Mixed Reality

Si votre application OpenXR ne démarre pas Windows Mixed Reality lors de son exécution, l’aperçu pour développeurs OpenXR réalité mixte ne peuvent pas être définie en tant que le runtime actif.  Veillez à exécuter l’application mixte réalité OpenXR Developer Preview et suivez les instructions pour rendre le runtime actif.

### <a name="mixed-reality-openxr-developer-preview-app-cannot-be-installed"></a>Application de réalité OpenXR Developer Preview mixte ne peut pas être installée 

Vérifiez que vous exécutez au moins les fenêtres de mise à jour 10 octobre 2018.  Si vous êtes sur une version antérieure de Windows 10, vous pouvez mettre à niveau vers l’octobre 2018 mettre à jour à l’aide de la [l’Assistant Mise à jour de Windows 10](https://www.microsoft.com/en-us/software-download/windows10).

Si l’installation de bouton sur l’application mixte réalité OpenXR Developer Preview ne rien sur Windows 10 octobre 2018 met à jour, votre système ont mis en cache obsolète configuration requise pour l’application.  Vous pouvez exécuter la commande `wsreset.exe` à partir d’une invite de commandes pour effacer le cache.

## <a name="see-also"></a>Voir aussi

* [Plus d’informations sur OpenXR](https://www.khronos.org/openxr/)
* [Spécification de OpenXR provisoires 0,90](https://www.khronos.org/registry/OpenXR/specs/0.90/html/xrspec.html)
* [Référence de l’API OpenXR provisoires 0,90](https://www.khronos.org/registry/OpenXR/specs/0.90/man/html/)
* [En-têtes de OpenXR provisoires 0,90](https://github.com/KhronosGroup/OpenXR-Docs/tree/master/include/openxr)
