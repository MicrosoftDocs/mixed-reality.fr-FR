---
title: MR et Azure 305 - fonctions et stockage
description: Terminer ce cours pour apprendre à implémenter le stockage Azure et des fonctions dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, fonctions, stockage, hololens, réalité virtuelle immersive,
ms.openlocfilehash: a828c7f0ac3016462f5c7e874545bf50a2db6771
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593546"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br> 

# <a name="mr-and-azure-305-functions-and-storage"></a>MR et Azure 305 : Fonctions et stockage

![produit final-Démarrer](images/AzureLabs-Lab5-00.png)

Dans ce cours, vous allez apprendre à créer et utiliser Azure Functions et stocker des données avec une ressource de stockage Azure, dans une application de réalité mixte.

*Azure Functions* est un service Microsoft, ce qui permet aux développeurs d’exécuter de petits morceaux de code, « fonctions », dans Azure. Cela fournit un moyen permettant de déléguer le cloud, plutôt que votre application locale, ce qui peut avoir de nombreux avantages. *Azure Functions* prend en charge plusieurs langages de développement, y compris C\#, F\#, Node.js, Java et PHP. Pour plus d’informations, visitez le [article d’Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview).

*Stockage Azure* est un service de cloud Microsoft, ce qui permet aux développeurs de stocker des données, avec l’assurance qu’il sera hautement disponible, sécurisé, durable, évolutif et redondant. Cela signifie que Microsoft gère toutes les maintenance et les problèmes critiques pour vous. Pour plus d’informations, visitez le [l’article Azure Storage](https://docs.microsoft.com/azure/storage/common/storage-introduction).

Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :

1.  Autoriser l’utilisateur à les regards autour d’une scène.
2.  Déclencher la génération dynamique des objets lors de son de l’utilisateur à une 3D « button ».
3.  Les objets générées seront sélectionnées par une fonction Azure.
4.  Comme chaque objet est généré, l’application stocke le type d’objet dans un *fichiers Azure*, situé dans *stockage Azure*.
5.  Lors du chargement d’une deuxième fois, le *fichiers Azure* données sont récupérées et permet de relire les actions de génération à partir de l’instance précédente de l’application.

Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception. Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity. Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre Application de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>MR et Azure 305 : Fonctions et stockage</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens. Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens.

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
- Un abonnement à un compte Azure pour la création de ressources Azure
- Accès à Internet pour la récupération de données et le programme d’installation Azure

## <a name="before-you-start"></a>Avant de commencer

Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).

## <a name="chapter-1---the-azure-portal"></a>Chapitre 1 : le portail Azure

Pour utiliser le **Service de stockage Azure**, vous devez créer et configurer un **compte de stockage** dans le portail Azure.

1.  Connectez-vous à la [Azure Portal](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *compte de stockage*, puis cliquez sur **entrée**.

    ![recherche de stockage Azure](images/AzureLabs-Lab5-01.png)

    > [!NOTE]
    > Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.

3.  La nouvelle page doit fournir une description de la *compte de stockage Azure* service. En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.

    ![créer le service](images/AzureLabs-Lab5-02.png)

4.  Une fois que vous avez cliqué sur **créer**:

    1.  Insérer un *nom* pour votre compte, n’oubliez pas ce champ accepte uniquement des lettres minuscules et chiffres.

    2.  Pour *modèle de déploiement*, sélectionnez **Resource manager**.

    3.  Pour *type de compte*, sélectionnez **stockage (usage général v1)**.

    4.  Déterminer le *emplacement* pour votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions.

    5.  Pour *réplication* sélectionnez **en lecture-access-geo-redundant storage (RA-GRS)**.

    6.  Pour *performances*, sélectionnez **Standard**.

    7.  Laissez *transfert sécurisé requis* comme **désactivé**.

    8.  Sélectionnez un *abonnement*.

    9. Choisissez un *groupe de ressources* ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs). 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    10. Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.

    11. Sélectionnez **Créer**.

        ![informations sur le service d’entrée](images/AzureLabs-Lab5-03.png)

5.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.

6.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![nouvelle notification dans le portail azure](images/AzureLabs-Lab5-04.png)

7.  Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.

    ![accéder à la ressource](images/AzureLabs-Lab5-05.png)

8.  Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. Vous serez dirigé vers votre nouvelle *compte de stockage* instance de service.

    ![touches d’accès rapide](images/AzureLabs-Lab5-06.png)

9.  Cliquez sur *clés d’accès*, pour faire apparaître les points de terminaison pour ce service cloud. Utilisez *le bloc-notes* ou similaire, de copier l’un de vos clés pour une utilisation ultérieure. En outre, notez le *chaîne de connexion* valeur, car il sera utilisé dans le *AzureServices* (classe), ce qui vous créerez ultérieurement.

    ![Copiez la chaîne de connexion](images/AzureLabs-Lab5-07.png)

## <a name="chapter-2---setting-up-an-azure-function"></a>Chapitre 2 - Configuration d’une fonction Azure

Vous allez maintenant écrire un **Azure** **fonction** dans le Service Azure.

Vous pouvez utiliser un **Azure Function** à faire presque tout ce que vous le feriez avec une fonction classique dans votre code, la différence étant que cette fonction est accessible par toute application qui a des informations d’identification pour accéder à votre compte Azure.

Pour créer une fonction Azure :

1.  À partir de votre *Azure Portal*, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *Function App*, puis cliquez sur **entrée**.

    ![Créer l’application de fonction](images/AzureLabs-Lab5-08.png)

    > [!NOTE]
    > Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.

2.  La nouvelle page doit fournir une description de la *Azure Function App* service. En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.

    ![informations sur l’application (fonction)](images/AzureLabs-Lab5-09.png)

