---
title: Entrée vocale
description: Didacticiel sur la configuration et l’utilisation de l’entrée vocale dans HoloLens 2 et le moteur inréel
author: hferrone
ms.author: v-haferr
ms.date: 04/08/2020
ms.topic: article
keywords: Windows Mixed Reality, non réel, moteur 4, UE4, HoloLens 2, voix, entrée vocale, reconnaissance vocale, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, développement de jeux
ms.openlocfilehash: 134a8c5bbeb700a973d3732d24fa9078feb568ef
ms.sourcegitcommit: 7f50210b71a65631fd1bc3fdb215064e0db34333
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84551785"
---
# <a name="voice-input-in-unreal"></a>Entrée vocale en non réel

## <a name="overview"></a>Vue d’ensemble
Les entrées vocales en temps réel vous permettent d’interagir avec un hologramme sans avoir à utiliser des mouvements manuels et n’est pris en charge que pour HoloLens 2. Même si l’entrée vocale sur HoloLens 2 est alimentée par le même moteur qui prend en charge la reconnaissance vocale dans toutes les autres applications Windows universelles, inréel utilise un moteur plus limité qui lui est propre pour traiter l’entrée vocale. Cela limite les fonctionnalités d’entrée vocales dans des mappages de reconnaissance vocale non réels, qui sont traités dans les sections suivantes. 

## <a name="enabling-speech-recognition"></a>Activation de la reconnaissance vocale

Pour activer la reconnaissance vocale sur HoloLens :
1. Sélectionnez **paramètres du projet > plateforme > HoloLens > fonctionnalités** et activer le **microphone**. 
2. Activez la reconnaissance vocale dans **paramètres > confidentialité > voix** et sélectionnez **anglais**.

> [!NOTE]
> La reconnaissance vocale fonctionne toujours dans la langue d’affichage Windows configurée dans l’application **paramètres** . Il est recommandé d’activer également la **reconnaissance vocale en ligne** pour une qualité de service optimale.

![Paramètres de reconnaissance vocale Windows](images/unreal/speech-recognition-settings.png)

3. Une boîte de dialogue s’affiche lorsque l’application commence par vous demander si vous souhaitez activer le microphone. Si vous sélectionnez **Oui** , l’entrée vocale démarre dans l’application.

L’entrée vocale ne nécessite pas d’API Windows Mixed Reality spéciales. Il repose sur l’API existante de mappage [d’entrée](https://docs.unrealengine.com/Gameplay/Input/index.html) de moteur non réel. 

## <a name="adding-speech-mappings"></a>Ajout de mappages vocaux
La connexion vocale à l’action est une étape importante lors de l’utilisation de l’entrée vocale. Ces mappages surveillent l’application pour les mots clés vocaux qu’un utilisateur peut prononcer, puis déclenchent une action liée. Vous pouvez trouver des mappages de reconnaissance vocale en procédant comme suit :
1. Sélectionnez **modifier > paramètres du projet**, faites défiler jusqu’à la section **moteur** , puis cliquez sur **entrée**.

Pour ajouter un nouveau mappage de reconnaissance vocale pour une commande de saut :
1. Cliquez sur l' **+** icône en regard d' **éléments de tableau** et remplissez les valeurs suivantes :
    * **jumpWord** pour le nom de l' **action**
    * **raccourci** pour le **mot clé Speech**

> [!NOTE]
> Vous pouvez utiliser n’importe quel mot ou phrase (s) en anglais comme mot clé. 

![Paramètres d’entrée du moteur UE4](images/unreal/engine-input.png)

Les mappages vocaux peuvent être utilisés en tant que composants d’entrée comme les mappages d’action ou d’axe ou en tant que nœuds de plan dans le graphique d’événements. Par exemple, vous pouvez lier la commande Jump pour imprimer deux journaux différents selon le moment où le mot est parlé :

1. Double-cliquez sur un plan pour l’ouvrir dans le **graphique des événements**.
2. **Cliquez avec le bouton droit** et recherchez le **nom d’action** de votre mappage de reconnaissance vocale (dans le cas présent **jumpWord**), puis appuyez sur **entrée**. Cela ajoute un nœud **d’action d’entrée** au graphique.
3. Faites glisser et déposez le code PIN **appuyé** pour imprimer le nœud de **chaîne** comme indiqué dans l’image ci-dessous. Vous pouvez faire en sorte que le code confidentiel **libéré** soit vide. il n’exécutera rien pour les mappages vocaux.
 
![Action simple pour la voix](images/unreal/voice-input-img-03.png)

4. Lisez l’application, disons le mot **Jump** et regardez la console imprimer les journaux !

C’est tout ce dont vous avez besoin pour commencer à ajouter des entrées vocales à vos applications HoloLens en toute situation. Vous trouverez plus d’informations sur la voix et l’interactivité dans les liens ci-dessous, et veillez à réfléchir à l’expérience que vous créez pour vos utilisateurs.

## <a name="see-also"></a>Voir aussi
* [Entrée vocale](voice-input.md)
* [Pointer et valider](gaze-and-commit.md)
* [Interactions instinctuelles](interaction-fundamentals.md)
* [Réalité mixte - Entrées - Cours 212 : Voix](holograms-212.md)

