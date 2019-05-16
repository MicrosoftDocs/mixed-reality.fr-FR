---
title: Rendu dans DirectX
description: Explique le rendu pour la réalité mixte Windows HOLOGRAPHIQUE.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, hologrammes, de rendu, de graphiques 3D, HolographicFrame, restituer la boucle, la boucle de mise à jour, procédure pas à pas, exemple de code
ms.openlocfilehash: 6edcaf808f2d7d48f480169e5579adb8984678a0
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629037"
---
# <a name="rendering-in-directx"></a><span data-ttu-id="b756e-104">Rendu dans DirectX</span><span class="sxs-lookup"><span data-stu-id="b756e-104">Rendering in DirectX</span></span>

<span data-ttu-id="b756e-105">Windows Mixed Reality repose sur DirectX pour produire riche, 3D graphique des expériences aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b756e-105">Windows Mixed Reality is built on DirectX to produce rich, 3D graphical experiences for users.</span></span> <span data-ttu-id="b756e-106">L’abstraction de rendu se trouve juste au-dessus de DirectX et permet une raison de l’application sur la position et l’orientation d’un ou plusieurs observateurs d’une scène HOLOGRAPHIQUE, comme prévu par le système.</span><span class="sxs-lookup"><span data-stu-id="b756e-106">The rendering abstraction sits just above DirectX and lets an app reason about the position and orientation of one or more observers of a holographic scene, as predicted by the system.</span></span> <span data-ttu-id="b756e-107">Le développeur peut ensuite localiser leurs hologrammes par rapport à chaque appareil photo, ce qui permet l’application de rendu ces hologrammes dans différents systèmes de coordonnées spatiales de l’utilisateur se déplace.</span><span class="sxs-lookup"><span data-stu-id="b756e-107">The developer can then locate their holograms relative to each camera, letting the app render these holograms in various spatial coordinate systems as the user moves around.</span></span>

## <a name="update-for-the-current-frame"></a><span data-ttu-id="b756e-108">Mise à jour pour le frame actuel</span><span class="sxs-lookup"><span data-stu-id="b756e-108">Update for the current frame</span></span>

<span data-ttu-id="b756e-109">Pour mettre à jour l’état de l’application pour hologrammes, une fois par frame de l’application sera :</span><span class="sxs-lookup"><span data-stu-id="b756e-109">To update the application state for holograms, once per frame the app will:</span></span>
* <span data-ttu-id="b756e-110">Obtenir un <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> à partir du système de gestion complet.</span><span class="sxs-lookup"><span data-stu-id="b756e-110">Get a <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> from the display management system.</span></span>
* <span data-ttu-id="b756e-111">Mettre à jour de la scène avec la prédiction actuelle d’où sera la vue de l’appareil photo lors de la restitution effectuée.</span><span class="sxs-lookup"><span data-stu-id="b756e-111">Update the scene with the current prediction of where the camera view will be when render is completed.</span></span> <span data-ttu-id="b756e-112">Notez qu’il peut y avoir plus d’un appareil photo pour la scène HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="b756e-112">Note, there can be more than one camera for the holographic scene.</span></span>

<span data-ttu-id="b756e-113">Pour restituer des vues de caméra HOLOGRAPHIQUE, une fois par frame de l’application sera :</span><span class="sxs-lookup"><span data-stu-id="b756e-113">To render to holographic camera views, once per frame the app will:</span></span>
* <span data-ttu-id="b756e-114">Pour chaque appareil photo, afficher la scène pour le frame actuel, à l’aide de matrices de projection et d’affichage de caméra à partir du système.</span><span class="sxs-lookup"><span data-stu-id="b756e-114">For each camera, render the scene for the current frame, using the camera view and projection matrices from the system.</span></span>

### <a name="create-a-new-holographic-frame-and-get-its-prediction"></a><span data-ttu-id="b756e-115">Créer un nouveau frame holographique et obtenir sa prédiction</span><span class="sxs-lookup"><span data-stu-id="b756e-115">Create a new holographic frame and get its prediction</span></span>

<span data-ttu-id="b756e-116">Le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> a des informations de l’application a besoin pour mettre à jour et afficher le frame actuel.</span><span class="sxs-lookup"><span data-stu-id="b756e-116">The <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> has information that the app needs in order to update and render the current frame.</span></span> <span data-ttu-id="b756e-117">L’application commence à chaque nouvelle image en appelant le **CreateNextFrame** (méthode).</span><span class="sxs-lookup"><span data-stu-id="b756e-117">The app begins each new frame by calling the **CreateNextFrame** method.</span></span> <span data-ttu-id="b756e-118">Lorsque cette méthode est appelée, les prédictions sont établies en utilisant les dernières données de capteur disponibles et encapsulées dans **CurrentPrediction** objet.</span><span class="sxs-lookup"><span data-stu-id="b756e-118">When this method is called, predictions are made using the latest sensor data available, and encapsulated in **CurrentPrediction** object.</span></span>

<span data-ttu-id="b756e-119">Un nouvel objet de frame doit être utilisé pour chaque frame rendu comme il est uniquement valide pendant un instant précis.</span><span class="sxs-lookup"><span data-stu-id="b756e-119">A new frame object must be used for each rendered frame as it is only valid for an instant in time.</span></span> <span data-ttu-id="b756e-120">Le **CurrentPrediction** propriété contient des informations telles que la position de la caméra.</span><span class="sxs-lookup"><span data-stu-id="b756e-120">The **CurrentPrediction** property contains information such as the camera position.</span></span> <span data-ttu-id="b756e-121">Les informations sont extrapolées à un moment exact de temps lorsque le frame est censé être visibles par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b756e-121">The information is extrapolated to the exact moment in time when the frame is expected to be visible to the user.</span></span>

<span data-ttu-id="b756e-122">Le code suivant est extrait de **AppMain::Update**:</span><span class="sxs-lookup"><span data-stu-id="b756e-122">The following code is excerpted from **AppMain::Update**:</span></span>

```cpp
// The HolographicFrame has information that the app needs in order
// to update and render the current frame. The app begins each new
// frame by calling CreateNextFrame.
HolographicFrame holographicFrame = m_holographicSpace.CreateNextFrame();

// Get a prediction of where holographic cameras will be when this frame
// is presented.
HolographicFramePrediction prediction = holographicFrame.CurrentPrediction();
```

### <a name="process-camera-updates"></a><span data-ttu-id="b756e-123">Mises à jour de la caméra de processus</span><span class="sxs-lookup"><span data-stu-id="b756e-123">Process camera updates</span></span>

<span data-ttu-id="b756e-124">Mémoires tampons d’arrière-plan peuvent changer à partir d’une image à l’autre.</span><span class="sxs-lookup"><span data-stu-id="b756e-124">Back buffers can change from frame to frame.</span></span> <span data-ttu-id="b756e-125">Votre application a besoin pour valider l’arrière de la mémoire tampon pour chaque appareil photo et mise en production et recréer les affichages de ressources et les tampons de profondeur en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="b756e-125">Your app needs to validate the back buffer for each camera, and release and recreate resource views and depth buffers as needed.</span></span> <span data-ttu-id="b756e-126">Notez que le jeu de risque de poser dans la prédiction est la liste faisant autorité des caméras utilisé dans le frame actuel.</span><span class="sxs-lookup"><span data-stu-id="b756e-126">Notice that the set of poses in the prediction is the authoritative list of cameras being used in the current frame.</span></span> <span data-ttu-id="b756e-127">En règle générale, vous utilisez cette liste pour itérer au sein de l’ensemble des appareils photo.</span><span class="sxs-lookup"><span data-stu-id="b756e-127">Usually, you use this list to iterate on the set of cameras.</span></span>

