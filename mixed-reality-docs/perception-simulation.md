---
title: Simulation des perceptions
description: Guide d’utilisation de la bibliothèque de simulation de perception pour automatiser une entrée simulée pour des applications immersifs
author: pbarnettms
ms.author: pbarnett
ms.date: 05/12/2020
ms.topic: article
keywords: HoloLens, simulation, test
ms.openlocfilehash: 701fd39490d87b70df9bd68cc99da6482d41b676
ms.sourcegitcommit: 6d9d01d53137435c787f247f095d5255581695fc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/12/2020
ms.locfileid: "83228024"
---
# <a name="perception-simulation"></a><span data-ttu-id="8209b-104">Simulation des perceptions</span><span class="sxs-lookup"><span data-stu-id="8209b-104">Perception simulation</span></span>

<span data-ttu-id="8209b-105">Voulez-vous créer un test automatisé pour votre application ?</span><span class="sxs-lookup"><span data-stu-id="8209b-105">Do you want to build an automated test for your app?</span></span> <span data-ttu-id="8209b-106">Voulez-vous que vos tests vont au-delà des tests unitaires au niveau du composant et pour vraiment exercer votre application de bout en bout ?</span><span class="sxs-lookup"><span data-stu-id="8209b-106">Do you want your tests to go beyond component-level unit testing and really exercise your app end-to-end?</span></span> <span data-ttu-id="8209b-107">La simulation de perception correspond à ce que vous recherchez.</span><span class="sxs-lookup"><span data-stu-id="8209b-107">Perception Simulation is what you're looking for.</span></span> <span data-ttu-id="8209b-108">La bibliothèque de simulation de perception envoie des données d’entrée humaines et mondiales à votre application afin que vous puissiez automatiser vos tests.</span><span class="sxs-lookup"><span data-stu-id="8209b-108">The Perception Simulation library sends human and world input data to your app so you can automate your tests.</span></span> <span data-ttu-id="8209b-109">Par exemple, vous pouvez simuler l’entrée d’un utilisateur cherchant à une position renouvelée et spécifique, puis d’effectuer un mouvement ou d’utiliser un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="8209b-109">For example, you can simulate the input of a human looking to a specific, repeatable position and then performing a gesture or using a motion controller.</span></span>

<span data-ttu-id="8209b-110">La simulation de perception peut envoyer une entrée simulée comme celle-ci à un HoloLens physique, à l’émulateur HoloLens (1ère génération), à l’émulateur HoloLens 2 ou à un PC avec portail de réalité mixte installé.</span><span class="sxs-lookup"><span data-stu-id="8209b-110">Perception Simulation can send simulated input like this to a physical HoloLens, the HoloLens emulator (1st gen), the HoloLens 2 Emulator, or a PC with Mixed Reality Portal installed.</span></span> <span data-ttu-id="8209b-111">La simulation de perception contourne les capteurs actifs sur un appareil de réalité mixte et envoie une entrée simulée aux applications qui s’exécutent sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8209b-111">Perception Simulation bypasses the live sensors on a Mixed Reality device and sends simulated input to applications running on the device.</span></span> <span data-ttu-id="8209b-112">Les applications reçoivent ces événements d’entrée via les mêmes API qu’ils utilisent toujours et ne peuvent pas indiquer la différence entre l’exécution avec des capteurs réels et l’exécution avec la simulation de perception.</span><span class="sxs-lookup"><span data-stu-id="8209b-112">Applications receive these input events through the same APIs they always use and can't tell the difference between running with real sensors versus running with Perception Simulation.</span></span> <span data-ttu-id="8209b-113">La simulation de perception est la même technologie que celle utilisée par les émulateurs HoloLens pour envoyer une entrée simulée à la machine virtuelle HoloLens.</span><span class="sxs-lookup"><span data-stu-id="8209b-113">Perception Simulation is the same technology used by the HoloLens emulators to send simulated input to the HoloLens Virtual Machine.</span></span>

<span data-ttu-id="8209b-114">Pour commencer à utiliser la simulation dans votre code, commencez par créer un objet IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="8209b-114">To begin using simulation in your code, start by creating an IPerceptionSimulationManager object.</span></span> <span data-ttu-id="8209b-115">À partir de cet objet, vous pouvez émettre des commandes pour contrôler les propriétés d’un « humain » simulé, y compris la position de la tête, la position de la main et les gestes, et vous pouvez activer et manipuler les contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="8209b-115">From that object, you can issue commands to control properties of a simulated "human", including head position, hand position, and gestures, and you can enable and manipulate motion controllers.</span></span>

## <a name="setting-up-a-visual-studio-project-for-perception-simulation"></a><span data-ttu-id="8209b-116">Configuration d’un projet Visual Studio pour la simulation de perception</span><span class="sxs-lookup"><span data-stu-id="8209b-116">Setting Up a Visual Studio Project for Perception Simulation</span></span>
1. <span data-ttu-id="8209b-117">[Installez l’émulateur HoloLens](install-the-tools.md) sur votre PC de développement.</span><span class="sxs-lookup"><span data-stu-id="8209b-117">[Install the HoloLens emulator](install-the-tools.md) on your development PC.</span></span> <span data-ttu-id="8209b-118">L’émulateur comprend les bibliothèques que vous allez utiliser pour la simulation de perception.</span><span class="sxs-lookup"><span data-stu-id="8209b-118">The emulator includes the libraries you will use for Perception Simulation.</span></span>
2. <span data-ttu-id="8209b-119">Créez un projet de bureau Visual Studio C# (un projet de console fonctionne bien pour commencer).</span><span class="sxs-lookup"><span data-stu-id="8209b-119">Create a new Visual Studio C# desktop project (a Console Project works great to get started).</span></span>
3. <span data-ttu-id="8209b-120">Ajoutez les fichiers binaires suivants à votre projet en tant que références (Project->Add->Reference...). Vous pouvez les Rechercher dans% ProgramFiles (x86)% \ Microsoft XDE \\ (version), par exemple **% ProgramFiles (x86)% \ Microsoft XDE \\ 10.0.18362.0** pour l’émulateur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="8209b-120">Add the following binaries to your project as references (Project->Add->Reference...). You can find them in %ProgramFiles(x86)%\Microsoft XDE\\(version), such as **%ProgramFiles(x86)%\Microsoft XDE\\10.0.18362.0** for the HoloLens 2 Emulator.</span></span>  <span data-ttu-id="8209b-121">(Remarque : bien que les fichiers binaires fassent partie de l’émulateur HoloLens 2, ils fonctionnent également pour Windows Mixed Reality sur le bureau.) un.</span><span class="sxs-lookup"><span data-stu-id="8209b-121">(Note: although the binaries are part of the HoloLens 2 Emulator, they also work for Windows Mixed Reality on the desktop.) a.</span></span> <span data-ttu-id="8209b-122">PerceptionSimulationManager. Interop. dll-Wrapper C# managé pour la simulation de perception.</span><span class="sxs-lookup"><span data-stu-id="8209b-122">PerceptionSimulationManager.Interop.dll - Managed C# wrapper for Perception Simulation.</span></span>
    <span data-ttu-id="8209b-123">b.</span><span class="sxs-lookup"><span data-stu-id="8209b-123">b.</span></span> <span data-ttu-id="8209b-124">PerceptionSimulationRest. dll-Library pour la configuration d’un canal de communication de sockets Web vers le HoloLens ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="8209b-124">PerceptionSimulationRest.dll - Library for setting up a web-socket communication channel to the HoloLens or emulator.</span></span>
    <span data-ttu-id="8209b-125">c.</span><span class="sxs-lookup"><span data-stu-id="8209b-125">c.</span></span> <span data-ttu-id="8209b-126">SimulationStream. Interop. dll : types partagés pour la simulation.</span><span class="sxs-lookup"><span data-stu-id="8209b-126">SimulationStream.Interop.dll - Shared types for simulation.</span></span>
4. <span data-ttu-id="8209b-127">Ajoutez le fichier binaire d’implémentation PerceptionSimulationManager. dll à votre projet a.</span><span class="sxs-lookup"><span data-stu-id="8209b-127">Add the implementation binary PerceptionSimulationManager.dll to your project a.</span></span> <span data-ttu-id="8209b-128">Tout d’abord, ajoutez-le en tant que fichier binaire au projet (Project->ajouter >élément existant...). Enregistrez-le en tant que lien afin qu’il ne soit pas copié dans le dossier source de votre projet.</span><span class="sxs-lookup"><span data-stu-id="8209b-128">First add it as a binary to the project (Project->Add->Existing Item...). Save it as a link so that it doesn't copy it to your project source folder.</span></span> <span data-ttu-id="8209b-129">![Ajoutez PerceptionSimulationManager. dll au projet en tant que lien ](images/saveaslink.png) b.</span><span class="sxs-lookup"><span data-stu-id="8209b-129">![Add PerceptionSimulationManager.dll to the project as a link](images/saveaslink.png) b.</span></span> <span data-ttu-id="8209b-130">Ensuite, assurez-vous qu’il est copié dans votre dossier de sortie lors de la génération.</span><span class="sxs-lookup"><span data-stu-id="8209b-130">Then make sure that it get's copied to your output folder on build.</span></span> <span data-ttu-id="8209b-131">Il s’agit de la feuille de propriétés pour le binaire.</span><span class="sxs-lookup"><span data-stu-id="8209b-131">This is in the property sheet for the binary .</span></span> <span data-ttu-id="8209b-132">![Marquer PerceptionSimulationManager. dll pour copier dans le répertoire de sortie](images/copyalways.png)</span><span class="sxs-lookup"><span data-stu-id="8209b-132">![Mark PerceptionSimulationManager.dll to copy to the output directory](images/copyalways.png)</span></span>
5. <span data-ttu-id="8209b-133">Définissez la plateforme de votre solution active sur x64.</span><span class="sxs-lookup"><span data-stu-id="8209b-133">Set your active solution platform to x64.</span></span>  <span data-ttu-id="8209b-134">(Utilisez la Configuration Manager pour créer une entrée de plateforme pour x64, si elle n’existe pas déjà.)</span><span class="sxs-lookup"><span data-stu-id="8209b-134">(Use the Configuration Manager to create a Platform entry for x64 if one does not already exist.)</span></span>

## <a name="creating-an-iperceptionsimulation-manager-object"></a><span data-ttu-id="8209b-135">Création d’un objet IPerceptionSimulation Manager</span><span class="sxs-lookup"><span data-stu-id="8209b-135">Creating an IPerceptionSimulation Manager Object</span></span>

<span data-ttu-id="8209b-136">Pour contrôler la simulation, vous allez émettre des mises à jour des objets récupérés à partir d’un objet IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="8209b-136">To control simulation, you'll issue updates to objects retrieved from an IPerceptionSimulationManager object.</span></span> <span data-ttu-id="8209b-137">La première étape consiste à obtenir cet objet et à le connecter à votre appareil ou émulateur cible.</span><span class="sxs-lookup"><span data-stu-id="8209b-137">The first step is to get that object and connect it to your target device or emulator.</span></span> <span data-ttu-id="8209b-138">Vous pouvez récupérer l’adresse IP de votre émulateur en cliquant sur le bouton du portail de l’appareil dans la [barre d’outils](using-the-hololens-emulator.md) .</span><span class="sxs-lookup"><span data-stu-id="8209b-138">You can get the IP address of your emulator by clicking on the Device Portal button in the [toolbar](using-the-hololens-emulator.md)</span></span>

<span data-ttu-id="8209b-139">![Icône Ouvrir le portail de l’appareil ](images/emulator-deviceportal.png) **ouvrir le portail**de l’appareil : Ouvrez le portail de périphériques Windows pour le système d’exploitation HoloLens dans l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="8209b-139">![Open Device Portal icon](images/emulator-deviceportal.png) **Open Device Portal**: Open the Windows Device Portal for the HoloLens OS in the emulator.</span></span>  <span data-ttu-id="8209b-140">Pour Windows Mixed Reality, vous pouvez le récupérer dans l’application paramètres sous « mettre à jour & sécurité », puis « pour les développeurs » dans la section « se connecter à l’aide de » sous « activer le portail d’appareils ».</span><span class="sxs-lookup"><span data-stu-id="8209b-140">For Windows Mixed Reality, this can be retrieved in the Settings app under "Update & Security", then "For developers" in the "Connect using:" section under "Enable Device Portal."</span></span>  <span data-ttu-id="8209b-141">Veillez à noter l’adresse IP et le port.</span><span class="sxs-lookup"><span data-stu-id="8209b-141">Be sure to note both the IP address and port.</span></span>

