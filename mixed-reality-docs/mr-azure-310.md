---
title: MR et Azure 310-détection d’objets
description: Suivez ce cours pour apprendre à former un modèle de Machine Learning, puis à utiliser le modèle formé pour reconnaître des objets similaires et leur position dans le monde réel à partir d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, vision personnalisée, détection d’objets, réalité mixte, Académie, Unity, didacticiel, API, hololens
ms.openlocfilehash: 89ee79943a88de8a34c679ae33621db5770908b0
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63544458"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

# <a name="mr-and-azure-310-object-detection"></a>Mr et Azure 310: Détection d’objet

Dans ce cours, vous allez apprendre à reconnaître le contenu visuel personnalisé et sa position spatiale dans une image fournie, en utilisant les fonctionnalités de «détection d’objets» d’Azure Custom Vision dans une application de réalité mixte.

Ce service vous permet d’effectuer l’apprentissage d’un modèle de Machine Learning à l’aide d’images d’objet. Vous allez ensuite utiliser le modèle formé pour reconnaître des objets similaires et se rapprocher de leur emplacement dans le monde réel, tel que fourni par la capture de l’appareil photo de Microsoft HoloLens ou d’une caméra qui se connecte à un PC pour les casques immersifs (VR).

![résultat du cours](images/AzureLabs-Lab310-00.png)

**Azure Custom vision, la détection d’objets** est un service Microsoft qui permet aux développeurs de créer des classifieurs d’images personnalisées. Ces classifieurs peuvent ensuite être utilisés avec de nouvelles images pour détecter des objets dans cette nouvelle image, en fournissant des **limites de zone** au sein de l’image elle-même. Le service fournit un portail en ligne simple et facile à utiliser pour simplifier ce processus. Pour plus d’informations, consultez les liens suivants:

* [Page Custom Vision Azure](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home)
* [Limites et quotas](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/limits-and-quotas)

À la fin de ce cours, vous disposerez d’une application de réalité mixte qui sera en mesure d’effectuer les opérations suivantes:

1. L’utilisateur sera en *mesure de* pointer vers un objet, qu’il a formé à l’aide du service vision personnalisée Azure, détection d’objet. 
2. L’utilisateur utilise le geste *Tap* pour capturer une image de ce qu’il examine.
3. L’application enverra l’image à la Service Vision personnalisée Azure.
4. Il y aura une réponse du service qui affichera le résultat de la reconnaissance sous forme de texte d’espace universel. Pour ce faire, vous devez utiliser le suivi spatial de Microsoft HoloLens, afin de comprendre la position universelle de l’objet reconnu, puis l’utilisation de la *balise* associée à ce qui est détecté dans l’image, pour fournir le texte de l’étiquette.

Ce cours couvre également le chargement manuel d’images, la création de balises et l’apprentissage du service, pour reconnaître différents objets (dans l’exemple fourni, une tasse), en définissant la *zone limite* dans l’image que vous envoyez. 

> [!IMPORTANT]
> Après la création et l’utilisation de l’application, le développeur doit revenir à la Service Vision personnalisée Azure, identifier les prédictions effectuées par le service et déterminer si elles sont correctes ou non (en marquant tout ce que le service a manqué) et réglage des *zones englobantes*). Le service peut ensuite être réformé, ce qui augmente la probabilité qu’il reconnaisse les objets réels.

Ce cours vous apprend à obtenir les résultats de la Service Vision personnalisée Azure, la détection d’objets, dans un exemple d’application à base d’Unity. Il vous faudra appliquer ces concepts à une application personnalisée que vous pouvez générer.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 310: Détection d’objet</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:

