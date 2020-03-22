---
title: Son spatial dans Unity
description: Lire le son spatial à partir d’un point 3D spécifique dans votre scène Unity.
author: kegodin
ms.author: kegodin
ms.date: 11/07/2019
ms.topic: article
keywords: Unity, son spatial, HRTF, taille de la salle
ms.openlocfilehash: af3f1486c3e931ad93d7b8960d822653ec740c12
ms.sourcegitcommit: ee8c7e821cb337cbccd8af64b13ee5f50109a776
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80082040"
---
# <a name="spatial-sound-in-unity"></a><span data-ttu-id="821eb-104">Son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="821eb-104">Spatial sound in Unity</span></span>

<span data-ttu-id="821eb-105">Cette page contient des liens vers des ressources pour le son spatial dans Unity.</span><span class="sxs-lookup"><span data-stu-id="821eb-105">This page links to resources for spatial sound in Unity.</span></span>

## <a name="spatializer-options"></a><span data-ttu-id="821eb-106">Options de Spatializer</span><span class="sxs-lookup"><span data-stu-id="821eb-106">Spatializer options</span></span>
<span data-ttu-id="821eb-107">Les options Spatializer pour les applications de réalité mixte sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="821eb-107">Spatializer options for mixed reality applications include:</span></span>
* <span data-ttu-id="821eb-108">*Spatializer MS HRTF*.</span><span class="sxs-lookup"><span data-stu-id="821eb-108">The *MS HRTF Spatializer*.</span></span> <span data-ttu-id="821eb-109">Unity fournit cela dans le cadre du package facultatif *Windows Mixed Reality* .</span><span class="sxs-lookup"><span data-stu-id="821eb-109">Unity provides this as part of the *Windows Mixed Reality* optional package.</span></span>
  * <span data-ttu-id="821eb-110">Cela s’exécute sur le processeur dans une architecture à source unique à coût plus élevé.</span><span class="sxs-lookup"><span data-stu-id="821eb-110">This runs on CPU in a higher-cost 'single-source' architecture.</span></span>
  * <span data-ttu-id="821eb-111">Elle est fournie à des fins de compatibilité descendante avec les applications HoloLens d’origine.</span><span class="sxs-lookup"><span data-stu-id="821eb-111">This is provided for backwards compatibility with original HoloLens applications.</span></span>
