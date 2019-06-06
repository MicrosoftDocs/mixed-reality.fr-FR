---
title: Processus de création de ressource
description: Conseils sur la création de ressources pour les expériences de réalité mixte.
author: paseb
ms.author: paseb
ms.date: 03/21/2018
ms.topic: article
keywords: élément multimédia, la création, processus, budget, polygones, textures, nuanceurs et performances
ms.openlocfilehash: 513a9856ac35e4229cfb7bc8bcb92d9d6a152980
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66692299"
---
# <a name="asset-creation-process"></a>Processus de création de ressource

Réalité mixte Windows s’appuie sur des décennies d’investissement, que Microsoft a apporté dans DirectX. Cela signifie que tous les développeurs de l’expérience et les compétences avoir avec création 3D graphics continue d’être précieuse sur HoloLens.

Les ressources que vous créez pour un projet se présentent sous des formes variées. Il peuvent être constituées d’une série de textures/images, audio, vidéo, des modèles 3D et les animations. Nous ne pouvons pas commencer à couvrir tous les outils qui sont disponibles pour créer les différents types de ressources utilisées dans un projet. Cet article, nous nous concentrerons sur les méthodes de création de ressources 3D.

![Flux de concept, la création, l’intégration et itération](images/concept-creation-integration-iteration-flow-640px.jpg)<br>
*Flux de concept, la création, l’intégration et itération*

## <a name="things-to-consider"></a>Points à prendre en considération

Lorsque examinant l’expérience que vous tentez de créer la considérer comme un **budget** dont vous disposez pour essayer de créer la meilleure expérience. Ne comporte pas nécessairement limité sur le nombre de **polygones** ou **types de matériaux** utiliser dans vos ressources, mais plus un ensemble de budgétisé de compromis.

Voici une allocation de réserve d’exemple pour votre expérience. Performances ne sont généralement pas un point unique de défaillance mais mort par morceaux mille par-se.
<br>

<table style="float:right; margin-left: 10px;">
<tr>
<th style="text-align:left;"><b>Ressources</b></th><th style="text-align:right;"> Processeur</th><th> Processeur graphique</th><th> Mémoire</th>
</tr><tr>
<td> Polygones</td><td> 0%</td><td> 5%</td><td> 10%</td>
</tr><tr>
<td> Textures</td><td> 5%</td><td> 15%</td><td>25%</td>
</tr><tr>
<td> Nuanceurs</td><td> 15%</td><td> 35%</td><td> 0%</td>
</tr><tr>
<td> <b>Dynamics</b></td><td></td><td></td><td></td>
</tr><tr>
<td> Physique</td><td> 5%</td><td> 15%</td><td> 0%</td>
</tr><tr>
<td> Éclairage d’en temps réel</td><td> 10%</td><td> 0%</td><td> 0%</td>
</tr><tr>
<td> Média (audio/vidéo)</td><td> -</td><td> 15%</td><td> 25%</td>
</tr><tr>
<td> / Logique de script</td><td> 25%</td><td> 0%</td><td> 5%</td>
</tr><tr>
<td> Frais généraux</td><td> 5%</td><td> 5%</td><td> 5%</td>
</tr><tr>
<td> <b>Total</b></td><td> <b>65%</b></td><td> <b>90%</b></td><td> <b>70%</b></td>
</tr>
</table>

**Nombre total de ressources**
* Nombre de ressources est actif dans la scène ?

**Complexité des actifs**
* Combien de triangles / polygones ?
* La complexité est le nuanceur ?

Les développeurs et les artistes ont à prendre en compte les fonctionnalités de l’appareil et le moteur de graphiques. Microsoft HoloLens dispose de toutes le calcul et graphiques intégré à l’appareil. Il partage les fonctionnalités que les développeurs se trouverait sur une plateforme mobile.

