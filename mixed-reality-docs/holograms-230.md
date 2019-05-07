---
title: MR Spatial 230 - mappage Spatial
description: Suivez cette procédure pas à pas à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des concepts de mappage spatial de codage.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, didacticiel, mappage spatial, reconstruction aire de conception, de maillage
ms.openlocfilehash: ed58676a0fda660cc6b4c197239aeb53166baa4d
ms.sourcegitcommit: aa88f6b42aa8d83e43104b78964afb506a368fb4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/02/2019
ms.locfileid: "64993558"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-spatial-230-spatial-mapping"></a>MR 230 spatiale : Mappage spatial

[Mappage spatial](spatial-mapping.md) combine le monde réel et le monde virtuel par hologrammes sur l’environnement d’enseignement. Dans MR Spatial 230 (projet PLANÉTARIUM) nous apprendrons comment :

* Analyser l’environnement et transférer des données à partir de la HoloLens sur votre ordinateur de développement.
* Explorez les nuanceurs et découvrez comment les utiliser pour visualiser votre espace.
* Décomposer la maille de salle dans les plans simples à l’aide du traitement de la maille.
* Accédez au-delà les techniques de sélection élective que vous avez appris dans [101 des principes fondamentaux de M.](holograms-101.md)et fournir des commentaires sur où un hologramme peut être placé dans l’environnement.
* Explorez les effets de l’occlusion, donc lorsque votre hologramme est derrière un objet réel, vous pouvez le voir toujours avec vision rayons x !

>[!VIDEO https://www.youtube.com/embed/NSNYRkUX6Mw]

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>MR 230 spatiale : Mappage spatial</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).
* Base C# possibilité de programmation.
* Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-230-SpatialMapping.zip) requise par le projet. Nécessite Unity 2017.2 ou version ultérieure.
  * Si vous avez besoin de prise en charge de Unity 5.6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-230.zip).
  * Si vous avez besoin de prise en charge de Unity 5.5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-230.zip).
  * Si vous avez besoin de prise en charge de Unity 5.4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-230.zip).
* Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.

>[!NOTE]
>Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-230-SpatialMapping).

### <a name="notes"></a>Notes

* « Activer uniquement mon Code » dans Visual Studio doit être désactivée (*unchecked*) sous Outils > Options > débogage afin d’atteindre des points d’arrêt dans votre code.

## <a name="unity-setup"></a>Programme d’installation Unity

