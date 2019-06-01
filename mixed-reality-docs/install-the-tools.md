---
title: Installer les outils
description: Commencez ici pour préparer pour le développement de réalité mixte. Cet article doit toujours refléter les dernières versions d’Unity, Visual Studio et autres outils recommandés pour le développement d’immersives casque HoloLens et Windows Mixed Reality.
author: yoyozilla
ms.author: yoyozilla
ms.date: 2/11/2019
ms.topic: article
ms.localizationpriority: high
keywords: mis à jour, outils, prise en main, principes de base, unity, visual studio, le Kit de ressources
ms.openlocfilehash: 32dcda0eceb8d3717de7b2502d86f03cda975b8f
ms.sourcegitcommit: 60060386305eabfac2758a2c861a43c36286b151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453728"
---
# <a name="install-the-tools"></a>Installer les outils

Obtenez les outils que vous avez besoin pour créer des applications pour Microsoft HoloLens et des casques Windows Mixed Reality IMMERSIFS (VR). Il n’existe aucun développement de kit de développement logiciel pour Windows Mixed Reality distinct ; vous allez utiliser Visual Studio avec le SDK Windows 10.

Vous n’avez un appareil de réalité mixte ? Vous pouvez installer le [HoloLens émulateur](using-the-hololens-emulator.md) pour tester certaines fonctionnalités des applications de réalité mixte sans un HoloLens. Vous pouvez également utiliser le [simulateur de réalité mixte Windows](using-the-windows-mixed-reality-simulator.md) pour tester vos applications de réalité mixte pour des casques IMMERSIFS.

Nous vous recommandons d’installer le moteur de jeu Unity comme le moyen le plus simple pour commencer à créer des applications de réalité mixte, toutefois, vous pouvez également générer par rapport à DirectX si vous souhaitez que d’utiliser un moteur personnalisé.

>[!TIP]
>Marquer cette page et vérifiez régulièrement pour maintenir à jour sur la version la plus récente de chaque outil recommandé pour le développement de réalité mixte.

<br>

