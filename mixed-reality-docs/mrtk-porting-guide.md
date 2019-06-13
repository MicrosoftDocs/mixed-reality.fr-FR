---
title: Préparation d’une application pour HoloLens 2
description: S’adresse aux développeurs qui disposent déjà d’une application HoloLens (1ère génération) et/ou d’une ancienne version de MRTK, et qui souhaitent effectuer le portage de MRTK version 2 vers HoloLens 2.
author: grbury
ms.author: grbury
ms.date: 04/12/19
ms.topic: article
ms.localizationpriority: high
keywords: Windows Mixed Reality, test, MRTK, MRTK version 2, HoloLens 2
ms.openlocfilehash: 02dabd21b7a6add2ce53fe291a447e49057184d0
ms.sourcegitcommit: f20beea6a539d04e1d1fc98116f7601137eebebe
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66270392"
---
# <a name="getting-your-existing-app-ready-for-hololens-2"></a>Préparation d’une application existante pour HoloLens 2

Ce guide a été spécialement conçu pour aider les développeurs qui disposent d’une application Unity pour HoloLens (1ère génération) à effectuer le portage de leur application vers le nouvel appareil HoloLens 2. Le portage d’une application Unity pour HoloLens (1ère génération) vers HoloLens 2 comprend quatre étapes clés. Les sections ci-dessous expliquent en détail chacune de ces étapes. 

| Étape 1 | Étape 2 | Étape 3 | Étape 4 |
|----------|-------------------|-------------------|-------------------|
| ![Logo Visual Studio](images/visualstudio_logo.png) | ![Logo Unity](images/unity_logo.png)| ![Icône Unity](images/hololens2_icon.jpg) | ![Logo MRTK](images/MRTKIcon.jpg) |
| Télécharger les derniers outils | Mettre à jour un projet Unity | Compiler pour ARM | Effectuer une migration vers MRTK v2

Avant de démarrer le processus de portage, il est **vivement recommandé** aux développeurs d’utiliser le contrôle de code source afin d’enregistrer un instantané de l’état d’origine de leur application. En outre, il est recommandé d’*enregistrer* les états des points de contrôle à différents stades du processus. Le fait de disposer d’une autre instance Unity de l’application d’origine peut vous être très utile, car cela vous permet d’effectuer une comparaison côte à côte au cours du processus de portage. 

> [!NOTE]
> Avant d’effectuer le portage, vérifiez que vous avez installé les derniers outils de développement Windows Mixed Reality. Pour la plupart des développeurs HoloLens, il s’agira principalement d’effectuer une mise à jour vers la dernière version de Visual Studio 2017 et d’installer le SDK Windows correspondant. Le contenu ci-dessous offre une présentation détaillée des différentes versions de Unity et de MRTK version 2.
>
> Pour plus d’informations, consultez [Installer les outils](install-the-tools.md).

## <a name="migrate-project-to-latest-version-of-unity"></a>Effectuer la migration d’un projet vers la dernière version de Unity

Si vous utilisez MRTK v2, Unity 2018 LTS sera le chemin de prise en charge le mieux adapté dans le long terme, car il ne nécessite aucune modification importante dans Unity ou MRTK.  Selon la section « Installer les outils » mentionnée plus haut, la build Unity recommandée est la build 2018.3, qui deviendra la version LTS pour Unity 2018.  En outre, MRTK v2 garantit la prise en charge de Unity 2018 LTS, mais pas nécessairement celle de chaque itération de Unity 2019.x. 

Vous trouverez ci-dessous la liste des différences entre Unity 2018.3.x et Unity 2019.1.x, la principale étant la capacité d’Unity 2019 à compiler pour ARM64. 

