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
# <a name="winrt-in-unreal"></a><span data-ttu-id="428cd-104">WinRT dans Unreal</span><span class="sxs-lookup"><span data-stu-id="428cd-104">WinRT in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="428cd-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="428cd-105">Overview</span></span>

<span data-ttu-id="428cd-106">Au cours de votre développement HoloLens, vous devrez peut-être écrire une fonctionnalité à l’aide de WinRT.</span><span class="sxs-lookup"><span data-stu-id="428cd-106">Over the course of your HoloLens development you may need to write a feature using WinRT.</span></span> <span data-ttu-id="428cd-107">Par exemple, l’ouverture d’une boîte de dialogue de fichier dans une application HoloLens nécessiterait FileSavePicker dans le fichier d’en-tête WinRT/Windows. Storage. Pickrs. h.</span><span class="sxs-lookup"><span data-stu-id="428cd-107">For example, opening a file dialogue in a HoloLens application would need the FileSavePicker in winrt/Windows.Storage.Pickers.h header file.</span></span>  <span data-ttu-id="428cd-108">Étant donné que la non-réelle ne compile pas le code WinRT en mode natif, il s’agit de votre travail pour générer un fichier binaire distinct qui peut être consommé par le système de génération inréel.</span><span class="sxs-lookup"><span data-stu-id="428cd-108">Since Unreal doesn't natively compile WinRT code, it's your job to build a separate binary and that can be consumed by Unreal’s build system.</span></span> <span data-ttu-id="428cd-109">Ce didacticiel vous guide tout au long de ce scénario.</span><span class="sxs-lookup"><span data-stu-id="428cd-109">This tutorial will walk you through just such a scenario.</span></span>

## <a name="objectives"></a><span data-ttu-id="428cd-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="428cd-110">Objectives</span></span>
- <span data-ttu-id="428cd-111">Créer une DLL Windows universelle qui ouvre un FileSaveDialogue</span><span class="sxs-lookup"><span data-stu-id="428cd-111">Create a Universal Windows DLL that opens a FileSaveDialogue</span></span>
- <span data-ttu-id="428cd-112">Lier cette DLL à un projet de jeu inréel</span><span class="sxs-lookup"><span data-stu-id="428cd-112">Link that DLL to an Unreal game project</span></span>
- <span data-ttu-id="428cd-113">Enregistrer un fichier sur HoloLens à partir d’un modèle non réel à l’aide de la nouvelle DLL</span><span class="sxs-lookup"><span data-stu-id="428cd-113">Save a file on the HoloLens from an Unreal blueprint using the new DLL</span></span>

