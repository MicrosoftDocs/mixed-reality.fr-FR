---
title: Mode de recherche de HoloLens
description: Utilisez le mode de recherche sur HoloLens, une application peut accéder aux flux de capteur clé d’appareil (profondeur, l’environnement de suivi et réflectivité de runtime d’intégration).
author: davidgedye
ms.author: dgedye
ms.date: 05/03/2018
ms.topic: article
keywords: mode de recherche, cv, rs4, vision par ordinateur, recherche, HoloLens
ms.openlocfilehash: e9a7683f8d582b459185066e74655e8f2b236db4
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829932"
---
# <a name="hololens-research-mode"></a><span data-ttu-id="72dab-104">Mode de recherche de HoloLens</span><span class="sxs-lookup"><span data-stu-id="72dab-104">HoloLens Research mode</span></span>

> [!NOTE]
> <span data-ttu-id="72dab-105">Cette fonctionnalité a été ajoutée dans le cadre de la [mettre à jour du 10 avril 2018 Windows](release-notes-april-2018.md) pour HoloLens et n’est pas disponible sur les versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="72dab-105">This feature was added as part of the [Windows 10 April 2018 Update](release-notes-april-2018.md) for HoloLens, and is not available on earlier releases.</span></span>

<span data-ttu-id="72dab-106">Mode de recherche est une nouvelle fonctionnalité de HoloLens qui fournit l’accès d’application pour les capteurs de clé sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="72dab-106">Research mode is a new capability of HoloLens that provides application access to the key sensors on the device.</span></span> <span data-ttu-id="72dab-107">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="72dab-107">These include:</span></span>
- <span data-ttu-id="72dab-108">Les quatre environnement suivi des caméras utilisées par le système pour la création de la carte et de suivi principal.</span><span class="sxs-lookup"><span data-stu-id="72dab-108">The four environment tracking cameras used by the system for map building and head tracking.</span></span>
- <span data-ttu-id="72dab-109">Deux versions des données de caméra profondeur – celui de détection de près de profondeur (30 i/s) à fréquence élevée, couramment utilisé de suivi dans la main et l’autre pour la fréquence inférieure (1 i/s) plus en profondeur de détection, actuellement utilisaient par le mappage Spatial,</span><span class="sxs-lookup"><span data-stu-id="72dab-109">Two versions of the depth camera data – one for high-frequency (30 FPS) near-depth sensing, commonly used in hand tracking, and the other for lower-frequency (1 FPS) far-depth sensing, currently used by Spatial Mapping,</span></span>
- <span data-ttu-id="72dab-110">Deux versions d’un flux de runtime d’intégration-réflectivité, utilisé par le HoloLens pour calculer la profondeur, mais seront utiles à part entière comme ces images sont éclairés à partir de la HoloLens et raisonnablement pas affectés par la lumière ambiante.</span><span class="sxs-lookup"><span data-stu-id="72dab-110">Two versions of an IR-reflectivity stream, used by the HoloLens to compute depth, but valuable in its own right as these images are illuminated from the HoloLens and reasonably unaffected by ambient light.</span></span>

<span data-ttu-id="72dab-111">![Capture d’écran de recherche en Mode application](images/sensor-stream-viewer.jpg)</span><span class="sxs-lookup"><span data-stu-id="72dab-111">![Research Mode app screenshot](images/sensor-stream-viewer.jpg)</span></span><br>
<span data-ttu-id="72dab-112">*Une capture de réalité mixte d’une application de test qui affiche les flux de huit capteurs disponibles en mode de recherche*</span><span class="sxs-lookup"><span data-stu-id="72dab-112">*A mixed reality capture of a test application that displays the eight sensor streams available in Research mode*</span></span>

## <a name="device-support"></a><span data-ttu-id="72dab-113">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="72dab-113">Device support</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="72dab-114"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="72dab-114"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="72dab-115"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="72dab-115"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="72dab-116"><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></span><span class="sxs-lookup"><span data-stu-id="72dab-116"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="72dab-117">Mode de recherche</span><span class="sxs-lookup"><span data-stu-id="72dab-117">Research mode</span></span></td>
        <td><span data-ttu-id="72dab-118">✔️</span><span class="sxs-lookup"><span data-stu-id="72dab-118">✔️</span></span></td>
        <td><span data-ttu-id="72dab-119">❌</span><span class="sxs-lookup"><span data-stu-id="72dab-119">❌</span></span></td>
    </tr>
</table>

