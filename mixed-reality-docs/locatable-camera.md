---
title: Appareil photo localisable
description: Informations générales sur la caméra HoloLens frontale, son fonctionnement et les profils et résolutions disponibles pour les développeurs.
author: cdedmonds
ms.author: wguyman, cdedmonds
ms.date: 06/12/2019
ms.topic: article
keywords: appareil photo, hololens, caméra couleur, frontal, hololens 2, CV, vision par ordinateur, fiduciaire, marqueurs, code QR, QR, photo, vidéo
ms.openlocfilehash: 368943dd70c721a41ca7c265a19ecb7c394db312
ms.sourcegitcommit: 4ac761fed7a9570977f6d031ba4f870585d6630a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68861724"
---
# <a name="locatable-camera"></a>Appareil photo localisable

HoloLens intègre une caméra universelle montée sur l’avant de l’appareil, ce qui permet aux applications de voir ce que l’utilisateur voit. Les développeurs ont accès à l’appareil photo et le contrôle de ce dernier, tout comme pour les caméras couleur sur les smartphones, les ordinateurs portables ou les ordinateurs de bureau. Les mêmes API Universal Windows [Media capture](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.mediacapture.aspx) et Windows Media Foundation qui fonctionnent sur les appareils mobiles et de bureau sur HoloLens. Unity [a également encapsulé ces API Windows](locatable-camera-in-unity.md) pour simplifier l’utilisation simple de l’appareil photo sur HoloLens pour des tâches telles que la mise en place de photos et vidéos normales (avec ou sans hologrammes) et la localisation de la caméra dans et la perspective sur la scène.

## <a name="device-camera-information"></a>Informations sur l’appareil photo

### <a name="hololens-first-generation"></a>HoloLens (première génération)

* Correction de l’appareil photo/vidéo (PV) avec balance des blancs automatique, exposition automatique et pipeline de traitement d’image complète.
* La lumière blanche sur la confidentialité dans le monde s’illumine quand l’appareil photo est actif
* L’appareil photo prend en charge les modes suivants (tous les modes sont des proportions 16:9) à 30, 24, 20, 15 et 5 i/s:

  |  Vidéo  |  Preview  |  Subsist  |  Champ horizontal de l’affichage (H-angle d’affichage) |  Utilisation suggérée | 
  |----------|----------|----------|----------|----------|
  |  1280 x 720 |  1280 x 720 |  1280 x 720 |  45deg  |  (mode par défaut avec stabilisation vidéo) | 
  |  N/A |  N/A |  2048x1152 |  67deg |  Image toujours la plus haute résolution | 
  |  1408x792 |  1408x792 |  1408x792 |  48deg |  Résolution de suranalyse (remplissage) avant la stabilisation vidéo | 
  |  1344x756 |  1344x756 |  1344x756 |  67deg |  Mode vidéo grand angle avec suranalyse | 
  |  896x504 |  896x504 |  896x504 |  48deg |  Mode faible puissance/faible résolution pour les tâches de traitement des images | 

### <a name="hololens-2"></a>HoloLens 2

