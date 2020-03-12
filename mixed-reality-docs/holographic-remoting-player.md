---
title: Lecteur de communication à distance holographique
description: Le lecteur de communication à distance holographique est une application auxiliaire qui se connecte aux applications de PC et aux jeux qui prennent en charge la communication à distance holographique. La communication à distance holographique diffuse du contenu holographique depuis un PC vers votre Microsoft HoloLens en temps réel, à l’aide d’une connexion Wi-Fi.
author: FlorianBagarMicrosoft
ms.author: flbagar
ms.date: 03/11/2020
ms.topic: article
keywords: HoloLens, communication à distance, communication à distance holographique
ms.openlocfilehash: 88a9aa0bb058776a32016e51fc22bcb73f08ab85
ms.sourcegitcommit: 0a1af2224c9cbb34591b6cb01159b60b37dfff0c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/11/2020
ms.locfileid: "79092374"
---
# <a name="holographic-remoting-player"></a>Lecteur de communication à distance holographique

>[!IMPORTANT]
>La communication à distance holographique pour HoloLens 2 est une modification majeure de la version. Les [applications distantes pour **hololens (1re génération)** ](add-holographic-remoting.md) doivent utiliser le package NuGet version **1. x. x** et les [applications distantes pour **hololens 2** ](holographic-remoting-create-host.md) doivent utiliser **2. x**. x. Cela implique que les applications distantes écrites pour HoloLens 2 ne sont pas compatibles avec HoloLens (1ère génération) et vice versa.

