---
title: MR spatial 230-spatial Mapping
description: Suivez cette procédure pas à pas de codage à l’aide d’Unity, Visual Studio et HoloLens pour apprendre les concepts de mappage spatial.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, mappage spatial, reconstruction de surface, maille
ms.openlocfilehash: cf4a2dd3e5eb74c0aaf849442e5f5e404d7cb661
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434579"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. [Une nouvelle série de didacticiels](mrlearning-base.md) a été publiée pour HoloLens 2.

<br>

# <a name="mr-spatial-230-spatial-mapping"></a>MR spatial 230 : mappage spatial

Le [mappage spatial](spatial-mapping.md) combine le monde réel et le monde virtuel ensemble en apprenant des hologrammes sur l’environnement. Dans l’spatial spatial 230 (Project Planetarium), nous allons apprendre à :

* Analyser l’environnement et transférer des données de HoloLens vers votre ordinateur de développement.
* Explorez les nuanceurs et apprenez à les utiliser pour visualiser votre espace.
* Décomposez le maillage de la pièce en plans simples à l’aide du traitement de maillage.
* Allez au-delà des techniques de placement que nous avons appris dans les [notions de base de m. 101](holograms-101.md)et fournissez des commentaires sur l’endroit où un hologramme peut être placé dans l’environnement.
* Explorez les effets d’occlusion. par conséquent, lorsque votre hologramme se trouve derrière un objet réel, vous pouvez toujours le voir avec la vision x-ray !

>[!VIDEO https://www.youtube.com/embed/NSNYRkUX6Mw]

## <a name="device-support"></a>Périphériques pris en charge

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>MR spatial 230 : mappage spatial</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Conditions préalables

* Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).
* Certaines fonctionnalités C# de programmation de base.
* Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-230-SpatialMapping.zip) requis par le projet. Requiert Unity 2017,2 ou une version ultérieure.
  * Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-230.zip).
  * Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-230.zip).
  * Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-230.zip).
* Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-230-SpatialMapping).

### <a name="notes"></a>Notes

* Dans Visual Studio, l’option « Activer Uniquement mon code » doit être désactivée (*décochée*) sous Outils > Options > débogage pour atteindre les points d’arrêt dans votre code.

## <a name="unity-setup"></a>Configuration de Unity

