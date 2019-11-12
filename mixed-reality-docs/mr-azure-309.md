---
title: MR et Azure 309-application Insights
description: Suivez ce cours pour apprendre à collecter des analyses concernant le comportement des utilisateurs au sein d’une application de réalité mixte, à l’aide du service Azure Application Insights.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, Unity, didacticiel, API, application Insights, hololens, immersif, VR
ms.openlocfilehash: 481fe3fc16ada06085a64c86867a1a892c76f2ad
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926902"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

<br> 

# <a name="mr-and-azure-309-application-insights"></a>MR et Azure 309 : application Insights

![produit final-début](images/AzureLabs-Lab309-00.png)

Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de Application Insights à une application de réalité mixte, à l’aide de l’API Azure Application Insights pour collecter des analyses concernant le comportement des utilisateurs.

Application Insights est un service Microsoft qui permet aux développeurs de collecter des analyses à partir de leurs applications et de les gérer à partir d’un portail facile à utiliser. Les analyses peuvent avoir n’importe quelle valeur, des performances aux informations personnalisées que vous souhaitez collecter. Pour plus d’informations, consultez la [page application Insights](https://azure.microsoft.com/services/application-insights/).

Une fois ce cours terminé, vous disposerez d’une application de casque immersif en réalité mixte, qui sera en mesure d’effectuer les opérations suivantes :

1.  Autorisez l’utilisateur à se déplacer dans une scène.
2.  Déclencher l’envoi des analyses au *Service application Insights*, par le biais de l’utilisation du regard et de la proximité des objets dans la scène.
3.  L’application appellera également sur le service, en extrayant les informations sur l’objet qui a été approché le plus par l’utilisateur au cours des dernières 24 heures. Cet objet va changer sa couleur en vert.

Ce cours vous apprend à obtenir les résultats du service Application Insights, dans un exemple d’application à base d’Unity. Il vous faudra appliquer ces concepts à une application personnalisée que vous pouvez générer.

## <a name="device-support"></a>Périphériques pris en charge

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 309 : application Insights</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Bien que ce cours se concentre principalement sur les casques de Windows Mixed Reality (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours à Microsoft HoloLens. À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge HoloLens. Lorsque vous utilisez HoloLens, vous remarquerez peut-être un écho pendant la capture vocale.

## <a name="prerequisites"></a>Conditions préalables

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours :

- Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)
- [Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé](install-the-tools.md#installation-checklist)
- [Le dernier Kit de développement logiciel Windows 10](install-the-tools.md#installation-checklist)
- [Unity 2017,4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé
- Un jeu de casque avec un microphone intégré (si le casque n’a pas de MIC et de haut-parleurs intégrés)
- Accès Internet pour l’installation d’Azure et la récupération des données de Application Insights

## <a name="before-you-start"></a>Avant de commencer

Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).

> [!WARNING] 
> N’oubliez pas que les données qui vont *application Insights* prennent du temps, donc soyez patient. Si vous souhaitez vérifier si le service a reçu vos données, consultez le [chapitre 14](#chapter-14---the-application-insights-service-portal), qui vous montrera comment naviguer dans le portail.

## <a name="chapter-1---the-azure-portal"></a>Chapitre 1-portail Azure

Pour utiliser *application Insights*, vous devez créer et configurer un *Service Application Insights* dans le portail Azure.

1.  Connectez-vous au [portail Azure](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas encore de compte Azure, vous devez en créer un. Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche, recherchez *application Insights*, puis cliquez sur **entrée**.

    > [!NOTE]
    > Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.

    ![Portail Azure](images/AzureLabs-Lab309-01.png)

3.  La nouvelle page qui s’affiche à droite fournit une description du service *Azure application Insights* . En bas à gauche de cette page, cliquez sur le bouton **créer** pour créer une association avec ce service.

    ![Portail Azure](images/AzureLabs-Lab309-02.png)

4.  Une fois que vous avez cliqué sur **créer**:

    1.  Insérez le **nom** de votre choix pour cette instance de service.

    2.  Pour **type d’application**, sélectionnez **général**.

    3.  Sélectionnez un **abonnement**approprié.

    4.  Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5.  Sélectionnez un **emplacement**.

    6.  Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.

    7.  Sélectionnez **Créer**.

        ![Portail Azure](images/AzureLabs-Lab309-03.png)

5.  Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.

6.  Une notification s’affichera dans le portail une fois l’instance de service créée.

    ![Portail Azure](images/AzureLabs-Lab309-04.png)

7.  Cliquez sur les notifications pour explorer votre nouvelle instance de service.

    ![Portail Azure](images/AzureLabs-Lab309-05.png)

8.  Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service. Vous êtes dirigé vers votre nouvelle instance de *Service application Insights* .

    ![Portail Azure](images/AzureLabs-Lab309-06.png)

    > [!NOTE]
    >  Gardez cette page Web ouverte et facile à consulter. vous y reviendrez souvent pour voir les données collectées.

    > [!IMPORTANT]
    > Pour implémenter Application Insights, vous devrez utiliser trois (3) valeurs spécifiques : la **clé d’instrumentation**, l' **ID d’application**et la **clé API**. Vous verrez ci-dessous comment récupérer ces valeurs à partir de votre service. Veillez à noter ces valeurs dans une page vide du *bloc-notes* , car vous les utiliserez bientôt dans votre code.

9.  Pour trouver la **clé d’instrumentation**, vous devez faire défiler la liste des fonctions de service, puis cliquer sur **Propriétés**. l’onglet affiché affiche la **clé de service**.

    ![Portail Azure](images/AzureLabs-Lab309-07.png)

10. Une petite des **Propriétés**ci-dessous vous permet d' **accéder à l’API**, sur laquelle vous devez cliquer. Le panneau à droite fournit l’ID d' **application** de votre application.

    ![Portail Azure](images/AzureLabs-Lab309-08.png)

11. Si le panneau de l’ID de l' **application** est toujours ouvert, cliquez sur **créer une clé API**pour ouvrir le panneau *créer une clé API* .

    ![Portail Azure](images/AzureLabs-Lab309-09.png)

12. Dans le volet créer maintenant une *clé d’API* , tapez une description et **cochez les trois cases**.

13. Cliquez sur **générer la clé**. Votre **clé API** sera créée et affichée. 

    ![Portail Azure](images/AzureLabs-Lab309-10.png)
        
    > [!WARNING]
    > Il s’agit de la seule fois où votre **clé de service** sera affichée. Veillez donc à en faire une copie maintenant.

## <a name="chapter-2---set-up-the-unity-project"></a>Chapitre 2-configurer le projet Unity

Ce qui suit est une configuration classique pour le développement avec la réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **nouveau**.

    ![Configurer le projet Unity](images/AzureLabs-Lab309-11.png)

2.  Vous devez maintenant fournir un nom de projet Unity, insérer **rm\_application Azure\_\_Insights**. Assurez-vous que le *modèle* est défini sur **3D**. Définissez l' *emplacement* approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés). Ensuite, cliquez sur **créer un projet**.

    ![Configurer le projet Unity](images/AzureLabs-Lab309-12.png)

3.  Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**. Accédez à **modifier \> préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**. Remplacez l' **éditeur de script externe** par **Visual Studio 2017**. Fermez la fenêtre **Préférences** .

    ![Configurer le projet Unity](images/AzureLabs-Lab309-13.png)

4.  Accédez ensuite à **fichier \> paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .

    ![Configurer le projet Unity](images/AzureLabs-Lab309-14.png)

5.  Accédez à **fichier \> paramètres de build** et assurez-vous que :

    1.  L' **appareil cible** est défini sur **n’importe quel appareil**

        > Pour Microsoft HoloLens, définissez **appareil cible** sur *HoloLens*.

    2.  Le **type de build** est **D3D**

    3.  Le **SDK** est configuré sur le **dernier installé**

    4.  La **génération et l’exécution** sont définies sur l' **ordinateur local**

    5.  Enregistrez la scène et ajoutez-la à la Build.

        1.  Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**. Une fenêtre d’enregistrement s’affiche.

            ![Configurer le projet Unity](images/AzureLabs-Lab309-15.png)

        2. Créez un nouveau dossier pour cela, ainsi que toute scène future, puis cliquez sur le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez-le **scenes**.

            ![Configurer le projet Unity](images/AzureLabs-Lab309-16.png)

        3. Ouvrez le dossier **scenes** nouvellement créé, puis dans le champ *nom de fichier :* , tapez **ApplicationInsightsScene**, puis cliquez sur **Enregistrer**.

            ![Configurer le projet Unity](images/AzureLabs-Lab309-17.png)

6.  Les paramètres restants, dans **paramètres de build**, doivent être laissés par défaut pour le moment.

7.  Dans la fenêtre **paramètres de build** , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** .

    ![Configurer le projet Unity](images/AzureLabs-Lab309-18.png)

8. Dans ce volet, quelques paramètres doivent être vérifiés :

    1.  Sous l’onglet **autres paramètres** :

        1.  La **version du runtime** de **script** doit être **expérimentale (.net 4,6 équivalent)** , ce qui déclenche la nécessité de redémarrer l’éditeur.

        2.  Le **backend de script** doit être **.net**

        3.  Le **niveau de compatibilité** de l’API doit être **.net 4,6**

        ![Configurer le projet Unity](images/AzureLabs-Lab309-19.png)

    2.  Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher :

        - **InternetClient**     

            ![Configurer le projet Unity](images/AzureLabs-Lab309-20.png)

    3.  Plus bas dans le panneau, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.

        ![Configurer le projet Unity](images/AzureLabs-Lab309-21.png)

9.  De retour dans les **paramètres de build**, les  **C# projets Unity** ne sont plus grisés. Cochez la case en regard de cette option.

10.  Fermez la fenêtre Paramètres de Build.

11.  Enregistrez votre scène et votre projet (**fichier** > **enregistrer la scène/le fichier** > enregistrer le **projet**).


## <a name="chapter-3---import-the-unity-package"></a>Chapitre 3-importer le package Unity

> [!IMPORTANT]
> Si vous souhaitez ignorer les composants de *configuration d’Unity* de ce cours et continuer à accéder directement au code, n’hésitez pas à télécharger ce fichier [Azure-Mr-309. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/Azure-MR-309.unitypackage), importez-le dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html). Elle contient également les dll du chapitre suivant. Après l’importation, passez [**au chapitre 6**](#chapter-6---create-the-applicationinsightstracker-class).

> [!IMPORTANT]
> Pour utiliser Application Insights dans Unity, vous devez importer la DLL associée, ainsi que la DLL Newtonsoft. Il existe actuellement un problème connu dans Unity qui nécessite que les plug-ins soient reconfigurés après l’importation. Ces étapes (4-7 dans cette section) ne sont plus nécessaires une fois que le bogue a été résolu.

Pour importer Application Insights dans votre propre projet, assurez-vous d’avoir [téléchargé « . pour Unity », contenant les plug-ins](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/AppInsights_LabPlugins.unitypackage). Ensuite, procédez comme suit :

1.  Ajoutez le fichier **. pour Unity** à Unity à l’aide de l’option de menu **ressources \> importer le package \> package personnalisé** .

2.  Dans la zone **importer le package Unity** qui s’affiche, vérifiez que tous les **plug-ins** sous (et y compris) sont sélectionnés.

    ![Importer le package Unity](images/AzureLabs-Lab309-22.png)

3.  Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.

4.  Accédez au dossier **Insights** sous **plug-ins** dans la vue projet et sélectionnez les plug-ins suivants *uniquement*:

    -   Microsoft. ApplicationInsights

    ![Importer le package Unity](images/AzureLabs-Lab309-23.png)

5.  Si ce *plug-in* est sélectionné, assurez-vous que **toutes les plateformes** sont **décochées**, vérifiez que **WSAPlayer** est également **désactivé**, puis cliquez sur **appliquer**. Cela suffit pour confirmer que les fichiers sont correctement configurés.

    ![Importer le package Unity](images/AzureLabs-Lab309-24.png)

    > [!NOTE]
    > Le marquage des plug-ins comme celui-ci permet de les configurer pour qu’ils soient utilisés uniquement dans l’éditeur Unity. Il existe un ensemble différent de dll dans le dossier WSA qui sera utilisé une fois que le projet est exporté d’Unity.

6.  Ensuite, vous devez ouvrir le dossier **WSA** , dans le dossier **Insights** . Vous verrez une copie du même fichier que celui que vous venez de configurer. Sélectionnez ce fichier, puis, dans l’inspecteur, assurez-vous que **toutes les plateformes** **sont décochées**, puis vérifiez que **seul** **WSAPlayer** est **activé**. Cliquez sur **Apply** (Appliquer).

    ![Importer le package Unity](images/AzureLabs-Lab309-25.png)

7. Vous devez maintenant suivre les **étapes 4-6**, mais pour les plug-ins *Newtonsoft* à la place. Consultez la capture d’écran ci-dessous pour savoir à quoi doit ressembler le résultat.

    ![Importer le package Unity](images/AzureLabs-Lab309-25-5.png)    

## <a name="chapter-4---set-up-the-camera-and-user-controls"></a>Chapitre 4-configurer l’appareil photo et les contrôles utilisateur

Dans ce chapitre, vous allez configurer l’appareil photo et les contrôles pour permettre à l’utilisateur de voir et de se déplacer dans la scène.

1.  Cliquez avec le bouton droit dans une zone vide du panneau hiérarchie, puis sur **créer** > **vide**.

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-26.png)

2.  Renommez le nouveau GameObject vide en **parent Camera**.

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-27.png)

3.  Cliquez avec le bouton droit dans une zone vide du panneau hiérarchie, puis sur **objet 3D**, puis sur **sphère**.

4.  Renommez la sphère **avec la main droite**.

5.  Définissez l' **échelle de transformation** de la main droite sur **0,1, 0,1, 0,1**

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-28.png)

6.  Retirez le composant **Sphere collision** de la main droite en cliquant sur l' **engrenage** dans le composant *Sphere collision* , puis en **supprimant le composant**.

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-29.png)

7.  Dans le panneau hiérarchie, faites glisser les objets main **Camera** et **Right main** sur l’objet **parent Camera** .

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-30.png)

