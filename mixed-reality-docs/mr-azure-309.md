---
title: MR et Azure 309 - Application insights
description: Terminer ce cours pour apprendre à collecter analytique concernant le comportement des utilisateurs au sein d’une application de réalité mixte, à l’aide du Service Azure Application Insights.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, insights d’application, hololens, immersives, vr
ms.openlocfilehash: 838dbe38724d29f4c5987e2f6ac7a07231015c82
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596993"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br> 

# <a name="mr-and-azure-309-application-insights"></a>MR et Azure 309 : Insights d’application

![produit final-Démarrer](images/AzureLabs-Lab309-00.png)

Dans ce cours, vous allez apprendre à ajouter des fonctionnalités d’Application Insights à une application de réalité mixte, à l’aide de l’API Azure Application Insights pour collecter analytique concernant le comportement de l’utilisateur.

Application Insights est un service Microsoft, permettant aux développeurs de collecter analytique à partir de leurs applications et de gérer à partir d’un portail facile à utiliser. L’analytique peut être des performances pour les informations personnalisées que vous souhaitez collecter. Pour plus d’informations, visitez le [page Application Insights](https://azure.microsoft.com/services/application-insights/).

Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :

1.  Autoriser l’utilisateur à l’utilisation et vous déplacer dans une scène.
2.  Déclencher l’envoi d’analytique pour le *Service Application Insights*, via l’utilisation du pointage de regard et proximité avec les objets de contexte.
3.  L’application appellera également sur le Service, l’extraction d’informations sur l’objet a été a élaboré le meilleur par l’utilisateur, dans les dernières 24 heures. Cet objet sera modifier sa couleur verte.

Ce cours va vous apprendre à obtenir les résultats à partir du Service Application Insights, dans une application basée sur Unity. Il le sera jusqu'à vous permettent d’appliquer ces concepts à une application personnalisée, que vous voudrez peut-être générer.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 309 : Insights d’application</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

> [!NOTE]
> Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens. Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens. Lorsque vous utilisez HoloLens, vous pouvez remarquer quelques echo durant la capture de la voix.

## <a name="prerequisites"></a>Prérequis

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.

Nous recommandons le matériel et logiciel pour ce cours suivants :

- Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)
- [Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé](install-the-tools.md#installation-checklist)
- [Le SDK Windows 10 dernières](install-the-tools.md#installation-checklist)
- [Unity 2017.4](install-the-tools.md#installation-checklist)
- [Visual Studio 2017](install-the-tools.md#installation-checklist)
- Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé
- Un ensemble de casque avec un microphone intégré (si le casque n’a pas un mic intégré et les haut-parleurs)
- Accès à Internet pour le programme d’installation Azure et l’extraction de données Application Insights

## <a name="before-you-start"></a>Avant de commencer

Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).

> [!WARNING] 
> Gardez à l’esprit, données transférées vers *Application Insights* prend du temps, par conséquent, soyez patient. Si vous souhaitez vérifier si le Service a reçu vos données, consultez [chapitre 14](#chapter-14---the-application-insights-service-portal), qui illustrent comment naviguer dans le portail.

## <a name="chapter-1---the-azure-portal"></a>Chapitre 1 : le portail Azure

Pour utiliser *Application Insights*, vous devez créer et configurer un *Service Application Insights* dans le portail Azure.

1.  Connectez-vous à la [Azure Portal](https://portal.azure.com).

    > [!NOTE]
    > Si vous n’avez pas déjà un compte Azure, vous devrez créer un. Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.

2.  Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez *Application Insights*, puis cliquez sur **entrée**.

    > [!NOTE]
    > Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.

    ![Portail Azure](images/AzureLabs-Lab309-01.png)

3.  La nouvelle page à droite fournit une description de la *Azure Application Insights* Service. En bas à gauche de cette page, sélectionnez le **créer** bouton, pour créer une association avec ce Service.

    ![Portail Azure](images/AzureLabs-Lab309-02.png)

4.  Une fois que vous avez cliqué sur **créer**:

    1.  Insérez votre souhaitée **nom** pour cette instance de Service.

    2.  En tant que **Type d’Application**, sélectionnez **général**.

    3.  Sélectionnez un **abonnement**.

    4.  Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5.  Sélectionnez un **emplacement**.

    6.  Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.

    7.  Sélectionnez **Créer**.

        ![Portail Azure](images/AzureLabs-Lab309-03.png)

5.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.

6.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![Portail Azure](images/AzureLabs-Lab309-04.png)

7.  Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.

    ![Portail Azure](images/AzureLabs-Lab309-05.png)

8.  Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. Vous serez dirigé vers votre nouvelle *Service Application Insights* instance.

    ![Portail Azure](images/AzureLabs-Lab309-06.png)

    > [!NOTE]
    >  Ne fermez pas cette page web et faciles d’accès, vous serez revenez ici régulièrement pour voir les données collectées.

    > [!IMPORTANT]
    > Pour implémenter l’Application Insights, vous devez utiliser des valeurs spécifiques trois (3) : **Clé d’instrumentation**, **ID d’Application**, et **clé API**. Ci-dessous, vous verrez comment récupérer ces valeurs à partir de votre Service. Veillez à noter ces valeurs sur une valeur vide *le bloc-notes* page, car vous les utiliserez bientôt dans votre code.

9.  Pour rechercher le **clé d’Instrumentation**, vous devez faire défiler vers le bas la liste des fonctions de Service, puis cliquez sur **propriétés**, révèle l’onglet affiché le **clé du Service**.

    ![Portail Azure](images/AzureLabs-Lab309-07.png)

10. Un peu ci-dessous **propriétés**, vous trouverez **accès à l’API**, dont vous avez besoin de cliquer sur. Le volet à droite fournira la **ID d’Application** de votre application.

    ![Portail Azure](images/AzureLabs-Lab309-08.png)

11. Avec le **ID d’Application** panneau toujours ouverte, cliquez sur **créer une clé API**, qui ouvre le *créer une clé API* Panneau de configuration.

    ![Portail Azure](images/AzureLabs-Lab309-09.png)

12. Au sein de l’ouvrir maintenant *créer une clé API* panneau, tapez une description, et **Cochez les trois zones**.

13. Cliquez sur **générer la clé**. Votre **clé API** sera créé et affiché. 

    ![Portail Azure](images/AzureLabs-Lab309-10.png)
        
    > [!WARNING]
    > C’est la seule fois votre **clé Service** s’affiche, assurez-vous donc vous faire une copie de celle-ci maintenant.

## <a name="chapter-2---set-up-the-unity-project"></a>Chapitre 2 : configurer le projet Unity

Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.

1.  Ouvrez *Unity* et cliquez sur **New**.

    ![Configurer le projet Unity](images/AzureLabs-Lab309-11.png)

2.  Vous devez maintenant fournir un nom de projet Unity, insérer **MR\_Azure\_Application\_Insights**. Assurez-vous que le *modèle* a la valeur **3D**. Définir le *emplacement* à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable). Ensuite, cliquez sur **créer un projet**.

    ![Configurer le projet Unity](images/AzureLabs-Lab309-12.png)

3.  Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**. Accédez à **modifier \> préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**. Modification **éditeur de Script externe** à **Visual Studio 2017**. Fermer le **préférences** fenêtre.

    ![Configurer le projet Unity](images/AzureLabs-Lab309-13.png)

4.  Ensuite, accédez à **fichier \> paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **plateforme basculer** bouton.

    ![Configurer le projet Unity](images/AzureLabs-Lab309-14.png)

5.  Accédez à **fichier \> paramètres de Build** et vous assurer que :

    1.  **Équipement cible** a la valeur **n’importe quel appareil**

        > Pour le Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.

    2.  **Type de build** a la valeur **D3D**

    3.  **Kit de développement logiciel** a la valeur **dernière installé**

    4.  **Générez et exécutez** est défini sur **ordinateur Local**

    5.  Enregistrer la scène et l’ajouter à la build.

        1.  Cela en sélectionnant **ajouter un arrière-plan Open**. Une fenêtre d’enregistrement s’affiche.

            ![Configurer le projet Unity](images/AzureLabs-Lab309-15.png)

        2. Créez un dossier pour cela et toutes les scènes future, puis cliquez sur le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.

            ![Configurer le projet Unity](images/AzureLabs-Lab309-16.png)

        3. Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier :* champ de texte, tapez **ApplicationInsightsScene**, puis cliquez sur **enregistrer**.

            ![Configurer le projet Unity](images/AzureLabs-Lab309-17.png)

6.  Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.

7.  Dans le **paramètres de Build** fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le **inspecteur** se trouve.

    ![Configurer le projet Unity](images/AzureLabs-Lab309-18.png)

8. Dans ce panneau, quelques paramètres doivent être vérifiées :

    1.  Dans le **autres paramètres** onglet :

        1.  **Écriture de scripts** **Version du Runtime** doit être **expérimental (équivalent .NET 4.6)**, ce qui déclenchera une nécessité de redémarrer l’éditeur.

        2.  **Script principal** doit être **.NET**

        3.  **Niveau de compatibilité d’API** doit être **.NET 4.6**

        ![Configurer le projet Unity](images/AzureLabs-Lab309-19.png)

    2.  Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :

        - **InternetClient**     

            ![Configurer le projet Unity](images/AzureLabs-Lab309-20.png)

    3.  Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **Windows Mixed Reality Kit de développement logiciel** est ajouté.

        ![Configurer le projet Unity](images/AzureLabs-Lab309-21.png)

9.  Dans **paramètres de Build**, **Unity C\# projets** est n’est plus grisée ; Cochez la case à cocher en regard de cela.

10.  Fermez la fenêtre Paramètres de Build.

11.  Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).


## <a name="chapter-3---import-the-unity-package"></a>Chapitre 3 - importer le package Unity

> [!IMPORTANT]
> Si vous souhaitez ignorer le *Unity configurer* les composants de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [Azure-MR-309.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/Azure-MR-309.unitypackage), importez-le dans votre projet en tant qu’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html). Il contient également les DLL dans le chapitre suivant. Après l’importation, continuer à partir de [ **chapitre 6**](#chapter-6---create-the-applicationinsightstracker-class).

> [!IMPORTANT]
> Pour utiliser Application Insights dans Unity, vous devez importer la DLL, ainsi que la DLL Newtonsoft. Il est actuellement un problème connu dans Unity qui nécessite des plug-ins à être reconfiguré après l’importation. Ces étapes (4-7 de cette section) ne sera plus nécessaires une fois que le bogue a été résolu.

Pour importer l’Application Insights dans votre propre projet, assurez-vous que vous avez [téléchargé '.unitypackage', qui contient les plug-ins](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20309%20-%20Application%20insights/AppInsights_LabPlugins.unitypackage). Ensuite, procédez comme suit :

1.  Ajouter le **.unitypackage** à Unity à l’aide de la **actifs \> importer un Package \> Package personnalisé** option de menu.

2.  Dans le **importer un Package Unity** emballer qui apparaît, vérifiez tous les éléments sous (y compris) **plug-ins** est sélectionné.

    ![Importer le package Unity](images/AzureLabs-Lab309-22.png)

3.  Cliquez sur le **importation** bouton permettant d’ajouter les éléments à votre projet.

4.  Accédez à la **Insights** dossier sous **plug-ins** dans le projet afficher, puis sélectionnez les plug-ins suivants *uniquement*:

    -   Microsoft.ApplicationInsights

    ![Importer le package Unity](images/AzureLabs-Lab309-23.png)

5.  Avec cette *plug-in* sélectionnée, vérifiez que **plateforme Any** est **unchecked**, puis assurez-vous que **WSAPlayer** est également  **unchecked**, puis cliquez sur **appliquer**. Cette opération est juste pour confirmer que les fichiers sont correctement configurés.

    ![Importer le package Unity](images/AzureLabs-Lab309-24.png)

    > [!NOTE]
    > Marquer les plug-ins comme suit, les configure uniquement à être utilisé dans l’éditeur Unity. Il existe un autre ensemble de DLL dans le dossier WSA qui sera utilisée une fois que le projet est exporté à partir d’Unity.

6.  Ensuite, vous devez ouvrir le **WSA** dossier, en respectant le **Insights** dossier. Vous verrez une copie du même fichier que vous venez de configurer. Sélectionnez ce fichier et dans l’inspecteur, vérifiez que **plateforme Any** est **unchecked**, puis assurez-vous que **uniquement** **WSAPlayer** est **vérifiée**. Cliquez sur **Appliquer**.

    ![Importer le package Unity](images/AzureLabs-Lab309-25.png)

7. Vous devrez désormais suivre **les étapes 4 à 6**, mais pour le *Newtonsoft* plug-ins à la place. Consultez la capture d’écran de ce que le résultat doit se présenter comme ci-dessous.

    ![Importer le package Unity](images/AzureLabs-Lab309-25-5.png)    

## <a name="chapter-4---set-up-the-camera-and-user-controls"></a>Chapitre 4 - configurer des contrôles de l’appareil photo et l’utilisateur

Dans ce chapitre, vous allez définir des contrôles et de l’appareil photo pour autoriser l’utilisateur de voir et déplacer dans la scène.

1.  Avec le bouton droit dans une zone vide dans le volet de la hiérarchie, puis sur **créer > vide**.

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-26.png)

2.  Renommez le nouveau GameObject vide à **Parent de l’appareil photo**.

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-27.png)

3.  Avec le bouton droit dans une zone vide dans le volet de la hiérarchie, puis sur **objet 3D**, puis sur **sphère**.

4.  Renommer la sphère à **droite**.

5.  Définir le **transformer échelle** de la main droite pour **0.1, 0.1, 0.1**

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-28.png)

