---
title: Eye-tracking
description: Eye-tracking
author: sostel
ms.author: sostel
ms.date: 04/05/2019
ms.topic: article
ms.localizationpriority: high
keywords: Eye Tracking, eye-tracking, oculométrie, suivi rétinien, suivi du mouvement des yeux, réalité mixte, entrée, suivi du regard, pointage du regard
ms.openlocfilehash: 7298a34a946f86aaf789cfe44ad971169fc8ece3
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66453703"
---
# <a name="eye-tracking-on-hololens-2"></a>Eye-tracking sur HoloLens 2
HoloLens 2 permet d’accéder à un tout nouveau niveau de compréhension contextuelle et humaine au sein de l’expérience holographique en offrant aux développeurs l’incroyable capacité d’utiliser des informations sur ce que les utilisateurs regardent. Cette page fournit une vue d’ensemble des avantages dont peuvent tirer parti les développeurs dans le domaine de l’eye-tracking pour divers cas d’usage. Elle décrit également les éléments à prendre en compte durant la conception d’interfaces utilisateur basées sur le suivi du regard. 

## <a name="use-cases"></a>Cas d’utilisation
L’eye-tracking permet aux applications de savoir où l’utilisateur regarde en temps réel. Cette section décrit certains cas d’usage potentiels ainsi que les nouvelles interactions possibles liées à l’eye-tracking dans le domaine de la réalité mixte.
Avant de commencer, sachez que nous allons mentionner à plusieurs reprises le [Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html), car il fournit de nombreux exemples intéressants et puissants d’utilisation de l’eye-tracking, par exemple le ciblage oculaire rapide et sans effort ainsi que le défilement automatique d’un texte en fonction de l’endroit où l’utilisateur regarde. 

### <a name="user-intent"></a>Intention de l’utilisateur    
Les informations relatives aux mouvements oculaires d’un utilisateur fournissent un **contexte puissant pour d’autres entrées**, par exemple la voix, les mains et les contrôleurs.
Cela peut être utile pour diverses tâches.
Par exemple, cela peut aller du **ciblage** rapide et sans effort en regardant simplement un hologramme et en disant « sélectionner » (consultez également [Suivre de la tête et valider](gaze-and-commit.md)), ou en disant « mettre ceci... », puis en regardant là où vous souhaitez placer l’hologramme, et en disant « là ». Vous trouverez des exemples à ce sujet dans [Mixed Reality Toolkit - Sélection d’une cible à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html) et [Mixed Reality Toolkit - Positionnement d’une cible à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Positioning.html).

Il existe un autre exemple possible d’intention de l’utilisateur. Il consiste à tirer parti des informations relatives à ce que recherchent les utilisateurs pour améliorer l’engagement avec les agents virtuels incorporés et les hologrammes interactifs. Par exemple, les agents virtuels peuvent adapter les options disponibles et leur comportement en fonction du contenu visualisé. 

### <a name="implicit-actions"></a>Actions implicites
La catégorie des actions implicites est étroitement liée à l’intention de l’utilisateur.
L’idée consiste à faire en sorte que les hologrammes ou les éléments d’interface utilisateur réagissent de manière plus ou moins instinctive. Ainsi, il n’est plus vraiment question d’une interaction avec le système mais plutôt d’une synchronisation entre le système et l’utilisateur. Dans ce domaine, le **défilement automatique basé sur le suivi du regard** est un exemple très réussi. L’idée est simple : L’utilisateur lit un texte et peut simplement continuer sa lecture. Le texte défile progressivement en permettant aux utilisateurs de conserver leur flux de lecture. La vitesse de défilement est un aspect clé, car elle s’adapte à la vitesse de lecture de l’utilisateur.
La fonctionnalité de **zoom et défilement panoramique à l’aide du regard** est un autre exemple pour lequel l’utilisateur peut avoir l’impression de plonger exactement vers ce sur quoi il se concentre. Le déclenchement du zoom et le réglage de la vitesse du zoom peuvent être contrôlés par entrée vocale ou manuelle, ce qui est important pour donner une impression de contrôle et éviter de surcharger l’utilisateur (nous en parlerons plus en détail dans les recommandations de conception ci-dessous). Une fois le zoom effectué, l’utilisateur peut suivre en douceur le parcours d’une rue, par exemple, pour explorer son quartier juste par suivi du regard.
Vous trouverez des démonstrations de ces types d’interaction dans l’exemple [Mixed Reality Toolkit - Navigation à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html).

