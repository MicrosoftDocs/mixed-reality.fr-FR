---
title: Didacticiels de mise en route-6. Exploration des options d’entrée avancées
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: bb6aa620cebfda74b0b6b5f6ca04e1eeb68d9c7b
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438458"
---
# <a name="6-exploring-advanced-input-options"></a>6. exploration des options d’entrée avancées

Dans ce didacticiel, plusieurs options d’entrée avancées pour HoloLens 2 sont explorées, notamment l’utilisation de commandes vocales, le mouvement panoramique et le suivi des yeux. 

## <a name="objectives"></a>Objectifs

- Déclencher des événements à l’aide de commandes et de mots clés vocaux
- Utilisez des mains suivies pour faire pivoter des textures et des objets 3D avec des mains suivies
- Tirez parti des fonctionnalités de suivi oculaire HoloLens 2 pour sélectionner des objets

## <a name="instructions"></a>Instructions

### <a name="enabling-voice-commands"></a>Activation des commandes vocales

Dans cette section, deux commandes vocales sont implémentées. Tout d’abord, la possibilité de basculer vers le panneau Diagnostics de la fréquence d’images est introduite en disant « activer/désactiver les Diagnostics ». Deuxièmement, la possibilité de lire un son avec une commande vocale est explorée. Les profils et paramètres MRTK responsables de la configuration des commandes vocales sont examinés en premier. 

1. Dans la hiérarchie de la scène de base, sélectionnez MixedRealityToolkit. Dans le volet de l’inspecteur, faites défiler l’écran jusqu’à paramètres système d’entrée. Double-cliquez pour ouvrir le profil de système d’entrée. Clonez le profil de système d’entrée pour le rendre modifiable comme nous l’avons appris dans la [leçon 1](mrlearning-base-ch1.md) 

Dans le profil de système d’entrée, il existe un grand nombre de paramètres. Pour les commandes vocales, sélectionnez Paramètres de commande vocale. 

![Lesson5 Chapter1 Step2im](images/Lesson5_Chapter1_step2im.PNG)

2. Clonez le profil des commandes vocales pour le rendre modifiable comme nous l’avons appris dans la [leçon 1](mrlearning-base-ch1.md). Double-cliquez sur le profil de commande vocale dans lequel vous remarquerez une plage de paramètres. Pour obtenir une description complète de ces paramètres, reportez-vous à la [documentation MRTK Speech](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Speech.html>). 

>Remarque : par défaut, le comportement général est démarrage automatique. Vous pouvez le remplacer par Manual-Start, si vous le souhaitez. Toutefois, pour cet exemple, conservez-le au démarrage automatique. Le MRTK est fourni avec plusieurs commandes vocales par défaut, telles que menu, activer/désactiver les diagnostics et basculer le profileur. Nous allons utiliser le mot clé « activer/désactiver les diagnostics » afin d’activer et de désactiver le compteur de trames de fréquence des Diagnostics. Nous allons également ajouter une nouvelle commande vocale lors des étapes ci-dessous.
>
> ![Lesson5 Chapter1 Noteim](images/Lesson5_chapter1_noteim.PNG)

3. Ajoutez une nouvelle commande vocale. Pour ce faire, cliquez sur le bouton + Ajouter une nouvelle commande vocale. Vous verrez une nouvelle ligne qui apparaît sous la liste des commandes vocales existantes. Tapez la commande vocale que vous souhaitez utiliser. Dans cet exemple, utilisez la commande « lire la musique ».

>Conseil : vous pouvez également définir un code de commande pour les commandes vocales. Cela permet aux commandes vocales de déclencher des événements à l’appui d’une touche du clavier.    

4. Ajoutez la capacité à répondre aux commandes vocales. Sélectionnez un objet dans la hiérarchie de scènes de base à laquelle aucun autre script d’entrée n’est attaché (par exemple, aucun gestionnaire de manipulation). Dans le panneau Inspecteur, cliquez sur Ajouter un composant. Tapez « gestionnaire d’entrée vocale » et sélectionnez-le.

   ![Lesson5 fichier chapter1 Step4im](images/Lesson5_chapter1_step4im.PNG)

   