6.  Supprimer le **sphère Collider** composant à partir de la droite en cliquant sur le **ENGRENAGE** dans le *sphère Collider* composant, puis **supprimer un composant** .

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-29.png)

7.  Dans l’opération de glisser du Panneau de la hiérarchie le **Main Camera** et **droite** objets sur le **Parent de l’appareil photo** objet.

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-30.png)

8.  Définir le **Position transformer** des deux le **Main Camera** et le **droite** objet **0, 0, 0**.

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-31.png)

    ![Configurer l’appareil photo et les contrôles utilisateur](images/AzureLabs-Lab309-32.png)

## <a name="chapter-5---set-up-the-objects-in-the-unity-scene"></a>Chapitre 5 - configurer les objets dans la scène Unity

Vous allez maintenant créer certaines formes de base pour votre scène, avec lesquels l’utilisateur peut interagir.

1.  Avec le bouton droit dans une zone vide dans le *hiérarchie panneau*, puis sur **objet 3D**, puis sélectionnez **plan**.

2.  Définir le plan de **transformer Position** à **0, -1, 0**.

3.  Définir le plan de **transformer échelle** à **5, 1, 5**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-33.png)

4.  Créer un matériau de base à utiliser avec votre **plan** de l’objet, afin que les autres formes sont plus faciles à voir. Accédez à votre *panneau projet*, avec le bouton droit, puis **créer**, suivie **dossier**, pour créer un nouveau dossier. Nommez-le **matériaux**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-34.png) ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-35.png)

