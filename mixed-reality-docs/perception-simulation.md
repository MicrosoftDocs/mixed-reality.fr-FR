---
title: Simulation de perception
description: Un guide d’utilisation de la bibliothèque de Simulation de Perception pour automatiser l’entrée simulée pour des applications immersives
author: pbarnettms
ms.author: pbarnett
ms.date: 04/26/2019
ms.topic: article
keywords: HoloLens, simulation, test
ms.openlocfilehash: 8152181bdbe8c83d2b706b34f1f2fb5d51f4c880
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414533"
---
# <a name="perception-simulation"></a><span data-ttu-id="9d8f3-104">Simulation de perception</span><span class="sxs-lookup"><span data-stu-id="9d8f3-104">Perception simulation</span></span>

<span data-ttu-id="9d8f3-105">Vous souhaitez générer un test automatisé pour votre application ?</span><span class="sxs-lookup"><span data-stu-id="9d8f3-105">Do you want to build an automated test for your app?</span></span> <span data-ttu-id="9d8f3-106">Voulez-vous que vos tests d’aller au-delà des tests d’unités au niveau du composant et de véritablement tester votre application end-to-end ?</span><span class="sxs-lookup"><span data-stu-id="9d8f3-106">Do you want your tests to go beyond component-level unit testing and really exercise your app end-to-end?</span></span> <span data-ttu-id="9d8f3-107">Simulation de perception est ce que vous cherchez.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-107">Perception Simulation is what you're looking for.</span></span> <span data-ttu-id="9d8f3-108">La bibliothèque de Simulation de Perception envoie humaine et world les données d’entrée à votre application afin d’automatiser vos tests.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-108">The Perception Simulation library sends human and world input data to your app so you can automate your tests.</span></span> <span data-ttu-id="9d8f3-109">Par exemple, vous pouvez simuler l’entrée d’un humain cherche à une position spécifique, reproductible et puis en effectuant un mouvement ou à l’aide d’un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-109">For example, you can simulate the input of a human looking to a specific, repeatable position and then performing a gesture or using a motion controller.</span></span>

<span data-ttu-id="9d8f3-110">Simulation de perception peut envoyer simulée entrée comme ceci à un HoloLens physique, l’émulateur de HoloLens (1er gen), le HoloLens 2 émulateur ou un PC avec le portail de réalité mixte installé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-110">Perception Simulation can send simulated input like this to a physical HoloLens, the HoloLens emulator (1st gen), the HoloLens 2 Emulator, or a PC with Mixed Reality Portal installed.</span></span> <span data-ttu-id="9d8f3-111">Perception Simulation ignore les capteurs en direct sur un appareil de réalité mixte et envoie simulés entrée aux applications s’exécutant sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-111">Perception Simulation bypasses the live sensors on a Mixed Reality device and sends simulated input to applications running on the device.</span></span> <span data-ttu-id="9d8f3-112">Les applications reçoivent ces événements d’entrée via les mêmes API qu’ils utilisent toujours et que vous ne pouvez pas faire la différence entre l’exécution avec des capteurs réels et l’exécution avec Simulation de Perception.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-112">Applications receive these input events through the same APIs they always use and can't tell the difference between running with real sensors versus running with Perception Simulation.</span></span> <span data-ttu-id="9d8f3-113">Simulation de perception est la technologie utilisée par les émulateurs de HoloLens d’envoyer l’entrée simulée à la Machine virtuelle HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-113">Perception Simulation is the same technology used by the HoloLens emulators to send simulated input to the HoloLens Virtual Machine.</span></span>

<span data-ttu-id="9d8f3-114">Pour commencer à l’aide de la simulation dans votre code, commencez par créer un objet IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-114">To begin using simulation in your code, start by creating an IPerceptionSimulationManager object.</span></span> <span data-ttu-id="9d8f3-115">À partir de cet objet, vous pouvez émettre des commandes permettant de contrôler les propriétés d’un simulé « humaine », y compris la position de tête, la position de la main et mouvements, et vous pouvez activer et manipuler des contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-115">From that object, you can issue commands to control properties of a simulated "human", including head position, hand position, and gestures, and you can enable and manipulate motion controllers.</span></span>

## <a name="setting-up-a-visual-studio-project-for-perception-simulation"></a><span data-ttu-id="9d8f3-116">Configuration d’un projet Visual Studio pour la Simulation de Perception</span><span class="sxs-lookup"><span data-stu-id="9d8f3-116">Setting Up a Visual Studio Project for Perception Simulation</span></span>
1. <span data-ttu-id="9d8f3-117">[Installer l’émulateur de HoloLens](install-the-tools.md) sur votre PC de développement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-117">[Install the HoloLens emulator](install-the-tools.md) on your development PC.</span></span> <span data-ttu-id="9d8f3-118">L’émulateur inclut les bibliothèques que vous allez utiliser pour la Simulation de Perception.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-118">The emulator includes the libraries you will use for Perception Simulation.</span></span>
2. <span data-ttu-id="9d8f3-119">Créer un nouveau Visual Studio C# projet de bureau (un projet Console fonctionne très bien prise en main).</span><span class="sxs-lookup"><span data-stu-id="9d8f3-119">Create a new Visual Studio C# desktop project (a Console Project works great to get started).</span></span>
3. <span data-ttu-id="9d8f3-120">Ajouter les fichiers binaires suivants à votre projet en tant que références (projet -> Ajouter -> référence...). Vous pouvez les trouver dans % ProgramFiles% (x86) %\Microsoft XDE\\(version), tel que **% ProgramFiles (x86) %\Microsoft XDE\\10.0.18362.0** pour l’émulateur de 2 HoloLens.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-120">Add the following binaries to your project as references (Project->Add->Reference...). You can find them in %ProgramFiles(x86)%\Microsoft XDE\\(version), such as **%ProgramFiles(x86)%\Microsoft XDE\\10.0.18362.0** for the HoloLens 2 Emulator.</span></span>  <span data-ttu-id="9d8f3-121">(Remarque : bien que les fichiers binaires font partie de l’émulateur de 2 HoloLens, ils fonctionnent également pour la réalité mixte Windows sur le bureau.) une barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-121">(Note: although the binaries are part of the HoloLens 2 Emulator, they also work for Windows Mixed Reality on the desktop.) a.</span></span> <span data-ttu-id="9d8f3-122">PerceptionSimulationManager.Interop.dll - managé C# wrapper pour la Simulation de Perception.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-122">PerceptionSimulationManager.Interop.dll - Managed C# wrapper for Perception Simulation.</span></span>
    <span data-ttu-id="9d8f3-123">b.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-123">b.</span></span> <span data-ttu-id="9d8f3-124">PerceptionSimulationRest.dll - bibliothèque de configuration d’un canal de communication de socket web à l’HoloLens ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-124">PerceptionSimulationRest.dll - Library for setting up a web-socket communication channel to the HoloLens or emulator.</span></span>
    <span data-ttu-id="9d8f3-125">c.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-125">c.</span></span> <span data-ttu-id="9d8f3-126">SimulationStream.Interop.dll - types partagés pour la simulation.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-126">SimulationStream.Interop.dll - Shared types for simulation.</span></span>
4. <span data-ttu-id="9d8f3-127">Ajoutez l’implémentation PerceptionSimulationManager.dll binaire à votre projet une.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-127">Add the implementation binary PerceptionSimulationManager.dll to your project a.</span></span> <span data-ttu-id="9d8f3-128">Tout d’abord l’ajouter sous forme binaire au projet (projet -> Ajouter -> élément existant...). Enregistrez-le sous forme de lien afin qu’il ne le copie vers votre dossier source du projet.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-128">First add it as a binary to the project (Project->Add->Existing Item...). Save it as a link so that it doesn't copy it to your project source folder.</span></span> <span data-ttu-id="9d8f3-129">![Ajouter au projet sous forme de lien PerceptionSimulationManager.dll](images/saveaslink.png) b.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-129">![Add PerceptionSimulationManager.dll to the project as a link](images/saveaslink.png) b.</span></span> <span data-ttu-id="9d8f3-130">Assurez-vous qu’il le copié dans votre dossier de sortie sur la build.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-130">Then make sure that it get's copied to your output folder on build.</span></span> <span data-ttu-id="9d8f3-131">Il s’agit de la feuille de propriétés pour le fichier binaire.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-131">This is in the property sheet for the binary .</span></span> <span data-ttu-id="9d8f3-132">![Marquer PerceptionSimulationManager.dll pour copier vers le répertoire de sortie](images/copyalways.png)</span><span class="sxs-lookup"><span data-stu-id="9d8f3-132">![Mark PerceptionSimulationManager.dll to copy to the output directory](images/copyalways.png)</span></span>
5. <span data-ttu-id="9d8f3-133">Définissez votre plateforme de solution active x64.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-133">Set your active solution platform to x64.</span></span>  <span data-ttu-id="9d8f3-134">(Utilisez le Gestionnaire de Configuration pour créer une entrée de plateforme pour x64 s’il n’existe pas déjà).</span><span class="sxs-lookup"><span data-stu-id="9d8f3-134">(Use the Configuration Manager to create a Platform entry for x64 if one does not already exist.)</span></span>

## <a name="creating-an-iperceptionsimulation-manager-object"></a><span data-ttu-id="9d8f3-135">Création d’un objet de gestionnaire IPerceptionSimulation</span><span class="sxs-lookup"><span data-stu-id="9d8f3-135">Creating an IPerceptionSimulation Manager Object</span></span>

<span data-ttu-id="9d8f3-136">Pour contrôler la simulation, vous allez émettre des mises à jour pour les objets récupérés à partir d’un objet IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-136">To control simulation, you'll issue updates to objects retrieved from an IPerceptionSimulationManager object.</span></span> <span data-ttu-id="9d8f3-137">La première étape consiste à obtenir cet objet et le connecter à votre appareil cible ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-137">The first step is to get that object and connect it to your target device or emulator.</span></span> <span data-ttu-id="9d8f3-138">Vous pouvez obtenir l’adresse IP de votre émulateur en cliquant sur le bouton de portail de l’appareil dans le [barre d’outils](using-the-hololens-emulator.md)</span><span class="sxs-lookup"><span data-stu-id="9d8f3-138">You can get the IP address of your emulator by clicking on the Device Portal button in the [toolbar](using-the-hololens-emulator.md)</span></span>

<span data-ttu-id="9d8f3-139">![Icône d’ouverture de portail de l’appareil](images/emulator-deviceportal.png) **ouvrir le portail de périphérique**: ouvre le Portail d’appareil Windows pour le système d’exploitation HoloLens dans l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-139">![Open Device Portal icon](images/emulator-deviceportal.png) **Open Device Portal**: Open the Windows Device Portal for the HoloLens OS in the emulator.</span></span>  <span data-ttu-id="9d8f3-140">Pour la réalité mixte Windows, il peut être récupéré dans l’application de paramètres sous « Mise à jour et sécurité », puis « pour les développeurs » dans le « se connecter à l’aide de : « section sous « Portail de l’appareil Enable ».</span><span class="sxs-lookup"><span data-stu-id="9d8f3-140">For Windows Mixed Reality, this can be retrieved in the Settings app under "Update & Security", then "For developers" in the "Connect using:" section under "Enable Device Portal."</span></span>  <span data-ttu-id="9d8f3-141">Veillez à noter l’adresse IP et le port.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-141">Be sure to note both the IP address and port.</span></span>

