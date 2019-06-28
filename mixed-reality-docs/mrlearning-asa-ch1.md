---
title: Module MR Learning ASA Azure spatiale de point d’ancrage sur HoloLens 2
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: c120d22f955d366042bbcb9ac73eaa4f13dc20e9
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67415267"
---
# <a name="getting-started-with-azure-spatial-anchors-on-hololens-2"></a>Prise en main Azure les ancres spatiale sur HoloLens 2

Bienvenue dans le deuxième module du didacticiel 2 HoloLens. Avant de commencer, assurez-vous que tous les de la [conditions préalables](https://docs.microsoft.com/en-us/azure/spatial-anchors/quickstarts/get-started-unity-hololens) sont terminées. Si vous n’avez pas terminé la première, [module Base](mrlearning-base.md) encore, il est recommandé que vous effectuez tout d’abord ce module. Si vous démarrez à partir d’un projet Unity, suivez les étapes de la création du nouveau projet dans le [module Base](mrlearning-base.md). 

## <a name="objectives"></a>Objectifs

* Découvrez les principes fondamentaux du développement avec ancres spatiale d’Azure avec la version 2 HoloLens

* Créer, charger et télécharger des ancres Spatial

  

## <a name="instructions"></a>Instructions

### <a name="downloading-and-importing-assets"></a>Téléchargement et importation d’éléments
Avant de commencer, téléchargez et importez les ressources suivantes :

[Azure Spatial Anchors](https://github.com/azure/azure-spatial-anchors-samples/releases)

[Module de Base de MR Pack de ressources](https://github.com/microsoft/mixedrealitylearning/releases/tag/v1.1)

[Module ASA Pack de ressources](https://github.com/microsoft/MixedRealityLearning/releases/tag/ASA_B2)

[Kit de ressources de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases)

> Remarque: Consultez l’étape 5 pour obtenir des instructions spécifiques sur la façon d’importer ancres spatiale d’Azure, étape 6 pour obtenir des instructions spécifiques sur le module de Base de MR Pack de ressources et des étapes 3 à 4 pour obtenir des instructions spécifiques sur le Kit de ressources de réalité mixte (MRKT).

1. créer une nouvelle scène dans votre projet. Cliquez avec le bouton droit sur le dossier de votre scène, cliquez sur « Créer », puis sur scène. Nom de la nouvelle scène ASALearningmodule.

![module2chapter1step1im](images/module2chapter1step1im.PNG)

2. Double-cliquez sur ASALearningmodule pour afficher des éléments prédéfinis apparaissent, ainsi que la nouvelle scène. 
3. Configurer la scène pour le développement de réalité mixte. 

![module2chapter1step3im](images/module2chapter1step3im.PNG)

> Remarque: Vous verrez une fenêtre contextuelle qui dit, « Vous devez choisir un fichier pour le Kit de ressources de réalité mixte ». En cliquant sur Ok, vous accédez à l’étape 4.

4. Lorsque vous choisissez un fichier pour le MRTK, sélectionnez DefaultMixedRealityToolkitConfigurationProfile.

   > Remarque: Si vous avez votre propre profil de configuration, n’hésitez pas à utiliser à la place.

![module2chapter1step4im](images/module2chapter1step4im.PNG)

La scène est maintenant configurée pour la réalité mixte. Veillez à enregistrer votre scène (effectuer cette opération avec des contrôles / cmd + S ou cliquez sur fichier, puis cliquez sur Enregistrer sous). 

5. Importer le [Azure ancres Spatial](https://github.com/azure/azure-spatial-anchors-samples/releases). Pour pouvoir utiliser les ancres spatiales, vous devez importer cette ressource. Cliquez sur le lien ci-dessus et cliquez avec le bouton droit sur AzureSpatialAnchors.unitypackage. Cliquez sur Enregistrer la cible sous et enregistrez-le sur votre ordinateur. 

   ![module2chapter1step5aim](images/module2chapter1step5aim.PNG)

   Une fois qu’elle est enregistrée, revenir dans Unity, cliquez sur ressources, pour importer un Package s’arrêtent. Puis cliquez sur le Package personnalisé... Fichiers de votre ordinateur seront ouvre. Quand ils font, trouver où vous avez enregistré le package ancres Spatial Azure et sélectionnez-le. Puis cliquez sur Ouvrir.

   ![module2chapter1step5bim](images/module2chapter1step5bim.PNG)

   Une fenêtre contextuelle s’affiche, providingg une liste d’outils et paramètres et vous demandant les éléments à importer. Sélectionnez ***tous les*** des options disponibles, puis cliquez sur Importer.

   ![module2chapter1step5cim](images/module2chapter1step5cim.PNG)

   > Remarque: Soyez patient, il prendra quelques minutes à importer. 

   6. Importation [module MR Base Pack de ressources](https://github.com/microsoft/mixedrealitylearning/releases/tag/v1.1) suivant. Beaucoup comme étape 5, cliquez sur le lien ci-dessus. Cliquez avec le bouton droit sur BasemoduleAssetsV1 1.unitypackag et cliquez sur Enregistrer la cible sous, puis enregistrez-le sur votre ordinateur.

   ![module2chapter1step6aim](images/module2chapter1step6aim.PNG)

   > Astuce : Enregistrez toutes ces ressources dans le même dossier afin qu’ils soient plus faciles à trouver et ont accès à. Il conserve tous les éléments agréable et organisées.

   Tout comme l’étape 5, revenir en arrière dans à Unity et cliquez sur ressources survolez importer un Package. Cliquez sur le Package personnalisé... Fichiers de votre ordinateur seront affichent à nouveau. Accédez à où vous avez stocké le module de Base Pack de ressources. et sélectionnez-le. Cliquez sur Ouvrir.

   ![module2chapter1step5bim](images/module2chapter1step5bim.PNG)

   > Remarque: Il peut y avoir plus de ressources nécessaires plus loin dans ce module. Suivez ces étapes pour importer les ressources mentionnées à ce stade. 
                                                                                                                                                                                                                    
7. Importer l’accusé de réception du module ASA à l’aide de la même approche que pour l’importation de packages précédentes.

### <a name="configuring-your-scene"></a>Configuration de votre scène

Dans cette section, nous allons ajouter prefabs et les scripts dans la scène pour créer une série de boutons qui illustrent les principes fondamentaux du comportement des ancres locales et Azure les ancres Spatial dans une application.

7. Dans l’onglet projet, sous le dossier Assets, cliquez sur ASAmoduleAssets. Une fois sélectionnée, vous verrez deux prefabs : ButtonParent et ParentAnchor.

![module2chapter1step7im](images/module2chapter1step7im.PNG)

8. Faites glisser les deux prefabs dans la scène. 

![module2chapter1step8im](images/module2chapter1step8im.PNG)

9. Double-cliquez sur le point d’ancrage du parent pour le sélectionner. Vous devrez peut-être ajuster votre affichage pour afficher la scène entière. Ajuster votre scène en fonction des besoins.

    Familiarisez-vous avec le préfabriqué ParentAnchor. Actuellement, l’objet de jeu nommé, ParentAnchor, est un cube en couleur à des fins de démonstration. Finalement, nous », ll masquer le cube et placer notre contenu en tant qu’enfant de le ParentAnchor. Cette préfabriqué inclut le script AzureSpatialAnchorsDemoWrapper.cs (inclus avec le SDK ASA) et le script ASAmoduleScript.cs, inclus dans le cadre de ce module à l’objet ParentAnchor. 

10. Configurer les boutons. Sous le préfabriqué ParentAnchor, notez que plusieurs boutons étiquetés. Ces boutons sont créés à partir de préfabriqués de PressableButton de la MRTK. En savoir plus sur la création de boutons PRESSEE depuis le [module Base](mrlearning-base-ch2.md). Pour chaque bouton, ajoutez un événement est déclenché lorsque l’utilisateur appuie ou sélectionne le bouton en fonction de la liste ci-dessous. 

- Pour le bouton, StartAzureSession, créez un nouvel événement sous le déclencheur d’événement bouton enfoncé, ainsi que le déclencheur d’événement sur cliquez sur. Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode StartAzureSession() à partir du composant de l’objet ParentAnchor ASAmoduleScript.

  ![module2chapter1step10aim](images/module2chapter1step10aim.PNG)

  ![module2chapter1step10bim](images/module2chapter1step10bim.PNG)

  ![module2chapter1step10cim](images/module2chapter1step10fim.PNG)

- Pour le nom de bouton, StopAzureSession, créez un nouvel événement sous le déclencheur d’événement bouton enfoncé, ainsi que le déclencheur d’événement sur cliquez sur. Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode StopAzureSession() à partir du composant de l’objet ParentAnchor ASAmoduleScript.

- Pour le bouton, CreateAnchor, créez un nouvel événement sous le déclencheur d’événement bouton enfoncé, ainsi que le déclencheur d’événement sur cliquez sur. Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode CreateAzureAnchor() à partir du composant de l’objet ParentAnchor ASAmoduleScript.

- Déclencheur d’événements pour le bouton, démarrer la recherche pour d’ancrage, créer un nouvel événement sous le bouton Presse-papiers » ainsi que le déclencheur d’événement sur cliquez sur. Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode FindAzureAnchor() à partir du composant de l’objet ParentAnchor ASAmoduleScript.

- Pour le bouton, DeleteAzureAnchor, créez un nouvel événement sous le déclencheur d’événement bouton enfoncé, ainsi que le déclencheur d’événement sur cliquez sur. Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode DeleteAzureAnchor() à partir du composant de l’objet ParentAnchor ASAmoduleScript.

- Pour le bouton, supprimer les ancre Local, créez un nouvel événement sous le déclencheur d’événement bouton enfoncé, ainsi que le déclencheur d’événement sur cliquez sur. Faites glisser l’objet ParentAnchor dans le champ vide et affecter la méthode RemoveLocalAnchor() à partir du composant de l’objet ParentAnchor ASAmoduleScript.

### <a name="build-and-demonstrate-base-application"></a>Générer et de démontrer l’Application de Base

Maintenant que votre scène est configurée pour illustrer les principes fondamentaux d’ancres spatiale d’Azure, nous générera et illustrer le comportement de base des ancres spatiale d’Azure. 

1. Si vous avez fermé la fenêtre Build Settings dans les sections précédentes, rouvrez-la en choisissant File>Build Settings.
    ![Lesson1Chapter5Step1](images/Lesson1Chapter5Step1.JPG)

2. Vérifiez la scène que vous souhaitez essayer est en arrière-plan dans la liste de Build en cliquant sur le bouton Ajouter un arrière-plan ouverte.

3. Appuyez sur le bouton Build (Générer) pour commencer le processus de génération.
    ![Lesson1Chapter5Step3](images/Lesson1Chapter5Step3.JPG)

4. Créez un dossier pour votre application et nommez-le. Dans l’image ci-dessous, un dossier portant le nom d’application a été créé pour contenir l’application. Cliquez sur Sélectionner un dossier pour commencer à créer dans le dossier nouvellement créé. Fenêtre une fois la build terminée, vous pouvez fermer le paramètre de Build » dans Unity. 
    ![Lesson1Chapter5Step4](images/Lesson1Chapter5Step4.JPG)

  > REMARQUE : Si la génération échoue, essayez de renouveler l’opération, éventuellement après avoir redémarré Unity. Si vous voyez une erreur comme « Error : CS0246 = le nom de type ou espace de noms « XX » est introuvable (vous manque-t-il une à l’aide de la directive ou une référence d’assembly ?). Vous devrez peut-être installer [SDK Windows 10 (10.0.18362.0)](<https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk>) 
  >

5. Une fois la génération terminée, ouvrez le dossier créé qui contient vos fichiers d’application nouvellement générés. Double-cliquez sur the"MixedRealityBase.sln solution ou le nom correspondant. Si vous avez utilisé un autre nom pour votre projet pour ouvrir le fichier de solution dans Visual Studio.

  > Remarque: Veillez à ouvrir le dossier nouvellement créé (par exemple, le dossier App, si suit les conventions d’affectation de noms des étapes précédentes, car il y aura un fichier .sln portant le même nom en dehors de ce dossier ne doit ne pas être confondue avec le fichier .sln dans le dossier de génération. 

![Lesson1Chapter5Step5](images/Lesson1Chapter5Step5.JPG)

  > Remarque: Si Visual Studio vous demande d’installer de nouveaux composants, prenez un moment pour vous assurer que tous les composants requis sont installés comme spécifique dans [la page « Installer les outils »](install-the-tools.md) 

6. Branchez l’appareil HoloLens 2 à votre PC avec le câble USB. Ces instructions de la leçon suppose que vous déployez un test avec un appareil HoloLens 2, vous pouvez également choisir de déployer à la [HoloLens 2 émulateur](using-the-hololens-emulator.md) ou choisissez de créer un [package d’application pour le chargement de version test](<https://docs.microsoft.com/en-us/windows/uwp/packaging/packaging-uwp-apps>)

7. Avant d’effectuer la génération sur votre appareil, vérifiez que ce dernier est en mode développeur. S’il s’agit de votre premier déploiement sur l’appareil HoloLens 2, Visual Studio peut vous demander de l’associer à un code confidentiel. Suivez [ces instructions](https://docs.microsoft.com/en-us/windows/mixed-reality/using-visual-studio) si vous devez activer le mode développeur ou couplé à Visual Studio.

8. Configurer Visual Studio pour la création de votre 2 HoloLens en sélectionnant la configuration Release et l’architecture « RM ».
    ![Lesson1Chapter5Step8](images/Lesson1Chapter5Step8.JPG)
   
9. L’étape finale consiste à créer pour votre appareil en sélectionnant le débogage > Démarrer sans débogage. Sélectionnez Démarrer sans débogage provoque l’application à démarrer immédiatement sur votre appareil sur une build réussie d’informations de débogage ithout apparaissant dans Visual Studio. Cela signifie également que vous pouvez déconnecter le câble USB pendant que votre application s’exécute sur votre appareil HoloLens 2 sans arrêter celle-ci. Vous pouvez également sélectionner génération > déployer la Solution pour déployer sur votre appareil sans avoir à l’application de démarrer automatiquement.
    ![Lesson1Chapter5Step9](images/Lesson1Chapter5Step9.JPG)
    
10. Suivez les instructions. Lorsque l’application s’exécute sur votre appareil, suivez l’à l’écran des instructions. Appuyez sur les boutons de scène correspondant à la procédure ci-dessous.
    
    ![module2chapter1step10eim](images/module2chapter1step10eim.PNG)
    
    1. Démarrer la session ancres spatiale.
    
    2. Déplacer le cube à un autre emplacement.
    
    3. Enregistrer les ancres spatiales Azure à l’emplacement du cube.
    
    4. Arrêter la session Azure ancres spatiale.
    
    5. Supprimer le point d’ancrage local sur le cube pour autoriser l’utilisateur à déplacer le cube.
    6. Déplacer le cube à un autre endroit.
    
    7. Démarrez Azure ancres spatial session.
    
    8. Recherchez Azure Spatial aachors. 
    
    e, vous devez revenir à l’emplacement d’origine vous mets lorsque vous avez créé le point d’ancrage).
    9. Supprimer d’ancrage spatial Azure.
    
    10. Arrêter la session Azure.

### <a name="anchoring-an-experience"></a>Ancrage d’une expérience

Dans les sections précédentes, vous avez appris les notions de base des ancres spatiale d’Azure. Nous avons utilisé un cube pour représenter et de visualiser l’objet de jeu parent avec le point d’ancrage attaché. Dans cette section, vous allez apprendre à l’ancrage d’une expérience entière en le plaçant en tant qu’enfant de l’objet ParentAnchor. Pour cet exemple, nous utilisons le module lunaire application de démonstration d’Assembly qui a été créé pendant [module Base Leçon 6](mrlearning-base-ch6.md).

1. Recherchez le préfabriqué lunaire Module Assembly complet et la faire glisser vers votre hiérarchie en tant qu’enfant de le gameobject AnchorParent comme indiqué dans l’image ci-dessous.

   ![module2chapter1step11](images/module2chapter1step11im.PNG)

2. Position de l’assembly de module expérience afin que le cube est toujours exposé comme indiqué dans l’image ci-dessous. Dans l’application, les utilisateurs peuvent repositionner l’expérience entière en déplaçant le cube. 

   ![module2chapter1step12im](images/module2chapter1step12im.PNG)

   > Remarque: Il existe une variété de flux d’expérience utilisateur pour le repositionnement des expériences, y compris l’utilisation d’un bouton pour activer/désactiver une zone englobante qui entoure l’expérience, l’utilisation d’un objet repositionnement (par exemple, le cube utilisé dans cette étape), l’utilisation de la rotation et position gizmos et bien plus encore.

## <a name="congratulations"></a>Félicitations
Dans cette leçon, vous avez appris les notions de base des ancres spatiale d’Azure. Cette esson fournies vous avec plusieurs boutons qui vous permettent d’Explorer les différentes étapes requises pour démarrer et arrêter une session d’Azure, créer, charger et télécharger azure ancres sur un seul appareil. Dans la leçon suivante, nous allez apprendre comment enregistrer des ID d’ancrage Azure dans votre 2 HoloLens pour la récupération, même après le redémarrage de l’application. Lors de la série, vous allez également apprendre à transférer d’ancrage ID entre plusieurs appareils pour obtenir l’alignement spatial et en savoir plus sur multi-utilisateurs partagé sessions (bientôt disponibles dans le cadre du partage de module).

[Leçon suivante : ASA leçon 2](mrlearning-asa-ch2.md)

