---
title: RM partageant 250-HoloLens et des casques immersifs
description: Suivez cette procédure pas à pas de codage à l’aide des casques Unity, Visual Studio, HoloLens et Windows Mixed Reality pour apprendre les détails du partage d’hologrammes entre des appareils de réalité mixte.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, immersion, contrôleur de mouvement, partage, contrôleur Xbox, mise en réseau, inter-appareils
ms.openlocfilehash: 9e1cb0d168b8bf830b4477190516cd19caef7972
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63506113"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br>

# <a name="mr-sharing-250-hololens-and-immersive-headsets"></a>RM partageant 250: HoloLens et casques immersifs

Avec la flexibilité de plateforme Windows universelle (UWP), il est facile de créer une application qui s’étend sur plusieurs appareils. Grâce à cette flexibilité, nous pouvons créer des expériences qui tirent parti des avantages de chaque appareil. Ce didacticiel couvre une expérience partagée de base qui s’exécute à la fois sur HoloLens et sur les casques immersifs de la réalité mixte Windows. Ce contenu a été fourni à l’origine lors de la Conférence Microsoft Build 2017 à Seattle, WA.

**Dans ce didacticiel, nous allons:**

* Configurer un réseau à l’aide de UNET.
* Partager des hologrammes sur des appareils de réalité mixte.
* Établissez une vue différente de l’application en fonction de l’appareil de réalité mixte utilisé.
* Créez une expérience partagée dans laquelle les utilisateurs de HoloLens guident les utilisateurs immersifs à travers des puzzles simples.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>RM partageant 250: HoloLens et casques immersifs</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 avec les [outils de développement nécessaires](install-the-tools.md) et [configuré pour prendre en charge un casque immersif Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines).
* Un contrôleur Xbox qui fonctionne avec votre PC.
* Au moins un appareil HoloLens et un casque immersif.
* Réseau qui autorise la diffusion UDP pour la découverte.

### <a name="project-files"></a>Fichiers projet

* Téléchargez les [fichiers](https://github.com/Microsoft/MixedReality250/archive/master.zip) requis par le projet. Extrayez les fichiers à un emplacement facile à mémoriser.
* Ce projet nécessite la [version d’Unity recommandée avec prise en charge de Windows Mixed Reality](install-the-tools.md).

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/MixedReality250).

## <a name="chapter-1---holo-world"></a>Chapitre 1-Holo World

