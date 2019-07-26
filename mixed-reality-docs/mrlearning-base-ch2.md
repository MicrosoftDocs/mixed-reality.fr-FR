---
title: Module de base d’apprentissage de la réalité mixte - Interface utilisateur, suivi manuel et configuration du Kit de ressources de réalité mixte
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 6257b5a4b42127a7f15b235dbdd6b44967684fcb
ms.sourcegitcommit: b086d7a62ee0c7913aa8f66c90e9d2527f270264
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68485756"
---
# <a name="3-creating-user-interface-and-configure-mixed-reality-toolkit"></a>3. Création d’une interface utilisateur et configuration d’une réalité mixte Toolkit 

Dans la leçon précédente, vous avez appris certaines des possibilités offertes par le kit de MRTK (Mixed Reality Toolkit) en démarrant votre première application pour HoloLens 2. Dans cette leçon, vous allez apprendre à créer et à organiser des boutons avec des panneaux de texte d’interface utilisateur et à utiliser l’interaction par défaut (Touch) pour interagir avec chaque bouton. Vous allez également découvrir comment ajouter des actions et des effets simples, comme changer la taille, la sonorité et la couleur des objets. Ce module présente les concepts de base de la modification des profils MRTK, en commençant par la désactivation de la visualisation de maillage spatial. 

## <a name="objectives"></a>Objectifs

* Personnaliser et configurer des profils MRTK
* Interagir avec des hologrammes à l’aide d’éléments d’interface utilisateur et de boutons
* Entrées et interactions de base pour le suivi de la main

## <a name="instructions"></a>Instructions

### <a name="how-to-configure-the-mixed-reality-toolkit-profiles-change-spatial-awareness-display-option"></a>Comment configurer les profils MRTK (Changer l’option d’affichage avec reconnaissance spatiale)
Dans cette section, vous allez apprendre à personnaliser et à configurer les profils MRTK par défaut en ajustant l’option d’affichage du maillage de la sensibilisation spatiale. Vous pouvez suivre ces mêmes principes pour ajuster des paramètres ou des valeurs dans les profils MRTK.

1. Sélectionnez MRTK (Mixed-Reality Toolkit) dans la hiérarchie BaseScene. Dans le panneau Inspecteur, recherchez le script Mixed Reality Toolkit et sélectionnez le profil actif comme indiqué dans la figure ci-dessous. Double-cliquez sur celui-ci pour l’ouvrir.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step1im.PNG)

>Remarque : Par défaut, les profils MRTK ne sont pas modifiables. Il s’agit de modèles de profil par défaut que vous pouvez copier et personnaliser. Il existe plusieurs couches de personnalisation et de profils. Par conséquent, il est recommandé de copier et de personnaliser plusieurs profils lors de la configuration d’un ou de plusieurs paramètres.
>
>Pour en savoir plus sur les profils MRTK et leur architecture, consultez la [documentation de MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Architecture/SpatialAwareness/SpatialAwarenessSystemArchitecture.html>).

2. Créez une copie du profil par défaut pour le personnaliser. Pour copier un profil par défaut, cliquez sur Copier & personnaliser (Voir l’image). Ceci crée une copie du profil MRTK. Avec votre propre copie du profil MRTK, vous pouvez maintenant personnaliser des paramètres de ce profil. Vous devrez également répéter l’étape de copie et de personnalisation pour tous les profils supplémentaires imbriqués sous ce profil, comme décrit dans les étapes suivantes.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step2im.PNG)

3. Désactiver la visibilité du maillage de reconnaissance spatiale. Pour ce faire, recherchez les paramètres système de sensibilisation spatiale comme indiqué dans l’image. Cliquez sur le bouton cloner à droite du profil système de sensibilisation spatiale pour remplacer le profil par défaut par une copie personnalisable. Si une fenêtre contextuelle s’affiche, appuyez sur le bouton Cloner, comme indiqué dans la deuxième image ci-dessous.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step3im.PNG)

![MR213_BuildSettings](images/mrlearning-base-ch2-1step3bim.jpg)

4. Créez une copie personnalisée du « Default Mixed Reality Spatial Mesh Observer » (Observateur du maillage spatial de réalité mixte). Cliquez sur la flèche vers le bas en regard de l’observateur de maillage spatial Windows Mixed realisation pour afficher des options supplémentaires. Dans ces options, vous verrez l’observateur de maillage spatial par défaut de la réalité mixte qui est grisé (non modifiable). Vous devez remplacer ce profil par défaut par une copie personnalisable pour pouvoir le modifier. Cliquez sur le bouton à droite (marqué d’une flèche verte) pour cloner une copie.

![MR213_BuildSettings](images/mrlearning-base-ch2-1step4im.PNG)

