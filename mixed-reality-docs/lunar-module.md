---
title: Module lunaire
description: LunarModule est un exemple d’application open source des laboratoires de conception de la réalité mixte de Microsoft. Avec ce projet, vous pouvez apprendre à étendre les gestes de base HoloLens avec le suivi à deux mains et l’entrée du contrôleur Xbox, créer des objets qui sont réactifs dans le mappage de surface et la recherche de plan, et implémenter des systèmes de menus simples.
author: radicalad
ms.author: adlinv
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, exemples d’applications, conception, HoloLens
ms.openlocfilehash: 1df2b7e9aaf92a7045aa3c378d3029cf09e085a6
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438537"
---
# <a name="lunar-module"></a>Module lunaire

>[!NOTE]
>Cet article présente un exemple exploratoire que nous avons créé dans les [laboratoires de conception de réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity), un endroit où nous partageons nos connaissances et des suggestions concernant le développement d’applications de réalité mixte. Nos articles et code liés à la conception évoluent à mesure que nous effectuons de nouvelles découvertes.

Le [module lunaire](https://github.com/Microsoft/MRDesignLabs_Unity_LunarModule) est un exemple d’application open source des laboratoires de conception de la réalité mixte de Microsoft. Avec ce projet, vous pouvez apprendre à étendre les gestes de base HoloLens avec le suivi à deux mains et l’entrée du contrôleur Xbox, créer des objets qui sont réactifs dans le mappage de surface et la recherche de plan, et implémenter des systèmes de menus simples. Tous les composants du projet peuvent être utilisés dans vos expériences d’application de réalité mixte.

## <a name="rethinking-classic-experiences-for-windows-mixed-reality"></a>Repenser les expériences classiques pour Windows Mixed Reality

Dans l’atmosphère, une petite rappelle d’expédition du module Apollo examine méthodiquement le terrain en escalier ci-dessous. Notre pilote Fearless répond à une zone de débarquement appropriée. La descente est ardue mais heureusement, ce voyage a été effectué plusieurs fois avant...

![interface d’origine à partir du Lander lunaire 1979 de Atari](images/640px-atari-lunar-lander.png)<br>
*Interface d’origine à partir du Lander lunaire 1979 de Atari*

Le [Lander lunaire](https://en.wikipedia.org/wiki/Lunar_Lander_(1979_video_game)) est un arcade classique où les joueurs essaient de piloter un Lander de lune sur un spot plat de terrain lunaire. Toute personne nés dans les années 1970 a probablement passé des heures dans une arcade avec des yeux collés à ce vecteur plummeting à partir du ciel. Lorsqu’un joueur parcourt son livre vers une zone de destination souhaitée, le terrain se met à l’échelle pour révéler plus de détails. La réussite signifie un lancement dans le seuil de sécurité horizontal et vertical. Les points sont attribués pour le temps passé au palier et au carburant restant, avec un multiplicateur basé sur la taille de la zone de destination.

Outre le jeu, l’ère des arcades des jeux a apporté une innovation constante des schémas de contrôle. Des configurations de manette de jeu à 4 voies et de boutons les plus simples (affichées dans l’sous forme de l' [homme-](https://en.wikipedia.org/wiki/Pac-Man)vert) aux schémas très spécifiques et compliqués observés à la fin des années 90 et des 00S (comme ceux des simulateurs de golf et des pousseurs de rail). Le schéma d’entrée utilisé dans l’ordinateur Lander lunaire est particulièrement fascinant pour deux raisons : l’attrait et l’immersion.

![console d’arcade du Lander lunaire de Atari](images/atariconsole.png)<br>
*Console Atari Lander d’arcade lunaire*

Pourquoi Atari et tellement d’autres sociétés de jeux décident-elles de repenser les entrées ?

Un enfant qui se passe au travers d’une arcade sera naturellement intrigué par le dernier ordinateur flashiest. Mais la Lander lunaire présente un nouveau mécanicien en entrée qui s’est retiré de la foule.

Le Lander lunaire utilise deux boutons pour faire pivoter l’expédition vers la gauche et vers la droite, et un **levier de Poussée** pour contrôler la quantité de poussée produite par le navire. Ce levier offre aux utilisateurs un certain niveau de finesse qu’une manette de jeu normale ne peut pas fournir. Il s’agit également d’un composant commun aux cockpits aéronautiques modernes. Atari souhaitait que les Lander lunaires plongent dans le sentiment qu’ils étaient en cours de pilotage d’un module lunaire. Ce concept est appelé **immersion tactile**.

L’immersion tactile est l’expérience des commentaires sensorielles suite à l’exécution d’actions répétitives. Dans ce cas, l’action répétitive consistant à ajuster le levier de limitation et la rotation que nos yeux voient et nos oreilles entendre, permet de connecter le joueur à l’action de débarquement d’un navire sur la surface de la lune. Ce concept peut être lié au concept psychologique de « Flow ». Lorsqu’un utilisateur est entièrement absorbé dans une tâche qui a le bon mélange de stimulation et de récompense, ou en fait plus simplement, il est « dans la zone ».

En fait, le type le plus important d’immersion dans la réalité mixte est l’immersion spatiale. Le point de la réalité mixte est de tromper-nous en estimant que ces objets numériques existent dans le monde réel. Nous synthétisons des hologrammes dans notre environnement, immergés spatialement dans des environnements et des expériences entiers. Cela ne signifie pas que nous ne pouvons pas encore utiliser d’autres types d’immersion dans nos expériences, comme Atari l’ont fait avec une immersion tactile dans le Lander lunaire.

## <a name="designing-with-immersion"></a>Conception avec immersion

Comment pouvons-nous appliquer l’immersion tactile à un faites jaugé mis à jour vers Atari Classic ? Avant de s’attaquer au schéma d’entrée, la construction du jeu pour l’espace 3D doit être traitée.

![visualiser le mappage des surfaces dans HoloLens](images/surfacemapping.png)<br>
*Visualisation du mappage spatial dans HoloLens*

En tirant parti de l’environnement d’un utilisateur, nous avons des options de terrain infinies pour palier notre module lunaire. Pour que le jeu ressemble au titre d’origine, un utilisateur peut potentiellement manipuler et placer des blocages de différentes difficultés dans son environnement.

![volant le module lunaire](images/640px-lm-hero.jpg)<br>
*Volant le module lunaire*

Le fait de demander à l’utilisateur d’apprendre le schéma d’entrée, de contrôler le navire et de faire de la petite taille sur le terrain est beaucoup à demander. La réussite d’une expérience de jeu est la bonne combinaison de défis et de récompenses. L’utilisateur doit être en mesure de choisir un niveau de difficulté, le mode le plus simple nécessitant simplement que l’utilisateur se trouve dans une zone définie par l’utilisateur sur une surface analysée par le HoloLens. Une fois qu’un utilisateur obtient le blocage du jeu, il peut s’adapter à la difficulté qu’il voit.

### <a name="adding-input-for-hand-gestures"></a>Ajout d’entrées pour les gestes manuels

L’entrée de base HoloLens n’a que deux gestes : le [robinet et le toucher de l’air](gaze-and-commit.md#composite-gestures). Les utilisateurs n’ont pas besoin de mémoriser des nuances contextuelles ou une liste de mouvements spécifiques qui rendent l’interface de la plateforme polyvalente et facile à apprendre. Alors que le système peut uniquement exposer ces deux gestes, HoloLens en tant qu’appareil est en mesure de suivre deux mains à la fois. Notre Ode à la Lander lunaire est une [application immersive](app-model.md) , ce qui signifie que nous avons la possibilité d’étendre l’ensemble de base des gestes pour tirer parti de deux mains et ajouter nos propres moyens de navigation pour les modules lunaires.

En recherchant le schéma de contrôle d’origine, **nous avions besoin de résoudre la Poussée et la rotation**. L’inconvénient est la rotation dans le nouveau contexte ajoute un axe supplémentaire (techniquement deux, mais l’axe Y est moins important pour le débarquement). Les deux mouvements d’expédition distincts se prêtent naturellement à être mappés à chaque main :

![geste de pression et de glissement pour faire pivoter les Lander sur les trois axes](images/module-handdrag.gif)<br>
*Appuyer et faire glisser le geste pour faire pivoter les Lander sur les trois axes*

**Exercé**

Le levier sur la machine d’arcade d’origine est mappé à une échelle de valeurs, plus le levier a été déplacé, plus la Poussée a été appliquée au navire. Une nuance importante à souligner ici est que l’utilisateur peut prendre la main du contrôle et maintenir une valeur souhaitée. Nous pouvons efficacement utiliser le comportement tap-and-Drag pour obtenir le même résultat. La valeur de Poussée commence à zéro. L’utilisateur appuie sur le glisser-déplacer pour augmenter la valeur. À ce stade, ils peuvent laisser le jour. Toute modification de valeur de mouvement d’appui et de déplacement serait le delta de la valeur d’origine.

**Rotation**

C’est un peu plus délicat. Le fait de disposer de boutons de « rotation » holographiques permet d’effectuer une expérience terrible. Comme il n’y a pas de contrôle physique à exploiter, le comportement doit provenir de la manipulation d’un objet représentant le Lander ou du Lander lui-même. Nous avons obtenu une méthode qui utilise le tap-and-Drag qui permet à un utilisateur de « pousser » et de l’extraire dans le sens où il souhaite le faire face. À chaque fois qu’un utilisateur appuie et maintient, le point dans l’espace où le mouvement a été initié devient l’origine de la rotation. Le fait de faire glisser à partir de l’origine convertit le delta de la translation de la main (X, Y, Z) et l’applique au delta des valeurs de rotation de Lander. Ou plus simplement, le *fait de faire glisser le curseur vers la gauche <-> vers la droite, vers le haut < > vers le bas, vers l’arrière < de retour dans les espaces fait pivoter le navire en conséquence*.

Étant donné que le HoloLens peut effectuer le suivi de deux mains, la rotation peut être assignée à la main droite alors que la Poussée est contrôlée par la gauche. Finesse est le facteur déterminant pour la réussite de ce jeu. L' *aspect* de ces interactions est la priorité la plus élevée absolue. En particulier dans le contexte d’une immersion tactile. Un navire qui réagit trop rapidement serait inutilement difficile à prendre en main, tandis que l’un d’eux trop lent obligerait l’utilisateur à « pousser et tirer » sur le navire pour une durée beaucoup plus délicate.

### <a name="adding-input-for-game-controllers"></a>Ajout d’entrées pour les contrôleurs de jeu

Tandis que les gestes de main sur le HoloLens fournissent une nouvelle méthode de contrôle précis, il y a toujours un certain nombre de commentaires tactiles « vrai » que vous pouvez obtenir à partir des contrôles analogiques. La connexion d’un contrôleur de jeu Xbox permet de rétablir ce sens de la physique tout en tirant parti des bâtons de contrôle afin de conserver un contrôle affiné.

Il existe plusieurs façons d’appliquer le schéma de contrôle relativement simple au contrôleur Xbox. Étant donné que nous essayons de rester aussi près que possible de la configuration de l’arcade d’origine, la carte de **Poussée** est la mieux adaptée au bouton de déclenchement. Ces boutons sont des contrôles analogiques, ce qui signifie qu’ils ont plus de simples États *on et OFF* , ils répondent en fait au degré de pression qui leur est posé. Cela nous donne une construction similaire comme **levier de Poussée**. Contrairement au jeu d’origine et au mouvement manuel, ce contrôle réduit la poussée du navire une fois qu’un utilisateur a cessé de placer de la pression sur le déclencheur. Il donne toujours à l’utilisateur le même degré de finesse que le jeu d’arcade d’origine.

![stick analogique gauche est mappé sur le lacet et le rouleau, le Stick à droite est mappé à la tonalité et au rouleau](images/thumbsticksidebyside.gif)<br>
*Le stick analogique gauche est mappé sur le lacet et le roulis ; le joystick droit est mappé à la tonalité et au rouleau*

Le double Thumbsticks se prête naturellement à contrôler la rotation de l’expédition. Malheureusement, il y a 3 axes sur lesquels le navire peut pivoter et deux Thumbsticks qui prennent tous deux en charge deux axes. Cette incompatibilité signifie que l’un des deux contrôleurs est un axe ; ou il existe un chevauchement des axes pour le Thumbsticks. La première solution s’est terminée avec le sentiment « cassé », car Thumbsticks fusionne fondamentalement leurs valeurs X et Y locales. La dernière solution nécessitait des tests pour trouver les axes redondants les plus naturels. L’exemple final utilise le *lacet* et le *rouleau* (axes Y et x) pour le stick analogique gauche, ainsi que la hauteur et la *largeur* *(axes* Z et x) pour le stick analogique droit. Cela a pensé que la *Roll* la plus naturelle semble être parfaitement couplée avec le *lacet* et le *tangage*. En guise de note, l’utilisation de Thumbsticks pour le *Roll* se produit également pour doubler la valeur de rotation ; Il est assez amusant de faire en sorte que les Lander fassent des boucles.

Cet exemple d’application montre comment la reconnaissance spatiale et l’immersion tactile peuvent considérablement changer une expérience grâce aux modalités d’entrée extensible de Windows Mixed Reality. Alors que les Lander lunaires peuvent être proches de 40 ans d’âge, les concepts exposés avec ce petit petit-est en temps réel. En imaginant le futur, pourquoi ne pas regarder le passé ?

## <a name="technical-details"></a>Détails techniques

Vous trouverez des scripts et des prefabs pour l’exemple d’application de module lunaire sur le GitHub de conception de la [réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity_LunarModule).

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60"><img alt="Picture of Addison Linville" width="60" height="60" src="images/addisonlinville-tile-60px.jpg"></td>
<td style="border-style: none"><b>ADDISON Linville</b><br>@Microsoft du concepteur UX</td>
</tr>
</table>

## <a name="see-also"></a>Articles associés
* [Contrôleurs de mouvement](motion-controllers.md)
* [Pointer du regard vers l’avant et valider](gaze-and-commit.md)
* [Types d’applications de réalité mixte](types-of-mixed-reality-apps.md)
