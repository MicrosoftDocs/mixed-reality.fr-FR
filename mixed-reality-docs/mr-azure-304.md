---
title: MR et Azure 304 - reconnaissance faciale
description: Terminer ce cours pour apprendre à implémenter la reconnaissance faciale de Azure au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, mixte réalité academy, unity, didacticiel, api, face à la reconnaissance, vr immersives, hololens,
ms.openlocfilehash: 6330d3e5c51d6b2cbc43ea795a3f953a5b14d6f1
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596466"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br> 

# <a name="mr-and-azure-304-face-recognition"></a>MR et Azure 304 : Reconnaissance faciale

![résultat de cette formation](images/AzureLabs-Lab4-00.png)

Dans ce cours vous allez apprendre à ajouter des fonctionnalités de reconnaissance de face à une application de réalité mixte, à l’aide d’Azure Cognitive Services, avec l’API visage de Microsoft.

*Azure API visage* est un service Microsoft, qui fournit aux développeurs avec les algorithmes de reconnaissance faciale plus avancées, tout cela dans le cloud. Le *API visage* a deux fonctions principales : détection avec des attributs de visage et doivent faire face de reconnaissance. Cela permet aux développeurs de simplement définir un ensemble de groupes de visages et ensuite, envoyez des images de la requête au service ultérieurement, pour déterminer auxquels appartient un visage. Pour plus d’informations, visitez le [page de reconnaissance faciale de Azure](https://azure.microsoft.com/services/cognitive-services/face/).

Avoir terminé ce cours, vous aurez une réalité mixte application HoloLens, qui sera en mesure d’effectuer les opérations suivantes :

1. Utilisez un **appuyez sur le mouvement** pour initier la capture d’une image à l’aide de la caméra HoloLens intégrée. 
2. Envoyer l’image capturée à le *API visage de Azure* service.
3. Recevoir les résultats de la *API visage* algorithme.
4. Utiliser une Interface utilisateur simple, pour afficher le nom des personnes mise en correspondance.

Cela va vous apprendre à obtenir les résultats à partir du Service d’API visage dans votre application basée sur Unity de réalité mixte.

Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception. Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity. Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 304 : Reconnaissance faciale</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Si ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques Windows Mixed Reality IMMERSIFS (VR). Étant donné que des casques IMMERSIFS (VR) ne sont pas accessibles caméras, vous devez une caméra externe connectée à votre PC. Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge des casques IMMERSIFS (VR).

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .

Nous recommandons le matériel et logiciel pour ce cours suivants :

- Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)
- [Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé](install-the-tools.md)
- [Le SDK Windows 10 dernières](install-the-tools.md)
- [Unity 2017.4](install-the-tools.md)
- [Visual Studio 2017](install-the-tools.md)
- Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé
- Un appareil photo connecté à votre PC (pour le développement de casque immersives)
- Accès à Internet pour le programme d’installation Azure et l’extraction de l’API visage

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).
2.  Configurer et tester votre HoloLens. Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur). 

Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1---the-azure-portal"></a>Chapitre 1 : le portail Azure

Pour utiliser le *API visage* service dans Azure, vous devez configurer une instance du service à être mis à disposition de votre application.

1.  Tout d’abord, connectez-vous à la [Azure Portal](https://portal.azure.com). 

    > [!NOTE]
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *API visage*, appuyez sur **entrée**.

    ![Rechercher des api visage](images/AzureLabs-Lab4-01.png)

    > [!NOTE]
    > Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.

3.  La nouvelle page doit fournir une description de la *API visage* service. En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.

    ![doivent faire face les informations sur l’api](images/AzureLabs-Lab4-02.png)

4.  Une fois que vous avez cliqué sur **créer**:

    1. Insérez votre nom souhaité pour cette instance de service.

    2. Sélectionnez un abonnement.

    3. Sélectionnez le niveau de tarification approprié pour vous, si c’est la première heure de création d’un *Service de l’API visage*, un niveau gratuit (nommé F0) doit être disponible pour vous.

    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs). 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. L’application UWP, **personne Maker**, que vous utilisez une version ultérieure, requiert l’utilisation de « Ouest des États-Unis » pour l’emplacement.

    6. Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.

    7. Sélectionnez **créer*.**

        ![Créer face service api](images/AzureLabs-Lab4-03.png)

