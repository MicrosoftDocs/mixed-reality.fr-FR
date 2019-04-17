---
title: Comprendre les performances pour la réalité mixte
description: Avancée des rubriques et des détails sur l’optimisation des performances pour les applications de réalité mixte Windows
author: Troy-Ferrell
ms.author: trferrel
ms.date: 3/26/2019
ms.topic: article
keywords: Windows mixte réalité, réalité mixte, réalité virtuelle, VR, MR, les performances, l’optimisation, UC, GPU
ms.openlocfilehash: ce59f9023c21dc7c981a2bb97d9fbd0c57622dbf
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596076"
---
# <a name="understanding-performance-for-mixed-reality"></a>Comprendre les performances pour la réalité mixte

Cet article est une introduction au rationalisation de l’importance des performances pour votre application de réalité mixte.  Expérience utilisateur peut se dégrader considérablement si votre application ne s’exécute pas à la fréquence d’images optimale. Hologrammes apparaîtront instables et principal suivi de l’environnement sera inexact conduisant à une mauvaise expérience pour l’utilisateur. En effet, les performances doivent être considérée comme une fonctionnalité de première classe pour le développement de réalité mixte et pas une stabilisation, à la fin de la tâche de cycle.

Pour la révision, les valeurs de fréquence d’images performante pour chaque plateforme cible sont répertoriées ci-dessous.

| Plateforme | Fréquence d’images cible |
|----------|-------------------|
| [HoloLens](hololens-hardware-details.md) | 60 FPS |
| [Windows Mixed Reality Ultra PC](immersive-headset-hardware-details.md) | 90 FPS |
| [Windows mixte réalité PC](immersive-headset-hardware-details.md) | 60 FPS |

Le framework ci-dessous donne un aperçu général pour les meilleures pratiques et une vue différente pour atteindre cible des fréquences d’images. Pour Explorer plus en détail, vous pouvez lire le [recommandations relatives aux performances pour l’article de Unity](performance-recommendations-for-unity.md). En particulier, cet article connexe explique comment mesurer la fréquence d’images dans votre application de réalité mixte Windows de Unity, ainsi que les étapes à suivre dans l’environnement Unity pour améliorer les performances.

## <a name="understanding-performance-bottlenecks"></a>Comprendre les goulots d’étranglement de performances

Si votre application a une fréquence d’images peu performantes, la première étape consiste à analyser et à comprendre où votre application est intensif. Il existe deux processeurs principales responsable de travail pour afficher votre scène : le processeur et le GPU. Chacun de ces deux composants gérer différentes opérations et les étapes de votre application de réalité mixte. Il existe trois endroits où les goulots d’étranglement peuvent se produire. 

1. **Application UC pour ce Thread -** -ce thread est responsable de votre logique d’application. Cela comprend le traitement d’entrée, des animations, physique et autres logique/état de l’application
2. **Rendre Thread - UC à GPU** -ce thread est chargé d’envoyer vos appels de dessin vers le GPU. Lorsque votre application veut afficher un objet tel qu’un cube ou modèle, ce thread envoie une demande au GPU, qui possède une architecture optimisée pour le rendu, pour effectuer ces opérations.
3. **GPU** - 
    ce processeur gère généralement du pipeline graphique de votre application pour transformer des données 3D (modèles, des textures, etc.) en pixels et produisent finalement une image 2D à envoyer à l’écran votre appareil.

![Durée de vie d’un Frame](images/lifetime-of-a-frame.png)

En règle générale, les applications de HoloLens seront limitée de GPU. Toutefois, cela n’est pas vrai dans chaque application et par conséquent, il est recommandé d’utiliser les outils et les techniques ci-dessous pour accéder à réelles pour votre application.

## <a name="how-to-analyze-your-application"></a>Comment analyser votre application

Il existe de nombreux outils qui vous permettent en tant que développeur de comprendre le profil de performance de votre application de réalité mixte. Ceux-ci vous permettront pour les deux cibles où vous avez les goulots d’étranglement et comment ils sont prend forme eux-mêmes pour déboguer les.

