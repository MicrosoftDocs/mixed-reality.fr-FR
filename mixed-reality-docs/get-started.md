---
title: Prise en main
description: Ce guide décrit le moyen le plus rapide pour être rapidement opérationnel avec le développement de réalité mixte.
author: mattzmsft
ms.author: mazeller
ms.date: 08/06/2018
ms.topic: article
keywords: prise en main, principes de base, HoloLens, casque immersif, ar, vr, unity, visual studio, Guide de démarrage rapide, comment
ms.openlocfilehash: 92fbc6eee227da571ff36401f84cf81a093062d7
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594859"
---
# <a name="get-started"></a>Prise en main

Bienvenue dans le monde du développement de réalité mixte ! Si vous débutez avec MR, ce guide sera votre hub pour être opérationnel et en cours d’exécution aussi rapidement que possible. Nous allons vous aider à préparer votre jeu de PC pour le développement, préparer votre ou vos appareils et installer les outils qui permettent d’accélérer le processus de développement MR. 

## <a name="intro-to-mixed-reality"></a>Introduction à la réalité mixte

Avoir des questions sur ce que nous entendons par « réalité mixte » et sa relation avec la réalité augmentée (AR) et la réalité virtuelle (VR). En bref, réalité mixte est la fusion du monde physique avec le monde numérique, il s’agit d’une gamme qui couvre tous les éléments à partir de la réalité augmentée, où le contenu numérique est placé dans le monde réel, réalité virtuelle, où votre monde réel est presque entièrement remplacé par la numérique. 

![Exemple d’une application de réalité mixte qui prend en charge HoloLens et des casques IMMERSIFS (VR)](images/mr-island.png)<br>
*Applications de réalité mixte peuvent prendre en charge HoloLens et des casques IMMERSIFS (VR)*

Nous avons créé la réalité mixte Windows en tant que plateforme de développement unique et ensemble d’outils permettant de couvrir le spectre MR, et nous prenons en charge deux types d’appareils qui couvrent la gamme même : [Microsoft HoloLens](https://www.microsoft.com/hololens), première autonome HOLOGRAPHIQUE casque dans le monde, et [des casques IMMERSIFS réalité mixte Windows et les contrôleurs de mouvement](https://www.microsoft.com/windows/windows-mixed-reality), laquelle se connecter à un PC pour des expériences de réalité virtuelle puissante. Vous pouvez consulter notre ce qui est [une réalité mixte ?] (article pour une réponse plus approfondie si cela vous intéresse.

## <a name="choose-your-development-path"></a>Choisissez votre chemin d’accès de développement

À l’aide de la façon la plus simple de développer une application de réalité mixte [Unity](https://unity3d.com), un outil d’intergiciel (middleware) puissants et les plus souvent utilisé pour le développement de jeux. Si vous souhaitez utiliser un moteur personnalisé, vous pouvez également [générer avec DirectX](directx-development-overview.md), mais la plupart des développeurs MR utiliser Unity pour leurs applications et jeux. Avec Unity, vous serez en mesure de créer une application de réalité mixte qui cible HoloLens, des casques IMMERSIFS (VR) ou les deux !

## <a name="prepare-your-pc-and-devices-for-development"></a>Préparer vos PC et appareils pour le développement

Si vous créez une application de réalité mixte qui cible HoloLens, des casques IMMERSIFS (VR) ou les deux, vous allez utiliser un ensemble commun d’outils et API. Vous allez également s’assurer que votre PC est suffisamment puissant pour le développement, que vous allez faire. 

>[!NOTE]
>Vous pouvez trouver des spécifications de nos recommandations sur les PC de développement, les versions prises en charge de chaque outil de logiciels et paramètres correspondants ou configuration note pour chacune d’elles dans le [installer les outils](install-the-tools.md) article. Veuillez consulter cet article avant d’installer les outils ci-dessous.

Outils pour installer :
* [Unity](https://store.unity.com/download)
* [Visual Studio (avec Windows 10 SDK)](https://developer.microsoft.com/windows/downloads)
* [Kit de ressources de réalité mixte pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/GettingStarted.md)

Vous souhaiterez également [mis votre appareil cible en mode développeur et configurer Visual Studio pour le déploiement d’applications sur l’appareil cible](using-visual-studio.md).

### <a name="a-note-about-the-mixed-reality-toolkit-for-unity"></a>Remarque à propos de la boîte à outils de réalité mixte pour Unity

![MRTK pour Unity](images/mrtkandunity.png)<br>

***JOJO VEUILLEZ DONNER VIE À CE STADE ET TOUT LE MONDE DIRE POURQUOI MRTK-UNITY EST SI ÉPATANTE ET TOUS LES AVANTAGES OFFERTS QU’À L’INTÉRIEUR DE  :)***

Le Toolkit de réalité mixte est une collection de scripts et les composants destinés à accélérer le développement d’applications qui ciblent Microsoft HoloLens et Windows Mixed Reality casques. Le projet est destiné à réduire les barrières à l’entrée à créer des applications de réalité mixte et contribuer à la Communauté, tous les besoins d’évolution.

## <a name="start-your-first-mr-project"></a>Démarrer votre premier projet MR

Maintenant que votre PC et les périphériques sont configurés, vous êtes prêt à créer votre premier projet de réalité mixte dans Unity. Suivez notre premier cours academy MR, [MR principes de base 100 : Mise en route avec Unity](holograms-100.md), et à la fin, vous aurez un cube soit opérationnel dans un casque de réalité mixte.

![Capture d’écran d’un cube dans un projet Unity de réalité mixte](images/mr-cube.PNG)<br>
*Votre premier projet de réalité mixte dans Unity - Bonjour tout le monde !*

## <a name="learn-more-and-get-help"></a>En savoir plus et obtenir de l’aide

Maintenant que vous avez créé votre premier projet MR, vous avez probablement faim et bien plus encore ! Voici quelques ressources qui peut aider à :
* [Mixte de documentation pour développeurs réalité](mixed-reality.md) - vous êtes déjà ici, mais il est bien plus encore à consulter, y compris la documentation technique, des conseils de conception, des exemples de projets et des études de cas.
* [Académie de réalité mixte](academy.md) -suivre des didacticiels qui couvrent tous les éléments à partir de la configuration de projets, à l’implémentation des principaux blocs de construction MR, à l’intégration d’Azure cloud services dans votre application MR.
* [Découvrez Unity](https://unity3d.com/learn) -site Web de Unity propose des didacticiels, des projets et des sessions de formation en direct pour les créateurs à chaque étape de la formation.

Vous pouvez également vous aider à partir de ces ressources de communauté très :
* [Une réalité mixte forums de développeurs](https://forums.hololens.com/) -le forum officiel pour les développeurs de réalité mixte à poser et répondre aux questions, ainsi que pour lire les actualités de développement MR directement auprès de Microsoft.
* [Canal de HoloDevelopers Slack](https://holodevelopersslack.azurewebsites.net/) -le plus robuste et ingénieux externes mixte de canal de développeur spécifique à la réalité ; ici les développeurs d’être compétentes et utile.
* [Forums de Unity](https://forum.unity3d.com/) -forums officielles de Unity.
