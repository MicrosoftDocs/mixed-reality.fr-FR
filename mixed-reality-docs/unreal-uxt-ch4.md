---
title: 4. Rendre votre scène interactive
description: Partie 4 d’un tutoriel pour créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools de Mixed Reality Toolkit
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: 2e4d26ed4e0b8199bfc629016aea688bd1c41ef8
ms.sourcegitcommit: 09d9fa153cd9072f60e33a5f83ced8167496fcd7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/18/2020
ms.locfileid: "83520024"
---
# <a name="4-making-your-scene-interactive"></a>4. Rendre votre scène interactive

Cette section présente le plug-in open source UX Tools de Mixed Reality Toolkit, qui fournit un ensemble d’outils permettant de rendre facilement votre scène interactive. À la fin de cette section, les pièces de votre jeu d’échecs répondront aux entrées utilisateur. 

## <a name="objectives"></a>Objectifs

* Inclure le plug-in UX Tools de Mixed Reality Toolkit dans votre projet
* Ajoutez des acteurs d’interaction manuelle à vos doigts
* Créer et attacher des manipulateurs à votre échiquier et à vos pièces 
* Utiliser la simulation d’entrée pour valider votre projet

## <a name="download-the-mixed-reality-toolkit-ux-tools-plugin"></a>Télécharger le plug-in UX Tools de Mixed Reality Toolkit

1.  Clonez ou téléchargez et décompressez la dernière version du plug-in UX Tools de MRTK à partir du [dépôt GitHub UX Tools](https://github.com/microsoft/MixedReality-UXTools-Unreal/releases)

2.  Dans le dossier racine de votre projet de jeu d’échecs, créez un dossier appelé « Plugins ». Copiez le plug-in UX Tools décompressé dans ce dossier. Redémarrez l’éditeur Unreal. 

![Créer un dossier de plug-ins de projet](images/unreal-uxt/4-plugins.PNG)

3.  Après le redémarrage, si vous ne voyez pas le contenu du plug-in UX Tools dans le panneau de vos sources, il peut être nécessaire de cliquer sur **View Options > Show Plugin Content**. Vous verrez que le plug-in UX Tools fournit un dossier de contenu avec des pointeurs, une simulation d’entrée et un bouton simple ainsi qu’un dossier de classes C++ avec des sous-dossiers distincts selon les fonctions.  

![Montrer le contenu du plug-in](images/unreal-uxt/4-showplugincontent.PNG)

## <a name="spawn-hand-interaction-actors"></a>Générer des acteurs d’interaction manuelle

1.  Commençons par générer des acteurs d’interaction manuelle à partir de notre MRPawn, pour 1) pouvoir visualiser MRPawn avec un curseur au bout des index du pion, 2) pouvoir fournir des événements d’entrée manuelle articulée (et donc manipuler directement les acteurs) via le pion et 3) pouvoir fournir des événements d’entrée d’interaction à distance à travers des rayons manuels partant de nos paumes. Ouvrez le blueprint **MRPawn** et accédez à **Event Graph**. 

2.  Faites glisser la broche d’exécution depuis l’événement BeginPlay et relâchez-la pour placer un nouveau nœud. Sélectionnez le nœud **Spawn Actor from Class**. Cliquez sur la liste déroulante en regard de la broche **Class** et recherchez **Uxt Hand Interaction Actor**. Faites glisser la broche d’exécution à partir du nœud SpawnActor Uxt Hand, relâchez-le, puis recherchez la fonction **Set Hand** contenue dans la classe Uxt Hand Interaction Actor. Connectez la valeur de retour du nœud SpawnActor à la broche cible du nœud Set Hand pour définir la main de l’acteur d’interaction manuelle sur **Left**. Générez un deuxième **Acteur d’interaction manuelle Uxt**, en définissant cette fois la main sur **Right**, de sorte que quand l’événement débute, un acteur d’interaction manuelle Uxt soit généré sur chaque main. 

![Générer des acteurs d’interaction manuelle UXT](images/unreal-uxt/4-spawnactor.PNG)

3.  Ensuite, nous devons fournir à nos acteurs d’interaction manuelle Uxt une transformation initiale où faire la génération et un propriétaire. Faites glisser la broche de l’une des broches **Spawn Transform** et relâchez-la pour placer un nouveau nœud. Recherchez le nœud **Make Transform**. La transformation initiale n’a en réalité pas d’importance, car les acteurs d’interaction manuelle vont se placer sur nos mains dès qu’elles sont visibles (du code qui est déjà écrit pour nous dans le plug-in UX Tools) ; sinon, ils disparaissent. Cependant, la fonction SpawnActor nécessite une transformation en entrée pour éviter une erreur du compilateur : nous allons donc simplement conserver les valeurs par défaut dans Make Transform. Faites également glisser la **valeur de retour** de Make Transform sur la transformation de génération d’acteur d’interaction de l’autre main. 