<span data-ttu-id="8209b-142">Tout d’abord, vous devez appeler RestSimulationStreamSink. Create pour obtenir un objet RestSimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="8209b-142">First, you'll call RestSimulationStreamSink.Create to get a RestSimulationStreamSink object.</span></span> <span data-ttu-id="8209b-143">Il s’agit de l’appareil ou de l’émulateur cible que vous allez contrôler sur une connexion http.</span><span class="sxs-lookup"><span data-stu-id="8209b-143">This is the target device or emulator that you will control over an http connection.</span></span> <span data-ttu-id="8209b-144">Vos commandes sont transmises à et gérées par le [portail de périphériques Windows](using-the-windows-device-portal.md) exécuté sur l’appareil ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="8209b-144">Your commands will be passed to and handled by the [Windows Device Portal](using-the-windows-device-portal.md) running on the device or emulator.</span></span> <span data-ttu-id="8209b-145">Les quatre paramètres dont vous avez besoin pour créer un objet sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="8209b-145">The four parameters you'll need to create an object are:</span></span>
* <span data-ttu-id="8209b-146">URI Uri : adresse IP de l’appareil cible (par exemple, « https://123.123.123.123 » ou «» https://123.123.123.123:50080 )</span><span class="sxs-lookup"><span data-stu-id="8209b-146">Uri uri - IP address of the target device (e.g., "https://123.123.123.123" or "https://123.123.123.123:50080")</span></span>
* <span data-ttu-id="8209b-147">Informations d’identification System .net. NetworkCredential-nom d’utilisateur/mot de passe pour la connexion au [portail d’appareils Windows](using-the-windows-device-portal.md) sur l’appareil ou l’émulateur cible.</span><span class="sxs-lookup"><span data-stu-id="8209b-147">System.Net.NetworkCredential credentials - Username/password for connecting to the [Windows Device Portal](using-the-windows-device-portal.md) on the target device or emulator.</span></span> <span data-ttu-id="8209b-148">Si vous vous connectez à l’émulateur via son adresse locale (par exemple,*168...* \*) sur le même PC, toutes les informations d’identification seront acceptées.</span><span class="sxs-lookup"><span data-stu-id="8209b-148">If you are connecting to the emulator via its local address (e.g., 168.*.*.\*) on the same PC, any credentials will be accepted.</span></span>
* <span data-ttu-id="8209b-149">bool normal-true pour la priorité normale, false pour basse priorité.</span><span class="sxs-lookup"><span data-stu-id="8209b-149">bool normal - True for normal priority, false for low priority.</span></span> <span data-ttu-id="8209b-150">Vous souhaitez généralement définir cette propriété sur *true* pour les scénarios de test, ce qui permet à votre test de prendre le contrôle.</span><span class="sxs-lookup"><span data-stu-id="8209b-150">You generally want to set this to *true* for test scenarios, which allows your test to take control.</span></span>  <span data-ttu-id="8209b-151">La simulation de l’émulateur et de la réalité mixte Windows utilise des connexions de faible priorité.</span><span class="sxs-lookup"><span data-stu-id="8209b-151">The emulator and Windows Mixed Reality simulation use low priority connections.</span></span>  <span data-ttu-id="8209b-152">Si votre test utilise également une connexion de faible priorité, la connexion établie le plus récemment sera Control.</span><span class="sxs-lookup"><span data-stu-id="8209b-152">If your test also uses a low priority connection, the most recently established connection will be in control.</span></span>
* <span data-ttu-id="8209b-153">Jeton-jeton System. Threading. CancellationToken pour annuler l’opération asynchrone.</span><span class="sxs-lookup"><span data-stu-id="8209b-153">System.Threading.CancellationToken token - Token to cancel the async operation.</span></span>

<span data-ttu-id="8209b-154">Ensuite, vous allez créer le IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="8209b-154">Second you will create the IPerceptionSimulationManager.</span></span> <span data-ttu-id="8209b-155">Il s’agit de l’objet que vous utilisez pour contrôler la simulation.</span><span class="sxs-lookup"><span data-stu-id="8209b-155">This is the object you use to control simulation.</span></span> <span data-ttu-id="8209b-156">Notez que cela doit également être fait dans une méthode Async.</span><span class="sxs-lookup"><span data-stu-id="8209b-156">Note that this must also be done in an async method.</span></span>

## <a name="control-the-simulated-human"></a><span data-ttu-id="8209b-157">Contrôler l’homme simulé</span><span class="sxs-lookup"><span data-stu-id="8209b-157">Control the simulated Human</span></span>

<span data-ttu-id="8209b-158">Un IPerceptionSimulationManager a une propriété humaine qui retourne un objet ISimulatedHuman.</span><span class="sxs-lookup"><span data-stu-id="8209b-158">An IPerceptionSimulationManager has a Human property that returns an ISimulatedHuman object.</span></span> <span data-ttu-id="8209b-159">Pour contrôler l’homme simulé, effectuez des opérations sur cet objet.</span><span class="sxs-lookup"><span data-stu-id="8209b-159">To control the simulated human, perform operations on this object.</span></span> <span data-ttu-id="8209b-160">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8209b-160">For example:</span></span>

```
manager.Human.Move(new Vector3(0.1f, 0.0f, 0.0f))
```

## <a name="basic-sample-c-console-application"></a><span data-ttu-id="8209b-161">Exemple d’application de console C# de base</span><span class="sxs-lookup"><span data-stu-id="8209b-161">Basic Sample C# console application</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.PerceptionSimulation;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            Task.Run(async () =>
            {
                RestSimulationStreamSink sink = null;
                CancellationToken token = new System.Threading.CancellationToken();

                try
                {
                    sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("https://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        token);

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e);
                }

                // Always close the sink to return control to the previous application.
                if (sink != null)
                {
                    await sink.Close(token);
                }
            });

            // If main exits, the process exits.  
            Console.WriteLine("Press any key to exit...");
            Console.ReadLine();
        }
    }
}
```

## <a name="extended-sample-c-console-application"></a><span data-ttu-id="8209b-162">Exemple d’application de console C# étendue</span><span class="sxs-lookup"><span data-stu-id="8209b-162">Extended Sample C# console application</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.PerceptionSimulation;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            RestSimulationStreamSink sink = null;
            CancellationToken token = new System.Threading.CancellationToken();

            Task.Run(async () =>
            {
                try
                {
                    sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("https://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        token);

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);

                    // Now, we'll simulate a sequence of actions.
                    // Sleeps in-between each action give time to the system
                    // to be able to properly react.
                    // This is just an example. A proper automated test should verify
                    // that the app has behaved correctly
                    // before proceeding to the next step, instead of using Sleeps.

                    // Activate the right hand
                    manager.Human.RightHand.Activated = true;

                    // Simulate Bloom gesture, which should cause Shell to disappear
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);

                    // Simulate Bloom gesture again... this time, Shell should reappear
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);

                    // Simulate a Head rotation down around the X axis
                    // This should cause gaze to aim about the center of the screen
                    manager.Human.Head.Rotate(new Rotation3(0.04f, 0.0f, 0.0f));
                    Thread.Sleep(300);

                    // Simulate a finger press & release
                    // Should cause a tap on the center tile, thus launching it
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(2000);

                    // Simulate a second finger press & release
                    // Should activate the app that was launched when the center tile was clicked
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(5000);

                    // Simulate a Head rotation towards the upper right corner
                    manager.Human.Head.Rotate(new Rotation3(-0.14f, 0.17f, 0.0f));
                    Thread.Sleep(300);

                    // Simulate a third finger press & release
                    // Should press the Remove button on the app
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(2000);

                    // Simulate Bloom gesture again... bringing the Shell back once more
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e);
                }
            });

            // If main exits, the process exits.  
            Console.WriteLine("Press any key to exit...");
            Console.ReadLine();

            // Always close the sink to return control to the previous application.
            if (sink != null)
            {
                sink.Close(token);
            }
        }
    }
}
```

## <a name="note-on-6-dof-controllers"></a><span data-ttu-id="8209b-163">Remarque sur les contrôleurs 6-DDL</span><span class="sxs-lookup"><span data-stu-id="8209b-163">Note on 6-DOF controllers</span></span>

<span data-ttu-id="8209b-164">Avant d’appeler des propriétés sur des méthodes sur un contrôleur 6-DDL simulé, vous devez activer le contrôleur.</span><span class="sxs-lookup"><span data-stu-id="8209b-164">Before calling any properties on methods on a simulated 6-DOF controller, you must activate the controller.</span></span>  <span data-ttu-id="8209b-165">Si ce n’est pas le cas, une exception est générée.</span><span class="sxs-lookup"><span data-stu-id="8209b-165">Not doing so will result in an exception.</span></span>  <span data-ttu-id="8209b-166">À compter de la mise à jour de Windows 10 2019 mai, les contrôleurs 6-DDL simulés peuvent être installés et activés en définissant la propriété Status sur l’objet ISimulatedSixDofController sur SimulatedSixDofControllerStatus. active.</span><span class="sxs-lookup"><span data-stu-id="8209b-166">Starting with the Windows 10 May 2019 Update, simulated 6-DOF controllers can be installed and activated by setting the Status property on the ISimulatedSixDofController object to SimulatedSixDofControllerStatus.Active.</span></span>
<span data-ttu-id="8209b-167">Dans la mise à jour 2018 de Windows 10 octobre et les versions antérieures, vous devez d’abord installer séparément un contrôleur 6-DDL simulé en appelant l’outil PerceptionSimulationDevice situé dans le dossier \Windows\System32.</span><span class="sxs-lookup"><span data-stu-id="8209b-167">In the Windows 10 October 2018 Update and earlier, you must separately install a simulated 6-DOF controller first by calling the PerceptionSimulationDevice tool located in the \Windows\System32 folder.</span></span>  <span data-ttu-id="8209b-168">L’utilisation de cet outil est la suivante :</span><span class="sxs-lookup"><span data-stu-id="8209b-168">The usage of this tool is as follows:</span></span>


```
    PerceptionSimulationDevice.exe <action> 6dof <instance>
```

<span data-ttu-id="8209b-169">Par exemple</span><span class="sxs-lookup"><span data-stu-id="8209b-169">For example</span></span>

```
    PerceptionSimulationDevice.exe i 6dof 1
```

<span data-ttu-id="8209b-170">Les actions prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="8209b-170">Supported actions are:</span></span>
* <span data-ttu-id="8209b-171">i = installation</span><span class="sxs-lookup"><span data-stu-id="8209b-171">i = install</span></span>
* <span data-ttu-id="8209b-172">q = requête</span><span class="sxs-lookup"><span data-stu-id="8209b-172">q = query</span></span>
* <span data-ttu-id="8209b-173">r = supprimer</span><span class="sxs-lookup"><span data-stu-id="8209b-173">r = remove</span></span>

<span data-ttu-id="8209b-174">Les instances prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="8209b-174">Supported instances are:</span></span>
* <span data-ttu-id="8209b-175">1 = le contrôleur 6-DDL de gauche</span><span class="sxs-lookup"><span data-stu-id="8209b-175">1 = the left 6-DOF controller</span></span>
* <span data-ttu-id="8209b-176">2 = le contrôleur 6-DDL correct</span><span class="sxs-lookup"><span data-stu-id="8209b-176">2 = the right 6-DOF controller</span></span>

<span data-ttu-id="8209b-177">Le code de sortie du processus indique la réussite (valeur de retour zéro) ou l’échec (valeur de retour différente de zéro).</span><span class="sxs-lookup"><span data-stu-id="8209b-177">The exit code of the process will indicate success (a zero return value) or failure (a non-zero return value).</span></span>  <span data-ttu-id="8209b-178">Lorsque vous utilisez l’action q pour demander si un contrôleur est installé ou non, la valeur de retour est zéro (0) si le contrôleur n’est pas déjà installé ou un (1) si le contrôleur est installé.</span><span class="sxs-lookup"><span data-stu-id="8209b-178">When using the 'q' action to query whether or not a controller is installed, the return value will be zero (0) if the controller is not already installed or one (1) if the controller is installed.</span></span>

<span data-ttu-id="8209b-179">Lorsque vous supprimez un contrôleur sur la mise à jour 2018 de Windows 10 octobre ou une version antérieure, définissez son état sur OFF via l’API en premier, puis appelez l’outil PerceptionSimulationDevice.</span><span class="sxs-lookup"><span data-stu-id="8209b-179">When removing a controller on the Windows 10 October 2018 Update or earlier, set its status to Off via the API first, then call the PerceptionSimulationDevice tool.</span></span>

<span data-ttu-id="8209b-180">Notez que cet outil doit être exécuté en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8209b-180">Note that this tool must be run as Administrator.</span></span>




## <a name="api-reference"></a><span data-ttu-id="8209b-181">Référence API</span><span class="sxs-lookup"><span data-stu-id="8209b-181">API Reference</span></span>

### <a name="microsoftperceptionsimulationsimulateddevicetype"></a><span data-ttu-id="8209b-182">Microsoft. PerceptionSimulation. SimulatedDeviceType</span><span class="sxs-lookup"><span data-stu-id="8209b-182">Microsoft.PerceptionSimulation.SimulatedDeviceType</span></span>

<span data-ttu-id="8209b-183">Décrit un type d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="8209b-183">Describes a simulated device type</span></span>

```
public enum SimulatedDeviceType
{
    Reference = 0
}
```

<span data-ttu-id="8209b-184">**Microsoft. PerceptionSimulation. SimulatedDeviceType. Reference**</span><span class="sxs-lookup"><span data-stu-id="8209b-184">**Microsoft.PerceptionSimulation.SimulatedDeviceType.Reference**</span></span>

<span data-ttu-id="8209b-185">Un appareil de référence fictif, la valeur par défaut pour PerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="8209b-185">A fictitious reference device, the default for PerceptionSimulationManager</span></span>

### <a name="microsoftperceptionsimulationheadtrackermode"></a><span data-ttu-id="8209b-186">Microsoft. PerceptionSimulation. HeadTrackerMode</span><span class="sxs-lookup"><span data-stu-id="8209b-186">Microsoft.PerceptionSimulation.HeadTrackerMode</span></span>

<span data-ttu-id="8209b-187">Décrit un mode de suivi d’en-tête</span><span class="sxs-lookup"><span data-stu-id="8209b-187">Describes a head tracker mode</span></span>

```
public enum HeadTrackerMode
{
    Default = 0,
    Orientation = 1,
    Position = 2
}
```

<span data-ttu-id="8209b-188">**Microsoft. PerceptionSimulation. HeadTrackerMode. default**</span><span class="sxs-lookup"><span data-stu-id="8209b-188">**Microsoft.PerceptionSimulation.HeadTrackerMode.Default**</span></span>

<span data-ttu-id="8209b-189">Suivi des en-têtes par défaut.</span><span class="sxs-lookup"><span data-stu-id="8209b-189">Default Head Tracking.</span></span> <span data-ttu-id="8209b-190">Cela signifie que le système peut sélectionner le mode de suivi optimal en fonction des conditions d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8209b-190">This means the system may select the best head tracking mode based upon runtime conditions.</span></span>

<span data-ttu-id="8209b-191">**Microsoft. PerceptionSimulation. HeadTrackerMode. orientation**</span><span class="sxs-lookup"><span data-stu-id="8209b-191">**Microsoft.PerceptionSimulation.HeadTrackerMode.Orientation**</span></span>

<span data-ttu-id="8209b-192">Suivi d’en-tête d’orientation uniquement.</span><span class="sxs-lookup"><span data-stu-id="8209b-192">Orientation Only Head Tracking.</span></span> <span data-ttu-id="8209b-193">Cela signifie que la position suivie peut ne pas être fiable, et certaines fonctionnalités qui dépendent de la position de la tête peuvent ne pas être disponibles.</span><span class="sxs-lookup"><span data-stu-id="8209b-193">This means that the tracked position may not be reliable, and some functionality dependent on head position may not be available.</span></span>

<span data-ttu-id="8209b-194">**Microsoft. PerceptionSimulation. HeadTrackerMode. position**</span><span class="sxs-lookup"><span data-stu-id="8209b-194">**Microsoft.PerceptionSimulation.HeadTrackerMode.Position**</span></span>

<span data-ttu-id="8209b-195">Suivi de l’en-tête positionnel.</span><span class="sxs-lookup"><span data-stu-id="8209b-195">Positional Head Tracking.</span></span> <span data-ttu-id="8209b-196">Cela signifie que la position et l’orientation de la tête de suivi sont fiables</span><span class="sxs-lookup"><span data-stu-id="8209b-196">This means that the tracked head position and orientation are both reliable</span></span>

### <a name="microsoftperceptionsimulationsimulatedgesture"></a><span data-ttu-id="8209b-197">Microsoft. PerceptionSimulation. SimulatedGesture</span><span class="sxs-lookup"><span data-stu-id="8209b-197">Microsoft.PerceptionSimulation.SimulatedGesture</span></span>

<span data-ttu-id="8209b-198">Décrit un mouvement simulé</span><span class="sxs-lookup"><span data-stu-id="8209b-198">Describes a simulated gesture</span></span>

```
public enum SimulatedGesture
{
    None = 0,
    FingerPressed = 1,
    FingerReleased = 2,
    Home = 4,
    Max = Home
}
```

<span data-ttu-id="8209b-199">**Microsoft. PerceptionSimulation. SimulatedGesture. None**</span><span class="sxs-lookup"><span data-stu-id="8209b-199">**Microsoft.PerceptionSimulation.SimulatedGesture.None**</span></span>

<span data-ttu-id="8209b-200">Valeur de sentinelle utilisée pour indiquer l’absence de gestes.</span><span class="sxs-lookup"><span data-stu-id="8209b-200">A sentinel value used to indicate no gestures.</span></span>

<span data-ttu-id="8209b-201">**Microsoft. PerceptionSimulation. SimulatedGesture. FingerPressed**</span><span class="sxs-lookup"><span data-stu-id="8209b-201">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerPressed**</span></span>

<span data-ttu-id="8209b-202">Mouvement appuyé sur le doigt.</span><span class="sxs-lookup"><span data-stu-id="8209b-202">A finger pressed gesture.</span></span>

<span data-ttu-id="8209b-203">**Microsoft. PerceptionSimulation. SimulatedGesture. FingerReleased**</span><span class="sxs-lookup"><span data-stu-id="8209b-203">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerReleased**</span></span>

<span data-ttu-id="8209b-204">Mouvement de libération d’un doigt.</span><span class="sxs-lookup"><span data-stu-id="8209b-204">A finger released gesture.</span></span>

<span data-ttu-id="8209b-205">**Microsoft. PerceptionSimulation. SimulatedGesture. orig**</span><span class="sxs-lookup"><span data-stu-id="8209b-205">**Microsoft.PerceptionSimulation.SimulatedGesture.Home**</span></span>

<span data-ttu-id="8209b-206">Mouvement de démarrage/système.</span><span class="sxs-lookup"><span data-stu-id="8209b-206">The home/system gesture.</span></span>

