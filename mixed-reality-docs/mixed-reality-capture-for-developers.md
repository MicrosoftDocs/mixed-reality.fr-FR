---
title: Mixte de capture de la réalité pour les développeurs
description: Meilleures pratiques pour la réalité mixte de capture pour les développeurs.
author: mattzmsft
ms.author: mazeller
ms.date: 02/24/2019
ms.topic: article
keywords: mrc, photo, video, capture, camera
ms.openlocfilehash: c2d98baf16b2ea724247224aabadc1e2ca533ec1
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594007"
---
# <a name="mixed-reality-capture-for-developers"></a>Mixte de capture de la réalité pour les développeurs

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes). 

Consultez [l’activation de cette option dans votre application](#enabling-mrc-in-your-app) ci-dessous pour obtenir des conseils sur une nouvelle fonctionnalité MRC pour HoloLens 2.

Dans la mesure où un utilisateur peut prendre un [mixte de capture de la réalité](mixed-reality-capture.md) photo (MRC) ou de vidéo à tout moment, il existe quelques points que vous devez garder à l’esprit lorsque vous développez votre application. Cela inclut les meilleures pratiques pour la qualité visuelle MRC et être réactive aux modifications du système tout en les CMR sont capturées.

Les développeurs peuvent intégrer également de façon transparente de capture de réalité mixte et de l’insertion dans leurs applications.

Cette option sur HoloLens (première génération) prend en charge les vidéos et vos photos jusqu'à 720p, tandis que MRC sur HoloLens 2 prend en charge une vidéos jusqu'à 1080p et photos jusqu'à résolution 4 K.

## <a name="the-importance-of-quality-mrc"></a>L’importance de la qualité MRC

Réalité mixte capturées photos et vidéos sont probablement la première exposition à qu'un utilisateur aura de votre application. Si vous en tant que des captures d’écran de réalité mixte sur votre page de Microsoft Store ou à partir d’autres utilisateurs qui partagent les CMR sur les réseaux sociaux. Vous pouvez utiliser cette option pour votre application de démonstration, de former les utilisateurs, d’encourager les utilisateurs à partager leurs interactions world mixte et à la recherche de l’utilisateur et de la résolution des problèmes.

## <a name="how-mrc-impacts-your-app"></a>Comment MRC a un impact sur votre application

### <a name="enabling-mrc-in-your-app"></a>L’activation de cette option dans votre application

Par défaut, une application n’a pas rien à faire pour permettre aux utilisateurs de prendre des captures de réalité mixte. Toutefois, étant donné que la conception de HoloLens 2 augmente la distance entre l’appareil photo photo/vidéo (PV) et l’affichage, nous proposerons une nouvelle option pour produire un rendu de caméra 3e aligné sur l’appareil photo PV de **HoloLens 2**. 

Désactivation de caméra 3e restituer sur HoloLens 2 offre les améliorations suivantes sur l’expérience de cette option par défaut :
* Alignement hologramme à votre environnement physique et les mains (pour les interactions quasiment) doit être précise à tous les distances, au lieu d’avoir un décalage de distance autre que le [concentrer point](focus-point-in-unity.md) comme vous pouvez voir dans la valeur par défaut de cette option.
* Le œil droit dans le casque ne seront pas compromise, car il n’est utilisé pour restituer les hologrammes pour la sortie de cette option.

### <a name="disabling-mrc-in-your-app"></a>La désactivation de cette option dans votre application

Lorsqu’une application 2D utilise [DXGI_PRESENT_RESTRICT_TO_OUTPUT](https://msdn.microsoft.com/library/windows/desktop/bb509554(v=vs.85).aspx) ou [DXGI_SWAP_CHAIN_FLAG_HW_PROTECTED](https://msdn.microsoft.com/library/windows/desktop/bb173076(v=vs.85).aspx) pour afficher le contenu protégé avec une chaîne de permutation correctement configurée, sera contenu visuel de l’application masquées automatiquement pendant l’exécution de capture de réalité mixte.

### <a name="knowing-when-mrc-is-active"></a>Savoir quand cette option est active

Le [AppCapture](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.appcapture.aspx) classe peut être utilisée par une application de savoir quand système mixte de capture de la réalité est en cours d’exécution (pour le contenu audio ou vidéo).

>[!NOTE]
>De AppCapture [GetForCurrentView](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.appcapture.getforcurrentview.aspx) API peut retourner null si la capture de la réalité de mixte n’est pas disponible sur l’appareil. Il est également important de l’événement CapturingChanged quand votre application est suspendue annuler l’inscription, sinon MRC peut passer à un état bloqué.

### <a name="best-practices-hololens-specific"></a>Meilleures pratiques (HoloLens spécifique)

Cette option est censée fonctionner sans travail supplémentaire des développeurs, mais il existe quelques éléments à connaître pour fournir une expérience mieux la réalité mixte capture de votre application.

**MRC utilise le canal alpha de l’hologramme pour fusionner avec le [caméra](locatable-camera.md) IMAGERIE**

L’étape la plus importante est de s’assurer que les traces en vidant le noir transparent au lieu d’effacement sur noir opaque à votre application. Dans Unity, cela s’effectue par défaut avec le MixedRealityToolkit, mais si vous développez dans non Unity, vous devrez peut-être modifier un ligne par ligne.

Voici les artefacts que vous pouvez voir dans cette option si votre application n’est pas effacer le noir transparent à :

**Échecs de l’exemple**: Noir bords autour du contenu (le basculement effacer le noir transparent à)

<table>
<tr>
<td>
<img src="images/chessboardblackedges-300px.jpg" alt="Failing to clear to transparent black: black edge artifacts around holograms"/>
</td>
<td>
<img src="images/fieldblackedges-300px.jpg" alt="Failing to clear to transparent black: black edge artifacts around holograms"/>
</td>
</tr>
</table>

**Échecs de l’exemple**: La scène de l’ensemble de l’arrière-plan de l’hologramme s’affiche en noire. La valeur alpha d’arrière-plan 1 résultats dans un arrière-plan noir

![La valeur alpha d’arrière-plan 1 résultats dans un arrière-plan noir](images/clearopaqueblack-300px.png)

**Résultat attendu**: Hologrammes apparaissent correctement combinées avec le monde réel (résultat attendu si l’effacement à noir transparent)

![Résultat attendu si l’effacement à noir transparent](images/cleartransparentblack-300px.png)

**Solution** :
* Modifiez le contenu qui ne s’affiche en noir opaque pour avoir une valeur alpha de 0.
* Assurez-vous que l’application en vidant le noir transparent à.
* Valeurs par défaut de Unity pour effacer pour effacer automatiquement avec le MixedRealityToolkit, mais si elle est une application non Unity que vous devez modifier la couleur utilisée avec ID3D11DeiceContext::ClearRenderTargetView(). Vous souhaitez garantir que vous désactivez à noir transparent (0,0,0,0) au lieu de noir opaque (0,0,0,1).

Vous pouvez désormais paramétrer les valeurs alphabétiques de vos ressources si vous souhaitez, mais en général, n’avez pas besoin. La plupart du temps, les CMR apparaîtront correctement prêts à l’emploi. Cette option suppose alpha prémultiplié. Les valeurs alphabétiques n’affectent que la capture de cette option.

### <a name="what-to-expect-when-mrc-is-enabled-on-hololens"></a>À quoi s’attendre lorsque cette option est activée sur HoloLens

Les éléments suivants s’appliquent aux HoloLens (première génération) et 2 HoloLens, sauf indication contraire :

* Le système limite l’application au rendu de 30Hz. Cette opération crée pour cette option exécuter afin de l’application n’a pas besoin de conserver une réserve de budget constante certains accueillir et correspond également à la fréquence d’images vidéo enregistrement MRC de 30 i/s
* HOLOGRAMME contenu dans les yeux de droite de l’appareil peut apparaître « sparkle » lors de l’enregistrement/la diffusion en continu MRC : texte peut devenir plus difficile à lire et les bords hologramme peuvent apparaître plus dentelés (désactivation de caméra 3e restituer sur **HoloLens 2** évite Ce compromis)
* MRC photos et vidéos respecte l’application [concentrer point](focus-point-in-unity.md) si l’application a activé, ce qui permet de s’assurer hologrammes sont positionnés avec précision. Pour les vidéos, le Point de Focus est lissé donc vntana peut sembler lente dérive en place si la profondeur de Point de Focus change de façon significative. Hologrammes situés à des profondeurs différents à partir du point de focus peuvent s’afficher décalage dans le monde réel (voir l’exemple ci-dessous où le Point de Focus est défini à 2 mètres mais hologramme est positionné sur 1 mètre).

![Hologrammes à 2 mètres apparaîtra parfaitement inscrits au monde. Hologrammes à fermer ou lointain distances peuvent décaler légèrement.](images/hologramaccuracydistancemrc-1000px.png)

## <a name="integrating-mrc-functionality-from-within-your-app"></a>L’intégration de fonctionnalités MRC à partir de votre application

Votre application de réalité mixte peut initier des photos MRC ou capture vidéo à partir de l’application, et le contenu capturé est accessible à votre application sans être stockées à le d’appareil « pellicule. » Vous pouvez créer un enregistreur MRC personnalisé ou tirer parti de l’interface utilisateur de capture photo intégré. 

### <a name="mrc-with-built-in-camera-ui"></a>OPTION avec l’interface utilisateur de photo intégré

Les développeurs peuvent utiliser le *[API de l’interface utilisateur de Capture photo](https://docs.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-cameracaptureui)* pour obtenir une photo de l’utilisateur capturées de réalité mixte ou une vidéo avec seulement quelques lignes de code.

Cette API lance la caméra MRC intégrée l’interface utilisateur, à partir duquel l’utilisateur peut prendre une photo ou vidéo et renvoie la capture résultant à votre application.  Si vous souhaitez créer votre propre interface utilisateur de la caméra, ou avez besoin de bas niveau accès au flux de capture, vous pouvez créer un enregistreur de capturer de réalité mixte personnalisé.

### <a name="creating-a-custom-mrc-recorder"></a>Création d’un enregistreur MRC personnalisé

Bien que l’utilisateur a toujours peut déclencher une photo ou vidéo à l’aide du système MRC du service de capture, une application peut souhaiter créer une application de caméra personnalisé, mais inclure hologrammes dans le flux de caméra à l’instar des MRC. Cela permet à l’application à lancer des captures de part de l’utilisateur, créer un enregistrement personnalisé l’interface utilisateur ou personnaliser les paramètres de cette option pour citer que quelques-uns.

**HoloStudio ajoute une caméra MRC personnalisée à l’aide d’effets MRC**

![HoloStudio ajoute une caméra MRC personnalisée à l’aide d’effets MRC](images/cameraiconholostudio-300px.jpg)

Les Applications Unity devrait [Locatable_camera_in_Unity](locatable-camera-in-unity.md) pour la propriété pour activer hologrammes.

Autres applications peuvent le faire à l’aide de la [API de Capture de média Windows](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.mediacapture.aspx) pour contrôler l’appareil photo et ajouter un effet Audio et vidéo de cette option pour inclure les hologrammes virtuels et les applications audio dans des vidéos et des images fixes.

Applications ont deux options pour ajouter l’effet :
* L’ancienne API : [Windows.Media.Capture.MediaCapture.AddEffectAsync()](https://msdn.microsoft.com/library/windows/apps/br211961.aspx)
* Le nouveau Microsoft recommandé API (retourne un objet, ce qui permet de manipuler les propriétés dynamiques) : [Windows.Media.Capture.MediaCapture.AddVideoEffectAsync()](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.mediacapture.addvideoeffectasync.aspx) / [Windows.Media.Capture.MediaCapture.AddAudioEffectAsync()](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.mediacapture.addaudioeffectasync.aspx) qui nécessitent l’application créer sa propre implémentation de [IVideoEffectDefinition](https://msdn.microsoft.com/library/windows/apps/windows.media.effects.ivideoeffectdefinition.aspx) et [IAudioEffectDefinition](https://msdn.microsoft.com/library/windows/apps/windows.media.effects.iaudioeffectdefinition.aspx). Consultez l’exemple d’effet MRC pour des exemples d’utilisation.

(Notez que ces espaces de noms ne sont pas reconnus par Visual Studio, mais les chaînes sont toujours valides)

Effet vidéo MRC (**Windows.Media.MixedRealityCapture.MixedRealityCaptureVideoEffect**)

|  Nom de la propriété  |  Type  |  Valeur par défaut  |  Description | 
|----------|----------|----------|----------|
|  StreamType  |  UInt32 ([MediaStreamType](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.mediastreamtype.aspx))  |  1 (VideoRecord)  |  Décrire le flux de capture cet effet est utilisé pour. Audio n’est pas disponible. | 
|  HologramCompositionEnabled  |  booléen  |  TRUE  |  Indicateur pour activer ou désactiver hologrammes dans la capture vidéo. | 
|  RecordingIndicatorEnabled  |  booléen  |  TRUE  |  Indicateur pour activer ou désactiver l’indicateur d’enregistrement sur l’écran pendant hologramme capture. | 
|  VideoStabilizationEnabled  |  booléen  |  FALSE  |  Indicateur pour activer ou désactiver la stabilisation vidéo alimentée par le dispositif de suivi HoloLens. | 
|  VideoStabilizationBufferLength  |  UINT32  |  0  |  Définir le nombre d’images historique est utilisé pour la stabilisation vidéo. 0 est presque « gratuite » à partir d’une perspective de puissance et de performances et de latence de 0. 15 est recommandée pour une qualité optimale (au prix de 15 images de latence et de la mémoire). | 
|  GlobalOpacityCoefficient  |  flottant  |  0.9 (HoloLens) 1.0 (casque immersif)  |  La valeur coefficient opacité global de hologramme dans la plage comprise entre 0.0 (complètement transparent) 1.0 (entièrement opaque). | 
|  BlankOnProtectedContent  |  booléen  |  FALSE  |  Indicateur pour activer ou désactiver le retour un cadre vide s’il existe un contenu d’affichage d’application UWP protégé 2d. Si cet indicateur a la valeur false et un 2d application UWP est montrant protégé le contenu, que l’application UWP 2d sera remplacée par une texture de contenu protégée dans les deux le casque et dans la capture de réalité mixte. |
|  ShowHiddenMesh  |  booléen  |  FALSE  |  Indicateur pour activer ou désactiver montrant la maille de zone masquée de la caméra holographique et voisines de contenu. |

Effet Audio MRC (**Windows.Media.MixedRealityCapture.MixedRealityCaptureAudioEffect**)

<table>
<tr>
<th>Nom de la propriété</th>
<th>Type</th>
<th>Valeur par défaut</th>
<th>Description</th>
</tr>
<tr>
<td>MixerMode</td>
<td>UINT32</td>
<td>2</td>
<td>
<ul>
<li>0 : Uniquement des données audio mic</li>
<li>1 : Audio système uniquement</li>
<li>2 : MIC et l’audio système</li>
</ul>
</td>
</tr>
</table>

### <a name="simultaneous-mrc-limitations"></a>Limitations de MRC simultanées

Il existe certaines limitations autour de plusieurs applications l’accès à cette option en même temps.

#### <a name="photovideo-camera-access"></a>Accès à la caméra vidéo/photo

La caméra vidéo/photo est limitée au nombre de processus qui peuvent y accéder en même temps. Pendant un processus est d’enregistrement vidéo ou prendre une photo à un autre processus ne pourra pas acquérir de la caméra vidéo/photo. (cela s’applique à la Capture de réalité mixte et de capture de photo/vidéo standard)

Avec Windows 10 avril 2018 mise à jour, cette restriction ne s’applique pas si l’appareil photo intégré de MRC l’interface utilisateur est utilisé pour prendre une photo ou une vidéo une fois une application a démarré à l’aide de la caméra vidéo/photo. Dans ce cas, la résolution et la fréquence d’images de l’appareil photo intégré de MRC l’interface utilisateur peuvent être réduites à partir de ses valeurs normales.

Avec Windows 10 octobre 2018 mise à jour, cette restriction ne s’applique pas à la diffusion MRC via Miracast.

#### <a name="mrc-access"></a>Accès MRC

Avec Windows 10 avril 2018 mise à jour, il n’est plus une limitation autour de plusieurs applications l’accès aux flux MRC (Toutefois, l’accès à la caméra vidéo/photo a toujours limitations).

Précédent pour le 10 avril 2018 de Windows mise à jour, d’enregistreur MRC personnalisé d’une application a été mutuellement avec système MRC (capture de photos, vidéos de capture ou de diffusion en continu à partir de la Windows Device Portal).

## <a name="see-also"></a>Voir aussi
* [Capture de réalité mixte](mixed-reality-capture.md)
* [Vue du spectateur](spectator-view.md)
