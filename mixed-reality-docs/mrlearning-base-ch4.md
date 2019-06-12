---
title: Module de base d’apprentissage de la réalité mixte - Interaction avec des objets 3D
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 45e772de0825fe2161f880a165d6c75c755b849e
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "65730909"
---
# <a name="mr-learning-base-module---3d-object-interaction"></a>Module de base d’apprentissage de la réalité mixte - Interaction avec des objets 3D

Dans cette leçon, nous allons aborder les bases du contenu et de l’expérience utilisateur 3D. Nous allons découvrir comment organiser les objets 3D dans le cadre d’une collection, et découvrir des informations sur les cadres englobants pour la manipulation de base, l’interaction de près et de loin, les gestes tactiles et de préhension avec le suivi de la main. 

## <a name="objectives"></a>Objectifs

* Découvrir comment organiser le contenu 3D avec la collection d’objets de grille du MRTK
* Implémenter des cadres englobants
* Configurer des objets 3D pour la manipulation de base (déplacement, rotation et mise à l’échelle)
* Explorer l’interaction de près et de loin
* Découvrir des informations sur les gestes de suivi de la main, comme la préhension et l’interaction tactile

## <a name="instructions"></a>Instructions

### <a name="organizing-3d-objects-in-a-collection"></a>Organisation des objets 3D dans une collection

1. Cliquez avec le bouton droit sur votre hiérarchie et sélectionnez « create empty » (Créer vide). Ceci crée un objet de jeu vide. Renommez-le en « 3DObjectCollection ». C’est là où nous allons placer tous nos objets 3D. Vérifiez que le positionnement de la collection est défini sur x = 0, y = 0 et z = 0.

![Lesson4 Chapter1 Step1im](images/Lesson4_Chapter1_step1im.PNG)

2. Importez les ressources de BaseModule en suivant les mêmes instructions pour importer des packages personnalisés que celles décrites dans [Lesson1](mrlearning-base-ch1.md). Les ressources de BaseModule incluent des modules 3D et d’autres scripts utiles qui seront utilisés dans ce tutoriel. Vous trouverez le package Unity BaseModule ici : <https://github.com/Microsoft/MixedRealityLearning/releases/tag/V1.1>

3. L’élément préfabriqué figurant une tasse de café peut être identifié grâce au cube bleu figurant en regard de celui-ci. Ne sélectionnez pas la tasse de café avec le cube bleu et le petit papier blanc (qui indique le modèle 3D d’origine et pas l’élément préfabriqué.) 

![Lesson4 Chapter1 Noteaim](images/Lesson4_chapter1_noteaim.PNG)

4. Faites glisser l’élément préfabriqué figurant une tasse de café de votre choix dans l’objet de jeu « 3DObjectCollection » de l’étape 1. La tasse de café est maintenant un enfant de la collection.

![Lesson4 Chapter1 Step4ima](images/Lesson4_chapter1_step4ima.PNG)

5. Ensuite, nous allons ajouter davantage d’objets 3D dans notre scène. Voici une liste d’objets, que nous allons ajouter dans cet exemple. Quand vous ajoutez les objets, vous pouvez constater qu’ils apparaissent dans votre scène dans différentes tailles. Ajustez l’échelle de chaque modèle 3D sous le paramètre de transformation dans le panneau de l’inspecteur. Les ajustements recommandés pour cet exemple sont listés avec les objets ci-dessous. Recherchez ces mots dans la zone de recherche du panneau de votre projet et faites glisser l’élément préfabriqué de l’objet 3D dans l’objet « 3DObjectCollection » d’une façon similaire à l’étape précédente. Vous trouverez cette collection de préfabriqués dans Assets>BaseModuleAssets>Base Module Prefabs (Ressources>Ressources du module de base>Préfabriqués du module de base)
- Recherchez « TheModule_BaseModuleIncomplete ». Faites-le glisser dans la scène. Définissez l’échelle sur x = 0,03, y = 0,03, z = 0,03. 
- Recherchez « Octa_BaseModuleIncomplete ». Faites-le glisser dans la scène. Définissez l’échelle sur x = 0,13, y = 0,13, z =0,13.
- Recherchez « EarthCore_BaseModuleIncomplete ». Faites-le glisser dans la scène. Définissez l’échelle sur x = 50,0, y = 50,0, z = 50,0.
- Recherchez « Cheese_BaseModuleIncomplete ». Faites-le glisser dans la scène. Définissez l’échelle sur x = 0,05, y = 0,05, z = 0,05.
- Recherchez « Model_Platonic_BaseModuleIncomplete ». Faites-le glisser dans la scène. Définissez l’échelle sur x = 0,13, y = 0,13, z = 0,13.
- Recherchez « CoffeeCup_BaseModuleIncomplete ». Faites-le glisser dans la scène.

