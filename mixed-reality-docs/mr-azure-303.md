---
title: MR et Azure 303-compréhension du langage naturel (LUIS)
description: Suivez ce cours pour apprendre à implémenter Azure Language Understanding Intelligence Service (LUIS) dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, Unity, didacticiel, API, Language Understanding Intelligence Service, Luis, hololens, immersif, VR
ms.openlocfilehash: fb00fe9079e49a7ada507e7407ef45fa7eeb0d7e
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63555298"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br>

# <a name="mr-and-azure-303-natural-language-understanding-luis"></a>MR et Azure 303: Compréhension du langage naturel (LUIS)

Dans ce cours, vous allez apprendre à intégrer Language Understanding dans une application de réalité mixte à l’aide d’Azure Cognitive Services, avec le API Language Understanding.

![résultat de l’atelier](images/AzureLabs-Lab3-000.png)

*Language Understanding (Luis)* est un service Microsoft Azure, qui permet aux applications de tirer parti de l’entrée utilisateur, par exemple en extrayant ce qu’une personne peut souhaiter, dans ses propres mots. Cela est possible via Machine Learning, qui comprend et apprend les informations d’entrée, puis peut répondre avec des informations détaillées et pertinentes. Pour plus d’informations, visitez la [page Azure Language Understanding (Luis)](https://azure.microsoft.com/services/cognitive-services/language-understanding-intelligent-service/).

Une fois ce cours terminé, vous disposerez d’une application de casque immersif en réalité mixte, qui sera en mesure d’effectuer les opérations suivantes:

1.  Capturez la parole d’entrée d’utilisateur à l’aide du microphone attaché au casque immersif. 
2.  Envoyez la dictée capturée au *Language Understanding intelligent service Azure* (*Luis*). 
3.  Utilisez LUIS Extract la signification des informations d’envoi, qui sera analysée et tentera de déterminer l’objectif de la demande de l’utilisateur.

Le développement inclut la création d’une application dans laquelle l’utilisateur peut utiliser la voix et/ou le point de regard pour modifier la taille et la couleur des objets dans la scène. L’utilisation de contrôleurs de mouvement n’est pas couverte.

Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception. Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity. C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.

Préparez-vous à former LUIS plusieurs fois, ce qui est abordé dans le [chapitre 12](#chapter-12--improving-your-luis-service). Vous obtiendrez de meilleurs résultats le plus souvent, LUIS a été formé.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>MR et Azure 303: Compréhension du langage naturel (LUIS)</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Bien que ce cours se concentre principalement sur les casques de Windows Mixed Reality (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours à Microsoft HoloLens. À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge HoloLens. Lorsque vous utilisez HoloLens, vous remarquerez peut-être un écho pendant la capture vocale.

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:

- Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](install-the-tools.md)
- [Le dernier Kit de développement logiciel Windows 10](install-the-tools.md)
- [Unity 2017,4](install-the-tools.md)
- [Visual Studio 2017](install-the-tools.md)
- Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé
- Un jeu de casque avec un microphone intégré (si le casque n’a pas de MIC et de haut-parleurs intégrés)
- Accès Internet pour l’installation d’Azure et la récupération LUIS

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération). 
2.  Pour permettre à votre ordinateur d’activer la dictée, accédez à **Paramètres Windows > confidentialité > reconnaissance vocale, écriture manuscrite & typage** , puis appuyez sur le bouton **activer les services vocaux et les suggestions de saisie**.
3.  Le code de ce didacticiel vous permet d’enregistrer à partir de l’ensemble du **périphérique microphone par défaut** sur votre ordinateur. Assurez-vous que le périphérique microphone par défaut est défini comme celui que vous souhaitez utiliser pour capturer votre voix.
4.  Si votre casque dispose d’un microphone intégré, assurez-vous que l’option *«lors de l’usure du casque, basculez vers casque MIC»* est activée dans les paramètres du portail de la *réalité mixte* .

    ![Configuration du casque immersif](images/AzureLabs-Lab3-00.png)

## <a name="chapter-1--setup-azure-portal"></a>Chapitre 1-configurer le portail Azure

Pour utiliser le service de *Language Understanding* dans Azure, vous devez configurer une instance du service qui sera mise à la disposition de votre application.

1.  Connectez-vous au [portail Azure](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas encore de compte Azure, vous devez en créer un. Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche, recherchez *Language Understanding*, puis cliquez sur **entrée**. 

    ![Créer une ressource LUIS](images/AzureLabs-Lab3-01.png)

    > [!NOTE]
    > Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.
 
3.  La nouvelle page qui s’affiche à droite fournit une description du service Language Understanding. En bas à gauche de cette page, cliquez sur le bouton **créer** pour créer une instance de ce service.

    ![Création du service LUIS-Notice légale](images/AzureLabs-Lab3-02.png)
 
4.  Une fois que vous avez cliqué sur créer:

    1. Insérez le **nom** de votre choix pour cette instance de service.
    2. Sélectionnez un **abonnement**.
    3. Sélectionnez le **niveau tarifaire** approprié, s’il s’agit de la première fois que vous créez un *service Luis*, vous devez disposer d’un niveau gratuit (nommé F0). L’allocation gratuite doit être plus que suffisante pour ce cours.
    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun. 

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources). L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait. Certaines ressources Azure sont uniquement disponibles dans certaines régions.
    6. Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.
    7. Sélectionnez **Créer**.

        ![Créer un service LUIS-entrée utilisateur](images/AzureLabs-Lab3-03.png)
 
