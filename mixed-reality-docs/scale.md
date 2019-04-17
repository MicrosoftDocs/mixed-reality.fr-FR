---
title: Scale
description: Une clé à l’affichage de contenu qui recherche réaliste sous forme HOLOGRAPHIQUE consiste à imiter les statistiques visual du monde réel aussi fidèlement que possible.
author: mavitazk
ms.author: mavitazk
ms.date: 03/21/2018
ms.topic: article
keywords: Conception de Windows Mixed Reality, Style,
ms.openlocfilehash: f13414bff7d84692e8e87aa2abdcded15627346f
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593791"
---
# <a name="scale"></a>Scale

Une clé à l’affichage de contenu qui recherche réaliste sous forme HOLOGRAPHIQUE consiste à imiter les statistiques visual du monde réel aussi fidèlement que possible. Cela signifie incorporant des signaux visuels autant que possible qui nous (dans le monde réel) aident à comprendre où les objets sont, la taille qu’ils sont, et qu’ils sont composés de. La mise à l’échelle d’un objet est une des plus importantes de ces signaux visuels, ce qui donne une visionneuse une idée de la taille d’un objet, ainsi que des signaux à son emplacement (en particulier pour les objets qui ont une taille connue). En outre, affichage des objets à l’échelle réelle est apparue comme un des facteurs de différenciation clé expérience une réalité mixte en général – quelque chose qui n’a pas été possible sur l’écran d’affichage précédemment.

## <a name="how-to-suggest-the-scale-of-objects-and-environments"></a>Comment proposer la mise à l’échelle des objets et des environnements

Il existe de nombreuses façons pour suggérer l’échelle d’un objet, dont certaines ont des effets possibles sur d’autres facteurs perceptible. La clé est simplement afficher les objets à une taille « réelle » et la maintenance de cette taille réaliste que les utilisateurs se déplacent. Cela signifie hologrammes peut prendre jusqu'à une quantité différente de l’angle de visibilité d’un utilisateur d’un utilisateur de leur proche ou plus loin, la même manière que des objets réels.

### <a name="utilize-the-distance-of-objects-as-they-are-presented-to-the-user"></a>Utiliser la distance d’objets, elles sont présentées à l’utilisateur

Une méthode courante consiste à utiliser la distance d’objets comme elles sont présentées à l’utilisateur. Par exemple, considérez la visualisation d’une voiture grande famille devant l’utilisateur. Si la voiture ont été directement placé devant, dans la longueur d’arm, il serait trop grande pour tenir dans le champ de vue utilisateur. Cela nécessiterait l’utilisateur de déplacer leur tête et du corps de comprendre l’intégralité de l’objet. Si la voiture ont été placée plus absent (à travers la pièce), l’utilisateur peut établir une idée de la mise à l’échelle en visualisant l’intégralité de l’objet dans leur champ de vision, puis vers eux-mêmes plus près à inspecter les zones en détail.

