---
title: Notes de publication-août 2016
description: HoloLens les notes de version pour les 10 anniversaire de publication de Windows (automne 2016)
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, release notes, système d’exploitation, plate-forme, fonctionnalités, suite commerciale
ms.openlocfilehash: 2fde8665f3572589abd3dcdfb3747ca487b66afb
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596358"
---
# <a name="release-notes---august-2016"></a>Notes de publication-août 2016

L’équipe HoloLens est écouté les développeurs dans le programme Insider de Windows pour hiérarchiser son travail. Continuez à [envoyez-nous vos commentaires](give-us-feedback.md) via le Hub de commentaires, la [forums de développeurs](https://forums.hololens.com) et [Twitter via @HoloLens ](https://twitter.com/hololens). Comme Windows 10 intègre que la mise à jour anniversaire, l’équipe de HoloLens est heureux de vous fournir améliore davantage l’expérience HOLOGRAPHIQUE. Dans cette mise à jour, nous nous sommes concentrés sur les principaux correctifs, améliorations et présentation des fonctionnalités demandées par les entreprises et disponible dans la Suite de commerciaux Microsoft HoloLens.

**Version la plus récente :** Mise à jour de Windows HOLOGRAPHIQUE août 2016 (**10.0.14393.0**, version d’anniversaire Windows 10)

>[!VIDEO https://www.youtube.com/embed/tNd0e2CiAkE]

Pour [mise à jour vers la version actuelle](updating-hololens.md), ouvrez le *paramètres* application, accédez à *mise à jour & sécurité*, puis sélectionnez le *vérifier les mises à jour* bouton.

## <a name="new-features"></a>Nouvelles fonctionnalités

**Attacher au débogage d’un processus** HoloLens prend désormais en charge le débogage de l’attacher au processus. Vous pouvez utiliser Visual Studio 2015 Update 3 pour se connecter à une application en cours d’exécution sur un HoloLens et [commencer à le déboguer](using-visual-studio.md#debugging-an-installed-or-running-app). Cela fonctionne sans avoir à déployer à partir d’un projet Visual Studio.

**Mise à jour de HoloLens émulateur** nous avons également publié une version mise à jour de l’émulateur HoloLens.

**Prise en charge de Gamepad** vous pouvez maintenant associer et utiliser des boîtiers de commande Bluetooth avec HoloLens ! Le qui vient d’être publiées Xbox sans fil contrôleur propose les fonctionnalités Bluetooth et peut être utilisé pour lire vos applications et jeux prenant en charge gamepad favoris. Un [mise à jour du contrôleur](http://support.xbox.com/xbox-one/accessories/update-controller-for-stereo-headset-adapter) doivent être appliquées avant de pouvoir connecter le S de contrôleur sans fil Xbox avec HoloLens. Les opérations de mappage contrôleur Xbox sans fil est pris en charge par [XInput](https://msdn.microsoft.com/library/windows/desktop/hh405053(v=vs.85).aspx) et [Windows.Gaming.Input](https://msdn.microsoft.com/library/windows/apps/windows.gaming.input.aspx) API. Les modèles supplémentaires de contrôleurs de Bluetooth est accessible via la [Windows.Gaming.Input](https://msdn.microsoft.com/library/windows/apps/windows.gaming.input.aspx) API.

## <a name="improvements-and-fixes"></a>Améliorations et correctifs

Nous sont synchronisées avec le reste de la mise à jour anniversaire Windows 10, donc en plus des correctifs spécifiques Hololens, vous recevez également tous les bienfaits à partir de la mise à jour de Windows pour augmenter les performances et la fiabilité de la plateforme. Vos commentaires sont hautement valued et par ordre de priorité pour les corrections apportées à la version.

Nous avons amélioré les expériences suivantes :
* Ouvrez une session dans les expériences.
* jonction d’espace.
* l’efficacité des transitions d’état de périphérique d’alimentation de l’alimentation.
* stabilité avec la capture de réalité mixte.
* fiabilité pour la connectivité Bluetooth
* persistance hologramme dans un scénario d’application multiples.

Nous avons résolu les problèmes suivants :
* les profileurs Visual Studio et le débogueur graphics pas pouvoir se connecter.
* photos et documents ne s’affichent pas dans l’Explorateur de fichiers dans le portail de l’appareil.
* la barre des applications peut clignoter lorsque le curseur est placé au-dessus de lui en mode de réglage.
* En mode de réglage, l’yeux regards point curseur se transforme le curseur en flèche de 4 dans quelques instants plus lentement.
* « Hey Cortana écouter de la musique » ne lance pas de Groove.
* après la mise à jour précédente, indiquant que « Go Home » n’affiche pas le panneau de codes confidentiels correctement.

## <a name="introducing-microsoft-hololens-commercial-suite"></a>Présentation de la Suite du Commercial de Microsoft HoloLens

Microsoft HoloLens Commercial Suite est prête pour le déploiement de l’entreprise. Nous avons ajouté plusieurs demandés [fonctionnalités commerciales](commercial-features.md) à partir de nos partenaires commerciaux anticipée.

Veuillez contacter votre responsable de compte Microsoft pour acheter Microsoft HoloLens Commercial Suite.

### <a name="key-commercial-features"></a>Fonctionnalités commerciales clées 

* **Mode plein écran.** Avec le mode plein écran HoloLens, vous pouvez limiter les applications à exécuter pour permettre des expériences de démonstration ou de présentation.<br>
  ![Avec le mode plein écran, HoloLens lance directement dans l’application de votre choix.](images/201608-kioskmode-400px.png)
* **Gestion des appareils mobiles (MDM) pour HoloLens.** Votre service informatique peut gérer plusieurs appareils HoloLens simultanément à l’aide de solutions telles que Microsoft Intune. Vous serez en mesure de gérer les paramètres, de sélectionner les applications à installer et de définir les configurations de sécurité adaptées aux besoins de votre entreprise.<br>
  ![Gestion des appareils mobiles sur HoloLens fournit la gestion des appareils grade enterprise sur plusieurs appareils.](images/201608-enterprisemanagement-400px.png)
* **Mise à jour de Windows pour les entreprises.** Contrôler les mises à jour du système d’exploitation sur des appareils et de prise en charge pour long-term servicing branch.
* **Sécurité des données.** Le chiffrement de données BitLocker est activé sur HoloLens pour fournir le même niveau de protection de sécurité comme tout autre périphérique de Windows.
* **Accès Professionnel.** Toute personne de votre organisation peut se connecter à distance au réseau d’entreprise via un réseau privé virtuel sur un HoloLens. HoloLens peut accéder également à des réseaux Wi-Fi qui nécessitent des informations d’identification.
* **Microsoft Store pour entreprises.** Votre service informatique peut également configurer un magasin privé d’entreprise, contenant uniquement des applications de votre entreprise pour votre utilisation de HoloLens spécifiques. Distribuer en toute sécurité vos logiciels d’entreprise à un groupe sélectionné d’utilisateurs en entreprise.

### <a name="development-edition-vs-commercial-suite"></a>Édition de développement Visual Studio. Commercial Suite

<table>
<tr>
<th>Fonctionnalités</th><th>Development Edition</th><th>Commercial Suite</th>
</tr><tr>
<td>Chiffrement (Bitlocker) de l’appareil</td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Réseau privé virtuel (VPN)</td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td><a href="using-the-windows-device-portal.md#kiosk-mode">Mode plein écran</a></td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<th colspan="3" style="text-align: left;"> Gestion et déploiement</th>
</tr><tr>
<td>Gestion des appareils mobiles</td><td style="text-align: center;"></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Possibilité de bloquer l’annulation de l’inscription</td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Certificat en fonction d’accès Wi-Fi d’entreprise</td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Microsoft Store (consommateur)</td><td style="text-align: center;">Consommateur</td><td style="text-align: center;">Filtrage par le biais de gestion des appareils mobiles</td>
</tr><tr>
<td><a href="https://technet.microsoft.com/itpro/windows/manage/working-with-line-of-business-apps">Portail d’entreprise Store</a></td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<th colspan="3" style="text-align: left;"> Sécurité et identité</th>
</tr><tr>
<td>Connexion avec Azure Active Directory (AAD)</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Connectez-vous avec le compte Microsoft (MSA)</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Déverrouiller des informations d’identification de prochaine génération avec code PIN</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td><a href="https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/secure-boot-overview">Démarrage sécurisé</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<th colspan="3" style="text-align: left;"> Prise en charge et de maintenance</th>
</tr><tr>
<td>Système automatique des mises à jour dès leur arrivée</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td><a href="https://technet.microsoft.com/itpro/windows/plan/windows-update-for-business">Mise à jour de Windows pour les entreprises</a></td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Branche de maintenance à long terme</td><td></td><td style="text-align: center;">✔️</td>
</tr>
</table>

## <a name="prior-release-notes"></a>Notes de version antérieure
* [Notes de publication-mai 2016](release-notes-may-2016.md)
* [Notes de publication-mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Problèmes connus de HoloLens](hololens-known-issues.md)
* [Fonctionnalités commerciales](commercial-features.md)
* [Installer les outils](install-the-tools.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
