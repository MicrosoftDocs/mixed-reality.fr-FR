---
title: Autocar à main
description: mains en 3D qui sont déclenchées lorsque le système ne détecte pas les mains de l’utilisateur pour aider à les assister.
author: grayclee
ms.author: glee
ms.date: 09/25/2019
ms.topic: article
keywords: Windows Mixed Reality, conception, coach, casque immersif, MRTK, mains, main
ms.openlocfilehash: c5f0a0c241ff71dc93f370a5a8caa627128bfb1a
ms.sourcegitcommit: 1ec628a9107194c0a9d4073b5ca09ee816030e85
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/01/2020
ms.locfileid: "78202733"
---
# <a name="hand-coach"></a>Autocar à main

La main est un modèle de mains en 3D qui est déclenché lorsque le système ne détecte pas les mains de l’utilisateur. Elle est implémentée en tant que composant « d’apprentissage » qui aide à guider l’utilisateur lorsque le mouvement n’a pas été enseigné. Si les utilisateurs n’ont pas effectué le mouvement spécifié pour un point, les mains sont en boucle avec un délai. L’entraîneur peut être utilisé pour représenter un bouton ou un hologramme.  


![exemple : main](images/HandCoach/MRTK_handCoach.jpg)<br>
*Exemple HandCoach à partir de MRTK*

## <a name="hand-coach-provided"></a>Autocar fourni

Le modèle d’interaction actuel représente un large éventail de contrôles de mouvement, tels que le défilement, l’amplitude de sélection et le TAP. Vous trouverez ci-dessous une liste complète des gestes existants disponibles dans<a href="https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets"> MRTK</a>:

:::row:::
    :::column:::
       ![exemple de près de Select](images/HandCoach/NearSelect.gif)<br>
       **Exemple de près de Select-used montre comment sélectionner des boutons ou fermer des objets interactifs**<br>
    :::column-end:::
    :::column:::
       ![exemple de pression d’air](images/HandCoach/AirTap.gif)<br>
        **Exemple de robinet d’air-utilisé pour montrer comment sélectionner des objets éloignés**<br>
    :::column-end:::
    :::column:::
       ![exemple de déplacement](images/HandCoach/Move.gif)<br>
       **Exemple de déplacement d’un objet dans l’espace utilisé pour montrer comment déplacer un hologramme dans l’espace**<br>
    :::column-end:::
    :::column:::
       ![exemple de rotation](images/HandCoach/Rotate.gif)<br>
       **Exemple de Rotate-utilisé pour montrer comment faire pivoter des hologrammes ou des objets**<br>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
       ![exemple de](images/HandCoach/Scale.gif) de mise à l’échelle<br>
       **Exemple de mise à l’échelle : utilisé pour montrer comment manipuler les hologrammes pour qu’ils soient plus grands ou plus petits**<br>
    :::column-end:::
    :::column:::
       ![exemple de](images/HandCoach/PalmUp.gif) de palmier<br>
        **Exemple de Palm up – utilisation suggérée pour afficher les menus de la main**<br>
    :::column-end:::
    :::column:::
       ![exemple de HandFlip](images/HandCoach/HandFlip.gif)<br>
       **Tour de main : un autre moyen d’afficher des menus manuels**<br>
    :::column-end:::
    :::column:::
       ![exemple de défilement](images/HandCoach/Scoll.gif)<br>
       **Exemple de défilement : utilisé pour faire défiler une liste ou un document long**<br>
    :::column-end:::
:::row-end:::

## <a name="design-concepts"></a>Concepts de conception

Pour Hololens2, nous avons conçu des interactions de handles basées sur les gestes instinctual et Natural main. Nous pensons que ceux-ci sont intuitifs pour la plupart des utilisateurs et n’ont donc pas créé de moments d’apprentissage de mouvement dédiés. Au lieu de cela, nous avons créé le coach pour aider les utilisateurs qui peuvent être bloqués ou qui ne sont pas familiarisés avec l’interaction avec les hologrammes en savoir plus sur ces gestes. Sans un moment d’apprentissage, nous avons pensé que les utilisateurs indiquent comment effectuer une action en montrant qu’il s’agit de la meilleure option. Dans nos études, nous avons découvert que les utilisateurs étaient en mesure de déterminer le geste, mais ont besoin d’un peu de conseils. Si nous détectons qu’un utilisateur n’interagit pas avec un objet pendant un certain laps de temps, un autocar manuel sera déclenché pour illustrer la main correcte et le positionnement des doigts. 

