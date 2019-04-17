---
title: Vue du spectateur
description: Visualiser hologrammes à partir d’un périphérique externe dans le but de démontrer une expérience de réalité mixte sur un moniteur externe ou de l’enregistrement vidéo d’une expérience de réalité mixte.
author: chrisfromwork
ms.author: chriba
ms.date: 02/11/2019
ms.topic: article
keywords: Vue du spectateur, iPhone, iOS, iPad, OpenCV, appareil photo, ARKit, HoloLens, réalité mixte, MixedRealityToolkit, démonstration, enregistrement
ms.openlocfilehash: 77102cf5fb1c23f27f7f2d651c6ca1ae9df5a1d1
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595416"
---
# <a name="spectator-view-for-hololens"></a>Vue spectateur pour HoloLens

![Marker](images/SpecViewPhoneHero.jpg)


## <a name="current-refactor"></a>Refactoriser en cours

> [!NOTE]
>Vue spectateur pour HoloLens est refactorisé activement. Ce travail est destiné à consolider la version d’évaluation Pro codebases et étendre la prise en charge pour HoloLens 2. 

Pour afficher les actuel état de la refactorisation de vue du spectateur consultez branches ' fonctionnalité/spectatorView' dans les référentiels MixedRealityToolkit et de MixedRealityToolkit-Unity :

https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/feature/spectatorView/Assets/MixedRealityToolkit.Extensions/SpectatorView

et

https://github.com/Microsoft/MixedRealityToolkit/tree/feature/spectatorView/SpectatorViewPlugin

## <a name="overview"></a>Vue d'ensemble

Lorsqu’a porter un HoloLens, nous oublions souvent qu’une personne qui ne l’ont pas ne peut pas découvrir les merveilles possible. Vue de spectateur permet d’autres utilisateurs peuvent voir sur un écran 2D ce que voit un utilisateur de HoloLens dans leur environnement.
Vue spectateur (version préliminaire) est rapide et abordable approche enregistrement hologrammes dans HD, tandis que spectateur vue Pro vise l’enregistrement de qualité professionnelle des hologrammes.

Le tableau suivant présente les options et leurs fonctionnalités. Choisissez l’option qui convient le mieux à vos besoins d’enregistrement vidéo :

|                                      | Vue spectateur (version préliminaire) |              Spectateur afficher Pro              |
|--------------------------------------|:-----------------------:|:-------------------------------------------:|
| Qualité HD                         |         HD complète         |        Qualité professionnelle filmer (tel que déterminé par DSLR)      |
| Mouvement de la caméra facile                      |            ✔            |                                             |
| Troisième personne                    |            ✔            |                      ✔                      |
| Peut être diffusé aux écrans           |            ✔            |                      ✔                      |
| Portable                             |            ✔            |                                             |
| Sans fil                             |            ✔            |                                             |
| Matériel requis         |     iPhone (ou iPad)    | HoloLens + plate-forme + trépied + DSLR + PC + Unity |
| Investir dans du matériel                  |           Faible           |                     Élevée                    |
| Système multiplateforme                       |           iOS           |                                             |
| Visionneuse peut interagir.                  |            ✔            |                                             |
| Mise en réseau (UNET scripting) |            ✔            |                      ✔                      |
| Durée d’exécution le programme d’installation               |         Instant         |                     Lent                    |

## <a name="spectator-view-preview"></a>Vue spectateur (version préliminaire)

![Marker](images/SpecViewPhoneDemo.jpg)

### <a name="use-cases"></a>Cas d’utilisation

- Filmer hologrammes dans HD : À l’aide de la vue du spectateur (version préliminaire), vous pouvez enregistrer une expérience de réalité mixte à l’aide d’un iPhone. Enregistrement d’HD complète et appliquer l’anticrénelage à hologrammes et des ombres. C’est un moyen économique et rapide pour capturer les vidéos de hologrammes.
- Démonstrations en direct : Réalité mixte live Stream expériences à Apple TV directement à partir de votre iPhone ou iPad, libre de retard !
- Partagez l’expérience avec invités : Laisser les utilisateurs non HoloLens expérience hologrammes directement à partir de leurs téléphones ou leurs tablettes.

### <a name="current-features"></a>Fonctionnalités actuelles

- Automatique-découverte du réseau pour l’ajout de téléphones à la session.
- Gestion de session automatique, donc les utilisateurs sont ajoutés à la session correcte.
- Synchronisation spatiale de hologrammes, afin que tout le monde détecte hologrammes au même endroit exact.
- prise en charge d’iOS (appareils prenant en charge ARKit).
- Plusieurs iOS invités.
- L’enregistrement de vidéo + hologrammes + son ambiant + son de hologramme.
- Partager feuille, donc vous pouvez enregistrer vidéo, par courrier électronique ou partager avec d’autres applications prenant en charge.


>[!NOTE] 
>Le code de vue du spectateur (version préliminaire) ne peut pas être utilisé avec le code de la version Pro de vue spectateur. Nous vous recommandons de mettre en œuvre de nouveaux projets où un enregistrement vidéo de hologrammes est requis.

