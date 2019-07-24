---
title: Exportation et génération d’une solution Unity Visual Studio
description: Cet article décrit l’exportation de votre projet de réalité mixte à partir d’Unity afin que vous puissiez le générer et le déployer dans Visual Studio.
author: ''
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: Unity, Visual Studio, exporter, générer, déployer
ms.openlocfilehash: 68c86fdfe0e589536dafe2bf53c7d4e5dffcc514
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63525839"
---
# <a name="exporting-and-building-a-unity-visual-studio-solution"></a>Exportation et génération d’une solution Unity Visual Studio

Si vous n’envisagez pas d’utiliser le clavier du système dans votre application, nous vous recommandons d’utiliser *D3D* , car votre application utilisera un peu moins de mémoire et une durée de lancement légèrement plus rapide. Si vous utilisez l’API TouchScreenKeyboard dans votre projet pour utiliser le clavier du système, vous devez exporter en tant que *code XAML*.

## <a name="how-to-export-from-unity"></a>Exportation à partir d’Unity

![Paramètres de build Unity](images/unitybuildsettings-300px.png)<br>
*Paramètres de build Unity*

1. Lorsque vous êtes prêt à exporter votre projet à partir d’Unity, ouvrez le menu **fichier** et sélectionnez **paramètres de Build...**
2. Cliquez sur **Ajouter des scènes ouvertes** pour ajouter votre scène à la Build.
3. Dans la boîte de dialogue **paramètres de build** , choisissez les options suivantes à exporter pour HoloLens:
   * **Multi** *Plateforme Windows universelle* et veillez à sélectionner **changer la plateforme** pour que votre sélection prenne effet.
   * **SDK** *Universal 10*.
   * **Type de build UWP:** *D3D*.
4. **Facultatif** : **Projets C# Unity:** Désactivé.

>[!NOTE]
>L’activation de cette case à cocher vous permet d’effectuer les opérations suivantes:
>* Déboguez votre application dans le débogueur distant Visual Studio.
>* Modifiez les scripts dans le C# projet Unity tout en utilisant IntelliSense pour les API WinRT.

5. Dans la fenêtre **paramètres de Build...** , ouvrez paramètres du **lecteur...**
6. Sélectionnez les **paramètres de plateforme Windows universelle** onglet.
7. Développez le groupe de **paramètres XR** .
8. Dans la section **paramètres XR** , cochez la case **Virtual Really Supported** pour ajouter une nouvelle liste d’appareils de **réalité virtuelle** et confirmer **«Windows Mixed Reality»** est répertoriée en tant qu’appareil pris en charge.
9. Revenez à la boîte de dialogue **paramètres de build** .
10. Sélectionnez **Build**.
11. Dans la boîte de dialogue de l’Explorateur Windows qui s’affiche, créez un nouveau dossier pour contenir la sortie de la génération d’Unity. En règle générale, nous nommez le dossier «App».
12. Sélectionnez le dossier nouvellement créé, puis cliquez sur **Sélectionner un dossier**.
13. Une fois la génération de Unity terminée, une fenêtre de l’Explorateur Windows s’ouvre sur le répertoire racine du projet. Accédez au dossier nouvellement créé.
14. Ouvrez le fichier de solution Visual Studio généré situé dans ce dossier.

## <a name="when-to-re-export-from-unity"></a>Moment de la réexportation à partir d’Unity

L’activation deC# la case à cocher «projets» lors de l’exportation de votre application à partir d’Unity crée une solution Visual Studio qui comprend tous vos fichiers de script Unity. Cela vous permet d’effectuer une itération sur vos scripts sans réexportation à partir d’Unity. Toutefois, si vous souhaitez apporter des modifications à votre projet qui ne changent pas le contenu des scripts, vous devrez réexporter à partir d’Unity. Voici quelques exemples de tentatives de réexportation à partir d’Unity:
* Vous ajoutez ou supprimez des ressources dans l’onglet projet.
* Vous pouvez modifier n’importe quelle valeur sous l’onglet Inspector.
* Vous ajoutez ou supprimez des objets dans l’onglet hiérarchie.
* Vous modifiez les paramètres d’un projet Unity

## <a name="building-and-deploying-a-unity-visual-studio-solution"></a>Génération et déploiement d’une solution Unity Visual Studio

Le reste de la génération et du déploiement d’applications s’effectue dans [Visual Studio](using-visual-studio.md). Vous devrez spécifier une configuration de build Unity. Les conventions d’affectation des noms de Unity peuvent différer de ce que vous utilisez habituellement dans Visual Studio:

|  Configuration  |  Explication | 
|----------|----------|
|  Débogage  |  Toutes les optimisations désactivées et le profileur est activé. Utilisé pour déboguer les scripts. | 
|  Maître  |  Toutes les optimisations sont activées et le profileur est désactivé. Utilisé pour soumettre des applications au Windows Store. | 
|  Libérer  |  Toutes les optimisations sont activées et le profileur est activé. Utilisé pour évaluer les performances de l’application. | 

Notez que la liste ci-dessus est un sous-ensemble des déclencheurs courants qui entraînent la génération du projet Visual Studio. En général, la modification des fichiers. cs à partir de Visual Studio ne nécessite pas la régénération du projet à partir d’Unity.

## <a name="troubleshooting"></a>Résolution des problèmes

Si vous constatez que les modifications apportées à vos fichiers. cs ne sont pas reconnues dans votre projet Visual Studio C# , assurez-vous que l’option «projets Unity» est activée lorsque vous générez le projet vs à partir du menu générer de Unity.
