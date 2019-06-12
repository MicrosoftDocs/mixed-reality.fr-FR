---
title: Module de base d’apprentissage de la réalité mixte - Interface utilisateur, suivi manuel et configuration du Kit de ressources de réalité mixte
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 1800d36b7292b9cb53b09fdd4b9c4fb763d49e79
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "65730950"
---
# <a name="mr-learning-base-module---user-interface-hand-tracking-and-mixed-reality-toolkit-configuration"></a>Module de base d’apprentissage de la réalité mixte - Interface utilisateur, suivi manuel et configuration du Kit de ressources de réalité mixte

Dans la leçon précédente, vous avez découvert certaines des fonctionnalités offertes par le Kit de ressources de réalité mixte (MRTK, Mixed Reality Toolkit) en commençant votre première application pour HoloLens 2. Dans cette leçon suivante, vous allez découvrir comment créer et organiser des boutons et des panneaux de texte de l’interface utilisateur, et comment utiliser l’interaction par défaut (tactile) pour interagir avec chaque bouton. Vous allez également découvrir comment ajouter des actions et des effets simples, comme changer la taille, la sonorité et la couleur des objets. Ce module présente les concepts de base sur la façon de modifier des profils MRTK, en commençant par la désactivation de la visualisation du maillage spatial. 

## <a name="objectives"></a>Objectifs

* Personnaliser et configurer des profils MRTK
* Interaction avec des hologrammes avec des éléments d’interface utilisateur et des boutons
* Entrées et interactions de base pour le suivi de la main

## <a name="instructions"></a>Instructions

### <a name="how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option"></a>Comment configurer les profils MRTK (Changer l’option d’affichage avec reconnaissance spatiale)
Dans cette section, vous allez découvrir comment personnaliser et configurer les profils MRTK par défaut en ajustant l’option d’affichage du maillage avec reconnaissance spatiale. Vous pouvez suivre ces mêmes principes pour ajuster des paramètres ou des valeurs dans les profils MRTK.

1. Sélectionnez Mixed-Reality Toolkit (MRTK) dans la hiérarchie « BaseScene ». Dans le panneau de l’inspecteur, recherchez « Mixed Reality Toolkit Script » et sélectionnez le « profil actif », comme illustré dans la figure ci-dessous. Double-cliquez sur celui-ci pour l’ouvrir.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step1im.PNG)

>Remarque: Par défaut, les profils MRTK ne sont pas modifiables. Il s’agit de modèles de profil par défaut que vous pouvez copier, puis personnaliser. Il existe plusieurs couches de personnalisation et plusieurs profils : c’est donc une pratique courante que de copier et de personnaliser plusieurs profils lors de la configuration d’un ou plusieurs paramètres.
>
>Pour en savoir plus sur les profils MRTK et leur architecture, consultez la [documentation de MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Architecture/SpatialAwareness/SpatialAwarenessSystemArchitecture.html>).

2. Créez une copie du profil par défaut pour le personnaliser. Pour copier un profil par défaut, cliquez sur le bouton « Copy & Customize » (Copier et personnaliser) (voir l’image). Ceci crée une copie du profil MRTK. Avec votre propre copie du profil MRTK, vous pouvez maintenant personnaliser des paramètres de ce profil. Vous devez également répéter l’étape de copie/personnalisation pour des profils supplémentaires imbriqués sous ce profil, comme décrit dans les étapes suivantes.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step2im.PNG)

3. Désactiver la visibilité du maillage de reconnaissance spatiale. Pour cela, recherchez « Spatial Awareness System Settings » (Paramètres du système de reconnaissance spatiale) comme indiqué dans l’image. Cliquez sur le bouton « clone » à droite de « Spatial Awareness System Settings » pour remplacer le profil par défaut par une copie personnalisable. Si une fenêtre contextuelle apparaît, appuyez sur le bouton « Clone », comme indiqué dans la deuxième image ci-dessous.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step3im.PNG)

