---
title: La mise à jour de votre application SteamVR pour la réalité mixte Windows
description: Meilleures pratiques pour la mise à jour de votre application SteamVR pour optimiser la compatibilité avec les casques Windows Mixed Reality.
author: thmignon
ms.author: thmignon
ms.date: 03/21/2018
ms.topic: article
keywords: SteamVR, compatibilité
ms.openlocfilehash: db21651df8e586edf500f0d05def4b1ea5474284
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593367"
---
# <a name="updating-your-steamvr-application-for-windows-mixed-reality"></a>La mise à jour de votre application SteamVR pour la réalité mixte Windows

Nous encourageons les développeurs à tester et optimiser leurs expériences SteamVR pour s’exécuter sur les casques Windows Mixed Reality. Cette documentation traite des améliorations courants, les développeurs peuvent rendre pour vous assurer que leur expérience s’exécute parfaitement sur Windows Mixed Reality.

## <a name="initial-setup-instructions"></a>Instructions d’installation initiale

Pour démarrer le testerez votre jeu ou votre application à la création de réalité mixte Windows que pour le premier suivi notre [guide Mise en route.](http://aka.ms/WindowsMixedRealitySteamVR)

## <a name="controller-models"></a>Modèles de contrôleur
1. Si votre application effectue le rendu des modèles de contrôleur :
    * Utilisez le [modèles de contrôleur de mouvement Windows Mixed Reality](motion-controllers.md#rendering-the-motion-controller-model)
    * IVRRenderModel::GetComponentState d’utilisation pour obtenir local se transforme en composants (par exemple). Pointeur pose)
2. Expériences qui ont une notion de gaucher/droitier doivent obtenir les indicateurs à partir de l’API pour différencier les contrôleurs d’entrée [(par exemple, Unity)](gestures-and-motion-controllers-in-unity.md#unity-buttonaxis-mapping-table)

## <a name="controls"></a>Contrôles

Lors de la conception ou en ajustant la disposition de votre contrôle n’oubliez pas l’ensemble de commandes réservés suivant :
1. En cliquant sur vers le bas le **stick analogique gauche et droite analogique** est réservé pour le **tableau de bord à vapeur**.
2. Le **bouton de Windows** retournera toujours les utilisateurs à Windows Mixed Reality domestique.

Si possible, valeur par défaut pour le curseur de défilement stick basée téléportation pour faire correspondre le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md#getting-around-your-home) téléportation comportement

## <a name="tooltips-and-ui"></a>Info-bulles et interface utilisateur

De nombreux jeux de réalité virtuelle tirer parti des info-bulles du contrôleur de mouvement et des superpositions à enseigner aux utilisateurs les commandes plus importantes pour leur jeu ou votre application. Lors du paramétrage de votre application pour la réalité mixte Windows nous vous recommandons de consulter cette partie de votre expérience s’assurer que les info-bulles mapper vers les modèles de contrôleur de Windows.

En outre s’il existe des points de votre expérience où vous afficher des images des contrôleurs veillez à fournir des images mises à jour à l’aide de contrôleurs de mouvement de réalité mixte de Windows.

## <a name="haptics"></a>HAPTIQUES

Compter les [mettre à jour du 10 avril 2018 Windows](release-notes-april-2018.md), HAPTIQUES sont désormais pris en charge pour des expériences de SteamVR sur Windows Mixed Reality. Si votre application de SteamVR ou votre jeu comprend déjà la prise en charge de HAPTIQUES, il devrait désormais fonctionner (sans aucun travail supplémentaire) avec [contrôleurs de mouvement Windows Mixed Reality](motion-controllers.md).

Contrôleurs de mouvement de réalité mixte Windows utilisent un moteur HAPTIQUES standard, par opposition à linéaires ACTIONNEURS trouvé dans certains autres SteamVR motion contrôleurs, ce qui peuvent entraîner une expérience utilisateur légèrement différente que prévu. Par conséquent, nous vous recommandons de tester et de configurer votre conception HAPTIQUES avec des contrôleurs de mouvement de réalité mixte Windows. Par exemple, les pulsations HAPTIQUES parfois courtes (5 à 10 ms) sont moins visibles sur les contrôleurs de mouvement Windows Mixed Reality. Pour produire une impulsion plus notable, faites des essais avec l’envoi d’une plus longue « click » (40-70ms) pour accorder le moteur plus de temps pour mettre en place avant d’être prié à puissance à nouveau.

## <a name="launching-steamvr-apps-from-windows-mixed-reality-start-menu"></a>Lancement des applications SteamVR à partir du menu Démarrer de réalité mixte Windows

Pour des expériences VR distribués via Steam, nous avons [mis à jour de la réalité mixte Windows pour la version bêta de SteamVR](https://steamcommunity.com/games/719950/announcements/detail/1687045485866139800) , ainsi que la dernière version [Windows Insider](https://insider.windows.com) RS5 vols afin que les titres SteamVR affichent désormais dans le Menu Démarrer de réalité mixte Windows « toutes les applications » liste automatiquement. Avec ces versions des logiciels installées, vos clients peuvent maintenant lancer des titres SteamVR directement à partir de la réalité mixte Windows domestique sans supprimer leurs casques.

## <a name="windows-mixed-reality-logo"></a>Logo de Windows Mixed Reality

Pour afficher la prise en charge de Windows Mixed Reality pour votre titre, accédez au lien « Modifier la Page Store » sur la Page d’accueil de votre application, cliquez sur l’onglet « Informations de base » et faites défiler jusqu'à la « Réalité virtuelle ». Désactivez le « masquer Windows Mixed Reality », puis publiez dans le magasin.

## <a name="bugs-and-feedback"></a>Bogues et commentaires

Vos commentaires sont très utiles lorsqu’il s’agit de l’amélioration de l’expérience SteamVR de réalité mixte Windows. Veuillez envoyer tous les commentaires et les bogues via le [Hub de commentaires Windows](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/filing-feedback). Voici quelques [conseils sur la façon de rendre vos commentaires SteamVR aussi utile que possible](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/using-steamvr-with-windows-mixed-reality#sharing-feedback-on-steamvr).

Si vous avez des questions ou commentaires à partager, vous pouvez également nous contacter sur notre [forum de vapeur](http://steamcommunity.com/app/719950/discussions/).

## <a name="faqs-and-troubleshooting"></a>FAQ et résolution des problèmes

Si vous rencontrez des problèmes d’ordre général la configuration ou de lecture de votre expérience, [Découvrez les étapes de dépannage les plus récentes](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#steamvr).

## <a name="see-also"></a>Voir aussi
* [Installer les outils](install-the-tools.md)
* [Historique de pilote de contrôleur casque et de mouvement](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/mixed-reality-software)
* [Recommandations de compatibilité Windows Mixed Reality minimale PC matérielles](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)