<span data-ttu-id="b756e-128">À partir de **AppMain::Update**:</span><span class="sxs-lookup"><span data-stu-id="b756e-128">From **AppMain::Update**:</span></span>

```cpp
m_deviceResources->EnsureCameraResources(holographicFrame, prediction);
```

<span data-ttu-id="b756e-129">À partir de **DeviceResources::EnsureCameraResources**:</span><span class="sxs-lookup"><span data-stu-id="b756e-129">From **DeviceResources::EnsureCameraResources**:</span></span>

```cpp
for (HolographicCameraPose const& cameraPose : prediction.CameraPoses())
{
    HolographicCameraRenderingParameters renderingParameters = frame.GetRenderingParameters(cameraPose);
    CameraResources* pCameraResources = cameraResourceMap[cameraPose.HolographicCamera().Id()].get();
    pCameraResources->CreateResourcesForBackBuffer(this, renderingParameters);
}
```

### <a name="get-the-coordinate-system-to-use-as-a-basis-for-rendering"></a><span data-ttu-id="b756e-130">Obtenir le système de coordonnées à utiliser comme base pour le rendu</span><span class="sxs-lookup"><span data-stu-id="b756e-130">Get the coordinate system to use as a basis for rendering</span></span>

<span data-ttu-id="b756e-131">Réalité mixte Windows permet à votre application de créer divers [systèmes de coordonnées](coordinate-systems-in-directx.md) en fonction des besoins, telles que l’image de référence jointes et de l’image de référence stationnaire, qui assurent le suivi des emplacements dans le monde physique.</span><span class="sxs-lookup"><span data-stu-id="b756e-131">Windows Mixed Reality lets your app create various [coordinate systems](coordinate-systems-in-directx.md) as needed, such as the attached reference frame and the stationary reference frame, that track locations in the physical world.</span></span> <span data-ttu-id="b756e-132">Votre application peut ensuite utiliser ces systèmes de coordonnées à raisonner sur l’emplacement afficher hologrammes chaque frame.</span><span class="sxs-lookup"><span data-stu-id="b756e-132">Your app can then use these coordinate systems to reason about where to render holograms each frame.</span></span> <span data-ttu-id="b756e-133">Lorsque vous demandez des coordonnées à partir d’une API, vous passerez toujours dans le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a> au sein de laquelle vous souhaitez que ces coordonnées exprimer.</span><span class="sxs-lookup"><span data-stu-id="b756e-133">When requesting coordinates from an API, you will always pass in the <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialcoordinatesystem" target="_blank">SpatialCoordinateSystem</a> within which you want those coordinates to be expressed.</span></span>

<span data-ttu-id="b756e-134">À partir de **AppMain::Update**:</span><span class="sxs-lookup"><span data-stu-id="b756e-134">From **AppMain::Update**:</span></span>

```cpp
pose = SpatialPointerPose::TryGetAtTimestamp(
    m_stationaryReferenceFrame.CoordinateSystem(), prediction.Timestamp());
```

<span data-ttu-id="b756e-135">Ces systèmes de coordonnées peut ensuite servir à générer des matrices de vue stéréo lors du rendu du contenu dans votre scène.</span><span class="sxs-lookup"><span data-stu-id="b756e-135">These coordinate systems can then be used to generate stereo view matrices when rendering the content in your scene.</span></span>

<span data-ttu-id="b756e-136">À partir de **CameraResources::UpdateViewProjectionBuffer**:</span><span class="sxs-lookup"><span data-stu-id="b756e-136">From **CameraResources::UpdateViewProjectionBuffer**:</span></span>

```cpp
// Get a container object with the view and projection matrices for the given
// pose in the given coordinate system.
auto viewTransformContainer = cameraPose.TryGetViewTransform(coordinateSystem);
```

### <a name="process-gaze-and-gesture-input"></a><span data-ttu-id="b756e-137">Regards de processus et des mouvements d’entrée</span><span class="sxs-lookup"><span data-stu-id="b756e-137">Process gaze and gesture input</span></span>

<span data-ttu-id="b756e-138">[Utilisation](gaze-in-directx.md) et [main](hands-and-motion-controllers-in-directx.md) d’entrée ne sont pas basés sur le temps et n’ayant donc pas à mettre à jour dans le **StepTimer** (fonction).</span><span class="sxs-lookup"><span data-stu-id="b756e-138">[Gaze](gaze-in-directx.md) and [hand](hands-and-motion-controllers-in-directx.md) input are not time-based and thus do not have to update in the **StepTimer** function.</span></span> <span data-ttu-id="b756e-139">Toutefois, cette entrée est quelque chose que l’application a besoin d’examiner chaque frame.</span><span class="sxs-lookup"><span data-stu-id="b756e-139">However this input is something that the app needs to look at each frame.</span></span>

### <a name="process-time-based-updates"></a><span data-ttu-id="b756e-140">Processus temporelle des mises à jour</span><span class="sxs-lookup"><span data-stu-id="b756e-140">Process time-based updates</span></span>

<span data-ttu-id="b756e-141">N’importe quelle application de rendu en temps réel sera besoin d’un moyen pour traiter les mises à jour heure ; Nous fournirons un moyen pour ce faire, dans le modèle d’application Windows HOLOGRAPHIQUE via un **StepTimer** implémentation.</span><span class="sxs-lookup"><span data-stu-id="b756e-141">Any real-time rendering app will need some way to process time-based updates; we provide a way to do this in the Windows Holographic app template via a **StepTimer** implementation.</span></span> <span data-ttu-id="b756e-142">Cela revient au StepTimer fourni dans le modèle application DirectX 11 UWP, par conséquent, si vous avez déjà consulté ce modèle vous devez être en terrain familier.</span><span class="sxs-lookup"><span data-stu-id="b756e-142">This is similar to the StepTimer provided in the DirectX 11 UWP app template, so if you already have looked at that template you should be on familiar ground.</span></span> <span data-ttu-id="b756e-143">Cette classe d’assistance d’exemple StepTimer est en mesure de fournir des mises à jour de temps fixes, ainsi que les mises à jour de temps variable, et le mode par défaut est celle de temps variable.</span><span class="sxs-lookup"><span data-stu-id="b756e-143">This StepTimer sample helper class is able to provide fixed time-step updates, as well as variable time-step updates, and the default mode is variable time steps.</span></span>

<span data-ttu-id="b756e-144">Dans le cas de rendu HOLOGRAPHIQUE, nous avons spécifiquement choisi de ne pas placer trop dans la fonction de minuteur.</span><span class="sxs-lookup"><span data-stu-id="b756e-144">In the case of holographic rendering, we've specifically chosen not to put too much into the timer function.</span></span> <span data-ttu-id="b756e-145">Il s’agit, car vous pouvez configurer pour qu’il soit une étape de temps fixe, auquel cas peut obtenir appelée plusieurs fois par frame – ou pas du tout, pour certaines images – et nos mises à jour de données HOLOGRAPHIQUE doivent se produire qu’une seule fois par trame.</span><span class="sxs-lookup"><span data-stu-id="b756e-145">This is because you can configure it to be a fixed time step, in which case it might get called more than once per frame – or not at all, for some frames – and our holographic data updates should happen once per frame.</span></span>


<span data-ttu-id="b756e-146">À partir de **AppMain::Update**:</span><span class="sxs-lookup"><span data-stu-id="b756e-146">From **AppMain::Update**:</span></span>

```cpp
m_timer.Tick([this]()
{
    m_spinningCubeRenderer->Update(m_timer);
});
```

