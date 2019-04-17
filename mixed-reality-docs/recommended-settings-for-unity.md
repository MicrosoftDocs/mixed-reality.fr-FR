---
title: Paramètres recommandés pour Unity
description: Unity propose certains comportements spécifiques à une réalité mixte qui peut être activé ou désactivée par le biais des paramètres de projet.
author: Troy-Ferrell
ms.author: trferrel
ms.date: 03/26/2019
ms.topic: article
keywords: Unity, les paramètres, réalité mixte
ms.openlocfilehash: a67c3a65819855be6d43941c05f9a0027abf2f6d
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594287"
---
# <a name="recommended-settings-for-unity"></a>Paramètres recommandés pour Unity

Unity fournit un ensemble d’options par défaut qui sont généralement le cas moyen pour toutes les plateformes. Toutefois, Unity propose certains comportements spécifiques à une réalité mixte qui peut être activé ou désactivée par le biais des paramètres de projet.

## <a name="performant-environment-set-up"></a>Configuration d’environnement performant

### <a name="low-quality-setting"></a>Paramètre de qualité inférieure

Il est important de modifier le **les paramètres de qualité de Unity** pour votre environnement à **plus « rapide »**. Cela permet de s’assurer que votre application s’exécute efficacement à la fréquence d’images appropriée. Ceci est extrêmement important pour le développement de Hololens. Pour le développement sur des casques IMMERSIFS, selon les spécifications du bureau mise sous tension de l’expérience de réalité virtuelle, un peut toujours obtenir une fréquence d’images sans les paramètres de qualité la plus basse. 

Dans Unity 2018 LTS +, le niveau de qualité du projet peut être défini :

Sous **modifier** > **paramètres du projet** > **qualité** > définir le **par défaut** en cliquant sur le flèche vers le bas pour le **Fastest** niveau de qualité

### <a name="single-pass-instancing-rendering-path"></a>Chemin d’accès de rendu instanciation unique pass

Dans les applications de réalité mixte, la scène est affichée à deux reprises, une fois pour chaque œil à l’utilisateur. Par rapport au développement 3D traditionnel, cela double efficacement la quantité de travail qui doit être calculée. Par conséquent, il est important de sélectionner le chemin d’accès plus efficace de rendu dans Unity pour enregistrer les deux sur le temps CPU et GPU. Rendu instanciées passage unique optimise le pipeline de rendu Unity pour les applications de réalité mixte et par conséquent, il est recommandé d’activer ce paramètre par défaut pour chaque projet. 

Pour activer cette fonctionnalité dans votre projet Unity
1)  Ouvrez **paramètres du lecteur XR** (accédez à **modifier** > **paramètres du projet** > **Player**  >  **XR paramètres**)
2) Sélectionnez **unique passer une instance créée** à partir de la **méthode de rendu stéréo** menu déroulant (**virtuel pris en charge de réalité** case doit être cochée)

Pour plus d’informations avec cette approche de rendu, lisez les articles suivants à partir d’Unity.
- [Comment optimiser les performances des AR et VR avec rendu stéréo avancé](https://blogs.unity3d.com/2017/11/21/how-to-maximize-ar-and-vr-performance-with-advanced-stereo-rendering/)
- [L’instanciation unique Pass](https://docs.unity3d.com/Manual/SinglePassInstancing.html) 

>[!NOTE]
> Un problème courant avec unique passer instancié rendu se produit si les développeurs ont déjà des nuanceurs personnalisés existants non écrits pour l’instanciation. Après avoir activé cette fonctionnalité, les développeurs remarquerez certains rendu uniquement GameObjects d’un oeil. Il s’agit comme les nuanceurs personnalisés associés n’ont pas les propriétés appropriées pour l’instanciation.
>
> Consultez [unique passer stéréo rendu pour HoloLens](https://docs.unity3d.com/Manual/SinglePassStereoRenderingHoloLens.html) à partir d’Unity pour savoir comment résoudre le problème

### <a name="enable-depth-buffer-sharing"></a>Activer le partage de mémoire tampon de profondeur

Pour obtenir une meilleure stabilité hologramme à partir de la perception de l’utilisateur, il est recommandé d’activer le **partage de mémoire tampon de profondeur** propriété dans Unity. En activant cette, Unity partageront la carte de profondeur générée par votre application avec la plateforme Windows Mixed Reality. La plateforme sera ensuite en mesure de mieux optimiser la stabilité hologramme spécifiquement pour votre scène pour une image donnée restituée par votre application.

Pour activer cette fonctionnalité dans votre projet Unity
1) Ouvrez **paramètres du lecteur XR** (accédez à **modifier** > **paramètres du projet** > **Player**  >  **XR paramètres**)
2) Activez la case à cocher pour **activer le partage de mémoire tampon de profondeur** sous **SDK de réalité virtuelle** > **Windows Mixed Reality** expansion (**virtuelle Prise en charge de la réalité** case doit être cochée)

En outre, il est recommandé de sélectionner **16 bits profondeur** sous le **profondeur Format** configuration dans ce panneau, en particulier pour le développement de Hololens. Sélection de 16 bits par rapport aux 24 bits réduit considérablement la bande passante car moins de données en aurez besoin être déplacée/traité.

>[!NOTE]
> Les développeurs doivent Méfiez-vous des Z fighting lorsque vous modifiez ces valeurs ainsi que les paramètres de plan proche/éloigné de la caméra. Z Fighting se produit lorsque deux gameobjects essayez restituer au même pixel et en raison des limitations de fidélité de la mémoire tampon de profondeur (ex.) profondeur z), Unity ne peut pas déterminer quel objet se trouve devant l’autre. Les développeurs note un scintillement entre deux objets de jeu en tant qu’ils *combattre* pour la même valeur z en profondeur. Pour résoudre ce problème en basculant vers le format de 24 bits profondeur comme il y aura une plus grande plage de valeurs pour chaque objet calculer lors de leur profondeur de z à partir de l’appareil photo.
>
> Toutefois, il est recommandé, en particulier pour Hololens développement, pour modifier l’appareil photo de près et beaucoup des plans à une plage plus petite à la place et en conservant la profondeur de 16 bits formater. La profondeur de z est non linéaire mappée à la plage de valeurs le long de l’appareil photo proches plans. Ce paramètre peut être modifié en sélectionnant le *Main Camera* dans votre scène et, sous **inspecteur**, modifier le **proche & beaucoup de plan de coupe** valeurs afin de réduire leur plage (ex.) à partir de 1 000 m à 100 m ou autre valeur x, etc.)

