---
title: MR et Azure 302b-vision personnalisée
description: Suivez ce cours pour apprendre à former un modèle de Machine Learning, puis à utiliser le modèle formé pour reconnaître des objets similaires dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/03/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, vision personnalisée, hololens, immersif, VR
ms.openlocfilehash: e6e9782a8d559af660dc4765556f1e926c5360b1
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63553607"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br>

# <a name="mr-and-azure-302b-custom-vision"></a>RM et Azure 302b: Vision personnalisée

Dans ce cours, vous allez apprendre à reconnaître du contenu visuel personnalisé dans une image fournie, à l’aide des fonctionnalités d’Azure Custom Vision dans une application de réalité mixte.

Ce service vous permet d’effectuer l’apprentissage d’un modèle de Machine Learning à l’aide d’images d’objet. Vous utiliserez ensuite le modèle formé pour reconnaître des objets similaires, fournis par la capture de l’appareil photo de Microsoft HoloLens ou un appareil photo connecté à votre PC pour les casques immersifs (VR).

![résultat du cours](images/AzureLabs-Lab302b-00.png)

Azure Custom Vision est un service cognitive de Microsoft qui permet aux développeurs de créer des classifieurs d’images personnalisées. Ces classifieurs peuvent ensuite être utilisés avec de nouvelles images pour reconnaître, ou classer, des objets dans cette nouvelle image. Le service fournit un portail en ligne simple et facile à utiliser pour simplifier le processus. Pour plus d’informations, consultez la [page service vision personnalisée Azure](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home).

À la fin de ce cours, vous disposerez d’une application de réalité mixte qui pourra fonctionner en deux modes:

-   **Mode d’analyse**: configuration manuelle du service vision personnalisée en chargeant des images, en créant des balises et en formant une formation au service pour reconnaître différents objets (dans ce cas, la souris et le clavier). Vous allez ensuite créer une application HoloLens qui capturera les images à l’aide de l’appareil photo et essayez de reconnaître ces objets dans le monde réel.

-   **Mode d’apprentissage**: vous allez implémenter le code qui activera un «mode d’apprentissage» dans votre application. Le mode d’apprentissage vous permet de capturer des images à l’aide de l’appareil photo HoloLens, de charger les images capturées dans le service et d’effectuer l’apprentissage du modèle de vision personnalisée.

Ce cours vous apprend à obtenir les résultats de la Service Vision personnalisée dans un exemple d’application basée sur Unity. Il vous faudra appliquer ces concepts à une application personnalisée que vous pouvez générer.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> RM et Azure 302b: Vision personnalisée</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Bien que ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques pour Windows Mixed Reality (VR). Étant donné que les casques immersifs ne disposent pas de caméras accessibles, vous aurez besoin d’une caméra externe connectée à votre PC. À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge les écouteurs immersifs (VR).

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:

- Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](install-the-tools.md#installation-checklist)
- [Le dernier Kit de développement logiciel Windows 10](install-the-tools.md#installation-checklist)
- [Unity 2017,4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé
- Appareil photo connecté à votre PC (pour le développement d’un casque immersif)
- Accès à Internet pour l’installation d’Azure et la récupération de l’API Custom Vision
- Une série d’au moins cinq (5) images (dix (10) recommandé) pour chaque objet que vous souhaitez que le Service Vision personnalisée reconnaître. Si vous le souhaitez, vous pouvez utiliser [les images déjà fournies dans ce cours (une souris d’ordinateur et un clavier) ](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).
2.  Configurez et testez votre HoloLens. Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur). 

Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1---the-custom-vision-service-portal"></a>Chapitre 1-portail Service Vision personnalisée

Pour utiliser le *service vision personnalisée* dans Azure, vous devez configurer une instance du service qui sera mise à la disposition de votre application.

1.  Tout d’abord, [accédez à la page principale *service vision personnalisée* ](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).

2.  Cliquez sur le bouton **prise en main** .

    ![](images/AzureLabs-Lab302b-01.png)

3.  Connectez-vous au portail *service vision personnalisée* .

    ![](images/AzureLabs-Lab302b-02.png)

    > [!NOTE]
    > Si vous n’avez pas encore de compte Azure, vous devez en créer un. Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.

4.  Une fois que vous êtes connecté pour la première fois, vous êtes invité à entrer dans le panneau *des conditions d’accès* . Cliquez sur la case à cocher pour accepter les termes du contrat. Cliquez ensuite sur **J’accepte**.

    ![](images/AzureLabs-Lab302b-03.png)

5.  Une fois les conditions accordées, vous accédez à la section *projets* du portail. Cliquez sur **nouveau projet**.

    ![](images/AzureLabs-Lab302b-04.png)

6.  Un onglet s’affiche sur le côté droit, ce qui vous invite à spécifier certains champs pour le projet.

    1.  Insérez un *nom* pour votre projet.

    2.  Insérez une *Description* de votre projet (*facultatif*).

    3.  Choisissez un *groupe de ressources* ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.

    4. Définir les *types de projets* sur **classification**
    
    5. Définissez les *domaines* comme étant **généraux**.

        ![](images/AzureLabs-Lab302b-05.png)

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

7.  Une fois que vous avez terminé, cliquez sur **créer un projet**, vous serez redirigé vers la page service vision personnalisée, projet.

## <a name="chapter-2---training-your-custom-vision-project"></a>Chapitre 2-formation de votre projet Custom Vision

Une fois dans le portail Custom Vision, votre objectif principal est de former votre projet à la reconnaissance d’objets spécifiques dans les images. Vous avez besoin d’au moins cinq (5) images, même si dix (10) sont préférables pour chaque objet que vous souhaitez que votre application reconnaisse. [Vous pouvez utiliser les images fournies dans ce cours (une souris d’ordinateur et un clavier)](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip). 

Pour former votre projet Service Vision personnalisée:

1.  Cliquez sur le **+** bouton en regard de **balises.**

    ![](images/AzureLabs-Lab302b-06.png)

2.  Ajoutez le **nom** de l’objet que vous souhaitez reconnaître. Cliquez sur **Enregistrer**.

    ![](images/AzureLabs-Lab302b-07.png)

3.  Vous remarquerez que votre balise a été ajoutée (vous devrez peut-être recharger votre page pour qu’elle apparaisse). Cliquez sur la case à cocher en regard de votre nouvelle balise, si elle n’est pas déjà activée.

    ![](images/AzureLabs-Lab302b-08.png)

4.  Cliquez sur **Ajouter des images** au centre de la page.

    ![](images/AzureLabs-Lab302b-09.png)

5.  Cliquez sur **Parcourir les fichiers locaux**et recherchez, puis sélectionnez les images que vous souhaitez télécharger, avec un minimum de cinq (5). N’oubliez pas que toutes ces images doivent contenir l’objet que vous êtes en train de former.

    > [!NOTE]
    >  Vous pouvez sélectionner plusieurs images à la fois, à télécharger.

6.  Une fois que vous pouvez voir les images dans l’onglet, sélectionnez la balise appropriée dans la zone **mes balises** .

    ![](images/AzureLabs-Lab302b-10.png)

7.  Cliquez sur **charger les fichiers**. Le chargement des fichiers va commencer. Une fois que vous avez confirmé le téléchargement, cliquez sur **terminé**.

    ![](images/AzureLabs-Lab302b-11.png)

8.  Répétez le même processus pour créer une nouvelle balise nommée **Keyboard** et chargez les photos appropriées pour celle-ci. Veillez à ne pas **vérifier** la *souris* une fois que vous avez créé les nouvelles balises, afin d’afficher la fenêtre *Ajouter des images* .

9.  Une fois que les deux balises sont configurées, cliquez sur **train**, et la première itération d’apprentissage commencera la génération.

    ![](images/AzureLabs-Lab302b-12.png)

10. Une fois qu’elle est créée, vous pouvez voir deux boutons nommés **créer par défaut** et **URL**de prédiction. Cliquez d’abord sur **créer par défaut** , puis sur **URL**de prédiction.

    ![](images/AzureLabs-Lab302b-13.png)

    > [!NOTE] 
    > L’URL du point de terminaison qui est fournie à partir de ce, est définie sur l' *itération* qui a été marquée comme valeur par défaut. Par conséquent, si vous effectuez ultérieurement une nouvelle *itération* et la mettez à jour par défaut, vous n’aurez pas besoin de modifier votre code.

11. Une fois que vous avez cliqué sur *URL*de prédiction, ouvrez *le bloc-notes*, puis copiez et collez l' **URL** et la clé de prédiction, afin de pouvoir la récupérer lorsque vous en aurez besoin ultérieurement dans le code.

    ![](images/AzureLabs-Lab302b-14.png)

12. Cliquez sur le **roue dentée** en haut à droite de l’écran.

    ![](images/AzureLabs-Lab302b-15.png)

13. Copiez la **clé de formation** et collez-la dans un *bloc-notes*, pour une utilisation ultérieure.

    ![](images/AzureLabs-Lab302b-16.png)

14. Copiez également votre **ID de projet**, puis collez-le dans votre fichier *bloc-notes* pour une utilisation ultérieure.

    ![](images/AzureLabs-Lab302b-16a.png)

## <a name="chapter-3---set-up-the-unity-project"></a>Chapitre 3-configurer le projet Unity

Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **nouveau**.

    ![](images/AzureLabs-Lab302b-17.png)

2.  Vous devez maintenant fournir un nom de projet Unity. Insérez **AzureCustomVision.** Assurez-vous que le modèle de projet est défini sur **3D**. Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés). Ensuite, cliquez sur **créer un projet**.

    ![](images/AzureLabs-Lab302b-18.png)

3.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**. Accédez à **modifier* > les*Préférences** , puis à partir de la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio 2017**. Fermez la fenêtre **Préférences** .

    ![](images/AzureLabs-Lab302b-19.png)

4.  Accédez ensuite à **fichier > paramètres de build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le bouton **changer de plateforme** pour appliquer votre sélection.

    ![](images/AzureLabs-Lab302b-20.png)

5.  Tout en conservant les **paramètres de génération de > de fichiers** et assurez-vous que:

    1.  L' **appareil cible** est défini sur **Hololens**

        > Pour les casques immersifs, définissez **appareil cible** sur *n’importe quel appareil*.
        
    2.  Le **type de build** est **D3D**
    3.  Le **SDK** est configuré sur le **dernier installé**
    4.  **Version de Visual Studio** définie sur le **dernier installé**
    5.  La **génération et l’exécution** sont définies sur l' **ordinateur local**
    6.  Enregistrez la scène et ajoutez-la à la Build. 

        1. Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**. Une fenêtre d’enregistrement s’affiche.

            ![](images/AzureLabs-Lab302b-21.png)

        2. Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le Scenes.

            ![](images/AzureLabs-Lab302b-22.png)

        3. Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier:* , tapez **CustomVisionScene**, puis cliquez sur **Enregistrer**.

            ![](images/AzureLabs-Lab302b-23.png)

            > Sachez que vous devez enregistrer vos scènes Unity dans le dossier *ressources* , car elles doivent être associées au projet Unity. La création du dossier scenes (et d’autres dossiers similaires) est un moyen classique de structurer un projet Unity.
            
    7.  Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.

        ![](images/AzureLabs-Lab302b-24.png)

6.  Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* .

7. Dans ce volet, quelques paramètres doivent être vérifiés:

    1.  Sous l’onglet **autres paramètres** :

        1.  La **version du runtime de script** doit être **expérimentale (.net 4,6 équivalent)** , ce qui déclenche la nécessité de redémarrer l’éditeur.

        2. Le **backend de script** doit être **.net**

        3. Le **niveau de compatibilité** de l’API doit être **.net 4,6**

        ![](images/AzureLabs-Lab302b-25.png)

    2.  Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:

        1. **InternetClient**

        2.  **Webcam**

        3. **Cravate**

        ![](images/AzureLabs-Lab302b-26.png)

    3.  Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.

    ![](images/AzureLabs-Lab302b-27.png)

8.  De retour dans les *paramètres de build* les *\# projets Unit C* ne sont plus grisés; cochez la case en regard de cette option.

9.  Fermez la fenêtre Paramètres de Build.

10.  Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).


