---
title: Suivi de le œil
description: Suivi de le œil
author: sostel
ms.author: sostel
ms.date: 04/05/2019
ms.topic: article
ms.localizationpriority: high
keywords: Suivi des yeux, mixte réalité, entrée, surveillez les regards
ms.openlocfilehash: 948d6ad36bfa3f7b179268a8e6241c9a2ce8e732
ms.sourcegitcommit: c20563b8195c0c374a927b96708d958b127ffc8f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974764"
---
# <a name="eye-tracking-on-hololens-2"></a>Yeux sur HoloLens 2
HoloLens 2 permet un niveau inédite de contexte et la compréhension humaine dans le Holographic expérience en fournissant aux développeurs la possibilité d’incroyable de l’utilisation d’informations sur ce que les utilisateurs regardez. Cette page donne un aperçu de comment les développeurs peuvent tirer profit suivi d’oeil pour différents cas d’utilisation et les solutions à prendre en compte lors de la conception d’interfaces utilisateur basées sur des regards yeux. 

## <a name="use-cases"></a>Cas d’utilisation
Suivi de le œil permet aux applications d’effectuer le suivi de la recherche dans laquelle l’utilisateur en temps réel. Cette section décrit certaines des utilisations potentielles et interactions nouvelle qui devient possibles avec les yeux dans la réalité mixte.
Avant de commencer, dans l’exemple suivant nous mentionne le [Toolkit de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html) plusieurs fois car il fournit plusieurs exemples intéressantes et puissantes pour l’utilisation du suivi des yeux comme rapide et sans effort cible pris en charge des yeux sélections et faire défiler automatiquement texte selon où examine l’utilisateur. 

### <a name="user-intent"></a>Intention de l’utilisateur    
Plus d’informations sur l’endroit où un utilisateur examine fournit un puissant **contexte pour les autres entrées**, comme la voix, mains et contrôleurs.
Cela peut servir pour diverses tâches.
Par exemple, cela peut aller de rapidement et sans effort **ciblant** entre la scène en examinant un hologramme simplement et en indiquant que « select » (voir également [regards de tête et de validation](gaze-and-commit.md)) ou en disant « placez ceci... », puis qui regarde par-dessus où vous voulez placer l’hologramme et dire »... « There ». Vous trouverez des exemples pour ce dans [Toolkit de réalité mixte - sélection de la cible pris en charge des yeux](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html) et [Toolkit de réalité mixte - prise en charge des yeux le positionnement de cible](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Positioning.html).

Un exemple supplémentaire pour l’intention de l’utilisateur peut inclure à l’aide des informations sur les utilisateurs ayant consulté pour améliorer l’engagement avec des agents virtuels incorporées et hologrammes interactives. Par exemple, les agents virtuels peuvent adapter les options disponibles et leur comportement selon actuellement affiché le contenu. 

### <a name="implicit-actions"></a>Actions implicites
La catégorie d’actions implicites est étroitement lié à l’intention de l’utilisateur.
L’idée est que hologrammes ou éléments d’interface utilisateur réagissent de manière quelque peu instinctual qui semble ne peut-être pas encore comme vous interagissez avec le système du tout, mais plutôt que le système et l’utilisateur sont synchronisés. Par exemple, un exemple très réussi est **défilement automatique en fonction des regards yeux**. L’idée est aussi simple : L’utilisateur lit un texte et peut simplement continuer la lecture. Le texte progressivement déplace vers le haut informer les utilisateurs dans leurs flux de lecture. Un aspect clé est que la vitesse de défilement s’adapte à la vitesse de lecture de l’utilisateur.
Un autre exemple est **prise en charge des yeux un zoom avant et panoramique** pour lequel l’utilisateur peut s’apparentent à vous plonger exactement vers qu’il se concentre sur. Déclencher le zoom et en contrôlant la vitesse de zoom peuvent être contrôlés par le biais de voix ou transmettre d’entrée, ce qui est importante à fournir le sentiment de contrôle et éviter de surcharger l’utilisateur (nous aborderons ces instructions de conception plus en détail ci-dessous). Une fois qu’un zoom avant, l’utilisateur peut ensuite sans heurts suivre, par exemple, au cours d’une rue pour Explorer son voisinage simplement à l’aide de leurs regards yeux.
Vous trouverez des exemples de démonstration pour ces types d’interactions dans les [Toolkit de réalité mixte – Navigation pris en charge des yeux](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html) exemple.