5.  Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.
6.  Une notification s’affichera dans le portail une fois l’instance de service créée. 
 
    ![Nouvelle image de notification Azure](images/AzureLabs-Lab3-04.png)

7.  Cliquez sur la notification pour explorer votre nouvelle instance de service.

    ![Notification de création de ressource réussie](images/AzureLabs-Lab3-05.png)
 
8.  Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service. Vous êtes dirigé vers votre nouvelle instance de service LUIS. 
 
    ![Accès aux clés LUIS](images/AzureLabs-Lab3-06.png)

9.  Dans ce didacticiel, votre application doit effectuer des appels à votre service, à l’aide de la clé d’abonnement de votre service.
10. À partir de la page *démarrage rapide* , de votre service *API Luis* , accédez à la première étape, *saisissez vos clés*, puis cliquez sur **clés** (vous pouvez également y parvenir en cliquant sur les touches de lien bleu, situées dans le menu de navigation services, indiqué par icône de clé). Cela permet de révéler vos *clés*de service.
11. Prenez une copie de l’une des clés affichées, car vous en aurez besoin plus tard dans votre projet. 
12. Dans la page *service* , cliquez sur *Language Understanding portail* pour être redirigé vers la page Web que vous utiliserez pour créer votre nouveau service, au sein de l’application Luis. 

## <a name="chapter-2--the-language-understanding-portal"></a>Chapitre 2 – portail Language Understanding

Dans cette section, vous allez apprendre à créer une application LUIS sur le portail LUIS. 

