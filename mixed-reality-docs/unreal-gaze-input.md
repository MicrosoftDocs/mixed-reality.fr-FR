---
title: Entrée en pointage en regard
description: Explique comment utiliser l’entrée en regard dans le temps
author: AndreyChistyakov
ms.author: anchisty
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, HoloLens, suivi oculaire
ms.openlocfilehash: 7387bb3f25cdbdfac32f508c173fbd098f844e84
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82835621"
---
# <a name="gaze-input"></a>Entrée en regard

Le plug-in Windows Mixed Reality ne fournit pas de fonctions spéciales pour l’entrée en regard. Tout fonctionne par le biais de l’API inréelles standard.

[API de pointage de tête](https://docs.unrealengine.com/en-US/BlueprintAPI/Input/HeadMountedDisplay/index.html)

## <a name="eye-tracking"></a>Eye-tracking

Pour utiliser l’API de suivi oculaire, les développeurs doivent activer la fonctionnalité « entrée de regard » dans leurs paramètres de projet HoloLens. Lorsque l’application démarre, l’utilisateur voit l’invite de consentement suivante

![Autorisations d’entrée oculaire](images/unreal/eye-input-permissions.png)
 
Si l’utilisateur donne son autorisation, l’application obtient une entrée en regard de l’œil. 

L’API de suivi des yeux inréel est documentée [ici](https://docs.unrealengine.com/en-US/BlueprintAPI/EyeTracking/index.html)

Les détails techniques du suivi oculaire sont [ici](eye-tracking.md)

Notez que, spécifiquement pour le suivi des yeux HoloLens non réels, a un seul rayon de regard pour les deux yeux. HoloLens ne fournit pas de suivi oculaire stéréoscopique.
