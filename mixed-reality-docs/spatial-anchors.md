---
title: Ancres spatiales
description: Meilleures pratiques d’utilisation ancres spatiales pour restituer hologrammes stables.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: système de coordonnées, système de coordonnées spatial, à l’échelle mondiale, monde, mise à l’échelle, position, orientation, ancre, ancre spatiale, persistance world-verrouillé, verrouillage world, partage
ms.openlocfilehash: eb0fae7881f1b6517da57305ef2fa3cb1ed78648
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597128"
---
# <a name="spatial-anchors"></a>Ancres spatiales

Un point d’ancrage spatial représente un point important dans le monde que le système doit effectuer le suivi au fil du temps. Chaque point d’ancrage a un [système de coordonnées](coordinate-systems.md) qui s’ajuste en fonction des besoins, par rapport à d’autres points d’ancrage ou placer des images de référence, afin de garantir que hologrammes ancrés restent précisément dans.  Rendu d’un hologramme dans le système de coordonnées d’un point d’ancrage vous donne le plus précis de positionnement pour cet hologramme à un moment donné. Cela est fourni au prix de petites modifications au fil du temps à la position de l’hologramme, comme le système en permanence son Replace en place par rapport à la réalité.

Vous pouvez également conserver et partager des ancres spatiales sur les sessions d’application et les appareils :
* En enregistrant les ancres spatiales locales sur le disque et le chargement de que les récupérer plus tard, votre application peut examiner le même emplacement dans le monde réel entre plusieurs sessions d’application sur un seul appareil HoloLens.
* À l’aide de <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour créer un point d’ancrage de cloud, votre application peut partager un point d’ancrage spatial entre plusieurs HoloLens, appareils iOS et Android. En demandant à chaque appareil de restituer un hologramme à l’aide de l’ancre spatial même, tous les utilisateurs voient l’hologramme apparaissent au même endroit dans le monde réel.  Ainsi, les expériences partagées en temps réel.
* Vous pouvez également utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour la persistance hologramme asynchrone sur HoloLens, appareils iOS et Android.  En partageant une ancre spatial cloud durable, plusieurs périphériques peuvent observer l’hologramme persistante même au fil du temps, même si ces appareils ne sont pas présents ensemble en même temps.