### <a name="building-for-il2cpp"></a>Création pour IL2CPP

Unity a déconseillé la prise en charge des scripts de serveur principal et donc aux développeurs il est recommandé d’utiliser .NET **IL2CPP** pour leur UWP visual studio génère. Bien que cela introduit des différents avantages, création de votre solution visual studio à partir d’Unity pour **Il2CPP** peut être plus lent que l’ancienne méthode .NET de façon significative. Par conséquent, il est vivement recommandé de suivre les pratiques recommandées pour bâtir **IL2CPP** à enregistrer sur le temps d’itération de développement.

1) Génération incrémentielle de tirer parti en créant votre projet dans le même répertoire chaque fois, réutiliser des il les fichiers prédéfinis
2) Désactiver les analyses de logiciels anti-programmes malveillants pour votre projet et créer des dossiers
   - Ouvrez **protection de Virus et menaces** sous votre application de paramètres de Windows 10
   - Sélectionnez **gérer les paramètres** sous **les paramètres de protection de Virus et menaces**
   - Sélectionnez **ajouter ou supprimer des exclusions** sous le **Exclusions** section
   - Cliquez sur **ajoutez une exclusion** et sélectionnez le dossier contient le code de votre projet Unity et générer fournit en sortie
3) Utiliser un disque SSD pour la génération

Veuillez lire [optimiser le temps de Build pour IL2CPP](https://docs.unity3d.com/Manual/IL2CPP-OptimizingBuildTimes.html) pour plus d’informations.

## <a name="publishing-properties"></a>Propriétés de publication

### <a name="holographic-splash-screen"></a>Écran de démarrage HOLOGRAPHIQUE

HoloLens a un mobile-classe CPU et GPU, ce qui signifie que les applications peuvent prendre un peu plus de temps à charger. Pendant le chargement de l’application, les utilisateurs voient seulement les noir, et donc, ils peuvent se demandent ce qui se passe. Pour les convaincre pendant le chargement, que vous pouvez ajouter un écran de démarrage HOLOGRAPHIQUE.

Pour activer/désactiver l’écran de démarrage HOLOGRAPHIQUE :
1) Accédez à **modifier** > **paramètres du projet** > **Player** page
2) Cliquez sur le **Windows Store** onglet et ouvrez le **Image de démarrage** section
3) Appliquer votre image de votre choix sous le **Windows HOLOGRAPHIQUE > Image de démarrage HOLOGRAPHIQUE** propriété.
    - Activation/désactivation du **afficher un écran de démarrage de Unity** option active ou désactive l’écran de démarrage personnalisée de Unity. Si vous n’avez pas une licence Pro Unity, l’écran de démarrage de la marque de Unity sera toujours affichée.
    - Si un **HOLOGRAPHIQUE Image de démarrage** est appliqué, il sera toujours affichée que la case à cocher Afficher un écran de démarrage de Unity soit activé ou désactivé. Spécification d’une image de démarrage HOLOGRAPHIQUE personnalisé est uniquement disponible pour les développeurs avec une licence Pro Unity.

|  Afficher l’écran de démarrage d’Unity  |  Image de démarrage HOLOGRAPHIQUE  |  Comportement |
|----------|----------|----------|
|  Activé  |  Aucune  |  Afficher l’écran de démarrage par défaut Unity 5 secondes ou jusqu'à ce que l’application est chargée, la plus longue étant retenue. | 
|  Activé  |  Custom  |  Afficher l’écran de démarrage personnalisé pendant 5 secondes, ou jusqu'à ce que l’application est chargée, la plus longue étant retenue. | 
|  Désactivé  |  Aucune  |  Afficher le noir transparent (nothing) jusqu'à ce que l’application est chargée. | 
|  Désactivé  |  Custom  |  Afficher l’écran de démarrage personnalisé pendant 5 secondes, ou jusqu'à ce que l’application est chargée, la plus longue étant retenue. | 

