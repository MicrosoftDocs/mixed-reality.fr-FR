---
title: Prise en main MRTK version 2
description: Pour les nouveaux développeurs qui souhaitent en tirant parti de MRTK
author: grbury
ms.author: grbury
ms.date: 02/22/19
ms.topic: article
keywords: Windows Mixed Reality, test, version MRTK 2, MRTK, outils, SDK, HoloLens, HoloLens 2
ms.openlocfilehash: 44e5fe0fd4384af68922eda4bcb0594d39a1c1b7
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594238"
---
# <a name="getting-started-with-mrtk-version-2"></a>Prise en main MRTK version 2

Le MRTK est un kit d’outils open source étonnantes qui existe dans la mesure où le HoloLens est sorti et ne serait pas où il est aujourd'hui sans le gros du travail de notre communauté de développeurs qui ont contribué à ce dernier. Sur les 3 dernières années, nous avons écouté les commentaires de notre communauté de développeurs et généré MRTK version 2 pour tenir compte des principales préoccupations.  

La version 2 MRTK avec Unity est un kit de développement multiplateforme open source pour les applications de réalité mixte.  MRTK version 2 est destiné à accélérer le développement d’applications qui ciblent Microsoft HoloLens, des casques Windows Mixed Reality IMMERSIFS (VR) et plateforme de OpenVR. Le projet est destiné à réduire les barrières à l’entrée à créer des applications de réalité mixte et contribuer à la Communauté, tous les besoins d’évolution. 


Consultez le <a href="https://github.com/Microsoft/MixedRealityToolkit-Unity/wiki/Getting-Started-with-MRTK-v2" target="_blank">MRTK version 2 wiki</a> mise en route et en savoir plus.

## <a name="new-with-mrtk-version-2"></a>Nouveauté de MRTK version 2
Nous voulons souligner notre engagement à ces outils de plateforme.  En fait, nous avons exploité MRTK version 2 pour développer des expériences notre boîte de réception, tels que l’expérience d’installation (OOBE) et notre application Learning de réalité mixte.  Également attendez-vous à voir les nouvelles fonctionnalités de HoloLens 2 d’abord été exposées via MRTK, car nous pensons que c’est le meilleur moyen pour développer sur notre plateforme. 

### <a name="modular"></a>Modular
Nous avons l’intégré de manière modulaire, afin que vous n’avez pas besoin de tenir chaque bit du Kit de ressources de votre projet.  Il existe en fait quelques avantages à cela.  Il conserve la taille de votre projet plus petits, ainsi que des rend plus facile à gérer.  En plus de cela, car il est créé avec les objets scriptables et vise l’interface, il est également possible de remplacer les composants qui sont inclus avec votre propre pour prendre en charge d’autres services, les systèmes et plates-formes.


### <a name="cross-platform"></a>Système multiplateforme
En parlant d’autres plateformes, il a prise en charge multiplateforme.  Et, bien que cela ne signifie pas que chaque plateforme unique est prise en charge prête à l’emploi, nous avons veillé à ce que le code du Kit de ressources s’arrête lorsque vous basculez votre cible de build à d’autres plateformes.  La robustesse et l’extensibilité avec la conception modulaire configure sur un chemin d’accès bon pour être en mesure de prendre en charge plusieurs plateformes, telles que ARCore, ARKit et OpenVR.


### <a name="performant"></a>Performant
Utilisation des plateformes mobiles, nous avons construit avec des performances à l’esprit.  Ceci est très important, et nous souhaitions pour vous assurer que les outils vont pas fonctionner avec vous.


## <a name="see-also"></a>Voir aussi
* [Installer les outils](install-the-tools.md)
* [Portage de HTK/MRTK vers MRTK version 2](mrtk-porting-guide.md)