5.  Ouvrez le **matériaux** dossier, puis avec le bouton droit, cliquez **créer**, puis **matériau**, pour créer un nouveau matériau. Nommez-le **bleu**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-36.png) ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-37.png)

6.  Avec la nouvelle **bleu** matériel sélectionné, recherchez à le *inspecteur*, puis cliquez sur la fenêtre rectangulaire en même temps que **Albedo**. Sélectionnez une couleur bleu (l’une image ci-dessous est **couleur hexadécimale : \#3592FFFF**). Une fois que vous avez choisi, cliquez sur le bouton Fermer.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-38.png)

7.  Faites glisser votre nouveau matériel à partir de la **matériaux** dossier, sur votre nouvellement créé **plan**, au sein de votre scène (ou déposez-le sur le **plan** au sein de l’objet le  *Hiérarchie*).

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-39.png)

8.  Avec le bouton droit dans une zone vide dans le *hiérarchie panneau*, puis sur **objet 3D, Capsule**.

    -  Avec le **Capsule** sélectionné, affectez son **transformer** *Position* à : **-10, 1, 0**.

9.  Avec le bouton droit dans une zone vide dans le *hiérarchie panneau*, puis sur **objet 3D, Cube**.

    -  Avec le **Cube** sélectionné, affectez son **transformer** *Position* à : **0, 0, 10**.

