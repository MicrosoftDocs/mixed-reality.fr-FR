# <a name="speech-sdk-learning-module"></a>Module d’apprentissage de kit de développement logiciel de reconnaissance vocale

Dans ce didacticiel, vous allez créer une application de réalité mixte qui explore l’utilisation d’Azure Cognitive Services Speech SDK avec la version 2 HoloLens. Lorsque vous avez terminé avec cette série de didacticiels, vous serez en mesure d’utiliser le microphone de votre appareil à transcrire reconnaissance vocale en temps réel, transcrivez dans d’autres langues et tirer parti de fonctionnalité d’intention du Speech SDK pour comprendre les commandes vocales à l’aide de intelligence artificielle.

Objectifs :

- Découvrez comment intégrer le Kit de développement vocale dans une application de HoloLens 2
- Découvrez comment utiliser les commandes vocales
- Découvrez comment utiliser les fonctionnalités de la parole-texte

## <a name="instructions"></a>Instructions

### <a name="getting-started"></a>Prise en main

1. Démarrer Unity et créer un nouveau projet. Entrez le nom du projet « Module de formation Speech SDK ». Choisissez un emplacement pour l’emplacement où enregistrer votre projet. Puis cliquez sur « Créer un projet ».

![Module2Chapter3step1im](images/module4chapter1step1im.PNG)

> Remarque: Assurez-vous que le modèle est défini sur « 3D », comme illustré dans l’image ci-dessus.

2. Téléchargez le [Toolkit de réalité mixte](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC2/Microsoft.MixedReality.Toolkit.Unity.Foundation-v2.0.0-RC2.unitypackage) Unity empaqueter et enregistrez-la dans un dossier sur votre PC. Importer le package dans votre projet Unity. Pour obtenir des instructions détaillées sur la façon de procéder, consultez [leçon de module de base 1](mrlearning-base-ch1.md). 

