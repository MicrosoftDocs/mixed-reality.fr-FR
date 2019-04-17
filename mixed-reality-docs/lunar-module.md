---
title: Module de lunaire
description: LunarModule est un exemple de l’open source d’application à partir de laboratoires de conception réalité mixte de Microsoft. Avec ce projet, vous pouvez apprendre à étendre les mouvements de base des Hololens avec le suivi des deux mains et Xbox contrôleur d’entrée, créer des objets qui sont réactives sur une aire de conception et recherche de plan et implémenter des systèmes de menu simple.
author: radicalad
ms.author: adlinv
ms.date: 03/21/2018
ms.topic: article
keywords: Windows mixte réalité, HoloLens des applications, conception, exemple
ms.openlocfilehash: 38f70d78b5572930b874e221fa4a85572c07b342
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595543"
---
# <a name="lunar-module"></a>Module de lunaire

>[!NOTE]
>Cet article présente un exemple exploratoire, nous avons créé dans le [laboratoires de conception de réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity), un emplacement où nous partageons nos connaissances acquises sur et des suggestions pour développement d’applications de réalité mixte. Nos articles relatifs à la conception et le code évoluera lors de nos nouvelles découvertes.

[Module de lunaire](https://github.com/Microsoft/MRDesignLabs_Unity_LunarModule) est un exemple de l’open source d’application à partir de laboratoires de conception réalité mixte de Microsoft. Avec ce projet, vous pouvez apprendre à étendre les mouvements de base des Hololens avec le suivi des deux mains et Xbox contrôleur d’entrée, créer des objets qui sont réactives sur une aire de conception et recherche de plan et implémenter des systèmes de menu simple. Tous les composants du projet sont disponibles pour une utilisation dans vos propres expériences d’application de réalité mixte.

## <a name="rethinking-classic-experiences-for-windows-mixed-reality"></a>Repenser l’expérience classique pour la réalité mixte Windows

Haut élevé dans l’atmosphère, un petit navire rappelle celle du module Apollo enquêtes méthodiquement terrain en escalier ci-dessous. Notre opération pilote crains repérer une zone d’accueil approprié. La profondeur est compliquée mais heureusement, ce parcours a été maintes reprises...

![Interface d’origine à partir du jeu Atari 1979 lunaire Lander](images/640px-atari-lunar-lander.png)<br>
*Interface d’origine à partir du jeu Atari 1979 lunaire Lander*

[Lunaire Lander](https://en.wikipedia.org/wiki/Lunar_Lander_(1979_video_game)) est un classique d’arcade que tentent de joueurs pour piloter un lander lune vers un emplacement plat de terrain lunaire. Toute personne nés dans les années 1970 a probablement passé des heures dans une arcade avec leurs yeux collé à cette livraison de vector plummeting du ciel. Comme un lecteur navigue leur expédition vers une zone de lancement de votre choix au terrain met à l’échelle progressivement plus détaillée. Réussite signifie d’accueil dans le seuil sécurisé de vitesse horizontal et vertical. Les points sont attribués pour les temps de lancement et restant de carburant, avec un multiplicateur selon la taille de la zone d’accueil.

Outre le jeu, l’ère arcade de jeux mis innovation constante des schémas de contrôle. Des configurations manette de jeu et bouton 4 voies la plus simple (vu dans sous la forme d’icône [Pac-Man](https://en.wikipedia.org/wiki/Pac-Man)) pour les schémas complexes et hautement spécifiques illustrés à la fin des années 90 et 00s (comme ceux utilisés dans les simulateurs de golf et subjectifs de rail). Le schéma d’entrée utilisé dans la machine Lander lunaire est particulièrement prometteur pour deux raisons : maîtriser le recours et immersion.

![Console d’arcade de Lander Atari lunaire](images/atariconsole.png)<br>
*Console de jeu Atari Lander lunaire arcade*

Pourquoi Atari et nombre d’autres entreprises jeu décidé de repenser l’entrée ?

Un kid parcourant une arcade est naturellement être intrigué par la plus récente, flashiest machine. Mais Lander lunaire un garagiste d’entrée nouveaux qui distingué des autres candidats.

Lander lunaire utilise deux boutons de rotation de l’expédition de gauche et droite et un **poussée levier** pour contrôler la quantité de produit de la livraison de poussée. Cette manette représente offre aux utilisateurs un certain niveau d’un joystick régulière ne peut pas fournir de finesse. Il est également se trouve être un composant commun pour les cockpits aviation modernes. Atari souhaitait lunaire Lander au cœur de l’utilisateur dans le sentiment qu’ils ont été pilotage en fait d’un module lunaire. Ce concept est appelé **immersion tactile**.

Immersion tactile est l’expérience de commentaires organes d’effectuer des actions répétitives. Dans ce cas, l’action répétitive d’ajustement de la manette de limitation et la rotation qui consultez nos yeux et nos oreilles entendre, permet de connecter le lecteur à l’acte de lancement d’un navire sur la surface de la lune. Ce concept peut être lié au concept psychologique de « flux ». Lorsqu’un utilisateur est entièrement pris en charge dans une tâche qui a le droit mélange de challenge et de récompense ou plus simplement, ils sont « dans la zone ».

En fait, le type phare d’immersion dans la réalité mixte est immersion spatiale. L’objectif de réalité mixte est nous-mêmes tromper en lui faisant croire ces objets numériques existent dans le monde réel. Nous allons synthétiser hologrammes à notre environnement, en étant immergé dans l’espace dans les expériences et des environnements entiers. Cela ne signifie pas que nous ne pouvons pas toujours employer des autres types d’immersion dans nos expériences comme Atari l’avez fait avec tactile immersion dans Lander lunaire.

## <a name="designing-with-immersion"></a>Conception d’immersion

Comment pourrions nous s’appliquent immersion tactile à une mise à jour, volumétrique suite le Atari classique ? Avant d’entreprendre le schéma d’entrée, la construction de jeu pour l’espace 3D doit être traité.

![Visualisation de mappage de l’aire de conception dans HoloLens](images/surfacemapping.png)<br>
*Visualisation de mappage spatial dans HoloLens*

En tirant parti de son environnement d’un utilisateur, nous avons efficacement les options de terrain infinie d’arrivée de notre module lunaire. Pour que le jeu la plupart des comme le titre d’origine, un utilisateur peut potentiellement manipuler et placez les panneaux d’accueil de difficultés différentes dans leur environnement.

![Battant le Module lunaire](images/640px-lm-hero.jpg)<br>
*Battant le Module lunaire*

Obliger l’utilisateur à apprendre le schéma d’entrée, contrôler le navire et ont une petite cible arrivent sur est beaucoup de choses à demander. Les fonctionnalités d’une expérience de jeu réussi la combinaison équilibrée de challenge et de récompense. L’utilisateur doit être en mesure de choisir un niveau de difficulté, avec le mode le plus simple demandant simplement à l’utilisateur avec succès arrivent dans une zone définie par l’utilisateur sur une surface analysés par le HoloLens. Une fois qu’un utilisateur obtient le blocage du jeu, ils peuvent ensuite Casquette de la difficulté à leur convenance.

### <a name="adding-input-for-hand-gestures"></a>Ajout d’une entrée pour les mouvements de main

Entrée de base de HoloLens a uniquement deux mouvements - [appuyez sur Air et Bloom](gestures.md). Les utilisateurs n’aient pas à vous souvenir nuances contextuelles ou une liste de linge de gestes spécifiques, ce qui rend les interface de la plateforme souple et facile à apprendre. Alors que le système peut exposer uniquement ces deux mouvements, HoloLens en tant qu’appareil est capable de suivi à la fois des deux mains. Notre ode à Lander lunaire est un [application captivante](app-model.md) ce qui signifie que nous avons la possibilité d’étendre l’ensemble de mouvements à tirer parti des deux mains et d’ajouter nos propres moyens délicieusement tactiles pour la navigation lunaire module de base.

Si l'on examine le schéma de contrôle d’origine, **nous avions besoin résoudre de poussée et de rotation**. L’inconvénient est la rotation dans le nouveau contexte ajoute un axe supplémentaire (techniquement, deux, mais l’axe des Y est moins importante pour d’accueil). Les mouvements de livraison distinctes deux prêtent naturellement à associer à chaque main :

![Appuyez sur, puis faites glisser le mouvement pour faire pivoter lander sur tous les trois axes](images/module-handdrag.gif)<br>
*Appuyez sur, puis faites glisser le mouvement pour faire pivoter lander sur tous les trois axes*

**Poussée**

La manette sur l’ordinateur d’origine arcade mappée à une échelle de valeurs, plus la manette a été déplacée la plus poussée a été appliquée à la livraison. Une nuance importante à noter ici est l’utilisateur peut prendre la main sur le contrôle et mettre à jour une valeur souhaitée. Nous pouvons utiliser efficacement de comportement du tap et faites glisser pour obtenir le même résultat. La valeur de la poussée commence à zéro. L’utilisateur appuie sur et fait glisser pour augmenter la valeur. À ce stade, ils peuvent laisser tomber à sa conservation. Toute modification de valeur tap et geste serait le delta à partir de la valeur d’origine.

**Rotation**

Il s’agit d’un peu plus difficile. Avoir des boutons « rotate » holographique et profitez de fait pour une expérience catastrophique. Il n’est pas un contrôle physique pour tirer parti, donc le comportement doit provenir de manipulation d’un objet représentant le lander, ou avec le lander lui-même. Nous avons élaboré une méthode à l’aide de clic et glisser qui permet à un utilisateur d’efficacement « push et pull » dans le sens où ils le souhaitent faire face. Lorsqu’un utilisateur appuie sur et qu’il conserve, le point dans l’espace où le mouvement a été initié devient l’origine pour la rotation. En faisant glisser depuis l’origine convertit le delta de traduction de la main (X, Y, Z) et l’applique au delta des valeurs de rotation de la lander. Ou plus simplement, *en faisant glisser gauche <> – droite, haut <> – vers le bas, vers l’avant <> – dans les espaces en conséquence fait pivoter le navire*.

Dans la mesure où le HoloLens peut suivre deux mains, rotation permettre être allouée à la vers la droite, tandis que la poussée est contrôlée par la gauche. Finesse est un facteur déterminant pour la réussite dans ce jeu. Le *sentir* de ces interactions est la plus haute priorité absolue. En particulier dans le contexte d’immersion tactile. Un destinataire qui réagit trop rapidement serait inutilement difficile de diriger, pendant une trop lent nécessiterait l’utilisateur de « push et pull » sur la livraison pour un laps de temps prolongé maladroitement.

### <a name="adding-input-for-game-controllers"></a>Ajout d’une entrée pour les contrôleurs de jeu

Tandis que les mouvements de la main sur le HoloLens fournissent la nouvelle méthode d’un contrôle précis, il existe toujours un certain manque de rétroaction tactile 'true' que vous obtenez à partir de contrôles analogiques. Permet de se connecter à un contrôleur de jeu Xbox pour ramener ce goût physicality tout en exploitant les modules de contrôle pour conserver un contrôle précis.

Il existe plusieurs façons d’appliquer le schéma de contrôle de relativement simple au contrôleur Xbox. Étant donné que nous tentons de rester plus près l’arcade d’origine configurés en tant que possible, **poussée** mappe le mieux au bouton du déclencheur. Ces boutons sont des contrôles analogiques, ce qui signifie qu’ils ont plus que de simples *et désactiver* indique, ils répondent en fait au degré de sollicitation de la placer sur ces derniers. Cela nous donne une construction similaire en tant que le **poussée levier**. Contrairement au jeu d’origine et le mouvement de la main, ce contrôle sera Couper poussée du navire une fois qu’un utilisateur arrête l’ajout de pression sur le déclencheur. Il offre de l’utilisateur le même degré de finesse comme le faisait le jeu d’arcade d’origine.

![Stick analogique gauche est mappé pour lacet et à une restauration, Stick analogique droit est mappé pour discuter et à une restauration](images/thumbsticksidebyside.gif)<br>
*Stick analogique gauche est mappé pour lacet et restaurer ; stick analogique droit est mappé pour discuter et à une restauration*

Les sticks analogiques doubles naturellement se prêtent à contrôle rotation d’expédition. Malheureusement, il existe 3 axes sur laquelle le destinataire peut faire pivoter et deux sticks analogiques qui les prennent en charge les deux axes. Cette incohérence signifie soit un stick analogique contrôles un axe ; ou il existe un chevauchement des axes pour la sticks analogiques. La première solution retrouvés vous vous sentez « interrompue » dans la mesure où sticks analogiques blend, par nature, leur local des valeurs X et Y. La deuxième solution requis des tests pour trouver les axes redondants naturelles le plus. L’exemple final utilise *lacet* et *restaurer* (axes X et Y) pour le stick analogique gauche, et *pitch* et *restaurer par* (axes Z et X) pour le droit stick analogique. Cela pensé plus naturel que *rouleau* semble indépendamment s’associer à bien *lacet* et *pitch*. Note à part, à l’aide de ces deux sticks analogiques pour *rouleau* se trouve également double de la valeur de rotation ; c’est très amusant d’avoir le lander de boucles do loops.

Cet exemple d’application montre comment spatiale reconnaissance et immersion tactile peut changer considérablement d’une expérience grâce à des modalités d’entrée extensibles de réalité mixte Windows. Tandis que Lander lunaire peut être arrivent à 40 ans dans l’âge, les concepts exposés avec que peu octogone avec legs se trouvera sur constant. Lorsque vous imaginer à l’avenir, pourquoi ne pas consulter le passé ?

## <a name="technical-details"></a>Détails techniques

Vous pouvez trouver des scripts et prefabs pour l’exemple d’application lunaire Module sur le [GitHub de laboratoires de conception réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity_LunarModule).

## <a name="about-the-author"></a>À propos de l’auteur

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60"><img alt="Picture of Addison Linville" width="60" height="60" src="images/addisonlinville-tile-60px.jpg"></td>
<td style="border-style: none"><b>Addison Linville</b><br>Concepteur UX @Microsoft</td>
</tr>
</table>

## <a name="see-also"></a>Voir aussi
* [Contrôleurs de mouvement](motion-controllers.md)
* [Mouvements](gestures.md)
* [Types d’applications de réalité mixte](types-of-mixed-reality-apps.md)
