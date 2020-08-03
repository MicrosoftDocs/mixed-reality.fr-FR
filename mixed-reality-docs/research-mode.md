---
title: Mode de recherche HoloLens
description: En utilisant le mode de recherche sur HoloLens, une application peut accéder aux flux de capteur de périphérique clé (profondeur, suivi de l’environnement et réflectivité de l’IR).
author: hferrone
ms.author: v-haferr
ms.date: 07/31/2020
ms.topic: article
keywords: Mode de recherche, CV, RS4, vision par ordinateur, recherche, HoloLens, HoloLens 2
ms.openlocfilehash: dd49186d1218b6a6a6c9a8d5943159daad3bcefb
ms.sourcegitcommit: 36316e2658d3dfa804d798b9f4fb2f9186052144
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/01/2020
ms.locfileid: "87507693"
---
# <a name="hololens-research-mode"></a>Mode de recherche HoloLens

Le mode de recherche a été introduit dans le HoloLens de 1re génération pour permettre l’accès aux capteurs de clé sur l’appareil, en particulier pour les applications de recherche qui ne sont pas destinées au déploiement.  Le mode de recherche pour HoloLens 2 conserve les fonctionnalités de HoloLens 1, en ajoutant l’accès aux flux supplémentaires :

* **Caméras de suivi de l’environnement clair visibles** -caméras de nuances de gris utilisées par le système pour le suivi des têtes et la génération de cartes.
* **Appareil photo de profondeur** : fonctionne en deux modes :  
    + Détection presque-profondeur AHAT, à fréquence élevée (45 FPS) utilisée pour le suivi des handles. De la même façon que le mode de levée abrégée de la première version, AHAT fournit une Pseudo-profondeur avec un retour à la ligne au-delà de 1 mètre. 
    + Détection de longueurs longues, à faible fréquence (1-5 FPS), utilisée par le [mappage spatial](spatial-mapping.md)

* **Deux versions du flux de réflectivité IR** -utilisées par le HoloLens pour calculer la profondeur. Ces images sont éclairées par infrarouge et ne sont pas affectées par la lumière visible ambiante.

Si vous utilisez un HoloLens 2, vous avez également accès aux entrées supplémentaires ci-dessous :

* **Accéléromètre** : utilisé par le système pour déterminer l’accélération linéaire le long des axes X, Y et Z et la gravité.
* **Gyroscope** : utilisé par le système pour déterminer les rotations.
* **Magnétomètre** : utilisé par le système pour estimer l’orientation absolue.

> [!IMPORTANT]
> Le mode de recherche est actuellement en version préliminaire publique. Les exemples, les didacticiels et la documentation complète de l’API HoloLens 2 seront disponibles sur [ECCV 2020](https://eccv2020.eu/
 ) dans le référentiel git en mode de recherche.

![Capture d’écran de l’application en mode recherche](images/sensor-stream-viewer.jpg)<br>
*Capture de réalité mixte d’une application de test qui affiche les huit flux de capteurs disponibles en mode de recherche*

## <a name="usage"></a>Usage

Le mode de recherche est conçu pour les chercheurs universitaires et industriels qui explorent de nouvelles idées dans les domaines de la Vision par ordinateur et de la robotique.  Elle n’est pas destinée aux applications déployées dans des environnements d’entreprise ou disponibles via le Microsoft Store ou d’autres canaux de distribution.

En outre, Microsoft ne garantit pas que le mode de recherche ou les fonctionnalités équivalentes seront pris en charge dans les futures mises à jour du matériel ou du système d’exploitation. Toutefois, cela ne vous empêche pas de l’utiliser pour développer et tester de nouvelles idées !

## <a name="security-and-performance"></a>Sécurité et performances

