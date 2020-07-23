---
title: Installer les outils
description: Préparez-vous au développement de réalité mixte. Cet article fait référence aux dernières versions d’Unity, de Visual Studio et des autres outils recommandés pour le développement de casques immersifs HoloLens et Windows Mixed Reality.
author: thetuvix
ms.author: alexturn
ms.date: 3/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: mise à jour, outils, bien démarrer, principes de base, unity, visual studio, kit de ressources
ms.openlocfilehash: d29d27c8549a2ecdc98fa27df745fee07d1c056e
ms.sourcegitcommit: b392847529961ac36bbff154ce0830f8b2dbd766
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86300541"
---
# <a name="install-the-tools"></a>Installer les outils

Obtenez les outils dont vous avez besoin pour créer des applications Microsoft HoloLens et des casques immersifs Windows Mixed Reality (VR). Il n’existe pas de SDK de développement Windows Mixed Reality. Vous allez donc utiliser Visual Studio avec le SDK Windows 10.

Vous n’avez pas d’appareil de réalité mixte ? Si vous ne disposez pas d’un appareil HoloLens, vous pouvez installer l’[émulateur HoloLens](using-the-hololens-emulator.md) pour tester certaines fonctionnalités des applications de réalité mixte. Vous pouvez également utiliser le [simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md) pour tester les applications de réalité mixte si vous ne disposez pas d’un casque immersif.

Nous vous recommandons d’installer le moteur de jeu Unity, qui est la méthode la plus simple pour commencer à créer des applications de réalité mixte. Toutefois, vous pouvez également créer sur DirectX si vous souhaitez utiliser un moteur personnalisé.

>[!TIP]
>Ajoutez cette page à vos favoris, et consultez-la régulièrement pour être informé de la publication des nouvelles versions de chaque outil recommandé pour le développement de réalité mixte.

<br>

## <a name="installation-checklist"></a>Liste de contrôle pour l’installation


| Outil | Description | Remarques |
|---------|---------|---------|
| ![Logo Windows](images/Windows10_logo.png)<br><br><a href="https://www.microsoft.com/software-download/windows10" target="_blank">**Windows 10** (lien vers l’installation manuelle)</a> | Installez la version la plus récente de Windows 10 pour que le système d’exploitation de l’ordinateur soit le même que celui de la plateforme pour laquelle vous créez des applications de réalité mixte. | **Installation de Windows 10** <br> <ul><li>Vous pouvez installer la version la plus récente de Windows 10 via Windows Update, dans les paramètres, ou en créant un support d’installation à l’aide du lien situé dans la colonne de gauche.<li>Pour plus d’informations sur les dernières fonctionnalités de réalité mixte de chaque version de Windows 10, consultez les [notes de publication de la dernière version](release-notes-october-2018.md).</ul> **Activez le mode développeur sur votre PC** dans Paramètres > Mise à jour et sécurité > Pour les développeurs. <br><br> **Remarque concernant les ordinateurs gérés par l’entreprise :** si votre poste de travail est géré par le service informatique de votre entreprise, vous aurez peut-être besoin de le contacter pour les mises à jour. <br><br> **Versions « N » de Windows :** les casques immersifs Windows Mixed Reality ne sont pas pris en charge sur les versions « N » de Windows. |
| ![Logo Visual Studio](images/visualstudio_logo.png)<br><br><a href="https://visualstudio.microsoft.com/downloads/" target="_blank">**Visual Studio 2019 (16.2 ou ultérieur)** (lien vers l’installation)</a> | Environnement de développement intégré (IDE) complet pour Windows, et bien plus encore. Vous utiliserez Visual Studio pour écrire, déboguer, tester et déployer du code. | Veillez à installer les charges de travail suivantes : <ul><li>**Développement Desktop en C++**</li><li>**Développement pour la plateforme Windows universelle (UWP)**</li></ul>Dans la charge de travail UWP, n’oubliez pas de sélectionner le composant facultatif suivant si vous développez pour HoloLens :<ul><li>**Connectivité des périphériques USB**</li></ul>**Remarque concernant Unity :** Sauf si vous essayez intentionnellement d’installer une version plus récente (non LTS) de Unity dans un but spécifique, nous vous recommandons de *ne pas installer* la charge de travail Unity dans le cadre de l’installation de Visual Studio. Nous recommandons au lieu de cela d’installer le flux **Unity 2019 LTS**, comme indiqué ci-dessous.<br> <br>**Remarque :** Il existe actuellement des problèmes connus liés au débogage des applications de réalité mixte dans Visual Studio 2019, version 16.0.  Veillez à effectuer la mise à jour vers **Visual Studio 2019 version 16.2 ou ultérieure**. |
| ![Logo Windows](images/Windows10_logo.png)<br><br><a href="https://developer.microsoft.com//windows/downloads/windows-10-sdk" target="_blank">**Windows 10 SDK (10.0.18362.0)** (lien vers l’installation manuelle)</a> | Fournit les tout derniers en-têtes, bibliothèques, métadonnées et outils indispensables au développement des applications Windows 10 sur HoloLens 2. | Pour créer des applications HoloLens 2, vous devez installer le kit de développement logiciel (SDK) Windows, build 18362 ou ultérieur.<br> <br> Si vous développez uniquement des applications pour les casques de bureau Windows Mixed Reality ou HoloLens (1re génération), vous pouvez utiliser le SDK Windows qui est installé en même temps que Visual Studio 2017. |
| ![Logo Visual Studio](images/HoloLensIcon.jpg)<br><br><a href="https://go.microsoft.com/fwlink/?linkid=2132415" target="_blank">**Émulateur HoloLens 2 (Windows Holographique, version 2004, mise à jour de juin 2020)** (Lien d’installation : 10.0.19041.1106)</a><br> <br><a href="https://go.microsoft.com/fwlink/?linkid=2065980" target="_blank">**Émulateur HoloLens (1ère génération)** (Lien vers l’installation : 10.0.17763.134)</a> | L’émulateur vous permet d’exécuter des applications sur une image de machine virtuelle HoloLens si vous ne disposez pas d’un appareil HoloLens physique.<br> <br> | Pour bien démarrer avec l’émulateur, consultez [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md).<br> <br> **Votre système doit prendre en charge Hyper-V** pour que l’émulateur puisse être installé. Pour plus d’informations, consultez la section concernant la configuration système ci-dessous. <br>|

