---
title: Utilisation de son dans les applications de réalité mixte
description: Le son spatial est un outil puissant pour la conception de l’immersion, de l’accessibilité et de l’expérience utilisateur dans les applications de réalité mixte.
author: kegodin
ms.author: kegodin
ms.date: 11/02/2019
ms.topic: article
keywords: Windows Mixed Reality, son spatial, design, style
ms.openlocfilehash: c069095808eaa9d31b1ffa41dbaa29c9f635837b
ms.sourcegitcommit: 2e54d0aff91dc31aa0020c865dada3ae57ae0ffc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73641062"
---
# <a name="using-sound-in-mixed-reality-applications"></a>Utilisation de son dans les applications de réalité mixte

Utilisez le son pour informer et renforcer le modèle mental de l’utilisateur de l’état de l’application. Utilisez Spatialization, le cas échéant, pour placer des sons dans le monde mixte. La connexion de l’audit et du visuel de cette façon permet d’approfondir la nature intuitive de nombreuses interactions et de renforcer la confiance de l’utilisateur.

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/aB3TDjYklmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## <a name="when-should-i-add-sounds"></a>Quand dois-je ajouter des sons ?
Les applications de réalité mixte ont souvent des besoins plus importants en ce qui concerne les applications sur un écran 2D, en raison de l’absence d’une interface physique. Des sons doivent être ajoutés lorsqu’ils informent l’utilisateur ou renforcent les interactions.

### <a name="inform-and-reinforce"></a>Informer et renforcer
* Pour les événements non initiés par l’utilisateur, tels que les notifications, envisagez d’ajouter des sons pour informer l’utilisateur qu’une modification a eu lieu.
* Les interactions peuvent avoir plusieurs étapes. Envisagez d’utiliser des sons pour renforcer les transitions d’étape.

Voir ci-dessous pour obtenir des exemples d’interactions, d’événements et de caractéristiques sonores suggérées.

### <a name="exercise-restraint"></a>Contrainte d’exercice
Les utilisateurs ne disposent pas d’une capacité illimitée pour les informations audio :
* Chaque son doit communiquer des informations précieuses et spécifiques
* Lorsque vous jouez des sons destinés à informer l’utilisateur, vous réduisez temporairement le volume des autres sons
* Pour les sons de pointage de bouton (voir ci-dessous), ajoutez un délai pour empêcher un déclenchement excessif des sons

### <a name="dont-rely-solely-on-sounds"></a>Ne vous fiez pas uniquement aux sons
Les sons utilisés sont bien utiles lorsque vos utilisateurs peuvent les entendre, mais que votre application est utilisable même si le son est désactivé.
* Les utilisateurs peuvent être malentendants
* Votre application peut être utilisée dans un environnement bruyant
* Les utilisateurs peuvent avoir une confidentialité ou d’autres raisons de désactiver l’audio de l’appareil

## <a name="how-should-i-sonify-interactions"></a>Comment sonify les interactions ?
Les types d’interaction en réalité mixte incluent le mouvement, la manipulation directe et la voix. Utilisez les caractéristiques suggérées ci-dessous pour sélectionner ou créer des sons pour ces interactions.

### <a name="gesture-interactions"></a>Interactions de mouvement
En réalité mixte, les utilisateurs peuvent interagir avec des boutons à l’aide d’un curseur. Les actions de bouton sont généralement effectuées lorsque l’utilisateur a relâché le bouton, plutôt qu’une fois que vous l’avez appuyé, pour permettre à l’utilisateur d’annuler l’interaction. Utilisez des sons pour renforcer ces étapes. En outre, pour aider les utilisateurs à cibler des boutons distants, envisagez d’utiliser un son de survol de curseur.
* Les sons d’appui sur le bouton doivent avoir un clic rapide et tactile. Exemple : [MRTK_ButtonPress. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_ButtonPress.wav)
* Les sons de la dépression du bouton doivent avoir une apparence tactile similaire. Le fait d’avoir une tonalité élevée par rapport au son de presse renforce le sens de l’achèvement. Exemple : [MRTK_ButtonUnpress. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_ButtonUnpress.wav)
* Pour les sons sensitifs, envisagez d’utiliser un son subtil et non menaçant, tel qu’un Thud ou une bosse basse fréquence.


