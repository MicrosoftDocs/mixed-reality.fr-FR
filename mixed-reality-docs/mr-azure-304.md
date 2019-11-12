---
title: RM et Azure 304-reconnaissance faciale
description: Suivez ce cours pour découvrir comment implémenter la reconnaissance faciale Azure au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, reconnaissance faciale, hololens, immersif, VR
ms.openlocfilehash: 23676684c2ec325f9d6f1924e7a0bad14d41f13e
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926792"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br> 

# <a name="mr-and-azure-304-face-recognition"></a>MR et Azure 304 : reconnaissance faciale

![résultat de la fin de ce cours](images/AzureLabs-Lab4-00.png)

Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de reconnaissance faciale à une application de réalité mixte, à l’aide d’Azure Cognitive Services, avec la API Visage Microsoft.

*Azure API visage* est un service Microsoft qui fournit aux développeurs les algorithmes les plus avancés, le tout dans le Cloud. La *API visage* a deux fonctions principales : la détection des visages avec les attributs et la reconnaissance faciale. Cela permet aux développeurs de définir simplement un ensemble de groupes pour les visages, puis d’envoyer des images de requête au service ultérieurement, pour déterminer à qui appartient une face. Pour plus d’informations, consultez la [page reconnaissance des visages Azure](https://azure.microsoft.com/services/cognitive-services/face/).

Une fois ce cours terminé, vous disposerez d’une application HoloLens de réalité mixte, qui sera en mesure d’effectuer les opérations suivantes :

1. Utilisez un **mouvement TAP** pour initier la capture d’une image à l’aide de l’appareil photo HoloLens intégré. 
2. Envoyez l’image capturée au service *Azure API visage* .
3. Recevoir les résultats de l’algorithme *API visage* .
4. Utilisez une interface utilisateur simple pour afficher le nom des personnes mises en correspondance.

Cela vous apprend à obtenir les résultats du service API Visage dans votre application de réalité mixte basée sur Unity.

Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception. Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity. C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Périphériques pris en charge

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 304 : reconnaissance faciale</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Bien que ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques pour Windows Mixed Reality (VR). Étant donné que les casques immersifs ne disposent pas de caméras accessibles, vous aurez besoin d’une caméra externe connectée à votre PC. À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge les écouteurs immersifs (VR).

## <a name="prerequisites"></a>Conditions préalables

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours :

- Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](install-the-tools.md)
- [Le dernier Kit de développement logiciel Windows 10](install-the-tools.md)
- [Unity 2017,4](install-the-tools.md)
- [Visual Studio 2017](install-the-tools.md)
- Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé
- Appareil photo connecté à votre PC (pour le développement d’un casque immersif)
- Accès à Internet pour l’installation d’Azure et la récupération de API Visage

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).
2.  Configurez et testez votre HoloLens. Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur). 

Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens-2).

Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1---the-azure-portal"></a>Chapitre 1-portail Azure

Pour utiliser le service de *API visage* dans Azure, vous devez configurer une instance du service qui sera mise à la disposition de votre application.

1.  Tout d’abord, connectez-vous au [portail Azure](https://portal.azure.com). 

    > [!NOTE]
    > Si vous n’avez pas encore de compte Azure, vous devez en créer un. Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche et recherchez *API visage*, appuyez sur **entrée**.

    ![Rechercher l’API visage](images/AzureLabs-Lab4-01.png)

    > [!NOTE]
    > Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.

3.  La nouvelle page fournit une description du service *API visage* . En bas à gauche de cette invite, sélectionnez le bouton **créer** pour créer une association avec ce service.

    ![informations sur l’API visage](images/AzureLabs-Lab4-02.png)

4.  Une fois que vous avez cliqué sur **créer**:

    1. Insérez le nom de votre choix pour cette instance de service.

    2. Sélectionnez un abonnement.

    3. Sélectionnez le niveau tarifaire approprié, s’il s’agit de la première fois que vous créez un *Service API visage*, vous devez disposer d’un niveau gratuit (nommé F0).

    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun). 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. L’application UWP, **Person Maker**, que vous utilisez ultérieurement, requiert l’utilisation de « West US » pour l’emplacement.

    6. Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.

    7. Sélectionnez **créer *.**

        ![créer un service d’API visage](images/AzureLabs-Lab4-03.png)

5.  Une fois que vous avez cliqué sur **créer *,** vous devez attendre que le service soit créé. cette opération peut prendre une minute.

6.  Une notification s’affichera dans le portail une fois l’instance de service créée.

    ![notification de création de service](images/AzureLabs-Lab4-04.png)

7.  Cliquez sur les notifications pour explorer votre nouvelle instance de service.

    ![accéder à la notification de ressource](images/AzureLabs-Lab4-05.png)