Veuillez lire [documentation d’écran de démarrage d’Unity](https://docs.unity3d.com/Manual/class-PlayerSettingsSplashScreen.html) pour plus d’informations.

### <a name="tracking-loss"></a>Suivi de la perte

Un casque de réalité mixte dépend de l’affichage de l’environnement autour de lui pour construire [systèmes de coordonnées world-verrouillé](coordinate-systems-in-unity.md), qui permettent à hologrammes reste en place. Quand le casque est incapable de localiser lui-même dans le monde, le casque est dite avoir *perdu suivi*. Dans ce cas, les fonctionnalités qui dépendent de systèmes de coordonnées world-verrouillé, tels qu’étapes spatiales, ancres spatiales et mappage spatial, ne fonctionnent pas.

Si une perte de suivi se produit, par défaut d’Unity consiste à arrêter hologrammes de rendu, de suspendre le [boucle du jeu](http://docs.unity3d.com/Manual/ExecutionOrder.html), et l’affichage de suivi perdu notification autrement confortablement suit le regard des utilisateurs. Notifications personnalisées peuvent également être fournies sous la forme d’un suivi image de perte. Pour les applications qui dépendent de suivi pour leur intégralité de l’expérience, il suffit d’Unity permettent de gérer cette situation complètement jusqu'à ce suivi est récupéré. Les développeurs peuvent fournir une image personnalisée à afficher pendant le suivi de la perte. 

Pour personnaliser l’image de perte de suivi :
1) Accédez à **modifier** > **paramètres du projet** > **Player** page
2) Cliquez sur le **Windows Store** onglet et ouvrez le **Image de démarrage** section
3) Appliquer votre image de votre choix sous le **Windows HOLOGRAPHIQUE > Image de perte de suivi** propriété.

#### <a name="opt-out-of-automatic-pause"></a>Annulations de pause automatique

Certaines applications peuvent ne pas exiger de suivi (par exemple, [applications orientation seule](coordinate-systems-in-unity.md) telles que les visionneuses de vidéo à 360 degrés) ou peut-être à continuer sans interruption pendant le suivi du traitement n’est perdu. Dans ces cas, les applications peuvent refuser la perte de valeur par défaut du comportement de suivi. Les développeurs qui choisissent cette sont responsables de masquage/la désactivation de tous les objets qui affichait pas correctement dans un scénario de perte de suivi. Dans la plupart des cas, seul le contenu qui est recommandé pour être rendu dans la mesure cas est verrouillé de corps de contenu, centrée autour de la caméra principale.

Pour désactiver le comportement de pause automatique :
1) Accédez à **modifier** > **paramètres du projet** > **Player** page
2) Cliquez sur le **Windows Store** onglet et ouvrez le **Image de démarrage** section
3) Modifier le **Windows HOLOGRAPHIQUE > sur Pause de perte de suivi et afficher l’Image** case à cocher.

#### <a name="tracking-loss-events"></a>Le suivi des événements de perte

Pour définir un comportement personnalisé en cas de perte de suivi, gérer global [le suivi des événements de perte](tracking-loss-in-unity.md).

### <a name="capabilities"></a>Fonctionnalités

Pour une application tirer parti de certaines fonctionnalités, il doit déclarer les fonctionnalités appropriées dans son manifeste. Les déclarations de manifeste peuvent être rendues Unity, ils sont inclus dans chaque exportation ultérieures du projet. 

Fonctionnalités peuvent être activées pour une application de réalité mixte par :
1) Accédez à **modifier** > **paramètres du projet** > **Player** page
2) Cliquez sur le **Windows Store** onglet et ouvrez le **paramètres de publication** section et recherchez le **fonctionnalités** liste

Les fonctionnalités applicables pour l’activation de l’API couramment utilisées pour les applications HOLOGRAPHIQUE sont :
<br>

|  Fonctionnalité  |  API nécessitant une fonctionnalité |
|----------|----------|
|  SpatialPerception  |  SurfaceObserver | 
|  WebCam  |  PhotoCapture et VideoCapture | 
|  Bibliothèque d’images / VideosLibrary  |  PhotoCapture ou VideoCapture, respectivement (lorsque vous stockez le contenu capturé) | 
|  Microphone  |  VideoCapture (lors de la capture audio), DictationRecognizer, GrammarRecognizer et KeywordRecognizer | 
|  InternetClient  |  DictationRecognizer (et à utiliser le Profiler Unity) | 

## <a name="see-also"></a>Voir aussi
* [Vue d’ensemble du développement Unity](unity-development-overview.md)
* [Performances Understaing pour la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations relatives aux performances pour Unity](performance-recommendations-for-unity.md)