> [!IMPORTANT]
> N’oubliez pas que la configuration des *entités*, des *intentions*et des énoncés  dans ce chapitre n’est que la première étape de la création de votre service Luis: vous devrez également reformer le service, plusieurs fois, afin de le rendre plus précis. La reformation de votre service est traitée dans le [dernier chapitre](#chapter-12--improving-your-luis-service) de ce cours. Assurez-vous donc de l’effectuer.

1.  Quand vous atteignez le *portail Language Understanding*, vous devrez peut-être vous connecter, si ce n’est déjà fait, avec les mêmes informations d’identification que votre portail Azure. 

    ![Page de connexion LUIS](images/AzureLabs-Lab3-07.png)
 
2.  Si vous utilisez LUIS pour la première fois, vous devez faire défiler vers le bas de la page d’accueil, pour rechercher et cliquer sur le bouton **créer une application Luis** .

    ![Page créer une application LUIS](images/AzureLabs-Lab3-08.png)
 
3.  Une fois connecté, cliquez sur **mes applications** (si vous n’êtes pas actuellement dans cette section). Vous pouvez ensuite cliquer sur **créer une nouvelle application**.

    ![LUIS-image de mon application](images/AzureLabs-Lab3-09.png)
 
4.  Donnez un *nom*à votre application.
5.  Si votre application est censée comprendre une langue différente de l’anglais, vous devez modifier la *culture* en fonction de la langue appropriée.
6.  Ici, vous pouvez également ajouter une *Description* de votre nouvelle application Luis.

    ![LUIS-créer une application](images/AzureLabs-Lab3-10.png)

7.  Une fois que vous avez **terminé**, vous accédez à la page de *génération* de votre nouvelle application *Luis* .
8.  Voici quelques concepts importants à comprendre:

    -   *Intentionnelle*, représente la méthode qui sera appelée à la suite d’une requête de l’utilisateur. Une *intention* peut avoir une ou plusieurs *entités*.
    -   *Entité*, est un composant de la requête qui décrit les informations relatives à l' *intention*.
    -   Les énoncés, sont des exemples de requêtes fournies par le développeur, que Luis utilise pour se former lui-même.

Si ces concepts ne sont pas parfaitement clairs, ne vous inquiétez pas, car ce cours les clarifie plus en détail dans ce chapitre.

Vous commencerez par créer les *entités* nécessaires à la création de ce cours.

9.  Sur le côté gauche de la page, cliquez sur *entités*, puis sur **créer une entité**.

    ![Créer une entité](images/AzureLabs-Lab3-11.png)

10. Appelez la nouvelle *couleur*d’entité, définissez son type sur *simple*, puis appuyez sur **terminé**.

    ![Créer une entité simple-couleur](images/AzureLabs-Lab3-12.png)
 
11. Répétez ce processus pour créer trois (3) autres entités simples nommées:

    -   *augmenter*
    -   *réduire*
    -   *Indicatif*

Le résultat doit ressembler à l’image ci-dessous:

![Résultat de la création de l’entité](images/AzureLabs-Lab3-13.png)
 
À ce stade, vous pouvez commencer à créer des *intentions*. 

> [!WARNING]
> Ne supprimez pas l’intention **None** .

12. Sur le côté gauche de la page, cliquez sur **intentions**, puis sur **créer un nouvel objectif**.

    ![Créer des intentions](images/AzureLabs-Lab3-14.png)

13. Appelez le nouveau  **ChangeObjectColor**d’intention.

    > [!IMPORTANT]
    > Ce nom d' *intention* est utilisé dans le code plus loin dans ce cours. pour obtenir de meilleurs résultats, utilisez ce nom exactement comme indiqué.

Une fois que vous avez confirmé le nom, vous êtes dirigé vers la page intentions.

![Page LUIS-intentions](images/AzureLabs-Lab3-15.png)

Vous remarquerez qu’une zone de texte vous demande de taper 5 ou plusieurs *énoncés*différents.

> [!NOTE]
> LUIS convertit tous les énoncés en minuscules.

14. Insérez l' *énoncé* suivant dans la zone de texte supérieure (actuellement avec le type de texte *environ 5 exemples...* ) et appuyez sur **entrée**:

```
The color of the cylinder must be red
```

Vous remarquerez que le nouvel *énoncé* s’affiche dans une liste sous.

En suivant le même processus, insérez les six (6) énoncés suivants:

```
make the cube black

make the cylinder color white

change the sphere to red

change it to green

make this yellow

change the color of this object to blue
```

Pour chaque énoncé que vous avez créé, vous devez identifier les mots qui doivent être utilisés par LUIS comme entités. Dans cet exemple, vous devez étiqueter toutes les couleurs en tant qu’entité de *couleur* et toutes les références possibles à une cible en tant qu’entité *cible* .

15. Pour ce faire, essayez de cliquer sur le mot *Cylinder* dans le premier énoncé et sélectionnez *target (cible*).

    ![Identifier les cibles d’énoncé](images/AzureLabs-Lab3-16.png)
 
16. Cliquez maintenant sur le mot *Red* dans le premier énoncé et sélectionnez *couleur*.

    ![Identifier les entités énoncées](images/AzureLabs-Lab3-17.png)
 
17. Étiquetez également la ligne suivante, où *cube* doit être une *cible*et *noir* doit être une *couleur*. Notez également l’utilisation des mots *«This»* , *«IT»* et *«This Object»* , que nous fournissons, afin que les types de cibles non spécifiques soient également disponibles. 

18. Répétez le processus ci-dessus jusqu’à ce que tous les énoncés aient les entités étiquetées. Si vous avez besoin d’aide, consultez l’image ci-dessous.

    > [!TIP]
    > Lorsque vous sélectionnez des mots pour les étiqueter en tant qu’entités:
    > - Pour les mots uniques, cliquez dessus.
    > - Pour un ensemble de deux ou de plusieurs mots, cliquez au début et à la fin de l’ensemble.

    > [!NOTE]
    > Vous pouvez utiliser le bouton bascule de la *vue jetons* pour basculer entre les **entités/jetons**.

19. Les résultats doivent être affichés dans les images ci-dessous, avec la **vue entités/jetons**:

    ![Jetons & vues entités](images/AzureLabs-Lab3-18.png)
  
20. À ce stade, appuyez sur le bouton **train** en haut à droite de la page et attendez que le petit indicateur rond soit vert. Cela indique que LUIS a été correctement formé pour reconnaître cet objectif.

    ![Former LUIS](images/AzureLabs-Lab3-19.png)
 
21. En guise d’exercice pour vous, créez une intention appelée **ChangeObjectSize**, en utilisant les entités *target*, Resize et  *Resize*.
22. En suivant le même processus que l’intention précédente, insérez les huit (8) énoncés suivants pour la modification de la *taille* :

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

23. Le résultat doit être similaire à celui de l’image ci-dessous:

    ![Configurer les jetons/entités ChangeObjectSize](images/AzureLabs-Lab3-20.png) 

24. Une fois que les deux intentions, **ChangeObjectColor** et **ChangeObjectSize**, ont été créées et formés, cliquez sur le bouton **publier** situé en haut de la page.

    ![Publier le service LUIS](images/AzureLabs-Lab3-21.png)

25. Sur la page de *publication* , vous allez finaliser et publier votre application Luis afin que votre code puisse y accéder.

    1. Définissez la *publication de* la liste déroulante sur **production**.
    2. Définissez le fuseau *horaire sur votre* fuseau horaire.
    3. Cochez la case **inclure tous les scores d’intention prédits**.
    4. Cliquez sur **publier dans l’emplacement de production**.

        ![Paramètres de publication](images/AzureLabs-Lab3-22.png)

26. Dans la section *ressources et clés*:

    1.  Sélectionnez la région que vous définissez pour l’instance de service dans le portail Azure.
    2.  Vous remarquerez un élément **Starter_Key** ci-dessous, ignorez-le.
    3.  Cliquez sur **Ajouter une clé** et insérez la *clé* obtenue dans le portail Azure lors de la création de votre instance de service. Si votre Azure et le portail LUIS sont enregistrés dans le même utilisateur, vous trouverez des menus déroulants pour le *nom du client*, le nom de l' *abonnement*et la *clé* que vous souhaitez utiliser (le nom que vous avez fourni précédemment dans le portail Azure est le même que celui que vous avez fourni précédemment).

    > [!IMPORTANT] 
    > Sous *point de terminaison*, prenez une copie du point de terminaison correspondant à la clé que vous avez insérée, vous allez bientôt l’utiliser dans votre code.
 
## <a name="chapter-3--set-up-the-unity-project"></a>Chapitre 3: configurer le projet Unity

Ce qui suit est une configuration classique pour le développement avec la réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **nouveau**. 

    ![Démarrez le nouveau projet Unity.](images/AzureLabs-Lab3-24.png)

2.  Vous devez maintenant fournir un nom de projet Unity, insérer **MR_LUIS**. Assurez-vous que le type de projet est défini sur **3D**. Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés). Ensuite, cliquez sur **créer un projet**.

    ![Fournissez des détails pour le nouveau projet Unity.](images/AzureLabs-Lab3-25.png)
 
