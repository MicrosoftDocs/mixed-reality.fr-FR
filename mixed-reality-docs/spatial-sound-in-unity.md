---
title: Son spatial dans Unity
description: Lecture d’un son spatial provient d’un point en 3D spécifique au sein de votre scène Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, son spatial, HRTF, taille de la pièce
ms.openlocfilehash: e2b321d7086314a14a940d57aa17e67636c758b8
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593231"
---
# <a name="spatial-sound-in-unity"></a><span data-ttu-id="0cb38-104">Son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="0cb38-104">Spatial sound in Unity</span></span>

<span data-ttu-id="0cb38-105">Cette rubrique décrit comment utiliser le son de Spatial dans vos projets Unity.</span><span class="sxs-lookup"><span data-stu-id="0cb38-105">This topic describes how to use Spatial Sound in your Unity projects.</span></span> <span data-ttu-id="0cb38-106">Il couvre les fichiers de plug-in requis ainsi que les composants de Unity et les propriétés qui permettent son de Spatial.</span><span class="sxs-lookup"><span data-stu-id="0cb38-106">It covers the required plugin files as well as the Unity components and properties that enable Spatial Sound.</span></span>

## <a name="enabling-spatial-sound-in-unity"></a><span data-ttu-id="0cb38-107">L’activation de son Spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="0cb38-107">Enabling Spatial Sound in Unity</span></span>

<span data-ttu-id="0cb38-108">Spatial son, dans Unity, est activé à l’aide d’un plug-in spatial audio.</span><span class="sxs-lookup"><span data-stu-id="0cb38-108">Spatial Sound, in Unity, is enabled using an audio spatializer plugin.</span></span> <span data-ttu-id="0cb38-109">Les fichiers de plug-in sont regroupées directement dans Unity, par conséquent, l’activation de son spatial est aussi simple que va **Modifier > Paramètres du projet > Audio** et en modifiant le **plug-in spatial** dans l’inspecteur pour les  **MS HRTF spatial**.</span><span class="sxs-lookup"><span data-stu-id="0cb38-109">The plugin files are bundled directly into Unity so enabling spatial sound is as easy as going to **Edit > Project Settings > Audio** and changing the **Spatializer Plugin** in the Inspector to the **MS HRTF Spatializer**.</span></span> <span data-ttu-id="0cb38-110">Dans la mesure où le spatial Microsoft uniquement Hz 48000 prend actuellement en charge, vous devez également définir votre taux d’échantillonnage système à 48000 afin d’éviter un échec HRTF dans les rares cas que votre périphérique de sortie du système n’est pas déjà définie sur 48000 :</span><span class="sxs-lookup"><span data-stu-id="0cb38-110">Since the Microsoft spatializer only supports 48000Hz currently, you should also set your System Sample Rate to 48000 to prevent an HRTF failure in the rare case that your system output device is not set to 48000 already:</span></span>

<span data-ttu-id="0cb38-111">![Inspecteur pour AudioManager](images/audio-250px.png)</span><span class="sxs-lookup"><span data-stu-id="0cb38-111">![Inspector for AudioManager](images/audio-250px.png)</span></span><br>
<span data-ttu-id="0cb38-112">*Inspecteur pour AudioManager*</span><span class="sxs-lookup"><span data-stu-id="0cb38-112">*Inspector for AudioManager*</span></span>

<span data-ttu-id="0cb38-113">Votre projet Unity est maintenant configuré pour utiliser le son de Spatial.</span><span class="sxs-lookup"><span data-stu-id="0cb38-113">Your Unity project is now configured to use Spatial Sound.</span></span>

