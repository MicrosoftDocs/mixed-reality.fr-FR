---
title: Conception de mappage spatial
description: L’utilisation effective du mappage spatial dans HoloLens requiert un examen attentif de nombreux facteurs.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, mappage spatial, HoloLens, reconstruction de surface, maille
ms.openlocfilehash: 02e64727f9a23bea28e018d7c4e5a8b89c152447
ms.sourcegitcommit: 60f73ca23023c17c1da833c83d2a02f4dcc4d17b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69566009"
---
# <a name="spatial-mapping-design"></a>Conception de mappage spatial

L’utilisation effective du mappage spatial dans HoloLens requiert un examen attentif de nombreux facteurs.

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Conception de mappage spatial</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="why-is-spatial-mapping-important"></a>Pourquoi le mappage spatial est-il important?

Le mappage spatial permet de placer des objets sur des surfaces réelles. Cela permet d’ancrer les objets dans le monde de l’utilisateur et de tirer parti des indications de profondeur dans le monde réel. Boucher vos hologrammes en fonction d’autres hologrammes et des objets réels vous aide à convaincre l’utilisateur que ces hologrammes sont en fait dans leur espace. Les hologrammes flottants en espace ou en mouvement avec l’utilisateur ne seront pas aussi réels. Lorsque cela est possible, placez les éléments pour plus de confort.

Visualisez les surfaces lors du placement ou du déplacement d’hologrammes (utilisez une grille projetée simple). Cela permet à l’utilisateur de savoir où il peut placer ses hologrammes et montre l’utilisateur si l’endroit où il tente de placer l’hologramme n’a pas encore été mappé. Vous pouvez «encadrer des éléments» pour l’utilisateur s’ils finissent à un trop grand angle.

## <a name="what-influences-spatial-mapping-quality"></a>Qu’est-ce qui influence la qualité du mappage spatial?

Plusieurs facteurs, détaillés [ici](environment-considerations-for-hololens.md), peuvent affecter la fréquence et la gravité de ces erreurs.  Toutefois, vous devez concevoir votre application afin que l’utilisateur puisse atteindre ses objectifs même en présence d’erreurs dans les données de mappage spatiale.

## <a name="the-environment-scanning-experience"></a>Expérience d’analyse de l’environnement

Chaque application qui utilise le mappage spatial doit envisager de fournir une «expérience d’analyse»; processus par lequel l’application guide l’utilisateur pour analyser les surfaces nécessaires au bon fonctionnement de l’application.

![Exemple d’analyse](images/sr-mixedworld-140429-8pm-00068-1000px.png)<br>
*Exemple d’analyse*

La nature de cette expérience d’analyse peut varier considérablement en fonction des besoins de chaque application, mais deux principes principaux doivent guider sa conception.

Tout d’abord, une **communication claire avec l’utilisateur est la préoccupation principale**. L’utilisateur doit toujours savoir si les exigences de l’application sont respectées. Lorsqu’ils ne sont pas satisfaits, l’utilisateur doit immédiatement savoir pourquoi c’est le cas et il doit être rapidement dirigé pour prendre les mesures appropriées.

Deuxièmement, **les applications doivent tenter d’équilibrer l’efficacité et la fiabilité**. Lorsqu’il est possible de le faire de façon **fiable**, les applications doivent analyser automatiquement les données de mappage spatiale pour économiser le temps utilisateur. Lorsqu’il n’est pas possible de le faire de manière fiable, les applications doivent à la place permettre à l’utilisateur de fournir rapidement à l’application les informations supplémentaires dont il a besoin.

Pour faciliter la conception de l’expérience d’analyse, prenez en compte les possibilités suivantes applicables à votre application:

* **Aucune expérience d’analyse**
   * Une application peut fonctionner parfaitement sans aucune expérience d’analyse guidée. elle présente des informations sur les surfaces observées au cours du déplacement des utilisateurs naturels.
   * Par exemple, une application qui permet à l’utilisateur de dessiner sur des surfaces avec la peinture de pulvérisation holographique ne nécessite que les connaissances des surfaces actuellement visibles pour l’utilisateur.
   * L’environnement peut être complètement analysé s’il s’agit d’un environnement dans lequel l’utilisateur a déjà passé beaucoup de temps à l’aide de HoloLens.
   * Gardez à l’esprit que l’appareil photo utilisé par le mappage spatial ne peut voir que 3,1 m devant l’utilisateur; par conséquent, le mappage spatial ne connaîtra pas d’autres surfaces distantes, sauf si l’utilisateur les a observées à partir d’une distance plus proche dans le passé.
   * L’utilisateur comprend donc les surfaces qui ont été analysées, l’application doit fournir un retour visuel à cet effet. par exemple, le cast d’ombres virtuelles sur des surfaces numérisées peut aider l’utilisateur à placer des hologrammes sur ces surfaces.
   * Dans ce cas, les volumes limites de l’observateur de surface spatiale doivent être mis à jour sur chaque cadre pour obtenir un [système de coordonnées spatiales](coordinate-systems.md)verrouillé, afin qu’ils suivent l’utilisateur.

