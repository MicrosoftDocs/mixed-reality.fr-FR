---
title: Notes de publication-mai 2016
description: Les notes de publication HoloLens pour Windows holographique peuvent être mises à jour 2016.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, notes de publication, système d’exploitation, fonctionnalités, Build, plateforme
ms.openlocfilehash: bc4e09c36a3ab6643be1144873a624fc5ed66e37
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524574"
---
# <a name="release-notes---may-2016"></a>Notes de publication-mai 2016

L’équipe HoloLens s’engage à vous fournir une mise à jour de nos derniers développements de fonctionnalités et de correctifs principaux par le biais du programme Windows Insider. Grâce à toutes vos suggestions, nous prenons vos commentaires à coeur. Continuez à [nous faire part de vos commentaires](give-us-feedback.md) via le hub de commentaires, les [Forums des développeurs](https://forums.hololens.com) et [Twitter via @HoloLens ](https://twitter.com/hololens).

**Version Release:** Windows holographique mai 2016 mise à jour (**10.0.14342.1016**)

>[!VIDEO https://www.youtube.com/embed/XM5OHHrOGqQ]

Pour effectuer une mise à jour vers la version actuelle, ouvrez l’application *paramètres* , accédez à *mettre à jour & sécurité*, puis sélectionnez le bouton *Rechercher les mises à jour* .

## <a name="new-features"></a>Nouvelles fonctionnalités

* Vous pouvez désormais **Exécuter jusqu’à trois applications en mode 2D simultanément**. Cela permet des cas d’utilisation infinis pour le multitâche dans HoloLens. Utilisez le nouveau hub de commentaires avec la liste des quests ouverte tout en explorant les nouvelles fonctionnalités de ce vol.

  ![HoloLens peut exécuter trois applications en même temps](images/img-3625-400px.jpg)<br>
  Exécuter jusqu’à trois applications en mode 2D simultanément

* Nous avons ajouté de nouvelles **commandes vocales**:
   * Essayez d’examiner un hologramme et de le faire pivoter en disant «Facer»
   * Modifiez sa taille en disant «plus grande» ou «plus petite»
   * Déplacez une application en disant «Hey Cortana, déplacer le nom de l' *application* ici».
* Nous avons **facilité le développement de HoloLens**. Vous pouvez maintenant parcourir, télécharger et télécharger des fichiers via le [portail des appareils Windows](using-the-windows-device-portal.md). Vous pouvez accéder au dossier documents, au dossier images et au stockage local pour toutes les applications que vous avez chargées ou déployées par le biais de Visual Studio.
* L' **émulateur prend maintenant en charge la connexion avec un compte Microsoft** comme vous le feriez sur un HoloLens réel. Vous pouvez l’activer à partir du menu outils supplémentaires «> >».
* **les applications 2D masquent désormais la barre et le curseur de l’application lorsque vous regardez la vidéo en mode plein écran** pour éviter toute distraction. Avec cela, votre expérience de visionnage vidéo sera encore plus agréable sur HoloLens.
* Vous pouvez également **Épingler des photos sans la barre de l’application** dans votre monde.

  ![La barre de l’application peut être masquée pour les applications 2D comme les photos](images/img-3626-400px.jpg)<br>
  La barre de l’application peut être masquée pour les applications avec une vue 2D, comme les photos
  
* Le sélecteur de fichier fonctionne comme s’il s’agissait d’un **Sélecteur de fichiers** sur HoloLens.
* **Navigateur Edge** mis à jour pour mapper l’expérience utilisateur unifiée avec le bureau et le téléphone. Nous avons activé plusieurs instances de votre navigateur, une page de nouvel onglet HoloLens personnalisée, une lecture à onglets et une ouverture dans de nouvelles fenêtres, ainsi que des améliorations des performances de Power &.
* L’application **Groove Music** est maintenant sur HoloLens. Visitez le Store pour le télécharger et essayez de vous lancer en arrière-plan.
* Vous pouvez facilement personnaliser la disposition des applications dans votre monde. Essayez de faire **pivoter vos hologrammes** en mode d’ajustement simplement en cliquant et en faisant glisser le cercle dans le milieu vertical des maquettes. Vous remarquerez peut-être que les hologrammes disposent de **zones englobantes** plus étroites pour garantir une interaction agrandie. Vous pouvez également redimensionner toutes les applications plates verticalement (à l’exception des photos et des applications d’hologramme).

  ![Vous pouvez faire pivoter les hologrammes une fois que vous les avez placés dans le monde](images/img-3627-400px.jpg)<br>
  Faites pivoter les hologrammes après les avoir placés dans le monde entier

* Nous avons apporté de nombreuses améliorations en matière de **saisie** dans ce vol. Vous pouvez connecter une souris Bluetooth normale à HoloLens. Le clic a été ajusté pour permettre le redimensionnement & des hologrammes avec un clic. Le clavier fonctionne également mieux que jamais.
* Vous pouvez désormais utiliser des **images de réalité mixte** en appuyant simplement sur la touche Monter le volume + volume. Vous pouvez également partager vos photos & des vidéos capturées en réalité mixte sur Facebook, Twitter et YouTube.
* La durée d’enregistrement maximale des **vidéos de réalité mixte** a été augmentée à cinq minutes.
* L' **application photos** diffuse désormais des vidéos à partir de OneDrive au lieu de télécharger l’intégralité de la vidéo avant la lecture.
* Nous avons amélioré la façon dont vos **hologrammes seront bons à l’endroit où vous les avez laissés**. Vous serez également invité à vous reconnecter au Wi-Fi et réessayer si HoloLens ne parvient pas à détecter son emplacement.
* Le clavier offre une **mise en page améliorée pour la saisie de l’adresse e-mail** avec des clés qui vous permettent d’entrer les domaines de messagerie les plus populaires en un seul clic.
* **Inscription d’application** plus rapide et **détection automatique du fuseau horaire** pendant l’OOBE, ce qui vous offre la meilleure expérience utilisateur.
* Le **sens du stockage** vous permet d’afficher l’espace disque restant et utilisé par le système et les applications dans l’application paramètres.
* Nous disposons d’une application de commentaires convergée dans un concentrateur de **Commentaires** sur une application unique qui sera l’outil incontournable pour nous faire **part de vos commentaires**, les fonctionnalités que vous aimez, les fonctionnalités que vous pourriez faire sans, ou quand un résultat peut être amélioré. Quand vous rejoignez le programme Insider, vous pouvez suivre les **dernières nouvelles**de l’Insider, **évaluer** les builds et vous rendre sur les **Commentaires** de votre Hub de commentaires.
* Nous avons également [publié une build d’émulateur HoloLens mise à jour](install-the-tools.md) .
* Vos vidéos de réalité mixte s’affichent désormais mieux en raison d’une **stabilisation vidéo**automatique.

## <a name="major-fixes"></a>Correctifs principaux

Nous avons résolu les problèmes avec les espaces d’hologramme où les espaces seraient lents ou détectés de manière incorrecte. Nous avons résolu un problème d’arrêt qui pouvait continuer à essayer de lancer le shell pendant l’arrêt.

Nous avons résolu un problème
* cela bloque la possibilité de reprendre une application XAML.
* Lorsqu’un incident laisse un écran noir et des lignes en escalier.
* le défilement se bloquerait parfois dans la mauvaise direction lors de l’utilisation de certaines applications.
* les voyants d’alimentation peuvent indiquer un état désactivé lorsque l’appareil est toujours allumé.
* Le WiFi peut être désactivé après la reprise de la mise en veille.
* le fournisseur d’identité Xbox offre une configuration d’identité, puis est bloqué dans une boucle.
* l’interpréteur de commandes se bloque parfois lors de la sélection d’un fichier téléchargé dans le sélecteur de fichiers OneDrive.
* Quand vous appuyez sur un lien et que vous le maintenez, les deux ouvrent parfois un nouvel onglet rompu et ouvre un menu contextuel.
* où le portail de périphériques Windows n’autorise pas les réglages IPD de 50 à 80

Nous avons résolu les problèmes liés aux photos où
* une image peut parfois être pivotée en raison de l’ignorance de la propriété d’orientation EXIF.
* elle peut se bloquer lors du démarrage sur des photos épinglées.
* les vidéos redémarreront après une pause au lieu de reprendre là où elle a été suspendue.
* la relecture d’une vidéo partagée peut être empêchée si elle était partagée pendant la lecture.
* Les enregistrements de capture de réalité mixte commencent par 0,5-1 seconde du flux audio uniquement.
* le bouton de synchronisation disparaît pendant la synchronisation OneDrive initiale.

Nous avons résolu les problèmes liés aux paramètres où
* une actualisation était nécessaire lors de la modification de l’environnement.
* La touche entrée du clavier ne se comporte pas comme si vous cliquiez sur suivant dans certaines boîtes de dialogue.
* il était difficile de savoir quand le coupleur a échoué.
* Il peut cesser de répondre avec WiFi Disconnect et Connect.

Nous avons résolu les problèmes avec Cortana là où
* Il peut être bloqué en affichant l’interface utilisateur d’écoute.
* Si vous avez répondu à la demande «Hey Cortana, que puis-je prononcer» à partir d’une application en mode exclusif, vous avez peut-être bloqué la demande pour quitter l’application.
* l’interface utilisateur d’écoute Cortana ne reprend pas correctement si vous demandez à Cortana de passer en mode veille et de reprendre.
* les requêtes «quel réseau suis-je connecté?» et «suis-je connecté?» peut échouer lorsque le premier profil réseau est rétabli sans connectivité.
* l’interface utilisateur figée sur «Listening», mais à la sortie d’une application a immédiatement commencé la reconnaissance vocale.
* Si la déconnexion de l’application Cortana ne vous permet pas de vous reconnecter jusqu’à un redémarrage.
* elle n’est pas lancée lorsque l’interface utilisateur de capture de la réalité mixte était active.

Nous avons résolu les problèmes liés à Visual Studio où
* le débogage des tâches en arrière-plan n’a pas été effectué.
* l’analyse des frames du débogueur Graphics ne fonctionne pas.
* l’émulateur HoloLens n’apparaissait pas dans la liste déroulante de Visual Studio, sauf si TargetPlatformVersion de votre projet a été défini sur 10240.

## <a name="changes-from-previous-release"></a>Modifications par rapport à la version précédente
* La commande Cortana **Hey Cortana, redémarrage de l’appareil** ne fonctionne pas. L’utilisateur peut indiquer **Hey Cortana, redémarrer** ou **Hey Cortana, redémarrer l’appareil**.
* Le mode plein écran a été supprimé du produit.

## <a name="prior-release-notes"></a>Notes de publication antérieures
* [Notes de publication - Mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Problèmes connus concernant HoloLens](hololens-known-issues.md)
* [Installer les outils](install-the-tools.md)
* [Shell](navigating-the-windows-mixed-reality-home.md)
* [Mise à jour des applications UWP 2D pour la réalité mixte](building-2d-apps.md)
* [Accessoires matériels](hardware-accessories.md)
* [Capture de Réalité Mixte](mixed-reality-capture.md)
* [Entrée vocale](voice-input.md)
* [Envoi d’une application au Windows Store](submitting-an-app-to-the-microsoft-store.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