## <a name="chapter-4---importing-the-newtonsoft-dll-in-unity"></a>Chapitre 4-importation de la DLL Newtonsoft dans Unity

> [!IMPORTANT]
> Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [Azure-Mr-302b. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/Azure-MR-302b.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au [chapitre 6 ](#chapter-6---create-the-customvisionanalyser-class).

Ce cours requiert l’utilisation de la bibliothèque **Newtonsoft** , que vous pouvez ajouter en tant que dll à vos ressources. Le package contenant [cette bibliothèque peut être téléchargé à partir de ce lien](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/NewtonsoftDLL.unitypackage).
Pour importer la bibliothèque Newtonsoft dans votre projet, utilisez le package Unity fourni avec ce cours.

1.  Ajoutez le fichier *. pour Unity* à Unity à l’aide de l’option de menu  **package* *personnalisé* du *package* > d'*importation* de *ressources* > * .

2.  Dans la zone **importer le package Unity** qui s’affiche, vérifiez que tous les plug- **ins** sous (et y compris) sont sélectionnés.

    ![](images/AzureLabs-Lab302b-28.png)

3.  Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.

4.  Accédez au dossier **Newtonsoft** sous **plug-ins** dans la vue projet et sélectionnez le *plug-in Newtonsoft. JSON*.

    ![](images/AzureLabs-Lab302b-29.png)

5.  Une fois le *plug-in Newtonsoft. JSON* sélectionné, assurez-vous que **toutes les plateformes** sont décochées, vérifiez que **WSAPlayer** est également **désactivé**, puis cliquez sur **appliquer**. Cela vous permet de vérifier que les fichiers sont correctement configurés.

    ![](images/AzureLabs-Lab302b-30.png)

    > [!NOTE]
    > Le marquage de ces plug-ins permet de les configurer pour qu’ils soient utilisés uniquement dans l’éditeur Unity. Il y en a un ensemble différent dans le dossier WSA qui sera utilisé une fois que le projet est exporté d’Unity.

6.  Ensuite, vous devez ouvrir le dossier **WSA** , dans le dossier **Newtonsoft** . Vous verrez une copie du même fichier que celui que vous venez de configurer. Sélectionnez le fichier, puis, dans l’inspecteur, vérifiez que
    -   **Aucune plateforme** n' est désactivée 
    -   **uniquement** **WSAPlayer** est **activé**
    -   L’option ne pas **traiter le processus** est **activée**

    ![](images/AzureLabs-Lab302b-31.png)

## <a name="chapter-5---camera-setup"></a>Chapitre 5-Configuration de l’appareil photo

1.  Dans le panneau hiérarchie, sélectionnez l' *appareil photo principal*.

2.  Une fois sélectionné, vous pouvez voir tous les composants de la *caméra principale* dans le *panneau Inspecteur*.

    1.  L’objet *Camera* doit être nommé **Camera main** (Notez l’orthographe!)

    2.  La balise principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe!)

    3.  Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0

    4.  Affectez à **effacer les indicateurs** la **couleur unie** (ignorer ce point pour le casque immersif).

    5.  Définissez la couleur d' **arrière-plan** du composant Camera sur **Black, alpha 0 (Code hex: #00000000)** (ignorez-le pour le casque immersif).

    ![](images/AzureLabs-Lab302b-32.png)


## <a name="chapter-6---create-the-customvisionanalyser-class"></a>Chapitre 6-créer la classe CustomVisionAnalyser.

À ce stade, vous êtes prêt à écrire du code.

Vous allez commencer par la classe *CustomVisionAnalyser* .

> [!NOTE]
> Les appels au **service vision personnalisée** effectués dans le code ci-dessous sont effectués à l’aide de l' **API REST Custom vision**. À l’aide de ce guide, vous allez apprendre à implémenter et à utiliser cette API (utile pour comprendre comment implémenter des éléments similaires). Sachez que Microsoft propose un **Kit de développement logiciel (SDK) service vision personnalisée** qui peut également être utilisé pour effectuer des appels au service. Pour plus d’informations, consultez l’article du [Kit de développement logiciel (SDK) service vision personnalisée](https://github.com/Microsoft/Cognitive-CustomVision-Windows/) .

Cette classe est chargée des opérations suivantes:

-   Chargement de la dernière image capturée sous la forme d’un tableau d’octets.

-   Envoi du tableau d’octets à votre instance Azure *service vision personnalisée* à des fins d’analyse.

-   Réception de la réponse sous forme de chaîne JSON.

-   La désérialisation de la réponse et le passage de la prédiction résultante à la classe *SceneOrganiser* , qui s’occupera du mode d’affichage de la réponse.

Pour créer cette classe:

1.  Cliquez avec le bouton droit sur le *dossier Asset* situé dans le *panneau Projet*, puis cliquez sur **créer un dossier >** . Appelez le dossier **scripts**.

    ![](images/AzureLabs-Lab302b-33.png)

2.  Double-cliquez sur le dossier que vous venez de créer pour l’ouvrir.

3.  Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer** > un**script C\#** . Nommez le script *CustomVisionAnalyser*.

4.  Double-cliquez sur le nouveau script *CustomVisionAnalyser* pour l’ouvrir avec **Visual Studio**.

5.  Mettez à jour les espaces de noms en haut de votre fichier pour qu’ils correspondent à ce qui suit:

    ```csharp
    using System.Collections;
    using System.IO;
    using UnityEngine;
    using UnityEngine.Networking;
    using Newtonsoft.Json;
    ```

6.  Dans la classe *CustomVisionAnalyser* , ajoutez les variables suivantes:

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
    > Veillez à insérer votre **clé** de prédiction dans la variable **PredictionKey** et votre **point de terminaison** de prédiction dans la variable **predictionEndpoint** . Vous les avez copiées dans le *bloc-notes* plus tôt dans le cours.

7.  Le code pour **éveillé ()** doit maintenant être ajouté pour initialiser la variable d’instance:

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

8.  Supprimez les méthodes **Start ()** et **Update ()** .

9.  Ensuite, ajoutez la Coroutine (avec la méthode statique **GetImageAsByteArray ()** en dessous de celle-ci), qui obtiendra les résultats de l’analyse de l’image capturée par la classe *ImageCapture* .

    > [!NOTE]
    > Dans la Coroutine **AnalyseImageCapture** , il y a un appel à la classe *SceneOrganiser* que vous êtes encore en cours de création. Par conséquent, **laissez ces lignes commentées pour l’instant**.

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

10.  Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenirà Unity.

## <a name="chapter-7---create-the-customvisionobjects-class"></a>Chapitre 7-créer la classe CustomVisionObjects

La classe que vous allez créer est maintenant la classe *CustomVisionObjects* .

Ce script contient un certain nombre d’objets utilisés par d’autres classes pour sérialiser et désérialiser les appels passés au *service vision personnalisée*.

> [!WARNING]
> Il est important de noter le point de terminaison que la Service Vision personnalisée vous fournit, car la structure JSON ci-dessous a été configurée pour fonctionner avec [*Custom vision prédiction v 2.0*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/450e4ba4d72542e889d93fd7b8e960de/operations/5a6264bc40d86a0ef8b2c290). Si vous disposez d’une version différente, vous devrez peut-être mettre à jour la structure ci-dessous.

Pour créer cette classe:

1.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** . Appelez le script *CustomVisionObjects*.

2.  Double-cliquez sur le nouveau script **CustomVisionObjects** pour l’ouvrir avec **Visual Studio**.

3.  Ajoutez les espaces de noms suivants au début du fichier:

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  Supprimez les méthodes **Start ()** et **Update ()** à l’intérieur de la classe *CustomVisionObjects* ; Cette classe doit maintenant être vide.

5.  Ajoutez les classes suivantes **en dehors** de la classe *CustomVisionObjects* . Ces objets sont utilisés par la bibliothèque *Newtonsoft* pour sérialiser et désérialiser les données de réponse:

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

## <a name="chapter-8---create-the-voicerecognizer-class"></a>Chapitre 8-créer la classe VoiceRecognizer

Cette classe reconnaît la saisie vocale de l’utilisateur.

Pour créer cette classe:

1.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** . Appelez le script *VoiceRecognizer*.

2.  Double-cliquez sur le nouveau script **VoiceRecognizer** pour l’ouvrir avec **Visual Studio**.

3.  Ajoutez les espaces de noms suivants au-dessus de la classe *VoiceRecognizer* :

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.Windows.Speech;
    ```

4.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe *VoiceRecognizer* , au-dessus de la méthode *Start ()* :

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

5.  Ajoutez les méthodes **éveillé ()** et **Start ()** , dont la dernière configurera les *Mots clés* utilisateur pour qu’ils soient reconnus lors de l’Association d’une balise à une image:

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

6.  Supprimez la méthode **Update ()** .

7.  Ajoutez le gestionnaire suivant, qui est appelé chaque fois que l’entrée vocale est reconnue:

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

8.  Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenirà Unity.

> [!NOTE]
> Ne vous inquiétez pas du code qui peut sembler avoir une erreur, car vous fournirez bientôt d’autres classes, ce qui les corrigera.

## <a name="chapter-9---create-the-customvisiontrainer-class"></a>Chapitre 9-créer la classe CustomVisionTrainer

Cette classe chaînera une série d’appels Web pour former l' *service vision personnalisée*. Chaque appel sera expliqué en détail juste au-dessus du code.

Pour créer cette classe:

1.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** . Appelez le script *CustomVisionTrainer*.

2.  Double-cliquez sur le nouveau script *CustomVisionTrainer* pour l’ouvrir avec **Visual Studio**.

3.  Ajoutez les espaces de noms suivants au-dessus de la classe *CustomVisionTrainer* :

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Collections.Generic;
    using System.IO;
    using System.Text;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe *CustomVisionTrainer* , au-dessus de la méthode **Start ()** . 

    > [!NOTE]
    > L’URL de formation utilisée ici est fournie dans la documentation *Custom vision formation 1,2* et présente la structure suivante: https://southcentralus.api.cognitive.microsoft.com/customvision/v1.2/Training/projects/{projectId}/  
    > Pour plus d’informations, consultez l' [*API de référence de Custom vision formation v 1.2*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).

    > [!WARNING]
    > Il est important de noter le point de terminaison que la Service Vision personnalisée vous fournit pour le mode d’apprentissage, car la structure JSON utilisée (dans la classe **CustomVisionObjects** ) a été configurée pour fonctionner avec [*Custom vision formation v 1.2*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f). Si vous disposez d’une version différente, vous devrez peut-être mettre à jour la structure des *objets* .

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
    > Veillez à ajouter la valeur de **clé de service** (clé de formation) et la valeur d' **ID de projet** , que vous avez notée précédemment; Il s’agit des valeurs que vous avez [collectées à partir du portail plus haut dans le cours (chapitre 2, étape 10)](#chapter-2---training-your-custom-vision-oroject).

5.  Ajoutez les méthodes **Start ()** et **éveillé ()** suivantes. Ces méthodes sont appelées lors de l’initialisation et contiennent l’appel pour configurer l’interface utilisateur:

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

6.  Supprimez la méthode **Update ()** . Cette classe n’en a pas besoin.

7.  Ajoutez la méthode **RequestTagSelection ()** . Cette méthode est la première à être appelée lorsqu’une image a été capturée et stockée dans l’appareil et qu’elle est maintenant prête à être envoyée à la *service vision personnalisée*pour l’effectuer. Cette méthode affiche, dans l’interface utilisateur de formation, un ensemble de mots clés que l’utilisateur peut utiliser pour baliser l’image capturée. Elle alerte également la classe *VoiceRecognizer* pour commencer à écouter l’utilisateur pour l’entrée vocale.

    ```csharp
        internal void RequestTagSelection()
        {
            trainingUI_TextMesh.gameObject.SetActive(true);
            trainingUI_TextMesh.text = $" \nUse voice command \nto choose between the following tags: \nMouse\nKeyboard \nor say Discard";

            VoiceRecognizer.Instance.keywordRecognizer.Start();
        }
    ```

8.  Ajoutez la méthode **VerifyTag ()** . Cette méthode recevra l’entrée vocale reconnue par la classe **VoiceRecognizer** et vérifiera sa validité, puis commencera le processus d’apprentissage.

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

9.  Ajoutez la méthode **SubmitImageForTraining ()** . Cette méthode démarre le processus de formation Service Vision personnalisée. La première étape consiste à récupérer l' **ID** de balise à partir du service associé à l’entrée vocale validée de l’utilisateur. L' **ID** de balise sera ensuite téléchargé avec l’image.

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

10. Ajoutez la méthode **TrainCustomVisionProject ()** . Une fois que l’image a été envoyée et balisée, cette méthode est appelée. Il créera une nouvelle itération qui sera formée avec toutes les images précédentes soumises au service, ainsi que l’image qui vient d’être téléchargée. Une fois l’apprentissage terminé, cette méthode appellera une méthode pour définir l' **itération** nouvellement créée **par défaut**, afin que le point de terminaison que vous utilisez pour l’analyse soit la dernière itération formée.

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

11. Ajoutez la méthode **SetDefaultIteration ()** . Cette méthode définit l’itération précédemment créée et formée comme *valeur par défaut*. Une fois l’opération terminée, cette méthode devra supprimer l’itération précédente existante dans le service. Au moment de la rédaction de ce cours, il existe une limite de dix (10) itérations maximum autorisées à exister simultanément dans le service.

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

12. Ajoutez la méthode **DeletePreviousIteration ()** . Cette méthode recherche et supprime l’itération précédente non définie par défaut:

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

13. La dernière méthode à ajouter dans cette classe est la méthode **GetImageAsByteArray ()** , utilisée sur les appels Web pour convertir l’image capturée dans un tableau d’octets.

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

14. Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenirà Unity.

## <a name="chapter-10---create-the-sceneorganiser-class"></a>Chapitre 10-créer la classe SceneOrganiser

Cette classe effectuera les opérations suivantes:

-   Créez un objet **curseur** à attacher à l’appareil photo principal.

-   Créez un objet **étiquette** qui s’affiche lorsque le service reconnaît les objets réels.

-   Configurez la caméra principale en y joignant les composants appropriés.

-   En **mode analyse**, générez les étiquettes au moment de l’exécution, dans l’espace universel approprié par rapport à la position de la caméra principale, puis affichez les données reçues de la service vision personnalisée.

-   En **mode d’apprentissage**, générez l’interface utilisateur qui affichera les différentes étapes du processus d’apprentissage.

Pour créer cette classe:

1.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** . Nommez le script *SceneOrganiser*.

2.  Double-cliquez sur le nouveau script *SceneOrganiser* pour l’ouvrir avec **Visual Studio**.

3.  Vous n’aurez besoin que d’un seul espace de noms, supprimez les autres au-dessus de la classe *SceneOrganiser* :

    ```csharp
    using UnityEngine;
    ```

4.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe *SceneOrganiser* , au-dessus de la méthode **Start ()** :

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

5.  Supprimez les méthodes **Start ()** et **Update ()** .

6.  Juste en dessous des variables, ajoutez la méthode **éveillé ()** , qui initialisera la classe et configurera la scène.

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

7.  Ajoutez à présent la méthode **CreateCameraCursor ()** qui crée et positionne le curseur principal de l’appareil photo, et la méthode **CreateLabel ()** , qui crée l’objet **étiquette d’analyse** .

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

8. Ajoutez la méthode **SetCameraStatus ()** , qui gérera les messages destinés à la maille de texte qui fournit l’état de l’appareil photo.

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

9. Ajoutez les méthodes **PlaceAnalysisLabel ()** et **SetTagsToLastLabel ()** , qui génèrent et affichent les données de la service vision personnalisée dans la scène.

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

10. Enfin, ajoutez la méthode **CreateTrainingUI ()** , qui générera l’interface utilisateur en affichant les différentes étapes du processus d’apprentissage lorsque l’application est en mode d’apprentissage. Cette méthode est également exploitable pour créer l’objet d’état de l’appareil photo.

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

11. Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenirà Unity.

> [!IMPORTANT]
> Avant de continuer, ouvrez la classe **CustomVisionAnalyser** et, dans la méthode **AnalyseLastImageCaptured ()** , *supprimez les marques de commentaire* des lignes suivantes:
>
> ```csharp
>   AnalysisObject analysisObject = new AnalysisObject();
>   analysisObject = JsonConvert.DeserializeObject<AnalysisObject>(jsonResponse);
>   SceneOrganiser.Instance.SetTagsToLastLabel(analysisObject);
> ```

## <a name="chapter-11---create-the-imagecapture-class"></a>Chapitre 11-créer la classe ImageCapture

La classe suivante que vous allez créer est la classe *ImageCapture* .

Cette classe est chargée des opérations suivantes:

-   Capture d’une image à l’aide de la caméra HoloLens et stockage dans le dossier de l' *application* .

-   Gestion des gestes TAP de l’utilisateur.

-   Maintien de la valeur *enum* qui détermine si l’application s’exécutera en mode d' *analyse* ou en mode d' *apprentissage* .

Pour créer cette classe:

1.  Accédez au dossier **scripts** que vous avez créé précédemment.

2.  Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer > script C\#** . Nommez le script *ImageCapture*.

3.  Double-cliquez sur le nouveau script **ImageCapture** pour l’ouvrir avec **Visual Studio**.

4.  Remplacez les espaces de noms en haut du fichier par les éléments suivants:

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    using UnityEngine.XR.WSA.WebCam;
    ```

5.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe *ImageCapture* , au-dessus de la méthode **Start ()** :

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

6.  Vous devez maintenant ajouter le code des méthodes **éveillés ()** et **Start ()** :

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

7.  Implémentez un gestionnaire qui sera appelé quand un mouvement TAP se produit.

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
    > En mode *analyse* , la méthode **TapHandler** agit comme un commutateur pour démarrer ou arrêter la boucle de capture photo.
    >
    > En mode d' *apprentissage* , une image est capturée à partir de l’appareil photo.
    >
    > Lorsque le curseur est vert, cela signifie que l’appareil photo est disponible pour prendre l’image.
    >
    > Lorsque le curseur est rouge, cela signifie que l’appareil photo est occupé.

8.  Ajoutez la méthode utilisée par l’application pour démarrer le processus de capture d’image et stocker l’image.

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

9.  Ajoutez les gestionnaires qui seront appelés lorsque la photo a été capturée et le moment où elle sera prête à être analysée. Le résultat est ensuite transmis à *CustomVisionAnalyser* ou *CustomVisionTrainer* selon le mode sur lequel le code est défini.

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

10. Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenirà Unity.

11. Maintenant que tous les scripts ont été exécutés, revenez dans l’éditeur Unity, puis cliquez et faites glisser la classe **SceneOrganiser** du dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*.

## <a name="chapter-12---before-building"></a>Chapitre 12-avant génération

Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre HoloLens.

Avant cela, assurez-vous que:

- Tous les paramètres mentionnés dans le [Chapitre 2](#chapter-2---training-your-custom-vision-project) sont correctement définis.

- Tous les champs de l' **appareil photo principal**, du panneau Inspecteur, sont correctement affectés.

- Le script **SceneOrganiser** est attaché à l’objet **Camera principal** .

- Veillez à insérer votre **clé** de prédiction dans la variable **predictionKey** .

- Vous avez inséré votre **point de terminaison** de prédiction dans la variable **predictionEndpoint** .

- Vous avez inséré votre **clé de formation** dans la variable **trainingKey** de la classe *CustomVisionTrainer* .

- Vous avez inséré votre **ID de projet** dans la variable **ProjectId** de la classe *CustomVisionTrainer* .

## <a name="chapter-13---build-and-sideload-your-application"></a>Chapitre 13-créer et chargement votre application

Pour commencer le processus de *génération* :

1.  Accédez à **fichier > paramètres de build**.

2.  **Projets Tick Unity C\#** .

3.  Cliquez sur **Build**. Unity lance une fenêtre de l' **Explorateur de fichiers** , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application. Créez ce dossier maintenant, puis nommez-le **application**. Ensuite, avec le dossier d' **application** sélectionné, cliquez sur **Sélectionner un dossier**.

4.  Unity commence à générer votre projet dans le dossier de l' **application** .

5.  Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).

Pour effectuer un déploiement sur HoloLens:

1.  Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur**. Pour ce faire :

    1.  Tout en portant votre HoloLens, ouvrez les **paramètres**.

    2.  Accéder au **réseau &**  > **Options avancées** **de Wi-Fi** > Internet

    3.  Notez l’adresse **IPv4** .

    4.  Ensuite, revenez aux **paramètres**, puis pour **mettre à jour & sécurité** > **pour les développeurs**

    5.  Définissez **le mode développeur sur**.

2.  Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.

3.  Dans la *configuration* de lasolution, sélectionnez Déboguer.

4.  Dans la *plateforme*de la solution, sélectionnez **x86, ordinateur distant**. Vous serez invité à insérer l' **adresse IP** d’un périphérique distant (le HoloLens, dans ce cas, que vous avez noté).

    ![](images/AzureLabs-Lab302b-34.png)

5. Accédez au menu **générer** , puis cliquez sur **déployer la solution** pour chargement l’application à votre HoloLens.

6. Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.

> [!NOTE]
> Pour effectuer un déploiement sur un casque immersif, définissez la plateforme de la **solution** sur *ordinateur local*et définissez la **configuration** sur déboguer, avec *x86* comme **plateforme**. Déployez ensuite sur l’ordinateur local, à l’aide de l’élément de menu **générer** , en sélectionnant *déployer la solution*. 

## <a name="to-use-the-application"></a>Pour utiliser l’application:

Pour basculer la fonctionnalité de l’application entre le mode d' *apprentissage* et le mode de prédiction, vous devez mettre à jour la variable **AppMode** , située dans la méthode **éveillé ()** située dans la classe *ImageCapture* .

```
        // Change this flag to switch between Analysis mode and Training mode 
        AppMode = AppModes.Training;
```
ou Gestionnaire de configuration
```
        // Change this flag to switch between Analysis mode and Training mode 
        AppMode = AppModes.Analysis;
```

En mode d' *apprentissage* :

- Regardez la **souris** ou le **clavier** et utilisez le **mouvement TAP**.

- Ensuite, du texte s’affiche pour vous demander de fournir une balise.

- Disons **la souris** ou le **clavier**.


En mode de prédiction:

- Examinez un objet et utilisez le **mouvement TAP**.

- Du texte s’affiche pour indiquer l’objet détecté, avec la probabilité la plus élevée (cette opération est normalisée).

## <a name="chapter-14---evaluate-and-improve-your-custom-vision-model"></a>Chapitre 14-évaluer et améliorer votre modèle de Custom Vision

Pour améliorer la précision de votre service, vous devrez continuer à former le modèle utilisé pour la prédiction. Pour ce faire, vous pouvez utiliser votre nouvelle application, à la fois avec les modes de *formation* et de prédiction, avec ceux qui vous demandent de visiter le portail, ce qui est abordé dans ce chapitre. Préparez-vous à revisiter votre portail plusieurs fois, afin d’améliorer continuellement votre modèle.

1. Accédez à nouveau à votre portail Azure Custom Vision et, une fois que vous êtes dans votre projet , sélectionnez l’onglet prédictions (à partir du centre en haut de la page):

    ![](images/AzureLabs-Lab302b-35.png)

2. Vous verrez toutes les images qui ont été envoyées à votre service pendant l’exécution de votre application. Si vous pointez sur les images, elles vous fourniront les prédictions qui ont été effectuées pour cette image:

    ![](images/AzureLabs-Lab302b-36.png)

3. Sélectionnez l’une de vos images pour l’ouvrir. Une fois ouvert, vous verrez les prédictions effectuées pour cette image à droite. Si les prédictions sont correctes et que vous souhaitez ajouter cette image au modèle d’apprentissage de votre service, cliquez sur la zone de texte *mes balises* , puis sélectionnez la balise que vous souhaitez associer. Lorsque vous avez terminé, cliquez sur le bouton *enregistrer et fermer* en bas à droite, puis passez à l’image suivante.

    ![](images/AzureLabs-Lab302b-37.png)

4. Une fois que vous revenez à la grille des images, vous remarquerez que les images auxquelles vous avez ajouté des balises (et enregistrées) seront supprimées. Si vous trouvez des images dont vous pensez que vous n’avez pas besoin de votre élément balisé, vous pouvez les supprimer en cliquant sur le bouton de l’image (cette opération peut s’effectuer pour plusieurs images), puis en cliquant sur *supprimer* dans le coin supérieur droit de la page de grille. Dans le menu contextuel qui suit, vous pouvez cliquer sur *Oui, supprimer* ou *non*pour confirmer la suppression ou l’annuler, respectivement. 

    ![](images/AzureLabs-Lab302b-38.png)

5. Lorsque vous êtes prêt à continuer, cliquez sur le bouton vert *train* en haut à droite. Votre modèle de service sera formé avec toutes les images que vous avez fournies (ce qui le rendra plus précis). Une fois l’apprentissage terminé, veillez à cliquer une fois de plus sur le bouton *créer par défaut* , afin que votre *URL* de prédiction continue à utiliser l’itération la plus récente de votre service.

    ![](images/AzureLabs-Lab302b-39.png) ![](images/AzureLabs-Lab302b-40.png)

## <a name="your-finished-custom-vision-api-application"></a>Votre application API Custom Vision terminée

Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API Azure Custom Vision pour reconnaître des objets réels, former le modèle de service et afficher la confiance de ce qui a été observé.

![](images/AzureLabs-Lab302b-00.png)

## <a name="bonus-exercises"></a>Exercices bonus

### <a name="exercise-1"></a>Exercice 1

Formez votre **service vision personnalisée** pour qu’il reconnaisse plus d’objets.

### <a name="exercise-2"></a>Exercice 2

Pour vous familiariser avec ce que vous avez appris, effectuez les exercices suivants:

Émettre un signal sonore lorsqu’un objet est reconnu.

### <a name="exercise-3"></a>Exercice 3

Utilisez l’API pour reformer votre service avec les mêmes images que celles que votre application analyse, afin de rendre le service plus précis (effectuer la prédiction et la formation simultanément).
