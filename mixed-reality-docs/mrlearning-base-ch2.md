---
title: MR Learning Module de Base - Interface utilisateur, remettez le suivi et mixte de Configuration du Kit de ressources réalité
description: Terminer ce cours pour apprendre à implémenter la reconnaissance faciale de Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, hololens (didacticiel), unity,
ms.openlocfilehash: 1800d36b7292b9cb53b09fdd4b9c4fb763d49e79
ms.sourcegitcommit: 1c0fbee8fa887525af6ed92174edc42c05b25f90
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65730950"
---
# <a name="mr-learning-base-module---user-interface-hand-tracking-and-mixed-reality-toolkit-configuration"></a>MR Learning Module de Base - Interface utilisateur, remettez le suivi et mixte de Configuration du Kit de ressources réalité

Dans la leçon précédente, vous avez appris certaines des fonctionnalités de que la MRTK a à offrir, en démarrant votre première application pour HoloLens 2. Dans la leçon suivante, vous allez apprendre à créer et organiser des boutons, ainsi que les panneaux de texte de l’interface utilisateur et l’interaction par défaut (tactile) pour interagir avec chaque bouton. Vous allez également découvrir l’ajout des actions simples et des effets tels que la modification de la taille, sonore et la couleur des objets. Ce module présente les concepts de base sur la façon de modifier des profils MRTK, en commençant par la désactivation de la visualisation de la maille spatiale. 

## <a name="objectives"></a>Objectifs

* Personnaliser et configurer des profils de kit de ressources de réalité mixte
* Interaction avec hologrammes à l’aide des boutons et des éléments d’interface utilisateur
* Interactions et les entrées de suivi de la part de base

## <a name="instructions"></a>Instructions

### <a name="how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option"></a>Comment configurer les profils de kit de ressources de réalité mixte (Option d’affichage Spatial de sensibilisation à la modification)
Dans cette section, que vous allez apprendre à personnaliser et configurer les profils de kit de ressources de réalité mixte par défaut en ajustant l’option d’affichage de la sensibilisation spatiale à la maille. Vous pouvez suivre ces mêmes principes pour ajuster les paramètres ou les valeurs dans les profils MRTK.

1. Sélectionnez le Kit de ressources de réalité mixte (MRTK) à partir de la hiérarchie « BaseScene ». Dans ce panneau, recherchez le « mixte réalité Toolkit Script » et sélectionnez le « profil actif », comme illustré dans la figure ci-dessous. Double-cliquez sur pour l’ouvrir.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step1im.PNG)

>Remarque: Par défaut, les profils MRTK ne sont pas modifiables. Il s’agit de modèles de profil par défaut à partir de laquelle vous pouvez copier et personnaliser. Il existe plusieurs couches de personnalisation et de profils, il est pratique courante pour copier et personnaliser plusieurs profils lors de la configuration d’un ou plusieurs paramètres.
>
>Pour en savoir plus sur les profils MRTK ainsi que leur architecture, visitez le [documentation de MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Architecture/SpatialAwareness/SpatialAwarenessSystemArchitecture.html>).

2. Créer une copie du profil par défaut pour le personnaliser. Pour copier un profil par défaut, cliquez sur la « copie & Personnaliser » bouton (voir l’image). Cette opération crée une copie du profil MRTK. Avec votre propre copie du profil MRTK, vous avez désormais la possibilité de personnaliser des paramètres dans ce profil. Vous devez également répéter l’étape de copie/personnaliser pour des profils supplémentaires imbriqués sous ce profil, comme décrit dans les étapes suivantes.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step2im.PNG)

3. Désactiver la visibilité de la maille de reconnaissance spatiale. Pour ce faire, recherchez « Paramètres de système de reconnaissance spatiale » comme indiqué dans l’image. Cliquez sur le bouton « cloner » à droite de la le « Spatial sensibilisation profil de système » pour remplacer le profil par défaut avec une copie personnalisable. Si une fenêtre contextuelle s’affiche, appuyez sur le bouton « Cloner », comme indiqué dans la deuxième image ci-dessous.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step3im.PNG)

![MR213_BuildSettings](images/mrlearning-base-ch2-1step3bim.jpg)

4. Créer une copie personnalisée de le par défaut mixte réalité spatiale de maillage Observateur. Cliquez sur la flèche bas en regard de « Windows mixte réalité spatiale de maillage observateur » pour afficher des options supplémentaires. Dans ces options, vous verrez le « par défaut mixte réalité spatiale de maillage observateur » qui apparaît grisée (non modifiable). Vous devez remplacer ce profil par défaut avec une copie personnalisable qui vous pouvez de le modifier. Pour cloner une copie, cliquez sur le bouton à droite (marqué par une flèche verte).

![MR213_BuildSettings](images/mrlearning-base-ch2-1step4im.PNG)

