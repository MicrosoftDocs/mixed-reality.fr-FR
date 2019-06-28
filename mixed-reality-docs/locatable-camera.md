---
title: Appareil photo localisable
description: Informations générales sur la caméra HoloLens, son fonctionnement et les profils et les solutions disponibles pour les développeurs.
author: cdedmonds
ms.author: wguyman, cdedmonds
ms.date: 06/12/2019
ms.topic: article
keywords: appareil photo, hololens, appareil photo de couleur, front face, hololens 2, cv, vision par ordinateur, repère, marqueurs, code qr, qr, photo, vidéo
ms.openlocfilehash: e4e7fce50ec2865650b6b7cbafa59af8819d220c
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67415265"
---
# <a name="locatable-camera"></a>Appareil photo localisable

HoloLens inclut une caméra world à l’avant de l’appareil qui permet aux applications voir ce que voit l’utilisateur. Les développeurs ont accès et le contrôle de l’appareil photo comme ils le feraient pour des caméras de couleur sur les smartphones, les ordinateurs portables et postes de travail. Les mêmes fenêtres universelles [de capture de média](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.mediacapture.aspx) et windows media API qui fonctionnent sur desktop et mobile travaux sur HoloLens. Unity [a encapsulé également ces API windows](locatable-camera-in-unity.md) d’abstraire la simple utilisation de la caméra sur HoloLens pour des tâches comme prenant régulières photos et vidéos (avec ou sans hologrammes) et de localisation du point de vue et la position de la caméra dans sur le scène.

## <a name="device-camera-information"></a>Informations sur l’appareil photo

### <a name="hololens-first-generation"></a>HoloLens (première génération)

* Focus fixe photo / (PV) caméra vidéo avec balance des blancs, exposition auto et pipeline de traitement complet de l’image.
* LED de confidentialité blanc accessible sur le monde s’allume chaque fois que l’appareil photo est active
* L’appareil photo prend en charge les modes suivants (tous les modes sont proportions 16:9) à 30, 24, 20, 15 et 5 i/s :

  |  Vidéo  |  Preview  |  Toujours  |  Champ de vision horizontal (H-angle d’ouverture) |  Utilisation suggérée | 
  |----------|----------|----------|----------|----------|
  |  1280 x 720 |  1280 x 720 |  1280 x 720 |  45deg  |  (mode par défaut avec une stabilisation vidéo) | 
  |  N/A |  N/A |  2048x1152 |  67deg |  Image toujours la résolution plus élevée | 
  |  1408x792 |  1408x792 |  1408x792 |  48deg |  Résolution de surbalayage (remplissage) avant une stabilisation vidéo | 
  |  1344x756 |  1344x756 |  1344x756 |  67deg |  Mode vidéo de grand angle d’ouverture avec surbalayage | 
  |  896x504 |  896x504 |  896x504 |  48deg |  Basse consommation / tâches de traitement du mode de faible résolution d’image | 

### <a name="hololens-2"></a>HoloLens 2

