---
title: Module MR Learning Base - Interaction des objets 3D
description: Terminer ce cours pour apprendre à implémenter la reconnaissance faciale de Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, hololens (didacticiel), unity,
ms.openlocfilehash: 344b3bc892839bc22445e10af644771bc7008ac3
ms.sourcegitcommit: a32f673814a6cd6ff00f936f448885788b3b882c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2019
ms.locfileid: "64929584"
---
# <a name="mr-learning-base-module---3d-object-interaction"></a>Module MR Learning Base - Interaction des objets 3D

Dans cette leçon, nous allons via le contenu 3D de base et l’expérience utilisateur. Nous allez apprendre comment organiser les objets 3D dans le cadre d’une collection, en savoir plus sur le cadre de sélection pour la manipulation de base, en savoir plus sur l’interaction proches et en savoir plus sur les fonctions tactiles et saisir les mouvements de main de suivi. 

## <a name="objectives"></a>Objectifs

* Découvrez comment organiser le contenu 3D à l’aide de la Collection d’objets de MRTK grille
* Implémenter des zones englobantes
* Configurer des objets 3D pour la manipulation de base (déplacement, rotation et mise à l’échelle)
* Explorez l’interaction proches
* En savoir plus sur supplémentaire manuellement le suivi des mouvements tels que la manipulation et l’interaction tactile

## <a name="instructions"></a>Instructions

### <a name="organizing-3d-objects-in-a-collection"></a>Organisation des objets 3D dans une Collection

1. Cliquez avec le bouton droit sur votre hiérarchie et sélectionnez, « créer vide ». Cette opération crée un objet de jeu vide. Renommer en « 3DObjectCollection ». Il s’agit où placer tous nos objets 3D. Assurez-vous que le positionnement de la collection est définie sur x = 0, y = 0 et z = 0.

![Lesson4 Chapter1 Step1im](images/Lesson4_Chapter1_step1im.PNG)

2. Importer à l’aide de ressources de module les mêmes instructions pour importer des packages personnalisés décrites dans [Lesson1](mrlearning-base-ch1.md). Les ressources de module incluent des modules 3D et autres scripts utiles qui seront utilisés tout au long de ce didacticiel. Vous trouverez ici le package unity de module : <https://github.com/Microsoft/MixedRealityLearning/releases/tag/V1.1>

3. La tasse de café prefab peut être identifiée par un cube bleu en regard de celle-ci. Ne sélectionnez pas la tasse de café avec le cube bleu et un petit livre blanc (qui indique le modèle d’origine de 3D et pas le préfabriqué.) 

![Lesson4 Chapter1 Noteaim](images/Lesson4_chapter1_noteaim.PNG)

4. Faites glisser le préfabriqué tasse de café de votre choix dans l’objet de jeu de « 3DObjectCollection » à l’étape 1. La tasse de café est maintenant un enfant de la collection.

![Lesson4 Chapter1 Step4ima](images/Lesson4_chapter1_step4ima.PNG)

5. Ensuite, nous allons ajouter davantage d’objets 3D dans notre scène. Voici une liste d’objets, que nous allons ajouter dans cet exemple. Lorsque vous ajoutez les objets, vous constaterez qu’elles apparaissent dans votre scène dans différentes tailles. Ajuster l’échelle de chaque modèle 3D sous le paramètre de transformation dans le panneau de l’inspecteur. Réglages recommandés pour cet exemple sont répertoriées avec les objets ci-dessous. Rechercher les mots suivants dans la zone de recherche dans votre Panneau de configuration de projet et faites glisser l’objet 3D préfabriqué dans l’objet « 3DObjectCollection » semblable à l’étape précédente. Vous trouverez ces collection de prefabs actifs > BaseModuleAssets > Prefabs de Module de Base
- Recherchez « TheModule_BaseModuleIncomplete ». Faites glisser dans la scène. La valeur de l’échelle x = 0,03, y = 0,03, z = 0,03. 
- Recherchez « Octa_BaseModuleIncomplete ». Faites glisser dans la scène. La valeur de l’échelle x = 0,13. y = 0.13, z =0.13.
- Recherchez « EarthCore_BaseModuleIncomplete ». Faites glisser dans la scène. La valeur de l’échelle x = 50,0 y = 50,0, z = 50,0.
- Recherchez « Cheese_BaseModuleIncomplete ». Faites glisser dans la scène. La valeur de l’échelle x = 0,05, y = 0,05, z = 0,05.
- Recherchez « Model_Platonic_BaseModuleIncomplete ». Faites glisser dans la scène. La valeur de l’échelle x = 0,13, y = 0,13, z = 0,13.
- Recherchez « CoffeeCup_BaseModuleIncomplete ». Faites glisser dans la scène.

