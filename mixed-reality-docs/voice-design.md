---
title: Exécution des commandes vocales
description: Regards, les gestes et voix (GGV) constituent le principal moyen d’interaction sur HoloLens. Cet article fournit une assistance détaillée sur la conception de la voix.
author: shentan
ms.author: shentan
ms.date: 04/21/2019
ms.topic: article
ms.localizationpriority: high
keywords: Windows Mixed Reality, conception, interaction, voix
ms.openlocfilehash: f2362400cba2946c3e97a7128c410ddcd17b4362
ms.sourcegitcommit: 5b4292ef786447549c0199003e041ca48bb454cd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402369"
---
# <a name="voice-commanding"></a>Exécution des commandes vocales

Lorsque vous utilisez les commandes vocales, regards est généralement utilisé comme le ciblage mechaninism, soit comme un pointeur (« select ») ou d’indiquer à votre commande à une application (« voir, dites-le »). Bien entendu, certaines commandes vocales ne nécessitent pas une cible, comme « accédez à démarrer » ou « Hé, Cortana. »


## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1er gen)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>Exécution des commandes vocales</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️ (avec casque attaché)</td>
</tr>
</table>



## <a name="how-to-use-voice"></a>Comment utiliser la voix

Envisagez d’ajouter des commandes vocales à aucune expérience que vous générez. Voix est un moyen puissant et pratique contrôler le système et les applications. Étant donné que les utilisateurs parlent avec un large éventail de langages et des accents, des choix approprié de mots clés de reconnaissance vocale permet de garantir que les commandes de vos utilisateurs sont interprétés sans ambiguïté.

### <a name="best-practices"></a>Meilleures pratiques

Voici quelques pratiques qui vous aideront à la reconnaissance vocale sans heurts.
* **Utilisez les commandes concis** - dans la mesure du possible, choisissez des mots clés de deux ou plusieurs des syllabes. Celui-SYLLABE mots ont tendance à utiliser les sons des voyelles différents lors de la lecture par des personnes de différents accents. Exemple : « Lire la vidéo » est « Lire la vidéo actuellement sélectionnée » bien supérieures
* **Utiliser le vocabulaire simple** -exemple : « Afficher la note » est meilleure que « Show résumé des »
* **Assurez-vous que les commandes sont non destructifs** : Assurez-vous que toute action qui peut être effectuée par une commande de reconnaissance vocale est non destructive et peuvent facilement être annulées en cas d’une autre personne en parlant accidentellement près de l’utilisateur déclenche une commande.
* **Éviter les commandes de consonance similaire** -éviter d’inscrire plusieurs commandes vocales très similaires. Exemple : « Afficher plus » et « Show store » peuvent être consonance similaire.
* **Annuler l’inscription de votre application lorsqu’elle n'utilise pas** : quand votre application n’est pas dans un état dans lequel une commande de reconnaissance vocale est valide, envisagez d’en le désinscrivant afin que les autres commandes ne sont pas confondues pour qu’un.
* **Test avec différentes accents** -tester votre application avec des utilisateurs de différents accents.
* **Maintenir la cohérence des commandes vocales** - en cas de « Revenir en arrière » à la page précédente, maintenir ce comportement dans vos applications.
* **Évitez d’utiliser les commandes du système** -commandes vocales suivantes sont réservées pour le système. Ils ne doivent pas être utilisés par les applications.
   * « Hey Cortana »
   * « Sélectionner »

### <a name="select"></a>« Sélectionner »

Indiquant que « select » à tout moment activera tout ce qui est positionné le curseur du pointage de regard. 

>Remarque: HoloLens 2, le regards curseur doit être appelée en premier en indiquant que le mot « select ». Par exemple, « select » à nouveau à activer. Pour masquer le curseur du pointage de regard, simplement vos mains--airtap ou touch d’un objet. 

### <a name="see-it-say-it"></a>Voir, par exemple, il

Réalité mixte Windows a utilisé un modèle de voix « voir, dites » où **étiquettes sur les boutons sont identiques aux commandes vocales associé**. Car il n’est pas tout dissonance entre l’étiquette et les commandes vocales, les utilisateurs puissent mieux comprendre ce qu’il faut dire à contrôler le système. Pour cela, renforcer lors de logement sur un bouton, un **« Conseil m’attarderai pas voix »** s’affiche pour communiquer les boutons sont voix activée.


![Découvrez-le dites-le exemple 1](images/voice-seeitsayit1-640px.jpg)

![Découvrez-le dites-le exemple 2](images/voice-seeitsayit2-640px.jpg)<br>
*Exemples de « voir, dites-le »*

### <a name="voices-strengths"></a>Points forts de voix

