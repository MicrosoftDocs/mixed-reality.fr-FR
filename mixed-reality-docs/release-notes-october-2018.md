---
title: Notes de publication-octobre 2018
description: HoloLens et notes de publication Windows Mixed Reality pour Windows 10 octobre 2018 mettre à jour (également appelé RS5).
author: mattzmsft
ms.author: mazeller
ms.date: 10/02/2018
ms.topic: article
keywords: Release notes, version, windows 10, build, rs5, système d’exploitation
ms.openlocfilehash: 9838b4dcbdedc4bf2c94a8e31f3f8eb4c9634d36
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596730"
---
# <a name="release-notes---october-2018"></a>Notes de publication-octobre 2018

Le **[Windows 10 octobre 2018 Update](https://blogs.windows.com/windowsexperience/2018/10/02/find-out-whats-new-in-windows-and-office-in-october/)** (également appelé RS5) inclut de nouvelles fonctionnalités pour HoloLens et Windows Mixed Reality des casques IMMERSIFS connectés au PC. 

Pour mettre à jour vers la dernière version sur PC ou HoloLens (pour les casques (VR) IMMERSIFS Windows Mixed Reality), ouvrez le **paramètres** application, accédez à **mise à jour & sécurité**, puis sélectionnez le **recherchez mises à jour** bouton. Sur un PC Windows 10, vous pouvez également installer manuellement Windows 10 octobre 2018 mettre à jour à l’aide de la [outil de création de Windows media](https://www.microsoft.com/software-download/windows10).

**Version la plus récente pour le bureau :** Mise à jour de Windows 10 octobre 2018 (**10.0.17763.107**)<br>
**Version la plus récente pour HoloLens :** Mise à jour de Windows 10 octobre 2018 (**10.0.17763.134**)<br>

## <a name="new-features-for-windows-mixed-reality-immersive-headsets"></a>Nouvelles fonctionnalités pour les casques IMMERSIFS Windows Mixed Reality

Windows 10 octobre 2018 mise à jour comprend de nombreuses améliorations pour l’utilisation des casques Windows Mixed Reality IMMERSIFS (VR) avec votre ordinateur de bureau.

### <a name="for-everyone"></a>Pour tout le monde

* **Mixte réalité torche** : ouvrir un portail dans le monde réel pour trouver votre clavier, de voir des personnes à proximité, ou un œil à votre environnement sans supprimer votre casque ! Vous pouvez activer torche de réalité mixte dans le menu Démarrer, en appuyant sur Windows + manipulation sur votre contrôleur de mouvement, ou en disant « Torche activé/désactivé. » Pointez votre contrôleur dans la direction de ce que vous souhaitez afficher, comme à l’aide d’une torche dans l’obscurité.

    ![Réalité mixte torche](images/mr-flashlight.png)

* **Nouvelles applications et les moyens de lancer le contenu dans la réalité mixte domestique**
    * Si vous utilisez [Windows Mixed Reality pour SteamVR](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/using-steamvr-with-windows-mixed-reality), vos titres SteamVR affichent désormais dans le menu Démarrer et lanceurs d’applications pour chacun peuvent être placés dans la réalité mixte domestique.
    
        ![Lanceurs d’applications SteamVR](images/steamvr-launchers.png)
        
    * Nouvelle *360 vidéos* application pour découvrir une sélection régulièrement organisée de vidéos de 360 degrés.
    * Nouvelle *WebVR Showcase* expériences d’application pour découvrir une sélection régulièrement organisée de WebVR.
    * Clients de Windows Mixed Reality première Entrez le Cliff House et trouver qu'il rempli au préalable avec les lanceurs d’applications 3D pour certaines de nos applications immersives favorites et de jeux à partir du Microsoft Store.
    * Windows de Microsoft Edge incluent désormais un *partage* bouton.
* **Menu actions rapides** -à partir d’une application de réalité mixte immersives, vous pouvez appuyer sur le bouton Windows d’accéder à un nouveau menu actions rapides, avec un accès facile aux *SteamVR menu*, *capture photo/vidéo*, *torche*, et *domestique*.
* **Prise en charge de sac à DOS PC** -Windows Mixed Reality des casques IMMERSIFS (VR) exécutant sur sac à DOS PC sans procéder un émulateur d’affichage une fois que le programme d’installation est terminée.
* **Nouvelles fonctionnalités audio** -vous pouvez désormais refléter l’audio à partir d’une expérience de réalité mixte Windows pour les deux jack audio (ou un casque) dans votre casque *et* un périphérique audio est connecté à votre PC (par exemple, les haut-parleurs externes). Nous avons également ajouté un indicateur visuel pour le niveau de volume dans l’affichage de votre casque.
* **Autres améliorations**
    * Mises à jour de portail de réalité mixtes sont désormais remis via le Microsoft Store, l’activation des mises à jour plus rapides entre les versions majeures de Windows. Notez que cela s’applique uniquement à l’application de bureau et l’expérience de casque Windows Mixed Reality toujours met à jour avec le système d’exploitation. 
    * Lorsque les casques se mettre en veille, les applications de réalité mixte Windows sont suspendues au lieu de fin (tant que portail de réalité mixte est fermé).
    
### <a name="for-developers"></a>Pour les développeurs

* **[Code QR suivi](qr-code-tracking.md)**  -code QR d’activer le suivi des modifications dans votre application de réalité mixte, ce qui permet des casques Windows Mixed Reality IMMERSIFS (VR) Rechercher les codes QR et les signaler revenir à des applications concernées.
* **Matériel DRM prennent en charge pour les applications immersives** -les développeurs peuvent les textures de mémoire tampon d’arrière-plan matériel protégé demande maintenant si pris en charge par le matériel d’affichage, permettant aux applications d’utiliser le contenu protégé par le matériel à partir de sources telles que PlayReady.
* **[Interface utilisateur de capture de réalité mixte intégrer des applications immersives](mixed-reality-capture-for-developers.md#integrating-mrc-functionality-from-within-your-app)**  -les développeurs peuvent intégrer la capture de réalité mixte dans leurs applications à l’aide de la Windows intégrés [interface utilisateur de capture photo](https://docs.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-cameracaptureui) avec seulement quelques lignes de code.

## <a name="new-features-for-hololens"></a>Nouvelles fonctionnalités pour HoloLens

Le 10 octobre 2018 de Windows Update est publiquement disponible pour tous les clients de HoloLens et inclut un certain nombre d’améliorations, telles que :

### <a name="for-everyone"></a>Pour tout le monde

* **Menu actions rapides** -à partir d’une application de réalité mixte immersives, vous pouvez appuyer sur le bouton Windows d’accéder à un nouveau menu actions rapides, avec un accès facile aux *démarrer l’enregistrement vidéo*, *prendre des photos*, *Accueil de réalité mixte*, *modifier le volume*, et *Connect*.
* **Démarrer/arrêter la capture vidéo à partir du début ou du menu actions rapides** -si vous démarrez la capture vidéo à partir du menu Démarrer ou du menu actions rapides, vous serez en mesure d’arrêter l’enregistrement à partir de la même place. (N’oubliez pas que vous pouvez toujours faire avec les commandes vocales trop.)
* **Projet pour un appareil miracast** -votre contenu HoloLens à un périphérique de la surface d’exposition proche ou TV/analyse de projet si vous utilisez un moniteur compatible ou un adaptateur.
* **Nouvelles notifications** -vue et réagir aux notifications sur HoloLens, comme vous le feriez sur un PC.  
* **Les superpositions utiles dans les applications immersives de réalité mixte** -vous voyez désormais superpositions tels que le clavier, les boîtes de dialogue de sélecteur de fichiers, etc. lors de l’utilisation immersive des applications de réalité mixte.
* **Indicateur visuel pour la modification de volume** : quand vous utilisez le volume / vers le bas de boutons sur votre HoloLens, vous verrez un indicateur visuel du niveau de volume dans le casque.
* **Nouveaux éléments visuels pour le démarrage de l’appareil** -un indicateur de chargement a été ajouté pendant le processus de démarrage pour fournir des commentaires visuels le système en cours de chargement.
* **À proximité de partage** -expérience de partage à proximité de la Windows vous permet de partager une capture avec un appareil Windows à proximité.  
* **Partage à partir de Microsoft Edge** -Microsoft Edge inclut désormais un *partage* bouton. 

### <a name="for-developers"></a>Pour les développeurs

* **[Interface utilisateur de capture de réalité mixte intégrer des applications immersives](mixed-reality-capture-for-developers.md#integrating-mrc-functionality-from-within-your-app)**  -les développeurs peuvent intégrer la capture de réalité mixte dans leurs applications à l’aide de la Windows intégrés [interface utilisateur de capture photo](https://docs.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-cameracaptureui) avec seulement quelques lignes de code.

### <a name="for-commercial-customers"></a>Pour les clients commerciaux

* **Activer la configuration de post-installation** -vous pouvez maintenant appliquer un package de configuration à tout moment à l’aide des paramètres d’exécution.
* **Affecter l’accès avec les groupes Azure AD** -vous pouvez maintenant utiliser des groupes Azure AD pour la configuration de Windows l’accès attribué à pour définir la configuration d’unique ou des applications multiples plein écran.
* **ÉPINGLER connectez-vous sur le commutateur de profil à partir de l’écran de connexion** -connectez-vous du code confidentiel est désormais disponible pour « Un autre utilisateur » à l’écran de connexion. 
* **Connectez-vous avec le fournisseur d’informations d’identification Web à l’aide du mot de passe** -vous pouvez maintenant sélectionner cette icône pour lancer web connectez-vous avec votre mot de passe. 
* **Lire des informations sur le périphérique matériel via MDM** -les administrateurs informatiques peuvent voir et suivre HoloLens par numéro de série d’appareil dans leur console de gestion des appareils mobiles.
* **Définir le nom de l’appareil HoloLens via MDM (renommer)** -les administrateurs informatiques peuvent voir et renommer les appareils HoloLens dans leur console de gestion des appareils mobiles.

### <a name="for-international-customers"></a>Pour les clients internationaux

Vous pouvez maintenant utiliser HoloLens avec interface utilisateur localisée pour le chinois simplifié ou le japonais, y compris le clavier Pinyin localisé, la dictée, TTS (Text) et les commandes vocales.

## <a name="known-issues"></a>Problèmes connus

Nous avons travaillé dur pour fournir une excellente expérience de réalité mixte Windows, mais nous sommes toujours le suivi des problèmes connus. Si vous trouvez d’autres, veuillez [envoyez-nous vos commentaires](https://docs.microsoft.com/windows/mixed-reality/give-us-feedback).

### <a name="hololens"></a>HoloLens
 
#### <a name="after-update"></a>Après mise à jour
Vous pouvez remarquer les problèmes suivants lors de l’aide de Windows 10 octobre 2018 mise à jour sur votre HoloLens :
* **Les applications peuvent arriver dans connexion boucle lorsque lancée à partir d’une notification** – certaines applications nécessitant une connexion peuvent fin à distance dans une boucle sans fin connectez-vous lorsque lancée à partir d’une notification. Par exemple, cela peut se produire après l’installation de l’application portail d’entreprise Microsoft à partir du Microsoft Store et en le lançant à partir d’une notification complète de l’installation.
* **Page de connexion de l’application peut se terminer avec une page vierge** : dans certains cas lors d’une invite de connexion présente sur votre application, à la fin de la page de connexion ne ferme pas et affiche à la place une page vierge (noire). Vous pouvez fermer la page vierge ou déplacez-le pour découvrir l’application en dessous. Par exemple, cela peut se produire lors de la connexion lors de l’inscription de gestion des appareils mobiles à partir de l’application paramètres. 

## <a name="provide-feedback-and-report-issues"></a>Fournir des commentaires et signalez les problèmes

Utilisez le [application Hub de commentaires sur votre PC Windows 10 ou sur HoloLens](give-us-feedback.md) pour fournir des commentaires et signalez les problèmes. À l’aide du Hub de commentaires garantit que toutes les informations de diagnostic nécessaire sont incluses pour aider à nos ingénieurs déboguer rapidement et de résoudre le problème.

>[!NOTE]
>Veillez à accepter l’invite vous demandant si vous souhaitez que le Hub de commentaires pour accéder à votre dossier Documents (sélectionnez **Oui** lorsque vous y êtes invité).

## <a name="prior-release-notes"></a>Notes de version antérieure

* [Notes de publication-avril 2018](release-notes-april-2018.md)
* [Notes de publication-octobre 2017](release-notes-october-2017.md)
* [Notes de publication-août 2016](release-notes-august-2016.md)
* [Notes de publication-mai 2016](release-notes-may-2016.md)
* [Notes de publication-mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Prise en charge de casque immersive (lien externe)](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality)
* [Prise en charge de HoloLens (lien externe)](https://support.microsoft.com/products/hololens)
* [Installer les outils](install-the-tools.md)
* [Envoyez-nous vos commentaires](give-us-feedback.md)

