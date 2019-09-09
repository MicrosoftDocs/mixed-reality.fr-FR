---
title: Œil-point de regard
description: HoloLens 2 permet d’accéder à un nouveau niveau de compréhension contextuelle et humaine au sein de l’expérience holographique en offrant aux développeurs la capacité d’utiliser des informations sur ce que les utilisateurs regardent.
author: sostel
ms.author: sostel
ms.date: 04/05/2019
ms.topic: article
keywords: Suivi oculaire, réalité mixte, entrée, point de regard
ms.openlocfilehash: 51779b7b210522aa4d19b5a32d7df6ccb2cb3a35
ms.sourcegitcommit: ff330a7e36e5ff7ae0e9a08c0e99eb7f3f81361f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70122064"
---
# <a name="eye-gaze-on-hololens-2"></a>Eye-point de regard sur HoloLens 2
HoloLens 2 permet d’accéder à un nouveau niveau de compréhension contextuelle et humaine au sein de l’expérience holographique en offrant aux développeurs la capacité d’utiliser des informations sur ce que les utilisateurs regardent. Cette page explique aux développeurs comment ils peuvent tirer parti du suivi oculaire pour divers cas d’usage, ainsi que des éléments à rechercher lors de la conception d’interfaces utilisateur orientées yeux. 


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
Par exemple, cette opération peut être effectuée rapidement et facilement **sur la** scène en regardant simplement un hologramme et en disant « sélectionner » (voir également le point d’interrogation [et de validation](gaze-and-commit.md)) ou en disant *« Placer cela... »* , puis en consultant l’emplacement où l’utilisateur veut placer l’hologramme et indiquer *«... là»* . Vous trouverez des exemples à ce sujet dans [Mixed Reality Toolkit - Sélection d’une cible à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html) et [Mixed Reality Toolkit - Positionnement d’une cible à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Positioning.html).

En outre, un exemple d’intention de l’utilisateur peut inclure des informations sur ce que les utilisateurs cherchent pour améliorer l’engagement avec des agents virtuels et des hologrammes interactifs. Par exemple, les agents virtuels peuvent adapter les options disponibles et leur comportement en fonction du contenu actuellement affiché. 

### <a name="implicit-actions"></a>Actions implicites
La catégorie des actions implicites est étroitement liée à l’intention de l’utilisateur.
L’idée est que les hologrammes ou les éléments d’interface utilisateur réagissent de façon quelque peu instinctual, qui peut même ne pas se comporter comme l’utilisateur qui interagit avec le système, mais plutôt que le système et l’utilisateur sont synchronisés. Par exemple, le **défilement automatique orienté vers le regard** de l’utilisateur peut lire un texte long qui commence automatiquement à faire défiler une fois que l’utilisateur accède au bas de la zone de texte pour que l’utilisateur reste dans le sens de la lecture sans soulever de doigt.  
Un aspect clé de cela est que la vitesse de défilement s’adapte à la vitesse de lecture de l’utilisateur.
Un autre exemple est un **Zoom et un panoramique pris en charge par l’œil,** où l’utilisateur peut sembler se plonger exactement sur ce qu’il est concentré. Le déclenchement du zoom et du contrôle de la vitesse de zoom peut être contrôlé par des entrées vocales ou de la main, ce qui est important pour fournir à l’utilisateur le sentiment de contrôle tout en évitant d’être submergé. Nous parlerons des instructions de conception plus en détail ci-dessous. Une fois le zoom avant effectué, l’utilisateur peut suivre facilement, par exemple, le cours d’une rue pour explorer son voisinage en utilisant simplement son regard.
Vous trouverez des démonstrations de ces types d’interaction dans l’exemple [Mixed Reality Toolkit - Navigation à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html).

Des cas d’usage supplémentaires pour les _actions implicites_ peuvent inclure :
- **Notifications intelligentes :** Avez-vous déjà été ennuyé par des notifications qui apparaissent juste là où vous concentrez votre attention ? En tenant compte de ce à quoi un utilisateur fait attention, vous pouvez améliorer cette expérience en décalant les notifications à partir de l’endroit où l’utilisateur est actuellement Gazing. Cela limite les distractions et les ignore automatiquement une fois que l’utilisateur a terminé la lecture. 
- **Hologrammes attentifs :** Des hologrammes qui réagissent à la légère sur le regard. Cela peut aller de quelques éléments d’interface utilisateur à une fleur très lente à un animal de compagnie virtuel, commençant à regarder l’utilisateur ou à essayer d’éviter l’oeil de l’utilisateur après une étoile prolongée. Cette interaction peut fournir un sens intéressant de la connectivité et de la satisfaction dans votre application.

