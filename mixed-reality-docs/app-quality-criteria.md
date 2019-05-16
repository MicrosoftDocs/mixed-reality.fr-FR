---
title: Critères de qualité des applications
description: Ce document décrit les principaux facteurs ayant un impact sur la qualité des applications de réalité mixte.
author: cjdgit
ms.author: crderr
ms.date: 03/21/2018
ms.topic: article
keywords: critères de qualité des applications, une réalité, mixte mixte des applications en réalité
ms.openlocfilehash: e9f6cd5a6017e11cd167c8141d29b82f89af08e4
ms.sourcegitcommit: 45676da11ebe33a2aa3dccec0e8ad7d714420853
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65628988"
---
# <a name="app-quality-criteria"></a>Critères de qualité des applications

Ce document décrit les principaux facteurs ayant un impact sur la qualité des applications de réalité mixte. Pour chaque facteur les informations suivantes sont fournies
* Vue d’ensemble : une brève description du facteur de qualité et pourquoi il est important.
* Impact de l’appareil - type d’appareil de réalité mixte de fenêtre est affectée.
* Critères de qualité – comment évaluer le facteur de qualité.
* Comment mesurer : méthodes pour mesurer le problème (ou l’expérience).
* Recommandations : résumées des approches pour fournir une meilleure expérience utilisateur.
* Ressources – développement pertinentes et les ressources de conception qui sont utiles pour créer de meilleures expériences d’application.

## <a name="frame-rate"></a>Fréquence d’images

Fréquence d’images est le premier pilier de confort de la stabilité et l’utilisateur hologramme. Fréquence d’images ci-dessous les cibles recommandées peut provoquer hologrammes apparaisse instable, un impact négatif sur le believability de l’expérience et ce qui peut entraîner fatigue des yeux. La fréquence d’images cible pour votre expérience sur des casques IMMERSIFS Windows Mixed Reality sera soit 60 ou 90Hz selon les PC compatibles Windows mixte réalité que vous souhaitez prendre en charge. Pour HoloLens la fréquence d’images cible est de 60Hz.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
| L’application satisfait régulièrement les images par le deuxième objectif (i/s) pour l’appareil cible : 60 i/s sur HoloLens ; 90 i/s sur les PC Ultra ; et 60 i/s sur les PC grand public. | L’application a gouttes de frame intermittents ne pas entraver l’expérience core ; ou i/s est systématiquement inférieurs à l’objectif souhaité, mais n’entrave pas l’expérience de l’application. | L’application rencontre une chute de la fréquence d’images en moyenne de toutes les dix secondes ou moins. |

### <a name="how-to-measure"></a>Comment mesurer

