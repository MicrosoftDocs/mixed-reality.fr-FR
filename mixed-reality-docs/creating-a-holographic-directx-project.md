---
title: Création d’un projet de DirectX HOLOGRAPHIQUE
description: Explique comment créer une application HOLOGRAPHIQUE basée sur le modèle d’application Windows Mixed Reality.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, application HOLOGRAPHIQUE, nouvelle application, application UWP, application du modèle, hologrammes, nouveau projet, procédure pas à pas, téléchargement, exemple de code
ms.openlocfilehash: a7eac9d8056fe5f7bcc442d6441f71331fa96cf6
ms.sourcegitcommit: 19c9bff21061d485821b61c9f3498daef8fa8235
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65828129"
---
# <a name="creating-a-holographic-directx-project"></a>Création d’un projet de DirectX HOLOGRAPHIQUE

Une application HOLOGRAPHIQUE que vous créez pour une HoloLens sera un <a href="https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide" target="_blank">application universelle Windows Platform (UWP)</a>.  Si vous ciblez les casques de bureau Windows Mixed Reality, vous pouvez créer une application UWP ou une application Win32.

Le modèle d’application DirectX 11 HOLOGRAPHIQUE UWP est similaire au modèle d’application DirectX 11 UWP ; Il inclut une boucle de programme (ou le « jeu boucle »), un **DeviceResources** classe pour gérer les appareils de Direct3D et le contexte et une classe de renderer de contenu simplifiée. Il possède également un <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview" target="_blank">IFrameworkView</a>, à l’instar de toute autre application UWP.

L’application de réalité mixte, toutefois, a des fonctions supplémentaires qui ne sont pas présentes dans une application Direct3D 11 UWP classique. Le modèle d’application Windows holographique est en mesure de :
* Gérer les ressources de périphérique Direct3D associés au HOLOGRAPHIQUES caméras.
* Récupérer des mémoires tampons d’arrière-plan caméra à partir du système.
* Gérer [les regards](gaze.md) d’entrée et de reconnaître une simple [mouvement](gestures.md).
* Passer en mode de rendu stéréo plein écran.

## <a name="how-do-i-get-started"></a>Comment pour démarrer ?

Première [installer les outils](install-the-tools.md), suivant les instructions sur le téléchargement de Visual Studio 2017 et l’émulateur Microsoft HoloLens. Les modèles d’application HOLOGRAPHIQUE sont inclus dans le même programme d’installation en tant que l’émulateur Microsoft HoloLens. Assurez-vous également que la possibilité d’installer les modèles est sélectionnée avant d’installer.

Vous êtes maintenant prêt à créer votre application DirectX 11 Windows Mixed Reality ! Notez que pour supprimer l’exemple de contenu, commentez la **DRAW_SAMPLE_CONTENT** directive de préprocesseur dans *pch.h*.

## <a name="creating-a-uwp-project"></a>Création d’un projet UWP

Une fois le [outils sont installés](install-the-tools.md) vous pouvez ensuite créer un projet de DirectX UWP HOLOGRAPHIQUE.

Pour créer un nouveau projet :
1. Démarrer **Visual Studio**.
2. À partir de la **fichier** menu, pointez sur **New** et sélectionnez **projet** dans le menu contextuel. Le **nouveau projet** boîte de dialogue s’ouvre.
3. Développez **installé** sur la gauche et développez le **Visual C++**  nœud de langage.
4. Accédez à la **Windows universel > Holographic** nœud et sélectionnez **application de 11 HOLOGRAPHIQUE DirectX (Windows universel) (C++/WinRT)**.
   ![Capture d’écran de la HOLOGRAPHIQUE DirectX 11 C++modèle de projet d’application WinRT UWP dans Visual Studio](images/holographic-directx-app-cpp-new-project.png)<br>
   *HOLOGRAPHIQUE DirectX 11 C++modèle de projet d’application WinRT UWP dans Visual Studio*
   >[!IMPORTANT]
   >N’oubliez pas que le nom du modèle de projet inclut « (C++/WinRT) ».  Si ce n’est pas le cas, vous avez une version antérieure des modèles de projet HOLOGRAPHIQUE installé.  Pour obtenir les derniers modèles de projet, [installer l’émulateur de HoloLens dernière](using-the-hololens-emulator.md).
