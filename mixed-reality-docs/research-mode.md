---
title: Mode de recherche HoloLens
description: En utilisant le mode de recherche sur HoloLens, une application peut accéder aux flux de capteur de périphérique clé (profondeur, suivi de l’environnement et réflectivité de l’IR).
author: hferrone
ms.author: v-haferr
ms.date: 05/03/2018
ms.topic: article
keywords: mode de recherche, CV, RS4, vision par ordinateur, recherche, HoloLens, HoloLens 2
ms.openlocfilehash: ec6f7b73a1f25932f10c10a7f0daaf78e536c0c4
ms.sourcegitcommit: 7f50210b71a65631fd1bc3fdb215064e0db34333
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84533101"
---
# <a name="hololens-research-mode"></a>Mode de recherche HoloLens

## <a name="overview"></a>Vue d’ensemble

Le mode de recherche a été introduit dans le HoloLens de 1re génération pour permettre l’accès aux capteurs de clé sur l’appareil, en particulier pour les applications de recherche qui ne sont pas destinées au déploiement. Vous pouvez maintenant collecter des données à partir des entrées suivantes :

* **Caméras de suivi de l’environnement clair visibles** -utilisées par le système pour le suivi des têtes et la génération de cartes.
* **Appareil photo de profondeur** : fonctionne en deux modes :  
    + Détection quasi-profondeur (30 i/s) à court terme et à fréquence élevée utilisée pour le suivi de la [main](interaction-fundamentals.md)
    + Détection de longueurs longues, à faible fréquence (1-5 FPS), utilisée par le [mappage spatial](spatial-mapping.md)
* **Deux versions du flux de réflectivité IR** -utilisées par le HoloLens pour calculer la profondeur. Ces images sont éclairées par infrarouge et ne sont pas affectées par la lumière visible ambiante.

Si vous utilisez un HoloLens 2, vous pouvez également accéder aux entrées suivantes :

* **Accéléromètre** : utilisé par le système pour déterminer l’accélération linéaire le long des axes X, Y et Z et la gravité.
* **Gyroscope** : utilisé par le système pour déterminer les rotations.
* **Magnétomètre** : utilisé par le système pour estimer l’orientation absolue.

![Capture d’écran de l’application en mode recherche](images/sensor-stream-viewer.jpg)<br>
*Capture de réalité mixte d’une application de test qui affiche les huit flux de capteurs disponibles en mode de recherche*

> [!NOTE]
> La fonctionnalité du mode de recherche a été ajoutée dans le cadre de la [mise à jour 2018 de Windows 10 avril](release-notes-april-2018.md) pour HoloLens et n’est pas disponible dans les versions antérieures.

## <a name="usage"></a>Usage

Le mode de recherche est conçu pour les chercheurs universitaires et industriels qui explorent de nouvelles idées dans les domaines de la Vision par ordinateur et de la robotique.  Elle n’est pas destinée aux applications déployées dans des environnements d’entreprise ou disponibles via le Microsoft Store ou d’autres canaux de distribution.

En outre, Microsoft ne garantit pas que le mode de recherche ou les fonctionnalités équivalentes seront pris en charge dans les futures mises à jour du matériel ou du système d’exploitation. Toutefois, cela ne vous empêche pas de l’utiliser pour développer et tester de nouvelles idées !

## <a name="security-and-performance"></a>Sécurité et performances