![MR213_BuildSettings](images/mrlearning-base-ch2-1step3bim.jpg)

4. Créez une copie personnalisée du « Default Mixed Reality Spatial Mesh Observer » (Observateur du maillage spatial de réalité mixte). Cliquez sur la flèche bas en regard de « Windows Mixed Reality Spatial Mesh Observer » pour voir des options supplémentaires. Dans ces options, « Default Mixed Reality Spatial Mesh Observer » apparaît en grisé (non modifiable). Vous devez remplacer ce profil par défaut par une copie personnalisable pour pouvoir le modifier. Cliquez sur le bouton à droite (marqué par une flèche verte) pour cloner une copie.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step4im.PNG)

5. Ensuite, vous allez ajuster les paramètres pour l’option d’affichage pour indiquer « occlusion ». Ceci rend le maillage spatial invisible, tout en continuant de masquer les objets du jeu derrière le maillage spatial (on parle d’occlusion).

![MR213_BuildSettings](images/mrlearning-base-ch2-1step5im.PNG)

>Remarque: Le maillage de mappage spatial n’est pas visible, mais il est toujours présent et vous pouvez interagir avec lui. Les hologrammes présents derrière le maillage de mappage spatial (par exemple un hologramme derrière votre mur visible) ne sont pas visibles en raison du paramètre d’occlusion.

Félicitations ! Vous venez de découvrir comment modifier un paramètre dans le profil MRTK. Comme vous pouvez le voir, pour pouvoir modifier les paramètres du MRTK, vous devez créer des copies des profils par défaut. Vous conservez toujours les profils par défaut (qui ne sont pas modifiables), auxquels vous pouvez revenir si vous voulez créer un profil avec de nouveaux paramètres ou auxquels vous référer. Vous pouvez ajuster de nombreux paramètres. Pour des informations de référence complètes sur les paramètres des profils MRTK, reportez-vous à la documentation du MRTK ici : https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html

### <a name="hand-tracking-gestures-and-interactable-buttons"></a>Gestes de suivi de la main et boutons d’interaction
Dans cette section, vous allez découvrir comment utiliser le suivi de la main pour appuyer sur un bouton d’interaction.

1. Sélectionnez « Assets » (Ressources) dans le dossier des projets.

2. Tapez « pressablebutton » dans la barre de recherche.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step1im.PNG)

3. Faites glisser l’élément préfabriqué (représenté par une zone bleue) nommé « PressableButton » dans votre hiérarchie. 

   > Remarque: Si vous recevez un message concernant « importing TMP Essentials », importez-le à ce moment-là. Si TMP Essentials ne faisait pas déjà partie de votre projet, il peut être nécessaire de répéter cette étape après l’importation de TMP Essentials, sans quoi le texte du bouton risque de ne pas apparaître.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step3im.PNG)

4. Double cliquez sur l’objet de jeu « PressableButton » (qui doit maintenant être présent dans votre hiérarchie BaseScene) pour le voir dans votre scène, comme illustré dans l’image ci-dessous (les représentations de vos boutons peuvent être différentes de celles de l’image ci-dessous). 

![MR213_BuildSettings](images/mrlearning-base-ch2-2step4im.PNG)

5. Dans le panneau de l’inspecteur, cliquez sur « Add Event » (Ajouter un événement) pour donner au bouton un événement auquel répondre quand l’utilisateur appuie dessus. Dans l’option qui apparaît, sélectionnez le menu déroulant. Sélectionnez « InteractableOnPressReciever ». Ceci permet au bouton de répondre à un événement d’appui quand une main suivie appuie sur le bouton.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step5im.PNG)

