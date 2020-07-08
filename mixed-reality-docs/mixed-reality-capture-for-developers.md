---
title: Capture de Réalité Mixte pour les développeurs
description: Meilleures pratiques pour la capture de réalité mixte pour les développeurs.
author: mattzmsft
ms.author: mazeller
ms.date: 02/24/2019
ms.topic: article
keywords: MRC, photo, vidéo, capture, appareil photo
ms.openlocfilehash: 44b853e96ab956e5ea6c03d8c23a61e91ac733d4
ms.sourcegitcommit: fef42e2908e49822f2d13b05d2f9260bf0d72158
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86061142"
---
# <a name="mixed-reality-capture-for-developers"></a>Capture de Réalité Mixte pour les développeurs

> [!NOTE]
> Pour obtenir des conseils sur une nouvelle fonctionnalité MRC pour HoloLens 2, voir [rendu à partir de l’appareil photo PV](#render-from-the-pv-camera-opt-in) ci-dessous.

Comme un utilisateur peut prendre à tout moment une photo ou une vidéo MRC ( [Mixed Reality capture](mixed-reality-capture.md) ), vous devez garder à l’esprit quelques points lorsque vous développez votre application. Cela comprend les meilleures pratiques pour la qualité visuelle MRC et la réponse aux modifications du système pendant la capture des MRCs.

Les développeurs peuvent également intégrer en toute transparence la capture de réalité mixte et l’insertion dans leurs applications.

La MRC sur HoloLens (première génération) prend en charge les vidéos et les photos jusqu’à 720p, tandis que la MRC sur HoloLens 2 prend en charge les vidéos jusqu’à 1080p et les photos jusqu’à 4 Ko.

## <a name="the-importance-of-quality-mrc"></a>L’importance de la qualité du MRC

Les photos et vidéos capturées en réalité mixte sont probablement la première exposition d’un utilisateur de votre application. Le fait que des captures d’écran de réalité mixte sur votre page Microsoft Store ou d’autres utilisateurs partagent des MRCs sur des réseaux sociaux. Vous pouvez utiliser la fonction MRC pour faire la démonstration de votre application, éduquer les utilisateurs, encourager les utilisateurs à partager leurs interactions avec le monde mixte et pour la recherche des utilisateurs et la résolution des problèmes.

## <a name="how-mrc-impacts-your-app"></a>Impact de la MRC sur votre application

### <a name="enabling-mrc-in-your-app"></a>Activation de la MRC dans votre application

Par défaut, une application n’a rien à faire pour permettre aux utilisateurs d’effectuer des captures de réalité mixte.

### <a name="enabling-improved-alignment-for-mrc-in-your-app"></a>Activation de l’alignement amélioré pour la MRC dans votre application

Par défaut, la capture de la réalité mixte combine la sortie holographique de l’oeil droit avec l’appareil photo/vidéo (PV). Ces deux sources sont combinées à l’aide du point de focus défini par l’application immersif en cours d’exécution.

Cela signifie que les hologrammes en dehors du plan de focus ne s’alignent pas de la même manière (en raison de la distance physique entre la caméra va et l’affichage à droite).

#### <a name="set-the-focus-point"></a>Définir le point de focus

Les applications immersives (sur HoloLens) doivent définir le [point de focalisation](focus-point-in-unity.md) de leur plan de stabilisation. Cela garantit l’alignement optimal dans le casque et dans la capture de réalité mixte.

Si un point de focus n’est pas défini, le plan de stabilisation prend par défaut la valeur de deux mètres.

#### <a name="render-from-the-pv-camera-opt-in"></a>Rendre à partir de l’appareil photo PV (abonnement)

HoloLens 2 ajoute la possibilité pour une application immersif de s' **afficher à partir de l’appareil photo PV pendant l’exécution de la capture de la** réalité mixte. Pour vous assurer que l’application prend en charge le rendu supplémentaire correctement, l’application doit accepter cette fonctionnalité.

Le rendu à partir de la caméra va offre les améliorations suivantes par rapport à l’expérience MRC par défaut :
* L’alignement de l’hologramme sur votre environnement physique et les mains (pour les interactions proches) doivent être exacts à toutes les distances, au lieu d’avoir un décalage à des distances autres que le point de focus, comme vous pouvez le voir dans la MRC par défaut.
* L’oeil droit du casque n’est pas compromis, car il ne sera pas utilisé pour afficher les hologrammes de la sortie MRC.

Il existe trois étapes pour activer le rendu à partir de l’appareil photo PV :
1. Activer PhotoVideoCamera HolographicViewConfiguration
2. Gérer le rendu HolographicCamera supplémentaire
3. Vérifier les nuanceurs et le rendu du code correctement à partir de ce HolographicCamera supplémentaire

##### <a name="enable-the-photovideocamera-holographicviewconfiguration-in-directx"></a>Activer le HolographicViewConfiguration PhotoVideoCamera dans DirectX

Pour s’abonner au rendu à partir de l’appareil photo PV, une application active simplement le [HolographicViewConfiguration](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfiguration)de PhotoVideoCamera :
```csharp
var display = Windows.Graphics.Holographic.HolographicDisplay.GetDefault();
var view = display.TryGetViewConfiguration(Windows.Graphics.Holographic.HolographicViewConfigurationKind.PhotoVideoCamera);
if (view != null)
{
    view.IsEnabled = true;
}
```

##### <a name="handle-the-additional-holographiccamera-render-in-directx"></a>Gérer le rendu HolographicCamera supplémentaire dans DirectX

Lorsque l’application a choisi d’effectuer le rendu à partir de l’appareil photo PV et que la capture de la réalité mixte démarre :
1. L’événement CameraAdded de HolographicSpace se déclenche. Cet événement peut être différé si l’application ne peut pas gérer l’appareil photo pour l’instant.
2. Une fois que l’événement est terminé (et qu’il n’y a aucun différé en suspens), le HolographicCamera apparaît dans la liste AddedCameras suivante du HolographicFrame.

Quand la capture de la réalité mixte s’arrête (ou si l’application désactive la configuration de la vue alors que la capture de la réalité mixte est en cours d’exécution) : le HolographicCamera s’affiche dans la liste RemovedCameras du HolographicFrame suivant et l’événement CameraRemoved du HolographicSpace est déclenché.

Une propriété [ViewConfiguration](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.viewconfiguration) a été ajoutée à HolographicCamera pour aider à identifier la configuration à laquelle une caméra appartient.

##### <a name="enable-the-photovideocamera-holographicviewconfiguration-in-unity"></a>Activer le HolographicViewConfiguration PhotoVideoCamera dans Unity

> [!NOTE]
> Cela nécessite **Unity 2018.4.13 F1**, **Unity 2019.3.0 F1**ou plus récent.

Pour accepter le rendu à partir de l’appareil photo PV, lorsque vous utilisez la boîte à outils de la [réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/README.html), activez le fournisseur de [paramètres d’appareil photo Windows Mixed Reality](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/CameraSystem/WindowsMixedRealityCameraSettings.html) et vérifiez le paramètre **rendu à partir d’une caméra va** .

Si vous n’utilisez pas la boîte à outils de réalité mixte, vous pouvez utiliser un composant pour vous [abonner manuellement](#enable-the-photovideocamera-holographicviewconfiguration-in-directx) comme décrit ci-dessus pour DirectX.

##### <a name="handle-the-additional-holographiccamera-render-in-unity"></a>Gérer le rendu HolographicCamera supplémentaire dans Unity

Cette opération est effectuée automatiquement par Unity.

##### <a name="enable-the-photovideocamera-holographicviewconfiguration-in-unreal"></a>Activer le HolographicViewConfiguration PhotoVideoCamera dans Unreal

> [!NOTE]
> Cela nécessite **Unreal Engine 4.25** ou ultérieur.

Pour choisir le rendu à partir de l’appareil photo/vidéo :

1. Appelez **SetEnabledMixedRealityCamera** et **ResizeMixedRealityCamera**
    * Utilisez les valeurs de taille **Size X** et **Size Y** pour définir les dimensions de la vidéo.

![Troisième caméra](images/unreal-camera-3rd.PNG)

##### <a name="handle-the-additional-holographiccamera-render-in-unreal"></a>Gérer le rendu HolographicCamera supplémentaire dans inréel

Cette opération est effectuée automatiquement par inréel.

##### <a name="verify-shaders-and-code-support-additional-cameras"></a>Vérifier que les nuanceurs et le code prennent en charge des caméras supplémentaires

Exécutez une capture de la réalité mixte et vérifiez l’alignement inhabituel, le contenu manquant ou les problèmes de performances. Mettez à jour les nuanceurs et le code comme il convient.

Si certaines scènes ne peuvent pas prendre en charge le rendu sur une caméra supplémentaire, vous pouvez désactiver les HolographicViewConfiguration du PhotoVideoCamera.

### <a name="disabling-mrc-in-your-app"></a>Désactivation de la MRC dans votre application

#### <a name="2d-app"></a>application 2D

les applications 2D peuvent choisir de masquer leur contenu visuel lorsque la capture de la réalité mixte s’exécute :
* Présent avec l’indicateur [DXGI_PRESENT_RESTRICT_TO_OUTPUT](https://docs.microsoft.com/windows/desktop/direct3ddxgi/dxgi-present)
* Créer la chaîne de permutation de l’application avec l’indicateur [DXGI_SWAP_CHAIN_FLAG_HW_PROTECTED](https://docs.microsoft.com/windows/desktop/api/dxgi/ne-dxgi-dxgi_swap_chain_flag)
* Avec la mise à jour de Windows 10 mai 2019, la définition de [IsScreenCaptureEnabled](https://docs.microsoft.com/uwp/api/windows.ui.viewmanagement.applicationview.isscreencaptureenabled) de ApplicationView

#### <a name="immersive-app"></a>Application immersif

Les applications immersives peuvent choisir d’exclure leur contenu visuel de la capture de la réalité mixte en :
* Définition de [IsContentProtectionEnabled](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.iscontentprotectionenabled) de HolographicCameraRenderingParameter pour désactiver la capture de réalité mixte pour le frame associé
* Définition de la [IsHardwareContentProtectionEnabled](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamera.ishardwarecontentprotectionenabled) de HolographicCamera pour désactiver la capture de réalité mixte pour sa caméra holographique associée

#### <a name="password-keyboard"></a>Clavier du mot de passe

Avec la mise à jour de Windows 10 mai 2019, le contenu visuel est automatiquement exclu de la capture de la réalité mixte lorsqu’un mot de passe ou un clavier de code confidentiel est visible.

### <a name="knowing-when-mrc-is-active"></a>Savoir quand la MRC est active

La classe [AppCapture](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.AppCapture) peut être utilisée par une application pour savoir quand la capture de la réalité mixte du système est en cours d’exécution (audio ou vidéo).

>[!NOTE]
>L’API [GetForCurrentView](https://docs.microsoft.com/uwp/api/windows.media.capture.appcapture.getforcurrentview) de AppCapture peut retourner la valeur null si la capture de la réalité mixte n’est pas disponible sur l’appareil. Il est également important de supprimer l’inscription de l’événement CapturingChanged lorsque votre application est suspendue, sinon, la désactivation de l’événement peut être bloquée.

### <a name="best-practices-hololens-specific"></a>Meilleures pratiques (spécifiques à HoloLens)

La MRC est censée fonctionner sans travail supplémentaire des développeurs, mais il existe quelques éléments à connaître pour fournir la meilleure expérience de capture de la réalité mixte de votre application.

**MRC utilise le canal alpha de l’hologramme pour mélanger avec l’image de l' [appareil photo](locatable-camera.md)**

L’étape la plus importante consiste à s’assurer que votre application est déclassée au noir transparent au lieu d’être vidée en noir opaque. Dans Unity, cette opération est effectuée par défaut avec le MixedRealityToolkit, mais si vous effectuez un développement dans non Unity, vous devrez peut-être modifier une seule ligne.

Voici certains des artefacts que vous pouvez voir dans la MRC si votre application n’est pas dépendante du noir transparent :

**Exemples d’échecs**: bords noirs autour du contenu (ne pas effacer jusqu’au noir transparent)

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

**Exemples d’échecs**: la scène d’arrière-plan complète de l’hologramme s’affiche en noir. La définition d’une valeur alpha d’arrière-plan de 1 produit un arrière-plan noir

![La définition d’une valeur alpha d’arrière-plan de 1 produit un arrière-plan noir](images/clearopaqueblack-300px.png)

**Résultat attendu**: les hologrammes apparaissent correctement fusionnés avec le monde réel (résultat attendu en cas d’effacement au noir transparent)

![Résultat attendu en cas d’effacement au noir transparent](images/cleartransparentblack-300px.png)

**Solution**:
* Modifiez tout le contenu affiché en noir opaque pour avoir une valeur alpha de 0.
* Assurez-vous que l’application est en mode d’effacement transparent noir.
* La valeur par défaut Unity est Clear pour être désactivée automatiquement avec MixedRealityToolkit, mais s’il s’agit d’une application non Unity, vous devez modifier la couleur utilisée avec ID3D11DeiceContext :: ClearRenderTargetView (). Vous souhaitez vous assurer que vous vous dépassez du noir transparent (0, 0, 0, 0) au lieu du noir opaque (0, 0, 0, 1).

Vous pouvez maintenant ajuster les valeurs alpha de vos ressources si vous le souhaitez, mais cela n’est généralement pas nécessaire. La plupart du temps, MRCs semble prêt à l’emploi. MRC suppose une alpha prémultipliée. Les valeurs alpha n’affectent que la capture MRC.

### <a name="what-to-expect-when-mrc-is-enabled-on-hololens"></a>Ce qui se passe lorsque la MRC est activée sur HoloLens

Les éléments suivants s’appliquent à la fois à HoloLens (première génération) et à HoloLens 2, sauf indication contraire :

* Le système limite l’application au rendu 30Hz. Cela crée de l’espace pour l’exécution de la MRC afin que l’application n’ait pas besoin de conserver une réserve de budget constante et qu’elle corresponde à la fréquence d’enregistrement de l’enregistrement vidéo MRC de 30fps
* Le contenu de l’hologramme dans le bon œil de l’appareil peut sembler « Spark » lors de l’enregistrement/de la diffusion en continu MRC : le texte peut devenir plus difficile à lire et les bords de l’hologramme peuvent apparaître plus dentelés (l’activation d’un rendu de troisième appareil photo sur **HoloLens 2** évite ce compromis)
* Les photos et vidéos MRC respectent le point de [focalisation](focus-point-in-unity.md) de l’application si l’application l’a activée, ce qui permet de s’assurer que les hologrammes sont correctement positionnés. Pour les vidéos, le point de focalisation est lissé, de sorte que les hologrammes peuvent paraître lentement en place si la profondeur du point de focalisation change de façon significative. Les hologrammes qui se trouvent à des profondeurs différents du point de focalisation peuvent apparaître dans le monde réel (Voir l’exemple ci-dessous où le point de focus est défini à 2 mètres, mais l’hologramme est positionné à 1 mètre).

![Les hologrammes à 2 mètres sont parfaitement inscrits au monde entier. Les hologrammes à des distances proches ou éloignées peuvent être légèrement décalés.](images/hologramaccuracydistancemrc-1000px.png)

## <a name="integrating-mrc-functionality-from-within-your-app"></a>Intégration de la fonctionnalité MRC à partir de votre application

Votre application de réalité mixte peut initier la capture de photos ou de vidéos MRC à partir de l’application, et le contenu capturé est mis à la disposition de votre application sans être stocké dans le « rouleau de caméra » de l’appareil. Vous pouvez créer un enregistreur MRC personnalisé ou tirer parti de l’interface utilisateur de capture d’appareil photo intégrée. 

### <a name="mrc-with-built-in-camera-ui"></a>MRC avec l’interface utilisateur de l’appareil photo intégré

Les développeurs peuvent utiliser l' *[API d’interface utilisateur de capture de l’appareil photo](https://docs.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-cameracaptureui)* pour obtenir une photo ou une vidéo de réalité mixte capturée par l’utilisateur avec quelques lignes de code.

Cette API lance l’interface utilisateur de la caméra MRC intégrée, à partir de laquelle l’utilisateur peut prendre une photo ou une vidéo, et retourne la capture obtenue à votre application.  Si vous souhaitez créer votre propre interface utilisateur d’appareil photo ou si vous avez besoin d’un accès de niveau inférieur au flux de capture, vous pouvez créer un enregistreur de capture de réalité mixte personnalisé.

### <a name="creating-a-custom-mrc-recorder"></a>Création d’un enregistreur MRC personnalisé

Bien que l’utilisateur puisse toujours déclencher une photo ou une vidéo à l’aide du service de capture MRC du système, une application peut souhaiter créer une application de caméra personnalisée, mais inclure des hologrammes dans le flux de l’appareil photo comme MRC. Cela permet à l’application de lancer des captures pour le compte de l’utilisateur, de créer une interface utilisateur d’enregistrement personnalisée ou de personnaliser les paramètres MRC pour nommer quelques exemples.

**HoloStudio ajoute une caméra MRC personnalisée à l’aide des effets MRC**

![HoloStudio ajoute une caméra MRC personnalisée à l’aide des effets MRC](images/cameraiconholostudio-300px.jpg)

Les applications Unity doivent voir [Locatable_camera_in_Unity](locatable-camera-in-unity.md) pour la propriété pour activer les hologrammes.

D’autres applications peuvent le faire à l’aide des [API de capture Windows Media](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaCapture) pour contrôler l’appareil photo et ajouter un effet de vidéo et d’audio MRC pour inclure les hologrammes virtuels et l’audio de l’application dans les images et les vidéos.

Les applications ont deux options pour ajouter l’effet :
* API plus ancienne : [Windows. Media. capture. MediaCapture. AddEffectAsync ()](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.addeffectasync)
* La nouvelle API recommandée par Microsoft (retourne un objet, ce qui permet de manipuler des propriétés dynamiques) : [Windows. Media. capture. MediaCapture. AddVideoEffectAsync ()](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.addvideoeffectasync)  /  [Windows. Media. capture. MediaCapture. AddAudioEffectAsync ()](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacapture.addaudioeffectasync) qui requièrent que l’application crée sa propre implémentation de [IVideoEffectDefinition](https://docs.microsoft.com/uwp/api/Windows.Media.Effects.IVideoEffectDefinition) et [IAudioEffectDefinition](https://docs.microsoft.com/uwp/api/windows.media.effects.iaudioeffectdefinition). Pour obtenir un exemple d’utilisation, consultez l’exemple d’effet MRC.

>[!NOTE]
> L’espace de noms Windows. Media. MixedRealityCapture n’est pas reconnu par Visual Studio, mais les chaînes sont toujours valides.

Effet vidéo MRC (**Windows. Media. MixedRealityCapture. MixedRealityCaptureVideoEffect**)

|  Nom de la propriété  |  Type  |  Valeur par défaut  |  Description |
|----------|----------|----------|----------|
|  StreamType  |  UINT32 ([MediaStreamType](https://docs.microsoft.com/uwp/api/Windows.Media.Capture.MediaStreamType))  |  1 (VideoRecord)  |  Décrivez le flux de capture pour lequel cet effet est utilisé. L’audio n’est pas disponible. |
|  HologramCompositionEnabled  |  boolean  |  TRUE  |  Indicateur permettant d’activer ou de désactiver les hologrammes dans la capture vidéo. |
|  RecordingIndicatorEnabled  |  boolean  |  TRUE  |  Indicateur permettant d’activer ou de désactiver l’indicateur d’enregistrement à l’écran pendant la capture d’hologramme. |
|  VideoStabilizationEnabled  |  boolean  |  FALSE  |  Indicateur d’activation ou de désactivation de la stabilisation vidéo optimisée par le dispositif de suivi HoloLens. |
|  VideoStabilizationBufferLength  |  UINT32  |  0  |  Définissez le nombre de frames d’historique utilisés pour la stabilisation vidéo. 0 est une latence de 0 et presque « gratuit » du point de vue de l’alimentation et des performances. 15 est recommandé pour une qualité optimale (au prix de 15 trames de latence et de mémoire). |
|  GlobalOpacityCoefficient  |  float  |  0,9 (HoloLens) 1,0 (casque immersif)  |  Définissez le coefficient d’opacité globale de l’hologramme dans une plage allant de 0,0 (entièrement transparent) à 1,0 (entièrement opaque). |
|  BlankOnProtectedContent  |  boolean  |  FALSE  |  Indicateur d’activation ou de désactivation du retour d’un frame vide si une application UWP 2d présente un contenu protégé. Si cet indicateur a la valeur false et qu’une application UWP 2D affiche du contenu protégé, l’application UWP 2D est remplacée par une texture de contenu protégé dans le casque et dans la capture de la réalité mixte. |
|  ShowHiddenMesh  |  boolean  |  FALSE  |  Indicateur permettant d’activer ou de désactiver l’indication du maillage de zone masqué et du contenu voisin de l’appareil photo holographique. |
| En-dessous | Taille | 0, 0 | Définissez la taille de sortie souhaitée après rognage pour la stabilisation vidéo. Une taille de rognage par défaut est choisie si 0 ou si une taille de sortie non valide est spécifiée. |
| PreferredHologramPerspective | UINT32 | **Rendre à partir des** paramètres de l’appareil photo dans le portail des appareils Windows | Énumération utilisée pour indiquer la configuration de vue d’appareil photo holographique à capturer : 0 (affichage) signifie que l’application n’est pas invitée à effectuer le rendu à partir de la caméra photo/vidéo, 1 (PhotoVideoCamera) demande à l’application de s’afficher à partir de la caméra photo/vidéo (si l’application la prend en charge). Pris en charge uniquement sur HoloLens 2 |

>[!NOTE]
> Vous pouvez modifier la valeur par défaut de **PreferredHologramPerspective** dans le portail de périphériques Windows en accédant à la page de capture de la [réalité mixte](using-the-windows-device-portal.md#mixed-reality-capture) et en désactivez **afficher à partir de l’appareil photo**. La valeur par défaut est **1 (PhotoVideoCamera)**, mais elle peut être désactivée pour lui attribuer la valeur **0 (affichage)**.
>
> La valeur par défaut de **PreferredHologramPerspective** était **0 (affichage)** avant la mise à jour du 2020 juin (windows holographique, version 2004 Build 19041,1106 et windows holographique, version 1903 Build 18362,1064).

Effet audio MRC (**Windows. Media. MixedRealityCapture. MixedRealityCaptureAudioEffect**)

| Nom de la propriété | Type | Valeur par défaut | Description |
|----------|----------|----------|----------|
| MixerMode | UINT32 | 2 (MIC et système audio) | Énumération utilisée pour indiquer les sources audio à utiliser : 0 (MIC audio uniquement), 1 (système audio uniquement), 2 (MIC et système audio) |
| LoopbackGain | float | Paramètre de **gain audio** de l’application dans le portail des appareils Windows | Gain à appliquer au volume audio système. Les plages sont comprises entre 0,0 et 5,0. Pris en charge uniquement sur HoloLens 2 |
| MicrophoneGain | float | Paramètre de **gain audio MIC** dans le portail d’appareils Windows | Gain à appliquer au volume Mic. Les plages sont comprises entre 0,0 et 5,0. Pris en charge uniquement sur HoloLens 2 |

>[!NOTE]
> Vous pouvez modifier la valeur par défaut de **LoopbackGain** ou **MicrophoneGain** dans le portail de périphériques Windows en accédant à la page de capture de la [réalité mixte](using-the-windows-device-portal.md#mixed-reality-capture) et en réglant le curseur en regard de leurs paramètres respectifs. Les deux paramètres ont par défaut la valeur **1,0**, mais peuvent être définis sur n’importe quelle valeur comprise entre **0,0** et **5,0**.
>
> L’utilisation du portail d’appareils Windows pour configurer les valeurs par défaut a été ajoutée avec la mise à jour de juin 2020 (Windows holographique, version 2004 Build 19041,1106 et Windows holographique, version 1903 Build 18362,1064).

### <a name="simultaneous-mrc-limitations"></a>Limitations de la MRC simultanée

Certaines restrictions s’imposent pour plusieurs applications qui accèdent à MRC en même temps.

#### <a name="photovideo-camera-access"></a>Accès à la photo/caméra vidéo

La caméra photo/vidéo est limitée au nombre de processus qui peuvent y accéder en même temps. Lorsqu’un processus enregistre une vidéo ou prend une photo, tout autre processus ne parvient pas à acquérir l’appareil photo/vidéo. (cela s’applique à la fois à la capture de réalité mixte et à la capture de photos/vidéos standard)

Avec HoloLens 2, une application peut utiliser la propriété MediaCaptureInitializationSettings' [SharingMode](https://docs.microsoft.com/uwp/api/windows.media.capture.mediacaptureinitializationsettings.sharingmode) pour indiquer qu’elle souhaite exécuter SharedReadOnly si elle n’a pas besoin d’un contrôle exclusif sur la caméra photo/vidéo. Cela signifie que la résolution et la fréquence d’images de la capture se limitent à ce que les autres applications ont configurées pour la caméra.

##### <a name="built-in-mrc-photovideo-camera-access"></a>Accès intégré à la caméra photo/vidéo MRC

Fonctionnalité MRC intégrée à Windows 10 (via Cortana, menu Démarrer, raccourcis matériels, Miracast, portail de périphériques Windows) :
* S’exécutera avec ExclusiveControl par défaut

Toutefois, une prise en charge a été ajoutée à chaque sous-système pour fonctionner en mode partagé :
* Si une application demande un accès ExclusiveControl à la caméra photo/vidéo, la MRC intégrée arrête automatiquement l’utilisation de la caméra photo/vidéo pour que la demande de l’application aboutisse.
* Si la MRC intégrée est démarrée alors qu’une application dispose d’un ExclusiveControl, la MRC intégrée s’exécutera en mode SharedReadOnly

Cette fonctionnalité du mode partagé présente certaines restrictions :
* Photo via Cortana, les raccourcis matériels ou le menu Démarrer : requiert la mise à jour 2018 d’avril de Windows 10 (ou version ultérieure)
* Vidéo via Cortana, les raccourcis matériels ou le menu Démarrer : requiert la mise à jour 2018 de Windows 10 avril (ou version ultérieure)
* Streaming MRC sur Miracast : requiert la mise à jour 2018 de Windows 10 octobre (ou version ultérieure)
* Diffusion en continu de la MRC sur le portail de périphériques Windows ou via l’application auxiliaire HoloLens : requiert HoloLens 2

>[!NOTE]
> La résolution et la cadence de l’interface utilisateur de la caméra MRC intégrée peuvent être réduites par rapport à leurs valeurs normales lorsqu’une autre application utilise la caméra photo/vidéo.

#### <a name="mrc-access"></a>Accès MRC

Avec la mise à jour 2018 d’avril de Windows 10, il n’existe plus de limitation concernant plusieurs applications qui accèdent au flux MRC (Toutefois, l’accès à la caméra photo/vidéo présente toujours des limites).

Avant la mise à jour 2018 de Windows 10 avril, l’enregistreur MRC personnalisé d’une application était mutuellement exclusif avec la MRC du système (capture de photos, capture de vidéos ou diffusion en continu à partir du portail de périphériques Windows).

## <a name="see-also"></a>Voir aussi

* [MRC (Mixed Reality Capture)](mixed-reality-capture.md)
* [Vue Spectateur](spectator-view.md)
* [Vue d’ensemble du développement Unity](unity-development-overview.md)
* [Vue d’ensemble du développement Unreal](unreal-development-overview.md)
