---
title: MR et Azure 313 - Service IoT Hub
description: Terminer ce cours pour apprendre à implémenter le Service Azure IoT Hub sur une machine virtuelle exécutant Ubuntu 16.4 et puis visualiser les données de message à l’aide de Microsoft HoloLens ou un casque (VR) immersif.
author: drneil
ms.author: jemccull
ms.date: 07/11/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, edge, iot edge, didacticiel, api, notification, fonctions, tables, hololens, immersives, vr, iot, machine virtuelle, ubuntu, python
ms.openlocfilehash: 1ab7c48ac3cff1cb2283cadb171098af9e148628
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593254"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

# <a name="mr-and-azure-313-iot-hub-service"></a>MR et Azure 313 : Service IoT Hub

![résultat de cours](images/AzureLabs-Lab313-00.png)

Dans ce cours, vous allez apprendre à implémenter un **Service Azure IoT Hub** sur une machine virtuelle exécutant le système d’exploitation Ubuntu 16.4. Un **Azure Function App** servira pour recevoir des messages à partir de votre VM Ubuntu et stocker le résultat dans un **Service de Table Azure**. Vous serez ensuite en mesure d’afficher ce à l’aide de données **Power BI** sur Microsoft HoloLens ou immersif casque (VR).

Le contenu de ce cours *est applicable* pour les appareils IoT Edge, bien que pour les besoins de ce cours, le focus sera dans un environnement de machine virtuelle, afin que l’accès à un périphérique de périmètre physique n’est pas nécessaire.

En fin de ce didacticiel, vous allez apprendre à :

- Déployer un **module IoT Edge** à une Machine virtuelle (Ubuntu 16 OS), qui représentera votre appareil IoT.
- Ajouter un **Azure Custom Vision Tensorflow modèle** pour le module de Edge avec du code qui analysera les images stockées dans le conteneur.
- Configurer le module pour envoyer le message de résultat d’analyse à votre **Service IoT Hub**.
- Utilisez un **Azure Function App** pour stocker le message dans une **Table Azure**.
- Configurer **Power BI** pour collecter les messages stocké et créer un rapport.
- Visualisez vos données de message IoT dans **Power BI**.

Les Services que vous allez utiliser sont les suivantes :

- **Azure IoT Hub** est un Service Microsoft Azure, ce qui permet aux développeurs de se connecter, surveiller et gérer des ressources IoT. Pour plus d’informations, visitez le [ **Service Azure IoT Hub** page](https://azure.microsoft.com/en-au/services/iot-hub/).

- **Azure Container Registry** est un Service Microsoft Azure, ce qui permet aux développeurs de stocker les images de conteneur pour différents types de conteneurs. Pour plus d’informations, visitez le [ **le Registre Azure Container Service** page](https://azure.microsoft.com/en-au/services/container-registry/).

- **Azure Function App** est un Service Microsoft Azure, ce qui permet aux développeurs d’exécuter de petits morceaux de code, « fonctions », dans Azure. Cela fournit un moyen permettant de déléguer le cloud, plutôt que votre application locale, ce qui peut avoir de nombreux avantages. **Azure Functions** prend en charge plusieurs langages de développement, y compris C\#, F\#, Node.js, Java et PHP. Pour plus d’informations, visitez le [ **Azure Functions** page](https://docs.microsoft.com/azure/azure-functions/functions-overview).

- **Stockage Azure : Tables** est un Microsoft Azure Service, ce qui permet aux développeurs de stocker structurées, non SQL, les données dans le cloud, rendant facilement accessibles n’importe où. Le Service possède une conception sans schéma, permettant ainsi l’évolution des tables en fonction des besoins et il est donc très flexible. Pour plus d’informations, visitez le [ **Tables Azure** page](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)

Ce cours va vous apprendre à configurer et utiliser le Service IoT Hub et ensuite visualiser une réponse fournie par un appareil. Il le sera jusqu'à vous permettent d’appliquer ces concepts à une installation de Service IoT Hub personnalisée, vous voudrez peut-être générer.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td> MR et Azure 313 : Service IoT Hub</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="prerequisites"></a>Prérequis

Pour les conditions préalables plus récentes pour le développement avec la réalité mixte, notamment avec le Microsoft HoloLens, visitez le [installer les outils](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) article.

> [!NOTE]
> Ce didacticiel est conçu pour les développeurs qui ont une expérience de base avec Python. Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018). Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récente que celle ci-dessous.

Les matériels et logiciels suivants sont requises :

- Windows 10 Fall Creators Update (ou version ultérieure), **Mode développeur est activé**

    > [!WARNING]
    > Vous ne pouvez pas exécuter une Machine virtuelle à l’aide de Hyper-V sur Windows 10 Édition familiale.

- SDK Windows 10 (version la plus récente)
- Un HoloLens, **Mode développeur est activé**
- Visual Studio 2017.15.4 (utilisé uniquement pour accéder à l’Explorateur de Cloud Azure)
- L’accès à Internet pour Azure et pour le Service IoT Hub. Pour plus d’informations, veuillez suivre ce [lien vers la page du Service IoT Hub](https://azure.microsoft.com/en-au/services/iot-hub/)
- Un modèle d’apprentissage automatique. Si vous n’avez pas votre propre prêtes à l’emploi de modèle, [vous pouvez utiliser le modèle fourni avec ce cours](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip).
- **Hyper-V** logiciel est activé sur votre ordinateur de développement Windows 10.
- Une Machine virtuelle exécutant Ubuntu (16.4 ou 18.4), en cours d’exécution sur votre ordinateur de développement, ou vous pouvez également vous pouvez utiliser un ordinateur distinct exécutant Linux (Ubuntu 16.4 ou 18.4). Vous trouverez plus d’informations sur la façon de créer une machine virtuelle sur Windows à l’aide de Hyper-V dans le [« Avant de commencer » de chapitre](#before-you-start). () https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine).  



### <a name="before-you-start"></a>Avant de commencer

1. Configurer et tester votre HoloLens. Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup).
2. Il est judicieux d’effectuer **étalonnage** et **capteur réglage** lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur).

Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).

Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).

