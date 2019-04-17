---
title: MR et Azure Machine learning 307-
description: Terminer ce cours pour apprendre à implémenter Azure Machine Learning Studio au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, apprentissage automatique, ml studio d’apprentissage machine, hololens, immersives, vr
ms.openlocfilehash: 726a6cce91d46ad878f8502381d085fb979ac72a
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594338"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-and-azure-307-machine-learning"></a>MR et Azure 307 : Machine Learning

![produit final-Démarrer](images/AzureLabs-Lab7-0.png)

Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de Machine Learning (ML) à une application de réalité mixte à l’aide d’Azure Machine Learning Studio.

*Azure Machine Learning Studio* est un service Microsoft, qui fournit aux développeurs un grand nombre d’algorithmes d’apprentissage, ce qui peut aider à l’entrée de données, de sortie, de préparation et de visualisation. À partir de ces composants, il est alors possible de développer une expérience d’analytique prédictive, effectuer une itération sur celle-ci et utilisez-la dans votre modèle. Suivant une formation, vous pouvez rendre votre modèle opérationnel dans le cloud Azure, afin qu’il peut ensuite évaluer les nouvelles données. Pour plus d’informations, visitez le [page Azure Machine Learning Studio](https://azure.microsoft.com/en-au/services/machine-learning-studio/).

Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte et aurez appris comment effectuer les opérations suivantes :

1.  Fournir une table de données de ventes pour le *Azure Machine Learning Studio* portal et la conception un algorithme pour prédire les ventes futures d’éléments les plus courants.
2.  Créer un **projet Unity**, ce qui peut recevoir et interpréter les données de prédiction à partir du service de ML.
3.  Afficher les données de prédiction visuellement dans le **projet Unity**, jusqu'à fournissant des articles de la ventes les plus populaires, sur une étagère.

Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception. Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity. Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.

Ce cours est un didacticiel autonome, ce qui n’implique pas directement de tous les autres laboratoires réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 307 : Machine Learning</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens. Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens. Lorsque vous utilisez HoloLens, vous pouvez remarquer quelques echo durant la capture de la voix.

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer l’article outils](install-the-tools.md), mais il doit être pas supposé que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .

Nous recommandons le matériel et logiciel pour ce cours suivants :

- Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)
- [Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé](install-the-tools.md#installation-checklist)
- [Le SDK Windows 10 dernières](install-the-tools.md#installation-checklist)
- [Unity 2017.4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé
- Accès à Internet pour le programme d’installation Azure et l’extraction de données de ML

## <a name="before-you-start"></a>Avant de commencer

Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération). 

## <a name="chapter-1---azure-storage-account-setup"></a>Chapitre 1 - Configuration d’un compte de stockage Azure

Pour utiliser l’API de Translator Azure, vous devrez configurer une instance du service à être mis à disposition de votre application.
1.  Connectez-vous à la [Azure Portal](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **comptes de stockage** dans le menu de gauche.

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab7-1.png)

    > [!NOTE]
    > Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.

3.  Sur le **comptes de stockage** onglet, cliquez sur **ajouter**.

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab7-2.png)

4.  Dans le **créer un compte de stockage** panneau :

    1.  Insérer un **nom** pour votre compte, n’oubliez pas ce champ accepte uniquement des lettres minuscules et chiffres.
    2.  Pour **modèle de déploiement,** sélectionnez **Resource manager**.
    3.  Pour **type de compte**, sélectionnez **stockage (usage général v1)**.
    4.  Pour **performances**, sélectionnez **Standard**.
    5.  Pour **réplication** sélectionnez **en lecture-access-geo-redundant storage (RA-GRS)**.
    6.  Laissez **transfert sécurisé requis** comme **désactivé**.
    7.  Sélectionnez un **abonnement**.
    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).
    
    5.  Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions.

5.  Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab7-3.png)

6.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.

7.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab7-4.png)

## <a name="chapter-2---the-azure-machine-learning-studio"></a>Chapitre 2 - Azure Machine Learning Studio

Pour utiliser le *Azure Machine Learning*, vous devez configurer une instance du service Machine Learning à être mis à disposition de votre application.

