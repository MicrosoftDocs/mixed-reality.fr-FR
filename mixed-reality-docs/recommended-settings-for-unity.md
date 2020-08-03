---
title: Paramètres recommandés pour Unity
description: Unity offre des comportements spécifiques à la réalité mixte qui peuvent être activés via les paramètres du projet.
author: troy-ferrell
ms.author: trferrel
ms.date: 07/29/2020
ms.topic: article
keywords: Unity, paramètres, réalité mixte
ms.openlocfilehash: 414e18686926fd8105726fb3811f3eef1d365bd9
ms.sourcegitcommit: ef0bf03833eda826ed0b884859b4573775112aba
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2020
ms.locfileid: "87476721"
---
# <a name="recommended-settings-for-unity"></a>Paramètres recommandés pour Unity

Unity fournit un ensemble d’options par défaut qui sont généralement le cas moyen pour toutes les plateformes. Toutefois, Unity offre des comportements spécifiques à la réalité mixte qui peuvent être activés via les paramètres du projet.

## <a name="performant-environment-set-up"></a>Configuration de l’environnement performante

### <a name="low-quality-settings"></a>Paramètres de qualité inférieure

Il est important de modifier les **paramètres de qualité des Unity** pour votre environnement afin qu’ils soient **très faibles**. Cela permet de s’assurer que votre application exécute efficacement à la fréquence appropriée. Cela est extrêmement important pour le développement HoloLens. Pour le développement sur des casques immersifs, selon les spécifications du bureau qui alimente l’expérience VR, vous pouvez toujours obtenir une fréquence d’images sans les paramètres de qualité la plus basse.

Dans Unity 2019 LTS +, vous pouvez définir le niveau de qualité du projet en accédant à **modifier**  >  **Project Settings**  >  la**qualité** des paramètres du projet et en définissant la **valeur par défaut** en cliquant sur la flèche vers le bas jusqu’au niveau de qualité **très faible** .

### <a name="lighting-settings"></a>Paramètres d’éclairage

À l’instar des paramètres de scène de qualité, il est important de définir des paramètres d’éclairage optimaux pour votre application de réalité mixte. Dans Unity, le paramètre d’éclairage qui aura généralement le plus grand impact sur les performances de votre scène est l' **éclairage global en temps réel**. Vous pouvez désactiver cette option en sélectionnant Paramètres d’éclairage de l’affichage de la **fenêtre**  >  **Rendering**  >  **Lighting Settings**  >  **éclairage global en temps réel**.

Il existe un autre paramètre d’éclairage, un **éclairage global cuit**. Ce paramètre peut fournir des résultats performants et visuellement sur les casques immersifs, mais il n’est généralement pas applicable au développement HoloLens. Le **Illumniation global cuit** est calculé uniquement pour les GameObjects statiques qui sont généralement introuvables dans les scènes HoloLens en raison de la nature d’un environnement inconnu et en cours de modification.

Pour plus d’informations, consultez [illumination globale à partir d’Unity](https://docs.unity3d.com/Manual/GIIntro.html) . 

>[!NOTE]
> L' **éclairage global en temps réel** est défini **par scène** et les développeurs doivent donc enregistrer cette propriété pour chaque scène Unity dans leur projet.

### <a name="single-pass-instancing-rendering-path"></a>Chemin de rendu d’instanciation à passage unique

Dans les applications de réalité mixte, la scène est restituée deux fois, une fois pour chaque œil à l’utilisateur. Comparé au développement 3D traditionnel, cela double la quantité de travail qui doit être calculée. Par conséquent, il est important de sélectionner le chemin de rendu le plus efficace dans Unity pour enregistrer les temps processeur et GPU. Le rendu d’instance à passage unique optimise le pipeline de rendu Unity pour les applications de réalité mixte. par conséquent, il est recommandé d’activer ce paramètre par défaut pour chaque projet.

Pour activer cette fonctionnalité dans votre projet Unity

1)  Ouvrez **Player XR Settings** (accédez à **Edit** > **Project Settings** > **Player** > **XR Settings**).
2) Sélectionnez **Single Pass Instanced** dans le menu déroulant **Stereo Rendering Method** (la case **Virtual Reality Supported** doit être cochée).

Lisez les articles suivants sur Unity pour plus d’informations sur cette approche de rendu.