Autres utilisations pour _actions implicites_ peuvent inclure :
- **Notifications actives :** Jamais obtenir aurait ennuyé par les notifications dépilant là où vous concentraient ? En prenant en compte dans lequel un utilisateur est actuellement attention à, vous pouvez l’améliorer ! Afficher les notifications décalée par rapport à où l’utilisateur est actuellement à limiter les distractions et automatiquement les ignorer une fois fini sa lecture. 
- **Hologrammes attentifs :** Hologrammes légèrement réagissent lorsque regardée. Cela peut aller à partir des éléments d’interface utilisateur légèrement lumineux, une fleur lentement florissant a de départ compagnie virtuel garder à vous ou essayant d’éviter des regards de vos yeux après un fera prolongée. Cela peut indiquer une idée intéressante de satisfaction dans votre application et de connectivité.

### <a name="attention-tracking"></a>Attention de suivi   
Savoir où rechercher des utilisateurs à est un outil très puissant pour évaluer la facilité d’utilisation de conceptions et à identifier les problèmes de flux de travail efficace. À ce stade, les yeux de visualisation et analytique sont déjà une pratique courante dans différents domaines d’application. Avec 2 HoloLens, nous fournissons une nouvelle dimension à cette présentation comme hologrammes 3D peuvent être placés dans des contextes concrets et évalués en même temps que. Le [Toolkit de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html) fournit des exemples simples pour la journalisation et le chargement des données de suivi de le œil et pour savoir comment les afficher.

Autres applications dans ce domaine peuvent inclure : 
-   **Visualisation des regards œil à distance :** Visualiser les collaborateurs à distance examinez, par exemple, vérifiez si des instructions sont correctement interprétées et suivies.
-   **Études de recherche d’utilisateur :** Attention suivi peut servir à Explorer la manière dont novice ou les utilisateurs experts analyser visuellement le contenu ou leur coordination yeux disponible pour les tâches complexes (par exemple, pour l’analyse des données médicales ou en exploitant des machines).
-   **Analyse des performances et des simulations de formation :** Entraînez-vous et optimiser l’exécution de tâches en identifiant les goulots d’étranglement plus efficacement dans le flux d’exécution.
-   **Concevoir des évaluations, de publicité et de recherche en marketing :** Suivi de le œil est un outil commun pour plusieurs études de marché évaluer les conceptions de site Web et de produit.

### <a name="additional-use-cases"></a>Cas d’utilisation supplémentaires
- **Jeux :** Avez-vous déjà souhaité avoir super-pouvoirs ? Voici votre chance ! Levitate hologrammes en fixant les. Dépanner des faisceaux laser de vos yeux. Transformer des ennemis en pierre ou figez-les ! Utilisez votre vision x-Ray pour explorer des bâtiments. La limite est de votre imagination !  

- **Avatars expressifs :** Yeux contribue à la plus expressifs avatars 3D à l’aide de la date de suivi de le œil en direct pour animer les yeux de l’avatar pour indiquer que l’utilisateur est actuellement affiché. Il ajoute également l’expressivité plus en ajoutant clins de œil et clignote. 

- **Entrée de texte :** Suivi de le œil utilisable comme une alternative intéressante pour l’entrée de texte de l’effort faible en particulier lors de la reconnaissance vocale ou des mains sont peu pratiques à utiliser. 


