---
title: Installer les outils
description: Préparez-vous au développement de réalité mixte. Cet article fait référence aux dernières versions d’Unity, de Visual Studio et des autres outils recommandés pour le développement de casques immersifs HoloLens et Windows Mixed Reality.
author: thetuvix
ms.author: alexturn
ms.date: 07/31/2020
ms.topic: article
ms.localizationpriority: high
keywords: mise à jour, outils, bien démarrer, principes de base, unity, visual studio, kit de ressources
ms.openlocfilehash: f5c779aa0bb89fe66b53419b03ec1b4d3e6b562b
ms.sourcegitcommit: ef0bf03833eda826ed0b884859b4573775112aba
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2020
ms.locfileid: "87476890"
---
# <a name="install-the-tools"></a>Installer les outils

Obtenez les outils dont vous avez besoin pour créer des applications Microsoft HoloLens et des casques immersifs Windows Mixed Reality (VR). Il n’existe pas de SDK de développement Windows Mixed Reality. Vous allez donc utiliser Visual Studio avec le SDK Windows 10.

Vous n’avez pas d’appareil de réalité mixte ? Si vous ne disposez pas d’un appareil HoloLens, vous pouvez installer l’[émulateur HoloLens](using-the-hololens-emulator.md) pour tester certaines fonctionnalités des applications de réalité mixte. Vous pouvez également utiliser le [simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md) pour tester les applications de réalité mixte si vous ne disposez pas d’un casque immersif. Si vous utilisez Unity, vous pouvez vous servir de la simulation d’entrée de [Mixed Reality Toolkit (MRTK)](https://github.com/Microsoft/MixedRealityToolkit-Unity) pour tester différents types d’interactions d’entrée, comme le suivi de la main et le suivi oculaire.

Nous vous recommandons d’installer le moteur de jeu Unity, qui est la méthode la plus simple pour commencer à créer des applications de réalité mixte. Toutefois, vous pouvez également créer sur DirectX si vous souhaitez utiliser un moteur personnalisé.

>[!TIP]
>Ajoutez cette page à vos favoris, et consultez-la régulièrement pour être informé de la publication des nouvelles versions de chaque outil recommandé pour le développement de réalité mixte.

<br>

## <a name="installation-checklist"></a>Liste de contrôle pour l’installation


| Outil | Remarques |
|---------|---------|
| ![Logo Windows](images/Windows10_logo.png)<br><br><a href="https://www.microsoft.com/software-download/windows10" target="_blank">**Windows 10** (lien vers l’installation manuelle)</a><br><br>Installez la version la plus récente de Windows 10 pour que le système d’exploitation de l’ordinateur soit le même que celui de la plateforme pour laquelle vous créez des applications de réalité mixte.  | **Installation de Windows 10** <br> Vous pouvez installer la version la plus récente de Windows 10 via Windows Update, dans les paramètres, ou en créant un support d’installation à l’aide du lien situé dans la colonne de gauche. <br><br>Pour plus d’informations sur les dernières fonctionnalités de réalité mixte de chaque version de Windows 10, consultez les [notes de publication de la dernière version](release-notes-october-2018.md). **Activez le mode développeur sur votre PC** dans Paramètres > Mise à jour et sécurité > Pour les développeurs. <br><br> **Note pour les PC qui appartiennent ou sont gérés par l’entreprise**<br>Si votre PC est géré par le service informatique de votre entreprise, vous aurez probablement besoin de le contacter pour les mises à jour. <br><br> **Versions « N » de Windows**<br> les casques immersifs Windows Mixed Reality ne sont pas pris en charge sur les versions « N » de Windows. |
| ![Logo Visual Studio](images/visualstudio_logo.png)<br><br><a href="https://visualstudio.microsoft.com/downloads/" target="_blank">**Visual Studio 2019 (16.2 ou ultérieur)** (lien vers l’installation)</a> <br><br>Environnement de développement intégré (IDE) complet pour Windows, et bien plus encore. Vous utiliserez Visual Studio pour écrire, déboguer, tester et déployer du code. | Veillez à installer les charges de travail suivantes : <br><br>**● Développement Desktop en C++**<br>**● Développement UWP (Plateforme Windows universelle)**<br><br>Dans la charge de travail UWP, n’oubliez pas de sélectionner le composant facultatif suivant si vous développez pour HoloLens :<br><br>**● Connectivité des appareils USB**<br><br>**Note sur Unity**<br>Sauf si vous essayez intentionnellement d’installer une version plus récente (non LTS) de Unity dans un but spécifique, nous vous recommandons de *ne pas installer* la charge de travail Unity dans le cadre de l’installation de Visual Studio. Nous recommandons au lieu de cela d’installer le flux **Unity 2019 LTS**, comme indiqué ci-dessous.<br><br>**Remarque**<br>Il existe actuellement des problèmes connus liés au débogage des applications de réalité mixte dans Visual Studio 2019, version 16.0.  Veillez à effectuer la mise à jour vers **Visual Studio 2019 version 16.2 ou ultérieure**. |
| ![Logo Windows](images/Windows10_logo.png)<br><br><a href="https://developer.microsoft.com//windows/downloads/windows-10-sdk" target="_blank">**Windows 10 SDK (10.0.18362.0)** (lien vers l’installation manuelle)</a> <br><br>Fournit les tout derniers en-têtes, bibliothèques, métadonnées et outils indispensables au développement des applications Windows 10 sur HoloLens 2. | **Pour créer des applications HoloLens 2, vous devez installer le kit SDK Windows, build 18362 ou ultérieur.**<br> <br> Si vous développez uniquement des applications pour les casques de bureau Windows Mixed Reality ou HoloLens (1re génération), vous pouvez utiliser le SDK Windows qui est installé en même temps que Visual Studio 2017. |
| ![Logo Visual Studio](images/HoloLensIcon.jpg)<br><br><a href="https://go.microsoft.com/fwlink/?linkid=2132415" target="_blank">**Émulateur HoloLens 2 (Windows Holographique, version 2004, mise à jour de juin 2020)** (Lien d’installation : 10.0.19041.1106)</a><br> <br><a href="https://go.microsoft.com/fwlink/?linkid=2065980" target="_blank">**Émulateur HoloLens (1ère génération)** (Lien vers l’installation : 10.0.17763.134)</a> <br><br>L’émulateur vous permet d’exécuter des applications sur une image de machine virtuelle HoloLens si vous ne disposez pas d’un appareil HoloLens physique.<br> <br> | Pour bien démarrer avec l’émulateur, consultez [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md).<br> <br> **Votre système doit prendre en charge Hyper-V** pour que l’émulateur puisse être installé. Pour plus d’informations, consultez la section concernant la configuration système ci-dessous. <br>|

## <a name="choose-your-engine"></a>Choisir votre moteur

Maintenant que vous avez Windows 10, Visual Studio et le SDK Windows 10, nous allons choisir un moteur. 

[!INCLUDE[](~/includes/tools-overview.md)]