Il existe d’autres cas d’usage supplémentaires pour les _actions implicites_ :
- **Notifications intelligentes :** Avez-vous déjà été ennuyé par des notifications qui apparaissent juste là où vous concentrez votre attention ? En tenant compte de l’endroit où un utilisateur concentre son attention, vous pouvez améliorer son expérience ! Affichez des notifications décalées par rapport à l’endroit où l’utilisateur concentre son attention pour limiter les distractions et les masquer automatiquement une fois la lecture terminée. 
- **Hologrammes attentifs :** Hologrammes qui réagissent subtilement quand vous les regardez. Cela peut aller d’éléments d’IU légèrement brillants ou d’une fleur qui éclot lentement à un animal de compagnie virtuel qui vous rend votre regard ou, au contraire, essaie de l’éviter quand vous le fixez avec insistance. Cela peut donner un sentiment intéressant de connectivité et de satisfaction à l’utilisateur de votre application.

### <a name="attention-tracking"></a>Suivi de l’attention   
Les informations sur les endroits où regardent les utilisateurs constituent un outil extrêmement puissant, qui permet d’évaluer la convivialité de la conception d’une interface et d’identifier les problèmes d’efficacité des flux de travail. Aujourd’hui, la visualisation et l’analyse des données d’eye-tracking sont une pratique courante dans divers domaines d’application. Avec HoloLens 2, nous fournissons une nouvelle dimension à cette compréhension, car les hologrammes 3D peuvent être placés dans des contextes concrets et évalués en même temps. [Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html) fournit des exemples de base pour la journalisation et le chargement des données d’eye-tracking ainsi que leur visualisation.

Autres applications possibles dans ce domaine : 
-   **Visualisation du suivi du regard à distance :** Visualisez ce que les collaborateurs distants regardent. Par exemple, vérifiez que les instructions sont correctement comprises et suivies.
-   **Études de recherche sur les utilisateurs :** Le suivi de l’attention permet de comparer les utilisateurs novices aux utilisateurs experts sur la façon dont ils analysent visuellement du contenu ou sur leur coordination œil-main pour des tâches complexes (l’analyse de données médicales ou le maniement de certains appareils, par exemple).
-   **Simulations d’apprentissage et analyse des performances :** Entraînez-vous et optimisez l’exécution de certaines tâches en identifiant plus efficacement les goulots d’étranglement du flux d’exécution.
-   **Évaluations de conception, études publicitaires et marketing :** L’eye-tracking (ou « suivi oculaire ») est un outil répandu d’étude de marché qui permet d’évaluer l’ergonomie des sites web et des produits.

### <a name="additional-use-cases"></a>Cas d’usage supplémentaires
- **Jeux :** Vous avez toujours souhaité avoir des super pouvoirs ? Voilà votre chance ! Faites léviter les hologrammes en les fixant. Envoyez des rayons laser avec vos yeux. Transformez vos ennemis en pierre ou gelez-les ! Utilisez votre vision à rayons X pour explorer des bâtiments. La seule limite, c’est votre imagination !  

- **Avatars expressifs :** L’eye-tracking contribue à créer des avatars 3D plus expressifs en utilisant des données d’eye-tracking en temps réel pour animer les yeux de l’avatar et indiquer ce que l’utilisateur regarde. Il permet également d’accroître l’expressivité en ajoutant des clins d’œil. 

