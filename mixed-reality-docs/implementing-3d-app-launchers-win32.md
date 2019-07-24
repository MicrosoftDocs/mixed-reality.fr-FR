---
title: Implémenter des lanceurs d’applications en 3D (applications Win32)
description: Comment créer des programmes de lancement et des logos d’applications en 3D pour les jeux et les applications Win32 VR (distribués en dehors de la vapeur) afin qu’ils s’affichent dans le menu Démarrer et l’environnement d’accueil de Windows Mixed Reality.
author: thmignon
ms.author: thmignon
ms.date: 07/12/2018
ms.topic: article
keywords: 3D, logo, icône, modélisation, lanceur, lanceur 3D, vignette, cube actif, Win32
ms.openlocfilehash: ac3d5e17614bcd1072f6843a46bf0525f441f130
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63515606"
---
# <a name="implement-3d-app-launchers-win32-apps"></a><span data-ttu-id="bb7fb-104">Implémenter des lanceurs d’applications en 3D (applications Win32)</span><span class="sxs-lookup"><span data-stu-id="bb7fb-104">Implement 3D app launchers (Win32 apps)</span></span>

> [!NOTE]
> <span data-ttu-id="bb7fb-105">Cette fonctionnalité est uniquement disponible pour les PC qui exécutent les derniers vols de [Windows](https://insider.windows.com) Insider (RS5), Build 17704 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-105">This feature is only available to PCs running the latest [Windows Insider](https://insider.windows.com) flights (RS5), build 17704 and newer.</span></span>

<span data-ttu-id="bb7fb-106">La [base de la réalité Windows Mixed](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs se trouvent avant de lancer des applications.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-106">The [Windows Mixed Reality home](navigating-the-windows-mixed-reality-home.md) is the starting point where users land before launching applications.</span></span> <span data-ttu-id="bb7fb-107">Par défaut, les applications et les jeux Win32 VR Win32 sont lancés à partir de l’extérieur du casque et n’apparaissent pas dans la liste «toutes les applications» dans le menu Démarrer de Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-107">By default, immersive Win32 VR apps and games have to be launched from outside the headset and won't appear in the "All apps" list on the Windows Mixed Reality Start menu.</span></span> <span data-ttu-id="bb7fb-108">Toutefois, en suivant les instructions de cet article pour implémenter un lanceur d’applications 3D, votre expérience Win32 VR peut être lancée à partir du menu Démarrer et de l’environnement d’accueil de Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-108">However, by following the instructions in this article to implement a 3D app launcher, your immersive Win32 VR experience can be launched from within the Windows Mixed Reality Start menu and home environment.</span></span>

<span data-ttu-id="bb7fb-109">Cela est vrai uniquement pour les expériences Win32 VR distributied en dehors de la vapeur.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-109">This is only true for immersive Win32 VR experiences distributied outside of Steam.</span></span> <span data-ttu-id="bb7fb-110">Pour les expériences VR [distribuées par vapeur](updating-your-steamvr-application-for-windows-mixed-reality.md), nous avons [mis à jour la version bêta de Windows Mixed Reality for SteamVR](https://steamcommunity.com/games/719950/announcements/detail/1687045485866139800) avec les derniers vols Windows Insider RS5, de sorte que les titres de SteamVR s’affichent dans le menu Démarrer de la réalité mixte de Windows dans la liste «toutes les applications». automatiquement à l’aide d’un lanceur par défaut.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-110">For VR experiences [distributed through Steam](updating-your-steamvr-application-for-windows-mixed-reality.md), we've [updated the Windows Mixed Reality for SteamVR Beta](https://steamcommunity.com/games/719950/announcements/detail/1687045485866139800) along with the latest Windows Insider RS5 flights so that SteamVR titles show up in the Windows Mixed Reality Start menu in the "All apps" list automatically using a default launcher.</span></span> <span data-ttu-id="bb7fb-111">En d’autres termes, la méthode décrite dans cet article n’est pas nécessaire pour les titres SteamVR et sera remplacée par la fonctionnalité bêta de Windows Mixed Reality pour SteamVR.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-111">In other words, the method described in this article is unnecessary for SteamVR titles and will be overridden by the Windows Mixed Reality for SteamVR Beta functionality.</span></span>

## <a name="3d-app-launcher-creation-process"></a><span data-ttu-id="bb7fb-112">processus de création du lanceur d’applications 3D</span><span class="sxs-lookup"><span data-stu-id="bb7fb-112">3D app launcher creation process</span></span>

<span data-ttu-id="bb7fb-113">La création d’un lanceur d’applications 3D comporte trois étapes:</span><span class="sxs-lookup"><span data-stu-id="bb7fb-113">There are 3 steps to creating a 3D app launcher:</span></span>
1. [<span data-ttu-id="bb7fb-114">Conception et concept</span><span class="sxs-lookup"><span data-stu-id="bb7fb-114">Designing and concepting</span></span>](3d-app-launcher-design-guidance.md)
2. [<span data-ttu-id="bb7fb-115">Modélisation et exportation</span><span class="sxs-lookup"><span data-stu-id="bb7fb-115">Modeling and exporting</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. <span data-ttu-id="bb7fb-116">Intégration dans votre application (cet article)</span><span class="sxs-lookup"><span data-stu-id="bb7fb-116">Integrating it into your application (this article)</span></span>

<span data-ttu-id="bb7fb-117">les ressources 3D à utiliser comme lanceurs pour votre application doivent être créées à l’aide des [instructions de création Windows Mixed realisation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) pour garantir la compatibilité.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-117">3D assets to be used as launchers for your application should be authored using the [Windows Mixed Reality authoring guidelines](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) to ensure compatibility.</span></span> <span data-ttu-id="bb7fb-118">Les ressources qui ne satisfont pas à cette spécification de création ne seront pas affichées dans la page d’hébergement de la réalité mixte Windows.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-118">Assets that fail to meet this authoring specification will not be rendered in the Windows Mixed Reality home.</span></span>

## <a name="configuring-the-3d-launcher"></a><span data-ttu-id="bb7fb-119">Configuration du lanceur 3D</span><span class="sxs-lookup"><span data-stu-id="bb7fb-119">Configuring the 3D launcher</span></span>

<span data-ttu-id="bb7fb-120">Les applications Win32 s’affichent dans la liste «toutes les applications» du menu Démarrer de Windows Mixed Reality si vous créez un lanceur d’applications en 3D pour eux.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-120">Win32 applications will appear in the "All apps" list on the Windows Mixed Reality Start menu if you create a 3D app launcher for them.</span></span> <span data-ttu-id="bb7fb-121">Pour ce faire, créez un fichier [manifeste d’éléments visuels](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) référençant le lanceur d’applications 3D en procédant comme suit:</span><span class="sxs-lookup"><span data-stu-id="bb7fb-121">To do that, create a [Visual Elements Manifest](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) XML file referencing the 3D App Launcher by following these steps:</span></span>

1. <span data-ttu-id="bb7fb-122">Créez un **fichier de ressource GLB de lancement d’application 3D** (voir [modélisation et exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)).</span><span class="sxs-lookup"><span data-stu-id="bb7fb-122">Create a **3D App Launcher asset GLB file** (See [Modeling and exporting](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)).</span></span>
2. <span data-ttu-id="bb7fb-123">Créez un **[manifeste d’éléments visuels](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx)** pour votre application.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-123">Create a **[Visual Elements Manifest](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx)** for your application.</span></span>
    1. <span data-ttu-id="bb7fb-124">Vous pouvez commencer par l' [exemple ci-dessous](#sample-visual-elements-manifest).</span><span class="sxs-lookup"><span data-stu-id="bb7fb-124">You can start with the [sample below](#sample-visual-elements-manifest).</span></span>  <span data-ttu-id="bb7fb-125">Pour plus d’informations, consultez la documentation complète du [manifeste des éléments visuels](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) .</span><span class="sxs-lookup"><span data-stu-id="bb7fb-125">See the full [Visual Elements Manifest](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) documentation for more details.</span></span>
    2. <span data-ttu-id="bb7fb-126">Mettez à jour **Square150x150Logo** et **Square70x70Logo** avec un fichier PNG/jpg/gif pour votre application.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-126">Update **Square150x150Logo** and **Square70x70Logo** with a PNG/JPG/GIF for your app.</span></span>
        * <span data-ttu-id="bb7fb-127">Ils seront utilisés pour le logo 2D de l’application dans la liste toutes les applications de la réalité mixte Windows et pour le menu Démarrer sur le bureau.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-127">These will be used for the app’s 2D logo in the Windows Mixed Reality All Apps list and for the Start Menu on desktop.</span></span>
        * <span data-ttu-id="bb7fb-128">Le chemin d’accès du fichier est relatif au dossier contenant le manifeste des éléments visuels.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-128">The file path is relative to the folder containing the Visual Elements Manifest.</span></span>
        * <span data-ttu-id="bb7fb-129">Vous devez toujours fournir une icône de menu Démarrer du Bureau pour votre application via les mécanismes standard.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-129">You still need to provide a desktop Start Menu icon for your app through the standard mechanisms.</span></span> <span data-ttu-id="bb7fb-130">Celui-ci peut être directement dans l’exécutable ou dans le raccourci que vous créez (par exemple, via IShellLink:: SetIconLocation).</span><span class="sxs-lookup"><span data-stu-id="bb7fb-130">This can either be directly in the executable or in the shortcut you create (e.g. via IShellLink::SetIconLocation).</span></span>
        * <span data-ttu-id="bb7fb-131">*Facultatif* : Vous pouvez utiliser un fichier Resources. pri si vous souhaitez que le fichier MRT fournisse plusieurs tailles de ressources pour différentes échelles de résolution et des thèmes à contraste élevé.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-131">*Optional:* You can use a resources.pri file if you would like for MRT to provide multiple asset sizes for different resolution scales and high contrast themes.</span></span>
    3. <span data-ttu-id="bb7fb-132">Mettre à jour le **chemin d’accès MixedRealityModel** pour pointer vers le GLB pour votre lanceur d’applications 3D</span><span class="sxs-lookup"><span data-stu-id="bb7fb-132">Update the **MixedRealityModel Path** to point to the GLB for your 3D App Launcher</span></span>
    4. <span data-ttu-id="bb7fb-133">Enregistrez le fichier sous le même nom que votre fichier exécutable, avec l’extension «. VisualElementsManifest. xml» et enregistrez-le dans le même répertoire.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-133">Save the file with the same name as your executable file, with an extension of ".VisualElementsManifest.xml" and save it in the same directory.</span></span> <span data-ttu-id="bb7fb-134">Par exemple, pour le fichier exécutable «contoso. exe», le fichier XML associé est nommé «contoso. visualelementsmanifest. Xml».</span><span class="sxs-lookup"><span data-stu-id="bb7fb-134">For example, for the executable file "contoso.exe", the accompanying XML file is named "contoso.visualelementsmanifest.xml".</span></span>
3. <span data-ttu-id="bb7fb-135">**Ajoutez un raccourci** à votre application dans le menu Démarrer de Windows Desktop.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-135">**Add a shortcut** to your application to the desktop Windows Start Menu.</span></span> <span data-ttu-id="bb7fb-136">Pour obtenir un exemple C++ d’implémentation, consultez l' [exemple ci-dessous](#sample-app-launcher-shortcut-creation) .</span><span class="sxs-lookup"><span data-stu-id="bb7fb-136">See the [sample below](#sample-app-launcher-shortcut-creation) for an example C++ implementation.</span></span> 
    * <span data-ttu-id="bb7fb-137">Créez-le dans%ALLUSERSPROFILE%\Microsoft\Windows\Start \ programme (machine) ou%APPDATA%\Microsoft\Windows\Start \ programme \ (utilisateur)</span><span class="sxs-lookup"><span data-stu-id="bb7fb-137">Create it in %ALLUSERSPROFILE%\Microsoft\Windows\Start Menu\Programs (machine) or %APPDATA%\Microsoft\Windows\Start Menu\Programs (user)</span></span>
    * <span data-ttu-id="bb7fb-138">Si une mise à jour modifie votre manifeste d’éléments visuels ou les ressources référencées par celle-ci, le programme d’installation ou le programme d’installation doit mettre à jour le raccourci de telle sorte que le manifeste soit analysé et que les ressources mises en cache soient mises à jour.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-138">If an update changes your visual elements manifest or the assets referenced by it, the updater or installer should update the shortcut such that the manifest is reparsed and cached assets are updated.</span></span>
4. <span data-ttu-id="bb7fb-139">*Facultatif* : Si le raccourci de votre bureau ne pointe pas directement vers l’exécutable de votre application (par exemple, s’il appelle un gestionnaire de protocole personnalisé comme «myapp://»), le menu Démarrer ne trouvera pas automatiquement le fichier VisualElementsManifest. XML de l’application.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-139">*Optional:* If your desktop shortcut does not point directly to your application’s EXE (e.g., if it invokes a custom protocol handler like “myapp://”), the Start Menu won’t automatically find the app’s VisualElementsManifest.xml file.</span></span> <span data-ttu-id="bb7fb-140">Pour résoudre ce cas, le raccourci doit spécifier le chemin d’accès du fichier manifeste des éléments visuels à l’aide de System. AppUserModel. VisualElementsManifestHintPath ().</span><span class="sxs-lookup"><span data-stu-id="bb7fb-140">To resolve this, the shortcut should specify the file path of the Visual Elements Manifest using System.AppUserModel.VisualElementsManifestHintPath ().</span></span> <span data-ttu-id="bb7fb-141">Cela peut être défini dans le raccourci en utilisant les mêmes techniques que System.AppUserModel.ID.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-141">This can be set in the shortcut using the same techniques as System.AppUserModel.ID.</span></span> <span data-ttu-id="bb7fb-142">Vous n’êtes pas obligé d’utiliser System.AppUserModel.ID, mais vous pouvez le faire si vous souhaitez que le raccourci corresponde à l’ID de modèle utilisateur d’application explicite de l’application, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-142">You are not required to use System.AppUserModel.ID but you may do so if you wish for the shortcut to match the explicit Application User Model ID of the application if one is used.</span></span>  <span data-ttu-id="bb7fb-143">Consultez la section [exemple de création](#sample-app-launcher-shortcut-creation) d’un raccourci de lanceur d’application ci-dessous pour obtenir un C++ exemple.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-143">See the [sample app launcher shortcut creation](#sample-app-launcher-shortcut-creation) section below for a C++ sample.</span></span>

### <a name="sample-visual-elements-manifest"></a><span data-ttu-id="bb7fb-144">Exemple de manifeste d’éléments visuels</span><span class="sxs-lookup"><span data-stu-id="bb7fb-144">Sample Visual Elements Manifest</span></span>

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

### <a name="sample-app-launcher-shortcut-creation"></a><span data-ttu-id="bb7fb-145">Exemple de création de raccourci de lancement d’application</span><span class="sxs-lookup"><span data-stu-id="bb7fb-145">Sample app launcher shortcut creation</span></span>

<span data-ttu-id="bb7fb-146">L’exemple de code ci-dessous montre comment vous pouvez créer C++un raccourci dans, y compris le remplacement du chemin d’accès au fichier XML du manifeste des éléments visuels.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-146">The sample code below shows how you can create a shortcut in C++, including overriding the path to the Visual Elements Manifest XML file.</span></span> <span data-ttu-id="bb7fb-147">Notez que le remplacement n’est nécessaire que dans les cas où votre raccourci ne pointe pas directement vers l’EXE associé au manifeste (par exemple,</span><span class="sxs-lookup"><span data-stu-id="bb7fb-147">Note the override is only required in cases where your shortcut does not point directly to the EXE associated with the manifest (eg.</span></span> <span data-ttu-id="bb7fb-148">votre raccourci utilise un gestionnaire de protocole personnalisé comme «myapp://»).</span><span class="sxs-lookup"><span data-stu-id="bb7fb-148">your shortcut uses a custom protocol handler like "myapp://").</span></span>

#### <a name="sample-lnk-shortcut-creation-c"></a><span data-ttu-id="bb7fb-149">Exemple. LNK création de raccourciC++()</span><span class="sxs-lookup"><span data-stu-id="bb7fb-149">Sample .LNK shortcut creation (C++)</span></span>

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

#### <a name="sample-url-launcher-shortcut"></a><span data-ttu-id="bb7fb-150">Exemple. Raccourci du lanceur d’URL</span><span class="sxs-lookup"><span data-stu-id="bb7fb-150">Sample .URL launcher shortcut</span></span> 

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

## <a name="see-also"></a><span data-ttu-id="bb7fb-151">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="bb7fb-151">See also</span></span>

* <span data-ttu-id="bb7fb-152">[Exemple de modèle de réalité mixte](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) contenant un lanceur d’application 3D.</span><span class="sxs-lookup"><span data-stu-id="bb7fb-152">[Mixed reality model sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) containing a 3D app launcher.</span></span>
* [<span data-ttu-id="bb7fb-153">Guide de conception du lanceur d’applications 3D</span><span class="sxs-lookup"><span data-stu-id="bb7fb-153">3D app launcher design guidance</span></span>](3d-app-launcher-design-guidance.md)
* [<span data-ttu-id="bb7fb-154">Création de modèles 3D à utiliser dans la page d’hébergement Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="bb7fb-154">Creating 3D models for use in the Windows Mixed Reality home</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [<span data-ttu-id="bb7fb-155">Implémentation de lanceurs d’applications en 3D (applications UWP)</span><span class="sxs-lookup"><span data-stu-id="bb7fb-155">Implementing 3D app launchers (UWP apps)</span></span>](implementing-3d-app-launchers.md)
* [<span data-ttu-id="bb7fb-156">Exploration de la page d’accueil Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="bb7fb-156">Navigating the Windows Mixed Reality home</span></span>](navigating-the-windows-mixed-reality-home.md)