<span data-ttu-id="8209b-207">**Microsoft. PerceptionSimulation. SimulatedGesture. Max**</span><span class="sxs-lookup"><span data-stu-id="8209b-207">**Microsoft.PerceptionSimulation.SimulatedGesture.Max**</span></span>

<span data-ttu-id="8209b-208">Mouvement maximal valide.</span><span class="sxs-lookup"><span data-stu-id="8209b-208">The maximum valid gesture.</span></span>

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerstatus"></a><span data-ttu-id="8209b-209">Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus</span><span class="sxs-lookup"><span data-stu-id="8209b-209">Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus</span></span>

<span data-ttu-id="8209b-210">États possibles d’un contrôleur 6-DDL simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-210">The possible states of a simulated 6-DOF controller.</span></span>

```
public enum SimulatedSixDofControllerStatus
{
    Off = 0,
    Active = 1,
    TrackingLost = 2,
}
```

<span data-ttu-id="8209b-211">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus. OFF**</span><span class="sxs-lookup"><span data-stu-id="8209b-211">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Off**</span></span>

<span data-ttu-id="8209b-212">Le contrôleur 6-DDL est désactivé.</span><span class="sxs-lookup"><span data-stu-id="8209b-212">The 6-DOF controller is turned off.</span></span>

<span data-ttu-id="8209b-213">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus. active**</span><span class="sxs-lookup"><span data-stu-id="8209b-213">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Active**</span></span>

<span data-ttu-id="8209b-214">Le contrôleur 6-DDL est activé et suivi.</span><span class="sxs-lookup"><span data-stu-id="8209b-214">The 6-DOF controller is turned on and tracked.</span></span>

<span data-ttu-id="8209b-215">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus. TrackingLost**</span><span class="sxs-lookup"><span data-stu-id="8209b-215">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.TrackingLost**</span></span>

<span data-ttu-id="8209b-216">Le contrôleur 6-DDL est activé, mais ne peut pas être suivi.</span><span class="sxs-lookup"><span data-stu-id="8209b-216">The 6-DOF controller is turned on but cannot be tracked.</span></span>

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerbutton"></a><span data-ttu-id="8209b-217">Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton</span><span class="sxs-lookup"><span data-stu-id="8209b-217">Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton</span></span>

<span data-ttu-id="8209b-218">Les boutons pris en charge sur un contrôleur 6-DDL simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-218">The supported buttons on a simulated 6-DOF controller.</span></span>

```
public enum SimulatedSixDofControllerButton
{
    None = 0,
    Home = 1,
    Menu = 2,
    Grip = 4,
    TouchpadPress = 8,
    Select = 16,
    TouchpadTouch = 32,
    Thumbstick = 64,
    Max = Thumbstick
}
```

<span data-ttu-id="8209b-219">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. None**</span><span class="sxs-lookup"><span data-stu-id="8209b-219">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.None**</span></span>

<span data-ttu-id="8209b-220">Valeur de sentinelle utilisée pour indiquer qu’aucun bouton n’est présent.</span><span class="sxs-lookup"><span data-stu-id="8209b-220">A sentinel value used to indicate no buttons.</span></span>

<span data-ttu-id="8209b-221">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. orig**</span><span class="sxs-lookup"><span data-stu-id="8209b-221">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Home**</span></span>

<span data-ttu-id="8209b-222">Le bouton d’hébergement est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="8209b-222">The Home button is pressed.</span></span>

<span data-ttu-id="8209b-223">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. menu**</span><span class="sxs-lookup"><span data-stu-id="8209b-223">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Menu**</span></span>

<span data-ttu-id="8209b-224">Le bouton de menu est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="8209b-224">The Menu button is pressed.</span></span>

<span data-ttu-id="8209b-225">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. poignée**</span><span class="sxs-lookup"><span data-stu-id="8209b-225">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Grip**</span></span>

<span data-ttu-id="8209b-226">Le bouton de la poignée est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="8209b-226">The Grip button is pressed.</span></span>

<span data-ttu-id="8209b-227">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. TouchpadPress**</span><span class="sxs-lookup"><span data-stu-id="8209b-227">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadPress**</span></span>

<span data-ttu-id="8209b-228">Le pavé tactile est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="8209b-228">The TouchPad is pressed.</span></span>

<span data-ttu-id="8209b-229">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. Select**</span><span class="sxs-lookup"><span data-stu-id="8209b-229">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Select**</span></span>

<span data-ttu-id="8209b-230">Le bouton Sélectionner est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="8209b-230">The Select button is pressed.</span></span>

<span data-ttu-id="8209b-231">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. TouchpadTouch**</span><span class="sxs-lookup"><span data-stu-id="8209b-231">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadTouch**</span></span>

<span data-ttu-id="8209b-232">Le pavé tactile est touché.</span><span class="sxs-lookup"><span data-stu-id="8209b-232">The TouchPad is touched.</span></span>

<span data-ttu-id="8209b-233">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. Stick**</span><span class="sxs-lookup"><span data-stu-id="8209b-233">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Thumbstick**</span></span>

<span data-ttu-id="8209b-234">Le stick analogique est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="8209b-234">The Thumbstick is pressed.</span></span>

<span data-ttu-id="8209b-235">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. Max**</span><span class="sxs-lookup"><span data-stu-id="8209b-235">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Max**</span></span>

<span data-ttu-id="8209b-236">Le bouton nombre maximal valide.</span><span class="sxs-lookup"><span data-stu-id="8209b-236">The maximum valid button.</span></span>


### <a name="microsoftperceptionsimulationsimulatedeyescalibrationstate"></a><span data-ttu-id="8209b-237">Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState</span><span class="sxs-lookup"><span data-stu-id="8209b-237">Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState</span></span>

<span data-ttu-id="8209b-238">État d’étalonnage des yeux simulés</span><span class="sxs-lookup"><span data-stu-id="8209b-238">The calibration state of the simulated eyes</span></span>

```
public enum SimulatedGesture
{
    Unavailable = 0,
    Ready = 1,
    Configuring = 2,
    UserCalibrationNeeded = 3
}
```

<span data-ttu-id="8209b-239">**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. non disponible**</span><span class="sxs-lookup"><span data-stu-id="8209b-239">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Unavailable**</span></span>

<span data-ttu-id="8209b-240">L’étalonnage des yeux n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="8209b-240">The eyes calibration is unavailable.</span></span>

<span data-ttu-id="8209b-241">**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. Ready**</span><span class="sxs-lookup"><span data-stu-id="8209b-241">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Ready**</span></span>

<span data-ttu-id="8209b-242">Les yeux ont été étalonnés.</span><span class="sxs-lookup"><span data-stu-id="8209b-242">The eyes have been calibrated.</span></span>  <span data-ttu-id="8209b-243">Il s’agit de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="8209b-243">This is the default value.</span></span>

<span data-ttu-id="8209b-244">**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. Configuration**</span><span class="sxs-lookup"><span data-stu-id="8209b-244">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Configuring**</span></span>

<span data-ttu-id="8209b-245">Les yeux sont calibrés.</span><span class="sxs-lookup"><span data-stu-id="8209b-245">The eyes are being calibrated.</span></span>

<span data-ttu-id="8209b-246">**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. UserCalibrationNeeded**</span><span class="sxs-lookup"><span data-stu-id="8209b-246">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.UserCalibrationNeeded**</span></span>

<span data-ttu-id="8209b-247">Les yeux doivent être étalonnés.</span><span class="sxs-lookup"><span data-stu-id="8209b-247">The eyes need to be calibrated.</span></span>

### <a name="microsoftperceptionsimulationsimulatedhandjointtrackingaccuracy"></a><span data-ttu-id="8209b-248">Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy</span><span class="sxs-lookup"><span data-stu-id="8209b-248">Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy</span></span>

<span data-ttu-id="8209b-249">Précision de suivi d’une jointure de la main.</span><span class="sxs-lookup"><span data-stu-id="8209b-249">The tracking accuracy of a joint of the hand.</span></span>

```
public enum SimulatedHandJointTrackingAccuracy
{
    Unavailable = 0,
    Approximate = 1,
    Visible = 2
}
```

<span data-ttu-id="8209b-250">**Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy. non disponible**</span><span class="sxs-lookup"><span data-stu-id="8209b-250">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Unavailable**</span></span>

<span data-ttu-id="8209b-251">La jointure n’est pas suivie.</span><span class="sxs-lookup"><span data-stu-id="8209b-251">The joint is not tracked.</span></span>

<span data-ttu-id="8209b-252">**Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy. approximatif**</span><span class="sxs-lookup"><span data-stu-id="8209b-252">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Approximate**</span></span>

<span data-ttu-id="8209b-253">La position conjointe est déduite.</span><span class="sxs-lookup"><span data-stu-id="8209b-253">The joint position is inferred.</span></span>

<span data-ttu-id="8209b-254">**Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy. visible**</span><span class="sxs-lookup"><span data-stu-id="8209b-254">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Visible**</span></span>

<span data-ttu-id="8209b-255">L’articulation est entièrement suivie.</span><span class="sxs-lookup"><span data-stu-id="8209b-255">The joint is fully tracked.</span></span>

### <a name="microsoftperceptionsimulationsimulatedhandpose"></a><span data-ttu-id="8209b-256">Microsoft. PerceptionSimulation. SimulatedHandPose</span><span class="sxs-lookup"><span data-stu-id="8209b-256">Microsoft.PerceptionSimulation.SimulatedHandPose</span></span>

<span data-ttu-id="8209b-257">Précision de suivi d’une jointure de la main.</span><span class="sxs-lookup"><span data-stu-id="8209b-257">The tracking accuracy of a joint of the hand.</span></span>

```
public enum SimulatedHandPose
{
    Closed = 0,
    Open = 1,
    Point = 2,
    Pinch = 3,
    Max = Pinch
}
```

<span data-ttu-id="8209b-258">**Microsoft. PerceptionSimulation. SimulatedHandPose. Closed**</span><span class="sxs-lookup"><span data-stu-id="8209b-258">**Microsoft.PerceptionSimulation.SimulatedHandPose.Closed**</span></span>

<span data-ttu-id="8209b-259">Les jointures Finger de la main sont configurées pour refléter une pose fermée.</span><span class="sxs-lookup"><span data-stu-id="8209b-259">The hand's finger joints are configured to reflect a closed pose.</span></span>

<span data-ttu-id="8209b-260">**Microsoft. PerceptionSimulation. SimulatedHandPose. Open**</span><span class="sxs-lookup"><span data-stu-id="8209b-260">**Microsoft.PerceptionSimulation.SimulatedHandPose.Open**</span></span>

<span data-ttu-id="8209b-261">Les jointures Finger de la main sont configurées pour refléter une pose ouverte.</span><span class="sxs-lookup"><span data-stu-id="8209b-261">The hand's finger joints are configured to reflect an open pose.</span></span>

<span data-ttu-id="8209b-262">**Microsoft. PerceptionSimulation. SimulatedHandPose. point**</span><span class="sxs-lookup"><span data-stu-id="8209b-262">**Microsoft.PerceptionSimulation.SimulatedHandPose.Point**</span></span>

<span data-ttu-id="8209b-263">Les jointures Finger de la main sont configurées pour refléter une pose de pointage.</span><span class="sxs-lookup"><span data-stu-id="8209b-263">The hand's finger joints are configured to reflect a pointing pose.</span></span>

<span data-ttu-id="8209b-264">**Microsoft. PerceptionSimulation. SimulatedHandPose. pincement**</span><span class="sxs-lookup"><span data-stu-id="8209b-264">**Microsoft.PerceptionSimulation.SimulatedHandPose.Pinch**</span></span>

<span data-ttu-id="8209b-265">Les jointures Finger de la main sont configurées pour refléter une pose de pincement.</span><span class="sxs-lookup"><span data-stu-id="8209b-265">The hand's finger joints are configured to reflect a pinching pose.</span></span>

<span data-ttu-id="8209b-266">**Microsoft. PerceptionSimulation. SimulatedHandPose. Max**</span><span class="sxs-lookup"><span data-stu-id="8209b-266">**Microsoft.PerceptionSimulation.SimulatedHandPose.Max**</span></span>

<span data-ttu-id="8209b-267">Valeur maximale valide pour SimulatedHandPose.</span><span class="sxs-lookup"><span data-stu-id="8209b-267">The maximum valid value for SimulatedHandPose.</span></span>


### <a name="microsoftperceptionsimulationplaybackstate"></a><span data-ttu-id="8209b-268">Microsoft. PerceptionSimulation. PlaybackState</span><span class="sxs-lookup"><span data-stu-id="8209b-268">Microsoft.PerceptionSimulation.PlaybackState</span></span>

<span data-ttu-id="8209b-269">Décrit l’état d’une lecture.</span><span class="sxs-lookup"><span data-stu-id="8209b-269">Describes the state of a playback.</span></span>

```
public enum PlaybackState
{
    Stopped = 0,
    Playing = 1,
    Paused = 2,
    End = 3,
}
```

<span data-ttu-id="8209b-270">**Microsoft. PerceptionSimulation. PlaybackState. Stopped**</span><span class="sxs-lookup"><span data-stu-id="8209b-270">**Microsoft.PerceptionSimulation.PlaybackState.Stopped**</span></span>

<span data-ttu-id="8209b-271">L’enregistrement est actuellement arrêté et prêt pour la lecture.</span><span class="sxs-lookup"><span data-stu-id="8209b-271">The recording is currently stopped and ready for playback.</span></span>

<span data-ttu-id="8209b-272">**Microsoft. PerceptionSimulation. PlaybackState. Playing**</span><span class="sxs-lookup"><span data-stu-id="8209b-272">**Microsoft.PerceptionSimulation.PlaybackState.Playing**</span></span>

<span data-ttu-id="8209b-273">L’enregistrement est en cours de diffusion.</span><span class="sxs-lookup"><span data-stu-id="8209b-273">The recording is currently playing.</span></span>

<span data-ttu-id="8209b-274">**Microsoft. PerceptionSimulation. PlaybackState. Paused**</span><span class="sxs-lookup"><span data-stu-id="8209b-274">**Microsoft.PerceptionSimulation.PlaybackState.Paused**</span></span>

<span data-ttu-id="8209b-275">L’enregistrement est actuellement suspendu.</span><span class="sxs-lookup"><span data-stu-id="8209b-275">The recording is currently paused.</span></span>

<span data-ttu-id="8209b-276">**Microsoft. PerceptionSimulation. PlaybackState. end**</span><span class="sxs-lookup"><span data-stu-id="8209b-276">**Microsoft.PerceptionSimulation.PlaybackState.End**</span></span>

<span data-ttu-id="8209b-277">L’enregistrement a atteint la fin.</span><span class="sxs-lookup"><span data-stu-id="8209b-277">The recording has reached the end.</span></span>

### <a name="microsoftperceptionsimulationvector3"></a><span data-ttu-id="8209b-278">Microsoft. PerceptionSimulation. Vector3</span><span class="sxs-lookup"><span data-stu-id="8209b-278">Microsoft.PerceptionSimulation.Vector3</span></span>

<span data-ttu-id="8209b-279">Décrit un vecteur de 3 composants, qui peut décrire un point ou un vecteur dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="8209b-279">Describes a 3 components vector, which might describe a point or a vector in 3D space.</span></span>

```
public struct Vector3
{
    public float X;
    public float Y;
    public float Z;
    public Vector3(float x, float y, float z);
}
```

<span data-ttu-id="8209b-280">**Microsoft. PerceptionSimulation. Vector3. X**</span><span class="sxs-lookup"><span data-stu-id="8209b-280">**Microsoft.PerceptionSimulation.Vector3.X**</span></span>

<span data-ttu-id="8209b-281">Composant X du vecteur.</span><span class="sxs-lookup"><span data-stu-id="8209b-281">The X component of the vector.</span></span>

