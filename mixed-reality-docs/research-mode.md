---
title: Mode de recherche HoloLens
description: En utilisant le mode de recherche sur HoloLens, une application peut accéder aux flux de capteur de périphérique clé (profondeur, suivi de l’environnement et réflectivité de l’IR).
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
keywords: mode de recherche, CV, RS4, vision par ordinateur, recherche, HoloLens, HoloLens 2
ms.openlocfilehash: 62b82e3a36452d4b104bf04999e556ec19d2a5e3
ms.sourcegitcommit: 45da0a056fa42088ff81ccdd11232830fbe8430f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84720395"
---
# <a name="hololens-research-mode"></a><span data-ttu-id="f4b3a-104">Mode de recherche HoloLens</span><span class="sxs-lookup"><span data-stu-id="f4b3a-104">HoloLens Research mode</span></span>

## <a name="overview"></a><span data-ttu-id="f4b3a-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="f4b3a-105">Overview</span></span>

<span data-ttu-id="f4b3a-106">Le mode de recherche a été introduit dans le HoloLens de 1re génération pour permettre l’accès aux capteurs de clé sur l’appareil, en particulier pour les applications de recherche qui ne sont pas destinées au déploiement.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-106">Research mode was introduced in the 1st Generation HoloLens to give access to key sensors on the device, specifically for research applications that are not intended for deployment.</span></span> <span data-ttu-id="f4b3a-107">Vous pouvez maintenant collecter des données à partir des entrées suivantes :</span><span class="sxs-lookup"><span data-stu-id="f4b3a-107">You can now gather data from the following inputs:</span></span>

