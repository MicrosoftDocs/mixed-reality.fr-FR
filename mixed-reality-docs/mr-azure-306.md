---
title: MR et Azure 306 - diffusion en continu de vidéo
description: Terminer ce cours pour apprendre à implémenter Azure Media Services au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, streaming media services, vidéo, 360, immersives, vr
ms.openlocfilehash: f6974ab6a72828a557649d5dc65b4e505a7484ff
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594019"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br> 

# <a name="mr-and-azure-306-streaming-video"></a>MR et Azure 306 : Diffusion en continu de vidéo

![produit final-Démarrer](images/AzureLabs-Lab6-00.png)
![finale du produit-Démarrer](images/AzureLabs-Lab6-01.png)

Dans ce cours, vous allez apprendre comment connecter votre Azure Media Services à une expérience de VR de réalité mixte Windows pour autoriser la lecture vidéo de 360 degrés sur des casques IMMERSIFS de diffusion en continu. 

**Azure Media Services** sont une collection de services qui vous offre des services de streaming de vidéo de qualité télévisuelle pour atteindre un large public sur les appareils mobiles populaires d’aujourd'hui. Pour plus d’informations, visitez le [page d’Azure Media Services](https://azure.microsoft.com/services/media-services).

Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte, qui sera en mesure d’effectuer les opérations suivantes :

1. Récupérer une vidéo de 360 degrés à partir d’un **stockage Azure**, jusqu'à la **Azure Media Services**.

2. Afficher la vidéo de 360 degrés récupérées dans une scène Unity.

3. Naviguer entre les deux scènes, avec deux vidéos différents.

Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception. Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity. Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 306 : Diffusion en continu de vidéo</td><td style="text-align: center;"> </td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer l’article outils](install-the-tools.md), mais il doit être pas supposé que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .

Nous recommandons le matériel et logiciel pour ce cours suivants :

- Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)
- [Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé](install-the-tools.md#installation-checklist)
- [Le SDK Windows 10 dernières](install-the-tools.md#installation-checklist)
- [Unity 2017.4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md)
- Accès à Internet pour la récupération de données et le programme d’installation Azure
- Deux vidéos à 360 degrés au format mp4 (vous trouverez des vidéos libres [à cette page de téléchargement](https://www.mettle.com/360vr-master-series-free-360-downloads-page))

## <a name="before-you-start"></a>Avant de commencer

1.  Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).
2.  Configurer et tester votre casque immersives de réalité mixte.

    > [!NOTE]
    > Vous allez **pas** nécessitent des contrôleurs de mouvement pour ce cours. Si vous avez besoin de prendre en charge de paramétrage le casque immersives, veuillez cliquer [lien sur la façon de configurer Windows Mixed Reality](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).

## <a name="chapter-1---the-azure-portal-creating-the-azure-storage-account"></a>Chapitre 1 : le portail Azure : création du compte de stockage Azure

Pour utiliser le **Service de stockage Azure**, vous devez créer et configurer un **compte de stockage** dans le portail Azure.

1.  Connectez-vous à la [Azure Portal](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **comptes de stockage** dans le menu de gauche.

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab6-02.png)

3.  Sur le **comptes de stockage** onglet, cliquez sur **ajouter**.

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab6-03.png)

4.  Dans le **créer le compte de stockage** onglet :

    1.  Insérer un **nom** pour votre compte, n’oubliez pas ce champ accepte uniquement des lettres minuscules et chiffres.

    2.  Pour **modèle de déploiement,** sélectionnez **Resource manager**.

    3.  Pour **type de compte**, sélectionnez **stockage (usage général v1)**.

    4.  Pour **performances**, sélectionnez **Standard*.**

    5.  Pour **réplication** sélectionnez **stockage localement redondant (LRS)**.

    6.  Laissez **transfert sécurisé requis** comme **désactivé**.

    7.  Sélectionnez un **abonnement**.

    8.  Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.

    9.  Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions.

5.  Vous devrez confirmer que vous avez compris les termes et Conditions appliquées à ce Service.

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab6-04.png)

6.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.

7.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab6-05.png)

8.  À ce stade vous n’avez pas besoin de suivre la ressource, il suffit de déplacer le chapitre suivant.

## <a name="chapter-2---the-azure-portal-creating-the-media-service"></a>Chapitre 2 : le portail Azure : création du Service de média

