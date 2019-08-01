---
title: Didacticiels de mise en route-5. Interaction avec les objets 3D
description: ''
author: jessemcculloch
ms.author: jemccull
ms.date: 05/02/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 29a31f794cbcda4f0c77b4e6e2d0e3c2c91dcb8c
ms.sourcegitcommit: af1602710c1ccb7ed870a491923350d387706129
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702016"
---
# <a name="5-interacting-with-3d-objects"></a>5. Interaction avec les objets 3D

Dans ce didacticiel, nous allons découvrir le contenu 3D de base et l’expérience utilisateur. Nous aborderons les éléments suivants: 
* Organisation des objets 3D dans le cadre d’une collection.
* Zones englobantes pour la manipulation de base.
* Interaction proche et éloignée.
* Mouvements tactiles et de manipulation avec suivi de la main. 

## <a name="objectives"></a>Objectifs

* Découvrez comment organiser le contenu 3D avec la collection d’objets Grid de MRTK
* Implémenter des cadres englobants
* Configurer des objets 3D pour la manipulation de base--déplacer, faire pivoter et mettre à l’échelle
* Explorer l’interaction de près et de loin
* En savoir plus sur les gestes supplémentaires de suivi de la main, tels que la manipulation et la saisie tactile

## <a name="instructions"></a>Instructions

### <a name="organizing-3d-objects-in-a-collection"></a>Organisation des objets 3D dans une collection

1. Cliquez avec le bouton droit sur votre hiérarchie et sélectionnez, créer un vide. Ceci crée un objet de jeu vide. Renommez-le 3DObjectCollection. C’est là où nous allons placer tous nos objets 3D. Vérifiez que le positionnement de la collection est défini sur x = 0, y = 0 et z = 0.

![Lesson4 Chapter1 Step1im](images/Lesson4_Chapter1_step1im.PNG)

2. Importez des ressources BaseModule en utilisant les mêmes instructions pour importer des packages personnalisés décrits dans [Lesson1](mrlearning-base-ch1.md). Les ressources BaseModule incluent des modules 3D et d’autres scripts utiles utilisés tout au long de ce didacticiel. Le package BaseModule Unity se trouve ici:<https://github.com/Microsoft/MixedRealityLearning/releases/tag/V1.1>

3. L’élément préfabriqué figurant une tasse de café peut être identifié grâce au cube bleu figurant en regard de celui-ci. Ne sélectionnez pas la tasse de café avec le cube bleu et un petit livre blanc, car cela dénote le modèle 3D d’origine et non pas le Prefab. 

![Lesson4 Chapter1 Noteaim](images/Lesson4_chapter1_noteaim.PNG)

4. Faites glisser le Prefab café de votre choix dans l’objet de jeu 3DObjectCollection de l’étape 1. La tasse de café est maintenant un enfant de la collection.

![Lesson4 Chapter1 Step4ima](images/Lesson4_chapter1_step4ima.PNG)

5. Ensuite, nous allons ajouter davantage d’objets 3D dans notre scène. Voici une liste d’objets, que nous allons ajouter dans cet exemple. À mesure que vous ajoutez les objets, vous pouvez constater qu’ils apparaissent dans votre scène dans différentes tailles. Ajustez l’échelle de chaque modèle 3D sous le paramètre transformer dans le panneau Inspecteur. Les ajustements recommandés pour cet exemple sont listés avec les objets ci-dessous. Recherchez ces mots dans la zone de recherche dans le panneau projet, puis faites glisser l’objet 3D Prefab dans l’objet 3DObjectCollection similaire à l’étape précédente. Vous trouverez ces collections de prefabs dans Ressources > BaseModuleAssets > module de base Prefabs
- Recherchez TheModule_BaseModuleIncomplete. Faites-le glisser dans la scène. Définissez l’échelle sur x = 0,03, y = 0,03, z = 0,03. 
- Recherchez Octa_BaseModuleIncomplete. Faites-le glisser dans la scène. Définissez l’échelle sur x = 0,13, y = 0,13, z =0,13.
- Recherchez EarthCore_BaseModuleIncomplete. Faites-le glisser dans la scène. Définissez l’échelle sur x = 50,0, y = 50,0, z = 50,0.
- Recherchez Cheese_BaseModuleIncomplete. Faites-le glisser dans la scène. Définissez l’échelle sur x = 0,05, y = 0,05, z = 0,05.
- Recherchez Model_Platonic_BaseModuleIncomplete. Faites-le glisser dans la scène. Définissez l’échelle sur x = 0,13, y = 0,13, z = 0,13.

