---
title: Résolution des problèmes OpenXR
description: Résolvez les problèmes dans vos applications OpenXR.
author: thetuvix
ms.author: alexturn
ms.date: 2/28/2020
ms.topic: article
keywords: OpenXR, Khronos, BasicXRApp, DirectX, native, application native, moteur personnalisé, intergiciel, résolution des problèmes
ms.openlocfilehash: 08ca671ded7230a4ba3cfcdc640233082af51040
ms.sourcegitcommit: 9de2cb11321e6517db69e8c93459a205900a2174
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/24/2020
ms.locfileid: "80163363"
---
# <a name="openxr-troubleshooting"></a>Résolution des problèmes OpenXR

Voici quelques conseils de dépannage pour le développement d’une application OpenXR à l’aide du runtime Windows Mixed Reality OpenXR.  Si vous avez d’autres questions sur la <a href="https://www.khronos.org/registry/OpenXR/specs/1.0/html/xrspec.html" target="_blank">spécification OpenXR 1,0</a>, visitez les <a href="https://community.khronos.org/c/openxr" target="_blank">Forums Khronos OpenXR</a> ou la <a href="https://khr.io/slack" target="_blank">marge #openxr canal</a>.

>[!NOTE]
>Il existe des problèmes connus dans le runtime Windows Mixed Reality OpenXR actuel avec les applications x86.  Vous devez créer des applications Desktop OpenXR pour x64 pour le moment.

### <a name="openxr-app-not-starting-windows-mixed-reality"></a>Application OpenXR ne démarrant pas Windows Mixed Reality

Si votre application OpenXR ne démarre pas Windows Mixed Reality quand vous l’exécutez, le runtime Windows Mixed Reality OpenXR peut ne pas être défini comme le runtime actif.  Veillez à suivre les instructions ci-dessus pour bien [Démarrer avec OpenXR pour les casques Windows Mixed Reality](openxr-getting-started.md#getting-started-with-openxr-for-windows-mixed-reality-headsets) pour rendre le runtime actif.

Vous pouvez également exécuter le [portail des développeurs OpenXR Windows Mixed Reality](openxr-getting-started.md#getting-the-windows-mixed-reality-openxr-developer-portal) pour obtenir une aide supplémentaire sur l’état du runtime Windows Mixed Reality OpenXR sur votre système.

### <a name="mixed-reality-portal-not-showing-set-up-openxr-menu-item"></a>Le portail de réalité mixte n’indique pas l’élément de menu « configurer OpenXR »

Assurez-vous que vous exécutez au moins la mise à jour 2018 de Windows 10 octobre (1809).  Si vous utilisez une version antérieure de Windows 10, vous pouvez effectuer la mise à niveau vers la mise à jour 2019 (1903) à l’aide de l' [Assistant Mise à jour de Windows 10](https://www.microsoft.com//software-download/windows10).

L’élément de menu « configurer OpenXR » peut ne pas être disponible si vous disposez d’une version antérieure de l’application portail de réalité mixte.  Recherchez une [mise à jour de l’application portail de réalité mixte](https://www.microsoft.com/p/mixed-reality-portal/9ng1h8b3zc7m) pour vous assurer que vous disposez de la dernière version.

Notez que l’élément de menu « configurer OpenXR » n’apparaît pas si le runtime Windows Mixed Reality OpenXR est déjà installé et actif.  Vous pouvez installer le [portail des développeurs OpenXR Windows Mixed Reality](openxr-getting-started.md#getting-the-windows-mixed-reality-openxr-developer-portal) pour déterminer l’état actuel du runtime OpenXR sur votre système.