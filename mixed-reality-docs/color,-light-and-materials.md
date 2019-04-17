---
title: Couleur, clair et supports
description: Conception de contenu pour la réalité mixte nécessite une attention particulière de couleur, d’éclairage et de documentations pour chacune des ressources visual utilisés dans votre expérience.
author: mavitazk
ms.author: pinkb
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, de couleur, de lumière, de matériaux
ms.openlocfilehash: 3f8ee8edfe4cbbaf8a55b3c4a9125f752823be9c
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594882"
---
# <a name="color-light-and-materials"></a>Couleur, clair et supports

Conception de contenu pour la réalité mixte nécessite une attention particulière de couleur, d’éclairage et de documentations pour chacune des ressources visual utilisés dans votre expérience. Ces décisions peuvent être pour à des fins esthétiques, comme à l’aide de la lumière et matériel pour définir le ton d’un environnement immersif et le point de vue fonctionnel, comme à l’aide de couleurs frappante pour avertir les utilisateurs d’une action imminente. Chacune de ces décisions doit être comparée aux opportunités et les contraintes de l’appareil de cible de votre expérience.

Voici les instructions spécifiques à des ressources de rendu sur des casques IMMERSIFS et HOLOGRAPHIQUES. Nombre d'entre elles sont étroitement liées à d’autres zones techniques et vous trouverez une liste de sujets connexes dans le [Voir aussi](color,-light-and-materials.md#see-also) section à la fin de cet article.

## <a name="rendering-on-immersive-vs-holographic-devices"></a>Rendu sur immersives et appareils HOLOGRAPHIQUE

Le contenu restitué dans des casques IMMERSIFS apparaîtra visuellement différent par rapport à du contenu dans les casques HOLOGRAPHIQUE. Alors que des casques IMMERSIFS généralement afficher le contenu autant que vous attendez sur un écran 2D, casques HOLOGRAPHIQUE comme l’utilisation de HoloLens RVB séquentiel de couleur, transparente affiche rendus hologrammes.

Toujours suivre le temps de tester vos expériences HOLOGRAPHIQUE dans un casque HOLOGRAPHIQUE. L’apparence du contenu, même s’il est conçu spécialement pour les appareils HOLOGRAPHIQUE, diffèrent comme indiqué sur des moniteurs secondaires, instantanés et dans la vue du spectateur. N’oubliez pas de porter les expériences avec un périphérique, le test de l’éclairage de hologrammes et en observant à partir de tous les côtés (ainsi que d’au-dessus et au-dessous) mode de rendu de votre contenu. Veillez à tester dans la plage de paramètres de luminosité sur l’appareil, car il est peu probable que tous les utilisateurs partagent une valeur par défaut, ainsi que d’un ensemble varié de conditions d’éclairage.

## <a name="fundamentals-of-rendering-on-holographic-devices"></a>Principes de base du rendu sur les appareils HOLOGRAPHIQUE
* **Appareils HOLOGRAPHIQUE ont affiche additifs** – hologrammes sont créées en ajoutant la lumière à la lumière à partir de la réalité – blanche apparaît lumineux, tout en noir apparaît transparent.
* **Impact des couleurs varie en fonction de l’environnement utilisateur** : il existe de nombreuses conditions d’éclairage diverses dans la salle de l’utilisateur. Créer du contenu avec des niveaux appropriés de contraste à plus de clarté.
* **Évitez d’éclairage dynamique** – hologrammes sont allumés uniformément dans les expériences HOLOGRAPHIQUE sont plus efficaces. À l’aide d’éclairage dynamique avancé dépassera probablement les fonctionnalités de nuanceurs mobiles.

## <a name="designing-with-color"></a>Conception de couleur

