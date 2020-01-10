---
title: Windows Mixed Reality et le nouveau Microsoft Edge
description: Comment contribuer à la documentation de Windows Mixed Reality.
author: mattzmsft
ms.author: mazeller
ms.date: 01/07/2020
ms.topic: article
keywords: Edge, nouveau, immersion sur le Web, Microsoft Edge, navigateur, VR
ms.openlocfilehash: cb0f96069ffaa8f7d40b64bae55ab2749f5f02c6
ms.sourcegitcommit: 6844930427b658ae31f642c395cd8a3b3cdbf857
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75727046"
---
# <a name="windows-mixed-reality-and-the-new-microsoft-edge"></a>Windows Mixed Reality et le nouveau Microsoft Edge

Comme vous l’avez peut-être entendu, le [nouveau Microsoft Edge sera bientôt disponible](https://blogs.windows.com/windowsexperience/2019/11/04/introducing-the-new-microsoft-edge-and-bing/)! Avec la disponibilité générale ciblée pour le 15 janvier 2020, nous souhaitons permettre aux clients du casque Windows Mixed realer VR de savoir ce qu’il faut attendre du nouveau Microsoft Edge et vous informer des mises à jour en attente qui amélioreront votre expérience de navigation sur le Web dans Windows Mixed Donner.

## <a name="introducing-the-new-microsoft-edge"></a>Présentation du nouveau Microsoft Edge

Le nouveau Microsoft Edge [adopte le projet open source de chrome](https://blogs.windows.com/windowsexperience/2018/12/06/microsoft-edge-making-the-web-better-through-more-open-source-collaboration/) sur le Bureau pour créer une meilleure compatibilité Web pour les clients et réduire la fragmentation du Web pour tous les développeurs Web. Il prend également en charge WebXR au lancement, la nouvelle norme pour créer des expériences Web immersifs pour les casques VR, à la place de WebVR.

## <a name="getting-ready-for-the-new-microsoft-edge"></a>Préparation au nouveau Microsoft Edge

Les clients du casque Windows Mixed Reality VR qui veulent utiliser le nouveau Microsoft Edge dans la réalité mixte doivent **effectuer une mise à niveau vers Windows 10 Version 1903 ou ultérieure pour la prise en charge native des applications Win32 (comme le nouveau Microsoft Edge)** dans la page d’hébergement de la réalité mixte. Vérifiez Windows Update ou [Installez manuellement la dernière version de Windows 10](https://www.microsoft.com/en-us/software-download/windows10).

Pour une expérience Microsoft Edge optimale dans la réalité mixte, nous vous recommandons également d’attendre des **optimisations clés de la réalité de Windows mixte pour le nouveau Microsoft Edge arrivant avec la mise à jour Cumulative 2020-01 pour Windows 10 Version 1903 (ou ultérieure)** , qui doit être disponible en Windows Update à la fin du janvier.

>[!IMPORTANT]
>Si vous choisissez de télécharger le nouveau Microsoft Edge avant de procéder à ces mises à jour, il y aura des problèmes connus avec son comportement dans Windows Mixed Reality (que vous pouvez voir ci-dessous).

## <a name="known-issues"></a>Problèmes connus

### <a name="known-issues-resolved-by-the-2020-01-cumulative-update-for-windows-10-version-1903-or-later"></a>Problèmes connus résolus par la mise à jour cumulative 2020-01 pour Windows 10 version 1903 (ou version ultérieure)

- Le lancement d’une application Win32, y compris le nouveau Microsoft Edge, provoque un blocage rapide de l’affichage du casque.
- La vignette Microsoft Edge disparaît du menu Démarrer Windows Mixed Reality (vous pouvez la trouver dans le dossier « applications classiques »).
- Les fenêtres de la version précédente de Microsoft Edge sont toujours placées autour de la réalité mixte, mais elles ne peuvent pas être utilisées. Tentative d’activation de l’Edge de lancement Windows à l’intérieur de l’application de bureau.
- La sélection d’un lien hypertexte dans la page d’hébergement de la réalité mixte lance un navigateur Web sur le bureau et non sur la réalité mixte.
- L’application WebVR Showcase est présente dans la réalité mixte, en dépit du fait que WebVR n’est plus pris en charge.
- Améliorations générales apportées au lancement et aux visuels du clavier.

### <a name="additional-known-issues"></a>Autres problèmes connus

-   Les sites Web ouverts dans Windows Mixed Reality sont perdus lorsque le portail de réalité mixte se ferme, bien que les fenêtres Microsoft Edge restent là où elles ont été placées dans la page d’hébergement de la réalité mixte.
-   L’audio des fenêtres Microsoft Edge n’est pas spatial.
-   L’ouverture d’une vidéo 360 à partir de YouTube dans Windows Mixed Reality peut entraîner la déformation de la vidéo dans le casque. L’actualisation de la page de la vidéo YouTube et le redémarrage de la vidéo 360 doivent résoudre le problème.
-   Pendant les sessions Windows Mixed Reality, les moniteurs virtuels s’affichent sous la forme de moniteurs physiques génériques dans les paramètres > système > écran.