![Lesson4 Chapter1 Step5im](images/Lesson4_Chapter1_step5im.PNG)

6. Ajoutez 3 cubes dans votre scène. Cliquez avec le bouton droit sur l’objet « 3DObjectCollection », sélectionnez « 3D Object » (Objet 3D), puis sélectionnez « Cube ». Définissez l’échelle sur x = 0,14, y = 0,14 et z = 0,14. Répétez cette étape 2 fois pour créer un total de 3 cubes. Vous pouvez également dupliquer le cube à deux reprises pour obtenir un total de 3 cubes. Vous pouvez également choisir d’utiliser les trois cubes préfabriqués préparés à partir Assets>BaseModuleAssets>Base Module Prefab (Ressources>Ressources du module de base>Préfabriqué du module de base) et sélectionner GreenCube_BaseModuleIncomplete, BlueCube_BaseModuleIncomplete et OrangeCube_BaseModuleIncomplete.

![Lesson4 Chapter1 Step6im](images/Lesson4_Chapter1_step6im.PNG)

7. Organisez votre collection d’objets pour former une grille selon la procédure décrite dans [Leçon 2](mrlearning-base-ch2.md) avec la collection d’objets de grille du MRTK. Reportez-vous à l’image ci-dessous pour voir un exemple de configuration des objets dans une grille de 3x3.

![Lesson4 Chapter1 Notebim](images/Lesson4_chapter1_notebim.PNG)

>Remarque: Vous pouvez remarquer que certains objets ne sont pas centrés, comme les objets de l’image ci-dessus. La raison en est que des préfabriqués ou des objets peuvent avoir des objets enfants qui ne sont pas alignés. N’hésitez pas à effectuer les ajustements nécessaires des positions des objets ou des objets enfants pour obtenir une grille bien alignée.


### <a name="manipulating-3d-objects"></a>Manipulation d’objets 3D
1. Ajoutez la possibilité de manipuler un cube. Pour ajouter la possibilité de manipuler des objets 3D, vous devez procédez comme suit :
-   Sélectionnez l’objet 3D que vous voulez manipuler dans votre hiérarchie (dans cet exemple, un de vos cubes).
-   Cliquez sur « add component » (Ajouter un composant). 
-   Recherchez « manipulation ».
-   Sélectionnez « manipulation handler » (Gestionnaire de manipulation).
-   Répétez ces étapes pour tous les objets 3D sous l’objet « 3DObjectCollection », mais pas pour l’objet « 3DObjectCollection » lui-même.
-   Vérifiez tous les objets 3D ont un collisionneur ou un cadre de collisionneur (Add Component > box collider) (Ajouter un composant > Cadre de collisionneur).

![Lesson4 Chapter2 Step1im](images/Lesson4_chapter2_step1im.PNG)

>Le gestionnaire de manipulation est un composant qui vous permet d’ajuster les paramètres déterminant comment les objets se comportent quand ils sont manipulés. Ceci inclut la rotation, la mise à l’échelle, le déplacement et les mouvements de contrainte sur certains axes. 

2. Limitez les possibilités sur un cube à la seule mise à l’échelle. Sélectionnez un cube dans l’objet « 3DObjectCollection ». Dans le panneau de l’inspecteur, en regard de « two handed manipulation type » (Type de manipulation à deux mains), cliquez sur le menu déroulant et sélectionnez « scale » (Mettre à l’échelle). Ceci fait que l’utilisateur peut seulement changer la taille du cube.

![Lesson4 Chapter2 Step2im](images/Lesson4_Chapter2_step2im.PNG)

3. Changez la couleur de chaque cube de façon à pouvoir les différencier. 
-   Accédez au panneau du projet et faites défiler jusqu’à voir « MixedRealityToolkit.SDK », puis sélectionnez-le.
-   Sélectionnez le dossier « Standard Assets ».
-   Cliquez sur le dossier « materials ».
-   Faites glisser un matériau différent sur chacun de vos cubes. 

>Remarque: Vous pouvez choisir n’importe quelle couleur pour vos cubes. Dans notre exemple, nous allons utiliser « glowingcyan », « glowingorange » et « green ». N’hésitez pas à faire des essais avec différentes couleurs. Pour ajouter la couleur au cube, cliquez sur le cube dont vous voulez changer la couleur, puis faites glisser le matériau vers le champ material (Matériau) de l’afficheur du maillage dans le panneau de l’inspecteur du cube. 