Par défaut, deux cases à cocher s’affichent. L’une est la case à cocher est le focus requis. Ainsi, tant que vous pointez au niveau de l’objet avec un anneau de rayon, le point de regard, le point de regard, ou la main, la commande vocale est déclenchée. Désactivez cette case à cocher pour que l’utilisateur n’ait pas besoin d’examiner l’objet pour utiliser la commande vocale.

5. Ajoutez la capacité à répondre à une commande vocale. Pour ce faire, cliquez sur le bouton + situé dans le gestionnaire d’entrée vocal et sélectionnez le mot clé auquel vous souhaitez répondre.

   > Remarque : ces mots clés sont remplis, en fonction du profil que vous avez modifié à l’étape précédente.

![Lesson5 Chapter1 Step5im](images/Lesson5_chapter1_step5im.PNG)

6. En regard de mot clé, vous verrez un menu déroulant. Sélectionnez Activer/désactiver les diagnostics afin que chaque fois que l’utilisateur indique l’expression « activer/désactiver les Diagnostics », il déclenche une action. Notez que vous devrez peut-être développer l’élément 0 en appuyant sur la flèche en regard de celui-ci.

![Lesson5 Chapter1 Step6im](images/Lesson5_chapter1_step6im.PNG)

7. Ajoutez le script de contrôle de démonstration des diagnostics pour activer ou désactiver le diagnostic des compteurs de fréquence d’images. Pour ce faire, appuyez sur Ajouter un composant, recherchez le script des contrôles de démonstration des diagnostics et ajoutez-le à partir du menu. Ce script peut être ajouté à n’importe quel objet. Toutefois, pour plus de simplicité, nous l’ajouterons au même objet que le gestionnaire d’entrée vocal. 

   > Remarque : ce script est inclus uniquement avec ces modules, mais pas avec le MRTK d’origine.

![Lesson5 Chapter1 Step7im](images/Lesson5_chapter1_step7im.PNG)

8. Ajoutez une nouvelle réponse dans le gestionnaire d’entrée vocal. Pour ce faire, cliquez sur le bouton « + » en dessous de l’emplacement où il indique la réponse () (marquée par une flèche verte dans l’image ci-dessus).

![Lesson5 Chapter1 Step7im](images/Lesson5_chapter1_step8.PNG)

9. Faites glisser l’objet qui contient le script des contrôles de démonstration de diagnostic vers la nouvelle réponse que vous venez de créer à l’étape 8.
    ![Lesson5 Chapter1 Step9im](images/Lesson5_chapter1_step9im.PNG)

10. Sélectionnez la liste déroulante « aucune fonction », puis le contrôle de démonstration de diagnostic. Sélectionnez ensuite la fonction « activer/désactiver les Diagnostics () », qui active ou désactive les Diagnostics.  ![Lesson5 Chapter1 Step10im](images/Lesson5_chapter1_step10im.PNG)
    
> Notez qu’avant de créer sur votre appareil, vous devez activer les paramètres MIC. Pour ce faire, cliquez sur fichier et accédez à paramètres de build, paramètres du lecteur, puis vérifiez que la fonctionnalité microphone est définie.

Ensuite, ajoutez la possibilité de lire un fichier audio à partir d’une commande vocale à l’aide de l’objet octa. Rappelez-vous à la [leçon 4](mrlearning-base-ch4.md) que la possibilité de lire un clip audio à partir de l’objet octa a été ajoutée. Nous allons utiliser cette même source audio pour notre commande vocale de musique.

11. Sélectionnez l’objet octa dans la hiérarchie de la scène de base.

12. Ajoutez un autre gestionnaire d’entrée vocale (répétez les étapes 4 et 5), mais avec l’objet octa. 

13. Au lieu d’ajouter la commande Activer/désactiver les diagnostics vocaux de l’étape 6, ajoutez la commande lire la musique musicale comme indiqué dans l’image ci-dessous.
    
     ![Lesson5 Chapter1 Step13im](images/Lesson5_chapter1_step13im.PNG)
    
    
    
14. Comme pour les étapes 8 et 9, ajoutez une nouvelle réponse et faites glisser l’objet octa dans l’emplacement de réponse vide.

15. Sélectionnez le menu déroulant qui n’indique aucune fonction. Sélectionnez ensuite source audio, suivi de PlayOneShot (AudioClip).