5. Renseignez le **nom** et **emplacement** zones de texte et cliquez ou appuyez sur **OK**. Le projet d’application holographique est créé.
6. Pour le développement ciblant uniquement les 2 HoloLens, vérifiez que le **version cible** et **version minimale** sont définies sur **Windows 10, version 1903**.  Si vous ciblez également HoloLens (1er gen) ou les casques de bureau Windows Mixed Reality, vous pouvez définir **version minimale** à **Windows 10, version 1809** au lieu de cela, bien que cela nécessite certaines <a href="https://docs.microsoft.com/windows/uwp/debug-test-perf/version-adaptive-code" target="_blank"> vérifications de versions adaptive</a> dans votre code lors de l’utilisation des nouvelles fonctionnalités de HoloLens 2.
   ![Capture d’écran de configuration Windows 10, version 1903 en tant que les versions minimale et cible](images/new-uwp-project.png)<br>
   *Paramètre **Windows 10, version 1903** en tant que les versions minimale et cible*
   >[!IMPORTANT]
   >Si vous ne voyez pas **Windows 10, version 1903** en tant qu’option, vous n’avez pas le dernier Windows 10 SDK installé.  Pour obtenir cette option s’affiche, <a href="https://developer.microsoft.com/en-US/windows/downloads/windows-10-sdk" target="_blank">Installer version 10.0.18362.0 ou ultérieure du SDK Windows 10</a>.

