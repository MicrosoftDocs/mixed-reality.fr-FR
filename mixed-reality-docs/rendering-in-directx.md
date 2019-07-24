---
title: Rendu dans DirectX
description: Décrit le rendu holographique pour Windows Mixed Reality.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, rendu, 3D Graphics, HolographicFrame, boucle de rendu, boucle de mise à jour, procédure pas à pas, exemple de code
ms.openlocfilehash: 6edcaf808f2d7d48f480169e5579adb8984678a0
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629037"
---
# <a name="rendering-in-directx"></a>Rendu dans DirectX

Windows Mixed Reality est basé sur DirectX pour produire des expériences graphiques riches et 3D pour les utilisateurs. L’abstraction de rendu se trouve juste au-dessus de DirectX et permet à une application de déterminer la position et l’orientation d’un ou plusieurs observateurs d’une scène holographique, comme prédit par le système. Le développeur peut ensuite localiser ses hologrammes par rapport à chaque caméra, ce qui permet à l’application de rendre ces hologrammes dans différents systèmes de coordonnées spatiales à mesure que l’utilisateur se déplace.

## <a name="update-for-the-current-frame"></a>Mettre à jour pour le frame actuel

Pour mettre à jour l’état de l’application pour les hologrammes, une fois par Frame, l’application effectue les opérations suivantes:
* Obtenir un <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> à partir du système de gestion de l’affichage.
* Mettez à jour la scène avec la prédiction actuelle de l’emplacement de la vue de la caméra lorsque le rendu est terminé. Notez qu’il peut y avoir plusieurs caméras pour la scène holographique.

Pour afficher les vues d’appareil photo holographique, une fois par Frame, l’application:
* Pour chaque caméra, affichez la scène du frame actuel, à l’aide de la vue caméra et des matrices de projection du système.

### <a name="create-a-new-holographic-frame-and-get-its-prediction"></a>Créer un nouveau Frame holographique et obtenir sa prédiction

Le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> contient des informations dont l’application a besoin pour mettre à jour et restituer le frame actuel. L’application commence chaque nouveau frame en appelant la méthode **CreateNextFrame** . Lorsque cette méthode est appelée, les prédictions sont effectuées à l’aide des dernières données de capteur disponibles et encapsulées dans l’objet **CurrentPrediction** .

Un nouvel objet Frame doit être utilisé pour chaque frame rendu, car il n’est valide que pour un instant donné. La propriété **CurrentPrediction** contient des informations telles que la position de la caméra. Les informations sont extrapolées au moment précis où le cadre est supposé être visible par l’utilisateur.

Le code suivant est extrait de **AppMain:: Update**:

```cpp
// The HolographicFrame has information that the app needs in order
// to update and render the current frame. The app begins each new
// frame by calling CreateNextFrame.
HolographicFrame holographicFrame = m_holographicSpace.CreateNextFrame();

// Get a prediction of where holographic cameras will be when this frame
// is presented.
HolographicFramePrediction prediction = holographicFrame.CurrentPrediction();
```

### <a name="process-camera-updates"></a>Traiter les mises à jour de l’appareil photo

Les mémoires tampons d’arrière-plan peuvent passer d’une image à l’autres. Votre application doit valider la mémoire tampon d’arrière-plan pour chaque caméra, puis libérer et recréer des vues de ressources et des tampons de profondeur en fonction des besoins. Notez que l’ensemble des poses dans la prédiction est la liste faisant autorité des caméras utilisées dans le frame actuel. En règle générale, vous utilisez cette liste pour effectuer une itération sur l’ensemble d’appareils photo.

À partir de **AppMain:: Update**:

```cpp
m_deviceResources->EnsureCameraResources(holographicFrame, prediction);
```

À partir de **DeviceResources:: EnsureCameraResources**:

```cpp
for (HolographicCameraPose const& cameraPose : prediction.CameraPoses())
{
    HolographicCameraRenderingParameters renderingParameters = frame.GetRenderingParameters(cameraPose);
    CameraResources* pCameraResources = cameraResourceMap[cameraPose.HolographicCamera().Id()].get();
    pCameraResources->CreateResourcesForBackBuffer(this, renderingParameters);
}
```

### <a name="get-the-coordinate-system-to-use-as-a-basis-for-rendering"></a>Obtenir le système de coordonnées à utiliser comme base pour le rendu

Windows Mixed Reality permet à votre application de créer différents [systèmes de coordonnées](coordinate-systems-in-directx.md) en fonction des besoins, comme le cadre de référence attaché et le cadre de référence fixe, qui suivent les emplacements dans le monde physique. Votre application peut ensuite utiliser ces systèmes de coordonnées pour savoir où afficher les hologrammes de chaque image. Lors de la demande de coordonnées à partir d’une API, vous transmettez toujours le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a> dans lequel vous souhaitez que ces coordonnées soient exprimées.

À partir de **AppMain:: Update**:

```cpp
pose = SpatialPointerPose::TryGetAtTimestamp(
    m_stationaryReferenceFrame.CoordinateSystem(), prediction.Timestamp());
```

Ces systèmes de coordonnées peuvent ensuite être utilisés pour générer des matrices de vue stéréo lors du rendu du contenu de votre scène.