* Autofocus photo / (PV) caméra vidéo avec balance des blancs, exposition auto et pipeline de traitement complet de l’image.
* LED de confidentialité blanc accessible sur le monde s’allume chaque fois que l’appareil photo est active.
* HoloLens 2 prend en charge les profils d’appareil photo différents. Découvrez comment [découvrir et sélectionner les fonctionnalités d’appareil photo](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/camera-profiles).
* L’appareil photo prend en charge les profils et les résolutions (tous les modes vidéo sont proportions 16:9) suivants :
  
  | Profil                                         | Vidéo     | Preview   | Toujours     | Fréquences d’images | Champ de vision horizontal (H-angle d’ouverture) | Utilisation suggérée                             |
  |-------------------------------------------------|-----------|-----------|-----------|-------------|----------------------------------|---------------------------------------------|
  | Legacy,0  BalancedVideoAndPhoto,100             | 2272x1278 | 2272x1278 |           | 15,30       | 64.69                            | Enregistrement vidéo de haute qualité                |
  | Legacy,0  BalancedVideoAndPhoto,100             |           |           | 3904x2196 |             | 64.69                            | Capture d’images de haute qualité                  |
  | BalancedVideoAndPhoto,120                       | 1952x1100 | 1952x1100 | 1952x1100 | 15,30       | 64.69                            | Scénarios de longue durée                     |
  | BalancedVideoAndPhoto,120                       | 1504x846  | 1504x846  |           | 15,30       | 64.69                            | Scénarios de longue durée                     |
  | Vidéoconférence, 100                           | 1952x1100 | 1952x1100 | 1952x1100 | 15,30,60    | 64.69                            | Conférence vidéo, les scénarios de longue durée |
  | Vidéoconférence, 100                           | 1504x846  | 1504x846  |           | 5,15,30,60  | 64.69                            | Conférence vidéo, les scénarios de longue durée |
  | Vidéoconférence, 100 BalancedVideoAndPhoto, 120 | 1920x1080 | 1920x1080 | 1920x1080 | 15,30       | 64.69                            | Conférence vidéo, les scénarios de longue durée |
  | Vidéoconférence, 100 BalancedVideoAndPhoto, 120 | 1280 x 720  | 1280 x 720  | 1280 x 720  | 15,30       | 64.69                            | Conférence vidéo, les scénarios de longue durée |
  | Vidéoconférence, 100 BalancedVideoAndPhoto, 120 | 1128 x 635  |           |           | 15,30       | 64.69                            | Conférence vidéo, les scénarios de longue durée |
  | Vidéoconférence, 100 BalancedVideoAndPhoto, 120 | 960 x 540   |           |           | 15,30       | 64.69                            | Conférence vidéo, les scénarios de longue durée |
  | Vidéoconférence, 100 BalancedVideoAndPhoto, 120 | 760x428   |           |           | 15,30       | 64.69                            | Conférence vidéo, les scénarios de longue durée |
  | Vidéoconférence, 100 BalancedVideoAndPhoto, 120 | 640 x 360   |           |           | 15,30       | 64.69                            | Conférence vidéo, les scénarios de longue durée |
  | Vidéoconférence, 100 BalancedVideoAndPhoto, 120 | 500 x 282   |           |           | 15,30       | 64.69                            | Conférence vidéo, les scénarios de longue durée |
  | Vidéoconférence, 100 BalancedVideoAndPhoto, 120 | 424 x 240   |           |           | 15,30       | 64.69                            | Conférence vidéo, les scénarios de longue durée |

>[!NOTE]
>Les clients peuvent exploiter [mixte de capture de la réalité](mixed-reality-capture.md) à prendre des photos de votre application, notamment hologrammes et stabilisation vidéo ou de vidéos.
>
>En tant que développeur, voici les considérations que vous devez prendre en compte lors de la création de votre application si vous souhaitez qu’il recherche aussi bon que possible lorsqu’un client capture le contenu. Vous pouvez également activer (et personnaliser) la capture de réalité mixte de directement au sein de votre application. En savoir plus sur [mixte de capture de la réalité pour les développeurs](mixed-reality-capture-for-developers.md).

## <a name="locating-the-device-camera-in-the-world"></a>Localisation de l’appareil photo dans le monde

Quand HoloLens prend les photos et vidéos, les frames capturés incluent l’emplacement de l’appareil photo dans le monde, ainsi que le modèle d’objectif de l’appareil photo. Cela permet aux applications de raisonner à propos de la position de la caméra dans le monde réel pour les scénarios de création d’images augmentées. Les développeurs de manière créative peuvent avoir un impact leurs propres scénarios à l’aide de leur traitement d’image préféré ou des bibliothèques de vision par ordinateur personnalisé.

« Photo » ailleurs dans la documentation de HoloLens peut-être faire référence à la « jeu caméra virtuelle » (le frustum l’application effectue le rendu à). À moins qu’indiqué dans le cas contraire, « photo » sur cette page fait référence à la caméra de couleur RVB réelles.

