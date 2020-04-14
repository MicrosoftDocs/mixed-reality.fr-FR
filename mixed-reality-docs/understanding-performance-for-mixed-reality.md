---
title: Comprendre les performances de la réalité mixte
description: Rubriques avancées et détails sur l’optimisation des performances pour les applications Windows Mixed Reality
author: troy-ferrell
ms.author: trferrel
ms.date: 3/26/2019
ms.topic: article
keywords: Windows Mixed Reality, la réalité mixte, la réalité virtuelle, VR, MR, performances, optimisation, UC, GPU
ms.openlocfilehash: 54e1eec5445fe655a0b498be5c18f08efe2270f0
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81277477"
---
# <a name="understanding-performance-for-mixed-reality"></a>Comprendre les performances de la réalité mixte

Cet article est une introduction à la compréhension de l’importance des performances de votre application de réalité mixte.  L’expérience utilisateur peut être très détériorée si votre application n’est pas exécutée à la fréquence d’images optimale. Les hologrammes apparaissent instables et le suivi des têtes de l’environnement n’est pas exact, ce qui entraîne une mauvaise expérience de l’utilisateur. Les performances doivent être considérées comme une fonctionnalité de première classe pour le développement de la réalité mixte et non pour une tâche polonaise.

Les valeurs de fréquence d’images performante pour chaque plateforme cible sont répertoriées ci-dessous.

| Plateforme | Fréquence d’images cible |
|----------|-------------------|
| [HoloLens](hololens-hardware-details.md) | 60 i/s |
| [Windows Mixed Reality ultra PC](immersive-headset-hardware-details.md) | 90 FPS |
| [PC Windows Mixed Reality](immersive-headset-hardware-details.md) | 60 i/s |

Le cadre ci-dessous décrit les meilleures pratiques pour atteindre les fréquences d’images cibles. Si vous développez dans Unity, lisez les [recommandations relatives aux performances de l’article Unity](performance-recommendations-for-unity.md) pour obtenir des conseils sur la mesure et l’amélioration de la fréquence d’images dans l’environnement Unity.

## <a name="understanding-performance-bottlenecks"></a>Comprendre les goulots d’étranglement des performances

Si votre application comporte une cadence de trames, la première étape consiste à analyser et à comprendre où votre application est gourmande en calculs. Deux processeurs principaux sont responsables du travail de rendu de votre scène : l’UC et le GPU. Chacun de ces éléments gère différents aspects de votre application de réalité mixte. Il existe trois emplacements clés où les goulots d’étranglement peuvent se produire : 

1. **Thread d’application-UC** : ce thread est responsable de la logique de votre application. Cela comprend le traitement des entrées, des animations, de la physique et d’autres logiques d’application.
2. **Rendu thread-CPU au GPU** : ce thread est chargé d’envoyer vos appels de dessin au GPU. Lorsque votre application souhaite afficher un objet tel qu’un cube ou un modèle, ce thread envoie une demande au GPU pour effectuer ces opérations.
3. **GPU** : ce processeur gère le plus souvent le pipeline graphique de votre application pour transformer des données 3D (modèles, textures, etc.) en pixels. Il produit finalement une image 2D à envoyer à l’écran de votre appareil.

![Durée de vie d’un frame](images/lifetime-of-a-frame.png)

En règle générale, les applications HoloLens sont liées au GPU, mais pas toujours. Utilisez les outils et les techniques ci-dessous pour comprendre où votre application particulière est engorgée.

## <a name="how-to-analyze-your-application"></a>Comment analyser votre application

De nombreux outils vous permettent de comprendre le profil de performances de votre application de réalité mixte. Ils vous permettront de déterminer où et pourquoi les goulots d’étranglement vous sont utiles. vous pouvez donc les résoudre.