- Un PC de développement
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [Le dernier Kit de développement logiciel Windows 10](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [Unity 2017,4 LTS](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [Visual Studio 2017](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [Microsoft HoloLens](https://docs.microsoft.com/windows/mixed-reality/hololens-hardware-details) avec mode développeur activé
- Accès à Internet pour l’installation d’Azure et la récupération de Service Vision personnalisée
-  Une série d’au moins quinze (15) images sont requises) pour chaque objet que vous souhaitez que le Custom Vision reconnaître. Si vous le souhaitez, vous pouvez utiliser les images déjà fournies dans ce cours, [une série de tasses](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).
2.  Configurez et testez votre HoloLens. Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur). 

Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1---the-custom-vision-portal"></a>Chapitre 1-portail Custom Vision

Pour utiliser le **service vision personnalisée Azure**, vous devez configurer une instance de ce dernier pour qu’il soit mis à la disposition de votre application.

1.  Accédez [à la page principale de **service vision personnalisée** ](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).

2.  Cliquez sur **prise en main**.

    ![](images/AzureLabs-Lab310-01.png)

3.  Connectez-vous au portail Custom Vision.

    ![](images/AzureLabs-Lab310-02.png)

4.  Si vous n’avez pas encore de compte Azure, vous devez en créer un. Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.

5.  Une fois que vous êtes connecté pour la première fois, vous êtes invité à entrer dans le panneau *des conditions d’accès* . Cochez la case pour *accepter les termes du contrat*. Cliquez ensuite sur **J’accepte**.

    ![](images/AzureLabs-Lab310-03.png)

6.  Après avoir accepté les termes, vous vous trouvez maintenant dans la section *mes projets* . Cliquez sur **nouveau projet**.

    ![](images/AzureLabs-Lab310-04.png)

7.  Un onglet s’affiche sur le côté droit, ce qui vous invite à spécifier certains champs pour le projet.

    1.  Insérer un nom pour votre projet

    2.  Insérer une description pour votre projet (**facultatif**)

    3.  Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.

        ![](images/AzureLabs-Lab310-05.png)

        > [!NOTE]
        > Si vous souhaitez [en savoir plus sur les groupes de ressources Azure, accédez aux documents associés](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal) .

    4.  Définissez les **types de projets** en tant que **détection d’objet (** préversion).

8.  Une fois que vous avez terminé, cliquez sur **créer un projet**. vous êtes alors redirigé vers la page du projet service vision personnalisée.


## <a name="chapter-2---training-your-custom-vision-project"></a>Chapitre 2-formation de votre projet Custom Vision

Une fois dans le portail Custom Vision, votre objectif principal est de former votre projet à la reconnaissance d’objets spécifiques dans les images.

Vous avez besoin d’au moins quinze (15) images pour chaque objet que vous souhaitez que votre application reconnaisse. Vous pouvez utiliser les images fournies avec ce cours ([une série de tasses](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).

Pour former votre projet Custom Vision:

1.  Cliquez sur le **+** bouton en regard de balises.

    ![](images/AzureLabs-Lab310-06.png)

2.  Ajoutez un **nom** pour la balise qui sera utilisée pour associer vos images à. Dans cet exemple, nous utilisons des images de tasses pour la reconnaissance, vous avez donc nommé la balise pour This, **Cup**. Cliquez sur **Enregistrer** une fois l’opération terminée.

    ![](images/AzureLabs-Lab310-07.png)

3.  Vous remarquerez  que votre balise a été ajoutée (vous devrez peut-être recharger votre page pour qu’elle apparaisse). 

    ![](images/AzureLabs-Lab310-08.png)

4.  Cliquez sur **Ajouter des images** au centre de la page.

    ![](images/AzureLabs-Lab310-09.png)

5.  Cliquez sur **Parcourir les fichiers locaux**et recherchez les images que vous souhaitez télécharger pour un objet, avec un minimum de 15 (15).

    > [!TIP]
    >  Vous pouvez sélectionner plusieurs images à la fois, à télécharger.

    ![](images/AzureLabs-Lab310-10.png)

6.  Appuyez sur **charger les fichiers** une fois que vous avez sélectionné toutes les images avec lesquelles vous souhaitez former le projet. Le chargement des fichiers va commencer. Une fois que vous avez confirmé le téléchargement, cliquez sur **terminé**.

    ![](images/AzureLabs-Lab310-11.png)

7.  À ce stade, vos images sont chargées, mais elles ne sont pas marquées.

    ![](images/AzureLabs-Lab310-12.png)

8.  Pour baliser vos images, utilisez la souris. Au fur et à mesure que vous pointez sur votre image, une sélection de sélection vous aidera en dessinant automatiquement une sélection autour de votre objet. Si ce n’est pas exact, vous pouvez créer les vôtres. Pour ce faire, vous devez maintenir le bouton gauche de la souris enfoncé et faire glisser la région de sélection pour englober votre objet. 

    ![](images/AzureLabs-Lab310-13.png) 

9. Après la sélection de votre objet dans l’image, une petite invite vous demande d’ajouter une *balise de région*. Sélectionnez votre balise créée précédemment («Cup», dans l’exemple ci-dessus), ou si vous ajoutez d’autres balises, tapez ce qui se trouve dans et cliquez sur le bouton **+ (plus)** .

    ![](images/AzureLabs-Lab310-14.png) 

10. Pour baliser l’image suivante, vous pouvez cliquer sur la flèche à droite du panneau ou fermer le panneau des balises (en cliquant sur le **X** dans le coin supérieur droit du panneau), puis sur l’image suivante. Une fois que l’image suivante est prête, répétez la même procédure. Procédez ainsi pour toutes les images que vous avez chargées, jusqu’à ce qu’elles soient toutes marquées. 

    > [!NOTE]
    >  Vous pouvez sélectionner plusieurs objets dans la même image, comme l’image ci-dessous: 
    > 
    > ![](images/AzureLabs-Lab310-15.png)

11. Une fois que vous les avez balisées, cliquez sur le bouton **balisé** , à gauche de l’écran, pour afficher les images avec balises. 

    ![](images/AzureLabs-Lab310-16.png)

12. Vous êtes maintenant prêt à former votre service. Cliquez sur le bouton **former** et la première itération d’apprentissage commencera.

    ![](images/AzureLabs-Lab310-17.png)

    ![](images/AzureLabs-Lab310-18.png)

13. Une fois qu’elle est créée, vous pouvez voir deux boutons nommés **créer par défaut** et **URL**de prédiction. Cliquez d’abord sur **créer par défaut** , puis sur **URL**de prédiction.

    ![](images/AzureLabs-Lab310-19.png)

    > [!NOTE] 
    > Le point de terminaison fourni à partir de ce est défini sur l' *itération* qui a été marquée comme valeur par défaut. Par conséquent, si vous effectuez ultérieurement une nouvelle *itération* et la mettez à jour par défaut, vous n’aurez pas besoin de modifier votre code.

14. Une fois que vous avez cliqué **sur URL**de prédiction, ouvrez le *bloc-notes*, puis copiez et collez l' **URL** (également appelée « **prédiction-point de terminaison»** ) et la **clé de prédiction de service**, afin de pouvoir la récupérer lorsque vous en aurez besoin ultérieurement dans le code.

    ![](images/AzureLabs-Lab310-20.png)

## <a name="chapter-3---set-up-the-unity-project"></a>Chapitre 3-configurer le projet Unity

Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez **Unity** et cliquez sur **nouveau**.

    ![](images/AzureLabs-Lab310-21.png)

2.  Vous devez maintenant fournir un nom de projet Unity. Insérez **CustomVisionObjDetection**. Assurez-vous que le type de projet est défini sur **3D**et définissez l’emplacement sur un **emplacement** approprié (n’oubliez pas que les répertoires racine sont plus proches). Ensuite, cliquez sur **créer un projet**.

    ![](images/AzureLabs-Lab310-22.png)

3.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**. Accédez à **modifier* > les*Préférences** , puis à partir de la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio**. Fermez la fenêtre **Préférences** .

    ![](images/AzureLabs-Lab310-23.png)

4.  Accédez ensuite à **fichier > paramètres de build** et basculez la **plateforme** sur *plateforme Windows universelle*, puis cliquez sur le bouton **changer de plateforme** .

    ![](images/AzureLabs-Lab310-24.png)

5.  Dans la même fenêtre **paramètres de build** , vérifiez que les éléments suivants sont définis:

    1.  L' **appareil cible** est défini sur **HoloLens**        
    2.  Le **type de build** est **D3D**
    3.  Le **SDK** est configuré sur le **dernier installé**
    4.  **Version de Visual Studio** définie sur le **dernier installé**
    5.  La **génération et l’exécution** sont définies sur l' **ordinateur local**            
    6.  Les paramètres restants, dans **paramètres de build**, doivent être laissés par défaut pour le moment.

        ![](images/AzureLabs-Lab310-25.png)

6.  Dans la même fenêtre **paramètres de build** , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** .

7. Dans ce volet, quelques paramètres doivent être vérifiés:

    1.  Sous l’onglet **autres paramètres** :

        1.  La **version du runtime de script** doit être **expérimentale** (.net 4,6 équivalent), ce qui déclenche la nécessité de redémarrer l’éditeur.

        2. Le **serveur principal de script** doit être **.net**.

        3. Le **niveau de compatibilité** de l’API doit être **.net 4,6**.

            ![](images/AzureLabs-Lab310-26.png)

    2.  Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:

        1. **InternetClient**

        2.  **Webcam**

        3. **SpatialPerception**

            ![](images/AzureLabs-Lab310-27.png) ![](images/AzureLabs-Lab310-28.png)

    3.  Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, puis assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.

        ![](images/AzureLabs-Lab310-29.png)

8.  De retour dans les **paramètres de build**, les *projets Unity C\#*  ne sont plus grisés: cochez la case en regard de celle-ci.

9.  Fermez la fenêtre **paramètres de build** .

10. Dans l' **éditeur**, cliquez sur **modifier** > les**paramètres** > du projet**graphiques**.

    ![](images/AzureLabs-Lab310-30.png)

11. Dans le **panneau Inspecteur** , les *paramètres graphiques* sont ouverts. Faites défiler jusqu’à ce que vous voyez un tableau appelé **toujours inclure**des nuanceurs. Ajoutez un emplacement en accroissant la variable de **taille** d’une unité (dans cet exemple, il s’agissait de 8, nous l’avons rendu 9). Un nouvel emplacement s’affiche à la dernière position du tableau, comme indiqué ci-dessous:

    ![](images/AzureLabs-Lab310-31.png)

12. Dans l’emplacement, cliquez sur le petit cercle cible en regard de l’emplacement pour ouvrir une liste de nuanceurs. Recherchez les nuanceurs **hérités/transparent/diffus** , puis double-cliquez dessus. 

    ![](images/AzureLabs-Lab310-32.png)

## <a name="chapter-4---importing-the-customvisionobjdetection-unity-package"></a>Chapitre 4-importation du package CustomVisionObjDetection Unity

Pour ce cours, vous disposez d’un package d’actifs Unity appelé **Azure-Mr-310. pour Unity**. 

> ACCÉLÉRATRICE Tous les objets pris en charge par Unity, y compris les scènes entières, peuvent être empaquetés dans un fichier **. pour Unity** , et exportés/importés dans d’autres projets. Il s’agit du moyen le plus sûr et le plus efficace de déplacer des éléments multimédias entre différents **projets Unity**.

Vous trouverez le [package Azure-Mr-310 que vous devez télécharger ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Azure-MR-310.unitypackage).

1.  Avec le tableau de bord Unity devant vous, cliquez sur **ressources** dans le menu en haut de l’écran, puis sur **importer le package > package personnalisé**.

    ![](images/AzureLabs-Lab310-33.png)

2.  Utilisez le sélecteur de fichiers pour sélectionner le package **Azure-Mr-310. pour Unity** , puis cliquez sur **ouvrir**. La liste des composants de cet élément multimédia vous est présentée. Confirmez l’importation en cliquant sur le bouton **Importer** .

    ![](images/AzureLabs-Lab310-34.png)

3.  Une fois l’importation terminée, vous remarquerez que les dossiers du package ont été ajoutés à votre dossier de **ressources** . Ce type de structure de dossiers est courant pour un projet Unity.

    ![](images/AzureLabs-Lab310-35.png)

    1.  Le  dossier Materials contient les éléments utilisés par le **curseur en regard**. 

    2.  Le dossier **plug-ins** contient la dll Newtonsoft utilisée par le code pour désérialiser la réponse Web du service. Les deux (2) différentes versions contenues dans le dossier, et sous-dossier, sont nécessaires pour permettre à la bibliothèque d’être utilisée et construite à la fois par l’éditeur Unity et par la build UWP. 

    3.  Le dossier **Prefabs** contient le Prefabs contenu dans la scène. Celles-ci sont les suivantes:

        1.  **GazeCursor**, le curseur utilisé dans l’application. Fonctionne conjointement avec le Prefab SpatialMapping pour pouvoir être placé dans la scène au-dessus des objets physiques.
        2.  L' **étiquette**, qui est l’objet d’interface utilisateur utilisé pour afficher la balise d’objet dans la scène, si nécessaire.
        3.  **SpatialMapping**, qui est l’objet qui permet à l’application d’utiliser la création d’une carte virtuelle, à l’aide du suivi spatial Microsoft HoloLens.

    4.  Le  dossier scenes qui contient actuellement la scène prédéfinie pour ce cours.

4.  Ouvrez le  dossier scenes, dans le **panneau Projet**, puis double-cliquez sur **ObjDetectionScene**pour charger la scène que vous allez utiliser pour ce cours.

    ![](images/AzureLabs-Lab310-36.png)

    > [!NOTE] 
    >  **Aucun code n’est inclus**, vous allez écrire le code en suivant ce cours.

## <a name="chapter-5---create-the-customvisionanalyser-class"></a>Chapitre 5-créer la classe CustomVisionAnalyser.

À ce stade, vous êtes prêt à écrire du code. Vous allez commencer par la classe **CustomVisionAnalyser** .

> [!NOTE]
> Les appels à la **service vision personnalisée**, effectués dans le code ci-dessous, sont effectués à l’aide de l' **API REST Custom vision**. À l’aide de ce guide, vous allez apprendre à implémenter et à utiliser cette API (utile pour comprendre comment implémenter des éléments similaires). Sachez que Microsoft propose un **Kit de développement logiciel (SDK) Custom vision** qui peut également être utilisé pour effectuer des appels au service. Pour plus d’informations, consultez l' [article du kit de développement logiciel (SDK) Custom vision](https://github.com/Microsoft/Cognitive-CustomVision-Windows/).

Cette classe est chargée des opérations suivantes:

- Chargement de la dernière image capturée sous la forme d’un tableau d’octets.

- Envoi du tableau d’octets à votre instance Azure **service vision personnalisée** à des fins d’analyse.

- Réception de la réponse sous forme de chaîne JSON.

- La désérialisation de la réponse et le passage  de la prédiction résultante à la classe **SceneOrganiser** , qui s’occupera du mode d’affichage de la réponse.

Pour créer cette classe:

1.  Cliquez avec le bouton droit sur le **dossier Asset**, situé dans le **panneau Projet**, puis cliquez sur **créer** > un**dossier**. Appelez le dossier **scripts**.

    ![](images/AzureLabs-Lab310-37.png)

2.  Double-cliquez sur le dossier nouvellement créé pour l’ouvrir.

3.  Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer** > un**script C\#** . Nommez le script **CustomVisionAnalyser.**

4.  Double-cliquez sur le nouveau script **CustomVisionAnalyser** pour l’ouvrir avec **Visual Studio.**

5.  Assurez-vous que les espaces de noms suivants sont référencés en haut du fichier:

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.IO;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

6.  Dans la classe **CustomVisionAnalyser** , ajoutez les variables suivantes:

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
    > Veillez à insérer votre **clé de prédiction de service** dans la variable **PredictionKey** et votre **point de terminaison de prédiction** dans la variable **predictionEndpoint** . Vous les avez copiées [précédemment dans le bloc-notes, au chapitre 2, étape 14](#chapter-2---training-your-custom-vision-project).

7.  Le code pour **éveillé ()** doit maintenant être ajouté pour initialiser la variable d’instance:

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

8.  Ajoutez la Coroutine (avec la méthode statique **GetImageAsByteArray ()** en dessous de celle-ci), qui obtiendra les résultats de l’analyse de l’image, capturés par la classe **ImageCapture** .

    > [!NOTE]
    > Dans la Coroutine **AnalyseImageCapture** , il y a un appel à la classe **SceneOrganiser** que vous êtes encore en cours de création. Par conséquent, **laissez ces lignes commentées pour l’instant**.

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

9. Supprimez les méthodes **Start ()** et **Update ()** , car elles ne seront pas utilisées. 

10.  Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.

> [!IMPORTANT]
> Comme mentionné précédemment, ne vous inquiétez pas du code qui peut sembler avoir une erreur, car vous fournirez bientôt d’autres classes, ce qui les corrigera.

## <a name="chapter-6---create-the-customvisionobjects-class"></a>Chapitre 6-créer la classe CustomVisionObjects

La classe que vous allez créer est maintenant la classe **CustomVisionObjects** .

Ce script contient un certain nombre d’objets utilisés par d’autres classes pour sérialiser et désérialiser les appels passés au Service Vision personnalisée.

Pour créer cette classe:

1.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** . Appelez le script **CustomVisionObjects.**

2.  Double-cliquez sur le nouveau script **CustomVisionObjects** pour l’ouvrir avec **Visual Studio.**

3.  Assurez-vous que les espaces de noms suivants sont référencés en haut du fichier:

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  Supprimez les méthodes **Start ()** et **Update ()** à l’intérieur de la classe **CustomVisionObjects** , cette classe doit maintenant être vide.

    > [!WARNING]
    > Il est important de suivre attentivement l’instruction suivante. Si vous placez les nouvelles déclarations de classe à l’intérieur de la classe **CustomVisionObjects** , vous obtiendrez des erreurs de compilation dans le [chapitre 10](#chapter-10---create-the-imagecapture-class), indiquant que **AnalysisRootObject** et **BoundingBox** sont introuvables.

5.  Ajoutez les classes suivantes *en dehors* de la classe **CustomVisionObjects** . Ces objets sont utilisés par la bibliothèque **Newtonsoft** pour sérialiser et désérialiser les données de réponse:

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

6.  Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.

## <a name="chapter-7---create-the-spatialmapping-class"></a>Chapitre 7-créer la classe SpatialMapping

Cette classe définit le **conflit de mappage spatial** dans la scène afin de pouvoir détecter les collisions entre les objets virtuels et les objets réels.

Pour créer cette classe:

1.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** . Appelez le script **SpatialMapping.**

2.  Double-cliquez sur le nouveau script **SpatialMapping** pour l’ouvrir avec **Visual Studio.**

3.  Assurez-vous que les espaces de noms suivants sont référencés au-dessus de la classe **SpatialMapping** :

    ```csharp
    using UnityEngine;
    using UnityEngine.XR.WSA;
    ```

4.  Ensuite, ajoutez les variables suivantes à l’intérieur de la classe **SpatialMapping** , au-dessus de la méthode **Start ()** :

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

5.  Ajoutez les éléments **éveillé ()** et **Start ()** :

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

6.  Supprimez la méthode **Update ()** .

7.  Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.


## <a name="chapter-8---create-the-gazecursor-class"></a>Chapitre 8-créer la classe GazeCursor

Cette classe est chargée de configurer le curseur à l’emplacement approprié dans l’espace réel, en utilisant le **SpatialMappingCollider**créé dans le chapitre précédent.

Pour créer cette classe:

1.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** . Appeler le script **GazeCursor**

2.  Double-cliquez sur le nouveau script **GazeCursor** pour l’ouvrir avec **Visual Studio.**

3.  Assurez-vous que l’espace de noms suivant est référencé au-dessus de la classe **GazeCursor** :

    ```csharp
    using UnityEngine;
    ```

4.  Ajoutez ensuite la variable suivante à l’intérieur de la classe **GazeCursor** , au-dessus de la méthode **Start ()** . 

    ```csharp
        /// <summary>
        /// The cursor (this object) mesh renderer
        /// </summary>
        private MeshRenderer meshRenderer;
    ```

5.  Mettez à jour la méthode **Start ()** avec le code suivant:

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

6.  Mettez à jour la méthode **Update ()** avec le code suivant:

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
    > Ne vous inquiétez pas de l’erreur pour la classe **SceneOrganiser** introuvable, vous allez la créer dans le chapitre suivant.

7. Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.

## <a name="chapter-9---create-the-sceneorganiser-class"></a>Chapitre 9-créer la classe SceneOrganiser

Cette classe effectuera les opérations suivantes:

-   Configurez la *caméra principale* en y joignant les composants appropriés.

-   Lorsqu’un objet est détecté, il est chargé de calculer sa position dans le monde réel et de placer une **étiquette** de balise près de celui-ci avec le **nom**de balise approprié.    

Pour créer cette classe:

1.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** . Nommez le script **SceneOrganiser**.

2.  Double-cliquez sur le nouveau script **SceneOrganiser** pour l’ouvrir avec **Visual Studio.**

3.  Assurez-vous que les espaces de noms suivants sont référencés au-dessus de la classe **SceneOrganiser** :

    ```csharp
    using System.Collections.Generic;
    using System.Linq;
    using UnityEngine;
    ```

4.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe **SceneOrganiser** , au-dessus de la méthode **Start ()** :

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

5.  Supprimez les méthodes **Start ()** et **Update ()** .

6.  Sous les variables, ajoutez la méthode **éveillé ()** , qui initialisera la classe et configurera la scène.

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

7.  Ajoutez la méthode **PlaceAnalysisLabel ()** , qui *instanciera* l’étiquette dans la scène (qui, à ce stade, est invisible pour l’utilisateur). Il place également le quadruple (également invisible) où l’image est placée et chevauche le monde réel. Cela est important, car les coordonnées de la zone récupérées à partir du service après l’analyse sont retracées dans ce Quad pour déterminer l’emplacement approximatif de l’objet dans le monde réel. 

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

8.  Ajoutez la méthode **FinaliseLabel ()** . Il est responsable des tâches suivantes:

    *   Définition du texte de l' *étiquette* avec la *balise* de la prédiction avec la confiance la plus élevée.
    *   Appel du calcul du *cadre englobant* sur l’objet quadruple, positionné précédemment, et placement de l’étiquette dans la scène.
    *   Ajustement de la profondeur des étiquettes à l’aide d’un Raycast vers le *cadre englobant*, qui doit entrer en conflit avec l’objet dans le monde réel.
    * Réinitialisation du processus de capture pour permettre à l’utilisateur de capturer une autre image.

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

9.  Ajoutez la méthode **CalculateBoundingBoxPosition ()** , qui héberge un certain nombre de calculs nécessaires pour convertir les coordonnées du *cadre englobant* récupérées à partir du service et les recréer proportionnellement sur le quadruple.

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

10. Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.

    > [!IMPORTANT]
    > Avant de continuer, ouvrez la classe **CustomVisionAnalyser** et, dans la méthode **AnalyseLastImageCaptured ()** , *supprimez les marques de commentaire* des lignes suivantes:
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
> Ne vous inquiétez pas du message «Impossible de trouver la classe **ImageCapture** », vous allez le créer dans le chapitre suivant.


## <a name="chapter-10---create-the-imagecapture-class"></a>Chapitre 10-créer la classe ImageCapture

La classe suivante que vous allez créer est la classe **ImageCapture** .

Cette classe est chargée des opérations suivantes:

*   Capture d’une image à l’aide de la caméra HoloLens et stockage dans le dossier de l' *application* .
*   Gestion des gestes *Tap* de l’utilisateur.

Pour créer cette classe:

1.  Accédez au dossier **scripts** que vous avez créé précédemment.

2.  Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer** > un**script C\#** . Nommez le script **ImageCapture**.

3.  Double-cliquez sur le nouveau script **ImageCapture** pour l’ouvrir avec **Visual Studio.**

4.  Remplacez les espaces de noms en haut du fichier par les éléments suivants:

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    using UnityEngine.XR.WSA.WebCam;
    ```

5.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe **ImageCapture** , au-dessus de la méthode **Start ()** :

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

6.  Vous devez maintenant ajouter le code des méthodes **éveillés ()** et **Start ()** :

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

7.  Implémentez un gestionnaire qui sera appelé quand un mouvement TAP se produit:

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
    > Lorsque le curseur est **vert**, cela signifie que l’appareil photo est disponible pour prendre l’image. Lorsque le curseur est **rouge**, cela signifie que l’appareil photo est occupé.

8.  Ajoutez la méthode utilisée par l’application pour démarrer le processus de capture d’image et stocker l’image:

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

9.  Ajoutez les gestionnaires qui seront appelés lorsque la photo a été capturée et le moment où elle sera prête à être analysée. Le résultat est ensuite transmis à **CustomVisionAnalyser** pour l’analyse.

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

10. Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.

## <a name="chapter-11---setting-up-the-scripts-in-the-scene"></a>Chapitre 11-configuration des scripts dans la scène

Maintenant que vous avez écrit l’ensemble du code nécessaire pour ce projet, il est temps de configurer les scripts dans la scène et, sur le prefabs, pour qu’ils se comportent correctement.

1.  Dans l' **éditeur Unity**, dans le **panneau hiérarchie**, sélectionnez l' **appareil photo principal**.
2.  Dans le **panneau Inspecteur**, avec l' **appareil photo principal** sélectionné, cliquez sur **Ajouter un composant**, puis recherchez le script **SceneOrganiser** et double-cliquez dessus pour l’ajouter.

    ![](images/AzureLabs-Lab310-38.png)

3.  Dans le **panneau Projet**, ouvrez le **dossier Prefabs**, faites glisser l' **étiquette** Prefab dans la zone d’entrée cible de référence de l' *étiquette* vide, dans le script **SceneOrganiser** que vous venez d’ajouter à la *caméra principale*, comme illustré dans l’image ci-dessous:

    ![](images/AzureLabs-Lab310-39.png)

4.  Dans le **volet hiérarchie**, sélectionnez l’enfant **GazeCursor** de l' **appareil photo principal**.
5.  Dans le **volet**de l’inspecteur, avec le **GazeCursor** sélectionné, cliquez sur **Ajouter un composant**, puis recherchez le script **GazeCursor** et double-cliquez dessus pour l’ajouter.

    ![](images/AzureLabs-Lab310-40.png)

6.  Là encore, dans le **panneau hiérarchie**, sélectionnez l’enfant **SpatialMapping** de l' **appareil photo principal**.
7.  Dans le **volet**de l’inspecteur, avec le **SpatialMapping** sélectionné, cliquez sur **Ajouter un composant**, puis recherchez le script **SpatialMapping** et double-cliquez dessus pour l’ajouter.

    ![](images/AzureLabs-Lab310-41.png)

Les scripts restants que vous n’avez pas définis seront ajoutés par le code dans le script **SceneOrganiser** , pendant l’exécution.

## <a name="chapter-12---before-building"></a>Chapitre 12-avant génération

Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre Microsoft HoloLens.

Avant cela, assurez-vous que:

-  Tous les paramètres mentionnés dans le [chapitre 3](#chapter-3---set-up-the-unity-project) sont correctement définis.
- Le script **SceneOrganiser** est attaché à l’objet **Camera principal** .
- Le script **GazeCursor** est attaché à l’objet **GazeCursor** .
- Le script **SpatialMapping** est attaché à l’objet **SpatialMapping** .
- Dans le [Chapitre 5](#chapter-5---create-the-customvisionanalyser-class), étape 6:

    - Veillez à insérer votre **clé** de prédiction de service dans la variable **predictionKey** .
    - Vous avez inséré votre **point de terminaison** de prédiction dans la classe **predictionEndpoint** .

## <a name="chapter-13---build-the-uwp-solution-and-sideload-your-application"></a>Chapitre 13: créer la solution UWP et chargement votre application

Vous êtes maintenant prêt à créer votre application en tant que solution UWP que vous pourrez déployer sur Microsoft HoloLens. Pour commencer le processus de génération:

1.  Accédez à **fichier > paramètres de build**.

2.  **Projets Tick Unity C\#** .

3.  Cliquez sur **Ajouter des scènes ouvertes**. Cette opération ajoute la scène actuellement ouverte à la Build.

    ![](images/AzureLabs-Lab310-42.png)

4.  Cliquez sur **Build**. Unity lance une fenêtre de l' *Explorateur de fichiers* , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application. Créez ce dossier maintenant, puis nommez-le **application**. Ensuite, avec le dossier d' **application** sélectionné, cliquez sur **Sélectionner un dossier**.

5.  Unity commence à générer votre projet dans le dossier de l' **application** .

6.  Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).

7.  Pour effectuer un déploiement sur Microsoft HoloLens, vous aurez besoin de l’adresse IP de cet appareil (pour le déploiement à distance) et pour vous assurer qu’il est également défini **en mode développeur** . Pour ce faire :

    1.  Tout en portant votre HoloLens, ouvrez les **paramètres**.

    2.  Accéder au **réseau &**  > **Options avancées** **de Wi-Fi** > Internet

    3.  Notez l’adresse **IPv4** .

    4.  Ensuite, revenez aux **paramètres**, puis pour **mettre à jour & sécurité** > **pour les développeurs**

    5.  Définissez le **mode développeur** *sur*.

8.  Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.

9.  Dans la configuration de la solution, sélectionnez Déboguer.

10. Dans la plateforme de la solution, sélectionnez **x86, ordinateur distant**. Vous serez invité à insérer l' **adresse IP** d’un périphérique distant (le Microsoft HoloLens, dans ce cas, que vous avez noté).

    ![](images/AzureLabs-Lab310-43.png)

11. Accédez au menu **générer** , puis cliquez sur **déployer la solution** pour chargement l’application à votre HoloLens.

12. Votre application doit maintenant apparaître dans la liste des applications installées sur votre Microsoft HoloLens, prête à être lancée.

### <a name="to-use-the-application"></a>Pour utiliser l’application:

* Examinez un objet, que vous avez formé avec votre **service vision personnalisée Azure, la détection d’objets**et utilisez le **geste TAP**.
* Si l’objet est correctement détecté, un *texte d’étiquette* de l’espace universel apparaît avec le nom de la balise.

> [!IMPORTANT]
> Chaque fois que vous capturez une photo et que vous l’envoyez au service, vous pouvez revenir à la page du service et reformer le service avec les images nouvellement capturées. Au début, vous devrez probablement corriger les *zones englobantes* pour qu’elles soient plus précises et reformer le service.

> [!NOTE]
> Le texte de l’étiquette placée peut ne pas apparaître près de l’objet lorsque les capteurs Microsoft HoloLens et/ou SpatialTrackingComponent dans Unity ne peuvent pas placer les conflits appropriés, par rapport aux objets réels. Si c’est le cas, essayez d’utiliser l’application sur une autre surface.

## <a name="your-custom-vision-object-detection-application"></a>Votre Custom Vision, application de détection d’objets

Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API de détection d’objets Azure Custom Vision, qui peut reconnaître un objet d’une image, puis fournir une position approximative pour cet objet dans l’espace 3D.

![](images/AzureLabs-Lab310-00.png)

## <a name="bonus-exercises"></a>Exercices bonus

### <a name="exercise-1"></a>Exercice 1

En ajoutant à l’étiquette de texte, utilisez un cube semi-transparent pour encapsuler l’objet réel dans un *rectangle englobant*3D.

### <a name="exercise-2"></a>Exercice 2

Formez votre Service Vision personnalisée pour qu’il reconnaisse plus d’objets.

### <a name="exercise-3"></a>Exercice 3

Émettre un signal sonore lorsqu’un objet est reconnu.

### <a name="exercise-4"></a>Exercice 4

Utilisez l’API pour reformer votre service avec les mêmes images que celles que votre application analyse, afin de rendre le service plus précis (effectuer la prédiction et la formation simultanément).
