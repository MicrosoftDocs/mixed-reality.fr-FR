---
title: Lecteur de communication à distance holographique
description: Le lecteur de communication à distance holographique est une application auxiliaire qui se connecte aux applications de PC et aux jeux qui prennent en charge la communication à distance holographique. La communication à distance holographique diffuse du contenu holographique depuis un PC vers votre Microsoft HoloLens en temps réel, à l’aide d’une connexion Wi-Fi.
author: JonMLyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: b8354295f9752e73cc9b34c1769254e49808b63f
ms.sourcegitcommit: c6b59f532a9c5818d9b25c355a174a231f5fa943
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66813720"
---
# <a name="holographic-remoting-player"></a>Lecteur de communication à distance holographique

Le lecteur de communication à distance holographique est une application auxiliaire qui se connecte aux applications de PC et aux jeux qui prennent en charge la communication à distance holographique. La communication à distance holographique diffuse du contenu holographique depuis un PC vers votre Microsoft HoloLens en temps réel, à l’aide d’une connexion Wi-Fi.

Le lecteur de communication à distance holographique peut uniquement être utilisé avec des applications de PC conçues spécifiquement pour prendre en charge la communication à distance holographique.

Le lecteur de communication à distance holographique est disponible à la fois pour HoloLens et HoloLens 2.  Les applications PC qui prennent en charge la communication à distance holographique avec HoloLens doivent être mises à jour pour prendre en charge les Remtoing holographiques avec HoloLens 2.  Si vous avez des questions sur les versions prises en charge, contactez le fournisseur de votre application.

## <a name="connecting-to-the-holographic-remoting-player"></a>Connexion au lecteur de communication à distance holographique

Suivez les instructions de votre application pour vous connecter au lecteur de communication à distance holographique. Vous devrez entrer l’adresse IP de votre appareil HoloLens, que vous pouvez voir sur l’écran principal du lecteur de communication à distance, comme suit:

![Lecteur de communication à distance holographique](images/holographicremotingplayer.png)

Chaque fois que vous voyez l’écran principal, vous savez que vous ne disposez pas d’une application connectée.

Notez que la connexion de communication à distance holographique n’est **pas chiffrée**. Vous devez toujours utiliser la communication à distance holographique sur une connexion Wi-Fi sécurisée à laquelle vous faites confiance.

## <a name="quality-and-performance"></a>Qualité et performances

La qualité et les performances de votre expérience varient en fonction de trois facteurs:
* **L’expérience holographique que vous exécutez-les** applications qui restituent du contenu haute résolution ou hautement détaillé peuvent nécessiter un PC plus rapide ou une connexion sans fil plus rapide.
* Le **matériel de votre PC** : votre ordinateur doit être en mesure d’exécuter et d’encoder votre expérience holographique à 60 images par seconde. Pour une carte graphique, nous recommandons généralement une solution GeForce GTX 970 ou AMD Radeon R9 290 ou plus. Une fois encore, votre expérience particulière peut nécessiter une carte de niveau supérieur ou inférieur.
* **Votre connexion Wi-Fi** : votre expérience holographique est diffusée via Wi-Fi. Utilisez un réseau rapide avec une faible congestion pour optimiser la qualité. L’utilisation d’un PC connecté via un câble Ethernet plutôt que le Wi-Fi peut également améliorer la qualité.

## <a name="diagnostics"></a>Diagnostics

Pour mesurer la qualité de votre connexion, dites **«activer les diagnostics»** dans l’écran principal du lecteur de communication à distance holographique. Lorsque les diagnostics sont activés, l’application vous indique:
* **Fps** : nombre moyen de trames rendues que le lecteur de communication à distance reçoit et restitue par seconde. L’idéal est de 60 FPS.
* **Latence** : temps moyen nécessaire pour qu’une image passe de votre PC à la vue HoloLens. Plus la solution est performante. Cela dépend en grande partie de votre réseau Wi-Fi.

Dans l’écran principal, vous pouvez indiquer **«Désactiver les diagnostics»** pour désactiver les Diagnostics.

## <a name="pc-system-requirements"></a>Configuration système requise pour PC
* Votre ordinateur **doit** exécuter la mise à jour anniversaire Windows 10 ou une version plus récente.
* Nous vous recommandons d’utiliser une carte graphique GeForce GTX 970 ou AMD Radeon R9 290 ou supérieure.
* Nous vous recommandons de connecter votre ordinateur à votre réseau via Ethernet pour réduire le nombre de sauts sans fil.

## <a name="see-also"></a>Voir aussi
* [Termes du contrat de licence pour Holographic Remoting Player](https://docs.microsoft.com/en-us/legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