Il s’agit d’une liste des outils puissants et populaires pour obtenir des informations de profilage approfondies pour votre application.
- [Analyseurs de performances graphiques Intel](https://software.intel.com/gpa)
- [Débogueurs de Visual Studio Graphics](https://docs.microsoft.com/visualstudio/debugger/graphics/visual-studio-graphics-diagnostics?view=vs-2017)
- [Unity Profiler](https://docs.unity3d.com/Manual/Profiler.html)
- [Débogueur Unity Frame](https://docs.unity3d.com/Manual/FrameDebugger.html)

### <a name="how-to-profile-in-any-environment"></a>Comment profiler dans n’importe quel environnement

Il est un simple test pour déterminer rapidement que si vous êtes susceptible de GPU délimité ou un processeur limité dans votre application. Si vous diminuez la résolution de la sortie de cible de rendu, il existe moins pixels pour calculer et par conséquent, moins de travail GPU doit effectuer pour restituer une image. Fenêtre d’affichage de la mise à l’échelle (résolution dynamique mise à l’échelle) est la pratique de rendu de votre image à un petit cible de rendu, puis votre périphérique de sortie peut afficher. L’appareil sera jusqu'à l’échantillon à partir du plus petit jeu de pixels pour afficher votre image finale.

Après réduction de la résolution de rendu, si :
1) Fréquence d’images de l’application **augmente**, puis vous êtes susceptible de **GPU délimité**
1) Fréquence d’images de l’application **inchangé**, puis vous êtes susceptible de **limitées de l’UC**

>[!NOTE]
>Unity fournit la possibilité de modifier facilement la résolution de cible de rendu de votre application lors de l’exécution via le *[XRSettings.renderViewportScale](https://docs.unity3d.com/ScriptReference/XR.XRSettings-renderViewportScale.html)* propriété. L’image finale présentée sur l’appareil a une résolution fixe. La plateforme va échantillonner pour créer une image de résolution plus élevée pour le rendu sur les écrans de sortie une résolution inférieure. 
>
>```CS
>UnityEngine.XR.XRSettings.renderScale = 0.7f;
>```

## <a name="how-to-improve-your-application"></a>Comment améliorer votre application

### <a name="cpu-performance-recommendations"></a>Recommandations relatives aux performances de processeur

En règle générale, la plupart du travail dans une application de réalité mixte sur le processeur implique de « simulation » de la scène et la logique d’application unique approfondis de traitement. Par conséquent, les domaines suivants sont généralement ciblés pour l’optimisation.

- Animations
- Simplifier physique
- Allocations de mémoire
- Algorithmes complexes (ex.) cinématique inverse, la recherche de chemin d’accès)

### <a name="gpu-performance-recommendations"></a>Recommandations relatives aux performances de GPU

#### <a name="understanding-bandwidth-vs-fill-rate"></a>Taux de remplissage de comprendre la bande passante vs
Lors du rendu d’un frame sur le GPU, une application est généralement limitée par le taux de remplissage ou de la bande passante de mémoire.

- **Bande passante de mémoire** est le taux de lectures et écritures le GPU peut effectuer à partir de la mémoire
    - Pour identifier les limitations de bande passante, réduire la qualité de la texture et vérifiez si le taux de trames améliorées.
    - Dans Unity, cela est possible en modifiant **qualité de la Texture** dans **modifier** > **paramètres du projet**  >   **[ Paramètres de qualité](https://docs.unity3d.com/Manual/class-QualitySettings.html)**.
- **Taux de remplissage** fait référence au débit de pixels rendus qui peuvent être dessinées par seconde par le GPU.
    - Pour identifier les limites de taux de remplissage, diminuez la résolution d’affichage et vérifiez si le taux de trames améliorées. 
    - Dans Unity, cela est possible le *[XRSettings.renderViewportScale](https://docs.unity3d.com/ScriptReference/XR.XRSettings-renderViewportScale.html)* propriété

Bande passante de mémoire implique généralement des optimisations soit
1) diminuer les résolutions de texture
2) utiliser moins de textures (ex.) etc. spéculaire, Normals)

Taux de remplissage est principalement axé sur ce qui réduit le nombre d’opérations qui doivent être calculés pour un pixel de rendu final. Exemples de ce appartiennent généralement à ce qui réduit
1) nombre d’objets au rendu/processus
2) nombre d’opérations par le nuanceur
3) nombre d’étapes GPU pour résultat final (Nuanciers Géométrie post-traitement effets, etc.)
4) nombre de pixels à restituer (ex.) résolution d’affichage)