### <a name="position-and-rotate-holograms-in-your-coordinate-system"></a><span data-ttu-id="b756e-147">Position et la rotation hologrammes dans votre système de coordonnées</span><span class="sxs-lookup"><span data-stu-id="b756e-147">Position and rotate holograms in your coordinate system</span></span>

<span data-ttu-id="b756e-148">Si vous évoluez dans un seul système de coordonnées, comme le fait le modèle avec le **SpatialStationaryReferenceFrame**, ce processus n’est pas différent de ce que vous êtes sinon utilisé dans les graphiques 3D.</span><span class="sxs-lookup"><span data-stu-id="b756e-148">If you are operating in a single coordinate system, as the template does with the **SpatialStationaryReferenceFrame**, this process isn't different from what you're otherwise used to in 3D graphics.</span></span> <span data-ttu-id="b756e-149">Ici, nous faire pivoter le cube et la valeur de la matrice de modèle par rapport à la position dans le système de coordonnées stationnaire.</span><span class="sxs-lookup"><span data-stu-id="b756e-149">Here, we rotate the cube and set the model matrix relative to the position in the stationary coordinate system.</span></span>

<span data-ttu-id="b756e-150">À partir de **SpinningCubeRenderer::Update**:</span><span class="sxs-lookup"><span data-stu-id="b756e-150">From **SpinningCubeRenderer::Update**:</span></span>

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

<span data-ttu-id="b756e-151">**Remarque sur les scénarios avancés :** Le cube en rotation est un exemple très simple de comment positionner un hologramme au sein d’une image de référence.</span><span class="sxs-lookup"><span data-stu-id="b756e-151">**Note about advanced scenarios:** The spinning cube is a very simple example of how to position a hologram within a single reference frame.</span></span> <span data-ttu-id="b756e-152">Il est également possible de [utiliser plusieurs SpatialCoordinateSystems](coordinate-systems-in-directx.md) dans le même frame rendu, en même temps.</span><span class="sxs-lookup"><span data-stu-id="b756e-152">It's also possible to [use multiple SpatialCoordinateSystems](coordinate-systems-in-directx.md) in the same rendered frame, at the same time.</span></span>

### <a name="update-constant-buffer-data"></a><span data-ttu-id="b756e-153">Mettre à jour les données de mémoire tampon constante</span><span class="sxs-lookup"><span data-stu-id="b756e-153">Update constant buffer data</span></span>

<span data-ttu-id="b756e-154">Transformations de modèle de contenu sont mis à jour comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="b756e-154">Model transforms for content are updated as usual.</span></span> <span data-ttu-id="b756e-155">À ce stade, vous serez calculée transformations valides pour le système de coordonnées que vous allez être rendu dans.</span><span class="sxs-lookup"><span data-stu-id="b756e-155">By now, you will have computed valid transforms for the coordinate system you'll be rendering in.</span></span>

<span data-ttu-id="b756e-156">À partir de **SpinningCubeRenderer::Update**:</span><span class="sxs-lookup"><span data-stu-id="b756e-156">From **SpinningCubeRenderer::Update**:</span></span>

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

<span data-ttu-id="b756e-157">Qu’en est-il des transformations de projection et d’affichage ?</span><span class="sxs-lookup"><span data-stu-id="b756e-157">What about view and projection transforms?</span></span> <span data-ttu-id="b756e-158">Pour de meilleurs résultats, nous souhaitons patienter jusqu'à ce que nous avons presque terminé pour nos appels de dessin avant de passer ces.</span><span class="sxs-lookup"><span data-stu-id="b756e-158">For best results, we want to wait until we're almost ready for our draw calls before we get these.</span></span>

## <a name="render-the-current-frame"></a><span data-ttu-id="b756e-159">Afficher le frame actuel</span><span class="sxs-lookup"><span data-stu-id="b756e-159">Render the current frame</span></span>

<span data-ttu-id="b756e-160">Rendu sur Windows Mixed Reality n’est pas très différent de rendu sur un écran de mono 2D, mais il existe des différences, que vous devez être conscient :</span><span class="sxs-lookup"><span data-stu-id="b756e-160">Rendering on Windows Mixed Reality is not much different from rendering on a 2D mono display, but there are some differences you need to be aware of:</span></span>
* <span data-ttu-id="b756e-161">Prédictions de frame HOLOGRAPHIQUE sont importantes.</span><span class="sxs-lookup"><span data-stu-id="b756e-161">Holographic frame predictions are important.</span></span> <span data-ttu-id="b756e-162">Le plus près la prédiction consiste à lorsque votre image est présentée, plus votre hologrammes ressemblera.</span><span class="sxs-lookup"><span data-stu-id="b756e-162">The closer the prediction is to when your frame is presented, the better your holograms will look.</span></span>
* <span data-ttu-id="b756e-163">Réalité mixte Windows contrôle les vues de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="b756e-163">Windows Mixed Reality controls the camera views.</span></span> <span data-ttu-id="b756e-164">Vous devez effectuer le rendu à chacun d'entre eux étant donné que le frame HOLOGRAPHIQUE présentera les pour vous plus tard.</span><span class="sxs-lookup"><span data-stu-id="b756e-164">You need to render to each one because the holographic frame will be presenting them for you later.</span></span>
* <span data-ttu-id="b756e-165">Rendu stéréo est recommandé d’être accomplies à l’aide de dessin instancié dans un tableau de cible de rendu.</span><span class="sxs-lookup"><span data-stu-id="b756e-165">Stereo rendering is recommended to be accomplished using instanced drawing to a render target array.</span></span> <span data-ttu-id="b756e-166">Le modèle d’application HOLOGRAPHIQUE utilise l’approche recommandée du dessin instancié dans un tableau de cible de rendu, qui utilise une vue de cible de rendu sur un **Texture2DArray**.</span><span class="sxs-lookup"><span data-stu-id="b756e-166">The holographic app template uses the recommended approach of instanced drawing to a render target array, which uses a render target view onto a **Texture2DArray**.</span></span>
* <span data-ttu-id="b756e-167">Si vous souhaitez restituer sans utiliser l’instanciation stéréo, vous devez créer deux non-tableau RenderTargetViews (une pour chaque œil) que chaque référence à un des deux tranches dans le **Texture2DArray** fourni à l’application à partir du système.</span><span class="sxs-lookup"><span data-stu-id="b756e-167">If you want to render without using stereo instancing, you will need to create two non-array RenderTargetViews (one for each eye) that each reference one of the two slices in the **Texture2DArray** provided to the app from the system.</span></span> <span data-ttu-id="b756e-168">Ceci n’est pas recommandé, car il est généralement beaucoup plus lent que l’utilisation de l’instanciation.</span><span class="sxs-lookup"><span data-stu-id="b756e-168">This is not recommended, as it is typically significantly slower than using instancing.</span></span>

### <a name="get-an-updated-holographicframe-prediction"></a><span data-ttu-id="b756e-169">Obtenir une prédiction HolographicFrame mis à jour</span><span class="sxs-lookup"><span data-stu-id="b756e-169">Get an updated HolographicFrame prediction</span></span>

<span data-ttu-id="b756e-170">La prédiction de frame de la mise à jour améliore l’efficacité de stabilisation de l’image, tout en permettant un positionnement plus précis des hologrammes en raison du temps plus court entre la prédiction et lorsque le frame est visible par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b756e-170">Updating the frame prediction enhances the effectiveness of image stabilization and allows for more accurate positioning of holograms due to the shorter time between the prediction and when the frame is visible to the user.</span></span> <span data-ttu-id="b756e-171">Dans l’idéal, mettez à jour votre prédiction trame juste avant le rendu.</span><span class="sxs-lookup"><span data-stu-id="b756e-171">Ideally update your frame prediction just before rendering.</span></span>

