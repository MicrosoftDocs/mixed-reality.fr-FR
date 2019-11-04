---
title: Mise à jour d’applications UWP 2D pour la réalité mixte
description: Cet article décrit la mise à jour de votre application plateforme Windows universelle 2D existante pour qu’elle s’exécute sur HoloLens et les casques immersifs de Windows Mixed Reality.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: application 2D, UWP, application plate, HoloLens, casque immersif, modèle d’application, bouton précédent, barre d’application, PPP, résolution, mise à l’échelle
ms.openlocfilehash: 46d2a9ca044dee977faecc84d610dc0811a4bfb7
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73436983"
---
# <a name="updating-2d-uwp-apps-for-mixed-reality"></a>Mise à jour d’applications UWP 2D pour la réalité mixte

Windows Mixed Reality permet à un utilisateur de voir des hologrammes comme s’ils se trouvent sur vous, dans votre monde physique ou numérique. À la base, HoloLens et les ordinateurs de bureau auxquels vous attachez des accessoires de casque sont des appareils Windows 10 ; Cela signifie que vous pouvez exécuter presque toutes les applications de plateforme Windows universelle (UWP) dans le Store en tant qu’applications 2D.

## <a name="creating-a-2d-uwp-app-for-mixed-reality"></a>Création d’une application UWP 2D pour la réalité mixte

La première étape pour placer une application 2D sur des casques de réalité mixtes consiste à faire en sorte que votre application s’exécute en tant qu’application 2D standard sur votre moniteur d’ordinateur.

### <a name="building-a-new-2d-uwp-app"></a>Création d’une application UWP 2D

Pour générer une application 2D pour la réalité mixte, il vous suffit de créer une application standard 2D plateforme Windows universelle (UWP). Aucune autre modification de l’application n’est requise pour que cette application s’exécute en tant que ardoise dans une réalité mixte.

