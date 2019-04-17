---
title: MR et 302 Azure - vision par ordinateur
description: Terminer ce cours pour apprendre à reconnaître le contenu visuel au sein d’une image fournie, à l’aide de la vision par ordinateur de Azure dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, vision par ordinateur, hololens, immersives, vr
ms.openlocfilehash: 9d5288904dd6cae08a995ae40a31b00fea655776
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593382"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-and-azure-302-computer-vision"></a>MR et Azure 302 : Vision par ordinateur

Dans ce cours, vous allez apprendre à reconnaître le contenu visuel au sein d’une image fournie, à l’aide des fonctionnalités de vision par ordinateur de Azure dans une application de réalité mixte.

Résultats de la reconnaissance seront affichera sous forme de balises descriptives. Vous pouvez utiliser ce service sans avoir à former un modèle d’apprentissage. Si votre implémentation requiert l’apprentissage d’un modèle d’apprentissage automatique, consultez [MR et Azure 302b](mr-azure-302b.md).

![résultat de laboratoire](images/AzureLabs-Lab2-000.png)

La vision par ordinateur de Microsoft est un ensemble d’API conçues pour offrir aux développeurs un traitement d’image et l’analyse (avec retour d’informations), à l’aide des algorithmes avancés, tout à partir du cloud. Les développeurs charger une image ou une URL de l’image et les algorithmes d’API de vision par ordinateur Microsoft analyser le contenu visuel, en fonction des entrées choisies l’utilisateur, ce qui peut retourner ensuite des informations, y compris, identifiant le type et la qualité d’une image, détecter les visages humains ( retour de leurs coordonnées) et de marquage, ou classer des images. Pour plus d’informations, visitez le [page de l’API de vision par ordinateur Azure](https://azure.microsoft.com/services/cognitive-services/computer-vision/).

Avoir terminé ce cours, vous aurez une réalité mixte application HoloLens, qui sera en mesure d’effectuer les opérations suivantes :

1.  À l’aide de l’action d’appuyer, l’appareil photo de l’HoloLens capture une image.
2.  L’image sera envoyée au Service de API vision par ordinateur de Azure. 
3.  Les objets reconnus seront afficheront dans un groupe de l’interface utilisateur simple positionné dans la scène Unity.

Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception. Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity. Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 302 : Vision par ordinateur</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Si ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques Windows Mixed Reality IMMERSIFS (VR). Étant donné que des casques IMMERSIFS (VR) ne sont pas accessibles caméras, vous devez une caméra externe connectée à votre PC. Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge des casques IMMERSIFS (VR).

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
- Un appareil photo connecté à votre PC (pour le développement de casque immersives)
- Accès à Internet pour le programme d’installation Azure et l’extraction de l’API vision par ordinateur

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).
2.  Configurer et tester votre HoloLens. Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup). 
3.  Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur). 

Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).

## <a name="chapter-1--the-azure-portal"></a>Chapitre 1 – le portail Azure

Pour utiliser le *API vision par ordinateur* service dans Azure, vous devez configurer une instance du service à être mis à disposition de votre application.

1.  Tout d’abord, connectez-vous à la [Azure Portal](https://portal.azure.com). 

    > [!NOTE]
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *API vision par ordinateur*, puis cliquez sur **entrée**.

    ![Créer une nouvelle ressource dans Azure](images/AzureLabs-Lab2-00.png)

    > [!NOTE]
    > Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.
 
3.  La nouvelle page doit fournir une description de la *API vision par ordinateur* service. En bas à gauche de cette page, sélectionnez le **créer** bouton permettant de créer une association avec ce service.

    ![Sur le service d’api de vision par ordinateur](images/AzureLabs-Lab2-01.png)
 
4.  Une fois que vous avez cliqué sur **créer**:

    1. Insérez votre souhaitée **nom** pour cette instance de service.
    2. Sélectionnez un **abonnement**.
    3. Sélectionnez le **niveau tarifaire** appropriés pour vous, s’il s’agit du premier temps à créer un *API vision par ordinateur* Service, un niveau gratuit (nommé F0) doit être disponible pour vous.
    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs). 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. Déterminer l’emplacement de votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions.

    6. Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.
    7. Cliquez sur Créer.

        ![Informations sur la création de service](images/AzureLabs-Lab2-02.png)

