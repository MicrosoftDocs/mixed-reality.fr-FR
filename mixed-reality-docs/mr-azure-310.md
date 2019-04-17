---
title: MR et 310 Azure - détection d’objets
description: Effectuez ce cours pour apprendre à former un modèle d’apprentissage, puis utilisez le modèle formé pour reconnaître des objets similaires et leur position dans le monde réel à partir d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, vision personnalisée, l’objet de détection, mixte réalité academy, unity, didacticiel, api, hololens
ms.openlocfilehash: 89ee79943a88de8a34c679ae33621db5770908b0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593286"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

# <a name="mr-and-azure-310-object-detection"></a>MR et Azure 310 : Détection d’objets

Dans ce cours, vous allez apprendre à reconnaître le contenu visuel personnalisé et sa position spatiale dans une image fournie, à l’aide de Vision personnalisée Azure des fonctionnalités de « Détection d’objets » dans une application de réalité mixte.

Ce service vous permettra de former un modèle d’apprentissage automatique à l’aide d’images de l’objet. Vous allez utiliser ensuite le modèle formé pour reconnaître des objets similaires et se rapprocher de leur emplacement dans le monde réel, tel que fourni par la capture de l’appareil photo de Microsoft HoloLens ou une caméra de se connecter à un PC pour des casques IMMERSIFS (VR).

![résultat de cours](images/AzureLabs-Lab310-00.png)

**Vision personnalisée Azure, la détection d’objets** est un Service Microsoft qui permet aux développeurs de créer des classifieurs de l’image personnalisée. Ces classifieurs peuvent ensuite servir avec les nouvelles images pour détecter des objets au sein de cette nouvelle image, en fournissant **limites de la zone** dans l’image elle-même. Le Service fournit un portail en ligne simple et facile à utiliser, pour simplifier ce processus. Pour plus d’informations, consultez les liens suivants :

* [Page de Vision personnalisée Azure](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home)
* [Limites et Quotas](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/limits-and-quotas)

À la fin de ce cours, vous disposez d’une application de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :

1. L’utilisateur sera en mesure de *les regards* à un objet, ils ont formé à l’aide de Azure Custom Vision Service, détection d’objets. 
2. L’utilisateur utilisera la *appuyez sur* mouvement à capturer une image de ce qu’ils cherchent à.
3. L’application envoie l’image à Azure Custom Vision Service.
4. Il y aura une réponse à partir du Service qui affiche le résultat de la reconnaissance en tant que texte de l’espace universel. Cela doit être effectué via l’utilisation spatiale de suivi du Microsoft HoloLens, comme un moyen de comprendre la position du monde de l’objet reconnu, puis en utilisant le *balise* associé à ce qui est détecté dans l’image, à fournir le texte d’étiquette.

Ce cours couvre également manuellement durant le chargement d’images, création de balises, et de formation au Service, à reconnaître différents objets (dans l’exemple fourni, une tasse), en définissant le *boîte limite* au sein de l’image que vous envoyez. 

> [!IMPORTANT]
> Après la création et l’utilisation de l’application, le développeur doit revenir à Azure Custom Vision Service et d’identifier les prédictions générées par le Service et déterminer si elles ont été correctes ou non (par le biais de balisage quoi que ce soit le Service manquée, et ajuster la *englobants*). Le Service peut ensuite être ré-formé, ce qui augmente la probabilité qu’il reconnaissance des objets du monde réel.

Ce cours va vous apprendre à obtenir les résultats à partir de Azure Custom Vision Service, détection d’objets, dans une application basée sur Unity. Il le sera jusqu'à vous permettent d’appliquer ces concepts à une application personnalisée, que vous voudrez peut-être générer.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 310 : Détection d’objets</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.

Nous recommandons le matériel et logiciel pour ce cours suivants :

