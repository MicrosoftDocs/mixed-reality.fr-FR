---
title: Appareil photo dans Unity
description: Comment utiliser la caméra principale d’Unity pour le développement de la réalité mixte Windows pour effectuer un rendu holographique
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, rendu holographique, holographique, immersif, point de focus, mémoire tampon de profondeur, orientation uniquement, positionnelle, opaque, transparent, clip
ms.openlocfilehash: 1a2e66d5c028109a58ea8682668521f50158add9
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79375586"
---
# <a name="camera-in-unity"></a>Appareil photo dans Unity

Quand vous portez un casque de réalité mixte, il devient le centre de votre monde holographique. Le composant [appareil photo](https://docs.unity3d.com/Manual/class-Camera.html) Unity gère automatiquement le rendu stéréoscopique et suit le mouvement et la rotation de votre tête lorsque l’appareil est sélectionné avec la « réalité virtuelle prise en charge » dans la section autres paramètres des paramètres du lecteur Windows Store. Cela peut être indiqué sous la forme « Windows holographique » dans les versions antérieures d’Unity.

Toutefois, pour optimiser complètement la qualité visuelle et la [stabilité des hologrammes](hologram-stability.md), vous devez définir les paramètres de l’appareil photo décrits ci-dessous.

>[!NOTE]
>Ces paramètres doivent être appliqués à l’appareil photo dans chaque scène de votre application.
>
>Par défaut, lorsque vous créez une nouvelle scène dans Unity, elle contient un GameObject d’appareil photo principal dans la hiérarchie qui comprend le composant Camera, mais les paramètres ci-dessous ne sont pas correctement appliqués.

## <a name="automatic-scene-and-camera-setup-with-mixed-reality-toolkit-v2"></a>Configuration automatique de la scène et de l’appareil photo avec Mixed Reality Toolkit v2

Suivez le guide [pas à pas](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html) pour ajouter Mixed Reality Toolkit v2 à votre projet Unity et configurez votre projet automatiquement.

Vous pouvez également configurer manuellement le projet sans MRTK avec le Guide de la section ci-dessous.

## <a name="holographic-vs-immersive-headsets"></a>Des casques holographiques et des casques immersifs

Les paramètres par défaut du composant appareil photo Unity sont destinés aux applications 3D traditionnelles qui ont besoin d’un arrière-plan skybox, car ils n’ont pas de monde réel.

* Quand vous exécutez sur un **[casque immersif](immersive-headset-hardware-details.md)** , vous affichez tout ce que l’utilisateur voit, et vous souhaiterez probablement conserver le skybox.
* Toutefois, en cas d’exécution sur un **casque holographique** comme [HoloLens](hololens-hardware-details.md), le monde réel doit apparaître derrière tout ce que l’appareil photo rend. Pour ce faire, définissez l’arrière-plan de l’appareil photo sur transparent (dans HoloLens, le rendu noir est transparent) au lieu d’une texture skybox :
    1. Sélectionner la caméra principale dans le volet de la hiérarchie
    2. Dans le panneau Inspecteur, recherchez le composant Camera et modifiez la liste déroulante Clear Flags de skybox en Color unie
    3. Sélectionnez le sélecteur de couleur d’arrière-plan et modifiez les valeurs RVBA en (0, 0, 0, 0)

Vous pouvez utiliser le code de script pour déterminer au moment de l’exécution si le casque est immersif ou holographique en vérifiant [HolographicSettings. IsDisplayOpaque](https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.IsDisplayOpaque.html).

## <a name="positioning-the-camera"></a>Positionnement de l’appareil photo

Il sera plus facile de disposer votre application si vous imaginez la position de départ de l’utilisateur comme (X : 0, Y : 0, Z : 0). Étant donné que la caméra principale effectue le suivi du mouvement de la tête de l’utilisateur, la position de départ de l’utilisateur peut être définie en définissant la position de départ de l’appareil photo principal.

1. Sélectionner la caméra principale dans le volet de la hiérarchie
2. Dans le volet de l’inspecteur, recherchez le composant transformer et remplacez la position (X : 0, Y : 1, Z :-10) par (X : 0, Y : 0, Z : 0)

   ![caméra dans le volet de l’inspecteur dans Unity](images/maincamera-350px.png)  
   *Caméra dans le volet de l’inspecteur dans Unity*

## <a name="clip-planes"></a>Plans de coupe

Le rendu du contenu trop proche de l’utilisateur peut ne pas être à l’aise avec la réalité mixte. Vous pouvez ajuster les [plans de clip proches et Far](hologram-stability.md#hologram-render-distances) sur le composant de l’appareil photo.

1. Sélectionner la caméra principale dans le volet de la hiérarchie
2. Dans le panneau Inspecteur, recherchez les plans de découpage du composant d’appareil photo et remplacez la valeur 0,3 de la zone de texte near par. 85. Le rendu du contenu est encore plus proche peut entraîner une gêne de l’utilisateur et doit être évité en fonction des [règles de distance de rendu](hologram-stability.md#hologram-render-distances).

## <a name="multiple-cameras"></a>Plusieurs caméras

Lorsqu’il existe plusieurs composants d’appareil photo dans la scène, Unity sait quelle caméra utiliser pour le rendu stéréoscopique et le suivi des têtes en vérifiant quel GameObject a la balise MainCamera.

## <a name="recentering-a-seated-experience"></a>Recentrer une expérience assise

Si vous créez une [expérience à l’échelle assise](coordinate-systems.md), vous pouvez recentrer l’origine du monde de l’unité à la position de la tête actuelle de l’utilisateur en appelant **[XR. Méthode InputTracking. recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html)** .

## <a name="reprojection-modes"></a>Modes de reprojection

Les casques HoloLens et immersif reprojeteront chaque image que votre application restituera pour s’ajuster pour une prédiction incorrecte de la position d’en-tête réelle de l’utilisateur lors de l’émission de photons.

Par défaut :

* Les **casques immersifs** effectuent une reprojection de position, en ajustant vos hologrammes pour la prédiction à la fois à la position et à l’orientation, si l’application fournit un tampon de profondeur pour un frame donné.  Si aucune mémoire tampon de profondeur n’est fournie, le système corrigera uniquement les prédictions incorrectes dans l’orientation.
* Les **casques holographiques** comme HoloLens effectuent une reprojection de position, que l’application fournisse ou non sa mémoire tampon de profondeur.  La reprojection positionnel est possible sans tampons de profondeur sur HoloLens, car le rendu est souvent épars avec un arrière-plan stable fourni par le monde réel.

Si vous savez que vous créez une [expérience d’orientation uniquement](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience) avec du contenu verrouillé de manière rigide (par exemple, du contenu vidéo de 360 degrés), vous pouvez définir explicitement le mode de reprojection sur la valeur orientation uniquement en définissant [HolographicSettings. ReprojectionMode](https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.ReprojectionMode.html) sur [HolographicReprojectionMode. OrientationOnly](https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.HolographicReprojectionMode.html).

## <a name="sharing-your-depth-buffers-with-windows"></a>Partage de vos mémoires tampons de profondeur avec Windows

En partageant le tampon de profondeur de votre application sur Windows, chaque trame donne à votre application l’un des deux boosters de stabilité de l’hologramme, en fonction du type de casque pour lequel vous effectuez le rendu :

* Les **casques immersifs** peuvent effectuer une reprojection de position lorsqu’une mémoire tampon de profondeur est fournie, en ajustant vos hologrammes pour la prédiction à la fois à la position et à l’orientation.
* Les **casques holographiques** présentent différentes méthodes. HoloLens 1 sélectionne automatiquement un [point de focus](focus-point-in-unity.md) lorsqu’une mémoire tampon de profondeur est fournie, ce qui optimise la stabilité de l’hologramme le long du plan qui croise la plus grande partie du contenu. HoloLens 2 va stabiliser le contenu à l’aide [de Depth LSR (consultez la section Notes)](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.setfocuspoint).

Pour définir si votre application Unity fournira un tampon de profondeur à Windows :

1. Accédez à **modifier** > **paramètres du projet** > **lecteur** > **onglet plateforme Windows universelle** > **paramètres XR**.
2. Développez l’élément du **Kit de développement logiciel (SDK) Windows Mixed Reality** .
3. Activez ou désactivez la case à cocher **activer le partage de tampons de profondeur** .  Cette option est activée par défaut dans les nouveaux projets créés, car cette fonctionnalité a été ajoutée à Unity et elle est désactivée par défaut pour les projets plus anciens qui ont été mis à niveau.

En fournissant une mémoire tampon de profondeur à Windows, vous pouvez améliorer la qualité visuelle tant que Windows peut mapper avec précision les valeurs de profondeur par pixel normalisées dans votre tampon de profondeur à des distances exprimées en mètres, à l’aide des plans proches et Far que vous avez définis dans Unity sur la caméra principale.  Si votre rendu passe les valeurs de profondeur des poignées de manière classique, vous devez généralement être précis ici, bien que le rendu translucide passe l’écriture dans le tampon de profondeur pendant que l’affichage aux pixels de couleur existants peut confondre la reprojection.  Si vous savez que vos passes de rendu conservent un grand nombre de pixels de profondeur finale avec des valeurs de profondeur inexactes, vous obtiendrez probablement une meilleure qualité visuelle en désactivant l’option « Activer le partage de mémoire tampon de profondeur ».

## <a name="see-also"></a>Voir aussi

* [Stabilité des hologrammes](hologram-stability.md)
* [MixedRealityToolkit main Camera. Prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input/Prefabs)
