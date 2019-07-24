---
title: Entrée MR 210-point de regard
description: Suivez cette procédure pas à pas de codage avec Unity, Visual Studio et HoloLens pour apprendre les détails des concepts de regard.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, point de regard
ms.openlocfilehash: 076314389ec5ed70347c26d50c6a993f55da0758
ms.sourcegitcommit: aa88f6b42aa8d83e43104b78964afb506a368fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/02/2019
ms.locfileid: "64993545"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

# <a name="mr-input-210-gaze"></a>Monsieur 210: Pointage du regard

Le point de [regard](gaze.md) est la première forme d’entrée et révèle l’intention et la sensibilisation de l’utilisateur. Monsieur l’entrée 210 (également appelée l’Explorateur de projets) est une présentation approfondie des concepts liés au regard de Windows Mixed Reality. Nous ajouterons une sensibilisation contextuelle à notre curseur et à vos hologrammes, en tirant pleinement parti de ce que votre application connaît sur le regard de l’utilisateur.

>[!VIDEO https://www.youtube.com/embed/yKAttGduVp0]

Nous disposons d’un astronautes convivial pour vous aider à apprendre les concepts de regard. Dans les [notions de base de m. 101](holograms-101.md), nous avions un curseur simple qui vient juste de vous faire suivre le regard. Aujourd’hui, nous allons déplacer une étape au-delà du curseur simple:

* Nous faisons en sorte que le curseur et nos hologrammes soient orientés vers le regard: les deux varient en fonction de la position de l’utilisateur ou de l’endroit où l’utilisateur *ne cherche pas* . Cela les rend compatibles avec le contexte.
* Nous ajouterons des commentaires à notre curseur et à vos hologrammes pour fournir à l’utilisateur davantage de contexte sur ce qui est ciblé. Ce feedback peut être audio et visuel.
* Nous allons vous montrer comment cibler des techniques pour aider les utilisateurs à atteindre des cibles plus petites.
* Nous allons vous montrer comment attirer l’attention de l’utilisateur sur vos hologrammes à l’aide d’un indicateur directionnel.
* Nous vous enseignerons les techniques permettant de faire passer vos hologrammes à l’utilisateur lorsqu’il se déplace dans votre monde.

>[!IMPORTANT]
>Les vidéos incorporées dans chacun des chapitres ci-dessous ont été enregistrées à l’aide d’une version antérieure d’Unity et de la réalité mixte Toolkit. Alors que les instructions pas à pas sont précises et actuelles, vous pouvez voir des scripts et des visuels dans les vidéos correspondantes qui sont obsolètes. Les vidéos restent incluses pour l’affiche et les concepts abordés s’appliquent toujours.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>Monsieur 210: Pointage du regard</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).
* Certaines fonctionnalités C# de programmation de base.
* Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-210-Gaze.zip) requis par le projet. Requiert Unity 2017,2 ou une version ultérieure.
* Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze).

### <a name="errata-and-notes"></a>Errata et notes

* Dans Visual Studio, l’option «Uniquement mon code» doit être désactivée (décochée) sous Outils-> Options-> le débogage pour atteindre les points d’arrêt dans votre code.

## <a name="chapter-1---unity-setup"></a>Chapitre 1-Configuration Unity

