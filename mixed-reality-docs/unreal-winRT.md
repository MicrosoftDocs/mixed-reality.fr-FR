---
title: WinRT dans Unreal
description: Vue d’ensemble du plug-in d’audio spatial pour le moteur Unreal.
author: fieldsJacksonG
ms.author: jacksonf
ms.date: 07/08/2020
ms.topic: article
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, streaming, communication à distance, réalité mixte, développement, démarrage, fonctionnalités, nouveau projet, émulateur, documentation, guides, fonctionnalités, hologrammes, développement de jeux
ms.openlocfilehash: 7a64002a5fa48bb589ab113f0a8dc1bfcb92d535
ms.sourcegitcommit: 2813f5b3027d47f7c6e9772338935eeccfa2aaec
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86408217"
---
# <a name="winrt-in-unreal"></a>WinRT dans Unreal

## <a name="overview"></a>Vue d’ensemble

Au cours de votre développement HoloLens, vous devrez peut-être écrire une fonctionnalité à l’aide de WinRT. Par exemple, l’ouverture d’une boîte de dialogue de fichier dans une application HoloLens nécessiterait FileSavePicker dans le fichier d’en-tête WinRT/Windows. Storage. Pickrs. h.  Étant donné que la non-réelle ne compile pas le code WinRT en mode natif, il s’agit de votre travail pour générer un fichier binaire distinct qui peut être consommé par le système de génération inréel. Ce didacticiel vous guide tout au long de ce scénario.

## <a name="objectives"></a>Objectifs
- Créer une DLL Windows universelle qui ouvre un FileSaveDialogue
- Lier cette DLL à un projet de jeu inréel
- Enregistrer un fichier sur HoloLens à partir d’un modèle non réel à l’aide de la nouvelle DLL