Pour commencer à créer une application UWP 2D, consultez l’article [créer votre première application](https://docs.microsoft.com/windows/uwp/get-started/your-first-app) .

### <a name="bringing-an-existing-2d-store-app-to-uwp"></a>Intégration d’une application de Store 2D existante à UWP

Si vous disposez déjà d’une application Windows 2D dans le Store, vous devez d’abord vous assurer qu’elle cible la plateforme Windows universelle Windows 10 (UWP). Voici tous les points de départ potentiels que vous pouvez avoir avec votre application Windows Store dès aujourd’hui :
<br>

|  Point de départ  |  Cible de plateforme de manifeste AppX  |  Comment faire pour que cela soit universel ? | 
|----------|----------|----------|
|  Windows Phone (Silverlight)  |  Manifeste de l’application Silverlight |  [Migrer vers WinRT](https://msdn.microsoft.com/library/windows/apps/dn642486(v=vs.105).aspx) | 
|  Windows Phone 8,1 universel  |  8,1 manifeste AppX qui n’inclut pas la plateforme cible  |  [Migrez votre application vers le plateforme Windows universelle](https://msdn.microsoft.com/library/mt148501.aspx) | 
|  Windows Store 8  |  8 manifeste AppX qui n’inclut pas la plateforme cible  |  [Migrez votre application vers le plateforme Windows universelle](https://msdn.microsoft.com/library/mt148501.aspx) | 
|  Windows Store 8,1 universel  |  8,1 manifeste AppX qui n’inclut pas la plateforme cible  |  [Migrez votre application vers le plateforme Windows universelle](https://msdn.microsoft.com/library/mt148501.aspx) | 

Si vous avez une application Unity 2D aujourd’hui créée en tant qu’application Win32 (la cible de build « PC, Mac & Linux Standalone »), vous pouvez cibler la réalité mixte en changeant Unity vers la cible de build « plateforme Windows universelle » à la place.

Nous aborderons les différentes façons dont vous pouvez limiter votre application spécifiquement à HoloLens à l’aide de la famille d’appareils Windows. holographique [ci-dessous](#publish-and-maintain-your-universal-app).

### <a name="run-your-2d-app-in-a-windows-mixed-reality-immersive-headset"></a>Exécuter votre application 2D dans un casque immersif Windows Mixed Reality

Si vous avez déployé votre application 2D sur l’ordinateur de bureau sur lequel vous le développez et que vous l’avez essayée sur votre moniteur, vous êtes déjà prêt à l’essayer dans un casque de bureau immersif !

Accédez simplement au menu Démarrer du casque de la réalité mixte et lancez l’application à partir de là. Le shell Desktop et le shell holographique partagent tous deux le même ensemble d’applications UWP, et l’application doit donc déjà être présente une fois que vous avez effectué le déploiement à partir de Visual Studio.

## <a name="targeting-both-immersive-headsets-and-hololens"></a>Ciblage à la fois des casques immersifs et HoloLens

Félicitations ! Votre application utilise désormais Windows 10 plateforme Windows universelle (UWP).

Votre application est désormais en mesure de s’exécuter sur des appareils Windows actuels tels que les ordinateurs de bureau, les appareils mobiles, la Xbox, les casques immersifs de Windows Mixed Reality et HoloLens, ainsi que les futurs appareils Windows. Toutefois, pour cibler réellement tous ces appareils, vous devez vous assurer que votre application cible la famille d’appareils Windows. Universal.

### <a name="change-your-device-family-to-windowsuniversal"></a>Remplacez votre famille d’appareils par Windows. Universal

Passons maintenant à votre manifeste AppX pour vous assurer que votre application UWP Windows 10 peut s’exécuter sur HoloLens :
* Ouvrez le fichier de solution de votre application avec **Visual Studio** et accédez au manifeste du package d’application.
* Cliquez avec le bouton droit sur le fichier **Package. appxmanifest** dans votre solution et accédez à **afficher le code**<br>
  ![package. appxmanifest dans Explorateur de solutions](images/openappxmanifest-500px.png)<br>
* Vérifiez que votre plateforme cible est Windows. Universal dans la section dépendances.
  ```
  <Dependencies>
    <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10586.0" />
  </Dependencies>
  ```
* Été!

Si vous n’utilisez pas Visual Studio pour votre environnement de développement, vous pouvez ouvrir **AppXManifest. xml** dans l’éditeur de texte de votre choix pour vous assurer que vous ciblez le *TargetDeviceFamily* **Windows. Universal** .

### <a name="run-in-the-hololens-emulator"></a>Exécuter dans l’émulateur HoloLens

Maintenant que votre application UWP cible « Windows. Universal », nous allons générer votre application et l’exécuter dans l' [émulateur HoloLens](using-the-hololens-emulator.md).
* Vérifiez que vous avez [installé l’émulateur HoloLens](install-the-tools.md).
* Dans Visual Studio, sélectionnez la configuration de build **x86** pour votre application

  ![configuration de build x86 dans Visual Studio](images/x86setting.png)<br>
* Sélectionnez **émulateur HoloLens** dans le menu déroulant cible de déploiement

  ![Émulateur HoloLens dans la liste cible de déploiement](images/deployemulator-500px.png)<br>
* Sélectionnez **Déboguer > démarrer le débogage** pour déployer votre application et démarrer le débogage.
* L’émulateur démarre et exécute votre application.
* Avec un clavier, une souris et/ou un contrôleur Xbox, placez votre application dans le monde entier pour la lancer.

  ![Émulateur HoloLens chargé avec un exemple UWP](images/hololensemulatorwithuwpsample-800px.png)<br>

### <a name="next-steps"></a>Étapes suivantes

À ce stade, l’une des deux situations suivantes peut se produire :
1. Votre application affichera son démarrage et commencera à s’exécuter une fois qu’elle sera placée dans l’émulateur ! Awesome!
2. Ou une fois que vous voyez une animation de chargement pour un hologramme 2D, le chargement s’arrête et vous verrez simplement votre application sur l’écran de démarrage. Cela signifie qu’une erreur est survenue et qu’il faut approfondir l’investigation pour comprendre comment amener votre application à la vie de la réalité mixte.

Pour accéder au bas de ce qui peut entraîner le non-démarrage de votre application UWP sur HoloLens, vous devez effectuer un débogage.

### <a name="running-your-uwp-app-in-the-debugger"></a>Exécution de votre application UWP dans le débogueur

Ces étapes vous guideront tout au long du débogage de votre application UWP à l’aide du débogueur Visual Studio.
* Si vous ne l’avez pas déjà fait, ouvrez votre solution dans Visual Studio. Remplacez la cible par l' **émulateur HoloLens** et la configuration de build par **x86**.
* Sélectionnez **Déboguer > démarrer le débogage** pour déployer votre application et démarrer le débogage.
* Placez l’application dans le monde entier à l’aide de la souris, du clavier ou du contrôleur Xbox.
* Visual Studio doit maintenant s’arrêter quelque part dans le code de votre application.
  - Si votre application ne se bloque pas immédiatement ou s’arrête dans le débogueur en raison d’une erreur non gérée, passez en revue un test des principales fonctionnalités de votre application pour vous assurer que tout est en cours d’exécution et fonctionnel. Vous pouvez voir des erreurs telles que celles illustrées ci-dessous (exceptions internes gérées). Pour vous assurer que vous ne manquez pas les erreurs internes qui ont un impact sur l’expérience de votre application, exécutez vos tests automatisés et tests unitaires pour vous assurer que tout se comporte comme prévu.

![Émulateur HoloLens chargé avec un exemple UWP présentant une exception système](images/hololensemulatorwithuwpsampleexception-800px.png)

## <a name="update-your-ui"></a>Mettre à jour votre interface utilisateur

Maintenant que votre application UWP s’exécute sur des casques immersifs et/ou HoloLens en tant qu’hologramme 2D, nous allons nous assurer que cela semble beau. Voici quelques points à prendre en compte :
* Windows Mixed Reality exécutera toutes les applications 2D à une résolution fixe et PPP qui correspond à 853x480 pixels effectifs. Considérez si votre conception a besoin d’être affinée à cette échelle et passez en revue les conseils de conception ci-dessous pour améliorer votre expérience sur HoloLens et les casques immersifs.
* Windows Mixed Reality [ne prend pas en charge](app-model.md) les vignettes dynamiques 2D. Si vos fonctionnalités principales présentent des informations sur une vignette dynamique, envisagez de déplacer ces informations dans votre application ou explorez les [lanceurs d’applications 3D](3d-app-launcher-design-guidance.md).

### <a name="2d-app-view-resolution-and-scale-factor"></a>résolution et facteur d’échelle de l’affichage des applications 2D

![À partir de la conception réactive](images/scale-500px.png)

Windows 10 déplace toutes les conceptions visuelles des pixels de l’écran réel vers les **pixels effectifs**. Cela signifie que les développeurs conçoivent leur interface utilisateur en suivant les instructions de l’interface utilisateur de Windows 10 pour les pixels effectifs, et la mise à l’échelle de Windows garantit que ces pixels effectifs sont la bonne taille pour la convivialité sur les appareils, les résolutions, les PPP, etc. Consultez cette présentation [sur MSDN](https://msdn.microsoft.com/library/windows/apps/Dn958435.aspx) pour en savoir plus, ainsi que sur cette présentation de la [Build](https://video.ch9.ms/sessions/build/2015/2-63_Build_2015_Windows_Scaling.pptx).

Même avec la capacité unique de placer des applications dans votre monde à un large éventail de distances, il est recommandé d’utiliser des distances d’affichage de type TV pour produire la meilleure lisibilité et l’interaction avec le point de vue des mouvements. En raison de cela, un ardoise virtuel dans la réalité mixte affiche votre vue UWP plate à l’adresse :

**1280 x 720, 150% dpi** (853x480 pixels effectifs)

Cette résolution présente plusieurs avantages :
* Cette disposition de pixels effective aura sur la même densité d’informations qu’une tablette ou un petit bureau.
* Il met en correspondance les pixels fixes DPI et effectifs pour les applications UWP s’exécutant sur Xbox One, ce qui permet une expérience transparente sur les appareils.
* Cette taille paraît bonne quand elle est mise à l’échelle sur notre gamme de distances d’exploitation pour les applications dans le monde.

### <a name="2d-app-view-interface-design-best-practices"></a>meilleures pratiques pour la conception d’une interface d’affichage d’application 2D

**Ne**
* Suivez les [instructions de l’interface utilisateur de Windows 10 (HIG)](https://dev.windows.com/design) pour les styles, les tailles de police et les tailles de bouton. HoloLens effectue le travail pour s’assurer que votre application aura des modèles d’application compatibles, des tailles de texte lisibles et un dimensionnement cible approprié.
* Assurez-vous que votre interface utilisateur suit les meilleures pratiques pour la [conception réactive](https://msdn.microsoft.com/library/windows/apps/dn958435.aspx) afin d’obtenir un meilleur aperçu de la résolution et de la résolution uniques de HoloLen.
* Utilisez les recommandations de thème de couleur « Light » de Windows.

**Ne pas:**
* Modifiez votre interface utilisateur trop radicalement en réalité mixte pour vous assurer que les utilisateurs ont une expérience familière dans et hors du casque.

### <a name="understand-the-app-model"></a>Comprendre le modèle d’application

Le [modèle d’application](app-model.md) pour la réalité mixte est conçu pour utiliser la vie de la réalité mixte, où de nombreuses applications sont regroupées. Imaginez cela comme l’équivalent de la réalité mixte du bureau, où vous exécutez plusieurs applications 2D en même temps. Cela a des implications sur le cycle de vie des applications, les vignettes et d’autres fonctionnalités clés de votre application.

### <a name="app-bar-and-back-button"></a>Barre d’application et bouton précédent

les vues 2D sont décorées avec une barre d’application au-dessus de leur contenu. La barre de l’application comporte deux points de personnalisation spécifiques à l’application :

**Title :** affiche le *DisplayName* de la vignette associée à l’instance de l’application

**Bouton précédent :** déclenche l’événement *[demandé](https://msdn.microsoft.com/library/windows/apps/windows.ui.core.systemnavigationmanager.backrequested.aspx)* lorsque l’utilisateur clique dessus. La visibilité du bouton précédent est contrôlée par *[SystemNavigationManager. AppViewBackButtonVisibility](https://msdn.microsoft.com/library/windows/apps/windows.ui.core.systemnavigationmanager.aspx)* .

![l’interface utilisateur de la barre de l’application dans la vue d’application 2D](images/12697297-10104100857470613-1470416918759008487-o-500px.jpg)<br>
*Interface utilisateur de la barre d’application dans la vue d’application 2D*

### <a name="test-your-2d-apps-design"></a>Tester la conception de votre application 2D

Il est important de tester votre application pour vous assurer que le texte est lisible, que les boutons peuvent être ciblés et que l’application globale semble correcte. Vous pouvez [tester](testing-your-app-on-hololens.md) sur un casque d’un bureau, un HoloLens, un émulateur ou un appareil tactile dont la résolution est définie sur 1280 x 720 @150%.

## <a name="new-input-possibilities"></a>Nouvelles possibilités d’entrée

HoloLens utilise des capteurs de profondeur avancés pour voir le monde et voir les utilisateurs. Cela permet des mouvements de main avancés tels que la [floraison](system-gesture.md#bloom) et l' [air](gaze-and-commit.md#composite-gestures). Les microphones puissants activent également les [expériences vocales](voice-input.md).

Avec les casques de bureau, les utilisateurs peuvent utiliser des contrôleurs de mouvement pour pointer vers des applications et prendre des mesures. Ils peuvent également utiliser un boîtier de sélection, en ciblant les objets avec le regard.

Windows s’occupe de toute cette complexité pour les applications UWP, en traduisant votre point de vue du [regard](gaze-and-commit.md), des gestes, de la voix et du contrôleur de mouvement en [événements pointeur](https://msdn.microsoft.com/library/windows/apps/mt404610#pointer_events) qui éliminent le mécanisme d’entrée. Par exemple, un utilisateur a peut-être fait un robinet avec sa main ou a retiré le déclencheur SELECT sur un contrôleur de mouvement, mais les applications 2D n’ont pas besoin de savoir où provient l’entrée. elles voient simplement une pression tactile 2D, comme sur un écran tactile.

Voici les concepts/scénarios de haut niveau que vous devez comprendre pour les entrées lors de l’intégration de votre application UWP à HoloLens :
* Le point d’arrêt de la souris se [transforme en](gaze-and-commit.md) événements de pointage, ce qui peut déclencher de manière inattendue des menus, des lanceurs ou d’autres éléments de l’interface utilisateur qui s’affichent simplement en Gazing de votre application.
* Le point de regard n’est pas aussi précis que l’entrée de la souris. Utilisez des cibles d’accès de taille appropriée pour HoloLens, de la même façon que les applications mobiles tactiles. Les petits éléments près des bords de l’application sont particulièrement difficiles à manipuler.
* Les utilisateurs doivent basculer entre les modes d’entrée pour aller du défilement au déplacement vers deux panoramiques de doigt. Si votre application a été conçue pour une entrée tactile, pensez à vous assurer qu’aucune fonctionnalité majeure n’est verrouillée derrière deux doigts. Dans ce cas, envisagez d’utiliser d’autres mécanismes d’entrée tels que des boutons qui peuvent initier deux panoramiques de doigt. Par exemple, l’application Maps peut effectuer un zoom avec deux panoramiques de doigt, mais a un bouton plus, moins et rotation pour simuler les mêmes interactions de zoom avec des clics simples.

L' [entrée vocale](voice-input.md) est un élément essentiel de l’expérience de la réalité mixte. Nous avons activé toutes les API de reconnaissance vocale qui se trouvent dans Windows 10 Powering Cortana lors de l’utilisation d’un casque.

## <a name="publish-and-maintain-your-universal-app"></a>Publier et tenir à jour votre application universelle

Une fois que votre application est en cours d’exécution, empaquetez votre application pour [la soumettre au Microsoft Store](submitting-an-app-to-the-microsoft-store.md).

## <a name="see-also"></a>Articles associés
* [Modèle d’application](app-model.md)
* [Pointer du regard vers l’avant et valider](gaze-and-commit.md)
* [Contrôleurs de mouvement](motion-controllers.md)
* [Entrée vocale](voice-input.md)
* [Envoi d’une application au Microsoft Store](submitting-an-app-to-the-microsoft-store.md)
* [Utilisation de l’émulateur HoloLens](using-the-hololens-emulator.md)
