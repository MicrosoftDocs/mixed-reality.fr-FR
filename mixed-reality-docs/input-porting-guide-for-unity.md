---
title: Entrée portage guide pour Unity
description: Découvrez comment gérer l’entrée pour la réalité mixte de Windows dans Unity.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: entrée, unity, portage
ms.openlocfilehash: 20e8efa09d20b0a9eaa246015d9c185884f9c216
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595728"
---
# <a name="input-porting-guide-for-unity"></a>Entrée portage guide pour Unity

Vous pouvez porter votre logique d’entrée à une réalité mixte Windows à l’aide d’une des deux approches, API Input.GetButton/GetAxis général d’Unity qui s’étendent sur plusieurs plateformes, ou le XR spécifiques à Windows. WSA. API d’entrée qui envoient des données plus riches spécifiquement pour les contrôleurs de mouvement et HoloLens mains.

## <a name="general-inputgetbuttongetaxis-apis"></a>API de Input.GetButton/GetAxis général

Unity utilise actuellement ses API Input.GetButton/Input.GetAxis général pour exposer une entrée pour [le SDK Oculus](https://docs.unity3d.com/Manual/OculusControllers.html) et [le SDK OpenVR](https://docs.unity3d.com/Manual/OpenVRControllers.html). Si vos applications sont déjà à l’aide de ces API pour l’entrée, il s’agit de la plus simple pour prendre en charge des contrôleurs de mouvement en réalité mixte Windows : vous devez simplement remapper les boutons et les axes dans le Gestionnaire d’entrée.

Pour plus d’informations, consultez le [table de mappage de bouton/axe Unity](gestures-and-motion-controllers-in-unity.md#unity-buttonaxis-mapping-table) et [vue d’ensemble de l’API Unity courantes](gestures-and-motion-controllers-in-unity.md#common-unity-apis-inputgetbuttongetaxis).

## <a name="windows-specific-xrwsainput-apis"></a>Windows spécifiques XR. WSA. API d’entrée

Si votre application génère déjà la logique d’entrée personnalisée pour chaque plateforme, vous pouvez choisir d’utiliser les API d’entrée spatiales spécifiques à Windows sous la **UnityEngine.XR.WSA.Input** espace de noms. Cela vous permet d’accéder à des informations supplémentaires, telles que de la précision de la position ou le type de source, ce qui vous permet d’indiquer les mains et contrôleurs éloignés sur HoloLens.

Pour plus d’informations, consultez le [vue d’ensemble des APIs UnityEngine.XR.WSA.Input](gestures-and-motion-controllers-in-unity.md#windows-specific-apis-xrwsainput).

## <a name="grip-pose-vs-pointing-pose"></a>Pose de poignée et pose de pointage

Réalité mixte Windows prend en charge les contrôleurs de mouvements dans un large éventail de facteurs de forme, avec la conception de chaque contrôleur qui se différencie par sa relation entre la position des utilisateurs manuellement et naturel « transférer » direction que les applications doit utiliser pour le pointage lors du rendu de la contrôleur.

Pour mieux représenter ces contrôleurs, il existe deux types de risque de poser que vous pouvez examiner pour chaque source de l’interaction :

* Le **pose de poignée**, représentant l’emplacement de la portée de main détectée par un HoloLens ou palm contenant un contrôleur de mouvement.
    * Sur des casques IMMERSIFS, cette pose mieux permet de restituer **main de l’utilisateur** ou **détenues par un objet à portée de main de l’utilisateur**, tel qu’un mot de passe ou les électrons.
    * Le **Attrapez position**: Le centroïde de palm naturellement, tout en maintenant le contrôleur ajustée gauche ou droite pour centrer la position au sein de la poignée.
    * Le **Attrapez axe de droite de l’orientation**: Lorsque vous ouvrez totalement la main pour former une pose plat 5-doigt, le rayon qui est normal pour votre palm (en avant à partir de la gauche palm, vers l’arrière de palm droite)
    * Le **Attrapez axe vers l’avant de l’orientation**: Lorsque vous fermez votre main partiellement (comme le cas maintenant le contrôleur), le rayon pointe « forward » via le tube formé par vos doigts non curseur.
    * Le **Attrapez orientation d’axe**: L’axe à distance impliqué par les définitions de droite, en avant.
    * Vous pouvez accéder à la pose de poignée via une entrée soit Unity entre fournisseurs API (**[XR. InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html). GetLocalPosition/Rotation**) ou via l’API Windows spécifique (**sourceState.sourcePose.TryGetPosition/Rotation**, demandant la pose de poignée).
* Le **pose de pointeur**, qui représente l’info-bulle du contrôleur qui pointe vers l’avant.
    * Cette pose est mieux utilisé pour raycast lorsque **vers l’interface utilisateur** lorsque vous restituez le modèle de contrôleur lui-même.
    * Actuellement, la pose de pointeur est uniquement disponible via l’API Windows spécifique (**sourceState.sourcePose.TryGetPosition/Rotation**, demandant la pose de pointeur).

Ces pose les coordonnées sont exprimées en coordonnées universelles de Unity.

## <a name="see-also"></a>Voir aussi
* [Contrôleurs de mouvement](motion-controllers.md)
* [Mouvements et les contrôleurs de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md)
* [UnityEngine.XR.WSA.Input](https://docs.unity3d.com/ScriptReference/XR.WSA.Input.InteractionManager.html)
* [UnityEngine.XR.InputTracking](https://docs.unity3d.com/ScriptReference/XR.InputTracking.html)
* [Portage des repères](porting-guides.md)
