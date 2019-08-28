---
title: Suivi du code QR
description: Découvrez comment détecter les codes QR sur HoloLens 2.
author: dorreneb
ms.author: dobrown
ms.date: 05/15/2019
ms.topic: article
keywords: VR, LBE, divertissement basé sur l’emplacement, VR arcade, arcade, immersif, QR, code QR, hololens2
ms.openlocfilehash: 736ab265db2145dd784c435e525059ed3a2fcbbb
ms.sourcegitcommit: 3b32339c5d5c79eaecd84ed27254a8f4321731f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70047165"
---
# <a name="qr-code-tracking"></a><span data-ttu-id="3675e-104">Suivi du code QR</span><span class="sxs-lookup"><span data-stu-id="3675e-104">QR code tracking</span></span>

<span data-ttu-id="3675e-105">HoloLens 2 peut détecter les codes QR dans l’environnement autour du casque, en établissant un système de coordonnées à l’emplacement réel de chaque code.</span><span class="sxs-lookup"><span data-stu-id="3675e-105">HoloLens 2 can detect QR codes in the environment around the headset, establishing a coordinate system at each code's real-world location.</span></span>

## <a name="device-support"></a><span data-ttu-id="3675e-106">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="3675e-106">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="3675e-107">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="3675e-107">Feature</span></span></th><th style="width:150px"> <span data-ttu-id="3675e-108"><a href="hololens-hardware-details.md">HoloLens (1ère génération)</a></span><span class="sxs-lookup"><span data-stu-id="3675e-108"><a href="hololens-hardware-details.md">HoloLens (1st gen)</a></span></span></th><th style="width:150px"><span data-ttu-id="3675e-109">HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="3675e-109">HoloLens 2</span></span></th><th style="width:150px"> <span data-ttu-id="3675e-110"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="3675e-110"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="3675e-111">Détection du code QR</span><span class="sxs-lookup"><span data-stu-id="3675e-111">QR code detection</span></span></td><td style="text-align: center;"><span data-ttu-id="3675e-112">️</span><span class="sxs-lookup"><span data-stu-id="3675e-112">️</span></span></td><td style="text-align: center;"> <span data-ttu-id="3675e-113">✔️</span><span class="sxs-lookup"><span data-stu-id="3675e-113">✔️</span></span></td><td style="text-align: center;"><span data-ttu-id="3675e-114">Voir la remarque</span><span class="sxs-lookup"><span data-stu-id="3675e-114">See note</span></span></td>
</tr>
</table>

>[!NOTE]
><span data-ttu-id="3675e-115">La prise en charge des casques Windows mixtes immersif sur les PC de bureau n’est actuellement pas prise en charge avec le package NuGet ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3675e-115">Support for immersive Windows Mixed Reality headsets on desktop PCs is not currently supported with the NuGet package below.</span></span>  <span data-ttu-id="3675e-116">Restez informé pour obtenir des mises à jour supplémentaires sur le support des postes de travail.</span><span class="sxs-lookup"><span data-stu-id="3675e-116">Stay tuned for further updates on desktop support.</span></span>

