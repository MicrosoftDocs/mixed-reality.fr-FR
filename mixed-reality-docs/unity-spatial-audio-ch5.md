---
title: Didacticiels audio spatiaux-5. Utilisation de la réverbération pour ajouter une distance à un son spatial
description: Ajoutez un effet de réverbération pour améliorer le sens de la variation de distance avec l’audio spatial.
author: kegodin
ms.author: kegodin
ms.date: 12/01/2019
ms.topic: article
keywords: réalité mixte, Unity, tutorial, hololens2, audio spatial
ms.openlocfilehash: abe78417dc231e6228d1942e03418ba699bc0938
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75182736"
---
# <a name="using-reverb-to-add-distance-to-spatial-audio"></a><span data-ttu-id="e01e1-105">Utilisation de la réverbération pour ajouter une distance à un son spatial</span><span class="sxs-lookup"><span data-stu-id="e01e1-105">Using reverb to add distance to spatial audio</span></span>

## <a name="objectives"></a><span data-ttu-id="e01e1-106">Objectifs</span><span class="sxs-lookup"><span data-stu-id="e01e1-106">Objectives</span></span>
<span data-ttu-id="e01e1-107">Dans les chapitres précédents, nous avons ajouté Spatialization aux sons pour leur offrir un sens de la direction.</span><span class="sxs-lookup"><span data-stu-id="e01e1-107">In previous chapters, we added spatialization to sounds to give them a sense of direction.</span></span> <span data-ttu-id="e01e1-108">Dans ce cinquième chapitre, nous allons ajouter un effet de réverbération pour fournir aux sons un sens de la distance.</span><span class="sxs-lookup"><span data-stu-id="e01e1-108">In this 5th chapter, we'll add a reverb effect to give sounds a sense of distance.</span></span> <span data-ttu-id="e01e1-109">Nos objectifs sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="e01e1-109">Our objectives are to:</span></span>
* <span data-ttu-id="e01e1-110">Améliorer la distance perçue des sources sonores en ajoutant une réverbération</span><span class="sxs-lookup"><span data-stu-id="e01e1-110">Improve perceived distance of sound sources by adding reverb</span></span>
* <span data-ttu-id="e01e1-111">Contrôle de la distance perçue du son à l’aide de la distance de l’écouteur à l’hologramme</span><span class="sxs-lookup"><span data-stu-id="e01e1-111">Control perceived distance of the sound using the listener's distance to the hologram</span></span>

## <a name="add-a-mixer-group-and-a-reverb-effect"></a><span data-ttu-id="e01e1-112">Ajouter un groupe de mixage et un effet de réverbération</span><span class="sxs-lookup"><span data-stu-id="e01e1-112">Add a mixer group and a reverb effect</span></span>
<span data-ttu-id="e01e1-113">Dans le [Chapitre 2](unity-spatial-audio-ch2.md), nous avons ajouté un mélangeur.</span><span class="sxs-lookup"><span data-stu-id="e01e1-113">In [Chapter 2](unity-spatial-audio-ch2.md), we added a mixer.</span></span> <span data-ttu-id="e01e1-114">Le mélangeur comprend un **groupe** par défaut nommé **maître**.</span><span class="sxs-lookup"><span data-stu-id="e01e1-114">The mixer includes one **Group** by default called **Master**.</span></span> <span data-ttu-id="e01e1-115">Étant donné que nous voulons uniquement appliquer un effet de réverbération à certains sons, nous allons ajouter un deuxième **groupe** pour ces sons.</span><span class="sxs-lookup"><span data-stu-id="e01e1-115">Because we'll only want to apply a reverb effect to some sounds, let's add a second **Group** for those sounds.</span></span> <span data-ttu-id="e01e1-116">Pour ajouter un **groupe**, cliquez avec le bouton droit sur le groupe **principal** dans le **mélangeur audio** , puis choisissez **Ajouter un groupe enfant**:</span><span class="sxs-lookup"><span data-stu-id="e01e1-116">To add a **Group**, right click on the **Master** group in the **Audio Mixer** and choose **Add child group**:</span></span>

![Ajouter un groupe enfant](images/spatial-audio/add-child-group.png)

