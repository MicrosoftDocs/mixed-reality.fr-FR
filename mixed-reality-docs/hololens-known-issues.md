---
title: Problèmes connus de HoloLens
description: Il s’agit de la liste des problèmes connus qui peuvent affecter les développeurs HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 07/10/2019
ms.topic: article
keywords: résolution des problèmes, problème connu, aide
ms.openlocfilehash: fe4e83764433cea5a772b26796d79ac156a59c5d
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434259"
---
# <a name="hololens-known-issues"></a>Problèmes connus de HoloLens

Voici la liste actuelle des problèmes connus liés à HoloLens qui affectent les développeurs. Vérifiez ici d’abord si vous constatez un comportement étrange. Cette liste est mise à jour à mesure que de nouveaux problèmes sont détectés ou signalés, ou lorsque des problèmes sont résolus dans les futures mises à jour logicielles HoloLens.

## <a name="unable-to-connect-and-deploy-to-hololens-through-visual-studio"></a>Impossible de se connecter à HoloLens et de le déployer dans Visual Studio

>[!NOTE]
>Dernière mise à jour : 8/8 @ 5:23 H 00-Visual Studio a publié VS 2019 version 16,2, qui inclut un correctif pour ce problème. Nous vous recommandons d’effectuer la mise à jour vers cette version la plus récente pour éviter d’avoir à rencontrer cette erreur.

Visual Studio a publié VS 2019 version 16,2, qui inclut un correctif pour résoudre ce problème. Nous vous recommandons d’effectuer la mise à jour vers cette version la plus récente pour éviter d’avoir à rencontrer cette erreur.

Cause première du problème : les utilisateurs qui ont utilisé Visual Studio 2015 ou les versions antérieures de Visual Studio 2017 pour déployer et déboguer des applications sur leur HoloLens, puis utiliser les dernières versions de Visual Studio 2017 ou Visual Studio 2019 avec le même HoloLens seront subi. Les nouvelles versions de Visual Studio déploient une nouvelle version d’un composant, mais les fichiers de la version antérieure sont conservés sur l’appareil, ce qui entraîne l’échec de la version plus récente.  Le message d’erreur suivant s’affiche : DEP0100 : Assurez-vous que le mode développeur est activé pour l’appareil cible. Impossible d’obtenir une licence de développeur sur <ip> en raison de l’erreur 80004005.
 
**Solution** : 

Bien que ce problème soit résolu dans Visual Studio 2019 16,2, les développeurs qui choisissent de rester dans les versions antérieures de Visual Studio peuvent utiliser les étapes suivantes pour contourner le problème et aider à débloquer le déploiement et le débogage :  
1. Ouvrir Visual Studio
2. Projet de > de fichiers >
3. Visual C# -> Windows Desktop-application console > (.NET Framework)
4. Donnez un nom au projet (par exemple, HoloLensDeploymentFix) et assurez-vous que l’infrastructure est définie sur au moins .NET Framework 4,5, puis cliquez sur OK.
5. Cliquez avec le bouton droit sur le nœud références dans Explorateur de solutions et ajoutez les références suivantes (cliquez sur la section « parcourir », puis sur « Parcourir... » bouton) :
    ```
    C:\Program Files (x86)\Windows Kits\10\bin\10.0.18362.0\x86\Microsoft.Tools.Deploy.dll
    C:\Program Files (x86)\Windows Kits\10\bin\10.0.18362.0\x86\Microsoft.Tools.Connectivity.dll
    C:\Program Files (x86)\Windows Kits\10\bin\10.0.18362.0\x86\SirepInterop.dll
    ```
    >[!NOTE]
    >Si 10.0.18362.0 n’est pas installé, utilisez la version la plus récente que vous avez.
 
6. Dans Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis choisissez Ajouter-> élément existant.
 
7. Accédez à C:\Program Files (x86) \Windows Kits\10\bin\10.0.18362.0\x86 et remplacez le filtre par «tous les fichiers (\*.\*)»
 
8. Sélectionnez SirepClient. dll et SshClient. dll, puis cliquez sur « Ajouter ».
 
9. Recherchez et sélectionnez les deux fichiers dans Explorateur de solutions (ils doivent se trouver au bas de la liste des fichiers) et remplacez « copier dans le répertoire de sortie » dans le Fenêtre Propriétés par « toujours copier ».
 