Le [lecteur de communication à distance holographique](https://www.microsoft.com/p/holographic-remoting-player/9nblggh4sv40) est une application auxiliaire qui se connecte aux applications de PC et aux jeux qui prennent en charge la communication à distance holographique. La communication à distance holographique diffuse du contenu holographique depuis un PC vers votre Microsoft HoloLens en temps réel, à l’aide d’une connexion Wi-Fi.

Le lecteur de communication à distance holographique peut uniquement être utilisé avec des applications de PC conçues spécifiquement pour prendre en charge la communication à distance holographique.

Le lecteur de communication à distance holographique est disponible à la fois pour HoloLens (1re génération) et HoloLens 2.  Les applications PC qui prennent en charge la communication à distance holographique avec HoloLens doivent être mises à jour pour prendre en charge la communication à distance holographique avec HoloLens 2. Si vous avez des questions sur les versions prises en charge, contactez le fournisseur de votre application.

## <a name="connecting-to-the-holographic-remoting-player"></a>Connexion au lecteur de communication à distance holographique

Suivez les instructions de votre application pour vous connecter au lecteur de communication à distance holographique. Vous devrez entrer l’adresse IP de votre appareil HoloLens, que vous pouvez voir sur l’écran principal du lecteur de communication à distance, comme suit :

![Lecteur de communication à distance holographique](images/holographicremotingplayer.png)

Chaque fois que vous voyez l’écran principal, vous savez que vous ne disposez pas d’une application connectée.

Notez que la connexion de communication à distance holographique n’est **pas chiffrée**. Vous devez toujours utiliser la communication à distance holographique sur une connexion Wi-Fi sécurisée à laquelle vous faites confiance.

## <a name="quality-and-performance"></a>Qualité et performances

La qualité et les performances de votre expérience varient en fonction de trois facteurs :
* **L’expérience holographique que vous exécutez-les** applications qui restituent du contenu haute résolution ou hautement détaillé peuvent nécessiter un PC plus rapide ou une connexion sans fil plus rapide.
* Le **matériel de votre PC** : votre ordinateur doit être en mesure d’exécuter et d’encoder votre expérience holographique à 60 images par seconde. Pour une carte graphique, nous recommandons généralement une solution GeForce GTX 970 ou AMD Radeon R9 290 ou plus. Une fois encore, votre expérience particulière peut nécessiter une carte de niveau supérieur ou inférieur.
* **Votre connexion Wi-Fi** : votre expérience holographique est diffusée via Wi-Fi. Utilisez un réseau rapide avec une faible congestion pour optimiser la qualité. L’utilisation d’un PC connecté via un câble Ethernet plutôt que le Wi-Fi peut également améliorer la qualité.

## <a name="diagnostics"></a>Diagnostics

Pour mesurer la qualité de votre connexion, dites **« activer les diagnostics »** dans l’écran principal du lecteur de communication à distance holographique. Lorsque les diagnostics sont activés, sur **HoloLens (1re génération)** , l’application vous indique :

* **Fps** : nombre moyen de trames rendues que le lecteur de communication à distance reçoit et restitue par seconde. L’idéal est de 60 FPS.
* **Latence** : temps moyen nécessaire pour qu’une image passe de votre PC à la vue HoloLens. Plus la solution est performante. Cela dépend en grande partie de votre réseau Wi-Fi.

Sur **HoloLens 2** , l’application vous indiquera :

![Diagnostics de lecteur de communication à distance holographique](images/holographicremotingplayer-diag.png)

* **Render** : nombre d’images rendu par le joueur de communication à distance au cours de la dernière seconde. Notez que cela ne dépend pas du nombre de trames qui sont arrivés via le réseau (voir **images vidéo**). En outre, l’affichage de l’heure Delta de rendu moyenne/maximale en millisecondes au cours de la dernière seconde entre les images rendues est affiché.

* **Trames vidéo** : le premier nombre affiché est ignoré, le second est une trame vidéo réutilisée, et la troisième les images vidéo. Tous les nombres représentent le nombre au cours de la dernière seconde.
    * ```Received frames``` est le nombre de trames vidéo arrivant au cours de la dernière seconde. Dans des conditions normales, cette valeur doit être 60, mais si ce n’est pas le cas, l’un des cadres est abandonné en raison de problèmes réseau ou la partie distante/distante ne produit pas de frames avec le taux attendu.
    * ```Reused frames``` est le nombre de trames vidéo utilisées plusieurs fois au cours de la dernière seconde. Par exemple, si des images vidéo arrivent en retard, la boucle de rendu du lecteur affiche toujours un frame, mais doit *réutiliser* le frame vidéo qu’il a déjà utilisé pour le frame précédent.
    * ```Skipped frames``` est le nombre de trames vidéo qui n’ont pas été utilisées par la boucle de rendu du lecteur. Par exemple, l’instabilité du réseau peut avoir pour effet que les trames vidéo qui arrivent ne sont plus distribuées uniformément. Par exemple, si certains sont en retard et que d’autres arrivent dans le temps avec le résultat, ils n’ont plus de Delta de 16,66 millisecondes lorsqu’ils s’exécutent sur 60 Hz. Cela peut se produire si plusieurs frames arrivent entre deux graduations de la boucle de rendu du joueur. Dans ce cas, le lecteur *ignore* un ou plusieurs frames, car il est supposé afficher toujours la dernière image vidéo reçue.

    >[!NOTE]
    >En cas d’instabilité du réseau, les trames ignorées et réutilisées sont généralement à la même. En revanche, si vous voyez uniquement les frames ignorés, cela indique que le lecteur n’atteint pas sa fréquence d’images cible. Dans ce cas, vous devez garder un œil sur l’heure de Delta de rendu maximale lors du diagnostic des problèmes.

* **Images vidéo Delta** : Delta minimum/maximum entre les trames vidéo reçues au cours de la dernière seconde. Ce nombre est généralement mis en corrélation avec les frames ignorés/réutilisés en cas de problèmes dus à l’instabilité du réseau.
* **Latence** : fréquence moyenne en millisecondes au cours de la dernière seconde. Dans ce contexte, le fait d’envoyer des données de pose/capteur de l’HoloLens au côté distant/distant jusqu’à l’affichage de la trame vidéo pour les données de pose/télémétrie sur l’affichage HoloLens.
* **Images vidéo ignorées** -nombre de trames vidéo rejetées au cours de la dernière seconde et depuis qu’une connexion a été établie. La cause principale des trames vidéo ignorées est lorsqu’une image vidéo n’arrive pas dans l’ordre et, pour cette raison, doit être ignorée, car il existe déjà une version plus récente. Cela est similaire aux *Trames ignorées* , mais la cause se trouve à un niveau inférieur dans la pile de communication à distance. Les trames vidéo ignorées ne sont attendues que dans des conditions de réseau médiocres.



Dans l’écran principal, vous pouvez indiquer **« Désactiver les diagnostics »** pour désactiver les Diagnostics.

## <a name="pc-system-requirements"></a>Configuration système requise pour PC
* Votre ordinateur **doit** exécuter la mise à jour anniversaire Windows 10 ou une version plus récente.
* Nous vous recommandons d’utiliser une carte graphique GeForce GTX 970 ou AMD Radeon R9 290 ou supérieure.
* Nous vous recommandons de connecter votre ordinateur à votre réseau via Ethernet pour réduire le nombre de sauts sans fil.

## <a name="see-also"></a>Voir aussi
* [HoloLens (1ère génération) : ajouter une communication à distance holographique](add-holographic-remoting.md)
* [HoloLens 2 : écriture d’une application distante holographique Remoting](holographic-remoting-create-host.md)
* [Termes du contrat de licence de la communication à distance holographique](https://docs.microsoft.com//legal/mixed-reality/microsoft-holographic-remoting-software-license-terms)
* [Déclaration de confidentialité Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