<span data-ttu-id="9d8f3-142">Tout d’abord, vous devez appeler RestSimulationStreamSink.Create pour obtenir un objet RestSimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-142">First, you'll call RestSimulationStreamSink.Create to get a RestSimulationStreamSink object.</span></span> <span data-ttu-id="9d8f3-143">Il s’agit le périphérique cible ou l’émulateur qui contrôle via une connexion http.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-143">This is the target device or emulator that you will control over an http connection.</span></span> <span data-ttu-id="9d8f3-144">Vos commandes seront passés à et gérés par le [Windows Device Portal](using-the-windows-device-portal.md) en cours d’exécution sur le périphérique ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-144">Your commands will be passed to and handled by the [Windows Device Portal](using-the-windows-device-portal.md) running on the device or emulator.</span></span> <span data-ttu-id="9d8f3-145">Les quatre paramètres que vous aurez besoin pour créer un objet sont :</span><span class="sxs-lookup"><span data-stu-id="9d8f3-145">The four parameters you'll need to create an object are:</span></span>
* <span data-ttu-id="9d8f3-146">Uri de l’URI : adresse IP de l’appareil cible (par exemple, « http://123.123.123.123 « ou » http://123.123.123.123:50080 »)</span><span class="sxs-lookup"><span data-stu-id="9d8f3-146">Uri uri - IP address of the target device (e.g., "http://123.123.123.123" or "http://123.123.123.123:50080")</span></span>
* <span data-ttu-id="9d8f3-147">Informations d’identification System.Net.NetworkCredential - nom d’utilisateur/mot de passe pour se connecter à la [Windows Device Portal](using-the-windows-device-portal.md) sur l’appareil cible ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-147">System.Net.NetworkCredential credentials - Username/password for connecting to the [Windows Device Portal](using-the-windows-device-portal.md) on the target device or emulator.</span></span> <span data-ttu-id="9d8f3-148">Si vous vous connectez à l’émulateur par le biais de son adresse locale (par exemple, 168. *.* . \*) sur le même ordinateur, les informations d’identification seront acceptées.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-148">If you are connecting to the emulator via its local address (e.g., 168.*.*.\*) on the same PC, any credentials will be accepted.</span></span>
* <span data-ttu-id="9d8f3-149">bool normal - True pour une priorité normale, false pour une priorité basse.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-149">bool normal - True for normal priority, false for low priority.</span></span> <span data-ttu-id="9d8f3-150">Vous souhaitez généralement définir cela *true* pour les scénarios de test, ce qui permet à votre test afin de prendre le contrôle.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-150">You generally want to set this to *true* for test scenarios, which allows your test to take control.</span></span>  <span data-ttu-id="9d8f3-151">L’émulateur et la simulation de réalité mixte Windows utilisent des connexions de basse priorité.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-151">The emulator and Windows Mixed Reality simulation use low priority connections.</span></span>  <span data-ttu-id="9d8f3-152">Si votre test utilise également une connexion de faible priorité, le plus récemment été établie connexion sera dans le contrôle.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-152">If your test also uses a low priority connection, the most recently established connection will be in control.</span></span>
* <span data-ttu-id="9d8f3-153">Jeton System.Threading.CancellationToken - jeton pour annuler l’opération asynchrone.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-153">System.Threading.CancellationToken token - Token to cancel the async operation.</span></span>

<span data-ttu-id="9d8f3-154">Ensuite, vous allez créer le IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-154">Second you will create the IPerceptionSimulationManager.</span></span> <span data-ttu-id="9d8f3-155">Il s’agit de l’objet que vous utilisez pour contrôler la simulation.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-155">This is the object you use to control simulation.</span></span> <span data-ttu-id="9d8f3-156">Notez que cela doit également être effectuée dans une méthode async.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-156">Note that this must also be done in an async method.</span></span>

## <a name="control-the-simulated-human"></a><span data-ttu-id="9d8f3-157">Contrôle l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="9d8f3-157">Control the simulated Human</span></span>

<span data-ttu-id="9d8f3-158">Un IPerceptionSimulationManager a une propriété humain qui retourne un objet ISimulatedHuman.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-158">An IPerceptionSimulationManager has a Human property that returns an ISimulatedHuman object.</span></span> <span data-ttu-id="9d8f3-159">Pour contrôler l’être humain simulé, effectuer des opérations sur cet objet.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-159">To control the simulated human, perform operations on this object.</span></span> <span data-ttu-id="9d8f3-160">Exemple :</span><span class="sxs-lookup"><span data-stu-id="9d8f3-160">For example:</span></span>

```
manager.Human.Move(new Vector3(0.1f, 0.0f, 0.0f))
```

## <a name="basic-sample-c-console-application"></a><span data-ttu-id="9d8f3-161">Exemple de base C# application console</span><span class="sxs-lookup"><span data-stu-id="9d8f3-161">Basic Sample C# console application</span></span>

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
                        new Uri("http://169.254.227.115"),
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

## <a name="extended-sample-c-console-application"></a><span data-ttu-id="9d8f3-162">Étendue exemple C# application console</span><span class="sxs-lookup"><span data-stu-id="9d8f3-162">Extended Sample C# console application</span></span>

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
                        new Uri("http://169.254.227.115"),
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

## <a name="note-on-6-dof-controllers"></a><span data-ttu-id="9d8f3-163">Remarque sur les contrôleurs de 6-DDL</span><span class="sxs-lookup"><span data-stu-id="9d8f3-163">Note on 6-DOF controllers</span></span>

<span data-ttu-id="9d8f3-164">Avant d’appeler toutes les propriétés sur les méthodes sur un contrôleur de 6-DDL simulé, vous devez activer le contrôleur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-164">Before calling any properties on methods on a simulated 6-DOF controller, you must activate the controller.</span></span>  <span data-ttu-id="9d8f3-165">Contraire, cela entraîne une exception.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-165">Not doing so will result in an exception.</span></span>  <span data-ttu-id="9d8f3-166">À compter de Windows 10 peut 2019 mise à jour, les contrôleurs simulé 6-DDL peuvent être installés et activés en définissant la propriété d’état sur l’objet ISimulatedSixDofController à SimulatedSixDofControllerStatus.Active.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-166">Starting with the Windows 10 May 2019 Update, simulated 6-DOF controllers can be installed and activated by setting the Status property on the ISimulatedSixDofController object to SimulatedSixDofControllerStatus.Active.</span></span>
<span data-ttu-id="9d8f3-167">Dans les fenêtres de 10 octobre 2018 mettre à jour et versions antérieures, vous devez installer séparément un contrôleur simulé 6-DDL tout d’abord en appelant l’outil PerceptionSimulationDevice situé dans le dossier \Windows\System32.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-167">In the Windows 10 October 2018 Update and earlier, you must separately install a simulated 6-DOF controller first by calling the PerceptionSimulationDevice tool located in the \Windows\System32 folder.</span></span>  <span data-ttu-id="9d8f3-168">L’utilisation de cet outil est la suivante :</span><span class="sxs-lookup"><span data-stu-id="9d8f3-168">The usage of this tool is as follows:</span></span>


```
    PerceptionSimulationDevice.exe <action> 6dof <instance>
```

<span data-ttu-id="9d8f3-169">Exemple :</span><span class="sxs-lookup"><span data-stu-id="9d8f3-169">For example</span></span>

```
    PerceptionSimulationDevice.exe i 6dof 1
```

<span data-ttu-id="9d8f3-170">Actions prises en charge sont :</span><span class="sxs-lookup"><span data-stu-id="9d8f3-170">Supported actions are:</span></span>
* <span data-ttu-id="9d8f3-171">J’ai = install</span><span class="sxs-lookup"><span data-stu-id="9d8f3-171">i = install</span></span>
* <span data-ttu-id="9d8f3-172">q = query</span><span class="sxs-lookup"><span data-stu-id="9d8f3-172">q = query</span></span>
* <span data-ttu-id="9d8f3-173">r = supprimer</span><span class="sxs-lookup"><span data-stu-id="9d8f3-173">r = remove</span></span>

<span data-ttu-id="9d8f3-174">Les instances prises en charge sont :</span><span class="sxs-lookup"><span data-stu-id="9d8f3-174">Supported instances are:</span></span>
* <span data-ttu-id="9d8f3-175">1 = le contrôleur 6-DDL gauche</span><span class="sxs-lookup"><span data-stu-id="9d8f3-175">1 = the left 6-DOF controller</span></span>
* <span data-ttu-id="9d8f3-176">2 = le contrôleur 6-DDL droite</span><span class="sxs-lookup"><span data-stu-id="9d8f3-176">2 = the right 6-DOF controller</span></span>

<span data-ttu-id="9d8f3-177">Indique le code de sortie du processus de réussite (valeur de retour de zéro) ou l’échec (une valeur de retour différente de zéro).</span><span class="sxs-lookup"><span data-stu-id="9d8f3-177">The exit code of the process will indicate success (a zero return value) or failure (a non-zero return value).</span></span>  <span data-ttu-id="9d8f3-178">Lorsque vous utilisez l’action « q » pour interroger ou non un contrôleur est installé, la valeur de retour sera égal à zéro (0) si le contrôleur n’est pas déjà installé ou un (1) si le contrôleur est installé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-178">When using the 'q' action to query whether or not a controller is installed, the return value will be zero (0) if the controller is not already installed or one (1) if the controller is installed.</span></span>

<span data-ttu-id="9d8f3-179">Lors de la suppression d’un contrôleur sur les fenêtres de mise à jour 10 octobre 2018 ou antérieures, définissez son état à désactiver via l’API tout d’abord, puis appelez l’outil PerceptionSimulationDevice.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-179">When removing a controller on the Windows 10 October 2018 Update or earlier, set its status to Off via the API first, then call the PerceptionSimulationDevice tool.</span></span>

<span data-ttu-id="9d8f3-180">Notez que cet outil doit être exécuté en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-180">Note that this tool must be run as Administrator.</span></span>




## <a name="api-reference"></a><span data-ttu-id="9d8f3-181">Référence de l’API</span><span class="sxs-lookup"><span data-stu-id="9d8f3-181">API Reference</span></span>

### <a name="microsoftperceptionsimulationsimulateddevicetype"></a><span data-ttu-id="9d8f3-182">Microsoft.PerceptionSimulation.SimulatedDeviceType</span><span class="sxs-lookup"><span data-stu-id="9d8f3-182">Microsoft.PerceptionSimulation.SimulatedDeviceType</span></span>

<span data-ttu-id="9d8f3-183">Décrit un type d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="9d8f3-183">Describes a simulated device type</span></span>

```
public enum SimulatedDeviceType
{
    Reference = 0
}
```

<span data-ttu-id="9d8f3-184">**Microsoft.PerceptionSimulation.SimulatedDeviceType.Reference**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-184">**Microsoft.PerceptionSimulation.SimulatedDeviceType.Reference**</span></span>

<span data-ttu-id="9d8f3-185">Un appareil de référence fictive, la valeur par défaut pour PerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="9d8f3-185">A fictitious reference device, the default for PerceptionSimulationManager</span></span>

### <a name="microsoftperceptionsimulationheadtrackermode"></a><span data-ttu-id="9d8f3-186">Microsoft.PerceptionSimulation.HeadTrackerMode</span><span class="sxs-lookup"><span data-stu-id="9d8f3-186">Microsoft.PerceptionSimulation.HeadTrackerMode</span></span>

<span data-ttu-id="9d8f3-187">Décrit un mode de suivi de la tête</span><span class="sxs-lookup"><span data-stu-id="9d8f3-187">Describes a head tracker mode</span></span>

```
public enum HeadTrackerMode
{
    Default = 0,
    Orientation = 1,
    Position = 2
}
```

<span data-ttu-id="9d8f3-188">**Microsoft.PerceptionSimulation.HeadTrackerMode.Default**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-188">**Microsoft.PerceptionSimulation.HeadTrackerMode.Default**</span></span>

<span data-ttu-id="9d8f3-189">Valeur par défaut de la tête de suivi.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-189">Default Head Tracking.</span></span> <span data-ttu-id="9d8f3-190">Cela signifie que le système peut sélectionner la tête meilleures mode en fonction de conditions de runtime de suivi.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-190">This means the system may select the best head tracking mode based upon runtime conditions.</span></span>

<span data-ttu-id="9d8f3-191">**Microsoft.PerceptionSimulation.HeadTrackerMode.Orientation**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-191">**Microsoft.PerceptionSimulation.HeadTrackerMode.Orientation**</span></span>

<span data-ttu-id="9d8f3-192">Orientation principaux uniquement le suivi.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-192">Orientation Only Head Tracking.</span></span> <span data-ttu-id="9d8f3-193">Cela signifie que la position de suivi n’est peut-être pas fiable, et certaines fonctionnalités qui dépendent de la position principale n’est peut-être pas disponible.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-193">This means that the tracked position may not be reliable, and some functionality dependent on head position may not be available.</span></span>

<span data-ttu-id="9d8f3-194">**Microsoft.PerceptionSimulation.HeadTrackerMode.Position**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-194">**Microsoft.PerceptionSimulation.HeadTrackerMode.Position**</span></span>

<span data-ttu-id="9d8f3-195">Suivi de la tête positionnels.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-195">Positional Head Tracking.</span></span> <span data-ttu-id="9d8f3-196">Cela signifie que la position de tête suivie et l’orientation sont fiables</span><span class="sxs-lookup"><span data-stu-id="9d8f3-196">This means that the tracked head position and orientation are both reliable</span></span>

### <a name="microsoftperceptionsimulationsimulatedgesture"></a><span data-ttu-id="9d8f3-197">Microsoft.PerceptionSimulation.SimulatedGesture</span><span class="sxs-lookup"><span data-stu-id="9d8f3-197">Microsoft.PerceptionSimulation.SimulatedGesture</span></span>

<span data-ttu-id="9d8f3-198">Décrit un mouvement simulé</span><span class="sxs-lookup"><span data-stu-id="9d8f3-198">Describes a simulated gesture</span></span>

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

<span data-ttu-id="9d8f3-199">**Microsoft.PerceptionSimulation.SimulatedGesture.None**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-199">**Microsoft.PerceptionSimulation.SimulatedGesture.None**</span></span>

<span data-ttu-id="9d8f3-200">Valeur de sentinelle permettant de n’indiquer aucune mouvements.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-200">A sentinel value used to indicate no gestures.</span></span>

<span data-ttu-id="9d8f3-201">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerPressed**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-201">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerPressed**</span></span>

<span data-ttu-id="9d8f3-202">Un doigt enfoncé mouvement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-202">A finger pressed gesture.</span></span>

<span data-ttu-id="9d8f3-203">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerReleased**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-203">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerReleased**</span></span>

<span data-ttu-id="9d8f3-204">Un mouvement du doigt publié.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-204">A finger released gesture.</span></span>

<span data-ttu-id="9d8f3-205">**Microsoft.PerceptionSimulation.SimulatedGesture.Home**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-205">**Microsoft.PerceptionSimulation.SimulatedGesture.Home**</span></span>

<span data-ttu-id="9d8f3-206">Le mouvement accueil/système.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-206">The home/system gesture.</span></span>

<span data-ttu-id="9d8f3-207">**Microsoft.PerceptionSimulation.SimulatedGesture.Max**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-207">**Microsoft.PerceptionSimulation.SimulatedGesture.Max**</span></span>

<span data-ttu-id="9d8f3-208">Le mouvement valid maximal.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-208">The maximum valid gesture.</span></span>

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerstatus"></a><span data-ttu-id="9d8f3-209">Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus</span><span class="sxs-lookup"><span data-stu-id="9d8f3-209">Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus</span></span>

<span data-ttu-id="9d8f3-210">Les états possibles d’un contrôleur de 6-DDL simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-210">The possible states of a simulated 6-DOF controller.</span></span>

```
public enum SimulatedSixDofControllerStatus
{
    Off = 0,
    Active = 1,
    TrackingLost = 2,
}
```

<span data-ttu-id="9d8f3-211">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Off**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-211">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Off**</span></span>

<span data-ttu-id="9d8f3-212">Le contrôleur de 6-DDL est désactivé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-212">The 6-DOF controller is turned off.</span></span>

<span data-ttu-id="9d8f3-213">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Active**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-213">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Active**</span></span>

<span data-ttu-id="9d8f3-214">Le contrôleur de 6-DDL est activé et suivi.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-214">The 6-DOF controller is turned on and tracked.</span></span>

<span data-ttu-id="9d8f3-215">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.TrackingLost**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-215">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.TrackingLost**</span></span>

<span data-ttu-id="9d8f3-216">Le contrôleur de 6-DDL est activé, mais ne peut pas être suivi.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-216">The 6-DOF controller is turned on but cannot be tracked.</span></span>

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerbutton"></a><span data-ttu-id="9d8f3-217">Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton</span><span class="sxs-lookup"><span data-stu-id="9d8f3-217">Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton</span></span>

<span data-ttu-id="9d8f3-218">Boutons de la prise en charge sur un contrôleur de 6-DDL simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-218">The supported buttons on a simulated 6-DOF controller.</span></span>

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

<span data-ttu-id="9d8f3-219">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.None**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-219">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.None**</span></span>

<span data-ttu-id="9d8f3-220">Valeur de sentinelle permettant de n’indiquer aucun bouton.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-220">A sentinel value used to indicate no buttons.</span></span>

<span data-ttu-id="9d8f3-221">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Home**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-221">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Home**</span></span>

<span data-ttu-id="9d8f3-222">Le bouton d’accueil est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-222">The Home button is pressed.</span></span>

<span data-ttu-id="9d8f3-223">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Menu**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-223">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Menu**</span></span>

<span data-ttu-id="9d8f3-224">Le bouton de Menu est activé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-224">The Menu button is pressed.</span></span>

<span data-ttu-id="9d8f3-225">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Grip**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-225">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Grip**</span></span>

<span data-ttu-id="9d8f3-226">La poignée de bouton est enfoncée.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-226">The Grip button is pressed.</span></span>

<span data-ttu-id="9d8f3-227">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadPress**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-227">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadPress**</span></span>

<span data-ttu-id="9d8f3-228">Le pavé tactile est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-228">The TouchPad is pressed.</span></span>

<span data-ttu-id="9d8f3-229">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Select**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-229">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Select**</span></span>

<span data-ttu-id="9d8f3-230">Le bouton Sélectionner est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-230">The Select button is pressed.</span></span>

<span data-ttu-id="9d8f3-231">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadTouch**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-231">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadTouch**</span></span>

<span data-ttu-id="9d8f3-232">Le pavé tactile est touché.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-232">The TouchPad is touched.</span></span>

<span data-ttu-id="9d8f3-233">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Thumbstick**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-233">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Thumbstick**</span></span>

<span data-ttu-id="9d8f3-234">Le stick analogique est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-234">The Thumbstick is pressed.</span></span>

<span data-ttu-id="9d8f3-235">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Max**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-235">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Max**</span></span>

<span data-ttu-id="9d8f3-236">Le bouton maximum valid.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-236">The maximum valid button.</span></span>


### <a name="microsoftperceptionsimulationsimulatedeyescalibrationstate"></a><span data-ttu-id="9d8f3-237">Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState</span><span class="sxs-lookup"><span data-stu-id="9d8f3-237">Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState</span></span>

<span data-ttu-id="9d8f3-238">L’état de l’étalonnage des yeux simulés</span><span class="sxs-lookup"><span data-stu-id="9d8f3-238">The calibration state of the simulated eyes</span></span>

```
public enum SimulatedGesture
{
    Unavailable = 0,
    Ready = 1,
    Configuring = 2,
    UserCalibrationNeeded = 3
}
```

<span data-ttu-id="9d8f3-239">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Unavailable**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-239">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Unavailable**</span></span>

<span data-ttu-id="9d8f3-240">L’étalonnage yeux n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-240">The eyes calibration is unavailable.</span></span>

<span data-ttu-id="9d8f3-241">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Ready**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-241">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Ready**</span></span>

<span data-ttu-id="9d8f3-242">Les yeux ont été étalonnés.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-242">The eyes have been calibrated.</span></span>  <span data-ttu-id="9d8f3-243">Valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-243">This is the default value.</span></span>

<span data-ttu-id="9d8f3-244">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Configuring**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-244">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Configuring**</span></span>

<span data-ttu-id="9d8f3-245">Les yeux sont en cours d’étalonnage.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-245">The eyes are being calibrated.</span></span>

<span data-ttu-id="9d8f3-246">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.UserCalibrationNeeded**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-246">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.UserCalibrationNeeded**</span></span>

<span data-ttu-id="9d8f3-247">Les yeux ont besoin d’être étalonné.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-247">The eyes need to be calibrated.</span></span>

### <a name="microsoftperceptionsimulationsimulatedhandjointtrackingaccuracy"></a><span data-ttu-id="9d8f3-248">Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy</span><span class="sxs-lookup"><span data-stu-id="9d8f3-248">Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy</span></span>

<span data-ttu-id="9d8f3-249">La précision de suivi d’un joint de la main.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-249">The tracking accuracy of a joint of the hand.</span></span>

```
public enum SimulatedHandJointTrackingAccuracy
{
    Unavailable = 0,
    Approximate = 1,
    Visible = 2
}
```

<span data-ttu-id="9d8f3-250">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Unavailable**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-250">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Unavailable**</span></span>

<span data-ttu-id="9d8f3-251">La jointure n’est pas suivie.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-251">The joint is not tracked.</span></span>

<span data-ttu-id="9d8f3-252">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Approximate**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-252">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Approximate**</span></span>

<span data-ttu-id="9d8f3-253">La position commune est déduite.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-253">The joint position is inferred.</span></span>

<span data-ttu-id="9d8f3-254">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Visible**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-254">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Visible**</span></span>

<span data-ttu-id="9d8f3-255">La jointure est entièrement suivie.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-255">The joint is fully tracked.</span></span>

### <a name="microsoftperceptionsimulationsimulatedhandpose"></a><span data-ttu-id="9d8f3-256">Microsoft.PerceptionSimulation.SimulatedHandPose</span><span class="sxs-lookup"><span data-stu-id="9d8f3-256">Microsoft.PerceptionSimulation.SimulatedHandPose</span></span>

<span data-ttu-id="9d8f3-257">La précision de suivi d’un joint de la main.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-257">The tracking accuracy of a joint of the hand.</span></span>

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

<span data-ttu-id="9d8f3-258">**Microsoft.PerceptionSimulation.SimulatedHandPose.Closed**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-258">**Microsoft.PerceptionSimulation.SimulatedHandPose.Closed**</span></span>

<span data-ttu-id="9d8f3-259">ARTICULATIONS du doigt de l’aiguille sont configurées pour refléter une pose fermée.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-259">The hand's finger joints are configured to reflect a closed pose.</span></span>

<span data-ttu-id="9d8f3-260">**Microsoft.PerceptionSimulation.SimulatedHandPose.Open**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-260">**Microsoft.PerceptionSimulation.SimulatedHandPose.Open**</span></span>

<span data-ttu-id="9d8f3-261">Joints du doigt de l’aiguille sont configurés pour refléter une pose ouvert.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-261">The hand's finger joints are configured to reflect an open pose.</span></span>

<span data-ttu-id="9d8f3-262">**Microsoft.PerceptionSimulation.SimulatedHandPose.Point**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-262">**Microsoft.PerceptionSimulation.SimulatedHandPose.Point**</span></span>

<span data-ttu-id="9d8f3-263">ARTICULATIONS du doigt de l’aiguille sont configurées pour refléter une pose de pointage.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-263">The hand's finger joints are configured to reflect a pointing pose.</span></span>

<span data-ttu-id="9d8f3-264">**Microsoft.PerceptionSimulation.SimulatedHandPose.Pinch**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-264">**Microsoft.PerceptionSimulation.SimulatedHandPose.Pinch**</span></span>

<span data-ttu-id="9d8f3-265">ARTICULATIONS du doigt de l’aiguille sont configurées pour refléter une pose pincement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-265">The hand's finger joints are configured to reflect a pinching pose.</span></span>

<span data-ttu-id="9d8f3-266">**Microsoft.PerceptionSimulation.SimulatedHandPose.Max**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-266">**Microsoft.PerceptionSimulation.SimulatedHandPose.Max**</span></span>

<span data-ttu-id="9d8f3-267">La valeur maximale valide pour SimulatedHandPose.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-267">The maximum valid value for SimulatedHandPose.</span></span>


### <a name="microsoftperceptionsimulationplaybackstate"></a><span data-ttu-id="9d8f3-268">Microsoft.PerceptionSimulation.PlaybackState</span><span class="sxs-lookup"><span data-stu-id="9d8f3-268">Microsoft.PerceptionSimulation.PlaybackState</span></span>

<span data-ttu-id="9d8f3-269">Décrit l’état d’une lecture.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-269">Describes the state of a playback.</span></span>

```
public enum PlaybackState
{
    Stopped = 0,
    Playing = 1,
    Paused = 2,
    End = 3,
}
```

<span data-ttu-id="9d8f3-270">**Microsoft.PerceptionSimulation.PlaybackState.Stopped**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-270">**Microsoft.PerceptionSimulation.PlaybackState.Stopped**</span></span>

<span data-ttu-id="9d8f3-271">L’enregistrement est actuellement arrêté et prêt pour la lecture.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-271">The recording is currently stopped and ready for playback.</span></span>

<span data-ttu-id="9d8f3-272">**Microsoft.PerceptionSimulation.PlaybackState.Playing**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-272">**Microsoft.PerceptionSimulation.PlaybackState.Playing**</span></span>

<span data-ttu-id="9d8f3-273">L’enregistrement en cours de lecture.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-273">The recording is currently playing.</span></span>

<span data-ttu-id="9d8f3-274">**Microsoft.PerceptionSimulation.PlaybackState.Paused**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-274">**Microsoft.PerceptionSimulation.PlaybackState.Paused**</span></span>

<span data-ttu-id="9d8f3-275">L’enregistrement est actuellement suspendu.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-275">The recording is currently paused.</span></span>

<span data-ttu-id="9d8f3-276">**Microsoft.PerceptionSimulation.PlaybackState.End**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-276">**Microsoft.PerceptionSimulation.PlaybackState.End**</span></span>

<span data-ttu-id="9d8f3-277">L’enregistrement a atteint la fin.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-277">The recording has reached the end.</span></span>

### <a name="microsoftperceptionsimulationvector3"></a><span data-ttu-id="9d8f3-278">Microsoft.PerceptionSimulation.Vector3</span><span class="sxs-lookup"><span data-stu-id="9d8f3-278">Microsoft.PerceptionSimulation.Vector3</span></span>

<span data-ttu-id="9d8f3-279">Décrit un vecteur de 3 composants, ce qui peut décrire un point ou un vecteur dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-279">Describes a 3 components vector, which might describe a point or a vector in 3D space.</span></span>

```
public struct Vector3
{
    public float X;
    public float Y;
    public float Z;
    public Vector3(float x, float y, float z);
}
```

<span data-ttu-id="9d8f3-280">**Microsoft.PerceptionSimulation.Vector3.X**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-280">**Microsoft.PerceptionSimulation.Vector3.X**</span></span>

<span data-ttu-id="9d8f3-281">Le composant X du vecteur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-281">The X component of the vector.</span></span>

<span data-ttu-id="9d8f3-282">**Microsoft.PerceptionSimulation.Vector3.Y**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-282">**Microsoft.PerceptionSimulation.Vector3.Y**</span></span>

<span data-ttu-id="9d8f3-283">Le composant Y du vecteur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-283">The Y component of the vector.</span></span>

<span data-ttu-id="9d8f3-284">**Microsoft.PerceptionSimulation.Vector3.Z**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-284">**Microsoft.PerceptionSimulation.Vector3.Z**</span></span>

<span data-ttu-id="9d8f3-285">Le composant Z du vecteur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-285">The Z component of the vector.</span></span>

<span data-ttu-id="9d8f3-286">**Microsoft.PerceptionSimulation.Vector3.#ctor(System.Single,System.Single,System.Single)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-286">**Microsoft.PerceptionSimulation.Vector3.#ctor(System.Single,System.Single,System.Single)**</span></span>

<span data-ttu-id="9d8f3-287">Construire un nouveau Vector3.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-287">Construct a new Vector3.</span></span>

<span data-ttu-id="9d8f3-288">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-288">Parameters</span></span>
* <span data-ttu-id="9d8f3-289">x - composant x du vecteur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-289">x - The x component of the vector.</span></span>
* <span data-ttu-id="9d8f3-290">y - composant y du vecteur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-290">y - The y component of the vector.</span></span>
* <span data-ttu-id="9d8f3-291">z - composant z du vecteur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-291">z - The z component of the vector.</span></span>

### <a name="microsoftperceptionsimulationrotation3"></a><span data-ttu-id="9d8f3-292">Microsoft.PerceptionSimulation.Rotation3</span><span class="sxs-lookup"><span data-stu-id="9d8f3-292">Microsoft.PerceptionSimulation.Rotation3</span></span>

<span data-ttu-id="9d8f3-293">Décrit une rotation de 3 composants.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-293">Describes a 3 components rotation.</span></span>

```
public struct Rotation3
{
    public float Pitch;
    public float Yaw;
    public float Roll;
    public Rotation3(float pitch, float yaw, float roll);
}
```

<span data-ttu-id="9d8f3-294">**Microsoft.PerceptionSimulation.Rotation3.Pitch**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-294">**Microsoft.PerceptionSimulation.Rotation3.Pitch**</span></span>

<span data-ttu-id="9d8f3-295">Le composant de hauteur de la Rotation, vers le bas autour de l’axe X.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-295">The Pitch component of the Rotation, down around the X axis.</span></span>

<span data-ttu-id="9d8f3-296">**Microsoft.PerceptionSimulation.Rotation3.Yaw**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-296">**Microsoft.PerceptionSimulation.Rotation3.Yaw**</span></span>

<span data-ttu-id="9d8f3-297">Le composant lacet de Rotation vers la droite autour de l’axe Y.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-297">The Yaw component of the Rotation, right around the Y axis.</span></span>

<span data-ttu-id="9d8f3-298">**Microsoft.PerceptionSimulation.Rotation3.Roll**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-298">**Microsoft.PerceptionSimulation.Rotation3.Roll**</span></span>

<span data-ttu-id="9d8f3-299">Le composant de la restauration de la Rotation autour de l’axe Z.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-299">The Roll component of the Rotation, right around the Z axis.</span></span>

<span data-ttu-id="9d8f3-300">**Microsoft.PerceptionSimulation.Rotation3.#ctor(System.Single,System.Single,System.Single)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-300">**Microsoft.PerceptionSimulation.Rotation3.#ctor(System.Single,System.Single,System.Single)**</span></span>

<span data-ttu-id="9d8f3-301">Construire un nouveau Rotation3.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-301">Construct a new Rotation3.</span></span>

<span data-ttu-id="9d8f3-302">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-302">Parameters</span></span>
* <span data-ttu-id="9d8f3-303">pitch - le composant de hauteur de la Rotation.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-303">pitch - The pitch component of the Rotation.</span></span>
* <span data-ttu-id="9d8f3-304">lacet - le composant lacet de la Rotation.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-304">yaw - The yaw component of the Rotation.</span></span>
* <span data-ttu-id="9d8f3-305">restauration - le composant de restauration de la Rotation.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-305">roll - The roll component of the Rotation.</span></span>

### <a name="microsoftperceptionsimulationsimulatedhandjointconfiguration"></a><span data-ttu-id="9d8f3-306">Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration</span><span class="sxs-lookup"><span data-stu-id="9d8f3-306">Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration</span></span>

<span data-ttu-id="9d8f3-307">Décrit la configuration d’un joint d’une part simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-307">Describes the configuration of a joint on a simulated hand.</span></span>

```
public struct SimulatedHandJointConfiguration
{
    public Vector3 Position;
    public Rotation3 Rotation;
    public SimulatedHandJointTrackingAccuracy TrackingAccuracy;
}
```

<span data-ttu-id="9d8f3-308">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Position**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-308">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Position**</span></span>

<span data-ttu-id="9d8f3-309">La position de la jointure.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-309">The position of the joint.</span></span>

<span data-ttu-id="9d8f3-310">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Rotation**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-310">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Rotation**</span></span>

<span data-ttu-id="9d8f3-311">La rotation de la jointure.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-311">The rotation of the joint.</span></span>

<span data-ttu-id="9d8f3-312">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.TrackingAccuracy**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-312">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.TrackingAccuracy**</span></span>

<span data-ttu-id="9d8f3-313">La précision de suivi de la jointure.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-313">The tracking accuracy of the joint.</span></span>


### <a name="microsoftperceptionsimulationfrustum"></a><span data-ttu-id="9d8f3-314">Microsoft.PerceptionSimulation.Frustum</span><span class="sxs-lookup"><span data-stu-id="9d8f3-314">Microsoft.PerceptionSimulation.Frustum</span></span>

<span data-ttu-id="9d8f3-315">Décrit un frustum vue, comme cela est généralement utilisé par un appareil photo.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-315">Describes a view frustum, as typically used by a camera.</span></span>

```
public struct Frustum
{
    float Near;
    float Far;
    float FieldOfView;
    float AspectRatio;
}
```

<span data-ttu-id="9d8f3-316">**Microsoft.PerceptionSimulation.Frustum.Near**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-316">**Microsoft.PerceptionSimulation.Frustum.Near**</span></span>

<span data-ttu-id="9d8f3-317">La distance minimale qui est contenue dans le frustum.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-317">The minimum distance that is contained in the frustum.</span></span>

<span data-ttu-id="9d8f3-318">**Microsoft.PerceptionSimulation.Frustum.Far**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-318">**Microsoft.PerceptionSimulation.Frustum.Far**</span></span>

<span data-ttu-id="9d8f3-319">La distance maximale qui est contenue dans le frustum.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-319">The maximum distance that is contained in the frustum.</span></span>

<span data-ttu-id="9d8f3-320">**Microsoft.PerceptionSimulation.Frustum.FieldOfView**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-320">**Microsoft.PerceptionSimulation.Frustum.FieldOfView**</span></span>

<span data-ttu-id="9d8f3-321">Le champ de vision horizontal de la frustum, en radians (inférieur à PI).</span><span class="sxs-lookup"><span data-stu-id="9d8f3-321">The horizontal field of view of the frustum, in radians (less than PI).</span></span>

<span data-ttu-id="9d8f3-322">**Microsoft.PerceptionSimulation.Frustum.AspectRatio**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-322">**Microsoft.PerceptionSimulation.Frustum.AspectRatio**</span></span>

<span data-ttu-id="9d8f3-323">Le ratio de champ de vision horizontal pour le champ de vision verticale.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-323">The ratio of horizontal field of view to vertical field of view.</span></span>

### <a name="microsoftperceptionsimulationiperceptionsimulationmanager"></a><span data-ttu-id="9d8f3-324">Microsoft.PerceptionSimulation.IPerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="9d8f3-324">Microsoft.PerceptionSimulation.IPerceptionSimulationManager</span></span>

<span data-ttu-id="9d8f3-325">Racine pour générer les paquets permettent de contrôler un appareil.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-325">Root for generating the packets used to control a device.</span></span>

```
public interface IPerceptionSimulationManager
{   
    ISimulatedDevice Device { get; }
    ISimulatedHuman Human { get; }
    void Reset();
}
```

<span data-ttu-id="9d8f3-326">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Device**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-326">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Device**</span></span>

<span data-ttu-id="9d8f3-327">Récupérer l’objet de périphérique simulé qui interprète l’être humain simulé et le monde simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-327">Retrieve the simulated device object that interprets the simulated human and the simulated world.</span></span>

<span data-ttu-id="9d8f3-328">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Human**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-328">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Human**</span></span>

<span data-ttu-id="9d8f3-329">Récupérer l’objet qui contrôle l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-329">Retrieve the object that controls the simulated human.</span></span>

<span data-ttu-id="9d8f3-330">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Reset**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-330">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Reset**</span></span>

<span data-ttu-id="9d8f3-331">Réinitialise la simulation à son état par défaut.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-331">Resets the simulation to its default state.</span></span>

### <a name="microsoftperceptionsimulationisimulateddevice"></a><span data-ttu-id="9d8f3-332">Microsoft.PerceptionSimulation.ISimulatedDevice</span><span class="sxs-lookup"><span data-stu-id="9d8f3-332">Microsoft.PerceptionSimulation.ISimulatedDevice</span></span>

<span data-ttu-id="9d8f3-333">Interface décrivant l’appareil qui interprète le monde simulé et l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="9d8f3-333">Interface describing the device which interprets the simulated world and the simulated human</span></span>

```
public interface ISimulatedDevice
{
    ISimulatedHeadTracker HeadTracker { get; }
    ISimulatedHandTracker HandTracker { get; }
    void SetSimulatedDeviceType(SimulatedDeviceType type);
}
```

<span data-ttu-id="9d8f3-334">**Microsoft.PerceptionSimulation.ISimulatedDevice.HeadTracker**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-334">**Microsoft.PerceptionSimulation.ISimulatedDevice.HeadTracker**</span></span>

<span data-ttu-id="9d8f3-335">Récupérer la tête de la mise hors tension à partir de l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-335">Retrieve the Head Tracker from the Simulated Device.</span></span>

<span data-ttu-id="9d8f3-336">**Microsoft.PerceptionSimulation.ISimulatedDevice.HandTracker**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-336">**Microsoft.PerceptionSimulation.ISimulatedDevice.HandTracker**</span></span>

<span data-ttu-id="9d8f3-337">Récupérer le dispositif de suivi disponible à partir de l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-337">Retrieve the Hand Tracker from the Simulated Device.</span></span>

<span data-ttu-id="9d8f3-338">**Microsoft.PerceptionSimulation.ISimulatedDevice.SetSimulatedDeviceType(Microsoft.PerceptionSimulation.SimulatedDeviceType)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-338">**Microsoft.PerceptionSimulation.ISimulatedDevice.SetSimulatedDeviceType(Microsoft.PerceptionSimulation.SimulatedDeviceType)**</span></span>

<span data-ttu-id="9d8f3-339">Définissez les propriétés de l’appareil simulé pour correspondre au type de l’appareil fourni.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-339">Set the properties of the simulated device to match the provided device type.</span></span>

<span data-ttu-id="9d8f3-340">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-340">Parameters</span></span>
* <span data-ttu-id="9d8f3-341">type - le nouveau type d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="9d8f3-341">type - The new type of Simulated Device</span></span>

### <a name="microsoftperceptionsimulationisimulatedheadtracker"></a><span data-ttu-id="9d8f3-342">Microsoft.PerceptionSimulation.ISimulatedHeadTracker</span><span class="sxs-lookup"><span data-stu-id="9d8f3-342">Microsoft.PerceptionSimulation.ISimulatedHeadTracker</span></span>

<span data-ttu-id="9d8f3-343">Interface décrivant la partie de l’appareil simulé qui assure le suivi de la tête de l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-343">Interface describing the portion of the simulated device that tracks the head of the simulated human.</span></span>

```
public interface ISimulatedHeadTracker
{
    HeadTrackerMode HeadTrackerMode { get; set; }
};
```

<span data-ttu-id="9d8f3-344">**Microsoft.PerceptionSimulation.ISimulatedHeadTracker.HeadTrackerMode**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-344">**Microsoft.PerceptionSimulation.ISimulatedHeadTracker.HeadTrackerMode**</span></span>

<span data-ttu-id="9d8f3-345">Récupère et définit le mode de suivi de la tête actuel.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-345">Retrieves and sets the current head tracker mode.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhandtracker"></a><span data-ttu-id="9d8f3-346">Microsoft.PerceptionSimulation.ISimulatedHandTracker</span><span class="sxs-lookup"><span data-stu-id="9d8f3-346">Microsoft.PerceptionSimulation.ISimulatedHandTracker</span></span>

<span data-ttu-id="9d8f3-347">Interface décrivant la partie de l’appareil simulé qui assure le suivi entre les mains de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="9d8f3-347">Interface describing the portion of the simulated device that tracks the hands of the simulated human</span></span>

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

<span data-ttu-id="9d8f3-348">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-348">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.WorldPosition**</span></span>

<span data-ttu-id="9d8f3-349">Récupérer la position du nœud en relation avec le monde entier, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-349">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="9d8f3-350">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Position**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-350">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Position**</span></span>

<span data-ttu-id="9d8f3-351">Récupérer et définir la position du dispositif de suivi main simulé, par rapport au centre de la tête.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-351">Retrieve and set the position of the simulated hand tracker, relative to the center of the head.</span></span>

<span data-ttu-id="9d8f3-352">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Pitch**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-352">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Pitch**</span></span>

<span data-ttu-id="9d8f3-353">Récupérez et définissez le pas vers le bas du dispositif de suivi main simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-353">Retrieve and set the downward pitch of the simulated hand tracker.</span></span>

<span data-ttu-id="9d8f3-354">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.FrustumIgnored**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-354">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.FrustumIgnored**</span></span>

<span data-ttu-id="9d8f3-355">Récupérez et définissez si le frustum du dispositif de suivi main simulé est ignoré.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-355">Retrieve and set whether the frustum of the simulated hand tracker is ignored.</span></span> <span data-ttu-id="9d8f3-356">Lorsque ignorées, deux mains sont toujours visibles.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-356">When ignored, both hands are always visible.</span></span> <span data-ttu-id="9d8f3-357">Lorsque ne pas ignorées (la valeur par défaut) mains affichent uniquement quand ils se trouvent dans le frustum du dispositif de suivi de main.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-357">When not ignored (the default) hands are only visible when they are within the frustum of the hand tracker.</span></span>

<span data-ttu-id="9d8f3-358">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Frustum**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-358">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Frustum**</span></span>

<span data-ttu-id="9d8f3-359">Récupérer et définir les propriétés de frustum permet de déterminer si les mains sont visibles au dispositif de suivi main simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-359">Retrieve and set the frustum properties used to determine if hands are visible to the simulated hand tracker.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhuman"></a><span data-ttu-id="9d8f3-360">Microsoft.PerceptionSimulation.ISimulatedHuman</span><span class="sxs-lookup"><span data-stu-id="9d8f3-360">Microsoft.PerceptionSimulation.ISimulatedHuman</span></span>

<span data-ttu-id="9d8f3-361">Interface de niveau supérieur pour le contrôle de l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-361">Top level interface for controlling the simulated human.</span></span>

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

<span data-ttu-id="9d8f3-362">**Microsoft.PerceptionSimulation.ISimulatedHuman.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-362">**Microsoft.PerceptionSimulation.ISimulatedHuman.WorldPosition**</span></span>

<span data-ttu-id="9d8f3-363">Récupérer et définir la position du nœud en relation avec le monde entier, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-363">Retrieve and set the position of the node with relation to the world, in meters.</span></span> <span data-ttu-id="9d8f3-364">La position correspond à un point dans le centre de mètres près de l’être humain.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-364">The position corresponds to a point at the center of the human's feet.</span></span>

<span data-ttu-id="9d8f3-365">**Microsoft.PerceptionSimulation.ISimulatedHuman.Direction**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-365">**Microsoft.PerceptionSimulation.ISimulatedHuman.Direction**</span></span>

<span data-ttu-id="9d8f3-366">Récupérer et définir la direction des visages humains simulés dans le monde.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-366">Retrieve and set the direction the simulated human faces in the world.</span></span> <span data-ttu-id="9d8f3-367">visages de 0 radian vers le bas de l’axe Z négatif.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-367">0 radians faces down the negative Z axis.</span></span> <span data-ttu-id="9d8f3-368">Radians positif rotation dans le sens horaire sur l’axe des Y.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-368">Positive radians rotate clockwise about the Y axis.</span></span>

<span data-ttu-id="9d8f3-369">**Microsoft.PerceptionSimulation.ISimulatedHuman.Height**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-369">**Microsoft.PerceptionSimulation.ISimulatedHuman.Height**</span></span>

<span data-ttu-id="9d8f3-370">Récupérer et définir la hauteur de l’être humain simulé, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-370">Retrieve and set the height of the simulated human, in meters.</span></span>

<span data-ttu-id="9d8f3-371">**Microsoft.PerceptionSimulation.ISimulatedHuman.LeftHand**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-371">**Microsoft.PerceptionSimulation.ISimulatedHuman.LeftHand**</span></span>

<span data-ttu-id="9d8f3-372">Récupérer la main gauche de l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-372">Retrieve the left hand of the simulated human.</span></span>

<span data-ttu-id="9d8f3-373">**Microsoft.PerceptionSimulation.ISimulatedHuman.RightHand**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-373">**Microsoft.PerceptionSimulation.ISimulatedHuman.RightHand**</span></span>

<span data-ttu-id="9d8f3-374">Récupérer la partie droite de l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-374">Retrieve the right hand of the simulated human.</span></span>

<span data-ttu-id="9d8f3-375">**Microsoft.PerceptionSimulation.ISimulatedHuman.Head**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-375">**Microsoft.PerceptionSimulation.ISimulatedHuman.Head**</span></span>

<span data-ttu-id="9d8f3-376">Récupérer la tête de l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-376">Retrieve the head of the simulated human.</span></span>

<span data-ttu-id="9d8f3-377">**Microsoft.PerceptionSimulation.ISimulatedHuman.Move(Microsoft.PerceptionSimulation.Vector3)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-377">**Microsoft.PerceptionSimulation.ISimulatedHuman.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="9d8f3-378">Déplacer l’être humain simulé par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-378">Move the simulated human relative to its current position, in meters.</span></span>

<span data-ttu-id="9d8f3-379">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-379">Parameters</span></span>
* <span data-ttu-id="9d8f3-380">traduction - la traduction à déplacer, par rapport à la position actuelle.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-380">translation - The translation to move, relative to current position.</span></span>

<span data-ttu-id="9d8f3-381">**Microsoft.PerceptionSimulation.ISimulatedHuman.Rotate(System.Single)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-381">**Microsoft.PerceptionSimulation.ISimulatedHuman.Rotate(System.Single)**</span></span>

<span data-ttu-id="9d8f3-382">Faire pivoter l’être humain simulé par rapport à sa direction actuelle, dans le sens horaire autour de l’axe Y</span><span class="sxs-lookup"><span data-stu-id="9d8f3-382">Rotate the simulated human relative to its current direction, clockwise about the Y axis</span></span>

<span data-ttu-id="9d8f3-383">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-383">Parameters</span></span>
* <span data-ttu-id="9d8f3-384">radians - la quantité pour faire pivoter autour de l’axe Y.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-384">radians - The amount to rotate around the Y axis.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhuman2"></a><span data-ttu-id="9d8f3-385">Microsoft.PerceptionSimulation.ISimulatedHuman2</span><span class="sxs-lookup"><span data-stu-id="9d8f3-385">Microsoft.PerceptionSimulation.ISimulatedHuman2</span></span>

<span data-ttu-id="9d8f3-386">Propriétés supplémentaires sont disponibles en effectuant un cast de la ISimulatedHuman à ISimulatedHuman2</span><span class="sxs-lookup"><span data-stu-id="9d8f3-386">Additional properties are available by casting the ISimulatedHuman to ISimulatedHuman2</span></span>

```
public interface ISimulatedHuman2
{
    /* New members in addition to those available on ISimulatedHuman */
    ISimulatedSixDofController LeftController { get; }
    ISimulatedSixDofController RightController { get; }
}
```

<span data-ttu-id="9d8f3-387">**Microsoft.PerceptionSimulation.ISimulatedHuman2.LeftController**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-387">**Microsoft.PerceptionSimulation.ISimulatedHuman2.LeftController**</span></span>

<span data-ttu-id="9d8f3-388">Récupérer le contrôleur gauche 6-DDL.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-388">Retrieve the left 6-DOF controller.</span></span>

<span data-ttu-id="9d8f3-389">**Microsoft.PerceptionSimulation.ISimulatedHuman2.RightController**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-389">**Microsoft.PerceptionSimulation.ISimulatedHuman2.RightController**</span></span>

<span data-ttu-id="9d8f3-390">Récupérer le contrôleur de droite 6-DDL.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-390">Retrieve the right 6-DOF controller.</span></span>


### <a name="microsoftperceptionsimulationisimulatedhand"></a><span data-ttu-id="9d8f3-391">Microsoft.PerceptionSimulation.ISimulatedHand</span><span class="sxs-lookup"><span data-stu-id="9d8f3-391">Microsoft.PerceptionSimulation.ISimulatedHand</span></span>

<span data-ttu-id="9d8f3-392">Interface décrivant une main de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="9d8f3-392">Interface describing a hand of the simulated human</span></span>

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

<span data-ttu-id="9d8f3-393">**Microsoft.PerceptionSimulation.ISimulatedHand.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-393">**Microsoft.PerceptionSimulation.ISimulatedHand.WorldPosition**</span></span>

<span data-ttu-id="9d8f3-394">Récupérer la position du nœud en relation avec le monde entier, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-394">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="9d8f3-395">**Microsoft.PerceptionSimulation.ISimulatedHand.Position**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-395">**Microsoft.PerceptionSimulation.ISimulatedHand.Position**</span></span>

<span data-ttu-id="9d8f3-396">Récupérer et définir la position de la main simulée par rapport à l’être humain, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-396">Retrieve and set the position of the simulated hand relative to the human, in meters.</span></span>

<span data-ttu-id="9d8f3-397">**Microsoft.PerceptionSimulation.ISimulatedHand.Activated**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-397">**Microsoft.PerceptionSimulation.ISimulatedHand.Activated**</span></span>

<span data-ttu-id="9d8f3-398">Récupérez et définissez la valeur indiquant si la main est actuellement activée.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-398">Retrieve and set whether the hand is currently activated.</span></span>

<span data-ttu-id="9d8f3-399">**Microsoft.PerceptionSimulation.ISimulatedHand.Visible**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-399">**Microsoft.PerceptionSimulation.ISimulatedHand.Visible**</span></span>

<span data-ttu-id="9d8f3-400">Récupérer si la main est actuellement visible pour le SimulatedDevice (si elle est dans une position pour être détecté par le HandTracker).</span><span class="sxs-lookup"><span data-stu-id="9d8f3-400">Retrieve whether the hand is currently visible to the SimulatedDevice (ie, whether it's in a position to be detected by the HandTracker).</span></span>

<span data-ttu-id="9d8f3-401">**Microsoft.PerceptionSimulation.ISimulatedHand.EnsureVisible**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-401">**Microsoft.PerceptionSimulation.ISimulatedHand.EnsureVisible**</span></span>

<span data-ttu-id="9d8f3-402">Déplacer la main tel qu’il soit visible par le SimulatedDevice.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-402">Move the hand such that it is visible to the SimulatedDevice.</span></span>

<span data-ttu-id="9d8f3-403">**Microsoft.PerceptionSimulation.ISimulatedHand.Move(Microsoft.PerceptionSimulation.Vector3)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-403">**Microsoft.PerceptionSimulation.ISimulatedHand.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="9d8f3-404">Déplacer la position de la main simulée par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-404">Move the position of the simulated hand relative to its current position, in meters.</span></span>

<span data-ttu-id="9d8f3-405">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-405">Parameters</span></span>
* <span data-ttu-id="9d8f3-406">traduction - quantité de laquelle translater la main simulée.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-406">translation - The amount to translate the simulated hand.</span></span>

<span data-ttu-id="9d8f3-407">**Microsoft.PerceptionSimulation.ISimulatedHand.PerformGesture(Microsoft.PerceptionSimulation.SimulatedGesture)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-407">**Microsoft.PerceptionSimulation.ISimulatedHand.PerformGesture(Microsoft.PerceptionSimulation.SimulatedGesture)**</span></span>

<span data-ttu-id="9d8f3-408">Effectuer un mouvement à l’aide de la main simulée.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-408">Perform a gesture using the simulated hand.</span></span>  <span data-ttu-id="9d8f3-409">Elle sera détectée par le système uniquement si la main est activée.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-409">It will only be detected by the system if the hand is enabled.</span></span>

<span data-ttu-id="9d8f3-410">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-410">Parameters</span></span>
* <span data-ttu-id="9d8f3-411">mouvement - mouvement à effectuer.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-411">gesture - The gesture to perform.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhand2"></a><span data-ttu-id="9d8f3-412">Microsoft.PerceptionSimulation.ISimulatedHand2</span><span class="sxs-lookup"><span data-stu-id="9d8f3-412">Microsoft.PerceptionSimulation.ISimulatedHand2</span></span>

<span data-ttu-id="9d8f3-413">Propriétés supplémentaires sont disponibles en effectuant un cast d’un ISimulatedHand à ISimulatedHand2.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-413">Additional properties are available by casting an ISimulatedHand to ISimulatedHand2.</span></span>
```
public interface ISimulatedHand2
{
    /* New members in addition to those available on ISimulatedHand */
    Rotation3 Orientation { get; set; }
}
```

<span data-ttu-id="9d8f3-414">**Microsoft.PerceptionSimulation.ISimulatedHand2.Orientation**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-414">**Microsoft.PerceptionSimulation.ISimulatedHand2.Orientation**</span></span>

<span data-ttu-id="9d8f3-415">Récupérer ou définir la rotation de l’aiguille simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-415">Retrieve or set the rotation of the simulated hand.</span></span>  <span data-ttu-id="9d8f3-416">Radians rotation horaire lors de la recherche sur l’axe positif.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-416">Positive radians rotate clockwise when looking along the axis.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhand3"></a><span data-ttu-id="9d8f3-417">Microsoft.PerceptionSimulation.ISimulatedHand3</span><span class="sxs-lookup"><span data-stu-id="9d8f3-417">Microsoft.PerceptionSimulation.ISimulatedHand3</span></span>

<span data-ttu-id="9d8f3-418">Propriétés supplémentaires sont disponibles en effectuant un cast d’un ISimulatedHand à ISimulatedHand3</span><span class="sxs-lookup"><span data-stu-id="9d8f3-418">Additional properties are available by casting an ISimulatedHand to ISimulatedHand3</span></span>
```
public interface ISimulatedHand3
{
    /* New members in addition to those available on ISimulatedHand and ISimulatedHand2 */
    GetJointConfiguration(SimulatedHandJoint joint, out SimulatedHandJointConfiguration jointConfiguration);
    SetJointConfiguration(SimulatedHandJoint joint, SimulatedHandJointConfiguration jointConfiguration);
    SetHandPose(SimulatedHandPose pose, bool animate);
}
```

<span data-ttu-id="9d8f3-419">**Microsoft.PerceptionSimulation.ISimulatedHand3.GetJointConfiguration**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-419">**Microsoft.PerceptionSimulation.ISimulatedHand3.GetJointConfiguration**</span></span>

<span data-ttu-id="9d8f3-420">Obtenir la configuration commune pour la liaison spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-420">Get the joint configuration for the specified joint.</span></span>

<span data-ttu-id="9d8f3-421">**Microsoft.PerceptionSimulation.ISimulatedHand3.SetJointConfiguration**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-421">**Microsoft.PerceptionSimulation.ISimulatedHand3.SetJointConfiguration**</span></span>

<span data-ttu-id="9d8f3-422">Définissez la configuration commune pour la liaison spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-422">Set the joint configuration for the specified joint.</span></span>

<span data-ttu-id="9d8f3-423">**Microsoft.PerceptionSimulation.ISimulatedHand3.SetHandPose**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-423">**Microsoft.PerceptionSimulation.ISimulatedHand3.SetHandPose**</span></span>

<span data-ttu-id="9d8f3-424">Une pose connue avec un indicateur facultatif pour animer la valeur la main.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-424">Set the hand to a known pose with an optional flag to animate.</span></span>  <span data-ttu-id="9d8f3-425">Remarque : animation n’obtiendriez pas articulations immédiatement refléter leurs configurations mixte finales.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-425">Note: animating won't result in joints immediately reflecting their final joint configurations.</span></span>


### <a name="microsoftperceptionsimulationisimulatedhead"></a><span data-ttu-id="9d8f3-426">Microsoft.PerceptionSimulation.ISimulatedHead</span><span class="sxs-lookup"><span data-stu-id="9d8f3-426">Microsoft.PerceptionSimulation.ISimulatedHead</span></span>

<span data-ttu-id="9d8f3-427">Interface décrivant la tête de l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-427">Interface describing the head of the simulated human.</span></span>

```
public interface ISimulatedHead
{
    Vector3 WorldPosition { get; }
    Rotation3 Rotation { get; set; }
    float Diameter { get; set; }
    void Rotate(Rotation3 rotation);
}
```

<span data-ttu-id="9d8f3-428">**Microsoft.PerceptionSimulation.ISimulatedHead.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-428">**Microsoft.PerceptionSimulation.ISimulatedHead.WorldPosition**</span></span>

<span data-ttu-id="9d8f3-429">Récupérer la position du nœud en relation avec le monde entier, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-429">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="9d8f3-430">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotation**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-430">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotation**</span></span>

<span data-ttu-id="9d8f3-431">Récupérer la rotation de la tête.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-431">Retrieve the rotation of the simulated head.</span></span> <span data-ttu-id="9d8f3-432">Radians rotation horaire lors de la recherche sur l’axe positif.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-432">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="9d8f3-433">**Microsoft.PerceptionSimulation.ISimulatedHead.Diameter**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-433">**Microsoft.PerceptionSimulation.ISimulatedHead.Diameter**</span></span>

<span data-ttu-id="9d8f3-434">Récupérer le diamètre de la tête simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-434">Retrieve the simulated head's diameter.</span></span> <span data-ttu-id="9d8f3-435">Cette valeur est utilisée pour déterminer le centre de la tête (point de rotation).</span><span class="sxs-lookup"><span data-stu-id="9d8f3-435">This value is used to determine the head's center (point of rotation).</span></span>

<span data-ttu-id="9d8f3-436">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-436">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span></span>

<span data-ttu-id="9d8f3-437">Faire pivoter la tête par rapport à sa rotation actuelle.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-437">Rotate the simulated head relative to its current rotation.</span></span> <span data-ttu-id="9d8f3-438">Radians rotation horaire lors de la recherche sur l’axe positif.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-438">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="9d8f3-439">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-439">Parameters</span></span>
* <span data-ttu-id="9d8f3-440">rotation - la quantité pour faire pivoter.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-440">rotation - The amount to rotate.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhead2"></a><span data-ttu-id="9d8f3-441">Microsoft.PerceptionSimulation.ISimulatedHead2</span><span class="sxs-lookup"><span data-stu-id="9d8f3-441">Microsoft.PerceptionSimulation.ISimulatedHead2</span></span>

<span data-ttu-id="9d8f3-442">Propriétés supplémentaires sont disponibles en effectuant un cast d’un ISimulatedHead à ISimulatedHead2</span><span class="sxs-lookup"><span data-stu-id="9d8f3-442">Additional properties are available by casting an ISimulatedHead to ISimulatedHead2</span></span>

```
public interface ISimulatedHead2
{
    /* New members in addition to those available on ISimulatedHead */
    ISimulatedEyes Eyes { get; }
}
```

<span data-ttu-id="9d8f3-443">**Microsoft.PerceptionSimulation.ISimulatedHead2.Eyes**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-443">**Microsoft.PerceptionSimulation.ISimulatedHead2.Eyes**</span></span>

<span data-ttu-id="9d8f3-444">Récupérer les yeux de l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-444">Retrieve the eyes of the simulated human.</span></span>

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller"></a><span data-ttu-id="9d8f3-445">Microsoft.PerceptionSimulation.ISimulatedSixDofController</span><span class="sxs-lookup"><span data-stu-id="9d8f3-445">Microsoft.PerceptionSimulation.ISimulatedSixDofController</span></span>

<span data-ttu-id="9d8f3-446">Interface décrivant un contrôleur de 6-DDL associé à l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-446">Interface describing a 6-DOF controller associated with the simulated human.</span></span>

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

<span data-ttu-id="9d8f3-447">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-447">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.WorldPosition**</span></span>

<span data-ttu-id="9d8f3-448">Récupérer la position du nœud en relation avec le monde entier, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-448">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="9d8f3-449">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Status**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-449">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Status**</span></span>

<span data-ttu-id="9d8f3-450">Récupérer ou définir l’état actuel du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-450">Retrieve or set the current state of the controller.</span></span>  <span data-ttu-id="9d8f3-451">L’état du contrôleur doit être définie sur une valeur autre que hors tension avant tout appel à déplacer, faire pivoter ou appuyez sur boutons réussira.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-451">The controller status must be set to a value other than Off before any calls to move, rotate or press buttons will succeed.</span></span>

<span data-ttu-id="9d8f3-452">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Position**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-452">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Position**</span></span>

<span data-ttu-id="9d8f3-453">Récupérer ou définir la position du contrôleur simulé par rapport à l’être humain, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-453">Retrieve or set the position of the simulated controller relative to the human, in meters.</span></span>

<span data-ttu-id="9d8f3-454">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Orientation**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-454">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Orientation**</span></span>

<span data-ttu-id="9d8f3-455">Récupérer ou définir l’orientation du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-455">Retrieve or set the orientation of the simulated controller.</span></span>

<span data-ttu-id="9d8f3-456">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Move(Microsoft.PerceptionSimulation.Vector3)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-456">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="9d8f3-457">Déplacer la position du contrôleur simulé par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-457">Move the position of the simulated controller relative to its current position, in meters.</span></span>

<span data-ttu-id="9d8f3-458">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-458">Parameters</span></span>
* <span data-ttu-id="9d8f3-459">traduction - quantité de laquelle translater le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-459">translation - The amount to translate the simulated controller.</span></span>

<span data-ttu-id="9d8f3-460">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.PressButton(SimulatedSixDofControllerButton)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-460">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.PressButton(SimulatedSixDofControllerButton)**</span></span>

<span data-ttu-id="9d8f3-461">Appuyez sur un bouton sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-461">Press a button on the simulated controller.</span></span>  <span data-ttu-id="9d8f3-462">Il est détecté par le système uniquement si le contrôleur est activé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-462">It will only be detected by the system if the controller is enabled.</span></span>

<span data-ttu-id="9d8f3-463">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-463">Parameters</span></span>
* <span data-ttu-id="9d8f3-464">bouton - appuyez sur le bouton.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-464">button - The button to press.</span></span>

<span data-ttu-id="9d8f3-465">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.ReleaseButton(SimulatedSixDofControllerButton)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-465">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.ReleaseButton(SimulatedSixDofControllerButton)**</span></span>

<span data-ttu-id="9d8f3-466">Relâchez un bouton sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-466">Release a button on the simulated controller.</span></span>  <span data-ttu-id="9d8f3-467">Il est détecté par le système uniquement si le contrôleur est activé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-467">It will only be detected by the system if the controller is enabled.</span></span>

<span data-ttu-id="9d8f3-468">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-468">Parameters</span></span>
* <span data-ttu-id="9d8f3-469">bouton - le bouton de mise en production.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-469">button - The button to release.</span></span>

<span data-ttu-id="9d8f3-470">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.GetTouchpadPosition(out float, out float)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-470">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.GetTouchpadPosition(out float, out float)**</span></span>

<span data-ttu-id="9d8f3-471">Obtient la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-471">Get the position of a simulated finger on the simulated controller's touchpad.</span></span>

<span data-ttu-id="9d8f3-472">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-472">Parameters</span></span>
* <span data-ttu-id="9d8f3-473">x - la position horizontale du doigt.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-473">x - The horizontal position of the finger.</span></span>
* <span data-ttu-id="9d8f3-474">y - la position verticale du doigt.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-474">y - The vertical position of the finger.</span></span>

<span data-ttu-id="9d8f3-475">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.SetTouchpadPosition(float, float)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-475">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.SetTouchpadPosition(float, float)**</span></span>

<span data-ttu-id="9d8f3-476">Définir la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-476">Set the position of a simulated finger on the simulated controller's touchpad.</span></span>

<span data-ttu-id="9d8f3-477">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-477">Parameters</span></span>
* <span data-ttu-id="9d8f3-478">x - la position horizontale du doigt.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-478">x - The horizontal position of the finger.</span></span>
* <span data-ttu-id="9d8f3-479">y - la position verticale du doigt.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-479">y - The vertical position of the finger.</span></span>

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller2"></a><span data-ttu-id="9d8f3-480">Microsoft.PerceptionSimulation.ISimulatedSixDofController2</span><span class="sxs-lookup"><span data-stu-id="9d8f3-480">Microsoft.PerceptionSimulation.ISimulatedSixDofController2</span></span>

<span data-ttu-id="9d8f3-481">Méthodes et propriétés supplémentaires sont disponibles en effectuant un cast d’un ISimulatedSixDofController à ISimulatedSixDofController2</span><span class="sxs-lookup"><span data-stu-id="9d8f3-481">Additional properties and methods are available by casting an ISimulatedSixDofController to ISimulatedSixDofController2</span></span>

```
public interface ISimulatedSixDofController2
{
    /* New members in addition to those available on ISimulatedSixDofController */
    void GetThumbstickPosition(out float x, out float y);
    void SetThumbstickPosition(float x, float y);
    float BatteryLevel { get; set; }
}
```

<span data-ttu-id="9d8f3-482">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.GetThumbstickPosition(out float, out float)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-482">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.GetThumbstickPosition(out float, out float)**</span></span>

<span data-ttu-id="9d8f3-483">Obtient la position du stick analogique simulé sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-483">Get the position of the simulated thumbstick on the simulated controller.</span></span>

<span data-ttu-id="9d8f3-484">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-484">Parameters</span></span>
* <span data-ttu-id="9d8f3-485">x - la position horizontale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-485">x - The horizontal position of the thumbstick.</span></span>
* <span data-ttu-id="9d8f3-486">y - la position verticale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-486">y - The vertical position of the thumbstick.</span></span>

<span data-ttu-id="9d8f3-487">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.SetThumbstickPosition(float, float)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-487">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.SetThumbstickPosition(float, float)**</span></span>

<span data-ttu-id="9d8f3-488">Positionnez le stick analogique simulé sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-488">Set the position of the simulated thumbstick on the simulated controller.</span></span>

<span data-ttu-id="9d8f3-489">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-489">Parameters</span></span>
* <span data-ttu-id="9d8f3-490">x - la position horizontale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-490">x - The horizontal position of the thumbstick.</span></span>
* <span data-ttu-id="9d8f3-491">y - la position verticale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-491">y - The vertical position of the thumbstick.</span></span>

<span data-ttu-id="9d8f3-492">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.BatteryLevel**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-492">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.BatteryLevel**</span></span>

<span data-ttu-id="9d8f3-493">Récupérer ou définir le niveau de la batterie du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-493">Retrieve or set the battery level of the simulated controller.</span></span>  <span data-ttu-id="9d8f3-494">La valeur doit être supérieure à 0,0 et inférieure ou égale à 100,0.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-494">The value must be greater than 0.0 and less than or equal to 100.0.</span></span>


### <a name="microsoftperceptionsimulationisimulatedeyes"></a><span data-ttu-id="9d8f3-495">Microsoft.PerceptionSimulation.ISimulatedEyes</span><span class="sxs-lookup"><span data-stu-id="9d8f3-495">Microsoft.PerceptionSimulation.ISimulatedEyes</span></span>

<span data-ttu-id="9d8f3-496">Interface décrivant les yeux de l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-496">Interface describing the eyes of the simulated human.</span></span>

```
public interface ISimulatedEyes
{
    Rotation3 Rotation { get; set; }
    void Rotate(Rotation3 rotation);
    SimulatedEyesCalibrationState CalibrationState { get; set; }
    Vector3 WorldPosition { get; }
}
```

<span data-ttu-id="9d8f3-497">**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotation**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-497">**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotation**</span></span>

<span data-ttu-id="9d8f3-498">Récupérer la rotation des yeux simulés.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-498">Retrieve the rotation of the simulated eyes.</span></span> <span data-ttu-id="9d8f3-499">Radians rotation horaire lors de la recherche sur l’axe positif.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-499">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="9d8f3-500">**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-500">**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span></span>

<span data-ttu-id="9d8f3-501">Faire pivoter les yeux simulés par rapport à sa rotation actuelle.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-501">Rotate the simulated eyes relative to its current rotation.</span></span> <span data-ttu-id="9d8f3-502">Radians rotation horaire lors de la recherche sur l’axe positif.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-502">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="9d8f3-503">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-503">Parameters</span></span>
* <span data-ttu-id="9d8f3-504">rotation - la quantité pour faire pivoter.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-504">rotation - The amount to rotate.</span></span>

<span data-ttu-id="9d8f3-505">**Microsoft.PerceptionSimulation.ISimulatedEyes.CalibrationState**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-505">**Microsoft.PerceptionSimulation.ISimulatedEyes.CalibrationState**</span></span>

<span data-ttu-id="9d8f3-506">Récupère ou définit l’état de l’étalonnage des yeux simulés.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-506">Retrieves or sets the calibration state of the simulated eyes.</span></span>

<span data-ttu-id="9d8f3-507">**Microsoft.PerceptionSimulation.ISimulatedEyes.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-507">**Microsoft.PerceptionSimulation.ISimulatedEyes.WorldPosition**</span></span>

<span data-ttu-id="9d8f3-508">Récupérer la position du nœud en relation avec le monde entier, en mètres.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-508">Retrieve the position of the node with relation to the world, in meters.</span></span>


### <a name="microsoftperceptionsimulationisimulationrecording"></a><span data-ttu-id="9d8f3-509">Microsoft.PerceptionSimulation.ISimulationRecording</span><span class="sxs-lookup"><span data-stu-id="9d8f3-509">Microsoft.PerceptionSimulation.ISimulationRecording</span></span>

<span data-ttu-id="9d8f3-510">Charger de l’interface permettant d’interagir avec un enregistrement unique pour la lecture.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-510">Interface for interacting with a single recording loaded for playback.</span></span>

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

<span data-ttu-id="9d8f3-511">**Microsoft.PerceptionSimulation.ISimulationRecording.DataTypes**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-511">**Microsoft.PerceptionSimulation.ISimulationRecording.DataTypes**</span></span>

<span data-ttu-id="9d8f3-512">Récupère la liste des types de données dans l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-512">Retrieves the list of data types in the recording.</span></span>

<span data-ttu-id="9d8f3-513">**Microsoft.PerceptionSimulation.ISimulationRecording.State**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-513">**Microsoft.PerceptionSimulation.ISimulationRecording.State**</span></span>

<span data-ttu-id="9d8f3-514">Récupère l’état actuel de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-514">Retrieves the current state of the recording.</span></span>

<span data-ttu-id="9d8f3-515">**Microsoft.PerceptionSimulation.ISimulationRecording.Play**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-515">**Microsoft.PerceptionSimulation.ISimulationRecording.Play**</span></span>

<span data-ttu-id="9d8f3-516">Démarrer la lecture.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-516">Start the playback.</span></span> <span data-ttu-id="9d8f3-517">Si l’enregistrement est suspendue, la lecture reprend à partir de l’emplacement en pause ; Si arrêté, la lecture démarre au début.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-517">If the recording is paused, playback will resume from the paused location; if stopped, playback will start at the beginning.</span></span> <span data-ttu-id="9d8f3-518">Si vous déjà des données, cet appel est ignoré.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-518">If already playing, this call is ignored.</span></span>

<span data-ttu-id="9d8f3-519">**Microsoft.PerceptionSimulation.ISimulationRecording.Pause**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-519">**Microsoft.PerceptionSimulation.ISimulationRecording.Pause**</span></span>

<span data-ttu-id="9d8f3-520">Suspend la lecture de son emplacement actuel.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-520">Pauses the playback at its current location.</span></span> <span data-ttu-id="9d8f3-521">Si l’enregistrement est arrêté, l’appel est ignoré.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-521">If the recording is stopped, the call is ignored.</span></span>

<span data-ttu-id="9d8f3-522">**Microsoft.PerceptionSimulation.ISimulationRecording.Seek(System.UInt64)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-522">**Microsoft.PerceptionSimulation.ISimulationRecording.Seek(System.UInt64)**</span></span>

<span data-ttu-id="9d8f3-523">Cherche de l’enregistrement à l’heure spécifiée (100 nanosecondes par intervalles d’à partir du début) et s’interrompt à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-523">Seeks the recording to the specified time (in 100 nanoseconds intervals from the beginning) and pauses at that location.</span></span> <span data-ttu-id="9d8f3-524">Si l’heure est après la fin de l’enregistrement, il est suspendu au niveau de la dernière image.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-524">If the time is beyond the end of the recording, it is paused at the last frame.</span></span>

<span data-ttu-id="9d8f3-525">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-525">Parameters</span></span>
* <span data-ttu-id="9d8f3-526">graduations - l’heure à laquelle effectuer une recherche.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-526">ticks - The time to which to seek.</span></span>

<span data-ttu-id="9d8f3-527">**Microsoft.PerceptionSimulation.ISimulationRecording.Stop**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-527">**Microsoft.PerceptionSimulation.ISimulationRecording.Stop**</span></span>

<span data-ttu-id="9d8f3-528">Arrête la lecture et réinitialise la position au début.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-528">Stops the playback and resets the position to the beginning.</span></span>

### <a name="microsoftperceptionsimulationisimulationrecordingcallback"></a><span data-ttu-id="9d8f3-529">Microsoft.PerceptionSimulation.ISimulationRecordingCallback</span><span class="sxs-lookup"><span data-stu-id="9d8f3-529">Microsoft.PerceptionSimulation.ISimulationRecordingCallback</span></span>

<span data-ttu-id="9d8f3-530">Interface pour la réception des modifications d’état pendant la lecture.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-530">Interface for receiving state changes during playback.</span></span>

```
public interface ISimulationRecordingCallback
{
    void PlaybackStateChanged(PlaybackState newState);
};
```

<span data-ttu-id="9d8f3-531">**Microsoft.PerceptionSimulation.ISimulationRecordingCallback.PlaybackStateChanged(Microsoft.PerceptionSimulation.PlaybackState)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-531">**Microsoft.PerceptionSimulation.ISimulationRecordingCallback.PlaybackStateChanged(Microsoft.PerceptionSimulation.PlaybackState)**</span></span>

<span data-ttu-id="9d8f3-532">Appelée lorsque l’état de la lecture d’un ISimulationRecording a changé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-532">Called when an ISimulationRecording's playback state has changed.</span></span>

<span data-ttu-id="9d8f3-533">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-533">Parameters</span></span>
* <span data-ttu-id="9d8f3-534">newState - le nouvel état de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-534">newState - The new state of the recording.</span></span>

### <a name="microsoftperceptionsimulationperceptionsimulationmanager"></a><span data-ttu-id="9d8f3-535">Microsoft.PerceptionSimulation.PerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="9d8f3-535">Microsoft.PerceptionSimulation.PerceptionSimulationManager</span></span>

<span data-ttu-id="9d8f3-536">Objet racine pour la création d’objets de Simulation de Perception.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-536">Root object for creating Perception Simulation objects.</span></span>

```
public static class PerceptionSimulationManager
{
    public static IPerceptionSimulationManager CreatePerceptionSimulationManager(ISimulationStreamSink sink);
    public static ISimulationStreamSink CreatePerceptionSimulationRecording(string path);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory, ISimulationRecordingCallback callback);
```

<span data-ttu-id="9d8f3-537">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationManager(Microsoft.PerceptionSimulation.ISimulationStreamSink)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-537">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationManager(Microsoft.PerceptionSimulation.ISimulationStreamSink)**</span></span>

<span data-ttu-id="9d8f3-538">Créer pour l’objet pour générer des paquets simulés et leur remise sur le récepteur fourni.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-538">Create on object for generating simulated packets and delivering them to the provided sink.</span></span>

<span data-ttu-id="9d8f3-539">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-539">Parameters</span></span>
* <span data-ttu-id="9d8f3-540">récepteur - récepteur qui recevra les paquets générés.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-540">sink - The sink that will receive all generated packets.</span></span>

<span data-ttu-id="9d8f3-541">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d8f3-541">Return value</span></span>

<span data-ttu-id="9d8f3-542">Le gestionnaire créé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-542">The created Manager.</span></span>

<span data-ttu-id="9d8f3-543">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationRecording(System.String)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-543">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationRecording(System.String)**</span></span>

<span data-ttu-id="9d8f3-544">Créer un récepteur qui stocke les paquets reçus tout dans un fichier sur le chemin d’accès spécifié.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-544">Create a sink which stores all received packets in a file at the specified path.</span></span>

<span data-ttu-id="9d8f3-545">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-545">Parameters</span></span>
* <span data-ttu-id="9d8f3-546">chemin d’accès - le chemin d’accès du fichier à créer.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-546">path - The path of the file to create.</span></span>

<span data-ttu-id="9d8f3-547">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d8f3-547">Return value</span></span>

<span data-ttu-id="9d8f3-548">Le récepteur créé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-548">The created sink.</span></span>

<span data-ttu-id="9d8f3-549">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-549">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory)**</span></span>

<span data-ttu-id="9d8f3-550">Charger un enregistrement à partir du fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-550">Load a recording from the specified file.</span></span>

<span data-ttu-id="9d8f3-551">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-551">Parameters</span></span>
* <span data-ttu-id="9d8f3-552">chemin d’accès - le chemin d’accès du fichier à charger.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-552">path - The path of the file to load.</span></span>
* <span data-ttu-id="9d8f3-553">Factory - il s’agit d’une fabrique utilisée par l’enregistrement pour la création d’un ISimulationStreamSink si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-553">factory - A factory used by the recording for creating an ISimulationStreamSink when required.</span></span>

<span data-ttu-id="9d8f3-554">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d8f3-554">Return value</span></span>

<span data-ttu-id="9d8f3-555">L’enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-555">The loaded recording.</span></span>

<span data-ttu-id="9d8f3-556">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording (System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory, Microsoft.PerceptionSimulation.ISimulationRecordingCallback)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-556">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory,Microsoft.PerceptionSimulation.ISimulationRecordingCallback)**</span></span>

<span data-ttu-id="9d8f3-557">Charger un enregistrement à partir du fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-557">Load a recording from the specified file.</span></span>

<span data-ttu-id="9d8f3-558">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-558">Parameters</span></span>
* <span data-ttu-id="9d8f3-559">chemin d’accès - le chemin d’accès du fichier à charger.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-559">path - The path of the file to load.</span></span>
* <span data-ttu-id="9d8f3-560">Factory - il s’agit d’une fabrique utilisée par l’enregistrement pour la création d’un ISimulationStreamSink si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-560">factory - A factory used by the recording for creating an ISimulationStreamSink when required.</span></span>
* <span data-ttu-id="9d8f3-561">rappel - un rappel qui reçoit des mises à jour déclassement d’état de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-561">callback - A callback which receives updates regrading the recording's status.</span></span>

<span data-ttu-id="9d8f3-562">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d8f3-562">Return value</span></span>

<span data-ttu-id="9d8f3-563">L’enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-563">The loaded recording.</span></span>

### <a name="microsoftperceptionsimulationstreamdatatypes"></a><span data-ttu-id="9d8f3-564">Microsoft.PerceptionSimulation.StreamDataTypes</span><span class="sxs-lookup"><span data-stu-id="9d8f3-564">Microsoft.PerceptionSimulation.StreamDataTypes</span></span>

<span data-ttu-id="9d8f3-565">Décrit les différents types de données de flux.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-565">Describes the different types of stream data.</span></span>

```
public enum StreamDataTypes
{
    None = 0x00,
    Head = 0x01,
    Hands = 0x02,
    SpatialMapping = 0x08,
    Calibration = 0x10,
    Environment = 0x20,
    All = None | Head | Hands | SpatialMapping | Calibration | Environment
}
```

<span data-ttu-id="9d8f3-566">**Microsoft.PerceptionSimulation.StreamDataTypes.None**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-566">**Microsoft.PerceptionSimulation.StreamDataTypes.None**</span></span>

<span data-ttu-id="9d8f3-567">Valeur de sentinelle permettant de n’indiquer aucun type de données de flux de données.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-567">A sentinel value used to indicate no stream data types.</span></span>

<span data-ttu-id="9d8f3-568">**Microsoft.PerceptionSimulation.StreamDataTypes.Head**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-568">**Microsoft.PerceptionSimulation.StreamDataTypes.Head**</span></span>

<span data-ttu-id="9d8f3-569">Stream des données relatives à la position et l’orientation de la tête.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-569">Stream of data regarding the position and orientation of the head.</span></span>

<span data-ttu-id="9d8f3-570">**Microsoft.PerceptionSimulation.StreamDataTypes.Hands**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-570">**Microsoft.PerceptionSimulation.StreamDataTypes.Hands**</span></span>

<span data-ttu-id="9d8f3-571">Stream de données sur la position et les mouvements de mains.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-571">Stream of data regarding the position and gestures of hands.</span></span>

<span data-ttu-id="9d8f3-572">**Microsoft.PerceptionSimulation.StreamDataTypes.SpatialMapping**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-572">**Microsoft.PerceptionSimulation.StreamDataTypes.SpatialMapping**</span></span>

<span data-ttu-id="9d8f3-573">Stream de données concernant le mappage spatial de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-573">Stream of data regarding spatial mapping of the environment.</span></span>

<span data-ttu-id="9d8f3-574">**Microsoft.PerceptionSimulation.StreamDataTypes.Calibration**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-574">**Microsoft.PerceptionSimulation.StreamDataTypes.Calibration**</span></span>

<span data-ttu-id="9d8f3-575">Stream de données concernant l’étalonnage de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-575">Stream of data regarding calibration of the device.</span></span> <span data-ttu-id="9d8f3-576">Paquets d’étalonnage sont uniquement acceptées par un système en Mode distant.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-576">Calibration packets are only accepted by a system in Remote Mode.</span></span>

<span data-ttu-id="9d8f3-577">**Microsoft.PerceptionSimulation.StreamDataTypes.Environment**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-577">**Microsoft.PerceptionSimulation.StreamDataTypes.Environment**</span></span>

<span data-ttu-id="9d8f3-578">Stream de données concernant l’environnement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-578">Stream of data regarding the environment of the device.</span></span>

<span data-ttu-id="9d8f3-579">**Microsoft.PerceptionSimulation.StreamDataTypes.All**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-579">**Microsoft.PerceptionSimulation.StreamDataTypes.All**</span></span>

<span data-ttu-id="9d8f3-580">Valeur de sentinelle utilisée pour indiquer tous les types de données enregistrées.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-580">A sentinel value used to indicate all recorded data types.</span></span>

### <a name="microsoftperceptionsimulationisimulationstreamsink"></a><span data-ttu-id="9d8f3-581">Microsoft.PerceptionSimulation.ISimulationStreamSink</span><span class="sxs-lookup"><span data-stu-id="9d8f3-581">Microsoft.PerceptionSimulation.ISimulationStreamSink</span></span>

<span data-ttu-id="9d8f3-582">Objet qui reçoit des paquets de données à partir d’un flux de données de simulation.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-582">An object that receives data packets from a simulation stream.</span></span>

```
public interface ISimulationStreamSink
{
    void OnPacketReceived(uint length, byte[] packet);
}
```

<span data-ttu-id="9d8f3-583">**Microsoft.PerceptionSimulation.ISimulationStreamSink.OnPacketReceived(uint length, byte[] packet)**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-583">**Microsoft.PerceptionSimulation.ISimulationStreamSink.OnPacketReceived(uint length, byte[] packet)**</span></span>

<span data-ttu-id="9d8f3-584">Reçoit un paquet unique, qui est en interne typés et avec contrôle de version.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-584">Receives a single packet, which is internally typed and versioned.</span></span>

<span data-ttu-id="9d8f3-585">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9d8f3-585">Parameters</span></span>
* <span data-ttu-id="9d8f3-586">Length - la longueur du paquet.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-586">length - The length of the packet.</span></span>
* <span data-ttu-id="9d8f3-587">paquet - les données du paquet.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-587">packet - The data of the packet.</span></span>

### <a name="microsoftperceptionsimulationisimulationstreamsinkfactory"></a><span data-ttu-id="9d8f3-588">Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory</span><span class="sxs-lookup"><span data-stu-id="9d8f3-588">Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory</span></span>

<span data-ttu-id="9d8f3-589">Objet qui crée ISimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-589">An object that creates ISimulationStreamSink.</span></span>

```
public interface ISimulationStreamSinkFactory
{
    ISimulationStreamSink CreateSimulationStreamSink();
}
```

<span data-ttu-id="9d8f3-590">**Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory.CreateSimulationStreamSink()**</span><span class="sxs-lookup"><span data-stu-id="9d8f3-590">**Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory.CreateSimulationStreamSink()**</span></span>

<span data-ttu-id="9d8f3-591">Crée une instance unique de ISimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-591">Creates a single instance of ISimulationStreamSink.</span></span>

<span data-ttu-id="9d8f3-592">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="9d8f3-592">Return value</span></span>

<span data-ttu-id="9d8f3-593">Le récepteur créé.</span><span class="sxs-lookup"><span data-stu-id="9d8f3-593">The created sink.</span></span>
