---
title: Meilleures pratiques pour travailler avec Unity et Visual Studio
description: Conseils et astuces pour rationaliser le flux de travail de création d’une application de réalité mixte avec Unity et Visual Studio.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: déployer, unity, casque immersives de visual studio, HoloLens,
ms.openlocfilehash: 80a533851b3bee0d747a90dfececbaa558c4ec1f
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596688"
---
# <a name="best-practices-for-working-with-unity-and-visual-studio"></a>Meilleures pratiques pour travailler avec Unity et Visual Studio

Un développeur crée une application de réalité mixte avec Unity devez basculer entre Unity et Visual Studio pour générer le package d’application est déployé sur HoloLens et/ou un casque immersif. Par défaut les deux instances de Visual Studio sont nécessaires (une pour modifier des scripts Unity) et à déployer sur l’appareil et le débogage. La procédure suivante permet de développement à l’aide de la seule instance de Visual Studio, réduit la fréquence d’exportation des projets Unity et améliore l’expérience de débogage.

## <a name="improving-iteration-time"></a>Améliorer le temps de l’itération

Un problème de flux de travail courant lorsque vous travaillez avec Unity et Visual Studio rencontre plusieurs fenêtres de Visual Studio ouvert et de devoir basculer constamment entre Visual Studio et Unity pour effectuer une itération.
1. **Unity** : pour modifier la scène et l’exportation d’une solution Visual Studio
2. **Visual Studio (1)** : pour la modification des scripts
3. **Visual Studio (2)** : pour générer et déployer la Unity exporté solution Visual Studio à l’appareil

Heureusement, il existe un moyen de simplifier à une seule instance de Visual Studio et réduire des exportations fréquentes à partir d’Unity.

Lorsque [exportation de votre projet à partir d’Unity](exporting-and-building-a-unity-visual-studio-solution.md), vérifiez le **Unity C# projets** case à cocher dans le menu « Fichier > Générer paramètres ». À présent, le projet que vous exportez à partir d’Unity inclut toutes les de votre projet C# scripts et présente plusieurs avantages :
* Utiliser la même instance de Visual Studio pour l’écriture de scripts et de génération/déploiement de votre projet
* Exporter à partir d’Unity uniquement lorsque la scène est modifiée dans l’éditeur Unity ; modification du contenu des scripts est possible dans Visual Studio sans une réexportation.

Avec **Unity C# projets** activé, qu’une seule instance de chaque programme besoin d’être ouverte :
1. **Unity** : pour modifier la scène et l’exportation d’une solution Visual Studio
2. **Visual Studio** : pour la modification des scripts, puis générer et déployer la Unity exporté solution Visual Studio à l’appareil

## <a name="visual-studio-tools-for-unity"></a>Visual Studio Tools pour Unity

Télécharger [Visual Studio Tools pour Unity](https://visualstudiogallery.msdn.microsoft.com/8d26236e-4a64-4d64-8486-7df95156aba9)

**Avantages de Visual Studio Tools pour Unity**
* Déboguer le mode de lecture de l’éditeur Unity à partir de Visual Studio en plaçant des points d’arrêt, l’évaluation des variables et des expressions complexes.
* Utilisez l’Explorateur de projets Unity pour rechercher votre script avec la même hiérarchie que Unity affiche.
* Obtenir la console Unity directement à l’intérieur de Visual Studio.
* Utiliser des Assistants pour rapidement créer ou accéder aux scripts.

## <a name="expose-c-class-variables-for-easy-tuning"></a>Exposer C# classe variables pour le paramétrage simple

Il existe deux façons d’exposer les variables de classe. La méthode recommandée pour ce faire consiste à ajouter l’attribut [SerializeField] à vos variables privées. Cela leur permet d’être accessible à partir de l’éditeur mais pas par programmation exposées.  L’autre option consiste à rendre C# public de variables de classe pour les exposer dans l’éditeur de l’interface utilisateur. 

Les deux approches permettent d’adapter facilement les variables lors de la lecture dans éditeur. Cela est particulièrement utile pour le paramétrage des propriétés mécanique interaction.

## <a name="regenerate-uwp-visual-studio-solutions-after-windows-sdk-or-unity-upgrade"></a>Régénérer les solutions UWP Visual Studio après une mise à niveau Windows SDK ou Unity

Solutions UWP Visual Studio archivées pour contrôle de code source peuvent obtenir obsolètes après la mise à niveau vers un nouveau moteur de kit de développement logiciel Windows ou Unity. Vous pouvez résoudre ce problème après la mise à niveau en créer une nouvelle solution UWP à partir d’Unity, puis en fusionnant toutes les différences dans la solution d’archivage.

## <a name="use-text-format-assets-for-easy-comparison-of-content-changes"></a>Utiliser des ressources de format de texte pour faciliter la comparaison des modifications de contenu

Stockage des ressources au format texte rend plus facile passer en revue les différences de modification de contenu dans Visual Studio. Vous pouvez l’activer sur « Modifier > Paramètres > Éditeur du projet » en modifiant **Asset sérialisation** mode à **forcer le texte**. Toutefois, la fusion des modifications des fichiers texte actif est sujette aux erreurs et ne pas recommandé, vous devez donc activer extractions binaire exclusives dans votre système de contrôle de code source.
