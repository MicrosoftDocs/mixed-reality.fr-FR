---
title: Visualisation d’analyse de salle
description: Les applications qui requièrent des données de mappage spatial s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions en tant que l’utilisateur explore leur environnement avec l’appareil actif.
author: mattzmsft
ms.author: alexpf
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, modèles d’application, la conception, HoloLens, analyse de la salle, spatiale de mappage, surface reconstruction, de maillage
ms.openlocfilehash: 09df4464ea4dac01dfad637886b07b861f468d4d
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829915"
---
# <a name="room-scan-visualization"></a>Visualisation d’analyse de salle

Les applications qui requièrent des données de mappage spatial s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions en tant que l’utilisateur explore leur environnement avec l’appareil actif. Le souci d’exhaustivité et la qualité de ces données dépend de plusieurs facteurs, notamment la quantité d’exploration de l’utilisateur a effectué, combien de temps écoulé depuis l’exploration et indique si les objets tels que des portes et meubles ont déplacés depuis le périphérique analyse la zone.

Pour garantir des données de mappage spatial utiles, les développeurs d’applications ont plusieurs options :
* S’appuient sur ce qui peut avoir déjà été collecté. Ces données peuvent être incomplètes initialement.
* Demandez à l’utilisateur à utiliser le mouvement de bloom pour accéder à la réalité mixte Windows domestique et ensuite Explorer la zone qu’ils souhaitent utiliser pour une expérience. Ils peuvent utiliser appui en l’air pour confirmer que la zone nécessaire est connue à l’appareil.
* Créer une expérience d’exploration personnalisés dans leur propre application.

Notez que dans tous ces cas, les données réelles collectées au cours de l’exploration sont stockées par le système et l’application n’a pas besoin pour ce faire.

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Visualisation d’analyse de salle</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>



## <a name="building-a-custom-scanning-experience"></a>Création d’une expérience d’analyse personnalisée

Les applications peuvent décider d’analyser les données de mappage spatial au début de l’expérience pour déterminer s’ils veulent que l’utilisateur d’effectuer des étapes supplémentaires pour améliorer son exhaustivité et la qualité. Si l’analyse indique la qualité doit être améliorée, les développeurs doivent fournir une visualisation à superposer sur le monde entier pour indiquer :
* La quantité du volume total à proximité des utilisateurs doit faire partie de l’expérience
* Où l’utilisateur doit accéder pour améliorer les données

Les utilisateurs ne savent pas ce qui rend une analyse « bonne ». Ils doivent être affichés ou dit que ce que vous recherchez s’il leur sont demandés pour évaluer une analyse – apparence à deux dimensions, la distance entre les murs réels, etc. Le développeur doit implémenter une boucle de rétroaction qui inclut l’actualisation des données de mappage spatial pendant la phase d’analyse ou l’exploration.

Dans de nombreux cas, il peut être préférable d’indiquer à l’utilisateur de ce qu’ils doivent (par exemple, examinez le plafond, recherchez derrière meubles), afin d’obtenir la qualité d’analyse nécessaires.

## <a name="cached-versus-continuous-spatial-mapping"></a>Mise en cache et continue mappage spatial

Les données de mappage spatial sont le poids de la plus importante des applications de source de données peuvent consommer. Pour éviter les problèmes de performances telles que suppression d’images ou interruption du son, la consommation de ces données doit être mûrement.

Analyse active durant une expérience peut être bénéfiques ou nuisibles et le développeur doit décider quelle méthode à utiliser en fonction de l’expérience.

### <a name="cached-spatial-mapping"></a>Mise en cache de mappage spatial

Dans le cas de mappage spatial mis en cache, l’application est généralement prend un instantané des données de mappage spatial et utilise cette capture instantanée pendant la durée de l’expérience.

**Avantages**
* Réduction des coûts sur le système pendant que l’expérience est en cours d’exécution pointe à une puissance importante, thermique et gains de performance de processeur.
* Une implémentation plus simple de l’expérience principale dans la mesure où il n’est pas interrompu par des modifications dans les données spatiales.
* Une seule une fois tout post-traitement des données spatiales pour les graphismes, graphiques et autres à des fins de coûts.

**Drawbacks**
* Le déplacement des objets du monde réel ou des personnes n’est pas reflété par les données en cache. Exemple l’application peut prendre en compte une porte ouverte lorsqu’il est fermé en fait maintenant.
* Mémoire potentiellement plus de l’application à mettre à jour la version mise en cache des données.

Un bon cas pour cette méthode est un environnement contrôlé ou un jeu en haut de la table.

### <a name="continuous-spatial-mapping"></a>Mappage spatial continue

Certaines applications peuvent reposer sur poursuit l’analyse pour actualiser les données de mappage spatial.

**Avantages**
* Vous n’avez pas besoin de générer un distinct analyse ou l’exploration expérience dès le départ dans votre application.
* Le déplacement des objets du monde réel peut être reflété par le jeu, mais avec un délai.

**Drawbacks**
* Plus haute complexité dans l’implémentation de l’expérience principale.
* Risque de surcharge du traitement supplémentaire pour le graphique ou physique en tant que modifications doivent être incrémentielle ingérés par ces systèmes.
* Améliorer la puissance, thermique et impact sur le processeur.

Un bon cas pour cette méthode est un où les hologrammes sont amenés à interagir avec le déplacement d’objets, par exemple, une voiture HOLOGRAPHIQUE que lecteurs sur le sol souhaitez correctement rencontrent une porte selon qu’il est ouvert ou fermé.

## <a name="see-also"></a>Voir aussi
* [Conception du mappage spatial](spatial-mapping-design.md)
* [Systèmes de coordonnées](coordinate-systems.md)
* [Conception du son spatial](spatial-sound-design.md)
