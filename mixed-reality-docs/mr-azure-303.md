---
title: MR et Azure 303 - langage naturel (LUIS)
description: Terminer ce cours pour apprendre à implémenter Azure Intelligence Service LUIS (Language Understanding) au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, service d’intelligence language understanding, luis, vr immersives, hololens,
ms.openlocfilehash: fb00fe9079e49a7ada507e7407ef45fa7eeb0d7e
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595914"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-and-azure-303-natural-language-understanding-luis"></a>MR et Azure 303 : Compréhension du langage naturel (LUIS)

Dans ce cours, vous allez apprendre à intégrer la compréhension du langage dans une application de réalité mixte à l’aide d’Azure Cognitive Services, avec l’API de compréhension du langage.

![résultat de laboratoire](images/AzureLabs-Lab3-000.png)

*Reconnaissance vocale (LUIS)* est un service Microsoft Azure, qui fournit aux applications la possibilité d’effectuer la signification en dehors de l’entrée d’utilisateur, telles que via extraction qu’une personne peut le souhaitez, dans leurs propres mots. Cela est possible via machine learning, qui comprend et apprend les informations d’entrée et qui peut ensuite répondre avec des informations détaillées et pertinentes. Pour plus d’informations, visitez le [page de Azure LUIS (Language Understanding)](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/).

Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :

1.  Capturer la voix d’entrée d’utilisateur, à l’aide du Microphone relié au casque immersif. 
2.  Envoyer la dictée capturée le *Azure Language Understanding Intelligent Service* (*LUIS*). 
3.  Avoir extrait LUIS ce qui signifie que l’envoi d’informations, qui sera analysé et tente de déterminer que l’intention de demande de l’utilisateur sera.

Développement incluent la création d’une application où l’utilisateur sera en mesure d’utiliser la voix et/ou les regards pour modifier la taille et la couleur des objets dans la scène. L’utilisation de contrôleurs de mouvement n’est pas traitée.

Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception. Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity. Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.

Soyez prêt à former LUIS plusieurs fois, ce qui est couvert dans [chapitre 12](#chapter-12--improving-your-luis-service). Vous obtiendrez meilleurs résultats les plus temps que Luis a été formé.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>MR et Azure 303 : Compréhension du langage naturel (LUIS)</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens. Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens. Lorsque vous utilisez HoloLens, vous pouvez remarquer quelques echo durant la capture de la voix.

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
- Un ensemble de casque avec un microphone intégré (si le casque n’a pas un mic intégré et les haut-parleurs)
- Accès à Internet pour le programme d’installation Azure et l’extraction de LUIS

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération). 
2.  Pour permettre à votre machine pour activer la dictée, accédez à **Windows Paramètres > confidentialité > vocale, la saisie manuscrite & tapant** et appuyez sur le bouton **sur Activer le services de reconnaissance vocale et les suggestions en tapant**.
3.  Le code dans ce didacticiel vous permettra d’enregistrer à partir de la **par défaut un appareil Microphone** sur votre ordinateur. Assurez-vous que l’appareil Microphone par défaut est défini comme celui que vous souhaitez utiliser pour capturer votre voix.
4.  Si votre casque a un microphone intégré, assurez-vous que l’option *« Lorsque j’ai wear mon casque, basculez vers casque mic »* est activé dans le *Portal de réalité mixte* paramètres.

    ![Configuration de casque immersive](images/AzureLabs-Lab3-00.png)

## <a name="chapter-1--setup-azure-portal"></a>Chapitre 1 : configurer le portail Azure

Pour utiliser le *Language Understanding* service dans Azure, vous devez configurer une instance du service à être mis à disposition de votre application.

1.  Connectez-vous à la [Azure Portal](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *Language Understanding*, puis cliquez sur **entrée**. 

    ![Créer une ressource de LUIS](images/AzureLabs-Lab3-01.png)

    > [!NOTE]
    > Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.
 
3.  La nouvelle page à droite fournit une description du service de reconnaissance vocale. En bas à gauche de cette page, sélectionnez le **créer** bouton, pour créer une instance de ce service.

    ![Création du service LUIS - notice légale](images/AzureLabs-Lab3-02.png)
 
4.  Une fois que vous avez cliqué sur Créer :

    1. Insérez votre souhaitée **nom** pour cette instance de service.
    2. Sélectionnez un **abonnement**.
    3. Sélectionnez le **niveau tarifaire** appropriés pour vous, s’il s’agit du premier temps à créer un *Service LUIS*, un niveau gratuit (nommé F0) doit être disponible pour vous. L’allocation gratuite doit être plus que suffisante pour ce cours.
    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs). 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions.
    6. Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.
    7. Sélectionnez **Créer**.

        ![Créer un service LUIS - entrée d’utilisateur](images/AzureLabs-Lab3-03.png)
 
5.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.
6.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail. 
 
    ![Nouvelle image de notification Azure](images/AzureLabs-Lab3-04.png)

7.  Cliquez sur la notification pour Explorer votre nouvelle instance de Service.

    ![Notification de création de ressources](images/AzureLabs-Lab3-05.png)
 
8.  Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. Vous êtes redirigé vers votre nouvelle instance de service LUIS. 
 
    ![Accès aux clés de LUIS](images/AzureLabs-Lab3-06.png)

9.  Dans ce didacticiel, votre application devra effectuer des appels à votre service, par l’intermédiaire à l’aide de la clé d’abonnement de votre service.
10. À partir de la *Guide de démarrage rapide* page, de votre *API LUIS* de service, accédez à la première étape, *récupérez vos clés*, puis cliquez sur **clés** (vous pouvez également parvenir en cliquant sur le lien hypertexte bleu clés, situé dans le menu de navigation de services, indiqué par l’icône de clé). Cela permet de révéler votre service *clés*.
11. Effectuez une copie de l’une des clés affichées, car vous en aurez besoin plus loin dans votre projet. 
12. Dans le *Service* page, cliquez sur *portail Language Understanding* d’être redirigé vers la page Web que vous utiliserez pour créer votre nouveau Service, au sein de l’application LUIS. 