Pour utiliser le Service de média Azure, vous devrez configurer une instance du service à être mis à disposition de votre application (où le titulaire du compte doit être un administrateur).

1.  Dans le portail Azure, cliquez sur **créer une ressource** dans le coin supérieur gauche coin inférieur droit, puis recherchez **Service multimédia,** appuyez sur **entrée**. Sur la ressource actuellement possède une icône rose ; cliquez dessus, pour afficher une nouvelle page.

    ![Le portail Azure](images/AzureLabs-Lab6-06.png)

2.  La nouvelle page doit fournir une description de la **Service multimédia**. En bas à gauche de cette invite, cliquez sur le **créer** bouton permettant de créer une association avec ce service.

    ![Le portail Azure](images/AzureLabs-Lab6-07.png)

3.  Une fois que vous avez cliqué sur **créer** un panneau s’affiche où vous devez fournir des détails sur votre nouveau Service de support :

    1.  Insérez votre souhaitée **nom du compte** pour cette instance de service.

    2.  Sélectionnez un **abonnement**.

    3. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs). 
    
    > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la gestion des groupes de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    4.  Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources). Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute. Certaines ressources Azure sont uniquement disponibles dans certaines régions.

    5.  Pour le **compte de stockage** , cliquez sur le **Veuillez sélectionner...**  section, puis cliquez sur le **compte de stockage** vous avez créé dans le dernier chapitre.

    6.  Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.

    7.  Cliquez sur **Create (Créer)**.

        ![Le portail Azure](images/AzureLabs-Lab6-08.png)

4.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.

5.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![Le portail Azure](images/AzureLabs-Lab6-09.png)

6.  Cliquez sur la notification pour Explorer votre nouvelle instance de Service.

    ![Le portail Azure](images/AzureLabs-Lab6-10.png)

7.  Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.

8.  Dans la nouvelle page de service de média, dans le volet gauche, cliquez sur le **actifs** lien, qui vise à mi-chemin vers le bas.

9.  Dans la page suivante, dans l’angle supérieur gauche de la page, cliquez sur **télécharger**.

    ![Le portail Azure](images/AzureLabs-Lab6-11.png)