## <a name="eye-tracking-api"></a>API de suivi des yeux
Avant d’aborder en détail les règles de conception spécifiques pour l’interaction d’OCULAIRE, nous souhaitons brièvement pointent vers les fonctionnalités qui fournit le dispositif de suivi HoloLens 2 yeux. Le [API de suivi des yeux](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose) est accessible via : `Windows.Perception.People.EyesPose`. Il fournit un rayon de regards yeux unique (regards origine et la direction) pour les développeurs.
Le suivi de l’oeil fournit des données sur _30 i/s_.
Les regards prédite yeux se trouve dans l’autorité de certification. 1.0-1,5 degrés visual angle autour du texte réel effectue la recherche sur la cible. Légères imprécisions sont normalement, vous devez planifier une marge autour de cette valeur de limite inférieure. Nous aborderons cela plus ci-dessous. Pour les yeux pour fonctionner correctement, chaque utilisateur est requise à passer par un œil suivi d’étalonnage de l’utilisateur. 

![Taille cible optimal à distance de compteur 2](images/gazetargeting-size-1000px.jpg)<br>
*Taille cible optimal à distance de compteur 2*


## <a name="eye-gaze-design-guidelines"></a>Instructions de conception yeux du pointage de regard
Création d’une interaction qui tire parti de ciblage yeux déplacement rapide peut s’avérer difficile. Dans cette section, nous résumons les principaux avantages et les défis à prendre en compte lors de la conception de votre application. 

### <a name="benefits-of-eye-gaze-input"></a>Avantages de l’entrée des regards œil
- **Haute vitesse pointe.** Le muscle œil est le muscle réaction plus rapide dans notre corps. 

- **Effort faible.** À peine les mouvements physiques sont nécessaires. 

- **Implicitness.** Souvent décrits par les utilisateurs comme « n’oubliez pas d’informations », plus d’informations sur les mouvements des yeux d’un utilisateur informe le système cible les plans utilisateur de s’engager avec. 

- **Autre canal d’entrée.** Les regards yeux peuvent fournir une entrée de la prise en charge puissante pour la main et la voix d’entrée création sur des années d’expérience à partir des utilisateurs en fonction de leur coordination main noir.

- **Attention visuelle.** Un autre avantage important est la possibilité de déduire ce que l’utilisateur s’intéresse aux. Cela peut être utile dans différents domaines d’application en allant plus efficacement l’évaluation des conceptions différentes pour cadrer dans les Interfaces utilisateur plus intelligentes et améliorée des signaux sociales pour la communication à distance.

En bref, à l’aide du pointage de regard yeux comme une entrée offre potentiellement un signal contextuel rapide et sans effort - c’est particulièrement puissant en combinaison avec d’autres entrées comme *voix* et *manuelle* entrée Confirmer l’intention de l’utilisateur.


### <a name="challenges-of-eye-gaze-as-an-input"></a>Défis de œil les regards en tant qu’entrée
Beaucoup d’énergie, s’accompagne un grand nombre de responsabilité : Si les regards yeux peuvent être utilisé pour créer des expériences utilisateur magique une sensation un super héros, il est également important de savoir qu’il n’est pas judicieux au compte pour ce en conséquence. Dans l’exemple suivant, nous aborderons certaines *défis* à prendre en compte et comment les résoudre lorsque vous travaillez avec une entrée du pointage de regard œil : 

- **Votre regard yeux est « always on »** au moment où vous ouvrez votre couvercles yeux, vos yeux démarrer fixation des choses dans votre environnement. Réagir à chaque rechercher marque et émission d’actions potentiellement accidentellement, car vous avez examiné quelque chose pour trop longtemps entraînerait une expérience terrible !
C’est pourquoi nous recommandons combinant des regards yeux avec un *commande vocale*, *main mouvement*, *clic* ou la durée d’affichage étendue pour déclencher la sélection d’une cible.
Cette solution permet également d’un mode dans lequel l’utilisateur peut librement cherchez sans le sentiment écrasant de déclenchement involontaire d’un élément. Ce problème doit également prendre en compte lors de la conception visuelle et auditive commentaires lorsque vous consultez simplement une cible.
Ne pas surcharger les effets immédiats pop-out à l’utilisateur ou pointez les sons. Subtilité est clé ! Lorsque nous parlons de recommandations de conception, nous allons décrire quelques-unes des meilleures pratiques pour cet élément ci-dessous.