![Lesson4 Chapter2 Step3im](images/Lesson4_Chapter2_step3im.PNG)

4. Sélectionnez un autre cube dans l’objet « 3DObjectCollection » et faites en sorte que son déplacement soit limité à une distance fixe de la tête. Pour cela, sur la droite de « constraint on movement » (Contrainte sur le déplacement), cliquez sur le menu déroulant et sélectionnez « fix distance from the head » (Distance fixe de la tête). Ceci fait que l’utilisateur peut déplacer le cube seulement dans son champ de vision. 

![Lesson4 Chapter2 Step4im](images/Lesson4_chapter2_step4im.PNG)

Objectif des étapes suivantes : Nous allons activer la préhension et l’interaction avec nos objets 3D. Nous allons appliquer différents paramètres de manipulation. 

5. Sélectionnez l’objet « cheese » (Fromage) et, dans le panneau de l’inspecteur, cliquez sur « add component » (Ajouter le composant). 

6. Recherchez « Near Interaction Grabbable » (Interaction de près avec préhension) et sélectionnez le script. Ce composant permet aux utilisateurs d’atteindre et de saisir les objets avec des mains suivies. Les objets peuvent aussi être manipulés à une certaine distance, sauf si la case « Allow Far Manipulation » (Autoriser la manipulation de loin) est décochée (indiqué par un cercle vert dans l’image ci-dessous).

![Lesson4 Chapter2 Step6im](images/Lesson4_Chapter2_step6im.PNG)

7. Ajoutez « Near Interaction Grabbable » à l’objet Octa, à l’objet Platonic, au noyau terrestre, au module lunaire et à la tasse de café, en répétant les étapes 5 et 6 sur ces objets.

8. Supprimez la possibilité de manipulation de loin sur l’objet Octa. Pour cela, sélectionnez l’objet Octa dans la hiérarchie et décochez la case « allow far manipulation » (indiquée par un cercle vert). Ceci fait que les utilisateurs peuvent interagir directement avec l’objet Octa seulement en utilisant les mains suivies.

>Remarque: Pour la documentation complète du composant Gestionnaire de manipulation et de ses paramètres associés, reportez-vous à la [Documentation du MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html).

9. Vérifiez que le composant « Near Interaction Grabbable » a été ajouté au noyau terrestre, au module lunaire et à la tasse de café (voir l’étape 7).

10. Pour le module lunaire, changez les paramètres du Gestionnaire de manipulation de façon à ce qu’il pivote autour du centre de l’objet pour les interactions de près et de loin, comme illustré dans l’image ci-dessous.

![Lesson4 Chapter2 Step10im](images/Lesson4_chapter2_step10im.PNG)

11 : Pour le noyau terrestre, changez le comportement de relâchement en « nothing » (Rien). Ceci fait qu’une fois le noyau terrestre libéré de la préhension des utilisateurs, il ne continue pas de se déplacer. 

![Lesson4 Chapter2 Step11im](images/Lesson4_Chapter2_step11im.PNG)

> Remarque: Ce paramètre est utile pour des scénarios comme la création d’une balle que vous pouvez lancer. Conserver la vitesse et la vitesse angulaire fait qu’une fois la balle lâchée, elle continue de se déplacer à la vitesse à laquelle elle a été lâchée, en se comportant de façon similaire à une balle physique.

### <a name="adding-bounding-boxes"></a>Ajout de cadres englobants
Les cadres englobants rendent plus facile et plus intuitive la manipulation des objets avec une seule main pour la manipulation directe (interaction de près) et pour la manipulation basée sur un rayon (interaction de loin). Les cadres englobants offrent des « poignées » qui peuvent être saisies pour la mise à l’échelle et la rotation des objets le long d’axes spécifiques.
>Remarque: Avant de pouvoir ajouter un cadre englobant à un objet, vous devez d’abord disposer d’un collisionneur sur l’objet (par exemple un cadre de collisionneur). Nous avons fait cela précédemment dans cette leçon. Vous pouvez ajouter des collisionneurs en sélectionnant l’objet puis, dans le panneau de l’inspecteur de l’objet, en sélectionnant Add Component>Box Collider (Ajouter un composant>Cadre de collisionneur).
>

1. Ajoutez un cadre de collisionneur à l’objet de noyau terrestre s’il n’existe pas déjà (le cadre de collisionneur et la configuration ne sont pas nécessaires si vous utilisez l’élément préfabriqué fourni dans le dossier Base Module Assets, conformément aux instructions fournies). Dans le cas du noyau terrestre, nous devons ajouter le cadre de collisionneur à l’objet « node_id30 » sous le noyau terrestre, comme illustré dans l’image ci-dessous. Sélectionnez node_id30 et, dans l’onglet Inspecteur de l’objet, cliquez sur « add component » et recherchez « box collider » (Cadre de collisionneur). 

