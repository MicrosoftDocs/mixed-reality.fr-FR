---
title: Utilisation du portail d’appareils Windows
description: Le portail d’appareils Windows pour HoloLens vous permet de configurer et de gérer votre appareil à distance via Wi-Fi ou USB. Le Device Portal est un serveur Web situé sur l'appareil auquel vous pouvez vous connecter depuis un navigateur Web sur votre PC. Le portail des appareils comprend de nombreux outils qui vous aideront à gérer votre HoloLens et à déboguer et optimiser vos applications.
author: JonMLyons
ms.author: jlyons
ms.date: 02/24/2019
ms.topic: article
keywords: Portail des appareils Windows, HoloLens
ms.openlocfilehash: 5a2440c07ade1a9c41f3c28c332748e0c97cd3ed
ms.sourcegitcommit: e5b677f92ac4b1dff9aad6c329345a5aca4fcef5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020229"
---
# <a name="using-the-windows-device-portal"></a>Utilisation du portail d’appareils Windows

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1ère génération)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> Windows Device Portal</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

Le portail d’appareils Windows pour HoloLens vous permet de configurer et de gérer votre appareil à distance via Wi-Fi ou USB. Le Device Portal est un serveur Web situé sur l'appareil auquel vous pouvez vous connecter depuis un navigateur Web sur votre PC. Le portail des appareils comprend de nombreux outils qui vous aideront à gérer votre HoloLens et à déboguer et optimiser vos applications.

Cette documentation concerne spécifiquement le portail de périphériques Windows pour HoloLens. Pour utiliser le portail d’appareils Windows pour les ordinateurs de bureau (y compris pour Windows Mixed Reality), consultez [vue d’ensemble du portail de périphériques Windows](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal)

## <a name="setting-up-hololens-to-use-windows-device-portal"></a>Configuration de HoloLens pour utiliser le portail d’appareils Windows