5.  Une fois que vous avez cliqué sur **créer*** avoir à attendre que le service doit être créé, cette opération peut prendre une minute.

6.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![notification de création de service](images/AzureLabs-Lab4-04.png)

7.  Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.

    ![Accédez à la notification de ressource](images/AzureLabs-Lab4-05.png)

8.  Lorsque vous êtes prêt, cliquez sur **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.

    ![accès doivent faire face les clés api](images/AzureLabs-Lab4-06.png)

9.  Dans ce didacticiel, votre application devra effectuer des appels à votre service, par l’intermédiaire à l’aide de l’abonnement de votre service 'key'. À partir de la *Guide de démarrage rapide* page, de votre *API visage* de service, le premier point est le numéro 1, à *récupérez vos clés.*

10. Sur le *Service* page Sélectionnez soit le bleu **clés** hyperlink (le cas sur la page de démarrage rapide), ou le **clés** lien dans le menu de navigation de services (à gauche, désigné par le ' clé ' icône), pour afficher vos clés.

    > [!NOTE] 
    > Prenez note de l’une des clés et à la sauvegarde, car vous en aurez besoin plus tard.

## <a name="chapter-2---using-the-person-maker-uwp-application"></a>Chapitre 2 : à l’aide de l’application de la « Personne Maker » UWP

Veillez à télécharger l’Application UWP prédéfini appelé [personne Maker](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/PersonMaker.zip). Cette application n’est pas le produit final de ce cours, un simple outil pour vous aider à créer vos entrées de Azure, le projet ultérieur se basent sur.

**Personne Maker** vous permet de créer les entrées Azure, qui sont associées à des personnes et groupes d’utilisateurs. L’application place toutes les informations nécessaires dans un format qui peut ensuite être utilisé ultérieurement par le FaceAPI, afin de reconnaître les visages des personnes auxquelles vous avez ajouté. 

