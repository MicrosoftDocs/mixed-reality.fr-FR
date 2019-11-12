---
title: Commander avec la voix
description: Le regard, les mouvements et la voix constituent les principaux moyens d’interaction avec HoloLens. Cet article fournit des instructions détaillées sur la conception des fonctionnalités de voix.
author: shengkait
ms.author: shentan
ms.date: 04/21/2019
ms.topic: article
keywords: Windows Mixed Reality, conception, interaction, voix
ms.openlocfilehash: 350acfbe777869f150b7c90c93124e10e155168d
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926712"
---
# <a name="voice-commanding"></a>Commander avec la voix

Lorsque vous utilisez des commandes vocales, le point de regard est généralement utilisé comme mécanisme de ciblage, qu’il s’agisse d’un pointeur (« Select ») ou d’une application (« voir », par exemple). Bien entendu, certaines commandes vocales ne nécessitent pas de cible. C’est le cas, par exemple, des commandes « aller au menu Démarrer » ou « Hey Cortana ».


## <a name="device-support"></a>Périphériques pris en charge

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
        <td>Commander avec la voix</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️ (avec casque)</td>
    </tr>
</table>



## <a name="how-to-use-voice"></a>Comment utiliser la voix

Il est recommandé d’ajouter des commandes vocales à toutes les expériences que vous créez. La voix est un moyen puissant et pratique de contrôler le système et les applications. Étant donné le nombre de dialectes et d’accents qui peuvent être utilisés, il est important de bien choisir les mots clés de reconnaissance vocale, afin de garantir que les commandes de vos utilisateurs seront correctement interprétées.

### <a name="best-practices"></a>Meilleures pratiques

Voici quelques bonnes pratiques qui faciliteront la reconnaissance vocale.
* **Utilisez des commandes concises** : dans la mesure du possible, choisissez des mots clés de deux syllabes minimum. Les mots d’une syllabe comprennent souvent des voyelles qui peuvent être prononcées différemment selon l’accent de la personne. Exemple : « lire la vidéo » est préférable à « lire la vidéo actuellement sélectionnée »
* **Utilisation d’un vocabulaire simple** -exemple : « afficher la note » est préférable à « afficher le résumé »
* **Utilisez des commandes non définitives** : assurez-vous que les actions réalisables par les commandes de reconnaissance vocale peuvent être facilement annulées, en cas de déclenchement involontaire provoqué par une personne parlant près de l’utilisateur.
* **Évitez les commandes avec des consonances similaires** : évitez d’enregistrer plusieurs commandes vocales ayant une consonance très similaire. Exemple : « afficher plus » et « afficher le magasin » peuvent être très similaires.
* **Désinscrivez votre application lorsque vous ne l’utilisez pas** : lorsque l’état de votre application rend une commande de reconnaissance vocale non valide, désinscrivez l’application pour que les autres commandes ne soient pas confondues avec celle-ci.
* **Testez les différents accents** : testez votre application avec des utilisateurs ayant différents accents.
* **Maintenez une certaine cohérence au sein des commandes vocales** : si la commande « Retour » permet de retourner à la page précédente, gardez ce comportement dans toutes vos applications.
* **Évitez d’utiliser des commandes du système** : les commandes vocales suivantes sont réservées au système. Elles ne doivent pas être utilisées par les applications.
   * « Hey Cortana »
   * « Sélectionner »

### <a name="select"></a>« Sélectionner »

La prononciation de la commande « Sélectionner » activera systématiquement l’élément qui est pointé par le curseur de pointage. 

>Remarque : dans HoloLens 2, le curseur en regard doit d’abord être appelé en disant le mot « Select ». Pour activer l’élément, vous devez prononcer une nouvelle fois la commande « Sélectionner ». Pour masquer le curseur de pointage, un mouvement suffit. Vous pouvez cliquer dans l’air ou appuyer sur un objet. 

### <a name="see-it-say-it"></a>Voir, prononcer

Windows Mixed Reality utilise un modèle de voix de type « voir, prononcer », dans lequel les **étiquettes des boutons sont identiques aux commandes vocales associées**. Puisqu’il y a cohérence entre les étiquettes et les commandes vocales, les utilisateurs comprennent plus facilement ce qu’il faut dire pour contrôler le système. Pour renforcer cela, lorsque vous stabilisez un bouton, une **« info-bulle »** s’affiche pour vous indiquer les boutons avec lesquels vous pouvez interagir à l’aide de la voix.


![Voir, prononcer - Exemple 1](images/voice-seeitsayit1-640px.jpg)

![Voir, prononcer - Exemple 2](images/voice-seeitsayit2-640px.jpg)<br>
*Exemples « voir, prononcer »*

### <a name="voices-strengths"></a>Points forts de la voix

