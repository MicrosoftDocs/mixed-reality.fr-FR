---
title: Œil-point de regard
description: HoloLens 2 permet à un nouveau niveau de compréhension du contexte et de l’homme au sein de l’expérience holographique en offrant aux développeurs la possibilité d’utiliser des informations sur ce que les utilisateurs cherchent.
author: sostel
ms.author: sostel
ms.date: 04/05/2019
ms.topic: article
keywords: Suivi oculaire, réalité mixte, entrée, point de regard oculaire
ms.openlocfilehash: 6c51e1cdc2057142f47b6f96e8a1f1aec0bbcc17
ms.sourcegitcommit: 3b32339c5d5c79eaecd84ed27254a8f4321731f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70047104"
---
# <a name="eye-gaze-on-hololens-2"></a>Eye-point de regard sur HoloLens 2
HoloLens 2 permet à un nouveau niveau de compréhension du contexte et de l’homme au sein de l’expérience holographique en offrant aux développeurs la possibilité d’utiliser des informations sur ce que les utilisateurs cherchent. Cette page explique aux développeurs comment ils peuvent tirer parti du suivi oculaire pour divers cas d’usage, ainsi que des éléments à rechercher lors de la conception d’interfaces utilisateur orientées yeux. 


## <a name="device-support"></a>Prise en charge des appareils

<table>
<colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
</colgroup>
<tr>
     <td><strong>Fonctionnalité</strong></td>
     <td><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></td>
     <td><strong>HoloLens 2</strong></td>
     <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
</tr>
<tr>
     <td>Œil-point de regard</td>
     <td>❌</td>
     <td>✔️</td>
     <td>❌</td>
</tr>
</table>

## <a name="use-cases"></a>Cas d’usage
L’eye-tracking permet aux applications de savoir où l’utilisateur regarde en temps réel. Les cas d’usage suivants décrivent certaines interactions possibles avec le suivi oculaire en réalité mixte.
N’oubliez pas que le [Kit d’outils de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html) est utile pour fournir plusieurs exemples intéressants et puissants pour l’utilisation du suivi oculaire, tels que des sélections de cibles rapides et faciles à prendre en charge par l’œil, ainsi que pour faire défiler automatiquement le texte en fonction de ce à quoi l’utilisateur regarde. 

### <a name="user-intent"></a>Intention de l’utilisateur    
Des informations sur l’emplacement et le rôle d’un utilisateur fournissent un **contexte puissant pour d’autres entrées**, telles que la voix, les mains et les contrôleurs.
Cela peut être utile pour diverses tâches.
Par exemple, cette opération peut être effectuée rapidement et facilement sur la scène en regardant simplement un hologramme et en disant «sélectionner» (voir également le point d’insertion [et de validation](gaze-and-commit.md)de la tête) ou en disant «placer cela...», puis en regardant à l’endroit où l’utilisateur veut placer l’hologramme et dites «... là». Vous trouverez des exemples à ce sujet dans [Mixed Reality Toolkit - Sélection d’une cible à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html) et [Mixed Reality Toolkit - Positionnement d’une cible à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Positioning.html).

En outre, un exemple d’intention de l’utilisateur peut inclure des informations sur ce que les utilisateurs cherchent pour améliorer l’engagement avec des agents virtuels et des hologrammes interactifs. Par exemple, les agents virtuels peuvent adapter les options disponibles et leur comportement en fonction du contenu actuellement affiché. 

### <a name="implicit-actions"></a>Actions implicites
La catégorie des actions implicites est étroitement liée à l’intention de l’utilisateur.
L’idée est que les hologrammes ou les éléments d’interface utilisateur réagissent de façon quelque peu instinctual, qui peut même ne pas se comporter comme l’utilisateur qui interagit avec le système, mais plutôt que le système et l’utilisateur sont synchronisés. Par exemple, le **défilement automatique orienté vers le regard** de l’utilisateur lit le texte lorsque le texte continue à faire défiler ou à se synchroniser avec le regard de l’utilisateur. Un aspect clé de cela est que la vitesse de défilement s’adapte à la vitesse de lecture de l’utilisateur.
Un autre exemple est un **Zoom et un panoramique pris en charge par l’œil,** où l’utilisateur peut sembler se plonger exactement sur ce qu’il est concentré. Le déclenchement du zoom et du contrôle de la vitesse de zoom peut être contrôlé par des entrées vocales ou de la main, ce qui est important pour fournir à l’utilisateur le sentiment de contrôle tout en évitant d’être submergé. Nous parlerons des instructions de conception plus en détail ci-dessous. Une fois le zoom avant effectué, l’utilisateur peut suivre facilement, par exemple, le cours d’une rue pour explorer son voisinage en utilisant simplement son regard.
Vous trouverez des démonstrations de ces types d’interaction dans l’exemple [Mixed Reality Toolkit - Navigation à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html).

