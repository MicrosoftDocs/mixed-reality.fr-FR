---
title: Notes de publication-mai 2020
description: Notes de publication de Windows Mixed Reality pour Windows 10 mai 2020 Update (également appelé 2004).
author: tmlyon
ms.author: tmlyon
ms.date: 05/27/2020
ms.topic: article
keywords: Notes de publication, version, Windows 10, Build, 20H1, se, 2020, 2004 mai
ms.openlocfilehash: ec92259662109001c02cf631eb6b9948d61ba9de
ms.sourcegitcommit: b0d15083ec1095e08c9d776e5bae66b4449383bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2020
ms.locfileid: "84124136"
---
# <a name="release-notes---may-2020"></a>Notes de publication-mai 2020

La **mise à jour Windows 10 mai 2020 (V2004)** comprend de nouvelles fonctionnalités pour les casques de Windows Mixed Reality (VR), telles que la possibilité de lancer des applications Win32 dans la réalité mixte. HoloLens (1re génération) est dans le service à long terme (LTS), avec des mises à jour de maintenance à publier chaque mois.

Pour effectuer une mise à jour vers la dernière version sur PC pour les casques de Windows Mixed Realing (VR), ouvrez l’application **paramètres** , accédez à **mettre à jour & sécurité**, puis sélectionnez le bouton **Rechercher les mises à jour** . Sur un PC Windows 10, vous pouvez également installer manuellement la **mise à jour de Windows 10 2020** à l’aide de l' [outil de création de médias Windows](https://www.microsoft.com/software-download/windows10).

**Dernière version pour ordinateur de bureau**: Windows 10 V2004 (10.0.19041.264)

## <a name="updates-for-windows-mixed-reality-immersive-headsets"></a>Mises à jour pour les casques immersif Windows Mixed Reality

### <a name="introducing-the-new-microsoft-edge"></a>Présentation du nouveau Microsoft Edge
Comme [annoncé précédemment](https://docs.microsoft.com/windows/mixed-reality/new-microsoft-edge), nous avons apporté des mises à jour pour une meilleure prise en charge de l’utilisation du nouveau navigateur Microsoft Edge dans Windows Mixed Reality. Le nouveau Microsoft Edge adopte le projet open source de chrome pour créer une meilleure compatibilité Web pour les clients et moins de fragmentation du Web pour tous les développeurs Web. Il prend également en charge WebXR, la nouvelle norme pour créer des expériences Web immersifs pour les casques VR, à la place de WebVR.

### <a name="improved-settings-for-wmr"></a>Paramètres améliorés pour WMR
Grâce à vos commentaires, nous avons ajouté et clarifié les paramètres sur la page d’affichage du casque :

* **Qualité visuelle de mon domicile** -la modification de ces paramètres affecte uniquement l’environnement d’hébergement de la réalité mixte (maison et Skyloft de la falaise) :

* **Ajuster le niveau de détail et la qualité des effets dans la vie de la réalité mixte** : cela modifie certains des effets de rendu que nous utilisons dans la page d’hébergement. En particulier, la qualité visuelle des différents matériaux (bois, béton, etc.) sera mise à l’échelle à mesure que vous modifiez ce paramètre de faible à élevé.

* **Modifier la résolution** de la fenêtre d’application : par défaut, la plupart des fenêtres 2D lancées à la page d’hébergement sont lancées avec une résolution 720p. Si vous pouvez les redimensionner manuellement horizontalement & verticalement, vous pouvez également choisir de les lancer tous sur 1080p à la place. Précédemment, cette option était disponible en tant qu’option très élevée (bêta) sous qualité visuelle. Nous l’avons correctement scindée en tant que paramètre distinct maintenant.

* **Options d’expérience** : ces options permettent d’ajuster l’expérience de la réalité mixte afin de réduire la charge sur les systèmes où le matériel peut éprouver des difficultés à respecter une 90 d’images à une fréquence illimitée. Vous pouvez choisir d’activer ou de désactiver explicitement ces paramètres supplémentaires, ou de choisir laisser Windows décider et laisser nos heuristiques décider quand les activer ou les désactiver.

* **Résolution** : Si vous avez un casque haute résolution tel que le réverbe HP, nous prenons en charge son exécution à sa résolution native ou à une résolution réduite pour des raisons de performances. Les casques antérieurs, tels que Samsung Odyssey et Odyssey +, ne prennent en charge qu’une seule résolution. vous ne pourrez donc pas modifier ce paramètre sur ces casques.

* **Fréquence d’images** : vous pouvez maintenant définir manuellement la fréquence d’images de l’affichage du casque, ou continuer à laisser Windows utiliser ses heuristiques pour déterminer si 60 hz ou 90 Hz est plus approprié.

* **Étalonnage** : comme précédemment, vous pouvez ajuster votre IPD (distance interpupillary) si elle est prise en charge par votre casque.

* **Basculement d’entrée** : basculez le comportement de basculement du focus d’entrée (Win + Y) pour qu’il soit automatique (en fonction des commentaires du capteur de présence) ou manuel.

### <a name="new-cortana-app"></a>Nouvelle application Cortana
Cette mise à jour de Windows comprend la version la plus récente de l’application Cortana, qui est actuellement en anglais uniquement et qui ne prend plus en charge certaines commandes spécifiques à la réalité mixte comme « prendre une photo » et « prendre une vidéo ». Vous serez toujours en mesure d’utiliser le nouveau Cortana pour lancer des applications. de plus, il prend en charge de nouvelles commandes axées sur la productivité, telles que « quand est-ce que la prochaine réunion ? ». ou « envoyez un e-mail à <name> ce que je suis en retard ».

#### <a name="please-help-us-improve"></a>Aidez-nous à améliorer !
Nous cherchons continuellement à améliorer la compatibilité.  Si vous constatez que votre application Win32 classique favorite ne se comporte pas correctement dans Windows Mixed Reality, envoyez vos commentaires via notre [Hub de commentaires](https://support.microsoft.com//help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub).

## <a name="prior-release-notes"></a>Notes de publication antérieures

* [Notes de publication-mai 2019](release-notes-may-2019.md)
* [Notes de publication - Octobre 2018](release-notes-october-2018.md)
* [Notes de publication-2018 avril](release-notes-april-2018.md)
* [Notes de publication - Octobre 2017](release-notes-october-2017.md)
* [Notes de publication - Août 2016](release-notes-august-2016.md)
* [Notes de publication - Mai 2016](release-notes-may-2016.md)
* [Notes de publication - Mars 2016](release-notes-march-2016.md)

## <a name="see-also"></a>Voir aussi
* [Prise en charge des casques immersifs (lien externe)](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality)
* [Prise en charge de HoloLens (lien externe)](https://support.microsoft.com/products/hololens)
* [Installer les outils](install-the-tools.md)
* [Faites-nous part de vos commentaires](give-us-feedback.md)
