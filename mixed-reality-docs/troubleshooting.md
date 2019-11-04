---
title: Résolution des problèmes HoloLens
description: Étapes de dépannage pour Microsoft HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: problèmes, bogue, dépannage, correction, aide, support, HoloLens
ms.openlocfilehash: 855bb0cafb0d3fba0d8d97c93d9415b51bcc2fb3
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438274"
---
# <a name="hololens-troubleshooting"></a>Résolution des problèmes HoloLens

## <a name="my-hololens-is-unresponsive-or-wont-boot"></a>Mon HoloLens ne répond pas ou ne démarre pas

Si votre HoloLens ne démarre pas :
* Si les voyants du bouton d’alimentation ne sont pas allumés, ou seulement 1 LED clignote brièvement, vous devrez peut-être charger votre HoloLens.
* Si les voyants s’allument lorsque vous appuyez sur le bouton d’alimentation, mais que vous ne voyez rien sur les écrans, maintenez le bouton d’alimentation enfoncé jusqu’à ce que les 5 témoins lumineux du bouton d’alimentation s’éteignent.

Si votre HoloLens est gelé ou ne répond pas :
* Désactivez votre HoloLens en appuyant sur le bouton d’alimentation jusqu’à ce que les 5 témoins lumineux du bouton d’alimentation s’éteignent ou pendant 10 secondes si les LED ne répondent pas. Appuyez de nouveau sur le bouton d’alimentation pour démarrer.

Si ces étapes ne fonctionnent pas :
* Vous pouvez essayer [de récupérer votre appareil](reset-or-recover-your-hololens.md).

## <a name="holograms-dont-look-good-or-are-moving-around"></a>Les hologrammes n’ont pas l’air correct ou se déplacent.

Si vos hologrammes sont instables ou incorrects, essayez l’une des solutions suivantes :
* Nettoyez votre visière d’appareils et assurez-vous que rien n’obstrue les capteurs.
* Assurez-vous qu’il y a suffisamment de lumière dans votre espace.
* Essayez de vous pencher sur votre environnement afin que HoloLens puisse les analyser plus complètement.
* Essayez d’exécuter l’application d’étalonnage. Il étalonne votre HoloLens pour qu’il fonctionne mieux pour vos yeux. Accédez à **paramètres** > **utilitaires**du > **système** . Sous étalonnage, sélectionnez **ouvrir l’étalonnage**.
* Si vous rencontrez toujours des problèmes après avoir exécuté l’application d’étalonnage, utilisez l’application de réglage du capteur pour régler vos capteurs d’appareil. Accédez à **paramètres** > **utilitaires**du > **système** . Sous réglage du capteur, sélectionnez **ouvrir le réglage du capteur**.

## <a name="hololens-doesnt-respond-to-my-gestures"></a>HoloLens ne répond pas à mes gestes.

Pour vous assurer que HoloLens peut voir vos mouvements, gardez votre main dans le cadre de mouvement, qui étend quelques mètres de part et d’autre de vous. Lorsque HoloLens peut voir votre main, le curseur passe d’un point à un anneau. En savoir plus sur l’utilisation des [mouvements](gaze-and-commit.md#composite-gestures).

Si votre environnement est trop sombre, vous risquez de ne pas voir votre main. Assurez-vous qu’il y a suffisamment de lumière.

Si votre visière présente des empreintes digitales ou des traînées, utilisez le chiffon de nettoyage microfiber fourni avec le HoloLens pour nettoyer doucement votre visière.

## <a name="hololens-doesnt-respond-to-my-voice-commands"></a>HoloLens ne répond pas à mes commandes vocales.

Si Cortana ne répond pas à vos commandes vocales, vérifiez que Cortana est activé. Dans la liste toutes les applications, sélectionnez Cortana > Menu > Paramètres > du bloc-notes pour apporter des modifications. Pour en savoir plus sur ce que vous pouvez prononcer, consultez utiliser votre voix pour contrôler HoloLens.

## <a name="i-cant-place-holograms-or-see-holograms-i-previously-placed"></a>Je ne peux pas placer d’hologrammes ou voir les hologrammes que j’ai précédemment placés.

Si HoloLens ne peut pas mapper ou charger votre espace, il entrera en mode limité et vous ne pourrez pas placer d’hologrammes ni voir les hologrammes que vous avez placés. Voici quelques opérations que vous pouvez tenter :
* Assurez-vous qu’il y a suffisamment de lumière dans votre environnement pour que HoloLens puisse voir et mapper l’espace.
* Vérifiez que vous êtes connecté à un réseau Wi-Fi. Si vous n’êtes pas connecté au Wi-Fi, HoloLens ne peut pas identifier et charger un espace connu.
* Si vous avez besoin de créer un nouvel espace, connectez-vous au Wi-Fi, puis redémarrez votre HoloLens.
* Pour voir si l’espace correct est actif ou si vous voulez charger un espace manuellement, accédez à **paramètres** > **espaces**du > **système** .
* Si l’espace correct est chargé et que vous rencontrez toujours des problèmes, l’espace est peut-être endommagé. Pour résoudre ce problème, sélectionnez l’espace, puis sélectionnez Supprimer. Une fois l’espace supprimé, HoloLens démarrera le mappage de votre environnement et créera un nouvel espace.

## <a name="my-hololens-frequently-enters-limited-mode-or-shows-a-tracking-lost-message"></a>Mon HoloLens passe fréquemment en mode limité ou affiche un message « suivi perdu ».

Si votre appareil affiche souvent un message « mode limité » ou « suivi perdu », essayez les suggestions de [mes hologrammes ne semblent pas correctes ou se déplacent](#holograms-dont-look-good-or-are-moving-around).

## <a name="my-hololens-cant-tell-what-space-im-in"></a>Mon HoloLens ne peut pas indiquer l’espace dans lequel je suis.

Si votre HoloLens ne peut pas identifier et charger automatiquement l’espace dans lequel vous vous trouvez, assurez-vous que vous êtes connecté au Wi-Fi, qu’il y a beaucoup de lumière dans la pièce et qu’il n’y a pas eu de modifications majeures dans l’environnement. Vous pouvez également charger un espace manuellement ou gérer vos espaces en accédant à **paramètres** > les **espaces**de > **système** .

## <a name="im-getting-a-low-disk-space-error"></a>J’obtiens une erreur « espace disque insuffisant ».

Vous devez libérer de l’espace de stockage en exécutant une ou plusieurs des opérations suivantes :
* Supprimez des espaces inutilisés. Accédez à **paramètres** > les **espaces**du > **système** , sélectionnez un espace dont vous n’avez plus besoin, puis sélectionnez **supprimer**.
* Retirez certains des hologrammes que vous avez placés.
* Supprimez des images et des vidéos dans l’application photos.
* Désinstallez des applications de votre HoloLens. Dans la liste toutes les applications, appuyez sur l’application que vous souhaitez désinstaller, maintenez-la enfoncée, puis sélectionnez **désinstaller**.

## <a name="my-hololens-cant-create-a-new-space"></a>Mon HoloLens ne peut pas créer un nouvel espace.

Le problème le plus probable est que vous manquez d’espace de stockage. Essayez l’une des [astuces ci-dessus](#im-getting-a-low-disk-space-error) pour libérer de l’espace disque.