10. En haut du fichier, ajoutez ce qui suit à la liste existante des instructions’Using' : 
    ```
    using Microsoft.Tools.Deploy;
    using System.Net;
    ```
 
11. Dans « static void main (...) », ajoutez le code suivant :
    ```
    RemoteDeployClient client = RemoteDeployClient.CreateRemoteDeployClient();
    client.Connect(new ConnectionOptions()
    {
        Credentials = new NetworkCredential("DevToolsUser", string.Empty),
        IPAddress = IPAddress.Parse(args[0])
    });
    client.RemoteDevice.DeleteFile(@"C:\Data\Users\DefaultAccount\AppData\Local\DevelopmentFiles\VSRemoteTools\x86\CoreCLR\mscorlib.ni.dll");
    ```
12. Build-> générer la solution
 
13. Ouvrez une invite de commandes dans le dossier qui contient le fichier. exe compilé (par exemple, C:\MyProjects\HoloLensDeploymentFix\bin\Debug).
 
14. Exécutez l’exécutable et fournissez l’adresse IP de l’appareil en tant qu’argument de ligne de commande.  (Si vous êtes connecté via USB, vous pouvez utiliser 127.0.0.1, sinon utiliser l’adresse IP WiFi de l’appareil.)  Par exemple, « HoloLensDeploymentFix 127.0.0.1 »
 
15. Une fois que l’outil s’est arrêté sans message (cette opération ne doit prendre que quelques secondes), vous pouvez désormais déployer et déboguer à partir de Visual Studio 2017 ou version ultérieure.  L’utilisation continue de l’outil n’est pas nécessaire.


## <a name="issues-launching-the-microsoft-store-and-apps-on-hololens"></a>Problèmes lors du lancement du Microsoft Store et des applications sur HoloLens

>[!NOTE]
>Dernière mise à jour : 4/2 @ 10-problème résolu. 

Vous pouvez rencontrer des problèmes lors de la tentative de lancement du Microsoft Store et des applications sur HoloLens. Nous avons déterminé que le problème se produit lorsque les mises à jour d’applications en arrière-plan déploient une version plus récente des packages d’infrastructure dans des séquences spécifiques alors qu’une ou plusieurs de leurs applications dépendantes sont toujours en cours d’exécution. Dans ce cas, une mise à jour d’application automatique a fourni une nouvelle version de l’infrastructure .NET Native (version 10.0.25531 vers 10.0.27413), a provoqué les applications qui exécutent pour qu’elles ne soient pas correctement mises à jour pour toutes les applications en cours d’exécution qui utilisent la version antérieure du Framework.  Le Flow pour la mise à jour du Framework est le suivant :-

1.  Le nouveau package d’infrastructure est téléchargé à partir du Store et installé
2.  Toutes les applications utilisant l’ancien Framework sont mises à jour pour utiliser la version la plus récente

Si l’étape 2 est interrompue avant la fin, toutes les applications pour lesquelles l’infrastructure récente n’a pas été inscrite ne pourront pas être lancées à partir du menu Démarrer.  Nous pensons que toute application sur HoloLens pourrait être affectée par ce problème.

Certains utilisateurs ont signalé que la fermeture des applications bloquées et le lancement d’autres applications telles que le hub de commentaires, la visionneuse 3D ou les photos résout le problème pour eux, mais cela ne fonctionne pas 100% du temps.

La racine a provoqué que ce problème n’a pas provoqué la mise à jour elle-même, mais un bogue dans le système d’exploitation qui a entraîné la gestion incorrecte de la mise à jour .NET Native Framework. Nous sommes heureux de vous annoncer que nous avons identifié un correctif et que vous avez publié une mise à jour (version 17763,380) contenant le correctif. 

Pour voir si votre appareil peut effectuer la mise à jour, procédez comme suit :

1.  Accédez à l’application « paramètres » et ouvrez « mettre à jour & sécurité ».
2.  Cliquez sur « Rechercher les mises à jour »
3.  Si la mise à jour vers 17763,380 est disponible, mettez-la à jour vers cette build pour recevoir le correctif pour le bogue de blocage de l’application
4.  Lors de la mise à jour vers cette version du système d’exploitation, les applications doivent fonctionner comme prévu.

