---
title: Test de votre application sur HoloLens
description: Conseils et suggestions pour tester votre application HoloLens
author: JonMLyons
ms.author: jlyons
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens, test
ms.openlocfilehash: 35e8eff230cdcd719952ad2633ec610c9a9a26a0
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63549056"
---
# <a name="testing-your-app-on-hololens"></a>Test de votre application sur HoloLens

Le test des applications HoloLens est très similaire au test des applications Windows. Toutes les zones habituelles doivent être considérées (fonctionnalités, interopérabilité, performances, sécurité, fiabilité, etc.). Toutefois, certaines zones nécessitent un traitement spécial ou une attention particulière aux détails qui ne sont généralement pas observés dans les applications PC ou téléphone. Les applications holographiques doivent s’exécuter sans heurts dans un ensemble diversifié d’environnements. Ils doivent également conserver les performances et le confort de l’utilisateur à tout moment. Les conseils pour tester ces domaines sont détaillés dans cette rubrique.

## <a name="performance"></a>Performances

Les applications holographiques doivent s’exécuter sans heurts dans un ensemble diversifié d’environnements. Ils doivent également conserver les performances et le confort de l’utilisateur à tout moment. Les performances sont si importantes pour l’expérience de l’utilisateur avec une application holographique dans laquelle nous avons une rubrique entière consacrée. Veillez à lire et à suivre la [Description des performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)

