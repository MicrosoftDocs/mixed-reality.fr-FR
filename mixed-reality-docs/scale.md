---
title: Scale
description: L’une des clés pour afficher du contenu qui semble réaliste sous forme holographique est de simuler les statistiques visuelles du monde réel aussi fidèlement que possible.
author: mavitazk
ms.author: mavitazk
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, style, Design
ms.openlocfilehash: f13414bff7d84692e8e87aa2abdcded15627346f
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524118"
---
# <a name="scale"></a>Scale

L’une des clés pour afficher du contenu qui semble réaliste sous forme holographique est de simuler les statistiques visuelles du monde réel aussi fidèlement que possible. Cela signifie qu’il est possible d’incorporer autant de signaux visuels que nous pouvons nous aider (dans le monde réel) à comprendre où se trouvent les objets, quelle est leur taille et à quoi ils servent. L’échelle d’un objet est l’une des plus importantes de ces signaux visuels, ce qui donne à une visionneuse une idée de la taille d’un objet ainsi que des signaux vers son emplacement (en particulier pour les objets qui ont une taille connue). En outre, l’affichage des objets à grande échelle a été considéré comme l’un des principaux éléments de différenciation de la réalité mixte en général, ce qui n’était pas possible dans l’affichage à l’écran.

## <a name="how-to-suggest-the-scale-of-objects-and-environments"></a>Comment suggérer l’échelle des objets et des environnements

Il existe de nombreuses façons de suggérer l’échelle d’un objet, certaines d’entre elles ayant des effets possibles sur d’autres facteurs de perception. La première consiste à afficher simplement des objets à une taille réelle, et à conserver une taille réaliste au fur et à mesure que les utilisateurs se déplacent. Cela signifie que les hologrammes occupent une quantité différente de l’angle visuel d’un utilisateur lorsqu’ils sont plus proches ou plus éloignés, de la même façon que les objets réels.

### <a name="utilize-the-distance-of-objects-as-they-are-presented-to-the-user"></a>Utiliser la distance des objets à mesure qu’ils sont présentés à l’utilisateur

Une méthode courante consiste à utiliser la distance des objets à mesure qu’ils sont présentés à l’utilisateur. Par exemple, considérez la visualisation d’une grande voiture de famille devant l’utilisateur. Si la voiture était directement à l’avant, dans la longueur du bras, elle serait trop grande pour tenir dans le champ de vue de l’utilisateur. Cela oblige l’utilisateur à déplacer son en-tête et son corps pour comprendre l’intégralité de l’objet. Si la voiture a été placée plus loin (dans la pièce), l’utilisateur peut établir un sens de mise à l’échelle en regardant l’intégralité de l’objet dans son champ d’affichage, puis en se déplaçant pour examiner les zones en détail.

[Volvo](https://www.youtube.com/watch?v=DilzwF90vec) a utilisé cette technique pour créer une expérience de salle de présentation pour une nouvelle voiture, en utilisant la mise à l’échelle de la voiture holographique de manière à ce qu’elle soit réaliste et intuitive pour l’utilisateur. L’expérience commence avec un hologramme de la voiture sur une table physique, ce qui permet à l’utilisateur de comprendre la taille totale et la forme du modèle. Plus tard dans l’expérience, la voiture se développe à une plus grande échelle (au-delà de la taille du champ de vision de l’appareil) mais, étant donné que l’utilisateur a déjà acquis une image de référence à partir du modèle le plus petit, il peut naviguer correctement autour des fonctionnalités de la voiture.

![Expérience Volvo Cars pour HoloLens](images/volvo-cars-microsoft-hololens-experience01-640px.jpg)<br>
*Expérience Volvo Cars pour HoloLens*

### <a name="use-holograms-to-modify-the-users-real-space"></a>Utiliser des hologrammes pour modifier l’espace réel de l’utilisateur

Une autre méthode consiste à utiliser des hologrammes pour modifier l’espace réel de l’utilisateur, en remplaçant les murs ou les plafonds existants par des environnements ou en ajoutant des «trous» ou des «fenêtres», ce qui permet aux objets de taille supérieure de passer apparemment à l’espace physique. Par exemple, une grande arborescence peut ne pas tenir dans la plupart des salles de vie des utilisateurs, mais en plaçant un ciel virtuel sur leur plafond, l’espace physique se développe dans le virtuel. Cela permet à l’utilisateur de parcourir la base de l’arborescence virtuelle et de recueillir une idée de la façon dont il apparaîtrait dans la vie réelle, puis de voir qu’il s’étend bien au-delà de l’espace physique de la pièce.

[Minecraft](https://minecraft.net/) a développé une expérience de concept à l’aide d’une technique similaire. En ajoutant une fenêtre virtuelle à une surface physique dans une pièce, les objets existants dans la salle sont placés dans le contexte d’un environnement largement plus grand, au-delà des limitations de l’échelle physique de la pièce.

![Expérience Minecraft concept pour HoloLens](images/800px-minecraftwindow-640px.jpg)<br>
*Expérience Minecraft concept pour HoloLens*

## <a name="experimenting-with-scale"></a>Expérimentation avec l’échelle

Dans certains cas, les concepteurs ont expérimenté la modification de l’échelle (en modifiant la taille réelle de l’objet) tout en conservant une position unique de l’objet, afin de rapprocher un objet plus proche ou plus proche d’une visionneuse sans aucun mouvement réel. Cela a été testé dans certains cas comme un moyen de simuler un affichage plus étroit des éléments tout en respectant les limitations de confort potentielles liées à l’affichage du contenu virtuel plus près que la «zone de confort».

Cela peut toutefois créer quelques artefacts possibles dans l’expérience:
* Pour les objets virtuels qui représentent un objet avec une taille «connue» pour la visionneuse, la modification de l’échelle sans changer la position amène aux signaux visuels conflictuels. les yeux peuvent toujours «voir» l’objet à une profondeur en raison des indications vergence (voir le [confort](comfort.md) article pour plus d’informations sur ce point), mais la taille agit comme un signal monoculaire que l’objet peut se rapprocher. Ces signaux conflictuels conduisent à des perceptions confuses. les visionneuses voient souvent que l’objet reste en place (en raison de la profondeur constante), mais augmente rapidement.
* Dans certains cas, la modification de l’échelle est considérée comme un repère «à l’aise», alors que l’objet peut ou non être vu pour changer l’échelle par une visionneuse, mais semble bouger directement vers les yeux de la visionneuse (ce qui peut être une sensation inconfortable).
* Avec les surfaces de comparaison dans le monde réel, ces changements de mise à l’échelle sont parfois considérés comme la modification de la position sur plusieurs axes. les objets peuvent sembler déplacés vers le bas au lieu de se rapprocher (similaire dans une projection 2D d’un mouvement 3D dans certains cas).
* Enfin, pour les objets sans une taille «réelle» connue (par exemple, des formes arbitraires avec des tailles arbitraires, des éléments d’interface utilisateur, etc.), la modification de l’échelle peut agir de façon fonctionnelle pour imiter les modifications de distance: les visionneuses n’ont pas autant de signaux descendants préexistants pour comprenez la taille réelle de l’objet ou son emplacement. l’échelle peut donc être traitée comme un signal plus important.

## <a name="see-also"></a>Voir aussi
* [Couleurs, éclairage et matériaux](color,-light-and-materials.md)
* [Typographie](typography.md)
* [Conception du son spatial](spatial-sound-design.md)
