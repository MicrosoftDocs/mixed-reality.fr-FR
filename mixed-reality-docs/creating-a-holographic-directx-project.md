---
title: Création d’un projet DirectX holographique
description: Explique comment créer une application holographique basée sur le modèle application Windows Mixed Reality.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, application holographique, nouvelle application, application UWP, modèle App, hologrammes, nouveau projet, procédure pas à pas, téléchargement, exemple de code
ms.openlocfilehash: d99478a0d98d0593b7b82f25080d20913789cb6c
ms.sourcegitcommit: f4812e1312c4751a22a2de56771c475b22a4ba24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/09/2019
ms.locfileid: "74940843"
---
# <a name="creating-a-holographic-directx-project"></a>Création d’un projet DirectX holographique

Une application holographique que vous créez pour un HoloLens sera une <a href="https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide" target="_blank">application plateforme Windows universelle (UWP)</a>.  Si vous ciblez des casques Windows mixtes de la réalité du bureau, vous pouvez créer une application UWP ou une application Win32.

Le modèle application UWP holographique DirectX 11 ressemble davantage au modèle d’application UWP DirectX 11. Il comprend une boucle de programme (ou « boucle de jeu »), une classe **DeviceResources** pour gérer le périphérique et le contexte Direct3D et une classe de convertisseur de contenu simplifiée. Il possède également un <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview" target="_blank">IFrameworkView</a>, comme n’importe quelle autre application UWP.

