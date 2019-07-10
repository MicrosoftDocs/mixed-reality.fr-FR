---
title: Mixte de capture de la réalité pour les développeurs
description: Meilleures pratiques pour la réalité mixte de capture pour les développeurs.
author: mattzmsft
ms.author: mazeller
ms.date: 02/24/2019
ms.topic: article
keywords: mrc, photo, video, capture, camera
ms.openlocfilehash: d1675d2d6c74c6d15ca245a66719e00f2a7c2111
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694361"
---
# <a name="mixed-reality-capture-for-developers"></a>Mixte de capture de la réalité pour les développeurs

> [REMARQUE !] Consultez [restituer à partir de l’appareil photo PV](#render-from-the-pv-camera-opt-in) ci-dessous pour obtenir des conseils sur une nouvelle fonctionnalité MRC pour HoloLens 2.

Dans la mesure où un utilisateur peut prendre un [mixte de capture de la réalité](mixed-reality-capture.md) photo (MRC) ou de vidéo à tout moment, il existe quelques points que vous devez garder à l’esprit lorsque vous développez votre application. Cela inclut les meilleures pratiques pour la qualité visuelle MRC et être réactive aux modifications du système tout en les CMR sont capturées.

Les développeurs peuvent intégrer également de façon transparente de capture de réalité mixte et de l’insertion dans leurs applications.

Cette option sur HoloLens (première génération) prend en charge les vidéos et vos photos jusqu'à 720p, tandis que MRC sur HoloLens 2 prend en charge une vidéos jusqu'à 1080p et photos jusqu'à résolution 4 K.

## <a name="the-importance-of-quality-mrc"></a>L’importance de la qualité MRC

Réalité mixte capturées photos et vidéos sont probablement la première exposition à qu'un utilisateur aura de votre application. Si vous en tant que des captures d’écran de réalité mixte sur votre page de Microsoft Store ou à partir d’autres utilisateurs qui partagent les CMR sur les réseaux sociaux. Vous pouvez utiliser cette option pour votre application de démonstration, de former les utilisateurs, d’encourager les utilisateurs à partager leurs interactions world mixte et à la recherche de l’utilisateur et de la résolution des problèmes.

## <a name="how-mrc-impacts-your-app"></a>Comment MRC a un impact sur votre application

### <a name="enabling-mrc-in-your-app"></a>L’activation de cette option dans votre application

Par défaut, une application n’a pas rien à faire pour permettre aux utilisateurs de prendre des captures de réalité mixte.

### <a name="enabling-improved-alignment-for-mrc-in-your-app"></a>L’activation de meilleur alignement pour cette option dans votre application

Par défaut, capture de réalité mixte combine la sortie holographique d’oeil droit avec l’appareil photo/vidéo (PV). Ces deux sources sont combinés en utilisant le point de focus défini par l’application en cours d’exécution immersive.

Cela signifie que hologrammes en dehors du plan de focus ne s’alignent pas également (en raison de la distance physique entre l’appareil photo PV et l’affichage de droite).

#### <a name="set-the-focus-point"></a>Définir le point de focus

Applications immersives (sur HoloLens) doivent définir le [concentrer point](focus-point-in-unity.md) où ils attendent leur plan de stabilisation pour être. Cela garantit le meilleur alignement dans les deux le casque et dans la capture de réalité mixte.

Si un point de focus n’est pas défini, le plan de stabilisation par défaut est deux compteurs.

#### <a name="render-from-the-pv-camera-opt-in"></a>Effectuer le rendu de la caméra PV (opt-in)

HoloLens 2 ajoute la possibilité pour une application captivante à **restituer à partir de l’appareil photo PV** pendant l’exécution de capture de réalité mixte. Pour garantir que l’application prend en charge le rendu supplémentaire correctement, l’application doit participer à cette fonctionnalité.

Afficher dans les offres de caméra PV les améliorations suivantes sur l’expérience de cette option par défaut :
* Alignement hologramme à votre environnement physique et les mains (pour les interactions quasiment) doit être précise à tous les distances, au lieu d’avoir un décalage de distance autre que le point de focus comme vous pouvez voir dans la valeur par défaut de cette option.
* Le œil droit dans le casque ne seront pas compromise, car il n’est utilisé pour restituer les hologrammes pour la sortie de cette option.

Il existe trois étapes pour activer le rendu de la caméra PV :
1. Activer la PhotoVideoCamera HolographicViewConfiguration
2. Gérer le rendu HolographicCamera supplémentaire
3. Vérifiez vos nuanceurs et code sont affichés correctement à partir de cette HolographicCamera supplémentaire

##### <a name="enable-the-photovideocamera-holographicviewconfiguration"></a>Activer la PhotoVideoCamera HolographicViewConfiguration

Pour participer, une application permet simplement le PhotoVideoCamera [HolographicViewConfiguration](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfiguration):
```csharp
var display = Windows.Graphics.Holographic.HolographicDisplay.GetDefault();
var view = display.TryGetViewConfiguration(Windows.Graphics.Holographic.HolographicViewConfiguration.PhotoVideoCamera);
if (view != null)
{
   view.IsEnabled = true;
}
```

##### <a name="handle-the-additional-holographiccamera-render-in-directx"></a>Gérer le rendu HolographicCamera supplémentaire dans DirectX

Lorsque l’application a participer à restituer à partir de l’appareil photo PV et démarre la capture de réalité mixte :
1. Événement de CameraAdded de HolographicSpace se déclenche. Cet événement peut être différé si l’application ne peut pas gérer l’appareil photo pour l’instant.
2. Une fois que l’événement terminé (et il n’y a aucune Reports en suspens) le HolographicCamera apparaîtront dans la liste de AddedCameras de la HolographicFrame suivant.

Lors de la réalité mixte capture s’arrête (ou si l’application désactive la configuration de l’affichage pendant l’exécution de capture de réalité mixte) : le HolographicCamera apparaissent dans RemovedCameras liste de la prochaine HolographicFrame et événements de CameraRemoved de la HolographicSpace sera se déclenche.

Un [ViewConfiguration](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.viewconfiguration) propriété a été ajoutée à HolographicCamera pour aider à identifier la configuration d’un appareil photo appartient.

##### <a name="handle-the-additional-holographiccamera-render-in-unity"></a>Gérer le rendu HolographicCamera supplémentaire dans Unity

>[!NOTE]
> Prise en charge de Unity à restituer à partir de l’appareil photo PV est en cours de développement et ne peut pas être utilisé, encore. Cette documentation sera mise à jour lorsqu’une build Unity avec prise en charge pour le rendu de la caméra PV est disponible.

##### <a name="verify-shaders-and-code-support-additional-cameras"></a>Vérifiez les nuanceurs et caméras supplémentaires de prise en charge de code

Exécuter une capture de réalité mixte et le vérifier pour alignement inhabituel, contenu manquant ou des problèmes de performances. Les nuanceurs de mise à jour et de code comme il convient.

S’il existe certaines scènes qui ne prennent pas en charge le rendu à une caméra supplémentaire, vous pouvez désactiver HolographicViewConfiguration du PhotoVideoCamera pendant leur déroulement.

### <a name="disabling-mrc-in-your-app"></a>La désactivation de cette option dans votre application

#### <a name="2d-app"></a>Application 2D

Applications 2D peuvent choisir d’avoir leur contenu visuel obscurcie lorsque la capture de réalité mixte est en cours d’exécution par :
* Présent avec les [DXGI_PRESENT_RESTRICT_TO_OUTPUT](https://docs.microsoft.com/windows/desktop/direct3ddxgi/dxgi-present) indicateur
* Créer la chaîne de permutation de l’application avec le [DXGI_SWAP_CHAIN_FLAG_HW_PROTECTED](https://docs.microsoft.com/windows/desktop/api/dxgi/ne-dxgi-dxgi_swap_chain_flag) indicateur
* Avec Windows 10 peut 2019 mettre à jour, définition de ApplicationView [IsScreenCaptureEnabled](https://docs.microsoft.com/uwp/api/windows.ui.viewmanagement.applicationview.isscreencaptureenabled)

#### <a name="immersive-app"></a>Application captivante

Applications immersives peuvent choisir d’avoir leur contenu visuel exclu de la capture en réalité mixte :
* Définition de HolographicCameraRenderingParameter [IsContentProtectionEnabled](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.iscontentprotectionenabled) pour désactiver la capture de réalité mixte pour sa trame associée
* Définition de HolographicCamera [IsHardwareContentProtectionEnabled](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.ishardwarecontentprotectionenabled) pour désactiver la capture de réalité mixte pour sa caméra HOLOGRAPHIQUE associée

#### <a name="password-keyboard"></a>Clavier de mot de passe

Avec Windows 10 mai 2019 mise à jour, contenu visuel est automatiquement exclu de capture de réalité mixte lorsqu’un clavier de mot de passe ou code confidentiel est visible.

### <a name="knowing-when-mrc-is-active"></a>Savoir quand cette option est active

Le [AppCapture](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.AppCapture) classe peut être utilisée par une application de savoir quand système mixte de capture de la réalité est en cours d’exécution (pour le contenu audio ou vidéo).

>[!NOTE]
>De AppCapture [GetForCurrentView](https://docs.microsoft.com/uwp/api/windows.media.capture.appcapture.getforcurrentview) API peut retourner null si la capture de la réalité de mixte n’est pas disponible sur l’appareil. Il est également important de l’événement CapturingChanged quand votre application est suspendue annuler l’inscription, sinon MRC peut passer à un état bloqué.

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

Autres applications peuvent le faire à l’aide de la [API de Capture de média Windows](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture) pour contrôler l’appareil photo et ajouter un effet Audio et vidéo de cette option pour inclure les hologrammes virtuels et les applications audio dans des vidéos et des images fixes.

Applications ont deux options pour ajouter l’effet :
* L’ancienne API : [Windows.Media.Capture.MediaCapture.AddEffectAsync()](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.addeffectasync)
* Le nouveau Microsoft recommandé API (retourne un objet, ce qui permet de manipuler les propriétés dynamiques) : [Windows.Media.Capture.MediaCapture.AddVideoEffectAsync()](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.addvideoeffectasync) / [Windows.Media.Capture.MediaCapture.AddAudioEffectAsync()](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.addaudioeffectasync) qui nécessitent l’application créer sa propre implémentation de [IVideoEffectDefinition](https://docs.microsoft.com/uwp/api/Windows.Media.Effects.IVideoEffectDefinition) et [IAudioEffectDefinition](https://docs.microsoft.com/uwp/api/windows.media.effects.iaudioeffectdefinition). Consultez l’exemple d’effet MRC pour des exemples d’utilisation.

>[!NOTE]
> L’espace de noms Windows.Media.MixedRealityCapture n’est pas reconnu par Visual Studio, mais les chaînes sont toujours valides.

Effet vidéo MRC (**Windows.Media.MixedRealityCapture.MixedRealityCaptureVideoEffect**)

|  Nom de la propriété  |  type  |  Valeur par défaut  |  Description | 
|----------|----------|----------|----------|
|  StreamType  |  UInt32 ([MediaStreamType](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaStreamType))  |  1 (VideoRecord)  |  Décrire le flux de capture cet effet est utilisé pour. Audio n’est pas disponible. | 
|  HologramCompositionEnabled  |  booléenne  |  TRUE  |  Indicateur pour activer ou désactiver hologrammes dans la capture vidéo. | 
|  RecordingIndicatorEnabled  |  booléenne  |  TRUE  |  Indicateur pour activer ou désactiver l’indicateur d’enregistrement sur l’écran pendant hologramme capture. | 
|  VideoStabilizationEnabled  |  booléenne  |  FALSE  |  Indicateur pour activer ou désactiver la stabilisation vidéo alimentée par le dispositif de suivi HoloLens. | 
|  VideoStabilizationBufferLength  |  UINT32  |  0  |  Définir le nombre d’images historique est utilisé pour la stabilisation vidéo. 0 est presque « gratuite » à partir d’une perspective de puissance et de performances et de latence de 0. 15 est recommandée pour une qualité optimale (au prix de 15 images de latence et de la mémoire). | 
|  GlobalOpacityCoefficient  |  flottant  |  0.9 (HoloLens) 1.0 (casque immersif)  |  La valeur coefficient opacité global de hologramme dans la plage comprise entre 0.0 (complètement transparent) 1.0 (entièrement opaque). | 
|  BlankOnProtectedContent  |  booléenne  |  FALSE  |  Indicateur pour activer ou désactiver le retour un cadre vide s’il existe un contenu d’affichage d’application UWP protégé 2d. Si cet indicateur a la valeur false et un 2d application UWP est montrant protégé le contenu, que l’application UWP 2d sera remplacée par une texture de contenu protégée dans les deux le casque et dans la capture de réalité mixte. |
|  ShowHiddenMesh  |  booléenne  |  FALSE  |  Indicateur pour activer ou désactiver montrant la maille de zone masquée de la caméra holographique et voisines de contenu. |
| OutputSize | Size | 0, 0 | Définissez la taille de sortie souhaité après rognage de stabilisation vidéo. Une taille de la culture par défaut est choisie si 0 ou une taille de sortie non valide est spécifiée. |
| PreferredHologramPerspective | UINT32 | 1 (PhotoVideoCamera) | Énumération utilisée pour indiquer quelle configuration de la vue HOLOGRAPHIQUE appareil photo doit être capturée. Définition de 0 signifie (affichage) que l’application ne seront pas invitée à effectuer le rendu de la caméra vidéo/photo |

Effet Audio MRC (**Windows.Media.MixedRealityCapture.MixedRealityCaptureAudioEffect**)

<table>
<tr>
<th>Nom de la propriété</th>
<th>type</th>
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

Avec 2 HoloLens, une application peut utiliser de MediaCaptureInitializationSettings [SharingMode](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacaptureinitializationsettings.sharingmode) propriété pour indiquer qu’ils souhaitent exécuter SharedReadOnly s’ils n’ont pas besoin d’un contrôle exclusif sur la caméra vidéo/photo. Vous aurez ainsi la résolution et la fréquence d’images de la capture se limite à ce qui autres applications ont configuré l’appareil photo pour fournir.

##### <a name="built-in-mrc-photovideo-camera-access"></a>Accès de caméra vidéo/photo MRC intégré

Fonctionnalité MRC intégrée à Windows 10 (via Cortana, Menu Démarrer, les raccourcis du matériel Miracast, Windows Device Portal) :
* S’exécute avec ExclusiveControl par défaut

Toutefois, la prise en charge a été ajouté à chaque sous-système pour fonctionner en mode partagé :
* Si une application demande l’accès à la caméra vidéo/photo ExclusiveControl, MRC intégré s’arrête automatiquement à l’aide de la caméra vidéo/photo afin de la demande de l’application réussit
* Si MRC intégrée est démarré pendant qu’une application a ExclusiveControl, MRC intégré s’exécute en mode de SharedReadOnly

Cette fonctionnalité en mode partagé présente certaines restrictions :
* Photo via Cortana, les raccourcis de matériel ou Menu Démarrer : Nécessite Windows 10 avril 2018 mettre à jour (ou version ultérieure)
* Vidéo via Cortana, les raccourcis de matériel ou Menu Démarrer : Nécessite Windows 10 avril 2018 mettre à jour (ou version ultérieure)
* Diffusion en continu de MRC sur Miracast : Nécessite les fenêtres de mise à jour 10 octobre 2018 (ou version ultérieure)
* Diffusion en continu MRC sur Windows Device Portal ou via l’application de complément HoloLens : Requiert HoloLens 2

>[!NOTE]
> La résolution et la fréquence d’images de l’appareil photo intégré de MRC l’interface utilisateur peuvent être réduites à partir de ses valeurs normales lorsqu’une autre application à l’aide de la caméra vidéo/photo.

#### <a name="mrc-access"></a>Accès MRC

Avec Windows 10 avril 2018 mise à jour, il n’est plus une limitation autour de plusieurs applications l’accès aux flux MRC (Toutefois, l’accès à la caméra vidéo/photo a toujours limitations).

Précédent pour le 10 avril 2018 de Windows mise à jour, d’enregistreur MRC personnalisé d’une application a été mutuellement avec système MRC (capture de photos, vidéos de capture ou de diffusion en continu à partir de la Windows Device Portal).

## <a name="see-also"></a>Voir aussi
* [Capture de Réalité Mixte](mixed-reality-capture.md)
* [Vue Spectateur](spectator-view.md)
