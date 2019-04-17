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
# <a name="implement-3d-app-launchers-win32-apps"></a>Implémenter des lanceurs d’applications 3D (applications Win32)

> [!NOTE]
> Cette fonctionnalité est uniquement disponible pour PC qui exécutent la dernière version [Windows Insider](https://insider.windows.com) vols (RS5), génération 17704 et les versions ultérieures.

Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs arrivent avant de lancer des applications. Par défaut, les applications Win32 VR IMMERSIFS et des jeux ont d’être lancé depuis le casque à l’extérieur et n’apparaîtront pas dans la liste « Toutes les applications » dans le menu Démarrer de réalité mixte Windows. Toutefois, en suivant les instructions de cet article pour implémenter un lanceur d’applications 3D, votre expérience d’immersion Win32 VR peut être lancé depuis dans le menu Démarrer de réalité mixte Windows et un environnement domestique.

Cela vaut uniquement pour distributied d’expériences Win32 VR immersive en dehors du flux. Pour des expériences de VR [distribués via Steam](updating-your-steamvr-application-for-windows-mixed-reality.md), nous avons [mis à jour de la réalité mixte Windows pour la version bêta de SteamVR](https://steamcommunity.com/games/719950/announcements/detail/1687045485866139800) , ainsi que la dernière RS5 de Insider de Windows vols afin que SteamVR titres show inscrire dans le Windows Menu Démarrer de réalité mixte dans la liste « Toutes les applications » automatiquement en utilisant un lanceur par défaut. En d’autres termes, la méthode décrite dans cet article n’est pas nécessaire pour les titres SteamVR et sera remplacée par la réalité mixte Windows pour les fonctionnalités de la version SteamVR bêta.

## <a name="3d-app-launcher-creation-process"></a>Processus de création de lanceur application 3D

Il existe 3 étapes à la création d’un lanceur d’applications 3D :
1. [Conception et concepting](3d-app-launcher-design-guidance.md)
2. [Modélisation et l’exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. L’intégration dans votre application (cet article)

Composants 3D à utiliser comme lanceurs pour votre application doivent être créés à l’aide de la [recommandations sur la programmation de Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) pour assurer la compatibilité. Actifs qui ne parviennent pas à répondre à cette spécification création seront affichera pas dans la réalité mixte Windows domestique.

## <a name="configuring-the-3d-launcher"></a>Configuration du Lanceur 3D

Les applications Win32 seront affiche dans la liste « Toutes les applications » dans le menu Démarrer de réalité mixte Windows si vous créez un lanceur d’applications 3D pour eux. Pour ce faire, créez un [éléments Visual manifeste](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) fichier XML référençant le Lanceur d’applications 3D en suivant ces étapes :

1. Créer un **fichier GLB de ressource de lanceur d’applications 3D** (consultez [modélisation et d’exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)).
2. Créer un **[éléments Visual manifeste](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx)** pour votre application.
    1. Vous pouvez démarrer avec la [exemple ci-dessous](#sample-visual-elements-manifest).  Afficher la version complète [éléments Visual manifeste](https://msdn.microsoft.com/library/windows/apps/dn393983.aspx) documentation pour plus d’informations.
    2. Mise à jour **Square150x150Logo** et **Square70x70Logo** avec une PNG/JPG/GIF pour votre application.
        * Il seront utilisés pour le logo 2D de l’application dans la liste Windows toutes les applications de réalité mixte et le Menu Démarrer sur le bureau.
        * Le chemin d’accès de fichier est relatif au dossier contenant les éléments de manifeste Visual.
        * Vous devez toujours fournir un icône de Menu Démarrer du bureau pour votre application via des mécanismes standard. Il peut s’agir directement dans le fichier exécutable ou dans le raccourci que vous créez (par exemple, via IShellLink::SetIconLocation).
        * *Facultatif :* Vous pouvez utiliser un fichier resources.pri si vous souhaitez que MRT fournir plusieurs tailles de ressource pour les échelles différentes résolutions et des thèmes à contraste élevé.
    3. Mise à jour le **chemin d’accès MixedRealityModel** pour pointer vers le GLB pour votre Lanceur d’applications 3D
    4. Enregistrez le fichier avec le même nom que votre fichier exécutable, avec l’extension ». VisualElementsManifest.xml » et l’enregistrer dans le même répertoire. Par exemple, pour le fichier exécutable « contoso.exe », le fichier XML qui accompagne cet article est nommé « contoso.visualelementsmanifest.xml ».
3. **Ajouter un raccourci** à votre application pour le Menu Démarrer du bureau Windows. Consultez le [exemple ci-dessous](#sample-app-launcher-shortcut-creation) pour obtenir un exemple C++ implémentation. 
    * Créez %ALLUSERSPROFILE%\Microsoft\Windows\Start Menu\Programs (ordinateur) ou %APPDATA%\Microsoft\Windows\Start Menu\Programs (utilisateur)
    * Si une mise à jour modifie votre manifeste d’éléments visuels ou les ressources qu’il référencés, la mise à jour ou le programme d’installation doit mettre à jour le raccourci telles que le manifeste est réanalysé et ressources mises en cache sont mises à jour.
4. *Facultatif :* Si votre raccourci du bureau ne désigne pas directement EXE de votre application (par exemple, si elle appelle un gestionnaire de protocole personnalisé comme « myapp : / / »), le Menu Démarrer ne trouvera automatiquement le fichier l’application VisualElementsManifest.xml. Pour résoudre ce problème, le raccourci doit spécifier le chemin d’accès de fichier du manifeste d’éléments visuel à l’aide de System.AppUserModel.VisualElementsManifestHintPath (). Cela peut être défini dans le raccourci à l’aide des mêmes techniques comme System.AppUserModel.ID. Vous n’êtes pas obligé d’utiliser System.AppUserModel.ID, mais vous pouvez le faire si vous le souhaitez pour le raccourci faire correspondre l’ID de modèle d’Application utilisateur explicite de l’application si elle est utilisée.  Consultez le [exemple de création d’un raccourci application Lanceur](#sample-app-launcher-shortcut-creation) section ci-dessous pour un C++ exemple.

### <a name="sample-visual-elements-manifest"></a>Exemple de fichier manifeste éléments visuels

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

### <a name="sample-app-launcher-shortcut-creation"></a>Création d’un raccourci du Lanceur application exemple

L’exemple de code ci-dessous montre comment vous pouvez créer un raccourci dans C++, y compris la substitution le chemin d’accès au fichier XML de manifeste Visual des éléments. Notez que le remplacement est nécessaire uniquement dans les cas où votre raccourci ne pointe pas directement au fichier .exe associé au manifeste (par ex. votre raccourci utilise un gestionnaire de protocole personnalisé comme « myapp : / / »).

#### <a name="sample-lnk-shortcut-creation-c"></a>Exemple. Création d’un raccourci LNK (C++)

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

#### <a name="sample-url-launcher-shortcut"></a>Exemple. Raccourci du Lanceur d’URL 

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

## <a name="see-also"></a>Voir aussi

* [Exemple de modèle de réalité mixte](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) contenant un lanceur d’applications 3D.
* [Guide de conception du Lanceur d’application 3D](3d-app-launcher-design-guidance.md)
* [Création de modèles 3D pour une utilisation dans la page d’accueil Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [Implémentation des lanceurs d’applications 3D (applications UWP)](implementing-3d-app-launchers.md)
* [Navigation dans Windows Mixed Reality domestique](navigating-the-windows-mixed-reality-home.md)
