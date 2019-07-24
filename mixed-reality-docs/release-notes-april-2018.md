---
title: Notes de publication-2018 avril
description: Notes de publication de HoloLens et de Windows Mixed Reality pour la mise à jour 2018 d’avril de Windows 10 (également appelée RS4).
author: mattzmsft
ms.author: mazeller
ms.date: 05/21/2018
ms.topic: article
keywords: Notes de publication, version, Windows 10, Build, RS4, système d’exploitation
ms.openlocfilehash: 1fc1b43b0581234e835379fd553b78121108086e
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524176"
---
# <a name="release-notes---april-2018"></a>Notes de publication-2018 avril

La **[mise à jour 2018 de Windows 10 avril](https://blogs.windows.com/windowsexperience/2018/04/30/whats-new-in-the-windows-10-april-2018-update)** (également connue sous le nom de RS4) comprend de nouvelles fonctionnalités pour les casques immersifs et les casques immersifs de la réalité mixte Windows, connectés aux PC. 

Pour effectuer une mise à jour vers la dernière version pour le type d’appareil, ouvrez l’application **paramètres** , accédez à **mettre à jour & sécurité**, puis sélectionnez le bouton **Rechercher les mises à jour** . Sur un PC Windows 10, vous pouvez également installer manuellement la mise à jour 2018 d’avril de Windows 10 à l’aide de l' [outil de création de média Windows](https://www.microsoft.com/software-download/windows10).

**Dernière version pour ordinateur de bureau:** Mise à jour 2018 d’avril de Windows 10 (**10.0.17134.1**)<br>
**Dernière version pour HoloLens:** Mise à jour 2018 d’avril de Windows 10 (**10.0.17134.80**)<br>
<br>

>[!VIDEO https://www.youtube.com/embed/O-84oWjSbr0]

*Message d’Alex Kipman et vue d’ensemble des nouvelles fonctionnalités de réalité mixte de la mise à jour 2018 de Windows 10 avril*

## <a name="new-features-for-windows-mixed-reality-immersive-headsets"></a>Nouvelles fonctionnalités pour les casques immersifs de Windows Mixed Reality

La mise à jour 2018 d’avril de Windows 10 offre de nombreuses améliorations pour l’utilisation des casques de Windows Mixed Reality (VR) avec votre ordinateur de bureau, par exemple: 

* **Nouveaux environnements pour la réalité mixte Accueil** : vous pouvez maintenant choisir entre la maison de la falaise et le nouvel environnement Skyloft en sélectionnant **emplacements** dans le menu Démarrer. Nous avons également ajouté [une fonctionnalité expérimentale](add-custom-home-environments.md) qui vous permettra d’utiliser des environnements personnalisés que vous avez créés.
* **Accès rapide à la capture de la réalité mixte** : vous pouvez désormais prendre des photos de réalité mixte à l’aide d’un contrôleur de mouvement. Maintenez le bouton Windows enfoncé, puis appuyez sur le déclencheur. Cela fonctionne dans les environnements et les applications, mais ne capture pas le contenu protégé par DRM.
* **Nouvelles options pour le lancement et** le redimensionnement de contenu: les applications sont maintenant placées automatiquement devant vous lorsque vous les lancez à partir du menu Démarrer. Vous pouvez également redimensionner les applications 2D en faisant glisser les bords et les angles de la fenêtre.
* **Accédez facilement au contenu à l’aide de la commande vocale «** de téléhébergement». vous pouvez désormais vous téléporter rapidement pour le contenu de la page d’Gazing de la réalité Windows mixed en le content et en disant «téléporter».
* Lanceurs d'  **[applications 3D animés](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#animation-guidelines) et [objets 3D décoratifs](enable-placement-of-3d-models-in-the-home.md) pour la réalité mixte** : vous pouvez maintenant ajouter une animation aux lanceurs d’applications 3D et permettre aux utilisateurs de placer des modèles 3D décoratifs à partir d’une page Web ou d’une application 2D dans la page d’hébergement de la réalité mixte Windows.
* **[Améliorations apportées à Windows Mixed Reality for SteamVR](updating-your-steamvr-application-for-windows-mixed-reality.md)** : Windows Mixed Reality for SteamVR n’est plus un «accès en avant-première» avec les nouvelles mises à niveau, y compris les commentaires haptique lors de l’utilisation de contrôleurs de mouvement, des performances et une fiabilité améliorées, ainsi que des améliorations du apparence des contrôleurs de mouvement dans SteamVR.
* **Autres améliorations** : les paramètres de performance automatique ont été mis à jour pour fournir une expérience plus optimisée (vous pouvez [remplacer manuellement](#visual-quality) ce paramètre). Le programme d’installation fournit maintenant des informations plus détaillées sur les problèmes de compatibilité courants avec les contrôleurs USB 3,0 et les cartes graphiques.

## <a name="new-features-for-hololens"></a>Nouvelles fonctionnalités de HoloLens

La mise à jour 2018 de Windows 10 avril est arrivée pour tous les clients HoloLens. Cette mise à jour est compressée avec des améliorations qui ont été introduites depuis la dernière version majeure du logiciel HoloLens en [août 2016](release-notes-august-2016.md).

### <a name="for-everyone"></a>Pour tout le monde

<table>
  <tr>
    <th>Fonctionnalité</th><th>Détails</th><th>Instructions</th>
  </tr>
  <tr>
    <td>Positionnement automatique du contenu 2D et 3D au lancement</td><td>Un lanceur d’applications 2D ou des applications UWP 2D à des emplacements automatiques dans le monde entier à une taille et une distance optimales lorsqu’ils sont lancés au lieu de demander à l’utilisateur de le placer. Si une <a href="app-views.md">application immersif</a> utilise un lanceur d’application 2D au lieu d’un lanceur d' <a href="3d-app-launcher-design-guidance.md">application 3D</a>, l’application immersif est lancée automatiquement à partir du lanceur d’application 2D comme dans RS1.<br><br>Un lanceur d’applications 3D à partir du menu Démarrer est également placé automatiquement dans le monde entier. Au lieu de lancer automatiquement l’application, les utilisateurs peuvent cliquer sur le lanceur pour lancer l’application immersif. le contenu 3D ouvert à partir de l’application hologrammes et à partir de Edge est également automatiquement placé dans le monde entier.</td><td>Lors de l’ouverture d’une application à partir du menu Démarrer, vous n’êtes plus invité à la placer dans le monde.<br><br>Si le positionnement du lanceur d’application 2D/d’application<a href="3d-app-launcher-design-guidance.md">3D</a> n’est pas optimal, vous pouvez facilement les déplacer à l’aide des manipulations d’application fluide décrites ci-dessous. Vous pouvez également repositionner le lanceur d’applications 2D/contenu 3D en disant «déplacer ce», puis en utilisant le point de vue du regard pour repositionner le contenu.</td>
  </tr>
  <tr>
    <td>Manipulation d’applications fluides</td><td>Déplacer, redimensionner et faire pivoter du contenu 2D et 3D sans avoir à passer en mode «ADJUST».</td><td>Pour déplacer une application UWP 2D ou un lanceur d’application 2D, pointez simplement sur la barre de l’application, puis utilisez le geste TAP + Hold + glisser-déplacer. Vous pouvez déplacer le contenu 3D en Gazing n’importe où sur l’objet, puis en utilisant TAP + Hold + glisser.<br><br>Pour redimensionner le contenu 2D, pointez le regard sur son angle. Le curseur en regard se transforme en curseur de redimensionnement, puis vous pouvez appuyer sur + maintenir + faire glisser pour redimensionner. Vous pouvez également rendre le contenu 2D plus grand ou plus grand en regardant ses bords et en le faisant glisser.<br><br>Pour redimensionner le contenu 3D, soulevez vos mains dans le cadre de mouvement, puis positionnez le curseur en position prête. Vous verrez que le curseur se transforme en un État avec 2 aiguilles de petite mains. Effectuez le mouvement tap and hold avec vos deux mains. En écartant vos mains plus près, vous modifiez la taille de l’objet. Le déplacement des mains vers l’avant et vers l’arrière par rapport à l’autre fait pivoter l’objet. Vous pouvez également redimensionner/faire pivoter le contenu 2D de cette manière.</td>
  </tr>
  <tr>
    <td>Redimensionnement horizontal de l’application 2D avec redistribution</td><td>Rendez une application UWP 2D plus large dans les proportions pour voir plus de contenu d’application. Par exemple, en rendant l’application de messagerie suffisamment grande pour afficher le volet de visualisation.</td><td>Pointez simplement sur le bord gauche ou droit de l’application UWP 2D pour voir le curseur de redimensionnement, puis utilisez le mouvement TAP + Hold + glisser pour le redimensionner.</td>
  </tr>
  <tr>
    <td>Prise en charge des commandes vocales étendue</td><td>Vous pouvez utiliser plus simplement votre voix.</td><td>Essayez ces commandes vocales:<ul><li>«Aller au début»-affiche le menu Démarrer ou ferme une <a href="app-views.md">application immersif</a>.</li><li>«Déplacer ce»-vous permet de déplacer un objet.</li></ul></td>
  </tr>
  <tr>
    <td>Applications d’hologrammes et de photos mises à jour</td><td>Application d’hologrammes mise à jour avec de nouveaux hologrammes. Application photos mise à jour.</td><td>Vous remarquerez une présentation mise à jour des applications hologrammes et photos. L’application hologrammes comprend plusieurs nouveaux hologrammes et un créateur d’étiquette pour faciliter la création de texte.</td>
  </tr>
  <tr>
    <td>Capture de réalité mixte améliorée</td><td>Vidéo de démarrage et de fin de raccourci matériel.</td><td>Maintenez le volume + enfoncé pendant 3 secondes pour démarrer l’enregistrement de la vidéo MRC. Appuyez à nouveau sur ou utilisez le geste de fleur pour terminer.</td>
  </tr>
  <tr>
    <td>Espaces consolidés</td><td>Simplifiez la gestion de l’espace des hologrammes dans un seul espace.</td><td>HoloLens localise automatiquement votre espace et ne vous demande plus de gérer ou de sélectionner des espaces. Si vous rencontrez des problèmes avec des hologrammes vous concernant, vous pouvez accéder aux <b>paramètres > > système hologrammes > supprimer</b>les hologrammes à proximité. Si nécessaire, vous pouvez également sélectionner <b>Supprimer tous les hologrammes</b>.</td>
  </tr>
  <tr>
    <td>Amélioration de l’immersion audio</td><td>Vous pouvez désormais parler à la solution HoloLens mieux dans les environnements bruyants et expérimenter un son plus réaliste à partir des applications, car leur son est masqué par des murs réels détectés par l’appareil.</td><td>Vous n’avez rien à faire pour profiter de l’amélioration du son spatial.</td>
  </tr>
  <tr>
    <td>Explorateur de fichiers</td><td>Déplacer et supprimer des fichiers à partir de HoloLens.</td><td>Vous pouvez utiliser l’application <b>Explorateur de fichiers</b> pour déplacer et supprimer des fichiers à partir de HoloLens.<br><br><b>Conseil :</b> Si vous ne voyez aucun fichier, le filtre «récent» peut être actif (l’icône d’horloge est mise en surbrillance dans le volet gauche). Pour corriger ce problème, sélectionnez l’icône de document de <b>ce périphérique</b> dans le volet gauche (sous l’icône d’horloge) ou ouvrez le menu et sélectionnez <b>cet appareil</b>.
</td>
  </tr>
  <tr>
    <td>Prise en charge du protocole MTP (Media Transfer Protocol)</td><td>Permet à votre ordinateur de bureau d’accéder à vos bibliothèques (photos, vidéos, documents) sur HoloLens pour faciliter le transfert.</td><td>À l’instar des autres appareils mobiles, connectez votre HoloLens à votre PC pour faire en sorte que l' <b>Explorateur de fichiers</b> accède à vos bibliothèques hololens (photos, vidéos, documents) afin de faciliter le transfert.<br><br><b>Conseil</b><ul><li>Si vous ne voyez aucun fichier, vérifiez que vous vous connectez à votre HoloLens pour activer l’accès à vos données.</li><li>Dans l' <b>Explorateur de fichiers</b> de votre PC, vous pouvez sélectionner les propriétés de l' <b>appareil</b> pour afficher le numéro de version du système d’exploitation Windows holographique (version du microprogramme) et le numéro de série de l’appareil.</li></ul><b>Problème connu :</b> L’attribution d’un nouveau nom à HoloLens via l' <b>Explorateur de fichiers</b> sur votre ordinateur n’est pas activée.</td>
  </tr>
  <tr>
    <td>Support réseau du portail captif pendant l’installation</td><td>Vous pouvez maintenant configurer votre HoloLens sur un réseau invité chez les hôtels, les centres de conférence, les magasins de détail ou les entreprises qui utilisent le portail captif.</td><td>Pendant l’installation, sélectionnez le réseau, cochez la case se connecter automatiquement si vous le souhaitez, puis entrez les informations sur le réseau à l’invite.</td>
  </tr>
  <tr>
    <td>Synchronisation des photos et des vidéos via l’application OneDrive</td><td>Vos photos et vidéos de HoloLens vont maintenant se synchroniser par le biais de l’application OneDrive à partir de la Microsoft Store plutôt que directement via l’application photos.</td><td>Pour le configurer, téléchargez et lancez l’application OneDrive à partir du Store. Lors de la première exécution, vous devez être invité à charger automatiquement vos photos sur OneDrive, ou vous pouvez trouver l’option dans les paramètres de l’application.</td>
  </tr>
</table>

### <a name="for-developers"></a>Pour les développeurs

<table>
  <tr>
    <th>Fonctionnalité</th><th>Détails</th><th>Instructions</th>
  </tr>
  <tr>
    <td>Améliorations du mappage spatial</td><td>Amélioration de la qualité, de la simplification et des performances.</td><td>Le maillage de mappage spatial apparaît plus clair: moins de triangles sont nécessaires pour représenter le même niveau de détail. Vous pouvez remarquer des modifications de la densité des triangles dans la scène.</td>
  </tr>
  <tr>
    <td>Sélection automatique du point de focus en fonction du tampon de profondeur</td><td>L’envoi d’un tampon de profondeur à Windows permet à HoloLens de sélectionner automatiquement un point de focus pour optimiser la stabilité de l’hologramme.</td><td>Dans Unity, accédez à <b>modifier > paramètres du projet > lecteur > plateforme Windows universelle > paramètres XR</b>, développez l’élément <b>SDK Windows Mixed Reality</b> et assurez-vous que l’option <b>activer le partage du tampon de profondeur</b> est cochée. Les nouveaux projets seront automatiquement vérifiés.<br><br>Pour les applications DirectX, veillez à appeler la méthode <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.commitdirect3d11depthbuffer">CommitDirect3D11DepthBuffer</a> sur <b>HolographicRenderingParameters</b> chaque frame pour fournir la mémoire tampon de profondeur à Windows.
</td>
  </tr>
  <tr>
    <td>Modes de reprojection holographique</td><td>Vous pouvez maintenant désactiver la reprojection de position sur HoloLens pour améliorer la stabilité de l’hologramme d’un contenu verrouillé de manière rigide, par exemple une vidéo de 360 degrés.</td><td>Dans Unity, définissez <a href="https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.ReprojectionMode.html">HolographicSettings. ReprojectionMode</a> sur <a href="https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.HolographicReprojectionMode.html">HolographicReprojectionMode. OrientationOnly</a> lorsque tout le contenu de la vue est verrouillé de façon rigide.<br><br>Pour les applications DirectX, définissez <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographiccamerarenderingparameters.reprojectionmode">HolographicCameraRenderingParameters. ReprojectionMode</a> sur <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicreprojectionmode">HolographicReprojectionMode. OrientationOnly</a> lorsque tout le contenu de la vue est verrouillé de façon rigide.</td>
  </tr>
  <tr>
    <td>API de personnalisation des applications</td><td>Les API Windows en savent plus sur l’emplacement d’exécution de votre application, par exemple si l’affichage de l’appareil est transparent (HoloLens) ou opaque (casque immersif) et si la vue 2D d’une application UWP s’affiche dans l’interpréteur de commandes holographique.</td><td>L’unité Unity avait auparavant exposé manuellement <a href="https://docs.unity3d.com/ScriptReference/XR.WSA.HolographicSettings.IsDisplayOpaque.html">HolographicSettings. IsDisplayOpaque</a> d’une manière qui fonctionnait avant cette version.<br><br>Pour les applications DirectX, vous pouvez désormais accéder aux API existantes, telles que <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicdisplay.isopaque">HolographicDisplay. GetDefault (). IsOpaque</a> et <a href="https://docs.microsoft.com/uwp/api/windows.applicationmodel.preview.holographic.holographicapplicationpreview.iscurrentviewpresentedonholographicdisplay">HolographicApplicationPreview. IsCurrentViewPresentedOnHolographicDisplay</a> sur HoloLens.
</td>
  </tr>
  <tr>
      <td>Mode de recherche</td><td>Permet aux développeurs d’accéder aux capteurs HoloLens clés lors de la création d’applications académiques et industrielles pour tester de nouvelles idées dans les domaines de la vision et de la robotique des ordinateurs, notamment:<ul><li>Les quatre caméras de suivi de l’environnement</li><li>Deux versions des données de la caméra de mappage de profondeur</li><li>Deux versions d’un flux de réflectivité IR</li></ul></td><td><a href="research-mode.md">Documentation du mode de recherche</a><br><a href="https://github.com/Microsoft/HoloLensForCV">Exemples d’applications en mode de recherche</a></td>
  </tr>
</table>

### <a name="for-commercial-customers"></a>Pour les clients commerciaux

<table>
  <tr>
    <th>Fonctionnalité</th><th>Détails</th><th>Instructions</th>
  </tr>
  <tr>
    <td>Utiliser plusieurs comptes d’utilisateur Azure Active Directory sur un seul appareil</td><td>Partager un HoloLens avec plusieurs utilisateurs Azure AD, chacun avec ses propres paramètres utilisateur et données utilisateur sur l’appareil.</td><td><a href="https://docs.microsoft.com/hololens/hololens-multiple-users">Centre informatique: Partager HoloLens avec plusieurs personnes</a></td>
  </tr>
  <tr>
    <td>Modifier le réseau Wi-Fi lors de la connexion</td><td>Modifier le réseau Wi-Fi avant la connexion pour permettre à un autre utilisateur de se connecter avec son compte d’utilisateur Azure AD pour la première fois, ce qui permet aux utilisateurs de partager des appareils à différents emplacements et sites de travail.</td><td>Dans l’écran de connexion, vous pouvez utiliser l’icône réseau sous le champ mot de passe pour vous connecter à un réseau. Cela est utile quand vous vous connectez pour la première fois à un appareil.</td>
  </tr>
  <tr>
    <td>Inscription unifiée</td><td>Il est désormais facile pour un utilisateur HoloLens qui configure l’appareil d’un compte Microsoft personnel d’ajouter un compte professionnel (Azure AD) et de joindre l’appareil à son serveur MDM.</td><td>Connectez-vous simplement avec un compte Azure AD et l’inscription s’effectue automatiquement.</td>
  </tr>
  <tr>
    <td>Synchronisation de la messagerie sans inscription MDM</td><td>La prise en charge de la synchronisation de la messagerie Exchange Active Sync (EAS) sans nécessiter l’inscription MDM.</td><td>Vous pouvez désormais synchroniser les e-mails sans inscription dans MDM. Vous pouvez configurer l’appareil avec un compte Microsoft, télécharger et installer l’application de messagerie et ajouter un compte de messagerie professionnel directement.</td>
  </tr>
</table>

### <a name="for-it-pros"></a>Pour les professionnels de l'informatique

<table>
  <tr>
    <th>Fonctionnalité</th><th>Détails</th><th>Instructions</th>
  </tr>
  <tr>
    <td>Nouveau nom du système d’exploitation Windows holographique for Business</td><td>Effacez les noms d’édition pour réduire la confusion sur l’application de licence de mise à niveau d’édition lorsque les fonctionnalités de suite commerciales sont activées sur HoloLens.</td><td>Vous pouvez voir quelle édition de Windows holographique se trouve sur votre appareil dans <b>paramètres > système > à propos</b>de. «Windows holographique for Business» s’affiche si une mise à jour d’édition a été appliquée pour activer les fonctionnalités de la suite commerciale. Découvrez comment <a href="https://docs.microsoft.com/hololens/hololens-upgrade-enterprise">déverrouiller les fonctionnalités Windows holographique for Business</a>.</td>
  </tr>
  <tr>
  <td>Concepteur de configuration Windows (WCD)</td><td>Créez et modifiez des packages d’approvisionnement pour configurer HoloLens via l’application mise à jour WCD. Assistant HoloLens simple pour la mise à jour d’édition, OOBE configurable, région/fuseau horaire, jeton de Azure AD en bloc, réseau et CSP développeur. Éditeur avancé filtré avec les options prises en charge par HoloLens, y compris les fournisseurs de services de chiffrement d’accès et de gestion des comptes affectés.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning">Centre informatique: Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
    <td>Configuration configurable (OOBE)</td><td>Masquer les écrans d’étalonnage, de mouvement de regard et de configuration Wi-Fi lors de l’installation.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning#create-a-provisioning-package-for-hololens-using-the-hololens-wizard">Centre informatique: Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
    <td>Prise en charge des jetons en bloc Azure AD</td><td>Pré-inscrire l’appareil sur Azure AD locataire d’annuaire pour un workflow d’installation utilisateur plus rapide.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning">Centre informatique: Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
  <td>Fournisseur de services de configuration DeveloperSetup</td><td>Déployez le profil pour configurer HoloLens en mode développeur. Utile pour les appareils de développement et de démonstration.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning">Centre informatique: Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
  <td>Fournisseur de services de configuration AccountManagement</td><td>Partager un appareil HoloLens et supprimer les données utilisateur après la déconnexion ou les seuils d’inactivité/stockage pour une utilisation temporaire. Prend en charge les comptes de Azure AD.</td><td><a href="https://docs.microsoft.com/hololens/hololens-provisioning">Centre informatique: Configurer HoloLens à l’aide d’un package d’approvisionnement</a></td>
  </tr>
  <tr>
  <td>Accès affecté</td><td>Windows a accès aux télétravailleurs ou aux démonstrations en première ligne. Verrouillage à une ou plusieurs applications. Vous n’avez pas besoin de déverrouiller les développeurs.</td><td><a href="https://docs.microsoft.com/hololens/hololens-kiosk">Centre informatique: Configurer HoloLens en mode plein écran</a></td>
  </tr>
  <tr>
  <td>Accès invité pour les appareils kiosque</td><td>Accès accordé à Windows avec un compte invité sans mot de passe pour les démonstrations. Verrouillage à une ou plusieurs applications. Vous n’avez pas besoin de déverrouiller les développeurs.</td><td><a href="https://docs.microsoft.com/hololens/hololens-kiosk#guest">Centre informatique: Configurer HoloLens en mode plein écran</a></td>
  </tr>
  <tr>
    <td>Configurer les Diagnostics (OOBE)</td><td>Obtenir les journaux de diagnostic à partir de HoloLens afin de pouvoir résoudre les échecs de connexion Azure AD (avant que le hub de commentaires soit disponible pour l’utilisateur dont la connexion a échoué).</td><td>En cas d’échec de l’installation ou de la connexion, choisissez l’option <b>collecter les informations</b> pour obtenir les journaux de diagnostic à des fins de dépannage.</td>
  </tr>
  <tr>
    <td>Expiration du mot de passe indéfiniment du compte local</td><td>Supprimer l’interruption de la réinitialisation de l’appareil lorsque le mot de passe du compte local expire.</td><td>Lors de l’approvisionnement d’un compte local, vous n’avez plus besoin de modifier le mot de passe tous les 42 jours dans les <b>paramètres</b>, car le mot de passe du compte n’expire plus.</td>
  </tr>
  <tr>
    <td>État et détails de la synchronisation MDM</td><td>Fonctionnalités Windows standard pour comprendre l’État et les détails de la synchronisation MDM à partir de HoloLens.</td><td>Vous pouvez vérifier l’état de synchronisation MDM d’un appareil dans <b>paramètres > des comptes > accéder aux informations de > professionnelles ou scolaires</b>. Dans la <b>section état<b> de la synchronisation des appareils, vous pouvez démarrer une synchronisation, voir zones gérées par MDM et créer et exporter un rapport de diagnostics avancés.</td>
  </tr>
</table>

## <a name="known-issues"></a>Problèmes connus

Nous avons travaillé dur pour offrir une expérience Windows Mixed Reality exceptionnelle, mais nous effectuons toujours le suivi de certains problèmes connus. Si vous en trouvez d’autres, faites [-nous part de vos commentaires](give-us-feedback.md).

### <a name="hololens"></a>HoloLens

#### <a name="after-update"></a>Après la mise à jour

Vous pouvez remarquer les problèmes suivants après la mise à jour de RS1 vers RS4 sur votre HoloLens:
* Réinitialisation des **codes confidentiels** : les applications 3x3 épinglées à votre menu Démarrer seront réinitialisées aux valeurs par défaut après la mise à jour. 
* Réinitialisation des **applications et** des hologrammes: les applications placées dans votre monde seront supprimées après la mise à jour et devront être replacées dans votre espace. 
* Il **se peut que le hub de commentaires ne démarre pas immédiatement** . immédiatement après la mise à jour, la mise à jour prend quelques minutes avant que vous ne puissiez lancer certaines applications de boîte de réception, comme le hub de commentaires, pendant qu’elles sont mises à jour. 
* Les **certificats Wi-Fi d’entreprise doivent être** resynchronisés-nous étudions un problème qui nécessite que le HoloLens soit connecté à un autre réseau pour que les certificats d’entreprise soient resynchronisés sur l’appareil avant de pouvoir se reconnecter à l’entreprise. réseaux utilisant des certificats. 
* **H. 265 HEVC la lecture vidéo ne fonctionne pas** : les applications qui essaient de lire les vidéos H. 265 reçoivent un message d’erreur. La solution de contournement consiste à [accéder au portail des appareils Windows](using-the-windows-device-portal.md), à sélectionner des **applications** dans la barre de navigation de gauche et à **supprimer** l’application HEVC. Ensuite, installez la dernière [extension vidéo HEVC](https://www.microsoft.com/p/hevc-video-extensions/9nmzlz57r3t7) à partir de la Microsoft Store. Nous étudions le problème. 

#### <a name="for-developers-updating-hololens-apps-for-devices-running-windows-10-april-2018-update"></a>Pour les développeurs: mise à jour des applications HoloLens pour les appareils exécutant Windows 10 avril 2018 Update

Avec la liste des [nouvelles fonctionnalités](#new-features-for-hololens), la mise à jour 2018 d’avril de Windows 10 (RS4) pour HoloLens applique certains comportements de code que les versions précédentes n’ont pas:
* **Demandes d’autorisation pour utiliser des ressources sensibles (caméra, microphone, etc.)** -RS4 sur HoloLens appliquera des demandes d’autorisation pour les applications qui accèdent à des ressources sensibles, telles que l’appareil photo ou le microphone. RS1 sur HoloLens n’a pas forcé ces invites. par conséquent, si votre application suppose un accès immédiat à ces ressources, elle peut se bloquer dans RS4 (même si l’utilisateur accorde l’autorisation à la ressource demandée). Pour plus d’informations, consultez l' [article déclarations des fonctionnalités d’application UWP](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations) appropriées.
* Les **appels à des applications en dehors de votre propre** RS4 sur HoloLens garantissent l’utilisation correcte de la [classe *Windows. System. Launcher* ](https://docs.microsoft.com/uwp/api/Windows.System.Launcher) pour lancer une autre application à partir de votre propre application. Par exemple, nous avons rencontré des problèmes avec les applications qui appellent *Windows. System. Launcher. LaunchUriForResultsAsync* à partir d’un thread non-asta (IU). Cela réussit dans RS1 sur HoloLens, mais RS4 requiert l’exécution de l’appel sur le thread d’interface utilisateur.

### <a name="windows-mixed-reality-on-desktop"></a>Windows Mixed Reality sur le Bureau

#### <a name="visual-quality"></a>Qualité visuelle

* Si vous remarquez après la mise à jour 2018 de Windows 10 avril que les graphiques sont plus flous qu’auparavant, ou que le champ de la vue est plus petit sur votre casque, le paramètre de performance automatique peut avoir été modifié afin de conserver une fréquence d’images suffisante sur un processeur moins puissant. carte graphique (par exemple, NVIDIA 1050). Vous pouvez remplacer cette valeur manuellement (si vous le souhaitez) en accédant à **paramètres > réalité mixte > affichage du casque > Options d’expérience > modifier** et en remplaçant «automatique» par «90 Hz». Vous pouvez également essayer de changer la **qualité visuelle** (sur la même page de paramètres) en «haute».

#### <a name="windows-mixed-reality-setup"></a>Programme d’installation de Windows Mixed Reality

* Quand vous configurez Windows avec un casque connecté, votre moniteur PC peut rester vide. Débranchez votre casque pour activer la sortie sur votre moniteur d’ordinateur pour terminer l’installation de Windows.
* Si vous n’avez pas de casque connecté, vous risquez de manquer des conseils supplémentaires lorsque vous visitez pour la première fois la page d’hébergement Windows Mixed Reality.
* D’autres périphériques Bluetooth peuvent entraîner des interférences avec les contrôleurs de mouvement. Si les contrôleurs de mouvement présentent des problèmes de connexion/appariement/suivi, assurez-vous que la radio Bluetooth (si une clé externe) est connectée à un emplacement non obstrué et qu’elle ne se trouve pas immédiatement à côté d’une autre clé Bluetooth. Essayez également de mettre hors tension d’autres périphériques Bluetooth pendant les sessions Windows Mixed Reality pour voir s’il est utile.

#### <a name="games-and-apps-from-the-microsoft-store"></a>Jeux et applications à partir du Microsoft Store

* Certains jeux graphiques intensifs, comme Forza Motorsport 7, peuvent entraîner des problèmes de performances sur les PC moins aptes lorsqu’ils sont lus dans Windows Mixed Reality.

#### <a name="audio"></a>Audio

* Si vous avez activé Cortana sur votre ordinateur hôte avant d’utiliser votre casque Windows Mixed Reality, vous risquez de perdre la simulation de son spatial appliquée aux applications que vous placez dans la page d’accueil de Windows Mixed Reality. 
   * La solution consiste à activer «Windows Sonic pour casque» sur tous les périphériques audio connectés à votre PC, y compris votre périphérique audio connecté à un casque:
      1. Cliquez avec le bouton gauche sur l’icône de haut-parleur dans la barre des tâches du bureau, puis sélectionnez dans la liste des périphériques audio.
      2. Cliquez avec le bouton droit sur l’icône de haut-parleur dans la barre des tâches du bureau, puis sélectionnez «Windows Sonic pour casque» dans le menu «Configuration des conférenciers».
      3. Répétez ces étapes pour tous vos périphériques audio (points de terminaison).
   * Une autre option consiste à désactiver «laisser Cortana répondre à Hey Cortana» dans **paramètres** > **Cortana** sur votre bureau avant de lancer Windows Mixed Reality.
* Lorsqu’un autre périphérique USB multimédia (par exemple, une webcam) partage le même concentrateur USB (externe ou à l’intérieur de votre ordinateur) avec le casque Windows Mixed Reality, dans de rares cas, le casque audio/casque peut avoir un signal sonore ou aucun son. Vous pouvez résoudre ce problème en utilisant votre casque sur un port USB qui ne partage pas le même concentrateur que l’autre, ou déconnecter/désactiver votre autre périphérique multimédia USB.
* Dans de très rares cas, le concentrateur USB de l’ordinateur hôte ne peut pas fournir suffisamment de puissance au casque Windows Mixed Reality. vous pouvez remarquer une rafale de bruit du casque connecté au casque.

#### <a name="holograms"></a>Hologrammes

* Si vous avez placé un grand nombre d’hologrammes dans votre foyer Windows Mixed Reality, certains peuvent disparaître et apparaître à l’impression. Pour éviter cela, supprimez certains des hologrammes dans cette zone de la famille Windows Mixed Reality.

#### <a name="motion-controllers"></a>Contrôleurs de mouvement

* Si l’entrée n’est pas acheminée vers le casque, le contrôleur de mouvement disparaît brièvement quand il est maintenu en regard de la limite de la salle. En appuyant sur Win + Y pour vous assurer qu’une bannière bleue s’affiche sur l’écran de l’ordinateur de bureau, vous pouvez résoudre ce cas. 
* Parfois, lorsque vous cliquez sur une page Web dans Microsoft Edge, le contenu est zoom au lieu de cliquer.

#### <a name="desktop-app-in-the-windows-mixed-reality-home"></a>Application de bureau dans la page d’hébergement Windows Mixed Reality

* L’outil capture ne fonctionne pas dans l’application de bureau.
* L’application de bureau n’est pas définie lors du redémarrage.
* Si vous utilisez la préversion du portail de réalité mixte sur votre bureau, lorsque vous ouvrez l’application de bureau dans la page d’accueil de Windows Mixed Reality, vous remarquerez peut-être l’effet de miroir infini. 
* L’exécution de l’application de bureau peut entraîner des problèmes de performances sur les PC non-ultra-Windows Mixed Reality. Cela n’est pas recommandé.  
* L’application de bureau peut être lancée automatiquement, car une fenêtre invisible sur le Bureau a le focus. 
* L’invite du contrôle de compte d’utilisateur du Bureau fera apparaître le casque en noir jusqu’à ce que l’invite soit terminée.

#### <a name="windows-mixed-reality-for-steamvr"></a>Windows Mixed Reality pour SteamVR

* Vous devrez peut-être lancer le portail de réalité mixte après la mise à jour pour vous assurer que les mises à jour logicielles nécessaires pour la mise à jour 2018 de Windows 10 avril sont terminées avant de lancer SteamVR. 
* Vous devez être sur une version récente de Windows Mixed Reality pour que SteamVR reste compatible avec la mise à jour 2018 de Windows 10 avril. Assurez-vous que les mises à jour automatiques sont activées pour Windows Mixed Reality pour SteamVR, qui se trouve dans la section «logiciel» de votre bibliothèque dans la vapeur.  

#### <a name="other-issues"></a>Autres problèmes

>[!IMPORTANT]
>Une version antérieure de la mise à jour 2018 du mois d’avril de Windows 10 a été envoyée aux initiateurs (version 17134,5), il manque un logiciel nécessaire à l’exécution de Windows Mixed Reality. Nous vous recommandons d’éviter cette version si vous utilisez Windows Mixed Reality. 

Nous avons identifié une régression des performances lors de l’utilisation de surface Book 2 sur la version initiale de cette mise à jour (10.0.17134.1) que nous travaillons à résoudre dans un correctif de mise à jour à venir. Nous vous suggérons de patienter jusqu’à ce que ce problème soit résolu avant la mise à jour manuelle ou l’attente du déploiement normal de la mise à jour.

## <a name="provide-feedback-and-report-issues"></a>Fournir des commentaires et signaler des problèmes

Utilisez l' [application Hub de commentaires sur votre PC HoloLens ou Windows 10](give-us-feedback.md) pour fournir des commentaires et signaler des problèmes. L’utilisation de feedback Hub garantit que toutes les informations de diagnostic nécessaires sont incluses pour aider nos ingénieurs à déboguer et résoudre rapidement le problème.

>[!NOTE]
>Veillez à accepter l’invite qui vous demande si vous souhaitez que le hub de commentaires accède à votre dossier documents (sélectionnez **Oui** lorsque vous y êtes invité).

## <a name="prior-release-notes"></a>Notes de publication antérieures

* [Notes de publication - Octobre 2017](release-notes-october-2017.md)
* [Notes de publication - Août 2016](release-notes-august-2016.md)
* [Notes de publication - Mai 2016](release-notes-may-2016.md)
* [Notes de publication - Mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Prise en charge des casques immersifs (lien externe)](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality)
* [Prise en charge de HoloLens (lien externe)](https://support.microsoft.com/products/hololens)
* [Installer les outils](install-the-tools.md)
* [Nous envoyer vos commentaires](give-us-feedback.md)