3.  Une fois que vous avez cliqué sur **créer**:

    1.  Fournir un *nom de l’application*. Uniquement des lettres et des chiffres peuvent être utilisés ici (limite supérieure ou inférieure est autorisé).

    2.  Sélectionnez votre *abonnement*.

    3. Choisissez un *groupe de ressources* ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs). 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    4.  Dans cet exercice, sélectionnez *Windows* comme choisi **système d’exploitation**.

    5.  Sélectionnez *Plan de consommation* pour le **Plan d’hébergement**.

    6.  Déterminer le *emplacement* pour votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions. Pour des performances optimales, sélectionnez la même région que le compte de stockage.

    7.  Pour *stockage*, sélectionnez **utiliser l’existant**, et puis en utilisant le menu déroulant, recherchez votre stockage créé précédemment.

    8.  Laissez *Application Insights* désactivée pour cet exercice.

        ![Détails de l’application d’entrée (fonction)](images/AzureLabs-Lab5-10.png)

4.  Cliquez sur le bouton **Créer**.

5.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.

6.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![nouvelle notification du portail azure](images/AzureLabs-Lab5-11.png)

7.  Cliquez sur les notifications pour Explorer votre nouvelle instance de Service. 

    ![Accédez à l’application de ressource (fonction)](images/AzureLabs-Lab5-12.png)

8.  Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. Vous serez dirigé vers votre nouvelle *Function App* instance de service.

9.  Sur le *Function App* tableau de bord, pointez votre souris sur *fonctions*, trouvé dans le volet gauche, puis cliquez sur le **+ (plus)** symbole.

    ![Créer une nouvelle fonction](images/AzureLabs-Lab5-13.png)

10. Sur la page suivante, vérifiez **Webhook + API** est sélectionnée et pour *choisir une langue,* sélectionnez **CSharp**, comme il s’agit de la langue utilisée pour ce didacticiel. Enfin, cliquez sur le **créer cette fonction** bouton.

    ![Sélectionnez web raccordement csharp](images/AzureLabs-Lab5-14.png)

11. Vous devez être dirigé vers le code page (run.csx), si ce n’est pas, cliquez sur la fonction qui vient d’être créée dans la liste des fonctions dans le panneau de gauche.

    ![Ouvrez la nouvelle fonction](images/AzureLabs-Lab5-15.png)

12. Copiez le code suivant dans votre fonction. Cette fonction retourne simplement un entier aléatoire compris entre 0 et 2 lorsqu’elle est appelée. Ne pas vous inquiétez pas sur le code existant, n’hésitez pas à coller au-dessus d’elle.

    ```csharp
        using System.Net;
        using System.Threading.Tasks;

        public static int Run(CustomObject req, TraceWriter log)
        {
            Random rnd = new Random();
            int randomInt = rnd.Next(0, 3);
            return randomInt;
        }

        public class CustomObject
        {
            public String name {get; set;}
        }
    ```

13. Sélectionnez **Enregistrer**.

14. Le résultat doit ressembler à l’image ci-dessous.

15. Cliquez sur **obtenir l’URL de la fonction** et prenez note de la *point de terminaison* affiché. Vous devez l’insérer dans le *AzureServices* classe que vous créerez plus loin dans ce cours.

    ![obtenir le point de terminaison (fonction)](images/AzureLabs-Lab5-16.png)

    ![obtenir le point de terminaison (fonction)](images/AzureLabs-Lab5-16-5.png)

## <a name="chapter-3---setting-up-the-unity-project"></a>Chapitre 3 - Configuration du projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

Configurer et tester votre casque immersives de réalité mixte.

> [!NOTE]
> Vous allez **pas** nécessitent des contrôleurs de mouvement pour ce cours. Si vous avez besoin de prendre en charge de paramétrage le casque immersif, veuillez [visitez la réalité mixte configurer article](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).

1.  Ouvrez Unity et cliquez sur **New**.

    ![créer un projet unity](images/AzureLabs-Lab5-17.png)