Pour permanent à l’échelle ou échelle de la salle des expériences pour les casques de postes de travail attachés qui demeurent dans un diamètre égal à 5 mètres, vous pouvez généralement utiliser le [de référence du stade](coordinate-systems.md#stage-frame-of-reference) au lieu des ancres spatiales, fournissant une seule système de coordonnées dans lequel afficher tout le contenu. Toutefois, si votre application doit permettre aux utilisateurs de plate-formes au-delà de 5 mètres sur HoloLens, peut-être d’exploitation tout au long d’un étage entier d’un bâtiment, vous devez ancres spatiales pour conserver le contenu stable.

Tandis que les ancres spatiales sont idéales pour hologrammes doivent rester la même dans le monde, lorsque vous placez un point d’ancrage, il ne peut pas être déplacé. Il existe des alternatives pour les points d’ancrage qui conviennent le mieux pour hologrammes dynamiques qui balisez ainsi que l’utilisateur. Il est préférable positionner hologrammes dynamiques à l’aide d’un système de référence stationnaire (Fondation pour les coordonnées de monde d’Unity) ou un cadre de référence jointe.

## <a name="best-practices"></a>Meilleures pratiques

Ces instructions spatiale d’ancrage vous aidera à effectuer le rendu hologrammes stables qui suivent avec précision le monde réel.

### <a name="create-spatial-anchors-where-users-place-them"></a>Créer des ancres spatiales où les utilisateurs les placer

La plupart du temps, les utilisateurs doivent être ceux explicitement mise ancres spatiales.

Par exemple, sur HoloLens, une application peut se croisent l’utilisateur [les regards](gaze.md) de rayon avec la [mappage spatial](spatial-mapping.md) maille à laisser l’utilisateur décider où placer un hologramme. Lorsque l’utilisateur appuie pour placer ce HOLOGRAMME, créer un point d’ancrage spatial au point d’intersection, puis placez le hologramme à l’origine du système de coordonnées de ce point d’ancrage.

Ancres spatiales locales sont faciles et performant pour créer et le système de consolider leurs données internes si plusieurs points d’ancrage peuvent partager leurs données de capteur sous-jacentes. Vous devez généralement créer une nouvelle ancre spatiale locale pour chaque hologramme qu’un utilisateur place explicitement, sauf dans les cas décrites ci-dessous, telles que les groupes de hologrammes rigides.

### <a name="always-render-anchored-holograms-within-3-meters-of-their-anchor"></a>Toujours effectuer le rendu hologrammes ancrés dans 3 mètres de leur point d’ancrage

Ancres spatiales stabiliser leur système de coordonnées près d’origine de l’ancre. Si vous effectuez le rendu hologrammes plus d’environ 3 mètres à cette origine, ces hologrammes peuvent rencontrer des erreurs de positionnement notables par rapport à leur distance par rapport à cette origine, en raison des effets de levier-arm. Cela fonctionne si l’utilisateur est l’abréviation près le point d’ancrage, dans la mesure où l’hologramme est loin de l’utilisateur, ce qui signifie que l’erreur angular l’hologramme éloigné sera petite. Toutefois, si l’utilisateur passe en ce hologramme éloigné, il sera ensuite volumineux dans leur vue afin de rendre les effets de levier-arm à partir de l’origine d’ancrage qui habitent loin tout à fait évidentes.

### <a name="group-holograms-that-should-form-a-rigid-cluster"></a>Hologrammes de groupe qui forment un cluster rigid

Hologrammes plusieurs peuvent partager le même point d’ancrage spatial si l’application est censée ces hologrammes pour maintenir les relations fixes entre eux.

Par exemple, si vous animez un système solaire HOLOGRAPHIQUE dans une salle, il est préférable de lier tous les objets système solaire à un point d’ancrage unique dans le centre, afin qu’ils se déplacent sans heurts entre eux. Dans ce cas, il est le système solaire dans sa globalité qui est ancrée, même si ses composants sont déplaçant dynamiquement le point d’ancrage.

L’inconvénient clé ici pour maintenir la stabilité de hologramme consiste à suivre de la règle 3-compteur ci-dessus.

### <a name="render-highly-dynamic-holograms-using-the-stationary-frame-of-reference-instead-of-a-local-spatial-anchor"></a>Restituer hologrammes hautement dynamiques à l’aide du système de référence stationnaire au lieu d’un point d’ancrage spatial local

Si vous avez un hologramme hautement dynamique, comme un caractère vous épargne la salle, ou une interface utilisateur flottante qui suit le long de la prise murale près de l’utilisateur, il convient d’ignorer les ancres spatiales locales et rendre ces hologrammes directement dans le système de coordonnées fournies par le [</C0>deréférencestationnaire<spanclass="notranslate">](coordinate-systems.md#stationary-frame-of-reference) (par exemple, dans Unity, vous obtenir cela en plaçant hologrammes directement dans les coordonnées universelles sans un WorldAnchor).</span> Hologrammes dans un système de référence stationnaire peuvent être confrontés dérive de l’utilisateur est loin d’être l’hologramme, mais cela est moins susceptible d’être perceptible pour hologrammes dynamiques : le hologramme bouge constamment malgré tout, ou son mouvement conserve constamment près de l’utilisateur , où une dérive sera réduite.

Un cas intéressant d’hologrammes dynamiques est un objet qui anime à partir d’un système de coordonnées ancré à un autre. Par exemple, avez peut-être des deux châteaux 10 mètres uns des autres, chacun sur leur propres ancre spatiale, avec un castle déclencher un cannonball à l’autre castle. Pour le moment que le cannonball est déclenché, vous pouvez l’afficher à l’emplacement approprié dans le système de référence stationnaire, pour coïncider avec le canon dans le système de coordonnées de la première castle ancré. Il peut puis suivez sa trajectoire dans le système de référence stationnaire comme il rentre 10 mètres via l’air. Comme le cannonball atteint le château autres, vous pouvez choisir de déplacer dans le château deuxième ancrée de système de coordonnées pour permettre des calculs avec un corps rigide de ce castle physique.

Si vous partagez un hologramme hautement dynamique sur des appareils, vous devrez choisir certains d’ancrage de cloud spatiale à agir en tant que leur parent, comme les images de référence STATIONNAIRES ne peut pas être partagées sur plusieurs appareils.  Toutefois, dans ce cas, vous devez vous assurer que soit l’hologramme dynamique ou les appareils affichant restent dans rayon 3 mètres de l’ancre, pour garantir que l’hologramme apparaît stable sur tous les appareils.

### <a name="avoid-creating-a-grid-of-spatial-anchors"></a>Évitez de créer une grille de points d’ancrage spatiales

Il se peut que vous pouvez être tenté d’avoir votre application à supprimer une grille de points d’ancrage spatiales lorsque l’utilisateur, en cours de transition des objets dynamiques à partir d’ancrage le point d’ancrage comme ils sont en déplacement. Toutefois, cela implique un grand nombre de gestion pour votre application, sans l’avantage des profondeur des données de capteur qui tient à jour le système lui-même en interne. Dans ce cas, vous serez généralement obtenir de meilleurs résultats avec moins d’efforts en plaçant votre hologrammes dans le système de référence stationnaire, comme décrit dans la section ci-dessus.

Lors du positionnement préalable d’un ensemble d’ancres spatial cloud autour d’un espace statique, envisagez de placer les ancres spatiales aux emplacements des clé hologrammes que l’utilisateur rencontre par le principe ci-dessus, plutôt que de créer une grille arbitraire de points d’ancrage.  Cela garantit que vous obtiendrez une stabilité maximale pour ces clés hologrammes.

### <a name="release-local-spatial-anchors-you-no-longer-need"></a>Locales ancres spatiales, que vous n’avez plus besoin de mise en production

Quand un point d’ancrage spatial local est active, le système de priorité conservation autour de ces données de capteur sont proche de ce point d’ancrage. Si vous n’utilisez plus un ancrage spatial, arrêter l’accès à son système de coordonnées. Ainsi, ses données de capteur sous-jacent doit être supprimé si nécessaire.

Cela est particulièrement important pour les ancres locales que vous avez conservé la Boutique spatiale. Les données de capteur derrière ces ancres restent autour définitivement pour permettre à votre application trouver ce point d’ancrage dans les futures sessions d’application, ce qui réduiront l’espace disponible pour effectuer le suivi d’autres points d’ancrage. Conserver uniquement les ancres locales dont vous avez besoin pour rechercher à nouveau dans les sessions ultérieures et les supprimer à partir du magasin lorsqu’ils ne sont plus explicites pour l’utilisateur.

Points d’ancrage spatial cloud, votre stockage peut évoluer à mesure que votre scénario requiert.  Vous pouvez stocker autant d’ancres cloud en fonction des besoins, les libérant uniquement lorsque vous savez que vos utilisateurs ne devront pas localiser hologrammes à ce point d’ancrage à nouveau.

## <a name="see-also"></a>Voir aussi
* [Systèmes de coordonnées](coordinate-systems.md)
* [Partage des expériences en réalité mixte](shared-experiences-in-mixed-reality.md)
* <a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Ancres Spatial Azure</a>
* [Persistance dans Unity](persistence-in-unity.md)
* [Ancres spatiales dans DirectX](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-spatial-anchors)
* [Étude de cas - parcourant des trous dans la réalité](case-study-looking-through-holes-in-your-reality.md)