10. Avec le bouton droit dans une zone vide dans le *hiérarchie panneau*, puis sur **objet 3D, de la sphère**.

    -  Avec le **sphère** sélectionné, affectez son **transformer** *Position* à : **10, 0, 0**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-40.png)

    > [!NOTE]
    > Ces *Position* sont des valeurs *suggestions*. Vous êtes libre de définir les positions des objets à ce que vous souhaitez que, bien qu’il soit plus facile pour l’utilisateur de l’application si les distances des objets ne sont pas trop loin de l’appareil photo.

11. Lorsque votre application s’exécute, il doit être en mesure d’identifier les objets au sein de la scène, pour y parvenir, elles doivent être marqués. Sélectionnez un des objets et dans le *inspecteur* du panneau, cliquez sur **ajouter une balise...** , qui vous remplacerez la *inspecteur* avec la **balises & couches** Panneau de configuration.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-41.png) ![](images/AzureLabs-Lab309-42.png)

12. Cliquez sur le **+ (plus)** de symboles, puis tapez le nom de balise en tant que **ObjectInScene**.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-43.png)

    > [!WARNING]
    > Si vous utilisez un autre nom pour votre étiquette, vous devez vous assurer que cette modification est également effectuée le *DataFromAnalytics*, *ObjectTrigger*, et *les regards*, scripts plus tard, afin que votre les objets sont trouvés et détectés, au sein de votre scène.

