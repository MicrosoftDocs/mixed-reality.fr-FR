---
title: Notes de publication-octobre 2017
description: Notes de publication Windows Mixed Reality pour le dans Windows 10 Fall Creators Update (octobre 2017).
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: Release notes, version, windows 10, build, rs3, système d’exploitation
ms.openlocfilehash: 7274dcf1db449fa35981eb72192fea9873fcc90a
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593358"
---
# <a name="release-notes---october-2017"></a>Notes de publication-octobre 2017

Page d’accueil Windows une réalité mixte ! La version de la **[Windows 10 Fall Creators Update](https://blogs.windows.com/windowsexperience/2017/10/17/whats-new-windows-10-fall-creators-update/)** introduit la prise en charge pour les nouveaux [des casques IMMERSIFS Windows Mixed Reality](immersive-headset-hardware-details.md) et [contrôleurs de mouvement ](motion-controllers.md), l’activation vous permettent d’Explorer de nouveaux mondes, jouer VR et expérience immersive divertissement lorsque connecté à un [PC compatibles Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines).

La version de casques de réalité mixte Windows et les contrôleurs de mouvement est le point culminant d’un travail d’équipe massive et une avancée considérable pour le [plate-forme de Windows Mixed Reality](mixed-reality.md), qui inclut [Microsoft HoloLens](hololens-hardware-details.md). Bien que HoloLens ne reçoit pas une mise à jour avec la version de Windows 10 Fall Creators Update, savoir que le travail sur HoloLens n’a pas encore arrêté ; Nous aurons un grand nombre de retours et d’analyse s’appliquent à partir de notre travail récent sur Windows Mixed Reality dans sa globalité. En fait, des casques IMMERSIFS Windows Mixed Reality et contrôleurs représentent une excellente voie d’accès de mouvement pointent vers le développement pour HoloLens, trop, comme les mêmes API, outils, et les concepts s’appliquent aux deux.

Pour mettre à jour vers la dernière version de chaque appareil, ouvrez le **paramètres** application, accédez à **mise à jour & sécurité**, puis sélectionnez le **vérifier les mises à jour** bouton. Sur un PC Windows 10, vous pouvez également installer manuellement l’à l’aide de Windows 10 Fall Creators Update le [outil de création de Windows media](https://www.microsoft.com/software-download/windows10).

 **Version la plus récente pour le bureau :** Le bureau de Windows 10 octobre 2017 (**10.0.16299.15**, Windows 10 Fall Creators Update)<br>
 **Version la plus récente pour HoloLens :** [Windows 10 HOLOGRAPHIQUE août 2016](release-notes-august-2016.md) (**10.0.14393.0**, mise à jour anniversaire Windows 10)

>[!VIDEO https://www.youtube.com/embed/YBcLy1lkegg]

## <a name="introducing-windows-mixed-reality"></a>Présentation de Windows Mixed Reality

Le Windows 10 Fall Creators Update introduit officiellement prise en charge pour les casques de réalité mixte Windows et des contrôleurs de mouvement, ainsi que la rendre Windows 10 premier système d’exploitation spatiales dans le monde. Voici les principales caractéristiques :
* **[Divers casques](https://blogs.windows.com/windowsexperience/2017/10/03/how-to-pre-order-your-windows-mixed-reality-headset/)**  -Windows Mixed Reality est permet aux partenaires à offrent un large éventail de casques qui débutent à 399 USD fourni avec les contrôleurs de mouvement.
* **[Contrôleurs de mouvement](motion-controllers.md)**  -contrôleurs de mouvement Windows Mixed Reality coupler avec votre PC via Bluetooth sans fil et degrés de liberté six de suivi, beaucoup de méthodes d’entrée et IMUs des fonctionnalités.
* **[Le programme d’installation facile et la portabilité](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/recommended-adapters-for-windows-mixed-reality-capable-pcs)**  - définir le configurer et de prise en main de moins de 10 minutes. Des casques IMMERSIFS utilisent le suivi d’intégrale pour effectuer le suivi de votre déplacement et de vos contrôleurs de mouvement, avec six degrés de liberté. Aucun des caméras externes ou marqueurs de phare nécessaires !
* **[Prise en charge pour une plage plus large de ses ordinateurs](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)**  -Windows Mixed Reality permettra à davantage de personnes de l’expérience de bureau VR qu’auparavant, avec prise en charge pour select intégré cartes graphiques et des PC en commençant à 499 USD.
* **[Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md)**  -premier système d’exploitation spatiales dans le monde fournit un environnement domestique familier des opérations multitâches avec les applications 2D, lancement VR jeux et applications et hologrammes décoratifs mis en place.
* **[Étonnants des jeux de réalité virtuelle et les applications dans le Microsoft Store](https://www.microsoft.com/store/collections/MR-All-ImmersiveContent/)**  - de divertissement immersive comme Hulu VR et 360 vidéo aux jeux épiques comme SUPERHOT VR et soleil d’Arizona, le Microsoft Store a une plage de contenu à l’expérience dans Windows mixte Réalité.
* **[Accès en avant-première SteamVR](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/using-steamvr-with-windows-mixed-reality)**  - The Windows 10 Fall Creators Update permet la prise en charge des titres SteamVR à jouer avec des casques de réalité mixte Windows et de contrôleurs, de rendre le catalogue le plus important de VR titres disponibles pour Windows mixte Utilisateurs de la réalité.

## <a name="known-issues"></a>Problèmes connus

Nous avons travaillé dur pour fournir une excellente expérience de réalité mixte Windows, mais nous sommes toujours le suivi des problèmes connus. Si vous trouvez d’autres, veuillez [envoyez-nous vos commentaires](give-us-feedback.md).

### <a name="desktop-app-in-the-windows-mixed-reality-home"></a>Application de bureau dans Windows Mixed Reality domestique
* L’outil capture ne fonctionne pas dans l’application de bureau.
* Application de bureau ne conserve pas de paramètre lors du redémarrage.
* Si vous utilisez version préliminaire du portail de réalité mixte sur votre bureau, lors de l’ouverture de l’application de bureau dans Windows Mixed Reality domestique, vous pouvez remarquer l’effet miroir infinie. 
* Exécution de l’application de bureau peut affecter les performances sur non - Ultra mixte réalité PC Windows ; Il n’est pas recommandé.  
* Application de bureau peut lancer automatiquement, car une fenêtre invisible sur le bureau a le focus. 
* Contrôle de compte d’utilisateur bureau invite rendra casque s’affichent en noir avant la fin de l’invite.

### <a name="windows-mixed-reality-setup"></a>Programme d’installation Windows Mixed Reality
* Lorsque vous configurez Windows avec un casque connecté, votre moniteur PC peut paraître vide. Débranchez votre casque pour activer la sortie vers le moniteur de votre ordinateur pour terminer l’installation de Windows.
* Lorsque vous créez une limite, le suivi peut échouer. Dans ce cas, essayez à nouveau, comme le système sera plus d’informations sur votre espace au fil du temps.
* Si vous activez Cortana ou désactiver pendant l’installation de Windows Mixed Reality, cette modification sera appliquée à vos postes de travail paramètres de Cortana.
* Si vous n’avez pas de casque connecté, vous risquez de manquer des conseils supplémentaires lorsque vous visitez tout d’abord Windows Mixed Reality domestique.
* Un casque Bluetooth peut provoquer des interférences avec des contrôleurs de mouvement. Nous vous recommandons de découplage ou Bluetooth contrôleurs hors tension pendant les sessions de réalité mixte de Windows.

### <a name="games-and-apps-from-windows-store"></a>Jeux et les applications à partir du Windows Store
* Certains jeux gourmandes en ressources graphiques, tels que Forza Motorsports 6, peut provoquer des problèmes de performances sur des PC moins compatibles lors de la lecture à l’intérieur de réalité mixte Windows.

### <a name="audio"></a>Audio
* Comme indiqué ci-dessus, les périphériques Bluetooth Audio ne fonctionnent pas correctement avec les voix de réalité mixte Windows et des expériences de sons spatiales. Elles peuvent également avoir un impact négatif affecter votre expérience de contrôleur de mouvement. Nous déconseillons l’utilisation de casques de Bluetooth Audio avec Windows Mixed Reality.
* Vous ne pouvez pas utiliser l’appareil connecté à audio (ou partie) le casque pour la lecture audio lorsque l’appareil n’est pas portée. Si vous avez uniquement un casque audio, il pourrez que vous souhaitez connecter le casque audio à l’ordinateur hôte au lieu du casque. Si, par conséquent, puis vous devez désactiver « basculer vers l’audio casque » **paramètres** > **Mixed Reality** > **Audio et reconnaissance vocale**.
* Certaines applications, y compris certains d'entre eux lancé via SteamVR, peuvent perdre des données audio ou se bloquer lorsque le périphérique audio change à mesure que vous démarrez ou arrêtez le portail de réalité mixte. Redémarrez l’application une fois que vous avez ouvert l’application de portail de réalité mixte pour corriger ce problème.
* Si vous avez Cortana est activé sur votre ordinateur hôte avant d’utiliser votre casque Windows Mixed Reality, vous risquez de perdre la simulation audio spatiale appliquée aux applications que vous placez autour de Windows Mixed Reality domestique. La solution de contournement consiste à activer « Windows Sonic pour un casque » sur tous les périphériques audio connectés à votre PC, et même votre casque audio appareil connecté :
   1. Cliquez sur l’icône haut-parleur dans la barre des tâches, puis sélectionnez à partir de la liste des périphériques audio.
   2. Avec le bouton droit sur la barre des tâches, l’icône de l’orateur et sélectionnez « Windows Sonic pour un casque » dans le menu « Le programme d’installation de l’orateur ».
   3. Répétez ces étapes pour tous les périphériques audio (points de terminaison).
>[!NOTE]
> - Étant donné que les écouteurs/haut-parleurs connectés à votre casque ne s’affiche pas, sauf si vous êtes le port, vous devez faire cela à partir de la fenêtre de l’application de bureau dans le Windows Mixed Reality domestique pour appliquer ce paramètre à l’appareil audio connecté à votre casque (ou intégré dans votre casque).
> - Une autre option consiste à désactiver les « Cortana de permettent de répondre à Hey Cortana » dans **paramètres** > **Cortana** sur votre bureau avant le lancement de Windows Mixed Reality.

* Quand un autre périphérique USB multimédia (par exemple, une webcam) partage le même concentrateur USB (externe ou à l’intérieur de votre PC) avec le casque Windows Mixed Reality, dans de rares cas audio jack/un casque du casque peut avoir un son bourdonnement ou sans contenu audio du tout. Vous pouvez résoudre ce problème en votre casque sur un port USB qui ne pas partager le même hub en tant que l’autre appareil, et vous déconnecter ou de désactiver votre appareil de multimédia USB.
* Dans les cas très rares, concentrateur USB de l’hôte du PC ne peut pas fournir une puissance suffisante pour le casque de réalité mixte Windows et vous pouvez remarquer une rafale de bruit le casque connecté au casque.

### <a name="speech"></a>Fonctions vocales
* Cortana peut échouer lire ses signaux audio pour les réponses à l’écoute/réflexions et audio aux commandes.
* Cortana sur les marchés de Chine et le Japon ne pas correctement afficher texte ci-dessous le cercle Cortana lors de l’utilisation.
* Cortana peut être lent à la première fois qu’elle est appelée dans une session du portail de réalité mixte. Vous pouvez contourner ce en rendant que « Let Cortana » répondre à Hey Cortana sous **paramètres** > **Cortana** > **communiquer avec Cortana** est activé.
* Cortana s’exécute plus lentement sur les PC qui ne sont pas des PC Windows Mixed Reality Ultra.
* Lorsque votre clavier système est définie sur une langue différente de la langue d’interface utilisateur dans Windows Mixed Reality, à l’aide de dictée à partir du clavier dans Windows Mixed Reality entraîne une boîte de dialogue d’erreur à propos de la dictée ne fonctionne ne pas en raison d’une connexion Wi-Fi n’ayant ne pas. Pour résoudre le problème Assurez-vous simplement que la langue du clavier système correspond à la langue de l’interface utilisateur de réalité mixte Windows.
* Espagne n’est pas correctement en cours reconnu comme un marché où vocale est activée pour la réalité mixte de Windows.

### <a name="holograms"></a>Hologrammes
* Si vous avez placé un grand nombre de hologrammes dans votre Windows Mixed Reality domestique, certains peuvent disparaître et réapparaître comme vous regardez autour. Pour éviter ce problème, supprimez certaines des hologrammes dans la zone de la réalité mixte Windows accueil.

### <a name="motion-controllers"></a>Contrôleurs de mouvement
* Parfois, si vous cliquez sur une page Web dans Edge, le contenu sera zoom au lieu de clic.
* Parfois, lorsque vous cliquez sur un lien dans Edge, la sélection ne fonctionnera pas.

## <a name="prior-release-notes"></a>Notes de version antérieure
* [Notes de publication-août 2016](release-notes-august-2016.md)
* [Notes de publication-mai 2016](release-notes-may-2016.md)
* [Notes de publication-mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Prise en charge de casque immersive (lien externe)](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality)
* [Problèmes connus de HoloLens](hololens-known-issues.md)
* [Installer les outils](install-the-tools.md)
* [Envoyez-nous vos commentaires](give-us-feedback.md)
