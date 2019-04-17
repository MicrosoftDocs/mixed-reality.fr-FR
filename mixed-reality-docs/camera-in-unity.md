---
title: Appareil photo dans Unity
description: Comment utiliser le développement de Main Camera pour Windows Mixed Reality d’Unity pour effectuer le rendu HOLOGRAPHIQUE
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, rendu HOLOGRAPHIQUE, point de focus holographique et immersive, mémoire tampon de profondeur, orientation uniquement, positionnel, opaque et transparent, élément
ms.openlocfilehash: 8ea5a1f53351faab1b2863a0afac74e958b4b1a0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593338"
---
# <a name="camera-in-unity"></a>Appareil photo dans Unity

Lorsque vous porter un casque de réalité mixte, il devient le centre de votre monde HOLOGRAPHIQUE. L’Unity [caméra](http://docs.unity3d.com/Manual/class-Camera.html) composant gérera automatiquement rendu stéréoscopique et suivent le mouvement de la tête et de rotation lorsque votre projet a « Virtuel réalité pris en charge » sélectionné avec « Windows Mixed Reality » en tant que l’appareil (dans la section autres paramètres les paramètres du lecteur Windows Store). Cela peut être répertorié en tant que « Windows HOLOGRAPHIQUE » dans les versions antérieures de Unity.

Toutefois, pour optimiser complètement qualité visuelle et [la stabilité hologramme](hologram-stability.md), vous devez définir les paramètres de la caméra décrites ci-dessous.

>[!NOTE]
>Ces paramètres doivent être appliquées à l’appareil photo dans chaque scène de votre application.
>
>Par défaut, lorsque vous créez une nouvelle scène dans Unity, il contiendra un GameObject de caméra principale dans la hiérarchie qui inclut le composant de l’appareil photo, mais n’a pas les paramètres ci-dessous correctement appliquées.

## <a name="holographic-vs-immersive-headsets"></a>Holographique et des casques IMMERSIFS

Les paramètres par défaut sur le composant de l’appareil photo Unity sont pour les applications 3D traditionnelles nécessitant un arrière-plan de type skybox qu’ils n’ont pas un monde réel.
* Lors de l’exécution un  **[casque immersif](immersive-headset-hardware-details.md)**, rendu tout ce que voit l’utilisateur et par conséquent, vous souhaiterez probablement garder le skybox.
* Toutefois, lors de l’exécution un **casque HOLOGRAPHIQUE** comme [HoloLens](hololens-hardware-details.md), le monde réel doit apparaître tout ce que l’appareil photo rendus. Pour ce faire, définir l’arrière-plan de l’appareil photo d’être transparents (dans HoloLens, devient noir transparent) au lieu d’une texture Skybox :
    1. Sélectionnez la caméra principale dans le volet de hiérarchie
    2. Dans le panneau d’inspecteur, de trouver le composant de l’appareil photo et modifiez la liste déroulante d’effacer les indicateurs Skybox par couleur unie
    3. Sélectionnez le sélecteur de couleurs d’arrière-plan et de modifier les valeurs RGBA (0, 0, 0, 0)

Vous pouvez utiliser le code de script pour déterminer, lors de l’exécution, si le casque est immersives ou HOLOGRAPHIQUE en vérifiant [HolographicSettings.IsDisplayOpaque](https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.IsDisplayOpaque.html).


## <a name="positioning-the-camera"></a>Positionnement de l’appareil photo

Il sera plus facile de créer votre application si vous imaginez la position de départ de l’utilisateur en tant que (x :) 0, Y : 0, Z : 0). Étant donné que la caméra principale effectue le suivi des mouvements de tête de l’utilisateur, vous pouvez définir la position de départ de l’utilisateur en définissant la position de départ de la caméra principale.
1. Sélectionnez Main Camera dans le volet de hiérarchie
2. Dans le panneau d’inspecteur, de trouver le composant de transformation et modifier la Position à partir de (x :) 0, Y : 1, Z: -10) à (x : 0, Y : 0, Z : 0)

   ![Appareil photo dans le volet de l’inspecteur dans Unity](images/maincamera-350px.png)<br>
   *Appareil photo dans le volet de l’inspecteur dans Unity*

