---
title: Comprendre les performances de la réalité mixte
description: Rubriques avancées et détails sur l’optimisation des performances pour les applications Windows Mixed Reality
author: Troy-Ferrell
ms.author: trferrel
ms.date: 3/26/2019
ms.topic: article
keywords: Windows Mixed Reality, la réalité mixte, la réalité virtuelle, VR, MR, performances, optimisation, UC, GPU
ms.openlocfilehash: ce59f9023c21dc7c981a2bb97d9fbd0c57622dbf
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63548844"
---
# <a name="understanding-performance-for-mixed-reality"></a>Comprendre les performances de la réalité mixte

Cet article est une introduction à la rationalisation de l’importance des performances pour votre application de réalité mixte.  L’expérience utilisateur peut être très détériorée si votre application n’est pas exécutée à la fréquence d’images optimale. Les hologrammes apparaissent instables et le suivi des têtes de l’environnement est incorrect, conduisant à une expérience médiocre pour l’utilisateur. En effet, les performances doivent être considérées comme une fonctionnalité de première classe pour le développement de la réalité mixte et non une tâche de stabilisation, de fin de cycle.

À des fins de révision, les valeurs de fréquence d’images performante pour chaque plateforme cible sont répertoriées ci-dessous.

| Plateforme | Fréquence d’images cible |
|----------|-------------------|
| [HoloLens](hololens-hardware-details.md) | 60 FPS |
| [Windows Mixed Reality ultra PC](immersive-headset-hardware-details.md) | 90 FPS |
| [PC Windows Mixed Reality](immersive-headset-hardware-details.md) | 60 FPS |

Le cadre ci-dessous fournit un plan général pour les meilleures pratiques et des compréhensions pour atteindre les fréquences d’images cibles. Pour approfondir vos connaissances, prenez connaissance [des recommandations relatives aux performances de l’article Unity](performance-recommendations-for-unity.md). En particulier, cet article décrit comment mesurer la fréquence d’images dans votre application Windows Mixed Reality Unity, ainsi que les étapes à suivre dans l’environnement Unity pour améliorer les performances.

## <a name="understanding-performance-bottlenecks"></a>Comprendre les goulots d’étranglement des performances

Si votre application comporte une cadence de trames, la première étape consiste à analyser et à comprendre où votre application est gourmande en calculs. Deux processeurs principaux sont responsables du travail de rendu de votre scène: l’UC et le GPU. Chacun de ces deux composants gère différentes opérations et étapes de votre application de réalité mixte. Il existe trois emplacements clés où les goulots d’étranglement peuvent se produire. 

1. **Thread d’application-UC** : ce thread est responsable de la logique de votre application. Cela comprend le traitement des entrées, des animations, de la physique et d’autres logiques/États de l’application.
2. **Rendu thread-CPU au GPU** : ce thread est chargé d’envoyer vos appels de dessin au GPU. Lorsque votre application souhaite effectuer le rendu d’un objet tel qu’un cube ou un modèle, ce thread envoie une requête au GPU, qui a une architecture optimisée pour le rendu, pour effectuer ces opérations.
3. **GPU** - 
    Le plus souvent, ce processeur gère le pipeline graphique de votre application pour transformer des données 3D (modèles, textures, etc.) en pixels et produire une image 2D à envoyer à l’écran de votre appareil.

![Durée de vie d’un frame](images/lifetime-of-a-frame.png)

En règle générale, les applications HoloLens sont limitées par GPU. Toutefois, ce n’est pas vrai dans chaque application. il est donc recommandé d’utiliser les outils & techniques ci-dessous pour obtenir une application spécifique.

## <a name="how-to-analyze-your-application"></a>Comment analyser votre application

De nombreux outils vous permettent de comprendre le profil de performances de votre application de réalité mixte en tant que développeur. Ils vous permettront de cibler à la fois les goulots d’étranglement et la façon dont ils se manifestent pour les déboguer.

