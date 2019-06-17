---
title: Problèmes connus de HoloLens
description: Il s’agit de la liste des problèmes connus susceptibles d’affecter les développeurs HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 04/1/2019
ms.topic: article
keywords: résoudre les problèmes, problème connu, aide
ms.openlocfilehash: 2423c7292e453d97461c299e8bddfa063a29d3cd
ms.sourcegitcommit: 2f600e5ad00cd447b180b0f89192b4b9d86bbc7e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148697"
---
# <a name="hololens-known-issues"></a>Problèmes connus de HoloLens

Il s’agit de la liste actuelle des problèmes connus pour les développeurs ayant un impact sur HoloLens. Commencez par vérifier ici si vous constatez un comportement étrange. Cette liste restent mis à jour comme nouveau problème détecté ou signalé ou que les problèmes sont traités dans les futures mises à jour de logiciel HoloLens.

## <a name="unable-to-connect-and-deploy-to-hololens-through-visual-studio"></a>Impossible de se connecter et à déployer sur HoloLens via Visual Studio

>[!NOTE]
>Dernière mise à jour : 6/14 à 18 h 00 - émettre incriminés.

Les équipes HoloLens et Visual Studio sont sur un problème qui peut empêcher les utilisateurs à partir de la déployer sur un appareil HoloLens via Visual Studio.
 
Pendant la phase de déploiement, les utilisateurs signaler le message d’erreur suivant, malgré les appareils HoloLens et développeur machine ayant *mode développeur* activé :

*DEP0100 : Vérifiez que cet appareil cible a le mode développeur est activé. Impossible d’obtenir une licence de développeur sur <device IP> en raison de l’erreur 80004005.*
 
**Solution** : 
 
Les utilisateurs signaler que la réinitialisation de l’appareil résout le problème, mais nous ne pouvons pas garantir que cela ne fonctionne pas dans tous les cas. Vous trouverez des instructions pour réinitialiser votre appareil [ici](https://support.microsoft.com/en-us/help/13452/hololens-restart-reset-or-recover-hololens).
 
Nous fournissons une mise à jour dès que le problème est causé de racine. 

## <a name="issues-launching-the-microsoft-store-and-apps-on-hololens"></a>Problèmes de lancement du Microsoft Store et les applications sur HoloLens

>[!NOTE]
>Dernière mise à jour : 4/2 @ 10 h - problème résolu. 

Vous pouvez rencontrer des problèmes lorsque vous tentez de lancer le Microsoft Store et les applications sur HoloLens. Nous avons déterminé que le problème se produit lorsque les mises à jour des applications d’arrière-plan déploiement une version plus récente des packages de framework dans des séquences spécifiques lors d’une ou plusieurs de leurs applications dépendantes sont en cours d’exécution. Dans ce cas, une mise à jour automatiques des applications remis une nouvelle version du Framework .NET Native (version 10.0.25531 à 10.0.27413) a provoqué les applications qui sont exécutent pas correctement mise à jour pour toutes les applications en cours d’exécution consomme la version précédente du framework.  Le flux de mise à jour de l’infrastructure est comme suit :-

1.  Le nouveau package de framework est téléchargé à partir du magasin et installé
2.  Toutes les applications à l’aide de l’infrastructure plus anciennes sont « updated » pour utiliser la version plus récente

Si l’étape 2 est interrompue avant la fin de toutes les applications pour lesquelles la toute dernière infrastructure n’a pas été inscrit échoue lancer à partir du menu Démarrer.  Nous pensons que n’importe quelle application sur HoloLens pourrait être affectée par ce problème.

Certains utilisateurs ont signalé que fermeture des applications bloquées et le lancement d’autres applications comme Hub de commentaires, 3D visionneuse ou Photos résout le problème pour eux - Toutefois, cela ne fonctionne pas 100 % du temps.

Nous avons racine a provoqué ce problème provoquée pas la mise à jour elle-même, mais un bogue dans le système d’exploitation qui a entraîné la mise à jour du framework .NET Native en cours pas correctement traité. Nous avons le plaisir d’annoncer que nous ont identifié un correctif et que vous avez publié une mise à jour (version 17763.380 du système d’exploitation) qui contient le correctif. 

Pour voir si votre appareil peut prendre la mise à jour de Veuillez :

1.  Accédez à l’application de « Paramètres » et ouvrez « Mise à jour et sécurité »
2.  Cliquez sur « Vérification des mises à jour »
3.  Si la mise à jour 17763.380 est disponible, mettez à jour vers cette version pour recevoir la correction du bogue de blocage d’application
4.  Lors de la mise à jour vers cette version du système d’exploitation, les applications doivent fonctionner comme prévu.

En outre, comme nous le faisons avec chaque nouvelle version du système d’exploitation HoloLens, nous avons enregistré l’image FFU pour le Microsoft Download Center au https://aka.ms/hololensdownload/10.0.17763.380. 

Si vous ne souhaitez pas prendre la mise à jour, nous avons publié une nouvelle version de l’application UWP de Microsoft Store à compter de 3/29. Une fois que vous avez la version mise à jour de la Store :

1) Ouvrez le Store et confirmez qu’il se charge.
2) Utiliser le mouvement de Bloom pour ouvrir le menu.
3) Tentative d’ouverture des applications précédemment endommagées
3) Si elle toujours ne peut pas être lancé, appuyez sur l’icône de l’application interrompue et sélectionnez Désinstaller.
4) Réinstallez ces applications à partir du magasin.