* Un graphique de taux de frame en temps réel est fourni par le biais par la [Windows Device Portal](using-the-windows-device-portal.md#system-performance) sous « Performances du système ».
* Pour le débogage de développement, ajoutez un compteur de diagnostic de taux de trames dans l’application. Consultez les ressources pour un exemple de compteur.
* Supprime des taux de cadre peut être testées dans l’appareil pendant l’exécution de l’application en déplaçant votre tête de gauche à droite. Si l’hologramme indique un mouvement instable inattendu, basse fréquence d’images ou le plan de la stabilité est probablement la cause.

### <a name="recommendations"></a>Recommandations

* Ajouter un compteur de taux de trames au début du travail de développement.
* Les modifications qui peuvent entraîner une baisse de la fréquence d’images doivent être évaluées et correctement résolues comme un bogue de performances.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Fréquence d’images et la stabilité HOLOGRAMME](hologram-stability.md#frame-rate)
* [Budget de performances Asset](asset-creation-process.md)
* [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Affichage du compteur MRToolkit, i/s](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/Utilities/README.md)
* [MRToolkit, Shaders](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit/Utilities/Shaders)

#### <a name="external-references"></a>Références externes

* [Unity, optimisation des applications mobiles](https://www.youtube.com/watch?v=j4YAY36xjwE)

## <a name="hologram-stability"></a>Stabilité HOLOGRAMME

Hologrammes stables augmentera l’utilisation et believability de votre application et créer une expérience d’affichage plus à l’aise pour l’utilisateur. La qualité de la stabilité hologramme est un résultat de développement de la bonne application et la capacité du périphérique (track) de comprendre son environnement. Tandis que la fréquence d’images est le premier pilier de la stabilité, d’autres facteurs peuvent avoir un impact sur la stabilité, y compris :

* Utilisation du plan de stabilisation
* Distance et ancres spatiales
* Suivi

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
|  Hologrammes s’affichent régulièrement stables. | Contenu secondaire présente un mouvement inattendu ; ou un mouvement inattendu n’entrave pas l’expérience de l’application globale. | Contenu principal dans le frame présente un mouvement inattendu. |

### <a name="how-to-measure"></a>Comment mesurer

Tandis que le port de l’appareil et l’expérience d’affichage :

* Déplacer votre tête de gauche à droite, si les hologrammes affichent un mouvement inattendu basse fréquence d’images ou un alignement incorrect du plan de stabilité pour le plan focal est la cause probable.
* Déplacer l’environnement et hologrammes, rechercher des comportements tels que natation et jumpiness. Ce type de déplacement est probablement due à l’analyse de périphérique ne pas l’environnement, ou la distance à l’ancre spatial.
* Si de grands ou hologrammes plusieurs se trouvent dans le frame, observer le comportement de hologramme à différentes profondeurs tandis que le déplacement de votre position principale de gauche à droite, si tremblement apparaît cela est probablement causé par le plan de stabilisation.

### <a name="recomendations"></a>Recommandations

* Ajouter un compteur de taux de trames au début du travail de développement.
* Utilisez le plan de stabilisation.
* Toujours afficher hologrammes ancrés dans 3 mètres de leur point d’ancrage.
* Assurez-vous que votre environnement est configuré pour le suivi approprié.
* Votre expérience afin d’éviter les hologrammes à différents niveaux de profondeur focal dans le cadre de la conception.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Fréquence d’images et la stabilité HOLOGRAMME](hologram-stability.md#frame-rate)
* [Étude de cas, à l’aide du plan de stabilisation](case-study-using-the-stabilization-plane-to-reduce-holographic-turbulence.md)
* [Comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)
* [Ancres spatiales](spatial-anchors.md)
* [Gestion des erreurs de suivi](coordinate-systems.md#handling-tracking-errors)
* [Système de référence stationnaire](coordinate-systems.md#stationary-frame-of-reference)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Kit d’accompagnement MR, Kinect IPD](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

## <a name="holograms-position-on-real-surfaces"></a>Position hologrammes sur des surfaces réels

Distorsions de hologrammes avec des objets physiques (si destinés à être mis en relation avec eux) est une indication claire de l’union de hologrammes et réalistes. Précision de l’emplacement doit être par rapport aux besoins du scénario ; par exemple, placement surface général peut utiliser le mappage spatial, mais plus précise placement nécessitera certains utilisation de marqueurs et d’étalonnage.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
| Hologrammes alignent sur la surface en général dans les centimètres à pouces plage. Si plus de précision est requise, l’application doit fournir un moyen efficace pour la collaboration au sein de la spécification de l’application souhaitée. | N/A | Les hologrammes apparaissent non alignés avec l’objet cible physique par rompre le plan de surface ou qui apparaissent pour les faire flotter en dehors de la surface. Si l’exactitude est requis, hologrammes doivent répondre à la spécification de la proximité du scénario. | 

### <a name="how-to-measure"></a>Comment mesurer

* Hologrammes sont placés sur la carte spatial ne doivent pas apparaître considérablement flotter au-dessus ou au-dessous de la surface.
* Hologrammes qui nécessitent le positionnement précis doivent avoir une forme de marqueur et système d’étalonnage adaptée aux besoins du scénario le.

### <a name="recommendations"></a>Recommandations

* Mappage spatial est utile pour placer des objets sur des surfaces lors de la précision n’est pas nécessaire.
* La meilleure précision, utiliser marqueurs ou des affiches pour déterminer les hologrammes et une manette Xbox (ou un mécanisme d’alignement manuel) d’étalonnage finale.
* Envisagez de diviser hologrammes de très grande taille en parties logiques et d’alignement de chaque partie vers l’aire.
* Mal ensemble interpupilary distance (IPD) peut également un effet sur les alignement hologramme. Configurez toujours HoloLens à IPD de l’utilisateur.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Placement de mappage spatial](spatial-mapping.md#placement)
* [Espace de processus d’analyse](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [Meilleures pratiques d’ancres spatial](spatial-anchors.md#best-practices)
* [Gestion des erreurs de suivi](coordinate-systems.md#handling-tracking-errors)
* [Mappage spatial dans Unity](spatial-mapping-in-unity.md)
* [Vue d’ensemble du développement Vuforia](vuforia-development-overview.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Réalité mixte - Fonctionnalités spatiales - Cours 230 : Mappage spatial](holograms-230.md)
* [MR boîte à outils, bibliothèques de mappage Spatial](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialMapping/README.md)
* [Kit de Compagnon MR, exemple d’étalonnage de Poster](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/PosterCalibrationSample)
* [Kit d’accompagnement MR, Kinect IPD](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/KinectIPD)

#### <a name="external-references"></a>Références externes

* [Étude de cas Lowes, alignement de précision](https://www.youtube.com/watch?v=LceMdyKZ4PI)

## <a name="viewing-zone-of-comfort"></a>Zone d’affichage de confort

Contrôle les développeurs d’applications où les yeux des utilisateurs convergent en plaçant le contenu et hologrammes à des profondeurs différents. Les utilisateurs qui HoloLens inclura toujours à m 2.0 pour maintenir une image claire, car HoloLens affiche sont fixés à une distance optique environ 2.0m éloignée de l’utilisateur. Profondeur de contenu incorrecte peut entraîner une gêne visual ou fatigue.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

<table>
<tr>
<td> Meilleur </td><td><ul>
<li>Placer le contenu à 2m.</li><li>Lorsque hologrammes ne peut pas être placés au 2m et les conflits entre convergence et d’hébergement ne peut pas être évitées, la zone optimale pour la sélection élective hologramme est entre 1,25 m et 5m.</li><li>Dans tous les cas, les concepteurs doivent structurer le contenu à encourager les utilisateurs à interagir 1 + m (par exemple, ajuster la taille du contenu et les paramètres de sélection élective par défaut).</li><li>Sauf si spécifiquement ne pas requis par le scénario, un plan de découpage doit être implémentez avec fadeout en commençant à 1 million.</li><li>Dans les cas où une observation plus proche d’un hologramme immobile est requise, le contenu ne doit pas être à moins de 50cm.</li>
</ul></td>
</tr><tr>
<td> Répond à</td><td> Contenu se trouve dans le Guide de visualisation et de mouvement, mais une utilisation incorrecte ou aucune utilisation du plan de découpage.</td>
</tr><tr>
<td> Échec </td><td> Le contenu est présenté trop près (généralement &lt;1,25 m, ou &lt;50 cm pour hologrammes STATIONNAIRES nécessitant une observation plus proche.)</td>
</tr>
</table>

### <a name="how-to-measure"></a>Comment mesurer

* Contenu doivent être généralement 2m absent, mais ne plus proche que 1,25 ou plus : optez 5m.
* À quelques exceptions près, la distance de rendu de découpage HoloLens doit être définie à .85CM avec fadeout du contenu, en commençant à 1 million. Approche le contenu et notez l’effet de plan de découpage.
* Contenu stationnaire ne doit pas être à moins de 50cm de suite.

### <a name="recommendations"></a>Recommandations

* Concevoir le contenu de la distance d’optimiser l’affichage de 2m.
* Définit la distance de rendu de découpage à 85cm avec fadeout du contenu, en commençant à 1 million.
* Pour hologrammes STATIONNAIRES nécessitant l’affichage de plus près, le plan de découpage doit être non moins de 30 centimètres et fadeout doit commencer au moins 10cm en dehors du plan de découpage.

### <a name="resources"></a>Ressources

* [Restituer la distance](hologram-stability.md#hologram-render-distances)
* [Point de focus dans Unity](focus-point-in-unity.md)
* [Expérimenter la mise à l’échelle](scale.md#experimenting-with-scale)
* [Texte, la taille de police recommandée](typography.md#recommended-font-size)

## <a name="depth-switching"></a>Profondeur de commutation

Quelle que soit la zone d’affichage des problèmes de confort, les demandes de l’utilisateur de basculer rapidement ou fréquemment entre près et présent focal objets (y compris les hologrammes et contenu du monde réel) peuvent entraîner la fatigue oculomotor et de gêne générale.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
|  Profondeur limitée ou naturelle de commutation qui n’entraîne pas l’utilisateur peut se concentrer Queues. | Profondeur brusque commutateur core et conçu dans l’expérience de l’application, ou profondeur brusque qui est provoquée par le contenu réel inattendu. | Commutateur de profondeur cohérent, ou profondeur brusque changement qui n’est pas nécessaire ou core à l’expérience de l’application. | 

### <a name="how-to-measure"></a>Comment mesurer

* Si l’application requiert l’utilisateur de manière cohérente et/ou brusquement définir le focus de profondeur, profondeur est problème de commutation.

### <a name="recommendations"></a>Recommandations

* Conserver le contenu principal à un plan focal cohérent et assurez-vous que le plan de stabilisation correspond à la focale. Cela résoudra oculomotor fatigue et déplacement des hologramme inattendue.

### <a name="resources"></a>Ressources

* [Restituer la distance](hologram-stability.md#hologram-render-distances)
* [Point de focus dans Unity](focus-point-in-unity.md)

## <a name="use-of-spatial-sound"></a>Utilisation de son spatial

En réalité mixte de Windows, le moteur audio fournit le composant auditif de l’expérience de réalité mixte en simulant 3D audio à l’aide de la direction, la distance et les simulations de l’environnement. À l’aide de son spatial dans une application permet aux développeurs de placer convaincante des sons dans un espace tridimensionnel 3 (sphère) autour de l’utilisateur. Ces sons paraîtra comme si elles provenaient d’objets physiques réel ou les hologrammes de réalité mixte dans son environnement de l’utilisateur. Son spatial est un outil puissant pour immersion, d’accessibilité et la conception de l’expérience utilisateur dans les applications de réalité mixte.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
|  Son est logiquement spatialized, et l’expérience utilisateur utilise correctement son afin de faciliter objet découverte et commentaires des utilisateurs. Son est naturel et pertinents aux objets et normalisée entre le scénario. | Audio spatial est utilisé convenablement pour believability mais manquant comme moyen de faciliter la détectabilité et les commentaires des utilisateurs. | Son n’est pas spatialized comme prévu, et/ou manque de son pour aider l’utilisateur au sein de l’expérience utilisateur. Ou spatial audio a été pas considéré comme utilisé dans la conception du scénario. | 

### <a name="how-to-measure"></a>Comment mesurer

* En règle générale, d’émettre des sons pertinentes à partir de hologrammes de cible (par ex., son écorce provenant HOLOGRAPHIQUE dog.)
* Signaux audio doivent être utilisées dans l’expérience utilisateur pour aider l’utilisateur avec des commentaires ou une connaissance des actions en dehors du cadre HOLOGRAPHIQUE.

### <a name="recommendations"></a>Recommandations

* Utilisez audio spatial afin de faciliter les interfaces utilisateur et de découverte de l’objet.
* Sons réels fonctionnent mieux que son non naturelle ou de synthèse.
* La plupart des sons doivent être spatialized.
* Évitez d’émetteurs invisibles.
* Évitez les masques spatiale.
* Normaliser toutes les sons.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Son spatial](spatial-sound.md)
* [Conception du son spatial](spatial-sound-design.md)
* [Son spatial dans Unity](spatial-sound-in-unity.md)
* [Étude de cas, Spatial audio pour HoloTour](case-study-spatial-sound-design-for-holotour.md)
* [Étude de cas, à l’aide de son spatial dans RoboRaid](case-study-using-spatial-sound-in-roboraid.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Réalité mixte - Fonctionnalités spatiales - Cours 220 : Son spatial](holograms-220.md)
* [MRToolkit, Audio Spatial](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit/SpatialSound/README.md)

## <a name="focus-on-holographic-frame-fov-boundaries"></a>Vous concentrer sur les limites du cadre HOLOGRAPHIQUE (angle d’ouverture)

Expériences utilisateur bien conçue peuvent créer et gérer un contexte utile de l’environnement virtuel qui s’étend sur les utilisateurs. Atténuer l’effet des limites d’angle d’ouverture implique une conception réfléchie de contenu à l’échelle et le contexte, utilisez de signal audio spatial, les systèmes de conseils et position de l’utilisateur. Si est correctement effectuée, l’utilisateur semblera étrange qu'inférieur altérée par les limites de l’angle d’ouverture, tout en ayant une expérience d’application à l’aise.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
|  Utilisateur perd jamais le contexte et l’affichage est à l’aise. L’assistance de contexte est fourni pour les objets volumineux. Détectabilité et l’affichage des instructions est fournie pour les objets en dehors du cadre. En règle générale, conception de mouvement et de mise à l’échelle des hologrammes conviennent pour une expérience d’affichage à l’aise. | Utilisateur perd jamais le contexte, mais le mouvement de cou supplémentaire peut être nécessaire dans des situations bien définies. Dans des situations bien définies à l’échelle provoque hologrammes arrêter l’exécution soit le frame vertical ou horizontal à l’origine de certains mouvements cou afficher les hologrammes. | Utilisateur risque de perdre le contexte et/ou de mouvement de cou cohérent est requis pour afficher les hologrammes. Aucune indication de contexte pour les objets volumineux HOLOGRAPHIQUE, déplacement d’objets facile de perdre en dehors du cadre sans les conseils de détectabilité, ni en hauteur hologrammes ne requiert cou régulière à afficher. | 

### <a name="how-to-measure"></a>Comment mesurer

* Contexte pour un hologramme (grand) est perdu ou pas comprise en raison d’être détourée aux limites de le.
* Emplacement de hologrammes sont difficiles à détecter en raison du manque de directeurs d’attention ou du contenu qui déplace rapidement vers et depuis le frame HOLOGRAPHIQUE.
* Scénario nécessite régulière et répétitives haut et bas de mouvement principal pour afficher entièrement un hologramme résultant de fatigue de col.

### <a name="recommendations"></a>Recommandations

* Démarrez l’expérience avec les petits objets ajuster l’angle d’ouverture, puis effectuer la transition des aides visuelles aux versions plus grande.
* Utilisez spatiales directeurs audio et d’attention pour la recherche de contenu utilisateur qui est en dehors de l’angle d’ouverture.
* Autant que possible, évitez hologrammes qui découper verticalement l’angle d’ouverture.
* Fournir à l’utilisateur dans l’application des conseils pour optimiser l’affichage d’emplacement.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Image holographique](holographic-frame.md)
* [Étude de cas, HoloStudio UI et apprentissages de conception d’interaction](case-study-3-holostudio-ui-and-interaction-design-learnings.md?#problem-2-modal-dialogs-are-sometimes-out-of-the-holographic-frame)
* [Mise à l’échelle des objets et des environnements](scale.md)
* [Curseurs, les signaux visuels](cursors.md#visual-cues)

#### <a name="external-references"></a>Références externes

* [Fait beaucoup de bruit sur l’angle d’ouverture](https://www.linkedin.com/pulse/hololens-much-ado-field-of-view-michael-hoffman?lipi=urn%3Ali%3Apage%3Ad_flagship3_feed%3B6iQ%2FbTevLDU93w3I2ewLJw%3D%3D)

## <a name="content-reacts-to-user-position"></a>Contenu réagit à la position de l’utilisateur

Hologrammes doivent réagir à la position de l’utilisateur dans à peu près la même façon que les objets de « vraies ». Une considération de conception importants est éléments d’interface utilisateur qui ne peut pas supposer nécessairement la position de l’utilisateur est à l’arrêt et s’adapter aux mouvements de l’utilisateur. Conception d’une application qui s’adapte correctement à la position de l’utilisateur pour créer une expérience plus crédible et rendre plus facile à utiliser.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

<table>
<tr>
<td> Meilleur </td><td> Contenu et l’interface utilisateur de s’adapter aux positions d’utilisateur qui permet à utilisateur d’interagir naturellement avec le contenu dans l’étendue du mouvement de l’utilisateur attendu.</td>
</tr><tr>
<td> Répond à </td><td> L’interface utilisateur s’adapte à la position de l’utilisateur, mais susceptible de compromettre l’affichage de contenu de clé nécessitant l’utilisateur d’ajuster leur position.</td>
</tr><tr>
<td> Échec </td><td><ol>
<li>Éléments d’interface utilisateur sont perdus ou verrouillés au cours de l’utilisateur entraînant le déplacement des queues revenir à (ou rechercher) des contrôles.</li><li>Éléments d’interface utilisateur restreindre l’affichage du contenu principal.</li><li>Déplacement de l’interface utilisateur n’est pas optimisé pour la distance d’affichage et l’inertie en particulier avec <a href="billboarding-and-tag-along.md">tag-along</a> éléments d’interface utilisateur.</li>
</ol></td>
</tr>
</table>

### <a name="how-to-measure"></a>Comment mesurer

* Toutes les mesures doivent être effectuées dans une étendue raisonnable du scénario. Tandis que le déplacement de l’utilisateur peut varier, n’essayez pas de tromper l’application avec le déplacement des utilisateur extrêmes.
* Pour les éléments d’interface utilisateur, les contrôles appropriés doivent être disponibles quel que soit le mouvement de l’utilisateur. Par exemple, si l’utilisateur est Affichez et vous épargne une carte 3D avec zoom, le contrôle de zoom doit être prête à l’utilisateur, quel que soit l’emplacement.

### <a name="recommendations"></a>Recommandations

* L’utilisateur est l’appareil photo et qu’ils contrôlent le déplacement. Let leur lecteur.
* Prendre en compte le billboarding pour le texte et pour vous déplacer dans les systèmes de rentrer qui seraient sinon être world-verrouillé ou masquées si un utilisateur étaient.
* Utiliser tag-along pour le contenu qui doit suivre l’utilisateur tout en permettant à l’utilisateur de voir ce qui est placé devant.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Conception de l’interaction](hologram.md)
* [Couleur, clair et matériel](color,-light-and-materials.md)
* [Billboarding et tag-along](billboarding-and-tag-along.md)
* [Fonctionnalités de base des interactions](interaction-fundamentals.md)
* [Automatique de mouvement et locomotion de l’utilisateur](comfort.md#self-motion-and-user-locomotion)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Réalité mixte - Entrées - Cours 210 : Pointage du regard](holograms-210.md)

## <a name="input-interaction-clarity"></a>Clarté de l’interaction d’entrée

Clarté de l’interaction d’entrée est essentielle à la facilité d’utilisation d’une application et inclut la cohérence d’entrée, de commodité, de détectabilité des méthodes d’interaction. Utilisateur doit être en mesure d’utiliser des interactions courantes à l’échelle de la plateforme sans efforts d’apprentissage. Si l’application a entrée personnalisée, il doit être clairement communiqué et démontré.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
|  Méthodes d’interaction d’entrée sont cohérents avec la réalité mixte Windows fourni [conseils](interaction-fundamentals.md). Toute entrée personnalisée ne doit pas être redondante avec l’entrée standard (plutôt utiliser l’interaction standard) et doit être clairement communiquée et démontrée à l’utilisateur. | Similaire aux entrées meilleures, mais personnalisées sont redondantes avec les méthodes d’entrée standards. Utilisateur peut toujours atteindre l’objectif et la progression via l’expérience de l’application. | Il est difficile de comprendre le mappage de bouton ou de la méthode d’entrée. Entrée est fortement personnalisée, ne prend pas en charge l’entrée standard, aucune instruction, ou susceptibles de provoquer des problèmes de fatigue et de confort. | 

### <a name="how-to-measure"></a>Comment mesurer

* L’application utilise cohérente [standard d’entrée des méthodes.](interaction-fundamentals.md)
* Si l’application a d’entrée personnalisés, il est clairement communiqué via :
* Expérience de première exécution
* Écrans d’introduction
* Info-bulles
* Coach de main
* Section aide
* VoiceOver

### <a name="recommendations"></a>Recommandations

* Utilisez les méthodes d’entrée standards chaque fois que possible.
* Fournir des démonstrations, des didacticiels et des info-bulles pour les méthodes d’entrée non standards.
* Utiliser un modèle d’interaction cohérente dans toute l’application.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Principes de base Windows MR interaction](interaction-fundamentals.md)
* [Objets sur](interactable-object.md)
* [Pointage du regard](gaze-targeting.md)
* [Curseurs](cursors.md)
* [Confort et regards](comfort.md#gaze-direction)
* [Mouvements](gestures.md)
* [Entrée vocale](voice-input.md)
* [Conception de la voix](voice-design.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Guide de portage des entrées pour Unity](input-porting-guide-for-unity.md)
* [Saisie au clavier dans Unity](keyboard-input-in-unity.md)
* [Pointage du regard dans Unity](gaze-in-unity.md)
* [Mouvements et contrôleurs de mouvement dans Unity](gestures-and-motion-controllers-in-unity.md)
* [Entrée vocale dans Unity](voice-input-in-unity.md)
* [Saisie à l’aide de la commande de jeu, du clavier et de la souris dans DirectX](keyboard,-mouse,-and-controller-input-in-directx.md)
* [HEAD et surveillez les regards dans DirectX](gaze-in-directx.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
* [Entrée vocale dans DirectX](voice-input-in-directx.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Étude de cas : La poursuite de l’informatique plus personnelle](case-study-the-pursuit-of-more-personal-computing.md#less-interface-in-your-face)
* [Étude de cast : HoloStudio UI et apprentissages de conception d’interaction](case-study-3-holostudio-ui-and-interaction-design-learnings.md)
* [Exemple d’application : Tableau périodique des éléments](periodic-table-of-the-elements.md)
* [Exemple d’application : Module de lunaire](lunar-module.md)
* [Réalité mixte - Entrées - Cours 210 : Pointage du regard](holograms-210.md)
* [Réalité mixte - Entrées - Cours 211 : Mouvements](holograms-211.md)
* [Réalité mixte - Entrées - Cours 212 : Voix](holograms-212.md)

## <a name="interactable-objects"></a>Objets sur

Un bouton a longtemps été une métaphore utilisée pour déclencher un événement dans le monde abstrait 2D. Dans le monde en trois dimensions de réalité mixte, nous n’êtes pas obligé d’être limitées à ce monde d’abstraction plus. Quoi que ce soit peut être un objet sur qui déclenche un événement. Un objet sur peut être représenté en tant que quoi que ce soit à partir d’une tasse de café sur la table à une info-bulle flottante en l’air. Quel que soit le formulaire, les objets sur doivent être clairement reconnaissables par l’utilisateur via des signaux visuels et audio.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
|  Quel que soit le formulaire, des objets sur sont reconnaissables par le biais des signaux visuels et audio sur trois états : inactif, ciblées et sélectionné. « Consultez, dites » effacer et de manière cohérente sert tout au long de l’expérience. Les objets sont mis à l’échelle et distribués pour autoriser l’erreur gratuit de ciblage. | Utilisateur peut reconnaître l’objet en tant que sur via des commentaires audio et visuels et cibler et activer l’objet. | Étant donné aucun signaux visual ou audio, utilisateur ne peut pas reconnaître un objet sur. Interactions sont sujettes en raison de l’échelle de l’objet ou la distance entre les objets. | 

### <a name="how-to-measure"></a>Comment mesurer

* Objets sur sont reconnus comme 'sur' ; y compris les boutons, menus et application de contenu spécifique. En règle générale il doit être un indice visuel et audio lors du ciblage des objets sur.

### <a name="recommendations"></a>Recommandations

* Utiliser des commentaires visuels et audio pour les interactions.
* Des commentaires visuels doivent être différenciées pour chaque d’entrée d’état (inactif, ciblé, sélectionné)
* Objets sur doivent être mis à l’échelle et placés par erreur gratuit de ciblage.
* Les objets groupés sur (par exemple, une barre de menus ou de la liste) doivent avoir espacement approprié pour le ciblage.
* Boutons et des menus qui prennent en charge de la commande vocale doivent fournir des étiquettes de texte pour le mot clé de commande (« voir, dites-le »)

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Objet avec interaction possible](interactable-object.md)
* [Texte dans Unity](text-in-unity.md)
* [Barre de l’application et cadre englobant](app-bar-and-bounding-box.md)
* [Conception de la voix](voice-design.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Réalité mixte Toolkit - UX](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="room-scanning"></a>Espace d’analyse

Les applications qui requièrent des données de mappage spatial s’appuient sur l’appareil pour collecter automatiquement ces données au fil du temps et entre les sessions en tant que l’utilisateur explore leur environnement avec l’appareil actif. Le souci d’exhaustivité et la qualité de ces données dépend de plusieurs facteurs, notamment la quantité d’exploration de l’utilisateur a effectué, combien de temps écoulé depuis l’exploration et indique si les objets tels que des portes et meubles ont déplacés depuis le périphérique analyse la zone. De nombreuses applications analysera les données de mappage spatial au début de l’expérience pour déterminer si l’utilisateur doit effectuer des étapes supplémentaires pour améliorer l’exhaustivité et la qualité de la carte spatiale à. Si l’utilisateur est requis pour l’analyse de l’environnement, effacer des conseils doivent être fournis lors de l’expérience d’analyse.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
|  Visualisation de la maille spatiale indiquent aux utilisateurs de l’analyse sont en cours. Utilisateur clairement sait quoi faire lorsque l’analyse démarre et s’arrête. | Visualisation de la maille spatiale est fournie, mais l’utilisateur ne peut pas clairement savoir comment procéder et aucune information de progression est fournie. | Aucune visualisation de la maille. Aucune information de conseils fournie à l’utilisateur concernant où rechercher, ou lorsque l’analyse démarre/arrête. |

### <a name="how-to-measure"></a>Comment mesurer

* Lors d’une analyse de l’espace requis, des conseils visuels et audio sont fourni qui indique où rechercher et quand commencer et l’arrêter l’analyse.

### <a name="recommendations"></a>Recommandations

* Indique la quantité du volume total à proximité des utilisateurs doit faire partie de l’expérience.
* Communiquer lors de l’analyse démarre et s’arrête comme un indicateur de progression.
* Utiliser une visualisation de la maille lors de l’analyse.
* Fournir des signaux visuels et audio pour inciter l’utilisateur à rechercher et vous déplacer dans la salle.
* Informer l’utilisateur où aller pour améliorer les données. Dans de nombreux cas, il peut être préférable d’indiquer à l’utilisateur de ce qu’ils doivent (par exemple, examinez le plafond, recherchez derrière meubles), afin d’obtenir la qualité d’analyse nécessaires.

### <a name="resources"></a>Ressources

#### <a name="documentation"></a>Documentation

* [Visualisation du balayage d’une pièce](room-scan-visualization.md)
* [Étude de cas : Développer les capacités de mappage spatial d’HoloLens](case-study-expanding-the-spatial-mapping-capabilities-of-hololens.md)
* [Étude de cas : Spatiale sonorisation pour HoloTour](case-study-spatial-sound-design-for-holotour.md)
* [Étude de cas : Création d’une expérience d’immersion dans les Fragments](case-study-creating-an-immersive-experience-in-fragments.md)

#### <a name="tools-and-tutorials"></a>Outils et didacticiels

* [Réalité mixte Toolkit - UX](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)

## <a name="directional-indicators"></a>Indicateurs directionnels

Dans une application de réalité mixte, le contenu peut être à l’extérieur du champ de vue ou bloqués par les objets du monde réel. Une application bien conçue rend plus facile pour l’utilisateur rechercher du contenu non visibles. Indicateurs directionnels alerter un utilisateur au contenu important et fournissent des conseils pour le contenu par rapport à la position de l’utilisateur. Conseils pour le contenu non visible peuvent prendre la forme d’émetteurs audio, flèches de direction ou des signaux visuels directs.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
|  Les signaux visuels et audio guident directement vers le contenu approprié à l’extérieur du champ de vue. | Une flèche ou un indicateur qui pointe vers l’utilisateur de la direction générale du contenu. | Le contenu approprié est en dehors du champ de vue et une mauvaise ou aucun guide de l’emplacement n’est fourni à l’utilisateur. | 

### <a name="how-to-measure"></a>Comment mesurer

* Le contenu approprié en dehors de l’utilisateur champ de vision est détectable par le biais des signaux visual et/ou audio.

### <a name="recommendations"></a>Recommandations

* Lorsque le contenu approprié est en dehors du champ de vision de l’utilisateur, utiliser des indicateurs directionnels et signaux audio pour guider l’utilisateur au contenu. Dans de nombreux cas, un guide visuel direct est préféré sur les flèches de direction.
* Les indicateurs de directionnelles ne doivent pas être créés dans le curseur.

### <a name="resources"></a>Ressources

* [Image holographique](holographic-frame.md)

## <a name="data-loading"></a>Chargement des données

Un contrôle de progression offre un retour à l’utilisateur lorsqu’une longue opération est en cours. Cela peut signifier que l’utilisateur ne peut pas interagir avec l’application lorsque l’indicateur de progression est visible et peut également indiquer la durée pendant laquelle le délai d’attente peut être.

### <a name="device-impact"></a>Impact de l’appareil

<table>
<tr>
<th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

### <a name="quality-criteria"></a>Critères de qualité

|  Meilleur  |  Répond à |  Échec |
--- | --- | ---
|  Indicateur visuel animée, sous la forme d’une barre de progression ou un anneau, affichant la progression au cours de toutes les données du chargement ou de traitement. L’indicateur visuel fournit des conseils sur la durée pendant laquelle l’attente pourrait être. | L’utilisateur est informé que le chargement des données est en cours d’exécution, mais il n’existe aucune indication de la durée pendant laquelle l’attente peut être. | Aucun lors du chargement de données ou les indicateurs de processus pour la tâche prend plus de 5 secondes. |

### <a name="how-to-measure"></a>Comment mesurer

* Pendant le chargement de données vérifier le que état n’est pas vide pendant plus de 5 secondes.

### <a name="recommendations"></a>Recommandations

* Fournir une d’animation de chargement de données affichant la progression dans n’importe quelle situation lorsque l’utilisateur peut-être percevoir cette application est bloqué ou est tombé en panne. Une règle empirique raisonnable est toute activité « chargement » qui peut prendre plus de 5 secondes.

### <a name="resources"></a>Ressources

* [Affichage de la progression](progress.md)