* <span data-ttu-id="f4b3a-108">**Caméras de suivi de l’environnement clair visibles** -utilisées par le système pour le suivi des têtes et la génération de cartes.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-108">**Visible Light Environment Tracking Cameras** - Used by the system for head tracking and map building.</span></span>
* <span data-ttu-id="f4b3a-109">**Appareil photo de profondeur** : fonctionne en deux modes :</span><span class="sxs-lookup"><span data-stu-id="f4b3a-109">**Depth Camera** – Operates in two modes:</span></span>  
    + <span data-ttu-id="f4b3a-110">Détection quasi-profondeur (30 i/s) à court terme et à fréquence élevée utilisée pour le suivi de la [main](interaction-fundamentals.md)</span><span class="sxs-lookup"><span data-stu-id="f4b3a-110">Short-throw, high-frequency (30 FPS) near-depth sensing used for [Hand Tracking](interaction-fundamentals.md)</span></span>
    + <span data-ttu-id="f4b3a-111">Détection de longueurs longues, à faible fréquence (1-5 FPS), utilisée par le [mappage spatial](spatial-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="f4b3a-111">Long-throw, low-frequency (1-5 FPS) far-depth sensing used by [Spatial Mapping](spatial-mapping.md)</span></span>
* <span data-ttu-id="f4b3a-112">**Deux versions du flux de réflectivité IR** -utilisées par le HoloLens pour calculer la profondeur.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-112">**Two versions of the IR-reflectivity stream** - Used by the HoloLens to compute depth.</span></span> <span data-ttu-id="f4b3a-113">Ces images sont éclairées par infrarouge et ne sont pas affectées par la lumière visible ambiante.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-113">These images are illuminated by infrared and unaffected by ambient visible light.</span></span>

<span data-ttu-id="f4b3a-114">Si vous utilisez un HoloLens 2, vous pouvez également accéder aux entrées suivantes :</span><span class="sxs-lookup"><span data-stu-id="f4b3a-114">If you're using a HoloLens 2 you will also be able to access the following inputs:</span></span>

* <span data-ttu-id="f4b3a-115">**Accéléromètre** : utilisé par le système pour déterminer l’accélération linéaire le long des axes X, Y et Z et la gravité.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-115">**Accelerometer** – Used by the system to determine linear acceleration along the X, Y and Z axes and gravity.</span></span>
* <span data-ttu-id="f4b3a-116">**Gyroscope** : utilisé par le système pour déterminer les rotations.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-116">**Gyro** – Used by the system to determine rotations.</span></span>
* <span data-ttu-id="f4b3a-117">**Magnétomètre** : utilisé par le système pour estimer l’orientation absolue.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-117">**Magnetometer** – Used by the system to estimate absolute orientation.</span></span>

<span data-ttu-id="f4b3a-118">![Capture d’écran de l’application en mode recherche](images/sensor-stream-viewer.jpg)</span><span class="sxs-lookup"><span data-stu-id="f4b3a-118">![Research Mode app screenshot](images/sensor-stream-viewer.jpg)</span></span><br>
<span data-ttu-id="f4b3a-119">*Capture de réalité mixte d’une application de test qui affiche les huit flux de capteurs disponibles en mode de recherche*</span><span class="sxs-lookup"><span data-stu-id="f4b3a-119">*A mixed reality capture of a test application that displays the eight sensor streams available in Research mode*</span></span>

> [!NOTE]
> <span data-ttu-id="f4b3a-120">La fonctionnalité du mode de recherche a été ajoutée dans le cadre de la [mise à jour 2018 de Windows 10 avril](release-notes-april-2018.md) pour HoloLens et n’est pas disponible dans les versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-120">The Research Mode feature was added as part of the [Windows 10 April 2018 Update](release-notes-april-2018.md) for HoloLens, and is not available on earlier releases.</span></span>

## <a name="usage"></a><span data-ttu-id="f4b3a-121">Usage</span><span class="sxs-lookup"><span data-stu-id="f4b3a-121">Usage</span></span>

<span data-ttu-id="f4b3a-122">Le mode de recherche est conçu pour les chercheurs universitaires et industriels qui explorent de nouvelles idées dans les domaines de la Vision par ordinateur et de la robotique.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-122">Research mode is designed for academic and industrial researchers exploring new ideas in the fields of Computer Vision and Robotics.</span></span>  <span data-ttu-id="f4b3a-123">Elle n’est pas destinée aux applications déployées dans des environnements d’entreprise ou disponibles via le Microsoft Store ou d’autres canaux de distribution.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-123">It's not intended for applications deployed in enterprise environments or available through the Microsoft Store or other distribution channels.</span></span>

<span data-ttu-id="f4b3a-124">En outre, Microsoft ne garantit pas que le mode de recherche ou les fonctionnalités équivalentes seront pris en charge dans les futures mises à jour du matériel ou du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-124">Additionally, Microsoft doesn't provide assurances that research mode or equivalent functionality is going to be supported in future hardware or OS updates.</span></span> <span data-ttu-id="f4b3a-125">Toutefois, cela ne vous empêche pas de l’utiliser pour développer et tester de nouvelles idées !</span><span class="sxs-lookup"><span data-stu-id="f4b3a-125">However, this shouldn't stop you from using it to develop and test new ideas!</span></span>

## <a name="security-and-performance"></a><span data-ttu-id="f4b3a-126">Sécurité et performances</span><span class="sxs-lookup"><span data-stu-id="f4b3a-126">Security and performance</span></span>

<span data-ttu-id="f4b3a-127">N’oubliez pas que l’activation du mode de recherche utilise davantage de batterie que l’utilisation de la mise à l’aide du système HoloLens 2 dans des conditions normales.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-127">Be aware that enabling research mode uses more battery power than using the HoloLens 2 under normal conditions.</span></span> <span data-ttu-id="f4b3a-128">Cela est vrai même si l’application qui utilise les fonctionnalités du mode de recherche n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-128">This is true even if the application using the research mode features is not running.</span></span>  <span data-ttu-id="f4b3a-129">L’activation de ce mode peut également réduire la sécurité globale de votre appareil, car les applications peuvent avoir recours à des données de capteur.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-129">Enabling this mode can also lower the overall security of your device because applications may misuse sensor data.</span></span>  <span data-ttu-id="f4b3a-130">Vous trouverez plus d’informations sur la sécurité des appareils dans le [Forum aux questions sur la sécurité HoloLens](https://docs.microsoft.com/hololens/hololens-faq-security).</span><span class="sxs-lookup"><span data-stu-id="f4b3a-130">You can find more information on device security in the [HoloLens security FAQ](https://docs.microsoft.com/hololens/hololens-faq-security).</span></span>  


## <a name="device-support"></a><span data-ttu-id="f4b3a-131">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="f4b3a-131">Device support</span></span>

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    <!-- <col width="33%" /> -->
    </colgroup>
    <tr>
        <td><span data-ttu-id="f4b3a-132"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="f4b3a-132"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="f4b3a-133"><a href="hololens-hardware-details.md"><strong>1re génération de HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="f4b3a-133"><a href="hololens-hardware-details.md"><strong>HoloLens 1st Gen</strong></a></span></span></td>
        <!-- <td><a href="hololens2-hardware.md"><strong>HoloLens 2</strong></a></td> -->
    </tr>
     <tr>
        <td><span data-ttu-id="f4b3a-134">Caméras de suivi des têtes</span><span class="sxs-lookup"><span data-stu-id="f4b3a-134">Head Tracking Cameras</span></span></td>
        <td><span data-ttu-id="f4b3a-135">✔️</span><span class="sxs-lookup"><span data-stu-id="f4b3a-135">✔️</span></span></td>
        <!-- <td>❌</td> -->
    </tr>
    <tr>
        <td><span data-ttu-id="f4b3a-136">Caméra de profondeur & IR</span><span class="sxs-lookup"><span data-stu-id="f4b3a-136">Depth & IR Camera</span></span></td>
        <td><span data-ttu-id="f4b3a-137">✔️</span><span class="sxs-lookup"><span data-stu-id="f4b3a-137">✔️</span></span></td>
        <!-- <td>❌</td> -->
    </tr>
    <tr>
        <td><span data-ttu-id="f4b3a-138">Accéléromètre</span><span class="sxs-lookup"><span data-stu-id="f4b3a-138">Accelerometer</span></span></td>
        <td>❌</td>
        <!-- <td>❌</td> -->
    </tr>
    <tr>
        <td><span data-ttu-id="f4b3a-139">Gyroscope</span><span class="sxs-lookup"><span data-stu-id="f4b3a-139">Gyroscope</span></span></td>
        <td>❌</td>
        <!-- <td>❌</td> -->
    </tr>
    <tr>
        <td><span data-ttu-id="f4b3a-140">Magnétomètre</span><span class="sxs-lookup"><span data-stu-id="f4b3a-140">Magnetometer</span></span></td>
        <td>❌</td>
        <!-- <td>❌</td> -->
    </tr>
</table>

> [!IMPORTANT]
> <span data-ttu-id="f4b3a-141">La prise en charge du mode de recherche pour HoloLens 2 devrait être disponible en version préliminaire publique en juillet 2020 et inclura toutes les fonctionnalités mentionnées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-141">Research Mode support for HoloLens 2 is expected to be available in public preview in July 2020 and will include all the features listed above.</span></span> <span data-ttu-id="f4b3a-142">Pour plus d’informations, revenez à la.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-142">Please check back for more information.</span></span> 

## <a name="enabling-research-mode"></a><span data-ttu-id="f4b3a-143">Activation du mode de recherche</span><span class="sxs-lookup"><span data-stu-id="f4b3a-143">Enabling Research mode</span></span>

<span data-ttu-id="f4b3a-144">Le mode de recherche est une extension du mode développeur.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-144">Research mode is an extension of Developer Mode.</span></span> <span data-ttu-id="f4b3a-145">Avant de commencer, les fonctionnalités de développement de l’appareil doivent être activées pour accéder aux paramètres du mode de recherche :</span><span class="sxs-lookup"><span data-stu-id="f4b3a-145">Before starting, the developer features of the device need to be enabled to access the research mode settings:</span></span> 

* <span data-ttu-id="f4b3a-146">Ouvrez le **menu démarrer > paramètres** , puis sélectionnez **mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-146">Open **Start Menu > Settings** and select **Updates**.</span></span>
* <span data-ttu-id="f4b3a-147">Sélectionnez **pour les développeurs** et activer le **mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-147">Select **For Developers** and enable **Developer Mode**.</span></span>
* <span data-ttu-id="f4b3a-148">Faites défiler l’appareil et activez le **portail des appareils**.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-148">Scroll down and enable **Device Portal**.</span></span>

<span data-ttu-id="f4b3a-149">Une fois les fonctionnalités du développeur activées, [Connectez-vous au portail](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens) de l’appareil pour activer les fonctionnalités du mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-149">After the developer features  are enabled, [connect to the device portal](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens) to enable the research mode features.</span></span>

<span data-ttu-id="f4b3a-150">Sur *HoloLens 1re génération*:</span><span class="sxs-lookup"><span data-stu-id="f4b3a-150">On *HoloLens 1st Gen*:</span></span>

* <span data-ttu-id="f4b3a-151">Accédez à **système > le mode de recherche** dans le portail de l' **appareil**.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-151">Go to **System > Research mode** in the **Device Portal**.</span></span>
* <span data-ttu-id="f4b3a-152">Sélectionnez **autoriser l’accès au flux de capteur**.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-152">Select **Allow access to sensor stream**.</span></span>
* <span data-ttu-id="f4b3a-153">Redémarrez l’appareil à partir de l’élément de menu **Power** situé en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-153">Restart the device from the **Power** menu item at the top of the page.</span></span>

<span data-ttu-id="f4b3a-154">Une fois que vous avez redémarré l’appareil, les applications chargées via le portail de l' **appareil** peuvent accéder aux flux en mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-154">Once you've restarted the device, the applications loaded through the **Device Portal** can access Research mode streams.</span></span>

<span data-ttu-id="f4b3a-155">![Onglet mode de recherche du portail de l’appareil HoloLens](images/ResearchModeDevPortal.png)</span><span class="sxs-lookup"><span data-stu-id="f4b3a-155">![Research Mode tab of HoloLens Device Portal](images/ResearchModeDevPortal.png)</span></span><br>
<span data-ttu-id="f4b3a-156">*Fenêtre du mode de recherche dans le portail d’appareils HoloLens*</span><span class="sxs-lookup"><span data-stu-id="f4b3a-156">*Research mode window in the HoloLens Device Portal*</span></span>

## <a name="using-sensor-data-in-your-apps"></a><span data-ttu-id="f4b3a-157">Utilisation des données de capteur dans vos applications</span><span class="sxs-lookup"><span data-stu-id="f4b3a-157">Using sensor data in your apps</span></span>

<span data-ttu-id="f4b3a-158">*1re génération de HoloLens*</span><span class="sxs-lookup"><span data-stu-id="f4b3a-158">*HoloLens 1st Gen*</span></span>

<span data-ttu-id="f4b3a-159">Les applications peuvent accéder aux données de flux de capteur de la même façon que les flux de photos et les vidéos de caméra vidéo sont accessibles par le biais de [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197).</span><span class="sxs-lookup"><span data-stu-id="f4b3a-159">Applications can access the sensor stream data in the same way that photo and video camera streams are accessed through [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197).</span></span> 

<span data-ttu-id="f4b3a-160">Toutes les API qui fonctionnent pour le développement HoloLens sont également disponibles en mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-160">All APIs that work for HoloLens development are also available in Research mode.</span></span> <span data-ttu-id="f4b3a-161">En particulier, l’application sait précisément où HoloLens se trouve dans l’espace 6DoF à chaque fois que la capture de l’image du capteur est terminée.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-161">In particular, the application  knows precisely where HoloLens is in 6DoF space at each sensor frame capture time.</span></span>

<span data-ttu-id="f4b3a-162">Vous trouverez des exemples d’applications sur l’accès aux différents flux en mode de recherche, sur l’utilisation des [intrinsèques et des extrinsics](https://docs.microsoft.com/windows/mixed-reality/locatable-camera#locating-the-device-camera-in-the-world), et sur l’enregistrement des flux dans le [HoloLensForCV GitHub référentiel](https://github.com/Microsoft/HoloLensForCV) référentiel.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-162">You can find sample applications on how to access the various Research mode streams, how to use the [intrinsics and extrinsics](https://docs.microsoft.com/windows/mixed-reality/locatable-camera#locating-the-device-camera-in-the-world), and how to record streams in the [HoloLensForCV GitHub repo](https://github.com/Microsoft/HoloLensForCV) repo.</span></span>

 > [!NOTE]
 > <span data-ttu-id="f4b3a-163">À ce stade, l’exemple HoloLensForCV ne fonctionne pas sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-163">At this time, the HoloLensForCV sample doesn't work on HoloLens 2.</span></span>

## <a name="known-issues"></a><span data-ttu-id="f4b3a-164">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="f4b3a-164">Known issues</span></span>

<span data-ttu-id="f4b3a-165">Vous pouvez utiliser le [suivi](https://github.com/Microsoft/HololensForCV/issues) des problèmes dans le référentiel HoloLensForCV pour suivre les problèmes connus.</span><span class="sxs-lookup"><span data-stu-id="f4b3a-165">You can use the [issue tracker](https://github.com/Microsoft/HololensForCV/issues) in the HoloLensForCV repository to follow known issues.</span></span>

## <a name="see-also"></a><span data-ttu-id="f4b3a-166">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f4b3a-166">See also</span></span>

* [<span data-ttu-id="f4b3a-167">Microsoft Media Foundation</span><span class="sxs-lookup"><span data-stu-id="f4b3a-167">Microsoft Media Foundation</span></span>](https://msdn.microsoft.com/library/windows/desktop/ms694197)
* [<span data-ttu-id="f4b3a-168">HoloLensForCV GitHub référentiel</span><span class="sxs-lookup"><span data-stu-id="f4b3a-168">HoloLensForCV GitHub repo</span></span>](https://github.com/Microsoft/HoloLensForCV)
* [<span data-ttu-id="f4b3a-169">Utilisation du portail d’appareil Windows</span><span class="sxs-lookup"><span data-stu-id="f4b3a-169">Using the Windows Device Portal</span></span>](using-the-windows-device-portal.md)
