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
# <a name="using-reverb-to-add-distance-to-spatial-audio"></a>Utilisation de la réverbération pour ajouter une distance à un son spatial

## <a name="objectives"></a>Objectifs
Dans les chapitres précédents, nous avons ajouté Spatialization aux sons pour leur offrir un sens de la direction. Dans ce cinquième chapitre, nous allons ajouter un effet de réverbération pour fournir aux sons un sens de la distance. Nos objectifs sont les suivants :
* Améliorer la distance perçue des sources sonores en ajoutant une réverbération
* Contrôle de la distance perçue du son à l’aide de la distance de l’écouteur à l’hologramme

## <a name="add-a-mixer-group-and-a-reverb-effect"></a>Ajouter un groupe de mixage et un effet de réverbération
Dans le [Chapitre 2](unity-spatial-audio-ch2.md), nous avons ajouté un mélangeur. Le mélangeur comprend un **groupe** par défaut nommé **maître**. Étant donné que nous voulons uniquement appliquer un effet de réverbération à certains sons, nous allons ajouter un deuxième **groupe** pour ces sons. Pour ajouter un **groupe**, cliquez avec le bouton droit sur le groupe **principal** dans le **mélangeur audio** , puis choisissez **Ajouter un groupe enfant**:

![Ajouter un groupe enfant](images/spatial-audio/add-child-group.png)

Dans cet exemple, nous avons nommé « effet Room » pour le nouveau groupe.

Chaque **groupe** a son propre ensemble d’effets. Ajoutez un effet de réverbération au nouveau groupe en cliquant sur **Ajouter...** dans le nouveau groupe, puis en choisissant **réverbe SFX**:

![Ajouter une réverbération SFX](images/spatial-audio/add-sfx-reverb.png)

Dans la terminologie audio, le son original, unreverberated, est appelé le chemin à l' _état sec_, et l’audio après le filtrage avec le filtre de réverbération est appelé le _chemin d’accès humide_. Les deux chemins d’accès sont envoyés à la sortie audio, et leurs forces relatives dans ce mélange sont appelées la _combinaison humide/sèche_. La combinaison humide/sèche affecte fortement le sens de la distance.

Le **reverbe SFX** comprend des contrôles pour ajuster la combinaison humide/sèche dans l’effet. Étant donné que le plug-in **Microsoft Spatializer** gère le chemin d’accès à sec, nous allons utiliser la **réverbération SFX** uniquement pour le chemin d’accès humide. Dans le volet de l' **inspecteur** de votre **réverbération SFX**:
* Définir la propriété de niveau Dry sur le paramètre le plus bas (-10000 Mo)
* Définir la propriété Room sur le paramètre le plus élevé (0 Mo)

Une fois ces modifications effectuées, le volet de l' **inspecteur** du **reverbe SFX** se présente comme suit :

![Propriétés de la réverbération SFX](images/spatial-audio/sfx-reverb-properties.png)

Les autres paramètres contrôlent l’apparence de la salle simulée. En particulier, le **temps de désintégration** est lié à la taille de l’espace perçu. 

## <a name="enable-reverb-on-the-video-playback"></a>Activer la réverbération sur la lecture vidéo
Il existe deux étapes pour activer la réverbération sur une source audio :
* Acheminer la **source audio** vers le **groupe** approprié
* Définir le plug-in **Microsoft Spatializer** pour transmettre l’audio au **groupe** pour traitement

Dans les étapes suivantes, nous allons ajuster notre script pour contrôler le routage audio et attacher un script de contrôle fourni avec le plug-in **Microsoft Spatializer** pour alimenter les données dans le verbe.

Dans le volet de l' **inspecteur** pour le **Quad**, cliquez sur **Ajouter un composant** et ajoutez le script de niveau d’envoi de l’effet de **pièce** :

![Ajouter un script de niveau d’envoi](images/spatial-audio/add-send-level-script.png)

> [!NOTE]
> À moins que vous activiez la fonctionnalité de niveau d’envoi de l' **effet de salle** du plug-in **Microsoft Spatializer** , il n’envoie pas d’audio au moteur audio Unity pour le traitement de l’effet.

Le composant de niveau d’envoi de l' **effet de salle** comprend un contrôle de graphique qui définit le niveau de l’audio envoyé au moteur audio Unity pour le traitement de la réverbération. Cliquez et faites glisser la courbe vers le bas pour définir le niveau sur about-30dB :

![Ajuster la courbe de réverbération](images/spatial-audio/adjust-reverb-curve.png)

Ensuite, supprimez les marques de commentaire des 4 lignes commentées dans le script **SpatializeOnOff** . Le script ressemble maintenant à ce qui suit :
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

Si vous supprimez les commentaires de ces lignes, vous ajoutez deux propriétés au volet de l' **inspecteur** pour le script. Pour les définir, dans le volet **inspecteur** du composant **spatial on off** du **Quad**:
* Définir la propriété **groupe d’effets** de la salle sur votre nouveau groupe de mixeur d’effets d’espace
* Définir la propriété de **groupe maître** sur le groupe de mixages principaux

Une fois ces modifications effectuées, les propriétés de l’espacement **inactif** se présentent comme suit :

![Spatialiser sur OFF étendu](images/spatial-audio/spatialize-on-off-extended.png)

## <a name="next-steps"></a>Étapes suivantes

Essayez votre application sur un HoloLens 2 ou dans l’éditeur Unity. Maintenant, quand vous touchez le bouton dans l’application pour activer Spatialization, le script achemine l’audio de la vidéo vers le groupe d’effets de la pièce pour ajouter une réverbération. Lorsque vous basculez en stéréo, il achemine l’audio vers le groupe maître et évite l’ajout d’une réverbération.

Vous avez terminé les didacticiels audio spatiaux HoloLens 2 pour Unity. Félicitations !