```cpp
holographicFrame.UpdateCurrentPrediction();
HolographicFramePrediction prediction = holographicFrame.CurrentPrediction();
```

### <a name="render-to-each-camera"></a><span data-ttu-id="b756e-172">Restituer à chaque appareil photo</span><span class="sxs-lookup"><span data-stu-id="b756e-172">Render to each camera</span></span>

<span data-ttu-id="b756e-173">Boucle sur l’ensemble de la pose d’appareil photo dans la prédiction et restituer à chaque appareil photo dans cet ensemble.</span><span class="sxs-lookup"><span data-stu-id="b756e-173">Loop on the set of camera poses in the prediction, and render to each camera in this set.</span></span>

<span data-ttu-id="b756e-174">**Configurer votre passe de rendu**</span><span class="sxs-lookup"><span data-stu-id="b756e-174">**Set up your rendering pass**</span></span>

<span data-ttu-id="b756e-175">Réalité mixte Windows utilisant des rendu stéréoscopique pour améliorer l’illusion de profondeur et à rendre grâce, gauche et l’affichage de droite sont actifs.</span><span class="sxs-lookup"><span data-stu-id="b756e-175">Windows Mixed Reality uses stereoscopic rendering to enhance the illusion of depth and to render stereoscopically, so both the left and the right display are active.</span></span> <span data-ttu-id="b756e-176">Avec le rendu stéréoscopique existe un décalage entre les deux écrans, le cerveau peut également rapprocher comme profondeur réelle.</span><span class="sxs-lookup"><span data-stu-id="b756e-176">With stereoscopic rendering there is an offset between the two displays, which the brain can reconcile as actual depth.</span></span> <span data-ttu-id="b756e-177">Cet section couvre stéréoscopique rendu à l’aide de l’instanciation, à l’aide de code à partir du modèle d’application Windows HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="b756e-177">This section covers stereoscopic rendering using instancing, using code from the Windows Holographic app template.</span></span>

<span data-ttu-id="b756e-178">Chaque caméra a son propre rendu les matrices de projection et cible (mémoire tampon d’arrière-plan) et d’affichage, dans l’espace HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="b756e-178">Each camera has its own render target (back buffer), and view and projection matrices, into the holographic space.</span></span> <span data-ttu-id="b756e-179">Votre application devra créer d’autres ressources basée sur l’appareil photo - telles que la mémoire tampon de profondeur - sur une base par caméra.</span><span class="sxs-lookup"><span data-stu-id="b756e-179">Your app will need to create any other camera-based resources - such as the depth buffer - on a per-camera basis.</span></span> <span data-ttu-id="b756e-180">Dans le modèle d’application Windows HOLOGRAPHIQUE, nous fournissons une classe d’assistance pour regrouper ces ressources dans DX::CameraResources.</span><span class="sxs-lookup"><span data-stu-id="b756e-180">In the Windows Holographic app template, we provide a helper class to bundle these resources together in DX::CameraResources.</span></span> <span data-ttu-id="b756e-181">Commencez par configurer les affichages de cible de rendu :</span><span class="sxs-lookup"><span data-stu-id="b756e-181">Start by setting up the render target views:</span></span>

<span data-ttu-id="b756e-182">À partir de **AppMain::Render**:</span><span class="sxs-lookup"><span data-stu-id="b756e-182">From **AppMain::Render**:</span></span>

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

<span data-ttu-id="b756e-183">**Utiliser la prédiction pour obtenir les matrices de projection et d’affichage pour l’appareil photo**</span><span class="sxs-lookup"><span data-stu-id="b756e-183">**Use the prediction to get the view and projection matrices for the camera**</span></span>

<span data-ttu-id="b756e-184">Les matrices de projection et d’affichage pour chaque caméra HOLOGRAPHIQUE change avec chaque trame.</span><span class="sxs-lookup"><span data-stu-id="b756e-184">The view and projection matrices for each holographic camera will change with every frame.</span></span> <span data-ttu-id="b756e-185">Actualiser les données dans la mémoire tampon constante pour chaque caméra HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="b756e-185">Refresh the data in the constant buffer for each holographic camera.</span></span> <span data-ttu-id="b756e-186">Faire une fois la mise à jour de la prédiction, et avant d’effectuer les appels de n’importe quel dessin pour cet appareil photo.</span><span class="sxs-lookup"><span data-stu-id="b756e-186">Do this after you updated the prediction, and before you make any draw calls for that camera.</span></span>

<span data-ttu-id="b756e-187">À partir de **AppMain::Render**:</span><span class="sxs-lookup"><span data-stu-id="b756e-187">From **AppMain::Render**:</span></span>

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

<span data-ttu-id="b756e-188">Ici, nous montrons comment les matrices sont acquis à partir de la pose d’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="b756e-188">Here, we show how the matrices are acquired from the camera pose.</span></span> <span data-ttu-id="b756e-189">Pendant ce processus, nous obtenons également la fenêtre d’affichage actuel de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="b756e-189">During this process we also obtain the current viewport for the camera.</span></span> <span data-ttu-id="b756e-190">Notez comment nous fournissons un système de coordonnées : il s’agit du même système de coordonnées nous permet de comprendre les regards, et il est identique à celui nous avons utilisé pour positionner le cube en rotation.</span><span class="sxs-lookup"><span data-stu-id="b756e-190">Note how we provide a coordinate system: this is the same coordinate system we used to understand gaze, and it's the same one we used to position the spinning cube.</span></span>


<span data-ttu-id="b756e-191">À partir de **CameraResources::UpdateViewProjectionBuffer**:</span><span class="sxs-lookup"><span data-stu-id="b756e-191">From **CameraResources::UpdateViewProjectionBuffer**:</span></span>

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

<span data-ttu-id="b756e-192">Chaque trame doit être défini à la fenêtre d’affichage.</span><span class="sxs-lookup"><span data-stu-id="b756e-192">The viewport should be set each frame.</span></span> <span data-ttu-id="b756e-193">Votre nuanceur de sommets (au moins) généralement devront accéder aux données de projection de la vue.</span><span class="sxs-lookup"><span data-stu-id="b756e-193">Your vertex shader (at least) will generally need access to the view/projection data.</span></span>


<span data-ttu-id="b756e-194">À partir de **CameraResources::AttachViewProjectionBuffer**:</span><span class="sxs-lookup"><span data-stu-id="b756e-194">From **CameraResources::AttachViewProjectionBuffer**:</span></span>

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

<span data-ttu-id="b756e-195">**Rendu à la mémoire tampon d’arrière-plan caméra et valider le tampon de profondeur**:</span><span class="sxs-lookup"><span data-stu-id="b756e-195">**Render to the camera back buffer and commit the depth buffer**:</span></span>

<span data-ttu-id="b756e-196">Il est judicieux de vérifier que **TryGetViewTransform** a réussi avant d’essayer d’utiliser les données de la projection de la vue, car si le système de coordonnées n’est pas localisable (par exemple, le suivi a été interrompu) votre application ne peut pas obtenir un rendu correspondant frame.</span><span class="sxs-lookup"><span data-stu-id="b756e-196">It's a good idea to check that **TryGetViewTransform** succeeded before trying to use the view/projection data, because if the coordinate system is not locatable (e.g., tracking was interrupted) your app cannot render with it for that frame.</span></span> <span data-ttu-id="b756e-197">Le modèle appelle uniquement **restituer** sur le cube en rotation si le **CameraResources** classe indique une mise à jour réussie.</span><span class="sxs-lookup"><span data-stu-id="b756e-197">The template only calls **Render** on the spinning cube if the **CameraResources** class indicates a successful update.</span></span>

