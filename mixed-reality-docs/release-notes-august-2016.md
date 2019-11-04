---
title: Notes de publication-août 2016
description: Notes de publication HoloLens pour la version anniversaire de Windows 10 (automne 2016)
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, notes de publication, système d’exploitation, plateforme, fonctionnalités, suite commerciale
ms.openlocfilehash: dcac64524cd8d1b1f2b0a496c4dcd2ad2fc7b690
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438092"
---
# <a name="release-notes---august-2016"></a>Notes de publication-août 2016

L’équipe HoloLens écoute les commentaires des développeurs du programme Windows Insider pour hiérarchiser notre travail. Continuez à [nous faire part de vos commentaires](give-us-feedback.md) via le hub de commentaires, les [Forums des développeurs](https://forums.hololens.com) et [Twitter via @HoloLens](https://twitter.com/hololens). Étant donné que Windows 10 adopte la mise à jour anniversaire, l’équipe HoloLens est ravie de fournir davantage d’améliorations à l’expérience holographique. Dans cette mise à jour, nous nous sommes concentrés sur les principaux correctifs, les améliorations et l’introduction des fonctionnalités demandées par les entreprises et disponibles dans la suite commerciale Microsoft HoloLens.

**Dernière version :** Mise à jour 2016 de Windows holographique août (**10.0.14393.0**, version anniversaire Windows 10)

>[!VIDEO https://www.youtube.com/embed/tNd0e2CiAkE]

Pour effectuer une [mise à jour vers la version actuelle](updating-hololens.md), ouvrez l’application *paramètres* , accédez à *mettre à jour & sécurité*, puis sélectionnez le bouton *Rechercher les mises à jour* .

## <a name="new-features"></a>Nouvelles fonctionnalités

**Attacher au débogage de processus** HoloLens prend désormais en charge le débogage d’attachement-à-processus. Vous pouvez utiliser Visual Studio 2015 Update 3 pour vous connecter à une application en cours d’exécution sur un HoloLens et [Démarrer le débogage](using-visual-studio.md#debugging-an-installed-or-running-app). Cela fonctionne sans qu’il soit nécessaire de procéder au déploiement à partir d’un projet Visual Studio.

**Émulateur HoloLens mis à jour** Nous avons également publié une version mise à jour de l’émulateur HoloLens.

**Prise en charge du boîtier de manette** Vous pouvez maintenant coupler et utiliser des manette Bluetooth avec HoloLens ! La nouvelle version du contrôleur Xbox Wireless S offre des fonctionnalités Bluetooth et peut être utilisée pour jouer à vos jeux et applications préférés. Une [mise à jour du contrôleur](https://support.xbox.com/xbox-one/accessories/update-controller-for-stereo-headset-adapter) doit être appliquée avant de pouvoir connecter les contrôleurs Xbox Wireless S avec HoloLens. Le contrôleur Xbox Wireless S est pris en charge par les API [XInput](https://msdn.microsoft.com/library/windows/desktop/hh405053(v=vs.85).aspx) et [Windows. Gaming. Input](https://msdn.microsoft.com/library/windows/apps/windows.gaming.input.aspx) . Il est possible d’accéder à d’autres modèles de contrôleurs Bluetooth via l’API [Windows. Gaming. Input](https://msdn.microsoft.com/library/windows/apps/windows.gaming.input.aspx) .

## <a name="improvements-and-fixes"></a>Améliorations et correctifs

Nous sommes synchronisés avec le reste de la mise à jour anniversaire Windows 10. par conséquent, en plus des correctifs spécifiques à HoloLens, vous bénéficiez également de tous les avantages de Windows Update pour améliorer la fiabilité et les performances de la plateforme. Vos commentaires sont très appréciés et classés par ordre de priorité pour les correctifs de la version.

Nous avons amélioré les expériences suivantes :
* Connectez-vous à l’expérience.
* jonction d’espace de travail.
* efficacité énergétique des transitions d’état d’alimentation des appareils.
* stabilité avec les captures de la réalité mixte.
* fiabilité de la connectivité Bluetooth
* persistance des hologrammes dans un scénario à plusieurs applications.

Nous avons résolu les problèmes suivants :
* les profileurs Visual Studio et le débogueur graphique ne parviennent pas à se connecter.
* les photos & documents ne sont pas affichés dans l’Explorateur de fichiers dans le portail de l’appareil.
* la barre d’application peut clignoter lorsque le curseur est placé au-dessus de lui en mode ajuster.
* En mode d’ajustement, le curseur en forme de point de regard de l’œil passe au curseur à quatre flèches plus lentement.
* « Hey Cortana Play Music » ne lance pas Groove.
* après la mise à jour précédente, la section « Go à l’origine » n’affiche pas correctement le panneau pin.

## <a name="introducing-microsoft-hololens-commercial-suite"></a>Présentation de Microsoft HoloLens commercial suite

Microsoft HoloLens commercial suite est prêt pour le déploiement d’entreprise. Nous avons ajouté plusieurs [fonctionnalités commerciales](commercial-features.md) très demandées auprès de nos premiers partenaires commerciaux.

Veuillez contacter votre gestionnaire de compte Microsoft local pour acheter la suite commerciale Microsoft HoloLens.

### <a name="key-commercial-features"></a>Principales fonctionnalités commerciales 

* **Mode plein écran.** Avec le mode plein écran HoloLens, vous pouvez limiter les applications à exécuter pour activer les expériences de démonstration ou de démonstration.<br>
  ![avec le mode plein écran, HoloLens démarre directement dans l’application de votre choix.](images/201608-kioskmode-400px.png)
* **Gestion des appareils mobiles (MDM) pour HoloLens.** Votre service informatique peut gérer plusieurs appareils HoloLens simultanément à l’aide de solutions telles que Microsoft Intune. Vous serez en mesure de gérer les paramètres, de sélectionner les applications à installer et de définir les configurations de sécurité adaptées aux besoins de votre entreprise.<br>
  ![la gestion des appareils mobiles sur HoloLens fournit une gestion des appareils de niveau entreprise sur plusieurs appareils.](images/201608-enterprisemanagement-400px.png)
* **Windows Update pour les entreprises.** Mises à jour contrôlées du système d’exploitation sur les appareils et prise en charge de la branche de maintenance à long terme.
* **Sécurité des données.** BitLocker Data Encryption est activé sur HoloLens pour fournir le même niveau de protection de sécurité qu’un autre appareil Windows.
* **Accès professionnel.** Toute personne de votre organisation peut se connecter à distance au réseau d’entreprise via un réseau privé virtuel sur un HoloLens. HoloLens peut également accéder aux réseaux Wi-Fi qui requièrent des informations d’identification.
* **Microsoft Store pour les entreprises.** Votre service informatique peut également configurer un magasin privé d’entreprise, contenant uniquement les applications de votre entreprise pour votre utilisation HoloLens spécifique. Distribuez en toute sécurité vos logiciels d’entreprise au groupe sélectionné d’utilisateurs d’entreprise.

### <a name="development-edition-vs-commercial-suite"></a>Édition Development et suite commerciale

<table>
<tr>
<th>Fonctionnalités</th><th>Édition Development</th><th>Suite commerciale</th>
</tr><tr>
<td>Chiffrement de l’appareil (BitLocker)</td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Réseau privé virtuel (VPN)</td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td><a href="using-the-windows-device-portal.md#kiosk-mode">Mode plein écran</a></td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<th colspan="3" style="text-align: left;"> Gestion et déploiement</th>
</tr><tr>
<td>Gestion des périphériques mobiles (GPM)</td><td style="text-align: center;"></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Possibilité de bloquer l’annulation de l’inscription</td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Accès Wi-Fi d’entreprise basé sur un certificat</td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Microsoft Store (consommateur)</td><td style="text-align: center;">Télévision</td><td style="text-align: center;">Filtrage via MDM</td>
</tr><tr>
<td><a href="https://technet.microsoft.com/itpro/windows/manage/working-with-line-of-business-apps">Portail Business Store</a></td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<th colspan="3" style="text-align: left;"> Sécurité et identité</th>
</tr><tr>
<td>Se connecter avec Azure Active Directory (AAD)</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Se connecter avec un compte Microsoft (MSA)</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Informations d’identification de prochaine génération avec déverrouillage du code confidentiel</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td><a href="https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/secure-boot-overview">Démarrage sécurisé</a></td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<th colspan="3" style="text-align: left;"> Maintenance et support</th>
</tr><tr>
<td>Mises à jour automatiques du système au fur et à mesure de leur arrivée</td><td style="text-align: center;">✔️</td><td style="text-align: center;">✔️</td>
</tr><tr>
<td><a href="https://technet.microsoft.com/itpro/windows/plan/windows-update-for-business">Windows Update pour les entreprises</a></td><td></td><td style="text-align: center;">✔️</td>
</tr><tr>
<td>Branche de maintenance à long terme</td><td></td><td style="text-align: center;">✔️</td>
</tr>
</table>

## <a name="prior-release-notes"></a>Notes de publication antérieures
* [Notes de publication - Mai 2016](release-notes-may-2016.md)
* [Notes de publication - Mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Articles associés
* [Problèmes connus concernant HoloLens](hololens-known-issues.md)
* [Fonctionnalités commerciales](commercial-features.md)
* [Installer les outils](install-the-tools.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