### <a name="attention-tracking"></a>Suivi de l’attention   
Des informations sur l’emplacement ou les utilisateurs qui regardent sont un outil très puissant pour évaluer la convivialité des conceptions et pour identifier les problèmes dans les flux de travail efficaces. La visualisation et l’analyse du suivi oculaire sont une pratique courante dans différents domaines d’application. Avec HoloLens 2, nous fournissons une nouvelle dimension à cette compréhension, car les hologrammes 3D peuvent être placés dans des contextes réels et évalués en conséquence. La [boîte à outils de la réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html) fournit des exemples de base pour la journalisation et le chargement des données de suivi visuel et comment les visualiser.

Les autres applications de cette zone peuvent inclure : 
-   **Œil à distance-visualisation du regard :** Visualisez ce que les collaborateurs distants examinent pour vérifier si les instructions sont correctement comprises et suivies.
-   **Études de recherche sur les utilisateurs :** Le suivi de l’attention peut être utilisé pour explorer la manière dont les utilisateurs débutants ou expérimentés analysent le contenu visuellement, ou comment leur coordination manuelle pour les tâches complexes, telles que l’analyse des données médicales ou les machines à fonctionner.
-   **Simulations d’apprentissage et analyse des performances :** Entraînez-vous et optimisez l’exécution de certaines tâches en identifiant plus efficacement les goulots d’étranglement du flux d’exécution.
-   **Évaluations de conception, études publicitaires et marketing :** Le suivi oculaire est un outil courant pour les recherches sur le marché lors de l’évaluation des conceptions de site Web et de produit.

### <a name="additional-use-cases"></a>Cas d’usage supplémentaires
- **Jeux :** Vous avez toujours souhaité avoir des super pouvoirs ? Voilà votre chance ! Vous pouvez faire en lévitation les hologrammes. Envoyez des rayons laser avec vos yeux. Transformez des ennemis en pierres ou figez-les. Utilisez votre vision à rayons X pour explorer des bâtiments. La seule limite, c’est votre imagination !  

- **Avatars expressifs :** Le suivi des yeux permet d’obtenir des avatars 3D plus expressifs en utilisant des données de suivi visuel actif pour animer les yeux de l’avatar qui indiquent ce que l’utilisateur examine. 

- **Entrée de texte :** Le suivi oculaire peut être utilisé comme alternative pour une entrée de texte à faible effort, en particulier lorsque la parole ou les mains sont peu pratiques à utiliser. 