![Lesson4 Chapter1 Step5im](images/Lesson4_Chapter1_step5im.PNG)

6. Ajoutez trois cubes à votre scène. Cliquez avec le bouton droit sur l’objet 3DObjectCollection, sélectionnez objet 3D, puis sélectionnez cube. Définissez l’échelle sur x = 0,14, y = 0,14 et z = 0,14. Répétez cette étape deux fois supplémentaires pour créer un total de trois cubes. Vous pouvez également dupliquer le cube deux fois pour un total de trois cubes. Vous pouvez également choisir d’utiliser les trois cubes préfabriqués préparés à partir Assets>BaseModuleAssets>Base Module Prefab (Ressources>Ressources du module de base>Préfabriqué du module de base) et sélectionner GreenCube_BaseModuleIncomplete, BlueCube_BaseModuleIncomplete et OrangeCube_BaseModuleIncomplete.

![Lesson4 Chapter1 Step6im](images/Lesson4_Chapter1_step6im.PNG)

7. Organisez votre collection d’objets pour former une grille selon la procédure décrite dans [Leçon 2](mrlearning-base-ch2.md) avec la collection d’objets de grille du MRTK. Reportez-vous à l’image ci-dessous pour voir un exemple de configuration des objets dans une grille de 3x3.

![Lesson4 Chapter1 Notebim](images/Lesson4_chapter1_notebim.PNG)

>Remarque : Vous remarquerez peut-être que certains objets sont décentrés, tels que les objets de l’image ci-dessus. La raison en est que des préfabriqués ou des objets peuvent avoir des objets enfants qui ne sont pas alignés. N’hésitez pas à effectuer les ajustements nécessaires des positions des objets ou des objets enfants pour obtenir une grille bien alignée.


### <a name="manipulating-3d-objects"></a>Manipulation d’objets 3D
1. Ajoutez la possibilité de manipuler un cube. Pour ajouter la possibilité de manipuler des objets 3D, procédez comme suit:
-   Sélectionnez l’objet 3D que vous souhaitez manipuler dans votre hiérarchie, c’est-à-dire l’un de vos cubes.
-   Cliquez sur Ajouter un composant. 
-   Recherche de manipulation.
-   Sélectionnez le gestionnaire de manipulation.
-   Répétez cette opération pour tous les objets 3D sous l’objet 3DObjectCollection, mais pas le 3DObjectCollection lui-même.
-   Vérifiez que tous les objets 3D comportent un conflit de collision ou de boîte (ajouter un composant > un conflit de boîte).

![Lesson4 Chapter2 Step1im](images/Lesson4_chapter2_step1im.PNG)

>Le gestionnaire de manipulation est un composant qui vous permet d’ajuster les paramètres de comportement des objets lorsqu’ils sont manipulés. Cela comprend la rotation, la mise à l’échelle, le déplacement et la limitation du mouvement sur un axe spécifique. 

2. Limitez les possibilités sur un cube à la seule mise à l’échelle. Sélectionnez un cube dans l’objet 3DObjectCollection. Dans le volet de l’inspecteur, en regard de deux types de manipulations de la main, cliquez sur le menu déroulant et sélectionnez mettre à l’échelle. Ceci fait que l’utilisateur peut seulement changer la taille du cube.

![Lesson4 Chapter2 Step2im](images/Lesson4_Chapter2_step2im.PNG)

3. Changez la couleur de chaque cube de façon à pouvoir les différencier. 
-   Accédez au panneau projet et faites défiler jusqu’à ce que vous voyez MixedRealityToolkit. SDK, puis sélectionnez-le.
-   Sélectionnez le dossier ressources standard.
-   Cliquez sur le dossier matériaux.
-   Faites glisser un matériau différent sur chacun de vos cubes. 

>Remarque : Vous pouvez choisir n’importe quelle couleur pour vos cubes. Pour notre exemple, nous allons utiliser glowingcyan, glowingorange et Green. N’hésitez pas à faire des essais avec différentes couleurs. Pour ajouter la couleur au cube, cliquez sur le cube que vous souhaitez modifier, puis faites glisser le matériau vers le champ Material du convertisseur de maillage dans le panneau inspecteur du cube. 

