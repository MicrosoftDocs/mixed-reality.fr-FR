---
title: Auto
description: L’étalonnage de votre IPD (distance interpupillary) peut améliorer la qualité de vos visuels. Les casques immersifs HoloLens et Windows Mixed Reality offrent des moyens de personnaliser la IPD.
author: xerxesb85
ms.author: xerxesb
ms.date: 02/24/2019
ms.topic: article
keywords: étalonnage, confort, visuels, qualité, IPD
ms.openlocfilehash: 1fc3904f4b3e441a967616f20e4287dbc7f08835
ms.sourcegitcommit: 3b32339c5d5c79eaecd84ed27254a8f4321731f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70047052"
---
# <a name="improve-visual-quality-and-comfort"></a>Améliorez la qualité visuelle et le confort
Les casques immersifs HoloLens, HoloLens 2 et Windows Mixed Reality offrent des méthodes différentes pour améliorer la qualité de l’expérience visuelle. 

## <a name="hololens-2"></a>Hololens 2

### <a name="calibration"></a>Auto

Hololens 2 est conçu pour fournir l’image visuelle et le confort les plus élevés pour nos clients. La technologie de suivi oculaire est utilisée pour améliorer l’expérience utilisateur de la visualisation et de l’interaction avec l’environnement virtuel.  
Sur HoloLens 2, vous serez invité à étalonner vos visuels pendant la configuration de l’appareil. Les utilisateurs sont invités à examiner l’ensemble des cibles de fixation. Cela permet à l’appareil d’ajuster le rendu de l’hologramme pour l’utilisateur afin de garantir des hologrammes correctement positionnés, une expérience d’affichage 3D confortable et une meilleure qualité d’affichage. Tous les ajustements se produisent à la volée, sans nécessiter de paramétrage manuel. En utilisant les yeux comme points de repère, l’appareil est ajusté pour chaque utilisateur et les visuels sont réglés à mesure que le casque passe légèrement tout au long de l’utilisation. Le suivi de la position oculaire est utilisé en interne par le système et les développeurs n’ont rien à faire pour tirer parti de cette fonctionnalité. Ces informations ne sont pas disponibles pour les développeurs. Sur Hololens 2, l’exécution de l’étalonnage garantit également un suivi des yeux oculaires précis pour chaque utilisateur. L’eye-tracking permet aux applications de savoir où l’utilisateur regarde en temps réel. Il s’agit de la fonctionnalité principale que les développeurs peuvent exploiter pour activer un tout nouveau niveau de contexte, une compréhension humaine et des interactions au sein de l’expérience holographique.  
L’étalonnage est stocké localement sur l’appareil et n’est associé à aucune information de compte. Il n’existe aucun enregistrement de qui a utilisé l’appareil sans étalonnage. Cela signifie que les nouveaux utilisateurs seront invités à étalonner des visuels lorsqu’ils utilisent l’appareil pour la première fois, ainsi qu’à des utilisateurs qui ont opté pour l’étalonnage précédemment ou en cas d’échec de l’étalonnage. L’étalonnage peut toujours être supprimé de l’appareil dans **paramètres** > **protection** > **oculaire**. 

### <a name="calibration-failures"></a>Échecs d’étalonnage

L’étalonnage doit fonctionner pour la plupart des utilisateurs, mais dans certains cas, il se peut que l’utilisateur ne puisse pas l’étalonner correctement.  
Voici quelques exemples d’échecs d’étalonnage:
- L’utilisateur est gêné et ne suit pas les objectifs d’étalonnage pendant l’expérimentation
- Visière d’appareil sale ou rayé ou visière d’appareil non positionné correctement 
- Verres sale ou rayé
- Certains types de lentilles et de lunettes de contact (lentilles de contact colorées, certaines lentilles de contact Toric, lunettes de blocage IR, des verres de prescription élevés, des lunettes de soleil, etc.)
- Composition plus prononcée, certaines extensions cils
- Occlusions d’oeil et/ou visière d’appareil (cheveux, quelques montures de lunettes épaisses)
- La physiologie oculaire, certaines conditions oculaires et/ou une chirurgie oculaire (quelques yeux étroits, des cils longs, amblyopia, nystagmus, certains cas de LASIK ou d’autres Surgeries oculaires, etc.)

Si l’étalonnage échoue, essayez l’un de ces correctifs: 
- Nettoyer votre visière d’appareils
- Nettoyez vos lunettes
- Poussez vos visières d’appareils dans
- Assurez-vous que rien n’obstrue les capteurs ou vos yeux (par exemple, cheveux) 
- Assurez-vous qu’il y a suffisamment de lumière dans votre espace et que vous n’êtes pas sous le soleil direct
- Vérifier que vous suivez soigneusement les cibles pendant l’étalonnage

Si vous avez suivi toutes les instructions et que l’étalonnage est toujours en échec, vous pouvez désactiver l’invite d’étalonnage dans **paramètres** > **étalonnage**du**système** > . Quand une nouvelle personne utilise ce Hololens, l’option demander automatiquement un étalonnage oculaire doit être désactivée. Sachez que cela peut entraîner une dégradation de la qualité et de la gêne de rendu des hologrammes.