[Volvo](https://www.youtube.com/watch?v=DilzwF90vec) cette technique permet de créer une expérience de la salle d’exposition pour une nouvelle voiture, en utilisant la mise à l’échelle de la voiture holographique d’une manière qui senti réaliste et intuitive pour l’utilisateur. L’expérience commence par un hologramme de la voiture sur une table physique, en autorisant l’utilisateur à comprendre la taille totale et la forme du modèle. Plus loin dans l’expérience, la voiture se développe en une plus grande échelle (au-delà de la taille du champ de vision de l’appareil), mais, étant donné que l’utilisateur a déjà acquis un cadre de référence du modèle plus petits, ils peuvent accéder correctement sur les fonctionnalités de la voiture.

![Expérience Volvo voitures pour HoloLens](images/volvo-cars-microsoft-hololens-experience01-640px.jpg)<br>
*Expérience Volvo voitures pour HoloLens*

### <a name="use-holograms-to-modify-the-users-real-space"></a>Hologrammes permet de modifier l’espace réel de l’utilisateur

Une autre méthode consiste à utiliser des hologrammes pour modifier l’espace réel de l’utilisateur, en remplaçant les murs ou des plafonds existant avec les environnements ou de l’ajout de « trous » ou « windows », permettant aux objets surdimensionnés à apparemment « break-through » l’espace physique. Par exemple, une grande arborescence ne pouvant pas tenir dans les salons la plupart des utilisateurs, mais en plaçant un ciel virtuel sur leur plafond, l’espace physique se développe en virtuel. Cela permet à l’utilisateur à parcourir la base de l’arborescence virtuel et de collecter une idée de la mise à l’échelle de comment il aurait apparaissent dans la vie réelle, puis rechercher pour s’étendre bien au-delà de l’espace physique de la salle.

[Minecraft](https://minecraft.net/) développé une expérience de concept à l’aide d’une technique similaire. En ajoutant une fenêtre virtuelle à une surface physique dans une salle, les objets existants dans la salle sont placés dans le contexte d’un environnement bien plus large, au-delà des limites physiques de l’échelle de la salle.

![Expérience de concept de Minecraft pour HoloLens](images/800px-minecraftwindow-640px.jpg)<br>
*Expérience de concept de Minecraft pour HoloLens*

## <a name="experimenting-with-scale"></a>Expérimenter la mise à l’échelle

Dans certains cas, les concepteurs ont expérimenté avec la modification de l’échelle (en modifiant la taille affichée 'vrai' de l’objet) tout en conservant une position unique de l’objet, pour se rapprocher d’un objet bien plus proche ou à la suite d’une visionneuse sans aucun déplacement réel. Cela a été testé dans certains cas comme un moyen de simuler des gros plan sur Affichage d’éléments tout en respectant encore des limitations de confort potentiels d’affichage de contenu virtuel plus près la « zone de confort » suggère.

Cela peut créer quelques artefacts sont possibles dans l’expérience toutefois :
* Pour des objets virtuels qui représentent un objet avec une taille « connu » dans l’Observateur, modification de l’échelle sans modifier la position des prospects pour les signaux visuels en conflit – les yeux peuvent néanmoins « voir » l’objet à certains profondeur en raison des signaux de vergence (voir la [confort ](comfort.md) article pour en savoir plus sur ce), mais la taille se comporte comme une file d’attente monoculaire que l’objet peut être plus en détail. Ces signaux en conflit entraîner perceptions confondues – visionneuses voir souvent l’objet en tant que de rester en place (en raison de la file d’attente profondeur constante), mais augmente rapidement.
* Dans certains cas, modification de la mise à l’échelle est considérée comme une file d’attente « approche » au lieu de cela, où l’objet peut ou ne peut pas se produire pour modifier la mise à l’échelle par une visionneuse, mais ne semble pas être transition directement vers les yeux de (qui peuvent être une sensation désagréable).
* Avec des surfaces de comparaison dans le monde réel, ces modifications de mise à l’échelle sont parfois considérées comme la modification de position le long de plusieurs axes : objets drop inférieure au lieu de déplacer plus proche peuvent sembler (comme dans une projection 2D en 3D du déplacement de dans certains cas).
* Enfin, pour les objets sans une taille connue « monde réel » (formes arbitraires par exemple, avec des tailles arbitraires, les éléments d’interface utilisateur, etc.), modifier l’échelle peut agir fonctionnellement comme un moyen pour imiter les modifications apportées à distance – visionneuses par n’ont pas autant des piles de haut en bas préexistants auquel comprendre la taille réelle de l’objet ou l’emplacement, afin de l’échelle peut être traitée comme une file d’attente plus important.

## <a name="see-also"></a>Voir aussi
* [Couleur, clair et supports](color,-light-and-materials.md)
* [Typographie](typography.md)
* [Sonorisation spatiale](spatial-sound-design.md)
