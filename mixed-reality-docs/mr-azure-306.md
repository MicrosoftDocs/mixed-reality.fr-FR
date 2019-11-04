---
title: RM et Azure 306-streaming video
description: Suivez ce cours pour apprendre à implémenter Azure Media Services dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, Media Services, streaming video, 360, immersif, VR
ms.openlocfilehash: 6585aa731ff7ebb89beae67ab0b61ac5ef026e47
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438567"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br> 

# <a name="mr-and-azure-306-streaming-video"></a>MR et Azure 306 : diffusion vidéo en continu

![produit final-début du](images/AzureLabs-Lab6-00.png)
![produit final-début](images/AzureLabs-Lab6-01.png)

Dans ce cours, vous allez apprendre comment connecter vos Azure Media Services à une expérience Windows Mixed Reality VR pour permettre une lecture vidéo en continu de 360 degrés sur des casques immersifs. 

**Azure Media Services** sont un ensemble de services qui vous offre des services de streaming vidéo de qualité broadcast pour atteindre un public plus large sur les appareils mobiles actuels les plus populaires. Pour plus d’informations, consultez la [page Azure Media Services](https://azure.microsoft.com/services/media-services).

Une fois ce cours terminé, vous disposerez d’une application de casque d’immersion en réalité mixte, capable d’effectuer les opérations suivantes :

1. Récupérez une vidéo de 360 degrés à partir d’un **stockage Azure**, via **Azure Media Service**.

2. Affichez la vidéo Récupérée de 360 degrés dans une scène Unity.

3. Naviguer entre deux scènes, avec deux vidéos différentes.

Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception. Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity. C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Périphériques pris en charge

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 306 : diffusion vidéo en continu</td><td style="text-align: center;"> </td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="prerequisites"></a>Conditions préalables

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l' [article installer les outils](install-the-tools.md), bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours :

- Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](install-the-tools.md#installation-checklist)
- [Le dernier Kit de développement logiciel Windows 10](install-the-tools.md#installation-checklist)
- [Unity 2017,4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md)
- Accès Internet pour l’installation d’Azure et la récupération de données
- Vidéos de 2 360 degrés au format MP4 (vous trouverez des vidéos gratuites sur les redevances dans [cette page de téléchargement](https://www.mettle.com/360vr-master-series-free-360-downloads-page))

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).
2.  Configurez et testez votre casque immersif en réalité mixte.

    > [!NOTE]
    > Vous n’aurez **pas** besoin de contrôleurs de mouvement pour ce cours. Si vous avez besoin de la prise en charge de la configuration du casque immersif, cliquez sur [le lien pour configurer Windows Mixed Reality](https://support.microsoft.com/help/4043101/windows-10-set-up-windows-mixed-reality).

## <a name="chapter-1---the-azure-portal-creating-the-azure-storage-account"></a>Chapitre 1-portail Azure : création du compte de stockage Azure

Pour utiliser le **service de stockage Azure**, vous devez créer et configurer un **compte de stockage** dans le portail Azure.

1.  Connectez-vous au [portail Azure](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas encore de compte Azure, vous devez en créer un. Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **comptes de stockage** dans le menu de gauche.

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab6-02.png)

3.  Dans l’onglet **comptes de stockage** , cliquez sur **Ajouter**.

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab6-03.png)

4.  Dans l’onglet **créer un compte de stockage** :

    1.  Insérez un **nom** pour votre compte. n’oubliez pas que ce champ accepte uniquement des chiffres et des lettres minuscules.

    2.  Pour **modèle de déploiement,** sélectionnez **Resource Manager**.

    3.  Pour **type de compte**, sélectionnez **stockage (à usage général v1)** .

    4.  Pour **performances**, sélectionnez **standard *.**

    5.  Pour **la réplication** , sélectionnez **stockage localement redondant (LRS)** .

    6.  Laissez le **transfert sécurisé requis** comme **désactivé**.

    7.  Sélectionnez un **abonnement**.

    8.  Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.

    9.  Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources). L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait. Certaines ressources Azure sont uniquement disponibles dans certaines régions.

5.  Vous devrez confirmer que vous avez compris les conditions générales appliquées à ce service.

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab6-04.png)

6.  Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.

7.  Une notification s’affichera dans le portail une fois l’instance de service créée.

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab6-05.png)

8.  À ce stade, vous n’avez pas besoin de suivre la ressource. passez simplement au chapitre suivant.

## <a name="chapter-2---the-azure-portal-creating-the-media-service"></a>Chapitre 2-portail Azure : création du service multimédia

Pour utiliser Azure Media Service, vous devez configurer une instance du service à mettre à la disposition de votre application (où le détenteur du compte doit être un administrateur).

1.  Dans le portail Azure, cliquez sur **créer une ressource** dans le coin supérieur gauche et recherchez **Media Service,** puis appuyez sur **entrée**. La ressource à laquelle vous souhaitez appliquer actuellement une icône rose ; Cliquez sur cette valeur pour afficher une nouvelle page.

    ![Le portail Azure](images/AzureLabs-Lab6-06.png)

