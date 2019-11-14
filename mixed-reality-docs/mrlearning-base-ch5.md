---
title: Didacticiels de mise en route-6. Exploration des options d’entrée avancées
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: b740c463e3d73d5df9b996562e9ff0a1952703f0
ms.sourcegitcommit: f2b7c6381006fab6d0472fcaa680ff7fb79954d6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/14/2019
ms.locfileid: "74064324"
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

1. Dans la hiérarchie BaseScene, sélectionnez MixedRealityToolkit. Ensuite, dans le panneau de l’inspecteur, sélectionnez entrée, puis cliquez sur le petit bouton cloner à gauche de l’DefaultMixedRealityInputSystemProfile pour ouvrir la fenêtre contextuelle cloner le profil. Dans le menu contextuel, cliquez sur Cloner pour créer un nouveau profil MixedRealityInputSystemProfile.

    ![mrlearning-base-CH5-1-step1a. png](images/mrlearning-base-ch5-1-step1a.png)

    Cela entraîne également le remplissage automatique du MixedRealityToolkitConfigurationProfile avec le MixedRealityInputSystemProfile nouvellement créé.

    ![mrlearning-base-CH5-1-step1b. png](images/mrlearning-base-ch5-1-step1b.png)

2. Dans le profil de système d’entrée, il existe un grand nombre de paramètres. Pour les commandes vocales, développez la section Speech et suivez le même processus que dans l’étape précédente pour cloner le DefaultMixedRealitySpeechCommandsProfile et le remplacer par votre propre copie modifiable.

    ![mrlearning-base-CH5-1-Step2. png](images/mrlearning-base-ch5-1-step2.png)

    Dans le profil de commande de reconnaissance vocale, vous remarquerez une plage de paramètres. Pour obtenir une description complète de ces paramètres, reportez-vous à la [documentation MRTK Speech](<https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Speech.html>).

    Par défaut, le comportement général est le démarrage automatique. Vous pouvez le remplacer par Manual-Start, si vous le souhaitez. Toutefois, pour cet exemple, conservez-le au démarrage automatique. Le MRTK est fourni avec plusieurs commandes vocales par défaut, telles que menu, activer/désactiver les diagnostics et basculer le profileur. Nous allons utiliser le mot clé « activer/désactiver les diagnostics » afin d’activer et de désactiver le compteur de trames de fréquence des Diagnostics. Nous allons également ajouter une nouvelle commande vocale lors des étapes ci-dessous.

3. Ajoutez une nouvelle commande vocale. Pour ce faire, cliquez sur le bouton + Ajouter une nouvelle commande vocale. Vous verrez une nouvelle ligne qui apparaît sous la liste des commandes vocales existantes. Tapez la commande vocale que vous souhaitez utiliser. Dans cet exemple, utilisez la commande « lire la musique ».

    ![mrlearning-base-CH5-1-step3. png](images/mrlearning-base-ch5-1-step3.png)

    >[!NOTE]
    >Vous pouvez également définir un code de touche pour les commandes vocales. Cela permet aux commandes vocales de déclencher des événements à l’appui d’une touche du clavier.

4. Ajoutez la capacité à répondre aux commandes vocales. Sélectionnez un objet dans la hiérarchie BaseScene auquel aucun autre script d’entrée n’est associé, par exemple, l’objet de jeu MixedRealityPlayspace. Dans le panneau Inspecteur, cliquez sur Ajouter un composant, recherchez « parole », puis sélectionnez le script du gestionnaire d’entrée vocale.

    ![mrlearning-base-CH5-1-step4. png](images/mrlearning-base-ch5-1-step4.png)

    Par défaut, deux cases à cocher s’affichent. L’une est la case à cocher est le focus requis. Ainsi, tant que vous pointez au niveau de l’objet avec un anneau de rayon, le point de regard, le point de regard, ou la main, la commande vocale est déclenchée. Désactivez cette case à cocher pour que l’utilisateur n’ait pas besoin d’examiner l’objet pour utiliser la commande vocale.

5. Ajoutez la capacité à répondre à une commande vocale. Pour ce faire, cliquez sur le bouton + situé dans le gestionnaire d’entrée vocal.

    ![mrlearning-base-CH5-1-step5. png](images/mrlearning-base-ch5-1-step5.png)