## <a name="before-using-research-mode"></a><span data-ttu-id="72dab-120">Avant d’utiliser le mode de recherche</span><span class="sxs-lookup"><span data-stu-id="72dab-120">Before using Research mode</span></span>

<span data-ttu-id="72dab-121">Mode de recherche est également nommé : elle est conçue pour les chercheurs universitaires et industriels essayant de nouvelles idées dans les champs de la robotique et de vision par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="72dab-121">Research mode is well named: it is intended for academic and industrial researchers trying out new ideas in the fields of Computer Vision and Robotics.</span></span>  <span data-ttu-id="72dab-122">Mode de recherche n’est pas destiné à être des applications qui seront déployées dans une entreprise ou à votre disposition dans le Microsoft Store.</span><span class="sxs-lookup"><span data-stu-id="72dab-122">Research mode is not intended for applications that will be deployed across an enterprise or made available in the Microsoft Store.</span></span> <span data-ttu-id="72dab-123">La raison à cela est que le mode de recherche réduit la sécurité de votre appareil et consomme beaucoup plus d’énergie à un fonctionnement normal.</span><span class="sxs-lookup"><span data-stu-id="72dab-123">The reason for this is that Research mode lowers the security of your device and consumes significantly more battery power than normal operation.</span></span> <span data-ttu-id="72dab-124">Microsoft ne valide pas à prendre en charge ce mode sur tous les périphériques futures.</span><span class="sxs-lookup"><span data-stu-id="72dab-124">Microsoft is not committing to supporting this mode on any future devices.</span></span> <span data-ttu-id="72dab-125">Par conséquent, nous vous recommandons de qu'utiliser il pour développer et tester de nouvelles idées ; Toutefois, vous ne serez pas en mesure de déployer largement les applications qui utilisent le mode de recherche ou ont n’importe quel assurance qu’il continue de fonctionner sur du matériel futures.</span><span class="sxs-lookup"><span data-stu-id="72dab-125">Thus, we recommend you use it to develop and test new ideas; however, you will not be able to widely deploy applications that use Research mode or have any assurance that it will continue to work on future hardware.</span></span>

## <a name="enabling-research-mode"></a><span data-ttu-id="72dab-126">L’activation du mode de recherche</span><span class="sxs-lookup"><span data-stu-id="72dab-126">Enabling Research mode</span></span>

<span data-ttu-id="72dab-127">Mode de recherche est un mode de sous-chemin de mode développeur.</span><span class="sxs-lookup"><span data-stu-id="72dab-127">Research mode is a sub-mode of developer mode.</span></span> <span data-ttu-id="72dab-128">Vous devez d’abord activer le mode développeur dans l’application Paramètres (**Paramètres > mise à jour & sécurité > pour les développeurs**) :</span><span class="sxs-lookup"><span data-stu-id="72dab-128">You first need to enable developer mode in the Settings app (**Settings > Update & Security > For developers**):</span></span>

1. <span data-ttu-id="72dab-129">La valeur « Utiliser les fonctionnalités de développement » **sur**</span><span class="sxs-lookup"><span data-stu-id="72dab-129">Set "Use developer features" to **On**</span></span>
2. <span data-ttu-id="72dab-130">La valeur est « Activer le portail de l’appareil » **sur**</span><span class="sxs-lookup"><span data-stu-id="72dab-130">Set "Enable Device Portal" to **On**</span></span>

<span data-ttu-id="72dab-131">Puis en utilisant un navigateur web qui est connecté au même réseau Wi-Fi en tant que votre HoloLens, accédez à l’adresse IP de votre HoloLens (obtenues via **Paramètres > réseau & Internet > Wi-Fi > Propriétés de matériel**).</span><span class="sxs-lookup"><span data-stu-id="72dab-131">Then using a web browser that is connected to the same Wi-Fi network as your HoloLens, navigate to the IP address of your HoloLens (obtained through **Settings > Network & Internet > Wi-Fi > Hardware properties**).</span></span> <span data-ttu-id="72dab-132">Il s’agit du [appareil portail](using-the-windows-device-portal.md), et vous trouverez une page « Mode de recherche » dans la section « Système » du portail :</span><span class="sxs-lookup"><span data-stu-id="72dab-132">This is the [Device Portal](using-the-windows-device-portal.md), and you will find a "Research mode" page in the "System" section of the portal:</span></span>