## <a name="chapter-2--the-language-understanding-portal"></a>Chapitre 2 – portail Language Understanding

Dans cette section, vous allez apprendre à rendre une application LUIS sur LUIS Portal. 

> [!IMPORTANT]
> Notez que la configuration la *entités*, *intentions*, et *énoncés* au sein de ce chapitre n'est que la première étape dans la création de votre service LUIS : vous devrez également reformer le service, plusieurs fois, par conséquent, pour le rendre plus précis. Reformation de votre service est couvert dans le [dernier chapitre](#chapter-12--improving-your-luis-service) de ce cours, par conséquent, assurez-vous de suivre la procédure.

1.  Lorsque vous atteignez le *portail Language Understanding*, vous devrez peut-être vous connecter, si vous n’êtes pas déjà fait, avec les mêmes informations d’identification que votre portail Azure. 

    ![Page de connexion de LUIS](images/AzureLabs-Lab3-07.png)
 
2.  S’il s’agit de la première fois à l’aide de LUIS, vous devez faire défiler jusqu’en bas de la page d’accueil, à rechercher, puis cliquez sur le **application LUIS créer** bouton.

    ![Créer la page d’application LUIS](images/AzureLabs-Lab3-08.png)
 
3.  Une fois connecté, cliquez sur **mes applications** (si vous n’êtes pas dans cette section). Vous pouvez ensuite cliquer sur **créer une nouvelle application**.

    ![LUIS - mon image d’applications](images/AzureLabs-Lab3-09.png)
 
4.  Donnez à votre application un *nom*.
5.  Si votre application est censée pour comprendre une langue différente de l’anglais, vous devez modifier le *Culture* à la langue appropriée.
6.  Vous pouvez également y ajouter un *Description* de votre nouvelle application LUIS.

    ![LUIS - créer une application](images/AzureLabs-Lab3-10.png)

7.  Une fois que vous appuyez sur **fait**, vous devez entrer le *Build* page de votre nouvelle *LUIS* application.
8.  Il existe quelques concepts importants ici :

    -   *Intention*, représente la méthode qui sera appelée après une requête à partir de l’utilisateur. Un *intention* peut avoir un ou plusieurs *entités*.
    -   *Entité*, est un composant de la requête qui décrit les informations relatives à la *intention*.
    -   *Énoncés*, sont des exemples de requêtes fournies par le développeur, ce LUIS utilisera pour effectuer l’apprentissage lui-même.

Si ces concepts ne sont pas parfaitement effacer, ne vous inquiétez pas, comme ce cours sera clarifier les davantage dans ce chapitre.

Vous allez commencer en créant le *entités* nécessaire pour générer ce cours.

9.  Sur le côté gauche de la page, cliquez sur *entités*, puis cliquez sur **créer entité**.

    ![Créer une nouvelle entité](images/AzureLabs-Lab3-11.png)

10. Appelez la nouvelle entité *couleur*, définissez son type sur *Simple*, puis appuyez sur **fait**.

    ![Créer une entité simple - couleur](images/AzureLabs-Lab3-12.png)
 
11. Répétez ce processus pour créer trois (3) plus Simple entités nommées :

    -   *upsize*
    -   *downsize*
    -   *target*

Le résultat doit ressembler à l’image ci-dessous :

![Résultat de la création d’entités](images/AzureLabs-Lab3-13.png)
 
À ce stade vous pouvez commencer à créer *intentions*. 

> [!WARNING]
> Ne supprimez pas le **aucun** intention.

12. Sur le côté gauche de la page, cliquez sur **intentions**, puis cliquez sur **créer nouveau intention**.

    ![Créer nouveau intentions](images/AzureLabs-Lab3-14.png)

13. Appelez la nouvelle *intention* **ChangeObjectColor**.

    > [!IMPORTANT]
    > Cela *intention* nom est utilisé dans le code plus loin dans ce cours, par conséquent, pour de meilleurs résultats, utilisez ce nom exactement comme prévu.

Après avoir confirmé le nom que vous serez dirigé vers la Page d’intentions.

![LUIS - page d’intentions](images/AzureLabs-Lab3-15.png)

Vous remarquerez qu’il existe une zone de texte vous invitant à type 5 ou plus différent *énoncés*.

> [!NOTE]
> LUIS convertit tous les énoncés en minuscules.

14. Insérez le code suivant *énoncé* dans la zone de texte supérieur (actuellement avec le texte *Type exemples environ 5...* ), puis appuyez sur **entrée**:

```
The color of the cylinder must be red
```

Vous remarquerez que la nouvelle *énoncé* s’affiche dans une liste en dessous.

Suivant le même processus, insérez les énoncés suivants de six (6) :

```
make the cube black

make the cylinder color white

change the sphere to red

change it to green

make this yellow

change the color of this object to blue
```

Pour chaque énoncé que vous avez créé, vous devez identifier quels mots doivent être utilisés par LUIS en tant qu’entités. Dans cet exemple, vous avez besoin étiqueter toutes les couleurs en tant qu’un *couleur* référence d’entité et toutes les la possible sur une cible, car un *cible* entité.

15. Pour ce faire, essayez de cliquer sur le mot *cylindre* dans la première énoncé, puis sélectionnez *cible*.

    ![Identifier les cibles d’énoncé](images/AzureLabs-Lab3-16.png)
 
16. Cliquez maintenant sur le mot *rouge* dans la première énoncé, puis sélectionnez *couleur*.

    ![Identifier les entités de l’énoncé](images/AzureLabs-Lab3-17.png)
 
17. En outre, l’étiquette de la ligne suivante où *cube* doit être un *cible*, et *noir* doit être un *couleur*. Notez également l’utilisation des mots *'this'*, *« it »*, et *'cet objet'*, ce qui nous mettons à disposition, par conséquent, pour que les types de cible non spécifique disponibles également. 