2.  La nouvelle page fournit une description du **service multimédia**. En bas à gauche de cette invite, cliquez sur le bouton **créer** pour créer une association avec ce service.

    ![Le portail Azure](images/AzureLabs-Lab6-07.png)

3.  Une fois que vous avez cliqué sur **créer** , un panneau s’affiche pour vous permettre de fournir des détails sur votre nouveau service multimédia :

    1.  Insérez le nom de votre **compte** souhaité pour cette instance de service.

    2.  Sélectionnez un **abonnement**.

    3. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun). 
    
    > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer les groupes de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    4.  Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources). L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait. Certaines ressources Azure sont uniquement disponibles dans certaines régions.

    5.  Pour la section **compte de stockage** , cliquez sur la section **Veuillez sélectionner..** ., puis cliquez sur le compte de **stockage** que vous avez créé dans le dernier chapitre.

    6.  Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.

    7.  Cliquez sur **Create (Créer)** .

        ![Le portail Azure](images/AzureLabs-Lab6-08.png)

4.  Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.

5.  Une notification s’affichera dans le portail une fois l’instance de service créée.

    ![Le portail Azure](images/AzureLabs-Lab6-09.png)

6.  Cliquez sur la notification pour explorer votre nouvelle instance de service.

    ![Le portail Azure](images/AzureLabs-Lab6-10.png)

7.  Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.

8.  Dans la page nouveau service multimédia, dans le volet de gauche, cliquez sur le lien **ressources** , qui est à mi-chemin.

9.  Sur la page suivante, dans le coin supérieur gauche de la page, cliquez sur **Télécharger**.

    ![Le portail Azure](images/AzureLabs-Lab6-11.png)