## <a name="getting-the-qr-package"></a><span data-ttu-id="3675e-117">Obtention du package QR</span><span class="sxs-lookup"><span data-stu-id="3675e-117">Getting the QR package</span></span>
<span data-ttu-id="3675e-118">Vous pouvez télécharger un package NuGet pour la détection du code QR [ici](https://github.com/dorreneb/mixed-reality/releases).</span><span class="sxs-lookup"><span data-stu-id="3675e-118">You can download a NuGet package for QR code detection [here](https://github.com/dorreneb/mixed-reality/releases).</span></span>

<span data-ttu-id="3675e-119">Les versions ultérieures de ce package seront disponibles via le référentiel de packages NuGet public.</span><span class="sxs-lookup"><span data-stu-id="3675e-119">Future versions of this package will be available through the public NuGet package repository.</span></span>

## <a name="detecting-qr-codes"></a><span data-ttu-id="3675e-120">Détection des codes QR</span><span class="sxs-lookup"><span data-stu-id="3675e-120">Detecting QR codes</span></span>

### <a name="adding-the-webcam-capability"></a><span data-ttu-id="3675e-121">Ajout de la fonctionnalité webcam</span><span class="sxs-lookup"><span data-stu-id="3675e-121">Adding the webcam capability</span></span>
<span data-ttu-id="3675e-122">Vous devrez ajouter la fonctionnalité `webcam` à votre manifeste pour détecter les codes QR.</span><span class="sxs-lookup"><span data-stu-id="3675e-122">You will need to add the capability `webcam` to your manifest to detect QR codes.</span></span> <span data-ttu-id="3675e-123">Cette fonctionnalité est requise, car les données dans les codes détectés dans l’environnement de l’utilisateur peuvent contenir des informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="3675e-123">This capability is required as the data within detected codes in the user's environment may contain sensitive information.</span></span>

<span data-ttu-id="3675e-124">L’autorisation peut être demandée en `QRCodeWatcher.RequestAccessAsync()`appelant:</span><span class="sxs-lookup"><span data-stu-id="3675e-124">Permission can be requested by calling `QRCodeWatcher.RequestAccessAsync()`:</span></span>

<span data-ttu-id="3675e-125">_C#:_</span><span class="sxs-lookup"><span data-stu-id="3675e-125">_C#:_</span></span>
```cs
await QRCodeWatcher.RequestAccessAsync();
```

<span data-ttu-id="3675e-126">_C++:_</span><span class="sxs-lookup"><span data-stu-id="3675e-126">_C++:_</span></span>
```cpp
co_await QRCodeWatcher.RequestAccessAsync();
```

<span data-ttu-id="3675e-127">L’autorisation doit être demandée avant la construction d’un objet QRCodeWatcher.</span><span class="sxs-lookup"><span data-stu-id="3675e-127">Permission should be requested before you construct a QRCodeWatcher object.</span></span>

<span data-ttu-id="3675e-128">Si la détection du code QR `webcam` requiert la fonctionnalité, la détection se produit à l’aide des caméras de suivi de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3675e-128">While QR code detection requires the `webcam` capability, the detection occurs using the device's tracking cameras.</span></span> <span data-ttu-id="3675e-129">Cela fournit un angle de détection plus vaste et une plus grande autonomie de batterie par rapport à la détection avec l’appareil photo/vidéo (PV) de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="3675e-129">This provides a wider detection FOV and better battery life compared to detection with the device's photo/video (PV) camera.</span></span>

### <a name="detecting-qr-codes-in-unity"></a><span data-ttu-id="3675e-130">Détection des codes QR dans Unity</span><span class="sxs-lookup"><span data-stu-id="3675e-130">Detecting QR codes in Unity</span></span>

<span data-ttu-id="3675e-131">Vous pouvez utiliser l’API de détection du code QR dans Unity sans dépendre de MRTK.</span><span class="sxs-lookup"><span data-stu-id="3675e-131">You can use the QR code detection API in Unity without taking a dependency on MRTK.</span></span> <span data-ttu-id="3675e-132">Pour ce faire, vous devez effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="3675e-132">To do so, you must:</span></span>

1. <span data-ttu-id="3675e-133">Créez un nouveau dossier dans le dossier composants de votre projet Unity avec le nom *plugins*.</span><span class="sxs-lookup"><span data-stu-id="3675e-133">Create a new folder in the assets folder of your unity project with the name *Plugins*.</span></span>
2. <span data-ttu-id="3675e-134">Copiez tous les fichiers requis à partir de ce dossier dans le dossier «Plug-ins» local que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="3675e-134">Copy all the required files from this folder into the local "Plugins" folder you just created.</span></span>

<span data-ttu-id="3675e-135">Il existe un exemple d’application Unity qui affiche un carré holographique sur les codes QR, ainsi que les données associées telles que le GUID, la taille physique, l’horodatage et les données décodées.</span><span class="sxs-lookup"><span data-stu-id="3675e-135">There is a sample Unity app that displays a holographic square over QR codes, along with the associated data such as GUID, physical size, timestamp, and decoded data.</span></span> <span data-ttu-id="3675e-136">Cette application peut se trouver à https://github.com/chgatla-microsoft/QRTracking/tree/master/SampleQRCodes l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="3675e-136">This app can be located at https://github.com/chgatla-microsoft/QRTracking/tree/master/SampleQRCodes.</span></span>

### <a name="detecting-qr-codes-in-c"></a><span data-ttu-id="3675e-137">Détection des codes QR dansC++</span><span class="sxs-lookup"><span data-stu-id="3675e-137">Detecting QR codes in C++</span></span>

>[!NOTE]
><span data-ttu-id="3675e-138">Les C++ extraits de code de cet article illustrent actuellement l’utilisation C++de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="3675e-138">The C++ code snippets in this article currently demonstrate the use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span> <span data-ttu-id="3675e-139">Les concepts sont équivalents pour C++un projet/WinRT, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="3675e-139">The concepts are equivalent for a C++/WinRT project, though you need to translate the code.</span></span>

```
using namespace Microsoft.MixedReality.QR;

    public ref class QRListHelper sealed
    {
    public:
        QRListHelper()
        {

        }

        void setApp(SpatialStageManager* pStage)
        {
            m_pStage = pStage;
        }

        void SetUpQRCodes()
        {
            if (QRCodeWatcher::IsSupported())
            {
                auto operation = QRCodeWatcher::RequestAccessAsync();

                WeakReference weakThis(this);

                operation->Completed = ref new AsyncOperationCompletedHandler<QRCodeWatcherAccessStatus>(
                    [weakThis](IAsyncOperation< QRCodeWatcherAccessStatus>^ operaion, AsyncStatus status)
                {
                    QRListHelper^ QRListHelper = weakThis.Resolve<QRListHelper>();
                    if (status == AsyncStatus::Completed)
                    {
                        QRListHelper->InitializeQR( operaion->GetResults());
                    }
                }
                );
            }
        }

    private:
        void OnAddedQRCode(Object^, QRCodeAddedEventArgs ^args)
        {
            m_pStage->OnAddedQRCode(args);
        }
        void OnUpdatedQRCode(Object^, QRCodeUpdatedEventArgs ^args)
        {
            m_pStage->OnUpdatedQRCode(args);
        }
        void OnEnumerationComplete(Object^, Object^)
        {
            m_pStage->OnEnumerationComplete();
        }

        SpatialStageManager* m_pStage;
        QRCodeWatcher^ m_qrWatcher;



        void InitializeQR(QRCodeWatcherAccessStatus status)
        {
            if (status == QRCodeWatcherAccessStatus::Allowed)
            {
                m_qrWatcher = ref new QRCodeWatcher();

                m_qrWatcher->Added += ref new EventHandler<Object^, QRCodeAddedEventArgs^>(this, &QRListHelper::OnAddedQRCode);
                m_qrWatcher->Updated += ref new EventHandler<Object^, QRCodeUpdatedEventArgs^>(this, &QRListHelper::OnUpdatedQRCode);
                m_qrWatcher->EnumerationCompleted += ref new EventHandler<Object^, Object^>(this, &QRListHelper::OnEnumerationComplete);
                try
                {
                    m_qrWatcher->Start();
                }
                catch (...)
                {

                }
            }
            else
            {
                // Permission denied by system or user
                // Handle the failures
            }
        }
    }; 
```

## <a name="getting-the-coordinate-system-for-a-qr-code"></a><span data-ttu-id="3675e-140">Obtention du système de coordonnées pour un code QR</span><span class="sxs-lookup"><span data-stu-id="3675e-140">Getting the coordinate system for a QR code</span></span>

<span data-ttu-id="3675e-141">Chaque code QR détecté expose un [système de coordonnées spatiales](coordinate-systems.md) aligné avec le code QR dans le coin supérieur gauche du carré détection rapide dans le coin supérieur gauche, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3675e-141">Each detected QR code exposes a [spatial coordinate system](coordinate-systems.md) aligned with the QR code at the top left corner of the fast detection square in the top left as seen below.</span></span>  <span data-ttu-id="3675e-142">Lorsque vous utilisez directement le kit de développement logiciel (SDK) QR, l’axe Z pointe sur le papier (non affiché)-en cas de conversion en coordonnées Unity, l’axe Z pointe hors du papier et est droitier.</span><span class="sxs-lookup"><span data-stu-id="3675e-142">When directly using the QR SDK, the Z-axis is pointing into the paper (not shown) - when converted into Unity coordinates, the Z-axis points out of the paper and is left-handed.</span></span>

<span data-ttu-id="3675e-143">L’alignement du SpatialCoordinateSystem d’un code QR est indiqué.</span><span class="sxs-lookup"><span data-stu-id="3675e-143">A QR code's SpatialCoordinateSystem aligns shown.</span></span> <span data-ttu-id="3675e-144">Ce système de coordonnées peut être obtenu à partir de la plateforme en appelant <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.createcoordinatesystemfornode" target="_blank">SpatialGraphInteropPreview:: CreateCoordinateSystemForNode</a> et en passant le SpatialGraphNodeId du code.</span><span class="sxs-lookup"><span data-stu-id="3675e-144">This coordinate system can be obtained from the platform by calling <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.preview.spatialgraphinteroppreview.createcoordinatesystemfornode" target="_blank">SpatialGraphInteropPreview::CreateCoordinateSystemForNode</a> and passing in the code's SpatialGraphNodeId.</span></span>

![Système de coordonnées du code QR](images/Qr-coordinatesystem.png) 

<span data-ttu-id="3675e-146">Pour un objet QRCode, le code C++/CX suivant montre comment créer un rectangle et le placer à l’aide du système de coordonnées du code QR:</span><span class="sxs-lookup"><span data-stu-id="3675e-146">For a QRCode object, the following C++/CX code shows how to create a rectangle and place it using the QR code's coordinate system:</span></span>

```cpp
// Creates a 2D rectangle in the x-y plane, with the specified properties.
std::vector<float3> SpatialStageManager::CreateRectangle(float width, float height)
{
    std::vector<float3> vertices(4);

    vertices[0] = { 0, 0, 0 };
    vertices[1] = { width, 0, 0 };
    vertices[2] = { width, height, 0 };
    vertices[3] = { 0, height, 0 };

    return vertices;
}
```

<span data-ttu-id="3675e-147">Vous pouvez utiliser la taille physique pour créer le rectangle QR:</span><span class="sxs-lookup"><span data-stu-id="3675e-147">You can use the physical size to create the QR rectangle:</span></span>

```cpp
std::vector<float3> qrVertices = CreateRectangle(Code->PhysicalSizeMeters, Code->PhysicalSizeMeters); 
```

<span data-ttu-id="3675e-148">Le système de coordonnées peut être utilisé pour dessiner le code QR ou pour attacher des hologrammes à l’emplacement:</span><span class="sxs-lookup"><span data-stu-id="3675e-148">The coordinate system can be used to draw the QR code or attach holograms to the location:</span></span>

```cpp
Windows::Perception::Spatial::SpatialCoordinateSystem^ qrCoordinateSystem = Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode(Code->SpatialGraphNodeId);
```

<span data-ttu-id="3675e-149">De même, votre *QRCodeWatcher:: QRCodeAddedHandler* peut se présenter comme suit:</span><span class="sxs-lookup"><span data-stu-id="3675e-149">Altogether, your *QRCodeWatcher::QRCodeAddedHandler* may look something like this:</span></span>

```cpp
void MyClass::OnAddedQRCode(Object ^sender, QRCodeWatcher::QRCodeAddedEventArgs ^args)
{
    std::vector<float3> qrVertices = CreateRectangle(args->Code->PhysicalSizeMeters, args->Code->PhysicalSizeMeters);
    std::vector<unsigned short> qrCodeIndices = TriangulatePoints(qrVertices);
    XMFLOAT3 qrAreaColor = XMFLOAT3(DirectX::Colors::Aqua);

    Windows::Perception::Spatial::SpatialCoordinateSystem^ qrCoordinateSystem =  Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode(args->Code->SpatialGraphNodeId);
    std::shared_ptr<SceneObject> m_qrShape =
        std::make_shared<SceneObject>(
            m_deviceResources,
            reinterpret_cast<std::vector<XMFLOAT3>&>(qrVertices),
            qrCodeIndices,
            qrAreaColor,
            qrCoordinateSystem);

    m_sceneController->AddSceneObject(m_qrShape);
}
```

## <a name="best-practices-for-qr-code-detection"></a><span data-ttu-id="3675e-150">Meilleures pratiques pour la détection du code QR</span><span class="sxs-lookup"><span data-stu-id="3675e-150">Best practices for QR code detection</span></span>

### <a name="quiet-zones-around-qr-codes"></a><span data-ttu-id="3675e-151">Zones calmes autour des codes QR</span><span class="sxs-lookup"><span data-stu-id="3675e-151">Quiet zones around QR Codes</span></span>

<span data-ttu-id="3675e-152">Pour être lu correctement, les codes QR nécessitent une marge autour de tous les côtés du code.</span><span class="sxs-lookup"><span data-stu-id="3675e-152">To be read correctly, QR codes require a margin around all sides of the code.</span></span> <span data-ttu-id="3675e-153">Cette marge ne doit pas contenir de contenu imprimé et doit être de quatre modules (un carré noir unique dans le code).</span><span class="sxs-lookup"><span data-stu-id="3675e-153">This margin must not contain any printed content and should be four modules (a single black square in the code) wide.</span></span> 

<span data-ttu-id="3675e-154">La [spécification QR](https://www.qrcode.com/en/howto/code.html) contient plus d’informations sur les zones silencieuses.</span><span class="sxs-lookup"><span data-stu-id="3675e-154">The [QR spec](https://www.qrcode.com/en/howto/code.html) contains more information about quiet zones.</span></span>

### <a name="lighting-and-backdrop"></a><span data-ttu-id="3675e-155">Éclairage et fond</span><span class="sxs-lookup"><span data-stu-id="3675e-155">Lighting and backdrop</span></span>
<span data-ttu-id="3675e-156">La qualité de la détection du code QR est susceptible de varier l’éclairage et le fond.</span><span class="sxs-lookup"><span data-stu-id="3675e-156">QR code detection quality is susceptible to varying illumination and backdrop.</span></span> 

<span data-ttu-id="3675e-157">Dans une scène avec un éclairage particulièrement clair, imprimez un code noir sur un arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="3675e-157">In a scene with particularly bright lighting, print a code that is black on a gray background.</span></span> <span data-ttu-id="3675e-158">Sinon, imprimez un code QR noir sur un arrière-plan blanc.</span><span class="sxs-lookup"><span data-stu-id="3675e-158">Otherwise, print a black QR code on a white background.</span></span>

<span data-ttu-id="3675e-159">Si le fond du code est particulièrement sombre, essayez un code noir en gris si votre taux de détection est faible.</span><span class="sxs-lookup"><span data-stu-id="3675e-159">If the backdrop to the code is particularly dark, try a black on gray code if your detection rate is low.</span></span> <span data-ttu-id="3675e-160">Si le fond est relativement clair, un code normal devrait fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="3675e-160">If the backdrop is relatively light, a regular code should work fine.</span></span>

### <a name="size-of-qr-codes"></a><span data-ttu-id="3675e-161">Taille des codes QR</span><span class="sxs-lookup"><span data-stu-id="3675e-161">Size of QR codes</span></span>
<span data-ttu-id="3675e-162">Les appareils Windows Mixed Reality ne fonctionnent pas avec les codes QR avec des côtés inférieurs à 5 cm chacun.</span><span class="sxs-lookup"><span data-stu-id="3675e-162">Windows Mixed Reality devices do not work with QR codes with sides smaller than 5 cm each.</span></span>

<span data-ttu-id="3675e-163">Pour les codes QR d’une longueur comprise entre 5 et 10 cm, vous devez être assez proche pour détecter le code.</span><span class="sxs-lookup"><span data-stu-id="3675e-163">For QR codes between 5 and 10 cm length sides, you must be fairly close to detect the code.</span></span> <span data-ttu-id="3675e-164">La détection des codes à cette taille prendra également plus de temps.</span><span class="sxs-lookup"><span data-stu-id="3675e-164">It will also take longer to detect codes at this size.</span></span> 

<span data-ttu-id="3675e-165">La durée exacte de la détection des codes dépend non seulement de la taille des codes QR, mais aussi de la portée du code.</span><span class="sxs-lookup"><span data-stu-id="3675e-165">The exact time to detect codes depends not only on the size of the QR codes, but how far you are away from the code.</span></span> <span data-ttu-id="3675e-166">Le déplacement plus proche du code aidera à décaler les problèmes de taille.</span><span class="sxs-lookup"><span data-stu-id="3675e-166">Moving closer to the code will help offset issues with size.</span></span>

### <a name="distance-and-angular-position-from-the-qr-code"></a><span data-ttu-id="3675e-167">Distance et position angulaire à partir du code QR</span><span class="sxs-lookup"><span data-stu-id="3675e-167">Distance and angular position from the QR code</span></span>
<span data-ttu-id="3675e-168">Les caméras de suivi peuvent uniquement détecter un certain niveau de détail.</span><span class="sxs-lookup"><span data-stu-id="3675e-168">The tracking cameras can only detect a certain level of detail.</span></span> <span data-ttu-id="3675e-169">Pour les codes très petits-< 10cm sur les côtés, vous devez être assez proche.</span><span class="sxs-lookup"><span data-stu-id="3675e-169">For really small codes - < 10cm along the sides - you must be fairly close.</span></span> <span data-ttu-id="3675e-170">Pour un code QR de version 1 variant de 10 à 25 cm de large, la distance de détection minimale est comprise entre 0,15 mètres et 0,5 mètres.</span><span class="sxs-lookup"><span data-stu-id="3675e-170">For a version 1 QR code varying from 10 to 25 cm wide, the minimum detection distance ranges from 0.15 meters to 0.5 meters.</span></span> 

<span data-ttu-id="3675e-171">La distance de détection pour la taille augmente de façon linéaire.</span><span class="sxs-lookup"><span data-stu-id="3675e-171">The detection distance for size increases linearly.</span></span> 

<span data-ttu-id="3675e-172">La détection QR fonctionne avec une plage d’angles + = 45deg.</span><span class="sxs-lookup"><span data-stu-id="3675e-172">QR detection works with a range of angles += 45deg.</span></span> <span data-ttu-id="3675e-173">Cela permet de garantir une résolution correcte de la détection du code.</span><span class="sxs-lookup"><span data-stu-id="3675e-173">This is to ensure we have proper resolution to detect the code.</span></span>

### <a name="qr-codes-with-logos"></a><span data-ttu-id="3675e-174">Codes QR avec logos</span><span class="sxs-lookup"><span data-stu-id="3675e-174">QR codes with logos</span></span>
<span data-ttu-id="3675e-175">Les codes QR avec des logos n’ont pas été testés et ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3675e-175">QR codes with logos have not been tested and are currently unsupported.</span></span>

### <a name="managing-qr-code-data"></a><span data-ttu-id="3675e-176">Gestion des données de code QR</span><span class="sxs-lookup"><span data-stu-id="3675e-176">Managing QR code data</span></span>
<span data-ttu-id="3675e-177">Les appareils Windows Mixed Reality détectent les codes QR au niveau du système dans le pilote.</span><span class="sxs-lookup"><span data-stu-id="3675e-177">Windows Mixed Reality devices detect QR codes at the system level in the driver.</span></span> <span data-ttu-id="3675e-178">Lorsque l’appareil est redémarré, les codes QR détectés ont disparu et sont à nouveau détectés en tant que nouveaux objets la prochaine fois.</span><span class="sxs-lookup"><span data-stu-id="3675e-178">When the device is rebooted, the detected QR codes are gone and will be re-detected as new objects next time.</span></span>

<span data-ttu-id="3675e-179">Il est recommandé de configurer votre application pour qu’elle ignore les codes QR antérieurs à un horodateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="3675e-179">It is recommended to configure your app to ignore QR codes older than a specific timestamp.</span></span> <span data-ttu-id="3675e-180">Actuellement, l’API ne prend pas en charge l’effacement de l’historique du code QR.</span><span class="sxs-lookup"><span data-stu-id="3675e-180">Currently, the API does not support clearing QR code history.</span></span>

### <a name="qr-code-placement-in-a-space"></a><span data-ttu-id="3675e-181">Positionnement du code QR dans un espace</span><span class="sxs-lookup"><span data-stu-id="3675e-181">QR code placement in a space</span></span>
<span data-ttu-id="3675e-182">Pour obtenir des recommandations sur l’emplacement et le positionnement des codes QR, reportez-vous à [considérations relatives à l’environnement pour HoloLens](environment-considerations-for-hololens.md).</span><span class="sxs-lookup"><span data-stu-id="3675e-182">For recommendations on where and how to place QR codes, please refer to [Environment considerations for HoloLens](environment-considerations-for-hololens.md).</span></span>

## <a name="qr-api-reference"></a><span data-ttu-id="3675e-183">Informations de référence sur l’API QR</span><span class="sxs-lookup"><span data-stu-id="3675e-183">QR API reference</span></span>

```cs
namespace Microsoft.MixedReality.QR
{
    /// <summary>
    /// Represents a detected QR code.
    /// </remarks>
    public class QRCode
    {
        /// <summary>
        /// Unique id that identifies this QR code for this session.
        /// </summary>
        public Guid Id { get; }

        /// <summary>
        /// Spatial graph node id for this QR code to create a coordinate system.
        /// </summary>
        public Guid SpatialGraphNodeId { get; }

        /// <summary>
        /// Version of this QR code. Version 1-40 are regular QR codes and 41-44 are Micro QR code formats 1-4.
        /// </summary>
        public VersionInfo Version { get; }

        /// <summary>
        /// Physical width and height of this QR code in meters.
        /// </summary>
        public float PhysicalSideLength { get; }

        /// <summary>
        /// Decoded QR code data.
        /// </summary>
        public String Data { get; }

        /// <summary>
        /// Size of the RawData of this QR code.
        /// </summary>
        public UInt32 RawDataSize { get; }

        /// <summary>
        /// Gets the error-corrected raw data bytes.
        /// Used when the platform is unable to decode the code's format,
        /// allowing your app to decode as needed.
        /// </summary>
        public void GetRawData(byte[] buffer);

        /// <summary>
        /// The last detected time in 100ns QPC ticks.
        /// </summary>
        public System.TimeSpan SystemRelativeLastDetectedTime { get; }

        /// <summary>
        /// The last detected time.
        /// </summary>
        public System.DateTimeOffset LastDetectedTime { get; }
    }

    /// <summary>
    /// Event arguments for a QRCodeWatcher's Added event.
    /// </summary>
    public class QRCodeAddedEventArgs
    {
        /// <summary>
        /// Gets the QR Code that was added
        /// </summary>
        public QRCode Code { get; }
    }

    /// <summary>
    /// Event arguments for a QRCodeWatcher's Removed event.
    /// </summary>
    public class QRCodeRemovedEventArgs
    {
        /// <summary>
        /// Gets the QR Code that was removed.
        /// </summary>
        public QRCode Code { get; }
    }

    /// <summary>
    /// Event arguments for a QRCodeWatcher's Updated event.
    /// </summary>
    public class QRCodeUpdatedEventArgs
    {
        /// <summary>
        /// Gets the QR Code that was updated.
        /// </summary>
        public QRCode Code { get; }
    }

    /// <summary>
    /// Represents the status of an access request for QR code detection.
    /// </summary>
    public enum QRCodeWatcherAccessStatus
    {
        /// <summary>
        /// The system has denied permission for the app to detect QR codes.
        /// </summary>
        DeniedBySystem = 0,
        /// <summary>
        /// The app has not declared the webcam capability in its manifest.
        /// </summary>
        NotDeclaredByApp = 1,
        /// <summary>
        /// The user has denied permission for the app to detect QR codes.
        /// </summary>
        DeniedByUser = 2,
        /// <summary>
        /// A user prompt is required to get permission to detect QR codes.
        /// </summary>
        UserPromptRequired = 3,
        /// <summary>
        /// The user has given permission to detect QR codes.
        /// </summary>
        Allowed = 4,
    }

    /// <summary>
    /// Detects QR codes in the user's environment.
    /// </summary>
    public class QRCodeWatcher
    {
        /// <summary>
        /// Gets whether QR code detection is supported on the current device.
        /// </summary>
        public static bool IsSupported();

        /// <summary>
        /// Request user consent before using QR code detection.
        /// </summary>
        public static IAsyncOperation<QRCodeWatcherAccessStatus> RequestAccessAsync();

        /// <summary>
        /// Constructs a new QRCodeWatcher.
        /// </summary>
        public QRCodeWatcher();

        /// <summary>
        /// Starts detecting QR codes.
        /// </summary>
        /// <remarks>
        /// Start should only be called once RequestAccessAsync has succeeded.
        /// Start should not be called if QR code detection is not supported.
        /// Check that IsSupported returns true before calling Start.
        /// </remarks>
        public void Start();

        /// <summary>
        /// Stops detecting QR codes.
        /// </summary>
        public void Stop();

        /// <summary>
        /// Get the list of QR codes detected.
        /// </summary>
        /// <remarks>
        /// </remarks>
        public IList<QRCode> GetList();

        /// <summary>
        /// Event representing the addition of a QR Code.
        /// </summary>
        public event EventHandler<QRCodeAddedEventArgs> Added;

        /// <summary>
        /// Event representing the removal of a QR Code.
        /// </summary>
        public event EventHandler<QRCodeRemovedEventArgs> Removed;

        /// <summary>
        /// Event representing the update of a QR Code.
        /// </summary>
        public event EventHandler<QRCodeUpdatedEventArgs> Updated;

        /// <summary>
        /// Event representing the enumeration of QR Codes completing after a Start call.
        /// </summary>
        public event EventHandler<Object> EnumerationCompleted;
    }

    /// <summary>
    /// Version info for QR codes, including Micro QR codes.
    /// </summary>
    public enum VersionInfo
    {
        QR1 = 1,
        QR2 = 2,
        QR3 = 3,
        QR4 = 4,
        QR5 = 5,
        QR6 = 6,
        QR7 = 7,
        QR8 = 8,
        QR9 = 9,
        QR10 = 10,
        QR11 = 11,
        QR12 = 12,
        QR13 = 13,
        QR14 = 14,
        QR15 = 15,
        QR16 = 16,
        QR17 = 17,
        QR18 = 18,
        QR19 = 19,
        QR20 = 20,
        QR21 = 21,
        QR22 = 22,
        QR23 = 23,
        QR24 = 24,
        QR25 = 25,
        QR26 = 26,
        QR27 = 27,
        QR28 = 28,
        QR29 = 29,
        QR30 = 30,
        QR31 = 31,
        QR32 = 32,
        QR33 = 33,
        QR34 = 34,
        QR35 = 35,
        QR36 = 36,
        QR37 = 37,
        QR38 = 38,
        QR39 = 39,
        QR40 = 40,
        MicroQRM1 = 41,
        MicroQRM2 = 42,
        MicroQRM3 = 43,
        MicroQRM4 = 44,
    }
}
```

## <a name="see-also"></a><span data-ttu-id="3675e-184">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3675e-184">See also</span></span>
* [<span data-ttu-id="3675e-185">Systèmes de coordonnées</span><span class="sxs-lookup"><span data-stu-id="3675e-185">Coordinate systems</span></span>](coordinate-systems.md)
* <span data-ttu-id="3675e-186"><a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a></span><span class="sxs-lookup"><span data-stu-id="3675e-186"><a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a></span></span>