13. Avec la balise est créée, il vous faut maintenant s’appliquent aux trois de vos objets. À partir de la *hiérarchie*, maintenez la **MAJ** de clé, puis cliquez sur le **Capsule**, **Cube**, et **sphère**, objets, puis, dans le *inspecteur*, cliquez sur le menu déroulant en même temps que **balise**, puis cliquez sur le *ObjectInScene* balise que vous avez créé.

    ![Configurer les objets dans la scène Unity](images/AzureLabs-Lab309-44.png) ![](images/AzureLabs-Lab309-45.png)

## <a name="chapter-6---create-the-applicationinsightstracker-class"></a>Chapitre 6 : créer la classe ApplicationInsightsTracker

Le premier script que vous créez est **ApplicationInsightsTracker**, qui est chargé de :

1.  Création d’événements en fonction des interactions de l’utilisateur à envoyer à Azure Application Insights.

2. Création des noms d’événements appropriés, en fonction de l’interaction de l’utilisateur.

3. Envoi des événements à l’instance de Service Application Insights.

Pour créer cette classe :

1.  Avec le bouton droit dans le *Panneau de configuration de projet*, puis **créer > dossier**. Nommez le dossier **Scripts**.

    ![Créer la classe ApplicationInsightsTracker](images/AzureLabs-Lab309-46.png)  ![Créer la classe ApplicationInsightsTracker](images/AzureLabs-Lab309-47.png)

2.  Avec le **Scripts** dossier créé, double-cliquez dessus pour ouvrir. Ensuite, dans ce dossier, avec le bouton droit, **créer > C\# Script**. Nommez le script **ApplicationInsightsTracker**.

