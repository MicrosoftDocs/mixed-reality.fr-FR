---
title: Rendu dans DirectX
description: Explique le rendu pour la réalité mixte Windows HOLOGRAPHIQUE.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, de rendu, de graphiques 3D, HolographicFrame, restituer la boucle, la boucle de mise à jour, procédure pas à pas, exemple de code
ms.openlocfilehash: fd35f971af4c3c9dfd7f21ee396c92216b3246e9
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597149"
---
# <a name="rendering-in-directx"></a>Rendu dans DirectX

Windows Mixed Reality repose sur DirectX pour produire riche, 3D graphique des expériences aux utilisateurs. L’abstraction de rendu se trouve juste au-dessus de DirectX et permet une raison de l’application sur la position et l’orientation d’un ou plusieurs observateurs d’une scène HOLOGRAPHIQUE, comme prévu par le système. Le développeur peut ensuite localiser leurs hologrammes par rapport à chaque appareil photo, ce qui permet l’application de rendu ces hologrammes dans différents systèmes de coordonnées spatiales de l’utilisateur se déplace.

## <a name="update-for-the-current-frame"></a>Mise à jour pour le frame actuel

Pour mettre à jour l’état de l’application pour hologrammes, une fois par frame de l’application sera :
* Obtenir un <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> à partir du système de gestion complet.
* Mettre à jour de la scène avec la prédiction actuelle d’où sera la vue de l’appareil photo lors de la restitution effectuée. Notez qu’il peut y avoir plus d’un appareil photo pour la scène HOLOGRAPHIQUE.

Pour restituer des vues de caméra HOLOGRAPHIQUE, une fois par frame de l’application sera :
* Pour chaque appareil photo, afficher la scène pour le frame actuel, à l’aide de matrices de projection et d’affichage de caméra à partir du système.

### <a name="create-a-new-holographic-frame-and-get-its-prediction"></a>Créer un nouveau frame holographique et obtenir sa prédiction

Le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> a des informations de l’application a besoin pour mettre à jour et afficher le frame actuel. L’application commence à chaque nouvelle image en appelant le **CreateNextFrame** (méthode). Lorsque cette méthode est appelée, les prédictions sont établies en utilisant les dernières données de capteur disponibles et encapsulées dans **CurrentPrediction** objet.

Un nouvel objet de frame doit être utilisé pour chaque frame rendu comme il est uniquement valide pendant un instant précis. Le **CurrentPrediction** propriété contient des informations telles que la position de la caméra. Les informations sont extrapolées à un moment exact de temps lorsque le frame est censé être visibles par l’utilisateur.

Le code suivant est extrait de **AppMain::Update**:

```cpp
// The HolographicFrame has information that the app needs in order
// to update and render the current frame. The app begins each new
// frame by calling CreateNextFrame.
HolographicFrame holographicFrame = m_holographicSpace.CreateNextFrame();

// Get a prediction of where holographic cameras will be when this frame
// is presented.
HolographicFramePrediction prediction = holographicFrame.CurrentPrediction();
```

### <a name="process-camera-updates"></a>Mises à jour de la caméra de processus

Mémoires tampons d’arrière-plan peuvent changer à partir d’une image à l’autre. Votre application a besoin pour valider l’arrière de la mémoire tampon pour chaque appareil photo et mise en production et recréer les affichages de ressources et les tampons de profondeur en fonction des besoins. Notez que le jeu de risque de poser dans la prédiction est la liste faisant autorité des caméras utilisé dans le frame actuel. En règle générale, vous utilisez cette liste pour itérer au sein de l’ensemble des appareils photo.

À partir de **AppMain::Update**:

```cpp
m_deviceResources->EnsureCameraResources(holographicFrame, prediction);
```

À partir de **DeviceResources::EnsureCameraResources**:

```cpp
for (HolographicCameraPose const& cameraPose : prediction.CameraPoses())
{
    HolographicCameraRenderingParameters renderingParameters = frame.GetRenderingParameters(cameraPose);
    CameraResources* pCameraResources = cameraResourceMap[cameraPose.HolographicCamera().Id()].get();
    pCameraResources->CreateResourcesForBackBuffer(this, renderingParameters);
}
```

### <a name="get-the-coordinate-system-to-use-as-a-basis-for-rendering"></a>Obtenir le système de coordonnées à utiliser comme base pour le rendu