10. Cliquez sur le **dossier** icône pour parcourir vos fichiers et sélectionnez la vidéo 360 tout d’abord que vous souhaitez diffuser en continu. 
    
    > Vous pouvez suivre cette [lien pour télécharger un exemple de vidéo](https://vimeo.com/214401712).

    ![Le portail Azure](images/AzureLabs-Lab6-12.png)

> [!WARNING]
> Noms de fichiers longs peut entraîner un problème avec l’encodeur : pour vous assurer de vidéos n’ont pas de problèmes, vous devez donc raccourcir la longueur des noms de votre fichier vidéo.

11. La barre de progression devient verte lorsque la vidéo a fini de télécharger.

    ![Le portail Azure](images/AzureLabs-Lab6-13.png)

12. Cliquez sur le texte ci-dessus (**yourservicename - ressources**) pour revenir à la **actifs** page.

13. Vous remarquerez que votre vidéo a été téléchargée avec succès. Cliquez dessus.

    ![Le portail Azure](images/AzureLabs-Lab6-14.png)

14. Affiche la page que vous êtes redirigé vers que vous des informations détaillées sur votre vidéo. Pour pouvoir utiliser votre vidéo, vous devez encoder, en cliquant sur le **Encode** bouton en haut à gauche de la page.

    ![Le portail Azure](images/AzureLabs-Lab6-15.png)

15. Un nouveau panneau s’affiche à droite, où vous serez en mesure de définir les options de codage pour votre fichier. Définissez les propriétés suivantes (certaines seront déjà défini par défaut) :

    1.  **Nom de l’encodeur multimédia *Media Encoder Standard***

    2.  **Présélection d’encodage *contenu ADAPTATIF MP4 à plusieurs débits***

    3.  **Nom de la tâche *traitement Media Encoder Standard de Video1.mp4***

    4.  **Nom du fichier multimédia sortie *Video1.mp4--Media Encoder Standard encodé***

        ![Le portail Azure](images/AzureLabs-Lab6-16.png)

16. Cliquez sur le bouton **Créer**.

17. Vous remarquerez une barre avec **travail d’encodage ajouté**, cliquez sur cette barre et un panneau s’affiche avec la progression de l’encodage affichée dans celui-ci.

    ![Le portail Azure](images/AzureLabs-Lab6-17.png)

    ![Le portail Azure](images/AzureLabs-Lab6-18.png)

18. Attendez la fin du travail. Une fois que cela est fait, n’hésitez pas à fermer le panneau avec le « X » en haut à droite de ce panneau.

    ![Le portail Azure](images/AzureLabs-Lab6-19.png)

    ![Le portail Azure](images/AzureLabs-Lab6-20.png)

    > [!IMPORTANT]
    > La durée, dépend de la taille du fichier de votre vidéo. Ce processus peut prendre un certain temps.

19. Maintenant que la version codée de la vidéo a été créée, vous pouvez le publier pour le rendre accessible. Pour ce faire, cliquez sur le lien bleu **actifs** pour revenir à la page de ressources.

    ![Le portail Azure](images/AzureLabs-Lab6-21.png)

20. Vous verrez votre vidéo, ainsi que l’autre, ce qui est de **Type de ressource *MP4 multidébit***.

    ![Le portail Azure](images/AzureLabs-Lab6-22.png)

    > [!NOTE] 
    > Vous pouvez remarquer que le nouvel élément multimédia, en même temps que votre vidéo initial, est *inconnu*, et a octets '0' pour qu’il est **taille**, actualisez simplement votre fenêtre pour pouvoir mettre à jour.

21. Cliquez sur cette nouvelle ressource.

    ![Le portail Azure](images/AzureLabs-Lab6-23.png)

22. Vous verrez un panneau semblable à celle que vous avez utilisé auparavant, simplement, il s’agit d’une autre ressource. Cliquez sur le **publier** bouton situé au centre en haut de la page.

    ![Le portail Azure](images/AzureLabs-Lab6-24.png)

23. Vous êtes invité à définir un **localisateur**, qui est le point d’entrée au fichier/s dans vos éléments multimédias. Pour votre scénario, définissez les propriétés suivantes :

    1.  **Type de localisateur** > **progressif**.

    2.  Le **date** et **temps** sont définies pour vous, à partir de votre date actuelle, à une heure dans le futur (cent ans dans le cas présent). Laissez tel quel ou le modifier en fonction.

    > [!NOTE]
    > Pour plus d’informations sur les localisateurs, et vous pouvez choisir, visitez le [Documentation Azure Media Services](https://docs.microsoft.com/azure/media-services/media-services-concepts).

24. En bas de ce panneau, cliquez sur le **ajouter** bouton.

    ![Le portail Azure](images/AzureLabs-Lab6-25.png)

25. Votre vidéo est à présent publiée et puisse être diffusé en continu à l’aide de son point de terminaison. Plus bas de la page est un **fichiers** section. Ceci est l’emplacement codé en différentes versions de votre vidéo. Sélectionnez la plus élevée possible une résolution (dans l’image ci-dessous est le 1920 x 960 fichier), et un volet à droite s’affichera. Vous y trouverez un **URL de téléchargement**. Copiez cette **point de terminaison** car vous l’utiliserez ultérieurement dans votre code.

    ![Le portail Azure](images/AzureLabs-Lab6-26.png)    

    ![Le portail Azure](images/AzureLabs-Lab6-27.png)

    > [!NOTE] 
    > Vous pouvez également appuyer sur la **lire** bouton pour lire votre vidéo et le tester.

26. Vous devez maintenant télécharger la deuxième vidéo que vous utiliserez dans ce laboratoire. Suivez les étapes ci-dessus, en répétant le même processus pour la deuxième vidéo. Assurez-vous que vous copiez la deuxième **point de terminaison** également. Utilisez la commande suivante [lien pour télécharger une vidéo deuxième](https://vimeo.com/214402865).

27. Une fois que les deux vidéos ont été publiés, vous êtes prêt à passer au chapitre suivant.

## <a name="chapter-3---setting-up-the-unity-project"></a>Chapitre 3 - Configuration du projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez **Unity** et cliquez sur **New**. 

    ![Le portail Azure](images/AzureLabs-Lab6-28.png)

2.  Vous devez maintenant fournir un nom de projet Unity, insérer **MR\_360VideoStreaming.**. Assurez-vous que le type de projet est défini sur **3D**. Définissez l’emplacement d’un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![Le portail Azure](images/AzureLabs-Lab6-29.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio.** Accédez à ***modifier* *préférences*** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![Le portail Azure](images/AzureLabs-Lab6-30.png)

4.  Ensuite, accédez à ***fichier* *paramètres de Build*** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **Plateforme de commutation** bouton.

5.  Assurez-vous également que :

    1. **Équipement cible** a la valeur **n’importe quel appareil.**
    
    2.  **Type de build** a la valeur **D3D.**

    3.  **Kit de développement logiciel** a la valeur **dernière installé.**

    4.  **Version de Visual Studio** a la valeur **dernière installé.**

    5.  **Générez et exécutez** est défini sur **ordinateur Local.**

    6.  Ne vous inquiétez pas sur la configuration de **scènes** dès que vous allez configurer ces ultérieurement.

    7.  Les autres paramètres doivent être conservées comme valeur par défaut pour l’instant.

        ![Configuration du projet Unity](images/AzureLabs-Lab6-31.png)

6.  Dans le **paramètres de Build** fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le **inspecteur** se trouve. 

7. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1.  Dans le **autres paramètres** onglet :

        1.  **Écriture de scripts** **Version du Runtime** doit être **Stable** (équivalent .NET 3.5).

        2. **Script principal** doit être **.NET.**

        3. **Niveau de compatibilité d’API** doit être **.NET 4.6.**

            ![Configuration du projet Unity](images/AzureLabs-Lab6-32.png)

    2.  Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.

        ![Configuration du projet Unity](images/AzureLabs-Lab6-33.png)

    3.  Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        - **InternetClient**

            ![Configuration du projet Unity](images/AzureLabs-Lab6-34.png)

8.  Une fois que vous avez effectué ces modifications, fermez le **paramètres de Build** fenêtre.

9.  Enregistrer votre projet **fichier* *enregistrer projet **.



## <a name="chapter-4---importing-the-insideoutsphere-unity-package"></a>Chapitre 4 - Importation du package InsideOutSphere Unity

> [!IMPORTANT]
> Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/Azure-MR-306.unitypackage), importez-le dans votre projet comme un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de **chapitre 5**. Vous devez toujours créer un projet Unity.

Pour ce cours, vous devez télécharger un Package de ressource Unity appelé [ **InsideOutSphere.unitypackage**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20306%20-%20Streaming%20video/InsideOutSphere.unitypackage).

Importation de procédures relatives à la **package**:

1.  Avec le tableau de bord Unity devant vous, cliquez sur **actifs** dans le menu en haut de l’écran, puis cliquez sur **importer un Package > Custom Package**.

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-35.png)

2.  Utilisez le sélecteur de fichiers pour sélectionner le **InsideOutSphere.unitypackage** du package et cliquez sur **Open**. Une liste des composants de cette ressource s’affichera pour vous. Confirmez l’importation en cliquant sur **importer**.

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-36.png)

3.  Une fois l’importation terminée, vous remarquerez trois nouveaux dossiers, **matériaux**, **modèles**, et **Prefabs**, ont été ajoutées à votre **actifs**dossier. Ce type de structure de dossiers est généralement utilisé pour un projet Unity.

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-37.png)

    1.  Ouvrez le **modèles** dossier et vous verrez que le **InsideOutSphere** modèle a été importé.

    2.  Dans le **matériaux** dossier, vous trouverez le **InsideOutSpheres** matériau *lambert1*, ainsi que d’un matériau appelé *ButtonMaterial*, qui est utilisé par le GazeButton, que vous le verrez bientôt.

    3.  Le **Prefabs** dossier contient le **InsideOutSphere** préfabriqué qui contient à la fois le **InsideOutSphere** *modèle* et le  *GazeButton*.

    4.  **Aucun code n’est inclus**, vous allez écrire le code en suivant ce cours.