5. Ensuite, vous allez ajuster les paramètres pour l’option d’affichage pour indiquer « occlusion ». Cela rend le maillage spatial invisible, mais masque toujours les objets de jeu derrière le maillage spatial, également appelé «occlusion».

![MR213_BuildSettings](images/mrlearning-base-ch2-1step5im.PNG)

>Remarque : Le maillage de mappage spatial n’est pas visible, mais il est toujours présent et vous pouvez interagir avec lui. Tout hologramme derrière le maillage de mappage spatial, tel qu’un hologramme derrière votre mur visible, n’est pas visible en raison du paramètre d’occlusion.

Félicitations ! Vous venez de découvrir comment modifier un paramètre dans le profil MRTK. Comme vous pouvez le voir, pour pouvoir modifier les paramètres du MRTK, vous devez créer des copies des profils par défaut. Vous disposez toujours des profils par défaut, qui ne sont pas modifiables, pour revenir à si vous souhaitez créer un profil avec de nouveaux paramètres, ou vous pouvez vous référer aux profils par défaut. Vous pouvez ajuster de nombreux paramètres. Pour des informations de référence complètes sur les paramètres des profils MRTK, reportez-vous à la documentation du MRTK ici : https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/GettingStartedWithTheMRTK.html

### <a name="hand-tracking-gestures-and-interactable-buttons"></a>Gestes de suivi de la main et boutons d’interaction
Dans cette section, vous allez apprendre à utiliser le suivi de la main pour appuyer sur un bouton enfoncé.

1. Sélectionnez ressources dans le dossier projets.

2. Tapez « pressablebutton » dans la barre de recherche.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step1im.PNG)

3. Faites glisser l’élément préfabriqué (représenté par une zone bleue) nommé « PressableButton » dans votre hiérarchie. 

   > Remarque : Si vous recevez un message d’importation de TMP Essentials, importez-le à ce stade. Si TMP Essentials ne faisait pas déjà partie de votre projet, vous devrez peut-être répéter cette étape après l’importation de TMP Essentials. sinon, le texte du bouton peut ne pas apparaître.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step3im.PNG)

4. Double-cliquez sur l’objet de jeu PressableButton, qui doit maintenant se trouver dans votre hiérarchie BaseScene, pour l’afficher dans votre scène, comme indiqué dans l’image ci-dessous. Les graphiques de bouton peuvent apparaître différents de l’image ci-dessous. 

![MR213_BuildSettings](images/mrlearning-base-ch2-2step4im.PNG)

5. Dans le volet de l’inspecteur, cliquez sur Ajouter un événement pour donner au bouton un événement auquel répondre lorsqu’il est poussé. Dans l’option qui s’affiche, sélectionnez le menu déroulant, puis sélectionnez InteractableOnPressReciever. Ceci permet au bouton de répondre à un événement d’appui quand une main suivie appuie sur le bouton.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step5im.PNG)

6. Ajoutez un cube à la scène. Cliquez avec le bouton droit sur la zone hiérarchie, sélectionnez un objet 3D, puis cliquez sur cube. Un cube doit maintenant se trouver dans votre affichage. Il apparaîtra très grand. Vous pouvez ajuster les coordonnées (tandis que le cube est toujours sélectionné dans la zone de hiérarchie) pour réduire la taille. Définissez comme ceci les valeurs de mise à l’échelle : x = 0,1, y = 0,1 et z = 0,1. Veillez à positionner le cube dans votre scène en le plaçant près du bouton enfonçable, mais sans recouvrir le bouton. Dans l’image ci-dessous, la position du cube est x = 0, y = 0,2 et z = 1. 

   > Remarque : En règle générale, 1 unité dans Unity est à peu près équivalente à 1 mètre dans le monde physique. Il y a des exceptions à cela, par exemple quand les objets sont des enfants d’objets mis à l’échelle.
   
   ![MR213_BuildSettings](images/mrlearning-base-ch2-1step6ima.PNG)

![MR213_BuildSettings](images/mrlearning-base-ch2-2step6imb.PNG)

7. Dans cette étape vous allez configurer le cube pour qu’il change de couleur quand l’utilisateur appuie sur le bouton. Sélectionnez PressableButton dans le menu BaseScene. Dans le panneau Inspecteur, sous la zone Sélectionner un type d’événement, cliquez sur le bouton +. Faites glisser le cube du menu BaseScene dans la zone Runtime only comme indiqué dans l’image ci-dessous.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step7ima.PNG)

Cliquez sur la liste déroulante qui indique aucune fonction. Sélectionnez MeshRenderer, puis matériau matériau. Cela vous permet de modifier la matière lorsque le bouton est enfoncé. 

![MR213_BuildSettings](images/mrlearning-base-ch2-2step7imb.PNG)