### <a name="direct-manipulation"></a>Manipulation directe
Sur HoloLens 2, le suivi articulé prend en charge la manipulation directe des éléments d’interface utilisateur. Les sons sont des remplacements importants pour l’absence de commentaires physiques.

Une **pression sur un bouton** est importante pour la manipulation directe, car l’utilisateur n’a pas d’indication physique sur le moment où il a atteint le bas du trajet de la touche. Les indicateurs visuels de la course de la clé peuvent être de petite taille, subtile et bloqués. Comme avec les interactions de mouvement, les enfoncements de bouton doivent avoir un son bref et tactile comme un clic, et les dépresseurs doivent avoir un clic similaire avec un pas de hauteur élevé.
* Exemple : [MRTK_ButtonPress. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_ButtonPress.wav)
* Exemple : [MRTK_ButtonUnpress. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_ButtonUnpress)

Il est difficile de communiquer visuellement une **capture** ou une **mise** en service dans une manipulation directe. La main de l’utilisateur se trouve souvent dans le sens d’un effet visuel, et les objets qui ne sont pas bien réalisés en dur n’ont pas d’équivalent visuel réel de « saisie ». En revanche, les sons peuvent communiquer efficacement avec les interactions réussies de capture et de libération.
* Les actions de manipulation doivent avoir un son tactile concis et un peu atténué qui évoque l’idée de la fermeture des doigts autour d’un objet. Parfois, cette opération est accompagnée d’un son « bizarres » conduisant à l’impact du son pour communiquer le mouvement de la main lors de la saisie. Exemple : [MRTK_Move_Start. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_Move_Start.wav)
* Les actions de mise en version doivent avoir un son très bref et tactile, généralement à hauteur du son et dans un ordre inverse dans le temps, ayant un impact, puis une « bizarres » pour communiquer l’objet en position de départ. Exemple : [MRTK_Move_End. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_Move_End.wav)

Une interaction de **dessin** doit avoir un son en boucle et un son persistant dont le volume est contrôlé par le mouvement de la main de l’utilisateur, et il est complètement silencieux lorsque la main de l’utilisateur est toujours, et à son volume maximal lorsque la main de l’utilisateur est déplacée rapidement.



### <a name="voice-interactions"></a>Interactions vocales
Les interactions vocales ont souvent des éléments visuels subtils. Renforcez les étapes d’interaction en utilisant des sons. Envisagez de choisir des sons tonals pour les distinguer des sons de manipulation de mouvement et directs.

* Utilisez une tonalité positive pour les **confirmations**de commandes vocales. Les tonalités en hausse et les intervalles musicaux importants sont efficaces.
* Utilisez un signal sonore plus rapide et moins positif pour l' **échec**de la commande vocale. Évitez les sons négatifs ; au lieu de cela, utilisez un son plus percutant et neutre pour communiquer l’application en passant de l’interaction.
* Si votre application utilise un mot de mise en éveil, utilisez un bref instant, lorsque l’appareil a **commencé à écouter**et un son en boucle subtil pendant que l’application écoute. 

### <a name="notifications"></a>Notifications
Les notifications communiquent les modifications de l’état de l’application et d’autres événements non initiés par l’utilisateur, tels que les saisies semi-automatiques des processus, les messages et les appels.

En réalité mixte, les objets qui se déplacent peuvent sortir du champ de vue de l’utilisateur. Accompagner les **objets animés** avec un son spatial qui dépend de l’objet et de la vitesse du mouvement.
* Il permet également de lire un son spatial à la fin d’une animation pour informer l’utilisateur de la nouvelle position
* Pour les mouvements progressifs, un son « bizarres » pendant le mouvement aide l’utilisateur à effectuer le suivi de l’objet

Les **notifications de messages** seront probablement entendues plusieurs fois, et parfois rapidement. Il est important qu’elle ne se distingue pas ou ne semble pas saine. Les sons tonals de milieu de gamme sont effectifs ici.

* Les appels doivent avoir des qualités similaires à la sonnerie d’un téléphone cellulaire. Il s’agit généralement de boucles de musique qui sont lues jusqu’à ce que l’utilisateur ait répondu à l’appel.
* La connexion et la déconnexion de la communication vocale doivent avoir un son petit et tonal. Le son de la connexion doit avoir un ton positif, indiquant la réussite de la connexion, tandis que le son de déconnexion doit être un signal sonore neutre indiquant la fin de l’appel.

