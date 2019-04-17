---
title: Résolution des problèmes de HoloLens
description: Étapes de dépannage pour Microsoft HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: problèmes, de bogues, dépannage, corriger, aider à prendre en charge, HoloLens
ms.openlocfilehash: 7b7a32a9a358ff75b2675d265445d9ef1acc1b9e
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593255"
---
# <a name="hololens-troubleshooting"></a>Résolution des problèmes de HoloLens

## <a name="my-hololens-is-unresponsive-or-wont-boot"></a>Mon HoloLens ne répond pas ou ne démarre pas

Si votre HoloLens ne démarre pas :
* Si les LED par le bouton d’alimentation ne s’allume uniquement 1, ou de LED clignote brièvement, vous devrez peut-être de facturer votre HoloLens.
* Si les témoins lumineux s’allume lorsque vous appuyez sur le bouton d’alimentation, mais vous ne voyez rien sur les affichages, maintenez le bouton d’alimentation jusqu'à ce que toutes les 5 voyants par le bouton d’alimentation de mettre hors tension.

Si votre HoloLens devient figé ou ne répond pas :
* Désactiver votre HoloLens en appuyant sur le bouton d’alimentation jusqu'à ce que toutes les 5 des LED par le bouton d’alimentation activer eux-mêmes, ou désactiver pendant 10 secondes les témoins lumineux s’il ne répond pas. Appuyez sur le bouton d’alimentation pour démarrer.

Si ces étapes ne fonctionnent pas :
* Vous pouvez essayer [la récupération de votre appareil](reset-or-recover-your-hololens.md).

## <a name="holograms-dont-look-good-or-are-moving-around"></a>Hologrammes ne soient bonnes ou sont en déplacement.

Si votre hologrammes sont instables, avec des sauts ou ne s’affichent pas correctement, essayez l’une de ces correctifs :
* Nettoyer votre visualiseur de l’appareil et assurez-vous que rien ne bloque les capteurs.
* Assurez-vous qu’il y a suffisamment de lumière dans votre salle.
* Essayez de vous épargne et en examinant votre environnement de HoloLens c’est le cas les analyser plus en détail.
* Essayez d’exécuter l’application d’étalonnage. Il étalonne votre HoloLens à mieux fonctionner pour vos yeux. Accédez à **paramètres** > **système** > **utilitaires**. Sous l’étalonnage, sélectionnez **étalonnage Open**.
* Si vous rencontrez toujours des problèmes après l’exécution de l’application d’étalonnage, utiliser l’application capteur paramétrage pour paramétrer les capteurs de votre appareil. Accédez à **paramètres** > **système** > **utilitaires**. Sous le réglage de capteur, sélectionnez **réglage de capteur Open**.

## <a name="hololens-doesnt-respond-to-my-gestures"></a>HoloLens ne répond pas à mes mouvements.

Pour vous assurer de que HoloLens peuvent voir vos mouvements, conservez la main dans le cadre de mouvement, ce qui étend les deux pieds de chaque côté de vous. Lorsque HoloLens peut voir votre main, le curseur change à partir d’un point vers un anneau. En savoir plus sur l’utilisation de [mouvements](gestures.md).

Si votre environnement est trop foncé, HoloLens ne peut pas voir votre main, assurez-vous qu’il y a suffisamment de lumière.

Si votre visualiseur comporte des empreintes digitales ou le doigt, utilisez le MICROFIBRES qui accompagne le HoloLens pour nettoyer votre visualiseur doucement de nettoyage.

## <a name="hololens-doesnt-respond-to-my-voice-commands"></a>HoloLens ne répond pas à mes commandes vocales.

Si Cortana ne répond pas à vos commandes vocales, assurez-vous que Cortana est activé. Dans la liste de toutes les applications, sélectionnez Cortana > Menu > bloc-notes > paramètres pour apporter des modifications. Pour en savoir plus sur ce que vous dites, consultez utiliser votre voix pour contrôler HoloLens.

## <a name="i-cant-place-holograms-or-see-holograms-i-previously-placed"></a>Impossible de placer hologrammes ou consultez hologrammes que précédemment, j’ai placé.

Si HoloLens ne peut pas mapper ou chargez votre espace, il passe en mode limité et vous ne pourrez pas placer hologrammes ou consultez hologrammes que vous avez placé. Voici quelques opérations que vous pouvez tenter :
* Assurez-vous qu’il y a suffisamment de lumière dans votre environnement pour HoloLens peut afficher et de mapper l’espace.
* Assurez-vous que vous êtes connecté à un réseau Wi-Fi. Si vous n’êtes pas connecté au réseau Wi-Fi, HoloLens ne peut pas identifier et charger un espace connu.
* Si vous avez besoin créer un nouvel espace, se connecter au réseau Wi-Fi, puis redémarrez votre HoloLens.
* Pour voir si l’espace approprié est active, ou pour charger manuellement un espace, accédez à **paramètres** > **système** > **espaces**.
* Si l’espace approprié est chargé et que vous rencontrez toujours des problèmes, l’espace est peut-être endommagé. Pour résoudre ce problème, sélectionnez l’espace, puis sélectionnez Supprimer. Une fois que l’espace est supprimé, HoloLens démarre le mappage de votre environnement et créer un espace.

## <a name="my-hololens-frequently-enters-limited-mode-or-shows-a-tracking-lost-message"></a>Mon HoloLens fréquemment passe en mode limité ou affiche un message « Suivi perdues ».

Si votre appareil n’affiche souvent un « mode limité » ou le message « suivi perdu », essayez les suggestions de [mes hologrammes ne soient bonnes ou déplacez autour de](#holograms-dont-look-good-or-are-moving-around).

## <a name="my-hololens-cant-tell-what-space-im-in"></a>Mon HoloLens ne peut pas déterminer l’espace dont je suis dans.

Si votre HoloLens ne peut pas identifier et charger l’espace que vous êtes dans automatiquement, vérifiez que vous êtes connecté au réseau Wi-Fi, il y a suffisamment de lumière dans la salle, et il n’ont pas été aucune modification importante pour son environnement. Vous pouvez également charger un espace manuellement ou gérer vos espaces en accédant à **paramètres** > **système** > **espaces**.

## <a name="im-getting-a-low-disk-space-error"></a>J’obtiens une erreur « espace disque faible ».

Vous devez libérer de l’espace de stockage en effectuant l’une des opérations suivantes :
* Supprimer des espaces non utilisés. Accédez à **paramètres** > **système** > **espaces**, sélectionnez un espace, vous n’avez plus besoin, puis sélectionnez **supprimer**.
* Supprimer une partie des hologrammes que vous avez placé.
* Supprimer des images et vidéos dans l’application de Photos.
* Désinstaller des applications à partir de votre HoloLens. Dans la liste de toutes les applications, cliquez et maintenez l’application que vous souhaitez désinstaller, puis sélectionnez **désinstallation**.

## <a name="my-hololens-cant-create-a-new-space"></a>Impossible de créer un nouvel espace de mon HoloLens.

Le problème le plus probable est que vous exécutez faible sur l’espace de stockage. Essayez l’une de la [conseils ci-dessus](#im-getting-a-low-disk-space-error) pour libérer l’espace disque.
