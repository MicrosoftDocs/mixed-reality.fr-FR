---
title: Didacticiels de mise en route-5. Interaction avec les objets 3D
description: ''
author: jessemcculloch
ms.author: jemccull
ms.date: 05/02/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: fe068d0cfcea369f10e6fa636eb73fecb3002fa7
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334383"
---
# <a name="5-interacting-with-3d-objects"></a>5. interaction avec les objets 3D

Dans ce didacticiel, vous allez découvrir le contenu 3D de base et l’expérience utilisateur, par exemple :

* Organisation d’objets 3D dans le cadre d’une collection
* Zones englobantes pour la manipulation de base
* Interaction proche et éloignée
* Mouvements tactiles et de manipulation avec suivi de la main

## <a name="objectives"></a>Objectifs

* Découvrez comment organiser le contenu 3D avec la collection d’objets Grid de MRTK
* Implémenter des cadres englobants
* Configurer des objets 3D pour la manipulation de base--déplacer, faire pivoter et mettre à l’échelle
* Explorer l’interaction de près et de loin
* En savoir plus sur les gestes supplémentaires de suivi de la main, tels que la manipulation et la saisie tactile

## <a name="organizing-3d-objects-in-a-collection"></a>Organisation des objets 3D dans une collection

1. Cliquez avec le bouton droit sur votre hiérarchie et sélectionnez Créer vide pour créer un objet de jeu vide, renommez-le 3DObjectCollection et assurez-vous qu’il est positionné sur x = 0, y = 0 et z = 0.

    ![mrlearning-base-CH4-1-Step1. png](images/mrlearning-base-ch4-1-step1.png)

2. Téléchargez le package Unity [Unity. HoloLens2. gettingstarted. tutoriels. Asset. 2.1.0.0](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.1.0.0/Unity.HoloLens2.GettingStarted.Tutorials.Asset.2.1.0.0.unitypackage) et importez-le à l’aide des mêmes instructions pour importer des packages personnalisés décrits dans [Lesson1](mrlearning-base-ch1.md). Ce package comprend des modèles 3D et d’autres ressources utiles utilisées dans ce didacticiel.

3. Dans le panneau projet, accédez à ressources > BaseModuleAssets > module base Prefabs et recherchez « incomplet », nous allons utiliser une partie de ces Prefabs.

    ![mrlearning-base-CH4-1-step3. png](images/mrlearning-base-ch4-1-step3.png)

4. Faites glisser le tasse café dans l’objet de jeu 3DObjectCollection de l’étape 1. La tasse de café est maintenant un enfant de la collection.

    ![mrlearning-base-CH4-1-step4. png](images/mrlearning-base-ch4-1-step4.png)

5. Ensuite, vous allez ajouter des objets 3D à notre scène en suivant le même processus que dans l’étape précédente. Vous trouverez ci-dessous une liste d’objets à ajouter dans cet exemple. À mesure que vous ajoutez les objets, vous pouvez les voir apparaître dans votre scène dans différentes tailles. Ajustez l’échelle de chaque modèle 3D sous paramètres de transformation dans le panneau Inspecteur. Les ajustements recommandés pour cet exemple sont listés avec les objets ci-dessous.

    * Cheese_BaseModuleIncomplete. Échelle : x = 0,05, y = 0,05, z = 0,05.
    * CoffeeCup_BaseModuleIncomplete. Échelle : x = 0,1, y = 0,1, z = 0,1.
    * EarthCore_BaseModuleIncomplete. Échelle : x = 50,0 y = 50,0, z = 50,0.
    * Model_Platonic_BaseModuleIncomplete. Échelle : x = 0,13, y = 0,13, z = 0,13.
    * Octa_BaseModuleIncomplete. Échelle : x = 0,13. y = 0,13, z =0,13.
    * TheModule_BaseModuleIncomplete. Échelle : x = 0,03, y = 0,03, z = 0,03.

    ![mrlearning-base-CH4-1-step5. png](images/mrlearning-base-ch4-1-step5.png)