8.  Définissez la **position** de la transformation de la **caméra principale** et de l’objet de **droite** sur **0, 0,** 0.

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-31.png)

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-32.png)

## <a name="chapter-5---set-up-the-objects-in-the-unity-scene"></a>Chapitre 5-configurer les objets dans la scène Unity

Vous allez maintenant créer des formes de base pour votre scène, avec lesquelles l’utilisateur peut interagir.

1.  Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, puis sur **objet 3D**et sélectionnez **plan**.

2.  Définissez la position de la **transformation** du plan sur **0,-1, 0**.

3.  Affectez à l' **échelle de transformation** du plan la valeur **5, 1, 5**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-33.png)

4.  Créez un matériau de base à utiliser avec votre objet **plan** , afin que les autres formes soient plus faciles à voir. Accédez au *panneau Projet*, cliquez avec le bouton droit, puis **créez**, suivi de **dossier**, pour créer un nouveau dossier. Nommez-la **matériel**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-34.png) ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-35.png)

5.  Ouvrez le dossier **matériaux** , cliquez avec le bouton droit sur, cliquez sur **créer**, puis sur **matériau**, pour créer un nouveau matériau. Nommez-le **Blue**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-36.png) ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-37.png)

6.  Une fois le nouveau matériau **bleu** sélectionné, examinez l' *inspecteur*, puis cliquez sur la fenêtre rectangulaire à côté de **Albedo**. Sélectionnez une couleur bleue (la seule image ci-dessous est **couleur hexadécimale : \#3592FFFF**). Cliquez sur le bouton Fermer une fois que vous avez choisi.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-38.png)

