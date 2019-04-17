---
title: MR et Azure 301 - traduction linguistique
description: Terminer ce cours pour apprendre à implémenter l’API Azure Translator Text dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, de texte translator text, hololens, immersives, vr
ms.openlocfilehash: 6fe31d1bcb72337f0a3e8664893ea0f7c0540aae
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596316"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-and-azure-301-language-translation"></a>MR et Azure 301 : Traduction linguistique

Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de traduction à une application de réalité mixte à l’aide d’Azure Cognitive Services, avec l’API Translator Text.

![Produit final](images/AzureLabs-Lab1-00.png)

L’API Translator Text est une Service qui fonctionne dans quasiment en temps réel de la traduction. Le Service est basé sur le cloud, et, à l’aide d’un appel d’API REST, une application peut effectuer permet de traduire du texte dans un autre langage de la technologie de traduction automatique NEURONALE. Pour plus d’informations, visitez le [page de l’API Translator Text Azure](https://azure.microsoft.com/services/cognitive-services/translator-text-api/).

À la fin de ce cours, vous disposez d’une application de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :

1.  L’utilisateur qui s’exprime en un microphone connecté à un casque (VR) immersif (ou le microphone intégré de HoloLens).
2.  L’application capture la dictée et l’envoyer à l’API Azure Translator Text.
3.  Le résultat de la traduction s’affichera dans un groupe de l’interface utilisateur simple dans la scène Unity.

Ce cours va vous apprendre à obtenir les résultats à partir du Service de traduction dans une application basée sur Unity. Il le sera jusqu'à vous permettent d’appliquer ces concepts à une application personnalisée, que vous voudrez peut-être générer.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 301 : Traduction linguistique</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens. Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens. Lorsque vous utilisez HoloLens, vous pouvez remarquer quelques echo durant la capture de la voix.

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .

Nous recommandons le matériel et logiciel pour ce cours suivants :

- Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)
- [Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé](install-the-tools.md#installation-checklist)
- [Le SDK Windows 10 dernières](install-the-tools.md#installation-checklist)
- [Unity 2017.4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé
- Un ensemble de casque avec un microphone intégré (si le casque n’a pas un mic intégré et les haut-parleurs)
- Accès à Internet pour la récupération Azure le programme d’installation et de traduction

## <a name="before-you-start"></a>Avant de commencer

- Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).
- Le code dans ce didacticiel vous permettra d’enregistrer à partir de l’appareil de microphone par défaut connecté à votre PC. Assurez-vous que l’appareil de microphone par défaut est définie sur l’appareil que vous prévoyez d’utiliser pour capturer votre voix.
- Pour permettre à votre PC activer la dictée, accédez à **Paramètres > confidentialité > vocale, la saisie manuscrite & tapant** et sélectionnez le bouton **sur Activer le services de reconnaissance vocale et les suggestions en tapant**.
- Si vous utilisez un microphone et le casque (ou intégré à) votre casque, assurez-vous que l’option « Lorsque je wear mon casque, basculez vers casque mic » est activée dans **Paramètres > une réalité mixte > Audio et reconnaissance vocale**.

   ![Paramètres de la réalité mixte](images/AzureLabs-Lab1-00-5.png)

   ![Paramètre du microphone](images/AzureLabs-Lab1-01.png)

> [!WARNING]
> N’oubliez pas que si vous développez pour un casque immersif pour ce laboratoire, vous pouvez rencontrer des problèmes de périphérique de sortie audio. Il s’agit d’un problème avec Unity, ce qui a été résolu dans les versions ultérieures de Unity (Unity 2018.2). Le problème empêche la modification le périphérique de sortie audio par défaut au moment de l’exécution d’Unity. Pour contourner ce problème, assurez-vous de qu'avoir effectué les étapes ci-dessus et fermez et rouvrez l’éditeur, lorsque ce problème se présente.

## <a name="chapter-1--the-azure-portal"></a>Chapitre 1 – le portail Azure

Pour utiliser l’API de Translator Azure, vous devrez configurer une instance du Service à être mis à disposition de votre application.

1.  Connectez-vous à la [Azure Portal](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche supérieur et recherchez « API Translator Text. » Sélectionnez **entrez**.

    ![Nouvelle ressource](images/AzureLabs-Lab1-02.png)

    > [!NOTE]
    > Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.

3.  La nouvelle page doit fournir une description de la *API Translator Text* Service. En bas à gauche de cette page, sélectionnez le **créer** bouton, pour créer une association avec ce Service.

    ![Créer le Service d’API Translator Text](images/AzureLabs-Lab1-03.png)

4.  Une fois que vous avez cliqué sur **créer**:

    1. Insérez votre souhaitée **nom** pour cette instance de Service.
    2. Sélectionnez un **abonnement**.
    3. Sélectionnez le **niveau tarifaire** appropriés pour vous, s’il s’agit du premier temps à créer un *Service de texte Translator*, un niveau gratuit (nommé F0) doit être disponible pour vous.
    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions.
    6. Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.
    7. Sélectionnez **Créer**.

        ![Sélectionnez le bouton Créer.](images/AzureLabs-Lab1-04.png)

5.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.
6.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail. 

    ![Notification de la création du Service Azure](images/AzureLabs-Lab1-05.png)

7.  Cliquez sur la notification pour Explorer votre nouvelle instance de Service. 

    ![Accédez au menu contextuel de ressources.](images/AzureLabs-Lab1-06.png)

8.  Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. Vous êtes redirigé vers votre nouvelle instance de Service d’API Translator Text. 

    ![Page du Service d’API de texte Translator](images/AzureLabs-Lab1-07.png)

9.  Dans ce didacticiel, votre application devra effectuer des appels à votre Service, par l’intermédiaire à l’aide de la clé d’abonnement de votre Service. 
10. À partir de la *Guide de démarrage rapide* page de votre *Translator Text* Service, accédez à la première étape, *récupérez vos clés*, puis cliquez sur **clés** (vous pouvez également y parvenir en cliquant sur le lien hypertexte bleu clés, situé dans le menu de navigation de Services, indiqué par l’icône de clé). Cela permet de révéler votre Service *clés*.
11. Effectuez une copie de l’une des clés affichées, car vous en aurez besoin plus loin dans votre projet. 

## <a name="chapter-2--set-up-the-unity-project"></a>Chapitre 2 : configurer le projet Unity

Configurer et tester votre casque immersives de réalité mixte.

> [!NOTE]
> Vous n'aurez pas besoin des contrôleurs de mouvement pour ce cours. Si vous avez besoin de prendre en charge de la configuration d’un casque immersive, veuillez [suivez ces étapes](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et, par conséquent, est un bon modèle pour d’autres projets :

1.  Ouvrez *Unity* et cliquez sur **New**. 

    ![Démarrer un nouveau projet Unity.](images/AzureLabs-Lab1-08.png)

2.  Maintenant, vous devez fournir un nom de projet Unity. Insérer **MR_Translation**. Assurez-vous que le type de projet est défini sur **3D**. Définir le *emplacement* à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![Fournissent des détails pour un projet Unity.](images/AzureLabs-Lab1-09.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **Modifier > Préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![Mettre à jour les préférences de l’éditeur de script.](images/AzureLabs-Lab1-10.png)

4.  Ensuite, accédez à **fichier > Paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **plateforme basculer** bouton.

    ![Fenêtre Paramètres, plateforme de commutation à UWP de la génération.](images/AzureLabs-Lab1-11.png)

5.  Accédez à **fichier > Paramètres de Build** et vous assurer que :

    1. **Équipement cible** a la valeur **n’importe quel appareil**.

        > Pour Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.

    2. **Type de build** a la valeur **D3D**
    3. **Kit de développement logiciel** a la valeur **dernière installé**
    4. **Version de Visual Studio** a la valeur **dernière installé**
    5. **Générez et exécutez** est défini sur **ordinateur Local**
    6. Enregistrer la scène et l’ajouter à la build.

        1. Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.

            ![Cliquez sur Ajouter un bouton scènes ouvert](images/AzureLabs-Lab1-12.png)

        2. Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![Créer un nouveau dossier de scripts](images/AzureLabs-Lab1-13.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **MR_TranslationScene**, puis appuyez sur **enregistrer**.

            ![Donnez un nom à nouvelle scène.](images/AzureLabs-Lab1-14.png)

            > N’oubliez pas, vous devez enregistrer vos séquences de Unity dans le *actifs* dossier, car ils doivent être associées au projet Unity. Création du dossier de scènes (et autres dossiers similaire) est un moyen classique de structurer un projet Unity.

    7. Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.

6. Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve. 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab1-15.png)

7. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1. Dans le **autres paramètres** onglet :

        1. **Version du Runtime de script** doit être **Stable** (équivalent .NET 3.5).
        2. **Script principal** doit être **.NET**
        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**

            ![Mettre à jour les autres paramètres.](images/AzureLabs-Lab1-16.png)
      
    2. Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        1. **InternetClient**
        2. **Microphone**

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab1-17.png)

    3. Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.

        ![Mettre à jour les paramètres de R X.](images/AzureLabs-Lab1-18.png)

8.  Dans **paramètres de Build**, *Unity C# projets* est n’est plus grisée ; Cochez la case à cocher en regard de cela. 
9.  Fermez la fenêtre Paramètres de Build.
10. Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).

## <a name="chapter-3--main-camera-setup"></a>Chapitre 3 – le programme d’installation de la caméra principale

> [!IMPORTANT]
> Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20301%20-%20Language%20translation/Azure-MR-301.unitypackage), importez-le dans votre projet en tant qu’un [ *Package personnalisé*](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 5](#chapter-5--create-the-results-class). Vous devez toujours créer un projet Unity.

1.  Dans le *hiérarchie panneau*, vous trouverez un objet appelé **Main Camera**, cet objet représente votre point de vue du « head » une fois que vous êtes « à l’intérieur » de votre application.
2.  Avec le tableau de bord Unity devant vous, sélectionnez le **GameObject de caméra principale**. Vous remarquerez que le *panneau Inspecteur* (généralement situé vers la droite, dans le tableau de bord) affiche les différents composants de qui *GameObject*, avec *transformer* en haut, suivie de *caméra*et certains autres composants. Vous devez réinitialiser la transformation de la caméra principale, donc il est positionné correctement.
3.  Pour ce faire, sélectionnez le **ENGRENAGE** icône en regard de la caméra *transformer* composant, puis en sélectionnant **réinitialiser**. 

    ![Réinitialiser la transformation Main Camera.](images/AzureLabs-Lab1-19.png)
 
4.  Le *transformer* composant doit alors ressembler :

    1. Le *Position* a la valeur **0, 0, 0**
    2. *Rotation* a la valeur **0, 0, 0**
    3. Et *mise à l’échelle* a la valeur **1, 1, 1**

        ![Transformer les informations pour l’appareil photo](images/AzureLabs-Lab1-20.png)

5.  Ensuite, avec le **Main Camera** de l’objet sélectionné, consultez le **ajouter un composant** bouton situé tout en bas de la *panneau Inspecteur*. 
6.  Sélectionnez ce bouton, puis rechercher (soit en saisissant *Audio Source* dans le champ de recherche ou de la navigation dans les sections) pour le composant appelé **Audio Source** comme indiqué ci-dessous et sélectionnez-le (appuyez sur entrée sur ce dernier fonctionne également).
7.  Un *Audio Source* composant sera ajouté à la **Main Camera**, comme illustré ci-dessous.

    ![Ajoutez un composant de Source de données Audio.](images/AzureLabs-Lab1-21.png)

    > [!NOTE]
    > Pour Microsoft HoloLens, vous devez également modifier les paramètres suivants, qui font partie de la **caméra** composant sur votre **Main Camera**:
    > - **Effacer les indicateurs :** Couleur unie.
    > - **Arrière-plan** ' noir, Alpha 0' – couleur hexadécimale : #00000000.

## <a name="chapter-4--setup-debug-canvas"></a>Chapitre 4 – le programme d’installation débogage canevas

Pour afficher l’entrée et la sortie de la traduction, une interface utilisateur de base doit être créé. Pour ce cours, vous allez créer un objet de l’interface utilisateur de la zone de dessin, avec plusieurs objets 'Text' pour afficher les données.

1.  Avec le bouton droit dans une zone vide de la *hiérarchie panneau*, sous **l’interface utilisateur**, ajouter un **canevas**.

    ![Ajouter un nouvel objet de l’interface utilisateur de la zone de dessin.](images/AzureLabs-Lab1-22.png)

2.  Avec l’objet de zone de dessin sélectionné, dans le *panneau Inspecteur* (dans le composant « Canevas »), modifiez **Mode de rendu** à **espace universel**. 
3.  Ensuite, modifiez les paramètres suivants dans le *Rect transformation du panneau Inspecteur*:

    1. *POS* -  **X** 0 **Y** 0 **Z** 40
    2. *Largeur* - 500
    3. *Hauteur* - 300
    4. *Mise à l’échelle* - **X** 0.13 **Y** 0.13 **Z** 0,13

        ![Mettre à jour de la transformation de rect pour la zone de dessin.](images/AzureLabs-Lab1-23.png)
 
4.  Cliquez avec le bouton droit sur le **canevas** dans le *hiérarchie panneau*, sous **l’interface utilisateur**et ajoutez un **panneau**. Cela **panneau** fournira un arrière-plan au texte que vous devez afficher dans la scène.
5.  Cliquez avec le bouton droit sur le **panneau** dans le *hiérarchie panneau*, sous **l’interface utilisateur**et ajoutez un **textuel**. Répétez ce processus jusqu'à ce que vous avez créé quatre objets de textes d’interface utilisateur au total (Conseil : Si vous avez le premier objet de 'Text' sélectionné, vous pouvez simplement appuyer sur **« Ctrl » + avait '**, dupliquer, jusqu'à ce que vous ayez quatre au total). 
6.  Pour chaque **textuel**, sélectionnez-le, puis utilisez le ci-dessous tables pour définir les paramètres le *panneau Inspecteur*.

    1. Pour le *Rect transformation* composant :

        | Nom                   | Transformer - *Position*             | Largeur      | Hauteur    |
        |:----------------------:|:----------------------------------:|:----------:|:---------:|
        | MicrophoneStatusLabel  | **X** -80 **Y** 90 **Z** 0         | 300        | 30        |
        | AzureResponseLabel     | **X** -80 **Y** 30 **Z** 0         | 300        | 30        |
        | DictationLabel         | **X** -80 **Y** -30 **Z** 0        | 300        | 30        |
        | TranslationResultLabel | **X** -80 **Y** -90 **Z** 0        | 300        | 30        |


    2. Pour le **texte (Script)** composant :


        | Nom                   | Text               | Taille de police    |
        |:----------------------:|:------------------:|:------------:|
        | MicrophoneStatusLabel  | État du microphone : | 20           |
        | AzureResponseLabel     | Réponse Web Azure | 20           |
        | DictationLabel         |   Vous l’avez dit simplement :   | 20           |
        | TranslationResultLabel |    Traduction :    | 20           |

        ![Entrez les valeurs correspondantes pour les étiquettes de l’interface utilisateur.](images/AzureLabs-Lab1-24.png)

    3. En outre, que le Style de police **gras**. Cela facilite le texte à lire.

        ![Police en gras.](images/AzureLabs-Lab1-25.png)

7.  Pour chaque *textuel de l’interface utilisateur* créé dans [chapitre 5](#chapter-5--create-the-results-class), créez un *enfant* **textuel de l’interface utilisateur**. Ces enfants affiche la sortie de l’application. Créer *enfant* objets par clic droit sur votre parent souhaité (par exemple, *MicrophoneStatusLabel*), puis sélectionnez **l’interface utilisateur** , puis sélectionnez **texte**.
8.  Pour chacun de ces enfants, sélectionnez-le et utilisez les tableaux pour définir les paramètres dans le panneau d’inspecteur suivants.

    1. Pour le **Rect transformation** composant :

        | Nom                  | Transformer - *Position* | Largeur      | Hauteur    |
        |:---------------------:|:----------------------:|:----------:|:---------:|
        | MicrophoneStatusText  | X 0 Y -30 Z 0          | 300        | 30        |
        | AzureResponseText     | X 0 Y -30 Z 0          | 300        | 30        |
        | DictationText         | X 0 Y -30 Z 0          | 300        | 30        |
        | TranslationResultText | X 0 Y -30 Z 0          | 300        | 30        |

    2. Pour le **texte (Script)** composant :

        | Nom                  | Text          | Taille de police    |
        |:---------------------:|:-------------:|:------------:|
        | MicrophoneStatusText  |      ??       | 20           |
        | AzureResponseText     |      ??       | 20           |
        | DictationText         |      ??       | 20           |
        | TranslationResultText |      ??       | 20           |

9. Ensuite, sélectionnez l’option d’alignement « centre » pour chaque composant de texte :

    ![Aligner le texte.](images/AzureLabs-Lab1-26.png)

10. Pour garantir la **enfant textes d’interface utilisateur** objets sont facilement lisibles, modifier leur *couleur*. Cela en cliquant sur la barre (actuellement « noir ») en regard *couleur*. 

    ![D’entrée correspondant des valeurs pour les sorties de texte de l’interface utilisateur.](images/AzureLabs-Lab1-27.png)
 
11. Ensuite, dans le nouveau, peu, *couleur* fenêtre, de modifier le *couleur hexadécimale* à : **0032EAFF**

    ![Mettre à jour de la couleur bleue.](images/AzureLabs-Lab1-28.png)
 
12. Voici comment la **l’interface utilisateur** doit se présenter.
    1.  Dans le *hiérarchie panneau*:

        ![Avoir hiérarchie dans la structure fournie.](images/AzureLabs-Lab1-29.png)

    2.  Dans le *scène* et *jeux vues*:

        ![Avoir les vues de la scène et le jeu dans la même structure.](images/AzureLabs-Lab1-30.png)

## <a name="chapter-5--create-the-results-class"></a>Chapitre 5 : créer la classe de résultats

Est le premier script que vous avez besoin pour créer le *résultats* (classe), qui est chargé de fournir un moyen pour afficher les résultats de la traduction. La classe stocke et affiche les informations suivantes : 

- Le résultat de la réponse à partir d’Azure.
- L’état du microphone. 
- Le résultat de la dictée (voix en texte).
- Le résultat de la traduction.

Pour créer cette classe : 

1.  Avec le bouton droit dans le *Panneau de configuration de projet*, puis **créer > dossier**. Nommez le dossier **Scripts**. 
 
    ![Créez le dossier scripts.](images/AzureLabs-Lab1-31.png)

    ![Ouvrez le dossier scripts.](images/AzureLabs-Lab1-32.png)
 
2.  Avec le **Scripts** créer de dossier, double-cliquez dessus pour l’ouvrir. Ensuite, dans ce dossier, avec le bouton droit, puis sélectionnez **créer >** puis  **C# Script**. Nommez le script *résultats*. 

    ![Créer le premier script.](images/AzureLabs-Lab1-33.png)
 
3.  Double-cliquez sur le nouveau *résultats* script pour l’ouvrir avec **Visual Studio**.
4.  Insérer des espaces de noms suivants :

    ```cs
        using UnityEngine;
        using UnityEngine.UI;
    ```

5.  À l’intérieur de la classe, insérez les variables suivantes :

    ```cs
        public static Results instance;
   
        [HideInInspector] 
        public string azureResponseCode;
   
        [HideInInspector] 
        public string translationResult;
   
        [HideInInspector] 
        public string dictationResult;
   
        [HideInInspector] 
        public string micStatus;
   
        public Text microphoneStatusText;
   
        public Text azureResponseText;
   
        public Text dictationText;
   
        public Text translationResultText;
    ```

6.  Ajoutez ensuite le *Awake()* (méthode), qui sera appelée lors de l’initialisation de la classe. 

    ```csharp
        private void Awake() 
        { 
            // Set this class to behave similar to singleton 
            instance = this;           
        } 
    ```

7.  Enfin, ajoutez les méthodes qui sont responsables de sortir les informations des résultats différents à l’interface utilisateur. 

    ```csharp
        /// <summary>
        /// Stores the Azure response value in the static instance of Result class.
        /// </summary>
        public void SetAzureResponse(string result)
        {
            azureResponseCode = result;
            azureResponseText.text = azureResponseCode;
        }
   
        /// <summary>
        /// Stores the translated result from dictation in the static instance of Result class. 
        /// </summary>
        public void SetDictationResult(string result)
        {
            dictationResult = result;
            dictationText.text = dictationResult;
        }
   
        /// <summary>
        /// Stores the translated result from Azure Service in the static instance of Result class. 
        /// </summary>
        public void SetTranslatedResult(string result)
        {
            translationResult = result;
            translationResultText.text = translationResult;
        }
   
        /// <summary>
        /// Stores the status of the Microphone in the static instance of Result class. 
        /// </summary>
        public void SetMicrophoneStatus(string result)
        {
            micStatus = result;
            microphoneStatusText.text = micStatus;
        }
    ```

8.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-6--create-the-microphonemanager-class"></a>Chapitre 6 : créer le *MicrophoneManager* classe

La deuxième classe que vous vous apprêtez à créer est le *MicrophoneManager*.

Cette classe est chargée de :

- Détection du périphérique d’enregistrement attaché à l’ordinateur (selon celui qui est la valeur par défaut) ou un casque.
- Capturer l’audio (voix) et la dictée pour stocker en tant que chaîne.
- Une fois que la voix a été suspendu, soumettez la dictée pour la classe de convertisseur.
- Héberger une méthode qui peut arrêter la capture vocale si vous le souhaitez.

Pour créer cette classe : 
1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir. 
2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**. Nommez le script *MicrophoneManager*. 
3.  Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.
4.  Mettre à jour les espaces de noms pour être le même que la commande suivante, en haut de la *MicrophoneManager* classe :

    ```csharp
        using UnityEngine; 
        using UnityEngine.Windows.Speech;
    ```

5.  Ensuite, ajoutez les variables suivantes à l’intérieur de la *MicrophoneManager* classe :

    ```csharp
        // Help to access instance of this object 
        public static MicrophoneManager instance; 
     
        // AudioSource component, provides access to mic 
        private AudioSource audioSource; 
   
        // Flag indicating mic detection 
        private bool microphoneDetected; 
   
        // Component converting speech to text 
        private DictationRecognizer dictationRecognizer; 
    ```

6.  Code pour le *Awake()* et *Start()* méthodes doit maintenant être ajouté. Il seront appelées lors de l’initialisation de la classe :

    ```csharp
        private void Awake() 
        { 
            // Set this class to behave similar to singleton 
            instance = this; 
        } 
    
        void Start() 
        { 
            //Use Unity Microphone class to detect devices and setup AudioSource 
            if(Microphone.devices.Length > 0) 
            { 
                Results.instance.SetMicrophoneStatus("Initialising..."); 
                audioSource = GetComponent<AudioSource>(); 
                microphoneDetected = true; 
            } 
            else 
            { 
                Results.instance.SetMicrophoneStatus("No Microphone detected"); 
            } 
        } 
    ```

7.  Vous pouvez *supprimer* le *Update()* étant donné que cette classe ne l’utilise pas de méthode.
8.  Maintenant, vous devez les méthodes que l’application utilise pour démarrer et arrêter la capture de la voix et transmettez-le à la *Translator* (classe), que vous allez générer plus rapidement. Copiez le code suivant et collez-le sous la *Start()* (méthode).

    ```csharp
        /// <summary> 
        /// Start microphone capture. Debugging message is delivered to the Results class. 
        /// </summary> 
        public void StartCapturingAudio() 
        { 
            if(microphoneDetected) 
            {               
                // Start dictation 
                dictationRecognizer = new DictationRecognizer(); 
                dictationRecognizer.DictationResult += DictationRecognizer_DictationResult; 
                dictationRecognizer.Start(); 
    
                // Update UI with mic status 
                Results.instance.SetMicrophoneStatus("Capturing..."); 
            }      
        } 
 
        /// <summary> 
        /// Stop microphone capture. Debugging message is delivered to the Results class. 
        /// </summary> 
        public void StopCapturingAudio() 
        { 
            Results.instance.SetMicrophoneStatus("Mic sleeping"); 
            Microphone.End(null); 
            dictationRecognizer.DictationResult -= DictationRecognizer_DictationResult; 
            dictationRecognizer.Dispose(); 
        }
    ```

    > [!TIP]
    > Bien que cette application ne fera pas l’utiliser, le *StopCapturingAudio()* méthode a également été fournie ici, si vous souhaitez implémenter la possibilité d’arrêter la capture audio dans votre application.

9.  Vous devez maintenant ajouter un gestionnaire de dictée qui sera appelé lorsque la voix s’arrête. Cette méthode passe ensuite le texte dicté à la *Translator* classe.

    ```csharp
        /// <summary>
        /// This handler is called every time the Dictation detects a pause in the speech. 
        /// Debugging message is delivered to the Results class.
        /// </summary>
        private void DictationRecognizer_DictationResult(string text, ConfidenceLevel confidence)
        {
            // Update UI with dictation captured
            Results.instance.SetDictationResult(text);
   
            // Start the coroutine that process the dictation through Azure 
            StartCoroutine(Translator.instance.TranslateWithUnityNetworking(text));   
        }
    ```

10. Veillez à enregistrer vos modifications dans Visual Studio avant de retourner à Unity.

> [!WARNING]  
> À ce stade, vous remarquerez une erreur qui apparaissent dans le *Console de l’éditeur Unity* panneau (« le nom « Translator » n’existe pas... »). Il s’agit, car le code fait référence le *Translator* (classe), que vous allez créer dans le chapitre suivant.

## <a name="chapter-7--call-to-azure-and-translator-service"></a>Chapitre 7 – appel au service Azure et translator

Est le dernier script, vous devez créer le *Translator* classe. 

Cette classe est chargée de :

-   L’authentification de l’application avec *Azure*, exchange pour un **du jeton d’authentification**.
-   Utilisez le **du jeton d’authentification** pour envoyer du texte (reçus à partir de la *MicrophoneManager* classe) à traduire.
-   Recevoir le résultat traduit et transmettez-le à la *résultats* classe à visualiser dans l’interface utilisateur.

Pour créer cette classe : 
1.  Accédez à la **Scripts** dossier que vous avez créé précédemment. 
2.  Avec le bouton droit dans le **Panneau de configuration de projet**, **créer > C# Script**. Appeler le script *Translator*.
3.  Double-cliquez sur le nouveau *Translator* script pour l’ouvrir **avec Visual Studio**.
4.  Ajoutez les espaces de noms suivantes au début du fichier :

    ```csharp
        using System;
        using System.Collections;
        using System.Xml.Linq;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  Puis ajoutez les variables suivantes à l’intérieur de la *Translator* classe :

    ```csharp
        public static Translator instance; 
        private string translationTokenEndpoint = "https://api.cognitive.microsoft.com/sts/v1.0/issueToken"; 
        private string translationTextEndpoint = "https://api.microsofttranslator.com/v2/http.svc/Translate?"; 
        private const string ocpApimSubscriptionKeyHeader = "Ocp-Apim-Subscription-Key"; 
    
        //Substitute the value of authorizationKey with your own Key 
        private const string authorizationKey = "-InsertYourAuthKeyHere-"; 
        private string authorizationToken; 
    
        // languages set below are: 
        // English 
        // French 
        // Italian 
        // Japanese 
        // Korean 
        public enum Languages { en, fr, it, ja, ko }; 
        public Languages from = Languages.en; 
        public Languages to = Languages.it; 
    ```

    > [!NOTE]
    > - Les langues insérées dans les langues **enum** sont de simples exemples. Vous pouvez ajouter plus si vous le souhaitez ; le [API prend en charge plus de 60 langues](https://docs.microsoft.com/azure/cognitive-services/translator/languages) (y compris Klingon) !
    > - Est un [page plus interactive sur des langages disponibles](https://www.microsoft.com/translator/business/languages/), sachez cependant à la page s’affiche uniquement pour fonctionner lorsque la langue du site est définie sur « en-us (et le site de Microsoft sera probablement rediriger vers votre langue maternelle). Vous pouvez modifier la langue du site au bas de la page ou en modifiant l’URL.
    > - Le **authorizationKey** valeur, dans l’extrait de code ci-dessus, doit être le **clé** que vous avez reçu lors de votre abonnement à la *Azure l’API Translator Text*. Cela a été couvert dans [chapitre 1](#chapter-1--the-azure-portal).

6.  Code pour le *Awake()* et *Start()* méthodes doit maintenant être ajouté. 
7.  Dans ce cas, le code effectue un appel à *Azure* à l’aide de l’autorisation de clé, pour obtenir un *jeton*.

    ```csharp
        private void Awake() 
        { 
            // Set this class to behave similar to singleton  
            instance = this; 
        } 
    
        // Use this for initialization  
        void Start() 
        { 
            // When the application starts, request an auth token 
            StartCoroutine("GetTokenCoroutine", authorizationKey); 
        }
    ```

    > [!NOTE]
    > Le jeton expire après 10 minutes. Selon le scénario de votre application, vous devrez peut-être rendre la coroutine même appeler plusieurs fois.

8.  La coroutine pour obtenir le jeton est la suivante :

    ```csharp
        /// <summary> 
        /// Request a Token from Azure Translation Service by providing the access key. 
        /// Debugging result is delivered to the Results class. 
        /// </summary> 
        private IEnumerator GetTokenCoroutine(string key)
        {
            if (string.IsNullOrEmpty(key))
            {
                throw new InvalidOperationException("Authorization key not set.");
            }

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Post(translationTokenEndpoint, string.Empty))
            {
                unityWebRequest.SetRequestHeader("Ocp-Apim-Subscription-Key", key);
                yield return unityWebRequest.SendWebRequest();

                long responseCode = unityWebRequest.responseCode;

                // Update the UI with the response code 
                Results.instance.SetAzureResponse(responseCode.ToString());

                if (unityWebRequest.isNetworkError || unityWebRequest.isHttpError)
                {
                    Results.instance.azureResponseText.text = unityWebRequest.error;
                    yield return null;
                }
                else
                {
                    authorizationToken = unityWebRequest.downloadHandler.text;
                }
            }

            // After receiving the token, begin capturing Audio with the MicrophoneManager Class 
            MicrophoneManager.instance.StartCapturingAudio();
        }
    ```

    > [!WARNING]
    > Si vous modifiez le nom de la méthode IEnumerator **GetTokenCoroutine()**, vous devez mettre à jour le *StartCoroutine* et *StopCoroutine* appeler des valeurs de chaîne dans le code ci-dessus. [Selon la documentation Unity](https://docs.unity3d.com/ScriptReference/MonoBehaviour.StartCoroutine.html), pour arrêter un spécifique *Coroutine*, vous devez utiliser la méthode de valeur de chaîne.

9.  Ensuite, ajoutez la coroutine (avec une méthode de flux « support » juste en dessous) pour obtenir la traduction du texte reçue par le *MicrophoneManager* classe. Ce code crée une chaîne de requête à envoyer à la *Azure l’API Translator Text*, puis utilise la classe Unity UnityWebRequest interne pour effectuer un appel de 'Get' pour le point de terminaison avec la chaîne de requête. Le résultat est ensuite utilisé pour définir la traduction dans votre objet de résultats. Le code ci-dessous illustre l’implémentation :

    ```csharp
        /// <summary> 
        /// Request a translation from Azure Translation Service by providing a string.  
        /// Debugging result is delivered to the Results class. 
        /// </summary> 
        public IEnumerator TranslateWithUnityNetworking(string text)
        {
            // This query string will contain the parameters for the translation 
            string queryString = string.Concat("text=", Uri.EscapeDataString(text), "&from=", from, "&to=", to);

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Get(translationTextEndpoint + queryString))
            {
                unityWebRequest.SetRequestHeader("Authorization", "Bearer " + authorizationToken);
                unityWebRequest.SetRequestHeader("Accept", "application/xml");
                yield return unityWebRequest.SendWebRequest();

                if (unityWebRequest.isNetworkError || unityWebRequest.isHttpError)
                {
                    Debug.Log(unityWebRequest.error);
                    yield return null;
                }

                // Parse out the response text from the returned Xml
                string result = XElement.Parse(unityWebRequest.downloadHandler.text).Value;
                Results.instance.SetTranslatedResult(result);
            }
        }
    ```

10. Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-8--configure-the-unity-scene"></a>Chapitre 8 : configurer la scène Unity

1.  Précédent dans l’éditeur Unity, cliquez et faites glisser le *résultats* classe *à partir de* le **Scripts** dossier pour le **Main Camera** objet dans le  *Panneau de la hiérarchie*.
2.  Cliquez sur le **Main Camera** et examinez le *panneau Inspecteur*. Vous remarquerez que dans récemment ajouté *Script* composant, il existe quatre champs avec des valeurs vides. Voici les références de sortie pour les propriétés dans le code. 
3.  Faites glisser le texte approprié **texte** objets à partir de la *hiérarchie panneau* à ces quatre emplacements, comme indiqué dans l’image ci-dessous.

    ![Mettre à jour les références de la cible avec les valeurs spécifiées.](images/AzureLabs-Lab1-34.png)
  
4.  Ensuite, cliquez et faites glisser le *Translator* classe à partir de la **Scripts** dossier pour le **Main Camera** de l’objet dans le *Panneau de la hiérarchie*. 
5.  Ensuite, cliquez et faites glisser le *MicrophoneManager* classe à partir de la **Scripts** dossier à la **Main Camera** de l’objet dans le *Panneau de la hiérarchie*. 
6.  Enfin, cliquez sur le **Main Camera** et examinez le *panneau Inspecteur*. Vous remarquerez que dans le script que vous avez fait glisser sur, il y a deux listes déroulantes qui vous permet de définir les langues.
 
    ![Vérifiez que les langues de traduction prévue sont entrées.](images/AzureLabs-Lab1-35.png)

## <a name="chapter-9--test-in-mixed-reality"></a>Chapitre 9 – Test en réalité mixte

À ce stade, vous devez tester que la scène a été implémentée correctement.

Vérifiez que :

- Tous les paramètres mentionnés dans [chapitre 1](#chapter-1--the-azure-portal) sont correctement définies. 
- Le *résultats*, *Translator*, et *MicrophoneManager*, les scripts sont attachés à la **Main Camera** objet. 
- Vous avez placé votre *Azure l’API Translator Text* Service **clé** au sein de la **authorizationKey** variable dans le *Translator* Script.  
- Tous les champs dans le *panneau Inspecteur de caméra principal* sont affectées correctement.
- Votre microphone fonctionne lors de l’exécution de votre scène (dans le cas contraire, vérifiez que votre microphone attaché est le *par défaut* appareil et que vous avez [configuré correctement dans Windows](https://support.microsoft.com/en-au/help/4027981/windows-how-to-set-up-and-test-microphones-in-windows-10)).

Vous pouvez tester le casque immersif en appuyant sur la **lire** situé dans le *éditeur Unity*.
L’application doit fonctionner via le casque immersif attaché.

> [!WARNING]  
> Si vous voyez une erreur dans la console Unity sur le périphérique audio par défaut modification, la scène peut ne pas fonctionne comme prévu. Cela est dû au mode que microphones intégrés pour les casques qui en sont munis porte sur le portail de réalité mixte. Si vous cette erreur se produit, simplement arrêtez la scène et démarrez à nouveau et les choses peuvent fonctionner comme prévu.

## <a name="chapter-10--build-the-uwp-solution-and-sideload-on-local-machine"></a>Chapitre 10 – générer la solution UWP et le chargement de version test sur l’ordinateur local

Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.

1.  Accédez à **les paramètres de génération**: **Fichier > Paramètres de Build...**
2.  À partir de la **paramètres de Build** fenêtre, cliquez sur **Build**.

    ![Générer la scène Unity.](images/AzureLabs-Lab1-36.png)
  
3.  Si pas déjà fait, cochez **Unity C# projets**.
4.  Cliquez sur **Build**. Unity lancera un *Explorateur de fichiers* fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans. Créez ce dossier, puis nommez-le *application*. Ensuite avec le *application* dossier sélectionné, appuyez sur **sélectionner le dossier**. 
5.  Unity commencera à générer votre projet pour le *application* dossier. 
6.  Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un *Explorateur de fichiers* fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).

## <a name="chapter-11--deploy-your-application"></a>Chapitre 11 – déployer votre application

Pour déployer votre application :

1.  Accédez à votre nouvelle build Unity (le *application* dossier) et ouvrez le fichier solution avec *Visual Studio*.
2.  Dans, sélectionnez la Configuration de Solution **déboguer**.
3.  Dans la plateforme de Solution, sélectionnez **x86**, **ordinateur Local**. 

    > Pour le Microsoft HoloLens, il peut s’avérer plus facile d’affecter à ce *Machine distante*, de sorte que vous ne sont pas attachés à votre ordinateur. Cependant, vous devez également effectuer les opérations suivantes :
    > - Connaître le **adresse IP** de votre HoloLens, ce qui se trouve dans le *Paramètres > réseau & Internet > Wi-Fi > Options avancées*; IPv4 est l’adresse que vous devez utiliser. 
    > - Vérifiez *Mode développeur* est **sur**; trouvé dans *Paramètres > mise à jour & sécurité > pour les développeurs*.

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab1-37.png)
    
 
4.  Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre PC.
5.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.
6.  Une fois lancé, l’application vous invite à autoriser l’accès à l’aide du Microphone. Veillez à cliquer sur le **Oui** bouton.
7.  Vous êtes maintenant prêt à commencer à traduire !

## <a name="your-finished-translation-text-api-application"></a>Votre application API de traduction texte terminée

Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API de texte de traduction de Azure pour convertissez la parole en texte traduit.

![Produit final.](images/AzureLabs-Lab1-00.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Pouvez-vous ajouter des fonctionnalités de synthèse vocale à l’application, afin que le texte retourné est lu ?

### <a name="exercise-2"></a>Exercice 2

Permettre à l’utilisateur de modifier les langues source et la sortie (« from » et « to ») au sein de l’application elle-même, afin de l’application n’a pas besoin d’être reconstruit chaque fois que vous souhaitez modifier les langues.