10. Cliquez sur l’icône de **dossier** pour parcourir vos fichiers et sélectionnez la première vidéo 360 que vous souhaitez diffuser en continu. 
    
    > Vous pouvez suivre ce [lien pour télécharger un exemple de vidéo](https://vimeo.com/214401712).

    ![Le portail Azure](images/AzureLabs-Lab6-12.png)

> [!WARNING]
> Les noms de fichiers longs peuvent entraîner un problème avec l’encodeur : ainsi, pour vous assurer que les vidéos n’ont pas de problèmes, envisagez de raccourcir la longueur des noms de vos fichiers vidéo.

11. La barre de progression devient verte lorsque le chargement de la vidéo est terminé.

    ![Le portail Azure](images/AzureLabs-Lab6-13.png)

12. Cliquez sur le texte ci-dessus (**yourservicename-Assets**) pour revenir à la page **composants** .

13. Vous remarquerez que votre vidéo a été chargée avec succès. Cliquez dessus.

    ![Le portail Azure](images/AzureLabs-Lab6-14.png)

14. La page que vous avez redirigée affiche des informations détaillées sur votre vidéo. Pour pouvoir utiliser votre vidéo, vous devez l’encoder en cliquant sur le bouton **Encoder** en haut à gauche de la page.

    ![Le portail Azure](images/AzureLabs-Lab6-15.png)

15. Un nouveau panneau s’affiche à droite, dans lequel vous pouvez définir des options d’encodage pour votre fichier. Définissez les propriétés suivantes (certaines seront déjà définies par défaut) :

    1.  **Nom de l’encodeur multimédia *Media Encoder standard***

    2.  **Encodage de *contenu prédéfini données à débit binaire multiple MP4***

    3.  **Nom *du travail Media Encoder standard traitement de VIDEO1. MP4***

    4.  **Output Media Media name *VIDEO1. MP4--Media Encoder standard encodé***

        ![Le portail Azure](images/AzureLabs-Lab6-16.png)

16. Cliquez sur le bouton **Créer**.

17. Vous remarquerez une barre avec un **travail d’encodage ajouté**, cliquez sur cette barre et un panneau s’affichera avec la progression de l’encodage affichée.

    ![Le portail Azure](images/AzureLabs-Lab6-17.png)

    ![Le portail Azure](images/AzureLabs-Lab6-18.png)

18. Attendez que le travail soit terminé. Une fois l’opération terminée, n’hésitez pas à fermer le panneau avec le « X » en haut à droite de ce panneau.

    ![Le portail Azure](images/AzureLabs-Lab6-19.png)

    ![Le portail Azure](images/AzureLabs-Lab6-20.png)

    > [!IMPORTANT]
    > Le temps nécessaire dépend de la taille de fichier de votre vidéo. Ce processus peut prendre un certain temps.

19. Maintenant que la version encodée de la vidéo a été créée, vous pouvez la publier pour la rendre accessible. Pour ce faire, cliquez sur les **éléments** de lien Blue pour revenir à la page composants.

    ![Le portail Azure](images/AzureLabs-Lab6-21.png)

20. Vous verrez votre vidéo avec une autre, qui est de **type de ressource _MP4 à débit binaire multiple_** .

    ![Le portail Azure](images/AzureLabs-Lab6-22.png)

    > [!NOTE] 
    > Vous remarquerez peut-être que la nouvelle ressource, avec votre vidéo initiale, est *inconnue*et a une valeur de « 0 » octets pour sa **taille**, actualisez simplement votre fenêtre pour qu’elle soit mise à jour.

21. Cliquez sur ce nouvel élément multimédia.

    ![Le portail Azure](images/AzureLabs-Lab6-23.png)

22. Vous verrez un panneau similaire à celui que vous avez utilisé précédemment, mais il s’agit d’une autre ressource. Cliquez sur le bouton **publier** situé en haut au centre de la page.

    ![Le portail Azure](images/AzureLabs-Lab6-24.png)

23. Vous serez invité à définir un **localisateur**, qui est le point d’entrée, dans les fichiers de vos ressources. Pour votre scénario, définissez les propriétés suivantes :

    1.  **Type de localisateur** > **progressif**.

    2.  La **Date** et l' **heure** seront définies pour vous, à partir de la date actuelle, à une heure future (100 ans dans le cas présent). Laissez tel quel ou modifiez-le pour l’adapter à vos besoins.

    > [!NOTE]
    > Pour plus d’informations sur les localisateurs et sur ce que vous pouvez choisir, consultez la [Documentation Azure Media Services](https://docs.microsoft.com/azure/media-services/media-services-concepts).

24. En bas de ce panneau, cliquez sur le bouton **Ajouter** .

    ![Le portail Azure](images/AzureLabs-Lab6-25.png)

25. Votre vidéo est maintenant publiée et peut être diffusée en continu à l’aide de son point de terminaison. Plus loin dans la page, il s’agit d’une section de **fichiers** . C’est là que se trouvent les différentes versions encodées de votre vidéo. Sélectionnez la résolution la plus élevée possible (dans l’image ci-dessous est le fichier 1920x960), puis un panneau à droite s’affiche. Vous y trouverez une **URL de téléchargement**. Copiez ce **point de terminaison** , car vous allez l’utiliser ultérieurement dans votre code.

    ![Le portail Azure](images/AzureLabs-Lab6-26.png)    

    ![Le portail Azure](images/AzureLabs-Lab6-27.png)

    > [!NOTE] 
    > Vous pouvez également appuyer sur le bouton de **lecture** pour lire votre vidéo et la tester.

26. Vous devez maintenant télécharger la deuxième vidéo que vous allez utiliser dans ce laboratoire. Suivez les étapes ci-dessus, en répétant la même procédure pour la deuxième vidéo. Veillez à copier également le deuxième **point de terminaison** . Utilisez le [lien suivant pour télécharger une deuxième vidéo](https://vimeo.com/214402865).

27. Une fois les deux vidéos publiées, vous êtes prêt à passer au chapitre suivant.

## <a name="chapter-3---setting-up-the-unity-project"></a>Chapitre 3-Configuration du projet Unity

Ce qui suit est une configuration classique pour le développement avec la réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez **Unity** et cliquez sur **nouveau**. 

    ![Le portail Azure](images/AzureLabs-Lab6-28.png)

2.  Vous devez maintenant fournir un nom de projet Unity, insérer **MR\_360VideoStreaming.** Assurez-vous que le type de projet est défini sur **3D**. Définissez l’emplacement approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés). Ensuite, cliquez sur **créer un projet**.

    ![Le portail Azure](images/AzureLabs-Lab6-29.png)

3.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio.** Accédez à ***modifier* les *Préférences*** , puis à partir de la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio 2017**. Fermez la fenêtre **Préférences** .

    ![Le portail Azure](images/AzureLabs-Lab6-30.png)

4.  Ensuite, accédez à ***fichier* *paramètres de build*** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .

5.  Assurez-vous également que :

    1. L' **appareil cible** est défini sur **n’importe quel appareil.**
    
    2.  Le **type de build** est **D3D.**

    3.  Le **SDK** est configuré sur le **dernier installé.**

    4.  La **version de Visual Studio** est **installée sur le plus récent.**

    5.  La **génération et l’exécution** sont définies sur l' **ordinateur local.**

    6.  Ne vous inquiétez pas de définir des **scènes** pour le moment, car vous allez les configurer ultérieurement.

    7.  Les paramètres restants doivent être laissés par défaut pour le moment.

        ![Configuration du projet Unity](images/AzureLabs-Lab6-31.png)

6.  Dans la fenêtre **paramètres de build** , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** . 

7. Dans ce volet, quelques paramètres doivent être vérifiés :

    1.  Sous l’onglet **autres paramètres** :

        1.  La **version du runtime** de **script** doit être **stable** (équivalent .net 3,5).

        2. Le **serveur principal de script** doit être **.net.**

        3. Le **niveau de compatibilité** de l’API doit être **.net 4,6.**

            ![Configuration du projet Unity](images/AzureLabs-Lab6-32.png)

    2.  Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.

        ![Configuration du projet Unity](images/AzureLabs-Lab6-33.png)

    3.  Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher :

        - **InternetClient**

            ![Configuration du projet Unity](images/AzureLabs-Lab6-34.png)

8.  Une fois ces modifications effectuées, fermez la fenêtre **paramètres de build** .

9.  Enregistrez votre projet **fichier* * enregistrer le projet * *.



## <a name="chapter-4---importing-the-insideoutsphere-unity-package"></a>Chapitre 4-importation du package InsideOutSphere Unity

> [!IMPORTANT]
> Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/Azure-MR-306.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au **Chapitre 5**. Vous devrez toujours créer un projet Unity.

Pour ce cours, vous devez télécharger un package d’actifs Unity appelé [**InsideOutSphere. pour Unity**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/InsideOutSphere.unitypackage).

Comment importer les **pour Unity**:

1.  Avec le tableau de bord Unity devant vous, cliquez sur **ressources** dans le menu en haut de l’écran, puis sur **importer le package > package personnalisé**.

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-35.png)

2.  Utilisez le sélecteur de fichiers pour sélectionner le package **InsideOutSphere. pour Unity** , puis cliquez sur **ouvrir**. La liste des composants de cet élément multimédia vous est présentée. Confirmez l’importation en cliquant sur **Importer**.

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-36.png)