>[!VIDEO https://www.youtube.com/embed/y2Y4LhK6TEM]

* Démarrer **Unity**.
* Sélectionnez **New** pour créer un nouveau projet.
* Nommez le projet **PLANÉTARIUM**.
* Vérifiez que le **3D** paramètre est sélectionné.
* Cliquez sur **créer le projet**.
* Une fois Unity lance, accédez à **Modifier > Paramètres du projet > Lecteur**.
* Dans le **inspecteur** panneau, recherchez et sélectionnez le vert **Windows Store** icône.
* Développez **autres paramètres**.
* Dans le **rendu** section, vérifiez le **virtuel pris en charge de réalité** option.
* Vérifiez que **Windows HOLOGRAPHIQUE** apparaît dans la liste de **SDK de réalité virtuelle**. Dans le cas contraire, sélectionnez le **+** bouton en bas de la liste et choisissez **Windows HOLOGRAPHIQUE**.
* Développez **paramètres de publication**.
* Dans le **fonctionnalités** section, vérifiez les paramètres suivants :
    * InternetClientServer
    * PrivateNetworkClientServer
    * Microphone
    * SpatialPerception
* Accédez à **Modifier > Paramètres du projet > qualité**
* Dans le **inspecteur** panneau, sous l’icône Windows Store, sélectionnez la flèche noire de la liste déroulante sous la ligne « Default » et modifiez le paramètre par défaut pour **très faible**.
* Accédez à **actifs > Importer un Package > Package personnalisé**.
* Accédez à la **...\HolographicAcademy-Holograms-230-SpatialMapping\Starting** dossier.
* Cliquez sur **Planetarium.unitypackage**.
* Cliquez sur **Ouvrir**.
* Un **importer un Package Unity** fenêtre s’affiche, cliquez sur le **importation** bouton.
* Attendez que Unity importer toutes les ressources que nous devons mener à bien ce projet.
* Dans le **hiérarchie** panneau, supprimez le **Main Camera**.
* Dans le **projet** Panneau de configuration, **HoloToolkit-SpatialMapping-230\Utilities\Prefabs** dossier, recherchez le **Main Camera** objet.
* Faites glisser et déposez le **Main Camera** prefab dans le **hiérarchie** Panneau de configuration.
* Dans le **hiérarchie** panneau, supprimez le **lumière directionnelle** objet.
* Dans le **projet** Panneau de configuration, **Vntana** dossier, recherchez le **curseur** objet.
* Glisser -déplacer le **curseur** prefab dans le **hiérarchie**.
* Dans le **hiérarchie** Panneau de configuration, sélectionnez le **curseur** objet.
* Dans le **inspecteur** du panneau, cliquez sur le **couche** liste déroulante et sélectionnez **couches modifier...** .
* Nom **couche utilisateur 31** en tant que «**SpatialMapping**».
* Enregistrer la nouvelle scène : **Fichier > Enregistrer la scène sous...**
* Cliquez sur **nouveau dossier** et nommez le dossier **scènes**.
* Nommez le fichier «**PLANÉTARIUM**» et l’enregistrer dans le **scènes** dossier.

## <a name="chapter-1---scanning"></a>Chapitre 1 - analyse

>[!VIDEO https://www.youtube.com/embed/888oW51z_cE]

**Objectifs**
* Découvrez le SurfaceObserver et comment profiter de son impact sur les paramètres et les performances.
* Créer une salle d’expérience pour collecter les panneaux de votre espace d’analyse.

**Instructions**
* Dans le **projet** panneau **HoloToolkit-SpatialMapping-230\SpatialMapping\Prefabs** dossier, recherchez le **SpatialMapping** prefab.
* Glisser -déplacer le **SpatialMapping** prefab dans le **hiérarchie** Panneau de configuration.

**Générer et déployer (partie 1)**
* Dans Unity, sélectionnez **fichier > Paramètres de Build**.
* Cliquez sur **ajouter un arrière-plan Open** pour ajouter le **PLANÉTARIUM** scène à la build.
* Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.
* Définissez **SDK** à **universelle 10** et **Type de Build UWP** à **D3D**.
* Vérifiez **Unity C# projets**.
* Cliquez sur **Build**.
* Créer un **nouveau dossier** nommé « Application ».
* Clic le **application** dossier.
* Appuyez sur la **sélectionner le dossier** bouton.
* Quand Unity est terminé, création d’une fenêtre de l’Explorateur de fichiers s’affiche.
* Double-cliquez sur le **application** dossier pour l’ouvrir.
* Double-cliquez sur **Planetarium.sln** pour charger le projet dans Visual Studio.
* Dans Visual Studio, utilisez la barre d’outils supérieure pour modifier la Configuration à **version**.
* Modifier la plateforme à **x86**.
* Cliquez sur la flèche déroulante à droite de le « Ordinateur Local », puis sélectionnez **Machine distante**.
* Entrez [adresse IP de votre périphérique](connecting-to-wi-fi-on-hololens.md#identifying-the-ip-address-of-your-hololens-on-the-wi-fi-network) dans l’adresse du champ et modifier le Mode d’authentification à **universel (protocole non chiffré)**.
* Cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.
* Regardez la **sortie** panneau dans Visual Studio pour la génération et l’état du déploiement.
* Une fois que votre application a été déployée, Guide autour de la pièce. Vous verrez les surfaces environnantes couvertes par les mailles filaire noir et blanc.
* Analyser votre environnement. Veillez à examiner les murs, plafonds et étages.

**Générer et déployer (partie 2)**

Maintenant Examinons comment le mappage Spatial peut affecter les performances.
* Dans Unity, sélectionnez **fenêtre > Profiler**.
* Cliquez sur **ajouter Profiler > GPU**.
* Cliquez sur **Profiler Active > <Enter IP>** .
* Entrez le **adresse IP** de votre HoloLens.
* Cliquer sur **Se connecter**.
* Observez le nombre de millisecondes que nécessaire pour le GPU afficher un frame.
* Arrêter l’application de s’exécuter sur l’appareil.
* Revenez à Visual Studio et ouvrez **SpatialMappingObserver.cs**. Vous le trouverez dans le dossier HoloToolkit\SpatialMapping du projet d’Assembly-CSharp (Universal Windows).
* Rechercher la **Awake()** de fonction, puis ajoutez la ligne de code suivante : **TrianglesPerCubicMeter = 1200 ;**
* Redéployez le projet sur votre appareil, puis **reconnecter le profileur**. Observez la modification du nombre de millisecondes pour afficher un frame.
* Arrêter l’application de s’exécuter sur l’appareil.

**Enregistrer et charger dans Unity**

Enfin, nous allons enregistrer notre maillage salle et chargez-le dans Unity.
* Revenez à Visual Studio et supprimer le **TrianglesPerCubicMeter** ligne que vous avez ajouté dans le **Awake()** fonction lors de la section précédente.
* Redéployez le projet sur votre appareil. Nous devons maintenant être en cours d’exécution avec **500** triangles par mètre.
* Ouvrez un navigateur et entrez dans votre HoloLens IPAddress pour accéder à la **Windows Device Portal**.
* Sélectionnez le **affichage 3D** option dans le volet gauche.
* Sous **Surface reconstruction** sélectionner le **mise à jour** bouton.
* Observez que les zones que vous avez analysé sur votre HoloLens s’affichent dans la fenêtre d’affichage.
* Pour enregistrer votre analyse de la salle, appuyez sur la **enregistrer** bouton.
* Ouvrez votre **télécharge** dossier pour découvrir le modèle enregistré salle **SRMesh.obj**.
* Copie **SRMesh.obj** à la **actifs** dossier de votre projet Unity.
* Dans Unity, sélectionnez le **SpatialMapping** de l’objet dans le **hiérarchie** Panneau de configuration.
* Recherchez le **objet Observateur de Surface (Script)** composant.
* Cliquez sur le cercle à droite de la **salle modèle** propriété.
* Recherchez et sélectionnez le **SRMesh** de l’objet, puis fermez la fenêtre.
* Vérifiez que le **salle modèle** propriété dans le **inspecteur** Panneau de configuration est maintenant définie sur **SRMesh**.
* Appuyez sur la **lire** bouton pour passer en mode de prévisualisation d’Unity.
* Le composant SpatialMapping chargera les panneaux à partir du modèle de salle enregistré, vous pouvez les utiliser dans Unity.
* Basculez vers **scène** vue pour voir tous les de votre modèle de salle affiché avec le nuanceur filaire.
* Appuyez sur la **lire** bouton pour quitter le mode Aperçu.

**REMARQUE :** La prochaine fois que vous entrez le mode Aperçu dans Unity, il charge le maillage salle enregistré par défaut.

## <a name="chapter-2---visualization"></a>Chapitre 2 - visualisation

>[!VIDEO https://www.youtube.com/embed/RnkvXl-aXD4]

**Objectifs**
* Découvrez les principes fondamentaux de nuanceurs.
* Visualiser votre environnement.

**Instructions**
* Dans Unity **hiérarchie** Panneau de configuration, sélectionnez le **SpatialMapping** objet.
* Dans le **inspecteur** panneau, recherchez le **Manager mappage Spatial (Script)** composant.
* Cliquez sur le cercle à droite de la **matériau de Surface** propriété.
* Recherchez et sélectionnez le **BlueLinesOnWalls** matériau et fermer la fenêtre.
* Dans le **projet** panneau **nuanceurs** dossier, double-cliquez sur **BlueLinesOnWalls** pour ouvrir le nuanceur dans Visual Studio.
* Il s’agit d’un pixel simple (vertex pour fragmenter) nuanceur, ce qui permet d’effectuer les tâches suivantes :
    1. Convertit l’emplacement d’un sommet à l’espace universel.
    2. Vérifie que le vertex's normal pour déterminer si un pixel est vertical.
    3. Définit la couleur du pixel pour le rendu.

**Générer et déployer**
* Revenir à Unity, puis appuyez sur **lire** pour passer en mode Aperçu.
* Les lignes bleues seront affichera sur toutes les surfaces verticales de la maille de salle (qui chargés automatiquement à partir de nos données analyse enregistrées).
* Basculez vers le **scène** tab pour ajuster votre affichage de la salle et voir comment la maille local s’affiche dans Unity.
* Dans le **projet** panneau, recherchez le **matériaux** dossier et sélectionnez le **BlueLinesOnWalls** matériau.
* Modifier certaines propriétés et voir comment les modifications apparaissent dans l’éditeur Unity.
    * Dans le **inspecteur** panneau, ajustez le **LineScale** valeur pour que les lignes apparaissent épaisse ou plus étroit.
    * Dans le **inspecteur** panneau, ajustez le **LinesPerMeter** valeur pour modifier le nombre de lignes s’affichent sur chaque mur.
* Cliquez sur **lire** pour quitter le mode Aperçu.
* Créer et déployer à l’HoloLens et observer la façon dont le nuanceur de rendu apparaît sur les surfaces réels.

Unity fait un travail remarquable afficher un aperçu des documents, mais il est toujours une bonne idée au rendu de l’extraction dans l’appareil.

## <a name="chapter-3---processing"></a>Chapitre 3 - traitement

>[!VIDEO https://www.youtube.com/embed/kaUKiNiDxwY]

**Objectifs**
* Découvrez des techniques pour traiter les données de mappage spatial pour une utilisation dans votre application.
* Analyser les données de mappage spatial pour rechercher des plans et supprimer des triangles.
* Utiliser des plans pour la sélection élective hologramme.

**Instructions**
* Dans Unity **projet** Panneau de configuration, **hologrammes** dossier, recherchez le **SpatialProcessing** objet.
* Glisser -déplacer le **SpatialProcessing** de l’objet dans le **hiérarchie** Panneau de configuration.

Le préfabriqué SpatialProcessing inclut des composants pour traiter les données de mappage spatial. **SurfaceMeshesToPlanes.cs** recherche et générer des plans en fonction des données de mappage spatial. Nous allons utiliser des plans dans notre application pour représenter les sols, murs et les plafonds. Cette préfabriqué inclut également **RemoveSurfaceVertices.cs** qui peut supprimer des sommets de la maille de mappage spatial. Cela peut être utilisé pour créer des trous dans la maille, ou pour supprimer les triangles excessives qui ne sont plus nécessaires (car les plans peuvent être utilisés à la place).
* Dans Unity **projet** Panneau de configuration, **hologrammes** dossier, recherchez le **SpaceCollection** objet.
* Faites glisser et déposez le **SpaceCollection** de l’objet dans le **hiérarchie** Panneau de configuration.
* Dans le **hiérarchie** Panneau de configuration, sélectionnez le **SpatialProcessing** objet.
* Dans le **inspecteur** panneau, recherchez le **lire Gestionnaire d’espace (Script)** composant.
* Double-cliquez sur **PlaySpaceManager.cs** pour l’ouvrir dans Visual Studio.

PlaySpaceManager.cs contient le code spécifique à l’application. Nous allons ajouter des fonctionnalités à ce script pour activer le comportement suivant :
1. Arrêter la collecte des données de mappage spatial après que nous dépassent la limite de temps analyse (10 secondes).
2. Traiter les données de mappage spatial :
    1. Utilisez SurfaceMeshesToPlanes pour créer une représentation plus simple du monde en tant que plans (murs, étages, plafonds, etc.).
    2. Utilisez RemoveSurfaceVertices pour supprimer les triangles aire de conception qui se situent dans les limites de plan.
3. Générer une collection de hologrammes dans le monde et les placer sur des plans de mur et étage près de l’utilisateur.

Effectuer les exercices de codage marqués dans PlaySpaceManager.cs ou remplacez le script avec la solution terminée ci-dessous :

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

**Générer et déployer**
* Avant de déployer à l’HoloLens, appuyez sur la **lire** bouton dans Unity pour passer en mode lecture.
* Une fois le maillage de l’espace est chargé à partir du fichier, attendez 10 secondes avant le démarrage de traitement sur le maillage de mappage spatial.
* Lorsque le traitement est terminé, les plans seront affiche pour représenter le sol murs, ceiling, etc.
* Après tout des plans ont été trouvés, un système solaire doit s’afficher sur une table d’étage près de l’appareil photo.
* Deux posters doivent apparaître trop des murs près de l’appareil photo. Basculez vers le **scène** si vous ne pouvez pas les voir dans l’onglet **jeu** mode.
* Appuyez sur la **lire** bouton pour quitter le mode de lecture.
* Générez et déployez à l’HoloLens, comme d’habitude.
* Attendez la numérisation et le traitement des données de mappage spatial pour terminer.
* Une fois que vous voyez des plans, essayez de trouver le système solaire et affiches dans votre monde.

## <a name="chapter-4---placement"></a>Chapitre 4 - sélection élective

>[!VIDEO https://www.youtube.com/embed/Srhtpid1uZc]

**Objectifs**
* Déterminer si un hologramme s’ajusteront sur une surface.
* Fournir des commentaires à l’utilisateur lorsqu’un hologramme peut/ne tiennent pas sur une surface.

**Instructions**
* Dans Unity **hiérarchie** Panneau de configuration, sélectionnez le **SpatialProcessing** objet.
* Dans le **inspecteur** panneau, recherchez le **maillages de plans Surface (Script)** composant.
* Modifier le **dessiner les plans** propriété **rien** pour effacer la sélection.
* Modifier le **dessiner les plans** propriété **mur**, ce qui seront affichera uniquement les plans de mur.
* Dans le **projet** Panneau de configuration, **Scripts** dossier, double-cliquez sur **Placeable.cs** pour l’ouvrir dans Visual Studio.

Le **Placeable** script est déjà attaché à l’affiches projection boîte et qui sont créés après la recherche de plan. Il nous suffit est ne pas commenter du code, et ce script permettent d’obtenir les éléments suivants :
1. Déterminer si un hologramme s’ajusteront sur une surface par raycasting à partir du centre et les quatre coins du cube englobant.
2. Vérification de la surface normale pour déterminer si elle est suffisamment bon pour l’hologramme asseoir vidage.
3. Afficher un cube englobant autour de l’hologramme pour afficher sa taille réelle moment d’être placé.
4. Convertir une ombre sous/derrière le hologramme pour montrer où il sera placé sur le sol/mur.
5. Afficher l’ombre en rouge et si l’hologramme ne peut pas être placé sur la surface, ou vert, si possible.
6. Réorienter l’hologramme pour s’aligner avec le type de surface (vertical ou horizontal) qu’il possède une affinité avec.
7. Placer correctement l’hologramme sur la surface sélectionnée afin d’éviter le moment du saut ou le comportement d’alignement.

Supprimez les commentaires de tout le code dans l’exercice de codage ci-dessous, ou utiliser cette solution terminée dans **Placeable.cs**:

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
    /// The aligntoVerticalSurface parameter is ignored if the object
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

**Générer et déployer**
* Comme précédemment, générez le projet et déployer sur le HoloLens.
* Attendez la numérisation et le traitement des données de mappage spatial pour terminer.
* Lorsque vous voyez le système solaire, à la zone de projection sous les regards et effectuer un mouvement sélectionnez Déplacer au sein. Alors que la zone de projection est sélectionnée, un cube englobant sera visible autour de la zone de projection.
* Vous déplacer head pour utilisation dans un autre emplacement dans la salle. La zone de projection doit suit votre regard. Lors de l’ombre sous la zone de projection devient rouge, vous ne pouvez pas placer l’hologramme sur cette surface. Lors de l’ombre sous la zone de projection devient verte, vous pouvez placer l’hologramme en effectuant des mouvements de sélectionner un autre.
* Recherchez et sélectionnez une des affiches HOLOGRAPHIQUE sur un mur pour le déplacer vers un nouvel emplacement. Notez que vous ne pouvez pas placer l’affiche sur le plancher ou le plafond, et qu’elle reste correctement orienté vers chaque mur que vous déplacez.

## <a name="chapter-5---occlusion"></a>Chapitre 5 - Occlusion

>[!VIDEO https://www.youtube.com/embed/6Xrzh_w-7SE]

**Objectifs**
* Déterminer si un hologramme est bloqué par la maille de mappage spatial.
* Appliquer des techniques d’occlusion différentes pour atteindre un plaisir effet.

**Instructions**

Tout d’abord, nous allons autoriser la maille de mappage spatial occlude autres hologrammes sans OCCLUSION le monde réel :
* Dans le **hiérarchie** Panneau de configuration, sélectionnez le **SpatialProcessing** objet.
* Dans le **inspecteur** panneau, recherchez le **lire Gestionnaire d’espace (Script)** composant.
* Cliquez sur le cercle à droite de la **matériau secondaire** propriété.
* Recherchez et sélectionnez le **Occlusion** matériau et fermer la fenêtre.

Ensuite, nous allons ajouter un comportement spécial à terre, afin qu’il ait une surbrillance bleue chaque fois qu’il devienne bloqué par un autre hologramme (par exemple, le soleil), ou par la maille de mappage spatial :
* Dans le **projet** volet le **Vntana** dossier, développez le **SolarSystem** objet.
* Cliquez sur **Earth**.
* Dans le **inspecteur** panel, trouver les documents de la terre (composant du bas).
* Dans le **déroulante nuanceur**, modifier le nuanceur **personnalisé > OcclusionRim**. Cela affichera une surbrillance bleue autour de la terre chaque fois qu’il est bloqué par un autre objet.

Enfin, nous allons activer un effet de vision x-Ray pour planètes dans notre système solaire. Nous devons modifier **PlanetOcclusion.cs** (figurant dans le dossier Scripts\SolarSystem) afin d’atteindre les objectifs suivants :
1. Déterminer si une planète est bloquée par la couche de SpatialMapping (salle mailles et plans).
2. Afficher la représentation sous forme de maquette d’une planète chaque fois qu’il est bloqué par la couche SpatialMapping.
3. Masquer la représentation sous forme de maquette d’une planète lorsqu’il n’est pas bloqué par la couche SpatialMapping.

Suivez l’exercice de codage dans PlanetOcclusion.cs, ou utiliser la solution suivante :

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

**Générer et déployer**
* Générer et déployer l’application sur HoloLens, comme d’habitude.
* Attendre que l’analyse et le traitement des données spatiales de mappage complet (vous devez voir les lignes bleues apparaissent sur les murs).
* Recherchez et sélectionnez la zone de projection du système solaire puis définissez la zone en regard d’un mur ou derrière un compteur.
* Vous pouvez afficher l’occlusion base en se cachant derrière les surfaces à homologuer à la zone affiche ou de projection.
* Recherchez la terre, il doit y avoir un effet de la surbrillance bleue chaque fois qu’il va derrière un autre hologramme ou surface.
* Écoutez les planètes déplacement derrière le mur ou autres surfaces dans la salle. Vous avez vision rayons x et pourrez voir leurs squelettes filaire !

## <a name="the-end"></a>La fin

Félicitations ! Vous avez maintenant terminé **230 Spatial MR : Mappage spatial**.
* Vous savez comment analyser vos données d’environnement et charge le mappage spatial à Unity.
* Vous comprenez les principes fondamentaux de nuanceurs et utilisation des supports pour visualiser de nouveau le monde.
* Vous avez appris de nouvelles techniques de traitement pour trouver des plans et la suppression des triangles à partir d’une maille.
* Vous avez pu déplacer et placer hologrammes sur les surfaces qui était logique.
* Vous a rencontré des techniques différentes occlusion et d’exploiter la puissance de vision rayons x !