<span data-ttu-id="72dab-133">![Onglet du Mode recherche du portail d’appareil HoloLens](images/ResearchModeDevPortal.png)</span><span class="sxs-lookup"><span data-stu-id="72dab-133">![Research Mode tab of HoloLens Device Portal](images/ResearchModeDevPortal.png)</span></span><br>
<span data-ttu-id="72dab-134">*Mode de recherche dans le portail des appareils HoloLens*</span><span class="sxs-lookup"><span data-stu-id="72dab-134">*Research mode in the HoloLens Device Portal*</span></span>

<span data-ttu-id="72dab-135">Après avoir sélectionné **autoriser l’accès au flux de données de capteur**, vous devrez redémarrer HoloLens.</span><span class="sxs-lookup"><span data-stu-id="72dab-135">After selecting **Allow access to sensor streams**, you will need to reboot HoloLens.</span></span> <span data-ttu-id="72dab-136">Pour cela, à partir du portail de l’appareil, sous l’élément de menu « Power » en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="72dab-136">You can do this from the Device Portal, under the "Power" menu item at the top of the page.</span></span>

<span data-ttu-id="72dab-137">Une fois que votre appareil a redémarré, les applications qui ont été chargées via le portail de l’appareil doivent être en mesure d’accéder aux flux de mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="72dab-137">Once your device has rebooted, applications that have been loaded through Device Portal should be able to access Research mode streams.</span></span>

## <a name="using-sensor-data-in-your-apps"></a><span data-ttu-id="72dab-138">À l’aide des données de capteur dans vos applications</span><span class="sxs-lookup"><span data-stu-id="72dab-138">Using sensor data in your apps</span></span>

<span data-ttu-id="72dab-139">Applications peuvent accéder aux données de flux de données de capteur en ouvrant [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197) flux dans exactement la même façon qu’ils le flux de caméra vidéo/photo.</span><span class="sxs-lookup"><span data-stu-id="72dab-139">Applications can access sensor stream data by opening [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197) streams in exactly the same way they access the photo/video camera stream.</span></span> 

<span data-ttu-id="72dab-140">Toutes les API qui fonctionnent pour le développement de HoloLens sont également disponibles en mode de recherche.</span><span class="sxs-lookup"><span data-stu-id="72dab-140">All APIs that work for HoloLens development are also available when in Research mode.</span></span> <span data-ttu-id="72dab-141">En particulier, l’application peut savoir précisément où HoloLens dans 6DoF espace à chaque heure de capture de frame de capteur.</span><span class="sxs-lookup"><span data-stu-id="72dab-141">In particular, the application can know precisely where HoloLens is in 6DoF space at each sensor frame capture time.</span></span>

<span data-ttu-id="72dab-142">Exemples d’applications en montrant comment vous accéder aux différents flux de mode de recherche, comment utiliser les fonctions intrinsèques et extrinsics et comment enregistrer le flux de données sont disponibles dans le [référentiel GitHub de HoloLensForCV](https://github.com/Microsoft/HoloLensForCV).</span><span class="sxs-lookup"><span data-stu-id="72dab-142">Sample applications showing how you access the various Research mode streams, how to use the intrinsics and extrinsics, and how to record streams are available in the [HoloLensForCV GitHub repo](https://github.com/Microsoft/HoloLensForCV).</span></span>

## <a name="known-issues"></a><span data-ttu-id="72dab-143">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="72dab-143">Known issues</span></span>

<span data-ttu-id="72dab-144">Consultez le [Traqueur](https://github.com/Microsoft/HololensForCV/issues) dans le référentiel HoloLensForCV.</span><span class="sxs-lookup"><span data-stu-id="72dab-144">See the [issue tracker](https://github.com/Microsoft/HololensForCV/issues) in the HoloLensForCV repository.</span></span>

## <a name="see-also"></a><span data-ttu-id="72dab-145">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="72dab-145">See also</span></span>

* [<span data-ttu-id="72dab-146">Microsoft Media Foundation</span><span class="sxs-lookup"><span data-stu-id="72dab-146">Microsoft Media Foundation</span></span>](https://msdn.microsoft.com/library/windows/desktop/ms694197)
* [<span data-ttu-id="72dab-147">Référentiel GitHub de HoloLensForCV</span><span class="sxs-lookup"><span data-stu-id="72dab-147">HoloLensForCV GitHub repo</span></span>](https://github.com/Microsoft/HoloLensForCV)
* [<span data-ttu-id="72dab-148">Utilisation du portail d’appareil Windows</span><span class="sxs-lookup"><span data-stu-id="72dab-148">Using the Windows Device Portal</span></span>](using-the-windows-device-portal.md)