7.  Faites glisser votre nouveau matériel à partir du dossier **matériaux** , sur le **plan**que vous venez de créer, dans votre scène (ou déposez-le sur l’objet **plan** dans la *hiérarchie*).

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-39.png)

8.  Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, puis sur **objet 3D, capsule**.

    -  Une fois la **capsule** sélectionnée, remplacez sa *position* de **transformation** par : **-10, 1,0**.

9.  Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, puis sur **objet 3D, cube**.

    -  Une fois le **cube** sélectionné, remplacez sa *position* de **transformation** par : **0, 0, 10**.

10. Cliquez avec le bouton droit dans une zone vide du *panneau hiérarchie*, puis sur **objet 3D, sphère**.

    -  Une fois la **sphère** sélectionnée, modifiez sa *position* de **transformation** en : **10, 0, 0**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-40.png)

    > [!NOTE]
    > Ces valeurs de *position* sont des *suggestions*. Vous êtes libre de définir la position des objets sur ce que vous souhaitez, bien qu’il soit plus facile pour l’utilisateur de l’application si les distances des objets ne sont pas trop éloignées de l’appareil photo.

11. Lorsque votre application est en cours d’exécution, elle doit être en mesure d’identifier les objets dans la scène. pour ce faire, elle doit être marquée. Sélectionnez l’un des objets, puis dans le panneau *inspecteur* , cliquez sur **Ajouter une étiquette...** , qui permutera l' *inspecteur* avec les **balises & panneau couches** .

    ![configurer les objets dans la scène Unity](images/AzureLabs-Lab309-41.png) ![](images/AzureLabs-Lab309-42.png)

12. Cliquez sur le signe **+ (plus)** , puis tapez le nom de la balise en tant que **ObjectInScene**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-43.png)

    > [!WARNING]
    > Si vous utilisez un nom différent pour votre balise, vous devez vous assurer que cette modification est également apportée aux scripts *DataFromAnalytics*, *ObjectTrigger*et pointage par la *suite, afin*que vos objets soient détectés et détectés dans votre scène.

13. Une fois la balise créée, vous devez l’appliquer à tous les trois objets. Dans la *hiérarchie*, maintenez la **touche Maj** enfoncée, cliquez sur les objets **capsule**, **cube**et **sphère**, puis dans l' *inspecteur*, cliquez sur le menu déroulant avec la **balise**, puis cliquez sur la balise *ObjectInScene* que vous avez créée.

    ![configurer les objets dans la scène Unity](images/AzureLabs-Lab309-44.png) ![](images/AzureLabs-Lab309-45.png)

## <a name="chapter-6---create-the-applicationinsightstracker-class"></a>Chapitre 6-créer la classe ApplicationInsightsTracker

Le premier script que vous devez créer est **ApplicationInsightsTracker**, qui est responsable des opérations suivantes :

1.  Création d’événements basés sur les interactions de l’utilisateur à envoyer à Azure Application Insights.

2. Création des noms d’événements appropriés, en fonction de l’interaction de l’utilisateur.

3. Envoi d’événements à l’instance de service Application Insights.

Pour créer cette classe :

1.  Cliquez avec le bouton droit dans le *panneau Projet*, puis **créez** > **dossier**. Nommez le dossier **scripts**.

    ![Créer la classe ApplicationInsightsTracker](images/AzureLabs-Lab309-46.png)  ![Créer la classe ApplicationInsightsTracker](images/AzureLabs-Lab309-47.png)

