---
title: Étude de cas - HoloSketch de génération, une disposition spatiale et un UX esquisse d’application pour HoloLens
description: HoloSketch est disposition spatiale sur l’appareil et l’expérience utilisateur esquisse outil pour HoloLens aider à créer des expériences HOLOGRAPHIQUE.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: HoloSketch, HoloLens, Windows Mixed Reality, esquisse, application
ms.openlocfilehash: d7f94a09bf4a8a16000c2345adf1a046dab4bd15
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594279"
---
# <a name="case-study---building-holosketch-a-spatial-layout-and-ux-sketching-app-for-hololens"></a>Étude de cas - HoloSketch de génération, une disposition spatiale et un UX esquisse d’application pour HoloLens

HoloSketch est disposition spatiale sur l’appareil et l’expérience utilisateur esquisse outil pour HoloLens aider à créer des expériences HOLOGRAPHIQUE. HoloSketch fonctionne avec un commandes de clavier et souris ainsi que gestuelle et vocale Bluetooth couplé. HoloSketch vise à fournir un outil de mise en page de l’expérience utilisateur simple pour l’itération et de visualisation rapide.

![HoloSketch : Une disposition spatiale et un UX esquisse d’application pour HoloLens.](images/holosketch-image-01-640px.png)<br>
*HoloSketch : disposition spatiale et l’expérience utilisateur esquisse d’application pour HoloLens*

![Un simple outil de disposition de l’expérience utilisateur visualisation rapide et une itération.](images/holosketch-image-02.png)<br>
*Un outil de mise en page de l’expérience utilisateur simple visualisation rapide et une itération*

## <a name="features"></a>Fonctionnalités

### <a name="primitives-for-quick-studies-and-scale-prototyping"></a>Primitives pour les études rapide et mise à l’échelle-prototypage

![À l’aide de formes primitifs](images/holosketch-primitives-giphy.gif)

Utiliser des formes primitifs pour études massing rapides et mise à l’échelle-prototypage.

### <a name="import-objects-through-onedrive"></a>Importer des objets via OneDrive

![l’importation d’objets](images/holosketch-importobjects-giphy.gif)

Importer des images PNG/JPG ou objets FBX 3D (nécessite l’empaquetage dans Unity) dans l’espace de réalité mixte via OneDrive.

### <a name="manipulate-objects"></a>Manipuler des objets

![manipulation des objets](images/manipulate-objects-640px.jpg)

Manipuler des objets (déplacement/faire pivoter/mise à l’échelle) avec une interface familière objet 3D.

### <a name="bluetooth-mousekeyboard-gestures-and-voice-commands"></a>Bluetooth, clavier/souris, mouvements et les commandes vocales

![prend en charge de Bluetooth](images/supports-bluetooth-640px.jpg)

HoloSketch prend en charge clavier/souris Bluetooth, les mouvements et les commandes vocales.

## <a name="background"></a>Arrière-plan

### <a name="importance-of-experiencing-your-design-in-the-device"></a>Importance de rencontre votre conception de l’appareil

Lorsque vous concevez quelque chose pour HoloLens, il est important profiter de votre conception de l’appareil. Un des plus grands défis dans la conception d’applications de réalité mixte est qu’il est difficile d’obtenir le sens de mise à l’échelle, de position et de profondeur, en particulier par le biais des croquis 2D traditionnels.

### <a name="cost-of-2d-based-communication"></a>Communication basée sur le coût de 2D

Pour communiquer efficacement des flux de l’expérience utilisateur et des scénarios pour d’autres, un concepteur peut retrouver beaucoup de temps à créer des ressources à l’aide des outils traditionnels 2D comme Illustrator, Photoshop et PowerPoint. Ces conceptions 2D nécessitent souvent un effort supplémentaire pour les convertir en 3D. Quelques idées sont perdues dans cette traduction à partir de 2D en 3D.

### <a name="complex-deployment-process"></a>Processus de déploiement complexes

Étant donné que la réalité mixte est un nouveau canevas pour nous, elle implique un grand nombre d’itération de conception et d’essais et erreurs par sa nature. Concepteur qui ne sont pas familiers avec les outils tels que Unity et Visual Studio, il n’est pas simple de créer quelque chose dans HoloLens. En général, vous devez passer par le processus ci-dessous pour voir votre illustration 2D/3D dans l’appareil. Il s’agissait d’une barrière big pour itérer rapidement sur des idées et des scénarios de concepteurs.

