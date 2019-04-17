---
title: Notes de publication-mai 2016
description: HoloLens les notes de publication pour Windows Holographic 2016 peuvent mettre à jour.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, notes de publication, du système d’exploitation, fonctionnalités, build, plateforme
ms.openlocfilehash: bc4e09c36a3ab6643be1144873a624fc5ed66e37
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596454"
---
# <a name="release-notes---may-2016"></a>Notes de publication-mai 2016

L’équipe HoloLens s’engage à vous fournir une mise à jour sur notre développement des dernières fonctionnalités et les principaux correctifs via le programme Insider de Windows. Je remercie toutes vos suggestions, nous prenons vos commentaires à cœur. Continuez à [envoyez-nous vos commentaires](give-us-feedback.md) via le Hub de commentaires, la [forums de développeurs](https://forums.hololens.com) et [Twitter via @HoloLens ](https://twitter.com/hololens).

**Version Release :** Mise à jour de Windows HOLOGRAPHIQUE mai 2016 (**10.0.14342.1016**)

>[!VIDEO https://www.youtube.com/embed/XM5OHHrOGqQ]

Pour mettre à jour vers la version actuelle, ouvrez le *paramètres* application, accédez à *mise à jour & sécurité*, puis sélectionnez le *vérifier les mises à jour* bouton.

## <a name="new-features"></a>Nouvelles fonctionnalités

* Vous pouvez à présent **exécuter simultanément des applications jusqu'à trois dans la vue 2D**. Ainsi, les cas d’utilisation illimitées pour le multitâche dans HoloLens. Avoir le nouveau Hub de commentaires avec la liste des quêtes ouverts lors de l’exploration des nouvelles fonctionnalités sur ce vol.

  ![HoloLens pouvez exécutez trois applications en même temps](images/img-3625-400px.jpg)<br>
  Exécuter simultanément des applications jusqu'à trois dans la vue 2D

* Nous avons ajouté de nouveaux **commandes vocales**:
   * Essayez d’examiner un hologramme et faire pivoter en disant « face me »
   * Modifier sa taille en disant « supérieure » ou « plus petit »
   * Déplacer une application en disant « Hey Cortana, déplacer *nom de l’application* ici. »
* Nous avons apporté **développement sur HoloLens plus facile**. Vous pouvez maintenant parcourir, charger et télécharger des fichiers via le [Windows Device Portal](using-the-windows-device-portal.md). Vous pouvez accéder le dossier Documents, dossier images et le stockage local pour n’importe quelle application que vous avez chargées ou déployé via Visual Studio.
* Le **émulateur prend désormais en charge connectez-vous avec un Account Microsoft** comme vous le feriez sur un véritable HoloLens. Vous pouvez activer cette option dans le menu Outils supplémentaires « >> ».
* **Applications 2D maintenant masquent la barre de l’application et le curseur lorsque vous regardez la vidéo en plein écran** afin d’éviter de vous laisser distraire par. Avec cela, votre expérience regarder la vidéo sera encore plus agréable sur HoloLens.
* Vous pouvez également **épingler des photos sans la barre des applications** dans votre monde.

  ![La barre d’application peut être masquée pour les applications 2D comme des photos](images/img-3626-400px.jpg)<br>
  La barre d’application peut être masquée pour les applications avec une vue en 2D, comme des Photos
  
* **Sélecteur de fichiers** fonctionne comme prévu sur HoloLens.
* Mise à jour **navigateur Edge** pour mapper l’expérience utilisateur unifiées avec le bureau et téléphone. Nous avons activé plusieurs instances de votre navigateur, personnalisé HoloLens nouvelle page d’onglets, aperçu de l’onglet, puis ouvrir dans de nouvelles fenêtres, ainsi que des améliorations d’alimentation et de performances.
* **Groove musique** application est maintenant sur HoloLens. Visitez les magasins pour le télécharger et essayez de lire en arrière-plan.
* Vous pouvez facilement personnaliser la façon dont les applications sont organisées dans votre monde. Essayez **faire pivoter votre hologrammes** en ajuster le mode par simple clic et faites glisser sur le cercle dans les modèles filaires de verticales du milieu. Vous remarquerez peut-être hologrammes ont **plus forte montée de zones englobantes** pour garantir une interaction agrandie. Vous pouvez également redimensionner toutes les applications plates verticalement (à l’exception des Photos et hologramme applications).

  ![Hologrammes peuvent pivoter une fois que vous les placez dans le monde](images/img-3627-400px.jpg)<br>
  Faire pivoter hologrammes une fois que vous les placez dans le monde

* Nous avons apporté de nombreuses **d’entrée amélioration** dans ce vol. Vous pouvez connecter une souris Bluetooth à HoloLens. Le clicker a été réglé pour activer le redimensionnement de & mander hologrammes avec un clicker. Clavier est également en cours d’exécution plu que jamais.
* Maintenant que vous pouvez prendre **mixte des images de réalité** en appuyant simplement sur bas le monter le volume + baisser le volume simultanément. Vous pouvez également partager vos photos de réalité mixte capturée et les vidéos à Facebook, Twitter et YouTube.
* La longueur maximale d’enregistrement de **mixte des vidéos de réalité** a été augmentée à cinq minutes.
* **Application de photos** diffuse désormais des vidéos à partir de OneDrive au lieu de devoir télécharger la vidéo entière avant la lecture.
* Nous avons amélioré comment votre **hologrammes seront en droit où vous les avez laissées**. Vous obtenez également l’option pour rétablir la connexion Wi-Fi et recommencez l’opération si HoloLens ne peut pas détecter lorsqu’elles sont.
* Le clavier a un **disposition améliorée permettant d’entrer l’adresse de messagerie** avec des clés qui vous permettent d’entrer l’e-mail populaire cliquez sur les domaines avec un seul.
* Plus rapidement **inscription d’application** et **auto détection du fuseau horaire** pendant la phase OOBE, ce qui vous donne le premier utilisateur meilleure expérience.
* **Logique de stockage** vous permet d’afficher l’espace de disque restant et utilisé par le système et les applications dans l’application paramètres.
* Nous avons convergé application de commentaires et à l’intérieur d’un Hub dans une seule application **Hub de commentaires** qui sera l’outil de prédilection pour **qui nous donne des commentaires**, les fonctionnalités qui vous plaît, les fonctionnalités que vous pouvez effectuer sans, ou lorsque un élément peut être préférable. Quand vous rejoignez le programme Insider, vous pouvez vous tenir **obtenir les dernières actualités Insider**, **taux builds** et accédez sur **quêtes de commentaires** à partir du Hub de commentaires.
* Nous avons également [publié un émulateur mis à jour de HoloLens](install-the-tools.md) générer.
* Vos vidéos de réalité mixte à présent se présenter mieux en raison d’automatique **stabilisation vidéo**.

## <a name="major-fixes"></a>Principaux correctifs

Nous avons résolu des problèmes avec des espaces hologramme où les espaces serait lente ou incorrectement détectés. Nous avons résolu un problème d’arrêt qui peut continuer à essayer de lancer l’interpréteur de commandes lors de l’arrêt.

Nous avons résolu un problème
* qui bloque la possibilité de reprendre une application XAML.
* où un incident laisserait un écran noir et autres traits en escalier.
* le défilement que parfois certains la retiennent dans la mauvaise direction lors de l’utilisation de certaines applications.
* la puissance LED peut indiquer un état de désactivation quand l’appareil était toujours activée.
* Wi-Fi peut obtenir désactivée après la reprise du mode veille.
* le fournisseur d’identité Xbox offre le programme d’installation gamertag et puis reste bloqué dans une boucle.
* l’interpréteur de commandes se bloque occasionnellement lors de la sélection d’un fichier téléchargé dans le sélecteur de fichiers OneDrive.
* enfoncée sur un lien parfois à la fois ouvre un onglet nouvelle, interrompu et un menu contextuel.
* où portail des appareils windows n’autorisait pas les ajustements IPD de 50 à 80

Nous avons résolu des problèmes avec les Photos où
* une image s’affiche parfois paysage en raison de la propriété orientation EXIF sera ignorée.
* Il peut se bloquer lors du démarrage de Photos épinglés.
* vidéos redémarre après une pause au lieu de continuer à partir de cas de la dernière suspension.
* relecture d’une vidéo partagée peut être évitée si elles étaient partagées pendant la lecture.
* Enregistrements de Capture de réalité mixtes seraient commencent par 1 de 0,5 seconde de flux uniquement audio.
* le bouton de synchronisation disparaît pendant la synchronisation initiale OneDrive.

Nous avons résolu des problèmes avec les paramètres où
* une actualisation était nécessaire lorsque l’environnement change.
* Entrez sur clavier n’aurait pas se comportent comme clic sur suivant dans certaines boîtes de dialogue.
* il était difficile de savoir jumelage lorsque le clicker a échoué.
* Il peut cesser de répondre avec Wi-Fi déconnecter et se connecter.

Nous avons résolu des problèmes avec Cortana où
* Il peut rester bloqué afficher l’interface utilisateur à l’écoute.
* demandant « Hey Cortana, que puis-je dire » à partir d’un mode exclusif d’application serait coincée si vous avez répondu Oui/non peut-être plutôt à la demande pour quitter l’application.
* Cortana à l’écoute de l’interface utilisateur ne redémarre pas correctement si vous demandez à Cortana pour accéder à la mise en veille et puis reprendre.
* les requêtes « quel réseau suis-je connecté au ? » et le « Am je connecté ? » peut échouer lorsque le premier profil de réseau est renvoyée sans connectivité.
* l’interface utilisateur intempestif sur « Écoute » mais en quittant une application serait immédiatement a commencé à effectuer la reconnaissance vocale à nouveau.
* où la déconnexion de l’application Cortana n’aurait pas permettre de vous connecter revenir à il avant un redémarrage.
* Il lancerait pas lorsque mixte réalité capturer l’interface utilisateur était actif.

Nous avons résolu des problèmes avec Visual Studio où
* débogage de la tâche en arrière-plan n’a pas fonctionné.
* analyse des frames dans le débogueur graphique n’a pas fonctionné.
* l’émulateur de HoloLens n’apparaissaient pas dans la liste déroulante pour Visual Studio, à moins que les TargetPlatformVersion de votre projet a été définie sur 10240.

## <a name="changes-from-previous-release"></a>Modifications à partir de la version précédente
* La commande Cortana **Hey Cortana, redémarrer l’appareil** ne fonctionne pas. Utilisateur peut dire **Hey Cortana, redémarrez** ou **Hey Cortana, redémarrez l’appareil**.
* Mode plein écran a été supprimé à partir du produit.

## <a name="prior-release-notes"></a>Notes de version antérieure
* [Notes de publication-mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Problèmes connus de HoloLens](hololens-known-issues.md)
* [Installer les outils](install-the-tools.md)
* [Shell](navigating-the-windows-mixed-reality-home.md)
* [La mise à jour des applications UWP 2D pour la réalité mixte](building-2d-apps.md)
* [Accessoires de matériel](hardware-accessories.md)
* [Capture de réalité mixte](mixed-reality-capture.md)
* [Entrée vocale](voice-input.md)
* [Soumission d’une application pour le Windows Store](submitting-an-app-to-the-microsoft-store.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