<span data-ttu-id="8209b-282">**Microsoft. PerceptionSimulation. Vector3. Y**</span><span class="sxs-lookup"><span data-stu-id="8209b-282">**Microsoft.PerceptionSimulation.Vector3.Y**</span></span>

<span data-ttu-id="8209b-283">Composant Y du vecteur.</span><span class="sxs-lookup"><span data-stu-id="8209b-283">The Y component of the vector.</span></span>

<span data-ttu-id="8209b-284">**Microsoft. PerceptionSimulation. Vector3. Z**</span><span class="sxs-lookup"><span data-stu-id="8209b-284">**Microsoft.PerceptionSimulation.Vector3.Z**</span></span>

<span data-ttu-id="8209b-285">Composant Z du vecteur.</span><span class="sxs-lookup"><span data-stu-id="8209b-285">The Z component of the vector.</span></span>

<span data-ttu-id="8209b-286">**Microsoft. PerceptionSimulation. Vector3. #ctor (System. Single, System. Single, System. Single)**</span><span class="sxs-lookup"><span data-stu-id="8209b-286">**Microsoft.PerceptionSimulation.Vector3.#ctor(System.Single,System.Single,System.Single)**</span></span>

<span data-ttu-id="8209b-287">Construisez un nouveau Vector3.</span><span class="sxs-lookup"><span data-stu-id="8209b-287">Construct a new Vector3.</span></span>

<span data-ttu-id="8209b-288">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-288">Parameters</span></span>
* <span data-ttu-id="8209b-289">x-composant x du vecteur.</span><span class="sxs-lookup"><span data-stu-id="8209b-289">x - The x component of the vector.</span></span>
* <span data-ttu-id="8209b-290">y : composant y du vecteur.</span><span class="sxs-lookup"><span data-stu-id="8209b-290">y - The y component of the vector.</span></span>
* <span data-ttu-id="8209b-291">z-composant z du vecteur.</span><span class="sxs-lookup"><span data-stu-id="8209b-291">z - The z component of the vector.</span></span>

### <a name="microsoftperceptionsimulationrotation3"></a><span data-ttu-id="8209b-292">Microsoft. PerceptionSimulation. Rotation3</span><span class="sxs-lookup"><span data-stu-id="8209b-292">Microsoft.PerceptionSimulation.Rotation3</span></span>

<span data-ttu-id="8209b-293">Décrit une rotation de 3 composants.</span><span class="sxs-lookup"><span data-stu-id="8209b-293">Describes a 3 components rotation.</span></span>

```
public struct Rotation3
{
    public float Pitch;
    public float Yaw;
    public float Roll;
    public Rotation3(float pitch, float yaw, float roll);
}
```

<span data-ttu-id="8209b-294">**Microsoft. PerceptionSimulation. Rotation3. brai**</span><span class="sxs-lookup"><span data-stu-id="8209b-294">**Microsoft.PerceptionSimulation.Rotation3.Pitch**</span></span>

<span data-ttu-id="8209b-295">Composant de pas de la rotation, en hauteur autour de l’axe X.</span><span class="sxs-lookup"><span data-stu-id="8209b-295">The Pitch component of the Rotation, down around the X axis.</span></span>

<span data-ttu-id="8209b-296">**Microsoft. PerceptionSimulation. Rotation3. lacet**</span><span class="sxs-lookup"><span data-stu-id="8209b-296">**Microsoft.PerceptionSimulation.Rotation3.Yaw**</span></span>

<span data-ttu-id="8209b-297">Composant de lacet de la rotation, à droite autour de l’axe Y.</span><span class="sxs-lookup"><span data-stu-id="8209b-297">The Yaw component of the Rotation, right around the Y axis.</span></span>

<span data-ttu-id="8209b-298">**Microsoft. PerceptionSimulation. Rotation3. Roll**</span><span class="sxs-lookup"><span data-stu-id="8209b-298">**Microsoft.PerceptionSimulation.Rotation3.Roll**</span></span>

<span data-ttu-id="8209b-299">Composant de roulement de la rotation, à droite autour de l’axe Z.</span><span class="sxs-lookup"><span data-stu-id="8209b-299">The Roll component of the Rotation, right around the Z axis.</span></span>

<span data-ttu-id="8209b-300">**Microsoft. PerceptionSimulation. Rotation3. #ctor (System. Single, System. Single, System. Single)**</span><span class="sxs-lookup"><span data-stu-id="8209b-300">**Microsoft.PerceptionSimulation.Rotation3.#ctor(System.Single,System.Single,System.Single)**</span></span>

<span data-ttu-id="8209b-301">Construisez un nouveau Rotation3.</span><span class="sxs-lookup"><span data-stu-id="8209b-301">Construct a new Rotation3.</span></span>

<span data-ttu-id="8209b-302">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-302">Parameters</span></span>
* <span data-ttu-id="8209b-303">tangage : composant de pas de la rotation.</span><span class="sxs-lookup"><span data-stu-id="8209b-303">pitch - The pitch component of the Rotation.</span></span>
* <span data-ttu-id="8209b-304">lacet : composant de lacet de la rotation.</span><span class="sxs-lookup"><span data-stu-id="8209b-304">yaw - The yaw component of the Rotation.</span></span>
* <span data-ttu-id="8209b-305">Roll-le composant Roll de la rotation.</span><span class="sxs-lookup"><span data-stu-id="8209b-305">roll - The roll component of the Rotation.</span></span>

### <a name="microsoftperceptionsimulationsimulatedhandjointconfiguration"></a><span data-ttu-id="8209b-306">Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration</span><span class="sxs-lookup"><span data-stu-id="8209b-306">Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration</span></span>

<span data-ttu-id="8209b-307">Décrit la configuration d’un joint sur une main simulée.</span><span class="sxs-lookup"><span data-stu-id="8209b-307">Describes the configuration of a joint on a simulated hand.</span></span>

```
public struct SimulatedHandJointConfiguration
{
    public Vector3 Position;
    public Rotation3 Rotation;
    public SimulatedHandJointTrackingAccuracy TrackingAccuracy;
}
```

<span data-ttu-id="8209b-308">**Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration. position**</span><span class="sxs-lookup"><span data-stu-id="8209b-308">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Position**</span></span>

<span data-ttu-id="8209b-309">Position de la jointure.</span><span class="sxs-lookup"><span data-stu-id="8209b-309">The position of the joint.</span></span>

<span data-ttu-id="8209b-310">**Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration. rotation**</span><span class="sxs-lookup"><span data-stu-id="8209b-310">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Rotation**</span></span>

<span data-ttu-id="8209b-311">Rotation de la jointure.</span><span class="sxs-lookup"><span data-stu-id="8209b-311">The rotation of the joint.</span></span>

<span data-ttu-id="8209b-312">**Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration. TrackingAccuracy**</span><span class="sxs-lookup"><span data-stu-id="8209b-312">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.TrackingAccuracy**</span></span>

<span data-ttu-id="8209b-313">Précision de suivi de la jointure.</span><span class="sxs-lookup"><span data-stu-id="8209b-313">The tracking accuracy of the joint.</span></span>


### <a name="microsoftperceptionsimulationfrustum"></a><span data-ttu-id="8209b-314">Microsoft. PerceptionSimulation. frustum</span><span class="sxs-lookup"><span data-stu-id="8209b-314">Microsoft.PerceptionSimulation.Frustum</span></span>

<span data-ttu-id="8209b-315">Décrit un frustum d’affichage, tel qu’il est généralement utilisé par un appareil photo.</span><span class="sxs-lookup"><span data-stu-id="8209b-315">Describes a view frustum, as typically used by a camera.</span></span>

```
public struct Frustum
{
    float Near;
    float Far;
    float FieldOfView;
    float AspectRatio;
}
```

<span data-ttu-id="8209b-316">**Microsoft. PerceptionSimulation. frustum. Near**</span><span class="sxs-lookup"><span data-stu-id="8209b-316">**Microsoft.PerceptionSimulation.Frustum.Near**</span></span>

<span data-ttu-id="8209b-317">Distance minimale contenue dans le frustum.</span><span class="sxs-lookup"><span data-stu-id="8209b-317">The minimum distance that is contained in the frustum.</span></span>

<span data-ttu-id="8209b-318">**Microsoft. PerceptionSimulation. frustum. Far**</span><span class="sxs-lookup"><span data-stu-id="8209b-318">**Microsoft.PerceptionSimulation.Frustum.Far**</span></span>

<span data-ttu-id="8209b-319">Distance maximale contenue dans le frustum.</span><span class="sxs-lookup"><span data-stu-id="8209b-319">The maximum distance that is contained in the frustum.</span></span>

<span data-ttu-id="8209b-320">**Microsoft. PerceptionSimulation. frustum. FieldOfView**</span><span class="sxs-lookup"><span data-stu-id="8209b-320">**Microsoft.PerceptionSimulation.Frustum.FieldOfView**</span></span>

<span data-ttu-id="8209b-321">Champ horizontal de la vue de frustum, en radians (inférieur à PI).</span><span class="sxs-lookup"><span data-stu-id="8209b-321">The horizontal field of view of the frustum, in radians (less than PI).</span></span>

<span data-ttu-id="8209b-322">**Microsoft. PerceptionSimulation. frustum. AspectRatio**</span><span class="sxs-lookup"><span data-stu-id="8209b-322">**Microsoft.PerceptionSimulation.Frustum.AspectRatio**</span></span>

<span data-ttu-id="8209b-323">Rapport entre le champ horizontal de la vue et le champ vertical de l’affichage.</span><span class="sxs-lookup"><span data-stu-id="8209b-323">The ratio of horizontal field of view to vertical field of view.</span></span>

### <a name="microsoftperceptionsimulationsimulateddisplayconfiguration"></a><span data-ttu-id="8209b-324">Microsoft. PerceptionSimulation. SimulatedDisplayConfiguration</span><span class="sxs-lookup"><span data-stu-id="8209b-324">Microsoft.PerceptionSimulation.SimulatedDisplayConfiguration</span></span>

<span data-ttu-id="8209b-325">Décrit la configuration de l’affichage du casque simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-325">Describes the configuration of the simulated headset's display.</span></span>

```
public struct SimulatedDisplayConfiguration
{
    public Vector3 LeftEyePosition;
    public Rotation3 LeftEyeRotation;
    public Vector3 RightEyePosition;
    public Rotation3 RightEyeRotation;
    public float Ipd;
    public bool ApplyEyeTransforms;
    public bool ApplyIpd;
}
```

<span data-ttu-id="8209b-326">**Microsoft. PerceptionSimulation. SimulatedDisplayConfiguration. LeftEyePosition**</span><span class="sxs-lookup"><span data-stu-id="8209b-326">**Microsoft.PerceptionSimulation.SimulatedDisplayConfiguration.LeftEyePosition**</span></span>

<span data-ttu-id="8209b-327">Transformation à partir du centre de la tête vers l’œil gauche à des fins de rendu stéréo.</span><span class="sxs-lookup"><span data-stu-id="8209b-327">The transform from the center of the head to the left eye for purposes of stereo rendering.</span></span>

<span data-ttu-id="8209b-328">**Microsoft. PerceptionSimulation. SimulatedDisplayConfiguration. LeftEyeRotation**</span><span class="sxs-lookup"><span data-stu-id="8209b-328">**Microsoft.PerceptionSimulation.SimulatedDisplayConfiguration.LeftEyeRotation**</span></span>

<span data-ttu-id="8209b-329">Rotation de l’œil gauche à des fins de rendu stéréo.</span><span class="sxs-lookup"><span data-stu-id="8209b-329">The rotation of the left eye for purposes of stereo rendering.</span></span>

<span data-ttu-id="8209b-330">**Microsoft. PerceptionSimulation. SimulatedDisplayConfiguration. RightEyePosition**</span><span class="sxs-lookup"><span data-stu-id="8209b-330">**Microsoft.PerceptionSimulation.SimulatedDisplayConfiguration.RightEyePosition**</span></span>

<span data-ttu-id="8209b-331">Transformation à partir du centre de la tête vers le bon œil à des fins de rendu stéréo.</span><span class="sxs-lookup"><span data-stu-id="8209b-331">The transform from the center of the head to the right eye for purposes of stereo rendering.</span></span>

<span data-ttu-id="8209b-332">**Microsoft. PerceptionSimulation. SimulatedDisplayConfiguration. RightEyeRotation**</span><span class="sxs-lookup"><span data-stu-id="8209b-332">**Microsoft.PerceptionSimulation.SimulatedDisplayConfiguration.RightEyeRotation**</span></span>

<span data-ttu-id="8209b-333">Rotation de l’œil droit à des fins de rendu stéréo.</span><span class="sxs-lookup"><span data-stu-id="8209b-333">The rotation of the right eye for purposes of stereo rendering.</span></span>

<span data-ttu-id="8209b-334">**Microsoft. PerceptionSimulation. SimulatedDisplayConfiguration. IPD**</span><span class="sxs-lookup"><span data-stu-id="8209b-334">**Microsoft.PerceptionSimulation.SimulatedDisplayConfiguration.Ipd**</span></span>

<span data-ttu-id="8209b-335">Valeur IPD signalée par le système à des fins de rendu stéréo.</span><span class="sxs-lookup"><span data-stu-id="8209b-335">The Ipd value reported by the system for purposes of stereo rendering.</span></span>

<span data-ttu-id="8209b-336">**Microsoft. PerceptionSimulation. SimulatedDisplayConfiguration. ApplyEyeTransforms**</span><span class="sxs-lookup"><span data-stu-id="8209b-336">**Microsoft.PerceptionSimulation.SimulatedDisplayConfiguration.ApplyEyeTransforms**</span></span>

<span data-ttu-id="8209b-337">Indique si les valeurs fournies pour les transformations d’œil gauche et droit doivent être considérées comme valides et appliquées au système en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8209b-337">Whether or not the values provided for left and right eye transforms should be considered valid and applied to the running system.</span></span>

<span data-ttu-id="8209b-338">**Microsoft. PerceptionSimulation. SimulatedDisplayConfiguration. ApplyIpd**</span><span class="sxs-lookup"><span data-stu-id="8209b-338">**Microsoft.PerceptionSimulation.SimulatedDisplayConfiguration.ApplyIpd**</span></span>

<span data-ttu-id="8209b-339">Indique si la valeur fournie pour IPD doit être considérée comme valide et appliquée au système en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8209b-339">Whether or not the value provided for Ipd should be considered valid and applied to the running system.</span></span>


### <a name="microsoftperceptionsimulationiperceptionsimulationmanager"></a><span data-ttu-id="8209b-340">Microsoft. PerceptionSimulation. IPerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="8209b-340">Microsoft.PerceptionSimulation.IPerceptionSimulationManager</span></span>

<span data-ttu-id="8209b-341">Racine pour la génération des paquets utilisés pour contrôler un appareil.</span><span class="sxs-lookup"><span data-stu-id="8209b-341">Root for generating the packets used to control a device.</span></span>

```
public interface IPerceptionSimulationManager
{   
    ISimulatedDevice Device { get; }
    ISimulatedHuman Human { get; }
    void Reset();
}
```

<span data-ttu-id="8209b-342">**Microsoft. PerceptionSimulation. IPerceptionSimulationManager. Device**</span><span class="sxs-lookup"><span data-stu-id="8209b-342">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Device**</span></span>

<span data-ttu-id="8209b-343">Récupérez l’objet d’appareil simulé qui interprète l’homme simulé et le monde simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-343">Retrieve the simulated device object that interprets the simulated human and the simulated world.</span></span>

<span data-ttu-id="8209b-344">**Microsoft. PerceptionSimulation. IPerceptionSimulationManager. Human**</span><span class="sxs-lookup"><span data-stu-id="8209b-344">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Human**</span></span>