N’oubliez pas que l’activation du mode de recherche utilise davantage de batterie que l’utilisation de la mise à l’aide du système HoloLens 2 dans des conditions normales. Cela est vrai même si l’application qui utilise les fonctionnalités du mode de recherche n’est pas en cours d’exécution.  L’activation de ce mode peut également réduire la sécurité globale de votre appareil, car les applications peuvent avoir recours à des données de capteur.  Vous trouverez plus d’informations sur la sécurité des appareils dans le [Forum aux questions sur la sécurité HoloLens](https://docs.microsoft.com/hololens/hololens-faq-security).  


## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="50%" />
    <col width="50%" />
    <!-- <col width="33%" /> -->
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>1re génération de HoloLens</strong></a></td>
        <!-- <td><a href="hololens2-hardware.md"><strong>HoloLens 2</strong></a></td> -->
    </tr>
     <tr>
        <td>Caméras de suivi des têtes</td>
        <td>✔️</td>
        <!-- <td>❌</td> -->
    </tr>
    <tr>
        <td>Caméra de profondeur & IR</td>
        <td>✔️</td>
        <!-- <td>❌</td> -->
    </tr>
    <tr>
        <td>Accéléromètre</td>
        <td>❌</td>
        <!-- <td>❌</td> -->
    </tr>
    <tr>
        <td>Gyroscope</td>
        <td>❌</td>
        <!-- <td>❌</td> -->
    </tr>
    <tr>
        <td>Magnétomètre</td>
        <td>❌</td>
        <!-- <td>❌</td> -->
    </tr>
</table>

> [!IMPORTANT]
> La prise en charge du mode de recherche pour HoloLens 2 devrait être disponible en version préliminaire publique en juillet 2020 et inclura toutes les fonctionnalités mentionnées ci-dessus. Pour plus d’informations, revenez à la. 

## <a name="enabling-research-mode"></a>Activation du mode de recherche

Le mode de recherche est une extension du mode développeur. Avant de commencer, les fonctionnalités de développement de l’appareil doivent être activées pour accéder aux paramètres du mode de recherche : 

* Ouvrez le **menu démarrer > paramètres** , puis sélectionnez **mises à jour**.
* Sélectionnez **pour les développeurs** et activer le **mode développeur**.
* Faites défiler l’appareil et activez le **portail des appareils**.

Une fois les fonctionnalités du développeur activées, [Connectez-vous au portail](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens) de l’appareil pour activer les fonctionnalités du mode de recherche.

Sur *HoloLens 1re génération*:

* Accédez à **système > le mode de recherche** dans le portail de l' **appareil**.
* Sélectionnez **autoriser l’accès au flux de capteur**.
* Redémarrez l’appareil à partir de l’élément de menu **Power** situé en haut de la page.

Une fois que vous avez redémarré l’appareil, les applications chargées via le portail de l' **appareil** peuvent accéder aux flux en mode de recherche.

![Onglet mode de recherche du portail de l’appareil HoloLens](images/ResearchModeDevPortal.png)<br>
*Fenêtre du mode de recherche dans le portail d’appareils HoloLens*

## <a name="using-sensor-data-in-your-apps"></a>Utilisation des données de capteur dans vos applications

*1re génération de HoloLens*

Les applications peuvent accéder aux données de flux de capteur de la même façon que les flux de photos et les vidéos de caméra vidéo sont accessibles par le biais de [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197). 

Toutes les API qui fonctionnent pour le développement HoloLens sont également disponibles en mode de recherche. En particulier, l’application sait précisément où HoloLens se trouve dans l’espace 6DoF à chaque fois que la capture de l’image du capteur est terminée.

Vous trouverez des exemples d’applications sur l’accès aux différents flux en mode de recherche, sur l’utilisation des [intrinsèques et des extrinsics](https://docs.microsoft.com/windows/mixed-reality/locatable-camera#locating-the-device-camera-in-the-world), et sur l’enregistrement des flux dans le [HoloLensForCV GitHub référentiel](https://github.com/Microsoft/HoloLensForCV) référentiel.

 > [!NOTE]
 > À ce stade, l’exemple HoloLensForCV ne fonctionne pas sur HoloLens 2.

## <a name="known-issues"></a>Problèmes connus

Vous pouvez utiliser le [suivi](https://github.com/Microsoft/HololensForCV/issues) des problèmes dans le référentiel HoloLensForCV pour suivre les problèmes connus.

## <a name="see-also"></a>Voir aussi

* [Microsoft Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197)
* [HoloLensForCV GitHub référentiel](https://github.com/Microsoft/HoloLensForCV)
* [Utilisation du portail d’appareil Windows](using-the-windows-device-portal.md)