Réalité mixte Windows permet à votre application de créer divers [systèmes de coordonnées](coordinate-systems-in-directx.md) en fonction des besoins, telles que l’image de référence jointes et de l’image de référence stationnaire, qui assurent le suivi des emplacements dans le monde physique. Votre application peut ensuite utiliser ces systèmes de coordonnées à raisonner sur l’emplacement afficher hologrammes chaque frame. Lorsque vous demandez des coordonnées à partir d’une API, vous passerez toujours dans le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a> au sein de laquelle vous souhaitez que ces coordonnées exprimer.

À partir de **AppMain::Update**:

```cpp
pose = SpatialPointerPose::TryGetAtTimestamp(
    m_stationaryReferenceFrame.CoordinateSystem(), prediction.Timestamp());
```

Ces systèmes de coordonnées peut ensuite servir à générer des matrices de vue stéréo lors du rendu du contenu dans votre scène.

À partir de **CameraResources::UpdateViewProjectionBuffer**:

```cpp
// Get a container object with the view and projection matrices for the given
// pose in the given coordinate system.
auto viewTransformContainer = cameraPose.TryGetViewTransform(coordinateSystem);
```

### <a name="process-gaze-and-gesture-input"></a>Regards de processus et des mouvements d’entrée

[Utilisation](gaze.md) et [mouvement](gestures.md) d’entrée ne sont pas basés sur le temps et n’ayant donc pas à mettre à jour dans le **StepTimer** (fonction). Toutefois [cette entrée](gaze,-gestures,-and-motion-controllers-in-directx.md) est quelque chose que l’application a besoin d’examiner chaque frame.

### <a name="process-time-based-updates"></a>Processus temporelle des mises à jour

N’importe quelle application de rendu en temps réel sera besoin d’un moyen pour traiter les mises à jour heure ; Nous fournirons un moyen pour ce faire, dans le modèle d’application Windows HOLOGRAPHIQUE via un **StepTimer** implémentation. Cela revient au StepTimer fourni dans le modèle application DirectX 11 UWP, par conséquent, si vous avez déjà consulté ce modèle vous devez être en terrain familier. Cette classe d’assistance d’exemple StepTimer est en mesure de fournir des mises à jour de temps fixes, ainsi que les mises à jour de temps variable, et le mode par défaut est celle de temps variable.

Dans le cas de rendu HOLOGRAPHIQUE, nous avons spécifiquement choisi de ne pas placer trop dans la fonction de minuteur. Il s’agit, car vous pouvez configurer pour qu’il soit une étape de temps fixe, auquel cas peut obtenir appelée plusieurs fois par frame – ou pas du tout, pour certaines images – et nos mises à jour de données HOLOGRAPHIQUE doivent se produire qu’une seule fois par trame.


À partir de **AppMain::Update**:

```cpp
m_timer.Tick([this]()
{
    m_spinningCubeRenderer->Update(m_timer);
});
```

### <a name="position-and-rotate-holograms-in-your-coordinate-system"></a>Position et la rotation hologrammes dans votre système de coordonnées

Si vous évoluez dans un seul système de coordonnées, comme le fait le modèle avec le **SpatialStationaryReferenceFrame**, ce processus n’est pas différent de ce que vous êtes sinon utilisé dans les graphiques 3D. Ici, nous faire pivoter le cube et la valeur de la matrice de modèle par rapport à la position dans le système de coordonnées stationnaire.

À partir de **SpinningCubeRenderer::Update**:

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

**Remarque sur les scénarios avancés :** Le cube en rotation est un exemple très simple de comment positionner un hologramme au sein d’une image de référence. Il est également possible de [utiliser plusieurs SpatialCoordinateSystems](coordinate-systems-in-directx.md) dans le même frame rendu, en même temps.

### <a name="update-constant-buffer-data"></a>Mettre à jour les données de mémoire tampon constante

Transformations de modèle de contenu sont mis à jour comme d’habitude. À ce stade, vous serez calculée transformations valides pour le système de coordonnées que vous allez être rendu dans.

À partir de **SpinningCubeRenderer::Update**:

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

Qu’en est-il des transformations de projection et d’affichage ? Pour de meilleurs résultats, nous souhaitons patienter jusqu'à ce que nous avons presque terminé pour nos appels de dessin avant de passer ces.

## <a name="render-the-current-frame"></a>Afficher le frame actuel