Entrée vocale est une façon naturelle pour communiquer nos intentions. Voix est particulièrement efficace pour interface **traversées** , car il peut aider les utilisateurs couper à travers plusieurs étapes d’une interface (un utilisateur peut dire « revenir en arrière » lors de la recherche dans la page Web, au lieu de devoir configurer et cliquez sur le bouton précédent dans l’application). Ce gain de temps de petites a un puissant **effet émotionnel** sur utilisateur de la perception de l’expérience et leur permet de donner des super-pouvoirs à une petite quantité. À l’aide de la voix est également une méthode pratique d’entrée lorsque nous avons notre armes complets ou que vous sont **multitâche**. Sur les appareils où il est difficile, de taper sur un clavier **vocal dictée** peut être une alternative efficace à l’entrée. Enfin, dans certains cas, lorsque le **plage de précision** pour regards et les mouvements sont limités, voix peut être d’un utilisateur seuls approuvés de méthode d’entrée.

**Quoi à l’aide de la voix peut vous aider l’utilisateur**
* Réduit le temps - il doit en faire l’objectif final plus efficace.
* Réduit l’effort : il doit établir des tâches plus fluide et sans effort.
* Réduit la charge cognitive - il est intuitives et faciles à apprendre et à mémoriser.
* Il est socialement acceptable : il doit s’inscrivent-ils dans sociétales normes en termes de comportement.
* Il s’agit de routine - voix peut devenir aisément un comportement habituelle.

### <a name="voices-weaknesses"></a>Faiblesses de voix

Voix a également quelques faiblesses. Un contrôle précis est un d’eux. (par exemple un utilisateur peut dire « plus fort », mais ne pouvez pas indiquer combien. « Une petite » est difficile à quantifier. Déplacement ou la mise à l’échelle des choses avec voix est également difficile (voix n’offre pas la granularité de contrôle). Voix peut également être imparfaite. Parfois, un système de voix entend une commande incorrecte ou ne parvient pas à entendre une commande. Récupération à partir de ces erreurs est un véritable défi dans n’importe quelle interface. Enfin, voix peut ne pas convenir sociale dans des lieux publics. Il existe certaines choses que les utilisateurs ne peuvent pas ou ne doivent pas dire. Ces Falaises autoriser la reconnaissance vocale à utiliser pour qu’il est préférable à.

### <a name="voice-feedback-states"></a>États de commentaires de voix

Lors de la voix est appliquée correctement, l’utilisateur comprenne bien **qu’ils peuvent par exemple et obtenir des commentaires clair** le système **entendu les correctement**. L’utilisateur de ces deux signaux être inspirent la confiance à l’aide de la voix comme une entrée principale. Voici un diagramme montrant ce qui se trouve le curseur lors de l’entrée de la voix est reconnue et qui communique à l’utilisateur.

![États de commentaires de voix pour curseur](images/voicefeedbackstates.png)<br>
*États de commentaires de voix pour curseur*

## <a name="top-things-users-should-know-about-speech-in-mixed-reality"></a>Les utilisateurs de choses doivent être informés sur « vocal » dans la réalité mixte
* Par exemple **« Select »** tout en ciblant un bouton (vous pouvez utiliser ceci en tout lieu à cliquer sur un bouton).
* Vous pouvez dire le **nom d’étiquette d’un bouton de barre d’application** dans certaines applications d’entreprendre une action. Par exemple, lorsque vous examinez une application, un utilisateur peut dire la commande « Supprimer » pour supprimer l’application du monde (Cela évite les temps d’avoir de cliquer dessus avec la main).
* Vous pouvez lancer Cortana écoute en disant **« Hey Cortana ».** Vous pouvez poser des questions son (« Hey Cortana, la hauteur est la tour Eiffel »), l’inviter à ouvrir une application (« Hey Cortana, ouvrez Netflix ») ou l’inviter à faire apparaître le Menu Démarrer (« Hey Cortana, take me d’accueil ») et bien plus encore.

## <a name="common-questions-and-concerns-users-have-about-voice"></a>Les utilisateurs de questions et inquiétudes courantes ont sur voix
* Que puis-je dire ?
* Comment savoir si que le système m’avez bien entendu correctement ?
   * Le système cesse de se Mes commandes vocales incorrect.
   * Il ne réagit pas quand je lui donne une commande vocale.
* Il réagit la mauvaise façon lorsque je lui donne une commande vocale.
* Comment cibler les mon voix à une application spécifique ou d’une commande de l’application ?
* Puis-je utiliser la voix à des éléments de commande out le frame HOLOGRAPHIQUE sur HoloLens ?

## <a name="see-also"></a>Voir aussi
* [Mouvements](gestures.md)
* [Suivre de la tête et stabiliser](gaze-and-dwell.md)