- Un PC de développement
- [Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [Le SDK Windows 10 dernières](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [Unity 2017.4 LTS](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [Visual Studio 2017](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- Un [Microsoft HoloLens](https://docs.microsoft.com/windows/mixed-reality/hololens-hardware-details) avec le mode développeur est activé
- Accès à Internet pour le programme d’installation Azure et de récupération du Service Vision personnalisée
-  Une série d’images au moins quinze (15) sont nécessaires) pour chaque objet que vous souhaitez que la Vision personnalisée pour reconnaître. Si vous le souhaitez, vous pouvez utiliser les images déjà fournis avec ce cours, [une série de tasses](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).
2.  Configurer et tester votre HoloLens. Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur). 

Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1---the-custom-vision-portal"></a>Chapitre 1 : le portail de Vision personnalisée

Pour utiliser le **Azure Custom Vision Service**, vous devez configurer une instance de celle-ci à la disposition de votre application.

1.  Accédez [à la **Service Vision personnalisée** page principale](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).

2.  Cliquez sur **mise en route**.

    ![](images/AzureLabs-Lab310-01.png)

3.  Connectez-vous au portail de Vision personnalisée.

    ![](images/AzureLabs-Lab310-02.png)

4.  Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

5.  Une fois que vous êtes connecté pour la première fois, vous serez invité au *termes du contrat de Service* Panneau de configuration. Cliquez sur la case à cocher pour *accepte les termes du contrat*. Puis cliquez sur **J’accepte**.

    ![](images/AzureLabs-Lab310-03.png)

6.  Ayant accepté les termes du contrat, vous êtes maintenant dans le *Mes projets* section. Cliquez sur **nouveau projet**.

    ![](images/AzureLabs-Lab310-04.png)

7.  Un onglet s’affiche sur le côté droit, qui vous invite à spécifier des champs pour le projet.

    1.  Insérer un nom pour votre projet

    2.  Insérer une description pour votre projet (**facultatif**)

    3.  Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).

        ![](images/AzureLabs-Lab310-05.png)

        > [!NOTE]
        > Si vous souhaitez [en savoir plus sur les groupes de ressources Azure, accédez à la documentation associée](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)

    4.  Définir le **Types de projets** comme **détection d’objets (version préliminaire)**.

8.  Une fois que vous avez terminé, cliquez sur **créer un projet**, et vous êtes redirigé vers la page de projet de Service Vision personnalisée.


## <a name="chapter-2---training-your-custom-vision-project"></a>Chapitre 2 - formation de votre projet de Vision personnalisée

Une fois dans le portail de Vision personnalisée, votre objectif principal est pour l’apprentissage de votre projet pour reconnaître des objets spécifiques dans des images.

Vous devez au moins quinze (15) les images pour chaque objet que vous souhaitez que votre application à reconnaître. Vous pouvez utiliser les images fournies avec ce cours ([une série de tasses](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).

Pour l’apprentissage de votre projet de Vision personnalisée :

1.  Cliquez sur le **+** situé en regard **balises**.

    ![](images/AzureLabs-Lab310-06.png)

2.  Ajouter un **nom** pour la balise qui sera utilisée pour associer vos images avec. Dans cet exemple, nous utilisons des images de tasses de reconnaissance, afin d’avoir nommé la balise pour ce faire, **Cup**. Cliquez sur **enregistrer** une fois terminé.

    ![](images/AzureLabs-Lab310-07.png)

3.  Vous remarquerez votre **balise** a été ajouté (vous devrez peut-être recharger votre page pour qu’il apparaisse). 

    ![](images/AzureLabs-Lab310-08.png)

4.  Cliquez sur **ajouter des images** dans le centre de la page.

    ![](images/AzureLabs-Lab310-09.png)

5.  Cliquez sur **parcourir les fichiers locaux**et cliquez sur Parcourir pour les images que vous voulez charger un objet, avec le minimum étant quinze (15).

    > [!TIP]
    >  Vous pouvez sélectionner plusieurs images à la fois, à télécharger.

    ![](images/AzureLabs-Lab310-10.png)

6.  Appuyez sur **charger des fichiers** une fois que vous avez sélectionné toutes les images vous souhaitez effectuer le projet avec l’apprentissage. Les fichiers de lancer le chargement. Une fois que vous avez la confirmation du téléchargement, cliquez sur **fait**.

    ![](images/AzureLabs-Lab310-11.png)

7.  À ce stade vos images sont téléchargées, mais pas marquées.

    ![](images/AzureLabs-Lab310-12.png)

8.  Pour marquer vos images, utilisez votre souris. Lorsque vous pointez sur votre image, une mise en surbrillance de sélection vous aider en dessinant automatiquement une sélection autour de votre objet. Si elle n’est pas exacte, vous pouvez dessiner vos propres. Pour cela, en maintenant le clic gauche sur la souris, en faisant glisser la zone sélectionnée pour votre objet. 

    ![](images/AzureLabs-Lab310-13.png) 

9. Après la sélection de votre objet dans l’image, une petite invite vous demandera vous *ajouter les balises Region*. Sélectionnez votre balise créé précédemment ('Cup', dans l’exemple ci-dessus), ou si vous ajoutez des balises de plus, dans le type et cliquez sur le **+ (plus)** bouton.

    ![](images/AzureLabs-Lab310-14.png) 

10. Pour marquer l’image suivante, cliquez sur la flèche à droite du panneau, ou fermez le panneau de balise (en cliquant sur le **X** dans l’angle supérieur droit du panneau) puis cliquez sur l’image suivante. Une fois que vous avez l’image suivante prêt, répétez la même procédure. Pour toutes les images que vous avez chargé, jusqu'à ce qu’elles sont marquées pour cela. 

    > [!NOTE]
    >  Vous pouvez sélectionner plusieurs objets dans la même image, comme dans l’image ci-dessous : 
    > 
    > ![](images/AzureLabs-Lab310-15.png)

11. Une fois que vous avez marqué toutes les, cliquez sur le **avec balises** bouton, sur la gauche de l’écran, pour afficher les images avec balises. 

    ![](images/AzureLabs-Lab310-16.png)

12. Vous êtes maintenant prêt à former votre Service. Cliquez sur le **Train** bouton et la première itération d’entraînement commencera.

    ![](images/AzureLabs-Lab310-17.png)

    ![](images/AzureLabs-Lab310-18.png)

13. Une fois qu’il est créé, vous serez en mesure de voir les deux boutons nommés **par défaut** et **prédiction URL**. Cliquez sur **par défaut** tout d’abord, puis cliquez sur **prédiction URL**.

    ![](images/AzureLabs-Lab310-19.png)

    > [!NOTE] 
    > Le point de terminaison qui est fourni à partir de ce problème, selon ce qui a *itération* a été marquée comme valeur par défaut. Par conséquent, si vous apportez ultérieurement un nouveau *itération* et mettez-le à jour comme valeur par défaut, vous ne devez pas modifier votre code.

14. Une fois que vous avez cliqué sur **prédiction URL**, ouvrez *le bloc-notes*, puis copiez et collez le **URL** (également appelé votre **prédiction-point de terminaison**) et le **prédiction-clé du Service**, de sorte que vous pouvez les récupérer lorsque vous en avez besoin plus loin dans le code.

    ![](images/AzureLabs-Lab310-20.png)

## <a name="chapter-3---set-up-the-unity-project"></a>Chapitre 3 - configurer le projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez **Unity** et cliquez sur **New**.

    ![](images/AzureLabs-Lab310-21.png)

2.  Maintenant, vous devez fournir un nom de projet Unity. Insérer **CustomVisionObjDetection**. Assurez-vous que le type de projet est défini sur **3D**et définissez le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![](images/AzureLabs-Lab310-22.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **modifier* > *préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio**. Fermer le **préférences** fenêtre.

    ![](images/AzureLabs-Lab310-23.png)

4.  Ensuite, accédez à **fichier > Paramètres de Build** et basculez le **plateforme** à *plateforme Windows universelle*, puis en cliquant sur le **basculer plateforme** bouton.

    ![](images/AzureLabs-Lab310-24.png)

5.  Dans le même **paramètres de Build** fenêtre, vérifiez les éléments suivants sont définis :

    1.  **Équipement cible** a la valeur **HoloLens**        
    2.  **Type de build** a la valeur **D3D**
    3.  **Kit de développement logiciel** a la valeur **dernière installé**
    4.  **Version de Visual Studio** a la valeur **dernière installé**
    5.  **Générez et exécutez** est défini sur **ordinateur Local**            
    6.  Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.

        ![](images/AzureLabs-Lab310-25.png)

6.  Dans le même **paramètres de Build** fenêtre, cliquez sur le **paramètres du lecteur** bouton, le panneau de configuration associée s’ouvre dans l’espace où le **inspecteur** se trouve.

7. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1.  Dans le **autres paramètres** onglet :

        1.  **Version du Runtime de script** doit être **expérimental** (.NET 4.6 équivalent), ce qui déclenchera une nécessité de redémarrer l’éditeur.

        2. **Script principal** doit être **.NET**.

        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**.

            ![](images/AzureLabs-Lab310-26.png)

    2.  Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        1. **InternetClient**

        2.  **Webcam**

        3. **SpatialPerception**

            ![](images/AzureLabs-Lab310-27.png) ![](images/AzureLabs-Lab310-28.png)

    3.  Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, puis assurez-vous que le **mixte Windows Réalité SDK** est ajouté.

        ![](images/AzureLabs-Lab310-29.png)

8.  Dans **paramètres de Build**, *Unity C\# projets* est n’est plus grisée : cochez la case à cocher en regard de cela.

9.  Fermer le **paramètres de Build** fenêtre.

10. Dans le **éditeur**, cliquez sur **modifier** > **paramètres du projet** > **graphiques**.

    ![](images/AzureLabs-Lab310-30.png)

11. Dans le **panneau Inspecteur** le *paramètres graphiques* seront ouvertes. Défiler vers le bas jusqu'à ce que vous voyiez un tableau appelé **incluent toujours les nuanceurs**. Ajouter un emplacement en augmentant la **taille** variable d’une unité (dans cet exemple, il avait la valeur 8 pourquoi nous fait il 9). Un nouvel emplacement s’affiche, dans la dernière position du tableau, comme indiqué ci-dessous :

    ![](images/AzureLabs-Lab310-31.png)

12. Dans l’emplacement, cliquez sur le cercle de cible de petite taille en regard de l’emplacement pour ouvrir une liste des nuanceurs. Recherchez le **hérité nuanceurs/Transparent/diffusion** nuanceur et double-cliquez dessus. 

    ![](images/AzureLabs-Lab310-32.png)

## <a name="chapter-4---importing-the-customvisionobjdetection-unity-package"></a>Chapitre 4 - Importation du package CustomVisionObjDetection Unity

Pour ce cours vous sont fournis avec un Package de ressource Unity appelé **Azure-MR-310.unitypackage**. 

> [CONSEIL] Tous les objets pris en charge par Unity, notamment des scènes, peuvent être empaquetés dans un **.unitypackage** de fichiers et exportés / importés dans d’autres projets. C’est le moyen le plus sûr et plus efficace, pour déplacer des ressources entre différents **projets Unity**.

Vous pouvez trouver la [package Azure-MR-310 dont vous avez besoin pour télécharger ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Azure-MR-310.unitypackage).

1.  Avec le tableau de bord Unity devant vous, cliquez sur **actifs** dans le menu en haut de l’écran, puis cliquez sur **importer un Package > Custom Package**.

    ![](images/AzureLabs-Lab310-33.png)

2.  Utilisez le sélecteur de fichiers pour sélectionner le **Azure-MR-310.unitypackage** du package et cliquez sur **Open**. Une liste des composants de cette ressource s’affichera pour vous. Confirmez l’importation en cliquant sur le **importer** bouton.

    ![](images/AzureLabs-Lab310-34.png)

3.  Une fois l’importation terminée, vous remarquerez que les dossiers à partir du package ont désormais été ajoutées à votre **actifs** dossier. Ce type de structure de dossiers est généralement utilisé pour un projet Unity.

    ![](images/AzureLabs-Lab310-35.png)

    1.  Le **matériaux** dossier contient le matériel utilisé par le **curseur les regards**. 

    2.  Le **plug-ins** dossier contient la DLL Newtonsoft utilisé par le code pour désérialiser la réponse du Service web. Les deux (2) différentes versions contenues dans le dossier et un sous-dossier, sont nécessaires pour que la bibliothèque à utiliser et généré par l’éditeur Unity et de la build UWP. 

    3.  Le **Prefabs** dossier contient les prefabs contenues dans la scène. Ce sont :

        1.  Le **GazeCursor**, le curseur utilisé dans l’application. Fonctionne avec le préfabriqué SpatialMapping pour pouvoir être placé dans la scène au-dessus des objets physiques.
        2.  Le **étiquette**, qui est l’objet d’interface utilisateur permettant d’afficher la balise object dans la scène lorsque nécessaire.
        3.  Le **SpatialMapping**, qui est l’objet qui permet à l’application à utiliser crée une carte virtuelle, à l’aide de suivi spatial du Microsoft HoloLens.

    4.  Le **scènes** dossier qui contient actuellement la scène prédéfinie pour ce cours.

4.  Ouvrir le **scènes** dossier, dans le **panneau projet**et double-cliquez sur le **ObjDetectionScene**, pour charger la scène que vous allez utiliser pour ce cours.

    ![](images/AzureLabs-Lab310-36.png)

    > [!NOTE] 
    >  **Aucun code n’est inclus**, vous allez écrire le code en suivant ce cours.

## <a name="chapter-5---create-the-customvisionanalyser-class"></a>Chapitre 5 : créer la classe CustomVisionAnalyser.

À ce stade, vous êtes prêt à écrire du code. Vous allez commencer avec le **CustomVisionAnalyser** classe.

> [!NOTE]
> Les appels à la **Service Vision personnalisée**, effectuée dans le code indiqué ci-dessous, sont effectuées à l’aide de la **API REST de Vision personnalisée**. Via l’utilisant, vous verrez comment implémenter et utiliser cette API (utile pour comprendre comment implémenter quelque chose de similaire sur votre propre). Sachez que Microsoft propose un **Custom Vision SDK** qui peut également être utilisé pour effectuer des appels au Service. Pour plus d’informations, visitez le [article du Kit de développement logiciel Custom Vision](https://github.com/Microsoft/Cognitive-CustomVision-Windows/).

Cette classe est chargée de :

- Chargement de la dernière image capturée sous la forme d’un tableau d’octets.

- Envoyer le tableau d’octets à votre Azure **Service Vision personnalisée** instance pour l’analyse.

- Recevoir une réponse sous forme de chaîne JSON.

- La désérialisation de la réponse et en passant résultant **prédiction** à la **SceneOrganiser** (classe), qui se chargera de la façon dont la réponse doit être affichée.

Pour créer cette classe :

1.  Avec le bouton droit dans le **dossier composants**, situé dans le **panneau projet**, puis cliquez sur **créer** > **dossier**. Appelez le dossier **Scripts**.

    ![](images/AzureLabs-Lab310-37.png)

2.  Double-cliquez sur le dossier nouvellement créé, pour l’ouvrir.

3.  Avec le bouton droit dans le dossier, puis cliquez sur **créer** > **C\# Script**. Nommez le script **CustomVisionAnalyser.**

4.  Double-cliquez sur le nouveau **CustomVisionAnalyser** script pour l’ouvrir avec **Visual Studio.**

5.  Vérifiez que vous disposez des espaces de noms suivants référencé au début du fichier :

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.IO;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

6.  Dans le **CustomVisionAnalyser** de classe, ajoutez les variables suivantes :

    ```csharp
        /// <summary>
        /// Unique instance of this class
        /// </summary>
        public static CustomVisionAnalyser Instance;

        /// <summary>
        /// Insert your prediction key here
        /// </summary>
        private string predictionKey = "- Insert your key here -";

        /// <summary>
        /// Insert your prediction endpoint here
        /// </summary>
        private string predictionEndpoint = "Insert your prediction endpoint here";

        /// <summary>
        /// Bite array of the image to submit for analysis
        /// </summary>
        [HideInInspector] public byte[] imageBytes;
    ```

    > [!NOTE]
    > Assurez-vous que vous insérez votre **prédiction-clé du Service** dans le **predictionKey** variable et votre **prédiction-point de terminaison** dans le **predictionEndpoint**  variable. Vous avez copié à [le bloc-notes précédemment, dans le chapitre 2, l’étape 14](#chapter-2---training-your-custom-vision-project).

7.  Code pour **Awake()** doit maintenant être ajouté pour initialiser la variable d’Instance :

    ```csharp
        /// <summary>
        /// Initializes this class
        /// </summary>
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            Instance = this;
        }
    ```

8.  Ajouter la coroutine (avec la méthode statique **GetImageAsByteArray()** méthode en dessous), qui obtient les résultats de l’analyse de l’image capturée par le **ImageCapture** classe.

    > [!NOTE]
    > Dans le **AnalyseImageCapture** coroutine, il existe un appel à la **SceneOrganiser** classe que vous êtes encore à créer. Par conséquent, **laisser les lignes commentées pour l’instant**.

    ```csharp    
        /// <summary>
        /// Call the Computer Vision Service to submit the image.
        /// </summary>
        public IEnumerator AnalyseLastImageCaptured(string imagePath)
        {
            Debug.Log("Analyzing...");

            WWWForm webForm = new WWWForm();

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Post(predictionEndpoint, webForm))
            {
                // Gets a byte array out of the saved image
                imageBytes = GetImageAsByteArray(imagePath);

                unityWebRequest.SetRequestHeader("Content-Type", "application/octet-stream");
                unityWebRequest.SetRequestHeader("Prediction-Key", predictionKey);

                // The upload handler will help uploading the byte array with the request
                unityWebRequest.uploadHandler = new UploadHandlerRaw(imageBytes);
                unityWebRequest.uploadHandler.contentType = "application/octet-stream";

                // The download handler will help receiving the analysis from Azure
                unityWebRequest.downloadHandler = new DownloadHandlerBuffer();

                // Send the request
                yield return unityWebRequest.SendWebRequest();

                string jsonResponse = unityWebRequest.downloadHandler.text;

                Debug.Log("response: " + jsonResponse);

                // Create a texture. Texture size does not matter, since
                // LoadImage will replace with the incoming image size.
                //Texture2D tex = new Texture2D(1, 1);
                //tex.LoadImage(imageBytes);
                //SceneOrganiser.Instance.quadRenderer.material.SetTexture("_MainTex", tex);

                // The response will be in JSON format, therefore it needs to be deserialized
                //AnalysisRootObject analysisRootObject = new AnalysisRootObject();
                //analysisRootObject = JsonConvert.DeserializeObject<AnalysisRootObject>(jsonResponse);

                //SceneOrganiser.Instance.FinaliseLabel(analysisRootObject);
            }
        }

        /// <summary>
        /// Returns the contents of the specified image file as a byte array.
        /// </summary>
        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);

            BinaryReader binaryReader = new BinaryReader(fileStream);

            return binaryReader.ReadBytes((int)fileStream.Length);
        }
    ```

9. Supprimer le **Start()** et **Update()** méthodes, car ils ne seront pas utilisés. 

10.  Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.

> [!IMPORTANT]
> Comme mentionné précédemment, ne vous inquiétez pas sur le code qui peut sembler avoir une erreur, comme vous fournit des classes plus rapidement, ce qui résoudra ces.

## <a name="chapter-6---create-the-customvisionobjects-class"></a>Chapitre 6 : créer la classe CustomVisionObjects

La classe que vous allez créer est maintenant le **CustomVisionObjects** classe.

Ce script contient un nombre d’objets utilisés par d’autres classes pour sérialiser et désérialiser les appels effectués vers le Service Vision personnalisée.

Pour créer cette classe :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**. Appeler le script **CustomVisionObjects.**

2.  Double-cliquez sur le nouveau **CustomVisionObjects** script pour l’ouvrir avec **Visual Studio.**

3.  Vérifiez que vous disposez des espaces de noms suivants référencé au début du fichier :

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  Supprimer le **Start()** et **Update()** méthodes à l’intérieur de la **CustomVisionObjects** classe, cette classe doit maintenant être vide.

    > [!WARNING]
    > Il est important que vous suivez la prochaine instruction avec précaution. Si vous placez les déclarations de classe nouvelle à l’intérieur de la **CustomVisionObjects** (classe), vous obtiendrez des erreurs de compilation [chapitre 10](#chapter-10---create-the-imagecapture-class), indiquant que **AnalysisRootObject** et  **BoundingBox** sont introuvables.

5.  Ajoutez les classes suivantes *en dehors de* le **CustomVisionObjects** classe. Ces objets sont utilisés par le **Newtonsoft** bibliothèque pour sérialiser et désérialiser les données de réponse :

    ```csharp
    // The objects contained in this script represent the deserialized version
    // of the objects used by this application 

    /// <summary>
    /// Web request object for image data
    /// </summary>
    class MultipartObject : IMultipartFormSection
    {
        public string sectionName { get; set; }

        public byte[] sectionData { get; set; }

        public string fileName { get; set; }

        public string contentType { get; set; }
    }

    /// <summary>
    /// JSON of all Tags existing within the project
    /// contains the list of Tags
    /// </summary> 
    public class Tags_RootObject
    {
        public List<TagOfProject> Tags { get; set; }
        public int TotalTaggedImages { get; set; }
        public int TotalUntaggedImages { get; set; }
    }

    public class TagOfProject
    {
        public string Id { get; set; }
        public string Name { get; set; }
        public string Description { get; set; }
        public int ImageCount { get; set; }
    }

    /// <summary>
    /// JSON of Tag to associate to an image
    /// Contains a list of hosting the tags,
    /// since multiple tags can be associated with one image
    /// </summary> 
    public class Tag_RootObject
    {
        public List<Tag> Tags { get; set; }
    }

    public class Tag
    {
        public string ImageId { get; set; }
        public string TagId { get; set; }
    }

    /// <summary>
    /// JSON of images submitted
    /// Contains objects that host detailed information about one or more images
    /// </summary> 
    public class ImageRootObject
    {
        public bool IsBatchSuccessful { get; set; }
        public List<SubmittedImage> Images { get; set; }
    }

    public class SubmittedImage
    {
        public string SourceUrl { get; set; }
        public string Status { get; set; }
        public ImageObject Image { get; set; }
    }

    public class ImageObject
    {
        public string Id { get; set; }
        public DateTime Created { get; set; }
        public int Width { get; set; }
        public int Height { get; set; }
        public string ImageUri { get; set; }
        public string ThumbnailUri { get; set; }
    }

    /// <summary>
    /// JSON of Service Iteration
    /// </summary> 
    public class Iteration
    {
        public string Id { get; set; }
        public string Name { get; set; }
        public bool IsDefault { get; set; }
        public string Status { get; set; }
        public string Created { get; set; }
        public string LastModified { get; set; }
        public string TrainedAt { get; set; }
        public string ProjectId { get; set; }
        public bool Exportable { get; set; }
        public string DomainId { get; set; }
    }

    /// <summary>
    /// Predictions received by the Service
    /// after submitting an image for analysis
    /// Includes Bounding Box
    /// </summary>
    public class AnalysisRootObject
    {
        public string id { get; set; }
        public string project { get; set; }
        public string iteration { get; set; }
        public DateTime created { get; set; }
        public List<Prediction> predictions { get; set; }
    }

    public class BoundingBox
    {
        public double left { get; set; }
        public double top { get; set; }
        public double width { get; set; }
        public double height { get; set; }
    }

    public class Prediction
    {
        public double probability { get; set; }
        public string tagId { get; set; }
        public string tagName { get; set; }
        public BoundingBox boundingBox { get; set; }
    }
    ```

6.  Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.

## <a name="chapter-7---create-the-spatialmapping-class"></a>Chapitre 7 - créer la classe SpatialMapping

Cette classe définira le **Collider de mappage Spatial** dans la scène. ainsi, pour être en mesure de détecter les collisions entre des objets virtuels et des objets réels.

Pour créer cette classe :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**. Appeler le script **SpatialMapping.**

2.  Double-cliquez sur le nouveau **SpatialMapping** script pour l’ouvrir avec **Visual Studio.**

3.  Vérifiez que vous disposez des espaces de noms suivants mentionnés ci-dessus le **SpatialMapping** classe :

    ```csharp
    using UnityEngine;
    using UnityEngine.XR.WSA;
    ```

4.  Ensuite, ajoutez les variables suivantes à l’intérieur de la **SpatialMapping** classe ci-dessus le **Start()** méthode :

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static SpatialMapping Instance;

        /// <summary>
        /// Used by the GazeCursor as a property with the Raycast call
        /// </summary>
        internal static int PhysicsRaycastMask;

        /// <summary>
        /// The layer to use for spatial mapping collisions
        /// </summary>
        internal int physicsLayer = 31;

        /// <summary>
        /// Creates environment colliders to work with physics
        /// </summary>
        private SpatialMappingCollider spatialMappingCollider;
    ```

5.  Ajouter le **Awake()** et **Start()**:

    ```csharp
        /// <summary>
        /// Initializes this class
        /// </summary>
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            Instance = this;
        }

        /// <summary>
        /// Runs at initialization right after Awake method
        /// </summary>
        void Start()
        {
            // Initialize and configure the collider
            spatialMappingCollider = gameObject.GetComponent<SpatialMappingCollider>();
            spatialMappingCollider.surfaceParent = this.gameObject;
            spatialMappingCollider.freezeUpdates = false;
            spatialMappingCollider.layer = physicsLayer;

            // define the mask
            PhysicsRaycastMask = 1 << physicsLayer;

            // set the object as active one
            gameObject.SetActive(true);
        }
    ```

6.  Supprimer le **Update()** (méthode).

7.  Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.


## <a name="chapter-8---create-the-gazecursor-class"></a>Chapitre 8 - créer la classe GazeCursor

Cette classe est responsable de la configuration du curseur à l’emplacement approprié dans l’espace réel, en utilisant le **SpatialMappingCollider**, créé dans le chapitre précédent.

Pour créer cette classe :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**. Appeler le script **GazeCursor**

2.  Double-cliquez sur le nouveau **GazeCursor** script pour l’ouvrir avec **Visual Studio.**

3.  Vérifiez que vous disposez de l’espace de noms suivant référencé ci-dessus le **GazeCursor** classe :

    ```csharp
    using UnityEngine;
    ```

4.  Puis ajoutez la variable suivante à l’intérieur de la **GazeCursor** de classe, au-dessus du **Start()** (méthode). 

    ```csharp
        /// <summary>
        /// The cursor (this object) mesh renderer
        /// </summary>
        private MeshRenderer meshRenderer;
    ```

5.  Mise à jour le **Start()** méthode avec le code suivant :

    ```csharp
        /// <summary>
        /// Runs at initialization right after the Awake method
        /// </summary>
        void Start()
        {
            // Grab the mesh renderer that is on the same object as this script.
            meshRenderer = gameObject.GetComponent<MeshRenderer>();

            // Set the cursor reference
            SceneOrganiser.Instance.cursor = gameObject;
            gameObject.GetComponent<Renderer>().material.color = Color.green;

            // If you wish to change the size of the cursor you can do so here
            gameObject.transform.localScale = new Vector3(0.01f, 0.01f, 0.01f);
        }
    ```

6.  Mise à jour le **Update()** méthode avec le code suivant :

    ```csharp
        /// <summary>
        /// Update is called once per frame
        /// </summary>
        void Update()
        {
            // Do a raycast into the world based on the user's head position and orientation.
            Vector3 headPosition = Camera.main.transform.position;
            Vector3 gazeDirection = Camera.main.transform.forward;

            RaycastHit gazeHitInfo;
            if (Physics.Raycast(headPosition, gazeDirection, out gazeHitInfo, 30.0f, SpatialMapping.PhysicsRaycastMask))
            {
                // If the raycast hit a hologram, display the cursor mesh.
                meshRenderer.enabled = true;
                // Move the cursor to the point where the raycast hit.
                transform.position = gazeHitInfo.point;
                // Rotate the cursor to hug the surface of the hologram.
                transform.rotation = Quaternion.FromToRotation(Vector3.up, gazeHitInfo.normal);
            }
            else
            {
                // If the raycast did not hit a hologram, hide the cursor mesh.
                meshRenderer.enabled = false;
            }
        }
    ```

    > [!NOTE]
    > Ne vous inquiétez pas sur l’erreur pour le **SceneOrganiser** classe introuvable, vous allez le créer dans le chapitre suivant.

7. Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.

## <a name="chapter-9---create-the-sceneorganiser-class"></a>Chapitre 9 - créer la classe SceneOrganiser

Cette classe sera :

-   Configurer le *Main Camera* en joignant les composants appropriés à ce dernier.

-   Lorsqu’un objet est détecté, il sera responsable du calcul de sa position dans le monde réel et place un **étiquette** près d’avec le bon **nom de balise**.    

Pour créer cette classe :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**. Nommez le script **SceneOrganiser**.

2.  Double-cliquez sur le nouveau **SceneOrganiser** script pour l’ouvrir avec **Visual Studio.**

3.  Vérifiez que vous disposez des espaces de noms suivants mentionnés ci-dessus le **SceneOrganiser** classe :

    ```csharp
    using System.Collections.Generic;
    using System.Linq;
    using UnityEngine;
    ```

4.  Puis ajoutez les variables suivantes à l’intérieur de la **SceneOrganiser** classe ci-dessus le **Start()** méthode :

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static SceneOrganiser Instance;

        /// <summary>
        /// The cursor object attached to the Main Camera
        /// </summary>
        internal GameObject cursor;

        /// <summary>
        /// The label used to display the analysis on the objects in the real world
        /// </summary>
        public GameObject label;

        /// <summary>
        /// Reference to the last Label positioned
        /// </summary>
        internal Transform lastLabelPlaced;

        /// <summary>
        /// Reference to the last Label positioned
        /// </summary>
        internal TextMesh lastLabelPlacedText;

        /// <summary>
        /// Current threshold accepted for displaying the label
        /// Reduce this value to display the recognition more often
        /// </summary>
        internal float probabilityThreshold = 0.8f;

        /// <summary>
        /// The quad object hosting the imposed image captured
        /// </summary>
        private GameObject quad;

        /// <summary>
        /// Renderer of the quad object
        /// </summary>
        internal Renderer quadRenderer;
    ```

5.  Supprimer le **Start()** et **Update()** méthodes.

6.  Sous les variables, ajoutez le **Awake()** (méthode), qui initialisent la classe et configurer la scène.

    ```csharp
        /// <summary>
        /// Called on initialization
        /// </summary>
        private void Awake()
        {
            // Use this class instance as singleton
            Instance = this;

            // Add the ImageCapture class to this Gameobject
            gameObject.AddComponent<ImageCapture>();

            // Add the CustomVisionAnalyser class to this Gameobject
            gameObject.AddComponent<CustomVisionAnalyser>();

            // Add the CustomVisionObjects class to this Gameobject
            gameObject.AddComponent<CustomVisionObjects>();
        }
    ```

7.  Ajouter le **PlaceAnalysisLabel()** (méthode), qui sera *instancier* l’étiquette dans la scène (qui est à ce stade invisible à l’utilisateur). Il place également les quatre cœurs (également invisibles) où l’image est placée et se chevauche avec le monde réel. Ceci est important, car les coordonnées de la zone est récupéré à partir du Service après l’analyse sont remonter dans cette quadruple déterminé l’emplacement approximatif de l’objet dans le monde réel. 

    ```csharp
        /// <summary>
        /// Instantiate a Label in the appropriate location relative to the Main Camera.
        /// </summary>
        public void PlaceAnalysisLabel()
        {
            lastLabelPlaced = Instantiate(label.transform, cursor.transform.position, transform.rotation);
            lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();
            lastLabelPlacedText.text = "";
            lastLabelPlaced.transform.localScale = new Vector3(0.005f,0.005f,0.005f);

            // Create a GameObject to which the texture can be applied
            quad = GameObject.CreatePrimitive(PrimitiveType.Quad);
            quadRenderer = quad.GetComponent<Renderer>() as Renderer;
            Material m = new Material(Shader.Find("Legacy Shaders/Transparent/Diffuse"));
            quadRenderer.material = m;

            // Here you can set the transparency of the quad. Useful for debugging
            float transparency = 0f;
            quadRenderer.material.color = new Color(1, 1, 1, transparency);

            // Set the position and scale of the quad depending on user position
            quad.transform.parent = transform;
            quad.transform.rotation = transform.rotation;

            // The quad is positioned slightly forward in font of the user
            quad.transform.localPosition = new Vector3(0.0f, 0.0f, 3.0f);

            // The quad scale as been set with the following value following experimentation,  
            // to allow the image on the quad to be as precisely imposed to the real world as possible
            quad.transform.localScale = new Vector3(3f, 1.65f, 1f);
            quad.transform.parent = null;
        }
    ```

8.  Ajouter le **FinaliseLabel()** (méthode). Il est chargé de :

    *   Définition de la *étiquette* texte avec le *balise* de la prédiction en toute confiance le plus élevé.
    *   Le calcul de l’appel le *le rectangle englobant* sur l’objet processeur quadruple, positionné précédemment et la placer l’étiquette dans la scène.
    *   Ajustement de la profondeur de l’étiquette à l’aide d’un Raycast vers le *le rectangle englobant*, qui doit entrer en conflit par rapport à l’objet dans le monde réel.
    * Réinitialiser le processus de capture pour autoriser l’utilisateur à capturer une autre image.

    ```csharp
        /// <summary>
        /// Set the Tags as Text of the last label created. 
        /// </summary>
        public void FinaliseLabel(AnalysisRootObject analysisObject)
        {
            if (analysisObject.predictions != null)
            {
                lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();
                // Sort the predictions to locate the highest one
                List<Prediction> sortedPredictions = new List<Prediction>();
                sortedPredictions = analysisObject.predictions.OrderBy(p => p.probability).ToList();
                Prediction bestPrediction = new Prediction();
                bestPrediction = sortedPredictions[sortedPredictions.Count - 1];

                if (bestPrediction.probability > probabilityThreshold)
                {
                    quadRenderer = quad.GetComponent<Renderer>() as Renderer;
                    Bounds quadBounds = quadRenderer.bounds;

                    // Position the label as close as possible to the Bounding Box of the prediction 
                    // At this point it will not consider depth
                    lastLabelPlaced.transform.parent = quad.transform;
                    lastLabelPlaced.transform.localPosition = CalculateBoundingBoxPosition(quadBounds, bestPrediction.boundingBox);

                    // Set the tag text
                    lastLabelPlacedText.text = bestPrediction.tagName;

                    // Cast a ray from the user's head to the currently placed label, it should hit the object detected by the Service.
                    // At that point it will reposition the label where the ray HL sensor collides with the object,
                    // (using the HL spatial tracking)
                    Debug.Log("Repositioning Label");
                    Vector3 headPosition = Camera.main.transform.position;
                    RaycastHit objHitInfo;
                    Vector3 objDirection = lastLabelPlaced.position;
                    if (Physics.Raycast(headPosition, objDirection, out objHitInfo, 30.0f,   SpatialMapping.PhysicsRaycastMask))
                    {
                        lastLabelPlaced.position = objHitInfo.point;
                    }
                }
            }
            // Reset the color of the cursor
            cursor.GetComponent<Renderer>().material.color = Color.green;

            // Stop the analysis process
            ImageCapture.Instance.ResetImageCapture();        
        }
    ```

9.  Ajouter le **CalculateBoundingBoxPosition()** (méthode), qui héberge un nombre de calculs nécessaires pour traduire le *le rectangle englobant* coordonnées extraites du Service et les recréer proportionnellement sur les quatre cœurs.

    ```csharp
        /// <summary>
        /// This method hosts a series of calculations to determine the position 
        /// of the Bounding Box on the quad created in the real world
        /// by using the Bounding Box received back alongside the Best Prediction
        /// </summary>
        public Vector3 CalculateBoundingBoxPosition(Bounds b, BoundingBox boundingBox)
        {
            Debug.Log($"BB: left {boundingBox.left}, top {boundingBox.top}, width {boundingBox.width}, height {boundingBox.height}");

            double centerFromLeft = boundingBox.left + (boundingBox.width / 2);
            double centerFromTop = boundingBox.top + (boundingBox.height / 2);
            Debug.Log($"BB CenterFromLeft {centerFromLeft}, CenterFromTop {centerFromTop}");

            double quadWidth = b.size.normalized.x;
            double quadHeight = b.size.normalized.y;
            Debug.Log($"Quad Width {b.size.normalized.x}, Quad Height {b.size.normalized.y}");

            double normalisedPos_X = (quadWidth * centerFromLeft) - (quadWidth/2);
            double normalisedPos_Y = (quadHeight * centerFromTop) - (quadHeight/2);

            return new Vector3((float)normalisedPos_X, (float)normalisedPos_Y, 0);
        }
    ```

10. Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.

    > [!IMPORTANT]
    > Avant de continuer, ouvrez le **CustomVisionAnalyser** (classe) et dans le **AnalyseLastImageCaptured()** (méthode), *Décommentez* les lignes suivantes :
    >
    >   ```csharp
    >   // Create a texture. Texture size does not matter, since 
    >   // LoadImage will replace with the incoming image size.
    >   Texture2D tex = new Texture2D(1, 1);
    >   tex.LoadImage(imageBytes);
    >   SceneOrganiser.Instance.quadRenderer.material.SetTexture("_MainTex", tex);
    >
    >   // The response will be in JSON format, therefore it needs to be deserialized
    >   AnalysisRootObject analysisRootObject = new AnalysisRootObject();
    >   analysisRootObject = JsonConvert.DeserializeObject<AnalysisRootObject>(jsonResponse);
    >
    >   SceneOrganiser.Instance.FinaliseLabel(analysisRootObject);
    >   ```

> [!NOTE]
> Ne vous inquiétez pas sur le **ImageCapture** classe message « est introuvable », vous allez le créer dans le chapitre suivant.


## <a name="chapter-10---create-the-imagecapture-class"></a>Chapitre 10 - créer la classe ImageCapture

La classe suivante, vous allez créer est la **ImageCapture** classe.

Cette classe est chargée de :

*   Capture d’une image à l’aide de l’appareil photo HoloLens et en le stockant dans le *application* dossier.
*   Gestion des *appuyez sur* mouvements de l’utilisateur.

Pour créer cette classe :

1.  Accédez à la **Scripts** dossier que vous avez créé précédemment.

2.  Avec le bouton droit dans le dossier, puis cliquez sur **créer** > **C\# Script**. Nommez le script **ImageCapture**.

3.  Double-cliquez sur le nouveau **ImageCapture** script pour l’ouvrir avec **Visual Studio.**

4.  Remplacez les espaces de noms en haut du fichier avec les éléments suivants :

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    using UnityEngine.XR.WSA.WebCam;
    ```

5.  Puis ajoutez les variables suivantes à l’intérieur de la **ImageCapture** classe ci-dessus le **Start()** méthode :

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static ImageCapture Instance;

        /// <summary>
        /// Keep counts of the taps for image renaming
        /// </summary>
        private int captureCount = 0;

        /// <summary>
        /// Photo Capture object
        /// </summary>
        private PhotoCapture photoCaptureObject = null;

        /// <summary>
        /// Allows gestures recognition in HoloLens
        /// </summary>
        private GestureRecognizer recognizer;

        /// <summary>
        /// Flagging if the capture loop is running
        /// </summary>
        internal bool captureIsActive;
        
        /// <summary>
        /// File path of current analysed photo
        /// </summary>
        internal string filePath = string.Empty;
    ```

6.  Code pour **Awake()** et **Start()** méthodes doit maintenant être ajouté :

    ```csharp
        /// <summary>
        /// Called on initialization
        /// </summary>
        private void Awake()
        {
            Instance = this;
        }

        /// <summary>
        /// Runs at initialization right after Awake method
        /// </summary>
        void Start()
        {
            // Clean up the LocalState folder of this application from all photos stored
            DirectoryInfo info = new DirectoryInfo(Application.persistentDataPath);
            var fileInfo = info.GetFiles();
            foreach (var file in fileInfo)
            {
                try
                {
                    file.Delete();
                }
                catch (Exception)
                {
                    Debug.LogFormat("Cannot delete file: ", file.Name);
                }
            } 

            // Subscribing to the Microsoft HoloLens API gesture recognizer to track user gestures
            recognizer = new GestureRecognizer();
            recognizer.SetRecognizableGestures(GestureSettings.Tap);
            recognizer.Tapped += TapHandler;
            recognizer.StartCapturingGestures();
        }
    ```

7.  Implémenter un gestionnaire qui sera appelé lorsqu’une action d’appuyer se produit :

    ```csharp
        /// <summary>
        /// Respond to Tap Input.
        /// </summary>
        private void TapHandler(TappedEventArgs obj)
        {
            if (!captureIsActive)
            {
                captureIsActive = true;

                // Set the cursor color to red
                SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.red;

                // Begin the capture loop
                Invoke("ExecuteImageCaptureAndAnalysis", 0);
            }
        }
    ```

    > [!IMPORTANT]
    > Lorsque le curseur se trouve **vert**, cela signifie que l’appareil photo est disponible pour la prise de l’image. Lorsque le curseur se trouve **rouge**, cela signifie que l’appareil photo est occupé.

8.  Ajoutez la méthode que l’application utilise pour démarrer le processus de capture d’image et de stocker l’image :

    ```csharp
        /// <summary>
        /// Begin process of image capturing and send to Azure Custom Vision Service.
        /// </summary>
        private void ExecuteImageCaptureAndAnalysis()
        {
            // Create a label in world space using the ResultsLabel class 
            // Invisible at this point but correctly positioned where the image was taken
            SceneOrganiser.Instance.PlaceAnalysisLabel();

            // Set the camera resolution to be the highest possible
            Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending
                ((res) => res.width * res.height).First();
            Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);

            // Begin capture process, set the image format
            PhotoCapture.CreateAsync(true, delegate (PhotoCapture captureObject)
            {
                photoCaptureObject = captureObject;

                CameraParameters camParameters = new CameraParameters
                {
                    hologramOpacity = 1.0f,
                    cameraResolutionWidth = targetTexture.width,
                    cameraResolutionHeight = targetTexture.height,
                    pixelFormat = CapturePixelFormat.BGRA32
                };

                // Capture the image from the camera and save it in the App internal folder
                captureObject.StartPhotoModeAsync(camParameters, delegate (PhotoCapture.PhotoCaptureResult result)
                {
                    string filename = string.Format(@"CapturedImage{0}.jpg", captureCount);
                    filePath = Path.Combine(Application.persistentDataPath, filename);          
                    captureCount++;              
                    photoCaptureObject.TakePhotoAsync(filePath, PhotoCaptureFileOutputFormat.JPG, OnCapturedPhotoToDisk);              
                });
            });
        }
    ```

9.  Ajoutez les gestionnaires qui seront appelées lorsque la photo a été capturée et quand il est prêt à être analysés. Le résultat est ensuite transmis à la **CustomVisionAnalyser** pour l’analyse.

    ```csharp
        /// <summary>
        /// Register the full execution of the Photo Capture. 
        /// </summary>
        void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
        {
            try
            {
                // Call StopPhotoMode once the image has successfully captured
                photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
            }
            catch (Exception e)
            {
                Debug.LogFormat("Exception capturing photo to disk: {0}", e.Message);
            }
        }

        /// <summary>
        /// The camera photo mode has stopped after the capture.
        /// Begin the image analysis process.
        /// </summary>
        void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
        {
            Debug.LogFormat("Stopped Photo Mode");
        
            // Dispose from the object in memory and request the image analysis 
            photoCaptureObject.Dispose();
            photoCaptureObject = null;

            // Call the image analysis
            StartCoroutine(CustomVisionAnalyser.Instance.AnalyseLastImageCaptured(filePath)); 
        }

        /// <summary>
        /// Stops all capture pending actions
        /// </summary>
        internal void ResetImageCapture()
        {
            captureIsActive = false;

            // Set the cursor color to green
            SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.green;

            // Stop the capture loop if active
            CancelInvoke();
        }
    ```

10. Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.

## <a name="chapter-11---setting-up-the-scripts-in-the-scene"></a>Chapitre 11 - configurer les scripts dans la scène

Maintenant que vous avez écrit tout le code nécessaire pour ce projet, est le temps pour configurer les scripts dans la scène et sur les prefabs, pour qu’ils se comportent correctement.

1.  Dans le **éditeur Unity**, dans le **hiérarchie panneau**, sélectionnez le **Main Camera**.
2.  Dans le **panneau Inspecteur**, avec le **Main Camera** sélectionné, cliquez sur **ajouter un composant**, puis recherchez **SceneOrganiser** script et Double-cliquez sur pour l’ajouter.

    ![](images/AzureLabs-Lab310-38.png)

3.  Dans le **panneau projet**, ouvrez le **dossier Prefabs**, faites glisser le **étiquette** prefab dans le *étiquette* zone, d’entrée cible de référence vide dans le **SceneOrganiser** script que vous venez d’ajouter à la *Main Camera*, comme illustré dans l’image ci-dessous :

    ![](images/AzureLabs-Lab310-39.png)

4.  Dans le **hiérarchie panneau**, sélectionnez le **GazeCursor** enfant de la **Main Camera**.
5.  Dans le **panneau Inspecteur**, avec le **GazeCursor** sélectionné, cliquez sur **ajouter un composant**, puis recherchez **GazeCursor** script et Double-cliquez sur pour l’ajouter.

    ![](images/AzureLabs-Lab310-40.png)

6.  Là encore, dans le **hiérarchie panneau**, sélectionnez le **SpatialMapping** enfant de la **Main Camera**.
7.  Dans le **panneau Inspecteur**, avec le **SpatialMapping** sélectionné, cliquez sur **ajouter un composant**, puis recherchez **SpatialMapping** script et le double-clic, pour l’ajouter.

    ![](images/AzureLabs-Lab310-41.png)

Les scripts restants que vous n’ont pas jeu est ajouté par le code dans le **SceneOrganiser** script, pendant l’exécution.

## <a name="chapter-12---before-building"></a>Chapitre 12 - avant la génération

Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre Microsoft HoloLens.

Avant de procéder, assurez-vous que :

-  Tous les paramètres mentionnés dans le [chapitre 3](#chapter-3---set-up-the-unity-project) sont correctement définies.
- Le script **SceneOrganiser** est attaché à la **Main Camera** objet.
- Le script **GazeCursor** est attaché à la **GazeCursor** objet.
- Le script **SpatialMapping** est attaché à la **SpatialMapping** objet.
- Dans [chapitre 5](#chapter-5---create-the-customvisionanalyser-class), étape 6 :

    - Assurez-vous que vous insérez votre **Service prédiction clé** dans le **predictionKey** variable.
    - Vous avez inséré votre **point de terminaison de prédiction** dans le **predictionEndpoint** classe.

## <a name="chapter-13---build-the-uwp-solution-and-sideload-your-application"></a>Chapitre 13 - générez la solution UWP et le chargement de version test, votre application

Vous êtes maintenant prêt à créer votre application en tant que UWP Solution auxquelles vous serez en mesure de déployer une session sur le Microsoft HoloLens. Pour commencer le processus de génération :

1.  Accédez à **fichier > Paramètres de Build**.

2.  Graduation **Unity C\# projets**.

3.  Cliquez sur **ajouter des scènes Open**. Cette opération ajoute la scène actuellement ouverte à la build.

    ![](images/AzureLabs-Lab310-42.png)

4.  Cliquez sur **Build**. Unity lancera un *Explorateur de fichiers* fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans. Créez ce dossier, puis nommez-le **application**. Ensuite avec le **application** dossier sélectionné, cliquez sur **sélectionner le dossier**.

5.  Unity commencera à générer votre projet pour le **application** dossier.

6.  Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).

7.  Pour déployer une session sur Microsoft HoloLens, vous devez l’adresse IP de cet appareil (pour les déployer à distance) et pour vous assurer qu’elle également a **Mode développeur** définie. Pour ce faire :

    1.  Tout en portant vos HoloLens, ouvrez le **paramètres**.

    2.  Accédez à **réseau & Internet** > **Wi-Fi** > **les Options avancées**

    3.  Remarque la **IPv4** adresse.

    4.  Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité** > **pour les développeurs**

    5.  Définissez **Mode développeur** *sur*.

8.  Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.

9.  Dans, sélectionnez la Configuration de Solution **déboguer**.

10. Dans la plateforme de Solution, sélectionnez **x86, ordinateur distant**. Vous devrez insérer le **adresse IP** d’un appareil distant (le Microsoft HoloLens, dans ce cas, que vous avez notée).

    ![](images/AzureLabs-Lab310-43.png)

11. Accédez à la **Build** menu et cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre HoloLens.

12. Votre application doit maintenant apparaître dans la liste des applications installées sur votre Microsoft HoloLens, prêt à être lancé !

### <a name="to-use-the-application"></a>Pour utiliser l’application :

* Examiner un objet, vous avez formé avec votre **Azure Custom Vision Service, la détection d’objets**et utiliser le **mouvement d’appui**.
* Si l’objet est détecté, un espace universel *texte de l’étiquette* s’affiche avec le nom de balise.

> [!IMPORTANT]
> Chaque fois que vous capturez une photo et l’envoyez au Service, vous pouvez revenir à la page du Service et reformer le Service avec les images qui vient d’être capturées. Au début, vous allez probablement également être amené à corriger le *englobants* pour être plus précis et de reformer le Service.

> [!NOTE]
> Le texte d’étiquette placée peuvent ne pas apparaître près de l’objet quand les capteurs Microsoft HoloLens et/ou le SpatialTrackingComponent dans Unity ne parvient pas à placer les colliders appropriés, par rapport aux objets du monde réel. Essayez d’utiliser l’application sur une surface différente si tel est le cas.

## <a name="your-custom-vision-object-detection-application"></a>Votre Vision personnalisée, application de détection d’objets

Félicitations, vous avez créé une application de réalité mixte qui tire parti de la Vision personnalisée Azure, API de détection de l’objet, qui peut reconnaître un objet à partir d’une image, puis indiquent une position approximative pour cet objet dans l’espace 3D.

![](images/AzureLabs-Lab310-00.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Ajout à l’étiquette de texte, utilisez un cube semi-transparent pour encapsuler l’objet réel dans une 3D *le rectangle englobant*.

### <a name="exercise-2"></a>Exercice 2

Formez votre Service de Vision personnalisée pour reconnaître des objets plus.

### <a name="exercise-3"></a>Exercice 3

Un signal sonore lorsqu’un objet est reconnu.

### <a name="exercise-4"></a>Exercice 4

Utiliser l’API pour recalculer votre Service avec les mêmes images de l’analyse de votre application, par conséquent, pour rendre le Service plus précis (effectuer la prédiction et la formation simultanément).
