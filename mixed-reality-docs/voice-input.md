---
title: Entrée vocale
description: L’entrée vocale est une entrée de base pour HoloLens et les casques immersifs immersifs de Windows Mixed Reality. La voix peut être utilisée pour les commandes, la dictée, Cortana et bien plus encore.
author: Hak0n
ms.author: hakons
ms.date: 10/03/2019
ms.topic: article
keywords: GGv, voix, Cortana, discours, entrée
ms.openlocfilehash: 7264b0b8882928f64860bc5a30b97683306cb19c
ms.sourcegitcommit: 781e47db2ca2f2c792c95e76ac309b44b3535555
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74105772"
---
# <a name="voice-input"></a>Entrée vocale

![Entrée vocale](images/UX/UX_Hero_VoiceCommand.jpg)

La voix est l’un des principaux types d’entrée sur HoloLens. Elle vous permet de directement commander un hologramme sans avoir à utiliser des gestes à la [main](gaze-and-commit.md#composite-gestures). L’entrée vocale peut être un moyen naturel de communiquer votre intention. La voix est particulièrement intéressante pour traverser les interfaces complexes, car elle permet aux utilisateurs de couper les menus imbriqués avec une commande.

L’entrée vocale est alimentée par le [moteur](https://msdn.microsoft.com/library/windows/apps/mt185615.aspx) qui prend en charge la reconnaissance vocale dans toutes les autres _applications universelles Windows_. Sur HoloLens, la reconnaissance vocale fonctionne toujours dans la langue d’affichage Windows configurée dans paramètres. 

<br>

## <a name="voice-and-gaze"></a>Voix et regard

Lorsque vous utilisez des commandes vocales (tête ou œil), le point de regard est généralement utilisé comme mécanisme de ciblage, que ce soit avec un curseur (« Select ») ou pour canaliser implicitement votre commande vers une application que vous examinez. Pour ce faire, il n’est même pas nécessaire de faire apparaître un curseur pointant vers le regard _(« Regardez-le, dites-le »)_ . Bien entendu, certaines commandes vocales ne nécessitent pas de cible, telles que « aller à démarrer » ou « Hey Cortana ».

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/eHMkOpNUtR8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


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
        <td>Entrée vocale</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️ (avec microphone)</td>
    </tr>
</table>

## <a name="the-select-command"></a>Commande « sélectionner »

**HoloLens (1re génération)**

Même sans ajouter spécifiquement la prise en charge vocale à votre application, vos utilisateurs peuvent activer des hologrammes simplement en disant à la commande System Voice « Select ». Cela se comporte de la même façon qu’un [TAP Air](gaze-and-commit.md#composite-gestures) sur HoloLens, en appuyant sur le bouton de sélection sur l’interactiveur [hololens](hardware-accessories.md#hololens-clicker)ou en appuyant sur le déclencheur sur un [contrôleur de mouvement Windows Mixed Reality](motion-controllers.md). Vous entendez un son et vous voyez une info-bulle avec « sélectionner » qui s’affiche comme confirmation. « SELECT » est activé par un algorithme de détection de mot-clé à faible consommation d’énergie. il est donc toujours disponible pour vous, à tout moment, avec un impact minimal sur la durée de vie de la batterie, même avec vos mains.

<br>

---

:::row:::
    :::column:::
        **HoloLens 2**<br><br>
        Pour utiliser la commande vocale « SELECT » dans HoloLens 2, vous devez d’abord afficher le curseur en regard à utiliser comme pointeur. La commande pour l’afficher est facile à mémoriser, par exemple « Select ».<br><br>
        Pour quitter le mode, il vous suffit de réutiliser vos mains, soit par air, en appuyant sur un bouton avec vos doigts, soit en utilisant le mouvement du système.<br>
        <br>
        *Image : dites « sélectionner » pour utiliser la commande vocale pour la sélection*
    :::column-end:::
        :::column:::
       ![Un utilisateur peut indiquer « sélectionner » pour utiliser la commande vocale pour une sélection.](images/kma-voice-select-00170.jpg)<br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="hey-cortana"></a>Hey Cortana

Vous pouvez également indiquer « Hey Cortana » pour afficher Cortana à tout moment. Vous n’avez pas besoin d’attendre qu’il apparaisse pour continuer à poser votre question ou de lui donner une instruction. par exemple, essayez de dire « Bonjour Cortana, qu’est-ce que la météo ? » comme une seule phrase. Pour plus d’informations sur Cortana et ce que vous pouvez faire, demandez-lui simplement ! Dites « Hey Cortana, que puis-je faire ? » et elle extrait une liste de commandes de travail et suggérées. Si vous êtes déjà dans l’application Cortana, vous pouvez également cliquer sur le **?** sur la barre latérale pour extraire le même menu.

**Commandes spécifiques à HoloLens**
* Qu’est-ce que je dis ?
* « Aller au début »-au lieu de [fleuri](system-gesture.md#bloom) pour accéder au [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu)
* « Launch <app>»
* « Déplacer <app> ici »
* « Prendre une photo »
* « Démarrer l’enregistrement »
* « Arrêter l’enregistrement »
* « Augmenter la luminosité »
* « Réduire la luminosité »
* « Augmenter le volume »
* « Réduire le volume »
* « Muet » ou « muet »
* « Arrêter l’appareil »
* « Redémarrer l’appareil »
* « Go to Sleep »
* « Quel est l’heure ? »
* « Quelle batterie ai-je laissée ? »



<br>

---

:::row:::
    :::column:::
        ## <a name="see-it-say-itbr"></a>« Regardez-le, dites-le »<br>
        HoloLens a un modèle de « voir », par exemple, le modèle d’entrée vocale, où les étiquettes sur les boutons indiquent aux utilisateurs les commandes vocales qu’ils peuvent également prononcer. Par exemple, lors de la consultation d’une fenêtre d’application dans HoloLens (1re génération), un utilisateur peut prononcer la commande « Adjust » qui s’affiche dans la barre de l’application pour ajuster la position de l’application dans le monde.<br>
        <br>
        *Image : un utilisateur peut prononcer la commande « Adjust » qui s’affiche dans la barre de l’application pour ajuster la position de l’application*
    :::column-end:::
        :::column:::
        espace de ![](images/spacer-20x582.png)<br>
        ![lors de la consultation d’une fenêtre d’application ou d’un hologramme, un utilisateur peut prononcer la commande « Adjust » qui s’affiche dans la barre de l’application pour ajuster la position de l’application dans le monde](images/microphone-600px.png)<br>
    :::column-end:::
:::row-end:::


<br>



:::row:::
    :::column:::
        Lorsque les applications suivent cette règle, les utilisateurs peuvent facilement comprendre ce qu’il faut savoir pour contrôler le système. Pour renforcer ce point, pendant que Gazing a un bouton dans HoloLens (1ère génération), vous verrez une info-bulle « de la voix » qui apparaît après une seconde si le bouton est activé pour la voix et affiche la commande pour dire à « appuyez ». Pour afficher les info-bulles vocales dans HoloLens 2, affichez le curseur vocal en disant « sélectionner » ou « que puis-je dire » (Voir l’image). <br>
        <br>
        *Image : les commandes « voir » s’affichent sous les boutons*
    :::column-end:::
        :::column:::
       ![Voyez-le, disons que les commandes s’affichent sous les boutons](images/voice-seeitsayit-600px.png)<br><br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="voice-commands-for-fast-hologram-manipulation"></a>Commandes vocales pour une manipulation d’hologramme rapide

Il existe un certain nombre de commandes vocales que vous pouvez prononcer Gazing sur un hologramme pour effectuer rapidement des tâches de manipulation. Ces commandes vocales fonctionnent sur les fenêtres d’application, ainsi que sur les objets 3D que vous avez placés dans le monde.

**Commandes de manipulation d’hologramme**
* Me faire face
* Plus grand | Enrichissement
* Grande

Sur HoloLens 2, vous pouvez également créer des interactions plus naturelles en association avec un regard en œil qui fournit implicitement des informations contextuelles sur ce à quoi vous faites référence. Par exemple, vous pouvez simplement regarder un hologramme et indiquer « placer _ce_», puis passer à l’emplacement où vous souhaitez le placer et indiquer « sur _ce_point ».
Ou bien, vous pouvez consulter un composant holographique sur une machine complexe et indiquer : « Donnez-moi plus d’informations à _ce_sujet ».



## <a name="discovering-voice-commands"></a>Détection des commandes vocales

Certaines commandes, telles que les commandes de manipulation rapide ci-dessus, peuvent être masquées. Pour en savoir plus sur les commandes que vous pouvez utiliser, pointez avec le regard sur un objet et dites « que puis-je prononcer ? ». Une liste de commandes possibles s’affiche. Vous pouvez également utiliser le curseur point-tête pour rechercher et afficher les info-bulles vocales de chaque bouton devant vous. 

Si vous souhaitez obtenir la liste complète, dites « afficher toutes les commandes » à tout moment. 


## <a name="dictation"></a>Dictée

Plutôt que de taper avec des [robinets](gaze-and-commit.md#composite-gestures), la dictée vocale peut être plus efficace pour entrer du texte dans une application. Cela peut accélérer l’entrée avec moins d’efforts pour l’utilisateur.

![la dictée vocale commence en sélectionnant le bouton microphone](images/micbuttonfordictation.png)<br>
*La dictée vocale commence en sélectionnant le bouton microphone sur le clavier.*

À chaque fois que le clavier holographique est actif, vous pouvez basculer en mode dictée au lieu de taper. Sélectionnez le microphone sur le côté de la zone d’entrée de texte pour commencer.


## <a name="adding-voice-commands-to-your-app"></a>Ajout de commandes vocales à votre application

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
   * « Aller au début »

### <a name="advantages-of-voice-input"></a>Avantages de l’entrée vocale

La voix est un moyen naturel de communiquer nos intentions. La voix est particulièrement intéressante pour les **parcours** d’interface, car elle peut aider les utilisateurs à franchir plusieurs étapes d’une interface (un utilisateur peut indiquer « revenir en arrière » lors de la consultation d’une page Web, au lieu de devoir cliquer sur le bouton précédent de l’application). Cette économie d’énergie a un **effet émotionnelle** puissant sur la perception de l’expérience de l’utilisateur et lui donne une petite quantité d’Superpower. L’utilisation de la voix est également pratique lorsque nous avons les mains occupées ou que nous effectuons **plusieurs tâches en même temps**. Sur les appareils où la saisie sur un clavier est difficile, la **dictée vocale** peut être un moyen efficace d’entrer du texte. Enfin, dans certains cas, lorsque la **plage de précision** du point de vue et du mouvement est limitée, la voix peut aider à lever l’ambiguïté de l’intention de l’utilisateur. 

**Avantages de l’utilisation de la voix**
* Gain de temps : l’objectif final est donc plus facile à atteindre.
* Efforts moindres : l’exécution des tâches est plus fluide et ne demande pas d’efforts.
* Réduction de la charge cognitive : les commandes vocales sont intuitives, et faciles à apprendre et à mémoriser.
* Acceptation sociale : leur comportement s’inscrit facilement dans les normes sociétales.
* Routine : l’utilisation de la voix peut facilement se transformer en habitude.

### <a name="challenges-for-voice-input"></a>Défis liés à l’entrée vocale

Bien que les entrées vocales soient intéressantes pour de nombreuses applications différentes, elles sont également confrontées à plusieurs défis. Le fait de comprendre les avantages et les défis liés aux entrées vocales permet aux développeurs d’applications de faire des choix plus intelligents quant à la façon et au moment d’utiliser les entrées vocales et à créer une expérience optimale pour leurs utilisateurs.

**Entrée vocale pour le contrôle d’entrée continu** Le contrôle affiné est l’un d’eux. Par exemple, un utilisateur peut souhaiter modifier son volume dans son application musical. Elle peut simplement indiquer « plus fort », mais il n’est pas clair que le système est censé créer le volume. L’utilisateur peut par exemple : « en faire un peu plus fort », mais « un peu » est difficile à quantifier. Le déplacement ou la mise à l’échelle d’hologrammes avec la voix est tout aussi difficile. 

**Fiabilité de la détection des entrées vocales** Bien que les systèmes d’entrée de voix soient plus performants et mieux, ils peuvent parfois entendre et interpréter une commande vocale de manière incorrecte.
La clé consiste à résoudre ce problème dans votre application en fournissant des commentaires à l’utilisateur lorsque le système est à l’écoute et ce que le système a compris pour créer une clarté sur les problèmes potentiels en maîtrisant correctement l’utilisateur.  

**Entrée vocale dans les espaces partagés** La voix ne peut pas être socialement acceptable dans les espaces que vous partagez avec d’autres personnes.
Voici quelques exemples :
* Il se peut que l’utilisateur ne souhaite pas déranger les autres (par exemple, dans une bibliothèque silencieuse ou un bureau partagé)
* Il se peut que les utilisateurs ne soient pas contraints de parler à eux-mêmes en public,
* Un utilisateur peut paraître inconfortant de dicter un message personnel ou confidentiel (y compris des mots de passe), tandis que d’autres sont à l’écoute

**Entrée vocale de mots uniques ou inconnus** Les problèmes d’entrée vocale se posent également lorsque les utilisateurs dictent des mots qui peuvent être inconnus du système, tels que des surnoms, certains mots d’argot ou abréviations. 

**Apprentissage des commandes vocales** Tandis que l’objectif ultime est de naturellement communiquer avec votre système, les applications s’appuient souvent sur des commandes vocales prédéfinies spécifiques.
Un défi associé à un grand nombre de commandes vocales est de savoir comment les enseigner sans surcharger l’utilisateur et comment aider l’utilisateur à les conserver. 

<br>

---

### <a name="voice-feedback-states"></a>Retours des commandes vocales

Lorsque la voix est utilisée correctement, l’utilisateur **comprend ce qu’il peut dire et reçoit la confirmation** que le système a **bien compris sa commande**. Ce sont ces deux éléments qui donnent envie à l’utilisateur de choisir la voix comme méthode d’entrée principale. Voici un diagramme qui montre ce qui se passe au niveau du curseur lorsque l’entrée vocale est reconnue, et comment celle-ci est communiquée à l’utilisateur.


:::row:::
    :::column:::
       ![1. État normal du curseur](images/voicefeedbackstates-regular.jpg)<br>
       **1. état normal du curseur**<br>
    :::column-end:::
    :::column:::
       ![2. Communique les commentaires vocaux, puis disparaît](images/voicefeedbackstates-voice.jpg)<br>
        **2. communique les commentaires vocaux, puis disparaît**<br>
    :::column-end:::
    :::column:::
       ![* 3. État normal du curseur](images/voicefeedbackstates-regular.jpg)<br>
       **3. retourne à l’état de curseur normal**<br>
    :::column-end:::
:::row-end:::

<br>

---

<br>

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

## <a name="communication"></a>Communication

Pour les applications qui souhaitent tirer parti des options de traitement d’entrée audio personnalisées fournies par HoloLens, il est important de comprendre les différentes [catégories de flux audio](https://msdn.microsoft.com/library/windows/desktop/hh404178(v=vs.85).aspx) que votre application peut consommer. Windows 10 prend en charge plusieurs catégories de flux et HoloLens en utilise trois pour permettre un traitement personnalisé afin d’optimiser la qualité audio du microphone adaptée à la parole, à la communication et à d’autres qui peuvent être utilisées pour l’audio de l’environnement ambiant. scénarios de capture (par exemple, « Camcorder »).
* La catégorie de flux de AudioCategory_Communications est personnalisée pour les scénarios de qualité des appels et de narration et fournit au client un flux audio mono 16kHz 24bit de la voix de l’utilisateur.
* La catégorie de flux de AudioCategory_Speech est personnalisée pour le moteur de reconnaissance de la parole HoloLens (Windows) et lui fournit un flux mono 16kHz 24bit de la voix de l’utilisateur. Cette catégorie peut être utilisée par les moteurs de reconnaissance vocale tiers si nécessaire.
* La catégorie de flux de AudioCategory_Other est personnalisée pour l’enregistrement audio de l’environnement ambiant et fournit au client un flux audio stéréo de 48 bits.

Tout ce traitement audio est l’accélération matérielle, ce qui signifie que les fonctionnalités se déchargent beaucoup moins d’énergie que si le même traitement a été effectué sur l’UC HoloLens. Évitez d’exécuter un autre traitement d’entrée audio sur le processeur pour maximiser la durée de vie de la batterie du système et tirer parti du traitement des entrées audio déchargées et intégrées.

## <a name="languages"></a>Langues

HoloLens 2 prend également en charge des langues supplémentaires. N’oubliez pas que les commandes vocales s’exécutent toujours dans la langue d’affichage du système même si plusieurs claviers sont installés ou si les applications essaient de créer un module de reconnaissance vocale dans une autre langue.

## <a name="troubleshooting"></a>Dépannage

Si vous rencontrez des problèmes à l’aide de « SELECT » et de « Hey Cortana », essayez de passer à un espace plus silencieux, à l’extérieur de la source de bruit, ou en parlant plus fort. À ce stade, toute la reconnaissance vocale sur HoloLens est réglée et optimisée spécifiquement pour les intervenants natifs de États-Unis anglais.

Pour la version 2017 de Windows Mixed Reality Edition, la logique de gestion des points de terminaison audio fonctionnera correctement (éternellement) après la déconnexion et la réinitialisation du PC Desktop après la première connexion HMD. Avant le premier événement de déconnexion/dans le cas de l’utilisation de WMR OOBE, l’utilisateur peut rencontrer différents problèmes de fonctionnalité audio, qu’il s’agisse d’aucun audio ou d’aucune commutation audio, en fonction de la configuration du système avant de connecter le HMD pour la première fois.

<br>

---

## <a name="voice-input-in-mrtkmixed-reality-toolkit-for-unity"></a>Entrée vocale dans MRTK (ensemble d’outils de réalité mixte) pour Unity
Avec **[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)** , vous pouvez facilement affecter une commande vocale à n’importe quel objet. Utilisez le **profil d’entrée vocale** de MRTK pour définir vos mots clés. En affectant le script **SpeechInputHandler** , vous pouvez faire en sorte qu’un objet réponde aux mots clés définis dans le profil d’entrée vocal. SpeechInputHandler fournit également une étiquette de confirmation vocale pour améliorer la confiance de l’utilisateur.

* [Commande MRTK-Voice](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Speech.html)


---

## <a name="see-also"></a>Articles associés
* [Pointer et valider](gaze-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Entrée MR 212 : voix](holograms-212.md)
* [Entrée vocale dans DirectX](voice-input-in-directx.md)
* [Entrée vocale dans Unity](voice-input-in-unity.md)
