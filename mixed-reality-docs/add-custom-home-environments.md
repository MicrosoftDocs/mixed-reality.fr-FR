---
title: Concevez vos propres environnements immersifs
description: Outre les environnements Windows Mixed Reality que nous fournissons, vous pouvez expérimenter la création et l’utilisation de vos propres environnements.
author: thmignon
ms.author: thmignon
ms.date: 04/30/2018
ms.topic: article
keywords: Windows Mixed Reality, la réalité mixte, la réalité virtuelle, VR, MR, famille, environnements personnalisés, lieux, salle de falaise, Skyloft, utilisateur, créer
ms.openlocfilehash: e133e1438410540592a51f54ed136aecd04c6244
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437077"
---
# <a name="design-your-own-immersive-environments"></a>Concevez vos propres environnements immersifs

>[!NOTE]
>Il s’agit d’une fonctionnalité expérimentale. Faites un essai et amusez-vous, mais ne soyez pas surpris si tout ne fonctionne pas comme prévu. Nous évaluons la viabilité de cette fonctionnalité et nous encourageons à l’utiliser. Veuillez donc nous faire part de votre expérience (et de tous les bogues que vous avez trouvés) dans les [Forums des développeurs](https://forums.hololens.com/categories/custom-home-environments).

À compter de la [mise à jour 2018 de Windows 10 avril](release-notes-april-2018.md), nous avons activé une fonctionnalité expérimentale qui vous permet d’ajouter des environnements personnalisés au sélecteur emplacements (dans le menu Démarrer) afin de l’utiliser comme page d’accueil de la [réalité mixte Windows](navigating-the-windows-mixed-reality-home.md). Windows Mixed Reality a deux environnements par défaut : la maison de falaise et Skyloft, que vous pouvez choisir comme maison. La création d’environnements personnalisés vous permet d’étendre cette liste avec vos propres créations. Nous mettons cela à disposition dans un état précoce pour évaluer l’intérêt des créateurs et des développeurs, consultez les genres de mondes que vous créez et comprenez comment vous travaillez avec différents outils de création.

Lorsque vous utilisez un environnement personnalisé, vous remarquerez que le téléportage, l’interaction avec les applications et le placement des hologrammes fonctionnent exactement comme dans la maison de la falaise et Skyloft. Vous pouvez naviguer sur le Web dans un paysage imaginaire ou remplir une ville d’anticipation avec des hologrammes. les possibilités sont infinies !

## <a name="device-support"></a>Périphériques pris en charge

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Environnements d’hébergement personnalisés</td>
        <td>❌</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="trying-a-sample-environment"></a>Essayer un exemple d’environnement

Nous avons créé un exemple d’environnement qui illustre certaines des possibilités créatives des environnements d’hébergement personnalisés. Pour le tester, procédez comme suit :
1. [Téléchargez notre exemple d’environnement d’îlots imaginaires](https://download.microsoft.com/download/B/2/5/B25C1AEF-40CD-4B03-A596-4BCA3D33035A/Fantasy_Island.exe) (points de lien vers un fichier exécutable à extraction automatique).

    exemple d’environnement de ![imaginaire](images/FantasyLand.jpg)<br>
    *Exemple d’environnement de l’îlot imaginaire*<br>

2. Exécutez le fichier **Fantasy_Island. exe** que vous venez de télécharger.

    > [!NOTE]
    > Lorsque vous tentez d’exécuter un fichier. exe téléchargé à partir du Web (comme celui-ci), vous pouvez rencontrer une fenêtre contextuelle « Windows a protégé votre PC ». Pour exécuter Fantasy_Island. exe à partir de ce menu contextuel, sélectionnez **plus d’informations** , puis **Exécutez quand même**. Ce paramètre de sécurité est destiné à vous protéger contre le téléchargement de fichiers que vous ne souhaitez peut-être pas approuver. par conséquent, choisissez cette option uniquement lorsque vous faites confiance à la source du fichier.

3. Ouvrez l' **Explorateur de fichiers** et accédez au dossier environnements en collant ce qui suit dans la barre d’adresses : `%LOCALAPPDATA%\Packages\EnvironmentsApp_cw5n1h2txyewy\LocalState`.
4. Copiez l’exemple d’environnement que vous avez téléchargé dans ce dossier.
5. Redémarrez le **portail de réalité mixte**. Cette opération actualise la liste des environnements dans le sélecteur emplacements.
6. Placez sur votre casque. Une fois que vous êtes dans la page d’accueil, ouvrez le **menu Démarrer** à l’aide du bouton Windows de votre contrôleur.
7. Sélectionnez l’icône **emplacements** au-dessus de la liste des applications épinglées pour choisir un environnement d’hébergement.
8. Vous trouverez l’environnement des îlots fantastiques que vous avez téléchargé dans la liste des emplacements. Sélectionnez **îlot imaginaire** pour accéder à votre nouvel environnement d’hébergement personnalisé.

## <a name="creating-your-own-custom-environment"></a>Création de votre propre environnement personnalisé

Outre l’utilisation de nos exemples d’environnements, vous pouvez exporter vos propres environnements personnalisés à l’aide de votre logiciel de modification 3D préféré. 

### <a name="modeling-guidelines"></a>Instructions de modélisation

Lorsque vous modélisez votre environnement, gardez à l’esprit les recommandations suivantes. Cela permet de s’assurer que l’utilisateur génère une orientation correcte dans un monde de taille incroyable :

1. Les utilisateurs s’exécuteront à 0, 0, afin de centraliser l’emplacement de génération souhaité autour de l’origine.
2. Les unités de travail doivent être définies sur des mètres afin que les ressources puissent être créées à l’échelle mondiale.
3. L’axe vers le haut doit être défini sur « Y ».
4. L’élément multimédia doit être orienté vers l’avant vers l’axe Z positif.
5. Il n’est pas nécessaire de combiner tous les maillages, mais il est recommandé si vous ciblez des appareils à ressources restreintes.

### <a name="exporting-your-environment"></a>Exportation de votre environnement

Windows Mixed Reality s’appuie sur un glTF binaire (. GLB) comme format de remise des ressources pour les environnements. glTF est une norme ouverte payante gratuite pour la remise de ressources en 3D gérée par le groupe Khronos. Comme glTF évolue comme une norme industrielle pour le contenu 3D interopérable, Microsoft prend en charge le format sur les applications et les expériences Windows.

La première étape de l’exportation des ressources à utiliser comme des environnements d’origine personnalisés consiste à générer un modèle glTF 2,0. Le groupe de travail glTF gère une [liste d’exportateurs et de convertisseurs pris en charge](https://github.com/KhronosGroup/glTF/blob/master/README.md#converters-and-exporters) pour créer un modèle glTF 2,0. Pour commencer, utilisez l’un des programmes figurant sur cette page pour créer et exporter un modèle glTF 2,0, ou pour convertir un modèle existant à l’aide de l’un des convertisseurs pris en charge.

En outre, consultez [cet article utile](https://www.khronos.org/blog/art-pipeline-for-gltf) qui fournit une vue d’ensemble d’un flux de travail artistique pour l’exportation de modèles glTF à partir de Blender et de 3ds Max directement. 

### <a name="environment-limits"></a>Limites de l’environnement

Tous les environnements doivent être < 256 Mo. Les environnements dont la taille est supérieure à 256 Mo ne peuvent pas se charger et revenir à un monde vide avec uniquement les skybox par défaut entourant l’utilisateur. Gardez cette limite de taille de fichier à l’esprit lors de la création de vos modèles. En outre, si vous envisagez d’optimiser votre environnement à l’aide du WindowsMRAssetConverter, comme décrit ci-dessous, Cognizant que la taille de la texture augmente à mesure que l’optimiseur crée des textures dont la taille de fichier est plus importante, mais se chargent plus rapidement. 

### <a name="optimizing-your-environment"></a>Optimisation de votre environnement

Windows Mixed Reality prend en charge un certain nombre d’optimisations facultatives, ce qui réduira considérablement le temps de chargement de vos environnements. Cela peut être particulièrement important pour les environnements avec de nombreuses textures, car ils expirent parfois pendant le chargement. En général, nous vous recommandons d’effectuer cette étape pour toutes les ressources. Toutefois, les environnements plus petits avec des textures à faible ou faible résolution ne le nécessitent pas toujours. 

Pour faciliter ce processus, nous avons créé le [convertisseur Windows Mixed Reality (disponible sur GitHub)](https://github.com/Microsoft/glTF-Toolkit/releases) pour effectuer vos optimisations. Cet outil utilise un ensemble d’utilitaires disponibles dans Microsoft glTF Toolkit pour optimiser les 2,0 glTF ou. GLB standard en effectuant une mise à l’échelle de texture supplémentaire, en réduisant la compression et en réduisant la résolution. 

Actuellement, le convertisseur prend en charge un certain nombre d’indicateurs pour affiner le comportement exact des optimisations. Pour de meilleurs résultats, nous vous recommandons d’exécuter avec les indicateurs suivants :

Flag|Valeur (s) recommandée (s)|Description
---|---|---
-Max-texture-taille|1024 ou 2048| Ajustez ceci pour améliorer la qualité des textures, la valeur par défaut est 512 x 512. Notez qu’une valeur plus grande aura un impact significatif sur la taille de fichier de l’environnement, tout en conservant la limite de 256 Mo à l’esprit.
-min-version|1803|Les environnements personnalisés ne sont pris en charge que sur les versions de Windows > = 1803. Cet indicateur supprime les textures des anciennes versions et réduit la taille du fichier de la ressource finale

Exemple :

```cmd
WindowsMRAssetConverter FileToConvert.gltf -max-texture-size 1024 -min-version 1803
```

### <a name="testing-your-environment"></a>Test de votre environnement

Une fois que vous avez votre environnement final. GLB, vous êtes prêt à le tester dans le casque. Commencez à l’étape 2 de la section [« tentative d’un environnement d’exemple »](#trying-a-sample-environment) pour utiliser votre environnement personnalisé comme page d’accueil de la réalité mixte. 

## <a name="feedback"></a>Retour d’expérience

Pendant que nous évaluons cette fonctionnalité expérimentale, nous nous intéressons à la façon dont vous utilisez les environnements personnalisés, aux bogues que vous pouvez rencontrer et à la façon dont vous aimez la fonctionnalité. Veuillez partager tous les commentaires relatifs à la création et à l’utilisation d’environnements d’hébergement personnalisés dans les [Forums des développeurs](https://forums.hololens.com/categories/custom-home-environments).

## <a name="troubleshooting-and-tips"></a>Résolution des problèmes et conseils

### <a name="how-do-i-change-the-name-of-the-environment"></a>Comment faire modifier le nom de l’environnement ?

Le nom du fichier dans le dossier environnements sera utilisé dans le sélecteur emplacements. Pour modifier le nom de votre environnement, il vous suffit de renommer le nom de fichier de l’environnement, puis de redémarrer le portail de réalité mixte.

### <a name="how-do-i-remove-custom-environments-from-my-places-picker"></a>Comment faire supprimer les environnements personnalisés du sélecteur de favoris ?

Pour supprimer un environnement personnalisé, ouvrez le dossier environnements sur votre ordinateur (`%LOCALAPPDATA%\Packages\EnvironmentsApp_cw5n1h2txyewy\LocalState`) et supprimez l’environnement. Une fois que vous avez redémarré le portail de réalité mixte, cet environnement n’apparaît plus dans le sélecteur emplacements. 

### <a name="how-do-i-default-to-my-favorite-custom-environment"></a>Comment faire par défaut à mon environnement personnalisé préféré ?

Vous ne pouvez pas modifier actuellement l’environnement par défaut. Chaque fois que vous redémarrez le portail de réalité mixte, vous êtes redirigé vers l’environnement de la maison de la falaise. 

### <a name="i-spawn-into-a-blank-space"></a>Je génère un espace vide

Windows Mixed Reality [ne prend pas en charge les environnements qui dépassent 256 Mo](#environment-limits). Quand un environnement dépasse cette limite, vous accédez à la zone ciel vide sans modèle.

### <a name="it-takes-a-long-time-to-load-my-environment"></a>Le chargement de mon environnement prend beaucoup de temps

Vous pouvez ajouter des optimisations facultatives à votre environnement pour accélérer le chargement. Pour plus d’informations, consultez [« optimisation de votre environnement »](#optimizing-your-environment) .

### <a name="the-scale-of-my-environment-is-incorrect"></a>L’échelle de mon environnement est incorrecte

Windows Mixed Reality convertit les unités glTF en 1 mètre lors du chargement des environnements. Si votre environnement charge une échelle inattendue, vérifiez-le pour vous assurer que vous effectuez la modélisation à une échelle à 1 mètre. 

### <a name="the-spawn-location-in-my-environment-is-incorrect"></a>L’emplacement de génération dans mon environnement est incorrect

L’emplacement de génération par défaut se trouve à 0, 0, 0 dans l’environnement. Comme il n’est pas possible actuellement de personnaliser cet emplacement, vous devez modifier le point de génération en exportant votre environnement avec l’origine positionnée sur le point de génération souhaité.

### <a name="the-audio-doesnt-sound-correct-in-the-environment"></a>L’audio ne fonctionne pas correctement dans l’environnement

Lorsque vous créez votre environnement personnalisé, il utilise une simulation de rendu acoustique qui ne correspond pas à l’espace physique que vous avez créé. Les sons peuvent provenir de mauvaises directions et le bruit peut être atténué. 

## <a name="see-also"></a>Articles associés
* [Convertisseur de ressources Windows Mixed Reality (sur GitHub)](https://github.com/Microsoft/glTF-Toolkit/releases)