### <a name="intuitive"></a>Peu

Quand vous animez des mains, cela doit être évident et shoudn’t provoquer des confusions. L’animation des mains est une représentation du geste que vous essayez de évoquer à l’utilisateur pour comprendre son rôle. 

Par exemple, si vous souhaitez qu’un utilisateur appuie sur un bouton, une main appuyant sur un bouton est déclenchée.

Exemple de ![: main près TAP](images/HandCoach/NearSelect_unity.gif)<br>
*Autocar montrant un témoin proche d’une gemme*  

### <a name="hand-scale"></a>Mise à l’échelle manuelle

Nous avons testé différentes tailles de main avec les menus de l’interface utilisateur et j’ai pensé que si la main était vraie, elle donnait une menaçant, mais si elle était trop petite, il était difficile de voir et de comprendre le geste. 

**Voix et mains**

Ne vous attendez pas à ce que les utilisateurs puissent écouter un ensemble d’instructions via la voix et regarder différentes instructions via la main. Séquencez vos instructions pour aider les utilisateurs à se concentrer sur leur attention et à réduire la surcharge sensorielle.


## <a name="can-i-create-my-own"></a>Puis-je créer mon propre ?

Oui. Nous vous encourageons à créer votre propre geste unique pour votre jeu et à contribuer à la communauté !
Nous avons fourni un fichier maya d’une main qui peut être utilisée pour votre application et qui peut être téléchargée ici : <a href="files/HandCoach_MRTK.zip">télécharger HandCoach_MRTK. zip</a>

![exemple de mains animées dans Maya](images/HandCoach/MayaSelect_Gif.gif)<br>
*Exemple de la main animée d’une boîte dans Maya*


**Outil de création recommandé**