![Lesson4 Chapter2 Step3im](images/Lesson4_Chapter2_step3im.PNG)

4. Sélectionnez un autre cube dans l’objet 3DObjectCollection et faites-le pour que son mouvement soit restreint à une distance fixe à partir de l’en-tête. Pour ce faire, à droite de l’étiquette de contrainte sur le mouvement, cliquez sur le menu déroulant et sélectionnez corriger la distance à partir de la tête. Ceci fait que l’utilisateur peut déplacer le cube seulement dans son champ de vision. 

![Lesson4 Chapter2 Step4im](images/Lesson4_chapter2_step4im.PNG)

L’objectif des étapes suivantes consiste à activer la saisie et l’interaction avec nos objets 3D et à appliquer des paramètres de manipulation différents.

5. Sélectionnez l’objet fromage, puis cliquez sur Ajouter un composant dans le panneau Inspecteur. 

6. Recherchez dans la zone de recherche pour obtenir une interaction proche de l’interaction, puis sélectionnez le script. Ce composant permet aux utilisateurs d’accéder aux objets et de les saisir avec des mains suivies. Les objets peuvent également être manipulés à partir d’une distance, sauf si la case à cocher autoriser la manipulation FAR est décochée par un cercle vert dans l’image ci-dessous.

![Lesson4 Chapter2 Step6im](images/Lesson4_Chapter2_step6im.PNG)

7. Ajoutez une approche d’interaction proche à l’objet octa, à l’objet platoniques, à la terre, au module lunaire et à la tasse de café en répétant les étapes 5 et 6 sur ces objets.

8. Supprimez la possibilité de manipulation de loin sur l’objet Octa. Pour ce faire, sélectionnez le octa dans la hiérarchie, puis décochez la case autoriser la manipulation Far (marquée d’un cercle vert). Ceci fait que les utilisateurs peuvent interagir directement avec l’objet Octa seulement en utilisant les mains suivies.

>Remarque : Pour la documentation complète du composant Gestionnaire de manipulation et de ses paramètres associés, reportez-vous à la [Documentation du MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html).

9. Assurez-vous que le composant pouvant être obtenu à l’approche d’interaction a été ajouté au noyau de la terre, au module lunaire et à la tasse café (Voir l’étape 7).

10. Pour le module lunaire, modifiez les paramètres du gestionnaire de manipulation afin qu’il pivote autour du centre de l’objet pour l’interaction proche et éloignée, comme illustré dans l’image ci-dessous.

![Lesson4 Chapter2 Step10im](images/Lesson4_chapter2_step10im.PNG)

11 : Pour le noyau de la terre, remplacez le comportement de la version par rien. Cela permet de faire en sorte qu’une fois que le noyau de la terre est sorti de l’utilisateur, il ne continue pas à bouger. 

![Lesson4 Chapter2 Step11im](images/Lesson4_Chapter2_step11im.PNG)

> Remarque : Ce paramètre est utile pour des scénarios comme la création d’une balle que vous pouvez lancer. Le fait de maintenir la vélocité et la vélocité angulaire le rend de manière à ce qu’une fois la balle relâché, elle continue à évoluer à la vitesse à laquelle elle a été libérée, de la même manière qu’une balle physique se comporterait.

### <a name="adding-bounding-boxes"></a>Ajout de cadres englobants
Les cadres englobants rendent plus facile et plus intuitive la manipulation des objets avec une seule main pour la manipulation directe (interaction de près) et pour la manipulation basée sur un rayon (interaction de loin). Les zones englobantes fournissent des poignées qui peuvent être saisies pour mettre à l’échelle et faire pivoter des objets le long d’un axe spécifique.
>Remarque : Avant de pouvoir ajouter un cadre englobant à un objet, vous devez d’abord avoir un conflit sur l’objet (par exemple, un conflit de boîte), comme nous l’avons fait précédemment dans cette leçon. Vous pouvez ajouter des collisionneurs en sélectionnant l’objet puis, dans le panneau de l’inspecteur de l’objet, en sélectionnant Add Component>Box Collider (Ajouter un composant>Cadre de collisionneur).
>

