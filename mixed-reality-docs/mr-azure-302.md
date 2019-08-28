---
title: MR et Azure 302-vision par ordinateur
description: Suivez ce cours pour apprendre à reconnaître le contenu visuel dans une image fournie, à l’aide d’Azure Vision par ordinateur dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, vision par ordinateur, hololens, immersif, VR
ms.openlocfilehash: 9cc526afdc36b8056afd61948fea5cf98015bb35
ms.sourcegitcommit: 3b32339c5d5c79eaecd84ed27254a8f4321731f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70047193"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br>

# <a name="mr-and-azure-302-computer-vision"></a>MR et Azure 302: Vision par ordinateur

Dans ce cours, vous allez apprendre à reconnaître du contenu visuel dans une image fournie, à l’aide des fonctionnalités d’Azure Vision par ordinateur dans une application de réalité mixte.

Les résultats de la reconnaissance s’affichent sous forme de balises descriptives. Vous pouvez utiliser ce service sans avoir à former un modèle de Machine Learning. Si votre implémentation nécessite l’apprentissage d’un modèle de Machine Learning, consultez [Mr et Azure 302b](mr-azure-302b.md).

![résultat de l’atelier](images/AzureLabs-Lab2-000.png)

Le Vision par ordinateur Microsoft est un ensemble d’API conçu pour fournir aux développeurs un traitement et une analyse d’image (avec des informations de retour), à l’aide d’algorithmes avancés, le tout à partir du Cloud. Les développeurs téléchargent une URL d’image ou d’image, et les algorithmes de API Vision par ordinateur Microsoft analysent le contenu visuel, en fonction des entrées choisies par l’utilisateur, qui peuvent ensuite retourner des informations, notamment, identifier le type et la qualité d’une image, détecter les visages humains ( retour de leurs coordonnées) et balisage, ou catégorisation d’images. Pour plus d’informations, consultez la [page API vision par ordinateur Azure](https://azure.microsoft.com/services/cognitive-services/computer-vision/).

Une fois ce cours terminé, vous disposerez d’une application HoloLens de réalité mixte, qui sera en mesure d’effectuer les opérations suivantes:

1.  À l’aide du mouvement TAP, l’appareil photo de HoloLens capture une image.
2.  L’image sera envoyée au service Azure API Vision par ordinateur. 
3.  Les objets reconnus seront listés dans un groupe d’interface utilisateur simple positionné dans la scène Unity.

Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception. Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity. C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 302: Vision par ordinateur</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Bien que ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques pour Windows Mixed Reality (VR). Étant donné que les casques immersifs ne disposent pas de caméras accessibles, vous aurez besoin d’une caméra externe connectée à votre PC. À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge les écouteurs immersifs (VR).

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:

- Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](install-the-tools.md#installation-checklist)
- [Le dernier Kit de développement logiciel Windows 10](install-the-tools.md#installation-checklist)
- [Unity 2017,4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé
- Appareil photo connecté à votre PC (pour le développement d’un casque immersif)
- Accès à Internet pour l’installation d’Azure et la récupération de API Vision par ordinateur

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).
2.  Configurez et testez votre HoloLens. Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur). 

Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens-2).

Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1--the-azure-portal"></a>Chapitre 1 – portail Azure

Pour utiliser le service de *API vision par ordinateur* dans Azure, vous devez configurer une instance du service qui sera mise à la disposition de votre application.

1.  Tout d’abord, connectez-vous au [portail Azure](https://portal.azure.com). 

    > [!NOTE]
    > Si vous n’avez pas encore de compte Azure, vous devez en créer un. Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche, recherchez *API vision par ordinateur*, puis cliquez sur **entrée**.

    ![Créer une ressource dans Azure](images/AzureLabs-Lab2-00.png)

    > [!NOTE]
    > Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.
 
3.  La nouvelle page fournit une description du service *API vision par ordinateur* . En bas à gauche de cette page, cliquez sur le bouton **créer** pour créer une association avec ce service.

    ![À propos du service d’API vision par ordinateur](images/AzureLabs-Lab2-01.png)
 
4.  Une fois que vous avez cliqué sur **créer**:

    1. Insérez le **nom** de votre choix pour cette instance de service.
    2. Sélectionnez un **abonnement**.
    3. Sélectionnez le **niveau tarifaire** approprié, s’il s’agit de la première fois que vous créez un service *API vision par ordinateur* , vous devez disposer d’un niveau gratuit (nommé F0).
    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun). 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. Déterminez l’emplacement de votre groupe de ressources (si vous créez un groupe de ressources). L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait. Certaines ressources Azure sont uniquement disponibles dans certaines régions.

    6. Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.
    7. Cliquez sur créer.

        ![Informations sur la création du service](images/AzureLabs-Lab2-02.png)