Les développeurs doivent évaluer les [dépendances de plug-ins](https://docs.unity3d.com/Manual/Plugins.html) de leur projet afin de déterminer si ces DLL peuvent être créées pour ARM64. Si un plug-in avec dépendance dure ne peut pas être créé pour ARM64, vous devrez utiliser Unity 2018 LTS.


| Unity 2018.3.x | Unity 2019.1+ |
|----------|-------------------|
| Prise en charge de la build ARM32 | Prise en charge des builds ARM32 et ARM64 |
| Build LTS stable | Stabilité de la version bêta |
| [Back-end d’écriture de scripts .NET](https://docs.unity3d.com/Manual/windowsstore-dotnet.html) *déprécié* | [Back-end d’écriture de scripts .NET](https://docs.unity3d.com/Manual/windowsstore-dotnet.html) *supprimé* |
| Réseau UNet *déprécié* | Réseaux UNet *supprimé* |

## <a name="update-sceneproject-settings-in-unity"></a>Mettre à jour les paramètres de scène et de projet dans Unity

Après la mise à jour vers Unity 2018.3.x ou Unity 2019+, il est recommandé de mettre à jour certains paramètres Unity pour des résultats optimaux sur l’appareil. Ces paramètres sont décrits en détail sous **[Paramètres recommandés pour Unity](Recommended-settings-for-Unity.md)** .

Pour rappel, le [back-end d’écriture de scripts .NET](https://docs.unity3d.com/Manual/windowsstore-dotnet.html) est déprécié dans Unity 2018, et il a été *supprimé* dans Unity 2019. Les développeurs sont donc encouragés à transférer leur projet vers [IL2CPP](https://docs.unity3d.com/Manual/IL2CPP.html). 

> [!NOTE]
> Il est possible que le back-end d’écriture de code IL2CPP entraîne des temps de génération plus longs entre Unity et Visual Studio. Les développeurs doivent donc configurer leur ordinateur de développement de manière à [optimiser les temps de génération IL2CPP](https://docs.unity3d.com/Manual/IL2CPP-OptimizingBuildTimes.html).
> En outre, il peut être avantageux de configurer un [serveur de cache](https://docs.unity3d.com/Manual/CacheServer.html), en particulier pour les projets Unity qui comprennent une grande quantité de ressources (à l’exclusion des fichiers de script), et pour les scènes ou ressources qui changent constamment. Lorsque vous ouvrez un projet, Unity stocke les ressources éligibles dans un format de cache interne sur l’ordinateur de développement. Les éléments doivent être réimportés, et donc retraités, après modification. Ce processus peut être effectué une fois puis enregistré dans un serveur de cache. Pour gagner du temps, vous pouvez le partager avec les autres développeurs, plutôt que de demander à chaque développeur de réimporter localement les éléments modifiés.

Une fois qu’ils ont pris en compte les changements importants entraînés par la mise à jour de la version d’Unity, les développeurs doivent générer et tester leurs applications sur HoloLens (1ère génération). En outre, il est utile de créer et d’enregistrer une validation du contrôle de code source. 

## <a name="compile-dependenciesplugins-for-arm-processor"></a>Compiler des dépendances ou des plug-ins pour processeurs ARM

HoloLens (1ère génération) exécutait les applications sur un processeur x86 alors que le nouvel appareil HoloLens 2 utilise un processeur ARM. Par conséquent, les applications existantes doivent être portées en vue de prendre en charge ARM. Comme nous l’avons vu précédemment, Unity 2018 prend en charge la compilation des applications ARM32, alors qu’Unity 2019+ prend en charge la compilation des applications ARM64. En général, il est recommandé de développer des applications ARM64, car celles-ci fournissent de meilleures performances. Toutefois, cela nécessite que toutes les [dépendances de plug-ins](https://docs.unity3d.com/Manual/Plugins.html) soient également conçues pour ARM64. 

Passez en revue toutes les dépendances DLL qui se trouvent actuellement dans votre application. Si vous n’avez plus besoin de l’une de ces dépendances, il est recommandé de la supprimer du projet. Pour les autres plug-ins nécessaires, ingérez les fichiers binaires ARM32 ou ARM64 dans votre projet Unity. 

Après l’ingestion des DLL nécessaires, créez une solution Visual Studio dans Unity, puis compilez un AppX pour ARM dans Visual Studio, afin de vérifier si votre application peut être conçue pour les processeurs ARM. Là encore, il est conseillé d’enregistrer une validation de votre solution de contrôle de code source. 

## <a name="update-to-mrtk-version-2"></a>Effectuer une mise à jour vers MRTK version 2

MRTK version 2 est le nouveau kit de ressources pour Unity qui prend en charge à la fois HoloLens (1ère génération) et HoloLens 2. Il comprend toutes les nouvelles fonctionnalités de HoloLens 2, telles que l’interaction manuelle et la fonction de « eye tracking ».

### <a name="prepare-for-the-migration"></a>Se préparer à la migration

Avant d’ingérer les nouveaux [fichiers *.unitypackage pour MRTK v2](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases), il est recommandé d’effectuer un inventaire de **1) tout code personnalisé intégré à MRTK v1** et **2) tout code personnalisé pour les interactions d’entrée ou les composants d’expérience utilisateur**. Lors de l’ingestion de MRTK v2, le conflit le plus fréquemment rencontré par les développeurs de réalité mixte concerne les entrées et les interactions. Par conséquent, nous vous recommandons de lire l’article concernant le [modèle d’entrée MRTK v2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Overview.html).

Enfin, MRTK v2 est passé d’un modèle de scripts et d’objets gestionnaires en scène à une architecture de configuration et de fournisseur de services. La hiérarchie de scène et le modèle d’architecture sont désormais plus propres. Toutefois, ce changement nécessite que vous compreniez les nouveaux profils de configuration. Pour cela, lisez le [Guide de configuration de Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/MixedRealityConfigurationGuide.html) afin de vous familiariser avec les profils et les paramètres importants que vous devez adapter aux besoins de votre application. 

### <a name="perform-the-migration"></a>Effectuer la migration

Après l’importation de MRTK v2, votre projet Unity comprendra probablement plusieurs erreurs liées au compilateur. La plupart du temps, ces erreurs sont dues à la nouvelle structure des espaces de noms et aux nouveaux noms de composants. Pour corriger ces erreurs, dans vos scripts, remplacez les anciens espaces de noms et composants par les nouveaux. 

Pour en savoir plus sur les différences entre HTK/MRTK et MRTK version 2 au niveau des API, consultez le guide de portage sur le [wiki MRTK Version 2](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/HTKToMRTKPortingGuide.html).

### <a name="best-practices"></a>Meilleures pratiques

- Privilégier l’utilisation du nuanceur MRTK Standard
- Travailler sur un seul changement important à la fois (par exemple, passer de IFocusable à IMixedRealityFocusHandler)
- Effectuer des tests après chaque modification et utiliser le contrôle de code source
- Utiliser l’expérience utilisateur MRTK par défaut (boutons, fenêtres, etc.) lorsque cela est possible
- Éviter de modifier directement les fichiers MRTK. Pour cela, ajouter des wrappers autour des composants MRTK.
    - Ceci empêchera toute future mise à jour ou ingestion de MRTK.
- Explorer les exemples de scènes fournis dans MRTK (surtout *HandInteractionExamples.scene*)
- Recréer une interface utilisateur basée sur les canevas avec des quadrants, des colliders et du texte TextMeshPro

### <a name="testing-your-application"></a>Tester votre application

Maintenant que les composants et les fonctionnalités HoloLens 2 sont disponibles dans MRTK version 2, à compter de la version [RC1](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases/tag/v2.0.0-RC1), vous pouvez simuler les interactions manuelles directement dans Unity et développer à l’aide des nouvelles API d’interaction manuelle et d’eye tracking.  L’appareil HoloLens 2 doit créer une expérience optimale, que vous pouvez découvrir en explorant les outils et la documentation. En outre, MRTK v2 prend en charge le développement sur HoloLens 1ère génération. Par conséquent, les modèles d’entrée traditionnels, comme la sélection via un clic aérien, peuvent encore être testés sur les appareils HoloLens 1ère génération. 

## <a name="updating-interaction-model-for-hololens-2"></a>Mise à jour du modèle d’interaction pour HoloLens 2

Une fois que vous avez procédé au portage et à la préparation de votre application pour HoloLens 2, vous êtes prêt pour la mise à jour de votre modèle d’interaction et de vos conceptions et positionnements d’hologrammes.
Étant donné qu’elle provient de HoloLens (1ère génération), votre application comprend probablement un modèle d’interaction de type « Suivi et validation », avec des hologrammes relativement lointains qui rentrent entièrement dans le champ de vision.

Voici les étapes permettant d’optimiser la conception de votre application pour HoloLens 2 :
1.  Composants MRTK : En fonction du travail préalable, si vous avez ajouté MRTK v2, vous pourrez tirer parti de plusieurs composants ou scripts conçus et optimisés pour HoloLens 2.

2.  Modèle d’interaction : Envisagez de mettre à jour votre modèle d’interaction.  Pour la plupart des scénarios, nous vous recommandons de passer du modèle « Suivi et validation » au modèle d’interaction manuelle.  Étant donné que les hologrammes sont généralement hors de portée, le passage à l’interaction manuelle permettra des rayons de pointage plus lointains et des mouvements de saisie.
Remarque : Dans certains cas, un modèle d’interaction de type « mains libres » est nécessaire. C’est le cas, par exemple, pour les ouvriers qui doivent tenir des outils. Pour ces cas de figure, des instructions spécifiques sont fournies pour la conception. 

3.  Positionnement des hologrammes : Une fois que vous êtes passé au modèle d’interaction manuelle, vous pouvez rapprocher les hologrammes afin d’interagir directement avec eux à l’aide de vos mains, en utilisant des mouvements de saisie.  Les types d’hologrammes qu’il est recommandé de rapprocher dans le but de les manipuler directement sont les menus, les contrôles et les boutons de petite taille, ainsi que les hologrammes qui rentrent entièrement dans le champ de vision HoloLens 2 lorsque vous les manipulez ou les inspectez.
<br>
Les applications et les scénarios ont tous leurs propres spécificités. Nous continuerons donc de fournir des instructions de conception adaptées à chaque situation, en nous basant sur vos commentaires et sur vos expériences.


## <a name="additional-learnings-from-moving-apps-from-x86-to-arm"></a>Autres points importants concernant le passage de x86 à ARM

- Les applications Unity standard sont simples, car vous pouvez créer un bundle appx ARM et le déployer directement sur l’appareil.
Les difficultés arrivent lorsque l’application Unity utilise des plug-ins natifs.  Tous les plug-ins natifs doivent être mis à niveau vers Visual Studio 2017 puis recréés pour ARM ou mis à niveau vers Unity 2019 pour ARM64.

- Une application utilisait le plug-in AudioKinetic Wwise pour Unity, et la version utilisée ne comprenait pas de plug-in UWP/ARM. Plusieurs jours de travail ont été nécessaires pour que le son de l’application fonctionne sur ARM.

- Dans d’autres cas, il n’y avait aucun plug-in UWP/ARM pour les plug-ins exigés par l’application, ce qui empêchait le portage et l’exécution de l’application sur HoloLens 2.  Un engagement auprès du fournisseur de plug-in peut être nécessaire pour débloquer et prendre en charge ARM.

- Dans les nuanceurs, minfloat (et ses variantes telles que min16float, minint, etc.) peuvent ne pas avoir le même comportement dans HoloLen 2 que dans HoloLens (1ère génération). Ceux-ci ont pour but de garantir que le nombre de bits spécifié sera utilisé (au minimum). Avec les processeurs graphiques Intel/Nvidia, ils sont le plus souvent traités comme des 32 bits. Sur ARM, le nombre de bits spécifié est respecté. Dans la pratique, cela signifie que les nombres peuvent avoir une précision moindre dans HoloLens 2 que dans HoloLens (1ère génération).

- Les instructions _asm ne semblent pas fonctionner sur ARM, ce qui signifie que tout code utilisant les instructions _asm doit être réécrit.

- Le jeu d’instructions SIMD n’est pas pris en charge sur ARM. Cela signifie que plusieurs en-têtes, comme xmmintrin.h, emmintrin.h, tmmintrin.h et immintrin.h, ne sont pas disponibles sur ARM.

- Sur ARM, le compilateur du nuanceur est exécuté lors du premier appel de dessin, après le chargement du nuanceur ou après la modification d’un élément dont dépend le nuanceur, mais pas au moment du chargement du nuanceur. L’impact sur le taux de trames peut être très visible, en fonction du nombre de nuanceurs qui doivent être compilés. Cela a plusieurs impacts sur la façon dont les nuanceurs doivent être gérés, empaquetés et mis à jour sur HoloLens 2, par rapport à HoloLens (1ère génération).

## <a name="see-also"></a>Voir également
* [Bien démarrer avec MRTK v2](mrtk-getting-started.md)
* [Guide pratique concernant MRTK version 2](https://microsoft.github.io/MixedRealityToolkit-Unity/External/HowTo/README.html)
* [Installer les outils](install-the-tools.md)
* [Paramètres recommandés pour Unity](recommended-settings-for-unity.md)
* [Comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)