8.  Quand vous êtes prêt, cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.

    ![clés d’API de visage d’accès](images/AzureLabs-Lab4-06.png)

9.  Dans ce didacticiel, votre application doit effectuer des appels à votre service, ce qui est effectué via l’utilisation de la « clé » de l’abonnement de votre service. Dans la page *démarrage rapide* de votre service *API visage* , le premier point est le numéro 1, pour *récupérer vos clés.*

10. Sur la page *service* , sélectionnez le lien hypertexte **touches** bleues (si sur la page démarrage rapide) ou le lien **clés** dans le menu de navigation services (à gauche, indiqué par l’icône « clé »), pour révéler vos clés.

    > [!NOTE] 
    > Prenez note de l’une des clés et protégez-la, car vous en aurez besoin plus tard.

## <a name="chapter-2---using-the-person-maker-uwp-application"></a>Chapitre 2-utilisation de l’application UWP « person Maker »

Veillez à télécharger l’application UWP prédéfinie appelée [Person Maker](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/PersonMaker.zip). Cette application n’est pas le produit final de ce cours. il ne s’agit là que d’un outil qui vous aide à créer vos entrées Azure, sur lesquelles repose le projet ultérieur.

**Person Maker** vous permet de créer des entrées Azure, qui sont associées à des personnes et à des groupes de personnes. L’application place toutes les informations nécessaires dans un format qui peut ensuite être utilisé par le FaceAPI, afin de reconnaître les visages des personnes que vous avez ajoutées. 

> PRÉCIEUSE **Person Maker** utilise une limitation de base pour s’assurer que vous ne dépassez pas le nombre d’appels de service par minute pour le **niveau d’abonnement gratuit**. Le texte vert en haut devient rouge et met à jour comme « actif » lorsque la limitation se produit ; Si c’est le cas, il vous suffit d’attendre l’application (elle attendra jusqu’à ce qu’elle puisse continuer à accéder au service face, en la mettant à jour comme « en cours » lorsque vous pourrez l’utiliser à nouveau).

