---
title: Guides en matière de portage
description: Une procédure pas à pas expliquant comment porter une application immersive existante vers Windows Mixed Reality.
author: JBrentJ
ms.author: alexturn
ms.date: 07/07/2020
ms.topic: article
keywords: port, Portage, Unity, intergiciel, moteur, UWP
ms.openlocfilehash: 5cf66ce857806ab6fcf8c94b94c7a9a540339b97
ms.sourcegitcommit: fef42e2908e49822f2d13b05d2f9260bf0d72158
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86061152"
---
# <a name="porting-guides"></a>Guides en matière de portage

## <a name="overview"></a>Vue d’ensemble

Windows 10 offre une prise en charge directe des casques immersifs et holographiques. Si vous avez créé du contenu pour d’autres appareils, tels que le rift Oculus ou le HTC, ceux-ci ont des dépendances vis-à-vis des bibliothèques qui se trouvent au-dessus de l’API de plateforme du système d’exploitation. L’intégration du contenu existant à Windows Mixed Reality implique le reciblage de l’utilisation de ces autres kits SDK sur les API Windows. Les [API de la plate-forme Windows pour la réalité mixte](https://docs.microsoft.com/uwp/api/Windows.Perception) fonctionnent avec le modèle d’application Windows x86 et le plateforme Windows universelle (UWP). Si votre application n’est pas déjà générée pour UWP, la modification de la plateforme UWP fera partie de l’expérience de Portage.

## <a name="porting-overview"></a>Vue d’ensemble du Portage

À un niveau élevé, les étapes suivantes sont impliquées dans le portage du contenu existant :
1. **Assurez-vous que votre ordinateur exécute la mise à jour des créateurs de automne Windows 10 (16299).** Nous vous déconseillons de recevoir des builds préliminaires à partir de la sonnerie d’inversion anticipée, car ces builds ne sont pas les plus stables pour le développement de la réalité mixte.
2. **Effectuez une mise à niveau vers la dernière version de votre graphique ou de votre moteur de jeux.** Les moteurs de jeu doivent prendre en charge la version 10.0.15063.0 du kit de développement logiciel (SDK) Windows 10 (publiée en avril 2017) ou une version ultérieure.
3. **Mettez à niveau les intergiciel, les plug-ins ou les composants.** Si votre application contient des composants, il est judicieux de procéder à une mise à niveau vers la dernière version. Les versions plus récentes des plug-ins les plus courants prennent en charge UWP.
4. **Supprimer les dépendances sur les kits de développement logiciel en double**. En fonction de l’appareil ciblé par votre contenu, vous devez supprimer ou compiler de façon conditionnelle ce kit de développement logiciel (par exemple, SteamVR) afin de pouvoir cibler les API Windows à la place.
5. **Résoudre les problèmes de génération.** À ce stade, l’exercice de Portage est spécifique à votre application, à votre moteur et aux dépendances de composants dont vous disposez.

## <a name="common-porting-steps"></a>Étapes de Portage courantes

### <a name="common-step-1-make-sure-you-have-the-right-development-hardware"></a>Étape courante 1 : Assurez-vous d’avoir le bon matériel de développement

La page [installer les outils](install-the-tools.md#for-immersive-vr-headset-development) répertorie le matériel de développement recommandé.

### <a name="common-step-2-upgrade-to-the-latest-flight-of-windows-10"></a>Étape 2 courante : mettre à niveau vers le dernier vol de Windows 10

La plateforme Windows Mixed Reality est toujours en cours de développement. Nous vous recommandons de [rejoindre le programme Windows Insider](https://insider.windows.com/) pour accéder au vol « Windows Insider Fast ».
1. Installer [Windows 10 Creators Update](https://www.microsoft.com/software-download/windows10)
2. [Participez](https://insider.windows.com/) au programme Windows Insider.
3. Activer le [mode développeur](https://docs.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
4. Basculer vers les [vols rapides Windows Insider](https://blogs.technet.microsoft.com/uktechnet/2016/07/01/joining-insider-preview) via les **paramètres > section mettre à jour la sécurité &**

### <a name="common-step-3-upgrade-to-the-most-recent-build-of-visual-studio-uwp-only"></a>Étape 3 courante : mettre à niveau vers la version la plus récente de Visual Studio (UWP uniquement)
* Consultez [installer la page outils](install-the-tools.md#installation-checklist) sous Visual Studio 2019

### <a name="common-step-4-be-ready-for-the-store-uwp-only"></a>Étape courante 4 : Soyez prêt pour le magasin (UWP uniquement)
* Utilisez le [Kit de certification des applications Windows](https://developer.microsoft.com/windows/develop/app-certification-kit) (également connu sous le nom de wack) tôt et souvent !
* Utiliser l' [Analyseur de portabilité](https://docs.microsoft.com/dotnet/standard/portability-analyzer) ([Téléchargement](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer))

### <a name="common-step-5-choose-the-correct-adapter"></a>Étape 5 courante : choisir l’adaptateur approprié
* Dans les systèmes tels que les blocs-notes avec deux GPU, [Ciblez l’adaptateur approprié](rendering-in-directx.md#hybrid-graphics-pcs-and-mixed-reality-applications). Cela s’applique aux applications d’Unity et DirectX natives où un ID3D11Device est créé, explicitement ou implicitement (Media Foundation), pour ses fonctionnalités.

## <a name="unity-porting-guidance"></a>Guide de Portage Unity

### <a name="unity-step-1-follow-the-common-porting-steps"></a>Étape 1 Unity : suivre les étapes de Portage courantes

Suivez toutes les étapes courantes. À l’étape #3, sélectionnez le **développement de jeux avec** la charge de travail Unity. Vous pouvez désélectionner le composant facultatif éditeur Unity, car vous installerez une version plus récente d’Unity à partir des instructions ci-dessous.

### <a name="unity-step-2-upgrade-to-the-latest-public-build-of-unity-with-windows-mr-support"></a>Étape 2 Unity : effectuez une mise à niveau vers la dernière version publique d’Unity avec prise en charge de Windows MR
1. Téléchargez la dernière [version publique recommandée d’Unity](install-the-tools.md) avec prise en charge de la réalité mixte.
2. Enregistrez une copie de votre projet avant de commencer
3. Consultez la [documentation](https://docs.unity3d.com/Manual/UpgradeGuides.html) disponible à partir de Unity sur le portage.
4. Suivez les [instructions](https://docs.unity3d.com/Manual/APIUpdater.html) sur le site de Unity pour utiliser son programme de mise à jour d’API automatique
5. Vérifiez s’il existe des modifications supplémentaires que vous devez apporter pour que votre projet s’exécute et pour traiter les erreurs et avertissements restants. 

> [!Note] 
> Si vous avez des intergiciels (middleware) dont vous dépendez, vérifiez que vous utilisez la dernière version (plus de détails à l’étape 3 ci-dessous).

### <a name="unity-step-3-upgrade-your-middleware-to-the-latest-versions"></a>Étape 3 Unity : mettre à niveau votre intergiciel vers les versions les plus récentes

Avec toute mise à jour Unity, il y a de bonnes chances que vous deviez mettre à jour un ou plusieurs packages middleware dont dépend votre jeu ou votre application. En outre, la mise à jour du middleware le plus récent augmente la probabilité de réussite tout au long du processus de Portage. De nombreux packages d’intergiciels (middleware) ont récemment ajouté la prise en charge de plateforme Windows universelle (UWP), et la mise à niveau vers les versions les plus récentes vous permettra de tirer parti de ce travail.

### <a name="unity-step-4-target-your-application-to-run-on-universal-windows-platform-uwp"></a>Étape 4 : cibler votre application pour qu’elle s’exécute sur plateforme Windows universelle (UWP)

Si vous ciblez Windows x86, vous pouvez ignorer cette étape et passer à l’étape 5.

Après avoir installé les outils, vous devez faire en sorte que votre application s’exécute en tant qu’application Windows universelle.

* Suivez les [instructions pas à pas détaillées](https://unity3d.com/partners/microsoft/porting-guides) fournies par Unity. Vous devez rester sur la toute dernière version de LTS (n’importe quelle version de 20xx. 4) pour Windows MR.
* Pour plus d’informations sur les ressources de développement UWP, consultez le [Guide de développement de jeux Windows 10](https://docs.microsoft.com/windows/uwp/gaming/e2e).

> [!NOTE]
> Unity continue d’améliorer la prise en charge de IL2CPP ; IL2CPP rend certains ports UWP plus faciles. Si vous ciblez actuellement le serveur principal de script .NET, vous devez envisager de convertir pour tirer parti du backend IL2CPP à la place.

* Vous pouvez ignorer « Unity Step 5 », car vous ciblez UWP au lieu de x86.

> [!NOTE] 
> Si votre application a des dépendances sur des services spécifiques à l’appareil, tels que la mise en correspondance à partir de la vapeur, vous devez les désactiver à cette étape. Vous pouvez vous connecter aux services équivalents fournis par Windows plus tard.

### <a name="unity-step-5-target-your-application-to-run-on-windows-x86"></a>Étape 5 : cibler votre application pour qu’elle s’exécute sous Windows x86

À l’intérieur de votre application Unity :

* Accéder aux paramètres de génération de > de fichiers
* Sélectionnez « PC, Mac, Linux standalone »
* Définir la plateforme cible sur « Windows »
* Définissez architecture sur « x86 », puis sélectionnez « changer la plateforme »


### <a name="unity-step-6-setup-your-windows-mixed-reality-hardware"></a>Étape 6 : configurer votre matériel Windows Mixed Reality
1. Passer en revue les étapes de [configuration du casque immersif](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/before-you-start
)
2. En savoir plus sur l' [utilisation du simulateur Windows Mixed Reality](using-the-windows-mixed-reality-simulator.md) et [la navigation dans la page d’informations Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)

### <a name="unity-step-7-target-your-application-to-run-on-windows-mixed-reality"></a>STEP 7 : cibler votre application pour qu’elle s’exécute sur Windows Mixed Reality
1. Tout d’abord, vous devez supprimer ou compiler de façon conditionnelle toute autre prise en charge de bibliothèque spécifique à un kit de développement logiciel (SDK) VR particulier. Ces ressources changent fréquemment les paramètres et les propriétés de votre projet de manière incompatible avec d’autres kits de développement logiciel (SDK) VR, tels que Windows Mixed Reality.
    * Par exemple, si votre projet fait référence au kit de développement logiciel (SDK) SteamVR, vous devez mettre à jour votre projet pour exclure ces appels d’API de prefabs et de script lors de l’exportation pour la cible de génération du Windows Store.
    * Les étapes spécifiques pour l’exclusion conditionnelle d’autres kits de développement logiciel VR sont bientôt disponibles.
2. Dans votre projet Unity, [Ciblez le kit de développement logiciel (SDK) Windows 10](holograms-100.md#target-windows-10-sdk)
3. Pour chaque scène, [configurer l’appareil photo](holograms-100.md#chapter-2---setup-the-camera)

### <a name="unity-step-8-use-the-stage-to-place-content-on-the-floor"></a>Step 8 : utiliser la phase pour placer le contenu à l’étage

Vous pouvez créer des expériences de réalité mixte sur une large gamme [d’expériences.](coordinate-systems.md)

Si vous déployez une expérience à l' **échelle assise**, vous devez vérifier que Unity est défini sur le type d’espace de suivi **fixe** :

```cs
XRDevice.SetTrackingSpaceType(TrackingSpaceType.Stationary);
```

Le code ci-dessus définit le système de coordonnées universel de Unity pour suivre le [cadre stationnaire de référence](coordinate-systems.md#spatial-coordinate-systems). Dans le mode de suivi fixe, le contenu placé dans l’éditeur juste devant l’emplacement par défaut de l’appareil photo (Forward is-Z) apparaît devant l’utilisateur au lancement de l’application. Pour recentrer l’origine assise de l’utilisateur, vous pouvez appeler XR de l’unité [. Méthode InputTracking. recenter](https://docs.unity3d.com/ScriptReference/XR.InputTracking.Recenter.html) .

Si vous effectuez une mise à l' **échelle permanente** ou une **expérience**de mise à l’échelle de l’espace, vous allez placer du contenu par rapport à l’étage. Vous avez raison de l’étage de l’utilisateur à l’aide de la **[Phase spatiale](coordinate-systems.md#spatial-coordinate-systems)**, qui représente l’origine de l’utilisateur et la limite facultative de l’espace, configurées lors de la première exécution. Pour ces expériences, vous devez vous assurer que Unity est défini sur le type d’espace de suivi **RoomScale** . Alors que RoomScale est la valeur par défaut, vous pouvez le définir explicitement et vous assurer que vous obtenez la valeur true, afin d’intercepter les situations où l’utilisateur a déplacé son ordinateur hors de la salle qu’il a étalonnée :

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

Une fois que votre application a correctement défini le type d’espace de suivi RoomScale, le contenu placé sur le plan y = 0 s’affiche sur le plancher. L’origine à (0, 0, 0) sera l’emplacement spécifique sur le plancher où l’utilisateur a pris la main pendant la configuration de la salle, avec-Z représentant la direction vers l’avant au cours de l’installation.

Dans le code de script, vous pouvez ensuite appeler la méthode TryGetGeometry sur vous êtes le type UnityEngine. expérimental. XR. Boundary pour obtenir un polygone de limite, en spécifiant un type de limite de TrackedArea. Si l’utilisateur a défini une limite (vous récupérez une liste de vertex), il est possible de fournir une expérience de mise à l’échelle de l' **espace** à l’utilisateur, où il peut se déplacer dans la scène que vous créez.

Le système affiche automatiquement la limite lorsque l’utilisateur l’approche. Votre application n’a pas besoin d’utiliser ce polygone pour restituer la limite elle-même.

Pour plus d’informations, consultez la page [systèmes de coordonnées dans Unity](coordinate-systems-in-unity.md) .

Certaines applications utilisent un rectangle pour limiter leur interaction. La récupération du plus grand rectangle inscrit n’est pas directement prise en charge dans l’API UWP ou Unity. L’exemple de code lié ci-dessous montre comment rechercher un rectangle dans les limites suivies. Il s’agit d’une méthode heuristique qui ne trouve pas la solution optimale, mais les résultats sont cohérents avec les attentes. Les paramètres de l’algorithme peuvent être réglés pour obtenir des résultats plus précis au détriment du temps de traitement. L’algorithme se trouve dans une fourche de la boîte à outils de réalité mixte qui utilise la version 5,6 Preview MRTP Unity. Cela n’est pas disponible publiquement. Le code doit être directement utilisable dans 2017,2 et versions ultérieures d’Unity. Le code sera porté sur le MRTK actuel dans un futur proche.

[fichier zip de code sur GitHub](https://github.com/KevinKennedy/MixedRealityToolkit-Unity/releases/tag/5.6.MRTP20) Fichiers importants :
* Ressources/HoloToolkit/stage/scripts/StageManager. cs-exemple d’utilisation
* Ressources/HoloToolkit/stage/scripts/LargestRectangle. cs-implémentation de l’algorithme
* Ressources/HoloToolkit-UnitTests/éditeur/stage/LargestRectangleTest. cs-test trivial de l’algorithme

Exemple de résultats :

![Exemple de résultats](images/largestrectangle-400px.jpg)

L’algorithme est basé sur un blog de Daniel Smilkov : le [plus grand rectangle dans un polygone](https://d3plus.org/blog/behind-the-scenes/2014/07/08/largest-rect/)

### <a name="unity-step-9-work-through-your-input-model"></a>Étape 9 Unity : utiliser votre modèle d’entrée

Chaque jeu ou application ciblant un HMD existant aura un ensemble d’entrées qu’il gère, les types d’entrées dont il a besoin pour l’expérience et les API spécifiques qu’il appelle pour obtenir ces entrées. Nous avons investi pour essayer de le rendre aussi simple et simple que possible pour tirer parti des entrées disponibles dans Windows Mixed Reality.
1. Lisez le **[Guide d’entrée pour Unity](input-porting-guide-for-unity.md)** pour plus d’informations sur la façon dont Windows Mixed Reality expose les entrées et sur la façon dont elles sont mappées à ce que votre application peut faire aujourd’hui.
2. Indiquez si vous souhaitez tirer parti de l’API d’entrée Cross-VR-SDK d’Unity ou de l’API d’entrée spécifique à MR. Les API d’entrée. GetButton/Input. GetAxis sont utilisées par les applications Unity VR aujourd’hui pour les entrées [Oculus](https://docs.unity3d.com/Manual/OculusControllers.html) et [OpenVR](https://docs.unity3d.com/Manual/OpenVRControllers.html). Si vos applications utilisent déjà ces API pour les contrôleurs de mouvement, il s’agit du chemin le plus simple. vous devez simplement remapper les boutons et les axes dans le gestionnaire d’entrée.
    * Vous pouvez accéder aux données du contrôleur de mouvement dans Unity à l’aide des API d’entrée. GetButton/Input. GetAxis, ou des API UnityEngine. XR. WSA. Input spécifiques à MR. (précédemment dans l’espace de noms UnityEngine. XR. WSA. Input dans Unity 5,6)
    * Consultez l' [exemple de la boîte à outils](https://github.com/Microsoft/HoloToolkit-Unity/pull/572) qui combine les contrôleurs de manette et de mouvement.

### <a name="unity-step-10-performance-testing-and-tuning"></a>Étape 10 : test et réglage des performances

Windows Mixed Reality sera disponible sur une vaste gamme d’appareils, allant des PC de jeux haut de gamme aux PC grand public. Selon le marché que vous ciblez, il existe une différence significative dans les budgets de calcul et graphiques disponibles pour votre application. Au cours de cet exercice de Portage, vous utilisez probablement un PC Premium et avez des budgets de calcul et graphiques importants disponibles pour votre application. Si vous souhaitez que votre application soit disponible pour un public plus large, vous devez tester et profiler votre application sur [le matériel représentatif que vous souhaitez cibler](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines).

[Unity](https://docs.unity3d.com/Manual/Profiler.html) et [Visual Studio](https://docs.microsoft.com/visualstudio/profiling/index) incluent des profileurs de performances, et [Microsoft](understanding-performance-for-mixed-reality.md) et [Intel](https://software.intel.com/articles/vr-content-developer-guide) publient des instructions sur le profilage et l’optimisation des performances. Une discussion complète sur les performances est disponible [pour comprendre les performances de la réalité mixte](understanding-performance-for-mixed-reality.md). En outre, il existe des détails spécifiques pour Unity sous [recommandations de performances pour Unity](performance-recommendations-for-unity.md).

## <a name="see-also"></a>Voir aussi
* [Guide de portage des entrées pour Unity](input-porting-guide-for-unity.md)
* [Instructions de compatibilité matérielle PC minimale pour Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)
* [Comprendre les performances de la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations en matière de performances pour Unity](performance-recommendations-for-unity.md)
* [Ajout de la prise en charge de Xbox Live à Unity pour UWP](https://docs.microsoft.com/windows/uwp/xbox-live/get-started-with-partner/partner-add-xbox-live-to-unity-uwp)
