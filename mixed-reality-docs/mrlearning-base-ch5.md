---
title: Module MR Learning Base - avancées d’entrée
description: Terminer ce cours pour apprendre à implémenter la reconnaissance faciale de Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
ms.localizationpriority: high
keywords: réalité mixte, hololens (didacticiel), unity,
ms.openlocfilehash: 32141aafd43c5d729919673509c93bb2014edd37
ms.sourcegitcommit: 1c0fbee8fa887525af6ed92174edc42c05b25f90
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65730932"
---
# <a name="mr-learning-base-module---advanced-input"></a>Module MR Learning Base - avancées d’entrée

Dans cette leçon, nous allons examiner plusieurs des options avancées d’entrée pour la version 2 HoloLens, y compris l’utilisation de commandes vocales, le mouvement de panoramique et un suivi de le œil. 

## <a name="objectives"></a>Objectifs

- Découvrez comment déclencher des événements à l’aide de mots clés et des commandes vocales
- Utiliser des mains suivies pour effectuer un panoramique de textures et des objets 3D
- Tirer parti des yeux du 2 de HoloLens des capacités pour sélectionner des objets de suivi

## <a name="instructions"></a>Instructions

### <a name="enabling-voice-commands"></a>L’activation des commandes vocales

Dans cette section, nous vous implémenterez deux commandes vocales. Tout d’abord, la possibilité d’activer/désactiver le panneau de diagnostics de taux de frame en disant « activer/désactiver les diagnostics ». Deuxièmement, la possibilité d’émettre un signal sonore avec une commande de la voix. Nous allons tout d’abord examiner les profils MRTK et les paramètres chargés de la configuration des commandes vocales. 

1. Dans la hiérarchie de la scène de Base, sélectionnez « MixedRealityToolkit ». Dans le panneau d’inspecteur, faites défiler les paramètres du système d’entrée. Double-cliquez pour ouvrir le profil de système d’entrée. Cloner le profil de système d’entrée pour le rendre modifiable, comme nous l’avez appris dans [leçon 1](mrlearning-base-ch1.md) 

Dans le profil de système d’entrée, vous verrez une variété de paramètres. Pour les commandes vocales, descend jusqu’aux intitulée, « Paramètres de commande vocale ». 

![Lesson5 Chapter1 Step2im](images/Lesson5_Chapter1_step2im.PNG)

2. Cloner le profil de commandes de reconnaissance vocale pour le rendre modifiable, comme nous l’avez appris dans [leçon 1](mrlearning-base-ch1.md). Double-cliquez sur le profil de la commande vocale, où vous remarquerez un éventail de paramètres. Pour obtenir une description complète de ces paramètres, consultez le [documentation de reconnaissance vocale MRTK](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Speech.html>). 

>Remarque: Par défaut, le comportement général est le démarrage automatique. Qui peut être modifiée pour le démarrage manuel si vous le souhaitez, mais pour cet exemple nous allons conserver sur le démarrage automatique. Le MRTK est fourni avec plusieurs commandes de voix par défaut (par exemple, menu, activer/désactiver des diagnostics et du Générateur de profils bascule). Nous allons utiliser le mot clé « activer/désactiver diagnostics » afin d’activer et désactiver le compteur de fréquence d’images de diagnostics. Nous allons également ajouter une nouvelle commande vocal dans les étapes ci-dessous.
>
> ![Lesson5 Chapter1 Noteim](images/Lesson5_chapter1_noteim.PNG)

3. Ajouter une nouvelle commande de voix. Pour ajouter une nouvelle commande de voix, cliquez sur le bouton « + Ajouter une nouvelle commande vocale » et vous verrez une nouvelle ligne apparaît vers le bas sous la liste des commandes vocales existantes. Tapez la commande de la voix à utiliser. Dans cet exemple musicample nous allons utiliser la commande « musique ».

>Astuce : Vous pouvez également définir un code de touche pour les commandes vocales. Cela permet des commandes vocales pour déclencher des appui sur une touche du clavier.   

4. Ajouter la possibilité de répondre aux commandes vocales. Sélectionnez n’importe quel objet dans la hiérarchie de la scène de base qui n’a pas de tous les autres scripts d’entrée attachés (par exemple, aucun gestionnaire de manipulation.) Dans ce panneau, cliquez sur « Ajouter le composant ». Tapez « Gestionnaire d’entrée vocale ». Sélectionnez-le.
   ![Lesson5 Chapter1 Step4im](images/Lesson5_chapter1_step4im.PNG)

   