![Lesson4 Chapter1 Step5im](images/Lesson4_Chapter1_step5im.PNG)

6. Ajoutez des 3 cubes dans votre scène. Cliquez avec le bouton droit sur l’objet « 3DObjectCollection », sélectionnez « objet 3D », puis sélectionnez « Cube ». La valeur de l’échelle x = 0.14, y = 0.14 et z = 0.14. Répétez cette étape 2 fois supplémentaires pour créer un total de 3 cubes. Vous pouvez également dupliquer le cube à deux reprises pour un total de 3 cubes. Vous pouvez également choisir d’utiliser les trois prefabs cube préparée à partir de ressources > BaseModuleAssets > Prefabs de Module de Base et sélectionnez GreenCube_BaseModuleIncomplete, BlueCube_BaseModuleIncomplete et OrangeCube_BaseModuleIncomplete.

![Lesson4 Chapter1 Step6im](images/Lesson4_Chapter1_step6im.PNG)

7. Organisez votre collection d’objets pour former une grille à l’aide de la procédure décrite dans [leçon 2](mrlearning-base-ch2.md) à l’aide de la Collection d’objets de la MRTK grille. Reportez-vous à l’image ci-dessous pour voir un exemple de configuration des objets dans une grille de 3 x 3.

![Lesson4 Chapter1 Notebim](images/Lesson4_chapter1_notebim.PNG)

>Remarque: Vous pouvez remarquer que certains objets sont hors tension-centre, tels que les objets dans l’image ci-dessus. Il s’agit, car prefabs ou les objets peuvent avoir des objets enfants qui ne sont pas alignées. N’hésitez pas à effectuer les ajustements nécessaires à l’objet ou d’emplacements d’objet enfant pour obtenir une grille bien alignée.


### <a name="manipulating-3d-objects"></a>Manipulation d’objets 3D
1. Ajouter la possibilité de manipuler un cube. Pour ajouter la possibilité de manipuler des objets 3D, vous devez procédez comme suit :
-   Sélectionnez l’objet 3D que vous voulez manipuler dans votre hiérarchie (dans cet exemple, un de vos cubes).
-   Cliquez sur « Ajouter un composant ». 
-   Recherchez « manipulation ».
-   Sélectionnez « Gestionnaire de manipulation. »
-   Répétez ces étapes pour tous les objets 3D sous l’objet « 3DObjectCollection » mais pas le « 3DObjectCollection » lui-même.
-   Vérifiez tous les objets 3D ont un collider ou le collider de zone (ajouter un composant > zone collider).

![Lesson4 Chapter2 Step1im](images/Lesson4_chapter2_step1im.PNG)

>Le Gestionnaire de manipulation est un composant qui vous permet d’ajuster les paramètres de la façon dont les objets se comportent lorsque manipulé. Cela inclut la rotation, mise à l’échelle, le déplacement et un mouvement de contrainte sur certains axes. 

2. Restreindre un cube afin qu’il peut uniquement être mis à l’échelle. Sélectionnez un cube dans l’objet « 3DObjectCollection ». Dans le panneau d’inspecteur, en regard de deux manipulation transmis « type », cliquez sur le menu déroulant et sélectionnez « échelle ». Cela rend afin que l’utilisateur peut modifier uniquement la taille.

![Lesson4 Chapter2 Step2im](images/Lesson4_Chapter2_step2im.PNG)

3. Modifier la couleur de chaque cube afin que nous pouvons faire la distinction entre eux. 
-   Accédez au panneau de projet et faites défiler jusqu'à ce que vous consultez « MixedRealityToolkit.SDK », puis sélectionnez.
-   Sélectionnez le dossier « Ressources Standard ».
-   Cliquez sur le dossier « documents ».
-   Faites glisser un matériau différents sur chacun de vos cubes. 

>Remarque: Vous pouvez choisir n’importe quelle couleur pour vos cubes. Dans notre exemple, nous allons utiliser « glowingcyan », « glowingorange » et « écologique ». N’hésitez pas à faire des essais avec différentes couleurs. Pour ajouter la couleur au cube, cliquez sur le cube que vous souhaitez modifier la couleur de, puis faites glisser le matériel au champ de matériau du convertisseur maillage dans le panneau d’inspecteur du cube. 