En raison de la nature des écrans additifs, certaines couleurs peuvent apparaître différents sur les écrans HOLOGRAPHIQUE. Certaines couleurs seront affiche dans les environnements d’éclairage, tandis que d’autres utilisateurs apparaît sous la forme moins qui risquent d’affecter. Les couleurs ont tendance à reculent en arrière-plan, tandis que les couleurs à chaud accéder au premier plan. Considérez les facteurs comme la couleur que vous explorez dans vos expériences :
* **Gamme** -HoloLens bénéficie d’une gamme « large » de couleur, conceptuellement semblable à Adobe RVB. Par conséquent, certaines couleurs peuvent présenter des différentes qualités et la représentation sous forme de l’appareil.
* **Gamma** -luminosité et contraste de l’image rendue varient entre les appareils immersives et HOLOGRAPHIQUE. Ces différences de périphériques apparaissent souvent pour rendre les zones sombres de couleur et les ombres, plus ou moins claires.
* **Séparation des couleurs** -également appelé « répartition couleur » ou « frange de couleur », séparation de couleur se produit généralement avec déplacement hologrammes (y compris le curseur) quand un utilisateur effectue le suivi des objets avec leurs yeux.
* **Couleur d’uniformité** -généralement hologrammes sont rendus suffisamment lumineux afin qu’elles conservent l’uniformité de couleur, quel que soit l’arrière-plan. Grandes zones peuvent devenir nette. Évitez les grandes régions de lumineuse, de couleur unie.
* **Rendu des couleurs claires** -blanc apparaît très clair et doivent être utilisé avec parcimonie. Pour la plupart des cas, envisagez une valeur du blanc autour de R 235 G 235 B 235. Grandes zones claires peuvent provoquer des maux de l’utilisateur.

**Rendu des couleurs sombres**

En raison de la nature des écrans additifs, les couleurs foncées semblent transparents. Un objet noir uni s’affiche ne diffère pas du monde réel. Canal Alpha de voir ci-dessous. Pour donner l’apparence de « noir » essayez une valeur RVB grise foncée très telles que 16,16,16.

![Normal et large gamme de couleurs](images/640px-widegamut.png)<br>
*Normal et large gamme de couleurs*

## <a name="technical-considerations"></a>Considérations techniques
* **Alias** -être tenir compte de l’utilisation d’alias, en escalier ou « étapes d’escalier » où le bord de la géométrie d’un hologramme répond à la réalité. À l’aide de textures avec beaucoup de détails peut aggraver cet effet. Textures doivent être mappés et le filtrage activé. Envisagez de fondu les bords de hologrammes ou l’ajout d’une texture qui crée une bordure noire edge autour des objets. Évitez de géométrie mince lorsque cela est possible.
* **Canal alpha** -vous devez effacer votre canal alpha entièrement transparents pour toutes les parties où vous ne sont pas rendu un hologramme. En laissant les prospects undefined alphabétiques pour les artefacts visuels lors de la création d’images/vidéos à partir de l’appareil ou avec la vue du spectateur.
* **Texture adoucissement** : étant donné que la lumière est additif dans les affichages HOLOGRAPHIQUE, il est préférable d’éviter les grandes régions de lumineuse, de couleur unie comme ils ne produisent souvent pas l’effet escompté visual.

## <a name="storytelling-with-light-and-color"></a>Narration avec la lumière et la couleur

Lumière et la couleur peuvent aider à rendre votre hologrammes apparaissent plus naturellement dans d’un utilisateur environnement ainsi qu’offrent des conseils et d’aide pour l’utilisateur. Pour des expériences HOLOGRAPHIQUE, considérez les facteurs que vous explorez l’éclairage et la couleur :
* **Vignettage** -un effet de « vignette » pour obscurcir les matériaux peut aider à concentrer l’attention des utilisateurs sur le centre de champ de vue. Cet effet assombrit matériel de l’hologramme à certains radius à partir de vecteur du pointage de regard de l’utilisateur. Notez que cela est également efficace lorsque l’utilisateur consulte hologrammes à partir d’un angle oblique ou oeil.
* **Accent** -attirer l’attention sur des objets ou des points d’interaction en mettant en contraste des couleurs, luminosité et d’éclairage. Pour une étude plus détaillée de méthodes d’éclairage dans leur interprétation, consultez [cinéma Pixel - un éclairage approche pour les graphiques de l’ordinateur](http://media.siggraph.org/education/cgsource/Archive/ConfereceCourses/S96/course30.pdf).

![Utilisation de couleur pour indiquer l’importance pour les éléments de narration, présentées dans une scène de Fragments.](images/640px-fragments.jpg)<br>
*Utilisation des couleurs pour afficher l’importance pour les éléments de narration, illustré ici dans une scène à partir de [Fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8).*

## <a name="see-also"></a>Voir aussi
* [Séparation des couleurs](hologram-stability.md#color-separation)
* [Hologrammes](hologram.md)
* [Langage de Microsoft Design - couleur](https://www.microsoft.com/design/color)
* [Plateforme Windows universelle - couleur](https://docs.microsoft.com/windows/uwp/style/color)