<span data-ttu-id="b756e-198">Pour conserver hologrammes où un développeur ou un utilisateur les place dans le monde, réalité mixte Windows inclut des fonctionnalités pour [stabilisation de l’image](hologram-stability.md).</span><span class="sxs-lookup"><span data-stu-id="b756e-198">To keep holograms where a developer or a user puts them in the world, Windows Mixed Reality includes features for [image stabilization](hologram-stability.md).</span></span> <span data-ttu-id="b756e-199">Stabilisation de l’image permet de masquer la latence inhérente dans un pipeline de rendu pour garantir les meilleures expériences HOLOGRAPHIQUE pour les utilisateurs ; un point de focus peut être spécifié pour améliorer la stabilisation image encore plus loin, ou un mémoire tampon de profondeur peut être fourni à calcul optimisé stabilisation d’image en temps réel.</span><span class="sxs-lookup"><span data-stu-id="b756e-199">Image stabilization helps hide the latency inherent in a rendering pipeline to ensure the best holographic experiences for users; a focus point may be specified to enhance image stabilization even further, or a depth buffer may be provided to compute optimized image stabilization in real time.</span></span>

<span data-ttu-id="b756e-200">Pour de meilleurs résultats, votre application doit fournir une mémoire tampon de profondeur à l’aide de la <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer" target="_blank">CommitDirect3D11DepthBuffer</a> API.</span><span class="sxs-lookup"><span data-stu-id="b756e-200">For best results, your app should provide a depth buffer using the <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer" target="_blank">CommitDirect3D11DepthBuffer</a> API.</span></span> <span data-ttu-id="b756e-201">Réalité mixte Windows peut ensuite utiliser informations sur la géométrie à partir de la mémoire tampon de profondeur pour optimiser la stabilisation d’image en temps réel.</span><span class="sxs-lookup"><span data-stu-id="b756e-201">Windows Mixed Reality can then use geometry information from the depth buffer to optimize image stabilization in real time.</span></span> <span data-ttu-id="b756e-202">Le modèle d’application Windows HOLOGRAPHIQUE valide la mémoire tampon de profondeur de l’application par défaut, aider à optimiser la stabilité hologramme.</span><span class="sxs-lookup"><span data-stu-id="b756e-202">The Windows Holographic app template commits the app's depth buffer by default, helping optimize hologram stability.</span></span>

<span data-ttu-id="b756e-203">À partir de **AppMain::Render**:</span><span class="sxs-lookup"><span data-stu-id="b756e-203">From **AppMain::Render**:</span></span>

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
><span data-ttu-id="b756e-204">Windows traite votre texture de profondeur sur le GPU, elle doit donc être possible d’utiliser votre mémoire tampon de profondeur comme une ressource de nuanceur.</span><span class="sxs-lookup"><span data-stu-id="b756e-204">Windows will process your depth texture on the GPU, so it must be possible to use your depth buffer as a shader resource.</span></span> <span data-ttu-id="b756e-205">ID3D11Texture2D que vous créez doit être dans un format sans type, et il doit être lié comme une vue de ressource de nuanceur.</span><span class="sxs-lookup"><span data-stu-id="b756e-205">The ID3D11Texture2D that you create should be in a typeless format and it should be bound as a shader resource view.</span></span> <span data-ttu-id="b756e-206">Voici un exemple montrant comment créer une texture de profondeur qui peut être validée pour la stabilisation de l’image.</span><span class="sxs-lookup"><span data-stu-id="b756e-206">Here is an example of how to create a depth texture that can be committed for image stabilization.</span></span>

<span data-ttu-id="b756e-207">Code pour **création de ressources de mémoire tampon de profondeur pour CommitDirect3D11DepthBuffer**:</span><span class="sxs-lookup"><span data-stu-id="b756e-207">Code for **Depth buffer resource creation for CommitDirect3D11DepthBuffer**:</span></span>

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

<span data-ttu-id="b756e-208">**Dessiner le contenu HOLOGRAPHIQUE**</span><span class="sxs-lookup"><span data-stu-id="b756e-208">**Draw holographic content**</span></span>

<span data-ttu-id="b756e-209">Le modèle d’application Windows HOLOGRAPHIQUE restitue le contenu en stéréo à l’aide de la technique recommandée de dessin géométrique instanciée à un Texture2DArray de taille de 2.</span><span class="sxs-lookup"><span data-stu-id="b756e-209">The Windows Holographic app template renders content in stereo by using the recommended technique of drawing instanced geometry to a Texture2DArray of size 2.</span></span> <span data-ttu-id="b756e-210">Examinons la partie instanciation de cela, et comment elle fonctionne sur Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="b756e-210">Let's look at the instancing part of this, and how it works on Windows Mixed Reality.</span></span>

<span data-ttu-id="b756e-211">À partir de **SpinningCubeRenderer::Render**:</span><span class="sxs-lookup"><span data-stu-id="b756e-211">From **SpinningCubeRenderer::Render**:</span></span>

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

<span data-ttu-id="b756e-212">Chaque instance accède à une matrice de projection et d’affichage différent à partir de la mémoire tampon constante.</span><span class="sxs-lookup"><span data-stu-id="b756e-212">Each instance accesses a different view/projection matrix from the constant buffer.</span></span> <span data-ttu-id="b756e-213">Voici la structure de mémoire tampon constante, ce qui est simplement un tableau de 2 matrices.</span><span class="sxs-lookup"><span data-stu-id="b756e-213">Here's the constant buffer structure, which is just an array of 2 matrices.</span></span>

<span data-ttu-id="b756e-214">À partir de **VertexShaderShared.hlsl**, fourni par **VPRTVertexShader.hlsl**:</span><span class="sxs-lookup"><span data-stu-id="b756e-214">From **VertexShaderShared.hlsl**, included by **VPRTVertexShader.hlsl**:</span></span>

```HLSL
// A constant buffer that stores each set of view and projection matrices in column-major format.
cbuffer ViewProjectionConstantBuffer : register(b1)
{
    float4x4 viewProjection[2];
};
```

<span data-ttu-id="b756e-215">L’index de tableau de cible de rendu doit être définie pour chaque pixel.</span><span class="sxs-lookup"><span data-stu-id="b756e-215">The render target array index must be set for each pixel.</span></span> <span data-ttu-id="b756e-216">Dans l’extrait de code suivant, output.viewId est mappé à la **SV_RenderTargetArrayIndex** sémantique.</span><span class="sxs-lookup"><span data-stu-id="b756e-216">In the following snippet, output.viewId is mapped to the **SV_RenderTargetArrayIndex** semantic.</span></span> <span data-ttu-id="b756e-217">Notez que cela nécessite de prise en charge pour une fonctionnalité de Direct3D 11.3 facultative, qui permet la sémantique soit définie à partir de n’importe quelle étape du nuanceur de l’index de tableau de cible de rendu.</span><span class="sxs-lookup"><span data-stu-id="b756e-217">Note that this requires support for an optional Direct3D 11.3 feature, which allows the render target array index semantic to be set from any shader stage.</span></span>

<span data-ttu-id="b756e-218">À partir de **VPRTVertexShader.hlsl**:</span><span class="sxs-lookup"><span data-stu-id="b756e-218">From **VPRTVertexShader.hlsl**:</span></span>

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

<span data-ttu-id="b756e-219">À partir de **VertexShaderShared.hlsl**, fourni par **VPRTVertexShader.hlsl**:</span><span class="sxs-lookup"><span data-stu-id="b756e-219">From **VertexShaderShared.hlsl**, included by **VPRTVertexShader.hlsl**:</span></span>

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