- **Entrée de texte :** L’eye-tracking peut représenter une solution intéressante pour saisir du texte sans effort, en particulier quand l’usage de la voix ou des mains n’est pas pratique. 


## <a name="eye-tracking-api"></a>API d’eye-tracking
Avant d’entrer dans les détails des recommandations de conception spécifiques à l’interaction par suivi du regard, nous souhaitons souligner brièvement les capacités offertes par le suiveur oculaire HoloLens 2. L’[API d’eye-tracking](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose) est accessible via `Windows.Perception.People.EyesPose`. Elle fournit aux développeurs un seul rayon de suivi du regard (origine et direction du pointage du regard).
Le suiveur oculaire fournit des données à raison de _30 FPS_ (images par seconde) environ.
Le suivi du regard prévu se situe dans un angle visuel compris entre 1,0 et 1,5 degrés autour de la cible observée. Comme de légères imprécisions sont attendues, vous devez prévoir une certaine marge autour de cette valeur de limite inférieure. Nous en discuterons plus en détail ci-dessous. Pour que l’eye-tracking fonctionne avec précision, chaque utilisateur doit effectuer un étalonnage. 

![Taille optimale de la cible à une distance de 2 mètres](images/gazetargeting-size-1000px.jpg)<br>
*Taille optimale de la cible à une distance de 2 mètres*


## <a name="eye-gaze-design-guidelines"></a>Recommandations de conception pour le suivi du regard
Créer une interaction qui tire parti d’un ciblage oculaire rapide peut être une tâche difficile. Dans cette section, nous récapitulons les principaux avantages et défis à prendre en compte durant la conception de votre application. 

### <a name="benefits-of-eye-gaze-input"></a>Avantages liés à l’entrée par suivi du regard
- **Pointage à haute vitesse.** Le muscle oculaire est le muscle le plus réactif de notre corps. 

- **Faible effort.** Pratiquement aucun mouvement physique n’est nécessaire. 

- **Implicite.** Souvent décrites par les utilisateurs comme une « lecture de l’esprit », les informations relatives aux mouvements oculaires d’un utilisateur permettent au système de savoir quelle est la cible de l’utilisateur. 

- **Autre canal d’entrée.** Le suivi du regard peut contribuer de manière importante aux entrées manuelle et vocale grâce aux années d’expérience accumulées dans le domaine de la coordination œil-main des utilisateurs.

- **Attention visuelle.** Pouvoir déduire ce qui intéresse l’utilisateur est un autre avantage important. Cela peut être utile dans divers domaines d’application, allant de l’évaluation plus efficace de différentes conceptions à la création d’interfaces utilisateur plus intelligentes et à l’amélioration des signaux sociaux pour la communication à distance.

En bref, le suivi du regard permet de fournir un signal contextuel rapide et sans effort. Ce signal est particulièrement puissant s’il est utilisé en combinaison avec d’autres entrées telles que les entrées *vocale* et *manuelle* pour confirmer l’intention de l’utilisateur.


### <a name="challenges-of-eye-gaze-as-an-input"></a>Les défis de l’entrée par suivi du regard
Un grand pouvoir implique de grandes responsabilités : Bien que le suivi du regard permette de créer des émotions proches de celles d’un super-héros, il est également important d’en connaître les risques pour l’utiliser de manière appropriée. Dans ce qui suit, nous allons aborder certains *défis* à prendre en compte ainsi que la manière de les résoudre quand vous utilisez l’entrée par suivi du regard : 

