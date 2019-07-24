---
title: Son spatial dans Unity
description: Lit le son spatial qui provient d’un point 3D spécifique dans votre scène Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, son spatial, HRTF, taille de la salle
ms.openlocfilehash: e2b321d7086314a14a940d57aa17e67636c758b8
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63549080"
---
# <a name="spatial-sound-in-unity"></a><span data-ttu-id="02a05-104">Son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="02a05-104">Spatial sound in Unity</span></span>

<span data-ttu-id="02a05-105">Cette rubrique explique comment utiliser un son spatial dans vos projets Unity.</span><span class="sxs-lookup"><span data-stu-id="02a05-105">This topic describes how to use Spatial Sound in your Unity projects.</span></span> <span data-ttu-id="02a05-106">Il couvre les fichiers de plug-in requis, ainsi que les composants et les propriétés Unity qui permettent le son spatial.</span><span class="sxs-lookup"><span data-stu-id="02a05-106">It covers the required plugin files as well as the Unity components and properties that enable Spatial Sound.</span></span>

## <a name="enabling-spatial-sound-in-unity"></a><span data-ttu-id="02a05-107">Activation du son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="02a05-107">Enabling Spatial Sound in Unity</span></span>

<span data-ttu-id="02a05-108">Le son spatial, dans Unity, est activé à l’aide d’un plug-in audio Spatializer.</span><span class="sxs-lookup"><span data-stu-id="02a05-108">Spatial Sound, in Unity, is enabled using an audio spatializer plugin.</span></span> <span data-ttu-id="02a05-109">Les fichiers de plug-in sont regroupés directement dans Unity, de sorte que l’activation du son spatial est aussi facile que la **modification > paramètres du projet > l’audio** et la modification du **plug-in Spatializer** dans l’inspecteur par le **Spatializer MS HRTF**.</span><span class="sxs-lookup"><span data-stu-id="02a05-109">The plugin files are bundled directly into Unity so enabling spatial sound is as easy as going to **Edit > Project Settings > Audio** and changing the **Spatializer Plugin** in the Inspector to the **MS HRTF Spatializer**.</span></span> <span data-ttu-id="02a05-110">Étant donné que Microsoft Spatializer prend uniquement en charge 48000Hz, vous devez également définir le taux d’échantillonnage du système sur 48000 pour éviter un échec HRTF dans le cas rare où votre périphérique de sortie système n’est pas déjà défini sur 48000:</span><span class="sxs-lookup"><span data-stu-id="02a05-110">Since the Microsoft spatializer only supports 48000Hz currently, you should also set your System Sample Rate to 48000 to prevent an HRTF failure in the rare case that your system output device is not set to 48000 already:</span></span>

<span data-ttu-id="02a05-111">![Inspector pour AudioManager](images/audio-250px.png)</span><span class="sxs-lookup"><span data-stu-id="02a05-111">![Inspector for AudioManager](images/audio-250px.png)</span></span><br>
<span data-ttu-id="02a05-112">*Inspector pour AudioManager*</span><span class="sxs-lookup"><span data-stu-id="02a05-112">*Inspector for AudioManager*</span></span>

<span data-ttu-id="02a05-113">Votre projet Unity est maintenant configuré pour utiliser un son spatial.</span><span class="sxs-lookup"><span data-stu-id="02a05-113">Your Unity project is now configured to use Spatial Sound.</span></span>

