---
title: Texte dans Unity
description: 'Pour afficher du texte dans Unity, il existe deux types de composants de texte que vous pouvez utiliser : le texte de l’interface utilisateur et le maillage de texte 3D.'
author: cre8ivepark
ms.author: dongpark
ms.date: 06/03/2019
ms.topic: article
keywords: Windows Mixed Reality, conception, contrôles, police, typographie, UI, UX
ms.openlocfilehash: 8662ff8a8e1e99455354392d7dc852feb1fe1589
ms.sourcegitcommit: 7ca383ef1c5dc895ca2a289435f2e9d4c1ee6e65
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85345709"
---
# <a name="text-in-unity"></a>Texte dans Unity

Le texte est l’un des composants les plus importants des applications holographiques. Pour afficher du texte dans Unity, il existe trois types de composants de texte que vous pouvez utiliser : texte de l’interface utilisateur, maillage de texte 3D et maillage Pro. Par défaut, le texte de l’interface utilisateur et le maillage de texte 3D apparaissent flous et sont trop grands. Vous devez ajuster quelques variables pour obtenir un texte clair et de haute qualité qui a une taille gérable dans HoloLens. En appliquant un facteur d’échelle pour obtenir des dimensions appropriées lorsque vous utilisez les composants texte de l’interface utilisateur et maillage de texte 3D, vous pouvez obtenir une meilleure qualité de rendu.

![Comment faire du texte clair et merveilleux](images/hug-text-02-640px.png)<br>
*Texte par défaut flou dans Unity*

## <a name="working-with-unitys-3d-text-text-mesh-and-ui-text"></a>Utilisation du texte 3D de Unity (maillage de texte) et du texte de l’interface utilisateur

Unity suppose que tous les nouveaux éléments ajoutés à une scène ont une taille de 1 unité Unity, ou une échelle de transformation 100%, qui se traduit par environ 1 mètre sur HoloLens. Dans le cas des polices, le cadre englobant d’un TextMesh 3D est fourni par défaut à environ 1 mètre en hauteur.

![Utilisation des polices dans Unity](images/640px-hug-text-03.png)<br>
*Le texte 3D Unity par défaut (maillage de texte) occupe 1 unité Unity qui est 1 mètre*

<br>
La plupart des concepteurs visuels utilisent des points pour définir les tailles de police dans le monde réel. Il y a environ 2835 (2 834.645666399962) points dans 1 mètre. En fonction de la conversion du système de point en 1 mètre et de la taille de police de la maille du texte par défaut de l’unité de mesure 13, la simple mathématique de 13 divisée par 2835 est égale à 0,0046 (0.004586111116), ce qui offre une bonne mise à l’échelle standard pour commencer (certains peuvent souhaiter aller jusqu’à 0,005). La mise à l’échelle de l’objet ou du conteneur de texte à ces valeurs n’autorise pas seulement la conversion de 1:1 de tailles de police dans un programme de conception, mais fournit également une norme pour vous permettre de maintenir la cohérence tout au long de votre expérience.

![Maillage de texte 3D Unity avec différentes tailles de police](images/Text_In_Unity_Measurements1.png)<br>
*Mise à l’échelle des valeurs pour le texte 3D Unity et texte de l’interface utilisateur*

<br>

![Maillage de texte 3D Unity avec différentes tailles de police](images/hug-text-05-1000px.png)<br>
*Maillage de texte 3D Unity avec des valeurs optimisées*

<br>
Quand vous ajoutez un élément de texte basé sur une interface utilisateur ou un canevas à une scène, la disparité de taille est encore plus importante. Les différences entre les deux tailles sont d’environ 1000%, ce qui fait passer le facteur d’échelle pour les composants de texte basés sur l’interface utilisateur à 0,00046 (0.0004586111116 est exact) ou 0,0005 pour la valeur arrondie.

![Texte de l’interface utilisateur Unity avec différents pixels dynamiques par valeur unitaire](images/hug-text-04-1000px.png)<br>
*Texte de l’interface utilisateur Unity avec des valeurs optimisées*

<br>

>[!NOTE]
>La valeur par défaut de toute police peut être affectée par la taille de la texture de cette police ou la manière dont la police a été importée dans Unity. Ces tests ont été exécutés en fonction de la police Arial par défaut dans Unity, ainsi que d’une autre police importée.

## <a name="working-with-text-mesh-pro"></a>Utilisation de Text Mesh Pro