La voix est un moyen naturel de communiquer nos intentions. Elle est particulièrement efficace pour les **traversées** d’interface, car elle permet aux utilisateurs d’éviter certaines étapes (par exemple, pour revenir à la page précédente, l’utilisateur peut dire « Retour », au lieu de retourner en haut de la page et de cliquer sur le bouton Précédent de l’application). Ce petit gain de temps a un **impact émotionnel** important sur l’utilisateur, qui a l’impression de disposer de petits super-pouvoirs. L’utilisation de la voix est également pratique lorsque nous avons les mains occupées ou que nous effectuons **plusieurs tâches en même temps**. Sur les appareils où il est difficile de taper sur un clavier, la **dictée** peut être une alternative efficace à la saisie manuelle. Enfin, dans les situations où la **plage de précision** est trop restreinte pour le regard et les mouvements, la voix peut constituer la seule méthode d’entrée fiable.

**Avantages de l’utilisation de la voix**
* Gain de temps : l’objectif final est donc plus facile à atteindre.
* Efforts moindres : l’exécution des tâches est plus fluide et ne demande pas d’efforts.
* Réduction de la charge cognitive : les commandes vocales sont intuitives, et faciles à apprendre et à mémoriser.
* Acceptation sociale : leur comportement s’inscrit facilement dans les normes sociétales.
* Routine : l’utilisation de la voix peut facilement se transformer en habitude.

### <a name="voices-weaknesses"></a>Points faibles de l’utilisation de la voix

L’utilisation de la voix présente également quelques points faibles. Le manque de précision des contrôles fait partie de ses points faibles. Par exemple, l’utilisateur peut dire « plus fort », mais il ne peut pas régler précisément le volume. En effet, la commande « un peu » est difficile à quantifier. Il est également difficile de déplacer des objets et de modifier leur taille (la voix ne permet pas de fournir des commandes précises). Les commandes vocales peuvent être imparfaites. Il arrive que le système vocal n’entende pas correctement une commande ou qu’il ne l’entende pas du tout. Il est alors difficile de récupérer après de telles erreurs, et ce, dans n’importe quelle interface. Enfin, l’utilisation de la voix peut être gênante dans les lieux publics. Il y a certaines choses que l’utilisateur ne peut pas ou ne doit pas dire. Il convient donc d’utiliser la reconnaissance vocale dans les situations adaptées.

### <a name="voice-feedback-states"></a>Retours des commandes vocales

Lorsque la voix est utilisée correctement, l’utilisateur **comprend ce qu’il peut dire et reçoit la confirmation** que le système a **bien compris sa commande**. Ce sont ces deux éléments qui donnent envie à l’utilisateur de choisir la voix comme méthode d’entrée principale. Voici un diagramme qui montre ce qui se passe au niveau du curseur lorsque l’entrée vocale est reconnue, et comment celle-ci est communiquée à l’utilisateur.

![Retours des commandes vocales au niveau du curseur](images/voicefeedbackstates.png)<br>
*Retours des commandes vocales au niveau du curseur*

## <a name="top-things-users-should-know-about-speech-in-mixed-reality"></a>Points importants concernant la reconnaissance vocale dans la réalité mixte
* Vous devez dire **« Sélectionner »** lorsque vous ciblez un bouton (vous pouvez l’utiliser n’importe où pour cliquer sur un bouton).
* Dans certaines applications, vous pouvez prononcer le **nom de l’étiquette d’un bouton de la barre d’application** pour exécuter une action. Par exemple, lorsqu’il regarde une application, l’utilisateur peut prononcer la commande « Supprimer » pour supprimer cette application (cela vous évite d’avoir à la supprimer manuellement).
* Vous pouvez activer Cortana à l’aide de la commande **« Hey Cortana »** . Vous pouvez lui poser des questions (« Hey Cortana, combien mesure la tour Eiffel ? »), lui demander d’ouvrir une application (« Hey Cortana, ouvre Netflix ») ou lui demander d’afficher le menu Démarrer (« Hey Cortana, ouvre le menu Démarrer »), et bien plus encore.

## <a name="common-questions-and-concerns-users-have-about-voice"></a>Questions et inquiétudes fréquentes concernant la reconnaissance vocale
* Que dois-je dire ?
* Comment savoir si le système m’a bien entendu ?
   * Le système ne comprend pas mes commandes vocales.
   * Il ne réagit pas quand je lui adresse une commande vocale.
* Il réagit de façon inadaptée lorsque je lui adresse une commande vocale.
* Comment choisir l’application ou la commande d’application à laquelle adresser mes commandes vocales ?
* Puis-je utiliser la voix pour contrôler les éléments holographiques sur HoloLens ?

## <a name="see-also"></a>Articles associés
* [Mouvements](gaze-and-commit.md#composite-gestures)
* [Suivre de la tête et stabiliser](gaze-and-dwell.md)