Le modèle génère un projet à l’aide <a href="https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/" target="_blank"> C++/WinRT</a>, une projection de 17 langage C ++ des APIs Windows Runtime qui prend en charge de n’importe quel conformes aux normes C ++ 17 du compilateur.  Le projet montre comment créer un cube verrouillé de world qui a placé deux compteurs de l’utilisateur. L’utilisateur peut [-appui en l’air](gestures.md#air-tap) ou appuyez sur un bouton sur le contrôleur pour placer le cube dans un autre emplacement spécifié par l’utilisateur [les regards](gaze.md). Vous pouvez modifier ce projet pour créer n’importe quelle application de réalité mixte.

Vous pouvez également créer un projet à l’aide du **Visual C#**  modèle de projet HOLOGRAPHIQUE, ce qui est basée sur SharpDX.  Si votre HOLOGRAPHIQUE C# projet n’a pas démarré à partir du modèle d’application Windows HOLOGRAPHIQUE, vous devez copier le fichier ms.fxcompile.targets à partir d’un Windows Mixed Reality C# modèle de projet et les importer dans votre fichier .csproj fichier afin de compiler HLSL fichiers que vous ajoutez à votre projet.

Révision [à l’aide de Visual Studio pour déployer et déboguer](using-visual-studio.md) pour plus d’informations sur la façon de générer et déployer l’exemple sur votre HoloLens, PC avec immersive appareil attaché ou un émulateur.

Le reste des instructions ci-dessous suppose que vous utilisez C++ pour générer votre application.

### <a name="uwp-app-entry-point"></a>Point d’entrée application UWP

Votre application UWP HOLOGRAPHIQUE démarre dans le **wWinMain** dans AppView.cpp (fonction). Le **wWinMain** fonction crée l’application <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview" target="_blank">IFrameworkView</a> et démarre la <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication" target="_blank">CoreApplication</a> avec lui.

À partir de **AppView.cpp**:

```cpp
// The main function bootstraps into the IFrameworkView.
int __stdcall wWinMain(HINSTANCE, HINSTANCE, PWSTR, int)
{
    winrt::init_apartment();
    CoreApplication::Run(AppViewSource());
    return 0;
}
```

À ce stade, la classe AppView gère l’interaction avec les événements d’entrée base Windows, les événements de CoreWindow et messagerie et ainsi de suite. Il crée également le HolographicSpace utilisé par votre application.

## <a name="creating-a-win32-project"></a>Création d’un projet Win32

Le moyen le plus simple pour commencer à créer un Win32 HOLOGRAPHIQUE projet consiste à adapter le <a href="https://github.com/Microsoft/Windows-classic-samples/tree/master/Samples/BasicHologram" target="_blank"> *BasicHologram* Win32, exemple</a>.

Cet exemple Win32 utilise <a href="https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/" target="_blank"> C++/WinRT</a>, une projection de 17 langage C ++ des APIs Windows Runtime qui prend en charge de n’importe quel conformes aux normes C ++ 17 du compilateur.  Le projet montre comment créer un cube verrouillé de world qui a placé deux compteurs de l’utilisateur. L’utilisateur peut appuyer sur un bouton sur le contrôleur pour placer le cube dans un autre emplacement spécifié par l’utilisateur [les regards](gaze.md). Vous pouvez modifier ce projet pour créer n’importe quelle application de réalité mixte.

### <a name="win32-app-entry-point"></a>Point d’entrée application Win32

Votre application Win32 HOLOGRAPHIQUE démarre dans le **wWinMain** dans AppMain.cpp (fonction). Le **wWinMain** fonction crée le HWND de l’application et commence sa boucle de message.

À partir de **AppMain.cpp**:

```cpp
int APIENTRY wWinMain(
    _In_     HINSTANCE hInstance,
    _In_opt_ HINSTANCE hPrevInstance,
    _In_     LPWSTR    lpCmdLine,
    _In_     int       nCmdShow)
{
    UNREFERENCED_PARAMETER(hPrevInstance);
    UNREFERENCED_PARAMETER(lpCmdLine);

    winrt::init_apartment();

    App app;

    // Initialize global strings, and perform application initialization.
    app.Initialize(hInstance);

    // Create the HWND and the HolographicSpace.
    app.CreateWindowAndHolographicSpace(hInstance, nCmdShow);

    // Main message loop:
    app.Run(hInstance);

    // Perform application teardown.
    app.Uninitialize();

    return 0;
}
```

À ce stade, la classe AppMain gère l’interaction avec les messages de fenêtre de base et ainsi de suite. Il crée également le HolographicSpace utilisé par votre application.

## <a name="render-holographic-content"></a>Afficher le contenu HOLOGRAPHIQUE

Le projet **contenu** dossier contient des classes pour hologrammes de rendu dans le [espace HOLOGRAPHIQUE](getting-a-holographicspace.md). L’hologramme par défaut dans le modèle est un cube en rotation qui a placé deux mètres de l’utilisateur. Dessin de ce cube est implémenté dans **SpinningCubeRenderer.cpp**, qui a ces méthodes clés :

|  Méthode  |  Explication | 
|----------|----------|
|  `CreateDeviceDependentResources` |  Charge les nuanceurs et crée le maillage de cube. | 
|  `PositionHologram` |  Place l’hologramme à l’emplacement spécifié par le <a href="https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerpose" target="_blank">SpatialPointerPose</a>. | 
|  `Update` |  Fait pivoter le cube et définit la matrice de modèle. | 
|  `Render` |  Affiche un frame à l’aide des nuanceurs de sommets et de pixels. | 

Le **nuanceurs** sous-dossier contient quatre implémentations de nuanceur par défaut :

|  Nuanceur  |  Explication | 
|----------|----------|
|  `GeometryShader.hlsl` |  Directe qui laisse la géométrie tels quels. | 
|  `PixelShader.hlsl` |  Traverse les données de couleur. Les données de couleur sont interpolées et assignées à un pixel à l’étape de rastérisation. | 
|  `VertexShader.hlsl` |  Nuanceur simple pour le traitement du sommet sur le GPU. | 
|  `VPRTVertexShader.hlsl` |  Nuanceur simple pour le traitement du sommet sur le GPU, qui est optimisé pour le rendu stéréo Windows Mixed Reality. | 

`VertexShaderShared.hlsl` contient du code commun partagé entre `VertexShader.hlsl` et `VPRTVertexShader.hlsl`.

Les nuanceurs sont compilés lorsque le projet est généré, et elles sont chargées dans le **SpinningCubeRenderer::CreateDeviceDependentResources** (méthode).

## <a name="interact-with-your-holograms"></a>Interagir avec votre hologrammes

L’entrée d’utilisateur est traitée dans le **SpatialInputHandler** classe, qui est un <a href="https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionmanager" target="_blank">SpatialInteractionManager</a> de l’instance et s’abonne à la <a href="https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed" target="_blank">SourcePressed</a> événement. Cela permet de détecter le mouvement d’appui en l’air et autres événements d’entrée spatiales.

## <a name="update-holographic-content"></a>Mettre à jour de contenu HOLOGRAPHIQUE

Vos mises à jour des applications de réalité mixte dans une boucle de jeu, qui par défaut est implémentée dans le **mise à jour** méthode dans `AppMain.cpp`. Le **mise à jour** méthode met à jour des objets de scène, telles que le cube en rotation et retourne un <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> objet qui est utilisé pour obtenir des matrices de projection et d’affichage à jour et de présenter la chaîne de permutation.

Le **restituer** méthode dans `AppMain.cpp` prend le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> et affiche le frame actuel pour chaque caméra HOLOGRAPHIQUE, en fonction de l’application actuelle et l’état de positionnement spatial.

## <a name="see-also"></a>Voir aussi
* [Obtention d’un HolographicSpace](getting-a-holographicspace.md)
* <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspaceh" target="_blank">HolographicSpace</a>
* [Rendu dans DirectX](rendering-in-directx.md)
* [Utilisation de Visual Studio pour le déploiement et le débogage](using-visual-studio.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Utilisation de code XAML avec les applications DirectX holographiques](using-xaml-with-holographic-directx-apps.md)