3.  Une fois l’importation terminée, vous remarquerez que trois nouveaux dossiers, **matériaux**, **modèles**et **Prefabs**ont été ajoutés à votre dossier de **ressources** . Ce type de structure de dossiers est courant pour un projet Unity.

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-37.png)

    1.  Ouvrez le dossier **Models** , et vous verrez que le modèle **InsideOutSphere** a été importé.

    2.  Dans le **dossier Materials** , vous trouverez la *Lambert1*de matériau **InsideOutSpheres** , ainsi qu’un document appelé *ButtonMaterial*, qui est utilisé par le GazeButton, que vous verrez bientôt.

    3.  Le dossier **Prefabs** contient le Prefab **InsideOutSphere** qui contient à la fois le *modèle* **InsideOutSphere** et le *GazeButton*.

    4.  **Aucun code n’est inclus**, vous allez écrire le code en suivant ce cours.


4.  Dans la **hiérarchie**, sélectionnez l’objet **Camera principal** et mettez à jour les composants suivants :

    1.  **Modifiez**

        1.  Position = **X**: 0, **Y**: 0, **Z**: 0.

        2. Rotation = **X**: 0, **Y**: 0, **Z**: 0.

        3. Échelle **X**: 1, **Y**: 1, **Z**: 1.

    2.  **Appareil photo**

        1. **Indicateurs d’effacement**: couleur unie.

        2.  **Plans de découpage**: près de 0,1, Far : 6.

            ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-38.png)

5.  Accédez au dossier **Prefab** , puis faites glisser le Prefab **InsideOutSphere** dans le panneau de **hiérarchie** .

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-39.png)

6.  Développez l’objet **InsideOutSphere** dans la **hiérarchie** en cliquant sur la petite flèche en regard de celui-ci. Vous verrez un objet **enfant** sous celui-ci appelé **GazeButton**. Ce sera utilisé pour modifier les scènes et, par conséquent, les vidéos.

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-40.png)

7.  Dans la fenêtre de l’inspecteur, cliquez sur le composant transformer du **InsideOutSphere**, vérifiez que les propriétés suivantes sont définies :

    |            |    TRANSFORMATION-POSITION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |          **Y** 0          |  **Z** 0  |

    |            |    TRANSFORMATION-ROTATION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |          **Y** -50        |  **Z** 0  |

    |            |     TRANSFORMATION-METTRE À L’ÉCHELLE     |           |
    | :---------:| :-----------------------: | :--------:|
    |  **X** 1   |          **Y** 1          |  **Z** 1  |

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-41.png)

8.  Cliquez sur l’objet enfant **GazeButton** et définissez sa **transformation** comme suit :

    |            |    TRANSFORMATION-POSITION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 3,6|          **Y** 1,3        |  **Z** 0  |

    |            |    TRANSFORMATION-ROTATION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |          **Y** 0          |  **Z** 0  |

    |            |     TRANSFORMATION-METTRE À L’ÉCHELLE     |           |
    | :---------:| :-----------------------: | :--------:|
    |  **X** 1   |          **Y** 1          |  **Z** 1  |

    ![Importation du package InsideOutSphere Unity](images/AzureLabs-Lab6-42.png)


## <a name="chapter-5---create-the-videocontroller-class"></a>Chapitre 5-créer la classe VideoController

La classe **VideoController** héberge les deux points de terminaison vidéo qui seront utilisés pour diffuser le contenu à partir du service multimédia Azure.

Pour créer cette classe :

1.  Cliquez avec le bouton droit sur le **dossier Asset**, situé dans le panneau **projet** , puis cliquez sur **créer un dossier >** . Nommez le dossier **scripts**.

    ![Créer la classe VideoController](images/AzureLabs-Lab6-43.png)

    ![Créer la classe VideoController](images/AzureLabs-Lab6-44.png)

2.  Double-cliquez sur le dossier **scripts** pour l’ouvrir.

3.  Cliquez avec le bouton droit dans le dossier, puis cliquez sur **create > C\# script**. Nommez le script **VideoController**.

    ![Créer la classe VideoController](images/AzureLabs-Lab6-45.png)