>[!VIDEO https://www.youtube.com/embed/IC0rp6rLiEc]

### <a name="objectives"></a>Objectifs

Assurez-vous que l’environnement de développement est prêt à l’emploi avec un projet simple.

### <a name="what-we-will-build"></a>Ce que nous allons créer

Application qui affiche un hologramme sur HoloLens ou sur un casque immersif Windows Mixed Reality.

### <a name="steps"></a>Étapes
* Ouvrez Unity.
    * Sélectionnez **ouvrir**.
    * Accédez à l’emplacement où vous avez extrait les fichiers projet.
    * Cliquez sur **Sélectionner un dossier**.
    * *Il faut un peu pour Unity pour traiter le projet la première fois.*
* Vérifiez que la réalité mixte est activée dans Unity.
    * Ouvrez la boîte de dialogue Paramètres de build (**Ctrl + Maj + B** ou **fichier > paramètres de Build...** ).
    * Sélectionnez **plateforme Windows universelle** puis cliquez sur **changer de plateforme**.
    * Sélectionnez **modifier les paramètres du lecteur >** .
    * Dans le volet de l' **inspecteur** situé sur le côté droit, développez **paramètres XR**.
    * Cochez la case la **réalité virtuelle est prise en charge** .
    * *Windows Mixed Reality doit être le kit de développement logiciel (SDK) de realisation virtuelle.*
* Créer une scène.
    * Dans la **hiérarchie** , cliquez avec le bouton droit sur **caméra principale** , sélectionnez **supprimer**.
    * À partir de **HoloToolkit > d’entrée > Prefabs** faire glisser **MixedRealityCameraParent** vers la **hiérarchie**.
* Ajouter des hologrammes à la scène
    * À partir de **AppPrefabs** , faites glisser **skybox** vers la **vue scène**.
    * Dans **AppPrefabs** , faites glisser les **gestionnaires** vers la **hiérarchie**.
    * Dans **AppPrefabs** , faites glisser l' **îlot** vers la **hiérarchie**.
* Enregistrer et générer
    * Save ( **Control + S** ou **file > Save Scene**)
    * Étant donné qu’il s’agit d’une nouvelle scène, vous devez la nommer. Le nom n’a pas d’importance, mais nous utilisons SharedMixedReality.
* Exporter vers Visual Studio
    * Ouvrez le menu Générer (**Ctrl + Maj + B** ou **fichier > paramètres de build**).
    * Cliquez sur **Ajouter des scènes ouvertes.**
    * Vérifier **les C# projets Unity**
    * Cliquez sur **Build**.
    * Dans la fenêtre de l’Explorateur de fichiers qui s’affiche, créez un nouveau dossier nommé **app**.
    * Cliquez sur le dossier de l' **application** .
    * Appuyez sur **Sélectionner un dossier.**
    * **Attendre la fin de la génération**
    * Dans la fenêtre de l’Explorateur de fichiers qui s’affiche, accédez au dossier de l' **application** .
    * Double-cliquez sur **SharedMixedReality. sln** pour lancer Visual Studio
* Générer à partir de Visual Studio
    * À l’aide de la barre d’outils supérieure, remplacez cible par **Release** et **x86**.
    * Cliquez sur la flèche en regard de **ordinateur local** , puis sélectionnez l' **appareil** à déployer dans HoloLens
    * Cliquez sur la flèche en regard de **périphérique** , puis sélectionnez **ordinateur local** à déployer pour le casque de la réalité mixte.
    * Cliquez sur déboguer **-> exécuter sans débogage** ou sur **CTRL + F5** pour démarrer l’application.

### <a name="digging-into-the-code"></a>Examen du code

Dans le panneau projet, accédez à **Assets\HoloToolkit\Input\Scripts\Utilities** et double-cliquez sur **MixedRealityCameraManager.cs** pour l’ouvrir.

**Vue** MixedRealityCameraManager.cs est un script simple qui ajuste le niveau de qualité et les paramètres d’arrière-plan en fonction de l’appareil. La clé ici est HolographicSettings. IsDisplayOpaque, qui permet à un script de détecter si l’appareil est un HoloLens (IsDisplayOpaque retourne la valeur false) ou un casque immersif (IsDisplayOpaque retourne la valeur true).

### <a name="enjoy-your-progress"></a>Profitez de votre progression

À ce stade, l’application affichera simplement un hologramme. Nous ajouterons l’interaction à l’hologramme ultérieurement. Les deux appareils affichent l’hologramme de la même façon. Le casque immersif affiche également un arrière-plan bleu ciel et Clouds.

## <a name="chapter-2---interaction"></a>Chapitre 2-interaction

>[!VIDEO https://www.youtube.com/embed/Lrb1y4sQRvI]

### <a name="objectives"></a>Objectifs

Montrez comment gérer les entrées pour une application Windows Mixed Reality.

### <a name="what-we-will-build"></a>Ce que nous allons créer

En s’appuyant sur l’application du chapitre 1, nous ajouterons des fonctionnalités pour permettre à l’utilisateur de sélectionner l’hologramme et de le placer sur une surface dans le monde réel dans HoloLens ou sur une table virtuelle dans un casque immersif.

**Actualisateur d’entrée:** Sur HoloLens, le geste de sélection est le **robinet d’air**. Sur les casques immersifs, nous allons utiliser le bouton **A** sur le contrôleur Xbox. Pour plus d’informations sur l’entrée, cliquez [ici](gestures.md).

### <a name="steps"></a>Étapes
* Ajouter un gestionnaire d’entrée
    * À partir de **HoloToolkit > d’entrée > Prefabs** faire glisser **InputManager** vers la **hiérarchie** en tant qu’enfant de **managers**.
    * À partir de **HoloToolkit > entrée > curseur de > Prefabs** , faites glisser **Cursor** vers **Hierarchy**.
* Ajouter un mappage spatial
    * À partir de **HoloToolkit > SpatialMapping > Prefabs** faites glisser **SpatialMapping** vers la **hiérarchie**.
* Ajouter des PlaySpace virtuels
    * Dans **hiérarchie** , développez **MixedRealityCameraParent** sélectionner une **limite**
    * Dans le panneau **inspecteur** , cochez la case pour activer la **limite**
    * Dans **AppPrefabs** , faites glisser **VRRoom** vers la **hiérarchie**.
* Ajouter WorldAnchorManager
    * Dans **hiérarchie**, sélectionnez **gestionnaires**.
    * Dans **Inspector**, cliquez sur **Ajouter un composant**.
    * Tapez **World Anchor Manager**.
    * Sélectionnez **World Anchor Manager** pour l’ajouter.
* Ajouter TapToPlace à l’îlot
    * Dans **hiérarchie**, développez **îlot**.
    * Sélectionnez **MixedRealityLand**.
    * Dans **Inspector**, cliquez sur **Ajouter un composant**.
    * Tapez **TAP pour la placer** et sélectionnez-le.
    * Cochez **Placer le parent sur TAP**.
    * Définissez **décalage de placement** sur **(0, 0,1, 0)** .
* Enregistrer et générer comme avant

### <a name="digging-into-the-code"></a>Examen du code

**Script 1-GamepadInput.cs**

Dans le panneau projet, accédez à **Assets\HoloToolkit\Input\Scripts\InputSources** et double-cliquez sur **GamepadInput.cs** pour l’ouvrir. À partir du même chemin d’accès dans le panneau projet, double-cliquez sur **InteractionSourceInputSource.cs**.

Notez que les deux scripts ont une classe de base commune, BaseInputSource.

BaseInputSource conserve une référence à un InputManager, qui permet à un script de déclencher des événements. Dans ce cas, l’événement InputClicked est pertinent. Il est important de se souvenir quand nous obtenons le script 2, TapToPlace. Dans le cas de GamePadInput, nous interrogeons le bouton A sur le contrôleur à enfoncer, puis nous déclencherons l’événement InputClicked. Dans le cas de InteractionSourceInputSource, l’événement InputClicked est déclenché en réponse au TappedEvent.

**Script 2-TapToPlace.cs**

Dans le panneau projet, accédez à **Assets\HoloToolkit\SpatialMapping\Scripts** et double-cliquez sur **TapToPlace.cs** pour l’ouvrir.

La première chose que de nombreux développeurs souhaitent implémenter lors de la création d’une application holographique est le déplacement d’hologrammes avec entrée de mouvement. C’est pourquoi nous avons fait en sorte de formuler des commentaires sur ce script. Quelques points méritent une mise en évidence pour ce didacticiel.

Tout d’abord, Notez que TapToPlace implémente IInputClickHandler. IInputClickHandler expose les fonctions qui gèrent l’événement InputClicked déclenché par GamePadInput.cs ou InteractionSourceInputSource.cs. OnInputClicked est appelé lorsqu’un BaseInputSource détecte un clic alors que l’objet avec TapToPlace est actif. L’activation de la pression sur HoloLens ou sur le bouton A sur le contrôleur Xbox déclenche l’événement.

Deuxièmement, le code doit être exécuté dans Update pour voir si une surface est recherchée afin que nous puissions placer l’objet de jeu sur une surface, par exemple une table. Le casque immersif n’a pas de concept de surfaces réelles, donc l’objet qui représente la table Top (Vroom > TableThingy > cube) a été marqué avec la couche physique SpatialMapping, de sorte que la mise à jour de Ray est en conflit avec la table virtuelle Top.

### <a name="enjoy-your-progress"></a>Profitez de votre progression

Cette fois, vous pouvez sélectionner l’îlot pour le déplacer. Sur HoloLens, vous pouvez déplacer l’îlot vers une surface réelle. Dans le casque immersif, vous pouvez déplacer l’îlot vers la table virtuelle que nous avons ajoutée.

## <a name="chapter-3---sharing"></a>Chapitre 3-partage

>[!VIDEO https://www.youtube.com/embed/1diycJvxfDc]

### <a name="objectives"></a>Objectifs

Assurez-vous que le réseau est correctement configuré et comment les ancres spatiales sont partagées entre les appareils.

### <a name="what-we-will-build"></a>Ce que nous allons créer

Nous allons convertir notre projet en projet multijoueur. Nous allons ajouter l’interface utilisateur et la logique pour héberger ou joindre des sessions. Les utilisateurs de HoloLens s’afficheront dans la session avec des clouds sur leurs têtes, et les utilisateurs de casque immersif présenteront des clouds proches de l’emplacement où se trouve l’ancre. Les utilisateurs des casques immersifs verront les utilisateurs HoloLens par rapport à l’origine de la scène. Les utilisateurs de HoloLens verront tous l’hologramme de l’île au même endroit. Il est important de noter que les utilisateurs des casques immersifs ne seront pas sur l’île au cours de ce chapitre, mais ils se comportent de la même façon que HoloLens, avec une vue d’ensemble des oiseaux de l’île.

### <a name="steps"></a>Étapes
* Supprimer l’îlot et VRRoom
    * Dans **hiérarchie** , cliquez avec le bouton droit sur **îlot** sélectionner **supprimer**
    * Dans **hiérarchie** , cliquez avec le bouton droit sur **VRRoom** sélectionner **supprimer**
* Ajouter Usland
    * Dans **AppPrefabs** , faites glisser **Usland** vers la **hiérarchie**.
* Dans **AppPrefabs** , faites glisser chacun des éléments suivants vers la **hiérarchie**:
    * **UNETSharingStage**
    * **UNetAnchorRoot**
    * **UIContainer**
    * **DebugPanelButton**
* Enregistrer et générer comme avant

### <a name="digging-into-the-code"></a>Examen du code

Dans le panneau projet, accédez à **Assets\AppPrefabs\Support\SharingWithUnet\Scripts** et double-cliquez sur **UnetAnchorManager.cs**. La possibilité pour un HoloLens de partager des informations de suivi avec un autre HoloLens de telle sorte que les deux appareils puissent partager le même espace est presque magique. La puissance de la réalité mixte est active lorsque deux personnes ou plus peuvent collaborer à l’aide des mêmes données numériques.

Voici quelques éléments à souligner dans ce script:

Dans la fonction Start, notez la vérification de **IsDisplayOpaque**. Dans ce cas, nous supposons que le point d’ancrage est établi. Cela est dû au fait que les casques immersifs n’exposent pas un moyen d’importer ou d’exporter des ancres. Toutefois, si nous exécutons un HoloLens, ce script implémente des ancres de partage entre les appareils. L’appareil qui démarre la session crée une ancre pour l’exportation. L’appareil qui rejoint une session demande l’ancre à partir de l’appareil qui a démarré la session.

**Export**

Lorsqu’un utilisateur crée une session, NetworkDiscoveryWithAnchors appelle la fonction UNETAnchorManagers CreateAnchor. Nous allons suivre CreateAnchor Flow.

Nous commençons par la maintenance, en effaçant toutes les données que nous avons pu collecter pour les ancres précédentes. Nous vérifions ensuite s’il y a une ancre mise en cache à charger. Les données d’ancrage ont tendance à avoir une taille comprise entre 5 et 20 Mo. par conséquent, la réutilisation des ancres mises en cache peut économiser sur la quantité de données que nous devons transférer sur le réseau. Nous verrons comment cela fonctionne un peu plus tard. Même si nous réutilisons le point d’ancrage, nous devons recevoir les données d’ancrage au cas où un nouveau client se connecte sans le point d’ancrage.

En ce qui concerne l’obtention des données d’ancrage, la classe WorldAnchorTransferBatch expose les fonctionnalités permettant de préparer les données d’ancrage pour les envoyer à un autre périphérique ou une autre application, ainsi que les fonctionnalités permettant d’importer les données d’ancrage. Étant donné que nous sommes dans le chemin d’exportation, nous allons ajouter notre point d’ancrage au WorldAnchorTransferBatch et appeler la fonction ExportAsync. ExportAsync appellera ensuite le rappel WriteBuffer lors de la génération de données pour l’exportation. Lorsque toutes les données ont été exportées, ExportComplete est appelé. Dans WriteBuffer, nous ajoutons le segment de données à une liste que nous conservons pour l’exportation. Dans ExportComplete, nous allons convertir la liste en tableau. La variable AnchorName est également définie, ce qui déclenche la demande de l’ancre à d’autres appareils, le cas échéant.

Dans certains cas, le point d’ancrage n’exportera pas ou créera donc un petit nombre de données que nous réessaierons. Ici, nous appelons simplement CreateAnchor.

Une fonction finale dans le chemin d’exportation est AnchorFoundRemotely. Lorsqu’un autre appareil trouve le point d’ancrage, cet appareil indique à l’ordinateur hôte, et l’hôte l’utilise comme signal indiquant que l’ancre est une «bonne ancre» et peut être mise en cache.

**Destination**

Lorsqu’un HoloLens rejoint une session, il doit importer une ancre. Dans la fonction de mise à jour de UNETAnchorManager, le AnchorName est interrogé. Lorsque le nom d’ancrage change, le processus d’importation commence. Tout d’abord, nous essayons de charger l’ancre avec le nom spécifié à partir du magasin d’ancrage local. Si nous l’avons déjà, nous pouvons l’utiliser sans télécharger à nouveau les données. Si ce n’est pas le cas, nous appelons WaitForAnchor, ce qui va lancer le téléchargement.

Une fois le téléchargement terminé, NetworkTransmitter_dataReadyEvent est appelé. Cela indique à la boucle de mise à jour d’appeler ImportAsync avec les données téléchargées. ImportAsync appellera ImportComplete lorsque le processus d’importation est terminé. Si l’importation réussit, le point d’ancrage est enregistré dans la Banque de lecteurs locale. PlayerController.cs effectue en fait l’appel à AnchorFoundRemotely pour permettre à l’hôte de savoir qu’une bonne ancre a été établie.

### <a name="enjoy-your-progress"></a>Profitez de votre progression

Cette fois, un utilisateur disposant d’un HoloLens hébergera une session à l’aide du bouton **Démarrer la session** dans l’interface utilisateur. D’autres utilisateurs, à la fois sur HoloLens ou sur un casque immersif, sélectionnent la session, puis sélectionnent le bouton **rejoindre la session** dans l’interface utilisateur. Si vous avez plusieurs personnes avec des appareils HoloLens, elles auront des clouds rouges sur leurs têtes. Il y aura également un Cloud bleu pour chaque casque immersif, mais les clouds bleus ne seront pas au-dessus des casques, car les casques n’essaient pas de trouver les mêmes espaces de coordonnées universelles que les appareils HoloLens.

Ce point dans le projet est une application de partage contenue. Il n’en fait pas beaucoup et peut servir de base. Dans les chapitres suivants, nous allons commencer à créer une expérience que les gens pourront apprécier. Pour obtenir des conseils supplémentaires sur la conception de l’expérience partagée, rendez-vous ici.

## <a name="chapter-4---immersion-and-teleporting"></a>Chapitre 4-immersion et téléportage

>[!VIDEO https://www.youtube.com/embed/kUHZ5tCOfvY]

### <a name="objectives"></a>Objectifs

Traitez l’expérience de chaque type d’appareil de réalité mixte.

### <a name="what-we-will-build"></a>Ce que nous allons créer

Nous mettrons à jour l’application pour placer les utilisateurs du casque immersif sur l’île avec une vue immersive. Les utilisateurs de HoloLens auront toujours la vue d’ensemble de l’île. Les utilisateurs de chaque type d’appareil peuvent voir d’autres utilisateurs tels qu’ils apparaissent dans le monde. Par exemple, les utilisateurs de casque immersif peuvent voir les autres avatars sur d’autres chemins d’accès sur l’île, et les utilisateurs HoloLens en tant que Clouds géants au-dessus de l’île. Les utilisateurs du casque immersif verront également le curseur du point de regard de l’utilisateur HoloLens si l’utilisateur HoloLens regarde l’île. Les utilisateurs de HoloLens verront un avatar sur l’île pour représenter chaque utilisateur de casque immersif.

**Entrée mise à jour pour l’appareil immersif:**
* Les boutons du pare-chocs gauche et du pare-chocs droit sur le contrôleur Xbox font pivoter le lecteur
* Le maintien du bouton Y sur le contrôleur Xbox [active un curseur](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) de téléopération. Si le curseur a un indicateur de flèche en rotation lorsque vous relâchez le bouton Y, vous serez téléporté à l’emplacement du curseur.

### <a name="steps"></a>Étapes
* Ajouter MixedRealityTeleport à MixedRealityCameraParent
    * Dans **hiérarchie**, sélectionnez **Usland**.
    * Dans **Inspector**, activez **le contrôle de niveau**.
    * Dans **hiérarchie**, sélectionnez **MixedRealityCameraParent**.
    * Dans **Inspector**, cliquez sur **Ajouter un composant**.
    * Tapez **Mixed realre** telela et sélectionnez-la.

### <a name="digging-into-the-code"></a>Examen du code

Les utilisateurs du casque immersif sont attachés à leurs PC avec un câble, mais notre îlot est plus grand que le câble est long. Pour compenser, nous avons besoin de la possibilité de déplacer l’appareil photo indépendamment du mouvement de l’utilisateur. Pour plus d’informations sur la conception de votre application de réalité mixte (en particulier automotion et locomotion), consultez la [page Comfort](comfort.md) .

Pour pouvoir décrire ce processus, il est utile de définir deux termes. Tout d’abord, la **poupée** est l’objet qui déplace l’appareil photo indépendamment de l’utilisateur. Un objet de jeu enfant de la **poupée** est l' **appareil photo principal**. La caméra principale est attachée à la tête de l’utilisateur.

Dans le panneau projet, accédez à **Assets\AppPrefabs\Support\Scripts\GameLogic** et double-cliquez sur **MixedRealityTeleport.cs**.

MixedRealityTeleport a deux tâches. Tout d’abord, elle gère la rotation à l’aide des champignons. Dans la fonction de mise à jour, nous interrogeons «ButtonUp» sur LeftBumper et RightBumper. GetButtonUp retourne uniquement la valeur true sur la première image. un bouton est activé après avoir été enfoncé. Si l’un des deux boutons a été déclenché, nous savons que l’utilisateur doit faire pivoter.

Lorsque nous faisons pivoter, nous faisons un fondu et un fondu dans à l’aide d’un script simple appelé «contrôle de fondu». Nous faisons cela pour empêcher l’utilisateur de voir un mouvement non naturel qui pourrait entraîner une gêne. L’effet d’atténuation et de sortie est relativement simple. Nous avons un blocage noir à l’avant de la **caméra principale**. En cas de fondu, nous transmettons la valeur alpha de 0 à 1. Cela provoque progressivement le rendu des pixels noirs du quad et leur masquage. Lors du fondu, nous transférons la valeur alpha à zéro.

Lorsque nous calculons la rotation, Notez que nous allons faire pivoter notre **poupée** , mais en calculant la rotation autour de la **caméra principale**. Ce point est important, car plus la **caméra principale** est éloignée de 0, 0, moins la précision d’une rotation autour de la poupée deviendra du point de vue de l’utilisateur. En fait, si vous ne faites pas pivoter la position de la caméra, l’utilisateur se déplacera sur un arc autour du **chariot** plutôt que sur la rotation.

La deuxième tâche pour MixedRealityTeleport consiste à gérer le déplacement de la **poupée**. Cette opération s’effectue dans SetWorldPosition. SetWorldPosition prend la position universelle souhaitée, c’est-à-dire la position à laquelle l’utilisateur veut percieve qu’il habite. Nous devons placer notre **poupée** à cette position, moins la position locale de la **caméra principale**, car ce décalage sera ajouté à chaque cadre.

Un deuxième script appelle SetWorldPosition. Examinons ce script. Dans le panneau projet, accédez à **Assets\AppPrefabs\Support\Scripts\GameLogic** et double-cliquez sur **TeleportScript.cs**.

Ce script est un peu plus impliqué dans MixedRealityTeleport. Le script vérifie que le bouton Y du contrôleur Xbox est maintenu enfoncé. Lorsque le bouton est maintenu enfoncé, un curseur de téléverrouillage est rendu et le script convertit un rayon à partir de la position de regard de l’utilisateur. Si ce rayon entre en conflit avec une surface qui est plus ou moins pointée vers le haut, la surface sera considérée comme une bonne surface de téléchargement et l’animation sur le curseur de télétentative sera activée. Si le rayon n’entre pas en conflit avec une surface qui pointe vers le haut, l’animation sur le curseur est désactivée. Lorsque le bouton Y est relâché et que le point calculé du rayon est une position valide, le script appelle SetWorldPosition avec la position de l’intersection entre le rayon et le rayon.

### <a name="enjoy-your-progress"></a>Profitez de votre progression

Cette fois, vous devez rechercher un ami.

Une fois encore, un utilisateur avec HoloLens hébergera une session. D’autres utilisateurs vont rejoindre la session. L’application place les trois premiers utilisateurs à joindre à partir d’un casque immersif sur l’un des trois tracés sur l’îlot. N’hésitez pas à explorer l’île dans cette section.

Détails à noter:
1. Vous pouvez voir les visages dans les Clouds, ce qui permet à un utilisateur immersif de voir la direction qu’un utilisateur HoloLens recherche.
2. Les avatars sur l’îlot ont des cou qui pivotent. Ils ne suivent pas ce que fait l’utilisateur en réalité (nous n’avons pas ces informations), mais il offre une expérience intéressante.
3. Si l’utilisateur HoloLens examine l’île, les utilisateurs immergés peuvent voir leur curseur.
4. Les clouds qui représentent les utilisateurs HoloLens convertient des ombres.

## <a name="chapter-5---finale"></a>Chapitre 5-finalisation

>[!VIDEO https://www.youtube.com/embed/n_HDWJbfpNg]

### <a name="objectives"></a>Objectifs

Créez une expérience interactive collaborative entre les deux types d’appareils.

### <a name="what-we-will-build"></a>Ce que nous allons créer

En s’appuyant sur le chapitre 4, lorsqu’un utilisateur avec un casque immersif est proche d’un puzzle sur l’île, les utilisateurs de HoloLens reçoivent une info-bulle avec un indice sur le puzzle. Une fois que tous les utilisateurs du casque immersif ont passé leurs puzzles et dans le panneau «Ready» dans la salle de fusée, le fusée démarre.

### <a name="steps"></a>Étapes
* Dans **hiérarchie**, sélectionnez **Usland**.
* Dans l' **inspecteur**, dans **contrôle de niveau**, activez la case à cocher Activer la **collaboration**.

### <a name="digging-into-the-code"></a>Examen du code

Nous allons maintenant examiner LevelControl.cs. Ce script est le cœur de la logique de jeu et gère l’état du jeu. Dans la mesure où il s’agit d’un jeu multijoueur utilisant UNET, nous devons comprendre la façon dont les données circulent, au moins suffisamment bien pour modifier ce didacticiel. Pour une vue d’ensemble plus complète de UNET, reportez-vous à la documentation d’Unity.

Dans le panneau projet, accédez à **Assets\AppPrefabs\Support\Scripts\GameLogic** et double-cliquez sur **LevelControl.cs**.

Voyons comment un casque immersif indique qu’ils sont prêts pour le lancement de fusée. La préparation au lancement de fusée est communiquée par la définition de l’un des trois bools dans une liste de bools qui correspondent aux trois tracés sur l’îlot. La valeur booléenne d’un chemin d’accès est définie lorsque l’utilisateur affecté au chemin d’accès se trouve au-dessus du pavé brun dans la salle de fusée. OK, maintenant aux détails.

Nous allons commencer par la fonction Update (). Vous noterez qu’il y a une fonction «triche». Nous l’avons utilisé en développement pour tester l’ordre de lancement et de réinitialisation des fusées. Elle ne fonctionnera pas dans l’expérience multi-utilisateur. J’espère que lorsque vous internalrez l’inversion suivante, vous pouvez le faire fonctionner. Une fois que nous avons vérifié que nous devrions faire une triche, nous vérifions si le joueur local est plongé. Nous souhaitons nous concentrer sur la façon dont nous sommes à l’objectif. À l’intérieur de la vérification if (immergée), un appel à CheckGoal est masqué derrière le **EnableCollaboration** bool. Cela correspond à la case à cocher que vous avez sélectionnée lors de l’exécution des étapes de ce chapitre. Dans EnableCollaboration, nous voyons un appel à CheckGoal ().

CheckGoal effectue certaines opérations mathématiques pour voir si nous sommes plus ou moins debout sur le boîtier. Dans ce cas, nous déboguons. log «arrivé à l’objectif», puis nous appelons «SendAtGoalMessage ()». Dans SendAtGoalMessage, nous appelons playerController. SendAtGoal. Pour gagner du temps, voici le code:

```cs
private void CmdSendAtGoal(int GoalIndex)
       {
           levelState.SetGoalIndex(GoalIndex);
       }
```

```cs
public void SendAtGoal(int GoalIndex)
       {
           if (isLocalPlayer)
           {
               Debug.Log("sending at goal " + GoalIndex);
               CmdSendAtGoal(GoalIndex);
           }
       }
```

Notez que SendAtGoalMessage appelle CmdSendAtGoal, qui appelle levelState. SetGoalIndex, qui est de nouveau dans LevelControl.cs. À première vue, cela semble étrange. Pourquoi ne pas simplement appeler SetGoalIndex au lieu d’effectuer un routage dans le contrôleur de lecteur? Cela est dû au fait que nous nous conformons au modèle de données utilisé par UNET pour maintenir la synchronisation des données. Pour empêcher la triche et le blocage, UNET nécessite que chaque objet dispose d’un utilisateur habilité à modifier les variables synchronisées. En outre, seul l’hôte (l’utilisateur qui a démarré la session) peut modifier directement les données. Les utilisateurs qui ne sont pas l’hôte, mais qui ont une autorité, doivent envoyer une «commande» à l’hôte qui modifiera la variable. Par défaut, l’hôte a autorité sur tous les objets, à l’exception de l’objet généré pour représenter l’utilisateur. Dans notre cas, cet objet contient le script playercontroller. Il existe un moyen de demander une autorité pour un objet, puis d’apporter des modifications, mais nous choisissons de tirer parti du fait que le contrôleur de lecteur dispose d’une autorité autonome et de commandes de routage via le contrôleur de lecteur.

Autrement dit, lorsque nous nous sommes trouvés dans notre objectif, le joueur doit indiquer à l’hôte, et l’hôte va dire à tous les autres utilisateurs.

De retour dans LevelControl.cs, consultez SetGoalIndex. Ici, nous définissons la valeur d’une valeur dans un SyncList (AtGoal). N’oubliez pas que nous sommes dans le contexte de l’hôte pendant que nous faisons cela. À l’instar d’une commande, un RPC est un problème que l’hôte peut émettre et qui entraînent l’exécution de code par tous les clients. Ici, nous appelons «RpcCheckAllGoals». Chaque client vérifie individuellement si les trois AtGoals sont définis et, le cas échéant, lance la fusée.

### <a name="enjoy-your-progress"></a>Profitez de votre progression

En s’appuyant sur le chapitre précédent, nous allons démarrer la session comme auparavant. Cette fois, lorsque les utilisateurs du casque immersif obtiennent la «porte» sur leur chemin d’accès, une info-bulle s’affiche pour que seuls les utilisateurs HoloLens puissent voir. Les utilisateurs de HoloLens sont responsables de la communication de cet indice aux utilisateurs du casque immersif. La fusée démarre sur espace une fois que chaque avatar a effectué un pas à pas sur son panneau brun correspondant à l’intérieur des Volcano. La scène sera réinitialisée après 60 secondes pour vous permettre de le faire à nouveau.

## <a name="see-also"></a>Voir aussi
* [Réalité mixte - Entrées - Cours 213 : Contrôleurs de mouvement](mixed-reality-213.md)
