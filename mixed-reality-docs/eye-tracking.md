---
title: Eye-tracking
description: HoloLens 2 permet à un nouveau niveau de contexte et de compréhension humaine au sein de l’expérience holographique en offrant aux développeurs la possibilité d’utiliser des informations sur ce que l’utilisateur examine.
author: sostel
ms.author: sostel
ms.date: 10/29/2019
ms.topic: article
keywords: Suivi oculaire, réalité mixte, entrée, point de regard, étalonnage
ms.openlocfilehash: 63520ee8d7d3ce73405776fccc62290cbbadd0a8
ms.sourcegitcommit: 2e54d0aff91dc31aa0020c865dada3ae57ae0ffc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73641142"
---
# <a name="eye-tracking-on-hololens-2"></a>Eye-tracking sur HoloLens 2

![Démonstration du suivi oculaire dans MRTK](images/mrtk_et_scenemenu.jpg)

HoloLens 2 permet à un nouveau niveau de contexte et de compréhension humaine au sein de l’expérience holographique en offrant aux développeurs la possibilité d’utiliser des informations sur ce que l’utilisateur examine. Cette page fournit une vue d’ensemble de cette nouvelle fonctionnalité destinée aux développeurs et aux concepteurs sur la façon dont ils peuvent tirer parti du suivi oculaire pour divers cas d’usage et des conseils de base pour les développeurs. 

### <a name="device-support"></a>Périphériques pris en charge
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
     <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></td>
     <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
</tr>
<tr>
     <td>Œil-point de regard</td>
     <td>❌</td>
     <td>✔️</td>
     <td>❌</td>
</tr>
</table>

<br>

## <a name="calibration"></a>Auto 
Pour que le suivi des yeux fonctionne correctement, chaque utilisateur doit passer par un [étalonnage d’utilisateur de suivi oculaire](calibration.md) pour lequel l’utilisateur doit examiner un ensemble de cibles holographiques. Cela permet à l’appareil d’ajuster le système pour une expérience d’affichage plus confortable et de meilleure qualité pour l’utilisateur et pour garantir un suivi visuel précis en même temps. 

Le suivi oculaire doit fonctionner pour la plupart des utilisateurs, mais dans de rares cas, un utilisateur peut ne pas être en mesure de l’étalonner correctement. L’étalonnage peut échouer pour diverses raisons, y compris mais sans s’y limiter : 
* L’utilisateur a précédemment choisi le processus d’étalonnage
* L’utilisateur a été distrait et n’a pas suivi les objectifs d’étalonnage
* L’utilisateur dispose de certains types de lentilles de contact et de lunettes que le système ne prend pas encore en charge. 
* L’utilisateur a des conditions oculaires, des conditions oculaires ou une chirurgie oculaire que le système ne prend pas encore en charge  
* Facteurs externes inhibant le suivi des yeux fiables, tels que les taches sur le Visor ou les lunettes, le soleil et les occlusions directs, en raison des cheveux en face des yeux

Les développeurs doivent veiller à fournir une prise en charge adéquate pour les utilisateurs pour lesquels les données de suivi oculaire peuvent ne pas être disponibles (qui ne peuvent pas être correctement étalonnes). Nous avons fourni des recommandations pour les solutions de secours dans la section en bas de cette page. 

Pour en savoir plus sur l’étalonnage et sur la façon de garantir une expérience sans heurts, consultez notre page d’étalonnage de l' [utilisateur de suivi oculaire](calibration.md) .

<br>