## <a name="getting-started"></a><span data-ttu-id="428cd-114">Prise en main</span><span class="sxs-lookup"><span data-stu-id="428cd-114">Getting started</span></span>
1. <span data-ttu-id="428cd-115">Vérifiez que tous les [Outils requis](unreal-uxt-ch1.md) sont installés</span><span class="sxs-lookup"><span data-stu-id="428cd-115">Check that you have all [required tools](unreal-uxt-ch1.md) installed</span></span>
2. <span data-ttu-id="428cd-116">[Créez un nouveau projet inréel](unreal-uxt-ch2.md#creating-a-new-unreal-project) et nommez-le **Consumewinrt**</span><span class="sxs-lookup"><span data-stu-id="428cd-116">[Create a new Unreal project](unreal-uxt-ch2.md#creating-a-new-unreal-project) and name it **Consumewinrt**</span></span>
3. <span data-ttu-id="428cd-117">Activer les [plug-ins requis](unreal-uxt-ch2.md#enabling-required-plugins) pour le développement HoloLens</span><span class="sxs-lookup"><span data-stu-id="428cd-117">Enable the [required plugins](unreal-uxt-ch2.md#enabling-required-plugins) for HoloLens development</span></span>
4. <span data-ttu-id="428cd-118">[Configuration pour le déploiement](unreal-uxt-ch6.md) sur un appareil ou un émulateur</span><span class="sxs-lookup"><span data-stu-id="428cd-118">[Setup for deployment](unreal-uxt-ch6.md) to a device or emulator</span></span>

## <a name="creating-a-winrt-dll"></a><span data-ttu-id="428cd-119">Création d’une DLL WinRT</span><span class="sxs-lookup"><span data-stu-id="428cd-119">Creating a WinRT DLL</span></span> 
1. <span data-ttu-id="428cd-120">Ouvrez un nouveau projet Visual Studio et créez un projet **dll (Windows universel)** dans le même répertoire que le fichier **uproject** du jeu inréel.</span><span class="sxs-lookup"><span data-stu-id="428cd-120">Open a new Visual Studio project and create a **DLL (Universal Windows)** project in the same directory to the Unreal game’s **uproject** file.</span></span> 

![Création d’une DLL](images/unreal-winrt-img-01.png)

2. <span data-ttu-id="428cd-122">Nommez le projet **HoloLensWinrtDLL** et définissez l’emplacement en tant que sous-répertoire **thirdparty** sur le fichier uproject du jeu inréel.</span><span class="sxs-lookup"><span data-stu-id="428cd-122">Name the project **HoloLensWinrtDLL** and set the location as a **ThirdParty** subdirectory to the Unreal game’s uproject file.</span></span> 
    * <span data-ttu-id="428cd-123">Sélectionnez **Placer la solution et le projet dans le même répertoire** pour simplifier la recherche des chemins d’accès ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="428cd-123">Select **Place solution and project in the same directory** to simplify looking for paths later.</span></span> 

![Configuration de la DLL](images/unreal-winrt-img-02.png)

> [!IMPORTANT]
> <span data-ttu-id="428cd-125">Une fois le nouveau projet compilé, vous devez prêter une attention particulière aux fichiers CPP et d’en-tête vides, nommés **HoloLensWinrtDLL. cpp** et **HoloLensWinrtDLL. h** , respectivement.</span><span class="sxs-lookup"><span data-stu-id="428cd-125">After the new project compiles, you want to pay special attention to the blank cpp and header files, named **HoloLensWinrtDLL.cpp** and **HoloLensWinrtDLL.h** respectively.</span></span> <span data-ttu-id="428cd-126">L’en-tête est le fichier include qui utilise la DLL dans Unreal, tandis que le CPP contient le corps de toutes les fonctions que vous exportez et inclut tout code WinRT qui, sans cela, ne serait pas en mesure de compiler.</span><span class="sxs-lookup"><span data-stu-id="428cd-126">The header is the include file that uses the DLL in Unreal, while the cpp holds the body of any functions you export and includes any WinRT code that Unreal wouldn't otherwise be able to compile.</span></span> 

3. <span data-ttu-id="428cd-127">Avant d’ajouter du code, vous devez mettre à jour les propriétés du projet pour vous assurer que le code WinRT dont vous avez besoin peut être compilé :</span><span class="sxs-lookup"><span data-stu-id="428cd-127">Before you add any code, you need to update the project properties to ensure the WinRT code you need can compile:</span></span> 
    * <span data-ttu-id="428cd-128">Cliquez avec le bouton droit sur le projet HoloLensWinrtDLL et sélectionnez **Propriétés** .</span><span class="sxs-lookup"><span data-stu-id="428cd-128">Right click on the HoloLensWinrtDLL project and select **properties**</span></span>  
    * <span data-ttu-id="428cd-129">Remplacez la liste déroulante **configuration** par **toutes les configurations** et le menu déroulant **plateforme** à **toutes les plateformes** .</span><span class="sxs-lookup"><span data-stu-id="428cd-129">Change the **Configuration** dropdown to **All Configurations** and the **Platform** dropdown to **All Platforms**</span></span>  
    * <span data-ttu-id="428cd-130">Sous **Propriétés de Configuration> C/C++> toutes les options**:</span><span class="sxs-lookup"><span data-stu-id="428cd-130">Under **Configuration Properties> C/C++> All Options**:</span></span>
        * <span data-ttu-id="428cd-131">Ajouter **await** à **des options supplémentaires** pour nous assurer que nous pouvons attendre des tâches asynchrones</span><span class="sxs-lookup"><span data-stu-id="428cd-131">Add **await** to **Additional Options** to ensure we can wait on async tasks</span></span>  
        * <span data-ttu-id="428cd-132">Remplacez la **norme du langage c++** par la norme **ISO C++ 17 (/std : C++ 17)** pour inclure tout code WinRT</span><span class="sxs-lookup"><span data-stu-id="428cd-132">Change **C++ Language Standard** to **ISO C++17 Standard (/std:c++17)** to include any WinRT code</span></span>

![Configuration de la DLL](images/unreal-winrt-img-03.png)

<span data-ttu-id="428cd-134">Votre projet est prêt à mettre à jour la source de la DLL avec le code WinRT qui ouvre une boîte de dialogue de fichier et enregistre un fichier sur le disque HoloLens.</span><span class="sxs-lookup"><span data-stu-id="428cd-134">Your project is ready to update the DLL’s source with WinRT code that opens a file dialogue and saves a file to the HoloLens disk.</span></span>  

## <a name="adding-the-dll-code"></a><span data-ttu-id="428cd-135">Ajout du code de la DLL</span><span class="sxs-lookup"><span data-stu-id="428cd-135">Adding the DLL code</span></span>
1. <span data-ttu-id="428cd-136">Ouvrez **HoloLensWinrtDLL. h** et ajoutez une fonction dll exportée pour l’utilisation de l’inréel :</span><span class="sxs-lookup"><span data-stu-id="428cd-136">Open **HoloLensWinrtDLL.h** and add a dll exported function for Unreal to consume:</span></span> 

```cpp
#pragma once

class HoloLensWinrtDLL
{
public:
    _declspec(dllexport) static void OpenFileDialogue();
};
```

2. <span data-ttu-id="428cd-137">Ouvrez **HoloLensWinrtDLL. cpp** et ajoutez tous les en-têtes qui seront utilisés par la classe :</span><span class="sxs-lookup"><span data-stu-id="428cd-137">Open **HoloLensWinrtDLL.cpp** and add all headers the class will use:</span></span>  

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
> <span data-ttu-id="428cd-138">Tout le code WinRT est stocké dans **HoloLensWinrtDLL. cpp** , si bien que non réel n’essaie pas d’inclure de code WinRT lors du référencement de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="428cd-138">All WinRT code is stored in **HoloLensWinrtDLL.cpp** so Unreal doesn't try to include any WinRT code when referencing the header.</span></span> 

3. <span data-ttu-id="428cd-139">Toujours dans **HoloLensWinrtDLL. cpp**, ajoutez un corps de fonction pour OpenFileDialogue () et tout le code pris en charge :</span><span class="sxs-lookup"><span data-stu-id="428cd-139">Still in **HoloLensWinrtDLL.cpp**, add a function body for OpenFileDialogue() and all supported code:</span></span> 

```cpp
// sgm is declared outside of OpenFileDialogue so it doesn't
// get destroyed when OpenFileDialogue goes out of scope.
SaveGameManager sgm;

void HoloLensWinrtDLL::OpenFileDialogue()
{
    sgm.SaveGame();
}
```

4. <span data-ttu-id="428cd-140">Ajoutez une classe SaveGameManager à **HoloLensWinrtDLL. cpp** pour gérer la boîte de dialogue de fichier et enregistrer le fichier :</span><span class="sxs-lookup"><span data-stu-id="428cd-140">Add a SaveGameManager class to **HoloLensWinrtDLL.cpp** to handle the file dialogue and saving the file:</span></span> 

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

5. <span data-ttu-id="428cd-141">Générez la solution pour la **version > ARM64** pour générer la dll dans le répertoire enfant ARM64/Release/HoloLensWinrtDLL à partir de la solution dll.</span><span class="sxs-lookup"><span data-stu-id="428cd-141">Build the solution for **Release > ARM64** to build the DLL to the child directory ARM64/Release/HoloLensWinrtDLL from the DLL solution.</span></span> 

## <a name="adding-the-winrt-binary-to-unreal"></a><span data-ttu-id="428cd-142">Ajout du fichier binaire WinRT à Unreal</span><span class="sxs-lookup"><span data-stu-id="428cd-142">Adding the WinRT binary to Unreal</span></span> 
<span data-ttu-id="428cd-143">La liaison et l’utilisation d’une DLL dans unreally requièrent un projet C++.</span><span class="sxs-lookup"><span data-stu-id="428cd-143">Linking and using a DLL in Unreal requires a C++ project.</span></span> <span data-ttu-id="428cd-144">Si vous utilisez un projet Blueprint, il peut être facilement converti en projet C++ en ajoutant une classe C++ :</span><span class="sxs-lookup"><span data-stu-id="428cd-144">If you're using a Blueprint project, it can be easily converted to a C++ project by adding a C++ class:</span></span>  

1. <span data-ttu-id="428cd-145">Dans l’éditeur inréaliste, ouvrez le **fichier > nouvelle classe C++...**</span><span class="sxs-lookup"><span data-stu-id="428cd-145">In the Unreal editor, open **File > New C++ Class…**</span></span> <span data-ttu-id="428cd-146">et créez un **acteur** nommé **WinrtActor** pour exécuter le code dans la dll :</span><span class="sxs-lookup"><span data-stu-id="428cd-146">and create a new **Actor** named **WinrtActor** to run the code in the DLL:</span></span> 

![Configuration de la DLL](images/unreal-winrt-img-04.png)

> [!NOTE]
> <span data-ttu-id="428cd-148">Une solution a été créée dans le même répertoire que le fichier uproject, avec un nouveau script de compilation nommé source/ConsumeWinRT/ConsumerWinRT. Build. cs.</span><span class="sxs-lookup"><span data-stu-id="428cd-148">A solution has now been created in the same directory as the uproject file along with a new build script named Source/ConsumeWinRT/ConsumerWinRT.Build.cs.</span></span>

2. <span data-ttu-id="428cd-149">Ouvrez la solution, recherchez le dossier **Games/ConsumeWinRT/source/ConsumeWinRT** , puis ouvrez **ConsumeWinRT.Build.cs**:</span><span class="sxs-lookup"><span data-stu-id="428cd-149">Open the solution, browse for the **Games/ConsumeWinRT/Source/ConsumeWinRT** folder, and open **ConsumeWinRT.build.cs**:</span></span>

![Configuration de la DLL](images/unreal-winrt-img-05.png)

### <a name="linking-the-dll"></a><span data-ttu-id="428cd-151">Liaison de la DLL</span><span class="sxs-lookup"><span data-stu-id="428cd-151">Linking the DLL</span></span>
1. <span data-ttu-id="428cd-152">Dans **ConsumeWinRT.Build.cs**, ajoutez une propriété pour rechercher le chemin d’accès include pour la dll (répertoire contenant HoloLensWinrtDLL. h).</span><span class="sxs-lookup"><span data-stu-id="428cd-152">In **ConsumeWinRT.build.cs**, add a property to find the include path for the DLL (the directory containing HoloLensWinrtDLL.h).</span></span> <span data-ttu-id="428cd-153">La DLL se trouve dans un répertoire enfant du chemin d’accès include. cette propriété sera donc utilisée comme répertoire racine binaire :</span><span class="sxs-lookup"><span data-stu-id="428cd-153">The DLL is in a child directory to the include path, so this property will be used as the binary root dir:</span></span>

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

2. <span data-ttu-id="428cd-154">Dans le constructeur de classe, ajoutez le code suivant pour mettre à jour le chemin d’accès include, liez la nouvelle bibliothèque et Retardez le chargement, puis copiez la DLL dans l’emplacement AppX empaqueté :</span><span class="sxs-lookup"><span data-stu-id="428cd-154">In the class constructor, add the following code to update the include path, link the new lib, and delay-load and copy the DLL to the packaged appx location:</span></span>

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

3. <span data-ttu-id="428cd-155">Ouvrez **WinrtActor. h** et ajoutez deux définitions de fonction, une qui peut être utilisée par un plan et une autre qui utilise le code de la dll :</span><span class="sxs-lookup"><span data-stu-id="428cd-155">Open **WinrtActor.h** and add two function definitions, one that a blueprint can use and another that uses the DLL code:</span></span> 
```cpp
public:
    UFUNCTION(BlueprintCallable)
    static void OpenFileDialogue;
```

4. <span data-ttu-id="428cd-156">Ouvrez **WinrtActor. cpp** et chargez la dll dans BeginPlay :</span><span class="sxs-lookup"><span data-stu-id="428cd-156">Open **WinrtActor.cpp** and load the DLL in BeginPlay:</span></span> 

```cpp
void AWinfrtActor::BeginPlay()
{
#if PLATFORM_HOLOLENS
    HoloLensWinrtDLL::OpenFileDialogue();
#endif
}
``` 

>[!CAUTION]
> <span data-ttu-id="428cd-157">La DLL doit être chargée avant d’appeler l’une de ses fonctions.</span><span class="sxs-lookup"><span data-stu-id="428cd-157">The DLL must be loaded before calling any of its functions.</span></span>

### <a name="building-the-game"></a><span data-ttu-id="428cd-158">Création du jeu</span><span class="sxs-lookup"><span data-stu-id="428cd-158">Building the game</span></span>
1. <span data-ttu-id="428cd-159">Générez la solution Game pour lancer l’éditeur inréel ouvert dans le projet Game :</span><span class="sxs-lookup"><span data-stu-id="428cd-159">Build the game solution to launch the Unreal editor opened to the game project:</span></span> 
    * <span data-ttu-id="428cd-160">Dans l’onglet **Placer les acteurs** , recherchez le nouveau **WinrtActor** et faites-le glisser dans la scène.</span><span class="sxs-lookup"><span data-stu-id="428cd-160">In the **Place Actors** tab, search for the new **WinrtActor** and drag it into the scene</span></span> 
    * <span data-ttu-id="428cd-161">Ouvrez le plan de niveau pour exécuter la fonction Blueprint Callable dans **WinrtActor**</span><span class="sxs-lookup"><span data-stu-id="428cd-161">Open the level blueprint to execute the blueprint callable function in the **WinrtActor**</span></span> 

![Configuration de la DLL](images/unreal-winrt-img-06.png)

2. <span data-ttu-id="428cd-163">Dans le **monde entier**, recherchez le **WindrtActor** précédemment déposé dans la scène et faites-le glisser vers le plan de niveau :</span><span class="sxs-lookup"><span data-stu-id="428cd-163">In the **World Outliner**, find the **WindrtActor** previously dropped into the scene and drag it into the level blueprint:</span></span> 

![Configuration de la DLL](images/unreal-winrt-img-07.png)

3. <span data-ttu-id="428cd-165">Dans le plan de niveau, faites glisser le nœud de sortie à partir de WinrtActor, recherchez la **boîte de dialogue Ouvrir le fichier**, puis routez le nœud à partir de n’importe quelle entrée d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="428cd-165">In the level blueprint, drag the output node from WinrtActor, search for **Open File Dialogue**, then route the node from any user input.</span></span>  <span data-ttu-id="428cd-166">Dans ce cas, la boîte de dialogue Ouvrir un fichier est appelée à partir d’un événement vocal :</span><span class="sxs-lookup"><span data-stu-id="428cd-166">In this case, Open File Dialogue is being called from a speech event:</span></span> 

![Configuration de la DLL](images/unreal-winrt-img-08.png)

4. <span data-ttu-id="428cd-168">[Empaquetez ce jeu pour HoloLens](unreal-uxt-ch6.md), déployez-le et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="428cd-168">[Package this game for HoloLens](unreal-uxt-ch6.md), deploy it, and run.</span></span>  

<span data-ttu-id="428cd-169">Lorsque l’appel d’OpenFileDialogue n’est pas vrai, une boîte de dialogue fichier s’ouvre sur le fichier HoloLens invitant à entrer un nom de fichier. txt.</span><span class="sxs-lookup"><span data-stu-id="428cd-169">When Unreal calls OpenFileDialogue, a File Dialogue opens on the HoloLens prompting for a .txt file name.</span></span>  <span data-ttu-id="428cd-170">Une fois le fichier enregistré, accédez à l’onglet **Explorateur de fichiers** dans le portail de l’appareil pour afficher le contenu « Hello WinRT ».</span><span class="sxs-lookup"><span data-stu-id="428cd-170">After the file is saved, go to the **File explorer** tab in the device portal to see the contents “Hello WinRT”.</span></span> 

## <a name="summary"></a><span data-ttu-id="428cd-171">Résumé</span><span class="sxs-lookup"><span data-stu-id="428cd-171">Summary</span></span> 

<span data-ttu-id="428cd-172">Nous vous encourageons à utiliser le code de ce didacticiel comme point de départ pour consommer du code WinRT dans des conditions inréelles.</span><span class="sxs-lookup"><span data-stu-id="428cd-172">We encourage you to use the code in this tutorial as a starting point for consuming WinRT code in Unreal.</span></span>  <span data-ttu-id="428cd-173">Elle permet aux utilisateurs d’enregistrer des fichiers sur le disque HoloLens en utilisant la même boîte de dialogue de fichier que Windows.</span><span class="sxs-lookup"><span data-stu-id="428cd-173">It allows users to save files to the HoloLens disk using the same file dialogue as Windows.</span></span>  <span data-ttu-id="428cd-174">Suivez le même processus pour exporter toutes les fonctions supplémentaires à partir de l’en-tête HoloLensWinrtDLL et les utiliser dans Unreal.</span><span class="sxs-lookup"><span data-stu-id="428cd-174">Follow the same process to export any additional functions from the HoloLensWinrtDLL header and used in Unreal.</span></span>  <span data-ttu-id="428cd-175">Notez le code DLL qui attend un code WinRT asynchrone dans un thread MTA d’arrière-plan, ce qui évite le blocage du thread de jeu inréel.</span><span class="sxs-lookup"><span data-stu-id="428cd-175">Note the DLL code that waits on any async WinRT code in a background MTA thread, which avoids deadlocking the Unreal game thread.</span></span> 

## <a name="see-also"></a><span data-ttu-id="428cd-176">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="428cd-176">See also</span></span>
* [<span data-ttu-id="428cd-177">API C++/WinRT</span><span class="sxs-lookup"><span data-stu-id="428cd-177">C++/WinRT APIs</span></span>](https://docs.microsoft.com/windows/uwp/cpp-and-winrt-apis/)
* [<span data-ttu-id="428cd-178">FileSavePicker, classe</span><span class="sxs-lookup"><span data-stu-id="428cd-178">FileSavePicker class</span></span>](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) 
* [<span data-ttu-id="428cd-179">Bibliothèques tierces non réelles</span><span class="sxs-lookup"><span data-stu-id="428cd-179">Unreal Third-Party Libraries</span></span>](https://docs.unrealengine.com/Programming/BuildTools/UnrealBuildTool/ThirdPartyLibraries/index.html) 
