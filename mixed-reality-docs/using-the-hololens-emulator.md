---
title: À l’aide de l’émulateur HoloLens
description: L’émulateur de HoloLens vous permet de tester des applications de réalité mixte sur votre PC sans un HoloLens physique.
author: JonMLyons
ms.author: jlyons
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens, l’émulateur
ms.openlocfilehash: 3551bf48037f0cb7e8d243f2d89d43664e7c3475
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596683"
---
# <a name="using-the-hololens-emulator"></a>À l’aide de l’émulateur HoloLens

L’émulateur de HoloLens vous permet de tester des applications HOLOGRAPHIQUE sur votre PC sans un HoloLens physique et est fourni avec l’ensemble d’outils de développement HoloLens. L’émulateur utilise un ordinateur virtuel Hyper-V. Les entrées homme et l’environnementales qui seraient généralement être lues par les capteurs sur le HoloLens sont simulées à la place à l’aide de votre clavier, souris ou manette Xbox. Les applications ne doivent être modifiés pour s’exécuter sur l’émulateur et ne connaissez pas qu’ils ne sont pas en cours d’exécution sur un véritable HoloLens.

Si vous avez besoin pour développer des applications de réalité mixte Windows immersives (VR) casque ou des jeux pour ordinateurs de bureau, consultez le [simulateur de réalité mixte Windows](using-the-windows-mixed-reality-simulator.md), ce qui vous permet de simuler les casques de postes de travail à la place.

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

## <a name="installing-the-hololens-emulator"></a>Installation de l’émulateur HoloLens