Des cas d’usage supplémentaires pour les _actions implicites_ peuvent inclure:
- **Notifications intelligentes :** Avez-vous déjà été ennuyé par des notifications qui apparaissent juste là où vous concentrez votre attention ? En tenant compte de ce à quoi un utilisateur fait attention, vous pouvez améliorer cette expérience en décalant les notifications à partir de l’endroit où l’utilisateur est actuellement Gazing. Cela limite les distractions et les ignore automatiquement une fois que l’utilisateur a terminé la lecture. 
- **Hologrammes attentifs :** Des hologrammes qui réagissent à la légère sur le regard. Cela peut aller de quelques éléments d’interface utilisateur à une fleur très lente à un animal de compagnie virtuel, commençant à regarder l’utilisateur ou à essayer d’éviter l’oeil de l’utilisateur après une étoile prolongée. Cette interaction peut fournir un sens intéressant de la connectivité et de la satisfaction dans votre application.

### <a name="attention-tracking"></a>Suivi de l’attention   
Des informations sur l’emplacement ou les utilisateurs qui regardent sont un outil très puissant pour évaluer la convivialité des conceptions et pour identifier les problèmes dans les flux de travail efficaces. La visualisation et l’analyse du suivi oculaire sont une pratique courante dans différents domaines d’application. Avec HoloLens 2, nous fournissons une nouvelle dimension à cette compréhension, car les hologrammes 3D peuvent être placés dans des contextes réels et évalués en conséquence. La [boîte à outils de la réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html) fournit des exemples de base pour la journalisation et le chargement des données de suivi visuel et comment les visualiser.

Les autres applications de cette zone peuvent inclure: 
-   **Œil à distance-visualisation du regard:** Visualisez ce que les collaborateurs distants examinent pour vérifier si les instructions sont correctement comprises et suivies.
-   **Études de recherche sur les utilisateurs :** Le suivi de l’attention peut être utilisé pour explorer la manière dont les utilisateurs débutants ou expérimentés analysent le contenu visuellement, ou comment leur coordination manuelle pour les tâches complexes, telles que l’analyse des données médicales ou les machines à fonctionner.
-   **Simulations d’apprentissage et analyse des performances :** Entraînez-vous et optimisez l’exécution de certaines tâches en identifiant plus efficacement les goulots d’étranglement du flux d’exécution.
-   **Évaluations de conception, études publicitaires et marketing :** Le suivi oculaire est un outil courant pour les recherches sur le marché lors de l’évaluation des conceptions de site Web et de produit.

### <a name="additional-use-cases"></a>Cas d’usage supplémentaires
- **Jeux :** Vous avez toujours souhaité avoir des super pouvoirs ? Voilà votre chance ! Vous pouvez faire en lévitation les hologrammes. Envoyez des rayons laser avec vos yeux. Transformez des ennemis en pierres ou figez-les. Utilisez votre vision à rayons X pour explorer des bâtiments. La seule limite, c’est votre imagination !  

- **Avatars expressifs :** Le suivi des yeux permet d’obtenir des avatars 3D plus expressifs en utilisant des données de suivi visuel actif pour animer les yeux de l’avatar qui indiquent ce que l’utilisateur examine. Il ajoute également plus d’expressivité en ajoutant des clignotements. 

- **Entrée de texte :** Le suivi oculaire peut être utilisé comme alternative pour une entrée de texte à faible effort, en particulier lorsque la parole ou les mains sont peu pratiques à utiliser. 