![Lesson5 Chapter1 Step15im](images/Lesson5_chapter1_step15im.PNG)

16. Pour cet exemple, nous allons utiliser le même clip audio de la [leçon 4](mrlearning-base-ch4.md). Accédez au panneau projet, recherchez le clip audio « MRTK_Gem » et faites-le glisser dans l’emplacement source audio, comme indiqué dans l’image ci-dessous. À présent, votre application répond aux commandes vocales « activer/désactiver les diagnostics » pour basculer vers le panneau compteur de fréquence d’images et lire la musique pour lire la chanson MRTK_Gem.
     ![Lesson5 Chapter1 Step16im](images/Lesson5_chapter1_step16im.PNG)


### <a name="the-pan-gesture"></a>Le mouvement panoramique 

Dans cette section, vous allez apprendre à utiliser le mouvement panoramique. Cela est utile pour faire défiler le contenu à l’aide de votre doigt ou main. Vous pouvez également utiliser le mouvement panoramique pour faire pivoter des objets, parcourir une collection d’objets 3D ou même faire défiler une interface utilisateur 2D. Nous apprendrons également comment utiliser le mouvement panoramique pour déformer une texture et comment déplacer une collection d’objets 3D.

1. Créez un quad. Dans votre hiérarchie de scènes de base, cliquez avec le bouton droit sur, puis sélectionnez « objet 3D » suivi de quadruple.

![Lesson5 Chapter2 Step2im](images/Lesson5_chapter2_step2im.PNG)

2. Repositionnez le quad, le cas échéant. Pour notre exemple, nous définissons x = 0, y = 0 et z = 1,5 en dehors de l’appareil photo pour une position confortable de HoloLens 2.

   > Remarque : si les Quad blocks ou est devant le contenu des leçons précédentes, veillez à le déplacer afin qu’il ne bloque pas les autres objets.

3. Appliquez un matériau au quad. Ce document sera ce que nous allons faire défiler avec le mouvement panoramique. 

![Lesson5 Chapter2 Step3im](images/Lesson5_chapter2_step3im.PNG)

4. Dans le panneau projets, tapez « panoramique du contenu » dans la zone de recherche. Faites glisser ce matériau sur le quadruple dans votre scène. 

> Remarque : le matériel de contenu panoramique n’est pas inclus dans le MRTK, mais une ressource dans le package de ressources de ce module, telle qu’elle a été importée dans les leçons précédentes. 

> Remarque : lorsque vous ajoutez le contenu panoramique, il peut sembler étiré. Vous pouvez résoudre ce problème en ajustant les valeurs x, y et z de la taille du quad jusqu’à être satisfait de son aspect.

Pour utiliser le mouvement panoramique, vous avez besoin d’un collider sur votre objet. Vous constaterez que le quad a déjà un mesh collider. Toutefois, celui-ci n’est pas idéal, car il est extrêmement fin et difficile à sélectionner. Nous vous suggérons de le remplacer par un box collider.

5. Cliquez avec le bouton droit sur le conflit de maille situé sur le quadruple à partir du panneau de l’inspecteur. Ensuite, supprimez-le en cliquant sur supprimer le composant.
    ![Lesson5 Chapter2 Step5im](images/Lesson5_chapter2_step5im.PNG)
6. À présent, ajoutez le conflit Box en cliquant sur Ajouter un composant et en recherchant « zone de conflit ». Le conflit de zone ajouté par défaut est toujours trop léger. par conséquent, cliquez sur le bouton modifier le conflit pour le modifier. Vous pouvez ajuster la taille à l’aide des valeurs x, y et z ou des éléments dans l’éditeur de scène. Dans notre exemple, nous voulons étendre un peu le box collider derrière le quad. Dans l’éditeur de scène, faites glisser le box collider de l’arrière vers l’extérieur (voir l’image ci-dessous). Cela permet à l’utilisateur de ne pas utiliser son doigt, mais de faire défiler son intégralité. 
    ![Lesson5 Chapter2 Step6im](images/Lesson5_chapter2_step6im.PNG)
7. Rendez-le interactif. Étant donné que nous voulons interagir directement avec le quad, nous voulons utiliser le composant touchable near-interaction que nous avons utilisé dans la leçon 4 pour écouter de la musique à partir de l’objet octa. Cliquez sur Ajouter un composant, recherchez « near interaction touchable » et sélectionnez-le comme indiqué dans les images ci-dessous. 

