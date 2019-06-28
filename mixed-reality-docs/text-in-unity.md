---
title: Texte dans Unity
description: 'Pour afficher du texte dans Unity, il existe deux types de composants de texte que vous pouvez utiliser : texte d’interface utilisateur et le maillage de texte 3D.'
author: cre8ivepark
ms.author: dongpark
ms.date: 06/03/2019
ms.topic: article
keywords: Windows Mixed Reality, conception, des contrôles, police, typographie, l’interface utilisateur, l’expérience utilisateur
ms.openlocfilehash: f57b04c7d57219b7426793879004ef010d2b1ea8
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67415438"
---
# <a name="text-in-unity"></a>Texte dans Unity

Texte est un des composants plus importants dans les applications HOLOGRAPHIQUE. Pour afficher du texte dans Unity, il existe trois types de composants de texte que vous pouvez utiliser : texte d’interface utilisateur, le maillage de texte 3D et texte de maillage Pro. Par défaut de textes d’interface utilisateur et de maillage de texte 3D floues et sont trop volumineux. Vous devez modifier quelques variables pour obtenir sharp, qualité de texte qui a une taille gérable dans HoloLens. En appliquant un facteur d’échelle pour obtenir des dimensions correctes lorsque vous utilisez le texte de l’interface utilisateur et les composants de texte de maillage 3D, vous pouvez obtenir une meilleure qualité de rendu.

![Comment obtenir le texte sharp et magnifiques](images/hug-text-02-640px.png)<br>
*Texte par défaut floue dans Unity*

## <a name="working-with-unitys-3d-texttext-mesh-and-ui-text"></a>Utilisation de texte 3D (maillage de texte) et le texte de l’interface utilisateur d’Unity

Unity suppose que tous les nouveaux éléments ajoutés à une scène sont 1 unité de Unity dans la taille ou d’échelle de transformation de 100 %, ce qui se traduit par environ 1 mètre sur HoloLens. Dans le cas des polices, la zone englobante pour un TextMesh 3D est fourni par défaut à environ 1 mètre en hauteur.

![Utilisation des polices dans Unity](images/640px-hug-text-03.png)<br>
*Par défaut Unity 3D Text (texte de maillage) occupe 1 unité de Unity qui est de 1 mètre*

<br>
La plupart des concepteurs visuels utilisent des points pour définir des tailles de police dans le monde réel. Il existe environ 2835 (2,834.645666399962) points dans 1 mètre. En fonction de la conversion point système 1 mètre et par défaut de maillage texte taille de police 13 d’Unity, les mathématiques simples de 13 divisé par 2835 equals 0.0046 (0.004586111116 pour être exact) fournit une bonne évolutivité standard pour commencer (Certains voudraient arrondir à 0,005). Mise à l’échelle de l’élément textuel ou le conteneur à ces valeurs offrira non seulement pour la conversion de 1:1 de police tailles dans un programme de conception, mais fournit également une norme afin de maintenir la cohérence tout au long de votre expérience.

![Unity 3D texte de maillage avec des tailles de police](images/Text_In_Unity_Measurements1.png)<br>
*Mise à l’échelle de valeurs pour le texte 3D Unity et le texte de l’interface utilisateur*

![Unity 3D texte de maillage avec des tailles de police](images/hug-text-05-1000px.png)<br>
*Unity 3D texte de maillage avec des valeurs optimisés*

<br>
Lorsque vous ajoutez un élément de texte en fonction de l’interface utilisateur ou de la zone de dessin à une scène, les différences de taille est toujours supérieure. Les différences dans les deux tailles est environ 1000 %, ce qui pourrait apporter le facteur d’échelle pour l’interface utilisateur en fonction des composants de texte à 0.00046 (0.0004586111116 pour être exact) ou 0,0005 pour la valeur arrondie.

![Texte de l’interface utilisateur de Unity avec différents pixels dynamiques par les valeurs d’unité](images/hug-text-04-1000px.png)<br>
*Texte de l’interface utilisateur de Unity avec valeurs optimisées*

<br>

>[!NOTE]
>La valeur par défaut de toutes les polices peut-être être affectée par la taille de texture de cette police ou la façon dont la police a été importée dans Unity. Ces tests ont été effectuées en fonction de la police Arial par défaut dans Unity, ainsi que d’une autre police importée.

## <a name="working-with-text-mesh-pro"></a>Utilisation de texte de maillage Pro