* **Trouver un emplacement approprié**
   * Une application peut être conçue pour être utilisée dans un emplacement avec des exigences spécifiques.
   * Par exemple, l’application peut nécessiter une zone vide autour de l’utilisateur afin qu’elle puisse s’assurer en toute sécurité le kung-fou holographique.
   * Les applications doivent communiquer toutes les exigences spécifiques à l’utilisateur au préalable et les renforcer avec des commentaires visuels clairs.
   * Dans cet exemple, l’application doit visualiser l’étendue de la zone vide requise et mettre visuellement en évidence la présence d’objets non désirés dans cette zone.
   * Dans ce cas, les volumes limites de l’observateur de surface spatiale doivent utiliser un système de [coordonnées spatiales](coordinate-systems.md) verrouillé à l’emplacement choisi.

* **Rechercher une configuration appropriée des surfaces**
   * Une application peut nécessiter une configuration spécifique de surfaces, par exemple deux parois larges, plates et opposées pour créer un couloir holographique de miroirs.
   * Dans ce cas, l’application doit analyser les surfaces fournies par le mappage spatial pour détecter les surfaces appropriées et diriger l’utilisateur vers ces surfaces.
   * L’utilisateur doit avoir une option de secours si l’analyse des surfaces de l’application n’est pas complètement fiable. Par exemple, si l’application identifie de manière incorrecte une porte comme un mur plat, l’utilisateur a besoin d’un moyen simple de corriger cette erreur.

* **Analyser une partie de l’environnement**
   * Une application peut souhaiter uniquement capturer une partie de l’environnement, comme indiqué par l’utilisateur.
   * Par exemple, l’application analyse une partie d’une salle afin que l’utilisateur puisse poster une publicité classée holographique pour le mobilier qu’elle souhaite vendre.
   * Dans ce cas, l’application doit capturer les données de mappage spatiale dans les régions observées par l’utilisateur lors de son analyse.

