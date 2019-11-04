---
title: Processus de création de ressources
description: Aide sur la création de ressources pour les expériences de réalité mixte.
author: shengkait
ms.author: shentan
ms.date: 03/21/2018
ms.topic: article
keywords: actif, création, processus, budget, polygones, textures, nuanceurs, performances
ms.openlocfilehash: fb8266a018e11a8fb944819a0cac5ace38f2cb25
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437003"
---
# <a name="asset-creation-process"></a>Processus de création de ressources

Windows Mixed Reality s’appuie sur les dizaines d’investissements réalisés par Microsoft dans DirectX. Cela signifie que toutes les expériences et compétences dont les développeurs ont besoin pour créer des graphiques 3D continuent à être utiles avec HoloLens.

Les ressources que vous créez pour un projet sont disponibles dans de nombreux formulaires et formes. Ils peuvent être constitués d’une série de textures/images, d’audio, de vidéo, de modèles 3D et d’animations. Nous ne pouvons pas commencer à couvrir tous les outils qui sont disponibles pour créer les différents types de ressources utilisés dans un projet. Pour cet article, nous allons nous concentrer sur les méthodes de création de ressources en 3D.

![concept, création, intégration et](images/concept-creation-integration-iteration-flow-640px.jpg) de workflow des itérations<br>
*Concept, création, intégration et déroulement des itérations*

## <a name="things-to-consider"></a>Points à prendre en considération

Lorsque vous examinez l’expérience que vous essayez de créer, pensez-y comme un **budget** que vous pouvez consacrer à essayer de créer la meilleure expérience. Il n’y a pas obligatoirement de limites imposées sur le nombre de **polygones** ou **de types d'** utilisation de matériaux dans vos ressources, mais plus un ensemble budgétaire de compromis.

Vous trouverez ci-dessous un exemple de budget pour votre expérience. En règle générale, les performances ne sont pas un point de défaillance unique, mais une mort de mille fois par se.
<br>

<table style="float:right; margin-left: 10px;">
<tr>
<th style="text-align:left;"><b>Ressources</b></th><th style="text-align:right;"> CPU</th><th> Processeur graphique</th><th> Mémoire</th>
</tr><tr>
<td> Polygones</td><td> entre</td><td> 5,5</td><td> 10</td>
</tr><tr>
<td> Textures</td><td> 5,5</td><td> 4,5</td><td>25 %</td>
</tr><tr>
<td> Nuanceurs</td><td> 4,5</td><td> 35%</td><td> entre</td>
</tr><tr>
<td> <b>Dynamiques</b></td><td></td><td></td><td></td>
</tr><tr>
<td> Physique</td><td> 5,5</td><td> 4,5</td><td> entre</td>
</tr><tr>
<td> Éclairage en temps réel</td><td> 10</td><td> entre</td><td> entre</td>
</tr><tr>
<td> Média (audio/vidéo)</td><td> -</td><td> 4,5</td><td> 25 %</td>
</tr><tr>
<td> Script/logique</td><td> 25 %</td><td> entre</td><td> 5,5</td>
</tr><tr>
<td> Surcharge générale</td><td> 5,5</td><td> 5,5</td><td> 5,5</td>
</tr><tr>
<td> <b>Nombre</b></td><td> <b>65%</b></td><td> <b>90%</b></td><td> <b>70%</b></td>
</tr>
</table>

**Nombre total de ressources**
* Combien de ressources sont actives dans la scène ?

**Complexité des ressources**
* Combien de triangles/polygones ?
* Quel est le degré de complexité du nuanceur ? Lors de l’utilisation de la boîte à outils de réalité mixte, il est recommandé d’utiliser le [nuanceur standard Mixed Reality Toolkit standard](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_MRTKStandardShader.md) pour réduire la complexité des nuanceurs.

Les développeurs et les artistes doivent prendre en compte les fonctionnalités de l’appareil et du moteur graphique. Microsoft HoloLens dispose de toutes les fonctionnalités de calcul et de graphique intégrées à l’appareil. Il partage les fonctionnalités que les développeurs trouveraient sur une plate-forme mobile.

