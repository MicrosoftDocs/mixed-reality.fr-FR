---
title: Frame HOLOGRAPHIQUE
description: Les utilisateurs voient le monde de la réalité mixte via le frame HOLOGRAPHIQUE.
author: mavitazk
ms.author: mavitazk
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, réalité mixte Windows, HOLOGRAPHIQUE frame, champ de vision
ms.openlocfilehash: 6773bc03dea471c97d0c6006d2ab7853a5ef3669
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593742"
---
# <a name="holographic-frame"></a>Frame HOLOGRAPHIQUE

Les utilisateurs voient le monde de la réalité mixte via une fenêtre d’affichage rectangulaire alimentée par leur casque. Sur le HoloLens, cette zone rectangulaire est appelée le frame holographique et permet aux utilisateurs de voir le contenu numérique incrustée dans le monde réel autour d’elles. Conception des expériences optimisées pour le frame HOLOGRAPHIQUE crée des opportunités, atténue les défis et améliore l’expérience utilisateur des applications de réalité mixte.

## <a name="designing-for-content"></a>Conception pour le contenu

Souvent, concepteurs ressentez le besoin de limiter l’étendue de leur expérience à ce que l’utilisateur peut voir immédiatement, pour autant sacrifier la mise à l’échelle réelle pour s’assurer que l’utilisateur voit un objet dans son intégralité. De même concepteurs avec des applications complexes surchargent souvent le frame holographique avec du contenu, submerger les utilisateurs avec des interactions difficile et les interfaces encombrés. Les concepteurs de créer du contenu réalité mixte doivent limite pas leur expérience à directement devant l’utilisateur et au sein de leur vue immédiate. Si le monde physique de l’utilisateur est mappé, puis toutes ces surfaces doivent être envisagés un canevas potentiel contenu numérique et les interactions. Une conception appropriée des interactions et du contenu au sein d’une expérience doit encourager l’utilisateur pour vous déplacer dans leur espace, en redirigeant son attention sur le contenu de clé et aider à voir le potentiel de réalité mixte.

Peut-être la plus importante à encourager le déplacement et l’exploration au sein d’une application consiste à **permettent aux utilisateurs d’ajuster l’expérience**. Donner aux utilisateurs un court délai 'libre de la tâche' avec l’appareil. Cela peut être aussi simple que de placer un objet dans l’espace et permettant aux utilisateurs de déplacer ou narration d’introduction à l’expérience. Cette heure doit être libre de toutes les tâches critiques ou spécifiques mouvements (par exemple, air-exercer une pression), à la place l’objectif pour permettre aux utilisateurs de s’adapter à l’affichage de contenu au travers du périphérique avant de nécessiter une interactivité ou progresse via les étapes de l’application. S’il s’agit d’un premier temps utilisateur avec l’appareil, cela est particulièrement important lorsqu’ils ont un contenu de voir à l’aise via le frame holographique et la nature des hologrammes.

### <a name="large-objects"></a>Objets volumineux

Fréquence à laquelle le contenu une expérience appelle pour, contenu réel en particulier, sera supérieure à la trame HOLOGRAPHIQUE. Les objets qui ne rentrent pas normalement dans le cadre HOLOGRAPHIQUE doivent être réduits en conséquence lorsqu’ils sont tout d’abord introduites (à petite échelle ou à distance). La clé est de **permettre aux utilisateurs de voir la taille complète de l’objet** avant la mise à l’échelle inonde le frame. Par exemple, un éléphant HOLOGRAPHIQUE doit être affiché pour tenir entièrement dans le frame, permettant aux utilisateurs former une compréhension spatiale de la forme générale de l’animal, avant de dimensionnement à [mise à l’échelle du monde réel](scale.md) près de l’utilisateur.

Avec la taille complète de l’objet à l’esprit, les utilisateurs doivent ensuite une attente de l’emplacement où déplacer et recherchez des parties spécifiques de cet objet. De même, dans une expérience avec un contenu immersive, il peut aider à avoir un moyen pour faire référence à la taille totale de ce contenu. Par exemple, si l’expérience implique le parcours autour d’un modèle d’une maison virtuel, vous pourriez tenter d’avoir une version réduite de la taille de la maison de poupée de l’expérience que les utilisateurs peuvent déclencher pour comprendre où ils sont à l’intérieur de la maison.

