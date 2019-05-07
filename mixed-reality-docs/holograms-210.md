---
title: Entrée M. 210 - regards
description: Suivez cette procédure pas à pas à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des regards concepts de codage.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, tutorial, gaze
ms.openlocfilehash: 076314389ec5ed70347c26d50c6a993f55da0758
ms.sourcegitcommit: aa88f6b42aa8d83e43104b78964afb506a368fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/02/2019
ms.locfileid: "64993545"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

# <a name="mr-input-210-gaze"></a>Entrée M. 210 : Pointage du regard

[Utilisation](gaze.md) est la première forme d’entrée et révèle intention et la reconnaissance de l’utilisateur. MR entrée 210 (également appelé Explorateur de projets) est une connaissance approfondie des concepts liés à regards pour la réalité mixte de Windows. Nous ajouterons une reconnaissance contextuelle et notre curseur hologrammes, tirant pleinement parti de ce que votre application connaît des regards de l’utilisateur.

>[!VIDEO https://www.youtube.com/embed/yKAttGduVp0]

Nous avons un astronaut convivial ici pour vous aider à apprendre les concepts du pointage de regard. Dans [101 des principes fondamentaux de M.](holograms-101.md), nous avions un curseur simple qui suivi simplement votre regard. Aujourd'hui, nous voit passer une étape au-delà du simple curseur :

* Nous simplifions le curseur et nos hologrammes prenant en charge les regards : les deux changent en fonction où l’utilisateur recherche - ou où l’utilisateur est *pas* recherche. Cela les rend sensible au contexte.
* Nous allons ajouter des commentaires et notre curseur hologrammes pour donner à l’utilisateur plus de contexte sur ce qui est ciblé. Ces commentaires peuvent être audio et visuels.
* Nous allons vous montrer des techniques de ciblage pour aider les utilisateurs à atteindre des objectifs plus petits.
* Nous allons vous montrer comment attirer l’attention de l’utilisateur sur votre hologrammes avec un indicateur d’orientation.
* Apprenez les techniques à prendre votre hologrammes avec l’utilisateur, car elle ne se déplace dans le monde.

>[!IMPORTANT]
>Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrés à l’aide d’une version antérieure de Unity et le Kit de ressources de réalité mixte. Tandis que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des éléments visuels dans les vidéos correspondantes qui sont obsolètes. Les vidéos restent inclus éternellement et car couvert les concepts s’appliquent toujours.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>Entrée M. 210 : Pointage du regard</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).
* Base C# possibilité de programmation.
* Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-210-Gaze.zip) requise par le projet. Nécessite Unity 2017.2 ou version ultérieure.
* Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.

>[!NOTE]
>Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze).

### <a name="errata-and-notes"></a>Errata et remarques

* Dans Visual Studio, « Uniquement mon Code » doit être désactivé (décoché) sous Outils -> Options -> débogage afin d’atteindre des points d’arrêt dans votre code.

## <a name="chapter-1---unity-setup"></a>Chapitre 1 - le programme d’installation Unity