6. Ajoutez trois cubes à votre scène. Cliquez avec le bouton droit sur l’objet 3DObjectCollection, sélectionnez objet 3D, puis sélectionnez cube. Définissez l’échelle sur x = 0,14, y = 0,14 et z = 0,14. Répétez cette étape deux fois supplémentaires pour créer un total de trois cubes. Vous pouvez également dupliquer le cube deux fois pour un total de trois cubes. Vous pouvez également choisir d’utiliser les trois cubes préfabriqués préparés à partir Assets>BaseModuleAssets>Base Module Prefab (Ressources>Ressources du module de base>Préfabriqué du module de base) et sélectionner GreenCube_BaseModuleIncomplete, BlueCube_BaseModuleIncomplete et OrangeCube_BaseModuleIncomplete.

    ![mrlearning-base-CH4-1-step6. png](images/mrlearning-base-ch4-1-step6.png)

7. Organisez votre collection d’objets pour former une grille, via la procédure décrite dans la [leçon 2](mrlearning-base-ch2.md), à l’aide de la collection d’objets Grid de MRTK. Reportez-vous à l’image ci-dessous pour obtenir un exemple de configuration des objets dans une grille 3x3.

    ![mrlearning-base-CH4-1-step7. png](images/mrlearning-base-ch4-1-step7.png)

    >[!NOTE]
    >Vous remarquerez peut-être que certains objets sont décentrés, tels que les objets de l’image ci-dessus. La raison en est que des préfabriqués ou des objets peuvent avoir des objets enfants qui ne sont pas alignés. N’hésitez pas à effectuer les ajustements nécessaires des positions des objets ou des objets enfants pour obtenir une grille bien alignée.

## <a name="manipulating-3d-objects"></a>Manipulation d’objets 3D

1. Ajoutez la possibilité de manipuler un cube. Pour ajouter la possibilité de manipuler des objets 3D, procédez comme suit :
    * Sélectionnez l’objet 3D que vous souhaitez manipuler dans votre hiérarchie (c’est-à-dire l’un de vos cubes).
    * Cliquez sur Ajouter un composant.
    * Rechercher « manipulation »
    * Sélectionner le gestionnaire de manipulation
    * Répétez cette opération pour tous les objets 3D sous l’objet 3DObjectCollection, mais pas le 3DObjectCollection lui-même.
    * Assurez-vous que tous les objets 3D disposent d’un conflit de collision ou de boîte (ajouter un composant > un conflit de boîte).

    ![Lesson4 Chapter2 Step1im](images/Lesson4_chapter2_step1im.PNG)

    >[!NOTE]
    >Le gestionnaire de manipulation est un composant qui vous permet d’ajuster les paramètres de comportement des objets lorsqu’ils sont manipulés. Cela comprend la rotation, la mise à l’échelle, le déplacement et la limitation du mouvement sur un axe spécifique.

2. Limitez les possibilités sur un cube à la seule mise à l’échelle. Sélectionnez un cube dans l’objet 3DObjectCollection. Dans le volet de l’inspecteur, en regard de deux types de manipulations de la main, cliquez sur le menu déroulant et sélectionnez mettre à l’échelle. Ceci fait que l’utilisateur peut seulement changer la taille du cube.

    ![Lesson4 Chapter2 Step2im](images/Lesson4_Chapter2_step2im.PNG)

3. Changez la couleur de chaque cube de façon à pouvoir les différencier.
    * Accédez au panneau projet et faites défiler jusqu’à ce que vous voyez MixedRealityToolkit. SDK, puis sélectionnez-le.
    * Sélectionnez le dossier ressources standard.
    * Cliquez sur le dossier matériaux.
    * Faites glisser un matériau différent sur chacun de vos cubes.

    >[!NOTE]
    >Vous pouvez choisir n’importe quelle couleur pour vos cubes. Pour cet exemple, glowingcyan, glowingorange et Green sont utilisés. N’hésitez pas à faire des essais avec différentes couleurs. Pour ajouter la couleur au cube, cliquez sur le cube que vous souhaitez modifier, puis faites glisser le matériau vers le champ Material du convertisseur de maillage dans le panneau inspecteur du cube.

    ![Lesson4 Chapter2 Step3im](images/Lesson4_Chapter2_step3im.PNG)