Voici quelques outils courants pour obtenir des informations de profilage détaillés pour votre application :
- [Analyseurs de performances graphiques Intel](https://software.intel.com/gpa)
- [Débogueurs graphiques Visual Studio](https://docs.microsoft.com/visualstudio/debugger/graphics/visual-studio-graphics-diagnostics?view=vs-2017)
- [Profileur Unity](https://docs.unity3d.com/Manual/Profiler.html)
- [Débogueur de frames Unity](https://docs.unity3d.com/Manual/FrameDebugger.html)

### <a name="how-to-profile-in-any-environment"></a>Comment Profiler dans n’importe quel environnement

Une façon de déterminer si vous êtes lié au GPU ou à l’UC dans votre application est de réduire la résolution de la sortie de la cible de rendu. En réduisant le nombre de pixels à calculer, vous réduisez la charge du GPU. L’appareil est rendu sur une texture plus petite, puis sur un échantillon pour afficher votre image finale.

Après une réduction de la résolution de rendu, si :
1) L’application de fréquence d’images **augmente**, vous êtes probablement **lié au GPU**
1) Fréquence d’application **inchangée**, vous êtes probablement lié à l' **UC**

>[!NOTE]
>Unity offre la possibilité de modifier facilement la résolution de la cible de rendu de votre application au moment de l’exécution via la propriété *[XRSettings. renderViewportScale](https://docs.unity3d.com/ScriptReference/XR.XRSettings-renderViewportScale.html)* . La résolution de l’image finale présentée sur l’appareil est fixe. La plateforme échantillonne la sortie de résolution inférieure pour générer une image de résolution supérieure pour le rendu sur les affichages. 
>
>```CS
>UnityEngine.XR.XRSettings.renderScale = 0.7f;
>```

## <a name="how-to-improve-your-application"></a>Comment améliorer votre application

### <a name="cpu-performance-recommendations"></a>Recommandations sur les performances de processeur

En règle générale, la plupart des travaux dans une application de réalité mixte sur l’UC impliquent la « simulation » de la scène et le traitement de votre logique d’application. Les zones suivantes sont généralement destinées à l’optimisation :

- Animations
- Physique
- Allocations de mémoire
- Algorithmes complexes (c.-à-d. cinématique inverse, recherche de chemin d’accès)

### <a name="gpu-performance-recommendations"></a>Recommandations sur les performances de GPU

#### <a name="understanding-bandwidth-vs-fill-rate"></a>Fonctionnement de la bande passante et du taux de remplissage
Lors du rendu d’une trame sur le GPU, une application est généralement liée par la bande passante de mémoire ou le taux de remplissage.

- La **bande passante** de la mémoire est le taux de lectures et d’écritures que le GPU peut exécuter à partir de la mémoire
    - Pour identifier les limitations de bande passante, réduisez la qualité de la texture et vérifiez si la fréquence d’images a été améliorée.
    - Dans Unity, cette opération peut être effectuée en modifiant la qualité de la **texture** dans **modifier** > **paramètres du projet** > paramètres de **[qualité](https://docs.unity3d.com/Manual/class-QualitySettings.html)** .
- Le **taux de remplissage** fait référence aux pixels qui peuvent être dessinés par seconde par le GPU.
    - Pour identifier les limitations du taux de remplissage, diminuez la résolution de l’affichage et vérifiez si les images sont améliorées. 
    - Dans Unity, cette opération peut être effectuée via la propriété *[XRSettings. renderViewportScale](https://docs.unity3d.com/ScriptReference/XR.XRSettings-renderViewportScale.html)*

La bande passante de la mémoire implique généralement des optimisations pour :
1) Réduire les résolutions de texture
2) Utilisez moins de textures (normales, spéculaire, etc.)

Le taux de remplissage est axé sur la réduction du nombre d’opérations qui doivent être calculées pour un pixel rendu final. Cela comprend la réduction des éléments suivants :
1) Nombre d’objets à restituer/traiter
2) Nombre d’opérations par nuanceur
3) Nombre d’étapes du GPU vers le résultat final (nuanceurs Geometry, effets de la postérieure au traitement, etc.)
4) Nombre de pixels à afficher (résolution d’affichage)

#### <a name="reduce-polygon-count"></a>Réduire le nombre de polygones