1.  Dans le portail Azure, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez **espace de travail Machine Learning Studio**, appuyez sur **entrée**.

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-5.png)

2.  La nouvelle page doit fournir une description de la **espace de travail Machine Learning Studio** service. En bas à gauche de cette invite, cliquez sur le **créer** bouton permettant de créer une association avec ce service.

3.  Une fois que vous avez cliqué sur **créer**, un panneau s’affiche où vous devez fournir des détails sur votre nouvelle **service Machine Learning Studio**:

    1.  Insérez votre souhaitée **nom de l’espace de travail** pour cette instance de service.

    2.  Sélectionnez un **abonnement**.

    3. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs). 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    4.  Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions. Vous devez utiliser le même groupe de ressources que vous avez utilisé pour créer le stockage Azure dans le chapitre précédent.

    5.  Pour le **compte de stockage** , cliquez sur **utiliser l’existant**, puis cliquez sur le menu déroulant, puis à partir de là, cliquez sur le **compte de stockage** vous avez créé dans le dernier chapitre.

    6.  Sélectionnez l’option appropriée **espace de travail de niveau tarifaire** pour vous, dans le menu déroulant.

    7.  Dans le **plan de service Web** , cliquez sur **créer** **nouveau,** puis insérez un nom pour celle-ci dans le champ de texte.

    8.  À partir de la **niveau tarifaire du plan de service Web** , sélectionnez le niveau de prix de votre choix. Un environnement de développement test niveau appelé **DEVTEST Standard** doivent être disponibles pour vous sans frais.

    9.  Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.

    10. Cliquez sur **Create (Créer)**.

        ![Azure Machine Learning Studio](images/AzureLabs-Lab7-6.png)

4.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.

5.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-7.png)

6.  Cliquez sur la notification pour Explorer votre nouvelle instance de Service.

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-8.png)

7.  Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.

8.  Dans la page affichée sous la **liens supplémentaires** , cliquez sur **lancer Machine Learning Studio**, qui sera votre navigateur, à la **Machine Learning Studio** portail.

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-9.png)

9.  Utilisez le **Sign In** button, en haut à droite ou dans le centre de se connecter à votre Machine Learning Studio.

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-10.png)


## <a name="chapter-3---the-machine-learning-studio-dataset-setup"></a>Chapitre 3 - Machine Learning Studio : Programme d’installation de jeu de données

Une des manières d’utiliser des algorithmes d’apprentissage automatique en analysant les données existantes et puis tente de prédire les futurs résultats repose sur le jeu de données existant. Ce qui signifie généralement les données plus existantes que vous avez, plus l’algorithme sera à prédire les futurs résultats.

Un exemple de table vous est fourni, ce cours, appelé [ProductsTableCSV et peut être téléchargé ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/MR%20and%20Azure%20307%20-%20Machine%20learning.zip).

