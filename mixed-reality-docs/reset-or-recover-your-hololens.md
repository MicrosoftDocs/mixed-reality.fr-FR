---
title: Réinitialiser ou récupérer votre HoloLens
description: Instructions de base et avancées pour le redémarrage ou réinitialisation de votre HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: savoir-faire, redémarrer, réinitialiser, récupérer, une réinitialisation matérielle, réinitialisation logicielle, cycle d’alimentation, HoloLens, arrêter
ms.openlocfilehash: abf71a5f122b1c6f800bf970f51da11a34be956b
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594178"
---
# <a name="reset-or-recover-your-hololens"></a>Réinitialiser ou récupérer votre HoloLens

Si vous rencontrez des problèmes avec votre HoloLens voulez-vous essayer un redémarrage, réinitialisation ou même mise à jour flash avec la récupération de l’appareil. Ce document vous guidera à travers les étapes recommandées à la suite.

## <a name="perform-a-device-reboot"></a>Effectuer un redémarrage de l’appareil

Si votre HoloLens rencontre des problèmes ou ne répond pas, essayez d’abord le redémarrage via une des méthodes ci-dessous.

### <a name="perform-a-safe-reboot-via-cortana"></a>Effectuer un redémarrage sans échec via Cortana

Le moyen le plus sûr pour redémarrer le HoloLens est via Cortana. Il s’agit généralement une excellente premier-étape lors de la rencontre un problème de HoloLens :
1. Placé sur votre appareil
2. Assurez-vous qu’il est mis sous tension, un utilisateur est connecté, et l’appareil n’est pas en attente pour un mot de passe pour le déverrouiller.
3. Par exemple « Hey Cortana, redémarrez » ou « Hey Cortana, redémarrez. »
4. Lorsqu’elle confirme qu’elle vous demandera confirmation. Patientez une seconde pour un son à lire une fois qu’elle a terminé sa question, indiquant qu’elle est à l’écoute pour vous et dites « Oui ».
5. L’appareil sera désormais redémarrage/le redémarrage.

### <a name="perform-a-safe-reboot-via-windows-device-portal"></a>Effectuer un redémarrage sans échec via Windows Device Portal

Si la méthode ci-dessus ne fonctionne pas, vous pouvez essayer de redémarrer l’appareil via [Windows Device Portal](using-the-windows-device-portal.md). Dans le coin supérieur droit, il n’est envisageable de redémarrer/arrêter l’appareil.

### <a name="perform-a-safe-reboot-via-the-power-button"></a>Effectuer un redémarrage sans échec via le bouton d’alimentation

Si vous ne pouvez pas toujours redémarrer votre appareil, vous pouvez essayer d’émettre un redémarrage via le bouton d’alimentation :
1. Maintenez le bouton d’alimentation pendant 5 secondes
   1. Après 1 seconde, vous verrez tous les illuminant LED 5, puis lentement désactiver de droite à gauche
   2. Après 5 secondes, tous les voyants doivent être éteints, indiquant que la commande d’arrêt a été émise avec succès
   3. Notez qu’il est important d’arrêter en appuyant sur le bouton immédiatement après que tous les témoins lumineux ont désactivé
2. Patientez une minute pour l’arrêt proprement réussisse. Notez que l’arrêt peut toujours être en cours d’exécution même si les affichages sont désactivés
3. Mise sous tension l’appareil à nouveau en maintenant enfoncé le bouton d’alimentation pendant 1 seconde

### <a name="perform-an-unsafe-forced-reboot"></a>Effectuer un redémarrage forcé unsafe

Si aucune des méthodes ci-dessus sont en mesure de redémarrer correctement votre appareil, vous pouvez forcer un redémarrage. Notez que cette méthode est équivalente à l’extraction de la batterie à partir de la HoloLens et par conséquent, est une opération dangereuse, ce qui peut laisser votre appareil dans un état endommagé. 

>[!WARNING]
>Ceci est une méthode potentiellement dangereux et ne doit être utilisé dans aucune des méthodes ci-dessus fonctionne l’événement.

1. Maintenez le bouton d’alimentation pendant au moins 10 secondes
   * Il s’agit d’OK à le maintenir enfoncé pendant plus de 10 secondes
   * Il est déconseillé d’ignorer toute activité LED
2. Relâchez le bouton et attendre 2 à 3 secondes
3. Mise sous tension l’appareil à nouveau en maintenant enfoncé le bouton d’alimentation pendant 1 seconde

## <a name="reset-the-device-to-a-factory-clean-state"></a>Réinitialiser l’appareil à un état propre fabrique

Si votre HoloLens rencontre toujours des problèmes après le redémarrage, vous pouvez essayer de rétablir à un état propre fabrique. Si vous réinitialisez votre appareil, vos données personnelles, applications et paramètres seront effacées. Réinitialisation installe uniquement la dernière version installée de Windows holographique et vous devrez rétablir toutes les étapes d’initialisation (étalonner, se connecter au Wi-Fi, créer un compte d’utilisateur, télécharger des applications, etc....).
1. Lancer le **paramètres** -> application **mise à jour** -> **réinitialiser**
2. Sélectionnez le **réinitialisation du périphérique** option et la lecture de la boîte de dialogue de confirmation
3. Si vous acceptez de réinitialiser votre appareil, l’appareil redémarre et afficher un ensemble d’engrenages avec une barre de progression de rotation
4. Attendez environ 30 minutes pour que ce processus soit effectué
5. La réinitialisation se termine et l’appareil redémarre dans l’emploi de l’expérience

## <a name="perform-a-full-device-recovery"></a>Effectuer une récupération complète de l’appareil

Si, après avoir effectué les options ci-dessus, votre appareil est **toujours** figé, ne répond pas ou rencontre mise à jour logicielle des problèmes ou vous pouvez récupérer à l’aide de la de Windows Device Recovery Tool. Récupération de votre appareil est similaire à la réinitialisation en ce sens qu’il effacera tout le contenu utilisateur sur l’appareil, notamment des applications, des jeux, des photos, des comptes d’utilisateur et bien plus encore. Si possible, sauvegardez toute information que vous souhaitez conserver.

Pour restaurer entièrement votre HoloLens :
1. Déconnecter tous les téléphones et appareils de Windows à partir de votre PC
2. Installez et lancez le [Windows Device Recovery Tool](https://support.microsoft.com/help/12379/windows-10-mobile-device-recovery-tool-faq) (WDRT) sur votre PC
3. Connecter votre HoloLens à votre PC à l’aide du câble micro-USB, il est fourni avec
   * Notez que ne pas tous les câbles USB sont égaux. Même si vous utilisez un autre câble correctement, ce flux exposera où le câble peut s’avérer également de nouveaux États. Le votre HoloLens fournie avec est l’option meilleures et plus testée
4. Si l’outil détecte automatiquement votre appareil, il affiche une vignette de HoloLens. Cliquez dessus et suivez les instructions pour terminer le processus

>[!NOTE]
>WDRT peut récupérer votre appareil vers une version antérieure de Windows HOLOGRAPHIQUE ; Vous devrez peut-être installer des mises à jour après le clignotement

Si l’outil ne peut pas détecter automatiquement de votre appareil, essayez ce qui suit :
1. Redémarrez votre PC et réessayez (cela résout la plupart des problèmes)
2. Cliquez sur le **mon appareil n’a pas été détectée. bouton**, choisissez **Microsoft HoloLens**, puis suivez le reste des instructions sur l’écran
