---
title: Notes de publication-octobre 2017
description: Notes de publication de Windows Mixed Reality pour la mise à jour des créateurs de automne Windows 10 (octobre 2017).
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: Notes de publication, version, Windows 10, Build, RS3, système d’exploitation
ms.openlocfilehash: 7274dcf1db449fa35981eb72192fea9873fcc90a
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524096"
---
# <a name="release-notes---october-2017"></a>Notes de publication-octobre 2017

Bienvenue dans Windows Mixed Reality! La publication de la **[mise à jour des créateurs de automne Windows 10](https://blogs.windows.com/windowsexperience/2017/10/17/whats-new-windows-10-fall-creators-update/)** introduit la prise en charge des nouveaux contrôleurs de [mouvement](motion-controllers.md)et casques immersifs de la [réalité Windows Mixed](immersive-headset-hardware-details.md) , ce qui vous permet d’explorer de nouveaux mondes, de jouer à des jeux VR et d’expérimenter les environnements immersifs. divertissement quand vous êtes connecté à un [PC Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines).

La sortie des casques et des contrôleurs de mouvement Windows Mixed Reality est l’aboutissement d’un effort d’équipe massif et d’un grand pas en avant pour la [plateforme Windows Mixed Reality](mixed-reality.md), qui comprend [Microsoft HoloLens](hololens-hardware-details.md). Si HoloLens ne reçoit pas de mise à jour avec la publication de la mise à jour des créateurs de automne Windows 10, sachez que le travail sur HoloLens n’a pas été arrêté. Nous aurons un grand nombre d’apprentissages et d’informations à appliquer à partir de notre travail récent sur Windows Mixed Reality dans son ensemble. En fait, les contrôleurs de mouvement et les casques immersifs de Windows Mixed Reality représentent un excellent point d’entrée pour le développement de HoloLens, car les mêmes API, outils et concepts s’appliquent aux deux.

Pour effectuer une mise à jour vers la dernière version pour chaque périphérique, ouvrez l’application **paramètres** , accédez à **mettre à jour & sécurité**, puis sélectionnez le bouton **Rechercher les mises à jour** . Sur un PC Windows 10, vous pouvez également installer manuellement la mise à jour des créateurs de automne Windows 10 à l’aide de l' [outil de création de média Windows](https://www.microsoft.com/software-download/windows10).

 **Dernière version pour ordinateur de bureau:** Windows 10 Desktop octobre 2017 (**10.0.16299.15**, Windows 10 automne Creators Update)<br>
 **Dernière version pour HoloLens:** [Windows 10, août 2016](release-notes-august-2016.md) (**10.0.14393.0**, mise à jour anniversaire Windows 10)

>[!VIDEO https://www.youtube.com/embed/YBcLy1lkegg]

## <a name="introducing-windows-mixed-reality"></a>Présentation de Windows Mixed Reality

La mise à jour des créateurs de automne de Windows 10 introduit officiellement la prise en charge des contrôleurs de mouvement et des casques de Windows Mixed Reality, ainsi que Windows 10 le premier système d’exploitation spatial au monde. Voici les points principaux :
* **[Variété de casques](https://blogs.windows.com/windowsexperience/2017/10/03/how-to-pre-order-your-windows-mixed-reality-headset/)** : Windows Mixed Reality permet aux partenaires d’offrir un large éventail de casques, qui démarrent à $399 USD avec les contrôleurs de mouvement.
* **[Contrôleurs de mouvement](motion-controllers.md)** : les contrôleurs de mouvement Windows Mixed Real sont couplés sans fil avec votre PC via Bluetooth et sont dotés de six degrés de liberté, d’une grande quantité de méthodes d’entrée et de IMUs.
* **[Facilité de configuration et](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/recommended-adapters-for-windows-mixed-reality-capable-pcs)** de portabilité: configurez et commencez en moins de 10 minutes. Les casques immersifs utilisent le suivi à l’intérieur pour suivre votre mouvement et vos contrôleurs de mouvement, avec six degrés de liberté. Aucun appareil photo ou marqueur de phare externe n’est nécessaire.
* **[Prise en charge d’un plus grand nombre de PC](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)** : Windows Mixed Reality permet à davantage de personnes d’expérimenter Desktop VR, avec la prise en charge de la sélection de cartes graphiques intégrées et de PC à partir de $499 USD.
* **[Windows Mixed Reality-page d’hébergement](navigating-the-windows-mixed-reality-home.md)** : le premier système d’exploitation spatial au monde fournit un environnement de travail familier pour le multitâche avec les applications 2D, le lancement de jeux et d’applications VR et la mise en place d’hologrammes décoratifs.
* Des **[jeux et des applications étonnants dans le Microsoft Store](https://www.microsoft.com/store/collections/MR-All-ImmersiveContent/)** , de la vidéo immersif comme Hulu vr et 360 Video à des jeux épiques comme SUPERHOT VR et Arizona soleil, le Microsoft Store a une gamme de contenu à rencontrer dans Windows Mixed Reality.
* **[Accès précoce à SteamVR](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/using-steamvr-with-windows-mixed-reality)** : la mise à jour des créateurs de automne Windows 10 permet la lecture des titres SteamVR avec les contrôleurs et les casques de réalité Windows Mixed, ce qui rend le plus grand catalogue de titres VR disponible pour les utilisateurs de Windows Mixed Reality.

## <a name="known-issues"></a>Problèmes connus

Nous avons travaillé dur pour offrir une expérience Windows Mixed Reality exceptionnelle, mais nous effectuons toujours le suivi de certains problèmes connus. Si vous en trouvez d’autres, faites [-nous part de vos commentaires](give-us-feedback.md).

### <a name="desktop-app-in-the-windows-mixed-reality-home"></a>Application de bureau dans la page d’hébergement Windows Mixed Reality
* L’outil capture ne fonctionne pas dans l’application de bureau.
* L’application de bureau n’est pas définie lors du redémarrage.
* Si vous utilisez la préversion du portail de réalité mixte sur votre bureau, lorsque vous ouvrez l’application de bureau dans la page d’accueil de Windows Mixed Reality, vous remarquerez peut-être l’effet de miroir infini. 
* L’exécution de l’application de bureau peut entraîner des problèmes de performances sur les PC non-ultra-Windows Mixed Reality. Cela n’est pas recommandé.  
* L’application de bureau peut être lancée automatiquement, car une fenêtre invisible sur le Bureau a le focus. 
* L’invite du contrôle de compte d’utilisateur du Bureau fera apparaître le casque en noir jusqu’à ce que l’invite soit terminée.

### <a name="windows-mixed-reality-setup"></a>Programme d’installation de Windows Mixed Reality
* Quand vous configurez Windows avec un casque connecté, votre moniteur PC peut rester vide. Débranchez votre casque pour activer la sortie sur votre moniteur d’ordinateur pour terminer l’installation de Windows.
* Lors de la création d’une limite, le suivi peut échouer. Si c’est le cas, réessayez, car le système va en savoir plus sur votre espace au fil du temps.
* Si vous activez ou désactivez Cortana au cours de l’installation de Windows Mixed Reality, cette modification sera appliquée aux paramètres de votre bureau Cortana.
* Si vous n’avez pas de casque connecté, vous risquez de manquer des conseils supplémentaires lorsque vous visitez pour la première fois la page d’hébergement Windows Mixed Reality.
* Le casque Bluetooth peut provoquer des interférences avec les contrôleurs de mouvement. Nous vous recommandons de découpler ou de mettre hors tension les contrôleurs Bluetooth pendant les sessions Windows Mixed Reality.

### <a name="games-and-apps-from-windows-store"></a>Jeux et applications à partir du Windows Store
* Certains jeux graphiques intensifs, tels que Forza Motorsports 6, peuvent entraîner des problèmes de performances sur les PC moins aptes lorsqu’ils sont lus dans Windows Mixed Reality.

### <a name="audio"></a>Audio
* Comme indiqué ci-dessus, les périphériques audio Bluetooth ne fonctionnent pas correctement avec Windows Mixed Reality Voice et les expériences de son spatial. Ils peuvent également avoir un impact négatif sur votre interface de contrôleur de mouvement. Nous vous déconseillons d’utiliser des casques audio Bluetooth avec Windows Mixed Reality.
* Vous ne pouvez pas utiliser le périphérique audio connecté (ou une partie du) au casque pour la lecture audio lorsque l’appareil n’est pas usé. Si vous n’avez qu’un seul casque audio, vous souhaiterez peut-être connecter le casque audio au PC hôte au lieu du casque. Si c’est le cas, vous devez désactiver l’option «Basculer vers l’audio du casque» dans **paramètres** > **voix et voix**de la**réalité** > mixte.
* Certaines applications, y compris un grand nombre de celles lancées via SteamVR, peuvent perdre du son ou se bloquer lorsque le périphérique audio change quand vous démarrez ou arrêtez le portail de réalité mixte. Redémarrez l’application après avoir ouvert l’application portail de réalité mixte pour corriger ce comportement.
* Si vous avez activé Cortana sur votre ordinateur hôte avant d’utiliser votre casque Windows Mixed Reality, vous risquez de perdre la simulation de son spatial appliquée aux applications que vous placez dans la page d’accueil de Windows Mixed Reality. La solution consiste à activer «Windows Sonic pour casque» sur tous les périphériques audio connectés à votre PC, y compris votre périphérique audio connecté à un casque:
   1. Cliquez avec le bouton gauche sur l’icône de haut-parleur dans la barre des tâches du bureau, puis sélectionnez dans la liste des périphériques audio.
   2. Cliquez avec le bouton droit sur l’icône de haut-parleur dans la barre des tâches du bureau, puis sélectionnez «Windows Sonic pour casque» dans le menu «Configuration des conférenciers».
   3. Répétez ces étapes pour tous vos périphériques audio (points de terminaison).
>[!NOTE]
> - Étant donné que les casques/enceintes connectés à votre casque ne s’affichent pas, sauf si vous les utilisez, vous devez le faire à partir de la fenêtre de l’application de bureau dans la page d’hébergement de Windows Mixed Reality pour appliquer ce paramètre au périphérique audio connecté à votre casque (ou intégré dans votre casque).
> - Une autre option consiste à désactiver «laisser Cortana répondre à Hey Cortana» dans **paramètres** > **Cortana** sur votre bureau avant de lancer Windows Mixed Reality.

* Lorsqu’un autre périphérique USB multimédia (par exemple, une webcam) partage le même concentrateur USB (externe ou à l’intérieur de votre ordinateur) avec le casque Windows Mixed Reality, dans de rares cas, le casque audio/casque peut avoir un signal sonore ou aucun son. Vous pouvez résoudre ce problème en utilisant votre casque sur un port USB qui ne partage pas le même concentrateur que l’autre, ou déconnecter/désactiver votre autre périphérique multimédia USB.
* Dans de très rares cas, le concentrateur USB de l’ordinateur hôte ne peut pas fournir suffisamment de puissance au casque Windows Mixed Reality. vous pouvez remarquer une rafale de bruit du casque connecté au casque.

### <a name="speech"></a>Fonctions vocales
* Cortana peut ne pas pouvoir lire ses signaux audio pour l’écoute/la réflexion et les réponses audio aux commandes.
* Cortana sur les marchés de la Chine et du Japon n’affiche pas correctement le texte sous le cercle Cortana en cours d’utilisation.
* Cortana peut être lente la première fois qu’elle est appelée dans une session de portail de réalité mixte. Vous pouvez contourner ce contournement en vous assurant que «laisser Cortana répondre à Hey Cortana» sous **paramètres** > **Cortana** > **communiquer avec Cortana** est activée.
* Cortana peut s’exécuter plus lentement sur les PC qui ne sont pas des PC Windows de réalité mixte.
* Lorsque votre clavier système est défini sur une langue différente de la langue de l’interface utilisateur dans Windows Mixed Reality, l’utilisation de la dictée à partir du clavier dans Windows Mixed Reality génère une boîte de dialogue d’erreur indiquant que la dictée ne fonctionne pas en raison de l’absence de connexion Wi-Fi. Pour résoudre le problème, assurez-vous simplement que la langue du clavier système correspond à la langue de l’interface utilisateur de Windows Mixed Reality.
* L’Espagne n’est pas reconnue correctement comme un marché sur lequel la reconnaissance vocale est activée pour Windows Mixed Reality.

### <a name="holograms"></a>Hologrammes
* Si vous avez placé un grand nombre d’hologrammes dans votre foyer Windows Mixed Reality, certains peuvent disparaître et apparaître à l’impression. Pour éviter cela, supprimez certains des hologrammes dans cette zone de la famille Windows Mixed Reality.

### <a name="motion-controllers"></a>Contrôleurs de mouvement
* Parfois, si vous cliquez sur une page Web dans Edge, le contenu est zoom au lieu de cliquer.
* Parfois, lorsque vous cliquez sur un lien dans Edge, la sélection ne fonctionne pas.

## <a name="prior-release-notes"></a>Notes de publication antérieures
* [Notes de publication - Août 2016](release-notes-august-2016.md)
* [Notes de publication - Mai 2016](release-notes-may-2016.md)
* [Notes de publication - Mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Prise en charge des casques immersifs (lien externe)](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality)
* [Problèmes connus concernant HoloLens](hololens-known-issues.md)
* [Installer les outils](install-the-tools.md)
* [Nous envoyer vos commentaires](give-us-feedback.md)
