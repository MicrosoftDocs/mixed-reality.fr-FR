---
title: Implémenter des lanceurs d’applications 3D (applications Win32)
description: Comment créer des lanceurs d’applications 3D et les logos des applications de réalité virtuelle Win32 et des jeux (distribuées en dehors de vapeur) par conséquent, ils apparaissent dans l’environnement de menu et accueil Démarrer de réalité mixte Windows.
author: thmignon
ms.author: thmignon
ms.date: 07/12/2018
ms.topic: article
keywords: 3D, logo, icône, modélisation, Lanceur, Lanceur 3D, vignette, cube en direct, win32
ms.openlocfilehash: ac3d5e17614bcd1072f6843a46bf0525f441f130
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594649"
---
# <a name="implement-3d-app-launchers-win32-apps"></a><span data-ttu-id="4fb3b-104">Implémenter des lanceurs d’applications 3D (applications Win32)</span><span class="sxs-lookup"><span data-stu-id="4fb3b-104">Implement 3D app launchers (Win32 apps)</span></span>

> [!NOTE]
> <span data-ttu-id="4fb3b-105">Cette fonctionnalité est uniquement disponible pour PC qui exécutent la dernière version [Windows Insider](https://insider.windows.com) vols (RS5), génération 17704 et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-105">This feature is only available to PCs running the latest [Windows Insider](https://insider.windows.com) flights (RS5), build 17704 and newer.</span></span>

<span data-ttu-id="4fb3b-106">Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs arrivent avant de lancer des applications.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-106">The [Windows Mixed Reality home](navigating-the-windows-mixed-reality-home.md) is the starting point where users land before launching applications.</span></span> <span data-ttu-id="4fb3b-107">Par défaut, les applications Win32 VR IMMERSIFS et des jeux ont d’être lancé depuis le casque à l’extérieur et n’apparaîtront pas dans la liste « Toutes les applications » dans le menu Démarrer de réalité mixte Windows.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-107">By default, immersive Win32 VR apps and games have to be launched from outside the headset and won't appear in the "All apps" list on the Windows Mixed Reality Start menu.</span></span> <span data-ttu-id="4fb3b-108">Toutefois, en suivant les instructions de cet article pour implémenter un lanceur d’applications 3D, votre expérience d’immersion Win32 VR peut être lancé depuis dans le menu Démarrer de réalité mixte Windows et un environnement domestique.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-108">However, by following the instructions in this article to implement a 3D app launcher, your immersive Win32 VR experience can be launched from within the Windows Mixed Reality Start menu and home environment.</span></span>

<span data-ttu-id="4fb3b-109">Cela vaut uniquement pour distributied d’expériences Win32 VR immersive en dehors du flux.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-109">This is only true for immersive Win32 VR experiences distributied outside of Steam.</span></span> <span data-ttu-id="4fb3b-110">Pour des expériences de VR [distribués via Steam](updating-your-steamvr-application-for-windows-mixed-reality.md), nous avons [mis à jour de la réalité mixte Windows pour la version bêta de SteamVR](https://steamcommunity.com/games/719950/announcements/detail/1687045485866139800) , ainsi que la dernière RS5 de Insider de Windows vols afin que SteamVR titres show inscrire dans le Windows Menu Démarrer de réalité mixte dans la liste « Toutes les applications » automatiquement en utilisant un lanceur par défaut.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-110">For VR experiences [distributed through Steam](updating-your-steamvr-application-for-windows-mixed-reality.md), we've [updated the Windows Mixed Reality for SteamVR Beta](https://steamcommunity.com/games/719950/announcements/detail/1687045485866139800) along with the latest Windows Insider RS5 flights so that SteamVR titles show up in the Windows Mixed Reality Start menu in the "All apps" list automatically using a default launcher.</span></span> <span data-ttu-id="4fb3b-111">En d’autres termes, la méthode décrite dans cet article n’est pas nécessaire pour les titres SteamVR et sera remplacée par la réalité mixte Windows pour les fonctionnalités de la version SteamVR bêta.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-111">In other words, the method described in this article is unnecessary for SteamVR titles and will be overridden by the Windows Mixed Reality for SteamVR Beta functionality.</span></span>

## <a name="3d-app-launcher-creation-process"></a><span data-ttu-id="4fb3b-112">Processus de création de lanceur application 3D</span><span class="sxs-lookup"><span data-stu-id="4fb3b-112">3D app launcher creation process</span></span>

<span data-ttu-id="4fb3b-113">Il existe 3 étapes à la création d’un lanceur d’applications 3D :</span><span class="sxs-lookup"><span data-stu-id="4fb3b-113">There are 3 steps to creating a 3D app launcher:</span></span>
1. [<span data-ttu-id="4fb3b-114">Conception et concepting</span><span class="sxs-lookup"><span data-stu-id="4fb3b-114">Designing and concepting</span></span>](3d-app-launcher-design-guidance.md)
2. [<span data-ttu-id="4fb3b-115">Modélisation et l’exportation</span><span class="sxs-lookup"><span data-stu-id="4fb3b-115">Modeling and exporting</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. <span data-ttu-id="4fb3b-116">L’intégration dans votre application (cet article)</span><span class="sxs-lookup"><span data-stu-id="4fb3b-116">Integrating it into your application (this article)</span></span>

<span data-ttu-id="4fb3b-117">Composants 3D à utiliser comme lanceurs pour votre application doivent être créés à l’aide de la [recommandations sur la programmation de Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) pour assurer la compatibilité.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-117">3D assets to be used as launchers for your application should be authored using the [Windows Mixed Reality authoring guidelines](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) to ensure compatibility.</span></span> <span data-ttu-id="4fb3b-118">Actifs qui ne parviennent pas à répondre à cette spécification création seront affichera pas dans la réalité mixte Windows domestique.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-118">Assets that fail to meet this authoring specification will not be rendered in the Windows Mixed Reality home.</span></span>

## <a name="configuring-the-3d-launcher"></a><span data-ttu-id="4fb3b-119">Configuration du Lanceur 3D</span><span class="sxs-lookup"><span data-stu-id="4fb3b-119">Configuring the 3D launcher</span></span>

<span data-ttu-id="4fb3b-120">Les applications Win32 seront affiche dans la liste « Toutes les applications » dans le menu Démarrer de réalité mixte Windows si vous créez un lanceur d’applications 3D pour eux.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-120">Win32 applications will appear in the "All apps" list on the Windows Mixed Reality Start menu if you create a 3D app launcher for them.</span></span> <span data-ttu-id="4fb3b-121">Pour ce faire, créez un [éléments Visual manifeste](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) fichier XML référençant le Lanceur d’applications 3D en suivant ces étapes :</span><span class="sxs-lookup"><span data-stu-id="4fb3b-121">To do that, create a [Visual Elements Manifest](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) XML file referencing the 3D App Launcher by following these steps:</span></span>

1. <span data-ttu-id="4fb3b-122">Créer un **fichier GLB de ressource de lanceur d’applications 3D** (consultez [modélisation et d’exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)).</span><span class="sxs-lookup"><span data-stu-id="4fb3b-122">Create a **3D App Launcher asset GLB file** (See [Modeling and exporting](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)).</span></span>
2. <span data-ttu-id="4fb3b-123">Créer un **[éléments Visual manifeste](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx)** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-123">Create a **[Visual Elements Manifest](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx)** for your application.</span></span>
    1. <span data-ttu-id="4fb3b-124">Vous pouvez démarrer avec la [exemple ci-dessous](#sample-visual-elements-manifest).</span><span class="sxs-lookup"><span data-stu-id="4fb3b-124">You can start with the [sample below](#sample-visual-elements-manifest).</span></span>  <span data-ttu-id="4fb3b-125">Afficher la version complète [éléments Visual manifeste](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) documentation pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-125">See the full [Visual Elements Manifest](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) documentation for more details.</span></span>
    2. <span data-ttu-id="4fb3b-126">Mise à jour **Square150x150Logo** et **Square70x70Logo** avec une PNG/JPG/GIF pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-126">Update **Square150x150Logo** and **Square70x70Logo** with a PNG/JPG/GIF for your app.</span></span>
        * <span data-ttu-id="4fb3b-127">Il seront utilisés pour le logo 2D de l’application dans la liste Windows toutes les applications de réalité mixte et le Menu Démarrer sur le bureau.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-127">These will be used for the app’s 2D logo in the Windows Mixed Reality All Apps list and for the Start Menu on desktop.</span></span>
        * <span data-ttu-id="4fb3b-128">Le chemin d’accès de fichier est relatif au dossier contenant les éléments de manifeste Visual.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-128">The file path is relative to the folder containing the Visual Elements Manifest.</span></span>
        * <span data-ttu-id="4fb3b-129">Vous devez toujours fournir un icône de Menu Démarrer du bureau pour votre application via des mécanismes standard.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-129">You still need to provide a desktop Start Menu icon for your app through the standard mechanisms.</span></span> <span data-ttu-id="4fb3b-130">Il peut s’agir directement dans le fichier exécutable ou dans le raccourci que vous créez (par exemple, via IShellLink::SetIconLocation).</span><span class="sxs-lookup"><span data-stu-id="4fb3b-130">This can either be directly in the executable or in the shortcut you create (e.g. via IShellLink::SetIconLocation).</span></span>
        * <span data-ttu-id="4fb3b-131">*Facultatif :* Vous pouvez utiliser un fichier resources.pri si vous souhaitez que MRT fournir plusieurs tailles de ressource pour les échelles différentes résolutions et des thèmes à contraste élevé.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-131">*Optional:* You can use a resources.pri file if you would like for MRT to provide multiple asset sizes for different resolution scales and high contrast themes.</span></span>
    3. <span data-ttu-id="4fb3b-132">Mise à jour le **chemin d’accès MixedRealityModel** pour pointer vers le GLB pour votre Lanceur d’applications 3D</span><span class="sxs-lookup"><span data-stu-id="4fb3b-132">Update the **MixedRealityModel Path** to point to the GLB for your 3D App Launcher</span></span>
    4. <span data-ttu-id="4fb3b-133">Enregistrez le fichier avec le même nom que votre fichier exécutable, avec l’extension ». VisualElementsManifest.xml » et l’enregistrer dans le même répertoire.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-133">Save the file with the same name as your executable file, with an extension of ".VisualElementsManifest.xml" and save it in the same directory.</span></span> <span data-ttu-id="4fb3b-134">Par exemple, pour le fichier exécutable « contoso.exe », le fichier XML qui accompagne cet article est nommé « contoso.visualelementsmanifest.xml ».</span><span class="sxs-lookup"><span data-stu-id="4fb3b-134">For example, for the executable file "contoso.exe", the accompanying XML file is named "contoso.visualelementsmanifest.xml".</span></span>
3. <span data-ttu-id="4fb3b-135">**Ajouter un raccourci** à votre application pour le Menu Démarrer du bureau Windows.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-135">**Add a shortcut** to your application to the desktop Windows Start Menu.</span></span> <span data-ttu-id="4fb3b-136">Consultez le [exemple ci-dessous](#sample-app-launcher-shortcut-creation) pour obtenir un exemple C++ implémentation.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-136">See the [sample below](#sample-app-launcher-shortcut-creation) for an example C++ implementation.</span></span> 
    * <span data-ttu-id="4fb3b-137">Créez %ALLUSERSPROFILE%\Microsoft\Windows\Start Menu\Programs (ordinateur) ou %APPDATA%\Microsoft\Windows\Start Menu\Programs (utilisateur)</span><span class="sxs-lookup"><span data-stu-id="4fb3b-137">Create it in %ALLUSERSPROFILE%\Microsoft\Windows\Start Menu\Programs (machine) or %APPDATA%\Microsoft\Windows\Start Menu\Programs (user)</span></span>
    * <span data-ttu-id="4fb3b-138">Si une mise à jour modifie votre manifeste d’éléments visuels ou les ressources qu’il référencés, la mise à jour ou le programme d’installation doit mettre à jour le raccourci telles que le manifeste est réanalysé et ressources mises en cache sont mises à jour.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-138">If an update changes your visual elements manifest or the assets referenced by it, the updater or installer should update the shortcut such that the manifest is reparsed and cached assets are updated.</span></span>
4. <span data-ttu-id="4fb3b-139">*Facultatif :* Si votre raccourci du bureau ne désigne pas directement EXE de votre application (par exemple, si elle appelle un gestionnaire de protocole personnalisé comme « myapp : / / »), le Menu Démarrer ne trouvera automatiquement le fichier l’application VisualElementsManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-139">*Optional:* If your desktop shortcut does not point directly to your application’s EXE (e.g., if it invokes a custom protocol handler like “myapp://”), the Start Menu won’t automatically find the app’s VisualElementsManifest.xml file.</span></span> <span data-ttu-id="4fb3b-140">Pour résoudre ce problème, le raccourci doit spécifier le chemin d’accès de fichier du manifeste d’éléments visuel à l’aide de System.AppUserModel.VisualElementsManifestHintPath ().</span><span class="sxs-lookup"><span data-stu-id="4fb3b-140">To resolve this, the shortcut should specify the file path of the Visual Elements Manifest using System.AppUserModel.VisualElementsManifestHintPath ().</span></span> <span data-ttu-id="4fb3b-141">Cela peut être défini dans le raccourci à l’aide des mêmes techniques comme System.AppUserModel.ID.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-141">This can be set in the shortcut using the same techniques as System.AppUserModel.ID.</span></span> <span data-ttu-id="4fb3b-142">Vous n’êtes pas obligé d’utiliser System.AppUserModel.ID, mais vous pouvez le faire si vous le souhaitez pour le raccourci faire correspondre l’ID de modèle d’Application utilisateur explicite de l’application si elle est utilisée.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-142">You are not required to use System.AppUserModel.ID but you may do so if you wish for the shortcut to match the explicit Application User Model ID of the application if one is used.</span></span>  <span data-ttu-id="4fb3b-143">Consultez le [exemple de création d’un raccourci application Lanceur](#sample-app-launcher-shortcut-creation) section ci-dessous pour un C++ exemple.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-143">See the [sample app launcher shortcut creation](#sample-app-launcher-shortcut-creation) section below for a C++ sample.</span></span>

### <a name="sample-visual-elements-manifest"></a><span data-ttu-id="4fb3b-144">Exemple de fichier manifeste éléments visuels</span><span class="sxs-lookup"><span data-stu-id="4fb3b-144">Sample Visual Elements Manifest</span></span>

```xml
<Application xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <VisualElements
    ShowNameOnSquare150x150Logo="on"
    Square150x150Logo="YOUR_APP_LOGO_150X150.png"
    Square70x70Logo=" YOUR_APP_LOGO_70X70.png"
    ForegroundText="light"
    BackgroundColor="#000000">
    <MixedRealityModel Path="YOUR_3D_APP_LAUNCHER_ASSET.glb">
        <SpatialBoundingBox Center="0,0,0" Extents="Auto" />
    </MixedRealityModel>
  </VisualElements>
</Application>
```

### <a name="sample-app-launcher-shortcut-creation"></a><span data-ttu-id="4fb3b-145">Création d’un raccourci du Lanceur application exemple</span><span class="sxs-lookup"><span data-stu-id="4fb3b-145">Sample app launcher shortcut creation</span></span>

<span data-ttu-id="4fb3b-146">L’exemple de code ci-dessous montre comment vous pouvez créer un raccourci dans C++, y compris la substitution le chemin d’accès au fichier XML de manifeste Visual des éléments.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-146">The sample code below shows how you can create a shortcut in C++, including overriding the path to the Visual Elements Manifest XML file.</span></span> <span data-ttu-id="4fb3b-147">Notez que le remplacement est nécessaire uniquement dans les cas où votre raccourci ne pointe pas directement au fichier .exe associé au manifeste (par ex.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-147">Note the override is only required in cases where your shortcut does not point directly to the EXE associated with the manifest (eg.</span></span> <span data-ttu-id="4fb3b-148">votre raccourci utilise un gestionnaire de protocole personnalisé comme « myapp : / / »).</span><span class="sxs-lookup"><span data-stu-id="4fb3b-148">your shortcut uses a custom protocol handler like "myapp://").</span></span>

#### <a name="sample-lnk-shortcut-creation-c"></a><span data-ttu-id="4fb3b-149">Exemple. Création d’un raccourci LNK (C++)</span><span class="sxs-lookup"><span data-stu-id="4fb3b-149">Sample .LNK shortcut creation (C++)</span></span>

```cpp
#include <windows.h>
#include <propkey.h>
#include <shlobj_core.h>
#include <shlwapi.h>
#include <propvarutil.h>
#include <wrl.h>

#include <memory>

using namespace Microsoft::WRL;

#define RETURN_IF_FAILED(x) do { HRESULT hr = x; if (FAILED(hr)) { return hr; } } while(0)
#define RETURN_IF_WIN32_BOOL_FALSE(x) do { DWORD res = x; if (res == 0) { return HRESULT_FROM_WIN32(GetLastError()); } } while(0)

int wmain()
{
    RETURN_IF_FAILED(CoInitializeEx(nullptr, COINIT_APARTMENTTHREADED));

    ComPtr<IShellLink> shellLink;
    RETURN_IF_FAILED(CoCreateInstance(__uuidof(ShellLink), nullptr, CLSCTX_INPROC_SERVER, IID_PPV_ARGS(&shellLink)));
    RETURN_IF_FAILED(shellLink->SetPath(L"MyLauncher://launch/app-identifier"));

    // It is also possible to use an icon file in another location. For example, "C:\Program Files (x86)\MyLauncher\assets\app-identifier.ico".
    RETURN_IF_FAILED(shellLink->SetIconLocation(L"C:\\Program Files (x86)\\MyLauncher\\apps\\app-identifier\\game.exe", 0 /*iIcon*/));

    ComPtr<IPropertyStore> propStore;
    RETURN_IF_FAILED(shellLink.As(&propStore));

    {
        // Optional: If the application has an explict Application User Model ID, then you should usually specify it in the shortcut.
        PROPVARIANT propVar;
        RETURN_IF_FAILED(InitPropVariantFromString(L"ExplicitAppUserModelID", &propVar));
        RETURN_IF_FAILED(propStore->SetValue(PKEY_AppUserModel_ID, propVar));
        PropVariantClear(&propVar);
    }

    {
        // A hint path to the manifest is only necessary if the target path of the shortcut is not a file path to the executable.
        // By convention the manifest is named <executable name>.VisualElementsManifest.xml and is in the same folder as the executable
        // (and resources.pri if applicable). Assets referenced by the manifest are relative to the folder containing the manifest.

        //
        // PropKey.h
        //
        //  Name:     System.AppUserModel.VisualElementsManifestHintPath -- PKEY_AppUserModel_VisualElementsManifestHintPath
        //  Type:     String -- VT_LPWSTR  (For variants: VT_BSTR)
        //  FormatID: {9F4C2855-9F79-4B39-A8D0-E1D42DE1D5F3}, 31
        //  
        //  Suggests where to look for the VisualElementsManifest for a Win32 app
        //
        // DEFINE_PROPERTYKEY(PKEY_AppUserModel_VisualElementsManifestHintPath, 0x9F4C2855, 0x9F79, 0x4B39, 0xA8, 0xD0, 0xE1, 0xD4, 0x2D, 0xE1, 0xD5, 0xF3, 31);
        // #define INIT_PKEY_AppUserModel_VisualElementsManifestHintPath { { 0x9F4C2855, 0x9F79, 0x4B39, 0xA8, 0xD0, 0xE1, 0xD4, 0x2D, 0xE1, 0xD5, 0xF3 }, 31 }

        PROPVARIANT propVar;
        RETURN_IF_FAILED(InitPropVariantFromString(L"C:\\Program Files (x86)\\MyLauncher\\apps\\app-identifier\\game.visualelementsmanifest.xml", &propVar));
        RETURN_IF_FAILED(propStore->SetValue(PKEY_AppUserModel_VisualElementsManifestHintPath, propVar));
        PropVariantClear(&propVar);
    }

    constexpr PCWSTR shortcutPath = L"%APPDATA%\\Microsoft\\Windows\\Start Menu\\Programs\\game.lnk";
    const DWORD requiredBufferLength = ExpandEnvironmentStrings(shortcutPath, nullptr, 0);
    RETURN_IF_WIN32_BOOL_FALSE(requiredBufferLength);

    const auto expandedShortcutPath = std::make_unique<wchar_t[]>(requiredBufferLength);
    RETURN_IF_WIN32_BOOL_FALSE(ExpandEnvironmentStrings(shortcutPath, expandedShortcutPath.get(), requiredBufferLength));

    ComPtr<IPersistFile> persistFile;
    RETURN_IF_FAILED(shellLink.As(&persistFile));
    RETURN_IF_FAILED(persistFile->Save(expandedShortcutPath.get(), FALSE));

    return 0;
}
```

#### <a name="sample-url-launcher-shortcut"></a><span data-ttu-id="4fb3b-150">Exemple. Raccourci du Lanceur d’URL</span><span class="sxs-lookup"><span data-stu-id="4fb3b-150">Sample .URL launcher shortcut</span></span> 

```
[{9F4C2855-9F79-4B39-A8D0-E1D42DE1D5F3}]
Prop31=C:\Program Files (x86)\MyLauncher\apps\app-identifier\game.visualelementsmanifest.xml
Prop5=ExplicitAppUserModelID

[{000214A0-0000-0000-C000-000000000046}]
Prop3=19,0

[InternetShortcut]
IDList=
URL=MyLauncher://launch/app-identifier
IconFile=C:\Program Files (x86)\MyLauncher\apps\app-identifier\game.exe
IconIndex=0
```

## <a name="see-also"></a><span data-ttu-id="4fb3b-151">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4fb3b-151">See also</span></span>

* <span data-ttu-id="4fb3b-152">[Exemple de modèle de réalité mixte](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) contenant un lanceur d’applications 3D.</span><span class="sxs-lookup"><span data-stu-id="4fb3b-152">[Mixed reality model sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) containing a 3D app launcher.</span></span>
* [<span data-ttu-id="4fb3b-153">Guide de conception du Lanceur d’application 3D</span><span class="sxs-lookup"><span data-stu-id="4fb3b-153">3D app launcher design guidance</span></span>](3d-app-launcher-design-guidance.md)
* [<span data-ttu-id="4fb3b-154">Création de modèles 3D pour une utilisation dans la page d’accueil Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="4fb3b-154">Creating 3D models for use in the Windows Mixed Reality home</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [<span data-ttu-id="4fb3b-155">Implémentation des lanceurs d’applications 3D (applications UWP)</span><span class="sxs-lookup"><span data-stu-id="4fb3b-155">Implementing 3D app launchers (UWP apps)</span></span>](implementing-3d-app-launchers.md)
* [<span data-ttu-id="4fb3b-156">Navigation dans Windows Mixed Reality domestique</span><span class="sxs-lookup"><span data-stu-id="4fb3b-156">Navigating the Windows Mixed Reality home</span></span>](navigating-the-windows-mixed-reality-home.md)
