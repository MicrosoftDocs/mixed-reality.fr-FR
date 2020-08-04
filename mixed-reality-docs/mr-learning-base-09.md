---
title: Tutoriels de démarrage - 9. Utilisation des commandes vocales
description: Ce cours montre comment utiliser Mixed Reality Toolkit (MRTK) pour créer une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: b0b9771d9569d100a354af96a34cd20ef2a3d7c4
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376591"
---
# <a name="9-using-speech-commands"></a>9. Utilisation des commandes vocales

## <a name="overview"></a>Vue d’ensemble

Dans ce tutoriel, vous allez apprendre à créer des commandes vocales et à les contrôler globalement. Vous allez également apprendre à contrôler les commandes vocales locales qui demandent à l’utilisateur de regarder l’objet qui contrôle la commande vocale.

## <a name="objectives"></a>Objectifs

* Apprendre à créer des commandes vocales
* Apprendre à contrôler les commandes vocales globalement et localement

## <a name="ensuring-the-microphone-capability-is-enabled"></a>Vérification de l’activation de la fonctionnalité Microphone

Dans le menu Unity, sélectionnez Mixed Reality Toolkit > Utilities > **Configure Unity Project** pour ouvrir la fenêtre **MRTK Project Configurator** puis, dans la section **UWP Capabilities**, vérifiez que l’option **Enable Microphone Capability** est grisée :

![mr-learning-base](images/mr-learning-base/base-09-section1-step1-1.png)

> [!NOTE]
> La fonctionnalité Microphone doit avoir été activée lors des instructions [Appliquer les paramètres de MRTK Project Configurator](mr-learning-base-02.md#1-apply-the-mrtk-project-configurator-settings) lorsque vous avez configuré le projet Unity au début de cette série de tutoriels. Toutefois, si elle n’est pas activée, veillez à l’activer maintenant.

## <a name="creating-speech-commands"></a>Création de commandes vocales

Dans la fenêtre de hiérarchie, sélectionnez l’objet **MixedRealityToolkit** puis, dans la fenêtre de l’inspecteur, sélectionnez l’onglet MixedRealityToolkit > **Input** et effectuez les étapes suivantes :

* Développez la section **Speech**.
* Clonez le **DefaultMixedRealitySpeechCommandsProfile** et donnez-lui un nom approprié, par exemple _GettingStarted_MixedRealitySpeechCommandsProfile_.
* Vérifiez que **Start Behaviour** (Comportement de démarrage) est défini sur **Auto Start** (Démarrage automatique).

![mr-learning-base](images/mr-learning-base/base-09-section2-step1-1.png)

> [!TIP]
> Pour vous rappeler comment cloner des profils MRTK, vous pouvez consulter les instructions fournies dans [Configuration des profils MRTK](mr-learning-base-03.md).

Dans la section Speech > **Speech Commands**, cliquez à quatre reprises sur le bouton **+ Add a New Speech Command** (Ajouter une commande vocale) pour ajouter quatre nouvelles commandes vocales à la liste des commandes vocales existantes puis, dans le champ **Keyword** (Mot clé), entrez les expressions suivantes :

* Activer l’indicateur
* Activer l’appui pour placement
* Activer le cadre englobant
* Désactiver le cadre englobant

![mr-learning-base](images/mr-learning-base/base-09-section2-step1-2.png)

> [!TIP]
> Si votre ordinateur ne dispose pas d’un microphone, vous pouvez affecter un code-clé aux commandes vocales, ce qui vous permettra de les déclencher lorsque vous appuierez sur la touche correspondante.

## <a name="controlling-speech-commands"></a>Contrôle des commandes vocales

Dans la Project projet, accédez au dossier **Assets** > **MRTK** > **SDK** > **Features** > **UX** > **Prefabs** > **ToolTip** pour localiser les préfabriqués d’info-bulle :

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-1.png)

Dans la fenêtre de hiérarchie, cliquez avec le bouton droit sur une zone vide et sélectionnez **Create Empty** pour ajouter un objet vide à votre scène.

Nommez l’objet **SpeechInputHandler_Global** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** pour ajouter le composant **SpeechInputHandler** et configurez-le comme suit :

* **Décochez** la case **Is Focus Required** afin que l’utilisateur ne soit pas obligé de regarder l’objet avec le composant SpeechInputHandler pour déclencher la commande vocale.
* À partir de la fenêtre Project, affectez le préfabriqué **SpeechConfirmation Tooltip** au champ **Speech Confirmation Tooltip Prefab** (Préfabriqué d’info-bulle de confirmation vocale) afin que ce préfabriqué s’affiche quand une commande vocale est reconnue.

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-2.png)

Sur le composant SpeechInputHandler, cliquez trois fois sur la petite icône **+** pour ajouter trois éléments de mot clé :

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-3.png)