4. Sélectionnez un autre cube dans l’objet 3DObjectCollection et faites-le pour que son mouvement soit restreint à une distance fixe à partir de l’en-tête. Pour ce faire, à droite de l’étiquette de contrainte sur le mouvement, cliquez sur le menu déroulant et sélectionnez corriger la distance à partir de la tête. Cela ajuste le cube pour qu’il se trouve dans son champ de vision.

    ![Lesson4 Chapter2 Step4im](images/Lesson4_chapter2_step4im.PNG)

    L’objectif des quelques étapes suivantes est d’activer la saisie et l’interaction avec nos objets 3D et d’appliquer différents paramètres de manipulation.

5. Sélectionnez l’objet fromage, puis cliquez sur Ajouter un composant dans le panneau Inspecteur.

6. Recherchez dans la zone de recherche pour rechercher des interactions proches et sélectionnez le script. Ce composant permet aux utilisateurs d’accéder aux objets et de les saisir avec des mains suivies. Les objets peuvent également être manipulés à partir d’une distance, sauf si la case à cocher autoriser la manipulation FAR est décochée par un cercle vert dans l’image ci-dessous.

    ![Lesson4 Chapter2 Step6im](images/Lesson4_Chapter2_step6im.PNG)

7. Ajoutez une approche d’interaction proche à l’objet octa, à l’objet platoniques, à la terre, au module lunaire et à la tasse de café en répétant les étapes 5 et 6 sur ces objets.

8. Supprimez la possibilité de manipulation de loin sur l’objet Octa. Pour ce faire, sélectionnez le octa dans la hiérarchie et décochez la case autoriser la manipulation Far (marquée d’un cercle vert). Cela permet aux utilisateurs d’interagir uniquement avec le octa à l’aide des mains suivies.

    >[!NOTE]
    >Pour obtenir la documentation complète du composant Gestionnaire de manipulation et des paramètres associés, reportez-vous à la [documentation MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html).

9. Assurez-vous que le composant pouvant être obtenu à l’approche d’interaction a été ajouté au noyau de la terre, au module lunaire et à la tasse café (Voir l’étape 7).

10. Pour le module lunaire, modifiez les paramètres du gestionnaire de manipulation afin qu’il pivote autour du centre de l’objet pour les interactions près et éloignées, comme le montre l’image ci-dessous.

    ![Lesson4 Chapter2 Step10im](images/Lesson4_chapter2_step10im.PNG)

11. Pour le noyau de la terre, remplacez le comportement de la version par rien. Cela permet de faire en sorte qu’une fois que le noyau de la terre est sorti de l’utilisateur, il ne continue pas à bouger.

    ![Lesson4 Chapter2 Step11im](images/Lesson4_Chapter2_step11im.PNG)

    >[!NOTE]
    >Ce paramètre est utile pour les scénarios, tels que la création d’une balle que vous pouvez lever. En conservant la vélocité appropriée et la vélocité angulaire pour garantir qu’une fois la balle relâché, elle continuera à évoluer à la vitesse à laquelle elle a été libérée. semblable à la façon dont une balle physique se comporterait.

## <a name="adding-bounding-boxes"></a>Ajout de cadres englobants

Les zones englobantes facilitent et rendent plus intuitive la manipulation d’objets avec une main pour la manipulation directe (Near interaction) et la manipulation basée sur les rayons (interaction lointaine). Les zones englobantes fournissent des poignées qui peuvent être saisies pour mettre à l’échelle et faire pivoter des objets le long d’un axe spécifique.

>[!NOTE]
>Avant de pouvoir ajouter un cadre englobant à un objet, vous devez d’abord avoir un conflit sur l’objet (par exemple, un conflit de boîte), comme nous l’avons vu précédemment dans cette leçon. Les conflits peuvent être ajoutés en sélectionnant l’objet et dans le panneau de l’inspecteur de l’objet, en sélectionnant Ajouter un composant > conflit de boîte.

