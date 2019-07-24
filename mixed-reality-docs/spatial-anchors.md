---
title: Ancres spatiales
description: Bonnes pratiques pour utiliser des ancres spatiales afin d’afficher des hologrammes stables.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: système de coordonnées, système de coordonnées spatiales, échelle mondiale, monde, échelle, position, orientation, ancre, ancre spatiale, verrouillage au monde, verrouillé au monde, partage
ms.openlocfilehash: 27b1dcd86c7edba176ca54840bdd27550736a16d
ms.sourcegitcommit: b0b1b8e1182cce93929d409706cdaa99ff24fdee
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68387737"
---
# <a name="spatial-anchors"></a>Ancres spatiales

Une ancre spatiale représente un point important dans le monde que le système effectue le suivi au fil du temps. Chaque ancre a un [système de coordonnées](coordinate-systems.md) qui s’ajuste en fonction des besoins, par rapport à d’autres ancres ou cadres de référence, afin que les hologrammes ancrés demeurent précisément en place.  Le rendu d’un hologramme dans le système de coordonnées d’une ancre vous donne le positionnement le plus précis de cet hologramme à un moment donné. Il s’agit du coût des petits ajustements au fil du temps jusqu’à la position de l’hologramme, car le système le replace continuellement en place par rapport au monde réel.

Vous pouvez également conserver et partager des ancres spatiales entre les sessions d’application et entre les appareils:
* En enregistrant les ancres spatiales locales sur le disque et en les chargeant ultérieurement, votre application peut calculer le même emplacement dans le monde réel sur plusieurs sessions d’application sur une même HoloLens.
* En utilisant des <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres spatiales Azure</a> pour créer une ancre Cloud, votre application peut partager une ancre spatiale sur plusieurs appareils HoloLens, iOS et Android. Si chaque appareil effectue le rendu d’un hologramme à l’aide de la même ancre spatiale, les utilisateurs voient l’hologramme apparaître au même endroit dans le monde réel. Cette technique autorise les expériences partagées en temps réel.
* Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> pour la persistance asynchrone des hologrammes sur les appareils HoloLens, iOS et Android. En partageant une ancre spatiale cloud durable, plusieurs appareils peuvent observer le même hologramme conservé au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.