- [How to maximize AR and VR performance with advanced stereo rendering](https://blogs.unity3d.com/2017/11/21/how-to-maximize-ar-and-vr-performance-with-advanced-stereo-rendering/)
- [Single Pass Instancing](https://docs.unity3d.com/Manual/SinglePassInstancing.html)

>[!NOTE]
> Un problème courant avec le rendu d’instance à passage unique se produit si les développeurs ont déjà des nuanceurs personnalisés existants non écrits pour l’instanciation. Une fois cette fonctionnalité activée, les développeurs peuvent remarquer que certains GameObjects ne sont rendus que dans un seul œil. Cela est dû au fait que les nuanceurs personnalisés associés n’ont pas les propriétés appropriées pour l’instanciation.
>
> Consultez [Single Pass Stereo Rendering for HoloLens](https://docs.unity3d.com/Manual/SinglePassStereoRenderingHoloLens.html) sur Unity pour savoir comment résoudre ce problème.

### <a name="enable-depth-buffer-sharing"></a>Activer le partage de mémoire tampon de profondeur

Pour obtenir une meilleure stabilité de l’hologramme à partir de la perception de l’utilisateur, il est recommandé d’activer la propriété de partage de la **mémoire tampon de profondeur** dans Unity. Si vous activez cette fonction, Unity partagera la carte de profondeur produite par votre application avec la plateforme Windows Mixed Reality. La plateforme sera alors en mesure de mieux optimiser la stabilité des hologrammes pour votre scène pour toute image donnée rendue par votre application.

Pour activer cette fonctionnalité dans votre projet Unity

1) Ouvrez **Player XR Settings** (accédez à **Edit** > **Project Settings** > **Player** > **XR Settings**).
2) Activez la case à cocher **activer le partage de tampons de profondeur** dans les kits de développement logiciel (SDK) **Virtual Real**  >  expansion**Windows Mixed realisation** (la case à cocher**Virtual Really Supported**

En outre, il est recommandé de sélectionner **profondeur de 16 bits** sous le paramètre **format de profondeur** dans ce panneau, en particulier pour le développement HoloLens. La sélection de 16 bits comparée à 24 bits réduit considérablement les besoins en bande passante, car moins de données devront être déplacées/traitées.

Pour que la plateforme Windows Mixed realisation optimise la stabilité des hologrammes, elle s’appuie sur la mémoire tampon de profondeur pour être exacte et correspond à n’importe quel hologramme rendu sur l’écran. Ainsi, avec le partage de mémoire tampon de profondeur sur, il est important de rendre la couleur de rendu, afin de rendre également la profondeur. Dans Unity, la plupart des matériaux opaques ou TransparentCutout restituent la profondeur par défaut, mais les objets transparents et textuels n’affichent généralement pas de profondeur, bien qu’il s’agisse d’un nuanceur dépendant, etc.

Si vous utilisez le [nuanceur standard](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_MRTKStandardShader.md)de la boîte à outils de la réalité mixte, pour restituer la profondeur des objets transparents :

1) Sélectionner la matière transparente qui utilise le nuanceur standard MRTK et ouvrir la fenêtre de l’éditeur de l’inspecteur
2) Sélectionnez le bouton **corriger maintenant** dans l’avertissement de partage de la mémoire tampon de profondeur. Vous pouvez également effectuer cette opération manuellement en définissant le **mode de rendu** sur **personnalisé**. puis définissez **mode** sur **transparent** et enfin définir l' **écriture de profondeur** **sur activé**

> [!IMPORTANT]
> Les développeurs doivent être attentifs à la lutte Z lors de la modification de ces valeurs avec les paramètres du plan proche/Far de l’appareil photo. Z-combat se produit lorsque deux Gameobjects essaient de s’afficher sur le même pixel et en raison de limitations de fidélité du tampon de profondeur (par exemple, profondeur z), Unity ne peut pas déterminer quel objet est devant l’autre. Les développeurs notent un scintillement entre deux objets de jeu lorsqu’ils *luttent contre* la même valeur de profondeur z. Cela peut être résolu en basculant au format de profondeur 24 bits, car il y aura une plus grande plage de valeurs pour chaque objet à calculer pour la profondeur z de l’appareil photo.
>
> Toutefois, il est recommandé, en particulier pour le développement HoloLens, de modifier les plans presque et Far de l’appareil photo vers une plage plus petite plutôt que de conserver le format de profondeur 16 bits. La profondeur z est mappée de manière non linéaire à la plage de valeurs le long des plans de caméra near et Far. Vous pouvez modifier cette valeur en sélectionnant la *caméra principale* dans votre scène et sous **Inspector**, en remontant le **plan de découpage proche & Far** pour réduire leur plage (c.-à-d. de 1000MD à 100 m ou à une autre valeur x, etc.)