6. En regard de mot clé, vous verrez un menu déroulant. Sélectionnez Activer/désactiver les diagnostics afin que chaque fois que l’utilisateur indique l’expression « activer/désactiver les Diagnostics », il déclenche une action. Notez que vous devrez peut-être développer l’élément 0 en appuyant sur la flèche en regard de celui-ci.

    ![mrlearning-base-CH5-1-step6. png](images/mrlearning-base-ch5-1-step6.png)

    >[!NOTE]
    >Ces mots clés sont remplis, en fonction du profil que vous avez modifié à l’étape 3.

7. Ajoutez le script des contrôles vocaux du système de diagnostic pour activer ou désactiver le diagnostic des compteurs de fréquence d’images. Pour ce faire, appuyez sur Ajouter un composant, recherchez le script des contrôles vocaux du système de diagnostics et ajoutez-le à partir du menu. Ce script peut être ajouté à n’importe quel objet, mais par souci de simplicité nous allons l’ajouter au même objet que le gestionnaire d’entrée vocale.

    ![mrlearning-base-CH5-1-step7. png](images/mrlearning-base-ch5-1-step7.png)

8. Ajoutez une nouvelle réponse dans le gestionnaire d’entrée vocal. Pour ce faire, cliquez sur l’icône « + » pour ajouter une nouvelle réponse à la liste des réponses.

    ![mrlearning-base-CH5-1-step8. png](images/mrlearning-base-ch5-1-step8.png)

9. Faites glisser l’objet qui contient le script des contrôles vocaux du système de diagnostic vers la nouvelle réponse que vous venez de créer à l’étape précédente.

    ![mrlearning-base-CH5-1-step9. png](images/mrlearning-base-ch5-1-step9.png)

10. Cliquez sur la liste déroulante fonction (dans laquelle aucune fonction n’est indiquée), puis sur contrôles vocaux du système de diagnostics et sélectionnez la fonction ToggleDiagnostics () qui active ou désactive les Diagnostics.

    ![mrlearning-base-CH5-1-step10. png](images/mrlearning-base-ch5-1-step10.png)

    >[!IMPORTANT]
    > Avant de créer sur votre appareil, vous devez activer les paramètres MIC. Pour ce faire, cliquez sur fichier et accédez à paramètres de build, paramètres du lecteur, puis vérifiez que la fonctionnalité microphone est définie.

    Ensuite, ajoutez la possibilité de lire un fichier audio à partir d’une commande vocale à l’aide de l’objet octa. Rappelez-vous à la [leçon 4](mrlearning-base-ch4.md) que la possibilité de lire un clip audio à partir de l’objet octa a été ajoutée. Nous allons utiliser cette même source audio pour notre commande vocale de musique.

11. Sélectionnez l’objet octa dans la hiérarchie BaseScene.

12. Ajoutez un autre gestionnaire d’entrée vocale (répétez les étapes 4 et 5), mais avec l’objet octa.

13. Au lieu d’ajouter la commande Activer/désactiver les diagnostics vocaux de l’étape 6, ajoutez la commande lire la musique musicale comme indiqué dans l’image ci-dessous.

    ![mrlearning-base-CH5-1-step13. png](images/mrlearning-base-ch5-1-step13.png)

14. Comme pour les étapes 8 et 9, ajoutez une nouvelle réponse et faites glisser l’objet octa, l’objet qui contient le script des contrôles vocaux du système de diagnostics, vers l’emplacement de réponse vide.

15. Sélectionnez le menu déroulant qui n’indique aucune fonction. Sélectionnez ensuite source audio, suivi de PlayOneShot (AudioClip).

    ![Lesson5 Chapter1 Step15im](images/Lesson5_chapter1_step15im.PNG)

16. Pour cet exemple, nous allons utiliser le même clip audio de la [leçon 4](mrlearning-base-ch4.md). Accédez au panneau projet, recherchez le clip audio « MRTK_Gem » et faites-le glisser dans l’emplacement source audio, comme indiqué dans l’image ci-dessous. À présent, votre application répond aux commandes vocales « activer/désactiver les diagnostics » pour basculer vers le panneau compteur de fréquence d’images et lire la musique pour lire la chanson MRTK_Gem.

    ![Lesson5 fichier chapter1 Step16im](images/Lesson5_chapter1_step16im.PNG)

### <a name="the-pan-gesture"></a>Le mouvement panoramique