5. Ensuite, vous allez ajuster les paramètres pour l’option d’affichage de dire « occlusion. » Cela rend la maille spatiale invisible, tout en masquant des objets de jeu derrière la maille spatiale (on parle d’occlusion.)

![MR213_BuildSettings](images/mrlearning-base-ch2-1step5im.PNG)

>Remarque: Alors que le maillage de mappage spatial n’est pas visible, il est toujours présent et que vous pouvez interagir avec lui. N’importe quel hologrammes derrière la maille de mappage spatial (par exemple, un hologramme derrière votre mur visible) ne seront pas visibles en raison du paramètre de l’occlusion.

Félicitations ! Vous venez d’apprendre comment modifier un paramètre dans le profil MRTK. Comme vous pouvez le voir, pour modifier les paramètres de MRTK, vous devez créer des copies des profils par défaut afin que vous puissiez les modifier. Vous aurez toujours les profils par défaut (qui ne sont pas modifiables) pour revenir à si vous souhaitez créer un profil avec les nouveaux paramètres, ou vous référer aux profils par défaut. Il existe de nombreux paramètres que vous pouvez ajuster. Pour obtenir une référence complète aux paramètres de profil MRTK, reportez-vous à la documentation de MRTK ici : https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html

### <a name="hand-tracking-gestures-and-interactable-buttons"></a>Suivi des mouvements de la main et des boutons sur
Dans cette section, vous allez apprendre à utiliser la main, appuyez sur un bouton sur le suivi.

1. Sélectionnez « Ressources » dans le dossier de projets.

2. Tapez dans la barre de recherche, « pressablebutton ».

![MR213_BuildSettings](images/mrlearning-base-ch2-2step1im.PNG)

3. Faites glisser le préfabriqué (représenté par une zone bleue) nommé « PressableButton » dans votre hiérarchie. 

   > Remarque: Si vous recevez un message « importation TMP Essentials », importez-le pour l’instant. Si TMP Essentials n’était pas déjà partie de votre projet, vous devrez peut-être répéter cette étape après l’importation Essentials TMP, sinon texte du bouton n’apparaisse pas.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step3im.PNG)

4. Double cliquez sur l’objet de jeu de « PressableButton » (qui doit être présent dans votre hiérarchie BaseScene) pour l’afficher dans votre scène, comme illustré dans l’image ci-dessous (vos graphiques de bouton peut être différente de celle illustrée ci-dessous). 

![MR213_BuildSettings](images/mrlearning-base-ch2-2step4im.PNG)

5. Dans ce panneau, cliquez sur « Ajouter un événement « pour accorder au bouton répondre à lorsque l’objet d’un push d’un événement. Dans l’option qui s’affiche, sélectionnez le menu déroulant. Sélectionnez « InteractableOnPressReciever ». Ainsi, le bouton répondre à un événement enfoncé lorsque main suivie appuie sur le bouton.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step5im.PNG)

6. Ajouter un cube à la scène. Cliquez avec le bouton droit sur la zone de la hiérarchie, sélectionnez l’objet 3D, puis cliquez sur « cube ». À présent, un cube doit être dans votre affichage. Il s’affichent très volumineux, ajustez les coordonnées (alors que « cube » est toujours sélectionné dans la zone de la hiérarchie) pour réduire la taille. Définissez les valeurs de mise à l’échelle x = 0,1, y = 0.1 et z = 0.1. Être sûr positionner le cube dans votre scène à côté du bouton PRESSEE, mais ne pas se chevaucher avec le bouton. Dans l’image ci-dessous, position du cube est x = 0, y = 0,2 et z = 1. 

   > Remarque: En règle générale, 1 unité dans Unity est à peu près équivalente à 1 mètre dans le monde physique. Il existe des exceptions, par exemple lorsque les objets sont des enfants des objets à l’échelle.
   
   ![MR213_BuildSettings](images/mrlearning-base-ch2-1step6ima.PNG)

![MR213_BuildSettings](images/mrlearning-base-ch2-2step6imb.PNG)

7. Dans cette étape vous allez configurer le cube pour modifier la couleur lorsque votre bouton est enfoncé. Sélectionnez le PressableButton dans le menu « BaseScene ». Dans ce panneau, sous la zone « Sélectionner le Type événement », cliquez sur le bouton « + ». Faites glisser le « cube » dans le menu « BaseScene » dans la zone « Runtime uniquement », comme illustré dans l’image ci-dessous

![MR213_BuildSettings](images/mrlearning-base-ch2-2step7ima.PNG)

Cliquez sur la liste déroulante indiquant « Aucune fonction ». Sélectionnez « MeshRenderer » puis « Matériel matériel ». Cela vous permettra de modifier le matériau lorsque le bouton est enfoncé. 