* <span data-ttu-id="821eb-112">*Microsoft Spatializer*.</span><span class="sxs-lookup"><span data-stu-id="821eb-112">The *Microsoft Spatializer*.</span></span> <span data-ttu-id="821eb-113">Celui-ci est disponible à partir du [dépôt github Microsoft Spatializer](https://github.com/microsoft/spatialaudio-unity).</span><span class="sxs-lookup"><span data-stu-id="821eb-113">This is available from the [Microsoft spatializer GitHub repository](https://github.com/microsoft/spatialaudio-unity).</span></span>
  * <span data-ttu-id="821eb-114">Cela utilise une architecture à plusieurs sources moins onéreuse.</span><span class="sxs-lookup"><span data-stu-id="821eb-114">This uses a lower-cost 'multi-source' architecture.</span></span>
  * <span data-ttu-id="821eb-115">Sur HoloLens 2, cette valeur est déchargée sur un accélérateur matériel.</span><span class="sxs-lookup"><span data-stu-id="821eb-115">On HoloLens 2, this is offloaded to a hardware accelerator.</span></span>

<span data-ttu-id="821eb-116">Pour les nouvelles applications, nous vous recommandons *Microsoft Spatializer*.</span><span class="sxs-lookup"><span data-stu-id="821eb-116">For new applications, we recommend the *Microsoft Spatializer*.</span></span>

## <a name="enable-spatialization"></a><span data-ttu-id="821eb-117">Activer Spatialization</span><span class="sxs-lookup"><span data-stu-id="821eb-117">Enable spatialization</span></span>

<span data-ttu-id="821eb-118">Utilisez [NuGet pour Unity](https://github.com/GlitchEnzo/NuGetForUnity/releases/latest) pour installer _Microsoft. SpatialAudio. Spatializer. Unity_ et choisissez **Microsoft Spatializer** dans les paramètres audio de votre projet.</span><span class="sxs-lookup"><span data-stu-id="821eb-118">Use [NuGet for Unity](https://github.com/GlitchEnzo/NuGetForUnity/releases/latest) to install _Microsoft.SpatialAudio.Spatializer.Unity_ and choose **Microsoft Spatializer** in your project's audio settings.</span></span> <span data-ttu-id="821eb-119">Puis :</span><span class="sxs-lookup"><span data-stu-id="821eb-119">Then:</span></span>
* <span data-ttu-id="821eb-120">Attacher une **source audio** à un objet dans la hiérarchie</span><span class="sxs-lookup"><span data-stu-id="821eb-120">Attach an **Audio Source** to an object in the hierarchy</span></span>
* <span data-ttu-id="821eb-121">Cochez la case **Enable Spatialization**</span><span class="sxs-lookup"><span data-stu-id="821eb-121">Check the **Enable spatialization** checkbox</span></span>
* <span data-ttu-id="821eb-122">Déplacez le curseur de **lissage spatial** sur « 1 »</span><span class="sxs-lookup"><span data-stu-id="821eb-122">Move the **Spatial Blend** slider to '1'</span></span>
* <span data-ttu-id="821eb-123">Assurez-vous que l’audio spatial est activé sur votre station de travail de développeur.</span><span class="sxs-lookup"><span data-stu-id="821eb-123">Ensure spatial audio is enabled on your developer workstation.</span></span> <span data-ttu-id="821eb-124">Activez-le en cliquant avec le bouton droit sur l’icône de volume dans la barre des tâches et en vous assurant que le son spatial est défini sur une valeur autre que « désactivé ».</span><span class="sxs-lookup"><span data-stu-id="821eb-124">Enable it by right-clicking on the volume icon in the task bar and making sure that Spatial Sound is set to something other than "off."</span></span> <span data-ttu-id="821eb-125">Pour obtenir la meilleure représentation de ce que vous entendez sur HoloLens 2, choisissez **Windows Sonic pour casque**.</span><span class="sxs-lookup"><span data-stu-id="821eb-125">To get the best representation of what you'll hear on HoloLens 2, choose **Windows Sonic for Headphones**.</span></span>

>[!NOTE]
><span data-ttu-id="821eb-126">Si vous recevez une erreur dans Unity sur le fait de ne pas pouvoir charger le plug-in Microsoft. SpatialAudio. Spatializer. Unity, car l’une de ses dépendances est manquante, vérifiez que la dernière version de [Microsoft Visual C++ Redistributable](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads) est installée sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="821eb-126">If you get an error in Unity about not being able to load plugin Microsoft.SpatialAudio.Spatializer.Unity because one of its dependencies is missing, check that you have the latest version of the [Microsoft Visual C++ Redistributable](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads) installed on your PC.</span></span>

<span data-ttu-id="821eb-127">Pour plus de détails, voir:</span><span class="sxs-lookup"><span data-stu-id="821eb-127">For more details, see:</span></span>
* [<span data-ttu-id="821eb-128">Dépôt GitHub Microsoft Spatializer</span><span class="sxs-lookup"><span data-stu-id="821eb-128">Microsoft spatializer GitHub repository</span></span>](https://github.com/microsoft/spatialaudio-unity)
* [<span data-ttu-id="821eb-129">Didacticiel Spatializer de Microsoft</span><span class="sxs-lookup"><span data-stu-id="821eb-129">Microsoft's spatializer tutorial</span></span>](unity-spatial-audio-ch1.md)
* [<span data-ttu-id="821eb-130">Documentation de la source audio de Unity</span><span class="sxs-lookup"><span data-stu-id="821eb-130">Unity's audio source documentation</span></span>](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html)
* [<span data-ttu-id="821eb-131">Documentation Spatializer de Unity</span><span class="sxs-lookup"><span data-stu-id="821eb-131">Unity's spatializer documentation</span></span>](https://docs.unity3d.com/Manual/VRAudioSpatializer.html)

## <a name="distance-based-attenuation"></a><span data-ttu-id="821eb-132">Atténuation basée sur la distance</span><span class="sxs-lookup"><span data-stu-id="821eb-132">Distance-based attenuation</span></span>
<span data-ttu-id="821eb-133">La dégradation basée sur les distances par défaut d’Unity a une distance minimale de 1 mètre et une distance maximale de 500 mètres, avec un Rolloff logarithmique.</span><span class="sxs-lookup"><span data-stu-id="821eb-133">Unity's default distance-based decay has a minimum distance of 1 meter and a maximum distance of 500 meters, with a logarithmic rolloff.</span></span> <span data-ttu-id="821eb-134">Ces paramètres peuvent fonctionner pour votre scénario, ou vous pouvez constater que les sources s’atténuent trop rapidement ou trop lentement.</span><span class="sxs-lookup"><span data-stu-id="821eb-134">These settings may work for your scenario, or you may find that sources attenuate too quickly or too slowly.</span></span> <span data-ttu-id="821eb-135">Pour plus de détails, voir:</span><span class="sxs-lookup"><span data-stu-id="821eb-135">For more details, see:</span></span>
* <span data-ttu-id="821eb-136">[Conception audio en réalité mixte](spatial-sound-design.md) pour les paramètres recommandés.</span><span class="sxs-lookup"><span data-stu-id="821eb-136">[Sound design in mixed reality](spatial-sound-design.md) for recommended settings.</span></span>
* <span data-ttu-id="821eb-137">[Documentation de la source audio de Unity](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html) pour obtenir des instructions sur la définition de ces courbes.</span><span class="sxs-lookup"><span data-stu-id="821eb-137">[Unity's audio source documentation](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html) for instructions on setting these curves.</span></span>

## <a name="reverb"></a><span data-ttu-id="821eb-138">Réverbération</span><span class="sxs-lookup"><span data-stu-id="821eb-138">Reverb</span></span>
<span data-ttu-id="821eb-139">Le _Spatializer Microsoft_ désactive les effets postérieurs à Spatializer par défaut.</span><span class="sxs-lookup"><span data-stu-id="821eb-139">The _Microsoft Spatializer_ disables post-spatializer effects by default.</span></span> <span data-ttu-id="821eb-140">Pour activer la réverbération et d’autres effets pour les sources spatiales :</span><span class="sxs-lookup"><span data-stu-id="821eb-140">To enable reverb and other effects for spatialized sources:</span></span>
* <span data-ttu-id="821eb-141">Attacher le composant de niveau d’envoi de l' **effet de salle** à chaque source</span><span class="sxs-lookup"><span data-stu-id="821eb-141">Attach the **Room Effect Send Level** component to each source</span></span>
* <span data-ttu-id="821eb-142">Ajustez la courbe de niveau d’envoi pour chaque source, afin de contrôler le gain sur le son renvoyé au graphique pour le traitement des effets</span><span class="sxs-lookup"><span data-stu-id="821eb-142">Adjust the send level curve for each source, to control the gain on the audio sent back to the graph for effects processing</span></span>

<span data-ttu-id="821eb-143">Pour plus d’informations, consultez [le chapitre 5 du didacticiel Spatializer](unity-spatial-audio-ch5.md) .</span><span class="sxs-lookup"><span data-stu-id="821eb-143">See [Chapter 5 of the spatializer tutorial](unity-spatial-audio-ch5.md) for details.</span></span>

## <a name="unity-spatial-sound-examples"></a><span data-ttu-id="821eb-144">Exemples de sons spatiaux Unity</span><span class="sxs-lookup"><span data-stu-id="821eb-144">Unity spatial sound examples</span></span>
<span data-ttu-id="821eb-145">Pour obtenir des exemples de son spatial dans Unity, consultez :</span><span class="sxs-lookup"><span data-stu-id="821eb-145">For examples of spatial sound in Unity, see:</span></span>
* [<span data-ttu-id="821eb-146">Démonstrations MRTK</span><span class="sxs-lookup"><span data-stu-id="821eb-146">MRTK demos</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.Examples/Demos/Audio)
* <span data-ttu-id="821eb-147">[Exemple de projet Microsoft Spatializer](https://github.com/microsoft/spatialaudio-unity/tree/master/Samples/MicrosoftSpatializerSample)</span><span class="sxs-lookup"><span data-stu-id="821eb-147">The [Microsoft Spatializer sample project](https://github.com/microsoft/spatialaudio-unity/tree/master/Samples/MicrosoftSpatializerSample)</span></span>

## <a name="next-steps"></a><span data-ttu-id="821eb-148">Étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="821eb-148">Next steps</span></span>
* [<span data-ttu-id="821eb-149">Conception audio en réalité mixte</span><span class="sxs-lookup"><span data-stu-id="821eb-149">Sound design in mixed reality</span></span>](spatial-sound-design.md)
* [<span data-ttu-id="821eb-150">Didacticiel Spatializer de Microsoft</span><span class="sxs-lookup"><span data-stu-id="821eb-150">Microsoft's spatializer tutorial</span></span>](unity-spatial-audio-ch1.md)