Avec le texte de la maille Pro de Unity, vous pouvez sécuriser la qualité de rendu du texte. Elle prend en charge les contours de texte nets, quelle que soit la distance à l’aide de la technique du [champ à distance signée (SDF)](https://steamcdn-a.akamaihd.net/apps/valve/2007/SIGGRAPH2007_AlphaTestedMagnification.pdf) . À l’aide de la méthode de calcul que nous avons utilisée ci-dessus pour le texte 3D et le texte de l’interface utilisateur, nous pouvons trouver les valeurs de mise à l’échelle appropriées à utiliser avec les points typographiques conventionnels. Étant donné que la police par défaut de maillage de texte 3D avec la taille 36 a une taille limite de 2,5 unités Unity (2,5 millions), nous pouvons utiliser une valeur de mise à l’échelle de 0,005 pour obtenir la taille en points. La taille de la limite par défaut de 25 unités Unity (25m) est définie dans le maillage de texte Pro du menu de l’interface utilisateur. Cela nous donne 0,0005 pour la valeur de mise à l’échelle.

![Maillage de texte 3D Unity avec différentes tailles de police](images/Text_In_Unity_Measurements2.png)<br>
*Mise à l’échelle des valeurs pour le texte 3D Unity et texte de l’interface utilisateur*

## <a name="recommended-text-size"></a>Taille de texte recommandée
Comme vous pouvez vous y attendre, les tailles de type que nous utilisons sur un PC ou un appareil tablette (généralement entre 12 et 32 points) semblent très petites à une distance de 2 mètres. Elle dépend des caractéristiques de chaque police, mais en général, l’angle de visualisation minimal recommandé et la hauteur de police pour la lisibilité sont autour de 0.35 °-0,4 °/12.21-13.97mm en fonction des études de recherche des utilisateurs. Il s’agit d’environ 35 40pt avec le facteur de mise à l’échelle présenté ci-dessus. 

Pour l’approche near interaction à 0.45 m (45cm), l’angle d’affichage de la police à la hauteur minimale et la hauteur sont de 0,4 °-0,5 °/3.14 – 3,9 mm. Elle est d’environ 9 à 12 PT avec le facteur d’échelle présenté ci-dessus.

![Contenu de plage d’interaction near et Far ](images/typography-distance-1000px.jpg)
 *dans une plage d’interaction proche et éloignée*

### <a name="the-minimum-legible-font-size"></a>Taille de police minimale lisible
| Distance | Angle d’affichage | Hauteur du texte | Taille de police |
|---------|---------|---------|---------|
| 45cm (distance de manipulation directe) | 0,4 °-0,5 ° | 3.14 – 3,9 mm | 8,9 – 11.13 PT |
| dollars | 0.35 °-0,4 ° | 12.21 – 13.97 mm | 34.63-39.58 PT |


### <a name="the-comfortably-legible-font-size"></a>Taille de police lisible
| Distance | Angle d’affichage | Hauteur du texte | Taille de police |
|---------|---------|---------|---------|
| 45cm (distance de manipulation directe) | 0,65 °-0,8 ° | 5.1-6.3 mm | 14.47-17.8 PT |
| dollars | 0,6 °-0,75 ° | 20.9-26.2 mm | 59.4-74.2 PT |

Segoe UI (police par défaut pour Windows) fonctionne bien dans la plupart des cas. Toutefois, évitez d’utiliser des familles de polices légères ou semi-claires en petite taille, car les traits verticaux fins vibreront et la lisibilité sera dégradée. Les polices modernes avec suffisamment d’épaisseur de trait fonctionnent bien. Par exemple, Helvetica et Arial semblent exceptionnels et sont très lisibles dans HoloLens avec des pondérations standard ou en gras.


![Affichage de la ](images/Text_In_Unity_ViewingAngle.jpg)
 *distance d’affichage de l’angle, angle et hauteur du texte*

## <a name="sharp-text-rendering-quality-with-proper-dimension"></a>Qualité de rendu de texte précise avec une dimension appropriée

En fonction de ces facteurs de mise à l’échelle, nous avons créé le [texte prefabs avec le texte de l’interface utilisateur et le maillage de texte 3D](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MRTK/SDK/StandardAssets/Prefabs/Text). Les développeurs peuvent utiliser ces prefabs pour optimiser le texte et la taille de police.

![Qualité de rendu de texte précise avec une dimension appropriée](images/hug-text-06-1000px.png)<br>
*Qualité de rendu de texte précise avec une dimension appropriée*

## <a name="shader-with-occlusion-support"></a>Nuanceur avec prise en charge d’occlusion

La matière de police par défaut d’Unity ne prend pas en charge l’occlusion. Pour cette raison, le texte derrière les objets s’affiche par défaut. Nous avons inclus un [nuanceur simple qui prend en charge l’occlusion](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Assets/MixedRealityToolkit/StandardAssets/Shaders/Text3DShader.shader). L’image ci-dessous montre le texte avec les éléments de police par défaut (à gauche) et le texte avec une occlusion appropriée (à droite).

![Nuanceur avec prise en charge d’occlusion](images/hug-text-07-1000px.png)<br>
*Nuanceur avec prise en charge d’occlusion*


## <a name="see-also"></a>Voir aussi
* [Texte Prefab dans le MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Prefabs/Text)
* [Typographie](typography.md)

 