<span data-ttu-id="b756e-220">Si vous souhaitez utiliser vos instances existantes des techniques de dessins avec cette méthode de dessin pour un stéréo restituer tableau cible, il vous suffit est dessiner deux fois le nombre d’instances que vous avez normalement.</span><span class="sxs-lookup"><span data-stu-id="b756e-220">If you want to use your existing instanced drawing techniques with this method of drawing to a stereo render target array, all you have to do is draw twice the number of instances you normally have.</span></span> <span data-ttu-id="b756e-221">Dans le nuanceur, divisez **input.instId** par 2 pour obtenir l’ID d’instance d’origine, qui peuvent être indexé (par exemple) sur une mémoire tampon de données de par objet : `int actualIdx = input.instId / 2;`</span><span class="sxs-lookup"><span data-stu-id="b756e-221">In the shader, divide **input.instId** by 2 to get the original instance ID, which can be indexed into (for example) a buffer of per-object data: `int actualIdx = input.instId / 2;`</span></span>

### <a name="important-note-about-rendering-stereo-content-on-hololens"></a><span data-ttu-id="b756e-222">Remarque importante sur le rendu de contenu stéréo sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="b756e-222">Important note about rendering stereo content on HoloLens</span></span>

<span data-ttu-id="b756e-223">Réalité mixte Windows prend en charge la possibilité de définir l’index de tableau de cible de rendu à partir de n’importe quelle étape du nuanceur ; en règle générale, il s’agit d’une tâche qui peut être effectuée uniquement dans l’étape du nuanceur de géométrie en raison de la façon dont la sémantique est définie pour Direct3D 11.</span><span class="sxs-lookup"><span data-stu-id="b756e-223">Windows Mixed Reality supports the ability to set the render target array index from any shader stage; normally, this is a task that could only be done in the geometry shader stage due to the way the semantic is defined for Direct3D 11.</span></span> <span data-ttu-id="b756e-224">Ici, nous présentons un exemple complet montrant comment configurer un pipeline de rendu avec simplement le sommets et pixels nuanceur étapes ensemble.</span><span class="sxs-lookup"><span data-stu-id="b756e-224">Here, we show a complete example of how to set up a rendering pipeline with just the vertex and pixel shader stages set.</span></span> <span data-ttu-id="b756e-225">Le code du nuanceur est comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b756e-225">The shader code is as described above.</span></span>

<span data-ttu-id="b756e-226">À partir de **SpinningCubeRenderer::Render**:</span><span class="sxs-lookup"><span data-stu-id="b756e-226">From **SpinningCubeRenderer::Render**:</span></span>

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

### <a name="important-note-about-rendering-on-non-hololens-devices"></a><span data-ttu-id="b756e-227">Remarque importante sur le rendu sur les appareils non HoloLens</span><span class="sxs-lookup"><span data-stu-id="b756e-227">Important note about rendering on non-HoloLens devices</span></span>

<span data-ttu-id="b756e-228">Définition de l’index de tableau de cible de rendu dans le nuanceur de sommets nécessite que le pilote graphique prend en charge une fonctionnalité de Direct3D 11.3 facultative, HoloLens ne prend pas en charge.</span><span class="sxs-lookup"><span data-stu-id="b756e-228">Setting the render target array index in the vertex shader requires that the graphics driver supports an optional Direct3D 11.3 feature, which HoloLens does support.</span></span> <span data-ttu-id="b756e-229">Votre application peut être en mesure d’implémenter en toute sécurité simplement cette technique pour le rendu, et toutes les exigences seront respectées dans s’exécutant sur le Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b756e-229">Your app may be able to safely implement just that technique for rendering, and all requirements will be met for running on the Microsoft HoloLens.</span></span>

<span data-ttu-id="b756e-230">Il peut arriver que vous souhaitez utiliser l’émulateur de HoloLens, ce qui peut être un outil de développement puissant pour votre application holographique - et prendre en charge les périphériques des casques IMMERSIFS Windows Mixed Reality qui sont attachés à un PC Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b756e-230">It may be the case that you want to use the HoloLens emulator as well, which can be a powerful development tool for your holographic app - and support Windows Mixed Reality immersive headset devices that are attached to Windows 10 PCs.</span></span> <span data-ttu-id="b756e-231">Prise en charge pour le chemin d’accès de rendu non HoloLens - et par conséquent, pour tous les Windows Mixed Reality - est également intégrée dans le modèle d’application Windows HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="b756e-231">Support for the non-HoloLens rendering path - and therefore, for all of Windows Mixed Reality - is also built into the Windows Holographic app template.</span></span> <span data-ttu-id="b756e-232">Dans le code du modèle, vous trouverez le code pour activer votre application HOLOGRAPHIQUE s’exécute sur le GPU dans votre PC de développement.</span><span class="sxs-lookup"><span data-stu-id="b756e-232">In the template code, you will find code to enable your holographic app to run on the GPU in your development PC.</span></span> <span data-ttu-id="b756e-233">Voici comment la **DeviceResources** vérifie cette prise en charge de la fonctionnalité facultative de la classe.</span><span class="sxs-lookup"><span data-stu-id="b756e-233">Here is how the **DeviceResources** class checks for this optional feature support.</span></span>

<span data-ttu-id="b756e-234">À partir de **DeviceResources::CreateDeviceResources**:</span><span class="sxs-lookup"><span data-stu-id="b756e-234">From **DeviceResources::CreateDeviceResources**:</span></span>

```cpp
// Check for device support for the optional feature that allows setting the render target array index from the vertex shader stage.
D3D11_FEATURE_DATA_D3D11_OPTIONS3 options;
m_d3dDevice->CheckFeatureSupport(D3D11_FEATURE_D3D11_OPTIONS3, &options, sizeof(options));
if (options.VPAndRTArrayIndexFromAnyShaderFeedingRasterizer)
{
    m_supportsVprt = true;
}
```

<span data-ttu-id="b756e-235">Pour prendre en charge du rendu sans cette fonctionnalité optionnelle, votre application doit utiliser un nuanceur de géométrie pour définir l’index de tableau de cible de rendu.</span><span class="sxs-lookup"><span data-stu-id="b756e-235">To support rendering without this optional feature, your app must use a geometry shader to set the render target array index.</span></span> <span data-ttu-id="b756e-236">Cet extrait de code serait ajouté *après* **VSSetConstantBuffers**, et *avant* **PSSetShader** dans l’exemple de code indiqué dans le précédent section qui explique comment effectuer le rendu stéréo sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b756e-236">This snippet would be added *after* **VSSetConstantBuffers**, and *before* **PSSetShader** in the code example shown in the previous section that explains how to render stereo on HoloLens.</span></span>

<span data-ttu-id="b756e-237">À partir de **SpinningCubeRenderer::Render**:</span><span class="sxs-lookup"><span data-stu-id="b756e-237">From **SpinningCubeRenderer::Render**:</span></span>

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

<span data-ttu-id="b756e-238">**REMARQUE DE HLSL**: Dans ce cas, vous devez également charger un nuanceur de sommets légèrement modifiée qui transmet l’index de tableau de cible de rendu pour le nuanceur de géométrie à l’aide d’un sémantique, telles que TEXCOORD0 de nuanceur toujours autorisé.</span><span class="sxs-lookup"><span data-stu-id="b756e-238">**HLSL NOTE**: In this case, you must also load a slightly modified vertex shader that passes the render target array index to the geometry shader using an always-allowed shader semantic, such as TEXCOORD0.</span></span> <span data-ttu-id="b756e-239">Le nuanceur de géométrie ne devra pas effectuer le travail ; le nuanceur de géométrie modèle traverse toutes les données, à l’exception de l’index de tableau de cible de rendu, qui est utilisé pour définir le SV_RenderTargetArrayIndex sémantique.</span><span class="sxs-lookup"><span data-stu-id="b756e-239">The geometry shader does not have to do any work; the template geometry shader passes through all data, with the exception of the render target array index, which is used to set the SV_RenderTargetArrayIndex semantic.</span></span>