Par défaut, vous verrez 2 cases à cocher, une est la case à cocher « n’est nécessaire de focus ». Cela signifie que tant que vous pointez l’objet avec un regards ray, (OCULAIRE, head-regards, regards de contrôleur ou du pointage de regard main) la commande vocale est déclenchée. Décochez cette case à cocher pour faire en sorte que l’utilisateur ne dispose pas d’examiner l’objet à utiliser les commandes vocales.

5. Ajouter la capacité à répondre à une commande de la voix. Pour ce faire, cliquez sur le bouton « + » qui se trouve dans le Gestionnaire d’entrée vocale et sélectionnez le mot clé que vous souhaitez répondre à.

   > Remarque: Ces mots clés sont remplies basé sur le profil que vous avez modifié à l’étape précédente.

![Lesson5 Chapter1 Step5im](images/Lesson5_chapter1_step5im.PNG)

6. En regard de « Keyword », vous verrez un menu déroulant. Sélectionnez « Activer/désactiver des Diagnostics. » Cela rend afin que chaque fois que l’utilisateur indique que l’expression « activer/désactiver les diagnostics », il déclenche une action. Notez que vous devrez peut-être développer « élément 0 » en appuyant sur la flèche en regard de celle-ci.

![Lesson5 Chapter1 Step6im](images/Lesson5_chapter1_step6im.PNG)

7. Ajouter le « diagnostics contrôle script de démonstration » pour activer ou désactiver le diagnostic de compteur de fréquence d’images. Pour ce faire, appuyez sur le bouton « Ajouter un composant » et recherchez « script de contrôle de démonstration diagnostics », puis ajoutez-le dans le menu. Ce script peut être ajouté à n’importe quel objet, mais par souci de simplicité, nous allons l’ajouter au même objet en tant que le Gestionnaire d’entrée vocale. 

   > Remarque : ce script est uniquement inclus dans ces modules et n’est pas inclus avec le MRTK d’origine.

![Lesson5 Chapter1 Step7im](images/Lesson5_chapter1_step7im.PNG)

8. Ajouter une nouvelle réponse dans le Gestionnaire d’entrée vocale. Pour faire cela cliquez sur le bouton « + » sous intitulée « réponse () » (marqués par une flèche verte dans l’image ci-dessus).

![Lesson5 Chapter1 Step7im](images/Lesson5_chapter1_step8.PNG)

9. Faites glisser l’objet qui contient le script de contrôles de démonstration de Diagnostics pour la nouvelle réponse que vous venez de créer à l’étape 8.
    ![Lesson5 Chapter1 Step9im](images/Lesson5_chapter1_step9im.PNG)

10. Sélectionnez la liste déroulante « aucune fonction », sélectionnez les contrôles de diagnostic de démonstration de maintenant, puis « sur Activer/désactiver diagnostics (). » Cette fonction active ou désactive vos diagnostics et désactiver.  ![Lesson5 Chapter1 Step10im](images/Lesson5_chapter1_step10im.PNG)
    
> Notez qu’avant la génération sur votre appareil vous devez activer les paramètres de mic. Pour faire ce clic sur le fichier, accédez à paramètres de génération, à partir de là, les paramètres du lecteur et vérifiez que la fonctionnalité de microphone est définie.

Ensuite, nous avons ajouté la possibilité de lire un fichier audio à partir de la commande vocale à l’aide de l’objet « huit ». Nous avons vu dans [leçon 4](mrlearning-base-ch4.md), nous avons ajouté la possibilité de lire un clip audio de toucher l’objet de huit. Nous s’appuieront sur cette même source audio pour notre commande vocale de musique.

11. Sélectionnez l’objet de huit dans la hiérarchie de la scène de base.

12. Ajouter un autre gestionnaire de l’entrée vocale (Répétez les étapes 4 et 5), mais avec l’objet de huit. 

13. Au lieu d’ajouter les commandes vocales de « Activer/désactiver Diagnostics » à l’étape 6, ajoutez la commande de voix « musique », comme illustré dans l’image ci-dessous.
    
     ![Lesson5 Chapter1 Step13im](images/Lesson5_chapter1_step13im.PNG)
    
    
    
14. Comme avec les étapes 8 et 9, ajouter une nouvelle réponse et faites glisser le huit à l’emplacement vide sur la réponse.

