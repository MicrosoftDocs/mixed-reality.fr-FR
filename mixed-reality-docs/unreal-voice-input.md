---
title: Entrée vocale
description: Explique comment utiliser l’entrée vocale
author: AndreyChistyakov
ms.author: anchisty
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality, HoloLens
ms.openlocfilehash: d61a9f9d40c76c8872ff0a1b39d65f95ae88d2b7
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82835307"
---
# <a name="voice-input"></a>Entrée vocale

Pour activer la reconnaissance vocale sur HoloLens, le développeur doit activer « microphone » dans l’éditeur non réel sous paramètres du projet > fonctionnalités de la plateforme > HoloLens >. La reconnaissance vocale de l’appareil doit également être activée dans paramètres > confidentialité > vocale et utilisez la langue anglaise.

![Paramètres de reconnaissance vocale Windows](images/unreal/speech-recognition-settings.png)

Il est recommandé d’activer la reconnaissance vocale en ligne pour la meilleure qualité possible du service. Vous trouverez des détails techniques sur la reconnaissance vocale sur HoloLens [ici](voice-input.md) .

L’utilisateur verra alors s’afficher une boîte de dialogue sur l’activation du microphone lors du premier démarrage de l’application. Si un utilisateur sélectionne Oui, l’application commence à obtenir une entrée vocale.

L’entrée vocale ne nécessite pas d’API de réalité mixte Windows spéciale et s’appuie plutôt sur l’API existante de mappage d’entrée de moteur non réel. Pour plus d’informations sur l’utilisation de l' [here](https://docs.unrealengine.com/en-US/Gameplay/Input/index.html) API d’entrée, consultez

Les mappages de reconnaissance vocale ont été ajoutés à la section liaisons du moteur – entrée sous les mappages action et axe. 

![Positions d’entrée du moteur UE4](images/unreal/engine-input.png)
 
Voici un exemple de la surveillance ajoutée pour le « Jump » universel. Vous pouvez utiliser n’importe quel mot ou phrase en anglais. 

Après l’ajout d’un mappage vocal via les paramètres du projet, un développeur peut alors utiliser une logique inhabituelle standard pour gérer l’entrée, comme dans l’exemple suivant : 
 
![Action simple pour la voix](images/unreal/input-action-bp.png)