<span data-ttu-id="b756e-240">Code de modèle d’application pour **GeometryShader.hlsl**:</span><span class="sxs-lookup"><span data-stu-id="b756e-240">App template code for **GeometryShader.hlsl**:</span></span>

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

## <a name="present"></a><span data-ttu-id="b756e-241">Présent</span><span class="sxs-lookup"><span data-stu-id="b756e-241">Present</span></span>

### <a name="enable-the-holographic-frame-to-present-the-swap-chain"></a><span data-ttu-id="b756e-242">Activer le frame HOLOGRAPHIQUE présenter la chaîne de permutation</span><span class="sxs-lookup"><span data-stu-id="b756e-242">Enable the holographic frame to present the swap chain</span></span>

<span data-ttu-id="b756e-243">Avec Windows Mixed Reality, le système de contrôle de la chaîne de permutation.</span><span class="sxs-lookup"><span data-stu-id="b756e-243">With Windows Mixed Reality, the system controls the swap chain.</span></span> <span data-ttu-id="b756e-244">Le système gère ensuite les images présentant à chaque caméra HOLOGRAPHIQUE pour garantir une expérience utilisateur de haute qualité.</span><span class="sxs-lookup"><span data-stu-id="b756e-244">The system then manages presenting frames to each holographic camera to ensure a high quality user experience.</span></span> <span data-ttu-id="b756e-245">Il fournit également une mise à jour de la fenêtre d’affichage chaque trame, pour chaque appareil photo, pour optimiser les aspects du système tels que la stabilisation de l’image ou de capturer de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="b756e-245">It also provides a viewport update each frame, for each camera, to optimize aspects of the system such as image stabilization or Mixed Reality Capture.</span></span> <span data-ttu-id="b756e-246">Par conséquent, une application HOLOGRAPHIQUE à l’aide de DirectX n’appelle pas **présent** sur un DXGI chaîne de permutation.</span><span class="sxs-lookup"><span data-stu-id="b756e-246">So, a holographic app using DirectX doesn't call **Present** on a DXGI swap chain.</span></span> <span data-ttu-id="b756e-247">Au lieu de cela, vous utilisez le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> classe pour présenter toutes les chaînes d’échange pour un frame, une fois que vous avez terminé dessiner.</span><span class="sxs-lookup"><span data-stu-id="b756e-247">Instead, you use the <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> class to present all swapchains for a frame once you're done drawing it.</span></span>

<span data-ttu-id="b756e-248">À partir de **DeviceResources::Present**:</span><span class="sxs-lookup"><span data-stu-id="b756e-248">From **DeviceResources::Present**:</span></span>

```
HolographicFramePresentResult presentResult = frame.PresentUsingCurrentPrediction();
```

<span data-ttu-id="b756e-249">Par défaut, cette API attend que le frame à terminer avant de retourner.</span><span class="sxs-lookup"><span data-stu-id="b756e-249">By default, this API waits for the frame to finish before it returns.</span></span> <span data-ttu-id="b756e-250">Applications HOLOGRAPHIQUE doivent attendre l’image précédente soit terminée avant de commencer à travailler sur un nouveau frame, car cela réduit la latence, tout en permettant de meilleurs résultats à partir des prédictions de frame HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="b756e-250">Holographic apps should wait for the previous frame to finish before starting work on a new frame, because this reduces latency and allows for better results from holographic frame predictions.</span></span> <span data-ttu-id="b756e-251">Ce n’est pas une règle de disque dur et si vous avez les trames qui durent plus longtemps que l’actualisation d’un seul écran pour vous rendre peuvent désactiver cette attente en transmettant le paramètre HolographicFramePresentWaitBehavior à <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.presentusingcurrentprediction" target="_blank">PresentUsingCurrentPrediction</a>.</span><span class="sxs-lookup"><span data-stu-id="b756e-251">This isn't a hard rule, and if you have frames that take longer than one screen refresh to render you can disable this wait by passing the HolographicFramePresentWaitBehavior parameter to <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.presentusingcurrentprediction" target="_blank">PresentUsingCurrentPrediction</a>.</span></span> <span data-ttu-id="b756e-252">Dans ce cas, vous utiliseriez probablement un thread de rendu asynchrone afin de maintenir une charge continue sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="b756e-252">In this case, you would likely use an asynchronous rendering thread in order to maintain a continuous load on the GPU.</span></span> <span data-ttu-id="b756e-253">Notez que la fréquence de rafraîchissement de l’appareil HoloLens est 60hz, où une image a une durée égale à environ 16 ms.</span><span class="sxs-lookup"><span data-stu-id="b756e-253">Note that the refresh rate of the HoloLens device is 60hz, where one frame has a duration of approximately 16 ms.</span></span> <span data-ttu-id="b756e-254">Périphériques des casques IMMERSIFS peuvent varier de 60hz à 90hz ; lors de l’actualisation de l’affichage à 90 hz, chaque image aura une durée égale à environ 11 ms.</span><span class="sxs-lookup"><span data-stu-id="b756e-254">Immersive headset devices can range from 60hz to 90hz; when refreshing the display at 90 hz, each frame will have a duration of approximately 11 ms.</span></span>

### <a name="handle-devicelost-scenarios-in-cooperation-with-the-holographicframe"></a><span data-ttu-id="b756e-255">Gestion de scénarios DeviceLost en coopération avec le HolographicFrame</span><span class="sxs-lookup"><span data-stu-id="b756e-255">Handle DeviceLost scenarios in cooperation with the HolographicFrame</span></span>

<span data-ttu-id="b756e-256">Les applications DirectX 11 souhaiteriez vérifier le HRESULT retourné par la chaîne de permutation DXGI **présent** fonction pour déterminer s’il y avait un **DeviceLost** erreur.</span><span class="sxs-lookup"><span data-stu-id="b756e-256">DirectX 11 apps would typically want to check the HRESULT returned by the DXGI swap chain's **Present** function to find out if there was a **DeviceLost** error.</span></span> <span data-ttu-id="b756e-257">Le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> classe gère cela automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b756e-257">The <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe" target="_blank">HolographicFrame</a> class handles this for you.</span></span> <span data-ttu-id="b756e-258">Inspecter le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframepresentresult" target="_blank">HolographicFramePresentResult</a> qu’il retourne pour savoir si vous devez libérer et recréer les appareil de Direct3D et les ressources basées sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="b756e-258">Inspect the <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframepresentresult" target="_blank">HolographicFramePresentResult</a> it returns to find out if you need to release and recreate the Direct3D device and device-based resources.</span></span>

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

<span data-ttu-id="b756e-259">Notez que si le périphérique Direct3D a été perdu et que vous l’avez fait la recréer, vous devez indiquer le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> pour commencer à utiliser le nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="b756e-259">Note that if the Direct3D device was lost, and you did recreate it, you have to tell the <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> to start using the new device.</span></span> <span data-ttu-id="b756e-260">La chaîne de permutation est recréée pour cet appareil.</span><span class="sxs-lookup"><span data-stu-id="b756e-260">The swap chain will be recreated for this device.</span></span>