4.  Dans le **hiérarchie**, sélectionnez le **Main Camera** l’objet et de mettre à jour les composants suivants :

    1.  **Transform**

        1.  Position = **X**: 0, **Y**: 0, **Z**: 0.

        2. Rotation = **X**: 0, **Y**: 0, **Z**: 0.

        3. Mise à l’échelle **X**: 1, **Y**: 1, **Z**: 1.

    2.  **Appareil photo**

        1. **Effacer les indicateurs**: Couleur unie.

        2.  **Plans de détourage**: Près de : 0,1, à présent : 6.

            ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-38.png)

5.  Accédez à la **Prefab** dossier, puis faites glisser le **InsideOutSphere** prefab dans le **hiérarchie** Panneau de configuration.

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-39.png)

6.  Développez le **InsideOutSphere** de l’objet dans le **hiérarchie** en cliquant sur la petite flèche située en regard de celle-ci. Vous verrez un **enfant** objet dessous appelé **GazeButton**. Cela sera utilisé pour modifier l’arrière-plan et par conséquent, des vidéos.

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-40.png)

7.  Dans la fenêtre Inspecteur, cliquez sur le **InsideOutSphere**du composant de transformation, assurez-vous que les propriétés suivantes sont définies :

    |            |    TRANSFORMATION - POSITION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |          **Y** 0          |  **Z** 0  |

    |            |    TRANSFORMATION - ROTATION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |          **Y** -50        |  **Z** 0  |

    |            |     TRANSFORMATION - MISE À L’ÉCHELLE     |           |
    | :---------:| :-----------------------: | :--------:|
    |  **X** 1   |          **Y** 1          |  **Z** 1  |

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-41.png)