Rendu sur Windows Mixed Reality n’est pas très différent de rendu sur un écran de mono 2D, mais il existe des différences, que vous devez être conscient :
* Prédictions de frame HOLOGRAPHIQUE sont importantes. Le plus près la prédiction consiste à lorsque votre image est présentée, plus votre hologrammes ressemblera.
* Réalité mixte Windows contrôle les vues de l’appareil photo. Vous devez effectuer le rendu à chacun d'entre eux étant donné que le frame HOLOGRAPHIQUE présentera les pour vous plus tard.
* Rendu stéréo est recommandé d’être accomplies à l’aide de dessin instancié dans un tableau de cible de rendu. Le modèle d’application HOLOGRAPHIQUE utilise l’approche recommandée du dessin instancié dans un tableau de cible de rendu, qui utilise une vue de cible de rendu sur un **Texture2DArray**.
* Si vous souhaitez restituer sans utiliser l’instanciation stéréo, vous devez créer deux non-tableau RenderTargetViews (une pour chaque œil) que chaque référence à un des deux tranches dans le **Texture2DArray** fourni à l’application à partir du système. Ceci n’est pas recommandé, car il est généralement beaucoup plus lent que l’utilisation de l’instanciation.

### <a name="get-an-updated-holographicframe-prediction"></a>Obtenir une prédiction HolographicFrame mis à jour

La prédiction de frame de la mise à jour améliore l’efficacité de stabilisation de l’image, tout en permettant un positionnement plus précis des hologrammes en raison du temps plus court entre la prédiction et lorsque le frame est visible par l’utilisateur. Dans l’idéal, mettez à jour votre prédiction trame juste avant le rendu.

```cpp
holographicFrame.UpdateCurrentPrediction();
HolographicFramePrediction prediction = holographicFrame.CurrentPrediction();
```

### <a name="render-to-each-camera"></a>Restituer à chaque appareil photo

Boucle sur l’ensemble de la pose d’appareil photo dans la prédiction et restituer à chaque appareil photo dans cet ensemble.

**Configurer votre passe de rendu**

Réalité mixte Windows utilisant des rendu stéréoscopique pour améliorer l’illusion de profondeur et à rendre grâce, gauche et l’affichage de droite sont actifs. Avec le rendu stéréoscopique existe un décalage entre les deux écrans, le cerveau peut également rapprocher comme profondeur réelle. Cet section couvre stéréoscopique rendu à l’aide de l’instanciation, à l’aide de code à partir du modèle d’application Windows HOLOGRAPHIQUE.

Chaque caméra a son propre rendu les matrices de projection et cible (mémoire tampon d’arrière-plan) et d’affichage, dans l’espace HOLOGRAPHIQUE. Votre application devra créer d’autres ressources basée sur l’appareil photo - telles que la mémoire tampon de profondeur - sur une base par caméra. Dans le modèle d’application Windows HOLOGRAPHIQUE, nous fournissons une classe d’assistance pour regrouper ces ressources dans DX::CameraResources. Commencez par configurer les affichages de cible de rendu :

À partir de **AppMain::Render**:

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

**Utiliser la prédiction pour obtenir les matrices de projection et d’affichage pour l’appareil photo**

Les matrices de projection et d’affichage pour chaque caméra HOLOGRAPHIQUE change avec chaque trame. Actualiser les données dans la mémoire tampon constante pour chaque caméra HOLOGRAPHIQUE. Faire une fois la mise à jour de la prédiction, et avant d’effectuer les appels de n’importe quel dessin pour cet appareil photo.

À partir de **AppMain::Render**:

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

Ici, nous montrons comment les matrices sont acquis à partir de la pose d’appareil photo. Pendant ce processus, nous obtenons également la fenêtre d’affichage actuel de l’appareil photo. Notez comment nous fournissons un système de coordonnées : il s’agit du même système de coordonnées nous permet de comprendre les regards, et il est identique à celui nous avons utilisé pour positionner le cube en rotation.


À partir de **CameraResources::UpdateViewProjectionBuffer**:

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

Chaque trame doit être défini à la fenêtre d’affichage. Votre nuanceur de sommets (au moins) généralement devront accéder aux données de projection de la vue.


À partir de **CameraResources::AttachViewProjectionBuffer**:

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

**Rendu à la mémoire tampon d’arrière-plan caméra et valider le tampon de profondeur**:

Il est judicieux de vérifier que **TryGetViewTransform** a réussi avant d’essayer d’utiliser les données de la projection de la vue, car si le système de coordonnées n’est pas localisable (par exemple, le suivi a été interrompu) votre application ne peut pas obtenir un rendu correspondant frame. Le modèle appelle uniquement **restituer** sur le cube en rotation si le **CameraResources** classe indique une mise à jour réussie.

Pour conserver hologrammes où un développeur ou un utilisateur les place dans le monde, réalité mixte Windows inclut des fonctionnalités pour [stabilisation de l’image](hologram-stability.md). Stabilisation de l’image permet de masquer la latence inhérente dans un pipeline de rendu pour garantir les meilleures expériences HOLOGRAPHIQUE pour les utilisateurs ; un point de focus peut être spécifié pour améliorer la stabilisation image encore plus loin, ou un mémoire tampon de profondeur peut être fourni à calcul optimisé stabilisation d’image en temps réel.

Pour de meilleurs résultats, votre application doit fournir une mémoire tampon de profondeur à l’aide de la <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer" target="_blank">CommitDirect3D11DepthBuffer</a> API. Réalité mixte Windows peut ensuite utiliser informations sur la géométrie à partir de la mémoire tampon de profondeur pour optimiser la stabilisation d’image en temps réel. Le modèle d’application Windows HOLOGRAPHIQUE valide la mémoire tampon de profondeur de l’application par défaut, aider à optimiser la stabilité hologramme.

À partir de **AppMain::Render**:

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
>Windows traite votre texture de profondeur sur le GPU, elle doit donc être possible d’utiliser votre mémoire tampon de profondeur comme une ressource de nuanceur. ID3D11Texture2D que vous créez doit être dans un format sans type, et il doit être lié comme une vue de ressource de nuanceur. Voici un exemple montrant comment créer une texture de profondeur qui peut être validée pour la stabilisation de l’image.

Code pour **création de ressources de mémoire tampon de profondeur pour CommitDirect3D11DepthBuffer**:

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

**Dessiner le contenu HOLOGRAPHIQUE**

Le modèle d’application Windows HOLOGRAPHIQUE restitue le contenu en stéréo à l’aide de la technique recommandée de dessin géométrique instanciée à un Texture2DArray de taille de 2. Examinons la partie instanciation de cela, et comment elle fonctionne sur Windows Mixed Reality.

À partir de **SpinningCubeRenderer::Render**:

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

Chaque instance accède à une matrice de projection et d’affichage différent à partir de la mémoire tampon constante. Voici la structure de mémoire tampon constante, ce qui est simplement un tableau de 2 matrices.

À partir de **VertexShaderShared.hlsl**, fourni par **VPRTVertexShader.hlsl**:

```HLSL
// A constant buffer that stores each set of view and projection matrices in column-major format.
cbuffer ViewProjectionConstantBuffer : register(b1)
{
    float4x4 viewProjection[2];
};
```

L’index de tableau de cible de rendu doit être définie pour chaque pixel. Dans l’extrait de code suivant, output.viewId est mappé à la **SV_RenderTargetArrayIndex** sémantique. Notez que cela nécessite de prise en charge pour une fonctionnalité de Direct3D 11.3 facultative, qui permet la sémantique soit définie à partir de n’importe quelle étape du nuanceur de l’index de tableau de cible de rendu.

À partir de **VPRTVertexShader.hlsl**:

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

À partir de **VertexShaderShared.hlsl**, fourni par **VPRTVertexShader.hlsl**:

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

Si vous souhaitez utiliser vos instances existantes des techniques de dessins avec cette méthode de dessin pour un stéréo restituer tableau cible, il vous suffit est dessiner deux fois le nombre d’instances que vous avez normalement. Dans le nuanceur, divisez **input.instId** par 2 pour obtenir l’ID d’instance d’origine, qui peuvent être indexé (par exemple) sur une mémoire tampon de données de par objet : `int actualIdx = input.instId / 2;`

### <a name="important-note-about-rendering-stereo-content-on-hololens"></a>Remarque importante sur le rendu de contenu stéréo sur HoloLens

Réalité mixte Windows prend en charge la possibilité de définir l’index de tableau de cible de rendu à partir de n’importe quelle étape du nuanceur ; en règle générale, il s’agit d’une tâche qui peut être effectuée uniquement dans l’étape du nuanceur de géométrie en raison de la façon dont la sémantique est définie pour Direct3D 11. Ici, nous présentons un exemple complet montrant comment configurer un pipeline de rendu avec simplement le sommets et pixels nuanceur étapes ensemble. Le code du nuanceur est comme décrit ci-dessus.

