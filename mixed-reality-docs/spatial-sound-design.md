---
title: Utiliser un son spatial dans des applications en réalité mixte
description: Le son spatial est un outil puissant pour la conception de l’immersion, de l’accessibilité et de l’expérience utilisateur dans les applications en réalité mixte.
author: kegodin
ms.author: kegodin
ms.date: 11/02/2019
ms.topic: article
keywords: Windows Mixed Reality, son spatial, design, style
ms.openlocfilehash: 34923e1ebfc8e46ea8e67a4444fe3c2691efd4db
ms.sourcegitcommit: 8bf7f315ba17726c61fb2fa5a079b1b7fb0dd73f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2019
ms.locfileid: "75182009"
---
# <a name="how-to-use-sound-in-mixed-reality-applications"></a>Comment utiliser le son dans des applications en réalité mixte

Vous pouvez utiliser le son pour informer et renforcer le modèle mental de l’utilisateur de l’état de l’application. Utilisez Spatialization, le cas échéant, pour placer des sons dans le monde de la réalité mixte. Lorsque vous connectez l’audit et le visuel de cette manière, vous Approfondissez la nature intuitive des interactions et augmentez la confiance de l’utilisateur.
<br><br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/aB3TDjYklmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## <a name="when-to-add-sounds"></a>Quand ajouter des sons
Les applications en réalité mixte ont souvent besoin d’un son plus grand que les applications 2D, en raison de leur manque d’interface tactile. Ajoutez des sons lorsqu’ils informent l’utilisateur ou renforcent les interactions.

### <a name="inform-and-reinforce"></a>Informer et renforcer
* Pour les événements qui ne sont pas initiés par l’utilisateur, tels que les notifications, utilisez le son pour informer l’utilisateur qu’une modification a eu lieu.
* Les interactions peuvent avoir plusieurs étapes. Utilisez le son pour renforcer les transitions d’étape.

Consultez les exemples suivants d’interactions, d’événements et de caractéristiques sonores suggérées.

### <a name="exercise-restraint"></a>Contrainte d’exercice
Les utilisateurs ne disposent pas d’une capacité illimitée pour les informations audio.
* Chaque son doit communiquer des informations précieuses.
* Lorsque votre application émet un son pour informer l’utilisateur, réduisez temporairement le volume des autres sons.
* Pour les sons de pointage de bouton (voir les informations suivantes), ajoutez un délai pour empêcher le déclenchement excessif du son.

### <a name="dont-rely-solely-on-sounds"></a>Ne vous fiez pas uniquement aux sons
Les sons qui sont utilisés correctement sont précieux pour vos utilisateurs. Mais assurez-vous que votre application est utilisable même si le son est désactivé.
* Les utilisateurs peuvent être malentendants.
* Votre application peut être utilisée dans un environnement bruyant.
* Les utilisateurs peuvent avoir des problèmes de confidentialité ou d’autres raisons de désactiver l’audio des appareils.

## <a name="how-to-sonify-interactions"></a>Comment sonify des interactions
Les types d’interaction en réalité mixte incluent le mouvement, la manipulation directe et la voix. Utilisez les caractéristiques suggérées ci-dessous pour sélectionner ou créer des sons pour ces interactions.

### <a name="gesture-interactions"></a>Interactions de mouvement
En réalité mixte, les utilisateurs peuvent interagir avec des boutons à l’aide d’une souris. Les actions de bouton se produisent généralement lorsque l’utilisateur relâche au lieu d’appuyer sur le bouton pour permettre à l’utilisateur d’annuler l’interaction. Utilisez des sons pour renforcer ces étapes. Pour aider les utilisateurs à cibler des boutons distants, envisagez également d’utiliser un son de pointage pointeur.
* Le bouton de pression sur les sons doit être un petit « clic » tactile.<br/>Exemple : [MRTK_ButtonPress. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_ButtonPress.wav)
* Les sons du bouton « dépresse » doivent avoir une apparence tactile similaire. Une tonalité plus élevée que le son de presse renforce le sens de l’achèvement.<br/>Exemple : [MRTK_ButtonUnpress. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_ButtonUnpress.wav)
* Pour les sons sensitifs, envisagez d’utiliser un son discret et non menaçant, tel qu’un Thud ou un bossage à basse fréquence.