>[!IMPORTANT]
> [Unity ne crée pas de tampon de stencil lors de](https://docs.unity3d.com/ScriptReference/RenderTexture-depth.html) l’utilisation du format de profondeur 16 bits. Ainsi, certains effets d’interface utilisateur Unity et d’autres effets requis par stencil ne fonctionneront pas, à moins que le format de profondeur 24 bits ne soit sélectionné, ce qui créera une [mémoire tampon de stencil de 8 bits](https://docs.unity3d.com/Manual/SL-Stencil.html).

### <a name="building-for-il2cpp"></a>Génération pour IL2CPP

Unity a déconseillé la prise en charge du backend de script .NET et recommande donc que les développeurs utilisent **IL2CPP** pour leurs builds Visual Studio UWP. Bien que cela offre différents avantages, la génération de votre solution Visual Studio à partir d’Unity pour **IL2CPP** peut être considérablement plus lente que l’ancienne méthode .net. Par conséquent, il est fortement recommandé de suivre les meilleures pratiques en matière de création de **IL2CPP** pour économiser l’heure de l’itération de développement.

1) Tirez parti de la création incrémentielle en générant votre projet dans le même répertoire à chaque fois, en réutilisant les fichiers prédéfinis
2) Désactiver les analyses logicielles anti-programme malveillant pour votre projet & les dossiers de build
   - Ouvrir la **protection contre les menaces contre les Virus &** sous votre application Paramètres Windows 10
   - Sélectionnez **gérer les paramètres** sous **virus & les paramètres de protection contre les menaces**
   - Sélectionnez **Ajouter ou supprimer des exclusions** sous la section **exclusions** .
   - Cliquez sur **Ajouter une exclusion** , puis sélectionnez le dossier contenant le code de votre projet Unity et les sorties de génération
3) Utiliser un SSD pour la génération

Pour plus d’informations, consultez [optimisation des durées de génération pour IL2CPP](https://docs.unity3d.com/Manual/IL2CPP-OptimizingBuildTimes.html) .

> [!NOTE]
> En outre, il peut être avantageux de configurer un [serveur de cache](https://docs.unity3d.com/Manual/CacheServer.html), en particulier pour les projets Unity qui comprennent une grande quantité de ressources (à l’exclusion des fichiers de script), et pour les scènes ou ressources qui changent constamment. Lorsque vous ouvrez un projet, Unity stocke les ressources éligibles dans un format de cache interne sur l’ordinateur de développement. Les éléments doivent être réimportés, et donc retraités, après modification. Ce processus peut être effectué une fois puis enregistré dans un serveur de cache. Pour gagner du temps, vous pouvez le partager avec les autres développeurs, plutôt que de demander à chaque développeur de réimporter localement les éléments modifiés.

## <a name="publishing-properties"></a>Propriétés de publication

### <a name="holographic-splash-screen"></a>Écran de démarrage holographique

HoloLens possède un processeur et un GPU de classe mobile, ce qui signifie que le chargement des applications peut prendre un peu plus de temps. Pendant le chargement de l’application, les utilisateurs voient simplement le noir et, par conséquent, peuvent se demander ce qui se passe. Pour les rassurer pendant le chargement, vous pouvez ajouter un écran de démarrage holographique.

Pour activer/désactiver l’écran de démarrage holographique :

1) Aller à la page **modifier**les  >  **paramètres du projet**, page du  >  **lecteur**
2) Cliquez sur l’onglet **Windows Store** et ouvrez la section **image de démarrage** .
3) Appliquez l’image souhaitée sous la propriété **image de démarrage holographique Windows holographique >** .
    - Le fait de basculer l’option **afficher l’écran de démarrage Unity** active ou désactive l’écran de démarrage de la personnalisation Unity. Si vous ne disposez pas d’une licence Pro Unity, l’écran de démarrage de la personnalisation Unity s’affiche toujours.
    - Si une **image de démarrage holographique** est appliquée, elle s’affiche toujours, que la case à cocher Afficher l’écran de démarrage Unity soit activée ou désactivée. La spécification d’une image de démarrage holographique personnalisée est disponible uniquement pour les développeurs disposant d’une licence Unity Pro.

|  Afficher l’écran de démarrage Unity  |  Image de démarrage holographique  |  Comportement |
|----------|----------|----------|
|  Activé  |  Aucun  |  Affiche l’écran de démarrage Unity par défaut pendant 5 secondes ou jusqu’à ce que l’application soit chargée, selon la valeur la plus longue. |
|  Activé  |  Custom  |  Affichez l’écran de démarrage personnalisé pendant 5 secondes ou jusqu’à ce que l’application soit chargée, selon la valeur la plus longue. |
|  Désactivé  |  Aucun  |  Affichez le noir transparent (rien) jusqu’à ce que l’application soit chargée. |
|  Désactivé  |  Custom  |  Affichez l’écran de démarrage personnalisé pendant 5 secondes ou jusqu’à ce que l’application soit chargée, selon la valeur la plus longue. |

