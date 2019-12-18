---
title: Son spatial dans Unity
description: Lire le son spatial à partir d’un point 3D spécifique dans votre scène Unity.
author: kegodin
ms.author: kegodin
ms.date: 11/07/2019
ms.topic: article
keywords: Unity, son spatial, HRTF, taille de la salle
ms.openlocfilehash: 3e7d0ea231545d5112d182dffbc02f217ca4a4a7
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75181989"
---
# <a name="spatial-sound-in-unity"></a><span data-ttu-id="c1cf0-104">Son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="c1cf0-104">Spatial sound in Unity</span></span>

<span data-ttu-id="c1cf0-105">Cette page contient des liens vers des ressources pour le son spatial dans Unity.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-105">This page links to resources for spatial sound in Unity.</span></span>

## <a name="spatializer-options"></a><span data-ttu-id="c1cf0-106">Options de Spatializer</span><span class="sxs-lookup"><span data-stu-id="c1cf0-106">Spatializer options</span></span>
<span data-ttu-id="c1cf0-107">Les options Spatializer pour les applications de réalité mixte sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="c1cf0-107">Spatializer options for mixed reality applications include:</span></span>
* <span data-ttu-id="c1cf0-108">*Spatializer MS HRTF*.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-108">The *MS HRTF Spatializer*.</span></span> <span data-ttu-id="c1cf0-109">Unity fournit cela dans le cadre du package facultatif *Windows Mixed Reality* .</span><span class="sxs-lookup"><span data-stu-id="c1cf0-109">Unity provides this as part of the *Windows Mixed Reality* optional package.</span></span>
  * <span data-ttu-id="c1cf0-110">Cela s’exécute sur le processeur dans une architecture à source unique à coût plus élevé.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-110">This runs on CPU in a higher-cost 'single-source' architecture.</span></span>
  * <span data-ttu-id="c1cf0-111">Elle est fournie à des fins de compatibilité descendante avec les applications HoloLens d’origine.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-111">This is provided for backwards compatibility with original HoloLens applications.</span></span>
* <span data-ttu-id="c1cf0-112">*Microsoft Spatializer*.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-112">The *Microsoft Spatializer*.</span></span> <span data-ttu-id="c1cf0-113">Celui-ci est disponible à partir du [dépôt github Microsoft Spatializer](https://github.com/microsoft/spatialaudio-unity).</span><span class="sxs-lookup"><span data-stu-id="c1cf0-113">This is available from the [Microsoft spatializer GitHub repository](https://github.com/microsoft/spatialaudio-unity).</span></span>
  * <span data-ttu-id="c1cf0-114">Cela utilise une architecture à plusieurs sources moins onéreuse.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-114">This uses a lower-cost 'multi-source' architecture.</span></span>
  * <span data-ttu-id="c1cf0-115">Sur HoloLens 2, cette valeur est déchargée sur un accélérateur matériel.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-115">On HoloLens 2, this is offloaded to a hardware accelerator.</span></span>

<span data-ttu-id="c1cf0-116">Pour les nouvelles applications, nous vous recommandons *Microsoft Spatializer*.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-116">For new applications, we recommend the *Microsoft Spatializer*.</span></span>

## <a name="enable-spatialization"></a><span data-ttu-id="c1cf0-117">Activer Spatialization</span><span class="sxs-lookup"><span data-stu-id="c1cf0-117">Enable spatialization</span></span>

