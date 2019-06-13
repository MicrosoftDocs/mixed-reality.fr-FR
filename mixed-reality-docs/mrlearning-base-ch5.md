---
title: Module d’apprentissage de base sur la réalité mixte - Entrée avancée
description: Suivez ce cours pour découvrir comment implémenter Reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 32141aafd43c5d729919673509c93bb2014edd37
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719896"
---
# <a name="mr-learning-base-module---advanced-input"></a>Module d’apprentissage de base sur la réalité mixte - Entrée avancée

Dans cette leçon, nous allons examiner plusieurs options d’entrée avancée pour HoloLens 2, notamment l’utilisation de commandes vocales, le mouvement de panoramique et l’eye-tracking. 

## <a name="objectives"></a>Objectifs

- Découvrir comment déclencher des événements à l’aide de mots clés et de commandes vocales
- Utiliser le suivi des mains pour faire un panoramique sur des textures et des objets 3D
- Tirer parti des fonctionnalités d’eye-tracking d’HoloLens 2 pour sélectionner des objets

## <a name="instructions"></a>Instructions

### <a name="enabling-voice-commands"></a>Activation des commandes vocales

Dans cette section, nous allons implémenter deux commandes vocales. Tout d’abord, la capacité à activer/désactiver le panneau de diagnostics de fréquence d’images en disant « toggle diagnostics ». Ensuite, la capacité à émettre un signal sonore avec une commande vocale. Nous allons tout d’abord examiner les profils et les paramètres MRTK responsables de la configuration des commandes vocales. 

1. Dans la hiérarchie Base Scene, sélectionnez « MixedRealityToolkit ». Dans le panneau d’inspecteur, faites défiler jusqu’aux paramètres du système d’entrée. Double-cliquez pour ouvrir le profil de système d’entrée. Clonez le profil de système d’entrée pour le rendre modifiable, comme vous l’avez appris dans la [Leçon 1](mrlearning-base-ch1.md). 

Dans le profil de système d’entrée, vous verrez différents paramètres. Pour les commandes vocales, descendez jusqu’à « Speech Command Settings ». 

![Lesson5 Chapter1 Step2im](images/Lesson5_Chapter1_step2im.PNG)

2. Clonez le profil de commandes de reconnaissance vocale pour le rendre modifiable, comme vous l’avez appris dans la [Leçon 1](mrlearning-base-ch1.md). Double-cliquez sur le profil de commandes de reconnaissance vocale ; toute une gamme de paramètres s’affiche. Pour obtenir une description complète de ces paramètres, consultez la [documentation sur la reconnaissance vocale MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Speech.html>). 

>Remarque: Par défaut, le comportement général est le démarrage automatique. Vous pouvez choisir le démarrage manuel si vous le souhaitez, mais pour cet exemple nous allons conserver le démarrage automatique. Le MRTK est fourni avec plusieurs commandes vocales par défaut (par exemple menu, toggle diagnostics et toggle profiler). Nous allons utiliser le mot clé « toggle diagnostics » pour activer et désactiver le compteur de fréquence d’images de diagnostics. Nous allons également ajouter une nouvelle commande vocale lors des étapes ci-dessous.
>
> ![Lesson5 Chapter1 Noteim](images/Lesson5_chapter1_noteim.PNG)

3. Ajoutez une nouvelle commande vocale. Pour ajouter une nouvelle commande vocale, cliquez sur le bouton « + add a new speech command » et vous verrez une nouvelle ligne apparaître sous la liste des commandes vocales existantes. Tapez la commande vocale à utiliser. Dans cet exemple, nous allons utiliser la commande « play music ».

>Astuce : Vous pouvez également définir un code de touche pour les commandes vocales. Cela permet de déclencher des commandes vocales lors d’un appui sur une touche du clavier.   

4. Ajoutez la capacité à répondre aux commandes vocales. Sélectionnez n’importe quel objet dans la hiérarchie de la scène de base auquel n’est attaché aucun autre script d’entrée (par exemple aucun gestionnaire de manipulation). Dans le panneau d’inspecteur, cliquez sur « add component ». Tapez « speech input handler ». Sélectionnez-le.
   ![Lesson5 Chapter1 Step4im](images/Lesson5_chapter1_step4im.PNG)

   