* **Analyser la totalité de la salle**
   * Une application peut nécessiter une analyse de toutes les surfaces dans la salle actuelle, y compris celles qui se trouvent derrière l’utilisateur.
   * Par exemple, un jeu peut mettre l’utilisateur dans le rôle de Gulliver, sous siege à partir de centaines de petites Lilliputians approchant de toutes les directions.
   * Dans ce cas, l’application doit déterminer le nombre de surfaces de la salle active qui ont déjà été analysées et diriger le point de regard de l’utilisateur pour combler les lacunes significatives.
   * La clé de ce processus consiste à fournir des commentaires visuels qui démontrent à l’utilisateur que les surfaces n’ont pas encore été analysées. L’application peut, par exemple, utiliser [un brouillard basé](https://msdn.microsoft.com/library/windows/desktop/bb173401%28v=vs.85%29.aspx) sur la distance pour mettre visuellement en surbrillance des zones qui ne sont pas couvertes par des surfaces de mappage spatiale.

* **Prendre un instantané initial de l’environnement**
   * Une application peut souhaiter ignorer toutes les modifications apportées à l’environnement après avoir effectué un «instantané» initial.
   * Cela peut être utile pour éviter toute interruption des données créées par l’utilisateur qui est étroitement couplée à l’état initial de l’environnement.
   * Dans ce cas, l’application doit faire une copie des données de mappage spatiale dans son état initial une fois l’analyse terminée.
   * Les applications doivent continuer à recevoir des mises à jour des données de mappage spatiale si les hologrammes continuent d’être correctement bloquéss par l’environnement.
   * Les mises à jour continues des données de mappage spatiale permettent également de visualiser les modifications qui se sont produites, en clarifiant l’utilisateur les différences entre les États antérieur et présent de l’environnement.

* **Prendre des instantanés initiés par l’utilisateur de l’environnement**
   * Une application ne souhaite peut-être répondre aux modifications environnementales que lorsqu’il est demandé par l’utilisateur.
   * Par exemple, l’utilisateur peut créer plusieurs «statues» en 3D d’un ami en capturant ses poses à des moments différents.

* **Autoriser l’utilisateur à modifier l’environnement**
   * Une application peut être conçue pour répondre en temps réel à toute modification apportée à l’environnement de l’utilisateur.
   * Par exemple, l’utilisateur qui dessine un rideau peut déclencher une «modification de la scène» pour qu’une lecture holographique se déroule de l’autre côté.

* **Guide de l’utilisateur pour éviter les erreurs dans les données de mappage spatiale**
   * Une application peut souhaiter fournir des conseils à l’utilisateur pendant qu’il analyse son environnement.
   * Cela peut aider l’utilisateur à éviter certains types d' [Erreurs dans les données de mappage spatiale](spatial-mapping-design.md#what-influences-spatial-mapping-quality), par exemple en restant à l’écart des fenêtres ou miroirs Sunlit.

L’un des détails supplémentaires à prendre en compte est que la «plage» de données de mappage spatiale n’est pas illimitée. Tandis que le mappage spatial crée une base de données permanente d’espaces de grande taille, il ne rend ces données disponibles qu’aux applications dont la taille est limitée à l’utilisateur. Par conséquent, si vous commencez au début d’un couloir long et que vous vous éloignez suffisamment du début, les surfaces spatiales finissent par disparaître. Vous pouvez bien sûr atténuer cela en mettant en cache ces surfaces dans votre application une fois qu’elles ont disparu des données de mappage spatiale disponibles.

## <a name="mesh-processing"></a>Traitement de maillage

Il peut être utile de détecter les types courants d’erreurs dans les surfaces et de filtrer, supprimer ou modifier les données de mappage spatiale comme il convient.

Gardez à l’esprit que les données de mappage spatiale sont destinées à être aussi fidèles que possible pour les surfaces réelles, de sorte que tout traitement que vous appliquez risque de faire passer vos surfaces plus loin de la «vérité».

Voici quelques exemples de différents types de traitement de maillage qui peuvent s’avérer utiles:

* **Remplissage de trous**
   * Si un petit objet constitué d’un matériau sombre ne parvient pas à être analysé, il laisse un trou dans la surface environnante.
   * Les trous affectent l’occlusion: les hologrammes peuvent être vus «jusqu’à» un trou dans une surface réaliste opaque.
   * Les trous affectent raycasts: Si vous utilisez raycasts pour aider les utilisateurs à interagir avec les surfaces, il peut être indésirable que ces rayons passent par des trous. Une solution de contournement consiste à utiliser un groupe de plusieurs raycasts couvrant une région de taille appropriée. Cela vous permettra de filtrer les résultats «aberrants», de sorte que même si un raycast traverse un petit trou, le résultat de l’agrégat restera valide. Toutefois, gardez à l’esprit que cette approche est un coût de calcul.
   * Les trous affectent les collisions physiques: un objet contrôlé par la simulation physique peut déplacer un trou à l’étage et être perdu.
   * Il est possible d’effectuer un remplissage algorithmique de ces trous dans le maillage des surfaces. Toutefois, vous devrez régler votre algorithme pour que les «véritables trous», tels que les fenêtres et les portes, ne soient pas remplis. Il peut être difficile de distinguer de manière fiable les «véritables trous» de «trous imaginaires». vous devrez donc faire des essais avec différents heuristiques, tels que «taille» et «forme limite».

* **Suppression de hallucination**
   * Les réflexions, les lumières brillantes et les objets mobiles peuvent rendre le petit «hallucinations» en attente flottant dans le milieu de l’air.
   * Hallucinations affecte l’occlusion: les hallucinations peuvent devenir visibles en tant que formes sombres se déplaçant devant et obturant d’autres hologrammes.
   * Hallucinations affecte raycasts: Si vous utilisez raycasts pour aider les utilisateurs à interagir avec les surfaces, ces rayons peuvent toucher un hallucination au lieu de la surface derrière. Comme avec les trous, une atténuation consiste à utiliser un grand nombre de raycasts au lieu d’un raycast unique, mais à nouveau cela aura un coût de calcul.
   * Les hallucinations affectent les collisions physiques: un objet contrôlé par la simulation physique peut être bloqué contre un hallucination et ne peut pas se déplacer dans une zone d’espace apparemment claire.
   * Il est possible de filtrer ce hallucinations à partir de la maille de surface. Toutefois, comme pour les trous, vous devez régler votre algorithme pour que les petits objets tels que les poignées de la porte et les béquilles ne soient pas supprimés.

* **Lissage**
   * Le mappage spatial peut retourner des surfaces qui semblent être rugueuses ou bruyantes par rapport à leurs équivalents réels.
   * Le lissage affecte les collisions physiques: si le plancher est grossier, une boule de golf simulée physiquement peut ne pas s’effectuer correctement sur une ligne droite.
   * Le lissage affecte le rendu: si une surface est visualisée directement, les normales des surfaces approximatives peuvent avoir une incidence sur l’apparence et perturber l’apparence d’un «nettoyage». Il est possible de réduire cela en utilisant l’éclairage et les textures appropriés dans le nuanceur qui est utilisé pour afficher l’aire.
   * Il est possible de lisser l’irrégularité dans un maillage de surface. Toutefois, cela peut éloigner la surface de la surface réelle correspondante. Il est important de maintenir une correspondance étroite pour produire une occlusion d’hologramme précise et permettre aux utilisateurs d’effectuer des interactions précises et prévisibles avec des surfaces holographiques.
   * Si seule une modification cosmétique est nécessaire, elle peut suffire à lisser les normales des sommets sans modifier les positions des sommets.

* **Recherche de plan**
   * Il existe de nombreuses formes d’analyse qu’une application peut souhaiter effectuer sur les surfaces fournies par le mappage spatial.
   * Un exemple simple consiste à «rechercher dans le plan». identification des régions délimitées, principalement planaires des surfaces.
   * Les régions planaires peuvent être utilisées comme des surfaces de travail holographiques, des régions où le contenu holographique peut être automatiquement placé par l’application.
   * Les régions planaires peuvent contraindre l’interface utilisateur, afin de guider les utilisateurs afin qu’ils puissent interagir avec les surfaces qui répondent le mieux à leurs besoins.
   * Les régions planaires peuvent être utilisées comme dans le monde réel, pour les équivalents holographiques aux objets fonctionnels, tels que les écrans LCD, les tables ou les tableaux blancs.
   * Les régions planaires peuvent définir des zones de lecture, formant ainsi la base des niveaux Videogame.
   * Les régions planaires peuvent aider les agents virtuels à naviguer dans le monde réel, en identifiant les zones d’étage que les gens sont susceptibles de parcourir.

## <a name="prototyping-and-debugging"></a>Prototypage et débogage

### <a name="useful-tools"></a>Outils utiles
* L' [émulateur hololens](using-the-hololens-emulator.md) peut être utilisé pour développer des applications à l’aide du mappage spatial sans accès à un HoloLens physique. Elle vous permet de simuler une session active sur un HoloLens dans un environnement réaliste, avec toutes les données que votre application consomme normalement, y compris le mouvement HoloLens, les systèmes de coordonnées spatiales et les maillages de mappage spatial. Cela peut être utilisé pour fournir des entrées fiables et reproductibles, ce qui peut être utile pour déboguer des problèmes et évaluer des modifications apportées à votre code.
* Pour reproduire un scénario, capturez les données de mappage spatiale sur le réseau à partir d’un HoloLens actif, puis enregistrez-les sur le disque et réutilisez-les dans les sessions de débogage suivantes.
* La [vue 3D du portail d’appareils Windows](using-the-windows-device-portal.md#3d-view) fournit un moyen de voir toutes les surfaces spatiales actuellement disponibles via le système de mappage spatial. Cela fournit une base de comparaison pour les surfaces spatiales à l’intérieur de votre application. par exemple, vous pouvez facilement savoir si des surfaces spatiales sont manquantes ou affichées au mauvais endroit.

### <a name="general-prototyping-guidance"></a>Conseils généraux sur le prototypage
* Étant donné que les [Erreurs](spatial-mapping-design.md#what-influences-spatial-mapping-quality) dans les données de mappage spatiale peuvent affecter fortement l’expérience de votre utilisateur, nous vous recommandons de tester votre application dans un large éventail d’environnements.
* Ne vous retrouvez pas à l’habitude de toujours tester dans le même emplacement, par exemple au niveau de votre bureau. Veillez à effectuer des tests sur différentes surfaces de différentes positions, formes, tailles et matériaux.
* De même, si les données synthétiques ou enregistrées peuvent être utiles pour le débogage, ne vous inquiétez pas trop sur les mêmes cas de test. Cela peut retarder la recherche de problèmes importants que des tests plus variés auraient été détectés précédemment.
* Il est judicieux d’effectuer des tests avec des utilisateurs réels (et idéalement non-surveillés), car ils ne peuvent pas utiliser le HoloLens ou votre application exactement de la même façon que vous le faites. En fait, il peut être surpris de savoir comment le comportement, les connaissances et les hypothèses de personnes divergentes peuvent être!

## <a name="see-also"></a>Voir aussi
* [Visualisation du balayage d’une pièce](room-scan-visualization.md)
* [Conception du son spatial](spatial-sound-design.md)
* [Persistance dans Unity](persistence-in-unity.md)