> [!IMPORTANT]
> Le fichier .zip ci-dessus contient à la fois le **ProductsTableCSV** et **.unitypackage**, dont vous aurez besoin dans [chapitre 6](#chapter-6---importing-the-mlproducts-unity-package). Ce package est également fourni dans ce chapitre, bien que distinct dans le fichier csv.

Ce jeu de données exemple contient un enregistrement des objets pape de toutes les heures de chaque jour de l’année 2017.
        
![Machine Learning Studio : Programme d’installation de jeu de données](images/AzureLabs-Lab7-11.png)

Par exemple, le jour 1 de 2017, à 13 h 00 (heure 13), l’élément pape était salt et poivre.

Cet exemple de table contient des 9998 entrées.

1.  Revenez à la **Machine Learning Studio** portail, et ajoutez cette table comme un **Dataset** pour votre ML. Cela en cliquant sur le **+ nouveau** bouton dans le coin inférieur gauche de l’écran.

    ![Machine Learning Studio : Programme d’installation de jeu de données](images/AzureLabs-Lab7-12.png)

2.  Une section s’allumera à partir du bas et au sein qu’il existe le panneau de navigation de gauche. Cliquez sur **Dataset**, puis vers la droite, **à partir d’un fichier Local**.

    ![Machine Learning Studio : Programme d’installation de jeu de données](images/AzureLabs-Lab7-13.png)

3.  Charger le nouveau **Dataset** en suivant ces étapes :

    1. La fenêtre de chargement s’affiche, dans laquelle vous pouvez **Parcourir** votre disque dur pour le nouveau jeu de données.

        ![Machine Learning Studio : Programme d’installation de jeu de données](images/AzureLabs-Lab7-14.png)

    2.  Une fois la sélection et dans la fenêtre de chargement, laissez la case à cocher décoché.

    3.  Dans le champ de texte ci-dessous, entrez **ProductsTableCSV.csv** comme nom pour le jeu de données (bien que doit être ajouté automatiquement).

    4.  À l’aide de la liste déroulante pour **Type**, sélectionnez **fichier CSV générique avec un en-tête (.csv)**.

    5.  Appuyez sur les graduations dans la partie inférieure droite de la fenêtre de chargement et votre **Dataset** sera téléchargé.

## <a name="chapter-4---the-machine-learning-studio-the-experiment"></a>Chapitre 4 - Machine Learning Studio : L’expérience

Avant de pouvoir générer votre système d’apprentissage automatique, vous devez créer une expérience, pour valider votre théorie sur vos données. Avec les résultats, vous savez que vous ayez besoin de davantage de données, ou s’il n’existe aucune corrélation entre les données et un résultat possible.

Pour commencer à créer une expérience :

1.  Cliquez de nouveau sur le **+ nouveau** bouton dans la coin inférieur gauche de la page, puis cliquez sur **expérience** > **expérience vide**.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-15.png)

2.  Une nouvelle page s’affiche avec une expérience vide :

3.  À partir du panneau sur la gauche développer **jeux de données enregistrés* > * Mes jeux de données ** et faites glisser le **ProductsTableCSV** à la **canevas de l’expérience**.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-16.png)

4.  Dans le volet gauche, développez **Transformation des données** > **Sample and Split**. Puis faites glisser le **fractionner les données** élément dans le **canevas de l’expérience**. L’élément de données de fractionnement fractionne le jeu de données en deux parties. Une partie, vous allez utiliser pour l’apprentissage de l’algorithme d’apprentissage. La deuxième partie est utilisée pour évaluer la précision de l’algorithme généré.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-17.png)

5.  Dans le volet de droite (lors de la fractionner les données élément sur le canevas est sélectionné), modifiez le **Fraction de lignes dans le premier jeu de données de sortie** à **0,7**. Il fractionne les données en deux parties, la première partie sera 70 % des données, et la deuxième partie est le 30 % restantes. Pour garantir que les données sont fractionnées de façon aléatoire, vérifiez que le **fractionnement aléatoire** case à cocher reste cochée.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-18.png)

6.  Faites glisser une connexion à partir de la base de la **ProductsTableCSV** élément sur le canevas en haut de l’élément de fractionner les données. Cela lier des éléments et envoyer le **ProductsTableCSV** sortie du jeu de données (données) à fractionner les données d’entrée.  

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-19.png)

7.  Dans le **expériences** panneau sur le côté gauche, développez **Machine Learning* > * Train **. Faites glisser le **former modèle ** élément out dans la zone de dessin. La zone de travail doit se présenter le même que le ci-dessous.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-20.png)

8.  À partir de la ***en bas à gauche*** de la **fractionner les données** élément faites glisser une connexion à la **en haut à droite** de la **former le modèle** élément. La première division de 70 % du jeu de données se servira pour l’apprentissage de l’algorithme de former le modèle.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-21.png)

9.  Sélectionnez le **former le modèle** élément sur le canevas et, dans le **propriétés** cliquez sur Panneau de configuration (sur le côté droit de la fenêtre du navigateur) le **lancer le sélecteur de colonne**  bouton.

10. Dans le type de zone de texte **produit** , puis appuyez sur **entrée**, *produit* sera définie comme une colonne pour l’apprentissage des prédictions. Ensuite, cliquez sur le **graduation** en bas à droite pour fermer la boîte de dialogue de sélection.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-22.png)