Par défaut, vous verrez deux cases à cocher, dont « is focus required ». Cela signifie que tant que vous pointez vers l’objet avec un rayon de suivi (suivi du regard, suivi de la tête, suivi de contrôle ou suivi de la main), la commande vocale est déclenchée. Décochez cette case pour faire en sorte que l’utilisateur ne soit pas obligé de regarder l’objet pour utiliser la commande vocale.

5. Ajoutez la capacité à répondre à une commande vocale. Pour cela, cliquez sur le bouton « + » qui se trouve dans le gestionnaire d’entrée vocale et sélectionnez le mot clé auquel vous souhaitez répondre.

   > Remarque: Ces mots clés sont renseignés d’après le profil que vous avez modifié à l’étape précédente.

![Lesson5 Chapter1 Step5im](images/Lesson5_chapter1_step5im.PNG)

6. En regard de « Keyword » figure un menu déroulant. Sélectionnez « Toggle Diagnostics ». Ainsi, chaque fois que l’utilisateur prononcera l’énoncé « toggle diagnostics », une action sera déclenchée. Notez que vous devrez peut-être développer « element 0 » en appuyant sur la flèche qui se trouve à côté.

![Lesson5 Chapter1 Step6im](images/Lesson5_chapter1_step6im.PNG)

7. Ajoutez le script « Diagnostics Demo Controls » pour activer ou désactiver le diagnostic de compteur de fréquence d’images. Pour cela, appuyez sur le bouton « add component » et recherchez le script « Diagnostics Demo Controls », puis ajoutez-le à partir du menu. Ce script peut être ajouté à n’importe quel objet, mais par souci de simplicité nous allons l’ajouter au même objet que le gestionnaire d’entrée vocale. 

   > Remarque : Ce script est fourni uniquement avec ces modules ; il n’est pas fourni avec le MRTK d’origine.

![Lesson5 Chapter1 Step7im](images/Lesson5_chapter1_step7im.PNG)

8. Ajoutez une nouvelle réponse dans le gestionnaire d’entrée vocale. Pour cela cliquez sur le bouton « + » sous « response () » (marqué par une flèche verte dans l’image ci-dessous).

![Lesson5 Chapter1 Step7im](images/Lesson5_chapter1_step8.PNG)

9. Faites glisser l’objet qui contient le script Diagnostics Demo Controls vers la nouvelle réponse que vous venez de créer à l’étape 8.
    ![Lesson5 Chapter1 Step9im](images/Lesson5_chapter1_step9im.PNG)

10. Maintenant, sélectionnez la liste déroulante « no function », sélectionnez les contrôles de démonstration de diagnostic, puis « on toggle diagnostics () ». Cette fonction active et désactive vos diagnostics.  ![Lesson5 Chapter1 Step10im](images/Lesson5_chapter1_step10im.PNG)
    
> Notez qu’avant la génération sur votre appareil vous devez activer les paramètres de microphone. Pour cela, cliquez sur le fichier, accédez aux paramètres de génération, puis aux paramètres du lecteur, et vérifiez que la fonctionnalité de microphone est activée.

Maintenant, nous allons ajouter la capacité à lire un fichier audio à partir d’une commande vocale à l’aide de l’objet « octa ». Souvenez-vous que dans la [Leçon 4](mrlearning-base-ch4.md) nous avons ajouté la capacité à lire un clip audio en cas de toucher sur l’objet octa. Nous allons utiliser cette même source audio pour notre commande vocale de musique.

11. Sélectionnez l’objet octa dans la hiérarchie de la scène de base.

12. Ajoutez un autre gestionnaire d’entrée vocale (répétez les étapes 4 et 5), mais avec l’objet octa. 

13. Au lieu d’ajouter la commande vocale « Toggle Diagnostics » de l’étape 6, ajoutez la commande vocale « play music », comme illustré dans l’image ci-dessous.
    
     ![Lesson5 Chapter1 Step13im](images/Lesson5_chapter1_step13im.PNG)
    
    
    
14. Comme avec les étapes 8 et 9, ajoutez une nouvelle réponse et faites glisser l’objet octa vers l’emplacement vide sur la réponse.

15. Sélectionnez le menu déroulant « no function », sélectionnez « Audio Source », puis « PlayOneShot (AudioClip) ».