4.  Double-cliquez sur le nouveau script **VideoController** pour l’ouvrir avec **Visual Studio 2017.**

    ![Créer la classe VideoController](images/AzureLabs-Lab6-46.png)

5.  Mettez à jour les espaces de noms en haut du fichier de code comme suit :

    ```csharp
    using System.Collections;
    using UnityEngine;
    using UnityEngine.SceneManagement;
    using UnityEngine.Video;
    ```

6.  Entrez les variables suivantes dans la classe **VideoController** , ainsi que la méthode **éveillé ()** :

    ```csharp
        /// <summary> 
        /// Provides Singleton-like behaviour to this class. 
        /// </summary> 
        public static VideoController instance; 
        
        /// <summary> 
        /// Reference to the Camera VideoPlayer Component.
        /// </summary> 
        private VideoPlayer videoPlayer; 
        
        /// <summary>
        /// Reference to the Camera AudioSource Component.
        /// </summary> 
        private AudioSource audioSource; 
        
        /// <summary> 
        /// Reference to the texture used to project the video streaming 
        /// </summary> 
        private RenderTexture videoStreamRenderTexture;

        /// <summary>
        /// Insert here the first video endpoint
        /// </summary>
        private string video1endpoint = "-- Insert video 1 Endpoint here --";

        /// <summary>
        /// Insert here the second video endpoint
        /// </summary>
        private string video2endpoint = "-- Insert video 2 Endpoint here --";

        /// <summary> 
        /// Reference to the Inside-Out Sphere. 
        /// </summary> 
        public GameObject sphere;

        void Awake()
        {
            instance = this;
        }
    ```

7.  Maintenant, vous pouvez entrer les points de terminaison à partir de vos vidéos Azure Media Services :

    1.  Premier dans la variable *video1endpoint* .
    
    2.  Deuxième dans la variable *video2endpoint* .

    > [!WARNING]
    > Il existe un problème connu lié à l’utilisation de *https* dans Unity, avec la version 2017.4.1 F1. Si les vidéos fournissent une erreur lors de la lecture, essayez d’utiliser « http » à la place.

8.  Ensuite, la méthode **Start ()** doit être modifiée. Cette méthode est déclenchée chaque fois que l’utilisateur change de scène (en basculant la vidéo) en regardant le bouton de regard.

    ```csharp
        // Use this for initialization
        void Start()
        {
            Application.runInBackground = true;
            StartCoroutine(PlayVideo());
        }
    ```

9.  À la suite de la méthode **Start ()** , insérez la méthode **playVideo ()** *IEnumerator* , qui sera utilisée pour démarrer des vidéos de manière transparente (aucune interruption n’est détectée).

    ```csharp
        private IEnumerator PlayVideo()
        {
            // create a new render texture to display the video 
            videoStreamRenderTexture = new RenderTexture(2160, 1440, 32, RenderTextureFormat.ARGB32);

            videoStreamRenderTexture.Create();

            // assign the render texture to the object material 
            Material sphereMaterial = sphere.GetComponent<Renderer>().sharedMaterial;

            //create a VideoPlayer component 
            videoPlayer = gameObject.AddComponent<VideoPlayer>();

            // Set the video to loop. 
            videoPlayer.isLooping = true;

            // Set the VideoPlayer component to play the video from the texture 
            videoPlayer.renderMode = VideoRenderMode.RenderTexture;

            videoPlayer.targetTexture = videoStreamRenderTexture;

            // Add AudioSource 
            audioSource = gameObject.AddComponent<AudioSource>();

            // Pause Audio play on Awake 
            audioSource.playOnAwake = true;
            audioSource.Pause();

            // Set Audio Output to AudioSource 
            videoPlayer.audioOutputMode = VideoAudioOutputMode.AudioSource;
            videoPlayer.source = VideoSource.Url;

            // Assign the Audio from Video to AudioSource to be played 
            videoPlayer.EnableAudioTrack(0, true);
            videoPlayer.SetTargetAudioSource(0, audioSource);

            // Assign the video Url depending on the current scene 
            switch (SceneManager.GetActiveScene().name)
            {
                case "VideoScene1":
                    videoPlayer.url = video1endpoint;
                    break;

                case "VideoScene2":
                    videoPlayer.url = video2endpoint;
                    break;

                default:
                    break;
            }

            //Set video To Play then prepare Audio to prevent Buffering 
            videoPlayer.Prepare();

            while (!videoPlayer.isPrepared)
            {
                yield return null;
            }

            sphereMaterial.mainTexture = videoStreamRenderTexture;

            //Play Video 
            videoPlayer.Play();

            //Play Sound 
            audioSource.Play();

            while (videoPlayer.isPlaying)
            {
                yield return null;
            }
        }
    ```

