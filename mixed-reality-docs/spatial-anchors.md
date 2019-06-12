---
title: Ancres spatiales
description: Bonnes pratiques pour utiliser des ancres spatiales afin d’afficher des hologrammes stables.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
ms.localizationpriority: high
keywords: système de coordonnées, système de coordonnées spatiales, échelle mondiale, monde, échelle, position, orientation, ancre, ancre spatiale, verrouillage au monde, verrouillé au monde, partage
ms.openlocfilehash: 16165194d040ad22f7885897eddcc65cf9dcaec3
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "65730858"
---
# <a name="spatial-anchors"></a>Ancres spatiales

Une ancre spatiale représente dans le monde un point important dont le système doit effectuer le suivi au fil du temps. Chaque ancre a un [système de coordonnées](coordinate-systems.md) qui s’ajuste en fonction des besoins, par rapport à d’autres ancres ou cadres de référence, afin que les hologrammes ancrés demeurent précisément en place.  Le rendu d’un hologramme dans le système de coordonnées d’une ancre vous donne le positionnement le plus précis de cet hologramme à un moment donné. Cette opération nécessite quelques ajustements réguliers de la position de l’hologramme, car le système le replace en permanence par rapport au monde réel.

Vous pouvez également conserver et partager des ancres spatiales dans les sessions d’application et dans les appareils :
* En enregistrant les ancres spatiales locales sur le disque et en les chargeant ultérieurement, votre application peut déterminer le même emplacement dans le monde réel entre plusieurs sessions d’application sur un même appareil HoloLens.
* En utilisant <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> pour créer une ancre cloud, votre application peut partager une ancre spatiale entre plusieurs appareils HoloLens, iOS et Android. Quand chaque appareil affiche un hologramme à l’aide de la même ancre spatiale, tous les utilisateurs voient l’hologramme au même endroit dans le monde réel.  Cette technique autorise les expériences partagées en temps réel.
* Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> pour la persistance asynchrone des hologrammes sur les appareils HoloLens, iOS et Android.  En partageant une ancre spatiale cloud durable, plusieurs appareils peuvent observer le même hologramme conservé au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.

