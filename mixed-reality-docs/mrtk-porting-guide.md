---
title: Préparation de votre application pour HoloLens 2
description: Destiné aux développeurs qui disposent d’une application existante sur HoloLens (1er gen) et/ou anciennes MRTK et la recherche vers le port MRTK version 2 et HoloLens 2.
author: author:grbury
ms.author: grbury
ms.date: 04/12/19
ms.topic: article
keywords: Windows Mixed Reality, tester, MRTK, MRTK version 2, HoloLens 2
ms.openlocfilehash: a5a329f69f5f9cc64666483adc92786ae8910b2f
ms.sourcegitcommit: 07773e094ace2e828e329bd55da759983be3b8c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59597200"
---
# <a name="getting-your-existing-app-ready-for-hololens-2"></a>Préparation de votre application existante pour HoloLens 2

Ce guide est conçu spécialement pour aider les développeurs qui disposent d’une application Unity pour 1 HoloLens porter leur application pour le nouvel appareil HoloLens 2. Il existe quatre étapes clés pour le portage d’une application de HoloLens 1 Unity pour HoloLens 2. Les sections ci-dessous décrit en détail les informations pour chaque phase. 

| Étape 1 | Étape 2 | Étape 3 | Étape 4 |
|----------|-------------------|-------------------|-------------------|
| ![Logo Visual Studio](images/visualstudio_logo.png) | ![Logo de Unity](images/unity_logo.png)| ![Icône de Unity](images/hololens2_icon.jpg) | ![Logo MRTK](images/MRTKIcon.jpg) |
| Téléchargez les outils les plus récents | Mettre à jour de projet Unity | Compiler pour ARM | Migrer vers MRTK v2

Il est **hautement recommandé** que, avant de commencer le processus de portage, les développeurs d’utiliser le contrôle de code source pour enregistrer un instantané de l’état d’origine de leur application. En outre, il est recommandé de *enregistrer* États de point de contrôle à différents stades au cours du processus. Il peut également être très utile de disposer d’une autre instance de Unity de l’application d’origine pour faciliter la comparaison de côte à côte au cours du processus de port. 

> [!NOTE]
> Avant de porter, assurez-vous de qu'avoir les derniers outils installés pour le développement Windows Mixed Reality. Pour la plupart des développeurs HoloLens existant, ce qui impliquera principalement la mise à jour vers la dernière version de Visual Studio 2017 et en installant le Kit de développement logiciel Windows approprié. Le contenu ci-dessous offre une présentation détaillée les différentes versions de Unity et de la version 2 de la boîte à outils de réalité mixte.
>
> Pour plus d’informations, consultez [installer les outils](install-the-tools.md).

## <a name="migrate-project-to-latest-version-of-unity"></a>Migrer un projet à la dernière version de Unity

La première étape pour le portage de votre application Unity seront pour l’ouvrir dans la dernière version de Unity. Actuellement, il existe deux options : Unity 2018.3.x ou bêta de 2019.1.x Unity. Il existe plusieurs compromis entre ces deux versions, mais la principale différence de l’argument précision est la possibilité de compiler pour ARM64 dans Unity 2019 +. 