8. Ajoutez la capacité à reconnaître le mouvement panoramique. Cliquez sur Ajouter un composant et tapez « main interaction Pan ». Vous aurez le choix entre « hand ray » (qui vous permet de faire un panoramique à distance) et « index finger ». Pour cet exemple, conservez « index finger ». 
    ![Lesson5 Chapter2 Step7 8Im](images/Lesson5_chapter2_step7-8im.PNG)

![Lesson5 Chapter2 Step8im](images/Lesson5_chapter2_step8im.PNG)

9. Dans le script de panoramique d’interaction main, les cases à cocher verrouiller horizontalement et verrouiller verticale verrouillent les mouvements, respectivement. Les paramètres de texture de retour à la ligne rendent la texture (mappage de texture) suivre les mouvements de panoramique de l’utilisateur. Pour cet exemple, vous allez activer cette case à cocher. Il y a également une vitesse active, qui, si elle est désactivée, le mouvement panoramique ne fonctionnera pas. Cochez aussi cette case. À présent, vous disposez d’un quadruple.

   

   Voyons maintenant comment faire un panoramique d’objets 3D. 

10. Cliquez avec le bouton droit sur l’objet Quad, sélectionnez objet 3D, puis cliquez sur cube. Mettez le cube à l’échelle avec des valeurs d’environ x = 0,1, y = 0,1 et z = 0,1. Copiez ce cube trois fois en cliquant avec le bouton droit sur le cube et en appuyant sur dupliquer, ou en appuyant sur Ctrl/Commande D. espacer uniformément. Votre scène doit ressembler à l’image ci-dessous.

![Lesson5 Chapter2 Step10im](images/Lesson5_chapter2_step10im.PNG)







11. Sélectionnez à nouveau le quad et, sous le script de panoramique d’interaction main, définissez les actions panoramiques sur chacun des cubes. Sous les récepteurs d’événements panoramiques, nous souhaitons spécifier le nombre d’objets recevant l’événement. Étant donné qu’il y a quatre cubes, tapez « 4 » et appuyez sur entrée. Quatre champs vides doivent apparaître.


![Lesson5 Chapter2 Step11im](images/Lesson5_chapter2_step11im.PNG)



12. Faites glisser chacun des cubes dans chacun des emplacements d’éléments vides.
     ![Lesson5 Chapter2 Step12im](images/Lesson5_chapter2_step12im.PNG)
    
13. Ajoutez le script Move with Pan à tous les cubes en appuyant sur et en maintenant le contrôle/la commande, puis sélectionnez chaque objet. Dans le panneau de l’inspecteur, cliquez sur Ajouter un composant et recherchez « déplacer avec un panoramique ». Cliquez sur le script et il est ajouté à chaque cube. Maintenant, les objets 3D sont déplacés avec votre mouvement de panoramique. Si vous supprimez le maillage sur votre quad, vous devriez maintenant avoir un quad invisible où vous pouvez faire un panoramique dans une liste d’objets 3D.

### <a name="eye-tracking"></a>Eye-tracking

Dans cette section, nous allons découvrir comment activer le suivi visuel dans notre démonstration. Nous allons faire tourner lentement nos éléments de menu 3D lorsqu’ils sont en regard avec votre point de regard. Nous déclencherons également un effet attrayant quand l’élément regardé est sélectionné.