À partir de **SpinningCubeRenderer::Render**:

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

### <a name="important-note-about-rendering-on-non-hololens-devices"></a>Remarque importante sur le rendu sur les appareils non HoloLens

Définition de l’index de tableau de cible de rendu dans le nuanceur de sommets nécessite que le pilote graphique prend en charge une fonctionnalité de Direct3D 11.3 facultative, HoloLens ne prend pas en charge. Votre application peut être en mesure d’implémenter en toute sécurité simplement cette technique pour le rendu, et toutes les exigences seront respectées dans s’exécutant sur le Microsoft HoloLens.

Il peut arriver que vous souhaitez utiliser l’émulateur de HoloLens, ce qui peut être un outil de développement puissant pour votre application holographique - et prendre en charge les périphériques des casques IMMERSIFS Windows Mixed Reality qui sont attachés à un PC Windows 10. Prise en charge pour le chemin d’accès de rendu non HoloLens - et par conséquent, pour tous les Windows Mixed Reality - est également intégrée dans le modèle d’application Windows HOLOGRAPHIQUE. Dans le code du modèle, vous trouverez le code pour activer votre application HOLOGRAPHIQUE s’exécute sur le GPU dans votre PC de développement. Voici comment la **DeviceResources** vérifie cette prise en charge de la fonctionnalité facultative de la classe.

À partir de **DeviceResources::CreateDeviceResources**:

```cpp
// Check for device support for the optional feature that allows setting the render target array index from the vertex shader stage.
D3D11_FEATURE_DATA_D3D11_OPTIONS3 options;
m_d3dDevice->CheckFeatureSupport(D3D11_FEATURE_D3D11_OPTIONS3, &options, sizeof(options));
if (options.VPAndRTArrayIndexFromAnyShaderFeedingRasterizer)
{
    m_supportsVprt = true;
}
```

Pour prendre en charge du rendu sans cette fonctionnalité optionnelle, votre application doit utiliser un nuanceur de géométrie pour définir l’index de tableau de cible de rendu. Cet extrait de code serait ajouté *après* **VSSetConstantBuffers**, et *avant* **PSSetShader** dans l’exemple de code indiqué dans le précédent section qui explique comment effectuer le rendu stéréo sur HoloLens.

À partir de **SpinningCubeRenderer::Render**:

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

**REMARQUE DE HLSL**: Dans ce cas, vous devez également charger un nuanceur de sommets légèrement modifiée qui transmet l’index de tableau de cible de rendu pour le nuanceur de géométrie à l’aide d’un sémantique, telles que TEXCOORD0 de nuanceur toujours autorisé. Le nuanceur de géométrie ne devra pas effectuer le travail ; le nuanceur de géométrie modèle traverse toutes les données, à l’exception de l’index de tableau de cible de rendu, qui est utilisé pour définir le SV_RenderTargetArrayIndex sémantique.

Code de modèle d’application pour **GeometryShader.hlsl**:

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

### <a name="enable-the-holographic-frame-to-present-the-swap-chain"></a>Activer le frame HOLOGRAPHIQUE présenter la chaîne de permutation

Avec Windows Mixed Reality, le système de contrôle de la chaîne de permutation. Le système gère ensuite les images présentant à chaque caméra HOLOGRAPHIQUE pour garantir une expérience utilisateur de haute qualité. Il fournit également une mise à jour de la fenêtre d’affichage chaque trame, pour chaque appareil photo, pour optimiser les aspects du système tels que la stabilisation de l’image ou de capturer de réalité mixte. Par conséquent, une application HOLOGRAPHIQUE à l’aide de DirectX n’appelle pas **présent** sur un DXGI chaîne de permutation. Au lieu de cela, vous utilisez le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> classe pour présenter toutes les chaînes d’échange pour un frame, une fois que vous avez terminé dessiner.

À partir de **DeviceResources::Present**:

```
HolographicFramePresentResult presentResult = frame.PresentUsingCurrentPrediction();
```

