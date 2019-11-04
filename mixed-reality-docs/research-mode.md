---
title: Mode de recherche HoloLens
description: En utilisant le mode de recherche sur HoloLens, une application peut accéder aux flux de capteur de périphérique clé (profondeur, suivi de l’environnement et réflectivité de l’IR).
author: davidgedye
ms.author: dgedye
ms.date: 05/03/2018
ms.topic: article
keywords: mode de recherche, CV, RS4, vision par ordinateur, recherche, HoloLens
ms.openlocfilehash: 307df0c226221422f13af09d8f4944c22ead3865
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438303"
---
# <a name="hololens-research-mode"></a>Mode de recherche HoloLens

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de la [mise à jour 2018 de Windows 10 avril](release-notes-april-2018.md) pour HoloLens et n’est pas disponible dans les versions antérieures.

Le mode de recherche est une nouvelle fonctionnalité de HoloLens qui permet à l’application d’accéder aux capteurs de clé sur l’appareil. Il s’agit des éléments suivants :
- Les quatre caméras de suivi de l’environnement utilisées par le système pour la création de cartes et le suivi des têtes.
- Deux versions des données de l’appareil photo de profondeur : une pour la détection presque approfondie à haute fréquence (30 i/s), couramment utilisée pour le suivi de la main, et l’autre pour la détection de profondeur à faible fréquence (1-5 FPS), actuellement utilisée par le mappage spatial,
- Deux versions d’un flux de réflectivité IR, utilisées par le HoloLens pour calculer la profondeur, mais précieuses à sa propre valeur, car ces images sont éclairées à partir du HoloLens et raisonnablement non affectées par la lumière ambiante.

capture d’écran de l’application en mode de recherche ![](images/sensor-stream-viewer.jpg)<br>
*Capture de réalité mixte d’une application de test qui affiche les huit flux de capteurs disponibles en mode de recherche*

## <a name="device-support"></a>Périphériques pris en charge

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Mode de recherche</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="before-using-research-mode"></a>Avant d’utiliser le mode de recherche

Le mode de recherche est bien nommé : il est destiné aux chercheurs universitaires et industriels qui essaient de nouvelles idées dans les domaines de la Vision par ordinateur et de la robotique.  Le mode de recherche n’est pas destiné aux applications qui seront déployées au sein d’une entreprise ou mises à disposition dans le Microsoft Store. Cela est dû au fait que le mode de recherche réduit la sécurité de votre appareil et consomme beaucoup plus d’énergie de batterie que le fonctionnement normal. Microsoft ne s’engage pas à prendre en charge ce mode sur les futurs appareils. Par conséquent, nous vous recommandons de l’utiliser pour développer et tester de nouvelles idées. Toutefois, vous ne serez pas en mesure de déployer largement des applications qui utilisent le mode de recherche ou qui ont l’assurance qu’elles continueront à fonctionner sur du matériel futur.

## <a name="enabling-research-mode"></a>Activation du mode de recherche

Le mode de recherche est un sous-mode du mode développeur. Vous devez d’abord activer le mode développeur dans l’application Paramètres (**paramètres > mise à jour & > de sécurité pour les développeurs**) :

1. Définir « utiliser les fonctionnalités pour les développeurs » **sur activé**
2. Définir « activer le portail des appareils » **sur activé**

Ensuite, à l’aide d’un navigateur Web connecté au même réseau Wi-Fi que votre HoloLens, accédez à l’adresse IP de votre HoloLens (obtenue via les **paramètres > réseau & Internet > les propriétés du matériel > Wi-Fi**). Il s’agit du portail de l' [appareil](using-the-windows-device-portal.md). vous trouverez une page « mode de recherche » dans la section « système » du portail :

![onglet du mode de recherche du portail de l’appareil HoloLens](images/ResearchModeDevPortal.png)<br>
*Mode de recherche dans le portail d’appareils HoloLens*

Après avoir sélectionné **autoriser l’accès aux flux de capteurs**, vous devrez redémarrer HoloLens. Vous pouvez le faire à partir du portail de l’appareil, sous l’élément de menu « Power » en haut de la page.

Une fois que votre appareil a redémarré, les applications qui ont été chargées par le biais du portail de l’appareil doivent pouvoir accéder aux flux en mode de recherche.

## <a name="using-sensor-data-in-your-apps"></a>Utilisation des données de capteur dans vos applications

Les applications peuvent accéder aux données de flux de capteur en ouvrant [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197) flux exactement de la même façon qu’ils accèdent au flux de caméra photo/vidéo. 

Toutes les API qui fonctionnent pour le développement HoloLens sont également disponibles en mode de recherche. En particulier, l’application peut savoir précisément où HoloLens se trouve dans l’espace 6DoF à chaque fois que la capture de l’image du capteur est terminée.

Des exemples d’applications qui montrent comment vous accédez aux différents flux en mode de recherche, comment utiliser les intrinsèques et les extrinsics et comment enregistrer des flux sont disponibles dans le [référentiel GitHub HoloLensForCV](https://github.com/Microsoft/HoloLensForCV).

## <a name="known-issues"></a>Problèmes connus

Consultez le [suivi des problèmes](https://github.com/Microsoft/HololensForCV/issues) dans le référentiel HoloLensForCV.

## <a name="see-also"></a>Articles associés

* [Microsoft Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197)
* [HoloLensForCV GitHub référentiel](https://github.com/Microsoft/HoloLensForCV)
* [Utilisation du portail d’appareil Windows](using-the-windows-device-portal.md)