<span data-ttu-id="e01e1-118">Dans cet exemple, nous avons nommé « effet Room » pour le nouveau groupe.</span><span class="sxs-lookup"><span data-stu-id="e01e1-118">In this example, we've named the new group "Room Effect".</span></span>

<span data-ttu-id="e01e1-119">Chaque **groupe** a son propre ensemble d’effets.</span><span class="sxs-lookup"><span data-stu-id="e01e1-119">Each **Group** has its own set of effects.</span></span> <span data-ttu-id="e01e1-120">Ajoutez un effet de réverbération au nouveau groupe en cliquant sur **Ajouter...** dans le nouveau groupe, puis en choisissant **réverbe SFX**:</span><span class="sxs-lookup"><span data-stu-id="e01e1-120">Add a reverb effect to the new group by clicking **Add...** on the new group, and choosing **SFX Reverb**:</span></span>

![Ajouter une réverbération SFX](images/spatial-audio/add-sfx-reverb.png)

<span data-ttu-id="e01e1-122">Dans la terminologie audio, le son original, unreverberated, est appelé le chemin à l' _état sec_, et l’audio après le filtrage avec le filtre de réverbération est appelé le _chemin d’accès humide_.</span><span class="sxs-lookup"><span data-stu-id="e01e1-122">In audio terminology, the original, unreverberated audio is called the _dry path_, and the audio after filtering with the reverb filter is called the _wet path_.</span></span> <span data-ttu-id="e01e1-123">Les deux chemins d’accès sont envoyés à la sortie audio, et leurs forces relatives dans ce mélange sont appelées la _combinaison humide/sèche_.</span><span class="sxs-lookup"><span data-stu-id="e01e1-123">Both paths are sent to the audio output, and their relative strengths in this mixture is called the _wet/dry mix_.</span></span> <span data-ttu-id="e01e1-124">La combinaison humide/sèche affecte fortement le sens de la distance.</span><span class="sxs-lookup"><span data-stu-id="e01e1-124">The wet/dry mix strongly affects the sense of distance.</span></span>

<span data-ttu-id="e01e1-125">Le **reverbe SFX** comprend des contrôles pour ajuster la combinaison humide/sèche dans l’effet.</span><span class="sxs-lookup"><span data-stu-id="e01e1-125">The **SFX Reverb** includes controls to adjust the wet/dry mix within the effect.</span></span> <span data-ttu-id="e01e1-126">Étant donné que le plug-in **Microsoft Spatializer** gère le chemin d’accès à sec, nous allons utiliser la **réverbération SFX** uniquement pour le chemin d’accès humide.</span><span class="sxs-lookup"><span data-stu-id="e01e1-126">Because the **Microsoft Spatializer** plugin handles the dry path, we'll be using the **SFX Reverb** only for the wet path.</span></span> <span data-ttu-id="e01e1-127">Dans le volet de l' **inspecteur** de votre **réverbération SFX**:</span><span class="sxs-lookup"><span data-stu-id="e01e1-127">On the **Inspector** pane of your **SFX Reverb**:</span></span>
* <span data-ttu-id="e01e1-128">Définir la propriété de niveau Dry sur le paramètre le plus bas (-10000 Mo)</span><span class="sxs-lookup"><span data-stu-id="e01e1-128">Set the Dry Level property to the lowest setting (-10000 mB)</span></span>
* <span data-ttu-id="e01e1-129">Définir la propriété Room sur le paramètre le plus élevé (0 Mo)</span><span class="sxs-lookup"><span data-stu-id="e01e1-129">Set the Room property to the highest setting (0 mB)</span></span>

<span data-ttu-id="e01e1-130">Une fois ces modifications effectuées, le volet de l' **inspecteur** du **reverbe SFX** se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="e01e1-130">After these changes, the **Inspector** pane of the **SFX Reverb** will look like this:</span></span>

![Propriétés de la réverbération SFX](images/spatial-audio/sfx-reverb-properties.png)

<span data-ttu-id="e01e1-132">Les autres paramètres contrôlent l’apparence de la salle simulée.</span><span class="sxs-lookup"><span data-stu-id="e01e1-132">The other settings control the feel of the simulated room.</span></span> <span data-ttu-id="e01e1-133">En particulier, le **temps de désintégration** est lié à la taille de l’espace perçu.</span><span class="sxs-lookup"><span data-stu-id="e01e1-133">In particular, **Decay Time** is related to perceived room size.</span></span> 

