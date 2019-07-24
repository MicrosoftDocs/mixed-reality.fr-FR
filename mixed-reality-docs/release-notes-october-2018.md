---
title: Notes de publication-octobre 2018
description: Notes de publication de HoloLens et de Windows Mixed Reality pour la mise à jour 2018 de Windows 10 octobre (également appelée RS5).
author: mattzmsft
ms.author: mazeller
ms.date: 10/02/2018
ms.topic: article
keywords: Notes de publication, version, Windows 10, Build, RS5, système d’exploitation
ms.openlocfilehash: 794050910be40e7f98d0a1f67c2e1cf6963305dd
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524255"
---
# <a name="release-notes---october-2018"></a>Notes de publication-octobre 2018

La **[mise à jour 2018 de Windows 10 octobre](https://blogs.windows.com/windowsexperience/2018/10/02/find-out-whats-new-in-windows-and-office-in-october/)** (également connue sous le nom de RS5) comprend de nouvelles fonctionnalités pour les casques immersif et Windows Mixed Real en réalité connectés aux PC. 

Pour effectuer une mise à jour vers la version la plus récente sur HoloLens ou PC (pour les casques en mode immersif Windows Mixed Reality), ouvrez l’application **paramètres** , accédez à **mettre à jour & sécurité**, puis sélectionnez le bouton **Rechercher les mises à jour** . Sur un PC Windows 10, vous pouvez également installer manuellement la mise à jour 2018 de Windows 10 octobre à l’aide de l' [outil de création de média Windows](https://www.microsoft.com/software-download/windows10).

**Dernière version pour ordinateur de bureau:** Mise à jour 2018 de Windows 10 octobre (**10.0.17763.107**)<br>
**Dernière version pour HoloLens:** Mise à jour 2018 de Windows 10 octobre (**10.0.17763.134**)<br>

## <a name="new-features-for-windows-mixed-reality-immersive-headsets"></a>Nouvelles fonctionnalités pour les casques immersifs de Windows Mixed Reality

La mise à jour 2018 d’octobre de Windows 10 offre de nombreuses améliorations pour l’utilisation des casques de Windows Mixed Reality (VR) avec votre PC de bureau.

### <a name="for-everyone"></a>Pour tout le monde

* Torche de la **réalité mixte** : ouvrez un portail dans le monde réel pour trouver votre clavier, consultez une personne à proximité ou examinez votre environnement sans supprimer votre casque! Vous pouvez activer le flash de la réalité mixte à partir du menu Démarrer, en appuyant sur Windows + attrape sur votre contrôleur de mouvement ou en disant «allumé/éteint». Pointez votre contrôleur dans la direction de ce que vous souhaitez voir, comme l’utilisation d’un torche dans l’obscurité.

    ![Torche de la réalité mixte](images/mr-flashlight.png)

* **Nouvelles applications et façons de lancer du contenu dans la réalité mixte**
    * Si vous utilisez [Windows Mixed Reality pour SteamVR](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/using-steamvr-with-windows-mixed-reality), vos titres SteamVR s’affichent désormais dans le menu Démarrer et les lanceurs d’applications de chaque peuvent être placés dans la page d’accueil de la réalité mixte.
    
        ![Lanceurs d’applications SteamVR](images/steamvr-launchers.png)
        
    * Nouvelle application *360 Video* pour découvrir une sélection régulièrement organisée de vidéos de 360 degrés.
    * Nouvelle application *WebVR Showcase* permettant de découvrir une sélection d’expériences WebVR régulièrement organisée.
    * Les clients Windows Mixed Really entrent dans la maison de la falaise et le trouvent préremplis avec les lanceurs d’applications en 3D pour certaines de nos applications et jeux immersifs favoris de la Microsoft Store.
    * Les fenêtres Microsoft Edge incluent maintenant un bouton *partager* .
* **Menu actions rapides** : à partir d’une application de réalité mixte immersive, vous pouvez appuyer sur le bouton Windows pour accéder à un nouveau menu actions rapides, avec un accès facile au *menu SteamVR*, à la *capture photo/vidéo*, à la torche et à la *page d’habitation*.
* **Prise en charge des PC de sac à dos** : les casques en immersion Windows Mixed Reality (VR) s’exécutent sur des PC de poche sans nécessiter d’émulateur d’affichage une fois l’installation terminée.
* **Nouvelles fonctionnalités audio** : vous pouvez désormais mettre en miroir le son à partir d’une expérience Windows Mixed Reality sur la prise jack audio (ou le casque) de votre casque *et* un périphérique audio connecté à votre PC (comme les haut-parleurs externes). Nous avons également ajouté un indicateur visuel pour le niveau du volume dans l’affichage de votre casque.
* **Autres améliorations**
    * Les mises à jour du portail de réalité mixte sont désormais fournies via le Microsoft Store, ce qui permet d’accélérer les mises à jour entre les versions majeures de Windows. Notez que cela s’applique uniquement à l’application de bureau et que l’expérience du casque Windows Mixed Reality est toujours mise à jour avec le système d’exploitation. 
    * Lorsque les casques sont en veille, les applications Windows Mixed Reality sont suspendues et non terminées (jusqu’à la fermeture du portail de réalité mixte).
    
### <a name="for-developers"></a>Pour les développeurs

* **[Suivi du code QR](qr-code-tracking.md)** -activer le suivi du code QR dans votre application de réalité mixte, ce qui permet aux casques de Windows Mixed Reality (VR) d’analyser les codes QR et de les renvoyer aux applications intéressées.
* **Prise en charge de la DRM matérielle pour les applications immersives** : les développeurs peuvent désormais demander des textures de mémoire tampon en mémoire tampon de matériel si elles sont prises en charge par le matériel d’affichage, ce qui permet aux applications d’utiliser du contenu protégé par le matériel provenant de sources telles que PlayReady
* **[Intégration de l’interface utilisateur de capture de réalité mixte dans des applications immersifs](mixed-reality-capture-for-developers.md#integrating-mrc-functionality-from-within-your-app)** : les développeurs peuvent intégrer la capture de réalité mixte dans leurs applications à l’aide de l' [interface utilisateur de capture](https://docs.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-cameracaptureui) de la caméra Windows intégrée avec quelques lignes de code.

## <a name="new-features-for-hololens"></a>Nouvelles fonctionnalités de HoloLens

La mise à jour 2018 de Windows 10 octobre est publiquement disponible pour tous les clients HoloLens et comprend un certain nombre d’améliorations, telles que:

### <a name="for-everyone"></a>Pour tout le monde

* **Menu actions rapides** : à partir d’une application de réalité mixte immersive, vous pouvez appuyer sur le bouton Windows pour accéder à un nouveau menu actions rapides, avec un accès facile pour *Démarrer l’enregistrement vidéo*, *prendre des photos*, accueil de la *réalité mixte*, *changer volume*et *Connectez-vous*.
* **Démarrer/arrêter la capture vidéo à partir du menu actions de démarrage ou rapide** : Si vous démarrez la capture vidéo à partir du menu Démarrer ou du menu actions rapides, vous pouvez arrêter l’enregistrement à partir du même emplacement. (N’oubliez pas que vous pouvez toujours le faire avec les commandes vocales.)
* **Projet sur un appareil compatible Miracast** -projetez votre contenu HoloLens sur un appareil à surface proche ou une TV/moniteur si vous utilisez un adaptateur ou un écran compatible miracast.
* **Nouvelles notifications** : Affichez et répondez aux notifications sur HoloLens, comme vous le feriez sur un PC.  
* **Superpositions utiles dans les applications de réalité mixte immersif** : vous verrez maintenant des superpositions telles que le clavier, les boîtes de dialogue, le sélecteur de fichiers, etc. lors de l’utilisation d’applications de réalité mixte immersives.
* **Indicateur visuel pour la modification de volume** -quand vous utilisez les boutons monter/descendre en volume dans votre HoloLens, vous verrez un indicateur visuel du niveau du volume dans le casque.
* **Nouveaux éléments visuels pour le démarrage de l’appareil** : un indicateur de chargement a été ajouté pendant le processus de démarrage pour fournir des commentaires visuels sur le chargement du système.
* **Partage proche** : l’expérience de partage Windows à proximité vous permet de partager une capture avec un appareil Windows proche.  
* **Partager à partir de Microsoft Edge** : Microsoft Edge comprend désormais un bouton *partager* . 

### <a name="for-developers"></a>Pour les développeurs

* **[Intégration de l’interface utilisateur de capture de réalité mixte dans des applications immersifs](mixed-reality-capture-for-developers.md#integrating-mrc-functionality-from-within-your-app)** : les développeurs peuvent intégrer la capture de réalité mixte dans leurs applications à l’aide de l' [interface utilisateur de capture](https://docs.microsoft.com/windows/uwp/audio-video-camera/capture-photos-and-video-with-cameracaptureui) de la caméra Windows intégrée avec quelques lignes de code.

### <a name="for-commercial-customers"></a>Pour les clients commerciaux

* **Activer l’approvisionnement après l’installation** : vous pouvez maintenant appliquer un package de configuration du runtime à tout moment à l’aide des paramètres.
* **Accès affecté avec les groupes de Azure ad** : vous pouvez désormais utiliser des groupes de Azure AD pour la configuration de l’accès affecté à Windows pour configurer la configuration d’un kiosque à une ou plusieurs applications.
* Épingler la connexion **sur le commutateur de profil à partir de l’écran** de connexion: la connexion du code confidentiel est maintenant disponible pour «autre utilisateur» dans l’écran de connexion. 
* **Lire les informations matérielles de l’appareil via MDM** -les administrateurs informatiques peuvent voir et suivre HoloLens par numéro de série de l’appareil dans leur console MDM.
* **Définir le nom de l’appareil hololens via MDM (Rename)** : les administrateurs informatiques peuvent voir et renommer des appareils hololens dans leur console MDM.

### <a name="for-international-customers"></a>Pour les clients internationaux

Vous pouvez maintenant utiliser HoloLens avec une interface utilisateur localisée pour le chinois simplifié ou le japonais, y compris le clavier pinyin localisé, la dictée, la conversion de texte par synthèse vocale (TTS) et les commandes vocales.

## <a name="known-issues"></a>Problèmes connus

Nous avons travaillé dur pour offrir une expérience Windows Mixed Reality exceptionnelle, mais nous effectuons toujours le suivi de certains problèmes connus. Si vous en trouvez d’autres, faites [-nous part de vos commentaires](https://docs.microsoft.com/windows/mixed-reality/give-us-feedback).

### <a name="hololens"></a>HoloLens
 
#### <a name="after-update"></a>Après la mise à jour
Vous pouvez remarquer les problèmes suivants lors de l’utilisation de la mise à jour 2018 de Windows 10 octobre sur votre HoloLens:
* **Les applications peuvent se retrouver dans une boucle de connexion lorsqu’elles sont lancées à partir d’une notification** : certaines applications nécessitant une connexion peuvent se retrouver dans une boucle de connexion sans fin lorsqu’elles sont lancées à partir d’une notification. Par exemple, cela peut se produire après l’installation de l’application Microsoft Portail d’entreprise à partir du Microsoft Store et son lancement à partir de la notification d’installation terminée.
* La **page de connexion de l’application peut s’exécuter avec une page vierge** : dans certains cas, lorsqu’une invite de connexion s’affiche sur votre application, à la fin, la page de connexion ne se ferme pas et affiche une page vide (noire). Vous pouvez fermer la page vide ou la déplacer pour dévoiler l’application ci-dessous. Par exemple, cela peut se produire lors de la connexion lors de l’inscription MDM à partir de l’application paramètres. 

## <a name="provide-feedback-and-report-issues"></a>Fournir des commentaires et signaler des problèmes

Utilisez l' [application Hub de commentaires sur votre PC HoloLens ou Windows 10](give-us-feedback.md) pour fournir des commentaires et signaler des problèmes. L’utilisation de feedback Hub garantit que toutes les informations de diagnostic nécessaires sont incluses pour aider nos ingénieurs à déboguer et résoudre rapidement le problème.

>[!NOTE]
>Veillez à accepter l’invite qui vous demande si vous souhaitez que le hub de commentaires accède à votre dossier documents (sélectionnez **Oui** lorsque vous y êtes invité).

## <a name="prior-release-notes"></a>Notes de publication antérieures

* [Notes de publication - Avril 2018](release-notes-april-2018.md)
* [Notes de publication - Octobre 2017](release-notes-october-2017.md)
* [Notes de publication - Août 2016](release-notes-august-2016.md)
* [Notes de publication - Mai 2016](release-notes-may-2016.md)
* [Notes de publication - Mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Prise en charge des casques immersifs (lien externe)](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality)
* [Prise en charge de HoloLens (lien externe)](https://support.microsoft.com/products/hololens)
* [Installer les outils](install-the-tools.md)
* [Nous envoyer vos commentaires](give-us-feedback.md)