![Processus de déploiement complexes](images/holosketch-image-03-1000px.png)<br>
*Processus de déploiement*

### <a name="simplified-process-with-holosketch"></a>Processus simplifié avec HoloSketch

Avec HoloSketch, nous souhaitons sans impliquer des outils de développement et le périphérique portail jumelage de simplifier ce processus. L’utilisation de OneDrive, les utilisateurs peuvent placer facilement les éléments multimédias en 2D/3D dans HoloLens.

![Processus simplifié avec HoloSketch](images/holosketch-image-04-1000px.png)<br>
*Processus simplifié avec HoloSketch*

### <a name="encouraging-three-dimensional-design-thinking-and-solutions"></a>Encourager la pensée de conception en trois dimensions et des solutions

Nous avons pensé que cet outil donnerait concepteurs une opportunité pour Explorer les solutions dans un espace tridimensionnel véritablement et ne pas être bloqué en 2D. Ils n’ont pas de réfléchir à la création d’un arrière-plan 3D pour leur interface utilisateur dans la mesure où l’arrière-plan est le monde réel dans le cas de Hololens. HoloSketch ouvre un moyen pour les concepteurs d’Explorer facilement conception 3D sur Hololens.

## <a name="get-started"></a>Prise en main

### <a name="how-to-import-2d-images-jpgpng-into-holosketch"></a>Comment importer des images 2D (JPG/PNG) dans HoloSketch

* Charger des images JPG/PNG dans votre dossier OneDrive « Documents/HoloSketch ».
* Dans le menu OneDrive HoloSketch, vous serez en mesure de sélectionner et de placer l’image dans l’environnement.

![L’importation d’images 2D](images/import-2d-images-1000px.jpg)<br>
*L’importation d’images et des objets 3D via OneDrive*

### <a name="how-to-import-3d-objects-into-holosketch"></a>Comment importer des objets 3D dans HoloSketch

Avant de charger dans votre dossier OneDrive, suivez les étapes ci-dessous pour empaqueter vos objets 3D dans un groupe de ressources Unity. À l’aide de ce processus vous pouvez importer vos fichiers FBX/OBJ contre les logiciels 3D telles que Maya, cinéma 4D et Microsoft Paint 3D.

>[!IMPORTANT]
>Actuellement, la création du regroupement actif est pris en charge avec Unity version 5.4.5f1.

