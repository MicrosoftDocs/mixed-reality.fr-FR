---
title: Réinitialiser ou récupérer votre HoloLens
description: Instructions de base et avancées pour le redémarrage ou la réinitialisation de votre HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: procédure, redémarrage, réinitialisation, récupération, réinitialisation matérielle, réinitialisation à chaud, cycle d’alimentation, HoloLens, arrêt
ms.openlocfilehash: abf71a5f122b1c6f800bf970f51da11a34be956b
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524032"
---
# <a name="reset-or-recover-your-hololens"></a>Réinitialiser ou récupérer votre HoloLens

Si vous rencontrez des problèmes avec votre HoloLens, vous souhaiterez peut-être essayer d’effectuer un redémarrage, une réinitialisation ou même un nouveau flash avec la récupération de l’appareil. Ce document vous guide tout au long des étapes recommandées successivement.

## <a name="perform-a-device-reboot"></a>Effectuer un redémarrage de l’appareil

Si votre HoloLens rencontre des problèmes ou ne répond pas, essayez d’abord de le redémarrer à l’aide de l’une des méthodes ci-dessous.

### <a name="perform-a-safe-reboot-via-cortana"></a>Effectuer un redémarrage en toute sécurité via Cortana

La méthode la plus sûre pour redémarrer le HoloLens est via Cortana. Il s’agit généralement d’une première étape intéressante pour rencontrer un problème avec HoloLens:
1. Placer sur votre appareil
2. Assurez-vous qu’il est sous tension, qu’un utilisateur est connecté et que l’appareil n’attend pas un mot de passe pour le déverrouiller.
3. Dites «Hey Cortana, restart» ou «Hey Cortana, restart».
4. Lorsqu’elle en accuse réception, elle vous demande de confirmer l’opération. Attendez une seconde pour qu’un son s’exécute une fois qu’elle a terminé sa question, indiquant qu’elle est à l’écoute, puis dites «oui».
5. L’appareil va maintenant redémarrer/redémarrer.

### <a name="perform-a-safe-reboot-via-windows-device-portal"></a>Effectuer un redémarrage en toute sécurité via le portail des appareils Windows

Si la version ci-dessus ne fonctionne pas, vous pouvez essayer de redémarrer l’appareil via le [portail d’appareils Windows](using-the-windows-device-portal.md). Dans l’angle supérieur droit, il existe une option pour redémarrer/arrêter l’appareil.

### <a name="perform-a-safe-reboot-via-the-power-button"></a>Effectuer un redémarrage en toute sécurité à l’aide du bouton d’alimentation

Si vous ne pouvez toujours pas redémarrer votre appareil, vous pouvez essayer d’émettre un redémarrage à l’aide du bouton d’alimentation:
1. Appuyez sur le bouton d’alimentation et maintenez-le enfoncé pendant 5 secondes
   1. Après 1 seconde, les 5 voyants s’allument, puis s’éteignent lentement de droite à gauche
   2. Après 5 secondes, tous les LED sont désactivés, ce qui indique que la commande d’arrêt a été correctement émise
   3. Notez qu’il est important d’arrêter d’appuyer sur le bouton immédiatement après que tous les LED ont été éteints.
2. Patientez 1 minute pour que l’arrêt aboutisse correctement. Notez que l’arrêt peut encore être en cours même si les affichages sont désactivés.
3. Mettez à nouveau sous tension l’appareil en appuyant sur le bouton d’alimentation et en le maintenant enfoncé pendant 1 seconde

### <a name="perform-an-unsafe-forced-reboot"></a>Effectuer un redémarrage forcé non sécurisé

Si aucune des méthodes ci-dessus ne peut redémarrer correctement votre appareil, vous pouvez forcer un redémarrage. Notez que cette méthode est équivalente à la traction de la batterie du HoloLens et, par conséquent, est une opération dangereuse qui peut rendre votre appareil dans un état endommagé. 

>[!WARNING]
>Il s’agit d’une méthode potentiellement dangereuse qui ne doit être utilisée que dans le cas où aucune des méthodes ci-dessus ne fonctionne.

1. Appuyez sur le bouton d’alimentation et maintenez-le enfoncé pendant au moins 10 secondes
   * Il est possible de conserver le bouton pendant plus de 10 secondes
   * Il est possible d’ignorer toute activité LED
2. Relâchez le bouton et attendez 2-3 secondes
3. Mettez à nouveau sous tension l’appareil en appuyant sur le bouton d’alimentation et en le maintenant enfoncé pendant 1 seconde

## <a name="reset-the-device-to-a-factory-clean-state"></a>Réinitialiser l’appareil à un état d’usine propre

Si votre HoloLens rencontre toujours des problèmes après avoir redémarré, vous pouvez essayer de le réaffecter à un état d’usine propre. Si vous réinitialisez votre appareil, toutes vos données, applications et paramètres personnels seront effacés. La réinitialisation installera uniquement la dernière version installée de Windows holographique et vous devrez répéter toutes les étapes d’initialisation (étalonner, se connecter à WiFi, créer un compte d’utilisateur, télécharger des applications, etc.).
1. Lancer l’application **paramètres** - **mettre à jour** -> la réinitialisation >
2. Sélectionnez l’option **Réinitialiser l’appareil** et lisez la boîte de dialogue de confirmation
3. Si vous acceptez de réinitialiser votre appareil, l’appareil redémarre et affiche un ensemble de rapports tournant avec une barre de progression
4. Patientez environ 30 minutes avant la fin de ce processus
5. La réinitialisation sera terminée et l’appareil redémarrera dans l’environnement prêt à l’emploi.

## <a name="perform-a-full-device-recovery"></a>Effectuer une récupération complète de l’appareil

Si, après avoir effectué les options ci-dessus, votre appareil est **toujours** gelé, ne répond pas ou rencontre des problèmes de mise à jour ou de logiciel, vous pouvez le récupérer à l’aide de l’outil de récupération des appareils Windows. La récupération de votre appareil est similaire à sa réinitialisation dans le sens où il efface tout le contenu de l’utilisateur sur l’appareil, y compris les applications, les jeux, les photos, les comptes d’utilisateur, et bien plus encore. Si possible, sauvegardez toutes les informations que vous souhaitez conserver.

Pour récupérer entièrement votre HoloLens:
1. Déconnecter tous les téléphones et appareils Windows de votre PC
2. Installer et lancer [Windows Device Recovery Tool](https://support.microsoft.com/help/12379/windows-10-mobile-device-recovery-tool-faq) (WDRT) sur votre PC
3. Connectez votre HoloLens à votre PC à l’aide du câble micro-USB avec lequel il a été fourni.
   * Notez que tous les câbles USB ne sont pas égaux. Même si vous avez utilisé un autre câble avec succès, ce circuit expose de nouveaux États dans lesquels le câble peut ne pas fonctionner également. L’option la mieux adaptée et la plus testée est celle qui a été fournie par votre HoloLens.
4. Si l’outil détecte automatiquement votre appareil, il affiche une vignette HoloLens. Cliquez dessus et suivez les instructions pour terminer le processus.

>[!NOTE]
>WDRT peut récupérer votre appareil sur une version antérieure de Windows holographique; vous devrez peut-être installer les mises à jour après le clignotement

Si l’outil ne parvient pas à détecter votre appareil automatiquement, procédez comme suit:
1. Redémarrez votre ordinateur et réessayez (cela résout la plupart des problèmes)
2. Cliquez sur le **bouton mon appareil n’a pas été détecté**, choisissez **Microsoft HoloLens**et suivez le reste des instructions à l’écran.
