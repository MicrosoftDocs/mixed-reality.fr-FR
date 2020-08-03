---
title: Mode de recherche HoloLens
description: En utilisant le mode de recherche sur HoloLens, une application peut accéder aux flux de capteur de périphérique clé (profondeur, suivi de l’environnement et réflectivité de l’IR).
author: hferrone
ms.author: v-haferr
ms.date: 07/31/2020
ms.topic: article
keywords: Mode de recherche, CV, RS4, vision par ordinateur, recherche, HoloLens, HoloLens 2
ms.openlocfilehash: dd49186d1218b6a6a6c9a8d5943159daad3bcefb
ms.sourcegitcommit: 36316e2658d3dfa804d798b9f4fb2f9186052144
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2020
ms.locfileid: "87507693"
---
# <a name="hololens-research-mode"></a><span data-ttu-id="7549c-104">Mode de recherche HoloLens</span><span class="sxs-lookup"><span data-stu-id="7549c-104">HoloLens Research Mode</span></span>

<span data-ttu-id="7549c-105">Le mode de recherche a été introduit dans le HoloLens de 1re génération pour permettre l’accès aux capteurs de clé sur l’appareil, en particulier pour les applications de recherche qui ne sont pas destinées au déploiement.</span><span class="sxs-lookup"><span data-stu-id="7549c-105">Research Mode was introduced in the 1st Generation HoloLens to give access to key sensors on the device, specifically for research applications that are not intended for deployment.</span></span>  <span data-ttu-id="7549c-106">Le mode de recherche pour HoloLens 2 conserve les fonctionnalités de HoloLens 1, en ajoutant l’accès aux flux supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="7549c-106">Research Mode for HoloLens 2 retains the capabilities of HoloLens 1, adding access to additional streams:</span></span>

* <span data-ttu-id="7549c-107">**Caméras de suivi de l’environnement clair visibles** -caméras de nuances de gris utilisées par le système pour le suivi des têtes et la génération de cartes.</span><span class="sxs-lookup"><span data-stu-id="7549c-107">**Visible Light Environment Tracking Cameras** - Gray-scale cameras used by the system for head tracking and map building.</span></span>
* <span data-ttu-id="7549c-108">**Appareil photo de profondeur** : fonctionne en deux modes :</span><span class="sxs-lookup"><span data-stu-id="7549c-108">**Depth Camera** – Operates in two modes:</span></span>  
    + <span data-ttu-id="7549c-109">Détection presque-profondeur AHAT, à fréquence élevée (45 FPS) utilisée pour le suivi des handles.</span><span class="sxs-lookup"><span data-stu-id="7549c-109">AHAT, high-frequency (45 FPS) near-depth sensing used for hand tracking.</span></span> <span data-ttu-id="7549c-110">De la même façon que le mode de levée abrégée de la première version, AHAT fournit une Pseudo-profondeur avec un retour à la ligne au-delà de 1 mètre.</span><span class="sxs-lookup"><span data-stu-id="7549c-110">Differently from the 1st version short-throw mode, AHAT gives pseudo-depth with phase wrap beyond 1 meter.</span></span> 
    + <span data-ttu-id="7549c-111">Détection de longueurs longues, à faible fréquence (1-5 FPS), utilisée par le [mappage spatial](spatial-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="7549c-111">Long-throw, low-frequency (1-5 FPS) far-depth sensing used by [Spatial Mapping](spatial-mapping.md)</span></span>

* <span data-ttu-id="7549c-112">**Deux versions du flux de réflectivité IR** -utilisées par le HoloLens pour calculer la profondeur.</span><span class="sxs-lookup"><span data-stu-id="7549c-112">**Two versions of the IR-reflectivity stream** - Used by the HoloLens to compute depth.</span></span> <span data-ttu-id="7549c-113">Ces images sont éclairées par infrarouge et ne sont pas affectées par la lumière visible ambiante.</span><span class="sxs-lookup"><span data-stu-id="7549c-113">These images are illuminated by infrared and unaffected by ambient visible light.</span></span>

<span data-ttu-id="7549c-114">Si vous utilisez un HoloLens 2, vous avez également accès aux entrées supplémentaires ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7549c-114">If you're using a HoloLens 2 you also have access to the additional inputs below:</span></span>

* <span data-ttu-id="7549c-115">**Accéléromètre** : utilisé par le système pour déterminer l’accélération linéaire le long des axes X, Y et Z et la gravité.</span><span class="sxs-lookup"><span data-stu-id="7549c-115">**Accelerometer** – Used by the system to determine linear acceleration along the X, Y and Z axes and gravity.</span></span>
* <span data-ttu-id="7549c-116">**Gyroscope** : utilisé par le système pour déterminer les rotations.</span><span class="sxs-lookup"><span data-stu-id="7549c-116">**Gyro** – Used by the system to determine rotations.</span></span>
* <span data-ttu-id="7549c-117">**Magnétomètre** : utilisé par le système pour estimer l’orientation absolue.</span><span class="sxs-lookup"><span data-stu-id="7549c-117">**Magnetometer** – Used by the system to estimate absolute orientation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7549c-118">Le mode de recherche est actuellement en version préliminaire publique.</span><span class="sxs-lookup"><span data-stu-id="7549c-118">Research Mode is currently in Public Preview.</span></span> <span data-ttu-id="7549c-119">Les exemples, les didacticiels et la documentation complète de l’API HoloLens 2 seront disponibles sur [ECCV 2020](https://eccv2020.eu/
 ) dans le référentiel git en mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="7549c-119">HoloLens 2 samples, tutorials, and full API documentation will be available at [ECCV 2020](https://eccv2020.eu/
 ) in the Research Mode Git repository.</span></span>