À partir de **CameraResources:: UpdateViewProjectionBuffer**:

```cpp
// Get a container object with the view and projection matrices for the given
// pose in the given coordinate system.
auto viewTransformContainer = cameraPose.TryGetViewTransform(coordinateSystem);
```

### <a name="process-gaze-and-gesture-input"></a>Traiter le point de regard et l’entrée de mouvement

Les entrées [de](hands-and-motion-controllers-in-directx.md) [regard](gaze-in-directx.md) et de pointage ne sont pas basées sur le temps et ne doivent donc pas être mises à jour dans la fonction **StepTimer** . Toutefois, cette entrée est une information dont l’application a besoin pour examiner chaque frame.

### <a name="process-time-based-updates"></a>Mettre à jour le processus basé sur le temps

Toute application de rendu en temps réel a besoin d’un moyen de traiter des mises à jour basées sur le temps. Nous fournissons un moyen de le faire dans le modèle d’application holographique Windows via une implémentation de **StepTimer** . Cela est similaire au StepTimer fourni dans le modèle d’application UWP DirectX 11, donc si vous avez déjà regardé ce modèle, vous devez être familiarisé. Cet exemple de classe d’assistance StepTimer est en mesure de fournir des mises à jour de temps fixes, ainsi que des mises à jour de temps variables, et le mode par défaut est une étape variable.

Dans le cas d’un rendu holographique, nous avons spécifiquement choisi de ne pas trop placer dans la fonction du minuteur. Cela est dû au fait que vous pouvez le configurer pour qu’il soit une étape fixe, auquel cas il peut être appelé plusieurs fois par trame, ou pas du tout, pour certains frames, et nos mises à jour de données holographiques doivent se produire une fois par frame.


À partir de **AppMain:: Update**:

```cpp
m_timer.Tick([this]()
{
    m_spinningCubeRenderer->Update(m_timer);
});
```

### <a name="position-and-rotate-holograms-in-your-coordinate-system"></a>Positionner et faire pivoter des hologrammes dans votre système de coordonnées

Si vous utilisez un système de coordonnées unique, étant donné que le modèle utilise le **SpatialStationaryReferenceFrame**, ce processus n’est pas différent de celui utilisé dans les graphiques 3D. Ici, nous allons faire pivoter le cube et définir la matrice du modèle par rapport à la position dans le système de coordonnées stationnaire.

À partir de **SpinningCubeRenderer:: Update**:

```cpp
// Rotate the cube.
// Convert degrees to radians, then convert seconds to rotation angle.
const float    radiansPerSecond = XMConvertToRadians(m_degreesPerSecond);
const double   totalRotation = timer.GetTotalSeconds() * radiansPerSecond;
const float    radians = static_cast<float>(fmod(totalRotation, XM_2PI));
const XMMATRIX modelRotation = XMMatrixRotationY(-radians);

// Position the cube.
const XMMATRIX modelTranslation = XMMatrixTranslationFromVector(XMLoadFloat3(&m_position));

// Multiply to get the transform matrix.
// Note that this transform does not enforce a particular coordinate system. The calling
// class is responsible for rendering this content in a consistent manner.
const XMMATRIX modelTransform = XMMatrixMultiply(modelRotation, modelTranslation);

// The view and projection matrices are provided by the system; they are associated
// with holographic cameras, and updated on a per-camera basis.
// Here, we provide the model transform for the sample hologram. The model transform
// matrix is transposed to prepare it for the shader.
XMStoreFloat4x4(&m_modelConstantBufferData.model, XMMatrixTranspose(modelTransform));
```

**Remarque sur les scénarios avancés:** Le cube en rotation est un exemple très simple qui montre comment positionner un hologramme dans une seule image de référence. Il est également possible d' [utiliser simultanément plusieurs SpatialCoordinateSystems](coordinate-systems-in-directx.md) dans le même frame rendu.

### <a name="update-constant-buffer-data"></a>Mettre à jour les données de mémoire tampon constante

Les transformations de modèle pour le contenu sont mises à jour comme d’habitude. À ce stade, vous aurez des transformations valides calculées pour le système de coordonnées dans lequel vous allez effectuer le rendu.

À partir de **SpinningCubeRenderer:: Update**:

```cpp
// Update the model transform buffer for the hologram.
context->UpdateSubresource(
    m_modelConstantBuffer.Get(),
    0,
    nullptr,
    &m_modelConstantBufferData,
    0,
    0
);
```

Qu’en est-il des transformations de vue et de projection? Pour des résultats optimaux, nous voulons attendre que nous ayons terminés pour nos appels de dessin avant de les obtenir.

## <a name="render-the-current-frame"></a>Restituer le frame actuel