11. Vous vous apprêtez à former un **Multiclass Logistic Regression** algorithme pour prédire les plus vendus **produit** selon l’heure de la journée et la date. Il n’entre pas dans le cadre de ce document pour expliquer les détails des différents algorithmes fournis par Azure Machine Learning studio, cependant, vous pouvez trouver plus d’informations à partir de la [Machine Learning aide-mémoire d’algorithme](https://docs.microsoft.com/azure/machine-learning/studio/algorithm-cheat-sheet)

12. Dans le panneau éléments expérience sur la gauche, développez ***Machine Learning* > *initialiser le modèle* > * classement ***et faites glisser le **Multiclass Logistique régression ** élément une session sur le canevas d’expérience.

13. Connectez la sortie, en bas de la **Multiclass Logistic Regression**, à l’entrée de l’angle supérieur gauche de la **former le modèle** élément.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-23.png)

14. Dans la liste des éléments d’expérience dans le volet gauche, développez **Machine Learning* > * Score**et faites glisser le **élément de modèle de Score ** une session sur le canevas.

15. Connectez la sortie, en bas de la **former le modèle**, à l’entrée de l’angle supérieur gauche de la **noter le modèle**.

16. Connectez la sortie en bas à droite de **fractionner les données**, à l’entrée en haut à droite de la **noter le modèle* élément *.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-24.png)

17. Dans la liste des **expérience** éléments dans le volet gauche, développez ***Machine Learning* > * évaluer ***et faites glisser le **élément modèle ** évaluer sur le canevas.

18. Connectez la sortie à partir de la **noter le modèle** à l’entrée de l’angle supérieur gauche de la **évaluer le modèle**.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-25.png)

19. Vous avez créé votre première expérience d’apprentissage Machine. Vous pouvez maintenant enregistrer et exécuter l’expérience. Dans le menu en bas de la page, cliquez sur le **enregistrer** bouton pour enregistrer votre expérience, puis sur **exécuter** au début de l’expérience.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-26.png)

20. Vous pouvez voir le **état** de l’expérience dans l’angle supérieur droit de la zone de dessin. Attendez quelques instants pour l’expérience se termine.

    > Si vous avez un jeu de données volumineuses (réel), il est probable que l’expérience peut prendre des heures à exécuter.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-27.png)

21. Cliquez avec le bouton droit sur le **évaluer le modèle** d’élément dans la zone de dessin et le pointage de menu contextuel à partir de la souris sur **résultats d’évaluation**, puis sélectionnez **visualiser**.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-28.png)

22. Les résultats d’évaluation seront affiche en montrant les résultats prédits par rapport aux résultats réels. Cet exemple utilise le 30 % du dataset d’origine, qui a été fractionné précédemment, pour évaluer le modèle. Vous pouvez voir que les résultats ne sont pas très bien, dans l’idéal, vous aurez le plus grand nombre dans chaque ligne est l’élément en surbrillance dans les colonnes.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-29.png)

23. Fermer le **résultats**.

24. Pour utiliser votre modèle Machine Learning reformé, vous devez exposer en tant qu’un **Service Web**. Pour ce faire, cliquez sur le **configurer le Service Web** dans le menu en bas de la page d’élément de menu, puis cliquez sur **Service Web prédictif**.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-30.png)

25. Un nouvel onglet est créé, et le former le modèle fusionnés pour créer le nouveau service web. 

26. Dans le menu en bas de la page, cliquez sur **enregistrer**, puis cliquez sur **exécuter**. Vous verrez l’état mis à jour dans l’angle supérieur droit de la zone de dessin.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-31.png)

27. Une fois qu’elle est terminée, un **déployer le Service Web** bouton s’affiche en bas de la page. Vous êtes prêt à déployer le service web. Cliquez sur **déployer le Service Web** (classique) dans le menu en bas de la page.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-32.png)

    > Votre navigateur peut vous demander pour autoriser une fenêtre contextuelle, ce qui vous convient **autoriser**, bien que vous devrez peut-être appuyer sur **déployer le Service Web** là encore, si la page déployer n’apparaît pas. 