6. Ajoutez un cube à la scène. Cliquez avec le bouton droit sur la zone de la hiérarchie, sélectionnez « 3D object » (Objet 3D), puis cliquez sur « cube ». Un cube doit maintenant se trouver dans votre affichage. Il va apparaître très grand : ajustez donc les coordonnées (avec « cube » sélectionné dans la zone de la hiérarchie) pour en réduire la taille. Définissez comme ceci les valeurs de mise à l’échelle : x = 0,1, y = 0,1 et z = 0,1. Veillez à positionner le cube dans votre scène en le plaçant près du bouton enfonçable, mais sans recouvrir le bouton. Dans l’image ci-dessous, la position du cube est x = 0, y = 0,2 et z = 1. 

   > Remarque: En règle générale, 1 unité dans Unity est à peu près équivalente à 1 mètre dans le monde physique. Il y a des exceptions à cela, par exemple quand les objets sont des enfants d’objets mis à l’échelle.
   
   ![MR213_BuildSettings](images/mrlearning-base-ch2-1step6ima.PNG)

![MR213_BuildSettings](images/mrlearning-base-ch2-2step6imb.PNG)

7. Dans cette étape vous allez configurer le cube pour qu’il change de couleur quand l’utilisateur appuie sur le bouton. Sélectionnez le bouton PressableButton dans le menu « BaseScene ». Dans le panneau de l’inspecteur, sous la zone « Select Event Type » (Sélectionner le type d’événement), cliquez sur le bouton « + ». Faites glisser le « cube » depuis le menu « BaseScene » dans la zone « Runtime only » (Exécution uniquement), comme illustré dans l’image ci-dessous

![MR213_BuildSettings](images/mrlearning-base-ch2-2step7ima.PNG)

Cliquez sur la liste déroulante indiquant « No Function » (Pas de fonction). Sélectionnez « MeshRenderer » puis « Material material » (Matériau). Ceci vous permettra de changer le matériau quand le bouton est enfoncé. 

![MR213_BuildSettings](images/mrlearning-base-ch2-2step7imb.PNG)

Accédez au panneau du projet et recherchez le matériau que vous voulez substituer au premier. Pour cet exemple, vous allez utiliser le matériau « MRTK_Standard_Cyan », que vous trouvez en tapant « cyan » dans la barre de recherche de l’onglet du projet (le MRTK inclut de nombreux matériaux et couleurs que vous pouvez sélectionner). Faites glisser le matériau dans la zone en dessous de « MeshRenderer.material ». Vous trouverez les matériaux du MRTK dans Assets>MixedRealityToolkit.SDK>StandardAssets>Materials (Ressources>MixedRealityToolkit.SDK>Ressources standard>Matériaux).

![MR213_BuildSettings](images/mrlearning-base-ch2-2step7imbb.PNG)

![MR213_BuildSettings](images/mrlearning-base-ch2-1step7imc.PNG)

L’événement est maintenant défini : ainsi, quand l’utilisateur appuie sur le bouton, le cube change de couleur en fonction du matériau que vous avez spécifié. Dans cet exemple, la couleur du cube passe à cyan.

8. Ensuite, vous allez configurer l’action liée au relâchement du bouton : ainsi, après le relâchement, le bouton revient à sa couleur par défaut. Répétez l’étape 7 (l’étape précédente), mais cette fois avec l’événement « OnRelease » au lieu de l’événement « OnPress », comme illustré dans l’image ci-dessous.

9.  Dans le panneau du projet, recherchez un matériau qui sera le matériau par défaut du cube après relâchement du bouton (dans notre cas, nous avons choisi MRTK_Standard_LightGray). Faites glisser le matériau dans la zone sous le champ « MeshRenderer.material ».

![MR213_BuildSettings](images/mrlearning-base-ch2-2step8im.PNG)