Dans cette section, vous allez apprendre à utiliser le mouvement panoramique. Cela est utile pour faire défiler le contenu à l’aide de votre doigt ou main. Vous pouvez également utiliser le mouvement panoramique pour faire pivoter des objets, parcourir une collection d’objets 3D ou même faire défiler une interface utilisateur 2D.

1. Créez un quad. Dans votre hiérarchie BaseScene, cliquez avec le bouton droit sur, puis sélectionnez « objet 3D » suivi de quadruple.

    ![Lesson5 Chapter2 Step2im](images/Lesson5_chapter2_step2im.PNG)

2. Repositionnez le quad, le cas échéant. Pour notre exemple, nous définissons x = 0, y = 0 et z = 1,5 en dehors de l’appareil photo pour une position confortable de HoloLens 2.

    >[!NOTE]
    >Si les Quad blocks ou est devant le contenu des leçons précédentes, veillez à le déplacer afin qu’il ne bloque pas les autres objets.

3. Appliquez un matériau au quad. Ce document sera ce que nous allons faire défiler avec le mouvement panoramique.

    ![Lesson5 Chapter2 Step3im](images/Lesson5_chapter2_step3im.PNG)

4. Dans le panneau projets, tapez « panoramique du contenu » dans la zone de recherche. Faites glisser ce matériau sur le quadruple dans votre scène.

    >[!NOTE]
    >Le matériel PanContent ne fait pas partie de MRTK, mais il est inclus avec la ressource BaseModuleAssets importée dans la leçon précédente.

    Pour utiliser le mouvement panoramique, vous avez besoin d’un collider sur votre objet. Vous constaterez que le quad a déjà un mesh collider. Toutefois, celui-ci n’est pas idéal, car il est extrêmement fin et difficile à sélectionner. Nous vous suggérons de le remplacer par un box collider.

5. Cliquez avec le bouton droit sur le conflit de maille situé sur le quadruple à partir du panneau de l’inspecteur. Ensuite, supprimez-le en cliquant sur supprimer le composant.

    ![Lesson5 Chapter2 Step5im](images/Lesson5_chapter2_step5im.PNG)

6. À présent, ajoutez le conflit Box en cliquant sur Ajouter un composant et en recherchant « zone de conflit ». Le conflit de zone ajouté par défaut est toujours trop léger. par conséquent, cliquez sur le bouton modifier le conflit pour le modifier. Vous pouvez ajuster la taille à l’aide des valeurs x, y et z ou des éléments dans l’éditeur de scène. Dans notre exemple, nous voulons étendre un peu le box collider derrière le quad. Dans l’éditeur de scène, faites glisser le box collider de l’arrière vers l’extérieur (voir l’image ci-dessous). Cela permet à l’utilisateur de ne pas utiliser son doigt, mais de faire défiler son intégralité.

    ![Lesson5 Chapter2 Step6im](images/Lesson5_chapter2_step6im.PNG)

7. Rendez-le interactif. Étant donné que nous voulons interagir directement avec le quad, nous voulons utiliser le composant touchable near-interaction que nous avons utilisé dans la leçon 4 pour écouter de la musique à partir de l’objet octa. Cliquez sur Ajouter un composant, recherchez « near interaction touchable » et sélectionnez-le comme indiqué dans les images ci-dessous.

    ![mrlearning-base-CH5-2-step7a. png](images/mrlearning-base-ch5-2-step7a.png)

    Si vous voyez un avertissement jaune sur les limites et/ou le centre ne correspondant pas à la taille et/ou au centre du BoxCollider, cliquez sur les boutons corriger les limites et/ou centre de correction pour mettre à jour les valeurs de centre et de limites.

    ![mrlearning-base-CH5-2-step7b. png](images/mrlearning-base-ch5-2-step7b.png)

8. Ajoutez la capacité à reconnaître le mouvement panoramique. Cliquez sur Ajouter un composant, tapez « interaction manuelle » dans le champ de recherche et ajoutez le composant de script main interaction Pan Zoom.

    ![mrlearning-base-CH5-2-step8a. png](images/mrlearning-base-ch5-2-step8a.png)

    Et avec cela, vous disposez d’un quadruple cœur.

    Comme vous pouvez le voir, le composant de script de zoom pan d’interaction manuelle a plusieurs paramètres, comme un exercice facultatif, n’hésitez pas à les utiliser.

    ![mrlearning-base-CH5-2-step8b. png](images/mrlearning-base-ch5-2-step8b.png)