10. La dernière méthode dont vous avez besoin pour cette classe est la méthode **ChangeScene ()** , qui sera utilisée pour échanger des scènes.

    ```csharp
        public void ChangeScene()
        {
            SceneManager.LoadScene(SceneManager.GetActiveScene().name == "VideoScene1" ? "VideoScene2" : "VideoScene1");
        }
    ```

    > [!TIP] 
    > La méthode **ChangeScene ()** utilise une fonctionnalité C\# pratique appelée *opérateur conditionnel*. Cela permet de vérifier les conditions, puis les valeurs retournées en fonction du résultat de la vérification, dans une instruction unique. Suivez ce [lien pour en savoir plus sur l’opérateur conditionnel](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/conditional-operator).

11. Enregistrez vos modifications dans Visual Studio avant de revenir à Unity.

12. De retour dans l’éditeur Unity, cliquez et faites glisser la classe **VideoController** [from] {. Underline} le dossier **scripts** vers l’objet **Camera principal** dans le panneau **hiérarchie** .

13. Cliquez sur l' **appareil photo principal** et observez le panneau de l' **inspecteur**. Vous remarquerez que dans le composant script qui vient d’être ajouté, il existe un champ avec une valeur vide. Il s’agit d’un champ de référence qui cible les variables publiques dans votre code.

14. Faites glisser l’objet **InsideOutSphere** du **volet** de la hiérarchie vers l’emplacement **Sphere** , comme indiqué dans l’image ci-dessous.

    ![créer la classe VideoController](images/AzureLabs-Lab6-47.png)
    ![créer la classe VideoController](images/AzureLabs-Lab6-48.png)

## <a name="chapter-6---create-the-gaze-class"></a>Chapitre 6-créer la classe en regard

Cette classe est chargée de créer un **Raycast** qui se transmettra à l’avant à partir de la **caméra principale**, pour détecter l’objet que l’utilisateur examine. Dans ce cas, le **Raycast** doit déterminer si l’utilisateur regarde l’objet **GazeButton** dans la scène et déclencher un comportement.

Pour créer cette classe :

1.  Accédez au dossier **scripts** que vous avez créé précédemment.

2.  Cliquez avec le bouton droit dans le panneau **projet** , **créez* * C\# script * *. Nommez le script point de **regard**.

3.  Double-cliquez sur le nouveau script de ***regard*** pour l’ouvrir avec **Visual Studio 2017.**

4.  Assurez-vous que l’espace de noms suivant figure en haut du script et supprimez les autres :

    ```csharp
    using UnityEngine;
    ```

5.  Ajoutez ensuite les variables suivantes à l’intérieur de la classe **regard** :

    ```csharp
        /// <summary> 
        /// Provides Singleton-like behaviour to this class. 
        /// </summary> 
        public static Gaze instance;

        /// <summary> 
        /// Provides a reference to the object the user is currently looking at. 
        /// </summary> 
        public GameObject FocusedGameObject { get; private set; }

        /// <summary> 
        /// Provides a reference to compare whether the user is still looking at 
        /// the same object (and has not looked away). 
        /// </summary> 
        private GameObject oldFocusedObject = null;

        /// <summary> 
        /// Max Ray Distance 
        /// </summary> 
        float gazeMaxDistance = 300;

        /// <summary> 
        /// Provides whether an object has been successfully hit by the raycast. 
        /// </summary> 
        public bool Hit { get; private set; }
    ```

6.  Vous devez maintenant ajouter du code pour les méthodes **éveillé ()** et **Start ()** .

    ```csharp
        private void Awake()
        {
            // Set this class to behave similar to singleton 
            instance = this;
        }

        void Start()
        {
            FocusedGameObject = null;
        }
    ```

7.  Ajoutez le code suivant dans la méthode **Update ()** pour projeter un Raycast et détecter l’accès cible :

    ```csharp
        void Update()
        {
            // Set the old focused gameobject. 
            oldFocusedObject = FocusedGameObject;
            RaycastHit hitInfo;

            // Initialise Raycasting. 
            Hit = Physics.Raycast(Camera.main.transform.position, Camera.main.transform.forward, out hitInfo, gazeMaxDistance);

            // Check whether raycast has hit. 
            if (Hit == true)
            {
                // Check whether the hit has a collider. 
                if (hitInfo.collider != null)
                {
                    // Set the focused object with what the user just looked at. 
                    FocusedGameObject = hitInfo.collider.gameObject;
                }
                else
                {
                    // Object looked on is not valid, set focused gameobject to null. 
                    FocusedGameObject = null;
                }
            }
            else
            {
                // No object looked upon, set focused gameobject to null.
                FocusedGameObject = null;
            }

            // Check whether the previous focused object is this same 
            // object (so to stop spamming of function). 
            if (FocusedGameObject != oldFocusedObject)
            {
                // Compare whether the new Focused Object has the desired tag we set previously. 
                if (FocusedGameObject.CompareTag("GazeButton"))
                {
                    FocusedGameObject.SetActive(false);
                    VideoController.instance.ChangeScene();
                }
            }
        }
    ```

8.  Enregistrez vos modifications dans Visual Studio avant de revenir à Unity.

9.  Cliquez et faites glisser **la classe pointage du dossier** scripts vers l’objet caméra principal dans le panneau **hiérarchie** .

