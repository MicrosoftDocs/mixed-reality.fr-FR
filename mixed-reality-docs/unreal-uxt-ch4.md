---
title: 4. Rendre votre scène interactive
description: Quatrième tutoriel d’une série de six visant à créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in Mixed Reality Toolkit UX Tools
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: 62c0ff839718f7fda34bdc7560eae634fa37d44f
ms.sourcegitcommit: 45da0a056fa42088ff81ccdd11232830fbe8430f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84720335"
---
# <a name="4-making-your-scene-interactive"></a>4. Rendre votre scène interactive

## <a name="overview"></a>Vue d’ensemble

Dans le tutoriel précédent, vous avez ajouté une session de réalité augmentée (ARSession), un pion (Pawn) et un mode Jeu (Game Mode) pour finaliser la configuration de réalité mixte de l’application de jeu d’échecs. Cette section se concentre sur l’utilisation du plug-in open source [Mixed Reality Toolkit UX Tools](https://github.com/microsoft/MixedReality-UXTools-Unreal), qui fournit des outils permettant de rendre une scène interactive. À la fin de cette section, vous serez capable de déplacer les pions du jeu d’échecs à l’aide de l’entrée utilisateur. 

## <a name="objectives"></a>Objectifs

* Téléchargement du plug-in Mixed Reality Toolkit UX Tools 
* Ajout d’acteurs d’interaction manuelle à vos doigts
* Création et ajout de manipulateurs aux objets de la scène
* Utilisation de la simulation d’entrée pour valider le projet

## <a name="downloading-the-mrtk-ux-tools-plugin"></a>Téléchargement du plug-in MRTK UX Tools
Avant de commencer à utiliser les entrées d’utilisateur, vous devez ajouter le plug-in au projet.

1.  Clonez ou téléchargez la dernière version du plug-in MRTK UX Tools à partir du [dépôt GitHub](https://github.com/microsoft/MixedReality-UXTools-Unreal/releases), puis décompressez le fichier.

2.  Créez un dossier nommé **Plugins** dans le dossier racine du projet. Copiez le plug-in UXTools que vous avez décompressé dans ce dossier, puis redémarrez l’éditeur Unreal. 

![Créer un dossier de plug-ins de projet](images/unreal-uxt/4-plugins.PNG)

3.  Le plug-in UXTools comprend un dossier Content qui contient des sous-dossiers pour les **pointeurs**, la **simulation d’entrée** et le **bouton simple**, ainsi qu’un dossier pour les classes C++ de chaque fonction.  

> [!NOTE]
> Si vous ne voyez pas la section **UXTools Content** (Contenu UXTools) dans le navigateur de contenu (**Content Browser**), cliquez sur **View Options > Show Plugin Content** (Afficher les options > Afficher le contenu du plug-in). 

![Montrer le contenu du plug-in](images/unreal-uxt/4-showplugincontent.PNG)

Une fois le plug-in installé de façon sécurisée, vous pouvez commencer à utiliser les outils qu’il propose, en commençant par les acteurs d’interaction manuelle.

## <a name="spawning-hand-interaction-actors"></a>Génération d’acteurs d’interaction manuelle
L’interaction manuelle avec les éléments de l’expérience utilisateur se fait à l’aide d’acteurs d’interaction manuelle qui créent et dirigent les pointeurs et les visuels, pour les interactions proches et lointaines.
- Les *interactions proches* sont effectuées en pinçant des éléments entre le pouce et l’index, ou en les poussant du bout du doigt. 
- Les *interactions lointaines* sont effectuées en pointant le rayon émanant de la main virtuelle sur un élément, et en appuyant simultanément avec l’index et le pouce.

Dans le cas présent, l’ajout d’un acteur d’interaction manuelle à **MRPawn** va :
- Ajouter un curseur au bout de l’index du pion (Pawn)
- Fournir des événements d’entrées manuelles articulées qui peuvent être manipulés par le pion
- Autoriser les événements d’entrées d’interactions lointaines effectuées à l’aide des rayons qui émanent de la paume de la main virtuelle

Pour bien assimiler ces concepts, nous vous invitons à consulter la [documentation](https://github.com/microsoft/MixedReality-UXTools-Unreal/blob/public/0.8.x/Docs/HandInteraction.md) concernant les interactions manuelles avant de poursuivre. 

Lorsque vous êtes prêt, ouvrez le blueprint **MRPawn** et accédez à **Event Graph**. 

1. Faites glisser puis relâchez la broche d’exécution à partir de **Event BeginPlay** pour placer un nouveau nœud. 
    * Sélectionnez **Spawn Actor from Class** (Générer un acteur à partir d’une classe), cliquez sur la liste déroulante à côté de la broche **Class**, puis recherchez **Uxt Hand Interaction Actor**. 

2. Faites glisser et relâchez la broche d’exécution à partir du nœud **SpawnActor Uxt Hand Interaction**, puis recherchez la fonction**Set Hand** contenue dans la classe **Uxt Hand Interaction Actor**. 
    * Connectez la valeur de retour (**Return Value**) du nœud **SpawnActor** à la broche cible (**Target**) du nœud **Set Hand** (Configurer la main). Cela sélectionne la main gauche (**Left**) pour l’acteur d’interaction manuelle. 

3. Générez un deuxième **Uxt Hand Interaction Actor**, mais cette fois-ci, choisissez la main droite (**Right**). Lorsque l’événement démarre, un acteur d’interaction manuelle Uxt est généré pour chaque main. 

Votre graphe d’événements (**Event Graph**) doit correspondre à la capture d’écran suivante :

![Générer des acteurs d’interaction manuelle UXT](images/unreal-uxt/4-spawnactor.PNG)

Les deux acteurs d’interaction manuelle Uxt ont besoin de propriétaires et d’emplacements de transformation initiale. La transformation initiale n’a pas d’importance dans la mesure où les acteurs d’interaction manuelle utiliseront les mains virtuelles dès qu’elles seront visibles (ce comportement est inclus dans le plug-in UX Tools). Toutefois, la fonction `SpawnActor` nécessite une entrée de transformation pour éviter une erreur du compilateur. Vous devez donc utiliser les valeurs par défaut. 

1. Faites glisser puis relâchez la broche de l’une des broches **Spawn Transform** pour placer un nouveau nœud. 
    * Recherchez le nœud **Make Transform** (Effectuer une transformation), puis faites glisser la valeur de retour (**Return Value**) vers le **Spawn Transform** de l’autre main, afin que les deux nœuds **SpawnActor** soient connectés. 

3.  Cliquez sur la **flèche bas** située en bas des deux nœuds **SpawnActor** pour afficher la broche **Owner**.    
    * Faites glisser la broche de l’une des broches **Owner** et relâchez-la pour placer un nouveau nœud. 
    * Recherchez **self**, puis sélectionnez la variable **Get a reference to self**. Ensuite, créez un lien entre le nœud de référence de l’objet **Self** et la broche **Owner** de l’acteur d’interaction de l’autre main. 
    * **Compilez**, **enregistrez**, puis revenez à la fenêtre principale. 

Vérifiez que les connexions correspondent à la capture d’écran suivante. Toutefois, n’hésitez pas à déplacer les nœuds pour rendre votre blueprint plus lisible.

![Effectuer la configuration de l’acteur d’interaction manuelle UXT](images/unreal-uxt/4-fingerptrs.PNG) 

Pour plus d’informations sur l’acteur d’interaction manuelle fourni dans le plug-in UX Tools de MRTK, consultez la [documentation](https://microsoft.github.io/MixedReality-UXTools-Unreal/version/public/0.8.x/Docs/HandInteraction.html).

À présent, les mains virtuelles du projet disposent d’un moyen pour sélectionner des objets. Toutefois, elles ne peuvent toujours pas les manipuler. Avant de tester l’application, la dernière tâche consiste à ajouter des composants Manipulateur aux acteurs de la scène.

## <a name="attaching-manipulators"></a>Ajout de manipulateurs

Un manipulateur est un composant qui répond à une entrée manuelle articulée. Il peut s’agir d’une saisie, d’une rotation ou d’une translation. L’application de la transformation du manipulateur à une transformation d’acteur permet une manipulation directe de l’acteur. 

1. Dans le blueprint **Board**, cliquez sur **Add Component** (Ajouter un composant), puis recherchez **Uxt Generic Manipulator**. dans le panneau **Components**.

![Ajouter un manipulateur générique](images/unreal-uxt/4-addmanip.PNG)

2. Développez la section **Generic Manipulator** (Manipulateur générique) dans le panneau **Details**. Vous pouvez définir une manipulation à une ou à deux mains, le mode de rotation, ainsi que l’adoucissage. N’hésitez pas à sélectionner le mode que vous souhaitez, puis **compilez** et **enregistrez** l’échiquier. 

![Définir le mode](images/unreal-uxt/4-setrotmode.PNG)

3. Répétez les étapes ci-dessus pour l’acteur **WhiteKing**.

Pour plus d’informations sur les composants Manipulateur qui sont fournis dans le plug-in UX Tools de MRTK, consultez la [documentation](https://microsoft.github.io/MixedReality-UXTools-Unreal/version/public/0.8.x/Docs/Manipulator.html).

## <a name="testing-the-scene"></a>Test de la scène
Bonne nouvelle ! Vous êtes prêt à tester l’application avec ses nouvelles mains virtuelles et vos entrées utilisateur. Appuyez sur **Play** dans la fenêtre principale. Vous devez voir deux mains maillées fournies par le plug-in UX Tools de MRTK, avec des rayons émanant de la paume de chaque main. Vous pouvez contrôler les mains et leurs interactions de la façon suivante :
- Maintenez enfoncée la touche **Alt de gauche** pour contrôler la **main gauche**, et la touche **Maj de gauche** pour contrôler la **main droite**. 
- Déplacez votre souris pour bouger la main, puis faites défiler avec la **roulette de la souris** pour déplacer la main **vers l’avant** ou **vers l’arrière**. 
- Cliquez sur le bouton gauche de la souris pour **pincer**, et cliquez sur le bouton central de la souris pour **pousser avec le doigt**. 

![Mains simulées dans la fenêtre d’affichage](images/unreal-uxt/4-handsim.PNG)

Essayez à présent d’utiliser les mains simulées pour sélectionner, déplacer et déposer le roi blanc du jeu d’échecs et manipuler l’échiquier. Expérimentez les interactions de près et de loin : quand vos mains sont suffisamment proches pour saisir directement l’échiquier et le roi, le rayon émanant de la main disparaît et est remplacé par un curseur au bout de l’index. 

Pour plus d’informations sur les fonctionnalités des mains simulées fournies dans le plug-in UX Tools de MRTK, consultez la [documentation](https://microsoft.github.io/MixedReality-UXTools-Unreal/version/public/0.8.x/Docs/InputSimulation.html).

Maintenant que vos mains virtuelles peuvent interagir avec les objets, vous êtes prêt à passer au tutoriel suivant pour ajouter des interfaces utilisateur et des événements.

[Section suivante : 5. Ajout d’un bouton et réinitialisation des emplacements de pièces](unreal-uxt-ch5.md)