3. Téléchargez et importez le Azure [Speech SDK](https://aka.ms/csspeech/unitypackage) pour le package de ressource Unity. Importer le package de Speech SDK en cliquant sur « ressources », en sélectionnant « package d’importation », puis en sélectionnant « package personnalisé ». Rechercher le package de Speech SDK téléchargé précédemment et l’ouvrir pour commencer le processus d’importation. 

![Module4Chapter1step3im](images/module4chapter1step3im.PNG)

4. Dans la fenêtre contextuelle suivante, cliquez sur « Importer » pour commencer l’importation du package de Speech SDK. Vérifiez tous les éléments sont activés, comme illustré dans l’image ci-dessous.

![Module4Chapter1step4im](images/module4chapter1step4im.PNG)


5. Téléchargez le [Lunarcom](https://github.com/levilais/Speech-SDK-Module/raw/master/Speech SDK Module/Lunarcom.unitypackage) package de l’élément multimédia. Le package de ressource Lunarcom est une collection de ressources et les scripts développés pour cette série de leçons pour présenter une utilisation pratique de Speech SDK d’Azure. Il s’agit d’un terminal de commande de voix qui sera finalement créent une interface avec l’expérience d’assembly lunaire module développé dans le [didacticiel de Module de Base.](mrlearning-base-ch6.md)
6. Importer le package de la ressource Lunarcom dans votre projet Unity en suivant les étapes similaires que vous avez suivies pour importer le Toolkit de réalité mixte et le Speech SDK.
7. Configurer le Kit de ressources de réalité mixte (MRTK). Pour ce faire, cliquez sur le panneau « Toolkit de réalité mixte » en haut de la fenêtre, puis sélectionnez « Ajouter à la scène et configurer ».

![Module4Chapter1step7im](images/module4chapter1step7im.PNG)

8. Votre scène sera désormais contenir plusieurs nouveaux éléments à partir de la MRTK. Enregistrez votre scène sous un autre nom en cliquant sur « fichier », « enregistrer sous », puis nommez votre scène « SpeechScene ». 

   > Remarque: Si vous appuyez sur le bouton de lecture sur votre scène une fois que vous ajoutez le MRTK à votre projet, et il n’entre pas le mode « lecture », vous devrez peut-être redémarrer Unity. 

9. Avec l’objet « MixedRealityToolkit » sélectionné dans votre hiérarchie, cliquez sur « Copier et personnaliser » dans le panneau de l’inspecteur.

![Module4Chapter1step9im](images/module4chapter1step9im.PNG)

10. Également dans le panneau Inspecteur (avec l’objet « MixedRealityToolkit » sélectionné dans votre hiérarchie), désactiver le système de diagnostic en décochant la case à droite de « Enable Diagnostics System. »

![Module4Chapter1step10im](images/module4chapter1step10im.PNG)

11. Dans le volet de projet, développez le dossier « Lunarcom » et faites glisser le préfabriqué « Lunarcom_Base » dans votre hiérarchie.

![Module4Chapter1step11im](images/module4chapter1step11im.PNG)

12. Sélectionnez l’objet « Lunarcom_Base » dans votre hiérarchie et vérifiez que la position est définie sur x = 0, y = 0 et z = 0, ainsi que la rotation de la valeur x = 0, y = 0 et z = 0. Définir l’échelle lecture x = 0.008, y = 0.008 et z = 0,01.

![Module4Chapter1step12im](images/module4chapter1step12im.PNG)

13. Cliquez sur « Ajouter un composant » puis recherchez et sélectionnez « LunarcomController ». Ce script est inclus dans le pack de ressources Lunarcom que vous avez importé à l’étape 6.

![Module4Chapter1step13im](images/module4chapter1step13im.PNG)

14. Pour vous connecter à notre application à Azure Cognitive Services, vous devez entrer une clé « abonnement » également appelé une « clé API » pour le Service de reconnaissance vocale. Suivez les instructions de [ce lien](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/get-started) pour obtenir une clé d’abonnement gratuit. Une fois que vous obtenez la clé d’abonnement, entrez-le dans le champ « Clé API du Service de reconnaissance vocale » du composant « LunarcomController » dans le panneau d’inspecteur, comme illustré dans l’image ci-dessous.

15. Entrez la région que vous avez choisi lors de votre inscription pour la clé d’abonnement dans le champ « Région du Service de reconnaissance vocale » du composant « LunarcomController » dans le panneau de l’inspecteur.

![Module4Chapter1step15im](images/module4chapter1step15im.PNG)

16. Dans votre hiérarchie, développez l’objet « Lunarcom_Base » en cliquant sur la flèche à gauche de celui-ci, puis faites de même pour son objet enfant, « Terminal Server » comme indiqué dans l’image ci-dessous.

17. « Lunarcom_Base » est sélectionnée, cliquez et faites « Lunarcom Text » à partir de la hiérarchie à l’emplacement « Sortie texte » dans le composant « LunarcomController » dans le panneau d’inspecteur, comme illustré dans l’image ci-dessous.
18. Maintenant effectuer la même chose avec l’objet « Terminal Server » dans l’emplacement « Terminal Server » et l’objet « Connexion Light » à l’emplacement « Connexion Light Controller ».

![Module4Chapter1step18im](images/module4chapter1step18im.PNG)

19. Cliquez sur la flèche en regard de la section « Lunarcom boutons » du script « LunarcomController » dans le panneau d’inspecteur et modifier la taille à 3 et appuyez sur la touche entrée ou retour de votre clavier. Ainsi, trois nouveaux champs « Element » apparaisse.

![Module4Chapter1step19im](images/module4chapter1step19im.PNG)

20. Développez les boutons « Lunarcom » en cliquant sur la flèche en regard de celle-ci dans votre hiérarchie et, à l’aide de la même procédure que ci-dessus, faites glisser le Mic, Satellite et Rocket gameobjects les références de l’élément 0, 1 et 2 respectivement dans le composant « LunarcomController » dans le Panneau de l’inspecteur. 

![Module4Chapter1step18im](images/module4chapter1step20im.PNG)

21. Sélectionnez l’objet « Lunarcom_Base » dans votre hiérarchie. Cliquez sur « Ajouter un composant » dans le panneau d’inspecteur, recherchez puis sélectionnez « LunarcomWakeWordRecognizer ».

![Module4Chapter1step18im](images/module4chapter1step21im.PNG)

22. Dans l’emplacement « Éveil par mot », tapez « Activer Terminal Server. » Également, dans l’emplacement « Ignorer Word », tapez « Terminal Dismiss. »

![Module4Chapter1step18im](images/module4chapter1step22im.PNG)

## <a name="congratulations"></a>Félicitations

Vous avez configuré la reconnaissance vocale dans votre application, alimentée par Azure ! Exécutez l’application pour vérifier que toutes les fonctions sont fonctionne correctement. Démarrer avec indiquant que le mot de mise en éveil que vous avez tapé à l’étape 22, « Activer Terminal Server. » Ensuite, sélectionnez le bouton du microphone pour démarrer la reconnaissance vocale et commencez à parler. Vous verrez vos mots lorsque vous parlez de transcription dans le terminal. Appuyez sur le bouton du microphone une deuxième fois pour arrêter la reconnaissance vocale. Par exemple « Ignorer Terminal Server » pour masquer le terminal Lunarcom. Dans la leçon suivante, nous allez apprendre à basculer dynamiquement à l’utilisation de la reconnaissance vocale sous tension l’appareil, pour les situations où speech d’Azure SDK n’est pas disponible en raison de la version 2 HoloLens hors connexion.

[Leçon suivante : Kit de développement logiciel de reconnaissance vocale leçon 2](mrlearning-speechSDK-ch2.md)

