---
title: MR Learning partage Module pour HoloLens 2
description: Terminer ce cours pour apprendre à implémenter plusieurs utilisateurs les expériences partagées au sein d’une application de HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 957813d24de95aad52c26b4bd0f0996a60d01358
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67326602"
---
# <a name="getting-unity-ready-for-development"></a>**Préparation de Unity pour le développement** 

Dans cette leçon, nous allez apprendre à préparer et configurer Unity pour le développement d’applications, y compris l’importation de la boîte à outils de réalité mixte, la configuration des paramètres de build et la préparation de notre scène.

Objectifs :

- Configurer Unity pour le développement d’applications

- Importer le Kit de ressources de réalité mixte

- Préparer votre scène du projet

### <a name="instructions"></a>Instructions

1. Téléchargez et enregistrez le package unity Toolkit de réalité mixte en cliquant sur [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC1-Refresh.unitypackage)
2. Dans Unity, cliquez sur le menu de ressources et sélectionnez « Importer un Package », puis cliquez sur « Custom Package ».

![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1. Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Importer pour commencer l’importation. L’importation du MRTK peut prendre plusieurs minutes.

![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

> Remarque: Le package téléchargé sera dans votre dossier local où vous avez enregistré le fichier. L’image ci-dessus ne transmettent pas où vous trouverez le package.

4. Créer une nouvelle scène (cela est possible en cliquant sur « fichier » et en sélectionnant « nouvelle scène »). Enregistrer la scène en tant que « HLSharedProjectMain ».

> Remarque : vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous. Pour l’instant, cliquez simplement sur « non ».
>
> ![Module3Chapter2note1im](images/module3chapter2note1im.PNG)

5. Sous « Toolkit de réalité mixte », cliquez sur « Ajouter à la scène et configurer ».

![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. Une fois cette opération terminée, un nouveau fichier de configuration s’affiche, ce qui vous donne la possibilité de personnaliser le profil. Cliquez sur « Copier et la personnaliser. »

![Module3Chapter2step6im](images/module3chapter2step6im.PNG)

7. Défiler vers le bas et décochez la case « Activer le système de diagnostic » si vous souhaitez masquer la fenêtre diagnostics. Nous recommandons de conserver la fenêtre diagnostics activés pendant le développement de l’application pour surveiller les performances et la désactivation lors des démonstrations de production ou d’application.

![Module3Chapter2step7im](images/module3chapter2step7im.PNG)

8. Ouvrez les paramètres de build en appuyant sur CTRL + MAJ + B ou en accédant au fichier > Paramètres de Build. Notez que le programme est actuellement défini sous la plateforme « PC, Mac et Linux autonome ». Pour le développement HoloLens 2, définissez la plateforme pour être « Plateforme Windows universelle ». Sélectionnez-le et cliquez sur « commutateur plateforme. »

   ![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

   9. Une fois terminé, cliquez sur la zone intitulée « Ajouter des scènes open ». Accédez à présent le panneau Inspecteur et vérifiez que la case à cocher à droite de la « réalité virtuelle pris en charge » (comme indiqué dans l’image ci-dessous) est activée. Vérifiez également que la case à cocher en regard de « arrière-plan/HLSharedProjectMain » est également activée, comme illustré dans l’image ci-dessous.

   ![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

   10. Sous « Paramètres de publication » section dans le panneau d’inspecteur défiler « Fonctionnalités » et vérifiez que les cases à cocher suivantes sont marqués :
    - client Internet
       
       - internet client server
       
       - serveur client de réseau privé
   
       - camera/webcam

       - Microphone
   
   11. Importer le package personnalisé appelé « Lesson2 », qui peut être téléchargé ici. TODO : Fournir un lien vers le pack de ressources.
   
   ![Module3Chapter2step12im](images/module3chapter2step11im.PNG)
   
   12. Désormais, dans le volet de projet, aller sur le dossier « prefabs », étant donné que dans les prochaines étapes, vous allez implémenter quelques prefabs dans la scène. Dans le dossier « prefabs », cliquez et faites glisser le préfabriqué, « DebugWindow » dans la hiérarchie. Une fois que vous avez terminé, enregistrez le projet (cliquez sur fichier, puis enregistrer, ou appuyez sur CTRL + S)
   
       ![Module3Chapter2step12im](images/module3chapter2step12im.PNG)
   
   > Remarque: Vous pouvez remarquer une fenêtre contextuelle s’affichent lorsque vous cliquez sur le préfabriqué, vous demandant sur TMP Essentials. Cliquez sur « Importation TMP Essentials » car ils vous seront utiles. Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le préfabriqué à partir de votre hiérarchie et de nouveau la faire glisser vers votre hiérarchie afin d’éviter les erreurs potentielles liées au texte.
   >
   > ![Module3Chapter2note2im](images/module3chapter2note2im.PNG)


## <a name="congratulations"></a>Félicitations

Votre projet Unity est maintenant prêt pour Photon ! Dans les leçons venir, nous allons créer cette scène et notre projet Unity vers une expérience complète partagée.

[Leçon suivante : Sharing(Photon) leçon 3](mrlearning-sharing(photon)-ch3.md)