![MR213_BuildSettings](images/mrlearning-base-ch2-2step7imb.PNG)

Accédez au panneau de configuration de projet et recherche pour le matériel que vous souhaitez pouvoir modifier. Vous vous apprêtez à utiliser le matériel de « MRTK_Standard_Cyan » pour cet exemple, trouvée en tapant dans « cyan » dans la barre de recherche de l’onglet projet (le MRTK inclut plusieurs matériaux et couleurs sélectionnables.) Faites glisser le matériel à la zone en dessous de « MeshRenderer.material ». Vous trouverez les supports MRTK dans actifs > MixedRealityToolkit.SDK > StandardAssets > matériaux.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step7imbb.PNG)

![MR213_BuildSettings](images/mrlearning-base-ch2-1step7imc.PNG)

L’événement est maintenant définie afin que lorsque le bouton est enfoncé, le cube change de couleur selon le matériel que vous avez spécifié. Dans cet exemple, le cube devient la couleur cyan.

8. Ensuite, vous allez configurer l’action de mise en production de sorte que dès son lancement, le bouton revient à sa couleur par défaut. Répétez l’étape 7 (l’étape précédente), mais cette fois avec l’événement de « de relâchement » au lieu de l’événement « OnPress », comme illustré dans l’image ci-dessous.

9.  Dans le volet de projet, recherchez un matériau pour le cube à la valeur par défaut sur le bouton Publier (dans notre cas, nous avons choisi MRTK_Standard_LightGray.) Faites glisser le matériel dans la zone sous le champ « MeshRenderer.material ».

![MR213_BuildSettings](images/mrlearning-base-ch2-2step8im.PNG)

Maintenant lorsque le bouton est enfoncé, il doit passer à une nouvelle couleur (par exemple, cyan) et lorsque le bouton est relâché il devez rétablir la couleur par défaut que vous avez spécifié (par exemple, gris clair.) Appuyez sur le bouton « lecture » en haut de l’écran pour faire un essai dans l’éditeur ou de déployer sur votre 2 HoloLens pour tester ! Pour en savoir plus sur la simulation dans l’éditeur, y compris la simulation de main lire le [page de documentation de simulation de MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/InputSimulation/InputSimulationService.html>). 

### <a name="creating-a-panel-of-buttons-using-mrtks-grid-object-collection"></a>Création d’un panneau de boutons à l’aide de la Collection d’objets de MRTK grille

Dans cette section, vous allez apprendre à aligner automatiquement plusieurs boutons dans une interface utilisateur intéressante à l’aide d’outil de GridObjectCollection de la MRTK.

1. Dupliquer le bouton de la section précédente jusqu'à ce que vous disposez de 5 boutons. Il existe plusieurs manières de procéder :
- Cliquez avec le bouton droit sur le bouton et cliquez sur « Copier », vers le bas sous le bouton et avec le bouton droit cliquez de nouveau sur puis dans cliquez sur « Coller ». 
- Cliquez avec le bouton droit sur le bouton, puis cliquez sur « en double ». 
- Utilisez la commande de clavier en cliquant sur le cube et en appuyant sur « ctrl D » de votre clavier.

Répétez cette jusqu'à ce que vous avez 5 boutons total (voir les flèches rouges 5 dans l’image ci-dessous).

![Base de Mrlearning Ch2 3Step1im](images/mrlearning-base-ch2-3step1im.PNG)

2. Regrouper les boutons sous un objet de jeu vide parent. Pour que les boutons dans la collection de la grille, vous devez regrouper vos boutons sous un objet parent commun. Cliquez avec le bouton droit dans le hiearachy et cliquez sur « Créer vide ». Cette opération crée un nouvel objet de jeu vide pour vous permet de placer tous les boutons. Elle s’affiche en tant que « gameObject ». Clic droit et renommez-le « ButtonCollection ».

![Base de Mrlearning Ch2 3Step2im](images/mrlearning-base-ch2-3step2im.PNG)

3. Déplacez tous les boutons dans la nouvelle collection. Cela, sélectionnez toutes les cinq les objets de bouton dans votre heirarch et les faire glisser toutes sous l’objet de jeu de « ButtonCollection », comme illustré dans l’image ci-dessous. Conseil : sélectionnez plusieurs éléments en maintenant la touche ctrl enfoncée tout en sélectionnant les éléments.

![Base de Mrlearning Ch2 3Step3imb](images/mrlearning-base-ch2-3step3imb.PNG)

4. Ajouter le composant de « Grille objet Collection » du MRTK à la collection de boutons.  Pour ce faire, sélectionnez l’objet parent de « ButtonCollection » et dans ce panneau, cliquez sur le bouton « Ajouter un composant ». Puis recherchez « Grille objet Collection » dans la barre de recherche et sélectionnez-le lorsqu’il apparaît dans la liste.

