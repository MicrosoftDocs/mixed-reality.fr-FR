---
title: Meilleures pratiques pour l’utilisation d’Unity et de Visual Studio
description: Trucs et astuces pour rationaliser le flux de travail de création d’une application de réalité mixte avec Unity et Visual Studio.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: déployer, Unity, Visual Studio, HoloLens, HoloLens 2, casque immersif
ms.openlocfilehash: b2c345a8cc9bddcbc447531eb5f6cdacc62f2e98
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522314"
---
# <a name="best-practices-for-working-with-unity-and-visual-studio"></a>Meilleures pratiques pour l’utilisation d’Unity et de Visual Studio

Un développeur qui crée une application de réalité mixte avec Unity doit basculer entre Unity et Visual Studio pour générer le package d’application déployé dans HoloLens et/ou un casque immersif. Par défaut, deux instances de Visual Studio sont nécessaires (l’une pour modifier les scripts Unity et l’autre pour le déploiement sur l’appareil et le débogage). La procédure suivante autorise le développement à l’aide d’une seule instance de Visual Studio, réduit la fréquence de l’exportation des projets Unity et améliore l’expérience de débogage.

## <a name="improving-iteration-time"></a>Amélioration de l’heure des itérations

La prise en charge du serveur principal de script .NET dans Unity est dépréciée dans Unity 2018 et supprimée dans Unity 2019 +. Par conséquent, il est recommandé de basculer vers [IL2CPP](https://docs.unity3d.com/Manual/IL2CPP.html). Toutefois, cela peut entraîner des temps de génération plus longs entre Unity et Visual Studio. Pour améliorer l’itération plus rapidement, il est recommandé de configurer son environnement pour optimiser les résultats de la compilation.

1) Tirez parti de la création incrémentielle en générant votre projet dans le même répertoire à chaque fois, en réutilisant les fichiers prédéfinis
2) Désactiver les analyses logicielles anti-programme malveillant pour votre projet & les dossiers de build
   - Ouvrir la **protection contre les menaces contre les Virus &** sous votre application Paramètres Windows 10
   - Sélectionnez **gérer les paramètres** sous **virus & les paramètres de protection contre les menaces**
   - Sélectionnez **Ajouter ou supprimer** des exclusions sous  la section exclusions.
   - Cliquez sur **Ajouter une exclusion** , puis sélectionnez le dossier qui contient le code de votre projet Unity et les sorties de génération
3) Utiliser un SSD pour la génération

Pour plus d’informations, consultez [optimisation des durées de génération pour IL2CPP](https://docs.unity3d.com/Manual/IL2CPP-OptimizingBuildTimes.html) . Consultez également [le débogage sur le serveur principal IL2CPP Scripting](https://docs.unity3d.com/Manual/windowsstore-debugging-il2cpp.html).

En outre, envisagez d’installer l' [extension Visual Studio *UnityScriptAnalyzer* ](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/UnityScriptAnalyzer). Cet outil analyse vos scripts Unity C# pour le code qui peut être écrit de façon plus optimisée.

## <a name="visual-studio-tools-for-unity"></a>Outils Visual Studio pour Unity

Télécharger [outils Visual Studio pour Unity](https://docs.microsoft.com/en-us/visualstudio/cross-platform/getting-started-with-visual-studio-tools-for-unity?view=vs-2019)

**Avantages de Outils Visual Studio pour Unity**
* Déboguez Unity en mode de lecture de l’éditeur à partir de Visual Studio en plaçant des points d’arrêt, en évaluant des variables et des expressions complexes.
* Utilisez l’Explorateur de projets Unity pour rechercher votre script avec exactement la même hiérarchie que celle affichée par Unity.
* Récupérez la console Unity directement à l’intérieur de Visual Studio.
* Utilisez les assistants pour créer rapidement des scripts ou y accéder.

## <a name="expose-c-class-variables-for-easy-tuning"></a>Exposer C# des variables de classe pour faciliter le paramétrage

Il existe deux façons d’exposer des variables de classe. Pour ce faire, la méthode recommandée consiste à ajouter l’attribut [SerializeField] à vos variables privées. Cela leur permet d’y accéder à partir de l’éditeur, mais pas de les exposer par programmation.  L’autre option consiste à rendre C# les variables de classe publiques pour les exposer dans l’interface utilisateur de l’éditeur. 

Les deux approches permettent de modifier facilement les variables tout en lisant dans l’éditeur. Cela s’avère particulièrement utile pour le paramétrage des propriétés de mécanicien d’interaction.

## <a name="regenerate-uwp-visual-studio-solutions-after-windows-sdk-or-unity-upgrade"></a>Régénérer les solutions Visual Studio UWP après une mise à niveau de SDK Windows ou Unity

Les solutions Visual Studio UWP archivées dans le contrôle de code source peuvent être obsolètes après la mise à niveau vers un nouveau SDK Windows ou un moteur Unity. Vous pouvez résoudre ce cas après la mise à niveau en créant une nouvelle solution UWP à partir d’Unity, puis en fusionnant toutes les différences dans la solution archivée.

## <a name="use-text-format-assets-for-easy-comparison-of-content-changes"></a>Utiliser des ressources au format texte pour faciliter la comparaison des modifications de contenu

Le stockage des ressources au format texte facilite l’examen des différences de modification de contenu dans Visual Studio. Vous pouvez l’activer dans «modifier les paramètres du projet > l’éditeur de >» en modifiant le mode de **sérialisation des ressources** pour **forcer le texte**. Toutefois, la fusion de modifications de fichiers de ressources texte est sujette aux erreurs et n’est pas recommandée. envisagez donc d’activer des extractions binaires exclusives dans votre système de contrôle de code source.

## <a name="see-also"></a>Voir aussi
- [Visual Studio Tools pour Unity](https://visualstudiogallery.msdn.microsoft.com/8d26236e-4a64-4d64-8486-7df95156aba9)
- [Optimisation des temps de génération pour IL2CPP](https://docs.unity3d.com/Manual/IL2CPP-OptimizingBuildTimes.html)
- [*UnityScriptAnalyzer* Extension Visual Studio](https://github.com/Microsoft/MixedRealityCompanionKit/tree/master/UnityScriptAnalyzer)