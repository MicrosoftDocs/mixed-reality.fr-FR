---
title: Ajouter des environnements d’accueil personnalisés
description: Outre les environnements de base Windows Mixed Reality que nous fournissons, vous pouvez expérimenter la création et à l’aide de votre propre.
author: thmignon
ms.author: thmignon
ms.date: 04/30/2018
ms.topic: article
keywords: Windows Mixed Reality, réalité mixte, réalité virtuelle, VR, MR, accueil, les environnements personnalisés, des lieux, maison de cliff, skyloft, utilisateur, créer
ms.openlocfilehash: 8f5a3a1bdf5728260b0b7717c74a50f3356ca04a
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829642"
---
# <a name="add-custom-home-environments"></a>Ajouter des environnements d’accueil personnalisés

>[!NOTE]
>Il s’agit d’une fonctionnalité expérimentale. Faites un essai et amusez-vous avec lui, mais ne soyez pas surpris si tous les éléments assez ne fonctionnent pas comme prévu. Nous évaluons la viabilité de cette fonctionnalité et l’intérêt de l’utiliser, par conséquent, veuillez Parlez-nous de votre expérience (et des bogues que vous avez trouvé) dans le [forums de développeurs](https://forums.hololens.com/categories/custom-home-environments).

En commençant par le [10 avril 2018 de Windows update](#release-notes-april-2018.md), nous avons activé une fonctionnalité expérimentale qui vous permet d’ajouter des environnements personnalisés pour le sélecteur d’emplacements (dans le menu Démarrer) pour l’utiliser comme la [Windows Mixed Reality accueil](#navigating-the-windows-mixed-reality-home.md). Réalité mixte Windows a deux environnements par défaut, Cliff House et Skyloft, que vous pouvez choisir comme votre page d’accueil. Création des environnements personnalisés vous permet d’étendre cette liste avec vos propres créations. Nous publions ce disponible dans un état anticipé pour évaluer l’intérêt des créateurs et développeurs, Découvrez quels types des mondes vous créez et comprenez l’utilisation des différents outils de création.

Lorsque vous utilisez un environnement personnalisé, vous remarquerez que teleporting, interagir avec les applications et en plaçant hologrammes fonctionnent exactement comme dans le Cliff House et Skyloft. Vous pouvez naviguer sur le web dans un paysage fantastique ou remplir une ville fiction avec hologrammes - les possibilités sont infinies !

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Environnements accueil personnalisés</td>
        <td>❌</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="trying-a-sample-environment"></a>Essayez un exemple d’environnement

Nous avons créé un exemple d’environnement qui montre certains des possibilités de création d’environnements d’accueil personnalisés. Suivez ces étapes pour essayer :
1. [Téléchargez notre exemple d’environnement fantastique île](https://download.microsoft.com/download/B/2/5/B25C1AEF-40CD-4B03-A596-4BCA3D33035A/Fantasy_Island.exe) (lien vers l’exécutable à extraction automatique).

    ![Exemple d’environnement fantastique (île)](images/FantasyLand.jpg)<br>
    *Exemple d’environnement fantastique (île)*<br>

2. Exécutez le **Fantasy_Island.exe** fichier que vous venez de télécharger.

    > [!NOTE]
    > Lorsque vous tentez d’exécuter un fichier .exe téléchargé à partir du web (comme celui-ci), vous pouvez rencontrer une fenêtre contextuelle « Windows protégé par votre PC ». Pour exécuter Fantasy_Island.exe à partir de cette fenêtre contextuelle, sélectionnez **plus d’informations** , puis **quand même exécuter**. Ce paramètre de sécurité est destiné à vous protéger contre le téléchargement de fichiers, vous pouvez souhaiter pas confiance, veuillez choisir cette option uniquement lorsque vous faites confiance à la source du fichier.

3. Ouvrez **Explorateur de fichiers** et accédez au dossier environnements en collant ce qui suit dans la barre d’adresses : `%LOCALAPPDATA%\Packages\EnvironmentsApp_cw5n1h2txyewy\LocalState`.
4. Copiez l’exemple d’environnement que vous avez téléchargé dans ce dossier.
5. Redémarrez **mixte réalité portail**. Cette opération actualise la liste des environnements dans le sélecteur d’emplacements.
6. Placez sur votre casque. Une fois que vous êtes dans la page d’accueil, ouvrez le **menu Démarrer** à l’aide de la Windows bouton votre contrôleur.
7. Sélectionnez le **emplacements** située au-dessus de la liste des applications épinglées pour choisir un environnement domestique.
8. Vous trouverez l’environnement (île) fantastique que vous avez téléchargé dans votre liste d’emplacements. Sélectionnez **fantastique île** à entrer votre nouvel environnement domestique personnalisé !

## <a name="creating-your-own-custom-environment"></a>Création de votre propre environnement personnalisé

Outre l’utilisation des environnements de notre exemple, vous pouvez exporter vos propres environnements personnalisés à l’aide de votre logiciel de retouche de 3D favori. 

### <a name="modeling-guidelines"></a>Instructions de modélisation

Lors de la modélisation de votre environnement, n’oubliez pas les recommandations suivantes. Cela permet de s’assurer l’utilisateur génère dans le bon sens dans un monde believably en taille réelle :

1. Les utilisateurs génèrera 0,0,0 centre c’est le cas, votre emplacement de votre choix de la génération dynamique autour de l’origine.
2. Unités de travaille doivent être définies sur les compteurs afin que les ressources peuvent être créées à l’échelle mondiale.
3. L’axe à distance doit être définie à « Y ».
4. L’élément multimédia doit faire face « forward » vers l’axe Z positif.
5. Toutes les mailles n’êtes pas obligé d’être combinés, mais il est recommandé si vous ciblez des appareils avec contraintes de ressources.

### <a name="exporting-your-environment"></a>Exportation de votre environnement

Réalité mixte Windows s’appuie sur glTF binaire (.glb) en tant que le format de remise pour les environnements actifs. glTF est une redevance gratuit norme ouverte pour la remise de ressources 3D gérée par le groupe Khronos. Comme glTF évolue en tant qu’industrie standard pour le contenu 3D interopérable, ce sera également le support technique de Microsoft pour le format entre les applications Windows et des expériences.

La première étape de l’exportation des ressources à utiliser en tant qu’environnements accueil personnalisés génère un modèle glTF 2.0. Le groupe de travail glTF conserve un [liste des convertisseurs et des exportateurs pris en charge](https://github.com/KhronosGroup/glTF/blob/master/README.md#converters-and-exporters) pour créer un modèle glTF 2.0. Pour commencer, utilisez une des programmes répertoriés dans cette page pour créer et exporter un modèle glTF 2.0 ou convertir un modèle existant à l’aide d’un des convertisseurs pris en charge.

Vous pouvez également consulter [cet article utile](https://www.khronos.org/blog/art-pipeline-for-gltf) qui fournit une vue d’ensemble d’un flux de travail de pointe pour l’exportation des modèles de glTF de Blender, 3DS Max directement. 

### <a name="environment-limits"></a>Limites de l’environnement

Tous les environnements doivent être < 256 Mo. Environnements comptant plus de 256 Mo ne peut pas charger et revenir à un monde vide avec simplement le skybox par défaut autour de l’utilisateur. Gardez cette limite de taille de fichier à l’esprit lors de la création de vos modèles. En outre, si vous envisagez d’optimiser votre environnement à l’aide de la WindowsMRAssetConverter comme décrit ci-dessous, être informé que la taille de texture augmentera à mesure que l’optimiseur crée des textures qui ont une plus grande taille de fichier, mais se chargent plus vite. 

### <a name="optimizing-your-environment"></a>Optimisation de votre environnement

Réalité mixte Windows prend en charge un nombre d’optimisations facultatifs qui réduit considérablement le temps de chargement de vos environnements. Cela peut être particulièrement important pour les environnements comptant plusieurs textures, comme ils expirent parfois lors du chargement. En général, nous vous recommandons cette étape pour toutes les ressources, toutefois, des environnements de petite taille avec peu ou basse résolution textures ne sont pas toujours besoin. 

Pour faciliter ce processus, nous avons créé le [mixte réalité Asset convertisseur Windows (disponible sur GitHub)](https://github.com/Microsoft/glTF-Toolkit/releases) pour effectuer votre optimisations. Cet outil utilise un ensemble d’utilitaires disponibles dans le Kit de ressources Microsoft glTF pour optimiser les .glb ni glTF 2.0 standard en effectuant une compression de texture supplémentaires, la compression et de résolution bas-mise à l’échelle. 

Le convertisseur prend en charge un nombre d’indicateurs pour modifier le comportement exact des optimisations. Nous vous recommandons en cours d’exécution avec les indicateurs suivants pour de meilleurs résultats :

Indicateur|Valeur (s) recommandée|Description
---|---|---
-max-texture-size|1024 ou 2048| Ajustements pour améliorer la qualité des textures, valeur par défaut est 512 x 512. Notez qu’une plus grande valeur affecte considérablement la taille du fichier de l’environnement, gardez la limite de 256 Mo à l’esprit
-min-version|1803|Environnements personnalisés sont uniquement pris en charge sur les versions de windows > = 1803. Cet indicateur supprime les textures pour les versions antérieures et réduire la taille du fichier de l’élément multimédia finale

Exemple :

```cmd
WindowsMRAssetConverter FileToConvert.gltf -max-texture-size 1024 -min-version 1803
```

### <a name="testing-your-environment"></a>Test de votre environnement

Une fois que vous avez votre environnement final .glb vous êtes prêt à le tester dans le casque. Commencez à l’étape 2 dans le [« Essayez un exemple d’environnement »](#trying-a-sample-environment) section pour utiliser votre environnement personnalisé en tant que la réalité mixte domestique. 

## <a name="feedback"></a>Commentaires

Pendant que nous évaluons cette fonctionnalité expérimentale, nous sommes en savoir comment vous utilisez des environnements personnalisés, des bogues que vous pouvez rencontrer, et comment vous que la fonctionnalité. Veuillez partager tous les commentaires pour créer et utiliser des environnements d’accueil personnalisés dans le [forums de développeurs](https://forums.hololens.com/categories/custom-home-environments).

## <a name="troubleshooting-and-tips"></a>Résolution des problèmes et conseils

### <a name="how-do-i-change-the-name-of-the-environment"></a>Comment modifier le nom de l’environnement ?

Le nom de fichier dans le dossier environnements sera utilisé dans le sélecteur d’emplacements. Pour modifier le nom de votre environnement simplement renommer l’environnement de nom de fichier et redémarrez Portal de réalité mixte.

### <a name="how-do-i-remove-custom-environments-from-my-places-picker"></a>Comment supprimer des environnements personnalisés à partir de mon sélecteur d’emplacements ?

Pour supprimer un environnement personnalisé, ouvrez le dossier environnements sur votre PC (`%LOCALAPPDATA%\Packages\EnvironmentsApp_cw5n1h2txyewy\LocalState`) et suppression de l’environnement. Une fois que vous redémarrez le portail de réalité mixte, cet environnement n’apparaît plus dans le sélecteur d’emplacements. 

### <a name="how-do-i-default-to-my-favorite-custom-environment"></a>Mode par défaut de mon environnement personnalisé préféré ?

Vous ne pouvez pas modifier actuellement l’environnement par défaut. Chaque fois que vous redémarrez Portal de réalité mixte, vous serez redirigé vers l’environnement Cliff House. 

### <a name="i-spawn-into-a-blank-space"></a>J’ai spawn dans un espace vide

Windows Mixed Reality [ne prend pas en charge les environnements qui dépassent 256 Mo](#environment-limits). Lorsqu’un environnement dépasse cette limite, vous accédez dans la zone de ciel vide sans modèle.

### <a name="it-takes-a-long-time-to-load-my-environment"></a>Il prend beaucoup de temps à charger mon environnement

Vous pouvez ajouter des optimisations facultatives à votre environnement pour le rendre se chargent plus vite. Consultez [« Optimisation de votre environnement »](#optimizing-your-environment) pour plus d’informations.

### <a name="the-scale-of-my-environment-is-incorrect"></a>La mise à l’échelle de mon environnement est incorrect

Windows Mixed Reality traduit unités glTF à 1 mètre lors du chargement des environnements. Si votre environnement charge une mise à l’échelle inattendue, vérifiez votre exportateur pour vous assurer que vous modélisez à une échelle de 1 mètre. 

### <a name="the-spawn-location-in-my-environment-is-incorrect"></a>L’emplacement de génération dans mon environnement est incorrect

L’emplacement de génération par défaut se trouve dans 0,0,0 dans l’environnement. Son pas actuellement possible de personnaliser cet emplacement, vous devez donc apporter le point de générer en exportant votre environnement avec l’origine positionné sur le point de génération souhaité.

### <a name="the-audio-doesnt-sound-correct-in-the-environment"></a>L’audio ne semble pas correct dans l’environnement

Lorsque vous créez votre environnement personnalisé, il utilisera une simulation de rendu acoustiques qui ne correspond pas à l’espace physique que vous avez créé. Son peuvent provenir les directions incorrectes et peut sembler muffled. 

## <a name="see-also"></a>Voir aussi
* [Navigation dans les fenêtres mixte réalité accueil](#navigating-the-windows-mixed-reality-home.md)
* [Windows mixte réalité Asset convertisseur (sur GitHub)](https://github.com/Microsoft/glTF-Toolkit/releases)