Pour plus d’informations, consultez la [documentation de l’écran de démarrage d’Unity](https://docs.unity3d.com/Manual/class-PlayerSettingsSplashScreen.html) .

### <a name="tracking-loss"></a>Perte de suivi

Un casque de réalité mixte dépend de l’environnement qui l’entoure pour construire des [systèmes de coordonnées à verrouillage universel](coordinate-systems-in-unity.md), qui permettent aux hologrammes de rester en position. Lorsque le casque ne parvient pas à se trouver dans le monde, le casque est dit qu’il a *perdu le suivi*. Dans ces cas, les fonctionnalités dépendantes des systèmes de coordonnées universels, tels que les étapes spatiales, les ancres spatiales et le mappage spatial, ne fonctionnent pas.

Si une perte de suivi se produit, le comportement par défaut d’Unity consiste à arrêter le rendu des hologrammes, à suspendre la [boucle de jeu](https://docs.unity3d.com/Manual/ExecutionOrder.html)et à afficher une notification de perte de suivi qui suit confortablement le point de vue des utilisateurs. Des notifications personnalisées peuvent également être fournies sous la forme d’une image de perte de suivi. Pour les applications qui dépendent du suivi pour leur expérience complète, il est suffisant pour permettre à Unity de la gérer entièrement jusqu’à ce que le suivi soit récupéré. Les développeurs peuvent fournir une image personnalisée à afficher pendant la perte de suivi.

Pour personnaliser l’image de suivi perdu :

1) Aller à la page **modifier**les  >  **paramètres du projet**, page du  >  **lecteur**
2) Cliquez sur l’onglet **Windows Store** et ouvrez la section **image de démarrage** .
3) Appliquez l’image souhaitée sous la propriété image de la **perte de suivi de > Windows holographique** .

#### <a name="opt-out-of-automatic-pause"></a>Désactiver la pause automatique

Certaines applications peuvent ne pas nécessiter de suivi (par exemple, des [applications d’orientation uniquement](coordinate-systems-in-unity.md) telles que des visionneuses vidéo de 360 degrés) ou doivent peut-être continuer le traitement sans interruption pendant que le suivi est perdu. Dans ces cas, les applications peuvent refuser la perte par défaut du comportement de suivi. Les développeurs qui choisissent cela sont responsables du masquage/désactivation de tous les objets qui ne s’affichent pas correctement dans un scénario de perte de suivi. Dans la plupart des cas, le seul contenu qui est recommandé pour être rendu dans ce cas est le contenu verrouillé, centré autour de l’appareil photo principal.

Pour refuser le comportement de pause automatique :

1) Accéder à la **page Modifier**les paramètres du  >  **projet**  >  **Player**
2) Cliquez sur l’onglet **Windows Store** et ouvrez la section **image de démarrage** .
3) Modifiez la case à cocher **Windows holographique > en cas de suspension de perte de suivi et d’affichage d’image** .

#### <a name="tracking-loss-events"></a>Suivi des événements de perte

Pour définir un comportement personnalisé lorsque le suivi est perdu, gérez les [événements de perte de suivi](tracking-loss-in-unity.md)global.

### <a name="capabilities"></a>Fonctionnalités

Pour qu’une application tire parti de certaines fonctionnalités, elle doit déclarer les fonctionnalités appropriées dans son manifeste. Les déclarations de manifeste peuvent être effectuées dans Unity afin qu’elles soient incluses dans chaque exportation de projet suivante.

Les fonctionnalités peuvent être activées pour une application de réalité mixte en :

1) Aller à la page **modifier**les  >  **paramètres du projet**, page du  >  **lecteur**
2) Cliquez sur l’onglet **Windows Store** , ouvrez la section **paramètres de publication** et recherchez la liste des **fonctionnalités** .

Les fonctionnalités applicables pour activer les API couramment utilisées pour les applications holographiques sont les suivantes :
<br>

|  Fonctionnalité  |  API nécessitant des fonctionnalités |
|----------|----------|
|  SpatialPerception  |  SurfaceObserver |
|  WebCam  |  PhotoCapture et VideoCapture |
|  PicturesLibrary/VideosLibrary  |  PhotoCapture ou VideoCapture, respectivement (lors du stockage du contenu capturé) |
|  Microphone  |  VideoCapture (lors de la capture de l’audio), DictationRecognizer, GrammarRecognizer et KeywordRecognizer |
|  InternetClient  |  DictationRecognizer (et pour utiliser le profileur Unity) |

## <a name="see-also"></a>Voir aussi

* [Vue d’ensemble du développement Unity](unity-development-overview.md)
* [Comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)