1. Ajoutez un conflit Box à l’objet de base terrestre s’il n’en existe pas déjà un. La boîte de conflit et le programme d’installation ne sont pas requis si vous utilisez le Prefab fourni dans le dossier composants de base du module pour les instructions fournies. Dans le cas du noyau de la terre, nous avons ajouté la boîte de conflit à l’objet, node_id30, sous le noyau de la terre, comme illustré dans l’image ci-dessous. Sélectionnez node_id30 dans l’onglet inspecteur de l’objet, cliquez sur Ajouter un composant, puis recherchez Box collision.

    ![Lesson4 Chapter3 Step1im](images/Lesson4_Chapter3_step1im.PNG)

    ![Lesson4 Chapter3 Step2im](images/Lesson4_chapter3_step2im.PNG)

    >[!NOTE]
    >Assurez-vous de dimensionner le conflit de cases pour qu’il ne soit pas trop grand ou trop petit. Il doit avoir à peu près la même taille que l’objet qu’il entoure (dans cet exemple, le noyau terrestre). Ajustez le conflit de zone si nécessaire en sélectionnant l’option modifier le conflit dans la zone conflit. Vous pouvez modifier les valeurs x, y et z ou faire glisser les gestionnaires de cadre englobant dans la fenêtre de la scène de l’éditeur.

    ![Lesson4 Chapter3 Noteim](images/Lesson4_Chapter3_noteim.PNG)

2. Ajoutez un cadre englobant à l’objet node_id30 du cœur de la terre. Pour ce faire, sélectionnez l’objet node_id30 dans 3DObjectCollection. Dans l’onglet inspecteur, cliquez sur Ajouter un composant, puis recherchez cadre englobant. Vérifiez que le cadre englobant, le cadre de collisionneur et les scripts de manipulation (gestionnaire de manipulation, interaction de près avec préhension) sont tous sur le même objet de jeu.

3. Dans la section comportement de la zone englobante, sélectionnez Activer au démarrage dans la liste déroulante activation. Pour consulter des informations supplémentaires sur les différentes options d’activation et les autres options de cadre englobant, consultez la [documentation relative au cadre englobant de MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html>) .

    *Dans les étapes suivantes, nous modifierons également la façon dont le cadre englobant se présente en ajustant le matériau par défaut, le matériau lorsqu’il est retiré, ainsi que la visualisation des poignées d’angle et de côté. Le MRTK contient plusieurs options pour personnaliser le cadre englobant.*

4. Dans le panneau projet, recherchez « BoundingBox ». vous verrez une liste de documents dénotés par une sphère bleue dans les résultats de la recherche, comme indiqué dans l’image ci-dessous.

5. Faites glisser le matériau BoundingBox dans l’emplacement de la boîte sur le composant de cadre englobant. Saisissez également le matériau boundingboxgrabbed et placez-le dans l’emplacement de matériau retiré de la boîte sur le composant de cadre englobant.

    ![mrlearning-base-CH4-3-step5. png](images/mrlearning-base-ch4-3-step5.png)

6. Faites glisser le Prefab MRTK_BoundingBox_ScaleHandle dans l’emplacement de la poignée d’échelle Prefab et le MRTK_BoundingBox_RotateHandle Prefab dans l’emplacement de la poignée de rotation du composant de zone de liaison.

    ![mrlearning-base-CH4-3-step6. png](images/mrlearning-base-ch4-3-step6.png)

7. Vérifiez que le cadre englobant cible le bon objet. Dans le composant de cadre englobant, il y a l’objet cible et les scripts de substitution. Faites glisser l’objet qui contient le cadre englobant sur ces deux emplacements. Dans cet exemple, faites glisser l’objet node_id30 vers ces deux emplacements, comme indiqué dans l’image ci-dessous.

    ![mrlearning-base-CH4-3-step7. png](images/mrlearning-base-ch4-3-step7.png)

    >[!NOTE]
    >Lorsque vous démarrez ou lisez l’application, votre objet est entouré d’un cadre bleu. Vous pouvez faire glisser les coins de cet encadrement pour redimensionner l’objet. Si vous souhaitez que les poignées de mise à l’échelle et les poignées de rotation soient plus larges et plus visibles, il est recommandé d’utiliser les paramètres du cadre englobant par défaut (en évitant les étapes 4-à 6).

8. Pour revenir à la visualisation du cadre englobant par défaut, dans le panneau Inspecteur de l’objet de la zone englobante, sélectionnez la poignée de rotation Prefab et appuyez sur la touche Suppr pour la supprimer. Lorsque vous entrez en mode lecture, Wou affiche une visualisation de cadre englobant similaire à l’image ci-dessous.

    ![mrlearning-base-CH4-3-step8. png](images/mrlearning-base-ch4-3-step8.png)

    >[!NOTE]
    >Les visualisations de cadre englobant s’affichent uniquement en mode lecture.

