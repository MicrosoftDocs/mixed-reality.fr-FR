---
title: Modèle d’application
description: Windows Mixed Reality utilise le modèle d’application fourni par le plateforme Windows universelle, un modèle et un environnement pour les applications Windows modernes.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: UWP, modèle d’application, cycle de vie, suspendre, reprendre, vignette, vues, contrats
ms.openlocfilehash: 5dc84122e591e7d91657b6f8eadf6eb947f2d706
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63517406"
---
# <a name="app-model"></a>Modèle d’application

Windows Mixed Reality utilise le modèle d’application fourni par le [plateforme Windows universelle](https://docs.microsoft.com/windows/uwp/get-started/) (UWP), un modèle et un environnement pour les applications Windows modernes. Le modèle d’application UWP définit la manière dont les applications sont installées, mises à jour, gérées par version et supprimées en toute sécurité. Elle régit le cycle de vie de l’application: la manière dont les applications s’exécutent, se mettent en veille et se terminent, et comment elles peuvent préserver l’État. Il couvre également l’intégration et l’interaction avec le système d’exploitation, les fichiers et d’autres applications.

![applications 2D organisées dans la page d’hébergement de la réalité Windows Mixed dans une zone de petit-déjeuner](images/20160112-055908-hololens-500px.jpg)<br>
*Applications avec une vue 2D organisée dans la page d’hébergement de Windows Mixed Reality*

## <a name="app-lifecycle"></a>Cycle de vie de l’application

Le cycle de vie d’une application de réalité mixte implique des concepts d’application standard tels que le placement, le lancement, l’arrêt et la suppression.

### <a name="placement-is-launch"></a>Le placement est lancé

Chaque application démarre en réalité mixte en plaçant une vignette d’application (juste une [vignette secondaire Windows](https://docs.microsoft.com/uwp/api/Windows.UI.StartScreen.SecondaryTile)) dans la page d’hébergement de la [réalité mixte Windows](navigating-the-windows-mixed-reality-home.md). Ces vignettes d’application, au positionnement, commencent à exécuter l’application. Ces vignettes d’application sont conservées et restent à l’emplacement où elles sont placées, agissant comme des lanceurs à chaque fois que vous souhaitez revenir à l’application.

![Placement place une vignette secondaire dans le monde](images/slide1-600px.png)<br>
*Placement place une vignette secondaire dans le monde*

Dès que l’emplacement est terminé (sauf si l’emplacement a été démarré par une [application au lancement de l’application](app-model.md#protocols) ), l’application démarre le lancement. Windows Mixed Reality peut exécuter un nombre limité d’applications en même temps. Dès que vous placez et lancez une application, d’autres applications actives peuvent s’interrompre, laissant une capture d’écran du dernier état de l’application sur sa vignette d’application où vous l’avez placée. Pour plus d’informations sur la gestion de la reprise et d’autres événements de cycle de vie des applications, consultez [cycle de vie des applications UWP Windows 10](https://docs.microsoft.com/windows/uwp/launch-resume/app-lifecycle) .

![Après avoir placé une vignette, l’application démarre](images/slide2-500px.png) le diagramme d’État en ![cours d’exécution pour l’application en cours d’exécution, suspendue ou non exécutée](images/ic576232-500px.png)<br>
*Left: après avoir placé une vignette, l’application commence à s’exécuter. Right: diagramme d’état de l’application en cours d’exécution, suspendue ou non exécutée.*

### <a name="remove-is-closeterminate-process"></a>Le processus de suppression est fermer/terminer

Lorsque vous supprimez une vignette d’application placée du monde entier, les processus sous-jacents sont fermés. Cela peut être utile pour s’assurer que votre application est terminée ou redémarrer une application problématique.

### <a name="app-suspensiontermination"></a>Interruption/arrêt de l’application

Dans la [page d’hébergement de la réalité mixte de Windows](navigating-the-windows-mixed-reality-home.md), l’utilisateur est en mesure de créer plusieurs points d’entrée pour une application. Pour ce faire, ils lancent votre application à partir du menu Démarrer et placent la vignette de l’application dans le monde. Chaque vignette d’application se comporte comme un point d’entrée différent et a une instance de vignette distincte dans le système. Une requête pour [SecondaryTile. FindAllAsync](https://docs.microsoft.com/uwp/api/Windows.UI.StartScreen.SecondaryTile#Windows_UI_StartScreen_SecondaryTile_FindAllAsync) entraîne un **SecondaryTile** pour chaque instance d’application.

Quand une application UWP s’interrompt, une capture d’écran est prise de l’état actuel.

![Des captures d’écran s’affichent pour les applications suspendues](images/slide9-800px.png)<br>
*Des captures d’écran s’affichent pour les applications suspendues*

L’une des principales différences par rapport aux autres shells Windows 10 est la façon dont l’application est informée de l’activation d’une instance d’application via les événements [CoreApplication.](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Core.CoreApplication#Windows_ApplicationModel_Core_CoreApplication_Resuming) Reforming et [CoreWindow. Activated](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow#Windows_UI_Core_CoreWindow_Activated) .

|  Scénario |  Reprise  |  Actif | 
|----------|----------|----------|
|  Lancer une nouvelle instance de l’application à partir du menu Démarrer  |   |  **Activé** avec un nouveau [TileId](https://docs.microsoft.com/uwp/api/windows.ui.startscreen.secondarytile#Windows_UI_StartScreen_SecondaryTile_TileId) | 
|  Lancer la seconde instance de l’application à partir du menu Démarrer  |   |  **Activé** avec un nouveau **TileId** | 
|  Sélectionnez l’instance de l’application qui n’est pas actuellement active  |   |  **Activé** avec le **TileId** associé à l’instance | 
|  Sélectionnez une autre application, puis sélectionnez l’instance précédemment active  |  **Reprise** déclenchée  |  | 
|  Sélectionnez une autre application, puis sélectionnez l’instance qui était précédemment inactive  |  **Reprise** déclenchée  |  Ensuite **activé** avec le **TileId** associé à l’instance | 

### <a name="extended-execution"></a>Exécution étendue

Parfois, votre application doit continuer à travailler en arrière-plan ou à exécuter des données audio. Les [tâches en arrière-plan](https://docs.microsoft.com/windows/uwp/launch-resume/declare-background-tasks-in-the-application-manifest) sont disponibles sur HoloLens.

![Les applications peuvent s’exécuter en arrière-plan](images/slide10-800px.png)<br>
*Les applications peuvent s’exécuter en arrière-plan*

## <a name="app-views"></a>Vues d’applications

Lorsque votre application est activée, vous pouvez choisir le type de vue que vous souhaitez afficher. Pour le **CoreApplication**d’une application, il existe toujours une [vue d’application](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationView) principale et un nombre quelconque d’autres affichages d’application que vous souhaitez créer. Sur le bureau, vous pouvez considérer une vue d’application comme une fenêtre. Nos modèles d’application de réalité mixte créent un projet Unity dans lequel la vue d’application principale est [immersive](app-views.md). 

Votre application peut créer une vue d’application 2D supplémentaire à l’aide de technologies telles que XAML, pour utiliser les fonctionnalités Windows 10 telles que l’achat dans l’application. Si votre application a démarré en tant qu’application UWP pour d’autres appareils Windows 10, votre vue principale est 2D, mais vous pouvez la «allumer» en réalité mixte en ajoutant une vue d’application supplémentaire qui est immersive pour montrer une expérience volumétrique. Imaginez la création d’une application de visionneuse de photos en XAML où le bouton de diaporama bascule vers une vue d’application immersif qui Flew des photos à partir de l’application dans le monde entier et des surfaces.

![L’application en cours d’exécution peut avoir une vue 2D ou une vue immersive](images/slide3-800px.png)<br>
*L’application en cours d’exécution peut avoir une vue 2D ou une vue immersive*

### <a name="creating-an-immersive-view"></a>Création d’une vue immersive

Les applications de réalité mixte sont celles qui créent une vue immersive, qui est obtenue avec le type [HolographicSpace](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace) .

Une application qui est purement immersive doit toujours créer une vue immersive au lancement, même si elle est lancée à partir du bureau. Les vues immersives s’affichent toujours dans le casque, quel que soit l’emplacement à partir duquel elles ont été créées. L’activation d’une vue immersive permet d’afficher le portail de réalité mixte et de guider l’utilisateur sur son casque.

Une application qui commence par une vue 2D sur le moniteur de bureau peut créer une vue immersive secondaire pour afficher le contenu du casque. C’est le cas, par exemple, d’une fenêtre de périphérie 2D sur le moniteur affichant une vidéo de 360 degrés dans le casque.

![Les applications qui s’exécutent en mode immersif sont les seules visibles](images/slide4-800px.png)<br>
*Une application en cours d’exécution dans une vue immersive est la seule visible*

### <a name="2d-view-in-the-windows-mixed-reality-home"></a>vue 2D dans la page d’hébergement de Windows Mixed Reality

Tout autre chose qu’une vue immersive est rendue sous la forme d’une vue 2D dans votre monde.

Une application peut avoir des vues 2D à la fois sur le moniteur de bureau et dans le casque. Notez qu’une nouvelle vue 2D sera placée dans le même Shell que la vue qui l’a créée, soit sur le moniteur, soit sur le casque. Il n’est pas actuellement possible pour une application ou un utilisateur de déplacer une vue 2D entre la réalité mixte et le moniteur.

![Les applications qui s’exécutent dans la vue 2D partagent l’espace dans le monde mixte avec d’autres applications](images/slide5-800px.png)<br>
*Les applications qui s’exécutent dans une vue 2D partagent l’espace avec d’autres applications*

### <a name="placement-of-additional-app-tiles"></a>Positionnement des vignettes d’application supplémentaires

Vous pouvez placer autant d’applications avec une vue 2D dans votre monde que vous le souhaitez avec les [API de vignette secondaires](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/secondary-tiles). Ces vignettes «épinglées» s’affichent sous forme d’écrans d’accueil que les utilisateurs doivent placer et peuvent ensuite utiliser pour lancer votre application. Windows Mixed Reality ne prend actuellement pas en charge le rendu d’un contenu de vignette 2D sous forme de vignettes dynamiques.

![Les applications peuvent avoir plusieurs placements à l’aide de vignettes secondaires](images/slide6-800px.png)<br>
*Les applications peuvent avoir plusieurs placements à l’aide de vignettes secondaires*

### <a name="switching-views"></a>Basculement des vues

#### <a name="switching-from-the-2d-xaml-view-to-the-immersive-view"></a>Passage de la vue XAML 2D à la vue immersif

Si l’application utilise du code XAML, le [IFRAMEWORKVIEWSOURCE](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkviewsource) XAML contrôle la première vue de l’application. L’application devra basculer vers la vue immersive avant d’activer le **CoreWindow**pour s’assurer que l’application démarre directement dans l’expérience immersive.

Utilisez [CoreApplication. CreateNewView](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Core.CoreApplication#Windows_ApplicationModel_Core_CoreApplication_CreateNewView_Windows_ApplicationModel_Core_IFrameworkViewSource_) et [ApplicationViewSwitcher. SwitchAsync](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationViewSwitcher#Windows_UI_ViewManagement_ApplicationViewSwitcher_SwitchAsync_System_Int32_) pour en faire la vue active.

> [!NOTE]
>* Ne spécifiez pas l’indicateur [ApplicationViewSwitchingOptions. ConsolidateViews](https://docs.microsoft.com/uwp/api/windows.ui.viewmanagement.applicationviewswitchingoptions) à **SwitchAsync** lors du passage de la vue XAML à la vue immersif, ou la ardoise qui a lancé l’application sera supprimée du monde entier.
>* **SwitchAsync** doit être appelé à l’aide du [répartiteur](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow#Windows_UI_Core_CoreWindow_Dispatcher) associé à l’affichage dans lequel vous passez.
>* Vous devrez **SwitchAsync** la vue XAML si vous devez lancer un clavier virtuel ou si vous souhaitez activer une autre application.

![Les applications peuvent basculer entre les vues 2D et](images/slide7-600px.png) les vues ![immersives quand une application passe dans une vue immersive, le monde mixte et d’autres applications disparaissent](images/slide8-600px.png)<br>
*Gauche: les applications peuvent basculer entre la vue 2D et l’affichage immersif. Droite: quand une application passe dans une vue immersive, la page d’hébergement de la réalité mixte Windows et d’autres applications disparaissent.*

#### <a name="switching-from-the-immersive-view-back-to-a-keyboard-xaml-view"></a>Basculement de la vue immersive vers une vue XAML de clavier

Une raison courante du basculement entre les vues est l’affichage d’un clavier dans une application de réalité mixte. L’interpréteur de commandes ne peut afficher le clavier système que si l’application affiche une vue 2D. Si l’application doit obtenir une entrée de texte, elle peut fournir une vue XAML personnalisée avec un champ d’entrée de texte, basculer vers celle-ci, puis revenir en arrière une fois l’entrée terminée.

Comme dans la section précédente, vous pouvez utiliser **ApplicationViewSwitcher. SwitchAsync** pour basculer vers une vue XAML à partir de votre vue immersif.

## <a name="app-size"></a>Taille de l’application

les vues d’application 2D s’affichent toujours dans une ardoise virtuelle fixe. Ainsi, toutes les vues 2D affichent exactement la même quantité de contenu. Voici des informations supplémentaires sur la taille de la vue 2D de votre application:
* Les proportions de l’application sont conservées pendant le redimensionnement.
* La [résolution et le facteur d’échelle](building-2d-apps.md#2d-app-view-resolution-and-scale-factor) de l’application ne sont pas modifiés par le redimensionnement.
* Les applications ne sont pas en mesure d’interroger leur taille réelle dans le monde.

![les applications 2D s’affichent avec des tailles de fenêtre fixes](images/12493521-10104043956964683-6118765685995662420-o-500px.jpg)<br>
*Les applications avec une vue 2D apparaissent avec des tailles de fenêtre fixes*

## <a name="app-tiles"></a>Vignettes d’application

Le menu Démarrer utilise la petite vignette standard et la vignette moyenne pour les codes confidentiels et la liste **toutes les applications** en réalité mixte. 

![Menu Démarrer pour Windows Mixed Reality](images/start-500px.png)<br>
*Menu Démarrer pour Windows Mixed Reality*

## <a name="app-to-app-interactions"></a>Interactions entre l’application et l’application

Lorsque vous créez des applications, vous avez accès aux mécanismes de communication de l’application enrichie aux applications disponibles sur Windows 10. La plupart des nouvelles API de protocole et des inscriptions de fichiers fonctionnent parfaitement sur HoloLens pour permettre le lancement et la communication de l’application. 

Notez que pour les casques de bureau, l’application associée à une extension de fichier ou un protocole donné peut être une application Win32 qui peut uniquement apparaître sur le moniteur du bureau ou dans la tablette du bureau.

### <a name="protocols"></a>Protocoles

HoloLens prend en charge l’application pour le lancement d’applications via les [API Windows. System. Launcher](https://docs.microsoft.com/uwp/api/Windows.System.Launcher).

Voici quelques éléments à prendre en compte lors du lancement d’une autre application:

* Quand vous procédez à un lancement non modal, tel que [LaunchUriAsync](https://docs.microsoft.com/uwp/api/Windows.System.Launcher#Windows_System_Launcher_LaunchUriAsync_Windows_Foundation_Uri_), l’utilisateur doit placer l’application avant d’interagir avec elle.

* Quand vous exécutez un lancement modal, par exemple par le biais de [LaunchUriForResultsAsync](https://docs.microsoft.com/uwp/api/Windows.System.Launcher#Windows_System_Launcher_LaunchUriForResultsAsync_Windows_Foundation_Uri_Windows_System_LauncherOptions_Windows_Foundation_Collections_ValueSet_), l’application modale est placée en haut de la fenêtre.

* Windows Mixed Reality ne peut pas superposer des applications par-dessus les vues exclusives. Pour afficher l’application lancée, Windows ramène l’utilisateur au monde entier pour afficher l’application.

### <a name="file-pickers"></a>Sélecteurs de fichiers

HoloLens prend en charge les contrats [FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) et [FileSavePicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) . Toutefois, aucune application n’est préinstallée et ne respecte pas les contrats de sélecteur de fichiers. Ces applications (par exemple, OneDrive) peuvent être installées à partir du Microsoft Store.

Si plusieurs applications de sélecteur de fichiers sont installées, vous ne verrez aucune interface utilisateur de désambiguïsation pour choisir l’application à lancer. au lieu de cela, le premier sélecteur de fichiers installé est choisi. Lors de l’enregistrement d’un fichier, le nom de fichier est généré, ce qui comprend l’horodateur. Cela ne peut pas être modifié par l’utilisateur.

Par défaut, les extensions suivantes sont prises en charge localement:

|  Application  |  Extensions | 
|----------|----------|
|  Photos  |  BMP, GIF, jpg, png, AVI, MOV, MP4, WMV | 
|  Microsoft Edge  |  htm, html, PDF, SVG, XML | 

### <a name="app-contracts-and-windows-mixed-reality-extensions"></a>Contrats d’application et extensions Windows Mixed Reality

Les contrats d’application et les points d’extension vous permettent d’inscrire votre application pour tirer parti des fonctionnalités plus profondes du système d’exploitation, telles que la gestion d’une extension de fichier ou l’utilisation de tâches en arrière-plan. Il s’agit d’une liste des contrats et des points d’extension pris en charge et non pris en charge sur HoloLens.

|  Contrat ou extension  |  Géré? | 
|----------|----------|
| [Fournisseur d’images de compte (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#account_picture_provider) | Non pris en charge | 
| [Tent](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#alarm) | Non pris en charge | 
| [App service](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#app_service) | Pris en charge, mais pas entièrement fonctionnel | 
| [Fournisseur de rendez-vous](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#appointmnets_provider) | Non pris en charge | 
| [Lecture automatique (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#autoplay) | Non pris en charge | 
| [Tâches en arrière-plan (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#background_tasts) | Partiellement pris en charge (tous les déclencheurs ne fonctionnent pas) | 
| [Tâche de mise à jour (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#update_task) | Pris en charge | 
| [Contrat de mise à jour de fichier mis en cache](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#cached_file_updater) | Pris en charge | 
| [Paramètres de l’appareil photo (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#camera_settings) | Non pris en charge | 
| [Protocole de numérotation](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#dial_protocol) | Non pris en charge | 
| [Activation de fichier (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#file_activation) | Pris en charge | 
| [Contrat de sélecteur de fichier ouvert](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#file_open_picker_contract) | Pris en charge | 
| [Contrat de sélecteur d’enregistrement de fichier](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#file_save_picker_contract) | Pris en charge | 
| [Appel de l’écran de verrouillage](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#lock_screen_call) | Non pris en charge | 
| [Lecture de contenu multimédia](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#media_playback) | Non pris en charge | 
| [Lire le contrat](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#playto_contract) | Non pris en charge | 
| [Tâche de configuration préinstallée](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#preinstalled_config_task) | Non pris en charge | 
| [Imprimer un flux de travail 3D](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#print_3d_workflow) | Pris en charge | 
| [Imprimer les paramètres de tâche (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#print_task_settings) | Non pris en charge | 
| [Activation d’URI (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#protocol_activation) | Pris en charge | 
| [Lancement restreint](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#restricted_launch) | Non pris en charge | 
| [Rechercher un contrat](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#search_contract) | Non pris en charge | 
| [Contrat de paramètres](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#settings_contract) | Non pris en charge | 
| [Partager le contrat](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#share_contract) | Non pris en charge | 
| [SSL/certificats (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#ssl_certificates) | Pris en charge | 
| [Fournisseur de comptes Web](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#web_account_provider) | Pris en charge | 

## <a name="app-file-storage"></a>Stockage de fichiers d’application

Tout le stockage s’effectue par le biais de l' [espace de noms Windows. Storage](https://docs.microsoft.com/uwp/api/Windows.Storage). Pour plus d’informations, consultez la documentation suivante. HoloLens ne prend pas en charge la synchronisation/l’itinérance du stockage d’application.

* [Fichiers, dossiers et bibliothèques](https://docs.microsoft.com/windows/uwp/files/index)
* [Stocker et récupérer des paramètres et autres données d’application](https://docs.microsoft.com/windows/uwp/design/app-settings/store-and-retrieve-app-data)

### <a name="known-folders"></a>Dossiers connus

Pour plus d’informations sur les applications UWP, consultez [fichier KnownFolders](https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders) .

<table>
<tr>
<th> Propriété</th><th> Pris en charge sur HoloLens</th><th> Pris en charge sur les casques immersifs</th><th> Description</th>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_AppCaptures">AppCaptures</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier de captures de l’application.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_CameraRoll">CameraRoll</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier du rouleau de l’appareil photo.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_DocumentsLibrary">DocumentsLibrary</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient la bibliothèque de documents. La bibliothèque de documents n’est pas destinée à une utilisation générale.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_MusicLibrary">MusicLibrary</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient la bibliothèque musicale.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_Objects3D">Objects3D</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier 3D d’objets.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_PicturesLibrary">PicturesLibrary</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient la bibliothèque d’images.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_Playlists">Sélections</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier de listes de lecture.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_SavedPictures">SavedPictures</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier images enregistrées.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_VideosLibrary">VideosLibrary</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient la bibliothèque de vidéos.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_HomeGroup">Résidentiel</a></td><td></td><td style="text-align: center;">✔️</td><td>Obtient le dossier du groupe résidentiel.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_MediaServerDevices">MediaServerDevices</a></td><td></td><td style="text-align: center;">✔️</td><td>Obtient le dossier des appareils Media Server (Digital vivant Network Alliance (DLNA)).</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_RecordedCalls">RecordedCalls</a></td><td></td><td style="text-align: center;">✔️</td><td>Obtient le dossier des appels enregistrés.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_RemovableDevices">RemovableDevices</a></td><td></td><td style="text-align: center;">✔️</td><td>Obtient le dossier des appareils amovibles.</td>
</tr>
</table>

## <a name="app-package"></a>Package de l’application

Avec Windows 10, vous ne ciblez plus un système d’exploitation, mais vous [Ciblez votre application sur une ou plusieurs familles d’appareils](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide#device-families). Une famille d’appareils identifie les API, les caractéristiques système et les comportements que vous pouvez attendre sur les différents appareils de cette famille. Il détermine également l’ensemble des appareils sur lesquels votre application peut être installée à partir de l' [Microsoft Store](submitting-an-app-to-the-microsoft-store.md#specifying-target-device-families).

* Pour cibler à la fois les casques de bureau et HoloLens, ciblez votre application sur la famille de périphériques **Windows. Universal** .
* Pour cibler uniquement des casques de bureau, ciblez votre application sur la famille de périphériques **Windows. Desktop** .
* Pour cibler uniquement HoloLens, ciblez votre application sur la famille d’appareils **Windows. holographique** .

## <a name="see-also"></a>Voir aussi

* [Vues d’applications](app-views.md)
* [Mise à jour des applications UWP 2D pour la réalité mixte](building-2d-apps.md)
* [Guide de conception du lanceur d’applications 3D](3d-app-launcher-design-guidance.md)
* [Implémentation des lanceurs d’applications 3D](implementing-3d-app-launchers.md)