Le processus de création des ressources est le même, que vous cibliez ou non une expérience pour un [appareil holographique ou un appareil immersif](mixed-reality.md#the-mixed-reality-spectrum). La principale chose à noter est la capacité de l’appareil, comme indiqué ci-dessus, ainsi que la mise à l’échelle puisque vous pouvez voir le monde réel en réalité mixte, vous souhaiterez conserver l’échelle appropriée en fonction de l’expérience. 

## <a name="authoring-assets"></a>Création de ressources

Nous allons commencer par les moyens d’obtenir des ressources pour votre projet :
1. Création de ressources (outils de création et capture d’objets)
2. Achats d’actifs (achat de ressources en ligne)
3. Portage des ressources (en tenant des ressources existantes)
4. Externalisation des ressources (importation de ressources des tiers)

### <a name="creating-assets"></a>Création de ressources

**Outils de création**<br>
Tout d’abord, vous pouvez créer vos propres ressources de plusieurs façons. les artistes 3D utilisent un certain nombre d’applications et d’outils pour créer des modèles qui se composent de **maillages**, de **textures**et de **matériaux**. Il est ensuite enregistré dans un format de fichier qui peut être importé ou utilisé par le moteur graphique utilisé par l’application, par exemple **. FBX** ou **. OBJ**. Tout outil qui génère un modèle pris en charge par le moteur graphique que vous avez choisi fonctionnera sur **HoloLens**. Parmi les artistes en 3D, beaucoup choisissent d’utiliser les [Maya de Autodesk qui peuvent lui-même utiliser HoloLens](https://www.youtube.com/watch?v=q0K3n0Gf8mA) pour transformer la façon dont les ressources sont créées. Si vous souhaitez obtenir un résultat rapide, vous pouvez également utiliser le [Générateur 3D](https://developer.microsoft.com/windows/hardware/3d-print/3d-builder-resources) fourni avec Windows pour l’exportation. OBJ à utiliser dans votre application.

**Capture d’objets**<br>
Vous pouvez également capturer des objets en 3D. La capture d’objets inanimés en 3D et leur modification avec le logiciel de création de contenu numérique sont de plus en plus populaires avec la hausse de l’impression en 3D. À l’aide du capteur **Kinect 2** et du [Générateur 3D](https://developer.microsoft.com/windows/hardware/3d-print/3d-builder-resources) , vous pouvez utiliser la fonctionnalité de capture pour créer des ressources à partir d’objets réels. Il s’agit également d’une [suite d’outils](https://en.wikipedia.org/wiki/Comparison_of_photogrammetry_software) permettant de faire de même avec **Photogrammetry** en traitant un certain nombre d’images pour assembler et mailler les textures.

### <a name="purchasing-assets"></a>Achats d’actifs

Une autre option idéale consiste à acheter des ressources pour votre expérience. Il existe une multitude d’actifs disponibles par le biais de services tels que le [magasin d’actifs Unity](https://www.assetstore.unity3d.com/) ou [Turbosquid](https://www.turbosquid.com/) .

Lorsque vous achetez des actifs auprès d’un tiers, vous devez toujours vérifier les éléments suivants :
* **Quel est le nombre de poly ?**
  * Est-il adapté à votre budget ?
* **Existe-t-il des niveaux de détail (LODs) pour le modèle ?**
  * Le niveau de détail d’un modèle vous permet de mettre à l’échelle les détails d’un modèle pour des performances optimales.
* **Le fichier source est-il disponible ?**
  * Généralement non inclus dans le [magasin d’actifs Unity](https://www.assetstore.unity3d.com/) , mais toujours inclus avec des services tels que [Turbosquid](https://www.turbosquid.com/).
  * Sans le fichier source, vous ne pourrez pas modifier la ressource.
  * Assurez-vous que le fichier source fourni peut être importé par vos outils 3D.
* **Savoir ce que vous obtenez**
  * Les animations sont-elles fournies ?
  * Veillez à consulter la liste de contenu de l’élément multimédia que vous achetez.

### <a name="porting-assets"></a>Portage de ressources

Dans certains cas, vous allez créer des ressources existantes qui ont été créées à l’origine pour d’autres appareils et différentes applications. Dans la plupart des cas, ces ressources peuvent être converties en formats compatibles avec le moteur graphique utilisé par leur application.

Lors du Portage des ressources à utiliser dans votre application HoloLens, vous devez demander ce qui suit :
* **Pouvez-vous importer directement ou doit être converti vers un autre format ?** Vérifiez le format que vous importez avec le moteur graphique que vous utilisez.
* **Si la conversion vers un format compatible est-elle perdue ?** Parfois, les détails peuvent être perdus ou les importations peuvent entraîner des artefacts qui doivent être nettoyés dans un outil de création 3D.
* **Quel est le nombre d’éléments triangulaires/polygones de l’élément multimédia ?** En fonction du budget de votre application, vous pouvez utiliser [Simplygon](https://www.simplygon.com/) ou des outils similaires pour décimer (réduire de manière manuelle ou manuelle le chiffrement poly) la ressource d’origine pour l’adapter au budget de vos applications.

### <a name="outsourcing-assets"></a>Ressources en External

Une autre option pour les projets plus volumineux qui requièrent plus de ressources que votre équipe est équipée pour la création consiste à externaliser la création d’actifs. Le processus d’externalisation consiste à trouver le Studio ou l’Agence approprié qui est spécialisé dans l’externalisation des ressources. Il peut s’agir de l’option la plus coûteuse, mais également de la plus souple dans ce que vous recevez.
* **Définissez clairement ce que vous demandez**
  * Fournir autant de détails que possible
  * Images de concept avant, arrière et arrière
  * Illustration de référence présentant un élément multimédia en contexte
  * Mise à l’échelle de l’objet (généralement spécifiée en centimètres)
* **Fournir un budget**
  * Plage de nombres poly
  * Nombre de textures
  * Type de nuanceur (pour Unity et HoloLens, vous devez toujours d’abord par défaut les nuanceurs mobiles)
* **Comprendre les coûts**
  * Quelle est la stratégie d’externalisation pour les demandes de modification ?

L’externalisation peut fonctionner très bien en fonction de la chronologie de vos projets, mais elle nécessite plus de supervision pour garantir que vous disposez des ressources dont vous avez besoin pour la première fois.