15. Sélectionnez le menu déroulant qui n’indique « aucune fonction, « sélectionnez « Audio Source », puis sélectionnez « PlayOneShot (AudioClip). »

![Lesson5 Chapter1 Step15im](images/Lesson5_chapter1_step15im.PNG)

16. Pour le clip audio, pour cet exemple nous allons utiliser le même clip audio à partir de [leçon 4](mrlearning-base-ch4.md). Aller dans Panneau de votre projet, recherchez le clip audio « MRTK_Gem » et la faire glisser vers l’emplacement source audio, comme illustré dans l’image ci-dessous. Maintenant votre application doit être en mesure de répondre aux commandes vocales « activer/désactiver diagnostics » pour activer/désactiver le volet des compteurs taux frame et « play music » pour lire la chanson MRTK_Gem.
     ![Lesson5 Chapter1 Step16im](images/Lesson5_chapter1_step16im.PNG)


### <a name="the-pan-gesture"></a>Le mouvement panoramique 

Dans ce chapitre, nous allez apprendre à utiliser le mouvement panoramique. Il est utile pour le défilement (à l’aide de votre doigt ou la main pour faire défiler le contenu.) Vous pouvez également utiliser le mouvement panoramique faire pour pivoter des objets, pour parcourir une collection d’objets 3D, ou même défilement un 2D de l’interface utilisateur. Nous sera être apprendre à utiliser le mouvement panoramique à warp une texture. Nous explorerons également comment déplacer une collection d’objets 3D.

1. Créer un quadruple. Dans votre hiérarchie de la scène de base, avec le bouton droit, sélectionnez « objet 3D », puis sur « Quadruple. »

![Lesson5 Chapter2 Step2im](images/Lesson5_chapter2_step2im.PNG)

2. Repositionner le quadruple comme il convient. Dans notre exemple, nous définissons le x = 0, y = 0 et z = 1.5 en dehors de l’appareil photo pour une position à l’aise à partir de la version 2 HoloLens.

   > Remarque: Si les blocs quad (est infront de) n’importe quel contenu issus des leçons précédentes, n’oubliez pas de déplacer telles qu’il ne bloque pas les autres objets.

3. Appliquer un matériau à le quadruple. Ce document sera le matériel que nous sera défiler avec le mouvement panoramique. 

![Lesson5 Chapter2 Step3im](images/Lesson5_chapter2_step3im.PNG)

4. Dans votre Panneau de configuration de projets, tapez dans la zone de recherche « panoramique contenu ». Une session sur les quatre cœurs dans votre scène, faites glisser ce matériau. 

> Remarque: Le matériel de « Effectuer un panoramique de contenu » n’est pas inclus dans le MRTK, mais il est un élément multimédia dans le package de ressource de ce module, comme importé dans les leçons précédentes. 

> Remarque: Lorsque vous ajoutez le contenu de panoramique, il peut apparaître étirée. Vous pouvez résoudre ce problème en ajustant les valeurs x, y et z des valeurs de la taille de la quadruple jusqu'à ce que vous êtes satisfait de son aspect.

Pour utiliser le mouvement panoramique, vous devez un collider sur votre objet. Vous pouvez voir que le quadruple a déjà un collider de maillage. Toutefois, le collider maillage n’est pas idéal, car il est extrêmement léger et difficile à sélectionner. Nous vous suggérons en remplaçant le collider maille avec un collider de zone.

5. Cliquez avec le bouton droit sur le collider maille qui se trouve sur le quadruple (dans le panneau Inspecteur), puis supprimez-la en cliquant sur « Supprimer le composant. » 
   ![Lesson5 Chapter2 Step5im](images/Lesson5_chapter2_step5im.PNG)

6. Ajoutez maintenant le collider boîte en cliquant sur « Ajouter un composant » et la recherche de « zone collider. » La valeur par défaut ajoutée collider de zone est toujours trop léger, par conséquent, cliquez sur le bouton « Modifier collider » pour le modifier. Lorsqu’elle est activée dans, vous pouvez ajuster la taille à l’aide de x, y et z des valeurs ou les éléments dans l’éditeur de la scène. Dans notre exemple, nous voulons étendre le collider boîte un peu derrière le quadruple. Dans l’éditeur de la scène, faites glisser le collider de zone à partir de l’arrière, vers l’extérieur (voir l’image ci-dessous). Cela fera est d’autoriser l’utilisateur à utiliser non seulement son doigt, mais leur part entière pour faire défiler. 
    ![Lesson5 Chapter2 Step6im](images/Lesson5_chapter2_step6im.PNG)