## <a name="choose-your-engine"></a>Choisir votre moteur

:::row:::
    :::column:::
        <a href="https://unity3d.com/unity/qa/lts-releases?version=2018.4" target="_blank">![Unity](images/unity_logo.png)<br>**Unity**</a><br>
        En général, nous recommandons d’utiliser le flux Unity LTS pour les nouveaux projets. Veillez à installer la dernière révision pour bénéficier des derniers correctifs de stabilité.<br>
        <br>
        Nous recommandons actuellement d’utiliser **Unity 2019**, qui est la version LTS nécessaire à MRTK v2.<br>
        <br>
        Certains développeurs voudront peut-être utiliser une version différente de Unity pour des raisons précises. Pour ces cas-là, Unity prend en charge les installations côte à côte de versions différentes.<br>
        <br>
        Consultez la [vue d’ensemble du développement Unity](unity-development-overview.md) afin de vous familiariser avec le développement Unity pour HoloLens 2 ou les casques immersifs Windows Mixed Reality.<br>
        <br>
        <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/releases" target="_blank">![MRTK](images/final_mrtk-small_logo.png)<br>**Mixed Reality Toolkit (MRTK)** </a><br>
        Mixed Reality Toolkit (MRTK) v2 pour Unity est un kit de développement multiplateforme open source pour les applications de réalité mixte.<br>
        <br>
        MRTK v2 vise à accélérer le développement des applications qui ciblent Microsoft HoloLens, les casques immersifs Windows Mixed Reality (VR) et la plateforme OpenVR. Le projet a pour but de réduire le nombre d’obstacles qui gênent la création d’applications de réalité mixte et d’apporter une contribution à la communauté à mesure que les choses évoluent.
    :::column-end:::
    :::column:::
        <a href="https://docs.unrealengine.com//GettingStarted/Installation/index.html" target="_blank">![Unreal](images/Unreal_logo.png)<br>**Unreal**</a><br>
        Unreal Engine 4 est un puissant moteur de création open source qui inclut une prise en charge complète de la réalité mixte en C++ et Blueprints.<br>
        <br>
        À compter d’Unreal Engine 4.25, la prise en charge d’HoloLens est complète et prête pour la production.<br>
        <br>
        Consultez la [vue d’ensemble du développement Unreal](unreal-development-overview.md) afin de vous familiariser avec le développement Unreal pour HoloLens 2.
    :::column-end:::
    :::column:::
        ![Développement d’applications en mode natif](images/visualstudio-small_logo.png)<br>
        [**Natif (OpenXR)** ](openxr-getting-started.md)<br>
        OpenXR est une norme d’API ouverte et libre de redevance proposée par Khronos. Elle permet aux moteurs d’accéder en mode natif à une large gamme d’appareils de nombreux fabricants qui couvrent le spectre de réalité mixte.  Le projet <a href="https://github.com/microsoft/OpenXR-MixedReality/tree/master/samples/BasicXrApp" target="_blank">BasicXrApp</a> illustre un exemple OpenXR simple composé de deux fichiers projet Visual Studio : l’un pour une application de bureau Win32 et l’autre pour une application HoloLens 2 UWP.<br>
        <br>
        <a href="https://marketplace.visualstudio.com/items?itemName=WindowsMixedRealityteam.WindowsMixedRealityAppTemplatesVSIX" target="_blank">**Natif (WinRT)** </a><br>
        Les <a href="https://marketplace.visualstudio.com/items?itemName=WindowsMixedRealityteam.WindowsMixedRealityAppTemplatesVSIX" target="_blank">modèles d’application natifs Windows Mixed Reality</a> fournissent tous les éléments de base dont vous avez besoin pour commencer à écrire une application de réalité mixte en utilisant DirectX avec des API natives. Comprend une boucle de rendu (ou « boucle de jeu »), une classe d’assistance DeviceResources pour gérer l’appareil et le contexte Direct3D, ainsi qu’un exemple de rendu d’hologramme simple. Disponible pour Direct3D11 et Direct3D 12.<br>
        <br>
        Consultez la [vue d’ensemble du développement natif](directx-development-overview.md) afin de vous familiariser avec le développement d’applications en mode natif avec WinRT ou OpenXR pour HoloLens 2 ou les casques immersifs Windows Mixed Reality.
    :::column-end:::
