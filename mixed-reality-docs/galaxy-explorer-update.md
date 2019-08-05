---
title: Création de l’Explorateur Galaxy pour HoloLens 2
description: Bienvenue dans la procédure de mise à jour de l’Explorateur Galaxy pour HoloLens 2. À l’instar de l’Explorateur Galaxy d’origine, notre équipe sera à l’origine du projet sur GitHub pour s’assurer que la Communauté dispose d’un accès complet.
author: l-garrett
ms.author: grbury
ms.date: 06/30/2019
ms.topic: article
keywords: Explorateur Galaxy, étude de cas, projet, exemple
ms.openlocfilehash: 1e04b27ff0382d87f8e6a15ae2b7b2284fa020e6
ms.sourcegitcommit: be3631932ea1c88ac3ad8b2390c98c5a6e8b93ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/04/2019
ms.locfileid: "68776472"
---
# <a name="the-making-of-galaxy-explorer-for-hololens-2"></a>Création de l’Explorateur Galaxy pour HoloLens 2

Bienvenue dans la procédure de mise à jour de l’Explorateur Galaxy pour HoloLens 2. [Explorateur Galaxy] L' (https://docs.microsoft.com/windows/mixed-reality/galaxy-explorer "Explorateur Galaxy") a été développé à l’origine en tant qu’application open source pour HoloLens (1ère génération) par le biais du programme partager votre idée, et est l’une des premières réalité mixtes que rencontrent de nombreuses personnes. À présent, nous mettons à jour ce dernier pour les [nouvelles fonctionnalités passionnantes de HoloLens 2](https://www.microsoft.com/hololens/hardware).

