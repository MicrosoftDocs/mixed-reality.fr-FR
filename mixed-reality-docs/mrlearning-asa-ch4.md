---
title: Module ASA d’apprentissage de la fonction d’ancrage spatial Azure sur HoloLens 2
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens
ms.openlocfilehash: 141aa90f2bf5d90527a0fe1e6a812c1ce56bd0eb
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437792"
---
# <a name="photon-correct-me-if-im-wrong"></a>Photonique (corrigez-moi si je ne suis pas correct)

Dans cette leçon, 

Cherché

* En savoir plus sur _____________________________________________

* En savoir plus sur _________________________________________________

  

## <a name="instructions"></a>Instructions

### <a name="setting-up-photon"></a>Configuration de photons

1. Configurez un compte de [photons](https://dashboard.photonengine.com//Account/SignUp) . Cela consiste à imputer votre adresse de messagerie et à passer par certaines étapes de vérification.
   

![Module2Chapter4step1im](images/Module2chapter4step1im.png)

2. Une fois que vous êtes inscrit, cliquez sur kits de développement logiciel (SDK). Une fois que vous êtes sur cette page, cliquez sur « serveur » et assurez-vous que le message « auto-hébergé » s’affiche. Faites défiler vers le bas et cliquez sur « serveur » comme illustré dans la deuxième image ci-dessous.

   

   ![Module2Chapter2step2aim](images/Module2chapter4step2aim.png)

   ![Module2Chapter2step2bim](images/Module2chapter4step2bim.png)
   
   3. Cela entraînera l’affichage d’une zone de texte intitulée « Lisez-moi ». Continuez et lisez-le. Une fois que vous avez terminé, cliquez sur le lien en regard de « downloadSDK » pour le télécharger.


![Module2Chapter4step3im](images/Module2chapter4step3im.png)

4. Double-cliquez sur le dossier une fois son téléchargement terminé.  Une fois que votre Explorateur de fichiers s’ouvre et affiche le dossier SDK, copiez le dossier SDK.
   
   - L’étape suivante consiste à accéder au lecteur Windows C : et à créer un nouveau dossier appelé « serveur ».
   
   ![Module2Chapter4step4im](images/Module2chapter4step4aim.png)
   
   - Ouvrez maintenant le dossier, puis collez le dossier SDK que vous avez copié précédemment.
   
   ![Module2Chapter4step4im](images/Module2chapter4step4bim.png)
   
5. Une fois cette opération terminée, ouvrez le dossier SDK et accédez à « Deploy », puis à « bin_Win64 », puis double-cliquez sur « contrôle de photons ».


![Module2Chapter4step4im](images/Module2chapter4step5im.png)

> Remarque : Si vous avez des questions concernant l’adresse IP, ou toute autre question similaire, vous pouvez trouver la plupart de vos informations dans la barre d’outils (comme indiqué dans l’image ci-dessous).
>
> ![Module2Chapter4step4im](images/Module2chapter4noteim.png)

6. Maintenant que le serveur est configuré et lancé, retournez sur le site Web de photons et cliquez sur l’icône de profil (boxed dans l’image ci-dessous), puis sélectionnez « vos applications ».
   

![Module2Chapter3step5im](images/Module2chapter4step6im.png)

7. Créez un ID d’application en cliquant sur le bouton « créer une application ».

   ![Module2Chapter3step8im](images/Module2chapter4step7aim.png)

   - Sélectionnez « série de photons » dans le menu déroulant sous « type de photons ». Ensuite, donnez-lui un nom (ce qui vous rappellerait). Dans cet exemple, nous l’avons nommé « HoloLensPhotonProject ». Une fois que vous avez terminé, cliquez sur « créer ».

   ![Module2Chapter3step8im](images/Module2chapter4step7bim.png)

8. Une fois cette opération effectuée, revenez à la page de votre application et vous devriez voir une image semblable à celle ci-dessous. Cliquez sur l’ID d’application et copiez-le. Coller est un endroit où vous pouvez accéder facilement à.  
   

![Module2Chapter4step9im](images/Module2chapter4step8im.png)

9. Créez un nouveau projet Unity. Ouvrez Unity Hub et cliquez sur « nouveau ». Nommez-la « HLSharingProject ». Cliquez ensuite sur créer. 

   > Remarque : le chargement peut prendre jusqu’à 2 minutes, en fonction de la vitesse de votre ordinateur.

![Module2Chapter4step9im](images/Module2chapter4step9im.png)

> Remarque : choisissez un emplacement pour enregistrer votre projet sur votre ordinateur en modifiant l’option « emplacement ». Enregistrez-le à un endroit dont vous vous souviendrez pour accéder facilement à.

10. Une fois le projet chargé, cliquez sur le « magasin d’actifs ». Ensuite, dans la zone de recherche présentée dans l’image ci-dessous, tapez « retentissante » et sélectionnez la ressource « photon retentissante-2 FREE ». 

    ![Module2Chapter4step10im](images/Module2chapter4step10im.PNG)
    
    11. Téléchargez et importez !
    
    ![Module2Chapter4step11im](images/Module2chapter4step11im.png)

### <a name="setting-up-the-unity-project"></a>**Configuration du projet Unity** 

11. Téléchargez une nouvelle ressource nécessaire à la configuration de photons dans Unity en cliquant [ici.](https://github.com/microsoft/MixedRealityToolkit-Unity/releases/download/v2.0.0-RC1-Refresh/Microsoft.MixedReality.Toolkit.Unity.Examples-v2.0.0-RC1-Refresh.unitypackage)

12. Dans Unity, cliquez sur le menu composants et sélectionnez « Importer des ressources », puis cliquez sur « ressources personnalisées ».

![Module2Chapter4step12im](images/Module2chapter4step12im.PNG)

13. Sélectionnez le package Unity que vous venez de télécharger à partir du lien fourni à l’étape 1. Une fois que le bouton Importer apparaît dans Unity, cliquez dessus.

![Module2Chapter4step13im](images/Module2chapter4step13im.png)

> Remarque : chaque fois que vous avez téléchargé le package dans, vous le trouverez. L’image ci-dessus ne décrit pas où se trouve le package.

14. Créez une nouvelle scène (cette opération peut être effectuée à l’aide de Control/Command + N ou en cliquant sur « file » et en sélectionnant « New Scene ».) Enregistrez la scène en tant que « HLSharedProjectMain ».

> Remarque : vous pouvez recevoir une fenêtre contextuelle qui ressemble à l’image ci-dessous. Pour le moment, cliquez simplement sur « non ».
>
> ![Module2Chapter4note2im](images/Module2chapter4note2im.png)

15. Sous « Mixed Reality Toolkit », cliquez sur « Ajouter à la scène et configurer ».

![Module2Chapter4step15im](images/Module2chapter4step15im.png)

16. Une fois cette opération terminée, un nouveau fichier de configuration s’affiche et vous donne la possibilité de personnaliser le profil. Cliquez sur « copier et personnaliser ».

![Module2Chapter4step16im](images/Module2chapter4step16im.png)

17. Faites défiler vers le dessous et décochez « activer le système de diagnostic ». Cela facilitera la configuration de ce projet.

![Module2Chapter4step17im](images/Module2chapter4step17im.png)

18. Ouvrez les paramètres de build (Ctrl + Maj + B). Notez que le programme est actuellement défini sous la plateforme « PC, Mac et Linux standalone ». Pour ce projet, définissez la plateforme sur « plateforme Windows universelle ». Sélectionnez-le et cliquez sur « changer de plateforme ».

![Module2Chapter4step18im](images/Module2chapter4step18im.png)

19. Une fois l’opération terminée, cliquez sur la case « Ajouter des scènes ouvertes ». Maintenant, accédez au panneau inspecteur et vérifiez que la case à cocher située à droite de « Virtual Reality pris en charge » (comme indiqué dans l’image ci-dessous) est cochée. 

![Module2Chapter4step19im](images/Module2chapter4step19im.png)

> Remarque : Assurez-vous également que la case à cocher en regard de « scènes/HLSharedProjectMain » est également activée.

20. Sous les paramètres de publication dans le volet de l’inspecteur, faites défiler la liste jusqu’à « fonctionnalités » et assurez-vous que seules les cases à cocher suivantes sont activées :

- client Internet
- serveur client Internet
- serveur client de réseau privé
- caméra/Webcam
- microphone

21. À l’instar de l’étape 12, l’étape suivante consiste à importer un autre package personnalisé appelé « Lesson2 », que vous pouvez télécharger [ici.] [lien lesson2. pour Unity ici] Importez ce package.

![Module2Chapter4step21im](images/Module2chapter4step20im.png)

22. Maintenant, dans le panneau projet, accédez au dossier « prefabs », car dans les étapes suivantes, vous allez implémenter quelques prefabs dans la scène. Dans le dossier « prefabs », cliquez et faites glisser Prefab, « DebugWindow » dans la hiérarchie. Une fois que vous avez terminé, enregistrez le projet (cliquez sur fichier, puis sur enregistrer ou sur contrôle + S).

![Module2Chapter4step22im](images/Module2chapter4step21im.PNG)

> Remarque : vous pouvez remarquer qu’une fenêtre contextuelle s’affiche lorsque vous cliquez sur Prefab pour vous poser des questions sur TMP Essentials. Cliquez sur « Importer TMP Essentials », car ils seront nécessaires.
>
> ![Module2Chapter4note3im](images/Module2chapter4note3im.PNG)

### <a name="connecting-multiple-users"></a>**Connexion de plusieurs utilisateurs**

23. Comme dans l’étape 22, dans le dossier « prefabs » du panneau projet, l’étape suivante consiste à faire glisser et déposer le Prefab « NetworkLobby » dans la hiérarchie. 

![Module2Chapter4step22im](images/Module2chapter4step22im.png)

24. Lorsque vous ouvrez le Prefab parent, « NetworkLobby », vous devez voir un Prefab enfant, « NetworkRoom ». Une fois l’option sélectionnée, accédez au panneau de l’inspecteur, puis cliquez sur Ajouter un composant. Recherchez « PhotonView » et ajoutez le composant.

![Module2Chapter4step23im](images/Module2chapter4step23im.png)

25. Créez un nouvel objet de jeu vide dans la hiérarchie (cliquez avec le bouton droit dans la hiérarchie et sélectionnez « vide »). Assurez-vous que le positionnement est défini sur x = 0, y = 0, z = 0 et nommez l’objet, « PhotonUser ».

![Module2Chapter4step24im](images/Module2chapter4step24im.png)

## <a name="congratulations"></a>Félicitations !