:::row-end:::

<br>

## <a name="mixed-reality-toolkit-mrtk"></a>Mixed Reality Toolkit (MRTK)

Mixed Reality Toolkit fournit des composants et des fonctionnalités qui sont destinés à accélérer le développement d’applications qui ciblent Microsoft HoloLens, les casques Windows Mixed Reality et la plateforme OpenVR. Le projet a pour but de réduire le nombre d’obstacles qui gênent la création d’applications de réalité mixte et d’apporter une contribution à la communauté au fur et à mesure de l’évolution.
* <a href="https://github.com/Microsoft/MixedRealityToolkit" target="_blank">Mixed Reality Toolkit</a> : ensemble de scripts et de composants destinés à accélérer le développement d’applications de réalité mixte.
* <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity" target="_blank">Mixed Reality Toolkit-Unity</a> : utilise le code du kit de ressources de base et facilite son utilisation dans Unity.
* <a href="https://github.com/Microsoft/MixedRealityToolkit-Unreal" target="_blank">Mixed Reality Toolkit - Unreal</a> : un ensemble de composants, sous forme de plug-ins, d’exemples et de documentations, conçus pour accélérer le développement d’applications de réalité mixte avec Unreal Engine.
* <a href="https://github.com/Microsoft/MixedRealityCompanionKit" target="_blank">Mixed Reality Companion Kit</a> : bits de code et composants pouvant ne pas s’exécuter directement sur HoloLens ou sur des casques immersifs (réalité virtuelle), mais au lieu de cela, se coupler à eux pour créer des expériences ciblant Windows Mixed Reality.

## <a name="setting-up-your-pc-for-mixed-reality-development"></a>Configuration de votre poste de travail pour le développement de réalité mixte

Le SDK Windows 10 fonctionne de manière optimale sur le système d’exploitation Windows 10. Ce SDK est également pris en charge par Windows 8.1, Windows 8, Windows 7, Windows Server 2012, Windows Server 2008 R2. Notez que les systèmes d’exploitation plus anciens ne prennent pas en charge tous les outils. 

### <a name="for-hololens-development"></a>Pour le développement HoloLens