>[!NOTE]
><span data-ttu-id="0cb38-114">Si vous n’utilisez pas un PC Windows 10 pour le développement, vous n’obtiendrez Spatial son dans l’éditeur, ni sur l’appareil (même si vous utilisez le SDK Windows 10).</span><span class="sxs-lookup"><span data-stu-id="0cb38-114">If you aren't using a Windows 10 PC for development, you won't get Spatial Sound in the editor nor on the device (even if you're using the Windows 10 SDK).</span></span>

## <a name="using-spatial-sound-in-unity"></a><span data-ttu-id="0cb38-115">À l’aide de son Spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="0cb38-115">Using Spatial Sound in Unity</span></span>

<span data-ttu-id="0cb38-116">Spatial son est utilisé dans votre projet Unity en ajustant les trois paramètres sur vos composants de la Source de données Audio.</span><span class="sxs-lookup"><span data-stu-id="0cb38-116">Spatial Sound is used in your Unity project by adjusting three settings on your Audio Source components.</span></span> <span data-ttu-id="0cb38-117">Les étapes suivantes va configurer les composants de votre Source de données Audio Spatial audio.</span><span class="sxs-lookup"><span data-stu-id="0cb38-117">The following steps will configure your Audio Source components for Spatial Sound.</span></span>
* <span data-ttu-id="0cb38-118">Dans le **hiérarchie** du panneau, sélectionnez l’objet de jeu qui a un attaché **Audio Source**.</span><span class="sxs-lookup"><span data-stu-id="0cb38-118">In the **Hierarchy** panel, select the game object that has an attached **Audio Source**.</span></span>
* <span data-ttu-id="0cb38-119">Dans le **inspecteur** panneau, sous la **Audio Source** composant</span><span class="sxs-lookup"><span data-stu-id="0cb38-119">In the **Inspector** panel, under the **Audio Source** component</span></span>
    * <span data-ttu-id="0cb38-120">Vérifier le **Spatialize** option.</span><span class="sxs-lookup"><span data-stu-id="0cb38-120">Check the **Spatialize** option.</span></span>
    * <span data-ttu-id="0cb38-121">Définissez **Blend Spatial** à **3D** (valeur numérique 1).</span><span class="sxs-lookup"><span data-stu-id="0cb38-121">Set **Spatial Blend** to **3D** (numeric value 1).</span></span>
    * <span data-ttu-id="0cb38-122">Pour de meilleurs résultats, développez **les paramètres audio 3D** et définissez **Volume écrêtage** à **personnalisé écrêtage**.</span><span class="sxs-lookup"><span data-stu-id="0cb38-122">For best results, expand **3D Sound Settings** and set **Volume Rolloff** to **Custom Rolloff**.</span></span>

<span data-ttu-id="0cb38-123">![Panneau Inspecteur dans Unity affichant la Source Audio](images/audiosource.png)</span><span class="sxs-lookup"><span data-stu-id="0cb38-123">![Inspector panel in Unity showing the Audio Source](images/audiosource.png)</span></span><br>
<span data-ttu-id="0cb38-124">*Panneau Inspecteur dans Unity affichant la Source Audio*</span><span class="sxs-lookup"><span data-stu-id="0cb38-124">*Inspector panel in Unity showing the Audio Source*</span></span>

<span data-ttu-id="0cb38-125">Votre sons réaliste existent maintenant dans l’environnement de votre projet !</span><span class="sxs-lookup"><span data-stu-id="0cb38-125">Your sounds now realistically exist inside your project's environment!</span></span>

<span data-ttu-id="0cb38-126">Il est fortement recommandé de vous familiariser avec la [les instructions de conception Spatial son](spatial-sound-design.md).</span><span class="sxs-lookup"><span data-stu-id="0cb38-126">It is strongly recommended that you become familiar with the [Spatial Sound design guidelines](spatial-sound-design.md).</span></span> <span data-ttu-id="0cb38-127">Ces instructions permettent d’intégrer votre audio en toute transparence dans votre projet et à plonger davantage vos utilisateurs dans l’expérience que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="0cb38-127">These guidelines help to integrate your audio seamlessly into your project and to further immerse your users into the experience you have created.</span></span>

## <a name="setting-spatial-sound-settings"></a><span data-ttu-id="0cb38-128">Définition des paramètres de son Spatial</span><span class="sxs-lookup"><span data-stu-id="0cb38-128">Setting Spatial Sound Settings</span></span>

<span data-ttu-id="0cb38-129">Le plug-in Microsoft Spatial Sound fournit un paramètre supplémentaire qui peut être défini, dans une application par Source Audio, pour permettre un contrôle supplémentaire de la simulation audio.</span><span class="sxs-lookup"><span data-stu-id="0cb38-129">The Microsoft Spatial Sound plugin provides an additional parameter that can be set, on a per Audio Source basis, to allow additional control of the audio simulation.</span></span> <span data-ttu-id="0cb38-130">Ce paramètre est la taille de la salle simulée.</span><span class="sxs-lookup"><span data-stu-id="0cb38-130">This parameter is the size of the simulated room.</span></span>

### <a name="room-size"></a><span data-ttu-id="0cb38-131">Taille de la pièce</span><span class="sxs-lookup"><span data-stu-id="0cb38-131">Room Size</span></span>

<span data-ttu-id="0cb38-132">La taille de salle de conversation est simulée par Spatial son.</span><span class="sxs-lookup"><span data-stu-id="0cb38-132">The size of room that is being simulated by Spatial Sound.</span></span> <span data-ttu-id="0cb38-133">La taille approximative des salles est ; petite (un bureau à une salle de conférence petit), moyenne (une grande salle de conférence) et de grande taille (un auditorium).</span><span class="sxs-lookup"><span data-stu-id="0cb38-133">The approximate sizes of the rooms are; small (an office to a small conference room), medium (a large conference room) and large (an auditorium).</span></span> <span data-ttu-id="0cb38-134">Vous pouvez également spécifier une taille de la pièce None pour simuler un environnement extérieur.</span><span class="sxs-lookup"><span data-stu-id="0cb38-134">You can also specify a room size of none to simulate an outdoor environment.</span></span> <span data-ttu-id="0cb38-135">La taille de la valeur par défaut est petite.</span><span class="sxs-lookup"><span data-stu-id="0cb38-135">The default room size is small.</span></span>

### <a name="example"></a><span data-ttu-id="0cb38-136">Exemple</span><span class="sxs-lookup"><span data-stu-id="0cb38-136">Example</span></span>

<span data-ttu-id="0cb38-137">Le MixedRealityToolkit pour Unity fournit une classe statique qui rend la configuration des paramètres Spatial son facile.</span><span class="sxs-lookup"><span data-stu-id="0cb38-137">The MixedRealityToolkit for Unity provides a static class that makes setting the Spatial Sound settings easy.</span></span> <span data-ttu-id="0cb38-138">Cette classe peut être trouvée dans le [MixedRealityToolkit\SpatialSound dossier](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialSound) et peut être appelée à partir de n’importe quel script dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="0cb38-138">This class can be found in the [MixedRealityToolkit\SpatialSound folder](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialSound) and can be called from any script in your project.</span></span> <span data-ttu-id="0cb38-139">Il est recommandé de définir ces paramètres sur chaque composant de Source de données Audio dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="0cb38-139">It is recommended that you set these parameters on each Audio Source component in your project.</span></span> <span data-ttu-id="0cb38-140">L’exemple suivant montre la sélection de la taille de la moyenne pour une Source Audio liée.</span><span class="sxs-lookup"><span data-stu-id="0cb38-140">The following example shows selecting the medium room size for an attached Audio Source.</span></span>

```cs
AudioSource audioSource = gameObject.GetComponent<AudioSource>()

if (audioSource != null) {
    SpatialSoundSettings.SetRoomSize(audioSource, SpatialMappingRoomSizes.Medium);
}
```

### <a name="directly-accessing-parameters-from-unity"></a><span data-ttu-id="0cb38-141">En accédant directement aux paramètres à partir d’Unity</span><span class="sxs-lookup"><span data-stu-id="0cb38-141">Directly Accessing Parameters from Unity</span></span>

<span data-ttu-id="0cb38-142">Si vous ne souhaitez pas utiliser les outils de l’Audio excellents dans la MixedRealityToolkit, voici comment vous pouvez modifier les paramètres de HRTF.</span><span class="sxs-lookup"><span data-stu-id="0cb38-142">If you don't want to use the excellent Audio tools in the MixedRealityToolkit, here is how you would change HRTF Parameters.</span></span> <span data-ttu-id="0cb38-143">Vous pouvez copier/coller cela dans un script appelé *SetHRTF.cs* que vous souhaitez attacher à chaque AudioSource HRTF.</span><span class="sxs-lookup"><span data-stu-id="0cb38-143">You can copy/paste this into a script called *SetHRTF.cs* that you will want to attach to every HRTF AudioSource.</span></span> <span data-ttu-id="0cb38-144">Il vous permet de modifier des paramètres importants pour HRTF.</span><span class="sxs-lookup"><span data-stu-id="0cb38-144">It lets you change parameters important to HRTF.</span></span>

```cs
using UnityEngine;
   using System.Collections;
   public class SetHRTF : MonoBehaviour    {
       public enum ROOMSIZE { Small, Medium, Large, None };
       public ROOMSIZE room = ROOMSIZE.Small;  // Small is regarded as the "most average"
       // defaults and docs from MSDN
       // https://msdn.microsoft.com/library/windows/desktop/mt186602(v=vs.85).aspx
       AudioSource audiosource;
       void Awake()
       {
           audiosource = this.gameObject.GetComponent<AudioSource>();
           if (audiosource == null)
           {
               print("SetHRTFParams needs an audio source to do anything.");
               return;
           }
           audiosource.spatialize = 1; // we DO want spatialized audio
           audiosource.spread = 0; // we dont want to reduce our angle of hearing
           audiosource.spatialBlend = 1;   // we do want to hear spatialized audio
           audiosource.SetSpatializerFloat(1, (float)room);    // 1 is the roomsize param
       }
   }
```
### <a name="spatial-sound-in-mixed-reality-toolkit"></a><span data-ttu-id="0cb38-145">Son spatial dans le Kit de ressources de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="0cb38-145">Spatial Sound in Mixed Reality Toolkit</span></span>
- [<span data-ttu-id="0cb38-146">HoloToolkit-Examples/SpatialSound/Scenes/UAudioManagerTest.unity</span><span class="sxs-lookup"><span data-stu-id="0cb38-146">HoloToolkit-Examples/SpatialSound/Scenes/UAudioManagerTest.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/UAudioManagerTest.unity)

<span data-ttu-id="0cb38-147">Les exemples suivants à partir de la boîte à outils de réalité mixte sont des exemples généraux effet audio qui illustrent des façons de rendre votre expérience plus riche à l’aide de son.</span><span class="sxs-lookup"><span data-stu-id="0cb38-147">The following examples from the Mixed Reality Toolkit are general audio effect examples that demonstrate ways to make your experiences more immersive by using sound.</span></span>
- [<span data-ttu-id="0cb38-148">HoloToolkit-Examples/SpatialSound/Scenes/AudioLoFiTest.unity</span><span class="sxs-lookup"><span data-stu-id="0cb38-148">HoloToolkit-Examples/SpatialSound/Scenes/AudioLoFiTest.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/AudioLoFiTest.unity)
- [<span data-ttu-id="0cb38-149">HoloToolkit-Examples/SpatialSound/Scenes/AudioOcclusionTest.unity</span><span class="sxs-lookup"><span data-stu-id="0cb38-149">HoloToolkit-Examples/SpatialSound/Scenes/AudioOcclusionTest.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/AudioOcclusionTest.unity)

## <a name="see-also"></a><span data-ttu-id="0cb38-150">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0cb38-150">See also</span></span>
* [<span data-ttu-id="0cb38-151">Son spatial</span><span class="sxs-lookup"><span data-stu-id="0cb38-151">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="0cb38-152">Sonorisation spatiale</span><span class="sxs-lookup"><span data-stu-id="0cb38-152">Spatial sound design</span></span>](spatial-sound-design.md)