<span data-ttu-id="8209b-345">Récupérez l’objet qui contrôle l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-345">Retrieve the object that controls the simulated human.</span></span>

<span data-ttu-id="8209b-346">**Microsoft. PerceptionSimulation. IPerceptionSimulationManager. Reset**</span><span class="sxs-lookup"><span data-stu-id="8209b-346">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Reset**</span></span>

<span data-ttu-id="8209b-347">Rétablit l’État par défaut de la simulation.</span><span class="sxs-lookup"><span data-stu-id="8209b-347">Resets the simulation to its default state.</span></span>

### <a name="microsoftperceptionsimulationisimulateddevice"></a><span data-ttu-id="8209b-348">Microsoft. PerceptionSimulation. ISimulatedDevice</span><span class="sxs-lookup"><span data-stu-id="8209b-348">Microsoft.PerceptionSimulation.ISimulatedDevice</span></span>

<span data-ttu-id="8209b-349">Interface décrivant l’appareil qui interprète le monde simulé et l’homme simulé</span><span class="sxs-lookup"><span data-stu-id="8209b-349">Interface describing the device which interprets the simulated world and the simulated human</span></span>

```
public interface ISimulatedDevice
{
    ISimulatedHeadTracker HeadTracker { get; }
    ISimulatedHandTracker HandTracker { get; }
    void SetSimulatedDeviceType(SimulatedDeviceType type);
}
```

<span data-ttu-id="8209b-350">**Microsoft. PerceptionSimulation. ISimulatedDevice. HeadTracker**</span><span class="sxs-lookup"><span data-stu-id="8209b-350">**Microsoft.PerceptionSimulation.ISimulatedDevice.HeadTracker**</span></span>

<span data-ttu-id="8209b-351">Récupérez le dispositif de suivi des têtes à partir de l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-351">Retrieve the Head Tracker from the Simulated Device.</span></span>

<span data-ttu-id="8209b-352">**Microsoft. PerceptionSimulation. ISimulatedDevice. HandTracker**</span><span class="sxs-lookup"><span data-stu-id="8209b-352">**Microsoft.PerceptionSimulation.ISimulatedDevice.HandTracker**</span></span>

<span data-ttu-id="8209b-353">Récupérez le dispositif de suivi de main à partir de l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-353">Retrieve the Hand Tracker from the Simulated Device.</span></span>

<span data-ttu-id="8209b-354">**Microsoft. PerceptionSimulation. ISimulatedDevice. SetSimulatedDeviceType (Microsoft. PerceptionSimulation. SimulatedDeviceType)**</span><span class="sxs-lookup"><span data-stu-id="8209b-354">**Microsoft.PerceptionSimulation.ISimulatedDevice.SetSimulatedDeviceType(Microsoft.PerceptionSimulation.SimulatedDeviceType)**</span></span>

<span data-ttu-id="8209b-355">Définissez les propriétés de l’appareil simulé pour qu’elles correspondent au type d’appareil fourni.</span><span class="sxs-lookup"><span data-stu-id="8209b-355">Set the properties of the simulated device to match the provided device type.</span></span>

<span data-ttu-id="8209b-356">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-356">Parameters</span></span>
* <span data-ttu-id="8209b-357">type-le nouveau type d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="8209b-357">type - The new type of Simulated Device</span></span>

### <a name="microsoftperceptionsimulationisimulateddevice2"></a><span data-ttu-id="8209b-358">Microsoft. PerceptionSimulation. ISimulatedDevice2</span><span class="sxs-lookup"><span data-stu-id="8209b-358">Microsoft.PerceptionSimulation.ISimulatedDevice2</span></span>

<span data-ttu-id="8209b-359">Des propriétés supplémentaires sont disponibles en convertissant le ISimulatedDevice en ISimulatedDevice2</span><span class="sxs-lookup"><span data-stu-id="8209b-359">Additional properties are available by casting the ISimulatedDevice to ISimulatedDevice2</span></span>

```
public interface ISimulatedDevice2
{
    bool IsUserPresent { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    SimulatedDisplayConfiguration DisplayConfiguration { get; set; }

};
```

<span data-ttu-id="8209b-360">**Microsoft. PerceptionSimulation. ISimulatedDevice2. IsUserPresent**</span><span class="sxs-lookup"><span data-stu-id="8209b-360">**Microsoft.PerceptionSimulation.ISimulatedDevice2.IsUserPresent**</span></span>

<span data-ttu-id="8209b-361">Récupérer ou définir si l’homme simulé porte activement le casque.</span><span class="sxs-lookup"><span data-stu-id="8209b-361">Retrieve or set whether or not the simulated human is actively wearing the headset.</span></span>

<span data-ttu-id="8209b-362">**Microsoft. PerceptionSimulation. ISimulatedDevice2. DisplayConfiguration**</span><span class="sxs-lookup"><span data-stu-id="8209b-362">**Microsoft.PerceptionSimulation.ISimulatedDevice2.DisplayConfiguration**</span></span>

<span data-ttu-id="8209b-363">Récupérer ou définir les propriétés de l’affichage simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-363">Retrieve or set the properties of the simulated display.</span></span>

### <a name="microsoftperceptionsimulationisimulatedheadtracker"></a><span data-ttu-id="8209b-364">Microsoft. PerceptionSimulation. ISimulatedHeadTracker</span><span class="sxs-lookup"><span data-stu-id="8209b-364">Microsoft.PerceptionSimulation.ISimulatedHeadTracker</span></span>

<span data-ttu-id="8209b-365">Interface décrivant la partie de l’appareil simulé qui effectue le suivi du chef de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-365">Interface describing the portion of the simulated device that tracks the head of the simulated human.</span></span>

```
public interface ISimulatedHeadTracker
{
    HeadTrackerMode HeadTrackerMode { get; set; }
};
```

<span data-ttu-id="8209b-366">**Microsoft. PerceptionSimulation. ISimulatedHeadTracker. HeadTrackerMode**</span><span class="sxs-lookup"><span data-stu-id="8209b-366">**Microsoft.PerceptionSimulation.ISimulatedHeadTracker.HeadTrackerMode**</span></span>

<span data-ttu-id="8209b-367">Récupère et définit le mode de suivi d’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="8209b-367">Retrieves and sets the current head tracker mode.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhandtracker"></a><span data-ttu-id="8209b-368">Microsoft. PerceptionSimulation. ISimulatedHandTracker</span><span class="sxs-lookup"><span data-stu-id="8209b-368">Microsoft.PerceptionSimulation.ISimulatedHandTracker</span></span>

<span data-ttu-id="8209b-369">Interface décrivant la partie de l’appareil simulé qui effectue le suivi des mains de l’homme simulé</span><span class="sxs-lookup"><span data-stu-id="8209b-369">Interface describing the portion of the simulated device that tracks the hands of the simulated human</span></span>

```
public interface ISimulatedHandTracker
{
    Vector3 WorldPosition { get; }
    Vector3 Position { get; set; }
    float Pitch { get; set; }
    bool FrustumIgnored { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    Frustum Frustum { get; set; }
}
```

<span data-ttu-id="8209b-370">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="8209b-370">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.WorldPosition**</span></span>

<span data-ttu-id="8209b-371">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-371">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="8209b-372">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. position**</span><span class="sxs-lookup"><span data-stu-id="8209b-372">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Position**</span></span>

<span data-ttu-id="8209b-373">Récupère et définit la position du suivi de la main simulé, par rapport au centre de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="8209b-373">Retrieve and set the position of the simulated hand tracker, relative to the center of the head.</span></span>

<span data-ttu-id="8209b-374">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. brai**</span><span class="sxs-lookup"><span data-stu-id="8209b-374">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Pitch**</span></span>

<span data-ttu-id="8209b-375">Récupérer et définir le pas à pas bas du suivi simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-375">Retrieve and set the downward pitch of the simulated hand tracker.</span></span>

<span data-ttu-id="8209b-376">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. FrustumIgnored**</span><span class="sxs-lookup"><span data-stu-id="8209b-376">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.FrustumIgnored**</span></span>

<span data-ttu-id="8209b-377">Récupérez et définissez si le frustum du suivi de la main simulé est ignoré.</span><span class="sxs-lookup"><span data-stu-id="8209b-377">Retrieve and set whether the frustum of the simulated hand tracker is ignored.</span></span> <span data-ttu-id="8209b-378">Lorsqu’ils sont ignorés, les deux mains sont toujours visibles.</span><span class="sxs-lookup"><span data-stu-id="8209b-378">When ignored, both hands are always visible.</span></span> <span data-ttu-id="8209b-379">Lorsqu’elles ne sont pas ignorées (par défaut), elles ne sont visibles que lorsqu’elles se trouvent dans le frustum du dispositif de suivi de la main.</span><span class="sxs-lookup"><span data-stu-id="8209b-379">When not ignored (the default) hands are only visible when they are within the frustum of the hand tracker.</span></span>

<span data-ttu-id="8209b-380">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. frustum**</span><span class="sxs-lookup"><span data-stu-id="8209b-380">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Frustum**</span></span>

<span data-ttu-id="8209b-381">Récupérez et définissez les propriétés frustum utilisées pour déterminer si les mains sont visibles pour le suivi de la main simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-381">Retrieve and set the frustum properties used to determine if hands are visible to the simulated hand tracker.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhuman"></a><span data-ttu-id="8209b-382">Microsoft. PerceptionSimulation. ISimulatedHuman</span><span class="sxs-lookup"><span data-stu-id="8209b-382">Microsoft.PerceptionSimulation.ISimulatedHuman</span></span>

<span data-ttu-id="8209b-383">Interface de niveau supérieur pour le contrôle de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-383">Top level interface for controlling the simulated human.</span></span>

```
public interface ISimulatedHuman 
{
    Vector3 WorldPosition { get; set; }
    float Direction { get; set; }
    float Height { get; set; }
    ISimulatedHand LeftHand { get; }
    ISimulatedHand RightHand { get; }
    ISimulatedHead Head { get; }
    void Move(Vector3 translation);
    void Rotate(float radians);
}
```

<span data-ttu-id="8209b-384">**Microsoft. PerceptionSimulation. ISimulatedHuman. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="8209b-384">**Microsoft.PerceptionSimulation.ISimulatedHuman.WorldPosition**</span></span>

<span data-ttu-id="8209b-385">Récupérer et définir la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-385">Retrieve and set the position of the node with relation to the world, in meters.</span></span> <span data-ttu-id="8209b-386">La position correspond à un point au centre des pieds de l’homme.</span><span class="sxs-lookup"><span data-stu-id="8209b-386">The position corresponds to a point at the center of the human's feet.</span></span>

<span data-ttu-id="8209b-387">**Microsoft. PerceptionSimulation. ISimulatedHuman. direction**</span><span class="sxs-lookup"><span data-stu-id="8209b-387">**Microsoft.PerceptionSimulation.ISimulatedHuman.Direction**</span></span>

<span data-ttu-id="8209b-388">Récupérez et définissez le sens des visages humains simulés dans le monde.</span><span class="sxs-lookup"><span data-stu-id="8209b-388">Retrieve and set the direction the simulated human faces in the world.</span></span> <span data-ttu-id="8209b-389">0 radians est confronté à l’axe Z négatif.</span><span class="sxs-lookup"><span data-stu-id="8209b-389">0 radians faces down the negative Z axis.</span></span> <span data-ttu-id="8209b-390">Les radians positifs pivotent dans le sens des aiguilles d’une montre autour de l’axe Y.</span><span class="sxs-lookup"><span data-stu-id="8209b-390">Positive radians rotate clockwise about the Y axis.</span></span>

<span data-ttu-id="8209b-391">**Microsoft. PerceptionSimulation. ISimulatedHuman. Height**</span><span class="sxs-lookup"><span data-stu-id="8209b-391">**Microsoft.PerceptionSimulation.ISimulatedHuman.Height**</span></span>

<span data-ttu-id="8209b-392">Récupérez et définissez la hauteur de l’homme simulé, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-392">Retrieve and set the height of the simulated human, in meters.</span></span>

<span data-ttu-id="8209b-393">**Microsoft. PerceptionSimulation. ISimulatedHuman. LeftHand**</span><span class="sxs-lookup"><span data-stu-id="8209b-393">**Microsoft.PerceptionSimulation.ISimulatedHuman.LeftHand**</span></span>

<span data-ttu-id="8209b-394">Récupérez la main gauche de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-394">Retrieve the left hand of the simulated human.</span></span>

<span data-ttu-id="8209b-395">**Microsoft. PerceptionSimulation. ISimulatedHuman. à droite**</span><span class="sxs-lookup"><span data-stu-id="8209b-395">**Microsoft.PerceptionSimulation.ISimulatedHuman.RightHand**</span></span>

<span data-ttu-id="8209b-396">Récupérez la main droite de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-396">Retrieve the right hand of the simulated human.</span></span>

<span data-ttu-id="8209b-397">**Microsoft. PerceptionSimulation. ISimulatedHuman. Head**</span><span class="sxs-lookup"><span data-stu-id="8209b-397">**Microsoft.PerceptionSimulation.ISimulatedHuman.Head**</span></span>

<span data-ttu-id="8209b-398">Récupérez l’en-tête de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-398">Retrieve the head of the simulated human.</span></span>

<span data-ttu-id="8209b-399">**Microsoft. PerceptionSimulation. ISimulatedHuman. Move (Microsoft. PerceptionSimulation. Vector3)**</span><span class="sxs-lookup"><span data-stu-id="8209b-399">**Microsoft.PerceptionSimulation.ISimulatedHuman.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="8209b-400">Déplacer le humain simulé par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-400">Move the simulated human relative to its current position, in meters.</span></span>

<span data-ttu-id="8209b-401">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-401">Parameters</span></span>
* <span data-ttu-id="8209b-402">translation : translation à déplacer, par rapport à la position actuelle.</span><span class="sxs-lookup"><span data-stu-id="8209b-402">translation - The translation to move, relative to current position.</span></span>

<span data-ttu-id="8209b-403">**Microsoft. PerceptionSimulation. ISimulatedHuman. Rotate (System. Single)**</span><span class="sxs-lookup"><span data-stu-id="8209b-403">**Microsoft.PerceptionSimulation.ISimulatedHuman.Rotate(System.Single)**</span></span>

<span data-ttu-id="8209b-404">Faire pivoter l’homme simulé par rapport à sa direction actuelle, dans le sens des aiguilles d’une montre autour de l’axe Y</span><span class="sxs-lookup"><span data-stu-id="8209b-404">Rotate the simulated human relative to its current direction, clockwise about the Y axis</span></span>

<span data-ttu-id="8209b-405">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-405">Parameters</span></span>
* <span data-ttu-id="8209b-406">radians-la valeur de rotation autour de l’axe Y.</span><span class="sxs-lookup"><span data-stu-id="8209b-406">radians - The amount to rotate around the Y axis.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhuman2"></a><span data-ttu-id="8209b-407">Microsoft. PerceptionSimulation. ISimulatedHuman2</span><span class="sxs-lookup"><span data-stu-id="8209b-407">Microsoft.PerceptionSimulation.ISimulatedHuman2</span></span>

<span data-ttu-id="8209b-408">Des propriétés supplémentaires sont disponibles en convertissant le ISimulatedHuman en ISimulatedHuman2</span><span class="sxs-lookup"><span data-stu-id="8209b-408">Additional properties are available by casting the ISimulatedHuman to ISimulatedHuman2</span></span>

```
public interface ISimulatedHuman2
{
    /* New members in addition to those available on ISimulatedHuman */
    ISimulatedSixDofController LeftController { get; }
    ISimulatedSixDofController RightController { get; }
}
```

