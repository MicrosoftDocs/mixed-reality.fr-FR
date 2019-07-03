# <a name="getting-unity-ready-for-development"></a>Préparation de Unity pour le développement 

Dans ce didacticiel, nous Découvrez comment préparer et configurer Unity pour le développement d’applications, y compris l’importation de la boîte à outils de réalité mixte, la configuration des paramètres de build et la préparation de notre scène.

Objectifs :

- Configurer Unity pour le développement d’applications

- Importer le Kit de ressources de réalité mixte

- Préparer votre scène du projet

### <a name="instructions"></a>Instructions

1. Téléchargez et enregistrez le package unity Toolkit de réalité mixte en cliquant sur [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC2.1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC2.1.unitypackage)
2. Dans Unity, cliquez sur le menu de ressources, puis sélectionnez Importer un Package, cliquez sur le Package personnalisé.

![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1. Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Importer pour commencer l’importation. L’importation du MRTK peut prendre plusieurs minutes.

![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

> Remarque: Le package téléchargé est dans votre dossier local où vous avez enregistré le fichier. L’image ci-dessus ne transmettent pas où vous trouverez le package.

4. Créer une nouvelle scène. Cet exemple est possible en cliquant sur fichier, puis en sélectionnant nouvelle scène »). Enregistrer la scène en tant que HLSharedProjectMain.

> Remarque : vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous. Pour l’instant, cliquez sur non.
>
> ![Module3Chapter2note1im](images/module3chapter2note1im.PNG)

5. Sous boîte à outils de réalité mixte, cliquez sur Ajouter à la scène et les configurer.

![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. Une fois cette opération terminée, un nouveau fichier de configuration s’affiche, ce qui vous donne la possibilité de personnaliser le profil. Cliquez sur Copier et personnaliser.

   ![Module3Chapter2step6ima](images/module3chapter2step6ima.PNG)

   ![Module3Chapter2step6imb](images/module3chapter2step6imb.PNG)

   ![Module3Chapter2step6imc](images/module3chapter2step6imc.PNG)

7. Défiler vers le bas et décochez la case Activer la Siagnostics système si vous souhaitez masquer la fenêtre de diagnostic. Nous recommandons de conserver la fenêtre diagnostics activés pendant le développement de l’application pour surveiller les performances et la désactivation lors des démonstrations de production ou d’application. 

   ![Module3Chapter2step7ima](images/module3chapter2step7ima.PNG)

8. Ouvrez les paramètres de build en appuyant sur CTRL + MAJ + B ou en accédant au fichier -> Paramètres de Build. Notez que le programme est actuellement défini sous la plateforme autonome PC, Mac et Linux. Pour le développement HoloLens 2, définissez la plateforme soit la plateforme Windows universelle. Sélectionnez-le et cliquez sur la plateforme de commutation.![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

9. Une fois terminé, cliquez sur la zone intitulée Ajouter un arrière-plan ouverte. Maintenant passer à la fenêtre d’inspecteur et vérifiez que la case à cocher à droite de virtuel pris en charge de réalité (comme indiqué dans l’image ci-dessous) est cochée. Assurez-vous également que la case à cocher en regard de l’arrière-plan/HLSharedProjectMain est cochée également de comme indiqué dans l’image ci-dessous.![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

10. Dans la section Paramètres de publication dans le panneau d’inspecteur, faites défiler jusqu'à fonctionnalités et vérifiez que les cases à cocher suivantes sont marquées :![Module3Chapter2step9imb](images/module3chapter2step9imb.PNG)

11. Importer le package personnalisé appelé SharingAssetCollection qui peut être téléchargée [ici.](https://github.com/microsoft/MixedRealityLearning/releases/download/Sharing_2/SharingAssetCollection.unitypackage) ![Module3Chapter2step12im](images/module3chapter2step11im.PNG)

12. Dans le volet de projet, accédez au dossier Prefabs. Dans les prochaines étapes vous implémenter quelques prefabs dans la scène. Dans le dossier Prefabs, cliquez et faites glisser le préfabriqué, DebugWindow dans la hiérarchie. Une fois que vous avez terminé, enregistrez le projet en clckin fichier, puis enregistrer ou appuyez sur CTRL + + S.

    ![Module3Chapter2step12im](images/module3chapter2step12im.PNG)

   > Remarque: Vous pouvez remarquer une fenêtre contextuelle s’affichent lorsque vous cliquez sur le préfabriqué, vous demandant sur TMP Essentials. Cliquez sur Importer TMP Essentials car ils sont nécessaires. Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le préfabriqué à partir de votre hiérarchie et de nouveau la faire glisser vers votre hiérarchie afin d’éviter les erreurs potentielles liées au texte.
   >
   > ![Module3Chapter2note2im](images/module3chapter2note2im.PNG)


## <a name="congratulations"></a>Félicitations

Votre projet Unity est maintenant prêt pour Photon. Dans les didacticiels venir, nous allons créer cette scène et notre projet Unity vers une expérience complète partagée.

[Didacticiel suivant : Plusieurs utilisateurs qui se connectent](mrlearning-sharing(photon)-ch3.md)