## <a name="eye-tracking-api"></a>API d’eye-tracking
Avant de décrire en détail les règles de conception spécifiques pour l’interaction avec le regard des yeux, nous souhaitons rapidement souligner les fonctionnalités fournies par l’API de suivi oculaire HoloLens 2 aux développeurs. Il fournit un point d’origine et une direction orientés vers l’œil, en fournissant des données à environ _30 Hz_. 

Le point de regard prédit se trouve dans l’autorité de certification. 1,0-1,5 degrés dans l’angle visuel autour de la cible réelle. Comme de légères imprécisions sont attendues, vous devez prévoir une certaine marge autour de cette valeur de limite inférieure. Nous en discuterons plus en détail ci-dessous. Pour que l’eye-tracking fonctionne avec précision, chaque utilisateur doit effectuer un étalonnage. 

![Taille optimale de la cible à une distance de 2 mètres](images/gazetargeting-size-1000px.jpg)<br>
*Taille de cible optimale à une distance de 2 mètres*
<br>
<br>
L' [API de suivi oculaire](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose) est accessible via: 'Windows. perception. People. EyesPose'. 

## <a name="calibration"></a>Auto 
Pour que l’eye-tracking fonctionne avec précision, chaque utilisateur doit effectuer un étalonnage. Sur HoloLens 2, l’utilisateur est invité à étalonner les visuels pendant la configuration de l’appareil, en examinant l’ensemble des cibles de fixation. Cela permet à l’appareil d’ajuster l’appareil pour une expérience d’affichage confortable et de qualité pour l’utilisateur et garantir un suivi visuel précis en même temps.  L’étalonnage doit fonctionner pour la plupart des utilisateurs, mais dans certains cas, il se peut que l’utilisateur ne puisse pas l’étalonner correctement.  Pour en savoir plus sur l’étalonnage, vérifiez l' [étalonnage](https://docs.microsoft.com/en-us/windows/mixed-reality/calibration).

## <a name="eye-gaze-design-guidelines"></a>Conseils pour la conception des regards
La création d’une interaction qui tire parti du ciblage visuel à déplacement rapide peut être difficile. Dans cette section, nous résumerons les principaux avantages et défis à prendre en compte lors de la conception de votre application. 

### <a name="benefits-of-eye-gaze-input"></a>Avantages de l’entrée en regard des yeux
- **Pointage à haute vitesse.** Le muscle oculaire est le muscle le plus rapide dans le corps humain. 

- **Faible effort.** Pratiquement aucun mouvement physique n’est nécessaire. 

- **Implicite.** Souvent décrits par les utilisateurs comme «sens de lecture», les informations relatives aux mouvements oculaires d’un utilisateur permettent au système de savoir à quelle cible l’utilisateur envisage de s’impliquer. 

- **Autre canal d’entrée.** L’œil-point de vue peut fournir une entrée de prise en charge puissante pour les entrées de main et vocales, basées sur des années d’expérience des utilisateurs en fonction de leur coordination manuelle.

- **Attention visuelle.** Un autre avantage important est la possibilité de déduire ce à quoi un utilisateur fait attention. Cela peut aider dans différents domaines d’application, allant de l’évaluation plus efficace de conceptions différentes à l’aide d’interfaces utilisateur plus intelligentes et de signaux sociaux améliorés pour la communication à distance.

Pour résumer, l’utilisation de l’œil en forme de point d’entrée offre un signal contextuel rapide et sans effort. Cela est particulièrement puissant lorsqu’il est combiné à d’autres entrées, telles que la *voix* et l’entrée *manuelle* , pour confirmer l’intention de l’utilisateur.


### <a name="challenges-of-eye-gaze-as-an-input"></a>Défis de l’entrée
Avec un grand nombre d’énergie, la responsabilité est importante.
Bien qu’il soit possible d’utiliser des yeux pour créer des expériences utilisateur satisfaisantes, il est également important de savoir ce qu’il n’est pas judicieux de prendre en compte. Ce qui suit présente certains *défis* à prendre en compte, ainsi que la façon de les résoudre quand vous travaillez avec des entrées de regard: 