3.  Double-cliquez sur le nouveau **ApplicationInsightsTracker** script pour l’ouvrir avec **Visual Studio**.

4.  Mettre à jour les espaces de noms en haut du script afin d’être comme suit :

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
    > Définir le **instrumentationKey, applicationId et API_Key** des valeurs de manière appropriée, en utilisant le *Service clés* à partir du portail Azure, comme indiqué dans [chapitre 1](#chapter-1---the-azure-portal), étape 9 et versions ultérieures.

6.  Ajoutez ensuite le **Start()** et **Awake()** méthodes, qui seront appelées lors de l’initialisation de la classe :

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

7.  Ajoutez les méthodes chargés d’envoyer les événements et les métriques inscrit par votre application :

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

8.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-7---create-the-gaze-script"></a>Chapitre 7 - créer le script du pointage de regard

Le script suivant pour créer le **les regards** script. Ce script est chargé de créer un *Raycast* qui est projeté vers l’avant à partir de la *Main Camera*, pour détecter quel objet consulte l’utilisateur. Dans ce cas, le *Raycast* devra identifier si l’utilisateur consulte un objet avec le **ObjectInScene** balise, puis compter combien de temps l’utilisateur *son* à cet objet.

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.

2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer** > **C\# Script**. Nommez le script **les regards**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Remplacez le code existant par le code suivant :

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

5.  Code pour le **Awake()** et **Start()** méthodes doit maintenant être ajouté.

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

6.  À l’intérieur de la **les regards** de classe, ajoutez le code suivant dans le **Update()** méthode au projet un *Raycast* et détecter la baisse de la cible :

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

7.  Ajouter le **ResetFocusedObject()** (méthode), pour envoyer des données à **Application Insights** lorsque l’utilisateur a examiné un objet.

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

8.  Vous avez maintenant terminé la **les regards** script. Enregistrez vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-8---create-the-objecttrigger-class"></a>Chapitre 8 - créer la classe ObjectTrigger

Le script suivant, vous devez créer est **ObjectTrigger**, qui est chargé de :

- Ajout de composants nécessaires de collision à la caméra principale.
- Détecter si l’appareil photo est près d’un objet marqué comme **ObjectInScene**.

Pour créer le script :

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.

2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer** **C\# > Script**. Nommez le script **ObjectTrigger**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio. Remplacez le code existant par le code suivant :

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

4.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-9---create-the-datafromanalytics-class"></a>Chapitre 9 - créer la classe DataFromAnalytics

Vous devez maintenant créer le **DataFromAnalytics** script, qui est chargé de :

- Extraction des données d’analytique sur les objets a été approché par l’appareil photo le plus.
- À l’aide de la *clés du Service*, qui autorise la communication avec votre instance de Service Azure Application Insights.
- Trier les objets dans la scène, selon ce qui a le nombre d’événements le plus élevé.
- Modification de la couleur du matériau, de l’objet plus approached, à *vert*.

Pour créer le script :

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.

2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer** **C\# > Script**. Nommez le script **DataFromAnalytics**.

3.  Double-cliquez sur le script pour l’ouvrir avec Visual Studio.

4.  Insérer des espaces de noms suivants :

    ```csharp
        using Newtonsoft.Json;
        using System;
        using System.Collections;
        using System.Collections.Generic;
        using System.Linq;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  Dans le script, insérez les éléments suivants :

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

6.  Dans le **DataFromAnalytics** class, juste après le **Start()** (méthode), ajoutez la méthode suivante nommée **FetchAnalytics()**. Cette méthode est chargée de remplir la liste des paires clé / valeur, avec un *GameObject* et un numéro de nombre d’événement espace réservé. Il initialise ensuite les **GetWebRequest()** coroutine. La structure de la requête de l’appel à *Application Insights* peut se trouver dans cette méthode, comme le *URL de la requête* point de terminaison.

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

7.  Juste en dessous du **FetchAnalytics()** (méthode), ajoutez une méthode appelée **GetWebRequest()**, qui retourne un *IEnumerator*. Cette méthode est chargée pour demander le nombre de fois où un événement, correspondant avec un spécifique *GameObject*, a été appelée au sein de *Application Insights*. Lorsque toutes les requêtes envoyées ont été retournés, le **DetermineWinner()** méthode est appelée.

    ```csharp
        /// <summary>
        /// Requests the data count for number of events, according to the
        /// input query URL.
        /// </summary>
        /// <param name="webQueryPair">Query URL and the list number count.</param>
        /// <returns></returns>
        private IEnumerator GetWebRequest(KeyValuePair<string, int> webQueryPair)
        {
            // Set the URL and count as their own variables (for readibility).
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

8.  La méthode suivante est **DetermineWinner()**, qui trie la liste des *GameObject* et *Int* paires, selon le nombre d’événements le plus élevé. Il remplace ensuite la couleur du matériau de qui *GameObject* à *vert* (en tant que commentaires pour lui avoir le nombre le plus élevé). Cela affiche un message avec les résultats d’analytique.

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

9.  Ajouter la structure de classe qui sera utilisée pour désérialiser l’objet JSON, reçu de *Application Insights*. Ajoutez ces classes tout en bas de votre **DataFromAnalytics** fichier de classe, **en dehors de** de la définition de classe.

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

10. Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-10---create-the-movement-class"></a>Chapitre 10 - créer la classe de mouvement

Le **mouvement** script est le prochain script, vous devez créer. Il est chargé de :

- Déplacement de la caméra principale en fonction de la direction de l’appareil photo recherche vers.
- Ajout de tous les autres scripts aux objets de scène.

Pour créer le script :

1.  Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.

2.  Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer** > **C\# Script**. Nommez le script **mouvement**.

3.  Double-cliquez sur le script pour l’ouvrir avec *Visual Studio*.

4.  Remplacez le code existant par le code suivant :

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

5.  Dans le **mouvement** (classe), *ci-dessous* vide **Update()** (méthode), insérer les méthodes suivantes permettant aux utilisateurs d’utiliser le contrôleur de main pour déplacer dans l’espace virtuel :

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

6.  Ajoutez enfin l’appel de méthode dans le **Update()** (méthode).

    ```csharp
        // Update is called once per frame
        void Update()
        {
            UpdateControllerState();
        }
    ```

7.  Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.

## <a name="chapter-11---setting-up-the-scripts-references"></a>Chapitre 11 - configurer les références de scripts

Dans ce chapitre, vous devez placer le **mouvement** de script sur le **Parent de l’appareil photo** et définissez ses cibles de référence. Ce script gère à placer les autres scripts où ils doivent être.

1.  À partir de la **Scripts** dossier dans le *panneau projet*, faites glisser le **le déplacement des** un script pour le **Parent de l’appareil photo** objet, se trouvant dans le  *Panneau de la hiérarchie*.

    ![Configurer les références de scripts dans la scène Unity](images/AzureLabs-Lab309-48.png)

2.  Cliquez sur le **Parent de l’appareil photo**. Dans le *hiérarchie panneau*, faites glisser le **droite** à partir de l’objet le *Panneau de la hiérarchie* à la cible de référence, **contrôleur**, dans le *Panneau Inspecteur*. Définir le **utilisateur vitesse** à **5**, comme illustré dans l’image ci-dessous.

    ![Configurer les références de scripts dans la scène Unity](images/AzureLabs-Lab309-49.png)

## <a name="chapter-12---build-the-unity-project"></a>Chapitre 12 - générer le projet Unity

Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.

1.  Accédez à **les paramètres de génération**, **(fichier > Paramètres de Build...)** .

2.  À partir de la **paramètres de Build** fenêtre, cliquez sur **Build**.

    ![Générez le projet Unity à UWP Solution](images/AzureLabs-Lab309-50.png)

3.  Un **Explorateur de fichiers** fenêtre va fenêtre contextuelle s’affiche, vous demandant de spécifier un emplacement pour la build. Créez un dossier (en cliquant sur **nouveau dossier** dans l’angle supérieur gauche) et nommez-le **génère**.

    ![Générez le projet Unity à UWP Solution](images/AzureLabs-Lab309-51.png)

    1.  Ouvrez le nouveau **génère** dossier et créez un autre dossier (à l’aide de **nouveau dossier** une fois de plus) et nommez-le **MR\_Azure\_Application\_ Insights**.

        ![Générez le projet Unity à UWP Solution](images/AzureLabs-Lab309-52.png)

    2.  Avec le **MR\_Azure\_Application\_Insights** dossier sélectionné, cliquez sur **sélectionner le dossier**. Le projet prendra une minute ou donc en créer.

4.  Suivant *Build*, **Explorateur de fichiers** s’affiche vous indiquant l’emplacement de votre nouveau projet.

## <a name="chapter-13---deploy-mrazureapplicationinsights-app-to-your-machine"></a>Chapitre 13 - déployer l’application de MR_Azure_Application_Insights sur votre ordinateur

Pour déployer le **MR\_Azure\_Application\_Insights** application sur votre ordinateur Local :

1.  Ouvrez le fichier de solution de votre **MR\_Azure\_Application\_Insights** app dans **Visual Studio**.

2.  Dans le **plateforme de Solution**, sélectionnez **x86, Local Machine**.

3.  Dans le **Configuration de la Solution** sélectionnez **déboguer**.

    ![Générez le projet Unity à UWP Solution](images/AzureLabs-Lab309-53.png)

4.  Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application sur votre ordinateur.

5.  Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.

6. Lancez l’application de réalité mixte.

7. Déplacer la scène, l’approche des objets et en recherchant les, lorsque le *Azure Insight Service* a collecté suffisamment de données événement, il définit l’objet qui a été a élaboré le plus au vert.

> [!IMPORTANT] 
> Alors que la durée d’attente moyenne pour le *événements et mesures* soit collecté par le Service prend environ 15 minutes, dans certains cas, il peut prendre jusqu'à 1 heure.

## <a name="chapter-14---the-application-insights-service-portal"></a>Chapitre 14 - le portail de Service Application Insights

Une fois que vous avez itinérante autour de la scène et gazed à plusieurs objets, vous pouvez voir les données collectées dans le *Service Application Insights* portail.

1.  Revenez à votre portail Service Application Insights.

2.  Cliquez sur *Metrics Explorer*.

    ![Examinez les données collectées](images/AzureLabs-Lab309-54.png)

3.  Il s’ouvre dans un onglet contenant le graphique qui représentent le *événements et mesures* relatives à votre application. Comme mentionné ci-dessus, il peut prendre un certain temps (jusqu'à 1 heure) pour les données à afficher dans le graphique

    ![Examinez les données collectées](images/AzureLabs-Lab309-55.png)

4.  Cliquez sur le *barre d’événements* dans le *Total d’événements* par la Version de l’Application pour afficher une description détaillée des événements avec leurs noms.

    ![Examinez les données collectées](images/AzureLabs-Lab309-56.png)

## <a name="your-finished-your-application-insights-service-application"></a>Votre terminé votre application de Service Application Insights

Félicitations, vous avez créé une application de réalité mixte qui tire parti du Service Application Insights pour surveiller l’activité de l’utilisateur au sein de votre application.

![résultat de cours](images/AzureLabs-Lab309-00.png)

## <a name="bonus-exercises"></a>Exercices de bonus

**Exercice 1**

Essayez de génération dynamique, plutôt que de création manuelle, les objets ObjectInScene et définir leurs coordonnées sur le plan dans vos scripts. De cette façon, vous pouvez demander à Azure populaires l’objet a été (soit à partir des résultats du pointage de regard ou proximité) et générer un *supplémentaire* un de ces objets.

**Exercice 2**

Trier les résultats de votre Application Insights en temps, afin que vous obtenez les données les plus pertinentes et implémentez les temps des données sensibles dans votre application.

