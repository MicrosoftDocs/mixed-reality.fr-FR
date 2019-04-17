---
title: Texte dans Unity
description: 'Pour afficher du texte dans Unity, il existe deux types de composants de texte que vous pouvez utiliser : texte d’interface utilisateur et le maillage de texte 3D.'
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, des contrôles, police, typographie, l’interface utilisateur, l’expérience utilisateur
ms.openlocfilehash: 02f282ab80a44190d21d2dadefeb7a624c862d04
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596364"
---
# <a name="text-in-unity"></a>Texte dans Unity

Texte est un des composants plus importants dans les applications HOLOGRAPHIQUE. Pour afficher du texte dans Unity, il existe deux types de composants de texte que vous pouvez utiliser : texte d’interface utilisateur et le maillage de texte 3D. Par défaut, ils floues et sont trop volumineux. Vous devez modifier quelques variables pour obtenir sharp, qualité de texte qui a une taille gérable dans HoloLens. En appliquant un facteur d’échelle pour obtenir des dimensions correctes lorsque vous utilisez le texte de l’interface utilisateur et les composants de texte de maillage 3D, vous pouvez obtenir une meilleure qualité de rendu.

![Comment obtenir le texte sharp et magnifiques](images/hug-text-02-640px.png)<br>
*Texte par défaut floue dans Unity*

## <a name="working-with-fonts-in-unity"></a>Utilisation des polices dans Unity

Unity suppose que tous les nouveaux éléments ajoutés à une scène sont 1 unité de Unity dans la taille ou d’échelle de transformation de 100 %, ce qui se traduit par environ 1 mètre sur HoloLens. Dans le cas des polices, la zone englobante pour un TextMesh 3D est fourni par défaut à environ 1 mètre en hauteur.

![Utilisation des polices dans Unity](images/640px-hug-text-03.png)<br>
*Texte de Unity par défaut occupe 1 unité de Unity qui est de 1 mètre*

<br>
La plupart des concepteurs visuels utilisent des points pour définir des tailles de police dans le monde réel. Il existe environ 2835 (2,834.645666399962) points dans 1 mètre. En fonction de la conversion point système 1 mètre et par défaut de maillage texte taille de police 13 d’Unity, les mathématiques simples de 13 divisé par 2835 equals 0.0046 (0.004586111116 pour être exact) fournit une bonne évolutivité standard pour commencer (Certains voudraient arrondir à 0,005). Mise à l’échelle de l’élément textuel ou le conteneur à ces valeurs offrira non seulement pour la conversion de 1:1 de police tailles dans un programme de conception, mais fournit également une norme, donc vous pouvez maintenir la cohérence de votre application ou votre jeu.

![Unity 3D texte de maillage avec des tailles de police](images/hug-text-05-1000px.png)<br>
*Unity 3D texte de maillage avec des valeurs optimisés*

<br>
Lorsque vous ajoutez un élément de texte en fonction de l’interface utilisateur ou de la zone de dessin à une scène, les différences de taille est toujours supérieure. Les différences dans les deux tailles est environ 1000 %, ce qui pourrait apporter le facteur d’échelle pour l’interface utilisateur en fonction des composants de texte à 0.00046 (0.0004586111116 pour être exact) ou 0,0005 pour la valeur arrondie.

![Texte de l’interface utilisateur de Unity avec différents pixels dynamiques par les valeurs d’unité](images/hug-text-04-1000px.png)<br>
*Texte de l’interface utilisateur de Unity avec valeurs optimisées*

<br>

>[!NOTE]
>La valeur par défaut de toutes les polices peut-être être affectée par la taille de texture de cette police ou la façon dont la police a été importée dans Unity. Ces tests ont été effectuées en fonction de la police Arial par défaut dans Unity, ainsi que d’une autre police importée.

## <a name="sharp-text-rendering-quality-with-proper-dimension"></a>Précise la qualité de rendu de texte avec la dimension appropriée

En fonction de ces facteurs d’échelle, nous avons créé [deux prefabs - texte d’interface utilisateur et le maillage de texte 3D](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/UX/Prefabs). Les développeurs peuvent utiliser ces prefabs pour obtenir le texte sharp et taille de police cohérente.

![Précise la qualité de rendu de texte avec la dimension appropriée](images/hug-text-06-1000px.png)<br>
*Précise la qualité de rendu de texte avec la dimension appropriée*

## <a name="shader-with-occlusion-support"></a>Nuanceur avec prise en charge de l’occlusion

Matériau de police par défaut d’Unity ne prend pas en charge l’occlusion. Pour cette raison, vous verrez le texte situé derrière les objets par défaut. Nous avons inclus une simple [nuanceur qui prend en charge de l’occlusion](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/UX/Shaders). L’image ci-dessous montre le texte des documents de police par défaut (à gauche) et le texte avec occlusion approprié (à droite).

![Nuanceur avec prise en charge de l’occlusion](images/hug-text-07-1000px.png)<br>
*Nuanceur avec prise en charge de l’occlusion*

## <a name="recommended-type-size"></a>Taille du type recommandée

Comme vous pouvez l’imaginer, les tailles de type que nous utilisons sur un PC ou une tablette (en général entre 12 – 32 points) Examinez relativement petites une distance de 2 mètres. Il dépend des caractéristiques de chaque police, mais en général la taille minimale recommandée pour une meilleure lisibilité sans vibration de trait est autour de 30pt, selon le facteur d’échelle présentée ci-dessus. Si votre application est censée être utilisée à distance plus proche, plus petites tailles de type peut être utilisés. Pour la sélection de la police Segoe UI (la police par défaut pour Windows) fonctionne bien dans la plupart des cas. Toutefois, évitez d’utiliser des polices claires light ou semi pour les tailles de type sous 42pt dans la mesure où les traits verticaux minces seront vibration et cela dégradera la lisibilité. Polices modernes avec suffisamment épaisseur du trait fonctionnent bien. Par exemple, Helvetica et Arial rechercher exceptionnelles et sont très lisible en HoloLens avec des poids réguliers ou en gras.

![Taille du type recommandée](images/hug-text-08-1000px.png)<br>
*Exemple de type de démarrage*

## <a name="see-also"></a>Voir aussi
* [Préfabriqué de texte dans le MixedRealityToolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/UX/Prefabs)
* [Scène et la disposition de texte d’exemple prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX/Scenes)
* [Typographie](typography.md)

 