Téléchargez le [HoloLens (1er gen) émulateur et les modèles de projet HOLOGRAPHIQUE](https://go.microsoft.com/fwlink/?linkid=2065980).

Vous trouverez des versions antérieures de l’émulateur HoloLens sur le [archive de l’émulateur HoloLens](hololens-emulator-archive.md) page.

### <a name="hololens-emulator-system-requirements"></a>Configuration système requise pour HoloLens émulateur

L’émulateur de HoloLens est basé sur Hyper-V et utilise de RemoteFx pour graphique accélérée de matériel. Pour utiliser l’émulateur, vérifiez que votre ordinateur répond à ces exigences de matériel :
* 64-bit Windows 10 Pro, entreprise ou l’enseignement 
    >[!NOTE]
    >Windows 10 Édition familiale ne prend pas en charge Hyper-V ou l’émulateur HoloLens
* Processeur 64 bits
* Processeur avec 4 cœurs (ou plusieurs processeurs avec un total de 4 cœurs)
* 8 Go de RAM ou plus
* Dans le BIOS, les fonctionnalités suivantes doivent être [pris en charge et activé](http://blogs.technet.com/b/iftekhar/archive/2010/08/09/enable-hardware-settings-in-bios-to-run-hyper-v.aspx):
   * Virtualisation assistée par le matériel
   * Traduction d’adresse de second niveau (SLAT, Second Level Address Translation)
   * Prévention de l’exécution des données au niveau matériel (DEP, Data Execution Prevention)
* Exigences de GPU (l’émulateur peut fonctionner avec un GPU non pris en charge, mais sera beaucoup plus lent)
   * DirectX 11.0 ou version ultérieure
   * Les pilotes WDDM 1.2 ou version ultérieure

Si votre système répond aux exigences ci-dessus, **, assurez-vous que la fonctionnalité « Hyper-V » a été activée sur votre système** via le panneau de configuration -> Programmes -> Programmes et fonctionnalités -> Activer les fonctionnalités de Windows ou off -> Vérifiez que « Hyper-V » est sélectionnée pour l’installation de l’émulateur réussir.

### <a name="installation-troubleshooting"></a>Dépannage de l’installation

Vous pouvez rencontrer une erreur lors de l’installation de l’émulateur dont vous avez besoin *« Visual Studio 2015 Update 1 and UWP tools version 1.2 »*. Il existe trois causes possibles de cette erreur :
* Vous n’avez pas une version suffisamment récente de Visual Studio (Visual Studio 2017 ou Visual Studio 2015 Update 1 ou version ultérieure). Pour corriger ce problème, installez la dernière version de Visual Studio.
* Vous avez une version suffisamment récente de Visual Studio, mais vous n’avez pas installé les outils de plateforme universelle Windows (UWP). Il s’agit d’une fonctionnalité facultative pour Visual Studio.

Vous pouvez également voir une erreur d’installation de l’émulateur sur un non-Enterprise/PRO/éducation référence (SKU) de Windows ou si vous n’avez pas de fonctionnalité de Hyper-V activé.
* Veuillez lire le [requise](#hololens-emulator-system-requirements) section ci-dessus pour un ensemble complet de la configuration requise.
* Vérifiez également que la fonctionnalité Hyper-V a été activée sur votre système.

## <a name="deploying-apps-to-the-hololens-emulator"></a>Déploiement d’applications sur l’émulateur HoloLens

1. Charger votre solution d’application dans Visual Studio 2015.
    >[!NOTE]
    >Lorsque vous utilisez Unity, générez votre projet à partir de Unity et puis chargez la solution créée dans Visual Studio comme d’habitude.
2. Vérifiez la plateforme est définie sur **x86**.
3. Sélectionnez le **HoloLens émulateur** en tant que l’appareil cible pour le débogage.
4. Accédez à **Déboguer > Démarrer le débogage** ou appuyez sur **F5** pour lancer l’émulateur et de déployer votre application pour le débogage.

L’émulateur peut prendre une minute ou plus pour démarrer lors du premier démarrage. Nous vous recommandons de conserver l’émulateur ouvert pendant votre session de débogage afin de déployer rapidement des applications à l’émulateur en cours d’exécution.

## <a name="basic-emulator-input"></a>Entrée de l’émulateur de base

Contrôle de l’émulateur est très similaire à de nombreux de jeux vidéo 3D courantes. Options d’entrée sont disponibles à l’aide du clavier, souris ou manette Xbox. Vous contrôlez l’émulateur en dirigeant les actions d’un utilisateur simulé a porter un HoloLens. Vos actions déplacement que l’utilisateur simulé autour et les applications qui s’exécutent dans l’émulateur répondent comme ils le feraient sur un appareil réel.
* **Remonter vers l’avant, arrière, gauche et avec le bouton droit** -utiliser le W, A, S et D clés sur votre clavier ou la clé gauche sur une manette Xbox.
* **Rechercher, vers le bas, gauche et avec le bouton droit** -cliquez et faites glisser la souris, utilisez les touches de direction sur votre clavier ou la clé droite sur une manette Xbox.
* **Geste d’appui en l’air** - avec le bouton droit de la souris, appuyez sur la touche entrée de votre clavier ou utilisez le bouton A sur un contrôleur Xbox.
* **Fleurir mouvement** : appuyez sur la clé de Windows ou la touche F2 du clavier, ou appuyez sur le bouton B sur une manette Xbox.
* **Remettez le déplacement des défilement** : maintenez la touche Alt enfoncée, maintenez le bouton droit de la souris et faites glisser la souris haut / bas, ou dans une manette Xbox maintenez le déclencheur de droite et un bouton et la clé droite haut et bas.

## <a name="anatomy-of-the-hololens-emulator"></a>Anatomie de l’émulateur HoloLens

### <a name="main-window"></a>Fenêtre principale

Quand l’émulateur démarre, vous verrez une fenêtre qui affiche le système d’exploitation HoloLens.

![Fenêtre principale de l’émulateur HoloLens](images/emulator-890px.png)

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

![Volet de HoloLens émulateur « Outils supplémentaires »](images/emulator-simulation-500px.png)

L’onglet de la Simulation affiche l’état actuel des capteurs simulés utilisé pour piloter le système d’exploitation de HoloLens au sein de l’émulateur. Vous placez le curseur sur n’importe quelle valeur dans l’onglet Simulation fournira une info-bulle qui décrit comment contrôler cette valeur.

### <a name="room-tab"></a>Onglet espace

L’émulateur simule entrée world sous la forme de la maille de mappage spatial de simulé « locaux ». Cet onglet vous permet de choisir quels salle à charger au lieu de la salle par défaut.

![Onglet de « Locaux » émulateur HoloLens](images/emulator-room-500px.png)

Salles simulées sont utiles pour tester votre application dans plusieurs environnements. Plusieurs pièces sont fournis avec l’émulateur et une fois que vous installez l’émulation, vous les trouverez dans % ProgramFiles(x86) %\Program fichiers (x86) \Microsoft XDE\10.0.11082.0\Plugins\Rooms. Toutes ces locaux ont été capturés dans des environnements réels à l’aide d’un HoloLens :
* **DefaultRoom.xef** -un petite salon grâce à un téléviseur, art et deux canapés. Chargé par défaut lorsque vous démarrez l’émulateur.
* **Bedroom1.xef** -petite votre chambre avec un support.
* **Bedroom2.xef** -votre chambre avec un banc de taille Dame, buffet, nightstands et walk-in placard.
* **GreatRoom.xef** -une salle de très grand espace ouvert avec salon, à manger table et cuisine.
* **LivingRoom.xef** : un salon grâce à un foyer, canapé, CANAPES, ainsi qu’une table de café avec un vase.

Vous pouvez également enregistrer vos propres locaux à utiliser dans l’émulateur à l’aide de la page de Simulation de la [Windows Device Portal](using-the-windows-device-portal.md) sur votre HoloLens.

Sur l’émulateur, vous verrez seulement hologrammes que vous effectuez le rendu et vous ne verrez pas la salle simulée derrière les hologrammes. Ceci est le véritable HoloLens là où se trouve à la fois à la différence fusionnée ensemble. Si vous souhaitez voir la salle simulée dans l’émulateur de HoloLens, vous devez mettre à jour votre application pour afficher le maillage de mappage spatial dans la scène.

### <a name="account-tab"></a>Onglet Compte

L’onglet compte permet de configurer l’émulateur pour se connecter avec un Account de Microsoft. Cela est utile pour tester les API qui oblige l’utilisateur à être connecté avec un compte. Après avoir vérifié la zone sur cette page, les lancements suivants de l’émulateur vous demande de connexion, comme le ferait un utilisateur la première fois le HoloLens est démarré.

## <a name="see-also"></a>Voir aussi
* [Entrée avancée d’émulateur de HoloLens et simulateur de réalité mixte](advanced-hololens-emulator-and-mixed-reality-simulator-input.md)
* [Historique de logiciel émulateur HoloLens](hololens-emulator-archive.md)
* [Mappage spatial dans Unity](spatial-mapping-in-unity.md)
* [Mappage spatial dans DirectX](spatial-mapping-in-directx.md)
