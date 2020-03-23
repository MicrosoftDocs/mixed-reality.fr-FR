---
title: Tutoriels sur les fonctionnalités multi-utilisateurs - 2. Préparation de Unity pour le développement
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateurs dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.localizationpriority: high
ms.openlocfilehash: f7ae77d6978b5da860d890bcfe5b6f7c3d4640c8
ms.sourcegitcommit: 5b2ba01aa2e4a80a3333bfdc850ab213a1b523b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79031237"
---
# <a name="2-getting-unity-ready-for-development"></a>2. Préparation de Unity pour le développement

Dans ce tutoriel, vous allez apprendre à préparer et à configurer Unity pour le développement d’applications, notamment à importer Mixed Reality Toolkit, à configurer des paramètres de génération et à préparer votre scène.

## <a name="objectives"></a>Objectifs

* Configurer Unity pour le développement d’applications
* Importer le Kit de ressources de réalité mixte
* Préparer la scène de votre projet

## <a name="instructions"></a>Instructions

1. Téléchargez et enregistrez le package Unity Mixed Reality Toolkit Foundation en cliquant [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.3.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.3.0.unitypackage)

2. Dans Unity, cliquez sur le menu Assets, sélectionnez Import Package, puis cliquez sur Custom Package.

    ![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1. Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Import pour commencer l’importation de MRTK. Cette opération peut prendre plusieurs minutes.

    ![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

    >[!NOTE]
    >Le package téléchargé se trouve dans votre dossier local, où vous avez enregistré le fichier. L’image ci-dessus ne reflète pas l’emplacement auquel vous allez trouver le package.

    Une fois le package importé, la fenêtre du configurateur de projet MRTK doit s’afficher. Si ce n’est pas le cas, ouvrez-la en sélectionnant Mixed Reality Toolkit > Utilities > Configure Unity Project dans le menu Unity.

    Dans la fenêtre MRTK Project Configurator, développez la section Modify Configurations, décochez la case Enable MSBuild for Unity, vérifiez que toutes les autres options sont cochées et cliquez sur le bouton Apply pour appliquer les paramètres.

    ![Module3Chapter2note1im](images/module3chapter2note1im-missing01.png)

    > [!CAUTION]
    > MSBuild for Unity ne prend peut-être pas en charge tous les SDK que vous utiliserez et peut être difficile à désactiver une fois qu’il a été activé. Par conséquent, il est vivement recommandé de ne pas activer MSBuild for Unity.
    
4. Créez une scène. Pour cela, cliquez sur File et sélectionnez New scene. Enregistrez-la sous HLSharedProjectMain.

5. Sous Mixed Reality Toolkit, cliquez sur Add to Scene and Configure.

    ![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. Une fois cette opération terminée, sélectionnez Mixed-Reality Toolkit (MRTK) dans la hiérarchie. Dans le panneau de l’inspecteur, remplacez le profil de configuration MRTK par DefaultHoloLens2ConfigurationProfile.

    ![Module2Chapter1step4ima](images/Module2Chapter1step4ima-missing01.png)

7. Sélectionnez Mixed-Reality Toolkit (MRTK) dans la hiérarchie. Dans le panneau de l’inspecteur, recherchez « Mixed Reality Toolkit Script » et appuyez sur le bouton « Copy & Customize », comme illustré dans la figure ci-dessous.  Une fenêtre s’affiche ensuite. Sélectionnez l’option Clone.

    ![Module3Chapter2step6imc](images/module3chapter2step6imc.PNG)

    ![Module3Chapter2step6imd](images/module3chapter2step6imd.PNG)

8. Faites défiler l’écran pour décocher Enable Diagnostics System si vous voulez masquer la fenêtre de diagnostic. Nous vous recommandons de laisser la fenêtre de diagnostic activée pendant le développement d’applications pour superviser les performances, puis de la désactiver pendant les démonstrations de production ou d’application. 

    ![Module3Chapter2step7ima](images/module3chapter2step7ima.PNG)

9. Ouvrez les paramètres de build en appuyant sur Ctrl+Maj+B ou en accédant à File->Build Settings. Notez que le programme est actuellement défini sous la plateforme autonome PC, Mac et Linux. Pour le développement HoloLens 2, choisissez la plateforme Windows universelle. Sélectionnez-la, puis cliquez sur Switch Platform.

    ![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

10. Quand vous avez terminé, cliquez sur la zone nommée Add Open Scenes. Maintenant, accédez au panneau Inspector pour vérifier que la case située à droite de Virtual Reality Supported (comme illustré dans l’image ci-dessous) est cochée. Vérifiez aussi que la case en regard de scenes/HLSharedProjectMain est aussi cochée, comme illustré dans l’image ci-dessous.

    ![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

11. Dans la section Publishing Settings du panneau Inspector, faites défiler l’écran jusqu’à Capabilities pour vérifier que les cases suivantes sont cochées :

    ![Module3Chapter2step9imb](images/module3chapter2step9imb.PNG)

12. Importez les packages personnalisés listés :

    * [AzureSpatialAnchors.unitypackage](https://github.com/Azure/azure-spatial-anchors-samples/releases/download/v2.1.1/AzureSpatialAnchors.unitypackage) (version 2.1.1)
    * [MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.3.0.2/MRTK.HoloLens2.Unity.Tutorials.Assets.GettingStarted.2.3.0.2.unitypackage)
    * [MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.0.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/azure-spatial-anchors-v2.3.0.0/MRTK.HoloLens2.Unity.Tutorials.Assets.AzureSpatialAnchors.2.3.0.0.unitypackage)
    * [MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.1.0.1.unitypackage](https://github.com/microsoft/MixedRealityLearning/releases/download/multi-user-capabilities-v2.1.0.1/MRTK.HoloLens2.Unity.Tutorials.Assets.MultiUserCapabilities.2.1.0.1.unitypackage)

    >[!TIP]
    >Pour obtenir un rappel sur la façon de configurer un projet Unity pour Azure Spatial Anchors, vous pouvez vous reporter au tutoriel [Bien démarrer avec Azure Spatial Anchors](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1) qui fait partie de la série de tutoriels sur [Azure Spatial Anchors](https://docs.microsoft.com/windows/mixed-reality/mrlearning-asa-ch1).


13. Dans le panneau Project, accédez au dossier Prefabs. Dans les étapes suivantes, vous allez implémenter quelques préfabriqués dans la scène. Dans le dossier Prefabs, cliquez sur le préfabriqué Debug Window pour le faire glisser dans la hiérarchie. Quand vous avez terminé, enregistrez le projet en cliquant sur File, puis sur Save ou en appuyant sur Ctrl+S.

    ![Module3Chapter2step12im](images/module3chapter2step12im.PNG)

    Vous remarquerez peu-être qu’une fenêtre contextuelle s’affiche quand vous cliquez sur le préfabriqué, pour vous donner des informations sur TMP Essentials. Cliquez sur Import TMP Essentials car cela est nécessaire. Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le préfabriqué de votre hiérarchie et le faire glisser à nouveau dans votre hiérarchie pour éviter d’éventuelles erreurs liées au texte.

    ![Module3Chapter2note2im](images/module3chapter2note2im.PNG)

## <a name="congratulations"></a>Félicitations

Votre projet Unity est maintenant prêt pour Photon. Dans les tutoriels à venir, nous allons nous appuyer sur cette scène pour faire de notre projet Unity une expérience partagée complète.

[Tutoriel suivant : 3. Connexion de plusieurs utilisateurs](mrlearning-sharing(photon)-ch3.md)
