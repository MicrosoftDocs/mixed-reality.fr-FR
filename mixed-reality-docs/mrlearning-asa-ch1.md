---
title: Didacticiels sur les ancres spatiales Azure-1. Prise en main des ancres spatiales Azure
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 563ed67a388444753e3b560d76d4e6be48249e15
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438465"
---
# <a name="1-getting-started-with-azure-spatial-anchors"></a>1. prise en main des ancres spatiales Azure

Bienvenue dans le deuxième module des didacticiels HoloLens 2. Avant de commencer, assurez-vous que toutes les [conditions préalables](https://docs.microsoft.com//azure/spatial-anchors/quickstarts/get-started-unity-hololens) sont remplies. Si vous n’avez pas encore effectué le premier [module de base](mrlearning-base.md) , il est recommandé d’effectuer d’abord ce module. Si vous démarrez à partir d’un nouveau projet Unity, suivez les étapes de création du nouveau projet dans le [module de base](mrlearning-base.md). 

## <a name="objectives"></a>Objectifs

* Découvrez les principes de base du développement avec les ancres spatiales Azure avec HoloLens 2

* Créer, charger et télécharger des ancres spatiales

## <a name="instructions"></a>Instructions

### <a name="downloading-and-importing-assets"></a>Téléchargement et importation de ressources
Avant de commencer, téléchargez et importez les ressources suivantes :

[Ancres spatiales Azure v 1.1.0](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v1.1.0/AzureSpatialAnchors.unitypackage)

[Pack d’actifs du module de base RM v 1.2](https://github.com/microsoft/MixedRealityLearning/releases/download/1.2/BaseModuleAssets-1.2.unitypackage)

[Module Asset Pack de ASA v 1.0](https://github.com/microsoft/MixedRealityLearning/releases/tag/ASA_1.3)

[Kit de la réalité mixte Toolkit 2.0.0 RC1](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC1-Refresh.unitypackage)

> Remarque : consultez l’étape 5 pour obtenir des instructions spécifiques sur l’importation des ancres spatiales Azure, étape 6 pour obtenir des instructions spécifiques sur le pack d’actifs du module de base RM et les étapes 3 à 4 pour obtenir des instructions spécifiques sur le kit de ressources de la réalité mixte (MRKT).

1. Créez une nouvelle scène dans votre projet. Cliquez avec le bouton droit sur le dossier de votre scène, cliquez sur créer, puis sur scène. Nommez la nouvelle scène ASALearningmodule.

![module2chapter1step1im](images/module2chapter1step1im.PNG)

2. Double-cliquez sur ASALearningmodule pour voir des éléments prédéfinis s’afficher en même temps que la nouvelle scène. 
3. Configurez la scène pour le développement de la réalité mixte. 

![module2chapter1step3im](images/module2chapter1step3im.PNG)

> Remarque : vous verrez une fenêtre contextuelle indiquant que vous devez choisir un fichier pour la réalité mixte Toolkit. Cliquez sur OK pour passer à l’étape 4.

4. Lors du choix d’un fichier pour le MRTK, sélectionnez, DefaultMixedRealityToolkitConfigurationProfile.

> Remarque : Si vous disposez de votre propre profil de configuration, n’hésitez pas à l’utiliser à la place.

![module2chapter1step4im](images/module2chapter1step4im.PNG)

La scène est maintenant configurée pour la réalité mixte. Veillez à enregistrer votre scène (procédez comme suit : contrôle/commande + S ou cliquez sur fichier, puis sur Enregistrer). 

5. Importez les [ancres spatiales Azure](https://github.com/azure/azure-spatial-anchors-samples/releases). Pour pouvoir utiliser des ancres spatiales, vous devez importer cette ressource. Cliquez sur le lien ci-dessus et cliquez avec le bouton droit sur AzureSpatialAnchors. pour Unity. Cliquez sur enregistrer la cible sous, puis enregistrez-la sur votre ordinateur. 

![module2chapter1step5aim](images/module2chapter1step5aim.PNG)

Une fois enregistré, revenez dans Unity, cliquez sur ressources, puis sur Importer le package. Cliquez ensuite sur package personnalisé... Vos fichiers d’ordinateur s’ouvrent. Dans ce cas, recherchez l’emplacement où vous avez enregistré le package d’ancrages spatiaux Azure, puis sélectionnez-le. Cliquez ensuite sur Ouvrir.

![module2chapter1step5bim](images/module2chapter1step5bim.PNG)

Une fenêtre contextuelle s’affiche, fournissant une liste d’outils et de paramètres et vous demandant ce qu’il faut importer. Sélectionnez ***toutes*** les options disponibles, puis cliquez sur Importer.

![module2chapter1step5cim](images/module2chapter1step5cim.PNG)

> Remarque : Soyez patient. l’importation prendra quelques minutes. 

6. Importez le [Pack de ressources du module de base Mr](https://github.com/microsoft/MixedRealityLearning/releases/tag/1.2) . À l’étape 5, cliquez sur le lien ci-dessus. Cliquez ensuite avec le bouton droit sur BasemoduleAssets-1.2. pour Unity, puis cliquez sur enregistrer la cible sous et enregistrez-la sur votre ordinateur.

![module2chapter1step6aim](images/module2chapter1step6aim.PNG)

> Conseil : enregistrez toutes ces ressources dans le même dossier afin qu’elles soient plus faciles à trouver et à y accéder. Tout est agréable et organisé.

Comme pour l’étape 5, revenez à Unity, cliquez sur ressources, puis pointez sur Importer le package. Cliquer sur le package personnalisé... Les fichiers de votre ordinateur s’affichent à nouveau. Accédez à l’emplacement où vous avez stocké le Pack de ressources du module de base. et sélectionnez-le. Cliquez sur Ouvrir.

![module2chapter1step5bim](images/module2chapter1step5bim.PNG)

> Remarque : il peut y avoir plus de ressources nécessaires plus tard dans ce module. Procédez comme suit pour importer les ressources mentionnées à partir de ce point sur. 

7. Importez le [Pack de module ASA](https://github.com/microsoft/MixedRealityLearning/releases/tag/ASA_1.3) en utilisant la même approche que l’importation des packages précédents.

### <a name="configuring-your-scene"></a>Configuration de votre scène

Dans cette section, nous allons ajouter des prefabs et des scripts dans la scène pour créer une série de boutons qui illustrent les principes de base de la façon dont les ancres locales et les ancres spatiales Azure se comportent dans une application.

8. Sous l’onglet projet, sous le dossier ressources, cliquez sur ASAmoduleAssets. Une fois sélectionné, vous verrez deux prefabs : ButtonParent et ParentAnchor.

![module2chapter1step7im](images/module2chapter1step7im.PNG)

9. Faites glisser les deux prefabs dans la scène. 

![module2chapter1step8im](images/module2chapter1step8im.PNG)

Remarque : Si vous souhaitez vérifier les journaux de débogage dans HoloLens. Vous pouvez glisser-déplacer le Prefab DebugWindow à partir du dossier ASAModuleAssets vers la scène. Attachez le script DebugWindowMessaging dans le panneau d’inspecteur DebugWindow. Activez l’option déboguer la fenêtre activée, puis faites glisser le Prefab DebugWindow dans le champ DebugText vide. Ajustez la position de DebugWindow lorsque cela est approprié.

10. Double-cliquez sur l’ancre parente pour la sélectionner. Vous devrez peut-être ajuster votre affichage pour voir l’intégralité de la scène. Ajustez votre scène en fonction des besoins.

Familiarisez-vous avec le Prefab ParentAnchor. Actuellement, l’objet de jeu nommé, ParentAnchor, est un cube coloré à des fins de démonstration. Finalement, nous allons masquer le cube et placer notre contenu en tant qu’enfant du ParentAnchor. Ce Prefab inclut le script AzureSpatialAnchorsDemoWrapper.cs (inclus avec le kit de développement logiciel (SDK) ASA) et le script ASAmoduleScript.cs, inclus dans le cadre de ce module, à l’objet ParentAnchor. 

Remarque : après avoir ajouté le ButtonParent dans la scène, un message s’affiche pour vous demander d’importer les ressources TMP. Importez uniquement le « TMP Essentials ». Après cela, si vous voyez un texte de police de grande taille dans la scène, supprimez l’objet ButtonParent et rajoutez-le à partir du dossier ASAmoduleAssets

11. Configurer des boutons. Sous le Prefab ButtonParent, notez plusieurs boutons étiquetés. Ces boutons sont créés à partir du prefabs PressableButton de MRTK. Apprenez-en davantage sur la création de boutons d’appui à partir du [module de base](mrlearning-base-ch2.md). Pour chaque bouton, ajoutez un événement qui est déclenché quand l’utilisateur appuie sur le bouton ou le sélectionne en fonction de la liste ci-dessous. 

- Pour le bouton nommé, StartAzureSession, créez un événement sous le déclencheur d’événements appuyé sur le bouton, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode StartAzureSession () à partir du composant ASAmoduleScript de l’objet ParentAnchor.

![module2chapter1step10aim](images/module2chapter1step10aim.PNG)

![module2chapter1step10bim](images/module2chapter1step10bim.PNG)

![module2chapter1step10cim](images/module2chapter1step10fim.PNG)

- Pour le nom du bouton, StopAzureSession, créez un événement sous le déclencheur d’événements appuyé sur le bouton, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode StopAzureSession () à partir du composant ASAmoduleScript de l’objet ParentAnchor.

- Pour le bouton nommé, CreateAnchor, créez un événement sous le déclencheur d’événements appuyé sur le bouton, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode CreateAzureAnchor () à partir du composant ASAmoduleScript de l’objet ParentAnchor.  Après cela, faites glisser à nouveau le ParentAnchor dans le champ vide suivant.

- Pour le bouton nommé, commencez à rechercher Anchor, créez un nouvel événement sous le bouton déclencheur d’événements Appuyez sur, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode FindAzureAnchor () à partir du composant ASAmoduleScript de l’objet ParentAnchor.

- Pour le bouton nommé, DeleteAzureAnchor, créez un événement sous le déclencheur d’événements appuyé sur le bouton, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode DeleteAzureAnchor () à partir du composant ASAmoduleScript de l’objet ParentAnchor.  Après cela, faites glisser l’objet ParentAnchor dans le champ vide suivant.

- Pour le bouton nommé, supprimer l’ancre locale, créez un événement sous le déclencheur d’événements enfoncé, ainsi que le déclencheur d’événements on Click. Faites glisser l’objet ParentAnchor dans le champ Empty, puis affectez la méthode RemoveLocalAnchor () à partir du composant ASAmoduleScript de l’objet ParentAnchor.

  Pour configurer des ancres spatiales Azure, accédez au dossier AzureSpatialAnchorsPlugin dans le dossier ressources, puis accédez à exemples-ressources >-> fichier AzureSpatialAnchorsDemoConfig. Dans le panneau Inspecteur, ajoutez l’ID de compte Azure et la clé de compte créés précédemment. Si vous n’avez pas créé ou si vous ne les avez pas, veuillez suivre les [conditions préalables](https://docs.microsoft.com//azure/spatial-anchors/quickstarts/get-started-unity-hololens). module2chapter1step13im
  
  ![module2chapter1step13im](images/module2chapter1step13im.PNG)

### <a name="build-and-demonstrate-base-application"></a>Générer et démontrer l’application de base

Maintenant que votre scène est configurée pour illustrer les principes de base des ancres spatiales Azure, nous allons créer et démontrer le comportement de base des ancres spatiales Azure. 

1. Si vous avez fermé la fenêtre Build Settings dans les sections précédentes, rouvrez-la en choisissant File>Build Settings.
![Lesson1Chapter5Step1](images/Lesson1Chapter5Step1.JPG)
2. Vérifiez que la scène que vous souhaitez essayer se trouve dans la liste scenes dans la build, en cliquant sur le bouton Ajouter des scènes en cours.
3. Vérifiez que la plateforme est définie sur plateforme Windows universelle. Si ce n’est pas le cas, définissez-le sur le même.
4. Appuyez sur le bouton Paramètres du lecteur et accédez à paramètres de publication. Sous fonctionnalités, activez : Internet, serveur client Internet, serveur client réseau privé, stockage amovible, webcam, microphone et perception spatiale.
5. Dans les mêmes paramètres de lecteur, accédez à paramètres XR et sélectionnez la réalité virtuelle prise en charge sur activé.
6. Appuyez sur le bouton Build (Générer) pour commencer le processus de génération.
   ![Lesson1Chapter5Step3](images/Lesson1Chapter5Step3.JPG)
7. Créez un dossier pour votre application et nommez-le. Dans l’image ci-dessous, un dossier avec le nom de l’application a été créé pour contenir l’application. Cliquez sur Sélectionner un dossier pour commencer à créer le dossier nouvellement créé. Une fois la génération terminée, vous pouvez fermer la fenêtre du paramètre de build dans Unity. 
    ![Lesson1Chapter5Step4](images/Lesson1Chapter5Step4.JPG)

  > Remarque : si la génération échoue, réessayez de générer ou redémarrez Unity, puis recommencez l’opération. Si vous voyez une erreur telle que « erreur : CS0246 = le type ou le nom d’espace de noms «XX » est introuvable (une directive using ou une référence d’assembly est-elle manquante ?). Vous devrez peut-être installer le [Kit de développement logiciel (SDK) Windows 10 (10.0.18362.0)](<https://developer.microsoft.com//windows/downloads/windows-10-sdk>) 
  >

8. Une fois la génération terminée, ouvrez le dossier créé qui contient vos fichiers d’application nouvellement générés. Double-cliquez sur la solution « MixedRealityBase. sln » ou le nom correspondant. Si vous avez utilisé un autre nom pour votre projet pour ouvrir le fichier solution dans Visual Studio.

  > Remarque : Veillez à ouvrir le dossier qui vient d’être créé (c’est-à-dire, le dossier de l’application, si vous respectez les conventions d’affectation des noms des étapes précédentes, car il existe un fichier. sln de même nom en dehors de ce dossier qui ne doit pas être confondu avec le fichier. sln dans le dossier de Build. 

![Lesson1Chapter5Step5](images/Lesson1Chapter5Step5.JPG)

> Remarque : si Visual Studio vous invite à installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants requis sont installés comme spécifiques dans [la page « installer les outils »](install-the-tools.md) 

9. Branchez l’appareil HoloLens 2 à votre PC avec le câble USB. Bien que ces instructions de leçon partent du principe que vous déploierez un test avec un appareil HoloLens 2, vous pouvez également choisir de déployer vers l' [émulateur hololens 2](using-the-hololens-emulator.md) ou de créer un [package d’application pour chargement](<https://docs.microsoft.com//windows/uwp/packaging/packaging-uwp-apps>)

10. Avant d’effectuer la génération sur votre appareil, vérifiez que ce dernier est en mode développeur. S’il s’agit de votre premier déploiement sur l’appareil HoloLens 2, Visual Studio peut vous demander de l’associer à un code confidentiel. Suivez [ces instructions](https://docs.microsoft.com//windows/mixed-reality/using-visual-studio) si vous devez activer le mode développeur ou le coupler avec Visual Studio.
11. Configurez Visual Studio pour la création dans votre HoloLens 2 en sélectionnant la configuration Release, ainsi que l’architecture ARM.
    ![Lesson1Chapter5Step8](images/Lesson1Chapter5Step8.JPG)

12. La dernière étape consiste à créer sur votre appareil en sélectionnant Déboguer > Exécuter sans débogage. Si vous sélectionnez l’option Exécuter sans débogage, l’application démarre immédiatement sur votre appareil après une génération réussie sans que des informations de débogage apparaissent dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci. Vous pouvez également sélectionner générer > déployer la solution pour déployer sur votre appareil sans démarrer automatiquement l’application.
    ![Lesson1Chapter5Step9](images/Lesson1Chapter5Step9.JPG)

13. Suivez les instructions. 
    Lorsque l’application s’exécute sur votre appareil, suivez les instructions à l’écran. Appuyez sur les boutons de la scène correspondant aux étapes ci-dessous.

![module2chapter1step10eim](images/module2chapter1step10eim.PNG)
    
    1. Démarrez la session d’ancrages spatiaux.
    
    2. Déplacez le cube vers un autre emplacement.
    
    3. Enregistrez les ancres spatiales Azure à l’emplacement du cube.
    
    4. Arrêtez la session d’ancrages spatiaux Azure.
    
    5. Supprimez l’ancre locale sur le cube pour permettre à l’utilisateur de déplacer le cube.
    
    6. Déplacez le cube ailleurs.
    
    7. Démarrez la session d’ancrages spatiaux Azure.
    
    8. Recherchez les ancres spatiales Azure. 
    Vous devez revenir à l’emplacement d’origine que vous avez placé lorsque vous avez créé le point d’ancrage.
    
    9. Supprimer une ancre spatiale Azure.
    
    10. Arrêtez la session Azure.

### <a name="anchoring-an-experience"></a>Ancrage d’une expérience

Dans les sections précédentes, vous avez appris les principes de base des ancres spatiales Azure. Nous avons utilisé un cube pour représenter et visualiser l’objet de jeu parent avec l’ancre attachée. Dans cette section, vous allez apprendre à ancrer une expérience complète en la plaçant en tant qu’enfant de l’objet ParentAnchor. Pour cet exemple, nous utilisons l’application de démonstration de l’assembly du module lunaire qui a été créée au cours de la [leçon 6 du module de base](mrlearning-base-ch6.md).

1. Recherchez l’assembly de module lunaire complet Prefab et faites-le glisser dans votre hiérarchie en tant qu’enfant de l’objet, comme indiqué dans l’image ci-dessous.

![module2chapter1step11](images/module2chapter1step11im.PNG)

2. Positionnez l’expérience de l’assembly du module afin que le cube soit toujours exposé comme indiqué dans l’image ci-dessous. Dans l’application, les utilisateurs peuvent repositionner l’intégralité de l’expérience en déplaçant le cube. 

![module2chapter1step12im](images/module2chapter1step12im.PNG)

> Remarque : il existe divers flux d’expérience utilisateur pour le repositionnement des expériences, y compris l’utilisation d’un bouton pour basculer un cadre englobant qui entoure l’expérience, l’utilisation d’un objet de repositionnement (tel que le cube utilisé dans cette étape), l’utilisation de la position et de la rotation gizmos, et bien plus encore.

## <a name="congratulations"></a>Félicitations !
Dans ce didacticiel, vous avez appris les principes de base des ancres spatiales Azure. Cette leçon vous a fourni plusieurs boutons qui vous permettent d’explorer les différentes étapes nécessaires au démarrage et à l’arrêt d’une session Azure, ainsi que la création, le chargement et le téléchargement d’ancres Azure sur un seul appareil. Dans la leçon suivante, nous allons apprendre à enregistrer des ID d’ancrage Azure dans votre HoloLens 2 pour la récupération, même après le redémarrage de l’application. Au cours de la série, vous apprendrez également à transférer des ID d’ancrage entre plusieurs appareils pour atteindre l’alignement spatial et à découvrir les sessions partagées multi-utilisateur, à venir dans le cadre du didacticiel de partage.

[Leçon suivante : 2. enregistrement, récupération et partage d’ancres spatiales Azure](mrlearning-asa-ch2.md)

