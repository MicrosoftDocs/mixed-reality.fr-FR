---
title: Appareil photo localisable
description: Informations générales sur le HoloLens accessible sur appareil photo.
author: wguyman
ms.author: wguyman
ms.date: 02/24/2019
ms.topic: article
keywords: appareil photo, hololens, appareil photo de couleur, accessible sur des serveurs frontaux
ms.openlocfilehash: ffcd6faf15dd8556db393237d468a3cdf60e4bdb
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596323"
---
# <a name="locatable-camera"></a>Appareil photo localisable

HoloLens inclut une caméra world à l’avant de l’appareil qui permet aux applications voir ce que voit l’utilisateur. Les développeurs ont accès et le contrôle de l’appareil photo comme ils le feraient pour des caméras de couleur sur les smartphones, les ordinateurs portables et postes de travail. Les mêmes fenêtres universelles [de capture de média](https://msdn.microsoft.com/library/windows/apps/windows.media.capture.mediacapture.aspx) et windows media API qui fonctionnent sur desktop et mobile travaux sur HoloLens. Unity [a encapsulé également ces API windows](locatable-camera-in-unity.md) d’abstraire la simple utilisation de la caméra sur HoloLens pour des tâches comme prenant régulières photos et vidéos (avec ou sans hologrammes) et de localisation du point de vue et la position de la caméra dans sur le scène.

## <a name="device-camera-information"></a>Informations sur l’appareil photo

### <a name="hololens-first-generation"></a>HoloLens (première génération)

* Appareil photo de photo/vidéo (PV) fixe le focus, en balance des blancs exposition auto et canal de traitement complet de l’image
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

* Appareil photo de photo/vidéo (PV) autofocus, en balance des blancs exposition auto et canal de traitement complet de l’image
* LED de confidentialité blanc accessible sur le monde s’allume chaque fois que l’appareil photo est active
* L’appareil photo prend en charge les modes suivants (tous les modes vidéo sont proportions 16:9) :

  >[!NOTE]
  >Ces modes sont susceptibles d’être modifiées avant la disponibilité générale de HoloLens 2.

  |  Vidéo  |  Preview  |  Toujours  |  Fréquences d’images  |  Champ de vision horizontal (H-angle d’ouverture) |  Utilisation suggérée | 
  |----------|----------|----------|----------|----------|----------|
  |  1920x1080 |  1920x1080 |  N/A |  30, 15 i/s  |  54deg  |  (mode par défaut avec une stabilisation vidéo) | 
  |  N/A |  N/A |  3904X2196 |  N/A  |  64deg |  Image toujours la résolution plus élevée | 
  |  2272x1278 |  2272x1278 |  N/A |  30, 15 i/s  |  64deg |  Résolution de surbalayage (remplissage) avant une stabilisation vidéo | 
  |  1952x1100 |  1952x1100 |  1952x1100  |  30, 15 i/s  |  64deg |  Qualité de diffusion en continu | 
  |  1280 x 720 |  1280 x 720 |  N/A |  30, 15, 5 i/s  |  64deg |  Mode alimentation basse/résolution pour la diffusion en continu et les tâches de traitement d’images | 

## <a name="locating-the-device-camera-in-the-world"></a>Localisation de l’appareil photo dans le monde

Quand HoloLens prend les photos et vidéos, les frames capturés incluent l’emplacement de l’appareil photo dans le monde, ainsi que la projection de perspective de l’appareil photo. Cela permet aux applications de raisonner à propos de la position de la caméra dans le monde réel pour les scénarios de création d’images augmentées. Les développeurs de manière créative peuvent avoir un impact leurs propres scénarios à l’aide de leur traitement d’image préféré ou des bibliothèques de vision par ordinateur personnalisé.

« Photo » ailleurs dans la documentation de HoloLens peut-être faire référence à la « jeu caméra virtuelle » (le frustum l’application effectue le rendu à). À moins qu’indiqué dans le cas contraire, « photo » sur cette page fait référence à la caméra de couleur RVB réelles.

Les détails sur cette traitent de la page [Media Foundation attributs](https://msdn.microsoft.com/library/windows/desktop/mt740395(v=vs.85).aspx), cependant, il existe également des API pour extraire la caméra à l’aide de fonctions intrinsèques [WinRT APIs](https://msdn.microsoft.com/library/windows/apps/windows.media.devices.core.cameraintrinsics).  

### <a name="images-with-coordinate-systems"></a>Images de systèmes de coordonnées

Chaque trame d’image (si photo ou vidéo) inclut un système de coordonnées, ainsi que les deux transformations importantes. La « vue » transformer des mappages depuis le système de coordonnées fourni à l’appareil photo et « projection » est mappé à partir de l’appareil photo pixels dans l’image. Ensemble, ces transformations définissent pour chaque pixel un rayon dans l’espace 3D représentant le chemin emprunté par photons qui a généré le pixel. Ces rayons peuvent être associées à d’autres contenus dans l’application en obtenant la transformation à partir du système de coordonnées de l’image à un autre système de coordonnées (par exemple, à partir d’un [de référence stationnaire](coordinate-systems.md#stationary-frame-of-reference)). Pour résumer, chaque trame d’image offre les avantages suivants :
* Données de pixels (au format de RVB/NV12/JPEG/etc.)
* 3 éléments de métadonnées (stockées en tant que [IMFAttributes](https://msdn.microsoft.com/library/windows/desktop/ms704598(v=vs.85).aspx)) qui font de chaque image « localisables » :

|  Nom d'attribut  |  Type  |  GUID  |  Description | 
|----------|----------|----------|----------|
|  MFSampleExtension_Spatial_CameraCoordinateSystem  |  IUnknown ([SpatialCoordinateSystem](https://msdn.microsoft.com/library/windows/apps/windows.perception.spatial.spatialcoordinatesystem.aspx))  |  {9D13C82F-2199-4E67-91CD-D1A4181F2534}  |  Stocke le [système de coordonnées](coordinate-systems-in-directx.md) de l’image capturée | 
|  MFSampleExtension_Spatial_CameraViewTransform  |  Objet BLOB ([Matrix4x4](https://msdn.microsoft.com/library/windows/apps/windows.foundation.numerics.matrix4x4.aspx))  |  {4E251FA4-830F-4770-859A-4B8D99AA809B}  |  Stocke la transformation extrinsèques de la caméra dans le système de coordonnées | 
|  MFSampleExtension_Spatial_CameraProjectionTransform  |  Objet BLOB ([Matrix4x4](https://msdn.microsoft.com/library/windows/apps/windows.foundation.numerics.matrix4x4.aspx))  |  {47F9FCB5-2A02-4F26-A477-792FDF95886A}  |  Stocke la transformation de projection de la caméra | 

La transformation de projection représente les propriétés intrinsèques (focale, centre de projection, incliner) de la glace mappé sur un plan de l’image qui s’étend de -1 à + 1 dans l’axe X et Y.

```
Matrix4x4 format          Terms
   m11 m12 m13 m14      fx    0   0   0
   m21 m22 m23 m24     skew  fy   0   0
   m31 m32 m33 m34      cx   cy   A  -1
   m41 m42 m43 m44       0    0   B   0
```

Différentes applications auront des différents systèmes de coordonnées. Voici une vue d’ensemble du flux pour localiser un pixel d’appareil photo pour une seule application :

![Transformations appliquées aux systèmes de coordonnées de caméra](images/pvcameratransform5-500px.png)

### <a name="camera-to-application-specified-coordinate-system"></a>Appareil photo pour le système de coordonnées spécifié par l’Application

Pour accéder à partir de la « CameraView » et « CameraCoordinateSystem » à votre système de coordonnées de monde d’application, vous devez les éléments suivants :

[Caméra localisable dans Unity](locatable-camera-in-unity.md): CameraToWorldMatrix est automatiquement fournie par PhotoCaptureFrame classe (de sorte que vous n’avez pas besoin de vous soucier de transformations CameraCoordinateSystem).

[Caméra localisable dans DirectX](locatable-camera-in-directx.md): Explique comment procéder à la requête pour la transformation entre le système de coordonnées de la caméra et votre propre coordinate system(s) application assez simple.

### <a name="application-specified-coordinate-system-to-pixel-coordinates"></a>Système de coordonnées spécifié par l’application en coordonnées de Pixel

Supposons que vous souhaitiez trouver ou dessiner à un emplacement 3d spécifique sur une image de l’appareil photo :

Les transformations de projection et d’affichage, pendant les deux 4x4 matrices, doivent servira légèrement différemment. À savoir une fois la Projection, un est « normaliser par w », cette étape supplémentaire dans la projection simule plusieurs emplacements 3d peuvent se retrouver en tant que le même emplacement 2d sur un écran (par exemple, tout le long d’un certain rayon s’affichera sur le même pixel). Par conséquent, points clés (code de nuanceur) :

```
// Usual 3d math:
 float4x4 WorldToCamera = inverse( CameraToWorld );
 float4 CameraSpacePos = mul( WorldToCamera, float4( WorldSpacePos.xyz, 1 ) ); // use 1 as the W component
 // Projection math:
 float4 ImagePosUnnormalized = mul( CameraProjection, float4( CameraSpacePos.xyz, 1 ) ); // use 1 as the W component
 float2 ImagePosProjected = ImagePosUnnormalized.xy / ImagePosUnnormalized.w; // normalize by W, gives -1 to 1 space
 float2 ImagePosZeroToOne = ( ImagePosProjected * 0.5 ) + float2( 0.5, 0.5 ); // good for GPU textures
 int2 PixelPos = int2( ImagePosZeroToOne.x * ImageWidth, ( 1 - ImagePosZeroToOne.y ) * ImageHeight ); // good for CPU textures
```

### <a name="pixel-to-application-specified-coordinate-system"></a>Pixel spécifié par l’Application de système de coordonnées

La transition de pixel des coordonnées de monde est un peu plus compliquée :

```
float2 ImagePosZeroToOne = float2( PixelPos.x / ImageWidth, 1.0 - (PixelPos.y / ImageHeight ) );
 float2 ImagePosProjected = ( ( ImagePosZeroToOne * 2.0 ) - float2(1,1) ); // -1 to 1 space
 float3 CameraSpacePos = UnProjectVector( Projection, float3( ImagePosProjected, 1) );
 float3 WorldSpaceRayPoint1 = mul( CameraToWorld, float4(0,0,0,1) ); // camera location in world space
 float3 WorldSpaceRayPoint2 = mul( CameraToWorld, CameraSpacePos ); // ray point in world space
```

Où nous définissons UnProject en tant que :

```
public static Vector3 UnProjectVector(Matrix4x4 proj, Vector3 to)
 {
   Vector3 from = new Vector3(0, 0, 0);
   var axsX = proj.GetRow(0);
   var axsY = proj.GetRow(1);
   var axsZ = proj.GetRow(2);
   from.z = to.z / axsZ.z;
   from.y = (to.y - (from.z * axsY.z)) / axsY.y;
   from.x = (to.x - (from.z * axsX.z)) / axsX.x;
   return from;
 }
```

Pour rechercher l’emplacement du monde réel d’un point, il vous faut : monde deux rayons et trouver leur intersection, ou une taille connue des points.

### <a name="distortion-error"></a>Erreur de distorsion

Sur HoloLens, les flux de l’image vidéo et toujours sont sans distorsion dans le pipeline de traitement d’image du système avant que les trames sont rendus disponibles pour l’application (le flux d’aperçu contient les images déformées d’origine). Étant donné qu’uniquement la matrice de projection est rendue disponible, applications doivent supposer image frames représentent une caméra STÉNOPÉIQUE parfait, cependant l’undistortion fonctionne dans le processeur d’images peut laisser toujours une erreur de jusqu'à 10 pixels lors de l’utilisation de la matrice de projection dans les métadonnées de frame. Dans de nombreux cas d’utilisation, cette erreur sera a pas d’importance, mais si vous alignez hologrammes au monde réel affiches/marqueurs, par exemple, et que vous remarquez une < 10px décalage (environ 11mm pour hologrammes positionné 2 mètres) cette altération peut être provoqué par erreur.

## <a name="locatable-camera-usage-scenarios"></a>Scénarios d’utilisation de caméra localisables

### <a name="show-a-photo-or-video-in-the-world-where-it-was-captured"></a>Afficher une photo ou une vidéo dans le monde dans lequel elle a été capturée

Les images de l’appareil photo sont fournis avec une transformation « Appareil photo pour World », qui peut être utilisée pour afficher exactement où l’appareil a ou non lorsque l’image a été effectuée. Par exemple, vous pouvez placer une petite icône HOLOGRAPHIQUE à cet emplacement (CameraToWorld.MultiplyPoint(Vector3.zero)) et même dessin une petite flèche située dans la direction que l’appareil photo a été confronté (CameraToWorld.MultiplyVector(Vector3.forward)).

### <a name="painting-the-world-using-a-camera-shader"></a>Peinture au monde à l’aide d’un nuanceur de caméra

Dans cette section, nous allons créer un matériau 'nuanceur' ce couleurs le monde selon où il est apparu dans la vue de l’appareil photo un appareil. Nous allons faire est effectivement que chaque vertex sera déterminer son emplacement relatif à l’appareil photo, puis chaque pixel utilisera la matrice de projection à la figure hors de l’image texel, il est associé. Enfin et si vous le souhaitez, nous allons fondu les angles de l’image pour la faire apparaître plus comme une mémoire de rêve de type :

```
// In the vertex shader:
 float4 worldSpace = mul( ObjectToWorld, float4( vertexPos.xyz, 1));
 float4 cameraSpace = mul( CameraWorldToLocal, float4(worldSpace.xyz, 1));

 // In the pixel shader:
 float4 unprojectedTex = mul( CameraProjection, float4( cameraSpace .xyz, 1));
 float2 projectedTex = (unprojectedTex.xy / unprojectedTex.w);
 float2 unitTexcoord = ((projectedTex * 0.5) + float4(0.5, 0.5, 0, 0));
 float4 cameraTextureColor = tex2D(_CameraTex, unitTexcoord);
 // Fade out edges for better look:
 float pctInView = saturate((1.0 - length(projectedTex.xy)) * 3.0);
 float4 finalColor = float4( cameraTextureColor.rgb, pctInView );
```

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
2. Rechercher la [fonctionnalité points associés](#pixel-to-application-specified-coordinate-system)et leurs rayons world
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

### <a name="render-holograms-from-the-cameras-position"></a>Restituer hologrammes à partir de la position de la caméra

Remarque: Si vous essayez de créer votre propre [mixte capture réalité (MRC)](mixed-reality-capture.md), qui fusionne hologrammes avec le flux de l’appareil photo, vous pouvez utiliser la [des effets MRC](mixed-reality-capture-for-developers.md) ou activer la propriété showHolograms dans [ Caméra localisable dans Unity](locatable-camera-in-unity.md).

Si vous souhaitez effectuer un rendu spécial directement sur le flux de l’appareil photo RVB, il est possible rendre hologrammes dans l’espace à partir de la position de la caméra synchronisée avec un flux vidéo afin de fournir un aperçu de l’enregistrement/live hologramme personnalisé.

Dans Skype, nous le faire pour afficher le client à distance à ce que voit l’utilisateur de HoloLens et leur permettre d’interagir avec les mêmes hologrammes. Avant d’envoyer sur chaque image vidéo via le service de Skype, nous extrayons les données de caméra correspondantes de chaque image. Nous empaquetez ensuite les métadonnées d’extrinsèques et intrinsèque de la caméra avec l’image vidéo et puis l’envoyer sur le service de Skype.

Côté réception, à l’aide de Unity, nous avons déjà synchronisées avec tous les hologrammes dans l’espace de l’utilisateur HoloLens en utilisant le même système de coordonnées. Cela nous permet à utiliser des métadonnées extrinsèques de la caméra pour placer la caméra de Unity dans l’emplacement exact dans le monde (par rapport à celui des hologrammes) l’utilisateur HoloLens a été permanent lors de cette image vidéo a été capturée, utilisez les informations intrinsèque de la caméra pour Vérifiez que la vue est le même.

Une fois l’appareil photo correctement configuré, nous avons combiné les hologrammes voit de l’appareil photo sur l’image que nous avons reçu de Skype, créez une vue de réalité mixte de ce que l’utilisateur HoloLens voit à l’aide de Graphics.Blit.

```cs
private void OnFrameReceived(Texture frameTexture, Vector3 cameraPosition, Quaternion cameraRotation, Matrix4x4 cameraProjectionMatrix)
{
    //set material that will be blitted onto the RenderTexture
    this.compositeMaterial.SetTexture(CompositeRenderer.CameraTextureMaterialProperty, frameTexture);
    //set the camera to be that of the HoloLens's device camera
    this.Camera.transform.position = cameraPosition;
    this.Camera.transform.rotation = cameraRotation;
    this.Camera.projectionMatrix = cameraProjectionMatrix;
    //trigger the Graphics's Blit now that the frame and camera are set up
    this.TextureReady = false;
}
private void OnRenderImage(RenderTexture source, RenderTexture destination)
{
    if (!this.TextureReady)
    {
        Graphics.Blit(source, destination, this.compositeMaterial);
        this.TextureReady = true;
    }
}
```

### <a name="track-or-identify-tagged-stationary-or-moving-real-world-objectsfaces-using-leds-or-other-recognizer-libraries"></a>Suivre ou identifier balisés stationnaire ou déplacement réel objets/des visages à l’aide des voyants ou autres bibliothèques de module de reconnaissance

Exemples :
* Les robots industriels avec voyants (ou les codes QR pour un déplacement plus lent des objets)
* Identifier et reconnaître les objets dans la salle
* Identifier et reconnaître les personnes dans la salle (par exemple, place HOLOGRAPHIQUE cartes de contact sur les visages)

## <a name="see-also"></a>Voir aussi
* [Caméra localisable dans DirectX](locatable-camera-in-directx.md)
* [Caméra localisable dans Unity](locatable-camera-in-unity.md)
* [Capture de réalité mixte](mixed-reality-capture.md)
* [Mixte de capture de la réalité pour les développeurs](mixed-reality-capture-for-developers.md)
* [Présentation de capture de média](https://msdn.microsoft.com/library/windows/apps/mt243896.aspx)
