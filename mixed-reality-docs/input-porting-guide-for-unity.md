---
title: Guide de Portage d’entrée pour Unity
description: Apprenez à gérer les entrées pour Windows Mixed Reality dans Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: entrée, Unity, Portage
ms.openlocfilehash: 20e8efa09d20b0a9eaa246015d9c185884f9c216
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63515497"
---
# <a name="input-porting-guide-for-unity"></a>Guide de Portage d’entrée pour Unity

Vous pouvez porter votre logique d’entrée vers Windows Mixed Reality à l’aide de l’une des deux approches, les API d’entrée générales d’Unity. GetButton/GetAxis qui s’étendent sur plusieurs plateformes ou sur le XR spécifique à Windows. WSA. API d’entrée qui offrent des données plus riches pour les contrôleurs de mouvement et les mains de HoloLens.

## <a name="general-inputgetbuttongetaxis-apis"></a>Entrées générales. GetButton/GetAxis API

Unity utilise actuellement ses API d’entrée. GetButton/Input. GetAxis pour exposer l’entrée pour [le kit de développement logiciel (SDK) Oculus](https://docs.unity3d.com/Manual/OculusControllers.html) et [le kit de développement logiciel (SDK) OpenVR](https://docs.unity3d.com/Manual/OpenVRControllers.html). Si vos applications utilisent déjà ces API pour l’entrée, il s’agit du chemin le plus simple pour la prise en charge des contrôleurs de mouvement dans Windows Mixed Reality: vous devez simplement remapper les boutons et les axes dans le gestionnaire d’entrée.

Pour plus d’informations, consultez le [tableau des mappages bouton Unity/AXIS](gestures-and-motion-controllers-in-unity.md#unity-buttonaxis-mapping-table) et [vue d’ensemble des API Unity courantes](gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis).

## <a name="windows-specific-xrwsainput-apis"></a>XR spécifique à Windows. WSA. API d’entrée

Si votre application crée déjà une logique d’entrée personnalisée pour chaque plateforme, vous pouvez choisir d’utiliser les API d’entrée spatiale spécifiques à Windows sous l’espace de noms **UnityEngine. XR. WSA. Input** . Cela vous permet d’accéder à des informations supplémentaires, telles que la précision de la position ou le genre de source, vous permettant de distinguer les mains et les contrôleurs de HoloLens.

Pour plus d’informations, consultez la [vue d’ensemble des API UnityEngine. XR. WSA. Input](gestures-and-motion-controllers-in-unity.md#windows-specific-apis-xrwsainput).

## <a name="grip-pose-vs-pointing-pose"></a>Poignée de pose et pose de pointage

Windows Mixed Reality prend en charge les contrôleurs de mouvement dans un large éventail de facteurs de forme, la conception de chaque contrôleur étant différente dans sa relation entre la position de l’utilisateur et la direction «avant» naturelle que les applications doivent utiliser pour pointer lors du rendu de la SideWinder.

Pour mieux représenter ces contrôleurs, il existe deux types de poses que vous pouvez examiner pour chaque source d’interaction:

* La **poignée pose**, représentant l’emplacement de la paume d’une main détectée par un HoloLens, ou la paume contenant un contrôleur de mouvement.
    * Sur les casques immersifs, cette pose est idéale pour afficher **la main de l’utilisateur** ou **un objet détenu par l’utilisateur**, tel qu’un arme ou un pistolet.
    * Position de la **poignée**: Le centre de la poche quand il maintient le contrôleur naturellement, ajusté à gauche ou à droite pour centrer la position au sein de la poignée.
    * **Axe droit de l’orientation de la poignée**: Lorsque vous ouvrez complètement votre main pour former une pose plate à 5 doigts, le rayon normal à votre Palm (à partir de la poche de gauche, en arrière depuis la paume de droite)
    * **Axe vers l’avant de l’orientation de la poignée**: Lorsque vous fermez partiellement votre main (comme si vous détenir le contrôleur), le rayon qui pointe vers l’avant dans le tube formé par vos doigts non thumbs.
    * **Axe vers le haut de l’orientation de la poignée**: Axe vers le haut impliqué par les définitions Right et Forward.
    * Vous pouvez accéder à la poignée à l’aide de l’API d’entrée entre fournisseurs de l’unité Unity ( **[XR. InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html). GetLocalPosition/rotation**) ou par le biais de l’API spécifique à Windows (**SourceState. SourcePose. TryGetPosition/rotation**, demandant la poignée pose).
* Le **pointeur se pose**, représentant l’extrémité du contrôleur pointant vers l’avant.
    * Ce modèle est mieux utilisé pour raycast quand vous **pointez sur l’interface utilisateur** lorsque vous rendez le modèle de contrôleur lui-même.
    * Actuellement, le pointeur pose est disponible uniquement par le biais de l’API spécifique à Windows (**sourceState. sourcePose. TryGetPosition/rotation**, demandant le pointeur pose).

Ces coordonnées de pose sont toutes exprimées en coordonnées universelles Unity.

## <a name="see-also"></a>Voir aussi
* [Contrôleurs de mouvement](motion-controllers.md)
* [Mouvements et contrôleurs de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md)
* [UnityEngine. XR. WSA. Input](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.html)
* [UnityEngine. XR. InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html)
* [Guides de Portage](porting-guides.md)