3.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**. Accédez à modifier > Préférences puis, dans la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio 2017**. Fermez la fenêtre **Préférences** .

    ![Mettre à jour la préférence éditeur de script.](images/AzureLabs-Lab3-26.png)
 
4.  Accédez ensuite à **fichier > paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .

    ![Fenêtre Paramètres de build, basculez plateforme vers UWP.](images/AzureLabs-Lab3-27.png)
 
5.  Accédez à **fichier > paramètres de build** et assurez-vous que:

    1. L' **appareil cible** est défini sur **n’importe quel appareil**

        > Pour Microsoft HoloLens, définissez **appareil cible** sur *HoloLens*.

    2. Le **type de build** est **D3D**
    3. Le **SDK** est configuré sur le **dernier installé**
    4. **Version de Visual Studio** définie sur le **dernier installé**
    5. La **génération et l’exécution** sont définies sur l' **ordinateur local**
    6. Enregistrez la scène et ajoutez-la à la Build.

        1. Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**. Une fenêtre d’enregistrement s’affiche.
        
            ![Cliquez sur le bouton Ajouter des scènes ouvertes](images/AzureLabs-Lab3-28.png)

        2. Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez- le Scenes.

            ![Créer un dossier de scripts](images/AzureLabs-Lab3-29.png)

        3. Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier*:, tapez **MR_LuisScene**, puis cliquez sur **Enregistrer**.

            ![Donnez un nom à la nouvelle scène.](images/AzureLabs-Lab3-30.png)

    7. Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.

6. Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* . 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab3-31.png) 
 
7. Dans ce volet, quelques paramètres doivent être vérifiés:

    1. Sous l’onglet **autres paramètres** :

        1. La **version du runtime de script** doit être **stable** (équivalent .net 3,5).
        2. Le **backend de script** doit être **.net**
        3. Le **niveau de compatibilité** de l’API doit être **.net 4,6**

            ![Mettez à jour d’autres paramètres.](images/AzureLabs-Lab3-32.png)
      
    2. Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:

        1. **InternetClient**
        2. **Cravate**

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab3-33.png)

    3. Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.

        ![Mettez à jour les paramètres X R.](images/AzureLabs-Lab3-34.png)

8.  De retour dans les *paramètres de build* , les projets _Unity C#_  ne sont plus grisés. Cochez la case en regard de cette option. 
9.  Fermez la fenêtre Paramètres de Build.
10. Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).

## <a name="chapter-4--create-the-scene"></a>Chapitre 4: créer la scène