28. Une fois que l’expérience a été créée, vous serez redirigé vers un **tableau de bord** page où vous disposerez votre **clé API** affiché. Copier dans un bloc-notes pour le moment, vous en aurez besoin très bientôt dans votre code. Une fois que vous avez indiqué votre clé API, cliquez sur le **demande/réponse** situé dans le **le point de terminaison par défaut** section en dessous de la clé.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-33.png)

    > [!NOTE] 
    > Si vous cliquez sur Test dans cette page, vous serez en mesure d’entrer des données d’entrée et afficher la sortie. Entrez le **jour** et **heure**. Laissez le **produit** entrée vide. Puis cliquez sur le **confirmer** bouton. La sortie au bas de la page affiche l’objet JSON qui représente la probabilité de chaque produit qui est le choix.

29. Une nouvelle page web s’ouvre, affichant les instructions et des exemples sur la structure de requête requis par Machine Learning Studio. Copie le **URI de requête** affichés dans cette page, dans votre bloc-notes.

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-34.png)

Vous avez maintenant créé un système de machine learning qui fournit le produit plus susceptible d’être vendus en fonction des données historiques d’achat, mis en corrélation avec l’heure de la journée et le jour de l’année.

Pour appeler le service web, vous devez l’URL pour le point de terminaison de service et une clé d’API pour le service. Cliquez sur le **consommer** onglet, dans le menu supérieur.

Le **consommation** page d’informations affiche les informations que vous devez appeler le service web à partir de votre code. Effectuez une copie de la **clé primaire** et le **demande-réponse** URL. Vous en aurez besoin dans le chapitre suivant.

## <a name="chapter-5---setting-up-the-unity-project"></a>Chapitre 5 : configuration du projet Unity

Configurer et tester votre casque immersives de réalité mixte.

> [!NOTE]
>  Vous allez **pas** nécessitent des contrôleurs de mouvement pour ce cours. Si vous avez besoin de prendre en charge de paramétrage le casque immersives, veuillez cliquer [ici](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).

1.  Ouvrez **Unity** et créez un projet Unity appelé **MR\_MachineLearning.** Assurez-vous que le type de projet est défini sur **3D**.

2.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à ***modifier* > *préférences*** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

3.  Ensuite, accédez à ***fichier* > *paramètres de Build*** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le ***plateforme de commutation*** bouton.

4.  Assurez-vous également que :

    1.  **Équipement cible** a la valeur **n’importe quel appareil**.

        > Pour le Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.

    2.  **Type de build** a la valeur **D3D**.

    3.  **Kit de développement logiciel** a la valeur **dernière installé**.

    4.  **Version de Visual Studio** a la valeur **dernière installé**.

    5.  **Générez et exécutez** a la valeur **ordinateur Local**.

    6.  Ne vous inquiétez pas sur la configuration de **scènes** dès que ces éléments sont fournis plus loin.

    7.  Les autres paramètres doivent être conservées comme valeur par défaut pour l’instant.

        ![Configuration du projet Unity](images/AzureLabs-Lab7-35.png)

5.  Dans le **paramètres de Build** fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le **inspecteur** se trouve. 

6. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1.  Dans le **autres paramètres** onglet :

        1.  **Écriture de scripts** **Version du Runtime** doit être **expérimental** (équivalent .NET 4.6)

        2. **Script principal** doit être ***.NET***

        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**

            ![Configuration du projet Unity](images/AzureLabs-Lab7-36.png)

    2.  Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        - **InternetClient**

            ![Configuration du projet Unity](images/AzureLabs-Lab7-37.png)

    3.  Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté

        ![Configuration du projet Unity](images/AzureLabs-Lab7-38.png)

    

6.  Dans **paramètres de Build** *Unity C#*  projets est n’est plus grisée ; Cochez la case à cocher en regard de cela. 

7.  Fermez la fenêtre Paramètres de Build.

8.  Enregistrer votre projet (**fichier > Enregistrer le projet**).

## <a name="chapter-6---importing-the-mlproducts-unity-package"></a>Chapitre 6 - importation du Package MLProducts Unity