* Appareil photo/vidéo (PV) de focalisation automatique avec balance des blancs automatique, exposition automatique et pipeline de traitement d’image complète.
* La lumière blanche sur la confidentialité dans le monde s’illumine quand l’appareil photo est actif.
* HoloLens 2 prend en charge différents profils d’appareil photo. Découvrez comment [découvrir et sélectionner les fonctionnalités de l’appareil photo](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/camera-profiles).
* L’appareil photo prend en charge les profils et résolutions suivants (tous les modes vidéo sont des proportions 16:9):
  
  | Profil                                         | Vidéo     | Preview   | Subsist     | Fréquences d’images | Champ horizontal de l’affichage (H-angle d’affichage) | Utilisation suggérée                             |
  |-------------------------------------------------|-----------|-----------|-----------|-------------|----------------------------------|---------------------------------------------|
  | Hérité, 0 BalancedVideoAndPhoto, 100             | 2272x1278 | 2272x1278 |           | 15, 30       | 64,69                            | Enregistrement vidéo de haute qualité                |
  | Hérité, 0 BalancedVideoAndPhoto, 100             | 896x504   | 896x504   |           | 15, 30       | 64,69                            | Aperçu du flux pour la capture de photos de haute qualité |
  | Hérité, 0 BalancedVideoAndPhoto, 100             |           |           | 3904x2196 |             | 64,69                            | Capture photo de haute qualité                  |
  | BalancedVideoAndPhoto, 120                       | 1952x1100 | 1952x1100 | 1952x1100 | 15, 30       | 64,69                            | Scénarios de longue durée                     |
  | BalancedVideoAndPhoto, 120                       | 1504x846  | 1504x846  |           | 15, 30       | 64,69                            | Scénarios de longue durée                     |
  | Visioconférence, 100                           | 1952x1100 | 1952x1100 | 1952x1100 | 15, 30, 60    | 64,69                            | Vidéoconférence, scénarios de longue durée |
  | Visioconférence, 100                           | 1504x846  | 1504x846  |           | 5, 15, 30, 60  | 64,69                            | Vidéoconférence, scénarios de longue durée |
  | Visioconférence, 100 BalancedVideoAndPhoto, 120 | 1920x1080 | 1920x1080 | 1920x1080 | 15, 30       | 64,69                            | Vidéoconférence, scénarios de longue durée |
  | Visioconférence, 100 BalancedVideoAndPhoto, 120 | 1280 x 720  | 1280 x 720  | 1280 x 720  | 15, 30       | 64,69                            | Vidéoconférence, scénarios de longue durée |
  | Visioconférence, 100 BalancedVideoAndPhoto, 120 | 1128x636  |           |           | 15, 30       | 64,69                            | Vidéoconférence, scénarios de longue durée |
  | Visioconférence, 100 BalancedVideoAndPhoto, 120 | 960 x 540   |           |           | 15, 30       | 64,69                            | Vidéoconférence, scénarios de longue durée |
  | Visioconférence, 100 BalancedVideoAndPhoto, 120 | 760x428   |           |           | 15, 30       | 64,69                            | Vidéoconférence, scénarios de longue durée |
  | Visioconférence, 100 BalancedVideoAndPhoto, 120 | 640 x 360   |           |           | 15, 30       | 64,69                            | Vidéoconférence, scénarios de longue durée |
  | Visioconférence, 100 BalancedVideoAndPhoto, 120 | 500x282   |           |           | 15, 30       | 64,69                            | Vidéoconférence, scénarios de longue durée |
  | Visioconférence, 100 BalancedVideoAndPhoto, 120 | 424x240   |           |           | 15, 30       | 64,69                            | Vidéoconférence, scénarios de longue durée |

>[!NOTE]
>Les clients peuvent tirer parti de la capture de la [réalité mixte](mixed-reality-capture.md) pour prendre des vidéos ou des photos de votre application, notamment des hologrammes et une stabilisation vidéo.
>
>En tant que développeur, vous devez tenir compte de certaines considérations lors de la création de votre application si vous souhaitez qu’elle apparaisse aussi bonne que possible quand un client capture du contenu. Vous pouvez également activer (et personnaliser) la capture de la réalité mixte à partir de directement dans votre application. En savoir plus sur la [capture de la réalité mixte pour les développeurs](mixed-reality-capture-for-developers.md).

## <a name="locating-the-device-camera-in-the-world"></a>Localisation de l’appareil photo de l’appareil dans le monde

Lorsque HoloLens prend des photos et des vidéos, les images capturées incluent l’emplacement de la caméra dans le monde, ainsi que le modèle de lentille de l’appareil photo. Cela permet aux applications de connaître la position de la caméra dans le monde réel pour les scénarios de création d’images augmentés. Les développeurs peuvent déployer de manière créative leurs propres scénarios à l’aide de leur traitement d’image préféré ou de leurs bibliothèques de vision d’ordinateur personnalisées.