Les détails sur ce garde de page à l’aide de la [MediaFrameReference](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.frames.mediaframereference) toutefois il existe également des API pour extraction caméra intrinsèques et les emplacements à l’aide de la classe [Media Foundation attributs](https://msdn.microsoft.com/library/windows/desktop/mt740395(v=vs.85).aspx). Reportez-vous à la [exemple de suivi de visage HOLOGRAPHIQUE](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking) pour plus d’informations.

### <a name="images-with-coordinate-systems"></a>Images de systèmes de coordonnées

Chaque trame d’image (si photo ou vidéo) inclut un [SpatialCoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem) racine est à l’appareil photo au moment de la capture, qui est accessible à l’aide de la [CoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.frames.mediaframereference.coordinatesystem#Windows_Media_Capture_Frames_MediaFrameReference_CoordinateSystem) propriété de votre [MediaFrameReference](https://docs.microsoft.com/en-us/uwp/api/Windows.Media.Capture.Frames.MediaFrameReference). En outre, chaque image contient une description du modèle d’objectif de caméra qui se trouve dans le [CameraIntrinsics](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.frames.videomediaframe.cameraintrinsics#Windows_Media_Capture_Frames_VideoMediaFrame_CameraIntrinsics) propriété. Ensemble, ces transformations définissent pour chaque pixel un rayon dans l’espace 3D représentant le chemin emprunté par photons qui a généré le pixel. Ces rayons peuvent être associées à d’autres contenus dans l’application en obtenant la transformation à partir du système de coordonnées de l’image à un autre système de coordonnées (par exemple, à partir d’un [de référence stationnaire](coordinate-systems.md#stationary-frame-of-reference)). Pour résumer, chaque trame d’image offre les avantages suivants :
* Données de pixels (au format de RVB/NV12/JPEG/etc.)
* Un [SpatialCoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem) à partir de l’emplacement de la capture
* Un [CameraIntrinsics](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.frames.videomediaframe.cameraintrinsics#Windows_Media_Capture_Frames_VideoMediaFrame_CameraIntrinsics) classe contenant le mode de filtre de l’appareil photo

### <a name="camera-to-application-specified-coordinate-system"></a>Appareil photo pour le système de coordonnées spécifié par l’Application

Pour accéder à partir de la « CameraIntrinsics » et « CameraCoordinateSystem » à votre système de coordonnées de monde d’application, vous devez les éléments suivants :

[Caméra localisable dans Unity](locatable-camera-in-unity.md): CameraToWorldMatrix est automatiquement fournie par PhotoCaptureFrame classe (de sorte que vous n’avez pas besoin de vous soucier de transformations CameraCoordinateSystem).

[Caméra localisable dans DirectX](locatable-camera-in-directx.md): Explique comment procéder à la requête pour la transformation entre le système de coordonnées de la caméra et votre propre coordinate system(s) application assez simple.

### <a name="distortion-error"></a>Erreur de distorsion

Sur HoloLens, les flux de l’image vidéo et toujours sont sans distorsion dans le pipeline de traitement d’image du système avant que les trames sont rendus disponibles pour l’application (le flux d’aperçu contient les images déformées d’origine). Car uniquement les CameraIntrinsics sont mis à disposition, applications doivent supposer image frames représentent une caméra STÉNOPÉIQUE parfait, cependant l’undistortion fonctionne dans le processeur d’images peut toujours laisser une erreur de jusqu'à 10 pixels sur HoloLens (première génération) Lorsque vous utilisez le CameraIntrinsics dans les métadonnées de frame. Dans de nombreux cas d’utilisation, cette erreur sera a pas d’importance, mais si vous alignez hologrammes au monde réel affiches/marqueurs, par exemple, et que vous remarquez une < 10px décalage (environ 11mm pour hologrammes positionné 2 mètres) cette altération peut être provoqué par erreur. 

## <a name="locatable-camera-usage-scenarios"></a>Scénarios d’utilisation de caméra localisables

### <a name="show-a-photo-or-video-in-the-world-where-it-was-captured"></a>Afficher une photo ou une vidéo dans le monde dans lequel elle a été capturée

Les images de l’appareil photo sont fournis avec une transformation « Appareil photo pour World », qui peut être utilisée pour afficher exactement où l’appareil a ou non lorsque l’image a été effectuée. Par exemple, vous pouvez placer une petite icône HOLOGRAPHIQUE à cet emplacement (CameraToWorld.MultiplyPoint(Vector3.zero)) et même dessin une petite flèche située dans la direction que l’appareil photo a été confronté (CameraToWorld.MultiplyVector(Vector3.forward)).

### <a name="tag--pattern--poster--object-tracking"></a>Balise / modèle / Poster / suivi d’objet

De nombreuses applications de réalité mixte utilisent une image reconnaissable ou un modèle visual pour créer un point traçable dans l’espace. Cela permet ensuite de restituer les objets par rapport à qui pointent ou créer un emplacement connu. Certaines utilisations pour HoloLens incluent recherche un objet du monde réel balisé avec rétrospectif (par exemple, un téléviseur avec un code QR), plaçant hologrammes sur rétrospectif et visuellement un appariement avec les appareils non HoloLens tels que des tablettes qui ont été configuré pour communiquer avec HoloLens via Wi-Fi.

Pour reconnaître un modèle visual, puis placer cet objet dans l’espace universel des applications, vous aurez besoin de quelques éléments :
1. Une image modèle reconnaissance boîte à outils, tels que le code QR, AR balises, visage, de traceurs du cercle, etc. de la reconnaissance optique de caractères.
2. Collecter les trames d’images lors de l’exécution et les passer à la couche de reconnaissance
3. Unproject leurs emplacements d’image au monde, ou les positions des rayons world probable. Consultez l'article
4. Placez vos modèles virtuels sur ces emplacements du monde

Certains liens de traitement important d’image :
* [OpenCV](http://opencv.org/)
* [QR balises](https://en.wikipedia.org/wiki/QR_code)
* [FaceSDK](http://research.microsoft.com/projects/facesdk/)
* [Microsoft Translator](https://www.microsoft.com/translator/business)

En conservant une fréquence d’images application interactive est cruciale, particulièrement lorsque vous traitez des algorithmes de reconnaissance d’image longs. Pour cette raison, nous utilisons généralement au format suivant :
1. Thread principal : gère l’objet caméra
2. Thread principal : demandes nouvelles images (asynchrone)
3. Thread principal : passer des nouvelles images au thread de suivi
4. Suivi de Thread : image de processus pour collecter des points clés
5. Thread principal : déplace le modèle virtuel en fonction de trouvé les points clés
6. Thread principal : Répétez les étapes 2

Certains systèmes de marqueur d’image fournissent uniquement un emplacement de pixel unique (d’autres fournissent la transformation complet auquel cas cette section n’est pas nécessaire), ce qui équivaut à un rayon des emplacements possibles. Pour accéder à un seul emplacement 3d, nous pouvons ensuite tirer parti de plusieurs rayons et trouver le résultat final en leur intersection approximative. Pour ce faire, vous aurez besoin à :
1. Obtenir une boucle va collecter plusieurs images de l’appareil photo
2. Rechercher les points de fonction associé et leurs rayons world
3. Lorsque vous disposez d’un dictionnaire des fonctionnalités, chacune avec plusieurs rayons de monde, vous pouvez utiliser le code suivant à l’intersection de ces rayons résoudre :

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

Étant donné deux ou plusieurs emplacements de balise de suivi, vous pouvez positionner une scène modelled selon le scénario actuel d’utilisateurs. Si vous ne pouvez pas supposer gravité, vous aurez besoin des trois emplacements de balise. Dans de nombreux cas, que nous utilisons un modèle de couleurs simple où sphères blanches représentent en temps réel suivies des emplacements de balise et sphères bleu représentent des emplacements de balise modélisées, cela permet à l’utilisateur à évaluer visuellement la qualité d’alignement. Nous partons du principe dans toutes les applications de nos la configuration suivante :
* Deux ou plusieurs emplacements de balise modélisées
* Un « espace d’étalonnage », qui est le parent des balises dans la scène
* Identificateur de la fonctionnalité appareil photo
* Comportement qui déplace l’espace d’étalonnage pour aligner les balises modelled avec les balises en temps réel (nous sommes prudent déplacer l’espace de parent, pas les marqueurs modelled eux-mêmes, étant donné que les autres connect est les positions par rapport à leur).

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

### <a name="track-or-identify-tagged-stationary-or-moving-real-world-objectsfaces-using-leds-or-other-recognizer-libraries"></a>Suivre ou identifier balisés stationnaire ou déplacement réel objets/des visages à l’aide des voyants ou autres bibliothèques de module de reconnaissance

Exemples :
* Les robots industriels avec voyants (ou les codes QR pour un déplacement plus lent des objets)
* Identifier et reconnaître les objets dans la salle
* Identifier et reconnaître les personnes dans la salle (par exemple, place HOLOGRAPHIQUE cartes de contact sur les visages)

## <a name="see-also"></a>Voir aussi
* [Appareil photo localisable dans DirectX](locatable-camera-in-directx.md)
* [Appareil photo localisable dans Unity](locatable-camera-in-unity.md)
* [Capture de Réalité Mixte](mixed-reality-capture.md)
* [Capture de Réalité Mixte pour les développeurs](mixed-reality-capture-for-developers.md)
* [Présentation de capture de média](https://msdn.microsoft.com/library/windows/apps/mt243896.aspx)
* [Exemple de suivi de visage HOLOGRAPHIQUE](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/HolographicFaceTracking)