Pour ce cours, vous devez télécharger un Package de ressource Unity appelé [ **Azure-MR-307.unitypackage**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/307-Scene-Setup.unitypackage). Ce package est livrée avec une scène, tous les objets d’autrement prédéfinis, par conséquent, vous pouvez vous concentrer sur l’obtention de tout fonctionne. Le **ShelfKeeper** script est fourni, mais ne conserve que les variables publiques, à des fins de structure de programme d’installation de scène. Vous devez effectuer toutes les autres sections. 

Pour importer ce package :

1.  Avec le tableau de bord Unity devant vous, cliquez sur **actifs** dans le menu en haut de l’écran, puis cliquez sur **importer un Package, le Package personnalisé**.

    ![Importation du Package MLProducts Unity](images/AzureLabs-Lab7-39.png)

2.  Utilisez le sélecteur de fichiers pour sélectionner le **Azure-MR-307.unitypackage** du package et cliquez sur **Open**.

3.  Une liste des composants de cette ressource s’affichera pour vous. Confirmez l’importation en cliquant sur **importer**.

    ![Importation du Package MLProducts Unity](images/AzureLabs-Lab7-40.png)

4.  Une fois l’importation terminée, vous remarquerez que certains nouveaux dossiers apparues dans votre Unity **panneau projet**. Ce sont les modèles 3D et les matériaux respectifs qui font partie de la scène prédéfinie, sur que vous allez travailler. Vous allez écrire la majorité du code dans ce cours.

    ![Importation du Package MLProducts Unity](images/AzureLabs-Lab7-41.png)

5.  Dans le **panneau projet** dossier, cliquez sur le **scènes** dossier et double cliquez sur la scène à l’intérieur (appelé **MR_MachineLearningScene**). La scène s’ouvre (voir l’image ci-dessous). Si les losanges rouge sont manquants, cliquez simplement sur le **Gizmos** bouton, dans la partie supérieure droite de la **Panneau de jeu**.

    ![Importation du Package MLProducts Unity](images/AzureLabs-Lab7-44.png)

## <a name="chapter-7---checking-the-dlls-in-unity"></a>Chapitre 7 - vérification des DLL dans Unity

Pour tirer parti de l’utilisation des bibliothèques JSON (utilisé pour sérialiser et désérialiser), une DLL Newtonsoft a été implémentée avec le package dans que vous est proposée. La bibliothèque doit avoir la configuration correcte, même si elle est valent (en particulier si vous rencontrez des problèmes avec le code ne fonctionne ne pas). 

Pour ce faire :

-  Cliquez sur le fichier Newtonsoft dans le dossier de plug-ins et examinez le **panneau Inspecteur**. Assurez-vous que **Any plateforme** est coché. Accédez à la **onglet UWP** et vérifiez également **ne pas traiter les** est coché.

    ![L’importation des DLL dans Unity](images/AzureLabs-Lab7-48.png)

## <a name="chapter-8---create-the-shelfkeeper-class"></a>Chapitre 8 - créer la classe ShelfKeeper

Le **ShelfKeeper** classe héberge des méthodes qui contrôlent l’interface utilisateur et les produits générés dans la scène.

Dans le cadre du package importé, vous vous ont été données cette classe, même si elle est incomplète. Il est maintenant temps de terminer cette classe :

1.  Double-cliquez sur le **ShelfKeeper** de script, dans le **Scripts** dossier, pour l’ouvrir avec **Visual Studio 2017**.

2.  Remplacez tout le code existant dans le script avec le code suivant, qui définit la date et l’heure et dispose d’une méthode pour afficher un produit.

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

3.  Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.