1. Téléchargez et ouvrez le projet Unity ['AssetBunlder_Unity'](https://github.com/Microsoft/MRDesignLabs/tree/master/ReleasedApps/HoloSketch/AssetBundler_Unity). Ce projet Unity inclut le script pour la génération de la ressource offre groupée.
2. Créer un nouveau GameObject.
3. Nommez le GameObject en fonction du contenu.
4. Dans ce panneau, cliquez sur Ajouter un composant et ajouter « Boîte Collider ». 

   ![Dans ce panneau, cliquez sur Ajouter un composant et ajoutez « Collider case »](images/holosketch-10a-assetbundles-1000px.png)
   
   ![Dans ce panneau, cliquez sur Ajouter un composant et ajoutez « boîte Collider' #2](images/holosketch-10b-assetbundles-1000px.png)

5. Importer le fichier FBX 3D en le faisant glisser dans le panneau de configuration de projet.
6. Faites glisser l’objet dans le volet hiérarchie **sous votre nouveau GameObject**.

   ![Faites glisser l’objet dans le volet de la hiérarchie sous votre nouveau GameObject](images/holosketch-12-assetbundles-1000px.png)

7. Ajustez la dimension collider si elle ne correspond pas à l’objet. Faire pivoter l’objet pour faire face à **z**.

   ![Ajustez la dimension de collider si elle ne correspond pas à l’objet.](images/holosketch-13-assetbundles-1000px.png)

8. Faites glisser l’objet à partir du Panneau de la hiérarchie vers le panneau de projet pour **rendent prefab**.
9. Au bas de ce panneau, cliquez sur la liste déroulante, créer et affecter un nouveau nom unique. Exemple ci-dessous illustre l’ajout et l’affectation de « brownchair » pour le nom AssetBundle. 

   ![Au bas de ce panneau, cliquez sur la liste déroulante et affecter un nouveau nom unique.](images/holosketch-14-assetbundles-1000px.png)

10. Préparer une image miniature de l’objet de modèle. 
   ![Faites glisser une image dans le panneau de configuration de projet, puis attribuez le nom utilisé pour l’objet.](images/holosketch-15-assetbundles-1000px.png)

11. Créez un dossier nommé « Assetbundles » sous le dossier de « Actifs » du projet Unity.

12. Dans le menu de ressources, sélectionnez « Build AssetBundles' pour générer le fichier. 
   ![Dans le menu de ressources, sélectionnez « Build AssetBundles' pour générer le fichier.](images/holosketch-15a-assetbundles.png)


13. **Chargez le fichier généré dans le dossier /Files/Documents/HoloSketch sur OneDrive.** Téléchargez le fichier asset_unique_name uniquement. Vous n’avez pas besoin de télécharger des fichiers manifeste ou AssetBundles fichier. <br>
![Ajouter des fichiers à des fichiers/Documents/HoloSketch/dossier](images/holosketch-onedriveupload-1000px.png)
![vous verrez un objet 3D ajouté dans le menu de OneDrive de HoloSketch](images/holosketch-14-onedriveexample-1000px.jpg)

## <a name="how-to-manipulate-the-objects"></a>Comment manipuler les objets

HoloSketch prend en charge l’interface traditionnelle est largement utilisé dans les logiciels 3D. Vous pouvez utiliser le déplacement, faire pivoter, mettre à l’échelle les objets avec des mouvements et une souris. Vous pouvez rapidement basculer entre différents modes avec voix ou du clavier.

### <a name="object-manipulation-modes"></a>Modes de manipulation d’objet

![Comment manipuler les objets](images/holosketch-image-06-1000px.png)<br>
*Comment manipuler les objets*

### <a name="contextual-and-tool-belt-menus"></a>Menus contextuelles et ' s Tool Belt

**Utilisez le Menu contextuel**

Double appui pour ouvrir le Menu contextuel. 

Éléments de menu :
* **Surface de disposition :** Ceci est un système de grille 3D dans lequel vous pouvez disposer plusieurs objets et les gérer en tant que groupe. Double-appui sur la Surface de disposition pour ajouter des objets.
* **Primitives :** Utilisez des cubes, de domaines, de cylindre et de cône pour massing études.
* **OneDrive :** Ouvrez le menu OneDrive pour importer des objets.
* **Aide :** Affiche l’écran d’aide.

![Menu contextuel](images/holosketch-image-07.png)<br>
*Menu contextuel*

**L’aide du Menu de la ceinture outil**

Déplacer, faire pivoter, mettre à l’échelle, enregistrer et la scène de charge sont disponibles dans le Menu de la ceinture outil. 

## <a name="using-keyboard-gestures-and-voice-commands"></a>À l’aide du clavier, les mouvements et les commandes vocales

![Clavier, les mouvements et les commandes vocales](images/holosketch-image-08-1000px.png)<br>
*Clavier, les mouvements et les commandes vocales*

## <a name="download-the-app"></a>Télécharger l’application

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="HoloSketch app icon" width="60" height="60" src="images/holosketch-app-icon.png">
</td>
<td style="border-style: none"><a href="https://www.microsoft.com/store/p/holosketch/9p3br4t5m4tv">Téléchargez et installez l’application HoloSketch gratuitement à partir du Microsoft Store</a>
</td>
</tr>
</table>

## <a name="known-issues"></a>Problèmes connus
* Actuellement pris en charge de la création de regroupement des éléments multimédias avec **Unity version 5.4.5f1.**
* Selon la quantité de données dans votre OneDrive, l’application peut apparaître comme s’il s’est arrêté lors du chargement du contenu de OneDrive
* Actuellement, enregistrer et la fonctionnalité de chargement prend uniquement en charge les objets de type primitif
* Texte, audio, vidéo et Photo menus sont désactivés dans le menu contextuel
* Le bouton lecture dans le menu's Tool Belt efface les gizmos de manipulation

## <a name="sharing-your-sketches"></a>Partage de votre croquis

Vous pouvez utiliser la fonctionnalité d’enregistrement vidéo dans HoloLens en disant « Hey Cortana, l’enregistrement de démarrage/arrêt ». Appuyez sur le volume haut/bas clé ensemble pour prendre une photo de votre ébauche de projet.

## <a name="about-the-authors"></a>À propos des auteurs

<table style="border-collapse:collapse">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><b>Dong Yoon Park</b><br>Concepteur UX @Microsoft</td>
</tr>
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Patrick Sebring" width="60" height="60" src="images/paseb-60px.jpg"></td>
<td style="border-style: none"><b>Patrick Sebring</b><br>Développeur @Microsoft</td>
</tr>
</table> 
