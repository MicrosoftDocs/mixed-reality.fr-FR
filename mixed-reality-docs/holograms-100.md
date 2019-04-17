---
title: Principes de base MR 100 - mise en route avec Unity
description: Apprenez à créer votre première application « hello world » de base de réalité mixte.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: mixte réalité, Windows Mixed Reality, HoloLens, immersive, vr, mr, prise en main, HOLOGRAMME, academy, didacticiel
ms.openlocfilehash: 1f4a5490383671fba694b386015ff6742d37241b
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593250"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-basics-100-getting-started-with-unity"></a>Principes de base MR 100 : Mise en route avec Unity

Ce didacticiel vous guidera dans la création d’une application de base de réalité mixte créée avec Unity.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>Principes de base MR 100 : Mise en route avec Unity</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).

## <a name="chapter-1---create-a-new-project"></a>Chapitre 1 - créer un nouveau projet

>[!VIDEO https://www.youtube.com/embed/2L5IFO0hnYA]

Pour créer une application avec Unity, vous devez d’abord créer un projet. Ce projet est organisé en plusieurs dossiers, le plus important est votre dossier de ressources. C’est le dossier qui conserve tous les composants que vous importez à partir des outils de création de contenus numériques telles que Maya, Max cinéma 4D ou Photoshop, tout code que vous créez avec Visual Studio ou votre éditeur de code favori, et n’importe quel nombre de fichiers de contenu que Unity crée en tant que vous composez des scènes , animations et autres types de ressource de Unity dans l’éditeur.

Pour générer et déployer des applications UWP, Unity peut exporter le projet comme une solution Visual Studio qui contiendra toutes les ressources nécessaires et les fichiers de code.

1. Démarrer Unity
2. Sélectionnez **nouveau**
3. Entrez un nom de projet (par exemple) "MixedRealityIntroduction")
4. Entrez un emplacement pour enregistrer votre projet
5. Vérifiez le **3D** bascule est sélectionné.
6. Sélectionnez **créer un projet**

Félicitations, vous êtes tous le programme d’installation pour commencer à utiliser vos personnalisations de réalité mixte maintenant.

## <a name="chapter-2---setup-the-camera"></a>Chapitre 2 - programme d’installation de l’appareil photo