Le rendu sur Windows Mixed Reality n’est pas très différent du rendu sur un affichage mono 2D, mais il existe quelques différences que vous devez connaître:
* Les prédictions de frame holographique sont importantes. Plus la prédiction est proche de la présentation de votre cadre, plus vos hologrammes seront performants.
* Windows Mixed realisation contrôle les vues de la caméra. Vous devez effectuer un rendu sur chacun d’eux, car le frame holographique les présentera ultérieurement.
* Il est recommandé d’effectuer le rendu stéréo à l’aide d’un dessin instancié sur un tableau cible de rendu. Le modèle d’application holographique utilise l’approche recommandée de dessin instancié dans un tableau cible de rendu, qui utilise une vue de la cible du rendu sur un **Texture2DArray**.
* Si vous souhaitez effectuer un rendu sans utiliser l’instanciation stéréo, vous devez créer deux RenderTargetViews non-tableau (un pour chaque œil) qui référencent chacun l’un des deux secteurs du **Texture2DArray** fourni à l’application à partir du système. Cela n’est pas recommandé, car il est généralement beaucoup plus lent que d’utiliser l’instanciation.

### <a name="get-an-updated-holographicframe-prediction"></a>Recevoir une prédiction HolographicFrame mise à jour

La mise à jour de la prédiction de frame améliore l’efficacité de la stabilisation d’image et permet un positionnement plus précis des hologrammes en raison du temps plus réduit entre la prédiction et le moment où le cadre est visible par l’utilisateur. Dans l’idéal, mettez à jour votre prédiction de frame juste avant le rendu.

```cpp
holographicFrame.UpdateCurrentPrediction();
HolographicFramePrediction prediction = holographicFrame.CurrentPrediction();
```

### <a name="render-to-each-camera"></a>Rendre sur chaque caméra

Effectue une boucle sur l’ensemble de la caméra dans la prédiction et effectue un rendu sur chaque caméra de cet ensemble.

**Configurer votre passe de rendu**

Windows Mixed Reality utilise le rendu stéréoscopique pour améliorer l’illusion de la profondeur et pour afficher stereoscopically, de sorte que les affichages gauche et droit sont actifs. Avec le rendu stéréoscopique, il existe un décalage entre les deux affichages, que le cerveau peut rapprocher comme profondeur réelle. Cette section traite du rendu stéréoscopique à l’aide de l’instanciation, à l’aide du code du modèle d’application holographique Windows.

Chaque caméra possède sa propre cible de rendu (mémoire tampon d’arrière-plan), ainsi que les matrices de vue et de projection, dans l’espace holographique. Votre application doit créer d’autres ressources basées sur la caméra, telles que le tampon de profondeur, en fonction de la caméra. Dans le modèle d’application holographique Windows, nous fournissons une classe d’assistance pour regrouper ces ressources dans DX:: CameraResources. Commencez par configurer les vues de la cible de rendu:

À partir de **AppMain:: Render**:

```cpp
// This represents the device-based resources for a HolographicCamera.
DX::CameraResources* pCameraResources = cameraResourceMap[cameraPose.HolographicCamera().Id()].get();

// Get the device context.
const auto context = m_deviceResources->GetD3DDeviceContext();
const auto depthStencilView = pCameraResources->GetDepthStencilView();

// Set render targets to the current holographic camera.
ID3D11RenderTargetView *const targets[1] =
    { pCameraResources->GetBackBufferRenderTargetView() };
context->OMSetRenderTargets(1, targets, depthStencilView);

// Clear the back buffer and depth stencil view.
if (m_canGetHolographicDisplayForCamera &&
    cameraPose.HolographicCamera().Display().IsOpaque())
{
    context->ClearRenderTargetView(targets[0], DirectX::Colors::CornflowerBlue);
}
else
{
    context->ClearRenderTargetView(targets[0], DirectX::Colors::Transparent);
}
context->ClearDepthStencilView(
    depthStencilView, D3D11_CLEAR_DEPTH | D3D11_CLEAR_STENCIL, 1.0f, 0);
```

**Utiliser la prédiction pour obtenir les matrices de vue et de projection pour l’appareil photo**

Les matrices de vue et de projection pour chaque caméra holographique changent avec chaque trame. Actualisez les données dans la mémoire tampon constante pour chaque caméra holographique. Procédez ainsi après avoir mis à jour la prédiction et avant d’effectuer des appels de dessin pour cette caméra.

À partir de **AppMain:: Render**:

```cpp
// The view and projection matrices for each holographic camera will change
// every frame. This function refreshes the data in the constant buffer for
// the holographic camera indicated by cameraPose.
if (m_stationaryReferenceFrame)
{
    pCameraResources->UpdateViewProjectionBuffer(
        m_deviceResources, cameraPose, m_stationaryReferenceFrame.CoordinateSystem());
}

// Attach the view/projection constant buffer for this camera to the graphics pipeline.
bool cameraActive = pCameraResources->AttachViewProjectionBuffer(m_deviceResources);
```

Ici, nous montrons comment les matrices sont acquises à partir de la pose de l’appareil photo. Au cours de ce processus, nous obtenons également la fenêtre d’affichage actuelle de l’appareil photo. Notez la manière dont nous fournissons un système de coordonnées: il s’agit du même système de coordonnées que celui utilisé pour comprendre le point de vue, et c’est celui que nous avons utilisé pour positionner le cube en rotation.


À partir de **CameraResources:: UpdateViewProjectionBuffer**:

```cpp
// The system changes the viewport on a per-frame basis for system optimizations.
auto viewport = cameraPose.Viewport();
m_d3dViewport = CD3D11_VIEWPORT(
    viewport.X,
    viewport.Y,
    viewport.Width,
    viewport.Height
);

// The projection transform for each frame is provided by the HolographicCameraPose.
HolographicStereoTransform cameraProjectionTransform = cameraPose.ProjectionTransform();

// Get a container object with the view and projection matrices for the given
// pose in the given coordinate system.
auto viewTransformContainer = cameraPose.TryGetViewTransform(coordinateSystem);

// If TryGetViewTransform returns a null pointer, that means the pose and coordinate
// system cannot be understood relative to one another; content cannot be rendered
// in this coordinate system for the duration of the current frame.
// This usually means that positional tracking is not active for the current frame, in
// which case it is possible to use a SpatialLocatorAttachedFrameOfReference to render
// content that is not world-locked instead.
DX::ViewProjectionConstantBuffer viewProjectionConstantBufferData;
bool viewTransformAcquired = viewTransformContainer != nullptr;
if (viewTransformAcquired)
{
    // Otherwise, the set of view transforms can be retrieved.
    HolographicStereoTransform viewCoordinateSystemTransform = viewTransformContainer.Value();

    // Update the view matrices. Holographic cameras (such as Microsoft HoloLens) are
    // constantly moving relative to the world. The view matrices need to be updated
    // every frame.
    XMStoreFloat4x4(
        &viewProjectionConstantBufferData.viewProjection[0],
        XMMatrixTranspose(XMLoadFloat4x4(&viewCoordinateSystemTransform.Left) *
            XMLoadFloat4x4(&cameraProjectionTransform.Left))
    );
    XMStoreFloat4x4(
        &viewProjectionConstantBufferData.viewProjection[1],
        XMMatrixTranspose(XMLoadFloat4x4(&viewCoordinateSystemTransform.Right) *
            XMLoadFloat4x4(&cameraProjectionTransform.Right))
    );
}
```

La fenêtre d’affichage doit être définie pour chaque image. Votre nuanceur vertex (au moins) doit généralement accéder aux données de la vue ou de la projection.


À partir de **CameraResources:: AttachViewProjectionBuffer**:

```cpp
// Set the viewport for this camera.
context->RSSetViewports(1, &m_d3dViewport);

// Send the constant buffer to the vertex shader.
context->VSSetConstantBuffers(
    1,
    1,
    m_viewProjectionConstantBuffer.GetAddressOf()
);
```

**Rendre à la mémoire tampon d’arrière-plan de l’appareil photo et valider la mémoire tampon de profondeur**:

Il est judicieux de vérifier que **TryGetViewTransform** a réussi avant d’essayer d’utiliser les données de la vue ou de la projection, car si le système de coordonnées n’est pas localisable (par exemple, si le suivi a été interrompu), votre application ne peut pas s’afficher avec elle pour ce frame. Le modèle appelle uniquement **Render** sur le cube tournant si la classe **CameraResources** indique une mise à jour réussie.

Pour conserver les hologrammes là où un développeur ou un utilisateur les place dans le monde, Windows Mixed Reality intègre des fonctionnalités de [stabilisation d’image](hologram-stability.md). La stabilisation d’image permet de masquer la latence inhérente à un pipeline de rendu pour garantir la meilleure expérience holographique pour les utilisateurs. un point de concentration peut être spécifié pour améliorer encore davantage la stabilisation de l’image, ou une mémoire tampon de profondeur peut être fournie pour calculer la stabilisation des images optimisées en temps réel.

Pour de meilleurs résultats, votre application doit fournir un tampon de profondeur à l’aide de l’API <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer" target="_blank">CommitDirect3D11DepthBuffer</a> . La réalité mixte Windows peut ensuite utiliser les informations géométriques de la mémoire tampon de profondeur pour optimiser la stabilisation de l’image en temps réel. Le modèle d’application holographique Windows valide la mémoire tampon de profondeur de l’application par défaut, ce qui contribue à optimiser la stabilité des hologrammes.

À partir de **AppMain:: Render**:

```cpp
// Only render world-locked content when positional tracking is active.
if (cameraActive)
{
    // Draw the sample hologram.
    m_spinningCubeRenderer->Render();
    if (m_canCommitDirect3D11DepthBuffer)
    {
        // On versions of the platform that support the CommitDirect3D11DepthBuffer API, we can 
        // provide the depth buffer to the system, and it will use depth information to stabilize 
        // the image at a per-pixel level.
        HolographicCameraRenderingParameters renderingParameters =
            holographicFrame.GetRenderingParameters(cameraPose);
        
        IDirect3DSurface interopSurface =
            DX::CreateDepthTextureInteropObject(pCameraResources->GetDepthStencilTexture2D());

        // Calling CommitDirect3D11DepthBuffer causes the system to queue Direct3D commands to 
        // read the depth buffer. It will then use that information to stabilize the image as
        // the HolographicFrame is presented.
        renderingParameters.CommitDirect3D11DepthBuffer(interopSurface);
    }
}
```

>[!NOTE]
>Windows traitera votre texture de profondeur sur le GPU. il doit donc être possible d’utiliser votre mémoire tampon de profondeur comme ressource de nuanceur. Le ID3D11Texture2D que vous créez doit être dans un format non typé et doit être lié en tant que vue de ressource de nuanceur. Voici un exemple de création d’une texture de profondeur qui peut être validée pour la stabilisation d’image.