## <a name="clip-planes"></a>Plans de coupe

Rendu de contenu trop proche de l’utilisateur peut être inconfortable en réalité mixte. Vous pouvez ajuster le [près et plans de coupe présent](hologram-stability.md#hologram-render-distances) sur le composant de l’appareil photo.
1. Sélectionnez la caméra principale dans le volet de hiérarchie
2. Dans le panneau d’inspecteur, rechercher les plans de découpage de composant de caméra et diffère de la zone de texte quasi 0.3.85. Le contenu restitué encore plus proche peut entraîner une gêne utilisateur et doit être évitée par le [restituer des instructions de distance](hologram-stability.md#hologram-render-distances).

## <a name="multiple-cameras"></a>Plusieurs caméras

Lorsqu’il existe plusieurs composants de l’appareil photo dans la scène, Unity sait quelle caméra à utiliser pour le rendu stéréoscopique et suivi principal en vérifiant le GameObject a la balise MainCamera.

## <a name="recentering-a-seated-experience"></a>Recentering une expérience assise

Si vous créez un [assis à l’échelle du expérience](coordinate-systems.md), vous pouvez l’origine du monde de recentrer Unity à la position principal actuel de l’utilisateur en appelant le **[XR. InputTracking.Recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html)** (méthode).

## <a name="reprojection-modes"></a>Modes de reprojection

HoloLens et des casques IMMERSIFS seront reproject chaque cadre de votre application effectue le rendu pour s’ajuster à toute mauvaise prédiction de position principal réelle de l’utilisateur lorsque photons sont émis.

Par défaut :

* **Des casques IMMERSIFS** effectuera reprojection positionnelle, ajuster votre hologrammes pour mauvaise prédiction de la position et l’orientation, si l’application fournit un mémoire tampon de profondeur pour une trame donnée.  Si un mémoire tampon de profondeur n’est pas fourni, le système corrige uniquement mispredictions dans l’orientation.
* **Les casques HOLOGRAPHIQUE** comme HoloLens effectuera positionnelle reprojection si l’application fournit sa mémoire tampon de profondeur ou non.  Reprojection positionnelle est possible sans les tampons de profondeur sur HoloLens comme rendu est souvent partiellement alloué avec un arrière-plan stable fourni par le monde réel.

Si vous savez que vous générez un [orientation seule expérience](coordinate-systems-in-unity.md#building-an-orientation-only-or-seated-scale-experience) avec du contenu de façon rigide verrouillé de corps (par exemple, à 360 degrés le contenu vidéo), vous pouvez définir explicitement le mode reprojection en orientation uniquement en définissant [ HolographicSettings.ReprojectionMode](https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.ReprojectionMode.html) à [HolographicReprojectionMode.OrientationOnly](https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.HolographicReprojectionMode.html).

## <a name="sharing-your-depth-buffers-with-windows"></a>Partage de vos tampons de profondeur avec Windows

Partage de mémoire tampon de profondeur de votre application pour chaque trame donnera votre application une des deux accroît de stabilité HOLOGRAMME, selon le type de casque de Windows que vous êtes rendu pour :
* **Des casques IMMERSIFS** réalisables reprojection positionnelle lorsqu’un mémoire tampon de profondeur est fourni, en ajustant vos hologrammes pour mauvaise prédiction de la position et l’orientation.
* **Les casques HOLOGRAPHIQUE** comme HoloLens sélectionne automatiquement un [concentrer point](focus-point-in-unity.md) lorsqu’un mémoire tampon de profondeur est fourni, optimisation de la stabilité hologramme le long du plan qui entre en intersection avec le contenu le plus.

Pour définir si votre application Unity fournira un mémoire tampon de profondeur à Windows :
1. Accédez à **modifier** > **paramètres du projet** > **Player** > **onglet plateforme Windows universelle**  >  **XR paramètres**.
2. Développez le **SDK de réalité mixte Windows** élément.
3. Activez ou désactivez le **activer le partage de mémoire tampon de profondeur** case à cocher.  Cela sera vérifié par défaut dans les nouveaux projets créés dans la mesure où cette fonctionnalité a été ajoutée à Unity et sera désactivée par défaut pour les anciens projets qui ont été mis à niveau.

Fournir un mémoire tampon de profondeur à Windows peut améliorer la qualité visuelle tant que Windows peut mapper correctement les valeurs de la profondeur normalisée par pixel dans votre mémoire tampon de profondeur à des distances en mètres, à l’aide des plans proches que vous avez défini dans Unity sur la caméra principale.  Si votre rendu transmet la profondeur de la poignée de valeurs dans les méthodes classiques, devrait généralement être ici, bien que le rendu translucide transmet qui écrivent dans la mémoire tampon de profondeur tout en montrant via à existant pixels de couleur peuvent ainsi être dérouté la reprojection.  Si vous savez que vos passes de rendu laissera la plupart de vos pixels profondeur finale avec les valeurs de profondeur inexactes, vous êtes susceptible d’obtenir une meilleure qualité visuelle en désactivant la case « Activer la profondeur de mémoire tampon partage ».

## <a name="mixed-reality-toolkits-automatic-scenesetup"></a>Programme d’installation automatique de scène de mixte réalité la boîte à outils
Lorsque vous importez [MRTK publie des packages de Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases) ou cloner le projet à partir de la [référentiel GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity), vous vous apprêtez à trouver un nouveau menu « Toolkit de réalité mixte » dans Unity. Sous le menu « Configurer », vous verrez le menu « Application des paramètres de scène réalité mixte ». Lorsque vous cliquez dessus, il supprime l’appareil photo par défaut et ajoute les composants fondamentaux - [InputManager](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/InputManager.prefab), [MixedRealityCameraParent](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/MixedRealityCameraParent.prefab), et [DefaultCursor](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Input/Prefabs/Cursor/DefaultCursor.prefab).

![Menu MRTK pour le programme d’installation de scène](images/MRTK_Input_Menu.png)<br>
*Menu MRTK pour le programme d’installation de scène*

![Programme d’installation automatique de scène dans MRTK](images/MRTK_HowTo_Input1.png)<br>
*Programme d’installation automatique de scène dans MRTK*

## <a name="mixedrealitycamera-prefab"></a>MixedRealityCamera prefab
Vous pouvez également ajouter manuellement à partir du panneau projet. Vous pouvez trouver ces composants en tant que prefabs. Si vous effectuez une recherche **MixedRealityCamera**, vous serez en mesure de voir les deux prefabs caméra différente. La différence est, **MixedRealityCamera** est l’appareil photo uniquement prefab tandis que **MixedRealityCameraParent** inclut des composants supplémentaires pour les casques IMMERSIFS telles que téléportation, Motion Contrôleur et limites.

![Prefabs caméra dans MRTK](images/MRTK_HowTo_Input2.png)<br>
*Prefabs caméra dans MRTK*

**MixedRealtyCamera** prend en charge HoloLens et immersif casque. Il détecte le type d’appareil et optimise les propriétés telles que d’effacer les indicateurs et Skybox. Vous trouverez ci-dessous certaines des propriétés utiles, vous pouvez personnaliser comme curseur personnalisé, les modèles de contrôleur de mouvement et Floor.

![Propriétés pour le contrôleur de mouvement, curseur et étage](images/MRTK_HowTo_Input3.png)<br>
*Propriétés pour le contrôleur de mouvement, curseur et étage*

## <a name="see-also"></a>Voir aussi
* [Stabilité HOLOGRAMME](hologram-stability.md)
* [MixedRealityToolkit Main Camera.prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Input/Prefabs)