## <a name="testing-3d-in-3d"></a>Test de 3D en 3D
1. **Testez votre application dans autant d’espaces que possible.** Essayez dans les grands locaux, les petites salles, les salles de bain, les cuisines, les chambres, les bureaux, etc. Prenez également en compte les chambres avec des fonctionnalités non standard, telles que les murs non verticaux, les murs incurvés et les limites non horizontales. Fonctionne-t-il bien lors de la transition entre des salles, des planchers, en passant par des couloirs ou des escaliers?
2. **Testez votre application dans des conditions d’éclairage différentes.** Répond-il correctement à différentes conditions environnementales, telles que l’éclairage, les surfaces noires, les surfaces transparentes/réfléchissantes telles que les miroirs, les murs de verre, etc.
3. **Testez votre application dans différentes conditions de mouvement.** Mettez sur l’appareil et essayez vos scénarios dans différents États de mouvement. Répond-il correctement à un mouvement ou à un état stable différent?
4. **Testez le fonctionnement de votre application à partir de différents angles.** Si vous avez un hologramme universel, que se passe-t-il si votre utilisateur s’en sert? Que se passe-t-il si un élément est présent entre l’utilisateur et l’hologramme? Que se passe-t-il si l’utilisateur regarde l’hologramme ci-dessus ou en dessous?
5. **Utilisez des signaux spatial et audio.** Assurez-vous que votre application les utilise pour empêcher la perte de l’utilisateur.
6. **Testez votre application à différents niveaux de bruit ambiant.** Si vous avez implémenté des commandes vocales, essayez de les appeler avec différents niveaux de bruit ambiant.
7. **Testez votre application en place et debout**. Veillez à tester à partir des sièges et des positions debout.
8. **Testez votre application à partir de différentes distances**. Les éléments d’interface utilisateur peuvent-ils être lus et interagis à partir de loin? Votre application réagit-elle aux utilisateurs qui se trouvent trop près de vos hologrammes?
9. **Testez votre application en fonction des interactions courantes de la barre d’application**. Toutes les vignettes d’application et les applications universelles 2D ont une [barre d’application](navigating-the-windows-mixed-reality-home.md#moving-and-adjusting-apps) qui vous permet de contrôler la façon dont l’application est positionnée dans le monde mixte. Assurez-vous que le fait de cliquer sur supprimer met fin à votre processus d’application et que le bouton précédent est pris en charge dans le contexte de votre application universelle 2D. Essayez de mettre à l’échelle et de déplacer votre application en [mode d’ajustement](navigating-the-windows-mixed-reality-home.md#moving-and-adjusting-apps) , tant qu’elle est active et qu’il s’agit d’une vignette d’application interrompue.

### <a name="environmental-test-matrix"></a>Matrice de test environnemental

![Matrice de test de l’environnement pour le développement d’applications HoloLens](images/environment-matrix-600px.png)

## <a name="comfort"></a>Optimal
1. **Plans de clip.** Soyez précis à l’endroit où [les hologrammes sont rendus](hologram-stability.md#hologram-render-distances).
2. **Évitez les mouvements virtuels incohérents avec le mouvement de la tête réelle.** Évitez de déplacer l’appareil photo d’une façon qui n’est pas représentative du mouvement réel de l’utilisateur. Si votre application nécessite de déplacer l’utilisateur via une scène, rendez le mouvement prévisible, réduisez l’accélération et laissez l’utilisateur contrôler le mouvement.
3. **Suivez les instructions de qualité de l’hologramme.** Les applications performantes qui implémentent les recommandations en matière de [qualité](hologram-stability.md) des hologrammes sont moins susceptibles d’entraîner une gêne pour l’utilisateur.
4. **Distribuez les hologrammes horizontalement plutôt que verticalement.** Forcer l’utilisateur à consacrer de longues périodes de temps à la recherche ou à la baisse peut entraîner une fatigue dans le cou.

## <a name="input"></a>Entrée

### <a name="gaze-and-gestures"></a>Point de regard et mouvements

Le point de [vue est une](gaze.md) forme de base d’entrée sur HoloLens qui permet aux utilisateurs de viser les hologrammes et l’environnement. Vous pouvez voir visuellement où le point de regard cible en fonction de la position du curseur. Il est courant d’associer le curseur en regard d’un curseur de souris.

Les [gestes](gestures.md) sont la manière dont vous interagissez avec les hologrammes, comme un clic de souris. La plupart du temps, les comportements de souris et de toucher sont identiques, mais il est important de comprendre et de valider le moment où ils diffèrent.

**Validez le moment où votre application a un comportement différent avec la souris et le toucher.** Cela permet d’identifier les incohérences et d’aider à prendre des décisions de conception pour rendre l’expérience plus naturelle pour les utilisateurs. Par exemple, le déclenchement d’une action basée sur le pointage.

> [!NOTE]
> Plus d’instructions spécifiques à HoloLens 2 bientôt [disponible](index.md#news-and-notes).

### <a name="custom-voice-commands"></a>Commandes vocales personnalisées

L' [entrée vocale](voice-input.md) est une forme naturelle d’interaction. L’expérience utilisateur peut être magique ou confuse en fonction de votre choix de commandes et de la façon dont vous les exposez. En règle générale, vous ne devez pas utiliser de commandes vocales système telles que «SELECT» ou «Hey Cortana» comme commandes personnalisées. Voici quelques points à prendre en compte:
1. **Évitez d’utiliser des commandes similaires.** Cela peut éventuellement déclencher une commande incorrecte.
2. **Choisissez des mots phonétiquement enrichis lorsque cela est possible.** Cela permet de réduire et/ou d’éviter les fausses activations.

### <a name="peripherals"></a>Périphériques

Les utilisateurs peuvent interagir avec votre application via des [périphériques](hardware-accessories.md). Les applications n’ont rien à faire pour tirer parti de cette fonctionnalité. Toutefois, il y a deux choses qui méritent d’être vérifiées.
1. **Validez les interactions personnalisées.** Des raccourcis clavier personnalisés pour votre application.
2. **Validez le basculement des types d’entrée.** Tentative d’utilisation de plusieurs méthodes d’entrée pour effectuer une tâche, telle que la voix, le mouvement, la souris et le clavier dans le même scénario.

## <a name="system-integration"></a>Intégration du système

### <a name="battery"></a>Batterie

Testez votre application sans une source d’alimentation connectée pour comprendre la vitesse à laquelle elle draine la batterie. L’un peut facilement comprendre l’état de la batterie en examinant les lectures de LED d’alimentation. ![États LED qui indiquent la puissance de la batterie](images/batterypowerledindication-500px.png)

### <a name="power-state-transitions"></a>Transitions d’état d’alimentation

Les scénarios de validation de clé fonctionnent comme prévu lors de la transition entre les États d’alimentation. Par exemple, l’application reste-t-elle à sa position d’origine? Conserve-t-il son état correctement? Continue-t-elle à fonctionner comme prévu?
1. **Veille/reprise.** Pour entrer en mode veille, vous pouvez appuyer sur le bouton d’alimentation et le relâcher immédiatement. L’appareil entrera également en veille automatiquement après 3 minutes d’inactivité. Pour reprendre en mode veille, vous pouvez appuyer sur le bouton d’alimentation et le relâcher immédiatement. L’appareil reprend également si vous le connectez ou le déconnectez d’une source d’alimentation.
2. **Arrêt/redémarrage.** Pour arrêter, appuyez sur le bouton d’alimentation et maintenez-le enfoncé pendant 6 secondes. Pour redémarrer, appuyez sur le bouton d’alimentation.

### <a name="multi-app-scenarios"></a>Scénarios à plusieurs applications

Validez les fonctionnalités principales de l’application lors du basculement entre les applications, en particulier si vous avez implémenté une tâche en arrière-plan. Le copier/coller et l’intégration Cortana méritent également de vérifier le cas échéant.

## <a name="telemetry"></a>Télémétrie

Utilisez les données de télémétrie et les analyses pour vous guider. L’intégration d’Analytics dans votre application vous aide à obtenir des informations sur votre application auprès de vos testeurs et utilisateurs finaux. Ces données peuvent être utilisées pour optimiser votre application avant son envoi au Windows Store et pour les futures mises à jour. Il existe de nombreuses options d’analyse. Si vous n’êtes pas sûr de l’emplacement de départ, consultez [application Insights](https://www.visualstudio.com/products/application-insights-vs.aspx).

Questions à prendre en compte:
1. Comment les utilisateurs utilisent-ils l’espace?
2. Comment l’application place-t-elle des objets dans le monde-peut-il détecter des problèmes?
3. Combien de temps consacrez-vous aux différentes étapes de l’application?
4. Combien de temps consacrez-vous à l’application?
5. Quels sont les chemins d’utilisation les plus courants que les utilisateurs essaient?
6. Les utilisateurs atteignent-ils des États et/ou des erreurs inattendus?

## <a name="emulator-and-simulated-input"></a>Émulateur et entrée simulée

L' [émulateur HoloLens](using-the-hololens-emulator.md) est un excellent moyen de tester efficacement votre application holographique avec une variété de caractéristiques et d’espaces simulés pour l’utilisateur. Voici quelques suggestions pour utiliser efficacement l’émulateur pour tester votre application:
1. **Utilisez les salles virtuelles de l’émulateur pour développer vos tests.** L’émulateur est fourni avec un ensemble de salles virtuelles que vous pouvez utiliser pour tester votre application dans encore plus d’environnements.
2. **Utilisez l’émulateur pour examiner votre application à partir de tous les angles.** Les clés PageUp/PageDn rendent votre utilisateur simulé plus grand ou plus petit.
3. **Testez votre application avec un véritable HoloLens.** L’émulateur HoloLens est un excellent outil pour vous aider à itérer rapidement sur une application et à intercepter de nouveaux bogues, mais veillez également à effectuer des tests sur un HoloLens physique avant de l’envoyer au Windows Store. Il est important de s’assurer que les performances et l’expérience sont importantes sur du matériel réel.

## <a name="automated-testing-with-perception-simulation"></a>Tests automatisés avec simulation de perception

Certains développeurs d’applications peuvent souhaiter automatiser les tests de leurs applications. Au-delà des tests unitaires simples, vous pouvez utiliser la pile de [simulation de perception](perception-simulation.md) dans HoloLens pour automatiser l’entrée humaine et mondiale dans votre application. L’API de simulation de perception peut envoyer une entrée simulée à l’émulateur HoloLens ou à un HoloLens physique.

## <a name="windows-app-certification-kit"></a>Kit de certification des applications Windows

Pour permettre à votre application d’être [publiée dans le Windows Store](submitting-an-app-to-the-microsoft-store.md), validez-la et testez-la localement avant de la soumettre à la certification. Si votre application cible la famille d’appareils Windows. holographique, le [Kit de certification des applications Windows](https://msdn.microsoft.com/library/windows/apps/xaml/mt186449.aspx) exécutera uniquement les tests d’analyse statique locaux sur votre PC. Aucun test ne sera exécuté sur votre HoloLens.

## <a name="see-also"></a>Voir aussi
* [Envoi d’une application au Windows Store](submitting-an-app-to-the-microsoft-store.md)