>[!VIDEO https://www.youtube.com/embed/_Ccn6riQ6vU]

### <a name="objectives"></a>Objectifs

* Optimiser Unity pour le développement HoloLens.
* Importer les ressources et configurer la scène.
* Affichez le astronautes dans HoloLens.

### <a name="instructions"></a>Instructions

1. Démarrez Unity.
2. Sélectionnez **nouveau projet**.
3. Nommez le projet **ModelExplorer**.
4. Entrez **l’emplacement** du dossier de pointage que vous avez précédemment désinstallé.
5. Vérifiez que le projet est défini sur **3D**.
6. Cliquez sur **Create Project**.

### <a name="unity-settings-for-hololens"></a>Paramètres Unity pour HoloLens

Nous devons permettre à Unity de savoir que l’application que nous essayons d’exporter doit créer une [vue immersive](app-views.md) au lieu d’une vue 2D. Pour cela, nous ajoutons HoloLens en tant qu’appareil de réalité virtuelle.

1. Accédez à **modifier > paramètres du projet > Player**.
2. Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez l’icône du **Windows Store** .
3. Développez le groupe de **paramètres XR** .
4. Dans la section **rendu** , activez la case à cocher **réalité virtuelle prise en charge** pour ajouter une nouvelle liste de **SDK de réalité virtuelle** .
5. Vérifiez que **Windows Mixed Reality** s’affiche dans la liste. Si ce n’est pas **+** le cas, sélectionnez le bouton en bas de la liste et choisissez **Windows holographique**.

Ensuite, nous devons définir notre backend de script sur .NET.

1. Accédez à **modifier > paramètres du projet > Player** (vous pouvez toujours le faire à l’étape précédente).
2. Dans le **panneau Inspecteur** pour les paramètres du lecteur, sélectionnez l’icône du **Windows Store** .
3. Dans la section configuration **des autres paramètres** , assurez-vous que le **serveur principal de script** est défini sur **.net**

Enfin, nous mettrons à jour nos paramètres de qualité pour obtenir des performances rapides sur HoloLens.

1. Accédez à **modifier > paramètres du projet > qualité**.
2. Cliquez sur la flèche pointant vers le bas dans la ligne **par défaut** sous l’icône Windows Store.
3. Sélectionnez **très faible** pour les **applications du Windows Store**.

### <a name="import-project-assets"></a>Importer des ressources de projet

1. Cliquez avec le bouton droit sur le dossier **ressources** dans le panneau **projet** .
2. Cliquez sur **Importer un package > package personnalisé**.
3. Accédez aux fichiers de projet que vous avez téléchargés, puis cliquez sur **ModelExplorer. pour Unity**.
4. Cliquez sur **Ouvrir**.
5. Une fois le package chargé, cliquez sur le bouton **Importer** .

### <a name="setup-the-scene"></a>Configurer la scène

1. Dans la hiérarchie, supprimez l' **appareil photo principal**.
2. Dans le dossier **HoloToolkit** , ouvrez le dossier **d’entrée** , puis ouvrez le dossier **Prefabs** .
3. Faites glisser et déposez le Prefab **MixedRealityCameraParent** à partir du dossier **Prefabs** dans la **hiérarchie**.
4. Cliquez avec le bouton droit sur la **lumière directionnelle** dans la hiérarchie et sélectionnez **supprimer**.
5. Dans le  dossier hologrammes, glissez-déposez les éléments suivants à la racine de la **hiérarchie**:
    * **AstroMan**
    * **Lampes**
    * **SpaceAudioSource**
    * **SpaceBackground**
6. Démarrez le **mode lecture** ▶ pour afficher le astronautes.
7. Cliquez à nouveau sur **mode lecture** ▶ pour **arrêter**.
8. Dans le  dossier hologrammes, recherchez la ressource **Fitbox** et faites-la glisser jusqu’à la racine de la **hiérarchie**.
9. Sélectionnez le **Fitbox** dans le volet de la **hiérarchie** .
10. Faites glisser la collection **AstroMan** de la **hiérarchie** vers la propriété de **collection hologramme** du Fitbox dans le panneau **inspecteur** .

### <a name="save-the-project"></a>Enregistrer le projet

1. Enregistrez la nouvelle scène: **Fichier > enregistrer la scène sous**.
2. Cliquez sur **nouveau dossier** et nommez le dossier Scenes.
3. Nommez le fichier «**ModelExplorer**» et enregistrez-le dans le dossier **scenes** .

### <a name="build-the-project"></a>Créer le projet

1. Dans Unity, sélectionnez **fichier > paramètres de build**.
2. Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.
3. Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur basculer la **plateforme**.
4. Si vous développez spécifiquement pour HoloLens, définissez **appareil cible** sur **hololens**. Dans le cas contraire, laissez-le sur **un appareil**.
5. Vérifiez que le **type de build** est défini sur **D3D** et que le **Kit de développement logiciel (SDK** ) est défini sur le **dernier installé** (qui doit être le SDK 16299 ou une version ultérieure).
6. Cliquez sur **Build**.
7. Créez un **dossier** nommé «App».
8. Cliquez sur le dossier de l' **application** .
9. Appuyez sur **Sélectionner un dossier**.

Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.

1. Ouvrez le dossier de l' **application** .
2. Ouvrez la **solution Visual Studio ModelExplorer**.

En cas de déploiement dans HoloLens:

1. À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.
2. Cliquez sur la flèche déroulante en regard du bouton ordinateur local, puis sélectionnez **ordinateur distant**.
3. Entrez **l’adresse IP de votre appareil HoloLens** et définissez le mode d’authentification sur **universel (protocole non chiffré)** . Cliquez sur **Sélectionner**. Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées**.
4. Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**. S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le coupler à [Visual Studio](using-visual-studio.md#pairing-your-device-hololens).
5. Une fois l’application déployée, ignorez le **Fitbox** avec un **mouvement Select**.

En cas de déploiement sur un casque immersif:

1. À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.
2. Assurez-vous que la cible de déploiement est définie sur **ordinateur local**.
3. Dans la barre de menus supérieure, cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
4. Une fois l’application déployée, Faites disparaître le **Fitbox** en tirant le déclencheur sur un contrôleur de mouvement.

## <a name="chapter-2---cursor-and-target-feedback"></a>Chapitre 2-commentaires sur les curseurs et les cibles

>[!VIDEO https://www.youtube.com/embed/S24u0V_T7ZI]

### <a name="objectives"></a>Objectifs

* Conception visuelle et comportement des curseurs.
* Commentaires sur le curseur orienté vers le regard.
* Commentaires sur l’hologramme en regard.

Nous allons baser notre travail sur certains principes de conception de curseur, à savoir:

* Le curseur est toujours présent.
* Ne laissez pas le curseur devenir trop petit ou grand.
* Évitez d’obstruer le contenu.

### <a name="instructions"></a>Instructions

1. Dans le dossier **HoloToolkit\Input\Prefabs** , recherchez la ressource **InputManager** .
2. Glissez-déplacez le **InputManager** sur la **hiérarchie**.
3. Dans le dossier **HoloToolkit\Input\Prefabs** , recherchez la ressource **curseur** .
4. Glissez-déposez le **curseur** sur la **hiérarchie**.
5. Sélectionnez l’objet **InputManager** dans la **hiérarchie**.
6. Faites glisser l’objet **Cursor** de la **hiérarchie** vers le champ **Cursor** du **SimpleSinglePointerSelector**de InputManager, en bas de l' **inspecteur**.

![Configuration du sélecteur de pointeur simple simple](images/holograms210-ssps.png)

### <a name="build-and-deploy"></a>Génération et déploiement

1. Régénérez l’application à partir du **fichier > paramètres de build**.
2. Ouvrez le **dossier**de l’application.
3. Ouvrez la **solution Visual Studio ModelExplorer**.
4. Cliquez sur déboguer **-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
5. Observez comment le curseur est dessiné et comment il change d’apparence s’il touche un hologramme.

### <a name="instructions"></a>Instructions

1. Dans le volet **hiérarchie** , développez l’objet **AstroMan**->**GEO_G**->**Back_Center** .
2. Double-cliquez sur **Interactible.cs** pour l’ouvrir dans Visual Studio.
3. Supprimez les marques de commentaire des lignes dans les rappels **IFocusable. OnFocusEnter ()** et **IFocusable. OnFocusExit ()** dans **Interactible.cs**. Celles-ci sont appelées par le InputManager du Toolkit de la réalité mixte lorsque le focus (soit par le point de présence ou par le contrôleur pointant) entre et quitte le conflit du GameObject spécifique.

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
>Nous utilisons `DisableKeyword` et versions ultérieures. `EnableKeyword` Pour pouvoir les utiliser dans votre propre application avec le nuanceur standard du kit de ressources, vous devez suivre les [instructions Unity pour accéder aux documents par le biais](https://docs.unity3d.com/Manual/MaterialsAccessingViaScript.html)d’un script. Dans ce cas, nous avons déjà inclus les [trois variantes de matériel mis](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-210-Gaze/Completed/ModelExplorer/Assets/Resources/Models/AstroMan/Materials) en surbrillance nécessaires dans le dossier ressources (recherchez les trois éléments avec la mise en surbrillance dans le nom).

### <a name="build-and-deploy"></a>Génération et déploiement

1. Comme précédemment, générez le projet et déployez sur HoloLens.
2. Observez ce qui se passe quand le point de regard est destiné à un objet et lorsqu’il ne l’est pas.

## <a name="chapter-3---targeting-techniques"></a>Chapitre 3-techniques de ciblage

>[!VIDEO https://www.youtube.com/embed/TFnuLva4VJ0]

### <a name="objectives"></a>Objectifs

* Facilitez la cible des hologrammes.
* Stabiliser les mouvements des têtes naturelles.

### <a name="instructions"></a>Instructions

1. Dans le volet **hiérarchie** , sélectionnez l’objet **InputManager** .
2. Dans le volet de l' **inspecteur** , recherchez le script de **stabilisation du regard** . Cliquez dessus pour l’ouvrir dans Visual Studio, si vous souhaitez jeter un coup d’œil.
    * Ce script itère sur des exemples de données Raycast et permet de stabiliser le regard de la précision de l’utilisateur.
3. Dans l' **inspecteur**, vous pouvez modifier la valeur des **exemples de stabilité stockés** . Cette valeur représente le nombre d’échantillons sur lesquels le stabilisateur effectue une itération pour calculer la valeur stabilisée.

## <a name="chapter-4---directional-indicator"></a>Chapitre 4-indicateur directionnel

>[!VIDEO https://www.youtube.com/embed/htVbJCMlj64]

### <a name="objectives"></a>Objectifs

* Ajoutez un indicateur directionnel sur le curseur pour faciliter la recherche des hologrammes.

### <a name="instructions"></a>Instructions

Nous allons utiliser le fichier **DirectionIndicator.cs** , qui:

1. Affichez l’indicateur directionnel si l’utilisateur n’est pas Gazing sur les hologrammes.
2. Masquer l’indicateur directionnel si l’utilisateur est Gazing sur les hologrammes.
3. Mettez à jour l’indicateur directionnel pour pointer vers les hologrammes.

Commençons.

1. Cliquez sur l’objet **AstroMan** dans le volet de **hiérarchie** , puis **cliquez sur la flèche pour le** développer.
2. Dans le volet **hiérarchie** , sélectionnez l’objet **DirectionalIndicator** sous **AstroMan**.
3. Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
4. Dans le menu, tapez dans l’indicateur de **direction**de la zone de recherche. Sélectionnez le résultat de la recherche.
5. Dans le volet **hiérarchie** , faites glisser et déposez l’objet **Cursor** sur la propriété **Cursor** de l' **inspecteur**.
6. Dans le panneau **projet** , dans le **dossier hologrammes** , faites glisser et déposez l’élément **DirectionalIndicator** sur la propriété **indicateur directionnel** de l' **inspecteur**.
7. Générez et déployez l’application.
8. Regardez comment l’objet indicateur directionnel vous aide à trouver le astronautes.

## <a name="chapter-5---billboarding"></a>Chapitre 5-panneaux

>[!VIDEO https://www.youtube.com/embed/qFiLr_LUACE]

### <a name="objectives"></a>Objectifs

* Utilisez le billboarding pour que les hologrammes soient toujours face à vous.

Nous utiliserons le fichier **Billboard.cs** pour garder un gameobject orienté de manière à ce qu’il soit à tout moment destiné à l’utilisateur.

1. Dans le volet **hiérarchie** , sélectionnez l’objet **AstroMan** .
2. Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
3. Dans le menu, tapez dans le **panneau**d’interzone de recherche. Sélectionnez le résultat de la recherche.
4. Dans l' **inspecteur** , affectez la valeur **Y**à l' **axe pivot** .
5. Essayez ! Générez et déployez l’application comme auparavant.
6. Découvrez comment l’objet de tableau blanc vous concerne, quelle que soit la façon dont vous modifiez le point de vue.
7. Supprimez le script du **AstroMan** pour le moment.

## <a name="chapter-6---tag-along"></a>Chapitre 6-balises

>[!VIDEO https://www.youtube.com/embed/Ct8ORZAX5JU]

### <a name="objectives"></a>Objectifs

* Utilisez la balise pour que nos hologrammes suivent la salle.

À mesure que nous travaillons sur ce problème, nous vous présenterons les contraintes de conception suivantes:

* Le contenu doit toujours être un aperçu.
* Le contenu ne doit pas être en cours de traitement.
* Le contenu de verrouillage de la tête est inconfortable.

La solution utilisée ici consiste à utiliser une approche «avec balises».

Une balise avec un objet ne quitte jamais entièrement la vue de l’utilisateur. Vous pouvez considérer la balise comme un objet attaché à la tête de l’utilisateur par les bandes de caoutchouc. Au fur et à mesure que l’utilisateur se déplace, le contenu reste dans un aperçu facile en faisant glisser vers le bord de la vue sans quitter complètement. Lorsque l’utilisateur fait un regard sur l’objet tag, il est plus complet à afficher.

Nous allons utiliser le fichier **SimpleTagalong.cs** , qui:

1. Déterminez si l’objet tag est dans les limites de l’appareil photo.
2. Si ce n’est pas le cas dans la vue frustum, placez la balise sur la partie de façon partielle dans la vue frustum.
3. Sinon, placez la balise sur une distance par défaut de l’utilisateur.

Pour ce faire, nous devons d’abord modifier le script **Interactible.cs** pour appeler **TagalongAction**.

1. Modifiez **Interactible.cs** en terminant le codage de l’exercice 6. a (supprimer les commentaires des lignes 84 à 87).

```cs
/* TODO: DEVELOPER CODING EXERCISE 6.a */
// 6.a: Uncomment the lines below to perform a Tagalong action.
if (interactibleAction != null)
{
    interactibleAction.PerformAction();
}
```

Le script **InteractibleAction.cs** , associé à **Interactible.cs** , effectue des actions personnalisées lorsque vous appuyez sur des hologrammes. Dans ce cas, nous allons en utiliser un spécifiquement pour la balise.

* Dans le dossier **scripts** , cliquez sur la ressource **TagalongAction.cs** pour l’ouvrir dans Visual Studio.
* Terminez l’exercice de codage ou remplacez-le par ce qui suit:
  * En haut de la **hiérarchie**, dans la barre de recherche, tapez **ChestButton_Center** et sélectionnez le résultat.
  * Dans le volet de l' **inspecteur** , cliquez sur le bouton **Ajouter un composant** .
  * Dans le menu, tapez dans la zone de recherche **accompagnent action**. Sélectionnez le résultat de la recherche.
  * Dans  le dossier hologrammes, recherchez la ressource **accompagnent** .
  * Sélectionnez l’objet **ChestButton_Center** dans la **hiérarchie**. Glissez-déplacez l’objet **accompagnent** à partir du panneau **projet** vers l' **inspecteur** dans la propriété **Object to accompagnent** .
  * Faites glisser l’objet d' **action accompagnent** à partir de l' **inspecteur** dans le champ d' **action Interactible** sur le script **Interactible** .
* Double-cliquez sur le script **TagalongAction** pour l’ouvrir dans Visual Studio.

![Configuration de Interactible](images/holograms210-interactible.png)

Nous devons ajouter ce qui suit:

* Ajoutez des fonctionnalités à la fonction PerformAction dans le script TagalongAction (héritée de InteractibleAction).
* Ajoutez un billboarding à l’objet pointant vers le regard et définissez l’axe pivot sur XY.
* Ensuite, ajoutez une balise simple, avec l’objet.

Voici notre solution, de **TagalongAction.cs**:

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
* Regardez comment le contenu suit le centre du point de regard, mais pas en continu et sans le bloquer.