Des nombres de polygones plus élevés entraînent davantage d’opérations pour le GPU. la [réduction du nombre de polygones](https://docs.microsoft.com/dynamics365/mixed-reality/import-tool/optimize-models#performance-targets) dans votre scène réduira le temps de rendu. D’autres facteurs sont impliqués dans l’ombrage de la géométrie qui peut être coûteuse, mais le nombre de polygones est la mesure la plus simple pour déterminer le coût de l’affichage d’une scène.

#### <a name="limit-overdraw"></a>Limiter le surdessin

Un surdessin élevé se produit lorsque plusieurs objets sont rendus mais non affichés à l’écran, car ils sont masqués par un objet occlusion. Imaginez que vous examinez un mur qui contient des objets en arrière-plan. Toute la géométrie est traitée pour le rendu, mais seul le mur opaque doit être rendu. Cela entraîne des opérations inutiles.

#### <a name="shaders"></a>Nuanceurs

Les nuanceurs sont des petits programmes qui s’exécutent sur le GPU et effectuent deux étapes importantes en matière de rendu :
1) Détermination des vertex à dessiner et de leur emplacement dans l’espace à l’écran (le nuanceur de sommets)
    - Le nuanceur vertex est généralement exécuté par vertex pour chaque maille.
2) Détermination de la couleur de chaque pixel (nuanceur de pixels)
    - Le nuanceur de pixels est exécuté par pixel rendu par la géométrie à la texture rendue.

En règle générale, les nuanceurs effectuent de nombreuses transformations et des calculs d’éclairage. Bien que les modèles d’éclairage complexes, les ombres et les autres opérations puissent générer des résultats fantastiques, ils sont également fournis avec un prix. La réduction du nombre d’opérations calculées dans les nuanceurs peut réduire considérablement le travail nécessaire pour le GPU par trame.

##### <a name="shader-coding-recommendations"></a>Recommandations en matière de codage de nuanceur

- Utiliser le filtrage bilinéaire, dans la mesure du possible
- Réorganiser les expressions pour utiliser des intrinsèques MAD afin d’effectuer une multiplication et un ajout en même temps
- Précalculez autant que possible sur le processeur et transmettez-les en tant que constantes au matériel.
- **Privilégier les opérations de déplacement du nuanceur de pixels vers le nuanceur de sommets**
    - En règle générale, le nombre de vertex est bien plus petit que le nombre de pixels (720p est de 921 600 pixels, 1080p est 2 073 600 pixels, etc.)

#### <a name="remove-gpu-stages"></a>Supprimer les étapes du GPU

Les effets postérieurs au traitement peuvent être très onéreux et augmenter le taux de remplissage de votre application. Cela comprend les techniques d’anticrénelage telles que MSAA. Sur HoloLens, il est recommandé d’éviter ces techniques entièrement, ainsi que des étapes de nuanceur supplémentaires telles que Geometry, la coque et les nuanceurs de calcul.

## <a name="memory-recommendations"></a>Recommandations sur la mémoire

Les opérations d’allocation et de désallocation de mémoire excessives peuvent entraîner des performances incohérentes, des frames figés et d’autres comportements nuisibles. Il est particulièrement important de comprendre les considérations relatives à la mémoire lors du développement dans Unity, car la gestion de la mémoire est contrôlée par le garbage collector.

#### <a name="object-pooling"></a>Mise en pool d’objets

Le mise en pool d’objets est une technique populaire pour réduire le coût des allocations et des désallocations continues d’objets. Pour la réaliser, vous devez allouer un grand pool d’objets identiques et réutiliser des instances inactives disponibles de ce pool au lieu de générer et détruire constamment des objets au fil du temps. Les pools d’objets conviennent parfaitement aux composants réutilisables qui ont une durée de vie variable pendant une application.

## <a name="see-also"></a>Voir aussi
- [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)
- [Paramètres recommandés pour Unity](recommended-settings-for-unity.md)
- [Optimiser les modèles 3D](https://docs.microsoft.com/dynamics365/mixed-reality/import-tool/optimize-models#performance-targets)
- [Meilleures pratiques pour la conversion et l’optimisation des modèles 3D en temps réel](https://docs.microsoft.com/dynamics365/mixed-reality/import-tool/best-practices)