- **Observation et contrôle** Imaginez que vous souhaitez aligner précisément une photo sur votre mur. Vous examinez ses bordures et ses environs pour voir si elle s’aligne également. Imaginez maintenant comment cela lorsqu’en même temps que vous souhaitez utiliser votre regard œil en tant qu’entrée pour déplacer l’image. Difficile, non ? Cette section décrit le rôle double des regards d’yeux lorsque cela est nécessaire à la fois pour l’entrée et de contrôle. 

- **Laissez cette option avant de cliquer sur :** Pour les sélections de cible rapide, des études ont montré que regards des yeux d’un utilisateur peut passer avant de conclure un manuel, cliquez sur (par exemple, un airtap). Par conséquent, une attention particulière doit être accordée à synchroniser le signal de regards œil rapide avec l’entrée de contrôle plus lente (par exemple, voix, mains, contrôleur).

- **Petite cibles :** Connaissez-vous le sentiment lorsque vous tentez de lire le texte qui est juste un peu trop petit pour lire correctement ? Ce sentiment de surcharger les yeux qui provoquent vous se sentir fatigué et hors étant donné que vous essayez de réajuster les yeux de mieux se concentrer ?
Il s’agit d’un sentiment que vous pouvez appeler vos utilisateurs lorsque les forcer à sélectionner les cibles trop petites dans votre application utilisant le ciblage des yeux.
Pour votre conception, pour créer une expérience agréable et à l’aise pour vos utilisateurs, nous recommandons que les cibles doivent être au moins 2° dans l’angle visual, de préférence supérieure.

- **En drapeau mouvements des regards yeux** nos yeux effectuer des mouvements rapides de fixation à par fixation. Si vous examinez les chemins d’accès de l’analyse des mouvements des yeux enregistrée, vous pouvez voir leur apparence déséquilibrées. Les yeux déplacement rapidement et de sauts spontanés par rapport à *regards principal* ou *les mouvements de main*.  

- **Fiabilité de suivi :** Suivi de précision de le œil peut dégrader un peu lors de la modification de lumière comme vos yeux adapter aux nouvelles conditions.
Bien que cela ne doit pas affecter nécessairement la conception de votre application, comme la précision ne doit pas dépasser la limitation à 2° mentionnée ci-dessus. Cela peut signifier que l’utilisateur doit s’exécuter une autre d’étalonnage. 


### <a name="design-recommendations"></a>Recommandations de conception
Dans l’exemple suivant, nous indiquons les recommandations de conception spécifiques basées sur les avantages décrits et défis pour les yeux les regards entrée :

1. **Les regards œil ! = regards de tête :**
    - **Prenez en compte si rapide encore yeux déséquilibrées mouvements ajuster votre tâche d’entrée :** Bien que notre mouvements d’oeil rapide et déséquilibrées soient très utile de sélectionner rapidement les cibles sur notre champ de vision, il est moins pertinents pour les tâches qui nécessitent des trajectoires lisses d’entrée (par exemple, pour le dessin ou tournant annotations). Dans ce cas, manuellement ou head pointant doit être préféré.
  
    - **Évitez de quelque chose association directe au regard d’yeux de l’utilisateur (par exemple, un slider ou un curseur).**
Dans le cas d’un curseur, cela peut entraîner l’effet « fuite curseur » en raison des décalages légères dans le signal de regards yeux projetée. Dans le cas d’un curseur, il est en conflit avec le rôle de double de contrôler le curseur avec les yeux tout en voulant également vérifier si l’objet est à l’emplacement correct. En bref, les utilisateurs peuvent rapidement avoir l’impression submergée et gênés, en particulier si le signal est imprécis pour cet utilisateur. 
  