Avec texte de maillage Pro du Unity, vous pouvez sécuriser la qualité de rendu de texte. Il prend en charge le contour du texte clair, quel que soit la distance à l’aide de la [SDF (champ de Distance Signed)](https://steamcdn-a.akamaihd.net/apps/valve/2007/SIGGRAPH2007_AlphaTestedMagnification.pdf) technique. À l’aide de la même méthode de calcul que nous avons utilisé ci-dessus pour le maillage de texte 3D et le texte de l’interface utilisateur, nous pouvons trouver les valeurs de mise à l’échelle appropriées à utiliser le Point typographique conventionnel. Étant donné que la police de texte de maillage Pro 3D par défaut avec la taille de 36 montre le cadre englobant de 2,5 Unit(2.5m) Unity, nous pouvons utiliser la valeur mise à l’échelle 0,005 pour utiliser la taille de Point. Le texte de maillage Pro sous le menu de l’interface utilisateur a la valeur par défaut englobant la taille de 25 Unit(25m) Unity. Cela nous donne 0,0005 pour la valeur mise à l’échelle.

![Unity 3D texte de maillage avec des tailles de police](images/Text_In_Unity_Measurements2.png)<br>
*Mise à l’échelle de valeurs pour le texte 3D Unity et le texte de l’interface utilisateur*

## <a name="recommended-text-size"></a>Taille du texte recommandée
Comme vous pouvez l’imaginer, les tailles de type que nous utilisons sur un PC ou une tablette (en général entre 12 – 32 points) Examinez relativement petites une distance de 2 mètres. Il dépend des caractéristiques de chaque police, mais en général le minimum recommandé affichage angle et la hauteur de police pour une meilleure lisibilité concernent 0.35°-0.4°/12.21-13.97mm selon nos études de recherche utilisateur. Il s’agit 35-40pt avec le facteur d’échelle présentée ci-dessus. 

Pour l’interaction proche à 0.45m(45cm), angle de visualisation de la police lisibles minimale et la hauteur sont 0,4 °-0,5 ° / 3.14 – 3.9 mm. Il s’agit 9-12 pt avec le facteur d’échelle présentée ci-dessus.

![NEAR et far plage d’interaction](images/typography-distance-1000px.jpg)
*plage de contenu à proximité et lointain interaction*

### <a name="the-minimum-legible-font-size"></a>La taille de police lisibles minimale
| Distance | Angle de visualisation | Hauteur du texte | Taille de police |
|---------|---------|---------|---------|
| 45 centimètres (distance manipulation directe) | 0.4°-0.5° | 3.14 – 3.9 mm | 8.9 – 11.13pt |
| 2m | 0.35°-0.4° | 12.21 – 13.97 mm | 34.63-39.58pt |


### <a name="the-comfortably-legible-font-size"></a>La taille de police confortablement lisibles
| Distance | Angle de visualisation | Hauteur du texte | Taille de police |
|---------|---------|---------|---------|
| 45 centimètres (distance manipulation directe) | 0.65°-0.8° | 5.1-6.3 mm | 14.47-17.8pt |
| 2m | 0.6°-0.75° | 20,9-26,2 mm | 59.4-74.2pt |

Segoe UI (la police par défaut pour Windows) fonctionne bien dans la plupart des cas. Toutefois, évitez d’utiliser les familles de polices clair light ou semi de petite taille dans la mesure où les traits verticaux minces seront vibration et cela dégradera la lisibilité. Polices modernes avec suffisamment épaisseur du trait fonctionnent bien. Par exemple, Helvetica et Arial rechercher exceptionnelles et sont très lisible en HoloLens avec des poids réguliers ou en gras.


![Angle d’affichage](images/Text_In_Unity_ViewingAngle.jpg)
*affichage hauteur distance et angle de texte*

## <a name="sharp-text-rendering-quality-with-proper-dimension"></a>Précise la qualité de rendu de texte avec la dimension appropriée

En fonction de ces facteurs d’échelle, nous avons créé [prefabs de texte avec le texte de l’interface utilisateur et le maillage de texte 3D](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Prefabs/Text). Les développeurs peuvent utiliser ces prefabs pour obtenir le texte sharp et taille de police cohérente.

![Précise la qualité de rendu de texte avec la dimension appropriée](images/hug-text-06-1000px.png)<br>
*Précise la qualité de rendu de texte avec la dimension appropriée*

## <a name="shader-with-occlusion-support"></a>Nuanceur avec prise en charge de l’occlusion

Matériau de police par défaut d’Unity ne prend pas en charge l’occlusion. Pour cette raison, vous verrez le texte situé derrière les objets par défaut. Nous avons inclus une simple [nuanceur qui prend en charge de l’occlusion](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Assets/MixedRealityToolkit/StandardAssets/Shaders/Text3DShader.shader). L’image ci-dessous montre le texte des documents de police par défaut (à gauche) et le texte avec occlusion approprié (à droite).

![Nuanceur avec prise en charge de l’occlusion](images/hug-text-07-1000px.png)<br>
*Nuanceur avec prise en charge de l’occlusion*


## <a name="see-also"></a>Voir aussi
* [Préfabriqué de texte dans le MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Prefabs/Text)
* [Typographie](typography.md)

 
