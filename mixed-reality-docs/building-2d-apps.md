---
title: La mise à jour des applications UWP 2D pour la réalité mixte
description: Cet article décrit la mise à jour de votre application de plateforme Windows universelle 2D existante pour s’exécuter sur des casques IMMERSIFS HoloLens et Windows Mixed Reality.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: Application 2D, UWP, application plat, HoloLens, immersives casque modèle d’application, nouveau bouton, barre de l’application, PPP, résolution, de mise à l’échelle
ms.openlocfilehash: 35a2e7774a79e35893821467f7e9ef8c004efa20
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595363"
---
# <a name="updating-2d-uwp-apps-for-mixed-reality"></a>La mise à jour des applications UWP 2D pour la réalité mixte

Réalité mixte Windows permet à un utilisateur Voir hologrammes comme s’ils étaient directement autour de vous, dans votre monde physique ou numérique. Fondamentalement, HoloLens et sont tous deux les PC de bureau vous attachez des accessoires immersives casque pour appareils Windows 10 ; Cela signifie que vous êtes en mesure d’exécuter presque toutes les applications Universal Windows Platform (UWP) dans le Store en tant qu’applications 2D.

## <a name="creating-a-2d-uwp-app-for-mixed-reality"></a>Création d’une application UWP 2D pour la réalité mixte

La première étape pour migrer une application 2D vers les casques de réalité mixte consiste à lancer votre application comme application 2D standard sur votre moniteur du bureau.

### <a name="building-a-new-2d-uwp-app"></a>Création d’une application UWP 2D

Pour générer une nouvelle application 2D pour la réalité mixte, vous créez simplement un 2D standard application universelle Windows Platform (UWP). Aucune autre modification de l’application est requise pour cette application, puis exécuter en tant qu’une ardoise en réalité mixte.