### <a name="direct-manipulation"></a>Manipulation directe
Sur HoloLens 2, le suivi articulé prend en charge la manipulation directe des éléments de l’interface utilisateur. Les sons sont importants lorsqu’il n’y a pas d’autres commentaires physiques.

Une *pression sur un bouton* est importante dans la manipulation directe, car l’utilisateur n’obtient aucune autre indication lorsqu’il atteint le bas du trait de touche. Les indicateurs sonores de la course de la clé peuvent être de petite taille, subtile et bloqués. Comme avec les interactions de mouvement, les enfoncements de bouton doivent obtenir un son bref et tactile comme un clic. Les dépressions doivent avoir un son de clic similaire, mais avec un pas de tonalité élevé.
* Exemple : [MRTK_ButtonPress. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_ButtonPress.wav)
* Exemple : [MRTK_ButtonUnpress. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_ButtonUnpress)

Il est difficile de confirmer visuellement une action de manipulation ou de libération. La main de l’utilisateur se trouve souvent dans le sens d’un effet visuel, et les objets qui ne sont pas bien réalisés en dur n’ont pas d’équivalent visuel réel de « saisie ». Les sons peuvent communiquer efficacement avec succès les interactions de capture et de libération.
* Les actions de manipulation doivent avoir un son tactile rapide et légèrement atténué qui évoque l’idée des doigts qui se ferment autour d’un objet. Parfois, il y a également un son « bizarres » qui amène le son de saisie pour communiquer le mouvement de la main.<br/>Exemple : [MRTK_Move_Start. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_Move_Start.wav)
* Les actions de mise en version doivent obtenir un son très bref et tactile. En règle générale, il est plus petit que le son et dans l’ordre inverse, avec un impact, puis un « bizarres » pour indiquer que l’objet est en cours de mise en place.<br/>Exemple : [MRTK_Move_End. wav](https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_development/Assets/MixedRealityToolkit.SDK/StandardAssets/Audio/MRTK_Move_End.wav)

Une interaction de *dessin* doit obtenir un son de bouclage persistant dont le volume est déterminé par le mouvement de la main de l’utilisateur. Elle doit être silencieuse lorsque la main de l’utilisateur est toujours et la plus forte quand la main est rapidement déplacée.

### <a name="voice-interactions"></a>Interactions vocales
Les interactions vocales ont souvent des éléments visuels subtils. Utilisez des sons pour renforcer les étapes d’interaction. Vous souhaiterez peut-être utiliser des sons plus tonals pour les distinguer des sons de mouvement et de manipulation directe.

* Utilisez une tonalité positive pour les *confirmations*de commandes vocales. Les tonalités en hausse et les intervalles musicaux importants sont efficaces.
* Utilisez une tonalité plus rapide et moins positive pour les *échecs*de commande vocale. Évitez les sons négatifs. Au lieu de cela, utilisez un son neutre plus percutant pour communiquer que l’application est en déplacement.
* Si votre application comporte un mot de mise en éveil, utilisez un bref instant lorsque l’appareil *commence à écouter*. Utilisez un son de bouclage subtil pendant que l’application *est* à l’écoute.

### <a name="notifications"></a>Notifications
Les notifications communiquent les modifications d’état de l’application et d’autres événements qui ne sont pas initiés par l’utilisateur, tels que les saisies semi-automatiques de processus, les messages et les appels téléphoniques.

En réalité mixte, les objets sortent parfois du champ de vue de l’utilisateur. Accompagner le déplacement d' *objets animés* avec un son spatial qui dépend du type d’objet et de la vitesse du mouvement.
* Il permet de lire un son spatial à la fin d’une animation pour informer l’utilisateur de la nouvelle position de l’objet.
* Pour les mouvements progressifs, un son « bizarres » pendant le déplacement permet à l’utilisateur de suivre l’objet.

Les sons de *notification de message* peuvent être entendus à plusieurs reprises, parfois en succession rapide. Il est important qu’elles ne soient pas dépendantes ou difficiles. Les sons tonals positifs de milieu de gamme sont efficaces.