>[!VIDEO https://www.youtube.com/embed/_Ccn6riQ6vU]

### <a name="objectives"></a>Objectifs

* Optimiser Unity pour le développement de HoloLens.
* Importer les ressources et le programme d’installation de la scène.
* Afficher l’astronautes dans la HoloLens.

### <a name="instructions"></a>Instructions

1. Démarrez Unity.
2. Sélectionnez **nouveau projet**.
3. Nommez le projet **ModelExplorer**.
4. Entrez l’emplacement que le **les regards** dossier vous précédemment non archivés.
5. Assurez-vous que le projet est défini sur **3D**.
6. Cliquez sur **créer le projet**.

### <a name="unity-settings-for-hololens"></a>Paramètres de Unity pour HoloLens

Nous devons informer Unity que l’application que nous tentons de les exporter doit créer un [vue immersive](app-views.md) au lieu d’une vue en 2D. Nous le faire en ajoutant HoloLens comme un périphérique de réalité virtuelle.

1. Accédez à **Modifier > Paramètres du projet > Lecteur**.
2. Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez le **Windows Store** icône.
3. Développez le **XR paramètres** groupe.
4. Dans le **rendu** section, vérifiez le **virtuel pris en charge de réalité** case à cocher pour ajouter un nouveau **SDK de réalité virtuelle** liste.
5. Vérifiez que **Windows Mixed Reality** apparaît dans la liste. Dans le cas contraire, sélectionnez le **+** bouton en bas de la liste et choisissez **Windows HOLOGRAPHIQUE**.

Ensuite, nous devons définir notre principal script vers .NET.

1. Accédez à **Modifier > Paramètres du projet > Lecteur** (que vous deviez toujours cette à partir de l’étape précédente).
2. Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez le **Windows Store** icône.
3. Dans le **autres paramètres** Configuration section, assurez-vous que l’option **Backend Scripting** a la valeur **.NET**

Enfin, nous mettrons à jour nos paramètres de qualité pour accélérer les performances sur HoloLens.

1. Accédez à **Modifier > Paramètres du projet > qualité**.
2. Cliquez sur la flèche vers le bas dans la **par défaut** ligne sous l’icône du Windows Store.
3. Sélectionnez **très faible** pour **applications du Windows Store**.

### <a name="import-project-assets"></a>Importer des éléments de projet

1. Bouton droit sur le **actifs** dossier dans le **projet** Panneau de configuration.
2. Cliquez sur **importer un Package > Package personnalisé**.
3. Accédez aux fichiers de projet que vous avez téléchargé, puis cliquez sur **ModelExplorer.unitypackage**.
4. Cliquez sur **Ouvrir**.
5. Une fois le package chargé, cliquez sur le **importation** bouton.

### <a name="setup-the-scene"></a>Le programme d’installation de la scène

1. Dans la hiérarchie, supprimez le **Main Camera**.
2. Dans le **HoloToolkit** dossier, ouvrez le **entrée** dossier, puis ouvrez le **Prefabs** dossier.
3. Faites glisser et déposez le **MixedRealityCameraParent** prefab à partir de la **Prefabs** dossier vers le **hiérarchie**.
4. Cliquez sur le **lumière directionnelle** dans la hiérarchie et choisissez **supprimer**.
5. Dans le **Vntana** dossier, faites glisser et déposez les ressources suivantes dans la racine de la **hiérarchie**:
    * **AstroMan**
    * **lumières**
    * **SpaceAudioSource**
    * **SpaceBackground**
6. Démarrer **Mode lecture** ▶ pour afficher l’astronautes !.
7. Cliquez sur **Mode lecture** ▶ à nouveau à **arrêter**.
8. Dans le **hologrammes** dossier, rechercher le **Fitbox** asset et faites-le glisser vers la racine de la **hiérarchie**.
9. Sélectionnez le **Fitbox** dans le **hiérarchie** Panneau de configuration.
10. Faites glisser le **AstroMan** collection à partir de la **hiérarchie** à la **hologramme Collection** propriété de la Fitbox dans le **inspecteur** panneau.

### <a name="save-the-project"></a>Enregistrer le projet

1. Enregistrer la nouvelle scène : **Fichier > Enregistrer la scène sous**.
2. Cliquez sur **nouveau dossier** et nommez le dossier **scènes**.
3. Nommez le fichier «**ModelExplorer**» et l’enregistrer dans le **scènes** dossier.

### <a name="build-the-project"></a>Générez le projet

1. Dans Unity, sélectionnez **fichier > Paramètres de Build**.
2. Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.
3. Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.
4. Si vous développez en particulier pour HoloLens, définissez **appareil cible** à **HoloLens**. Dans le cas contraire, laissez-le sur **n’importe quel appareil**.
5. Vérifiez **Type Build** a la valeur **D3D** et **SDK** a la valeur **dernière installé** (qui doit être SDK 16299 ou une version ultérieure).
6. Cliquez sur **Build**.
7. Créer un **nouveau dossier** nommé « Application ».
8. Clic le **application** dossier.
9. Appuyez sur **sélectionnez dossier**.

Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.

1. Ouvrez le **application** dossier.
2. Ouvrez le **ModelExplorer Visual Studio Solution**.

Si le déploiement sur HoloLens :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x86**.
2. Cliquez sur la flèche déroulante en regard du bouton de l’ordinateur Local, puis sélectionnez **Machine distante**.
3. Entrez **votre adresse IP du périphérique HoloLens** et définir le Mode d’authentification **universel (protocole non chiffré)**. Cliquez sur **Sélectionner**. Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées**.
4. Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**. S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device-hololens).
5. Lorsque l’application a été déployée, faire disparaître le **Fitbox** avec un **sélectionnez mouvement**.

