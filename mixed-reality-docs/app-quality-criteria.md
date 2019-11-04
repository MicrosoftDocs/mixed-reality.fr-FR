---
title: Critères de qualité des applications
description: Ce document décrit les principaux facteurs qui ont un impact sur la qualité des applications de réalité mixte.
author: cjdgit
ms.author: crderr
ms.date: 03/21/2018
ms.topic: article
keywords: critères de qualité des applications, réalité mixte, application de réalité mixte
ms.openlocfilehash: f98111ebe9aacc30778e86501be41e6ac5f6d165
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437050"
---
# <a name="app-quality-criteria"></a>Critères de qualité des applications

Ce document décrit les principaux facteurs qui ont un impact sur la qualité des applications de réalité mixte. Pour chaque facteur, les informations suivantes sont fournies
* Vue d’ensemble : brève description du facteur de qualité et de la raison pour laquelle il est important.
* Impact sur l’appareil : le type de l’appareil de la réalité mixte de la fenêtre est affecté.
* Critères de qualité : comment évaluer le facteur de qualité.
* Comment mesurer : méthodes pour mesurer (ou expérimenter) le problème.
* Recommandations : Résumé des approches pour offrir une meilleure expérience utilisateur.
* Ressources : ressources de conception et de développement pertinentes qui sont utiles pour créer de meilleures expériences d’application.

## <a name="frame-rate"></a>Fréquence d’images

La fréquence d’images est le premier pilier de la stabilité de l’hologramme et du confort de l’utilisateur. La fréquence d’images en dessous des cibles recommandées peut provoquer l’apparition d’hologrammes, ce qui a un impact négatif sur la qualité de l’expérience et éventuellement une fatigue oculaire. La fréquence d’images cible pour votre expérience sur les casques immersifs Windows Mixed Reality est 60 Hz ou 90Hz, selon les PC compatibles Windows Mixed realer que vous souhaitez prendre en charge. Pour HoloLens, la fréquence d’images cible est 60 Hz.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>✔️</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
| L’application répond régulièrement à l’objectif des images par seconde (FPS) pour l’appareil cible : 60fps sur HoloLens ; 90fps sur ultra PC ; et 60fps sur les PC grand public. | L’application présente des interruptions intermittentes de la trame sans gêner l’expérience de base. ou la valeur FPS est toujours inférieure à l’objectif souhaité, mais n’empêche pas l’expérience de l’application. | L’application rencontre une baisse de la fréquence d’images en moyenne toutes les dix secondes ou moins. |

### <a name="how-to-measure"></a>Comment mesurer