## <a name="spatialization"></a>Spatialization
Spatialization utilise des casques ou enceintes stéréo pour placer des sons dans le monde mixte.

### <a name="which-sounds-should-i-spatialize"></a>Quels sons dois-je spatialiser ?
Un son doit être spatial lorsqu’il est associé à un événement qui a un emplacement spatial. Cela comprend l’interface utilisateur, les voix des IA incorporées et les indicateurs visuels.

L’aménagement des éléments de l' **interface utilisateur** permet de nettoyer l’espace Sonic de l’utilisateur en limitant le nombre de sons stéréo verrouillés à leurs têtes. En particulier, dans les interactions de manipulation directe, le toucher, la saisie et la libération sont plus naturels lorsque les commentaires audio sont spatiaux. Toutefois, voir ci-dessous concernant l’atténuation des distances pour ces éléments.

L’espacement des **indicateurs visuels** et des **voix _incorporées incorporées_**  informe intuitivement les utilisateurs lorsqu’ils sont en dehors du champ de vue.
    
En revanche, évitez de Spatialization pour les **voix _Faceless_ ai**et d’autres éléments sans emplacement spatial bien défini. Spatialization sans élément visuel associé peut distraire les utilisateurs à penser qu’il y a un élément visuel qu’ils ne peuvent pas trouver.

L’ajout de Spatialization sera accompagné d’un coût d’UC. De nombreuses applications auront, au plus, deux sons joués simultanément. Dans ce cas, le coût de Spatialization peut être négligeable. Vous pouvez utiliser le moniteur de fréquence d’images MRTK pour évaluer l’impact de l’ajout de Spatialization. 

### <a name="when-and-how-should-i-apply-distance-based-attenuation"></a>Quand et comment appliquer une atténuation basée sur la distance ?
Dans le monde physique, les sons qui sont plus éloignés sont plus calmes. Votre moteur audio peut modéliser cette atténuation en fonction de la distance source. Utilisez l’atténuation basée sur la distance lorsqu’elle communique les informations pertinentes.

Les distances par rapport aux **indicateurs visuels**, aux **hologrammes animés**et à d’autres sons informatifs sont généralement pertinentes pour l’utilisateur. Utilisez l’atténuation basée sur la distance pour fournir intuitivement cette pile.
* Ajustez la courbe d’atténuation pour chaque source en fonction de la taille de vos espaces de monde mixte. La courbe par défaut de votre moteur audio est souvent destinée à des espaces de très grande taille (jusqu’à demi-kilomètre).

Les sons qui renforcent les **étapes progressives des boutons** et autres interactions ne doivent pas avoir d’atténuation appliquée. Les effets de renforcement de ces sons sont généralement plus importants que la communication entre la distance et le bouton. Les variations peuvent être gênantes, en particulier avec les claviers, où de nombreux clics de bouton seront audibles à la suite.

### <a name="which-spatialization-technology-should-i-use"></a>Quelle technologie Spatialization dois-je utiliser ?
Lors de l’utilisation d’écouteurs ou d’orateurs HoloLens, utilisez des technologies Spatialization basées sur HRTF (fonction de transfert associée à l’en-tête). Ils modélisent la propagation du son autour de la tête dans le monde physique. Même lorsqu’une source sonore est éloignée d’un côté de l’en-tête, le son se propage à l’oreille à distance avec une atténuation et un retard. Le panoramique des orateurs, en revanche, s’appuie uniquement sur l’atténuation, et applique une atténuation totale dans l’oreille gauche lorsque les sons se trouvent sur le côté droit (et vice versa). Cela peut ne pas être à l’aise avec les écouteurs de l’audition normale et inaccessible pour les écouteurs ayant un handicap auditif dans une oreille.

## <a name="next-steps"></a>Étapes suivantes
* [Utiliser un son spatial dans Unity](spatial-sound-in-unity.md)
* [Étude de cas de Roboraid](case-study-using-spatial-sound-in-roboraid.md)
* [Étude de cas de HoloTour](case-study-spatial-sound-design-for-holotour.md)