- **Votre regard est «Always on»** Le moment où vous ouvrez vos couvercles oculaires, vos yeux commencent que sur les choses de l’environnement. En réagissant à chaque fois que vous effectuez des actions et que vous émettez accidentellement des actions, parce que vous avez examiné un peu trop de temps, cela entraînerait une insatisfaction de l’expérience.
Par conséquent, nous vous recommandons de combiner Eye-regard avec une *commande vocale*, un *mouvement manuel*, un *clic de bouton* ou un logement étendu pour déclencher la sélection d’une cible.
Cette solution permet également à un mode dans lequel l’utilisateur peut effectuer des recherches librement sans être submergé par le déclenchement involontaire d’un événement. Ce problème doit également être pris en compte lors de la conception de commentaires visuels et auditifs quand vous examinez simplement une cible.
Ne surchargez pas l’utilisateur avec des effets immédiats d’ouverture dans une nouvelle fenêtre ou des sons de pointage. La subtilité est essentielle. Nous allons aborder plus loin certaines bonnes pratiques quand nous évoquerons les recommandations de conception.

- **Observation et contrôle** Imaginez que vous souhaitez redresser précisément une photographie sur votre mur. Vous regardez les bords de la photo et ce qui se trouve à proximité pour voir si elle est bien alignée. Imaginez maintenant comment procéder lorsque vous souhaitez utiliser le point de vue de l’œil pour déplacer l’image. Difficile, n’est-ce pas ? Cela décrit le double rôle de regard pour les entrées et les contrôles. 

- **Quitter avant de cliquer :** Pour les sélections de cibles rapides, l’étude a montré que le point de vue de l’utilisateur peut se déplacer avant de conclure un clic manuel (par exemple, un airtap). Par conséquent, une attention particulière doit être accordée à la synchronisation du signal rapide oeil-regard avec une entrée de contrôle plus lente (par exemple, voix, mains, contrôleur).

- **Petites cibles :** Savez-vous le sentiment quand vous essayez de lire du texte qui est un peu trop petit pour le lire confortablement? Ce sentiment de stress sur vos yeux peut vous amener à vous sentir fatigué et à s’en ressentir, car vous essayez de réajuster vos yeux pour mieux vous concentrer.
C’est un sentiment que vous pouvez appeler dans vos utilisateurs en les forçant à sélectionner des cibles qui sont trop petites dans votre application à l’aide d’un ciblage oculaire.
Durant la conception, si vous souhaitez créer une expérience utilisateur agréable et confortable, nous vous recommandons de privilégier des cibles ayant un angle de vue d’au moins 2°, sinon plus de préférence.

- **Mouvements de regard en œil irrégulier** Nos yeux effectuent des mouvements rapides de la fixation à la fixation. Si vous examinez un enregistrement des mouvements oculaires, vous pouvez voir qu’ils sont irréguliers. Vos yeux bougent rapidement et sautent spontanément par rapport au *suivi de la tête* ou aux *mouvements de la main*.  

- **Fiabilité du suivi :** La précision de l’eye-tracking peut se dégrader légèrement quand la lumière change, car votre œil s’adapte aux nouvelles conditions.
Même si cela ne doit pas nécessairement affecter la conception de votre application, car la précision doit être comprise dans la limite de 2 °, il peut être nécessaire que l’utilisateur l’étalonne à nouveau. 


## <a name="design-recommendations"></a>Recommandations de conception
La liste suivante répertorie les recommandations de conception spécifiques en fonction des avantages et des défis décrits pour les entrées de regard:

1. **L’œil-point de regard n’est pas le même que le point de regard:**
    - **Déterminez si des mouvements oculaires rapides mais irréguliers conviennent à votre tâche de saisie :** Si nos mouvements oculaires rapides et irréguliers sont très utiles pour sélectionner rapidement des cibles dans notre champ de vue, elles sont moins applicables aux tâches qui nécessitent des trajectoires d’entrée lisses (par exemple, des annotations de dessin ou de cercle). Dans ce cas, le pointage à la main ou avec la tête est préférable.
  
    - **Évitez de joindre un texte directement à l’oeil de l’utilisateur (par exemple, un curseur ou un curseur).**