## <a name="available-eye-tracking-data"></a>Données de suivi oculaire disponibles
Avant de passer en revue les cas d’utilisation spécifiques pour les entrées de regard oculaire, nous souhaitons rapidement souligner les fonctionnalités fournies par l' [API de suivi oculaire](https://docs.microsoft.com/uwp/api/windows.perception.people.eyespose) HoloLens 2. Les développeurs accèdent à un seul point d’accès en regard (origine du regard et direction) à environ _30 i/s (30 Hz)_ .
Pour plus d’informations sur la façon d’accéder aux données de suivi oculaire, reportez-vous à nos guides pour développeurs sur l’utilisation de la fonction [Eye-pointer](gaze-in-directx.md) dans le regard sur [Unity](https://aka.ms/mrtk-eyes).

Le point de regard prédit est approximativement de 1,5 degrés d’angle visuel autour de la cible réelle (Voir l’illustration ci-dessous). Les développeurs doivent prévoir une marge autour de cette valeur limite inférieure (par exemple, 2,0-3,0 degrés peut se traduire par une expérience bien plus confortable). Nous verrons comment traiter la sélection de petites cibles plus en détail ci-dessous. Pour que l’eye-tracking fonctionne avec précision, chaque utilisateur doit effectuer un étalonnage. 

![Taille optimale de la cible à une distance de 2 mètres](images/gazetargeting-size-1000px.jpg)<br>
*Taille de cible optimale à une distance de 2 mètres*

<br>

## <a name="use-cases"></a>Cas d’utilisation
L’eye-tracking permet aux applications de savoir où l’utilisateur regarde en temps réel. Les cas d’usage suivants décrivent certaines interactions possibles avec le suivi oculaire sur HoloLens 2 en réalité mixte.
Veuillez noter que ces cas d’utilisation ne font pas encore partie de l’expérience d’interpréteur de commandes holographique (c’est-à-dire, l’interface que vous voyez lorsque vous démarrez votre HoloLens 2).
Vous pouvez essayer certaines d’entre elles dans la [boîte à outils de la réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html) , qui fournit plusieurs exemples intéressants et puissants pour l’utilisation du suivi oculaire, tels que les sélections de cibles rapides et faciles à utiliser par l’œil, ainsi que le défilement automatique dans le texte. sur ce que l’utilisateur examine. 

### <a name="user-intent"></a>Intention de l’utilisateur    
Des informations sur l’emplacement et le rôle d’un utilisateur fournissent un **contexte puissant pour d’autres entrées**, telles que la voix, les mains et les contrôleurs.
Cela peut être utile pour diverses tâches.
Par exemple, cette opération peut être effectuée rapidement et facilement **sur la** scène en regardant simplement un hologramme et en disant *« Sélectionner »* (voir également le point d’interrogation et de [validation](gaze-and-commit.md)) ou en disant *« Placer cela... »* , puis en consultant l’emplacement où l’utilisateur veut placer l’hologramme et indiquer *«... là»* . Vous trouverez des exemples à ce sujet dans [Mixed Reality Toolkit - Sélection d’une cible à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_TargetSelection.html) et [Mixed Reality Toolkit - Positionnement d’une cible à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Positioning.html).

En outre, un exemple d’intention de l’utilisateur peut inclure des informations sur ce que les utilisateurs cherchent pour améliorer l’engagement avec des agents virtuels et des hologrammes interactifs. Par exemple, les agents virtuels peuvent adapter les options disponibles et leur comportement en fonction du contenu actuellement affiché. 

### <a name="implicit-actions"></a>Actions implicites
La catégorie des actions implicites est étroitement liée à l’intention de l’utilisateur.
L’idée est que les hologrammes ou les éléments d’interface utilisateur réagissent de manière instinctuale, qui peut ne pas avoir l’impression que l’utilisateur interagit avec le système, mais plutôt que le système et l’utilisateur sont synchronisés. Par exemple, le **défilement automatique orienté vers le regard** de l’utilisateur peut lire un texte long qui commence automatiquement à faire défiler une fois que l’utilisateur accède au bas de la zone de texte pour que l’utilisateur reste dans le sens de la lecture sans soulever de doigt.  
Un aspect clé de cela est que la vitesse de défilement s’adapte à la vitesse de lecture de l’utilisateur.
Un autre exemple est un **Zoom et un panoramique pris en charge par l’œil,** où l’utilisateur peut sembler se plonger exactement sur ce qu’il est concentré. Le déclenchement du zoom et du contrôle de la vitesse de zoom peut être contrôlé par des entrées vocales ou de la main, ce qui est important pour fournir à l’utilisateur le sentiment de contrôle tout en évitant d’être submergé. Nous parlerons de ces considérations de conception plus en détail ci-dessous. Une fois le zoom avant effectué, l’utilisateur peut suivre facilement, par exemple, le cours d’une rue pour explorer son voisinage en utilisant simplement son regard.
Vous trouverez des démonstrations de ces types d’interaction dans l’exemple [Mixed Reality Toolkit - Navigation à l’aide du regard](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Navigation.html).

Il existe d’autres cas d’usage supplémentaires pour les _actions implicites_ :
- **Notifications intelligentes :** Vous vous êtes-vous en désen être informé par des notifications qui se trouvent en haut de la recherche ? En tenant compte de ce à quoi un utilisateur fait attention, vous pouvez améliorer cette expérience en décalant les notifications à partir de l’endroit où l’utilisateur est actuellement Gazing. Cela limite les distractions et les ignore automatiquement une fois que l’utilisateur a terminé la lecture. 
- **Hologrammes précis :** Des hologrammes qui réagissent à la légère sur le regard. Cela peut aller d’un léger éclat aux éléments de l’interface utilisateur, une fleur très lente à un chien virtuel qui commence à regarder l’utilisateur et wagging sa queue. Cette interaction peut fournir un sens intéressant de la connectivité et de la satisfaction dans votre application.

### <a name="attention-tracking"></a>Suivi de l’attention   
Des informations sur l’emplacement ou les utilisateurs qui regardent sont un outil très puissant pour évaluer la convivialité des conceptions et pour identifier les problèmes dans les flux de travail efficaces. La visualisation et l’analyse du suivi oculaire sont une pratique courante dans différents domaines d’application. Avec HoloLens 2, nous fournissons une nouvelle dimension à cette compréhension, car les hologrammes 3D peuvent être placés dans des contextes réels et évalués en conséquence. La [boîte à outils de la réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_Main.html) fournit des exemples de base pour la journalisation et le chargement des données de suivi visuel et comment les visualiser.

Autres applications possibles dans ce domaine : 
-   **Œil à distance-visualisation du regard :** Visualisez ce que les collaborateurs distants examinent pour améliorer la compréhension partagée.
-   **Études de recherche des utilisateurs :** Le suivi de l’attention peut vous aider à mieux comprendre la façon dont nous percevons et faisons appel à notre environnement, qui peut aider à améliorer les modèles d’intention de l’homme pour plus d’instinctual. 
-   **Formation :** Amélioration de la formation des novices grâce à une meilleure compréhension des modèles de recherche visuelle des experts et de leur coordination manuelle pour les tâches complexes, telles que l’analyse des données médicales ou les machines à fonctionner.
-   **Évaluations de la conception et recherche sur le marché :** Le suivi oculaire est un outil courant pour les recherches sur le marché lors de l’évaluation des conceptions de site Web et de produit. Avec HoloLens 2, nous pouvons l’étendre aux espaces 3D en fusionnant les variantes de conception de produits numériques avec l’environnement physique. 

### <a name="additional-use-cases"></a>Cas d’usage supplémentaires
- **Jeux :** Avez-vous déjà souhaité des superalimentations ? Voilà votre chance ! Vous pouvez faire en lévitation les hologrammes. Prenez des faisceaux laser de vos yeux, essayez-le dans [RoboRaid pour HoloLens 2](https://www.microsoft.com/p/roboraid/9nblggh5fv3j).
Transformez des ennemis en pierres ou figez-les. Utilisez votre vision à rayons X pour explorer des bâtiments. La seule limite, c’est votre imagination !
ATTENTION : pour en savoir plus, consultez nos [instructions relatives à la conception d’entrées](eye-gaze-interaction.md)orientées regard.

- **Avatars expressifs :** Le suivi des yeux permet d’obtenir des avatars 3D plus expressifs en utilisant des données de suivi visuel actif pour animer les yeux de l’avatar qui indiquent ce que l’utilisateur examine. 

- **Entrée de texte :** Le suivi oculaire peut être utilisé comme alternative pour une entrée de texte à faible effort, en particulier lorsque la parole ou les mains sont peu pratiques à utiliser. 

<br>

## <a name="using-eye-gaze-for-interaction"></a>Utilisation de l’œil en regard de l’interaction
La création d’une interaction qui tire parti du ciblage visuel à déplacement rapide peut être difficile.
D’un côté, les yeux se déplacent tellement vite que vous devez être attentif à l’utilisation des entrées de regard, car sinon les utilisateurs peuvent se rendre compte de l’expérience insurmontable ou gênante. En revanche, vous pouvez également créer des expériences véritablement magiques qui exciteront vos utilisateurs ! Pour vous aider, consultez notre présentation des principaux avantages, défis et recommandations de conception pour [une interaction](eye-gaze-interaction.md)avec les yeux. 

<br>
 
## <a name="fallback-solutions-when-eye-tracking-is-not-available"></a>Solutions de secours lorsque le suivi oculaire n’est pas disponible
Dans de rares cas, les données de suivi oculaire peuvent ne pas être disponibles.
Cela peut être dû à différentes raisons, parmi lesquelles les plus courantes sont répertoriées ci-dessous :
* Le système n’a pas pu [étalonner l’utilisateur](calibration.md).
* L’utilisateur a ignoré l' [étalonnage](calibration.md).   
* L’utilisateur est étalonné, mais il a décidé de ne pas accorder à votre application l’autorisation d’utiliser ses données de suivi visuel.    
* L’utilisateur dispose de lunettes uniques ou d’une condition oculaire que le système ne prend pas encore en charge.    
* Facteurs externes qui empêchent le suivi des yeux fiables, tels que les taches sur le Visor ou les lunettes, les lumières et les occlusions directs du soleil en raison des cheveux devant les yeux.   
Par conséquent, les développeurs doivent s’assurer qu’il existe une prise en charge de secours appropriée pour ces utilisateurs. Sur la page [suivi des yeux dans DirectX](gaze-in-directx.md#fallback-when-eye-tracking-is-not-available) , nous expliquons les API requises pour détecter si les données de suivi visuel sont disponibles. 

Comme décrit ci-dessus, il existe plusieurs raisons pour lesquelles les données de suivi oculaire peuvent ne pas être disponibles.   
Alors que certains utilisateurs peuvent avoir des axent décidés de révoquer l’accès à leurs données de suivi visuel et qu’ils sont OK avec le compromis d’une expérience utilisateur inférieure à la confidentialité de ne pas fournir l’accès à leurs données de suivi visuel, dans certains cas cela peut être involontaire.  
Par conséquent, si votre application utilise le suivi oculaire et qu’il s’agit d’une partie importante de l’expérience, nous vous recommandons de le communiquer clairement à l’utilisateur.     
En informant l’utilisateur, pourquoi le suivi des yeux est essentiel pour votre application (peut-être même répertorier certaines fonctionnalités améliorées) afin de tirer le meilleur parti de votre application, peut aider l’utilisateur à mieux comprendre ce qu’il abandonne.    
Aidez l’utilisateur à identifier la raison pour laquelle le suivi oculaire peut ne pas fonctionner (sur la base des vérifications ci-dessus) et propose des suggestions pour résoudre rapidement les problèmes potentiels.  
Par exemple, si vous pouvez détecter que le système prend en charge le suivi oculaire, l’utilisateur est étalonné et même a donné son autorisation, mais aucune donnée de suivi oculaire n’est reçue, alors cela peut pointer vers d’autres problèmes tels que les traînées ou les yeux bloqués.    
Notez cependant qu’il y a de rares cas d’utilisateurs pour lesquels le suivi oculaire peut simplement ne pas fonctionner.    
Par conséquent, n’hésitez pas à le faire en autorisant à ignorer ou même à désactiver les rappels pour activer le suivi visuel dans votre application.

### <a name="fallback-for-apps-using-eye-gaze-as-a-primary-input-pointer"></a>Secours pour les applications utilisant des yeux en forme de point d’entrée principal
Si votre application utilise le point d’entrée de l’œil pour sélectionner rapidement des hologrammes dans la scène, mais que les données de suivi oculaire ne sont pas disponibles, nous vous recommandons de revenir à la tête de regard et de commencer à montrer le curseur en tête. Nous vous recommandons d’utiliser un délai d’expiration (par exemple, 500 – 1500 ms) pour déterminer s’il faut basculer ou non. Cela permet d’éviter de faire apparaître un curseur à chaque fois que le système risque de perdre brièvement le suivi en raison de mouvements oculaires rapides ou de clignotements. Si vous êtes un développeur Unity, la solution de secours automatique à la tête de regard est déjà gérée dans le kit de développement de la réalité mixte. Si vous êtes un développeur DirectX, vous devez gérer ce commutateur vous-même.

### <a name="fallback-for-other-eye-tracking-specific-applications"></a>Secours pour d’autres applications spécifiques au suivi des yeux
Votre application peut utiliser des regards à l’aide d’une méthode unique adaptée aux yeux, par exemple pour animer les yeux d’un avatar ou pour attirer l’attention sur les yeux cartes thermiques en se basant sur des informations précises sur l’attention visuelle. Dans ce cas, il n’y a pas de secours clair. Si le suivi oculaire n’est pas disponible, il se peut que vous deviez simplement désactiver ces fonctionnalités.
Là encore, nous vous recommandons de communiquer clairement à l’utilisateur qui ne sait pas que la fonctionnalité ne fonctionne pas.

<br>

Cette page vous a espérons vous fournir une bonne vue d’ensemble pour vous aider à comprendre le rôle du suivi oculaire et l’entrée de regard pour HoloLens 2. Pour commencer à développer, consultez nos informations sur le rôle de l' [oeil pour l’interaction avec les hologrammes](eye-gaze-interaction.md), le [point de regard sur Unity](https://aka.ms/mrtk-eyes) et les [yeux dans DirectX](gaze-in-directx.md).


## <a name="see-also"></a>Articles associés
* [Étalonnage](calibration.md)
* [Confort](comfort.md)
* [Interaction avec l’œil-regard](eye-gaze-interaction.md)
* [Œil-point de regard sur DirectX](gaze-in-directx.md)
* [Œil-point d’interfaut](https://aka.ms/mrtk-eyes)
* [Point de regard et validation](gaze-and-commit.md)
* [Entrée vocale](voice-design.md)