Il s’agit d’une liste d’outils populaires et puissants pour obtenir des informations de profilage détaillés pour votre application.
- [Analyseurs de performances graphiques Intel](https://software.intel.com/gpa)
- [Débogueurs graphiques Visual Studio](https://docs.microsoft.com/visualstudio/debugger/graphics/visual-studio-graphics-diagnostics?view=vs-2017)
- [Profileur Unity](https://docs.unity3d.com/Manual/Profiler.html)
- [Débogueur de frames Unity](https://docs.unity3d.com/Manual/FrameDebugger.html)

### <a name="how-to-profile-in-any-environment"></a>Comment Profiler dans n’importe quel environnement

Un test simple permet de déterminer rapidement si vous êtes susceptible de délimiter le GPU ou d’être limité par l’UC dans votre application. Si vous réduisez la résolution de la sortie de la cible de rendu, il y a moins de pixels à calculer et, par conséquent, moins de travail que le GPU doit effectuer pour afficher une image. La mise à l’échelle de la fenêtre d’affichage (mise à l’échelle dynamique) est la pratique qui consiste à rendre votre image sur une cible de rendu plus petite, alors que votre périphérique de sortie peut s’afficher. L’appareil dispose de l’échantillon de l’ensemble de pixels le plus petit pour afficher votre image finale.

Après une réduction de la résolution de rendu, si:
1) L’application de fréquence d’images **augmente**, vous êtes probablement limité par le **GPU**
1) Fréquence d’application inchangée, vous êtes probablement limité par l' **UC**

>[!NOTE]
>Unity offre la possibilité de modifier facilement la résolution de la cible de rendu de votre application au moment de l’exécution via la propriété *[XRSettings. renderViewportScale](https://docs.unity3d.com/ScriptReference/XR.XRSettings-renderViewportScale.html)* . La résolution de l’image finale présentée sur l’appareil est fixe. La plateforme échantillonne la sortie de résolution inférieure pour générer une image de résolution supérieure pour le rendu sur les affichages. 
>
>```CS
>UnityEngine.XR.XRSettings.renderScale = 0.7f;
>```

## <a name="how-to-improve-your-application"></a>Comment améliorer votre application

### <a name="cpu-performance-recommendations"></a>Recommandations relatives aux performances de l’UC

En règle générale, la plupart des travaux dans une application de réalité mixte sur l’UC impliquent la «simulation» de la scène et le traitement d’une logique d’application unique et complète. Par conséquent, les zones suivantes sont généralement destinées à l’optimisation.

- Animations
- Simplifier la physique
- Allocations de mémoire
- Algorithmes complexes (c.-à-d. cinématique inverse, recherche de chemin d’accès)

### <a name="gpu-performance-recommendations"></a>Recommandations relatives aux performances GPU

#### <a name="understanding-bandwidth-vs-fill-rate"></a>Fonctionnement de la bande passante et du taux de remplissage
Lors du rendu d’une trame sur le GPU, une application est généralement limitée par la bande passante de mémoire ou le taux de remplissage.

- La **bande passante** de la mémoire est le taux de lectures et d’écritures que le GPU peut exécuter à partir de la mémoire
    - Pour identifier les limitations de bande passante, réduisez la qualité de la texture et vérifiez si les images sont améliorées.
    - Dans Unity, vous pouvez effectuer cette opération en modifiant la qualité de la **texture** dans **modifier** > les paramètres de la **[qualité paramètres](https://docs.unity3d.com/Manual/class-QualitySettings.html)** du**projet** > .
- Le **taux de remplissage** fait référence au débit des pixels rendus qui peuvent être dessinés par seconde par le GPU.
    - Pour identifier les limitations du taux de remplissage, diminuez la résolution de l’affichage et vérifiez si les images sont améliorées. 
    - Dans Unity, cette opération peut être effectuée via la propriété *[XRSettings. renderViewportScale](https://docs.unity3d.com/ScriptReference/XR.XRSettings-renderViewportScale.html)*

La bande passante de la mémoire implique généralement des optimisations pour
1) réduire les résolutions de texture
2) Utilisez moins de textures (par exemple, Normals, spéculaire, etc.)

Le taux de remplissage est principalement axé sur la réduction du nombre d’opérations qui doivent être calculées pour un pixel rendu final. Des exemples de ce qui se limitent généralement à la réduction
1) nombre d’objets à restituer/traiter
2) nombre d’opérations par nuanceur
3) nombre d’étapes du GPU vers le résultat final (nuanceurs Geometry, effets de la postérieure au traitement, etc.)
4) nombre de pixels à afficher (c.-à-d. résolution d’affichage)

