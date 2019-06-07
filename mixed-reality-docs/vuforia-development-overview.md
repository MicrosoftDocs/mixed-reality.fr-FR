---
title: À l’aide de Vuforia avec Unity
description: Tirez parti de Vuforia pour créer des applications Windows Mixed Reality dans Unity.
author: ailyadis
ms.author: ''
ms.date: 01/28/2019
ms.topic: article
keywords: Vuforia, marqueurs, les coordonnées, de référence, de suivi
ms.openlocfilehash: c0d2f6d0707e1ddd3ee00d3eb80af9fb459f252b
ms.sourcegitcommit: c2a5bff423feba7d29d5431c870b6017c2fe1bc2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66750352"
---
# <a name="using-vuforia-engine-with-unity"></a>À l’aide du moteur de Vuforia avec Unity

Moteur de Vuforia apporte une fonctionnalité importante pour HoloLens : la puissance pour se connecter AR expériences pour les images spécifiques et des objets dans l’environnement. Vous pouvez utiliser cette fonctionnalité pour superposer des instructions pas à pas guidées par-dessus un mécanisme pour les entreprises industrielles ou ajouter des fonctionnalités numériques et des expériences d’un produit physique ou d’un jeu. 

Pour une plus grande flexibilité lorsque les expériences de développement AR, Vuforia moteur offre un large éventail de fonctionnalités et cibles. Un de nos fonctionnalités les plus récentes, Vuforia modèle cibles, est une fonctionnalité clé pour des utilisations commerciales et industrielles. Cibles de modèle permettent aux applications reconnaître des objets physiques telles que les ordinateurs, les véhicules automobiles ou toys et les suivent selon une CAO ou d’un modèle 3D numérique. Pour des utilisations industrielles, cette fonctionnalité peut fournir des travailleurs de l’assembly et les techniciens de service avec AR de travail des instructions et aide procédurale, tandis que dans la fabrique ou out dans le champ. 

Les applications Vuforia moteur existantes qui ont été créées pour les téléphones et tablettes peuvent facilement être configurées dans Unity s’exécute sur HoloLens. Vous pouvez même utiliser Vuforia moteur à suivre votre nouvelle application HoloLens pour tablettes Windows 10 tels que les 4 Surface Pro et la Surface Book.

## <a name="get-the-tools"></a>Obtenir les outils

[Installez les versions recommandées](install-the-tools.md) de Visual Studio et Unity, puis configurer Unity pour utiliser Visual Studio et l’IDE et du compilateur par défaut. 

Lorsque vous installez Unity, veillez à installer les « Windows Store .NET script principal » ou « Windows Store IL2CPP script principal ». En outre, veillez à sélectionner « Vuforia augmentée réalité Support » pour activer le moteur Vuforia dans Unity.


## <a name="getting-started-with-vuforia-engine"></a>Mise en route du moteur de Vuforia

