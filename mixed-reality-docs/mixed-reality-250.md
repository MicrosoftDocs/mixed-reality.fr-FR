---
title: MR 250 - HoloLens et des casques IMMERSIFS de partage
description: Suivez cette procédure pas à pas à l’aide de Unity, Visual Studio, HoloLens et Windows Mixed Reality casques pour connaître les détails du partage hologrammes entre les appareils de réalité mixte de codage.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, immersive, de mouvement contrôleur, le partage et la manette xbox, mise en réseau, entre les périphériques
ms.openlocfilehash: 9e1cb0d168b8bf830b4477190516cd19caef7972
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593443"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-sharing-250-hololens-and-immersive-headsets"></a>MR 250 de partage : HoloLens et des casques IMMERSIFS

Avec la flexibilité de plateforme universelle Windows (UWP), il est facile de créer une application qui s’étend sur plusieurs appareils. Grâce à cette flexibilité, nous pouvons créer des expériences exploitant les atouts de chaque appareil. Ce didacticiel couvre une expérience partagée de base qui s’exécute sur des casques IMMERSIFS HoloLens et Windows Mixed Reality. Ce contenu a été remis à l’origine lors de la conférence Microsoft Build 2017 à Seattle, WA.

**Dans ce didacticiel, nous allons :**

* Configuration d’un réseau à l’aide de UNET.
* Partager hologrammes entre les appareils de réalité mixte.
* Établir une vue différente de l’application selon le périphérique de réalité mixte est utilisé.
* Créer une expérience partagée où les utilisateurs HoloLens guident les utilisateurs des casques IMMERSIFS des énigmes simples.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>MR 250 de partage : HoloLens et des casques IMMERSIFS</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 avec le [outils de développement nécessaire](install-the-tools.md) et [configuré pour prendre en charge un casque immersif Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines).
* Une manette Xbox qui fonctionne avec votre PC.
* Au moins un appareil HoloLens et un casque immersif.
* Un réseau qui permet la diffusion UDP pour la découverte.

### <a name="project-files"></a>Fichiers projet

* Téléchargez le [fichiers](https://github.com/Microsoft/MixedReality250/archive/master.zip) requise par le projet. Extrayez les fichiers dans un facile à mémoriser l’emplacement.
* Ce projet requiert le [une version recommandée d’Unity avec prise en charge Windows Mixed Reality](install-the-tools.md).

>[!NOTE]
>Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/MixedReality250).

## <a name="chapter-1---holo-world"></a>Chapitre 1 - Holo World