![Lesson4 Chapter2 Step3im](images/Lesson4_Chapter2_step3im.PNG)

4. Sélectionnez un autre cube dans l’objet « 3DObjectCollection » et faire en sorte que son déplacement est limitée à la distance de correctif à partir de la tête. Pour ce faire, sur la droite de « contrainte sur le déplacement », cliquez sur le menu déroulant et sélectionnez « corriger la distance à partir de la tête. » Cela rend afin que l’utilisateur peut déplacer uniquement le cube dans leur champ de vision. 

![Lesson4 Chapter2 Step4im](images/Lesson4_chapter2_step4im.PNG)

Objectif des étapes suivantes : Nous allons activer la manipulation et l’interaction avec nos objets 3D. Nous allons appliquer les paramètres de manipulation différents 

5. Sélectionnez l’objet fromage et dans ce panneau, cliquez sur « Ajouter le composant ». 

6. Recherchez dans la zone de recherche « Près Interaction Grabbable » et sélectionnez le script. Ce composant permet aux utilisateurs de contacter et récupérer les objets des mains suivies. Objets également pourront être manipulé à partir d’une distance, à moins que la case à cocher « Autoriser présent Manipulation » est désactivée (indiquée par un cercle vert dans l’image ci-dessous).

![Lesson4 Chapter2 Step6im](images/Lesson4_Chapter2_step6im.PNG)

7. Ajoutez « Près Interaction Grabbable » aux huit objet, objet platoniques, core de terre, lunaire module et tasse de café en répétant l’étape 5 et 6 sur ces objets.

8. Supprimer la possibilité de manipulation lointain de l’objet de huit. Pour ce faire, sélectionnez le huit dans la hiérarchie et décochez la case à cocher « Autoriser la manipulation lointain » (marqué par un cercle vert). Cela rend afin que les utilisateurs peuvent interagir uniquement avec le huit directement à l’aide de mains suivies.

>Remarque: Pour la documentation complète du composant de gestionnaire de manipulation et il est associé à des paramètres, reportez-vous à la [MRTK Documentation](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ManipulationHandler.html).

9. Vérifiez que le composant « Près Interaction Grabbable » a été ajouté à la base de la terre, le module lunaire et la tasse de café (voir l’étape 7).

10. Pour le module lunaire, modifier les paramètres du Gestionnaire de Manipulation afin qu’il pivote autour de l’objet center pour les deux près et interaction lointain, comme indiqué dans l’image ci-dessous.

![Lesson4 Chapter2 Step10im](images/Lesson4_chapter2_step10im.PNG)

11: Pour le noyau de la terre, modifier le comportement de mise en production pour « nothing ». Cela rend afin qu’une fois que le cœur de la terre est libéré de la compréhension des utilisateurs, il cesse de déplacer. 

![Lesson4 Chapter2 Step11im](images/Lesson4_Chapter2_step11im.PNG)

> Remarque: Ce paramètre est utile pour les scénarios tels que la création d’une boule que vous pouvez lever. En conservant la rapidité et la vitesse angulaire rend afin qu’une fois la balle est libérée il continuera à déplacer, à la vitesse, qu'il a été lancé à, semblable au comporte d’une boule physique.

### <a name="adding-bounding-boxes"></a>Ajout de zones englobantes
Zones englobantes rendent plus simple et plus intuitive pour manipuler des objets d’une seule main pour la manipulation directe (près interaction) et de manipulation en fonction de ray (interaction lointain). Zones englobantes offrent des « handles » qui peuvent être saisies pour la mise à l’échelle et faire pivoter des objets le long des axes spécifiques.
>Remarque: Avant de pouvoir ajouter un rectangle englobant pour un objet, que vous devez d’abord disposer un collider sur l’objet (par exemple, un collider boîte.) Comme nous l’avons fait précédemment dans cette leçon. Colliders peuvent être ajoutés en sélectionnant l’objet et dans le panneau d’inspecteur de l’objet en sélectionnant Ajouter un composant > Collider de zone.
>

1. Ajouter un collider de zone à l’objet principal de la terre, si celle-ci n’existe pas (collider de zone et le programme d’installation ne pas requis si vous utilisez le préfabriqué fourni dans le dossier ressources de Module de Base, par les instructions fournies.) Dans le cas le cœur de la terre, nous devrons ajouter le collider de zone à l’objet « node_id30 » sous le cœur de la terre, comme illustré dans l’image ci-dessous. Sélectionnez node_id30 et dans l’onglet inspecteur de l’objet, cliquez sur « Ajouter un composant » et recherchez « zone collider. » 

