---
title: Didacticiels sur les fonctionnalités multi-utilisateur-2. Obtention d’Unity prête pour le développement
description: Suivez ce cours pour apprendre à implémenter des expériences partagées multi-utilisateur dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 6840bcc583fe3e42dcaa6f42e71098f4dbe76f4c
ms.sourcegitcommit: 23b130d03fea46a50a712b8301fe4e5deed6cf9c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/24/2019
ms.locfileid: "75334309"
---
# <a name="2-getting-unity-ready-for-development"></a>2. obtention d’Unity prête pour le développement

Dans ce didacticiel, vous allez apprendre à préparer et à configurer Unity pour le développement d’applications, notamment l’importation de la boîte à outils de réalité mixte, la configuration des paramètres de génération et la préparation de votre scène.

## <a name="objectives"></a>Objectifs

* Configurer Unity pour le développement d’applications
* Importer le Kit de ressources de réalité mixte
* Préparer la scène de votre projet

## <a name="instructions"></a>Instructions

1. Téléchargez et enregistrez le package d’Unity pour la réalité mixte en cliquant [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.1.0/Microsoft.MixedReality.Toolkit.Unity.Foundation.2.1.0.unitypackage)

2. Dans Unity, cliquez sur le menu composants, sélectionnez Importer un package, puis cliquez sur package personnalisé.

    ![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1. Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Importer pour commencer l’importation de la MRTK. Cette opération peut prendre quelques minutes.

    ![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

    >[!NOTE]
    >Le package téléchargé se trouve dans votre dossier local, où vous avez enregistré le fichier. L’image ci-dessus ne décrit pas où se trouve le package.

4. Créez une nouvelle scène. Pour ce faire, cliquez sur fichier et sélectionnez nouvelle scène. Enregistrez-le en tant que HLSharedProjectMain.

    Vous pouvez recevoir une fenêtre contextuelle ressemblant à l’image ci-dessous. Pour le moment, cliquez sur non.
    ![Module3Chapter2note1im](images/module3chapter2note1im.PNG)

5. Dans la boîte à outils de réalité mixte, cliquez sur Ajouter à la scène et configurer.

    ![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. Une fois cette opération terminée, un nouveau fichier de configuration s’affiche, vous donnant la possibilité de personnaliser le profil.

    ![Module2Chapter1step4ima](images/Module2Chapter1step4ima.PNG)

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

    a. [Unity. HoloLens2. GettingStarted. Tutorials. Asset. 2.1.0.0. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/getting-started-v2.1.0.0/Unity.HoloLens2.GettingStarted.Tutorials.Asset.2.1.0.0.unitypackage)

    b. [Unity. HoloLens2. MultiUserCapabilities. Tutorials. Asset. 2.1.0.0. pour Unity](https://github.com/microsoft/MixedRealityLearning/releases/download/multi-user-capabilities-v2.1.0.0/Unity.HoloLens2.MultiUserCapabilities.Tutorials.Asset.2.1.0.0.unitypackage)

    >[!TIP]
    >Si vous avez terminé les [didacticiels de mise](mrlearning-base-ch1.md)en route, il se peut que le package Unity nommé _Unity. HoloLens2. gettingstarted. tutoriels. Asset. 2.1.0.0. pour Unity_ soit stocké sur votre ordinateur. Si c’est le cas, vous pouvez ignorer le téléchargement de l’élément multimédia indiqué à l’étape a ci-dessus.

    ![Module3Chapter2step12im](images/module3chapter2step11im.PNG)

13. Dans le panneau projet, accédez au dossier Prefabs. Dans les étapes suivantes, vous allez implémenter quelques prefabs dans la scène. Dans le dossier Prefabs, cliquez sur la fenêtre de débogage Prefab, puis faites-la glisser dans la hiérarchie. Une fois que vous avez terminé, enregistrez le projet en cliquant sur fichier, puis sur enregistrer ou appuyez sur CTRL + S.

    ![Module3Chapter2step12im](images/module3chapter2step12im.PNG)

    Vous pouvez remarquer qu’une fenêtre contextuelle s’affiche lorsque vous cliquez sur le Prefab, qui vous demande des informations sur TMP Essentials. Cliquez sur Importer les bases TMP comme vous le souhaitez. Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le Prefab de votre hiérarchie et le faire glisser à nouveau dans votre hiérarchie pour éviter les erreurs liées au texte potentiel.

    ![Module3Chapter2note2im](images/module3chapter2note2im.PNG)

## <a name="congratulations"></a>Félicitations !

Votre projet Unity est maintenant prêt pour la photonique. Dans les didacticiels à venir, nous nous appuyons sur cette scène et notre projet Unity vers une expérience partagée complète.

[Didacticiel suivant : 3. connexion de plusieurs utilisateurs](mrlearning-sharing(photon)-ch3.md)