### <a name="launching-the-calibration-app-from-settings"></a>Lancement de l’application d’étalonnage à partir des paramètres
1. Utilisez l’option démarrer le mouvement pour accéder au [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu).
2. Sélectionnez **toutes les applications** pour afficher toutes les applications si **paramètres** n’est pas épinglé au démarrage.
3. **Paramètres**de lancement.
4. Accédez à étalonnage de l'**œil** de l'**étalonnage** > du **système** > et sélectionnez étalonnage de l' **œil**.

### <a name="calibration-when-sharing-a-devicesession"></a>Étalonnage lors du partage d’un appareil/d’une session

Hololens 2 peut être partagé entre les personnes, sans qu’il soit nécessaire que chaque personne passe par la configuration de l’appareil. Hololens 2 invite l’utilisateur à étalonner des éléments visuels lorsque l’appareil est placé sur l’en-tête si l’utilisateur est nouveau sur l’appareil. Si l’utilisateur a précédemment étalonné des éléments visuels sur l’appareil, l’affichage est ajusté en fonction de la qualité et d’une expérience d’affichage confortable quand l’utilisateur place l’appareil en tête. 


## <a name="hololens-v1"></a>Hololens (v1)

L’étalonnage de votre IPD (distance interpupillary) peut améliorer la qualité de vos visuels.

### <a name="during-setup"></a>Pendant l’installation

![Écran d’alignement de doigt IPD à la deuxième étape](images/ipd-finger-alignment-300px.jpg)<br>

*Écran d’alignement de doigt IPD à la deuxième étape*

Sur HoloLens, vous serez invité à étalonner vos éléments visuels lors de l’installation. Cela permet à l’appareil d’ajuster l’affichage de l’hologramme en fonction de la [distance interpupillary](https://en.wikipedia.org/wiki/Interpupillary_distance) (IPD) de l’utilisateur. Avec une IPD incorrecte, les hologrammes peuvent paraître instables ou à une distance incorrecte.

Une fois que Cortana s’est présente, la première étape d’installation est étalonnage. Il est recommandé d’effectuer l’étape d’étalonnage au cours de la phase d’installation, mais vous pouvez l’ignorer en attendant que Cortana vous invite à indiquer «ignorer» pour continuer.

Les utilisateurs sont invités à aligner leur doigt sur une série de six cibles par œil. Grâce à ce processus, HoloLens définit le IPD correct pour l’utilisateur. Si l’étalonnage doit être mis à jour ou ajusté pour un nouvel utilisateur, il peut être exécuté en dehors de l’installation à l’aide de l’application d’étalonnage.

### <a name="calibration-app"></a>Application d’étalonnage

L’étalonnage peut être effectué à tout moment par le biais de l’application d’étalonnage. L’application d’étalonnage est installée par défaut et est accessible à partir du menu Démarrer ou via l’application paramètres. L’étalonnage est recommandé si vous souhaitez améliorer la qualité de vos visuels ou étalonner des visuels pour un nouvel utilisateur.

**Lancement de l’application à partir du démarrage**
1. Utilisez [fleuri](gestures.md#bloom) pour accéder au [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu).
2. Sélectionnez **+** cette option pour afficher toutes les applications.
3. Lancement de l' **étalonnage**.

![Accès à l’application d’étalonnage à partir de l’interpréteur de commandes](images/calibration-shell.png)

![Application d’étalonnage affichée sous la forme d’un cube actif après son lancement](images/calibration-livecube-200px.png)

**Lancement de l’application à partir des paramètres**
1. Utilisez [fleuri](gestures.md#bloom) pour accéder au [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu).
2. Sélectionnez **+** cette option pour afficher toutes les applications si **paramètres** n’est pas épinglé au démarrage.
3. **Paramètres**de lancement.
4. Accédez à**utilitaires** **système** > et sélectionnez **ouvrir l’étalonnage**.

![Lancement de l’application d’étalonnage à partir de l’application paramètres](images/calibration-settings-500px.jpg)


## <a name="immersive-headsets"></a>Casques immersifs

Pour modifier l’IPD au sein de votre casque, ouvrez l’application paramètres et accédez à l'**affichage du casque** de **réalité** > mixte et déplacez le curseur. Vous verrez les modifications en temps réel dans votre casque. Si vous connaissez votre IPD, peut-être à partir d’une visite sur le Optometrist, vous pouvez également l’entrer directement.

Vous pouvez également ajuster ce paramètre en accédant à **paramètres** > **affichage du casque** de la**réalité** > mixte sur votre PC.

Si votre casque ne prend pas en charge la personnalisation IPD, ce paramètre est désactivé.

## <a name="see-also"></a>Voir aussi
* [Considérations relatives à l’environnement pour HoloLens](environment-considerations-for-hololens.md)