2.  Une fois le dossier **scripts** créé, double-cliquez dessus pour l’ouvrir. Ensuite, dans ce dossier, cliquez avec le bouton droit sur, puis **créez** >  **C# script**. Nommez le script **ApplicationInsightsTracker**.

3.  Double-cliquez sur le nouveau script **ApplicationInsightsTracker** pour l’ouvrir avec **Visual Studio**.

4.  Mettez à jour les espaces de noms en haut du script pour qu’ils soient comme indiqué ci-dessous :

    ```csharp
        using Microsoft.ApplicationInsights;
        using Microsoft.ApplicationInsights.DataContracts;
        using Microsoft.ApplicationInsights.Extensibility;
        using UnityEngine;
    ```

5.  À l’intérieur de la classe, insérez les variables suivantes :

    ```csharp
        /// <summary>
        /// Allows this class to behavior like a singleton
        /// </summary>
        public static ApplicationInsightsTracker Instance;
        
        /// <summary>
        /// Insert your Instrumentation Key here
        /// </summary>
        internal string instrumentationKey = "Insert Instrumentation Key here";

        /// <summary>
        /// Insert your Application Id here
        /// </summary>
        internal string applicationId = "Insert Application Id here";

        /// <summary>
        /// Insert your API Key here
        /// </summary>
        internal string API_Key = "Insert API Key here";

        /// <summary>
        /// Represent the Analytic Custom Event object
        /// </summary>
        private TelemetryClient telemetryClient;

        /// <summary>
        /// Represent the Analytic object able to host gaze duration
        /// </summary>
        private MetricTelemetry metric;
    ```

    > [!NOTE] 
    > Définissez les valeurs **instrumentationKey, ApplicationId et API_Key** de manière appropriée, à l’aide des *clés de service* à partir du portail Azure, comme indiqué au [Chapitre 1](#chapter-1---the-azure-portal), étape 9.

6.  Ajoutez ensuite les méthodes **Start ()** et **éveillé ()** , qui seront appelées lorsque la classe est initialisée :

    ```csharp
        /// <summary>
        /// Sets this class instance as a singleton
        /// </summary>
        void Awake()
        {
            Instance = this;
        }

        /// <summary>
        /// Use this for initialization
        /// </summary>
        void Start()
        {
            // Instantiate telemetry and metric
            telemetryClient = new TelemetryClient();

            metric = new MetricTelemetry();

            // Assign the Instrumentation Key to the Event and Metric objects
            TelemetryConfiguration.Active.InstrumentationKey = instrumentationKey;

            telemetryClient.InstrumentationKey = instrumentationKey;
        }
    ```

7.  Ajoutez les méthodes responsables de l’envoi des événements et des métriques inscrits par votre application :

    ```csharp
        /// <summary>
        /// Submit the Event to Azure Analytics using the event trigger object
        /// </summary>
        public void RecordProximityEvent(string objectName)
        {
            telemetryClient.TrackEvent(CreateEventName(objectName));
        }

        /// <summary>
        /// Uses the name of the object involved in the event to create 
        /// and return an Event Name convention
        /// </summary>
        public string CreateEventName(string name)
        {
            string eventName = $"User near {name}";
            return eventName;
        }

        /// <summary>
        /// Submit a Metric to Azure Analytics using the metric gazed object
        /// and the time count of the gaze
        /// </summary>
        public void RecordGazeMetrics(string objectName, int time)
        {
            // Output Console information about gaze.
            Debug.Log($"Finished gazing at {objectName}, which went for <b>{time}</b> second{(time != 1 ? "s" : "")}");

            metric.Name = $"Gazed {objectName}";

            metric.Value = time;

            telemetryClient.TrackMetric(metric);
        }
    ```

8.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.

## <a name="chapter-7---create-the-gaze-script"></a>Chapitre 7-créer le script de regard

Le script suivant à créer **est le script de regard.** Ce script est chargé de créer un *Raycast* qui sera projeté à partir de l' *appareil photo principal*, afin de détecter l’objet que l’utilisateur examine. Dans ce cas, le *Raycast* doit déterminer si l’utilisateur Regarde un objet avec la balise **ObjectInScene** , puis compter la durée pendant laquelle l’utilisateur fait un *regard* sur cet objet.

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir.

2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** >  **C# script**. Nommez le script point de **regard**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Remplacez le code existant par ce qui suit :

    ```csharp
        using UnityEngine;

        public class Gaze : MonoBehaviour
        {
            /// <summary>
            /// Provides Singleton-like behavior to this class.
            /// </summary>
            public static Gaze Instance;

            /// <summary>
            /// Provides a reference to the object the user is currently looking at.
            /// </summary>
            public GameObject FocusedGameObject { get; private set; }

            /// <summary>
            /// Provides whether an object has been successfully hit by the raycast.
            /// </summary>
            public bool Hit { get; private set; }

            /// <summary>
            /// Provides a reference to compare whether the user is still looking at 
            /// the same object (and has not looked away).
            /// </summary>
            private GameObject _oldFocusedObject = null;

            /// <summary>
            /// Max Ray Distance
            /// </summary>
            private float _gazeMaxDistance = 300;

            /// <summary>
            /// Max Ray Distance
            /// </summary>
            private float _gazeTimeCounter = 0;

            /// <summary>
            /// The cursor object will be created when the app is running,
            /// this will store its values. 
            /// </summary>
            private GameObject _cursor;
        }
    ```

5.  Vous devez maintenant ajouter du code pour les méthodes **éveillé ()** et **Start ()** .

    ```csharp
        private void Awake()
        {
            // Set this class to behave similar to singleton
            Instance = this;
            _cursor = CreateCursor();
        }

        void Start()
        {
            FocusedGameObject = null;
        }

        /// <summary>
        /// Create a cursor object, to provide what the user
        /// is looking at.
        /// </summary>
        /// <returns></returns>
        private GameObject CreateCursor()    
        {
            GameObject newCursor = GameObject.CreatePrimitive(PrimitiveType.Sphere);

            // Remove the collider, so it does not block raycast.
            Destroy(newCursor.GetComponent<SphereCollider>());

            newCursor.transform.localScale = new Vector3(0.1f, 0.1f, 0.1f);

            newCursor.GetComponent<MeshRenderer>().material.color = 
            Color.HSVToRGB(0.0223f, 0.7922f, 1.000f);

            newCursor.SetActive(false);
            return newCursor;
        }
    ```

6.  À l’intérieur de la classe de **regard** , ajoutez le code suivant dans la méthode **Update ()** pour projeter un *Raycast* et détecter l’accès cible :

    ```csharp
        /// <summary>
        /// Called every frame
        /// </summary>
        void Update()
        {
            // Set the old focused gameobject.
            _oldFocusedObject = FocusedGameObject;

            RaycastHit hitInfo;

            // Initialize Raycasting.
            Hit = Physics.Raycast(Camera.main.transform.position, Camera.main.transform.forward, out hitInfo, _gazeMaxDistance);

            // Check whether raycast has hit.
            if (Hit == true)
            {
                // Check whether the hit has a collider.
                if (hitInfo.collider != null)
                {
                    // Set the focused object with what the user just looked at.
                    FocusedGameObject = hitInfo.collider.gameObject;

                    // Lerp the cursor to the hit point, which helps to stabilize the gaze.
                    _cursor.transform.position = Vector3.Lerp(_cursor.transform.position, hitInfo.point, 0.6f);

                    _cursor.SetActive(true);
                }
                else
                {
                    // Object looked on is not valid, set focused gameobject to null.
                    FocusedGameObject = null;

                    _cursor.SetActive(false);
                }
            }
            else
            {
                // No object looked upon, set focused gameobject to null.
                FocusedGameObject = null;

                _cursor.SetActive(false);
            }

            // Check whether the previous focused object is this same object. If so, reset the focused object.
            if (FocusedGameObject != _oldFocusedObject)
            {
                ResetFocusedObject();
            }
            // If they are the same, but are null, reset the counter. 
            else if (FocusedGameObject == null && _oldFocusedObject == null)
            {
                _gazeTimeCounter = 0;
            }
            // Count whilst the user continues looking at the same object.
            else
            {
                _gazeTimeCounter += Time.deltaTime;
            }
        }
    ```

7.  Ajoutez la méthode **ResetFocusedObject ()** pour envoyer des données à **application Insights** lorsque l’utilisateur a regardé un objet.

    ```csharp
        /// <summary>
        /// Reset the old focused object, stop the gaze timer, and send data if it
        /// is greater than one.
        /// </summary>
        public void ResetFocusedObject()
        {
            // Ensure the old focused object is not null.
            if (_oldFocusedObject != null)
            {
                // Only looking for objects with the correct tag.
                if (_oldFocusedObject.CompareTag("ObjectInScene"))
                {
                    // Turn the timer into an int, and ensure that more than zero time has passed.
                    int gazeAsInt = (int)_gazeTimeCounter;

                    if (gazeAsInt > 0)
                    {
                        //Record the object gazed and duration of gaze for Analytics
                        ApplicationInsightsTracker.Instance.RecordGazeMetrics(_oldFocusedObject.name, gazeAsInt);
                    }
                    //Reset timer
                    _gazeTimeCounter = 0;
                }
            }
        }
    ```

8.  Vous avez maintenant terminé le script de **regard** . Enregistrez vos modifications dans *Visual Studio* avant de revenir à *Unity*.

## <a name="chapter-8---create-the-objecttrigger-class"></a>Chapitre 8-créer la classe ObjectTrigger

Le prochain script que vous devez créer est **ObjectTrigger**, qui est responsable des opérations suivantes :

- Ajout de composants nécessaires pour la collision à l’appareil photo principal.
- Détection de si l’appareil photo est proche d’un objet marqué comme **ObjectInScene**.

Pour créer le script :

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir.

2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** >  **C# script**. Nommez le script **ObjectTrigger**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio. Remplacez le code existant par ce qui suit :

    ```csharp
        using UnityEngine;

        public class ObjectTrigger : MonoBehaviour
        {
            private void Start()
            {
                // Add the Collider and Rigidbody components, 
                // and set their respective settings. This allows for collision.
                gameObject.AddComponent<SphereCollider>().radius = 1.5f;

                gameObject.AddComponent<Rigidbody>().useGravity = false;
            }

            /// <summary>
            /// Triggered when an object with a collider enters this objects trigger collider.
            /// </summary>
            /// <param name="collision">Collided object</param>
            private void OnCollisionEnter(Collision collision)
            {
                CompareTriggerEvent(collision, true);
            }

            /// <summary>
            /// Triggered when an object with a collider exits this objects trigger collider.
            /// </summary>
            /// <param name="collision">Collided object</param>
            private void OnCollisionExit(Collision collision)
            {
                CompareTriggerEvent(collision, false);
            }

            /// <summary>
            /// Method for providing debug message, and sending event information to InsightsTracker.
            /// </summary>
            /// <param name="other">Collided object</param>
            /// <param name="enter">Enter = true, Exit = False</param>
            private void CompareTriggerEvent(Collision other, bool enter)
            {
                if (other.collider.CompareTag("ObjectInScene"))
                {
                    string message = $"User is{(enter == true ? " " : " no longer ")}near <b>{other.gameObject.name}</b>";

                    if (enter == true)
                    {
                        ApplicationInsightsTracker.Instance.RecordProximityEvent(other.gameObject.name);
                    }
                    Debug.Log(message);
                }
            }
        }
    ```

4.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.

## <a name="chapter-9---create-the-datafromanalytics-class"></a>Chapitre 9-créer la classe DataFromAnalytics

Vous devez maintenant créer le script **DataFromAnalytics** , qui est responsable des opérations suivantes :

- Récupération des données d’analyse sur l’objet le plus proche de l’appareil photo.
- À l’aide des *clés de service*, qui autorisent la communication avec votre instance de service Azure application Insights.
- Tri des objets dans la scène, en fonction du nombre d’événements le plus élevé.
- La modification de la couleur matérielle, de l’objet le plus proche, en *vert*.

Pour créer le script :

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir.

2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** >  **C# script**. Nommez le script **DataFromAnalytics**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Insérez les espaces de noms suivants :

    ```csharp
        using Newtonsoft.Json;
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  Dans le script, insérez ce qui suit :

    ```csharp
        /// <summary>
        /// Number of most recent events to be queried
        /// </summary>
        private int _quantityOfEventsQueried = 10;

        /// <summary>
        /// The timespan with which to query. Needs to be in hours.
        /// </summary>
        private int _timepspanAsHours = 24;

        /// <summary>
        /// A list of the objects in the scene
        /// </summary>
        private List<GameObject> _listOfGameObjectsInScene;

        /// <summary>
        /// Number of queries which have returned, after being sent.
        /// </summary>
        private int _queriesReturned = 0;

        /// <summary>
        /// List of GameObjects, as the Key, with their event count, as the Value.
        /// </summary>
        private List<KeyValuePair<GameObject, int>> _pairedObjectsWithEventCount = new List<KeyValuePair<GameObject, int>>();

        // Use this for initialization
        void Start()
        {
            // Find all objects in scene which have the ObjectInScene tag (as there may be other GameObjects in the scene which you do not want).
            _listOfGameObjectsInScene = GameObject.FindGameObjectsWithTag("ObjectInScene").ToList();

            FetchAnalytics();
        }
    ```

6.  Dans la classe **DataFromAnalytics** , juste après la méthode **Start ()** , ajoutez la méthode suivante appelée **FetchAnalytics ()** . Cette méthode est chargée de remplir la liste des paires clé-valeur, avec un *gameobject* et un numéro d’événement d’espace réservé. Il initialise ensuite la Coroutine **GetWebRequest ()** . La structure de requête de l’appel à *application Insights* se trouve également dans cette méthode, comme point de terminaison de l’URL de la *requête* .

    ```csharp
        private void FetchAnalytics()
        {
            // Iterate through the objects in the list
            for (int i = 0; i < _listOfGameObjectsInScene.Count; i++)
            {
                // The current event number is not known, so set it to zero.
                int eventCount = 0;

                // Add new pair to list, as placeholder, until eventCount is known.
                _pairedObjectsWithEventCount.Add(new KeyValuePair<GameObject, int>(_listOfGameObjectsInScene[i], eventCount));

                // Set the renderer of the object to the default color, white
                _listOfGameObjectsInScene[i].GetComponent<Renderer>().material.color = Color.white;

                // Create the appropriate object name using Insights structure
                string objectName = _listOfGameObjectsInScene[i].name;
 
                // Build the queryUrl for this object.
                string queryUrl = Uri.EscapeUriString(string.Format(
                    "https://api.applicationinsights.io/v1/apps/{0}/events/$all?timespan=PT{1}H&$search={2}&$select=customMetric/name&$top={3}&$count=true",
                    ApplicationInsightsTracker.Instance.applicationId, _timepspanAsHours, "Gazed " + objectName, _quantityOfEventsQueried));


                // Send this object away within the WebRequest Coroutine, to determine it is event count.
                StartCoroutine("GetWebRequest", new KeyValuePair<string, int>(queryUrl, i));
            }
        }
    ```

7.  Juste en dessous de la méthode **FetchAnalytics ()** , ajoutez une méthode appelée **GetWebRequest ()** , qui retourne un *IEnumerator*. Cette méthode est chargée de demander le nombre de fois qu’un événement, correspondant à un *gameobject*spécifique, a été appelé dans *application Insights*. Lorsque toutes les requêtes envoyées ont été retournées, la méthode **DetermineWinner ()** est appelée.

    ```csharp
        /// <summary>
        /// Requests the data count for number of events, according to the
        /// input query URL.
        /// </summary>
        /// <param name="webQueryPair">Query URL and the list number count.</param>
        /// <returns></returns>
        private IEnumerator GetWebRequest(KeyValuePair<string, int> webQueryPair)
        {
            // Set the URL and count as their own variables (for readability).
            string url = webQueryPair.Key;
            int currentCount = webQueryPair.Value;

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Get(url))
            {
                DownloadHandlerBuffer handlerBuffer = new DownloadHandlerBuffer();

                unityWebRequest.downloadHandler = handlerBuffer;

                unityWebRequest.SetRequestHeader("host", "api.applicationinsights.io");

                unityWebRequest.SetRequestHeader("x-api-key", ApplicationInsightsTracker.Instance.API_Key);

                yield return unityWebRequest.SendWebRequest();

                if (unityWebRequest.isNetworkError)
                {
                    // Failure with web request.
                    Debug.Log("<color=red>Error Sending:</color> " + unityWebRequest.error);
                }
                else
                {
                    // This query has returned, so add to the current count.
                    _queriesReturned++;

                    // Initialize event count integer.
                    int eventCount = 0;

                    // Deserialize the response with the custom Analytics class.
                    Analytics welcome = JsonConvert.DeserializeObject<Analytics>(unityWebRequest.downloadHandler.text);

                    // Get and return the count for the Event
                    if (int.TryParse(welcome.OdataCount, out eventCount) == false)
                    {
                        // Parsing failed. Can sometimes mean that the Query URL was incorrect.
                        Debug.Log("<color=red>Failure to Parse Data Results. Check Query URL for issues.</color>");
                    }
                    else
                    {
                        // Overwrite the current pair, with its actual values, now that the event count is known.
                        _pairedObjectsWithEventCount[currentCount] = new KeyValuePair<GameObject, int>(_pairedObjectsWithEventCount[currentCount].Key, eventCount);
                    }

                    // If all queries (compared with the number which was sent away) have 
                    // returned, then run the determine winner method. 
                    if (_queriesReturned == _pairedObjectsWithEventCount.Count)
                    {
                        DetermineWinner();
                    }
                }
            }
        }
    ```

8.  La méthode suivante est **DetermineWinner ()** , qui trie la liste de paires *gameobject* et *int* , en fonction du nombre d’événements le plus élevé. Il modifie ensuite la couleur matérielle de ce *gameobject* en *vert* (en tant que commentaire pour qu’il ait le plus grand nombre). Un message s’affiche avec les résultats de l’analyse.

    ```csharp
        /// <summary>
        /// Call to determine the keyValue pair, within the objects list, 
        /// with the highest event count.
        /// </summary>
        private void DetermineWinner()
        {
            // Sort the values within the list of pairs.
            _pairedObjectsWithEventCount.Sort((x, y) => y.Value.CompareTo(x.Value));

            // Change its colour to green
            _pairedObjectsWithEventCount.First().Key.GetComponent<Renderer>().material.color = Color.green;

            // Provide the winner, and other results, within the console window. 
            string message = $"<b>Analytics Results:</b>\n " +
                $"<i>{_pairedObjectsWithEventCount.First().Key.name}</i> has the highest event count, " +
                $"with <i>{_pairedObjectsWithEventCount.First().Value.ToString()}</i>.\nFollowed by: ";

            for (int i = 1; i < _pairedObjectsWithEventCount.Count; i++)
            {
                message += $"{_pairedObjectsWithEventCount[i].Key.name}, " +
                    $"with {_pairedObjectsWithEventCount[i].Value.ToString()} events.\n";
            }

            Debug.Log(message);
        }
    ```

9.  Ajoutez la structure de classe qui sera utilisée pour désérialiser l’objet JSON, reçu de *application Insights*. Ajoutez ces classes au bas de votre fichier de classe **DataFromAnalytics** , **en dehors** de la définition de classe.

    ```csharp
        /// <summary>
        /// These classes represent the structure of the JSON response from Azure Insight
        /// </summary>
        [Serializable]
        public class Analytics
        {
            [JsonProperty("@odata.context")]
            public string OdataContext { get; set; }

            [JsonProperty("@odata.count")]
            public string OdataCount { get; set; }

            [JsonProperty("value")]
            public Value[] Value { get; set; }
        }

        [Serializable]
        public class Value
        {
            [JsonProperty("customMetric")]
            public CustomMetric CustomMetric { get; set; }
        }

        [Serializable]
        public class CustomMetric
        {
            [JsonProperty("name")]
            public string Name { get; set; }
        }
    ```

10. Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.

## <a name="chapter-10---create-the-movement-class"></a>Chapitre 10-créer la classe de mouvement

Le script de **déplacement** est le prochain script que vous devrez créer. Il est responsable des tâches suivantes :

- Déplacement de la caméra principale en fonction de la direction vers laquelle l’appareil photo regarde.
- Ajout de tous les autres scripts aux objets de scène.

Pour créer le script :

1.  Double-cliquez sur le dossier **scripts** pour l’ouvrir.

2.  Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** >  **C# script**. Nommez le **mouvement**du script.

3.  Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.

4.  Remplacez le code existant par ce qui suit :

    ```csharp
        using UnityEngine;
        using UnityEngine.XR.WSA.Input;

        public class Movement : MonoBehaviour
        {
            /// <summary>
            /// The rendered object representing the right controller.
            /// </summary>
            public GameObject Controller;

            /// <summary>
            /// The movement speed of the user.
            /// </summary>
            public float UserSpeed;

            /// <summary>
            /// Provides whether source updates have been registered.
            /// </summary>
            private bool _isAttached = false;

            /// <summary>
            /// The chosen controller hand to use. 
            /// </summary>
            private InteractionSourceHandedness _handness = InteractionSourceHandedness.Right;

            /// <summary>
            /// Used to calculate and proposes movement translation.
            /// </summary>
            private Vector3 _playerMovementTranslation;

            private void Start()
            {
                // You are now adding components dynamically 
                // to ensure they are existing on the correct object  

                // Add all camera related scripts to the camera. 
                Camera.main.gameObject.AddComponent<Gaze>();
                Camera.main.gameObject.AddComponent<ObjectTrigger>();
        
                // Add all other scripts to this object.
                gameObject.AddComponent<ApplicationInsightsTracker>();
                gameObject.AddComponent<DataFromAnalytics>();
            }

            // Update is called once per frame
            void Update()
            {
            
            }
        }
    ```

5.  Dans la classe de **déplacement** , *sous* la méthode empty **Update ()** , insérez les méthodes suivantes qui permettent à l’utilisateur d’utiliser le contrôleur de main pour se déplacer dans l’espace virtuel :

    ```csharp
        /// <summary>
        /// Used for tracking the current position and rotation of the controller.
        /// </summary>
        private void UpdateControllerState()
        {
    #if UNITY_WSA && UNITY_2017_2_OR_NEWER
            // Check for current connected controllers, only if WSA.
            string message = string.Empty;

            if (InteractionManager.GetCurrentReading().Length > 0)
            {
                foreach (var sourceState in InteractionManager.GetCurrentReading())
                {
                    if (sourceState.source.kind == InteractionSourceKind.Controller && sourceState.source.handedness == _handness)
                    {
                        // If a controller source is found, which matches the selected handness, 
                        // check whether interaction source updated events have been registered. 
                        if (_isAttached == false)
                        {
                            // Register events, as not yet registered.
                            message = "<color=green>Source Found: Registering Controller Source Events</color>";
                            _isAttached = true;

                            InteractionManager.InteractionSourceUpdated += InteractionManager_InteractionSourceUpdated;
                        }

                        // Update the position and rotation information for the controller.
                        Vector3 newPosition;
                        if (sourceState.sourcePose.TryGetPosition(out newPosition, InteractionSourceNode.Pointer) && ValidPosition(newPosition))
                        {
                            Controller.transform.localPosition = newPosition;
                        }

                        Quaternion newRotation;

                        if (sourceState.sourcePose.TryGetRotation(out newRotation, InteractionSourceNode.Pointer) && ValidRotation(newRotation))
                        {
                            Controller.transform.localRotation = newRotation;
                        }
                    }
                }
            }
            else
            {
                // Controller source not detected. 
                message = "<color=blue>Trying to detect controller source</color>";

                if (_isAttached == true)
                {
                    // A source was previously connected, however, has been lost. Disconnected
                    // all registered events. 

                    _isAttached = false;

                    InteractionManager.InteractionSourceUpdated -= InteractionManager_InteractionSourceUpdated;

                    message = "<color=red>Source Lost: Detaching Controller Source Events</color>";
                }
            }

            if(message != string.Empty)
            {
                Debug.Log(message);
            }
    #endif
        }
    ```

    ```csharp
        /// <summary>
        /// This registered event is triggered when a source state has been updated.
        /// </summary>
        /// <param name="obj"></param>
        private void InteractionManager_InteractionSourceUpdated(InteractionSourceUpdatedEventArgs obj)
        {
            if (obj.state.source.handedness == _handness)
            {
                if(obj.state.thumbstickPosition.magnitude > 0.2f)
                {
                    float thumbstickY = obj.state.thumbstickPosition.y;

                    // Vertical Input.
                    if (thumbstickY > 0.3f || thumbstickY < -0.3f)
                    {
                        _playerMovementTranslation = Camera.main.transform.forward;
                        _playerMovementTranslation.y = 0;
                        transform.Translate(_playerMovementTranslation * UserSpeed * Time.deltaTime * thumbstickY, Space.World);
                    }
                }
            }
        }
    ```

    ```csharp
        /// <summary>
        /// Check that controller position is valid. 
        /// </summary>
        /// <param name="inputVector3">The Vector3 to check</param>
        /// <returns>The position is valid</returns>
        private bool ValidPosition(Vector3 inputVector3)
        {
            return !float.IsNaN(inputVector3.x) && !float.IsNaN(inputVector3.y) && !float.IsNaN(inputVector3.z) && !float.IsInfinity(inputVector3.x) && !float.IsInfinity(inputVector3.y) && !float.IsInfinity(inputVector3.z);
        }

        /// <summary>
        /// Check that controller rotation is valid. 
        /// </summary>
        /// <param name="inputQuaternion">The Quaternion to check</param>
        /// <returns>The rotation is valid</returns>
        private bool ValidRotation(Quaternion inputQuaternion)
        {
            return !float.IsNaN(inputQuaternion.x) && !float.IsNaN(inputQuaternion.y) && !float.IsNaN(inputQuaternion.z) && !float.IsNaN(inputQuaternion.w) && !float.IsInfinity(inputQuaternion.x) && !float.IsInfinity(inputQuaternion.y) && !float.IsInfinity(inputQuaternion.z) && !float.IsInfinity(inputQuaternion.w);
        }   
    ```

6.  Enfin, ajoutez l’appel de méthode dans la méthode **Update ()** .

    ```csharp
        // Update is called once per frame
        void Update()
        {
            UpdateControllerState();
        }
    ```

7.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à *Unity*.

## <a name="chapter-11---setting-up-the-scripts-references"></a>Chapitre 11-configuration des références de scripts

Dans ce chapitre, vous devez placer le script de **déplacement** sur le parent de l' **appareil photo** et définir ses cibles de référence. Ce script gère alors le placement des autres scripts là où ils doivent être.

1.  Dans le dossier **scripts** du *panneau Projet*, faites glisser le script de **déplacement** vers l’objet parent de l' **appareil photo** , situé dans le *panneau hiérarchie*.

    ![Configuration des références de scripts dans la scène Unity](images/AzureLabs-Lab309-48.png)

2.  Cliquez sur le **parent de l’appareil photo**. Dans le *volet hiérarchie*, faites glisser l’objet de **droite** du *volet* de la hiérarchie vers la cible de référence, **contrôleur**, dans le *panneau Inspecteur*. Définissez la **Vitesse** de l’utilisateur sur **5**, comme indiqué dans l’image ci-dessous.

    ![Configuration des références de scripts dans la scène Unity](images/AzureLabs-Lab309-49.png)

## <a name="chapter-12---build-the-unity-project"></a>Chapitre 12-générer le projet Unity

Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.

1.  Accédez à **paramètres de build**, (**fichier** > **paramètres de build**).

2.  Dans la fenêtre **paramètres de build** , cliquez sur **générer**.

    ![Générer le projet Unity dans la solution UWP](images/AzureLabs-Lab309-50.png)

3.  Une fenêtre de l' **Explorateur de fichiers** s’affiche et vous invite à entrer un emplacement pour la Build. Créez un nouveau dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche), puis nommez-le **Builds**.

    ![Générer le projet Unity dans la solution UWP](images/AzureLabs-Lab309-51.png)

    1.  Ouvrez le nouveau dossier **Builds** , puis créez un autre dossier (à l’aide d’un **nouveau dossier** ) et nommez-le **rm\_application Azure\_\_Insights**.

        ![Générer le projet Unity dans la solution UWP](images/AzureLabs-Lab309-52.png)

    2.  Avec l' **application rm\_Azure\_\_dossier Insights** sélectionné, cliquez sur **Sélectionner un dossier**. La génération du projet prendra quelques minutes.

4.  Après la *génération*, l' **Explorateur de fichiers** s’affiche et vous indique l’emplacement de votre nouveau projet.

## <a name="chapter-13---deploy-mr_azure_application_insights-app-to-your-machine"></a>Chapitre 13-déployer MR_Azure_Application_Insights application sur votre ordinateur

Pour déployer l' **application\_Azure\_\_Insights** sur votre ordinateur local :

1.  Ouvrez le fichier solution de votre **application rm\_Azure\_application\_Insights** dans **Visual Studio**.

2.  Dans la **plateforme**de la solution, sélectionnez **x86, ordinateur local**.

3.  Dans la **configuration** de la solution, sélectionnez **Déboguer**.

    ![Générer le projet Unity dans la solution UWP](images/AzureLabs-Lab309-53.png)

4.  Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre ordinateur.

5.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.

6. Lancez l’application de réalité mixte.

7. Déplacez-vous dans la scène, en approchant les objets et en examinant ces derniers, lorsque le *service Azure Insight* a collecté suffisamment de données d’événement, il définit l’objet qui a été le plus proche du vert.

> [!IMPORTANT] 
> Alors que le temps d’attente moyen pour les *événements et les métriques* à collecter par le service prend environ 15 minutes, dans certains cas, cela peut prendre jusqu’à 1 heure.

## <a name="chapter-14---the-application-insights-service-portal"></a>Chapitre 14-Application Insights Service Portal

Une fois que vous avez accédé à la scène et que vous avez placé un regard sur plusieurs objets, vous pouvez voir les données collectées dans le portail de *Service application Insights* .

1.  Revenez à votre portail de service Application Insights.

2.  Cliquez sur *Metrics Explorer*.

    ![Examen des données collectées](images/AzureLabs-Lab309-54.png)

3.  Elle s’ouvre dans un onglet contenant le graphique qui représente les *événements et les métriques* associés à votre application. Comme indiqué ci-dessus, l’affichage des données dans le graphique peut prendre un certain temps (jusqu’à 1 heure).

    ![Examen des données collectées](images/AzureLabs-Lab309-55.png)

4.  Cliquez sur la *barre des événements* dans le *total des événements* par version de l’application pour afficher une répartition détaillée des événements avec leurs noms.

    ![Examen des données collectées](images/AzureLabs-Lab309-56.png)

## <a name="your-finished-your-application-insights-service-application"></a>Votre application de service Application Insights est terminée

Félicitations, vous avez créé une application de réalité mixte qui tire parti du service Application Insights pour surveiller l’activité de l’utilisateur au sein de votre application.

![résultat du cours](images/AzureLabs-Lab309-00.png)

## <a name="bonus-exercises"></a>Exercices bonus

**Exercice 1**

Essayez de créer dynamiquement, plutôt que de créer manuellement les objets ObjectInScene et de définir leurs coordonnées sur le plan au sein de vos scripts. De cette façon, vous pouvez demander à Azure ce que l’objet le plus populaire était (des résultats de proximité ou de proximité) et générer un *supplément* à l’un de ces objets.

**Exercice 2**

Triez vos résultats Application Insights par heure, afin d’obtenir les données les plus pertinentes, et d’implémenter ces données sensibles au temps dans votre application.