Maintenant, quand le bouton est enfoncé, il doit passer à une nouvelle couleur (par exemple cyan) et quand il est relâché, il doit revenir à la couleur par défaut que vous avez spécifiée (par exemple gris clair.) Appuyez sur le bouton « play » (Lecture) en haut de l’écran pour l’essayer dans l’éditeur, ou pour le déployer et le tester sur votre HoloLens 2 ! Pour en savoir plus sur la simulation dans l’éditeur, notamment la simulation de la main, consultez la [page de documentation de la simulation de MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/InputSimulation/InputSimulationService.html>). 

### <a name="creating-a-panel-of-buttons-using-mrtks-grid-object-collection"></a>Création d’un panneau de boutons avec la collection d’objets de grille du MRTK

Dans cette section, vous allez découvrir comment aligner automatiquement plusieurs boutons dans une interface utilisateur bien ordonnée en utilisant l’outil GridObjectCollection du MRTK.

1. Dupliquez le bouton de la section précédente jusqu’à obtenir 5 boutons. Il existe plusieurs façons de procéder :
- Cliquez avec le bouton droit et cliquez sur « copy » (Copier), puis placez-vous sous le bouton, recliquez avec le bouton droit, puis cliquez sur « paste » (Coller). 
- Cliquez avec le bouton droit, puis cliquez sur « duplicate » (Dupliquer). 
- Utilisez la commande du clavier en cliquant sur le cube et en appuyant sur « Ctrl+D » sur votre clavier.

Répétez cette opération jusqu’à avoir 5 boutons au total (voir les 5 flèches rouges dans l’image ci-dessous).

![Mrlearning Base Ch2 3Step1im](images/mrlearning-base-ch2-3step1im.PNG)

2. Regroupez les boutons sous un objet de jeu parent vide. Pour que les boutons soient dans une collection de grille, vous devez les regrouper sous un objet parent commun. Cliquez avec le bouton droit dans la hiérarchie, puis cliquez sur « create empty » (Créer vide). Ceci crée un objet de jeu vide où vous pouvez placer tous les boutons. Il s’affiche en tant que « gameObject ». Cliquez avec le bouton droit et renommez-le en « ButtonCollection ».

![Mrlearning Base Ch2 3Step2im](images/mrlearning-base-ch2-3step2im.PNG)

3. Déplacez tous les boutons dans la nouvelle collection. Faites cela en sélectionnant les cinq objets de bouton dans votre hiérarchie et en les faisant tous glisser sous l’objet de jeu « ButtonCollection », comme illustré dans l’image ci-dessous. Conseil : Sélectionnez plusieurs éléments en maintenant la touche Ctrl enfoncée tout en sélectionnant les éléments.

![Mrlearning Base Ch2 3Step3imb](images/mrlearning-base-ch2-3step3imb.PNG)

4. Ajoutez le composant « Grid Object Collection » (Collection d’objets de grille) du MRTK à la collection de boutons.  Pour cela, sélectionnez l’objet parent « ButtonCollection » puis, dans le panneau de l’inspecteur, cliquez sur le bouton « Add component » (Ajouter un composant). Recherchez ensuite « Grid Object Collection » dans la barre de recherche et sélectionnez-le quand il apparaît dans la liste.

![Mrlearning Base Ch2 3Step4im](images/mrlearning-base-ch2-3step4im.PNG)

Le composant Grid Object Collection vous permet d’organiser des boutons ou un ensemble d’objets dans une ligne, une colonne ou une grille bien ordonnée. Il s’agit d’un des composants fournis par le MRTK qui permet de créer rapidement et simplement de belles interfaces utilisateurs.

5. Configurez la collection d’objets de grille. Pour garantir que tous les boutons font face à l’utilisateur, sélectionnez « orient type » (Type d’orientation), puis « face parent forward » (Face parent vers l’avant), comme illustré dans l’image. Ensuite, changez la taille de la cellule pour définir l’espace entre vos boutons. Commencez par 0,12 unités par 0,12 unités pour la largeur de cellule et la hauteur de cellule, comme illustré dans l’image ci-dessous. Il peut être nécessaire d’ajuster ces valeurs, en fonction des ressources d’objet/de bouton choisies. Vérifiez que « Rows » (Lignes) est défini sur 1. Cliquez ensuite sur « Update Collection » (Mettre à jour la collection) : la scène doit alors ressembler à l’image ci-dessous. 