![Lesson5 Chapter1 Step15im](images/Lesson5_chapter1_step15im.PNG)

16. Comme clip audio, pour cet exemple nous allons utiliser celui de la [Leçon 4](mrlearning-base-ch4.md). Accédez au panneau de votre projet, recherchez le clip audio « MRTK_Gem » et faites-le glisser vers l’emplacement de source audio, comme illustré dans l’image ci-dessous. Maintenant, votre application devrait pouvoir répondre aux commandes vocales « toggle diagnostics » pour activer/désactiver le panneau de compteur de fréquence d’images et « play music » pour lire la chanson MRTK_Gem.
     ![Lesson5 Chapter1 Step16im](images/Lesson5_chapter1_step16im.PNG)


### <a name="the-pan-gesture"></a>Le mouvement panoramique 

Dans ce chapitre, nous allons découvrir comment utiliser le mouvement panoramique. Il est utile pour le défilement (utilisation d’un doigt ou de la main pour faire défiler le contenu). Vous pouvez également utiliser le mouvement panoramique pour faire pivoter des objets, parcourir une collection d’objets 3D ou même faire défiler une interface utilisateur 2D. Nous allons découvrir comment utiliser le mouvement panoramique pour déformer une texture. Nous verrons aussi comment déplacer une collection d’objets 3D.

1. Créez un quad. Dans votre hiérarchie de scène de base, cliquez avec le bouton droit, sélectionnez « 3D Object », puis « Quad ».

![Lesson5 Chapter2 Step2im](images/Lesson5_chapter2_step2im.PNG)

2. Repositionnez le quad comme il convient. Dans notre exemple, nous définissons x = 0, y = 0 et z = 1,5 par rapport à la caméra, afin de bénéficier d’une position confortable à partir de l’HoloLens 2.

   > Remarque: Si le quad bloque (apparaît devant) du contenu des leçons précédentes, n’oubliez pas de le déplacer afin qu’il ne bloque aucun autre objet.

3. Appliquez un matériau au quad. Il s’agira du matériau que nous ferons défiler avec le mouvement panoramique. 

![Lesson5 Chapter2 Step3im](images/Lesson5_chapter2_step3im.PNG)

4. Dans le panneau de votre projet, tapez « pan content » dans la zone de recherche. Faites glisser ce matériau sur le quad dans votre scène. 

> Remarque: Le matériau « Pan content » n’est pas fourni avec le MRTK ; il s’agit d’un élément multimédia du package de ressources de ce module, tel qu’importé dans les leçons précédentes. 

> Remarque: Quand vous ajoutez le contenu de panoramique, il peut apparaître étiré. Vous pouvez résoudre ce problème en ajustant les valeurs x, y et z de la taille du quad jusqu’à être satisfait de son aspect.

Pour utiliser le mouvement panoramique, vous avez besoin d’un collider sur votre objet. Vous constaterez que le quad a déjà un mesh collider. Toutefois, celui-ci n’est pas idéal, car il est extrêmement fin et difficile à sélectionner. Nous vous suggérons de le remplacer par un box collider.

5. Cliquez avec le bouton droit sur le mesh collider qui se trouve sur le quad (dans le panneau d’inspecteur), puis supprimez-le en cliquant sur « remove component ». 
   ![Lesson5 Chapter2 Step5im](images/Lesson5_chapter2_step5im.PNG)

6. Ajoutez maintenant le box collider en cliquant sur « add component » et en recherchant « box collider. » Le box collider ajouté par défaut étant encore trop fin, cliquez sur le bouton « edit collider » pour le modifier. Vous pouvez ajuster la taille à l’aide des valeurs x, y et z ou des éléments dans l’éditeur de scène. Dans notre exemple, nous voulons étendre un peu le box collider derrière le quad. Dans l’éditeur de scène, faites glisser le box collider de l’arrière vers l’extérieur (voir l’image ci-dessous). Cela permettra à l’utilisateur d’utiliser non seulement son doigt, mais toute sa main pour faire défiler. 
    ![Lesson5 Chapter2 Step6im](images/Lesson5_chapter2_step6im.PNG)
7. Rendez-le interactif. Comme nous souhaitons interagir directement avec le quad, nous devons utiliser le composant « near interaction touchable » (nous l’avons également utilisé dans la Leçon 4 pour lire la musique de l’objet octa). Cliquez sur « add component », recherchez « near interaction touchable » et sélectionnez-le, comme indiqué dans les images ci-dessous. 

