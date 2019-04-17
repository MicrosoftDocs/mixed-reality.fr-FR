---
title: MR et 302b Azure - vision personnalisée
description: Terminer ce cours pour apprendre à former un modèle d’apprentissage et ensuite utiliser le modèle formé pour reconnaître des objets similaires au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/03/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, vision personnalisée, hololens, immersives, vr
ms.openlocfilehash: e6e9782a8d559af660dc4765556f1e926c5360b1
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594226"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-and-azure-302b-custom-vision"></a>MR et 302b Azure : Vision personnalisée

Dans ce cours, vous allez apprendre à reconnaître un contenu visuel personnalisé au sein d’une image fournie, à l’aide des fonctionnalités de Vision personnalisée d’Azure dans une application de réalité mixte.

Ce service vous permettra de former un modèle d’apprentissage automatique à l’aide d’images de l’objet. Vous utiliserez ensuite le modèle formé pour reconnaître des objets semblables, tel que fourni par la capture de l’appareil photo de Microsoft HoloLens ou un appareil photo connecté à votre PC pour des casques IMMERSIFS (VR).

![résultat de cours](images/AzureLabs-Lab302b-00.png)

Vision personnalisée Azure est un Service COGNITIF de Microsoft qui permet aux développeurs de créer des classifieurs de l’image personnalisée. Ces classifieurs peuvent ensuite être utilisées avec les nouvelles images pour reconnaître ou classement, d’objets au sein de cette nouvelle image. Le Service fournit un portail en ligne simple et facile à utiliser, pour simplifier le processus. Pour plus d’informations, visitez le [page de Azure Custom Vision Service](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home).

À la fin de ce cours, vous disposez d’une application de réalité mixte qui sera en mesure de fonctionner dans deux modes :

-   **Mode d’analyse**: configurer le Service Vision personnalisée manuellement par le téléchargement d’images, création de balises et le Service de formation pour reconnaître des différents objets (dans ce cas de la souris et du clavier). Vous allez ensuite créer une application de HoloLens qui capture des images à l’aide de l’appareil photo, puis réessayer d’identifier ces objets dans le monde réel.

-   **Mode d’apprentissage**: vous implémentez le code qui permettra un « Mode de formation » dans votre application. Le mode d’apprentissage vous permettra de capturer des images à l’aide de la caméra des HoloLens, charger les images capturées dans le Service et former le modèle de vision personnalisée.

Ce cours va vous apprendre à obtenir les résultats à partir du Service de Vision personnalisée dans une application basée sur Unity. Il le sera jusqu'à vous permettent d’appliquer ces concepts à une application personnalisée, que vous voudrez peut-être générer.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et 302b Azure : Vision personnalisée</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Si ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques Windows Mixed Reality IMMERSIFS (VR). Étant donné que des casques IMMERSIFS (VR) ne sont pas accessibles caméras, vous devez une caméra externe connectée à votre PC. Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge des casques IMMERSIFS (VR).

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.

Nous recommandons le matériel et logiciel pour ce cours suivants :

- Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)
- [Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé](install-the-tools.md#installation-checklist)
- [Le SDK Windows 10 dernières](install-the-tools.md#installation-checklist)
- [Unity 2017.4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé
- Un appareil photo connecté à votre PC (pour le développement de casque immersives)
- Accès à Internet pour le programme d’installation Azure et l’extraction de l’API de Vision personnalisée
- Une série d’au moins cinq (5) images (dix (10) recommandé) pour chaque objet que vous souhaitez que le Service Vision personnalisée pour reconnaître. Si vous le souhaitez, vous pouvez utiliser [les images déjà fournis avec ce cours (une souris et un clavier) ](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).
2.  Configurer et tester votre HoloLens. Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur). 

Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1---the-custom-vision-service-portal"></a>Chapitre 1 : le portail de Service Vision personnalisée

Pour utiliser le *Service Vision personnalisée* dans Azure, vous devez configurer une instance du Service à être mis à disposition de votre application.

1.  Tout d’abord, [accédez à la *Service Vision personnalisée* page principale](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).

2.  Cliquez sur le **prise en main** bouton.

    ![](images/AzureLabs-Lab302b-01.png)

3.  Se connecter à la *Service Vision personnalisée* portail.

    ![](images/AzureLabs-Lab302b-02.png)

    > [!NOTE]
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

4.  Une fois que vous êtes connecté pour la première fois, vous serez invité au *termes du contrat de Service* Panneau de configuration. Cliquez sur la case à cocher pour accepter les termes du contrat. Cliquez ensuite sur **J’accepte**.

    ![](images/AzureLabs-Lab302b-03.png)

5.  Ayant accepté les termes du contrat, vous serez redirigé vers le *projets* section du portail. Cliquez sur **nouveau projet**.

    ![](images/AzureLabs-Lab302b-04.png)

6.  Un onglet s’affiche sur le côté droit, qui vous invite à spécifier des champs pour le projet.

    1.  Insérer un *nom* pour votre projet.

    2.  Insérer un *Description* pour votre projet (*facultatif*).

    3.  Choisissez un *groupe de ressources* ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).

    4. Définir le *Types de projets* à **Classification**
    
    5. Définir le *domaines* comme **général**.

        ![](images/AzureLabs-Lab302b-05.png)

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

7.  Une fois que vous avez terminé, cliquez sur **créer un projet**, vous serez redirigé vers le Service Vision personnalisée, page du projet.

## <a name="chapter-2---training-your-custom-vision-project"></a>Chapitre 2 - formation de votre projet de Vision personnalisée

Une fois dans le portail de Vision personnalisée, votre objectif principal est pour l’apprentissage de votre projet pour reconnaître des objets spécifiques dans des images. Vous avez besoin d’au moins cinq (5) les images, même si dix (10) est recommandée, pour chaque objet que vous souhaitez que votre application à reconnaître. [Vous pouvez utiliser les images fournies avec ce cours (une souris et un clavier)](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip). 

Pour l’apprentissage de votre projet de Service Vision personnalisée :

1.  Cliquez sur le **+** situé en regard **balises.**

    ![](images/AzureLabs-Lab302b-06.png)

2.  Ajouter le **nom** de l’objet à reconnaître. Cliquez sur **enregistrer**.

    ![](images/AzureLabs-Lab302b-07.png)

3.  Vous remarquerez votre **balise** a été ajouté (vous devrez peut-être recharger votre page pour qu’il apparaisse). Cliquez sur la case à cocher à côté de votre nouvelle balise, si elle n’est pas activée.

    ![](images/AzureLabs-Lab302b-08.png)

4.  Cliquez sur **ajouter des Images** dans le centre de la page.

    ![](images/AzureLabs-Lab302b-09.png)

5.  Cliquez sur **parcourir les fichiers locaux**, rechercher, puis sélectionnez, les images que vous voulez charger, le minimum étant cinq (5). N’oubliez pas que toutes ces images doivent contenir l’objet qui sont de formation.

    > [!NOTE]
    >  Vous pouvez sélectionner plusieurs images à la fois, à télécharger.

6.  Une fois que vous pouvez afficher les images dans l’onglet, sélectionnez la balise appropriée dans le **Mes balises** boîte.

    ![](images/AzureLabs-Lab302b-10.png)

7.  Cliquez sur **charger des fichiers**. Les fichiers de lancer le chargement. Une fois que vous avez la confirmation du téléchargement, cliquez sur **fait**.

    ![](images/AzureLabs-Lab302b-11.png)

8.  Répétez ce processus pour créer un nouveau **balise** nommé **clavier** et télécharger les photos appropriées pour celui-ci. Veillez à **Décochez** *souris* une fois que vous avez créé les nouvelles balises, par conséquent, pour afficher le *ajouter des images* fenêtre.

9.  Une fois que vous avez les deux balises à configurer, cliquez sur **Train**, et la première itération d’entraînement commencera la génération.

    ![](images/AzureLabs-Lab302b-12.png)

10. Une fois qu’il est créé, vous serez en mesure de voir les deux boutons nommés **par défaut** et **prédiction URL**. Cliquez sur **par défaut** tout d’abord, puis cliquez sur **prédiction URL**.

    ![](images/AzureLabs-Lab302b-13.png)

    > [!NOTE] 
    > L’URL de point de terminaison qui est fourni à partir de ce problème, selon ce qui a *itération* a été marquée comme valeur par défaut. Par conséquent, si vous apportez ultérieurement un nouveau *itération* et mettez-le à jour comme valeur par défaut, vous ne devez pas modifier votre code.

11. Une fois que vous avez cliqué sur *prédiction URL*, ouvrez *le bloc-notes*, puis copiez et collez le **URL** et **prédiction-clé**, de sorte que vous pouvez récupérer lorsque vous en avez besoin plus loin dans le code.

    ![](images/AzureLabs-Lab302b-14.png)

12. Cliquez sur le **représentant une roue dentée** dans la partie supérieure droite de l’écran.

    ![](images/AzureLabs-Lab302b-15.png)

13. Copie le **formation clé** et collez-la dans un *le bloc-notes*, pour une utilisation ultérieure.

    ![](images/AzureLabs-Lab302b-16.png)

14. Copiez également votre **Id de projet**et également le coller dans votre *le bloc-notes* fichier, pour une utilisation ultérieure.

    ![](images/AzureLabs-Lab302b-16a.png)

## <a name="chapter-3---set-up-the-unity-project"></a>Chapitre 3 - configurer le projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **New**.

    ![](images/AzureLabs-Lab302b-17.png)

2.  Maintenant, vous devez fournir un nom de projet Unity. Insérer **AzureCustomVision.** Assurez-vous que le modèle de projet est défini sur **3D**. Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![](images/AzureLabs-Lab302b-18.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **modifier* > *préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![](images/AzureLabs-Lab302b-19.png)

4.  Ensuite, accédez à **fichier > Paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation** bouton pour appliquer votre sélection.

    ![](images/AzureLabs-Lab302b-20.png)

5.  Lorsque vous êtes toujours dans **fichier > Paramètres de Build** et vous assurer que :

    1.  **Équipement cible** a la valeur **Hololens**

        > Pour des casques IMMERSIFS, définissez **appareil cible** à *n’importe quel appareil*.
        
    2.  **Type de build** a la valeur **D3D**
    3.  **Kit de développement logiciel** a la valeur **dernière installé**
    4.  **Version de Visual Studio** a la valeur **dernière installé**
    5.  **Générez et exécutez** est défini sur **ordinateur Local**
    6.  Enregistrer la scène et l’ajouter à la build. 

        1. Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.

            ![](images/AzureLabs-Lab302b-21.png)

        2. Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![](images/AzureLabs-Lab302b-22.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier :* champ de texte, tapez **CustomVisionScene**, puis cliquez sur **enregistrer**.

            ![](images/AzureLabs-Lab302b-23.png)

            > N’oubliez pas, vous devez enregistrer vos séquences de Unity dans le *actifs* dossier, car ils doivent être associées au projet Unity. Création du dossier de scènes (et autres dossiers similaire) est un moyen classique de structurer un projet Unity.
            
    7.  Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.

        ![](images/AzureLabs-Lab302b-24.png)

6.  Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.

7. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1.  Dans le **autres paramètres** onglet :

        1.  **Version du Runtime de script** doit être **expérimental (équivalent .NET 4.6)**, ce qui déclenchera une nécessité de redémarrer l’éditeur.

        2. **Script principal** doit être **.NET**

        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**

        ![](images/AzureLabs-Lab302b-25.png)

    2.  Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        1. **InternetClient**

        2.  **Webcam**

        3. **Microphone**

        ![](images/AzureLabs-Lab302b-26.png)

    3.  Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.

    ![](images/AzureLabs-Lab302b-27.png)

8.  Dans *paramètres de Build* *Unity C\# projets* est n’est plus grisée ; Cochez la case à cocher en regard de cela.

9.  Fermez la fenêtre Paramètres de Build.

10.  Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).


## <a name="chapter-4---importing-the-newtonsoft-dll-in-unity"></a>Chapitre 4 - Importation de la DLL Newtonsoft dans Unity

> [!IMPORTANT]
> Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [Azure-MR-302b.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/Azure-MR-302b.unitypackage), importez-le dans votre projet en tant qu’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 6](#chapter-6---create-the-customvisionanalyser-class).

Ce cours nécessite l’utilisation de la **Newtonsoft** bibliothèque que vous pouvez ajouter en tant que DLL à vos ressources. Le package contenant [cette bibliothèque peut être téléchargée à partir de ce lien](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/NewtonsoftDLL.unitypackage).
Pour importer la bibliothèque Newtonsoft dans votre projet, utilisez le Package Unity qui accompagne ce cours.

1.  Ajouter le *.unitypackage* à Unity à l’aide de la **actifs* > *importation* *Package*  >  *Personnalisé* *Package** option de menu.

2.  Dans le **importer un Package Unity** emballer qui apparaît, vérifiez tous les éléments sous (y compris) **plug-ins** est sélectionné.

    ![](images/AzureLabs-Lab302b-28.png)

3.  Cliquez sur le **importation** pour ajouter les éléments à votre projet.

4.  Accédez à la **Newtonsoft** dossier sous **plug-ins** dans la vue du projet, puis sélectionnez le *plug-in de Newtonsoft.Json*.

    ![](images/AzureLabs-Lab302b-29.png)

5.  Avec le *plug-in de Newtonsoft.Json* sélectionnée, vérifiez que **plateforme Any** est **unchecked**, puis assurez-vous que **WSAPlayer** est également **unchecked**, puis cliquez sur **appliquer**. Il s’agit juste pour confirmer que les fichiers sont correctement configurés.

    ![](images/AzureLabs-Lab302b-30.png)

    > [!NOTE]
    > Marquage de ces plug-ins les configure uniquement à être utilisé dans l’éditeur Unity. Il existe un ensemble différent d’eux dans le dossier WSA qui sera utilisé une fois que le projet est exporté à partir d’Unity.

6.  Ensuite, vous devez ouvrir le **WSA** dossier, en respectant le **Newtonsoft** dossier. Vous verrez une copie du même fichier que vous venez de configurer. Sélectionnez le fichier et dans l’inspecteur, vérifiez que
    -   **N’importe quelle plateforme** est **non contrôlé** 
    -   **uniquement** **WSAPlayer** est **activée**
    -   **Ne pas traiter les** est **activée**

    ![](images/AzureLabs-Lab302b-31.png)

## <a name="chapter-5---camera-setup"></a>Chapitre 5 - installation de l’appareil photo

1.  Dans le volet de la hiérarchie, sélectionnez le *Main Camera*.

2.  Une fois sélectionné, vous serez en mesure de voir tous les composants de la *Main Camera* dans le *panneau Inspecteur*.

    1.  Le *caméra* objet doit être nommé **Main Camera** (Notez l’orthographe !)

    2.  La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe !)

    3.  Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**

    4.  Définissez **effacer les indicateurs** à **couleur unie** (ignorer cela pour casque immersif).

    5.  Définir le **arrière-plan** couleur de l’appareil photo à **noir, Alpha 0 (Hex Code : #00000000)** (ignorer cela pour casque immersif).

    ![](images/AzureLabs-Lab302b-32.png)


## <a name="chapter-6---create-the-customvisionanalyser-class"></a>Chapitre 6 : créer la classe CustomVisionAnalyser.

À ce stade, vous êtes prêt à écrire du code.

Vous allez commencer avec le *CustomVisionAnalyser* classe.

> [!NOTE]
> Les appels à la **Service Vision personnalisée** apportées dans le code indiqué ci-dessous sont établies en utilisant le **API REST de Vision personnalisée**. Via l’utilisant, vous verrez comment implémenter et utiliser cette API (utile pour comprendre comment implémenter quelque chose de similaire sur votre propre). Sachez que Microsoft propose un **Custom Vision Service SDK** qui peut également être utilisé pour effectuer des appels au Service. Pour plus d’informations, visitez le [Custom Vision Service SDK](https://github.com/Microsoft/Cognitive-CustomVision-Windows/) article.

Cette classe est chargée de :

-   Chargement de la dernière image capturée sous la forme d’un tableau d’octets.

-   Envoyer le tableau d’octets à votre Azure *Service Vision personnalisée* instance pour l’analyse.

-   Recevoir une réponse sous forme de chaîne JSON.

-   La désérialisation de la réponse et en passant résultant *prédiction* à la *SceneOrganiser* (classe), qui se chargera de la façon dont la réponse doit être affichée.

Pour créer cette classe :

1.  Avec le bouton droit dans le *dossier composants* situé dans le *panneau projet*, puis cliquez sur **créer > dossier**. Appelez le dossier **Scripts**.

    ![](images/AzureLabs-Lab302b-33.png)

2.  Double-cliquez sur le dossier venez de créer, pour l’ouvrir.

3.  Avec le bouton droit dans le dossier, puis cliquez sur **créer** > **C\# Script**. Nommez le script *CustomVisionAnalyser*.

4.  Double-cliquez sur le nouveau *CustomVisionAnalyser* script pour l’ouvrir avec **Visual Studio**.

5.  Mettre à jour les espaces de noms en haut de votre fichier pour correspondre à ce qui suit :

    ```csharp
    using System.Collections;
    using System.IO;
    using UnityEngine;
    using UnityEngine.Networking;
    using Newtonsoft.Json;
    ```

6.  Dans le *CustomVisionAnalyser* de classe, ajoutez les variables suivantes :

    ```csharp
        /// <summary>
        /// Unique instance of this class
        /// </summary>
        public static CustomVisionAnalyser Instance;

        /// <summary>
        /// Insert your Prediction Key here
        /// </summary>
        private string predictionKey = "- Insert your key here -";

        /// <summary>
        /// Insert your prediction endpoint here
        /// </summary>
        private string predictionEndpoint = "Insert your prediction endpoint here";

        /// <summary>
        /// Byte array of the image to submit for analysis
        /// </summary>
        [HideInInspector] public byte[] imageBytes;
    ```

    > [!NOTE]
    > Assurez-vous que vous insérez votre **prédiction clé** dans le **predictionKey** variable et votre **point de terminaison de prédiction** dans le **predictionEndpoint** variable. Vous avez copié à *le bloc-notes* plus haut dans ce cours.

7.  Code pour **Awake()** doit maintenant être ajouté pour initialiser la variable d’Instance :

    ```csharp
        /// <summary>
        /// Initialises this class
        /// </summary>
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            Instance = this;
        }
    ```

8.  Supprimez les méthodes **Start()** et **Update()**.

9.  Ensuite, ajoutez la coroutine (avec la méthode statique **GetImageAsByteArray()** méthode en dessous), qui obtient les résultats de l’analyse de l’image capturée par le *ImageCapture* classe.

    > [!NOTE]
    > Dans le **AnalyseImageCapture** coroutine, il existe un appel à la *SceneOrganiser* classe que vous êtes encore à créer. Par conséquent, **laisser les lignes commentées pour l’instant**.

    ```csharp    
        /// <summary>
        /// Call the Computer Vision Service to submit the image.
        /// </summary>
        public IEnumerator AnalyseLastImageCaptured(string imagePath)
        {
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

                // The response will be in JSON format, therefore it needs to be deserialized    
    
                // The following lines refers to a class that you will build in later Chapters
                // Wait until then to uncomment these lines

                //AnalysisObject analysisObject = new AnalysisObject();
                //analysisObject = JsonConvert.DeserializeObject<AnalysisObject>(jsonResponse);
                //SceneOrganiser.Instance.SetTagsToLastLabel(analysisObject);
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

10.  Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.

## <a name="chapter-7---create-the-customvisionobjects-class"></a>Chapitre 7 - créer la classe CustomVisionObjects

La classe que vous allez créer est maintenant le *CustomVisionObjects* classe.

Ce script contient un nombre d’objets utilisés par d’autres classes pour sérialiser et désérialiser les appels effectués à la *Service Vision personnalisée*.

> [!WARNING]
> Il est important que vous notez le point de terminaison du Service de Vision personnalisé vous fournit, comme le JSON ci-dessous, structure a été configurée pour fonctionner avec [ *v2.0 de prédiction de Vision personnalisée*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/450e4ba4d72542e889d93fd7b8e960de/operations/5a6264bc40d86a0ef8b2c290). Si vous avez une version différente, vous devrez peut-être mettre à jour le ci-dessous structure.

Pour créer cette classe :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**. Appeler le script *CustomVisionObjects*.

2.  Double-cliquez sur le nouveau **CustomVisionObjects** script pour l’ouvrir avec **Visual Studio**.

3.  Ajoutez les espaces de noms suivantes au début du fichier :

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  Supprimer le **Start()** et **Update()** méthodes à l’intérieur de la *CustomVisionObjects* classe ; cette classe doit maintenant être vide.

5.  Ajoutez les classes suivantes **en dehors de** le *CustomVisionObjects* classe. Ces objets sont utilisés par le *Newtonsoft* bibliothèque pour sérialiser et désérialiser les données de réponse :

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
    /// JSON of Images submitted
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
    /// Predictions received by the Service after submitting an image for analysis
    /// </summary> 
    [Serializable]
    public class AnalysisObject
    {
        public List<Prediction> Predictions { get; set; }
    }

    [Serializable]
    public class Prediction
    {
        public string TagName { get; set; }
        public double Probability { get; set; }
    }
    ```

## <a name="chapter-8---create-the-voicerecognizer-class"></a>Chapitre 8 - créer la classe VoiceRecognizer

Cette classe reconnaîtra l’entrée vocale à partir de l’utilisateur.

Pour créer cette classe :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**. Appeler le script *VoiceRecognizer*.

2.  Double-cliquez sur le nouveau **VoiceRecognizer** script pour l’ouvrir avec **Visual Studio**.

3.  Ajouter des espaces de noms suivants ci-dessus le *VoiceRecognizer* classe :

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.Windows.Speech;
    ```

4.  Puis ajoutez les variables suivantes à l’intérieur de la *VoiceRecognizer* classe ci-dessus le *Start()* méthode :

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static VoiceRecognizer Instance;

        /// <summary>
        /// Recognizer class for voice recognition
        /// </summary>
        internal KeywordRecognizer keywordRecognizer;

        /// <summary>
        /// List of Keywords registered
        /// </summary>
        private Dictionary<string, Action> _keywords = new Dictionary<string, Action>();
    ```

5.  Ajouter le **Awake()** et **Start()** méthodes, ce dernier qui configureront l’utilisateur *mots clés* pour être reconnus lors de l’association d’une balise à une image :

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
        void Start ()
        {

            Array tagsArray = Enum.GetValues(typeof(CustomVisionTrainer.Tags));

            foreach (object tagWord in tagsArray)
            {
                _keywords.Add(tagWord.ToString(), () =>
                {
                    // When a word is recognized, the following line will be called
                    CustomVisionTrainer.Instance.VerifyTag(tagWord.ToString());
                });
            }

            _keywords.Add("Discard", () =>
            {
                // When a word is recognized, the following line will be called
                // The user does not want to submit the image
                // therefore ignore and discard the process
                ImageCapture.Instance.ResetImageCapture();
                keywordRecognizer.Stop();
            });

            //Create the keyword recognizer 
            keywordRecognizer = new KeywordRecognizer(_keywords.Keys.ToArray());

            // Register for the OnPhraseRecognized event 
            keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
        }
    ```

6.  Supprimer le **Update()** (méthode).

7.  Ajoutez le gestionnaire suivant, qui est appelé chaque fois que l’entrée vocale est reconnue :

    ```csharp    
        /// <summary>
        /// Handler called when a word is recognized
        /// </summary>
        private void KeywordRecognizer_OnPhraseRecognized(PhraseRecognizedEventArgs args)
        {
            Action keywordAction;
            // if the keyword recognized is in our dictionary, call that Action.
            if (_keywords.TryGetValue(args.text, out keywordAction))
            {
                keywordAction.Invoke();
            }
        }
    ```

8.  Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.

> [!NOTE]
> Ne vous inquiétez pas sur le code qui peut sembler avoir une erreur, comme vous fournit des classes de supplémentaires bientôt, ce qui résoudra ces.

## <a name="chapter-9---create-the-customvisiontrainer-class"></a>Chapitre 9 - créer la classe CustomVisionTrainer

Cette classe sera chaîner une série d’appels de web pour former le *Service Vision personnalisée*. Chaque appel est expliquée en détail juste au-dessus du code.

Pour créer cette classe :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**. Appeler le script *CustomVisionTrainer*.

2.  Double-cliquez sur le nouveau *CustomVisionTrainer* script pour l’ouvrir avec **Visual Studio**.

3.  Ajouter des espaces de noms suivants ci-dessus le *CustomVisionTrainer* classe :

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Collections.Generic;
    using System.IO;
    using System.Text;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  Puis ajoutez les variables suivantes à l’intérieur de la *CustomVisionTrainer* de classe, au-dessus du **Start()** (méthode). 

    > [!NOTE]
    > L’URL de formation utilisée ici est fourni dans le *1.2 de formation Vision personnalisée* documentation, et a une structure de : https://southcentralus.api.cognitive.microsoft.com/customvision/v1.2/Training/projects/{projectId}/  
    > Pour plus d’informations, visitez le [ *API de référence de formation de Vision personnalisée v1.2*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).

    > [!WARNING]
    > Il est important que vous notez le point de terminaison que le Service Vision personnalisée vous fournit pour le mode d’apprentissage, comme la structure JSON utilisée (dans le **CustomVisionObjects** classe) a été configuré pour fonctionner avec [  *Custom Vision v1.2 de formation*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f). Si vous avez une version différente, vous devrez peut-être mettre à jour le *objets* structure.

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static CustomVisionTrainer Instance;

        /// <summary>
        /// Custom Vision Service URL root
        /// </summary>
        private string url = "https://southcentralus.api.cognitive.microsoft.com/customvision/v1.2/Training/projects/";

        /// <summary>
        /// Insert your prediction key here
        /// </summary>
        private string trainingKey = "- Insert your key here -";

        /// <summary>
        /// Insert your Project Id here
        /// </summary>
        private string projectId = "- Insert your Project Id here -";

        /// <summary>
        /// Byte array of the image to submit for analysis
        /// </summary>
        internal byte[] imageBytes;

        /// <summary>
        /// The Tags accepted
        /// </summary>
        internal enum Tags {Mouse, Keyboard}

        /// <summary>
        /// The UI displaying the training Chapters
        /// </summary>
        private TextMesh trainingUI_TextMesh;
    ```

    > [!IMPORTANT]
    > Veillez à ajouter votre **clé Service** (clé de formation) valeur et **Id de projet** valeur, ce qui vous avez notée précédent ; ce sont les valeurs vous [collectées à partir du portail précédemment dans le (cours Chapitre 2, l’étape 10 et versions ultérieures)](#chapter-2---training-your-custom-vision-oroject).

5.  Ajoutez le code suivant **Start()** et **Awake()** méthodes. Ces méthodes sont appelées lors de l’initialisation et contient l’appel pour définir l’interface utilisateur :

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
        private void Start()
        { 
            trainingUI_TextMesh = SceneOrganiser.Instance.CreateTrainingUI("TrainingUI", 0.04f, 0, 4, false);
        }
    ```

6.  Supprimer le **Update()** (méthode). Cette classe en n'aurez pas besoin.

7.  Ajouter le **RequestTagSelection()** (méthode). Cette méthode est le premier à être appelée lorsqu’une image a été capturée et stockée dans l’appareil et est maintenant prêt à être soumis à la *Service Vision personnalisée*, former celui-ci. Cette méthode s’affiche dans la formation, l’interface utilisateur, un ensemble de mots clés de que l’utilisateur peut utiliser pour baliser l’image qui a été capturée. Il avertit également le *VoiceRecognizer* classe pour commencer à écouter entrée vocale à l’utilisateur.

    ```csharp
        internal void RequestTagSelection()
        {
            trainingUI_TextMesh.gameObject.SetActive(true);
            trainingUI_TextMesh.text = $" \nUse voice command \nto choose between the following tags: \nMouse\nKeyboard \nor say Discard";

            VoiceRecognizer.Instance.keywordRecognizer.Start();
        }
    ```

8.  Ajouter le **VerifyTag()** (méthode). Cette méthode reçoit l’entrée vocale reconnue par le **VoiceRecognizer** classe et vérifier sa validité et commencez le processus d’apprentissage.

    ```csharp
        /// <summary>
        /// Verify voice input against stored tags.
        /// If positive, it will begin the Service training process.
        /// </summary>
        internal void VerifyTag(string spokenTag)
        {
            if (spokenTag == Tags.Mouse.ToString() || spokenTag == Tags.Keyboard.ToString())
            {
                trainingUI_TextMesh.text = $"Tag chosen: {spokenTag}";
                VoiceRecognizer.Instance.keywordRecognizer.Stop();
                StartCoroutine(SubmitImageForTraining(ImageCapture.Instance.filePath, spokenTag));
            }
        }
    ```

9.  Ajouter le **SubmitImageForTraining()** (méthode). Cette méthode commence le processus d’apprentissage Service Vision personnalisée. La première étape consiste à récupérer le **Id de la balise** à partir du Service qui est associé à l’entrée vocale validé à partir de l’utilisateur. Le **Id de la balise** puis seront téléchargées, ainsi que l’image.

    ```csharp
        /// <summary>
        /// Call the Custom Vision Service to submit the image.
        /// </summary>
        public IEnumerator SubmitImageForTraining(string imagePath, string tag)
        {
            yield return new WaitForSeconds(2);
            trainingUI_TextMesh.text = $"Submitting Image \nwith tag: {tag} \nto Custom Vision Service";
            string imageId = string.Empty;
            string tagId = string.Empty;

            // Retrieving the Tag Id relative to the voice input
            string getTagIdEndpoint = string.Format("{0}{1}/tags", url, projectId);
            using (UnityWebRequest www = UnityWebRequest.Get(getTagIdEndpoint))
            {
                www.SetRequestHeader("Training-Key", trainingKey);
                www.downloadHandler = new DownloadHandlerBuffer();
                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;

                Tags_RootObject tagRootObject = JsonConvert.DeserializeObject<Tags_RootObject>(jsonResponse);

                foreach (TagOfProject tOP in tagRootObject.Tags)
                {
                    if (tOP.Name == tag)
                    {
                        tagId = tOP.Id;
                    }             
                }
            }

            // Creating the image object to send for training
            List<IMultipartFormSection> multipartList = new List<IMultipartFormSection>();
            MultipartObject multipartObject = new MultipartObject();
            multipartObject.contentType = "application/octet-stream";
            multipartObject.fileName = "";
            multipartObject.sectionData = GetImageAsByteArray(imagePath);
            multipartList.Add(multipartObject);

            string createImageFromDataEndpoint = string.Format("{0}{1}/images?tagIds={2}", url, projectId, tagId);

            using (UnityWebRequest www = UnityWebRequest.Post(createImageFromDataEndpoint, multipartList))
            {
                // Gets a byte array out of the saved image
                imageBytes = GetImageAsByteArray(imagePath);           

                //unityWebRequest.SetRequestHeader("Content-Type", "application/octet-stream");
                www.SetRequestHeader("Training-Key", trainingKey);

                // The upload handler will help uploading the byte array with the request
                www.uploadHandler = new UploadHandlerRaw(imageBytes);

                // The download handler will help receiving the analysis from Azure
                www.downloadHandler = new DownloadHandlerBuffer();

                // Send the request
                yield return www.SendWebRequest();

                string jsonResponse = www.downloadHandler.text;

                ImageRootObject m = JsonConvert.DeserializeObject<ImageRootObject>(jsonResponse);
                imageId = m.Images[0].Image.Id;
            }
            trainingUI_TextMesh.text = "Image uploaded";
            StartCoroutine(TrainCustomVisionProject());
        }
    ```

10. Ajouter le **TrainCustomVisionProject()** (méthode). Une fois que l’image a été soumise et marqué, cette méthode est appelée. Il crée une nouvelle itération sera formée avec toutes les images précédentes soumis pour le Service ainsi que l’image venez de télécharger. Une fois la formation terminée, cette méthode appelle une méthode pour définir le nouvellement créé **itération** comme **par défaut**, de sorte que le point de terminaison que vous utilisez pour l’analyse est la dernière itération formée.

    ```csharp
        /// <summary>
        /// Call the Custom Vision Service to train the Service.
        /// It will generate a new Iteration in the Service
        /// </summary>
        public IEnumerator TrainCustomVisionProject()
        {
            yield return new WaitForSeconds(2);

            trainingUI_TextMesh.text = "Training Custom Vision Service";

            WWWForm webForm = new WWWForm();

            string trainProjectEndpoint = string.Format("{0}{1}/train", url, projectId);

            using (UnityWebRequest www = UnityWebRequest.Post(trainProjectEndpoint, webForm))
            {
                www.SetRequestHeader("Training-Key", trainingKey);
                www.downloadHandler = new DownloadHandlerBuffer();
                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;
                Debug.Log($"Training - JSON Response: {jsonResponse}");

                // A new iteration that has just been created and trained
                Iteration iteration = new Iteration();
                iteration = JsonConvert.DeserializeObject<Iteration>(jsonResponse);

                if (www.isDone)
                {
                    trainingUI_TextMesh.text = "Custom Vision Trained";

                    // Since the Service has a limited number of iterations available,
                    // we need to set the last trained iteration as default
                    // and delete all the iterations you dont need anymore
                    StartCoroutine(SetDefaultIteration(iteration)); 
                }
            }
        }
    ```

11. Ajouter le **SetDefaultIteration()** (méthode). Cette méthode définit l’itération précédemment créée et formée en tant que *par défaut*. Une fois terminé, cette méthode sera obligé de supprimer l’itération précédente existant dans le Service. Au moment de la rédaction de ce cours, il existe une limite d’un itérations dix (10) maximal autorisé d’exister en même temps dans le Service.

    ```csharp
        /// <summary>
        /// Set the newly created iteration as Default
        /// </summary>
        private IEnumerator SetDefaultIteration(Iteration iteration)
        {
            yield return new WaitForSeconds(5);
            trainingUI_TextMesh.text = "Setting default iteration";

            // Set the last trained iteration to default
            iteration.IsDefault = true;

            // Convert the iteration object as JSON
            string iterationAsJson = JsonConvert.SerializeObject(iteration);
            byte[] bytes = Encoding.UTF8.GetBytes(iterationAsJson);

            string setDefaultIterationEndpoint = string.Format("{0}{1}/iterations/{2}", 
                                                            url, projectId, iteration.Id);

            using (UnityWebRequest www = UnityWebRequest.Put(setDefaultIterationEndpoint, bytes))
            {
                www.method = "PATCH";
                www.SetRequestHeader("Training-Key", trainingKey);
                www.SetRequestHeader("Content-Type", "application/json");
                www.downloadHandler = new DownloadHandlerBuffer();

                yield return www.SendWebRequest();

                string jsonResponse = www.downloadHandler.text;

                if (www.isDone)
                {
                    trainingUI_TextMesh.text = "Default iteration is set \nDeleting Unused Iteration";
                    StartCoroutine(DeletePreviousIteration(iteration));
                }
            }
        }
    ```

12. Ajouter le **DeletePreviousIteration()** (méthode). Cette méthode sera rechercher et supprimer l’itération par défaut précédente :

    ```csharp
        /// <summary>
        /// Delete the previous non-default iteration.
        /// </summary>
        public IEnumerator DeletePreviousIteration(Iteration iteration)
        {
            yield return new WaitForSeconds(5);

            trainingUI_TextMesh.text = "Deleting Unused \nIteration";

            string iterationToDeleteId = string.Empty;

            string findAllIterationsEndpoint = string.Format("{0}{1}/iterations", url, projectId);

            using (UnityWebRequest www = UnityWebRequest.Get(findAllIterationsEndpoint))
            {
                www.SetRequestHeader("Training-Key", trainingKey);
                www.downloadHandler = new DownloadHandlerBuffer();
                yield return www.SendWebRequest();

                string jsonResponse = www.downloadHandler.text;

                // The iteration that has just been trained
                List<Iteration> iterationsList = new List<Iteration>();
                iterationsList = JsonConvert.DeserializeObject<List<Iteration>>(jsonResponse);

                foreach (Iteration i in iterationsList)
                {
                    if (i.IsDefault != true)
                    {
                        Debug.Log($"Cleaning - Deleting iteration: {i.Name}, {i.Id}");
                        iterationToDeleteId = i.Id;
                        break;
                    }
                }
            }

            string deleteEndpoint = string.Format("{0}{1}/iterations/{2}", url, projectId, iterationToDeleteId);

            using (UnityWebRequest www2 = UnityWebRequest.Delete(deleteEndpoint))
            {
                www2.SetRequestHeader("Training-Key", trainingKey);
                www2.downloadHandler = new DownloadHandlerBuffer();
                yield return www2.SendWebRequest();
                string jsonResponse = www2.downloadHandler.text;

                trainingUI_TextMesh.text = "Iteration Deleted";
                yield return new WaitForSeconds(2);
                trainingUI_TextMesh.text = "Ready for next \ncapture";

                yield return new WaitForSeconds(2);
                trainingUI_TextMesh.text = "";
                ImageCapture.Instance.ResetImageCapture();
            }
        }
    ```

13. La dernière méthode pour ajouter dans cette classe est la **GetImageAsByteArray()** méthode, permet de convertir l’image capturée dans un tableau d’octets sur les appels web.

    ```csharp
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

14. Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.

## <a name="chapter-10---create-the-sceneorganiser-class"></a>Chapitre 10 - créer la classe SceneOrganiser

Cette classe sera :

-   Créer un **curseur** objet à attacher à la caméra principale.

-   Créer un **étiquette** objet qui s’affiche lorsque le Service reconnaît les objets du monde réel.

-   Configurer la caméra principale en joignant les composants appropriés à ce dernier.

-   En **Mode Analysis**, générer les étiquettes lors de l’exécution, dans l’espace de monde appropriée par rapport à la position de la caméra principale et afficher les données reçues à partir du Service de Vision personnalisée.

-   En **Mode d’apprentissage**, générer l’interface utilisateur qui affiche les différentes étapes du processus de formation.

Pour créer cette classe :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**. Nommez le script *SceneOrganiser*.

2.  Double-cliquez sur le nouveau *SceneOrganiser* script pour l’ouvrir avec **Visual Studio**.

3.  Vous devez uniquement un espace de noms, supprimez les autres ci-dessus le *SceneOrganiser* classe :

    ```csharp
    using UnityEngine;
    ```

4.  Puis ajoutez les variables suivantes à l’intérieur de la *SceneOrganiser* classe ci-dessus le **Start()** méthode :

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static SceneOrganiser Instance;

        /// <summary>
        /// The cursor object attached to the camera
        /// </summary>
        internal GameObject cursor;

        /// <summary>
        /// The label used to display the analysis on the objects in the real world
        /// </summary>
        internal GameObject label;

        /// <summary>
        /// Object providing the current status of the camera.
        /// </summary>
        internal TextMesh cameraStatusIndicator;

        /// <summary>
        /// Reference to the last label positioned
        /// </summary>
        internal Transform lastLabelPlaced;

        /// <summary>
        /// Reference to the last label positioned
        /// </summary>
        internal TextMesh lastLabelPlacedText;

        /// <summary>
        /// Current threshold accepted for displaying the label
        /// Reduce this value to display the recognition more often
        /// </summary>
        internal float probabilityThreshold = 0.5f;
    ```

5.  Supprimer le **Start()** et **Update()** méthodes.

6.  Directement sous les variables, ajoutez le **Awake()** (méthode), qui initialisent la classe et configurer la scène.

    ```csharp
        /// <summary>
        /// Called on initialization
        /// </summary>
        private void Awake()
        {
            // Use this class instance as singleton
            Instance = this;

            // Add the ImageCapture class to this GameObject
            gameObject.AddComponent<ImageCapture>();

            // Add the CustomVisionAnalyser class to this GameObject
            gameObject.AddComponent<CustomVisionAnalyser>();

            // Add the CustomVisionTrainer class to this GameObject
            gameObject.AddComponent<CustomVisionTrainer>();

            // Add the VoiceRecogniser class to this GameObject
            gameObject.AddComponent<VoiceRecognizer>();

            // Add the CustomVisionObjects class to this GameObject
            gameObject.AddComponent<CustomVisionObjects>();

            // Create the camera Cursor
            cursor = CreateCameraCursor();

            // Load the label prefab as reference
            label = CreateLabel();

            // Create the camera status indicator label, and place it above where predictions
            // and training UI will appear.
            cameraStatusIndicator = CreateTrainingUI("Status Indicator", 0.02f, 0.2f, 3, true);

            // Set camera status indicator to loading.
            SetCameraStatus("Loading");
        }
    ```

7.  À présent ajouter le **CreateCameraCursor()** méthode qui crée et place le curseur Main Camera, et le **CreateLabel()** (méthode), ce qui crée le **libellé d’analyse** objet .

    ```csharp
        /// <summary>
        /// Spawns cursor for the Main Camera
        /// </summary>
        private GameObject CreateCameraCursor()
        {
            // Create a sphere as new cursor
            GameObject newCursor = GameObject.CreatePrimitive(PrimitiveType.Sphere);

            // Attach it to the camera
            newCursor.transform.parent = gameObject.transform;

            // Resize the new cursor
            newCursor.transform.localScale = new Vector3(0.02f, 0.02f, 0.02f);

            // Move it to the correct position
            newCursor.transform.localPosition = new Vector3(0, 0, 4);

            // Set the cursor color to red
            newCursor.GetComponent<Renderer>().material = new Material(Shader.Find("Diffuse"));
            newCursor.GetComponent<Renderer>().material.color = Color.green;

            return newCursor;
        }

        /// <summary>
        /// Create the analysis label object
        /// </summary>
        private GameObject CreateLabel()
        {
            // Create a sphere as new cursor
            GameObject newLabel = new GameObject();

            // Resize the new cursor
            newLabel.transform.localScale = new Vector3(0.01f, 0.01f, 0.01f);

            // Creating the text of the label
            TextMesh t = newLabel.AddComponent<TextMesh>();
            t.anchor = TextAnchor.MiddleCenter;
            t.alignment = TextAlignment.Center;
            t.fontSize = 50;
            t.text = "";

            return newLabel;
        }
    ```

8. Ajouter le **SetCameraStatus()** méthode qui gérera les messages destinés à la maille de texte en fournissant l’état de l’appareil photo.

    ```csharp
        /// <summary>
        /// Set the camera status to a provided string. Will be coloured if it matches a keyword.
        /// </summary>
        /// <param name="statusText">Input string</param>
        public void SetCameraStatus(string statusText)
        {
            if (string.IsNullOrEmpty(statusText) == false)
            {
                string message = "white";

                switch (statusText.ToLower())
                {
                    case "loading":
                        message = "yellow";
                        break;

                    case "ready":
                        message = "green";
                        break;

                    case "uploading image":
                        message = "red";
                        break;

                    case "looping capture":
                        message = "yellow";
                        break;

                    case "analysis":
                        message = "red";
                        break;
                }

                cameraStatusIndicator.GetComponent<TextMesh>().text = $"Camera Status:\n<color={message}>{statusText}..</color>";
            }
        }
    ```

9. Ajouter le **PlaceAnalysisLabel()** et **SetTagsToLastLabel()** méthodes, ce qui permettra de générer dynamiquement et afficher les données à partir du Service de Vision personnalisée dans la scène.

    ```csharp
        /// <summary>
        /// Instantiate a label in the appropriate location relative to the Main Camera.
        /// </summary>
        public void PlaceAnalysisLabel()
        {
            lastLabelPlaced = Instantiate(label.transform, cursor.transform.position, transform.rotation);
            lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();
        }

        /// <summary>
        /// Set the Tags as Text of the last label created. 
        /// </summary>
        public void SetTagsToLastLabel(AnalysisObject analysisObject)
        {
            lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();

            if (analysisObject.Predictions != null)
            {
                foreach (Prediction p in analysisObject.Predictions)
                {
                    if (p.Probability > 0.02)
                    {
                        lastLabelPlacedText.text += $"Detected: {p.TagName} {p.Probability.ToString("0.00 \n")}";
                        Debug.Log($"Detected: {p.TagName} {p.Probability.ToString("0.00 \n")}");
                    }
                }
            }
        }
    ```

10. Enfin, ajoutez le **CreateTrainingUI()** (méthode), ce qui génèrera l’interface utilisateur affichant les plusieurs étapes du processus de formation lors de l’application est en Mode d’apprentissage. Cette méthode sera également être amenée à créer l’objet d’état de la caméra.

    ```csharp
        /// <summary>
        /// Create a 3D Text Mesh in scene, with various parameters.
        /// </summary>
        /// <param name="name">name of object</param>
        /// <param name="scale">scale of object (i.e. 0.04f)</param>
        /// <param name="yPos">height above the cursor (i.e. 0.3f</param>
        /// <param name="zPos">distance from the camera</param>
        /// <param name="setActive">whether the text mesh should be visible when it has been created</param>
        /// <returns>Returns a 3D text mesh within the scene</returns>
        internal TextMesh CreateTrainingUI(string name, float scale, float yPos, float zPos, bool setActive)
        {
            GameObject display = new GameObject(name, typeof(TextMesh));
            display.transform.parent = Camera.main.transform;
            display.transform.localPosition = new Vector3(0, yPos, zPos);
            display.SetActive(setActive);
            display.transform.localScale = new Vector3(scale, scale, scale);
            display.transform.rotation = new Quaternion();
            TextMesh textMesh = display.GetComponent<TextMesh>();
            textMesh.anchor = TextAnchor.MiddleCenter;
            textMesh.alignment = TextAlignment.Center;
            return textMesh;
        }
    ```

11. Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.

> [!IMPORTANT]
> Avant de continuer, ouvrez le **CustomVisionAnalyser** (classe) et dans le **AnalyseLastImageCaptured()** (méthode), *Décommentez* les lignes suivantes :
>
> ```csharp
>   AnalysisObject analysisObject = new AnalysisObject();
>   analysisObject = JsonConvert.DeserializeObject<AnalysisObject>(jsonResponse);
>   SceneOrganiser.Instance.SetTagsToLastLabel(analysisObject);
> ```

## <a name="chapter-11---create-the-imagecapture-class"></a>Chapitre 11 - créer la classe ImageCapture

La classe suivante, vous allez créer est la *ImageCapture* classe.

Cette classe est chargée de :

-   Capture d’une image à l’aide de l’appareil photo HoloLens et en le stockant dans le *application* dossier.

-   Gestion des gestes de drainage de l’utilisateur.

-   Maintenir la *Enum* valeur qui détermine si l’application s’exécutera *Analysis* mode ou *formation* Mode.

Pour créer cette classe :

1.  Accédez à la **Scripts** dossier que vous avez créé précédemment.

2.  Avec le bouton droit dans le dossier, puis cliquez sur **créer > C\# Script**. Nommez le script *ImageCapture*.

3.  Double-cliquez sur le nouveau **ImageCapture** script pour l’ouvrir avec **Visual Studio**.

4.  Remplacez les espaces de noms en haut du fichier avec les éléments suivants :

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    using UnityEngine.XR.WSA.WebCam;
    ```

5.  Puis ajoutez les variables suivantes à l’intérieur de la *ImageCapture* classe ci-dessus le **Start()** méthode :

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
        /// Loop timer
        /// </summary>
        private float secondsBetweenCaptures = 10f;

        /// <summary>
        /// Application main functionalities switch
        /// </summary>
        internal enum AppModes {Analysis, Training }
        
        /// <summary>
        /// Local variable for current AppMode
        /// </summary>
        internal AppModes AppMode { get; private set; }

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

            // Change this flag to switch between Analysis Mode and Training Mode 
            AppMode = AppModes.Training;
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

            // Subscribing to the Hololens API gesture recognizer to track user gestures
            recognizer = new GestureRecognizer();
            recognizer.SetRecognizableGestures(GestureSettings.Tap);
            recognizer.Tapped += TapHandler;
            recognizer.StartCapturingGestures();

            SceneOrganiser.Instance.SetCameraStatus("Ready");
        }
    ```

7.  Implémentez un gestionnaire qui sera appelé lorsqu’une action d’appuyer se produit.

    ```csharp
        /// <summary>
        /// Respond to Tap Input.
        /// </summary>
        private void TapHandler(TappedEventArgs obj)
        {
            switch (AppMode)
            {
                case AppModes.Analysis:
                    if (!captureIsActive)
                    {
                        captureIsActive = true;

                        // Set the cursor color to red
                        SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.red;
                        
                        // Update camera status to looping capture.
                        SceneOrganiser.Instance.SetCameraStatus("Looping Capture");

                        // Begin the capture loop
                        InvokeRepeating("ExecuteImageCaptureAndAnalysis", 0, secondsBetweenCaptures);
                    }
                    else
                    {
                        // The user tapped while the app was analyzing 
                        // therefore stop the analysis process
                        ResetImageCapture();
                    }
                    break;

                case AppModes.Training:
                    if (!captureIsActive)
                    {
                        captureIsActive = true;

                        // Call the image capture
                        ExecuteImageCaptureAndAnalysis();

                        // Set the cursor color to red
                        SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.red;

                        // Update camera status to uploading image.
                        SceneOrganiser.Instance.SetCameraStatus("Uploading Image");
                    }              
                    break;
            }     
        }
    ```

    > [!NOTE] 
    > Dans *Analysis* mode, le **TapHandler** méthode agit comme un commutateur pour démarrer ou arrêter la boucle de capture photo.
    >
    > Dans *formation* mode, il capture une image à partir de l’appareil photo.
    >
    > Lorsque le curseur est vert, cela signifie que l’appareil photo est disponible pour la prise de l’image.
    >
    > Lorsque le curseur est rouge, cela signifie que l’appareil photo est occupé.

8.  Ajoutez la méthode que l’application utilise pour démarrer le processus de capture d’image et de stocker l’image.

    ```csharp
        /// <summary>
        /// Begin process of Image Capturing and send To Azure Custom Vision Service.
        /// </summary>
        private void ExecuteImageCaptureAndAnalysis()
        {
            // Update camera status to analysis.
            SceneOrganiser.Instance.SetCameraStatus("Analysis");

            // Create a label in world space using the SceneOrganiser class 
            // Invisible at this point but correctly positioned where the image was taken
            SceneOrganiser.Instance.PlaceAnalysisLabel();

            // Set the camera resolution to be the highest possible
            Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();

            Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);

            // Begin capture process, set the image format
            PhotoCapture.CreateAsync(false, delegate (PhotoCapture captureObject)
            {
                photoCaptureObject = captureObject;

                CameraParameters camParameters = new CameraParameters
                {
                    hologramOpacity = 0.0f,
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

9.  Ajoutez les gestionnaires qui seront appelées lorsque la photo a été capturée et quand il est prêt à être analysés. Le résultat est ensuite transmis à la *CustomVisionAnalyser* ou *CustomVisionTrainer* selon le mode que le code est défini sur.

    ```csharp
        /// <summary>
        /// Register the full execution of the Photo Capture. 
        /// </summary>
        void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
        {
                // Call StopPhotoMode once the image has successfully captured
                photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
        }


        /// <summary>
        /// The camera photo mode has stopped after the capture.
        /// Begin the Image Analysis process.
        /// </summary>
        void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
        {
            Debug.LogFormat("Stopped Photo Mode");
        
            // Dispose from the object in memory and request the image analysis 
            photoCaptureObject.Dispose();
            photoCaptureObject = null;

            switch (AppMode)
            {
                case AppModes.Analysis:
                    // Call the image analysis
                    StartCoroutine(CustomVisionAnalyser.Instance.AnalyseLastImageCaptured(filePath));
                    break;

                case AppModes.Training:
                    // Call training using captured image
                    CustomVisionTrainer.Instance.RequestTagSelection();
                    break;
            }
        }

        /// <summary>
        /// Stops all capture pending actions
        /// </summary>
        internal void ResetImageCapture()
        {
            captureIsActive = false;

            // Set the cursor color to green
            SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.green;

            // Update camera status to ready.
            SceneOrganiser.Instance.SetCameraStatus("Ready");

            // Stop the capture loop if active
            CancelInvoke();
        }
    ```

10. Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.

11. Maintenant que tous les scripts ont été terminés, revenez dans l’éditeur Unity, puis cliquez et faites glisser le **SceneOrganiser** classe à partir de la **Scripts** dossier pour le **Main Camera** objet dans le *hiérarchie panneau*.

## <a name="chapter-12---before-building"></a>Chapitre 12 - avant la génération

Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre HoloLens.

Avant de procéder, assurez-vous que :

- Tous les paramètres mentionnés dans le [chapitre 2](#chapter-2---training-your-custom-vision-project) sont correctement définies.

- Tous les champs dans le **Main Camera**, panneau Inspecteur, sont affectées correctement.

- Le script **SceneOrganiser** est attaché à la **Main Camera** objet.

- Assurez-vous que vous insérez votre **prédiction clé** dans le **predictionKey** variable.

- Vous avez inséré votre **point de terminaison de prédiction** dans le **predictionEndpoint** variable.

- Vous avez inséré votre **formation clé** dans le **trainingKey** variable, de la *CustomVisionTrainer* classe.

- Vous avez inséré votre **ID de projet** dans le **projectId** variable, de la *CustomVisionTrainer* classe.

## <a name="chapter-13---build-and-sideload-your-application"></a>Chapitre 13 - Build et chargement de version test votre application

Pour commencer le *Build* processus :

1.  Accédez à **fichier > Paramètres de Build**.

2.  Graduation **Unity C\# projets**.

3.  Cliquez sur **Build**. Unity lancera un **Explorateur de fichiers** fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans. Créez ce dossier, puis nommez-le **application**. Ensuite avec le **application** dossier sélectionné, cliquez sur **sélectionner le dossier**.

4.  Unity commencera à générer votre projet pour le **application** dossier.

5.  Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).

Pour déployer sur HoloLens :

1.  Vous devez l’adresse IP de votre HoloLens (pour les déployer à distance) et pour vérifier que votre HoloLens est dans **Mode développeur**. Pour ce faire :

    1.  Tout en portant vos HoloLens, ouvrez le **paramètres**.

    2.  Accédez à **réseau & Internet** > **Wi-Fi** > **les Options avancées**

    3.  Remarque la **IPv4** adresse.

    4.  Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité** > **pour les développeurs**

    5.  Définissez **Mode développeur sur**.

2.  Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.

3.  Dans le *Configuration de la Solution* sélectionnez **déboguer**.

4.  Dans le *plateforme de Solution*, sélectionnez **x86, ordinateur distant**. Vous devrez insérer le **adresse IP** d’un appareil à distance (la HoloLens, dans ce cas, que vous avez notée).

    ![](images/AzureLabs-Lab302b-34.png)

5. Accédez à **Build** menu et cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre HoloLens.

6. Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !

> [!NOTE]
> Pour déployer sur casque immersif, définissez le **plateforme de Solution** à *ordinateur Local*et définissez le **Configuration** à *déboguer*, avec *x86* en tant que le **plateforme**. Déployer sur l’ordinateur local d’ordinateur, à l’aide de la **Build** élément de menu, en sélectionnant *déployer la Solution*. 

## <a name="to-use-the-application"></a>Pour utiliser l’application :

Pour basculer de la fonctionnalité d’application entre *formation* mode et *prédiction* mode, vous devez mettre à jour le **AppMode** variable, qui se trouve dans le **Awake()** méthode situés dans le *ImageCapture* classe.

```
        // Change this flag to switch between Analysis mode and Training mode 
        AppMode = AppModes.Training;
```
ou Gestionnaire de configuration
```
        // Change this flag to switch between Analysis mode and Training mode 
        AppMode = AppModes.Analysis;
```

Dans *formation* mode :

- Examinez **souris** ou **clavier** et utiliser le **mouvement d’appui**.

- Ensuite, le texte s’affiche vous demandant de fournir une balise.

- Indiquer **souris** ou **clavier**.


Dans *prédiction* mode :

- Rechercher un objet et d’utiliser le **mouvement d’appui**.

- Texte s’affiche en fournissant l’objet détecté, avec la probabilité la plus élevée (cela est normalisé).

## <a name="chapter-14---evaluate-and-improve-your-custom-vision-model"></a>Chapitre 14 - évaluer et améliorer votre modèle de Vision personnalisée

Pour rendre la plus précise de votre Service, vous devrez continuer à former le modèle utilisé pour la prédiction. Ceci est réalisé grâce à l’aide de votre nouvelle application, avec à la fois le *formation* et *prédiction* modes, avec le dernier que vous ayez à visiter le portail, c'est-à-dire des sujets traités dans ce chapitre. Soyez prêt à revenir sur votre portail plusieurs fois, afin d’améliorer en permanence votre modèle.

1. Accédez à nouveau à votre portail de Vision personnalisée Azure et une fois que vous êtes dans votre projet, sélectionnez le *prédictions* onglet (à partir de centre du bord supérieur de la page) :

    ![](images/AzureLabs-Lab302b-35.png)

2. Vous verrez toutes les images qui ont été envoyés à votre Service, tandis que votre application a été exécutée. Si vous pointez sur les images, ils vous fournira les prédictions qui ont été apportées pour cette image :

    ![](images/AzureLabs-Lab302b-36.png)

3. Sélectionnez une de vos images pour l’ouvrir. Une fois ouvert, vous verrez les prévisions effectuées pour cette image vers la droite. Si vous la justesse des prédictions correctes et que vous souhaitez ajouter cette image à un modèle d’apprentissage de votre Service, cliquez sur le *Mes balises* zone d’entrée, puis sélectionnez la balise que vous souhaitez associer. Lorsque vous avez terminé, cliquez sur le *enregistrer et fermer* bouton en bas à droite et de passer à l’image suivante.

    ![](images/AzureLabs-Lab302b-37.png)

4. Une fois que vous êtes à la grille des images, vous remarquerez les images que vous avez ajouté des balises à (et enregistré), va être supprimé. Si vous trouvez des images que vous pensez ne pas votre élément balisé en leur sein, vous pouvez les supprimer, en cliquant sur les graduations sur cette image (cette opération pour plusieurs images), puis sur *supprimer* dans le coin supérieur droit de la page de grille. Dans la fenêtre contextuelle qui suit, vous pouvez cliquer sur *Oui, supprimer* ou *non*, pour confirmer la suppression ou de l’annuler, respectivement. 

    ![](images/AzureLabs-Lab302b-38.png)

5. Lorsque vous êtes prêt à continuer, cliquez sur le vert *Train* bouton dans le coin supérieur droit. Votre modèle de Service sera formé avec toutes les images que vous avez maintenant fourni (ce qui rendent plus précis). Une fois la formation terminée, veillez à cliquer sur le *par défaut* bouton une fois de plus, afin que votre *prédiction URL* continue d’utiliser l’itération la plus récente de votre Service.

    ![](images/AzureLabs-Lab302b-39.png) ![](images/AzureLabs-Lab302b-40.png)

## <a name="your-finished-custom-vision-api-application"></a>Votre application API de Vision personnalisée terminée

Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API de Vision Azure personnalisée pour reconnaître des objets du monde réel, former le modèle de Service et afficher le niveau de confiance de ce qui a été vu.

![](images/AzureLabs-Lab302b-00.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Former votre **Service Vision personnalisée** à reconnaître plus d’objets.

### <a name="exercise-2"></a>Exercice 2

Comme un moyen pour développer ce que vous avez appris, effectuez les exercices suivants :

Un signal sonore lorsqu’un objet est reconnu.

### <a name="exercise-3"></a>Exercice 3

Utiliser l’API pour recalculer votre Service avec les mêmes images de l’analyse de votre application, par conséquent, pour rendre le Service plus précis (effectuer la prédiction et la formation simultanément).