Par défaut, cette API attend que le frame à terminer avant de retourner. Applications HOLOGRAPHIQUE doivent attendre l’image précédente soit terminée avant de commencer à travailler sur un nouveau frame, car cela réduit la latence, tout en permettant de meilleurs résultats à partir des prédictions de frame HOLOGRAPHIQUE. Ce n’est pas une règle de disque dur et si vous avez les trames qui durent plus longtemps que l’actualisation d’un seul écran pour vous rendre peuvent désactiver cette attente en transmettant le paramètre HolographicFramePresentWaitBehavior à <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.presentusingcurrentprediction" target="_blank">PresentUsingCurrentPrediction</a>. Dans ce cas, vous utiliseriez probablement un thread de rendu asynchrone afin de maintenir une charge continue sur le GPU. Notez que la fréquence de rafraîchissement de l’appareil HoloLens est 60hz, où une image a une durée égale à environ 16 ms. Périphériques des casques IMMERSIFS peuvent varier de 60hz à 90hz ; lors de l’actualisation de l’affichage à 90 hz, chaque image aura une durée égale à environ 11 ms.

### <a name="handle-devicelost-scenarios-in-cooperation-with-the-holographicframe"></a>Gestion de scénarios DeviceLost en coopération avec le HolographicFrame

Les applications DirectX 11 souhaiteriez vérifier le HRESULT retourné par la chaîne de permutation DXGI **présent** fonction pour déterminer s’il y avait un **DeviceLost** erreur. Le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> classe gère cela automatiquement. Inspecter le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframepresentresult" target="_blank">HolographicFramePresentResult</a> qu’il retourne pour savoir si vous devez libérer et recréer les appareil de Direct3D et les ressources basées sur l’appareil.

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

Notez que si le périphérique Direct3D a été perdu et que vous l’avez fait la recréer, vous devez indiquer le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> pour commencer à utiliser le nouvel appareil. La chaîne de permutation est recréée pour cet appareil.

À partir de **DeviceResources::InitializeUsingHolographicSpace**:

```
m_holographicSpace.SetDirect3D11Device(m_d3dInteropDevice);
```

Une fois que votre image est présentée, vous pouvez revenir à la boucle de programme principal et lui permettre de continuer à l’image suivante.

## <a name="hybrid-graphics-pcs-and-mixed-reality-applications"></a>PC de graphiques hybrides et les applications de réalité mixte

Windows 10 Creators Update PC peuvent être configurés avec **à la fois** GPU discrets et intégrées. Avec ces types d’ordinateurs, Windows choisira l’adaptateur à que le casque est connecté. Applications doivent s’assurer de l’appareil de DirectX qu'il crée utilise la même carte.

Exemple de code de Direct3D plus général illustre la création d’un périphérique DirectX à l’aide de l’adaptateur de matériel par défaut, qui ne peut pas être identique à celui utilisé pour le casque sur un système hybride.

Pour contourner les problèmes que cela peut entraîner, utilisez le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicadapterid" target="_blank">HolographicAdapterId</a> à partir de le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>. PrimaryAdapterId() ou <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicdisplay" target="_blank">HolographicDisplay</a>. AdapterId(). Cette adapterId peut ensuite servir à sélectionner le DXGIAdapter droit à l’aide de IDXGIFactory4.EnumAdapterByLuid.

À partir de **DeviceResources::InitializeUsingHolographicSpace**:

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

Le code vers **DeviceResources::CreateDeviceResources pour utiliser IDXGIAdapter de mettre à jour**

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

**Les graphiques hybrides et Media Foundation**

À l’aide de Media Foundation sur les systèmes hybrides peut entraîner des problèmes où vidéo n’affichera ou texture vidéo est endommagé. Cela peut se produire, car Media Foundation par défaut pour un comportement du système comme indiqué ci-dessus. Dans certains scénarios, la création d’un ID3D11Device distinct est requis pour la prise en charge multi-threading et la création correcte indicateurs sont définis.

Lors de l’initialisation du ID3D11Device, D3D11_CREATE_DEVICE_VIDEO_SUPPORT indicateur doit être défini dans le cadre de la D3D11_CREATE_DEVICE_FLAG. Une fois l’appareil et le contexte est créé, appelez <a href="https://docs.microsoft.com/windows/desktop/api/d3d10/nf-d3d10-id3d10multithread-setmultithreadprotected" target="_blank">SetMultithreadProtected</a> pour activer le multithreading. Pour associer l’appareil avec le <a href="https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfdxgidevicemanager" target="_blank">IMFDXGIDeviceManager</a>, utilisez le <a href="https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-resetdevice" target="_blank">IMFDXGIDeviceManager::ResetDevice</a> (fonction).

Le code vers **associer un ID3D11Device IMFDXGIDeviceManager**:

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