## <a name="chapter-7---setup-the-two-unity-scenes"></a>Chapitre 7 : configurer les deux scènes d’Unity

L’objectif de ce chapitre est de configurer les deux scènes, chacune hébergeant une vidéo à diffuser. Vous allez dupliquer la scène que vous avez déjà créée, afin de ne pas avoir à la reconfigurer, bien que vous modifiiez ensuite la nouvelle scène, afin que l’objet *GazeButton* se trouve à un emplacement différent et ait une apparence différente. Il s’agit de montrer comment changer entre les scènes.

1.  Pour ce faire, accédez à **fichier > enregistrer la scène sous...** . Une fenêtre d’enregistrement s’affiche. Cliquez sur le bouton **nouveau dossier** .

    ![Chapitre 7 : configurer les deux scènes d’Unity](images/AzureLabs-Lab6-49.png)

2.  Nommez le dossier **scenes**.

3.  La fenêtre **enregistrer la scène** est toujours ouverte. Ouvrez le dossier **scenes** que vous venez de créer.

4.  Dans le champ **nom de fichier :** , tapez **VideoScene1**, puis cliquez sur **Enregistrer**.

5.  De retour dans Unity, ouvrez votre dossier **scenes** , puis cliquez sur votre fichier **VideoScene1** . À l’aide de votre clavier, appuyez sur **Ctrl + D** pour dupliquer cette scène

    > [!TIP]
    > La commande **dupliquée** peut également être exécutée en accédant à **Modifier > doublon**.

6.  Unity incrémente automatiquement le numéro de nom de la scène, mais vérifie tout de même qu’il correspond au code précédemment inséré.

    >  Vous devez avoir **VideoScene1** et **VideoScene2**.

7.  Avec les deux scènes, accédez à **fichier > paramètres de build**. Une fois la fenêtre des **paramètres de build** ouverte, faites glisser vos scènes jusqu’à la section **scenes dans la build** .

    ![Chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-50.png)

    > [!TIP] 
    > Vous pouvez sélectionner les deux scènes dans votre dossier **scenes** tout en maintenant le bouton **CTRL** enfoncé, puis en cliquant avec le bouton gauche sur chaque scène et en faisant glisser les deux à la fois.

8.  Fermez la fenêtre **paramètres de build** , puis double-cliquez sur **VideoScene2**.

9.  Une fois la deuxième scène ouverte, cliquez sur l’objet enfant **GazeButton** du **InsideOutSphere**et définissez sa transformation comme suit :

    |            |    TRANSFORMATION-POSITION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |         **Y** 1,3         | **Z** 3,6 |

    |            |    TRANSFORMATION-ROTATION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |          **Y** 0          |  **Z** 0  |

    |            |     TRANSFORMATION-METTRE À L’ÉCHELLE     |           |
    | :---------:| :-----------------------: | :--------:|
    |  **X** 1   |          **Y** 1          |  **Z** 1  |

10. Avec l’enfant **GazeButton** toujours sélectionné, examinez l' **inspecteur** et le **filtre de maillage**. Cliquez sur la petite cible en regard du champ de référence de **maillage** :

    ![Chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-51.png)

11. Une fenêtre contextuelle **Sélectionner le maillage** s’affiche. Double-cliquez sur la maille du **cube** dans la liste des **ressources**.

    ![Chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-52.png)

12. Le **filtre de maillage** est mis à jour et est maintenant un **cube**. Maintenant, cliquez sur l’icône d' **engrenage** en regard de **Sphere collision** , puis cliquez sur **supprimer le composant**pour supprimer le conflit de cet objet.

    ![Chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-53.png)

13. Avec la **GazeButton** toujours sélectionnée, cliquez sur le bouton **Ajouter un composant** situé en bas de l' **inspecteur**. Dans le champ de recherche, la **zone**type et le **conflit de zone** sont une option qui permet d’ajouter un **conflit Box** à votre objet **GazeButton** .

    ![Chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-54.png)

14. Le **GazeButton** est maintenant partiellement mis à jour. Toutefois, vous allez maintenant créer un nouveau **matériau**, afin qu’il soit complètement différent et qu’il soit plus facile à reconnaître en tant qu’objet différent que l’objet dans la première scène.

15. Accédez à votre dossier **Materials** , dans le **panneau Projet**. Dupliquez le matériel **ButtonMaterial** (appuyez sur **CTRL** + **D** sur le clavier ou cliquez sur le **matériau**, puis sélectionnez **dupliquer**dans l’option de menu **modifier** le fichier).

    ![le chapitre 7--configurer les deux scènes Unity](images/AzureLabs-Lab6-55.png)
    ![chapitre 7--configurez les deux scènes Unity](images/AzureLabs-Lab6-56.png)

16. Sélectionnez le nouveau matériel **ButtonMaterial** (nommé **ButtonMaterial 1**) et, dans l' **inspecteur**, cliquez sur la fenêtre de couleur **Albedo** . Une fenêtre contextuelle s’affiche, dans laquelle vous pouvez sélectionner une autre couleur (choisissez celle qui vous plaît), puis fermer la fenêtre contextuelle. Le matériau sera sa propre instance et différent de l’original.

    ![Chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-57.png)

