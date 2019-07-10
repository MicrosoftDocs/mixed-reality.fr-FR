---
title: À l’aide de la Windows Device Portal
description: Le Windows Device Portal pour HoloLens permet de configurer et gérer votre appareil à distance via le Wi-Fi ou USB. Le Device Portal est un serveur Web situé sur l'appareil auquel vous pouvez vous connecter depuis un navigateur Web sur votre PC. Le portail de l’appareil comprend de nombreux outils qui vous aideront à gérer vos HoloLens et le débogage et optimiser vos applications.
author: JonMLyons
ms.author: jlyons
ms.date: 02/24/2019
ms.topic: article
keywords: Windows Device Portal, HoloLens
ms.openlocfilehash: 79a4a1f99125028fcaf71e185eb00093aa8c742f
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694585"
---
# <a name="using-the-windows-device-portal"></a>À l’aide de la Windows Device Portal

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1ère génération)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> Windows Device Portal</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

Le Windows Device Portal pour HoloLens permet de configurer et gérer votre appareil à distance via le Wi-Fi ou USB. Le Device Portal est un serveur Web situé sur l'appareil auquel vous pouvez vous connecter depuis un navigateur Web sur votre PC. Le portail de l’appareil comprend de nombreux outils qui vous aideront à gérer vos HoloLens et le débogage et optimiser vos applications.

Cette documentation est spécifiquement sur le Windows Device Portal pour HoloLens. Pour utiliser le portail de l’appareil Windows pour le bureau (y compris pour la réalité mixte Windows), consultez [vue d’ensemble de Windows Device Portal](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal)

## <a name="setting-up-hololens-to-use-windows-device-portal"></a>Configuration HoloLens pour utiliser Windows Device Portal