Lorsque vous configurez votre ordinateur de développement pour HoloLens, vérifiez qu’il répond aux exigences de configuration du système pour <a href="https://unity3d.com/unity/system-requirements" target="_blank">Unity</a> et <a href="https://docs.microsoft.com//visualstudio/releases/2019/system-requirements" target="_blank">Visual Studio</a>. Si vous prévoyez d’utiliser l’émulateur HoloLens, vérifiez également que votre ordinateur répond aux [exigences de configuration système de l’émulateur HoloLens](using-the-hololens-emulator.md#hololens-emulator-system-requirements).

Pour bien démarrer avec l’émulateur HoloLens, consultez [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md).

Si vous prévoyez de développer des applications pour HoloLens et pour les casques immersifs (VR) Windows Mixed Reality, suivez les recommandations et les exigences système fournies dans la section ci-dessous.

### <a name="for-immersive-vr-headset-development"></a>Développement pour casques immersifs

>[!NOTE]
>Les instructions suivantes constituent les spécifications minimales actuellement recommandées qui s’appliquent à votre *ordinateur de développement* pour casques immersifs (VR). Ces instructions font l’objet de mises à jour régulières.

>[!WARNING]
>Vous ne devez pas confondre ces instructions avec les [instructions de compatibilité matérielle minimale](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines), qui listent les *spécifications relatives à l’ordinateur personnel* qui est ciblé par votre application ou votre jeu pour casque immersif.

Si votre ordinateur de développement pour casques immersifs n’a pas de ports HDMI et/ou USB 3.0 de taille suffisante, vous aurez besoin d’[adaptateurs](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/recommended-adapters-for-windows-mixed-reality-capable-pcs) pour connecter votre casque.

Il existe actuellement des [problèmes connus](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality) avec certaines configurations matérielles, en particulier avec les notebooks à l’affichage hybride.

<table>
<tr>
<th></th><th> Minimum</th><th> Recommandé</th>
</tr><tr>
<td> Processeur</td><td> <b>Notebook :</b> Processeur Intel Mobile Core i5 7e génération, double cœur avec hyper-threading <b>Desktop :</b> Processeur Intel Desktop i5 6e génération, double cœur avec hyper-threading <b>OU</b> AMD FX4350 quadruple cœur 4.2 Ghz</td><td> <b>Desktop :</b> Intel Desktop i7 6e génération (6 cœurs) <b>OU</b> AMD Ryzen 5 1600 (6 noyaux, 12 threads)</td>
</tr><tr>
<td> GPU</td><td> <b>Notebook :</b> NVIDIA GTX 965M, AMD RX 460M (2 Go) ou supérieur, GPU compatible avec DX12 <b>Desktop :</b> NVIDIA GTX 960/1050, AMD Radeon RX 460 (2 Go) ou supérieur, GPU compatible avec DX12</td><td><b>Desktop :</b> NVIDIA GTX 980/1060, AMD Radeon RX 480 (2 Go) ou supérieur, GPU compatible avec DX12</td>
</tr><tr>
<td> Version WDDM du pilote GPU</td><td colspan="2"> Pilote WDDM 2.2</td>
</tr><tr>
<td> Enveloppe thermique</td><td colspan="2"> 15W ou supérieure</td>
</tr><tr>
<td> Ports d’affichage graphique</td><td colspan="2"> 1 port d’affichage graphique disponible pour les&#160;casques (HDMI 1.4 ou DisplayPort 1.2 pour les casques 60Hz, HDMI 2.0 ou DisplayPort 1.2 pour les casques 90Hz)</td>
</tr><tr>
<td> Résolution de l’affichage</td><td colspan="2"> Résolution : SVGA (800x600) ou une plus grande profondeur de couleurs : 32 bits de couleur par pixel</td>
</tr><tr>
<td> Memory</td><td> 8 Go de RAM ou plus</td><td> 16 Go de RAM ou plus</td>
</tr><tr>
<td> Stockage</td><td colspan="2"> &gt;10 Go d’espace libre supplémentaire</td>
</tr><tr>
<td> Ports USB</td><td colspan="2"> 1 port USB disponible pour les casques (USB 3.0 type A) <b>Remarque : il doit fournir un minimum de 900mA</b></td>
</tr><tr>
<td> Bluetooth</td><td colspan="2"> Bluetooth 4.0 (connectivité des accessoires)</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi

* [Vue d’ensemble du développement](development.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Utilisation du simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md)
* [Vue d’ensemble du développement Unity](unity-development-overview.md)
* [Vue d’ensemble du développement Unreal](unreal-development-overview.md)
* [Vue d’ensemble du développement DirectX](directx-development-overview.md)
* [Archive de l’émulateur HoloLens](hololens-emulator-archive.md)