8. Ajoutez la capacité à reconnaître le mouvement panoramique. Cliquez sur « add component » et tapez « hand interaction pan ». Vous aurez le choix entre « hand ray » (qui vous permet de faire un panoramique à distance) et « index finger ». Pour cet exemple, conservez « index finger ». 
    ![Lesson5 Chapter2 Step7 8Im](images/Lesson5_chapter2_step7-8im.PNG)

![Lesson5 Chapter2 Step8im](images/Lesson5_chapter2_step8im.PNG)

9. Dans le script « Hand Interaction Pan », les cases à cocher « lock horizontal » et « lock vertical » verrouilleront les mouvements respectivement horizontalement et verticalement. Les paramètres d’habillage de texture feront en sorte que la texture (mappage de texture) suive les mouvements de panoramique de l’utilisateur. Pour cet exemple, nous allons cocher cette case. Il y a aussi la case « velocity active ». Si elle est décochée, le mouvement panoramique ne fonctionnera pas. Cochez aussi cette case. Vous devriez maintenant avoir un quad prenant en charge le panoramique.

   

   Voyons maintenant comment faire un panoramique d’objets 3D. 

10. Cliquez avec le bouton droit sur l’objet quad, sélectionnez « 3D Object », puis cliquez sur « Cube ». Mettez le cube à l’échelle avec des valeurs d’environ x = 0,1, y = 0,1 et z = 0,1. Copiez trois fois ce cube (en cliquant dessus avec le bouton droit et en appuyant sur « Duplicate », ou en appuyant sur Contrôle/Commande D). Espacez-les uniformément. Votre scène doit ressembler à l’image ci-dessous.

![Lesson5 Chapter2 Step10im](images/Lesson5_chapter2_step10im.PNG)







11. Sélectionnez à nouveau le quad et, sous le script « Hand Interaction Pan », nous allons définir les actions de panoramique pour chacun des cubes. Sous « pan event receivers », nous devons spécifier le nombre d’objets qui reçoivent l’événement. Comme il y a quatre cubes, tapez « 4 » puis appuyez sur Entrée. Quatre champs vides doivent apparaître.


![Lesson5 Chapter2 Step11im](images/Lesson5_chapter2_step11im.PNG)



12. Faites glisser chacun des cubes vers chacun des emplacements d’éléments vides.
     ![Lesson5 Chapter2 Step12im](images/Lesson5_chapter2_step12im.PNG)
    
13. Ajoutez le script « Move With Pan » à tous les cubes. Pour cela, maintenez enfoncée Contrôle/Commande et sélectionnez chaque objet. Ensuite, dans le panneau d’inspecteur, cliquez sur « add component » et recherchez « Move With Pan ». Cliquez sur le script pour l’ajouter à chaque cube. Désormais, les objets 3D se déplaceront avec votre mouvement panoramique ! Si vous supprimez le maillage sur votre quad, vous devriez maintenant avoir un quad invisible où vous pouvez faire un panoramique dans une liste d’objets 3D.

### <a name="eye-tracking"></a>Eye-tracking

Dans ce chapitre, nous allons examiner comment activer l’eye-tracking dans notre démo. Nous allons faire tourner lentement les éléments de menu 3D quand l’utilisateur les fixe du regard, grâce aux fonctionnalités de suivi du regard. Nous déclencherons également un effet attrayant quand l’élément regardé est sélectionné.