Cette application utilise les bibliothèques *Microsoft. ProjectOxford. face* , ce qui vous permet de tirer pleinement parti de la API visage. Cette bibliothèque est disponible gratuitement en tant que package NuGet. Pour plus d’informations à ce sujet, et les API similaires, veillez [à consulter l’article de référence sur les API](https://docs.microsoft.com/azure/cognitive-services/face/apireference).

> [!NOTE] 
> Il s’agit uniquement des étapes requises. pour plus d’informations sur la façon de procéder, retrouvez le document. L’application **Person Maker** vous permettra d’effectuer les opérations suivantes :
>
> - Créez un *groupe de personnes*, qui est un groupe composé de plusieurs personnes que vous souhaitez associer à celui-ci. Avec votre compte Azure, vous pouvez héberger plusieurs groupes de personnes.
>
> - Créez une *personne*, qui est membre d’un groupe de personnes. Chaque personne est associée à un certain nombre d’images de *face* .
>
> -  Attribuez des *images de visage* à une *personne*pour permettre à votre service Azure API visage de reconnaître une *personne* par la *face*correspondante.
>
> -  *Formez votre* *service Azure API visage*.

N’oubliez pas que pour former cette application et reconnaître des personnes, vous aurez besoin de dix (10) photos proches de chaque personne que vous souhaitez ajouter à votre groupe de personnes. L’application Cam Windows 10 peut vous aider à prendre ces derniers. Vous devez vous assurer que chaque photo est claire (éviter le flou, le masquage ou être trop éloigné, du sujet), que la photo est au format jpg ou png, avec une taille de fichier image supérieure à **4 Mo**et inférieure ou égale à **1 Ko**.

> [!NOTE]
> Si vous suivez ce didacticiel, n’utilisez pas votre propre visage pour la formation, comme lorsque vous placez le HoloLens sur, vous ne pouvez pas vous lancer. Utilisez le visage d’un collègue ou d’un étudiant.

**Créateur de personne**en cours d’exécution :

1.  Ouvrez le dossier **PersonMaker** et double-cliquez sur la *solution PersonMaker* pour l’ouvrir avec *Visual Studio*.

2.  Une fois la *solution PersonMaker* ouverte, assurez-vous que :

    1. La *configuration* de la solution est définie sur **Debug**.

    2. La *plateforme de solution* est définie sur **x86**

    3. La *plateforme cible* est l' **ordinateur local**.

    4.  Vous devrez peut-être également *restaurer les packages NuGet* (cliquez avec le bouton droit sur la *solution* et sélectionnez **restaurer les packages NuGet**).

3.  Cliquez sur *ordinateur local* pour démarrer l’application. Sachez que, sur des écrans plus petits, tout le contenu peut ne pas être visible, bien que vous puissiez le faire défiler plus loin pour l’afficher.

    ![interface utilisateur person Maker](images/AzureLabs-Lab4-07.png)

4.  Insérez votre **clé d’authentification Azure**, que vous devez avoir, à partir de votre service *API visage* dans Azure.

5.  Insérer

    1. *ID* à affecter au *groupe de personnes*. L’ID doit être en minuscules, sans espace. Notez cet ID, car il sera requis plus tard dans votre projet Unity.
    2. *Nom* que vous souhaitez attribuer au groupe de *personnes* (peut avoir des espaces).


6.  Appuyez sur le bouton **créer un groupe de personnes** . Un message de confirmation doit s’afficher sous le bouton.

> [!NOTE]
> Si vous avez une erreur « Accès refusé », vérifiez l’emplacement que vous avez défini pour votre service Azure. Comme indiqué ci-dessus, cette application est conçue pour « ouest des États-Unis ».

> [!IMPORTANT]
> Vous remarquerez que vous pouvez également cliquer sur le bouton **récupérer un groupe connu** : Si vous avez déjà créé un groupe de personnes et que vous souhaitez l’utiliser, plutôt que d’en créer un nouveau. Sachez que si vous cliquez sur *créer un groupe de personnes* avec un groupe connu, cela permet également de récupérer un groupe.

7.  Insérez le *nom* de la *personne* que vous souhaitez créer.

    1. Cliquez sur le bouton **créer une personne** .

    2. Un message de confirmation doit s’afficher sous le bouton.

    3. Si vous souhaitez supprimer une personne que vous avez créée précédemment, vous pouvez écrire le nom dans la zone de texte et appuyer sur **Supprimer la personne**

8.  Assurez-vous de connaître l’emplacement des dix (10) photos de la personne que vous souhaitez ajouter à votre groupe.

9.  Appuyez sur **créer et ouvrir le dossier** pour ouvrir l’Explorateur Windows dans le dossier associé à la personne. Ajoutez les dix (10) images dans le dossier. Ils doivent être au format de fichier *jpg* ou *png* .

10. Cliquez sur **Envoyer à Azure**. Un compteur vous indique l’état de l’envoi, suivi d’un message lorsqu’il est terminé.

11. Une fois le compteur terminé et un message de confirmation s’affiche, cliquez sur **former** pour former votre service.

Une fois le processus terminé, vous êtes prêt à passer à Unity.

## <a name="chapter-3---set-up-the-unity-project"></a>Chapitre 3-configurer le projet Unity

Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **nouveau**. 

    ![Démarrez le nouveau projet Unity.](images/AzureLabs-Lab4-08.png)

2.  Vous devez maintenant fournir un nom de projet Unity. Insérez **MR_FaceRecognition**. Assurez-vous que le type de projet est défini sur **3D**. Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés). Ensuite, cliquez sur **créer un projet**.

    ![Fournissez des détails pour le nouveau projet Unity.](images/AzureLabs-Lab4-09.png)

3.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**. Accédez à **modifier > préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio 2017**. Fermez la fenêtre **Préférences** .

    ![Mettre à jour la préférence éditeur de script.](images/AzureLabs-Lab4-10.png)

4.  Accédez ensuite à **fichier > paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .

    ![Fenêtre Paramètres de build, basculez plateforme vers UWP.](images/AzureLabs-Lab4-11.png)

5.  Accédez à **fichier > paramètres de build** et assurez-vous que :

    1. L' **appareil cible** est défini sur **HoloLens**

        > Pour les casques immersifs, définissez **appareil cible** sur *n’importe quel appareil*.

    2. Le **type de build** est **D3D**
    3. Le **SDK** est configuré sur le **dernier installé**
    4. **Version de Visual Studio** définie sur le **dernier installé**
    5. La **génération et l’exécution** sont définies sur l' **ordinateur local**
    6. Enregistrez la scène et ajoutez-la à la Build. 

        1. Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**. Une fenêtre d’enregistrement s’affiche.

            ![Cliquez sur le bouton Ajouter des scènes ouvertes](images/AzureLabs-Lab4-12.png)

        2. Sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le **scenes**.

            ![Créer un dossier de scripts](images/AzureLabs-Lab4-13.png)

        3. Ouvrez le dossier **scenes** nouvellement créé, puis dans le champ **nom de fichier**:, tapez **FaceRecScene**, puis cliquez sur **Enregistrer**.

            ![Donnez un nom à la nouvelle scène.](images/AzureLabs-Lab4-14.png)

    7. Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.

6. Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* . 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab4-15.png)

