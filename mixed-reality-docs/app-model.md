---
title: Modèle d’application
description: Réalité mixte Windows utilise le modèle d’application fourni par la plateforme Windows universelle, un modèle et l’environnement pour les applications Windows modernes.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: UWP, le modèle d’application, le cycle de vie, suspendre, reprendre, vignette, vues et contrats
ms.openlocfilehash: 5dc84122e591e7d91657b6f8eadf6eb947f2d706
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595855"
---
# <a name="app-model"></a>Modèle d’application

Réalité mixte Windows utilise le modèle d’application fourni par le [plateforme Windows universelle](https://docs.microsoft.com/windows/uwp/get-started/) (UWP), un modèle et l’environnement pour les applications Windows modernes. Le modèle d’application UWP définit comment les applications sont installées, mis à jour, avec contrôle de version et supprimé en toute sécurité et complètement. Elle régit le cycle de vie d’application - comment applications execute, mise en veille et terminent - et comment ils peuvent conserver l’état. Il couvre également l’intégration et l’interaction avec le système d’exploitation, les fichiers et les autres applications.

![Applications 2D organisées en réalité mixte Windows accueil dans une zone de petit déjeuner](images/20160112-055908-hololens-500px.jpg)<br>
*Applications avec une vue en 2D organisés dans la réalité mixte Windows domestique*

## <a name="app-lifecycle"></a>Cycle de vie de l’application

Le cycle de vie d’une application de réalité mixte implique les concepts d’application standard telles que la sélection élective, lancement, arrêt et suppression.

### <a name="placement-is-launch"></a>Le positionnement est lancement

Chaque application démarre en réalité mixte en plaçant une vignette de l’application (juste un [vignette secondaire Windows](https://docs.microsoft.com/uwp/api/Windows.UI.StartScreen.SecondaryTile)) dans le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md). Ces vignettes de l’application, sur la sélection élective, démarre l’application en cours d’exécution. Ces vignettes des applications conserver et à rester à l’emplacement où ils sont placés, agissant comme lanceurs pour chaque fois que vous souhaitez revenir à l’application.

![Sélection élective place une vignette secondaire dans le monde](images/slide1-600px.png)<br>
*Sélection élective place une vignette secondaire dans le monde*

Dès que la sélection élective termine (sauf si le positionnement a été démarré par un [une application vers](app-model.md#protocols) lancer), l’application démarre le lancement. Réalité mixte Windows peut exécuter un nombre limité d’applications en même temps. Dès que vous placez et lancez une application, les autres applications actives peuvent suspendre, en laissant une capture d’écran du dernier état de l’application sur sa vignette de l’application chaque fois que vous l’avez placé. Consultez [cycle de vie des applications UWP Windows 10](https://docs.microsoft.com/windows/uwp/launch-resume/app-lifecycle) pour plus d’informations sur la gestion des reprise et autres événements de cycle de vie d’application.

![Après avoir ajouté une vignette, l’application commence à s’exécuter](images/slide2-500px.png) ![diagramme d’état de l’application en cours d’exécution, suspendu ou pas en cours d’exécution](images/ic576232-500px.png)<br>
*Gauche : après avoir ajouté une vignette, l’application commence à s’exécuter. Droite : diagramme d’état pour l’application en cours d’exécution, suspendues ou pas en cours d’exécution.*

### <a name="remove-is-closeterminate-process"></a>Remove consiste à fermer/arrêt

Lorsque vous supprimez une vignette de l’application placé dans le monde, cela ferme les processus sous-jacents. Cela peut être utile pour s’assurer de que votre application est arrêtée ou le redémarrage d’une application problématique.

### <a name="app-suspensiontermination"></a>Application suspension/arrêt

Dans le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md), l’utilisateur est en mesure de créer plusieurs points d’entrée pour une application. Ils cela en lançant votre application à partir du menu Démarrer et en plaçant la vignette de l’application dans le monde. Chaque vignette de l’application se comporte comme un point d’entrée différents et dispose d’une instance de la vignette séparées dans le système. Une requête pour [SecondaryTile.FindAllAsync](https://docs.microsoft.com/uwp/api/Windows.UI.StartScreen.SecondaryTile#Windows_UI_StartScreen_SecondaryTile_FindAllAsync) entraîne une **SecondaryTile** pour chaque instance d’application.

Lorsqu’une application UWP suspend, une capture d’écran provient de l’état actuel.

![Captures d’écran sont indiquées pour les applications suspendues](images/slide9-800px.png)<br>
*Captures d’écran sont indiquées pour les applications suspendues*

Une différence essentielle à partir d’autres interpréteurs de commandes Windows 10 est la façon dont l’application est informée d’une activation d’instance application via le [CoreApplication.Resuming](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Core.CoreApplication#Windows_ApplicationModel_Core_CoreApplication_Resuming) et [CoreWindow.Activated](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow#Windows_UI_Core_CoreWindow_Activated) événements.

|  Scénario |  Resuming  |  Actif | 
|----------|----------|----------|
|  Lancez une nouvelle instance de l’application à partir du menu Démarrer  |   |  **Activé** avec un nouveau [paramètre TileId](https://docs.microsoft.com/uwp/api/windows.ui.startscreen.secondarytile#Windows_UI_StartScreen_SecondaryTile_TileId) | 
|  Lancez la deuxième instance de l’application à partir du menu Démarrer  |   |  **Activé** avec un nouveau **paramètre TileId** | 
|  Sélectionnez l’instance de l’application qui n’est pas active actuellement  |   |  **Activé** avec la **paramètre TileId** associé à l’instance | 
|  Sélectionnez une autre application, puis sélectionnez l’instance précédemment actif  |  **La reprise** déclenché  |  | 
|  Sélectionnez une autre application, puis sélectionnez l’instance qui a été précédemment inactif  |  **La reprise** déclenché  |  Puis **Activated** avec la **paramètre TileId** associé à l’instance | 

### <a name="extended-execution"></a>Exécution étendue

Parfois, votre application doit continuer à travailler en arrière-plan ou de lecture de données audio. [Tâches en arrière-plan](https://docs.microsoft.com/windows/uwp/launch-resume/declare-background-tasks-in-the-application-manifest) sont disponibles sur HoloLens.

![Applications peuvent s’exécuter en arrière-plan](images/slide10-800px.png)<br>
*Applications peuvent s’exécuter en arrière-plan*

## <a name="app-views"></a>Vues d’applications

Lorsque votre application active, vous pouvez choisir de quel type de vue que vous souhaitez afficher. Pour une application **CoreApplication**, il y a toujours un principal [affichage de l’application](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationView) et un nombre quelconque de davantage les vues d’application vous souhaitez créer. Sur le bureau, vous pouvez considérer comme une fenêtre d’une vue de l’application. Nos modèles d’application de réalité mixte créent un projet Unity où la vue d’application principal est [immersives](app-views.md). 

Votre application peut créer une vue de l’application 2D supplémentaires à l’aide de technologies telles que XAML, à utiliser les fonctionnalités de Windows 10, telles que des achats dans l’application. Si votre application a démarré comme une application UWP pour d’autres appareils Windows 10, votre vue principale est 2D, mais vous pouvez « alléger » dans la réalité mixte en ajoutant une vue d’application supplémentaires est immersive pour afficher une expérience volumétrique. Imaginez la création d’une application de visionneuse de photos dans XAML où le bouton de diaporama bascule vers une vue d’application captivante a décollé photos à partir de l’application dans le monde et les surfaces.

![L’application en cours d’exécution peut avoir une vue en 2D ou une vue immersive](images/slide3-800px.png)<br>
*L’application en cours d’exécution peut avoir une vue en 2D ou une vue immersive*

### <a name="creating-an-immersive-view"></a>Création d’un affichage immersif

Applications de réalité mixte sont ceux qui créent une vue immersive, qui est obtenue avec la [HolographicSpace](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace) type.

Une application qui est purement immersive doit toujours créer une vue immersive au lancement, même si lancée à partir du bureau. Vues immersives s’afficheront toujours dans le casque, quel que soit l’endroit où ils ont été créés à partir. Activation d’une vue immersive pour afficher le portail de réalité mixte et guider l’utilisateur à mettre sur leur casque.

Une application qui démarre avec une vue en 2D sur le Moniteur du bureau peut créer une vue secondaire immersive pour afficher un contenu dans le casque. Un exemple de ceci est une fenêtre de Edge 2D sur l’écran d’affichage d’une vidéo à 360 degrés dans le casque.

![Applications qui s’exécutent en mode immersif sont le seul visible](images/slide4-800px.png)<br>
*Une application en cours d’exécution dans une vue immersive est le seul visible*

### <a name="2d-view-in-the-windows-mixed-reality-home"></a>Vue en 2D dans Windows Mixed Reality domestique

Autre chose qu’une vue immersive est restitué sous la forme d’une vue en 2D dans votre monde.

Une application peut avoir des vues 2D sur les deux le moniteur de bureau et dans le casque. Notez qu’une nouvelle vue 2D sera placée dans le shell en tant que la vue qui l’a créée, sur le moniteur ou dans le casque. Il n’est pas possible actuellement d’une application ou un utilisateur de déplacer une vue en 2D entre la page d’accueil réalité mixte et le moniteur.

![Applications qui s’exécutent dans la vue en 2D partagent l’espace dans le monde mixte avec d’autres applications](images/slide5-800px.png)<br>
*Applications qui s’exécutent dans une vue en 2D partagent l’espace avec d’autres applications*

### <a name="placement-of-additional-app-tiles"></a>Positionnement des vignettes des applications supplémentaires

Vous pouvez placer comme de nombreuses applications avec un 2D afficher dans votre monde que vous le souhaitez avec le [API de vignette secondaire](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/secondary-tiles). Ces vignettes « épinglés » seront affiche en tant que les écrans de démarrage que les utilisateurs doivent placer et puis peuvent utiliser ultérieurement pour lancer votre application. Réalité mixte Windows ne prend pas en charge n’importe quel contenu de la vignette 2D rendu sous forme de vignettes dynamiques.

![Les applications peuvent avoir plusieurs emplacements à l’aide des vignettes secondaires](images/slide6-800px.png)<br>
*Les applications peuvent avoir plusieurs emplacements à l’aide des vignettes secondaires*

### <a name="switching-views"></a>Le changement d’affichage

#### <a name="switching-from-the-2d-xaml-view-to-the-immersive-view"></a>Basculement à partir de la vue XAML 2D à la vue immersive

Si l’application utilise XAML, puis le XAML [IFrameworkViewSource](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.iframeworkviewsource) contrôlera la première vue de l’application. L’application a besoin basculer vers la vue immersive avant d’activer la **CoreWindow**, pour garantir l’application démarre directement dans l’expérience d’immersion.

Utilisez [CoreApplication.CreateNewView](https://docs.microsoft.com/uwp/api/Windows.ApplicationModel.Core.CoreApplication#Windows_ApplicationModel_Core_CoreApplication_CreateNewView_Windows_ApplicationModel_Core_IFrameworkViewSource_) et [ApplicationViewSwitcher.SwitchAsync](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationViewSwitcher#Windows_UI_ViewManagement_ApplicationViewSwitcher_SwitchAsync_System_Int32_) pour le rendre la vue active.

> [!NOTE]
>* Ne spécifiez pas le [ApplicationViewSwitchingOptions.ConsolidateViews](https://docs.microsoft.com/uwp/api/windows.ui.viewmanagement.applicationviewswitchingoptions) indicateur **SwitchAsync** lorsque passant de la vue XAML à la vue immersive, ou l’ardoise qui a lancé l’application sera supprimée dans le monde.
>* **SwitchAsync** doit être appelée à l’aide de la [répartiteur](https://docs.microsoft.com/uwp/api/windows.ui.core.corewindow#Windows_UI_Core_CoreWindow_Dispatcher) associé à la vue que vous insérez dans.
>* Vous devrez **SwitchAsync** revenir à la vue XAML, si vous avez besoin lancer un clavier virtuel ou à activer une autre application.

![Applications peuvent basculer entre les affichages 2D et immersives](images/slide7-600px.png) ![lorsqu’une application est dans une vue immersive, le monde mixte et autres applications disparaissent](images/slide8-600px.png)<br>
*Gauche : applications peuvent basculer entre immersives et affichage 2D. Right : lorsqu’une application est dans une vue immersive, les applications de base et d’autres Windows Mixed Reality disparaissent.*

#### <a name="switching-from-the-immersive-view-back-to-a-keyboard-xaml-view"></a>Basculer à partir de la vue immersive vers un vue XAML du clavier

Une des raisons courantes pour basculement back-et-les deux sens entre les vues affiche un clavier dans une application de réalité mixte. L’interpréteur de commandes peut uniquement afficher le clavier système si l’application affiche une vue en 2D. Si l’application a besoin obtenir une entrée de texte, il peut fournir une vue XAML personnalisée avec un champ d’entrée de texte, basculez vers celui-ci et faites après que l’entrée est terminée.

Comme dans la section précédente, vous pouvez utiliser **ApplicationViewSwitcher.SwitchAsync** à la transition vers une vue XAML à partir de votre vue immersive.

## <a name="app-size"></a>Taille de l’application

Vues de l’application 2D apparaissent toujours dans une ardoise virtuelle fixe. Ainsi, toutes les vues 2D montrent la même quantité exacte de contenu. Voici quelques détails supplémentaires sur la taille de la vue en 2D de votre application :
* Les proportions de l’application est conservée lors du redimensionnement.
* Application [facteur de résolution et de mise à l’échelle](building-2d-apps.md#2d-app-view-resolution-and-scale-factor) ne sont pas modifiés en redimensionnant.
* Les applications ne sont pas en mesure d’interroger leur taille réelle dans le monde.

![Applications 2D apparaissent avec des tailles de fenêtre fixe](images/12493521-10104043956964683-6118765685995662420-o-500px.jpg)<br>
*Applications avec une vue en 2D apparaissent avec des tailles de fenêtre fixe*

## <a name="app-tiles"></a>Vignettes d’applications

Le menu Démarrer utilise la petite vignette standard et la vignette moyenne pour les codes confidentiels et **toutes les applications** liste en réalité mixte. 

![Le menu Démarrer pour la réalité mixte Windows](images/start-500px.png)<br>
*Le menu Démarrer pour la réalité mixte Windows*

## <a name="app-to-app-interactions"></a>Application aux interactions de l’application

Lorsque vous générez des applications, vous avez accès aux mécanismes de communication d’une application vers riches disponibles sur Windows 10. La plupart des nouvelles API de protocole et les enregistrements de fichier fonctionnent parfaitement sur HoloLens pour activer la communication et lancement d’applications. 

Notez que pour les casques de bureau, l’application associée à une extension de fichier donné ou protocole peut être une application Win32 qui peut apparaître uniquement sur le moniteur de bureau ou dans la séquence de postes de travail.

### <a name="protocols"></a>Protocoles

HoloLens prend en charge le lancement d’une application vers la [Windows.System.Launcher APIs](https://docs.microsoft.com/uwp/api/Windows.System.Launcher).

Il existe quelques éléments à prendre en compte lors du lancement d’une autre application :

* Lors de l’exécution un lancement non modale, tel que [LaunchUriAsync](https://docs.microsoft.com/uwp/api/Windows.System.Launcher#Windows_System_Launcher_LaunchUriAsync_Windows_Foundation_Uri_), l’utilisateur doit placer l’application avant d’interagir avec lui.

* Lors de l’exécution un lancement modal, telles que via [LaunchUriForResultsAsync](https://docs.microsoft.com/uwp/api/Windows.System.Launcher#Windows_System_Launcher_LaunchUriForResultsAsync_Windows_Foundation_Uri_Windows_System_LauncherOptions_Windows_Foundation_Collections_ValueSet_), l’application modale est placée au-dessus de la fenêtre.

* Réalité mixte Windows ne peut pas superposer des applications sur des vues exclusifs. Pour afficher l’application lancée, Windows ramène l’utilisateur au monde pour afficher l’application.

### <a name="file-pickers"></a>Sélecteurs de fichier

HoloLens prend en charge les deux [FileOpenPicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileOpenPicker) et [FileSavePicker](https://docs.microsoft.com/uwp/api/Windows.Storage.Pickers.FileSavePicker) contrats. Toutefois, aucune application n’est préinstallée qui remplit les contrats de sélecteur de fichier. Ces applications - OneDrive, par exemple - peuvent être installées depuis le Microsoft Store.

Si vous avez plusieurs applications de sélecteur de fichier installée, vous ne verrez pas l’ambiguïté de l’interface utilisateur permettant de choisir quelle application pour lancer ; au lieu de cela, le premier sélecteur de fichiers installé sera choisi. Lorsque vous enregistrez un fichier, le nom de fichier est généré, ce qui inclut l’horodatage. Cela ne peut pas être modifié par l’utilisateur.

Par défaut, les extensions suivantes sont prises en charge en local :

|  App  |  Extensions | 
|----------|----------|
|  Photos  |  bmp, gif, jpg, png, avi, mov, mp4, wmv | 
|  Microsoft Edge  |  htm, html, pdf, svg, xml | 

### <a name="app-contracts-and-windows-mixed-reality-extensions"></a>Contrats d’application et les extensions Windows Mixed Reality

Contrats d’application et points d’extension vous permettent d’inscrire votre application pour tirer parti des fonctionnalités de système d’exploitation plus approfondies tels que la gestion d’une extension de fichier ou à l’aide de tâches en arrière-plan. Il s’agit d’une liste des contrats pris en charge et non pris en charge et des points d’extension sur HoloLens.

|  Contrat ou Extension  |  Prise en charge ? | 
|----------|----------|
| [Fournisseur d’images de compte (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#account_picture_provider) | Non pris en charge | 
| [Alarme](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#alarm) | Non pris en charge | 
| [Service d’application](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#app_service) | Prise en charge mais pas entièrement fonctionnel | 
| [Fournisseur de rendez-vous](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#appointmnets_provider) | Non pris en charge | 
| [AutoPlay (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#autoplay) | Non pris en charge | 
| [Tâches en arrière-plan (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#background_tasts) | Partiellement prises en charge (pas tous les déclencheurs travail) | 
| [Tâche de mise à jour (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#update_task) | Prise en charge | 
| [Contrat de mise à jour du fichier mis en cache](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#cached_file_updater) | Prise en charge | 
| [Paramètres de la caméra (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#camera_settings) | Non pris en charge | 
| [Protocole d’accès à distance](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#dial_protocol) | Non pris en charge | 
| [Activation de fichier (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#file_activation) | Prise en charge | 
| [Contrat de sélecteur d’ouverture de fichier](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#file_open_picker_contract) | Prise en charge | 
| [Contrat de sélecteur de fichier enregistrer](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#file_save_picker_contract) | Prise en charge | 
| [Appel d’écran de verrouillage](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#lock_screen_call) | Non pris en charge | 
| [Lecture de contenu multimédia](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#media_playback) | Non pris en charge | 
| [Contrat Play To](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#playto_contract) | Non pris en charge | 
| [Tâche de configuration préinstallée](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#preinstalled_config_task) | Non pris en charge | 
| [Imprimer le flux de travail 3D](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#print_3d_workflow) | Prise en charge | 
| [Paramètres de tâche d’impression (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#print_task_settings) | Non pris en charge | 
| [Activation de l’URI (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#protocol_activation) | Prise en charge | 
| [Lancement restreint](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#restricted_launch) | Non pris en charge | 
| [Contrat de recherche](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#search_contract) | Non pris en charge | 
| [Contrat de paramètres](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#settings_contract) | Non pris en charge | 
| [Contrat de partage](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#share_contract) | Non pris en charge | 
| [Certificats SSL / (extension)](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#ssl_certificates) | Prise en charge | 
| [Fournisseur de comptes Web](https://msdn.microsoft.com/library/windows/desktop/hh464906.aspx#web_account_provider) | Prise en charge | 

## <a name="app-file-storage"></a>Stockage de fichiers d’application

Tout le stockage s’effectue via le [espace de noms Windows.Storage](https://docs.microsoft.com/uwp/api/Windows.Storage). Consultez la documentation suivante pour plus d’informations. HoloLens ne prend pas en charge le stockage synchronisation/itinérance d’application.

* [Fichiers, dossiers et bibliothèques](https://docs.microsoft.com/windows/uwp/files/index)
* [Store et de récupérer les paramètres et autres données d’application](https://docs.microsoft.com/windows/uwp/design/app-settings/store-and-retrieve-app-data)

### <a name="known-folders"></a>Dossiers connus

Consultez [KnownFolders](https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders) pour plus d’informations pour les applications UWP.

<table>
<tr>
<th> Propriété</th><th> Prise en charge sur HoloLens</th><th> Prise en charge sur des casques IMMERSIFS</th><th> Description</th>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_AppCaptures">AppCaptures</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier de capture de l’application.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_CameraRoll">CameraRoll</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier pellicule.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_DocumentsLibrary">DocumentsLibrary</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient la bibliothèque de Documents. La bibliothèque de Documents n’est pas prévue pour une utilisation générale.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_MusicLibrary">MusicLibrary</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient la médiathèque.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_Objects3D">Objects3D</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier objets de 3D.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_PicturesLibrary">PicturesLibrary</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient la bibliothèque d’images.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_Playlists">Sélections</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier de listes de lecture.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_SavedPictures">SavedPictures</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient le dossier photos enregistrées.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_VideosLibrary">VideosLibrary</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td><td>Obtient la bibliothèque de vidéos.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_HomeGroup">HomeGroup</a></td><td></td><td style="text-align: center;">✔️</td><td>Obtient le dossier groupe résidentiel.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_MediaServerDevices">MediaServerDevices</a></td><td></td><td style="text-align: center;">✔️</td><td>Obtient le dossier support d’appareils de serveur (Digital Living Network Alliance (DLNA)).</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_RecordedCalls">RecordedCalls</a></td><td></td><td style="text-align: center;">✔️</td><td>Obtient le dossier des appels enregistrés.</td>
</tr><tr>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Storage.KnownFolders#Windows_Storage_KnownFolders_RemovableDevices">RemovableDevices</a></td><td></td><td style="text-align: center;">✔️</td><td>Obtient le dossier de périphériques amovibles.</td>
</tr>
</table>

## <a name="app-package"></a>Package de l’application

Avec Windows 10 vous ne ciblez plus un système d’exploitation, mais au lieu de cela [ciblez votre application sur un ou plusieurs familles d’appareils](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide#device-families). Une famille d’appareils identifie les API, les caractéristiques système et les comportements que vous pouvez attendre sur les différents appareils de cette famille. Il détermine également l’ensemble des périphériques sur lequel votre application peut être installée à partir de la [Microsoft Store](submitting-an-app-to-the-microsoft-store.md#specifying-target-device-families).

* Pour cibler les casques de bureau et HoloLens, ciblez votre application sur le **Windows.Universal** famille de périphériques.
* Pour cibler les casques simplement bureau, ciblez votre application sur le **Windows.Desktop** famille de périphériques.
* Pour cibler uniquement HoloLens, ciblez votre application sur le **Windows.Holographic** famille de périphériques.

## <a name="see-also"></a>Voir aussi

* [Vues de l’application](app-views.md)
* [La mise à jour des applications UWP 2D pour la réalité mixte](building-2d-apps.md)
* [Guide de conception du Lanceur d’application 3D](3d-app-launcher-design-guidance.md)
* [Implémentation des lanceurs d’applications 3D.](implementing-3d-app-launchers.md)