#### <a name="reduce-poly-count"></a>Réduire le nombre de poly
Des nombres de polygones plus élevés entraînent davantage d’opérations pour le GPU et la réduction du nombre de polygones dans votre scène réduira la durée de rendu de cette géométrie. D’autres facteurs sont impliqués dans l’ombrage de la géométrie qui peut toujours être coûteuse, mais le nombre de polygones est la mesure de base pour déterminer le coût de l’affichage d’une scène.

#### <a name="limit-overdraw"></a>Limiter le surdessin

Un surdessin élevé se produit lorsque plusieurs objets sont rendus mais non générés à l’écran, car ils sont masqués par un autre objet, en général plus proche de l’objet obturon. Imaginez qu’il s’agit d’un mur qui avait plusieurs pièces et une géométrie en arrière-plan. Toute la géométrie est traitée pour le rendu, mais seul le mur opaque doit vraiment être rendu, car il occludes la vue de tout autre contenu. Cela entraîne des opérations inutiles qui ne sont pas nécessaires pour l’affichage actuel.

#### <a name="shaders"></a>Nuanceurs

Les nuanceurs sont de petits programmes qui s’exécutent sur le GPU et déterminent généralement deux étapes importantes du rendu:
1) les sommets de l’objet qui doivent être dessinés à l’écran et l’emplacement où ils se trouvent dans l’espace à l’écran (c.-à-d. nuanceur de sommets)
    - Le nuanceur vertex est généralement exécuté par vertex pour chaque GameObject
2) comment colorer ces pixels (c.-à-d. nuanceur de pixels)
    - Le nuanceur de pixels est exécuté par pixel pour la texture rendue pour l’appareil présent

En général, les nuanceurs effectuent de nombreuses transformations et des calculs d’éclairage. Bien que les modèles d’éclairage complexes, les ombres et les autres opérations puissent générer des résultats fantastiques, ils sont également fournis avec un prix. La réduction du nombre d’opérations calculées dans les nuanceurs peut réduire considérablement le travail global nécessaire à la réalisation d’un GPU par trame.

##### <a name="shader-coding-recommendations"></a>Recommandations en matière de codage de nuanceur

- Utiliser le filtrage bilinéaire dans la mesure du possible
- Réorganiser les expressions pour utiliser des intrinsèques MAD afin d’effectuer une multiplication et un ajout en même temps
- Précalculez autant que possible sur le processeur et transmettez-les en tant que constantes au matériel.
- **Privilégier les opérations de déplacement du nuanceur de pixels vers le nuanceur de sommets**
    - En général, le nombre de vertex < < nombre de pixels (c.-à-d. 720p = = 921 600 pixels, 1080p = = 2 073 600 pixels, etc.)

#### <a name="remove-gpu-stages"></a>Supprimer les étapes du GPU
Les effets de la postérieure au traitement peuvent être très coûteux et, en général, inhiber le taux de remplissage de votre application. Cela comprend également des techniques d’anticrénelage telles que MSAA. Sur HoloLens, il est recommandé d’éviter ces techniques entièrement. En outre, des étapes de nuanceur supplémentaires, telles que Geometry, coque et les nuanceurs de calcul, doivent être évitées lorsque cela est possible.

## <a name="memory-recommendations"></a>Recommandations de mémoire
L’allocation de mémoire excessive & les opérations de désallocation peuvent avoir des effets négatifs sur votre application holographique, ce qui se traduit par des performances incohérentes, des trames figées et d’autres comportements nuisibles. Il est particulièrement important de comprendre les considérations relatives à la mémoire lors du développement dans Unity, car la gestion de la mémoire est contrôlée par le garbage collector.

#### <a name="object-pooling"></a>Mise en pool d’objets

Le mise en pool d’objets est une technique populaire pour réduire le coût des allocations continues & des désallocations d’objets. Pour ce faire, vous devez allouer un grand pool d’objets identiques et réutiliser les instances inactives de ce pool au lieu de générer et de détruire constamment des objets dans le temps. Les pools d’objets sont idéaux pour les composants réutilisables qui ont une durée de vie variable pendant une application.

## <a name="see-also"></a>Voir aussi
- [Recommandations de performances pour Unity](performance-recommendations-for-unity.md)
- [Paramètres recommandés pour Unity](recommended-settings-for-unity.md)