![Lesson4 chapitre3 Step1im](images/Lesson4_Chapter3_step1im.PNG)

![Lesson4 chapitre3 Step2im](images/Lesson4_chapter3_step2im.PNG)

> Remarque: Veillez à visualiser le collider zone afin qu’il n’est pas trop grand ou trop petit. Il doit être à peu près la même taille que l’objet qu'autour de (dans cet exemple, le cœur de la terre). Ajustez le collider zone selon vos besoins en sélectionnant l’option de collider modifier dans le collider de zone. Vous pouvez changeant x, y, les valeurs z ou faites glisser les gestionnaires de zone englobante dans la fenêtre Éditeur de la scène. 

![Lesson4 chapitre3 Noteim](images/Lesson4_Chapter3_noteim.PNG)

2. Ajouter un rectangle englobant pour l’objet « node_id30 » de la base la terre. Pour ce faire, sélectionnez l’objet « node_id30 » à partir de « 3DObjectCollection ». Dans l’onglet inspecteur, cliquez sur « Ajouter un composant » et recherchez « englobant ». Assurez-vous que la zone englobante, collider de zone et des scripts de manipulation (Gestionnaire de manipulation, près d’interaction grabbable) sont tous sur le même objet de jeu.

3.  Dans la section « Comportement » de la zone englobante, sélectionnez « Activer au démarrage » dans la liste déroulante de l’Activation. Pour consulter des détails supplémentaires concernant les différentes options d’activation et d’autres options de zone englobante, veuillez consulter la [MRTK de délimitation de la documentation de zone](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_BoundingBox.html>)

   

   *Dans les prochaines étapes, nous modifierons également l’aspect de la zone englobante en ajustant le matériau de zone par défaut, le matériel pendant qu’il est en cours saisi, ainsi que la visualisation de descripteurs (handles angle et latérales). Le MRTK contient plusieurs options pour personnaliser la zone englobante.*

4. Dans le volet de projet, recherchez « boundingbox » et vous verrez une liste des matériaux désigné par une sphère bleu dans les résultats de recherche, comme indiqué dans l’image ci-dessous. 

5. Faites glisser le matériel « boundingbox » dans l’emplacement de matériau boîte sur le composant de zone englobante. Également saisir le matériel de « boundingboxgrabbed » et placez-la dans l’emplacement de matériau grabbed boîte sur le composant de zone englobante.

6. Faites glisser le matériel de « MRTK_BoundingBox_ScaleWidget » dans l’emplacement prefab de handle de mise à l’échelle sur le composant de zone englobante. 

7. Faites glisser le matériel de « MRTK_BoundingBox_RotateWidget » dans l’emplacement de la poignée de rotation sur le composant de zone de collage.

![Lesson4 chapitre3 7Im de l’étape 4](images/Lesson4_chapter3_step4-7im.PNG)

8. Assurez-vous que la zone englobante ciblée par l’objet de droite. Dans le composant de zone englobante, il est le « objet cible » et des scripts « délimite override ». Veillez à faire glisser l’objet qui a le cadre englobant autour d’elle à deux de ces emplacements. Dans cet exemple, faites glisser l’objet « node_id30 » pour les deux de ces emplacements, comme indiqué dans l’image ci-dessous.

> Lorsque vous démarrez ou que vous lire de l’application, votre objet sera désormais entourée d’un cadre bleu. Vous êtes invité à faire glisser les angles de ce frame pour redimensionner l’objet. Si nous voulons que les poignées de mise à l’échelle et les poignées de rotation à être plus visibles et plus volumineux, nous vous recommandons d’utiliser la valeur par défaut englobant les paramètres de zone (en évitant les étapes 4 à 7.) 

![Lesson4 chapitre3 Step8im](images/Lesson4_Chapter3_step8im.PNG)

9. Pour revenir à la valeur par défaut englobant la visualisation de zone, dans le panneau de l’inspecteur de l’objet de la zone englobante, sélectionnez le préfabriqué de handle de rotation et appuyez sur la touche SUPPR, vous voyez maintenant une visualisation de zone englobante similaire à l’image ci-dessous. Remarque : les visualisations englobant de la zone s’affiche uniquement en mode de lecture.