7. Rendre interactive. Étant donné que nous souhaitons interagir directement avec le quadruple, nous voulons utiliser le composant « près interaction touchable » (nous avons également utilisé cela dans la leçon 4 pour la lecture de musique à partir de la huit). Cliquez sur « Ajouter un composant » et recherchez « près interaction touchable » et le sélectionner, comme indiqué dans les images ci-dessous. 

8. Ajouter la possibilité de reconnaître le mouvement panoramique. Cliquez sur « Ajouter un composant », tapez « hand panoramique de l’interaction. » Vous devez choisir entre ray main (ce qui vous permet d’effectuer un panoramique à distance) et votre index. Pour cet exemple, laissez votre index. 
    ![Lesson5 Chapter2 Step7 8Im](images/Lesson5_chapter2_step7-8im.PNG)

![Lesson5 Chapter2 Step8im](images/Lesson5_chapter2_step8im.PNG)

9. Dans le script de panoramique interaction disponible, le « verrou horizontale » et les cases à cocher « verrouillage vertical » se verrouille les mouvements, respectivement. Les paramètres de texture de type wrap rendra la texture (mappage de texture) suivre les mouvements de panoramique de l’utilisateur. Pour cet exemple, nous allons cette case à cocher. Il existe également des « velocity active » qui, si elle est désactivée, le mouvement panoramique ne fonctionne pas. Cochez cette case également. Maintenant, vous devez avoir un quadruple prenant en charge de panoramique.

   

   Ensuite, nous allez apprendre à effectuer un panoramique d’objets 3D. 

10. Cliquez avec le bouton droit sur l’objet quadruple, objet 3D puis cliquez sur « cube ». Mettre à l’échelle du cube afin qu’il soit à peu près x = 0,1, y = 0.1 et z = 0.1. Copiez ce cube 3 fois (en cliquant avec le bouton droit sur le cube en appuyant sur en double ou en appuyant sur/commande de contrôle D). Les espacer uniformément. Votre scène doit ressembler à l’image ci-dessous.

![Lesson5 Chapter2 Step10im](images/Lesson5_chapter2_step10im.PNG)







11. Sélectionnez de nouveau le quadruple, et sous la main interaction panoramique de scripts, nous souhaitons définir les actions de panoramique à chacun des cubes. Sous « récepteurs d’événements panoramique » nous voulons spécifier le nombre d’objets qui reçoivent l’événement. Dans la mesure où il n’y a 4 cubes, type « 4 » Appuyez sur ENTRÉE. 4 champs vides doivent apparaître.


![Lesson5 Chapter2 Step11im](images/Lesson5_chapter2_step11im.PNG)



12. Faites glisser chacune des cubes dans à chacun des emplacements d’élément vide.
     ![Lesson5 Chapter2 Step12im](images/Lesson5_chapter2_step12im.PNG)
    
13. Ajoutez le script de « déplacer avec panoramique » à tous les cubes. Pour ce faire, maintenez/commande de contrôle et sélectionnez chaque objet. Puis, dans ce panneau, cliquez sur « Ajouter un composant » et recherchez « déplacer avec panoramique ». Cliquez sur le script, et il sera ajouté à chaque cube. Désormais, les objets 3D déplacera avec votre mouvement panoramique ! Si vous supprimez la maille rendu sur votre quadruple, vous devez maintenant avoir un quadruple invisible, où vous pouvez effectuer un panoramique dans une liste d’objets 3D.

### <a name="eye-tracking"></a>Suivi de le œil

Dans ce chapitre, nous allons examiner comment activer le suivi des yeux dans notre démonstration. Nous tournera lentement les éléments de menu 3D lorsqu’ils sont en cours gazed avec les regards yeux lors de. Nous déclenche également un plaisir effet lors de l’élément à gazed est sélectionné.