4.  Revenez dans l’éditeur Unity, vérifiez que le **ShelfKeeper** classe ressemble à la ci-dessous :

    ![Créer la classe ShelfKeeper](images/AzureLabs-Lab7-51.png)

    > [!IMPORTANT]
    > Si votre script n’a pas les cibles de référence (par exemple, *Date (texte de maillage)*), faites simplement glisser les objets correspondants de la **hiérarchie panneau**, dans les champs de la cible. Voir ci-dessous pour savoir plus, si nécessaire :
    > 
    > 1.  Ouvrez le **Spawn Point** de tableau dans le **ShelfKeeper** script composant par clic gauche il. Une sous-section apparaît appelée **taille**, ce qui indique la taille du tableau. Type **3** dans la zone de texte suivant pour **taille** et appuyez sur **entrée**, et trois emplacements seront créés sous.
    > 2. Dans le **hiérarchie** développez la **affichage temps** objet (en cliquant dessus à la flèche en regard de celle-ci). Ensuite cliquez sur le ***Main Camera*** depuis le **hiérarchie**, de sorte que le **inspecteur** montre ses informations.
    > 3. Sélectionnez le **caméra principale** dans le **hiérarchie panneau**. Faites glisser le **Date** et **temps** objets à partir de la **Panneau de la hiérarchie** à la **texte de la Date** et **texte moment** emplacements au sein de la **inspecteur** de la **Main Camera** dans le **ShelfKeeper** composant.
    > 4. Faites glisser le **Spawn Points** à partir de la **Panneau de la hiérarchie** (sous le *étagère* objet) à la **3** **élément**référence cibles sous le **Spawn Point** de tableau, comme indiqué dans l’image.
    > 
    >     ![Créer la classe ShelfKeeper](images/AzureLabs-Lab7-52.png)

## <a name="chapter-9---create-the-productprediction-class"></a>Chapitre 9 - créer la classe ProductPrediction

La classe suivante, vous allez créer est la **ProductPrediction** classe.

Cette classe est chargée de :

-   Interrogation de la **Service Machine Learning** instance, qui fournit la date et heure actuelles.

-   La désérialisation de la réponse JSON en données exploitables.

-   Interprétation des données, récupérer les produits recommandés 3.

-   Appel de la **ShelfKeeper** méthodes pour afficher les données dans la scène de la classe.

Pour créer cette classe :

1.  Accédez à la **Scripts** dossier, dans le **panneau projet**.

2.  Avec le bouton droit dans le dossier, **créer** > **C\# Script**. Appeler le script **ProductPrediction**.

3.  Double-cliquez sur le nouveau **ProductPrediction** script pour l’ouvrir avec **Visual Studio 2017**.

4.  Si le **Modification de fichier détectée** boîte de dialogue s’affiche, cliquez sur ***recharger la Solution**.

5.  Ajoutez les espaces de noms suivantes au début de la classe ProductPrediction :

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

6.  À l’intérieur de la **ProductPrediction** classe insérer les deux objets suivants qui sont composées d’un nombre de classes imbriquées. Ces classes sont utilisées pour sérialiser et désérialiser l’objet JSON pour le Service Machine Learning.

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

7.  Puis ajoutez les variables suivantes au-dessus du code précédent (afin que le JSON liés code figure au bas du script, tous les autres code ci-dessous et en dehors de la façon) :

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
    > Veillez à insérer le **clé primaire** et **point de terminaison de requête-réponse**, à partir du portail de formation Machine, dans les variables ici. Les images ci-après montrent où vous aurait fallu la clé et le point de terminaison. 
    >  
    > ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-53-1.png)
    >
    > ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-53-2.png)

8.  Insérez ce code dans le **Start()** (méthode). Le **Start()** méthode est appelée lors de l’initialisation de la classe :

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

9.  Voici la méthode qui Récupère la date et l’heure à partir de Windows et le convertit en un format que notre expérience d’apprentissage Machine peut utiliser pour comparer avec les données stockées dans la table.

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

10. Vous pouvez **supprimer** le **Update()** étant donné que cette classe ne l’utilise pas de méthode.

11. Ajoutez la méthode suivante qui sera de communiquer la date et heure actuelles au point de terminaison Machine Learning et de recevoir une réponse au format JSON.

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

            // Serialise the request
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

12. Ajoutez la méthode suivante, qui est responsable de la désérialisation de la réponse JSON et communique le résultat de la désérialisation pour le **ShelfKeeper** classe. Ce résultat sera les noms des trois éléments prévues de vendre le plus à la date et heure actuelles. Insérez le code ci-dessous dans le **ProductPrediction** (classe), sous la méthode précédente.

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