Pour les expériences de mise à l’échelle à l’échelle ou en chambre pour les casques de bureau attachés qui restent dans un diamètre de 5 mètres, vous pouvez généralement utiliser le [cadre de la phase de référence](coordinate-systems.md#stage-frame-of-reference) au lieu des ancres spatiales, ce qui vous permet de disposer d’un système de coordonnées unique dans lequel restituer tout le contenu. Toutefois, si votre application a l’intention de laisser les utilisateurs se déplacer au-delà de 5 mètres dans HoloLens, peut-être en opérant tout au long d’un étage, vous aurez besoin d’ancres spatiales pour garantir la stabilité du contenu.

Bien que les ancres spatiales soient idéales pour les hologrammes qui doivent rester fixes dans le monde, une fois placée, une ancre ne peut pas être déplacée. Il existe des alternatives aux ancres qui sont plus appropriées pour les hologrammes dynamiques qui balisent avec l’utilisateur. Il est préférable de positionner les hologrammes dynamiques à l’aide d’un cadre de référence stationnaire (la base des coordonnées mondiales d’Unity) ou d’un cadre de référence attaché.

## <a name="best-practices"></a>Bonnes pratiques

Les recommandations ci-après sur les ancres spatiales vous aident à afficher des hologrammes stables qui suivent avec précision le monde réel.

### <a name="create-spatial-anchors-where-users-place-them"></a>Créer les ancres spatiales là où les utilisateurs les placent

En règle générale, les utilisateurs sont ceux qui placent explicitement des ancres spatiales.

Par exemple, sur HoloLens, une application peut croiser le point de [regard](gaze.md) de l’utilisateur avec le maillage de [mappage spatial](spatial-mapping.md) pour permettre à l’utilisateur de décider où placer un hologramme. Quand l’utilisateur appuie sur pour placer cet hologramme, créez une ancre spatiale au point d’intersection, puis placez l’hologramme à l’origine du système de coordonnées de cette ancre.

Les ancres spatiales locales sont faciles à créer. Le système consolide ses données internes si plusieurs ancres peuvent partager leurs données de capteur sous-jacentes. En règle générale, vous devez créer une ancre spatiale locale pour chaque hologramme qu’un utilisateur place explicitement, sauf dans les cas présentés ci-dessous, tels que des groupes rigides d’hologrammes.

### <a name="always-render-anchored-holograms-within-3-meters-of-their-anchor"></a>Toujours afficher les hologrammes ancrés à une distance maximale de 3 mètres de leur ancre

Les ancres spatiales stabilisent leur système de coordonnées près de leur origine. Si vous affichez des hologrammes de plus de 3 mètres à partir de cette origine, ces hologrammes peuvent rencontrer des erreurs de position perceptibles proportionnelles à leur distance par rapport à cette origine en raison des effets de levier. Cela fonctionne si l’utilisateur est proche de l’ancre, car l’hologramme est également éloigné de l’utilisateur. En d’autres termes, l’erreur angulaire de l’hologramme distant est faible. Toutefois, si l’utilisateur parcourt Cet hologramme distant, il sera de grande taille dans sa vue, ce qui rendra les effets de levier-ARM de l’origine de l’ancre lointaine très évident.

### <a name="group-holograms-that-should-form-a-rigid-cluster"></a>Regrouper les hologrammes qui doivent former un cluster rigide

Plusieurs hologrammes peuvent partager la même ancre spatiale si l’application s’attend à ce que ces hologrammes maintiennent les relations fixes les unes avec les autres.

Par exemple, si vous animez un système solaire holographique dans une pièce, il est préférable de lier tous les objets du système solaire à une seule ancre au Centre afin qu’ils se déplacent correctement l’un par rapport à l’autre. Dans ce cas, c’est le système solaire dans sa globalité qui est ancré, même si ses composants se déplacent dynamiquement autour de l’ancre.

La principale restriction pour maintenir la stabilité des hologrammes consiste à suivre la règle de 3 mètres ci-dessus.

### <a name="render-highly-dynamic-holograms-using-the-stationary-frame-of-reference-instead-of-a-local-spatial-anchor"></a>Afficher les hologrammes hautement dynamiques à l’aide du cadre de référence stationnaire au lieu d’une ancre spatiale locale

Si vous avez un hologramme très dynamique, tel qu’un personnage qui se trouve autour d’une pièce ou d’une interface utilisateur flottante qui suit le long du mur près de l’utilisateur, il est préférable d’ignorer les ancres spatiales locales et de rendre ces hologrammes directement dans le système de coordonnées fourni par le [ cadre de référence stationnaire](coordinate-systems.md#stationary-frame-of-reference). Pour ce faire, vous devez placer des hologrammes directement en coordonnées universelles sans WorldAnchor. Les hologrammes dans un cadre stationnaire peuvent être dérives lorsque l’utilisateur est éloigné de l’hologramme. Toutefois, cela est moins susceptible d’être perceptible pour les hologrammes dynamiques: l’hologramme se déplace constamment tout de même ou son mouvement le maintient constamment à proximité de l’utilisateur, où la dérive est réduite.

Un cas intéressant d’hologrammes dynamiques est un objet qui s’anime d’un système de coordonnées ancré à un autre. Par exemple, vous pouvez avoir deux mètres de 10 Castles séparés, chacun sur leur propre ancrage spatial avec un Castle déclenchant un Cannonball à l’autre Castle. Au moment où le Cannonball est activé, vous pouvez le rendre à l’emplacement approprié dans le cadre stationnaire de référence pour coïncider avec le Canon dans le système de coordonnées d’ancrage du premier Castle. Il peut ensuite suivre sa trajectoire dans le cadre stationnaire de référence quand il parcourt 10 mètres dans l’air. À mesure que le Cannonball atteint l’autre Castle, vous pouvez choisir de le déplacer dans le second système de coordonnées d’ancrage Castle pour permettre les calculs physiques avec les corps rigides de ce Castle.

Si vous partagez un hologramme hautement dynamique sur des appareils, vous devez choisir une ancre spatiale Cloud pour agir en tant que parent, car les images fixes de référence ne peuvent pas être partagées entre les appareils.  Toutefois, dans ce cas, vous devez vous assurer que l’hologramme dynamique ou les appareils qui l’affichent restent dans le rayon de 3 mètres de l’ancre pour s’assurer que l’hologramme semble stable sur tous les appareils.

### <a name="avoid-creating-a-grid-of-spatial-anchors"></a>Éviter de créer une grille d’ancres spatiales

Vous pouvez être tenté de faire en sorte que votre application supprime une grille normale d’ancres spatiales à mesure que l’utilisateur se déplace, en transférant les objets dynamiques depuis l’ancrage jusqu’au point d’ancrage. Toutefois, cela implique un grand nombre de gestion pour votre application, sans l’avantage des données de capteur profondes que le système lui-même gère en interne. Dans ce cas, vous obtiendrez généralement de meilleurs résultats avec moins d’efforts en plaçant vos hologrammes dans le cadre stationnaire de référence, comme décrit dans la section ci-dessus.
Lors du prépositionnement d’un ensemble d’ancres spatiales Cloud autour d’un espace statique, envisagez de placer les ancres spatiales aux emplacements des hologrammes de clé que l’utilisateur rencontre selon le principe ci-dessus plutôt que de créer une grille arbitraire d’ancres. Ainsi, vous obtenez une stabilité maximale pour ces hologrammes clés.

### <a name="release-local-spatial-anchors-you-no-longer-need"></a>Libérer les ancres spatiales locales dont vous n’avez plus besoin

Lorsqu’une ancre spatiale locale est active, le système hiérarchise la conservation des données de capteur qui se trouvent à proximité de cette ancre. Si vous n’utilisez plus une ancre spatiale, arrêtez d’accéder à son système de coordonnées. Cela permet de supprimer les données de capteur sous-jacentes si nécessaire.

Cela est particulièrement important pour les ancres locales que vous avez conservées dans le magasin des ancres spatiales. Les données de capteur sous-jacentes sont conservées de manière permanente pour permettre à votre application de trouver cette ancre dans les sessions ultérieures, ce qui réduit l’espace disponible pour effectuer le suivi d’autres points d’ancrage. Conservez uniquement les ancres locales que vous devez retrouver dans les sessions ultérieures, et supprimez-les du magasin lorsqu’elles ne sont plus significatives pour l’utilisateur.

Pour les ancres spatiales cloud, votre stockage peut évoluer en fonction de votre scénario. Vous pouvez stocker autant d’ancres Cloud que nécessaire, en les libérant uniquement lorsque vous savez que vos utilisateurs n’auront plus besoin de localiser les hologrammes à ce point d’ancrage.

## <a name="see-also"></a>Voir aussi
* [Systèmes de coordonnées](coordinate-systems.md)
* [Expériences partagées dans Mixed Reality](shared-experiences-in-mixed-reality.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a>
* [Persistance dans Unity](persistence-in-unity.md)
* [Ancres spatiales dans DirectX](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-spatial-anchors)
* [Étude de cas - Voir à travers vos objets](case-study-looking-through-holes-in-your-reality.md)
