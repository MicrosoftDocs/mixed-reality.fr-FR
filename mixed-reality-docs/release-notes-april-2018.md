---
title: Notes de publication-avril 2018
description: HoloLens et notes de publication Windows Mixed Reality pour Windows 10 avril 2018 mettre à jour (également appelé RS4).
author: mattzmsft
ms.author: mazeller
ms.date: 05/21/2018
ms.topic: article
keywords: Release notes, version, windows 10, build, rs4, système d’exploitation
ms.openlocfilehash: 1fc1b43b0581234e835379fd553b78121108086e
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594595"
---
# <a name="release-notes---april-2018"></a>Notes de publication-avril 2018

Le **[mettre à jour du 10 avril 2018 Windows](https://blogs.windows.com/windowsexperience/2018/04/30/whats-new-in-the-windows-10-april-2018-update)** (également appelé RS4) inclut de nouvelles fonctionnalités pour HoloLens et Windows Mixed Reality des casques IMMERSIFS connectés au PC. 

Pour mettre à jour vers la dernière version pour les deux types d’appareil, ouvrez le **paramètres** application, accédez à **mise à jour & sécurité**, puis sélectionnez le **vérifier les mises à jour** bouton. Sur un PC Windows 10, vous pouvez également installer manuellement Windows 10 avril 2018 mettre à jour à l’aide de la [outil de création de Windows media](https://www.microsoft.com/software-download/windows10).

**Version la plus récente pour le bureau :** Mise à jour de Windows 10 avril 2018 (**10.0.17134.1**)<br>
**Version la plus récente pour HoloLens :** Mise à jour de Windows 10 avril 2018 (**10.0.17134.80**)<br>
<br>

>[!VIDEO https://www.youtube.com/embed/O-84oWjSbr0]

*Un message à partir d’Alex Kipman et vue d’ensemble des nouvelles fonctionnalités de réalité mixte dans les fenêtres de mettre à jour les 10 avril 2018*

## <a name="new-features-for-windows-mixed-reality-immersive-headsets"></a>Nouvelles fonctionnalités pour les casques IMMERSIFS Windows Mixed Reality

Windows 10 avril 2018 mise à jour comprend de nombreuses améliorations pour l’utilisation des casques Windows Mixed Reality IMMERSIFS (VR) avec votre PC de bureau, tel que : 

* **Nouveaux environnements pour la réalité mixte accueil** -vous pouvez maintenant choisir entre la Cliff House et le nouvel environnement Skyloft en sélectionnant **emplacements** dans le menu Démarrer. Nous avons également ajouté [une fonctionnalité expérimentale](add-custom-home-environments.md) qui vous permet d’utiliser des environnements personnalisés que vous avez créé.
* **Accès rapide à la capture de réalité mixte** -vous pouvez maintenant prendre des photos de réalité mixte à l’aide d’un contrôleur de mouvement. Maintenez le bouton Windows et appuyez sur le déclencheur. Cela fonctionne dans des environnements et des applications, mais ne capturent pas de contenu protégé par DRM.
* **Nouvelles options de lancement et redimensionnement contenu** -applications sont désormais automatiquement placés devant vous lorsque vous l’ouvrez dans le menu Démarrer. Vous pouvez également désormais redimensionner applications 2D en faisant glisser les bords et les coins de la fenêtre.
* **Accéder facilement au contenu avec la commande « teleport » voix** -vous pouvez désormais rapidement teleport pour rester devant contenu dans la réalité mixte Windows domestique par gazing au contenu et en disant « teleport. »
* **[Animée lanceurs d’applications 3D](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#animation-guidelines) et [objets 3D décoratifs](enable-placement-of-3d-models-in-the-home.md) pour la réalité mixte accueil** -vous pouvez maintenant ajouter une animation à lanceurs d’applications 3D et permettre aux utilisateurs de placer des modèles 3D décoratifs à partir d’une application de page Web ou 2D dans le Windows Mixed Reality domestique.
* **[Améliorations apportées à Windows Mixed Reality for SteamVR](updating-your-steamvr-application-for-windows-mixed-reality.md)**  -Windows Mixed Reality pour SteamVR manque de « accès en avant-première » avec des mises à niveau, y compris : retour haptique lors de l’utilisation de contrôleurs de mouvement, améliorer les performances et la fiabilité et améliorations de l’apparence des contrôleurs de mouvement dans SteamVR.
* **Autres améliorations** -paramètres de performances automatique ont été mis à jour pour fournir une expérience plus optimisée (vous pouvez [remplacer manuellement](#visual-quality) ce paramètre). Le programme d’installation fournit désormais que des informations détaillées sur les problèmes de compatibilité courants avec USB 3.0 contrôleurs et cartes graphiques.

## <a name="new-features-for-hololens"></a>Nouvelles fonctionnalités pour HoloLens

Windows 10 avril 2018, mise à jour est arrivé pour tous les clients de HoloLens ! Cette mise à jour est doté d’améliorations qui ont été introduites depuis la dernière version majeure du logiciel HoloLens dans [août 2016](release-notes-august-2016.md).

### <a name="for-everyone"></a>Pour tout le monde

<table>
  <tr>
    <th>Fonctionnalité</th><th>Détails</th><th>Instructions</th>
  </tr>
  <tr>
    <td>Placement automatique du contenu 2D et 3D au lancement</td><td>Une application UWP du Lanceur ou 2D d’application 2D automatique-emplacements dans le monde entier à une taille optimale et la distance au lancement au lieu d’obliger l’utilisateur à placer. Si un <a href="app-views.md">application captivante</a> utilise un lanceur d’applications 2D au lieu d’un <a href="3d-app-launcher-design-guidance.md">Lanceur d’applications 3D</a>, l’application captivante lance à partir du Lanceur d’applications 2D même comme dans RS1.<br><br>Un lanceur d’applications 3D dans le menu Démarrer également automatique-emplacements dans le monde entier. Au lieu de lancement automatique de l’application, les utilisateurs peuvent puis cliquez sur le service de lancement pour lancer l’application captivante. Contenu 3D ouvert à partir de l’application hologrammes et bord également automatique-emplacements dans le monde.</td><td>Lors de l’ouverture d’une application dans le menu Démarrer, vous n’avez plus demandera de le placer dans le monde.<br><br>Si l’application 2D /<a href="3d-app-launcher-design-guidance.md">Lanceur d’applications 3D</a> sélection élective n’est pas optimale, vous pouvez les déplacer facilement à l’aide de la nouvelle manipulations FLUIDE application décrites ci-dessous. Vous pouvez également repositionner le contenu de lanceur/3D application 2D en disant « Déplacer ce » puis en utilisant du pointage de regard pour repositionner le contenu.</td>
  </tr>
  <tr>
    <td>Manipulation de l’application FLUIDE</td><td>Déplacer, redimensionner et faire pivoter de contenu 2D et 3D sans avoir à passer en mode « Ajuster ».</td><td>Pour déplacer un 2D application UWP ou le Lanceur d’applications 2D, remplacez simplement à sa barre de l’application et puis utiliser le tap contenir + faire glisser des mouvements. Vous pouvez déplacer un contenu 3D en gazing n’importe où sur l’objet et à l’aide de puis appuyez sur + contenir + faire glisser.<br><br>Pour redimensionner le contenu 2D, remplacez son coin. Le curseur de regards se transforme en curseur de redimensionnement, puis vous pouvez appuyez sur + Maintenez + faire glisser pour redimensionner. Vous pouvez également effectuer le contenu 2D plus grands ou large en examinant ses bords en faisant glisser.<br><br>Pour redimensionner le contenu 3D, soulevez des deux vos mains dans le cadre de mouvement, doigts dans la position de prête. Vous verrez le curseur se transformer en un état avec 2 petites mains. Faire le drainage et maintenez le mouvement à deux vos mains. Déplacement de vos mains proches ou éloigner, vous allez modifier la taille de l’objet. Déplacement de vos mains vers l’avant et vers l’arrière par rapport aux autres fera pivoter l’objet. Vous pouvez également redimensionner/faire pivoter contenu 2D de cette façon.</td>
  </tr>
  <tr>
    <td>Redimensionnement horizontal d’application 2D avec la redistribution</td><td>Rendre une application UWP la 2D plus large dans le rapport hauteur / largeur pour afficher le contenu de l’application plus. Par exemple, rendre l’application de messagerie assez large pour afficher le volet de visualisation.</td><td>Remplacez simplement sur le bord gauche ou droit de l’application UWP 2D pour le curseur de redimensionnement, puis utiliser le tap + maintenez + faire glisser le mouvement à redimensionner.</td>
  </tr>
  <tr>
    <td>Prise en charge de la commande voix développée</td><td>Vous pouvez effectuer la plus simple en utilisant votre voix.</td><td>Essayez ces commandes vocales :<ul><li>« Accédez à démarrer » - permet d’afficher le menu Démarrer ou quitte un <a href="app-views.md">application captivante</a>.</li><li>« Cela déplacer » - vous permet de déplacer un objet.</li></ul></td>
  </tr>
  <tr>
    <td>Applications Photos et hologrammes mises à jour</td><td>Application hologrammes mise à jour avec la nouvelle hologrammes. Application de Photos mis à jour.</td><td>Vous remarquerez une apparence mise à jour pour les applications hologrammes et Photos. L’application hologrammes inclut plusieurs hologrammes nouvelle et un créateur d’étiquette pour la création simplifiée de texte.</td>
  </tr>
  <tr>
    <td>Amélioration de capture de réalité mixte</td><td>Début de raccourci de matériel et de fin MRC vidéo.</td><td>Maintenez la touche Monter le Volume + bas pour 3 secondes commencer l’enregistrement vidéo de cette option. Cliquez de nouveau à la fois sur ou utiliser le mouvement de bloom pour se terminer.</td>
  </tr>
  <tr>
    <td>Espaces consolidées</td><td>Simplifier la gestion de l’espace pour hologrammes à un seul espace.</td><td>HoloLens trouve votre espace automatiquement et ne requiert plus vous permettent de gérer ou sélectionnez des espaces. Si vous rencontrez des problèmes avec hologrammes autour de vous, vous pouvez accéder à <b>Paramètres > système > hologrammes > Supprimer les plus proches hologrammes</b>. Si nécessaire, vous pouvez également sélectionner <b>supprimer tous les hologrammes</b>.</td>
  </tr>
  <tr>
    <td>Immersion audio améliorée</td><td>Vous pouvez désormais entendre HoloLens mieux dans des environnements bruyants et rencontrez plus réaliste son à partir d’applications comme leur son est masqué par des parois réels détectés par l’appareil.</td><td>Vous n’avez rien à faire pour bénéficier du son spatial amélioré.</td>
  </tr>
  <tr>
    <td>Explorateur de fichiers</td><td>Déplacer et supprimer des fichiers à partir de HoloLens.</td><td>Vous pouvez utiliser la <b>Explorateur de fichiers</b> application à déplacer et supprimer des fichiers à partir de HoloLens.<br><br><b>Conseil :</b> Si vous ne voyez pas tous les fichiers, le filtre « Récent » peut être actif (icône d’horloge est mise en surbrillance dans le volet gauche). Pour résoudre le problème, sélectionnez le <b>ce périphérique</b> document icône dans le volet de gauche (sous l’icône d’horloge), ou ouvrez le menu et sélectionnez <b>ce périphérique</b>.
</td>
  </tr>
  <tr>
    <td>Prise en charge du protocole MTP (Media Transfer Protocol)</td><td>Permet à votre ordinateur de bureau pour accéder à vos bibliothèques (photos, vidéos, documents) sur HoloLens pour faciliter le transfert.</td><td>Similaire à d’autres appareils mobiles, connectez votre HoloLens à votre PC pour faire apparaître <b>Explorateur de fichiers</b> pour accéder à vos bibliothèques HoloLens (photos, vidéos, documents) pour faciliter le transfert.<br><br><b>Astuces :</b><ul><li>Si vous ne voyez pas tous les fichiers, vérifiez que vous être connecté à votre HoloLens pour activer l’accès à vos données.</li><li>À partir de <b>Explorateur de fichiers</b> sur votre PC, vous pouvez sélectionner <b>propriétés de l’appareil</b> pour voir le numéro de version de système d’exploitation HOLOGRAPHIQUE Windows (version du microprogramme) et le numéro de série d’appareil.</li></ul><b>Problème connu :</b> Changement de nom HoloLens via <b>Explorateur de fichiers</b> sur votre PC n’est pas activé.</td>
  </tr>
  <tr>
    <td>Prise en charge de réseau du portail captif pendant l’installation</td><td>Vous pouvez désormais configurer votre HoloLens sur un réseau d’invité hôtels, centres de conférence, de magasins de détail ou les entreprises qui utilisent captive portal.</td><td>Pendant l’installation, sélectionnez le réseau, vérifiez la connexion automatique si vous le souhaitez et entrez les informations de réseau comme vous y êtes invité.</td>
  </tr>
  <tr>
    <td>Synchronisation de photo et vidéo via l’application OneDrive</td><td>Vos photos et vidéos à partir de HoloLens vont être synchronisés par le biais de l’application OneDrive à partir du Microsoft Store à la place de directement par le biais de l’application de Photos.</td><td>Pour ce faire, téléchargez et lancez l’application OneDrive à partir du Store. Lors de la première exécution vous devez être invité à charger automatiquement vos photos sur OneDrive, ou vous pouvez trouver l’option dans les paramètres d’application.</td>
  </tr>
</table>

### <a name="for-developers"></a>Pour les développeurs

<table>
  <tr>
    <th>Fonctionnalité</th><th>Détails</th><th>Instructions</th>
  </tr>
  <tr>
    <td>Améliorations apportées au mappage spatial</td><td>Améliorations de qualité, de simplification et de performances.</td><td>Maillage de mappage spatial apparaîtra plus propre : moins de triangles sont nécessaires pour représenter le même niveau de détail. Vous pouvez remarquer les modifications de la densité de triangle dans la scène.</td>
  </tr>
  <tr>
    <td>Sélection automatique du point de focus en fonction de la mémoire tampon de profondeur</td><td>La soumission d’un mémoire tampon de profondeur pour Windows permet HoloLens sélectionner un point de focus automatiquement pour optimiser la stabilité hologramme.</td><td>Dans Unity, accédez à <b>Modifier > Paramètres du projet > lecteur > onglet de la plateforme Windows universelle > XR paramètres</b>, développez le <b>SDK de réalité mixte Windows</b> d’élément et vous assurer <b>activer la mémoire tampon de profondeur Partage</b> est activée. Cela sera vérifié automatiquement pour les nouveaux projets.<br><br>Pour les applications DirectX, vérifiez que vous appelez le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer">CommitDirect3D11DepthBuffer </a> méthode sur <b>HolographicRenderingParameters</b> chaque frame pour fournir de la mémoire tampon de profondeur à Windows.
</td>
  </tr>
  <tr>
    <td>Modes de reprojection HOLOGRAPHIQUE</td><td>Vous pouvez maintenant désactiver positionnelle reprojection sur HoloLens pour améliorer la stabilité hologramme de façon rigide verrouillé de corps de contenu tels que de la vidéo de 360 degrés.</td><td>Dans Unity, définissez <a href="https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.ReprojectionMode.html">HolographicSettings.ReprojectionMode</a> à <a href="https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.HolographicReprojectionMode.html">HolographicReprojectionMode.OrientationOnly</a> lorsque tout le contenu est dans la vue préconçus strictement verrouillé de corps.<br><br>Pour les applications DirectX, définissez <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.reprojectionmode"> HolographicCameraRenderingParameters.ReprojectionMode</a> à <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicreprojectionmode">HolographicReprojectionMode.OrientationOnly</a> lorsque tout le contenu est dans la vue préconçus strictement verrouillé de corps.</td>
  </tr>
  <tr>
    <td>API de personnalisation d’application</td><td>API de Windows en savoir plus sur où votre application est en cours d’exécution, telles que si l’affichage du périphérique est (HoloLens) transparent ou opaque (casque immersif) et si vue en 2D d’une application UWP s’affichent dans l’interpréteur de commandes HOLOGRAPHIQUE.</td><td>Unity a exposé précédemment manuellement <a href="https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.IsDisplayOpaque.html">HolographicSettings.IsDisplayOpaque</a> d’une manière qui fonctionnait avant même de cette build.<br><br>Pour les applications DirectX, vous pouvez désormais accéder API existantes comme <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicdisplay.isopaque">HolographicDisplay.GetDefault(). IsOpaque</a> et <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.preview.holographic.holographicapplicationpreview.iscurrentviewpresentedonholographicdisplay">HolographicApplicationPreview.IsCurrentViewPresentedOnHolographicDisplay</a> sur HoloLens également.
</td>
  </tr>
  <tr>
      <td>Mode de recherche</td><td>Permet aux développeurs d’accéder aux clés capteurs HoloLens lorsque vous créez des applications universitaires et industrielles pour tester de nouvelles idées dans les champs de vision par ordinateur et de la robotique, y compris :<ul><li>Les quatre environnement suivi des caméras de surveillance</li><li>Deux versions des données de la caméra de mappage de profondeur</li><li>Deux versions d’un flux réflectivité de runtime d’intégration</li></ul></td><td><a href="research-mode.md">Documentation de mode de recherche</a><br><a href="https://github.com/Microsoft/HoloLensForCV">Recherche en mode exemples d’applications</a></td>
  </tr>
</table>

### <a name="for-commercial-customers"></a>Pour les clients commerciaux

<table>
  <tr>
    <th>Fonctionnalité</th><th>Détails</th><th>Instructions</th>
  </tr>
  <tr>
    <td>Utiliser plusieurs comptes d’utilisateur Azure Active Directory sur un seul appareil</td><td>Partager un HoloLens avec plusieurs utilisateurs Azure AD, chacun ayant leurs propres paramètres utilisateur et les données utilisateur sur l’appareil.</td><td><a href="https://docs.microsoft.com/hololens/hololens-multiple-users">Centre IT Pro : HoloLens partage avec plusieurs personnes</a></td>
  </tr>
  <tr>
    <td>Modifier le réseau Wi-Fi sur la connexion</td><td>Modifier le réseau Wi-Fi avant la connexion pour permettre à un autre utilisateur se connecter avec son compte d’utilisateur Azure AD pour la première fois, permettant aux utilisateurs de partager des périphériques à différents emplacements et de sites de travail.</td><td>Sur l’écran de connexion, vous pouvez utiliser l’icône de réseau sous le champ de mot de passe pour se connecter à un réseau. Cela est utile lorsque c’est la première fois que la connexion à un appareil.</td>
  </tr>
  <tr>
    <td>Inscription unifiée</td><td>Il est désormais facile pour un utilisateur de HoloLens qui a configuré l’appareil avec un compte Microsoft personnel pour ajouter un compte professionnel (Azure AD) et joindre l’appareil à leur serveur de gestion des appareils mobiles.</td><td>Simplement vous connecter avec un compte Azure AD et l’inscription s’effectue automatiquement.</td>
  </tr>
  <tr>
    <td>Synchronisation du courrier électronique sans l’inscription MDM</td><td>Prise en charge pour la synchronisation de messagerie Exchange Active Sync (EAS) sans nécessiter l’inscription MDM.</td><td>Vous pouvez désormais synchroniser le courrier électronique sans l’inscription dans des appareils mobiles. Vous pouvez configurer l’appareil avec un Account Microsoft, téléchargez et installez l’application de messagerie et ajouter un compte de messagerie professionnel directement.</td>
  </tr>
</table>

### <a name="for-it-pros"></a>Pour les professionnels de l'informatique

<table>
  <tr>
    <th>Fonctionnalité</th><th>Détails</th><th>Instructions</th>
  </tr>
  <tr>
    <td>Nouveau nom de « Windows Holographic for Business » du système d’exploitation</td><td>Désactivez l’édition d’affectation de noms afin de réduire la confusion quant à l’application de licence de mise à niveau d’édition lorsque les fonctionnalités commerciales Suite sont activées sur HoloLens.</td><td>Vous pouvez voir quelle édition de Windows HOLOGRAPHIQUE sur votre appareil dans <b>Paramètres > système > sur</b>. « Windows Holographic for Business » s’affiche si une mise à jour de l’édition a été appliqué pour activer des fonctionnalités commerciales Suite. Découvrez comment <a href="https://docs.microsoft.com/hololens/hololens-upgrade-enterprise">déverrouiller Windows Holographic for Business, les fonctionnalités</a>.</td>
  </tr>
  <tr>
  <td>Windows Configuration Designer (WCD)</td><td>Créer et modifier des packages d’approvisionnement pour configurer HoloLens via application WCD mise à jour. Assistant HoloLens simple pour la mise à jour de l’édition, OOBE configurable, région/fuseau horaire, jeton d’Azure AD en masse, réseau et développeur CSP. Éditeur avancé filtrée sur HoloLens pris en charge les options, y compris les accès affecté et fournisseurs de gestion de compte.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning">Centre IT Pro : Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
    <td>Programme d’installation configurable (OOBE)</td><td>Masquer d’étalonnage, mouvement/regards de formation et des écrans de configuration Wi-Fi pendant l’installation.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning#create-a-provisioning-package-for-hololens-using-the-hololens-wizard">Centre IT Pro : Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
    <td>Support de jeton Azure AD en bloc</td><td>Inscrivez-vous à l’avance l’appareil à l’annuaire Azure AD pour le flux de programme d’installation utilisateur plus rapide.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning">Centre IT Pro : Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
  <td>Fournisseur de services de configuration DeveloperSetup</td><td>Déployer un profil pour configurer HoloLens en mode développeur. Utile pour les appareils de développement et de démonstration.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning">Centre IT Pro : Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
  <td>Fournisseur de services de configuration AccountManagement</td><td>Partager un appareil HoloLens et supprimer les données de l’utilisateur après la déconnexion ou les seuils d’inactivité/stockage pour une utilisation temporaire. Prend en charge les comptes Azure AD.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning">Centre IT Pro : Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
  <td>Accès affecté</td><td>L’accès est attribué pour les travailleurs de la première ligne ou des démonstrations de Windows. Verrouillage unique ou des applications multiples. Pas nécessaire au développeur de déverrouillage.</td><td><a href="https://docs.microsoft.com/hololens/hololens-kiosk">Centre IT Pro : Configurer HoloLens en mode plein écran</a></td>
  </tr>
  <tr>
  <td>Accès invité pour les appareils plein écran</td><td>Affecté l’accès avec un compte invité de sans mot de passe pour des démonstrations de Windows. Verrouillage unique ou des applications multiples. Pas nécessaire au développeur de déverrouillage.</td><td><a href="https://docs.microsoft.com/hololens/hololens-kiosk#guest">Centre IT Pro : Configurer HoloLens en mode plein écran</a></td>
  </tr>
  <tr>
    <td>Configurer des diagnostics (OOBE)</td><td>Obtenir les journaux de diagnostic à partir de HoloLens afin de résoudre les échecs de connexion Azure AD (avant que le Hub de commentaires est disponible à l’utilisateur dont la connexion a échoué).</td><td>Lorsque le programme d’installation ou de connexion échoue, choisissez le nouveau <b>collecter des informations</b> option pour obtenir des journaux de diagnostic pour le dépannage.</td>
  </tr>
  <tr>
    <td>Expiration du mot indéfini compte local</td><td>Supprimer une interruption du périphérique réinitialisé lors de l’expiration du mot de passe de compte local.</td><td>Lorsque vous configurez un compte local, vous n’avez plus besoin de modifier le mot de passe tous les 42 jours dans <b>paramètres</b>, comme le mot de passe du compte n’est plus arrive à expiration.</td>
  </tr>
  <tr>
    <td>Détails et l’état de synchronisation de gestion des appareils mobiles</td><td>Fonctionnalités Windows standard pour comprendre l’état de synchronisation de gestion des appareils mobiles et des détails à partir de HoloLens.</td><td>Vous pouvez vérifier l’état de synchronisation de gestion des appareils mobiles pour un appareil dans <b>Paramètres > comptes > accès Professionnel ou scolaire > Info</b>. Dans le <b>état de synchronisation d’appareil<b> section, vous pouvez lancer une synchronisation, consultez les domaines gérés par gestion des appareils mobiles et créer et exporter un rapport de diagnostics avancés.</td>
  </tr>
</table>

## <a name="known-issues"></a>Problèmes connus

Nous avons travaillé dur pour fournir une excellente expérience de réalité mixte Windows, mais nous sommes toujours le suivi des problèmes connus. Si vous trouvez d’autres, veuillez [envoyez-nous vos commentaires](give-us-feedback.md).

### <a name="hololens"></a>HoloLens

#### <a name="after-update"></a>Après mise à jour

Vous pouvez remarquer les problèmes suivants après la mise à jour à partir de RS1 à RS4 sur votre HoloLens :
* **Réinitialiser des codes confidentiels** -le 3 x 3 applications épinglées à votre menu Démarrer reprennent les valeurs par défaut après la mise à jour. 
* **Applications et réinitialisation de hologrammes placé** -applications placés dans votre monde sera supprimés après la mise à jour et devez à nouveau placer tout au long de votre espace. 
* **Hub de commentaires ne peut-être pas lancer immédiatement** -immédiatement après la mise à jour, il prendra quelques minutes avant que vous êtes en mesure de lancer certaines applications de la boîte de réception, comme Hub de commentaires, pendant qu’ils se mettent à jour. 
* **Les certificats Wi-Fi d’entreprise doivent être de nouveau synchronisé** -nous nous intéressons à un problème qui nécessite le HoloLens être connecté à un autre réseau afin que les certificats d’entreprise être synchronisé de nouveau à l’appareil avant qu’il soit en mesure de se reconnecter à réseaux d’entreprise à l’aide de certificats. 
* **Lecture de vidéo HEVC H.265 ne fonctionne pas** -Applications qui tentent de lire les vidéos H.265 recevront un message d’erreur. La solution de contournement consiste à [accéder à la Windows Device Portal](using-the-windows-device-portal.md), sélectionnez **applications** dans la barre de navigation de gauche, et **supprimer** l’application HEVC. Ensuite, installez la dernière version [Extension de vidéo HEVC](https://www.microsoft.com/p/hevc-video-extensions/9nmzlz57r3t7) à partir du Microsoft Store. Nous étudions le problème. 

#### <a name="for-developers-updating-hololens-apps-for-devices-running-windows-10-april-2018-update"></a>Pour les développeurs : applications HoloLens pour les appareils exécutant Windows de la mise à jour de la mise à jour du 10 avril 2018

Avec une belle liste de [nouvelles fonctionnalités](#new-features-for-hololens), le Kit de développement Windows 10 avril 2018 Update (RS4) pour HoloLens applique certains comportements de code qui n’a pas le fait de versions précédentes :
* **Demandes d’autorisation d’utiliser des ressources sensibles (caméra, microphone, etc.).**  -RS4 sur HoloLens appliquera des demandes d’autorisation pour les applications ayant l’intention d’accéder aux ressources sensibles, telles que l’appareil photo ou d’un microphone. Rs1 sur HoloLens n’a pas entraîné ces invites, par conséquent, si votre application suppose un accès immédiat à ces ressources, il peut se bloquer dans RS4 (même si l’utilisateur accorde l’autorisation de la ressource demandée). Veuillez lire les informations pertinentes [article de déclarations de fonction d’application UWP](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations) pour plus d’informations.
* **Appels aux applications en dehors de votre propre** -RS4 sur HoloLens impose l’utilisation appropriée de la [ *Windows.System.Launcher* classe](https://docs.microsoft.com/uwp/api/Windows.System.Launcher) pour lancer une autre application à partir du vôtre. Par exemple, nous avons constaté des problèmes avec les applications appelant *Windows.System.Launcher.LaunchUriForResultsAsync* à partir d’un thread d’interface utilisateur - ASTA. Cela devrait aboutir dans RS1 sur HoloLens, mais RS4 nécessite l’appel doit être exécuté sur le thread d’interface utilisateur.

### <a name="windows-mixed-reality-on-desktop"></a>Réalité mixte de Windows sur le bureau

#### <a name="visual-quality"></a>Qualité visuelle

* Si vous remarquez après le 10 avril 2018 mise à jour Windows que les graphiques sont plus floues qu’avant, ou que le champ de vision semble plus petite sur votre casque, le paramètre de performance automatique peut avoir été modifié afin de maintenir un taux de trames suffisante sur moins puissants carte graphique (telles que Nvidia 1050). Vous pouvez substituer manuellement ce (si vous choisissez) en accédant à **Paramètres > une réalité mixte > affichage de casque > options d’expérience > modification** et changez « Automatique » en « 90 Hz. » Vous pouvez également essayer de modifier **qualité visuelle** (sur la même page de paramètres) à « High ».

#### <a name="windows-mixed-reality-setup"></a>Programme d’installation Windows Mixed Reality

* Lorsque vous configurez Windows avec un casque connecté, votre moniteur PC peut paraître vide. Débranchez votre casque pour activer la sortie vers le moniteur de votre ordinateur pour terminer l’installation de Windows.
* Si vous n’avez pas de casque connecté, vous risquez de manquer des conseils supplémentaires lorsque vous visitez tout d’abord Windows Mixed Reality domestique.
* Autres appareils Bluetooth peuvent provoquer des interférences avec des contrôleurs de mouvement. Si les contrôleurs de mouvement rencontrent des problèmes de connexion/de couplage/de suivi, assurez-vous que la case d’option Bluetooth (si une clé externe) est connecté à un emplacement dégagé et pas immédiatement en regard d’un autre récepteur Bluetooth. Essayez également d’autres périphériques Bluetooth hors tension pendant les sessions Windows Mixed Reality pour voir s’il est utile.

#### <a name="games-and-apps-from-the-microsoft-store"></a>Jeux et les applications à partir du Microsoft Store

* Certains jeux gourmandes en ressources graphiques, tels que Forza Motorsport 7, peut provoquer des problèmes de performances sur des PC moins compatibles lors de la lecture à l’intérieur de réalité mixte Windows.

#### <a name="audio"></a>Audio

* Si vous avez Cortana est activé sur votre ordinateur hôte avant d’utiliser votre casque Windows Mixed Reality, vous risquez de perdre spatiale simulation audio appliquée aux applications que vous placez autour de Windows Mixed Reality domestique. 
   * La solution de contournement consiste à activer « Windows Sonic pour un casque » sur tous les périphériques audio connectés à votre PC, et même votre casque audio appareil connecté :
      1. Cliquez sur l’icône haut-parleur dans la barre des tâches, puis sélectionnez à partir de la liste des périphériques audio.
      2. Avec le bouton droit sur la barre des tâches, l’icône de l’orateur et sélectionnez « Windows Sonic pour un casque » dans le menu « Le programme d’installation de l’orateur ».
      3. Répétez ces étapes pour tous les périphériques audio (points de terminaison).
   * Une autre option consiste à désactiver « Cortana de permettent de répondre à Hey Cortana » **paramètres** > **Cortana** sur votre bureau avant le lancement de Windows Mixed Reality.
* Quand un autre périphérique USB multimédia (par exemple, une webcam) partage le même concentrateur USB (externe ou à l’intérieur de votre PC) avec le casque Windows Mixed Reality, dans de rares cas audio jack/un casque du casque peut avoir un son bourdonnement ou sans contenu audio du tout. Vous pouvez résoudre ce problème en votre casque sur un port USB qui ne pas partager le même hub en tant que l’autre appareil, et vous déconnecter ou de désactiver votre appareil de multimédia USB.
* Dans les cas très rares, concentrateur USB de l’hôte du PC ne peut pas fournir une puissance suffisante pour le casque de réalité mixte Windows et vous pouvez remarquer une rafale de bruit le casque connecté au casque.

#### <a name="holograms"></a>Hologrammes

* Si vous avez placé un grand nombre de hologrammes dans votre Windows Mixed Reality domestique, certains peuvent disparaître et réapparaître comme vous regardez autour. Pour éviter ce problème, supprimez certaines des hologrammes dans la zone de la réalité mixte Windows accueil.

#### <a name="motion-controllers"></a>Contrôleurs de mouvement

* Si l’entrée n’est pas dirigée vers le casque, le contrôleur de mouvement disparaît brièvement lorsque qui se trouve en regard de la limite de la salle. En appuyant sur Win + Y pour garantir une bannière bleue sur le Moniteur du bureau résoudre cela. 
* Parfois, lorsque vous cliquez sur une page web dans Microsoft Edge, le contenu sera zoom au lieu de clic.

#### <a name="desktop-app-in-the-windows-mixed-reality-home"></a>Application de bureau dans Windows Mixed Reality domestique

* L’outil capture ne fonctionne pas dans l’application de bureau.
* Application de bureau ne conserve pas de paramètre lors du redémarrage.
* Si vous utilisez version préliminaire du portail de réalité mixte sur votre bureau, lors de l’ouverture de l’application de bureau dans Windows Mixed Reality domestique, vous pouvez remarquer l’effet miroir infinie. 
* Exécution de l’application de bureau peut affecter les performances sur non - Ultra mixte réalité PC Windows ; Il n’est pas recommandé.  
* Application de bureau peut lancer automatiquement, car une fenêtre invisible sur le bureau a le focus. 
* Contrôle de compte d’utilisateur bureau invite rendra casque s’affichent en noir avant la fin de l’invite.

#### <a name="windows-mixed-reality-for-steamvr"></a>Windows Mixed Reality pour SteamVR

* Vous devrez peut-être lancer le portail de réalité mixte après la mise à jour pour les mises à jour de logiciels nécessaires pour Windows 10 avril 2018 mise à jour terminées avant de lancer SteamVR. 
* Vous devez être sur une version récente de Windows Mixed Reality pour SteamVR de rester compatible avec les fenêtres de mettre à jour du 10 avril 2018. Assurez-vous que les mises à jour automatiques sont activées pour la réalité mixte Windows pour SteamVR, ce qui se trouve dans la section « Logiciel » de votre bibliothèque dans le flux.  

#### <a name="other-issues"></a>Autres problèmes

>[!IMPORTANT]
>Une version précoce de Windows 10 avril 2018 mise à jour vers Insiders (version 17134.5) n’a pas un élément logiciel nécessaire pour exécuter Windows Mixed Reality. Nous vous recommandons d’éviter cette version, si vous utilisez Windows Mixed Reality. 

Nous avons identifié une régression des performances lors de l’utilisation de la Surface Book 2 sur la version initiale de cette mise à jour (10.0.17134.1) nous nous efforçons de résoudre dans un correctif de mise à jour à venir. Nous vous suggérons d’attendre jusqu'à ce que ce problème a été résolu avant la mise à jour manuellement ou en attente de la mise à jour de déploiement normalement.

## <a name="provide-feedback-and-report-issues"></a>Fournir des commentaires et signalez les problèmes

Utilisez le [application Hub de commentaires sur votre PC Windows 10 ou sur HoloLens](give-us-feedback.md) pour fournir des commentaires et signalez les problèmes. À l’aide du Hub de commentaires garantit que toutes les informations de diagnostic nécessaire sont incluses pour aider à nos ingénieurs déboguer rapidement et de résoudre le problème.

>[!NOTE]
>Veillez à accepter l’invite vous demandant si vous souhaitez que le Hub de commentaires pour accéder à votre dossier Documents (sélectionnez **Oui** lorsque vous y êtes invité).

## <a name="prior-release-notes"></a>Notes de version antérieure

* [Notes de publication-octobre 2017](release-notes-october-2017.md)
* [Notes de publication-août 2016](release-notes-august-2016.md)
* [Notes de publication-mai 2016](release-notes-may-2016.md)
* [Notes de publication-mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Prise en charge de casque immersive (lien externe)](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality)
* [Prise en charge de HoloLens (lien externe)](https://support.microsoft.com/products/hololens)
* [Installer les outils](install-the-tools.md)
* [Envoyez-nous vos commentaires](give-us-feedback.md)

