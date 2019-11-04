---
title: Mode de recherche HoloLens
description: En utilisant le mode de recherche sur HoloLens, une application peut accéder aux flux de capteur de périphérique clé (profondeur, suivi de l’environnement et réflectivité de l’IR).
author: davidgedye
ms.author: dgedye
ms.date: 05/03/2018
ms.topic: article
keywords: mode de recherche, CV, RS4, vision par ordinateur, recherche, HoloLens
ms.openlocfilehash: 307df0c226221422f13af09d8f4944c22ead3865
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438303"
---
# <a name="hololens-research-mode"></a><span data-ttu-id="06b6f-104">Mode de recherche HoloLens</span><span class="sxs-lookup"><span data-stu-id="06b6f-104">HoloLens Research mode</span></span>

> [!NOTE]
> <span data-ttu-id="06b6f-105">Cette fonctionnalité a été ajoutée dans le cadre de la [mise à jour 2018 de Windows 10 avril](release-notes-april-2018.md) pour HoloLens et n’est pas disponible dans les versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="06b6f-105">This feature was added as part of the [Windows 10 April 2018 Update](release-notes-april-2018.md) for HoloLens, and is not available on earlier releases.</span></span>

<span data-ttu-id="06b6f-106">Le mode de recherche est une nouvelle fonctionnalité de HoloLens qui permet à l’application d’accéder aux capteurs de clé sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="06b6f-106">Research mode is a new capability of HoloLens that provides application access to the key sensors on the device.</span></span> <span data-ttu-id="06b6f-107">Il s’agit des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="06b6f-107">These include:</span></span>
- <span data-ttu-id="06b6f-108">Les quatre caméras de suivi de l’environnement utilisées par le système pour la création de cartes et le suivi des têtes.</span><span class="sxs-lookup"><span data-stu-id="06b6f-108">The four environment tracking cameras used by the system for map building and head tracking.</span></span>
- <span data-ttu-id="06b6f-109">Deux versions des données de l’appareil photo de profondeur : une pour la détection presque approfondie à haute fréquence (30 i/s), couramment utilisée pour le suivi de la main, et l’autre pour la détection de profondeur à faible fréquence (1-5 FPS), actuellement utilisée par le mappage spatial,</span><span class="sxs-lookup"><span data-stu-id="06b6f-109">Two versions of the depth camera data – one for high-frequency (30 FPS) near-depth sensing, commonly used in hand tracking, and the other for lower-frequency (1-5 FPS) far-depth sensing, currently used by Spatial Mapping,</span></span>
- <span data-ttu-id="06b6f-110">Deux versions d’un flux de réflectivité IR, utilisées par le HoloLens pour calculer la profondeur, mais précieuses à sa propre valeur, car ces images sont éclairées à partir du HoloLens et raisonnablement non affectées par la lumière ambiante.</span><span class="sxs-lookup"><span data-stu-id="06b6f-110">Two versions of an IR-reflectivity stream, used by the HoloLens to compute depth, but valuable in its own right as these images are illuminated from the HoloLens and reasonably unaffected by ambient light.</span></span>

<span data-ttu-id="06b6f-111">capture d’écran de l’application en mode de recherche ![](images/sensor-stream-viewer.jpg)</span><span class="sxs-lookup"><span data-stu-id="06b6f-111">![Research Mode app screenshot](images/sensor-stream-viewer.jpg)</span></span><br>
<span data-ttu-id="06b6f-112">*Capture de réalité mixte d’une application de test qui affiche les huit flux de capteurs disponibles en mode de recherche*</span><span class="sxs-lookup"><span data-stu-id="06b6f-112">*A mixed reality capture of a test application that displays the eight sensor streams available in Research mode*</span></span>

## <a name="device-support"></a><span data-ttu-id="06b6f-113">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="06b6f-113">Device support</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="06b6f-114"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="06b6f-114"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="06b6f-115"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="06b6f-115"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="06b6f-116"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="06b6f-116"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="06b6f-117">Mode de recherche</span><span class="sxs-lookup"><span data-stu-id="06b6f-117">Research mode</span></span></td>
        <td><span data-ttu-id="06b6f-118">✔️</span><span class="sxs-lookup"><span data-stu-id="06b6f-118">✔️</span></span></td>
        <td>❌</td>
    </tr>
</table>

## <a name="before-using-research-mode"></a><span data-ttu-id="06b6f-119">Avant d’utiliser le mode de recherche</span><span class="sxs-lookup"><span data-stu-id="06b6f-119">Before using Research mode</span></span>