## <a name="getting-started"></a>Prise en main
1. Vérifiez que tous les [Outils requis](unreal-uxt-ch1.md) sont installés
2. [Créez un nouveau projet inréel](unreal-uxt-ch2.md#creating-a-new-unreal-project) et nommez-le **Consumewinrt**
3. Activer les [plug-ins requis](unreal-uxt-ch2.md#enabling-required-plugins) pour le développement HoloLens
4. [Configuration pour le déploiement](unreal-uxt-ch6.md) sur un appareil ou un émulateur

## <a name="creating-a-winrt-dll"></a>Création d’une DLL WinRT 
1. Ouvrez un nouveau projet Visual Studio et créez un projet **dll (Windows universel)** dans le même répertoire que le fichier **uproject** du jeu inréel. 

![Création d’une DLL](images/unreal-winrt-img-01.png)

2. Nommez le projet **HoloLensWinrtDLL** et définissez l’emplacement en tant que sous-répertoire **thirdparty** sur le fichier uproject du jeu inréel. 
    * Sélectionnez **Placer la solution et le projet dans le même répertoire** pour simplifier la recherche des chemins d’accès ultérieurement. 

![Configuration de la DLL](images/unreal-winrt-img-02.png)

> [!IMPORTANT]
> Une fois le nouveau projet compilé, vous devez prêter une attention particulière aux fichiers CPP et d’en-tête vides, nommés **HoloLensWinrtDLL. cpp** et **HoloLensWinrtDLL. h** , respectivement. L’en-tête est le fichier include qui utilise la DLL dans Unreal, tandis que le CPP contient le corps de toutes les fonctions que vous exportez et inclut tout code WinRT qui, sans cela, ne serait pas en mesure de compiler. 

3. Avant d’ajouter du code, vous devez mettre à jour les propriétés du projet pour vous assurer que le code WinRT dont vous avez besoin peut être compilé : 
    * Cliquez avec le bouton droit sur le projet HoloLensWinrtDLL et sélectionnez **Propriétés** .  
    * Remplacez la liste déroulante **configuration** par **toutes les configurations** et le menu déroulant **plateforme** à **toutes les plateformes** .  
    * Sous **Propriétés de Configuration> C/C++> toutes les options**:
        * Ajouter **await** à **des options supplémentaires** pour nous assurer que nous pouvons attendre des tâches asynchrones  
        * Remplacez la **norme du langage c++** par la norme **ISO C++ 17 (/std : C++ 17)** pour inclure tout code WinRT

![Configuration de la DLL](images/unreal-winrt-img-03.png)

Votre projet est prêt à mettre à jour la source de la DLL avec le code WinRT qui ouvre une boîte de dialogue de fichier et enregistre un fichier sur le disque HoloLens.  

## <a name="adding-the-dll-code"></a>Ajout du code de la DLL
1. Ouvrez **HoloLensWinrtDLL. h** et ajoutez une fonction dll exportée pour l’utilisation de l’inréel : 

```cpp
#pragma once

class HoloLensWinrtDLL
{
public:
    _declspec(dllexport) static void OpenFileDialogue();
};
```

2. Ouvrez **HoloLensWinrtDLL. cpp** et ajoutez tous les en-têtes qui seront utilisés par la classe :  

```cpp
#include "pch.h"
#include "HoloLensWinrtDLL.h"

#include <winrt/Windows.Storage.h>
#include <winrt/Windows.Storage.Streams.h>
#include <winrt/Windows.Storage.Pickers.h>
#include <winrt/Windows.Foundation.h>
#include <winrt/Windows.Foundation.Collections.h>

#include <string>
#include <vector>
#include <thread>
```

> [!NOTE]
> Tout le code WinRT est stocké dans **HoloLensWinrtDLL. cpp** , si bien que non réel n’essaie pas d’inclure de code WinRT lors du référencement de l’en-tête. 

3. Toujours dans **HoloLensWinrtDLL. cpp**, ajoutez un corps de fonction pour OpenFileDialogue () et tout le code pris en charge : 

```cpp
// sgm is declared outside of OpenFileDialogue so it doesn't
// get destroyed when OpenFileDialogue goes out of scope.
SaveGameManager sgm;

void HoloLensWinrtDLL::OpenFileDialogue()
{
    sgm.SaveGame();
}
```

4. Ajoutez une classe SaveGameManager à **HoloLensWinrtDLL. cpp** pour gérer la boîte de dialogue de fichier et enregistrer le fichier : 

```cpp
class SaveGameManager
{
public:
    SaveGameManager()
    {
    }

    ~SaveGameManager()
    {
        // Wait for currently running thread to complete before terminating.
        if(m_thread.joinable())
        {
            m_thread.join();
        }
    }

    void SaveGame()
    {
        OpenFileDialogueAction();
    }

private:
    winrt::Windows::Storage::StorageFile m_file = winrt::Windows::Storage::StorageFile(nullprt);
    std::thread m_thread;

    winrt::Windows::Foundation::IAsyncAction OpenFileDialogueAction()
    {
        std::vector<winrt::hstring> extensions;
        extensions.push_back(L".txt");

        auto picker = winrt::Windows::Storage::Pickers::FileSavePicker();

        // FileSavePicker needs a file type to open without errors.
        picker.FileTypeChoices().Insert(L"Plain Text",
                                        winrt::single_threaded_vector<winrt::hstring>(
                                        std::move(extensions)));

        // Opening the FilePicker must be done on the Game UI thread.
        // Any other IAsyncOperations should be done on a background thread.
        m_file = co_await picker.PickSaveFileAsync();

        if(m_file)
        {
            // Unreal's game thread is an STA, async tasks need to run on
            // a background MTA thread, or waiting on them will deadlock.    
            std::thread thread([this]() { RunThread(); });
            m_thread = std::move(thread);
        }
    }

    void RunThread()
    {
        // Ensure this thread is an MTA
        winrt::init_apartment();
        Run().get();
    }

    winrt::Windows::Foundation::IAsyncAction Run()
    {
        co_await winrt::Windows::Storage::FileIO::WriteTextAsync(
                m_file, L"Hello WinRT");
    }
};
```

5. Générez la solution pour la **version > ARM64** pour générer la dll dans le répertoire enfant ARM64/Release/HoloLensWinrtDLL à partir de la solution dll. 

## <a name="adding-the-winrt-binary-to-unreal"></a>Ajout du fichier binaire WinRT à Unreal 
La liaison et l’utilisation d’une DLL dans unreally requièrent un projet C++. Si vous utilisez un projet Blueprint, il peut être facilement converti en projet C++ en ajoutant une classe C++ :  

1. Dans l’éditeur inréaliste, ouvrez le **fichier > nouvelle classe C++...** et créez un **acteur** nommé **WinrtActor** pour exécuter le code dans la dll : 

![Configuration de la DLL](images/unreal-winrt-img-04.png)

> [!NOTE]
> Une solution a été créée dans le même répertoire que le fichier uproject, avec un nouveau script de compilation nommé source/ConsumeWinRT/ConsumerWinRT. Build. cs.

2. Ouvrez la solution, recherchez le dossier **Games/ConsumeWinRT/source/ConsumeWinRT** , puis ouvrez **ConsumeWinRT.Build.cs**:

![Configuration de la DLL](images/unreal-winrt-img-05.png)

### <a name="linking-the-dll"></a>Liaison de la DLL
1. Dans **ConsumeWinRT.Build.cs**, ajoutez une propriété pour rechercher le chemin d’accès include pour la dll (répertoire contenant HoloLensWinrtDLL. h). La DLL se trouve dans un répertoire enfant du chemin d’accès include. cette propriété sera donc utilisée comme répertoire racine binaire :

```cs
public class ConsumeWinRT : ModuleRules
{
    private string WinrtIncPath
    {
        get 
        {
            string ModulePath = Path.GetDirectoryName(
                   RulesCompiler.GetFileNameFromType(this.GetType()));

            // Third party directory is at the project root,
            // which is two directories up from the game .exe (Binaries/HoloLens)
            return Path.GetFullPath(
                   Path.Combine(ModulePath,
                   "../../ThirddParty/HoloLensWinrtDLL"));
        }
    }
}
```

2. Dans le constructeur de classe, ajoutez le code suivant pour mettre à jour le chemin d’accès include, liez la nouvelle bibliothèque et Retardez le chargement, puis copiez la DLL dans l’emplacement AppX empaqueté :

```cs
public ConsumeWinRT(ReadOnlyTargetRules target) : base(Target)
{
    // This is the directory the DLL's include header is in.
    PublicIncludePaths.Add(WinrtIncPath);

    // The code in HoloLensWinrtDLL will only work in a Windows Store app.
    // Only link these binaries for HoloLens.
    // Similar code can be written for desktop and similarly linked 
    // to use the same features when using Holographic Remoting.
    if(Target.Platform == UnrealTargetPlatform.HoloLens)
    {
        // Link the lib
        PublicAdditionalLibraries.Add(Path.Combine(
              WinrtIncPath, "ARM64", "Release",
              "HoloLensWinrtDLL","HoloLensWinrtDLL.lib"));

        string winrtDLL = "HoloLensWinrtDLL.dll";
        // Mark the dll to be DelayLoaded
        PublicDelayLoadDLLs.Add(winrtDLL);
        // RuntimeDependencies are included in packaged builds.
        RuntimeDependencies.Add(Path.Combine(WinrtIncPath,
                "ARM64", "Release", "HoloLensWinrtDLL", winrtDLL));
    }

    // Preserve the original code in build.cs below:
}
```

3. Ouvrez **WinrtActor. h** et ajoutez deux définitions de fonction, une qui peut être utilisée par un plan et une autre qui utilise le code de la dll : 
```cpp
public:
    UFUNCTION(BlueprintCallable)
    static void OpenFileDialogue;
```

4. Ouvrez **WinrtActor. cpp** et chargez la dll dans BeginPlay : 

```cpp
void AWinfrtActor::BeginPlay()
{
#if PLATFORM_HOLOLENS
    HoloLensWinrtDLL::OpenFileDialogue();
#endif
}
``` 

>[!CAUTION]
> La DLL doit être chargée avant d’appeler l’une de ses fonctions.

### <a name="building-the-game"></a>Création du jeu
1. Générez la solution Game pour lancer l’éditeur inréel ouvert dans le projet Game : 
    * Dans l’onglet **Placer les acteurs** , recherchez le nouveau **WinrtActor** et faites-le glisser dans la scène. 
    * Ouvrez le plan de niveau pour exécuter la fonction Blueprint Callable dans **WinrtActor** 

![Configuration de la DLL](images/unreal-winrt-img-06.png)

2. Dans le **monde entier**, recherchez le **WindrtActor** précédemment déposé dans la scène et faites-le glisser vers le plan de niveau : 

![Configuration de la DLL](images/unreal-winrt-img-07.png)

3. Dans le plan de niveau, faites glisser le nœud de sortie à partir de WinrtActor, recherchez la **boîte de dialogue Ouvrir le fichier**, puis routez le nœud à partir de n’importe quelle entrée d’utilisateur.  Dans ce cas, la boîte de dialogue Ouvrir un fichier est appelée à partir d’un événement vocal : 

![Configuration de la DLL](images/unreal-winrt-img-08.png)

4. [Empaquetez ce jeu pour HoloLens](unreal-uxt-ch6.md), déployez-le et exécutez-le.  

Lorsque l’appel d’OpenFileDialogue n’est pas vrai, une boîte de dialogue fichier s’ouvre sur le fichier HoloLens invitant à entrer un nom de fichier. txt.  Une fois le fichier enregistré, accédez à l’onglet **Explorateur de fichiers** dans le portail de l’appareil pour afficher le contenu « Hello WinRT ». 

## <a name="summary"></a>Résumé 

Nous vous encourageons à utiliser le code de ce didacticiel comme point de départ pour consommer du code WinRT dans des conditions inréelles.  Elle permet aux utilisateurs d’enregistrer des fichiers sur le disque HoloLens en utilisant la même boîte de dialogue de fichier que Windows.  Suivez le même processus pour exporter toutes les fonctions supplémentaires à partir de l’en-tête HoloLensWinrtDLL et les utiliser dans Unreal.  Notez le code DLL qui attend un code WinRT asynchrone dans un thread MTA d’arrière-plan, ce qui évite le blocage du thread de jeu inréel. 

## <a name="see-also"></a>Voir aussi
* [API C++/WinRT](https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/)
* [FileSavePicker, classe](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) 
* [Bibliothèques tierces non réelles](https://docs.unrealengine.com/Programming/BuildTools/UnrealBuildTool/ThirdPartyLibraries/index.html) 