Les développeurs doivent évaluer les [les dépendances de plug-in](https://docs.unity3d.com/Manual/Plugins.html) qui existent actuellement dans leur projet et ou non ces DLL peut être générées pour ARM64. Si un plug-in de dépendance dure ne peut pas être généré pour ARM64, un avoir utiliser Unity 2018 LTS. Portage vers ARM64 est généralement souhaitée, si possible, car il existe de nombreuses améliorations des performances visibles sur l’appareil par rapport à ARM32.

En outre, le Toolkit de réalité mixte V2 sera toujours garantir la prise en charge de Unity 2018 LTS, mais pas nécessairement garantir la prise en charge pour chaque itération de Unity 2019.x+. 

| Unity 2018.3.x | Unity 2019.1 + |
|----------|-------------------|
| Prise en charge de la build ARM32 | ARM32 et ARM64 build prise en charge |
| LTS stables build mise en production | Stabilité de la version bêta |
| [Écriture de scripts .NET principal](https://docs.unity3d.com/Manual/windowsstore-dotnet.html) *déconseillée* | [Écriture de scripts .NET principal](https://docs.unity3d.com/Manual/windowsstore-dotnet.html) *supprimé* |
| La mise en réseau UNET *déconseillée* | La mise en réseau UNET *supprimé* |

## <a name="update-sceneproject-settings-in-unity"></a>Mettre à jour les paramètres de scène/projet dans Unity

Après la mise à jour à Unity 2018.3.x ou Unity 2019 +, il est recommandé de mettre à jour des paramètres particuliers dans Unity pour des résultats optimaux sur l’appareil. Ces paramètres sont décrites en détail sous  **[paramètres recommandés pour Unity](Recommended-settings-for-Unity.md)**.

Il doit être ré-itérée qui le [scripts .NET principal](https://docs.unity3d.com/Manual/windowsstore-dotnet.html) est déconseillé dans Unity 2018 et *supprimé* dans Unity 2019 et par conséquent, les développeurs doivent fortement envisager de basculer leur projet vers [ IL2CPP](https://docs.unity3d.com/Manual/IL2CPP.html). 

> [!NOTE]
> IL2CPP script principal peut entraîner des temps de génération à partir d’Unity pour Visual Studio et donc les développeurs doivent configurer leur ordinateur de développeur pour [optimisation de la durée de génération IL2CPP](https://docs.unity3d.com/Manual/IL2CPP-OptimizingBuildTimes.html).

Après avoir corrigé les modifications avec rupture après le passage à la version Unity mis à jour, les développeurs doivent générer et tester leurs applications en cours sur HoloLens (1er gen). En outre, il s’agit d’un bon point pour créer et enregistrer une validation pour le contrôle de code source. 

## <a name="compile-dependenciesplugins-for-arm-processor"></a>Compiler des dépendances/plug-ins pour les processeurs ARM

HoloLens (1er gen) exécutée des applications sur un x86 processeur alors que le nouvel appareil HoloLens 2 utilise un processeur ARM. Les applications existantes doivent doivent être portés sur pour prendre en charge ARM. Comme indiqué précédemment, Unity 2018 prend en charge la compilation pour les applications ARM32 de Unity 2019 + prend en charge la compilation pour les applications ARM64. Développement pour les applications ARM64 est généralement préférée car il existe une différence notable des performances. Toutefois, cela nécessite toutes [les dépendances de plug-in](https://docs.unity3d.com/Manual/Plugins.html) doit également être générée pour ARM64. 

Passez en revue toutes les dépendances DLL dans votre application actuellement. Si une dépendance n’est plus nécessaire, il est recommandé pour le supprimer de votre projet. Pour plug-ins restants qui sont requises, l’ingestion les binaires ARM32 ou ARM64 respectifs dans votre projet Unity. 

Après avoir reçu les DLL appropriées, générer une solution Visual Studio à partir d’Unity et puis compilez un AppX pour ARM dans Visual Studio pour tester que votre application peut être générée pour les processeurs ARM. Ce point un autre dans lequel il est conseillé d’enregistrer une validation dans votre solution de contrôle de code source. 

## <a name="update-to-mrtk-version-2"></a>Mettre à jour vers MRTK version 2

MRTK version 2 est la nouvelle boîte à outils sur Unity prenant en charge les deux HoloLens (1er gen) et 2 HoloLens, et où toutes les nouvelles fonctionnalités de HoloLens 2 ont été ajoutés, tels que remettez les interactions et suivi des yeux.

### <a name="prepare-for-the-migration"></a>Préparer la migration

Avant la réception de la nouvelle [fichiers *.unitypackage MRTK v2](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases), il est recommandé d’effectuer un inventaire de **1) n’importe quel code personnalisée qui s’intègre à MRTK v1** et **(2) n’importe quel code personnalisée pour les interactions d’entrée ou de composants de l’expérience utilisateur**. Les plus courants et répandu conflit pour un développeur de réalité mixte ingestion le nouveau v2 MRTK impliquera des entrées et interactions. Par conséquent, nous vous recommandons de commencer la lecture et la compréhension du [modèle d’entrée de v2 MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html).

Enfin, le nouveau v2 MRTK est passée d’un modèle de scripts et des objets de scène manager à une configuration et l’architecture de fournisseur de services. Cela entraîne un modèle d’architecture et de la hiérarchie de scène plus propre, mais nécessite une courbe d’apprentissage pour comprendre les nouveaux profils de configuration. Par conséquent, veuillez lire le [Guide de Configuration de kit de ressources de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) pour commencer à se familiariser avec les profils et les paramètres importants pour l’adapter aux besoins de votre application. 

### <a name="perform-the-migration"></a>Effectuer la migration

Après avoir importé MRTK v2, votre projet Unity aura probablement plusieurs erreurs liées au compilateur. Il s’agit généralement en raison de la nouvelle structure d’espace de noms et les nouveaux noms de composant. Passez à résoudre ces erreurs en modifiant vos scripts pour les nouveaux espaces de noms et les composants. 

Pour plus d’informations sur les différences d’API spécifiques entre HTK/MRTK et MRTK version 2, consultez le guide du portage sur le [MRTK Version 2 wiki](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html).

### <a name="best-practices"></a>Meilleures pratiques

- Préférez utiliser le nuanceur MRTK Standard
- Travail sur une rupture modifie le type à la fois (ex : IFocusable à IMixedRealityFocusHandler)
- Tester après chaque modification et d’utiliser le contrôle de code source
- Par défaut UX MRTK (boutons, tablettes tactiles, etc.) lorsque cela est possible
- Essayez de ne pas modifier directement les fichiers MRTK, au lieu de cela créer des wrappers autour des composants MRTK
    - Ceci ne vous protège contre les mises à jour et les futures ingestions MRTK
- Passez en revue et Explorer les scènes exemple fournis dans MRTK (surtout *HandInteractionExamples.scene*)
- Reconstruire basée sur le canevas de l’interface utilisateur avec quadrilatères, colliders et TextMeshPro texte à la place

### <a name="testing-your-application"></a>Test de votre application

Maintenant que HoloLens 2 composants et fonctionnalités sont disponibles dans MRTK version 2, comme de [RC1](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases/tag/v2.0.0-RC1), vous pouvez simuler les interactions main directement dans Unity et développer sur les nouvelles API pour les interactions de main et de suivi de le œil.  L’appareil HoloLens 2 est requis pour créer une expérience optimale, mais au moins l’un pourrait commencer une formation dans la documentation et outils. En outre, MRTK v2 prend en charge le développement sur HoloLens (1er gen) et par conséquent, entrée traditionnelle modélise telles que select via appui peut toujours être testées sur HoloLens (1er gen) des appareils. 

## <a name="updating-interaction-model-for-hololens-2"></a>La mise à jour de modèle d’interaction pour HoloLens 2

Une fois que vous avez porté et prêt pour HoloLens 2 votre application, vous êtes prêt à prendre en compte la mise à jour votre interaction modèle et hologramme conceptions ou de placement.
Provenant de HoloLens (1er gen), votre application probablement a un modèle d’interaction du pointage de regard et commit, avec hologrammes relativement loin pour tenir dans le champ de vision.

Étapes pour mettre à jour de votre conception de l’application sera la meilleure pour HoloLens 2 :
1.  Composants MRTK : Par le travail préalable, si vous avez ajouté MRTK v2, il existe différents composants/scripts de tirer parti de qui ont été conçues et optimisées pour HoloLens 2.

2.  Modèle d’interaction : Envisagez la mise à jour votre modèle d’interaction.  La plupart des scénarios, nous vous recommandons de passer à partir des regards et validez à des ateliers.  Avec votre hologrammes étant généralement hors des armes atteindre, l’à des ateliers de commutation entraîne des rayons pointage interaction lointain et saisir les mouvements.
Remarque : il existe des scénarios où un modèle d’interaction mains libres est requis, par exemple, un employé effectuant des tâches contenant les outils et conseils pratiques de conception spécifiques pour ces cas. 

3.  Sélection élective hologramme : Après avoir basculé vers un modèle d’interaction mains, passez quelques hologrammes plus proche d’interagir directement avec les hologrammes avec vos mains, à l’aide de près les mouvements de manipulation d’interaction.  Les types de hologrammes recommandées de se rapprocher de saisir directement ou d’interaction sont des menus de la cible de petite taille, des contrôles, des boutons et des hologrammes plus petites qui tiennent dans la champ HoloLens 2 de vue lorsqu’en saisissant et en inspectant l’hologramme.
<br>
Chaque application et le scénario sont différent, et nous continuerons à affiner et à valider la conception des conseils en fonction des commentaires et apprentissages de suite.


## <a name="additional-learnings-from-moving-apps-from-x86-to-arm"></a>Apprentissages supplémentaires d’une migration des applications à partir de x86 vers ARM

- Les applications Unity droites sont simples, comme vous pouvez créer une offre groupée d’appx ARM ou déployer directement sur l’appareil et il s’exécute.
Le défi est fourni lors de l’application Unity utilise des plug-ins natifs.  Tous les plug-ins natifs doivent être mis à niveau vers Visual Studio 2017 et recréés pour ARM et avec Unity 2019, ARM64.

- Une application, a utilisé le plug-in AudioKinetic Wwise pour Unity, et la version utilisée n’avait pas un plug-in UWP ARM. Il a fallu plusieurs jours à retravailler le son dans l’application de fonctionner sur ARM.

- Dans d’autres cas, un plug-in UWP/ARM n’existe pas pour l’application requise plug-ins, bloque la possibilité de déplacer et de s’exécuter sur HoloLens 2.  Engagement avec le fournisseur de plug-in peut être nécessaire de débloquer et de prendre en charge ARM.

- Minfloat (les variantes telles que min16float minint, etc.) dans les nuanceurs peuvent se comporter différemment sur 2 HoloLen que sur HoloLens (1er gen). Plus précisément, ces garantissent que « au moins le spécifié le nombre de bits sera utilisé ». Sur les processeurs graphiques Intel/Nvidia, ceux-ci sont en grande partie simplement assimilées à-32 bits. Sur ARM, le nombre de bits spécifié est réellement respecté. Cela signifie que dans la pratique, ces nombres ne peut avoir moins précision/plage sur HoloLens 2 que celles des HoloLens (1er gen).

- Les instructions _asm ne n’apparaissent pas pour travailler sur ARM, ce qui signifie que n’importe quel code en suivant les instructions _asm n’aura à réécrire.

- Le jeu d’instructions SIMD n’est pas pris en charge sur ARM. Cela signifie que différents en-têtes, telles que xmmintrin.h, emmintrin.h, tmmintrin.h et immintrin.h ne sont pas disponibles sur ARM.

- Le compilateur de nuanceur lors des exécutions ARM pendant le premier appel de dessin une fois que le nuanceur a été chargé ou quelque chose du nuanceur s’appuie sur a changé, pas au moment du chargement du nuanceur. L’impact sur la fréquence d’images peut être très sensible, en fonction de nuanceurs combien doivent être compilées. Ceci a des implications différentes pour comment nuanceurs doivent être gérées/empaqueté/mis à jour différemment sur HoloLens 2 vs HoloLens (1er gen).

## <a name="see-also"></a>Voir aussi
* [Prise en main MRTK version 2](mrtk-getting-started.md)
* [Comment faire pour la Version 2 de MRTK](https://microsoft.github.io/MixedRealityToolkit-Unity/External/HowTo/README.html)
* [Installer les outils](install-the-tools.md)
* [Paramètres recommandés pour Unity](recommended-settings-for-unity.md)
* [Comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)