>[!VIDEO https://www.youtube.com/embed/y2Y4LhK6TEM]

* Démarrez **Unity**.
* Sélectionnez **nouveau** pour créer un nouveau projet.
* Nommez le projet **Planetarium**.
* Vérifiez que le paramètre **3D** est sélectionné.
* Cliquez sur **Create Project**.
* Une fois Unity lancé, accédez à **modifier > paramètres du projet > Player**.
* Dans le volet de l' **inspecteur** , recherchez et sélectionnez l’icône du **Windows Store** vert.
* Développez **autres paramètres**.
* Dans la section **rendu** , activez la case à cocher **prise en charge de la réalité virtuelle** .
* Vérifiez que **Windows holographique** apparaît dans la liste des kits de développement logiciel (SDK) de **réalité virtuelle**. Si ce n’est pas le cas, sélectionnez le bouton **+** au bas de la liste et choisissez **Windows holographique**.
* Développez **paramètres de publication**.
* Dans la section **fonctionnalités** , vérifiez les paramètres suivants :
    * InternetClientServer
    * PrivateNetworkClientServer
    * Microphone
    * SpatialPerception
* Accédez à **modifier > paramètres du projet > qualité**
* Dans le volet de l' **inspecteur** , sous l’icône Windows Store, sélectionnez la flèche déroulante noire sous la ligne « default » et définissez le paramètre par défaut sur **très faible**.
* Accédez à **ressources > importer un package > package personnalisé**.
* Accédez au dossier **. ..\holographicacademy-holograms-230-SpatialMapping\Starting** .
* Cliquez sur **Planetarium. pour Unity**.
* Cliquez sur **Ouvrir**.
* Une fenêtre **Importer un package Unity** doit s’afficher. cliquez sur le bouton **Importer** .
* Attendez que Unity importe toutes les ressources dont nous aurons besoin pour terminer ce projet.
* Dans le panneau **hiérarchie** , supprimez l' **appareil photo principal**.
* Dans le panneau **projet** , dans le dossier **HoloToolkit-SpatialMapping-230\Utilities\Prefabs** , recherchez l’objet **Camera principal** .
* Glissez-déplacez le Prefab d' **appareil photo principal** dans le panneau de **hiérarchie** .
* Dans le panneau **hiérarchie** , supprimez l’objet de **lumière directionnelle** .
* Dans le panneau **projet** , dans le dossier **hologrammes** , localisez l’objet **curseur** .
* Faites glisser & déposez le **curseur** Prefab dans la **hiérarchie**.
* Dans le volet **hiérarchie** , sélectionnez l’objet **curseur** .
* Dans le panneau **inspecteur** , cliquez sur la liste déroulante **couche** , puis sélectionnez **modifier les couches...** .
* Nommez **User Layer 31** en «**SpatialMapping**».
* Enregistrez la nouvelle scène : **fichier > enregistrer la scène sous...**
* Cliquez sur **nouveau dossier** et nommez le dossier **scenes**.
* Nommez le fichier «**Planetarium**» et enregistrez-le dans le dossier **scenes** .

## <a name="chapter-1---scanning"></a>Chapitre 1-analyse

>[!VIDEO https://www.youtube.com/embed/888oW51z_cE]

**Cherché**

* Découvrez le SurfaceObserver et comment ses paramètres affectent l’expérience et les performances.
* Créez une expérience de numérisation de salle pour collecter les mailles de votre salle.

**Ample**

* Dans le dossier **HoloToolkit-SpatialMapping-230\SpatialMapping\Prefabs** du panneau **projet** , recherchez le Prefab **SpatialMapping** .
* Faites glisser & déposer le Prefab **SpatialMapping** dans le panneau de **hiérarchie** .

**Création et déploiement (partie 1)**

* Dans Unity, sélectionnez **fichier > paramètres de build**.
* Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène **Planetarium** à la Build.
* Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur **basculer la plateforme**.
* Définissez le **SDK** sur le **type de build** **Universal 10** et UWP sur **D3D**.
* Vérifiez **les C# projets Unity**.
* Cliquez sur **Build**.
* Créez un **dossier** nommé « App ».
* Cliquez sur le dossier de l' **application** .
* Appuyez sur le bouton **Sélectionner un dossier** .
* Une fois la création d’Unity terminée, une fenêtre de l’Explorateur de fichiers s’affiche.
* Double-cliquez sur le dossier de l' **application** pour l’ouvrir.
* Double-cliquez sur **Planetarium. sln** pour charger le projet dans Visual Studio.
* Dans Visual Studio, utilisez la barre d’outils supérieure pour changer la configuration en **Release**.
* Remplacez la plateforme par **x86**.
* Cliquez sur la flèche déroulante à droite de « ordinateur local », puis sélectionnez **ordinateur distant**.
* Entrez l' [adresse IP de votre appareil](connecting-to-wi-fi-on-hololens.md#identifying-the-ip-address-of-your-hololens-on-the-wi-fi-network) dans le champ adresse et changez le mode d’authentification en **protocole universel (protocole non chiffré)** .
* Cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.
* Regardez le panneau de **sortie** dans Visual Studio pour l’état de génération et de déploiement.
* Une fois votre application déployée, parcourez la salle. Vous verrez les surfaces environnantes couvertes par les maillages filaires noir et blanc.
* Analysez votre environnement. Veillez à examiner les murs, les limites et les étages.

**Génération et déploiement (partie 2)**

Voyons maintenant comment le mappage spatial peut affecter les performances.

* Dans Unity, sélectionnez **windows > Profiler**.
* Cliquez sur **Ajouter profiler > GPU**.
* Cliquez sur **> du profileur Active <Enter IP>** .
* Entrez l' **adresse IP** de votre HoloLens.
* Cliquez sur **Se connecter**.
* Observez le nombre de millisecondes nécessaires au rendu d’une trame par le GPU.
* Arrêtez l’exécution de l’application sur l’appareil.
* Revenez à Visual Studio et ouvrez **SpatialMappingObserver.cs**. Vous le trouverez dans le dossier HoloToolkit\SpatialMapping du projet assembly-CSharp (universel Windows).
* Recherchez la fonction **éveillé ()** , puis ajoutez la ligne de code suivante : **TrianglesPerCubicMeter = 1200 ;**
* Redéployez le projet sur votre appareil, puis **reconnectez le profileur**. Observez la modification du nombre de millisecondes pour le rendu d’un frame.
* Arrêtez l’exécution de l’application sur l’appareil.

**Enregistrer et charger dans Unity**

Enfin, nous allons enregistrer notre maillage d’espace et le charger dans Unity.

* Revenez à Visual Studio et supprimez la ligne **TrianglesPerCubicMeter** que vous avez ajoutée dans la fonction **éveillé ()** au cours de la section précédente.
* Redéployez le projet sur votre appareil. Nous devons maintenant être en cours d’exécution avec des triangles **500** par mètre cube.
* Ouvrez un navigateur et entrez dans votre adresseIP HoloLens pour accéder au **portail de périphériques Windows**.
* Sélectionnez l’option **vue 3D** dans le volet gauche.
* Sous **reconstruction** de la surface, sélectionnez le bouton **mettre à jour** .
* Regardez que les zones que vous avez analysées dans votre HoloLens s’affichent dans la fenêtre d’affichage.
* Pour enregistrer l’analyse de votre salle, appuyez sur le bouton **Enregistrer** .
* Ouvrez votre dossier **téléchargements** pour rechercher le modèle de salle enregistré **SRMesh. obj**.
* Copiez **SRMesh. obj** dans le dossier **composants** de votre projet Unity.
* Dans Unity, sélectionnez l’objet **SpatialMapping** dans le panneau **hiérarchie** .
* Localisez le composant **Observateur de surface d’objet (script)** .
* Cliquez sur le cercle situé à droite de la propriété **modèle de salle** .
* Recherchez et sélectionnez l’objet **SRMesh** , puis fermez la fenêtre.
* Vérifiez que la propriété **modèle de salle** dans le panneau **inspecteur** a désormais la valeur **SRMesh**.
* Appuyez sur le bouton de **lecture** pour entrer en mode aperçu Unity.
* Le composant SpatialMapping charge les maillages à partir du modèle de salle enregistré, afin que vous puissiez les utiliser dans Unity.
* Basculez en vue **scène** pour voir l’ensemble de votre modèle d’espace affiché avec le nuanceur filaire.
* Appuyez de nouveau sur le bouton **lecture** pour quitter le mode aperçu.

**Remarque :** La prochaine fois que vous passerez en mode aperçu dans Unity, le maillage Room enregistré sera chargé par défaut.

## <a name="chapter-2---visualization"></a>Chapitre 2-visualisation

>[!VIDEO https://www.youtube.com/embed/RnkvXl-aXD4]

**Cherché**

* Découvrez les principes de base des nuanceurs.
* Visualisez votre environnement.

**Ample**

* Dans le panneau de la **hiérarchie** Unity, sélectionnez l’objet **SpatialMapping** .
* Dans le volet de l' **inspecteur** , recherchez le composant de **Gestionnaire de mappage spatial (script)** .
* Cliquez sur le cercle situé à droite de la propriété **surface** .
* Recherchez et sélectionnez le matériel **BlueLinesOnWalls** et fermez la fenêtre.
* Dans le dossier **nuanciers** du panneau **projet** , double-cliquez sur **BlueLinesOnWalls** pour ouvrir le nuanceur dans Visual Studio.
* Il s’agit d’un nuanceur de pixels (vertex à fragment) simple qui effectue les tâches suivantes :
    1. Convertit l’emplacement d’un vertex en espace universel.
    2. Vérifie la normale du vertex pour déterminer si un pixel est vertical.
    3. Définit la couleur du pixel pour le rendu.

**Génération et déploiement**

* Revenez à Unity et appuyez sur **Play** pour passer en mode aperçu.
* Les lignes bleues sont affichées sur toutes les surfaces verticales de la maille de la salle (qui sont chargées automatiquement à partir de nos données d’analyse enregistrées).
* Basculez vers l’onglet **scène** pour ajuster la vue de la pièce et voir comment l’intégralité du maillage de la salle apparaît dans Unity.
* Dans le panneau **projet** , recherchez le dossier **matériaux** et sélectionnez le matériel **BlueLinesOnWalls** .
* Modifiez certaines propriétés et observez le mode d’affichage des modifications dans l’éditeur Unity.
    * Dans le panneau **inspecteur** , ajustez la valeur **LineScale** pour que les lignes apparaissent plus épaisses ou plus fines.
    * Dans le panneau **inspecteur** , ajustez la valeur **LinesPerMeter** pour modifier le nombre de lignes qui s’affichent sur chaque mur.
* Cliquez à nouveau sur **lire** pour quitter le mode aperçu.
* Générez et déployez sur HoloLens et observez la façon dont le rendu du nuanceur apparaît sur les surfaces réelles.

Unity fait un excellent travail d’aperçu des documents, mais il est toujours judicieux d’extraire le rendu dans l’appareil.

## <a name="chapter-3---processing"></a>Chapitre 3-traitement

>[!VIDEO https://www.youtube.com/embed/kaUKiNiDxwY]

**Cherché**

* Découvrez les techniques permettant de traiter les données de mappage spatiale pour une utilisation dans votre application.
* Analyser les données de mappage spatiale pour rechercher des plans et supprimer des triangles.
* Utilisez des plans pour le placement de l’hologramme.

**Ample**

* Dans le panneau **projet** d’Unity, dans le dossier **hologrammes** , recherchez l’objet **SpatialProcessing** .
* Faites glisser & déposez l’objet **SpatialProcessing** dans le panneau de **hiérarchie** .

SpatialProcessing Prefab comprend des composants pour traiter les données de mappage spatiale. **SurfaceMeshesToPlanes.cs** trouvera et générera des plans basés sur les données de mappage spatiale. Nous utiliserons des plans dans notre application pour représenter les murs, les étages et les plafonds. Ce Prefab comprend également **RemoveSurfaceVertices.cs** qui peut supprimer des vertex du maillage de mappage spatial. Cela peut être utilisé pour créer des trous dans la maille ou pour supprimer les triangles excédentaires qui ne sont plus nécessaires (car les plans peuvent être utilisés à la place).

* Dans le panneau **projet** d’Unity, dans le dossier **hologrammes** , recherchez l’objet **SpaceCollection** .
* Faites glisser et déposez l’objet **SpaceCollection** dans le panneau de **hiérarchie** .
* Dans le volet **hiérarchie** , sélectionnez l’objet **SpatialProcessing** .
* Dans le volet de l' **inspecteur** , recherchez le composant **Gestionnaire d’espace de lecture (script)** .
* Double-cliquez sur **PlaySpaceManager.cs** pour l’ouvrir dans Visual Studio.

PlaySpaceManager.cs contient le code spécifique à l’application. Nous ajouterons des fonctionnalités à ce script pour activer le comportement suivant :

1. Arrêtez la collecte des données de mappage spatiale après avoir dépassé la limite de temps d’analyse (10 secondes).
2. Traiter les données de mappage spatiale :
    1. Utilisez SurfaceMeshesToPlanes pour créer une représentation plus simple du monde comme plans (murs, étages, plafonds, etc.).
    2. Utilisez RemoveSurfaceVertices pour supprimer les triangles de surface qui se trouvent dans les limites du plan.
3. Générez un ensemble d’hologrammes dans le monde et placez-les sur des plans muraux et de plancher près de l’utilisateur.

Effectuez les exercices de codage marqués dans PlaySpaceManager.cs ou remplacez le script par la solution terminée ci-dessous :

```cs
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Windows.Speech;
using Academy.HoloToolkit.Unity;

/// <summary>
/// The SurfaceManager class allows applications to scan the environment for a specified amount of time 
/// and then process the Spatial Mapping Mesh (find planes, remove vertices) after that time has expired.
/// </summary>
public class PlaySpaceManager : Singleton<PlaySpaceManager>
{
    [Tooltip("When checked, the SurfaceObserver will stop running after a specified amount of time.")]
    public bool limitScanningByTime = true;

    [Tooltip("How much time (in seconds) that the SurfaceObserver will run after being started; used when 'Limit Scanning By Time' is checked.")]
    public float scanTime = 30.0f;

    [Tooltip("Material to use when rendering Spatial Mapping meshes while the observer is running.")]
    public Material defaultMaterial;

    [Tooltip("Optional Material to use when rendering Spatial Mapping meshes after the observer has been stopped.")]
    public Material secondaryMaterial;

    [Tooltip("Minimum number of floor planes required in order to exit scanning/processing mode.")]
    public uint minimumFloors = 1;

    [Tooltip("Minimum number of wall planes required in order to exit scanning/processing mode.")]
    public uint minimumWalls = 1;

    /// <summary>
    /// Indicates if processing of the surface meshes is complete.
    /// </summary>
    private bool meshesProcessed = false;

    /// <summary>
    /// GameObject initialization.
    /// </summary>
    private void Start()
    {
        // Update surfaceObserver and storedMeshes to use the same material during scanning.
        SpatialMappingManager.Instance.SetSurfaceMaterial(defaultMaterial);

        // Register for the MakePlanesComplete event.
        SurfaceMeshesToPlanes.Instance.MakePlanesComplete += SurfaceMeshesToPlanes_MakePlanesComplete;
    }

    /// <summary>
    /// Called once per frame.
    /// </summary>
    private void Update()
    {
        // Check to see if the spatial mapping data has been processed
        // and if we are limiting how much time the user can spend scanning.
        if (!meshesProcessed && limitScanningByTime)
        {
            // If we have not processed the spatial mapping data
            // and scanning time is limited...

            // Check to see if enough scanning time has passed
            // since starting the observer.
            if (limitScanningByTime && ((Time.time - SpatialMappingManager.Instance.StartTime) < scanTime))
            {
                // If we have a limited scanning time, then we should wait until
                // enough time has passed before processing the mesh.
            }
            else
            {
                // The user should be done scanning their environment,
                // so start processing the spatial mapping data...

                /* TODO: 3.a DEVELOPER CODING EXERCISE 3.a */

                // 3.a: Check if IsObserverRunning() is true on the
                // SpatialMappingManager.Instance.
                if(SpatialMappingManager.Instance.IsObserverRunning())
                {
                    // 3.a: If running, Stop the observer by calling
                    // StopObserver() on the SpatialMappingManager.Instance.
                    SpatialMappingManager.Instance.StopObserver();
                }

                // 3.a: Call CreatePlanes() to generate planes.
                CreatePlanes();

                // 3.a: Set meshesProcessed to true.
                meshesProcessed = true;
            }
        }
    }

    /// <summary>
    /// Handler for the SurfaceMeshesToPlanes MakePlanesComplete event.
    /// </summary>
    /// <param name="source">Source of the event.</param>
    /// <param name="args">Args for the event.</param>
    private void SurfaceMeshesToPlanes_MakePlanesComplete(object source, System.EventArgs args)
    {
        /* TODO: 3.a DEVELOPER CODING EXERCISE 3.a */

        // Collection of floor and table planes that we can use to set horizontal items on.
        List<GameObject> horizontal = new List<GameObject>();

        // Collection of wall planes that we can use to set vertical items on.
        List<GameObject> vertical = new List<GameObject>();

        // 3.a: Get all floor and table planes by calling
        // SurfaceMeshesToPlanes.Instance.GetActivePlanes().
        // Assign the result to the 'horizontal' list.
        horizontal = SurfaceMeshesToPlanes.Instance.GetActivePlanes(PlaneTypes.Table | PlaneTypes.Floor);

        // 3.a: Get all wall planes by calling
        // SurfaceMeshesToPlanes.Instance.GetActivePlanes().
        // Assign the result to the 'vertical' list.
        vertical = SurfaceMeshesToPlanes.Instance.GetActivePlanes(PlaneTypes.Wall);

        // Check to see if we have enough horizontal planes (minimumFloors)
        // and vertical planes (minimumWalls), to set holograms on in the world.
        if (horizontal.Count >= minimumFloors && vertical.Count >= minimumWalls)
        {
            // We have enough floors and walls to place our holograms on...

            // 3.a: Let's reduce our triangle count by removing triangles
            // from SpatialMapping meshes that intersect with our active planes.
            // Call RemoveVertices().
            // Pass in all activePlanes found by SurfaceMeshesToPlanes.Instance.
            RemoveVertices(SurfaceMeshesToPlanes.Instance.ActivePlanes);

            // 3.a: We can indicate to the user that scanning is over by
            // changing the material applied to the Spatial Mapping meshes.
            // Call SpatialMappingManager.Instance.SetSurfaceMaterial().
            // Pass in the secondaryMaterial.
            SpatialMappingManager.Instance.SetSurfaceMaterial(secondaryMaterial);

            // 3.a: We are all done processing the mesh, so we can now
            // initialize a collection of Placeable holograms in the world
            // and use horizontal/vertical planes to set their starting positions.
            // Call SpaceCollectionManager.Instance.GenerateItemsInWorld().
            // Pass in the lists of horizontal and vertical planes that we found earlier.
            SpaceCollectionManager.Instance.GenerateItemsInWorld(horizontal, vertical);
        }
        else
        {
            // We do not have enough floors/walls to place our holograms on...

            // 3.a: Re-enter scanning mode so the user can find more surfaces by
            // calling StartObserver() on the SpatialMappingManager.Instance.
            SpatialMappingManager.Instance.StartObserver();

            // 3.a: Re-process spatial data after scanning completes by
            // re-setting meshesProcessed to false.
            meshesProcessed = false;
        }
    }

    /// <summary>
    /// Creates planes from the spatial mapping surfaces.
    /// </summary>
    private void CreatePlanes()
    {
        // Generate planes based on the spatial map.
        SurfaceMeshesToPlanes surfaceToPlanes = SurfaceMeshesToPlanes.Instance;
        if (surfaceToPlanes != null && surfaceToPlanes.enabled)
        {
            surfaceToPlanes.MakePlanes();
        }
    }

    /// <summary>
    /// Removes triangles from the spatial mapping surfaces.
    /// </summary>
    /// <param name="boundingObjects"></param>
    private void RemoveVertices(IEnumerable<GameObject> boundingObjects)
    {
        RemoveSurfaceVertices removeVerts = RemoveSurfaceVertices.Instance;
        if (removeVerts != null && removeVerts.enabled)
        {
            removeVerts.RemoveSurfaceVerticesWithinBounds(boundingObjects);
        }
    }

    /// <summary>
    /// Called when the GameObject is unloaded.
    /// </summary>
    private void OnDestroy()
    {
        if (SurfaceMeshesToPlanes.Instance != null)
        {
            SurfaceMeshesToPlanes.Instance.MakePlanesComplete -= SurfaceMeshesToPlanes_MakePlanesComplete;
        }
    }
}
```

**Génération et déploiement**

* Avant de déployer sur HoloLens, appuyez sur le bouton de **lecture** dans Unity pour passer en mode lecture.
* Une fois le maillage de la salle chargé à partir du fichier, attendez 10 secondes avant le début du traitement sur le maillage de mappage spatial.
* Une fois le traitement terminé, les plans s’affichent pour représenter le plancher, les murs, le plafond, etc.
* Une fois tous les plans détectés, un système solaire doit s’afficher sur une table de plancher près de l’appareil photo.
* Deux affiches doivent également apparaître sur les murs près de l’appareil photo. Basculez vers l’onglet **scène** si vous ne les voyez pas en mode **jeu** .
* Appuyez de nouveau sur le bouton de **lecture** pour quitter le mode lecture.
* Générez et déployez sur HoloLens, comme d’habitude.
* Attendez la fin de l’analyse et du traitement des données de mappage spatiale.
* Une fois que vous voyez des plans, essayez de trouver le système solaire et les affiches dans votre monde.

## <a name="chapter-4---placement"></a>Chapitre 4-placement

>[!VIDEO https://www.youtube.com/embed/Srhtpid1uZc]

**Cherché**

* Déterminer si un hologramme peut tenir sur une surface.
* Fournir des commentaires à l’utilisateur lorsqu’un hologramme ne peut pas être ajusté sur une surface.

**Ample**

* Dans le panneau de la **hiérarchie** Unity, sélectionnez l’objet **SpatialProcessing** .
* Dans le volet de l' **inspecteur** , recherchez les **maillages des surfaces du composant plans (script)** .
* Remplacez la valeur de la propriété **dessiner des plans** par **Nothing** pour effacer la sélection.
* Remplacez la propriété **dessiner des plans** par **Wall**, afin que seuls les plans muraux soient rendus.
* Dans le panneau **projet** , cliquez sur le dossier **scripts** , double-cliquez sur **Placeable.cs** pour l’ouvrir dans Visual Studio.

Le script **positionnable** est déjà associé aux affiches et à la boîte de projection créées après la recherche du plan. Tout ce que nous devons faire, c’est supprimer les marques de commentaire de code, et ce script va obtenir ce qui suit :

1. Déterminez si un hologramme est ajusté sur une surface par Raycasting à partir du centre et quatre coins du cube englobant.
2. Vérifiez la normale de la surface pour déterminer si elle est suffisamment lisse pour que l’hologramme se vide.
3. Restituez un cube englobant autour de l’hologramme pour afficher sa taille réelle lors de son placement.
4. Convertit une ombre sous/derrière l’hologramme pour montrer où il sera placé sur le plancher/le mur.
5. Restitue l’ombre en rouge, si l’hologramme ne peut pas être placé sur l’aire, ou vert, si possible.
6. Réorienter l’hologramme pour qu’il s’aligne avec le type de surface (vertical ou horizontal) auquel il a une affinité.
7. Placez en douceur l’hologramme sur la surface sélectionnée pour éviter le comportement de saut ou d’alignement.

Supprimez les marques de commentaire de tout le code dans l’exercice de codage ci-dessous, ou utilisez cette solution terminée dans **Placeable.cs**:

```cs
using System.Collections.Generic;
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Enumeration containing the surfaces on which a GameObject
/// can be placed.  For simplicity of this sample, only one
/// surface type is allowed to be selected.
/// </summary>
public enum PlacementSurfaces
{
    // Horizontal surface with an upward pointing normal.
    Horizontal = 1,

    // Vertical surface with a normal facing the user.
    Vertical = 2,
}

/// <summary>
/// The Placeable class implements the logic used to determine if a GameObject
/// can be placed on a target surface. Constraints for placement include:
/// * No part of the GameObject's box collider impacts with another object in the scene
/// * The object lays flat (within specified tolerances) against the surface
/// * The object would not fall off of the surface if gravity were enabled.
/// This class also provides the following visualizations.
/// * A transparent cube representing the object's box collider.
/// * Shadow on the target surface indicating whether or not placement is valid.
/// </summary>
public class Placeable : MonoBehaviour
{
    [Tooltip("The base material used to render the bounds asset when placement is allowed.")]
    public Material PlaceableBoundsMaterial = null;

    [Tooltip("The base material used to render the bounds asset when placement is not allowed.")]
    public Material NotPlaceableBoundsMaterial = null;

    [Tooltip("The material used to render the placement shadow when placement it allowed.")]
    public Material PlaceableShadowMaterial = null;

    [Tooltip("The material used to render the placement shadow when placement it not allowed.")]
    public Material NotPlaceableShadowMaterial = null;

    [Tooltip("The type of surface on which the object can be placed.")]
    public PlacementSurfaces PlacementSurface = PlacementSurfaces.Horizontal;

    [Tooltip("The child object(s) to hide during placement.")]
    public List<GameObject> ChildrenToHide = new List<GameObject>();

    /// <summary>
    /// Indicates if the object is in the process of being placed.
    /// </summary>
    public bool IsPlacing { get; private set; }

    // The most recent distance to the surface.  This is used to 
    // locate the object when the user's gaze does not intersect
    // with the Spatial Mapping mesh.
    private float lastDistance = 2.0f;

    // The distance away from the target surface that the object should hover prior while being placed.
    private float hoverDistance = 0.15f;

    // Threshold (the closer to 0, the stricter the standard) used to determine if a surface is flat.
    private float distanceThreshold = 0.02f;

    // Threshold (the closer to 1, the stricter the standard) used to determine if a surface is vertical.
    private float upNormalThreshold = 0.9f;

    // Maximum distance, from the object, that placement is allowed.
    // This is used when raycasting to see if the object is near a placeable surface.
    private float maximumPlacementDistance = 5.0f;

    // Speed (1.0 being fastest) at which the object settles to the surface upon placement.
    private float placementVelocity = 0.06f;

    // Indicates whether or not this script manages the object's box collider.
    private bool managingBoxCollider = false;

    // The box collider used to determine of the object will fit in the desired location.
    // It is also used to size the bounding cube.
    private BoxCollider boxCollider = null;

    // Visible asset used to show the dimensions of the object. This asset is sized
    // using the box collider's bounds.
    private GameObject boundsAsset = null;

    // Visible asset used to show the where the object is attempting to be placed.
    // This asset is sized using the box collider's bounds.
    private GameObject shadowAsset = null;

    // The location at which the object will be placed.
    private Vector3 targetPosition;

    /// <summary>
    /// Called when the GameObject is created.
    /// </summary>
    private void Awake()
    {
        targetPosition = gameObject.transform.position;

        // Get the object's collider.
        boxCollider = gameObject.GetComponent<BoxCollider>();
        if (boxCollider == null)
        {
            // The object does not have a collider, create one and remember that
            // we are managing it.
            managingBoxCollider = true;
            boxCollider = gameObject.AddComponent<BoxCollider>();
            boxCollider.enabled = false;
        }

        // Create the object that will be used to indicate the bounds of the GameObject.
        boundsAsset = GameObject.CreatePrimitive(PrimitiveType.Cube);
        boundsAsset.transform.parent = gameObject.transform;
        boundsAsset.SetActive(false);

        // Create a object that will be used as a shadow.
        shadowAsset = GameObject.CreatePrimitive(PrimitiveType.Quad);
        shadowAsset.transform.parent = gameObject.transform;
        shadowAsset.SetActive(false);
    }

    /// <summary>
    /// Called when our object is selected.  Generally called by
    /// a gesture management component.
    /// </summary>
    public void OnSelect()
    {
        /* TODO: 4.a CODE ALONG 4.a */

        if (!IsPlacing)
        {
            OnPlacementStart();
        }
        else
        {
            OnPlacementStop();
        }
    }

    /// <summary>
    /// Called once per frame.
    /// </summary>
    private void Update()
    {
        /* TODO: 4.a CODE ALONG 4.a */

        if (IsPlacing)
        {
            // Move the object.
            Move();

            // Set the visual elements.
            Vector3 targetPosition;
            Vector3 surfaceNormal;
            bool canBePlaced = ValidatePlacement(out targetPosition, out surfaceNormal);
            DisplayBounds(canBePlaced);
            DisplayShadow(targetPosition, surfaceNormal, canBePlaced);
        }
        else
        {
            // Disable the visual elements.
            boundsAsset.SetActive(false);
            shadowAsset.SetActive(false);

            // Gracefully place the object on the target surface.
            float dist = (gameObject.transform.position - targetPosition).magnitude;
            if (dist > 0)
            {
                gameObject.transform.position = Vector3.Lerp(gameObject.transform.position, targetPosition, placementVelocity / dist);
            }
            else
            {
                // Unhide the child object(s) to make placement easier.
                for (int i = 0; i < ChildrenToHide.Count; i++)
                {
                    ChildrenToHide[i].SetActive(true);
                }
            }
        }
    }

    /// <summary>
    /// Verify whether or not the object can be placed.
    /// </summary>
    /// <param name="position">
    /// The target position on the surface.
    /// </param>
    /// <param name="surfaceNormal">
    /// The normal of the surface on which the object is to be placed.
    /// </param>
    /// <returns>
    /// True if the target position is valid for placing the object, otherwise false.
    /// </returns>
    private bool ValidatePlacement(out Vector3 position, out Vector3 surfaceNormal)
    {
        Vector3 raycastDirection = gameObject.transform.forward;

        if (PlacementSurface == PlacementSurfaces.Horizontal)
        {
            // Placing on horizontal surfaces.
            // Raycast from the bottom face of the box collider.
            raycastDirection = -(Vector3.up);
        }

        // Initialize out parameters.
        position = Vector3.zero;
        surfaceNormal = Vector3.zero;

        Vector3[] facePoints = GetColliderFacePoints();

        // The origin points we receive are in local space and we 
        // need to raycast in world space.
        for (int i = 0; i < facePoints.Length; i++)
        {
            facePoints[i] = gameObject.transform.TransformVector(facePoints[i]) + gameObject.transform.position;
        }

        // Cast a ray from the center of the box collider face to the surface.
        RaycastHit centerHit;
        if (!Physics.Raycast(facePoints[0],
                        raycastDirection,
                        out centerHit,
                        maximumPlacementDistance,
                        SpatialMappingManager.Instance.LayerMask))
        {
            // If the ray failed to hit the surface, we are done.
            return false;
        }

        // We have found a surface.  Set position and surfaceNormal.
        position = centerHit.point;
        surfaceNormal = centerHit.normal;

        // Cast a ray from the corners of the box collider face to the surface.
        for (int i = 1; i < facePoints.Length; i++)
        {
            RaycastHit hitInfo;
            if (Physics.Raycast(facePoints[i],
                                raycastDirection,
                                out hitInfo,
                                maximumPlacementDistance,
                                SpatialMappingManager.Instance.LayerMask))
            {
                // To be a valid placement location, each of the corners must have a similar
                // enough distance to the surface as the center point
                if (!IsEquivalentDistance(centerHit.distance, hitInfo.distance))
                {
                    return false;
                }
            }
            else
            {
                // The raycast failed to intersect with the target layer.
                return false;
            }
        }

        return true;
    }

    /// <summary>
    /// Determine the coordinates, in local space, of the box collider face that 
    /// will be placed against the target surface.
    /// </summary>
    /// <returns>
    /// Vector3 array with the center point of the face at index 0.
    /// </returns>
    private Vector3[] GetColliderFacePoints()
    {
        // Get the collider extents.  
        // The size values are twice the extents.
        Vector3 extents = boxCollider.size / 2;

        // Calculate the min and max values for each coordinate.
        float minX = boxCollider.center.x - extents.x;
        float maxX = boxCollider.center.x + extents.x;
        float minY = boxCollider.center.y - extents.y;
        float maxY = boxCollider.center.y + extents.y;
        float minZ = boxCollider.center.z - extents.z;
        float maxZ = boxCollider.center.z + extents.z;

        Vector3 center;
        Vector3 corner0;
        Vector3 corner1;
        Vector3 corner2;
        Vector3 corner3;

        if (PlacementSurface == PlacementSurfaces.Horizontal)
        {
            // Placing on horizontal surfaces.
            center = new Vector3(boxCollider.center.x, minY, boxCollider.center.z);
            corner0 = new Vector3(minX, minY, minZ);
            corner1 = new Vector3(minX, minY, maxZ);
            corner2 = new Vector3(maxX, minY, minZ);
            corner3 = new Vector3(maxX, minY, maxZ);
        }
        else
        {
            // Placing on vertical surfaces.
            center = new Vector3(boxCollider.center.x, boxCollider.center.y, maxZ);
            corner0 = new Vector3(minX, minY, maxZ);
            corner1 = new Vector3(minX, maxY, maxZ);
            corner2 = new Vector3(maxX, minY, maxZ);
            corner3 = new Vector3(maxX, maxY, maxZ);
        }

        return new Vector3[] { center, corner0, corner1, corner2, corner3 };
    }

    /// <summary>
    /// Put the object into placement mode.
    /// </summary>
    public void OnPlacementStart()
    {
        // If we are managing the collider, enable it. 
        if (managingBoxCollider)
        {
            boxCollider.enabled = true;
        }

        // Hide the child object(s) to make placement easier.
        for (int i = 0; i < ChildrenToHide.Count; i++)
        {
            ChildrenToHide[i].SetActive(false);
        }

        // Tell the gesture manager that it is to assume
        // all input is to be given to this object.
        GestureManager.Instance.OverrideFocusedObject = gameObject;

        // Enter placement mode.
        IsPlacing = true;
    }

    /// <summary>
    /// Take the object out of placement mode.
    /// </summary>
    /// <remarks>
    /// This method will leave the object in placement mode if called while
    /// the object is in an invalid location.  To determine whether or not
    /// the object has been placed, check the value of the IsPlacing property.
    /// </remarks>
    public void OnPlacementStop()
    {
        // ValidatePlacement requires a normal as an out parameter.
        Vector3 position;
        Vector3 surfaceNormal;

        // Check to see if we can exit placement mode.
        if (!ValidatePlacement(out position, out surfaceNormal))
        {
            return;
        }

        // The object is allowed to be placed.
        // We are placing at a small buffer away from the surface.
        targetPosition = position + (0.01f * surfaceNormal);

        OrientObject(true, surfaceNormal);

        // If we are managing the collider, disable it. 
        if (managingBoxCollider)
        {
            boxCollider.enabled = false;
        }

        // Tell the gesture manager that it is to resume
        // its normal behavior.
        GestureManager.Instance.OverrideFocusedObject = null;

        // Exit placement mode.
        IsPlacing = false;
    }

    /// <summary>
    /// Positions the object along the surface toward which the user is gazing.
    /// </summary>
    /// <remarks>
    /// If the user's gaze does not intersect with a surface, the object
    /// will remain at the most recently calculated distance.
    /// </remarks>
    private void Move()
    {
        Vector3 moveTo = gameObject.transform.position;
        Vector3 surfaceNormal = Vector3.zero;
        RaycastHit hitInfo;

        bool hit = Physics.Raycast(Camera.main.transform.position,
                                Camera.main.transform.forward,
                                out hitInfo,
                                20f,
                                SpatialMappingManager.Instance.LayerMask);

        if (hit)
        {
            float offsetDistance = hoverDistance;

            // Place the object a small distance away from the surface while keeping 
            // the object from going behind the user.
            if (hitInfo.distance <= hoverDistance)
            {
                offsetDistance = 0f;
            }

            moveTo = hitInfo.point + (offsetDistance * hitInfo.normal);

            lastDistance = hitInfo.distance;
            surfaceNormal = hitInfo.normal;
        }
        else
        {
            // The raycast failed to hit a surface.  In this case, keep the object at the distance of the last
            // intersected surface.
            moveTo = Camera.main.transform.position + (Camera.main.transform.forward * lastDistance);
        }

        // Follow the user's gaze.
        float dist = Mathf.Abs((gameObject.transform.position - moveTo).magnitude);
        gameObject.transform.position = Vector3.Lerp(gameObject.transform.position, moveTo, placementVelocity / dist);

        // Orient the object.
        // We are using the return value from Physics.Raycast to instruct
        // the OrientObject function to align to the vertical surface if appropriate.
        OrientObject(hit, surfaceNormal);
    }

    /// <summary>
    /// Orients the object so that it faces the user.
    /// </summary>
    /// <param name="alignToVerticalSurface">
    /// If true and the object is to be placed on a vertical surface, 
    /// orient parallel to the target surface.  If false, orient the object 
    /// to face the user.
    /// </param>
    /// <param name="surfaceNormal">
    /// The target surface's normal vector.
    /// </param>
    /// <remarks>
    /// The alignToVerticalSurface parameter is ignored if the object
    /// is to be placed on a horizontalSurface
    /// </remarks>
    private void OrientObject(bool alignToVerticalSurface, Vector3 surfaceNormal)
    {
        Quaternion rotation = Camera.main.transform.localRotation;

        // If the user's gaze does not intersect with the Spatial Mapping mesh,
        // orient the object towards the user.
        if (alignToVerticalSurface && (PlacementSurface == PlacementSurfaces.Vertical))
        {
            // We are placing on a vertical surface.
            // If the normal of the Spatial Mapping mesh indicates that the
            // surface is vertical, orient parallel to the surface.
            if (Mathf.Abs(surfaceNormal.y) <= (1 - upNormalThreshold))
            {
                rotation = Quaternion.LookRotation(-surfaceNormal, Vector3.up);
            }
        }
        else
        {
            rotation.x = 0f;
            rotation.z = 0f;
        }

        gameObject.transform.rotation = rotation;
    }

    /// <summary>
    /// Displays the bounds asset.
    /// </summary>
    /// <param name="canBePlaced">
    /// Specifies if the object is in a valid placement location.
    /// </param>
    private void DisplayBounds(bool canBePlaced)
    {
        // Ensure the bounds asset is sized and positioned correctly.
        boundsAsset.transform.localPosition = boxCollider.center;
        boundsAsset.transform.localScale = boxCollider.size;
        boundsAsset.transform.rotation = gameObject.transform.rotation;

        // Apply the appropriate material.
        if (canBePlaced)
        {
            boundsAsset.GetComponent<Renderer>().sharedMaterial = PlaceableBoundsMaterial;
        }
        else
        {
            boundsAsset.GetComponent<Renderer>().sharedMaterial = NotPlaceableBoundsMaterial;
        }

        // Show the bounds asset.
        boundsAsset.SetActive(true);
    }

    /// <summary>
    /// Displays the placement shadow asset.
    /// </summary>
    /// <param name="position">
    /// The position at which to place the shadow asset.
    /// </param>
    /// <param name="surfaceNormal">
    /// The normal of the surface on which the asset will be placed
    /// </param>
    /// <param name="canBePlaced">
    /// Specifies if the object is in a valid placement location.
    /// </param>
    private void DisplayShadow(Vector3 position,
                            Vector3 surfaceNormal,
                            bool canBePlaced)
    {
        // Rotate and scale the shadow so that it is displayed on the correct surface and matches the object.
        float rotationX = 0.0f;

        if (PlacementSurface == PlacementSurfaces.Horizontal)
        {
            rotationX = 90.0f;
            shadowAsset.transform.localScale = new Vector3(boxCollider.size.x, boxCollider.size.z, 1);
        }
        else
        {
            shadowAsset.transform.localScale = boxCollider.size;
        }

        Quaternion rotation = Quaternion.Euler(rotationX, gameObject.transform.rotation.eulerAngles.y, 0);
        shadowAsset.transform.rotation = rotation;

        // Apply the appropriate material.
        if (canBePlaced)
        {
            shadowAsset.GetComponent<Renderer>().sharedMaterial = PlaceableShadowMaterial;
        }
        else
        {
            shadowAsset.GetComponent<Renderer>().sharedMaterial = NotPlaceableShadowMaterial;
        }

        // Show the shadow asset as appropriate.
        if (position != Vector3.zero)
        {
            // Position the shadow a small distance from the target surface, along the normal.
            shadowAsset.transform.position = position + (0.01f * surfaceNormal);
            shadowAsset.SetActive(true);
        }
        else
        {
            shadowAsset.SetActive(false);
        }
    }

    /// <summary>
    /// Determines if two distance values should be considered equivalent. 
    /// </summary>
    /// <param name="d1">
    /// Distance to compare.
    /// </param>
    /// <param name="d2">
    /// Distance to compare.
    /// </param>
    /// <returns>
    /// True if the distances are within the desired tolerance, otherwise false.
    /// </returns>
    private bool IsEquivalentDistance(float d1, float d2)
    {
        float dist = Mathf.Abs(d1 - d2);
        return (dist <= distanceThreshold);
    }

    /// <summary>
    /// Called when the GameObject is unloaded.
    /// </summary>
    private void OnDestroy()
    {
        // Unload objects we have created.
        Destroy(boundsAsset);
        boundsAsset = null;
        Destroy(shadowAsset);
        shadowAsset = null;
    }
}
```

**Génération et déploiement**

* Comme précédemment, générez le projet et déployez sur HoloLens.
* Attendez la fin de l’analyse et du traitement des données de mappage spatiale.
* Lorsque vous voyez le système solaire, pointez le curseur en regard de la zone de projection ci-dessous et effectuez un mouvement de sélection pour le déplacer. Lorsque la zone de projection est sélectionnée, un cube englobant est visible autour de la zone de projection.
* Déplacez-vous vers le regard d’un autre endroit de la pièce. La zone de projection doit suivre votre point de regard. Lorsque l’ombre sous la zone de projection devient rouge, vous ne pouvez pas placer l’hologramme sur cette surface. Lorsque l’ombre sous la zone de projection devient verte, vous pouvez placer l’hologramme en effectuant un autre mouvement Select.
* Recherchez et sélectionnez l’une des affiches holographiques sur un mur pour la déplacer vers un nouvel emplacement. Notez que vous ne pouvez pas placer l’affiche à l’étage ou au plafond, et qu’il reste correctement orienté vers chaque mur au fur et à mesure que vous vous déplacez.

## <a name="chapter-5---occlusion"></a>Chapitre 5-occlusion

>[!VIDEO https://www.youtube.com/embed/6Xrzh_w-7SE]

**Cherché**

* Détermine si un hologramme est bloqués par le maillage de mappage spatial.
* Appliquez différentes techniques d’occlusion pour obtenir un effet amusant.

**Ample**

Tout d’abord, nous allons autoriser le maillage de mappage spatial à occultait d’autres hologrammes sans Boucher le monde réel :

* Dans le volet **hiérarchie** , sélectionnez l’objet **SpatialProcessing** .
* Dans le volet de l' **inspecteur** , recherchez le composant **Gestionnaire d’espace de lecture (script)** .
* Cliquez sur le cercle situé à droite de la propriété **matériau secondaire** .
* Recherchez et sélectionnez le matériel d' **occlusion** , puis fermez la fenêtre.

Nous allons ensuite ajouter un comportement spécial à la terre, afin qu’elle soit en surbrillance en bleu chaque fois qu’elle est bloqués par un autre hologramme (comme le soleil) ou par le maillage de mappage spatial :

* Dans le panneau **projet** , dans le dossier **hologrammes** , développez l’objet **SolarSystem** .
* Cliquez sur **terre**.
* Dans le panneau **inspecteur** , recherchez le matériau de la terre (composant le plus bas).
* Dans la **liste déroulante nuanceur**, remplacez le nuanceur par **personnalisé > OcclusionRim**. Cela permet d’afficher une surbrillance bleue autour de la terre chaque fois qu’elle est bloqués par un autre objet.

Enfin, nous allons activer un effet de vision x-ray pour les planètes dans notre système solaire. Nous devons modifier **PlanetOcclusion.cs** (qui se trouve dans le dossier Scripts\SolarSystem) afin d’obtenir les informations suivantes :

1. Déterminez si une planète est bloqués par la couche SpatialMapping (maillages et plans d’espace).
2. Affichez la représentation filaire d’une planète chaque fois qu’elle est bloqués par la couche SpatialMapping.
3. Masquer la représentation filaire d’une planète lorsqu’elle n’est pas bloquée par la couche SpatialMapping.

Suivez l’exercice de codage dans PlanetOcclusion.cs ou utilisez la solution suivante :

```cs
using UnityEngine;
using Academy.HoloToolkit.Unity;

/// <summary>
/// Determines when the occluded version of the planet should be visible.
/// This script allows us to do selective occlusion, so the occlusionObject
/// will only be rendered when a Spatial Mapping surface is occluding the planet,
/// not when another hologram is responsible for the occlusion.
/// </summary>
public class PlanetOcclusion : MonoBehaviour
{
    [Tooltip("Object to display when the planet is occluded.")]
    public GameObject occlusionObject;

    /// <summary>
    /// Points to raycast to when checking for occlusion.
    /// </summary>
    private Vector3[] checkPoints;

    // Use this for initialization
    void Start()
    {
        occlusionObject.SetActive(false);

        // Set the check points to use when testing for occlusion.
        MeshFilter filter = gameObject.GetComponent<MeshFilter>();
        Vector3 extents = filter.mesh.bounds.extents;
        Vector3 center = filter.mesh.bounds.center;
        Vector3 top = new Vector3(center.x, center.y + extents.y, center.z);
        Vector3 left = new Vector3(center.x - extents.x, center.y, center.z);
        Vector3 right = new Vector3(center.x + extents.x, center.y, center.z);
        Vector3 bottom = new Vector3(center.x, center.y - extents.y, center.z);

        checkPoints = new Vector3[] { center, top, left, right, bottom };
    }

    // Update is called once per frame
    void Update()
    {
        /* TODO: 5.a DEVELOPER CODING EXERCISE 5.a */

        // Check to see if any of the planet's boundary points are occluded.
        for (int i = 0; i < checkPoints.Length; i++)
        {
            // 5.a: Convert the current checkPoint to world coordinates.
            // Call gameObject.transform.TransformPoint(checkPoints[i]).
            // Assign the result to a new Vector3 variable called 'checkPt'.
            Vector3 checkPt = gameObject.transform.TransformPoint(checkPoints[i]);

            // 5.a: Call Vector3.Distance() to calculate the distance
            // between the Main Camera's position and 'checkPt'.
            // Assign the result to a new float variable called 'distance'.
            float distance = Vector3.Distance(Camera.main.transform.position, checkPt);

            // 5.a: Take 'checkPt' and subtract the Main Camera's position from it.
            // Assign the result to a new Vector3 variable called 'direction'.
            Vector3 direction = checkPt - Camera.main.transform.position;

            // Used to indicate if the call to Physics.Raycast() was successful.
            bool raycastHit = false;

            // 5.a: Check if the planet is occluded by a spatial mapping surface.
            // Call Physics.Raycast() with the following arguments:
            // - Pass in the Main Camera's position as the origin.
            // - Pass in 'direction' for the direction.
            // - Pass in 'distance' for the maxDistance.
            // - Pass in SpatialMappingManager.Instance.LayerMask as layerMask.
            // Assign the result to 'raycastHit'.
            raycastHit = Physics.Raycast(Camera.main.transform.position, direction, distance, SpatialMappingManager.Instance.LayerMask);

            if (raycastHit)
            {
                // 5.a: Our raycast hit a surface, so the planet is occluded.
                // Set the occlusionObject to active.
                occlusionObject.SetActive(true);

                // At least one point is occluded, so break from the loop.
                break;
            }
            else
            {
                // 5.a: The Raycast did not hit, so the planet is not occluded.
                // Deactivate the occlusionObject.
                occlusionObject.SetActive(false);
            }
        }
    }
}
```

**Génération et déploiement**

* Générez et déployez l’application dans HoloLens, comme d’habitude.
* Attendez la fin de l’analyse et du traitement des données de mappage spatiale (vous devriez voir apparaître des lignes bleues sur les murs).
* Recherchez et sélectionnez la zone de projection du système solaire, puis activez la case à cocher en regard d’un mur ou derrière un compteur.
* Vous pouvez afficher l’occlusion de base en masquant derrière les surfaces à l’homologue dans la zone d’affiche ou de projection.
* Si vous recherchez la terre, il doit y avoir un effet de surbrillance bleu lorsqu’il se trouve derrière un autre hologramme ou une autre surface.
* Regardez que les planètes se déplacent derrière le mur ou d’autres surfaces de la pièce. Vous avez maintenant une vision x-ray et vous pouvez voir leurs squelettes filaires !

## <a name="the-end"></a>La fin

Félicitations ! Vous avez maintenant terminé le **mappage spatial 230 : spatial**.

* Vous savez comment analyser votre environnement et charger des données de mappage spatiale sur Unity.
* Vous comprenez les notions de base des nuanceurs et comment les documents peuvent être utilisés pour revisualiser le monde.
* Vous avez appris les nouvelles techniques de traitement permettant de trouver des plans et de supprimer des triangles d’une maille.
* Vous avez pu déplacer et placer des hologrammes sur des surfaces qui ont été rendues logiques.
* Vous avez connu différentes techniques d’occlusion et vous avez utilisé la puissance de la vision x-ray !