- **Votre suivi du regard est « toujours actif »**  : dès que vous ouvrez les paupières, vos yeux fixent les objets de votre environnement. Si tout ce que vous regardez donne lieu à des actions et si votre regard s’attarde trop sur certaines choses, il peut en résulter des effets indésirables et une expérience utilisateur déplaisante !
C’est la raison pour laquelle nous recommandons de combiner le suivi du regard avec une *commande vocale*, un *mouvement de la main*, un *clic sur un bouton* ou un temps d’arrêt prolongé pour déclencher la sélection d’une cible.
Cette solution permet également d’accéder à un mode dans lequel l’utilisateur peut librement regarder autour de lui sans avoir l’impression constante de déclencher quelque chose involontairement. Ce problème doit également être pris en compte durant la conception d’une rétroaction visuelle et auditive quand l’utilisateur regarde simplement une cible.
Ne surchargez pas l’utilisateur avec des effets immédiats d’ouverture dans une nouvelle fenêtre ou des sons de pointage. De la subtilité, voilà la clé ! Nous allons aborder plus loin certaines bonnes pratiques quand nous évoquerons les recommandations de conception.

- **Observation et contrôle** : imaginez que vous souhaitiez aligner avec précision une photo sur un mur. Vous regardez les bords de la photo et ce qui se trouve à proximité pour voir si elle est bien alignée. Maintenant, imaginez comment procéder quand vous souhaitez déplacer l’image par suivi du regard. Difficile, n’est-ce pas ? Cela décrit le double rôle du suivi du regard quand il est nécessaire à la fois pour l’entrée et pour le contrôle. 

- **Quitter avant de cliquer :** Pour les sélections rapides de cibles, des recherches ont montré que le suivi du regard de l’utilisateur se déplace parfois avant un clic manuel (par exemple, un clic aérien). Il est donc nécessaire d’accorder une attention particulière à la synchronisation du signal rapide donné par le suivi du regard avec une entrée de commande plus lente (par exemple la voix, les mains, un contrôleur).

- **Petites cibles :** Avez-vous déjà ressenti cette désagréable sensation quand vous essayez de lire un texte trop petit pour être lu confortablement ? Cette sensation de tension oculaire qui vous fatigue et vous épuise, car vous essayez d’adapter votre vue pour mieux vous concentrer ?
Vous risquez de provoquer cette sensation chez vos utilisateurs quand vous les obligez à sélectionner des cibles trop petites dans votre application à l’aide du ciblage oculaire.
Durant la conception, si vous souhaitez créer une expérience utilisateur agréable et confortable, nous vous recommandons de privilégier des cibles ayant un angle de vue d’au moins 2°, sinon plus de préférence.

- **Mouvements de suivi du regard irréguliers** : nos yeux effectuent des mouvements rapides de fixation en fixation. Si vous examinez un enregistrement des mouvements oculaires, vous pouvez voir qu’ils sont irréguliers. Vos yeux bougent rapidement et sautent spontanément par rapport au *suivi de la tête* ou aux *mouvements de la main*.  

- **Fiabilité du suivi :** La précision de l’eye-tracking peut se dégrader légèrement quand la lumière change, car votre œil s’adapte aux nouvelles conditions.
Bien que cela n’affecte pas nécessairement la conception de votre application, la précision ne doit pas dépasser la limite mentionnée ci-dessus de 2°. Cela peut signifier que l’utilisateur doit exécuter un autre étalonnage. 


### <a name="design-recommendations"></a>Recommandations de conception
Dans ce qui suit, nous énumérons des recommandations de conception spécifiques basées sur les avantages et les défis relatifs au suivi du regard :

1. **Suivi du regard != Suivi de la tête :**
    - **Déterminez si des mouvements oculaires rapides mais irréguliers conviennent à votre tâche de saisie :** Nos mouvements oculaires rapides et irréguliers sont parfaits pour sélectionner rapidement des cibles dans notre champ de vision, mais ils sont moins utiles pour les tâches nécessitant des trajectoires d’entrée lisses (par exemple, dessiner ou entourer des annotations). Dans ce cas, le pointage à la main ou avec la tête est préférable.
  
    - **Évitez d’associer directement quelque chose au suivi du regard de l’utilisateur (par exemple un curseur).**
Dans le cas d’un curseur, cela peut entraîner un effet de « curseur fuyant » en raison de légers décalages dans le signal de suivi du regard projeté. Dans le cas d’un curseur, cela entre en conflit avec le double rôle qui consiste à contrôler le curseur à l’aide des yeux tout en souhaitant également vérifier si l’objet se trouve au bon emplacement. En bref, les utilisateurs peuvent rapidement se sentir submergés et gênés, en particulier si le signal est imprécis. 
  