2.  Maintenant, vous devez fournir un nom de projet Unity. Insérer **MR_Azure_Functions**. Assurez-vous que le type de projet est défini sur **3D**. Définir le *emplacement* à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![Donnez un nom à un projet unity](images/AzureLabs-Lab5-18.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **modifier* > *préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![ensemble de visual studio comme éditeur de script](images/AzureLabs-Lab5-19.png)

4.  Ensuite, accédez à **fichier > Paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **plateforme basculer** bouton.

    ![plateforme de commutation vers uwp](images/AzureLabs-Lab5-20.png)

5.  Accédez à **fichier > Paramètres de Build** et vous assurer que :

    1. **Équipement cible** a la valeur **n’importe quel appareil**.

        > Pour Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.

    2. **Type de build** a la valeur **D3D**

    3. **Kit de développement logiciel** a la valeur **dernière installé**

    4. **Version de Visual Studio** a la valeur **dernière installé**

    5. **Générez et exécutez** est défini sur **ordinateur Local**

    6. Enregistrer la scène et l’ajouter à la build.

        1.  Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.

            ![ajouter des scènes ouverts](images/AzureLabs-Lab5-21.png)

        2.  Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![créer le dossier de scènes](images/AzureLabs-Lab5-22.png)

        3.  Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le **nom de fichier :** champ de texte, tapez **FunctionsScene**, puis appuyez sur **enregistrer**.

            ![Enregistrer la scène de fonctions](images/AzureLabs-Lab5-23.png)

6.  Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.

    ![Enregistrer la scène de fonctions](images/AzureLabs-Lab5-24.png)

7.  Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.

    ![paramètres du lecteur dans l’inspecteur](images/AzureLabs-Lab5-25.png)

8.  Dans ce panneau, quelques paramètres doivent être vérifiées :

    1.  Dans le **autres paramètres** onglet :

        1.  **Version du Runtime de script** doit être **expérimental** (.NET 4.6 équivalent), ce qui déclenchera une nécessité de redémarrer l’éditeur.
        2.  **Script principal** doit être **.NET**
        3.  **Niveau de compatibilité d’API** doit être **.NET 4.6**

    2.  Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :
        
        -  **InternetClient**

            ![jeu de fonctionnalités](images/AzureLabs-Lab5-26.png)

    3.  Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **Windows Mixed Reality Kit de développement logiciel** est ajouté.

        ![définir les paramètres de XR](images/AzureLabs-Lab5-27.png)

9.  Dans *paramètres de Build* *Unity C# projets* est n’est plus grisée ; Cochez la case à cocher en regard de cela.

    ![projets c# graduation](images/AzureLabs-Lab5-28.png)

10.  Fermez la fenêtre Paramètres de Build.

11. Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).

## <a name="chapter-4---setup-main-camera"></a>Chapitre 4 - la caméra principale le programme d’installation

> [!IMPORTANT]
> Si vous souhaitez ignorer la *Unity configurer* les composants de ce cours et continuer directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20305%20-%20Functions%20and%20storage/Azure-MR-305.unitypackage)et l’importer dans votre projet en tant qu’un [personnalisé Package](https://docs.unity3d.com/Manual/AssetPackages.html). Il contient également les DLL dans le chapitre suivant. Après l’importation, continuer à partir de [chapitre 7](#chapter-7---create-the-azureservices-class). 

1.  Dans le *hiérarchie panneau*, vous trouverez un objet appelé **Main Camera**, cet objet représente votre point de vue du « head » une fois que vous êtes « à l’intérieur » de votre application.

2.  Avec le tableau de bord Unity devant vous, sélectionnez le **GameObject de caméra principale**. Vous remarquerez que le *panneau Inspecteur* (généralement situé vers la droite, dans le tableau de bord) affiche les différents composants de qui *GameObject*, avec *transformer* en haut, suivie de *caméra*et certains autres composants. Vous devez réinitialiser la transformation de la caméra principale, donc il est positionné correctement.

3.  Pour ce faire, sélectionnez le **ENGRENAGE** icône en regard de la caméra *transformer* composant, puis sélectionnez **réinitialiser**.

    ![Réinitialiser la transformation](images/AzureLabs-Lab5-29.png)

4.  Puis mettez à jour le **transformer** composant ressemble à :

    |         |    TRANSFORMATION - POSITION   |       |
    | :-----: | :-----------------------: | :----:|
    | **X**   | **Y**                     | **Z** |
    | 0       | 1                         | 0     |    

    |       | TRANSFORMATION - ROTATION |       |
    | :---: | :------------------: | :----:|
    | **X** | **Y**                | **Z** |
    | 0     | 0                    | 0     |

    |       | TRANSFORMATION - MISE À L’ÉCHELLE |       |
    | :---: | :---------------: | :---: |
    | **X** | **Y**             | **Z** |
    | 1     | 1                 | 1     |

    ![transformation de la caméra](images/AzureLabs-Lab5-30.png)

## <a name="chapter-5---setting-up-the-unity-scene"></a>Chapitre 5 : configuration de la scène Unity

1.  Avec le bouton droit dans une zone vide de la *hiérarchie panneau*, sous **objet 3D**, ajoutez un **plan**.

    ![créer un nouveau plan](images/AzureLabs-Lab5-31.png)

2.  Avec le **plan** de l’objet sélectionné, modifiez les paramètres suivants dans le *panneau Inspecteur*:

    |       | TRANSFORMATION - POSITION |       |
    | :---: | :------------------: | :---: |
    | **X** | **Y**                | **Z** |
    | 0     | 0                    | 4     |

    |       | TRANSFORMATION - MISE À L’ÉCHELLE |       |
    | :---: | :---------------: | :---: |
    | **X** | **Y**             | **Z** |
    | 10    | 1                 | 10    |

    ![position du jeu de plan et mise à l’échelle](images/AzureLabs-Lab5-32.png)

    ![vue de la scène du plan](images/AzureLabs-Lab5-33.png)

3.  Avec le bouton droit dans une zone vide de la *hiérarchie panneau*, sous **objet 3D**, ajoutez un **Cube**.

    1.  Renommer le Cube à **GazeButton** (avec le Cube sélectionné, appuyez sur « F2 »).

    2.  Modifiez les paramètres suivants dans le *panneau Inspecteur*:

        |       | TRANSFORMATION - POSITION |       |
        | :---: | :------------------: |:-----:|
        | **X** | **Y**                | **Z** |
        | 0     | 3                    | 5     |


        ![transformation de bouton regards de jeu](images/AzureLabs-Lab5-34.png)

        ![utilisation de vue de la scène bouton](images/AzureLabs-Lab5-35.png)

    3.  Cliquez sur le **balise** bouton de liste déroulante, puis cliquez sur **ajouter une balise** pour ouvrir le *balises & volet couches*.

        ![Ajouter une nouvelle balise](images/AzureLabs-Lab5-36.png)

        ![Sélectionnez plus (+)](images/AzureLabs-Lab5-37.png)

    4.  Sélectionnez le **+ (plus)** bouton, puis, dans le *nouveau nom de balise* , entrez **GazeButton**, puis appuyez sur **enregistrer**.

        ![nouvelle balise de nom](images/AzureLabs-Lab5-38.png)

    5.  Cliquez sur le **GazeButton** de l’objet dans le *hiérarchie panneau*, puis, dans le *panneau Inspecteur*, affecter nouvellement créé **GazeButton** balise.

        ![affecter des regards bouton la nouvelle balise](images/AzureLabs-Lab5-39.png)

4.  Avec le bouton droit sur le **GazeButton** de l’objet, dans le *Panneau de la hiérarchie*et ajoutez un **GameObject vide** (qui sera ajouté comme un *enfant* objet).

5.  Sélectionnez le nouvel objet et renommez-la **ShapeSpawnPoint**.

    1.  Modifiez les paramètres suivants dans le *panneau Inspecteur*:

        |       | TRANSFORMATION - POSITION |       |
        | :---: | :------------------: |:----: |
        | **X** |**Y**                 | **Z** |
        | 0     | -1                   | 0     |

        ![mettre à jour le point de la génération dynamique de forme Transformer](images/AzureLabs-Lab5-40.png)

        ![vue de la scène de forme de point de la génération dynamique](images/AzureLabs-Lab5-41.png)

6.  Vous allez ensuite créer un **texte 3D** objet pour fournir des commentaires sur l’état du service Azure.

    Cliquez avec le bouton droit sur le **GazeButton** panneau à nouveau dans la hiérarchie et ajoutez un **objet 3D > texte 3D** de l’objet en tant qu’un *enfant*.

    ![créer le nouvel objet de texte 3D](images/AzureLabs-Lab5-42.png)

7.  Renommer le **texte 3D** objet **AzureStatusText**.

8.  Modifier le **AzureStatusText** transformation de l’objet comme suit :

    |       | TRANSFORMATION - POSITION |       |
    | :---: | :------------------: | :---: |
    | **X** | **Y**                | **Z** |
    | 0     | 0                    | -0.6  |

    |       | TRANSFORMATION - MISE À L’ÉCHELLE |       |
    | :---: | :---------------: | :---: |
    | **X** | **Y**             | **Z** |
    | 0.1   | 0.1               | 0.1   |


    > [!NOTE]
    > Ne vous inquiétez pas si elle semble être hors tension-centre, que ce problème sera résolu lorsque la ci-dessous texte Mesh composant est mis à jour.

9.  Modifier le **texte maillage** composant pour faire correspondre le ci-dessous :

    ![composant de maillage de texte Set](images/AzureLabs-Lab5-43.png)

    > [!TIP]
    > La couleur sélectionnée ici est de couleur hexadécimale : **000000FF**, mais n’hésitez pas à choisir votre propre, assurez-vous simplement qu’il est lisible.

10. Votre structure de hiérarchie le panneau de configuration doit maintenant ressembler à ceci :

    ![texte de maillage dans la vue de la scène](images/AzureLabs-Lab5-43b.png)

10. Votre scène doit maintenant ressembler à ceci :

    ![texte de maillage dans la vue de la scène](images/AzureLabs-Lab5-44.png)


## <a name="chapter-6---import-azure-storage-for-unity"></a>Chapitre 6 - importer le stockage Azure pour Unity

Vous allez utiliser Azure Storage pour Unity (qui, elle s’appuie sur le kit SDK Azure .net). Vous trouverez plus d’informations sur ce point dans le [stockage Azure pour l’article de Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).

Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation. Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.

Pour importer le SDK dans votre propre projet, assurez-vous que vous avez téléchargé la dernière version ['.unitypackage' à partir de GitHub](https://aka.ms/azstorage-unitysdk). Ensuite, procédez comme suit :

1.  Ajouter le **.unitypackage** fichier à Unity à l’aide de la **actifs > Importer un Package > Custom Package** option de menu.

2.  Dans le **importer un Package Unity** zone s’affiche, vous pouvez sélectionner tous les éléments sous **plug-in* > *stockage**. Désactivez tout le reste, qu’il n’est pas nécessaire pour ce cours.

    ![importer dans le package](images/AzureLabs-Lab5-45.png)

3.  Cliquez sur le **importation** pour ajouter les éléments à votre projet.

4.  Accédez à la *stockage* dossier sous *plug-ins*, dans la vue du projet, puis sélectionnez les plug-ins suivants *uniquement*:

    -   Microsoft.Data.Edm
    -   Microsoft.Data.OData
    -   Microsoft.WindowsAzure.Storage
    -   Newtonsoft.Json
    -   System.Spatial

        ![Décochez la case n’importe quelle plateforme](images/AzureLabs-Lab5-46.png)

5.  Avec *ces plug-ins spécifiques* sélectionné, **Décochez** *plateforme Any* et **Décochez** *WSAPlayer* puis cliquez sur **appliquer**.

    ![appliquer des DLL de plateforme](images/AzureLabs-Lab5-47.png)

    > [!NOTE]
    > Nous allons marquer ces plug-ins particuliers à utiliser uniquement dans l’éditeur Unity. Il s’agit, car il existe différentes versions des mêmes plug-ins dans le dossier WSA qui sera utilisé après que le projet est exporté à partir d’Unity.

6.  Dans le *stockage* dossier de plug-in, sélectionnez uniquement :

    -   Microsoft.Data.Services.Client

        ![jeu de ne pas traiter les DLL](images/AzureLabs-Lab5-48.png)

7.  Vérifier le **processus ne** sous *paramètres de plateforme* et cliquez sur **appliquer**.

    ![n’appliquer aucun traitement](images/AzureLabs-Lab5-49.png)

    > [!NOTE]
    > Nous sommes marquage ce plug-in « Ne pas traiter », car l’utilitaire de correction Unity assembly a des difficultés à traiter ce plug-in. Le plug-in continue de fonctionner même si elle n’est pas traitée.

## <a name="chapter-7---create-the-azureservices-class"></a>Chapitre 7 - créer la classe AzureServices

La première classe que vous vous apprêtez à créer est le *AzureServices* classe.

Le *AzureServices* classe sera chargée de :

-   Stockage des informations d’identification de compte Azure.

-   Appel de votre application de fonction Azure.

-   Le chargement et le téléchargement du fichier de données dans votre stockage de Cloud Azure.

Pour créer cette classe :

1.  Avec le bouton droit dans le *Asset* dossier, situé dans le panneau de configuration de projet, **créer > dossier**. Nommez le dossier **Scripts**.

    ![créer un nouveau dossier](images/AzureLabs-Lab5-50.png)

    ![appelons le dossier - scripts](images/AzureLabs-Lab5-51.png)

2.  Double-cliquez sur le dossier venez de créer, pour l’ouvrir.

3.  Avec le bouton droit dans le dossier, **créer > C# Script**. Appeler le script *AzureServices*.

4.  Double-cliquez sur le nouveau *AzureServices* classe pour l’ouvrir avec *Visual Studio*.

5.  Ajoutez les espaces de noms suivantes au début de la *AzureServices*:

    ```csharp
        using System;
        using System.Threading.Tasks;
        using UnityEngine;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.File;
        using System.IO;
        using System.Net;
    ```

6.  Ajoutez les champs d’inspecteur suivants à l’intérieur de la *AzureServices* classe :

    ```csharp
        /// <summary>
        /// Provides Singleton-like behavior to this class.
        /// </summary>
        public static AzureServices instance;

        /// <summary>
        /// Reference Target for AzureStatusText Text Mesh object
        /// </summary>
        public TextMesh azureStatusText;
    ```

7.  Puis ajoutez les variables de membre suivantes à l’intérieur de la *AzureServices* classe :

    ```csharp
        /// <summary>
        /// Holds the Azure Function endpoint - Insert your Azure Function
        /// Connection String here.
        /// </summary>

        private readonly string azureFunctionEndpoint = "--Insert here you AzureFunction Endpoint--";

        /// <summary>
        /// Holds the Storage Connection String - Insert your Azure Storage
        /// Connection String here.
        /// </summary>
        private readonly string storageConnectionString = "--Insert here you AzureStorage Connection String--";

        /// <summary>
        /// Name of the Cloud Share - Hosts directories.
        /// </summary>
        private const string fileShare = "fileshare";

        /// <summary>
        /// Name of a Directory within the Share
        /// </summary>
        private const string storageDirectory = "storagedirectory";

        /// <summary>
        /// The Cloud File
        /// </summary>
        private CloudFile shapeIndexCloudFile;

        /// <summary>
        /// The Linked Storage Account
        /// </summary>
        private CloudStorageAccount storageAccount;

        /// <summary>
        /// The Cloud Client
        /// </summary>
        private CloudFileClient fileClient;

        /// <summary>
        /// The Cloud Share - Hosts Directories
        /// </summary>
        private CloudFileShare share;

        /// <summary>
        /// The Directory in the share that will host the Cloud file
        /// </summary>
        private CloudFileDirectory dir;
    ```

    > [!IMPORTANT]
    > Veillez à remplacer le *point de terminaison* et *chaîne de connexion* valeurs avec les valeurs de votre stockage Azure, trouvé dans le portail Azure

8.  Code pour *Awake()* et *Start()* méthodes doit maintenant être ajouté. Ces méthodes seront appelées lors de l’initialisation de la classe :

    ```csharp
        private void Awake()
        {
            instance = this;
        }

        // Use this for initialization
        private void Start()
        {
            // Set the Status text to loading, whilst attempting connection to Azure.
            azureStatusText.text = "Loading...";
        }

        /// <summary>
        /// Call to the Azure Function App to request a Shape.
        /// </summary>
        public async void CallAzureFunctionForNextShape()
        {

        }
    ```

    > [!IMPORTANT]
    > Nous permet de renseigner le code pour *CallAzureFunctionForNextShape()* dans un [chapitre futures](#chapter-10---completing-the-AzureServices-class).

9.  Supprimer le *Update()* étant donné que cette classe ne l’utilise pas de méthode.

10. Enregistrez vos modifications dans Visual Studio, puis revenez à Unity.

11. Cliquez et faites glisser le *AzureServices* classe à partir du dossier Scripts à l’objet Main Camera dans le *hiérarchie panneau*.

12. Sélectionnez la caméra principale, puis saisissez le **AzureStatusText** objet enfant à partir de sous le **GazeButton** de l’objet et placez-le dans le **AzureStatusText** cible de référence champ dans le *inspecteur*, pour fournir la référence à la *AzureServices* script.

    ![affecter la cible de référence de texte de statut azure](images/AzureLabs-Lab5-52.png)

## <a name="chapter-8---create-the-shapefactory-class"></a>Chapitre 8 - créer la classe ShapeFactory

Le script suivant pour créer, est la *ShapeFactory* classe. Le rôle de cette classe consiste à créer une nouvelle forme lorsque demandé et conserver un historique des formes créées dans un *forme historique*. Chaque fois qu’une forme est créée, le *forme historique* est mis à jour dans le *AzureService* classe et stockées dans votre *stockage Azure*. Lorsque l’application démarre, si un fichier stocké est trouvé dans votre *stockage Azure*, le *forme historique* est récupéré et relus, avec le **texte 3D** objet fournissant Indique si la forme générée est à partir du stockage, ou de nouvelles.

Pour créer cette classe :

1.  Accédez à la **Scripts** dossier que vous avez créé précédemment.

2.  Avec le bouton droit dans le dossier, **créer > C# Script**. Appeler le script *ShapeFactory*.

3.  Double-cliquez sur le nouveau *ShapeFactory* script pour l’ouvrir avec *Visual Studio*.

4.  Vérifiez le *ShapeFactory* classe inclut des espaces de noms suivants :

    ```csharp
        using System.Collections.Generic;
        using UnityEngine;
    ```

5.  Ajoutez les variables ci-dessous pour le *ShapeFactory* classe, puis remplacez le *Start()* et *Awake()* fonctions avec ceux ci-dessous :

    ```csharp
        /// <summary>
        /// Provide this class Singleton-like behaviour
        /// </summary>
        [HideInInspector]
        public static ShapeFactory instance;

        /// <summary>
        /// Provides an Inspector exposed reference to ShapeSpawnPoint
        /// </summary>
        [SerializeField]
        public Transform spawnPoint;

        /// <summary>
        /// Shape History Index
        /// </summary>
        [HideInInspector]
        public List<int> shapeHistoryList;

        /// <summary>
        /// Shapes Enum for selecting required shape
        /// </summary>
        private enum Shapes { Cube, Sphere, Cylinder }

        private void Awake()
        {
            instance = this;
        }

        private void Start()
        {
            shapeHistoryList = new List<int>();
        }
    ```

6.  Le *CreateShape()* méthode génère les formes primitifs, en fonction de la liste fournie *entier* paramètre. Le paramètre booléen est utilisé pour spécifier si la forme actuellement créée à partir du stockage, ou nouvelle. Placez le code suivant dans votre *ShapeFactory* (classe), sous les méthodes précédentes :

    ```csharp
        /// <summary>
        /// Use the Shape Enum to spawn a new Primitive object in the scene
        /// </summary>
        /// <param name="shape">Enumerator Number for Shape</param>
        /// <param name="storageShape">Provides whether this is new or old</param>
        internal void CreateShape(int shape, bool storageSpace)
        {
            Shapes primitive = (Shapes)shape;
            GameObject newObject = null;
            string shapeText = storageSpace == true ? "Storage: " : "New: ";

            AzureServices.instance.azureStatusText.text = string.Format("{0}{1}", shapeText, primitive.ToString());

            switch (primitive)
            {
                case Shapes.Cube:
                newObject = GameObject.CreatePrimitive(PrimitiveType.Cube);
                break;

                case Shapes.Sphere:
                newObject = GameObject.CreatePrimitive(PrimitiveType.Sphere);
                break;

                case Shapes.Cylinder:
                newObject = GameObject.CreatePrimitive(PrimitiveType.Cylinder);
                break;
            }

            if (newObject != null)
            {
                newObject.transform.position = spawnPoint.position;

                newObject.transform.localScale = new Vector3(0.5f, 0.5f, 0.5f);

                newObject.AddComponent<Rigidbody>().useGravity = true;

                newObject.GetComponent<Renderer>().material.color = UnityEngine.Random.ColorHSV(0f, 1f, 1f, 1f, 0.5f, 1f);
            }
        }
    ```

7.  Veillez à enregistrer vos modifications dans Visual Studio avant de retourner à Unity.

8.  Précédent dans l’éditeur Unity, cliquez et faites glisser le *ShapeFactory* classe à partir de la **Scripts** dossier pour le **Main Camera** de l’objet dans le *hiérarchie panneau*.

9. Avec la caméra principale sélectionnée, vous remarquerez le *ShapeFactory* du composant script est manquant le *Spawn Point* référence. Pour corriger ce problème, faites glisser le **ShapeSpawnPoint** de l’objet à partir de la *Panneau de la hiérarchie* à la **Spawn Point** cible de référence.

    ![cible de référence de jeu forme factory](images/AzureLabs-Lab5-53.png)

## <a name="chapter-9---create-the-gaze-class"></a>Chapitre 9 - créer la classe du pointage de regard

Est le dernier script, vous devez créer le *les regards* classe.

Cette classe est chargée pour la création d’un **Raycast** qui est projeté vers l’avant à partir de la caméra principale, pour détecter quel objet consulte l’utilisateur. Dans ce cas, le Raycast devrez déterminer si l’utilisateur consulte la **GazeButton** de l’objet dans la scène et déclencher un comportement.

Pour créer cette classe :

1.  Accédez à la **Scripts** dossier que vous avez créé précédemment.

2.  Avec le bouton droit dans le volet de projet, **créer > C# Script**. Appeler le script *les regards*.

3.  Double-cliquez sur le nouveau *les regards* script pour l’ouvrir avec *Visual Studio.*

4.  Vérifiez que l’espace de noms suivant est inclus en haut du script :

    ```csharp
        using UnityEngine;
    ```

5.  Puis ajoutez les variables suivantes à l’intérieur de la *les regards* classe :

    ```csharp
        /// <summary>
        /// Provides Singleton-like behavior to this class.
        /// </summary>
        public static Gaze instance;

        /// <summary>
        /// The Tag which the Gaze will use to interact with objects. Can also be set in editor.
        /// </summary>
        public string InteractibleTag = "GazeButton";

        /// <summary>
        /// The layer which will be detected by the Gaze ('~0' equals everything).
        /// </summary>
        public LayerMask LayerMask = ~0;

        /// <summary>
        /// The Max Distance the gaze should travel, if it has not hit anything.
        /// </summary>
        public float GazeMaxDistance = 300;

        /// <summary>
        /// The size of the cursor, which will be created.
        /// </summary>
        public Vector3 CursorSize = new Vector3(0.05f, 0.05f, 0.05f);

        /// <summary>
        /// The color of the cursor - can be set in editor.
        /// </summary>
        public Color CursorColour = Color.HSVToRGB(0.0223f, 0.7922f, 1.000f);

        /// <summary>
        /// Provides when the gaze is ready to start working (based upon whether
        /// Azure connects successfully).
        /// </summary>
        internal bool GazeEnabled = false;

        /// <summary>
        /// The currently focused object.
        /// </summary>
        internal GameObject FocusedObject { get; private set; }

        /// <summary>
        /// The object which was last focused on.
        /// </summary>
        internal GameObject _oldFocusedObject { get; private set; }

        /// <summary>
        /// The info taken from the last hit.
        /// </summary>
        internal RaycastHit HitInfo { get; private set; }

        /// <summary>
        /// The cursor object.
        /// </summary>
        internal GameObject Cursor { get; private set; }

        /// <summary>
        /// Provides whether the raycast has hit something.
        /// </summary>
        internal bool Hit { get; private set; }

        /// <summary>
        /// This will store the position which the ray last hit.
        /// </summary>
        internal Vector3 Position { get; private set; }

        /// <summary>
        /// This will store the normal, of the ray from its last hit.
        /// </summary>
        internal Vector3 Normal { get; private set; }

        /// <summary>
        /// The start point of the gaze ray cast.
        /// </summary>
        private Vector3 _gazeOrigin;

        /// <summary>
        /// The direction in which the gaze should be.
        /// </summary>
        private Vector3 _gazeDirection;
    ```

> [!IMPORTANT]
> Certaines de ces variables pourront être modifiées dans le *éditeur*.

6.  Code pour le *Awake()* et *Start()* méthodes doit maintenant être ajouté.

    ```csharp
        /// <summary>
        /// The method used after initialization of the scene, though before Start().
        /// </summary>
        private void Awake()
        {
            // Set this class to behave similar to singleton
            instance = this;
        }

        /// <summary>
        /// Start method used upon initialization.
        /// </summary>
        private void Start()
        {
            FocusedObject = null;
            Cursor = CreateCursor();
        }
    ```

7.  Ajoutez le code suivant, qui crée un objet curseur au début, ainsi que la *Update()* (méthode), qui sera exécuté par la méthode Raycast, ainsi que d’en cours où la valeur booléenne GazeEnabled est activé ou désactivé :

    ```csharp
        /// <summary>
        /// Method to create a cursor object.
        /// </summary>
        /// <returns></returns>
        private GameObject CreateCursor()
        {
            GameObject newCursor = GameObject.CreatePrimitive(PrimitiveType.Sphere);
            newCursor.SetActive(false);

            // Remove the collider, so it doesn't block raycast.
            Destroy(newCursor.GetComponent<SphereCollider>());
            newCursor.transform.localScale = CursorSize;

            newCursor.GetComponent<MeshRenderer>().material = new Material(Shader.Find("Diffuse"))
            {
                color = CursorColour
            };

            newCursor.name = "Cursor";

            newCursor.SetActive(true);

            return newCursor;
        }

        /// <summary>
        /// Called every frame
        /// </summary>
        private void Update()
        {
            if(GazeEnabled == true)
            {
                _gazeOrigin = Camera.main.transform.position;

                _gazeDirection = Camera.main.transform.forward;

                UpdateRaycast();
            }
        }
    ```

8. Ajoutez ensuite le *UpdateRaycast()* (méthode), ce qui permettra une Raycast de projet et détecter la cible du positionnement.

    ```csharp
        private void UpdateRaycast()
        {
            // Set the old focused gameobject.
            _oldFocusedObject = FocusedObject;

            RaycastHit hitInfo;

            // Initialise Raycasting.
            Hit = Physics.Raycast(_gazeOrigin,
                _gazeDirection,
                out hitInfo,
                GazeMaxDistance, LayerMask);

            HitInfo = hitInfo;

            // Check whether raycast has hit.
            if (Hit == true)
            {
                Position = hitInfo.point;

                Normal = hitInfo.normal;

                // Check whether the hit has a collider.
                if (hitInfo.collider != null)
                {
                    // Set the focused object with what the user just looked at.
                    FocusedObject = hitInfo.collider.gameObject;
                }
                else
                {
                    // Object looked on is not valid, set focused gameobject to null.
                    FocusedObject = null;
                }
            }
            else
            {
                // No object looked upon, set focused gameobject to null.
                FocusedObject = null;

                // Provide default position for cursor.
                Position = _gazeOrigin + (_gazeDirection * GazeMaxDistance);

                // Provide a default normal.
                Normal = _gazeDirection;
            }

            // Lerp the cursor to the given position, which helps to stabilize the gaze.
            Cursor.transform.position = Vector3.Lerp(Cursor.transform.position, Position, 0.6f);

            // Check whether the previous focused object is this same 
            //    object. If so, reset the focused object.
            if (FocusedObject != _oldFocusedObject)
            {
                ResetFocusedObject();

                if (FocusedObject != null)
                {
                if (FocusedObject.CompareTag(InteractibleTag.ToString()))
                {
                        // Set the Focused object to green - success!
                        FocusedObject.GetComponent<Renderer>().material.color = Color.green;

                        // Start the Azure Function, to provide the next shape!
                        AzureServices.instance.CallAzureFunctionForNextShape();
                    }
                }
            }
        }
    ```

9. Enfin, ajoutez le *ResetFocusedObject()* (méthode), ce qui active et désactive la couleur GazeButton objets actuelle, qui indique si elle crée une nouvelle forme ou non.

    ```csharp
        /// <summary>
        /// Reset the old focused object, stop the gaze timer, and send data if it
        /// is greater than one.
        /// </summary>
        private void ResetFocusedObject()
        {
            // Ensure the old focused object is not null.
            if (_oldFocusedObject != null)
            {
                if (_oldFocusedObject.CompareTag(InteractibleTag.ToString()))
                {
                    // Set the old focused object to red - its original state.
                    _oldFocusedObject.GetComponent<Renderer>().material.color = Color.red;
                }
            }
        }
    ```

10.  Enregistrez vos modifications dans Visual Studio avant de retourner à Unity.

11.  Cliquez et faites glisser le *les regards* classe à partir du dossier Scripts à la **Main Camera** de l’objet dans le *hiérarchie panneau*.

## <a name="chapter-10---completing-the-azureservices-class"></a>Chapitre 10 - fin de la classe AzureServices

Avec les autres scripts en place, il est possible de *complète* le *AzureServices* classe. Cela sera possible via :

1.  Ajout d’une nouvelle méthode nommée *CreateCloudIdentityAsync()*, pour définir les variables de l’authentification nécessaires pour communiquer avec Azure.

    > Cette méthode vérifie également l’existence d’un fichier précédemment stocké qui contient la liste de forme.
    >
    > **Si le fichier se trouve**, il désactivera l’utilisateur *les regards*et déclencher la création de forme, selon le modèle de formes, tel que stocké dans le **fichier de stockage Azure**. L’utilisateur peut voir cela, comme le **texte Mesh** fournira l’affichage « Stockage » ou « Nouveau », en fonction de l’origine de formes.
    >
    > **Si aucun fichier n’est trouvé**, il prend en charge la *les regards*, ce qui permet de créer des formes en examinant le **GazeButton** objet dans la scène.

    ```csharp
        /// <summary>
        /// Create the references necessary to log into Azure
        /// </summary>
        private async void CreateCloudIdentityAsync()
        {
            // Retrieve storage account information from connection string
            storageAccount = CloudStorageAccount.Parse(storageConnectionString);

            // Create a file client for interacting with the file service.
            fileClient = storageAccount.CreateCloudFileClient();

            // Create a share for organizing files and directories within the storage account.
            share = fileClient.GetShareReference(fileShare);

            await share.CreateIfNotExistsAsync();

            // Get a reference to the root directory of the share.
            CloudFileDirectory root = share.GetRootDirectoryReference();

            // Create a directory under the root directory
            dir = root.GetDirectoryReference(storageDirectory);

            await dir.CreateIfNotExistsAsync();

            //Check if the there is a stored text file containing the list
            shapeIndexCloudFile = dir.GetFileReference("TextShapeFile");

            if (!await shapeIndexCloudFile.ExistsAsync())
            {
                // File not found, enable gaze for shapes creation
                Gaze.instance.GazeEnabled = true;

                azureStatusText.text = "No Shape\nFile!";
            }
            else
            {
                // The file has been found, disable gaze and get the list from the file
                Gaze.instance.GazeEnabled = false;

                azureStatusText.text = "Shape File\nFound!";

                await ReplicateListFromAzureAsync();
            }
        }
    ```

2.  L’extrait de code suivant est depuis le *Start()* méthode ; où un appel sera le *CreateCloudIdentityAsync()* (méthode). N’hésitez pas à copier sur votre actuel *Start()* (méthode), avec la ci-dessous :

    ```csharp
        private void Start()
        {
            // Disable TLS cert checks only while in Unity Editor (until Unity adds support for TLS)
    #if UNITY_EDITOR
            ServicePointManager.ServerCertificateValidationCallback = delegate { return true; };
    #endif

            // Set the Status text to loading, whilst attempting connection to Azure.
            azureStatusText.text = "Loading...";

            //Creating the references necessary to log into Azure and check if the Storage Directory is empty
            CreateCloudIdentityAsync();
        }
    ```

3.  Renseignez le code pour la méthode *CallAzureFunctionForNextShape()*. Vous allez utiliser l’élément précédemment créé *Azure Function App* pour demander un index de la forme. Une fois la nouvelle forme est reçue, cette méthode envoie la forme pour le *ShapeFactory* classe pour créer la nouvelle forme dans la scène. Utilisez le code ci-dessous pour terminer le corps de *CallAzureFunctionForNextShape()*.

    ```csharp
        /// <summary>
        /// Call to the Azure Function App to request a Shape.
        /// </summary>
        public async void CallAzureFunctionForNextShape()
        {
            int azureRandomInt = 0;

            // Call Azure function
            HttpWebRequest webRequest = WebRequest.CreateHttp(azureFunctionEndpoint);

            WebResponse response = await webRequest.GetResponseAsync();

            // Read response as string
            using (Stream stream = response.GetResponseStream())
            {
                StreamReader reader = new StreamReader(stream);

                String responseString = reader.ReadToEnd();

                //parse result as integer
                Int32.TryParse(responseString, out azureRandomInt);
            }

            //add random int from Azure to the ShapeIndexList
            ShapeFactory.instance.shapeHistoryList.Add(azureRandomInt);

            ShapeFactory.instance.CreateShape(azureRandomInt, false);

            //Save to Azure storage
            await UploadListToAzureAsync();
        }
    ```

4.  Ajoutez une méthode pour créer une chaîne, en concaténant les entiers stockés dans la liste d’historique de forme et l’enregistrer dans votre *Azure stockage fichier*.

    ```csharp
        /// <summary>
        /// Upload the locally stored List to Azure
        /// </summary>
        private async Task UploadListToAzureAsync()
        {
            // Uploading a local file to the directory created above
            string listToString = string.Join(",", ShapeFactory.instance.shapeHistoryList.ToArray());

            await shapeIndexCloudFile.UploadTextAsync(listToString);
        }
    ```

5.  Ajoutez une méthode pour récupérer le texte stocké dans le fichier situé dans votre *Azure stockage fichier* et *désérialiser* dans une liste.

6.  Une fois ce processus est terminé, la méthode réactive les regards afin que l’utilisateur peut ajouter plusieurs formes à la scène.

    ```csharp
        ///<summary>
        /// Get the List stored in Azure and use the data retrieved to replicate 
        /// a Shape creation pattern
        ///</summary>
        private async Task ReplicateListFromAzureAsync()
        {
            string azureTextFileContent = await shapeIndexCloudFile.DownloadTextAsync();

            string[] shapes = azureTextFileContent.Split(new char[] { ',' });

            foreach (string shape in shapes)
            {
                int i;

                Int32.TryParse(shape.ToString(), out i);

                ShapeFactory.instance.shapeHistoryList.Add(i);

                ShapeFactory.instance.CreateShape(i, true);

                await Task.Delay(500);
            }

            Gaze.instance.GazeEnabled = true;

            azureStatusText.text = "Load Complete!";
        }
    ```

7.  Enregistrez vos modifications dans Visual Studio avant de retourner à Unity.

## <a name="chapter-11---build-the-uwp-solution"></a>Chapitre 11 - générer la Solution UWP

Pour commencer le processus de génération :

1.  Accédez à **fichier > Paramètres de Build**.

    ![Générez l’application](images/AzureLabs-Lab5-54.png)

2.  Cliquez sur **Build**. Unity lancera un *Explorateur de fichiers* fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans. Créez ce dossier, puis nommez-le *application*. Ensuite avec le *application* dossier sélectionné, appuyez sur **sélectionner le dossier**.

3.  Unity commencera à générer votre projet pour le *application* dossier.

4.  Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un *Explorateur de fichiers* fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).

## <a name="chapter-12---deploying-your-application"></a>Chapitre 12 - déploiement de votre application

Pour déployer votre application :

1.  Accédez à la *application* dossier qui a été créé dans le [dernier chapitre](#chapter-11---build-the-uwp-solution). Vous verrez un fichier avec le nom de votre applications, avec l’extension de « .sln », vous devez double-cliquer sur, par conséquent, pour l’ouvrir dans *Visual Studio*.

2.  Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.

3.  Dans le **Configuration de la Solution** sélectionnez **déboguer**.

    > Pour le Microsoft HoloLens, il peut s’avérer plus facile d’affecter à ce *Machine distante*, de sorte que vous ne sont pas attachés à votre ordinateur. Cependant, vous devez également effectuer les opérations suivantes :
    > - Connaître le **adresse IP** de votre HoloLens, ce qui se trouve dans le *Paramètres > réseau & Internet > Wi-Fi > Options avancées*; IPv4 est l’adresse que vous devez utiliser. 
    > - Vérifiez **Mode développeur** est **sur**; trouvé dans *Paramètres > mise à jour & sécurité > pour les développeurs*.

    ![déployer la solution](images/AzureLabs-Lab5-55.png)

4.  Accédez à la **Build** menu et cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.

5.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancé et testé !

## <a name="your-finished-azure-functions-and-storage-application"></a>Votre Azure Functions terminé et votre Application de stockage

Félicitations, vous avez créé une application de réalité mixte qui tire parti des services Azure Functions et de stockage Azure. Votre application sera en mesure de dessiner sur les données stockées et de fournir une action basée sur ces données.

![produit final-fin](images/AzureLabs-Lab5-00.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Créer un deuxième spawn point et un enregistrement qui a qu'un objet a été créé à partir de spawn. Lorsque vous chargez le fichier de données, relire les formes généré de façon dynamique à partir de l’emplacement qu’ils ont été créés à l’origine.

### <a name="exercise-2"></a>Exercice 2

Créer une méthode pour redémarrer l’application, plutôt que de devoir rouvrez ce dernier chaque fois. **Chargement des scènes** est un bon endroit pour démarrer. Après cela, créez une méthode pour effacer la liste stockée dans *stockage Azure*, ce qui peut être facilement réinitialisé à partir de votre application. 
