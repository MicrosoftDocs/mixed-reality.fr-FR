---
title: Entrée vocale
description: Entrée vocale est une entrée de base pour des casques IMMERSIFS HoloLens et Windows Mixed Reality. Voix utilisable pour les commandes, la dictée, Cortana et bien plus encore.
author: Hak0n
ms.author: hakons
ms.date: 02/24/2019
ms.topic: article
keywords: ggv, voix, cortana, saisie vocale
ms.openlocfilehash: 7fb5618c13ff1ed446241f744b598cfe2484ea45
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596981"
---
# <a name="voice-input"></a>Entrée vocale

Voix est la clé trois formes de d’entrée sur HoloLens. Il vous permet à la commande directement un hologramme sans avoir à utiliser [mouvements](gestures.md). Vous simplement [les regards](gaze.md) à un hologramme et parler de votre commande. Entrée vocale peut être une façon naturelle à communiquer votre intention. Voix est particulièrement efficace pour parcourir les interfaces complexes, car il permet aux utilisateurs de couper par le biais des menus imbriqués avec une seule commande.

Entrée vocale est alimentée par le [même moteur](https://msdn.microsoft.com/library/windows/apps/mt185615.aspx) qui prend en charge la reconnaissance vocale dans toutes les autres applications Windows universelles.

<br>

>[!VIDEO https://www.youtube.com/embed/eHMkOpNUtR8]

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1er gen)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> Entrée vocale</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️ (avec microphone)</td>
</tr>
</table>

## <a name="the-select-command"></a>La commande « select »

Même sans en ajoutant la prise en charge de la voix à votre application, vos utilisateurs peuvent activer hologrammes simplement en disant « select ». Ce comportement est identique à un [appui en l’air](gestures.md#air-tap) sur HoloLens, en appuyant sur le bouton de sélection le [HoloLens clicker](hardware-accessories.md#hololens-clicker), ou en appuyant sur le déclencheur un [contrôleur de mouvement Windows Mixed Reality](motion-controllers.md). Vous allez entendre un son et affiche une info-bulle avec « select » en tant que confirmation. « Select » est activé par un algorithme de détection de mot clé de faible consommation d’énergie, elle est toujours disponible pour vous dire à tout moment avec un impact minimal batterie vie, même avec vos mains de votre côté.

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

![Par exemple « sélectionner » pour utiliser les commandes vocales pour la sélection](images/kma-voice-select-00170-800px.png)<br>
*Par exemple « sélectionner » pour utiliser les commandes vocales pour la sélection*

## <a name="hey-cortana"></a>Hey Cortana

Vous pouvez également indiquer « Hey Cortana » pour faire apparaître Cortana à tout moment. Vous n’êtes pas obligé d’attendre de lui semble continuent de lui poser votre question ou en lui donnant une instruction - par exemple, essayez de dire « Hey Cortana quelle est la météo ? » en tant qu’une phrase unique. Pour plus d’informations sur Cortana et que vous pouvez faire, simplement lui demander ! Dites « Hey Cortana, ce qui peut dire ? » et elle vais extraire la liste des commandes de travail et les suggestions. Si vous êtes déjà dans l’application Cortana vous pouvez également cliquer sur le **?** icône dans la barre latérale pour extraire ce même menu.

**Commandes spécifiques HoloLens**
* Qu’est-ce que je dis ?
* « Go home » ou « Accéder au démarrage » - au lieu de [bloom](gestures.md#bloom) pour accéder à [Menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu)
* « Lancer <app>»
* « Déplacer <app> ici »
* « Prendre une photo »
* « Démarrer l’enregistrement »
* « Arrêter l’enregistrement »
* « Augmenter la luminosité »
* « Réduire la luminosité »
* « Augmenter le volume »
* « Diminuer le volume »
* « Activer » ou « Désactiver »
* « Arrêt de l’appareil »
* « Redémarrer l’appareil »
* « Go en veille »
* « Quelle heure est-elle ? »
* « La quantité do de batterie restant ? »
* « Appeler <contact>» (nécessite Skype pour HoloLens)

## <a name="see-it-say-it"></a>« Il consultez, dites-le »

HoloLens dispose d’un modèle « voir, dites-le » pour l’entrée de la voix, où les étiquettes sur les boutons indiquent aux utilisateurs les commandes vocales peut dire qu’aussi. Par exemple, lorsque vous examinez une application 2D, un utilisateur peut dire la commande « Ajuster » qui ils voient dans la barre des applications pour ajuster la position de l’application dans le monde.

![Lorsque vous examinez une application 2D ou d’un hologramme, un utilisateur peut dire la commande « Ajuster » qui ils voient dans la barre des applications pour ajuster la position de l’application dans le monde](images/microphone-600px.png)

Lorsque des applications suivent cette règle, les utilisateurs peuvent facilement comprendre ce qu’il faut dire à contrôler le système. Pour renforcer, tout en gazing à un bouton, vous verrez une info-bulle de « balayage voix » qui s’affiche après une seconde si le bouton est activé à la voix et affiche la commande de parler pour « appuyer ».

![Voir, par exemple, il les commandes apparaissent sous les boutons](images/voice-seeitsayit-600px.png)<br>
*« Consultez, dites » commandes apparaissent sous les boutons*

## <a name="voice-commands-for-fast-hologram-manipulation"></a>Commandes vocales pour la Manipulation des hologramme rapide

Il existe également un nombre de voix commandes que vous pouvez dire lors gazing à un hologramme pour effectuer rapidement les tâches de manipulation. Ces commandes vocales fonctionnent sur les applications 2D, ainsi que des objets 3D que vous avez placés dans le monde.

**Commandes de Manipulation HOLOGRAMME**
* Me face
* Plus grande | Améliorer
* Plus petit

## <a name="dictation"></a>Dictée

Au lieu de taper avec [air robinets](gestures.md#air-tap), la dictée vocale peut être plus efficace d’entrer du texte dans une application. Cela peut accélérer considérablement l’entrée ayant moins d’efforts pour l’utilisateur.

![La dictée vocale commence en sélectionnant le bouton du microphone](images/micbuttonfordictation.png)<br>
*La dictée vocale commence en sélectionnant le bouton du microphone du clavier*

Chaque fois que le clavier holographique est actif, vous pouvez basculer vers le mode dictée au lieu de taper. Sélectionnez le microphone sur le côté de la zone de texte d’entrée pour commencer.

## <a name="communication"></a>Communication

Pour les applications qui souhaitent tirer parti de l’entrée audio personnalisée fournies par HoloLens des options de traitement, il est important de comprendre les différents [catégories de flux audio](https://msdn.microsoft.com/library/windows/desktop/hh404178(v=vs.85).aspx) votre application peut consommer. Prend en charge de Windows 10 plusieurs catégories de flux de données différents et HoloLens rend utiliser de trois d'entre eux pour permettre un traitement personnalisé optimiser la qualité audio du microphone adaptée à la reconnaissance vocale, communication et autres qui peut être utilisé pour l’audio de l’environnement ambiant scénarios de capture (autrement dit, « caméscope »).
* La catégorie de flux AudioCategory_Communications est personnalisée pour les scénarios de qualité et de narration appel et fournit au client avec un flux audio mono 16kHz 24 bits de voix de l’utilisateur
* La catégorie de flux AudioCategory_Speech est personnalisée pour le moteur de reconnaissance vocale HoloLens (Windows) et lui fournit un flux de mono 16kHz 24 bits de voix de l’utilisateur. Cette catégorie peut être utilisée par les moteurs de reconnaissance vocale 3e partie si nécessaire.
* La catégorie de flux AudioCategory_Other est personnalisée pour l’enregistrement audio environnement ambiant et fournit au client avec un flux audio stéréo 48kHz 24 bits.

Tout ce traitement audio est ce qui signifie que les fonctionnalités drainer beaucoup moins d’énergie que si le même traitement a été effectué sur le processeur de HoloLens à accélération matérielle. Évitez d’exécuter d’autres sur l’UC pour optimiser l’autonomie du système et de tirer parti de la génération de traitement d’entrée audio, déchargées traitement d’entrée audio.

## <a name="troubleshooting"></a>Résolution des problèmes

Si vous rencontrez des problèmes à l’aide de « select » et le « Hey Cortana », essayez de le déplacer vers un espace plus calme, l’activation en dehors de la source de bruit ou en parlant plus fort. À ce stade, la reconnaissance vocale tous sur HoloLens est paramétrée et optimisée spécifiquement à maîtrisant l’anglais des États-Unis.

Pour la version de la réalité mixte Windows Developer Edition 2017, la logique de gestion de point de terminaison audio fonctionne correctement (pour toujours) une fois que la journalisation en arrière et revenir aux ordinateurs de bureau après la connexion HMD initiale. Avant ce signe out/dans l’événement après la passer en revue WMR OOBE, l’utilisateur peut rencontrer divers problèmes de fonctionnalité audio allant sans contenu audio au format audio aucun changement en fonction de la façon dont le système a été configuré avant de connecter le HMD pour la première fois.

## <a name="see-also"></a>Voir aussi
* [Entrée vocale dans DirectX](voice-input-in-directx.md)
* [Entrée vocale dans Unity](voice-input-in-unity.md)
* [Entrée M. 212 : Voix](holograms-212.md)