1. Mettez HoloLens sous tension et allumez l’appareil.
2. Effectuer le geste qui consiste à [maintenir sa paume de main vers le haut en serrant ses doigts et à les ouvrir](gestures.md#bloom) pour lancer le menu principal.
3. Fixez du regard le **paramètres** vignette et effectuer le [-appui en l’air](gestures.md#air-tap) mouvement. Effectuer une deuxième appui pour placer l’application dans votre environnement. L’application Paramètres démarre une fois placée.
4. Sélectionnez l’élément de menu **Mettre à jour**.
5. Sélectionnez l’élément de menu **Pour les développeurs**.
6. Activez **Mode développeur**.
7. [Défiler vers le bas](gestures.md#composite-gestures) et activer **portail appareils**.
8. Si vous configurez Windows Device Portal afin de déployer des applications à cette HoloLens via USB ou Wi-Fi, cliquez sur **paire** à [générer un code confidentiel appariement](using-visual-studio.md). Laissez l’application de paramètres à la fenêtre contextuelle de code PIN jusqu'à ce que vous entrez le code confidentiel dans Visual Studio pendant votre premier déploiement.

   ![L’activation du mode développeur dans l’application paramètres pour Windows Holographic](images/deviceportalsettings.png)

## <a name="connecting-over-wi-fi"></a>Connexion via le Wi-Fi

1. [Connecter votre HoloLens au Wi-Fi](connecting-to-wi-fi-on-hololens.md).
2. Rechercher l’adresse IP de votre périphérique.
   * Rechercher l’adresse IP sur l’appareil sous **Paramètres > réseau & Internet > Wi-Fi > Options avancées**.
3. À partir d’un navigateur web sur votre PC, accédez à https://<YOUR_HOLOLENS_IP_ADDRESS&gt ;
   * Le navigateur affiche le message suivant : « Il est un problème avec le certificat de sécurité de ce site Web ». Cela se produit car le certificat envoyé à Device Portal est un certificat de test. Vous pouvez ignorer cette erreur de certificat pour le moment et continuer.

## <a name="connecting-over-usb"></a>Connexion via USB

1. [Installer les outils](install-the-tools.md) pour vous assurer que vous avez Visual Studio Update 1 avec les outils de développement Windows 10 installés sur votre PC. Cela permet d’activer la connectivité USB.
2. Connectez votre HoloLens au PC à l’aide d’un câble micro-USB.
3. À partir d’un navigateur web sur votre PC, accédez à http://127.0.0.1:10080.

## <a name="connecting-to-an-emulator"></a>Connexion à un émulateur

Vous pouvez également utiliser Device Portal avec votre émulateur. Pour vous connecter au portail de l’appareil, utilisez le [barre d’outils](using-the-hololens-emulator.md). Cliquez sur cette icône : ![Icône d’ouverture de portail de l’appareil](images/emulator-deviceportal.png) **ouvrir le portail de périphérique**: ouvre le Portail d’appareil Windows pour le système d’exploitation HoloLens dans l’émulateur.

## <a name="creating-a-username-and-password"></a>Création d’un nom d’utilisateur et le mot de passe

![Configurer l’accès à Windows Device Portal](images/windows-device-portal-credentials-reset-page-1000px.png)<br>
*Configurer l’accès à Windows Device Portal*

Vous devrez créer un nom d’utilisateur et un mot de passe sur Device Portal de votre HoloLens lors de votre première connexion.
1. Dans un navigateur web sur votre PC, entrez l’adresse IP de l’HoloLens. La page d’accès à la configuration s’affiche.
2. Cliquez ou appuyez sur **demande pin** et examinez l’affichage de HoloLens pour obtenir le code confidentiel généré.
3. Entrez le code confidentiel dans la **code confidentiel affiché sur votre appareil** zone de texte.
4. Entrez le nom d’utilisateur que vous utiliserez pour vous connecter à Device Portal. Il n’est pas nécessaire qu’il s’agisse d’un nom de compte Microsoft (MSA) ou de domaine.
5. Entrez un mot de passe et confirmez-le. Le mot de passe doit comporter au moins sept caractères. Il n’est pas nécessaire qu’il s’agisse d’un mot de passe de compte Microsoft (MSA) ou de domaine.
6. Cliquez sur **paire** pour se connecter à Windows Device Portal sur le HoloLens.

Si vous souhaitez modifier ce nom d’utilisateur ou le mot de passe à tout moment, vous pouvez répéter ce processus en visitant la page de sécurité de périphérique en accédant à : https://<YOUR_HOLOLENS_IP_ADDRESS>/devicepair.htm.

## <a name="security-certificate"></a>Certificat de sécurité

Si une « erreur de certificat » s’affiche dans votre navigateur, vous pouvez la résoudre en créant une relation d’approbation avec l’appareil.

Chaque HoloLens génère un certificat auto-signé unique pour sa connexion SSL. Par défaut, ce certificat n’est pas approuvé par le navigateur web de votre PC, c’est la raison pour laquelle vous obtiendrez peut-être une « erreur de certificat ». En téléchargeant ce certificat à partir de votre HoloLens (via une connexion USB ou Wi-Fi approuvée) et en l’approuvant sur votre PC, vous pouvez vous connecter en toute sécurité à votre appareil.
1. **Vérifiez que vous êtes sur un réseau sécurisé (USB ou un réseau Wi-Fi approuvé).**
2. Télécharger le certificat de cet appareil à partir de la page « Sécurité » sur le portail de l’appareil.
   * Accédez à : https://<YOUR_HOLOLENS_IP_ADDRESS>/devicepair.htm
3. Installez le certificat dans le « Trusted Root Certification Authorities » stocker sur votre PC.
   * Dans le menu Windows, tapez : Gérer les certificats d’ordinateur et démarrer l’application.
   * Développez le **de l’autorité de Certification racine de confiance** dossier.
   * Cliquez sur le **certificats** dossier.
   * Dans le menu Action, sélectionnez : Toutes les tâches > Importer...
   * Terminez l’Assistant Importation de certificat en utilisant le fichier de certificat que vous avez téléchargé à partir de Device Portal.
4. Redémarrez le navigateur.

## <a name="device-portal-pages"></a>Pages de Device Portal

### <a name="home"></a>Dossier de base

![Page d’accueil de Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-home-page-1000px.png)<br>
*Page d’accueil de Windows Device Portal sur Microsoft HoloLens*

Votre session Device Portal démarre sur la page d’accueil. Accédez à d’autres pages à partir de la barre de navigation située sur le côté gauche de la page d’accueil.

La barre d’outils se trouvant en haut de la page permet d’accéder aux fonctionnalités et aux états couramment utilisés.
* **En ligne**: Indique si l’appareil est connecté au réseau Wi-Fi.
* **Arrêt**: Désactive l’appareil.
* **Redémarrez**: Cycles mise sous tension l’appareil.
* **Sécurité** : Ouvre la page sécurité de l’appareil.
* **Froid**: Indique la température de l’appareil.
* **MISE SOUS TENSION**: Indique si l’appareil est branché et de charge.
* **Aide**: Ouvre la page de documentation d’interface REST.

La page d’accueil affiche les informations suivantes :
* **État de l’appareil :** analyse l’intégrité de votre appareil et signale les erreurs critiques.
* **Informations de Windows :** affiche le nom de la HoloLens et la version actuellement installée de Windows.
* La section **Préférences** comprend les paramètres suivants :
   * **IPD**: Définit la distance interpupillary (IPD), qui est la distance, en millimètres, entre le centre d’élèves de l’utilisateur lors de la recherche directement à l’avance. Le paramètre prend immédiatement effet. La valeur par défaut a été calculée automatiquement lors de la configuration de votre appareil.
   * **Nom de l’appareil**: Attribuez un nom pour le HoloLens. Vous devez redémarrer l’appareil après avoir modifié cette valeur afin qu’elle soit prise en compte. Après avoir cliqué sur **enregistrer**, une boîte de dialogue vous demande si vous souhaitez redémarrer immédiatement de l’appareil ou le redémarrer ultérieurement.
   * **Paramètres de mise en veille**: Définit la longueur du délai d’attente avant que l’appareil se met en veille lorsqu’il est branché et lorsqu’il est sur batterie.

### <a name="3d-view"></a>Vue 3D

![Page de vue 3D dans Windows Device Portal sur Microsoft HoloLens](images/3dview-1000px.png)<br>
*Page de vue 3D dans Windows Device Portal sur Microsoft HoloLens*

Utilisez la page Vue 3D pour voir comment HoloLens interprète votre environnement. Naviguez dans la vue à l’aide de la souris :
* Faire pivoter : clic gauche + de souris ;
* Panoramique : avec le bouton droit cliquez sur + de souris ;
* Zoom : défilement de la souris.
* **Options de suivi**
   * Activer le suivi visuel continu en vérifiant **suivi visuel de Force**. 
   * **Pause** arrête le suivi visuel.
* **Afficher les options**: Définir les options sur l’affichage 3D :
  * **Suivi des**: Indique si le suivi visuel est actif.
  * **Afficher le plancher**: Affiche un plan d’étage carreaux.
  * **Afficher frustum**: Affiche le frustum de vue.
  * **Afficher le plan de stabilisation**: Affiche le plan HoloLens utilise pour la stabilisation du mouvement.
  * **Afficher le maillage**: Affiche le maillage de mappage spatial qui représente votre environnement.
  * **Afficher les ancres spatiales**: Affiche les ancres spatiales pour l’application active. Vous devez cliquer sur le bouton de mise à jour pour obtenir et actualiser les points d’ancrage.
  * **Afficher les détails**: Affiche hand positions, les quaternions rotation principal et le vecteur d’origine appareil mesure qu’elles changent en temps réel.
  * **Bouton plein écran**: Affiche la vue 3D en mode plein écran. Appuyez sur la touche ÉCHAP pour quitter le mode plein écran.
* **Reconstruction de la surface**: Cliquez ou appuyez sur **mise à jour** pour afficher le maillage plus récente du mappage spatial de l’appareil. Un passage complet peut nécessiter un certain temps, pouvant aller jusqu’à quelques secondes. La maille ne met pas à jour automatiquement dans la vue 3D, et vous devez cliquer manuellement sur **mettre à jour** pour obtenir la maille la plus récente à partir de l’appareil. Cliquez sur **enregistrer** enregistrer le maillage de mappage spatial actuel sous la forme d’un fichier obj sur votre PC.
* **Ancres spatiales**: Cliquez sur la mise à jour pour afficher ou mettre à jour les ancres spatiales pour l’application active.

### <a name="mixed-reality-capture"></a>MRC (Mixed Reality Capture)

![Page de Capture de réalité mixte dans Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-mixed-reality-capture-page-1000px.png)<br>
*Page de Capture de réalité mixte dans Windows Device Portal sur Microsoft HoloLens*

Utilisez la page MRC pour enregistrer les flux multimédias issus du casque HoloLens.
* **Paramètres**: Contrôler les flux multimédias qui sont capturés en vérifiant les paramètres suivants :
  * **Hologrammes**: Capture le contenu HOLOGRAPHIQUE dans le flux vidéo. Les hologrammes font l’objet d’un rendu en mono et non en stéréo.
  * **Appareil photo PV**: Capture le flux vidéo à partir de la caméra vidéo/photo.
  * **MIC Audio**: Capture audio à partir du tableau de microphone.
  * **Application Audio**: Capture des données audio à partir de l’application en cours d’exécution.
  * **Restituer à partir de l’appareil photo**: Aligne la capture pour être du point de vue de la caméra vidéo/photo, si [pris en charge par l’application en cours d’exécution](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in) (HoloLens 2 uniquement).
  * **Qualité de la version préliminaire de Live**: Sélectionnez la résolution d’écran, la fréquence d’images et le taux de diffusion en continu de l’aperçu en direct.
* Cliquez ou appuyez sur la **l’aperçu instantané** bouton pour afficher le flux de capture. **Arrêter l’aperçu instantané** arrête le flux de capture.
* Cliquez ou appuyez sur **enregistrement** pour démarrer l’enregistrement du flux de réalité mixte, en utilisant les paramètres spécifiés. **Arrêter l’enregistrement** met fin à l’enregistrement et l’enregistre.
* Cliquez ou appuyez sur **Take photo** à prendre une image fixe à partir du flux de capture.
* **Photos et vidéos**: Affiche une liste de captures vidéo et photo effectuée sur l’appareil.

> [!NOTE]
> Il existe [limitations MRC simultanée](mixed-reality-capture-for-developers.md#simultaneous-mrc-limitations):
> * Si une application tente d’accéder à la caméra de photo/vidéo pendant que Windows Device Portal est d’enregistrer une vidéo, l’enregistrement vidéo s’arrête.
>   * HoloLens 2 n’empêchera pas d’enregistrement vidéo si l’acesses application la caméra vidéo/photo avec le mode de SharedReadOnly.
> * Si une application utilise activement la caméra vidéo/photo, Windows Device Portal est en mesure de prendre une photo ou un enregistrement d’une vidéo.
> * Vidéo en flux continu :
>   * HoloLens (1er gen) empêche l’application d’accéder à la caméra vidéo/photo lors de la diffusion en continu à partir de Windows Device Portal.
>   * HoloLens (1er gen) ne parviendra pas à flux temps réel si une application utilise activement la caméra vidéo/photo.
>   * HoloLens 2 s’arrête automatiquement la diffusion en continu quand une application tente d’accéder à la caméra vidéo/photo en mode de ExclusiveControl.
>   * HoloLens 2 est en mesure de démarrer un flux en direct pendant une application est activement à l’aide de l’appareil photo PV.

### <a name="performance-tracing"></a>Suivi des performances

![Page Windows Device Portal sur Microsoft HoloLens de suivi des performances](images/windows-device-portal-performance-tracing-page-1000px.png)<br>
*Page Windows Device Portal sur Microsoft HoloLens de suivi des performances*

Capturer [enregistreur de Performance Windows](https://msdn.microsoft.com/library/windows/hardware/hh448205.aspx) traces (WPR) à partir de votre HoloLens.
* **Profils disponibles**: Sélectionnez le profil WPR dans la liste déroulante, cliquez sur ou sur **Démarrer** pour démarrer le suivi.
* **Profils personnalisés**: Cliquez ou appuyez sur **Parcourir** pour choisir un profil WPR à partir de votre PC. Cliquez ou appuyez sur **Charger et démarrer** pour commencer le suivi.

Pour arrêter la trace cliquez sur le lien Arrêter. Rester sur cette page jusqu'à ce que le fichier de trace a terminé le téléchargement.

Les fichiers ETL capturés peuvent être ouverts pour analyse dans [Windows Performance Analyzer](https://msdn.microsoft.com/library/windows/hardware/hh448170.aspx).

### <a name="processes"></a>Processus

![Page de processus dans Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-running-processes-page-1000px.png)<br>
*Page de processus dans Windows Device Portal sur Microsoft HoloLens*

Affiche les détails concernant les processus en cours d’exécution. Cela comprend les processus relatifs aux applications au système.

### <a name="system-performance"></a>Performances du système

![Page de performances système dans Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-system-performance-page-1000px.png)<br>
*Page de performances système dans Windows Device Portal sur Microsoft HoloLens*

Présente des graphiques en temps réel des informations de diagnostic système, telles que la consommation d’énergie, la fréquence d’images et la charge du processeur.

Voici les mesures disponibles :
* **SoC power**: Consommation d’énergie de système sur puce instantanée, moyenne par minute
* **Alimentation du système**: Consommation d’énergie système instantanée, moyenne par minute
* **Fréquence d’images**: Images par seconde, manqué VBlanks par seconde et consécutifs VBlanks manquée
* **GPU**: Moteur l’utilisation du GPU, pourcentage du total disponible
* **Processeur**: pourcentage du total disponible
* **E/S**: Lectures et écritures
* **Réseau** : Reçus et envoyés
* **Mémoire**: Total, en cours d’utilisation, validée, paginées et réserve non paginée

### <a name="apps"></a>Applications

![Page applications dans Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-apps-page-1000px.png)<br>
*Page applications dans Windows Device Portal sur Microsoft HoloLens*

Gère les applications qui sont installées sur le HoloLens.
* **Applications installées**: Supprimez et démarrer des applications.
* **Exécution d’applications**: Répertorie les applications qui sont en cours d’exécution.
* **Installer application**: Sélectionnez les packages d’application pour l’installation à partir d’un dossier sur votre ordinateur/réseau.
* **Dépendance**: Ajouter des dépendances de l’application que vous vous apprêtez à installer.
* **Déployer**: Déployer l’application sélectionnée + les dépendances sur le HoloLens.

### <a name="app-crash-dumps"></a>Vidages sur incident d’application

![Page de vidages sur incident d’application dans Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-dev-apps-crash-dumps-page-1000px.png)<br>
*Page de vidages sur incident d’application dans Windows Device Portal sur Microsoft HoloLens*

Cette page vous permet de recueillir les vidages sur incident de vos applications chargées de manière indépendante. Vérifier le **incident vidages activé** case à cocher pour chaque application pour laquelle vous souhaitez collecter les vidages sur incident. Revenez à cette page pour recueillir les vidages sur incident. Fichiers dump peuvent être [ouvert dans Visual Studio pour le débogage](https://msdn.microsoft.com/library/d5zhxt22.aspx).

### <a name="file-explorer"></a>Explorateur de fichiers

![Page de l’Explorateur de fichiers dans Windows Device Portal sur Microsoft HoloLens](images/fileexplorer-1000px.png)<br>
*Page de l’Explorateur de fichiers dans Windows Device Portal sur Microsoft HoloLens*

Utilisez l’Explorateur de fichiers pour parcourir, charger et télécharger des fichiers. Vous pouvez travailler avec des fichiers dans le dossier de Documents, le dossier images et dans les dossiers de stockage local pour les applications que vous avez déployé à partir de Visual Studio ou le portail de l’appareil.

### <a name="kiosk-mode"></a>Mode plein écran

>[!NOTE]
>Mode plein écran est disponible uniquement avec les [Microsoft HoloLens Commercial Suite](commercial-features.md).

Vérifiez le [configurer HoloLens en mode plein écran](https://docs.microsoft.com/hololens/hololens-kiosk#set-up-kiosk-mode-using-the-windows-device-portal-windows-10-version-1607-and-version-1803) article dans le Centre Windows IT Pro pour obtenir des instructions à jour sur l’activation du mode plein écran via Windows Device Portal.

### <a name="logging"></a>Journalisation

![Page d’enregistrement dans Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-logging-page-1000px.png)<br>
*Page d’enregistrement dans Windows Device Portal sur Microsoft HoloLens*

Gère en temps réel Event Tracing for Windows (ETW) sur le HoloLens.

Vérifiez **masquer fournisseurs** pour afficher le **événements** afficher uniquement la liste.
* **Inscrit les fournisseurs**: Sélectionnez le fournisseur ETW et le niveau de suivi. Le niveau de suivi est l’une des valeurs suivantes :
   1. Sortie ou arrêt anormal
   2. Erreurs graves
   3. Avertissements
   4. Avertissements sans erreur

Cliquez ou appuyez sur **Activer** pour démarrer le suivi. Le fournisseur est ajouté à la liste déroulante **Fournisseurs activés**.
* **Fournisseurs personnalisés**: Sélectionnez un fournisseur ETW personnalisé et le niveau de suivi. Identifiez le fournisseur par son GUID. N’insérez pas de crochets dans le GUID.
* **Les fournisseurs activés**: Répertorie les fournisseurs activés. Sélectionnez un fournisseur dans la liste déroulante, puis cliquez sur ou appuyez sur **Désactiver** pour arrêter le suivi. Cliquez ou appuyez sur **Arrêter tout** pour suspendre tout le suivi.
* **Historique de fournisseurs**: Présente les fournisseurs ETW qui ont été activées pendant la session active. Cliquez ou appuyez sur **Activer** pour activer un fournisseur qui a été désactivé. Cliquez ou appuyez sur **Effacer** pour supprimer l’historique.
* **événements**: Répertorie les événements ETW à partir de fournisseurs sélectionnés sous forme de tableau. Le tableau suivant est mis à jour en temps réel. Sous la table, cliquez sur le **clair** bouton pour supprimer tous les événements ETW de la table. Cela ne désactive pas les fournisseurs. Vous pouvez cliquer sur **Enregistrer dans le fichier** pour exporter vers un fichier CSV en local les événements ETW actuellement collectés.
* **Filtres**: Permettent de filtrer les événements ETW collectées par ID, mot clé, niveau, nom du fournisseur, nom de la tâche ou texte. Vous pouvez combiner plusieurs critères :
   1. Pour appliquer des critères pour la même propriété - événements peuvent satisfaire l’un de ces critères sont affichés.
   2. Pour les critères appliquant une propriété différente - événements doivent satisfaire tous les critères

Par exemple, vous pouvez spécifier les critères *(nom de la tâche contient « Foo » ou « Barre ») et (texte contient « error » ou « avertissement »)*

### <a name="simulation"></a>Simulation

![Page de simulation dans Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-simulation-page-1000px.png)<br>
*Page de simulation dans Windows Device Portal sur Microsoft HoloLens*

Vous permet d’enregistrer et de lire des données d’entrée pour le test.
* **Capturer la salle**: Utilisé pour télécharger un fichier de pièce simulé qui contient la maille de mappage spatial pour l’environnement de l’utilisateur. Nom de la salle et puis cliquez sur **capturer** pour enregistrer les données sous forme de fichier .xef sur votre PC. Ce fichier de pièce peut être chargé dans l’émulateur HoloLens.
* **L’enregistrement**: Vérifier le flux de données à enregistrer, de nom de l’enregistrement, puis cliquez ou appuyez sur **enregistrement** pour commencer à recoder. Effectuer des actions avec votre HoloLens, puis cliquez sur **arrêter** pour enregistrer les données sous forme de fichier .xef sur votre PC. Ce fichier peut être chargé dans l’émulateur ou l’appareil HoloLens.
* **Lecture**: Cliquez ou appuyez sur **chargement enregistrement** pour sélectionner un fichier xef à partir de votre PC et envoyer les données à l’HoloLens.
* **Mode de contrôle**: Sélectionnez **par défaut** ou **Simulation** à partir de la liste déroulante, cliquez sur ou sur le **définir** bouton pour sélectionner le mode sur le HoloLens. Choisissez Simulation pour désactiver les capteurs réels de votre casque HoloLens et utiliser les données simulées à la place. Si vous passez à Simulation, votre casque HoloLens ne répondra pas à l’utilisateur réel tant que vous ne serez pas revenu à l’utilisateur Par défaut.

### <a name="networking"></a>Mise en réseau

![Page de mise en réseau dans Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-networking-page-1000px.png)<br>
*Page de mise en réseau dans Windows Device Portal sur Microsoft HoloLens*

Gère les connexions Wi-Fi sur le HoloLens.
* **Adaptateurs de Wi-Fi**: Sélectionnez un adaptateur Wi-Fi et un profil en utilisant les contrôles de liste déroulante. Cliquez ou appuyez sur **Connect** à utiliser l’adaptateur sélectionné.
* **Les réseaux disponibles**: Répertorie les réseaux Wi-Fi le HoloLens pouvant se connecter à. Cliquez ou appuyez sur **Actualiser** pour mettre à jour la liste.
* **Configuration IP**: Affiche l’adresse IP et autres détails de la connexion réseau.

### <a name="virtual-input"></a>Entrée virtuelle

![Page d’entrée virtuelle dans Windows Device Portal sur Microsoft HoloLens](images/windows-device-portal-virtual-input-page-1000px.png)<br>
*Page d’entrée virtuelle dans Windows Device Portal sur Microsoft HoloLens*

Envoie la saisie au clavier de l’ordinateur distant au casque HoloLens.

Cliquez ou appuyez sur la région sous **virtuelle clavier** pour activer les touches envoi à l’HoloLens. Tapez dans la **texte d’entrée** zone de texte et cliquez ou appuyez sur **envoyer** pour envoyer les séquences de touches à l’application active.

## <a name="device-portal-rest-apis"></a>D’API REST portail des appareils

Tous les éléments dans le portail de l’appareil sont construit sur [l’API REST](device-portal-api-reference.md) que vous pouvez éventuellement utiliser pour accéder aux données et de contrôler par programmation de votre appareil.