>[!NOTE]
><span data-ttu-id="02a05-114">Si vous n’utilisez pas un PC Windows 10 pour le développement, vous n’obtiendrez pas de son spatial dans l’éditeur ni sur l’appareil (même si vous utilisez le kit de développement logiciel (SDK) Windows 10).</span><span class="sxs-lookup"><span data-stu-id="02a05-114">If you aren't using a Windows 10 PC for development, you won't get Spatial Sound in the editor nor on the device (even if you're using the Windows 10 SDK).</span></span>

## <a name="using-spatial-sound-in-unity"></a><span data-ttu-id="02a05-115">Utilisation du son spatial dans Unity</span><span class="sxs-lookup"><span data-stu-id="02a05-115">Using Spatial Sound in Unity</span></span>

<span data-ttu-id="02a05-116">Le son spatial est utilisé dans votre projet Unity en ajustant trois paramètres sur vos composants sources audio.</span><span class="sxs-lookup"><span data-stu-id="02a05-116">Spatial Sound is used in your Unity project by adjusting three settings on your Audio Source components.</span></span> <span data-ttu-id="02a05-117">Les étapes suivantes vous permettront de configurer vos composants de source audio pour le son spatial.</span><span class="sxs-lookup"><span data-stu-id="02a05-117">The following steps will configure your Audio Source components for Spatial Sound.</span></span>
* <span data-ttu-id="02a05-118">Dans le panneau **hiérarchie** , sélectionnez l’objet de jeu qui a une **source audio**attachée.</span><span class="sxs-lookup"><span data-stu-id="02a05-118">In the **Hierarchy** panel, select the game object that has an attached **Audio Source**.</span></span>
* <span data-ttu-id="02a05-119">Dans le panneau **inspecteur** , sous le composant **audio source**</span><span class="sxs-lookup"><span data-stu-id="02a05-119">In the **Inspector** panel, under the **Audio Source** component</span></span>
    * <span data-ttu-id="02a05-120">Vérifiez l’option **spatial** .</span><span class="sxs-lookup"><span data-stu-id="02a05-120">Check the **Spatialize** option.</span></span>
    * <span data-ttu-id="02a05-121">Définissez **spatial Blend** sur **3D** (valeur numérique 1).</span><span class="sxs-lookup"><span data-stu-id="02a05-121">Set **Spatial Blend** to **3D** (numeric value 1).</span></span>
    * <span data-ttu-id="02a05-122">Pour de meilleurs résultats, développez **paramètres audio 3D** et définissez **volume Rolloff** sur **personnalisé Rolloff**.</span><span class="sxs-lookup"><span data-stu-id="02a05-122">For best results, expand **3D Sound Settings** and set **Volume Rolloff** to **Custom Rolloff**.</span></span>

<span data-ttu-id="02a05-123">![Panneau de l’inspecteur dans Unity présentant la source audio](images/audiosource.png)</span><span class="sxs-lookup"><span data-stu-id="02a05-123">![Inspector panel in Unity showing the Audio Source](images/audiosource.png)</span></span><br>
<span data-ttu-id="02a05-124">*Panneau de l’inspecteur dans Unity présentant la source audio*</span><span class="sxs-lookup"><span data-stu-id="02a05-124">*Inspector panel in Unity showing the Audio Source*</span></span>

<span data-ttu-id="02a05-125">Vos sons sont désormais réalistes dans l’environnement de votre projet.</span><span class="sxs-lookup"><span data-stu-id="02a05-125">Your sounds now realistically exist inside your project's environment!</span></span>

<span data-ttu-id="02a05-126">Il est fortement recommandé de vous familiariser avec les [instructions de conception de son spatial](spatial-sound-design.md).</span><span class="sxs-lookup"><span data-stu-id="02a05-126">It is strongly recommended that you become familiar with the [Spatial Sound design guidelines](spatial-sound-design.md).</span></span> <span data-ttu-id="02a05-127">Ces instructions vous aident à intégrer votre audio en toute transparence dans votre projet et à plonger vos utilisateurs dans l’expérience que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="02a05-127">These guidelines help to integrate your audio seamlessly into your project and to further immerse your users into the experience you have created.</span></span>

## <a name="setting-spatial-sound-settings"></a><span data-ttu-id="02a05-128">Définition des paramètres de son spatial</span><span class="sxs-lookup"><span data-stu-id="02a05-128">Setting Spatial Sound Settings</span></span>

<span data-ttu-id="02a05-129">Le plug-in de son spatial Microsoft fournit un paramètre supplémentaire qui peut être défini, en fonction de la source audio, pour permettre un contrôle supplémentaire de la simulation audio.</span><span class="sxs-lookup"><span data-stu-id="02a05-129">The Microsoft Spatial Sound plugin provides an additional parameter that can be set, on a per Audio Source basis, to allow additional control of the audio simulation.</span></span> <span data-ttu-id="02a05-130">Ce paramètre correspond à la taille de la salle simulée.</span><span class="sxs-lookup"><span data-stu-id="02a05-130">This parameter is the size of the simulated room.</span></span>

### <a name="room-size"></a><span data-ttu-id="02a05-131">Taille de la salle</span><span class="sxs-lookup"><span data-stu-id="02a05-131">Room Size</span></span>

<span data-ttu-id="02a05-132">Taille de la salle qui est simulée par son spatial.</span><span class="sxs-lookup"><span data-stu-id="02a05-132">The size of room that is being simulated by Spatial Sound.</span></span> <span data-ttu-id="02a05-133">La taille approximative des salles est; petite (un bureau à une petite salle de conférence), moyen (une grande salle de conférence) et grand (un auditorium).</span><span class="sxs-lookup"><span data-stu-id="02a05-133">The approximate sizes of the rooms are; small (an office to a small conference room), medium (a large conference room) and large (an auditorium).</span></span> <span data-ttu-id="02a05-134">Vous pouvez également spécifier une taille de salle nulle pour simuler un environnement extérieur.</span><span class="sxs-lookup"><span data-stu-id="02a05-134">You can also specify a room size of none to simulate an outdoor environment.</span></span> <span data-ttu-id="02a05-135">La taille de la salle par défaut est petite.</span><span class="sxs-lookup"><span data-stu-id="02a05-135">The default room size is small.</span></span>

### <a name="example"></a><span data-ttu-id="02a05-136">Exemple</span><span class="sxs-lookup"><span data-stu-id="02a05-136">Example</span></span>

<span data-ttu-id="02a05-137">Le MixedRealityToolkit pour Unity fournit une classe statique qui facilite la définition des paramètres de son spatial.</span><span class="sxs-lookup"><span data-stu-id="02a05-137">The MixedRealityToolkit for Unity provides a static class that makes setting the Spatial Sound settings easy.</span></span> <span data-ttu-id="02a05-138">Cette classe se trouve dans le [dossier MixedRealityToolkit\SpatialSound](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialSound) et peut être appelée à partir de n’importe quel script de votre projet.</span><span class="sxs-lookup"><span data-stu-id="02a05-138">This class can be found in the [MixedRealityToolkit\SpatialSound folder](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/SpatialSound) and can be called from any script in your project.</span></span> <span data-ttu-id="02a05-139">Il est recommandé de définir ces paramètres sur chaque composant de la source audio dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="02a05-139">It is recommended that you set these parameters on each Audio Source component in your project.</span></span> <span data-ttu-id="02a05-140">L’exemple suivant illustre la sélection de la taille de la salle moyenne pour une source audio attachée.</span><span class="sxs-lookup"><span data-stu-id="02a05-140">The following example shows selecting the medium room size for an attached Audio Source.</span></span>

```cs
AudioSource audioSource = gameObject.GetComponent<AudioSource>()

if (audioSource != null) {
    SpatialSoundSettings.SetRoomSize(audioSource, SpatialMappingRoomSizes.Medium);
}
```

### <a name="directly-accessing-parameters-from-unity"></a><span data-ttu-id="02a05-141">Accès direct aux paramètres d’Unity</span><span class="sxs-lookup"><span data-stu-id="02a05-141">Directly Accessing Parameters from Unity</span></span>

<span data-ttu-id="02a05-142">Si vous ne souhaitez pas utiliser les excellents outils audio dans le MixedRealityToolkit, voici comment modifier les paramètres HRTF.</span><span class="sxs-lookup"><span data-stu-id="02a05-142">If you don't want to use the excellent Audio tools in the MixedRealityToolkit, here is how you would change HRTF Parameters.</span></span> <span data-ttu-id="02a05-143">Vous pouvez le copier/coller dans un script appelé *SetHRTF.cs* que vous souhaitez attacher à chaque audiosource HRTF.</span><span class="sxs-lookup"><span data-stu-id="02a05-143">You can copy/paste this into a script called *SetHRTF.cs* that you will want to attach to every HRTF AudioSource.</span></span> <span data-ttu-id="02a05-144">Elle vous permet de modifier les paramètres importants en HRTF.</span><span class="sxs-lookup"><span data-stu-id="02a05-144">It lets you change parameters important to HRTF.</span></span>

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
### <a name="spatial-sound-in-mixed-reality-toolkit"></a><span data-ttu-id="02a05-145">Son spatial dans la réalité mixte Toolkit</span><span class="sxs-lookup"><span data-stu-id="02a05-145">Spatial Sound in Mixed Reality Toolkit</span></span>
- [<span data-ttu-id="02a05-146">HoloToolkit-Examples/SpatialSound/scenes/UAudioManagerTest. Unity</span><span class="sxs-lookup"><span data-stu-id="02a05-146">HoloToolkit-Examples/SpatialSound/Scenes/UAudioManagerTest.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/UAudioManagerTest.unity)

<span data-ttu-id="02a05-147">Les exemples suivants de la boîte à outils de la réalité mixte sont des exemples d’effets audio généraux qui montrent comment rendre votre expérience plus immersive en utilisant le son.</span><span class="sxs-lookup"><span data-stu-id="02a05-147">The following examples from the Mixed Reality Toolkit are general audio effect examples that demonstrate ways to make your experiences more immersive by using sound.</span></span>
- [<span data-ttu-id="02a05-148">HoloToolkit-Examples/SpatialSound/scenes/AudioLoFiTest. Unity</span><span class="sxs-lookup"><span data-stu-id="02a05-148">HoloToolkit-Examples/SpatialSound/Scenes/AudioLoFiTest.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/AudioLoFiTest.unity)
- [<span data-ttu-id="02a05-149">HoloToolkit-Examples/SpatialSound/scenes/AudioOcclusionTest. Unity</span><span class="sxs-lookup"><span data-stu-id="02a05-149">HoloToolkit-Examples/SpatialSound/Scenes/AudioOcclusionTest.unity</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpatialSound/Scenes/AudioOcclusionTest.unity)

## <a name="see-also"></a><span data-ttu-id="02a05-150">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="02a05-150">See also</span></span>
* [<span data-ttu-id="02a05-151">Son spatial</span><span class="sxs-lookup"><span data-stu-id="02a05-151">Spatial sound</span></span>](spatial-sound.md)
* [<span data-ttu-id="02a05-152">Conception du son spatial</span><span class="sxs-lookup"><span data-stu-id="02a05-152">Spatial sound design</span></span>](spatial-sound-design.md)