Si votre appareil est toujours Impossible de charger les applications, vous pouvez charger une version du .NET Framework de natif et du Runtime par le biais du centre de téléchargement en effectuant :

1)  Téléchargez [ce fichier zip](http://download.microsoft.com/download/8/5/C/85C23745-794C-419D-B8D7-115FBCCD6DA7/netfx_1.7.zip) à partir du Microsoft Download Center.  Lors de la décompression produira deux fichiers.  Microsoft.NET.Native.Runtime.1.7.appx et Microsoft.NET.Native.Framework.1.7.appx
2)  Vérifiez que votre appareil est déverrouillé de développement.  Si vous n’avez pas fait avant les instructions pour ce faire sont [ici](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fwindows%2Fmixed-reality%2Fusing-the-windows-device-portal&data=02%7C01%7Cjalynch%40microsoft.com%7C3622a462ebd04870fccb08d6ae94cad6%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636888351416725140&sdata=ZB6Zdx9GV95PcU6FAVgWaP3eQNMsyIc%2FbNDEby3Sb8A%3D&reserved=0).
3)  Ensuite, vous souhaitez obtenir dans le Windows Device Portal.  Notre recommandation est de le faire via USB et que vous le feriez qui en tapant http://127.0.0.1:10080 dans votre navigateur.  
4)  Une fois que le Windows Device Portal de nous vous devons « chargement indépendant », les deux fichiers que vous avez téléchargé.  Pour ce faire, vous devez descendre de la barre latérale gauche jusqu'à ce que vous accédez à la section « Applications » et cliquez sur « Applications ».
5)  Vous verrez ensuite un écran semblable à la ci-dessous.  Vous souhaitez accéder à la section intitulée « Installer l’application » et recherchez où vous avez décompressé ces deux fichiers APPX.  Vous pouvez uniquement effectuer l’une à la fois, par conséquent, une fois que vous sélectionnez le premier, puis cliquez sur « Go » sous la section déployer.  Puis le faire pour le deuxième fichier APPX. 
  ![Windows Device Portal pour installer l’application de chargement indépendant](images/20190322-DevicePortal.png)<br>
6)  À ce stade, nous pensons que vos applications doivent commencer à utiliser à nouveau et que vous pouvez également accéder au Store.
7)  Dans certains cas, il est nécessaire en exécuter une étape supplémentaire de lancement de l’application de visionneuse 3D avant que les applications affectées lancera. 

Nous vous remercions de votre patience que nous avons parcouru la procédure pour résoudre ce problème, nous sommes impatients de continuer à fonctionner avec notre communauté à créer de réalité mixte réussie des expériences.

## <a name="connecting-to-wifi"></a>Connexion au réseau sans fil

Pendant l’OOBE & paramètres, il existe un délai d’expiration des informations d’identification de 2 minutes. Le nom d’utilisateur/mot de passe doit être entré dans les 2 minutes sinon que le champ nom d’utilisateur sera automatiquement supprimé.

