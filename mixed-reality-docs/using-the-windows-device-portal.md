---
title: Utilisation du portail d’appareil Windows
description: Le portail d’appareil Windows pour HoloLens vous permet de configurer et de gérer à distance votre appareil par le biais d’une connexion Wi-Fi ou USB. Le Device Portal est un serveur Web situé sur l'appareil auquel vous pouvez vous connecter depuis un navigateur Web sur votre PC. Le portail d’appareil comprend de nombreux outils qui vous aideront à gérer votre appareil HoloLens, ainsi qu’à déboguer et à optimiser vos applications.
author: JonMLyons
ms.author: jlyons
ms.date: 02/24/2019
ms.topic: article
keywords: Portail d’appareil Windows, HoloLens
ms.localizationpriority: high
ms.openlocfilehash: 6a5a0ef164cbbe80f74f0fe6cc42e08834d2a4b4
ms.sourcegitcommit: ee8c7e821cb337cbccd8af64b13ee5f50109a776
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80082091"
---
# <a name="using-the-windows-device-portal"></a>Utilisation du portail d’appareil Windows

<table>
<tr>
<th>Fonctionnalité</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens (1ère génération)</a></th><th style="width:150px">HoloLens 2</th><th style="width:150px"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> Portail d’appareil Windows</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"></td>
</tr>
</table>

Le portail d’appareil Windows pour HoloLens vous permet de configurer et de gérer à distance votre appareil par le biais d’une connexion Wi-Fi ou USB. Le Device Portal est un serveur Web situé sur l'appareil auquel vous pouvez vous connecter depuis un navigateur Web sur votre PC. Le portail d’appareil comprend de nombreux outils qui vous aideront à gérer votre appareil HoloLens, ainsi qu’à déboguer et à optimiser vos applications.

Cette documentation concerne spécifiquement le portail d’appareil Windows pour HoloLens. Si vous souhaitez utiliser le portail d’appareil Windows pour les ordinateurs de bureau (y compris pour Windows Mixed Reality), consultez [Vue d’ensemble du portail d’appareil Windows](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal).

## <a name="setting-up-hololens-to-use-windows-device-portal"></a>Configuration de HoloLens pour l’utilisation du portail d’appareil Windows