7. Dans ce volet, quelques paramètres doivent être vérifiés :

    1. Sous l’onglet **autres paramètres** :

        1. La **version du runtime** de **script** doit être **expérimentale** (équivalent .net 4,6). La modification de cette opération déclenche un besoin de redémarrage de l’éditeur.
        2. Le **backend de script** doit être **.net**
        3. Le **niveau de compatibilité** de l’API doit être **.net 4,6**

            ![Mettez à jour d’autres paramètres.](images/AzureLabs-Lab4-16.png)
      
    2. Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher :

        - **InternetClient**
        - **Webcam**

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab4-17.png)

    3. Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.

        ![Mettez à jour les paramètres X R.](images/AzureLabs-Lab4-18.png)

8.  De retour dans les *paramètres de build*, les  **C# projets Unity** ne sont plus grisés. Cochez la case en regard de cette option. 
9.  Fermez la fenêtre Paramètres de Build.
10. Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).

## <a name="chapter-4---main-camera-setup"></a>Chapitre 4-Configuration de l’appareil photo principal

> [!IMPORTANT]
> Si vous souhaitez ignorer le composant *Unity* configure de ce cours et continuer directement dans le code, n’hésitez pas à [Télécharger ce fichier. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/Azure-MR-304.unitypackage)et à l’importer dans votre projet en tant que [package personnalisé](https://docs.unity3d.com/Manual/AssetPackages.html). Sachez que ce package comprend également l’importation de la *dll Newtonsoft*, traitée dans le [Chapitre 5](#chapter-5--import-the-newtonsoftjson-library). Une fois cette importation effectuée, vous pouvez passer [au chapitre 6](#chapter-6---create-the-faceanalysis-class).

1.  Dans le panneau *hiérarchie* , sélectionnez l' **appareil photo principal**.

2.  Une fois sélectionné, vous pouvez voir tous les composants de la **caméra principale** dans le *panneau Inspecteur*.

    1. L' **objet Camera** doit être nommé **Camera main** (Notez l’orthographe !)

    2. La **balise** principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe !)

    3. Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0

    4. Définir des **indicateurs clairs** sur **couleur unie**

    5. Définir la couleur d' **arrière-plan** du composant Camera sur **Black, alpha 0 (Code hexadécimal : #00000000)**

        ![configurer les composants de l’appareil photo](images/AzureLabs-Lab4-19.png) 

## <a name="chapter-5--import-the-newtonsoftjson-library"></a>Chapitre 5-importer la bibliothèque Newtonsoft. JSON