<span data-ttu-id="c1cf0-118">Utilisez [NuGet pour Unity](https://github.com/GlitchEnzo/NuGetForUnity/releases/latest) pour installer _Microsoft. SpatialAudio. Spatializer. Unity_ et choisissez **Microsoft Spatializer** dans les paramètres audio de votre projet.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-118">Use [NuGet for Unity](https://github.com/GlitchEnzo/NuGetForUnity/releases/latest) to install _Microsoft.SpatialAudio.Spatializer.Unity_ and choose **Microsoft Spatializer** in your project's audio settings.</span></span> <span data-ttu-id="c1cf0-119">Alors :</span><span class="sxs-lookup"><span data-stu-id="c1cf0-119">Then:</span></span>
* <span data-ttu-id="c1cf0-120">Attacher une **source audio** à un objet dans la hiérarchie</span><span class="sxs-lookup"><span data-stu-id="c1cf0-120">Attach an **Audio Source** to an object in the hierarchy</span></span>
* <span data-ttu-id="c1cf0-121">Cochez la case **Enable Spatialization**</span><span class="sxs-lookup"><span data-stu-id="c1cf0-121">Check the **Enable spatialization** checkbox</span></span>
* <span data-ttu-id="c1cf0-122">Déplacez le curseur de **lissage spatial** sur « 1 »</span><span class="sxs-lookup"><span data-stu-id="c1cf0-122">Move the **Spatial Blend** slider to '1'</span></span>

<span data-ttu-id="c1cf0-123">Pour plus de détails, voir:</span><span class="sxs-lookup"><span data-stu-id="c1cf0-123">For more details, see:</span></span>
* [<span data-ttu-id="c1cf0-124">Dépôt GitHub Microsoft Spatializer</span><span class="sxs-lookup"><span data-stu-id="c1cf0-124">Microsoft spatializer GitHub repository</span></span>](https://github.com/microsoft/spatialaudio-unity)
* [<span data-ttu-id="c1cf0-125">Didacticiel Spatializer de Microsoft</span><span class="sxs-lookup"><span data-stu-id="c1cf0-125">Microsoft's spatializer tutorial</span></span>](unity-spatial-audio-ch1.md)
* [<span data-ttu-id="c1cf0-126">Documentation de la source audio de Unity</span><span class="sxs-lookup"><span data-stu-id="c1cf0-126">Unity's audio source documentation</span></span>](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html)
* [<span data-ttu-id="c1cf0-127">Documentation Spatializer de Unity</span><span class="sxs-lookup"><span data-stu-id="c1cf0-127">Unity's spatializer documentation</span></span>](https://docs.unity3d.com/Manual/VRAudioSpatializer.html)

## <a name="distance-based-attenuation"></a><span data-ttu-id="c1cf0-128">Atténuation basée sur la distance</span><span class="sxs-lookup"><span data-stu-id="c1cf0-128">Distance-based attenuation</span></span>
<span data-ttu-id="c1cf0-129">La dégradation basée sur les distances par défaut d’Unity a une distance minimale de 1 mètre et une distance maximale de 500 mètres, avec un Rolloff logarithmique.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-129">Unity's default distance-based decay has a minimum distance of 1 meter and a maximum distance of 500 meters, with a logarithmic rolloff.</span></span> <span data-ttu-id="c1cf0-130">Ces paramètres peuvent fonctionner pour votre scénario, ou vous pouvez constater que les sources s’atténuent trop rapidement ou trop lentement.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-130">These settings may work for your scenario, or you may find that sources attenuate too quickly or too slowly.</span></span> <span data-ttu-id="c1cf0-131">Pour plus de détails, voir:</span><span class="sxs-lookup"><span data-stu-id="c1cf0-131">For more details, see:</span></span>
* <span data-ttu-id="c1cf0-132">[Conception audio en réalité mixte](spatial-sound-design.md) pour les paramètres recommandés.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-132">[Sound design in mixed reality](spatial-sound-design.md) for recommended settings.</span></span>
* <span data-ttu-id="c1cf0-133">[Documentation de la source audio de Unity](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html) pour obtenir des instructions sur la définition de ces courbes.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-133">[Unity's audio source documentation](https://docs.unity3d.com/2019.3/Documentation/Manual/class-AudioSource.html) for instructions on setting these curves.</span></span>

## <a name="reverb"></a><span data-ttu-id="c1cf0-134">Réverbération</span><span class="sxs-lookup"><span data-stu-id="c1cf0-134">Reverb</span></span>
<span data-ttu-id="c1cf0-135">Le _Spatializer Microsoft_ désactive les effets postérieurs à Spatializer par défaut.</span><span class="sxs-lookup"><span data-stu-id="c1cf0-135">The _Microsoft Spatializer_ disables post-spatializer effects by default.</span></span> <span data-ttu-id="c1cf0-136">Pour activer la réverbération et d’autres effets pour les sources spatiales :</span><span class="sxs-lookup"><span data-stu-id="c1cf0-136">To enable reverb and other effects for spatialized sources:</span></span>
* <span data-ttu-id="c1cf0-137">Attacher le composant de niveau d’envoi de l' **effet de salle** à chaque source</span><span class="sxs-lookup"><span data-stu-id="c1cf0-137">Attach the **Room Effect Send Level** component to each source</span></span>
* <span data-ttu-id="c1cf0-138">Ajustez la courbe de niveau d’envoi pour chaque source, afin de contrôler le gain sur le son renvoyé au graphique pour le traitement des effets</span><span class="sxs-lookup"><span data-stu-id="c1cf0-138">Adjust the send level curve for each source, to control the gain on the audio sent back to the graph for effects processing</span></span>

<span data-ttu-id="c1cf0-139">Pour plus d’informations, consultez [le chapitre 5 du didacticiel Spatializer](unity-spatial-audio-ch5.md) .</span><span class="sxs-lookup"><span data-stu-id="c1cf0-139">See [Chapter 5 of the spatializer tutorial](unity-spatial-audio-ch5.md) for details.</span></span>

## <a name="unity-spatial-sound-examples"></a><span data-ttu-id="c1cf0-140">Exemples de sons spatiaux Unity</span><span class="sxs-lookup"><span data-stu-id="c1cf0-140">Unity spatial sound examples</span></span>
<span data-ttu-id="c1cf0-141">Pour obtenir des exemples de son spatial dans Unity, consultez :</span><span class="sxs-lookup"><span data-stu-id="c1cf0-141">For examples of spatial sound in Unity, see:</span></span>
* [<span data-ttu-id="c1cf0-142">Démonstrations MRTK</span><span class="sxs-lookup"><span data-stu-id="c1cf0-142">MRTK demos</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets/MixedRealityToolkit.Examples/Demos/Audio)
* <span data-ttu-id="c1cf0-143">[Exemple de projet Microsoft Spatializer](https://github.com/microsoft/spatialaudio-unity/tree/master/Samples/MicrosoftSpatializerSample)</span><span class="sxs-lookup"><span data-stu-id="c1cf0-143">The [Microsoft Spatializer sample project](https://github.com/microsoft/spatialaudio-unity/tree/master/Samples/MicrosoftSpatializerSample)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1cf0-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1cf0-144">Next steps</span></span>
* [<span data-ttu-id="c1cf0-145">Conception audio en réalité mixte</span><span class="sxs-lookup"><span data-stu-id="c1cf0-145">Sound design in mixed reality</span></span>](spatial-sound-design.md)
* [<span data-ttu-id="c1cf0-146">Didacticiel Spatializer de Microsoft</span><span class="sxs-lookup"><span data-stu-id="c1cf0-146">Microsoft's spatializer tutorial</span></span>](unity-spatial-audio-ch1.md)