Nous vous recommandons d’utiliser un clavier Bluetooth pour la saisie des mots de passe longs.

## <a name="device-update"></a>Mise à jour de l’appareil
* 30 secondes après une nouvelle mise à jour, l’interpréteur de commandes peut disparaître une seule fois. Veuillez effectuer la **bloom** mouvement à reprendre votre session.

## <a name="visual-studio"></a>Visual Studio
* Consultez [installer les outils](install-the-tools.md) pour la version la plus récente de Visual Studio recommandé pour le développement de HoloLens.
* Lorsque vous déployez une application à partir de Visual Studio à votre HoloLens, vous pouvez rencontrer l’erreur : **L’opération demandée ne peut pas être effectuée sur un fichier avec une section mappée utilisateur ouverte. (Exception de HRESULT : 0x800704C8)** . Si cela se produit, essayez à nouveau et votre déploiement généralement réussira.

## <a name="emulator"></a>Émulateur
* Pas toutes les applications dans le Microsoft Store sont compatibles avec l’émulateur. Par exemple, Young pétarade et des Fragments ne sont pas lisibles sur l’émulateur.
* Vous ne pouvez pas utiliser la webcam de PC dans l’émulateur.
* La fonctionnalité d’aperçu de la Windows Device Portal ne fonctionne pas avec l’émulateur. Vous pouvez toujours capturer des images et vidéos de réalité mixte.

## <a name="unity"></a>Unity
* Consultez [installer les outils](install-the-tools.md) pour la version la plus récente de Unity recommandé pour le développement de HoloLens.
* Problèmes connus avec Unity HoloLens Technical Preview sont documentées dans le [forums de HoloLens Unity](http://forum.unity3d.com/threads/known-issues.394627/).

## <a name="windows-device-portal"></a>Windows Device Portal
* La fonctionnalité d’aperçu instantané dans la capture de réalité mixte peut présenter plusieurs secondes de la latence.
* Dans la page d’entrée virtuelle, les contrôles de mouvement et défilement sous la section mouvements virtuel ne fonctionnent pas. Leur utilisation n’a aucun effet. Le clavier virtuel sur la même page fonctionne correctement.
* Après avoir activé le Mode développeur dans les paramètres, il peut prendre quelques secondes avant que le commutateur pour activer le portail de l’appareil est activé.

## <a name="api"></a>API
* Si l’application définit le [concentrer point](focus-point-in-unity.md) derrière l’utilisateur ou à la normale à camera.forward, hologrammes n’apparaîtra pas dans la Capture de réalité mixte des photos ou vidéos. Jusqu'à ce que ce bogue est résolu dans Windows, si les applications définissent activement le [concentrer point](focus-point-in-unity.md) elles devraient assurer la normale de plan a la valeur opposée caméra-forward (par exemple, normal = - camera.forward).

## <a name="xbox-wireless-controller"></a>Contrôleur sans fil Xbox
* Xbox sans fil contrôleur S doit être mis à jour avant de pouvoir être utilisé avec HoloLens. Assurez-vous de vous êtes [à jour](https://support.xbox.com/xbox-one/accessories/update-controller-for-stereo-headset-adapter) avant de tenter d’associer votre contrôleur avec un HoloLens.
* Si vous redémarrez votre HoloLens tandis que le contrôleur sans fil Xbox est connecté, le contrôleur sera automatiquement de se reconnecter à HoloLens. Le voyant Guide clignote lentement jusqu'à ce que les compétences de contrôleur désactivé après 3 minutes. Se reconnecter à votre contrôleur immédiatement, de mettre hors tension le contrôleur en maintenant le bouton Guide jusqu'à ce que la lumière désactive. Lorsque vous mettez votre contrôleur à nouveau, il se reconnectera à HoloLens.
* Si votre HoloLens entre en veille pendant que le contrôleur sans fil Xbox est connecté, n’importe quelle entrée sur le contrôleur sortira de veille la HoloLens. Vous pouvez éviter cela en mise hors tension de votre contrôleur lorsque vous avez terminé l’utiliser.