9. Voyons maintenant comment faire un panoramique d’objets 3D.

    Dans la hiérarchie, cliquez avec le bouton droit sur l’objet Quad, pour ouvrir le menu contextuel contextuel, puis sélectionnez **objet 3d** > **cube** pour ajouter un cube à votre scène.

    Assurez-vous que la **position** du cube est définie sur _0, 0,_ et qu’elle est positionnée correctement dans le quadruple. Augmentez la taille du cube jusqu’à une **échelle** de _0,1, 0,1, 0,1_.

    ![mrlearning-base-CH5-2-step9. png](images/mrlearning-base-ch5-2-step9.png)

    Dupliquez le cube trois fois en cliquant avec le bouton droit sur le cube pour ouvrir le menu contextuel contextuel, puis en sélectionnant **dupliquer**.

    Espacer uniformément les cubes. Votre scène doit ressembler à l’image ci-dessous.

10. Ajoutez le script MoveWithPan à tous les cubes en maintenant la touche CTRL enfoncée tout en sélectionnant chaque objet de **cube** dans le volet de la hiérarchie. Dans le panneau Inspecteur, cliquez sur Ajouter un composant, puis recherchez et sélectionnez le script **Move with Pan** pour l’ajouter à tous les cubes.

    ![mrlearning-base-CH5-2-step10a. png](images/mrlearning-base-ch5-2-step10a.png)

    >[!NOTE]
    >Le script MoveWithPan ne fait pas partie de MRTK, mais il est inclus avec la ressource BaseModuleAssets importée dans la leçon précédente.

    Avec les cubes toujours sélectionnés, faites glisser l’objet **quadruple** à partir du volet hiérarchie vers le champ **source d’entrée panoramique** du composant de script **Move with Pan** .

    ![mrlearning-base-CH5-2-step10b. png](images/mrlearning-base-ch5-2-step10b.png)

    À présent, les cubes se déplacent avec votre mouvement de panoramique.

    >[!TIP]
    >L’instance MoveWithPan sur chaque cube écoute l’événement PanUpdated envoyé à partir de l’instance HandInteractionPanZoom sur l’objet quadruple, que nous avons ajouté au champ source d’entrée de panoramique sur chacun des cubes, et met à jour la position de l’objet cube respectif en conséquence.

    Quand les cubes sont toujours sélectionnés, déplacez-les vers l’avant le long de leur axe Z afin que la maille de chaque cube se trouve à l’intérieur de la **boîte de collision** de la case **Quad**, en remplaçant les valeurs Z de la **position Z** par _0,7_.

    ![mrlearning-base-CH5-2-step10c. png](images/mrlearning-base-ch5-2-step10c.png)

    Maintenant, si vous désactivez le composant de **convertisseur de maillage** **Quad**en le désactivant dans le panneau Inspecteur, vous aurez un quadruple invisible où vous pouvez parcourir une liste d’objets 3D.

    ![mrlearning-base-CH5-2-step10d. png](images/mrlearning-base-ch5-2-step10d.png)

### <a name="eye-tracking"></a>Eye-tracking

Dans cette section, nous allons découvrir comment activer le suivi visuel dans notre démonstration. Nous allons faire tourner lentement nos éléments de menu 3D lorsqu’ils sont en regard avec votre point de regard. Nous déclencherons également un effet attrayant quand l’élément regardé est sélectionné.