1. Vérifiez que les profils MRTK sont correctement configurés. À ce jour, la configuration de profil Mixed Reality Toolkit n’inclut pas de fonctionnalités d’eye-tracking par défaut. Pour ajouter des fonctionnalités de suivi oculaire, suivez les instructions de la section « Configuration des profils MRTK requis pour le suivi oculaire », comme indiqué dans la documentation relative à la mise en place de la [réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#setting-up-the-mrtk-profiles-required-for-eye-tracking  ). Assurez-vous que le suivi oculaire est correctement configuré en suivant les étapes restantes dans le lien de la documentation ci-dessus, y compris l’activation du suivi oculaire dans GazeProvider (le composant attaché à l’appareil photo) et l’activation de la simulation du suivi oculaire dans l’éditeur Unity. Notez que les futures versions du MRTK peuvent inclure le suivi oculaire par défaut.

    Le lien ci-dessus fournit de brèves instructions pour les tâches suivantes :

    - Création de la Fournisseur de données de regard de l’œil pour une utilisation dans le profil MRTK
    - Activation de l’eye-tracking dans le Gaze Provider
    - Configuration d’une simulation de suivi oculaire dans l’éditeur
    - Modification des fonctionnalités de la solution Visual Studio pour permettre l’eye-tracking dans l’application générée

2. Ajoutez le composant Eye Tracking Target aux objets cibles. Pour permettre à un objet de répondre aux événements de point de vue oculaire, nous devons ajouter le composant EyeTrackingTarget sur chaque objet avec lequel nous souhaitons interagir à l’aide de l’œil. Ajoutez ce composant à chacun des neuf objets 3D qui font partie de la collection de la grille. Conseil : sélectionnez plusieurs éléments dans la hiérarchie pour ajouter en bloc le composant EyeTrackingTarget.
    ![Lesson5 Chapter3 Step2](images/Lesson5Chapter3Step2.JPG)

3. Nous allons ensuite ajouter le script EyeTrackingTutorialDemo pour des interactions passionnantes. Le script EyeTrackingTutorialDemo est inclus dans le référentiel de cette série de didacticiels. Elle n’est pas incluse par défaut dans la boîte à outils de la réalité mixte. Pour chaque objet 3D de la collection Grid, ajoutez le script EyeTrackingTutorialDemo en recherchant le composant dans le menu Ajouter un composant.
   ![Lesson5 Chapter3 Step3](images/Lesson5Chapter3Step3.JPG)

4. Faites pivoter l’objet tout en observant la cible. Nous voulons configurer notre objet 3D pour qu’il tourne pendant que nous le regardons. Pour ce faire, insérez un nouveau champ dans la section en regardant la cible () du composant EyeTrackingTarget, comme indiqué dans l’image ci-dessous. 

![Lesson5 Chapter3 Step4a](images/Lesson5Chapter3Step4a.JPG)
![Lesson5 Chapter3 Step4b](images/Lesson5Chapter3Step4b.JPG)



Dans le champ nouvellement créé, ajoutez l’objet de jeu actuel au champ vide, puis sélectionnez EyeTrackingTutorialDemo > RotateTarget (), comme indiqué dans l’image ci-dessous. L’objet 3D est maintenant configuré pour pivoter quand il est le focus de l’eye tracking. 

5. Ajoutez la possibilité de « spot cible » qui fait l’objet d’un regard sur Select by air ou en disant « Select » (sélectionner). Comme dans l’étape 4, nous voulons déclencher EyeTrackingTutorialDemo > BlipTarget () en l’affectant au champ Select () de l’objet Game du composant EyeTrackingTarget, comme illustré dans la figure ci-dessous. Une fois cette configuration effectuée, vous remarquerez un léger spot dans l’objet de jeu chaque fois que vous déclenchez une action Select, telle qu’un TAP-Air ou la commande vocale « Select ». 
    ![Lesson5 Chapter3 Step5](images/Lesson5Chapter3Step5.JPG)
6. Vérifiez que les fonctionnalités d’eye-tracking sont configurées correctement avant la génération dans HoloLens 2. Au moment de la rédaction de cet article, Unity n’a pas encore la possibilité de définir l’entrée de regard pour les fonctionnalités de suivi oculaire. La définition de cette fonctionnalité est nécessaire pour que le suivi oculaire fonctionne dans HoloLens 2. Suivez ces instructions fournies dans la documentation de Mixed Reality Toolkit pour activer la fonctionnalité d’entrée de pointage du regard : https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2 


## <a name="congratulations"></a>Félicitations !

Vous avez ajouté avec succès des fonctionnalités de suivi des yeux de base à votre application. Ces premiers pas vous ouvrent la voie vers tout un monde de possibilités avec l’eye-tracking. Ce chapitre conclut également la leçon 5, où nous avons appris les fonctionnalités d’entrée avancées, telles que les commandes vocales, les gestes panoramiques et le suivi oculaire. 

[Leçon suivante : 7. création d’un exemple d’application de module lunaire](mrlearning-base-ch6.md)