![Lesson4 chapitre3 Step9im](images/Lesson4_chapter3_step9im.PNG)

### <a name="adding-touch-effects"></a>Ajout d’effets de tactile
Dans cet exemple, nous allons émettre un son lorsque vous appuyez sur un objet avec votre main.

1. Ajouter un composant source audio à votre objet de jeu. Sélectionnez l’objet « huit » dans votre hiérarchie de la scène. Dans ce panneau, cliquez sur le bouton « Ajouter un composant », recherchez et sélectionnez « source audio ». Nous allons utiliser cette source audio pour émettre un son dans une étape ultérieure. 

>Remarque: Assurez-vous que l’objet « Huit » a un collider boîte dessus.

2. Ajouter le composant « près interaction touchable ». Cliquez sur le bouton « Ajouter un composant » dans le panneau Inspecteur et recherchez « interaction touchable à proximité ». Sélectionner pour ajouter le composant. Remarque : corriger la capture d’écran pour mettre en évidence que nous allons ajouter le composant et pas seulement la mise en surbrillance collider de zone.

>Remarque: Précédemment, nous avons ajouté « near interaction grabbable. » La différence entre ceci et « quasi interaction touchable » est que l’interaction « grabbable » est destinée à un objet à être saisi et les exploiter. Le « touchable » a été conçu pour l’objet à modifier. Les deux composants peuvent être utilisés ensemble pour une combinaison d’interactions.

![Lesson4 chapitre4 Step1 2Im](images/Lesson4_chapter4_step1-2im.PNG)

3. Ajoutez dans le script « tactile d’interaction de transférer ». Notez que ce script est inclus dans la scène unity que vous avez importé dans le cadre de ce package de démonstration et il n’est pas inclus dans le MRTK d’origine. Simplement, comme l’étape précédente, cliquez sur « Ajouter un composant » et recherchez « touch d’interaction main » pour l’ajouter. 
   Notez que vous disposez de 3 options avec le script : 

   - « Sur touch terminée. » Cette opération déclenche quand vous touchez et libérez l’objet. 
   - « Sur tactile prise en main. » Cette opération déclenche lorsque l’objet est touché. 
   - « Sur touch mis à jour. » Cela déclenche périodiquement pendant que votre main touche l’objet. 

   Pour cet exemple, nous travaillerons avec le paramètre « sur touch démarré ».

4. Cliquez sur le bouton « + » sur l’option « on touch démarré », comme illustré dans l’image ci-dessous. Dans le champ vide, faites glisser l’objet de huit. 

5. Dans la liste déroulante indiquant « aucune fonction » (en haut du rectangle vert dans l’image ci-dessous), sélectionnez AudioSource > PlayOneShot. Nous allons ajouter un clip audio à ce champ en utilisant les concepts ci-dessous :

   - Le MRTK fournit-il une petite liste d’éléments audio. N’hésitez pas à Explorer ces éléments dans le panneau de votre projet. Vous les trouverez sous le dossier « MixedRealityToolkit.SDK », puis le dossier « ressources standard ». Il vous verrez un dossier « audio » qui contient tous les clips audio.
   - Pour cet exemple, nous allons utiliser le clip audio « MRTK_Gem ». 
   - Pour ajouter un clip audio, faites simplement glisser l’image souhaitée à partir du panneau projet dans le AudioSource.PlayOneShot (marqués par zone verte dans l’exemple ci-dessus) dans le panneau de l’inspecteur.

   Maintenant lorsque l’utilisateur contacte et touche l’objet de huit, la piste audio « MRTK_Gem » sera lu. Le script « Main Interaction tactile » s’ajuste également la couleur de l’objet au toucher. 

![Étape 3 de chapitre4 Lesson4 Noteim 5](images/Lesson4_chapter4_step3-5-noteim.PNG)

### <a name="congratulations"></a>Félicitations ! 
Dans cette leçon, vous avez appris comment organiser les objets 3D dans une collection de grille et manipuler des objets 3D (mise à l’échelle, faire pivoter et déplacement) à l’aide de proche interaction (en saisissant directement des mains suivies) et l’interaction lointain (à l’aide des rayons du pointage de regard ou main rayons.) Appris à placer des cadres de sélection autour des objets 3D de que vous avez appris à utiliser et personnaliser les gizmos sur les zones englobantes. Enfin, vous avez appris à déclencher des événements de toucher un objet.

[Leçon suivante : Entrée avancée](mrlearning-base-ch5.md)