Pour obtenir un exemple de conception pour les objets volumineux, consultez [Volvo Cars](holographic-frame.md#volvo-cars).

### <a name="many-objects"></a>Nombre d’objets

Expériences avec de nombreux objets ou composants doivent prendre en compte pour éviter d’encombrer le frame HOLOGRAPHIQUE directement devant l’utilisateur à l’aide de l’espace complète autour de l’utilisateur. En général, il est conseillé d’introduire de contenu pour une expérience lentement et cela est particulièrement vrai pour les expériences que souhaitez servir un grand nombre d’objets à l’utilisateur. Tout comme avec les objets volumineux, la clé est de **permettent aux utilisateurs de comprendre la disposition du contenu** dans l’expérience, les aidant à acquérir une compréhension spatiale de ce qui est autour d’elles, comme le contenu est ajouté à l’expérience.

Une technique pour y parvenir consiste à fournir des points persistants (également appelés points de repère) dans l’expérience que le contenu d’ancrage dans le monde réel. Par exemple, un repère peut être un objet physique dans le monde réel, tel qu’une table où le contenu numérique s’affiche, ou un objet numérique, comme un ensemble d’écrans d’affichage dans lequel le contenu apparaît fréquemment. Objets peuvent également être placés dans la périphérie de l’image holographique à encourager à orienter vers la clé de contenu, tandis que la recherche de contenu au-delà de la périphérie peut être facilitée par utilisateur [directeurs d’attention](holographic-frame.md#attention-directors).

Placer des objets dans la périphérie peut encourager les utilisateurs pour rechercher vers le côté et cela peut être facilitée par les directeurs d’attention, comme décrit ci-dessous.

## <a name="user-comfort"></a>Confort de l’utilisateur

Pour des expériences de réalité mixte avec les objets volumineux ou de nombreux objets, il est essentiel à prendre en compte la quantité head et déplacement de cou est nécessaire pour interagir avec le contenu. Expériences peuvent être divisés en trois catégories en termes de mouvement de la tête : **Horizontal** (côte à côte) **vertical** (haut et bas), ou **immersives** (horizontal et vertical). Dans la mesure du possible, limitez la majorité des interactions à des catégories horizontales ou verticales, dans l’idéal, avec la plupart des expériences ayant lieu dans le centre de l’image holographique, tandis que la tête de l’utilisateur est dans une position neutre. Évitez les interactions qui provoquent l’utilisateur à déplacer constamment leur affichage à un non naturelles positions principal (par exemple, toujours recherchant pour accéder à une interaction de la clé de menu).

![Région optimale pour le contenu est de 0 à 35 degrés ci-dessous horizon](images/optimal-field-of-view-2-750px.png)<br>
*Région optimale pour le contenu est de 0 à 35 degrés ci-dessous horizon*

Mouvement de la tête horizontale est plus [à l’aise](comfort.md) pour les interactions fréquentes, tandis que les mouvements verticales doivent être réservés pour les événements rares. Par exemple, une expérience impliquant une chronologie horizontale long doit limiter mouvement vertical de la tête pour les interactions (par exemple, pour rechercher vers le bas dans un menu).

Envisager d’encourager des mouvements de corps d’intégral, plutôt que de mouvement de la tête simplement, en plaçant des objets autour de l’espace utilisateur. Expériences de déplacement des objets ou des objets volumineux Prêtez particulièrement attention au mouvement de la tête, en particulier dans lequel ils ont besoin mouvement fréquent sur les deux axes horizontales et verticales.

## <a name="interaction-considerations"></a>Considérations d’interaction

Comme avec le contenu, vous ne sont pas nécessairement limitées à ce que l’utilisateur peut voir immédiatement les interactions dans une expérience de réalité mixte. Interactions peuvent avoir lieu de n’importe où dans l’espace réel autour de l’utilisateur, et ces interactions peuvent aider à encourager les utilisateurs à se déplacer et explorez des expériences.

### <a name="attention-directors"></a>Directeurs de votre attention

Indiquant les points d’intérêt ou les interactions clées peuvent être essentielles aux utilisateurs de progression via une expérience. Attention de l’utilisateur et le déplacement de l’image holographique peuvent être dirigés de manière subtile ou heavy-handed. N’oubliez pas d’équilibrer les directeurs attention avec des périodes de gratuit exploration en réalité mixte (en particulier au début d’une expérience) pour éviter de surcharger l’utilisateur. En règle générale, il existe deux types de directeurs d’attention :
* **Directeurs Visual :** Pour informer l’utilisateur qu’ils doivent déplacer dans un sens spécifique, le plus simple consiste à fournir une indication visuelle. Cela est possible via un effet visuel (par exemple, un chemin d’accès de l’utilisateur peut suivre visuellement vers la partie suivante de l’expérience), voire par des flèches directionnelles simples. Notez que n’importe quel indicateur visuel doit ancrée au sein de l’environnement utilisateur, ne pas 'attaché' pour le frame HOLOGRAPHIQUE ou le curseur.
* **Directeurs audio :** [Son spatial](spatial-sound-design.md) peut fournir un moyen puissant pour établir des objets dans une scène (les utilisateurs d’objets entrant dans une expérience de génération d’alertes) ou attirer l’attention à un point spécifique dans l’espace (pour déplacer la vue de l’utilisateur vers les objets clés). À l’aide de directeurs audio pour guider l’attention des utilisateurs peut être plus subtil et moins importun que directeurs visual. Dans certains cas, il peut être préférable de commencer par un directeur audio, puis passer à un directeur visual si l’utilisateur ne reconnaît pas la file d’attente. Directeurs audio peuvent également être associés aux directeurs visual pour mettre en évidence.

### <a name="commanding-navigation-and-menus"></a>Exécution de commandes, de navigation et de menus

Interfaces dans les expériences de réalité mixte dans l’idéal, sont associés étroitement le contenu numérique qu’ils contrôlent. Par conséquent, menus 2D flottants sont souvent pas idéales pour l’interaction et peuvent être difficiles pour les utilisateurs à confortablement avec à l’intérieur du cadre HOLOGRAPHIQUE. Pour des expériences qui n’ont pas besoin des éléments d’interface tels que les menus ou les champs de texte, envisagez d’utiliser un [(méthode) tag-along](billboarding-and-tag-along.md) à suivre le frame HOLOGRAPHIQUE après un court délai. Éviter le verrouillage du contenu vers le frame comme un affichage tête haute, comme cela peut être désorienté pour l’utilisateur et le saut le sens d’immersion pour d’autres objets numériques dans la scène.

Vous pouvez également envisager de placer des éléments d’interface directement sur spécifique au contenu qu’ils contrôlent, ce qui permet d’interactions se produire naturellement autour d’espace physique de l’utilisateur. Par exemple, arrêter un menu complex en plusieurs parties distinctes. Avec chaque bouton ou un groupe de contrôles attaché à l’objet spécifique affecte l’interaction. Pour aller plus loin dans ce concept, envisagez d’utiliser [sur objets](interactable-object.md).

### <a name="gaze-and-gaze-targeting"></a>Utilisation et ciblant les regards

Le frame HOLOGRAPHIQUE présente un outil pour le développeur aux interactions de déclencheur ainsi évaluer dwells où d’attention de l’utilisateur. [Utilisation](gaze.md) est un du [clé interactions sur HoloLens](interaction-fundamentals.md), où les regards peuvent être associés à [mouvements](gestures.md) (tels qu’avec air-appui) ou [voix](voice-input.md) (permettant ainsi plus court plus naturelles interactions basée sur la voix). Cela rend le HOLOGRAPHIQUE frame par conséquent, un espace en observant le contenu numérique, ainsi que d’interagir avec lui. Si l’expérience appelle permettant d’interagir avec plusieurs objets autour de l’espace utilisateur (par exemple, vous sélectionnez plusieurs objets autour de l’espace utilisateur avec regards + mouvement), envisagez de placer ces objets en vue de l’utilisateur ou de limiter la quantité de tête nécessaire mouvement à promouvoir [confort de l’utilisateur](comfort.md).

Regards peut également servir à effectuer le suivi d’attention de l’utilisateur via une expérience et voir quels objets ou parties de la scène de l’utilisateur payant le plus d’attention à. Cela peut être particulièrement les utiliser pour le débogage d’une expérience permettant à des outils d’analyse comme cartes thermiques pour voir où les utilisateurs passent le plus de temps ou certains objets ou une interaction sont manquantes. Suivi des regards assure également un outil puissant d’animateurs dans les expériences (voir la [cuisine de Lowe](holographic-frame.md#lowes-kitchen) exemple).

## <a name="performance"></a>Performances

Utilisation appropriée de l’image holographique est essentielle à la [qualité des performances](understanding-performance-for-mixed-reality.md) expériences. La surcharge de frame de l’utilisateur avec du contenu numérique, à l’origine d’une dégradation des performances de rendu est un défi courant de techniques (et facilité d’utilisation). Prendre en compte au lieu d’utiliser l’espace complète autour de l’utilisateur pour réorganiser le contenu numérique, en utilisant les techniques décrites ci-dessus, pour alléger le fardeau de rendu et de garantir une qualité d’un affichage optimal.

Contenu numérique dans le cadre de la HoloLens de HOLOGRAPHIQUE permettre également être associé à la [plan de stabilisation](case-study-using-the-stabilization-plane-to-reduce-holographic-turbulence.md) pour des performances optimales et [la stabilité hologramme](hologram-stability.md).

## <a name="examples"></a>Exemples

### <a name="volvo-cars"></a>Volvo Cars

>[!VIDEO https://www.youtube.com/embed/DilzwF90vec]

Dans l’expérience de la salle de Volvo voitures, les clients sont invités à en savoir plus sur les fonctionnalités d’une nouvelle voiture dans une expérience de HoloLens guidée par une association Volvo. Volvo confronté un problème avec le frame HOLOGRAPHIQUE : une voiture en taille réelle est trop volumineuse pour placer juste à côté d’un utilisateur. La solution consistait à commencer l’expérience avec un repère physique, une table centrale dans la salle d’exposition, avec un modèle plus petits numérique de la voiture placé en haut de la table. Cela garantit que l’utilisateur voit la voiture complet lorsqu’elle est introduite, permettant ainsi une idée de présentation spatial, une fois que la voiture a atteint son échelle réalistes plus loin dans l’expérience.

Volvo rencontrer des rend également utiliser des directeurs visual, création d’un effet visuel long à partir du modèle de voiture à petite échelle sur la table à un mur dans la salle. Il en résulte un effet de « fenêtre magique », affichant une vue d’ensemble de la voiture à distance, qui illustre les fonctionnalités supplémentaires de la voiture à l’échelle du monde réel. Le mouvement de la tête est horizontal, sans aucune interaction directe à partir de l’utilisateur (au lieu de cela collecte des signaux visuellement et de narration le Volvo associée de l’expérience).

### <a name="lowes-kitchen"></a>Cuisine de Lowe

Une expérience de magasin à partir de Lowe invite les clients dans une maquette à grande échelle d’une cuisine pour illustrer les diverses possibilités réaménagement comme indiqué par le biais du HoloLens. La cuisine dans le magasin fournit la toile de fond physique pour les objets numériques, un canevas vide d’appliances, countertops et armoires à l’expérience de réalité mixte dérouler.

Les surfaces physique agissent en tant que points de repère statiques pour l’utilisateur à la terre eux-mêmes dans l’expérience, comme les associer d’un Lowe guident l’utilisateur dans les options de produit différents et se termine. De cette façon, l’association peut diriger verbalement de l’attention des utilisateurs à la « réfrigérateur » ou le centre de la cuisine à contenu numérique showcase.

![Association d’un Lowe utilise une tablette à guider les clients grâce à l’expérience de HoloLens.](images/loweskitchen-750px.jpg)<br>
*Association d’un Lowe utilise une tablette à guider les clients grâce à l’expérience de HoloLens.*

En partie, l’expérience utilisateur est géré par une expérience de tablette contrôlée par l’association de la Lowe. Partie du rôle de l’association dans ce cas serait également pour limiter le mouvement d’excessive de la tête, dirigeant sans heurts de leur attention sur les points d’intérêt dans la cuisine. L’expérience de tablette fournit également associé du Lowe du pointage de regard des données sous la forme d’une vue de la carte thermique de la cuisine, aider à comprendre où l’utilisateur est un logement (par exemple, sur une zone spécifique d’habillage) plus précisément leur fournir des conseils de remodelage.

Pour une expérience de cuisine du Lowe façon détaillée, consultez [discours d’ouverture de Microsoft lors de l’Ignite 2016](https://www.youtube.com/watch?v=gC_4JxF0e_k).

### <a name="fragments"></a>Fragments

Dans les Fragments de jeux de HoloLens, vous salon est transformée en scène du crime virtuel indices et les preuves, ainsi qu’une salle de réunion virtuel, où vous parlez avec les caractères qui se trouvent sur votre chaises et appuyer sur votre mur.

![Fragments a été conçu pour avoir lieu dans la page d’accueil d’un utilisateur, avec des caractères d’interagir avec des surfaces et les objets du monde réel.](images/fragments-750px.jpg)<br>
*Fragments a été conçu pour avoir lieu dans la page d’accueil d’un utilisateur, avec des caractères d’interagir avec des surfaces et les objets du monde réel.*

Lorsque les utilisateurs commencent initialement l’expérience, ils sont un court délai d’ajustement, où très peu d’interaction est requise, au lieu de cela en les encourageant à observer cet onglet. Cela vous permet également de garantir que la salle est correctement mappée pour contenu interactif du jeu.

Tout au long de l’expérience, les caractères deviennent des points de référence et agissent comme des directeurs visual (mouvements de la tête entre caractères, l’activation pour rechercher ou mouvements vers les zones d’intérêt). Le jeu s’appuie sur des signaux visuels plus visibles lorsqu’un utilisateur met trop de temps à chercher un objet ou un événement également et utilisation intensive de signal audio spatial (surtout avec voix lors de la saisie d’une scène de caractères).

### <a name="destination-mars"></a>Destination : Mars

Dans la Destination : Expérience de mars vedette à [Kennedy espace Center la NASA](https://blogs.windows.com/devices/2016/09/19/hololens-experience-destination-mars-now-open-at-kennedy-space-center-visitor-complex/), les visiteurs ont été invités dans un aller-retour immersif vers la surface de Mars, guidées par la représentation virtuelle d’astronaut légendaire aldrine Buzz.

![Un aldrine Buzz virtuel devient le point focal pour les utilisateurs de Destination : Mars.](images/destinationmars-750px.png)<br>
*Un aldrine Buzz virtuel devient le point focal pour les utilisateurs de Destination : Mars.*

Comme une expérience d’immersion, ces utilisateurs ont été invités pour observer cet onglet, déplacement leur tête dans toutes les directions pour voir le paysage Martian virtuel. Bien que, pour garantir le confort des utilisateurs, Buzz aldrine narration et présence virtuel fourni un point focal tout au long de l’expérience. Cet enregistrement virtuel buzz (créé par [Studios de Microsoft mixte réalité capturer](https://www.microsoft.com/mixed-reality/capture-studios)) trouvé à la taille réelle, humaine, dans le coin de la salle permettant aux utilisateurs de voir lui dans la vue supérieures. La narration de buzz de diriger les utilisateurs à se concentrer sur différents points dans l’environnement (par exemple, un ensemble de Martian est absolument exceptionnel sur le sol ou une plage de montagne dans la distance) avec les modifications de scène spécifique ou d’objets introduits par lui.

![Les narrators virtuels aura tendance à suivre le déplacement d’un utilisateur, création d’un point focal puissant tout au long de l’expérience.](images/gazereset-750px.png)<br>
*Les narrators virtuels aura tendance à suivre le déplacement d’un utilisateur, création d’un point focal puissant tout au long de l’expérience.*

La représentation sous forme réaliste buzz fourni un point focal puissant, complète avec les techniques de subtiles pour activer le Buzz vers l’utilisateur se sentir comme s’il est, en parlant pour vous. Lorsque l’utilisateur se trouve sur l’expérience, Buzz décale vers vous à un seuil avant de retourner à l’état neutre, si l’utilisateur déplace trop loin au-delà de son périphérie. Si l’utilisateur ressemble à partir de Buzz complètement (par exemple, pour examiner un élément ailleurs dans la scène) puis le reconvertit en Buzz, va de position directionnel du Narrateur qu’une seule fois à nouveau être consacré à l’utilisateur. Techniques ainsi sentiment puissant d’immersion et créer un point de référence dans le cadre HOLOGRAPHIQUE, ce qui réduit le mouvement de la tête excessive et promouvoir [confort de l’utilisateur](comfort.md).

## <a name="see-also"></a>Voir aussi
* [Notions fondamentales d’interaction](interaction-fundamentals.md)
* [Confort](comfort.md)
* [Échelle](scale.md)
* [Ciblage des regards](gaze-targeting.md)
* [Stabilité HOLOGRAMME](hologram-stability.md)