1. Ajoutez un conflit Box à l’objet de base terrestre s’il n’en existe pas déjà un. La boîte de conflit et le programme d’installation ne sont pas requis si vous utilisez le Prefab fourni dans le dossier composants de base du module pour les instructions fournies. Dans le cas du noyau de la terre, nous avons ajouté le «conflit de Box» à l’objet, node_id30, situé sous le noyau de la terre, comme indiqué dans l’image ci-dessous. Sélectionnez node_id30 dans l’onglet inspecteur de l’objet, cliquez sur Ajouter un composant, puis recherchez Box collision. 

![Lesson4 Chapter3 Step1im](images/Lesson4_Chapter3_step1im.PNG)

![Lesson4 Chapter3 Step2im](images/Lesson4_chapter3_step2im.PNG)

> Remarque : Assurez-vous de dimensionner le conflit de cases pour qu’il ne soit pas trop grand ou trop petit. Il doit avoir à peu près la même taille que l’objet qu’il entoure (dans cet exemple, le noyau terrestre). Ajustez le conflit de zone si nécessaire en sélectionnant l’option modifier le conflit dans la zone conflit. Vous pouvez modifier les valeurs x, y et z ou faire glisser les gestionnaires de cadre englobant dans la fenêtre de la scène de l’éditeur. 

![Lesson4 Chapter3 Noteim](images/Lesson4_Chapter3_noteim.PNG)

2. Ajoutez un cadre englobant à l’objet node_id30 du cœur de la terre. Pour ce faire, sélectionnez l’objet node_id30 dans 3DObjectCollection. Dans l’onglet inspecteur, cliquez sur Ajouter un composant, puis recherchez cadre englobant. Vérifiez que le cadre englobant, le cadre de collisionneur et les scripts de manipulation (gestionnaire de manipulation, interaction de près avec préhension) sont tous sur le même objet de jeu.

3.  Dans la section comportement de la zone englobante, sélectionnez Activer au démarrage dans la liste déroulante activation. Pour passer en revue les détails supplémentaires concernant les différentes options d’activation et les autres options du cadre englobant, consultez la [documentation du cadre englobant du MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html>)

   

   *Dans les étapes suivantes, nous modifierons également la façon dont le cadre englobant se présente en ajustant le matériau par défaut, le matériau lorsqu’il est retiré, ainsi que la visualisation des poignées d’angle et de côté. Le MRTK contient plusieurs options permettant de personnaliser le cadre englobant.*

4. Dans le panneau projet, recherchez BoundingBox et vous verrez une liste de documents dénotés par une sphère bleue dans les résultats de la recherche, comme indiqué dans l’image ci-dessous. 

5. Faites glisser le matériau BoundingBox dans l’emplacement de la boîte sur le composant de cadre englobant. Saisissez également le matériau boundingboxgrabbed et placez-le dans l’emplacement de matériau retiré de la boîte sur le composant de cadre englobant.

6. Faites glisser le Prefab MRTK_BoundingBox_ScaleWidget dans l’emplacement de la poignée d’échelle Prefab sur le composant de cadre englobant. 

7. Faites glisser le Prefab MRTK_BoundingBox_RotateWidget dans l’emplacement de la poignée de rotation sur le composant de zone de liaison.

![Lesson4 Chapter3 Step4 7Im](images/Lesson4_chapter3_step4-7im.PNG)

8. Vérifiez que le cadre englobant cible le bon objet. Dans le composant de cadre englobant, il y a l’objet cible et les scripts de substitution. Veillez à faire glisser l’objet entouré par le cadre englobant à ces deux emplacements. Dans cet exemple, faites glisser l’objet node_id30 sur ces deux emplacements comme indiqué dans l’image ci-dessous.

> Lorsque vous démarrez ou lisez l’application, votre objet est entouré d’un cadre bleu. Vous pouvez faire glisser les coins de cet encadrement pour redimensionner l’objet. Si vous souhaitez que les poignées de mise à l’échelle et les poignées de rotation soient plus larges et plus visibles, il est recommandé d’utiliser les paramètres du cadre englobant par défaut (en évitant les étapes 4 à 7). 

![Lesson4 Chapter3 Step8im](images/Lesson4_Chapter3_step8im.PNG)

9. Pour revenir à la visualisation du cadre englobant par défaut, dans le panneau Inspecteur de l’objet de la zone englobante, sélectionnez la poignée de rotation Prefab et appuyez sur la touche Suppr. Vous verrez une visualisation de cadre englobant similaire à l’image ci-dessous. Remarque : Les visualisations des cadres englobants apparaissent seulement en mode lecture.