Pour les expériences à l’échelle humaine ou d’une pièce avec des casques de poste de travail attachés qui demeurent dans un rayon de 5 mètres, vous pouvez en général simplement utiliser le [cadre de référence de la scène](coordinate-systems.md#stage-frame-of-reference) au lieu d’ancres spatiales, disposant ainsi d’un seul système de coordonnées pour le rendu de tout le contenu. Toutefois, si votre application doit permettre aux utilisateurs d’évoluer au-delà de 5 mètres sur HoloLens, éventuellement sur un étage entier d’un bâtiment, il est nécessaire que les ancres spatiales assurent la stabilité du contenu.

Bien que les ancres spatiales soient idéales pour les hologrammes qui doivent rester fixes dans le monde, une fois placée, une ancre ne peut pas être déplacée. Il existe des alternatives aux ancres qui conviennent mieux pour les hologrammes dynamiques devant accompagner l’utilisateur. Il est préférable de positionner les hologrammes dynamiques à l’aide d’un cadre de référence stationnaire (la base des coordonnées mondiales d’Unity) ou d’un cadre de référence attaché.

## <a name="best-practices"></a>Meilleures pratiques

Les recommandations ci-après sur les ancres spatiales vous aident à afficher des hologrammes stables qui suivent avec précision le monde réel.

### <a name="create-spatial-anchors-where-users-place-them"></a>Créer les ancres spatiales là où les utilisateurs les placent

La plupart du temps, ce sont les utilisateurs qui doivent explicitement placer les ancres spatiales.

Par exemple, sur HoloLens, une application peut croiser le rayon du [pointage du regard](gaze.md) de l’utilisateur avec le maillage du [mappage spatial](spatial-mapping.md) pour permettre à l’utilisateur de décider où placer un hologramme. Quand l’utilisateur appuie pour placer cet hologramme, créez une ancre spatiale au point d’intersection, puis placez l’hologramme à l’origine du système de coordonnées de cette ancre.

La création d’ancres spatiales locales est facile et efficace, et si plusieurs ancres peuvent partager leurs données de capteur sous-jacentes, le système consolide leurs données internes. Vous devez généralement créer une ancre spatiale locale pour chaque hologramme qu’un utilisateur place explicitement, sauf dans les cas décrits ci-dessous, tels que les groupes d’hologrammes rigides.

### <a name="always-render-anchored-holograms-within-3-meters-of-their-anchor"></a>Toujours afficher les hologrammes ancrés à une distance maximale de 3 mètres de leur ancre

Les ancres spatiales stabilisent leur système de coordonnées près de leur origine. Si vous affichez des hologrammes à une distance supérieure à environ 3 mètres de cette origine, ces hologrammes peuvent rencontrer des erreurs de positionnement notables par rapport à la distance qui les sépare de cette origine, en raison d’effets de bras de levier. Cela fonctionne si l’utilisateur se tient près de l’ancre, dans la mesure où l’hologramme est également loin de l’utilisateur ; dans ce cas, l’erreur angulaire de l’hologramme distant est petite. Toutefois, si l’utilisateur se déplace jusqu’à l’hologramme distant, ce dernier devient grand dans son champ de vision, rendant assez flagrants les effets de bras de levier à partir de l’origine de l’ancre distante.

### <a name="group-holograms-that-should-form-a-rigid-cluster"></a>Regrouper les hologrammes qui doivent former un cluster rigide

Plusieurs hologrammes peuvent partager la même ancre spatiale si l’application s’attend à ce qu’ils maintiennent des relations fixes entre eux.

Par exemple, si vous animez un système solaire holographique dans une pièce, il est préférable de lier tous les objets du système solaire à une seule ancre au centre, afin qu’ils se déplacent sans heurts les uns par rapport aux autres. Dans ce cas, c’est le système solaire dans sa globalité qui est ancré, même si ses composants se déplacent dynamiquement autour de l’ancre.

Le plus important ici pour maintenir la stabilité des hologrammes est de suivre la règle des 3 mètres évoquée plus haut.

### <a name="render-highly-dynamic-holograms-using-the-stationary-frame-of-reference-instead-of-a-local-spatial-anchor"></a>Afficher les hologrammes hautement dynamiques à l’aide du cadre de référence stationnaire au lieu d’une ancre spatiale locale

Si vous avez un hologramme hautement dynamique, tel qu’un personnage marchant dans la pièce ou une interface utilisateur flottante affichée au mur à proximité de l’utilisateur, il convient de délaisser les ancres spatiales locales et d’afficher ces hologrammes directement dans le système de coordonnées fourni par le [cadre de référence stationnaire](coordinate-systems.md#stationary-frame-of-reference) (par exemple, dans Unity, vous placez les hologrammes directement en utilisant des coordonnées mondiales sans composant WorldAnchor). Les hologrammes dans un cadre stationnaire de référence peuvent dériver quand l’utilisateur est loin d’eux, mais cela est moins susceptible d’être perceptible dans le cas des hologrammes dynamiques : l’hologramme bouge constamment ou son mouvement le maintient constamment près de l’utilisateur, le phénomène de dérive étant alors réduit au minimum.

Un cas intéressant d’hologrammes dynamiques est un objet qui s’anime d’un système de coordonnées ancré à un autre. Par exemple, imaginons deux châteaux distants de 10 mètres, chacun sur sa propre ancre spatiale, l’un d’eux tirant un boulet de canon en direction de l’autre. Au moment où le boulet de canon est tiré, vous pouvez l’afficher à l’emplacement approprié dans le cadre stationnaire de référence, pour le faire coïncider avec le canon dans le système de coordonnées ancré du premier château. Il peut ensuite suivre sa trajectoire dans le cadre stationnaire de référence quand il parcourt 10 mètres dans l’air. Quand le boulet de canon atteint l’autre château, vous pouvez choisir de le déplacer dans le système de coordonnées ancré du second château pour permettre des calculs de propriétés physiques impliquant le corps rigide de ce château.

Si vous partagez un hologramme hautement dynamique entre plusieurs appareils, vous devez choisir une ancre spatiale cloud en guise de parent de ces derniers, car les cadres stationnaires de référence ne peuvent pas être partagés entre plusieurs appareils.  Toutefois, dans ce cas, vous devez vous assurer que l’hologramme dynamique ou les appareils qui l’affichent demeurent dans un rayon de 3 mètres de l’ancre afin d’assurer la stabilité de l’hologramme sur tous les appareils.

### <a name="avoid-creating-a-grid-of-spatial-anchors"></a>Éviter de créer une grille d’ancres spatiales

Vous pouvez être tenté de faire en sorte que votre application dépose une grille régulière d’ancres spatiales quand l’utilisateur se déplace, faisant passer les objets dynamiques d’une ancre à l’autre au fil de leur déplacement. Toutefois, cela implique beaucoup de gestion pour votre application, sans qu’elle bénéficie de la profondeur des données de capteur que le système lui-même tient à jour en interne. Dans ce cas, pour obtenir de meilleurs résultats avec moins d’efforts, il convient généralement de placer vos hologrammes dans le cadre stationnaire de référence, comme décrit dans la section ci-dessus.

Quand vous pré-positionnez un ensemble d’ancres spatiales cloud autour d’un espace statique, envisagez de placer les ancres spatiales aux emplacements des hologrammes clés que l’utilisateur est susceptible de rencontrer d’après le principe évoqué plus haut, plutôt que de créer une grille d’ancres arbitraire.  Ainsi, vous obtenez une stabilité maximale pour ces hologrammes clés.

### <a name="release-local-spatial-anchors-you-no-longer-need"></a>Libérer les ancres spatiales locales dont vous n’avez plus besoin

Quand une ancre spatiale locale est active, le système privilégie la conservation à proximité des données de capteur qui sont proches de cette ancre. Si vous n’utilisez plus une ancre spatiale, arrêtez d’accéder à son système de coordonnées. Ainsi, ses données de capteur sous-jacentes peuvent être supprimées si nécessaire.

Cela est particulièrement important pour les ancres locales que vous avez conservées dans le magasin des ancres spatiales. Les données de capteur derrière ces ancres sont définitivement conservées à proximité pour permettre à votre application de trouver ces ancres dans de futures sessions d’application, ce qui réduit l’espace disponible pour le suivi d’autres ancres. Ne conservez que les ancres locales que vous devez rechercher à nouveau dans des sessions ultérieures et supprimez-les du magasin quand elles ne sont plus significatives pour l’utilisateur.

Pour les ancres spatiales cloud, votre stockage peut évoluer en fonction de votre scénario.  Vous pouvez stocker autant d’ancres cloud que nécessaire et ne les libérer que quand vous savez que vos utilisateurs n’ont plus besoin de rechercher des hologrammes au niveau de ces ancres.

## <a name="see-also"></a>Voir également
* [Systèmes de coordonnées](coordinate-systems.md)
* [Expériences partagées dans Mixed Reality](shared-experiences-in-mixed-reality.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>
* [Persistance dans Unity](persistence-in-unity.md)
* [Ancres spatiales dans DirectX](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-spatial-anchors)
* [Étude de cas - Voir à travers vos objets](case-study-looking-through-holes-in-your-reality.md)