1. Mettez HoloLens sous tension et allumez l’appareil.
2. Effectuer le geste qui consiste à [maintenir sa paume de main vers le haut en serrant ses doigts et à les ouvrir](gestures.md#bloom) pour lancer le menu principal.
3. Pointez avec le regard de la vignette **paramètres** et effectuez le mouvement d' [appui sur l’air](gestures.md#air-tap) . Effectuez un second appui sur l’air pour placer l’application dans votre environnement. L’application Paramètres démarre une fois placée.
4. Sélectionnez l’élément de menu **Mettre à jour**.
5. Sélectionnez l’élément de menu **Pour les développeurs**.
6. Activez **Mode développeur**.
7. [Faites](gestures.md#composite-gestures) défiler l’appareil et activez le **portail des appareils**.
8. Si vous configurez le portail de périphériques Windows afin de pouvoir déployer des applications sur ce réseau HoloLens sur USB ou Wi-Fi, cliquez sur **couple** pour [générer un code PIN de jumelage](using-visual-studio.md). Laissez l’application paramètres dans le menu contextuel du code confidentiel jusqu’à ce que vous entriez le code confidentiel dans Visual Studio lors de votre premier déploiement.

   ![Activation du mode développeur dans l’application paramètres pour Windows holographique](images/deviceportalsettings.png)

## <a name="connecting-over-wi-fi"></a>Connexion via Wi-Fi

1. [Connectez votre HoloLens à Wi-Fi](connecting-to-wi-fi-on-hololens.md).
2. Recherchez l’adresse IP de votre appareil.
   * Recherchez l’adresse IP sur l’appareil sous **paramètres > réseau & Internet > Wi-Fi > options avancées**.
3. À partir d’un navigateur Web sur votre PC, accédez à https://< YOUR_HOLOLENS_IP_ADDRESS >
   * Le navigateur affiche le message suivant: «Il y a un problème avec le certificat de sécurité de ce site Web». Cela se produit car le certificat envoyé à Device Portal est un certificat de test. Vous pouvez ignorer cette erreur de certificat pour le moment et continuer.

## <a name="connecting-over-usb"></a>Connexion via USB

1. [Installez les outils](install-the-tools.md) pour vérifier que vous disposez de Visual Studio Update 1 avec les outils de développement Windows 10 installés sur votre PC. Cela permet d’activer la connectivité USB.
2. Connectez votre HoloLens au PC à l’aide d’un câble micro-USB.
3. À partir d’un navigateur Web sur votre PC, [http://127.0.0.1:10080](http://127.0.0.1:10080)accédez à.

## <a name="connecting-to-an-emulator"></a>Connexion à un émulateur

Vous pouvez également utiliser Device Portal avec votre émulateur. Pour vous connecter au portail de l’appareil, utilisez la [barre d’outils](using-the-hololens-emulator.md). Cliquez sur cette icône : ![Icône](images/emulator-deviceportal.png) ouvrir le portail de l’appareil **ouvrir le portail**de l’appareil: ouvre le Portail d’appareil Windows pour le système d’exploitation HoloLens dans l’émulateur.

## <a name="creating-a-username-and-password"></a>Création d’un nom d’utilisateur et d’un mot de passe

![Configurer l’accès au portail des appareils Windows](images/windows-device-portal-credentials-reset-page-1000px.png)<br>
*Configurer l’accès au portail des appareils Windows*

Vous devrez créer un nom d’utilisateur et un mot de passe sur Device Portal de votre HoloLens lors de votre première connexion.
1. Dans un navigateur web sur votre PC, entrez l’adresse IP de l’HoloLens. La page d’accès à la configuration s’affiche.
2. Cliquez ou appuyez sur **demander un code PIN** , puis examinez l’affichage HoloLens pour obtenir le code confidentiel généré.
3. Entrez le code confidentiel dans le **code confidentiel affiché** dans la zone de texte de votre appareil.
4. Entrez le nom d’utilisateur que vous utiliserez pour vous connecter à Device Portal. Il n’est pas nécessaire qu’il s’agisse d’un nom de compte Microsoft (MSA) ou de domaine.
5. Entrez un mot de passe et confirmez-le. Le mot de passe doit comporter au moins sept caractères. Il n’est pas nécessaire qu’il s’agisse d’un mot de passe de compte Microsoft (MSA) ou de domaine.
6. Cliquez sur **paire** pour vous connecter au portail des appareils Windows sur le HoloLens.

Si vous souhaitez modifier ce nom d’utilisateur ou mot de passe à tout moment, vous pouvez répéter ce processus en visitant la page sécurité de l’appareil en accédant à: https://< YOUR_HOLOLENS_IP_ADDRESS >/devicepair.htm.

## <a name="security-certificate"></a>Certificat de sécurité

Si une « erreur de certificat » s’affiche dans votre navigateur, vous pouvez la résoudre en créant une relation d’approbation avec l’appareil.

Chaque HoloLens génère un certificat auto-signé unique pour sa connexion SSL. Par défaut, ce certificat n’est pas approuvé par le navigateur web de votre PC, c’est la raison pour laquelle vous obtiendrez peut-être une « erreur de certificat ». En téléchargeant ce certificat à partir de votre HoloLens (via une connexion USB ou Wi-Fi approuvée) et en l’approuvant sur votre PC, vous pouvez vous connecter en toute sécurité à votre appareil.
1. **Assurez-vous que vous êtes sur un réseau sécurisé (USB ou un réseau Wi-Fi auquel vous faites confiance).**
2. Téléchargez le certificat de cet appareil à partir de la page «sécurité» sur le portail de l’appareil.
   * Accédez à: https://< YOUR_HOLOLENS_IP_ADDRESS >/devicepair.htm
3. Installez le certificat dans le magasin «autorités de certification racines de confiance» sur votre PC.
   * Dans le menu Windows, tapez: Gérer les certificats d’ordinateur et démarrer l’applet.
   * Développez le dossier **autorité de certification racine de confiance** .
   * Cliquez sur le dossier **certificats** .
   * Dans le menu Action, sélectionnez: Toutes les tâches > Importer...
   * Terminez l’Assistant Importation de certificat en utilisant le fichier de certificat que vous avez téléchargé à partir de Device Portal.
4. Redémarrez le navigateur.

## <a name="device-portal-pages"></a>Pages de Device Portal

### <a name="home"></a>Dossier de base

![Page d’hébergement du portail des appareils Windows sur Microsoft HoloLens](images/windows-device-portal-home-page-1000px.png)<br>
*Page d’hébergement du portail des appareils Windows sur Microsoft HoloLens*

Votre session Device Portal démarre sur la page d’accueil. Accédez à d’autres pages à partir de la barre de navigation située sur le côté gauche de la page d’accueil.

La barre d’outils se trouvant en haut de la page permet d’accéder aux fonctionnalités et aux états couramment utilisés.
* **En ligne**: Indique si l’appareil est connecté au réseau Wi-Fi.
* **Arrêt**: Désactive l’appareil.
* **Redémarrage**: Recycle l’alimentation de l’appareil.
* **Sécurité** : Ouvre la page sécurité de l’appareil.
* **Cool**: Indique la température de l’appareil.
* **A/C**: Indique si l’appareil est branché et en cours de chargement.
* **Aide**: Ouvre la page de documentation de l’interface REST.

La page d’accueil affiche les informations suivantes :
* **État du périphérique:** analyse l’intégrité de votre appareil et signale les erreurs critiques.
* **Informations Windows:** affiche le nom du HoloLens et la version de Windows actuellement installée.
* La section **Préférences** comprend les paramètres suivants :
   * **IPD**: Définit la distance interpupillary (IPD), qui est la distance, en millimètres, entre le Centre des élèves de l’utilisateur lors de la recherche directe. Le paramètre prend immédiatement effet. La valeur par défaut a été calculée automatiquement lors de la configuration de votre appareil.
   * **Nom**de l’appareil: Assignez un nom à HoloLens. Vous devez redémarrer l’appareil après avoir modifié cette valeur afin qu’elle soit prise en compte. Après avoir cliqué sur **Enregistrer**, une boîte de dialogue vous demande si vous souhaitez redémarrer l’appareil immédiatement ou redémarrer ultérieurement.
   * **Paramètres de veille**: Définit la durée d’attente avant que l’appareil ne se met en veille lorsqu’il est branché et lorsqu’il est sur batterie.

### <a name="3d-view"></a>Vue 3D

![page vue 3D dans le portail d’appareils Windows sur Microsoft HoloLens](images/3dview-1000px.png)<br>
*page vue 3D dans le portail d’appareils Windows sur Microsoft HoloLens*

Utilisez la page Vue 3D pour voir comment HoloLens interprète votre environnement. Naviguez dans la vue à l’aide de la souris :
* Pivoter: clic gauche + souris;
* Panoramique: clic droit + souris;
* Zoom: défilement de la souris.
* **Options de suivi**
   * Activez le suivi visuel continu en activant la case à cocher **forcer le suivi visuel**. 
   * **Suspendre** arrête le suivi visuel.
* **Options d’affichage**: Définissez les options de la vue 3D:
  * **Suivi**: Indique si le suivi visuel est actif.
  * **Afficher le plancher**: Affiche un plan d’étage à damier.
  * **Afficher frustum**: Affiche la vue frustum.
  * **Afficher le plan de stabilisation**: Affiche le plan utilisé par HoloLens pour stabiliser le mouvement.
  * **Afficher le maillage**: Affiche le maillage de mappage spatial qui représente votre environnement.
  * **Afficher**les ancres spatiales: Affiche les ancres spatiales de l’application active. Vous devez cliquer sur le bouton mettre à jour pour récupérer et actualiser les ancres.
  * **Afficher les détails**: Affiche les positions des handles, les quaternions de rotation de la tête et le vecteur d’origine de l’appareil lorsqu’ils évoluent en temps réel.
  * **Bouton plein écran**: Affiche la vue 3D en mode plein écran. Appuyez sur la touche ÉCHAP pour quitter le mode plein écran.
* **Reconstruction de surface**: Cliquez ou appuyez sur **mettre à jour** pour afficher le maillage de mappage spatial le plus récent à partir de l’appareil. Un passage complet peut nécessiter un certain temps, pouvant aller jusqu’à quelques secondes. La maille ne se met pas à jour automatiquement dans la vue 3D et vous devez cliquer sur **mettre à jour** manuellement pour obtenir le maillage le plus récent de l’appareil. Cliquez sur **Enregistrer** pour enregistrer le maillage de mappage spatial actuel sous la forme d’un fichier OBJ sur votre PC.
* **Ancres spatiales**: Cliquez sur mettre à jour pour afficher ou mettre à jour les ancres spatiales de l’application active.

### <a name="mixed-reality-capture"></a>MRC (Mixed Reality Capture)

![Page capture de la réalité mixte dans le portail de périphériques Windows sur Microsoft HoloLens](images/windows-device-portal-mixed-reality-capture-page-1000px.png)<br>
*Page capture de la réalité mixte dans le portail de périphériques Windows sur Microsoft HoloLens*

Utilisez la page MRC pour enregistrer les flux multimédias issus du casque HoloLens.
* **Paramètres**: Contrôlez les flux de médias capturés en vérifiant les paramètres suivants:
  * **Hologrammes**: Capture le contenu holographique dans le flux vidéo. Les hologrammes font l’objet d’un rendu en mono et non en stéréo.
  * **Appareil photo PV**: Capture le flux vidéo à partir de la caméra photo/vidéo.
  * **Audio MIC**: Capture l’audio à partir du tableau du microphone.
  * **Audio**de l’application: Capture l’audio de l’application en cours d’exécution.
  * **Rendre à partir de l’appareil photo**: Aligne la capture à partir du point de vue de la caméra photo/vidéo, si elle est [prise en charge par l’application en cours d’exécution](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in) (HoloLens 2 uniquement).
  * **Qualité de l’aperçu instantané**: Sélectionnez la résolution d’écran, la fréquence d’images et la vitesse de diffusion en continu pour l’aperçu instantané.
* Cliquez ou appuyez sur le bouton **aperçu instantané** pour afficher le flux de capture. **Arrêter l’aperçu instantané** arrête le flux de capture.
* Cliquez ou appuyez sur **enregistrement** pour commencer l’enregistrement du flux de réalité mixte, à l’aide des paramètres spécifiés. **Arrêter l’enregistrement** met fin à l’enregistrement et l’enregistre.
* Cliquez ou appuyez sur **prendre une photo** pour prendre une image continue du flux de capture.
* **Vidéos et photos**: Affiche la liste des captures vidéo et photo effectuées sur l’appareil.

> [!NOTE]
> Il existe des [limitations à la MRC simultanée](mixed-reality-capture-for-developers.md#simultaneous-mrc-limitations):
> * Si une application tente d’accéder à la caméra photo/vidéo alors que le portail de périphériques Windows enregistre une vidéo, l’enregistrement vidéo s’arrête.
>   * HoloLens 2 n’arrête pas l’enregistrement de la vidéo si l’application crée une ACE avec le mode SharedReadOnly.
> * Si une application utilise activement la caméra photo/vidéo, le portail d’appareils Windows peut prendre une photo ou enregistrer une vidéo.
> * Streaming en direct:
>   * HoloLens (1re génération) empêche une application d’accéder à la caméra photo/vidéo pendant la diffusion en direct à partir du portail de périphériques Windows.
>   * HoloLens (1ère génération) échouera à la diffusion en continu si une application utilise activement la caméra photo/vidéo.
>   * HoloLens 2 arrête automatiquement la diffusion en continu en direct quand une application tente d’accéder à la caméra photo/vidéo en mode ExclusiveControl.
>   * HoloLens 2 est en mesure de démarrer un flux Live quand une application utilise activement l’appareil photo PV.

### <a name="performance-tracing"></a>Suivi des performances

![Page suivi des performances dans le portail de périphériques Windows sur Microsoft HoloLens](images/windows-device-portal-performance-tracing-page-1000px.png)<br>
*Page suivi des performances dans le portail de périphériques Windows sur Microsoft HoloLens*

Capturer les traces de l' [enregistreur de performances Windows](https://msdn.microsoft.com/library/windows/hardware/hh448205.aspx) (WPR) à partir de votre HoloLens.
* **Profils disponibles**: Sélectionnez le profil WPR dans la liste déroulante, puis cliquez ou appuyez sur **Démarrer** pour démarrer le suivi.
* **Profils personnalisés**: Cliquez ou appuyez sur **Parcourir** pour choisir un profil WPR sur votre PC. Cliquez ou appuyez sur **Charger et démarrer** pour commencer le suivi.

Pour arrêter la trace, cliquez sur le lien arrêter. Restez sur cette page tant que le téléchargement du fichier de trace n’est pas terminé.

Les fichiers ETL capturés peuvent être ouverts pour analyse dans [Windows Performance Analyzer](https://msdn.microsoft.com/library/windows/hardware/hh448170.aspx).

### <a name="processes"></a>Processus

![Page processus dans le portail de périphériques Windows sur Microsoft HoloLens](images/windows-device-portal-running-processes-page-1000px.png)<br>
*Page processus dans le portail de périphériques Windows sur Microsoft HoloLens*

Affiche les détails concernant les processus en cours d’exécution. Cela comprend les processus relatifs aux applications au système.

### <a name="system-performance"></a>Performances du système

![Page performances du système dans le portail de périphériques Windows sur Microsoft HoloLens](images/windows-device-portal-system-performance-page-1000px.png)<br>
*Page performances du système dans le portail de périphériques Windows sur Microsoft HoloLens*

Présente des graphiques en temps réel des informations de diagnostic système, telles que la consommation d’énergie, la fréquence d’images et la charge du processeur.

Voici les mesures disponibles :
* **Alimentation SOC**: Utilisation instantanée de l’alimentation système sur puce, moyenne sur une minute
* **Puissance du système**: Utilisation de l’alimentation du système instantanée, moyenne d’une minute
* **Fréquence d’images**: Frames par seconde, VBlanks manqués par seconde et VBlanks manqués consécutifs
* **GPU**: Utilisation du moteur GPU, pourcentage du total disponible
* **UC**: pourcentage du total disponible
* **E/S**: Lectures et écritures
* **Réseau** : Reçu et envoyé
* **Mémoire**: Total, en cours d’utilisation, validé, paginé et non paginé

### <a name="apps"></a>Applications

![Page applications dans le portail de périphériques Windows sur Microsoft HoloLens](images/windows-device-portal-apps-page-1000px.png)<br>
*Page applications dans le portail de périphériques Windows sur Microsoft HoloLens*

Gère les applications qui sont installées sur HoloLens.
* **Applications installées**: Supprimer et démarrer des applications.
* **Applications en cours d’exécution**: Répertorie les applications qui s’exécutent actuellement.
* **Installer l’application**: Sélectionnez packages d’application pour l’installation à partir d’un dossier sur votre ordinateur/réseau.
* **Dépendance**: Ajoutez des dépendances pour l’application que vous allez installer.
* **Déployer**: Déployez l’application et les dépendances sélectionnées dans le HoloLens.

### <a name="app-crash-dumps"></a>Vidages sur incident d’application

![Page vidages sur incident de l’application dans le portail de périphériques Windows sur Microsoft HoloLens](images/windows-device-portal-dev-apps-crash-dumps-page-1000px.png)<br>
*Page vidages sur incident de l’application dans le portail de périphériques Windows sur Microsoft HoloLens*

Cette page vous permet de recueillir les vidages sur incident de vos applications chargées de manière indépendante. Activez la case à cocher vidages sur **incident activés** pour chaque application pour laquelle vous souhaitez collecter des vidages sur incident. Revenez à cette page pour recueillir les vidages sur incident. Les fichiers dump peuvent être [ouverts dans Visual Studio pour](https://msdn.microsoft.com/library/d5zhxt22.aspx)le débogage.

### <a name="file-explorer"></a>Explorateur de fichiers

![Page Explorateur de fichiers dans le portail de périphériques Windows sur Microsoft HoloLens](images/fileexplorer-1000px.png)<br>
*Page Explorateur de fichiers dans le portail de périphériques Windows sur Microsoft HoloLens*

Utilisez l’Explorateur de fichiers pour parcourir, télécharger et télécharger des fichiers. Vous pouvez utiliser des fichiers dans le dossier documents, le dossier images et dans les dossiers de stockage locaux pour les applications que vous avez déployées à partir de Visual Studio ou du portail de l’appareil.

### <a name="kiosk-mode"></a>Mode plein écran

>[!NOTE]
>Le mode plein écran est disponible uniquement avec [Microsoft HoloLens commercial suite](commercial-features.md).

Pour obtenir des instructions à jour sur l’activation du mode plein écran via le portail des appareils Windows, consultez l’article [configurer HoloLens en mode plein écran](https://docs.microsoft.com/hololens/hololens-kiosk#set-up-kiosk-mode-using-the-windows-device-portal-windows-10-version-1607-and-version-1803) dans le Centre Windows IT Pro.

### <a name="logging"></a>Journalisation

![Page journalisation dans le portail de périphériques Windows sur Microsoft HoloLens](images/windows-device-portal-logging-page-1000px.png)<br>
*Page journalisation dans le portail de périphériques Windows sur Microsoft HoloLens*

Gère les Suivi d’v nements pour Windowss en temps réel (ETW) sur le HoloLens.

Cochez **Masquer les fournisseurs** pour afficher uniquement la liste des **événements** .
* **Fournisseurs inscrits**: Sélectionnez le fournisseur ETW et le niveau de suivi. Le niveau de suivi est l’une des valeurs suivantes :
   1. Sortie ou arrêt anormal
   2. Erreurs graves
   3. Avertissements
   4. Avertissements sans erreur

Cliquez ou appuyez sur **Activer** pour démarrer le suivi. Le fournisseur est ajouté à la liste déroulante **Fournisseurs activés**.
* **Fournisseurs personnalisés**: Sélectionnez un fournisseur ETW personnalisé et le niveau de suivi. Identifiez le fournisseur par son GUID. N’insérez pas de crochets dans le GUID.
* **Fournisseurs activés**: Répertorie les fournisseurs activés. Sélectionnez un fournisseur dans la liste déroulante, puis cliquez sur ou appuyez sur **Désactiver** pour arrêter le suivi. Cliquez ou appuyez sur **Arrêter tout** pour suspendre tout le suivi.
* **Historique des fournisseurs**: Affiche les fournisseurs ETW qui ont été activés au cours de la session active. Cliquez ou appuyez sur **Activer** pour activer un fournisseur qui a été désactivé. Cliquez ou appuyez sur **Effacer** pour supprimer l’historique.
* **Événements**: Répertorie les événements ETW des fournisseurs sélectionnés sous forme de table. Le tableau suivant est mis à jour en temps réel. Sous le tableau, cliquez sur le bouton **Effacer** pour supprimer tous les événements ETW de la table. Cela ne désactive pas les fournisseurs. Vous pouvez cliquer sur **Enregistrer dans le fichier** pour exporter vers un fichier CSV en local les événements ETW actuellement collectés.
* **Filtres**: Vous permettent de filtrer les événements ETW collectés par ID, mot clé, niveau, nom du fournisseur, nom de la tâche ou texte. Vous pouvez combiner plusieurs critères:
   1. Pour les critères appliqués à la même propriété, les événements peuvent répondre à l’un de ces critères.
   2. Pour les critères appliqués à des événements de propriété différents doivent satisfaire à tous les critères

Par exemple, vous pouvez spécifier les critères *(le nom de la tâche contient «foo» ou «bar») et (le texte contient «Error» ou «Warning»)*

### <a name="simulation"></a>Simulation

![Page de simulation dans le portail d’appareils Windows sur Microsoft HoloLens](images/windows-device-portal-simulation-page-1000px.png)<br>
*Page de simulation dans le portail d’appareils Windows sur Microsoft HoloLens*

Vous permet d’enregistrer et de lire des données d’entrée pour le test.
* **Salle de capture**: Utilisé pour télécharger un fichier de la salle simulée qui contient le maillage de mappage spatial pour l’environnement de l’utilisateur. Nommez la salle, puis cliquez sur **capturer** pour enregistrer les données sous la forme d’un fichier. XEF sur votre PC. Ce fichier de pièce peut être chargé dans l’émulateur HoloLens.
* **Enregistrement**: Vérifiez les flux à enregistrer, nommez l’enregistrement, puis cliquez ou appuyez sur **Enregistrer** pour démarrer le recodage. Effectuez des actions avec votre HoloLens, puis cliquez sur **arrêter** pour enregistrer les données sous forme de fichier. XEF sur votre PC. Ce fichier peut être chargé dans l’émulateur ou l’appareil HoloLens.
* **Lecture**: Cliquez ou appuyez sur **charger l’enregistrement** pour sélectionner un fichier baxef sur votre ordinateur et envoyer les données vers le HoloLens.
* **Mode de contrôle**: Sélectionnez **par défaut** ou **simulation** dans la liste déroulante, puis cliquez ou appuyez sur le bouton **définir** pour sélectionner le mode sur le HoloLens. Choisissez Simulation pour désactiver les capteurs réels de votre casque HoloLens et utiliser les données simulées à la place. Si vous passez à Simulation, votre casque HoloLens ne répondra pas à l’utilisateur réel tant que vous ne serez pas revenu à l’utilisateur Par défaut.

### <a name="networking"></a>Mise en réseau

![Page mise en réseau dans le portail de périphériques Windows sur Microsoft HoloLens](images/windows-device-portal-networking-page-1000px.png)<br>
*Page mise en réseau dans le portail de périphériques Windows sur Microsoft HoloLens*

Gère les connexions Wi-Fi sur le HoloLens.
* **Adaptateurs Wi-Fi**: Sélectionnez un adaptateur Wi-Fi et un profil à l’aide des contrôles de liste déroulante. Cliquez ou appuyez sur **se connecter** pour utiliser l’adaptateur sélectionné.
* **Réseaux disponibles**: Répertorie les réseaux Wi-Fi auxquels le HoloLens peut se connecter. Cliquez ou appuyez sur Actualiser pour mettre à jour la liste.
* **Configuration IP**: Affiche l’adresse IP et d’autres détails de la connexion réseau.

### <a name="virtual-input"></a>Entrée virtuelle

![Page d’entrée virtuelle dans le portail de périphériques Windows sur Microsoft HoloLens](images/windows-device-portal-virtual-input-page-1000px.png)<br>
*Page d’entrée virtuelle dans le portail de périphériques Windows sur Microsoft HoloLens*

Envoie la saisie au clavier de l’ordinateur distant au casque HoloLens.

Cliquez ou appuyez sur la région sous **clavier virtuel** pour activer l’envoi des séquences de touches au HoloLens. Tapez dans la zone de **texte texte d’entrée** , puis cliquez ou appuyez sur **Envoyer** pour envoyer les séquences de touches à l’application active.

## <a name="device-portal-rest-apis"></a>API REST du portail des appareils

Tout le contenu du portail de l’appareil repose sur des [API REST](device-portal-api-reference.md) que vous pouvez éventuellement utiliser pour accéder aux données et contrôler votre appareil par programme.