> [!IMPORTANT]
> Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20303%20-%20Natural%20language%20understanding/Azure-MR-303.unitypackage), à l’importer dans votre projet en tant que [package personnalisé](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au [Chapitre 5](#chapter-5--create-the-microphonemanager-class). 

1.  Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, sous **objet 3D**, ajoutez un **plan**.

    ![Créez un plan.](images/AzureLabs-Lab3-35.png)

2.  Sachez que lorsque vous cliquez à nouveau avec le bouton droit dans la *hiérarchie* pour créer d’autres objets, si le dernier objet est toujours sélectionné, l’objet sélectionné est le parent de votre nouvel objet. Évitez de cliquer avec le bouton droit sur un espace vide dans la hiérarchie, puis cliquez avec le bouton droit.

3.  Répétez la procédure ci-dessus pour ajouter les objets suivants:

    1. *Cercle*
    2. *Éprouvette*
    3. *Dernier*
    4. *Texte 3D*

4.  La *hiérarchie* de scène qui en résulte doit être semblable à celle de l’image ci-dessous:

    ![Configuration de la hiérarchie de scène.](images/AzureLabs-Lab3-36.png)
 
5.  Cliquez sur l' **appareil photo principal** pour le sélectionner, regardez dans le *panneau* de l’inspecteur, vous verrez l’objet Camera avec tous ses composants.
6.  Cliquez sur le bouton **Ajouter un composant** situé en bas du panneau de l' *inspecteur*.

    ![Ajouter une source audio](images/AzureLabs-Lab3-37.png)
 
7.  Recherchez le composant appelé *source audio*, comme indiqué ci-dessus.
8.  Assurez-vous également que le composant *transformer* de l’appareil photo principal est défini sur (0, 0, 0). pour ce faire, appuyez sur l’icône d' **engrenage** en regard du composant *transformer* de l’appareil photo, puis sélectionnez **Réinitialiser**. Le composant *transformer* doit alors ressembler à ceci:

    1.  La *position* est définie sur **0, 0, 0**.
    2.  La *rotation* est définie sur **0, 0,** 0.

    > [!NOTE] 
    > Pour Microsoft HoloLens, vous devez également modifier les éléments suivants, qui font partie du composant **Camera** , qui se trouve sur votre **caméra principale**:
    > - **Indicateurs d’effacement:** Couleur unie.
    > - **Arrière-plan** 'Black, alpha 0 ' – couleur hexadécimale: #00000000.

9.  Cliquez avec le gauche sur le **plan** pour le sélectionner. Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes:

    |       | Transformation- *position* |       |
    |:-----:|:----------------------:|:-----:|
    | **X** | **Y**                  | **Z** |
    | 0     | -1                     | 0     |


10. Cliquez sur la **sphère** à gauche pour la sélectionner. Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes:

    |       | Transformation- *position* |       |
    |:-----:|:----------------------:|:-----:|
    | **X** | **Y**                  | **Z** |
    | 2     | 1                      | 2     |

11. Cliquez avec le gauche sur le **cylindre** pour le sélectionner. Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes:

    |       | Transformation- *position* |       |
    |:-----:|:----------------------:|:-----:|
    | **X** | **Y**                  | **Z** |
    | 2    | 1                      | 2     |

12. Cliquez sur le **cube** pour le sélectionner. Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes:

    |        | Transformation- *position* |       |  \| |       | Transformation- *rotation* |       |
    |:------:|:----------------------:|:-----:|:---:|:-----:|:----------------------:|:-----:|
    | **X** | **Y**                   | **Z** |  \| | **X** | **Y**                  | **Z** |
    | 0     | 1                       | 4     |  \| | 45    | 45                     | 0     | 

13. Cliquez sur le **nouvel objet texte** pour le sélectionner. Dans le *volet* de l’inspecteur, définissez le composant *transformer* avec les valeurs suivantes:

    |       | Transformation- *position* |       |  \| |       | Transformation-mettre à l' *échelle* |       |
    |:-----:|:----------------------:|:-----:|:---:|:-----:|:-------------------:|:-----:|
    | **X** | **Y**                  | **Z** |  \| | **X** | **Y**               | **Z** |
    | 2    | 6\.                      | 9     |  \| | 0.1   | 0.1                 | 0.1   | 

14. Remplacez la **taille de police** du composant de maillage de **texte** par **50**.
15. Modifiez le *nom* de l’objet de **maillage de texte** en **texte**de dictée.

    ![Créer un objet de texte 3D](images/AzureLabs-Lab3-38.png)
 
16. La structure de votre volet de hiérarchie doit maintenant ressembler à ceci:

    ![maillage de texte en mode scène](images/AzureLabs-Lab3-38b.png)


17. La scène finale doit ressembler à l’image ci-dessous:

    ![Vue scène.](images/AzureLabs-Lab3-39.png)
    
 
## <a name="chapter-5--create-the-microphonemanager-class"></a>Chapitre 5: créer la classe MicrophoneManager

Le premier script que vous allez créer est la classe *MicrophoneManager* . À la suite de cela, vous allez créer le *LuisManager*, la classe des *comportements* et enfin la classe du *regard* (n’hésitez pas à créer tous ces éléments maintenant, bien qu’elle soit couverte à mesure que vous atteignez chaque chapitre).

La classe *MicrophoneManager* est chargée des opérations suivantes:

-   Détection du périphérique d’enregistrement connecté au casque ou à l’ordinateur (selon la valeur par défaut).
-   Capturez l’audio (voix) et utilisez la dictée pour le stocker en tant que chaîne.
-   Une fois que la voix a été suspendue, soumettez la dictée à la classe *LuisManager* . 

Pour créer cette classe: 

1.  Cliquez avec le bouton droit dans le *panneau Projet*, puis **créez > dossier**. Appelez le dossier **scripts**. 

    ![Créer un dossier de scripts.](images/AzureLabs-Lab3-40.png)
 
2.  Après avoir créé le dossier **scripts** , double-cliquez dessus pour l’ouvrir. Ensuite, dans ce dossier, cliquez avec le bouton droit sur, puis **créez > C# script**. Nommez le script *MicrophoneManager*. 

3.  Double-cliquez sur *MicrophoneManager* pour l’ouvrir avec *Visual Studio*.
4.  Ajoutez les espaces de noms suivants au début du fichier:

    ```csharp
        using UnityEngine;
        using UnityEngine.Windows.Speech;
    ```

5.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe *MicrophoneManager* :

    ```csharp
        public static MicrophoneManager instance; //help to access instance of this object
        private DictationRecognizer dictationRecognizer;  //Component converting speech to text
        public TextMesh dictationText; //a UI object used to debug dictation result
    ``` 

6.  Vous devez maintenant ajouter le code des méthodes *éveillés ()* et *Start ()* . Ils sont appelés lorsque la classe est initialisée:

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
 
7.  À présent, vous avez besoin de la méthode utilisée par l’application pour démarrer et arrêter la capture vocale, et la passer à la classe *LuisManager* , que vous allez bientôt créer. 

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

8.  Ajoutez un *Gestionnaire* de dictée qui sera appelé lorsque la voix sera interrompue. Cette méthode passera le texte de dictée à la classe *LuisManager* .

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
    > Supprimez la méthode *Update ()* puisque cette classe ne l’utilisera pas.

9.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.

    > [!NOTE]
    > À ce stade, vous remarquerez qu’une erreur s’affiche dans le panneau de la console de l' *éditeur Unity*. Cela est dû au fait que le code fait référence à la classe *LuisManager* que vous allez créer dans le chapitre suivant.

## <a name="chapter-6--create-the-luismanager-class"></a>Chapitre 6: créer la classe LUISManager

Il est temps de créer la classe *LuisManager* , qui fera l’appel au service Azure Luis. 

L’objectif de cette classe est de recevoir le texte de dictée de la classe *MicrophoneManager* et de l’envoyer au *API Language Understanding Azure* à analyser.

Cette classe va désérialiser la réponse *JSON* et appeler les méthodes appropriées de la classe des *comportements* pour déclencher une action.

Pour créer cette classe: 

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir. 
2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**. Nommez le script *LuisManager*. 
3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.
4.  Ajoutez les espaces de noms suivants au début du fichier:

    ```csharp
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.IO;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  Vous commencerez par créer trois classes **à l’intérieur** de la classe *LuisManager* (dans le même fichier de script, au-dessus de la méthode *Start ()* ) qui représenteront la réponse JSON désérialisée d’Azure.

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

6.  Ensuite, ajoutez les variables suivantes à l’intérieur de la classe *LuisManager* :
 
    ```csharp
        public static LuisManager instance;

        //Substitute the value of luis Endpoint with your own End Point
        string luisEndpoint = "https://westus.api.cognitive... add your endpoint from the Luis Portal";
    ```

7.  Veillez à placer votre point de terminaison LUIS à l’heure actuelle (que vous aurez sur votre portail LUIS).

8.  Le code de la méthode *éveillé ()* doit maintenant être ajouté. Cette méthode est appelée lorsque la classe est initialisée:

    ```csharp
        private void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }
    ```

9.  À présent, vous avez besoin des méthodes utilisées par cette application pour envoyer la dictée reçue de la classe *MicrophoneManager* à *Luis*, puis recevoir et désérialiser la réponse. 
10. Une fois que la valeur de l’intention, et les entités associées, ont été déterminées, elles sont passées à l’instance de la classe des *comportements* pour déclencher l’action prévue.

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
 
11. Créez une nouvelle méthode appelée *AnalyseResponseElements ()* qui lira les *AnalysedQuery* résultants et déterminez les entités. Une fois ces entités déterminées, elles sont transmises à l’instance de la classe des *comportements* à utiliser dans les actions.

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
    > Supprimez les méthodes *Start ()* et *Update ()* puisque cette classe ne les utilise pas.

12. Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.

> [!NOTE]
> À ce stade, vous remarquerez que plusieurs erreurs apparaissent dans le panneau de la console de l' *éditeur Unity*. Cela est dû au fait que le code fait référence à la classe des *comportements* que vous allez créer dans le chapitre suivant.

## <a name="chapter-7--create-the-behaviours-class"></a>Chapitre 7: créer la classe des comportements

La classe des *comportements* déclenchera les actions à l’aide des entités fournies par la classe *LuisManager* .

Pour créer cette classe: 

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir. 
2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**. Nommez les *comportements*de script. 
3.  Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.
4.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe des *comportements* :

    ```csharp
        public static Behaviours instance;

        // the following variables are references to possible targets
        public GameObject sphere;
        public GameObject cylinder;
        public GameObject cube;
        internal GameObject gazedTarget;
    ```
 
5.  Ajoutez le code de la méthode *éveillé ()* . Cette méthode est appelée lorsque la classe est initialisée:

    ```csharp
        void Awake()
        {
            // allows this class instance to behave like a singleton
            instance = this;
        }
    ```
 
6.  Les méthodes suivantes sont appelées par la classe *LuisManager* (que vous avez créée précédemment) pour déterminer l’objet qui est la cible de la requête, puis déclencher l’action appropriée.

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
 
7.  Ajoutez la méthode *FindTarget ()* pour déterminer laquelle du *GameObjects* est la cible de l’intention actuelle. Cette méthode définit par défaut la cible sur le *gameobject* «en regard» si aucune cible explicite n’est définie dans les entités.

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
    > Supprimez les méthodes *Start ()* et *Update ()* puisque cette classe ne les utilise pas.

8.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.

## <a name="chapter-8--create-the-gaze-class"></a>Chapitre 8: créer la classe en regard

La dernière classe dont vous aurez besoin pour compléter cette application est la classe de *regard* . Cette classe met à jour la référence au *gameobject* actuellement dans le focus visuel de l’utilisateur.

Pour créer cette classe: 

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir. 
2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**. Nommez le script point de *regard*. 
3.  Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.
4.  Insérez le code suivant pour cette classe:

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
 
5.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.

## <a name="chapter-9--completing-the-scene-setup"></a>Chapitre 9: fin de la configuration de la scène

1.  Pour terminer la configuration de la scène, faites glisser chaque script que vous avez créé à partir du dossier scripts vers l’objet **caméra principale** dans le *panneau hiérarchie*.
2.  Sélectionnez l' **appareil photo principal** et examinez le panneau de l' *inspecteur*, vous devez être en mesure de voir chaque script joint, et vous remarquerez qu’il existe des paramètres sur chaque script qui doivent être définis.

    ![Définition des cibles de référence de l’appareil photo.](images/AzureLabs-Lab3-41.png)

3.  Pour définir correctement ces paramètres, suivez ces instructions:

    1. *MicrophoneManager*:

        - À partir du *panneau hiérarchie*, faites glisser l’objet **texte** de dictée dans la zone valeur du paramètre de **texte** de dictée.

    2. *Comportements*, à partir du *volet hiérarchie*:

        - Faites glisser l’objet **Sphere** dans la zone de la cible de référence *Sphere* .
        - Faites glisser le **cylindre** dans la zone de la cible de référence *cylindrique* .
        - Faites glisser le **cube** dans la zone de la cible de la référence du *cube* .

    3. Point de *regard*:

        - Définissez la *distance maximale* du point de regard sur **300** (si ce n’est pas déjà le cas). 

4.  Le résultat doit ressembler à l’image ci-dessous:

    ![L’indication des cibles de référence de l’appareil photo, désormais définie.](images/AzureLabs-Lab3-42.png)
 
## <a name="chapter-10--test-in-the-unity-editor"></a>Chapitre 10 – test dans l’éditeur Unity

Vérifiez que la configuration de la scène est correctement implémentée.

Assurez-vous que :

-   Tous les scripts sont attachés à l’objet **Camera principal** . 
-   Tous les champs du volet principal de l’inspecteur de l' *appareil photo* sont correctement affectés.

1.  Appuyez sur le bouton **lecture** dans l' *éditeur Unity*. L’application doit s’exécuter au sein du casque immersif attaché.

2.  Essayez quelques énoncés, tels que:

    ```
    make the cylinder red

    change the cube to yellow

    I want the sphere blue

    make this to green

    change it to white
    ```

    > [!NOTE]
    > Si une erreur s’affiche dans la console Unity à propos du changement de périphérique audio par défaut, la scène peut ne pas fonctionner comme prévu. Cela est dû à la façon dont le portail de réalité mixte traite les microphones intégrés pour les casques. Si vous voyez cette erreur, arrêtez simplement la scène et redémarrez-la et les choses devraient fonctionner comme prévu.

## <a name="chapter-11--build-and-sideload-the-uwp-solution"></a>Chapitre 11: créer et chargement la solution UWP

Une fois que vous avez vérifié que l’application fonctionne dans l’éditeur Unity, vous êtes prêt à créer et à déployer.

Pour générer:

1.  Enregistrez la scène en cours en cliquant sur **fichier > enregistrer**.
2.  Accédez à **fichier > paramètres de build**.
3.  Cochez la case **projets C# Unity** (utile pour afficher et déboguer votre code une fois le projet UWP créé.
4.  Cliquez sur **Ajouter des scènes ouvertes**, puis cliquez sur **générer**.

    ![Fenêtre Paramètres de build](images/AzureLabs-Lab3-43.png)

4.  Vous serez invité à sélectionner le dossier dans lequel vous souhaitez générer la solution. 

5.  Créez un  dossier Builds et, dans ce dossier, créez un autre dossier avec le nom approprié de votre choix. 
6.  Cliquez sur **Sélectionner un dossier** pour commencer la build à cet emplacement.
 
    ![Créer un dossier](images/AzureLabs-Lab3-44.png)
    ![builds sélectionner le dossier Builds](images/AzureLabs-Lab3-45.png)
 
7.  Une fois la génération de Unity terminée (cela peut prendre un certain temps), elle doit ouvrir une fenêtre de l' **Explorateur de fichiers** à l’emplacement de votre Build.

Pour déployer sur l’ordinateur local:

1.  Dans *Visual Studio*, ouvrez le fichier solution créé dans le [chapitre précédent](#chapter-10--test-in-the-unity-editor).
2.  Dans la **plateforme**de la solution, sélectionnez **x86**, **ordinateur local**.
3.  Dans la **configuration** de la solution, sélectionnez Déboguer.

    > Pour Microsoft HoloLens, il peut s’avérer plus facile de définir cette valeur sur *machine*distante, afin de ne pas être attaché à votre ordinateur. Toutefois, vous devez également effectuer les opérations suivantes:
    > - Identifiez l' **adresse IP** de votre HoloLens, qui se trouve dans les *paramètres > réseau & Internet > les options avancées du Wi-Fi >* ; IPv4 est l’adresse que vous devez utiliser. 
    > - Assurez-vous que le **mode développeur** est **activé**; trouvé dans *paramètres > mettre à jour & > de sécurité pour les développeurs*.

    ![Déployer l’application](images/AzureLabs-Lab3-46.png)
 
4.  Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre ordinateur.
5.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.
6.  Une fois lancé, l’application vous invite à autoriser l’accès au _microphone_. Utilisez les *contrôleurs de mouvement*ou l' *entrée vocale*, ou le *clavier* pour appuyer sur le bouton **Oui** . 

## <a name="chapter-12--improving-your-luis-service"></a>Chapitre 12: amélioration de votre service LUIS

>[!IMPORTANT] 
> Ce chapitre est extrêmement important et devra peut-être être interated à plusieurs moments, car cela permet d’améliorer la précision de votre service LUIS: Veillez à effectuer cette opération.

Pour améliorer le niveau de compréhension fourni par LUIS, vous devez capturer de nouveaux énoncés et les utiliser pour former à nouveau votre application LUIS.

Par exemple, vous avez peut-être formé LUIS pour comprendre l’augmentation et la taille, mais ne souhaitez-vous pas que votre application comprenne également des mots tels que «agrandir»?

Une fois que vous avez utilisé votre application plusieurs fois, tout ce que vous avez dit est collecté par LUIS et disponible dans le portail LUIS.

1.  Accédez à votre application de portail en suivant ce [lien](https://www.luis.ai/home)et connectez-vous.
2.  Une fois que vous êtes connecté avec vos informations d’identification MS, cliquez sur le nom de votre *application*.
3.  Cliquez sur le bouton vérifier les énoncés de **point de terminaison** à gauche de la page.

    ![Passer en revue les énoncés](images/AzureLabs-Lab3-47.png)
 
4.  Une liste des énoncés qui ont été envoyés à LUIS par votre application de réalité mixte s’affiche.

    ![Liste des énoncés](images/AzureLabs-Lab3-48.png)
 
Vous remarquerez certaines *entités*en surbrillance. 

En pointant sur chaque mot en surbrillance, vous pouvez examiner chaque énoncé et déterminer l’entité qui a été reconnue correctement, les entités qui sont incorrectes et les entités qui sont manquées.

Dans l’exemple ci-dessus, il a été constaté que le mot «Spear» avait été mis en surbrillance comme cible. il est donc nécessaire de corriger l’erreur, ce qui se fait en pointant sur le mot avec la souris et en cliquant sur **Supprimer l’étiquette**.

![Vérifier l’image](images/AzureLabs-Lab3-49.png)
de l’étiquette![supprimer les énoncés](images/AzureLabs-Lab3-50.png)
 
5.  Si vous trouvez des énoncés qui ne sont pas corrects, vous pouvez les supprimer à l’aide du bouton **supprimer** sur le côté droit de l’écran.

    ![Supprimer les énoncés erronés](images/AzureLabs-Lab3-51.png)

6.  Ou si vous pensez que LUIS a interprété correctement l’énoncé, vous pouvez valider sa compréhension en utilisant le bouton **Ajouter à l’intention alignée** .

    ![Ajouter à l’intention alignée](images/AzureLabs-Lab3-52.png)

7.  Une fois que vous avez trié tous les énoncés affichés, essayez de recharger la page pour voir si d’autres sont disponibles.
8.  Il est très important de répéter ce processus autant de fois que possible pour améliorer la compréhension de votre application. 

**Amusez-vous!**

## <a name="your-finished-luis-integrated-application"></a>Votre application intégrée LUIS est terminée

Félicitations, vous avez créé une application de réalité mixte qui s’appuie sur le service Azure Language Understanding intelligence pour comprendre ce que l’utilisateur dit, et agir sur ces informations.

![résultat de l’atelier](images/AzureLabs-Lab3-000.png)

## <a name="bonus-exercises"></a>Exercices bonus

### <a name="exercise-1"></a>Exercice 1

Si vous utilisez cette application, vous remarquerez peut-être que si vous pointez sur l’objet Floor et que vous demandez à changer sa couleur, il le fera. Pouvez-vous apprendre comment empêcher votre application de changer la couleur d’étage?

### <a name="exercise-2"></a>Exercice 2

Essayez d’étendre les fonctionnalités de LUIS et de l’application, en ajoutant des fonctionnalités supplémentaires pour les objets dans la scène. par exemple, créez des objets au point d’accès en regard, en fonction de ce que l’utilisateur prétend, puis pouvez utiliser ces objets avec les objets de scène actuels, avec les commandes existantes. 