Parmi les artistes en 3D, beaucoup choisissent d’utiliser les [Maya de Autodesk qui peuvent lui-même utiliser HoloLens](https://www.youtube.com/watch?v=q0K3n0Gf8mA) pour transformer la façon dont les ressources sont créées. Le fichier mains fourni est un fichier binaire Maya. il est donc recommandé d’utiliser Maya pour animer et exporter les mains. Si vous préférez utiliser un autre programme 3D, voici un <b>. FBX</b>: <a href="files/HandCoachMRTK_FBX.zip">Téléchargez HandCoachMRTK_FBX. zip</a> pour créer votre propre configuration de contrôleur. 

Si vous utilisez le fichier. Maya téléchargeable fourni, il est recommandé de réduire les mains dans Unity à 0,6.

Exemple de ![: une plate-forme de autocar dans Maya](images/HandCoach/MayaExample.png)<br>
*Mains*

### <a name="technical-specs"></a>Caractéristiques techniques

*   Deux fichiers droitier sont disponibles au format ASCII Maya
*    La partie droite et la main gauche sont disponibles au format binaire Maya
*   Définir votre fichier maya sur 24 ips
*   Dans le fichier, il y a une main gauche et une main droite qui peuvent être utilisées pour deux gestes droitiers ou à sens unique. La main droite est visible uniquement par défaut.
*   Il est recommandé de conserver une mémoire tampon d’environ 10 frames au début et à la fin pour les disparitions
*   En cas d’animation d’un objet avec une cible spécifiée, il est recommandé d’animer une case par défaut ou une valeur null.
*   Si la main anime un objet physique tel qu’une zone, il est recommandé de ne pas animer la translation dans Maya, mais d’en faire une animation dans Unity ou dans le code.
*   L’animation visible doit être de 1,5 secondes pour que toutes les informations significatives soient transmises
*   Quand vous êtes satisfait de votre animation :
    *   Sélectionner tous les joints et les images clés de cuisson
    *   Supprimez les contrôleurs, sélectionnez les jointures et les maillages, puis exportez-les en tant que FBX
    *  S’il existe plusieurs animations, vous pouvez utiliser l’exportateur de jeux intégré à Maya : https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2015/ENU/Maya/files/Game-Exporter-htm.html

## <a name="exporting-from-maya"></a>Exportation à partir de Maya

Une fois que vous êtes satisfait de votre animation
* Sélectionner tous les jointures : sélectionnez > hiérarchie

     ![Exemple : emplacement du menu](images/HandCoach/Hierarchy.png)<br>
* Intégrer votre animation : basculer vers l’animation > touche > animation de cuisson

     ![Exemple : emplacement du menu](images/HandCoach/BakeAnimation.png)<br>
* Supprimer la plate-forme de contrôleur : > MainR_Grp ou MainL_Grp

     ![Exemple : emplacement du menu](images/HandCoach/ControllerRig.png)<br>

* Exporter en tant que FBX : sélectionnez JNT + maille : fichier > Exporter la sélection (case d’option) > Exporter la sélection

     ![Exemple : emplacement du menu](images/HandCoach/OptionBox.png)<br>

     ![Exemple : emplacement du menu](images/HandCoach/SelectionExport.png)<br>

     ![Exemple : emplacement du menu](images/HandCoach/FBXSelection.png)<br>


 Lorsque vous exportez en tant que FBX et que vous mettez sous Unity, mettez à l’échelle les mains jusqu’à 0,6. Nous avons découvert que ce fut parfait pour l’affichage des mains. 

Exemple de ![: paramètres Unity](images/HandCoach/HandHintScale.png)<br>
*Paramètres Unity pour HandCoach_R Prefab trouvés dans MRTK*


## <a name="implementing-hands-into-your-unity-project"></a>Implémentation des mains dans votre projet Unity

### <a name="best-practices"></a>Meilleures pratiques
*    Il est suggéré de réduire les mains d’Unity à 0,6
*   Les mains doivent être jouées deux fois et si elles ne sont pas terminées, puis en boucle jusqu’à ce que le geste soit terminé. Les mains doivent être bouclées deux fois pour garantir que l’utilisateur avait le temps de s’inscrire et de voir le mouvement. Les mains doivent apparaître et disparaître entre les boucles. 
 *  Si les mains de l’utilisateur sont visibles par les appareils photo HL2, mais que les utilisateurs n’effectuent pas l’interaction dont ils ont besoin, les mains s’affichent au bout de 10 secondes.
*   Si les mains de l’utilisateur ne sont pas visibles par les appareils photo HL2, les mains s’affichent au bout de 5 secondes.  
*   Si les mains de l’utilisateur sont visibles par les appareils photo HL2 au milieu de l’animation, l’animation se termine et disparaît en fondu.
*   Si vous incluez la voix, nous suggérons qu’elle corresponde au geste de la main.
*   Si vous avez enseigné les mains au moins une fois, répétez uniquement le mouvement si son a détecté que l’utilisateur est bloqué.
*   Si les positions de doigt/main spécifiques sont critiques, assurez-vous que les utilisateurs peuvent voir clairement ces nuances dans l’animation. Essayez droite les mains pour que les parties les plus importantes soient clairement visibles. 
* Si vous constatez une distorsion des mains, vous devez accéder aux paramètres de qualité de Unity pour augmenter la quantité d’os. 
 Accédez à modifier > paramètres du projet > qualité > autres > poids de la fusion. Assurez-vous que « 4 segments » sont sélectionnés pour afficher des articulations lisses. 

   ![Exemple : emplacement du menu](images/HandCoach/ProjectSettings.png)<br>





### <a name="what-to-avoid"></a>Éléments à éviter
* Mise à l’échelle des mains trop grandes
* le placement des mains trop près de l’utilisateur
* Les mains ne doivent être enseignées qu’une seule fois. L’apprentissage peut entraîner des confusions et des opérations
*   En le plaçant dans Unity, téléchargez la dernière version de MRTK ici : https://github.com/microsoft/MixedRealityToolkit-Unity
    *   Matériel : Teaching_Hand2
    *   Scripts : consultez MRTK Guidelines for <a href= "https://github.com/MixedRealityToolkit-Unity/blob/'HandCoachUX'/Documentation/README_HandCoach.md">MRTK main coach</a>
    *   Paramètre par projet
        *   Scène définie sur UWP : l’instruction se trouve dans le [projet configurer Unity](Configure-Unity-Project.md) pour Windows Mixed Reality

## <a name="see-also"></a>Voir aussi
* [Interaction-notions de base](interaction-fundamentals.md)
* [Processus de création de ressources](asset-creation-process.md)
* [Mouvements](gestures.md)
* [Installer les outils](install-the-tools.md)
* [Configurer le projet Unity](Configure-Unity-Project.md)
* [Vue d’ensemble du développement Unity](unity-development-overview.md)
* [MRTK 101](mrtk-101.md)