> [IMPORTANT] **Personne Maker** utilise une limitation base, afin de garantir que vous ne dépassez pas le nombre d’appels de service par minute pour le **niveau d’abonnement gratuit**. Le texte vert en haut modifie en rouge et mettre à jour « Active » lors de la limitation s’applique ; Si c’est le cas, attendez simplement l’application (il attend jusqu'à ce qu’il peut ensuite continuer d’accéder au service de visage, la mise à jour « IN-active » lorsque vous pouvez l’utiliser à nouveau).

Cette application utilise le *Microsoft.ProjectOxford.Face* utilisent des bibliothèques, ce qui vous permet de rendre complet de l’API visage. Cette bibliothèque est disponible gratuitement en tant qu’un NuGet Package. Pour plus d’informations sur ce point et est similaire, API [veillez à consulter l’article de référence API](https://docs.microsoft.com/azure/cognitive-services/face/apireference).

> [!NOTE] 
> Il s’agit simplement les étapes requises, des instructions pour savoir comment effectuer les opérations suivantes est plus bas dans le document. Le **personne Maker** application vous permettra de :
>
> - Créer un *groupe de personnes*, qui est un groupe composé de plusieurs personnes que vous souhaitez lui associer. Avec votre compte Azure, vous pouvez héberger plusieurs groupes de personnes.
>
> - Créer un *personne*, qui est un membre d’un groupe de personnes. Chaque personne dispose d’un nombre de *Face* images associées.
>
> -  Affecter *doivent faire face les images* à un *personne*pour permettre à votre Service d’API visage Azure de reconnaître un *personne* par correspondant *face*.
>
> -  *Train* votre *Azure doivent faire Face les API Service*.

Sachez, pour former à reconnaître les personnes de cette application, vous devez en gros plan photos dix (10) de chaque personne pour laquelle vous souhaitez ajouter à votre groupe de personnes. L’application de FAO Windows 10 peuvent vous aider à prendre ceux-ci. Vous devez vous assurer que chaque photo est désactivée (évitez flou, en masquant ou en cours trop loin, à partir de l’objet), ont la photo au format jpg ou png, avec la taille du fichier image en cours ne dépassant **4 Mo**et pas moins de **1 Ko**.

> [!NOTE]
> Si vous suivez ce didacticiel, n’utilisez pas votre propre image pour l’apprentissage, comme quand vous placez le HoloLens, vous ne pouvez pas regarder vous-même. Utilisez la face d’un collègue ou fellow étudiant.

En cours d’exécution **personne Maker**:

1.  Ouvrez le **PersonMaker** dossier et double cliquez sur le *PersonMaker solution* pour l’ouvrir avec *Visual Studio*.

2.  Une fois le *PersonMaker solution* est ouvert, assurez-vous que :

    1. Le *Configuration de la Solution* a la valeur **déboguer**.

    2. Le *plateforme de Solution* a la valeur **x86**

    3. Le *plateforme cible* est **ordinateur Local**.

    4.  Vous devrez peut-être également *restaurer les Packages NuGet* (avec le bouton droit le *Solution* et sélectionnez **restaurer les Packages NuGet**).

3.  Cliquez sur *ordinateur Local* et démarre l’application. N’oubliez pas, sur les petits écrans, tout le contenu n’est pas forcément visible, bien que vous pouvez faire défiler plus bas pour l’afficher.

    ![interface utilisateur personne maker](images/AzureLabs-Lab4-07.png)

4.  Insérez votre **clé d’authentification Azure**, qui doit avoir, à partir de votre *API visage* service dans Azure.

5.  Insertion :

    1. Le *ID* vous souhaitez affecter à la *groupe de personnes*. L’ID doit être en minuscules, sans espaces. Notez cet ID, car il sera requis plus loin dans votre projet Unity.
    2. Le *nom* vous souhaitez affecter à la *groupe de personnes* (peut avoir des espaces).


6.  Appuyez sur **créer un groupe de personnes** bouton. Un message de confirmation doit apparaître sous le bouton.

> [!NOTE]
> Si vous avez une erreur « Accès refusé », vérifiez l’emplacement que vous définissez pour votre service Azure. Comme indiqué ci-dessus, cette application est conçue pour les États-Unis de l’ouest.

> [!IMPORTANT]
> Vous remarquerez que vous pouvez également cliquer sur le **extraire un groupe connu** bouton : il s’agit de si vous avez déjà créé une personne, groupe et qui souhaitent utiliser, plutôt que de créer un nouveau. N’oubliez pas, si vous cliquez sur *créer un groupe de personnes* avec un groupe connu, cette opération va également extraire un groupe.

7.  Insérer le *nom* de la *personne* vous souhaitez créer.

    1. Cliquez sur le **personne créer** bouton.

    2. Un message de confirmation doit apparaître sous le bouton.

    3. Si vous souhaitez supprimer une personne que vous avez créé précédemment, vous pouvez écrire le nom dans la zone de texte et appuyez sur **supprimer la personne**

8.  Assurez-vous que vous connaissez l’emplacement de photos dix (10) de la personne que vous souhaitez ajouter à votre groupe.

9.  Appuyez sur **créer et ouvrir le dossier** pour ouvrir l’Explorateur Windows dans le dossier associé à la personne. Ajoutez les images de dix (10) dans le dossier. Elles doivent être *JPG* ou *PNG* format de fichier.

10. Cliquez sur **envoyer sur Azure**. Un compteur vous montrera l’état de l’envoi, suivi d’un message lorsqu’il se termine.

11. Une fois que le compteur est terminée et un message de confirmation a été affiché, cliquez sur **former** pour l’apprentissage de votre Service.

Une fois le processus terminé, vous êtes prêt à passer dans Unity.

## <a name="chapter-3---set-up-the-unity-project"></a>Chapitre 3 - configurer le projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **New**. 

    ![Démarrer un nouveau projet Unity.](images/AzureLabs-Lab4-08.png)

2.  Maintenant, vous devez fournir un nom de projet Unity. Insérer **MR_FaceRecognition**. Assurez-vous que le type de projet est défini sur **3D**. Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![Fournissent des détails pour un projet Unity.](images/AzureLabs-Lab4-09.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **Modifier > Préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![Mettre à jour les préférences de l’éditeur de script.](images/AzureLabs-Lab4-10.png)

4.  Ensuite, accédez à **fichier > Paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **plateforme basculer** bouton.

    ![Fenêtre Paramètres, plateforme de commutation à UWP de la génération.](images/AzureLabs-Lab4-11.png)

5.  Accédez à **fichier > Paramètres de Build** et vous assurer que :

    1. **Équipement cible** a la valeur **HoloLens**

        > Pour des casques IMMERSIFS, définissez **appareil cible** à *n’importe quel appareil*.

    2. **Type de build** a la valeur **D3D**
    3. **Kit de développement logiciel** a la valeur **dernière installé**
    4. **Version de Visual Studio** a la valeur **dernière installé**
    5. **Générez et exécutez** est défini sur **ordinateur Local**
    6. Enregistrer la scène et l’ajouter à la build. 

        1. Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.

            ![Cliquez sur Ajouter un bouton scènes ouvert](images/AzureLabs-Lab4-12.png)

        2. Sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![Créer un nouveau dossier de scripts](images/AzureLabs-Lab4-13.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le **nom de fichier**: champ de texte, tapez **FaceRecScene**, puis appuyez sur **enregistrer**.

            ![Donnez un nom à nouvelle scène.](images/AzureLabs-Lab4-14.png)

    7. Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.

6. Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve. 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab4-15.png)

7. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1. Dans le **autres paramètres** onglet :

        1. **Écriture de scripts** **Version du Runtime** doit être **expérimental** (équivalent .NET 4.6). Si vous modifiez cet déclenchera une nécessité de redémarrer l’éditeur.
        2. **Script principal** doit être **.NET**
        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**

            ![Mettre à jour les autres paramètres.](images/AzureLabs-Lab4-16.png)
      
    2. Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        - **InternetClient**
        - **Webcam**

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab4-17.png)

    3. Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.

        ![Mettre à jour les paramètres de R X.](images/AzureLabs-Lab4-18.png)

8.  Dans *paramètres de Build*, **Unity C# projets** est n’est plus grisée ; Cochez la case à cocher en regard de cela. 
9.  Fermez la fenêtre Paramètres de Build.
10. Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).

## <a name="chapter-4---main-camera-setup"></a>Chapitre 4 - le programme d’installation de la caméra principale

> [!IMPORTANT]
> Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/Azure-MR-304.unitypackage)et l’importer dans votre projet en tant qu’un [personnalisé Package](https://docs.unity3d.com/Manual/AssetPackages.html). N’oubliez pas que ce package inclut également l’importation de la *DLL Newtonsoft*, comme indiqué dans [chapitre 5](#chapter-5--import-the-newtonsoft.json-library). Avec cela importé, vous pouvez continuer à partir de [chapitre 6](#chapter-6-create-the-faceanalysis-class).

1.  Dans le *hiérarchie* Panneau de configuration, sélectionnez le **Main Camera**.

2.  Une fois sélectionné, vous serez en mesure de voir tous les composants de la **Main Camera** dans le *panneau Inspecteur*.

    1. Le **objet caméra** doit être nommé **Main Camera** (Notez l’orthographe !)

    2. La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe !)

    3. Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**

    4. Définissez **d’effacer les indicateurs** à **couleur unie**

    5. Définir le **arrière-plan** couleur du composant de caméra à **noir, Alpha 0 (Hex Code : #00000000)**

        ![configurer les composants de l’appareil photo](images/AzureLabs-Lab4-19.png) 

## <a name="chapter-5--import-the-newtonsoftjson-library"></a>Chapitre 5 : importer la bibliothèque de Newtonsoft.Json

> [!IMPORTANT]
> Si vous avez importé le « .unitypackage » dans le [dernier chapitre](#chapter-4--main-camera-setup), vous pouvez ignorer ce chapitre.

Pour vous aider à désérialiser et sérialiser des objets reçus et envoyés au Service Bot, vous devez télécharger le *Newtonsoft.Json* bibliothèque. Vous trouverez une version compatible déjà organisée avec la structure de dossiers Unity correcte dans ce [fichier de package Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20304%20-%20Face%20recognition/newtonsoftDLL.unitypackage). 

Pour importer la bibliothèque :

1.  Télécharger le Package Unity.
2.  Cliquez sur **actifs**, **importer un Package**, **Package personnalisé**.

    ![Importer la bibliothèque de Newtonsoft.Json](images/AzureLabs-Lab4-20.png)

3.  Recherchez le Package Unity que vous avez téléchargé, puis cliquez sur Ouvrir.
4.  Assurez-vous que tous les composants du package sont cochés et cliquez sur **importation**.

    ![Importer la bibliothèque de Newtonsoft.Json](images/AzureLabs-Lab4-21.png)

## <a name="chapter-6---create-the-faceanalysis-class"></a>Chapitre 6 : créer la classe FaceAnalysis

L’objectif de la classe FaceAnalysis consiste à héberger les méthodes nécessaires pour communiquer avec votre Service de reconnaissance de visage Azure. 

- Après l’envoi d’une image de capture le service, il analyse il et identifier des visages détectés et déterminer si une appartient à une personne connue. 
- Si une personne connue est trouvée, cette classe affiche son nom sous forme de texte de l’interface utilisateur dans la scène.

Pour créer le *FaceAnalysis* classe :

 1. Avec le bouton droit dans le *dossier Assets* situé dans le panneau de configuration de projet, puis cliquez sur **créer** > **dossier**. Appelez le dossier **Scripts**. 

    ![Créer la classe FaceAnalysis.](images/AzureLabs-Lab4-22.png)

2.  Double-cliquez sur le dossier venez de créer, pour l’ouvrir. 
3.  Avec le bouton droit dans le dossier, puis cliquez sur **créer**  >   **C# Script**. Appeler le script *FaceAnalysis*. 
4.  Double-cliquez sur le nouveau *FaceAnalysis* script pour l’ouvrir avec Visual Studio 2017.
5.  Entrez les espaces de noms suivants ci-dessus le *FaceAnalysis* classe :

    ```csharp
        using Newtonsoft.Json;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

6.  Vous devez maintenant ajouter tous les objets qui sont utilisés pour deserialising. Ces objets doivent être ajoutés **en dehors de** de la *FaceAnalysis* script (en dessous de l’accolade en bas). 

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
7. Le *Start()* et *Update()* méthodes ne sera pas utilisé, donc les supprimer maintenant. 

8.  À l’intérieur de la *FaceAnalysis* de classe, ajoutez les variables suivantes :

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
    > Remplacez le **clé** et **personGroupId** avec votre clé de Service et l’Id du groupe que vous avez créé précédemment.

9.  Ajouter le *Awake()* (méthode), lequel initialises la classe, ajout de la *ImageCapture* classe à la caméra principale et appelle la méthode de création d’étiquette :

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

10. Ajouter le *CreateLabel()* (méthode), ce qui crée le *étiquette* objet pour afficher le résultat de l’analyse :

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

11. Ajouter le *DetectFacesFromImage()* et *GetImageAsByteArray()* (méthode). La première demande le Service de reconnaissance de visage pour détecter les visages possible dans l’image soumis, alors que ce dernier est nécessaire pour convertir l’image capturée dans un tableau d’octets :

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

12. Ajouter le *IdentifyFaces()* (méthode), qui demande le *Service de reconnaissance faciale* pour identifier toute face connu précédemment détecté dans l’image soumis. La demande renvoie un id de la personne identifiée mais pas le nom :

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

            // Serialise to Json format
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

13. Ajouter le *GetPerson()* (méthode). En fournissant son id, cette méthode, les demandes pour le *Service de reconnaissance faciale* pour retourner le nom de la personne identifié :

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

14.  N’oubliez pas de **enregistrer** les modifications avant de revenir à l’éditeur Unity.
15.  Dans l’éditeur Unity, faites glisser le script FaceAnalysis à partir du dossier Scripts dans le panneau de configuration de projet à l’objet Main Camera dans le *Panneau de la hiérarchie*. Le nouveau composant de script sera être ainsi ajouté à la caméra principale. 

![FaceAnalysis place sur la caméra principale](images/AzureLabs-Lab4-23.png)


## <a name="chapter-7---create-the-imagecapture-class"></a>Chapitre 7 - créer la classe ImageCapture

L’objectif de la *ImageCapture* classe consiste à héberger les méthodes nécessaires pour communiquer avec votre *Service de reconnaissance de visage Azure* pour analyser l’image que vous allez capturer, identification des visages qu’il contient et déterminer s’il appartient à une personne connue. Si une personne connue est trouvée, cette classe affiche son nom sous forme de texte de l’interface utilisateur dans la scène.

Pour créer le *ImageCapture* classe :
 
1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier que vous avez créé précédemment, puis cliquez sur **créer**,  **C# Script**. Appeler le script *ImageCapture*. 
2.  Double-cliquez sur le nouveau *ImageCapture* script pour l’ouvrir avec Visual Studio 2017.
3.  Entrez les espaces de noms suivantes au-dessus de la classe ImageCapture :

    ```csharp
        using System.IO;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;
        using UnityEngine.XR.WSA.WebCam;
    ```

4.  À l’intérieur de la *ImageCapture* de classe, ajoutez les variables suivantes :

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

5.  Ajouter le *Awake()* et *Start()* méthodes nécessaires pour initialiser la classe et de permettre la HoloLens capturer les mouvements de l’utilisateur :

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

6.  Ajouter le *TapHandler()* qui est appelée lorsque l’utilisateur effectue un *appuyez sur* mouvements :

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

7.  Ajouter le *ExecuteImageCaptureAndAnalysis()* (méthode), qui commence le processus de capture d’Image :

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

8.  Ajoutez les gestionnaires sont appelés quand le processus de capture photo est terminé :

    ```csharp
        /// <summary>
        /// Called right after the photo capture process has concluded
        /// </summary>
        void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
        {
            photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
        }

        /// <summary>
        /// Register the full execution of the Photo Capture. If successfull, it will begin the Image Analysis process.
        /// </summary>
        void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
        {
            photoCaptureObject.Dispose();
            photoCaptureObject = null;

            // Request image caputer analysis
            StartCoroutine(FaceAnalysis.Instance.DetectFacesFromImage());
        }
    ```

9. N’oubliez pas de **enregistrer** les modifications avant de revenir à l’éditeur Unity.

## <a name="chapter-8---building-the-solution"></a>Chapitre 8 - Création d’une solution

Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre HoloLens.

Avant de procéder, assurez-vous que :

-   Tous les paramètres mentionnés dans le chapitre 3 sont correctement définies. 
-   Le script *FaceAnalysis* est attaché à l’objet Main Camera. 
-   Les deux le **Auth Key** et **Id de groupe** ont été définies dans le *FaceAnalysis* script.

Ce point que vous êtes prêt à générer la Solution. Une fois que la Solution a été créée, vous serez prêt à déployer votre application.

Pour commencer le processus de génération :

1.  En cliquant sur fichier, enregistrer, enregistrer la scène actuelle.
2.  Accédez à fichier, les paramètres de Build, cliquez sur Ajouter un arrière-plan ouverte.
3.  Veillez à l’autre Unity C# projets.

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-24.png)

4.  Appuyez sur Build. Lors de cette façon, Unity lancera une fenêtre d’Explorateur de fichiers, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans. À présent, de créer ce dossier au sein du projet Unity et l’appeler application. Le dossier d’application sélectionné, appuyez sur Sélectionner un dossier. 
5.  Unity commence la création de votre projet, dans le dossier d’application. 
6.  Une fois Unity a terminé la génération (il peut prendre un certain temps), il ouvre une fenêtre d’Explorateur de fichiers à l’emplacement de votre build.

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-25.png)

7.  Ouvrez le dossier d’application et ouvrez la nouvelle Solution de projet (comme indiqué ci-dessus, MR_FaceRecognition.sln).


## <a name="chapter-9---deploying-your-application"></a>Chapitre 9 - déploiement de votre application

Pour déployer sur HoloLens :

1.  Vous devez l’adresse IP de votre HoloLens (pour les déployer à distance) et pour vérifier que votre HoloLens est dans **Mode développeur**. Pour ce faire :

    1. Tout en portant vos HoloLens, ouvrez le **paramètres**.
    2. Accédez à **réseau & Internet > Wi-Fi > Options avancées**
    3. Remarque la **IPv4** adresse.
    4. Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité > pour les développeurs** 
    5. Définir le Mode développeur.

2.  Accédez à votre nouvelle build Unity (le *application* dossier) et ouvrez le fichier solution avec *Visual Studio*.
3.  Dans, sélectionnez la Configuration de Solution **déboguer**.
4.  Dans la plateforme de Solution, sélectionnez **x86**, **Machine distante**. 

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab4-26.png)
 
5.  Accédez à la **menu Générer** , puis cliquez sur **déployer la Solution**, chargement de version test l’application à votre HoloLens.
6.  Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !

> [!NOTE]
> Pour déployer sur casque immersif, définissez le **plateforme de Solution** à *ordinateur Local*et définissez le **Configuration** à *déboguer*, avec *x86* en tant que le **plateforme**. Déployer sur l’ordinateur local d’ordinateur, à l’aide de la **menu Générer**, en sélectionnant *déployer la Solution*. 


## <a name="chapter-10---using-the-application"></a>Chapitre 10 - à l’aide de l’application

1.  Porter le HoloLens, lancez l’application.
2.  Examinez la personne que vous avez enregistrée avec le *API visage*. Vérifiez que :

    -  Visage de la personne n’est pas trop éloignées et clairement visibles
    -  L’éclairage d’environnement n’est pas trop sombre

3.  Utilisez l’action d’appuyer pour capturer l’image de la personne.
4.  Attendez que l’application envoyer la demande d’analyse et de recevoir une réponse.
5.  Si la personne qui a été reconnue, le nom de personne s’affiche sous forme de texte de l’interface utilisateur.
6.  Vous pouvez répéter le processus de capture à l’aide de l’action d’appuyer après quelques secondes.

## <a name="your-finished-azure-face-api-application"></a>Votre Application d’API de visage Azure terminée

Félicitations, vous avez créé une application de réalité mixte qui tire parti du service de reconnaissance faciale de Azure pour détecter les visages dans une image et identifier des visages connus.

![résultat de cette formation](images/AzureLabs-Lab4-00.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Le **API visage de Azure** est suffisamment puissant pour détecter jusqu'à 64 visages dans une seule image. Étendre l’application, afin qu’il peut reconnaître les visages de deux ou trois parmi de nombreuses autres personnes.

### <a name="exercise-2"></a>Exercice 2

Le **API visage de Azure** est également en mesure de fournir de nouveau toutes sortes d’informations sur les attributs. Intégrer cela dans l’application. Cela pourrait être encore plus intéressant, lorsqu’elles sont combinées avec le [API émotion](https://azure.microsoft.com/en-au/services/cognitive-services/emotion/).