<span data-ttu-id="06b6f-120">Le mode de recherche est bien nommé : il est destiné aux chercheurs universitaires et industriels qui essaient de nouvelles idées dans les domaines de la Vision par ordinateur et de la robotique.</span><span class="sxs-lookup"><span data-stu-id="06b6f-120">Research mode is well named: it is intended for academic and industrial researchers trying out new ideas in the fields of Computer Vision and Robotics.</span></span>  <span data-ttu-id="06b6f-121">Le mode de recherche n’est pas destiné aux applications qui seront déployées au sein d’une entreprise ou mises à disposition dans le Microsoft Store.</span><span class="sxs-lookup"><span data-stu-id="06b6f-121">Research mode is not intended for applications that will be deployed across an enterprise or made available in the Microsoft Store.</span></span> <span data-ttu-id="06b6f-122">Cela est dû au fait que le mode de recherche réduit la sécurité de votre appareil et consomme beaucoup plus d’énergie de batterie que le fonctionnement normal.</span><span class="sxs-lookup"><span data-stu-id="06b6f-122">The reason for this is that Research mode lowers the security of your device and consumes significantly more battery power than normal operation.</span></span> <span data-ttu-id="06b6f-123">Microsoft ne s’engage pas à prendre en charge ce mode sur les futurs appareils.</span><span class="sxs-lookup"><span data-stu-id="06b6f-123">Microsoft is not committing to supporting this mode on any future devices.</span></span> <span data-ttu-id="06b6f-124">Par conséquent, nous vous recommandons de l’utiliser pour développer et tester de nouvelles idées. Toutefois, vous ne serez pas en mesure de déployer largement des applications qui utilisent le mode de recherche ou qui ont l’assurance qu’elles continueront à fonctionner sur du matériel futur.</span><span class="sxs-lookup"><span data-stu-id="06b6f-124">Thus, we recommend you use it to develop and test new ideas; however, you will not be able to widely deploy applications that use Research mode or have any assurance that it will continue to work on future hardware.</span></span>

## <a name="enabling-research-mode"></a><span data-ttu-id="06b6f-125">Activation du mode de recherche</span><span class="sxs-lookup"><span data-stu-id="06b6f-125">Enabling Research mode</span></span>

<span data-ttu-id="06b6f-126">Le mode de recherche est un sous-mode du mode développeur.</span><span class="sxs-lookup"><span data-stu-id="06b6f-126">Research mode is a sub-mode of developer mode.</span></span> <span data-ttu-id="06b6f-127">Vous devez d’abord activer le mode développeur dans l’application Paramètres (**paramètres > mise à jour & > de sécurité pour les développeurs**) :</span><span class="sxs-lookup"><span data-stu-id="06b6f-127">You first need to enable developer mode in the Settings app (**Settings > Update & Security > For developers**):</span></span>

1. <span data-ttu-id="06b6f-128">Définir « utiliser les fonctionnalités pour les développeurs » **sur activé**</span><span class="sxs-lookup"><span data-stu-id="06b6f-128">Set "Use developer features" to **On**</span></span>
2. <span data-ttu-id="06b6f-129">Définir « activer le portail des appareils » **sur activé**</span><span class="sxs-lookup"><span data-stu-id="06b6f-129">Set "Enable Device Portal" to **On**</span></span>

<span data-ttu-id="06b6f-130">Ensuite, à l’aide d’un navigateur Web connecté au même réseau Wi-Fi que votre HoloLens, accédez à l’adresse IP de votre HoloLens (obtenue via les **paramètres > réseau & Internet > les propriétés du matériel > Wi-Fi**).</span><span class="sxs-lookup"><span data-stu-id="06b6f-130">Then using a web browser that is connected to the same Wi-Fi network as your HoloLens, navigate to the IP address of your HoloLens (obtained through **Settings > Network & Internet > Wi-Fi > Hardware properties**).</span></span> <span data-ttu-id="06b6f-131">Il s’agit du portail de l' [appareil](using-the-windows-device-portal.md). vous trouverez une page « mode de recherche » dans la section « système » du portail :</span><span class="sxs-lookup"><span data-stu-id="06b6f-131">This is the [Device Portal](using-the-windows-device-portal.md), and you will find a "Research mode" page in the "System" section of the portal:</span></span>