<span data-ttu-id="7549c-120">![Capture d’écran de l’application en mode recherche](images/sensor-stream-viewer.jpg)</span><span class="sxs-lookup"><span data-stu-id="7549c-120">![Research Mode app screenshot](images/sensor-stream-viewer.jpg)</span></span><br>
<span data-ttu-id="7549c-121">*Capture de réalité mixte d’une application de test qui affiche les huit flux de capteurs disponibles en mode de recherche*</span><span class="sxs-lookup"><span data-stu-id="7549c-121">*A mixed reality capture of a test application that displays the eight sensor streams available in Research Mode*</span></span>

## <a name="usage"></a><span data-ttu-id="7549c-122">Usage</span><span class="sxs-lookup"><span data-stu-id="7549c-122">Usage</span></span>

<span data-ttu-id="7549c-123">Le mode de recherche est conçu pour les chercheurs universitaires et industriels qui explorent de nouvelles idées dans les domaines de la Vision par ordinateur et de la robotique.</span><span class="sxs-lookup"><span data-stu-id="7549c-123">Research Mode is designed for academic and industrial researchers exploring new ideas in the fields of Computer Vision and Robotics.</span></span>  <span data-ttu-id="7549c-124">Elle n’est pas destinée aux applications déployées dans des environnements d’entreprise ou disponibles via le Microsoft Store ou d’autres canaux de distribution.</span><span class="sxs-lookup"><span data-stu-id="7549c-124">It's not intended for applications deployed in enterprise environments or available through the Microsoft Store or other distribution channels.</span></span>

<span data-ttu-id="7549c-125">En outre, Microsoft ne garantit pas que le mode de recherche ou les fonctionnalités équivalentes seront pris en charge dans les futures mises à jour du matériel ou du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="7549c-125">Additionally, Microsoft doesn't provide assurances that Research Mode or equivalent functionality is going to be supported in future hardware or OS updates.</span></span> <span data-ttu-id="7549c-126">Toutefois, cela ne vous empêche pas de l’utiliser pour développer et tester de nouvelles idées !</span><span class="sxs-lookup"><span data-stu-id="7549c-126">However, this shouldn't stop you from using it to develop and test new ideas!</span></span>