5.  Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.
6.  Une notification s’affichera dans le portail une fois l’instance de service créée.

    ![Consultez la nouvelle notification pour votre nouveau service](images/AzureLabs-Lab2-03.png) 
 
7.  Cliquez sur la notification pour explorer votre nouvelle instance de service. 

    ![Sélectionnez le bouton atteindre la ressource.](images/AzureLabs-Lab2-04.png)
 
8. Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service. Vous êtes dirigé vers votre nouvelle instance de service API Vision par ordinateur. 

    ![Votre nouveau service API Vision par ordinateur](images/AzureLabs-Lab2-05.png)
 
9.  Dans ce didacticiel, votre application doit effectuer des appels à votre service, à l’aide de la clé d’abonnement de votre service.
10. Dans la page *démarrage rapide* de votre service *API vision par ordinateur* , accédez à la première étape, *saisissez vos clés*, puis cliquez sur **clés** (vous pouvez également y parvenir en cliquant sur les touches de lien bleu, situées dans le menu de navigation services, indiqué par l’icône de clé). Cela permet de révéler vos *clés*de service.
11. Prenez une copie de l’une des clés affichées, car vous en aurez besoin plus tard dans votre projet. 

12. Revenez à la page de *démarrage rapide* et, à partir de là, récupérez votre point de terminaison. N’oubliez pas que la vôtre peut être différente, en fonction de votre région (si c’est le cas, vous devrez apporter une modification à votre code ultérieurement). Prendre une copie de ce point de terminaison pour une utilisation ultérieure:

    ![Votre nouveau service API Vision par ordinateur](images/AzureLabs-Lab2-05-5.png)

    > [!TIP]
    > Vous pouvez vérifier les différents points de terminaison [ici](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa). 

## <a name="chapter-2--set-up-the-unity-project"></a>Chapitre 2: configurer le projet Unity

Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **nouveau**. 

    ![Démarrez le nouveau projet Unity.](images/AzureLabs-Lab2-06.png)

2.  Vous devez maintenant fournir un nom de projet Unity. Insérez **MR_ComputerVision**. Assurez-vous que le type de projet est défini sur **3D**. Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés). Ensuite, cliquez sur **créer un projet**.

    ![Fournissez des détails pour le nouveau projet Unity.](images/AzureLabs-Lab2-07.png)

3.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**. Accédez à **modifier > préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio 2017**. Fermez la fenêtre **Préférences** .

    ![Mettre à jour la préférence éditeur de script.](images/AzureLabs-Lab2-08.png)

4.  Accédez ensuite à **fichier > paramètres de build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le bouton **changer de plateforme** pour appliquer votre sélection.

    ![Fenêtre Paramètres de build, basculez plateforme vers UWP.](images/AzureLabs-Lab2-10.png)

5.  Tout en conservant les **paramètres de génération de > de fichiers** et assurez-vous que:

    1. L' **appareil cible** est défini sur **HoloLens**

        > Pour les casques immersifs, définissez **appareil cible** sur *n’importe quel appareil*.

    2. Le **type de build** est **D3D**
    3. Le **SDK** est configuré sur le **dernier installé**
    4. **Version de Visual Studio** définie sur le **dernier installé**
    5. La **génération et l’exécution** sont définies sur l' **ordinateur local**
    6. Enregistrez la scène et ajoutez-la à la Build.

        1. Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**. Une fenêtre d’enregistrement s’affiche.
        
            ![Cliquez sur le bouton Ajouter des scènes ouvertes](images/AzureLabs-Lab2-11.png)

        2. Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le Scenes.

            ![Créer un dossier de scripts](images/AzureLabs-Lab2-12.png)

        3. Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier*:, tapez **MR_ComputerVisionScene**, puis cliquez sur **Enregistrer**.

            ![Donnez un nom à la nouvelle scène.](images/AzureLabs-Lab2-13.png)

            > Sachez que vous devez enregistrer vos scènes Unity dans le dossier *ressources* , car elles doivent être associées au projet Unity. La création du dossier scenes (et d’autres dossiers similaires) est un moyen classique de structurer un projet Unity.

    7. Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.

6. Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* . 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab2-14.png)

7. Dans ce volet, quelques paramètres doivent être vérifiés:

    1. Sous l’onglet **autres paramètres** :

        1. La **version du runtime de script** doit être **stable** (équivalent .net 3,5).
        2. Le **backend de script** doit être **.net**
        3. Le **niveau de compatibilité** de l’API doit être **.net 4,6**

            ![Mettez à jour d’autres paramètres.](images/AzureLabs-Lab2-15.png)
      
    2. Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:

        1. **InternetClient**
        2. **Webcam**

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab2-16.png)

    3. Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.

        ![Mettez à jour les paramètres X R.](images/AzureLabs-Lab2-17.png)

8.  De retour dans les *paramètres de build* , les projets _Unity C#_  ne sont plus grisés. Cochez la case en regard de cette option. 
9.  Fermez la fenêtre Paramètres de Build.
10. Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).

## <a name="chapter-3--main-camera-setup"></a>Chapitre 3 – Configuration de l’appareil photo principal

> [!IMPORTANT]
> Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302%20-%20Computer%20vision/Azure-MR-302.unitypackage), à l’importer dans votre projet en tant que [package personnalisé](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au [Chapitre 5](#chapter-5--create-the-resultslabel-class).

1.  Dans le *panneau hiérarchie*, sélectionnez l' **appareil photo principal**. 
2.  Une fois sélectionné, vous pouvez voir tous les composants de la **caméra principale** dans le *panneau Inspecteur*.

    1. L' **objet Camera** doit être nommé **Camera main** (Notez l’orthographe!)
    2. La balise principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe!)
    3. Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0
    4. Affectez à **effacer les indicateurs** la **couleur unie** (ignorer ce point pour le casque immersif).
    5. Définissez la couleur d' **arrière-plan** du composant Camera sur **Black, alpha 0 (Code hex: #00000000)** (ignorez-le pour le casque immersif).

        ![Mettez à jour les composants de l’appareil photo.](images/AzureLabs-Lab2-18.png)
 
3.  Ensuite, vous devez créer un objet «Cursor» simple attaché à l' **appareil photo principal**, ce qui vous aidera à positionner la sortie de l’analyse d’image lorsque l’application est en cours d’exécution. Ce curseur détermine le point central du focus de l’appareil photo.

Pour créer le curseur:

1.  Dans le *panneau hiérarchie*, cliquez avec le bouton droit sur l' **appareil photo principal**. Sous **objet 3D**, cliquez sur **sphère**.

    ![Sélectionnez l’objet curseur.](images/AzureLabs-Lab2-19.png)
 
2.  Renommez la **sphère** en **curseur** (double-cliquez sur l’objet curseur ou appuyez sur le bouton clavier F2 avec l’objet sélectionné) et vérifiez qu’il est situé en tant qu’enfant de l' **appareil photo principal**.

3.  Dans le *volet*de la hiérarchie, cliquez sur le **curseur**à gauche. Après avoir sélectionné le curseur, ajustez les variables suivantes dans le *panneau Inspecteur*:

    1. Définir la *position* de la transformation sur **0, 0,5**
    2. Définir l' *échelle* sur **0,02, 0,02, 0,02**

        ![Mettez à jour la position et l’échelle de la transformation.](images/AzureLabs-Lab2-20.png)
  
## <a name="chapter-4--setup-the-label-system"></a>Chapitre 4-configurer le système d’étiquette

Une fois que vous avez capturé une image à l’aide de la caméra HoloLens, cette image est envoyée à votre instance *Azure API vision par ordinateur* service à des fins d’analyse. 

Les résultats de cette analyse seront une liste d’objets reconnus appelés **balises**. 

Vous allez utiliser des étiquettes (comme du texte 3D dans l’espace universel) pour afficher ces balises à l’emplacement où la photo a été prise.

Les étapes suivantes montrent comment configurer l’objet **label** .

1.  Cliquez avec le bouton droit n’importe où dans le volet de la hiérarchie (l’emplacement n’a pas d’importance à ce stade), sous **objet 3D**, ajoutez un **texte 3D**. Nommez-le **LabelText**.

    ![Créez un objet de texte 3D.](images/AzureLabs-Lab2-21.png)
 
2.  Dans le *volet*de la hiérarchie, cliquez sur le **LabelText**. Une fois le **LabelText** sélectionné, ajustez les variables suivantes dans le *panneau Inspecteur*:

    1. Définir la **position** sur **0, 0, 0**
    2. Définir l' **échelle** sur **0,01, 0,01, 0,01**
    3. Dans la **maille du texte**du composant:
    4. Remplacer tout le texte dans le **texte**par «...»        
    5. Définir le **point d’ancrage** au **milieu** central
    6. Définir l' **alignement** sur **Center**
    7. Définir la **taille** des tabulations sur **4**
    8. Définir la **taille** de la police sur **50**
    9. Définir la **couleur** sur **#FFFFFFFF**

    ![Composant de texte](images/AzureLabs-Lab2-21-5.png)

3.  Faites glisser le **LabelText** à partir du *panneau*de la hiérarchie, dans le *dossier Asset*, dans le *panneau Projet*. Cela rend le **LabelText** Prefab, afin qu’il puisse être instancié dans le code.

    ![Créez un Prefab de l’objet LabelText.](images/AzureLabs-Lab2-22.png)
 
4.  Vous devez supprimer le **LabelText** du *panneau de hiérarchie*, afin qu’il ne s’affiche pas dans la scène d’ouverture. Comme il s’agit maintenant d’un Prefab, que vous allez appeler pour des instances individuelles à partir de votre dossier de ressources, il n’est pas nécessaire de le conserver dans la scène. 
5.  La dernière structure de l’objet dans le volet de la *hiérarchie* doit être similaire à celle illustrée dans l’image ci-dessous:

    ![Structure finale du panneau de la hiérarchie.](images/AzureLabs-Lab2-23.png)

## <a name="chapter-5--create-the-resultslabel-class"></a>Chapitre 5: créer la classe ResultsLabel

Le premier script que vous devez créer est la classe *ResultsLabel* , qui est chargée des opérations suivantes: 

- Création des étiquettes dans l’espace universel approprié, par rapport à la position de l’appareil photo.
- Affichage des balises à partir de l’image analyse.

Pour créer cette classe: 

1.  Cliquez avec le bouton droit dans le *panneau Projet*, puis **créez > dossier**. Nommez le dossier **scripts**. 

    ![Créer un dossier de scripts.](images/AzureLabs-Lab2-24.png)

2.  Avec le dossier **scripts** créer, double-cliquez dessus pour l’ouvrir. Ensuite, dans ce dossier, cliquez avec le bouton droit, puis sélectionnez **créer >**  **C# script**. Nommez le script *ResultsLabel*. 

3.  Double-cliquez sur le nouveau script *ResultsLabel* pour l’ouvrir avec **Visual Studio**.

4.  À l’intérieur de la classe, insérez le code suivant dans la classe *ResultsLabel* :

    ```csharp
        using System.Collections.Generic;
        using UnityEngine;

        public class ResultsLabel : MonoBehaviour
        {   
            public static ResultsLabel instance;

            public GameObject cursor;

            public Transform labelPrefab;

            [HideInInspector]
            public Transform lastLabelPlaced;

            [HideInInspector]
            public TextMesh lastLabelPlacedText;

            private void Awake()
            {
                // allows this instance to behave like a singleton
                instance = this;
            }

            /// <summary>
            /// Instantiate a Label in the appropriate location relative to the Main Camera.
            /// </summary>
            public void CreateLabel()
            {
                lastLabelPlaced = Instantiate(labelPrefab, cursor.transform.position, transform.rotation);

                lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();

                // Change the text of the label to show that has been placed
                // The final text will be set at a later stage
                lastLabelPlacedText.text = "Analysing...";
            }

            /// <summary>
            /// Set the Tags as Text of the last Label created. 
            /// </summary>
            public void SetTagsToLastLabel(Dictionary<string, float> tagsDictionary)
            {
                lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();

                // At this point we go through all the tags received and set them as text of the label
                lastLabelPlacedText.text = "I see: \n";

                foreach (KeyValuePair<string, float> tag in tagsDictionary)
                {
                    lastLabelPlacedText.text += tag.Key + ", Confidence: " + tag.Value.ToString("0.00 \n");
                }    
            }
        }
    ```

6.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenirà Unity.
7.  De retour dans l' *éditeur Unity*, cliquez et faites glisser la classe *ResultsLabel* du dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*.
8.  Cliquez sur l' **appareil photo principal** et observez le panneau de l' *inspecteur*.

Vous remarquerez qu’à partir du script que vous venez de faire glisser dans l’appareil photo, il y a deux champs: **Curseur** et **étiquette Prefab**.

9.  Faites glisser l’objet appelé **Cursor** du *volet* de la hiérarchie vers l’emplacement nommé **Cursor**, comme indiqué dans l’image ci-dessous.
10. Faites glisser l’objet appelé **LabelText** du *dossier composants* du *panneau projet* vers l’emplacement nommé **étiquette Prefab**, comme indiqué dans l’image ci-dessous. 

    ![Définissez les cibles de référence dans Unity.](images/AzureLabs-Lab2-25.png)

## <a name="chapter-6--create-the-imagecapture-class"></a>Chapitre 6: créer la classe ImageCapture

La classe suivante que vous allez créer est la classe *ImageCapture* . Cette classe est chargée des opérations suivantes:

-   Capture d’une image à l’aide de la caméra HoloLens et stockage dans le dossier de l’application.
-   Capture des gestes TAP de l’utilisateur.

Pour créer cette classe: 

1.  Accédez au dossier **scripts** que vous avez créé précédemment. 
2.  Cliquez avec le bouton droit dans le dossier, **créez > C# script**. Appelez le script *ImageCapture*. 
3.  Double-cliquez sur le nouveau script *ImageCapture* pour l’ouvrir avec **Visual Studio**.
4.  Ajoutez les espaces de noms suivants au début du fichier:

    ```csharp
        using System.IO;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;
        using UnityEngine.XR.WSA.WebCam;
    ```

5.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe *ImageCapture* , au-dessus de la méthode *Start ()* :

    ```csharp
        public static ImageCapture instance; 
        public int tapsCount;
        private PhotoCapture photoCaptureObject = null;
        private GestureRecognizer recognizer;
        private bool currentlyCapturing = false;
    ```
 
La variable **tapsCount** stocke le nombre de gestes TAP capturés par l’utilisateur. Ce nombre est utilisé pour nommer les images capturées.

6.  Vous devez maintenant ajouter le code des méthodes *éveillés ()* et *Start ()* . Ils sont appelés lorsque la classe est initialisée:

    ```csharp
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            instance = this;
        }

        void Start()
        {
            // subscribing to the Hololens API gesture recognizer to track user gestures
            recognizer = new GestureRecognizer();
            recognizer.SetRecognizableGestures(GestureSettings.Tap);
            recognizer.Tapped += TapHandler;
            recognizer.StartCapturingGestures();
        }
    ```

7.  Implémentez un gestionnaire qui sera appelé quand un mouvement TAP se produit. 

    ```csharp
        /// <summary>
        /// Respond to Tap Input.
        /// </summary>
        private void TapHandler(TappedEventArgs obj)
        {
            // Only allow capturing, if not currently processing a request.
            if(currentlyCapturing == false)
            {
                currentlyCapturing = true;
            
                // increment taps count, used to name images when saving
                tapsCount++;

                // Create a label in world space using the ResultsLabel class
                ResultsLabel.instance.CreateLabel();

                // Begins the image capture and analysis procedure
                ExecuteImageCaptureAndAnalysis();
            }
        }
    ```
 
La méthode *TapHandler ()* incrémente le nombre de clics capturés à l’utilisateur et utilise la position actuelle du curseur pour déterminer où positionner une nouvelle étiquette.

Cette méthode appelle ensuite la méthode *ExecuteImageCaptureAndAnalysis ()* pour commencer les fonctionnalités principales de cette application.

8.  Une fois qu’une image a été capturée et stockée, les gestionnaires suivants sont appelés. Si le processus réussit, le résultat est passé au *VisionManager* (que vous êtes en train de créer) à des fins d’analyse.

    ```csharp
        /// <summary>
        /// Register the full execution of the Photo Capture. If successful, it will begin 
        /// the Image Analysis process.
        /// </summary>
        void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
        {
            // Call StopPhotoMode once the image has successfully captured
            photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
        }

        void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
        {
            // Dispose from the object in memory and request the image analysis 
            // to the VisionManager class
            photoCaptureObject.Dispose();
            photoCaptureObject = null;
            StartCoroutine(VisionManager.instance.AnalyseLastImageCaptured()); 
        }
    ```
 
9.  Ajoutez ensuite la méthode utilisée par l’application pour démarrer le processus de capture d’image et stocker l’image.

    ```csharp    
        /// <summary>    
        /// Begin process of Image Capturing and send To Azure     
        /// Computer Vision service.   
        /// </summary>    
        private void ExecuteImageCaptureAndAnalysis()  
        {    
            // Set the camera resolution to be the highest possible    
            Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();    

            Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);
    
            // Begin capture process, set the image format    
            PhotoCapture.CreateAsync(false, delegate (PhotoCapture captureObject)    
            {    
                photoCaptureObject = captureObject;    
                CameraParameters camParameters = new CameraParameters();    
                camParameters.hologramOpacity = 0.0f;    
                camParameters.cameraResolutionWidth = targetTexture.width;    
                camParameters.cameraResolutionHeight = targetTexture.height;    
                camParameters.pixelFormat = CapturePixelFormat.BGRA32;
    
                // Capture the image from the camera and save it in the App internal folder    
                captureObject.StartPhotoModeAsync(camParameters, delegate (PhotoCapture.PhotoCaptureResult result)
                {    
                    string filename = string.Format(@"CapturedImage{0}.jpg", tapsCount);
    
                    string filePath = Path.Combine(Application.persistentDataPath, filename);

                    VisionManager.instance.imagePath = filePath;
    
                    photoCaptureObject.TakePhotoAsync(filePath, PhotoCaptureFileOutputFormat.JPG, OnCapturedPhotoToDisk);

                    currentlyCapturing = false;
                });   
            });    
        }
    ```
 
> [!WARNING] 
> À ce stade, vous remarquerez qu’une erreur s’affiche dans le panneau de la console de l' *éditeur Unity*. Cela est dû au fait que le code fait référence à la classe *VisionManager* que vous allez créer dans le chapitre suivant.

## <a name="chapter-7--call-to-azure-and-image-analysis"></a>Chapitre 7 – appel à Azure et à l’analyse des images

Le dernier script que vous devez créer est la classe *VisionManager* . 

Cette classe est chargée des opérations suivantes:

-   Chargement de la dernière image capturée sous la forme d’un tableau d’octets.
-   Envoi du tableau d’octets à votre instance *Azure API vision par ordinateur* service à des fins d’analyse.
-   Réception de la réponse sous forme de chaîne JSON.
-   Désérialisation de la réponse et transmission des balises résultantes à la classe *ResultsLabel* .
 
Pour créer cette classe:

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir. 
2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**. Nommez le script *VisionManager*. 
3.  Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.
4.  Mettez à jour les espaces de noms pour qu’ils soient identiques à ce qui suit, en haut de la classe *VisionManager* :

    ```csharp
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using UnityEngine;
        using UnityEngine.Networking;
    ```
 
5.  En haut de votre script, à l' *intérieur* de la classe *VisionManager* (au-dessus de la méthode *Start ()* ), vous devez maintenant créer deux *classes* qui représenteront la réponse JSON désérialisée à partir d’Azure:

    ```csharp
        [System.Serializable]
        public class TagData
        {
            public string name;
            public float confidence;
        }

        [System.Serializable]
        public class AnalysedObject
        {
            public TagData[] tags;
            public string requestId;
            public object metadata;
        }
    ```

    > [!NOTE] 
    > Les classes *TagData* et *AnalysedObject* doivent avoir l’attribut *[System. Serializable]* ajouté avant la déclaration pour pouvoir être désérialisées avec les bibliothèques Unity.

6.  Dans la classe VisionManager, vous devez ajouter les variables suivantes:

    ```csharp
        public static VisionManager instance;

        // you must insert your service key here!    
        private string authorizationKey = "- Insert your key here -";    
        private const string ocpApimSubscriptionKeyHeader = "Ocp-Apim-Subscription-Key";
        private string visionAnalysisEndpoint = "https://westus.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags";   // This is where you need to update your endpoint, if you set your location to something other than west-us.
  
        internal byte[] imageBytes;

        internal string imagePath;
    ```

    > [!WARNING] 
    > Veillez à insérer votre **clé d’authentification** dans la variable **authorizationKey** . Vous aurez noté votre **clé d’authentification** au début de ce cours, [Chapitre 1](#chapter-1--the-azure-portal).

    > [!WARNING] 
    > La variable **visionAnalysisEndpoint** peut être différente de celle spécifiée dans cet exemple. L' **ouest des États-Unis** fait strictement référence aux instances de service créées pour la région États-Unis de l’Ouest. Mettez-le à jour avec votre [URL de point de terminaison](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa); Voici quelques exemples de ce qui peut ressembler à ceci:
    > - Europe de l’Ouest:`https://westeurope.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`
    > - Asie du sud-est:`https://southeastasia.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`
    > - Est de l’Australie:`https://australiaeast.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`

7.  Le code pour éveillé doit maintenant être ajouté. 

    ```csharp
        private void Awake()
        {
            // allows this instance to behave like a singleton
            instance = this;
        }
    ```

8.  Ensuite, ajoutez la Coroutine (avec la méthode de flux statique ci-dessous), qui obtiendra les résultats de l’analyse de l’image capturée par la classe *ImageCapture* . 

    ```csharp
        /// <summary>
        /// Call the Computer Vision Service to submit the image.
        /// </summary>
        public IEnumerator AnalyseLastImageCaptured()
        {
            WWWForm webForm = new WWWForm();
            using (UnityWebRequest unityWebRequest = UnityWebRequest.Post(visionAnalysisEndpoint, webForm))
            {
                // gets a byte array out of the saved image
                imageBytes = GetImageAsByteArray(imagePath);
                unityWebRequest.SetRequestHeader("Content-Type", "application/octet-stream");
                unityWebRequest.SetRequestHeader(ocpApimSubscriptionKeyHeader, authorizationKey);

                // the download handler will help receiving the analysis from Azure
                unityWebRequest.downloadHandler = new DownloadHandlerBuffer();

                // the upload handler will help uploading the byte array with the request
                unityWebRequest.uploadHandler = new UploadHandlerRaw(imageBytes);
                unityWebRequest.uploadHandler.contentType = "application/octet-stream";

                yield return unityWebRequest.SendWebRequest();

                long responseCode = unityWebRequest.responseCode;     

                try
                {
                    string jsonResponse = null;
                    jsonResponse = unityWebRequest.downloadHandler.text;

                    // The response will be in Json format
                    // therefore it needs to be deserialized into the classes AnalysedObject and TagData
                    AnalysedObject analysedObject = new AnalysedObject();
                    analysedObject = JsonUtility.FromJson<AnalysedObject>(jsonResponse);

                    if (analysedObject.tags == null)
                    {
                        Debug.Log("analysedObject.tagData is null");
                    }
                    else
                    {
                        Dictionary<string, float> tagsDictionary = new Dictionary<string, float>();

                        foreach (TagData td in analysedObject.tags)
                        {
                            TagData tag = td as TagData;
                            tagsDictionary.Add(tag.name, tag.confidence);                            
                        }

                        ResultsLabel.instance.SetTagsToLastLabel(tagsDictionary);
                    }
                }
                catch (Exception exception)
                {
                    Debug.Log("Json exception.Message: " + exception.Message);
                }

                yield return null;
            }
        }
    ```

    ```csharp
        /// <summary>
        /// Returns the contents of the specified file as a byte array.
        /// </summary>
        private static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }  
    ```

9.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenirà Unity.
10. De retour dans l’éditeur Unity, cliquez et faites glisser les classes *VisionManager* et *ImageCapture* du dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*. 

## <a name="chapter-8--before-building"></a>Chapitre 8 – avant la génération

Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre HoloLens.
Avant cela, assurez-vous que:

-   Tous les paramètres mentionnés dans le [Chapitre 2](#chapter-2--set-up-the-unity-project) sont correctement définis. 
-   Tous les scripts sont attachés à l’objet **Camera principal** . 
-   Tous les champs du volet principal de l’inspecteur de l' *appareil photo* sont correctement affectés.
-   Veillez à insérer votre **clé d’authentification** dans la variable **authorizationKey** .
-   Vérifiez que vous avez également vérifié votre point de terminaison dans votre script *VisionManager* et qu’il est aligné sur *votre* région (ce document utilise par défaut *West-US* ).

## <a name="chapter-9--build-the-uwp-solution-and-sideload-the-application"></a>Chapitre 9: créer la solution UWP et chargement l’application
Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.

1.  Accédez au fichier des *paramètres* - de build **> paramètres de Build...**
2.  Dans la fenêtre *paramètres de build* , cliquez sur **générer**.

    ![Génération de l’application à partir d’Unity](images/AzureLabs-Lab2-26.png)

3.  Si ce n’est pas déjà fait, les **projets C# Unity**.
4.  Cliquez sur **Build**. Unity lance une fenêtre de l' *Explorateur de fichiers* , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application. Créez ce dossier maintenant, puis nommez-le *application*. Ensuite, avec le dossier d' *application* sélectionné, appuyez sur **Sélectionner un dossier**. 
5.  Unity commence à générer votre projet dans le dossier de l' *application* . 
6.  Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' *Explorateur de fichiers* s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).

## <a name="chapter-10--deploy-to-hololens"></a>Chapitre 10 – déployer dans HoloLens

Pour effectuer un déploiement sur HoloLens:

1.  Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur**. Pour ce faire :

    1. Tout en portant votre HoloLens, ouvrez les **paramètres**.
    2. Accéder au **réseau & Internet > Wi-Fi > options avancées**
    3. Notez l’adresse **IPv4** .
    4. Ensuite, revenez aux **paramètres**, puis à **mettre à jour & > de sécurité pour les développeurs** 
    5. Définissez le mode développeur sur.

2.  Accédez à votre nouvelle build Unity (le dossier de l' *application* ) et ouvrez le fichier solution avec *Visual Studio*.
3.  Dans la configuration de lasolution, sélectionnez Déboguer.
4.  Dans la plateforme de la solution, sélectionnez **x86**, **ordinateur distant**. 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab2-27.png)
 
5.  Accédez au **menu Générer** , puis cliquez sur **déployer la solution**pour chargement l’application à votre HoloLens.
6.  Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.

> [!NOTE]
> Pour effectuer un déploiement sur un casque immersif, définissez la plateforme de la **solution** sur *ordinateur local*et définissez la **configuration** sur déboguer, avec *x86* comme **plateforme**. Déployez ensuite sur l’ordinateur local, à l’aide du **menu Générer**, en sélectionnant *déployer la solution*. 

## <a name="your-finished-computer-vision-api-application"></a>Votre application API Vision par ordinateur terminée

Félicitations, vous avez créé une application de réalité mixte qui tire parti de la API Vision par ordinateur Azure pour reconnaître des objets réels, et afficher la confiance de ce qui a été observé.

![résultat de l’atelier](images/AzureLabs-Lab2-000.png)

## <a name="bonus-exercises"></a>Exercices bonus

### <a name="exercise-1"></a>Exercice 1

Tout comme vous avez utilisé le paramètre *Tags* (tel qu’il est prouvé dans le *point de terminaison* utilisé dans *VisionManager*), étendez l’application pour détecter d’autres informations. Examinez les autres paramètres auxquels vous avez accès [ici](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).

### <a name="exercise-2"></a>Exercice 2

Affichez les données Azure retournées, d’une manière plus conversationnele et lisible, en masquant éventuellement les nombres. Comme si un bot était en contact avec l’utilisateur.