En outre, comme nous le faisons avec chaque version du système d’exploitation HoloLens, nous avons publié l’image FFU dans le centre de téléchargement Microsoft à l’adresse https://aka.ms/hololensdownload/10.0.17763.380. 

Si vous ne souhaitez pas effectuer la mise à jour, nous avons publié une nouvelle version de l’application Microsoft Store UWP à partir du 3/29. Une fois que vous disposez de la version mise à jour du magasin :

1) Ouvrez le magasin et confirmez qu’il est chargé.
2) Utilisez le geste fleuri pour ouvrir le menu.
3) Tentative d’ouverture d’applications qui ont été interrompues
3) S’il ne peut toujours pas être lancé, appuyez et maintenez l’icône de l’application endommagée, puis sélectionnez Désinstaller.
4) Resinstall ces applications à partir du Store.

Si votre appareil n’est toujours pas en mesure de charger des applications, vous pouvez chargement une version de l’infrastructure .NET Native et du runtime à l’aide du centre de téléchargement en procédant comme suit :

1)  Téléchargez [ce fichier zip](https://download.microsoft.com/download/8/5/C/85C23745-794C-419D-B8D7-115FBCCD6DA7/netfx_1.7.zip) à partir du centre de téléchargement Microsoft.  La décompression produira deux fichiers.  Microsoft. NET. native. Runtime. 1.7. AppX et Microsoft. NET. native. Framework. 1.7. AppX
2)  Vérifiez que votre appareil est déverrouillé.  Si vous ne l’avez pas fait, les instructions à cet effet sont disponibles [ici](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2F%2Fwindows%2Fmixed-reality%2Fusing-the-windows-device-portal&data=02%7C01%7Cjalynch%40microsoft.com%7C3622a462ebd04870fccb08d6ae94cad6%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C636888351416725140&sdata=ZB6Zdx9GV95PcU6FAVgWaP3eQNMsyIc%2FbNDEby3Sb8A%3D&reserved=0).
3)  Vous souhaitez ensuite accéder au portail de périphériques Windows.  Nous vous recommandons de le faire par le biais d’une interface USB. pour ce faire, vous devez taper https://127.0.0.1:10080 dans votre navigateur.  
4)  Une fois que vous disposez du portail des appareils Windows, nous avons besoin de « charger en charge » les deux fichiers que vous avez téléchargés.  Pour ce faire, vous devez descendre dans la barre latérale de gauche jusqu’à ce que vous obteniez la section « Apps » et que vous cliquiez sur « apps ».
5)  Un écran similaire à celui ci-dessous s’affiche.  Vous souhaitez accéder à la section intitulée « installer l’application » et accéder à l’emplacement où vous avez décompressé ces deux fichiers APPX.  Vous ne pouvez effectuer qu’un seul à la fois. par conséquent, après avoir sélectionné le premier, cliquez sur « Go » sous la section déployer.  Effectuez ensuite cette opération pour le deuxième fichier APPX. 
  ![le portail de l’appareil Windows pour installer l’application chargée côté](images/20190322-DevicePortal.png)<br>
6)  À ce stade, nous pensons que vos applications doivent commencer à fonctionner à nouveau et que vous pouvez également accéder au Store.
7)  Dans certains cas, il est nécessaire d’exécuter l’étape supplémentaire de lancement de l’application de visionneuse 3D avant le lancement des applications affectées. 

Nous vous remercions de votre patience, car nous avons passé en revue le processus de résolution de ce problème. nous sommes impatients de continuer à travailler avec notre communauté pour créer des expériences de réalité mixte fructueuses.

## <a name="connecting-to-wifi"></a>Connexion au Wi-Fi

Au cours des paramètres d' & OOBE, le délai d’expiration des informations d’identification est de 2 minutes. Le nom d’utilisateur et le mot de passe doivent être entrés dans un délai de 2 minutes, sinon, le champ nom d’utilisateur est automatiquement effacé.

Nous vous recommandons d’utiliser un clavier Bluetooth pour entrer des mots de passe longs.