Étant donné que le moteur de Vuforia est intégré à Unity, les développeurs n’avez pas besoin télécharger ou installer des outils supplémentaires. La version recommandée d’Unity est le flux LTS qui est actuellement au 2017.3 et comprend le moteur de Vuforia 7.0.57. Le meilleur point de départ pour apprendre à utiliser le moteur de Vuforia avec HoloLens est avec la [Vuforia moteur HoloLens exemple](https://assetstore.unity.com/packages/templates/packs/vuforia-hololens-sample-101553) (disponible dans le Store Asset Unity). L’exemple fournit un projet de HoloLens complet, y compris les scènes préconfigurés qui peuvent être déployées sur un HoloLens.

Les coulisses montrent comment utiliser des cibles d’Image Vuforia à reconnaître une image et de lui ajouter avec du contenu numérique dans une expérience de HoloLens. Les développeurs qui utilisent des versions plus récentes de Unity et Vuforia ont accès à des exemples mis à jour qui incluent une scène montrant l’utilisation de modèle cibles sur HoloLens. Vous pouvez facilement remplacer votre propre contenu dans les coulisses pour faire des essais avec la création d’applications HoloLens qui utilisent le moteur de Vuforia.


## <a name="configuring-a-vuforia-app-for-hololens"></a>Configuration d’une application Vuforia pour HoloLens

Développement d’une application de moteur de Vuforia pour HoloLens est fondamentalement le même que le développement d’applications de moteur de Vuforia pour d’autres appareils. Vous pouvez ensuite appliquer les paramètres de build et les configurations décrites dans la section ci-dessous. C’est tout ce qui est nécessaire pour activer le moteur Vuforia fonctionnent avec le mappage spatial HoloLens et positionnels des systèmes de suivi.

## <a name="build-and-run-the-vuforia-engine-sample-for-hololens"></a>Générer et exécuter l’exemple Vuforia moteur pour HoloLens
1.  Téléchargez le [exemple Vuforia moteur pour HoloLens](https://assetstore.unity.com/packages/templates/packs/vuforia-hololens-sample-101553) à partir du Store Asset Unity
2.  Appliquer le [les options de moteur Unity pour l’alimentation et de performances recommandées](performance-recommendations-for-unity.md)
3.  Ajoutez les coulisses de l’exemple à l’arrière-plan dans la Build.
4.  Définir votre plateforme cible de build pour « Plateforme Windows universelle » dans fichier > Paramètres de Build.
5.  Sélectionnez les paramètres de configuration de build plateforme suivants : 
   * Équipement cible = HoloLens
   * Type de build = D3D
   * Kit de développement logiciel = dernière version installée
   * Version de Visual Studio = dernière version installée
   * Générer et exécuter on = ordinateur Local
6.  Définir une valeur unique **Product Name**, dans **paramètres du lecteur**, comme le nom de l’application lors de l’installation sur le HoloLens.
7.  Vérifiez **Vuforia une réalité augmentée** et **pris en charge de réalité virtuelle** dans **paramètres du lecteur > XR paramètres**
8.  Également sous **XR paramètres**, assurez-vous que « Windows Mixed Reality » est ajouté à la **SDK de réalité virtuelle** liste
9.  Vérifiez les fonctionnalités suivantes dans les paramètres du lecteur > Paramètres de publication 
   * InternetClient
   * WebCam
   * SpatialPerception - si vous envisagez d’utiliser l’API d’observateur de Surface
10. Sélectionnez la Build pour générer un projet Visual Studio
11. Générez le fichier exécutable à partir de Visual Studio et installez-le sur votre HoloLens

Remarque: Depuis la version 7.2, l’exemple de moteur Vuforia pour HoloLens inclut une scène d’exemple, y compris des exemples d’utilisation des cibles de modèle

## <a name="the-vuforia-developer-portal"></a>Le portail des développeurs de Vuforia

Les développeurs qui souhaitent pour créer leur propres AR rencontre avec Vuforia moteur et HoloLens doit s’inscrire sur notre portail des développeurs Vuforia à [developer.vuforia.com](https://developer.vuforia.com/). Dans le portail, les développeurs ont accès à la [Vuforia moteur Forums](https://developer.vuforia.com/forum) où ils peuvent participer à des discussions de la Communauté, un [bibliothèque](https://library.vuforia.com/) avec une documentation détaillée sur toutes les fonctionnalités de moteur Vuforia et le [ Gestionnaire de cible Vuforia](https://developer.vuforia.com/target-manager) où les utilisateurs peuvent créer leurs propres cibles personnalisées. Les développeurs peuvent également s’inscrire pour une licence de développeur libre à l’aide du [Vuforia License Manager](https://developer.vuforia.com/license-manager).

## <a name="extended-tracking-with-vuforia"></a>Étendue de suivi avec Vuforia

[Le suivi étendu](https://library.vuforia.com/articles/Training/Extended-Tracking) crée un mappage de l’environnement pour conserver le même quand une cible n’est plus dans la vue de suivi. Il est équivalent Vuforia moteurs pour le mappage spatial effectué par HoloLens. Lorsque vous activez le suivi étendu sur une cible, vous activez la pose de qui ciblent à passer au système de mappage spatial. De cette façon, les cibles peuvent exister dans le moteur de Vuforia et HoloLens systèmes de coordonnées spatiales, bien que pas simultanément.

![Fenêtre Paramètres de Unity](images/vuforia-extendedtracking.png)<br>
*Fenêtre Paramètres de Unity*

**Activer le suivi des étendues du serveur cible**

Moteur de Vuforia transformera automatiquement la pose d’une cible qui utilise le suivi étendu dans le système de coordonnées spatial HoloLens. Cela permet de HoloLens à prendre le relais suivi et à intégrer n’importe quel contenu en décuplant le volume dans le mappage spatial de son environnement de la cible. Ce processus se produit entre Vuforia moteur et la réalité mixte API dans Unity et ne nécessite pas de programmation par le développeur, il est géré automatiquement.

**Voici ce qui se produit...**
1. Cible de Vuforia Tracker reconnaît la cible
2. Cible de suivi est ensuite initialisée
3. La position et la rotation de la cible sont analysés pour fournir une estimation pose robuste pour HoloLens à utiliser
4. Vuforia transforme pose de la cible de l’espace de coordonnées de mappage spatial HoloLens
5. HoloLens adopte le suivi et le dispositif de suivi Vuforia est désactivée

Le développeur peut contrôler ce processus, pour retourner le contrôle à Vuforia, en désactivant l’étendue de suivi sur le TargetBehaviour.

**REMARQUE :** À compter de Vuforia 7.2, étendues de suivi n’est plus activée sur une base par cible. Au lieu de cela, les développeurs peuvent activer sur le dispositif de suivi pour activer des fonctionnalités similaires sur toutes les cibles dans la scène.


## <a name="see-also"></a>Voir aussi
* [Installer les outils](install-the-tools.md)
* [Systèmes de coordonnées](coordinate-systems.md)
* [Mappage spatial](spatial-mapping.md)
* [Appareil photo dans Unity](camera-in-unity.md)
* [Exportation et création de solutions Unity Visual Studio](exporting-and-building-a-unity-visual-studio-solution.md)
* [Documentation de Vuforia : Développement pour Windows 10 dans Unity](https://library.vuforia.com/articles/Solution/Developing-for-Windows-10-in-Unity)
* [Documentation de Vuforia : Comment installer l’extension Vuforia Unity](https://library.vuforia.com/articles/Solution/Installing-the-Unity-Extension)
* [Documentation de Vuforia : Utilisation de l’exemple HoloLens dans Unity](https://library.vuforia.com/articles/Solution/Working-with-the-HoloLens-sample-in-Unity)
* [Documentation de Vuforia : Étendue de suivi dans Vuforia](https://library.vuforia.com/articles/Training/Extended-Tracking)