18. Répétez le processus ci-dessus jusqu'à ce que tous les énoncés ont les entités étiquetées. Voir l’image si vous avez besoin d’aide ci-dessous.

    > [!TIP]
    > Lors de la sélection de mots à les étiqueter en tant qu’entités :
    > - Pour les mots isolés cliquez simplement sur eux.
    > - Pour un ensemble de deux ou plusieurs mots, cliquez sur au début, à la fin de l’ensemble.

    > [!NOTE]
    > Vous pouvez utiliser la *jetons vue* bouton bascule pour basculer entre les **entités ou jetons afficherez**!

19. Les résultats doivent être comme indiqué dans les images ci-dessous, montrant la **entités ou jetons afficherez**:

    ![Jetons et des vues d’entités](images/AzureLabs-Lab3-18.png)
  
20. À ce stade appuyez sur le **Train** bouton dans l’angle supérieur droit de la page et attendez que l’indicateur round petit dessus en vert. Cela indique que LUIS a été correctement formé pour reconnaître cette intention.

    ![Train LUIS](images/AzureLabs-Lab3-19.png)
 
21. En guise d’exercice pour vous, créer une intention de nouveau appelée **ChangeObjectSize**, à l’aide d’entités *cible*, *migrer*, et *réduire*.
22. Suivant le même processus que l’intention précédente, insérez les énoncés suivants huit (8) pour *taille* modifier :

    ```
    increase the dimensions of that

    reduce the size of this

    i want the sphere smaller

    make the cylinder bigger

    size down the sphere

    size up the cube

    decrease the size of that object

    increase the size of this object
    ```

23. Le résultat doit être celle présentée dans l’image ci-dessous :

    ![Le programme d’installation les jetons ChangeObjectSize / entités](images/AzureLabs-Lab3-20.png) 

24. Une fois les deux modes, **ChangeObjectColor** et **ChangeObjectSize**, ont été créés et formé, cliquez sur le **publier** situé en haut de la page.

    ![Publier le service LUIS](images/AzureLabs-Lab3-21.png)

25. Sur le *publier* page, vous allez finaliser et publier votre application LUIS afin qu’il est accessible par votre code.

    1. Définir la liste *Publish To* comme **Production**.
    2. Définir le *fuseau horaire* sur votre fuseau horaire.
    3. Cochez la case **inclure tous les prédite scores intentions**.
    4. Cliquez sur **publier à l’emplacement de Production**.

        ![Paramètres de publication](images/AzureLabs-Lab3-22.png)

26. Dans la section *ressources et les clés*:

    1.  Sélectionnez la région que vous définissez pour l’instance de service dans le portail Azure.
    2.  Vous remarquerez une **Starter_Key** élément ci-dessous, ignorez-la.
    3.  Cliquez sur **ajouter une clé** et insérez le *clé* que vous avez obtenue dans le portail Azure lorsque vous avez créé votre instance de Service. Si votre Azure et le portail de LUIS sont connectés au même utilisateur, vous bénéficiez de listes déroulantes pour *nom_client*, *nom de l’abonnement*et le *clé* vous souhaitez utiliser () aura le même nom que vous avez fourni précédemment dans le portail Azure.

    > [!IMPORTANT] 
    > En dessous *point de terminaison*, effectuez une copie du point de terminaison correspondant à la clé que vous avez inséré, vous allez bientôt l’utiliser dans votre code.
 
## <a name="chapter-3--set-up-the-unity-project"></a>Chapitre 3 : configurer le projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **New**. 

    ![Démarrer un nouveau projet Unity.](images/AzureLabs-Lab3-24.png)

2.  Vous devez maintenant fournir un nom de projet Unity, insérer **MR_LUIS**. Assurez-vous que le type de projet est défini sur **3D**. Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![Fournissent des détails pour un projet Unity.](images/AzureLabs-Lab3-25.png)
 
3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Allez à modifier > Préférences, puis à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![Mettre à jour les préférences de l’éditeur de script.](images/AzureLabs-Lab3-26.png)
 
4.  Ensuite, accédez à **fichier > Paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **plateforme basculer** bouton.

    ![Fenêtre Paramètres, plateforme de commutation à UWP de la génération.](images/AzureLabs-Lab3-27.png)
 
5.  Accédez à **fichier > Paramètres de Build** et vous assurer que :

    1. **Équipement cible** a la valeur **n’importe quel appareil**

        > Pour le Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.

    2. **Type de build** a la valeur **D3D**
    3. **Kit de développement logiciel** a la valeur **dernière installé**
    4. **Version de Visual Studio** a la valeur **dernière installé**
    5. **Générez et exécutez** est défini sur **ordinateur Local**
    6. Enregistrer la scène et l’ajouter à la build.

        1. Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.
        
            ![Cliquez sur Ajouter un bouton scènes ouvert](images/AzureLabs-Lab3-28.png)

        2. Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![Créer un nouveau dossier de scripts](images/AzureLabs-Lab3-29.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **MR_LuisScene**, puis appuyez sur **enregistrer**.

            ![Donnez un nom à nouvelle scène.](images/AzureLabs-Lab3-30.png)

    7. Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.

6. Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve. 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab3-31.png) 
 
7. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1. Dans le **autres paramètres** onglet :

        1. **Version du Runtime de script** doit être **Stable** (équivalent .NET 3.5).
        2. **Script principal** doit être **.NET**
        3. **Niveau de compatibilité d’API** doit être **.NET 4.6**

            ![Mettre à jour les autres paramètres.](images/AzureLabs-Lab3-32.png)
      
    2. Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        1. **InternetClient**
        2. **Microphone**

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab3-33.png)

    3. Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.

        ![Mettre à jour les paramètres de R X.](images/AzureLabs-Lab3-34.png)

8.  Dans *paramètres de Build* _Unity C#_  projets est n’est plus grisée ; Cochez la case à cocher en regard de cela. 
9.  Fermez la fenêtre Paramètres de Build.
10. Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).

## <a name="chapter-4--create-the-scene"></a>Chapitre 4 : créer la scène