3. Configurer votre **Machine virtuelle Ubuntu** à l’aide de **Hyper-V**. Les ressources suivantes vous aideront avec le processus.
    1.  Tout d’abord, suivez ce lien pour [télécharger le fichier ISO Ubuntu 16.04.4 LTS (Xenial Xerus)](http://au.releases.ubuntu.com/16.04/). Sélectionnez le **image de bureau de PC (AMD64) 64 bits**.
    2.  Assurez-vous que **Hyper-V** est activée sur votre ordinateur Windows 10. Vous pouvez suivre ce lien pour obtenir des conseils sur [installation et l’activation d’Hyper-V sur Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).
    3.  Démarrer Hyper-V et créer une nouvelle VM Ubuntu. Vous pouvez suivre ce lien pour une [guide étape par étape sur la façon de créer une machine virtuelle avec Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine). Lorsque la demande est **« Installer un système d’exploitation à partir d’un fichier image de démarrage »**, sélectionnez le **ISO Ubuntu** avoir téléchargement précédemment.

    > [!NOTE]
    > À l’aide de **création rapide Hyper-V** n’est pas conseillée.  

## <a name="chapter-1---retrieve-the-custom-vision-model"></a>Chapitre 1 : récupérer le modèle de Vision personnalisée

Grâce à ce cours, vous aurez accès à un [modèle de Vision personnalisée avant génération](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip) qui détecte des claviers et des souris à partir d’images. Si vous utilisez cette option, passez à [chapitre 2](#chapter-2---the-container-registry-service).

Toutefois, vous pouvez suivre ces étapes si vous souhaitez utiliser votre propre modèle de Vision personnalisée :

1. Dans votre **Custom Vision Project** accédez à la **performances** onglet.

    > [!WARNING]
    > Votre modèle doit utiliser un *compact* domaine, pour exporter le modèle. Vous pouvez modifier votre domaine de modèles dans les paramètres de votre projet.

    ![onglet performances](images/AzureLabs-Lab313-01.png)

2. Sélectionnez le **itération** vous souhaitez exporter, puis cliquez sur **exporter**. Un panneau s’affiche.

    ![panneau d’exportation](images/AzureLabs-Lab313-02.png)

3. Dans le panneau, cliquez sur **fichier Docker**.

    ![Sélectionnez docker](images/AzureLabs-Lab313-03.png)

4. Cliquez sur **Linux** dans le menu déroulant et puis cliquez sur **télécharger**.

    ![Cliquez sur Télécharger](images/AzureLabs-Lab313-04.png)

5. Décompressez le contenu. Vous l’utiliserez plus loin dans ce cours.

## <a name="chapter-2---the-container-registry-service"></a>Chapitre 2 - le Service de Registre de conteneur

Le **Service de Registre de conteneur** est le référentiel utilisé pour héberger vos conteneurs.

Le **Service IoT Hub** laquelle générer et utiliser dans ce cours, fait référence à **Service de Registre de conteneur** pour obtenir les conteneurs à déployer dans votre appareil Edge.

1. Tout d’abord, suivez ce [lien vers le portail Azure](https://portal.azure.com/)et connectez-vous avec vos informations d’identification.

2. Accédez à **créer une ressource** et recherchez **Registre de conteneurs**.

    ![Registre de conteneurs](images/AzureLabs-Lab313-05.png)

3. Cliquez sur **créer**.

    ![](images/AzureLabs-Lab313-06.png)

4. Configurer le Service de paramètres d’installation :

    1. Insérez un nom pour votre projet, dans cet exemple ses appelée **IoTCRegistry**.

    2. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, de contrôler l’accès, disposition et de gérer, de facturation pour une collection de ressources Azure. Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).

    3. Définissez l’emplacement du Service.

    4. Définissez **utilisateur_administrateur** à **activer**.

    5. Définissez **référence (SKU)** à **base**. 

    ![](images/AzureLabs-Lab313-07.png)

5. Cliquez sur **créer** et attendez que les Services doit être créé. 

6. Une fois que la notification s’affiche vous informant de la création réussie de la *Registre de conteneurs*, cliquez sur **accéder à la ressource** d’être redirigé vers la page de votre Service.

    ![](images/AzureLabs-Lab313-08.png)

7. Dans le *Registre de conteneurs* page des services, cliquez sur **clés d’accès**.

8. Prenez note (vous pouvez utiliser votre bloc-notes) des paramètres suivants :
    1. **Serveur de connexion**
    2. **Nom d’utilisateur**
    3. **Mot de passe**

    ![](images/AzureLabs-Lab313-09.png)

## <a name="chapter-3---the-iot-hub-service"></a>Chapitre 3 - le Service IoT Hub

Maintenant vous allez commencer la création et la configuration de votre **Service IoT Hub**.

1. Si pas déjà connecté, connectez-vous à la [Azure Portal](https://portal.azure.com).

2.  Une fois connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche coin inférieur droit, puis recherchez **IoT Hub**, puis cliquez sur **entrée**.

 ![Recherchez le compte de stockage](images/AzureLabs-Lab313-10.png)

3.  La nouvelle page doit fournir une description de la **compte de stockage** Service. En bas à gauche de cette invite, cliquez sur le **créer** bouton, pour créer une instance de ce Service.

    ![créer l’instance de stockage](images/AzureLabs-Lab313-11.png)

4.  Une fois que vous avez cliqué sur **créer**, un panneau s’affiche :

    1. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure. Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).


    2. Sélectionnez un **emplacement** (utilisez le même emplacement pour tous les Services que vous créez dans ce cours).

    3. Insérez votre souhaitée **nom** pour cette instance de Service.    

5.  En bas de la page, cliquez sur **suivant : Taille et échelle**.

    ![créer l’instance de stockage](images/AzureLabs-Lab313-12.png)

6.  Dans cette page, sélectionnez votre **niveau de tarification et mise à l’échelle** (s’il s’agit de votre première instance de Service IoT Hub, une version gratuite doit être disponible pour vous).  

7.  Cliquez sur **vérifier + créer**.

    ![créer l’instance de stockage](images/AzureLabs-Lab313-13.png)

8.  Passez en revue vos paramètres, puis cliquez sur **créer**.

    ![créer l’instance de stockage](images/AzureLabs-Lab313-14.png)

9. Une fois que la notification s’affiche vous informant de la création réussie de la *IoT Hub* Service, cliquez sur **accéder à la ressource** d’être redirigé vers la page de votre Service.

    ![créer l’instance de stockage](images/AzureLabs-Lab313-15.png)

10. Faites défiler le panneau latéral gauche jusqu'à ce que vous voyiez *gestion automatique des appareils*, cliquez sur **IoT Edge**.

    ![créer l’instance de stockage](images/AzureLabs-Lab313-16.png)

11. Dans la fenêtre qui apparaît à droite, cliquez sur **ajouter un appareil IoT Edge**. Un panneau s’affiche à droite.

12. Dans le panneau, fournir votre nouvel appareil un **ID d’appareil** (il s’agit d’un nom de votre choix). Ensuite, cliquez sur **enregistrer**. Le *principal* et *clés secondaires* auto génère, si vous avez **générer automatiquement** coché.

    ![créer l’instance de stockage](images/AzureLabs-Lab313-17.png)

13. Vous permet d’accéder à la *appareils IoT Edge* section, dans laquelle votre nouvel appareil est répertoriée. Cliquez sur votre nouvel appareil (entourée en rouge dans l’image ci-dessous). 

    ![créer l’instance de stockage](images/AzureLabs-Lab313-18.png)

14. Sur le *détails de l’appareil* page qui s’affiche, effectuez une copie de la **chaîne de connexion** (clé primaire).

    ![créer l’instance de stockage](images/AzureLabs-Lab313-19.png)

15. Revenez au panneau sur la gauche, puis cliquez sur *stratégies d’accès partagé*, pour l’ouvrir. 

16. Dans la page qui s’affiche, cliquez sur **iothubowner**, et un panneau s’affiche à droite de l’écran. 

17. Prenez note (sur votre bloc-notes) de la **chaîne de connexion** (clé primaire), pour une utilisation ultérieure lors de la définition du *chaîne de connexion* à votre appareil.

    ![créer l’instance de stockage](images/AzureLabs-Lab313-20.png)

## <a name="chapter-4---setting-up-the-development-environment"></a>Chapitre 4 - Configuration de l’environnement de développement

Pour créer et déployer des modules pour *IoT Hub Edge*, vous aurez besoin des composants suivants sur votre ordinateur de développement exécutant Windows 10 :

1.  [Docker pour Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows), il vous sera demandé de créer un compte pour pouvoir télécharger. 

    [![téléchargement de docker pour windows](images/AzureLabs-Lab313-21.png)](https://store.docker.com/editions/community/docker-ce-desktop-windows)

    > [!IMPORTANT]
    > Nécessite docker *Windows 10 PRO*, *Enterprise 14393*, ou *Windows Server 2016 RTM*, à exécuter. Si d’autres versions de Windows 10 sont en cours d’exécution, vous pouvez essayer d’installer Docker en utilisant le [boîte à outils Docker](https://docs.docker.com/toolbox/toolbox_install_windows/).

2.  [Python 3.6](https://www.python.org/downloads/).

    [![Téléchargez python 3.6](images/AzureLabs-Lab313-22.png)](https://www.python.org/downloads/)

3.  [Visual Studio Code (également appelé VS Code)](https://code.visualstudio.com/download).

    [![Télécharger Visual Studio Code](images/AzureLabs-Lab313-23.png)](https://code.visualstudio.com/download)

Après avoir installé le logiciel mentionné ci-dessus, vous devrez redémarrer votre ordinateur.

## <a name="chapter-5---setting-up-the-ubuntu-environment"></a>Chapitre 5 : configuration de l’environnement Ubuntu

Maintenant vous pouvez passer à la configuration de votre appareil **en cours d’exécution du système d’exploitation Ubuntu**. Suivez les étapes ci-dessous pour installer le logiciel nécessaire, pour déployer vos conteneurs sur votre carte :

> [!IMPORTANT]
> Vous devez toujours faire précéder les commandes terminal avec **sudo** à exécuter en tant qu’utilisateur administrateur. ex :
> 
>   ```bash
>   sudo docker \<option> \<command> \<argument>
>   ```

1.  Ouvrez le **Ubuntu Terminal**et utilisez la commande suivante pour installer **pip**:

    > [! Conseil] vous pouvez ouvrir *Terminal* très facilement à l’aide du raccourci clavier : **Ctrl + Alt + T**.

    ```bash
        sudo apt-get install python-pip
    ```

2.  Tout au long de ce chapitre, vous pouvez être invité, par *Terminal*d’autorisation d’utilisation du stockage de l’appareil et vous saisissiez **o/n** (Oui ou non), type **'y'**, puis appuyez sur la **Entrée** clé, à accepter.

3.  Une fois cette commande terminée, utilisez la commande suivante pour installer **curl**:

    ```bash
        sudo apt install curl
    ```

4.  Une fois **pip** et **curl** sont installés, utilisez la commande suivante pour installer le **runtime IoT Edge**, cela est nécessaire pour déployer et contrôler les modules sur votre carte :

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

5. À ce stade vous êtes invité à ouvrir le *fichier de configuration de runtime*, pour insérer le **Device Connection String**, que vous avez notée (dans votre bloc-notes), lors de la création du **Service IoT Hub**  ([à l’étape 14, du chapitre 3](#chapter-3---the-iot-hub-service)). Exécutez la ligne suivante dans le terminal pour ouvrir ce fichier :

    ```bash
        sudo nano /etc/iotedge/config.yaml
    ```

6. Le **config.yaml** fichier sera affichée, vous pouvez modifier :

    > [!WARNING]
    > Lorsque ce fichier s’ouvre, il peut être prêter à confusion. Vous serez dans ce fichier, l’édition de texte le *Terminal* lui-même. 

    1.  Utilisez les touches de direction de votre clavier pour faire défiler vers le bas (vous devez faire défiler de façon un peu) pour atteindre la ligne contenant « :

        "**\<AJOUTER ICI DEVICE CONNECTION STRING &GT;**".

    2. Remplacez la ligne, **y compris les crochets**, avec le **Device Connection String** que vous avez noté précédemment.

7. Avec votre chaîne de connexion en place, sur votre clavier, appuyez sur la **Ctrl-X** clés pour enregistrer le fichier. Il vous demandera de confirmer en tapant **Y**. Ensuite, appuyez sur la **entrée** clé, pour confirmer. Vous revenez à la mise à jour *Terminal*. 

8. Une fois que ces commandes ont tous exécuté avec succès, vous avez installé le **Runtime de IoT Edge**. Une fois initialisé, le runtime démarre sur son propre chaque fois que l’appareil est mis sous tension et sera placé dans l’arrière-plan, en attente pour les modules à déployer à partir de la **Service IoT Hub**.

9.  Exécuter la ligne de commande suivante pour initialiser le *Runtime de IoT Edge*:

    ```bash
        sudo systemctl restart iotedge
    ```

    > [!IMPORTANT]
    > Si vous apportez des modifications à votre fichier .yaml ou la configuration ci-dessus, vous devez réexécuter la ligne de redémarrage ci-dessus, au sein de *Terminal*.

10. Vérifier le *Runtime de IoT Edge* état en exécutant la ligne de commande suivante. Le runtime doit apparaître avec l’état **actif (en cours d’exécution)** en vert.

    ```bash
        sudo systemctl status iotedge
    ```

11. Appuyez sur la **Ctrl-C** clés, pour quitter la page d’état. Vous pouvez vérifier que le *Runtime de IoT Edge* extrait les conteneurs correctement en tapant la commande suivante :

    ```bash
        sudo docker ps
    ```

12. Une liste avec des conteneurs de deux (2) doit apparaître. Il s’agit de modules par défaut qui sont automatiquement créés par le Service IoT Hub (edgeAgent et edgeHub). Une fois que vous créez et déployez vos propres modules, ils apparaîtront dans cette liste, en dessous de celles par défaut.

## <a name="chapter-6---install-the-extensions"></a>Chapitre 6 : installer les extensions

> [!IMPORTANT]
> Les chapitres suivants (6-9) ne doivent être exécutées sur votre ordinateur Windows 10.

1. Ouvrez **VS Code**.

2. Cliquez sur le **Extensions** bouton (carré) sur la gauche de VS Code barres, pour ouvrir le **panneau Extensions**.

3. Rechercher et installer les extensions suivantes (comme indiqué dans l’image ci-dessous) :

    1. Azure IoT Edge
    2. Kit de ressources Azure IoT
    3. Docker   

    ![Créez votre conteneur](images/AzureLabs-Lab313-24.png)

4. Une fois que les extensions sont installées, fermez et rouvrez VS Code.

5. Avec VS Code, ouvrez une fois de plus, accédez à **Affichage > terminal intégré**.

6. Vous allez maintenant installer **Cookiecutter**. Dans le terminal, exécutez la commande bash suivante :

    ```bash
        pip install --upgrade --user cookiecutter
    ```

    > [! Conseil] Si vous rencontrez des difficultés avec cette commande : 
    >1. Redémarrez VS Code, et / ou votre ordinateur.
    >2. Il peut être nécessaire de basculer le **VS Code Terminal** à celle que vous avez utilisé pour installer Python, par exemple, **Powershell** (en particulier au cas où l’environnement Python a déjà été installée sur votre ordinateur). Le Terminal ouvert, vous trouverez la liste déroulante sur le côté droit du Terminal.
     ![Créez votre conteneur](images/AzureLabs-Lab313-24b.png) 
    >3. Assurez-vous que le **Python** chemin d’installation est ajouté en tant que **Variable d’environnement** sur votre ordinateur. Cookiecutter doit faire partie de la même chemin d’accès d’emplacement. Veuillez suivre ce [lien pour plus d’informations sur les Variables d’environnement](https://msdn.microsoft.com/library/windows/desktop/ms682653(v=vs.85).aspx), 

7. Une fois **Cookiecutter** a terminé l’installation, vous devez redémarrer votre ordinateur, afin que **Cookiecutter** est reconnu comme une commande, au sein de l’environnement de votre système.

## <a name="chapter-7---create-your-container-solution"></a>Chapitre 7 - créer votre solution de conteneurs

À ce stade, vous devez créer le conteneur, avec le module, pour être placé dans le *Registre de conteneurs*. Une fois que vous avez envoyé votre conteneur, vous allez utiliser le *IoT Hub Edge* Service à la déployer sur votre appareil, ce qui est en cours d’exécution le *runtime IoT Edge*.

1. À partir du Code de Visual Studio, cliquez sur **vue > palette de commandes**.

2. Dans la palette, rechercher et exécuter **Azure IoT Edge : Nouvelle Solution Iot Edge**.

3. Naviguer dans un emplacement où vous souhaitez créer votre solution. Appuyez sur la **entrée** clé, pour accepter l’emplacement.

4. Donnez un nom à votre solution. Appuyez sur la **entrée** clé, pour confirmer votre nom fourni.

5. Vous devez maintenant choisir le framework de modèle pour votre solution. Cliquez sur **Module Python**. Appuyez sur la **entrée** clé, pour confirmer ce choix.

6. Donnez un nom à votre module. Appuyez sur la **entrée** clé, pour confirmer le nom de votre module. Veillez à prendre note (avec votre bloc-notes) du nom du module, comme nous l’utiliserons ultérieurement.

7. Vous pouvez remarquer un prédéfinis *référentiel d’images Docker* adresse apparaîtra dans la palette. Il doit ressembler :

    **localhost:5000 /-nom de votre MODULE -**. 

8. Supprimer **localhost:5000**et dans son insertion place le *Container Registry* **serveur de connexion** adresse que vous avez notée lors de la création du **conteneur Service de Registre** ([à l’étape 8, chapitre 2](#chapter-2---the-container-registry-service)). Appuyez sur la **entrée** clé, pour confirmer l’adresse.

9. À ce stade, la solution qui contient le modèle pour votre module Python sera créée et sa structure s’affichera dans le **onglet Explorer**, de Visual Studio Code, sur le côté gauche de l’écran. Si le **onglet Explorer** est pas ouverte, vous pouvez l’ouvrir en cliquant sur le bouton le plus haut, dans la barre de gauche.

    ![Créez votre conteneur](images/AzureLabs-Lab313-25.png)

10. La dernière étape de ce chapitre, est de cliquer sur et ouvrez le **fichier .env**, depuis le **onglet Explorer**et ajoutez votre *Registre de conteneurs* **nom d’utilisateur** et **mot de passe**. Ce fichier est ignoré par git, mais sur la création du conteneur, définit les informations d’identification pour accéder à la **Service de Registre de conteneur**.

    ![Créez votre conteneur](images/AzureLabs-Lab313-26.png)

## <a name="chapter-8---editing-your-container-solution"></a>Chapitre 8 - modification de votre solution de conteneurs

Vous allez maintenant effectuer la solution de conteneur, en mettant à jour les fichiers suivants :

- *principal<span></span>.py* script python.
- *requirements.txt*.
- *deployment.template.json*.
- *Dockerfile.amd64*

Vous allez ensuite créer le *images* dossier, utilisé par le script python pour rechercher les images à mettre en correspondance votre *modèle de Vision personnalisée*. Enfin, vous allez ajouter le *labels.txt* fichier, pour aider à lire votre modèle et le *model.pb* fichier, qui est votre modèle.

1. Avec VS Code ouvrir, accédez à votre dossier de module et recherchez le script appelé **principal<span></span>.py**. Double-cliquez pour l’ouvrir.

2. Supprimer le contenu du fichier et insérez le code suivant :

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

3.  Ouvrez le fichier appelé **requirements.txt**, puis remplacez son contenu par le code suivant :

    ```
    azure-iothub-device-client==1.4.0.0b3
    opencv-python==3.3.1.11
    tensorflow==1.8.0
    pillow==5.1.0
    ```

4.  Ouvrez le fichier appelé **deployment.template.json**, puis remplacez son contenu suivant le ci-dessous indication :

    1. Étant donné que vous avez votre propre, unique, structure JSON, vous devrez modifier manuellement (au lieu de copier un exemple). Pour faciliter la tâche, utilisez l’image en tant que guide ci-dessous.
    2. Les zones qui aura un aspect différents à la vôtre, mais que vous **ne devez pas modifier sont mis en surbrillance jaune**.
    3. **Les sections dont vous avez besoin à supprimer, sont mis en surbrillance rouge.**
    4. Veillez à supprimer les crochets corrects et également supprimer les virgules.

        ![Créez votre conteneur](images/AzureLabs-Lab313-27.png)

    5. Le JSON terminé doit ressembler à l’image suivante (Cependant, avec votre différences uniques : *références de nom d’utilisateur/mot de passe/nom/un module*) :

        ![Créez votre conteneur](images/AzureLabs-Lab313-28.png)

5.  Ouvrez le fichier appelé **Dockerfile.amd64**, puis remplacez son contenu par le code suivant :

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

6.  Avec le bouton droit sur le dossier sous **modules** (il aura le nom que vous avez fourni précédemment ; dans l’exemple vers le bas, il est appelé *pythonmodule*), puis cliquez sur **nouveau dossier**. Nommez le dossier **images**.

7.  Dans le dossier, ajouter des images contenant la souris ou le clavier. Ceux-ci seront les images qui seront analysées par le modèle Tensorflow.

    > [!WARNING]
    > Si vous utilisez votre propre modèle, vous devez modifier pour refléter vos propres données de modèles.

8.  Vous devez maintenant récupérer le **labels.txt** et **model.pb** à partir du dossier de modèle que vous avez téléchargé les fichiers (ou créé à partir de votre propre **Service Vision personnalisée** ), dans [chapitre 1](#chapter-1---retrieve-the-custom-vision-model). Une fois que vous disposez des fichiers, les placer dans votre solution, en même temps que les autres fichiers. Le résultat final doit ressembler à l’image ci-dessous :

    ![Créez votre conteneur](images/AzureLabs-Lab313-29.png)

## <a name="chapter-9---package-the-solution-as-a-container"></a>Chapitre 9 - Package de la solution en tant que conteneur

1.  Vous êtes maintenant prêt à « package » de vos fichiers en tant que conteneur et les distribuer à vos **Azure Container Registry**. Dans VS Code, ouvrez le *Terminal intégré* (**Affichage > Terminal intégré / CTRL + '**) et utilisez la ligne suivante pour vous connecter à **Docker** (remplacez les valeurs de la commande avec les informations d’identification de votre **Azure Container Registry (ACR)**) :

    ```bash
        docker login -u <ACR username> -p <ACR password> <ACR login server>
    ```

2. Avec le bouton droit sur le fichier **deployment.template.json**, puis cliquez sur **générer la Solution IoT Edge**. Ce processus de génération prend un certain temps (en fonction de votre appareil), préparez-vous à attendre. Une fois le processus de génération est terminée, un **Deployment.JSON ainsi** fichier sera créé à l’intérieur d’un nouveau dossier appelé **config**.

    ![créer un déploiement](images/AzureLabs-Lab313-30.png)

3. Ouvrez le **Palette de commandes** à nouveau et recherchez **Azure : Connectez-vous**. Suivez les invites à l’aide de vos informations d’identification du compte Azure ; VS Code vous fournira une option permettant de *copier et ouvrir*, qui copiera le code de l’appareil vous aurez bientôt besoin et ouvrez votre navigateur web. Lorsque vous êtes invité, collez le code de l’appareil, pour authentifier votre ordinateur.

    ![copier et ouvrir](images/AzureLabs-Lab313-31.png)

4. Une fois signé en vous remarquerez, sur le côté inférieur de la *Explorer* panneau, une nouvelle section appelée **appareils Azure IoT Hub**. Cliquez sur cette section pour la développer.

    ![APPAREIL Edge](images/AzureLabs-Lab313-32.png)

5. Si votre appareil n’est pas ici, vous devrez avec le bouton droit *appareils Azure IoT Hub*, puis cliquez sur **définir la chaîne de connexion IoT Hub**. Vous verrez ensuite que le **Palette de commandes** (en haut de VS Code), vous invitera à entrer votre *chaîne de connexion*. Il s’agit du *chaîne de connexion* que vous avez noté à la fin de [chapitre 3](#chapter-3---the-iot-hub-service). Appuyez sur la **entrée** de clé, une fois que vous avez copiée dans la chaîne de.    

6. Votre appareil doit charger et s’affichent. Avec le bouton droit sur le nom du périphérique, puis cliquez sur, **créer un déploiement pour un seul appareil**.

    ![créer un déploiement](images/AzureLabs-Lab313-33b.png)

7. Vous obtiendrez un *Explorateur de fichiers* invite, où vous pouvez accéder à la **config** dossier, puis sélectionnez le **Deployment.JSON ainsi** fichier. Ce fichier est sélectionné, cliquez sur le **sélectionner un manifeste de déploiement Edge** bouton.

    ![créer un déploiement](images/AzureLabs-Lab313-34.png)

8. À ce stade, vous avez fourni votre **Service IoT Hub** avec le manifeste pour pouvoir déployer votre conteneur, en tant que module, à partir de votre **Azure Container Registry**, efficacement déployer sur votre appareil.

9. Pour afficher les messages envoyés à partir de votre appareil à IoT Hub, avec le bouton droit à nouveau sur le nom de votre appareil dans le **appareils Azure IoT Hub** section, dans le **Explorer** panneau, puis cliquez sur **démarrer l’analyse D2C Message**. Les messages envoyés à partir de votre appareil doivent apparaître dans le Terminal VS. Soyez patient, comme cela peut prendre un certain temps. Consultez le chapitre suivant pour le débogage et en vérifiant si le déploiement a réussi.

Ce module effectuera une itération maintenant entre les images dans le **images** dossier et les analyser, avec chaque itération. Il s’agit évidemment juste une démonstration illustrant comment obtenir le modèle de base de machine learning pour travailler dans un environnement d’appareil IoT Edge. 

Pour développer les fonctionnalités de cet exemple, peut procéder de plusieurs façons. Une façon pourrait être, y compris du code dans le conteneur, qui capture des photos à partir d’une webcam qui est connecté à l’appareil et enregistre les images dans le dossier images. 

Une autre façon pouvez copier les images à partir de l’appareil IoT dans le conteneur. Un moyen pratique de le faire consiste à exécuter la commande suivante dans l’appareil IoT Terminal Server (peut-être une petite application Impossible d’effectuer la tâche, si vous voulez automatiser le processus). Vous pouvez tester cette commande en exécutant manuellement à partir de l’emplacement du dossier où sont stockés vos fichiers :

```bash
    sudo docker cp <filename> <modulename>:/app/images/<a name of your choice>
```

## <a name="chapter-10---debugging-the-iot-edge-runtime"></a>Chapitre 10 - débogage du Runtime IoT Edge

Voici une liste des lignes de commande et obtenir des conseils, pour vous aider à surveiller et déboguer l’activité de messagerie de le *Runtime de IoT Edge*, à partir de votre **appareil Ubuntu**. 

- Vérifier le *Runtime de IoT Edge* état en exécutant la ligne de commande suivante :

    ```bash
        sudo systemctl status iotedge
    ```

    > [!NOTE]
    > N’oubliez pas d’appuyer sur **Ctrl + C**, pour terminer l’affichage de l’état.

- Répertorier les conteneurs qui sont actuellement déployées. Si le *Service IoT Hub* a déployé les conteneurs, ils seront affichés en exécutant la ligne de commande suivante :

    ```bash
        sudo iotedge list
    ```

    Ou

    ```bash
        sudo docker ps
    ```

    > [!NOTE]
    > La méthode ci-dessus est un bon moyen pour vérifier si votre module a été correctement déployé, tel qu’il apparaîtra dans la liste ; vous allez sinon **uniquement** voir le *edgeHub* et *edgeAgent*.

- Pour afficher les journaux de code d’un conteneur, exécutez la ligne de commande suivante :

    ```bash
        journalctl -u iotedge
    ```

**Commandes utiles pour gérer le Runtime IoT Edge :**

-  Pour supprimer tous les conteneurs dans l’hôte :

    ```bash
        sudo docker rm -f $(sudo docker ps -aq)
    ```

-  Pour arrêter la *Runtime de IoT Edge*:

    ```bash
        sudo systemctl stop iotedge
    ```

## <a name="chapter-11---create-table-service"></a>Chapitre 11 - créer le Service de Table 

Accédez à votre portail Azure, où vous allez créer un Service de Tables Azure, en créant une ressource de stockage.

1. Si pas déjà connecté, connectez-vous à la [Azure Portal](https://portal.azure.com).

2. Une fois connecté, cliquez sur **créer une ressource**, dans le coin supérieur gauche de coin et recherchez **compte de stockage**, puis appuyez sur la **entrée** clé, la recherche doit commencer.

3. Une fois que l’application s’affiche, cliquez sur **compte de stockage - blob, fichier, table, file d’attente** à partir de la liste.

    ![Recherchez le compte de stockage](images/AzureLabs-Lab313-35.png)

4. La nouvelle page doit fournir une description de la **compte de stockage** Service. En bas à gauche de cette invite, cliquez sur le **créer** bouton, pour créer une instance de ce Service.

    ![créer l’instance de stockage](images/AzureLabs-Lab313-36.png)

5. Une fois que vous avez cliqué sur **créer**, un panneau s’affiche :

    1. Insérez votre souhaitée **nom** pour cette instance de Service (*doit être en minuscules*).

    2. Pour **modèle de déploiement**, cliquez sur **Resource manager**.

    3. Pour **type de compte**, utilisez le menu déroulant, cliquez sur **stockage (usage général v1)**.

    4. Cliquez sur un texte approprié **emplacement**.
    
    5. Pour le **réplication** menu déroulant, cliquez sur **en lecture-access-geo-redundant storage (RA-GRS)**.

    6. Pour **performances**, cliquez sur **Standard**.

    7. Dans le **transfert sécurisé requis** , cliquez sur **désactivé**.

    8. À partir de la **abonnement** menu déroulant, cliquez sur un abonnement approprié.

    9. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, de contrôler l’accès, disposition et de gérer, de facturation pour une collection de ressources Azure. Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    10. Laissez **réseaux virtuels** comme **désactivé**, s’il s’agit d’une option pour vous.

    11. Cliquez sur **Create (Créer)**.

        ![Renseignez les détails de stockage](images/AzureLabs-Lab313-37.png)

6. Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.

7. Une fois que l’instance de Service est créée, une notification s’affiche dans le portail. Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.

    ![nouvelle notification de stockage](images/AzureLabs-Lab313-38.png)

8. Cliquez sur le **accéder à la ressource** bouton dans la notification et vous serez dirigé vers votre nouvelle page de vue d’ensemble d’instance Service de stockage.

    ![accéder à la ressource](images/AzureLabs-Lab313-39.png)

9. Dans la page Vue d’ensemble, à droite, cliquez sur **Tables**.
    
    ![Tables](images/AzureLabs-Lab313-40.png)

10. Le volet de droite change et indique le **Service de Table** plus d’informations, dans laquelle vous devez ajouter une nouvelle table. Cela en cliquant sur le **+ Table** bouton vers le coin supérieur gauche.

    ![ouvrir des Tables](images/AzureLabs-Lab313-41.png)

11. Une nouvelle page s’affiche, dans laquelle vous devez entrer un **nom de la Table**. Il s’agit du nom que vous utiliserez pour faire référence aux données dans votre application dans les chapitres (création d’application de fonction et Power BI). Insérer **IoTMessages** comme nom (vous pouvez choisir votre propre, n’oubliez pas qu’il lorsqu’il est utilisé plus loin dans ce document) et cliquez sur **OK**. 

12. Une fois que la nouvelle table a été créée, vous serez en mesure de voir dans le **Service de Table** page (en bas).

    ![nouvelle table créée](images/AzureLabs-Lab313-42.png)  

13. Cliquez maintenant sur **clés d’accès** et effectuez une copie de la **nom de compte de stockage** et **clé** (à l’aide de votre bloc-notes), vous utiliserez ces valeurs plus loin dans ce cours, lorsque vous créez le **Azure Function App**.

    ![nouvelle table créée](images/AzureLabs-Lab313-43.png) 

14. Utilisation du Panneau de gauche à nouveau, faites défiler vers le *Service de Table* section, puis cliquez sur **Tables** (ou **parcourir les Tables**, dans les portails plus récente) et effectuez une copie de la  **URL de la table** (à l’aide de votre bloc-notes). Vous utiliserez cette valeur plus loin dans ce cours, lors de la liaison de votre table à votre **Power BI** application.

    ![nouvelle table créée](images/AzureLabs-Lab313-44.png)

## <a name="chapter-12---completing-the-azure-table"></a>Chapitre 12 - fin de la Table Azure

Maintenant que votre **Service de Table** compte de stockage a été configuré, il est temps d’ajouter des données, qui sera utilisé pour stocker et récupérer des informations. La modification de vos Tables peut être effectuée via **Visual Studio**.

1. Ouvrez **Visual Studio** (**pas** Visual Studio Code).

2. Dans le menu, cliquez sur **Affichage > Cloud Explorer**.

    ![Ouvrez cloud explorer](images/AzureLabs-Lab313-45.png)

3. Le **Cloud Explorer** s’ouvre comme un élément ancré (patient, comme le chargement peut prendre un temps).

    > [!WARNING] 
    > Si l’abonnement que vous avez utilisé pour créer votre *comptes de stockage* n’est pas visible, assurez-vous d’avoir : 
    > - Ouvert une session le même compte que celui utilisé pour le portail Azure.
    > - Sélectionné de votre abonnement à partir de la page de gestion des comptes (vous devrez peut-être appliquer un filtre à partir de vos paramètres de compte) :  
    >
    >   ![trouver un abonnement](images/AzureLabs-Lab313-46.png)

4. Vos Services cloud Azure seront affichera. Rechercher **comptes de stockage** et cliquez sur la flèche à gauche de cette option pour développer vos comptes.

    ![ouvrir des comptes de stockage](images/AzureLabs-Lab313-47.png)

5. Une fois développé, vous avez récemment créé **compte de stockage** doit être disponible. Cliquez sur la flèche à gauche de votre stockage et recherchez une fois qui est développé, **Tables** et cliquez sur la flèche à côté de cela, pour faire apparaître le **Table** vous avez créé dans le dernier chapitre. Double-cliquez sur votre **Table**.

6. Votre table sera ouvert dans le centre de la fenêtre Visual Studio. Cliquez sur l’icône de table avec la **+** (plus) sur celui-ci.

    ![Ajouter une nouvelle table](images/AzureLabs-Lab313-48.png)

7. Une fenêtre s’affiche invite pour pouvoir *ajouter une entité*. Vous allez créer qu’une seule entité, s’il trois propriétés. Vous remarquerez que *PartitionKey* et *RowKey* sont déjà fournies, car elles sont utilisées par la table à rechercher vos données. 

    ![clé de partition et de ligne](images/AzureLabs-Lab313-49.png)

8. Mettre à jour les valeurs suivantes :

    - Nom : **PartitionKey**, valeur : **PK_IoTMessages** 

    - Nom : **RowKey**, valeur : **RK_1_IoTMessages** 

9. Ensuite, cliquez sur **ajouter une propriété** (à l’angle inférieur gauche de la *ajouter une entité* fenêtre) et ajoutez la propriété suivante :

    - **Le MessageContent**, comme un *chaîne*, laissez la valeur vide.

10. Votre table doit correspondre à celui de l’image ci-dessous :

    ![ajouter des valeurs correctes](images/AzureLabs-Lab313-50.png)

    > [!NOTE] 
    > La raison pour laquelle l’entité dispose le numéro 1 dans la clé de ligne, est, car vous souhaiterez peut-être ajouter plus de messages, vous souhaitez faire des essais avec ce cours.

11. Cliquez sur **OK** lorsque vous avez terminé. Votre table est maintenant prête à être utilisé.

## <a name="chapter-13---create-an-azure-function-app"></a>Chapitre 13 - créer une application de fonction Azure 

Il est temps maintenant de créer un *Azure Function App*, qui sera appelé par le *Service IoT Hub* pour stocker le *IoT Edge* messages d’appareil dans le **Table** Service, que vous avez créé dans le chapitre précédent.

Vous devez tout d’abord, créez un fichier qui permettra à votre fonction Azure charger les bibliothèques que vous avez besoin.

1.  Ouvrez **le bloc-notes** (appuyez sur la *Windows clé*et le type *le bloc-notes*).

    ![Ouvrez le bloc-notes](images/AzureLabs-Lab313-51.png)

2.  Avec le bloc-notes ouvert, insérer la structure JSON ci-dessous. Une fois que vous avez terminé, enregistrez-le sur votre bureau en tant que **project.json**. Ce fichier définit les bibliothèques de que votre fonction utilisera. Si vous avez utilisé NuGet, il vous sera familier.
    
    > [!WARNING]
    > Il est important que l’attribution de noms est correcte ; faire en sorte qu’il cas **n’a pas un .txt** extension de fichier. Pour référence, voir ci-dessous :
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

3.  Connectez-vous à la [Azure Portal](https://portal.azure.com).

4.  Une fois que vous êtes connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche coin inférieur droit, puis recherchez **Function App**, puis appuyez sur la **entrée** clé, à rechercher. Cliquez sur *Function App* dans les résultats, pour ouvrir un nouveau volet.

    ![recherche de l’application de fonction](images/AzureLabs-Lab313-53.png)

5.  Le nouveau panneau fournit une description de la **Function App** Service. En bas à gauche de ce panneau, cliquez sur le **créer** bouton, pour créer une association avec ce Service.

    ![instance d’application (fonction)](images/AzureLabs-Lab313-54.png)

6.  Une fois que vous avez cliqué sur **créer**, renseignez les valeurs suivantes :

    1. Pour **nom de l’application**, insérez votre nom souhaité pour cette instance de Service.

    2. Sélectionnez un **abonnement**.

    3. Sélectionnez le niveau de tarification approprié pour vous, si c’est la première heure de création d’un **Service Function App**, un niveau gratuit doit être disponible pour vous.

    4. Choisissez un **groupe de ressources** ou créez-en un. Un groupe de ressources offre un moyen pour surveiller, de contrôler l’accès, disposition et de gérer, de facturation pour une collection de ressources Azure. Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).

        > Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).

    5. Pour **système d’exploitation**, cliquez sur Windows, car il s’agit de la plateforme.

    6. Sélectionnez un **Plan d’hébergement** (à l’aide de ce didacticiel est un **Plan de consommation**.

    7. Sélectionnez un **emplacement** (choisissez le même emplacement que le stockage que vous avez créé à l’étape précédente)

    8. Pour le **stockage** section, **vous devez sélectionner le Service de stockage que vous avez créé à l’étape précédente**.

    9. Vous n’aurez pas *Application Insights* dans cette application, par conséquent, n’hésitez pas à laisser **hors**.

    10. Cliquez sur **Create (Créer)**.

        ![créer la nouvelle instance](images/AzureLabs-Lab313-55.png)

7.  Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.

8.  Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.

    ![nouvelle notification](images/AzureLabs-Lab313-56.png)

9.  Cliquez sur la notification, une fois que le déploiement a réussi (terminée).

10. Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service. 

    ![accéder à la ressource](images/AzureLabs-Lab313-57.png)

11. Dans la partie gauche du panneau Nouveau, cliquez sur le **+** (plus) de l’icône située à côté *fonctions*, pour créer une nouvelle fonction.

    ![ajouter la nouvelle fonction](images/AzureLabs-Lab313-58.png)

12. Dans le volet central, le **fonction** fenêtre de création s’affiche. Descendez plus bas, puis cliquez sur **fonction personnalisée**.

    ![fonction personnalisée](images/AzureLabs-Lab313-59.png)

13. Défilement vers le bas de la page suivante, jusqu'à ce que vous trouviez **IoT Hub (Event Hub)**, puis cliquez dessus.

    ![fonction personnalisée](images/AzureLabs-Lab313-60.png)

14. Dans le **IoT Hub (Event Hub)** panneau, définissez la **langage** à **C#** , puis cliquez sur **nouveau**.

    ![fonction personnalisée](images/AzureLabs-Lab313-61.png)

15. Dans la fenêtre qui s’affiche, assurez-vous que **IoT Hub** est sélectionné et le nom de la *IoT Hub* champ correspond au nom de votre *Service IoT Hub* que vous avez créé précédemment ([à l’étape 8, du chapitre 3](#chapter-3---the-iot-hub-service)). Puis cliquez sur le **sélectionnez** bouton.

    ![fonction personnalisée](images/AzureLabs-Lab313-62.png)

16. Sur le **IoT Hub (Event Hub)** panneau, cliquez sur **créer**.

    ![fonction personnalisée](images/AzureLabs-Lab313-63.png)

17. Vous êtes redirigé vers l’éditeur de fonction.

    ![fonction personnalisée](images/AzureLabs-Lab313-64.png)

18. Supprimez tout le code qu’il contient et remplacez-le par ce qui suit :

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

19. Modifier les variables suivantes, afin qu’ils correspondent aux valeurs appropriées (**Table** et **stockage** valeurs, à partir de [l’étape 11 et 13, respectivement, du chapitre 11](#chapter-11---create-table-service)), que vous rencontrerez dans vos **compte de stockage**:

    - **tableName**, avec le nom de votre **Table** situé dans votre **compte de stockage**.
    - **tableURL**, avec l’URL de votre **Table** situé dans votre **compte de stockage**.
    - **storageAccountName**, avec le nom de la valeur correspondant avec le nom de votre **compte de stockage** nom.
    - **storageAccountKey**, avec la clé que vous avez obtenu dans le Service de stockage que vous avez créé précédemment.

    ![fonction personnalisée](images/AzureLabs-Lab313-65.png)

20. Le code en place, cliquez sur **enregistrer**.

21. Ensuite, cliquez sur le **\<** icône (flèche), sur le côté droit de la page.

    ![fonction personnalisée](images/AzureLabs-Lab313-66.png)

22. Un glisser en partant de la droite. Dans ce panneau, cliquez sur **télécharger**et un *Explorateur de fichiers* s’affiche.

23. Accédez à, puis cliquez sur, la **project.json** fichier que vous avez créé dans **le bloc-notes** précédemment, puis cliquez sur le **Open** bouton. Ce fichier définit les bibliothèques utilisées par votre fonction.

    ![fonction personnalisée](images/AzureLabs-Lab313-67.png)

24. Quand le fichier a été chargé, il apparaît dans le volet de droite. En cliquant sur il s’ouvre dans le **fonction** éditeur. Il doit rechercher **exactement** identique à l’image suivante.

    ![fonction personnalisée](images/AzureLabs-Lab313-68.png)

25. À ce stade il serait judicieux de tester la fonction de votre fonction pour stocker le message sur votre *Table*. Sur le côté droit de la fenêtre, cliquez sur **Test**.

    ![fonction personnalisée](images/AzureLabs-Lab313-69.png)

26. Insérer un message sur le **corps de la demande**, comme illustré dans l’image ci-dessus, puis cliquez sur **exécuter**. 

27. La fonction s’exécute, en affichant l’état de résultat (vous remarquerez le vert **état 202 accepté**, ci-dessus le *sortie* fenêtre, ce qui signifie qu’il a un appel réussi) :

    ![résultat de sortie](images/AzureLabs-Lab313-70.png)

## <a name="chapter-14---view-active-messages"></a>Chapitre 14 - afficher les messages actives

Si vous ouvrez Visual Studio (**pas** Visual Studio Code), vous pouvez visualiser les résultats de votre message test, tel qu’il sera stocké dans le *le MessageContent* zone de chaîne.

![fonction personnalisée](images/AzureLabs-Lab313-71.png)

Avec le Service de Table et l’application de fonction en place, les messages de votre appareil Ubuntu seront affichera dans votre *IoTMessages* Table. Si pas déjà en cours d’exécution, redémarrez votre appareil et vous serez en mesure de voir les messages de résultat à partir de votre appareil et le module, au sein de votre Table, l’aide de Visual Studio *Cloud Explorer*.

![Visualiser les données](images/AzureLabs-Lab313-72.png)


## <a name="chapter-15---power-bi-setup"></a>Chapitre 15 - le programme d’installation de Power BI

Pour visualiser les données à partir de votre appareil IOT vous permettra de configurer **Power BI** (version de bureau), pour collecter les données à partir de la *Table* Service, qui vous venez de créer. Le *HoloLens* version de Power BI utiliserez ensuite ces données pour visualiser le résultat.

1.  Ouvrez le Microsoft Store sur Windows 10 et recherchez **Power BI Desktop**.

    ![Power BI](images/AzureLabs-Lab313-73.png)

2.  Télécharger l’application. Une fois le téléchargement terminé, l’ouvrir.

3.  Connectez-vous à *Power BI* avec votre **compte Microsoft 365**. Vous pouvez être redirigé vers un navigateur, pour vous inscrire. Une fois que vous êtes inscrit, revenez à l’application Power BI et vous reconnecter.

4.  Cliquez sur **obtenir des données** , puis cliquez sur **plus...** .

    ![Power BI](images/AzureLabs-Lab313-74.png)

5.  Cliquez sur **Azure**, **stockage Table Azure**, puis cliquez sur **Connect**.

    ![Power BI](images/AzureLabs-Lab313-75.png)

6.  Vous devrez insérer le **Table URL** que vous avez collectées précédemment ([à l’étape 13 du chapitre 11](#chapter-11---create-table-service)), lors de la création de votre Service de Table. Après avoir inséré l’URL, supprimez la portion du chemin d’accès faisant référence à la Table « sous-dossier » (qui était IoTMessages, dans ce cours). Le résultat final doit être tel qu’affiché dans l’image ci-dessous. Cliquez ensuite sur **OK**.

    ![Power BI](images/AzureLabs-Lab313-76.png)

7.  Vous devrez insérer le **clé de stockage** que vous avez notée ([à l’étape 11 du chapitre 11](#chapter-11---create-table-service)) antérieures lors de la création de votre stockage Table. Cliquez ensuite sur **Connect**.

    ![Power BI](images/AzureLabs-Lab313-77.png)  

8. Un **panneau navigation** s’affiche, cochez la case en regard de votre Table et cliquez sur **charge**.

    ![Power BI](images/AzureLabs-Lab313-78.png)  

9. Votre table a maintenant été chargée sur Power BI, mais elle nécessite une requête pour afficher les valeurs qu’il contient. Pour ce faire, cliquez sur le nom de la table situé dans le **panneau champs** sur le côté droit de l’écran. Cliquez ensuite sur **modifier la requête**.

    ![Power BI](images/AzureLabs-Lab313-79.png) 

10. Un **Power Query Editor** ouvrira une nouvelle fenêtre, affichage de votre table. Cliquez sur le mot **enregistrement** au sein de la *contenu* colonne de la table, pour visualiser votre contenu stocké.

    ![Power BI](images/AzureLabs-Lab313-80.png)    

11. Cliquez sur **dans la Table**, à l’angle supérieur gauche de la fenêtre. 

    ![Power BI](images/AzureLabs-Lab313-81.png)

12. Cliquez sur **Fermer & appliquer**.

    ![Power BI](images/AzureLabs-Lab313-82.png)

13. Une fois qu’il a terminé de charger la requête, dans le **panneau champs**, sur le côté droit de l’écran, cochez les cases à cocher correspondant aux paramètres **nom** et **valeur**, à visualiser le **le MessageContent** contenu de la colonne.

    ![Power BI](images/AzureLabs-Lab313-83.png)

14. Cliquez sur le **icône de disque bleu** en haut à gauche de la fenêtre pour enregistrer votre travail dans un dossier de votre choix.

    ![Power BI](images/AzureLabs-Lab313-84.png)

15. Vous pouvez maintenant cliquer sur le bouton Publier pour charger votre table dans votre espace de travail. Lorsque vous y êtes invité, cliquez sur **mon espace de travail** et cliquez sur *sélectionnez*. Attendez qu’elle afficher le résultat de réussite de l’envoi.

    ![Power BI](images/AzureLabs-Lab313-85.png)

    ![Power BI](images/AzureLabs-Lab313-86.png)

> [!WARNING]
> Le chapitre suivant est HoloLens spécifique. Power BI n’est pas actuellement disponible en tant qu’une application, mais vous pouvez exécuter la version de bureau dans le portail de réalité mixte Windows (également appelé Cliff House), via l’application de bureau.

## <a name="chapter-16---display-power-bi-data-on-hololens"></a>Chapitre 16 - données d’affichage Power BI sur HoloLens

1. Sur votre HoloLens, connectez-vous à la **Microsoft Store**, en appuyant sur son icône dans la liste des applications.

    ![Power BI HL](images/AzureLabs-Lab313-87.png)

2. Recherchez et téléchargez ensuite le **Power BI** application.

    ![Power BI HL](images/AzureLabs-Lab313-88.png)

3. Démarrer **Power BI** à partir de votre liste d’applications. 

4. **Power BI** peut vous demander de se connecter à votre **compte Microsoft 365**.

5. Une fois à l’intérieur de l’application, l’espace de travail doit afficher par défaut comme indiqué dans l’image ci-dessous. Si qui ne se produit pas, cliquez simplement sur l’icône de l’espace de travail sur le côté gauche de la fenêtre.

    ![Power BI HL](images/AzureLabs-Lab313-89.png)

## <a name="your-finished-your-iot-hub-application"></a>Votre application de votre IoT Hub terminée

Félicitations, vous avez créé un Service IoT Hub, avec un appareil simulé Edge de la Machine virtuelle. Votre appareil peut communiquer les résultats d’un modèle machine learning à un Service de Table Azure, facilité par une application de fonction Azure, qui est lu dans Power BI et visualisées dans un Microsoft HoloLens.
 
![Power BI](images/AzureLabs-Lab313-00.png)

## <a name="bonus-exercises"></a>Exercices de bonus

### <a name="exercise-1"></a>Exercice 1

Développez la structure de messagerie stockée dans la table et l’afficher sous forme de graphique. Vous souhaiterez peut-être collecter davantage de données et les stocker dans la même table, pour être affiché ultérieurement.

### <a name="exercise-2"></a>Exercice 2

Créer un autre module « capture de l’appareil photo » doit être déployé sur le tableau IoT, afin qu’il peut capturer des images via l’appareil photo à analyser.