1. Mettez HoloLens sous tension et allumez l’appareil.
2. Pour lancer le menu principal, effectuez le [mouvement associé au menu Démarrer](https://docs.microsoft.com/hololens/hololens2-basic-usage#start-gesture) sur un appareil HoloLens 2 ou [écartez les doigts paume vers le haut](https://docs.microsoft.com/hololens/hololens1-basic-usage#open-the-start-menu-with-bloom) sur un appareil HoloLens (1ère génération). 
3. Pointez avec le regard sur la vignette **Paramètres**, puis [cliquez dans l’air](https://docs.microsoft.com/hololens/hololens1-basic-usage#select-holograms-with-gaze-and-air-tap) sur un appareil HoloLens (1re génération), ou sélectionnez la vignette [en la touchant ou en effectuant le geste de rayon émanant de la main](https://docs.microsoft.com/hololens/hololens2-basic-usage) sur un appareil HoloLens 2. 
4. Sélectionnez l’élément de menu **Mettre à jour**.
5. Sélectionnez l’élément de menu **Pour les développeurs**.
6. Activez **Mode développeur**.
7. [Faites défiler](gaze-and-commit.md#composite-gestures) la liste et activez le **portail d’appareil**.
8. Si vous configurez le portail d’appareil Windows afin de pouvoir déployer des applications sur cet appareil HoloLens via une connexion USB ou Wi-Fi, cliquez sur **Appairer** pour [générer un code confidentiel d’appairage](using-visual-studio.md). Dans l’application Paramètres, laissez le menu contextuel Code confidentiel ouvert jusqu’à ce que vous entriez le code confidentiel dans Visual Studio lors du premier déploiement.

   ![Activation du mode Développeur dans l’application Paramètres pour Windows Holographique](images/deviceportalsettings.png)

## <a name="connecting-over-wi-fi"></a>Connexion Wi-Fi

1. [Connectez votre appareil HoloLens au Wi-Fi](connecting-to-wi-fi-on-hololens.md).
2. Recherchez l’adresse IP de votre appareil.
   * L’adresse IP de l’appareil se trouve sous **Paramètres > Réseau et Internet > Wi-Fi > Options avancées**.
3. Sur votre PC, dans un navigateur web, accédez à https://<ADRESSE_IP_DE_VOTRE_APPAREIL_HOLOLENS>
   * Le navigateur affichera le message suivant : « Le certificat de sécurité de ce site web présente un problème ». Cela se produit car le certificat envoyé à Device Portal est un certificat de test. Vous pouvez ignorer cette erreur de certificat pour le moment et continuer.

## <a name="connecting-over-usb"></a>Connexion USB

1. [Installez les outils](install-the-tools.md) pour vérifier que Visual Studio Update 1 et les outils de développement Windows 10 sont installés sur votre PC. Cela permet d’activer la connectivité USB.
2. Connectez votre appareil HoloLens à votre PC à l’aide d’un câble micro-USB pour HoloLens (1re génération) ou d’un câble USB-C pour HoloLens 2.
3. Sur votre PC, dans un navigateur web, accédez à [https://127.0.0.1:10080](https://127.0.0.1:10080).

## <a name="connecting-to-an-emulator"></a>Connexion à un émulateur

Vous pouvez également utiliser Device Portal avec votre émulateur. Pour vous connecter au portail d’appareil, utilisez la [barre d’outils](using-the-hololens-emulator.md). Cliquez sur cette icône : ![Icône Ouvrir le portail d’appareil](images/emulator-deviceportal.png) **Ouvrir le portail d’appareil** : ouvre le Portail d’appareil Windows pour le système d’exploitation HoloLens dans l’émulateur.

## <a name="creating-a-username-and-password"></a>Création d’un nom d’utilisateur et d’un mot de passe

![Configurer l’accès au portail d’appareil Windows](images/windows-device-portal-credentials-reset-page-1000px.png)<br>
*Configurer l’accès au portail d’appareil Windows*

Vous devrez créer un nom d’utilisateur et un mot de passe sur Device Portal de votre HoloLens lors de votre première connexion.
1. Dans un navigateur web sur votre PC, entrez l’adresse IP de l’HoloLens. La page d’accès à la configuration s’affiche.
2. Cliquez ou appuyez sur **Demander un code confidentiel**, puis regardez l’écran HoloLens pour obtenir le code confidentiel généré.
3. Entrez le code confidentiel dans la **zone de texte prévue à cet effet de votre appareil**.
4. Entrez le nom d’utilisateur que vous utiliserez pour vous connecter à Device Portal. Il n’est pas nécessaire qu’il s’agisse d’un nom de compte Microsoft (MSA) ou de domaine.
5. Entrez un mot de passe et confirmez-le. Le mot de passe doit comporter au moins sept caractères. Il n’est pas nécessaire qu’il s’agisse d’un mot de passe de compte Microsoft (MSA) ou de domaine.
6. Cliquez sur **Appairer** pour vous connecter au portail d’appareil Windows sur l’appareil HoloLens.

Si vous souhaitez modifier ce nom d’utilisateur ou ce mot de passe, vous pouvez à tout moment répéter ce processus en accédant à la page de sécurité de l’appareil : https://<ADRESSE_IP_DE_VOTRE_APPAREIL_HOLOLENS>/devicepair.htm.

## <a name="security-certificate"></a>Certificat de sécurité

Si une « erreur de certificat » s’affiche dans votre navigateur, vous pouvez la résoudre en créant une relation d’approbation avec l’appareil.

Chaque HoloLens génère un certificat auto-signé unique pour sa connexion SSL. Par défaut, ce certificat n’est pas approuvé par le navigateur web de votre PC, c’est la raison pour laquelle vous obtiendrez peut-être une « erreur de certificat ». En téléchargeant ce certificat à partir de votre HoloLens (via une connexion USB ou Wi-Fi approuvée) et en l’approuvant sur votre PC, vous pouvez vous connecter en toute sécurité à votre appareil.
1. **Vérifiez que vous vous trouvez sur un réseau sécurisé (USB ou réseau Wi-Fi approuvé)** .
2. Téléchargez le certificat de cet appareil à partir de la page « Sécurité » sur le portail de l’appareil.
   * Accédez à : https://<ADRESSE_IP_DE_VOTRE_APPAREIL_HOLOLENS>/devicepair.htm
   * Ouvrez le nœud Système > Préférences. 
   * Faites défiler jusqu’à Sécurité des appareils, puis cliquez sur le bouton « Télécharger le certificat de cet appareil ».
3. Installez le certificat dans le magasin de « Autorités de certification racines de confiance » de votre PC.
   * Dans le menu Windows, tapez : gérer les certificats d’ordinateur et démarrer l’applet.
   * Développez le dossier **Trusted Root Certification Authority**.
   * Cliquez sur le dossier **Certificats**.
   * Dans le menu Action, sélectionnez : Toutes les tâches > Importer...
   * Terminez l’Assistant Importation de certificat en utilisant le fichier de certificat que vous avez téléchargé à partir de Device Portal.
4. Redémarrez le navigateur.

>[!NOTE]
> Ce certificat sera uniquement approuvé pour l’appareil et l’utilisateur devra recommencer le processus si l’appareil est flashé.


## <a name="device-portal-pages"></a>Pages de Device Portal

### <a name="home"></a>page d'accueil

![Page d’accueil du portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-home-page-1000px.png)<br>
*Page d’accueil du portail d’appareil Windows sur Microsoft HoloLens*

Votre session Device Portal démarre sur la page d’accueil. Accédez à d’autres pages à partir de la barre de navigation située sur le côté gauche de la page d’accueil.

La barre d’outils se trouvant en haut de la page permet d’accéder aux fonctionnalités et aux états couramment utilisés.
* **En ligne** : indique si l’appareil est connecté au Wi-Fi.
* **Arrêt** : éteint l’appareil.
* **Redémarrer** : mise sous tension de l’appareil par cycle.
* **Sécurité** : ouvre la page de sécurité de l’appareil.
* **Froid** : indique la température de l’appareil.
* **Secteur** : indique si l’appareil est branché sur le secteur et en cours de chargement.
* **Aide** : ouvre la page relative à la documentation de l’interface REST.

La page d’accueil affiche les informations suivantes :
* **État de l’appareil** : supervise l’état de votre appareil et signale les erreurs critiques.
* **Informations Windows** : affiche le nom du casque HoloLens et la version de Windows installée.
* La section **Préférences** comprend les paramètres suivants :
   * **IPD** : définit l’écart pupillaire correspondant à la distance, exprimée en millimètres, séparant le centre des pupilles de l’utilisateur lorsqu’il regarde droit devant lui. Le paramètre prend immédiatement effet. La valeur par défaut a été calculée automatiquement lors de la configuration de votre appareil.
   * **Nom de l’appareil** : attribuez un nom au casque HoloLens. Vous devez redémarrer l’appareil après avoir modifié cette valeur afin qu’elle soit prise en compte. Après avoir cliqué sur **Enregistrer**, une boîte de dialogue vous demande si vous voulez redémarrer l’appareil immédiatement ou ultérieurement.
   * **Paramètres de la veille** : définit le délai d’attente avant la mise en veille de l’appareil lorsque celui-ci est branché ou sur batterie.

### <a name="3d-view"></a>Vue 3D

![Page Vue 3D dans le portail d’appareil Windows sur Microsoft HoloLens](images/3dview-1000px.png)<br>
*Page Vue 3D dans le portail d’appareil Windows sur Microsoft HoloLens*

Utilisez la page Vue 3D pour voir comment HoloLens interprète votre environnement. Naviguez dans la vue à l’aide de la souris :
* Pivoter : clic gauche + souris
* Mouvement panoramique : clic droit + souris
* Zoom : défilement à l’aide de la souris.
* **Options de suivi** :
   * activez le suivi visuel en continu en cochant **Forcer le suivi visuel**. 
   * **Suspendre** arrête le suivi visuel.
* **Options d’affichage** : définissez les options de l’affichage 3D :
  * **Suivi** : indique si le suivi visuel est actif.
  * **Afficher le sol** : affiche un plan de sol en damier.
  * **Afficher le tronc de cône** : affiche le tronc de cône.
  * **Afficher le plan de stabilisation** : affiche le plan utilisé par HoloLens pour stabiliser le mouvement.
  * **Afficher le maillage** : affiche le maillage de mappage de surface qui représente votre environnement.
  * **Afficher les ancres spatiales** : affiche les ancres spatiales de l’application active. Vous devez cliquer sur le bouton Mettre à jour pour récupérer et actualiser les ancres.
  * **Afficher les détails** : affiche la position des mains, les quaternions de rotation de la tête et le vecteur d’origine à mesure de leur changement en temps réel.
  * **Bouton plein écran** : affiche la vue 3D en mode plein écran. Appuyez sur la touche ÉCHAP pour quitter le mode plein écran.
* **Reconstruction de surface** : cliquez ou appuyez sur **Mettre à jour** pour afficher le tout dernier maillage de mappage spatial à partir de l’appareil. Un passage complet peut nécessiter un certain temps (pouvant aller jusqu’à quelques secondes). Le maillage ne se met pas à jour automatiquement dans la vue 3D. Vous devez cliquer sur **Mettre à jour** pour obtenir le tout dernier maillage à partir de l’appareil. Cliquez sur **Enregistrer** pour enregistrer le maillage de mappage spatial actuel en tant que fichier obj sur votre PC.
* **Ancres spatiales** : cliquez sur Mettre à jour pour afficher ou mettre à jour les ancres spatiales de l’application active.

### <a name="mixed-reality-capture"></a>MRC (Mixed Reality Capture)

![Page Capture de Réalité Mixte dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-mixed-reality-capture-page-1000px.png)<br>
*Page Capture de Réalité Mixte dans le portail d’appareil Windows sur Microsoft HoloLens*

Utilisez la page MRC pour enregistrer les flux multimédias issus du casque HoloLens.
* **Paramètres** : contrôle les flux multimédias capturés en vérifiant les paramètres suivants :
  * **Hologrammes** : capture le contenu holographique du flux vidéo. Les hologrammes font l’objet d’un rendu en mono et non en stéréo.
  * **Caméra PV** : capture le flux vidéo à partir de l’appareil photo ou de la caméra vidéo.
  * **Son du micro** : capture les données audio à partir du réseau de microphones.
  * **Son de l’application** : capture les données audio à partir de l’application en cours d’exécution.
  * **Afficher à partir de la caméra** : aligne la capture sur le point de vue de l’appareil photo ou de la caméra vidéo, si cela est [pris en charge par l’application en cours d’exécution](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in) (HoloLens 2 uniquement).
  * **Qualité de l’aperçu instantané** : sélectionnez la résolution d’écran, la fréquence d’images et la vitesse de streaming de l’aperçu instantané.
* Cliquez ou appuyez sur le bouton **Aperçu instantané** pour afficher le flux de capture. **Arrêter l’aperçu instantané** arrête le flux de capture.
* Cliquez ou appuyez sur **Enregistrer** pour commencer à enregistrer le flux de réalité mixte à l’aide des paramètres spécifiés. **Arrêter l’enregistrement** arrête l’enregistrement et le sauvegarde.
* Cliquez ou appuyez sur **Prendre une photo** pour prendre une image fixe à partir du flux de capture.
* **Photos et vidéos** : affiche une liste des captures photo et vidéo prises sur l’appareil.

> [!NOTE]
> Il existe des [limites concernant les captures de Réalité Mixte simultanées](mixed-reality-capture-for-developers.md#simultaneous-mrc-limitations) :
> * Si une application tente d’accéder à l’appareil photo ou à la caméra vidéo alors que le portail de d’appareil Windows est en train d’enregistrer une vidéo, l’enregistrement vidéo s’arrête.
>   * HoloLens 2 n’arrête pas l’enregistrement vidéo si l’application accède à l’appareil photo ou à la caméra vidéo en mode SharedReadOnly.
> * Si une application utilise activement l’appareil photo ou la caméra vidéo, le portail d’appareil Windows peut prendre une photo ou enregistrer une vidéo.
> * Streaming en direct :
>   * HoloLens (1re génération) empêche une application d’accéder à l’appareil photo ou à la caméra vidéo pendant le streaming en direct à partir du portail d’appareil Windows.
>   * HoloLens (1ère génération) ne parviendra pas à effectuer un streaming en direct si une application utilise activement l’appareil photo ou la caméra vidéo.
>   * HoloLens 2 arrête automatiquement le streaming en direct quand une application tente d’accéder à l’appareil photo ou à la caméra vidéo en mode ExclusiveControl.
>   * HoloLens 2 peut démarrer un flux en direct pendant qu’une application utilise activement la caméra PV.

### <a name="performance-tracing"></a>Suivi des performances

![Page Suivi des performances dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-performance-tracing-page-1000px.png)<br>
*Page Suivi des performances dans le portail d’appareil Windows sur Microsoft HoloLens*

Capturez les suivis de l’[Enregistreur de performance Windows](https://msdn.microsoft.com/library/windows/hardware/hh448205.aspx) (WPR) à partir de votre appareil HoloLens.
* **Profils disponibles** : sélectionnez le profil WPR dans la liste déroulante, puis cliquez ou appuyez sur **Démarrer** pour commencer le suivi.
* **Profils personnalisés** : cliquez ou appuyez sur **Parcourir** pour choisir un profil WPR sur votre PC. Cliquez ou appuyez sur **Charger et démarrer** pour commencer le suivi.

Pour arrêter le suivi, cliquez sur le lien Arrêter. Restez dans cette page jusqu’à ce que le fichier de suivi ait terminé le téléchargement.

Les fichiers ETL capturés peuvent être ouverts pour analyse dans [Windows Performance Analyzer](https://msdn.microsoft.com/library/windows/hardware/hh448170.aspx).

### <a name="processes"></a>Processus

![Page Processus dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-running-processes-page-1000px.png)<br>
*Page Processus dans le portail d’appareil Windows sur Microsoft HoloLens*

Affiche les détails concernant les processus en cours d’exécution. Cela comprend les processus relatifs aux applications au système.

### <a name="system-performance"></a>Performances du système

![Page Performances du système dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-system-performance-page-1000px.png)<br>
*Page Performances du système dans le portail d’appareil Windows sur Microsoft HoloLens*

Présente des graphiques en temps réel des informations de diagnostic système, telles que la consommation d’énergie, la fréquence d’images et la charge du processeur.

Voici les mesures disponibles :
* **Alimentation SOC** : utilisation de l’alimentation système sur puce instantanée, moyenne par minute
* **Alimentation système** : utilisation de l’alimentation système instantanée, moyenne par minute
* **Fréquence d’images** : images par seconde, VBlanks manqués par seconde et VBlanks manqués successifs
* **GPU** : utilisation du moteur GPU, pourcentage du total disponible
* **Processeur** : pourcentage du total disponible
* **E/S** : lectures et écritures
* **Réseau** : réceptions et envois
* **Mémoire** : totale, en cours d’utilisation, disponible validée, paginée et non paginée

### <a name="apps"></a>Applications

![Page Applications dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-apps-page-1000px.png)<br>
*Page Applications dans le portail d’appareil Windows sur Microsoft HoloLens*

Gère les applications qui sont installées sur l’appareil HoloLens.
* **Applications installées** : supprime et démarre des applications.
* **Applications en cours d’exécution** : liste les applications en cours d’exécution.
* **Installer l’application** : sélectionne les packages d’application à installer à partir d’un dossier de votre ordinateur ou de votre réseau.
* **Dépendance** : ajoute des dépendances à l’application que vous souhaitez installer.
* **Déployer** : déploie l’application et les dépendances sélectionnées sur l’appareil HoloLens.

### <a name="app-crash-dumps"></a>Vidages sur incident des applications

![Page Vidages sur incident des applications dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-dev-apps-crash-dumps-page-1000px.png)<br>
*Page Vidages sur incident des applications dans le portail d’appareil Windows sur Microsoft HoloLens*

Cette page vous permet de recueillir les vidages sur incident de vos applications chargées de manière indépendante. Cochez la case **Activation des vidages sur incident** pour chaque application pour laquelle vous souhaitez recueillir des vidages sur incident. Revenez à cette page pour recueillir les vidages sur incident. Les fichiers de vidage peuvent être [ouverts dans Visual Studio pour le débogage](https://msdn.microsoft.com/library/d5zhxt22.aspx).

### <a name="file-explorer"></a>Explorateur de fichiers

![Page Explorateur de fichiers dans le portail d’appareil Windows sur Microsoft HoloLens](images/fileexplorer-1000px.png)<br>
*Page Explorateur de fichiers dans le portail d’appareil Windows sur Microsoft HoloLens*

Utilisez l’Explorateur de fichiers pour parcourir, charger et télécharger des fichiers. Vous pouvez utiliser les fichiers du dossier Documents, du dossier Images et des dossiers de stockage local des applications que vous avez déployées à partir de Visual Studio ou du portail d’appareil.

### <a name="kiosk-mode"></a>Mode plein écran

>[!NOTE]
>Le mode plein écran est disponible uniquement avec la suite [Microsoft HoloLens Commercial Suite](commercial-features.md).

Pour obtenir des instructions à jour sur l’activation du mode plein écran via le portail d’appareil Windows, consultez l’article [Configurer HoloLens en mode plein écran](https://docs.microsoft.com/hololens/hololens-kiosk#set-up-kiosk-mode-using-the-windows-device-portal-windows-10-version-1607-and-version-1803) sur Windows IT Pro Center.

### <a name="logging"></a>Journalisation

![Page Journalisation dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-logging-page-1000px.png)<br>
*Page Journalisation dans le portail d’appareil Windows sur Microsoft HoloLens*

Gère en temps réel le suivi d’événements pour Windows (ETW) sur l’appareil HoloLens.

Cochez la case **Masquer les fournisseurs** pour n’afficher que la liste **Événements**.
* **Fournisseurs inscrits** : sélectionnez le fournisseur ETW et le niveau de suivi. Le niveau de suivi est l’une des valeurs suivantes :
   1. Sortie ou arrêt anormal
   2. Erreurs graves
   3. Avertissements
   4. Avertissements sans erreur

Cliquez ou appuyez sur **Activer** pour démarrer le suivi. Le fournisseur est ajouté à la liste déroulante **Fournisseurs activés**.
* **Fournisseurs personnalisés** : sélectionnez un fournisseur ETW personnalisé et le niveau de suivi. Identifiez le fournisseur par son GUID. N’insérez pas de crochets dans le GUID.
* **Fournisseurs activés** : liste les fournisseurs activés. Sélectionnez un fournisseur dans la liste déroulante, puis cliquez sur ou appuyez sur **Désactiver** pour arrêter le suivi. Cliquez ou appuyez sur **Arrêter tout** pour suspendre tout le suivi.
* **Historique des fournisseurs** : affiche les fournisseurs ETW activés pendant la session active. Cliquez ou appuyez sur **Activer** pour activer un fournisseur qui a été désactivé. Cliquez ou appuyez sur **Effacer** pour supprimer l’historique.
* **Événements** : liste les événements ETW des fournisseurs sélectionnés sous forme de tableau. Le tableau suivant est mis à jour en temps réel. En dessous du tableau, cliquez sur le bouton **Effacer** pour supprimer tous les événements ETW du tableau. Cela ne désactive pas les fournisseurs. Vous pouvez cliquer sur **Enregistrer dans le fichier** pour exporter vers un fichier CSV en local les événements ETW actuellement collectés.
* **Filtres** : permettent de filtrer les événements ETW collectés par ID, mot clé, niveau, nom du fournisseur, nom de la tâche ou texte. Vous pouvez combiner plusieurs critères :
   1. Pour les critères qui sont appliqués à une même propriété, les événements qui peuvent satisfaire l’un de ces critères sont affichés.
   2. Pour les critères qui sont appliqués à une propriété différente, les événements doivent satisfaire à tous les critères.

Par exemple, vous pouvez spécifier les critères *(Le nom de la tâche contient 'Foo' ou 'Bar') AND (Le texte contient 'erreur' ou 'avertissement')*

### <a name="simulation"></a>Simulation

![Page Simulation dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-simulation-page-1000px.png)<br>
*Page Simulation dans le portail d’appareil Windows sur Microsoft HoloLens*

Vous permet d’enregistrer et de lire des données d’entrée pour le test.
* **Capturer la salle** : permet de télécharger un fichier de simulation de pièce contenant le maillage de mappage spatial de l’environnement de l’utilisateur. Nommez la pièce, puis cliquez sur **Capturer** pour enregistrer les données sous forme de fichier .xef sur votre PC. Ce fichier de pièce peut être chargé dans l’émulateur HoloLens.
* **Enregistrement** : cochez les flux à enregistrer, nommez l’enregistrement, puis cliquez ou appuyez sur **Enregistrer** pour démarrer l’enregistrement. Effectuer des actions avec votre HoloLens, puis cliquez sur **Arrêter** pour enregistrer les données sous forme de fichier .xef sur votre PC. Ce fichier peut être chargé dans l’émulateur ou l’appareil HoloLens.
* **Lecture** : cliquez ou appuyez sur **Charger l’enregistrement** pour sélectionner un fichier xef à partir de votre PC et envoyer les données à HoloLens.
* **Mode contrôle** : sélectionnez **Par défaut** ou **Simulation** dans la liste déroulante, puis cliquez ou appuyez sur le bouton **Définir** pour sélectionner le mode sur le casque HoloLens. Choisissez Simulation pour désactiver les capteurs réels de votre casque HoloLens et utiliser les données simulées à la place. Si vous passez à Simulation, votre casque HoloLens ne répondra pas à l’utilisateur réel tant que vous ne serez pas revenu à l’utilisateur Par défaut.

### <a name="networking"></a>Mise en réseau

![Page Réseaux dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-networking-page-1000px.png)<br>
*Page Réseaux dans le portail d’appareil Windows sur Microsoft HoloLens*

Gère les connexions Wi-Fi sur l’appareil HoloLens.
* **Adaptateurs Wi-Fi** : sélectionnez un adaptateur Wi-Fi et un profil à l’aide des contrôles de la liste déroulante. Cliquez ou appuyez sur **Se connecter** pour utiliser l’adaptateur sélectionné.
* **Réseaux disponibles** : liste les réseaux Wi-Fi auxquels l’appareil HoloLens peut se connecter. Cliquez ou appuyez sur **Actualiser** pour mettre à jour la liste.
* **Configuration IP** : affiche l’adresse IP et d’autres informations concernant la connexion réseau.

### <a name="virtual-input"></a>Entrée virtuelle

![Page Entrée virtuelle dans le portail d’appareil Windows sur Microsoft HoloLens](images/windows-device-portal-virtual-input-page-1000px.png)<br>
*Page Entrée virtuelle dans le portail d’appareil Windows sur Microsoft HoloLens*

Envoie la saisie au clavier de l’ordinateur distant au casque HoloLens.

Cliquez ou appuyez sur la zone située sous le **clavier virtuel** pour permettre l’envoi de séquences de touches au casque HoloLens. Saisissez du texte dans la **zone de saisie de texte**, puis cliquez ou appuyez sur **Envoyer** pour envoyer les séquences de touches à l’application active.

## <a name="device-portal-rest-apis"></a>API REST du portail d’appareil

Dans le portail d’appareil, tout repose sur les [API REST](device-portal-api-reference.md) que vous pouvez utiliser pour accéder aux données et contrôler votre appareil par programmation, si vous le souhaitez.