Accédez au panneau projet et recherchez le matériel pour lequel vous souhaitez le changer. Pour cet exemple, vous allez utiliser la documentation MRTK_Standard_Cyan, qui se trouve en tapant «cyan» dans la barre de recherche de l’onglet projet. (Le MRTK comprend de nombreux matériaux et couleurs à sélectionner.) Faites glisser le matériau vers la zone sous MeshRenderer. Material. Vous trouverez les matériaux du MRTK dans Assets>MixedRealityToolkit.SDK>StandardAssets>Materials (Ressources>MixedRealityToolkit.SDK>Ressources standard>Matériaux).

![MR213_BuildSettings](images/mrlearning-base-ch2-1step7imc.PNG)

L’événement est maintenant défini : ainsi, quand l’utilisateur appuie sur le bouton, le cube change de couleur en fonction du matériau que vous avez spécifié. Dans cet exemple, la couleur du cube passe à cyan.

8. Ensuite, vous allez configurer l’action liée au relâchement du bouton : ainsi, après le relâchement, le bouton revient à sa couleur par défaut. Répétez l’étape 7 ci-dessus. Mais cette fois, avec l’événement OnRelease au lieu de l’événement OnPress, comme indiqué dans l’image ci-dessous.

9.  Dans le panneau projet, recherchez un matériau pour le cube par défaut en fonction de la version finale du bouton. Dans ce cas, nous avons choisi MRTK_Standard_LightGray. Faites glisser le matériau dans la zone située sous le champ MeshRenderer. Material.

![MR213_BuildSettings](images/mrlearning-base-ch2-2step8im.PNG)

Désormais, lorsque le bouton est enfoncé, il passe à une nouvelle couleur cyan. Lorsque le bouton est relâché, il passe à la couleur par défaut que vous avez spécifiée (par exemple, gris clair). Appuyez sur le bouton de lecture en haut de l’écran pour l’essayer dans l’éditeur ou le déployer sur votre HoloLens 2 pour effectuer un test. Pour en savoir plus sur la simulation dans l’éditeur, y compris la simulation manuelle, lisez la [page de documentation sur la simulation de MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/InputSimulation/InputSimulationService.html>). 

### <a name="creating-a-panel-of-buttons-using-mrtks-grid-object-collection"></a>Création d’un panneau de boutons avec la collection d’objets de grille du MRTK

Dans cette section, vous allez apprendre à aligner automatiquement plusieurs boutons dans une interface utilisateur claire à l’aide de l’outil GridObjectCollection de MRTK.

1. Dupliquez le bouton à partir de la section précédente jusqu’à ce que vous ayez cinq boutons. Il existe plusieurs façons de procéder :
- Cliquez avec le bouton droit sur le bouton, puis cliquez sur copier. Ensuite, accédez au-dessous du bouton et cliquez à nouveau avec le bouton droit, puis cliquez sur coller. 
- Cliquez avec le bouton droit sur le bouton, puis cliquez sur dupliquer. 
- Utilisez la commande clavier en cliquant sur le cube, puis en appuyant sur Ctrl D sur votre clavier.

Répétez cette opération jusqu’à ce que vous ayez cinq boutons. consultez les cinq flèches rouges dans l’image ci-dessous.

![Mrlearning Base Ch2 3Step1im](images/mrlearning-base-ch2-3step1im.PNG)

2. Regroupez les boutons sous un objet de jeu parent vide. Pour que les boutons de la collection de grille s’importent, vous devez regrouper vos boutons sous un objet parent commun. Cliquez avec le bouton droit dans le hiearachy, puis cliquez sur créer vide. Ceci crée un objet de jeu vide où vous pouvez placer tous les boutons. Il s’affiche sous la forme gameObject. Cliquez avec le bouton droit et renommez-le, ButtonCollection.

![Mrlearning Base Ch2 3Step2im](images/mrlearning-base-ch2-3step2im.PNG)

3. Déplacez tous les boutons dans la nouvelle collection. Pour ce faire, sélectionnez les cinq objets de bouton dans votre hiérarchie et faites-les glisser tous sous l’objet de jeu ButtonCollection comme indiqué dans l’image ci-dessous. Conseil: sélectionnez plusieurs éléments en maintenant la touche CTRL enfoncée tout en sélectionnant des éléments.

![Mrlearning Base Ch2 3Step3imb](images/mrlearning-base-ch2-3step3imb.PNG)

4. Ajoutez le composant de collection d’objets Grid de MRTK à la collection de boutons. Pour ce faire, sélectionnez l’objet parent ButtonCollection. Dans le panneau de l’inspecteur, cliquez sur le bouton Ajouter un composant. Recherchez la collection d’objets Grid dans la barre de recherche, puis sélectionnez-la lorsqu’elle apparaît dans la liste.