<span data-ttu-id="b756e-261">À partir de **DeviceResources::InitializeUsingHolographicSpace**:</span><span class="sxs-lookup"><span data-stu-id="b756e-261">From **DeviceResources::InitializeUsingHolographicSpace**:</span></span>

```
m_holographicSpace.SetDirect3D11Device(m_d3dInteropDevice);
```

<span data-ttu-id="b756e-262">Une fois que votre image est présentée, vous pouvez revenir à la boucle de programme principal et lui permettre de continuer à l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="b756e-262">Once your frame is presented, you can return back to the main program loop and allow it to continue to the next frame.</span></span>

## <a name="hybrid-graphics-pcs-and-mixed-reality-applications"></a><span data-ttu-id="b756e-263">PC de graphiques hybrides et les applications de réalité mixte</span><span class="sxs-lookup"><span data-stu-id="b756e-263">Hybrid graphics PCs and mixed reality applications</span></span>

<span data-ttu-id="b756e-264">Windows 10 Creators Update PC peuvent être configurés avec **à la fois** GPU discrets et intégrées.</span><span class="sxs-lookup"><span data-stu-id="b756e-264">Windows 10 Creators Update PCs may be configured with **both** discrete and integrated GPUs.</span></span> <span data-ttu-id="b756e-265">Avec ces types d’ordinateurs, Windows choisira l’adaptateur à que le casque est connecté.</span><span class="sxs-lookup"><span data-stu-id="b756e-265">With these types of computers, Windows will choose the adapter the headset is connected to.</span></span> <span data-ttu-id="b756e-266">Applications doivent s’assurer de l’appareil de DirectX qu'il crée utilise la même carte.</span><span class="sxs-lookup"><span data-stu-id="b756e-266">Applications must ensure the DirectX device it creates uses the same adapter.</span></span>

<span data-ttu-id="b756e-267">Exemple de code de Direct3D plus général illustre la création d’un périphérique DirectX à l’aide de l’adaptateur de matériel par défaut, qui ne peut pas être identique à celui utilisé pour le casque sur un système hybride.</span><span class="sxs-lookup"><span data-stu-id="b756e-267">Most general Direct3D sample code demonstrates creating a DirectX device using the default hardware adapter, which on a hybrid system may not be the same as the one used for the headset.</span></span>

<span data-ttu-id="b756e-268">Pour contourner les problèmes que cela peut entraîner, utilisez le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicadapterid" target="_blank">HolographicAdapterId</a> à partir de le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>. PrimaryAdapterId() ou <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicdisplay" target="_blank">HolographicDisplay</a>. AdapterId().</span><span class="sxs-lookup"><span data-stu-id="b756e-268">To work around any issues this may cause, use the <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicadapterid" target="_blank">HolographicAdapterId</a> from either <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>.PrimaryAdapterId() or <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicdisplay" target="_blank">HolographicDisplay</a>.AdapterId().</span></span> <span data-ttu-id="b756e-269">Cette adapterId peut ensuite servir à sélectionner le DXGIAdapter droit à l’aide de IDXGIFactory4.EnumAdapterByLuid.</span><span class="sxs-lookup"><span data-stu-id="b756e-269">This adapterId can then be used to select the right DXGIAdapter using IDXGIFactory4.EnumAdapterByLuid.</span></span>

<span data-ttu-id="b756e-270">À partir de **DeviceResources::InitializeUsingHolographicSpace**:</span><span class="sxs-lookup"><span data-stu-id="b756e-270">From **DeviceResources::InitializeUsingHolographicSpace**:</span></span>

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

<span data-ttu-id="b756e-271">Le code vers **DeviceResources::CreateDeviceResources pour utiliser IDXGIAdapter de mettre à jour**</span><span class="sxs-lookup"><span data-stu-id="b756e-271">Code to **update DeviceResources::CreateDeviceResources to use IDXGIAdapter**</span></span>

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

<span data-ttu-id="b756e-272">**Les graphiques hybrides et Media Foundation**</span><span class="sxs-lookup"><span data-stu-id="b756e-272">**Hybrid graphics and Media Foundation**</span></span>

<span data-ttu-id="b756e-273">À l’aide de Media Foundation sur les systèmes hybrides peut entraîner des problèmes où vidéo n’affichera ou texture vidéo est endommagé.</span><span class="sxs-lookup"><span data-stu-id="b756e-273">Using Media Foundation on hybrid systems may cause issues where video will not render or video texture is corrupt.</span></span> <span data-ttu-id="b756e-274">Cela peut se produire, car Media Foundation par défaut pour un comportement du système comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b756e-274">This can occur because Media Foundation is defaulting to a system behavior as mentioned above.</span></span> <span data-ttu-id="b756e-275">Dans certains scénarios, la création d’un ID3D11Device distinct est requis pour la prise en charge multi-threading et la création correcte indicateurs sont définis.</span><span class="sxs-lookup"><span data-stu-id="b756e-275">In some scenarios, creating a separate ID3D11Device is required to support multi-threading and the correct creation flags are set.</span></span>

<span data-ttu-id="b756e-276">Lors de l’initialisation du ID3D11Device, D3D11_CREATE_DEVICE_VIDEO_SUPPORT indicateur doit être défini dans le cadre de la D3D11_CREATE_DEVICE_FLAG.</span><span class="sxs-lookup"><span data-stu-id="b756e-276">When initializing the ID3D11Device, D3D11_CREATE_DEVICE_VIDEO_SUPPORT flag must be defined as part of the D3D11_CREATE_DEVICE_FLAG.</span></span> <span data-ttu-id="b756e-277">Une fois l’appareil et le contexte est créé, appelez <a href="https://docs.microsoft.com/windows/desktop/api/d3d10/nf-d3d10-id3d10multithread-setmultithreadprotected" target="_blank">SetMultithreadProtected</a> pour activer le multithreading.</span><span class="sxs-lookup"><span data-stu-id="b756e-277">Once the device and context is created, call <a href="https://docs.microsoft.com/windows/desktop/api/d3d10/nf-d3d10-id3d10multithread-setmultithreadprotected" target="_blank">SetMultithreadProtected</a> to enable multithreading.</span></span> <span data-ttu-id="b756e-278">Pour associer l’appareil avec le <a href="https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfdxgidevicemanager" target="_blank">IMFDXGIDeviceManager</a>, utilisez le <a href="https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-resetdevice" target="_blank">IMFDXGIDeviceManager::ResetDevice</a> (fonction).</span><span class="sxs-lookup"><span data-stu-id="b756e-278">To associate the device with the <a href="https://docs.microsoft.com/windows/desktop/api/mfobjects/nn-mfobjects-imfdxgidevicemanager" target="_blank">IMFDXGIDeviceManager</a>, use the <a href="https://docs.microsoft.com/windows/desktop/api/mfobjects/nf-mfobjects-imfdxgidevicemanager-resetdevice" target="_blank">IMFDXGIDeviceManager::ResetDevice</a> function.</span></span>

<span data-ttu-id="b756e-279">Le code vers **associer un ID3D11Device IMFDXGIDeviceManager**:</span><span class="sxs-lookup"><span data-stu-id="b756e-279">Code to **associate a ID3D11Device with IMFDXGIDeviceManager**:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="b756e-280">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b756e-280">See also</span></span>
* [<span data-ttu-id="b756e-281">Systèmes de coordonnées dans DirectX</span><span class="sxs-lookup"><span data-stu-id="b756e-281">Coordinate systems in DirectX</span></span>](coordinate-systems-in-directx.md)
* [<span data-ttu-id="b756e-282">Utilisation de l’émulateur HoloLens</span><span class="sxs-lookup"><span data-stu-id="b756e-282">Using the HoloLens emulator</span></span>](using-the-hololens-emulator.md)