## <a name="security-and-performance"></a><span data-ttu-id="7549c-127">Sécurité et performances</span><span class="sxs-lookup"><span data-stu-id="7549c-127">Security and performance</span></span>

<span data-ttu-id="7549c-128">N’oubliez pas que l’activation du mode de recherche utilise davantage de batterie que l’utilisation de la mise à l’aide du système HoloLens 2 dans des conditions normales.</span><span class="sxs-lookup"><span data-stu-id="7549c-128">Be aware that enabling Research Mode uses more battery power than using the HoloLens 2 under normal conditions.</span></span> <span data-ttu-id="7549c-129">Cela est vrai même si l’application qui utilise les fonctionnalités du mode de recherche n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7549c-129">This is true even if the application using the Research Mode features is not running.</span></span>  <span data-ttu-id="7549c-130">L’activation de ce mode peut également réduire la sécurité globale de votre appareil, car les applications peuvent avoir recours à des données de capteur.</span><span class="sxs-lookup"><span data-stu-id="7549c-130">Enabling this mode can also lower the overall security of your device because applications may misuse sensor data.</span></span>  <span data-ttu-id="7549c-131">Vous trouverez plus d’informations sur la sécurité des appareils dans le [Forum aux questions sur la sécurité HoloLens](https://docs.microsoft.com/hololens/hololens-faq-security).</span><span class="sxs-lookup"><span data-stu-id="7549c-131">You can find more information on device security in the [HoloLens security FAQ](https://docs.microsoft.com/hololens/hololens-faq-security).</span></span>  

## <a name="device-support"></a><span data-ttu-id="7549c-132">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="7549c-132">Device support</span></span>
<table><span data-ttu-id="7549c-133">
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" /> </colgroup>
    </span><span class="sxs-lookup"><span data-stu-id="7549c-133">
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" /> </colgroup>
    </span></span><tr>
        <td><span data-ttu-id="7549c-134"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="7549c-134"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="7549c-135"><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="7549c-135"><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens 1st Gen</strong></a></span></span></td>
        <td><span data-ttu-id="7549c-136"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></a></span><span class="sxs-lookup"><span data-stu-id="7549c-136"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="7549c-137">Caméras de suivi des têtes</span><span class="sxs-lookup"><span data-stu-id="7549c-137">Head Tracking Cameras</span></span></td>
        <td><span data-ttu-id="7549c-138">✔️</span><span class="sxs-lookup"><span data-stu-id="7549c-138">✔️</span></span></td>
        <td><span data-ttu-id="7549c-139">✔️</span><span class="sxs-lookup"><span data-stu-id="7549c-139">✔️</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="7549c-140">Caméra de profondeur & IR</span><span class="sxs-lookup"><span data-stu-id="7549c-140">Depth & IR Camera</span></span></td>
        <td><span data-ttu-id="7549c-141">✔️</span><span class="sxs-lookup"><span data-stu-id="7549c-141">✔️</span></span></td>
        <td><span data-ttu-id="7549c-142">✔️</span><span class="sxs-lookup"><span data-stu-id="7549c-142">✔️</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="7549c-143">Accéléromètre</span><span class="sxs-lookup"><span data-stu-id="7549c-143">Accelerometer</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="7549c-144">✔️</span><span class="sxs-lookup"><span data-stu-id="7549c-144">✔️</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="7549c-145">Gyroscope</span><span class="sxs-lookup"><span data-stu-id="7549c-145">Gyroscope</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="7549c-146">✔️</span><span class="sxs-lookup"><span data-stu-id="7549c-146">✔️</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="7549c-147">Magnétomètre</span><span class="sxs-lookup"><span data-stu-id="7549c-147">Magnetometer</span></span></td>
        <td>❌</td>
        <td><span data-ttu-id="7549c-148">✔️</span><span class="sxs-lookup"><span data-stu-id="7549c-148">✔️</span></span></td>
    </tr>
</table>

