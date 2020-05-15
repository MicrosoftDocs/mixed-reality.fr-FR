---
title: 3. Configuration de votre projet pour la réalité mixte
description: Partie 3 d’un tutoriel pour créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools du Mixed Reality Toolkit
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: b5b5e2de787279602341e60f2bfa29aa05ea9b31
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840618"
---
# <a name="3-setting-up-your-project-for-mixed-reality"></a>3. Configuration de votre projet pour la réalité mixte

Cette section vous guide pas à pas tout au long du processus de configuration de votre application pour le développement de la réalité mixte. 

## <a name="objectives"></a>Objectifs

* Comprendre comment configurer un projet de réalité mixte avec ARSessionConfig, Pawn et GameMode

## <a name="configure-the-session"></a>Configurer la session

1. Dans le navigateur de contenu, revenez au dossier **Content**. Cliquez sur **Add New > Miscellaneous > Data Asset**. 

2. Sélectionnez la classe **ARSessionConfig**, puis cliquez sur **Select**. Nommez la ressource « ARSessionConfig ».

![Créer une ressource de données](images/unreal-uxt/3-createasset.PNG)

3. Double-cliquez sur la ressource ARSessionConfig pour l’ouvrir. Une ressource de données ARSessionConfig contient divers paramètres AR utiles, notamment pour le mappage spatial et l’occlusion. Pour plus d’informations sur ARSessionConfig, consultez [UARSessionConfig](https://docs.unrealengine.com/en-US/API/Runtime/AugmentedReality/UARSessionConfig/index.html) dans la documentation Unreal Engine. Pour notre application de jeu d’échecs, nous n’avons pas besoin de modifier les paramètres. Sélectionnez simplement **Save** et revenez dans la fenêtre principale. 

![Configuration de la session AR](images/unreal-uxt/3-arsessionconfig.PNG)

4. Dans la barre d’outils au-dessus de la fenêtre Viewport, cliquez sur **Blueprints > Open Level Blueprint**. Level Blueprint est un Blueprint spécial qui a le rôle de graphe d'événements (« Event Graph ») global à l’échelle du niveau. Nous allons démarrer une session AR ici pour que sa configuration soit appliquée au début du niveau.  

5. Faites glisser le nœud d’exécution en dehors de **Event BeginPlay** et relâchez-le. Recherchez le nœud **Start AR Session**. Cliquez sur **Session Config** et sélectionnez votre nouvelle ressource **ARSessionConfig**. Sélectionnez **Compile**, puis **Save**. Revenez dans la fenêtre principale.

![Démarrer la session AR](images/unreal-uxt/3-startarsession.PNG)

## <a name="create-a-pawn"></a>Créer un Pawn

1.  Dans le dossier Content, créez un Blueprint qui hérite de **DefaultPawn**. Dans Unreal, un Pawn est la représentation de l’utilisateur dans le jeu ou, ici, de l’expérience HoloLens 2. Renommez votre nouveau Pawn en « MRPawn » et double-cliquez sur MRPawn pour l’ouvrir. 

![Créer un Pawn héritant de DefaultPawn](images/unreal-uxt/3-defaultpawn.PNG)

2.  Par défaut, le Pawn a un composant de maillage et un composant de collision ; dans la plupart des projets Unreal, les Pawns contrôlés par l’utilisateur sont des objets solides qui entrent en collision avec d’autres composants. Dans ce cas, étant donné que l’utilisateur est le Pawn, nous souhaitons pouvoir transférer des hologrammes sans générer de collisions. Dans le panneau Components, sélectionnez **CollisionComponent**. Dans le volet Details, faites défiler le contenu jusqu’à la section Collision, puis cliquez sur la liste déroulante à côté de Collision Presets. Sélectionnez **NoCollision** à la place de Pawn. Répétez cette opération pour **MeshComponent**. Sélectionnez **Compile** et **Save** pour compiler et enregistrer le Blueprint. Revenez dans la fenêtre principale. 

![Changer la valeur Pawn dans Collision Presets](images/unreal-uxt/3-nocollision.PNG)

## <a name="create-a-game-mode"></a>Créer un mode de jeu

1.  Dans le dossier Content du navigateur de contenu, créez un Blueprint avec le parent **Game Mode Base**. Nommez le Blueprint « MRGameMode » et double-cliquez dessus pour l’ouvrir. Dans Unreal, le mode de jeu (Game Mode) définit plusieurs paramètres du jeu ou de l’expérience, y compris le Pawn par défaut à utiliser. 

![MRGameMode dans le navigateur de contenu](images/unreal-uxt/3-gamemode.PNG)

2.  Dans le volet Details, recherchez la section Classes. Pour l’option Default Pawn Class, changez DefaultPawn par le **MRPawn** que vous venez de créer. Sélectionnez **Compile**, puis **Save**. Revenez dans la fenêtre principale. 

![Définir l’option Default Pawn Class](images/unreal-uxt/3-setpawn.PNG)

3.  La dernière étape de la configuration de votre projet consiste à indiquer à Unreal d’utiliser MRGameMode comme mode de jeu par défaut. Accédez à la section **Edit > Projects Settings > Maps & Modes** (dans Projects). Dans la section Default Modes, cliquez sur la liste déroulante et choisissez **MRGameMode**. Dans la section Default Maps juste en dessous, changez **EditorStartupMap** et **GameDefaultMap** à **Main**. De cette façon, quand vous fermez l’éditeur et le rouvrez, la carte principale (Main) est sélectionnée par défaut. De même, lorsque vous jouez, la carte principale est le niveau de démarrage. 

![Project Settings - Maps & Modes](images/unreal-uxt/3-mapsandmodes.PNG)

[Section suivante : 4. Rendre votre scène interactive](unreal-uxt-ch4.md)