4.  Cliquez sur la **flèche bas** en bas des deux nœuds SpawnActor pour afficher la broche **Owner**. Faites glisser la broche de l’une des broches **Owner** et relâchez-la pour placer un nouveau nœud. Recherchez « self » et sélectionnez la variable **Get a reference to self**. Créez aussi un lien entre le nœud de référence de l’objet Self et la broche Owner de l’acteur d’interaction manuelle. N’hésitez pas à faire glisser les nœuds pour rendre votre blueprint plus lisible. **Compilez**, **enregistrez**, puis revenez à la fenêtre principale. 

![Effectuer la configuration de l’acteur d’interaction manuelle UXT](images/unreal-uxt/4-fingerptrs.PNG)

Pour plus d’informations sur l’acteur d’interaction manuelle fourni dans le plug-in UX Tools de MRTK, consultez la [documentation](https://microsoft.github.io/MixedReality-UXTools-Unreal/version/public/0.8.x/Docs/HandInteraction.html) officielle.

## <a name="attach-manipulators"></a>Attacher des manipulateurs

1.  Nous allons ensuite attacher des manipulateurs à nos acteurs Échiquier et Roi. Un manipulateur est un composant qui répond à une entrée manuelle articulée et qui peut être tiré, pivoté et translaté ; en appliquant la transformation du manipulateur à celle d’un acteur, les acteurs peuvent être manipulés directement. 

2.  Ouvrez le blueprint de l’échiquier. Dans le panneau **Components**, cliquez sur **Add Component** et recherchez **Uxt Generic Manipulator**. Dans le volet d’informations, vous trouverez une section intitulée **Generic Manipulator** où vous pouvez définir si vous voulez activer la manipulation à une ou à deux mains, le mode de rotation et le lissage. N’hésitez pas à sélectionner le mode que vous souhaitez, puis **compilez** et **enregistrez** l’échiquier. 

![Ajouter un manipulateur générique](images/unreal-uxt/4-addmanip.PNG)

![Définir le mode](images/unreal-uxt/4-setrotmode.PNG)

3.  Répétez les étapes ci-dessus pour l’acteur WhiteKing.

Pour plus d’informations sur les composants de manipulateur fournis dans le plug-in UX Tools de MRTK, consultez la [documentation](https://microsoft.github.io/MixedReality-UXTools-Unreal/version/public/0.8.x/Docs/Manipulator.html) officielle.

## <a name="test-out-your-scene-with-simulated-hands"></a>Tester votre scène avec des mains simulées

1.  Dans la fenêtre principale, appuyez sur **Play**. Vous devez voir deux mains maillées fournies par le plug-in UX Tools de MRTK, avec des rayons manuels partant de la paume de chaque main ! 

![Mains simulées dans la fenêtre d’affichage](images/unreal-uxt/4-handsim.PNG)

2.  Pour contrôler la **main droite**, maintenez enfoncé le bouton **Alt gauche**. Déplacez votre souris pour déplacer la main. Faites défiler avec la **roulette de la souris** pour déplacer la main **vers l’avant** ou **vers l’arrière**. Cliquez sur le bouton gauche de la souris pour **pincer**, cliquez sur le bouton central de la souris pour **pousser avec le doigt**.

3.  Pour contrôler la **main gauche**, maintenez enfoncé le bouton **Maj gauche**. Les contrôles permettant de déplacer la main gauche sont les mêmes que ceux de la main droite. 

4.  Essayez à présent d’utiliser les mains simulées pour sélectionner, déplacer et déposer le roi blanc du jeu d’échecs. Vous pouvez également manipuler l’échiquier ! Expérimentez les interactions de près et de loin : quand vos mains sont suffisamment proches pour saisir directement l’échiquier et le roi, le rayon manuel disparaît et est remplacé par un curseur de doigt au bout de l’index. 

Pour plus d’informations sur les fonctionnalités des mains simulées fournies dans le plug-in UX Tools de MRTK, consultez la [documentation](https://microsoft.github.io/MixedReality-UXTools-Unreal/version/public/0.8.x/Docs/InputSimulation.html) officielle.

[Section suivante : 5. Ajout d’un bouton et réinitialisation des emplacements de pièces](unreal-uxt-ch5.md)
