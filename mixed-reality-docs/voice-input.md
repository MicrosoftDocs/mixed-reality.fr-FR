---
title: Entrée vocale
description: L’entrée vocale est une entrée de base pour HoloLens et les casques immersifs immersifs de Windows Mixed Reality. La voix peut être utilisée pour les commandes, la dictée, Cortana et bien plus encore.
author: Hak0n
ms.author: hakons
ms.date: 02/24/2019
ms.topic: article
keywords: GGv, voix, Cortana, discours, entrée
ms.openlocfilehash: e21310b940e4a4c3019f61edea695b452e74ab62
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829950"
---
# <a name="voice-input"></a>Entrée vocale

La voix est l’une des trois formes clés d’entrée sur HoloLens. Elle vous permet de directement commander un hologramme sans avoir à utiliser des [mouvements](gestures.md). Il vous [suffit de](gaze.md) pointer sur un hologramme et de parler de votre commande. L’entrée vocale peut être un moyen naturel de communiquer votre intention. La voix est particulièrement intéressante pour traverser des interfaces complexes, car elle permet aux utilisateurs de couper les menus imbriqués à l’aide d’une seule commande.

L’entrée vocale est alimentée par le [moteur](https://msdn.microsoft.com/library/windows/apps/mt185615.aspx) qui prend en charge la reconnaissance vocale dans toutes les autres applications universelles Windows.

<br>

>[!VIDEO https://www.youtube.com/embed/eHMkOpNUtR8]

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
        <td>Entrée vocale</td>
        <td>✔️</td>
        <td>✔️</td>
        <td>✔️ (avec microphone)</td>
    </tr>
</table>

## <a name="the-select-command"></a>Commande «sélectionner»

Même sans ajouter spécifiquement la prise en charge vocale à votre application, vos utilisateurs peuvent activer des hologrammes simplement en disant «sélectionner». Cela se comporte de la même façon qu’un [TAP Air](gestures.md#air-tap) sur HoloLens, en appuyant sur le bouton de sélection sur l’interactiveur [hololens](hardware-accessories.md#hololens-clicker)ou en appuyant sur le déclencheur sur un [contrôleur de mouvement Windows Mixed Reality](motion-controllers.md). Vous entendez un son et vous voyez une info-bulle avec «sélectionner» qui s’affiche comme confirmation. «SELECT» est activé par un algorithme de détection de mot-clé à faible consommation d’énergie. il est donc toujours disponible pour vous, à tout moment, avec un impact minimal sur la durée de vie de la batterie, même avec vos mains.

> [!NOTE]
> Plus d’instructions spécifiques à HoloLens 2 bientôt [disponible](index.md#news-and-notes).

![Dites «sélectionner» pour utiliser la commande vocale pour la sélection](images/kma-voice-select-00170-800px.png)<br>
*Dites «sélectionner» pour utiliser la commande vocale pour la sélection*

## <a name="hey-cortana"></a>Hey Cortana

Vous pouvez également indiquer «Hey Cortana» pour afficher Cortana à tout moment. Vous n’avez pas besoin d’attendre qu’il apparaisse pour continuer à poser votre question ou de lui donner une instruction. par exemple, essayez de dire «Hé Cortana qu’est-ce que la météo?» comme une seule phrase. Pour plus d’informations sur Cortana et ce que vous pouvez faire, demandez-lui simplement! Dites-le «Hé Cortana que puis-je prononcer?» et elle extrait une liste de commandes de travail et suggérées. Si vous êtes déjà dans l’application Cortana, vous pouvez également cliquer sur le **?** sur la barre latérale pour extraire le même menu.

**Commandes spécifiques à HoloLens**
* Qu’est-ce que je dis ?
* «Go Start» ou «Go to Start»-au lieu de [fleuri](gestures.md#bloom) pour accéder au [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu)
* «Lancer <app>»
* «Déplacer <app> ici»
* «Prendre une photo»
* «Démarrer l’enregistrement»
* «Arrêter l’enregistrement»
* «Augmenter la luminosité»
* «Réduire la luminosité»
* «Augmenter le volume»
* «Réduire le volume»
* «Muet» ou «muet»
* «Arrêter l’appareil»
* «Redémarrer l’appareil»
* «Go to Sleep»
* «Quel est l’heure?»
* «Quelle batterie ai-je laissée?»
* «Appeler <contact>» (nécessite Skype pour HoloLens)

## <a name="see-it-say-it"></a>«Regardez-le, dites-le»

HoloLens a un modèle de «voir», par exemple, le modèle d’entrée vocale, où les étiquettes sur les boutons indiquent aux utilisateurs les commandes vocales qu’ils peuvent également prononcer. Par exemple, lors de la consultation d’une application 2D, un utilisateur peut prononcer la commande «Adjust» qui s’affiche dans la barre de l’application pour ajuster la position de l’application dans le monde.

![Lors de la consultation d’une application 2D ou d’un hologramme, un utilisateur peut prononcer la commande «Adjust» qui s’affiche dans la barre de l’application pour ajuster la position de l’application dans le monde.](images/microphone-600px.png)

Lorsque les applications suivent cette règle, les utilisateurs peuvent facilement comprendre ce qu’il faut savoir pour contrôler le système. Pour renforcer cela, alors que Gazing à un bouton, vous verrez une info-bulle «de la voix» qui apparaît après une seconde si le bouton est activé pour la voix et affiche la commande pour dire à «appuyer» dessus.

![Voyez-le, disons que les commandes s’affichent sous les boutons](images/voice-seeitsayit-600px.png)<br>
*«Voir les commandes, dites» s’affichent sous les boutons*

## <a name="voice-commands-for-fast-hologram-manipulation"></a>Commandes vocales pour une manipulation d’hologramme rapide

Il existe également un certain nombre de commandes vocales que vous pouvez prononcer Gazing sur un hologramme pour effectuer rapidement des tâches de manipulation. Ces commandes vocales fonctionnent sur les applications 2D, ainsi que sur les objets 3D que vous avez placés dans le monde.

**Commandes de manipulation d’hologramme**
* Me faire face
* Plus grand | Enrichissement
* Grande

## <a name="dictation"></a>Dictée

Plutôt que de taper avec des [pressions en l’air](gestures.md#air-tap), la dictée vocale peut être plus efficace pour entrer du texte dans une application. Cela peut accélérer l’entrée avec moins d’efforts pour l’utilisateur.

![La dictée vocale commence en sélectionnant le bouton microphone](images/micbuttonfordictation.png)<br>
*La dictée vocale commence en sélectionnant le bouton microphone sur le clavier.*

À chaque fois que le clavier holographique est actif, vous pouvez basculer en mode dictée au lieu de taper. Sélectionnez le microphone sur le côté de la zone d’entrée de texte pour commencer.

## <a name="communication"></a>Communication

Pour les applications qui souhaitent tirer parti des options de traitement d’entrée audio personnalisées fournies par HoloLens, il est important de comprendre les différentes [catégories de flux audio](https://msdn.microsoft.com/library/windows/desktop/hh404178(v=vs.85).aspx) que votre application peut consommer. Windows 10 prend en charge plusieurs catégories de flux et HoloLens en utilise trois pour permettre un traitement personnalisé afin d’optimiser la qualité audio du microphone adaptée à la parole, à la communication et à d’autres qui peuvent être utilisées pour l’audio de l’environnement ambiant. scénarios de capture (par exemple, «Camcorder»).
* La catégorie de flux AudioCategory_Communications est personnalisée pour les scénarios de qualité des appels et de narration et fournit au client un flux audio mono 16kHz 24bit de la voix de l’utilisateur.
* La catégorie de flux AudioCategory_Speech est personnalisée pour le moteur de reconnaissance de la parole HoloLens (Windows) et lui fournit un flux mono 16kHz 24bit de la voix de l’utilisateur. Cette catégorie peut être utilisée par les moteurs de reconnaissance vocale tiers si nécessaire.
* La catégorie de flux AudioCategory_Other est personnalisée pour l’enregistrement audio de l’environnement ambiant et fournit au client un flux audio stéréo de 48 bits.

Tout ce traitement audio est l’accélération matérielle, ce qui signifie que les fonctionnalités se déchargent beaucoup moins d’énergie que si le même traitement a été effectué sur l’UC HoloLens. Évitez d’exécuter un autre traitement d’entrée audio sur le processeur pour maximiser la durée de vie de la batterie du système et tirer parti du traitement des entrées audio déchargées et intégrées.

## <a name="troubleshooting"></a>Résolution des problèmes

Si vous rencontrez des problèmes à l’aide de «SELECT» et de «Hey Cortana», essayez de passer à un espace plus silencieux, à l’extérieur de la source de bruit, ou en parlant plus fort. À ce stade, toute la reconnaissance vocale sur HoloLens est réglée et optimisée spécifiquement pour les intervenants natifs de États-Unis anglais.

Pour la version 2017 de Windows Mixed Reality Edition, la logique de gestion des points de terminaison audio fonctionnera correctement (éternellement) après la déconnexion et la réinitialisation du PC Desktop après la première connexion HMD. Avant le premier événement de déconnexion/dans le cas de l’utilisation de WMR OOBE, l’utilisateur peut rencontrer différents problèmes de fonctionnalité audio, qu’il s’agisse d’aucun audio ou d’aucune commutation audio, en fonction de la configuration du système avant de connecter le HMD pour la première fois.

## <a name="see-also"></a>Voir aussi
* [Entrée vocale dans DirectX](voice-input-in-directx.md)
* [Entrée vocale dans Unity](voice-input-in-unity.md)
* [Réalité mixte - Entrées - Cours 212 : Voix](holograms-212.md)
