---
title: Didacticiels sur les fonctionnalités multi-utilisateur-2. Obtention d’Unity prête pour le développement
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 2bcec7e70949186c6e711120c36ee8649c006ec7
ms.sourcegitcommit: bd536f4f99c71418b55c121b7ba19ecbaf6336bb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/21/2020
ms.locfileid: "77553833"
---
# <a name="2-getting-unity-ready-for-development"></a>2. obtention d’Unity prête pour le développement

Dans ce didacticiel, vous allez apprendre à préparer et à configurer Unity pour le développement d’applications, notamment l’importation de la boîte à outils de réalité mixte, la configuration des paramètres de génération et la préparation de votre scène.

## <a name="objectives"></a>Objectifs

* Configurer Unity pour le développement d’applications
* Importer le Kit de ressources de réalité mixte
* Préparer la scène de votre projet

## <a name="instructions"></a>Instructions

1. Téléchargez et enregistrez le package d’Unity pour la réalité mixte en cliquant [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.3.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage)

2. Dans Unity, cliquez sur le menu composants, sélectionnez Importer un package, puis cliquez sur package personnalisé.

    ![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1. Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Importer pour commencer l’importation de la MRTK. Cette opération peut prendre plusieurs minutes.

    ![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

    >[!NOTE]
    >Le package téléchargé se trouve dans votre dossier local, où vous avez enregistré le fichier. L’image ci-dessus ne décrit pas où se trouve le package.

    Une fois le package importé, la fenêtre du configurateur de projet MRTK doit s’afficher. Si ce n’est pas le cas, ouvrez-le en sélectionnant Mixed Reality Toolkit > Utilities > configurer le projet Unity dans le menu Unity.

    Dans la fenêtre du Configurateur de projet MRTK, développez la section modifier les configurations, décochez la case Activer MSBuild pour Unity, vérifiez que toutes les autres options sont cochées, puis cliquez sur le bouton appliquer pour appliquer les paramètres.

    ![Module3Chapter2note1im](images/module3chapter2note1im-missing01.png)

    > [!CAUTION]
    > MSBuild for Unity ne prend peut-être pas en charge tous les SDK que vous utiliserez et peut être difficile à désactiver une fois qu’il a été activé. Par conséquent, il est vivement recommandé de ne pas activer MSBuild for Unity.
    
4. Créez une nouvelle scène. Pour ce faire, cliquez sur fichier et sélectionnez nouvelle scène. Enregistrez-le en tant que HLSharedProjectMain.

5. Dans la boîte à outils de réalité mixte, cliquez sur Ajouter à la scène et configurer.

    ![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. Une fois cette opération terminée, sélectionnez la boîte à outils de réalité mixte (MRTK) dans la hiérarchie. Dans le volet de l’inspecteur, remplacez le profil de configuration MRTK par DefaultHoloLens2ConfigurationProfile.

    ![Module2Chapter1step4ima](images/Module2Chapter1step4ima-missing01.png)

7. Sélectionnez la boîte à outils de réalité mixte (MRTK) dans la hiérarchie. Dans le volet de l’inspecteur, recherchez le script Mixed Reality Toolkit, puis appuyez sur le bouton « Copier & Personnaliser », comme indiqué dans la figure ci-dessous.  Une liste déroulante s’affiche après cela et sélectionnez l’option cloner dans le menu contextuel.

    ![Module3Chapter2step6imc](images/module3chapter2step6imc.PNG)

    ![Module3Chapter2step6imd](images/module3chapter2step6imd.PNG)

8. Faites défiler vers le dessous et décochez activer le système de diagnostic si vous souhaitez masquer la fenêtre de diagnostic. Nous vous recommandons de laisser la fenêtre de diagnostics activée pendant le développement d’applications pour surveiller les performances, puis la désactiver pendant les démonstrations de production ou d’application. 

    ![Module3Chapter2step7ima](images/module3chapter2step7ima.PNG)

9. Ouvrez les paramètres de build en appuyant sur Ctrl + Maj + B ou en accédant à fichier-> paramètres de Build. Notez que le programme est actuellement défini sous la plateforme autonome PC, Mac et Linux. Pour le développement HoloLens 2, définissez la plateforme sur plateforme Windows universelle. Sélectionnez-le, puis cliquez sur basculer la plateforme.

    ![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

10. Une fois terminé, cliquez sur la zone intitulée ajouter des scènes ouvertes. Maintenant, accédez au panneau de l’inspecteur et vérifiez que la case à cocher située à droite de la réalité virtuelle prise en charge (comme indiqué dans l’image ci-dessous) est activée. Assurez-vous également que la case à cocher en regard de scenes/HLSharedProjectMain est également activée, comme illustré dans l’image ci-dessous.

    ![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

11. Dans la section paramètres de publication du panneau Inspecteur, faites défiler l’écran jusqu’à fonctionnalités et vérifiez que les cases à cocher suivantes sont activées :

    ![Module3Chapter2step9imb](images/module3chapter2step9imb.PNG)

12. Importez les packages personnalisés listés :

    * [AzureSpatialAnchors. pour Unity](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)
    * [MRTK. HoloLens2. Unity. Tutorials. Assets. GettingStarted. 2.3.0.2. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.2/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage)
    * [MRTK. HoloLens2. Unity. Tutorials. Assets. AzureSpatialAnchors. 2.3.0.0. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.0.unitypackage)
    * [MRTK. HoloLens2. Unity. Tutorials. Assets. MultiUserCapabilities. 2.1.0.1. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/multi-user-capabilities-v2.1.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.1.0.1.unitypackage)

    >[!TIP]
    >Pour obtenir un rappel sur la configuration d’un projet Unity pour les ancres spatiales Azure, vous pouvez consulter le didacticiel [prise en main d’ancres spatiales](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) Azure, qui fait partie de la série de didacticiels sur les [ancres spatiales Azure](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) .


13. Dans le panneau projet, accédez au dossier Prefabs. Dans les étapes suivantes, vous allez implémenter quelques prefabs dans la scène. Dans le dossier Prefabs, cliquez sur la fenêtre de débogage Prefab, puis faites-la glisser dans la hiérarchie. Une fois que vous avez terminé, enregistrez le projet en cliquant sur fichier, puis sur enregistrer ou appuyez sur CTRL + S.

    ![Module3Chapter2step12im](images/module3chapter2step12im.PNG)

    Vous pouvez remarquer qu’une fenêtre contextuelle s’affiche lorsque vous cliquez sur le Prefab, qui vous demande des informations sur TMP Essentials. Cliquez sur Importer les bases TMP comme vous le souhaitez. Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le Prefab de votre hiérarchie et le faire glisser à nouveau dans votre hiérarchie pour éviter les erreurs liées au texte potentiel.

    ![Module3Chapter2note2im](images/module3chapter2note2im.PNG)

## <a name="congratulations"></a>Félicitations

Votre projet Unity est maintenant prêt pour la photonique. Dans les didacticiels à venir, nous nous appuyons sur cette scène et notre projet Unity vers une expérience partagée complète.

[Didacticiel suivant : 3. connexion de plusieurs utilisateurs](mrlearning-sharing(photon)-ch3.md)