> [!IMPORTANT]
> Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20303%20-%20Natural%20language%20understanding/Azure-MR-303.unitypackage), importez-le dans votre projet comme un [Package personnalisé ](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 5](#chapter-5--create-the-microphonemanager-class). 

1.  Avec le bouton droit dans une zone vide de la *hiérarchie panneau*, sous **objet 3D**, ajoutez un **plan**.

    ![Créer un plan.](images/AzureLabs-Lab3-35.png)

2.  N’oubliez pas que lorsque vous cliquez sur dans le *hiérarchie* à nouveau pour créer des objets de plus, si vous avez toujours le dernier objet sélectionné, l’objet sélectionné sera le parent de votre nouvel objet. Éviter ce problème clic gauche dans un espace vide dans la hiérarchie et puis effectuant un clic droit.

3.  Répétez la procédure ci-dessus pour ajouter les objets suivants :

    1. *Sphere*
    2. *Cylindre*
    3. *Cube*
    4. *Texte 3D*

4.  La scène qui en résulte *hiérarchie* doit être semblable à celui de l’image ci-dessous :

    ![Paramètres de hiérarchie de scène.](images/AzureLabs-Lab3-36.png)
 
5.  Cliquez sur le **Main Camera** pour le sélectionner, examinez le *panneau Inspecteur* vous verrez l’objet caméra avec toutes le ses composants.
6.  Cliquez sur le **ajouter un composant** bouton situé tout en bas de la *panneau Inspecteur*.

    ![Ajouter une Source Audio](images/AzureLabs-Lab3-37.png)
 
7.  Recherchez le composant appelé *Audio Source*, comme indiqué ci-dessus.
8.  Assurez-vous également que le *transformer* composant de la caméra principale est (0,0,0), cela est possible en appuyant sur la **ENGRENAGE** icône en regard de la caméra *transformer* composant et en sélectionnant **réinitialiser**. Le *transformer* composant doit alors ressembler :

    1.  *Position* a la valeur **0, 0, 0**.
    2.  *Rotation* a la valeur **0, 0, 0**.

    > [!NOTE] 
    > Pour le Microsoft HoloLens, vous devez également modifier les paramètres suivants, qui font partie de la **caméra** composant, qui se trouve sur votre **Main Camera**:
    > - **Effacer les indicateurs :** Couleur unie.
    > - **Arrière-plan** ' noir, Alpha 0' – couleur hexadécimale : #00000000.

9.  Cliquez sur le **plan** pour le sélectionner. Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :

    |       | Transformer - *Position* |       |
    |:-----:|:----------------------:|:-----:|
    | **X** | **Y**                  | **Z** |
    | 0     | -1                     | 0     |


10. Cliquez sur le **sphère** pour le sélectionner. Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :

    |       | Transformer - *Position* |       |
    |:-----:|:----------------------:|:-----:|
    | **X** | **Y**                  | **Z** |
    | 2     | 1                      | 2     |

11. Cliquez sur le **cylindre** pour le sélectionner. Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :

    |       | Transformer - *Position* |       |
    |:-----:|:----------------------:|:-----:|
    | **X** | **Y**                  | **Z** |
    | -2    | 1                      | 2     |

12. Cliquez sur le **Cube** pour le sélectionner. Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :

    |        | Transformer - *Position* |       |  \| |       | Transformer - *Rotation* |       |
    |:------:|:----------------------:|:-----:|:---:|:-----:|:----------------------:|:-----:|
    | **X** | **Y**                   | **Z** |  \| | **X** | **Y**                  | **Z** |
    | 0     | 1                       | 4     |  \| | 45    | 45                     | 0     | 

13. Cliquez sur le **nouveau texte** objet pour le sélectionner. Dans le *panneau Inspecteur* définir le *transformer* composant avec les valeurs suivantes :

    |       | Transformer - *Position* |       |  \| |       | Transformer - *mise à l’échelle* |       |
    |:-----:|:----------------------:|:-----:|:---:|:-----:|:-------------------:|:-----:|
    | **X** | **Y**                  | **Z** |  \| | **X** | **Y**               | **Z** |
    | -2    | 6                      | 9     |  \| | 0.1   | 0.1                 | 0.1   | 

14. Modification **la taille de police** dans le **texte Mesh** à **50**.
15. Modifier le *nom* de la **maillage de texte** objet **dictée texte**.

    ![Création d’objet de texte 3D](images/AzureLabs-Lab3-38.png)
 
16. Votre structure de hiérarchie le panneau de configuration doit maintenant ressembler à ceci :

    ![texte de maillage dans la vue de la scène](images/AzureLabs-Lab3-38b.png)


17. La scène finale doit ressembler à l’image ci-dessous :

    ![La vue de la scène.](images/AzureLabs-Lab3-39.png)
    
 
## <a name="chapter-5--create-the-microphonemanager-class"></a>Chapitre 5 : créer la classe MicrophoneManager

Le premier Script que vous vous apprêtez à créer est le *MicrophoneManager* classe. Après cela, vous allez créer le *LuisManager*, le *comportements* (classe) et enfin la *les regards* classe (vous pouvez créer tous ces maintenant, bien que sera traité en tant que vous atteindre chaque chapitre).

Le *MicrophoneManager* classe est chargée de :

-   Détection du périphérique d’enregistrement attaché à l’ordinateur (selon celui qui est celle par défaut) ou un casque.
-   Capturer l’audio (voix) et la dictée pour stocker en tant que chaîne.
-   Une fois que la voix a été suspendu, soumettez la dictée pour le *LuisManager* classe. 

Pour créer cette classe : 

1.  Avec le bouton droit dans le *Panneau de configuration de projet*, **créer > dossier**. Appelez le dossier **Scripts**. 

    ![Créez le dossier Scripts.](images/AzureLabs-Lab3-40.png)
 
2.  Avec le **Scripts** dossier créé, double-cliquez dessus, pour l’ouvrir. Ensuite, dans ce dossier, avec le bouton droit, **créer > C# Script**. Nommez le script *MicrophoneManager*. 

3.  Double-cliquez sur *MicrophoneManager* pour l’ouvrir avec *Visual Studio*.
4.  Ajoutez les espaces de noms suivantes au début du fichier :

    ```csharp
        using UnityEngine;
        using UnityEngine.Windows.Speech;
    ```

5.  Puis ajoutez les variables suivantes à l’intérieur de la *MicrophoneManager* classe :

    ```csharp
        public static MicrophoneManager instance; //help to access instance of this object
        private DictationRecognizer dictationRecognizer;  //Component converting speech to text
        public TextMesh dictationText; //a UI object used to debug dictation result
    ``` 

6.  Code pour *Awake()* et *Start()* méthodes doit maintenant être ajouté. Il seront appelées lors de l’initialisation de la classe :

    ```csharp
        private void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }

        void Start()
        {
            if (Microphone.devices.Length > 0)
            {
                StartCapturingAudio();
                Debug.Log("Mic Detected");
            }
        }
    ```
 
7.  Maintenant, vous devez la méthode utilisée par l’application à démarrer et arrêter la capture de la voix et transmettez-le à la *LuisManager* (classe), que vous allez générer plus rapidement. 

    ```csharp
        /// <summary>
        /// Start microphone capture, by providing the microphone as a continual audio source (looping),
        /// then initialise the DictationRecognizer, which will capture spoken words
        /// </summary>
        public void StartCapturingAudio()
        {
            if (dictationRecognizer == null)
            {
                dictationRecognizer = new DictationRecognizer
                {
                    InitialSilenceTimeoutSeconds = 60,
                    AutoSilenceTimeoutSeconds = 5
                };

                dictationRecognizer.DictationResult += DictationRecognizer_DictationResult;
                dictationRecognizer.DictationError += DictationRecognizer_DictationError;
            }
            dictationRecognizer.Start();
            Debug.Log("Capturing Audio...");
        }

        /// <summary>
        /// Stop microphone capture
        /// </summary>
        public void StopCapturingAudio()
        {
            dictationRecognizer.Stop();
            Debug.Log("Stop Capturing Audio...");
        }
    ```

8.  Ajouter un *dictée gestionnaire* qui sera appelé lorsque la voix est maintenu. Cette méthode passe le texte de dictée à la *LuisManager* classe.

    ```csharp
        /// <summary>
        /// This handler is called every time the Dictation detects a pause in the speech. 
        /// This method will stop listening for audio, send a request to the LUIS service 
        /// and then start listening again.
        /// </summary>
        private void DictationRecognizer_DictationResult(string dictationCaptured, ConfidenceLevel confidence)
        {
            StopCapturingAudio();
            StartCoroutine(LuisManager.instance.SubmitRequestToLuis(dictationCaptured, StartCapturingAudio));
            Debug.Log("Dictation: " + dictationCaptured);
            dictationText.text = dictationCaptured;
        }

        private void DictationRecognizer_DictationError(string error, int hresult)
        {
            Debug.Log("Dictation exception: " + error);
        }
    ```
 
    > [!IMPORTANT]
    > Supprimer le *Update()* étant donné que cette classe ne l’utilise pas de méthode.

9.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

    > [!NOTE]
    > À ce stade, vous remarquerez une erreur qui apparaissent dans le *volet de Console Unity Editor*. Il s’agit, car le code fait référence le *LuisManager* classe que vous allez créer dans le chapitre suivant.

## <a name="chapter-6--create-the-luismanager-class"></a>Chapitre 6 : créer la classe LUISManager

Il est temps de créer le *LuisManager* (classe), ce qui rend l’appel au service Azure LUIS. 

L’objectif de cette classe consiste à recevoir le texte de dictée à partir de la *MicrophoneManager* classe et l’envoyer à la *API Azure Language Understanding* à analyser.

Cette classe désérialisera le *JSON* réponse et appeler les méthodes appropriées de la *comportements* classe pour déclencher une action.

Pour créer cette classe : 

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir. 
2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**. Nommez le script *LuisManager*. 
3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.
4.  Ajoutez les espaces de noms suivantes au début du fichier :

    ```csharp
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  Vous allez commencer par créer trois classes **à l’intérieur** le *LuisManager* classe (dans le même fichier de script, au-dessus de la *Start()* méthode) qui représentera désérialisé Réponse JSON à partir d’Azure.

    ```csharp
        [Serializable] //this class represents the LUIS response
        public class AnalysedQuery
        {
            public TopScoringIntentData topScoringIntent;
            public EntityData[] entities;
            public string query;
        }

        // This class contains the Intent LUIS determines 
        // to be the most likely
        [Serializable]
        public class TopScoringIntentData
        {
            public string intent;
            public float score;
        }

        // This class contains data for an Entity
        [Serializable]
        public class EntityData
        {
            public string entity;
            public string type;
            public int startIndex;
            public int endIndex;
            public float score;
        }
    ```

6.  Ensuite, ajoutez les variables suivantes à l’intérieur de la *LuisManager* classe :
 
    ```csharp
        public static LuisManager instance;

        //Substitute the value of luis Endpoint with your own End Point
        string luisEndpoint = "https://westus.api.cognitive... add your endpoint from the Luis Portal";
    ```

7.  Veillez à placer votre point de terminaison LUIS maintenant (ce qui vous aurez à partir de votre portail LUIS).

8.  Code pour le *Awake()* méthode doit maintenant être ajouté. Cette méthode est appelée lors de l’initialisation de la classe :

    ```csharp
        private void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }
    ```

9.  Maintenant, vous devez les méthodes de cette application utilise pour envoyer la dictée reçue à partir de la *MicrophoneManager* classe *LUIS*, puis recevoir et désérialiser la réponse. 
10. Une fois que la valeur de l’objectif et les entités associées, ont été déterminées, ils sont passés à l’instance de la *comportements* classe déclenche l’action prévue.

    ```csharp
        /// <summary>
        /// Call LUIS to submit a dictation result.
        /// The done Action is called at the completion of the method.
        /// </summary>
        public IEnumerator SubmitRequestToLuis(string dictationResult, Action done)
        {
            string queryString = string.Concat(Uri.EscapeDataString(dictationResult));

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Get(luisEndpoint + queryString))
            {
                yield return unityWebRequest.SendWebRequest();

                if (unityWebRequest.isNetworkError || unityWebRequest.isHttpError)
                {
                    Debug.Log(unityWebRequest.error);
                }
                else
                {
                    try
                    {
                        AnalysedQuery analysedQuery = JsonUtility.FromJson<AnalysedQuery>(unityWebRequest.downloadHandler.text);

                        //analyse the elements of the response 
                        AnalyseResponseElements(analysedQuery);
                    }
                    catch (Exception exception)
                    {
                        Debug.Log("Luis Request Exception Message: " + exception.Message);
                    }
                }

                done();
                yield return null;
            }
        }
    ```
 
11. Créer une nouvelle méthode appelée *AnalyseResponseElements()* qui lira résultant *AnalysedQuery* et déterminer les entités. Une fois que ces entités sont déterminées, ils seront passés à l’instance de la *comportements* classe à utiliser dans les actions.

    ```csharp
        private void AnalyseResponseElements(AnalysedQuery aQuery)
        {
            string topIntent = aQuery.topScoringIntent.intent;

            // Create a dictionary of entities associated with their type
            Dictionary<string, string> entityDic = new Dictionary<string, string>();

            foreach (EntityData ed in aQuery.entities)
            {
                entityDic.Add(ed.type, ed.entity);
            }

            // Depending on the topmost recognised intent, read the entities name
            switch (aQuery.topScoringIntent.intent)
            {
                case "ChangeObjectColor":
                    string targetForColor = null;
                    string color = null;

                    foreach (var pair in entityDic)
                    {
                        if (pair.Key == "target")
                        {
                            targetForColor = pair.Value;
                        }
                        else if (pair.Key == "color")
                        {
                            color = pair.Value;
                        }
                    }

                    Behaviours.instance.ChangeTargetColor(targetForColor, color);
                    break;

                case "ChangeObjectSize":
                    string targetForSize = null;
                    foreach (var pair in entityDic)
                    {
                        if (pair.Key == "target")
                        {
                            targetForSize = pair.Value;
                        }
                    }

                    if (entityDic.ContainsKey("upsize") == true)
                    {
                        Behaviours.instance.UpSizeTarget(targetForSize);
                    }
                    else if (entityDic.ContainsKey("downsize") == true)
                    {
                        Behaviours.instance.DownSizeTarget(targetForSize);
                    }
                    break;
            }
        }
    ```
 
    > [!IMPORTANT]
    > Supprimer le *Start()* et *Update()* méthodes étant donné que cette classe ne les utiliserez pas.

12. Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

> [!NOTE]
> À ce stade, vous remarquerez plusieurs erreurs survenues dans le *volet de Console Unity Editor*. Il s’agit, car le code fait référence le *comportements* classe que vous allez créer dans le chapitre suivant.

## <a name="chapter-7--create-the-behaviours-class"></a>Chapitre 7 – créer la classe de comportements

Le *comportements* classe déclenche les actions à l’aide d’entités fournies par le *LuisManager* classe.

Pour créer cette classe : 

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir. 
2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**. Nommez le script *comportements*. 
3.  Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.
4.  Puis ajoutez les variables suivantes à l’intérieur de la *comportements* classe :

    ```csharp
        public static Behaviours instance;

        // the following variables are references to possible targets
        public GameObject sphere;
        public GameObject cylinder;
        public GameObject cube;
        internal GameObject gazedTarget;
    ```
 
5.  Ajouter le *Awake()* code de la méthode. Cette méthode est appelée lors de l’initialisation de la classe :

    ```csharp
        void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }
    ```
 
6.  Les méthodes suivantes sont appelées par le *LuisManager* classe (que vous avez créé précédemment) pour déterminer quel objet est la cible de la requête, puis déclencher l’action appropriée.

    ```csharp
        /// <summary>
        /// Changes the color of the target GameObject by providing the name of the object
        /// and the name of the color
        /// </summary>
        public void ChangeTargetColor(string targetName, string colorName)
        {
            GameObject foundTarget = FindTarget(targetName);
            if (foundTarget != null)
            {
                Debug.Log("Changing color " + colorName + " to target: " + foundTarget.name);

                switch (colorName)
                {
                    case "blue":
                        foundTarget.GetComponent<Renderer>().material.color = Color.blue;
                        break;

                    case "red":
                        foundTarget.GetComponent<Renderer>().material.color = Color.red;
                        break;

                    case "yellow":
                        foundTarget.GetComponent<Renderer>().material.color = Color.yellow;
                        break;

                    case "green":
                        foundTarget.GetComponent<Renderer>().material.color = Color.green;
                        break;

                    case "white":
                        foundTarget.GetComponent<Renderer>().material.color = Color.white;
                        break;

                    case "black":
                        foundTarget.GetComponent<Renderer>().material.color = Color.black;
                        break;
                }          
            }
        }

        /// <summary>
        /// Reduces the size of the target GameObject by providing its name
        /// </summary>
        public void DownSizeTarget(string targetName)
        {
            GameObject foundTarget = FindTarget(targetName);
            foundTarget.transform.localScale -= new Vector3(0.5F, 0.5F, 0.5F);
        }

        /// <summary>
        /// Increases the size of the target GameObject by providing its name
        /// </summary>
        public void UpSizeTarget(string targetName)
        {
            GameObject foundTarget = FindTarget(targetName);
            foundTarget.transform.localScale += new Vector3(0.5F, 0.5F, 0.5F);
        }
    ```
 
7.  Ajouter le *FindTarget()* méthode pour déterminer quels de la *GameObjects* est la cible de l’objectif actuel. Cette méthode par défaut est la cible pour le *GameObject* en cours « gazed » si aucune cible explicite n’est définie dans les entités.

    ```csharp
        /// <summary>
        /// Determines which obejct reference is the target GameObject by providing its name
        /// </summary>
        private GameObject FindTarget(string name)
        {
            GameObject targetAsGO = null;

            switch (name)
            {
                case "sphere":
                    targetAsGO = sphere;
                    break;

                case "cylinder":
                    targetAsGO = cylinder;
                    break;

                case "cube":
                    targetAsGO = cube;
                    break;

                case "this": // as an example of target words that the user may use when looking at an object
                case "it":  // as this is the default, these are not actually needed in this example
                case "that":
                default: // if the target name is none of those above, check if the user is looking at something
                    if (gazedTarget != null) 
                    {
                        targetAsGO = gazedTarget;
                    }
                    break;
            }
            return targetAsGO;
        }
    ```
 
    > [!IMPORTANT]
    > Supprimer le *Start()* et *Update()* méthodes étant donné que cette classe ne les utiliserez pas.

8.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-8--create-the-gaze-class"></a>Chapitre 8 : créer la classe du pointage de regard

La dernière classe dont vous aurez besoin pour terminer cette application est la *les regards* classe. Cette classe met à jour la référence à la *GameObject* actuellement de focus visuels de l’utilisateur.

Pour créer cette classe : 

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir. 
2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**. Nommez le script *les regards*. 
3.  Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.
4.  Insérez le code suivant pour cette classe :

    ```csharp
        using UnityEngine;

        public class Gaze : MonoBehaviour
        {        
            internal GameObject gazedObject;
            public float gazeMaxDistance = 300;

            void Update()
            {
                // Uses a raycast from the Main Camera to determine which object is gazed upon.
                Vector3 fwd = gameObject.transform.TransformDirection(Vector3.forward);
                Ray ray = new Ray(Camera.main.transform.position, fwd);
                RaycastHit hit;
                Debug.DrawRay(Camera.main.transform.position, fwd);

                if (Physics.Raycast(ray, out hit, gazeMaxDistance) && hit.collider != null)
                {
                    if (gazedObject == null)
                    {
                        gazedObject = hit.transform.gameObject;

                        // Set the gazedTarget in the Behaviours class
                        Behaviours.instance.gazedTarget = gazedObject;
                    }
                }
                else
                {
                    ResetGaze();
                }         
            }

            // Turn the gaze off, reset the gazeObject in the Behaviours class.
            public void ResetGaze()
            {
                if (gazedObject != null)
                {
                    Behaviours.instance.gazedTarget = null;
                    gazedObject = null;
                }
            }
        }
    ```
 
5.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-9--completing-the-scene-setup"></a>Chapitre 9 – fin de l’installation de la scène

1.  Pour terminer l’installation de la scène, faites glisser chaque script que vous avez créé à partir du dossier Scripts à la **Main Camera** de l’objet dans le *hiérarchie panneau*.
2.  Sélectionnez le **Main Camera** et examinez le *panneau Inspecteur*, vous devez être en mesure de voir chaque script que vous avez associée, et vous remarquerez qu’il existe des paramètres qui doivent encore être définies sur chaque script.

    ![La définition des cibles de référence de la caméra.](images/AzureLabs-Lab3-41.png)

3.  Pour définir correctement ces paramètres, suivez ces instructions :

    1. *MicrophoneManager*:

        - À partir de la *hiérarchie panneau*, faites glisser le **dictée texte** de l’objet dans le **dictée texte** boîte valeur du paramètre.

    2. *Comportements*, à partir de la *hiérarchie panneau*:

        - Faites glisser le **sphère** de l’objet dans le *sphère* zone cible de référence.
        - Faites glisser le **cylindre** dans le *cylindre* zone cible de référence.
        - Faites glisser le **Cube** dans le *Cube* zone cible de référence.

    3. *Utilisation*:

        - Définir le *les regards de Distance de Max* à **300** (s’il n’est pas déjà). 

4.  Le résultat doit ressembler à l’image ci-dessous :

    ![Afficher les cibles de référence de caméra, maintenant définir.](images/AzureLabs-Lab3-42.png)
 
## <a name="chapter-10--test-in-the-unity-editor"></a>Chapitre 10 – Test dans l’éditeur Unity

Vérifiez que le programme d’installation de la scène est correctement implémentée.

Vérifiez que :

-   Tous les scripts sont attachés à la **Main Camera** objet. 
-   Tous les champs dans le *panneau Inspecteur de caméra principal* sont affectées correctement.

1.  Appuyez sur la **lire** situé dans le *éditeur Unity*. L’application doit s’exécuter dans le casque immersif attaché.

2.  Essayer quelques énoncés, telles que :

    ```
    make the cylinder red

    change the cube to yellow

    I want the sphere blue

    make this to green

    change it to white
    ```

    > [!NOTE]
    > Si vous voyez une erreur dans la console Unity sur le périphérique audio par défaut modification, la scène peut ne pas fonctionne comme prévu. Cela est dû au mode que microphones intégrés pour les casques qui en sont munis porte sur le portail de réalité mixte. Si vous cette erreur se produit, simplement arrêtez la scène et démarrez à nouveau et les choses peuvent fonctionner comme prévu.

## <a name="chapter-11--build-and-sideload-the-uwp-solution"></a>Chapitre 11 – Build et chargement indépendant de la Solution UWP

Une fois que vous vous assurez que l’application fonctionne dans l’éditeur Unity, vous êtes prêt à générer et déployer.

Pour générer :

1.  Enregistrer la scène actuelle en cliquant sur **fichier > Enregistrer**.
2.  Accédez à **fichier > Paramètres de Build**.
3.  Cochez la case appelée **Unity C# projets** (utile pour visualiser et de débogage de votre code une fois que le projet UWP est créé.
4.  Cliquez sur **ajouter un arrière-plan Open**, puis cliquez sur **Build**.

    ![Fenêtre de paramètres de build](images/AzureLabs-Lab3-43.png)

4.  Vous êtes invité à sélectionner le dossier dans lequel vous souhaitez générer la Solution. 

5.  Créer un *génère* dossier et dans ce dossier, créez un autre dossier avec un nom approprié de votre choix. 
6.  Cliquez sur **sélectionner le dossier** pour commencer la génération à cet emplacement.
 
    ![Créer le dossier Builds](images/AzureLabs-Lab3-44.png)
    ![sélectionnez crée le dossier](images/AzureLabs-Lab3-45.png)
 
7.  Une fois Unity a terminé la génération (il peut prendre un certain temps), il doit s’ouvrir un **Explorateur de fichiers** fenêtre à l’emplacement de votre build.

Pour déployer sur l’ordinateur Local :

1.  Dans *Visual Studio*, ouvrez le fichier solution qui a été créé dans le [chapitre précédent](#chapter-10--test-in-the-unity-editor).
2.  Dans le **plateforme de Solution**, sélectionnez **x86**, **ordinateur Local**.
3.  Dans le **Configuration de la Solution** sélectionnez **déboguer**.

    > Pour le Microsoft HoloLens, il peut s’avérer plus facile d’affecter à ce *Machine distante*, de sorte que vous ne sont pas attachés à votre ordinateur. Cependant, vous devez également effectuer les opérations suivantes :
    > - Connaître le **adresse IP** de votre HoloLens, ce qui se trouve dans le *Paramètres > réseau & Internet > Wi-Fi > Options avancées*; IPv4 est l’adresse que vous devez utiliser. 
    > - Vérifiez **Mode développeur** est **sur**; trouvé dans *Paramètres > mise à jour & sécurité > pour les développeurs*.

    ![Déploiement d’une application](images/AzureLabs-Lab3-46.png)
 
4.  Accédez à la **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.
5.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancé !
6.  Une fois lancé, l’application vous invite à autoriser l’accès à la _Microphone_. Utilisez le *contrôleurs de mouvement*, ou *entrée vocale*, ou le *clavier* d’appuyer sur le **Oui** bouton. 

## <a name="chapter-12--improving-your-luis-service"></a>Chapitre 12 – amélioration de votre service LUIS

>[!IMPORTANT] 
> Ce chapitre est extrêmement important et peut devoir être interated à plusieurs reprises, car elle permet d’améliorer la précision de votre service LUIS : Vérifiez le terme de l’opération.

Pour améliorer le niveau de présentation fourni par LUIS, vous devez capturer les énoncés nouvelle et utilisez-les pour recalculer votre application LUIS.

Par exemple, peut avoir effectué l’apprentissage LUIS pour comprendre « Increase » et « Migrer », mais vous ne voudriez pas que votre application afin de comprendre également des mots tels que « Agrandir » ?

Une fois que vous avez utilisé votre application plusieurs fois, tout ce dont vous avez dit seront collectées par LUIS et disponibles dans le portail de LUIS.

1.  Accédez à votre application de portail suivant ce [lien](https://www.luis.ai/home)et se connecter.
2.  Une fois que vous êtes connecté avec vos Credentials MS, cliquez sur votre *nom de l’application*.
3.  Cliquez sur le **passez en revue les énoncés de point de terminaison** situé à gauche de la page.

    ![Passez en revue les énoncés](images/AzureLabs-Lab3-47.png)
 
4.  Vous verrez une liste des énoncés qui lui ont été envoyés LUIS par votre Application de réalité mixte.

    ![Liste des énoncés](images/AzureLabs-Lab3-48.png)
 
Vous remarquerez certaines en surbrillance *entités*. 

En plaçant le curseur sur chaque mot en surbrillance, vous pouvez consulter chaque énoncé et déterminer quels entité a été reconnue correctement, qui sont des entités incorrectes et quelles entités ne sont pas incluses.

Dans l’exemple ci-dessus, il a été constaté que le mot « spear » avait été mis en surbrillance en tant que cible, par conséquent, il est nécessaire pour corriger l’erreur, ce qui est effectué en pointant sur le mot avec la souris et en cliquant sur **supprimer une étiquette**.

![Vérifier les énoncés](images/AzureLabs-Lab3-49.png)
![supprimer Image d’étiquette](images/AzureLabs-Lab3-50.png)
 
5.  Si vous trouvez les énoncés qui sont complètement incorrect, vous pouvez les supprimer à l’aide de la **supprimer** bouton sur le côté droit de l’écran.

    ![Supprimer des énoncés incorrects](images/AzureLabs-Lab3-51.png)

6.  Ou si vous pensez que LUIS a interprété l’énoncé correctement, vous pouvez valider sa présentation à l’aide de la **ajouter l’intention aligné** bouton.

    ![Ajouter à l’intention alignée](images/AzureLabs-Lab3-52.png)

7.  Une fois que vous avez trié de tous les énoncés affichées, essayez et rechargez la page pour voir si plusieurs sont disponibles.
8.  Il est très important de répéter ce processus autant de fois que possible pour améliorer votre compréhension de l’application. 

**Amusez-vous !**

## <a name="your-finished-luis-integrated-application"></a>Votre application LUIS intégrée terminée

Félicitations, vous avez créé une application de réalité mixte qui s’appuie sur Azure Language Understanding Intelligence Service, de comprendre ce qui indique un utilisateur et agir sur ces informations.

![résultat de laboratoire](images/AzureLabs-Lab3-000.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Lors de l’utilisation de cette application, vous pouvez remarquer que si vous remplacez l’objet Floor et posez modifier sa couleur, il procédera ainsi. Vous pouvez imaginer comment arrêter votre application à partir de la modification de la couleur de l’étage

### <a name="exercise-2"></a>Exercice 2

Essayez d’étendre les fonctions LUIS et application, en ajoutant des fonctionnalités supplémentaires pour les objets de scène ; par exemple, créer de nouveaux objets aux regards indique un point d’accès, selon ce que l’utilisateur et puis être en mesure d’utiliser ces objets en même temps que les objets de scène actuels, avec les commandes existantes. 