1. Vérifiez que les profils MRTK sont correctement configurés pour le suivi oculaire. Pour ce faire, accédez au Guide de prise en main du [suivi oculaire dans MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html) et vérifiez que le suivi oculaire est correctement configuré en examinant les étapes de la section Configuration de l’outil de [suivi des yeux](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#setting-up-eye-tracking-step-by-step) . Effectuez les étapes restantes dans la documentation.

    >[!NOTE]
    >Si vous avez utilisé le DefaultHoloLens2InputSystemProfile, comme indiqué dans la leçon [configurer la boîte à outils de la réalité mixte](https://docs.microsoft.com/windows/mixed-reality/mrlearning-base-ch1#configure-the-mixed-reality-toolkit) , pour cloner votre profil de configuration MRTK personnalisé, le suivi oculaire est activé par défaut dans le projet Unity, mais vous devez toujours configurer la simulation du suivi oculaire pour l’éditeur Unity et configurer Visual Studio pour autoriser le suivi visuel de la Build.

    Le lien ci-dessus fournit de brèves instructions pour les tâches suivantes :

    - Création du point de vue des yeux de la réalité Windows Mixed Fournisseur de données pour une utilisation dans le profil MRTK
    - Activation du suivi oculaire dans le fournisseur de regard attaché à l’appareil photo
    - Configuration d’une simulation de suivi oculaire dans l’éditeur Unity
    - Modification des fonctionnalités de la solution Visual Studio pour permettre l’eye-tracking dans l’application générée

2. Ajoutez le composant Eye Tracking Target aux objets cibles. Pour permettre à un objet de répondre aux événements de point de vue oculaire, nous devons ajouter le composant EyeTrackingTarget sur chaque objet avec lequel nous souhaitons interagir à l’aide de l’œil. Ajoutez ce composant à chacun des neuf objets 3D qui font partie de la collection de la grille.

    >[!TIP]
    >Vous pouvez utiliser les touches Maj et/ou CRTL pour sélectionner plusieurs éléments dans la hiérarchie, puis ajouter en bloc le composant EyeTrackingTarget.

    ![Lesson5 Chapter3 étape 2](images/Lesson5Chapter3Step2.JPG)

3. Nous allons ensuite ajouter le script EyeTrackingTutorialDemo pour des interactions passionnantes. Pour chaque objet 3D de la collection Grid, ajoutez le script EyeTrackingTutorialDemo en recherchant le composant dans le menu Ajouter un composant.

    ![Lesson5 Chapter3 step3](images/Lesson5Chapter3Step3.JPG)

    >[!NOTE]
    >Le support de script EyeTrackingTutorialDemo ne fait pas partie de MRTK, mais il est inclus avec la ressource BaseModuleAssets importée dans la leçon précédente.

4. Faites pivoter l’objet tout en observant la cible. Nous voulons configurer nos objets 3D pour qu’ils tournent pendant que nous les regardons. Pour ce faire, insérez un nouveau champ dans la section en regardant la cible () du composant EyeTrackingTarget, comme indiqué dans l’image ci-dessous.

    ![Lesson5 Chapter3 Step4a](images/Lesson5Chapter3Step4a.JPG)

    Dans le champ nouvellement créé, ajoutez l’objet de jeu actuel au champ vide, puis sélectionnez EyeTrackingTutorialDemo > RotateTarget (), comme indiqué dans l’image ci-dessous. L’objet 3D est maintenant configuré pour pivoter quand il est le focus de l’eye tracking.

    ![Lesson5 Chapter3 Step4b](images/Lesson5Chapter3Step4b.JPG)

5. Ajoutez la possibilité de « spot cible » qui fait l’objet d’un regard sur Select by air ou en disant « Select » (sélectionner). Comme dans l’étape 4, nous voulons déclencher EyeTrackingTutorialDemo > BlipTarget () en l’affectant au champ Select () de l’objet Game du composant EyeTrackingTarget, comme illustré dans la figure ci-dessous. Une fois cette configuration effectuée, vous remarquerez un léger spot dans l’objet de jeu chaque fois que vous déclenchez une action Select, telle qu’un TAP-Air ou la commande vocale « Select ».

    ![Lesson5 Chapter3 étape 5](images/Lesson5Chapter3Step5.JPG)

6. Vérifiez que les fonctionnalités d’eye-tracking sont configurées correctement avant la génération dans HoloLens 2. Au moment de la rédaction de cet article, Unity n’a pas encore la possibilité de définir l’entrée de regard pour les fonctionnalités de suivi oculaire. La définition de cette fonctionnalité est nécessaire pour que le suivi oculaire fonctionne dans HoloLens 2. Suivez le [test de votre application Unity sur les instructions HoloLens 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/EyeTracking/EyeTracking_BasicSetup.html#testing-your-unity-app-on-a-hololens-2) pour activer la fonctionnalité de saisie en regard.

## <a name="congratulations"></a>Félicitations !

Vous avez ajouté avec succès des fonctionnalités de suivi des yeux de base à votre application. Ces premiers pas vous ouvrent la voie vers tout un monde de possibilités avec l’eye-tracking. Ce chapitre conclut également la leçon 5, où nous avons appris les fonctionnalités d’entrée avancées, telles que les commandes vocales, les gestes panoramiques et le suivi oculaire.

[Leçon suivante : 7. création d’un exemple d’application de module lunaire](mrlearning-base-ch6.md)
