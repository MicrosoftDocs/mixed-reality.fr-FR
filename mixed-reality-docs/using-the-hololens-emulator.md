---
title: À l’aide de l’émulateur HoloLens
description: L’émulateur de HoloLens vous permet de tester des applications de réalité mixte sur votre PC sans un HoloLens physique.
author: pbarnettms
ms.author: pbarnett
ms.date: 04/25/2019
ms.topic: article
keywords: HoloLens, l’émulateur
ms.openlocfilehash: 0a8fa6bb7c7c5bb846604b7a1878911f028d8cba
ms.sourcegitcommit: f5c1dedb3b9e29f27f627025b9e7613931a7ce18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64580657"
---
# <a name="using-the-hololens-emulator"></a>À l’aide de l’émulateur HoloLens

L’émulateur de HoloLens vous permet de tester des applications HOLOGRAPHIQUE sur votre PC sans un HoloLens physique et est fourni avec l’ensemble d’outils de développement HoloLens. L’émulateur utilise un ordinateur virtuel Hyper-V. Les entrées homme et l’environnementales qui seraient généralement être lues par les capteurs sur le HoloLens sont simulées à la place à l’aide de votre clavier, souris ou manette Xbox. Les applications ne doivent être modifiés pour s’exécuter sur l’émulateur et ne connaissez pas qu’ils ne sont pas en cours d’exécution sur un véritable HoloLens.

Si vous avez besoin pour développer des applications de réalité mixte Windows immersives (VR) casque ou des jeux pour ordinateurs de bureau, consultez le [simulateur de réalité mixte Windows](using-the-windows-mixed-reality-simulator.md), ce qui vous permet de simuler les casques de postes de travail à la place.


## <a name="installing-the-hololens-emulator"></a>Installation de l’émulateur HoloLens
Télécharger l’émulateur de HoloLens et modèles de projet HOLOGRAPHIQUE.

