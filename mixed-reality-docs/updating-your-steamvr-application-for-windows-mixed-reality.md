---
title: Mise à jour de votre application SteamVR
description: Bonnes pratiques pour la mise à jour de votre application SteamVR afin d’optimiser la compatibilité avec les casques de Windows Mixed Reality.
author: thmignon
ms.author: thmignon
ms.date: 03/21/2018
ms.topic: article
keywords: SteamVR, compatibilité
ms.openlocfilehash: 6479130b14b8b50828ebecd3a648fd8a425aec15
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438202"
---
# <a name="updating-your-steamvr-application"></a>Mise à jour de votre application SteamVR
Nous encourageons les développeurs à tester et à optimiser leurs expériences SteamVR pour qu’elles s’exécutent sur des casques Windows de réalité mixte. Cette documentation couvre les améliorations courantes que les développeurs peuvent apporter pour s’assurer que leur expérience s’exécute parfaitement sur Windows Mixed Reality.

## <a name="initial-setup-instructions"></a>Instructions d’installation initiales

Pour commencer à tester votre jeu ou votre application sur Windows Mixed Reality, veillez à suivre tout d’abord notre [Guide de prise](https://aka.ms/WindowsMixedRealitySteamVR) en main.

## <a name="controller-models"></a>Modèles de contrôleur
1. Si votre application restitue des modèles de contrôleur :
    * Utiliser les [modèles de contrôleur de mouvement Windows Mixed Reality](motion-controllers.md#rendering-the-motion-controller-model)
    * Utilisez IVRRenderModel :: GetComponentState pour accéder aux transformations locales des composants (par exemple, Pose du pointeur)
2. Les expériences qui ont une notion de droitier doivent obtenir des indications des API d’entrée aux contrôleurs de différenciation [(exemple Unity)](gestures-and-motion-controllers-in-unity.md#unity-buttonaxis-mapping-table)

## <a name="controls"></a>Contrôles

Lorsque vous concevez ou ajustez la disposition de votre contrôle, gardez à l’esprit l’ensemble suivant de commandes réservées :
1. Cliquer sur le **bouton gauche et le stick analogique droit** est réservé au **tableau de bord**de la vapeur.
2. Le **bouton Windows** renvoie toujours les utilisateurs vers la page d’hébergement Windows Mixed Reality.

Si possible, par défaut, la télélocalisation basée sur un bâton de pouce est conforme au comportement de téléportage de la [page d’hébergement Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md#getting-around-your-home)

## <a name="tooltips-and-ui"></a>Info-bulles et interface utilisateur

De nombreux jeux VR tirent parti des info-bulles et des superpositions des contrôleurs motion pour enseigner aux utilisateurs les commandes les plus importantes pour leur jeu ou application. Lorsque vous paramétrez votre application pour Windows Mixed Reality, nous vous recommandons de consulter cette partie de votre expérience pour vous assurer que les info-bulles sont mappées aux modèles de contrôleur Windows.

En outre, si vous avez des points dans votre expérience où vous affichez des images des contrôleurs, veillez à fournir des images mises à jour à l’aide des contrôleurs de mouvement Windows Mixed Reality.

## <a name="haptics"></a>Haptique

À compter de la [mise à jour 2018 de Windows 10 avril](release-notes-april-2018.md), les interfaces tactiles sont désormais prises en charge pour les expériences SteamVR sur Windows Mixed Reality. Si votre application ou jeu SteamVR prend déjà en charge les haptique, elle doit maintenant fonctionner (sans travail supplémentaire) avec les [contrôleurs de mouvement Windows Mixed Reality](motion-controllers.md).

Les contrôleurs de mouvement Windows Mixed Reality utilisent un moteur haptique standard, par opposition aux actionneurs linéaires présents dans d’autres contrôleurs de mouvement SteamVR, ce qui peut entraîner une expérience utilisateur légèrement différente de celle attendue. Nous vous recommandons donc de tester et de paramétrer votre conception haptique avec les contrôleurs de mouvement Windows Mixed Reality. Par exemple, parfois des impulsions tactiles courtes (5-10 ms) sont moins perceptibles sur les contrôleurs de mouvement Windows Mixed Reality. Pour générer une impulsion plus perceptible, expérimentez l’envoi d’un « clic » plus long (40-70ms) pour donner au moteur plus de temps pour s’arrêter avant d’être informé de nouveau.

## <a name="launching-steamvr-apps-from-windows-mixed-reality-start-menu"></a>Lancement des applications SteamVR à partir du menu Démarrer de Windows Mixed Reality

Pour les expériences de VR distribuées par vapeur, nous avons [mis à jour la version bêta de Windows Mixed Reality for SteamVR](https://steamcommunity.com/games/719950/announcements/detail/1687045485866139800) avec les derniers vols de [Windows Insider](https://insider.windows.com) RS5, de sorte que les titres de SteamVR s’affichent désormais dans le menu Démarrer de la réalité mixte de Windows dans le menu « toutes les applications » Répertorier automatiquement. Lorsque ces versions logicielles sont installées, vos clients peuvent désormais lancer des titres SteamVR directement à partir de la page d’hébergement de la réalité Windows Mixed sans supprimer leurs casques.

## <a name="windows-mixed-reality-logo"></a>Logo Windows Mixed Reality

Pour afficher la prise en charge de Windows Mixed Reality pour votre titre, accédez au lien « modifier la page du magasin » sur la page d’accueil de votre application, cliquez sur l’onglet « informations de base », puis faites défiler jusqu’à « réalité virtuelle ». Décochez la case « masquer la réalité mixte Windows », puis publiez-la dans le Windows Store.

## <a name="bugs-and-feedback"></a>Bogues et commentaires

Vos commentaires sont précieux lorsqu’il s’agit d’améliorer l’expérience SteamVR Windows Mixed Reality. Envoyez tous les commentaires et bogues via le [Hub de commentaires Windows](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/filing-feedback). Voici quelques [conseils sur la façon de rendre vos commentaires SteamVR aussi utiles que possible](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/using-steamvr-with-windows-mixed-reality#sharing-feedback-on-steamvr).

Si vous avez des questions ou des commentaires à partager, vous pouvez également nous contacter sur notre [Forum de vapeur](https://steamcommunity.com/app/719950/discussions/).

## <a name="faqs-and-troubleshooting"></a>FAQ et résolution des problèmes

Si vous rencontrez des problèmes généraux lors de la configuration ou de la diffusion de votre expérience, [consultez les dernières étapes de dépannage](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/troubleshooting-windows-mixed-reality#steamvr).

## <a name="see-also"></a>Articles associés
* [Installer les outils](install-the-tools.md)
* [Historique du pilote du contrôleur de mouvement et du casque](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/mixed-reality-software)
* [Instructions de compatibilité matérielle PC minimale pour Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)