>[!VIDEO https://www.youtube.com/embed/IC0rp6rLiEc]

### <a name="objectives"></a>Objectifs

Assurez-vous que l’environnement de développement est prêt à commencer avec un projet simple.

### <a name="what-we-will-build"></a>Nous allons créer

Une application qui montre un hologramme sur HoloLens ou un casque immersif Windows Mixed Reality.

### <a name="steps"></a>Étapes
* Ouvrez Unity.
    * Sélectionnez **Open**.
    * Accédez à où vous avez extrait les fichiers de projet.
    * Cliquez sur **Sélectionner un dossier**.
    * *Il prendra un peu tandis que pour Unity traiter le projet la première fois.*
* Vérifiez que la réalité mixte est activée dans Unity.
    * Ouvrez la boîte de dialogue de paramètres de build (**CTRL + MAJ + B** ou **fichier > Paramètres de Build...** ).
    * Sélectionnez **plateforme Windows universelle** puis cliquez sur **plateforme de commutation**.
    * Sélectionnez **Modifier > Paramètres du lecteur**.
    * Dans le **inspecteur** panneau sur le côté droit, développez **XR paramètres**.
    * Vérifier le **virtuel pris en charge de réalité** boîte.
    * *Réalité mixte Windows doit être le SDK de réalité virtuelle.*
* Créer une scène.
    * Dans le **hiérarchie** avec le bouton droit cliquez sur **Main Camera** sélectionnez **supprimer**.
    * À partir de **HoloToolkit > entrée > Prefabs** faites glisser **MixedRealityCameraParent** à la **hiérarchie**.
* Ajouter hologrammes à la scène
    * À partir de **AppPrefabs** faites glisser **Skybox** à la **vue de la scène**.
    * À partir de **AppPrefabs** faites glisser **gestionnaires** à la **hiérarchie**.
    * À partir de **AppPrefabs** faites glisser **île** à la **hiérarchie**.
* Enregistrez et générez
    * Enregistrer (soit **contrôle + S** ou **fichier > Enregistrer la scène**)
    * Dans la mesure où il s’agit d’une nouvelle scène, vous devrez nommer. Nom n’a pas d’importance, mais nous utilisons SharedMixedReality.
* Exporter vers Visual Studio
    * Ouvrez le menu build (**CTRL + MAJ + B** ou **fichier > Paramètres de Build**)
    * Cliquez sur **ajouter des scènes ouverts.**
    * Vérifiez **Unity C# projets**
    * Cliquez sur **Build**.
    * Dans la fenêtre Explorateur de fichiers qui s’affiche, créez un dossier nommé **application**.
    * Clic le **application** dossier.
    * Appuyez sur **sélectionnez dossier.**
    * **Attendez que la génération soit terminée**
    * Dans la fenêtre Explorateur de fichiers qui s’affiche, accédez à la **application** dossier.
    * Double-cliquez sur **SharedMixedReality.sln** pour lancer Visual Studio
* Construire à partir de Visual Studio
    * À l’aide de la barre d’outils supérieure de modifier la cible à **version** et **x86**.
    * Cliquez sur la flèche en regard **ordinateur Local** et sélectionnez **appareil** à déployer sur HoloLens
    * Cliquez sur la flèche en regard **appareil** et sélectionnez **ordinateur Local** à déployer pour le casque de réalité mixte.
    * Cliquez sur **Déboguer -> Démarrer sans débogage** ou **CTRL + F5** pour démarrer l’application.

### <a name="digging-into-the-code"></a>Analyser le code

Dans le panneau de configuration de projet, accédez à **Assets\HoloToolkit\Input\Scripts\Utilities** et double-cliquez sur **MixedRealityCameraManager.cs** pour l’ouvrir.

**Vue d’ensemble :** MixedRealityCameraManager.cs est un script simple qui ajuste les paramètres de qualité niveau et d’arrière-plan en fonction de l’appareil. Clé ici est HolographicSettings.IsDisplayOpaque, ce qui permet un script pour détecter si l’appareil est un HoloLens (IsDisplayOpaque retourne la valeur false) ou un casque immersif (IsDisplayOpaque retourne la valeur true).

### <a name="enjoy-your-progress"></a>Profitez de votre progression

À ce stade, l’application sera restituez simplement un hologramme. Nous allons ajouter interaction à l’hologramme ultérieurement. Les deux périphériques restitue l’hologramme les mêmes. Le casque immersif affiche également un arrière-plan bleu ciel et des nuages.

## <a name="chapter-2---interaction"></a>Chapitre 2 - Interaction

>[!VIDEO https://www.youtube.com/embed/Lrb1y4sQRvI]

### <a name="objectives"></a>Objectifs

Montrer comment gérer l’entrée pour une application Windows Mixed Reality.

### <a name="what-we-will-build"></a>Nous allons créer

S’appuyant sur l’application à partir de chapitre 1, nous allons ajouter des fonctionnalités permettant de l’utilisateur de capter l’hologramme et placez-le sur une surface du monde réel dans HoloLens ou sur une table virtuelle dans un casque immersive.

**Actualisateur d’entrée :** Sur HoloLens le mouvement select est la **appui en l’air**. Sur des casques IMMERSIFS, nous allons utiliser le **A** bouton sur le contrôleur de la Xbox. Pour plus d’informations sur l’entrée [Démarrer ici](gestures.md).

### <a name="steps"></a>Étapes
* Ajouter le Gestionnaire d’entrée
    * À partir de **HoloToolkit > entrée > Prefabs** faites glisser **InputManager** à **hiérarchie** en tant qu’enfant de **gestionnaires**.
    * À partir de **HoloToolkit > entrée > Prefabs > curseur** faites glisser **curseur** à **hiérarchie**.
* Ajouter un mappage Spatial
    * À partir de **HoloToolkit > SpatialMapping > Prefabs** faites glisser **SpatialMapping** à **hiérarchie**.
* Ajouter Playspace virtuel
    * Dans **hiérarchie** développez **MixedRealityCameraParent** sélectionnez **limite**
    * Dans **inspecteur** panneau Cochez la case pour activer **limite**
    * À partir de **AppPrefabs** faites glisser **VRRoom** à **hiérarchie**.
* Ajouter WorldAnchorManager
    * Dans **hiérarchie**, sélectionnez **gestionnaires**.
    * Dans **inspecteur**, cliquez sur **ajouter un composant**.
    * Type **World d’ancrage Manager**.
    * Sélectionnez **World d’ancrage Manager** pour l’ajouter.
* Ajouter TapToPlace à l’île
    * Dans **hiérarchie**, développez **île**.
    * Sélectionnez **MixedRealityLand**.
    * Dans **inspecteur**, cliquez sur **ajouter un composant**.
    * Type **appuyez sur la Place** et sélectionnez-le.
    * Vérifiez **placer Parent sur Tap**.
    * Définissez **décalage de la sélection élective** à **(0, 0.1, 0)**.
* Enregistrez et générez comme auparavant

### <a name="digging-into-the-code"></a>Analyser le code

**Script 1 - GamepadInput.cs**

Dans le panneau de configuration de projet, accédez à **Assets\HoloToolkit\Input\Scripts\InputSources** et double-cliquez sur **GamepadInput.cs** pour l’ouvrir. Dans le même chemin d’accès dans le panneau de configuration de projet, également double-cliquez sur **InteractionSourceInputSource.cs**.

Notez que les deux scripts ont une classe de base commune, BaseInputSource.

BaseInputSource conserve une référence à un InputManager, ce qui permet à un script pour déclencher des événements. Dans ce cas, l’événement InputClicked est pertinente. Cela sera important de se rappeler lorsque nous aborderons le script 2, TapToPlace. Dans le cas GamePadInput, nous interroger pour le bouton A sur le contrôleur à enfoncer, puis nous déclencher l’événement InputClicked. Dans le cas InteractionSourceInputSource, nous déclencher l’événement InputClicked en réponse à la TappedEvent.

**Script 2 - TapToPlace.cs**

Dans le panneau de configuration de projet, accédez à **Assets\HoloToolkit\SpatialMapping\Scripts** et double-cliquez sur **TapToPlace.cs** pour l’ouvrir.

La première chose que de nombreux développeurs souhaitent implémenter lors de la création d’une application HOLOGRAPHIQUE bouge hologrammes avec l’entrée de mouvement. Par conséquent, nous avons s’efforce de commenter soigneusement ce script. Quelques éléments méritent d’être mise en surbrillance pour ce didacticiel.

Tout d’abord, notez que TapToPlace implémente IInputClickHandler. IInputClickHandler expose les fonctions qui gèrent l’événement InputClicked déclenché par GamePadInput.cs ou InteractionSourceInputSource.cs. OnInputClicked est appelée quand un BaseInputSource détecte un clic pendant que l’objet avec TapToPlace est en focus. Airtapping sur HoloLens ou en appuyant sur le bouton A sur le contrôleur Xbox déclenche l’événement.

Est ensuite le code exécuté dans la mise à jour pour voir si une surface est regardée donc nous pouvons placer l’objet de jeu sur une surface, telles qu’une table. Le casque immersif n’a pas un concept de surfaces réels, par conséquent, l’objet qui représente le haut de la table (Vroom > TableThingy > Cube) a été marqué avec la couche physique SpatialMapping, donc le rayon utilisé pour effectuer un cast de la mise à jour va entrer en conflit avec le haut de la table virtuelle.

### <a name="enjoy-your-progress"></a>Profitez de votre progression

Cette fois, vous pouvez sélectionner l’îlot de le déplacer. Sur HoloLens, vous pouvez déplacer l’île à une surface réelle. Dans le casque immersif, vous pouvez déplacer l’île à la table virtuelle que nous avons ajouté.

## <a name="chapter-3---sharing"></a>Chapitre 3 - partage

>[!VIDEO https://www.youtube.com/embed/1diycJvxfDc]

### <a name="objectives"></a>Objectifs

Assurez-vous que le réseau est correctement configuré et décrit en détail comment les ancres spatiales sont partagés entre les appareils.

### <a name="what-we-will-build"></a>Nous allons créer

Nous convertira notre projet à un projet multijoueur. Nous allons ajouter l’interface utilisateur et la logique aux sessions d’hôte ou de jointure. HoloLens les utilisateurs voient l’autre dans la session avec les clouds aux supérieurs et les utilisateurs casque IMMERSIFS ont des nuages proches où le point d’ancrage est. Utilisateurs des casques IMMERSIFS voient les utilisateurs HoloLens relatif à l’origine de la scène. Les utilisateurs HoloLens voient toutes le hologramme de l’île au même endroit. Il est essentiel de noter que les utilisateurs dans des casques IMMERSIFS ne sera pas sur l’île au cours de ce chapitre, mais seront comporte de manière très similaire pour HoloLens, avec une vue d’ensemble de l’île oiseaux.

### <a name="steps"></a>Étapes
* Île de suppression et VRRoom
    * Dans **hiérarchie** avec le bouton droit **île** sélectionnez **supprimer**
    * Dans **hiérarchie** avec le bouton droit **VRRoom** sélectionnez **supprimer**
* Ajouter Usland
    * À partir de **AppPrefabs** faites glisser **Usland** à **hiérarchie**.
* À partir de **AppPrefabs** faites glisser chacune de ces éléments **hiérarchie**:
    * **UNETSharingStage**
    * **UNetAnchorRoot**
    * **UIContainer**
    * **DebugPanelButton**
* Enregistrez et générez comme auparavant

### <a name="digging-into-the-code"></a>Analyser le code

Dans le panneau de configuration de projet, accédez à **Assets\AppPrefabs\Support\SharingWithUnet\Scripts** et double-cliquez sur **UnetAnchorManager.cs**. La possibilité pour un HoloLens partager des informations de suivi avec un autre HoloLens telles que les deux périphériques peuvent partager le même espace est proche de magique. La puissance de réalité mixte est active lorsque deux ou plusieurs personnes peuvent collaborer à l’aide des mêmes données numériques.

Quelques points à souligner dans ce script :

Dans la fonction start, notez la vérification de **IsDisplayOpaque**. Dans ce cas, nous supposons que le point d’ancrage est établie. Il s’agit, car des casques IMMERSIFS n’exposent pas d’un moyen pour importer ou exporter des points d’ancrage. Si nous exécutons sur un HoloLens, toutefois, ce script implémente ancres partage entre les appareils. L’appareil qui démarre la session créera un point d’ancrage pour l’exportation. L’appareil qui rejoint une session demande l’ancre de l’appareil qui a démarré la session.

**Exportation :**

Lorsqu’un utilisateur crée une session, NetworkDiscoveryWithAnchors appellera UNETAnchorManagers CreateAnchor (fonction). Nous allons suivre CreateAnchor flux.

Nous allons commencer par effectuer certaines tâches de nettoyage, effacement de toutes les données que nous pouvons avoir collectées pour les points d’ancrage précédents. Puis nous vérifier s’il existe un point d’ancrage mis en cache à charger. Les données d’ancrage a tendance à être comprise entre 5 et 20 Mo, afin de réutiliser les ancres mis en cache peut enregistrer sur la quantité de données, vous devez donc transférer sur le réseau. Nous allons voir comment cela fonctionne un peu plus tard. Même si nous réutilisons le point d’ancrage, nous devons obtenir le point d’ancrage données prêtes en cas d’un nouveau client joint qui n’ont pas le point d’ancrage.

À propos de préparer les données d’ancrage, la classe WorldAnchorTransferBatch expose la fonctionnalité permettant de préparer les données d’ancrage pour envoyer à un autre appareil ou application et les fonctionnalités pour importer les données de point d’ancrage. Étant donné que nous sommes sur le chemin d’exportation, nous ajouter notre point d’ancrage à la WorldAnchorTransferBatch et appeler la fonction ExportAsync. ExportAsync appelle ensuite le rappel WriteBuffer qu’il génère des données pour l’exportation. Lorsque toutes les données ont été exportées ExportComplete est appelée. Dans WriteBuffer, nous ajoutons le segment de données à une liste, que nous conservons pour l’exportation. Dans ExportComplete nous convertir la liste vers un tableau. La variable AnchorName est également définie, ce qui déclenchera autres appareils pour demander le point d’ancrage si elles ne l’avez pas.

Dans certains cas, le point d’ancrage n’exporter ou créera petite quantité de données qui nous essaierons à nouveau. Ici nous suffit d’appeler CreateAnchor à nouveau.

Une fonction finale dans le chemin d’exportation est AnchorFoundRemotely. Lorsqu’un autre appareil détecte le point d’ancrage, cet appareil indiquera l’hôte et l’hôte qui utilisera comme un signal indiquant que le point d’ancrage est une « ancre bon » et peut être mis en cache.

**L’importation :**

Lorsqu’un HoloLens rejoint une session, il doit importer un point d’ancrage. Dans la fonction de mise à jour de UNETAnchorManager, le AnchorName est interrogé. Lorsque le nom de point d’ancrage change, le processus d’importation commence. Tout d’abord, nous essayons de charger le point d’ancrage portant le nom spécifié à partir du magasin local de point d’ancrage. Si nous avons déjà cela, nous pouvons l’utiliser sans avoir à télécharger les données à nouveau. Si nous ne l’avez pas, nous appelons la WaitForAnchor qui lance le téléchargement.

Lorsque le téléchargement est terminé, NetworkTransmitter_dataReadyEvent est appelée. Il signale la boucle de mise à jour pour appeler ImportAsync avec les données téléchargées. ImportAsync appellera ImportComplete lorsque le processus d’importation est terminé. Si l’importation a réussi, le point d’ancrage sera enregistré dans le magasin de lecteur local. PlayerController.cs effectue l’appel à AnchorFoundRemotely pour informer l’hôte qu’un bon point d’ancrage a été établie.

### <a name="enjoy-your-progress"></a>Profitez de votre progression

Cette fois un utilisateur avec un HoloLens hébergera une session à l’aide de la **démarrer la session** bouton dans l’interface utilisateur. Les autres utilisateurs, à la fois sur HoloLens ou un casque immersif, seront sélectionnez la session, puis le **rejoindre session** bouton dans l’interface utilisateur. Si vous avez plusieurs personnes avec des appareils HoloLens, ils bénéficieront des clouds rouge sur leurs têtes. Il y aura également un cloud bleu pour chaque casque immersif, mais les clouds bleu ne sera pas ci-dessus les casques, comme les casques n’essayant pas à trouver le même espace de coordonnées de monde en tant que les appareils HoloLens.

Ce point dans le projet est une application de partage de relation contenant-contenue ; Il ne fait pas beaucoup et peut servir d’une ligne de base. Dans les chapitres suivants, nous allons commencer la création d’une expérience pour les personnes de profiter. Pour obtenir davantage de conseils sur la conception de l’expérience partagée, cliquez ici.

## <a name="chapter-4---immersion-and-teleporting"></a>Chapitre 4 - Immersion et teleporting

>[!VIDEO https://www.youtube.com/embed/kUHZ5tCOfvY]

### <a name="objectives"></a>Objectifs

Gérer l’expérience à chaque type d’unité de réalité mixte.

### <a name="what-we-will-build"></a>Nous allons créer

Nous mettrons à jour l’application à mettre les utilisateurs casque immersives sur l’île avec une vue immersive. HoloLens les utilisateurs auront toujours la vue générale de l’île. Les utilisateurs de chaque type d’appareil peuvent voir les autres utilisateurs telles qu’elles apparaissent dans le monde. Par exemple, les utilisateurs de casque immersives peuvent voir les autres les avatars sur d’autres chemins d’accès sur l’île, et ils voient les utilisateurs de HoloLens en tant que clouds giant au-dessus de l’île. Casque immersives utilisateurs également voient le curseur de ray du pointage de regard de l’utilisateur HoloLens si l’utilisateur HoloLens consulte l’île. HoloLens s’affiche un avatar sur l’île pour représenter chaque utilisateur immersives casque.

**Mise à jour d’entrée pour le périphérique Immersive :**
* Les boutons d’animations et des pare-choc droite gauche sur le contrôleur Xbox faire pivoter le lecteur
* Maintenant le bouton de Y sur le contrôleur Xbox permettra une [teleport](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) curseur. Si le curseur a un indicateur de flèche ROTATIF lorsque vous relâchez le bouton de Y, vous serez teleported à l’emplacement du curseur.

### <a name="steps"></a>Étapes
* Ajouter MixedRealityTeleport à MixedRealityCameraParent
    * Dans **hiérarchie**, sélectionnez **Usland**.
    * Dans **inspecteur**, activer **au niveau du contrôle**.
    * Dans **hiérarchie**, sélectionnez **MixedRealityCameraParent**.
    * Dans **inspecteur**, cliquez sur **ajouter un composant**.
    * Type **Teleport de réalité mixte** et sélectionnez-le.

### <a name="digging-into-the-code"></a>Analyser le code

Les utilisateurs de casque immersives seront être attachés à leurs PC avec un câble, mais notre (île) est plus grand que le câble est long. Pour compenser, nous avons besoin de la possibilité de déplacer la caméra indépendamment de mouvement de l’utilisateur. Veuillez consulter la [page confirmation](comfort.md) pour plus d’informations sur la conception de votre application de réalité mixte (notamment personnel motion et locomotion).

Pour décrire ce processus, il sera utile de définir deux termes. Tout d’abord, **chariot** sera l’objet qui déplace la caméra indépendamment de l’utilisateur. Un objet de jeu d’enfant de la **chariot** sera le **caméra principale**. La caméra principale est attachée à la tête de l’utilisateur.

Dans le panneau de configuration de projet, accédez à **Assets\AppPrefabs\Support\Scripts\GameLogic** et double-cliquez sur **MixedRealityTeleport.cs**.

MixedRealityTeleport exécute deux tâches. Tout d’abord, il gère la rotation à l’aide des champignons. Dans la fonction de mise à jour nous interrogent pour rechercher « ButtonUp' sur LeftBumper et RightBumper. GetButtonUp uniquement retourne la valeur true sur la première image, qu'un bouton est relâché après avoir été arrêté. Si l’un des boutons avaient été levée, nous savons que l’utilisateur a besoin pour faire pivoter.

Quand nous avons faites pivoter nous un fondu et fondu à l’aide d’un script simple appelé « contrôle de fondu ». Nous faisons cela pour empêcher l’utilisateur de voir un mouvement non naturels, ce qui peut entraîner une gêne. Le fondu et arrière effet est relativement simple. Nous avons un quadruple noir négatif devant le **caméra principale**. Lorsque le fondu faire passer la valeur alpha de 0 à 1. Cela entraîne progressivement les pixels noirs du quadruple pour afficher et masquer rien derrière les. Lorsque le fondu dans faire passer la valeur alpha à zéro.

Lorsque nous calculons la rotation, notez que nous allons faire pivoter notre **chariot** , mais le calcul de la rotation autour de le **caméra principale**. Il est important que loin le **caméra principale** s’éloigne de 0,0,0, moins précise une rotation autour du chariot deviendrait à partir du point de vue de l’utilisateur. En fait, si vous ne sont pas en rotation autour de la position de la caméra, l’utilisateur passe un arc autour de la **chariot** plutôt que de la rotation.

La deuxième tâche pour MixedRealityTeleport consiste à gérer le déplacement de la **chariot**. Pour cela, utilisez SetWorldPosition. SetWorldPosition prend la position souhaitée world, la position où l’utilisateur souhaite percieve qu’ils occupent. Nous devons placer notre **chariot** à cette position moins la position locale de la **caméra principale**, comme ce décalage sera ajouté à chaque frame.

Un deuxième script appelle SetWorldPosition. Examinons ce script. Dans le panneau de configuration de projet, accédez à **Assets\AppPrefabs\Support\Scripts\GameLogic** et double-cliquez sur **TeleportScript.cs**.

Ce script est un peu plus complexe que MixedRealityTeleport. Le script est la vérification du bouton de Y sur le contrôleur de la Xbox à être maintenu enfoncé. Alors que le bouton est maintenu vers le bas un teleport curseur s’affiche et le script effectue un cast d’un rayon à partir de la position du pointage de regard de l’utilisateur. Si ce rayon est en conflit avec une surface qui est plus ou moins pointant vers le haut, la surface sera considérée comme une bonne surface à teleport à, et l’animation sur le curseur teleport sera activée. Si le rayon n’entre pas en conflit avec une surface plus ou moins pointage haut, l’animation sur le curseur sera désactivée. Lorsque le bouton Y est publié et le point calculé du rayon est une position valide, le script appelle SetWorldPosition avec la position d’une intersection le rayon.

### <a name="enjoy-your-progress"></a>Profitez de votre progression

Cette fois, vous devez rechercher un ami.

Une fois encore, un utilisateur avec le HoloLens hébergera une session. La session se connectent aux autres utilisateurs. L’application place les trois premiers utilisateurs à rejoindre dans un casque immersif sur l’un des trois chemins sur l’île. N’hésitez pas à Explorer l’île dans cette section.

Détails à noter :
1. Vous pouvez voir les visages dans les clouds, qui permet à un utilisateur immergé voir la direction dans laquelle un utilisateur HoloLens recherche.
2. Les avatars sur l’île ont d’étranglement qui assurent la rotation. Ils ne suivent pas ce que fait l’utilisateur est une réalité réelle (nous n’avons pas ces informations), mais rend la pour une expérience agréable.
3. Si l’utilisateur HoloLens consulte l’île, les utilisateurs immergés peuvent voir leur curseur.
4. Les clouds qui représentent les utilisateurs HoloLens les ombres portées.

## <a name="chapter-5---finale"></a>Chapitre 5 - Finale

>[!VIDEO https://www.youtube.com/embed/n_HDWJbfpNg]

### <a name="objectives"></a>Objectifs

Créer une expérience interactive de collaboration entre les types d’appareils de deux.

### <a name="what-we-will-build"></a>Nous allons créer

S’appuyant sur le chapitre 4, lorsqu’un utilisateur avec un casque immersif obtient près un puzzle sur l’île, les utilisateurs de HoloLens obtiendra une info-bulle avec un indice du puzzle. Une fois tous les utilisateurs de casque immersives au-delà de leurs puzzles et sur le « panneau prêt » dans la salle de fusée, lance le rocket.

### <a name="steps"></a>Étapes
* Dans **hiérarchie**, sélectionnez **Usland**.
* Dans **inspecteur**, dans **au niveau du contrôle**, vérifiez **Collaboration activer**.

### <a name="digging-into-the-code"></a>Analyser le code

Maintenant examinons LevelControl.cs. Ce script est au cœur de la logique de jeu et conserve l’état du jeu. Dans la mesure où il s’agit d’un jeu multijoueur à l’aide de UNET, nous devons comprendre le flux des données, au moins suffisamment bien pour modifier ce didacticiel. Pour une présentation plus complète de UNET, reportez-vous à la documentation de Unity.

Dans le panneau de configuration de projet, accédez à **Assets\AppPrefabs\Support\Scripts\GameLogic** et double-cliquez sur **LevelControl.cs**.

Nous devons comprendre comment un casque immersif indique qu’ils sont prêts pour le lancement de fusée. Préparation du lancement de fusée est communiquée en définissant une des trois booléennes dans une liste de booléennes qui correspondent aux trois chemins sur l’île. Valeur booléenne d’un chemin d’accès est défini lorsque l’utilisateur affecté pour le chemin d’accès est sur le pavé marron à l’intérieur de la salle de fusée. OK, maintenant aux détails.

Nous allons commencer dans la fonction Update(). Notez qu’il existe une fonction « tricher ». Nous avons utilisé ce dans le développement pour tester le lancement de fusée et de réinitialiser la séquence. Il ne fonctionnera pas dans l’expérience des utilisateurs multiples. J’espère qu’au moment où que vous intérioriser les informations suivantes vous lui faire fonctionner. Une fois que nous vérifions si nous devons tricher, nous vérifions si le lecteur local est plongé. Nous souhaitons vous concentrer sur la façon dont nous trouver que nous sommes à l’objectif. À l’intérieur d’if (immergé) vérifier, il existe un appel à CheckGoal masquage derrière le **EnableCollaboration** bool. Cela correspond à la case à cocher que vous avez coché tout en effectuant les étapes décrites dans ce chapitre. À l’intérieur de EnableCollaboration, nous voyons un appel à CheckGoal().

CheckGoal effectue quelques formules mathématiques pour voir si nous ne sont plus ou moins se trouvant sur le panneau. Lorsque nous sommes, nous Debug.Log « Arrivé à objectif », puis nous appeler « SendAtGoalMessage() ». Dans SendAtGoalMessage, nous appelons playerController.SendAtGoal. Pour vous faire gagner du temps, voici le code :

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

Notez que SendAtGoalMessage appelle CmdSendAtGoal, les appels levelState.SetGoalIndex, qui est de retour dans LevelControl.cs. À première vue, cela semble étrange. Pourquoi ne pas simplement appeler SetGoalIndex plutôt que cette étrange de routage par le biais du contrôleur player ? La raison est que nous sommes conformes au modèle de données QU'UNET utilise pour synchroniser les données. Pour empêcher tricher et écroulement, UNET nécessite que chaque objet possède un utilisateur qui a la possibilité de modifier les variables synchronisés. En outre, seul l’hôte (l’utilisateur qui a démarré la session) peut modifier des données directement. Les utilisateurs qui ne sont pas l’ordinateur hôte, mais ont autorité, doivent envoyer une commande' ' à l’hôte, ce qui modifie la variable. Par défaut l’hôte a autorité sur tous les objets, à l’exception de l’objet généré dynamiquement pour représenter l’utilisateur. Dans notre cas, cet objet a le script playercontroller. Il existe un moyen pour demander l’autorité pour un objet et apporter des modifications, mais nous choisissons de tirer parti du fait que le contrôleur de lecteur dispose des commandes autorité et l’itinéraire personnels par le biais du contrôleur player.

Autrement dit, lorsque nous avons constaté nous-mêmes à notre objectif, le joueur doit indiquer à l’hôte et l’hôte indiquera tout le monde.

Dans LevelControl.cs examiner SetGoalIndex. Ici, nous définissons la valeur d’une valeur dans un synclist (AtGoal). N’oubliez pas que nous sommes dans le contexte de l’hôte pendant que nous faisons cela. Similaire à une commande, un appel RPC est que l’hôte peut émettre entraîne tous les clients d’exécuter du code. Ici, nous appelons « RpcCheckAllGoals ». Chaque client individuellement vérifier a posteriori si tous les trois AtGoals sont définies et si tel est le cas, lancez le rocket.

### <a name="enjoy-your-progress"></a>Profitez de votre progression

S’appuyant sur le chapitre précédent, nous allons commencer la session en tant qu’avant. Cette fois que les utilisateurs dans le casque immersives obtenir la « porte » dans leur chemin d’accès, une info-bulle s’affiche que seuls les utilisateurs de HoloLens peuvent voir. Les utilisateurs de HoloLens sont responsables de la communication cet indice pour les utilisateurs dans le casque immersif. Une fois que chaque avatar a échelonnée sur son panneau marron correspondant à l’intérieur du volcan, la rocket lancera espace. La scène réinitialisera après 60 secondes, vous pouvez l’effectuer à nouveau.

## <a name="see-also"></a>Voir aussi
* [Entrée M. 213 : Contrôleurs de mouvement](mixed-reality-213.md)