<span data-ttu-id="06b6f-132">![onglet du mode de recherche du portail de l’appareil HoloLens](images/ResearchModeDevPortal.png)</span><span class="sxs-lookup"><span data-stu-id="06b6f-132">![Research Mode tab of HoloLens Device Portal](images/ResearchModeDevPortal.png)</span></span><br>
<span data-ttu-id="06b6f-133">*Mode de recherche dans le portail d’appareils HoloLens*</span><span class="sxs-lookup"><span data-stu-id="06b6f-133">*Research mode in the HoloLens Device Portal*</span></span>

<span data-ttu-id="06b6f-134">Après avoir sélectionné **autoriser l’accès aux flux de capteurs**, vous devrez redémarrer HoloLens.</span><span class="sxs-lookup"><span data-stu-id="06b6f-134">After selecting **Allow access to sensor streams**, you will need to reboot HoloLens.</span></span> <span data-ttu-id="06b6f-135">Vous pouvez le faire à partir du portail de l’appareil, sous l’élément de menu « Power » en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="06b6f-135">You can do this from the Device Portal, under the "Power" menu item at the top of the page.</span></span>

<span data-ttu-id="06b6f-136">Une fois que votre appareil a redémarré, les applications qui ont été chargées par le biais du portail de l’appareil doivent pouvoir accéder aux flux en mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="06b6f-136">Once your device has rebooted, applications that have been loaded through Device Portal should be able to access Research mode streams.</span></span>

## <a name="using-sensor-data-in-your-apps"></a><span data-ttu-id="06b6f-137">Utilisation des données de capteur dans vos applications</span><span class="sxs-lookup"><span data-stu-id="06b6f-137">Using sensor data in your apps</span></span>

<span data-ttu-id="06b6f-138">Les applications peuvent accéder aux données de flux de capteur en ouvrant [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197) flux exactement de la même façon qu’ils accèdent au flux de caméra photo/vidéo.</span><span class="sxs-lookup"><span data-stu-id="06b6f-138">Applications can access sensor stream data by opening [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197) streams in exactly the same way they access the photo/video camera stream.</span></span> 

<span data-ttu-id="06b6f-139">Toutes les API qui fonctionnent pour le développement HoloLens sont également disponibles en mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="06b6f-139">All APIs that work for HoloLens development are also available when in Research mode.</span></span> <span data-ttu-id="06b6f-140">En particulier, l’application peut savoir précisément où HoloLens se trouve dans l’espace 6DoF à chaque fois que la capture de l’image du capteur est terminée.</span><span class="sxs-lookup"><span data-stu-id="06b6f-140">In particular, the application can know precisely where HoloLens is in 6DoF space at each sensor frame capture time.</span></span>

<span data-ttu-id="06b6f-141">Des exemples d’applications qui montrent comment vous accédez aux différents flux en mode de recherche, comment utiliser les intrinsèques et les extrinsics et comment enregistrer des flux sont disponibles dans le [référentiel GitHub HoloLensForCV](https://github.com/Microsoft/HoloLensForCV).</span><span class="sxs-lookup"><span data-stu-id="06b6f-141">Sample applications showing how you access the various Research mode streams, how to use the intrinsics and extrinsics, and how to record streams are available in the [HoloLensForCV GitHub repo](https://github.com/Microsoft/HoloLensForCV).</span></span>

## <a name="known-issues"></a><span data-ttu-id="06b6f-142">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="06b6f-142">Known issues</span></span>

<span data-ttu-id="06b6f-143">Consultez le [suivi des problèmes](https://github.com/Microsoft/HololensForCV/issues) dans le référentiel HoloLensForCV.</span><span class="sxs-lookup"><span data-stu-id="06b6f-143">See the [issue tracker](https://github.com/Microsoft/HololensForCV/issues) in the HoloLensForCV repository.</span></span>

## <a name="see-also"></a><span data-ttu-id="06b6f-144">Articles associés</span><span class="sxs-lookup"><span data-stu-id="06b6f-144">See also</span></span>

* [<span data-ttu-id="06b6f-145">Microsoft Media Foundation</span><span class="sxs-lookup"><span data-stu-id="06b6f-145">Microsoft Media Foundation</span></span>](https://msdn.microsoft.com/library/windows/desktop/ms694197)
* [<span data-ttu-id="06b6f-146">HoloLensForCV GitHub référentiel</span><span class="sxs-lookup"><span data-stu-id="06b6f-146">HoloLensForCV GitHub repo</span></span>](https://github.com/Microsoft/HoloLensForCV)
* [<span data-ttu-id="06b6f-147">Utilisation du portail d’appareil Windows</span><span class="sxs-lookup"><span data-stu-id="06b6f-147">Using the Windows Device Portal</span></span>](using-the-windows-device-portal.md)