<br>

>[!VIDEO https://www.youtube.com/embed/3fXlPw_FGLg]


### <a name="licenses"></a>Licences

- [OpenCV - (3-clause BSD licence)](https://opencv.org/license.html)
- [Unity ARKit - (licence MIT)](https://bitbucket.org/Unity-Technologies/unity-arkit-plugin/src/3691df77caca2095d632c5e72ff4ffa68ced111f/LICENSES/MIT_LICENSE?at=default&fileviewer=file-view-default)

## <a name="how-to-set-up-spectator-view-preview"></a>Comment configurer la vue spectateur (version préliminaire)

### <a name="requirements"></a>Configuration requise

- [Le plug-in de spectateur vue et les fichiers binaires nécessaires de OpenCV](https://github.com/Microsoft/MixedRealityToolkit/tree/master/SpectatorViewPlugin) -vous trouverez plus d’informations sur la façon de générer le plug-in spectateur vue natif ci-dessous. Dans les fichiers binaires générés, vous aurez besoin :

    - opencv_aruco343.dll
    - opencv_calib3d343.dll
    - opencv_core343.dll
    - opencv_features2d343.dll
    - opencv_flann343.dll
    - opencv_imgproc343.dll

    - zlib1.dll
    - SpectatorViewPlugin.dll
- Vue du spectateur utilise Unity mise en réseau (UNET) pour sa découverte du réseau et la synchronisation spatiale. Cela signifie que tous les interactivité lors de l’application a besoin d’être synchronisées entre les appareils.
- Unity 2017.2.1p2 ou version ultérieure
- Matériel
    - Un HoloLens
    - PC Windows exécutant Windows 10
    - Périphérique compatible ARKit (iPhone 6 s et versions ultérieures / iPad Pro 2016 et versions ultérieures / iPad 2017 et versions ultérieures)-en cours d’exécution iOS 11 ou version ultérieure
    - Mac avec xcode 9.2 et versions ultérieures
- Compte de développeur Apple, libre ou [payé](https://developer.apple.com/)
- Microsoft Visual Studio 2017

### <a name="building-the-spectator-view-native-plugin"></a>Création du plug-in natif spectateur vue

Pour générer les fichiers requis, procédez comme suit : https://github.com/Microsoft/MixedRealityToolkit/blob/master/SpectatorViewPlugin/README.md

### <a name="project-setup"></a>Programme d’installation de projet

1. Préparer votre scène, assurer que toutes les gameobjects visible au sein de votre scène sont contenus sous un gameobject de racine du monde entier.

    ![Racine du monde](images/SpecViewPhoneWorldRoot2.PNG)

2. Ajouter le préfabriqué SpectatorView ([Assets/HoloToolkit-Preview/SpectatorView/Prefabs/SpectatorView.prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Preview/SpectatorView/Prefabs/SpectatorView.prefab)) dans votre scène.
3. Ajouter le préfabriqué SpectatorViewNetworking ([Assets/HoloToolkit-Preview/SpectatorView/Prefabs/SpectatorViewNetworking.prefab](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Preview/SpectatorView/Prefabs/SpectatorViewNetworking.prefab)) dans votre scène.
4. Sélectionnez le gameobject SpectatorViewNetworking et sur le composant SpectatorViewNetworkingManager, il existe quelques éléments que vous pouvez lier. Si gauche pas modifié ce composant recherche les scripts nécessaires lors de l’exécution.
    - Marqueur détection HoloLens -> SpectatorView/Hololens/MarkerDetection
    - Marqueur génération 3D -> SpectatorView/IPhone/SyncMarker/3DMarker

    ![Découverte du réseau de SpectatorView](images/SpecViewPhoneNetworkDiscovery.PNG)

### <a name="networking-your-app"></a>Mise en réseau de votre application

- Vue du spectateur utilise UNET pour sa mise en réseau et gère toutes les connexions client à l’hôte pour vous.
- Les données d’application spécifique doit être synchronisées avec succès et implémentée par vous, en utilisant par exemple SyncVars, NetworkTransform, NetworkBehavior.
- Pour plus d’informations sur la mise en réseau de Unity visitez [mise en réseau et le mode multijoueur](https://docs.unity3d.com/Manual/UNet.html). (Remarque : UNet a été déconseillé ; la refactorisation en cours de la base de code de vue du spectateur résoudre ce problème)

### <a name="building-for-each-platform-hololens-or-ios"></a>Création pour chaque plateforme (HoloLens ou iOS)

- Lorsque vous générez pour iOS, veillez à que vous retirez le composant GLTF de MRTK car il n’est pas encore compatible avec cette plateforme.
- Au niveau supérieur de la préfabriqué SpectatorView, il existe un composant appelé « Plateforme sélecteur ». Sélectionnez la plateforme que vous souhaitez générer votre projet.
    - Si vous sélectionnez « Hololens », vous devez voir tous les gameobjects sous le gameobject iPhone dans le préfabriqué SpectatorView deviennent inactif et tous les gameobjects sous « Hololens » deviennent actifs.
    - Cela peut prendre un peu de temps comme selon la plateforme, vous choisissez la HoloToolkit est ajouté ou supprimé du projet.

    ![Sélecteur de plateforme](images/SpecViewPhoneSwitcher.PNG)

- Vérifiez que vous générez toutes les versions de l’application à l’aide de la même instance d’éditeur Unity (effectuez pas fermer Unity entre les builds) en raison d’un problème non résolu avec Unity.

### <a name="running-your-app"></a>Exécution de votre application

Une fois que vous avez créé et déployé une version de l’application sur iPhone et sur HoloLens, il se peut que vous devez être en mesure de les connecter.

1. Assurez-vous que les deux appareils sont sur le même réseau Wi-Fi.
2. Démarrez l’application sur les appareils, sans ordre spécifique. Le processus de démarrage de l’application sur l’iPhone doit déclencher la caméra HoloLens pour activer et commencer à prendre des photos.
3. Dès que l’application iPhone démarre, elle recherchera surfaces comme étages ou des tableaux. Lorsque les surfaces sont détectées, vous devez voir un marqueur semblable à celle ci-dessous. Afficher ce marqueur pour le HoloLens.

    ![Marker](images/SpecViewPhoneMarker.PNG)

4. Une fois que le marqueur a été détecté par le HoloLens, il doit disparaître tandis que les deux appareils doivent être connectés et synchronisés dans l’espace.

### <a name="recording-video"></a>Enregistrement vidéo

1. Pour capturer et enregistrer une vidéo à partir de l’iPhone, appuyez et maintenez la touche l’écran pendant 1 seconde. Le menu d’enregistrement s’ouvre.
2. Appuyez sur le bouton d’enregistrement rouge, cela permet de démarrer un compte à rebours avant de commencer à enregistrer l’écran.
3. Pour terminer l’enregistrement tap et maintenez la touche l’écran pendant 1 seconde un autre, puis appuyez sur le bouton Arrêter.
4. Une fois l’enregistrements vidéo chargée, un bouton d’aperçu (bouton bleu) s’affiche, appuyez sur pour regarder la vidéo enregistrée.
5. Ouvrez la feuille de partage et sélectionnez Enregistrer pour pellicule.

### <a name="example-scene"></a>Scène d’exemple

Vous trouverez une scène d’exemple dans [HoloToolkit-Examples\SpectatorView\Scenes\SpectatorViewExample.unity](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/SpectatorView/Scenes/SpectatorViewExample.unity)

### <a name="troubleshooting"></a>Résolution des problèmes

**L’éditeur Unity ne se connectera à une session hébergée par un appareil HoloLens**

- Cela peut être le pare-feu Windows.
- Accédez à options de pare-feu de Windows.
- Autoriser une application ou une fonctionnalité via le pare-feu de Windows.
- Pour toutes les instances de l’éditeur Unity dans le cycle de la liste, domaine, privé et Public.
- Puis revenez dans options de pare-feu de Windows.
- Cliquez sur Paramètres avancés.
- Cliquez sur règles de trafic entrant.
- Toutes les instances de l’éditeur Unity doivent avoir une coche verte est visible.
- Pour toutes les instances de l’éditeur Unity qui n’ont pas une coche verte est visible :
    - Double-cliquez dessus.
    - Dans la boîte de dialogue action, sélectionnez Autoriser la connexion.
    - Cliquez sur OK.
    - Redémarrez l’éditeur Unity.

**Lors de l’exécution, l’écran iPhone indique « Localisation Floor... » mais n’affiche ne pas un marqueur AR.**

- L’iPhone est recherchez une surface horizontale donc essayer pointant vers l’appareil photo iPhone par rapport à l’étage ou une table. Cela vous aidera ARKit trouver surfaces nécessaires à la synchronisation des SPATIALEMENT avec HoloLens.

**Appareil photo HoloLens n’active pas automatiquement lorsque iPhone tente de joindre.**

- Assurez-vous que HoloLens et iPhone sont en cours d’exécution sur le même réseau Wi-Fi.

**Lors du lancement d’une application de vue du spectateur sur un appareil mobile, autres hololens exécutant d’autres applications de la vue du spectateur allument leur appareil photo**

- GoTo le composant NewDeviceDiscovery et modifiez le port de la clé de la diffusion et la diffusion à deux valeurs uniques.
- Accédez à SpectatorViewDiscovery et modifier la clé de diffusion et le port de diffusion vers un autre ensemble de nombres uniques.

**Le HoloLens ne se connectera avec l’éditeur Unity mac.**

- Il s’agit d’un problème connu qui peut être lié à la version Unity. Création pour l’iPhone doit toujours fonctionner et connectez-vous comme d’habitude.

**L’appareil photo HoloLens active mais n’est pas en mesure d’analyser le marqueur.**

- Vérifiez que vous générez toutes les versions de l’application à l’aide de la même instance d’éditeur Unity (effectuez pas fermer Unity entre les builds). Il s’agit d’un problème inconnu avec Unity.

## <a name="spectator-view-pro"></a>Spectateur afficher Pro

![Programme d’installation de spectateur vue](images/spectatorview-300px.png)

À l’aide de spectateur vue Pro implique ces quatre composants :
1. Une application créée spécifiquement pour permettre la vue spectateur, ce qui est basée sur [partagé des expériences dans la réalité mixte](shared-experiences-in-mixed-reality.md).
2. Un utilisateur a porter HoloLens à l’aide de l’application.
3. Une plate-forme de caméra spectateur vue fournissant une vidéo de la perspective de la troisième personne.
4. Un PC de bureau exécutant l’application de l’expérience partagée et de la composition les hologrammes dans une vidéo de vue du spectateur.

![Programme d’installation de la vue Pro spectator](images/hololensspectatorview-500px.jpg) 

### <a name="use-cases"></a>Cas d’utilisation

>[!VIDEO https://www.youtube.com/embed/DgIHjxoPy_c]


*Vue de spectateur peut être utilisée pour le partage de vos créations HOLOGRAPHIQUE, qu’ils soient une image fixe, un clip vidéo ou une démonstration en direct.*


Il existe trois principaux scénarios qui fonctionnent bien avec cette technologie :

**1. Capture de photos**<br>
À l’aide de cette technologie, vous pouvez capturer des images haute résolution de votre hologrammes. Ces images peuvent être utilisées pour présenter le contenu des événements de commercialisation, envoyer à vos clients potentiels ou encore soumettre votre application pour le Windows Store. Vous pouvez décider quelle caméra de photo que vous souhaitez utiliser pour capturer ces images, par conséquent, vous pouvez préférer une caméra DSLR de qualité.


![Exemple de capture photo Pro vue spectator](images/fall-350px.jpg)<br>
*Exemple de capture photo - rendant le plancher est constituée de lave.*


**2. Capture vidéo**<br>
Vidéos sont la meilleure option indiquant le mécanisme de partage d’une expérience d’application holographique avec de nombreuses personnes. Vue du spectateur vous permet de choisir l’appareil photo, objectif et tramage plus adaptés de la façon dont vous souhaitez présenter votre application. Il vous permet de contrôler la qualité vidéo en fonction du matériel vidéo, vous avez disponibles.

![Exemple de capture vidéo de vue Pro spectator](images/spectatorviewvideo.gif)<br>
*Exemple de capture vidéo - l’enregistrement d’une expérience de collaboration de réalité mixte.*


**3. Démonstrations en direct**<br>
Vue du spectateur est une meilleure approche pour des démonstrations en direct que la position d’une caméra reste stable ou contrôlée. Étant donné que vous pouvez utiliser une caméra vidéo de haute qualité, vous pouvez également produire des images de haute qualité destinées à un grand écran. Cela est également approprié pour des démonstrations en direct sur un écran, éventuellement aux participants de hâtif attend dans la ligne leur tour de diffusion en continu.

### <a name="comparing-video-capture-techniques"></a>Comparaison des techniques de capture vidéo

[Capture de la réalité de mixte](mixed-reality-capture.md) (MRC) fournit un composite vidéo de ce que voit l’utilisateur HoloLens à partir d’une personne du premier point de vue. Vue du spectateur produit une vidéo à partir d’une perspective de la troisième personne, ce qui permet de l’Observateur de vidéo voir l’environnement avec hologrammes et l’utilisateur a porter un appareil HoloLens. Étant donné que vous avez le choix de l’appareil photo, les vues spectateur peuvent également produire une résolution plus élevée et les images de meilleure qualité que la photo HoloLens intégré utilisé pour les images de cette option. Pour cette raison, vue de spectateur est mieux adapté pour les images d’application dans le Store de Windows, vidéos, de marketing ou de la projection d’un affichage en temps réel pour un public.

![Caméra Pro vue professionnelle spectateur utilisée dans les présentations des discours d’ouverture de Microsoft](images/spectator-view-professional-red-camera-300px.jpg)<br>
*Caméra Pro vue professionnelle spectateur utilisée dans les présentations des discours d’ouverture de Microsoft*


Vue du spectateur a été un élément essentiel de la façon dont Microsoft HoloLens a présenté des expériences pour des audiences depuis le début lorsque le produit a été annoncé en janvier 2015. Le programme d’installation Professionnel utilisé avait des exigences élevées et une étiquette de prix coûteuse à atteindre. Par exemple, l’appareil photo utilise un signal genlock pour garantir un minutage précis qui coordonne avec le système de suivi de HoloLens. Dans cette configuration, déplacement de la caméra de vue spectateur était possible tout en conservant hologrammes stable pour correspondre à l’expérience d’une personne présentant l’expérience directement dans HoloLens.

La version open-source de vue du spectateur compense la possibilité de faire de la plate-forme d’appareil photo afin de réduire considérablement le coût de la configuration globale. Ce projet utilise une caméra externe montée de façon rigide à un HoloLens pour prendre des photos de haute définition et de la vidéo de votre projet Unity HOLOGRAPHIQUE. **Lors des démonstrations en direct, l’appareil photo doit rester dans une position fixe.** Déplacement de la caméra peut entraîner l’instabilité hologramme ou dérive. Il s’agit, car le délai de l’image vidéo et le rendu de hologrammes sur le PC ne soient pas précisément synchronisées. Par conséquent, en conservant la caméra stable ou limitant le mouvement produira un résultat proche de ce que la personne a porter un HoloLens peut voir.

Pour rendre votre application prête pour la vue du spectateur, vous devez créer un [partagé expérience](holograms-240.md) application et vérifiez que l’application peut s’exécuter sur HoloLens ainsi que sur le bureau dans l’éditeur Unity. La version de bureau de l’application aura créé dans cette épreuve la vidéo de flux avec les rendu hologrammes des composants supplémentaires.

## <a name="how-to-set-up-spectator-view-pro"></a>Comment configurer spectateur vue Pro 

### <a name="requirements"></a>Configuration requise

![Plateforme de test Pro spectateur vue](images/spectatorviewrig-350px.jpg)

#### <a name="hardware-shopping-list"></a>Liste d’achat de matériel

Voici une liste recommandée du matériel, mais vous pouvez faire des essais avec d’autres unités compatibles trop. 

|Composant matériel                                                                     |Recommandation               | 
|:--------------------------------------------------------------------------------------|:----------------------------|
|Configuration d’un PC qui fonctionne pour le développement holographique avec l’émulateur HoloLens  |                              | 
|Appareil photo avec sortie HDMI ou de capture photo SDK                                             | Pour la photo et de capture vidéo, nous avons testé la [Canon EOS 5D Mark III](https://www.amazon.com/Canon-Frame-Full-HD-Digital-Camera/dp/B007FGYZFI/ref=sr_1_3?s=photo&ie=UTF8&qid=1480537693&sr=1-3&keywords=Canon+5D+Mark+III) appareil photo. Pour des démonstrations en direct, nous avons testé la [Blackmagic conception Production caméra 4K](https://www.amazon.com/Blackmagic-Design-Production-Camera-Mount/dp/B00CWLSHYG/ref=sr_1_1?s=photo&ie=UTF8&qid=1480537790&sr=1-1&keywords=blackmagic+design+production+camera+4k).<br><br>Notez que n’importe quelle caméra avec HDMI out (par exemple, GoPro) devrait fonctionner. La plupart de nos vidéos utilisent le [Canon EF 14mm f/2.8 L II USM Ultra Wide Angle fixe de l’objectif](https://www.amazon.com/Canon-Ultra-Wide-Angle-Digital-Cameras/dp/B000V5P94Q), mais vous devez choisir un objectif de l’appareil photo qui répond à vos besoins. | 
|Carte de votre PC pour obtenir des cadres de couleur à partir de votre appareil photo de calibrer votre plateforme de test et afficher un aperçu de votre scène composite de capture |  Nous avons testé la [Blackmagic conception intensité Pro 4K carte de capture](https://www.amazon.com/dp/B00U3QNP7Q). | 
|Câbles                                                                                 |  [HDMI à Mini HDMI](https://www.amazon.com/AmazonBasics-High-Speed-Mini-HDMI-HDMI-Cable/dp/B014I8UHXE?ie=UTF8&psc=1&redirect=true&ref_=oh_aui_detailpage_o03_s00) pour joindre votre appareil photo sur votre carte de capture. Vérifiez que vous achetez un facteur de forme HDMI qui correspond à votre appareil photo. (GoPro, par exemple, génère sur [Micro HDMI](https://www.amazon.com/dp/B014I8U33I/ref=twister_B0198TA40O?_encoding=UTF8&psc=1).)<br><br>[Câble HDMI](https://www.amazon.com/dp/B014I8TC4E/ref=twister_B016I3XG0S?_encoding=UTF8&th=1) pour l’affichage composite de flux sur un écran de contrôle ou de télévision | 
|Usinées crochet aluminum pour connecter votre HoloLens à l’appareil photo. | [Crochet de ALUMINUM](https://github.com/Microsoft/MixedRealityCompanionKit/blob/master/LegacySpectatorView/Hardware/HoloLens_Mount.stp)   | 
|3D imprimé adaptateur pour se connecter au montage HoloLens à la sur caméra caméra.| [Carte imprimée 3D](https://github.com/Microsoft/MixedRealityCompanionKit/blob/master/LegacySpectatorView/Hardware/Mount_Adapter.stl)  | 
|Fixation sur caméra pour monter l’adaptateur sur caméra                                       |  [Élément de fixation sur caméra](https://www.amazon.com/Fotasy-SCX2-Adapter-Premier-Cleaning/dp/B00HPAPFNU/ref=redir_mobile_desktop?ie=UTF8&psc=1&ref_=yo_ii_img) | 
|Outils, bolts et assorties z                                                |  [1/4-20 » z](https://www.amazon.com/Hillman-Group-150003-20-Inch-100-Pack/dp/B000BPEPNW/ref=redir_mobile_desktop?ie=UTF8&psc=1&ref_=yo_ii_img)<br>[1/4-20 "x 3/4" Bolts](https://www.amazon.com/Hard-Find-Fastener-014973100032-4-20-Inch/dp/B004S6RZPK/ref=redir_mobile_desktop?ie=UTF8&psc=1&ref_=yo_ii_img) <br>[Pilotes d’érable 7/16](https://www.amazon.com/Klein-Tools-630-7-Cushion-Grip-Hollow-Shank/dp/B000BPG4CW/ref=sr_1_1?ie=UTF8&qid=1479853212&sr=8-1)<br>[T15 Torx](https://www.amazon.com/Stanley-60-011-Standard-Torx-Screwdriver/dp/B000KFXDWW/ref=sr_1_1?ie=UTF8&qid=1479853303&sr=8-1)<br>[T7 Torx](https://www.amazon.com/SE-7542ST-6-Piece-Professional-Screwdriver/dp/B000ST3K3W/ref=sr_1_1?ie=UTF8&qid=1479853479&sr=8-1) | 

#### <a name="software-components"></a>Composants logiciels

1. Logiciel téléchargé à partir de la [projet GitHub pour la vue du spectateur](https://github.com/Microsoft/HoloLensCompanionKit/tree/master/SpectatorView).
2. [Carte de Capture de BlackMagic SDK](https://www.blackmagicdesign.com/support). \
 Recherche de développeur pour PC vidéo SDK dans « Derniers téléchargements ».
3. [Runtime vidéo BlackMagic Desktop](https://www.blackmagicdesign.com/support). \
 Recherchez des postes de travail vidéo mise à jour dans « Derniers téléchargements ». \
 Vérifiez les correspondances de numéro de version de la version SDK.
4. [OpenCV 3.1](https://opencv.org/releases.html) d’étalonnage ou de capture vidéo sans la carte de capture Blackmagic.
5. [Canon SDK](https://www.usa.canon.com/internet/portal/us/home/explore/solutions-services/digital-camera-sdk-information) (facultatif). \
 Si vous utilisez un appareil photo Canon et que vous avez accès au kit SDK Canon, vous pouvez attache votre appareil photo à votre PC pour prendre une résolution d’image.
6. Unity pour votre développement d’applications HOLOGRAPHIQUE. \
 Vous trouverez la version prise en charge dans le projet Open source.
7. Visual Studio 2015 avec les dernières mises à jour.

### <a name="building-your-own-spectator-view-pro-camera"></a>Création de votre propre appareil photo spectateur vue Pro

**AVIS ET EXCLUSION DE RESPONSABILITÉ :** Lorsque vous modifiez votre matériel HoloLens (y compris, mais sans limitation, configurer votre HoloLens pour « vue spectateur ») base précautions de sécurité doivent toujours être respectées. Lire toutes les instructions et les manuels avant d’apporter des modifications. Il vous incombe de suivre toutes les instructions et utiliser des outils comme indiqué. Vous avez acheté ou votre HoloLens avec une garantie limitée ou aucune garantie d’une licence. Veuillez lire votre applicable [contrat de licence de HoloLens ou de conditions d’utilisation et de vente](https://www.microsoft.com/hololens/support/warranty) pour comprendre vos options de garantie.

<br>

>[!VIDEO https://www.youtube.com/embed/aKX8UMejtWc]

#### <a name="rig-assembly"></a>Assembly de plateforme de test

![Rayon spectateur vue Pro assemblé avec appareil photo HoloLens et DSLR.](images/assembly.gif)<br>
*Plateforme de test spectateur vue Pro assemblé avec appareil photo HoloLens et DSLR*


* Utilisez un tournevis T7 pour supprimer le DOTEES à partir de la HoloLens. Une fois les vis libres, piocher les out avec un trombone à partir de l’autre côté.
* Supprimez le plafond de vis à l’intérieur avant de l’hyperviseur HoloLens avec un petit tournevis plat.
* Utilisez un tournevis T15 pour supprimer les bolts torx petit crochet HoloLens à vous supprimer et en forme de raccordement de pièces jointes.
* Placez le HoloLens sur le support, en alignant le trou exposé à l’intérieur de l’hyperviseur avec l’extrusion à l’avant du support. Les armes des HoloLens doivent rester en place par les codes confidentiels dans la partie inférieure du support.
* Vous rattachez et en forme de raccordement de pièces jointes pour sécuriser la HoloLens pour le support.
* Attacher la fixation sur caméra à la sur caméra de votre appareil photo.
* Rattacher la carte de montage à la fermeture sur caméra.
* Faire pivoter l’adaptateur afin du côté étroit est face vers l’avant et un parallèle pour de l’objectif.
* Sécuriser l’adaptateur en place avec un érable 1/4 » à l’aide du pilote d’érable 7/16.
* Positionner le crochet par rapport à l’adaptateur afin de l’avant du visualiseur des HoloLens est aussi proche que possible au premier rang de l’objectif.
* Fixez le support avec 4 1/4" rouages l’utilisation du pilote d’érable 7/16.

#### <a name="pc-setup"></a>Programme d’installation de PC
* Installer le logiciel à partir de la section des composants logiciels.
* Ajouter la carte de capture à un emplacement PCIe ouvert sur votre carte mère.
* Branchez un câble HDMI à partir de votre appareil photo vers l’emplacement HDMI externe (HDMI-entrant) sur la carte de capture.
* Branchez un câble HDMI à partir de l’emplacement HDMI center (HDMI-Out) sur la carte de capture pour une analyse de l’aperçu facultatif.

#### <a name="camera-setup"></a>le programme d’installation de la caméra
* Modifiez votre appareil photo en Mode de vidéo afin qu’elle génère à la résolution de 1920 x 1080 complète et non un rognée résolution photo de 3:4.
* Rechercher les paramètres de HDMI de votre appareil et activer **mise en miroir** ou **double moniteur**.
* Définir la résolution de sortie à 1 080 P.
* Désactiver **Live sur écran affichage de la vue** ainsi les superpositions de n’importe quel écran n’apparaissent pas dans le flux de composite.
* Allumez votre appareil photo **affichage en temps réel**.
* Si vous utilisez le **Canon SDK** et souhaitez utiliser une unité flash, désactivez **dépanner de LV silencieux**.
* Branchez un câble HDMI à partir de la caméra vers l’emplacement HDMI externe (HDMI-entrant) sur la carte de capture.

#### <a name="calibration"></a>Étalonnage

Après avoir configuré votre plateforme de vue du spectateur, vous devez calibrer afin d’obtenir le décalage de position et la rotation de votre appareil photo à votre HoloLens.
* Ouvrez la solution d’étalonnage Visual Studio sous Calibration\Calibration.sln.
* Dans cette solution, vous trouverez le dependencies.props de fichier qui crée des macros pour les emplacements inc des sources tierces 3e.
* Mettre à jour de ce fichier avec l’emplacement vous avez installé OpenCV 3.1, le SDK Blackmagic et le Kit de développement logiciel Canon (le cas échéant)

![Instantané d’emplacements de dépendance dans Visual Studio](images/dependencies-600px.png)<br>
*Instantané d’emplacements de dépendance dans Visual Studio*


* Imprimer le modèle d’étalonnage Calibration\CalibrationPatterns\2_66_grid_FULL.png sur une surface plane et rigide.
* Branchez votre HoloLens sur votre PC via USB.
* Mettre à jour les définitions de préprocesseur **HOLOLENS_USER** et **HOLOLENS_PW** dans **stdafx.h** avec les informations d’identification de portail des votre HoloLens appareils.
* Connecter votre appareil photo sur votre carte de capture sur HDMI et activez-le.
* Exécutez la solution d’étalonnage.
* Déplacer le modèle de damier autour de la vue comme suit :

![Étalonnage de la plate-forme spectateur vue Pro](images/calibration.gif)<br>
*Étalonnage de la plate-forme spectateur vue Pro*


* Une image est automatiquement exécutée lorsqu’un damier est dans la vue. Recherchez la lumière blanche sur Visualiseur des HoloLens avant de passer à la pose suivante.
* Lorsque vous avez terminé, appuyez sur **entrée** avec l’application d’étalonnage en mode focus pour créer un **CalibrationData.txt** fichier.
* Ce fichier sera enregistré à **Documents\CalibrationFiles\CalibrationData.txt**
* Inspectez ce fichier pour voir si vos données d’étalonnage sont exactes :
   * **DSLR RMS** doit être proche de 0.
   * **HoloLens RMS** doit être proche de 0.
   * **RMS stéréo** peut être entre 20 et 50, cela est acceptable car le champ de vision entre les deux caméras peut être différente.
   * **Traduction** est la distance à partir de l’appareil photo des HoloLens et joint de l’objectif. Il s’agit en mètres.
   * **Rotation** doit être proche d’identité.
   * **DSLR_fov** valeur y doit être proche prévu à partir de n’importe quel facteur de rognage de corps de la caméra et de focale d’objectif de votre champ de vision verticale.
* Si une des valeurs ci-dessus ne semblent pas de sens, revoir.
* Copier ce fichier sur le **actifs** répertoire dans votre projet Unity.

### <a name="compositor"></a>Compositeur

Le constructeur est une extension Unity qui s’exécute en tant que fenêtre dans l’éditeur Unity. Pour ce faire, la solution Visual Studio de compositeur doit d’abord être généré.
* Ouvrez la solution Visual Studio de compositeur sous Compositor\Compositor.sln
* Mettre à jour dependencies.props avec les mêmes critères de la solution d’étalonnage ci-dessus. Si vous avez suivi les étapes de l’étalonnage, ce fichier sera déjà avoir été mis à jour.
* Générez la solution complète en tant que la version et l’architecture qui correspond à architecture de votre version Unity. En cas de doute, générez x x86 et x64.
* Si vous avez créé la solution pour x64, également générer le projet SpatialPerceptionHelper comme x86 dans la mesure où il s’exécutera sur le HoloLens.
* Fermez Unity s’il s’exécute votre application. Unity doit être relancé si les DLL sont modifiés lors de l’exécution.
* Exécutez Compositor\CopyDLL.cmd pour copier les DLL générés à partir de cette solution à votre projet Unity. Ce script copie les DLL vers le projet exemple inclus. Une fois que vous avez votre propre projet configuré, vous pouvez exécuter CopyDLL avec un argument de ligne de commande qui pointe vers le répertoire de ressources de votre projet à copier également il.
* Lancez l’exemple d’application Unity.

### <a name="unity-app"></a>Application Unity

Le constructeur s’exécute en tant que fenêtre dans l’éditeur Unity. Le projet exemple inclus tous les éléments configurés pour a utiliser spectateur vue une fois le compositeur que DLL sont copiés.

Vue du spectateur, l’application doit être exécuté en tant qu’un [partagé expérience](holograms-240.md). Cela signifie que des modifications d’état application qui se produisent sur le HoloLens doivent être mis en réseau pour mettre à jour de l’application en cours d’exécution trop dans Unity.

Si le démarrage à partir d’un projet Unity, vous devrez effectuer une configuration particulière tout d’abord :
* Copie **Addons/ressources/HolographicCameraRig** à partir de l’exemple de projet à votre projet.
* Ajoutez la dernière MixedRealityToolkit à votre projet, y compris **partage**, **csc.rsp**, **gmcs.rsp**, et **smcs.rsp**.
* Ajouter votre **CalibrationData.txt** fichier dans votre répertoire de ressources.

![Instantané de répertoire de ressources Unity](images/files-400px.png)

* Ajouter le **HolographicCameraRig\Prefabs\SpectatorViewManager** prefab à votre scène et renseignez les champs :
   * **HolographicCameraManager** doit être rempli avec le préfabriqué HolographicCameraManager à partir du répertoire prefab HolographicCameraRig.
   * **Point d’ancrage** doit être rempli avec le préfabriqué d’ancrage à partir du répertoire prefab HolographicCameraRig.
   * **Partage** doit être rempli avec le préfabriqué de partage à partir de la MixedRealityToolkit.
   * Remarque: Si un de ces prefabs existe déjà dans votre hiérarchie de projet, les prefabs existants servira au lieu de ces ceux.
   * **Spectateur vue IP** doit être l’adresse IP de votre HoloLens attaché à votre plateforme de vue du spectateur.
   * **IP du Service de partage** doit être l’adresse IP de l’ordinateur exécutant le MixedRealityToolkit SharingService.
   * Facultatif : Si vous avez plusieurs spectateur afficher plateformes attachés à plusieurs PC de, **IP d’ordinateur Local** doit être défini avec l’ordinateur communique avec la plate-forme de vue du spectateur.

![Propriétés de gestionnaire d’affichages spectateur dans Unity](images/spectatorviewmanager-500px.png)

* Démarrer le MixedRealityToolkit **Service de partage**
* Générez et déployez l’application qu’une UWP D3D pour le HoloLens associé à la plate-forme de vue du spectateur.
* Déployer l’application sur tous les autres appareils HoloLens dans l’expérience.
* Vérifier le **exécuter en arrière-plan** case à cocher sous **modifier/lecteur/paramètres de projet**.

![Exécuter dans le paramètre d’arrière-plan dans Unity](images/run-in-bg-400px.png)
* Lancer la fenêtre de compositeur sous **spectateur vue/compositeur**

![Vue du compositeur pour affichage spectateur dans Unity](images/compositor-500px.png)

* Cette fenêtre vous permet de :
   * Démarrer l’enregistrement de vidéos
   * Prendre une photo
   * Modifiez l’opacité de HOLOGRAMME
   * Modifier le décalage de trame (qui ajuste l’horodatage de couleur pour prendre en compte pour la latence de carte de capture)
   * Ouvrez le répertoire dans que les captures sont enregistrés
   * Demander des données de mappage spatial de la caméra de vue spectateur (s’il existe un SpatialMappingManager dans votre projet)
   * Visualiser affichage composite, ainsi que la couleur, la hologrammes et le canal alpha de la scène individuellement.
   * Allumez votre appareil photo.
   * Appuyez sur le play dans Unity.
   * Lorsque l’appareil photo est déplacé, hologrammes dans Unity doivent être où elles se trouvent dans le monde réel par rapport à la couleur de la caméra de flux.

## <a name="see-also"></a>Voir aussi

* [Capture de réalité mixte](mixed-reality-capture.md) 
* [Mixte de capture de la réalité pour les développeurs](mixed-reality-capture-for-developers.md)
* [Partage des expériences en réalité mixte](shared-experiences-in-mixed-reality.md)
* [Code de vue (version préliminaire) spectateur sur GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/SpectatorView)
* [Spectateur vue (version préliminaire) en code natif sur GitHub](https://github.com/Microsoft/MixedRealityToolkit/tree/master/SpectatorViewPlugin)
* [Code de vue Pro spectateur sur GitHub](https://github.com/Microsoft/HoloLensCompanionKit/tree/master/SpectatorView)
