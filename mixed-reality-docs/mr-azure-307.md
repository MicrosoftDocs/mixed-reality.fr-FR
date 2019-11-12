---
title: MR et Azure 307-machine learning
description: Suivez ce cours pour apprendre à implémenter Azure Machine Learning Studio dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, Machine Learning, ml, Machine Learning Studio, hololens, immersif, VR
ms.openlocfilehash: e302e287049cd746a436904c2af2bcc2b0835796
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926617"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br>

# <a name="mr-and-azure-307-machine-learning"></a>MR et Azure 307 : machine learning

![produit final-début](images/AzureLabs-Lab7-0.png)

Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de Machine Learning (ML) à une application de réalité mixte à l’aide d’Azure Machine Learning Studio.

*Azure machine learning Studio* est un service Microsoft qui fournit aux développeurs un grand nombre d’algorithmes de machine learning, qui peuvent aider à l’entrée, à la sortie, à la préparation et à la visualisation des données. À partir de ces composants, il est alors possible de développer une expérience d’analyse prédictive, d’effectuer une itération sur celle-ci et de l’utiliser pour former votre modèle. Après la formation, vous pouvez rendre votre modèle opérationnel dans le Cloud Azure, afin qu’il puisse noter de nouvelles données. Pour plus d’informations, consultez la [page Azure machine learning Studio](https://azure.microsoft.com/services/machine-learning-studio/).

Après avoir terminé ce cours, vous disposerez d’une application de casque d’immersion en réalité mixte et vous aurez appris comment effectuer les opérations suivantes :

1.  Fournissez une table de données de ventes au portail *Azure machine learning Studio* et concevez un algorithme pour prédire les ventes futures d’éléments populaires.
2.  Créez un **projet Unity**, qui peut recevoir et interpréter les données de prédiction du service ml.
3.  Affichez les données de prédicat visuellement dans le **projet Unity**, en fournissant les Articles de vente les plus populaires sur une étagère.

Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception. Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity. C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.

Ce cours est un didacticiel autonome qui n’implique pas directement d’autres laboratoires de réalité mixte.

## <a name="device-support"></a>Périphériques pris en charge

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 307 : machine learning</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Bien que ce cours se concentre principalement sur les casques de Windows Mixed Reality (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours à Microsoft HoloLens. À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge HoloLens. Lorsque vous utilisez HoloLens, vous remarquerez peut-être un écho pendant la capture vocale.

## <a name="prerequisites"></a>Conditions préalables

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l' [article installer les outils](install-the-tools.md), bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours :

- Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](install-the-tools.md#installation-checklist)
- [Le dernier Kit de développement logiciel Windows 10](install-the-tools.md#installation-checklist)
- [Unity 2017,4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé
- Accès Internet pour l’installation d’Azure et la récupération de données ML

## <a name="before-you-start"></a>Avant de commencer

Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération). 

## <a name="chapter-1---azure-storage-account-setup"></a>Chapitre 1-Configuration d’un compte de stockage Azure

Pour utiliser l’API Azure translator, vous devez configurer une instance du service qui sera mise à la disposition de votre application.
1.  Connectez-vous au [portail Azure](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas encore de compte Azure, vous devez en créer un. Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **comptes de stockage** dans le menu de gauche.

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab7-1.png)

    > [!NOTE]
    > Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.

3.  Dans l’onglet **comptes de stockage** , cliquez sur **Ajouter**.

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab7-2.png)

4.  Dans le panneau **créer un compte de stockage** :

    1.  Insérez un **nom** pour votre compte. n’oubliez pas que ce champ accepte uniquement des chiffres et des lettres minuscules.
    2.  Pour **modèle de déploiement,** sélectionnez **Resource Manager**.
    3.  Pour **type de compte**, sélectionnez **stockage (à usage général v1)** .
    4.  Pour **performances**, sélectionnez **standard**.
    5.  Pour **la réplication** , sélectionnez **Read-Access-géo-redondant Storage (RA-GRS)** .
    6.  Laissez le **transfert sécurisé requis** comme **désactivé**.
    7.  Sélectionnez un **abonnement**.
    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).
    
    5.  Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources). L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait. Certaines ressources Azure sont uniquement disponibles dans certaines régions.

5.  Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab7-3.png)

6.  Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.

7.  Une notification s’affichera dans le portail une fois l’instance de service créée.

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab7-4.png)

## <a name="chapter-2---the-azure-machine-learning-studio"></a>Chapitre 2-Azure Machine Learning Studio

Pour utiliser l' *Azure machine learning*, vous devez configurer une instance du service machine learning à mettre à la disposition de votre application.

1.  Dans le portail Azure, cliquez sur **nouveau** dans l’angle supérieur gauche et recherchez **machine learning Studio espace de travail**, appuyez sur **entrée**.

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-5.png)

2.  La nouvelle page fournit une description du service d' **espace de travail machine learning Studio** . En bas à gauche de cette invite, cliquez sur le bouton **créer** pour créer une association avec ce service.

