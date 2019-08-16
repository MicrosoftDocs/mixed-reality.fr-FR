---
title: Prise en main
description: Ce guide décrit le moyen le plus rapide d’être opérationnel avec le développement de réalité mixte.
author: mattzmsft
ms.author: mazeller
ms.date: 08/06/2018
ms.topic: article
keywords: prise en main, principes de base, HoloLens, casque immersif, AR, VR, Unity, Visual Studio, démarrage rapide, comment
ms.openlocfilehash: 4277de37ffe4a7ab03f382626452b96bf9157634
ms.sourcegitcommit: 90ce9415889e7121dd2fd76a893dc3734672881b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64873959"
---
# <a name="get-started"></a>Prise en main

Bienvenue dans le monde du développement de la réalité mixte! Si vous débutez avec m... ce guide vous permettra de devenir opérationnel aussi rapidement que possible. Nous vous aiderons à configurer votre ordinateur pour le développement, à préparer vos appareils et à installer des outils qui accélèrent le processus de développement d’un MR. 

## <a name="intro-to-mixed-reality"></a>Présentation de la réalité mixte

Vous avez peut-être des questions sur ce que nous entendons par «réalité mixte» et sur la façon dont il se réfère à la réalité augmentée (AR) et à la réalité virtuelle (VR). En bref, la réalité mixte est la fusion du monde physique avec l’univers numérique. il s’agit donc d’un spectre qui couvre tout, de la réalité augmentée, où le contenu numérique est placé dans le monde réel jusqu’à la réalité virtuelle, où votre monde réel est presque entièrement remplacé par le numérique. 

![Exemple d’application de réalité mixte qui prend en charge les casques HoloLens et immersif (VR)](images/mr-island.png)<br>
*Les applications de réalité mixte peuvent prendre en charge les casques HoloLens et immersif (VR)*

Nous avons créé Windows Mixed Reality comme une plate-forme de développement unique et un ensemble d’outils qui peuvent couvrir le spectre de MR, et nous prenons actuellement en charge deux types d’appareils couvrant le même spectre: [Microsoft HoloLens](https://www.microsoft.com/hololens), le premier casque holographique autonome au monde et les contrôleurs [de mouvement et les casques immersifs immersifs de Windows Mixed Reality](https://www.microsoft.com/windows/windows-mixed-reality), qui se connectent à un PC pour de puissantes expériences de réalité virtuelle. Vous pouvez consulter notre présentation [réalité mixte?] (article pour obtenir une réponse plus complète si vous êtes intéressé.

## <a name="choose-your-development-path"></a>Choisir votre chemin de développement

Le moyen le plus simple de développer une application de réalité mixte est d’utiliser [Unity](https://unity3d.com), outil middleware puissant et populaire souvent utilisé pour le développement de jeux. Si vous souhaitez utiliser un moteur personnalisé, vous pouvez également effectuer une [génération par rapport à DirectX](directx-development-overview.md), mais la plupart des développeurs de Mr utilisent Unity pour leurs jeux et leurs applications. Avec Unity, vous pouvez créer une application de réalité mixte qui cible les casques HoloLens, immersifs (VR) ou les deux.

## <a name="prepare-your-pc-and-devices-for-development"></a>Préparer votre PC et vos appareils à des fins de développement

Que vous soyez en train de créer une application de réalité mixte qui cible des casques HoloLens, immersifs (VR), ou les deux, vous utiliserez un ensemble commun d’outils et d’API. Vous devez également vous assurer que votre ordinateur est suffisamment puissant pour le développement. 

>[!NOTE]
>Vous trouverez nos recommandations sur les spécifications des PC de développement, les versions prises en charge de chaque outil logiciel et les paramètres ou notes de configuration appropriés pour chacun d’entre eux dans l’article [installer les outils](install-the-tools.md) . Consultez cet article avant d’installer les outils ci-dessous.

Outils à installer:
* [Unity](https://store.unity.com/download)
* [Visual Studio (avec le kit de développement logiciel Windows 10)](https://developer.microsoft.com/windows/downloads)
* [Kit de pratiques de réalité mixte pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/GettingStarted.md)

Vous pouvez également [mettre votre appareil cible en mode développeur et configurer Visual Studio pour déployer des applications sur l’appareil cible](using-visual-studio.md).

### <a name="a-note-about-the-mixed-reality-toolkit-for-unity"></a>Note relative à la réalité mixte Toolkit pour Unity

![MRTK pour Unity](images/mrtkandunity.png)<br>

***YOYO ÉTOFFEZ-VOUS ET DITES À TOUT LE MONDE POURQUOI MRTK-UNITY EST SI INCROYABLE ET TOUT CE QU’IL POSSÈDE DANS:)***

La boîte à outils de réalité mixte est un ensemble de scripts et de composants destinés à accélérer le développement d’applications ciblant Microsoft HoloLens et les casques de réalité mixte Windows. Le projet a pour but de réduire le nombre d’obstacles qui gênent la création d’applications de réalité mixte et d’apporter une contribution à la Communauté de la réalité mixte.

## <a name="start-your-first-mr-project"></a>Commencez votre premier projet MR

Maintenant que votre PC et vos appareils sont configurés, vous êtes prêt à créer votre premier projet de réalité mixte dans Unity. Suivez notre premier cours sur Monsieur Academy, [Monsieur Basics 100: Prise en main d'](holograms-100.md)Unity, et à la fin, vous disposerez d’un cube opérationnel dans un casque de réalité mixte.

![Capture d’écran d’un cube dans un projet Unity de réalité mixte](images/mr-cube.PNG)<br>
*Votre premier projet de réalité mixte dans Unity-Hello World!*

## <a name="learn-more-and-get-help"></a>En savoir plus et obtenir de l’aide

Maintenant que vous avez créé votre premier projet MR, vous avez probablement d’autres à vous en faire! Voici quelques ressources qui devraient vous aider:
* [Documentation du développeur de la réalité mixte](mixed-reality.md) : vous êtes déjà ici, mais il y a bien plus à consulter, y compris la documentation technique, des conseils de conception, des exemples de projets et des études de cas.
* [Didacticiels de réalité mixte](tutorials.md) : suivez les didacticiels relatifs à la configuration des projets, à l’implémentation des blocs de construction RM de base, à l’intégration des services Cloud Azure dans votre application RM.
* [Découvrez Unity](https://unity3d.com/learn) : le site Web de Unity propose des didacticiels, des projets et des sessions de formation en direct pour les créateurs à chaque étape de l’apprentissage.

Vous pouvez également obtenir de l’aide auprès de ces formidables ressources de la communauté:
* [Forums de développeurs de réalité mixte](https://forums.hololens.com/) : forum officiel pour les développeurs de réalité mixte pour poser et répondre à des questions, ainsi que lire les actualités de développement Mr directement de Microsoft.
* [Canal HoloDevelopers](https://holodevelopersslack.azurewebsites.net/) -le canal de développeur spécifique à la réalité mixte, le plus robuste et le ingénieux; les développeurs ici sont compétents et utiles.
* [Forums Unity](https://forum.unity3d.com/) : forums officiels Unity.