![Lesson4 Chapter3 Step9im](images/Lesson4_chapter3_step9im.PNG)

### <a name="adding-touch-effects"></a>Ajout d’effets tactiles
Dans cet exemple, nous allons émettre un son quand vous touchez un objet avec votre main.

1. Ajoutez un composant Source audio à votre objet de jeu. Sélectionnez l’objet octa dans votre hiérarchie de scènes. Dans le volet de l’inspecteur, cliquez sur le bouton Ajouter un composant, recherchez et sélectionnez source audio. Nous allons utiliser cette source audio pour produire un effet sonore dans une étape ultérieure. 

>Remarque : Assurez-vous que l’objet octa a une zone de conflit sur celui-ci.

2. Ajoutez le composant touchable near interaction. Cliquez sur le bouton Ajouter un composant dans le panneau inspecteur et recherchez near interaction touchable. Sélectionnez-le pour ajouter le composant. 

>Remarque : Auparavant, nous avons ajouté une approche de capture d’interaction proche. La différence entre ce touchable et l’approche near-interaction est que l’interaction pouvant être extraite est destinée à un objet à saisir et auquel interagir. Le composant touchable est destiné à l’objet à toucher. Les deux composants peuvent être utilisés ensemble pour une combinaison d’interactions.

![Lesson4 Chapter4 Step1 2Im](images/Lesson4_chapter4_step1-2im.PNG)

3. Ajoutez dans le script tactile d’interaction manuelle. Notez que ce script est inclus dans la scène Unity que vous avez importée dans le cadre de cette démonstration et qu’il n’est pas inclus dans le MRTK d’origine. Comme l’étape précédente, cliquez sur Ajouter un composant et recherchez interaction tactile pour l’ajouter.

>Notez que vous avez trois options avec le script: 

>   - À la saisie tactile: Se déclenche lorsque vous touchez et relâchez l’objet
>   - At Touch Started: Se déclenche lorsque l’objet est touché
>   - À la saisie tactile mise à jour: Déclenche périodiquement lorsque votre main touche l’objet

>   Pour cet exemple, nous allons utiliser le paramètre at Touch Started.

4. Cliquez sur le bouton + de l’option on Touch Started comme indiqué dans l’image ci-dessous. Faites glisser l’objet octa dans le champ vide. 

5. Dans la liste déroulante qui indique aucune fonction (au-dessus du rectangle vert dans l’image ci-dessous), sélectionnez AudioSource-> PlayOneShot. Nous allons ajouter un clip audio à ce champ en utilisant les concepts ci-dessous :

   - Le MRTK fournit-il une petite liste de clips audio. N’hésitez pas à explorer ces éléments dans le panneau de votre projet. Vous les trouverez dans le dossier MixedRealityToolkit. SDK, puis dans le dossier ressources standard. Vous verrez un dossier audio dans lequel se trouvent tous les clips audio.
   - Pour cet exemple, nous allons utiliser le clip audio MRTK_Gem. 
   - Pour ajouter un clip audio, faites simplement glisser le clip souhaité à partir du panneau du projet dans AudioSource.PlayOneShot (marqué par le rectangle vert dans l’exemple ci-dessus) dans le panneau de l’inspecteur.

   Désormais, lorsque l’utilisateur atteint et touche l’objet octa, la piste audio MRTK_Gem est lue. Le script tactile d’interaction manuelle ajuste également la couleur de l’objet lorsqu’il est touché. 

![Lesson4 Chapter4 Step3 5 Noteim](images/Lesson4_chapter4_step3-5-noteim.PNG)

## <a name="congratulations"></a>Félicitations 
Dans ce didacticiel, vous avez appris à organiser des objets 3D dans une collection de grilles et à manipuler des objets 3D (mise à l’échelle, rotation et déplacement) à l’aide de l’interaction proche (saisie directe des mains) et de l’interaction lointaine (à l’aide de rayons ou rayons de main). Vous avez également appris à placer des zones englobantes autour des objets 3D et appris à utiliser et à personnaliser les gizmos dans les zones englobantes. Enfin, vous avez découvert comment déclencher des événements quand l’utilisateur touche un objet.

[Leçon suivante : 6. Exploration des options d’entrée avancées](mrlearning-base-ch5.md)

