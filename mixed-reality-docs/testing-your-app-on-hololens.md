---
title: Test de votre application sur HoloLens
description: Des conseils et des suggestions pour tester votre application HoloLens
author: JonMLyons
ms.author: jlyons
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens, test
ms.openlocfilehash: 35e8eff230cdcd719952ad2633ec610c9a9a26a0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594215"
---
# <a name="testing-your-app-on-hololens"></a>Test de votre application sur HoloLens

Tester des applications HoloLens sont très similaires à tester les applications Windows. Toutes les zones habituels doivent être considérés (fonctionnalité, l’interopérabilité, performances, sécurité, fiabilité, etc.). Toutefois, il existe certaines zones nécessitant un traitement spécial ou aux détails qui ne sont pas généralement observées dans les applications PC ou téléphone. Applications HOLOGRAPHIQUE doivent fonctionner correctement dans un ensemble varié d’environnements. Ils doivent également tenir à jour le confort de performances et l’utilisateur à tout moment. Conseils pour tester ces domaines sont détaillée dans cette rubrique.

## <a name="performance"></a>Performances

Applications HOLOGRAPHIQUE doivent fonctionner correctement dans un ensemble varié d’environnements. Ils doivent également tenir à jour le confort de performances et l’utilisateur à tout moment. Performances sont donc important de l’expérience utilisateur avec une application HOLOGRAPHIQUE que nous avons un ensemble de la rubrique consacrée à celle-ci. Vérifiez que vous lire et suivez le [comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)

