---
title: Rendu
description: Rendu HOLOGRAPHIQUE permet à votre application dessiner un hologramme dans un emplacement précis dans le monde de l’utilisateur, si elle est placée avec précision dans le monde physique ou dans un domaine virtuel que vous avez créé.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: rendu, HOLOGRAMME
ms.openlocfilehash: 45713fd7a30fc55a799da7e89ef52aff8f7eec46
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67415410"
---
# <a name="rendering"></a>Rendu

Rendu HOLOGRAPHIQUE permet à votre application dessiner un hologramme dans un emplacement précis dans le monde de l’utilisateur, si elle est placée avec précision dans le monde physique ou dans un domaine virtuel que vous avez créé. [Hologrammes](hologram.md) sont des objets de lumière et son. Rendu permet à votre application Ajouter la lumière.

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><strong>HoloLens 2</strong></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Rendu</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="holographic-rendering"></a>Rendu HOLOGRAPHIQUE

Au holographic rendu est essentiel si vous effectuez un rendu à un affichage transparent comme HoloLens qui permet à l’utilisateur de consulter le monde physique et votre hologrammes ensemble--ou un affichage opaque comme un casque immersif Windows Mixed Reality qui bloque out le monde.

Appareils avec **affiche transparente**, par exemple [HoloLens](hololens-hardware-details.md), ajoutez la lumière au monde. Pixels noirs sont entièrement transparentes, tandis que des pixels plus clairs sont plus en plus opaques. Étant donné que la lumière à partir de l’affiche est ajoutée à la lumière dans le monde réel, pixels blancs sont quelque peu translucides.

Alors que rendu stéréoscopique fournit un effet de profondeur pour votre hologrammes, ajout [mise à la terre des effets](interaction-fundamentals.md) peut aider les utilisateurs à voir plus facilement le surface un hologramme est proche. Une technique de mise à la terre consiste à ajouter un rayonnement autour d’un hologramme sur l’aire de proximité, puis pour restituer une ombre contre cette lumière. De cette façon, vos clichés instantanés s’affiche à soustraire de lumière à partir de l’environnement. [Son spatial](spatial-sound.md) est une autre file d’attente profondeur extrêmement important, vous permettant de motif d’utilisateurs sur la distance et l’emplacement relatif d’un hologramme.

Appareils avec **affiche opaque**, comme [des casques IMMERSIFS Windows Mixed Reality](immersive-headset-hardware-details.md), bloquer l’univers. Pixels noirs sont noire unie, et toute autre couleur s’affichent en tant que cette couleur à l’utilisateur. Votre application est responsable du rendu de tout ce que l’utilisateur voit. Cela rend encore plus important de conserver une fréquence d’actualisation constante afin que les utilisateurs aient une expérience à l’aise.

## <a name="predicted-rendering-parameters"></a>Paramètres de rendu prédites

Mixte casques réalité (HoloLens et des casques IMMERSIFS) en permanence, effectuer le suivi de la position et l’orientation de tête de l’utilisateur par rapport à leur environnement. Lorsque votre application commence à préparer son frame suivant, le système prédit où tête de l’utilisateur est à l’avenir pour le moment exact le frame s’affiche sur l’affiche. Selon cette prédiction, le système calcule les transformations de projection et d’affichage à utiliser pour ce frame. Votre application **doit utiliser ces transformations pour produire des résultats corrects**; si transformations fourni par le système ne sont pas utilisées, l’image résultante n’est pas alignées avec le monde réel, ce qui conduit à une gêne utilisateur.

Notez que pour prédire avec précision quand un nouveau frame atteindra l’affiche, le système en permanence évalue la latence de bout en bout effective du pipeline de rendu de votre application. Alors que le système s’ajuste à la longueur de votre pipeline de rendu, vous pouvez améliorer la stabilité hologramme en conservant ce pipeline aussi courte que possible.

Les applications qui utilisent des techniques avancées pour améliorer la prédiction de système peuvent remplacer les transformations de projection et d’affichage du système. Ces applications doivent doit toujours utiliser transformations fourni par le système comme base pour des transformations personnalisées afin de produire des résultats significatifs.

## <a name="other-rendering-parameters"></a>Autres paramètres de rendu

Lors du rendu d’un frame, le système définit la fenêtre d’affichage de la mémoire tampon d’arrière-plan dans lequel votre application doit être dessiné. Cette fenêtre d’affichage est souvent inférieure à la taille totale de la mémoire tampon de trame. Quelle que soit la taille de la fenêtre d’affichage, une fois que le frame est affiché par l’application, le système upscales l’image pour remplir l’intégralité de l’affiche.

