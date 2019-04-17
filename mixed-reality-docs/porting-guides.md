---
title: Guides en matière de portage
description: Une procédure pas à pas à pas expliquant comment porter une application existante à la réalité mixte de Windows.
author: ChimeraScorn
ms.author: cwhite
ms.date: 10/02/2018
ms.topic: article
keywords: port portage, unity, intergiciel (middleware), du moteur, UWP
ms.openlocfilehash: a4a8c78f1c45fd8e3b85a767d139bae9f67540e0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595362"
---
# <a name="porting-guides"></a>Guides en matière de portage

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

Windows 10 prend en charge des casques IMMERSIFS et HOLOGRAPHIQUES directement. Si vous avez créé le contenu pour un autre appareil, telles que le Oculus Rift ou HTC Vive, ils ont des dépendances sur les bibliothèques qui existent au-dessus des API de la plateforme du système d’exploitation. Réunir le contenu existant à Windows Mixed Reality implique le reciblage de l’utilisation de ces autres kits SDK aux API Windows. Le [API de la plate-forme Windows pour la réalité mixte](https://docs.microsoft.com/uwp/api/Windows.Perception) fonctionnent uniquement dans le modèle d’application Universal Windows Platform (UWP). Par conséquent, si votre application n’est pas déjà créée pour UWP, portage vers UWP fera partie de l’expérience de portage.

## <a name="porting-overview"></a>Vue d’ensemble de portage

À un niveau élevé, voici les étapes impliquées dans le portage de contenu existant :
1. **Assurez-vous que votre ordinateur est en cours d’exécution de de Windows 10 Fall Creators Update (16299).** Nous ne recommandons plus recevoir preview builds à partir de l’anneau Insider ignorer à l’avance, car ces builds ne seront plus stable pour le développement de réalité mixte.
2. **Mettre à niveau vers la dernière version de votre graphique ou d’un moteur de jeu.** Moteurs de jeu doit prendre en charge le SDK Windows 10 version 10.0.15063.0 (publiée en avril 2017) ou une version ultérieure.
3. **Mettre à niveau n’importe quel intergiciel (middleware), les plug-ins ou les composants.** Si votre application contient tous les composants, il est judicieux de mettre à niveau vers la dernière version. Les versions plus récentes des plug-ins courants ont prise en charge pour UWP.
4. **Supprimer les dépendances sur les kits de développement logiciel en double**. Selon l’appareil ciblage de votre contenu, vous devez supprimer ou effectuer une compilation conditionnelle out ce Kit de développement logiciel (par exemple, SteamVR) pour cibler les API Windows à la place.
5. **Étudier les problèmes de génération.** À ce stade, l’exercice de portage est spécifique à votre application, votre moteur et les dépendances de composants que vous avez.

## <a name="common-porting-steps"></a>Étapes de portage courantes

### <a name="common-step-1-make-sure-you-have-the-right-development-hardware"></a>Common étape 1 : Assurez-vous que vous disposez du matériel de développement appropriées

Le [installer les outils](install-the-tools.md#for-immersive-vr-headset-development) page répertorie le matériel de développement recommandées.

### <a name="common-step-2-upgrade-to-the-latest-flight-of-windows-10"></a>Common étape 2 : Mise à niveau vers le dernier vol de Windows 10

La plateforme Windows Mixed Reality est toujours en cours de développement, et pour être plus efficace, nous vous recommandons d’en cours sur le vol « Windows Insider rapide ». Pour accéder aux vols de windows, vous devrez [rejoindre le programme Insider de Windows](https://insider.windows.com/).
1. Installer le [Windows 10 Creators Update](https://www.microsoft.com/software-download/windows10)
2. [Joindre](https://insider.windows.com/) le programme Insider de Windows.
3. Activer [Mode développeur](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
4. Basculez vers le [Windows Insider rapide vols](https://blogs.technet.microsoft.com/uktechnet/2016/07/01/joining-insider-preview) via les paramètres--> mise à jour & sécurité Section

### <a name="common-step-3-upgrade-to-the-most-recent-build-of-visual-studio"></a>Common étape 3 : Mise à niveau vers la build la plus récente de Visual Studio
* Consultez [installer les outils](install-the-tools.md#installation-checklist) page sous Visual Studio 2017

### <a name="common-step-4-be-ready-for-the-store"></a>Common étape 4 : Être prêt pour le Store
* Utilisez [Kit de Certification des applications Windows](https://developer.microsoft.com/windows/develop/app-certification-kit) (également appelé Kit) très tôt et souvent !
* Utilisez [Analyseur de portabilité](https://docs.microsoft.com/dotnet/standard/portability-analyzer) ([télécharger](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer))

### <a name="common-step-5-choose-the-correct-adapter"></a>Common étape 5 : Choisissez l’adaptateur approprié
* Dans les systèmes tels que des ordinateurs portables avec deux GPU, [cibler l’adaptateur approprié](rendering-in-directx.md#hybrid-graphics-pcs-and-mixed-reality-applications). Cela s’applique aux applications Unity, en outre des applications DirectX natives, où un ID3D11Device est créé, explicitement ou implicitement (Media Foundation), pour ses fonctionnalités.

## <a name="unity-porting-guidance"></a>Instructions de transfert de Unity

### <a name="unity-step-1-follow-the-common-porting-steps"></a>Étape 1 de Unity : Suivez les étapes de portage courantes

Suivez les étapes courantes. Lorsqu’à l’étape 3 de #, sélectionnez le **le développement de jeux avec Unity** charge de travail. Vous pouvez désactiver le composant facultatif de l’éditeur Unity dans la mesure où vous allez installer une version plus récente de Unity dans les instructions ci-dessous.

### <a name="unity-step-2-upgrade-to-the-latest-public-build-of-unity-with-windows-mr-support"></a>Étape 2 de Unity : Mettre à niveau vers la dernière version publique d’Unity avec prise en charge Windows MR
1. Téléchargez la dernière version [recommandé build publique Unity](install-the-tools.md) avec la réalité mixte prennent en charge.
2. Enregistrer une copie de votre projet avant de commencer
3. Examinez le [documentation](https://docs.unity3d.com/Manual/UpgradeGuides.html) disponible à partir d’Unity sur le portage.
4. Suivez le [instructions](https://docs.unity3d.com/Manual/APIUpdater.html) sur site d’Unity pour l’utilisation de leur mise à jour automatique de API
5. Vérifier et s’il existe des modifications supplémentaires que vous devez effectuer tirer votre projet en cours d’exécution, puis suivez les autres erreurs et avertissements. Remarque: Si vous disposez d’intergiciel (middleware) dont vous dépendez, vous devrez peut-être mettre à jour cet intergiciel (middleware) pour vous aider (plus de détails à l’étape 3 ci-dessous).

### <a name="unity-step-3-upgrade-your-middleware-to-the-latest-versions"></a>Étape 3 de Unity : Mettre à niveau votre intergiciel (middleware) avec les dernières versions

Toute mise à jour Unity, il existe de bonnes chances que vous devez mettre à jour un ou plusieurs packages de middleware votre jeu ou votre application dépend de. En outre, la version plus récente de tous vos logiciels intermédiaires augmentera vos chances de réussite dans le reste du processus de portage. De nombreux packages d’intergiciel (middleware) ont récemment ajouté la prise en charge pour Universal Windows Platform (UWP) et mise à niveau vers les versions les plus récentes vous permettra de tirer parti de ce travail.

### <a name="unity-step-4-target-your-application-to-run-on-universal-windows-platform-uwp"></a>Étape 4 de Unity : Cibler votre application s’exécute sur Universal Windows Platform (UWP)

Après avoir installé les outils, vous devez obtenir votre application en cours d’exécution en tant qu’une application Windows universelle.
* Suivez le [détaillées étape par étape procédure pas à pas](https://unity3d.com/partners/microsoft/porting-guides) fourni par Unity. Veuillez noter que vous devez rester sur la dernière version LTS (n’importe quelle version 20xx.4) pour Windows MR.
* D’autres ressources de développement UWP, examinons le [guide de développement de jeux Windows 10](https://docs.microsoft.com/windows/uwp/gaming/e2e).
* Veuillez noter que Unity continue à améliorer la prise en charge IL2CPP ; IL2CPP facilite certaines UWP ports considérablement. Si vous ciblez actuellement des scripts de serveur principal .net, vous devez envisager de convertir pour tirer parti du back-end IL2CPP à la place.

Remarque: Si votre application comporte des dépendances sur des services spécifiques à un appareil, par exemple, correspondance à partir de flux, vous devez les désactiver à cette étape. Ultérieurement, vous pouvez vous raccorder à l’équivalents services fournis par Windows.

### <a name="unity-step-5-deprecated"></a>Étape 5 de Unity : (Déconseillée)

Étape 5 n’est plus nécessaire. Nous allons le laisser ici afin que l’indexation des étapes reste le même.

### <a name="unity-step-6-get-your-windows-mixed-reality-hardware-set-up"></a>Étape 6 de Unity : Obtenir votre installation matérielle Windows Mixed Reality
1. Revue les étapes [le programme d’installation immersives casque](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/before-you-start
)
2. En savoir plus sur [l’utilisation du simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md) et [navigation dans la page d’accueil Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)

### <a name="unity-step-7-target-your-application-to-run-on-windows-mixed-reality"></a>Étape 7 de Unity : Cibler votre application s’exécute sur Windows Mixed Reality
1. Tout d’abord, vous devez supprimer ou effectuer une compilation conditionnelle n’importe quel autre bibliothèque prise en charge spécifique à un particulier VR SDK. Ces ressources changent fréquemment des paramètres et les propriétés de votre projet de manière à n’est pas compatibles avec les autres kits de développement logiciel VR, tels que Windows Mixed Reality.
    * Par exemple, si votre projet référence le SDK SteamVR, vous devez mettre à jour votre projet pour exclure ces prefabs et les appels d’API de script lors de l’exportation pour la cible de build de Windows Store.
    * Les étapes spécifiques de manière conditionnelle à l’exclusion des autres kits de développement logiciel VR sera bientôt disponible.
2. Dans votre projet Unity, [cibler le SDK Windows 10](holograms-100.md#target-windows-10-sdk)
3. Pour chaque scène, [le programme d’installation de l’appareil photo](holograms-100.md#chapter-2---setup-the-camera)

### <a name="unity-step-8-use-the-stage-to-place-content-on-the-floor"></a>Étape 8 de Unity : Utilisez l’étape de placer le contenu sur le sol

Vous pouvez créer des expériences de réalité mixte sur un large éventail de [expérience échelles](coordinate-systems.md).

Si vous portez un **assis à l’échelle du expérience**, vous devez vous assurer de Unity est défini sur le **stationnaire** suivi du type de l’espace :

```cs
XRDevice.SetTrackingSpaceType(TrackingSpaceType.Stationary);
```

Cela définit le système de coordonnées de monde d’Unity pour suivre le [de référence stationnaire](coordinate-systems.md#spatial-coordinate-systems). Dans le mode de suivi stationnaire, contenu placé dans l’éditeur juste devant l’emplacement par défaut de l’appareil photo (-Z est vers l’avant) apparaît devant l’utilisateur quand l’application démarre. Pour recentrer l’utilisateur d’assis d’origine, vous pouvez appeler d’Unity [XR. InputTracking.Recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html) (méthode).

Si vous portez un **permanent à l’échelle expérience** ou **expérience de l’échelle de la salle**, vous allez placer contenu par rapport à l’étage. Sur l’utilisateur de la raison floor, à l’aide de la  **[étape spatial](coordinate-systems.md#spatial-coordinate-systems)**, qui représente l’utilisateur défini au niveau du sol origine et les limites de salle facultatif, définissez au cours de première exécution. Pour ces expériences, vous devez vous assurer Unity est défini sur le **RoomScale** suivi du type d’espace. Alors que RoomScale est la valeur par défaut, vous voudrez définir explicitement et bénéficier de retour true pour intercepter les situations où l’utilisateur a déplacé son ordinateur en dehors de la salle qu'ils étalonnés :

```cs
if (XRDevice.SetTrackingSpaceType(TrackingSpaceType.RoomScale))
{
    // RoomScale mode was set successfully.  App can now assume that y=0 in Unity world coordinate represents the floor.
}
else
{
    // RoomScale mode was not set successfully.  App cannot make assumptions about where the floor plane is.
}
```

Une fois que votre application définit correctement le RoomScale suivi de type d’espace, contenu placé sur la y = 0 plan s’affiche sur le sol. L’origine (0, 0, 0) sera l’emplacement spécifique sur le lieu où l’utilisateur a su résister pendant l’installation de la salle, avec -Z qui représente la direction avant qu’ils ont été confrontés pendant l’installation.

Dans le code de script, vous pouvez, puis appelez la méthode TryGetGeometry vous êtes du genre à UnityEngine.Experimental.XR.Boundary pour obtenir un polygone de la limite, en spécifiant un type de limite de TrackedArea. Si l’utilisateur défini une limite (vous obtenez une liste de sommets), vous savez qu’il fournir un **expérience de l’échelle de la salle** à l’utilisateur, où ils peuvent la scène vous guider créer.

Notez que le système affiche automatiquement la limite lors de l’utilisateur à l’approche. Votre application n’a pas besoin d’utiliser ce polygone pour restituer la limite de lui-même.

Pour plus d’informations, consultez le [systèmes de coordonnées dans Unity](coordinate-systems-in-unity.md) page.

Certaines applications utilisent un rectangle pour limiter leur interaction. Récupération le plus grand rectangle inscrit n’est pas directement pris en charge dans les API UWP ou Unity. L’exemple de code lié à ci-dessous montre comment rechercher un rectangle dans les limites tracées. Il est heuristique basée peut ne pas trouver la solution optimale, toutefois, les résultats sont généralement conformes aux attentes. Paramètres de l’algorithme peuvent être paramétrés pour rechercher des résultats plus précis au détriment du temps de traitement. L’algorithme est dans une duplication de la boîte à outils de réalité mixte qui utilise la version d’évaluation version MRTP Unity 5.6. Cela n’est pas disponible publiquement. Le code doit être directement utilisable dans les versions Unity 2017.2 et versions ultérieures. Le code sera facilement être porté vers le MRTK actuel dans un avenir proche.

[fichier zip du code sur GitHub](https://github.com/KevinKennedy/MixedRealityToolkit-Unity/releases/tag/5.6.MRTP20) fichiers importants :
* Assets/HoloToolkit/Stage/Scripts/StageManager.cs - exemple d’utilisation
* Assets/HoloToolkit/Stage/Scripts/LargestRectangle.cs - implémentation de l’algorithme
* Assets/HoloToolkit-UnitTests/Editor/Stage/LargestRectangleTest.cs - test trivial de l’algorithme

Exemple de résultats :

![Exemple de résultats](images/largestrectangle-400px.jpg)

Algorithme est basé sur un blog par Daniel Smilkov : [Plus grand rectangle dans un polygone](https://d3plus.org/blog/behind-the-scenes/2014/07/08/largest-rect/)

### <a name="unity-step-9-work-through-your-input-model"></a>Étape 9 de Unity : Travailler dans votre modèle d’entrée

Chaque jeu ou une application ciblant un HMD existant a un ensemble d’entrées qu’il gère, types d’entrées dont il a besoin pour une expérience et des API spécifiques qu’elle appelle pour obtenir ces entrées. Nous avons investi dans la tentative de la rendre aussi simple et rapide que possible pour tirer parti des entrées disponibles dans Windows Mixed Reality.
1. Lisez le **[d’entrée portage guide pour Unity](input-porting-guide-for-unity.md)** pour plus d’informations Windows Mixed Reality expose d’entrée, et comment qui mappe à ce que votre application peut faire aujourd'hui.
2. Choisissez si vous vous apprêtez à augmenter la portée d’Unity cross-VR-SDK API ou spécifique au MR d’entrée d’API. Les API de Input.GetButton/Input.GetAxis général sont utilisées par les applications de réalité virtuelle Unity dès aujourd'hui pour [Oculus entrée](https://docs.unity3d.com/Manual/OculusControllers.html) et [OpenVR entrée](https://docs.unity3d.com/Manual/OpenVRControllers.html). Si vos applications sont déjà à l’aide de ces API pour les contrôleurs de mouvement, c’est le chemin le plus simple, vous devez simplement remapper les boutons et les axes dans le Gestionnaire d’entrée.
    * Vous pouvez accéder des données de contrôleur de mouvement dans Unity à l’aide soit du général entre-VR-SDK Input.GetButton/Input.GetAxis API ou le MR UnityEngine.XR.WSA.Input APIs spécifiques. (précédemment dans l’espace de noms UnityEngine.XR.WSA.Input dans Unity 5.6)
    * Consultez le [exemple dans le Kit de ressources](https://github.com/Microsoft/HoloToolkit-Unity/pull/572) qui combine des contrôleurs gamepad et de mouvement.

### <a name="unity-step-10-performance-testing-and-tuning"></a>Étape 10 de Unity : Tests de performances et réglage

Windows Mixed Reality seront disponibles sur une large classe de périphériques, allant haute fin des jeux PC, jusqu'à la vaste marché grand public PC. Selon quel marché que vous ciblez, il existe une différence significative dans les calcul et les graphiques des budgets disponibles pour votre application. Au cours de cet exercice de portage, vous sont susceptibles d’en tirant parti d’un PC premium et avez eu des importantes budgets de calcul et graphiques disponibles à votre application. Si vous souhaitez rendre votre application disponible pour un public plus large, vous devez tester et profiler votre application sur [le matériel représentatif que vous souhaitez cible](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines).

Les deux [Unity](https://docs.unity3d.com/Manual/Profiler.html) et [Visual Studio](https://docs.microsoft.com/visualstudio/profiling/index) incluent les profileurs de code et les deux [Microsoft](understanding-performance-for-mixed-reality.md) et [Intel](https://software.intel.com/articles/vr-content-developer-guide) sur des lignes directrices profilage des performances et l’optimisation. Une description détaillée des performances est disponible au [comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md). En outre, il existe des détails spécifiques à Unity sous [recommandations relatives aux performances pour Unity](performance-recommendations-for-unity.md).

## <a name="see-also"></a>Voir aussi
* [Entrée portage guide pour Unity](input-porting-guide-for-unity.md)
* [Recommandations de compatibilité Windows Mixed Reality minimale PC matérielles](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)
* [Comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations relatives aux performances pour Unity](performance-recommendations-for-unity.md)
* [Ajouter la prise en charge de Xbox Live à Unity pour UWP](https://docs.microsoft.com/windows/uwp/xbox-live/get-started-with-partner/partner-add-xbox-live-to-unity-uwp)