8.  Cliquez sur le **GazeButton** objet enfant et définissez son **transformer** comme suit :

    |            |    TRANSFORMATION - POSITION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 3.6|          **Y** 1.3        |  **Z** 0  |

    |            |    TRANSFORMATION - ROTATION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |          **Y** 0          |  **Z** 0  |

    |            |     TRANSFORMATION - MISE À L’ÉCHELLE     |           |
    | :---------:| :-----------------------: | :--------:|
    |  **X** 1   |          **Y** 1          |  **Z** 1  |

    ![Importation du Package InsideOutSphere Unity](images/AzureLabs-Lab6-42.png)


## <a name="chapter-5---create-the-videocontroller-class"></a>Chapitre 5 : créer la classe VideoController

Le **VideoController** classe héberge les deux points de terminaison vidéo permet de diffuser le contenu à partir du Service de média Azure.

Pour créer cette classe :

1.  Avec le bouton droit dans le **dossier composants**, situé dans le **projet** Panneau de configuration, puis cliquez sur **créer > dossier**. Nommez le dossier **Scripts**.

    ![Créer la classe VideoController](images/AzureLabs-Lab6-43.png)

    ![Créer la classe VideoController](images/AzureLabs-Lab6-44.png)

2.  Double-cliquez sur le **Scripts** dossier pour l’ouvrir.

3.  Avec le bouton droit dans le dossier, puis cliquez sur **créer > C\# Script**. Nommez le script **VideoController**.

    ![Créer la classe VideoController](images/AzureLabs-Lab6-45.png)

4.  Double-cliquez sur le nouveau **VideoController** script pour l’ouvrir avec **Visual Studio 2017.**

    ![Créer la classe VideoController](images/AzureLabs-Lab6-46.png)

5.  Mettre à jour les espaces de noms en haut du fichier de code comme suit :

    ```csharp
    using System.Collections;
    using UnityEngine;
    using UnityEngine.SceneManagement;
    using UnityEngine.Video;
    ```

6.  Entrez les variables suivantes dans le **VideoController** classe, ainsi que la **Awake()** méthode :

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

7.  Il est temps de saisir les points de terminaison de vos vidéos Azure Media Services :

    1.  Le premier dans le *video1endpoint* variable.
    
    2.  La seconde dans le *video2endpoint* variable.

    > [!WARNING]
    > Il existe un problème connu avec à l’aide de *https* dans Unity, avec la version 2017.4.1f1. Si les vidéos fournissent une erreur sur play, essayez plutôt d’utiliser « http ».

8.  Ensuite, le **Start()** méthode doit être modifié. Cette méthode est déclenchée chaque fois que l’utilisateur change de scène (basculement en conséquence de la vidéo) en examinant le bouton d’utilisation.

    ```csharp
        // Use this for initialization
        void Start()
        {
            Application.runInBackground = true;
            StartCoroutine(PlayVideo());
        }
    ```

9.  Suivant le **Start()** (méthode), insérez le **PlayVideo()** *IEnumerator* (méthode), qui sera utilisé pour démarrer des vidéos en toute transparence (donc aucune interruption ne se produite).

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