3.  Une fois que vous avez cliqué sur **créer**, un panneau s’affiche pour vous permettre de fournir des détails sur votre nouveau **service machine learning Studio**:

    1.  Insérez le nom de l' **espace de travail** de votre choix pour cette instance de service.

    2.  Sélectionnez un **abonnement**.

    3. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun). 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    4.  Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources). L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait. Certaines ressources Azure sont uniquement disponibles dans certaines régions. Vous devez utiliser le même groupe de ressources que celui que vous avez utilisé pour créer le stockage Azure dans le chapitre précédent.

    5.  Pour la section **compte de stockage** , cliquez sur utiliser l' **existant**, puis cliquez sur le menu déroulant, et à partir de là, cliquez sur le compte de **stockage** que vous avez créé dans le dernier chapitre.

    6.  Sélectionnez le **niveau tarifaire** de l’espace de travail approprié dans le menu déroulant.

    7.  Dans la section **plan de service Web** , cliquez sur **créer** **nouveau,** puis insérez un nom dans le champ de texte.

    8.  Dans la section **niveau tarifaire du plan de service Web** , sélectionnez le niveau tarifaire de votre choix. Un niveau de test de développement appelé **DEVTEST standard** doit être disponible gratuitement.

    9.  Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.

    10. Cliquez sur **Create (Créer)** .

        ![Azure Machine Learning Studio](images/AzureLabs-Lab7-6.png)

4.  Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.

5.  Une notification s’affichera dans le portail une fois l’instance de service créée.

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-7.png)

6.  Cliquez sur la notification pour explorer votre nouvelle instance de service.

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-8.png)

7.  Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.

8.  Dans la page qui s’affiche, sous la section **liens supplémentaires** , cliquez sur **lancer machine learning Studio**, ce qui permet de diriger votre navigateur vers le portail des **machine learning Studio** .

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-9.png)

9.  Utilisez le bouton **se connecter** , en haut à droite ou au centre, pour vous connecter à votre machine learning Studio.

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-10.png)


## <a name="chapter-3---the-machine-learning-studio-dataset-setup"></a>Chapitre 3-Machine Learning Studio : installation du jeu de données

L’une des méthodes Machine Learning fonctionnement des algorithmes consiste à analyser les données existantes et à essayer de prédire les résultats futurs en fonction du jeu de données existant. Cela signifie généralement que plus vous avez de données existantes, plus l’algorithme sera adapté à la prévision des résultats futurs.

Un exemple de table est fourni pour vous, dans le cadre de ce cours, appelé [ProductsTableCSV et peut être téléchargé ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/MR%20and%20Azure%20307%20-%20Machine%20learning.zip).

> [!IMPORTANT]
> Le fichier. zip ci-dessus contient à la fois **ProductsTableCSV** et **. pour Unity**, dont vous aurez besoin au [chapitre 6](#chapter-6---importing-the-mlproducts-unity-package). Ce package est également fourni dans ce chapitre, bien qu’il soit séparé par le fichier CSV.

Cet exemple de jeu de données contient un enregistrement des objets les plus vendus à chaque heure de chaque jour de l’année 2017.
        
![Machine Learning Studio : configuration du jeu de données](images/AzureLabs-Lab7-11.png)

Par exemple, le jour 1 de 2017, à 13h00 (heure 13), l’article le mieux vendu était sel et poivron.

Cet exemple de table contient 9998 entrées.

1.  Revenez au portail **machine learning Studio** et ajoutez ce tableau en tant que **jeu de données** pour votre ml. Pour ce faire, cliquez sur le bouton **+ nouveau** dans le coin inférieur gauche de l’écran.

    ![Machine Learning Studio : configuration du jeu de données](images/AzureLabs-Lab7-12.png)

2.  Une section s’affiche à partir du bas et, dans la partie gauche du panneau de navigation. Cliquez sur **DataSet**, puis à droite de celui-ci, **à partir du fichier local**.

    ![Machine Learning Studio : configuration du jeu de données](images/AzureLabs-Lab7-13.png)

3.  Téléchargez le nouveau **jeu de données** en procédant comme suit :

    1. La fenêtre de chargement s’affiche, dans laquelle vous pouvez **Parcourir** votre disque dur pour le nouveau jeu de données.

        ![Machine Learning Studio : configuration du jeu de données](images/AzureLabs-Lab7-14.png)

    2.  Une fois que vous avez sélectionné, puis de nouveau dans la fenêtre de chargement, laissez la case à cocher désactivée.

    3.  Dans le champ de texte ci-dessous, entrez **ProductsTableCSV. csv** comme nom du jeu de données (bien qu’il soit ajouté automatiquement).

    4.  Dans le menu déroulant **type**, sélectionnez **fichier CSV générique avec un en-tête (. csv)** .

    5.  Appuyez sur la coche dans le coin inférieur droit de la fenêtre de chargement pour charger votre **jeu de données** .

## <a name="chapter-4---the-machine-learning-studio-the-experiment"></a>Chapitre 4-Machine Learning Studio : l’expérience

Avant de pouvoir créer votre système Machine Learning, vous devrez créer une expérience pour valider votre théorie sur vos données. Avec les résultats, vous saurez si vous avez besoin de davantage de données, ou s’il n’existe aucune corrélation entre les données et un résultat possible.

Pour commencer à créer une expérience :

1.  Cliquez à nouveau sur le bouton **+ nouveau** en bas à gauche de la page, puis cliquez sur **expérience** > **expérience vide**.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-15.png)