## <a name="testing-3d-in-3d"></a>Test 3D en 3D
1. **Testez votre application dans différents espaces autant que possible.** Essayez dans les salles big, petites pièces, salles de bain, cuisines, chambres, bureaux, etc. Prennent également en salles considération avec fonctionnalités non standard telles que les murs non verticales, murs courbes, les plafonds horizontales. Il fonctionne bien lors de la transition entre les salles de conversation, étages, passer par des couloirs ou escalier ?
2. **Testez votre application dans les conditions d’éclairage différentes.** Il répond correctement à différentes conditions d’environnement telles qu’éclairage, les surfaces noir transparent/réfléchissante surfaces comme miroirs, murs de verre, etc.
3. **Testez votre application dans des conditions de mouvement différent.** Placer sur l’appareil et essayez de vos scénarios dans différents États du mouvement. Réagit-il correctement pour le déplacement des différents ou un état stable ?
4. **Tester le fonctionnement de votre application sous différents angles.** Si vous avez un hologramme world verrouillé, que se passe-t-il si votre utilisateur présente derrière lui ? Que se passe-t-il si quelque chose arrive entre l’utilisateur et l’hologramme ? Que se passe-t-il si l’utilisateur présente l’hologramme d’au-dessus ou en dessous ?
5. **Utiliser des signaux audio et spatiales.** Assurez-vous que votre application utilise ces propriétés pour empêcher l’utilisateur d’être perdu.
6. **Testez votre application à différents niveaux de bruit ambiant.** Si vous avez implémenté des commandes vocales, essayez de les appeler avec différents niveaux de bruit ambiant.
7. **Tester votre application en place et la représentativité**. Veillez à tester à partir de la salle et les positions permanent.
8. **Tester votre application à partir de différentes distances**. Éléments d’interface utilisateur peuvent être lue et interagis avec de très loin ? Fait react de votre application pour les utilisateurs bien trop proche de votre hologrammes ?
9. **Tester votre application sur les interactions de barre application commune**. Toutes les vignettes des applications et des applications universelles 2D possèdent un [barre de l’application](navigating-the-windows-mixed-reality-home.md#moving-and-adjusting-apps) qui vous permet de contrôler la façon dont l’application est positionnée dans le monde mixte. Assurez-vous en cliquant sur Supprimer pour achever votre application normalement et que le bouton précédent est pris en charge dans le contexte de votre application universelle 2D. Mise à l’échelle de try et de déplacement de votre application dans [Adjust mode](navigating-the-windows-mixed-reality-home.md#moving-and-adjusting-apps) lorsqu’elle est active, et bien qu’il soit une vignette de l’application interrompue.

### <a name="environmental-test-matrix"></a>Matrice de l’environnement de Test

![Matrice de Test d’environnement pour le développement d’applications HoloLens](images/environment-matrix-600px.png)

## <a name="comfort"></a>Confort
1. **Plans de coupe.** Être attentif vers l’emplacement où [hologrammes sont rendus](hologram-stability.md#hologram-render-distances).
2. **Évitez de déplacement virtuel incohérent avec le mouvement réel de la tête.** Évitez de déplacer l’appareil photo d’une manière qui n’est pas représentative de mouvement réel de l’utilisateur. Si votre application requiert le déplacement de l’utilisateur via une scène, rendre le mouvement prévisible, réduire l’accélération et permettre à l’utilisateur de contrôler le déplacement.
3. **Suivez les instructions sur la qualité hologramme.** Applications performantes qui implémentent le [conseils de qualité hologramme](hologram-stability.md) sont moins susceptibles d’entraîner une gêne utilisateur.
4. **Distribuer hologrammes horizontalement plutôt que verticalement.** Forcer l’utilisateur à passer pendant de longues périodes de temps à rechercher ou vers le bas peut entraîner fatigue dans col.

## <a name="input"></a>Entrée

### <a name="gaze-and-gestures"></a>Regards et des mouvements

[Utilisation](gaze.md) est un formulaire de base d’entrée sur HoloLens permettant aux utilisateurs de visent à hologrammes et l’environnement. Vous pouvez visuellement voir où votre regard cible en fonction de la position du curseur. Il est courant d’associer le curseur du pointage de regard d’un curseur de la souris.

[Mouvements](gestures.md) vous permettent d’interagir avec hologrammes, comme un clic de souris. La plupart du temps les comportements de la souris et l’interaction tactile sont les mêmes, mais il est important de comprendre et à valider lorsqu’elles diffèrent.

**Valider si votre application dispose d’un comportement différent avec la souris et l’interaction tactile.** Cela identifie les incohérences et faciliter les décisions de conception pour rendre l’expérience plus naturel pour les utilisateurs. Par exemple, pour déclencher une action basée sur le pointage.

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

### <a name="custom-voice-commands"></a>Commandes vocales personnalisées

[Entrée voix](voice-input.md) est une forme naturelle d’interaction. L’expérience utilisateur peut être confus selon votre choix de commandes et la façon dont vous les exposez ou magique. En règle générale, vous ne devez pas utiliser les commandes vocales de système telles que « Select » ou « Hey Cortana » en tant que commandes personnalisées. Voici quelques points à prendre en compte :
1. **Évitez d’utiliser des commandes similaires.** Cette étape peut potentiellement déclencher la commande incorrecte.
2. **Choisissez des mots phonétiquement enrichies lorsque cela est possible.** Cela sera réduire et/ou éviter les activations false.

### <a name="peripherals"></a>Périphériques

Les utilisateurs peuvent interagir avec votre application via [périphériques](hardware-accessories.md). Les applications n’avez pas besoin de rien de spécial à tirer parti de cette fonctionnalité, cependant, il existe quelques points à examiner.
1. **Valider des interactions personnalisées.** Par exemple des raccourcis clavier personnalisés pour votre application.
2. **Valider les types d’entrée de commutation.** Tentative d’utilisation de plusieurs méthodes d’entrée pour effectuer une tâche, telles que la voix, mouvement, la souris et clavier dans le même scénario.

## <a name="system-integration"></a>Intégration de système

### <a name="battery"></a>Batterie

Tester votre application sans une source d’alimentation pour comprendre la vitesse à laquelle il draine la batterie. Un peut facilement comprendre l’état de la batterie en examinant les relevés de LED d’alimentation. ![États de LED qui indiquent la puissance de la batterie](images/batterypowerledindication-500px.png)

### <a name="power-state-transitions"></a>Transitions d’état d’alimentation

Valider le travail des scénarios clés comme prévu lors de la transition entre les États d’alimentation. Par exemple, l’application ne reste pas à sa position d’origine ? Conserve son état correctement ? Il continue à fonctionner comme prévu ?
1. **En veille / reprise.** Pour passer en mode veille, il est possible appuyez sur et relâchez le bouton d’alimentation immédiatement. L’appareil sera également passer en mode veille automatiquement au bout de 3 minutes d’inactivité. Pour sortir du mode veille, il est possible appuyez sur et relâchez le bouton d’alimentation immédiatement. L’appareil reprend également si vous vous connectez ou vous déconnecter à partir d’une source d’alimentation.
2. **Arrêter / redémarrer.** Pour arrêter, maintenez le bouton d’alimentation en continu pendant 6 secondes. Pour redémarrer, appuyez sur le bouton d’alimentation.

### <a name="multi-app-scenarios"></a>Scénarios d’applications multiples

Valider les fonctionnalités principales de l’application lors du passage entre les applications, en particulier si vous avez implémenté une tâche en arrière-plan. Copier/coller et intégration de Cortana valent également la vérification, le cas échéant.

## <a name="telemetry"></a>Télémétrie

Utilisation de la télémétrie et analytique qui vous guideront. L’intégration analytique dans votre application vous aidera à obtenir des informations relatives à votre application à partir de vos bêta-testeurs et les utilisateurs finaux. Ces données peuvent être utilisées pour aider à optimiser votre application avant la soumission pour le Store et pour les futures mises à jour. Il existe de nombreuses options d’analytique ici. Si vous ne savez pas où commencer, consultez [App Insights](https://www.visualstudio.com/products/application-insights-vs.aspx).

Questions à prendre en compte :
1. Comment les utilisateurs utilisent l’espace ?
2. Comment est l’application de placer des objets dans le monde - vous pouvez détecter des problèmes ?
3. Combien de temps passent-ils sur les différentes étapes de l’application ?
4. Combien de temps passent-ils sur l’application ?
5. Essayez de quelles sont les plus courantes chemins d’accès de l’utilisation les utilisateurs ?
6. Les utilisateurs rencontrez des erreurs et/ou d’états inattendues ?

## <a name="emulator-and-simulated-input"></a>Émulateur et entrée simulée

Le [HoloLens émulateur](using-the-hololens-emulator.md) est un excellent moyen pour tester efficacement votre application holographique avec un large éventail d’espaces et les caractéristiques de l’utilisateur simulé. Voici quelques suggestions pour efficacement à l’aide de l’émulateur pour tester votre application :
1. **Utiliser les salles virtuel de l’émulateur pour développer vos tests.** L’émulateur est fourni avec un ensemble de salles virtuels que vous pouvez utiliser pour tester votre application dans d’autres environnements.
2. **Utiliser l’émulateur pour examiner votre application à partir de tous les angles.** Les touches PG. préc. / PageDn fera de votre utilisateur simulé agrandir ou réduire.
3. **Testez votre application avec un véritable HoloLens.** L’émulateur de HoloLens est un excellent outil pour vous aider à rapidement itérer sur une application et intercepter les nouveaux bogues, mais veillez à également tester sur un HoloLens physique avant de les envoyer vers le Windows Store. Il est important de s’assurer que les performances et l’expérience sont très utiles sur du vrai matériel.

## <a name="automated-testing-with-perception-simulation"></a>Tests automatisés avec Simulation de Perception

Certains développeurs d’application peuvent souhaiter automatiser le test de leurs applications. Au-delà de tests unitaires simple, vous pouvez utiliser la [simulation de perception](perception-simulation.md) pile dans HoloLens pour automatiser une entrée humaine et monde à votre application. L’API de simulation de perception peut envoyer une entrée simulée à l’émulateur de HoloLens ou un HoloLens physique.

## <a name="windows-app-certification-kit"></a>Kit de certification des applications Windows

Donner à votre application les meilleures chances d’être [publié sur le Windows Store](submitting-an-app-to-the-microsoft-store.md), valider et tester localement avant de le soumettre pour certification. Si votre application cible de la famille de périphériques Windows.Holographic, le [Kit de Certification des applications Windows](https://msdn.microsoft.com/library/windows/apps/xaml/mt186449.aspx) s’exécuter uniquement les tests de l’analyse statique locale sur votre PC. Aucun test sera exécuté sur votre HoloLens.

## <a name="see-also"></a>Voir aussi
* [Soumission d’une application pour le Windows Store](submitting-an-app-to-the-microsoft-store.md)