10. La dernière méthode que vous avez besoin de cette classe est la **ChangeScene()** (méthode), qui sera utilisé pour basculer entre deux séquences.

    ```csharp
        public void ChangeScene()
        {
            SceneManager.LoadScene(SceneManager.GetActiveScene().name == "VideoScene1" ? "VideoScene2" : "VideoScene1");
        }
    ```

    > [!TIP] 
    > Le **ChangeScene()** méthode utilise une pratique C\# fonctionnalité appelée la *opérateur conditionnel*. Ainsi, les conditions à vérifier, et puis valeurs retournées en fonction du résultat de la vérification, au sein d’une instruction unique. Suivez ce [lien en savoir plus sur l’opérateur conditionnel](https://docs.microsoft.com/dotnet/csharp/language-reference/operators/conditional-operator).

11. Enregistrez vos modifications dans Visual Studio avant de retourner à Unity.

12. Précédent dans l’éditeur Unity, cliquez et faites glisser le **VideoController** classe [from] {.underline} le **Scripts** dossier pour le **Main Camera** de l’objet dans le  **Hiérarchie** Panneau de configuration.

13. Cliquez sur le **Main Camera** et examinez le **panneau Inspecteur**. Vous remarquerez que dans le composant de Script qui vient d’être ajouté, est un champ avec une valeur vide. Il s’agit d’un champ de référence, qui cible les variables publiques dans votre code.

14. Faites glisser le **InsideOutSphere** à partir de l’objet le **hiérarchie panneau** à la **sphère** emplacement, comme illustré dans l’image ci-dessous.

    ![Créer la classe VideoController](images/AzureLabs-Lab6-47.png)
    ![créer la classe VideoController](images/AzureLabs-Lab6-48.png)

## <a name="chapter-6---create-the-gaze-class"></a>Chapitre 6 : créer la classe du pointage de regard

Cette classe est chargée pour la création d’un **Raycast** que beprojected transfère à partir de la **Main Camera**, pour détecter quel objet consulte l’utilisateur. Dans ce cas, le **Raycast** devra identifier si l’utilisateur consulte la **GazeButton** de l’objet dans la scène et déclencher un comportement.

Pour créer cette classe :

1.  Accédez à la **Scripts** dossier que vous avez créé précédemment.

2.  Avec le bouton droit dans le **projet** panneau, **créer* *C\# Script**. Nommez le script **les regards**.

3.  Double-cliquez sur le nouveau ***les regards*** script pour l’ouvrir avec **Visual Studio 2017.**

4.  Vérifiez que l’espace de noms suivant s’affiche en haut du script et supprimez tous les autres :

    ```csharp
    using UnityEngine;
    ```

5.  Puis ajoutez les variables suivantes à l’intérieur de la **les regards** classe :

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

6.  Code pour le **Awake()** et **Start()** méthodes doit maintenant être ajouté.

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

7.  Ajoutez le code suivant dans le **Update()** méthode projeter une Raycast et de détecter le positionnement de la cible :

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

8.  Enregistrez vos modifications dans Visual Studio avant de retourner à Unity.

9.  Cliquez et faites glisser le **les regards** classe à partir du dossier Scripts à l’objet Main Camera dans le **hiérarchie** Panneau de configuration.

## <a name="chapter-7---setup-the-two-unity-scenes"></a>Chapitre 7 - le programme d’installation les deux Unity scènes

L’objectif de ce chapitre consiste à configurer les deux scènes, chacune hébergeant une vidéo au flux. Vous allez dupliquer la scène, vous avez déjà créé, afin qu’est inutile de l’ajouter à nouveau, bien que vous allez ensuite modifier la nouvelle scène, afin que le *GazeButton* objet est dans un emplacement différent et a une apparence différente. Il s’agit de montrer comment changer entre les scènes.

1.  Cela en accédant à **fichier > Enregistrer la scène en tant que...** . Une fenêtre d’enregistrement s’affiche. Cliquez sur le **nouveau dossier** bouton.

    ![Chapitre 7 - le programme d’installation les deux Unity scènes](images/AzureLabs-Lab6-49.png)

2.  Nommez le dossier **scènes**.

3.  Le **enregistrer la scène** fenêtre sera toujours ouverte. Ouvrez votre nouvellement créé **scènes** dossier.

4.  Dans le **nom de fichier :** champ de texte, tapez **VideoScene1**, puis appuyez sur **enregistrer**.

5.  Dans Unity, ouvrez votre **scènes** dossier et cliquez sur votre **VideoScene1** fichier. Utiliser le clavier, appuyez sur **Ctrl + D** vous allez dupliquer cette scène

    > [!TIP]
    > Le **dupliquer** commande peut également être effectuée en accédant à **Modifier > Dupliquer**.