## <a name="adding-touch-effects"></a>Ajout d’effets tactiles

Dans cet exemple, nous allons émettre un son quand vous touchez un objet avec votre main.

1. Ajoutez un composant Source audio à votre objet de jeu. Sélectionnez l’objet octa dans votre hiérarchie de scènes. Dans le volet de l’inspecteur, cliquez sur le bouton Ajouter un composant, recherchez et sélectionnez source audio. Nous allons utiliser cette source audio pour produire un effet sonore dans une étape ultérieure.

    >[!NOTE]
    >Assurez-vous que l’objet octa a une zone de conflit sur celui-ci.

2. Ajoutez le composant touchable near interaction. Cliquez sur le bouton Ajouter un composant dans le panneau inspecteur et recherchez near interaction touchable. Sélectionnez-le pour ajouter le composant.

    >[!NOTE]
    >Auparavant, nous avons ajouté une approche de capture d’interaction proche. La différence entre ce touchable et l’approche near-interaction est que l’interaction pouvant être extraite est destinée à un objet à saisir et auquel interagir. Le composant touchable est destiné à l’objet à toucher. Les deux composants peuvent être utilisés ensemble pour une combinaison d’interactions.

    ![Lesson4 Chapter4 Step1 2Im](images/Lesson4_chapter4_step1-2im.PNG)

3. Ajoutez dans le script tactile d’interaction manuelle. Comme l’étape précédente, cliquez sur Ajouter un composant et recherchez interaction tactile pour l’ajouter.

    Notez que vous avez trois options avec le script :
    * Sur Touch terminé : déclencheurs quand vous touchez et relâchez l’objet
    * At Touch Started : déclencheurs quand l’objet est touché
    * À la saisie tactile mise à jour : déclenche périodiquement pendant que votre main touche l’objet

    Pour cet exemple, nous allons utiliser le paramètre at Touch Started.

    >[!NOTE]
    >Ce script est inclus dans le package BaseModuleAssets Unity que vous avez importé comme au début de ce didacticiel et il n’est pas inclus dans le MRTK d’origine.

4. Cliquez sur le bouton + de l’option on Touch Started, puis faites glisser l’objet octa dans le champ Empty.

    ![mrlearning-base-CH4-4-step4. png](images/mrlearning-base-ch4-4-step4.png)

5. Dans la liste déroulante qui indique aucune fonction, sélectionnez AudioSource > PlayOneShot. Nous allons ajouter un clip audio à ce champ en utilisant les concepts ci-dessous :

    * Le MRTK fournit-il une petite liste de clips audio. N’hésitez pas à les explorer dans le panneau de votre projet. Vous les trouverez sous les ressources > MixedRealityToolkit. SDK > les ressources standard > dossier audio.
    * Pour cet exemple, nous allons utiliser le clip audio MRTK_Gem.
    * Pour ajouter un clip audio, il vous suffit de faire glisser le clip souhaité du panneau projet vers le champ AudioSource. PlayOneShot.

    ![mrlearning-base-CH4-4-step5. png](images/mrlearning-base-ch4-4-step5.png)

   Désormais, lorsque l’utilisateur atteint et touche l’objet octa, la piste audio MRTK_Gem est lue. Le script tactile d’interaction manuelle ajuste également la couleur de l’objet lorsqu’il est touché.

## <a name="congratulations"></a>Félicitations !

Dans ce didacticiel, vous avez appris à organiser les objets 3D dans une collection de grilles et à manipuler ces objets (mise à l’échelle, rotation et déplacement) à l’aide de Near interaction (saisie directe des mains) et de l’interaction lointaine (à l’aide de rayons ou de rayons main). Vous avez également appris à placer des zones englobantes autour des objets 3D et appris à utiliser et à personnaliser les gizmos dans les zones englobantes. Enfin, vous avez découvert comment déclencher des événements quand l’utilisateur touche un objet.

[Leçon suivante : 6. exploration des options d’entrée avancées](mrlearning-base-ch5.md)