1. Vérifiez que les profils de kit de ressources de réalité mixte sont correctement configurés. À ce jour, la configuration de profil de kit de ressources de réalité mixte n’inclut pas les yeux des capacités de suivi par défaut. Pour ajouter des fonctionnalités de suivi de le œil, suivez les instructions dans la section « Configuration de profils MRTK requis pour le suivi des yeux » comme indiqué dans le [Documentation du Kit de ressources réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#setting-up-the-mrtk-profiles-required-for-eye-tracking  ). Vérifiez que ce suivi de le œil est correctement configuré en suivant les étapes restantes dans le lien vers la documentation ci-dessus, y compris l’activation de suivi des yeux dans GazeProvider (composant attaché à la caméra) et l’activation de simulation de œil, suivi des modifications dans l’éditeur Unity. Remarque Cette version future de la MRTK peut inclure le suivi des yeux par défaut.

    Le lien ci-dessus fournit des instructions pour :

    - Création de le œil les regards fournisseur de données dans le profil MRTK
    - Activer le suivi des yeux dans le fournisseur de l’utilisation
    - Configurer pour simuler les yeux dans l’éditeur
    - Modification des fonctionnalités de la solution Visual Studio pour permettre le suivi des yeux dans l’application générée

2. Ajouter le composant de la cible de suivi à des objets cibles. Pour permettre à un objet répondre aux événements des regards yeux, nous devrons ajouter le composant EyeTrackingTarget sur chaque objet que nous souhaitons interagir à l’aide du pointage de regard yeux. Ajoutez ce composant pour chacun des neuf objets 3D qui font partie de la collection de la grille. Conseil : sélectionnez plusieurs éléments dans la hiérarchie pour le composant EyeTrackingTarget-ajouter en bloc.
    ![Étape 2 de chapitre3 Lesson5](images/Lesson5Chapter3Step2.JPG)

3. Ensuite, nous allons ajouter le script EyeTrackingTutorialDemo pour certaines interactions intéressantes. Le script EyeTrackingTutorialDemo est inclus dans le cadre du référentiel de cette série de didacticiels et n’est pas inclus par défaut avec le Kit de ressources de réalité mixte. Pour chaque objet 3D dans la collection de la grille, ajoutez le script de EyeTrackingTutorialDemo en effectuant une recherche pour le composant dans le menu « Ajouter un composant ».
   ![Étape 3 de chapitre3 Lesson5](images/Lesson5Chapter3Step3.JPG)

   4. Faire pivoter l’objet lors de la recherche au niveau de la cible. Nous souhaitons configurer notre objet 3D pour mettre en place pendant que nous nous intéressons à elle. Pour ce faire, insérez un nouveau champ dans la section « Pendant que vous recherchez à cible » du composant EyeTrackingTarget, comme indiqué dans l’image ci-dessous. 

![Lesson5 chapitre3 Step4a](images/Lesson5Chapter3Step4a.JPG)
![Lesson5 chapitre3 Step4b](images/Lesson5Chapter3Step4b.JPG)



Dans le champ nouvellement créé, ajoutez l’objet de jeu actuelle dans le champ vide, puis sélectionnez EyeTrackingTutorialDemo > RotateTarget() comme indiqué dans l’image ci-dessous. Maintenant, l’objet 3D est configuré pour faire tourner lorsqu’il est en cours gazed sur avec le suivi des yeux. 

5. Ajoutez dans la possibilité de « spot cible » est en cours gazed à fonction select (-appui en l’air ou indiquant que « select »). Similaire à l’étape 4, nous voulons déclencher EyeTrackingTutorialDemo > BlipTarget(), affectez au champ « Select() » de l’objet de jeu du composant EyeTrackingTarget, comme illustré dans la figure ci-dessous. Ceci est désormais configuré, vous remarquerez un légère spot dans l’objet de jeu chaque fois que vous déclenchez une action « sélectionner », tels que-appui en l’air ou les commandes vocales « sélectionner ». 
    ![Étape 5 de chapitre3 Lesson5](images/Lesson5Chapter3Step5.JPG)
6. Vérifier les fonctions de suivi yeux sont correctement configurées avant la génération 2 de HoloLens. À ce jour, Unity n’a pas encore la possibilité de définir la capacité d’entrée (pour le suivi de le œil) du pointage de regard. Définition de cette fonctionnalité est requise pour le suivi d’oeil travailler sur le 2 HoloLens. Suivez ces instructions sur la documentation du Kit de ressources réalité mixte pour activer la fonctionnalité d’entrée du pointage de regard : https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2 


### <a name="congratulations"></a>Félicitations ! 
Vous avez ajouté avec succès les yeux de base des fonctions de suivi à l’application. Ces actions sont uniquement le début d’un monde de possibilités avec suivi de le œil. Ce chapitre conclut également la leçon 5, où nous avons découvert des fonctionnalités avancées d’entrée tels que des commandes vocales, panoramique mouvements et suivi des yeux. 

[Leçon suivante : Module de lunaire Assembly exemple expérience](mrlearning-base-ch6.md)