>[!VIDEO https://www.youtube.com/embed/3l20TWhw4S8]

## <a name="installation-checklist"></a>Aide-mémoire d’installation


| Tool | Description | Notes |
|---------|---------|---------|
| ![Logo Windows](images/Windows10_logo.png)<br><br><a href="https://www.microsoft.com/software-download/windows10" target="_blank">**Windows 10**<br>(Installation manuelle d’un lien)</a> | Installez la version la plus récente de Windows 10 afin de système d’exploitation de l’ordinateur correspond à la plateforme pour laquelle vous créez des applications de réalité mixte. | **Installation de Windows 10** <br> <ul><li>Vous pouvez installer la version la plus récente de Windows 10 via Windows Update dans les paramètres ou en créant le support d’installation (en utilisant le lien dans la colonne de gauche).<li>Consultez [notes de publication](release-notes-october-2018.md) pour plus d’informations sur la plus récente mixte des fonctionnalités de réalité disponibles avec chaque version de Windows 10.</ul> **Activer le mode développeur sur votre PC** à Paramètres > mise à jour & sécurité > pour les développeurs. <br><br> **Remarque pour l’entreprise et les PC d’entreprise gérés :** si votre PC est géré par un de votre organisation informatique, vous devrez peut-être contacter pour mettre à jour. <br><br> **Versions de « n » de Windows :** Des casques Windows Mixed Reality IMMERSIFS (VR) ne sont pas pris en charge sur les versions de « n » de Windows. |
| ![Logo Visual Studio](images/visualstudio_logo.png)<br><br><a href="https://visualstudio.microsoft.com/downloads/" target="_blank">**Visual Studio 2017**<br>(Lien d’installation)</a> | Environnement complet de développement intégré (IDE) pour Windows et bien plus encore. Vous utiliserez Visual Studio pour écrire du code, déboguer, tester et déployer. | **Pour installer les charges de travail :** <ul><li>Développement Desktop en C++</li><li>Développement de plate-forme de Windows Universal</li></ul>**Remarque à propos de Unity :** Sauf si vous êtes intentionnellement essayez d’installer une version plus récente de (non-LTS) de Unity dans un but spécifique, nous recommandons *pas* l’installation de la charge de travail Unity dans le cadre de l’installation de Visual Studio et installer à la place les 2018.4 LTS flux de Unity comme indiqué ci-dessous.<br> <br>**Remarque :** Il existe certains problèmes connus avec le développement de réalité mixte dans Visual Studio 2019 pour le moment.  Pour l’instant, nous vous recommandons de continuer à l’aide de Visual Studio 2017. |
| ![Logo Windows](images/Windows10_logo.png)<br><br><a href="https://developer.microsoft.com/en-US/windows/downloads/windows-10-sdk" target="_blank">**Windows 10 SDK (10.0.18362.0)**<br>(Installation manuelle d’un lien)</a> | Fournit la dernière en-têtes, bibliothèques, métadonnées et les outils pour la création d’applications Windows 10 sur HoloLens 2. | Pour générer des applications de HoloLens 2, vous devez installer le Kit de développement logiciel, build 18362 ou version ultérieure de Windows.<br> <br> Si vous seulement développez des applications pour les casques de bureau Windows Mixed Reality ou HoloLens (1ère génération), vous pouvez utiliser le Kit de développement logiciel Windows installé par Visual Studio 2017. |
| ![Logo Visual Studio](images/HoloLensIcon.jpg)<br><br><a href="https://go.microsoft.com/fwlink/?linkid=2087187" target="_blank">**Émulateur de HoloLens 2**<br>(Lien d’installation : 10.0.18362.1005)</a><br> <br><a href="https://go.microsoft.com/fwlink/?linkid=2065980" target="_blank">**HoloLens (1er gen) émulateur**<br>(Lien d’installation : 10.0.17763.253)</a> | L’émulateur vous permet d’exécuter des applications sur une image de machine virtuelle HoloLens sans un HoloLens physique.<br> <br> Ce package inclut également des modèles de projet DirectX HOLOGRAPHIQUE pour Visual Studio. | Consultez [à l’aide de l’émulateur HoloLens](using-the-hololens-emulator.md) pour plus d’informations sur la mise en route avec l’émulateur.<br> <br> **Votre système doit prendre en charge Hyper-V** pour l’installation de l’émulateur réussisse. Veuillez vous reporter la section de configuration système requise ci-dessous pour plus d’informations. Si vous le souhaitez, vous pouvez sélectionner pour installer uniquement les modèles sans l’émulateur.<br>|
| ![Logo de Unity](images/unity_logo.png)<br><br><a href="https://unity3d.com/unity/qa/lts-releases?version=2018.4" target="_blank">**Unity 2018.4**<br>(Lien d’installation)</a> | Le moteur de jeu Unity est le moyen le plus simple pour créer des expériences de réalité mixte, avec prise en charge intégrée pour les fonctionnalités de Windows Mixed Reality. | Nous recommandons généralement le flux Unity LTS (prise en charge de Long terme) en tant que la meilleure version avec lequel démarrer de nouveaux projets, la mise à jour à sa dernière révision à assimiler les derniers correctifs de stabilité.<br> <br>Recommandation actuelle consiste à utiliser **Unity 2018.4.x**, qui est la version LTS requise pour v2 MRTK ci-dessous.<br> <br>Certains développeurs voudront à utiliser une version différente de Unity pour des raisons spécifiques. Pour ces cas, Unity prend en charge les installations côte à côte de différentes versions. |
| ![Logo MRTK](images/MRTKIcon.jpg)<br><br><a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/releases" target="_blank">**La boîte à outils de réalité mixte (MRTK v2) pour Unity**</a> | V2 MRTK pour Unity est un kit de développement multiplateforme open source pour les applications de réalité mixte.<br><br> MRTK v2 vise à accélérer le développement d’applications qui ciblent Microsoft HoloLens, des casques Windows Mixed Reality IMMERSIFS (VR) et la plateforme OpenVR. Le projet est destiné à réduire les obstacles à l’entrée pour créer des applications de réalité mixte et qui contribuent à la Communauté en tant que nous avons tous de croître. | En savoir plus sur MRTK v2 en visitant le projet <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/wiki" target="_blank">wiki GitHub</a>. |


## <a name="mixed-reality-toolkit"></a>Kit de ressources de réalité mixte

Le Kit de ressources de réalité mixte fournit des composants et des fonctionnalités qui sont destinées à accélérer le développement d’applications qui ciblent Microsoft HoloLens, casques de réalité mixte Windows et OpenVR plateforme. Le projet est destiné à réduire les barrières à l’entrée à créer des applications de réalité mixte et contribuer à la Communauté, tous les besoins d’évolution.
* <a href="https://github.com/Microsoft/MixedRealityToolkit" target="_blank">MixedRealityToolkit</a>
* <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">Unity-MixedRealityToolkit</a> - utilise le code à partir de la boîte à outils de base et le rend plus faciles à utiliser dans Unity.
* <a href="https://github.com/Microsoft/MixedRealityCompanionKit" target="_blank">MixedRealityCompanionKit</a> - code bits et les composants qui ne peuvent pas s’exécuter directement sur HoloLens ou des casques IMMERSIFS (VR), mais au lieu de cela paire avec eux pour créer des expériences ciblant Windows Mixed Reality.

## <a name="setting-up-your-pc-for-mixed-reality-development"></a>Configuration de votre PC pour le développement de réalité mixte

Le SDK Windows 10 fonctionne mieux sur le système d’exploitation Windows 10. Ce SDK est également pris en charge sur Windows 8.1, Windows 8, Windows 7, Windows Server 2012, Windows Server 2008 R2. Notez que tous les outils sont pris en charge sur les systèmes d’exploitation plus anciens. 

### <a name="for-hololens-development"></a>Pour le développement de HoloLens

Lorsque vous configurez votre PC de développement pour le développement de HoloLens, vérifiez qu’il répond à la configuration système requise pour les deux <a href="https://unity3d.com/unity/system-requirements" target="_blank">Unity</a> et <a href="https://www.visualstudio.com/productinfo/vs2017-system-requirements-vs" target="_blank">Visual Studio</a>. Si vous envisagez d’utiliser le HoloLens (1er gen) émulateur, vous voudrez Assurez-vous que votre PC de possède le [configuration système requise pour HoloLens émulateur](using-the-hololens-emulator.md#hololens-emulator-system-requirements) également.

Pour commencer avec l’émulateur de HoloLens, consultez [à l’aide de l’émulateur HoloLens](using-the-hololens-emulator.md).

Si vous envisagez de développer pour HoloLens et Windows Mixed Reality casques (VR) immersives, utilisez les recommandations système et les exigences dans la section ci-dessous.

### <a name="for-immersive-vr-headset-development"></a>Pour le développement de casque immersive (VR)

>[!NOTE]
>Les instructions suivantes sont les spécifications minimales et recommandées actuelles pour votre casque (VR) immersive *PC de développement*et peut être mis à jour régulièrement.

>[!WARNING]
>Ne confondez pas ceci avec la [les instructions de compatibilité du matériel PC minimale](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines), qui présente le *caractéristiques du consommateur PC* auquel vous devez cibler votre application de casque captivante (VR) ou votre jeu.

Si votre PC de développement immersif casque n’a pas de ports HDMI et/ou USB 3.0 en taille réelle, vous devez [adaptateurs](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/recommended-adapters-for-windows-mixed-reality-capable-pcs) pour se connecter à votre casque.

Il existe actuellement [problèmes connus](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality) avec certaines configurations matérielles, en particulier avec les ordinateurs portables qui ont les graphiques hybrides.

<table>
<tr>
<th></th><th> Minimum</th><th> Recommandé</th>
</tr><tr>
<td> Processeur</td><td> <b>carnet de notes :</b> Intel Mobile Core i5 7e génération de processeur, double cœur avec Hyper-Threading <b>Desktop :</b> Intel Desktop i5 6ème génération de processeur, double cœur avec Hyper-Threading <b>ou</b> AMD FX4350 équivalent de cœurs 4.2 Ghz</td><td> <b>Bureau :</b> Bureau d’Intel i7 6ème génération (6 cœurs) <b>ou</b> AMD Ryzen 1600 5 (6 noyaux, 12 threads)</td>
</tr><tr>
<td> Processeur graphique</td><td> <b>carnet de notes :</b> NVIDIA GTX 965M, AMD RX 460M (2 Go) équivalente ou supérieure de GPU compatible avec DX12 <b>Desktop :</b> NVIDIA GTX 960/1050, GPU compatible avec DX12 équivalente ou supérieure AMD Radeon RX 460 (2 Go)</td><td><b>Bureau :</b> NVIDIA GTX 980/1060, GPU compatible avec DX12 équivalente ou supérieure AMD Radeon RX 480 (2 Go)</td>
</tr><tr>
<td> Version du GPU pilote WDDM</td><td colspan="2"> Pilote WDDM 2.2</td>
</tr><tr>
<td> Puissance de conception thermique</td><td colspan="2"> 15W ou supérieur</td>
</tr><tr>
<td> Ports d’affichage graphique</td><td colspan="2"> 1 x graphiques disponibles de port pour l’écran&#160;casque (HDMI 1.4 ou 1.2 DisplayPort pour casques 60Hz, HDMI 2.0 ou 1.2 DisplayPort pour les casques 90Hz)</td>
</tr><tr>
<td> Résolution d’affichage</td><td colspan="2"> Résolution : SVGA (800 x 600) ou une plus grande profondeur de couleur : 32 bits de couleur par pixel</td>
</tr><tr>
<td> Mémoire</td><td> 8&#160;Go de RAM ou supérieur</td><td> 16 Go de RAM ou supérieur</td>
</tr><tr>
<td> Stockage</td><td colspan="2"> &gt;10 Go d’espace libre supplémentaire</td>
</tr><tr>
<td> Ports USB</td><td colspan="2"> 1 x USB disponible le port pour casque (USB 3.0 Type-A) <b>Remarque : USB doit fournir un minimum de 900mA</b></td>
</tr><tr>
<td> Bluetooth</td><td colspan="2"> 4.0 Bluetooth (pour la connectivité accessoire)</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi

* [Vue d’ensemble du développement](development-overview.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Utilisation du simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md)
* [Vue d’ensemble du développement Unity](unity-development-overview.md)
* [Vue d’ensemble du développement DirectX](directx-development-overview.md)
* [Archive de l’émulateur HoloLens](hololens-emulator-archive.md)