![Mrlearning Base Ch2 3Step5im](images/mrlearning-base-ch2-3step5im.PNG)

>Remarque: Selon l’orientation des objets enfants ou de l’objet parent, vous devrez probablement ajuster différemment le paramètre d’orientation dans les projets futurs. Il peut également être nécessaire de définir différemment les champs Cell Width (Largeur de cellule) et Cell Height (Hauteur de cellule), en fonction de la taille des objets de votre collection.

### <a name="adding-text-into-your-scene"></a>Ajout de texte dans votre scène

Dans cette section, vous allez découvrir comment ajouter et modifier du texte dans votre expérience de réalité mixte. Si vous ne l’avez pas déjà fait, vérifiez que TextMeshPro est activé dans Unity en suivant les instructions expliquées [ici](https://docs.unity3d.com/Packages/com.unity.textmeshpro@2.0/manual/index.html#installation).

1. Sélectionnez l’objet parent « ButtonCollection », puis cliquez avec le bouton droit sur la collection. Développez « 3D object » dans le menu déroulant, puis sélectionnez « TextMeshPro – Text ». Vous voyez normalement un objet TextMeshPro sous la collection de boutons, comme illustré dans l’image ci-dessous.

![Lesson2 Chapter4 Step1a](images/Lesson2_Chapter4_Step1a.JPG)
![Lesson2 Chapter4 Step1b](images/Lesson2_Chapter4_Step1b.JPG)

2. Dans le champ Text du composant TextMeshPro (situé dans le panneau de l’inspecteur, comme illustré ci-dessous), tapez « Button Collection Text » (Texte de la collection de boutons). Le texte s’affichera dans la scène, mais il sera masqué derrière les boutons et/ou aura une taille incorrecte.

![Lesson2 Chapter4 Step2](images/Lesson2_Chapter4_Step2.JPG)

3. Pour améliorer la taille et l’emplacement du texte pour une meilleure lisibilité, ajustez le champ « font size » (Taille de police) dans le composant TextMeshPro pour changer la taille de la police. Vous devrez également ajuster la position et l’échelle de « Rect Transform » (Transformation du rectangle), comme illustré dans l’image ci-dessous. Regardez les images ci-dessous pour les valeurs utilisées pour la configuration de notre texte : si vous le souhaitez, vous pouvez utiliser ces valeurs comme point de départ, puis améliorer la taille et le positionnement de votre champ de texte.

![Lesson2 Chapter4 Step3](images/Lesson2_Chapter4_Step3.JPG)
![Lesson2 Chapter4 Step4](images/Lesson2_Chapter4_Step4.JPG)

5. Pour modifier les valeurs du texte sur les objets de bouton, cliquez sur la flèche en regard d’un des boutons pour le développer et accédez à l’objet « SeeItSayItLabel », puis accédez à « TextMeshPro », où vous pouvez modifier le texte de vos boutons comme décrit dans les étapes ci-dessus.

![Lesson2 Chapter4 Step5](images/Lesson2_Chapter4_Step5.JPG)

### <a name="congratulations"></a>Félicitations !
Dans cette leçon, vous avez découvert comment copier, personnaliser et configurer un paramètre de profil MRTK (par exemple la visibilité du maillage avec reconnaissance spatiale). Vous avez également découvert comment interagir avec un bouton pour déclencher des événements en utilisant des mains suivies sur HoloLens 2. Enfin, vous avez découvert comment créer une interface utilisateur simple avec Text Mesh Pro d’Unity, le composant de collection d’objets de grille du MRTK.

[Leçon suivante : Placement de contenu dynamique et solveurs](mrlearning-base-ch3.md)