![Lesson4 Chapter3 Step1im](images/Lesson4_Chapter3_step1im.PNG)

![Lesson4 Chapter3 Step2im](images/Lesson4_chapter3_step2im.PNG)

> Remarque: Veillez à visualiser le cadre de collisionneur de façon à ce qu’il ne soit ni trop grand ni trop petit. Il doit avoir à peu près la même taille que l’objet qu’il entoure (dans cet exemple, le noyau terrestre). Ajustez le cadre de collisionneur selon les besoins en sélectionnant l’option de modification du collisionneur dans le cadre de collisionneur. Vous pouvez changer les valeurs de x, y et z, ou faire glisser les poignées du cadre englobant dans la fenêtre de l’éditeur de scène. 

![Lesson4 Chapter3 Noteim](images/Lesson4_Chapter3_noteim.PNG)

2. Ajoutez un cadre englobant à l’objet « node_id30 » du noyau terrestre. Pour cela, sélectionnez l’objet « node_id30 » dans « 3DObjectCollection ». Dans le panneau de l’inspecteur, cliquez sur « add component » et recherchez « bounding box ». Vérifiez que le cadre englobant, le cadre de collisionneur et les scripts de manipulation (gestionnaire de manipulation, interaction de près avec préhension) sont tous sur le même objet de jeu.

3.  Dans la section « Behavior » (Comportement) du cadre englobant, sélectionnez « activate on start » (Activer au démarrage) dans la liste déroulante Activation. Pour passer en revue les détails supplémentaires concernant les différentes options d’activation et les autres options du cadre englobant, consultez la [documentation du cadre englobant du MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html>)

   

   *Dans les prochaines étapes, nous allons aussi changer l’aspect du cadre englobant en ajustant le matériau par défaut du cadre, le matériau qui apparaît pendant la préhension ainsi que la visualisation des poignées (poignées d’angle et latérales). Le MRTK contient plusieurs options permettant de personnaliser le cadre englobant.*

4. Dans le panneau du projet, recherchez « boundingbox » : vous voyez alors une liste des matériaux indiquée par une sphère bleue dans les résultats de la recherche, comme illustré dans l’image ci-dessous. 

5. Faites glisser le matériau « boundingbox » dans l’emplacement des matériaux du cadre sur le composant Cadre englobant. Prenez aussi le matériau « boundingboxgrabbed » et placez-le à l’emplacement des matériaux sélectionnés du cadre sur le composant Cadre englobant.

6. Faites glisser le matériau « MRTK_BoundingBox_ScaleWidget » à l’emplacement des éléments préfabriqués des poignées de mise à l’échelle sur le composant Cadre englobant. 

7. Faites glisser le matériau « MRTK_BoundingBox_RotateWidget » à l’emplacement des éléments préfabriqués des poignées de rotation sur le composant Cadre englobant.

![Lesson4 Chapter3 Step4 7Im](images/Lesson4_chapter3_step4-7im.PNG)

8. Vérifiez que le cadre englobant cible le bon objet. Le composant Cadre englobant contient un « objet cible » et des scripts de « remplacement des limites ». Veillez à faire glisser l’objet entouré par le cadre englobant à ces deux emplacements. Dans cet exemple, faites glisser l’objet « node_id30 » à ces deux emplacements, comme illustré dans l’image ci-dessous.

> Quand vous démarrez ou que vous exécutez l’application, votre objet sera entouré d’un encadrement bleu. Vous pouvez faire glisser les coins de cet encadrement pour redimensionner l’objet. Si nous voulons que les poignées de mise à l’échelle et les poignées de rotation soient plus grandes et plus visibles, nous vous recommandons d’utiliser les paramètres par défaut du cadre englobant (en évitant les étapes 4 à 7). 

![Lesson4 Chapter3 Step8im](images/Lesson4_Chapter3_step8im.PNG)

9. Pour revenir à la visualisation du cadre englobant par défaut, dans le panneau de l’inspecteur de l’objet Cadre englobant, sélectionnez l’élément préfabriqué de poignée de rotation et appuyez sur la touche Suppr : vous voyez maintenant une visualisation du cadre englobant similaire à l’image ci-dessous. Remarque : Les visualisations des cadres englobants apparaissent seulement en mode lecture.

![Lesson4 Chapter3 Step9im](images/Lesson4_chapter3_step9im.PNG)