>[!NOTE]
> Si le mauvais réseau est sélectionné au cours de l’OOBE, l’appareil doit être entièrement réinitialisé. Vous trouverez des instructions [ici.](https://docs.microsoft.com//windows/mixed-reality/reset-or-recover-your-hololens#perform-a-full-device-recovery) 

## <a name="device-update"></a>Mise à jour de l’appareil
* 30 secondes après une nouvelle mise à jour, l’interpréteur de commandes peut disparaître une fois. Effectuez le geste de **floraison** pour reprendre votre session.

## <a name="visual-studio"></a>Visual Studio
* Consultez [installer les outils](install-the-tools.md) pour la version la plus récente de Visual Studio recommandée pour le développement HoloLens.
* Lorsque vous déployez une application à partir de Visual Studio dans votre HoloLens, vous pouvez voir s’afficher l’erreur : **l’opération demandée ne peut pas être effectuée sur un fichier avec une section mappée par l’utilisateur ouverte. (Exception de HRESULT : 0x800704C8)** . Si cela se produit, réessayez et votre déploiement fonctionnera généralement.

## <a name="emulator"></a>Émulateur
* Toutes les applications dans le Microsoft Store ne sont pas compatibles avec l’émulateur. Par exemple, les Conker et les fragments de Young ne sont pas lisibles sur l’émulateur.
* Vous ne pouvez pas utiliser la webcam de l’ordinateur dans l’émulateur.
* La fonctionnalité d’aperçu instantané du portail de périphériques Windows ne fonctionne pas avec l’émulateur. Vous pouvez toujours capturer des vidéos et des images de réalité mixte.

## <a name="unity"></a>Unity
* Consultez [installer les outils](install-the-tools.md) pour la version la plus à jour d’Unity recommandée pour le développement HoloLens.
* Les problèmes connus avec Unity HoloLens Technical Preview sont documentés dans les [Forums Hololens Unity](https://forum.unity3d.com/threads/known-issues.394627/).

## <a name="windows-device-portal"></a>Windows Device Portal
* La fonctionnalité d’aperçu instantané de la capture de la réalité mixte peut présenter plusieurs secondes de latence.
* Sur la page d’entrée virtuelle, les contrôles de mouvement et de défilement sous la section des mouvements virtuels ne sont pas fonctionnels. Leur utilisation n’aura aucun effet. Le clavier virtuel sur la même page fonctionne correctement.
* Après l’activation du mode développeur dans les paramètres, l’activation du commutateur Device Portal peut prendre quelques secondes.

## <a name="api"></a>API
* Si l’application définit le [point de focus](focus-point-in-unity.md) sous-jacent à l’utilisateur ou normal à Camera. Forward, les hologrammes n’apparaîtront pas dans la réalité mixte capturer des photos ou des vidéos. Jusqu’à ce que ce bogue soit résolu dans Windows, si les applications définissent activement le [point de focalisation](focus-point-in-unity.md) , elles doivent s’assurer que la normale du plan est définie à l’opposé de la caméra (par exemple, normal =-Camera. Forward).

## <a name="xbox-wireless-controller"></a>Contrôleur Xbox Wireless
* Les contrôleurs Xbox Wireless S doivent être mis à jour avant de pouvoir être utilisés avec HoloLens. Vérifiez que vous êtes à [jour](https://support.xbox.com/xbox-one/accessories/update-controller-for-stereo-headset-adapter) avant d’essayer de coupler votre contrôleur à un HoloLens.
* Si vous redémarrez votre HoloLens alors que le contrôleur sans fil Xbox est connecté, le contrôleur ne se reconnectera pas automatiquement à HoloLens. La lumière du bouton du repère clignote lentement jusqu’à ce que le contrôleur s’éteigne après 3 minutes. Pour reconnecter immédiatement votre contrôleur, mettez le contrôleur hors tension en maintenant le bouton du repère enfoncé jusqu’à ce que la lumière s’arrête. Lorsque vous remettez votre contrôleur sous tension, il se reconnecte à HoloLens.
* Si votre HoloLens passe en mode veille alors que le contrôleur sans fil Xbox est connecté, toute entrée sur le contrôleur sort le contrôle HoloLens. Vous pouvez éviter cela en éteignant votre contrôleur lorsque vous avez fini de l’utiliser.
