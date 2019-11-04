---
title: Couleur, lumière et matériaux
description: La conception de contenu pour la réalité mixte nécessite d’accorder une attention particulière à la couleur, à l’éclairage et aux matériaux de chacune des ressources visuelles utilisées dans votre expérience.
author: mavitazk
ms.author: pinkb
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, design, Color, Light, Materials
ms.openlocfilehash: c49d88c2bb53c07adcb77e8dbb0e3cd77e1e78ae
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73436406"
---
# <a name="color-light-and-materials"></a>Couleur, lumière et matériaux

La conception de contenu pour la réalité mixte nécessite d’accorder une attention particulière à la couleur, à l’éclairage et aux matériaux de chacune des ressources visuelles utilisées dans votre expérience. Ces décisions peuvent être utilisées à des fins esthétiques, comme l’utilisation de la lumière et du matériau pour définir la tonalité d’un environnement immersif, et des fonctions fonctionnelles, comme l’utilisation de couleurs saisissantes pour alerter les utilisateurs d’une action imminente. Chacune de ces décisions doit être pesée par rapport aux opportunités et contraintes de l’appareil cible de votre expérience.

Vous trouverez ci-dessous des instructions spécifiques au rendu des ressources sur les casques immersifs et holographiques. Un grand nombre d’entre eux sont étroitement liés à d’autres domaines techniques et une liste de sujets connexes est disponible dans la section [Voir aussi](color,-light-and-materials.md#see-also) à la fin de cet article.

## <a name="rendering-on-immersive-vs-holographic-devices"></a>Rendu sur des appareils immersifs et holographiques

Le contenu rendu dans les casques immersifs s’affiche visuellement différent par rapport au contenu rendu dans les casques holographiques. Bien que les casques immersifs affichent généralement le contenu comme vous le feriez sur un écran 2D, les casques holographiques tels que les HoloLens utilisent des couleurs séquentielles, voir les affichages RGB pour afficher les hologrammes.

Prenez toujours le temps de tester vos expériences holographiques dans un casque holographique. L’apparence du contenu, même s’il est conçu spécifiquement pour les appareils holographiques, varie en fonction des analyses secondaires, des instantanés et de la vue spectateur. N’oubliez pas de vous familiariser avec les expériences d’un appareil, de tester l’éclairage des hologrammes et d’observer tous les côtés (ainsi que d’un niveau supérieur ou inférieur) de la façon dont votre contenu est rendu. Veillez à tester à une plage de paramètres de luminosité sur l’appareil, car il est peu probable que tous les utilisateurs partagent une valeur par défaut supposée, ainsi qu’un ensemble diversifié de conditions d’éclairage.

## <a name="fundamentals-of-rendering-on-holographic-devices"></a>Notions de base du rendu sur les appareils holographiques
* Les **appareils holographiques ont des affichages** supplémentaires : les hologrammes sont créés en ajoutant de la lumière à la lumière à partir du monde réel : le blanc s’affiche vivement, tandis que le noir apparaît en transparence.
* **L’impact des couleurs varie en fonction de l’environnement de l’utilisateur** : il existe de nombreuses conditions d’éclairage différentes dans la salle d’un utilisateur. Créez du contenu avec des niveaux de contraste appropriés pour faciliter la clarté.
* **Évitez l’éclairage dynamique** : les hologrammes qui sont allumés uniformément dans les expériences holographiques sont les plus efficaces. L’éclairage dynamique est susceptible de dépasser les capacités des appareils mobiles. Lorsque l’éclairage dynamique est requis, il est recommandé d’utiliser le [nuanceur standard Mixed Reality Toolkit standard](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_MRTKStandardShader.md). 

## <a name="designing-with-color"></a>Conception avec couleur

En raison de la nature des affichages additifs, certaines couleurs peuvent apparaître différentes sur les affichages holographiques. Certaines couleurs s’affichent dans les environnements d’éclairage, tandis que d’autres sont moins impactables. Les couleurs froides ont tendance à être remplacées en arrière-plan, tandis que les couleurs chaudes sautent au premier plan. Tenez compte de ces facteurs lorsque vous explorez les couleurs dans vos expériences :
* La **gamme** -HoloLens bénéficie d’une « gamme étendue » de couleurs, conceptuellement similaire à Adobe RGB. Par conséquent, certaines couleurs peuvent présenter des qualités et une représentation différentes dans l’appareil.
* **Gamma** : la luminosité et le contraste de l’image rendue varient en fonction des appareils immersifs et holographiques. Ces différences d’appareils semblent souvent faire apparaître des zones sombres de couleur et des ombres, plus ou moins lumineuses.
* **Séparation** des couleurs : également appelée « répartition des couleurs » ou « frange des couleurs », la séparation des couleurs se produit le plus souvent avec des hologrammes mobiles (y compris le curseur) quand un utilisateur effectue le suivi des objets avec leurs yeux.
* **Uniformité des couleurs** -en général, les hologrammes sont rendues suffisamment brillants pour maintenir l’uniformité des couleurs, quel que soit l’arrière-plan. Les grandes zones peuvent devenir nettes. Évitez les grandes zones de couleur lumineuse et unie.
* **Rendu des couleurs claires** : le blanc semble très brillant et doit être utilisé avec modération. Dans la plupart des cas, envisagez une valeur blanche autour de R 235 G 235 B 235. Les grandes zones lumineuses peuvent entraîner une gêne pour l’utilisateur.

**Rendu des couleurs sombres**

En raison de la nature des affichages additifs, les couleurs sombres sont transparentes. Un objet noir Uni n’est pas différent du monde réel. Voir canal alpha ci-dessous. Pour obtenir l’apparence « Black », essayez une valeur RVB grise très sombre, telle que 16, 16, 16.

![une gamme de couleurs standard ou large](images/640px-widegamut.png)<br>
*Gamme de couleurs standard et large*

## <a name="technical-considerations"></a>Considérations techniques
* **Alias** : Tenez compte des alias, des étapes en escalier ou des « étapes d’escalier » où le bord de la géométrie d’un hologramme répond au monde réel. L’utilisation de textures avec des détails élevés peut aggraver cet effet. Les textures doivent être mappées et le filtrage activé. Envisagez de faire déborder les bords des hologrammes ou d’ajouter une texture qui crée une bordure noire autour des objets. Évitez la géométrie fine lorsque cela est possible.
* **Canal alpha** : vous devez effacer votre canal alpha pour qu’il soit entièrement transparent pour les parties où vous n’effectuez pas le rendu d’un hologramme. Si vous laissez la valeur alpha non définie, les artefacts visuels sont pris en charge lors de la création d’images/de vidéos à partir de l’appareil ou de la vue spectateur.
* **Adoucissement des textures** -étant donné que la lumière est additive dans les affichages holographiques, il est préférable d’éviter les grandes zones de couleur lumineuse et unie, car elles ne produisent pas l’effet visuel souhaité.

## <a name="storytelling-with-light-and-color"></a>Narration avec lumière et couleur

Le clair et la couleur peuvent vous aider à faire apparaître vos hologrammes plus naturellement dans l’environnement d’un utilisateur, ainsi qu’à offrir des conseils et de l’aide à l’utilisateur. Pour les expériences holographiques, tenez compte de ces facteurs lorsque vous explorez l’éclairage et la couleur :

:::row:::
    :::column:::
* **Vignette** : l’effet « vignette » sur les matériaux obscurcis peut aider à attirer l’attention de l’utilisateur sur le centre du champ de l’affichage. Cet effet assombrit le matériau de l’hologramme à un rayon à partir du vecteur de pointage de l’utilisateur. Notez que cela est également efficace lorsque les vues de l’utilisateur s’hologramment à partir d’un angle oblique ou parcourant.<br>
* **Accentuation** : attirez l’attention sur les objets ou les points d’interaction en contrastant les couleurs, la luminosité et l’éclairage. Pour plus d’informations sur les méthodes d’éclairage dans le récits, consultez [pixels cinématographiques-approche d’éclairage pour les images informatiques](https://media.siggraph.org/education/cgsource/Archive/ConfereceCourses/S96/course30.pdf).<br>
        <br>
        *Image : utilisation de la couleur pour mettre en évidence les éléments de narration, présentés ici dans une scène à partir de [fragments](https://www.microsoft.com/p/fragments/9nblggh5ggm8).*
    :::column-end:::
        :::column:::
        ![Utilisation de la couleur pour mettre en évidence les éléments de narration, indiqués ici dans une scène à partir de fragments.](images/640px-fragments.jpg)<br>
    :::column-end:::
:::row-end:::


<br>

---

## <a name="see-also"></a>Articles associés
* [Séparation des couleurs](hologram-stability.md#color-separation)
* [Hologrammes](hologram.md)
* [Langue de design Microsoft-couleur](https://www.microsoft.com/design/color)
* [plateforme Windows universelle couleur](https://docs.microsoft.com/windows/uwp/style/color)