N’oubliez pas que l’activation du mode de recherche utilise davantage de batterie que l’utilisation de la mise à l’aide du système HoloLens 2 dans des conditions normales. Cela est vrai même si l’application qui utilise les fonctionnalités du mode de recherche n’est pas en cours d’exécution.  L’activation de ce mode peut également réduire la sécurité globale de votre appareil, car les applications peuvent avoir recours à des données de capteur.  Vous trouverez plus d’informations sur la sécurité des appareils dans le [Forum aux questions sur la sécurité HoloLens](https://docs.microsoft.com/hololens/hololens-faq-security).  

## <a name="device-support"></a>Prise en charge des appareils
<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" /> </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens1-hardware"><strong>HoloLens (1ère génération)</strong></a></td>
        <td><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></a></td>
    </tr>
     <tr>
        <td>Caméras de suivi des têtes</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td>Caméra de profondeur & IR</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td>Accéléromètre</td>
        <td>❌</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td>Gyroscope</td>
        <td>❌</td>
        <td>✔️</td>
    </tr>
    <tr>
        <td>Magnétomètre</td>
        <td>❌</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="enabling-research-mode-hololens-1st-gen-and-hololens-2"></a>Activation du mode de recherche (HoloLens 1re génération et HoloLens 2)

Le mode de recherche est une extension du mode développeur. Avant de commencer, les fonctionnalités de développement de l’appareil doivent être activées pour accéder aux paramètres du mode de recherche : 

* Ouvrez le **menu démarrer > paramètres** , puis sélectionnez **mises à jour**.
* Sélectionnez **pour les développeurs** et activer le **mode développeur**.
* Faites défiler la liste et activez le **portail d’appareil**.

Une fois les fonctionnalités du développeur activées, [Connectez-vous au portail de l’appareil](https://docs.microsoft.com/windows/uwp/debug-test-perf/device-portal-hololens) pour activer les fonctionnalités du mode de recherche :

* Accédez à **système > le mode de recherche** dans le portail de l' **appareil**.
* Sélectionnez **autoriser l’accès au flux de capteur**.
* Redémarrez l’appareil à partir de l’élément de menu **Power** situé en haut de la page.

Une fois que vous avez redémarré l’appareil, les applications chargées via le portail de l' **appareil** peuvent accéder aux flux en mode de recherche.

![Onglet mode de recherche du portail de l’appareil HoloLens](images/ResearchModeDevPortal.png)<br>
*Fenêtre du mode de recherche dans le portail d’appareils HoloLens*

> [!IMPORTANT]
> Le mode de recherche pour HoloLens 2 est disponible à partir de la build 19041,1356. Si vous avez besoin d’accéder à une version antérieure, inscrivez-vous à notre programme [Insider Preview](https://docs.microsoft.com/hololens/hololens-insider) .

### <a name="using-sensor-data-in-your-apps"></a>Utilisation des données de capteur dans vos applications

Les applications peuvent accéder aux données de flux de capteur de la même façon que les flux de photos et les vidéos de caméra vidéo sont accessibles par le biais de [Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197). 

Toutes les API qui fonctionnent pour le développement HoloLens sont également disponibles en mode de recherche. En particulier, l’application sait précisément où HoloLens se trouve dans l’espace 6DoF à chaque fois que la capture de l’image du capteur est terminée.

Vous trouverez des exemples d’applications sur l’accès aux différents flux en mode de recherche, sur l’utilisation des [intrinsèques et des extrinsics](https://docs.microsoft.com/windows/mixed-reality/locatable-camera#locating-the-device-camera-in-the-world), et sur l’enregistrement des flux dans le [HoloLensForCV GitHub référentiel](https://github.com/Microsoft/HoloLensForCV) référentiel.

 > [!NOTE]
 > À ce stade, l’exemple HoloLensForCV ne fonctionne pas sur HoloLens 2.

## <a name="support"></a>Support

Utilisez le [suivi](https://github.com/Microsoft/HololensForCV/issues) des problèmes dans le référentiel HoloLensForCV pour publier des commentaires et effectuer le suivi des problèmes connus.

## <a name="see-also"></a>Voir aussi

* [Microsoft Media Foundation](https://msdn.microsoft.com/library/windows/desktop/ms694197)
* [HoloLensForCV GitHub référentiel](https://github.com/Microsoft/HoloLensForCV)
* [Utilisation du portail d’appareil Windows](using-the-windows-device-portal.md)