2.  Une nouvelle page s’affiche avec une expérience vide :

3.  Dans le volet de gauche, développez **DataSets enregistrés** > **mes jeux de données** , puis faites glisser le **ProductsTableCSV** dans la **zone de dessin**de l’expérience.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-16.png)

4.  Dans le volet de gauche, développez **transformation des données** > **échantillon et fractionner**. Ensuite, faites glisser l’élément **fractionner les données** dans la **zone de dessin**de l’expérience. L’élément fractionner les données divise le jeu de données en deux parties. Une partie que vous allez utiliser pour l’apprentissage de l’algorithme Machine Learning. La deuxième partie sera utilisée pour évaluer la précision de l’algorithme généré.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-17.png)

5.  Dans le volet droit (tandis que l’élément fractionner les données sur le canevas est sélectionné), modifiez la **fraction des lignes du premier jeu** de données de sortie sur **0,7**. Cela répartit les données en deux parties, la première partie est de 70% des données, et la deuxième partie sera les 30% restants. Pour vous assurer que les données sont fractionnées de façon aléatoire, assurez-vous que la case à cocher **fractionnement aléatoire** reste activée.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-18.png)

6.  Faites glisser une connexion de la base de l’élément **ProductsTableCSV** sur la zone de dessin vers le haut de l’élément de données fractionnées. Cela permet de connecter les éléments et d’envoyer la sortie du jeu de données **ProductsTableCSV** (les données) à l’entrée de fractionnement des données.  

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-19.png)

7.  Dans le panneau **expériences** sur le côté gauche, développez **machine learning** > **train**. Faites glisser l’élément **former le modèle** dans la zone de dessin de l’expérience. Votre canevas doit ressembler à ce qui suit.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-20.png)

8.  En ***bas à gauche*** de l’élément de **données fractionnées** , faites glisser une connexion en **haut à droite** de l’élément former le **modèle** . La première division de 70% du jeu de données sera utilisée par le modèle de formation pour former l’algorithme.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-21.png)

9.  Sélectionnez l’élément **former le modèle** sur la zone de dessin, puis dans le panneau **Propriétés** (sur le côté droit de la fenêtre de votre navigateur), cliquez sur le bouton lancer le **Sélecteur de colonne** .

10. Dans la zone de texte type **Product** , puis appuyez sur **entrée**, *Product* sera défini en tant que colonne pour former des prédictions. Ensuite, cliquez sur la **coche** dans le coin inférieur droit pour fermer la boîte de dialogue de sélection.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-22.png)

11. Vous allez former un algorithme de **régression logistique multiclasse** afin de prédire le **produit** le plus vendu en fonction de l’heure de la journée et de la date. L’explication des différents algorithmes fournis par le Azure Machine Learning Studio n’entre pas dans le cadre de ce document. Toutefois, vous pouvez en savoir plus sur l’aide-mémoire de l' [algorithme machine learning](https://docs.microsoft.com/azure/machine-learning/studio/algorithm-cheat-sheet)

12. Dans le panneau des éléments d’expérience sur la gauche, développez **Machine Learning** > **initialiser le modèle** > **classification**, puis faites glisser l’élément **multiCLASS logistique Regression** sur la zone de dessin de l’expérience.

13. Connectez la sortie, en bas de la **régression logistique multiclasse**, à l’entrée en haut à gauche de l’élément de **modèle de formation** .

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-23.png)

14. Dans la liste des éléments d’expérience dans le panneau de gauche, développez **Machine Learning** > **score**, puis faites glisser l’élément de **modèle de score** sur le canevas.

15. Connectez la sortie, du bas du modèle de **formation**, à l’entrée en haut à gauche du **modèle de score**.

16. Connectez la sortie en bas à droite à partir des **données de fractionnement**à l’entrée en haut à droite de l’élément de **modèle de score** .

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-24.png)

17. Dans la liste des éléments d' **expérience** dans le volet gauche, développez **machine learning** > **évaluer**, puis faites glisser l’élément de **modèle Evaluate** sur le canevas.

18. Connectez la sortie du **modèle de score** à l’entrée située en haut à gauche du **modèle d’évaluation**.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-25.png)

19. Vous avez créé votre première expérience Machine Learning. Vous pouvez maintenant enregistrer et exécuter l’expérience. Dans le menu situé en bas de la page, cliquez sur le bouton **Enregistrer** pour enregistrer votre expérience, puis cliquez sur **exécuter** jusqu’au début de l’expérience.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-26.png)

20. Vous pouvez voir l' **État** de l’expérience dans l’angle supérieur droit de la zone de dessin. Attendez quelques instants que l’expérience se termine.

    > Si vous avez un jeu de données volumineux (réel), il est probable que l’expérience peut prendre plusieurs heures.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-27.png)

21. Cliquez avec le bouton droit sur l’élément de **modèle Evaluate** dans le canevas, puis, dans le menu contextuel, pointez avec la souris sur résultats de l' **évaluation**, puis sélectionnez **visualiser**.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-28.png)

22. Les résultats de l’évaluation s’affichent et indiquent les résultats prédits par rapport aux résultats réels. Cela utilise les 30% du jeu de données d’origine, qui a été divisé précédemment, pour l’évaluation du modèle. Vous pouvez voir que les résultats ne sont pas excellents. dans l’idéal, le nombre le plus élevé dans chaque ligne est l’élément mis en surbrillance dans les colonnes.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-29.png)