## <a name="enable-reverb-on-the-video-playback"></a><span data-ttu-id="e01e1-134">Activer la réverbération sur la lecture vidéo</span><span class="sxs-lookup"><span data-stu-id="e01e1-134">Enable reverb on the video playback</span></span>
<span data-ttu-id="e01e1-135">Il existe deux étapes pour activer la réverbération sur une source audio :</span><span class="sxs-lookup"><span data-stu-id="e01e1-135">There are two steps to enable reverb on an audio source:</span></span>
* <span data-ttu-id="e01e1-136">Acheminer la **source audio** vers le **groupe** approprié</span><span class="sxs-lookup"><span data-stu-id="e01e1-136">Route the **Audio Source** to the appropriate **Group**</span></span>
* <span data-ttu-id="e01e1-137">Définir le plug-in **Microsoft Spatializer** pour transmettre l’audio au **groupe** pour traitement</span><span class="sxs-lookup"><span data-stu-id="e01e1-137">Set the **Microsoft Spatializer** plugin to pass audio into the **Group** for processing</span></span>

<span data-ttu-id="e01e1-138">Dans les étapes suivantes, nous allons ajuster notre script pour contrôler le routage audio et attacher un script de contrôle fourni avec le plug-in **Microsoft Spatializer** pour alimenter les données dans le verbe.</span><span class="sxs-lookup"><span data-stu-id="e01e1-138">In the following steps, we'll adjust our script to control the audio routing, and attach a control script provided with the **Microsoft Spatializer** plugin to feed data into the reverb.</span></span>

<span data-ttu-id="e01e1-139">Dans le volet de l' **inspecteur** pour le **Quad**, cliquez sur **Ajouter un composant** et ajoutez le script de niveau d’envoi de l’effet de **pièce** :</span><span class="sxs-lookup"><span data-stu-id="e01e1-139">On the **Inspector** pane for the **Quad**, click **Add Component** and add the **Room Effect Send Level** script:</span></span>

![Ajouter un script de niveau d’envoi](images/spatial-audio/add-send-level-script.png)

> [!NOTE]
> <span data-ttu-id="e01e1-141">À moins que vous activiez la fonctionnalité de niveau d’envoi de l' **effet de salle** du plug-in **Microsoft Spatializer** , il n’envoie pas d’audio au moteur audio Unity pour le traitement de l’effet.</span><span class="sxs-lookup"><span data-stu-id="e01e1-141">Unless you enable **Room Effect Send Level** feature of the **Microsoft Spatializer** plugin, it doesn't send any audio back to the Unity audio engine for effect processing.</span></span>

<span data-ttu-id="e01e1-142">Le composant de niveau d’envoi de l' **effet de salle** comprend un contrôle de graphique qui définit le niveau de l’audio envoyé au moteur audio Unity pour le traitement de la réverbération.</span><span class="sxs-lookup"><span data-stu-id="e01e1-142">The **Room Effect Send Level** component includes a graph control that sets the level of the audio sent to the Unity audio engine for reverb processing.</span></span> <span data-ttu-id="e01e1-143">Cliquez et faites glisser la courbe vers le bas pour définir le niveau sur about-30dB :</span><span class="sxs-lookup"><span data-stu-id="e01e1-143">Click and drag the curve downwards to set the level to about -30dB:</span></span>

![Ajuster la courbe de réverbération](images/spatial-audio/adjust-reverb-curve.png)