17. Faites glisser le nouveau **matériau** sur l’enfant **GazeButton** pour mettre à jour complètement son apparence, afin qu’il soit facilement facile à distinguer du bouton premières scènes.

    ![Chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-58.png)

18. À ce stade, vous pouvez tester le projet dans l’éditeur avant de générer le projet UWP.

    -  Appuyez sur le bouton de **lecture** dans l' **éditeur** et portez votre casque.

        ![Chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-59.png)

19. Examinez les deux objets **GazeButton** pour basculer entre la première et la deuxième vidéo.

## <a name="chapter-8---build-the-uwp-solution"></a>Chapitre 8-créer la solution UWP

Une fois que vous avez vérifié que l’éditeur n’a pas d’erreurs, vous êtes prêt à générer.

Pour générer :

1.  Enregistrez la scène en cours en cliquant sur **fichier > enregistrer**.

2.  Activez la case à cocher « **Unity C\# projets** » (c’est important, car cela vous permettra de modifier les classes une fois la génération terminée).

3.  Accédez à **fichier > paramètres de build**, puis cliquez sur **Build**.

4.  Vous serez invité à sélectionner le dossier dans lequel vous souhaitez buildThe la solution.

5.  Créez un dossier **Builds** et, dans ce dossier, créez un autre dossier avec le nom approprié de votre choix.

6.  Cliquez sur votre nouveau dossier, puis sur **Sélectionner un dossier**, afin de choisir ce dossier, pour commencer la build à cet emplacement.

    ![chapitre 8--créer la solution UWP](images/AzureLabs-Lab6-60.png)
    ![chapitre 8--créer la solution UWP](images/AzureLabs-Lab6-61.png)

7.  Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build.

## <a name="chapter-9---deploy-on-local-machine"></a>Chapitre 9-déployer sur l’ordinateur local

Une fois la génération terminée, une fenêtre de l' **Explorateur de fichiers** s’affiche à l’emplacement de votre Build. Ouvrez le dossier que vous avez nommé et créé, puis double-cliquez sur le fichier de solution (. sln) dans ce dossier pour ouvrir votre solution avec Visual Studio 2017.

La seule chose à faire est de déployer votre application sur votre ordinateur (ou *ordinateur local*).

Pour effectuer le déploiement sur l’ordinateur local :

1.  Dans **Visual Studio 2017**, ouvrez le fichier solution qui vient d’être créé.

2.  Dans la **plateforme**de la solution, sélectionnez **x86, ordinateur local**.

3.  Dans la **configuration** de la solution, sélectionnez **Déboguer**.

    ![Chapitre 9--déployer sur l’ordinateur local](images/AzureLabs-Lab6-62.png)

4.  Vous devez à présent restaurer les packages dans votre solution. Cliquez avec le bouton droit sur votre **solution**, puis cliquez sur **restaurer les packages NuGet pour la solution...**

    > [!NOTE] 
    > Cela est dû au fait que les packages créés par Unity doivent être ciblés pour fonctionner avec vos références d’ordinateurs locaux.

5.  Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre ordinateur. Visual Studio commence par générer, puis déployer votre application.

6.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.

    ![Chapitre 9--déployer sur l’ordinateur local](images/AzureLabs-Lab6-63.png)

Lorsque vous exécutez l’application de réalité mixte, vous êtes dans le modèle **InsideOutSphere** que vous avez utilisé dans votre application. Cette sphère sera l’endroit où la vidéo sera diffusée, en fournissant une vue 360 de la vidéo entrante (qui a été filmée pour ce type de perspective). Ne soyez pas surpris si le chargement de la vidéo prend quelques secondes, votre application est soumise à votre vitesse Internet disponible, car la vidéo doit être récupérée, puis téléchargée, afin de diffuser dans votre application.
Quand vous êtes prêt, modifiez les scènes et ouvrez votre deuxième vidéo, par Gazing à la sphère rouge ! N’hésitez pas à revenir en arrière, en utilisant le cube bleu dans la deuxième scène !

## <a name="your-finished-azure-media-service-application"></a>Votre application Azure Media service terminée
 
Félicitations, vous avez créé une application de réalité mixte qui tire parti d’Azure Media service pour diffuser des vidéos 360.

![résultat de l’atelier](images/AzureLabs-Lab6-00.png)

![résultat de l’atelier](images/AzureLabs-Lab6-01.png)

## <a name="bonus-exercises"></a>Exercices bonus

**Exercice 1**

Il est tout à fait possible d’utiliser une seule scène pour modifier les vidéos de ce didacticiel. Expérimentez votre application et faites-en une seule scène ! Peut-être même ajouter une autre vidéo à la combinaison.

**Exercice 2**

Expérimentez Azure et Unity et tentez d’implémenter la possibilité pour l’application de sélectionner automatiquement une vidéo avec une taille de fichier différente, en fonction de la force d’une connexion Internet.