Développez **Element 0** et configurez-le comme suit :

* Dans le champ **Keyword**, entrez **Activer l’indicateur** afin de référencer la commande vocale Activer l’indicateur que vous avez créée dans la section précédente.
* Cliquez sur la petite icône **+** pour ajouter un événement.
* Dans la fenêtre de hiérarchie, affectez l’objet **Indicator** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **GameObject** > **SetActive (bool)** pour définir cette fonction en tant qu’action à exécuter lorsque l’événement est déclenché.
* **Cochez** la case de l’argument.

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-4.png)

Développez **Element 1** et configurez-le comme suit :

* Dans le champ **Keyword**, entrez **Activer le cadre englobant** afin de référencer la commande vocale Activer le cadre englobant que vous avez créée dans la section précédente.
* Cliquez sur la petite icône **+** pour ajouter un événement.
* Dans la fenêtre de hiérarchie, affectez l’objet **RoverExplorer** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **BoundingBox** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
* **Cochez** la case de l’argument.
* Cliquez sur la petite icône **+** pour ajouter un autre événement.
* Dans la fenêtre de hiérarchie, affectez l’objet **RoverExplorer** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **ObjectManipulator** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
* **Cochez** la case de l’argument.

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-5.png)

Développez **Element 2** et configurez-le comme suit :

* Dans le champ **Keyword**, entrez **Désactiver le cadre englobant** afin de référencer la commande vocale Désactiver le cadre englobant que vous avez créée dans la section précédente.
* Cliquez sur la petite icône **+** pour ajouter un événement.
* Dans la fenêtre de hiérarchie, affectez l’objet **RoverExplorer** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **BoundingBox** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
* Vérifiez que la case de l’argument est **décochée**.
* Cliquez sur la petite icône **+** pour ajouter un autre événement.
* Dans la fenêtre de hiérarchie, affectez l’objet **RoverExplorer** au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **ObjectManipulator** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
* Vérifiez que la case de l’argument est **décochée**.

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-6.png)

Dans la fenêtre de hiérarchie, sélectionnez l’objet RoverExplorer > **RoverAssembly** puis, dans la fenêtre de l’inspecteur, utilisez le bouton **Add Component** pour ajouter le composant **SpeechInputHandler** et configurez-le comme suit :

* Vérifiez que la case **Is Focus Required** est **cochée** afin que l’utilisateur ne soit pas obligé de regarder l’objet avec le composant SpeechInputHandler (autrement dit, RoverAssembly) pour déclencher la commande vocale.
* À partir de la fenêtre Project, affectez le préfabriqué **SpeechConfirmation Tooltip** au champ **Speech Confirmation Tooltip Prefab** (Préfabriqué d’info-bulle de confirmation vocale) afin que ce préfabriqué s’affiche quand une commande vocale est reconnue.

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-7.png)

Sur le composant SpeechInputHandler, cliquez sur la petite icône **+** pour ajouter un élément Keyword, développez l’élément qui vient d’être créé, puis configurez-le comme suit :

* Dans le champ **Keyword**, entrez **Activer l’appui pour placement** afin de référencer la commande vocale Activer l’appui pour placement que vous avez créée dans la section précédente.
* Cliquez sur la petite icône **+** pour ajouter un événement.
* Dans la fenêtre de hiérarchie, assignez l’objet lui-même, c’est-à-dire le même objet **RoverAssembly**, au champ **None (Object)** .
* Dans la liste déroulante **No Function**, sélectionnez **TapToPlace** > **bool enabled** pour mettre à jour cette valeur de propriété lorsque l’événement est déclenché.
* **Cochez** la case de l’argument.

![mr-learning-base](images/mr-learning-base/base-09-section3-step1-8.png)

## <a name="congratulations"></a>Félicitations

Dans ce tutoriel, vous avez appris à créer des commandes vocales et à les contrôler globalement. Vous avez également appris à contrôler les commandes vocales locales qui demandent à l’utilisateur de regarder l’objet qui contrôle la commande vocale.

Cela conclut également la série de [Tutoriels de démarrage](mr-learning-base-01.md). En suivant ces tutoriels, vous avez réussi à créer une expérience de réalité mixte complète à l’aide de MRTK.

Dans les deux prochaines séries de tutoriels, [Tutoriels Azure Spatial Anchors](mr-learning-asa-01.md) et [Tutoriels sur les fonctionnalités multiutilisateurs](mr-learning-sharing-01.md), vous allez d’abord apprendre à intégrer Azure Spatial Anchors dans votre projet afin d’ancrer l’expérience Rover Explorer que vous avez créée dans le monde réel. Ensuite, vous apprendrez à ajouter des fonctionnalités multiutilisateurs à votre projet afin de partager des mouvements d’utilisateur et d’objet en temps réel.