Toutefois, l’application de réalité mixte possède des fonctionnalités supplémentaires qui ne sont pas présentes dans une application standard Direct3D UWP. Le modèle d’application Windows Mixed Reality est capable d’effectuer les opérations suivantes :
* Gérer les ressources d’appareil Direct3D associées aux appareils photo holographiques.
* Récupérez les mémoires tampons d’arrière-plan de l’appareil photo, ou (dans le cas de directement Direct3D 12) Créez des ressources de mémoire tampon d’arrière-plan holographique et gérez les durées de vie des ressources.
* Gérer les entrées de [regard](gaze-and-commit.md) et reconnaître un [mouvement](gaze-and-commit.md#composite-gestures)simple.
* Passez en mode de rendu stéréo plein écran.

## <a name="how-do-i-get-started"></a>Comment démarrer ?

Installez d’abord [les outils](install-the-tools.md)en suivant les instructions de téléchargement de Visual Studio 2019 et des modèles d’application Windows Mixed Reality. Les modèles d’application de réalité mixte sont disponibles sur la place de marché Visual Studio en tant que [téléchargement Web](https://marketplace.visualstudio.com/items?itemName=WindowsMixedRealityteam.WindowsMixedRealityAppTemplatesVSIX), ou en les installant en tant qu’extension par le biais de l’interface utilisateur de Visual Studio.

Vous êtes maintenant prêt à créer votre application DirectX 11 Windows Mixed Reality ! Remarque : pour supprimer l’exemple de contenu, commentez la directive de préprocesseur **DRAW_SAMPLE_CONTENT** dans *pch. h*.

## <a name="creating-a-uwp-project"></a>Création d’un projet UWP

Une fois les [Outils installés](install-the-tools.md) , vous pouvez créer un projet holographique DirectX UWP.

Pour créer un nouveau projet dans Visual Studio 2019 :
1. Démarrez **Visual Studio**.
2. Dans la section **prise en main** sur la droite, sélectionnez **créer un nouveau projet**.
3. Dans les menus déroulants de la boîte de dialogue **créer un nouveau projet** , sélectionnez **C++** **Windows Mixed Reality**et **UWP**.
4. Sélectionnez **application holographique DirectX 11 (Windows universel) (C++/WinRT)** .
   Capture d’écran ![du modèle de C++projet d’application UWP DirectX 11/WinRT dans Visual Studio 2019](images/holographic-directx-app-cpp-new-project-2019.png)<br>
   *Modèle de projet C++application UWP DirectX 11/WinRT holographique dans Visual Studio 2019*
   >[!IMPORTANT]
   >Assurez-vous que le nom du modèle de projetC++comprend « (/WinRT) ».  Si ce n’est pas le cas, une version antérieure des modèles de projet holographique est installée.  Pour accéder aux derniers modèles de projet, [Installez-les](install-the-tools.md) en tant qu’extension de Visual Studio 2019.
5. Cliquez sur **Suivant**.
5. Renseignez les zones de texte **nom du projet** et **emplacement** , puis cliquez ou appuyez sur **créer**. Le projet d’application holographique est créé.
6. Pour le développement ciblant uniquement HoloLens 2, assurez-vous que la version **cible** et la **version minimale** sont définies sur **Windows 10, version 1903**.  Si vous ciblez également des casques HoloLens (1er génération) ou de bureau Windows Mixed Reality, vous pouvez définir la **version minimale** sur **Windows 10, version 1809** , mais cela nécessitera des <a href="https://docs.microsoft.com/windows/uwp/debug-test-perf/version-adaptive-code" target="_blank">vérifications adaptatives de version</a> dans votre code lors de l’utilisation des nouvelles fonctionnalités de HoloLens 2.
   ![capture d’écran de la configuration de Windows 10, version 1903 en tant que versions cible et minimale](images/new-uwp-project.png)<br>
   *Définition de **Windows 10, version 1903 comme version** cible et minimale*
   >[!IMPORTANT]
   >Si vous ne voyez pas **Windows 10, version 1903** , vous n’avez pas le dernier Kit de développement logiciel (SDK) Windows 10 installé.  Pour que cette option s’affiche, <a href="https://developer.microsoft.com/windows/downloads/windows-10-sdk" target="_blank">Installez la version 10.0.18362.0 ou ultérieure du kit de développement logiciel (SDK) Windows 10</a>.

Pour créer un nouveau projet dans Visual Studio 2017 :
1. Démarrez **Visual Studio**.
2. Dans le menu **fichier** , pointez sur **nouveau** , puis sélectionnez **projet** dans le menu contextuel. La boîte **de dialogue Nouveau projet** s’ouvre.
3. Développez **installé** sur la gauche, puis développez le nœud de langage **visuel C++**  .
4. Accédez au nœud **Windows Universal > holographique** et sélectionnez **application holographique DirectX 11 (Windows universel) (C++/WinRT)** .
   Capture d’écran ![du modèle de C++projet d’application UWP DirectX 11/WinRT dans Visual Studio 2017](images/holographic-directx-app-cpp-new-project.png)<br>
   *Modèle de projet C++application UWP DirectX 11/WinRT holographique dans Visual Studio 2017*
   >[!IMPORTANT]
   >Assurez-vous que le nom du modèle de projetC++comprend « (/WinRT) ».  Si ce n’est pas le cas, une version antérieure des modèles de projet holographique est installée.  Pour accéder aux derniers modèles de projet, [Installez-les](install-the-tools.md) en tant qu’extension de Visual Studio 2017.
5. Renseignez les zones de texte **nom** et **emplacement** , puis cliquez ou appuyez sur **OK**. Le projet d’application holographique est créé.
6. Pour le développement ciblant uniquement HoloLens 2, assurez-vous que la version **cible** et la **version minimale** sont définies sur **Windows 10, version 1903**.  Si vous ciblez également des casques HoloLens (1er génération) ou de bureau Windows Mixed Reality, vous pouvez définir la **version minimale** sur **Windows 10, version 1809** , mais cela nécessitera des <a href="https://docs.microsoft.com/windows/uwp/debug-test-perf/version-adaptive-code" target="_blank">vérifications adaptatives de version</a> dans votre code lors de l’utilisation des nouvelles fonctionnalités de HoloLens 2.
   ![capture d’écran de la configuration de Windows 10, version 1903 en tant que versions cible et minimale](images/new-uwp-project.png)<br>
   *Définition de **Windows 10, version 1903 comme version** cible et minimale*
   >[!IMPORTANT]
   >Si vous ne voyez pas **Windows 10, version 1903** , vous n’avez pas le dernier Kit de développement logiciel (SDK) Windows 10 installé.  Pour que cette option s’affiche, <a href="https://developer.microsoft.com/windows/downloads/windows-10-sdk" target="_blank">Installez la version 10.0.18362.0 ou ultérieure du kit de développement logiciel (SDK) Windows 10</a>.

Le modèle génère un projet à <a href="https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/" target="_blank"> C++</a>l’aide de/WinRT, une projection de langage c++ 17 des API Windows Runtime qui prend en charge tout compilateur c++ 17 conforme aux normes.  Le projet montre comment créer un cube verrouillé à deux mètres de l’utilisateur. L' [utilisateur peut appuyer ou appuyer sur un](gaze-and-commit.md#composite-gestures) bouton du contrôleur pour placer le cube dans un autre emplacement que celui spécifié par le point de [regard](gaze-and-commit.md)de l’utilisateur. Vous pouvez modifier ce projet pour créer une application de réalité mixte.

Vous pouvez également créer un nouveau projet à l’aide du modèle de projet **Visual C#**  holographique, qui est basé sur SharpDX.  Si votre projet C# holographique n’a pas démarré à partir du modèle d’application holographique Windows, vous devez copier le fichier MS. fxcompile. targets à partir d' C# un projet de modèle de réalité mixte Windows et l’importer dans votre fichier. csproj afin de compiler les fichiers HLSL que vous ajoutez à votre projet. Un modèle Direct3D 12 est également fourni dans l’extension des modèles d’application Windows Mixed Reality à Visual Studio.

Consultez [utilisation de Visual Studio pour déployer et déboguer](using-visual-studio.md) pour plus d’informations sur la façon de créer et de déployer l’exemple dans votre HoloLens, votre PC avec un appareil immersif attaché ou un émulateur.

Le reste des instructions ci-dessous suppose que vous utilisez C++ pour générer votre application.

### <a name="uwp-app-entry-point"></a>Point d’entrée de l’application UWP

Votre application UWP holographique démarre dans la fonction **wWinMain** dans AppView. cpp. La fonction **wWinMain** crée le <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkview" target="_blank">IFrameworkView</a> de l’application et démarre le <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplication" target="_blank">CoreApplication</a> avec celle-ci.

À partir de **AppView. cpp**:

```cpp
// The main function bootstraps into the IFrameworkView.
int __stdcall wWinMain(HINSTANCE, HINSTANCE, PWSTR, int)
{
    winrt::init_apartment();
    CoreApplication::Run(AppViewSource());
    return 0;
}
```

À partir de là, la classe AppView gère l’interaction avec les événements d’entrée Windows Basic, les événements CoreWindow et la messagerie, etc. Il créera également le HolographicSpace utilisé par votre application.

## <a name="creating-a-win32-project"></a>Création d’un projet Win32

Le moyen le plus simple de commencer à créer un projet holographique Win32 consiste à adapter l' <a href="https://github.com/Microsoft/Windows-classic-samples/tree/master/Samples/BasicHologram" target="_blank">exemple Win32 *BasicHologram* </a>.

Cet exemple Win32 utilise <a href="https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/" target="_blank"> C++/WinRT</a>, une projection de langage c++ 17 des API Windows Runtime qui prend en charge tout compilateur c++ 17 conforme aux normes.  Le projet montre comment créer un cube verrouillé à deux mètres de l’utilisateur. L’utilisateur peut appuyer sur un bouton du contrôleur pour placer le cube à une position différente spécifiée par le [regard](gaze-and-commit.md)de l’utilisateur. Vous pouvez modifier ce projet pour créer une application de réalité mixte.

### <a name="win32-app-entry-point"></a>Point d’entrée de l’application Win32

Votre application holographique Win32 démarre dans la fonction **wWinMain** dans AppMain. cpp. La fonction **wWinMain** crée le HWND de l’application et démarre sa boucle de messages.

À partir de **AppMain. cpp**:

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

À partir de là, la classe AppMain gère l’interaction avec les messages de fenêtre de base, et ainsi de suite. Il créera également le HolographicSpace utilisé par votre application.

## <a name="render-holographic-content"></a>Afficher le contenu holographique

Le dossier de **contenu** du projet contient des classes pour le rendu des hologrammes dans l' [espace holographique](getting-a-holographicspace.md). L’hologramme par défaut dans le modèle est un cube tournant à deux mètres à l’écart de l’utilisateur. Le dessin de ce cube est implémenté dans **SpinningCubeRenderer. cpp**, qui possède les principales méthodes suivantes :

|  Méthode  |  Explication | 
|----------|----------|
|  `CreateDeviceDependentResources` |  Charge les nuanceurs et crée la maille du cube. | 
|  `PositionHologram` |  Place l’hologramme à l’emplacement spécifié par le <a href="https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerpose" target="_blank">SpatialPointerPose</a>fourni. | 
|  `Update` |  Fait pivoter le cube et définit la matrice du modèle. | 
|  `Render` |  Génère le rendu d’un frame à l’aide des nuanceurs vertex et de pixels. | 

Le sous-dossier **nuanciers** contient quatre implémentations de nuanceur par défaut :

|  Nuance  |  Explication | 
|----------|----------|
|  `GeometryShader.hlsl` |  Un transfert qui laisse la géométrie non modifiée. | 
|  `PixelShader.hlsl` |  Transmet les données de couleur. Les données de couleur sont interpolées et affectées à un pixel à l’étape de pixellisation. | 
|  `VertexShader.hlsl` |  Nuanceur simple pour le traitement des vertex sur le GPU. | 
|  `VPRTVertexShader.hlsl` |  Nuanceur simple pour le traitement des vertex sur le GPU, qui est optimisé pour le rendu stéréo Windows Mixed Reality. | 

`VertexShaderShared.hlsl` contient du code commun partagé entre `VertexShader.hlsl` et `VPRTVertexShader.hlsl`.

Remarque : le modèle d’application Direct3D 12 comprend également `ViewInstancingVertexShader.hlsl`. Cette variante utilise des fonctionnalités facultatives D3D12 pour rendre les images stéréo plus efficaces.

Les nuanceurs sont compilés lorsque le projet est généré et sont chargés dans la méthode **SpinningCubeRenderer :: CreateDeviceDependentResources** .

## <a name="interact-with-your-holograms"></a>Interagissez avec vos hologrammes

L’entrée utilisateur est traitée dans la classe **SpatialInputHandler** , qui obtient une instance <a href="https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionmanager" target="_blank">SpatialInteractionManager</a> et s’abonne à l’événement <a href="https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed" target="_blank">SourcePressed</a> . Cela permet de détecter le mouvement d’appui sur l’air et d’autres événements d’entrée spatiale.

## <a name="update-holographic-content"></a>Mettre à jour le contenu holographique

Votre application de réalité mixte est mise à jour dans une boucle de jeu, qui est implémentée par défaut dans la méthode de **mise à jour** de `AppMain.cpp`. La méthode **Update** met à jour les objets de scène, comme le cube en rotation, et retourne un objet <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> qui est utilisé pour obtenir des matrices de projection et d’affichage à jour et pour présenter la chaîne de permutation.

La méthode **Render** dans `AppMain.cpp` prend le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> et restitue le frame actuel sur chaque caméra holographique, en fonction de l’état actuel de l’application et du positionnement spatial.

## <a name="notes"></a>Notes

Le modèle d’application Windows Mixed Reality prend désormais en charge la compilation avec l’indicateur d’atténuation spectre activé (/Qspectre). Veillez à installer la version spectre-atténuée des bibliothèques Runtime Microsoft C++ Visual (MSVC) avant de compiler une configuration avec l’atténuation spectre activée. Pour installer les C++ bibliothèques atténuées par spectre, lancez le Visual Studio installer et sélectionnez **modifier**. Accédez à **composants individuels** et recherchez « spectre ». Sélectionnez les zones correspondant aux plateformes cibles et à la version MSVC dont vous avez besoin pour compiler le code atténué spectre pour, puis cliquez sur **modifier** pour commencer l’installation.

## <a name="see-also"></a>Articles associés
* [Obtention d’un HolographicSpace](getting-a-holographicspace.md)
* <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspaceh" target="_blank">HolographicSpace</a>
* [Rendu dans DirectX](rendering-in-directx.md)
* [Utilisation de Visual Studio pour le déploiement et le débogage](using-visual-studio.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
* [Utilisation de code XAML avec les applications DirectX holographiques](using-xaml-with-holographic-directx-apps.md)
