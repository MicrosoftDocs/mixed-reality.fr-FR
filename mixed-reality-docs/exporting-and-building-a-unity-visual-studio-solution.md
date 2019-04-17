---
title: Exportation et création d’une solution de Unity Visual Studio
description: Cet article décrit l’exportation de votre projet de réalité mixte à partir d’Unity afin de pouvoir générer et déployer dans Visual Studio.
author: ''
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, visual studio, exporter, créer, déployer
ms.openlocfilehash: 68c86fdfe0e589536dafe2bf53c7d4e5dffcc514
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596382"
---
# <a name="exporting-and-building-a-unity-visual-studio-solution"></a>Exportation et création d’une solution de Unity Visual Studio

Si vous n’envisagez pas sur l’utilisation du clavier système dans votre application, nous vous recommandons consiste à utiliser *D3D* comme utiliser légèrement moins de mémoire et ont un temps de lancement légèrement plus rapide de votre application. Si vous utilisez l’API TouchScreenKeyboard dans votre projet pour utiliser le clavier système, vous devez exporter en tant que *XAML*.

## <a name="how-to-export-from-unity"></a>Comment exporter à partir d’Unity

![Paramètres de build Unity](images/unitybuildsettings-300px.png)<br>
*Paramètres de build Unity*

1. Lorsque vous êtes prêt à exporter votre projet Unity, ouvrez le **fichier** menu et sélectionnez **paramètres de Build...**
2. Cliquez sur **ajouter un arrière-plan Open** pour ajouter votre scène à la build.
3. Dans le **paramètres de Build** boîte de dialogue, choisissez les options suivantes pour exporter pour HoloLens :
   * **Plateforme :** *Plateforme Windows universelle* et veillez à sélectionner **plateforme de commutation** pour votre sélection entrent en vigueur.
   * **KIT DE DÉVELOPPEMENT LOGICIEL :** *10 universelle*.
   * **Type de Build UWP :** *D3D*.
4. **Facultatif**: **Unity C# projets :** Vérifié.

>[!NOTE]
>Cochez cette case vous permet de :
>* Déboguer votre application dans le débogueur distant Visual Studio.
>* Modifier des scripts dans Unity C# projet lors de l’utilisation d’IntelliSense pour les APIs WinRT.

5. À partir de la **paramètres de Build...**  fenêtre, ouvrez **paramètres du lecteur...**
6. Sélectionnez le **paramètres pour la plateforme Windows universelle** onglet.
7. Développez le **XR paramètres** groupe.
8. Dans le **XR paramètres** section, vérifiez le **virtuel pris en charge de réalité** case à cocher pour ajouter un nouveau **des appareils de réalité virtuelle** liste et confirmez **mixte Windows » Réalité »** est répertorié comme un appareil pris en charge.
9. Retour à la **paramètres de Build** boîte de dialogue.
10. Sélectionnez **Build**.
11. Dans la boîte de dialogue de l’Explorateur Windows, créez un dossier pour contenir la sortie de la génération d’Unity. En règle générale, nous nommer le dossier « Application ».
12. Sélectionnez le dossier nouvellement créé et cliquez sur **sélectionner le dossier**.
13. Une fois que Unity a terminé la construction, une fenêtre de l’Explorateur Windows s’ouvre sur le répertoire racine du projet. Naviguer dans le dossier nouvellement créé.
14. Ouvrez le fichier de solution Visual Studio généré situé à l’intérieur de ce dossier.

## <a name="when-to-re-export-from-unity"></a>Quand la ré-exportez à partir d’Unity

Vérification de la «C# projets « case à cocher lors de l’exportation de votre application à partir d’Unity crée une solution Visual Studio qui inclut tous vos fichiers de script Unity. Cela vous permet d’itérer sur vos scripts sans ré-exporter à partir d’Unity. Toutefois, si vous souhaitez apporter des modifications à votre projet qui ne sont pas changer simplement le contenu des scripts, vous devez exporter de nouveau à partir d’Unity. Quelques exemples de fois où que vous devez exporter de nouveau à partir d’Unity sont :
* Vous ajoutez ou supprimez des ressources dans l’onglet projet.
* Vous modifier n’importe quelle valeur dans l’onglet inspecteur.
* Vous ajoutez ou supprimez des objets à partir de l’onglet de la hiérarchie.
* Modifier les paramètres de projet Unity

## <a name="building-and-deploying-a-unity-visual-studio-solution"></a>Création et déploiement d’une solution de Unity Visual Studio

Le reste de la création et déploiement d’applications se produit dans [Visual Studio](using-visual-studio.md). Vous devez spécifier une configuration de build Unity. Conventions d’affectation de noms d’Unity peuvent différer de ce que vous êtes généralement habitué dans Visual Studio :

|  Configuration  |  Explication | 
|----------|----------|
|  Déboguer  |  Toutes les optimisations hors tension et le profileur est activé. Utilisé pour déboguer des scripts. | 
|  Maître  |  Toutes les optimisations sont activées et le profileur est désactivé. Permet de proposer des applications dans le Store. | 
|  Release  |  Toutes les optimisations sont activées et le profileur est activé. Utilisé pour évaluer les performances des applications. | 

Notez que la liste ci-dessus est un sous-ensemble des déclencheurs courants qui génère le projet Visual Studio doivent être générés. En règle générale, la modification des fichiers .cs à partir de Visual Studio ne nécessite pas le projet pour être régénéré à partir de Unity.

## <a name="troubleshooting"></a>Résolution des problèmes

Si vous trouvez que les modifications apportées à vos fichiers .cs ne sont pas reconnues dans votre projet Visual Studio, vérifiez que « Unity C# projets » est activée lorsque vous générez le projet Visual Studio à partir du menu de génération d’Unity.