23. Fermez les **résultats**.

24. Pour utiliser votre modèle de Machine Learning nouvellement formé, vous devez l’exposer en tant que **service Web**. Pour ce faire, cliquez sur l’élément de menu **configurer le service Web** dans le menu situé en bas de la page, puis cliquez sur **service Web prédictif**.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-30.png)

25. Un nouvel onglet est créé, et le modèle de formation est fusionné pour créer le nouveau service Web. 

26. Dans le menu situé en bas de la page, cliquez sur **Enregistrer**, puis sur **exécuter**. L’État mis à jour s’affiche dans l’angle supérieur droit de la zone de dessin de l’expérience.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-31.png)

27. Une fois l’exécution terminée, un bouton **déployer le service Web** s’affiche en bas de la page. Vous êtes prêt à déployer le service Web. Cliquez sur **déployer le service Web** (classique) dans le menu situé en bas de la page.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-32.png)

    > Votre navigateur peut demander à autoriser une fenêtre contextuelle, que vous devez **autoriser**, bien que vous deviez cliquer à nouveau sur **déployer le service Web** , si la page déployer ne s’affiche pas. 

28. Une fois l’expérience créée, vous êtes redirigé vers une page du **tableau de bord** où votre **clé API** sera affichée. Copiez-la dans un bloc-notes pour le moment. vous en aurez besoin dans votre code très rapidement. Une fois que vous avez noté votre clé API, cliquez sur le bouton **requête/réponse** dans la section **point de terminaison par défaut** sous la clé.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-33.png)

    > [!NOTE] 
    > Si vous cliquez sur tester dans cette page, vous serez en mesure d’entrer les données d’entrée et d’afficher la sortie. Entrez le **jour** et l' **heure**. Laissez l’entrée du **produit** vide. Cliquez ensuite sur le bouton **confirmer** . La sortie en bas de la page affiche le JSON qui représente la probabilité que chaque produit soit le choix.

29. Une nouvelle page Web s’ouvre, affichant les instructions et des exemples sur la structure de demande requise par le Machine Learning Studio. Copiez l' **URI de demande** affiché dans cette page dans votre bloc-notes.

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-34.png)

Vous avez maintenant créé un système de Machine Learning qui fournit le produit le plus probable à vendre en fonction des données d’achat historiques, corrélées avec l’heure du jour et du jour de l’année.

Pour appeler le service Web, vous aurez besoin de l’URL du point de terminaison de service et d’une clé API pour le service. Dans le menu supérieur, cliquez sur l’onglet **consommer** .

La page informations sur la **consommation** affiche les informations dont vous aurez besoin pour appeler le service Web à partir de votre code. Effectuez une copie de la **clé primaire** et de l’URL **de requête-réponse** . Vous en aurez besoin dans le chapitre suivant.

## <a name="chapter-5---setting-up-the-unity-project"></a>Chapitre 5-Configuration du projet Unity

Configurez et testez votre casque immersif en réalité mixte.