Dans le cas d’un curseur, cela peut entraîner l’effet de «curseur Fleeing» en raison de légers décalages dans le signal de point de regard projeté. Dans le cas d’un curseur, il peut entrer en conflit avec le double rôle de contrôle du curseur avec vos yeux, tout en souhaitant vérifier si l’objet se trouve à l’emplacement approprié. Pour résumer, les utilisateurs peuvent devenir submergés et perturbés, en particulier si le signal n’est pas précis pour cet utilisateur. 
  
2. **Combinez les yeux avec d’autres entrées:** L’intégration du suivi oculaire avec d’autres entrées, telles que les gestes manuels, les commandes vocales ou les enfoncements de bouton, offre plusieurs avantages:
    - **Permettre une observation libre :** Étant donné que le rôle principal de nos yeux est d’observer notre environnement, il est important que les utilisateurs soient autorisés à regarder sans déclencher les commentaires ou les actions (visuel, audit, etc.). 
    La combinaison du suivi oculaire et d’un autre contrôle d’entrée permet une transition sans heurts entre l’observation du suivi oculaire et les modes de contrôle d’entrée.
  
    - **Fournisseur de contexte puissant :** L’utilisation d’informations sur l’emplacement et le rôle de l’utilisateur lors de la mise en circulation d’une commande vocale ou de l’exécution d’un mouvement manuel permet de canaliser en toute transparence l’entrée dans le champ de la vue. Exemple : « Mettre ça là » pour sélectionner et positionner rapidement et facilement un hologramme dans la scène en regardant simplement une cible et une destination. 

    - **Nécessité de synchroniser les entrées multimodales (problème du « quitter avant de cliquer ») :** La combinaison rapide de mouvements oculaires avec des entrées supplémentaires plus complexes, telles que des commandes vocales longues ou des gestes de main, risque de poursuivre votre attention avant de terminer la commande d’entrée supplémentaire. Par conséquent, si vous créez vos propres contrôles d’entrée (par exemple, des gestes personnalisés), veillez à consigner le début de cette entrée ou la durée approximative pour la mettre en corrélation avec le point de regard d’un utilisateur dans le passé.
    
3. **Rétroaction subtile pour une entrée par eye-tracking :** Il est utile de fournir des commentaires lorsqu’une cible est examinée pour indiquer que le système fonctionne comme prévu, mais qu’il doit rester discret. Cela peut inclure la fusion lente, l’inversion et l’extraction, les surbrillances visuelles ou l’exécution d’autres comportements de cible subtils, tels que des mouvements lents, tels que l’amélioration de la taille cible, pour indiquer que le système a détecté correctement que l’utilisateur regarde une cible sans interruption inutile du flux de travail actuel de l’utilisateur. 

4. **Évitez d’appliquer des mouvements oculaires artificiels en tant qu’entrées :** Ne forcez pas les utilisateurs à effectuer des mouvements d’oeil spécifiques (mouvements de regard) pour déclencher des actions dans votre application.

5. **Tenez compte des imprécisions :** Nous distingueons deux types d’imprécisions qui sont perceptibles pour les utilisateurs: décalage et instabilité. Le moyen le plus simple de traiter un décalage consiste à fournir des cibles suffisamment volumineuses pour interagir avec. Il est recommandé d’utiliser un angle visuel supérieur à 2 ° comme référence. Par exemple, votre miniature est d’environ 2 ° dans l’angle visuel lorsque vous étirez votre bras. Il en résulte les conseils d’aide suivants :
    - Ne forcez pas les utilisateurs à sélectionner des cibles minuscules. La recherche a montré que si les cibles sont suffisamment volumineuses et que le système est bien conçu, les utilisateurs décrivent leurs interactions sans effort et magique. Si les cibles deviennent trop petites, les utilisateurs décrivent l’expérience comme étant fatigante et frustrante.
   

## <a name="see-also"></a>Voir aussi
* [Suivre de la tête et valider](gaze-and-commit.md)
* [Tête et œil-pointez avec le regard dans DirectX](gaze-in-directx.md)
* [Œil-point d’interfaut](https://aka.ms/mrtk-eyes)
* [Étalonnage](https://docs.microsoft.com/en-us/windows/mixed-reality/calibration)
* [Mouvements des mains](gestures.md)
* [Entrée vocale](voice-design.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Confort](comfort.md)