## <a name="enabling-research-mode-hololens-1st-gen-and-hololens-2"></a><span data-ttu-id="7549c-149">Activation du mode de recherche (HoloLens 1re génération et HoloLens 2)</span><span class="sxs-lookup"><span data-stu-id="7549c-149">Enabling Research Mode (HoloLens 1st Gen and HoloLens 2)</span></span>

<span data-ttu-id="7549c-150">Le mode de recherche est une extension du mode développeur.</span><span class="sxs-lookup"><span data-stu-id="7549c-150">Research Mode is an extension of Developer Mode.</span></span> <span data-ttu-id="7549c-151">Avant de commencer, les fonctionnalités de développement de l’appareil doivent être activées pour accéder aux paramètres du mode de recherche :</span><span class="sxs-lookup"><span data-stu-id="7549c-151">Before starting, the developer features of the device need to be enabled to access the Research Mode settings:</span></span> 

* <span data-ttu-id="7549c-152">Ouvrez le **menu démarrer > paramètres** , puis sélectionnez **mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="7549c-152">Open **Start Menu > Settings** and select **Updates**.</span></span>
* <span data-ttu-id="7549c-153">Sélectionnez **pour les développeurs** et activer le **mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="7549c-153">Select **For Developers** and enable **Developer Mode**.</span></span>
* <span data-ttu-id="7549c-154">Faites défiler la liste et activez le **portail d’appareil**.</span><span class="sxs-lookup"><span data-stu-id="7549c-154">Scroll down and enable **Device Portal**.</span></span>

<span data-ttu-id="7549c-155">Une fois les fonctionnalités du développeur activées, [Connectez-vous au portail de l’appareil](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens) pour activer les fonctionnalités du mode de recherche :</span><span class="sxs-lookup"><span data-stu-id="7549c-155">After the developer features  are enabled, [connect to the device portal](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens) to enable the Research Mode features:</span></span>

* <span data-ttu-id="7549c-156">Accédez à **système > le mode de recherche** dans le portail de l' **appareil**.</span><span class="sxs-lookup"><span data-stu-id="7549c-156">Go to **System > Research Mode** in the **Device Portal**.</span></span>
* <span data-ttu-id="7549c-157">Sélectionnez **autoriser l’accès au flux de capteur**.</span><span class="sxs-lookup"><span data-stu-id="7549c-157">Select **Allow access to sensor stream**.</span></span>
* <span data-ttu-id="7549c-158">Redémarrez l’appareil à partir de l’élément de menu **Power** situé en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="7549c-158">Restart the device from the **Power** menu item at the top of the page.</span></span>

<span data-ttu-id="7549c-159">Une fois que vous avez redémarré l’appareil, les applications chargées via le portail de l' **appareil** peuvent accéder aux flux en mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="7549c-159">Once you've restarted the device, the applications loaded through the **Device Portal** can access Research Mode streams.</span></span>

<span data-ttu-id="7549c-160">![Onglet mode de recherche du portail de l’appareil HoloLens](images/ResearchModeDevPortal.png)</span><span class="sxs-lookup"><span data-stu-id="7549c-160">![Research Mode tab of HoloLens Device Portal](images/ResearchModeDevPortal.png)</span></span><br>
<span data-ttu-id="7549c-161">*Fenêtre du mode de recherche dans le portail d’appareils HoloLens*</span><span class="sxs-lookup"><span data-stu-id="7549c-161">*Research Mode window in the HoloLens Device Portal*</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7549c-162">Le mode de recherche pour HoloLens 2 est disponible à partir de la build 19041,1356.</span><span class="sxs-lookup"><span data-stu-id="7549c-162">Research Mode for HoloLens 2 is available beginning with build 19041.1356.</span></span> <span data-ttu-id="7549c-163">Si vous avez besoin d’accéder à une version antérieure, inscrivez-vous à notre programme [Insider Preview](https://docs.microsoft.com/hololens/hololens-insider) .</span><span class="sxs-lookup"><span data-stu-id="7549c-163">If you need access in an earlier build, sign up for our [Insider Preview](https://docs.microsoft.com/hololens/hololens-insider) program.</span></span>