### <a name="adding-touch-effects"></a>Ajout d’effets tactiles
Dans cet exemple, nous allons émettre un son quand vous touchez un objet avec votre main.

1. Ajoutez un composant Source audio à votre objet de jeu. Sélectionnez l’objet « octa » dans la hiérarchie de votre scène. Dans le panneau de l’inspecteur, cliquez sur le bouton « add component », puis recherchez et sélectionnez « audio source ». Nous allons utiliser cette source audio pour produire un effet sonore dans une étape ultérieure. 

>Remarque: Vérifiez qu’un cadre de collisionneur est placé sur l’objet « Octa ».

2. Ajoutez le composant « near interaction touchable » (Interaction tactile de près). Cliquez sur le bouton « Add Component » dans le panneau de l’inspecteur et recherchez « near interaction touchable ». Sélectionnez-le pour ajouter le composant. REMARQUE : corriger la capture d’écran pour mettre en évidence le fait que nous ajoutons le composant, et ne pas seulement mettre en évidence le cadre de collisionneur.

>Remarque: Précédemment, nous avons ajouté « near interaction grabbable. » La différence entre ceci et « near interaction touchable » est que l’interaction « grabbable » est destinée à la préhension et à l’interaction avec un objet. Le composant « touchable » (tactile) a est destiné à être utilisé pour toucher l’objet. Les deux composants peuvent être utilisés ensemble pour une combinaison d’interactions.

![Lesson4 Chapter4 Step1 2Im](images/Lesson4_chapter4_step1-2im.PNG)

3. Ajoutez le script « hand interaction touch » (Interaction tactile avec la main). Notez que ce script est inclus dans la scène Unity que vous avez importée dans le cadre de ce package de démonstration et qu’il n’est pas inclus dans le MRTK d’origine. Tout comme à l’étape précédente, cliquez sur « add component » et recherchez « hand interaction touch » pour l’ajouter. 
   Notez que vous disposez de 3 options avec le script : 

   - « On touch completed » (À la fin de l’interaction tactile) Ceci va déclencher quand vous touchez et que vous relâchez l’objet. 
   - « On touch started » (Au début de l’interaction tactile) Ceci va déclencher quand vous touchez l’objet. 
   - « On touch updated » (À la mise à jour de l’interaction tactile) Ceci va déclencher périodiquement pendant que votre main touche l’objet. 

   Pour cet exemple, nous allons utiliser le paramètre « on touch started ».

4. Cliquez sur le bouton « + » sur l’option « on touch started », comme illustré dans l’image ci-dessous. Faites glisser l’objet « Octa » dans le champ vide. 

5. Dans la liste déroulante indiquant « no function » (pas de fonction) (en haut du rectangle vert dans l’image ci-dessous), sélectionnez AudioSource > PlayOneShot. Nous allons ajouter un clip audio à ce champ en utilisant les concepts ci-dessous :

   - Le MRTK fournit-il une petite liste de clips audio. N’hésitez pas à explorer ces éléments dans le panneau de votre projet. Vous les trouverez sous le dossier « MixedRealityToolkit.SDK », dans le dossier « standard assets ». Vous y verrez un dossier « audio » qui contient tous les clips audio.
   - Pour cet exemple, nous allons utiliser le clip audio « MRTK_Gem ». 
   - Pour ajouter un clip audio, faites simplement glisser le clip souhaité à partir du panneau du projet dans AudioSource.PlayOneShot (marqué par le rectangle vert dans l’exemple ci-dessus) dans le panneau de l’inspecteur.

   Maintenant, quand l’utilisateur atteint et touche l’objet « octa », le clip audio « MRTK_Gem » est joué. Le script « Hand Interaction Touch » ajuste également la couleur de l’objet quand il est touché. 

![Lesson4 Chapter4 Step3 5 Noteim](images/Lesson4_chapter4_step3-5-noteim.PNG)

### <a name="congratulations"></a>Félicitations ! 
Dans cette leçon, vous avez découvert comment organiser des objets 3D dans une collection de grille et comment manipuler des objets 3D (mise à l’échelle, rotation et déplacement) en utilisant l’interaction de près (en saisissant directement avec les mains suivies) et l’interaction de loin (en utilisant des rayons de suivi ou des rayons de main). Vous avez aussi découvert comment placer des cadres englobants autour des objets 3D, et comment utiliser et personnaliser les éléments sur les cadres englobants. Enfin, vous avez découvert comment déclencher des événements quand l’utilisateur touche un objet.

[Leçon suivante : Entrée avancée](mrlearning-base-ch5.md)

