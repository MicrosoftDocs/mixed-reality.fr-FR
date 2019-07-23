---
title: MR et Azure 308 - les notifications entre les périphériques
description: Terminer ce cours pour apprendre à implémenter Azure Notification Hubs, Azure Functions, stockage Azure et des Tables dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, notification, fonctions, tables, les concentrateurs de notification, vr immersives, hololens,
ms.openlocfilehash: 3b6e930acd81c7d6e3addc107ec0da605d38cad1
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694606"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-and-azure-308-cross-device-notifications"></a>MR et Azure 308 : Notifications entre les périphériques

![produit final-Démarrer](images/AzureLabs-Lab8-00.png)

Dans ce cours, vous allez apprendre à ajouter des fonctionnalités des concentrateurs de Notification à une application de réalité mixte à l’aide d’Azure Notification Hubs, les Tables Azure et Azure Functions.

**Azure Notification Hubs** est un service Microsoft, qui permet aux développeurs d’envoyer des notifications push ciblées et personnalisées à n’importe quelle plateforme, tout mise hors tension dans le cloud. Cela peut efficacement permettent aux développeurs de communiquer avec les utilisateurs finaux, ou même communiquer entre différentes applications, en fonction du scénario. Pour plus d’informations, visitez le **Azure Notification Hubs** [page](https://docs.microsoft.com/azure/notification-hubs/notification-hubs-push-notification-overview).

**Azure Functions** est un service Microsoft, ce qui permet aux développeurs d’exécuter de petits morceaux de code, « fonctions », dans Azure. Cela fournit un moyen permettant de déléguer le cloud, plutôt que votre application locale, ce qui peut avoir de nombreux avantages. **Azure Functions** prend en charge plusieurs langages de développement, y compris C\#, F\#, Node.js, Java et PHP. Pour plus d’informations, visitez le **Azure Functions** [page](https://docs.microsoft.com/azure/azure-functions/functions-overview).

**Les Tables Azure** est un service de cloud Microsoft, ce qui permet aux développeurs de stocker des données non structurées-SQL dans le cloud, qu’il soit facilement accessible n’importe où. Le service est doté d’une conception sans schéma, permettant ainsi l’évolution des tables en fonction des besoins et est donc très flexible. Pour plus d’informations, visitez le **Tables Azure** [page](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)

Avoir terminé ce cours, vous aurez une réalité mixte casque immersives et l’application un PC de bureau qui sera en mesure d’effectuer les opérations suivantes :

1. L’application de bureau PC permet à l’utilisateur de déplacer un objet dans l’espace 2D (X et Y), à l’aide de la souris.

2. Le déplacement des objets au sein de l’application de PC sera envoyé vers le cloud à l’aide de JSON, qui sera sous la forme d’une chaîne, qui contient un ID d’objet, type et transformer les informations (coordonnées X et Y). 

3. L’application de réalité mixte, ce qui a une scène identique à l’application de bureau, recevra les notifications concernant le déplacement d’objets, à partir du service de Notification Hubs (qui a simplement été mis à jour par l’application de PC de bureau). 

4. Lors de la réception d’une notification, qui contiendra l’ID d’objet, type et les informations de transformation, l’application de réalité mixte appliquera les informations reçues à son propre scène.

Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception. Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity. Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte. Ce cours est un didacticiel autonome, ce qui n’implique pas directement de tous les autres laboratoires réalité mixte.

## <a name="device-support"></a>Périphériques pris en charge

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 308 : Notifications entre les périphériques</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
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
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé
- Accès à Internet pour le programme d’installation Azure et d’accéder à des Hubs de Notification

## <a name="before-you-start"></a>Avant de commencer

- Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).
- Vous devez être le propriétaire de votre portail des développeurs Microsoft et votre portail de l’enregistrement d’Application, sinon vous ne devez pas autorisé à accéder à l’application dans [chapitre 2](#chapter-2---retrieve-your-new-apps-credentials).

## <a name="chapter-1---create-an-application-on-the-microsoft-developer-portal"></a>Chapitre 1 : créer une application sur le portail des développeurs Microsoft

Pour utiliser le **Azure Notification Hubs** Service, vous devez créer une Application sur le portail des développeurs Microsoft, comme votre application doivent être inscrites, afin qu’il peut envoyer et recevoir des notifications.

1.  Connectez-vous à la [portail des développeurs de Microsoft](https://developer.microsoft.com/dashboard).

    > Vous devez vous connecter à votre Account de Microsoft.

2.  Dans le tableau de bord, cliquez sur **créer une application**.

    ![Créer une application](images/AzureLabs-Lab8-01.png)

3.  Une fenêtre contextuelle s’affiche, dans laquelle vous devez réserver un nom pour votre nouvelle application. Dans la zone de texte, insérez un nom approprié ; Si le nom choisi est disponible, une coche s’affiche à droite de la zone de texte. Une fois que vous avez un nom disponible inséré, cliquez sur le **réserver le nom de produit** bouton vers le bas à gauche de la fenêtre contextuelle.

    ![un nom inverse](images/AzureLabs-Lab8-02.png)

4.  Avec l’application est maintenant créée, vous êtes prêt à passer au chapitre suivant.

## <a name="chapter-2---retrieve-your-new-apps-credentials"></a>Chapitre 2 - récupérer vos nouvelles informations d’identification des applications

Connectez-vous au portail de l’inscription d’Application, où votre nouvelle application sera répertorié et récupérer les informations d’identification qui seront utilisé pour le programme d’installation le **Service de Notification Hubs** au sein de la **Azure Portal**.

1.  Accédez à la [portail d’inscription des applications](http://apps.dev.microsoft.com).

    ![portail d’inscription des applications](images/AzureLabs-Lab8-03.png)

    > [!WARNING] 
    > Vous devez utiliser votre Account Microsoft pour se connecter.  
    > Cela **doit** Account Microsoft que vous avez utilisées dans la précédente [chapitre](#chapter-1---create-an-application-on-the-microsoft-developer-portal), avec le portail des développeurs de Store Windows.

2.  Vous trouverez votre application sous le **mes applications** section. Une fois que vous l’avez trouvé, cliquez dessus, vous êtes redirigé vers une nouvelle page qui possède l’application nom plu **inscription**.

    ![votre application nouvellement inscrite](images/AzureLabs-Lab8-04.png)

3.  Défilement vers le bas de la page d’inscription pour trouver votre **Secrets d’Application** section et la **SID du Package** pour votre application. Copiez les deux pour une utilisation avec la configuration de la **Azure Notification Hubs Service** dans le chapitre suivant.

    ![Secrets d’application](images/AzureLabs-Lab8-05.png)

## <a name="chapter-3---setup-azure-portal-create-notification-hubs-service"></a>Chapitre 3 - le programme d’installation portail : créer le Service de Notification Hubs

Avec vos informations d’identification des applications récupéré, vous devrez accéder au portail Azure, où vous allez créer un Service de concentrateurs de Notification Azure.

1.  Connectez-vous à la [Azure Portal](https://portal.azure.com).

    > [!NOTE] 
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez **Hub de Notification**, puis cliquez sur ***entrée***.

    ![Recherchez le hub de notification](images/AzureLabs-Lab8-06.png)

    > [!NOTE] 
    > Le mot ***New*** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.

3.  La nouvelle page doit fournir une description de la *Notification Hubs* service. En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.

    ![créer l’instance de hub de notification](images/AzureLabs-Lab8-07.png)

4.  Une fois que vous avez cliqué sur ***créer***:

    1.  Insérez votre nom souhaité pour cette instance de service.

    2.  Fournir un **espace de noms** dont vous pourrez plus l’associer à cette application.

    3.  Sélectionnez un **emplacement.**

    4.  Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal). 

    5.  Sélectionnez un **abonnement**.

    6.  Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.

    7. Sélectionnez **Créer**.

        ![Renseignez les détails du service](images/AzureLabs-Lab8-08.png)

5.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.

6.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![notification](images/AzureLabs-Lab8-09.png)

7.  Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. Vous serez dirigé vers votre nouvelle **Hub de Notification** instance de service.

    ![accéder à la ressource](images/AzureLabs-Lab8-10.png)
    
8.  Dans la page Vue d’ensemble, à mi-chemin dans la page, cliquez sur **Windows (WNS).** Le volet de droite changera aux champs de texte afficher deux, qui nécessitent votre **SID du Package** et **clé de sécurité**, à partir de l’application que vous avez configurés précédemment.

    ![qui vient d’être créé service hubs](images/AzureLabs-Lab8-11.png)

9. Une fois que vous avez copié les détails dans les champs appropriés, cliquez sur **enregistrer**, et vous recevrez une notification lorsque le Hub de Notification a été mis à jour avec succès.

    ![copier les détails de la sécurité](images/AzureLabs-Lab8-12.png)

## <a name="chapter-4---setup-azure-portal-create-table-service"></a>Chapitre 4 - le programme d’installation portail : créer le Service de Table

Après avoir créé votre instance de Service de Notification Hubs, accédez à votre portail Azure, où vous allez créer un Service de Tables Azure en créant une ressource de stockage.

1.  Si pas déjà connecté, connectez-vous à la [Azure Portal](https://portal.azure.com).

2.  Une fois connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez **compte de stockage**, puis cliquez sur **entrée**.

    > [!NOTE] 
    > Le mot ***New*** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.

3.  Sélectionnez **compte de stockage - blob, fichier, table, file d’attente** à partir de la liste.

    ![Recherchez le compte de stockage](images/AzureLabs-Lab8-13.png)

4.  La nouvelle page doit fournir une description de la **compte de stockage** service. En bas à gauche de cette invite, sélectionnez le **créer** bouton, pour créer une instance de ce service.

    ![créer l’instance de stockage](images/AzureLabs-Lab8-14.png)

5.  Une fois que vous avez cliqué sur **créer**, un panneau s’affiche :

    1. Insérez votre souhaitée **nom** pour cette instance de service (doit être en minuscules).

    2. Pour **modèle de déploiement**, cliquez sur **Resource manager**.

    3.  Pour **type de compte**, à l’aide de la liste déroulante, sélectionnez **stockage (usage général v1)** .

    4. Sélectionnez un **emplacement**.
    
    5.  Pour le **réplication** menu déroulant, sélectionnez **en lecture-access-geo-redundant storage (RA-GRS)** .

    6.  Pour **performances**, cliquez sur **Standard**.

    7.  Dans le **transfert sécurisé requis** section, sélectionnez **désactivé**.

    8.  À partir de la **abonnement** menu déroulant, sélectionnez un abonnement approprié.

    9.  Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    10. Laissez **réseaux virtuels** comme **désactivé** s’il s’agit d’une option pour vous.

    11. Cliquez sur **Créer**.

        ![Renseignez les détails de stockage](images/AzureLabs-Lab8-15.png)

6.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.

7.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail. Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.

    ![nouvelle notification de stockage](images/AzureLabs-Lab8-16.png)

8.  Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. Vous êtes redirigé vers votre nouvelle page de vue d’ensemble instance de Service de stockage.

    ![accéder à la ressource](images/AzureLabs-Lab8-17.PNG)

9. Dans la page Vue d’ensemble, à droite, cliquez sur **Tables**.
    
    ![](images/AzureLabs-Lab8-18.PNG)

10. Le volet de droite change et indique le **service de Table** plus d’informations, dans laquelle vous devez ajouter une nouvelle table. Cela en cliquant sur le **+** **Table** bouton vers le coin supérieur gauche.

    ![ouvrir des Tables](images/AzureLabs-Lab8-19.png)

11. Une nouvelle page s’affiche, dans laquelle vous devez entrer un **nom de la Table**. Il s’agit du nom que vous utiliserez pour faire référence aux données dans votre application dans les chapitres. Insérez un nom approprié et cliquez sur **OK**.

    ![Créer la nouvelle table](images/AzureLabs-Lab8-20.png)    

12. Une fois que la nouvelle table a été créée, vous serez en mesure de voir dans le **service de Table** page (en bas).

    ![nouvelle table créée](images/AzureLabs-Lab8-21.png)
    

## <a name="chapter-5---completing-the-azure-table-in-visual-studio"></a>Chapitre 5 - fin de la Table Azure dans Visual Studio

Maintenant que votre **service de Table** compte de stockage a été configuré, il est temps d’ajouter des données, qui sera utilisé pour stocker et récupérer des informations. La modification de vos Tables peut être effectuée via **Visual Studio**.

1.  Ouvrez **Visual Studio**.

2.  Dans le menu, cliquez sur **vue** > **Cloud Explorer**.

    ![Ouvrez cloud explorer](images/AzureLabs-Lab8-22.png)

3.  Le **Cloud Explorer** s’ouvre comme un élément ancré (patient, comme le chargement peut prendre un temps).

    > [!NOTE] 
    > Si l’abonnement que vous avez utilisé pour créer votre *comptes de stockage* n’est pas visible, assurez-vous d’avoir : 
    > - Ouvert une session le même compte que celui utilisé pour le portail Azure.
    > - Sélectionné de votre abonnement à partir de la Page de gestion de compte (vous devrez peut-être appliquer un filtre à partir de vos paramètres de compte) :  
    >
    >   ![trouver un abonnement](images/AzureLabs-Lab8-22-5.png)

4.  Vos services cloud Azure seront affichera. Rechercher **comptes de stockage** et cliquez sur la flèche à gauche de cette option pour développer vos comptes.

    ![ouvrir des comptes de stockage](images/AzureLabs-Lab8-23.png)

5.  Une fois développé, vous avez récemment créé **compte de stockage** doit être disponible. Cliquez sur la flèche à gauche de votre stockage et recherchez une fois qui est développé, **Tables** et cliquez sur la flèche à côté de cela, pour faire apparaître le **Table** vous avez créé dans le dernier chapitre. Double-cliquez sur votre **Table**.

    ![Ouvrez le tableau d’objets de scène](images/AzureLabs-Lab8-24.png)

6.  Votre table sera ouvert dans le centre de la fenêtre Visual Studio. Cliquez sur l’icône de table avec la **+** (plus) sur celui-ci.

    ![Ajouter une nouvelle table](images/AzureLabs-Lab8-25.png)

7.  Une fenêtre s’affiche invite pour pouvoir *ajouter une entité*. Vous allez créer trois entités au total, chacune avec plusieurs propriétés. Vous remarquerez que *PartitionKey* et *RowKey* sont déjà fournies, car elles sont utilisées par la table à rechercher vos données. 

    ![clé de partition et de ligne](images/AzureLabs-Lab8-26.png)

8. Mise à jour le *valeur* de la **PartitionKey** et **RowKey** comme suit (n’oubliez pas d’effectuer cette opération pour chaque propriété de ligne que vous ajoutez, cependant incrémenter l’attribut RowKey chaque fois) :

    ![ajouter des valeurs correctes](images/AzureLabs-Lab8-26-5.png)

9.  Cliquez sur **ajouter une propriété** pour ajouter des lignes de données supplémentaires. Faites votre premier tableau vide correspondre le tableau ci-dessous.

10. Cliquez sur **OK** lorsque vous avez terminé.

    ![Cliquez sur OK lorsque vous avez terminé](images/AzureLabs-Lab8-27.png)

    > [!WARNING] 
    > Vérifiez que vous avez modifié le **Type** de la **X**, **Y**, et **Z**, entrées à **Double**. 

11. Vous remarquerez que votre table a maintenant une ligne de données. Cliquez sur le **+** (icône à nouveau pour ajouter une autre entité plus).

    ![première ligne](images/AzureLabs-Lab8-27-5.png)

12. Créez une propriété supplémentaire et puis définissez les valeurs de la nouvelle entité pour correspondre à celles présentées ci-dessous.

    ![ajouter le cube](images/AzureLabs-Lab8-28.png)

13. Répétez la dernière étape pour ajouter une autre entité. Définissez les valeurs pour cette entité à celles présentées ci-dessous.

    ![Ajouter cylindre](images/AzureLabs-Lab8-29.png)

14. Votre table doit maintenant ressembler à celui ci-dessous.

    ![table complète](images/AzureLabs-Lab8-30.png)

15. Vous avez terminé ce chapitre. Veillez à enregistrer.

## <a name="chapter-6---create-an-azure-function-app"></a>Chapitre 6 : créer une application de fonction Azure

Créer une application de fonction Azure qui sera appelée par l’application de bureau pour mettre à jour le **Table** servir et envoyer une notification via le **Hub de Notification**.

Vous devez tout d’abord, créez un fichier qui permettra à votre fonction Azure charger les bibliothèques que vous avez besoin.

1.  Ouvrez **le bloc-notes** (appuyez sur Windows et tapez notepad).

    ![Ouvrez le bloc-notes](images/AzureLabs-Lab8-31.png)

2.  Avec le bloc-notes ouvert, insérer la structure JSON ci-dessous. Une fois que vous avez terminé, enregistrez-le sur votre bureau en tant que **project.json**. Il est important que l’attribution de noms est correcte : faire en sorte qu’il cas **n’a pas un .txt** extension de fichier. Ce fichier définit les bibliothèques de que votre fonction utilisera, si vous avez utilisé NuGet, il doit vous paraître familier.

    ```json
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "WindowsAzure.Storage": "7.0.0",
            "Microsoft.Azure.NotificationHubs" : "1.0.9",
            "Microsoft.Azure.WebJobs.Extensions.NotificationHubs" :"1.1.0"
        }
        }
    }
    }
    ```

3.  Connectez-vous à la [Azure Portal](https://portal.azure.com).

4.  Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez **Function App**, appuyez sur **entrée**.

    ![recherche de l’application de fonction](images/AzureLabs-Lab8-32.png)

    > [!NOTE] 
    > Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.

5.  La nouvelle page doit fournir une description de la **Function App** service. En bas à gauche de cette invite, sélectionnez le **créer** bouton permettant de créer une association avec ce service.

    ![instance d’application (fonction)](images/AzureLabs-Lab8-33.png)

6.  Une fois que vous avez cliqué sur **créer**, renseignez les valeurs suivantes :

    1. Pour **nom de l’application**, insérez votre nom souhaité pour cette instance de service.

    2. Sélectionnez un **abonnement**.

    3. Sélectionnez le niveau de tarification approprié pour vous, si c’est la première heure de création d’un **Service Function App**, un niveau gratuit doit être disponible pour vous.

    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. Pour **système d’exploitation**, cliquez sur Windows, car il s’agit de la plateforme.

    6. Sélectionnez un **Plan d’hébergement** (à l’aide de ce didacticiel est un **Plan de consommation**.

    7. Sélectionnez un **emplacement** **(choisissez le même emplacement que le stockage que vous avez créé à l’étape précédente)**

    8. Pour le **stockage** section, **vous devez sélectionner le Service de stockage que vous avez créé à l’étape précédente**.

    9. Vous n’aurez pas *Application Insights* dans cette application, par conséquent, n’hésitez pas à laisser **hors**.

    10. Cliquez sur **Créer**.

        ![créer la nouvelle instance](images/AzureLabs-Lab8-34.png)

7.  Une fois que vous avez cliqué sur **créer** avoir à attendre que le service doit être créé, cette opération peut prendre une minute.

8.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![nouvelle notification](images/AzureLabs-Lab8-35.png)

9.  Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.

10. Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. 

    ![accéder à la ressource](images/AzureLabs-Lab8-36.png)

11. Cliquez sur le **+** (plus) de l’icône située à côté *fonctions*à *créer un nouveau*.

    ![ajouter la nouvelle fonction](images/AzureLabs-Lab8-37.png)

12. Dans le volet central, le **fonction** fenêtre de création s’affiche. Ignorer les informations contenues dans la partie supérieure du panneau, puis cliquez sur **fonction personnalisée**, qui se trouve près du bas (dans la zone bleue, comme indiqué ci-dessous).

    ![fonction personnalisée](images/AzureLabs-Lab8-38.png)

13. La nouvelle page au sein de la fenêtre affiche différents types de fonction. Défiler vers le bas pour afficher les types violet, puis cliquez sur **HTTP PUT** élément.

    ![HTTP put de lien](images/AzureLabs-Lab8-39.png)

    > [!IMPORTANT]
    > Vous devrez peut-être faire défiler vers le bas la page (et cette image soit exactement la même, si les mises à jour du portail Azure ont eu lieu), toutefois, que vous recherchez un élément appelé *HTTP PUT*.

14. Le **HTTP PUT** fenêtre s’affiche, où vous devez configurer la fonction (voir image ci-dessous).

    1.  Pour **Language,** à l’aide de la liste déroulante, sélectionnez C\#.

    2.  Pour **nom,** d’entrée d’un nom approprié.

    3.  Dans le **niveau d’authentification** menu déroulant, sélectionnez **fonction**.

    4.  Pour le **nom de la Table** section, vous devez utiliser le nom exact que vous avez utilisé pour créer votre **Table** service (y compris la même casse).

    5.  Dans le **connexion au compte de stockage** section, utilisez le menu déroulant et sélectionnez votre compte de stockage à partir de là. Si elle n’est pas là, cliquez sur le **New** lien hypertexte en même temps que le titre de section pour afficher un autre panneau, où votre compte de stockage doit être répertorié.

        ![nouveau stockage](images/AzureLabs-Lab8-40.png)

15. Cliquez sur **créer** et vous recevrez une notification que vos paramètres ont été mis à jour avec succès.

    ![créer (fonction)](images/AzureLabs-Lab8-41.png)

16. Après avoir cliqué sur **créer**, vous serez redirigé vers l’éditeur de fonction.

    ![mettre à jour le code de fonction](images/AzureLabs-Lab8-42.png)

17. Insérez le code suivant dans l’éditeur (fonction) (en remplaçant le code dans la fonction) :

    ```csharp
    #r "Microsoft.WindowsAzure.Storage"

    using System;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Table;
    using Microsoft.Azure.NotificationHubs;
    using Newtonsoft.Json;

    public static async Task Run(UnityGameObject gameObj, CloudTable table, IAsyncCollector<Notification> notification, TraceWriter log)
    {
        //RowKey of the table object to be changed
        string rowKey = gameObj.RowKey;

        //Retrieve the table object by its RowKey
        TableOperation operation = TableOperation.Retrieve<UnityGameObject>("UnityPartitionKey", rowKey); 

        TableResult result = table.Execute(operation);

        //Create a UnityGameObject so to set its parameters
        UnityGameObject existingGameObj = (UnityGameObject)result.Result; 

        existingGameObj.RowKey = rowKey;
        existingGameObj.X = gameObj.X;
        existingGameObj.Y = gameObj.Y;
        existingGameObj.Z = gameObj.Z;

        //Replace the table appropriate table Entity with the value of the UnityGameObject
        operation = TableOperation.Replace(existingGameObj); 

        table.Execute(operation);

        log.Verbose($"Updated object position");

        //Serialize the UnityGameObject
        string wnsNotificationPayload = JsonConvert.SerializeObject(existingGameObj);
        
        log.Info($"{wnsNotificationPayload}");

        var headers = new Dictionary<string, string>();

        headers["X-WNS-Type"] = @"wns/raw";

        //Send the raw notification to subscribed devices
        await notification.AddAsync(new WindowsNotification(wnsNotificationPayload, headers)); 

        log.Verbose($"Sent notification");
    }

    // This UnityGameObject represent a Table Entity
    public class UnityGameObject : TableEntity
    {
        public string Type { get; set; }
        public double X { get; set; }
        public double Y { get; set; }
        public double Z { get; set; }
        public string RowKey { get; set; }
    }
    ```

    > [!NOTE]
    > Grâce aux bibliothèques inclus, la fonction reçoit le nom et l’emplacement de l’objet qui a été déplacé dans la scène Unity (comme un C# objet, appelé **UnityGameObject**). Cet objet est ensuite utilisé pour mettre à jour les paramètres de l’objet dans la table créée. Ensuite, la fonction effectue un appel à votre service de Notification Hub créé, qui avertit les applications de tous les abonnés.

18. Le code en place, cliquez sur **enregistrer**.

19. Ensuite, cliquez sur le **\<** icône (flèche), sur le côté droit de la page.

    ![chargement ouvrir le panneau de configuration](images/AzureLabs-Lab8-43.png)

20. Un glisser en partant de la droite. Dans ce panneau, cliquez sur **télécharger**, et un Explorateur de fichiers s’affiche.

21. Accédez à, puis cliquez sur, la **project.json** fichier que vous avez créé dans **le bloc-notes** précédemment, puis cliquez sur le **Open** bouton. Ce fichier définit les bibliothèques utilisées par votre fonction.

    ![Télécharger json](images/AzureLabs-Lab8-44.png)

22. Quand le fichier a été chargé, il apparaît dans le volet de droite. En cliquant sur il s’ouvre dans le **fonction** éditeur. Il doit rechercher **exactement** identique à l’image suivante (sous l’étape 23).

23. Ensuite, dans le volet gauche, sous **fonctions**, cliquez sur le **intégrer** lien.

    ![intégrer (fonction)](images/AzureLabs-Lab8-45.png)

24. Dans la page suivante, dans l’angle supérieur droit, cliquez sur **éditeur avancé** (comme ci-dessous).

    ![ouvrir l’éditeur avancé](images/AzureLabs-Lab8-46.png)

25. Un **function.json** fichier sera ouvert dans le panneau central, ce qui doit être remplacé par l’extrait de code suivant. Définit la fonction que vous générez et les paramètres transmis à la fonction.

    ```json
    {
    "bindings": [
        {
        "authLevel": "function",
        "type": "httpTrigger",
        "methods": [
            "get",
            "post"
        ],
        "name": "gameObj",
        "direction": "in"
        },
        {
        "type": "table",
        "name": "table",
        "tableName": "SceneObjectsTable",
        "connection": "mrnothubstorage_STORAGE",
        "direction": "in"
        },
        {
        "type": "notificationHub",
        "direction": "out",
        "name": "notification",
        "hubName": "MR_NotHub_ServiceInstance",
        "connection": "MRNotHubNS_DefaultFullSharedAccessSignature_NH",
        "platform": "wns"
        }
    ]
    }
    ```

26. Votre éditeur doit maintenant ressembler à l’image ci-dessous :

    ![Revenez à l’éditeur standard](images/AzureLabs-Lab8-47.png)

27. Vous pouvez remarquer les paramètres d’entrée que vous venez d’insérer les détails de votre table et de stockage ne peuvent pas correspondre et par conséquent doit être mis à jour avec vos informations. **Ne le faites pas ici**, car il est couvert ensuite. Cliquez simplement sur le **éditeur Standard** lien, dans l’angle supérieur droit de la page, pour revenir en arrière.

28. Dans le **éditeur Standard**, cliquez sur **Azure Table Storage (table)** , sous **entrées**. 
    
    ![Entrées de table](images/AzureLabs-Lab8-47-5.png)

29. Garantir la correspondance suivante à **votre** plus d’informations, car ils peuvent être différents (une image se trouve ci-dessous les étapes suivantes) :

    1.  **Nom de la table**: le nom de la table que vous avez créé dans votre stockage Azure, le service de Tables.

    2.  **Connexion au compte de stockage :** cliquez sur **nouveau**, qui s’affiche en même temps que le menu déroulant et un panneau s’affiche à droite de la fenêtre.

        ![nouveau stockage](images/AzureLabs-Lab8-48.png)

        1.  Sélectionnez votre **compte de stockage**, que vous avez créé précédemment pour héberger le **applications de fonction.**

        2. Vous remarquerez que le **compte de stockage** valeur de la connexion a été créée.

        3. Veillez à appuyer sur **enregistrer** une fois que vous avez terminé.

    3.  Le **entrées** page doit maintenant correspondre à l’affichage ci-dessous, **votre** plus d’informations.

        ![entrées terminée](images/AzureLabs-Lab8-49.png)

30. Ensuite, cliquez sur **Azure Notification Hub (notification)** : sous **sorties**. Vérifiez les éléments suivants sont mis en correspondance avec **votre** plus d’informations, car ils peuvent être différents (une image se trouve ci-dessous les étapes suivantes) :

    1.  **Nom du Hub de notification**: il s’agit du nom de votre **Hub de Notification** instance de service, vous avez créé précédemment.

    2.  **Connexion d’espace de noms notification Hubs**: cliquez sur **nouveau**, qui s’affiche en même temps que le menu déroulant.

        ![Vérifiez les sorties](images/AzureLabs-Lab8-50.png)

    3. Le **connexion** fenêtre contextuelle s’affiche (voir l’image ci-dessous), où vous devez sélectionner le **Namespace** de la **Hub de Notification**, que vous avez configuré précédemment.

    4. Sélectionnez votre **Hub de Notification** nom dans le menu déroulant du milieu.

    5.  Définir le **stratégie** menu déroulant à **DefaultFullSharedAccessSignature**.

    6. Cliquez sur le **sélectionnez** bouton revenir en arrière.

        ![mise à jour de la sortie](images/AzureLabs-Lab8-51.png)

31.  Le **sorties** page doit maintenant correspondre à la ci-dessous, mais avec **votre** informations à la place. Veillez à appuyer sur **enregistrer**.

> [!WARNING]
> *Ne pas modifier directement le nom du Hub de Notification* (cela doit-elle tous être effectuée à l’aide de la **éditeur avancé**, à condition que vous avez suivi les étapes précédentes correctement.

![sorties terminée](images/AzureLabs-Lab8-50.png)

32. À ce stade, vous devez tester la fonction, pour vous assurer qu’il fonctionne. Pour cela, procédez comme suit : 

    1. Accédez à la page de la fonction une fois de plus :

        ![sorties terminée](images/AzureLabs-Lab8-50-1.png)

    2. Dans la page de la fonction, cliquez sur le **Test** onglet à l’extrémité droite de la page, pour ouvrir le *Test* panneau :

        ![sorties terminée](images/AzureLabs-Lab8-50-2.png)

    3. Dans le **corps de la demande** zone de texte du panneau, collez le code ci-dessous :

        ```
        {  
            "Type":null,
            "X":3,
            "Y":0,
            "Z":1,
            "PartitionKey":null,
            "RowKey":"Obj2",
            "Timestamp":"0001-01-01T00:00:00+00:00",
            "ETag":null
        }
        ```

    4. Avec le code de test en place, cliquez sur le **exécuter** situé en bas à droite et le test sera exécuté. Les journaux de sortie du test seront affiche dans la zone de la console, sous votre code de fonction.

        ![sorties terminée](images/AzureLabs-Lab8-50-3.png)

    > [!WARNING]
    > Si le test ci-dessus échoue, vous devez vérifier que vous avez suivi les étapes ci-dessus en exactement, en particulier les paramètres dans le **intégrer panneau**. 

## <a name="chapter-7---set-up-desktop-unity-project"></a>Chapitre 7 - configuration de projet Unity de bureau

> [!IMPORTANT]
> L’application de bureau que vous créez, **ne sera pas** Professionnel dans l’éditeur Unity. Il doit être exécuté en dehors de l’éditeur, suivant la création de l’application, à l’aide de Visual Studio (ou l’application déployée). 

Ce qui suit est un standard configurée pour le développement avec Unity et de réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

Configurer et tester votre casque immersives de réalité mixte.

> [!NOTE] 
> Vous allez **pas** nécessitent des contrôleurs de mouvement pour ce cours. Si vous avez besoin de prendre en charge de paramétrage le casque immersif, veuillez suivre ce [lien sur la façon de configurer Windows Mixed Reality](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).

1.  Ouvrez **Unity** et cliquez sur **New**.

    ![nouveau projet unity](images/AzureLabs-Lab8-52.png)

2.  Vous devez fournir un nom de projet Unity, insérez **UnityDesktopNotifHub**. Assurez-vous que le type de projet est défini sur **3D**. Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![créer le projet](images/AzureLabs-Lab8-53.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **modifier** > **préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![ensemble des outils externes Visual Studio](images/AzureLabs-Lab8-54.png)

4.  Ensuite, accédez à **fichier** > **paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation**bouton pour appliquer votre sélection.

    ![changer de plate-forme](images/AzureLabs-Lab8-55.png)

5.  Lorsque vous êtes toujours dans **fichier** > **paramètres de Build**, assurez-vous que :

    1.  **Équipement cible** a la valeur **n’importe quel appareil**

        > Cette Application sera pour votre bureau, doivent donc être **n’importe quel appareil**

    2.  **Type de build** a la valeur **D3D**

    3.  **Kit de développement logiciel** a la valeur **dernière installé**

    4.  **Version de Visual Studio** a la valeur **dernière installé**

    5.  **Générez et exécutez** est défini sur **ordinateur Local**

    6.  Cet emplacement, il est important de l’enregistrement de la scène et en l’ajoutant à la build.

        1. Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.

            ![ajouter des scènes ouverts](images/AzureLabs-Lab8-56.png)

        2. Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![nouveau dossier de scènes](images/AzureLabs-Lab8-57.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le **nom de fichier :** champ de texte, tapez **NH\_Desktop\_scène**, puis appuyez sur **Enregistrer**.

            ![nouvelle NH_Desktop_Scene](images/AzureLabs-Lab8-58.png)

    7.  Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.

6.  Dans la même fenêtre, cliquez sur le **paramètres du lecteur** bouton, le panneau de configuration associée s’ouvre dans l’espace où le **inspecteur** se trouve.

7.  Dans ce panneau, quelques paramètres doivent être vérifiées :

    1.  Dans le **autres paramètres** onglet :

        1.  **Version du Runtime de script** doit être **expérimental (équivalent .NET 4.6)**

        2. **Script principal** doit être **.NET**

        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**

            ![version de net 4.6](images/AzureLabs-Lab8-59.png)

    2.  Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        - **InternetClient**

            ![client internet de graduation](images/AzureLabs-Lab8-60.png)

8.  Dans **paramètres de Build** *Unity C\# projets* est n’est plus grisée ; Cochez la case à cocher en regard de cela.

9.  Fermer le **paramètres de Build** fenêtre.

10. Enregistrer votre projet et scène **fichier** > **enregistrer la scène / fichier** > **enregistrer le projet**.

    > [!IMPORTANT]
    > Si vous souhaitez ignorer la *Unity configurer* composant pour ce projet (application de bureau) et toujours directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-Desktop.unitypackage), importez-le dans votre projet en tant qu’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).  Vous devrez toujours ajouter les composants de script.

## <a name="chapter-8---importing-the-dlls-in-unity"></a>Chapitre 8 - importation des DLL dans Unity

Vous allez utiliser Azure Storage pour Unity (qui, elle s’appuie sur le kit SDK Azure .net). Pour plus d’informations suivre ce [lien sur Azure Storage pour Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).

Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation. Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.

Pour importer le SDK dans votre propre projet, assurez-vous que vous avez téléchargé la dernière version [ **.unitypackage** ](https://aka.ms/azstorage-unitysdk) à partir de GitHub. Ensuite, procédez comme suit :

1.  Ajouter le **.unitypackage** à Unity à l’aide de la **actifs \> importer un Package \> Package personnalisé** option de menu.

2.  Dans le **importer un Package Unity** zone s’affiche, vous pouvez sélectionner tous les éléments sous **plug-in**\>**stockage**.  Désactivez tout le reste, qu’il n’est pas nécessaire pour ce cours.

    ![importer dans le package](images/AzureLabs-Lab8-61.png)

3.  Cliquez sur le ***importation*** pour ajouter les éléments à votre projet.

4.  Accédez à la **stockage** dossier sous **plug-ins** dans le projet afficher, puis sélectionnez les plug-ins suivants *uniquement*:

    -   Microsoft.Data.Edm
    -   Microsoft.Data.OData
    -   Microsoft.WindowsAzure.Storage
    -   Newtonsoft.Json
    -   System.Spatial

![Décochez la case n’importe quelle plateforme](images/AzureLabs-Lab8-62.png)

5.  Avec *ces plug-ins spécifiques* sélectionné, **Décochez** **plateforme Any** et **Décochez** **WSAPlayer** puis cliquez sur **appliquer**.

    ![appliquer des DLL de plateforme](images/AzureLabs-Lab8-63.png)

    > [!NOTE] 
    > Nous allons marquer ces plug-ins particuliers à utiliser uniquement dans l’éditeur Unity. Il s’agit, car il existe différentes versions des mêmes plug-ins dans le dossier WSA qui sera utilisé après que le projet est exporté à partir d’Unity.

6.  Dans le **stockage** dossier de plug-in, sélectionnez uniquement :

    -   Microsoft.Data.Services.Client

        ![jeu de ne pas traiter les DLL](images/AzureLabs-Lab8-64.png)

7.  Vérifier le **processus ne** sous **paramètres de plateforme** et cliquez sur ***appliquer***.

    ![n’appliquer aucun traitement](images/AzureLabs-Lab8-65.png)

    > [!NOTE] 
    > Nous sommes marquage ce plug-in « Ne pas traiter les », car l’utilitaire de correction Unity assembly a des difficultés à traiter ce plug-in. Le plug-in continue de fonctionner même si elle n’est pas traitée.

## <a name="chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project"></a>Chapitre 9 - créer la classe TableToScene dans le projet Unity de bureau

Vous devez maintenant créer les scripts qui contient le code pour exécuter cette application.

Le premier script que vous créez est **TableToScene**, qui est chargé de :

-   Lecture d’entités dans le stockage Table Azure.
-   À l’aide de données de la Table, de déterminer les objets à générer et à quelle position.

Le deuxième script que vous créez est **CloudScene**, qui est chargé de :

-   Enregistrement de l’événement de clic gauche, pour autoriser l’utilisateur à faire glisser des objets autour de la scène.
-   Sérialiser les données d’objet à partir de cette scène Unity et de les envoyer à l’application de fonction Azure.

Pour créer cette classe :

1.  Avec le bouton droit dans le **Asset** dossier se trouve dans le volet de projet, **créer** > **dossier**. Nommez le dossier **Scripts**.

    ![créer le dossier de scripts](images/AzureLabs-Lab8-66.png)

    ![créer le dossier scripts 2](images/AzureLabs-Lab8-67.png)

2.  Double-cliquez sur le dossier venez de créer, pour l’ouvrir.

3.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**  >   **C# Script**. Nommez le script **TableToScene**.

    ![script c#](images/AzureLabs-Lab8-68.png)
    ![TableToScene le changement de nom](images/AzureLabs-Lab8-69.png)

4.  Double-cliquez sur le script pour l’ouvrir dans Visual Studio 2017.

5.  Ajoutez les espaces de noms suivants :

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    using UnityEngine;
    ```

6.  Dans la classe, insérez les variables suivantes :

    ```csharp
        /// <summary>    
        /// allows this class to behave like a singleton
        /// </summary>    
        public static TableToScene instance;

        /// <summary>    
        /// Insert here you Azure Storage name     
        /// </summary>    
        private string accountName = " -- Insert your Azure Storage name -- ";

        /// <summary>    
        /// Insert here you Azure Storage key    
        /// </summary>    
        private string accountKey = " -- Insert your Azure Storage key -- ";
    ```
    
    > [!NOTE] 
    > Remplacez le **accountName** valeur avec le nom de votre Service de stockage Azure et **accountKey** valeur avec la valeur de clé trouvée dans le Service de stockage Azure, dans le portail Azure (voir Image ci-dessous). 
    >
    > ![clé de compte d’extraction](images/AzureLabs-Lab8-70.png)

7.  Ajoutez maintenant le **Start()** et **Awake()** méthodes pour initialiser la classe.

    ```csharp
        /// <summary>
        /// Triggers before initialization
        /// </summary>
        void Awake()
        {
            // static instance of this class
            instance = this;
        }

        /// <summary>
        /// Use this for initialization
        /// </summary>
        void Start()
        {  
            // Call method to populate the scene with new objects as 
            // pecified in the Azure Table
            PopulateSceneFromTableAsync();
        }
    ```

8.  Dans le **TableToScene** de classe, ajoutez la méthode qui Récupère les valeurs à partir de la Table Azure et les utiliser pour générer dynamiquement les primitives appropriés dans la scène.

    ```csharp
        /// <summary>    
        /// Populate the scene with new objects as specified in the Azure Table    
        /// </summary>    
        private async void PopulateSceneFromTableAsync()
        {
            // Obtain credentials for the Azure Storage
            StorageCredentials creds = new StorageCredentials(accountName, accountKey);

            // Storage account
            CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
            
            // Storage client
            CloudTableClient client = account.CreateCloudTableClient(); 
            
            // Table reference
            CloudTable table = client.GetTableReference("SceneObjectsTable");

            TableContinuationToken token = null;

            // Query the table for every existing Entity
            do
            {
                // Queries the whole table by breaking it into segments
                // (would happen only if the table had huge number of Entities)
                TableQuerySegment<AzureTableEntity> queryResult = await table.ExecuteQuerySegmentedAsync(new TableQuery<AzureTableEntity>(), token); 

                foreach (AzureTableEntity entity in queryResult.Results)
                {
                    GameObject newSceneGameObject = null;
                    Color newColor;

                    // check for the Entity Type and spawn in the scene the appropriate Primitive
                    switch (entity.Type)
                    {
                        case "Cube":
                            // Create a Cube in the scene
                            newSceneGameObject = GameObject.CreatePrimitive(PrimitiveType.Cube);
                            newColor = Color.blue;
                            break;

                        case "Sphere":
                            // Create a Sphere in the scene
                            newSceneGameObject = GameObject.CreatePrimitive(PrimitiveType.Sphere);
                            newColor = Color.red;
                            break;

                        case "Cylinder":
                            // Create a Cylinder in the scene
                            newSceneGameObject = GameObject.CreatePrimitive(PrimitiveType.Cylinder);
                            newColor = Color.yellow;
                            break;
                        default:
                            newColor = Color.white;
                            break;
                    }

                    newSceneGameObject.name = entity.RowKey;

                    newSceneGameObject.GetComponent<MeshRenderer>().material = new Material(Shader.Find("Diffuse"))
                    {
                        color = newColor
                    };

                    //check for the Entity X,Y,Z and move the Primitive at those coordinates
                    newSceneGameObject.transform.position = new Vector3((float)entity.X, (float)entity.Y, (float)entity.Z);
                }

                // if the token is null, it means there are no more segments left to query
                token = queryResult.ContinuationToken;
            }

            while (token != null);
        }
    ```

9.  En dehors du **TableToScene** (classe), vous devez définir la classe utilisée par l’application pour sérialiser et désérialiser les **entités de Table**.

    ```csharp
        /// <summary>
        /// This objects is used to serialize and deserialize the Azure Table Entity
        /// </summary>
        [System.Serializable]
        public class AzureTableEntity : TableEntity
        {
            public AzureTableEntity(string partitionKey, string rowKey)
                : base(partitionKey, rowKey) { }

            public AzureTableEntity() { }
            public string Type { get; set; }
            public double X { get; set; }
            public double Y { get; set; }
            public double Z { get; set; }
        }
    ```

10. Assurez-vous que vous **enregistrer** avant de revenir à l’éditeur Unity.

11. Cliquez sur le **Main Camera** à partir de la **hiérarchie** panneau, afin que ses propriétés s’affichent dans le **inspecteur**.

12. Avec le **Scripts** dossier ouvert, sélectionnez le script **TableToScene fichier** et faites-le glisser sur le **Main Camera**. Le résultat doit être comme suit :

    ![Ajouter un script à la caméra principale](images/AzureLabs-Lab8-71.png)

## <a name="chapter-10---create-the-cloudscene-class-in-the-desktop-unity-project"></a>Chapitre 10 - créer la classe CloudScene dans le projet Unity de bureau

Le deuxième script que vous créez est **CloudScene**, qui est chargé de :

-   Enregistrement de l’événement de clic gauche, pour autoriser l’utilisateur à faire glisser des objets autour de la scène.

-   Sérialiser les données d’objet à partir de cette scène Unity et de les envoyer à l’application de fonction Azure.

Pour créer le deuxième script :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**, **C\# Script**. Nommez le script **CloudScene**
    
    ![script c#](images/AzureLabs-Lab8-72.png)
    ![renommer CloudScene](images/AzureLabs-Lab8-73.png)

2.  Ajoutez les espaces de noms suivants :

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Text;
    using System.Threading.Tasks;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

3.  Insérez les variables suivantes :

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static CloudScene instance;

        /// <summary>
        /// Insert here you Azure Function Url
        /// </summary>
        private string azureFunctionEndpoint = "--Insert here you Azure Function Endpoint--";

        /// <summary>
        /// Flag for object being moved
        /// </summary>
        private bool gameObjHasMoved;

        /// <summary>
        /// Transform of the object being dragged by the mouse
        /// </summary>
        private Transform gameObjHeld;

        /// <summary>
        /// Class hosted in the TableToScene script
        /// </summary>
        private AzureTableEntity azureTableEntity;
    ```

4.  Remplacez le **azureFunctionEndpoint** valeur avec votre URL d’application de fonction Azure trouvée dans le Service d’application de fonction Azure, dans le portail Azure, comme illustré dans l’image ci-dessous :

    ![obtenir l’URL de la fonction](images/AzureLabs-Lab8-74.png)

5.  Ajoutez maintenant le **Start()** et **Awake()** méthodes pour initialiser la classe.

    ```csharp
        /// <summary>
        /// Triggers before initialization
        /// </summary>
        void Awake()
        {
            // static instance of this class
            instance = this;
        }

        /// <summary>
        /// Use this for initialization
        /// </summary>
        void Start()
        {
            // initialise an AzureTableEntity
            azureTableEntity = new AzureTableEntity();
        }
    ```

6.  Dans le **Update()** (méthode), ajoutez le code suivant qui détecte l’entrée de la souris et faites glisser, qui à son tour déplacera GameObjects dans la scène. Si l’utilisateur a glisser -déplacer un objet, il transmet le nom et les coordonnées de l’objet à la méthode **UpdateCloudScene()** , qui appelle le service d’application Azure Function App, qui met à jour la table Azure et le déclencheur le notification.

    ```csharp
        /// <summary>
        /// Update is called once per frame
        /// </summary>
        void Update()
        {
            //Enable Drag if button is held down
            if (Input.GetMouseButton(0))
            {
                // Get the mouse position
                Vector3 mousePosition = new Vector3(Input.mousePosition.x, Input.mousePosition.y, 10);

                Vector3 objPos = Camera.main.ScreenToWorldPoint(mousePosition);

                Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);

                RaycastHit hit;

                // Raycast from the current mouse position to the object overlapped by the mouse
                if (Physics.Raycast(ray, out hit))
                {
                    // update the position of the object "hit" by the mouse
                    hit.transform.position = objPos;

                    gameObjHasMoved = true;

                    gameObjHeld = hit.transform;
                }
            }

            // check if the left button mouse is released while holding an object
            if (Input.GetMouseButtonUp(0) && gameObjHasMoved)
            {
                gameObjHasMoved = false;

                // Call the Azure Function that will update the appropriate Entity in the Azure Table
                // and send a Notification to all subscribed Apps
                Debug.Log("Calling Azure Function");

                StartCoroutine(UpdateCloudScene(gameObjHeld.name, gameObjHeld.position.x, gameObjHeld.position.y, gameObjHeld.position.z));
            }
        }
    ```

7.  Ajoutez maintenant le **UpdateCloudScene()** méthode, comme indiqué ci-dessous :

    ```csharp
        private IEnumerator UpdateCloudScene(string objName, double xPos, double yPos, double zPos)
        {
            WWWForm form = new WWWForm();

            // set the properties of the AzureTableEntity
            azureTableEntity.RowKey = objName;

            azureTableEntity.X = xPos;

            azureTableEntity.Y = yPos;

            azureTableEntity.Z = zPos;

            // Serialize the AzureTableEntity object to be sent to Azure
            string jsonObject = JsonConvert.SerializeObject(azureTableEntity);

            using (UnityWebRequest www = UnityWebRequest.Post(azureFunctionEndpoint, jsonObject))
            {
                byte[] jsonToSend = new System.Text.UTF8Encoding().GetBytes(jsonObject);

                www.uploadHandler = new UploadHandlerRaw(jsonToSend);

                www.uploadHandler.contentType = "application/json";

                www.downloadHandler = new DownloadHandlerBuffer();

                www.SetRequestHeader("Content-Type", "application/json");

                yield return www.SendWebRequest();

                string response = www.responseCode.ToString();
            }
        }
    ```

8.  Enregistrer le code et revenir à Unity

9.  Faites glisser le **CloudScene** de script sur le **Main Camera**. 

    1. Cliquez sur le **Main Camera** à partir de la **hiérarchie** panneau, afin que ses propriétés s’affichent dans le **inspecteur**. 

    2. Avec le **Scripts** ouvert, sélectionnez de dossier le **CloudScene** de script et faites-le glisser sur le **Main Camera**. Le résultat doit être comme suit :

        > ![faire glisser cloud script caméra principale](images/AzureLabs-Lab8-75.png)

## <a name="chapter-11---build-the-desktop-project-to-uwp"></a>Chapitre 11 - générer le projet de bureau vers UWP

Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée.

1.  Accédez à **les paramètres de génération** (**fichier** > **paramètres de Build**).

2.  À partir de la **paramètres de Build** fenêtre, cliquez sur **Build**.

    ![Générer le projet](images/AzureLabs-Lab8-76.png)

3.  Un **Explorateur de fichiers** fenêtre va contextuelle, vous invite à entrer un emplacement de Build. Créez un dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche) et nommez-le **génère**.

    ![nouveau dossier de build](images/AzureLabs-Lab8-77.png)

    1.  Ouvrez le nouveau **génère** dossier et créez un autre dossier (à l’aide de **nouveau dossier** une fois de plus) et nommez-le **NH\_Desktop\_application**.

        ![nom du dossier NH_Desktop_App](images/AzureLabs-Lab8-78.png)

    2.  Avec le **NH\_Desktop\_application** sélectionné. Cliquez sur **sélectionnez dossier**. Le projet prendra une minute ou donc en créer.

4.  Après la génération, **Explorateur de fichiers** s’affiche vous indiquant l’emplacement de votre nouveau projet. Pas nécessaire pour l’ouvrir, bien que, comme vous avez besoin créer l’autre Unity projet tout d’abord, dans les prochains chapitres.


## <a name="chapter-12---set-up-mixed-reality-unity-project"></a>Chapitre 12 - configurer des projets de Unity de réalité mixte

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez **Unity** et cliquez sur **New**.

    ![nouveau projet unity](images/AzureLabs-Lab8-79.png)

2.  Vous devez maintenant fournir un nom de projet Unity, insérer **UnityMRNotifHub**. Assurez-vous que le type de projet est défini sur **3D**. Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![name UnityMRNotifHub](images/AzureLabs-Lab8-80.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **modifier** > **préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![éditeur externe de jeu à Visual Studio](images/AzureLabs-Lab8-81.png)

4.  Ensuite, accédez à **fichier** > **paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **basculer la plateforme**  bouton.

    ![plateformes de commutateur vers UWP](images/AzureLabs-Lab8-82.png)

5.  Accédez à **fichier** > **paramètres de Build** et vous assurer que :

    1.  **Équipement cible** a la valeur **n’importe quel appareil**

        > Pour le Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.

    2.  **Type de build** a la valeur **D3D**

    3.  **Kit de développement logiciel** a la valeur **dernière installé**

    4.  **Version de Visual Studio** a la valeur **dernière installé**

    5.  **Générez et exécutez** est défini sur **ordinateur Local**

    6.  Cet emplacement, il est important de l’enregistrement de la scène et en l’ajoutant à la build.

        1. Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.

            ![ajouter des scènes ouverts](images/AzureLabs-Lab8-83.png)

        2. Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![nouveau dossier de scènes](images/AzureLabs-Lab8-84.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le **nom de fichier :** champ de texte, tapez **NH\_MR\_scène**, puis appuyez sur  **Enregistrer**.

            ![nouvelle scène - NH_MR_Scene](images/AzureLabs-Lab8-85.png)

    7.  Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.

6.  Dans la même fenêtre, cliquez sur le **paramètres du lecteur** bouton, le panneau de configuration associée s’ouvre dans l’espace où le **inspecteur** se trouve.    

    ![Ouvrez les paramètres du lecteur](images/AzureLabs-Lab8-86.png)

7.  Dans ce panneau, quelques paramètres doivent être vérifiées :

    1.  Dans le **autres paramètres** onglet :

        1.  **Version du Runtime de script** doit être **expérimental** (équivalent .NET 4.6)
        2.  **Script principal** doit être ***.NET***
        3.  **Niveau de compatibilité d’API** doit être **.NET 4.6**

            ![compatibilité d’API](images/AzureLabs-Lab8-87.png)

    2.  Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté

        ![mettre à jour les paramètres xr](images/AzureLabs-Lab8-88.png)        

    3.  Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, diable :

        - **InternetClient**           

            ![client internet de graduation](images/AzureLabs-Lab8-89.png)

8.  Dans **paramètres de Build**, **Unity C# projets** est n’est plus grisée : cochez la case à cocher en regard de cela.

9.  Avec ces modifications effectuées, fermez la fenêtre de paramètres de Build.

10. Enregistrer votre projet et scène **fichier** > **enregistrer la scène / fichier** > **enregistrer le projet**.

    > [!IMPORTANT]
    > Si vous souhaitez ignorer la *Unity configurer* composant pour ce projet (mixte réalité application) et toujours directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20308%20-%20Cross-device%20notifications/Azure-MR-308-MR.unitypackage), importez-le dans votre projet sous la forme d’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 14](#chapter-14---creating-the-tabletoscene-class-in-the-mixed-reality-unity-project). Vous devrez toujours ajouter les composants de script.

### <a name="chapter-13---importing-the-dlls-in-the-mixed-reality-unity-project"></a>Chapitre 13 - importation des DLL dans le projet Unity de réalité mixte

Vous utiliserez le stockage Azure pour bibliothèque Unity (qui utilise le kit SDK .net pour Azure). Veuillez suivre ce [lien sur l’utilisation du stockage Azure avec Unity](https://docs.microsoft.com/sandbox/gamedev/unity/azure-storage-unity).
Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation. Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.

Pour importer le SDK dans votre propre projet, assurez-vous que vous avez téléchargé la dernière version [.unitypackage](https://aka.ms/azstorage-unitysdk). Ensuite, procédez comme suit :

1.  Ajouter le .unitypackage que vous avez téléchargé à partir de l’exemple ci-dessus, à Unity à l’aide de la **actifs** > **importer un Package** > **Package personnalisé** option de menu .

2.  Dans le **importer un Package Unity** zone s’affiche, vous pouvez sélectionner tous les éléments sous **plug-in** > **stockage**.

    ![importer un package](images/AzureLabs-Lab8-90.png)

3.  Cliquez sur le **importation** pour ajouter les éléments à votre projet.

4.  Accédez à la **stockage** dossier sous **plug-ins** dans le projet afficher, puis sélectionnez les plug-ins suivants *uniquement*:

    -   Microsoft.Data.Edm
    -   Microsoft.Data.OData
    -   Microsoft.WindowsAzure.Storage
    -   Newtonsoft.Json
    -   System.Spatial

    ![Sélectionnez les plug-ins](images/AzureLabs-Lab8-91.png)

5.  Avec *ces plug-ins spécifiques* sélectionné, **Décochez** **plateforme Any** et **Décochez** **WSAPlayer** puis cliquez sur **appliquer**.

    ![appliquer les modifications de la plateforme](images/AzureLabs-Lab8-92.png)

    > [!NOTE] 
    > Vous marquez ces plug-ins particuliers à utiliser uniquement dans l’éditeur Unity. Il s’agit, car il existe différentes versions des mêmes plug-ins dans le dossier WSA qui sera utilisé après que le projet est exporté à partir d’Unity.

6.  Dans le **stockage** dossier de plug-in, sélectionnez uniquement :

    -   Microsoft.Data.Services.Client

        ![Sélectionnez le client des services de données](images/AzureLabs-Lab8-93.png)

7.  Vérifier le **processus ne** sous **paramètres de plateforme** et cliquez sur **appliquer**.

    ![ne pas traiter](images/AzureLabs-Lab8-94.png)

    > [!NOTE] 
    > Vous marquez ce plug-in « Ne pas traiter », car l’utilitaire de correction Unity assembly a des difficultés à traiter ce plug-in. Le plug-in continue de fonctionner même si elle n’est pas traitée.

## <a name="chapter-14---creating-the-tabletoscene-class-in-the-mixed-reality-unity-project"></a>Chapitre 14 - Création de la classe de TableToScene dans le projet Unity de réalité mixte

Le **TableToScene** classe est identique à celle qui est expliquée dans [chapitre 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project). Créer la même classe dans la réalité mixte projet Unity suivant la même procédure est expliquée dans [chapitre 9](#chapter-9---create-the-tabletoscene-class-in-the-desktop-unity-project).

Une fois que vous avez terminé ce chapitre, à la fois de votre **projets Unity** aura cette classe configurée sur l’appareil photo de Main.

## <a name="chapter-15---creating-the-notificationreceiver-class-in-the-mixed-reality-unity-project"></a>Chapitre 15 - création de la classe de NotificationReceiver dans le projet Unity de réalité mixte

Le deuxième script que vous créez est **NotificationReceiver**, qui est chargé de :

-   L’inscription de l’application avec le Hub de Notification lors de l’initialisation.
-   Écouter les notifications provenant du Hub de Notification.
-   Désérialiser les données d’objet à partir des notifications reçues.
-   Déplacer les GameObjects dans la scène, selon les données désérialisées.

Pour créer le **NotificationReceiver** script :

1.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer**, **C\# Script**. Nommez le script **NotificationReceiver**.

    ![création du nouveau script c#](images/AzureLabs-Lab8-95.png)
    ![nommez-le NotificationReceiver](images/AzureLabs-Lab8-96.png)

2.  Double-cliquez sur le script pour l’ouvrir.

3.  Ajoutez les espaces de noms suivants :

    ```csharp
    //using Microsoft.WindowsAzure.Messaging;
    using Newtonsoft.Json;
    using System;
    using System.Collections;
    using UnityEngine;

    #if UNITY_WSA_10_0 && !UNITY_EDITOR
    using Windows.Networking.PushNotifications;
    #endif
    ```

4.  Insérez les variables suivantes :

    ```csharp
        /// <summary>
        /// allows this class to behave like a singleton
        /// </summary>
        public static NotificationReceiver instance;

        /// <summary>
        /// Value set by the notification, new object position
        /// </summary>
        Vector3 newObjPosition;

        /// <summary>
        /// Value set by the notification, object name
        /// </summary>
        string gameObjectName;

        /// <summary>
        /// Value set by the notification, new object position
        /// </summary>
        bool notifReceived;

        /// <summary>
        /// Insert here your Notification Hub Service name 
        /// </summary>
        private string hubName = " -- Insert the name of your service -- ";

        /// <summary>
        /// Insert here your Notification Hub Service "Listen endpoint"
        /// </summary>
        private string hubListenEndpoint = "-Insert your Notification Hub Service Listen endpoint-";
    ```

5.  Remplacez le **hubName** valeur avec le nom de votre Service de Hub de Notification, et **hubListenEndpoint** valeur avec la valeur de point de terminaison située dans l’onglet de stratégies d’accès, le Service Azure Notification Hub, le Portail Azure (voir l’image ci-dessous).

    ![Insérer le point de terminaison de notification hubs stratégie](images/AzureLabs-Lab8-97.png)

6.  Ajoutez maintenant le **Start()** et **Awake()** méthodes pour initialiser la classe.

    ```csharp
        /// <summary>
        /// Triggers before initialization
        /// </summary>
        void Awake()
        {
            // static instance of this class
            instance = this;
        }

        /// <summary>
        /// Use this for initialization
        /// </summary>
        void Start()
        {
            // Register the App at launch
            InitNotificationsAsync();

            // Begin listening for notifications
            StartCoroutine(WaitForNotification());
        }
    ```

7.  Ajouter le **WaitForNotification** méthode pour autoriser l’application recevoir des notifications à partir de la bibliothèque de Hub de Notification sans conflit avec le Thread principal :

    ```csharp
        /// <summary>
        /// This notification listener is necessary to avoid clashes 
        /// between the notification hub and the main thread   
        /// </summary>
        private IEnumerator WaitForNotification()
        {
            while (true)
            {
                // Checks for notifications each second
                yield return new WaitForSeconds(1f);

                if (notifReceived)
                {
                    // If a notification is arrived, moved the appropriate object to the new position
                    GameObject.Find(gameObjectName).transform.position = newObjPosition;

                    // Reset the flag
                    notifReceived = false;
                }
            }
        }
    ```

8.  La méthode suivante, **InitNotificationAsync()** , inscription de l’application avec la Service de Hub de notification lors de l’initialisation. Le code est commenté car Unity ne seront pas en mesure de générer le projet. Vous allez supprimer les commentaires lorsque vous importez le package Nuget de messagerie Azure dans Visual Studio.

    ```csharp
        /// <summary>
        /// Register this application to the Notification Hub Service
        /// </summary>
        private async void InitNotificationsAsync()
        {
            // PushNotificationChannel channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // NotificationHub hub = new NotificationHub(hubName, hubListenEndpoint);

            // Registration result = await hub.RegisterNativeAsync(channel.Uri);

            // If registration was successful, subscribe to Push Notifications
            // if (result.RegistrationId != null)
            // {
            //     Debug.Log($"Registration Successful: {result.RegistrationId}");
            //     channel.PushNotificationReceived += Channel_PushNotificationReceived;
            // }
        }
    ```

9.  Le gestionnaire suivant, **canal\_PushNotificationReceived()** , sera déclenchée chaque fois qu’une notification est reçue. Il désérialise la notification, qui sera l’entité de Table Azure qui a été déplacé sur l’Application de bureau et puis déplacez le GameObject correspondant dans la scène MR vers la même position. 
    
    > [!IMPORTANT]
    > Le code est commenté, car le code fait référence à la bibliothèque de messagerie Azure, vous allez ajouter après la génération du projet Unity à l’aide du Gestionnaire de Package Nuget dans Visual Studio. Par conséquent, le projet Unity ne sera pas en mesure de générer, sauf si elle est commentée. Sachez que devez vous générez votre projet et que vous souhaitez ensuite revenir à Unity, vous devrez **nouveau commentaire** ce code.

    ```csharp
        ///// <summary>
        ///// Handler called when a Push Notification is received
        ///// </summary>
        //private void Channel_PushNotificationReceived(PushNotificationChannel sender, PushNotificationReceivedEventArgs args)    
        //{
        //    Debug.Log("New Push Notification Received");
        //
        //    if (args.NotificationType == PushNotificationType.Raw)
        //    {
        //        //  Raw content of the Notification
        //        string jsonContent = args.RawNotification.Content;
        //
        //        // Deserialise the Raw content into an AzureTableEntity object
        //        AzureTableEntity ate = JsonConvert.DeserializeObject<AzureTableEntity>(jsonContent);
        //
        //        // The name of the Game Object to be moved
        //        gameObjectName = ate.RowKey;          
        //
        //        // The position where the Game Object has to be moved
        //        newObjPosition = new Vector3((float)ate.X, (float)ate.Y, (float)ate.Z);
        //
        //        // Flag thats a notification has been received
        //        notifReceived = true;
        //    }
        //}
    ```

10. Pensez à enregistrer vos modifications avant de revenir à l’éditeur Unity.

11. Cliquez sur le **Main Camera** à partir de la **hiérarchie** panneau, afin que ses propriétés s’affichent dans le **inspecteur**.

12. Avec le **Scripts** ouvert, sélectionnez de dossier le **NotificationReceiver** de script et faites-le glisser sur le **Main Camera**. Le résultat doit être comme suit :

    ![Faites glisser de script de récepteur de notification à l’appareil photo](images/AzureLabs-Lab8-98.png)

    > [!NOTE]
    > Si vous développez cela pour le Microsoft HoloLens, vous devez mettre à jour le **Main Camera**de *caméra* composant, afin que :
    > - Effacer les indicateurs : Couleur unie
    > - Background : Noir

## <a name="chapter-16---build-the-mixed-reality-project-to-uwp"></a>Chapitre 16 - générer le projet de réalité mixte vers UWP

Ce chapitre est identique au processus pour le projet précédent de génération. Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.

1.  Accédez à **les paramètres de génération** ( **fichier** > **paramètres de Build** ).

2.  À partir de la **paramètres de Build** menu, vérifiez **Unity C# projets*** est cochée (ce qui vous permettra de modifier les scripts dans ce projet, après génération).

3.  Une fois cette opération est effectuée, cliquez sur **Build**.

    ![Générer le projet](images/AzureLabs-Lab8-99.png)

4.  Un **Explorateur de fichiers** fenêtre va contextuelle, vous invite à entrer un emplacement de Build. Créez un dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche) et nommez-le **génère**.

    ![créer le dossier de builds](images/AzureLabs-Lab8-100.png)

    1.  Ouvrez le nouveau **génère** dossier et créez un autre dossier (à l’aide de **nouveau dossier** une fois de plus) et nommez-le **NH\_MR\_application**.

        ![créer le dossier de NH_MR_Apps](images/AzureLabs-Lab8-101.png)

    2.  Avec le **NH\_MR\_application** sélectionné. Cliquez sur **sélectionnez dossier**. Le projet prendra une minute ou donc en créer.

5.  Suivant la génération, un **Explorateur de fichiers** fenêtre s’ouvre à l’emplacement de votre nouveau projet.



## <a name="chapter-17---add-nuget-packages-to-the-unitymrnotifhub-solution"></a>Chapitre 17 - ajouter des packages NuGet à la UnityMRNotifHub Solution

> [!WARNING] 
> N’oubliez pas que, une fois que vous ajoutez les Packages NuGet suivants (et les commentaires du code dans les prochains [chapitre](#chapter-18---edit-unitymrnotifhub-application-notificationreceiver-class)), le Code, la réouverture du projet Unity, présentera des erreurs. Si vous souhaitez revenir en arrière et continuer à modifier dans l’éditeur Unity, vous avez besoin de commenter ce code errosome et puis supprimez les commentaires plus tard, une fois que vous êtes de retour dans Visual Studio. 

Une fois la build de réalité mixte a été terminée, accédez au projet de réalité mixte, que vous avez créé, et double-cliquez sur le fichier solution (.sln) dans ce dossier, pour ouvrir votre solution avec Visual Studio 2017.
Vous devrez maintenant ajouter le **WindowsAzure.Messaging.managed** package NuGet ; il s’agit d’une bibliothèque qui est utilisée pour recevoir des Notifications à partir du Hub de Notification.

Pour importer le package NuGet :

1.  Dans le **l’Explorateur de solutions**, cliquez avec le bouton droit sur votre Solution

2.  Cliquez sur **gérer les Packages NuGet**.

    ![Ouvrez le gestionnaire nuget](images/AzureLabs-Lab8-102.png)

3.  Sélectionnez le ***Parcourir*** onglet et recherchez **WindowsAzure.Messaging.managed**.

    ![Recherchez le package de messagerie windows azure](images/AzureLabs-Lab8-103.png)

4.  Sélectionnez le résultat (comme indiqué ci-dessous) et dans la fenêtre à droite, sélectionnez la case à cocher à côté **projet**. Cela place un cycle dans la case à cocher à côté **projet**, ainsi que la case à cocher à côté du **Assembly-CSharp** et **UnityMRNotifHub** projet.

    ![Cochez tous les projets](images/AzureLabs-Lab8-104.png)

5.  La version fournie initialement **ne peut pas** être compatible avec ce projet. Par conséquent, cliquez sur le menu déroulant à côté **Version**, puis cliquez sur **Version 0.1.7.9**, puis cliquez sur **installer**.

6.  Vous avez maintenant terminé l’installation du package NuGet. Rechercher le code commenté que vous avez entré dans le **NotificationReceiver** classe et supprimez les commentaires...



## <a name="chapter-18---edit-unitymrnotifhub-application-notificationreceiver-class"></a>Chapitre 18 - application d’édition UnityMRNotifHub, NotificationReceiver classe

Après avoir ajouté le **les Packages NuGet**, vous devrez *supprimez les commentaires* partie du code dans le **NotificationReceiver** classe.

Cela comprend les éléments suivants :

1. L’espace de noms en haut :

    ```csharp
    using Microsoft.WindowsAzure.Messaging;
    ```

2. Tout le code dans le **InitNotificationsAsync()** méthode :

    ```csharp
        /// <summary>
        /// Register this application to the Notification Hub Service
        /// </summary>
        private async void InitNotificationsAsync()
        {
            PushNotificationChannel channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            NotificationHub hub = new NotificationHub(hubName, hubListenEndpoint);

            Registration result = await hub.RegisterNativeAsync(channel.Uri);

            // If registration was successful, subscribe to Push Notifications
            if (result.RegistrationId != null)
            {
                Debug.Log($"Registration Successful: {result.RegistrationId}");
                channel.PushNotificationReceived += Channel_PushNotificationReceived;
            }
        }
    ```

> [!WARNING]
> Le code ci-dessus comporte un commentaire : Vérifiez que vous n’avez pas accidentellement *sans commentaire* qui commentaire (comme le code compilera pas si vous avez !).

3. Et, enfin, le **Channel_PushNotificationReceived** événement :

    ```csharp
        /// <summary>
        /// Handler called when a Push Notification is received
        /// </summary>
        private void Channel_PushNotificationReceived(PushNotificationChannel sender, PushNotificationReceivedEventArgs args)
        {
            Debug.Log("New Push Notification Received");

            if (args.NotificationType == PushNotificationType.Raw)
            {
                //  Raw content of the Notification
                string jsonContent = args.RawNotification.Content;

                // Deserialize the Raw content into an AzureTableEntity object
                AzureTableEntity ate = JsonConvert.DeserializeObject<AzureTableEntity>(jsonContent);

                // The name of the Game Object to be moved
                gameObjectName = ate.RowKey;

                // The position where the Game Object has to be moved
                newObjPosition = new Vector3((float)ate.X, (float)ate.Y, (float)ate.Z);

                // Flag thats a notification has been received
                notifReceived = true;
            }
        }
    ```

Avec ces sans commentaire, assurez-vous que vous enregistrerez, puis passez au chapitre suivant.

## <a name="chapter-19---associate-the-mixed-reality-project-to-the-store-app"></a>Chapitre 19 - associer le projet de réalité mixte à l’application de Store

Vous devez maintenant associer la **une réalité mixte** projet à l’application de Store que vous avez créé dans au début du laboratoire.

1.  Ouvrez la solution.

2.  Cliquez avec le bouton droit sur l’application UWP projet dans le volet Explorateur de solutions, permettant d’atteindre **Store**, et **associer l’application avec le Store...** .

    ![ouverture d’association de magasin](images/AzureLabs-Lab8-105.png)

3.  Une nouvelle fenêtre s’affiche appelée **associer votre application du Windows Store**. Cliquez sur **Suivant**.

    ![Accédez à l’écran suivant](images/AzureLabs-Lab8-106.png)

4.  Il charge toutes les applications associé au compte sur lequel vous êtes connecté. Si vous n’êtes pas connecté votre compte, vous pouvez **Log In** sur cette page.

5.  Rechercher la **nom de l’application de Store** que vous avez créé au début de ce didacticiel et sélectionnez-le. Ensuite, cliquez sur **Suivant**.

    ![Recherchez et sélectionnez votre nom de magasin](images/AzureLabs-Lab8-107.png)

6.  Cliquez sur **associer**.

    ![associer l’application](images/AzureLabs-Lab8-108.png)

7.  Votre application est maintenant **associés** avec l’application de Store. Cela est nécessaire pour l’activation des Notifications.

## <a name="chapter-20---deploy-unitymrnotifhub-and-unitydesktopnotifhub-applications"></a>Chapitre 20 - déployer des applications UnityMRNotifHub et UnityDesktopNotifHub

Ce chapitre peut être plus facile avec deux personnes, comme le résultat inclut les applications en cours d’exécution, une en cours d’exécution sur votre ordinateur de bureau et l’autre au sein de votre casque immersive.

L’application de casque immersives attend de recevoir des modifications à la scène (modifications de la position de la GameObjects local), et l’application de bureau apporter des modifications à leur scène local (changements de position), qui est partagé par l’application MR. Il judicieux pour déployer l’application MR en premier, suivie de l’application de bureau, afin que le récepteur peut commencer à écouter.

Pour déployer le **UnityMRNotifHub** application sur votre ordinateur Local :

1.  Ouvrez le fichier de solution de votre **UnityMRNotifHub** app dans **Visual Studio 2017**.

2.  Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.

3.  Dans le **Configuration de la Solution** sélectionnez **déboguer**.

    ![configuration de projet de jeu](images/AzureLabs-Lab8-109.png)

4.  Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.

5.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.

Pour déployer le **UnityDesktopNotifHub** application sur l’ordinateur Local :

1.  Ouvrez le fichier de solution de votre **UnityDesktopNotifHub** app dans **Visual Studio 2017**.

2.  Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.

3.  Dans le **Configuration de la Solution** sélectionnez **déboguer**.

    ![configuration de projet de jeu](images/AzureLabs-Lab8-110.png)

4.  Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.

5.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.

6.  Lancez l’application de réalité mixte, suivie de l’application de bureau.

Avec les deux applications en cours d’exécution, déplacer un objet dans la scène de postes de travail (en utilisant le bouton de la souris gauche). Ces changements de position seront être effectuées localement, sérialisés et envoyés au service d’application de fonction. Le service d’application de fonction sera puis mettez à jour la Table, ainsi que le Hub de Notification. Ayant reçu une mise à jour, le Hub de Notification envoie les données mises à jour directement à toutes les applications inscrites (dans ce cas, l’application casque immersives) qui seront ensuite désérialiser les données entrantes et appliquer les nouvelles données positionnelles aux objets locales, en les déplaçant dans la scène.


## <a name="your-finished-your-azure-notification-hubs-application"></a>Votre terminé votre application Azure Notification Hubs
 
Félicitations, vous avez créé une application de réalité mixte qui tire parti du Service de concentrateurs de Notification Azure et autorise la communication entre les applications.
 
![produit final-fin](images/AzureLabs-Lab8-00.png)
 
## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Vous pouvez imaginer comment modifier la couleur de la GameObjects et envoyer cette notification vers d’autres applications d’affichage de la scène

### <a name="exercise-2"></a>Exercice 2

Possibilité d’ajouter le déplacement de la GameObjects à votre application MR et voir la scène mis à jour dans votre application de bureau ?