Versions : 
* [Émulateur de 2 HoloLens et modèles de projet HOLOGRAPHIQUE](https://go.microsoft.com/fwlink/?linkid=2087187).
* [Émulateur de HoloLens (1er Gen) et les modèles de projet HOLOGRAPHIQUE](https://go.microsoft.com/fwlink/?linkid=2065980).

Vous trouverez des versions antérieures de l’émulateur HoloLens sur le [archive de l’émulateur de HoloLens](hololens-emulator-archive.md) page.

### <a name="hololens-emulator-system-requirements"></a>Configuration requise HoloLens émulateur

L’émulateur de HoloLens utilise Hyper-V avec RemoteFx (1er Gen émulateur) ou du GPU-PV (HoloLens 2 émulateur) pour le matériel accéléré des graphiques. Pour utiliser l’émulateur, vérifiez que votre ordinateur répond à ces exigences de matériel :
* 64-bit Windows 10 Pro, entreprise ou l’enseignement 
    >[!NOTE]
    >Windows 10 Édition familiale ne prend pas en charge Hyper-V ou l’émulateur de HoloLens.  
    >L’émulateur de 2 HoloLens nécessite de mettre à jour du 10 octobre 2018 Windows ou une version ultérieure.
* Processeur 64 bits
* Processeur avec 4 cœurs (ou plusieurs processeurs avec un total de 4 cœurs)
* 8 Go de RAM ou plus
* Dans le BIOS, les fonctionnalités suivantes doivent être [pris en charge et activé](http://blogs.technet.com/b/iftekhar/archive/2010/08/09/enable-hardware-settings-in-bios-to-run-hyper-v.aspx):
   * Virtualisation assistée par le matériel
   * Traduction d’adresse de second niveau (SLAT, Second Level Address Translation)
   * Prévention de l’exécution des données au niveau matériel (DEP, Data Execution Prevention)
* Configuration requise du GPU
   * DirectX 11.0 ou version ultérieure
   * Pilote de graphiques WDDM 1.2 ou version ultérieure (1er Gen)
   * Pilote de graphiques WDDM 2.5 (HoloLens 2 émulateur)
   * L’émulateur peut fonctionner avec un GPU non pris en charge, mais sera beaucoup plus lent

Si votre système répond aux exigences ci-dessus, **, assurez-vous que la fonctionnalité « Hyper-V » a été activée sur votre système** via le panneau de configuration -> Programmes -> Programmes et fonctionnalités -> Activer les fonctionnalités de Windows ou off -> Vérifiez que « Hyper-V » est sélectionnée pour l’installation de l’émulateur réussir.

## <a name="deploying-apps-to-the-hololens-emulator"></a>Déploiement d’applications sur l’émulateur HoloLens

1. Charger votre solution d’application dans Visual Studio.
    >[!NOTE]
    >Lorsque vous utilisez Unity, générez votre projet à partir de Unity et puis chargez la solution créée dans Visual Studio comme d’habitude.
2. Pour l’émulateur de HoloLens (1er Gen), vérifiez la plateforme est définie sur **x86**. Pour l’émulateur de 2 HoloLens, vérifiez la plateforme est définie sur **x86** ou **x64**.
3. Sélectionnez l’élément **HoloLens émulateur** version en tant que l’appareil cible pour le débogage.
4. Accédez à **Déboguer > Démarrer le débogage** ou appuyez sur **F5** pour lancer l’émulateur et de déployer votre application pour le débogage.

L’émulateur peut prendre une minute ou plus pour démarrer lors du premier démarrage. Nous vous recommandons de conserver l’émulateur ouvert pendant votre session de débogage afin de déployer rapidement des applications à l’émulateur en cours d’exécution.

## <a name="basic-emulator-input"></a>Entrée de l’émulateur de base

Contrôle de l’émulateur est très similaire à de nombreux de jeux vidéo 3D courantes. Options d’entrée sont disponibles à l’aide du clavier, souris ou manette Xbox. Vous contrôlez l’émulateur en dirigeant les actions d’un utilisateur simulé a porter un HoloLens. Vos actions déplacement que l’utilisateur simulé autour et les applications qui s’exécutent dans l’émulateur répondent comme ils le feraient sur un appareil réel.

Le curseur sur HoloLens (1er Gen) suit le mouvement de la tête et de rotation.  Dans l’émulateur de 2 HoloLens, le curseur suit les mouvements de main et l’orientation.

* **Remonter vers l’avant, arrière, gauche et avec le bouton droit** -utiliser le W, A, S et D clés sur votre clavier ou la clé gauche sur une manette Xbox.
* **Rechercher, vers le bas, gauche et avec le bouton droit** -cliquez et faites glisser la souris, utilisez les touches de direction sur votre clavier ou la clé droite sur une manette Xbox.
* **Geste d’appui en l’air** - avec le bouton droit de la souris, appuyez sur la touche entrée de votre clavier ou utilisez le bouton A sur un contrôleur Xbox.
* **Mouvement de Bloom/système** : appuyez sur la clé de Windows ou la touche F2 du clavier, ou appuyez sur le bouton B sur une manette Xbox.
* **Remettez le déplacement des défilement** : maintenez la touche Alt enfoncée, maintenez le bouton droit de la souris et faites glisser la souris haut / bas, ou dans une manette Xbox maintenez le déclencheur de droite et un bouton et la clé droite haut et bas.
* **Remettez le déplacement et l’orientation** (2 HoloLens émulateur uniquement) - maintenez la touche Alt enfoncée et faites glisser la souris en haut / bas / gauche / droite pour déplacer la main ou utiliser les touches de direction et Q / E pour faire pivoter et incliner l’aiguille.  Pour une manette Xbox, maintenez la touche gauche ou droit pare-chocs et utilisez le stick analogique gauche pour déplacer la main gauche / droite / vers l’avant / arrière, le stick analogique droit pour faire pivoter et haut / bas sur le Dpad pour augmenter ou diminuer la main.

## <a name="anatomy-of-the-hololens-2-emulator"></a>Anatomie de l’émulateur HoloLens 2 

### <a name="main-window"></a>Fenêtre principale

![Fenêtre principale de HoloLens 2 émulateur](images/emulator2-900px.png)

### <a name="toolbar"></a>Barre d’outils

À droite de la fenêtre principale, se trouve dans la barre d’outils de l’émulateur. La barre d’outils contient les boutons suivants :
* ![Icône de fermeture](images/emulator-close.png) **fermer**: Ferme l’émulateur.
* ![Icône de réduction](images/emulator-minimize.png) **réduire**: Réduit la fenêtre de l’émulateur.
* ![Simulation_icon](images/emulator-simulation-panel.png) **Simulation le panneau de configuration**: Afficher ou masquer la [Simulation le panneau de configuration](#simulation-control-panel) pour configurer et contrôler [d’entrée à l’émulateur](#basic-emulator-input).
* ![Ajuster à l’icône de l’écran](images/emulator-fit.png) **ajuster à l’écran**: Ajuste l’émulateur à l’écran.
* ![Icône de zoom](images/emulator-zoom.png) **Zoom**: À l’émulateur de grands et plus petits.
* ![Icône d’aide](images/emulator-help.png) **aide**: Ouvrir l’aide de l’émulateur.
* ![Icône de portail périphérique ouvert](images/emulator-deviceportal.png) **ouvrir le portail de périphérique**: Ouvrez le Windows Device Portal pour le système d’exploitation de HoloLens dans l’émulateur.
* ![Icône Tools](images/emulator-tools.png) **outils**: Ouvrez le **des outils supplémentaires** volet.

### <a name="simulation-control-panel"></a>Panneau de configuration de simulation

Le panneau de configuration de Simulation permet de vous permet d’afficher la position actuelle et l’orientation d’appareils simulés humaines et simulés d’entrée.  Il vous permet également à configurer les deux entrée simulé, comme l’affichage ou masquage d’un ou deux mains et appareils utilisés pour contrôler l’entrée simulée tels que le clavier, souris et gamepad de votre ordinateur.

![Panneau de configuration de simulation](images/emulator-simulation-control-panel.png)

* Pour afficher ou masquer le volet de simulation, cliquez sur le bouton de barre d’outils ou appuyez sur F7 sur votre clavier.
* Pointez la souris sur un contrôle ou un champ pour afficher une info-bulle qui contient des contrôles de clavier et souris gamepad pour celui-ci.
* Pour afficher ou masquer une main, basculez l’approprié sous la main gauche ou droite.
* Pour contrôler la main, utilisez les touches Alt gauche ou droite sur votre clavier ou pare-chocs gauche ou droit du boîtier de commande.
* Pour indiquer toutes les entrées à un ou deux mains, cliquez sur le bouton punaise sous le bouton bascule.  Il s’agit de l’équivalent de maintenant la touche Alt enfoncée pour la main.
* Pour contrôler la direction du regard yeux, cliquez sur la punaise dans la section « Yeux ».  Il s’agit de l’équivalent d’enfoncée la touche « Y » sur le clavier.
* Pour charger une salle de l’enregistrement, cliquez sur le bouton « Load » dans la section « Enregistrement ».  Consultez [simulated salles](#simulated-rooms) pour plus d’informations.
* Pour ajuster la vitesse à laquelle les appareils simulés humaines ou simulés d’entrée seront déplacer ou faire pivoter en réponse à un clavier, souris ou boîtier de commande d’entrée et cliquez sur l’icône d’engrenage en regard de « Paramètres d’entrée » réglez les curseurs.
* Par défaut, entrée au clavier contrôle l’entrée humaine et simulée simulée.  Pour que l’entrée au clavier de votre PC envoyée via pour le HoloLens, décochez la case « Utilisation du clavier pour la simulation ».  F4 est la touche de raccourci pour ce paramètre.
* Si le volet de la simulation est déjà visible, sur la touche F8 déplace le focus clavier vers elle.
* Pour détacher le panneau de la simulation à partir de la fenêtre de l’émulateur, cliquez sur le bouton en bas du panneau, ou appuyez sur F9 sur votre clavier.  Fermeture de la fenêtre ou en appuyant sur F9 à nouveau retournera la fenêtre à l’émulateur.
* Le panneau de configuration de simulation peut être lancé comme une application distincte, ce qui vous permet de vous connecter à et contrôler l’émulateur de 2 HoloLens, un appareil HoloLens 2 ou simulation de réalité mixte Windows en exécutant PerceptionSimulationInput.exe à partir de % ProgramFiles(x86) % \ Windows Kits\10\Microsoft XDE\10.0.18362.0\.

### <a name="account-tab"></a>Onglet Compte

L’onglet compte permet de configurer l’émulateur pour se connecter avec un Account de Microsoft. Cela est utile pour tester les API qui oblige l’utilisateur à être connecté avec un compte.  Activation/désactivation de cette option nécessite complètement fermez et redémarrez l’émulateur de HoloLens pour le paramètre prenne effet.  Si cette option est activée, les lancements suivants de l’émulateur vous demande de connexion, tout comme un utilisateur serait la première fois que le HoloLens est démarré.  Pour rapidement entrer vos informations d’identification à l’aide du clavier de votre PC, tout d’abord désactiver « Utilisation du clavier pour la simulation » dans le panneau de configuration de Simulation, ou appuyez sur F4 sur votre clavier pour activer/désactiver le paramètre de clavier ou désactiver.

### <a name="optional-settings-tab"></a>Onglet Paramètres facultatifs

L’onglet Paramètres facultatifs affiche un contrôle pour activer ou désactiver le graphique accélérée de matériel.  Graphique accélérée de matériel sera utilisé par défaut si pris en charge par le pilote de carte de graphiques de votre PC.  Si le pilote de votre carte graphique ne prend pas en charge les GPU-PV, cette option ne sera pas visible.

### <a name="diagnostics-tab"></a>Onglet Diagnostics

L’onglet Diagnostics montre adresse IP de l’émulateur sous la forme d’un lien pour Windows Device Portal, ainsi que l’état du GPU virtuel.


## <a name="anatomy-of-the-hololens-1st-gen-emulator"></a>Anatomie de la HoloLens (1er Gen) émulateur

### <a name="main-window"></a>Fenêtre principale

Quand l’émulateur démarre, vous verrez une fenêtre qui affiche le système d’exploitation HoloLens.

![Fenêtre principale d’émulateur de HoloLens](images/emulator-890px.png)

### <a name="toolbar"></a>Barre d’outils

À droite de la fenêtre principale, se trouve dans la barre d’outils de l’émulateur. La barre d’outils contient les boutons suivants :
* ![Icône de fermeture](images/emulator-close.png) **fermer**: Ferme l’émulateur.
* ![Icône de réduction](images/emulator-minimize.png) **réduire**: Réduit la fenêtre de l’émulateur.
* ![Icône d’entrée humaine](images/emulator-control.png) **humaine d’entrée**: Clavier et souris permettent de simuler humaine [d’entrée à l’émulateur](#basic-emulator-input).
* ![Icône d’entrée de clavier et souris](images/emulator-input.png) **clavier et souris d’entrée**: Entrée clavier et souris sont passées directement au système d’exploitation HoloLens en tant qu’événements de clavier et souris comme si vous connecté un clavier et souris Bluetooth.
* ![Ajuster à l’icône de l’écran](images/emulator-fit.png) **ajuster à l’écran**: Ajuste l’émulateur à l’écran.
* ![Icône de zoom](images/emulator-zoom.png) **Zoom**: À l’émulateur de grands et plus petits.
* ![Icône d’aide](images/emulator-help.png) **aide**: Ouvrir l’aide de l’émulateur.
* ![Icône de portail périphérique ouvert](images/emulator-deviceportal.png) **ouvrir le portail de périphérique**: Ouvrez le Windows Device Portal pour le système d’exploitation de HoloLens dans l’émulateur.
* ![Icône Tools](images/emulator-tools.png) **outils**: Ouvrez le **des outils supplémentaires** volet.

### <a name="simulation-tab"></a>Onglet de simulation

L’onglet par défaut dans le **des outils supplémentaires** volet est le **Simulation** onglet.

![Volet « Outils supplémentaires » de HoloLens émulateur](images/emulator-simulation-500px.png)

L’onglet de la Simulation affiche l’état actuel des capteurs simulés utilisé pour piloter le système d’exploitation de HoloLens au sein de l’émulateur. Vous placez le curseur sur n’importe quelle valeur dans l’onglet Simulation fournira une info-bulle qui décrit comment contrôler cette valeur.

### <a name="room-tab"></a>Onglet espace

L’émulateur simule entrée world sous la forme de la maille de mappage spatial de simulé « locaux ». Cet onglet vous permet de choisir quels salle à charger au lieu de la salle par défaut.

![Onglet 'Salles de conversation' d’émulateur de HoloLens](images/emulator-room-500px.png)

Consultez [simulated salles](#simulated-rooms) pour plus d’informations.

### <a name="account-tab"></a>Onglet Compte

L’onglet compte permet de configurer l’émulateur pour se connecter avec un Account de Microsoft. Cela est utile pour tester les API qui oblige l’utilisateur à être connecté avec un compte. Après avoir vérifié la zone sur cette page, les lancements suivants de l’émulateur vous demande de connexion, comme le ferait un utilisateur la première fois le HoloLens est démarré.

## <a name="simulated-rooms"></a>Salles simulés

Salles simulées sont utiles pour tester votre application dans plusieurs environnements. Plusieurs pièces sont fournis avec l’émulateur et une fois que vous installez l’émulation, vous les trouverez dans % ProgramFiles% (x86) %\Windows Kits\10\Microsoft XDE\\(version) \Plugins\Rooms. Toutes ces locaux ont été capturés dans des environnements réels à l’aide d’un HoloLens :
* **DefaultRoom.xef** -un petite salon grâce à un téléviseur, art et deux canapés. Chargé par défaut lorsque vous démarrez l’émulateur.
* **Bedroom1.xef** -petite votre chambre avec un support.
* **Bedroom2.xef** -votre chambre avec un banc de taille Dame, buffet, nightstands et walk-in placard.
* **GreatRoom.xef** -une salle de très grand espace ouvert avec salon, à manger table et cuisine.
* **LivingRoom.xef** : un salon grâce à un foyer, canapé, CANAPES, ainsi qu’une table de café avec un vase.

Vous pouvez également enregistrer vos propres locaux à utiliser dans l’émulateur à l’aide de la page de Simulation de la [Windows Device Portal](using-the-windows-device-portal.md) sur votre HoloLens (1er Gen).

Dans l’émulateur, vous verrez seulement hologrammes que vous effectuez le rendu et vous ne verrez pas la salle simulée derrière les hologrammes. Ceci est le véritable HoloLens là où se trouve à la fois à la différence fusionnée ensemble. Si vous souhaitez voir la salle simulée dans l’émulateur de HoloLens, vous devez mettre à jour votre application pour afficher le maillage de mappage spatial dans la scène.

## <a name="troubleshooting"></a>Résolution des problèmes

Vous pouvez rencontrer une erreur lors de l’installation de l’émulateur dont vous avez besoin *« Visual Studio 2015 Update 1 and UWP tools version 1.2 »*. Il existe trois causes possibles de cette erreur :
* Vous n’avez pas une version suffisamment récente de Visual Studio (Visual Studio 2019, Visual Studio 2017 ou Visual Studio 2015 Update 1 ou version ultérieure). Pour corriger ce problème, installez la dernière version de Visual Studio.
* Vous avez une version suffisamment récente de Visual Studio, mais vous n’avez pas installé les outils de plateforme universelle Windows (UWP). Il s’agit d’une fonctionnalité facultative pour Visual Studio.

Vous pouvez également voir une erreur d’installation de l’émulateur sur un non-Enterprise/Pro/éducation référence (SKU) de Windows ou si vous n’avez pas de fonctionnalité de Hyper-V activé.
* Veuillez lire le [requise](#hololens-emulator-system-requirements) section ci-dessus pour un ensemble complet de la configuration requise.
* Vérifiez également que la fonctionnalité Hyper-V a été activée sur votre système.

Si votre installation est terminée avec succès, mais vous ne voyez pas l’émulateur de HoloLens en tant qu’option de déploiement et le débogage, vérifiez les éléments suivants :
* Configuration de votre projet Visual Studio a x86 (Gen 1 st HoloLens) ou x86 ou x64 (HoloLens 2 émulateur).
* Si vous utilisez Visual Studio 2019, l’ensemble d’outils de plateforme dans votre configuration de projet a la valeur v142.

Si votre installation est terminée avec succès, mais Visual Studio affiche une erreur de tentative de lancement de l’émulateur HoloLens, essayez les opérations suivantes :
* Exécuter Visual Studio en tant qu’administrateur
* Si vous avez toujours eu Visual Studio 2019 installé, vérifiez que la valeur de Registre « KitsRoot10 » au HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Kits\Installed racines pointe vers votre dossier de Program Files 32 bits (par exemple, « C:\Program Files (x86) \Windows Kits \10 »).  Si elle n’est pas le cas, désinstallez l’émulateur de HoloLens, modifier la valeur de Registre dans votre dossier Program Files de 32 bits, puis réinstallez l’émulateur de HoloLens.  Ce problème est résolu dans Visual Studio 2019 16.0.3.

Si l’émulateur affiche une boîte de dialogue Erreur « Encodage octets non valide » lors du lancement :
* Supprimez tous les fichiers %localappdata%\Microsoft\XDE\HCS et réessayez.

Si votre liste de cible de débogage dans Visual Studio est vide (par exemple, « Start » est la seule option) et que vous avez suivi toutes les étapes de dépannage ci-dessus :
* Supprimez le dossier « ConfigurationCache » dans %localappdata%\Microsoft\VisualStudio\\<*id d’installation*> \CoreCon et réessayez.

Si votre système se bloque lors du démarrage de l’émulateur, désactivez l’accélération matérielle pour les graphiques de l’émulateur.
* Créez une valeur DWORD de Registre nommée « DisableGPU » à HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\XDE\10.0 et définissez sa valeur sur 1.

## <a name="see-also"></a>Voir aussi
* [Entrées avancées dans l’émulateur HoloLens et le simulateur de réalité mixte](advanced-hololens-emulator-and-mixed-reality-simulator-input.md)
* [Historique de l’émulateur de HoloLens logiciel](hololens-emulator-archive.md)
* [Mappage spatial dans Unity](spatial-mapping-in-unity.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)