## <a name="available-eye-tracking-data"></a>Données de suivi oculaire disponibles
Avant de décrire en détail les règles de conception spécifiques pour l’interaction avec le regard des yeux, nous souhaitons rapidement souligner les fonctionnalités fournies par l' [API de suivi oculaire](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose) HoloLens 2. Les développeurs accèdent à un seul point d’accès en regard (origine du regard et direction) à environ _30 i/s (60 Hz)_ .
Pour plus d’informations sur la façon d’accéder aux données de suivi oculaire, reportez-vous à nos guides pour développeurs sur l’utilisation de la fonction [Eye-pointer](gaze-in-directx.md) dans le regard sur [Unity](https://aka.ms/mrtk-eyes).

Le point de regard prédit est approximativement de 1,5 degrés d’angle visuel autour de la cible réelle (Voir l’illustration ci-dessous). Les développeurs doivent prévoir une marge autour de cette valeur limite inférieure (par exemple, 2,0-3,0 degrés peut se traduire par une expérience bien plus confortable). Nous verrons comment traiter la sélection de petites cibles plus en détail ci-dessous. Pour que l’eye-tracking fonctionne avec précision, chaque utilisateur doit effectuer un étalonnage. 

![Taille optimale de la cible à une distance de 2 mètres](images/gazetargeting-size-1000px.jpg)<br>
*Taille de cible optimale à une distance de 2 mètres*

## <a name="calibration"></a>Auto 
Pour que le suivi des yeux fonctionne correctement, chaque utilisateur doit passer par un [étalonnage d’utilisateur de suivi oculaire](calibration.md) pour lequel l’utilisateur doit examiner un ensemble de cibles holographiques. Cela permet à l’appareil d’ajuster le système pour une expérience d’affichage plus confortable et de meilleure qualité pour l’utilisateur et pour garantir un suivi visuel précis en même temps. Le suivi oculaire doit fonctionner pour la plupart des utilisateurs, mais dans certains cas, il se peut qu’un utilisateur ne puisse pas l’étalonner correctement.
Pour en savoir plus sur l’étalonnage, vérifiez l' [étalonnage](calibration.md).

## <a name="eye-gaze-input-design-guidelines"></a>Conseils pour la conception d’entrées de regard
La création d’une interaction qui tire parti du ciblage visuel à déplacement rapide peut être difficile. Dans cette section, nous résumerons les principaux avantages et défis à prendre en compte lors de la conception de votre application. 

### <a name="benefits-of-eye-gaze-input"></a>Avantages de l’entrée en regard des yeux
- **Pointage à haute vitesse.** Le muscle oculaire est le muscle le plus rapide dans le corps humain. 

- **Faible effort.** Pratiquement aucun mouvement physique n’est nécessaire. 

- **Implicite.** Souvent décrits par les utilisateurs comme « sens de lecture », les informations relatives aux mouvements oculaires d’un utilisateur permettent au système de savoir à quelle cible l’utilisateur envisage de s’impliquer. 

- **Autre canal d’entrée.** L’œil-point de vue peut fournir une entrée de prise en charge puissante pour les entrées de main et vocales, basées sur des années d’expérience des utilisateurs en fonction de leur coordination manuelle.

- **Attention visuelle.** Un autre avantage important est la possibilité de déduire ce à quoi un utilisateur fait attention. Cela peut aider dans différents domaines d’application, allant de l’évaluation plus efficace de conceptions différentes à l’aide d’interfaces utilisateur plus intelligentes et de signaux sociaux améliorés pour la communication à distance.

Pour résumer, l’utilisation de l’œil en forme de point d’entrée offre un signal contextuel rapide et sans effort. Cela est particulièrement puissant lorsqu’il est combiné à d’autres entrées, telles que la *voix* et l’entrée *manuelle* , pour confirmer l’intention de l’utilisateur.


### <a name="challenges-of-eye-gaze-as-an-input"></a>Défis de l’entrée
Avec un grand nombre d’énergie, la responsabilité est importante.
Bien qu’il soit possible d’utiliser des yeux pour créer des expériences utilisateur satisfaisantes, il est également important de savoir ce qu’il n’est pas judicieux de prendre en compte. Ce qui suit présente certains *défis* à prendre en compte, ainsi que la façon de les résoudre quand vous travaillez avec des entrées de regard : 

- **Votre regard est « Always on »** Le moment où vous ouvrez vos couvercles oculaires, vos yeux commencent que sur les choses de l’environnement. En réagissant à chaque fois que vous effectuez des actions et que vous émettez accidentellement des actions, parce que vous avez examiné un peu trop de temps, cela entraînerait une insatisfaction de l’expérience.
Par conséquent, nous vous recommandons de combiner Eye-regard avec une *commande vocale*, un *mouvement manuel*, un *clic de bouton* ou un logement étendu pour déclencher la sélection d’une cible.
Cette solution permet également à un mode dans lequel l’utilisateur peut effectuer des recherches librement sans être submergé par le déclenchement involontaire d’un événement. Ce problème doit également être pris en compte lors de la conception de commentaires visuels et auditifs quand vous examinez simplement une cible.
Ne surchargez pas l’utilisateur avec des effets immédiats d’ouverture dans une nouvelle fenêtre ou des sons de pointage. La subtilité est essentielle. Nous allons aborder plus loin certaines bonnes pratiques quand nous évoquerons les recommandations de conception.

- **Observation et contrôle** Imaginez que vous souhaitez redresser précisément une photographie sur votre mur. Vous regardez les bords de la photo et ce qui se trouve à proximité pour voir si elle est bien alignée. Imaginez maintenant comment procéder lorsque vous souhaitez utiliser le point de vue de l’œil pour déplacer l’image. Difficile, n’est-ce pas ? Cela décrit le double rôle de regard pour les entrées et les contrôles. 

- **Quitter avant de cliquer :** Pour les sélections de cibles rapides, l’étude a montré que le point de vue de l’utilisateur peut se déplacer avant de conclure un clic manuel (par exemple, un airtap). Par conséquent, une attention particulière doit être accordée à la synchronisation du signal rapide oeil-regard avec une entrée de contrôle plus lente (par exemple, voix, mains, contrôleur).

- **Petites cibles :** Savez-vous le sentiment quand vous essayez de lire du texte qui est un peu trop petit pour le lire confortablement ? Ce sentiment de stress sur vos yeux peut vous amener à vous sentir fatigué et à s’en ressentir, car vous essayez de réajuster vos yeux pour mieux vous concentrer.
C’est un sentiment que vous pouvez appeler dans vos utilisateurs en les forçant à sélectionner des cibles qui sont trop petites dans votre application à l’aide d’un ciblage oculaire.
Durant la conception, si vous souhaitez créer une expérience utilisateur agréable et confortable, nous vous recommandons de privilégier des cibles ayant un angle de vue d’au moins 2°, sinon plus de préférence.

- **Mouvements de regard en œil irrégulier** Nos yeux effectuent des mouvements rapides de la fixation à la fixation. Si vous examinez un enregistrement des mouvements oculaires, vous pouvez voir qu’ils sont irréguliers. Vos yeux se déplacent rapidement et dans des passages spontanés par rapport aux mouvements du point de vue de la *main*ou du *regard* .  

- **Fiabilité du suivi :** La précision de l’eye-tracking peut se dégrader légèrement quand la lumière change, car votre œil s’adapte aux nouvelles conditions.
Même si cela ne doit pas nécessairement affecter la conception de votre application, car la précision doit être comprise dans la limite de 2 °, il peut être nécessaire que l’utilisateur l’étalonne à nouveau. 


## <a name="design-recommendations"></a>Recommandations de conception
La liste suivante répertorie les recommandations de conception spécifiques en fonction des avantages et des défis décrits pour les entrées de regard :

1. **L’œil-point de regard n’est pas le même que le point de regard :**
    - **Déterminez si des mouvements oculaires rapides mais irréguliers conviennent à votre tâche de saisie :** Si nos mouvements oculaires rapides et irréguliers sont très utiles pour sélectionner rapidement des cibles dans notre champ de vue, elles sont moins applicables aux tâches qui nécessitent des trajectoires d’entrée lisses (par exemple, des annotations de dessin ou de cercle). Dans ce cas, le pointage à la main ou avec la tête est préférable.
  
    - **Évitez de joindre un texte directement à l’oeil de l’utilisateur (par exemple, un curseur ou un curseur).**
Dans le cas d’un curseur, cela peut entraîner l’effet de « curseur Fleeing » en raison de légers décalages dans le signal de point de regard projeté. Dans le cas d’un curseur, il peut entrer en conflit avec le double rôle de contrôle du curseur avec vos yeux, tout en souhaitant vérifier si l’objet se trouve à l’emplacement approprié. Pour résumer, les utilisateurs peuvent devenir submergés et perturbés, en particulier si le signal n’est pas précis pour cet utilisateur. 
  
2. **Combinez les yeux avec d’autres entrées :** L’intégration du suivi oculaire avec d’autres entrées, telles que les gestes manuels, les commandes vocales ou les enfoncements de bouton, offre plusieurs avantages :
    - **Permettre une observation libre :** Étant donné que le rôle principal de nos yeux est d’observer notre environnement, il est important que les utilisateurs soient autorisés à regarder sans déclencher les commentaires ou les actions (visuel, audit, etc.). 
    La combinaison du suivi oculaire et d’un autre contrôle d’entrée permet une transition sans heurts entre l’observation du suivi oculaire et les modes de contrôle d’entrée.
  
    - **Fournisseur de contexte puissant :** L’utilisation d’informations sur l’emplacement et le rôle de l’utilisateur lors de la mise en circulation d’une commande vocale ou de l’exécution d’un mouvement manuel permet de canaliser en toute transparence l’entrée dans le champ de la vue. Exemple : « Mettre ça là » pour sélectionner et positionner rapidement et facilement un hologramme dans la scène en regardant simplement une cible et une destination. 

    - **Nécessité de synchroniser les entrées multimodales (problème du « quitter avant de cliquer ») :** La combinaison rapide de mouvements oculaires avec des entrées supplémentaires plus complexes, telles que des commandes vocales longues ou des gestes de main, risque de poursuivre votre attention avant de terminer la commande d’entrée supplémentaire. Par conséquent, si vous créez vos propres contrôles d’entrée (par exemple, des gestes personnalisés), veillez à consigner le début de cette entrée ou la durée approximative pour la corréler avec ce qu’un utilisateur a regardé dans le passé.
    
3. **Rétroaction subtile pour une entrée par eye-tracking :** Il est utile de fournir des commentaires lorsqu’une cible est examinée pour indiquer que le système fonctionne comme prévu, mais qu’il doit rester discret. Cela peut inclure la fusion lente, l’inversion et l’extraction, les surbrillances visuelles ou l’exécution d’autres comportements de cible subtils, tels que des mouvements lents, tels que l’amélioration de la taille cible, pour indiquer que le système a détecté correctement que l’utilisateur regarde une cible sans interruption inutile du flux de travail actuel de l’utilisateur. 

4. **Évitez d’appliquer des mouvements oculaires artificiels en tant qu’entrées :** Ne forcez pas les utilisateurs à effectuer des mouvements d’oeil spécifiques (mouvements de regard) pour déclencher des actions dans votre application.

5. **Tenez compte des imprécisions :** Nous distingueons deux types d’imprécisions qui sont perceptibles pour les utilisateurs : décalage et instabilité. Le moyen le plus simple de traiter un décalage consiste à fournir des cibles suffisamment volumineuses pour interagir avec. Il est recommandé d’utiliser un angle visuel supérieur à 2 ° comme référence. Par exemple, votre miniature est d’environ 2 ° dans l’angle visuel lorsque vous étirez votre bras. Il en résulte les conseils d’aide suivants :
    - Ne forcez pas les utilisateurs à sélectionner des cibles minuscules. La recherche a montré que si les cibles sont suffisamment volumineuses et que le système est bien conçu, les utilisateurs décrivent leurs interactions sans effort et magique. Si les cibles deviennent trop petites, les utilisateurs décrivent l’expérience comme étant fatigante et frustrante.
  
## <a name="dev-guidance-what-if-eye-tracking-is-not-available"></a>Guide de développement : Que se passe-t-il si le suivi oculaire n’est pas disponible ?
Dans certaines situations, votre application ne recevra peut-être aucune donnée de suivi oculaire pour différentes raisons, notamment :
* L’utilisateur a ignoré l’étalonnage du suivi oculaire.
* L’utilisateur a étalonné, mais a décidé de ne pas accorder à votre application l’autorisation d’utiliser ses données de suivi visuel.
* L’utilisateur dispose de lunettes uniques ou d’une condition oculaire que le système ne prend pas encore en charge.
* Facteurs externes qui empêchent le suivi des yeux fiables, tels que les taches sur le Visor ou les lunettes, les lumières et les occlusions directs du soleil en raison des cheveux devant les yeux.

Pour vous, en tant que développeur d’applications, cela signifie que vous devez prendre en compte la prise en charge des utilisateurs pour lesquels les données de suivi oculaire peuvent ne pas être disponibles. Nous vous expliquons tout d’abord comment détecter si le suivi oculaire est disponible et comment résoudre le cas où il n’est pas disponible pour différentes applications.

### <a name="1-how-to-detect-that-eye-tracking-is-available"></a>1. Comment détecter que le suivi oculaire est disponible
Quelques vérifications permettent de déterminer si les données de suivi visuel sont disponibles. Vérifier si...
* ... le système prend en charge le suivi visuel. Appelez la *méthode*suivante : [Windows. perception. People. EyesPose. IsSupported ()](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.issupported#Windows_Perception_People_EyesPose_IsSupported)

* ... l’utilisateur est étalonné. Appelez la *propriété*suivante : [Windows. perception. People. EyesPose. IsCalibrationValid](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid)

* ... l’utilisateur a donné à votre application l’autorisation d’utiliser ses données de suivi visuel : Récupère le _« GazeInputAccessStatus »_ actuel. Vous trouverez un exemple de la procédure à suivre pour [demander l’accès aux entrées de regard](https://docs.microsoft.com/en-us/windows/mixed-reality/gaze-in-directX#requesting-access-to-gaze-input).

En outre, vous souhaiterez peut-être vérifier que vos données de suivi oculaire ne sont pas obsolètes en ajoutant un délai d’expiration entre les mises à jour reçues des données de suivi oculaire et en configurant le point de vue dans le point de vue ci-dessous. 

Comme décrit ci-dessus, il existe plusieurs raisons pour lesquelles les données de suivi oculaire peuvent ne pas être disponibles. Alors que certains utilisateurs peuvent avoir des axent décidés de révoquer l’accès à leurs données de suivi visuel et qu’ils sont OK avec le compromis d’une expérience utilisateur inférieure à la confidentialité de ne pas fournir l’accès à leurs données de suivi visuel, dans certains cas cela peut être involontaire. Par conséquent, si votre application utilise le suivi oculaire et qu’il s’agit d’une partie importante de l’expérience, nous vous recommandons de le communiquer clairement à l’utilisateur. En informant l’utilisateur, pourquoi le suivi des yeux est essentiel pour votre application (peut-être même répertorier certaines fonctionnalités améliorées) afin de tirer le meilleur parti de votre application, peut aider l’utilisateur à mieux comprendre ce qu’il abandonne. Aidez l’utilisateur à identifier la raison pour laquelle le suivi oculaire peut ne pas fonctionner (sur la base des vérifications ci-dessus) et propose des suggestions pour résoudre rapidement les problèmes potentiels. Par exemple, si vous pouvez détecter que le système prend en charge le suivi oculaire, l’utilisateur est étalonné et même a donné son autorisation, mais aucune donnée de suivi oculaire n’est reçue, alors cela peut pointer vers d’autres problèmes tels que les traînées ou les yeux bloqués. Notez cependant qu’il y a de rares cas d’utilisateurs pour lesquels le suivi oculaire peut simplement ne pas fonctionner. Par conséquent, n’hésitez pas à le faire en autorisant à ignorer ou même à désactiver les rappels pour activer le suivi visuel dans votre application.

### <a name="2-fallback-for-apps-using-eye-gaze-as-a-primary-input-pointer"></a>2. Secours pour les applications utilisant des yeux en forme de point d’entrée principal
Si votre application utilise le point d’entrée de l’œil pour sélectionner rapidement des hologrammes dans la scène, mais que les données de suivi oculaire ne sont pas disponibles, nous vous recommandons de revenir à la tête de regard et de commencer à montrer le curseur en tête. Nous vous recommandons d’utiliser un délai d’expiration (par exemple, 500 – 1500 ms) pour déterminer s’il faut basculer ou non. Cela permet d’éviter de faire apparaître un curseur à chaque fois que le système risque de perdre brièvement le suivi en raison de mouvements oculaires rapides ou de clignotements. Si vous êtes un développeur Unity, la solution de secours automatique à la tête de regard est déjà gérée dans le kit de développement de la réalité mixte. Si vous êtes un développeur DirectX, vous devez gérer ce commutateur vous-même.

### <a name="3-fallback-for-other-eye-tracking-specific-applications"></a>3. Secours pour d’autres applications spécifiques au suivi des yeux
Votre application peut utiliser des regards à l’aide d’une méthode unique adaptée aux yeux, par exemple pour animer les yeux d’un avatar ou pour attirer l’attention sur les yeux cartes thermiques en se basant sur des informations précises sur l’attention visuelle. Dans ce cas, il n’y a pas de secours clair. Si le suivi oculaire n’est pas disponible, il se peut que vous deviez simplement désactiver ces fonctionnalités. 

<br>

Cette page vous a espérons vous fournir une bonne vue d’ensemble pour vous aider à comprendre le rôle du suivi oculaire et l’entrée de regard pour HoloLens 2. Pour commencer à développer, consultez les informations sur les [yeux](https://aka.ms/mrtk-eyes) et les [yeux dans DirectX](gaze-in-directx.md).


## <a name="see-also"></a>Voir aussi
* [Œil-point de regard sur DirectX](gaze-in-directx.md)
* [Œil-point d’interfaut](https://aka.ms/mrtk-eyes)
* [Étalonnage](calibration.md)
* [Suivre de la tête et valider](gaze-and-commit.md)
* [Mouvements de la main](gestures.md)
* [Entrée vocale](voice-design.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Confort](comfort.md)