![Mrlearning Base Ch2 3Step4im](images/mrlearning-base-ch2-3step4im.PNG)

Le composant de collection d’objets grille vous permet d’organiser des boutons ou un ensemble d’objets dans une ligne, une colonne ou une grille soignée. Il s’agit de l’un des blocs de construction fournis par le MRTK qui vous offre un moyen simple et rapide de créer des interfaces utilisateur attrayantes.

5. Configurez la collection d’objets de grille. Pour vous assurer que tous les boutons sont en face de l’utilisateur, sélectionnez orienter le type. Sélectionnez ensuite face parent Forward comme indiqué dans l’image ci-dessous. Ensuite, changez la taille de la cellule pour définir l’espace entre vos boutons. Commencez par 0,12 unités par 0,12 unités pour la largeur de cellule et la hauteur de cellule comme indiqué dans l’image ci-dessous. Vous devrez peut-être ajuster ces valeurs en fonction des ressources d’objet et de bouton qui ont été choisies. Assurez-vous que lignes a la valeur 1. Cliquez sur mettre à jour la collection. La scène ressemble à l’image ci-dessous. 


![Mrlearning Base Ch2 3Step5im](images/mrlearning-base-ch2-3step5im.PNG)

>Remarque : Selon l’orientation des objets enfants ou de l’objet parent, vous devrez probablement ajuster différemment le paramètre d’orientation dans les projets futurs. Il peut également être nécessaire de définir différemment les champs Cell Width (Largeur de cellule) et Cell Height (Hauteur de cellule), en fonction de la taille des objets de votre collection.

### <a name="adding-text-into-your-scene"></a>Ajout de texte dans votre scène

Dans cette section, vous allez découvrir comment ajouter et modifier du texte dans votre expérience de réalité mixte. Si vous ne l’avez pas déjà fait, vérifiez que TextMeshPro est activé dans Unity en suivant les instructions expliquées [ici](https://docs.unity3d.com/Packages/com.unity.textmeshpro@2.0/manual/index.html#installation).

1. Sélectionnez l’objet parent ButtonCollection, puis cliquez avec le bouton droit sur le regroupement. Développez objet 3D dans le menu déroulant. Sélectionnez ensuite TextMeshPro-Text. Vous devez voir un objet TextMeshPro sous la collection de boutons comme indiqué dans l’image ci-dessous.

![Lesson2 Chapter4 Step1a](images/Lesson2_Chapter4_Step1a.JPG)
![Lesson2 Chapter4 Step1b](images/Lesson2_Chapter4_Step1b.JPG)

2. Pour améliorer la taille et le positionnement du texte, ajustez le champ Taille de la police dans le composant TextMeshPro pour modifier la taille de la police. Vous devrez également ajuster la position de la transformation Rect et l’échelle comme indiqué dans l’image ci-dessous. Consultez les images ci-dessous pour connaître les valeurs utilisées pour la configuration de votre texte. N’hésitez pas à utiliser ces valeurs comme point de départ pour améliorer davantage la taille et l’emplacement de votre champ de texte.

![Lesson2 chapter4 step3](images/Lesson2_Chapter4_Step3.JPG)

3. Dans le champ de texte du composant TextMeshPro du panneau Inspecteur, comme indiqué ci-dessous. Tapez le texte de la collection de boutons. Le texte apparaît dans la scène, mais il est masqué derrière les boutons et/ou la mauvaise taille.

![Lesson2 chapter4 étape 2](images/Lesson2_Chapter4_Step2.JPG)
![Lesson2 chapter4 étape 4](images/Lesson2_Chapter4_Step4.JPG)

4. Pour modifier les valeurs de texte sur les objets bouton, cliquez sur la flèche en regard de n’importe quel bouton pour la développer et accéder à l’objet SeeItSayItLabel. Accédez à TextMeshPro où vous pouvez modifier le texte en fonction de vos boutons, comme décrit dans les étapes ci-dessus.

![Lesson2 Chapter4 Step5](images/Lesson2_Chapter4_Step5.JPG)

## <a name="congratulations"></a>Félicitations !
Dans cette leçon, vous avez découvert comment copier, personnaliser et configurer un paramètre de profil MRTK (par exemple la visibilité du maillage avec reconnaissance spatiale). Vous avez également découvert comment interagir avec un bouton pour déclencher des événements en utilisant des mains suivies sur HoloLens 2. Enfin, vous avez découvert comment créer une interface utilisateur simple avec Text Mesh Pro d’Unity, le composant de collection d’objets de grille du MRTK.

[Leçon suivante : 4. Placement du contenu dynamique et utilisation de solveurs](mrlearning-base-ch3.md)