<span data-ttu-id="8209b-409">**Microsoft. PerceptionSimulation. ISimulatedHuman2. LeftController**</span><span class="sxs-lookup"><span data-stu-id="8209b-409">**Microsoft.PerceptionSimulation.ISimulatedHuman2.LeftController**</span></span>

<span data-ttu-id="8209b-410">Récupérez le contrôleur 6-DDL de gauche.</span><span class="sxs-lookup"><span data-stu-id="8209b-410">Retrieve the left 6-DOF controller.</span></span>

<span data-ttu-id="8209b-411">**Microsoft. PerceptionSimulation. ISimulatedHuman2. RightController**</span><span class="sxs-lookup"><span data-stu-id="8209b-411">**Microsoft.PerceptionSimulation.ISimulatedHuman2.RightController**</span></span>

<span data-ttu-id="8209b-412">Récupérez le contrôleur 6-DDL approprié.</span><span class="sxs-lookup"><span data-stu-id="8209b-412">Retrieve the right 6-DOF controller.</span></span>


### <a name="microsoftperceptionsimulationisimulatedhand"></a><span data-ttu-id="8209b-413">Microsoft. PerceptionSimulation. ISimulatedHand</span><span class="sxs-lookup"><span data-stu-id="8209b-413">Microsoft.PerceptionSimulation.ISimulatedHand</span></span>

<span data-ttu-id="8209b-414">Interface décrivant une main de l’homme simulé</span><span class="sxs-lookup"><span data-stu-id="8209b-414">Interface describing a hand of the simulated human</span></span>

```
public interface ISimulatedHand
{
    Vector3 WorldPosition { get; }
    Vector3 Position { get; set; }
    bool Activated { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    bool Visible { [return: MarshalAs(UnmanagedType.Bool)] get; }
    void EnsureVisible();
    void Move(Vector3 translation);
    void PerformGesture(SimulatedGesture gesture);
}
```

<span data-ttu-id="8209b-415">**Microsoft. PerceptionSimulation. ISimulatedHand. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="8209b-415">**Microsoft.PerceptionSimulation.ISimulatedHand.WorldPosition**</span></span>

<span data-ttu-id="8209b-416">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-416">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="8209b-417">**Microsoft. PerceptionSimulation. ISimulatedHand. position**</span><span class="sxs-lookup"><span data-stu-id="8209b-417">**Microsoft.PerceptionSimulation.ISimulatedHand.Position**</span></span>

<span data-ttu-id="8209b-418">Récupérer et définir la position de la main simulée par rapport à l’homme, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-418">Retrieve and set the position of the simulated hand relative to the human, in meters.</span></span>

<span data-ttu-id="8209b-419">**Microsoft. PerceptionSimulation. ISimulatedHand. Activated**</span><span class="sxs-lookup"><span data-stu-id="8209b-419">**Microsoft.PerceptionSimulation.ISimulatedHand.Activated**</span></span>

<span data-ttu-id="8209b-420">Récupère et définit si la main est actuellement activée.</span><span class="sxs-lookup"><span data-stu-id="8209b-420">Retrieve and set whether the hand is currently activated.</span></span>

<span data-ttu-id="8209b-421">**Microsoft. PerceptionSimulation. ISimulatedHand. visible**</span><span class="sxs-lookup"><span data-stu-id="8209b-421">**Microsoft.PerceptionSimulation.ISimulatedHand.Visible**</span></span>

