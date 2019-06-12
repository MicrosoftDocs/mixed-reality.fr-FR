---
title: Mode de recherche de HoloLens
description: Utilisez le mode de recherche sur HoloLens, une application peut accéder aux flux de capteur clé d’appareil (profondeur, l’environnement de suivi et réflectivité de runtime d’intégration).
author: davidgedye
ms.author: dgedye
ms.date: 05/03/2018
ms.topic: article
keywords: mode de recherche, cv, rs4, vision par ordinateur, recherche, HoloLens
ms.openlocfilehash: e9a7683f8d582b459185066e74655e8f2b236db4
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829932"
---
# <a name="hololens-research-mode"></a>Mode de recherche de HoloLens

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de la [mettre à jour du 10 avril 2018 Windows](release-notes-april-2018.md) pour HoloLens et n’est pas disponible sur les versions antérieures.

Mode de recherche est une nouvelle fonctionnalité de HoloLens qui fournit l’accès d’application pour les capteurs de clé sur l’appareil. Par exemple :
- Les quatre environnement suivi des caméras utilisées par le système pour la création de la carte et de suivi principal.
- Deux versions des données de caméra profondeur – celui de détection de près de profondeur (30 i/s) à fréquence élevée, couramment utilisé de suivi dans la main et l’autre pour la fréquence inférieure (1 i/s) plus en profondeur de détection, actuellement utilisaient par le mappage Spatial,
- Deux versions d’un flux de runtime d’intégration-réflectivité, utilisé par le HoloLens pour calculer la profondeur, mais seront utiles à part entière comme ces images sont éclairés à partir de la HoloLens et raisonnablement pas affectés par la lumière ambiante.

![Capture d’écran de recherche en Mode application](images/sensor-stream-viewer.jpg)<br>
*Une capture de réalité mixte d’une application de test qui affiche les flux de huit capteurs disponibles en mode de recherche*

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Mode de recherche</td>
        <td>✔️</td>
        <td>❌</td>
    </tr>
</table>

## <a name="before-using-research-mode"></a>Avant d’utiliser le mode de recherche

Mode de recherche est également nommé : elle est conçue pour les chercheurs universitaires et industriels essayant de nouvelles idées dans les champs de la robotique et de vision par ordinateur.  Mode de recherche n’est pas destiné à être des applications qui seront déployées dans une entreprise ou à votre disposition dans le Microsoft Store. La raison à cela est que le mode de recherche réduit la sécurité de votre appareil et consomme beaucoup plus d’énergie à un fonctionnement normal. Microsoft ne valide pas à prendre en charge ce mode sur tous les périphériques futures. Par conséquent, nous vous recommandons de qu'utiliser il pour développer et tester de nouvelles idées ; Toutefois, vous ne serez pas en mesure de déployer largement les applications qui utilisent le mode de recherche ou ont n’importe quel assurance qu’il continue de fonctionner sur du matériel futures.

## <a name="enabling-research-mode"></a>L’activation du mode de recherche

Mode de recherche est un mode de sous-chemin de mode développeur. Vous devez d’abord activer le mode développeur dans l’application Paramètres (**Paramètres > mise à jour & sécurité > pour les développeurs**) :

1. La valeur « Utiliser les fonctionnalités de développement » **sur**
2. La valeur est « Activer le portail de l’appareil » **sur**

Puis en utilisant un navigateur web qui est connecté au même réseau Wi-Fi en tant que votre HoloLens, accédez à l’adresse IP de votre HoloLens (obtenues via **Paramètres > réseau & Internet > Wi-Fi > Propriétés de matériel**). Il s’agit du [appareil portail](using-the-windows-device-portal.md), et vous trouverez une page « Mode de recherche » dans la section « Système » du portail :

![Onglet du Mode recherche du portail d’appareil HoloLens](images/ResearchModeDevPortal.png)<br>
*Mode de recherche dans le portail des appareils HoloLens*

Après avoir sélectionné **autoriser l’accès au flux de données de capteur**, vous devrez redémarrer HoloLens. Pour cela, à partir du portail de l’appareil, sous l’élément de menu « Power » en haut de la page.

Une fois que votre appareil a redémarré, les applications qui ont été chargées via le portail de l’appareil doivent être en mesure d’accéder aux flux de mode de recherche.

## <a name="using-sensor-data-in-your-apps"></a>À l’aide des données de capteur dans vos applications

Applications peuvent accéder aux données de flux de données de capteur en ouvrant [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197) flux dans exactement la même façon qu’ils le flux de caméra vidéo/photo. 

Toutes les API qui fonctionnent pour le développement de HoloLens sont également disponibles en mode de recherche. En particulier, l’application peut savoir précisément où HoloLens dans 6DoF espace à chaque heure de capture de frame de capteur.

Exemples d’applications en montrant comment vous accéder aux différents flux de mode de recherche, comment utiliser les fonctions intrinsèques et extrinsics et comment enregistrer le flux de données sont disponibles dans le [référentiel GitHub de HoloLensForCV](https://github.com/Microsoft/HoloLensForCV).

## <a name="known-issues"></a>Problèmes connus

Consultez le [Traqueur](https://github.com/Microsoft/HololensForCV/issues) dans le référentiel HoloLensForCV.

## <a name="see-also"></a>Voir aussi

* [Microsoft Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197)
* [Référentiel GitHub de HoloLensForCV](https://github.com/Microsoft/HoloLensForCV)
* [Utilisation du portail d’appareil Windows](using-the-windows-device-portal.md)