Pour les applications qui se retrouvent Impossible de restituer à la fréquence de rafraîchissement requis, [système rendu paramètres peuvent être configurés](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfiguration#Windows_Graphics_Holographic_HolographicViewConfiguration) afin de réduire la sollicitation de la mémoire et les coûts de rendu au détriment de l’alias de pixel accrue. Le format de la mémoire tampon d’arrière-plan peut également être modifié, ce qui pour certaines applications peut aider à améliorer le débit de bande passante et de pixels de mémoire.

Le frustum de rendu, la résolution et la fréquence d’images dans lequel votre application doit s’afficher peuvent également changer à partir d’une image à l’autre et peuvent différer entre le œil gauche et droite. Par exemple, lorsque [mixte de capture de la réalité](mixed-reality-capture.md) (MRC) est actif et le [afficher la configuration de caméra vidéo/photo](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfigurationKind#Windows_Graphics_Holographic_HolographicViewConfigurationKind) n’est pas choisi-dans, un oeil peut être rendu avec un angle d’ouverture ou de résolution supérieure.

Pour chaque frame, votre application *doit* rendus à l’aide de la transformation d’affichage, la transformation de projection et la résolution de la fenêtre d’affichage fourni par le système. En outre, votre application ne doit jamais supposer que n’importe quel paramètre de rendu ou de la vue reste fixe à partir de l’image à l’autre. Moteurs de tels que Unity gèrent toutes ces transformations pour vous dans leurs propres objets caméra afin que le déplacement physique de vos utilisateurs et l’état du système est toujours respecté. Si votre application accepte le déplacement des virtuels de l’utilisateur à travers le monde (par exemple, en utilisant le stick analogique sur un boîtier de commande), vous pouvez ajouter un objet de la plateforme de test parent au-dessus de l’appareil photo qui se déplace sur. Par conséquent, l’appareil photo afin de refléter les mouvements physiques et virtuels de l’utilisateur. Si votre application modifie la transformation d’affichage, de la transformation de projection ou de la dimension de la fenêtre d’affichage fournie par le système, il doit informer le système en appelant approprié [remplacer API](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicCameraPose#Windows_Graphics_Holographic_HolographicCameraPose).

Pour améliorer la stabilité de votre rendu HOLOGRAPHIQUE, votre application doit fournir pour Windows chaque frame de la mémoire tampon de profondeur qu'il utilisé pour le rendu. Si votre application ne fournit pas un mémoire tampon de profondeur, il doit avoir des valeurs de profondeur cohérente, avec la profondeur exprimée en mètres à partir de l’appareil photo. Ainsi, le système à utiliser vos données de profondeur par pixel pour stabiliser mieux contenu si tête de l’utilisateur se retrouve légèrement décalée par rapport à l’emplacement prédite. Si vous n’êtes pas en mesure de fournir votre mémoire tampon de profondeur, vous pouvez fournir un point de focus et de la normale, définissant un plan qui réduit à la plupart de votre contenu. Si la mémoire tampon de profondeur et un plan de focus sont fournis, le système peut utiliser les deux. En particulier, il est utile fournir la mémoire tampon de profondeur et un point de focus qui inclut un vecteur de rapidité lorsque votre application affiche hologrammes qui sont en mouvement.

Reportez-vous à [rendu dans DirectX](rendering-in-directx.md) article pour plus d’informations de bas niveau à son sujet.

## <a name="holographic-cameras"></a>Caméras HOLOGRAPHIQUE

Windows Mixed Reality introduit le concept d’un **caméra HOLOGRAPHIQUE**. Caméras HOLOGRAPHIQUE sont similaires à la caméra traditionnelle trouvée dans les textes de graphismes 3D : elles définissent les deux extrinsèques (position et l’orientation) et les propriétés de caméra intrinsèque. (Par exemple :, champ de vue est utilisé pour afficher une scène 3D virtuelle.) Contrairement aux caméras 3D traditionnels, l’application n’est pas dans le contrôle de la position, l’orientation et les propriétés intrinsèques de l’appareil photo. Au lieu de cela, la position et l’orientation de la caméra holographique est implicitement contrôlé par le déplacement de l’utilisateur. Déplacement de l’utilisateur est relayé à l’application sur une base d’image par image via une transformation d’affichage. De même, les propriétés intrinsèques de la caméra sont définies par optique étalonné de l’appareil et relayée image par image par le biais de la transformation de projection.

En règle générale, votre application affichera pour une seule caméra stéréo. Toutefois, une boucle de rendu robuste prendra en charge plusieurs caméras et prendra en charge les caméras stéréo et mono. Par exemple, le système peut demander à votre application pour effectuer le rendu à partir d’un autre point de vue lorsque l’utilisateur Active une fonctionnalité comme [mixte de capture de la réalité](mixed-reality-capture.md) MRC (), en fonction de la forme du casque en question. Applications prenant en charge plusieurs caméras obtenez-les [désactivation dans](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfiguration#Windows_Graphics_Holographic_HolographicViewConfiguration) à la [type](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfigurationKind#Windows_Graphics_Holographic_HolographicViewConfigurationKind) des caméras, ils peuvent prendre en charge.

## <a name="volume-rendering"></a>Rendu de volume

Lorsque rendu IRM médicaux ou de volumes en 3D, d’ingénierie [rendu de volume](volume-rendering.md) techniques sont souvent utilisées. Ces techniques peuvent être particulièrement intéressants dans la réalité mixte, où les utilisateurs peuvent afficher naturellement un volume à partir des angles de clé, en déplaçant leur tête.

## <a name="supported-resolutions-on-hololens-1st-gen"></a>Prise en charge des résolutions sur HoloLens (1er gen)
> [!NOTE]
> Autres mises à jour sont à venir. [Afficher la liste de mise à jour](release-notes-april-2018.md)

* Les résolutions prises en charge actuelles et maximales sont des propriétés de la [afficher la configuration](https://docs.microsoft.com/uwp/api/Windows.Graphics.Holographic.HolographicViewConfiguration#Windows_Graphics_Holographic_HolographicViewConfiguration). HoloLens est défini sur la résolution maximale, qui est 720p (1268 x 720), par défaut.
* La taille de la fenêtre d’affichage de la plus basse pris en charge est de 50 % de 720p, c'est-à-dire 360p (634 x 360). Sur HoloLens, il s’agit d’un ViewportScaleFactor de 0,5.
* Quoi que ce soit inférieures 540p est **déconseillé** en raison de la dégradation visual, mais peut être utilisé pour identifier les goulets d’étranglement dans les taux de remplissage de pixel.

## <a name="supported-resolutions-on-hololens-2"></a>Résolutions prises en charge sur HoloLens 2

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).


## <a name="see-also"></a>Voir aussi
* [Stabilité des hologrammes](hologram-stability.md)
* [Rendu dans DirectX](rendering-in-directx.md)