En tant qu’un des [Studios Microsoft Mixed Reality](galaxy-explorer-update.md#mixed-reality-studios), nous développons généralement des solutions de qualité commerciale et développons des tests & sur des plateformes cibles tout au long du processus de développement et créatif. Nous avons maintenant une situation unique où vous n’avez pas encore accès aux appareils HoloLens 2, mais que vous êtes ravi de démarrer les mises à jour de l’Explorateur Galaxy. Nous envoyons ce projet à l’aide des infrastructures et des outils (tels que [MRTK v2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html)) à mesure qu’ils sont mis à la disposition des États-Unis et de la Communauté, et nous souhaitons vous apporter le plus de temps.

À l’instar de l’Explorateur Galaxy d’origine, [notre équipe](galaxy-explorer-update.md#meet-the-team) sera à [l’origine du projet sur GitHub](https://github.com/Microsoft/GalaxyExplorer) pour s’assurer que la Communauté dispose d’un accès complet. Nous allons également documenter notre voyage ici dans une transparence complète sur la façon dont nous avons effectué le portage de MRTK v1 vers MRTK v2, la façon dont nous avons amélioré l’expérience en fonction des nouvelles fonctionnalités disponibles dans HoloLens 2, et de la façon dont nous avons veillé à ce que l’Explorateur Galaxy restait un expérience multi-plateforme. Si vous affichez l’Explorateur Galaxy sur HoloLens (1ère génération), HoloLens 2, un casque Windows Mixed Reality ou sur votre poste de travail Windows 10, nous souhaitons vous assurer que vous disposez d’une expérience immersive et que nous apprécions le voyage.

Cette page se développe au fur et à mesure que nous progressons dans le projet, et nous allons nous attacher à des articles plus détaillés, du code, des artefacts de conception, une documentation supplémentaire de MRTK v2, etc., afin de vous fournir une vue Insider du projet.

## <a name="unveiling-the-new-logo"></a>Présentation du nouveau logo

Nous sommes ravis de lancer une version préliminaire du nouveau logo de l’Explorateur Galaxy! Tout en payant hommage au logo d’origine, nous avons conçu une visualisation réaliste et mis à jour la typographie pour offrir une sensation plus élégante et plus moderne. L’une des nouvelles icônes est incluse dans le logo.

![Nouveau logo de l’Explorateur Galaxy](images/ge-update-app-icon.png)

La conception et la typographie du logo définissent la tonalité pour l’apparence globale des éléments d’interface utilisateur tout au long de l’expérience. 

## <a name="thinking-about-interactions"></a>Réflexion sur les interactions

En tant que Creative Studio, nous étions ecstatics sur le privilège de portage de l’Explorateur Galaxy vers HoloLens 2. Nous savions que nous souhaitions que l’expérience soit une fête du nouvel appareil et pour démontrer que l’autonomie de la réalité mixte est limitée uniquement à l’imagination.

HoloLens 2 permet aux utilisateurs de toucher, de saisir et de déplacer des hologrammes de manière naturelle: ils répondent beaucoup à des objets réels. Les modèles de handles entièrement articulés sont incroyables, car ils permettent aux utilisateurs de faire ce qu’ils estiment naturels. Par exemple, tout le monde sélectionne une tasse légèrement différente, et au lieu de mettre en œuvre une manière particulière de le faire, HoloLens 2 vous permet de le faire à votre façon.

>[!VIDEO https://www.youtube.com/embed/wogJv5v9x-s]

Il s’agit d’un grand changement par rapport aux interfaces basées sur le robinet sur les appareils HoloLens de première génération. Au lieu d’interagir avec des hologrammes à distance, les utilisateurs peuvent désormais se trouver «haut et proche». Lors du Portage d’expériences existantes vers HoloLens 2 ou en planifiant de nouvelles, il est important de vous familiariser avec la manipulation directe des hologrammes.

### <a name="direct-manipulation-vs-the-vast-distances-in-space"></a>Manipulation directe et les grandes distances dans l’espace

Il s’agit d’une expérience magique pour être en mesure d’atteindre, de saisir une planète et de la maintenir à portée de main. Le défi de cette approche est la taille du système solaire, c’est énorme! L’utilisateur doit parcourir sa salle pour se rapprocher de chaque planète pour pouvoir interagir avec lui.

Pour permettre aux utilisateurs d’interagir avec des objets plus éloignés, MRTK propose des rayons de main qui se déplacent à partir du centre de la paume de l’utilisateur, agissant comme une extension de la main. Un curseur en forme de bouée est attaché à la fin du rayon pour indiquer l’intersection entre le rayon et un objet cible. L’objet sur lequel le curseur atterrit peut alors recevoir des commandes gestuelles de la main. 

>[!VIDEO https://www.youtube.com/embed/Qol5OFNfN14]

Dans la version d’origine de l’Explorateur Galaxy, l’utilisateur ciblerait une planète avec le curseur en regard, puis appuyez sur air pour l’appeler plus près. Le moyen le plus simple de porter l’expérience dans HoloLens 2 est d’adopter ce comportement et d’utiliser des rayons de main pour sélectionner des planètes. Bien que cela soit fonctionnel, nous les avons laissés plus en plus.

### <a name="back-to-the-drawing-board"></a>Retour à la carte de dessin

Nous sommes parvenus à ideate ce qui pouvait être construit en plus des interactions existantes. Le raisonnement était le suivant: Bien que HoloLens 2 permette aux utilisateurs d’interagir avec des hologrammes de manière naturelle et réaliste, les hologrammes ne sont pas réels. Ainsi, tant qu’une interaction est plausible pour l’utilisateur, peu importe si cette interaction serait possible avec un vrai objet ou non, nous pouvons la rendre possible.

Un concept que nous avons exploré était basé sur Telekinesis, la puissance permettant de manipuler des objets à l’esprit. Souvent vu dans les films de super héros, une personne peut se joindre et appeler un objet dans sa main ouverte. Nous nous sommes mis en œuvre avec l’idée et nous sommes parvenus avec une ébauche rapide du fonctionnement du concept.

![Concept de l’interaction de manipulation forcée](images/ge-update-interactions-concept-force-grab.png)

L’utilisateur peut pointer le rayon de la main sur une planète, ce qui fournit des commentaires sur les cibles. À mesure que l’utilisateur étend sa main ouverte, la planète est déplacée vers l’utilisateur par une force magique jusqu’à ce qu’elle soit suffisamment proche pour être récupérée. Par conséquent, notre nom pour l’interaction: forcer la manipulation. À mesure que l’utilisateur pousse la planète avec sa main ouverte, il retournerait à son orbite.

### <a name="force-grab-prototyping"></a>Forcer le prototypage de la manipulation

Nous avons ensuite créé plusieurs prototypes pour tester le concept: Comment l’interaction a-t-elle un sens général? L’objet appelé doit-il s’arrêter devant l’utilisateur ou s’entourer de ses mains jusqu’à ce qu’il soit placé? L’objet appelé doit-il changer la taille ou la mise à l’échelle lors de l’appel?

<!--
Here is Amit Rojtblat (Technical Artist) presenting one of the prototypes to Yasushi Zonno (Creative Lead).

------------------------------------------------------------------

__*--- VIDEO OF AMIT PLAYING AND EXPLAINING THE PROTOTYPE ---*__

__*--- NEEDS TO BE UPLOADED (TO YOUTUBE?) AND LINKED ---*__

------------------------------------------------------------------
-->

### <a name="implementing-force-grab-into-the-application"></a>Implémentation de la manipulation forcée dans l’application

Lorsque nous avons essayé de s’emparer de la force sur les planètes, nous avons réalisé que nous devions modifier l’échelle du système solaire. Il s’est avéré qu’une représentation précise et de taille moyenne du système solaire est difficile pour les utilisateurs de comprendre et de naviguer. elles ne savent pas où chercher. Toutefois, une représentation précise de petite taille a rendu certaines planètes trop petites pour être facilement sélectionnées. Par conséquent, la taille des planètes et l’espacement entre les objets solaires ont été conçus pour se sentir à l’aise dans une salle de taille moyenne tout en maintenant la précision relative.

Au cours des étapes ultérieures de notre Sprint de développement, nous étions heureux d’avoir des experts en la réalité mixtes MSFT en interne. nous avons donc eu l’occasion d’obtenir leur contribution en tant que testeurs experts et d’effectuer des itérations rapides sur l’interaction de manipulation forcée.

![Isabelb Kam testant une version préliminaire de l’Explorateur Galaxy](images/ge-update-user-testing.png)

Dans l’image: Kam, responsable de la conception senior, qui teste un travail en cours de l’Explorateur Galaxy.

### <a name="adding-affordances-for-targeting"></a>Ajout de intuitivité pour le ciblage

À mesure que nous avons expérimentés sur HoloLens 2, nous avons constaté que bien que les nouvelles interactions soient naturelles et intuitives, les hologrammes restent les mêmes: sans aucune sensation de poids ou tactile. Étant donné que les hologrammes ne fournissent pas de commentaires naturels que les humains reçoivent lorsqu’ils interagissent avec les objets, nous avions besoin de les créer.

Nous avons pensé aux commentaires visuels et audio que les utilisateurs seraient fournis pour les différentes étapes de leurs interactions, et puisque le mécanisme de manipulation forcée est essentiel à l’interaction avec l’Explorateur Galaxy, nous avons effectué de nombreuses itérations. L’objectif était de trouver le juste équilibre entre les retours audio et visuels pour chaque étape de l’interaction: en se concentrant sur l’objet prévu, en l’appelant à l’utilisateur, puis en le publiant. Ce que nous avons appris, c’est que beaucoup plus de retours audio et visuels étaient requis pour renforcer l’interaction que celle utilisée pour HoloLens (1ère génération).

![Visual intuitivité sur les planètes](images/ge-update-planet-affordances.png)

### <a name="adding-affordances-for-force-grab"></a>Ajout de intuitivité pour la capture forcée
 
Une fois que nous avions le mécanisme de base de la manipulation forcée avec l’audio et l’intuitivité de Visual, nous avons vu comment sélectionner des planètes plus conviviales. Deux éléments principaux sont à prendre en compte: Étant donné que le système solaire est une interface de déplacement 3D, les utilisateurs ont une complexité supplémentaire pour apprendre à cibler les objets de manière cohérente. Cela a été aggravé par le fait que le rayon de la main est très rapide à la sélection d’un objet, ce qui fait que les planètes se déplacent très rapidement vers l’utilisateur.

Nous l’avons envisagée avec une solution à trois branches. Le premier était assez intuitif: Ralentissez le processus de sélection afin que les planètes approchent l’utilisateur à un rythme plus naturel. Une fois la vitesse réglée, nous avons dû revisiter l’audio et l’intuitivité visuel, en ajoutant des commentaires audio supplémentaires à mesure que la planète était suivie vers l’utilisateur.

La deuxième partie de la solution consistait à rendre la visualisation de l’intégralité de l’interaction de manipulation forcée extrêmement tangible. Nous avons visualisé une ligne épaisse qui se déplace vers l’objet ciblé une fois que la main Ray s’y connecte, puis remet l’objet à l’utilisateur, comme un lasso. 

![Intuitivité visuel «lasso» pour la capture forcée](images/ge-update-lasso-affordances.png)

Enfin, nous avons optimisé l’échelle du système solaire afin que les planètes soient suffisamment grandes pour que les rayons de l’utilisateur les ciblent. 

Ces trois améliorations permettaient aux utilisateurs d’effectuer des sélections précises, en leur appelant de manière intuitive. Globalement, l’effet de la capture de la force finale est une expérience plus immersive et interactive dans le système solaire.

## <a name="spotlight-on-jupiter"></a>Spotlight sur Jupiter

La création des corps solaires de la manière lactée était une expérience intéressant. En particulier, les caractéristiques uniques de Jupiter en font une vision de Behold. C’est la plus grande et la plus colorée des géants du gaz et contient plus de masse que toutes les autres planètes combinées. Sa taille et ses bandes mesmerizings de turbulence et de Dynamics Cloud sont Prefect pour une attention particulière.

### <a name="geometry-and-meshes"></a>Géométrie et maillages

En tant que géant du gaz, les coques externes de Jupiter se composent de couches gazeuses. La combinaison de sa vitesse de rotation rapide, de l’échange de chaleur interne et des forces de Coriolis crée des couches et des flux colorés qui constituent le tourbillon des ceintures et des Vortices. La capture de cette beauté compliquée était essentielle pour créer notre système solaire.

Il a été immédiatement clair que l’utilisation de techniques de visualisation comme les simulations de fluides et les textures animées avec des flux précalculés était en dehors des questions. La puissance de calcul requise pour simuler cette combinaison avec tout ce qui se passe simultanément aurait eu un impact négatif significatif sur les performances. 

![Vue d’ensemble de l’objet Jupiter](images/ge-update-jupiter-shells-complete.jpg)

L’approche suivante était une solution «fumée-and-Mirror», consistant à superposer des couches de texture transparentes, chacune ayant traité un aspect spécifique du mouvement atmosphérique, compilée sur une composition de mailles tournantes.

Dans l’image ci-dessous, vous pouvez voir l’interpréteur de commandes interne sur la gauche. Cette couche de Matt a fourni un arrière-plan à la composition pour se prémunir contre les petits écarts entre les différentes couches qui composent les clouds. En raison de la rotation lente de la couche, elle a également servi de tampon visuel entre les bandes mobiles plus rapides afin d’aider à créer une unité visuelle dans les couches.

Après avoir défini cette ancre sur le modèle, les couches Cloud mobiles ont ensuite été projetées sur les mailles du milieu et de droite, comme indiqué ci-dessous.

![Vue d’ensemble de l’objet Jupiter avec des coques séparées](images/ge-update-jupiter-shells-separated.jpg)

### <a name="texturing"></a>Texturation

La texture existante a été divisée en un Atlas de texture en trois parties: Le troisième héberge une couche motionless de clouds avec des trous pour fournir un effet de parallaxe, la section du milieu contient les flux externes à déplacement rapide, tandis que le tiers inférieur contient une couche de base interne pivotée lentement.

Le point rouge très caractéristique a également été divisé en plusieurs parties mobiles, puis insérées dans une zone de la texture autrement invisible. Ces composants peuvent être considérés comme des taches en rouge-toned dans la section du milieu de l’image ci-dessous.

Étant donné que chaque bande a une direction et une vitesse spécifiques, la texture a été appliquée individuellement à chaque maille. Les maillages comportaient alors un centre commun et un point pivot, afin de pouvoir animer de façon centrée la surface entière.

![Vue d’ensemble des textures Jupiter](images/ge-update-jupiter-planet-cloud-texture.png)

### <a name="rotation-and-texture-behavior"></a>Comportement de la rotation et de la texture

Maintenant que la composition visuelle de Jupiter a été définie, nous avons besoin de garantir que les vitesses de rotation et d’orbite ont été correctement calculées et appliquées en conséquence. Il faut environ 9 heures pour que Jupiter effectue une rotation complète. Il s’agit d’une question de définition en raison de sa rotation différentielle. Par conséquent, le flux équatoriale a été défini en tant que «flux maître», en utilisant 3600 frames pour une rotation complète. Chaque autre couche devait avoir une vitesse de rotation comme un facteur de 3600 afin de correspondre à sa position initiale, en autorisant par exemple 600, 900, 1200, 1800, etc.

![Textures de Shell Jupiter](images/ge-update-shell-texture.jpg)


### <a name="the-great-red-spot"></a>La belle zone rouge

Les flux de rotation individuels offraient une bonne impression visuelle, mais ils ne sont pas détaillés lorsqu’ils sont observés à la fin de la plage.

La partie la plus attrayante était la belle zone rouge de Jupiter. nous avons donc créé un ensemble de mailles et de textures spécifiquement pour la présenter.
 
Nous avons utilisé un mécanisme similaire à celui des bandes de Jupiter: un ensemble de parties tournantes se compose les unes sur les autres, tout en étant regroupées sous sa «couche principale» pour s’assurer qu’elles restent en position, quelle que soit la vitesse de déplacement du reste.

Lorsque les mailles ont été configurées et en place, différentes couches du vortex Storm ont été appliquées et chaque disque a ensuite été animé individuellement, le Centre se déplaçant plus rapidement, avec le reste progressivement ralenti lorsqu’il se déplace vers l’extérieur.

![De la maille rouge à points](images/ge-update-great-red-spot-mesh.jpg)

La composition avait également le même pivot que chaque autre maille, tout en conservant son inclinaison de l’axe y d’origine (!) pour permettre l’animation de la rotation. 3600 frames est le taux de base, chaque couche ayant un facteur comme une période de rotation.

![Texture de spots rouges Jupiter](images/ge-update-red-spot-mesh-texture.jpg)

### <a name="getting-it-right-in-unity"></a>Obtention du droit dans Unity

Il y a quelques points importants à garder à l’esprit lors de l’implémentation de This dans Unity.

Unity est facilement confondue lors du traitement de grands ensembles de couches transparentes. La solution consistait à dupliquer le matériel de texture pour chaque maillage et à appliquer des valeurs de file d’attente de rendu croissantes progressivement de l’intérieur vers l’extérieur de 5 à chaque matériau.

Le résultat était le shell interne avait une valeur de file d’attente de rendu de 3000 (valeur par défaut), la valeur externe rouge-toned statique avait une valeur de 3005, les clouds externes blancs rapides avaient 3010. Le point rouge (en progressant de l’intérieur à la couche externe) est terminé avec une valeur de 3025 dans ce modèle.

![Objet final Jupiter](images/ge-update-jupiter-final.jpg)

### <a name="final-touches"></a>Touches finales

Les couches Jupiter texturées ont été configurées au début, ce qui s’est avéré insuffisant pour l’implémentation.

Le nuanceur standard de la planète (et toutes ses variantes) reçoit les informations d’éclairage via un script, le SunLightReceiver, qui n’est pas pris en charge par le nuanceur standard MRTK.

Le simple fait de permuter les nuanceurs n’était pas une solution, car le nuanceur standard de planète ne prend pas en charge les cartes de texture avec des transparences. Nous avons modifié ce nuanceur afin que la build Jupiter fonctionne comme prévu.

Enfin, les fusions alpha devaient être configurées en affectant à la fusion source la valeur 10, ainsi qu’à la fusion de destination la valeur 5.

![Propriétés de Jupiter Unity](images/ge-update-jupiter-unity-render-queue.jpg)

Vous pouvez voir le rendu final de Jupiter dans l’Explorateur Galaxy.

## <a name="meet-the-team"></a>Rencontrez l’équipe 

Notre équipe de réalité mixte Studio est composée de concepteurs, d’artistes 3D, d’experts de l’expérience utilisateur, de développeurs, d’un responsable de programme et d’une tête de Studio. Nous sommes à la pointe du monde entier: La Belgique, le Canada, l’Allemagne, Israël, le Japon, le Royaume-Uni et le États-Unis. Nous sommes une équipe pluridisciplinaire qui vient d’un arrière-plan diversifié: les jeux, à la fois traditionnels et indie, le marketing numérique, les soins de santé et la science.

Nous sommes ravis de créer l’Explorateur Galaxy pour HoloLens 2 et de mettre à jour les versions HoloLens (1re génération), VR et Desktop. 

![L’équipe de l’Explorateur Galaxy](images/ge-update-team-image.png)

De gauche à droite: Artemis Tsouflidou (Developer), Angie Teickner (concepteur visuel), David Janer (Concepteur de l’expérience utilisateur), Laura Garrett (distribution & Lead de production), Yasushi Zonno (Creative Lead), Eline Ledent (Developer) et Ben Turner (SR. Developer).
En bas, de gauche à droite: Amit Rojtblat (artiste technique), Martin Wettig (3D Artist) et Dirk Songuer (Studio Head).
Non proposé: Tim Gerken (Lead Tech) et Oscar Saland (concepteur visuel).

## <a name="additional-information"></a>Informations supplémentaires

### <a name="mixed-reality-studios"></a>Studios de réalité mixte

Les équipes Microsoft Mixed Reality Studio, situées en Amérique, en Europe et en Asie-Pacifique, sont des experts de la conception de l’expérience utilisateur, de l’informatique holographique, des technologies AR/VR et du développement 3D. y compris la création de ressources 3D, DirectX, Unity et Unreal. Nous vous aidons à prévoir les futurs besoins, concevoir, créer et fournir des solutions, tout en permettant aux clients de créer un impact mesurable au sein de leur organisation. Les Studios travaillent en étroite collaboration avec plus de 22 000 professionnels des services Microsoft pour l’intégration, l’adoption, les opérations et le support des applications d’entreprise.