### <a name="using-sensor-data-in-your-apps"></a><span data-ttu-id="7549c-164">Utilisation des données de capteur dans vos applications</span><span class="sxs-lookup"><span data-stu-id="7549c-164">Using sensor data in your apps</span></span>

<span data-ttu-id="7549c-165">Les applications peuvent accéder aux données de flux de capteur de la même façon que les flux de photos et les vidéos de caméra vidéo sont accessibles par le biais de [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197).</span><span class="sxs-lookup"><span data-stu-id="7549c-165">Applications can access the sensor stream data in the same way that photo and video camera streams are accessed through [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197).</span></span> 

<span data-ttu-id="7549c-166">Toutes les API qui fonctionnent pour le développement HoloLens sont également disponibles en mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="7549c-166">All APIs that work for HoloLens development are also available in Research Mode.</span></span> <span data-ttu-id="7549c-167">En particulier, l’application sait précisément où HoloLens se trouve dans l’espace 6DoF à chaque fois que la capture de l’image du capteur est terminée.</span><span class="sxs-lookup"><span data-stu-id="7549c-167">In particular, the application  knows precisely where HoloLens is in 6DoF space at each sensor frame capture time.</span></span>

<span data-ttu-id="7549c-168">Vous trouverez des exemples d’applications sur l’accès aux différents flux en mode de recherche, sur l’utilisation des [intrinsèques et des extrinsics](https://docs.microsoft.com/windows/mixed-reality/locatable-camera#locating-the-device-camera-in-the-world), et sur l’enregistrement des flux dans le [HoloLensForCV GitHub référentiel](https://github.com/Microsoft/HoloLensForCV) référentiel.</span><span class="sxs-lookup"><span data-stu-id="7549c-168">You can find sample applications on how to access the various Research Mode streams, how to use the [intrinsics and extrinsics](https://docs.microsoft.com/windows/mixed-reality/locatable-camera#locating-the-device-camera-in-the-world), and how to record streams in the [HoloLensForCV GitHub repo](https://github.com/Microsoft/HoloLensForCV) repo.</span></span>

 > [!NOTE]
 > <span data-ttu-id="7549c-169">À ce stade, l’exemple HoloLensForCV ne fonctionne pas sur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="7549c-169">At this time, the HoloLensForCV sample doesn't work on HoloLens 2.</span></span>

## <a name="support"></a><span data-ttu-id="7549c-170">Support</span><span class="sxs-lookup"><span data-stu-id="7549c-170">Support</span></span>

<span data-ttu-id="7549c-171">Utilisez le [suivi](https://github.com/Microsoft/HololensForCV/issues) des problèmes dans le référentiel HoloLensForCV pour publier des commentaires et effectuer le suivi des problèmes connus.</span><span class="sxs-lookup"><span data-stu-id="7549c-171">Please use the [issue tracker](https://github.com/Microsoft/HololensForCV/issues) in the HoloLensForCV repository to post feedback and track known issues.</span></span>

## <a name="see-also"></a><span data-ttu-id="7549c-172">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7549c-172">See also</span></span>

* [<span data-ttu-id="7549c-173">Microsoft Media Foundation</span><span class="sxs-lookup"><span data-stu-id="7549c-173">Microsoft Media Foundation</span></span>](https://msdn.microsoft.com/library/windows/desktop/ms694197)
* [<span data-ttu-id="7549c-174">HoloLensForCV GitHub référentiel</span><span class="sxs-lookup"><span data-stu-id="7549c-174">HoloLensForCV GitHub repo</span></span>](https://github.com/Microsoft/HoloLensForCV)
* [<span data-ttu-id="7549c-175">Utilisation du portail d’appareil Windows</span><span class="sxs-lookup"><span data-stu-id="7549c-175">Using the Windows Device Portal</span></span>](using-the-windows-device-portal.md)