Si le déploiement sur un casque immersif :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x64**.
2. Assurez-vous que la cible de déploiement est définie sur **ordinateur Local**.
3. Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.
4. Lorsque l’application a été déployée, faire disparaître le **Fitbox** en extrayant le déclencheur sur un contrôleur de mouvement.

## <a name="chapter-2---cursor-and-target-feedback"></a>Chapitre 2 - commentaires curseur et la cible

>[!VIDEO https://www.youtube.com/embed/S24u0V_T7ZI]

### <a name="objectives"></a>Objectifs

* Conception visuelle du curseur et le comportement.
* Curseur du pointage de regard.
* Commentaires de hologramme basée sur des regards.

Nous allons notre travail de base sur quelques principes de conception de curseur, à savoir :

* Le curseur est toujours présent.
* Ne laissez pas le curseur obtenir trop petite ou grande.
* Évitez l’obstruction de contenu.

### <a name="instructions"></a>Instructions

1. Dans le **HoloToolkit\Input\Prefabs** dossier, recherchez le **InputManager** actif.
2. Faites glisser et déposez le **InputManager** sur le **hiérarchie**.
3. Dans le **HoloToolkit\Input\Prefabs** dossier, recherchez le **curseur** actif.
4. Faites glisser et déposez le **curseur** sur le **hiérarchie**.
5. Sélectionnez le **InputManager** de l’objet dans le **hiérarchie**.
6. Faites glisser le **curseur** à partir de l’objet le **hiérarchie** dans le InputManager **SimpleSinglePointerSelector**de **curseur** champ, à la en bas de la **inspecteur**.

![Configuration de sélecteur de pointeur unique simple](images/holograms210-ssps.png)

### <a name="build-and-deploy"></a>Générer et déployer

1. Régénérer l’application à partir de **fichier > Paramètres de Build**.
2. Ouvrez le **dossier application**.
3. Ouvrez le **ModelExplorer Visual Studio Solution**.
4. Cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.
5. Observez comment le curseur est dessiné, et comment elles évoluent apparence si elle est toucher un hologramme.

### <a name="instructions"></a>Instructions

1. Dans le **hiérarchie** volet, développez le **AstroMan**->**GEO_G**->**Back_Center** objet.
2. Double-cliquez sur **Interactible.cs** pour l’ouvrir dans Visual Studio.
3. Ne pas commenter les lignes dans le **IFocusable.OnFocusEnter()** et **IFocusable.OnFocusExit()** rappels dans **Interactible.cs**. Ceux-ci sont appelées par InputManager du Toolkit de réalité mixte lorsque le focus (soit en regards ou en pointant de contrôleur) entre et sort des collider du GameObject spécifique.

```cs
/* TODO: DEVELOPER CODING EXERCISE 2.d */

void IFocusable.OnFocusEnter()
{
    for (int i = 0; i < defaultMaterials.Length; i++)
    {
        // 2.d: Uncomment the below line to highlight the material when gaze enters.
        defaultMaterials[i].EnableKeyword("_ENVIRONMENT_COLORING");
    }
}

void IFocusable.OnFocusExit()
{
    for (int i = 0; i < defaultMaterials.Length; i++)
    {
        // 2.d: Uncomment the below line to remove highlight on material when gaze exits.
        defaultMaterials[i].DisableKeyword("_ENVIRONMENT_COLORING");
    }
}
```

>[!NOTE]
>Nous utilisons `EnableKeyword` et `DisableKeyword` ci-dessus. Afin de rendre utiliser ces éléments dans votre propre application avec nuanceur Standard de la boîte à outils, vous devrez suivre la [les instructions permettant d’accéder aux documents via un script Unity](https://docs.unity3d.com/Manual/MaterialsAccessingViaScript.html). Dans ce cas, nous avons déjà inclus le [trois variantes de matériau en surbrillance](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze/Completed/ModelExplorer/Assets/Resources/Models/AstroMan/Materials) nécessaires dans le dossier de ressources (recherchez les trois documents avec mise en surbrillance dans le nom).

### <a name="build-and-deploy"></a>Générer et déployer

1. Comme précédemment, générez le projet et déployer sur le HoloLens.
2. Observez que se passe-t-il lorsque les regards vise à un objet et quand il n’est pas.

## <a name="chapter-3---targeting-techniques"></a>Chapitre 3 - Techniques de ciblage

>[!VIDEO https://www.youtube.com/embed/TFnuLva4VJ0]

### <a name="objectives"></a>Objectifs

* Faciliter les hologrammes cible.
* Stabilisez les mouvements de la tête naturelles.

### <a name="instructions"></a>Instructions

1. Dans le **hiérarchie** Panneau de configuration, sélectionnez le **InputManager** objet.
2. Dans le **inspecteur** panneau, recherchez le **les regards de stabilisation** script. Cliquez dessus pour l’ouvrir dans Visual Studio, si vous souhaitez jeter un coup de œil.
    * Ce script effectue une itération sur les échantillons de données de Raycast et vous aide à stabiliser les regards de l’utilisateur pour le ciblage de précision.
3. Dans le **inspecteur**, vous pouvez modifier le **stockées des exemples de la stabilité** valeur. Cette valeur représente le nombre d’échantillons qui la stabilisation effectue une itération à calculer la valeur stabilisée.

## <a name="chapter-4---directional-indicator"></a>Chapitre 4 - indicateur directionnel

>[!VIDEO https://www.youtube.com/embed/htVbJCMlj64]

### <a name="objectives"></a>Objectifs

* Ajouter un indicateur directionnel sur le curseur pour aider à trouver hologrammes.

### <a name="instructions"></a>Instructions

Nous allons utiliser le **DirectionIndicator.cs** fichier qui contiendra :

1. Afficher l’indicateur directionnel si l’utilisateur n’est pas gazing aux hologrammes.
2. Masquer l’indicateur directionnel si l’utilisateur est gazing aux hologrammes.
3. Mettre à jour l’indicateur directionnel pour pointer vers les hologrammes.

Commençons.

1. Cliquez sur le **AstroMan** de l’objet dans le **hiérarchie** panneau et **cliquez sur la flèche** pour le développer.
2. Dans le **hiérarchie** Panneau de configuration, sélectionnez le **DirectionalIndicator** objet sous **AstroMan**.
3. Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.
4. Dans le menu, tapez dans la zone de recherche **indicateur de Direction**. Sélectionnez le résultat de recherche.
5. Dans le **hiérarchie** volet, faites glisser le **curseur** de l’objet sur le **curseur** propriété dans le **inspecteur**.
6. Dans le **projet** volet le **hologrammes** dossier, faites glisser et déposez le **DirectionalIndicator** actif sur le **indicateur directionnel**propriété dans le **inspecteur**.
7. Générez et déployez l’application.
8. Regardez la façon dont l’objet de l’indicateur directionnel vous permet de trouver l’astronautes !.

## <a name="chapter-5---billboarding"></a>Chapitre 5 - le Billboarding

>[!VIDEO https://www.youtube.com/embed/qFiLr_LUACE]

### <a name="objectives"></a>Objectifs

* Utilisez le billboarding avoir hologrammes toujours faire face vers vous.

Nous allons utiliser le **Billboard.cs** à conserver un GameObject orientée services de sorte qu’il est accessible sur l’utilisateur à tout moment.

1. Dans le **hiérarchie** Panneau de configuration, sélectionnez le **AstroMan** objet.
2. Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.
3. Dans le menu, tapez dans la zone de recherche **Billboard**. Sélectionnez le résultat de recherche.
4. Dans le **inspecteur** définir le **axe de tableau croisé dynamique** à **Y**.
5. Essayez ! Générer et déployer l’application comme avant.
6. Voir comment l’objet Billboard faces, quel que soit la façon dont vous modifiez le point de vue.
7. Supprimez le script à partir de la **AstroMan** pour l’instant.

## <a name="chapter-6---tag-along"></a>Chapitre 6 - Tag-Along

>[!VIDEO https://www.youtube.com/embed/Ct8ORZAX5JU]

### <a name="objectives"></a>Objectifs

* Utilisez Tag-Along pour que notre hologrammes Suivez-nous autour de la pièce.

Car nous travaillons à ce problème, nous allons guidées par les contraintes de conception suivantes :

* Contenu doit toujours être un coup de œil de suite.
* Contenu ne doit pas être de la façon.
* Verrouillage de tête le contenu est désagréable.

La solution utilisée ici est d’utiliser une approche « tag-along ».

Un objet tag-along quitte jamais complètement la vue de l’utilisateur. Vous pouvez considérer l’un tag-along comme étant un objet attaché à la tête de l’utilisateur par élastiques. Lorsque l’utilisateur se trouve, le contenu reste au sein d’un simple coup de œil en faisant glisser vers le bord de la vue sans quitter complètement. Lorsque l’utilisateur son rapprocher de l’objet tag-along, il s’agit plus en détail dans la vue.

Nous allons utiliser le **SimpleTagalong.cs** fichier qui contiendra :

1. Détermine si l’objet Tag-Along dans les limites de l’appareil photo.
2. Si ce n’est pas le cas dans le frustum vue, placer le Tag-Along à partiellement dans frustum de la vue.
3. Sinon, positionnez le Tag-Along à une distance par défaut à partir de l’utilisateur.

Pour ce faire, nous devons changiez le **Interactible.cs** script pour appeler le **TagalongAction**.

1. Modifier **Interactible.cs** en effectuant le codage exercice 6.a (suppression de commentaires dans les lignes 84 à 87).

```cs
/* TODO: DEVELOPER CODING EXERCISE 6.a */
// 6.a: Uncomment the lines below to perform a Tagalong action.
if (interactibleAction != null)
{
    interactibleAction.PerformAction();
}
```

Le **InteractibleAction.cs** script, associé au **Interactible.cs** effectue des actions personnalisées lorsque vous appuyez sur hologrammes. Dans ce cas, nous utiliserons un en particulier pour tag-along.

* Dans le **Scripts** dossier, cliquez sur **TagalongAction.cs** asset pour ouvrir dans Visual Studio.
* Terminer l’exercice de codage ou le remplacer par ceci :
  * En haut de la **hiérarchie**, dans le type de barre de recherche **ChestButton_Center** et sélectionnez le résultat.
  * Dans le **inspecteur** du panneau, cliquez sur le **ajouter un composant** bouton.
  * Dans le menu, tapez dans la zone de recherche **accompagnent Action**. Sélectionnez le résultat de recherche.
  * Dans **Vntana** dossier rechercher la **accompagnent** actif.
  * Sélectionnez le **ChestButton_Center** de l’objet dans le **hiérarchie**. Faites glisser et déposez le **accompagnent** à partir de l’objet le **projet** panneau sur le **inspecteur** dans le **objet à accompagnent** propriété.
  * Faites glisser le **accompagnent Action** à partir de l’objet le **inspecteur** dans le **Action Interactible** champ sur le **Interactible** script.
* Double-cliquez sur le **TagalongAction** script pour l’ouvrir dans Visual Studio.

![Configuration interactible](images/holograms210-interactible.png)

Nous devons ajouter les éléments suivants :

* Ajouter des fonctionnalités à la fonction PerformAction dans le script TagalongAction (héritée de InteractibleAction).
* Ajoutez le billboarding à l’objet gazed sur et la valeur de l’axe de tableau croisé dynamique XY.
* Ajoutez ensuite Tag-Along simple à l’objet.

Voici notre solution, à partir de **TagalongAction.cs**:

```cs
// Copyright (c) Microsoft Corporation. All rights reserved.
// Licensed under the MIT License. See LICENSE in the project root for license information.

using HoloToolkit.Unity;
using UnityEngine;

public class TagalongAction : InteractibleAction
{
    [SerializeField]
    [Tooltip("Drag the Tagalong prefab asset you want to display.")]
    private GameObject objectToTagalong;

    private void Awake()
    {
        if (objectToTagalong != null)
        {
            objectToTagalong = Instantiate(objectToTagalong);
            objectToTagalong.SetActive(false);

            /* TODO: DEVELOPER CODING EXERCISE 6.b */

            // 6.b: AddComponent Billboard to objectToTagAlong,
            // so it's always facing the user as they move.
            Billboard billboard = objectToTagalong.AddComponent<Billboard>();

            // 6.b: AddComponent SimpleTagalong to objectToTagAlong,
            // so it's always following the user as they move.
            objectToTagalong.AddComponent<SimpleTagalong>();

            // 6.b: Set any public properties you wish to experiment with.
            billboard.PivotAxis = PivotAxis.XY; // Already the default, but provided in case you want to edit
        }
    }

    public override void PerformAction()
    {
        // Recommend having only one tagalong.
        if (objectToTagalong == null || objectToTagalong.activeSelf)
        {
            return;
        }

        objectToTagalong.SetActive(true);
    }
}
```

* Essayez ! Générez et déployez l’application.
* Regardez comment le contenu suit le centre du point du pointage de regard, mais pas en permanence et sans blocage.