Pour commencer la création d’une application UWP 2D, consultez la [créer votre première application](https://docs.microsoft.com/windows/uwp/get-started/your-first-app) article.

### <a name="bringing-an-existing-2d-store-app-to-uwp"></a>Mettre une application de Store 2D existante vers UWP

Si vous disposez déjà d’une application Windows 2D dans le Store, vous devez vous assurer qu’il cible le Windows 10 Universal Windows Platform (UWP). Voici tous des points de départ potentiels que vous auriez conclus avec votre application de Store dès aujourd'hui :
<br>

|  Point de départ  |  Manifeste AppX plateforme cible  |  Comment rendre cette universel ? | 
|----------|----------|----------|
|  Windows Phone (Silverlight)  |  Manifeste de l’application Silverlight |  [Migrer vers WinRT](https://msdn.microsoft.com/library/windows/apps/dn642486(v=vs.105).aspx) | 
|  Windows Phone 8.1 universel  |  8.1 manifeste AppX n’incluant pas de plateforme cible  |  [Migrer votre application vers la plateforme Windows universelle](https://msdn.microsoft.com/library/mt148501.aspx) | 
|  Windows Store 8  |  Manifeste AppX 8 qui n’inclut pas plateforme cible  |  [Migrer votre application vers la plateforme Windows universelle](https://msdn.microsoft.com/library/mt148501.aspx) | 
|  Windows Store 8.1 universel  |  8.1 manifeste AppX n’incluant pas de plateforme cible  |  [Migrer votre application vers la plateforme Windows universelle](https://msdn.microsoft.com/library/mt148501.aspx) | 

Si vous avez une application Unity 2D aujourd'hui générée sous la forme d’une application Win32 (« PC, Mac et Linux Standalone » build cible), vous pouvez cibler la réalité mixte en basculant Unity à la cible de build « Plateforme Windows universelle » à la place.

Nous allons parler des méthodes que vous pouvez restreindre votre application en particulier pour HoloLens à l’aide de la famille de périphériques Windows.Holographic [ci-dessous](#publish-and-maintain-your-universal-app).

### <a name="run-your-2d-app-in-a-windows-mixed-reality-immersive-headset"></a>Exécuter votre application 2D dans un casque immersif Windows Mixed Reality

Si vous avez déployé votre application 2D à l’ordinateur de bureau où vous développez et testée sur votre écran, vous êtes déjà prêt à l’essayer dans un casque bureau immersif !

Allez dans le menu Démarrer dans le casque de réalité mixte et lancez l’application à partir de là. Le shell de bureau et l’interpréteur de commandes HOLOGRAPHIQUE partagent le même ensemble d’applications UWP, et par conséquent, il est possible que l’application doit être déjà présente une fois que vous avez déployé à partir de Visual Studio.

## <a name="targeting-both-immersive-headsets-and-hololens"></a>Ciblage des casques IMMERSIFS et HoloLens

Félicitations ! Votre application utilise désormais la Windows 10 Universal Windows Platform (UWP).

Votre application est désormais capable de s’exécutant sur les appareils Windows aujourd'hui comme bureau, mobiles, Xbox, casques IMMERSIFS Windows Mixed Reality et HoloLens, ainsi que les appareils de Windows. Toutefois, pour réellement cibler tous ces appareils, vous devez garantir que votre application vise la famille de périphériques Windows.Universal.

### <a name="change-your-device-family-to-windowsuniversal"></a>Modifier votre famille de périphériques à Windows.Universal

Maintenant revenons dans votre manifeste AppX pour garantir votre application UWP Windows 10 peut s’exécuter sur HoloLens :
* Ouvrez le fichier de solution de votre application avec **Visual Studio** et accédez au manifeste de package d’application
* Bouton droit sur le **Package.appxmanifest** fichier dans votre Solution et accédez à **afficher le Code**<br>
  ![package.appxmanifest dans l’Explorateur de solutions](images/openappxmanifest-500px.png)<br>
* Vérifiez que votre plateforme cible est Windows.Universal dans la section dépendances
  ```
  <Dependencies>
    <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10586.0" />
  </Dependencies>
  ```
* sauvegarder !

Si vous n’utilisez pas Visual Studio pour votre environnement de développement, vous pouvez ouvrir **AppXManifest.xml** dans l’éditeur de texte de votre choix pour vous assurer que vous ciblez le **Windows.Universal**  *TargetDeviceFamily*.

### <a name="run-in-the-hololens-emulator"></a>Exécuter dans l’émulateur HoloLens

Maintenant que votre application UWP cible « Windows.Universal », nous allons générer votre application et l’exécuter dans le [HoloLens émulateur](using-the-hololens-emulator.md).
* Vérifiez que vous avez [installé l’émulateur de HoloLens](install-the-tools.md).
* Dans Visual Studio, sélectionnez le **x86** générer la configuration de votre application

  ![x86 build configuration dans Visual Studio](images/x86setting.png)<br>
* Sélectionnez **HoloLens émulateur** dans le menu de liste déroulante de cible de déploiement

  ![Émulateur HoloLens dans la liste cible de déploiement](images/deployemulator-500px.png)<br>
* Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et de démarrer le débogage.
* L’émulateur démarre et exécuter votre application.
* Avec un clavier, souris et/ou une manette Xbox, placez votre application dans le monde pour la lancer.

  ![HoloLens émulateur chargé avec un exemple d’UWP](images/hololensemulatorwithuwpsample-800px.png)<br>

### <a name="next-steps"></a>Étapes suivantes

À ce stade, une des deux choses permettre se produire :
1. Votre application affiche son démarrage et démarrer une fois, il est placé dans l’émulateur en cours d’exécution ! Génial !
2. Ou, une fois que vous voyez une animation de chargement pour un hologramme 2D, le chargement s’arrête et vous verrez simplement votre application à son écran de démarrage. Cela signifie que quelque chose s’est produite et il prendra un examen plus approfondi pour comprendre comment intégrer votre application à vie en réalité mixte.

Pour accéder au bas de votre application UWP pouvant causer ne pas à démarrer sur HoloLens, vous devrez déboguer.

### <a name="running-your-uwp-app-in-the-debugger"></a>Votre application UWP en cours d’exécution dans le débogueur

Ces étapes vous guidera le débogage de votre application UWP à l’aide du débogueur Visual Studio.
* Si vous n’avez pas déjà fait, ouvrez votre solution dans Visual Studio. Modifier la cible pour le **HoloLens émulateur** et la configuration de build à **x86**.
* Sélectionnez **Déboguer > Démarrer le débogage** pour déployer votre application et de démarrer le débogage.
* Placez l’application dans le monde entier avec la souris, un clavier ou une manette Xbox.
* Visual Studio doit maintenant s’arrêter quelque part dans le code de votre application.
  - Si votre application n’immédiatement se bloquer ou s’arrêter dans le débogueur en raison d’une erreur non gérée, puis de passer par un test des principales fonctionnalités de votre application pour vérifier que tout est en cours d’exécution et fonctionnelles. Des erreurs peuvent apparaître comme illustré ci-dessous (exceptions internes qui sont gérées). Pour vous assurer de que ne pas manquer les erreurs internes qui affecte l’expérience de votre application, exécuter vos tests automatisés et les tests unitaires pour vous assurer que tout se comporte comme prévu.

![HoloLens émulateur chargé avec un exemple qui UWP indique une exception de système](images/hololensemulatorwithuwpsampleexception-800px.png)

## <a name="update-your-ui"></a>Mettre à jour de votre interface utilisateur

Maintenant que votre application UWP est en cours d’exécution sur des casques IMMERSIFS et/ou HoloLens comme un hologramme 2D, ensuite nous veillerons à ce qu'apparemment magnifiques. Voici quelques éléments à prendre en compte :
* Windows Mixed Reality exécutera toutes les applications 2D à une résolution fixe et de résolution qui équivaut à pixels efficaces 853 x 480. Déterminez si votre conception doit affinement à cette échelle et passez en revue les conseils de conception ci-dessous pour améliorer votre expérience sur HoloLens et des casques IMMERSIFS.
* Windows Mixed Reality [ne prend pas en charge](app-model.md) 2D vignettes dynamiques. Si votre fonctionnalité principale affiche des informations sur une vignette dynamique, envisagez de déplacer ces informations de retour dans votre application ou explorez [lanceurs d’applications 3D](3d-app-launcher-design-guidance.md).

### <a name="2d-app-view-resolution-and-scale-factor"></a>Facteur de résolution et de mise à l’échelle de la vue application 2D

![À partir de la conception réactive](images/scale-500px.png)

Windows 10 déplace toutes les zone de conception visuelle de pixels écran réel à **pixels effectifs**. Cela signifie que les développeurs conçoivent leur interface utilisateur suivant le Windows 10 Human Interface Guidelines pour pixels efficaces et mise à l’échelle Windows garantit ces pixels effectifs sont la bonne taille pour la facilité d’utilisation sur les appareils, les résolutions, les PPP, etc. Consultez ce [excellent en lecture sur MSDN](https://msdn.microsoft.com/library/windows/apps/Dn958435.aspx) pour en savoir plus, ainsi que cela [BUILD présentation](http://video.ch9.ms/sessions/build/2015/2-63_Build_2015_Windows_Scaling.pptx).

Même avec la capacité unique de placer des applications dans votre monde à une plage de distances, affichage de celle de la télévision distances sont recommandés pour produire l’optimiser la lisibilité et l’interaction avec les regards/mouvement. Pour cette raison, une ardoise virtuelle dans la page d’accueil réalité mixte affiche votre affichage en 2D UWP à :

**1280 x 720, 150 % ppp** (pixels effectifs 853 x 480)

Cette résolution présente plusieurs avantages :
* Cette disposition pixels aura sur la même densité d’informations en tant qu’une tablette ou un petit bureau.
* Elle correspond à la résolution fixe et pixels efficaces pour les applications UWP en cours d’exécution sur Xbox One, l’activation d’une expérience transparente entre les appareils.
* Cette taille semble correcte lors de la mise à l’échelle sur notre gamme de fonctionnement des distances pour les applications dans le monde entier.

### <a name="2d-app-view-interface-design-best-practices"></a>Application 2D vue interface meilleures pratiques de conception

**Procédez comme :**
* Suivez le [instructions Interface humaine (HIG) de Windows 10](https://dev.windows.com/design) pour les styles, les tailles de police et les tailles de bouton. HoloLens effectuent l’opération pour vous assurer de que votre application aura des modèles d’applications compatibles, des tailles de texte lisible et dimensionnement de la cible d’accès approprié.
* Vérifiez votre suit l’interface utilisateur de meilleures pratiques pour [conception réactive](https://msdn.microsoft.com/library/windows/apps/dn958435.aspx) mieux en résolution unique et une résolution de HoloLen.
* Utilisez les recommandations de thème de couleur « light » à partir de Windows.

**Ne pas :**
* Modifier votre interface utilisateur trop considérablement en réalité mixte, pour garantir aux utilisateurs une expérience familière vers et depuis le casque.

### <a name="understand-the-app-model"></a>Comprendre le modèle d’application

Le [modèle d’application](app-model.md) pour la réalité mixte est conçue pour utiliser la maison de réalité mixte, où de nombreuses applications live ensemble. Considérez cela comme l’équivalent de réalité mixte du bureau, sur lequel vous exécutez de nombreuses applications 2D à la fois. Cela a des conséquences sur le cycle de vie d’application, les vignettes et les autres fonctionnalités clées de votre application.

### <a name="app-bar-and-back-button"></a>Barre de l’application et le bouton précédent

Vues 2D sont décorées avec une barre de l’application au-dessus de leur contenu. La barre d’application a deux points de personnalisation spécifiques à l’application :

**Titre :** affiche le *displayname* de la vignette associée à l’instance d’application

**Bouton précédent :** déclenche le *[BackRequested](https://msdn.microsoft.com/library/windows/apps/windows.ui.core.systemnavigationmanager.backrequested.aspx)* événement lorsque enfoncé. Visibilité de bouton précédente est contrôlée par  *[SystemNavigationManager.AppViewBackButtonVisibility](https://msdn.microsoft.com/library/windows/apps/windows.ui.core.systemnavigationmanager.aspx)*.

![Application barre de l’interface utilisateur dans la vue de l’application 2D](images/12697297-10104100857470613-1470416918759008487-o-500px.jpg)<br>
*Application barre de l’interface utilisateur dans la vue de l’application 2D*

### <a name="test-your-2d-apps-design"></a>Tester la conception de votre application 2D

Il est important de tester votre application pour vous assurer que le texte est lisible, les boutons sont pouvant être ciblées, et l’application globale semble correcte. Vous pouvez [tester](testing-your-app-on-hololens.md) sur un casque de bureau, un HoloLens, un émulateur ou un périphérique tactile avec une résolution de 1280 x 720 @150%.

## <a name="new-input-possibilities"></a>Nouvelles possibilités d’entrée

HoloLens utilise des capteurs de profondeur avancés pour voir le monde et voir les utilisateurs. Cela permet des mouvements de main avancées telles que [bloom](gestures.md#bloom) et [-appui en l’air](gestures.md#air-tap). Microphones puissantes permettent également [vocal expériences](voice-input.md).

Avec Bureau casques, les utilisateurs peuvent utiliser des contrôleurs de mouvement pour pointer vers les applications et de prendre des mesures. Ils peuvent également utiliser un boîtier de commande, en ciblant des objets avec leurs regards.

Windows prend en charge tous les cette complexité pour les applications UWP, traduire votre [les regards](gaze.md), mouvements, vocale et de mouvement d’entrée de contrôleur à [événements de pointeur](https://msdn.microsoft.com/library/windows/apps/mt404610#pointer_events) qui clarifient le mécanisme d’entrée. Par exemple, un utilisateur peut avoir effectué un appui avec la main ou extraites sélectionnez le déclencheur sur un contrôleur de mouvement, mais n’avez pas besoin de savoir où l’entrée provenance : ils simplement voient une pression tactile 2D appuyez, comme si vous utilisez un écran tactile applications 2D.

Voici les concepts de haut niveau/scénarios que vous devez comprendre pour l’entrée lorsque vous importez votre application UWP dans HoloLens :
* [Utilisation](gaze.md) se transforme en événements de pointage, qui peuvent déclencher inopinément les menus, les menus volants ou autres éléments d’interface utilisateur apparaître juste par gazing autour de votre application.
* Regards n’est pas aussi précis que l’entrée de la souris. Utilisez la taille appropriée d’accès cibles pour HoloLens, similaires aux applications mobiles tactile. Petits éléments près des bords de l’application sont particulièrement difficiles à interagir avec.
* Les utilisateurs doivent basculer les modes d’entrée pour accéder à partir de la faire défiler vers le faisant glisser vers le panoramique à deux doigts. Si votre application a été conçue pour une entrée tactile, envisagez de vous assurer qu’aucune fonctionnalité majeure est derrière panoramique à deux doigts. Dans ce cas, envisagez de disposer d’autres mécanismes d’entrée comme des boutons qui peuvent initier le panoramique à deux doigts. Par exemple, l’application Maps peut effectuer un zoom avec panoramique à deux doigts mais a un signe plus, moins et faire pivoter le bouton pour simuler les interactions de zoom même clics unique.

[Entrée voix](voice-input.md) est un élément essentiel de l’expérience de réalité mixte. Nous avons activé toutes l’API qui se trouvent dans Windows 10 mise sous tension Cortana lors de l’utilisation d’un casque de reconnaissance vocale.

## <a name="publish-and-maintain-your-universal-app"></a>Publier et mettre à jour votre application universelle

Une fois que votre application est en cours d’exécution, empaqueter votre application à [soumettez-le sur le Microsoft Store](submitting-an-app-to-the-microsoft-store.md).

## <a name="see-also"></a>Voir aussi
* [Modèle d’application](app-model.md)
* [Gaze](gaze.md)
* [Mouvement](gestures.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Voice](voice-input.md)
* [Soumission d’une application pour le Microsoft Store](submitting-an-app-to-the-microsoft-store.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