* Les sons d’appel entrant doivent avoir des qualités similaires à une sonnerie de téléphone cellulaire. Il s’agit généralement de boucles de musique qui sont lues jusqu’à ce que l’utilisateur réponde à l’appel.
* La connexion et la déconnexion de la communication vocale doivent avoir un son petit et tonal. Le son de la connexion doit être un ton positif pour indiquer une connexion réussie. Le son de déconnexion doit être un signal sonore neutre pour indiquer la fin de l’appel.

## <a name="handle-spatialization"></a>Handle Spatialization
Spatialization utilise des casques ou enceintes stéréo pour placer des sons dans le monde de la réalité mixte.

### <a name="which-sounds-to-spatialize"></a>Les sons à spatialiser
Un son doit être spatial lorsqu’il est associé à un événement qui a un emplacement spatial. Cela comprend l’interface utilisateur, les voix des IA incorporées et les indicateurs visuels.

Spatialiser les éléments de l' *interface utilisateur* pour nettoyer l’espace « espace » de l’utilisateur en limitant le nombre de sons stéréo qu’ils entendent. Les interactions de manipulation, telles que le toucher, la saisie et la libération, semblent plus naturelles quand les commentaires audio sont spatiaux. Tenez compte des informations suivantes sur l’atténuation des distances pour ces éléments.

Spatialer les *indicateurs visuels* et les voix de l' *IA incorporés* pour informer intuitivement les utilisateurs lorsque ces éléments se trouvent en dehors du champ d’affichage.
    
En revanche, évitez Spatialization pour les *voix Faceless ai* et d’autres éléments qui n’ont pas d’emplacement spatial bien défini. Spatialization sans élément visuel associé peut distraire les utilisateurs à penser qu’il y a un élément visuel qu’ils ne peuvent pas trouver.

Spatialization est fourni avec un coût d’UC. De nombreuses applications ont au maximum deux sons lus simultanément. Dans ce cas, le coût de Spatialization est probablement négligeable. Vous pouvez utiliser le moniteur de fréquence d’images MRTK pour évaluer l’impact de l’ajout de Spatialization.

### <a name="when-and-how-to-apply-distance-based-attenuation"></a>Quand et comment appliquer l’atténuation basée sur la distance
Dans le monde physique, les sons qui sont plus éloignés sont plus calmes. Votre moteur audio peut modéliser cette atténuation en fonction de la distance source. Utilisez l’atténuation basée sur la distance lorsqu’elle communique les informations pertinentes.

Les distances par rapport aux *indicateurs visuels*, aux *hologrammes animés*et à d’autres sons informatifs sont généralement pertinentes pour l’utilisateur. Utilisez l’atténuation basée sur la distance pour fournir intuitivement des piles.

Ajustez la courbe d’atténuation pour chaque source en fonction de la taille des espaces de votre monde de réalité mixte. La courbe par défaut de votre moteur audio est souvent destinée à des espaces de très grande taille (jusqu’à demi-kilomètre).

Les sons qui renforcent les *étapes progressives des actions de bouton et d'* autres interactions ne doivent pas être appliqués. Les effets de renforcement de ces sons sont généralement plus importants que la communication entre la distance et le bouton. Les variations peuvent être gênantes, en particulier avec les claviers, lorsque de nombreux clics de bouton peuvent être audibles à la suite.

### <a name="which-spatialization-technology-to-use"></a>La technologie Spatialization à utiliser
Avec les haut-parleurs casque ou HoloLens, utilisez les technologies Spatialization basées sur la fonction de transfert HRTF. Ces technologies modélisent la propagation du son autour de la tête dans le monde physique. Même lorsqu’une source audio se trouve à l’extrémité de l’une des têtes, le son se propage à l’oreille lointaine avec une atténuation et un retard. Le panoramique des orateurs, en revanche, s’appuie uniquement sur l’atténuation et applique une atténuation totale dans l’oreille gauche lorsque les sons se trouvent sur le côté droit (et vice-versa). Cette technique peut ne pas être confortable pour les écouteurs « audition normale » et inaccessible pour les écouteurs qui ont un handicap auditif dans une oreille.

## <a name="next-steps"></a>Étapes suivantes
* [Utiliser un son spatial dans Unity](spatial-sound-in-unity.md)
* [Étude de cas de Roboraid](case-study-using-spatial-sound-in-roboraid.md)
* [Étude de cas de HoloTour](case-study-spatial-sound-design-for-holotour.md)