<span data-ttu-id="8209b-422">Récupère si la main est actuellement visible pour le SimulatedDevice (IE, si elle se trouve dans une position à détecter par le HandTracker).</span><span class="sxs-lookup"><span data-stu-id="8209b-422">Retrieve whether the hand is currently visible to the SimulatedDevice (ie, whether it's in a position to be detected by the HandTracker).</span></span>

<span data-ttu-id="8209b-423">**Microsoft. PerceptionSimulation. ISimulatedHand. EnsureVisible**</span><span class="sxs-lookup"><span data-stu-id="8209b-423">**Microsoft.PerceptionSimulation.ISimulatedHand.EnsureVisible**</span></span>

<span data-ttu-id="8209b-424">Déplacez la main de manière à ce qu’elle soit visible par le SimulatedDevice.</span><span class="sxs-lookup"><span data-stu-id="8209b-424">Move the hand such that it is visible to the SimulatedDevice.</span></span>

<span data-ttu-id="8209b-425">**Microsoft. PerceptionSimulation. ISimulatedHand. Move (Microsoft. PerceptionSimulation. Vector3)**</span><span class="sxs-lookup"><span data-stu-id="8209b-425">**Microsoft.PerceptionSimulation.ISimulatedHand.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="8209b-426">Déplacer la position de la main simulée par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-426">Move the position of the simulated hand relative to its current position, in meters.</span></span>

<span data-ttu-id="8209b-427">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-427">Parameters</span></span>
* <span data-ttu-id="8209b-428">translation-le montant pour traduire la main simulée.</span><span class="sxs-lookup"><span data-stu-id="8209b-428">translation - The amount to translate the simulated hand.</span></span>

<span data-ttu-id="8209b-429">**Microsoft. PerceptionSimulation. ISimulatedHand. PerformGesture (Microsoft. PerceptionSimulation. SimulatedGesture)**</span><span class="sxs-lookup"><span data-stu-id="8209b-429">**Microsoft.PerceptionSimulation.ISimulatedHand.PerformGesture(Microsoft.PerceptionSimulation.SimulatedGesture)**</span></span>

<span data-ttu-id="8209b-430">Effectuez un mouvement à l’aide de la main simulée.</span><span class="sxs-lookup"><span data-stu-id="8209b-430">Perform a gesture using the simulated hand.</span></span>  <span data-ttu-id="8209b-431">Elle sera détectée uniquement par le système si la main est activée.</span><span class="sxs-lookup"><span data-stu-id="8209b-431">It will only be detected by the system if the hand is enabled.</span></span>

<span data-ttu-id="8209b-432">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-432">Parameters</span></span>
* <span data-ttu-id="8209b-433">geste : mouvement à effectuer.</span><span class="sxs-lookup"><span data-stu-id="8209b-433">gesture - The gesture to perform.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhand2"></a><span data-ttu-id="8209b-434">Microsoft. PerceptionSimulation. ISimulatedHand2</span><span class="sxs-lookup"><span data-stu-id="8209b-434">Microsoft.PerceptionSimulation.ISimulatedHand2</span></span>

<span data-ttu-id="8209b-435">Des propriétés supplémentaires sont disponibles en convertissant un ISimulatedHand en ISimulatedHand2.</span><span class="sxs-lookup"><span data-stu-id="8209b-435">Additional properties are available by casting an ISimulatedHand to ISimulatedHand2.</span></span>
```
public interface ISimulatedHand2
{
    /* New members in addition to those available on ISimulatedHand */
    Rotation3 Orientation { get; set; }
}
```

<span data-ttu-id="8209b-436">**Microsoft. PerceptionSimulation. ISimulatedHand2. orientation**</span><span class="sxs-lookup"><span data-stu-id="8209b-436">**Microsoft.PerceptionSimulation.ISimulatedHand2.Orientation**</span></span>

<span data-ttu-id="8209b-437">Récupère ou définit la rotation de la main simulée.</span><span class="sxs-lookup"><span data-stu-id="8209b-437">Retrieve or set the rotation of the simulated hand.</span></span>  <span data-ttu-id="8209b-438">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="8209b-438">Positive radians rotate clockwise when looking along the axis.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhand3"></a><span data-ttu-id="8209b-439">Microsoft. PerceptionSimulation. ISimulatedHand3</span><span class="sxs-lookup"><span data-stu-id="8209b-439">Microsoft.PerceptionSimulation.ISimulatedHand3</span></span>

<span data-ttu-id="8209b-440">Des propriétés supplémentaires sont disponibles en convertissant un ISimulatedHand en ISimulatedHand3</span><span class="sxs-lookup"><span data-stu-id="8209b-440">Additional properties are available by casting an ISimulatedHand to ISimulatedHand3</span></span>
```
public interface ISimulatedHand3
{
    /* New members in addition to those available on ISimulatedHand and ISimulatedHand2 */
    GetJointConfiguration(SimulatedHandJoint joint, out SimulatedHandJointConfiguration jointConfiguration);
    SetJointConfiguration(SimulatedHandJoint joint, SimulatedHandJointConfiguration jointConfiguration);
    SetHandPose(SimulatedHandPose pose, bool animate);
}
```

<span data-ttu-id="8209b-441">**Microsoft. PerceptionSimulation. ISimulatedHand3. GetJointConfiguration**</span><span class="sxs-lookup"><span data-stu-id="8209b-441">**Microsoft.PerceptionSimulation.ISimulatedHand3.GetJointConfiguration**</span></span>

<span data-ttu-id="8209b-442">Obtient la configuration conjointe pour l’articulation spécifiée.</span><span class="sxs-lookup"><span data-stu-id="8209b-442">Get the joint configuration for the specified joint.</span></span>

<span data-ttu-id="8209b-443">**Microsoft. PerceptionSimulation. ISimulatedHand3. SetJointConfiguration**</span><span class="sxs-lookup"><span data-stu-id="8209b-443">**Microsoft.PerceptionSimulation.ISimulatedHand3.SetJointConfiguration**</span></span>

<span data-ttu-id="8209b-444">Définit la configuration conjointe pour l’articulation spécifiée.</span><span class="sxs-lookup"><span data-stu-id="8209b-444">Set the joint configuration for the specified joint.</span></span>

<span data-ttu-id="8209b-445">**Microsoft. PerceptionSimulation. ISimulatedHand3. SetHandPose**</span><span class="sxs-lookup"><span data-stu-id="8209b-445">**Microsoft.PerceptionSimulation.ISimulatedHand3.SetHandPose**</span></span>

<span data-ttu-id="8209b-446">Définissez la main sur une pose connue avec un indicateur facultatif à animer.</span><span class="sxs-lookup"><span data-stu-id="8209b-446">Set the hand to a known pose with an optional flag to animate.</span></span>  <span data-ttu-id="8209b-447">Remarque : l’animation ne permettra pas aux jointures de refléter immédiatement leurs configurations conjointes finales.</span><span class="sxs-lookup"><span data-stu-id="8209b-447">Note: animating won't result in joints immediately reflecting their final joint configurations.</span></span>


### <a name="microsoftperceptionsimulationisimulatedhead"></a><span data-ttu-id="8209b-448">Microsoft. PerceptionSimulation. ISimulatedHead</span><span class="sxs-lookup"><span data-stu-id="8209b-448">Microsoft.PerceptionSimulation.ISimulatedHead</span></span>

<span data-ttu-id="8209b-449">Interface décrivant l’en-tête de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-449">Interface describing the head of the simulated human.</span></span>

```
public interface ISimulatedHead
{
    Vector3 WorldPosition { get; }
    Rotation3 Rotation { get; set; }
    float Diameter { get; set; }
    void Rotate(Rotation3 rotation);
}
```

<span data-ttu-id="8209b-450">**Microsoft. PerceptionSimulation. ISimulatedHead. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="8209b-450">**Microsoft.PerceptionSimulation.ISimulatedHead.WorldPosition**</span></span>

<span data-ttu-id="8209b-451">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-451">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="8209b-452">**Microsoft. PerceptionSimulation. ISimulatedHead. rotation**</span><span class="sxs-lookup"><span data-stu-id="8209b-452">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotation**</span></span>

<span data-ttu-id="8209b-453">Récupère la rotation de la tête simulée.</span><span class="sxs-lookup"><span data-stu-id="8209b-453">Retrieve the rotation of the simulated head.</span></span> <span data-ttu-id="8209b-454">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="8209b-454">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="8209b-455">**Microsoft. PerceptionSimulation. ISimulatedHead. diametre**</span><span class="sxs-lookup"><span data-stu-id="8209b-455">**Microsoft.PerceptionSimulation.ISimulatedHead.Diameter**</span></span>

<span data-ttu-id="8209b-456">Récupérer le diamètre de la tête simulée.</span><span class="sxs-lookup"><span data-stu-id="8209b-456">Retrieve the simulated head's diameter.</span></span> <span data-ttu-id="8209b-457">Cette valeur est utilisée pour déterminer le centre de l’en-tête (point de rotation).</span><span class="sxs-lookup"><span data-stu-id="8209b-457">This value is used to determine the head's center (point of rotation).</span></span>

<span data-ttu-id="8209b-458">**Microsoft. PerceptionSimulation. ISimulatedHead. Rotate (Microsoft. PerceptionSimulation. Rotation3)**</span><span class="sxs-lookup"><span data-stu-id="8209b-458">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span></span>

<span data-ttu-id="8209b-459">Faire pivoter la tête simulée par rapport à sa rotation actuelle.</span><span class="sxs-lookup"><span data-stu-id="8209b-459">Rotate the simulated head relative to its current rotation.</span></span> <span data-ttu-id="8209b-460">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="8209b-460">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="8209b-461">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-461">Parameters</span></span>
* <span data-ttu-id="8209b-462">rotation : quantité à faire pivoter.</span><span class="sxs-lookup"><span data-stu-id="8209b-462">rotation - The amount to rotate.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhead2"></a><span data-ttu-id="8209b-463">Microsoft. PerceptionSimulation. ISimulatedHead2</span><span class="sxs-lookup"><span data-stu-id="8209b-463">Microsoft.PerceptionSimulation.ISimulatedHead2</span></span>

<span data-ttu-id="8209b-464">Des propriétés supplémentaires sont disponibles en convertissant un ISimulatedHead en ISimulatedHead2</span><span class="sxs-lookup"><span data-stu-id="8209b-464">Additional properties are available by casting an ISimulatedHead to ISimulatedHead2</span></span>

```
public interface ISimulatedHead2
{
    /* New members in addition to those available on ISimulatedHead */
    ISimulatedEyes Eyes { get; }
}
```

<span data-ttu-id="8209b-465">**Microsoft. PerceptionSimulation. ISimulatedHead2. Eyes**</span><span class="sxs-lookup"><span data-stu-id="8209b-465">**Microsoft.PerceptionSimulation.ISimulatedHead2.Eyes**</span></span>

<span data-ttu-id="8209b-466">Récupérez les yeux de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-466">Retrieve the eyes of the simulated human.</span></span>

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller"></a><span data-ttu-id="8209b-467">Microsoft. PerceptionSimulation. ISimulatedSixDofController</span><span class="sxs-lookup"><span data-stu-id="8209b-467">Microsoft.PerceptionSimulation.ISimulatedSixDofController</span></span>

<span data-ttu-id="8209b-468">Interface décrivant un contrôleur 6-DDL associé à l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-468">Interface describing a 6-DOF controller associated with the simulated human.</span></span>

```
public interface ISimulatedSixDofController
{
    Vector3 WorldPosition { get; }
    SimulatedSixDofControllerStatus Status { get; set; }
    Vector3 Position { get; }
    Rotation3 Orientation { get; set; }
    void Move(Vector3 translation);
    void PressButton(SimulatedSixDofControllerButton button);
    void ReleaseButton(SimulatedSixDofControllerButton button);
    void GetTouchpadPosition(out float x, out float y);
    void SetTouchpadPosition(float x, float y);
}
```

<span data-ttu-id="8209b-469">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="8209b-469">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.WorldPosition**</span></span>

<span data-ttu-id="8209b-470">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-470">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="8209b-471">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. Status**</span><span class="sxs-lookup"><span data-stu-id="8209b-471">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Status**</span></span>

<span data-ttu-id="8209b-472">Récupère ou définit l’état actuel du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="8209b-472">Retrieve or set the current state of the controller.</span></span>  <span data-ttu-id="8209b-473">L’état du contrôleur doit être défini sur une valeur autre que OFF avant que les appels au déplacement, à la rotation ou à l’appui sur les boutons échouent.</span><span class="sxs-lookup"><span data-stu-id="8209b-473">The controller status must be set to a value other than Off before any calls to move, rotate or press buttons will succeed.</span></span>

<span data-ttu-id="8209b-474">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. position**</span><span class="sxs-lookup"><span data-stu-id="8209b-474">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Position**</span></span>

<span data-ttu-id="8209b-475">Récupérez ou définissez la position du contrôleur simulé par rapport à l’homme, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-475">Retrieve or set the position of the simulated controller relative to the human, in meters.</span></span>

<span data-ttu-id="8209b-476">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. orientation**</span><span class="sxs-lookup"><span data-stu-id="8209b-476">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Orientation**</span></span>

<span data-ttu-id="8209b-477">Récupérer ou définir l’orientation du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-477">Retrieve or set the orientation of the simulated controller.</span></span>

<span data-ttu-id="8209b-478">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. Move (Microsoft. PerceptionSimulation. Vector3)**</span><span class="sxs-lookup"><span data-stu-id="8209b-478">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="8209b-479">Déplacer la position du contrôleur simulé par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-479">Move the position of the simulated controller relative to its current position, in meters.</span></span>

<span data-ttu-id="8209b-480">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-480">Parameters</span></span>
* <span data-ttu-id="8209b-481">Traduction : quantité de conversion du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-481">translation - The amount to translate the simulated controller.</span></span>

<span data-ttu-id="8209b-482">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. PressButton (SimulatedSixDofControllerButton)**</span><span class="sxs-lookup"><span data-stu-id="8209b-482">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.PressButton(SimulatedSixDofControllerButton)**</span></span>

<span data-ttu-id="8209b-483">Appuyez sur un bouton sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-483">Press a button on the simulated controller.</span></span>  <span data-ttu-id="8209b-484">Il ne sera détecté par le système que si le contrôleur est activé.</span><span class="sxs-lookup"><span data-stu-id="8209b-484">It will only be detected by the system if the controller is enabled.</span></span>

<span data-ttu-id="8209b-485">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-485">Parameters</span></span>
* <span data-ttu-id="8209b-486">Button-bouton sur lequel appuyer.</span><span class="sxs-lookup"><span data-stu-id="8209b-486">button - The button to press.</span></span>

<span data-ttu-id="8209b-487">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. ReleaseButton (SimulatedSixDofControllerButton)**</span><span class="sxs-lookup"><span data-stu-id="8209b-487">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.ReleaseButton(SimulatedSixDofControllerButton)**</span></span>

<span data-ttu-id="8209b-488">Publiez un bouton sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-488">Release a button on the simulated controller.</span></span>  <span data-ttu-id="8209b-489">Il ne sera détecté par le système que si le contrôleur est activé.</span><span class="sxs-lookup"><span data-stu-id="8209b-489">It will only be detected by the system if the controller is enabled.</span></span>

<span data-ttu-id="8209b-490">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-490">Parameters</span></span>
* <span data-ttu-id="8209b-491">Button-bouton à libérer.</span><span class="sxs-lookup"><span data-stu-id="8209b-491">button - The button to release.</span></span>

<span data-ttu-id="8209b-492">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. GetTouchpadPosition (sortie float, out float)**</span><span class="sxs-lookup"><span data-stu-id="8209b-492">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.GetTouchpadPosition(out float, out float)**</span></span>

<span data-ttu-id="8209b-493">Obtient la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-493">Get the position of a simulated finger on the simulated controller's touchpad.</span></span>

<span data-ttu-id="8209b-494">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-494">Parameters</span></span>
* <span data-ttu-id="8209b-495">x-la position horizontale du doigt.</span><span class="sxs-lookup"><span data-stu-id="8209b-495">x - The horizontal position of the finger.</span></span>
* <span data-ttu-id="8209b-496">y : position verticale du doigt.</span><span class="sxs-lookup"><span data-stu-id="8209b-496">y - The vertical position of the finger.</span></span>

<span data-ttu-id="8209b-497">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. SetTouchpadPosition (float, float)**</span><span class="sxs-lookup"><span data-stu-id="8209b-497">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.SetTouchpadPosition(float, float)**</span></span>

<span data-ttu-id="8209b-498">Définit la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-498">Set the position of a simulated finger on the simulated controller's touchpad.</span></span>

<span data-ttu-id="8209b-499">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-499">Parameters</span></span>
* <span data-ttu-id="8209b-500">x-la position horizontale du doigt.</span><span class="sxs-lookup"><span data-stu-id="8209b-500">x - The horizontal position of the finger.</span></span>
* <span data-ttu-id="8209b-501">y : position verticale du doigt.</span><span class="sxs-lookup"><span data-stu-id="8209b-501">y - The vertical position of the finger.</span></span>

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller2"></a><span data-ttu-id="8209b-502">Microsoft. PerceptionSimulation. ISimulatedSixDofController2</span><span class="sxs-lookup"><span data-stu-id="8209b-502">Microsoft.PerceptionSimulation.ISimulatedSixDofController2</span></span>

<span data-ttu-id="8209b-503">Des propriétés et méthodes supplémentaires sont disponibles en convertissant un ISimulatedSixDofController en ISimulatedSixDofController2</span><span class="sxs-lookup"><span data-stu-id="8209b-503">Additional properties and methods are available by casting an ISimulatedSixDofController to ISimulatedSixDofController2</span></span>

```
public interface ISimulatedSixDofController2
{
    /* New members in addition to those available on ISimulatedSixDofController */
    void GetThumbstickPosition(out float x, out float y);
    void SetThumbstickPosition(float x, float y);
    float BatteryLevel { get; set; }
}
```

<span data-ttu-id="8209b-504">**Microsoft. PerceptionSimulation. ISimulatedSixDofController2. GetThumbstickPosition (sortie float, out float)**</span><span class="sxs-lookup"><span data-stu-id="8209b-504">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.GetThumbstickPosition(out float, out float)**</span></span>

<span data-ttu-id="8209b-505">Obtient la position du stick analogique simulé sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-505">Get the position of the simulated thumbstick on the simulated controller.</span></span>

<span data-ttu-id="8209b-506">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-506">Parameters</span></span>
* <span data-ttu-id="8209b-507">x-la position horizontale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="8209b-507">x - The horizontal position of the thumbstick.</span></span>
* <span data-ttu-id="8209b-508">y : position verticale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="8209b-508">y - The vertical position of the thumbstick.</span></span>

<span data-ttu-id="8209b-509">**Microsoft. PerceptionSimulation. ISimulatedSixDofController2. SetThumbstickPosition (float, float)**</span><span class="sxs-lookup"><span data-stu-id="8209b-509">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.SetThumbstickPosition(float, float)**</span></span>

<span data-ttu-id="8209b-510">Définissez la position du stick analogique simulé sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-510">Set the position of the simulated thumbstick on the simulated controller.</span></span>

<span data-ttu-id="8209b-511">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-511">Parameters</span></span>
* <span data-ttu-id="8209b-512">x-la position horizontale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="8209b-512">x - The horizontal position of the thumbstick.</span></span>
* <span data-ttu-id="8209b-513">y : position verticale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="8209b-513">y - The vertical position of the thumbstick.</span></span>

<span data-ttu-id="8209b-514">**Microsoft. PerceptionSimulation. ISimulatedSixDofController2. BatteryLevel**</span><span class="sxs-lookup"><span data-stu-id="8209b-514">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.BatteryLevel**</span></span>

<span data-ttu-id="8209b-515">Récupérez ou définissez le niveau de batterie du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-515">Retrieve or set the battery level of the simulated controller.</span></span>  <span data-ttu-id="8209b-516">La valeur doit être supérieure à 0,0 et inférieure ou égale à 100,0.</span><span class="sxs-lookup"><span data-stu-id="8209b-516">The value must be greater than 0.0 and less than or equal to 100.0.</span></span>


### <a name="microsoftperceptionsimulationisimulatedeyes"></a><span data-ttu-id="8209b-517">Microsoft. PerceptionSimulation. ISimulatedEyes</span><span class="sxs-lookup"><span data-stu-id="8209b-517">Microsoft.PerceptionSimulation.ISimulatedEyes</span></span>

<span data-ttu-id="8209b-518">Interface décrivant les yeux de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-518">Interface describing the eyes of the simulated human.</span></span>

```
public interface ISimulatedEyes
{
    Rotation3 Rotation { get; set; }
    void Rotate(Rotation3 rotation);
    SimulatedEyesCalibrationState CalibrationState { get; set; }
    Vector3 WorldPosition { get; }
}
```

<span data-ttu-id="8209b-519">**Microsoft. PerceptionSimulation. ISimulatedEyes. rotation**</span><span class="sxs-lookup"><span data-stu-id="8209b-519">**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotation**</span></span>

<span data-ttu-id="8209b-520">Récupérer la rotation des yeux simulés.</span><span class="sxs-lookup"><span data-stu-id="8209b-520">Retrieve the rotation of the simulated eyes.</span></span> <span data-ttu-id="8209b-521">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="8209b-521">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="8209b-522">**Microsoft. PerceptionSimulation. ISimulatedEyes. Rotate (Microsoft. PerceptionSimulation. Rotation3)**</span><span class="sxs-lookup"><span data-stu-id="8209b-522">**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span></span>

<span data-ttu-id="8209b-523">Faire pivoter les yeux simulés par rapport à sa rotation actuelle.</span><span class="sxs-lookup"><span data-stu-id="8209b-523">Rotate the simulated eyes relative to its current rotation.</span></span> <span data-ttu-id="8209b-524">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="8209b-524">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="8209b-525">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-525">Parameters</span></span>
* <span data-ttu-id="8209b-526">rotation : quantité à faire pivoter.</span><span class="sxs-lookup"><span data-stu-id="8209b-526">rotation - The amount to rotate.</span></span>

<span data-ttu-id="8209b-527">**Microsoft. PerceptionSimulation. ISimulatedEyes. CalibrationState**</span><span class="sxs-lookup"><span data-stu-id="8209b-527">**Microsoft.PerceptionSimulation.ISimulatedEyes.CalibrationState**</span></span>

<span data-ttu-id="8209b-528">Récupère ou définit l’état d’étalonnage des yeux simulés.</span><span class="sxs-lookup"><span data-stu-id="8209b-528">Retrieves or sets the calibration state of the simulated eyes.</span></span>

<span data-ttu-id="8209b-529">**Microsoft. PerceptionSimulation. ISimulatedEyes. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="8209b-529">**Microsoft.PerceptionSimulation.ISimulatedEyes.WorldPosition**</span></span>

<span data-ttu-id="8209b-530">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="8209b-530">Retrieve the position of the node with relation to the world, in meters.</span></span>


### <a name="microsoftperceptionsimulationisimulationrecording"></a><span data-ttu-id="8209b-531">Microsoft. PerceptionSimulation. ISimulationRecording</span><span class="sxs-lookup"><span data-stu-id="8209b-531">Microsoft.PerceptionSimulation.ISimulationRecording</span></span>

<span data-ttu-id="8209b-532">Interface pour l’interaction avec un enregistrement unique chargé pour la lecture.</span><span class="sxs-lookup"><span data-stu-id="8209b-532">Interface for interacting with a single recording loaded for playback.</span></span>

```
public interface ISimulationRecording
{
    StreamDataTypes DataTypes { get; }
    PlaybackState State { get; }
    void Play();
    void Pause();
    void Seek(UInt64 ticks);
    void Stop();
};
```

<span data-ttu-id="8209b-533">**Microsoft. PerceptionSimulation. ISimulationRecording. DataTypes**</span><span class="sxs-lookup"><span data-stu-id="8209b-533">**Microsoft.PerceptionSimulation.ISimulationRecording.DataTypes**</span></span>

<span data-ttu-id="8209b-534">Récupère la liste des types de données dans l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="8209b-534">Retrieves the list of data types in the recording.</span></span>

<span data-ttu-id="8209b-535">**Microsoft. PerceptionSimulation. ISimulationRecording. State**</span><span class="sxs-lookup"><span data-stu-id="8209b-535">**Microsoft.PerceptionSimulation.ISimulationRecording.State**</span></span>

<span data-ttu-id="8209b-536">Récupère l’état actuel de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="8209b-536">Retrieves the current state of the recording.</span></span>

<span data-ttu-id="8209b-537">**Microsoft. PerceptionSimulation. ISimulationRecording. Play**</span><span class="sxs-lookup"><span data-stu-id="8209b-537">**Microsoft.PerceptionSimulation.ISimulationRecording.Play**</span></span>

<span data-ttu-id="8209b-538">Démarrez la lecture.</span><span class="sxs-lookup"><span data-stu-id="8209b-538">Start the playback.</span></span> <span data-ttu-id="8209b-539">Si l’enregistrement est suspendu, la lecture reprendra à partir de l’emplacement suspendu ; s’il est arrêté, la lecture démarre au début.</span><span class="sxs-lookup"><span data-stu-id="8209b-539">If the recording is paused, playback will resume from the paused location; if stopped, playback will start at the beginning.</span></span> <span data-ttu-id="8209b-540">Si elle est déjà en cours d’exécution, cet appel est ignoré.</span><span class="sxs-lookup"><span data-stu-id="8209b-540">If already playing, this call is ignored.</span></span>

<span data-ttu-id="8209b-541">**Microsoft. PerceptionSimulation. ISimulationRecording. pause**</span><span class="sxs-lookup"><span data-stu-id="8209b-541">**Microsoft.PerceptionSimulation.ISimulationRecording.Pause**</span></span>

<span data-ttu-id="8209b-542">Suspend la lecture à son emplacement actuel.</span><span class="sxs-lookup"><span data-stu-id="8209b-542">Pauses the playback at its current location.</span></span> <span data-ttu-id="8209b-543">Si l’enregistrement est arrêté, l’appel est ignoré.</span><span class="sxs-lookup"><span data-stu-id="8209b-543">If the recording is stopped, the call is ignored.</span></span>

<span data-ttu-id="8209b-544">**Microsoft. PerceptionSimulation. ISimulationRecording. Seek (System. UInt64)**</span><span class="sxs-lookup"><span data-stu-id="8209b-544">**Microsoft.PerceptionSimulation.ISimulationRecording.Seek(System.UInt64)**</span></span>

<span data-ttu-id="8209b-545">Recherche l’enregistrement à l’heure spécifiée (dans les intervalles de 100 nanosecondes à partir du début) et s’interrompt à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="8209b-545">Seeks the recording to the specified time (in 100 nanoseconds intervals from the beginning) and pauses at that location.</span></span> <span data-ttu-id="8209b-546">Si l’heure est postérieure à la fin de l’enregistrement, elle est mise en pause au niveau de la dernière image.</span><span class="sxs-lookup"><span data-stu-id="8209b-546">If the time is beyond the end of the recording, it is paused at the last frame.</span></span>

<span data-ttu-id="8209b-547">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-547">Parameters</span></span>
* <span data-ttu-id="8209b-548">cycles : heure à laquelle effectuer la recherche.</span><span class="sxs-lookup"><span data-stu-id="8209b-548">ticks - The time to which to seek.</span></span>

<span data-ttu-id="8209b-549">**Microsoft. PerceptionSimulation. ISimulationRecording. Stop**</span><span class="sxs-lookup"><span data-stu-id="8209b-549">**Microsoft.PerceptionSimulation.ISimulationRecording.Stop**</span></span>

<span data-ttu-id="8209b-550">Arrête la lecture et réinitialise la position au début.</span><span class="sxs-lookup"><span data-stu-id="8209b-550">Stops the playback and resets the position to the beginning.</span></span>

### <a name="microsoftperceptionsimulationisimulationrecordingcallback"></a><span data-ttu-id="8209b-551">Microsoft. PerceptionSimulation. ISimulationRecordingCallback</span><span class="sxs-lookup"><span data-stu-id="8209b-551">Microsoft.PerceptionSimulation.ISimulationRecordingCallback</span></span>

<span data-ttu-id="8209b-552">Interface pour la réception des modifications d’État pendant la lecture.</span><span class="sxs-lookup"><span data-stu-id="8209b-552">Interface for receiving state changes during playback.</span></span>

```
public interface ISimulationRecordingCallback
{
    void PlaybackStateChanged(PlaybackState newState);
};
```

<span data-ttu-id="8209b-553">**Microsoft. PerceptionSimulation. ISimulationRecordingCallback. PlaybackStateChanged (Microsoft. PerceptionSimulation. PlaybackState)**</span><span class="sxs-lookup"><span data-stu-id="8209b-553">**Microsoft.PerceptionSimulation.ISimulationRecordingCallback.PlaybackStateChanged(Microsoft.PerceptionSimulation.PlaybackState)**</span></span>

<span data-ttu-id="8209b-554">Appelé lorsque l’état de lecture d’un ISimulationRecording a changé.</span><span class="sxs-lookup"><span data-stu-id="8209b-554">Called when an ISimulationRecording's playback state has changed.</span></span>

<span data-ttu-id="8209b-555">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-555">Parameters</span></span>
* <span data-ttu-id="8209b-556">newState : nouvel état de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="8209b-556">newState - The new state of the recording.</span></span>

### <a name="microsoftperceptionsimulationperceptionsimulationmanager"></a><span data-ttu-id="8209b-557">Microsoft. PerceptionSimulation. PerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="8209b-557">Microsoft.PerceptionSimulation.PerceptionSimulationManager</span></span>

<span data-ttu-id="8209b-558">Objet racine pour la création d’objets de simulation de perception.</span><span class="sxs-lookup"><span data-stu-id="8209b-558">Root object for creating Perception Simulation objects.</span></span>

```
public static class PerceptionSimulationManager
{
    public static IPerceptionSimulationManager CreatePerceptionSimulationManager(ISimulationStreamSink sink);
    public static ISimulationStreamSink CreatePerceptionSimulationRecording(string path);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory, ISimulationRecordingCallback callback);
```

<span data-ttu-id="8209b-559">**Microsoft. PerceptionSimulation. PerceptionSimulationManager. CreatePerceptionSimulationManager (Microsoft. PerceptionSimulation. ISimulationStreamSink)**</span><span class="sxs-lookup"><span data-stu-id="8209b-559">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationManager(Microsoft.PerceptionSimulation.ISimulationStreamSink)**</span></span>

<span data-ttu-id="8209b-560">Créez sur un objet pour générer des paquets simulés et les fournir au récepteur fourni.</span><span class="sxs-lookup"><span data-stu-id="8209b-560">Create on object for generating simulated packets and delivering them to the provided sink.</span></span>

<span data-ttu-id="8209b-561">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-561">Parameters</span></span>
* <span data-ttu-id="8209b-562">Sink : récepteur qui recevra tous les paquets générés.</span><span class="sxs-lookup"><span data-stu-id="8209b-562">sink - The sink that will receive all generated packets.</span></span>

<span data-ttu-id="8209b-563">Valeur retournée</span><span class="sxs-lookup"><span data-stu-id="8209b-563">Return value</span></span>

<span data-ttu-id="8209b-564">Gestionnaire créé.</span><span class="sxs-lookup"><span data-stu-id="8209b-564">The created Manager.</span></span>

<span data-ttu-id="8209b-565">**Microsoft. PerceptionSimulation. PerceptionSimulationManager. CreatePerceptionSimulationRecording (System. String)**</span><span class="sxs-lookup"><span data-stu-id="8209b-565">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationRecording(System.String)**</span></span>

<span data-ttu-id="8209b-566">Créez un récepteur qui stocke tous les paquets reçus dans un fichier au chemin d’accès spécifié.</span><span class="sxs-lookup"><span data-stu-id="8209b-566">Create a sink which stores all received packets in a file at the specified path.</span></span>

<span data-ttu-id="8209b-567">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-567">Parameters</span></span>
* <span data-ttu-id="8209b-568">chemin d’accès : chemin d’accès du fichier à créer.</span><span class="sxs-lookup"><span data-stu-id="8209b-568">path - The path of the file to create.</span></span>

<span data-ttu-id="8209b-569">Valeur retournée</span><span class="sxs-lookup"><span data-stu-id="8209b-569">Return value</span></span>

<span data-ttu-id="8209b-570">Récepteur créé.</span><span class="sxs-lookup"><span data-stu-id="8209b-570">The created sink.</span></span>

<span data-ttu-id="8209b-571">**Microsoft. PerceptionSimulation. PerceptionSimulationManager. LoadPerceptionSimulationRecording (System. String, Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory)**</span><span class="sxs-lookup"><span data-stu-id="8209b-571">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory)**</span></span>