2. **Combiner les yeux regards avec les autres entrées :** L’intégration de suivi des yeux avec les autres entrées, telles que les mouvements de main, les commandes vocales ou appuie sur le bouton, a plusieurs avantages :
    - **Autoriser l’observation gratuitement :** Étant donné que le rôle principal de nos yeux consiste à observer notre environnement, il est important de permettre aux utilisateurs d’observer cet onglet sans déclencher une (visuels, auditifs,...) des commentaires ou des actions. 
    Permet de combiner ET avec un autre contrôle d’entrée pour la transition sans heurts entre les modes de contrôle d’entrée et de d’observation ET.
  
    - **Fournisseur de contexte puissantes :** À l’aide d’informations sur où l’utilisateur consulte lors de la mise en circulation d’une commande vocale ou effectuant un mouvement de la main permet d’acheminement sans effort de l’entrée dans le champ de vision. Par exemple : « Put qui il » rapidement et aisément sélectionner et positionner un hologramme entre la scène en consultant simplement à une cible et une destination. 

    - **Nécessaire pour la synchronisation des entrées multimodales (« ne pas avant de cliquer sur » problème) :** Combinant les mouvements rapides des yeux avec des entrées supplémentaires plus complexes (par exemple, les commandes vocales long ou les mouvements de main) assume le risque de déplacement avec votre regard yeux avant la fin de la commande d’entrée supplémentaire. Par conséquent, si vous créez vos propres contrôles d’entrée (par exemple, les mouvements de main), veillez à ouvrir une session l’apparition de cette durée d’entrée ou approximative à corréler avec qu’un utilisateur avait fixated sur dans le passé.
    
3. **Commentaires subtiles pour l’entrée de suivi de le œil :** Il est utile fournir des commentaires si une cible est examinée (pour indiquer que le système fonctionne comme prévu) mais doit être conservée subtile. Cela peut inclure une fusion lentement en entrée/sortie mises en surbrillance visual ou effectuer d’autres comportements cible subtiles, telles que les mouvements lente (par exemple, légèrement augmentant ainsi la cible) pour indiquer que le système correctement a détecté que l’utilisateur consulte une cible, toutefois, sans inutilement interrompre le flux de travail actuel de l’utilisateur. 

4. **Éviter l’application des mouvements des yeux non naturelles en tant qu’entrée :** Ne forcez pas aux utilisateurs d’effectuer des mouvements des yeux spécifique (mouvements regards) pour déclencher des actions dans votre application.

5. **Compte pour enregistrer les imprécisions dans :** Nous faisons la distinction deux types d’imprécisions qui sont visibles pour les utilisateurs : Décalage et d’instabilité. Le moyen le plus simple aux décalages de l’adresse est de fournir des cibles suffisamment grands pour interagir avec (2° > dans l’angle visual – en tant que référence : votre miniature est environ 2° dans l’angle visual lorsque vous agrandissez votre arm (1)). Il en résulte les conseils suivants :
    - Ne forcez pas aux utilisateurs de sélectionner des cibles minuscules : Research a montré que si les cibles sont suffisamment grandes (et le système est bien conçu), les utilisateurs décrivent l’interaction sans effort et magique. Si les cibles deviennent trop petites, les utilisateurs décrivent l’expérience comme fatigante et frustrante.
    
# <a name="eye-gaze-design-guidelines"></a>Instructions de conception yeux du pointage de regard