>[!VIDEO https://www.youtube.com/embed/eP1ZwB4wSNA]

La caméra principale Unity gère la tête de suivi et rendu stéréoscopique. Il existe quelques modifications à apporter à la caméra principale à utiliser avec la réalité mixte.
1. Sélectionnez Fichier > nouvelle scène

Tout d’abord, il sera plus facile de créer votre application si vous imaginez la position de départ de l’utilisateur en tant que (**X**: 0, **Y**: 0, **Z**: 0). Étant donné que la caméra principale effectue le suivi des mouvements de tête de l’utilisateur, vous pouvez définir la position de départ de l’utilisateur en définissant la position de départ de la caméra principale.
1. Sélectionnez **Main Camera** dans le **hiérarchie** Panneau de configuration
2. Dans le **inspecteur** panneau, recherchez le **transformer** composant et modifier le **Position** à partir de (**X**: 0, **Y**: 1, **Z**: -10) à (**X**: 0, **Y**: 0, **Z**: 0)

Deuxièmement, l’arrière-plan de caméra par défaut doit réflexion.

**Pour les applications de HoloLens**, le monde réel doit apparaître tout ce que l’appareil photo est restitué, pas une texture Skybox.
1. Avec le **Main Camera** toujours sélectionné dans le **hiérarchie** panneau, recherchez le **caméra** composant dans le **inspecteur** panneau et modifier le **Effacer les indicateurs** liste déroulante à partir de **Skybox** à **couleur unie**.
2. Sélectionnez le **arrière-plan** sélecteur de couleurs et de modifier le **RGBA** valeurs (0, 0, 0, 0)

**Pour les applications de réalité mixte ciblées pour des casques IMMERSIFS**, nous pouvons utiliser la texture Skybox par défaut qui fournit de Unity.
1. Avec le **Main Camera** toujours sélectionné dans le **hiérarchie** panneau, recherchez le **caméra** composant dans le **inspecteur** panneau et conserver la **Effacer les indicateurs** menu déroulant pour **Skybox**.

Troisièmement, nous prendre en compte la rapprochée clip dans Unity et objets inaccessibles affiché trop près aux utilisateurs yeux comme un utilisateur proche d’un objet ou un objet est proche d’un utilisateur.

**Pour les applications de HoloLens**, du plan de clip proche peut être défini sur le [HoloLens recommandé](camera-in-unity.md#clip-planes) 0.85 mètres.
1. Avec le **Main Camera** toujours sélectionné dans le **hiérarchie** panneau, recherchez le **caméra** composant dans le **inspecteur** panneau et modifier le **Près du plan de découpage** champ à partir de la valeur par défaut **0.3** à la HoloLens recommandé **0,85**.

**Pour les applications de réalité mixte ciblées pour des casques IMMERSIFS**, nous pouvons utiliser le paramètre par défaut qui fournit de Unity.
1. Avec le **Main Camera** toujours sélectionné dans le **hiérarchie** panneau, recherchez le **caméra** composant dans le **inspecteur** panneau et conserver la **Près du plan de découpage** champ à la valeur par défaut **0.3**.

Enfin, nous enregistrer notre progression jusqu'à présent. Pour enregistrer les modifications de la scène, sélectionnez **fichier > Enregistrer la scène sous**, nommez la scène **Main**, puis sélectionnez **enregistrer**.

## <a name="chapter-3---setup-the-project-settings"></a>Chapitre 3 - le programme d’installation les paramètres du projet

>[!VIDEO https://www.youtube.com/embed/ItRoiXccC0g]

Dans ce chapitre, nous allons définir certains paramètres de projet Unity qui nous aident à cible le Windows HOLOGRAPHIQUE Kit de développement logiciel pour le développement. Nous allons également définir certains paramètres de qualité pour notre application. Enfin, nous nous assurons que notre cibles de génération sont définies sur le Windows Store.

### <a name="unity-performance-and-quality-settings"></a>Paramètres de performances et la qualité de Unity

**Paramètres de qualité de Unity pour HoloLens**

![Paramètres de qualité de Unity pour HoloLens](images/qualitysettings.png) 

Dans la mesure où il est si important de maintenir une haute fréquence d’images sur HoloLens, nous voulons les paramètres de qualité adaptées à de meilleures performances. Pour plus d’informations sur les performances, [recommandations relatives aux performances pour Unity](performance-recommendations-for-unity.md).
1. Sélectionnez **Modifier > Paramètres du projet > qualité**
2. Sélectionnez le **déroulante** sous le **Windows Store** logo, puis sélectionnez **très faible**. Vous saurez que le paramètre est appliqué correctement lorsque la case dans la colonne du Windows Store et de la ligne le plus rapide est vert.

**Pour les applications de réalité mixte ciblées à affiche un vaisseau**, vous pouvez laisser les paramètres de qualité à ses valeurs par défaut.

### <a name="target-windows-10-sdk"></a>Cibler Windows 10 SDK

**Kit de développement logiciel cible Windows HOLOGRAPHIQUE**

![Kit de développement logiciel cible Windows HOLOGRAPHIQUE](images/xrsettings.png) 

Nous devons informer Unity que l’application que nous tentons de les exporter doit créer un [vue immersive](app-views.md) au lieu d’une vue en 2D. Nous cela en activant la prise en charge de réalité virtuelle sur Unity ciblant le SDK Windows 10.
1. Accédez à **Modifier > Paramètres du projet > Lecteur**.
2. Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez le **Windows Store** icône.
3. Développez le **XR paramètres** groupe.
4. Dans le **rendu** section, vérifiez le **virtuel pris en charge de réalité** case à cocher pour ajouter un nouveau **SDK de réalité virtuelle** liste.
5. Vérifiez que **Windows Mixed Reality** apparaît dans la liste. Dans le cas contraire, sélectionnez le **+** bouton en bas de la liste et choisissez **Windows Mixed Reality**.

>[!NOTE]
>Si vous ne voyez pas le **Windows Store** icône, vérifiez par deux fois pour vous assurer que vous avez sélectionné le Windows Store de script serveur principal .NET avant l’installation. Si ce n’est pas le cas, vous devrez peut-être réinstaller Unity lors de l’installation correcte de Windows.

**Vérifier la Configuration de .NET**

![Vérifier la Configuration de .NET](images/configoptions-375px.png)

1. Accédez à **Modifier > Paramètres du projet > Lecteur** (que vous deviez toujours cette à partir de l’étape précédente).
2. Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez le **Windows Store** icône.
3. Dans le **autres paramètres** Configuration section, assurez-vous que l’option **Backend Scripting** a la valeur **.NET**

Joli travail sur l’obtention de tous les paramètres de projet appliquées. Ensuite, ajoutons un hologramme !

## <a name="chapter-4---create-a-cube"></a>Chapitre 4 - créer un cube

>[!VIDEO https://www.youtube.com/embed/qKcK1Yuj-HQ]

Création d’un cube dans votre projet Unity s’apparente à la création de n’importe quel autre objet dans Unity. Il est facile de placer un cube devant l’utilisateur, car le système de coordonnées d’Unity est mappé à la réalité - où un compteur dans Unity est environ un compteur dans le monde réel.
1. Dans le coin supérieur gauche de la **hiérarchie** Panneau de configuration, sélectionnez le **créer** liste déroulante et choisissez **objet 3D > Cube**.
2. Sélectionnez nouvellement créé **Cube** dans le **hiérarchie** Panneau de configuration
3. Dans le **inspecteur** trouver la **transformer** composant et modification **Position** à (**X**: 0, **Y**: 0, **Z**: 2). *Cela positionne des 2 mesures du cube devant la position de départ de l’utilisateur.*
4. Dans le **transformer** composant, modification **Rotation** à (**X**: 45, **Y**: 45, **Z**: 45) et modifiez **mise à l’échelle** à (**X**: 0,25, **Y**: 0,25, **Z**: 0.25). *Cela permet de dimensionner le cube à 0,25 mètres.*
5. Pour enregistrer les modifications de la scène, sélectionnez **fichier > Enregistrer la scène**.

## <a name="chapter-5---verify-on-device-from-unity-editor"></a>Chapitre 5 - vérifier sur l’appareil à partir de l’éditeur Unity

>[!VIDEO https://www.youtube.com/embed/vmCfiIdRb6Q]

Maintenant que nous avons créé notre cube, il est temps de faire une vérification rapide dans l’appareil. Vous pouvez faire cela directement à partir de l’éditeur Unity.

### <a name="initial-setup"></a>Programme d’installation initiale
1. Sur votre PC, de développement dans Unity, ouvrez **fichier > Paramètres de Build** fenêtre.
2. Modification **plateforme** à **plateforme Windows universelle** et cliquez sur **résidants de commutateur**

### <a name="for-hololens-use-unity-remoting"></a>Pour une utilisation HoloLens Unity Remoting
1. Sur votre HoloLens, installer et exécuter le [HOLOGRAPHIQUE Player de communication à distance](holographic-remoting-player.md), disponible depuis le Windows Store. Lancez l’application sur l’appareil, et il entre dans un état d’attente et affichent l’adresse IP de l’appareil. Notez l’adresse IP.
2. Ouvrez **fenêtre > XR > émulation HOLOGRAPHIQUE**.
3. Modification **Mode d’émulation** de **aucun** à **à distance à l’appareil**.
4. Dans **Machine distante**, entrez l’adresse IP de votre HoloLens indiqué précédemment.
5. Cliquer sur **Se connecter**.
6. Vérifiez le **état de la connexion** vert **connecté**.
7. Maintenant que vous pouvez maintenant cliquer **lire** dans l’éditeur Unity.

Vous serez maintenant en mesure de voir le cube dans l’appareil et dans l’éditeur. Vous pouvez suspendre, inspecter les objets et déboguer comme vous exécutez une application dans l’éditeur, car il s’agit essentiellement ce qui se passe, mais avec vidéo, audio et entrée de périphérique transmises dans les deux sens entre le réseau entre l’ordinateur hôte et de l’appareil.

### <a name="for-other-mixed-reality-supported-headsets"></a>Pour les autres réalité mixte les casques de prise en charge

1. Connectez le casque à votre PC à l’aide du câble USB et le câble HDMI de développement ou afficher des câbles de port.
2. Lancer le **Portal de réalité mixte** et vérifiez que vous avez terminé la première utilisation.
3. À partir d’Unity, vous pouvez maintenant appuyer sur le bouton de lecture.

Vous serez maintenant en mesure de voir le rendu de cube dans votre casque de réalité mixte et dans l’éditeur.

## <a name="chapter-6---build-and-deploy-to-device-from-visual-studio"></a>Chapitre 6 - générer et déployer sur les appareils à partir de Visual Studio

>[!VIDEO https://www.youtube.com/embed/USSu8yHUdbk]

Nous sommes maintenant prêts à compiler notre projet dans Visual Studio et déployer avec le périphérique cible.

### <a name="export-to-the-visual-studio-solution"></a>Exporter vers la solution Visual Studio
1.  Ouvrez **fichier > Paramètres de Build** fenêtre.
2.  Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.
3.  Modification **plateforme** à **plateforme Windows universelle** et cliquez sur **plateforme de commutation**.
4.  Dans **Windows Store** paramètres garantissent, **SDK** est **10 universelle**.
5.  Pour l’appareil cible, laissez à **n’importe quel appareil** pour affiche un vaisseau ou basculer vers **HoloLens**.
6.  **Type de Build UWP** doit être **D3D**.
7.  **SDK UWP** peuvent être laissées à **dernière installé**.
8.  Vérifiez **Unity C# projets** en mode de débogage.
9.  Cliquez sur **Build**.
10. Dans l’Explorateur de fichiers, cliquez sur **nouveau dossier** et nommez le dossier **« Application »**.
11. Avec le **application** dossier sélectionné, cliquez sur le **sélectionner le dossier** bouton.
12. Quand Unity est terminé, création d’une fenêtre d’Explorateur de fichiers Windows s’affiche.
13. Ouvrez le **application** dossier dans l’Explorateur de fichiers.
14. Ouvrez la solution Visual Studio générée (MixedRealityIntroduction.sln dans cet exemple)

### <a name="compile-the-visual-studio-solution"></a>Compilez la solution Visual Studio

Enfin, nous compilez la solution Visual Studio exportée, déployer et testez-la sur l’appareil.
1. À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible à partir de **déboguer** à **version** et à partir de **ARM** à **X86**.

Les instructions diffèrent pour le déploiement sur un appareil par rapport à l’émulateur. Suivez les instructions qui correspondent à votre configuration.

### <a name="deploy-to-mixed-reality-device-over-wi-fi"></a>Déployer sur des appareils de réalité mixte par Wi-Fi
1. Cliquez sur la flèche à côté du **ordinateur Local** bouton et changer la cible de déploiement à **Machine distante**.
2. Entrez l’adresse IP de votre appareil de réalité mixte et modifier **Mode d’authentification** universelles (protocole non chiffré) pour HoloLens et **Windows** pour d’autres appareils.
3. Cliquez sur **Déboguer > Démarrer sans débogage**.

**Pour HoloLens**, s’il s’agit du premier déploiement sur votre appareil, vous devrez paire [à l’aide de Visual Studio](using-visual-studio.md).

### <a name="deploy-to-mixed-reality-device-over-usb"></a>Déployer sur des appareils de réalité mixte via USB

Vérifiez que votre appareil est branché via le câble USB.
1. **Pour HoloLens**, cliquez sur la flèche à côté du **ordinateur Local** bouton et changer la cible de déploiement à **appareil**.
2. **Pour cibler un vaisseau périphériques connectés à votre PC**, conserver le paramètre à l’ordinateur Local. Assurez-vous d’avoir le **Portal de réalité mixte** en cours d’exécution.
3. Cliquez sur **Déboguer > Démarrer sans débogage**.

### <a name="deploy-to-emulator"></a>Déployer à l’émulateur
1. Cliquez sur la flèche à côté du **appareil** bouton et à partir de la liste déroulante Sélectionnez **HoloLens émulateur**.
2. Cliquez sur **Déboguer > Démarrer sans débogage**.

### <a name="try-out-your-app"></a>Tester votre application

Maintenant que votre application est déployée, essayez de déplacer tout autour du cube et observez qu’elle reste dans le monde devant vous.

## <a name="see-also"></a>Voir aussi
* [Vue d’ensemble du développement Unity](unity-development-overview.md)
* [Meilleures pratiques pour travailler avec Unity et Visual Studio](best-practices-for-working-with-unity-and-visual-studio.md)
* [Principes de base MR 101](holograms-101.md)
* [Principes de base MR 101E](holograms-101e.md)