<span data-ttu-id="8209b-572">Charge un enregistrement à partir du fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="8209b-572">Load a recording from the specified file.</span></span>

<span data-ttu-id="8209b-573">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-573">Parameters</span></span>
* <span data-ttu-id="8209b-574">chemin d’accès : chemin d’accès du fichier à charger.</span><span class="sxs-lookup"><span data-stu-id="8209b-574">path - The path of the file to load.</span></span>
* <span data-ttu-id="8209b-575">Factory : fabrique utilisée par l’enregistrement pour créer un ISimulationStreamSink quand cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8209b-575">factory - A factory used by the recording for creating an ISimulationStreamSink when required.</span></span>

<span data-ttu-id="8209b-576">Valeur retournée</span><span class="sxs-lookup"><span data-stu-id="8209b-576">Return value</span></span>

<span data-ttu-id="8209b-577">Enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="8209b-577">The loaded recording.</span></span>

<span data-ttu-id="8209b-578">**Microsoft. PerceptionSimulation. PerceptionSimulationManager. LoadPerceptionSimulationRecording (System. String, Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory, Microsoft. PerceptionSimulation. ISimulationRecordingCallback)**</span><span class="sxs-lookup"><span data-stu-id="8209b-578">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory,Microsoft.PerceptionSimulation.ISimulationRecordingCallback)**</span></span>

<span data-ttu-id="8209b-579">Charge un enregistrement à partir du fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="8209b-579">Load a recording from the specified file.</span></span>

<span data-ttu-id="8209b-580">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-580">Parameters</span></span>
* <span data-ttu-id="8209b-581">chemin d’accès : chemin d’accès du fichier à charger.</span><span class="sxs-lookup"><span data-stu-id="8209b-581">path - The path of the file to load.</span></span>
* <span data-ttu-id="8209b-582">Factory : fabrique utilisée par l’enregistrement pour créer un ISimulationStreamSink quand cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8209b-582">factory - A factory used by the recording for creating an ISimulationStreamSink when required.</span></span>
* <span data-ttu-id="8209b-583">callback : rappel qui reçoit les mises à jour qui regradent l’état de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="8209b-583">callback - A callback which receives updates regrading the recording's status.</span></span>

<span data-ttu-id="8209b-584">Valeur retournée</span><span class="sxs-lookup"><span data-stu-id="8209b-584">Return value</span></span>

<span data-ttu-id="8209b-585">Enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="8209b-585">The loaded recording.</span></span>

### <a name="microsoftperceptionsimulationstreamdatatypes"></a><span data-ttu-id="8209b-586">Microsoft. PerceptionSimulation. StreamDataTypes</span><span class="sxs-lookup"><span data-stu-id="8209b-586">Microsoft.PerceptionSimulation.StreamDataTypes</span></span>

<span data-ttu-id="8209b-587">Décrit les différents types de données de flux.</span><span class="sxs-lookup"><span data-stu-id="8209b-587">Describes the different types of stream data.</span></span>

```
public enum StreamDataTypes
{
    None = 0x00,
    Head = 0x01,
    Hands = 0x02,
    SpatialMapping = 0x08,
    Calibration = 0x10,
    Environment = 0x20,
    SixDofControllers = 0x40,
    Eyes = 0x80,
    DisplayConfiguration = 0x100
    All = None | Head | Hands | SpatialMapping | Calibration | Environment | SixDofControllers | Eyes | DisplayConfiguration
}
```

<span data-ttu-id="8209b-588">**Microsoft. PerceptionSimulation. StreamDataTypes. None**</span><span class="sxs-lookup"><span data-stu-id="8209b-588">**Microsoft.PerceptionSimulation.StreamDataTypes.None**</span></span>

<span data-ttu-id="8209b-589">Valeur de sentinelle utilisée pour indiquer l’absence de type de données de flux.</span><span class="sxs-lookup"><span data-stu-id="8209b-589">A sentinel value used to indicate no stream data types.</span></span>

<span data-ttu-id="8209b-590">**Microsoft. PerceptionSimulation. StreamDataTypes. Head**</span><span class="sxs-lookup"><span data-stu-id="8209b-590">**Microsoft.PerceptionSimulation.StreamDataTypes.Head**</span></span>

<span data-ttu-id="8209b-591">Flux de données concernant la position et l’orientation de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="8209b-591">Stream of data regarding the position and orientation of the head.</span></span>

<span data-ttu-id="8209b-592">**Microsoft. PerceptionSimulation. StreamDataTypes. mains**</span><span class="sxs-lookup"><span data-stu-id="8209b-592">**Microsoft.PerceptionSimulation.StreamDataTypes.Hands**</span></span>

<span data-ttu-id="8209b-593">Flux de données concernant la position et les gestes des mains.</span><span class="sxs-lookup"><span data-stu-id="8209b-593">Stream of data regarding the position and gestures of hands.</span></span>

<span data-ttu-id="8209b-594">**Microsoft. PerceptionSimulation. StreamDataTypes. SpatialMapping**</span><span class="sxs-lookup"><span data-stu-id="8209b-594">**Microsoft.PerceptionSimulation.StreamDataTypes.SpatialMapping**</span></span>

<span data-ttu-id="8209b-595">Flux de données concernant le mappage spatial de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="8209b-595">Stream of data regarding spatial mapping of the environment.</span></span>

<span data-ttu-id="8209b-596">**Microsoft. PerceptionSimulation. StreamDataTypes. étalonnage**</span><span class="sxs-lookup"><span data-stu-id="8209b-596">**Microsoft.PerceptionSimulation.StreamDataTypes.Calibration**</span></span>

<span data-ttu-id="8209b-597">Flux de données concernant l’étalonnage de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8209b-597">Stream of data regarding calibration of the device.</span></span> <span data-ttu-id="8209b-598">Les paquets d’étalonnage sont acceptés uniquement par un système en mode distant.</span><span class="sxs-lookup"><span data-stu-id="8209b-598">Calibration packets are only accepted by a system in Remote Mode.</span></span>

<span data-ttu-id="8209b-599">**Microsoft. PerceptionSimulation. StreamDataTypes. Environment**</span><span class="sxs-lookup"><span data-stu-id="8209b-599">**Microsoft.PerceptionSimulation.StreamDataTypes.Environment**</span></span>

<span data-ttu-id="8209b-600">Flux de données concernant l’environnement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8209b-600">Stream of data regarding the environment of the device.</span></span>

<span data-ttu-id="8209b-601">**Microsoft. PerceptionSimulation. StreamDataTypes. SixDofControllers**</span><span class="sxs-lookup"><span data-stu-id="8209b-601">**Microsoft.PerceptionSimulation.StreamDataTypes.SixDofControllers**</span></span>

<span data-ttu-id="8209b-602">Flux de données concernant les contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="8209b-602">Stream of data regarding motion controllers.</span></span>

<span data-ttu-id="8209b-603">**Microsoft. PerceptionSimulation. StreamDataTypes. Eyes**</span><span class="sxs-lookup"><span data-stu-id="8209b-603">**Microsoft.PerceptionSimulation.StreamDataTypes.Eyes**</span></span>

<span data-ttu-id="8209b-604">Flux de données concernant les yeux de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="8209b-604">Stream of data regarding the eyes of the simulated human.</span></span>

<span data-ttu-id="8209b-605">**Microsoft. PerceptionSimulation. StreamDataTypes. DisplayConfiguration**</span><span class="sxs-lookup"><span data-stu-id="8209b-605">**Microsoft.PerceptionSimulation.StreamDataTypes.DisplayConfiguration**</span></span>

<span data-ttu-id="8209b-606">Flux de données concernant la configuration d’affichage de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8209b-606">Stream of data regarding the display configuration of the device.</span></span>

<span data-ttu-id="8209b-607">**Microsoft. PerceptionSimulation. StreamDataTypes. All**</span><span class="sxs-lookup"><span data-stu-id="8209b-607">**Microsoft.PerceptionSimulation.StreamDataTypes.All**</span></span>

<span data-ttu-id="8209b-608">Valeur de sentinelle utilisée pour indiquer tous les types de données enregistrés.</span><span class="sxs-lookup"><span data-stu-id="8209b-608">A sentinel value used to indicate all recorded data types.</span></span>

### <a name="microsoftperceptionsimulationisimulationstreamsink"></a><span data-ttu-id="8209b-609">Microsoft. PerceptionSimulation. ISimulationStreamSink</span><span class="sxs-lookup"><span data-stu-id="8209b-609">Microsoft.PerceptionSimulation.ISimulationStreamSink</span></span>

<span data-ttu-id="8209b-610">Objet qui reçoit les paquets de données d’un flux de simulation.</span><span class="sxs-lookup"><span data-stu-id="8209b-610">An object that receives data packets from a simulation stream.</span></span>

```
public interface ISimulationStreamSink
{
    void OnPacketReceived(uint length, byte[] packet);
}
```

<span data-ttu-id="8209b-611">**Microsoft. PerceptionSimulation. ISimulationStreamSink. OnPacketReceived (uint Length, Byte [] paquet)**</span><span class="sxs-lookup"><span data-stu-id="8209b-611">**Microsoft.PerceptionSimulation.ISimulationStreamSink.OnPacketReceived(uint length, byte[] packet)**</span></span>

<span data-ttu-id="8209b-612">Reçoit un paquet unique, qui est typé en interne et avec version.</span><span class="sxs-lookup"><span data-stu-id="8209b-612">Receives a single packet, which is internally typed and versioned.</span></span>

<span data-ttu-id="8209b-613">Paramètres</span><span class="sxs-lookup"><span data-stu-id="8209b-613">Parameters</span></span>
* <span data-ttu-id="8209b-614">Length-Longueur du paquet.</span><span class="sxs-lookup"><span data-stu-id="8209b-614">length - The length of the packet.</span></span>
* <span data-ttu-id="8209b-615">paquet : données du paquet.</span><span class="sxs-lookup"><span data-stu-id="8209b-615">packet - The data of the packet.</span></span>

### <a name="microsoftperceptionsimulationisimulationstreamsinkfactory"></a><span data-ttu-id="8209b-616">Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory</span><span class="sxs-lookup"><span data-stu-id="8209b-616">Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory</span></span>

<span data-ttu-id="8209b-617">Objet qui crée ISimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="8209b-617">An object that creates ISimulationStreamSink.</span></span>

```
public interface ISimulationStreamSinkFactory
{
    ISimulationStreamSink CreateSimulationStreamSink();
}
```

<span data-ttu-id="8209b-618">**Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory. CreateSimulationStreamSink ()**</span><span class="sxs-lookup"><span data-stu-id="8209b-618">**Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory.CreateSimulationStreamSink()**</span></span>

<span data-ttu-id="8209b-619">Crée une seule instance de ISimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="8209b-619">Creates a single instance of ISimulationStreamSink.</span></span>

<span data-ttu-id="8209b-620">Valeur retournée</span><span class="sxs-lookup"><span data-stu-id="8209b-620">Return value</span></span>

<span data-ttu-id="8209b-621">Récepteur créé.</span><span class="sxs-lookup"><span data-stu-id="8209b-621">The created sink.</span></span>
