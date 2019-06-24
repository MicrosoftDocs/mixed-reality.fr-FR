---
title: Module MR Learning ASA Azure ancre spatiale sur HoloLens 2
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: b29f27284c352d27fb1d4d4de701a1ebc2a7cd1c
ms.sourcegitcommit: 30246ab9b9be44a3c707061753e53d4bf401eb6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2019
ms.locfileid: "67327082"
---
# <a name="photon-correct-me-if-im-wrong"></a>Photon (corriger me si je suis incorrect)

Dans cette leçon, 

Objectifs :

* Découvrez comment ___

* Découvrez comment ___

  

## <a name="instructions"></a>Instructions

### <a name="setting-up-photon"></a>Configuration de Photon

1. Configurer un [Photon](https://dashboard.photonengine.com/en-US/Account/SignUp) compte. Cette opération sera constitué de saisir votre adresse de messagerie et de passer par certaines étapes de vérification.
   

![Module2Chapter4step1im](images/Module2chapter4step1im.png)

2. Une fois que vous êtes inscrit, cliquez sur les kits de développement logiciel. Une fois que vous êtes sur cette page, cliquez sur « server » et vous assurer de l’état est « auto-hébergé. » Puis faites défiler vers le bas et cliquez sur « server », comme indiqué dans la deuxième image ci-dessous.

   

   ![Module2Chapter2step2aim](images/Module2chapter4step2aim.png)

   ![Module2Chapter2step2bim](images/Module2chapter4step2bim.png)
   
   3. Si vous le faites étiqueté, une zone de texte « lire me. » Continuons et le lire. Une fois que vous avez terminé, cliquez sur le lien en regard de « downloadSDK » afin de le télécharger.


![Module2Chapter4step3im](images/Module2chapter4step3im.png)

4. Sur le dossier une fois le téléchargement terminé.  Une fois que l’Explorateur de fichiers s’ouvre, révélant le dossier du Kit de développement logiciel, copiez le dossier SDK.
   
   - L’étape suivante consisterait à aller dans le lecteur C: windows et créez un dossier appelé « serveur ».
   
   ![Module2Chapter4step4im](images/Module2chapter4step4aim.png)
   
   - Ouvrez le dossier et coller le dossier SDK que vous avez copiée précédemment.
   
   ![Module2Chapter4step4im](images/Module2chapter4step4bim.png)
   
5. Une fois cette opération terminée, ouvrez le dossier SDK et accédez à « déployer », puis « bin_Win64 », et double-cliquez sur « contrôle photon ».


![Module2Chapter4step4im](images/Module2chapter4step5im.png)

> Remarque: Si vous avez des questions sur l’adresse IP ou autres questions similaires, vous trouverez la plupart de vos informations dans la barre d’outils (comme indiqué dans l’image ci-dessous).
>
> ![Module2Chapter4step4im](images/Module2chapter4noteim.png)

6. Maintenant que le serveur est configuré et lancé, revenez en arrière vers le site Web de Photon et cliquez sur l’icône de profil (converti (boxed) dans l’image ci-dessous) et sélectionnez « vos applications. »
   

![Module2Chapter3step5im](images/Module2chapter4step6im.png)

7. Créer un ID d’application en cliquant sur le bouton « Créer une nouvelle application ».

   ![Module2Chapter3step8im](images/Module2chapter4step7aim.png)

   - Sélectionnez « Exécuter Photon » dans le menu déroulant sous « type photon. » Puis lui donner un nom (quelque chose que vous devez vous rappeler). Dans cet exemple, nous l’avons appelé « HoloLensPhotonProject ». Une fois que vous avez terminé, cliquez sur « Créer ».

   ![Module2Chapter3step8im](images/Module2chapter4step7bim.png)

8. Une fois cette opération effectuée, revenez à la page de vos applications et vous devriez voir quelque chose de similaire à l’image ci-dessous. Cliquez sur l’ID d’application et copiez-la. Coller est dans un endroit que facilement accessible.  
   

![Module2Chapter4step9im](images/Module2chapter4step8im.png)

9. Créez un projet unity. Ouvrez le Hub de Unity, puis cliquez sur « Nouveau ». Nommez-le « HLSharingProject. » Cliquez ensuite sur Créer. 

   > Remarque : Cela peut prendre jusqu'à 2 minutes à charger, selon la vitesse de votre ordinateur.

![Module2Chapter4step9im](images/Module2chapter4step9im.png)

> Remarque : choisir un emplacement pour enregistrer votre projet sur votre ordinateur en modifiant l’option « emplacement ». Enregistrez-le dans un emplacement conserve et ont un accès facile aux.

10. Une fois le projet se charge, cliquez sur le « magasin de ressources ». Puis, dans la zone de recherche illustrée dans l’image ci-dessous, tapez « A » et sélectionnez la ressource « Photon gratuit a-2 ». 

    ![Module2Chapter4step10im](images/Module2chapter4step10im.PNG)
    
    11. Téléchargez et importez !
    
    ![Module2Chapter4step11im](images/Module2chapter4step11im.png)

### <a name="setting-up-the-unity-project"></a>**Configuration du projet Unity** 

11. télécharger une nouvelle ressource nécessaire pour configurer Photon dans Unity en cliquant sur [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Examples-v2.0.0-RC1-Refresh.unitypackage)

12. Dans Unity, cliquez sur le menu de ressources et sélectionnez « Importer des actifs », puis cliquez sur « ressources personnalisées ».

![Module2Chapter4step12im](images/Module2chapter4step12im.PNG)

13. Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1. Une fois que le bouton Importer s’affiche dans Unity, cliquez dessus.

![Module2Chapter4step13im](images/Module2chapter4step13im.png)

> Remarque :, là où vous avez téléchargé le package sera où vous le trouver. L’image ci-dessus ne transmettent pas où vous trouverez le package.

14. Créer une nouvelle scène (Cela peut être effectuée à l’aide de contrôle / commande + N ou en cliquant sur « fichier » et sélectionnez « nouvelle scène. »). Enregistrer la scène en tant que « HLSharedProjectMain ».

> Remarque : vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous. Pour l’instant, cliquez simplement sur « non ».
>
> ![Module2Chapter4note2im](images/Module2chapter4note2im.png)

15. Sous « Toolkit de réalité mixte », cliquez sur « Ajouter à la scène et configurer ».

![Module2Chapter4step15im](images/Module2chapter4step15im.png)

16. Une fois cette opération terminée, un nouveau fichier de configuration s’affiche, ce qui vous donne la possibilité de personnaliser le profil. Cliquez sur « Copier et la personnaliser. »

![Module2Chapter4step16im](images/Module2chapter4step16im.png)

17. Défiler vers le bas et décochez la case « Activer le système de diagnostic ». Cela rend plus facile de configurer ce projet.

![Module2Chapter4step17im](images/Module2chapter4step17im.png)

18. Ouvrez les paramètres de build (contrôle + MAJ + B). Notez que le programme est actuellement défini sous la plateforme « PC, Mac et Linux autonome ». Pour ce projet, définissez la plateforme pour être « plateforme windows universelle. » Sélectionnez-le et cliquez sur « commutateur plateforme. »

![Module2Chapter4step18im](images/Module2chapter4step18im.png)

19. Une fois terminé, cliquez sur la zone intitulée « Ajouter des scènes open ». Accédez à présent le panneau Inspecteur et vérifiez que la case à cocher à droite de la « réalité virtuelle pris en charge » (comme indiqué dans l’image ci-dessous) est activée. 

![Module2Chapter4step19im](images/Module2chapter4step19im.png)

> Remarque : Assurez-vous également que la case à cocher en regard de « arrière-plan/HLSharedProjectMain » est également cochée.

20. Sous « paramètres de publication » dans le panneau Inspecteur faites défiler jusqu'à « fonctionnalités » et vous assurer seulement les cases à cocher suivantes sont marquées :

- client Internet
- internet client server
- serveur client de réseau privé
- camera/webcam
- Microphone

21. Comme étape 12, l’étape suivante serait pour importer un autre package personnalisé appelé « Lesson2 », qui peut être téléchargé [ici]. [lesson2.unitypackage lien ici] Importez ce package.

![Module2Chapter4step21im](images/Module2chapter4step20im.png)

22. Désormais, dans le volet de projet, aller sur le dossier « prefabs », étant donné que dans les prochaines étapes, vous allez implémenter quelques prefabs dans la scène. Dans le dossier « prefabs », cliquez et faites glisser le préfabriqué, « DebugWindow » dans la hiérarchie. Une fois que vous avez terminé, enregistrez le projet (cliquez sur fichier, puis l’enregistrer, ou CTRL + S)

![Module2Chapter4step22im](images/Module2chapter4step21im.PNG)

> Remarque : Vous pouvez remarquer une fenêtre contextuelle s’affichent lorsque vous cliquez sur le préfabriqué, vous demandant sur TMP Essentials. Cliquez sur « Importation TMP Essentials » car ils vous seront utiles.
>
> ![Module2Chapter4note3im](images/Module2chapter4note3im.PNG)

### <a name="connecting-multiple-users"></a>**Plusieurs utilisateurs qui se connectent**

23. À l’étape 22, dans le dossier « prefabs » dans le volet de projet, l’étape suivante consiste à glisser -déplacer le préfabriqué « NetworkLobby » à la hiérarchie. 

![Module2Chapter4step22im](images/Module2chapter4step22im.png)

24. Lorsque vous ouvrez le préfabriqué parent, « NetworkLobby », vous devez voir un enfant prefab, « NetworkRoom ». Avec qu’elle est sélectionnée, accédez au volet d’inspecteur, puis cliquez sur « Ajouter le composant ». Recherchez « PhotonView » et ajouter le composant.

![Module2Chapter4step23im](images/Module2chapter4step23im.png)

25. Créer un nouvel objet de jeu vide dans la hiérarchie (clic droit dans la hiérarchie et choisissez « vide »). Vérifiez le positionnement est défini sur x = 0, y = 0, z = 0 et nommer l’objet, « PhotonUser ».

![Module2Chapter4step24im](images/Module2chapter4step24im.png)

## <a name="congratulations"></a>Félicitations