> [!NOTE]
>  Vous n’aurez **pas** besoin de contrôleurs de mouvement pour ce cours. Si vous avez besoin de la prise en charge de la configuration du casque immersif, cliquez [ici](https://support.microsoft.com/help/4043101/windows-10-set-up-windows-mixed-reality).

1.  Ouvrez **Unity** et créez un nouveau projet Unity appelé **Mr\_MachineLearning.** Assurez-vous que le type de projet est défini sur **3D**.

2.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**. Accédez à **modifier** > **Préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio 2017**. Fermez la fenêtre **Préférences** .

3.  Accédez ensuite à **fichier** > **paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton changer de ***plateforme*** .

4.  Assurez-vous également que :

    1.  L' **appareil cible** est défini sur **n’importe quel appareil**.

        > Pour Microsoft HoloLens, définissez **appareil cible** sur *HoloLens*.

    2.  Le **type de build** est **D3D**.

    3.  Le **SDK** est configuré sur le **dernier installé**.

    4.  La **version de Visual Studio** est **installée sur le plus récent**.

    5.  La **génération et l’exécution** sont définies sur l' **ordinateur local**.

    6.  Ne vous inquiétez pas de définir des **scènes** pour le moment, car elles sont fournies plus tard.

    7.  Les paramètres restants doivent être laissés par défaut pour le moment.

        ![Configuration du projet Unity](images/AzureLabs-Lab7-35.png)

5.  Dans la fenêtre **paramètres de build** , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** . 

6. Dans ce volet, quelques paramètres doivent être vérifiés :

    1.  Sous l’onglet **autres paramètres** :

        1.  La **version du runtime** de **script** doit être **expérimentale** (équivalent .net 4,6)

        2. Le **backend de script** doit être ***.net***

        3. Le **niveau de compatibilité** de l’API doit être **.net 4,6**

            ![Configuration du projet Unity](images/AzureLabs-Lab7-36.png)

    2.  Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher :

        - **InternetClient**

            ![Configuration du projet Unity](images/AzureLabs-Lab7-37.png)

    3.  Plus bas dans le panneau, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté

        ![Configuration du projet Unity](images/AzureLabs-Lab7-38.png)

    

6.  De retour dans les **paramètres de build** , les projets *Unity C#*  ne sont plus grisés. Cochez la case en regard de cette option. 

7.  Fermez la fenêtre Paramètres de Build.

8.  Enregistrez votre projet (**fichier > enregistrer le projet**).

## <a name="chapter-6---importing-the-mlproducts-unity-package"></a>Chapitre 6-importation du package MLProducts Unity

Pour ce cours, vous devrez télécharger un package d’actifs Unity appelé [**Azure-Mr-307. pour Unity**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/307-Scene-Setup.unitypackage). Ce package est complété par une scène, avec tous les objets de ce prégénération, ce qui vous permet de vous concentrer sur son fonctionnement. Le script **ShelfKeeper** est fourni, bien que ne contienne que les variables publiques, à des fins de structure de configuration de scène. Vous devrez effectuer toutes les autres sections. 

Pour importer ce package :

1.  Avec le tableau de bord Unity devant vous, cliquez sur **ressources** dans le menu en haut de l’écran, puis cliquez sur **Importer un package, puis sur package personnalisé**.

    ![Importation du package MLProducts Unity](images/AzureLabs-Lab7-39.png)

2.  Utilisez le sélecteur de fichiers pour sélectionner le package **Azure-Mr-307. pour Unity** , puis cliquez sur **ouvrir**.

3.  La liste des composants de cet élément multimédia vous est présentée. Confirmez l’importation en cliquant sur **Importer**.

    ![Importation du package MLProducts Unity](images/AzureLabs-Lab7-40.png)

4.  Une fois l’importation terminée, vous remarquerez que certains nouveaux dossiers apparaissent dans le **panneau Projet**Unity. Il s’agit des modèles 3D et des matériaux correspondants qui font partie de la scène prédéfinie sur laquelle vous allez travailler. Vous allez écrire la majorité du code dans ce cours.

    ![Importation du package MLProducts Unity](images/AzureLabs-Lab7-41.png)

5.  Dans le dossier du **panneau Projet** , cliquez sur le dossier **scenes** et double-cliquez sur la scène dans (appelée **MR_MachineLearningScene**). La scène s’ouvre (Voir l’image ci-dessous). Si les losanges rouges sont manquants, cliquez simplement sur le bouton **gizmos** , en haut à droite du **panneau du jeu**.

    ![Importation du package MLProducts Unity](images/AzureLabs-Lab7-44.png)

## <a name="chapter-7---checking-the-dlls-in-unity"></a>Chapitre 7-vérification des dll dans Unity

Pour tirer parti de l’utilisation de bibliothèques JSON (utilisées pour la sérialisation et la désérialisation), une DLL Newtonsoft a été implémentée avec le package que vous avez fourni. La configuration de la bibliothèque doit être correcte, bien qu’il soit important de le vérifier (en particulier si vous rencontrez des problèmes de fonctionnement du code). 

Pour ce faire :

-  Cliquez sur le fichier Newtonsoft dans le dossier plugins et observez le panneau de l' **inspecteur**. Assurez **-vous que toutes les plateformes** sont cochées. Accédez à l' **onglet UWP** et assurez-vous que **ne pas traiter** est coché.

    ![Importation des dll dans Unity](images/AzureLabs-Lab7-48.png)

## <a name="chapter-8---create-the-shelfkeeper-class"></a>Chapitre 8-créer la classe ShelfKeeper

La classe **ShelfKeeper** héberge des méthodes qui contrôlent l’interface utilisateur et les produits générés dans la scène.

Dans le cadre du package importé, vous aurez reçu cette classe, bien qu’elle soit incomplète. Il est maintenant temps de terminer cette classe :

1.  Double-cliquez sur le script **ShelfKeeper** , dans le dossier **scripts** , pour l’ouvrir avec **Visual Studio 2017**.

2.  Remplacez tout le code existant dans le script par le code suivant, qui définit la date et l’heure et a une méthode pour afficher un produit.

    ```csharp
    using UnityEngine;

    public class ShelfKeeper : MonoBehaviour
    {
        /// <summary>
        /// Provides this class Singleton-like behavior
        /// </summary>
        public static ShelfKeeper instance;

        /// <summary>
        /// Unity Inspector accessible Reference to the Text Mesh object needed for data
        /// </summary>
        public TextMesh dateText;

        /// <summary>
        /// Unity Inspector accessible Reference to the Text Mesh object needed for time
        /// </summary>
        public TextMesh timeText;

        /// <summary>
        /// Provides references to the spawn locations for the products prefabs
        /// </summary>
        public Transform[] spawnPoint;

        private void Awake()
        {
            instance = this;
        }

        /// <summary>
        /// Set the text of the date in the scene
        /// </summary>
        public void SetDate(string day, string month)
        {
            dateText.text = day + " " + month;
        }

        /// <summary>
        /// Set the text of the time in the scene
        /// </summary>
        public void SetTime(string hour)
        {
            timeText.text = hour + ":00";
        }

        /// <summary>
        /// Spawn a product on the shelf by providing the name and selling grade
        /// </summary>
        /// <param name="name"></param>
        /// <param name="sellingGrade">0 being the best seller</param>
        public void SpawnProduct(string name, int sellingGrade)
        {
            Instantiate(Resources.Load(name),
                spawnPoint[sellingGrade].transform.position, spawnPoint[sellingGrade].transform.rotation);
        }
    }
    ```

3.  Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenir à **Unity**.

4.  De retour dans l’éditeur Unity, vérifiez que la classe **ShelfKeeper** ressemble à ceci :

    ![Créer la classe ShelfKeeper](images/AzureLabs-Lab7-51.png)

    > [!IMPORTANT]
    > Si votre script ne possède pas les cibles de référence (par exemple, *Date (maillage de texte)* ), faites simplement glisser les objets correspondants à partir du volet de la **hiérarchie**vers les champs cibles. Voir ci-dessous pour plus d’explications, si nécessaire :
    > 
    > 1.  Ouvrez le tableau de **points de génération** dans le script du composant **ShelfKeeper** en cliquant dessus avec le bouton gauche. Une sous-section s’affiche appelée **Size**, qui indique la taille du tableau. Tapez **3** dans la zone de texte en regard de **taille** , puis appuyez sur **entrée**, et trois emplacements seront créés sous.
    > 2. Dans la **hiérarchie** , développez l’objet d’affichage de l' **heure** (en cliquant avec le bouton gauche sur la flèche à côté de lui). Ensuite, cliquez sur la ***caméra principale*** à l’intérieur de la **hiérarchie**, afin que l' **inspecteur** affiche ses informations.
    > 3. Sélectionnez la **caméra principale** dans le **volet**de la hiérarchie. Faites glisser les objets **Date** et **heure** du **panneau de hiérarchie** vers les emplacements de texte de **Date** et d' **heure** dans l' **inspecteur** de la **caméra principale** dans le composant **ShelfKeeper** .
    > 4. Faites glisser **les points de génération** à partir du panneau de la **hiérarchie** (sous l’objet *étagère* ) vers les cibles de référence d' **élément** **3** sous le tableau de **points de génération** , comme indiqué dans l’image.
    > 
    >     ![Créer la classe ShelfKeeper](images/AzureLabs-Lab7-52.png)

## <a name="chapter-9---create-the-productprediction-class"></a>Chapitre 9-créer la classe ProductPrediction

La classe suivante que vous allez créer est la classe **ProductPrediction** .

Cette classe est chargée des opérations suivantes :

-   Interrogation de l’instance de **Service machine learning** , en fournissant la date et l’heure actuelles.

-   Désérialisation de la réponse JSON en données utilisables.

-   Interprétation des données, récupération des 3 produits recommandés.

-   Appel des méthodes de la classe **ShelfKeeper** pour afficher les données dans la scène.

Pour créer cette classe :

1.  Accédez au dossier **scripts** , dans le **panneau Projet**.

2.  Cliquez avec le bouton droit dans le dossier, **créez** >  **C# script**. Appelez le script **ProductPrediction**.

3.  Double-cliquez sur le nouveau script **ProductPrediction** pour l’ouvrir avec **Visual Studio 2017**.

4.  Si la boîte de dialogue **modification de fichier détectée** s’affiche, cliquez sur ***recharger la solution**.

5.  Ajoutez les espaces de noms suivants en haut de la classe ProductPrediction :

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using System.Linq;
    using Newtonsoft.Json;
    using UnityEngine.Networking;
    using System.Runtime.Serialization;
    using System.Collections;
    ```

6.  À l’intérieur de la classe **ProductPrediction** , insérez les deux objets suivants qui sont composés d’un certain nombre de classes imbriquées. Ces classes sont utilisées pour sérialiser et désérialiser le JSON pour le service Machine Learning.

    ```csharp
        /// <summary>
        /// This object represents the Prediction request
        /// It host the day of the year and hour of the day
        /// The product must be left blank when serialising
        /// </summary>
        public class RootObject
        {
            public Inputs Inputs { get; set; }
        }

        public class Inputs
        {
            public Input1 input1 { get; set; }
        }

        public class Input1
        {
            public List<string> ColumnNames { get; set; }
            public List<List<string>> Values { get; set; }
        }
    ```

    ```csharp
        /// <summary>
        /// This object containing the deserialised Prediction result
        /// It host the list of the products
        /// and the likelihood of them being sold at current date and time
        /// </summary>
        public class Prediction
        {
            public Results Results { get; set; }
        }

        public class Results
        {
            public Output1 output1;
        }

        public class Output1
        {
            public string type;
            public Value value;
        }

        public class Value
        {
            public List<string> ColumnNames { get; set; }
            public List<List<string>> Values { get; set; }
        }
    ```

7.  Ajoutez ensuite les variables suivantes au-dessus du code précédent (afin que le code JSON soit au bas du script, sous tout le code, et à l’extérieur) :

    ```csharp
        /// <summary>
        /// The 'Primary Key' from your Machine Learning Portal
        /// </summary>
        private string authKey = "-- Insert your service authentication key here --";

        /// <summary>
        /// The 'Request-Response' Service Endpoint from your Machine Learning Portal
        /// </summary>
        private string serviceEndpoint = "-- Insert your service endpoint here --";

        /// <summary>
        /// The Hour as set in Windows
        /// </summary>
        private string thisHour;

        /// <summary>
        /// The Day, as set in Windows
        /// </summary>
        private string thisDay;

        /// <summary>
        /// The Month, as set in Windows
        /// </summary>
        private string thisMonth;

        /// <summary>
        /// The Numeric Day from current Date Conversion
        /// </summary>
        private string dayOfTheYear;

        /// <summary>
        /// Dictionary for holding the first (or default) provided prediction 
        /// from the Machine Learning Experiment
        /// </summary>    
        private Dictionary<string, string> predictionDictionary;

        /// <summary>
        /// List for holding product prediction with name and scores
        /// </summary>
        private List<KeyValuePair<string, double>> keyValueList;
    ```

    > [!IMPORTANT]
    > Veillez à insérer la **clé primaire** et le **point de terminaison de requête-réponse**, à partir du portail machine learning, dans les variables ici. Les images ci-dessous indiquent où vous avez pris la clé et le point de terminaison. 
    >  
    > ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-53-1.png)
    >
    > ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-53-2.png)

8.  Insérez ce code dans la méthode **Start ()** . La méthode **Start ()** est appelée lors de l’initialisation de la classe :

    ```csharp
        void Start()
        {
            // Call to get the current date and time as set in Windows
            GetTodayDateAndTime();

            // Call to set the HOUR in the UI
            ShelfKeeper.instance.SetTime(thisHour);

            // Call to set the DATE in the UI
            ShelfKeeper.instance.SetDate(thisDay, thisMonth);

            // Run the method to Get Predication from Azure Machine Learning
            StartCoroutine(GetPrediction(thisHour, dayOfTheYear));
        }
    ```

9.  Voici la méthode qui collecte la date et l’heure de Windows et les convertit dans un format que notre expérience Machine Learning peut utiliser pour comparer avec les données stockées dans la table.

    ```csharp
        /// <summary>
        /// Get current date and hour
        /// </summary>
        private void GetTodayDateAndTime()
        {
            // Get today date and time
            DateTime todayDate = DateTime.Now;

            // Extrapolate the HOUR
            thisHour = todayDate.Hour.ToString();

            // Extrapolate the DATE
            thisDay = todayDate.Day.ToString();
            thisMonth = todayDate.ToString("MMM");

            // Extrapolate the day of the year
            dayOfTheYear = todayDate.DayOfYear.ToString();
        }
    ```

10. Vous pouvez **supprimer** la méthode **Update ()** puisque cette classe ne l’utilise pas.

11. Ajoutez la méthode suivante, qui communiquera la date et l’heure actuelles au point de terminaison Machine Learning et recevra une réponse au format JSON.

    ```csharp
        private IEnumerator GetPrediction(string timeOfDay, string dayOfYear)
        {
            // Populate the request object 
            // Using current day of the year and hour of the day
            RootObject ro = new RootObject
            {
                Inputs = new Inputs
                {
                    input1 = new Input1
                    {
                        ColumnNames = new List<string>
                        {
                            "day",
                            "hour",
                        "product"
                        },
                        Values = new List<List<string>>()
                    }
                }
            };

            List<string> l = new List<string>
            {
                dayOfYear,
                timeOfDay,
                ""
            };

            ro.Inputs.input1.Values.Add(l);

            Debug.LogFormat("Score request built");

            // Serialize the request
            string json = JsonConvert.SerializeObject(ro);

            using (UnityWebRequest www = UnityWebRequest.Post(serviceEndpoint, "POST"))
            {
                byte[] jsonToSend = new System.Text.UTF8Encoding().GetBytes(json);
                www.uploadHandler = new UploadHandlerRaw(jsonToSend);

                www.downloadHandler = new DownloadHandlerBuffer();
                www.SetRequestHeader("Authorization", "Bearer " + authKey);
                www.SetRequestHeader("Content-Type", "application/json");
                www.SetRequestHeader("Accept", "application/json");

                yield return www.SendWebRequest();
                string response = www.downloadHandler.text;

                // Deserialize the response
                DataContractSerializer serializer;
                serializer = new DataContractSerializer(typeof(string));
                DeserialiseJsonResponse(response);
            }
        }
    ```

12. Ajoutez la méthode suivante, qui est chargée de désérialiser la réponse JSON et de communiquer le résultat de la désérialisation à la classe **ShelfKeeper** . Ce résultat sera le nom des trois éléments prédits pour vendre le plus à la date et à l’heure actuelles. Insérez le code ci-dessous dans la classe **ProductPrediction** , sous la méthode précédente.

    ```csharp
        /// <summary>
        /// Deserialize the response received from the Machine Learning portal
        /// </summary>
        public void DeserialiseJsonResponse(string jsonResponse)
        {
            // Deserialize JSON
            Prediction prediction = JsonConvert.DeserializeObject<Prediction>(jsonResponse);
            predictionDictionary = new Dictionary<string, string>();

            for (int i = 0; i < prediction.Results.output1.value.ColumnNames.Count; i++)
            {
                if (prediction.Results.output1.value.Values[0][i] != null)
                {
                    predictionDictionary.Add(prediction.Results.output1.value.ColumnNames[i], prediction.Results.output1.value.Values[0][i]);
                }
            }

            keyValueList = new List<KeyValuePair<string, double>>();

            // Strip all non-results, by adding only items of interest to the scoreList
            for (int i = 0; i < predictionDictionary.Count; i++)
            {
                KeyValuePair<string, string> pair = predictionDictionary.ElementAt(i);
                if (pair.Key.StartsWith("Scored Probabilities"))
                {
                    // Parse string as double then simplify the string key so to only have the item name
                    double scorefloat = 0f;
                    double.TryParse(pair.Value, out scorefloat);
                    string simplifiedName =
                        pair.Key.Replace("\"", "").Replace("Scored Probabilities for Class", "").Trim();
                    keyValueList.Add(new KeyValuePair<string, double>(simplifiedName, scorefloat));
                }
            }

            // Sort Predictions (results will be lowest to highest)
            keyValueList.Sort((x, y) => y.Value.CompareTo(x.Value));

            // Spawn the top three items, from the keyValueList, which we have sorted
            for (int i = 0; i < 3; i++)
            {
                ShelfKeeper.instance.SpawnProduct(keyValueList[i].Key, i);
            }

            // Clear lists in case of reuse
            keyValueList.Clear();
            predictionDictionary.Clear();
        }
    ```

13. Enregistrez **Visual Studio** et revenez à **Unity**.

14. Faites glisser le script de la classe **ProductPrediction** du dossier **script** vers l’objet **Camera principal** .

15. Enregistrez votre scène et votre **fichier** projet > **enregistrer la séquence/le fichier** > enregistrer le **projet**.

## <a name="chapter-10---build-the-uwp-solution"></a>Chapitre 10 : créer la solution UWP

Il est maintenant temps de générer votre projet en tant que solution UWP, afin qu’il puisse s’exécuter en tant qu’application autonome.

Pour générer :

1.  Enregistrez la scène en cours en cliquant sur **fichier** > **enregistrer des scènes**.

2.  Atteindre le **fichier** > les **paramètres de build**

3.  Cochez la case **projets Unity C#**  (c’est important, car cela vous permettra de modifier les classes une fois la génération terminée).

4.  Cliquez sur **Ajouter des scènes ouvertes**.

5.  Cliquez sur **Build**.

    ![Créer la solution UWP](images/AzureLabs-Lab7-54.png)

6.  Vous serez invité à sélectionner le dossier dans lequel vous souhaitez générer la solution.

7.  Créez un dossier **Builds** et, dans ce dossier, créez un autre dossier avec le nom approprié de votre choix.

8.  Cliquez sur votre nouveau dossier, puis sur **Sélectionner un dossier**pour commencer la build à cet emplacement.

    ![Créer la solution UWP](images/AzureLabs-Lab7-55.png)

    ![Créer la solution UWP](images/AzureLabs-Lab7-56.png)

9.  Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).

## <a name="chapter-11---deploy-your-application"></a>Chapitre 11-déployer votre application

Pour déployer votre application :

1.  Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.

2.  Avec Visual Studio Open, vous devez restaurer les packages NuGet. pour ce faire, vous pouvez cliquer avec le bouton droit sur votre solution MachineLearningLab_Build, à partir de la Explorateur de solutions (située à droite de Visual Studio), puis en cliquant sur restaurer les packages NuGet :

    ![Ajouter des packages NuGet](images/AzureLabs-Lab7-57.png)

3.  Dans la configuration de la solution, sélectionnez **Déboguer**.

4.  Dans la plateforme de la solution, sélectionnez **x86**, **ordinateur local**. 

    > Pour Microsoft HoloLens, il peut s’avérer plus facile de définir cette valeur sur *machine distante*, afin de ne pas être attaché à votre ordinateur. Toutefois, vous devez également effectuer les opérations suivantes :
    > - Identifiez l' **adresse IP** de votre HoloLens, qui se trouve dans les *paramètres > réseau & Internet > les options avancées du Wi-Fi >* ; IPv4 est l’adresse que vous devez utiliser. 
    > - Assurez-vous que le **mode développeur** est **activé**; trouvé dans *paramètres > mettre à jour & > de sécurité pour les développeurs*.

    ![Ajouter des packages NuGet](images/AzureLabs-Lab7-58.png)

5.  Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre PC.

6.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.

Lorsque vous exécutez l’application de réalité mixte, vous voyez le banc qui a été configuré dans votre scène Unity et, à partir de l’initialisation, les données que vous avez configurées dans Azure sont extraites. Les données seront désérialisées au sein de votre application et les trois premiers résultats de la date et de l’heure actuelles seront fournis visuellement, sous la forme de trois modèles sur le banc d’essai.


## <a name="your-finished-machine-learning-application"></a>Votre application Machine Learning terminée
 
Félicitations, vous avez créé une application de réalité mixte qui tire parti de la Azure Machine Learning pour effectuer des prédictions de données et les afficher sur votre scène.

![Ajouter des packages NuGet](images/AzureLabs-Lab7-0.png)

## <a name="exercise"></a>Exercices

**Exercice 1**

Expérimentez l’ordre de tri de votre application et faites en sorte que les trois prédictions les plus basses s’affichent sur l’étagère, car ces données peuvent également être utiles.

**Exercice 2**

L’utilisation de **tables Azure** remplit une nouvelle table avec les informations météorologiques et crée une nouvelle expérience à l’aide des données.