5.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.
6.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![Consultez la notification de nouveau pour votre nouveau service](images/AzureLabs-Lab2-03.png) 
 
7.  Cliquez sur la notification pour Explorer votre nouvelle instance de Service. 

    ![Sélectionnez le bouton d’accéder à la ressource.](images/AzureLabs-Lab2-04.png)
 
8. Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. Vous êtes redirigé vers votre nouvelle instance de service API vision par ordinateur. 

    ![Votre nouveau service de l’API vision par ordinateur](images/AzureLabs-Lab2-05.png)
 
9.  Dans ce didacticiel, votre application devra effectuer des appels à votre service, par l’intermédiaire à l’aide de la clé d’abonnement de votre service.
10. À partir de la *Guide de démarrage rapide* page, de votre *API vision par ordinateur* de service, accédez à la première étape, *récupérez vos clés*et cliquez sur **clés** () Vous pouvez également y parvenir en cliquant sur le lien hypertexte bleu clés, situé dans le menu de navigation de services, indiqué par l’icône de clé). Cela permet de révéler votre service *clés*.
11. Effectuez une copie de l’une des clés affichées, car vous en aurez besoin plus loin dans votre projet. 

12. Revenez à la *Guide de démarrage rapide* page et à partir de là, fetch votre point de terminaison. N’oubliez pas la vôtre peut être différent, selon votre région (qui dans le cas, vous devez apporter une modification à votre code plus tard). Effectuez une copie de ce point de terminaison pour une utilisation ultérieure :

    ![Votre nouveau service de l’API vision par ordinateur](images/AzureLabs-Lab2-05-5.png)

    > [!TIP]
    > Vous pouvez vérifier quelles sont les différents points de terminaison [ici](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa). 

## <a name="chapter-2--set-up-the-unity-project"></a>Chapitre 2 : configurer le projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **New**. 

    ![Démarrer un nouveau projet Unity.](images/AzureLabs-Lab2-06.png)

2.  Maintenant, vous devez fournir un nom de projet Unity. Insérer **MR_ComputerVision**. Assurez-vous que le type de projet est défini sur **3D**. Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![Fournissent des détails pour un projet Unity.](images/AzureLabs-Lab2-07.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **Modifier > Préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![Mettre à jour les préférences de l’éditeur de script.](images/AzureLabs-Lab2-08.png)

4.  Ensuite, accédez à **fichier > Paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation** bouton pour appliquer votre sélection.

    ![Fenêtre Paramètres, plateforme de commutation à UWP de la génération.](images/AzureLabs-Lab2-10.png)

5.  Lorsque vous êtes toujours dans **fichier > Paramètres de Build** et vous assurer que :

    1. **Équipement cible** a la valeur **HoloLens**

        > Pour des casques IMMERSIFS, définissez **appareil cible** à *n’importe quel appareil*.

    2. **Type de build** a la valeur **D3D**
    3. **Kit de développement logiciel** a la valeur **dernière installé**
    4. **Version de Visual Studio** a la valeur **dernière installé**
    5. **Générez et exécutez** est défini sur **ordinateur Local**
    6. Enregistrer la scène et l’ajouter à la build.

        1. Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.
        
            ![Cliquez sur Ajouter un bouton scènes ouvert](images/AzureLabs-Lab2-11.png)

        2. Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![Créer un nouveau dossier de scripts](images/AzureLabs-Lab2-12.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **MR_ComputerVisionScene**, puis cliquez sur **enregistrer** .

            ![Donnez un nom à nouvelle scène.](images/AzureLabs-Lab2-13.png)

            > N’oubliez pas, vous devez enregistrer vos séquences de Unity dans le *actifs* dossier, car ils doivent être associées au projet Unity. Création du dossier de scènes (et autres dossiers similaire) est un moyen classique de structurer un projet Unity.

    7. Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.

6. Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve. 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab2-14.png)

7. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1. Dans le **autres paramètres** onglet :

        1. **Version du Runtime de script** doit être **Stable** (équivalent .NET 3.5).
        2. **Script principal** doit être **.NET**
        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**

            ![Mettre à jour les autres paramètres.](images/AzureLabs-Lab2-15.png)
      
    2. Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        1. **InternetClient**
        2. **Webcam**

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab2-16.png)

    3. Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.

        ![Mettre à jour les paramètres de R X.](images/AzureLabs-Lab2-17.png)

