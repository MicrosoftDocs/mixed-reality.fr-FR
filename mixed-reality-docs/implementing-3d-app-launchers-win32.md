---
title: Implémenter des lanceurs d’applications en 3D (applications Win32)
description: Comment créer des programmes de lancement et des logos d’applications en 3D pour les jeux et les applications Win32 VR (distribués en dehors de la vapeur) afin qu’ils s’affichent dans le menu Démarrer et l’environnement d’accueil de Windows Mixed Reality.
author: thmignon
ms.author: thmignon
ms.date: 07/12/2018
ms.topic: article
keywords: 3D, logo, icône, modélisation, lanceur, lanceur 3D, vignette, cube actif, Win32
ms.openlocfilehash: 87eadfb5184f9fb5f8d513ab00a2a954e71df376
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438572"
---
# <a name="implement-3d-app-launchers-win32-apps"></a>Implémenter des lanceurs d’applications en 3D (applications Win32)

> [!NOTE]
> Cette fonctionnalité est uniquement disponible pour les PC qui exécutent les derniers vols de [Windows Insider](https://insider.windows.com) (RS5), Build 17704 et versions ultérieures.

La [base de la réalité Windows Mixed](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs se trouvent avant de lancer des applications. Par défaut, les applications et les jeux Win32 VR Win32 sont lancés à partir de l’extérieur du casque et n’apparaissent pas dans la liste « toutes les applications » dans le menu Démarrer de Windows Mixed Reality. Toutefois, en suivant les instructions de cet article pour implémenter un lanceur d’applications 3D, votre expérience Win32 VR peut être lancée à partir du menu Démarrer et de l’environnement d’accueil de Windows Mixed Reality.

Cela est vrai uniquement pour les expériences Win32 VR distributied en dehors de la vapeur. Pour les expériences VR [distribuées par vapeur](updating-your-steamvr-application-for-windows-mixed-reality.md), nous avons [mis à jour la version bêta de Windows Mixed Reality for SteamVR](https://steamcommunity.com/games/719950/announcements/detail/1687045485866139800) avec les derniers vols Windows Insider RS5, de sorte que les titres de SteamVR s’affichent dans le menu Démarrer de la réalité mixte de Windows dans la liste « toutes les applications ». automatiquement à l’aide d’un lanceur par défaut. En d’autres termes, la méthode décrite dans cet article n’est pas nécessaire pour les titres SteamVR et sera remplacée par la fonctionnalité bêta de Windows Mixed Reality pour SteamVR.

## <a name="3d-app-launcher-creation-process"></a>processus de création du lanceur d’applications 3D

La création d’un lanceur d’applications 3D comporte trois étapes :
1. [Conception et concept](3d-app-launcher-design-guidance.md)
2. [Modélisation et exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. Intégration dans votre application (cet article)

les ressources 3D à utiliser comme lanceurs pour votre application doivent être créées à l’aide des [instructions de création Windows Mixed realisation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) pour garantir la compatibilité. Les ressources qui ne satisfont pas à cette spécification de création ne seront pas affichées dans la page d’hébergement de la réalité mixte Windows.

## <a name="configuring-the-3d-launcher"></a>Configuration du lanceur 3D

Les applications Win32 s’affichent dans la liste « toutes les applications » du menu Démarrer de Windows Mixed Reality si vous créez un lanceur d’applications en 3D pour eux. Pour ce faire, créez un fichier [manifeste d’éléments visuels](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) référençant le lanceur d’applications 3D en procédant comme suit :

1. Créez un **fichier de ressource GLB de lancement d’application 3D** (voir [modélisation et exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)).
2. Créez un **[manifeste d’éléments visuels](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx)** pour votre application.
    1. Vous pouvez commencer par l' [exemple ci-dessous](#sample-visual-elements-manifest).  Pour plus d’informations, consultez la documentation complète du [manifeste des éléments visuels](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) .
    2. Mettez à jour **Square150x150Logo** et **Square70x70Logo** avec un fichier PNG/jpg/gif pour votre application.
        * Ils seront utilisés pour le logo 2D de l’application dans la liste toutes les applications de la réalité mixte Windows et pour le menu Démarrer sur le bureau.
        * Le chemin d’accès du fichier est relatif au dossier contenant le manifeste des éléments visuels.
        * Vous devez toujours fournir une icône de menu Démarrer du Bureau pour votre application via les mécanismes standard. Celui-ci peut être directement dans l’exécutable ou dans le raccourci que vous créez (par exemple, via IShellLink :: SetIconLocation).
        * *Facultatif :* Vous pouvez utiliser un fichier Resources. pri si vous souhaitez que le fichier MRT fournisse plusieurs tailles de ressources pour différentes échelles de résolution et des thèmes à contraste élevé.
    3. Mettre à jour le **chemin d’accès MixedRealityModel** pour pointer vers le GLB pour votre lanceur d’applications 3D
    4. Enregistrez le fichier sous le même nom que votre fichier exécutable, avec l’extension «. VisualElementsManifest. xml» et enregistrez-le dans le même répertoire. Par exemple, pour le fichier exécutable « contoso. exe », le fichier XML associé est nommé « contoso. visualelementsmanifest. Xml ».
3. **Ajoutez un raccourci** à votre application dans le menu Démarrer de Windows Desktop. Pour obtenir un exemple C++ d’implémentation, consultez l' [exemple ci-dessous](#sample-app-launcher-shortcut-creation) . 
    * Créez-le dans%ALLUSERSPROFILE%\Microsoft\Windows\Start \ programme (machine) ou%APPDATA%\Microsoft\Windows\Start \ programme \ (utilisateur)
    * Si une mise à jour modifie votre manifeste d’éléments visuels ou les ressources référencées par celle-ci, le programme d’installation ou le programme d’installation doit mettre à jour le raccourci de telle sorte que le manifeste soit analysé et que les ressources mises en cache soient mises à jour.
4. *Facultatif :* Si le raccourci de votre bureau ne pointe pas directement vers l’exécutable de votre application (par exemple, s’il appelle un gestionnaire de protocole personnalisé comme « myapp:// »), le menu Démarrer ne trouvera pas automatiquement le fichier VisualElementsManifest. XML de l’application. Pour résoudre ce cas, le raccourci doit spécifier le chemin d’accès du fichier manifeste des éléments visuels à l’aide de System. AppUserModel. VisualElementsManifestHintPath (). Cela peut être défini dans le raccourci en utilisant les mêmes techniques que System.AppUserModel.ID. Vous n’êtes pas obligé d’utiliser System.AppUserModel.ID, mais vous pouvez le faire si vous souhaitez que le raccourci corresponde à l’ID de modèle utilisateur d’application explicite de l’application, le cas échéant.  Consultez la section exemple de création d’un [raccourci de lanceur d’application](#sample-app-launcher-shortcut-creation) ci-dessous pour obtenir un C++ exemple.

### <a name="sample-visual-elements-manifest"></a>Exemple de manifeste d’éléments visuels

```xml
<Application xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance">
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

### <a name="sample-app-launcher-shortcut-creation"></a>Exemple de création de raccourci de lancement d’application

L’exemple de code ci-dessous montre comment vous pouvez créer C++un raccourci dans, y compris le remplacement du chemin d’accès au fichier XML du manifeste des éléments visuels. Notez que le remplacement n’est nécessaire que dans les cas où votre raccourci ne pointe pas directement vers l’EXE associé au manifeste (par exemple, votre raccourci utilise un gestionnaire de protocole personnalisé comme « myapp:// »).

#### <a name="sample-lnk-shortcut-creation-c"></a>Exemple. LNK création de raccourciC++()

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

#### <a name="sample-url-launcher-shortcut"></a>Exemple. Raccourci du lanceur d’URL 

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

## <a name="see-also"></a>Articles associés

* [Exemple de modèle de réalité mixte](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) contenant un lanceur d’application 3D.
* [Guide de conception du lanceur d’applications 3D](3d-app-launcher-design-guidance.md)
* [Création de modèles 3D à utiliser dans la page d’hébergement Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [Implémentation de lanceurs d’applications en 3D (applications UWP)](implementing-3d-app-launchers.md)
* [Exploration de la page d’accueil Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)