Le processus de création de ressources est le même quelle que soit la si vous ciblez une expérience pour un [HOLOGRAPHIQUE appareil ou un appareil immersif](mixed-reality.md#the-mixed-reality-spectrum). La principale chose à noter est la fonctionnalité de l’appareil comme indiqué ci-dessus, ainsi que la mise à l’échelle dans la mesure où vous pouvez voir le monde réel dans la réalité mixte, que vous pouvez mettre à jour de la mise à l’échelle correcte en fonction de l’expérience. 

## <a name="authoring-assets"></a>Création de ressources

Nous allons commencer par les méthodes pour obtenir des ressources de votre projet :
1. Création d’éléments multimédias (objet capturer et outils de création)
2. Achat de ressources (actifs acheter en ligne)
3. Portage des ressources (en prenant les ressources existantes)
4. Externalisation des ressources (actifs de l’importation à partir de la 3e parties)

### <a name="creating-assets"></a>Création d’éléments multimédias

**Outils de création**<br>
Tout d’abord, vous pouvez créer vos propres ressources dans un nombre de différentes façons. Artistes 3D utilisent un nombre d’applications et des outils pour créer des modèles qui sont composées de **maillages**, **textures**, et **matériaux**. Il est ensuite enregistré dans un format de fichier qui peut être importé ou utilisé par le moteur de graphiques utilisé par l’application, comme **. FBX** ou **. OBJ**. Fonctionne sur n’importe quel outil qui génère un modèle qui prend en charge de votre moteur de graphiques choisi **HoloLens**. Parmi les artistes 3D, nombreuses choisir d’utiliser [Maya d’Autodesk qui lui-même est en mesure d’utiliser HoloLens](https://www.youtube.com/watch?v=q0K3n0Gf8mA) pour transformer les ressources de façon sont créés. Si vous souhaitez obtenir quelque chose dans rapide, vous pouvez également utiliser [3D Builder](https://developer.microsoft.com/windows/hardware/3d-print/3d-builder-resources) qui est fourni avec Windows à exporter. OBJ pour une utilisation dans votre application.

**Capture de l’objet**<br>
Il est également l’option pour capturer des objets en 3D. Capture des objets inanimés en 3D et les modifier avec le logiciel de création de contenus numériques sont de plus en plus populaire avec l’augmentation de l’impression 3D. À l’aide de la **Kinect 2** capteur et [3D Builder](https://developer.microsoft.com/windows/hardware/3d-print/3d-builder-resources) vous pouvez utiliser la fonctionnalité de capture pour créer des ressources à partir des objets du monde réel. C’est également un [suite d’outils](https://en.wikipedia.org/wiki/Comparison_of_photogrammetry_software) à faire de même avec **PHOTOGRAMMÉTRIE** par traitement d’un nombre d’images à la maille et agrafage ensemble et des textures.

### <a name="purchasing-assets"></a>Achat de ressources

Une autre excellente option consiste à acheter des ressources pour votre expérience. Il existe une multitude de ressources disponibles via les services tels que le [Unity Asset Store](https://www.assetstore.unity3d.com/) ou [TurboSquid](http://www.turbosquid.com/) entre autres.

Lorsque vous achetez des ressources à partir d’un tiers 3e toujours voulez-vous vérifier les points suivants :
* **Quel est le nombre de poly ?**
  * Il tient au sein de votre budget ?
* **Existe-t-il des niveaux de détail (degrés) pour le modèle ?**
  * Niveau de détail d’un modèle permettent de mettre à l’échelle les détails d’un modèle pour les performances.
* **Le fichier source est disponible ?**
  * En général ne pas inclus avec [Unity Asset Store](https://www.assetstore.unity3d.com/) , mais il est toujours inclus dans les services tels que [TurboSquid](http://www.turbosquid.com/).
  * Sans le fichier source, vous ne pourrez pas modifier l’élément multimédia.
  * Assurez-vous que le fichier source fourni peut être importé par vos outils 3D.
* **Savoir à quoi vous vous engagez**
  * Animations sont fournies ?
  * Veillez à vérifier la liste de contenu de la ressource que vous achetez.

### <a name="porting-assets"></a>Portage des ressources

Dans certains cas vous devez transmettre des ressources existantes qui ont été initialement générées pour les autres appareils et les différentes applications. Dans la plupart des cas, ces ressources peuvent être convertis aux formats compatibles avec le moteur de graphiques à l’aide de leur application.

Lors du portage des ressources à utiliser dans votre application de HoloLens, vous devez demander ce qui suit :
* **Vous importez directement ou ne doivent pas être converti en un autre format ?** Vérifiez le format que vous importez avec le moteur de graphiques que vous utilisez.
* **Si la conversion vers un format compatible est perdu quoi que ce soit ?** Parfois, les détails peuvent être perdues ou l’importation peut entraîner des artefacts devant être nettoyées dans un outil de création de 3D.
* **What ' s les triangles / nombre de polygones de la ressource ?** En fonction du budget pour l’application que vous pouvez utiliser [Simplygon](https://www.simplygon.com/) ou des outils similaires à Décimer (manuellement ou procédurale réduction du nombre de poly) la ressource d’origine pour s’ajuster au budget de vos applications.

### <a name="outsourcing-assets"></a>Ressources de l’externalisation

Une autre option pour les grands projets qui requièrent plus de ressources que votre équipe est équipé pour créer consiste à externaliser la création des éléments multimédias. Le processus de l’externalisation consiste à trouver le studio droit ou une agence spécialisée dans les ressources de l’externalisation. Cela peut être l’option la plus coûteuse mais également le plus flexible dans ce que vous obtenez.
* **Définir clairement ce que vous demandez.**
  * Fournissez autant de détails que possible
  * Avant, de côté et images de concept de serveur
  * Ressource de montrant art de référence dans le contexte
  * Mise à l’échelle de l’objet (généralement spécifié en centimètres)
* **Fournir un Budget**
  * Plage du nombre POLY
  * Nombre de textures
  * Type de Nuancier (pour Unity et HoloLens, vous devez toujours par défaut des shaders mobiles tout d’abord)
* **Comprendre les coûts**
  * Quelle est la stratégie de l’externalisation des demandes de modification ?

Externalisation peut fonctionner très bien selon votre chronologie de projets, mais nécessite plus de supervision pour garantir que vous obtenez les ressources critiques, que vous devez la première fois.