8.  Dans *paramètres de Build* _Unity C#_  projets est n’est plus grisée ; Cochez la case à cocher en regard de cela. 
9.  Fermez la fenêtre Paramètres de Build.
10. Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).

## <a name="chapter-3--main-camera-setup"></a>Chapitre 3 – le programme d’installation de la caméra principale

> [!IMPORTANT]
> Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302%20-%20Computer%20vision/Azure-MR-302.unitypackage), importez-le dans votre projet comme un [Package personnalisé ](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 5](#chapter-5--create-the-resultslabel-class).

1.  Dans le *hiérarchie panneau*, sélectionnez le **Main Camera**. 
2.  Une fois sélectionné, vous serez en mesure de voir tous les composants de la **Main Camera** dans le *panneau Inspecteur*.

    1. Le **objet caméra** doit être nommé **Main Camera** (Notez l’orthographe !)
    2. La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe !)
    3. Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**
    4. Définissez **effacer les indicateurs** à **couleur unie** (ignorer cela pour casque immersif).
    5. Définir le **arrière-plan** couleur du composant de caméra à **noir, Alpha 0 (Hex Code : #00000000)** (ignorer cela pour casque immersif).

        ![Mettre à jour des composants de l’appareil photo.](images/AzureLabs-Lab2-18.png)
 
3.  Ensuite, vous devrez créer un objet simple « curseur » attaché à la **Main Camera**, ce qui vous aident à positionner l’analyse d’image génère lorsque l’application est en cours d’exécution. Ce curseur déterminera le point central de la vue de l’appareil photo.

Pour créer le curseur :

1.  Dans le *hiérarchie panneau*, avec le bouton droit sur le **Main Camera**. Sous **objet 3D**, cliquez sur **sphère**.

    ![Sélectionnez l’objet curseur.](images/AzureLabs-Lab2-19.png)
 
2.  Renommer le **sphère** à **curseur** (double-cliquez sur l’objet curseur ou appuyez sur le bouton de clavier « F2 » avec l’objet sélectionné) et assurez-vous qu’il se trouve en tant qu’enfant de le **Main Camera**.

3.  Dans le *hiérarchie panneau*, cliquez sur le **curseur**. Avec le curseur sélectionné, ajuster les variables suivantes dans le *panneau Inspecteur*:

    1. Définir le *transformer Position* à **0, 0, 5**
    2. Définir le *mise à l’échelle* à **0,02, 0,02, 0,02**

        ![Mettre à jour la Position de la transformation et de la mise à l’échelle.](images/AzureLabs-Lab2-20.png)
  
## <a name="chapter-4--setup-the-label-system"></a>Chapitre 4 – programme d’installation du système d’étiquette

Une fois que vous avez capturé une image avec l’appareil photo des HoloLens, cette image sera envoyée à votre *API de vision par ordinateur Azure* instance de Service pour l’analyse. 

Les résultats de cette analyse sera une liste d’objets reconnus appelé **balises**. 

Vous utiliserez des étiquettes (comme un texte 3D dans l’espace universel) pour afficher ces balises à l’emplacement de que la photo a été effectuée.

Les étapes suivantes expliquent comment configurer le **étiquette** objet.

1.  Avec le bouton droit n’importe où dans le volet de hiérarchie (l’emplacement n’a pas d’importance à ce stade), sous **objet 3D**, ajoutez un **texte 3D**. Nommez-le **LabelText**.

    ![Créer un objet de texte 3D.](images/AzureLabs-Lab2-21.png)
 
2.  Dans le *hiérarchie panneau*, cliquez sur le **LabelText**. Avec le **LabelText** sélectionnée, d’ajuster les variables suivantes dans le *panneau Inspecteur*:

    1. Définir le **Position** à **0,0,0**
    2. Définir le **mise à l’échelle** à **0,01, 0,01, 0,01**
    3. Dans le composant **texte Mesh**:
    4. Remplacez tout le texte dans **texte**, avec «... »        
    5. Définir le **ancre** à **milieu centre**
    6. Définir le **alignement** à **Center**
    7. Définir le **taille des tabulations** à **4**
    8. Définir le **la taille de police** à **50**
    9. Définir le **couleur** à **#FFFFFFFF**

    ![Composant de texte](images/AzureLabs-Lab2-21-5.png)

3.  Faites glisser le **LabelText** à partir de la *Panneau de la hiérarchie*, dans le *dossier composants*, en respectant dans le *Panneau de configuration de projet*. Cela rendra le **LabelText** un préfabriqué, afin qu’elle peut être instancié dans le code.

    ![Créer un préfabriqué de l’objet LabelText.](images/AzureLabs-Lab2-22.png)
 
4.  Vous devez supprimer le **LabelText** à partir de la *hiérarchie panneau*, afin qu’il s’affichera pas dans la scène d’ouverture. Comme il est désormais un préfabriqué, qui vous appellera pour les instances individuelles de votre dossier de ressources, il n’est pas nécessaire pour conserver dans la scène. 
5.  La structure de l’objet final dans le *hiérarchie panneau* doit être semblable à celui illustré dans l’image ci-dessous :

    ![Structure finale du Panneau de hiérarchie.](images/AzureLabs-Lab2-23.png)

## <a name="chapter-5--create-the-resultslabel-class"></a>Chapitre 5 : créer la classe ResultsLabel

Est le premier script que vous avez besoin pour créer le *ResultsLabel* (classe), qui est chargé pour les éléments suivants : 

- Créer les étiquettes dans l’espace de monde approprié, par rapport à la position de la caméra.
- Afficher les balises à partir de l’analyse de l’Image.

Pour créer cette classe : 

1.  Avec le bouton droit dans le *Panneau de configuration de projet*, puis **créer > dossier**. Nommez le dossier **Scripts**. 

    ![Créez le dossier scripts.](images/AzureLabs-Lab2-24.png)

2.  Avec le **Scripts** créer de dossier, double-cliquez dessus pour l’ouvrir. Ensuite, dans ce dossier, avec le bouton droit, puis sélectionnez **créer >** puis  **C# Script**. Nommez le script *ResultsLabel*. 

3.  Double-cliquez sur le nouveau *ResultsLabel* script pour l’ouvrir avec **Visual Studio**.

4.  À l’intérieur de la classe, insérez le code suivant dans le *ResultsLabel* classe :

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

6.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.
7.  Dans le *éditeur Unity*, cliquez et faites glisser le *ResultsLabel* classe à partir de la **Scripts** dossier pour le **Main Camera** objet dans le  *Panneau de la hiérarchie*.
8.  Cliquez sur le **Main Camera** et examinez le *panneau Inspecteur*.

Vous remarquerez qu’à partir du script que vous venez de faire glisser dans l’appareil photo, il existe deux champs : **Curseur** et **étiquette Prefab**.

9.  Faites glisser l’objet appelé **curseur** à partir de la *hiérarchie panneau* vers l’emplacement nommé **curseur**, comme illustré dans l’image ci-dessous.
10. Faites glisser l’objet appelé **LabelText** à partir de la *dossier Assets* dans le *panneau projet* vers l’emplacement nommé **Prefab étiquette**, comme illustré dans la image ci-dessous. 

    ![Définir les cibles de référence dans Unity.](images/AzureLabs-Lab2-25.png)

## <a name="chapter-6--create-the-imagecapture-class"></a>Chapitre 6 : créer la classe ImageCapture

La classe suivante, vous allez créer est la *ImageCapture* classe. Cette classe est chargée de :

-   Capture d’une Image à l’aide de l’appareil photo HoloLens et en le stockant dans le dossier d’application.
-   Mouvements de drainage de capture à partir de l’utilisateur.

Pour créer cette classe : 

1.  Accédez à la **Scripts** dossier que vous avez créé précédemment. 
2.  Avec le bouton droit dans le dossier, **créer > C# Script**. Appeler le script *ImageCapture*. 
3.  Double-cliquez sur le nouveau *ImageCapture* script pour l’ouvrir avec **Visual Studio**.
4.  Ajoutez les espaces de noms suivantes au début du fichier :

    ```csharp
        using System.IO;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;
        using UnityEngine.XR.WSA.WebCam;
    ```

5.  Puis ajoutez les variables suivantes à l’intérieur de la *ImageCapture* classe ci-dessus le *Start()* méthode :

    ```csharp
        public static ImageCapture instance; 
        public int tapsCount;
        private PhotoCapture photoCaptureObject = null;
        private GestureRecognizer recognizer;
        private bool currentlyCapturing = false;
    ```
 
Le **tapsCount** variable stocke le nombre de mouvements tap capturées à partir de l’utilisateur. Ce nombre est utilisé dans l’affectation des noms des images capturées.

6.  Code pour *Awake()* et *Start()* méthodes doit maintenant être ajouté. Il seront appelées lors de l’initialisation de la classe :

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

7.  Implémentez un gestionnaire qui sera appelé lorsqu’une action d’appuyer se produit. 

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
 
Le *TapHandler()* méthode incrémente le nombre de coefficients capturées à partir de l’utilisateur et utilise la position actuelle du curseur pour déterminer où positionner une nouvelle étiquette.

Cette méthode appelle ensuite la *ExecuteImageCaptureAndAnalysis()* méthode pour commencer à la fonctionnalité principale de cette application.

8.  Une fois qu’une Image a été capturée et stockée, les gestionnaires suivants seront appelées. Si le processus réussit, le résultat est passé à la *VisionManager* (ce qui vous êtes encore à créer) pour l’analyse.

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
 
9.  Ajoutez ensuite la méthode que l’application utilise pour démarrer le processus de capture d’Image et de stocker l’image.

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
> À ce stade, vous remarquerez une erreur qui apparaissent dans le *volet de Console Unity Editor*. Il s’agit, car le code fait référence le *VisionManager* classe que vous allez créer dans le chapitre suivant.

## <a name="chapter-7--call-to-azure-and-image-analysis"></a>Chapitre 7 – appel à Azure et d’analyse d’Image

Est le dernier script, vous devez créer le *VisionManager* classe. 

Cette classe est chargée de :

-   Chargement de la dernière image capturée sous la forme d’un tableau d’octets.
-   Envoi de tableau d’octets à votre *API de vision par ordinateur Azure* instance de Service pour l’analyse.
-   Recevoir une réponse sous forme de chaîne JSON.
-   La désérialisation de la réponse et en passant les balises qui en résulte à la *ResultsLabel* classe.
 
Pour créer cette classe :

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir. 
2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**. Nommez le script *VisionManager*. 
3.  Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.
4.  Mettre à jour les espaces de noms pour être le même que la commande suivante, en haut de la *VisionManager* classe :

    ```csharp
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using UnityEngine;
        using UnityEngine.Networking;
    ```
 
5.  En haut de votre script, *à l’intérieur de* le *VisionManager* classe (au-dessus de la *Start()* méthode), vous devez maintenant créer deux *Classes* qui représente la réponse JSON désérialisée à partir d’Azure :

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
    > Le *TagData* et *AnalysedObject* classes ont besoin d’avoir le *[System.Serializable]* attribut ajouté avant la déclaration pour pouvoir être désérialisé avec la Unity bibliothèques.

6.  Dans la classe VisionManager, vous devez ajouter les variables suivantes :

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
    > Assurez-vous que vous insérez votre **Auth Key** dans le **authorizationKey** variable. Avoir noté votre **Auth Key** au début de ce cours, [chapitre 1](#chapter-1--the-azure-portal).

    > [!WARNING] 
    > Le **visionAnalysisEndpoint** variable peut-être différer de celle spécifiée dans cet exemple. Le **west-us** strictement fait référence à des instances de Service créés pour la région ouest des États-Unis. Mettre à jour avec votre [URL de point de terminaison](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa); ici sont des exemples de ce que peuvent ressembler :
    > - Europe de l’ouest : `https://westeurope.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`
    > - Asie du Sud-est : `https://southeastasia.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`
    > - Est de l’Australie : `https://australiaeast.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Tags`

7.  Code pour Awake doit maintenant être ajouté. 

    ```csharp
        private void Awake()
        {
            // allows this instance to behave like a singleton
            instance = this;
        }
    ```

8.  Ensuite, ajoutez la coroutine (avec la méthode statique de flux en dessous), qui obtient les résultats de l’analyse de l’image capturée par le *ImageCapture* classe. 

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

9.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.
10. Précédent dans l’éditeur Unity, cliquez et faites glisser le *VisionManager* et *ImageCapture* classes à partir de la **Scripts** dossier pour le **Main Camera**de l’objet dans le *hiérarchie panneau*. 

## <a name="chapter-8--before-building"></a>Chapitre 8 – avant la génération

Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre HoloLens.
Avant de procéder, assurez-vous que :

-   Tous les paramètres mentionnés dans [chapitre 2](#chapter-2--set-up-the-unity-project) sont correctement définies. 
-   Tous les scripts sont attachés à la **Main Camera** objet. 
-   Tous les champs dans le *panneau Inspecteur de caméra principal* sont affectées correctement.
-   Assurez-vous que vous insérez votre **Auth Key** dans le **authorizationKey** variable.
-   Vérifiez que vous avez vérifié également votre point de terminaison votre *VisionManager* script et qu’il s’aligne sur *votre* région (ce document utilise *ouest des États-Unis-us* par défaut).

## <a name="chapter-9--build-the-uwp-solution-and-sideload-the-application"></a>Chapitre 9 – générer la Solution de UWP et le chargement de version test, l’application
Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.

1.  Accédez à *les paramètres de génération* - **fichier > Paramètres de Build...**
2.  À partir de la *paramètres de Build* fenêtre, cliquez sur **Build**.

    ![Création de l’application à partir d’Unity](images/AzureLabs-Lab2-26.png)

3.  Si pas déjà fait, cochez **Unity C# projets**.
4.  Cliquez sur **Build**. Unity lancera un *Explorateur de fichiers* fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans. Créez ce dossier, puis nommez-le *application*. Ensuite avec le *application* dossier sélectionné, appuyez sur **sélectionner le dossier**. 
5.  Unity commencera à générer votre projet pour le *application* dossier. 
6.  Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un *Explorateur de fichiers* fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).

## <a name="chapter-10--deploy-to-hololens"></a>Chapitre 10 – déployer sur HoloLens

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

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab2-27.png)
 
5.  Accédez à la **menu Générer** , puis cliquez sur **déployer la Solution**, chargement de version test l’application à votre HoloLens.
6.  Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !

> [!NOTE]
> Pour déployer sur casque immersif, définissez le **plateforme de Solution** à *ordinateur Local*et définissez le **Configuration** à *déboguer*, avec *x86* en tant que le **plateforme**. Déployer sur l’ordinateur local d’ordinateur, à l’aide de la **menu Générer**, en sélectionnant *déployer la Solution*. 

## <a name="your-finished-computer-vision-api-application"></a>Votre application API vision par ordinateur terminée

Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API de vision par ordinateur Azure pour reconnaître des objets du monde réel et afficher le niveau de confiance de ce qui a été vu.

![résultat de laboratoire](images/AzureLabs-Lab2-000.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Tout comme vous avez utilisé le *balises* paramètre (comme le démontre au sein de la *point de terminaison* utilisé dans le *VisionManager*), étendre l’application pour détecter d’autres informations ; un œil à les autres paramètres que vous avez accès à [ici](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa).

### <a name="exercise-2"></a>Exercice 2

Afficher les données retournées Azure, de façon plus CONVERSATIONNELLE et lisible, peut-être masquer les numéros de. Comme si un robot peut-être parler à l’utilisateur.