13. Enregistrer **Visual Studio** et revenez **Unity**.

14. Faites glisser le **ProductPrediction** classe le script à partir de la **Script** dossier, sur le **Main Camera** objet.

15. Enregistrer votre projet et scène **fichier** > ***enregistrer la scène* / *fichier***   >  **Enregistrer le projet**.

## <a name="chapter-10---build-the-uwp-solution"></a>Chapitre 10 - générer la Solution UWP

Il est maintenant temps de générer votre projet comme une solution UWP, afin qu’il peut s’exécuter comme une application autonome.

Pour générer :

1.  Enregistrer la scène actuelle en cliquant sur **fichier** **enregistrer les scènes**.

2.  Accédez à **fichier** **les paramètres de génération**

3.  Cochez la case appelée **Unity C\# projets** (Ceci est important, car il vous permettra de modifier les classes après de la build est terminée).

4.  Cliquez sur **ajouter des scènes Open**,

5.  Cliquez sur **Build**.

    ![Générez la Solution UWP](images/AzureLabs-Lab7-54.png)

6.  Vous êtes invité à sélectionner le dossier dans lequel vous souhaitez générer la Solution.

7.  Créer un **génère** dossier et dans ce dossier, créez un autre dossier avec un nom approprié de votre choix.

8.  Cliquez sur votre nouveau dossier, puis **sélectionner le dossier**à commencer la build à cet emplacement.

    ![Générez la Solution UWP](images/AzureLabs-Lab7-55.png)

    ![Générez la Solution UWP](images/AzureLabs-Lab7-56.png)

9.  Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).

## <a name="chapter-11---deploy-your-application"></a>Chapitre 11 - déployer votre Application

Pour déployer votre application :

1.  Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.

2.  Visual Studio ouvert, vous devez restaurer les Packages NuGet, ce qui peut être effectué via un clic droit sur votre solution MachineLearningLab_Build, à partir de l’Explorateur de solutions (situé à droite de Visual Studio), puis cliquez sur Restaurer les Packages NuGet :

    ![Ajout de Packages NuGet](images/AzureLabs-Lab7-57.png)

3.  Dans, sélectionnez la Configuration de Solution **déboguer**.

4.  Dans la plateforme de Solution, sélectionnez **x86**, **ordinateur Local**. 

    > Pour le Microsoft HoloLens, il peut s’avérer plus facile d’affecter à ce *Machine distante*, de sorte que vous ne sont pas attachés à votre ordinateur. Cependant, vous devez également effectuer les opérations suivantes :
    > - Connaître le **adresse IP** de votre HoloLens, ce qui se trouve dans le *Paramètres > réseau & Internet > Wi-Fi > Options avancées*; IPv4 est l’adresse que vous devez utiliser. 
    > - Vérifiez **Mode développeur** est **sur**; trouvé dans *Paramètres > mise à jour & sécurité > pour les développeurs*.

    ![Ajout de Packages NuGet](images/AzureLabs-Lab7-58.png)

5.  Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre PC.

6.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.

Lorsque vous exécutez l’application de réalité mixte, vous verrez le banc qui a été configuré dans votre scène Unity, et à partir de l’initialisation, seront extraites les données que vous configurez dans Azure. Les données seront désérialisées au sein de votre application, et fournirons visuellement, en tant que trois modèles sur le banc les trois premiers résultats pour votre date et heure actuelles.


## <a name="your-finished-machine-learning-application"></a>Votre application de Machine Learning terminée
 
Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’Azure Machine Learning pour effectuer des prédictions de données et l’afficher dans votre scène.

![Ajout de Packages NuGet](images/AzureLabs-Lab7-0.png)

## <a name="exercise"></a>Exercice

**Exercice 1**

Faire des essais avec l’ordre de tri de votre application et afficher les prédictions de trois bas en rayon, comme ces données potentiellement serait utiles également.

**Exercice 2**

À l’aide de **Tables Azure** remplir une nouvelle table avec les informations météorologiques et créer une expérience à l’aide de données.