<span data-ttu-id="e01e1-145">Ensuite, supprimez les marques de commentaire des 4 lignes commentées dans le script **SpatializeOnOff** .</span><span class="sxs-lookup"><span data-stu-id="e01e1-145">Next, uncomment the 4 commented lines in the **SpatializeOnOff** script.</span></span> <span data-ttu-id="e01e1-146">Le script ressemble maintenant à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="e01e1-146">The script will now look like this:</span></span>
```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Audio;

[RequireComponent(typeof(AudioSource))]
public class SpatializeOnOff : MonoBehaviour
{
    public GameObject ButtonTextObject;
    public AudioMixerGroup RoomEffectGroup;
    public AudioMixerGroup MasterGroup;

    private AudioSource m_SourceObject;
    private bool m_IsSpatialized;
    private TMPro.TextMeshPro m_TextMeshPro;

    public void Start()
    {
        m_SourceObject = gameObject.GetComponent<AudioSource>();
        m_TextMeshPro = ButtonTextObject.GetComponent<TMPro.TextMeshPro>();
        SetSpatialized();
    }

    public void SwapSpatialization()
    {
        if (m_IsSpatialized)
        {
            SetStereo();
        }
        else
        {
            SetSpatialized();
        }
    }

    private void SetSpatialized()
    {
        m_IsSpatialized = true;
        m_SourceObject.spatialBlend = 1;
        m_TextMeshPro.SetText("Set Stereo");
        m_SourceObject.outputAudioMixerGroup = RoomEffectGroup;
    }

    private void SetStereo()
    {
        m_IsSpatialized = false;
        m_SourceObject.spatialBlend = 0;
        m_TextMeshPro.SetText("Set Spatialized");
        m_SourceObject.outputAudioMixerGroup = MasterGroup;
    }

}
```

<span data-ttu-id="e01e1-147">Si vous supprimez les commentaires de ces lignes, vous ajoutez deux propriétés au volet de l' **inspecteur** pour le script.</span><span class="sxs-lookup"><span data-stu-id="e01e1-147">Uncommenting these lines adds two properties to the **Inspector** pane for the script.</span></span> <span data-ttu-id="e01e1-148">Pour les définir, dans le volet **inspecteur** du composant **spatial on off** du **Quad**:</span><span class="sxs-lookup"><span data-stu-id="e01e1-148">To set these, on the **Inspector** pane of the **Spatialize On Off** component of the **Quad**:</span></span>
* <span data-ttu-id="e01e1-149">Définir la propriété **groupe d’effets** de la salle sur votre nouveau groupe de mixeur d’effets d’espace</span><span class="sxs-lookup"><span data-stu-id="e01e1-149">Set the **Room Effect Group** property to your new Room Effect mixer group</span></span>
* <span data-ttu-id="e01e1-150">Définir la propriété de **groupe maître** sur le groupe de mixages principaux</span><span class="sxs-lookup"><span data-stu-id="e01e1-150">Set the **Master Group** property to the Master mixer group</span></span>

<span data-ttu-id="e01e1-151">Une fois ces modifications effectuées, les propriétés de l’espacement **inactif** se présentent comme suit :</span><span class="sxs-lookup"><span data-stu-id="e01e1-151">After these changes, the **Spatialize On Off** properties will look like this:</span></span>

![Spatialiser sur OFF étendu](images/spatial-audio/spatialize-on-off-extended.png)

## <a name="next-steps"></a><span data-ttu-id="e01e1-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e01e1-153">Next steps</span></span>

<span data-ttu-id="e01e1-154">Essayez votre application sur un HoloLens 2 ou dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="e01e1-154">Try out your app on a HoloLens 2 or in the Unity editor.</span></span> <span data-ttu-id="e01e1-155">Maintenant, quand vous touchez le bouton dans l’application pour activer Spatialization, le script achemine l’audio de la vidéo vers le groupe d’effets de la pièce pour ajouter une réverbération.</span><span class="sxs-lookup"><span data-stu-id="e01e1-155">Now, when touching the button in the app to activate spatialization, the script will route the video's audio to the Room Effect Group to add reverb.</span></span> <span data-ttu-id="e01e1-156">Lorsque vous basculez en stéréo, il achemine l’audio vers le groupe maître et évite l’ajout d’une réverbération.</span><span class="sxs-lookup"><span data-stu-id="e01e1-156">When switching to stereo, it will route the audio to the Master group, and avoid adding reverb.</span></span>

<span data-ttu-id="e01e1-157">Vous avez terminé les didacticiels audio spatiaux HoloLens 2 pour Unity.</span><span class="sxs-lookup"><span data-stu-id="e01e1-157">You've completed the HoloLens 2 spatial audio tutorials for Unity.</span></span> <span data-ttu-id="e01e1-158">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="e01e1-158">Congratulations!</span></span>