Code pour la **création de ressources de mémoire tampon de profondeur pour CommitDirect3D11DepthBuffer**:

```cpp
// Create a depth stencil view for use with 3D rendering if needed.
CD3D11_TEXTURE2D_DESC depthStencilDesc(
    DXGI_FORMAT_R16_TYPELESS,
    static_cast<UINT>(m_d3dRenderTargetSize.Width),
    static_cast<UINT>(m_d3dRenderTargetSize.Height),
    m_isStereo ? 2 : 1, // Create two textures when rendering in stereo.
    1, // Use a single mipmap level.
    D3D11_BIND_DEPTH_STENCIL | D3D11_BIND_SHADER_RESOURCE
);

winrt::check_hresult(
    device->CreateTexture2D(
        &depthStencilDesc,
        nullptr,
        &m_d3dDepthStencil
    ));

CD3D11_DEPTH_STENCIL_VIEW_DESC depthStencilViewDesc(
    m_isStereo ? D3D11_DSV_DIMENSION_TEXTURE2DARRAY : D3D11_DSV_DIMENSION_TEXTURE2D,
    DXGI_FORMAT_D16_UNORM
);
winrt::check_hresult(
    device->CreateDepthStencilView(
        m_d3dDepthStencil.Get(),
        &depthStencilViewDesc,
        &m_d3dDepthStencilView
    ));
```

**Dessiner du contenu holographique**

Le modèle d’application holographique Windows restitue le contenu en stéréo à l’aide de la technique recommandée de dessin de la géométrie d’instance vers un Texture2DArray de taille 2. Examinons la partie instanciation de ce et son fonctionnement sur Windows Mixed Reality.

À partir de **SpinningCubeRenderer:: Render**:

```cpp
// Draw the objects.
context->DrawIndexedInstanced(
    m_indexCount,   // Index count per instance.
    2,              // Instance count.
    0,              // Start index location.
    0,              // Base vertex location.
    0               // Start instance location.
);
```

Chaque instance accède à une matrice de projection/vue différente de la mémoire tampon constante. Voici la structure de mémoire tampon constante, qui n’est qu’un tableau de 2 matrices.

À partir de **VertexShaderShared. HLSL**, inclus par **VPRTVertexShader. HLSL**:

```HLSL
// A constant buffer that stores each set of view and projection matrices in column-major format.
cbuffer ViewProjectionConstantBuffer : register(b1)
{
    float4x4 viewProjection[2];
};
```

L’index du tableau cible du rendu doit être défini pour chaque pixel. Dans l’extrait de code suivant, output. viewId est mappé à la sémantique **SV_RenderTargetArrayIndex** . Notez que cela nécessite la prise en charge d’une fonctionnalité Direct3D 11,3 facultative, qui permet de définir la sémantique d’index du tableau cible de rendu à partir d’une étape de nuanceur.

À partir de **VPRTVertexShader. HLSL**:

```HLSL    
// Per-vertex data passed to the geometry shader.
struct VertexShaderOutput
{
    min16float4 pos     : SV_POSITION;
    min16float3 color   : COLOR0;

    // The render target array index is set here in the vertex shader.
    uint        viewId  : SV_RenderTargetArrayIndex;
};
```

À partir de **VertexShaderShared. HLSL**, inclus par **VPRTVertexShader. HLSL**:

```HLSL
// Per-vertex data used as input to the vertex shader.
struct VertexShaderInput
{
    min16float3 pos     : POSITION;
    min16float3 color   : COLOR0;
    uint        instId  : SV_InstanceID;
};

// Simple shader to do vertex processing on the GPU.
VertexShaderOutput main(VertexShaderInput input)
{
    VertexShaderOutput output;
    float4 pos = float4(input.pos, 1.0f);

    // Note which view this vertex has been sent to. Used for matrix lookup.
    // Taking the modulo of the instance ID allows geometry instancing to be used
    // along with stereo instanced drawing; in that case, two copies of each 
    // instance would be drawn, one for left and one for right.
    int idx = input.instId % 2;

    // Transform the vertex position into world space.
    pos = mul(pos, model);

    // Correct for perspective and project the vertex position onto the screen.
    pos = mul(pos, viewProjection[idx]);
    output.pos = (min16float4)pos;

    // Pass the color through without modification.
    output.color = input.color;

    // Set the render target array index.
    output.viewId = idx;

    return output;
}
```

Si vous souhaitez utiliser vos techniques de dessin d’instances existantes avec cette méthode de dessin vers un tableau de cibles de rendu stéréo, il vous suffit de dessiner deux fois le nombre d’instances que vous avez normalement. Dans le nuanceur, divisez **Input. instId** par 2 pour obtenir l’ID d’instance d’origine, qui peut être indexé dans (par exemple) une mémoire tampon de données par objet:`int actualIdx = input.instId / 2;`

### <a name="important-note-about-rendering-stereo-content-on-hololens"></a>Remarque importante à propos du rendu du contenu stéréo sur HoloLens