2. **Combiner le suivi du regard avec d’autres entrées :** L’intégration de l’eye-tracking à d’autres entrées, par exemple les mouvements des mains, les commandes vocales ou les actions visant à appuyer sur un bouton présente plusieurs avantages :
    - **Permettre une observation libre :** Étant donné que le rôle principal de nos yeux est d’observer notre environnement, il est important de permettre aux utilisateurs de regarder autour d’eux sans déclencher de rétroactions ou d’actions (visuelles, auditives, etc.). 
    La combinaison de l’eye-tracking avec un autre contrôle d’entrée permet une transition en douceur entre les modes d’observation par eye-tracking et de contrôle d’entrée.
  
    - **Fournisseur de contexte puissant :** L’utilisation d’informations liées au regard de l’utilisateur en même temps que l’émission d’une commande vocale ou l’exécution d’un mouvement de la main permet de canaliser sans effort l’entrée dans le champ de vision. Par exemple : « Mettre ça là » pour sélectionner et positionner rapidement et facilement un hologramme dans la scène en regardant simplement une cible et une destination. 

    - **Nécessité de synchroniser les entrées multimodales (problème du « quitter avant de cliquer ») :** Si des mouvements oculaires rapides sont combinés avec des entrées supplémentaires plus complexes (par exemple des commandes vocales longues ou des mouvements des mains), l’utilisateur risque de suivre autre chose du regard avant d’achever la commande d’entrée supplémentaire. Ainsi, si vous créez vos propres contrôles d’entrée (mouvements des mains personnalisés, par exemple), veillez à journaliser le début de cette entrée ou sa durée approximative pour la corréler avec ce que l’utilisateur a fixé antérieurement.
    
3. **Rétroaction subtile pour une entrée par eye-tracking :** Il est utile de fournir une rétroaction à l’utilisateur s’il regarde une cible (pour indiquer que le système fonctionne comme prévu), mais celle-ci doit rester subtile. Cela peut inclure des apparitions/disparitions en fondu ou d’autres comportements subtils de la cible, par exemple des mouvements lents (léger grossissement de la cible) pour indiquer que le système a correctement détecté que l’utilisateur regarde une cible, sans toutefois interrompre inutilement son flux de travail. 

4. **Évitez d’appliquer des mouvements oculaires artificiels en tant qu’entrées :** Ne forcez pas les utilisateurs à effectuer des mouvements oculaires spécifiques (mouvements par pointage du regard) pour déclencher des actions dans votre application.

5. **Tenez compte des imprécisions :** Nous distinguons deux types d’imprécision perceptibles par les utilisateurs : le décalage et l’instabilité. Le moyen le plus simple de gérer les décalages consiste à fournir des cibles suffisamment grandes pour rendre une interaction possible (angle visuel > 2° : à titre de référence, votre ongle de pouce a un angle visuel d’environ 2° quand vous tendez le bras (1)). Il en résulte les conseils d’aide suivants :
    - Ne forcez pas les utilisateurs à sélectionner des cibles minuscules : Des recherches ont montré que si les cibles sont suffisamment grandes (et si le système est bien conçu), les utilisateurs décrivent l’interaction comme étant magique et sans effort. Si les cibles deviennent trop petites, les utilisateurs décrivent l’expérience comme étant fatigante et frustrante.
   

## <a name="see-also"></a>Voir également
* [Suivre de la tête et valider](gaze-and-commit.md)
* [Suivre de la tête et du regard dans DirectX](gaze-in-directx.md)
* [Suivi du regard dans Unity (Mixed Reality Toolkit)](https://aka.ms/mrtk-eyes)
* [Mouvements des mains](gestures.md)
* [Entrée vocale](voice-design.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Confort](comfort.md)