* Un graphique de fréquence d’images en temps réel est fourni par le biais du [portail d’appareils Windows](using-the-windows-device-portal.md#system-performance) sous « performances système ».
* Pour le débogage de développement, ajoutez un compteur de diagnostic de fréquence d’images dans l’application. Consultez ressources pour obtenir un exemple de compteur.
* Les chutes de fréquence d’images peuvent être rencontrées dans l’appareil pendant que l’application est en cours d’exécution en déplaçant votre tête d’un côté à l’autre. Si l’hologramme présente un mouvement instable inattendue, la fréquence d’images faible ou le plan de stabilité est probablement la cause.

### <a name="recommendations"></a>Recommandations

* Ajoutez un compteur de fréquence d’images au début du travail de développement.
* Les modifications qui entraînent une chute de la fréquence d’images doivent être évaluées et résolues de manière appropriée en tant que bogue de performance.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Comprendre les performances de la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Stabilité et fréquence d’hologramme](hologram-stability.md#frame-rate)
* [Budget des performances des actifs](asset-creation-process.md)
* [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [MRToolkit, affichage du compteur FPS](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Utilities/README.md)
* [MRToolkit, nuanceurs](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Utilities/Shaders)

#### <a name="external-references"></a>Références externes

* [Unity, optimisation des applications mobiles](https://www.youtube.com/watch?v=j4YAY36xjwE)

## <a name="hologram-stability"></a>Stabilité de l’hologramme

Les hologrammes stables augmenteront la convivialité et l’incroyableté de votre application et créeront une expérience d’affichage plus confortable pour l’utilisateur. La qualité de la stabilité des hologrammes résulte d’un développement d’applications correct et de la capacité de l’appareil à comprendre (suivre) son environnement. Alors que la fréquence d’images est le premier pilier de la stabilité, d’autres facteurs peuvent avoir un impact sur la stabilité, notamment :

* Utilisation du plan de stabilisation
* Distance aux ancres spatiales
* Suivre

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
|  Les hologrammes semblent constamment stables. | Le contenu secondaire présente un mouvement inattendu ; ou un mouvement inattendu ne fait pas obstacle à l’expérience globale de l’application. | Le contenu principal du cadre présente un mouvement inattendu. |

### <a name="how-to-measure"></a>Comment mesurer

Lors de l’usure de l’appareil et de l’affichage de l’expérience :

* Déplacez votre tête d’un côté à l’autre, si les hologrammes affichent un mouvement inattendu, alors une fréquence d’images faible ou un alignement incorrect du plan de stabilité sur le plan focal est la cause probable.
* Déplacez-vous autour des hologrammes et de l’environnement, recherchez des comportements tels que natation et jumpiness. Ce type de mouvement est probablement dû au fait que l’appareil n’effectue pas le suivi de l’environnement ou à la distance vers l’ancrage spatial.
* Si un grand nombre ou plusieurs hologrammes se trouvent dans le cadre, observez le comportement de l’hologramme à différentes profondes tout en déplaçant la position de votre tête d’un côté à l’autre, si shakiness apparaît que cela est probablement dû au plan de stabilisation.

### <a name="recomendations"></a>Recommandations

* Ajoutez un compteur de fréquence d’images au début du travail de développement.
* Utilisez le plan de stabilisation.
* Affichez toujours les hologrammes ancrés dans les 3 mètres de leur ancrage.
* Assurez-vous que votre environnement est configuré pour un suivi correct.
* Concevez votre expérience afin d’éviter les hologrammes à différents niveaux de profondeur focale dans le cadre.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Stabilité et fréquence d’hologramme](hologram-stability.md#frame-rate)
* [Étude de cas, à l’aide du plan de stabilisation](case-study-using-the-stabilization-plane-to-reduce-holographic-turbulence.md)
* [Comprendre les performances de la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)
* [Ancres spatiales](spatial-anchors.md)
* [Gestion des erreurs de suivi](coordinate-systems.md#handling-tracking-errors)
* [Cadre de référence stationnaire](coordinate-systems.md#stationary-frame-of-reference)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Kit de complément MR, IPD Kinect](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

## <a name="holograms-position-on-real-surfaces"></a>Position des hologrammes sur les surfaces réelles

Un mauvais alignement des hologrammes avec des objets physiques (s’ils sont destinés à être placés les uns par rapport aux autres) est une indication claire de l’absence d’Union des hologrammes et du monde réel. La précision de la position doit être relative aux besoins du scénario ; par exemple, le positionnement de surface général peut utiliser la carte spatiale, mais un positionnement plus précis nécessitera l’utilisation de marqueurs et d’étalonnage.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
| Les hologrammes s’alignent sur la surface généralement dans la plage de centimètres en pouces. Si une plus grande précision est requise, l’application doit fournir un moyen efficace de collaboration au sein de la spécification de l’application souhaitée. | N/A | Les hologrammes apparaissent non alignés avec l’objet cible physique en rompant le plan de surface ou en s’éloignant de l’aire. Si la précision est requise, les hologrammes doivent répondre aux spécifications de proximité du scénario. | 

### <a name="how-to-measure"></a>Comment mesurer

* Les hologrammes placés sur la carte spatiale ne doivent pas sembler très flotter au-dessus ou en dessous de la surface.
* Les hologrammes qui nécessitent un placement précis doivent avoir une forme de système de marqueur et de système d’étalonnage qui est précis à l’exigence du scénario.

### <a name="recommendations"></a>Recommandations

* La carte spatiale est utile pour placer des objets sur des surfaces lorsque la précision n’est pas requise.
* Pour une meilleure précision, utilisez des marqueurs ou des affiches pour définir les hologrammes et un contrôleur Xbox (ou un mécanisme d’alignement manuel) pour l’étalonnage final.
* Envisagez de casser des hologrammes très grands en parties logiques et en alignant chaque partie sur l’aire de conception.
* Une distance incorrecte (IPD) peut également affecter l’alignement de l’hologramme. Configurez toujours HoloLens sur l’IPD de l’utilisateur.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Positionnement du mappage spatial](spatial-mapping.md#placement)
* [Processus d’analyse de la salle](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [Meilleures pratiques pour les ancrages spatiaux](spatial-anchors.md#best-practices)
* [Gestion des erreurs de suivi](coordinate-systems.md#handling-tracking-errors)
* [Mappage spatial dans Unity](spatial-mapping-in-unity.md)
* [Présentation du développement Vuforia](vuforia-development-overview.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [MR spatial 230 : mappage spatial](holograms-230.md)
* [Boîte à outils MR, bibliothèques de mappage spatiale](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialMapping/README.md)
* [Kit de complément MR, exemple d’étalonnage d’affiches](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/PosterCalibrationSample)
* [Kit de complément MR, IPD Kinect](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

#### <a name="external-references"></a>Références externes

* [Étude de cas Lowes, alignement de précision](https://www.youtube.com/watch?v=LceMdyKZ4PI)

## <a name="viewing-zone-of-comfort"></a>Affichage de la zone de confort

Les développeurs d’applications contrôlent l’emplacement des yeux des utilisateurs en plaçant le contenu et les hologrammes à différents niveaux. Les utilisateurs qui ont le port HoloLens s’intègrent toujours à la version 2.0 m pour maintenir une image claire, car les affichages HoloLens sont fixés à une distance optique d’environ 2,0 mètres de l’utilisateur. Une profondeur de contenu incorrecte peut entraîner une gêne visuelle ou une fatigue.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

<table>
<tr>
<td> Meilleures </td><td><ul>
<li>Placez le contenu à 2 m.</li><li>Quand les hologrammes ne peuvent pas être placés à 2 ou 2 millions de conflits entre la convergence et l’hébergement, la zone optimale pour le placement de l’hologramme est comprise entre 1,25 m et 5 m.</li><li>Dans tous les cas, les concepteurs doivent structurer le contenu pour encourager les utilisateurs à interagir à distance de 1 + m (par exemple, ajuster la taille du contenu et les paramètres de positionnement par défaut).</li><li>À moins qu’il ne soit spécifiquement pas requis par le scénario, un plan de découpage doit être implémenté avec fadeout à partir de 1 million.</li><li>Dans les cas où une observation plus proche d’un hologramme motionless est requise, le contenu ne doit pas être plus proche que 50cm.</li>
</ul></td>
</tr><tr>
<td> Présente</td><td> Le contenu se trouve dans le Guide d’affichage et de mouvement, mais il n’utilise pas ou n’utilise pas le plan de découpage.</td>
</tr><tr>
<td> Incident </td><td> Le contenu est présenté trop près (généralement &lt;1,25 m, ou &lt;50cm pour les hologrammes fixes nécessitant une observation plus proche.)</td>
</tr>
</table>

### <a name="how-to-measure"></a>Comment mesurer

* Le contenu doit généralement être en 2 millions de dollars, mais pas plus près de 1,25 ou plus que 5 m.
* À quelques exceptions près, la distance de rendu du découpage HoloLens doit être définie sur. 85CM avec fadeout de contenu à partir de 1 million. Approchez le contenu et notez l’effet plan de découpage.
* Le contenu fixe ne doit pas être plus proche de 50cm.

### <a name="recommendations"></a>Recommandations

* Concevez du contenu pour une distance d’affichage optimale de 2 m.
* Définissez la distance de rendu du découpage sur 85cm avec fadeout de contenu à partir de 1M.
* Pour les hologrammes fixes qui nécessitent un affichage plus étroit, le plan de découpage ne doit pas être plus proche de 30cm et fadeout doit démarrer au moins 10cm à partir du plan de découpage.

### <a name="resources"></a>Ressources

* [Distance de rendu](hologram-stability.md#hologram-render-distances)
* [Point de focus dans Unity](focus-point-in-unity.md)
* [Expérimentation avec l’échelle](scale.md#experimenting-with-scale)
* [Texte, taille de police recommandée](typography.md#recommended-font-size)

## <a name="depth-switching"></a>Basculement de profondeur

Indépendamment de l’affichage des problèmes liés à la zone de confort, les demandes pour l’utilisateur de basculer fréquemment ou rapidement entre des objets de niveau proche et lointain (y compris des hologrammes et du contenu réel) peuvent entraîner une fatigue oculomotor et une gêne générale.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>✔️</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
|  Basculement de profondeur limitée ou naturelle qui ne permet pas à l’utilisateur de se concentrer de manière non naturelle. | Commutateur à profondeur brusque : il s’agit du noyau et est conçu pour l’expérience de l’application, ou le commutateur de profondeur brusque provoqué par un contenu réel inattendu. | Commutateur de profondeur cohérent ou basculement de profondeur brusque qui n’est pas nécessaire ou essentiel à l’expérience de l’application. | 

### <a name="how-to-measure"></a>Comment mesurer

* Si l’application exige que l’utilisateur change de manière cohérente et/ou brusquement le focus de profondeur, il y a un problème de changement de profondeur.

### <a name="recommendations"></a>Recommandations

* Conservez le contenu principal dans un plan focal cohérent et assurez-vous que le plan de stabilisation correspond au plan focal. Cela permet d’atténuer la fatigue oculomotor et le mouvement d’hologramme inattendu.

### <a name="resources"></a>Ressources

* [Distance de rendu](hologram-stability.md#hologram-render-distances)
* [Point de focus dans Unity](focus-point-in-unity.md)

## <a name="use-of-spatial-sound"></a>Utilisation du son spatial

Dans Windows Mixed Reality, le moteur audio fournit le composant d’acoustique de l’expérience de la réalité mixte en simulant le son en 3D à l’aide de la direction, de la distance et des simulations environnementales. L’utilisation d’un son spatial dans une application permet aux développeurs de placer de manière convaincante des sons dans un espace à 3 Dimensions (sphère) autour de l’utilisateur. Ces sons semblent apparaître comme s’ils étaient issus d’objets physiques réels ou d’hologrammes de réalité mixte dans l’environnement de l’utilisateur. Le son spatial est un outil puissant pour la conception de l’immersion, de l’accessibilité et de l’expérience utilisateur dans les applications de réalité mixte.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>✔️</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
|  Le son est logiquement spatial, et l’expérience utilisateur utilise le son de manière appropriée pour faciliter la détection d’objets et les commentaires des utilisateurs. Les sons sont naturels et pertinents pour les objets et normalisés dans le scénario. | L’audio spatial est utilisé de façon appropriée pour la récupération, mais il est manquant comme moyen d’aider aux commentaires des utilisateurs et à la découverte. | Le son n’est pas spatial comme prévu, et/ou manque de son pour aider l’utilisateur au sein de l’expérience utilisateur. Ou l’audio spatial n’a pas été pris en compte ou utilisé dans la conception du scénario. | 

### <a name="how-to-measure"></a>Comment mesurer

* En général, les sons pertinents doivent émettre des hologrammes cibles (par exemple, des sons d’écorce provenant du chien holographique).
* Des signaux sonores doivent être utilisés tout au long de l’expérience utilisateur pour aider l’utilisateur à faire part de ses commentaires ou à connaître des actions en dehors du cadre holographique.

### <a name="recommendations"></a>Recommandations

* Utilisez l’audio spatial pour faciliter la détection d’objets et les interfaces utilisateur.
* Les sons réels fonctionnent mieux que la synthèse ou le son non naturel.
* La plupart des sons doivent être spatiaux.
* Évitez les émetteurs invisibles.
* Évitez le masquage spatial.
* Normaliser tous les sons.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Son spatial](spatial-sound.md)
* [Conception du son spatial](spatial-sound-design.md)
* [Son spatial dans Unity](spatial-sound-in-unity.md)
* [Étude de cas, son spatial pour HoloTour](case-study-spatial-sound-design-for-holotour.md)
* [Étude de cas utilisant le son spatial dans RoboRaid](case-study-using-spatial-sound-in-roboraid.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [MR spatial 220 : son spatial](holograms-220.md)
* [MRToolkit, audio spatial](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialSound/README.md)

## <a name="focus-on-holographic-frame-fov-boundaries"></a>Focalisation sur les limites du cadre holographique

Les expériences utilisateur bien conçues peuvent créer et gérer le contexte utile de l’environnement virtuel qui s’étend autour des utilisateurs. L’atténuation de l’effet des limites de l’aide implique une conception réfléchie de l’échelle et du contexte du contenu, l’utilisation de l’audio spatial, les systèmes d’aide et la position de l’utilisateur. Si vous avez terminé, l’utilisateur se sentira moins affecté par les limites de l’aide, tout en disposant d’une expérience d’application confortable.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
|  L’utilisateur ne perd jamais de contexte et l’affichage est à l’aise. L’assistance contextuelle est fournie pour les objets volumineux. Les informations de découverte et d’affichage sont fournies pour les objets en dehors du frame. En général, la conception de mouvement et l’échelle des hologrammes sont appropriées pour une expérience d’affichage confortable. | L’utilisateur ne perd jamais de contexte, mais un mouvement de cou supplémentaire peut être nécessaire dans des situations limitées. Dans le cas d’une mise à l’échelle limitée, les hologrammes rompent le cadre vertical ou horizontal provoquant un mouvement du cou pour afficher les hologrammes. | L’utilisateur risque de perdre du contexte et/ou un mouvement de cou cohérent est nécessaire pour afficher les hologrammes. Aucun guide de contexte pour les grands objets holographiques, déplacement d’objets facile à perdre en dehors du cadre sans guide de détectabilité, ou hologrammes de haut, nécessite un mouvement de cou normal. | 

### <a name="how-to-measure"></a>Comment mesurer

* Le contexte d’un (grand) hologramme est perdu ou n’est pas compris en raison d’un découpage aux limites.
* L’emplacement des hologrammes est difficile à trouver en raison du manque d’administrateurs ou de contenus qui se déplacent rapidement dans le cadre holographique.
* Le scénario nécessite un mouvement de tête normal et répétitif pour voir entièrement un hologramme entraînant une fatigue du cou.

### <a name="recommendations"></a>Recommandations

* Démarrez l’expérience avec les petits objets qui correspondent à l’angle d’ouverture, puis faites la transition avec des signaux visuels vers des versions plus grandes.
* Utilisez des directeurs audio et d’avertissement pour aider l’utilisateur à trouver du contenu en dehors de l’aide.
* Évitez autant que possible les hologrammes qui découpent verticalement l’angle de la verticale.
* Fournissez à l’utilisateur des conseils dans l’application pour un meilleur affichage de l’emplacement.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Image holographique](holographic-frame.md)
* [Étude de cas, interface utilisateur HoloStudio et apprentissages de conception d’interaction](case-study-3-holostudio-ui-and-interaction-design-learnings.md?#problem-2-modal-dialogs-are-sometimes-out-of-the-holographic-frame)
* [Échelle des objets et des environnements](scale.md)
* [Curseurs, signaux visuels](cursors.md#visual-cues)

#### <a name="external-references"></a>Références externes

* [Bien d’ADO sur l’angle d’été](https://www.linkedin.com/pulse/hololens-much-ado-field-of-view-michael-hoffman?lipi=urn%3Ali%3Apage%3Ad_flagship3_feed%3B6iQ%2FbTevLDU93w3I2ewLJw%3D%3D)

## <a name="content-reacts-to-user-position"></a>Le contenu réagit à la position de l’utilisateur

Les hologrammes doivent réagir à la position de l’utilisateur à peu près de la même façon que les objets « réels ». L’un des éléments d’interface utilisateur qui ne peuvent pas nécessairement supposer que la position d’un utilisateur est stationnaire et s’adapte au mouvement de l’utilisateur est une considération notable. La conception d’une application qui s’adapte correctement à la position de l’utilisateur crée une expérience plus crédible et la rend plus facile à utiliser.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>✔️</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

<table>
<tr>
<td> Meilleures </td><td> Le contenu et l’interface utilisateur s’adaptent aux postes des utilisateurs, ce qui permet à l’utilisateur d’interagir naturellement avec le contenu dans le cadre du déplacement d’utilisateur attendu.</td>
</tr><tr>
<td> Présente </td><td> L’interface utilisateur s’adapte à la position de l’utilisateur, mais peut empêcher l’affichage du contenu de la clé qui oblige l’utilisateur à ajuster sa position.</td>
</tr><tr>
<td> Incident </td><td><ol>
<li>Les éléments d’interface utilisateur sont perdus ou verrouillés au cours du mouvement, provoquant ainsi un retour à (ou une recherche) anormal des contrôles.</li><li>Les éléments d’interface utilisateur limitent l’affichage du contenu principal.</li><li>Le déplacement de l’interface utilisateur n’est pas optimisé pour l’affichage de la distance et de l’inertie, en particulier avec les éléments de <a href="billboarding-and-tag-along.md">balisage</a> .</li>
</ol></td>
</tr>
</table>

### <a name="how-to-measure"></a>Comment mesurer

* Toutes les mesures doivent être effectuées dans une étendue raisonnable du scénario. Si le déplacement des utilisateurs varie, n’essayez pas de tromper l’application avec un déplacement extrême de l’utilisateur.
* Pour les éléments d’interface utilisateur, les contrôles pertinents doivent être disponibles quel que soit le déplacement de l’utilisateur. Par exemple, si l’utilisateur consulte et parcourt une carte 3D avec zoom, le contrôle de zoom doit être immédiatement accessible à l’utilisateur, quel que soit son emplacement.

### <a name="recommendations"></a>Recommandations

* L’utilisateur est l’appareil photo et il contrôle le mouvement. Laissez-les sur le lecteur.
* Envisagez l’utilisation de panneaux pour le texte et les systèmes de menus qui, autrement, seraient universellement verrouillés ou obscurcis si un utilisateur devait se déplacer.
* Utilisez tag-avec pour le contenu qui doit suivre l’utilisateur tout en permettant à l’utilisateur de voir ce qui est devant eux.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Conception d’interaction](hologram.md)
* [Couleur, lumière et matériau](color,-light-and-materials.md)
* [Billboarding et tag-along](billboarding-and-tag-along.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Automotion et utilisateur locomotion](comfort.md#self-motion-and-user-locomotion)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Monsieur-entrée 210 : point de regard](holograms-210.md)

## <a name="input-interaction-clarity"></a>Clarté d’interaction d’entrée

La clarté de l’interaction d’entrée est essentielle à l’utilisation d’une application et comprend la cohérence des entrées, l’approche, la détectabilité des méthodes d’interaction. L’utilisateur doit être en mesure d’utiliser des interactions communes à l’ensemble de la plateforme sans réapprendre. Si l’application dispose d’une entrée personnalisée, elle doit être clairement communiquée et démontrée.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>✔️</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
|  Les méthodes d’interaction d’entrée sont cohérentes avec les [recommandations](interaction-fundamentals.md)fournies par Windows Mixed Reality. Toute entrée personnalisée ne doit pas être redondante avec une entrée standard (plutôt que d’utiliser l’interaction standard) et doit être clairement communiquée et présentée à l’utilisateur. | Semblable au meilleur, mais les entrées personnalisées sont redondantes avec des méthodes d’entrée standard. L’utilisateur peut toujours atteindre l’objectif et progresser dans l’expérience de l’application. | Il est difficile de comprendre la méthode d’entrée ou le mappage de bouton. L’entrée est fortement personnalisée, ne prend pas en charge les entrées standard, aucune instruction, ou risque de provoquer des problèmes de fatigue et de confort. | 

### <a name="how-to-measure"></a>Comment mesurer

* L’application utilise des [méthodes d’entrée standard](interaction-fundamentals.md) cohérentes.
* Si l’application a des entrées personnalisées, elle est clairement communiquée à :
* Expérience de première exécution
* Écrans d’introduction
* Info-bulles
* Autocar à main
* Section d’aide
* Voix sur

### <a name="recommendations"></a>Recommandations

* Utilisez des méthodes d’entrée standard dans la mesure du possible.
* Fournissez des démonstrations, des didacticiels et des info-bulles pour les méthodes d’entrée non standard.
* Utilisez un modèle d’interaction cohérent dans l’ensemble de l’application.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Interactions instinctuelles](interaction-fundamentals.md)
* [Objets interactifs](interactable-object.md)
* [Suivre de la tête et stabiliser](gaze-and-dwell.md)
* [Curseurs](cursors.md)
* [Confort et point de regard](comfort.md#gaze-direction)
* [Entrée vocale](voice-input.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Guide de portage des entrées pour Unity](input-porting-guide-for-unity.md)
* [Saisie au clavier dans Unity](keyboard-input-in-unity.md)
* [Pointage du regard dans Unity](gaze-in-unity.md)
* [Mouvements et contrôleurs de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md)
* [Entrée vocale dans Unity](voice-input-in-unity.md)
* [Saisie à l’aide de la commande de jeu, du clavier et de la souris dans DirectX](keyboard,-mouse,-and-controller-input-in-directx.md)
* [Suivre de la tête et du regard dans DirectX](gaze-in-directx.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Entrée vocale dans DirectX](voice-input-in-directx.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Étude de cas : la poursuite de l’informatique plus personnelle](case-study-the-pursuit-of-more-personal-computing.md#less-interface-in-your-face)
* [Étude de Cast : interface utilisateur HoloStudio et apprentissages de conception d’interaction](case-study-3-holostudio-ui-and-interaction-design-learnings.md)
* [Exemple d’application : table périodique des éléments](periodic-table-of-the-elements.md)
* [Exemple d’application : module lunaire](lunar-module.md)
* [Monsieur-entrée 210 : point de regard](holograms-210.md)
* [Entrée MR 211 : gestes](holograms-211.md)
* [Entrée MR 212 : voix](holograms-212.md)

## <a name="interactable-objects"></a>Objets interactifs

Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait en 2D. Dans le monde de la réalité mixte en trois dimensions, nous n’avons plus à limiter le monde de l’abstraction. Tout peut être un objet pouvant être utilisé qui déclenche un événement. Un objet pouvant être en interaction peut être représenté sous la forme d’un objet à partir d’une tasse de café sur la table. Quelle que soit la forme, les objets interactifs doivent être clairement reconnus par l’utilisateur via des signaux visuels et audio.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>✔️</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
|  Quelle que soit la forme, les objets interactifs sont reconnaissables par des signaux audio et visuels dans les trois États : inactif, ciblé et sélectionné. « Regardez-le, dites-le » est clair et constamment utilisé tout au long de l’expérience. Les objets sont mis à l’échelle et distribués pour permettre le ciblage gratuit des erreurs. | L’utilisateur peut reconnaître un objet comme étant en interaction avec des retours audio ou visuels, et peut cibler et activer l’objet. | En l’absence de signaux visuels ou audio, l’utilisateur ne peut pas reconnaître un objet pouvant être en interaction. Les interactions sont sujettes aux erreurs en raison de l’échelle de l’objet ou de la distance entre les objets. | 

### <a name="how-to-measure"></a>Comment mesurer

* Les objets interactifs sont reconnaissables comme « interactifs »; y compris les boutons, les menus et le contenu spécifique à l’application. En règle générale, il doit exister un signal visuel et audio pour cibler les objets interactifs.

### <a name="recommendations"></a>Recommandations

* Utilisez des commentaires visuels et audio pour les interactions.
* Les commentaires visuels doivent être différenciés pour chaque État d’entrée (inactif, ciblé, sélectionné)
* Les objets interactifs doivent être mis à l’échelle et placés en vue d’une erreur de ciblage libre.
* Les objets interactifs groupés (tels qu’une barre de menus ou une liste) doivent avoir un espacement correct pour le ciblage.
* Les boutons et les menus qui prennent en charge les commandes vocales doivent fournir des étiquettes de texte pour le mot clé de commande (« consultez-le », dites-le «»)

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Objet avec interaction possible](interactable-object.md)
* [Texte dans Unity](text-in-unity.md)
* [Rectangle englobant et barre de l’application](app-bar-and-bounding-box.md)
* [Entrée vocale](voice-input.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Kit de pratiques de réalité mixte-UX](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="room-scanning"></a>Analyse de la salle

Les applications qui requièrent des données de mappage spatiale s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions lorsque l’utilisateur explore son environnement avec l’appareil actif. L’exhaustivité et la qualité de ces données dépendent d’un certain nombre de facteurs, notamment la quantité d’exploration effectuée par l’utilisateur, le temps écoulé depuis l’exploration et si les objets tels que les meubles et les portes ont été déplacés depuis que l’appareil a analysé la zone. De nombreuses applications analysent les données de mappage spatiale au début de l’expérience afin de déterminer si l’utilisateur doit effectuer des étapes supplémentaires pour améliorer l’exhaustivité et la qualité de la carte spatiale. Si l’utilisateur est invité à analyser l’environnement, vous devez fournir des instructions claires au cours de l’analyse.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>❌</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
|  La visualisation de la maille spatiale indique aux utilisateurs que l’analyse est en cours. L’utilisateur sait clairement ce qu’il doit faire et quand l’analyse démarre et s’arrête. | La visualisation du maillage spatial est fournie, mais l’utilisateur peut ne pas savoir clairement ce qu’il faut faire et aucune information de progression n’est fournie. | Aucune visualisation de la maille. Aucune information n’est fournie à l’utilisateur quant à son emplacement ou au démarrage ou à l’arrêt de l’analyse. |

### <a name="how-to-measure"></a>Comment mesurer

* Au cours d’une analyse de la salle requise, des conseils visuels et audio sont fournis pour indiquer l’emplacement et le moment du démarrage et de l’arrêt de l’analyse.

### <a name="recommendations"></a>Recommandations

* Indiquez la quantité de volume total des utilisateurs avoisinants qui doit faire partie de l’expérience.
* Communiquer quand l’analyse démarre et s’arrête, comme un indicateur de progression.
* Utilisez une visualisation de la maille pendant l’analyse.
* Fournissez des signaux visuels et audio pour encourager l’utilisateur à regarder et à se déplacer dans la pièce.
* Informez l’utilisateur où accéder à pour améliorer les données. Dans de nombreux cas, il peut être préférable de dire à l’utilisateur ce qu’il doit faire (par exemple, regarder le plafond, regarder derrière le mobilier), afin d’obtenir la qualité d’analyse nécessaire.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Visualisation du balayage d’une pièce](room-scan-visualization.md)
* [Étude de cas : développement des fonctionnalités de mappage spatial de HoloLens](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [Étude de cas : conception de son spatial pour HoloTour](case-study-spatial-sound-design-for-holotour.md)
* [Étude de cas : création d’une expérience immersive dans des fragments](case-study-creating-an-immersive-experience-in-fragments.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Kit de pratiques de réalité mixte-UX](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="directional-indicators"></a>Indicateurs directionnels

Dans une application de réalité mixte, le contenu peut être en dehors du champ de vue ou bloqués par des objets réels. Une application bien conçue permettra à l’utilisateur de trouver plus facilement du contenu non visible. Les indicateurs directionnels signalent à un utilisateur un contenu important et fournissent des conseils sur le contenu relatif à la position de l’utilisateur. Les instructions relatives au contenu non visible peuvent prendre la forme d’émetteurs de sons, de flèches directionnelles ou de signaux visuels directs.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>✔️</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
|  Les signaux audio et visuel guident directement l’utilisateur vers du contenu pertinent en dehors du champ de vue. | Une flèche ou un indicateur qui dirige l’utilisateur dans la direction générale du contenu. | Le contenu pertinent est en dehors du champ de la vue, et de mauvaises instructions de localisation sont fournies à l’utilisateur. | 

### <a name="how-to-measure"></a>Comment mesurer

* Le contenu pertinent en dehors du champ utilisateur de la vue est détectable via des signaux visuels et/ou audio.

### <a name="recommendations"></a>Recommandations

* Quand le contenu pertinent est en dehors du champ de vue de l’utilisateur, utilisez des indicateurs directionnels et des signaux audio pour guider l’utilisateur vers le contenu. Dans de nombreux cas, un guide visuel direct est préférable sur les flèches directionnelles.
* Les indicateurs directionnels ne doivent pas être intégrés au curseur.

### <a name="resources"></a>Ressources

* [Image holographique](holographic-frame.md)

## <a name="data-loading"></a>Chargement de données

Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours. Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer la durée du délai d’attente.

### <a name="device-impact"></a>Impact de l’appareil

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
        <td></td>
    </tr>
     <tr>
        <td>✔️</td>
        <td>✔️</td>
        <td></td>
    </tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleures  |  Présente |  Incident |
--- | --- | ---
|  Indicateur visuel animé, sous la forme d’une barre de progression ou d’un anneau, indiquant la progression pendant le chargement ou le traitement des données. L’indicateur visuel fournit des indications sur la durée de l’attente. | L’utilisateur est informé que le chargement des données est en cours, mais il n’existe aucune indication sur la durée de l’attente. | Aucun chargement de données ou indicateur de processus pour la tâche ne dure plus de 5 secondes. |

### <a name="how-to-measure"></a>Comment mesurer

* Pendant le chargement des données, vérifiez qu’il n’y a pas d’état vide pendant plus de 5 secondes.

### <a name="recommendations"></a>Recommandations

* Fournissez un animateur de chargement des données qui indique la progression dans toutes les situations où l’utilisateur peut percevoir cette application comme étant bloquée ou bloquée. Une règle raisonnable est toute activité de « chargement » qui peut prendre plus de 5 secondes.

### <a name="resources"></a>Ressources

* [Affichage de la progression](progress.md)