6.  Unity sera automatiquement incrémente le nombre de noms de scène, mais vérifier tout de même, pour vous assurer qu’il correspond au code inséré précédemment.

    >  Vous devez avoir **VideoScene1** et **VideoScene2**.

7.  Avec vos deux scènes, accédez à **fichier > Paramètres de Build**. Avec le **paramètres de Build** fenêtre ouverte, faites glisser votre arrière-plan pour le **scènes dans la Build** section.

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-50.png)

    > [!TIP] 
    > Vous pouvez sélectionner les deux de vos scènes à partir de votre **scènes** dossier via contenant le **Ctrl** bouton, puis clic gauche chaque scène et enfin, faites glisser les deux sur.

8.  Fermer le **paramètres de Build** fenêtre et double-clic sur **VideoScene2**.

9.  Avec la seconde séquence ouverte, cliquez sur le **GazeButton** objet enfant de la **InsideOutSphere**et définissez sa transformation comme suit :

    |            |    TRANSFORMATION - POSITION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |         **Y** 1.3         | **Z** 3.6 |

    |            |    TRANSFORMATION - ROTATION   |           |
    | :---------:| :-----------------------: | :--------:|
    |   **X** 0  |          **Y** 0          |  **Z** 0  |

    |            |     TRANSFORMATION - MISE À L’ÉCHELLE     |           |
    | :---------:| :-----------------------: | :--------:|
    |  **X** 1   |          **Y** 1          |  **Z** 1  |

10. Avec le **GazeButton** enfants étant toujours sélectionnée, regardez à la **inspecteur** et à la **filtre Mesh**. Cliquez sur la cible peu en regard du **Mesh** champ de référence :

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-51.png)

11. Un **sélectionnez maillage** fenêtre contextuelle s’affiche. Double-cliquez sur le **Cube** de maillage dans la liste des **ressources**.

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-52.png)

12. Le **filtre Mesh** met à jour et être maintenant un **Cube**. Maintenant, cliquez sur le **ENGRENAGE** icône située à côté **sphère Collider** et cliquez sur **supprimer un composant**, permet de supprimer le collider de cet objet.

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-53.png)

13. Avec le **GazeButton** toujours sélectionnée, cliquez sur le **ajouter un composant** bouton en bas de la **inspecteur**. Dans le champ de recherche, tapez **boîte**, et **Collider de la boîte de** sera l’option--cliquer ici, pour ajouter un **boîte Collider** à votre **GazeButton** objet .

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-54.png)

14. Le **GazeButton** est maintenant mis à jour partiellement, pour un aspect différent, toutefois, vous allez maintenant créer un nouveau **matériau**, afin qu’il est complètement différente et est plus facile à reconnaître qu’un autre objet, à la objet dans la première séquence.

15. Accédez à votre **matériaux** dossier, en respectant le **panneau projet**. Dupliquer la **ButtonMaterial** matériau (appuyez sur **Ctrl** + **D** sur le clavier, ou cliquez sur le **matériau**, puis à partir de la **modifier** option de menu, sélectionnez fichier **dupliquer**).

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-55.png)
    ![chapitre 7 : configurer les deux scènes Unity](images/AzureLabs-Lab6-56.png)

16. Sélectionnez la nouvelle **ButtonMaterial** matériau (ici nommé **ButtonMaterial 1**) et dans le **inspecteur**, cliquez sur le **Albedo** couleur fenêtre. Une fenêtre contextuelle s’affiche, dans laquelle vous pouvez sélectionner une autre couleur (choisissez celle que vous préférez), puis fermez la fenêtre contextuelle. Le matériel d’être sa propre instance et l’autre à l’original.

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-57.png)

17. Faites glisser la nouvelle **matériau** sur le **GazeButton** enfant, désormais entièrement mis à jour son apparence, afin qu’il soit facilement reconnaissable à partir du premier bouton de scènes.

    ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-58.png)

18. À ce stade, vous pouvez tester le projet dans l’éditeur avant de générer le projet UWP.

    -  Appuyez sur la **lire** situé dans le **éditeur** et porter votre casque.

        ![Chapitre 7 : Configurer les deux scènes Unity](images/AzureLabs-Lab6-59.png)

19. Examinez les deux **GazeButton** objets pour basculer entre la première et deuxième vidéo.

