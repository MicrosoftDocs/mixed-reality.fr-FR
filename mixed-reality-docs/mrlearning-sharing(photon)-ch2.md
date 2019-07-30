# <a name="2-getting-unity-ready-for-development"></a>2. Obtention d’Unity prête pour le développement 


Dans ce didacticiel, nous allons apprendre à préparer et à configurer Unity pour le développement d’applications, notamment l’importation du kit de développement de la réalité mixte, la configuration des paramètres de génération et la préparation de notre scène.

## <a name="objectives"></a>Objectifs

- Configurer Unity pour le développement d’applications

- Importer le Kit de ressources de réalité mixte

- Préparer la scène de votre projet

## <a name="instructions"></a>Instructions

1. Téléchargez et enregistrez le package Unity du kit d’outils de réalité mixte en cliquant [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC2.1/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC2.1.unitypackage)

2. Dans Unity, cliquez sur le menu composants et sélectionnez Importer un package, puis cliquez sur package personnalisé.

![Module3Chapter2step2im](images/module3chapter2step2im.PNG)

3. Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1. Une fois que la fenêtre contextuelle d’importation s’affiche dans Unity, cliquez sur le bouton Importer pour commencer l’importation. L’importation du MRTK peut prendre plusieurs minutes.

![Module3Chapter2step3im](images/module3chapter2step3im.PNG)

> Remarque : Le package téléchargé se trouve dans votre dossier local où vous avez enregistré le fichier. L’image ci-dessus ne décrit pas où se trouve le package.

4. Créez une nouvelle scène. Pour ce faire, cliquez sur fichier, puis sélectionnez nouvelle scène». Enregistrez la scène en tant que HLSharedProjectMain.

> Remarque: vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous. Pour le moment, cliquez sur non.
>
> ![Module3Chapter2note1im](images/module3chapter2note1im.PNG)

5. Dans la boîte à outils de réalité mixte, cliquez sur Ajouter à la scène et configurer.

![Module3Chapter2step5im](images/module3chapter2step5im.PNG)

6. Une fois cette opération terminée, un nouveau fichier de configuration s’affiche, vous donnant la possibilité de personnaliser le profil. Cliquez sur copier et personnaliser.

![Module3Chapter2step6ima](images/module3chapter2step6ima.PNG)

![Module3Chapter2step6imb](images/module3chapter2step6imb.PNG)

![Module3Chapter2step6imc](images/module3chapter2step6imc.PNG)

7. Faites défiler vers le dessous et décochez activer le système de diagnostic si vous souhaitez masquer la fenêtre de diagnostic. Nous vous recommandons de conserver la fenêtre de diagnostic activée pendant le développement d’applications pour surveiller les performances et la désactiver pendant les démonstrations de production ou d’application. 

![Module3Chapter2step7ima](images/module3chapter2step7ima.PNG)

8. Ouvrez les paramètres de build en appuyant sur Ctrl + Maj + B ou en accédant à fichier-> paramètres de Build. Notez que le programme est actuellement défini sous la plateforme autonome PC, Mac et Linux. Pour le développement HoloLens 2, définissez la plateforme sur plateforme Windows universelle. Sélectionnez-le, puis cliquez sur basculer la plateforme.

![Module3Chapter2step8im](images/module3chapter2step8im.PNG)

9. Une fois terminé, cliquez sur la zone qui indique ajouter des scènes ouvertes. Maintenant, accédez au panneau inspecteur et vérifiez que la case à cocher située à droite de Virtual Reality pris en charge (comme indiqué dans l’image ci-dessous) est cochée. Vérifiez également que la case à cocher en regard de scenes/HLSharedProjectMain est également activée comme indiqué dans l’image ci-dessous.

![Module3Chapter2step9im](images/module3chapter2step9im.PNG)

10. Dans la section paramètres de publication du panneau Inspecteur, faites défiler l’écran jusqu’à fonctionnalités, puis vérifiez que les cases à cocher suivantes sont activées:

![Module3Chapter2step9imb](images/module3chapter2step9imb.PNG)

11. Importez le package personnalisé appelé SharingAssetCollection qui peut être téléchargé [ici.](https://github.com/microsoft/MixedRealityLearning/releases/tag/development)

![Module3Chapter2step12im](images/module3chapter2step11im.PNG)

12. Dans le panneau projet, accédez au dossier Prefabs. Dans les étapes suivantes, vous allez implémenter quelques prefabs dans la scène. Dans le dossier Prefabs, cliquez sur la fenêtre de débogage Prefab, puis faites-la glisser dans la hiérarchie. Une fois que vous avez terminé, enregistrez le projet en cliquant sur fichier, puis sur enregistrer ou appuyez sur CTRL + S.

![Module3Chapter2step12im](images/module3chapter2step12im.PNG)

   > Remarque : Vous pouvez remarquer qu’une fenêtre contextuelle s’affiche lorsque vous cliquez sur le Prefab, qui vous demande des informations sur TMP Essentials. Cliquez sur Importer les bases TMP comme vous le souhaitez. Si cette fenêtre contextuelle s’affiche, vous devrez peut-être supprimer le Prefab de votre hiérarchie et le faire glisser à nouveau dans votre hiérarchie pour éviter les erreurs liées au texte potentiel.
   >
>![Module3Chapter2note2im](images/module3chapter2note2im.PNG)


## <a name="congratulations"></a>Félicitations

Votre projet Unity est maintenant prêt pour la photonique. Dans les didacticiels à venir, nous nous appuyons sur cette scène et notre projet Unity vers une expérience partagée complète.

[Didacticiel suivant: 3. Connexion de plusieurs utilisateurs](mrlearning-sharing(photon)-ch3.md)