> [!IMPORTANT]
> Si vous avez importé le « . pour Unity » dans le [dernier chapitre](#chapter-4---main-camera-setup), vous pouvez ignorer ce chapitre.

Pour vous aider à désérialiser et à sérialiser les objets reçus et envoyés au service bot, vous devez télécharger la bibliothèque *Newtonsoft. JSON* . Vous trouverez une version compatible déjà organisée avec la structure de dossiers Unity correcte dans ce [fichier de package Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/newtonsoftDLL.unitypackage). 

Pour importer la bibliothèque :

1.  Téléchargez le package Unity.
2.  Cliquez sur **composants**, **Importer un package**, **package personnalisé**.

    ![Importer la bibliothèque Newtonsoft. JSON](images/AzureLabs-Lab4-20.png)

3.  Recherchez le package Unity que vous avez téléchargé, puis cliquez sur Ouvrir.
4.  Assurez-vous que tous les composants du package sont cochés et cliquez sur **Importer**.

    ![Importer la bibliothèque Newtonsoft. JSON](images/AzureLabs-Lab4-21.png)

## <a name="chapter-6---create-the-faceanalysis-class"></a>Chapitre 6-créer la classe FaceAnalysis

L’objectif de la classe FaceAnalysis est d’héberger les méthodes nécessaires pour communiquer avec votre service de reconnaissance faciale Azure. 

- Une fois que le service a envoyé une image de capture, il l’analyse et identifie les visages dans et détermine s’il appartient à une personne connue. 
- Si une personne connue est trouvée, cette classe affiche son nom en tant que texte de l’interface utilisateur dans la scène.

Pour créer la classe *FaceAnalysis* :

 1. Cliquez avec le bouton droit dans le *dossier ressources* situé dans le panneau projet, puis cliquez sur **créer** un **dossier**de > . Appelez le dossier **scripts**. 

    ![Créez la classe FaceAnalysis.](images/AzureLabs-Lab4-22.png)

2.  Double-cliquez sur le dossier que vous venez de créer pour l’ouvrir. 
3.  Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer** >  **C# script**. Appelez le script *FaceAnalysis*. 
4.  Double-cliquez sur le nouveau script *FaceAnalysis* pour l’ouvrir avec Visual Studio 2017.
5.  Entrez les espaces de noms suivants au-dessus de la classe *FaceAnalysis* :

    ```csharp
        using Newtonsoft.Json;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

6.  Vous devez maintenant ajouter tous les objets qui sont utilisés pour deserialising. Ces objets doivent être ajoutés **en dehors** du script *FaceAnalysis* (sous l’accolade inférieure). 

    ```csharp
        /// <summary>
        /// The Person Group object
        /// </summary>
        public class Group_RootObject
        {
            public string personGroupId { get; set; }
            public string name { get; set; }
            public object userData { get; set; }
        }

        /// <summary>
        /// The Person Face object
        /// </summary>
        public class Face_RootObject
        {
            public string faceId { get; set; }
        }

        /// <summary>
        /// Collection of faces that needs to be identified
        /// </summary>
        public class FacesToIdentify_RootObject
        {
            public string personGroupId { get; set; }
            public List<string> faceIds { get; set; }
            public int maxNumOfCandidatesReturned { get; set; }
            public double confidenceThreshold { get; set; }
        }

        /// <summary>
        /// Collection of Candidates for the face
        /// </summary>
        public class Candidate_RootObject
        {
            public string faceId { get; set; }
            public List<Candidate> candidates { get; set; }
        }

        public class Candidate
        {
            public string personId { get; set; }
            public double confidence { get; set; }
        }

        /// <summary>
        /// Name and Id of the identified Person
        /// </summary>
        public class IdentifiedPerson_RootObject
        {
            public string personId { get; set; }
            public string name { get; set; }
        }
    ```
7. Les méthodes *Start ()* et *Update ()* ne seront pas utilisées. Supprimez-les maintenant. 

8.  À l’intérieur de la classe *FaceAnalysis* , ajoutez les variables suivantes :

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static FaceAnalysis Instance;

        /// <summary>
        /// The analysis result text
        /// </summary>
        private TextMesh labelText;

        /// <summary>
        /// Bytes of the image captured with camera
        /// </summary>
        internal byte[] imageBytes;

        /// <summary>
        /// Path of the image captured with camera
        /// </summary>
        internal string imagePath;

        /// <summary>
        /// Base endpoint of Face Recognition Service
        /// </summary>
        const string baseEndpoint = "https://westus.api.cognitive.microsoft.com/face/v1.0/";

        /// <summary>
        /// Auth key of Face Recognition Service
        /// </summary>
        private const string key = "- Insert your key here -";

        /// <summary>
        /// Id (name) of the created person group 
        /// </summary>
        private const string personGroupId = "- Insert your group Id here -";
    ```

    > [!NOTE]
    > Remplacez la **clé** et le **PersonGroupId** par votre clé de service et l’ID du groupe que vous avez créé précédemment.

9.  Ajoutez la méthode *éveillé ()* , qui initialise la classe, en ajoutant la classe *ImageCapture* à la caméra principale et en appelant la méthode de création d’étiquette :

    ```csharp
        /// <summary>
        /// Initialises this class
        /// </summary>
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            Instance = this;

            // Add the ImageCapture Class to this Game Object
            gameObject.AddComponent<ImageCapture>();

            // Create the text label in the scene
            CreateLabel();
        }
    ```

10. Ajoutez la méthode *CreateLabel ()* , qui crée l’objet *label* pour afficher le résultat de l’analyse :

    ```csharp
        /// <summary>
        /// Spawns cursor for the Main Camera
        /// </summary>
        private void CreateLabel()
        {
            // Create a sphere as new cursor
            GameObject newLabel = new GameObject();

            // Attach the label to the Main Camera
            newLabel.transform.parent = gameObject.transform;
            
            // Resize and position the new cursor
            newLabel.transform.localScale = new Vector3(0.4f, 0.4f, 0.4f);
            newLabel.transform.position = new Vector3(0f, 3f, 60f);

            // Creating the text of the Label
            labelText = newLabel.AddComponent<TextMesh>();
            labelText.anchor = TextAnchor.MiddleCenter;
            labelText.alignment = TextAlignment.Center;
            labelText.tabSize = 4;
            labelText.fontSize = 50;
            labelText.text = ".";       
        }
    ```

11. Ajoutez la méthode *DetectFacesFromImage ()* et *GetImageAsByteArray ()* . La première demande au service de reconnaissance faciale de détecter tout visage possible dans l’image envoyée, tandis que ce dernier est nécessaire pour convertir l’image capturée en un tableau d’octets :

    ```csharp
        /// <summary>
        /// Detect faces from a submitted image
        /// </summary>
        internal IEnumerator DetectFacesFromImage()
        {
            WWWForm webForm = new WWWForm();
            string detectFacesEndpoint = $"{baseEndpoint}detect";

            // Change the image into a bytes array
            imageBytes = GetImageAsByteArray(imagePath);

            using (UnityWebRequest www = 
                UnityWebRequest.Post(detectFacesEndpoint, webForm))
            {
                www.SetRequestHeader("Ocp-Apim-Subscription-Key", key);
                www.SetRequestHeader("Content-Type", "application/octet-stream");
                www.uploadHandler.contentType = "application/octet-stream";
                www.uploadHandler = new UploadHandlerRaw(imageBytes);
                www.downloadHandler = new DownloadHandlerBuffer();

                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;
                Face_RootObject[] face_RootObject = 
                    JsonConvert.DeserializeObject<Face_RootObject[]>(jsonResponse);

                List<string> facesIdList = new List<string>();
                // Create a list with the face Ids of faces detected in image
                foreach (Face_RootObject faceRO in face_RootObject)
                {
                    facesIdList.Add(faceRO.faceId);
                    Debug.Log($"Detected face - Id: {faceRO.faceId}");
                }
                
                StartCoroutine(IdentifyFaces(facesIdList));
            }
        }

        /// <summary>
        /// Returns the contents of the specified file as a byte array.
        /// </summary>
        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);
            BinaryReader binaryReader = new BinaryReader(fileStream);
            return binaryReader.ReadBytes((int)fileStream.Length);
        }
    ```

12. Ajoutez la méthode *IdentifyFaces ()* , qui demande au *service de reconnaissance faciale* d’identifier toute face connue précédemment détectée dans l’image soumise. La demande retourne un ID de la personne identifiée, mais pas le nom :

    ```csharp
        /// <summary>
        /// Identify the faces found in the image within the person group
        /// </summary>
        internal IEnumerator IdentifyFaces(List<string> listOfFacesIdToIdentify)
        {
            // Create the object hosting the faces to identify
            FacesToIdentify_RootObject facesToIdentify = new FacesToIdentify_RootObject();
            facesToIdentify.faceIds = new List<string>();
            facesToIdentify.personGroupId = personGroupId;
            foreach (string facesId in listOfFacesIdToIdentify)
            {
                facesToIdentify.faceIds.Add(facesId);
            }
            facesToIdentify.maxNumOfCandidatesReturned = 1;
            facesToIdentify.confidenceThreshold = 0.5;

            // Serialize to Json format
            string facesToIdentifyJson = JsonConvert.SerializeObject(facesToIdentify);
            // Change the object into a bytes array
            byte[] facesData = Encoding.UTF8.GetBytes(facesToIdentifyJson);

            WWWForm webForm = new WWWForm();
            string detectFacesEndpoint = $"{baseEndpoint}identify";

            using (UnityWebRequest www = UnityWebRequest.Post(detectFacesEndpoint, webForm))
            {
                www.SetRequestHeader("Ocp-Apim-Subscription-Key", key);
                www.SetRequestHeader("Content-Type", "application/json");
                www.uploadHandler.contentType = "application/json";
                www.uploadHandler = new UploadHandlerRaw(facesData);
                www.downloadHandler = new DownloadHandlerBuffer();

                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;
                Debug.Log($"Get Person - jsonResponse: {jsonResponse}");
                Candidate_RootObject [] candidate_RootObject = JsonConvert.DeserializeObject<Candidate_RootObject[]>(jsonResponse);

                // For each face to identify that ahs been submitted, display its candidate
                foreach (Candidate_RootObject candidateRO in candidate_RootObject)
                {
                    StartCoroutine(GetPerson(candidateRO.candidates[0].personId));
                    
                    // Delay the next "GetPerson" call, so all faces candidate are displayed properly
                    yield return new WaitForSeconds(3);
                }           
            }
        }
    ```

13. Ajoutez la méthode *GetPerson ()* . En fournissant l’ID de personne, cette méthode demande au *service de reconnaissance faciale* de retourner le nom de la personne identifiée :

    ```csharp
        /// <summary>
        /// Provided a personId, retrieve the person name associated with it
        /// </summary>
        internal IEnumerator GetPerson(string personId)
        {
            string getGroupEndpoint = $"{baseEndpoint}persongroups/{personGroupId}/persons/{personId}?";
            WWWForm webForm = new WWWForm();

            using (UnityWebRequest www = UnityWebRequest.Get(getGroupEndpoint))
            {
                www.SetRequestHeader("Ocp-Apim-Subscription-Key", key);
                www.downloadHandler = new DownloadHandlerBuffer();
                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;

                Debug.Log($"Get Person - jsonResponse: {jsonResponse}");
                IdentifiedPerson_RootObject identifiedPerson_RootObject = JsonConvert.DeserializeObject<IdentifiedPerson_RootObject>(jsonResponse);

                // Display the name of the person in the UI
                labelText.text = identifiedPerson_RootObject.name;
            }
        }
    ```

14.  N’oubliez pas d' **Enregistrer** les modifications avant de revenir à l’éditeur Unity.
15.  Dans l’éditeur Unity, faites glisser le script FaceAnalysis du dossier scripts du panneau projet vers l’objet caméra principal dans le *panneau hiérarchie*. Le nouveau composant script sera ajouté à la caméra principale. 

![Placer FaceAnalysis sur l’appareil photo principal](images/AzureLabs-Lab4-23.png)


## <a name="chapter-7---create-the-imagecapture-class"></a>Chapitre 7-créer la classe ImageCapture

L’objectif de la classe *ImageCapture* est d’héberger les méthodes nécessaires pour communiquer avec votre *service de reconnaissance faciale Azure* afin d’analyser l’image que vous allez capturer, d’identifier les visages et de déterminer si elle appartient à une personne connue. Si une personne connue est trouvée, cette classe affiche son nom en tant que texte de l’interface utilisateur dans la scène.

Pour créer la classe *ImageCapture* :
 
1.  Cliquez avec le bouton droit dans le dossier **scripts** que vous avez créé précédemment, puis cliquez sur **créer**,  **C# script**. Appelez le script *ImageCapture*. 
2.  Double-cliquez sur le nouveau script *ImageCapture* pour l’ouvrir avec Visual Studio 2017.
3.  Entrez les espaces de noms suivants au-dessus de la classe ImageCapture :

    ```csharp
        using System.IO;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;
        using UnityEngine.XR.WSA.WebCam;
    ```

4.  À l’intérieur de la classe *ImageCapture* , ajoutez les variables suivantes :

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static ImageCapture instance;

        /// <summary>
        /// Keeps track of tapCounts to name the captured images 
        /// </summary>
        private int tapsCount;

        /// <summary>
        /// PhotoCapture object used to capture images on HoloLens 
        /// </summary>
        private PhotoCapture photoCaptureObject = null;

        /// <summary>
        /// HoloLens class to capture user gestures
        /// </summary>
        private GestureRecognizer recognizer;
    ```

5.  Ajoutez les méthodes *éveillé ()* et *Start ()* nécessaires à l’initialisation de la classe et autorisez le HoloLens à capturer les mouvements de l’utilisateur :

    ```csharp
        /// <summary>
        /// Initialises this class
        /// </summary>
        private void Awake()
        {
            instance = this;
        }

        /// <summary>
        /// Called right after Awake
        /// </summary>
        void Start()
        {
            // Initialises user gestures capture 
            recognizer = new GestureRecognizer();
            recognizer.SetRecognizableGestures(GestureSettings.Tap);
            recognizer.Tapped += TapHandler;
            recognizer.StartCapturingGestures();
        }
    ```

6.  Ajoutez le *TapHandler ()* qui est appelé lorsque l’utilisateur effectue un mouvement *Tap* :

    ```csharp
        /// <summary>
        /// Respond to Tap Input.
        /// </summary>
        private void TapHandler(TappedEventArgs obj)
        {
            tapsCount++;
            ExecuteImageCaptureAndAnalysis();
        }
    ```

7.  Ajoutez la méthode *ExecuteImageCaptureAndAnalysis ()* , qui va commencer le processus de capture d’image :

    ```csharp
        /// <summary>
        /// Begin process of Image Capturing and send To Azure Computer Vision service.
        /// </summary>
        private void ExecuteImageCaptureAndAnalysis()
        {
            Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending
                ((res) => res.width * res.height).First();
            Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);

            PhotoCapture.CreateAsync(false, delegate (PhotoCapture captureObject)
            {
                photoCaptureObject = captureObject;

                CameraParameters c = new CameraParameters();
                c.hologramOpacity = 0.0f;
                c.cameraResolutionWidth = targetTexture.width;
                c.cameraResolutionHeight = targetTexture.height;
                c.pixelFormat = CapturePixelFormat.BGRA32;

                captureObject.StartPhotoModeAsync(c, delegate (PhotoCapture.PhotoCaptureResult result)
                {
                    string filename = string.Format(@"CapturedImage{0}.jpg", tapsCount);
                    string filePath = Path.Combine(Application.persistentDataPath, filename);

                    // Set the image path on the FaceAnalysis class
                    FaceAnalysis.Instance.imagePath = filePath;

                    photoCaptureObject.TakePhotoAsync
                    (filePath, PhotoCaptureFileOutputFormat.JPG, OnCapturedPhotoToDisk);
                });
            });
        }
    ```

8.  Ajoutez les gestionnaires qui sont appelés lorsque le processus de capture de photos est terminé :

    ```csharp
        /// <summary>
        /// Called right after the photo capture process has concluded
        /// </summary>
        void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
        {
            photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
        }

        /// <summary>
        /// Register the full execution of the Photo Capture. If successful, it will begin the Image Analysis process.
        /// </summary>
        void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
        {
            photoCaptureObject.Dispose();
            photoCaptureObject = null;

            // Request image caputer analysis
            StartCoroutine(FaceAnalysis.Instance.DetectFacesFromImage());
        }
    ```

9. N’oubliez pas d' **Enregistrer** les modifications avant de revenir à l’éditeur Unity.

## <a name="chapter-8---building-the-solution"></a>Chapitre 8-génération de la solution

Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre HoloLens.

Avant cela, assurez-vous que :

-   Tous les paramètres mentionnés dans le chapitre 3 sont correctement définis. 
-   Le script *FaceAnalysis* est attaché à l’objet Camera principal. 
-   La **clé d’authentification** et l' **ID de groupe** ont été définis dans le script *FaceAnalysis* .

R ce point vous êtes prêt à générer la solution. Une fois la solution générée, vous êtes prêt à déployer votre application.

Pour commencer le processus de génération :

1.  Enregistrez la scène en cours en cliquant sur fichier, puis sur Enregistrer.
2.  Accédez à fichier, paramètres de build, puis cliquez sur Ajouter des scènes ouvertes.
3.  Veillez à cocher C# les projets Unity.

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-24.png)

4.  Appuyez sur générer. Dans ce cas, Unity lance une fenêtre de l’Explorateur de fichiers, où vous devez créer, puis sélectionner un dossier dans lequel créer l’application. Créez ce dossier maintenant, dans le projet Unity, et appelez-le. Ensuite, avec le dossier d’application sélectionné, appuyez sur Sélectionner un dossier. 
5.  Unity commence à générer votre projet, en dehors du dossier de l’application. 
6.  Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l’Explorateur de fichiers s’ouvre à l’emplacement de votre Build.

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-25.png)

7.  Ouvrez le dossier de votre application, puis ouvrez la solution nouveau projet (comme indiqué ci-dessus, MR_FaceRecognition. sln).


## <a name="chapter-9---deploying-your-application"></a>Chapitre 9-déploiement de votre application

Pour effectuer un déploiement sur HoloLens :

1.  Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur**. Pour cela, procédez comme suit :

    1. Tout en portant votre HoloLens, ouvrez les **paramètres**.
    2. Accéder au **réseau & Internet > Wi-Fi > options avancées**
    3. Notez l’adresse **IPv4** .
    4. Ensuite, revenez aux **paramètres**, puis à **mettre à jour & > de sécurité pour les développeurs** 
    5. Définissez le mode développeur sur.

2.  Accédez à votre nouvelle build Unity (le dossier de l' *application* ) et ouvrez le fichier solution avec *Visual Studio*.
3.  Dans la configuration de la solution, sélectionnez **Déboguer**.
4.  Dans la plateforme de la solution, sélectionnez **x86**, **ordinateur distant**. 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-26.png)
 
5.  Accédez au **menu Générer** , puis cliquez sur **déployer la solution**pour chargement l’application à votre HoloLens.
6.  Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.

> [!NOTE]
> Pour effectuer un déploiement sur un casque immersif, définissez la plateforme de la **solution** sur *ordinateur local*et définissez la **configuration** sur *Déboguer*, avec *x86* comme **plateforme**. Déployez ensuite sur l’ordinateur local, à l’aide du **menu Générer**, en sélectionnant *déployer la solution*. 


## <a name="chapter-10---using-the-application"></a>Chapitre 10-utilisation de l’application

1.  Porter le HoloLens, lancer l’application.
2.  Examinez la personne que vous avez inscrite auprès du *API visage*. Vérifiez que :

    -  Le visage de la personne n’est pas trop éloigné et clairement visible
    -  L’éclairage de l’environnement n’est pas trop sombre

3.  Utilisez le geste TAP pour capturer l’image de la personne.
4.  Attendez que l’application envoie la demande d’analyse et que vous receviez une réponse.
5.  Si la personne a été correctement reconnue, le nom de la personne s’affiche comme texte de l’interface utilisateur.
6.  Vous pouvez répéter le processus de capture à l’aide du geste TAP (TAP) toutes les quelques secondes.

## <a name="your-finished-azure-face-api-application"></a>Votre application Azure API Visage terminée

Félicitations, vous avez créé une application de réalité mixte qui tire parti du service de reconnaissance faciale Azure pour détecter les visages au sein d’une image et identifier les visages connus.

![résultat de la fin de ce cours](images/AzureLabs-Lab4-00.png)

## <a name="bonus-exercises"></a>Exercices bonus

### <a name="exercise-1"></a>Exercice 1

Le **API visage Azure** est suffisamment puissant pour détecter jusqu’à 64 faces dans une image unique. Étendez l’application afin qu’elle puisse reconnaître deux ou trois visages, parmi de nombreuses autres personnes.

### <a name="exercise-2"></a>Exercice 2

Le **API visage Azure** est également en mesure de fournir toutes sortes d’informations sur les attributs. Intégrez cela dans l’application. Cela peut être encore plus intéressant, lorsqu’il est associé au [API émotion](https://azure.microsoft.com/services/cognitive-services/emotion/).