Avec 2 HoloLens, nous avons l’occasion idéale pour améliorer les regards & validation plus rapide et plus à l’aise en utilisant des regards de œil au lieu de regards principal. Toutefois, les regards yeux se comportement différemment de regards principal d’une certaine façon et, par conséquent, est fourni avec un nombre de défis uniques. Dans règles de conception les regards yeux, nous résumons les avantages et les défis à prendre en compte lorsque vous utilisez le suivi des yeux comme un moyen d’entrée dans votre application HOLOGRAPHIQUE. Dans cette section, nous nous concentrons sur les considérations de conception spécifiques pour les regards yeux & validation. Tout d’abord, nos yeux extrêmement vite et est donc idéales au ciblage rapidement sur la vue. Cela rend les yeux utilisation idéal pour les regards rapide & Valider les actions en particulier lorsqu’elles sont combinées avec des validations rapides comme un appui en l’air ou bouton press.

Ne pas afficher un curseur : S’il est presque impossible d’interagir sans un curseur lors de l’utilisation de tête les regards, le curseur se transforme rapidement parasites et agaçante lors de l’utilisation du pointage de regard yeux. Au lieu d’utiliser un curseur pour informer l’utilisateur si le suivi de le œil fonctionne et a correctement détecté actuellement consultés sur la cible, visual subtiles utilisation met en évidence (plus de détails ci-dessous).

À tout prix des commentaires subtiles pointage combinées : Ce qui paraît excellent retour visuel pour les regards principal peut entraîner une terrible, écrasant expériences à l’aide du pointage de regard yeux. N’oubliez pas que les yeux sont extrêmement rapides, darting rapidement entre les points de votre champ de vision. Commentaires flickery peuvent entraîner des modifications de mise en surbrillance soudaine rapide (activé/désactivé) lors de la recherche. Par conséquent, lorsque vous fournissez des commentaires de pointage, nous vous recommandons d’utiliser une mise en surbrillance correctement fusionnés dans (et fusionnée à la sortie lors de la recherche de suite). Cela signifie que dans un premier temps vous à peine remarquerait les commentaires lorsque vous examinez une cible. Au cours de 500 à 1000 ms, la mise en surbrillance augmenterait en intensité. Tandis que les utilisateurs novices peuvent continuer à chercher à la cible pour vous assurer que le système a déterminé correctement la cible ayant le focus, les utilisateurs expérimentés pourraient rapidement les regards & sont validées sans attendre que les commentaires sont à son intensité complète. En outre, nous vous recommandons également d’à l’aide de blend montée lorsque atténuant progressivement les commentaires de pointage. Research a montré que les modifications rapides de mouvement et contraste sont très visibles dans votre vision périphérique (par conséquent, la zone de votre champ visuel où vous cherchez pas). Le fondu ne doit pas être lentes en tant que blend dans. Cela est essentiel uniquement lorsque vous avez un contraste élevé ou des modifications de couleur pour votre mise en surbrillance. Si les commentaires de pointage étaient assez subtile pour commencer, vous ne constaterez certainement une différence.

Rechercher des signaux regards et validation de synchronisation : La synchronisation des signaux d’entrée est peut-être moins difficile pour les regards simple & validation, par conséquent, ne vous inquiétez pas ! Il est quelque chose à prendre en compte au cas où vous souhaitez utiliser des actions de validation plus complexes que qui peut impliquer des commandes vocales long ou mouvements de main compliqué. Imaginez que vous examinez cible et prononcez une commande longue vocale. Prise en compte l’heure à laquelle vous avez besoin de parler et l’heure à laquelle le système nécessaires pour détecter ce que vous l’avez dit, votre regard yeux est généralement long passé à une nouvelle cible dans la scène. Par conséquent, apportez vos utilisateurs qu’ils peuvent pas besoin de continuer à chercher à une cible jusqu'à ce que la commande a été reconnue ou gérer l’entrée de manière à déterminer le début de la commande et ce que l’utilisateur avait été regardez à l’époque.

## <a name="see-also"></a>Voir aussi
* [Suivre de la tête et valider](gaze-and-commit.md)
* [Mouvements](gestures.md)
* [Commander avec la voix](voice-design.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Confort](comfort.md)