![Base de Mrlearning Ch2 3Step4im](images/mrlearning-base-ch2-3step4im.PNG)

Le composant de la Collection d’objets de grille vous permet d’organiser des boutons ou l’un ensemble d’objets dans une ligne intéressante, une colonne ou une grille. Il s’agit d’un des blocs de construction fournis par le MRTK qui vous offre un moyen rapide et simple de créer de superbes interfaces utilisateurs.

5. Configurer la collection d’objets de grille. Pour vérifier que tous les visages de boutons à l’utilisateur, sélectionnez « orienter type » puis « face parent vers l’avant » (comme indiqué dans l’image.) Ensuite, modifiez la taille de cellule pour définir l’espace entre vos boutons. Démarrez avec des unités 0.12 par 0.12 unités pour la largeur de cellule et la hauteur de cellule, comme illustré dans l’image ci-dessous. Vous devrez peut-être ajuster ces valeurs, en fonction des ressources d’objet/bouton choisis. Vérifiez que « Lignes » sont définis sur 1. Puis cliquez sur « Mise à jour collecte » et la scène doit ressembler à l’image ci-dessous. 


![Base de Mrlearning Ch2 3Step5im](images/mrlearning-base-ch2-3step5im.PNG)

>Remarque: Selon l’orientation des objets enfants ou de l’objet parent, vous aurez probablement besoin d’ajuster l’orientation de la définir différemment dans les futurs projets. La largeur des cellules et les champs de la hauteur de cellule également devront peut-être être définies différemment, selon la taille des objets dans votre collection.

### <a name="adding-text-into-your-scene"></a>Ajout de texte dans votre scène

Dans cette section, vous allez apprendre à ajouter et modifier du texte à votre expérience de réalité mixte. Si vous n’avez pas déjà, vérifiez que vous avez activé dans Unity en suivant les instructions de TextMeshPro [ici](https://docs.unity3d.com/Packages/com.unity.textmeshpro@2.0/manual/index.html#installation).

1. Sélectionnez l’objet parent de « ButtonCollection » et cliquez avec le bouton droit sur la collection. Développez des « objet 3D » dans le menu déroulant, puis sélectionnez « TextMeshPro – texte ». Vous devriez voir un objet TextMeshPro sous la collection de boutons, comme illustré dans l’image ci-dessous.

![Leçon 2 chapitre4 Step1a](images/Lesson2_Chapter4_Step1a.JPG)
![Lesson2 chapitre4 Step1b](images/Lesson2_Chapter4_Step1b.JPG)

2. Dans le champ de texte du composant TextMeshPro (situé dans le panneau d’inspecteur, comme indiqué ci-dessous), tapez « Bouton de Collection texte ». Le texte s’affiche dans la scène, mais il est masqué derrière les boutons et/ou de taille incorrecte.

![Leçon 2 chapitre4 Step2](images/Lesson2_Chapter4_Step2.JPG)

3. Pour améliorer la taille du texte et le positionnement pour une meilleure lisibilité, réglez le champ « Taille de police » dans le composant TextMeshPro pour modifier la taille de la police. Vous devrez également ajuster la position de « Rect transformer » et de la mise à l’échelle comme indiqué dans l’image ci-dessous. Afficher les images ci-dessous pour les valeurs utilisées pour la configuration de notre texte et vous pouvez utiliser ces valeurs comme point de départ à partir de laquelle améliorer encore plus la taille et le positionnement de votre champ de texte.

![Leçon 2 chapitre4 Step3](images/Lesson2_Chapter4_Step3.JPG)
![Lesson2, chapitre4 étape 4](images/Lesson2_Chapter4_Step4.JPG)

5. Pour modifier les valeurs de texte sur les objets de bouton, cliquez sur la flèche en regard de n’importe quel bouton pour le développer et accédez à l’objet « SeeItSayItLabel », puis accédez à « TextMeshPro », où vous pouvez modifier le texte à vos boutons comme décrit dans les étapes ci-dessus.

![Étape 5 de chapitre4 leçon 2](images/Lesson2_Chapter4_Step5.JPG)

### <a name="congratulations"></a>Félicitations !
Dans cette leçon, vous avez appris à copier, personnaliser et configurer un paramètre de profil MRTK (par exemple, visibilité de maille spatial sensibilisation.) Vous avez également appris comment interagir avec un bouton pour déclencher des événements à l’aide de mains suivies sur la version 2 HoloLens. Enfin, vous avez appris à créer une simple interface de l’interface utilisateur à l’aide texte Mesh Pro d’Unity composant de Collection d’objets de grille de la MRTK.

[Leçon suivante : Solveurs et l’emplacement de contenu dynamique](mrlearning-base-ch3.md)