La «caméra» dans la documentation HoloLens peut faire référence à la «caméra de jeu virtuelle» (le frustum rendu de l’application à). Sauf indication contraire, «Camera» sur cette page fait référence à la caméra de couleurs RVB réelle.

Les détails de cette page traitent de l’utilisation de la classe [MediaFrameReference](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.frames.mediaframereference) . Toutefois, il existe également des API permettant d’extraire des emplacements et des intrinsèques de caméra à l’aide d' [attributs Media Foundation](https://msdn.microsoft.com/library/windows/desktop/mt740395(v=vs.85).aspx). Pour plus d’informations, reportez-vous à l' [exemple de suivi de visage holographique](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking) .

### <a name="images-with-coordinate-systems"></a>Images avec systèmes de coordonnées

Chaque image (qu’il s’agisse de photo ou de vidéo) comprend un [SpatialCoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem) enraciné à l’appareil photo au moment de la capture, qui est accessible à l’aide de la propriété [CoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.frames.mediaframereference.coordinatesystem#Windows_Media_Capture_Frames_MediaFrameReference_CoordinateSystem) de votre [MediaFrameReference](https://docs.microsoft.com/en-us/uwp/api/Windows.Media.Capture.Frames.MediaFrameReference). En outre, chaque cadre contient une description du modèle d’objectif de l’appareil photo, qui se trouve dans la propriété [CameraIntrinsics](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.frames.videomediaframe.cameraintrinsics#Windows_Media_Capture_Frames_VideoMediaFrame_CameraIntrinsics) . Ensemble, ces transformations définissent pour chaque pixel un rayon dans l’espace 3D représentant le chemin emprunté par les photons qui ont produit le pixel. Ces rayons peuvent être liés à d’autres contenus dans l’application en obtenant la transformation du système de coordonnées du cadre vers un autre système de coordonnées (par exemple, à partir d’une [image stationnaire de référence](coordinate-systems.md#stationary-frame-of-reference)). Pour résumer, chaque frame d’image fournit les éléments suivants:
* Données de pixels (au format RGB/NV12/JPEG/etc.)
* Un [SpatialCoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem) à partir de l’emplacement de capture
* Une classe [CameraIntrinsics](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.frames.videomediaframe.cameraintrinsics#Windows_Media_Capture_Frames_VideoMediaFrame_CameraIntrinsics) contenant le mode de l’objectif de l’appareil photo

### <a name="camera-to-application-specified-coordinate-system"></a>Appareil photo vers système de coordonnées spécifié par l’application

Pour passer de «CameraIntrinsics» et «CameraCoordinateSystem» à votre système de coordonnées de l’application/du monde, vous avez besoin des éléments suivants:

[Appareil photo localisable dans Unity](locatable-camera-in-unity.md): CameraToWorldMatrix est automatiquement fourni par la classe PhotoCaptureFrame (vous n’avez donc pas à vous soucier des transformations CameraCoordinateSystem).

[Appareil photo localisable dans DirectX](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking): L’exemple de suivi de visage holographique illustre la façon assez simple d’interroger la transformation entre le système de coordonnées de l’appareil photo et vos propres systèmes de coordonnées d’application.

### <a name="distortion-error"></a>Erreur de distorsion

Sur HoloLens, les flux vidéo et d’images fixes ne sont pas déformés dans le pipeline de traitement d’image du système avant que les frames ne soient mis à disposition de l’application (le flux de préversion contient les frames déformés d’origine). Étant donné que seules les CameraIntrinsics sont disponibles, les applications doivent supposer que les images d’images représentent une caméra Pinhole parfaite.

Sur HoloLens (première génération), la fonction de désdistortion dans le processeur d’images peut toujours provoquer une erreur pouvant atteindre 10 pixels lors de l’utilisation de CameraIntrinsics dans les métadonnées de frame. Dans de nombreux cas d’utilisation, cette erreur n’a pas d’importance, mais si vous alignez des hologrammes sur des affiches/marqueurs réels, par exemple, et que vous remarquez un décalage de < 10px (à peu près 11mm pour les hologrammes positionnés sur 2 mètres), cette erreur peut être due à une déformation. 

## <a name="locatable-camera-usage-scenarios"></a>Scénarios d’utilisation d’appareil photo localisables

### <a name="show-a-photo-or-video-in-the-world-where-it-was-captured"></a>Afficher une photo ou une vidéo dans le monde où elle a été capturée

Les cadres de l’appareil photo sont fournis avec une transformation «caméra à toute la vie», qui peut être utilisée pour indiquer exactement où se trouvait l’appareil lorsque l’image a été prise. Par exemple, vous pouvez positionner une petite icône holographique à cet emplacement (CameraToWorld. MultiplyPoint (Vector3. Zero)) et même dessiner une petite flèche dans la direction vers laquelle l’appareil photo était dirigée (CameraToWorld. MultiplyVector (Vector3. Forward)).

### <a name="tag--pattern--poster--object-tracking"></a>Étiquette/modèle/affiche/suivi d’objet

De nombreuses applications de réalité mixte utilisent une image ou un modèle visuel identifiable pour créer un point de suivi dans l’espace. Il est ensuite utilisé pour restituer des objets par rapport à ce point ou créer un emplacement connu. Certaines utilisations de HoloLens incluent la recherche d’un objet réel marqué avec des apparis (par exemple, un moniteur TV avec un code QR), le placement d’hologrammes sur des personnes fiduciaires et le couplage visuel avec des appareils non-HoloLens tels que des tablettes qui ont été configurés pour communiquer avec HoloLens via Wi-Fi.

Pour reconnaître un modèle visuel, puis placer cet objet dans l’espace universel des applications, vous avez besoin de quelques éléments:
1. Boîte à outils de reconnaissance de modèle d’image, telle que le code QR, les balises AR, le Finder de visages, les traceurs de cercle, la reconnaissance optique, etc.
2. Collecter les trames d’image au moment de l’exécution et les transmettre à la couche de reconnaissance
3. Déprojetez leurs emplacements d’images dans des positions universelles ou des rayons de monde probables. Consultez l'article
4. Positionner vos modèles virtuels sur ces emplacements mondiaux

Voici quelques liens importants sur le traitement des images:
* [OpenCV](http://opencv.org/)
* [Balises QR](https://en.wikipedia.org/wiki/QR_code)
* [FaceSDK](http://research.microsoft.com/projects/facesdk/)
* [Microsoft Translator](https://www.microsoft.com/translator/business)

Le maintien d’une fréquence d’images d’application interactive est essentiel, en particulier lors du traitement des algorithmes de reconnaissance d’images à long terme. Pour cette raison, nous utilisons généralement le modèle suivant:
1. Thread principal: gère l’objet Camera
2. Thread principal: demande de nouveaux frames (Async)
3. Thread principal: passer de nouveaux frames au thread de suivi
4. Thread de suivi: traite l’image pour collecter des points clés
5. Thread principal: déplace le modèle virtuel pour trouver les points clés trouvés
6. Thread principal: répéter à l’étape 2

Certains systèmes de marqueurs d’images ne fournissent qu’un seul emplacement de pixel (les autres fournissent la transformation complète, auquel cas cette section n’est pas nécessaire), qui équivaut à un rayon d’emplacements possibles. Pour atteindre un emplacement 3D unique, nous pouvons ensuite tirer parti de plusieurs rayons et trouver le résultat final en fonction de leur intersection approximative. Pour ce faire, vous devez:
1. Obtenir une boucle qui collecte plusieurs images d’appareil photo
2. Rechercher les points de fonctionnalités associés et leurs rayons mondiaux
3. Lorsque vous disposez d’un dictionnaire de fonctionnalités, chacun avec plusieurs rayons de monde, vous pouvez utiliser le code suivant pour résoudre l’intersection de ces rayons:

```
public static Vector3 ClosestPointBetweenRays(
   Vector3 point1, Vector3 normalizedDirection1,
   Vector3 point2, Vector3 normalizedDirection2) {
   float directionProjection = Vector3.Dot(normalizedDirection1, normalizedDirection2);
   if (directionProjection == 1) {
     return point1; // parallel lines
   }
   float projection1 = Vector3.Dot(point2 - point1, normalizedDirection1);
   float projection2 = Vector3.Dot(point2 - point1, normalizedDirection2);
   float distanceAlongLine1 = (projection1 - directionProjection * projection2) / (1 - directionProjection * directionProjection);
   float distanceAlongLine2 = (projection2 - directionProjection * projection1) / (directionProjection * directionProjection - 1);
   Vector3 pointOnLine1 = point1 + distanceAlongLine1 * normalizedDirection1;
   Vector3 pointOnLine2 = point2 + distanceAlongLine2 * normalizedDirection2;
   return Vector3.Lerp(pointOnLine2, pointOnLine1, 0.5f);
 }
```

À partir de deux ou plusieurs emplacements d’étiquette suivis, vous pouvez positionner une scène modélisée pour l’adapter au scénario actuel des utilisateurs. Si vous ne pouvez pas supposer la gravité, vous aurez besoin de trois emplacements de balises. Dans de nombreux cas, nous utilisons un modèle de couleurs simple où les blancs représentent les emplacements de balises suivi en temps réel, et les sphères bleues représentent les emplacements de balise modélisés, ce qui permet à l’utilisateur de mesurer visuellement la qualité d’alignement. Nous supposons l’installation suivante dans toutes nos applications:
* Deux ou plusieurs emplacements de balise modélisés
* Un «espace d’étalonnage» qui, dans la scène, est le parent des balises
* Identificateur de la fonctionnalité de l’appareil photo
* Comportement qui déplace l’espace d’étalonnage pour aligner les balises modélisées avec les balises en temps réel (nous sommes prudents de déplacer l’espace parent, et non les marqueurs modélisés, car d’autres connexions sont des positions relatives à eux).

```
// In the two tags case:
 Vector3 idealDelta = (realTags[1].EstimatedWorldPos - realTags[0].EstimatedWorldPos);
 Vector3 curDelta = (modelledTags[1].transform.position - modelledTags[0].transform.position);
 if (IsAssumeGravity) {
   idealDelta.y = 0;
   curDelta.y = 0;
 }
 Quaternion deltaRot = Quaternion.FromToRotation(curDelta, idealDelta);
 trans.rotation = Quaternion.LookRotation(deltaRot * trans.forward, trans.up);
 trans.position += realTags[0].EstimatedWorldPos - modelledTags[0].transform.position;
```

### <a name="track-or-identify-tagged-stationary-or-moving-real-world-objectsfaces-using-leds-or-other-recognizer-libraries"></a>Suivre ou identifier des objets/visages à l’aide de voyants ou d’autres bibliothèques de reconnaissance

Exemples :
* Robots industriels avec del (ou codes QR pour des objets en déplacement plus lents)
* Identifier et reconnaître des objets dans la salle
* Identifier et reconnaître les personnes de la pièce (par exemple, placer des cartes de contact holographiques sur des visages)

## <a name="see-also"></a>Voir aussi
* [Exemple d’appareil photo localisable](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking)
* [Appareil photo localisable dans Unity](locatable-camera-in-unity.md)
* [Capture de Réalité Mixte](mixed-reality-capture.md)
* [Capture de Réalité Mixte pour les développeurs](mixed-reality-capture-for-developers.md)
* [Présentation de la capture multimédia](https://msdn.microsoft.com/library/windows/apps/mt243896.aspx)
* [Exemple de suivi de visage holographique](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking)