## <a name="chapter-8---build-the-uwp-solution"></a>Chapitre 8 - générer la Solution UWP

Une fois que vous vous assurez que l’éditeur n’a aucune erreur, vous êtes prêt à générer.

Pour générer :

1.  Enregistrer la scène actuelle en cliquant sur **fichier > Enregistrer**.

2.  Cochez la case appelée **Unity C\# projets** (Ceci est important, car il vous permettra de modifier les classes après de la build est terminée).

3.  Accédez à **fichier > Paramètres de Build**, cliquez sur **Build**.

4.  Vous êtes invité à sélectionner le dossier où vous souhaitez buildthe Solution.

5.  Créer un **génère** dossier et dans ce dossier, créez un autre dossier avec un nom approprié de votre choix.

6.  Cliquez sur votre nouveau dossier, puis **sélectionner le dossier**, par conséquent, pour choisir ce dossier, pour commencer la génération à cet emplacement.

    ![Chapitre 8--Générer la Solution UWP](images/AzureLabs-Lab6-60.png)
    ![chapitre 8--générer la Solution UWP](images/AzureLabs-Lab6-61.png)

7.  Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build.

## <a name="chapter-9---deploy-on-local-machine"></a>Chapitre 9 - déployer sur l’ordinateur Local

Une fois la build terminée, un **Explorateur de fichiers** fenêtre s’affiche à l’emplacement de votre build. Ouvrez le dossier que vous avez nommé et intégrées à, puis double-cliquez sur le fichier solution (.sln) dans ce dossier, pour ouvrir votre solution avec Visual Studio 2017.

La seule chose à faire est de déployer votre application sur votre ordinateur (ou *ordinateur Local*).

Pour déployer sur l’ordinateur Local :

1.  Dans **Visual Studio 2017**, ouvrez le fichier solution qui vient d’être créé.

2.  Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.

3.  Dans le **Configuration de la Solution** sélectionnez **déboguer**.

    ![Chapitre 9--Déployer sur l’ordinateur Local](images/AzureLabs-Lab6-62.png)

4.  Maintenant, vous devrez restaurer tous les packages à votre solution. Avec le bouton droit sur votre **Solution**, puis cliquez sur **restaurer les Packages NuGet pour la Solution...**

    > [!NOTE] 
    > Pour cela, car les packages qui Unity généré doivent être ciblés pour fonctionner avec vos références de machines locales.

5.  Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur. Visual Studio tout d’abord créer et déployer votre application.

6.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.

    ![Chapitre 9--Déployer sur l’ordinateur Local](images/AzureLabs-Lab6-63.png)

Lorsque vous exécutez l’application de réalité mixte, vous allez vous se trouver dans le **InsideOutSphere** modèle que vous avez utilisées au sein de votre application. Ce domaine sera où la vidéo est diffusée, en fournissant une vue à 360 degrés, de la vidéo entrante (qui a été filmée pour ce type de point de vue). Ne soyez pas surpris que si la vidéo prend quelques secondes pour charger, votre application est soumis à vitesse de votre Internet disponible, comme la vidéo doit être extraite, puis téléchargées, par conséquent, pour diffuser en continu dans votre application.
Lorsque vous êtes prêt, modifier l’arrière-plan et ouvrez votre deuxième vidéo, par gazing à la sphère rouge ! Puis n’hésitez pas à revenir en arrière à l’aide du cube bleu dans la seconde séquence !

## <a name="your-finished-azure-media-service-application"></a>Votre application Azure Media Services terminée
 
Félicitations, vous avez créé une application de réalité mixte qui tire parti du Service de média Azure pour diffuser des 360 vidéos.

![résultat de laboratoire](images/AzureLabs-Lab6-00.png)

![résultat de laboratoire](images/AzureLabs-Lab6-01.png)

## <a name="bonus-exercises"></a>Exercices de bonus

**Exercice 1**

Il est tout à fait possible d’utiliser uniquement une scène unique pour modifier des vidéos au sein de ce didacticiel. Faire des essais avec votre application et la convertir en une scène unique ! Peut-être même ajouter une autre vidéo à la combinaison.

**Exercice 2**

Faire des essais avec Azure et Unity et tentez de mettre en œuvre la possibilité pour l’application sélectionner automatiquement une vidéo avec une taille de fichier différent, en fonction du niveau d’une connexion Internet.