Windows Mixed Reality prend en charge la possibilité de définir l’index du tableau cible de rendu à partir de n’importe quelle étape du nuanceur; normalement, il s’agit d’une tâche qui peut uniquement être effectuée dans l’étape de nuanceur Geometry en raison de la façon dont la sémantique est définie pour Direct3D 11. Ici, nous présentons un exemple complet montrant comment configurer un pipeline de rendu uniquement avec les étapes du nuanceur de vertex et de pixels définies. Le code du nuanceur est décrit ci-dessus.

À partir de **SpinningCubeRenderer:: Render**:

```cpp
const auto context = m_deviceResources->GetD3DDeviceContext();

// Each vertex is one instance of the VertexPositionColor struct.
const UINT stride = sizeof(VertexPositionColor);
const UINT offset = 0;
context->IASetVertexBuffers(
    0,
    1,
    m_vertexBuffer.GetAddressOf(),
    &stride,
    &offset
);
context->IASetIndexBuffer(
    m_indexBuffer.Get(),
    DXGI_FORMAT_R16_UINT, // Each index is one 16-bit unsigned integer (short).
    0
);
context->IASetPrimitiveTopology(D3D11_PRIMITIVE_TOPOLOGY_TRIANGLELIST);
context->IASetInputLayout(m_inputLayout.Get());

// Attach the vertex shader.
context->VSSetShader(
    m_vertexShader.Get(),
    nullptr,
    0
);
// Apply the model constant buffer to the vertex shader.
context->VSSetConstantBuffers(
    0,
    1,
    m_modelConstantBuffer.GetAddressOf()
);

// Attach the pixel shader.
context->PSSetShader(
    m_pixelShader.Get(),
    nullptr,
    0
);

// Draw the objects.
context->DrawIndexedInstanced(
    m_indexCount,   // Index count per instance.
    2,              // Instance count.
    0,              // Start index location.
    0,              // Base vertex location.
    0               // Start instance location.
);
```

### <a name="important-note-about-rendering-on-non-hololens-devices"></a>Remarque importante à propos du rendu sur des appareils non-HoloLens

La définition de l’index du tableau cible du rendu dans le nuanceur vertex nécessite que le pilote Graphics prenne en charge une fonctionnalité Direct3D 11,3 facultative, que HoloLens prend en charge. Votre application peut être en mesure d’implémenter simplement cette technique pour le rendu, et toutes les spécifications seront respectées pour s’exécuter sur Microsoft HoloLens.

Il se peut que vous souhaitiez utiliser également l’émulateur HoloLens, qui peut être un puissant outil de développement pour votre application holographique et prendre en charge les appareils de casque immersif Windows Mixed Real qui sont attachés à des PC Windows 10. La prise en charge du chemin de rendu non-HoloLens, et donc, pour l’ensemble de la réalité mixte Windows, est également intégrée dans le modèle d’application holographique Windows. Dans le code du modèle, vous trouverez du code pour permettre à votre application holographique de s’exécuter sur le GPU sur votre PC de développement. Voici comment la classe **DeviceResources** vérifie cette prise en charge facultative des fonctionnalités.

À partir de **DeviceResources:: CreateDeviceResources**:

```cpp
// Check for device support for the optional feature that allows setting the render target array index from the vertex shader stage.
D3D11_FEATURE_DATA_D3D11_OPTIONS3 options;
m_d3dDevice->CheckFeatureSupport(D3D11_FEATURE_D3D11_OPTIONS3, &options, sizeof(options));
if (options.VPAndRTArrayIndexFromAnyShaderFeedingRasterizer)
{
    m_supportsVprt = true;
}
```

Pour prendre en charge le rendu sans cette fonctionnalité facultative, votre application doit utiliser un nuanceur Geometry pour définir l’index du tableau cible du rendu. Cet extrait de code est ajouté *après* **VSSetConstantBuffers**et *avant* **PSSetShader** dans l’exemple de code présenté dans la section précédente qui explique comment afficher la stéréo sur HoloLens.

À partir de **SpinningCubeRenderer:: Render**:

```cpp
if (!m_usingVprtShaders)
{
    // On devices that do not support the D3D11_FEATURE_D3D11_OPTIONS3::
    // VPAndRTArrayIndexFromAnyShaderFeedingRasterizer optional feature,
    // a pass-through geometry shader is used to set the render target 
    // array index.
    context->GSSetShader(
        m_geometryShader.Get(),
        nullptr,
        0
    );
}
```

**REMARQUE HLSL**: Dans ce cas, vous devez également charger un nuanceur de sommets légèrement modifié qui transmet l’index du tableau cible du rendu au nuanceur Geometry à l’aide d’une sémantique de nuanceur toujours autorisée, telle que TEXCOORD0. Le nuanceur Geometry n’a pas à effectuer de travail. le nuanceur Geometry de modèle transmet toutes les données, à l’exception de l’index de tableau cible de rendu qui est utilisé pour définir la sémantique SV_RenderTargetArrayIndex.

Code du modèle d’application pour **GeometryShader. HLSL**:

```HLSL
// Per-vertex data from the vertex shader.
struct GeometryShaderInput
{
    min16float4 pos     : SV_POSITION;
    min16float3 color   : COLOR0;
    uint        instId  : TEXCOORD0;
};

// Per-vertex data passed to the rasterizer.
struct GeometryShaderOutput
{
    min16float4 pos     : SV_POSITION;
    min16float3 color   : COLOR0;
    uint        rtvId   : SV_RenderTargetArrayIndex;
};

// This geometry shader is a pass-through that leaves the geometry unmodified 
// and sets the render target array index.
[maxvertexcount(3)]
void main(triangle GeometryShaderInput input[3], inout TriangleStream<GeometryShaderOutput> outStream)
{
    GeometryShaderOutput output;
    [unroll(3)]
    for (int i = 0; i < 3; ++i)
    {
        output.pos   = input[i].pos;
        output.color = input[i].color;
        output.rtvId = input[i].instId;
        outStream.Append(output);
    }
}
```

## <a name="present"></a>Présent

### <a name="enable-the-holographic-frame-to-present-the-swap-chain"></a>Activer le frame holographique pour présenter la chaîne de permutation

Avec Windows Mixed Reality, le système contrôle la chaîne de permutation. Le système gère ensuite la présentation des trames sur chaque caméra holographique pour garantir une expérience utilisateur de haute qualité. Il fournit également une fenêtre d’affichage qui met à jour chaque image, pour chaque caméra, afin d’optimiser les aspects du système, tels que la stabilisation d’image ou la capture de réalité mixte. Ainsi, une application holographique utilisant DirectX **n’appelle pas** la chaîne de permutation DXGI. Au lieu de cela, vous utilisez la classe <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> pour présenter toutes les chaînes d’échange d’un frame une fois que vous avez terminé de le dessiner.

À partir de **DeviceResources::P renvoyé**:

```
HolographicFramePresentResult presentResult = frame.PresentUsingCurrentPrediction();
```

Par défaut, cette API attend que le frame se termine avant de retourner. Les applications holographiques doivent attendre la fin de la trame précédente avant de commencer à travailler sur un nouveau Frame, car cela réduit la latence et permet d’obtenir de meilleurs résultats des prédictions de frame holographique. Il ne s’agit pas d’une règle difficile, et si vous avez des frames qui prennent plus d’une actualisation de l’écran pour le rendu, vous pouvez désactiver cette attente en passant le paramètre HolographicFramePresentWaitBehavior à <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.presentusingcurrentprediction" target="_blank">PresentUsingCurrentPrediction</a>. Dans ce cas, vous utiliserez probablement un thread de rendu asynchrone afin de conserver une charge continue sur le GPU. Notez que la fréquence d’actualisation de l’appareil HoloLens est 60 Hz, où une image a une durée d’environ 16 ms. Les appareils de casque immersif peuvent aller de 60 Hz à 90Hz; lors de l’actualisation de l’affichage à 90 Hz, chaque trame aura une durée d’environ 11 ms.

### <a name="handle-devicelost-scenarios-in-cooperation-with-the-holographicframe"></a>Gérer les scénarios DeviceLost en collaboration avec HolographicFrame

En général, les applications DirectX 11 veulent vérifier le HRESULT retourné par **la fonction dxgi** de la chaîne d’échange pour déterminer s’il y a eu une erreur **DeviceLost** . La classe <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> gère cela pour vous. Inspectez le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframepresentresult" target="_blank">HolographicFramePresentResult</a> qu’il retourne pour déterminer si vous devez libérer et recréer les ressources basées sur l’appareil et l’appareil Direct3D.

```cpp
// The PresentUsingCurrentPrediction API will detect when the graphics device
// changes or becomes invalid. When this happens, it is considered a Direct3D
// device lost scenario.
if (presentResult == HolographicFramePresentResult::DeviceRemoved)
{
    // The Direct3D device, context, and resources should be recreated.
    HandleDeviceLost();
}
```

Notez que si le périphérique Direct3D a été perdu et que vous l’avez recréé, vous devez indiquer à <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> de commencer à utiliser le nouvel appareil. La chaîne de permutation sera recréée pour cet appareil.

À partir de **DeviceResources:: InitializeUsingHolographicSpace**:

```
m_holographicSpace.SetDirect3D11Device(m_d3dInteropDevice);
```

Une fois votre Frame présenté, vous pouvez revenir à la boucle principale du programme et l’autoriser à passer à l’image suivante.

## <a name="hybrid-graphics-pcs-and-mixed-reality-applications"></a>PC graphiques hybrides et applications de réalité mixte

**Les** PC Windows 10 Creators Update peuvent être configurés avec des GPU discrets et intégrés. Avec ces types d’ordinateurs, Windows choisit la carte à laquelle le casque est connecté. Les applications doivent s’assurer que le périphérique DirectX qu’il crée utilise le même adaptateur.

La plupart des exemples de code Direct3D généraux illustrent la création d’un périphérique DirectX à l’aide de la carte matérielle par défaut, qui, sur un système hybride, peut être différent de celui utilisé pour le casque.

Pour contourner les problèmes que cela peut entraîner, utilisez <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicadapterid" target="_blank">HolographicAdapterId</a> à partir de <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>. PrimaryAdapterId () ou <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicdisplay" target="_blank">HolographicDisplay</a>. AdapterId (). Cette adapterId peut ensuite être utilisée pour sélectionner le bon DXGIAdapter à l’aide de IDXGIFactory4. EnumAdapterByLuid.

À partir de **DeviceResources:: InitializeUsingHolographicSpace**:

```cpp
// The holographic space might need to determine which adapter supports
// holograms, in which case it will specify a non-zero PrimaryAdapterId.
LUID id =
{
    m_holographicSpace.PrimaryAdapterId().LowPart,
    m_holographicSpace.PrimaryAdapterId().HighPart
};

// When a primary adapter ID is given to the app, the app should find
// the corresponding DXGI adapter and use it to create Direct3D devices
// and device contexts. Otherwise, there is no restriction on the DXGI
// adapter the app can use.
if ((id.HighPart != 0) || (id.LowPart != 0))
{
    UINT createFlags = 0;

    // Create the DXGI factory.
    ComPtr<IDXGIFactory1> dxgiFactory;
    winrt::check_hresult(
        CreateDXGIFactory2(
            createFlags,
            IID_PPV_ARGS(&dxgiFactory)
        ));
    ComPtr<IDXGIFactory4> dxgiFactory4;
    winrt::check_hresult(dxgiFactory.As(&dxgiFactory4));

    // Retrieve the adapter specified by the holographic space.
    winrt::check_hresult(
        dxgiFactory4->EnumAdapterByLuid(
            id,
            IID_PPV_ARGS(&m_dxgiAdapter)
        ));
}
else
{
    m_dxgiAdapter.Reset();
}
```

Code pour **mettre à jour DeviceResources:: CreateDeviceResources pour utiliser IDXGIAdapter**

```cpp
// Create the Direct3D 11 API device object and a corresponding context.
ComPtr<ID3D11Device> device;
ComPtr<ID3D11DeviceContext> context;

const D3D_DRIVER_TYPE driverType = m_dxgiAdapter == nullptr ? D3D_DRIVER_TYPE_HARDWARE : D3D_DRIVER_TYPE_UNKNOWN;
const HRESULT hr = D3D11CreateDevice(
    m_dxgiAdapter.Get(),        // Either nullptr, or the primary adapter determined by Windows Holographic.
    driverType,                 // Create a device using the hardware graphics driver.
    0,                          // Should be 0 unless the driver is D3D_DRIVER_TYPE_SOFTWARE.
    creationFlags,              // Set debug and Direct2D compatibility flags.
    featureLevels,              // List of feature levels this app can support.
    ARRAYSIZE(featureLevels),   // Size of the list above.
    D3D11_SDK_VERSION,          // Always set this to D3D11_SDK_VERSION for Windows Runtime apps.
    &device,                    // Returns the Direct3D device created.
    &m_d3dFeatureLevel,         // Returns feature level of device created.
    &context                    // Returns the device immediate context.
);
```

**Graphiques et Media Foundation hybrides**

L’utilisation de Media Foundation sur des systèmes hybrides peut entraîner des problèmes où la vidéo n’est pas rendue ou la texture vidéo est endommagée. Cela peut se produire en raison de la valeur par défaut du comportement du système Media Foundation comme indiqué ci-dessus. Dans certains scénarios, la création d’un ID3D11Device distinct est nécessaire pour prendre en charge le Multi-Threading et les indicateurs de création corrects sont définis.

Lors de l’initialisation de ID3D11Device, l’indicateur D3D11_CREATE_DEVICE_VIDEO_SUPPORT doit être défini dans le cadre du D3D11_CREATE_DEVICE_FLAG. Une fois l’appareil et le contexte créés, appelez <a href="https://docs.microsoft.com/windows/desktop/api/d3d10/nf-d3d10-id3d10multithread-setmultithreadprotected" target="_blank">SetMultithreadProtected</a> pour activer le multithreading. Pour associer l’appareil à <a href="https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfdxgidevicemanager" target="_blank">IMFDXGIDeviceManager</a>, utilisez la fonction <a href="https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-resetdevice" target="_blank">IMFDXGIDeviceManager:: ResetDevice</a> .

Code pour **associer un ID3D11Device à IMFDXGIDeviceManager**:

```cpp
// create dx device for media pipeline
winrt::com_ptr<ID3D11Device> spMediaDevice;

// See above. Also make sure to enable the following flags on the D3D11 device:
//   * D3D11_CREATE_DEVICE_VIDEO_SUPPORT
//   * D3D11_CREATE_DEVICE_BGRA_SUPPORT
if (FAILED(CreateMediaDevice(spAdapter.get(), &spMediaDevice)))
    return;                                                     

// Turn multithreading on 
winrt::com_ptr<ID3D10Multithread> spMultithread;
if (spContext.try_as(spMultithread))
{
    spMultithread->SetMultithreadProtected(TRUE);
}

// lock the shared dxgi device manager
// call MFUnlockDXGIDeviceManager when no longer needed
UINT uiResetToken;
winrt::com_ptr<IMFDXGIDeviceManager> spDeviceManager;
hr = MFLockDXGIDeviceManager(&uiResetToken, spDeviceManager.put());
if (FAILED(hr))
    return hr;
    
// associate the device with the manager
hr = spDeviceManager->ResetDevice(spMediaDevice.get(), uiResetToken);
if (FAILED(hr))
    return hr;
```

## <a name="see-also"></a>Voir aussi
* [Systèmes de coordonnées dans DirectX](coordinate-systems-in-directx.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