#### <a name="reduce-poly-count"></a>Réduire le nombre de poly
Polygone supérieur compte résultat dans des opérations plus pour le GPU et réduisant le nombre de polygones dans votre scène réduit la quantité de temps à rendre cette géométrie. D’autres facteurs impliqués ainsi lors de l’ombrage de la géométrie qui peut toujours être coûteuse, mais le compte de polygones est la mesure de base pour déterminer comment onéreux une scène sera à restituer.

#### <a name="limit-overdraw"></a>Limite de superposition

Superposition haut se produit lorsque plusieurs objets sont rendus, mais pas générés à l’écran comme ils sont masqués par un autre objet OCCLUSION généralement plus près. Imaginez examinant un mur ayant plusieurs salles et geometry derrière lui. Tous de la géométrie seraient traitée pour le rendu, mais uniquement le mur opaque doit vraiment être affiché comme il occludes l’affichage de tout autre contenu. Cela entraîne des opérations peu rentable qui ne sont pas nécessaires pour l’affichage actuel.

#### <a name="shaders"></a>Nuanceurs

Nuanceurs sont de petits programmes qui s’exécutent sur le GPU et déterminent généralement deux étapes importantes de rendu :
1) les sommets de l’objet doivent être dessinées sur l’écran et où elles se trouvent dans l’espace à l’écran (ex.) le nuanceur de sommets)
    - Le nuanceur de sommets est généralement exécuté par vertex pour chaque GameObject
2) les éléments à la couleur des pixels (ex.) le nuanceur de pixels)
    - Le nuanceur de pixels est exécuté par pixel pour la texture restituée pour périphérique présent

Nuanceurs effectuent généralement de nombreuses transformations et les calculs d’éclairage. Bien que les modèles d’éclairage complexes, des ombres et autres opérations peuvent générer des résultats fantastiques, ils s’accompagnent également un prix. En réduisant le nombre d’opérations calculées dans les nuanceurs peut réduire considérablement le travail global à effectuer par un GPU par trame.

##### <a name="shader-coding-recommendations"></a>Recommandations de codage de nuanceur

- Utiliser le filtrage bilinéaire autant que possible
- Réorganiser des expressions pour utiliser des fonctions intrinsèques MAD pour effectuer une multiplication et un ajout en même temps
- Précalculent autant que possible sur l’UC et de transmettre en tant que constantes à la documentation
- **Favoriser les opérations de déplacement à partir du nuanceur de pixels au nuanceur de sommets**
    - En règle générale, le nombre de vertex << # de pixels (ex.) 720p == 921,600 pixels, 1080p == 2,073,600 pixels, etc)

#### <a name="remove-gpu-stages"></a>Supprimer des étapes GPU
Effets de post-traitement peut s’avérer très coûteuse et généralement inhiber le taux de remplissage de votre application. Cela inclut également des techniques de l’anticrénelage, telles que MSAA. Sur HoloLens, il est recommandé d’éviter ces techniques entièrement. En outre, les étapes du nuanceur supplémentaires telles que geometry, convexe et nuanceurs de calcul doivent être évitées lorsque cela est possible.

## <a name="memory-recommendations"></a>Recommandations de mémoire
Opérations d’allocation et désallocation de mémoire excessive peuvent avoir des effets négatifs sur votre application holographique avec performances incohérent, cadres figés et autres comportements nuisibles. Il est particulièrement important de comprendre les considérations relatives à la mémoire lors du développement dans Unity, étant donné que la gestion de la mémoire est contrôlée par le garbage collector.

#### <a name="object-pooling"></a>Pool d’objets

Le pool d’objets est une technique répandue qui permet de réduire le coût des allocations continues & désallocations d’objets. Pour cela, en allouant un grand nombre d’objets identiques et en réutilisant les instances inactives, disponibles à partir de ce pool au lieu de constamment lors de la génération et la destruction d’objets au fil du temps. Les pools d’objet sont idéales pour des composants réutilisables qui possèdent la durée de vie des variable au cours d’une application.

## <a name="see-also"></a>Voir aussi
- [Recommandations relatives aux performances pour Unity](performance-recommendations-for-unity.md)
- [Paramètres recommandés pour Unity](recommended-settings-for-unity.md)