1. Vérifiez que les profils Mixed Reality Toolkit sont configurés correctement. À ce jour, la configuration de profil Mixed Reality Toolkit n’inclut pas de fonctionnalités d’eye-tracking par défaut. Pour ajouter des fonctionnalités d’eye-tracking, suivez les instructions fournies dans la section « Setting up the MRTK profiles required for Eye Tracking » de la [Documentation de Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#setting-up-the-mrtk-profiles-required-for-eye-tracking  ). Vérifiez que l’eye-tracking est configuré correctement en suivant les étapes restantes décrites dans la documentation fournie en lien ci-dessus, notamment l’activation de l’eye-tracking dans GazeProvider (composant attaché à la caméra) et l’activation de la simulation de l’eye-tracking dans l’éditeur Unity. Notez que les versions ultérieures du MRTK pourront inclure l’eye-tracking par défaut.

    Le lien ci-dessus fournit de brèves instructions pour les tâches suivantes :

    - Création de l’Eye Gaze Data Provider pour une utilisation dans le profil MRTK
    - Activation de l’eye-tracking dans le Gaze Provider
    - Configuration de la simulation de l’eye-tracking dans l’éditeur
    - Modification des fonctionnalités de la solution Visual Studio pour permettre l’eye-tracking dans l’application générée

2. Ajoutez le composant Eye Tracking Target aux objets cibles. Pour permettre à un objet de répondre aux événements de suivi du regard, nous devons ajouter le composant EyeTrackingTarget sur chaque objet avec lequel nous souhaitons interagir à l’aide du suivi du regard. Ajoutez ce composant à chacun des neuf objets 3D qui font partie de la collection de la grille. Conseil : Sélectionnez plusieurs éléments dans la hiérarchie pour ajouter en bloc le composant EyeTrackingTarget.
    ![Lesson5 Chapter3 Step2](images/Lesson5Chapter3Step2.JPG)

3. Maintenant, nous allons ajouter le script EyeTrackingTutorialDemo pour obtenir quelques interactions intéressantes. Le script EyeTrackingTutorialDemo est fourni dans le cadre du référentiel de cette série de tutoriels ; il n’est pas fourni par défaut avec Mixed Reality Toolkit. Pour chaque objet 3D de la collection de grille, ajoutez le script EyeTrackingTutorialDemo en recherchant le composant dans le menu « Add Component ».
   ![Lesson5 Chapter3 Step3](images/Lesson5Chapter3Step3.JPG)

   4. Faites pivoter l’objet tout en observant la cible. Nous souhaitons configurer notre objet 3D pour qu’il pivote pendant que nous le regardons. Pour cela, insérez un nouveau champ dans la section « While Looking At Target » du composant EyeTrackingTarget, comme indiqué dans l’image ci-dessous. 

![Lesson5 Chapter3 Step4a](images/Lesson5Chapter3Step4a.JPG)
![Lesson5 Chapter3 Step4b](images/Lesson5Chapter3Step4b.JPG)



Dans le nouveau champ vide, ajoutez l’objet Game actif, puis sélectionnez EyeTrackingTutorialDemo > RotateTarget() comme indiqué dans l’image ci-dessous. L’objet 3D est maintenant configuré pour pivoter quand il est le focus de l’eye tracking. 

5. Ajoutez la fonctionnalité « blip target » sur la cible pointée du regard lors de sa sélection (appui en l’air ou prononciation de l’énoncé « select »). Comme pour l’étape 4, nous souhaitons déclencher EyeTrackingTutorialDemo > BlipTarget() en l’affectant au champ « Select() » de l’objet Game du composant EyeTrackingTarget, comme illustré dans la figure ci-dessous. Ceci étant désormais configuré, vous remarquerez un léger spot dans l’objet Game chaque fois que vous déclencherez une action de sélection, telle qu’un appui en l’air ou la commande vocale « select ». 
    ![Lesson5 Chapter3 Step5](images/Lesson5Chapter3Step5.JPG)
6. Vérifiez que les fonctionnalités d’eye-tracking sont configurées correctement avant la génération dans HoloLens 2. À ce jour, Unity n’offre pas encore la possibilité de configurer la fonctionnalité d’entrée de pointage du regard (pour l’eye-tracking). La configuration de cette fonctionnalité est nécessaire pour que l’eye-tracking fonctionne sur HoloLens 2. Suivez ces instructions fournies dans la documentation de Mixed Reality Toolkit pour activer la fonctionnalité d’entrée de pointage du regard : https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2 


### <a name="congratulations"></a>Félicitations ! 
Vous avez réussi à ajouter des fonctionnalités d’eye-tracking de base à l’application. Ces premiers pas vous ouvrent la voie vers tout un monde de possibilités avec l’eye-tracking. Ce chapitre conclut également la leçon 5, où nous avons découvert des fonctionnalités d’entrée avancées telles que les commandes vocales, les mouvements panoramiques et l’eye-tracking. 

[Leçon suivante : Exemple d’expérience d’assembly de module lunaire](mrlearning-base-ch6.md)

