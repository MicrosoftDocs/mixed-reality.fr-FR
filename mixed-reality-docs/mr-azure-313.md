---
title: RM et Azure 313-IoT Hub service
description: Suivez ce cours pour apprendre à implémenter Azure IoT Hub service sur une machine virtuelle exécutant Ubuntu 16,4, puis visualisez les données de message à l’aide de Microsoft HoloLens ou d’un casque immersif.
author: drneil
ms.author: jemccull
ms.date: 07/11/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, périphérie, IOT Edge, didacticiel, API, notification, fonctions, tables, hololens, immersif, VR, IOT, machine virtuelle, Ubuntu, Python
ms.openlocfilehash: 93f7dc64426360d2e02b0ee0a9b1796fc8f2b469
ms.sourcegitcommit: 06ac2200d10b50fb5bcc413ce2a839e0ab6d6ed1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67694600"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.

# <a name="mr-and-azure-313-iot-hub-service"></a>MR et Azure 313: Service IoT Hub

![résultat du cours](images/AzureLabs-Lab313-00.png)

Dans ce cours, vous allez apprendre à implémenter un **service Azure IOT Hub** sur une machine virtuelle exécutant le système d’exploitation Ubuntu 16,4. Un **Function App Azure** est ensuite utilisé pour recevoir des messages de votre machine virtuelle Ubuntu et stocker le résultat dans un **service de table Azure**. Vous pourrez ensuite afficher ces données à l’aide de **Power bi** sur Microsoft HoloLens ou un casque immersif (VR).

Le contenu de ce cours *s’applique* aux appareils IOT Edge, bien que dans le cadre de ce cours, l’objectif est de se concentrer sur un environnement de machine virtuelle, de sorte que l’accès à un appareil de périphérie physique n’est pas nécessaire.

En suivant ce cours, vous allez apprendre à:

- Déployez un **module IOT Edge** sur une machine virtuelle (Ubuntu 16 OS) qui représente votre appareil IOT.
- Ajoutez un **modèle Tensorflow Azure Custom vision** au module Edge, avec le code qui analysera les images stockées dans le conteneur.
- Configurez le module pour renvoyer le message de résultat de l’analyse à votre **service de IOT Hub**.
- Utilisez un **Function App Azure** pour stocker le message dans une **table Azure**.
- Configurez **Power bi** pour collecter le message stocké et créer un rapport.
- Visualisez les données de vos messages IoT dans **Power bi**.

Les services que vous allez utiliser sont les suivants:

- **Azure IOT Hub** est un service Microsoft Azure qui permet aux développeurs de connecter, surveiller et gérer des ressources IOT. Pour plus d’informations, consultez la page du [ **Service Azure IOT Hub** ](https://azure.microsoft.com/en-au/services/iot-hub/).

- **Azure Container Registry** est un service Microsoft Azure qui permet aux développeurs de stocker des images de conteneur pour différents types de conteneurs. Pour plus d’informations, consultez la page du [ **service Azure Container Registry** ](https://azure.microsoft.com/en-au/services/container-registry/).

- **Azure Function App** est un service Microsoft Azure, qui permet aux développeurs d’exécuter de petits morceaux de code, «functions», dans Azure. Cela permet de déléguer le travail au Cloud, plutôt qu’à votre application locale, ce qui peut avoir de nombreux avantages. **Azure Functions** prend en charge plusieurs langages de\#développement,\#notamment C, F, node. js, Java et php. Pour plus d’informations, consultez la [page **Azure Functions** ](https://docs.microsoft.com/azure/azure-functions/functions-overview).

- **Stockage Azure: Tables** est un service Microsoft Azure, qui permet aux développeurs de stocker des données structurées non SQL dans le Cloud, ce qui les rend facilement accessibles en tout lieu. Le service dispose d’une conception sans schéma, ce qui permet l’évolution des tables en fonction des besoins et est donc très flexible. Pour plus d’informations, consultez la [page **tables Azure**](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)

Ce cours vous apprend à configurer et à utiliser le service IoT Hub, puis à visualiser une réponse fournie par un appareil. Il vous faudra appliquer ces concepts à une configuration de service IoT Hub personnalisée, que vous pouvez générer.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td> MR et Azure 313: Service IoT Hub</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="prerequisites"></a>Prérequis

Pour obtenir les conditions préalables les plus récentes concernant le développement avec la réalité mixte, y compris avec Microsoft HoloLens, consultez l’article [installer les outils](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) .

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base avec Python. Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018). Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.

Le matériel et les logiciels suivants sont requis:

- Windows 10 automne Creators Update (ou version ultérieure), **mode développeur activé**

    > [!WARNING]
    > Vous ne pouvez pas exécuter une machine virtuelle à l’aide d’Hyper-V sur Windows 10 édition personnelle.

- SDK Windows 10 (dernière version)
- HoloLens, **mode développeur activé**
- Visual Studio 2017.15.4 (uniquement utilisé pour accéder à Azure Cloud Explorer)
- Accès Internet pour Azure et pour IoT Hub service. Pour plus d’informations, cliquez sur le lien ci-dessous [pour IOT Hub page de service](https://azure.microsoft.com/en-au/services/iot-hub/)
- Modèle de Machine Learning. Si vous n’avez pas votre propre modèle prêt à l’emploi, [vous pouvez utiliser le modèle fourni avec ce cours](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip).
- Logiciel **Hyper-V** activé sur votre ordinateur de développement Windows 10.
- Une machine virtuelle exécutant Ubuntu (16,4 ou 18,4) en cours d’exécution sur votre ordinateur de développement. vous pouvez également utiliser un autre ordinateur exécutant Linux (Ubuntu 16,4 ou 18,4). Vous trouverez plus d’informations sur la création d’une machine virtuelle sur Windows à l’aide d’Hyper-V dans le [chapitre «avant de commencer»](#before-you-start). (https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine).  



### <a name="before-you-start"></a>Avant de commencer

1. Configurez et testez votre HoloLens. Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup).
2. Il est judicieux d’effectuer un réglage de l' **étalonnage** et du **capteur** au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur).

Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).

3. Configurez votre **machine virtuelle Ubuntu** à l’aide d' **Hyper-V**. Les ressources suivantes vous aideront à effectuer le processus.
    1.  Tout d’abord, suivez ce lien pour [Télécharger le fichier ISO Ubuntu 16.04.4 LTS (Xenial Xerus)](http://au.releases.ubuntu.com/16.04/). Sélectionnez l' **image de bureau 64-bit PC (amd64)** .
    2.  Vérifiez que **Hyper-V** est activé sur votre ordinateur Windows 10. Vous pouvez suivre ce lien pour obtenir des conseils sur [l’installation et l’activation d’Hyper-V sur Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).
    3.  Démarrez Hyper-V et créez une nouvelle machine virtuelle Ubuntu. Vous pouvez suivre ce lien pour obtenir un [Guide pas à pas sur la création d’une machine virtuelle avec Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine). Lorsque vous êtes invité à **«installer un système d’exploitation à partir d’un fichier image de démarrage»** , sélectionnez le fichier **ISO Ubuntu** que vous avez téléchargé plus tôt.

    > [!NOTE]
    > L’utilisation de la **création rapide Hyper-V** n’est pas suggérée.  

## <a name="chapter-1---retrieve-the-custom-vision-model"></a>Chapitre 1-récupération du modèle de Custom Vision

Ce cours vous permet d’accéder à un [modèle de Custom vision prédéfini](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip) qui détecte les claviers et les souris à partir d’images. Si vous utilisez cette valeur, passez au [Chapitre 2](#chapter-2---the-container-registry-service).

Toutefois, vous pouvez suivre ces étapes si vous souhaitez utiliser votre propre Custom Vision modèle:

1. Dans votre **projet Custom vision** , accédez à l’onglet **performances** .

    > [!WARNING]
    > Votre modèle doit utiliser un domaine *compact* pour exporter le modèle. Vous pouvez modifier votre domaine de modèles dans les paramètres de votre projet.

    ![onglet performances](images/AzureLabs-Lab313-01.png)

2. Sélectionnez l' **itération** que vous souhaitez exporter, puis cliquez sur **Exporter**. Un panneau s’affiche.

    ![panneau exporter](images/AzureLabs-Lab313-02.png)

3. Dans le panneau, cliquez sur le fichier de l' **ancrage**.

    ![sélectionner un ancrage](images/AzureLabs-Lab313-03.png)

4. Dans le menu déroulant, cliquez sur **Linux** , puis sur **Télécharger**.

    ![Cliquez sur Télécharger](images/AzureLabs-Lab313-04.png)

5. Décompressez le contenu. Vous l’utiliserez plus loin dans ce cours.

## <a name="chapter-2---the-container-registry-service"></a>Chapitre 2-service Container Registry

Le **Service Container Registry** est le référentiel utilisé pour héberger vos conteneurs.

Le **service IOT Hub** que vous allez générer et utiliser dans ce cours fait référence à **Container Registry service** pour obtenir les conteneurs à déployer sur votre appareil Edge.

1. Tout d’abord, suivez ce [lien vers le portail Azure](https://portal.azure.com/)et connectez-vous avec vos informations d’identification.

2. Accédez à **créer une ressource** et recherchez **Container Registry**.

    ![Registre de conteneurs](images/AzureLabs-Lab313-05.png)

3. Cliquez sur **créer**.

    ![](images/AzureLabs-Lab313-06.png)

4. Définissez les paramètres de configuration du service:

    1. Insérez un nom pour votre projet, dans cet exemple, son appelé **IoTCRegistry**.

    2. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.

    3. Définissez l’emplacement du service.

    4. Définissez **utilisateur administrateur** sur **activer**.

    5. Définissez **SKU** sur de **base**. 

    ![](images/AzureLabs-Lab313-07.png)

5. Cliquez sur **créer** et attendez que les services soient créés. 

6. Une fois que la notification s’affiche pour vous informer de la réussite de la création de l' *Container Registry*, cliquez sur **accéder à la ressource** pour être redirigé vers la page de votre service.

    ![](images/AzureLabs-Lab313-08.png)

7. Dans la page service *Container Registry* , cliquez sur **clés d’accès**.

8. Prenez note (vous pouvez utiliser votre bloc-notes) des paramètres suivants:
    1. **Serveur de connexion**
    2. **Nom d’utilisateur**
    3. **Mot de passe**

    ![](images/AzureLabs-Lab313-09.png)

## <a name="chapter-3---the-iot-hub-service"></a>Chapitre 3-service IoT Hub

À présent, vous allez commencer la création et la configuration de votre **Service IOT Hub**.

1. Si vous n’êtes pas déjà connecté, connectez-vous au [portail Azure](https://portal.azure.com).

2.  Une fois connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche, recherchez **IOT Hub**, puis cliquez sur **entrée**.

 ![Rechercher le compte de stockage](images/AzureLabs-Lab313-10.png)

3.  La nouvelle page fournit une description du service de **compte de stockage** . En bas à gauche de cette invite, cliquez sur le bouton **créer** pour créer une instance de ce service.

    ![créer une instance de stockage](images/AzureLabs-Lab313-11.png)

4.  Une fois que vous avez cliqué sur **créer**, un panneau s’affiche:

    1. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).


    2. Sélectionnez un **emplacement** approprié (utilisez le même emplacement pour tous les services que vous créez dans ce cours).

    3. Insérez le **nom** de votre choix pour cette instance de service.    

5.  En bas de la page, cliquez **sur suivant: Taille et échelle**.

    ![créer une instance de stockage](images/AzureLabs-Lab313-12.png)

6.  Dans cette page, sélectionnez votre **niveau de tarification et** de mise à l’échelle (s’il s’agit de votre première instance de service IOT Hub, vous devez disposer d’un niveau gratuit).  

7.  Cliquez sur **révision + créer**.

    ![créer une instance de stockage](images/AzureLabs-Lab313-13.png)

8.  Passez en revue vos paramètres, puis cliquez sur **créer**.

    ![créer une instance de stockage](images/AzureLabs-Lab313-14.png)

9. Une fois que la notification s’affiche pour vous informer de la réussite de la création du service *IOT Hub* , cliquez sur **accéder à la ressource** pour être redirigé vers votre page de service.

    ![créer une instance de stockage](images/AzureLabs-Lab313-15.png)

10. Faites défiler le panneau latéral sur la gauche jusqu’à ce que la *gestion automatique des appareils*s’affiche, cliquez sur **IOT Edge**.

    ![créer une instance de stockage](images/AzureLabs-Lab313-16.png)

11. Dans la fenêtre qui s’affiche à droite, cliquez sur **ajouter IOT Edge appareil**. Un panneau s’affiche à droite.

12. Dans le panneau, fournissez à votre nouvel appareil un **ID d’appareil** (le nom de votre choix). Cliquez ensuite sur **Enregistrer**. Les clés *primaires* et *secondaires* seront générées automatiquement, si la **génération automatique** est cochée.

    ![créer une instance de stockage](images/AzureLabs-Lab313-17.png)

13. Vous revenez à la section *IOT Edge* Devices, où votre nouveau périphérique sera listé. Cliquez sur votre nouvel appareil (indiqué en rouge dans l’image ci-dessous). 

    ![créer une instance de stockage](images/AzureLabs-Lab313-18.png)

14. Sur la page Détails de l' *appareil* qui s’affiche, effectuez une copie de la **chaîne de connexion** (clé primaire).

    ![créer une instance de stockage](images/AzureLabs-Lab313-19.png)

15. Revenez au volet de gauche, puis cliquez sur *stratégies d’accès partagé*pour l’ouvrir. 

16. Sur la page qui s’affiche, cliquez sur **iothubowner**. un panneau s’affiche à droite de l’écran. 

17. Prenez note (dans votre bloc-notes) de la **chaîne de connexion** (clé primaire), pour une utilisation ultérieure lors de la définition de la *chaîne de connexion* à votre appareil.

    ![créer une instance de stockage](images/AzureLabs-Lab313-20.png)

## <a name="chapter-4---setting-up-the-development-environment"></a>Chapitre 4-Configuration de l’environnement de développement

Pour créer et déployer des modules pour *IOT Hub Edge*, vous devez installer les composants suivants sur votre ordinateur de développement exécutant Windows 10:

1.  [Docker pour Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows), vous êtes invité à créer un compte pour pouvoir effectuer le téléchargement. 

    [![Télécharger l’ancrage pour Windows](images/AzureLabs-Lab313-21.png)](https://store.docker.com/editions/community/docker-ce-desktop-windows)

    > [!IMPORTANT]
    > L’ancrage requiert *Windows 10 professionnel*, *Enterprise 14393*ou *Windows Server 2016 RTM*pour s’exécuter. Si vous exécutez d’autres versions de Windows 10, vous pouvez essayer d’installer l’outil d’ancrage à l’aide de la [boîte à outils](https://docs.docker.com/toolbox/toolbox_install_windows/)de l’ancrage.

2.  [Python 3,6](https://www.python.org/downloads/).

    [![Télécharger python 3,6](images/AzureLabs-Lab313-22.png)](https://www.python.org/downloads/)

3.  [Visual Studio code (également appelé vs code)](https://code.visualstudio.com/download).

    [![Télécharger VS Code](images/AzureLabs-Lab313-23.png)](https://code.visualstudio.com/download)

Après avoir installé le logiciel mentionné ci-dessus, vous devrez redémarrer votre ordinateur.

## <a name="chapter-5---setting-up-the-ubuntu-environment"></a>Chapitre 5-Configuration de l’environnement Ubuntu

Vous pouvez maintenant passer à la configuration de votre appareil **exécutant le système d’exploitation Ubuntu**. Suivez les étapes ci-dessous pour installer les logiciels nécessaires, afin de déployer vos conteneurs sur votre tableau:

> [!IMPORTANT]
> Vous devez toujours précéder les commandes de terminal avec **sudo** pour qu’elles s’exécutent en tant qu’administrateur. celles
> 
>   ```bash
>   sudo docker \<option> \<command> \<argument>
>   ```

1.  Ouvrez le **Terminal Ubuntu**et utilisez la commande suivante pour installer **PIP**:

    > [! Conseil] vous pouvez facilement ouvrir un *Terminal* à l’aide du raccourci clavier: **CTRL + ALT + T**.

    ```bash
        sudo apt-get install python-pip
    ```

2.  Tout au long de ce chapitre, vous pouvez être invité, par *Terminal*, à utiliser le stockage de votre appareil. pour entrer **y/n** (oui ou non), tapez **«y»** , puis appuyez sur la touche **entrée** pour accepter.

3.  Une fois cette commande terminée, utilisez la commande suivante pour installer la **boucle**:

    ```bash
        sudo apt install curl
    ```

4.  Une fois **PIP** et **bouclé** installés, utilisez la commande suivante pour installer le **Runtime IOT Edge**, ce qui est nécessaire pour déployer et contrôler les modules de votre tableau:

    ```bash
        curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list

        sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

        curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg

        sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/

        sudo apt-get update

        sudo apt-get install moby-engine

        sudo apt-get install moby-cli

        sudo apt-get update

        sudo apt-get install iotedge
    ```

5. À ce stade, vous serez invité à ouvrir le fichier de *configuration du runtime*, à insérer la **chaîne de connexion**de l’appareil, que vous avez noté (dans votre bloc-notes), lors de la création du **service IOT Hub** ([à l’étape 14, du chapitre 3](#chapter-3---the-iot-hub-service)). Exécutez la ligne suivante sur le terminal pour ouvrir ce fichier:

    ```bash
        sudo nano /etc/iotedge/config.yaml
    ```

6. Le fichier **config. YAML** s’affiche et vous pouvez le modifier:

    > [!WARNING]
    > Lorsque ce fichier s’ouvre, il peut être quelque peu déroutant. Vous allez modifier le texte de ce fichier, au sein du *Terminal* lui-même. 

    1.  Utilisez les touches de direction de votre clavier pour faire défiler vers le bas (vous devez faire défiler une petite façon) pour atteindre la ligne contenant «:

        " **\<AJOUTER ICI DEVICE CONNECTION STRING &GT;** ".

    2. Ligne de remplacement, **y compris les crochets**, avec la **chaîne de connexion** de l’appareil que vous avez notée précédemment.

7. Une fois votre chaîne de connexion en place, sur votre clavier, appuyez sur les touches **CTRL-X** pour enregistrer le fichier. Vous êtes invité à confirmer en tapant **Y**. Appuyez ensuite sur la touche **entrée** pour confirmer. Vous allez revenir au *Terminal*standard. 

8. Une fois que l’exécution de ces commandes est terminée, vous avez installé le **Runtime IOT Edge**. Une fois initialisé, le runtime démarre automatiquement chaque fois que l’appareil est mis sous tension, et se assiste en arrière-plan, en attendant que les modules soient déployés à partir du **Service IOT Hub**.

9.  Exécutez la ligne de commande suivante pour initialiser le *Runtime IOT Edge*:

    ```bash
        sudo systemctl restart iotedge
    ```

    > [!IMPORTANT]
    > Si vous apportez des modifications à votre fichier. YAML, ou au programme d’installation ci-dessus, vous devrez réexécuter la ligne de redémarrage ci-dessus, dans le *Terminal*.

10. Vérifiez l’état de l' *exécution de IOT Edge* en exécutant la ligne de commande suivante. Le Runtime doit s’afficher avec l’état **actif (en cours d’exécution)** en texte vert.

    ```bash
        sudo systemctl status iotedge
    ```

11. Appuyez sur les touches **Ctrl + C** pour quitter la page d’État. Vous pouvez vérifier que le *Runtime IOT Edge* récupère correctement les conteneurs en tapant la commande suivante:

    ```bash
        sudo docker ps
    ```

12. Une liste contenant deux (2) conteneurs doit s’afficher. Il s’agit des modules par défaut qui sont créés automatiquement par le service IoT Hub (edgeAgent et edgeHub). Une fois que vous avez créé et déployé vos propres modules, ceux-ci s’affichent dans cette liste, sous les paramètres par défaut.

## <a name="chapter-6---install-the-extensions"></a>Chapitre 6-installer les extensions

> [!IMPORTANT]
> Les chapitres suivants (6-9) doivent être exécutés sur votre ordinateur Windows 10.

1. Ouvrez **vs code**.

2. Cliquez sur le bouton **Extensions** (carré) dans la barre de gauche de vs code pour ouvrir le **panneau extensions**.

3. Recherchez et installez les extensions suivantes (comme indiqué dans l’image ci-dessous):

    1. Azure IoT Edge
    2. Boîte à outils Azure IoT
    3. Docker   

    ![Créer votre conteneur](images/AzureLabs-Lab313-24.png)

4. Une fois les extensions installées, fermez et rouvrez VS Code.

5. Une fois que vs code ouvert, accédez à **Afficher** > le**Terminal intégré**.

6. Vous allez maintenant installer **Cookiecutter**. Dans le terminal, exécutez la commande bash suivante:

    ```bash
        pip install --upgrade --user cookiecutter
    ```

    > [! Conseil] Si vous rencontrez des problèmes avec cette commande: 
    >1. Redémarrez VS Code et/ou votre ordinateur.
    >2. Il peut être nécessaire de basculer le **Terminal vs code** vers celui que vous avez utilisé pour installer Python, C.-à-d. **PowerShell** (en particulier si l’environnement python était déjà installé sur votre ordinateur). Une fois le terminal ouvert, vous trouverez le menu déroulant sur le côté droit du terminal.
     ![Créer votre conteneur](images/AzureLabs-Lab313-24b.png) 
    >3. Assurez-vous que le chemin d’installation de **python** est ajouté en tant que **variable d’environnement** sur votre ordinateur. Cookiecutter doit faire partie du même chemin d’emplacement. [Pour plus d’informations sur les variables d’environnement](https://msdn.microsoft.com/library/windows/desktop/ms682653(v=vs.85).aspx), cliquez sur le lien suivant: 

7. Une fois l’installation de **Cookiecutter** terminée, vous devez redémarrer votre ordinateur pour que **Cookiecutter** soit reconnu en tant que commande dans l’environnement de votre système.

## <a name="chapter-7---create-your-container-solution"></a>Chapitre 7-créer votre solution de conteneur

À ce stade, vous devez créer le conteneur, avec le module, pour faire l’objet d’un push dans le *Container Registry*. Une fois que vous avez poussé votre conteneur, vous allez utiliser le service *IOT Hub Edge* pour le déployer sur votre appareil, qui exécute le *IOT Edge Runtime*.

1. Dans vs code, cliquez sur **Afficher** > la**palette de commandes**.

2. Dans la palette, recherchez et exécutez **Azure IOT Edge: Nouvelle solution**IOT Edge.

3. Accédez à l’emplacement où vous souhaitez créer votre solution. Appuyez sur la touche **entrée** pour accepter l’emplacement.

4. Donnez un nom à votre solution. Appuyez sur la touche **entrée** pour confirmer le nom fourni.

5. Vous êtes maintenant invité à choisir l’infrastructure de modèle pour votre solution. Cliquez sur **module python**. Appuyez sur la touche **entrée** pour confirmer ce choix.

6. Donnez un nom à votre module. Appuyez sur la touche **entrée** pour confirmer le nom de votre module. Veillez à prendre note (avec votre bloc-notes) du nom du module, car il est utilisé ultérieurement.

7. Vous remarquerez que l’adresse d’un *référentiel d’images d’ancrage* prédéfini s’affichera dans la palette. Elle doit ressembler à ceci:

    **localhost: 5000/-le nom de votre module-** . 

8. Supprimez **localhost: 5000**et, à sa place, insérez l’adresse du **serveur de connexion** *Container Registry* , que vous avez notée lors de la création du **service Container Registry** ([à l’étape 8, du chapitre 2](#chapter-2---the-container-registry-service)). Appuyez sur la touche **entrée** pour confirmer l’adresse.

9. À ce stade, la solution contenant le modèle pour votre module Python est créée et sa structure s’affiche sous l' **onglet Explorer**, de vs code, sur le côté gauche de l’écran. Si l' **onglet Explorer** n’est pas ouvert, vous pouvez l’ouvrir en cliquant sur le bouton supérieur, dans la barre à gauche.

    ![Créer votre conteneur](images/AzureLabs-Lab313-25.png)

10. La dernière étape de ce chapitre consiste à cliquer et à ouvrir le **fichier. env**, à partir de l' **onglet Explorer**, et à ajouter votre **nom d’utilisateur** et votre **mot de passe** *Container Registry* . Ce fichier est ignoré par git, mais lors de la création du conteneur, les informations d’identification sont définies pour accéder au **Service Container Registry**.

    ![Créer votre conteneur](images/AzureLabs-Lab313-26.png)

## <a name="chapter-8---editing-your-container-solution"></a>Chapitre 8-modification de votre solution de conteneur

Vous allez maintenant terminer la solution Container, en mettant à jour les fichiers suivants:

- *main<span></span>. py* python script.
- *Requirements. txt*.
- *Deployment. template. JSON*.
- *Fichier dockerfile. amd64*

Vous allez ensuite créer le dossier *images* , utilisé par le script Python pour rechercher les images à faire correspondre à votre *modèle de Custom vision*. Enfin, vous allez ajouter le fichier *labels. txt* , pour vous aider à lire votre modèle et le fichier *Model. PB* , qui est votre modèle.

1. Avec VS Code ouvrir, accédez à votre dossier de module, puis recherchez le script nommé **main<span></span>. py**. Double-cliquez pour l’ouvrir.

2. Supprimez le contenu du fichier et insérez le code suivant:

    ```python
    # Copyright (c) Microsoft. All rights reserved.
    # Licensed under the MIT license. See LICENSE file in the project root for
    # full license information.

    import random
    import sched, time
    import sys
    import iothub_client
    from iothub_client import IoTHubModuleClient, IoTHubClientError, IoTHubTransportProvider
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError
    import json
    import os
    import tensorflow as tf
    import os
    from PIL import Image
    import numpy as np
    import cv2

    # messageTimeout - the maximum time in milliseconds until a message times out.
    # The timeout period starts at IoTHubModuleClient.send_event_async.
    # By default, messages do not expire.
    MESSAGE_TIMEOUT = 10000

    # global counters
    RECEIVE_CALLBACKS = 0
    SEND_CALLBACKS = 0

    TEMPERATURE_THRESHOLD = 25
    TWIN_CALLBACKS = 0

    # Choose HTTP, AMQP or MQTT as transport protocol.  Currently only MQTT is supported.
    PROTOCOL = IoTHubTransportProvider.MQTT


    # Callback received when the message that we're forwarding is processed.
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )


    def convert_to_opencv(image):
        # RGB -> BGR conversion is performed as well.
        r,g,b = np.array(image).T
        opencv_image = np.array([b,g,r]).transpose()
        return opencv_image

    def crop_center(img,cropx,cropy):
        h, w = img.shape[:2]
        startx = w//2-(cropx//2)
        starty = h//2-(cropy//2)
        return img[starty:starty+cropy, startx:startx+cropx]

    def resize_down_to_1600_max_dim(image):
        h, w = image.shape[:2]
        if (h < 1600 and w < 1600):
            return image

        new_size = (1600 * w // h, 1600) if (h > w) else (1600, 1600 * h // w)
        return cv2.resize(image, new_size, interpolation = cv2.INTER_LINEAR)

    def resize_to_256_square(image):
        h, w = image.shape[:2]
        return cv2.resize(image, (256, 256), interpolation = cv2.INTER_LINEAR)

    def update_orientation(image):
        exif_orientation_tag = 0x0112
        if hasattr(image, '_getexif'):
            exif = image._getexif()
            if (exif != None and exif_orientation_tag in exif):
                orientation = exif.get(exif_orientation_tag, 1)
                # orientation is 1 based, shift to zero based and flip/transpose based on 0-based values
                orientation -= 1
                if orientation >= 4:
                    image = image.transpose(Image.TRANSPOSE)
                if orientation == 2 or orientation == 3 or orientation == 6 or orientation == 7:
                    image = image.transpose(Image.FLIP_TOP_BOTTOM)
                if orientation == 1 or orientation == 2 or orientation == 5 or orientation == 6:
                    image = image.transpose(Image.FLIP_LEFT_RIGHT)
        return image


    def analyse(hubManager):

        messages_sent = 0;

        while True:
            #def send_message():
            print ("Load the model into the project")
            # These names are part of the model and cannot be changed.
            output_layer = 'loss:0'
            input_node = 'Placeholder:0'

            graph_def = tf.GraphDef()
            labels = []

            labels_filename = "labels.txt"
            filename = "model.pb"

            # Import the TF graph
            with tf.gfile.FastGFile(filename, 'rb') as f:
                graph_def.ParseFromString(f.read())
                tf.import_graph_def(graph_def, name='')

            # Create a list of labels
            with open(labels_filename, 'rt') as lf:
                for l in lf:
                    labels.append(l.strip())
            print ("Model loaded into the project")

            results_dic = dict()

            # create the JSON to be sent as a message
            json_message = ''

            # Iterate through images 
            print ("List of images to analyse:")
            for file in os.listdir('images'):
                print(file)

                image = Image.open("images/" + file)

                # Update orientation based on EXIF tags, if the file has orientation info.
                image = update_orientation(image)

                # Convert to OpenCV format
                image = convert_to_opencv(image)

                # If the image has either w or h greater than 1600 we resize it down respecting
                # aspect ratio such that the largest dimension is 1600
                image = resize_down_to_1600_max_dim(image)

                # We next get the largest center square
                h, w = image.shape[:2]
                min_dim = min(w,h)
                max_square_image = crop_center(image, min_dim, min_dim)

                # Resize that square down to 256x256
                augmented_image = resize_to_256_square(max_square_image)

                # The compact models have a network size of 227x227, the model requires this size.
                network_input_size = 227

                # Crop the center for the specified network_input_Size
                augmented_image = crop_center(augmented_image, network_input_size, network_input_size)

                try:
                    with tf.Session() as sess:     
                        prob_tensor = sess.graph.get_tensor_by_name(output_layer)
                        predictions, = sess.run(prob_tensor, {input_node: [augmented_image] })
                except Exception as identifier:
                    print ("Identifier error: ", identifier)

                print ("Print the highest probability label")
                highest_probability_index = np.argmax(predictions)
                print('FINAL RESULT! Classified as: ' + labels[highest_probability_index])

                l = labels[highest_probability_index]

                results_dic[file] = l

                # Or you can print out all of the results mapping labels to probabilities.
                label_index = 0
                for p in predictions:
                    truncated_probablity = np.float64(round(p,8))
                    print (labels[label_index], truncated_probablity)
                    label_index += 1

            print("Results dictionary")
            print(results_dic)

            json_message = json.dumps(results_dic)
            print("Json result")
            print(json_message)

            # Initialize a new message
            message = IoTHubMessage(bytearray(json_message, 'utf8'))
        
            hubManager.send_event_to_output("output1", message, 0)

            messages_sent += 1
            print("Message sent! - Total: " + str(messages_sent))      
            print('----------------------------')
            
            # This is the wait time before repeating the analysis
            # Currently set to 10 seconds
            time.sleep(10)


    class HubManager(object):
        
        def __init__(
                self,
                protocol=IoTHubTransportProvider.MQTT):
            self.client_protocol = protocol
            self.client = IoTHubModuleClient()
            self.client.create_from_environment(protocol)

            # set the time until a message times out
            self.client.set_option("messageTimeout", MESSAGE_TIMEOUT)

        # Forwards the message received onto the next stage in the process.
        def forward_event_to_output(self, outputQueueName, event, send_context):
            self.client.send_event_async(
                outputQueueName, event, send_confirmation_callback, send_context)

        def send_event_to_output(self, outputQueueName, event, send_context):
            self.client.send_event_async(outputQueueName, event, send_confirmation_callback, send_context)

    def main(protocol):
        try:
            hub_manager = HubManager(protocol)
            analyse(hub_manager)
            while True:
                time.sleep(1)

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubModuleClient sample stopped" )

    if __name__ == '__main__':
        main(PROTOCOL)
    ```

3.  Ouvrez le fichier nommé **Requirements. txt**et remplacez son contenu par ce qui suit:

    ```
    azure-iothub-device-client==1.4.0.0b3
    opencv-python==3.3.1.11
    tensorflow==1.8.0
    pillow==5.1.0
    ```

4.  Ouvrez le fichier nommé **Deployment. template. JSON**et remplacez son contenu en suivant les instructions ci-dessous:

    1. Étant donné que vous aurez votre propre structure JSON unique, vous devrez la modifier manuellement (plutôt que de copier un exemple). Pour faciliter cette opération, utilisez l’image ci-dessous comme guide.
    2. Les zones qui sont différentes des vôtres, mais que vous ne **devez pas modifier sont mises**en surbrillance en jaune.
    3. **Les sections que vous devez supprimer sont en rouge.**
    4. Veillez à supprimer les crochets appropriés et à supprimer également les virgules.

        ![Créer votre conteneur](images/AzureLabs-Lab313-27.png)

    5. Le JSON complet doit ressembler à l’image suivante (avec les différences uniques suivantes: *nom d’utilisateur/mot de passe/nom de module/références de module*):

        ![Créer votre conteneur](images/AzureLabs-Lab313-28.png)

5.  Ouvrez le fichier nommé **fichier dockerfile. amd64**et remplacez son contenu par ce qui suit:

    ```
    FROM ubuntu:xenial

    WORKDIR /app

    RUN apt-get update && \
        apt-get install -y --no-install-recommends libcurl4-openssl-dev python-pip libboost-python-dev && \
        rm -rf /var/lib/apt/lists/* 
    RUN pip install --upgrade pip
    RUN pip install setuptools

    COPY requirements.txt ./
    RUN pip install -r requirements.txt

    RUN pip install pillow
    RUN pip install numpy

    RUN apt-get update && apt-get install -y \ 
        pkg-config \
        python-dev \ 
        python-opencv \ 
        libopencv-dev \ 
        libav-tools  \ 
        libjpeg-dev \ 
        libpng-dev \ 
        libtiff-dev \ 
        libjasper-dev \ 
        python-numpy \ 
        python-pycurl \ 
        python-opencv


    RUN pip install opencv-python
    RUN pip install tensorflow
    RUN pip install --upgrade tensorflow

    COPY . .

    RUN useradd -ms /bin/bash moduleuser
    USER moduleuser

    CMD [ "python", "-u", "./main.py" ]

    ```

6.  Cliquez avec le bouton droit sur le dossier sous **modules** (il porte le nom que vous avez fourni précédemment. dans cet exemple, il est appelé *pythonmodule*), puis cliquez sur **nouveau dossier**. Nommez le dossier **images**.

7.  Dans le dossier, ajoutez des images contenant la souris ou le clavier. Il s’agira des images qui seront analysées par le modèle Tensorflow.

    > [!WARNING]
    > Si vous utilisez votre propre modèle, vous devrez le modifier pour refléter vos propres données de modèles.

8.  Vous devez maintenant récupérer les fichiers **labels. txt** et **Model. PB** à partir du dossier Model, que vous avez précédemment téléchargé (ou créé à partir de votre propre **service vision personnalisée**), au [Chapitre 1](#chapter-1---retrieve-the-custom-vision-model). Une fois que vous avez les fichiers, placez-les dans votre solution, en même temps que les autres fichiers. Le résultat final doit ressembler à l’image ci-dessous:

    ![Créer votre conteneur](images/AzureLabs-Lab313-29.png)

## <a name="chapter-9---package-the-solution-as-a-container"></a>Chapitre 9-empaqueter la solution en tant que conteneur

1.  Vous êtes maintenant prêt à «empaqueter» vos fichiers en tant que conteneur et à les envoyer à votre **Azure Container Registry**. Dans vs code, ouvrez le *Terminal intégré* (**Affichez** > le**Terminal intégré** ou **CTRL**+ **\`** ) et utilisez la ligne suivante pour vous  connecter à dockr (remplacez les valeurs de la avec les informations d’identification de votre **Azure Container Registry (ACR)** ):

    ```bash
        docker login -u <ACR username> -p <ACR password> <ACR login server>
    ```

2. Cliquez avec le bouton droit sur le fichier **Deployment. template. JSON**, puis cliquez sur **générer IOT Edge solution**. Ce processus de génération prend un certain temps (en fonction de votre appareil), soyez donc prêt à attendre. Une fois le processus de génération terminé, un fichier de **déploiement. JSON** a été créé dans un nouveau dossier nommé **config**.

    ![créer un déploiement](images/AzureLabs-Lab313-30.png)

3. Rouvrez la **palette de commandes** et recherchez **Azure: Connectez-vous.** Suivez les invites à l’aide des informations d’identification de votre compte Azure. VS Code vous fournira une option de *copie et d’ouverture*, qui copiera le code de l’appareil dont vous aurez bientôt besoin et ouvrira votre navigateur Web par défaut. Lorsque vous y êtes invité, collez le code de l’appareil pour authentifier votre ordinateur.

    ![copier et ouvrir](images/AzureLabs-Lab313-31.png)

4. Une fois que vous êtes connecté, vous remarquerez, sur le côté inférieur du panneau d' *exploration* , une nouvelle section appelée **appareils Azure IOT Hub**. Cliquez sur cette section pour la développer.

    ![appareil de périphérie](images/AzureLabs-Lab313-32.png)

5. Si votre appareil n’est pas ici, vous devez cliquer avec le bouton droit sur *Azure IOT Hub*Devices, puis cliquer sur **définir IOT Hub chaîne de connexion**. Vous verrez alors que la **palette de commandes** (en haut de vs code) vous invitera à entrer votre *chaîne de connexion*. Il s’agit de la *chaîne de connexion* que vous avez notée à la fin du [chapitre 3](#chapter-3---the-iot-hub-service). Appuyez sur la touche **entrée** , une fois que vous avez copié la chaîne dans.    

6. Votre appareil doit se charger et s’afficher. Cliquez avec le bouton droit sur le nom de l’appareil, puis cliquez sur **créer un déploiement pour un seul appareil**.

    ![créer un déploiement](images/AzureLabs-Lab313-33b.png)

7. Une invite de l' *Explorateur de fichiers* s’affiche, dans laquelle vous pouvez accéder au dossier **config** , puis sélectionner le fichier **Deployment. JSON** . Une fois ce fichier sélectionné, cliquez sur le bouton **Sélectionner le manifeste de déploiement Edge** .

    ![créer un déploiement](images/AzureLabs-Lab313-34.png)

8. À ce stade, vous avez fourni à votre **Service IOT Hub** le manifeste pour le déploiement de votre conteneur, en tant que module, à partir de votre **Azure Container Registry**, en le déployant efficacement sur votre appareil.

9. Pour afficher les messages envoyés à partir de votre appareil au IoT Hub, cliquez à nouveau avec le bouton droit sur le nom de votre appareil dans la section **appareils IOT Hub Azure** , dans le panneau **Explorateur** , puis cliquez sur **Démarrer l’analyse du message D2C**. Les messages envoyés à partir de votre appareil doivent apparaître dans le terminal VS. Soyez patient, car cela peut prendre un certain temps. Consultez le chapitre suivant pour le débogage et vérification de la réussite du déploiement.

Ce module va à présent itérer entre les images du dossier **images** et les analyser, avec chaque itération. Il s’agit évidemment d’une démonstration de la façon d’obtenir le modèle de Machine Learning de base pour travailler dans un environnement d’appareil IoT Edge. 

Pour développer les fonctionnalités de cet exemple, vous pouvez procéder de plusieurs façons. L’une des façons peut inclure du code dans le conteneur, qui capture les photos à partir d’une webcam connectée à l’appareil et enregistre les images dans le dossier images. 

Vous pouvez également copier les images à partir de l’appareil IoT dans le conteneur. Pour ce faire, il est pratique d’exécuter la commande suivante dans le terminal de l’appareil IoT (peut-être une petite application peut-elle effectuer le travail, si vous souhaitez automatiser le processus). Vous pouvez tester cette commande en l’exécutant manuellement à partir de l’emplacement du dossier où sont stockés vos fichiers:

```bash
    sudo docker cp <filename> <modulename>:/app/images/<a name of your choice>
```

## <a name="chapter-10---debugging-the-iot-edge-runtime"></a>Chapitre 10-débogage du runtime IoT Edge

Vous trouverez ci-dessous une liste de lignes de commande et de conseils pour vous aider à surveiller et à déboguer l’activité de messagerie du *IOT Edge Runtime*, à partir de votre **appareil Ubuntu**. 

- Vérifiez l’état de l' *exécution de IOT Edge* en exécutant la ligne de commande suivante:

    ```bash
        sudo systemctl status iotedge
    ```

    > [!NOTE]
    > N’oubliez pas d’appuyer sur **Ctrl + C**pour terminer l’affichage de l’État.

- Répertorie les conteneurs qui sont actuellement déployés. Si le *Service IOT Hub* a déployé correctement les conteneurs, ceux-ci sont affichés en exécutant la ligne de commande suivante:

    ```bash
        sudo iotedge list
    ```

    Ou

    ```bash
        sudo docker ps
    ```

    > [!NOTE]
    > L’exemple ci-dessus est un bon moyen de vérifier si votre module a été correctement déployé, tel qu’il apparaîtra dans la liste. Sinon, vous ne verrez **que** *edgeHub* et *edgeAgent*.

- Pour afficher les journaux de code d’un conteneur, exécutez la ligne de commande suivante:

    ```bash
        journalctl -u iotedge
    ```

**Commandes utiles pour gérer le runtime IoT Edge:**

-  Pour supprimer tous les conteneurs de l’hôte:

    ```bash
        sudo docker rm -f $(sudo docker ps -aq)
    ```

-  Pour arrêter l' *exécution du IOT Edge*:

    ```bash
        sudo systemctl stop iotedge
    ```

## <a name="chapter-11---create-table-service"></a>Chapitre 11-créer un service de table 

Revenez à votre portail Azure, où vous allez créer un service de tables Azure, en créant une ressource de stockage.

1. Si vous n’êtes pas déjà connecté, connectez-vous au [portail Azure](https://portal.azure.com).

2. Une fois connecté, cliquez sur **créer une ressource**, dans le coin supérieur gauche, recherchez compte de **stockage**, puis appuyez sur la touche **entrée** pour lancer la recherche.

3. Une fois qu’il s’est affiché, cliquez sur **compte de stockage-BLOB, fichier, table, file d’attente** dans la liste.

    ![Rechercher le compte de stockage](images/AzureLabs-Lab313-35.png)

4. La nouvelle page fournit une description du service de **compte de stockage** . En bas à gauche de cette invite, cliquez sur le bouton **créer** pour créer une instance de ce service.

    ![créer une instance de stockage](images/AzureLabs-Lab313-36.png)

5. Une fois que vous avez cliqué sur **créer**, un panneau s’affiche:

    1. Insérez le **nom** souhaité pour cette instance de service (*doit être tout*en minuscules).

    2. Pour **modèle de déploiement**, cliquez sur Resource **Manager**.

    3. Pour **type de compte**, dans le menu déroulant, cliquez sur **stockage (v1 à usage général)** .

    4. Cliquez sur un **emplacement**approprié.
    
    5. Dans le  menu déroulant réplication, cliquez sur **stockage avec accès géo-redondant (RA-GRS)** .

    6. Pour les **performances**, cliquez sur **standard**.

    7. Dans la section **transfert sécurisé requis** , cliquez sur **désactivé**.

    8. Dans le menu déroulant **abonnement** , cliquez sur un abonnement approprié.

    9. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    10. Laissez les **réseaux virtuels** désactivés, s’il s’agit d’une option pour vous.

    11. Cliquez sur **Créer**.

        ![renseigner les détails du stockage](images/AzureLabs-Lab313-37.png)

6. Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.

7. Une notification s’affichera dans le portail une fois l’instance de service créée. Cliquez sur les notifications pour explorer votre nouvelle instance de service.

    ![nouvelle notification de stockage](images/AzureLabs-Lab313-38.png)

8. Cliquez sur le bouton **atteindre la ressource** dans la notification pour accéder à la page vue d’ensemble de votre nouvelle instance de service de stockage.

    ![Accéder à la ressource](images/AzureLabs-Lab313-39.png)

9. Dans la page vue d’ensemble, sur le côté droit, cliquez sur **tables**.
    
    ![Elles](images/AzureLabs-Lab313-40.png)

10. Le panneau à droite change pour afficher les informations sur le **service de table** , où vous devez ajouter une nouvelle table. Pour ce faire, cliquez sur le bouton **+ table** dans le coin supérieur gauche.

    ![Tables ouvertes](images/AzureLabs-Lab313-41.png)

11. Une nouvelle page s’affiche, dans laquelle vous devez entrer un nom de **table**. Il s’agit du nom que vous allez utiliser pour faire référence aux données de votre application dans les chapitres ultérieurs (création d’Function App et Power BI). Insérez **IoTMessages** comme nom (vous pouvez choisir les vôtres, mémorisez-les quand vous les utilisez plus loin dans ce document), puis cliquez sur **OK**. 

12. Une fois la nouvelle table créée, vous pouvez la voir dans la page **service de table** (en bas).

    ![nouvelle table créée](images/AzureLabs-Lab313-42.png)  

13. Maintenant, cliquez sur **clés d’accès** et copiez le **nom** et la **clé** du compte de stockage (à l’aide de votre bloc-notes). vous utiliserez ces valeurs plus loin dans ce cours, lors de la création de l' **Function App Azure**.

    ![nouvelle table créée](images/AzureLabs-Lab313-43.png) 

14. À nouveau, à l’aide du panneau situé à gauche, faites défiler jusqu’à la section *service de table* , puis cliquez sur **tables** (ou **Parcourir les tables**, dans nouveaux portails) et prenez une copie de l’URL de la **table** (à l’aide de votre bloc-notes). Vous utiliserez cette valeur plus loin dans ce cours, lors de la liaison de votre table à votre application **Power bi** .

    ![nouvelle table créée](images/AzureLabs-Lab313-44.png)

## <a name="chapter-12---completing-the-azure-table"></a>Chapitre 12-remplissage de la table Azure

Maintenant que votre compte de stockage de **service de table** a été configuré, il est temps d’y ajouter des données qui seront utilisées pour stocker et récupérer des informations. La modification de vos tables peut être effectuée par le biais de **Visual Studio**.

1. Ouvrez **Visual Studio** (**pas** Visual Studio code).

2. Dans le menu, cliquez sur **Afficher** > le**Cloud Explorer**.

    ![ouvrir Cloud Explorer](images/AzureLabs-Lab313-45.png)

3. Le **Cloud Explorer** s’ouvre en tant qu’élément ancré (patienter, car le chargement peut prendre du temps).

    > [!WARNING] 
    > Si l’abonnement que vous avez utilisé pour créer vos *comptes de stockage* n’est pas visible, vérifiez que vous disposez des éléments suivants: 
    > - Connectez-vous au même compte que celui que vous avez utilisé pour le portail Azure.
    > - Sélectionnez votre abonnement dans la page de gestion des comptes (vous devrez peut-être appliquer un filtre à partir de vos paramètres de compte):  
    >
    >   ![Rechercher un abonnement](images/AzureLabs-Lab313-46.png)

4. Vos services Cloud Azure s’affichent. Recherchez les **comptes de stockage** et cliquez sur la flèche à gauche de celle-ci pour développer vos comptes.

    ![ouvrir les comptes de stockage](images/AzureLabs-Lab313-47.png)

5. Une fois développé, le **compte de stockage** que vous venez de créer doit être disponible. Cliquez sur la flèche à gauche de votre stockage, puis une fois celle-ci développée, recherchez des **tables** , puis cliquez sur la flèche en regard de celle-ci pour afficher la **table** que vous avez créée dans le dernier chapitre. Double-cliquez sur votre **table**.

6. Votre table s’ouvre au centre de votre fenêtre Visual Studio. Cliquez sur l’icône de table **+** avec (plus).

    ![Ajouter une nouvelle table](images/AzureLabs-Lab313-48.png)

7. Une fenêtre s’affiche pour vous inviter à *Ajouter une entité*. Vous ne créerez qu’une seule entité, bien qu’elle ait trois propriétés. Vous remarquerez que *PartitionKey* et *RowKey* sont déjà fournis, car ils sont utilisés par la table pour rechercher vos données. 

    ![clé de partition et de ligne](images/AzureLabs-Lab313-49.png)

8. Mettez à jour les valeurs suivantes:

    - Nom : **PartitionKey**, valeur: **PK_IoTMessages** 

    - Nom : **RowKey**, valeur: **RK_1_IoTMessages** 

9. Ensuite, cliquez sur **Ajouter une propriété** (dans l’angle inférieur gauche de la fenêtre Ajouter une *entité* ) et ajoutez la propriété suivante:

    - **MessageContent**, en tant que *chaîne*, laissez la valeur vide.

10. Votre table doit correspondre à celle de l’image ci-dessous:

    ![Ajouter les valeurs correctes](images/AzureLabs-Lab313-50.png)

    > [!NOTE] 
    > La raison pour laquelle l’entité a le numéro 1 dans la clé de ligne est que vous souhaiterez peut-être ajouter d’autres messages, si vous souhaitez approfondir ce cours.

11. Cliquez sur **OK** lorsque vous avez terminé. Votre table est maintenant prête à être utilisée.

## <a name="chapter-13---create-an-azure-function-app"></a>Chapitre 13-créer un Function App Azure 

Il est maintenant temps de créer un *Function App Azure*, qui sera appelé par le *service IOT Hub* pour stocker les messages de l’appareil *IOT Edge* dans le service de **table** , que vous avez créé dans le chapitre précédent.

Tout d’abord, vous devez créer un fichier qui permettra à votre fonction Azure de charger les bibliothèques dont vous avez besoin.

1.  Ouvrez le **bloc-notes** (appuyez sur la *touche Windows*, puis tapez *Notepad*).

    ![ouvrir le bloc-notes](images/AzureLabs-Lab313-51.png)

2.  Avec le bloc-notes ouvert, insérez la structure JSON ci-dessous. Une fois que vous avez effectué cette opération, enregistrez-la sur votre bureau en tant que **Project. JSON**. Ce fichier définit les bibliothèques que votre fonction utilisera. Si vous avez utilisé NuGet, il vous semblera familier.
    
    > [!WARNING]
    > Il est important que le nom soit correct; Assurez-vous qu’il n' **a pas d’extension de fichier. txt** . Voir ci-dessous pour référence:
    >
    > ![Enregistrement JSON](images/AzureLabs-Lab313-52.png)

    ```json
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "WindowsAzure.Storage": "9.2.0"
        }
        }
    }
    }
    ```

3.  Connectez-vous au [portail Azure](https://portal.azure.com).

4.  Une fois que vous êtes connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche et recherchez **Function App**, puis appuyez sur la touche **entrée** pour effectuer la recherche. Cliquez sur *Function App* dans les résultats pour ouvrir un nouveau panneau.

    ![Rechercher une application de fonction](images/AzureLabs-Lab313-53.png)

5.  Le nouveau panneau fournit une description du service **Function App** . En bas à gauche de ce panneau, cliquez sur le bouton **créer** pour créer une association avec ce service.

    ![instance de l’application de fonction](images/AzureLabs-Lab313-54.png)

6.  Une fois que vous avez cliqué sur **créer**, renseignez les éléments suivants:

    1. Pour **nom**de l’application, insérez le nom de votre choix pour cette instance de service.

    2. Sélectionnez un **abonnement**.

    3. Sélectionnez le niveau tarifaire approprié, s’il s’agit de la première fois que vous créez un **Service Function App**, vous devez disposer d’un niveau gratuit.

    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure. Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. Pour **système d’exploitation**, cliquez sur Windows, car il s’agit de la plateforme prévue.

    6. Sélectionnez un **plan d’hébergement** (ce didacticiel utilise un **plan de consommation**.

    7. Sélectionnez un **emplacement** (choisissez le même emplacement que celui du stockage que vous avez créé à l’étape précédente)

    8. Pour la section **stockage** , **vous devez sélectionner le service de stockage que vous avez créé à l’étape précédente**.

    9. Vous n’aurez pas besoin de *application Insights* dans cette **application. n'** hésitez donc pas à la conserver.

    10. Cliquez sur **Créer**.

        ![créer une nouvelle instance](images/AzureLabs-Lab313-55.png)

7.  Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.

8.  Une notification s’affichera dans le portail une fois l’instance de service créée.

    ![nouvelle notification](images/AzureLabs-Lab313-56.png)

9.  Cliquez sur la notification, une fois le déploiement réussi (terminé).

10. Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service. 

    ![Accéder à la ressource](images/AzureLabs-Lab313-57.png)

11. Sur le côté gauche du nouveau panneau, cliquez sur l' **+** icône (plus) en regard de *fonctions*pour créer une fonction.

    ![Ajouter une nouvelle fonction](images/AzureLabs-Lab313-58.png)

12. Dans le panneau central, la fenêtre de création de **fonction** s’affiche. Faites défiler vers le dessous, puis cliquez sur **fonction personnalisée**.

    ![fonction personnalisée](images/AzureLabs-Lab313-59.png)

13. Faites défiler la page suivante jusqu’à ce que vous trouviez **IOT Hub (Event Hub)** , puis cliquez dessus.

    ![fonction personnalisée](images/AzureLabs-Lab313-60.png)

14. Dans le panneau **IOT Hub (Event Hub)** , définissez la **langue** **C#** sur, puis cliquez sur **nouveau**.

    ![fonction personnalisée](images/AzureLabs-Lab313-61.png)

15. Dans la fenêtre qui s’affiche, assurez-vous que **IOT Hub** est sélectionné et que le nom du champ *IOT Hub* correspond au nom de votre *service IOT Hub* que vous avez créé précédemment ([à l’étape 8, du chapitre 3](#chapter-3---the-iot-hub-service)). Cliquez ensuite sur le bouton **Sélectionner** .

    ![fonction personnalisée](images/AzureLabs-Lab313-62.png)

16. De retour dans le panneau **IOT Hub (Event Hub)** , cliquez sur **créer**.

    ![fonction personnalisée](images/AzureLabs-Lab313-63.png)

17. Vous serez redirigé vers l’éditeur de fonction.

    ![fonction personnalisée](images/AzureLabs-Lab313-64.png)

18. Supprimez tout le code qu’il contient et remplacez-le par ce qui suit:

    ```csharp
    #r "Microsoft.WindowsAzure.Storage"
    #r "NewtonSoft.Json"

    using System;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Table;
    using Newtonsoft.Json;
    using System.Threading.Tasks;

    public static async Task Run(string myIoTHubMessage, TraceWriter log)
    {
        log.Info($"C# IoT Hub trigger function processed a message: {myIoTHubMessage}");
        
        //RowKey of the table object to be changed
        string tableName = "IoTMessages";
        string tableURL = "https://iothubmrstorage.table.core.windows.net/IoTMessages";

        // If you did not name your Storage Service as suggested in the course, change the name here with the one you chose.
        string storageAccountName = "iotedgestor"; 

        string storageAccountKey = "<Insert your Storage Key here>";   

        string partitionKey = "PK_IoTMessages";
        string rowKey = "RK_1_IoTMessages";

        Microsoft.WindowsAzure.Storage.Auth.StorageCredentials storageCredentials =
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(storageAccountName, storageAccountKey);

        CloudStorageAccount storageAccount = new CloudStorageAccount(storageCredentials, true);

        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

        // Get a reference to a table named "IoTMessages"
        CloudTable messageTable = tableClient.GetTableReference(tableName);

        //Retrieve the table object by its RowKey
        TableOperation operation = TableOperation.Retrieve<MessageEntity>(partitionKey, rowKey);
        TableResult result = await messageTable.ExecuteAsync(operation);

        //Create a MessageEntity so to set its parameters
        MessageEntity messageEntity = (MessageEntity)result.Result;

        messageEntity.MessageContent = myIoTHubMessage;
        messageEntity.PartitionKey = partitionKey;
        messageEntity.RowKey = rowKey;

        //Replace the table appropriate table Entity with the value of the MessageEntity Ccass structure.
        operation = TableOperation.Replace(messageEntity);

        // Execute the insert operation.
        await messageTable.ExecuteAsync(operation);
    }

    // This MessageEntity structure which will represent a Table Entity
    public class MessageEntity : TableEntity
    {
        public string Type { get; set; }
        public string MessageContent { get; set; }   
    }
    ```

19. Modifiez les variables suivantes pour qu’elles correspondent aux valeurs appropriées (**tables** et valeurs de **stockage** , [respectivement des étapes 11 et 13 du chapitre 11](#chapter-11---create-table-service)), que vous trouverez dans votre **compte de stockage**:

    - **TableName**, avec le nom de votre **table** située dans votre **compte de stockage**.
    - **tableURL**, avec l’URL de votre **table** située dans votre **compte de stockage**.
    - **storageAccountName**, avec le nom de la valeur correspondant au nom de votre **compte de stockage** .
    - **storageAccountKey**, avec la clé que vous avez obtenue dans le service de stockage que vous avez créé précédemment.

    ![fonction personnalisée](images/AzureLabs-Lab313-65.png)

20. Avec le code en place, cliquez sur **Enregistrer**.

21. Ensuite, cliquez sur **\<** l’icône (flèche), sur le côté droit de la page.

    ![fonction personnalisée](images/AzureLabs-Lab313-66.png)

22. Un panneau s’affiche à partir de la droite. Dans ce panneau, cliquez sur **Télécharger**et un *Explorateur de fichiers* s’affiche.

23. Accédez à, puis cliquez sur le fichier **Project. JSON** que vous avez créé précédemment dans le **bloc-notes** , puis cliquez sur le bouton **ouvrir** . Ce fichier définit les bibliothèques que votre fonction utilisera.

    ![fonction personnalisée](images/AzureLabs-Lab313-67.png)

24. Une fois le fichier chargé, il s’affiche dans le volet de droite. Cliquez dessus pour l’ouvrir dans l’éditeur de **fonctions** . Elle doit ressembler **exactement** à l’image suivante.

    ![fonction personnalisée](images/AzureLabs-Lab313-68.png)

25. À ce stade, il serait judicieux de tester la capacité de votre fonction à stocker le message sur votre *table*. Dans la partie supérieure droite de la fenêtre, cliquez sur **test**.

    ![fonction personnalisée](images/AzureLabs-Lab313-69.png)

26. Insérez un message dans le **corps**de la demande, comme indiqué dans l’image ci-dessus, puis cliquez sur **exécuter**. 

27. La fonction s’exécute et affiche l’état du résultat (vous remarquerez que l' **état vert 202 est accepté**, au-dessus de la fenêtre *sortie* , ce qui signifie qu’il s’agit d’un appel réussi):

    ![résultat de sortie](images/AzureLabs-Lab313-70.png)

## <a name="chapter-14---view-active-messages"></a>Chapitre 14-afficher les messages actifs

Si vous ouvrez maintenant Visual Studio (**pas** Visual Studio code), vous pouvez visualiser le résultat de votre message de test, car il sera stocké dans la zone de chaîne *MessageContent* .

![fonction personnalisée](images/AzureLabs-Lab313-71.png)

Une fois le service de table et le Function App en place, vos messages d’appareil Ubuntu s’affichent dans votre table *IoTMessages* . S’il n’est pas déjà en cours d’exécution, redémarrez votre appareil et vous pourrez voir les messages de résultats de votre appareil et du module dans votre table, à l’aide de Visual Studio *Cloud Explorer*.

![Visualiser les données](images/AzureLabs-Lab313-72.png)


## <a name="chapter-15---power-bi-setup"></a>Chapitre 15-configuration de Power BI

Pour visualiser les données de votre appareil IOT, vous allez configurer **Power bi** (version de bureau) pour collecter les données à partir du service de *table* , que vous venez de créer. La version *HoloLens* de Power bi utilisera ensuite ces données pour visualiser le résultat.

1.  Ouvrez la Microsoft Store sur Windows 10 et recherchez **Power bi Desktop**.

    ![Power BI](images/AzureLabs-Lab313-73.png)

2.  Téléchargez l’application. Une fois le téléchargement terminé, ouvrez-le.

3.  Connectez-vous à *Power bi* avec votre **compte Microsoft 365**. Vous pouvez être redirigé vers un navigateur pour vous inscrire. Une fois que vous êtes inscrit, revenez à l’application Power BI, puis reconnectez-vous.

4.  Cliquez sur **obtenir des données** , puis cliquez sur **plus...** .

    ![Power BI](images/AzureLabs-Lab313-74.png)

5.  Cliquez sur **Azure**, **stockage table Azure**, puis sur **se connecter**.

    ![Power BI](images/AzureLabs-Lab313-75.png)

6.  Vous serez invité à insérer l’URL de **table** que vous avez collectée précédemment ([à l’étape 13 du chapitre 11](#chapter-11---create-table-service)), lors de la création de votre service de table. Après avoir inséré l’URL, supprimez la partie du chemin d’accès qui fait référence au sous-dossier de la table (qui était IoTMessages, dans ce cours). Le résultat final doit être affiché dans l’image ci-dessous. Cliquez ensuite sur **OK**.

    ![Power BI](images/AzureLabs-Lab313-76.png)

7.  Vous serez invité à insérer la clé de **stockage** que vous avez notée ([à l’étape 11 du chapitre 11](#chapter-11---create-table-service)) plus tôt lors de la création de votre stockage de table. Cliquez ensuite sur **se connecter**.

    ![Power BI](images/AzureLabs-Lab313-77.png)  

8. Un **panneau de navigation** s’affiche. cochez la case en regard de votre table, puis cliquez sur **charger**.

    ![Power BI](images/AzureLabs-Lab313-78.png)  

9. Votre table est maintenant chargée sur Power BI, mais elle nécessite une requête pour afficher les valeurs qu’elle contient. Pour ce faire, cliquez avec le bouton droit sur le nom de la table situé dans le **volet champs** sur le côté droit de l’écran. Cliquez ensuite sur **modifier la requête**.

    ![Power BI](images/AzureLabs-Lab313-79.png) 

10. Un **éditeur de Power Query** s’ouvre en tant que nouvelle fenêtre, affichant votre tableau. Cliquez sur l' **enregistrement** Word dans la colonne *contenu* de la table pour visualiser le contenu stocké.

    ![Power BI](images/AzureLabs-Lab313-80.png)    

11. Cliquez sur dans le **tableau**, en haut à gauche de la fenêtre. 

    ![Power BI](images/AzureLabs-Lab313-81.png)

12. Cliquez sur **fermer & appliquer**.

    ![Power BI](images/AzureLabs-Lab313-82.png)

13. Une fois que le chargement de la requête est terminé, dans le **volet champs**, sur le côté droit de l’écran, cochez les cases correspondant aux paramètres **nom** et **valeur**, pour visualiser le contenu de la colonne **MessageContent** .

    ![Power BI](images/AzureLabs-Lab313-83.png)

14. Cliquez sur l' **icône de disque bleu** en haut à gauche de la fenêtre pour enregistrer votre travail dans un dossier de votre choix.

    ![Power BI](images/AzureLabs-Lab313-84.png)

15. Vous pouvez maintenant cliquer sur le bouton publier pour charger votre table dans votre espace de travail. Lorsque vous y êtes invité, cliquez sur **mon espace de travail** , puis sur *Sélectionner*. Attendez qu’il affiche le résultat réussi de la soumission.

    ![Power BI](images/AzureLabs-Lab313-85.png)

    ![Power BI](images/AzureLabs-Lab313-86.png)

> [!WARNING]
> Le chapitre suivant est spécifique à HoloLens. Power BI n’est actuellement pas disponible en tant qu’application immersif, vous pouvez néanmoins exécuter la version de bureau dans le portail Windows Mixed Reality (également appelé maison), à l’aide de l’application de bureau.

## <a name="chapter-16---display-power-bi-data-on-hololens"></a>Chapitre 16-afficher les données de Power BI sur HoloLens

1. Sur votre HoloLens, connectez-vous au **Microsoft Store**, en appuyant sur son icône dans la liste des applications.

    ![Power BI HL](images/AzureLabs-Lab313-87.png)

2. Recherchez, puis téléchargez l’application **Power bi** .

    ![Power BI HL](images/AzureLabs-Lab313-88.png)

3. Démarrez **Power bi** à partir de votre liste d’applications. 

4. **Power bi** pouvez vous demander de vous connecter à votre **compte Microsoft 365**.

5. Une fois à l’intérieur de l’application, l’espace de travail doit s’afficher par défaut comme indiqué dans l’image ci-dessous. Si cela ne se produit pas, cliquez simplement sur l’icône de l’espace de travail sur le côté gauche de la fenêtre.

    ![Power BI HL](images/AzureLabs-Lab313-89.png)

## <a name="your-finished-your-iot-hub-application"></a>Votre application IoT Hub est terminée

Félicitations, vous avez créé avec succès un service IoT Hub, avec un appareil de périphérie de machine virtuelle simulé. Votre appareil peut communiquer les résultats d’un modèle de Machine Learning à un service de table Azure, facilité par un Function App Azure, qui est lu dans Power BI et visualisé dans un Microsoft HoloLens.
 
![Power BI](images/AzureLabs-Lab313-00.png)

## <a name="bonus-exercises"></a>Exercices bonus

### <a name="exercise-1"></a>Exercice 1

Développez la structure de messagerie stockée dans la table et affichez-la sous forme de graphique. Vous souhaiterez peut-être collecter davantage de données et les stocker dans la même table, pour les afficher ultérieurement.

### <a name="exercise-2"></a>Exercice 2

Créez un module «capture d’appareil photo» supplémentaire à déployer sur le tableau IoT, afin qu’il puisse capturer des images via l’appareil photo à analyser.
