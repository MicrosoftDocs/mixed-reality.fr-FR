---
title: MR Spatial 220 - son Spatial
description: Suivez cette procédure pas à pas codage à l’aide de Unity, Visual Studio et HoloLens pour connaître les détails des concepts de sons spatiales.
author: keveleigh
ms.author: kurtie
ms.date: 03/21/2018
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-unity, academy, didacticiel, son spatial
ms.openlocfilehash: 50d17fe8c9a6e3f18b1309a59c9c41af982a7505
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593831"
---
>[!NOTE]
>Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.  Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.  Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.  Ils seront conservées pour continuer à travailler sur les appareils pris en charge. Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.  Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.

<br>

# <a name="mr-spatial-220-spatial-sound"></a>MR 220 spatiale : Son spatial

[Son spatial](spatial-sound.md) breathes vie dans hologrammes et leur donne la présence dans notre monde. Hologrammes sont composées de lumière et son, et s’il vous arrive de perdre de votre hologrammes, son spatial peut vous aider à les trouver. Son spatial n’est pas comme le son classique que vous devez entendre sur la case d’option, il est son qui est positionné dans l’espace 3D. Avec son spatial, vous pouvez rendre hologrammes audio comme ils sont derrière vous, en regard de vous, ou même sur votre tête ! Dans ce cours, vous allez :

* Configurer votre environnement de développement pour utiliser Microsoft Spatial Sound.
* Utiliser le son Spatial pour améliorer les interactions.
* Utiliser le son Spatial conjointement avec le mappage Spatial.
* Comprendre sonorisation et en combinant les meilleures pratiques.
* Utiliser le son pour améliorer les effets spéciaux et placer l’utilisateur dans le monde de réalité mixte.

## <a name="device-support"></a>Prise en charge des appareils

<table>
<tr>
<th>Cours</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></th>
</tr><tr>
<td>MR 220 spatiale : Son spatial</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Prérequis

* Un PC Windows 10 configuré avec le bon [outils installés](install-the-tools.md).
* Base C# possibilité de programmation.
* Vous devez avoir terminé [101 de principes de base MR](holograms-101.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez le [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-220-SpatialSound.zip) requise par le projet. Nécessite Unity 2017.2 ou version ultérieure.
  * Si vous avez besoin de prise en charge de Unity 5.6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-220.zip). Cette version peut ne plus être à jour.
  * Si vous avez besoin de prise en charge de Unity 5.5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-220.zip). Cette version peut ne plus être à jour.
  * Si vous avez besoin de prise en charge de Unity 5.4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-220.zip). Cette version peut ne plus être à jour.
* Annuler-archive les fichiers sur votre bureau ou autres facilement atteindre l’emplacement.

>[!NOTE]
>Si vous souhaitez examiner le code source avant de télécharger, il a [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-220-SpatialSound).

### <a name="errata-and-notes"></a>Errata et remarques

* « Activer uniquement mon Code » doit être désactivé (*unchecked*) dans Visual Studio sous Outils -> Options -> débogage afin d’atteindre des points d’arrêt dans votre code.

## <a name="chapter-1---unity-setup"></a>Chapitre 1 - le programme d’installation Unity

### <a name="objectives"></a>Objectifs

* Modifier la configuration de son d’Unity pour utiliser Microsoft Spatial Sound.
* Ajouter des sons 3D à un objet dans Unity.

### <a name="instructions"></a>Instructions

* Démarrez Unity.
* Sélectionnez **Open**.
* Accédez à votre bureau et de rechercher le dossier vous précédemment non archivés.
* Cliquez sur le **Starting\Decibel** dossier et appuyez sur la **sélectionner le dossier** bouton.
* Attendez que le projet à charger dans Unity.
* Dans le **projet** Panneau de configuration, ouvrez **Scenes\Decibel.unity**.
* Dans le **hiérarchie** volet, développez **HologramCollection** et sélectionnez **P0LY**.
* Dans l’inspecteur, développez **AudioSource** et notez qu’il y a aucune **Spatialize** case à cocher.

Par défaut, Unity ne charge pas un plug-in spatial. Les étapes suivantes activera le son de Spatial dans le projet.

* Dans le menu supérieur de Unity, accédez à **Modifier > Paramètres du projet > Audio**.
* Rechercher la **plug-in spatial** liste déroulante, puis sélectionnez **MS HRTF Spatializer**.
* Dans le **hiérarchie** panneau, sélectionnez **HologramCollection > P0LY**.
* Dans le **inspecteur** panneau, recherchez le **Audio Source** composant.
* Vérifier le **Spatialize** case à cocher.
* Faites glisser le **Blend Spatial** curseur jusqu’au **3D**, ou entrez **1** dans la zone d’édition.

Maintenant nous générer le projet dans Unity et configurer la solution dans Visual Studio.

1. Dans Unity, sélectionnez **fichier > Paramètres de Build**.
2. Cliquez sur **ajouter un arrière-plan Open** pour ajouter la scène.
3. Sélectionnez **plateforme Windows universelle** dans le **plateforme** liste et cliquez sur **plateforme de commutation**.
4. Si vous développez en particulier pour HoloLens, définissez **appareil cible** à **HoloLens**. Dans le cas contraire, laissez-le sur **n’importe quel appareil**.
5. Vérifiez **Type Build** a la valeur **D3D** et **SDK** a la valeur **dernière installé** (qui doit être SDK 16299 ou une version ultérieure).
6. Cliquez sur **Build**.
7. Créer un **nouveau dossier** nommé « Application ».
8. Clic le **application** dossier.
9. Appuyez sur **sélectionnez dossier**.

Quand Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.

1. Ouvrez le **application** dossier.
2. Ouvrez le **Solution de Visual Studio en décibels**.

Si le déploiement sur HoloLens :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x86**.
2. Cliquez sur la flèche déroulante en regard du bouton de l’ordinateur Local, puis sélectionnez **Machine distante**.
3. Entrez **votre adresse IP du périphérique HoloLens** et définir le Mode d’authentification **universel (protocole non chiffré)**. Cliquez sur **Sélectionner**. Si vous ne connaissez pas votre adresse IP du périphérique, recherchez dans **Paramètres > réseau & Internet > Options avancées**.
4. Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**. S’il s’agit de la première fois le déploiement sur votre périphérique, vous devrez [Couplez-le Visual Studio](using-visual-studio.md#pairing-your-device---hololens-1st-gen).

Si le déploiement sur un casque immersif :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, de modifier la cible de débogage pour **version** et à partir d’ARM pour **x64**.
2. Assurez-vous que la cible de déploiement est définie sur **ordinateur Local**.
3. Dans la barre de menus supérieure, cliquez sur **Déboguer -> Démarrer sans débogage** ou appuyez sur **Ctrl + F5**.

## <a name="chapter-2---spatial-sound-and-interaction"></a>Chapitre 2 - son Spatial et Interaction

### <a name="objectives"></a>Objectifs

* Améliorer le réalisme hologramme à l’aide de son.
* Diriger le regard de l’utilisateur à l’aide de son.
* Fournir des commentaires de mouvement à l’aide de son.

### <a name="part-1---enhancing-realism"></a>Partie 1 - amélioration de réalisme

#### <a name="key-concepts"></a>Concepts clés

* Spatialize les sons hologramme.
* Sources audio doivent être placés à l’emplacement approprié sur l’hologramme.

L’emplacement approprié pour le son est tout dépendra de l’hologramme. Par exemple, si l’hologramme est d’un humain, la source audio doit se trouver près de la bouche et pas les pieds.

#### <a name="instructions"></a>Instructions

Les instructions suivantes seront attache un son spatialized un hologramme.

* Dans le **hiérarchie** volet, développez **HologramCollection** et sélectionnez **P0LY**.
* Dans le **inspecteur** volet le **AudioSource**, cliquez sur le cercle en regard **AudioClip** et sélectionnez **PolyHover** à partir de la fenêtre contextuelle.
* Cliquez sur le cercle en regard **sortie** et sélectionnez **effets sonores** à partir de la fenêtre contextuelle.

Projet décibels utilise un Unity **AudioMixer** composant pour activer l’ajustement des niveaux audio pour les groupes de sons. En regroupant des sons de cette façon, le volume total peut être ajusté tout en conservant le volume relatif de chaque son.

* Dans le **AudioSource**, développez **les paramètres audio 3D**.
* Définissez **Doppler niveau** à **0**.

La définition Doppler niveau pour zéro désactive les modifications à la tonalité a provoqué par motion (soit de l’hologramme ou de l’utilisateur). Un exemple classique de Doppler est une voiture évoluant rapidement. Approche de la voiture un écouteur stationnaire, la tonalité du moteur de données augmente. Lorsqu’il passe à l’écouteur, le tangage réduit à distance.

### <a name="part-2---directing-the-users-gaze"></a>Partie 2 : diriger du pointage de regard l’utilisateur

#### <a name="key-concepts"></a>Concepts clés

* Utiliser le son pour attirer l’attention sur hologrammes importants.
* Les oreilles vous permettent de diriger où les yeux doivent se présenter.
* Le cerveau a certaines attentes appris.

Un exemple d’attentes appris est qu’oiseaux est généralement ci-dessus les têtes de personnes impliquées. Si un utilisateur entend un son bird, leur réaction initiale consiste à rechercher. Placer un oiseau ci-dessous l’utilisateur peut entraîner les accessible sur la direction correcte du son, mais l’impossibilité de trouver l’hologramme en fonction de l’attente d’avoir à rechercher.

#### <a name="instructions"></a>Instructions

Les instructions suivantes activent P0LY masquer derrière vous, afin que son permet de localiser l’hologramme.

* Dans le **hiérarchie** panneau, sélectionnez **gestionnaires**.
* Dans le **inspecteur** panneau, recherchez **Gestionnaire d’entrée vocale**.
* Dans **Gestionnaire d’entrée vocale**, développez **accédez masquer**.
* Modification **aucune fonction** à **PolyActions.GoHide**.

![mot clé : Accédez masquer](images/gohide.png)

### <a name="part-3---gesture-feedback"></a>Partie 3 : les commentaires de mouvement

#### <a name="key-concepts"></a>Concepts clés

* Fournir à l’utilisateur avec la confirmation de mouvement positive à l’aide de son
* Ne surchargent pas l’utilisateur - get sons trop forts de la façon
* Travail sons subtiles meilleures - assombrissent pas l’expérience

#### <a name="instructions"></a>Instructions

* Dans le **hiérarchie** volet, développez **HologramCollection**.
* Développez **EnergyHub** et sélectionnez **Base**.
* Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Gestionnaire de mouvements son**.
* Dans **Gestionnaire de mouvements son**, cliquez sur le cercle en regard **Navigation démarré Clip** et **Clip mis à jour de Navigation** et sélectionnez **RotateClick**à partir de la fenêtre contextuelle pour les deux.
* Double-cliquez sur « GestureSoundHandler » pour charger dans Visual Studio.

Gestionnaire de mouvements son effectue les tâches suivantes :

* Créer et configurer un **AudioSource**.
* Place le **AudioSource** à l’emplacement du approprié **GameObject**.
* Lit le **AudioClip** associées au geste.

#### <a name="build-and-deploy"></a>Générer et déployer

1. Dans Unity, sélectionnez **fichier > Paramètres de Build**.
2. Cliquez sur **Build**.
3. Clic le **application** dossier.
4. Appuyez sur **sélectionnez dossier**.

Vérifiez que la barre d’outils indique « Release », « x 86 » ou « x64 » et « Appareil à distance ». Si ce n’est pas le cas, c’est l’instance de codage de Visual Studio. Vous devrez peut-être ouvrir à nouveau la solution à partir du dossier d’application.

* Si vous y êtes invité, rechargez les fichiers de projet.
* Comme auparavant, vous déployez à partir de Visual Studio.

Une fois que l’application est déployée :

* Observez comment le son change à mesure que vous déplacez P0LY.
* Par exemple *« Accédez masquer »* P0LY pour déplacer vers un emplacement derrière vous. Rechercher le son.
* Utilisation à la base du Hub d’énergie. Cliquez et faites glisser les gauche ou droite pour faire pivoter l’hologramme et notez la façon dont le son clic confirme le mouvement.

Remarque: Il existe un volet de texte qui sera tag-along avec vous. Il contient les commandes vocales disponibles que vous pouvez utiliser tout au long de ce cours.

## <a name="chapter-3---spatial-sound-and-spatial-mapping"></a>Chapitre 3 - mappage audio et Spatial Spatial

### <a name="objectives"></a>Objectifs

* Confirmer l’interaction entre hologrammes et le monde réel à l’aide de son.
* Occlude son à l’aide du monde physique.

### <a name="part-1---physical-world-interaction"></a>1ère partie-Interaction du monde physique

#### <a name="key-concepts"></a>Concepts clés

* Objets physiques font généralement un son lorsqu’il rencontre une aire ou un autre objet.
* Sons doivent être le contexte approprié au sein de l’expérience.

Par exemple, définissant une tasse sur une table doit rendre un son moins fort que la suppression d’un boulder sur une pièce de métal.

#### <a name="instructions"></a>Instructions

* Dans le **hiérarchie** volet, développez **HologramCollection**.
* Développez **EnergyHub**, sélectionnez **Base**.
* Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Action et appuyez sur les Place à avec son**.
* Dans **appuyez sur à la Place avec Action et son**:
  * Vérifiez **placer Parent sur Tap**.
  * Définissez **Placement son** à **Place**.
  * Définissez **Pickup son** à **Pickup**.
  * Appuyez sur le signe + en bas à droite dans les répertoires **sur l’Action Pickup** et **sur l’Action de sélection élective**. Faites glisser EnergyHub à partir de la scène dans la **None (objet)** champs.
    * Sous **sur l’Action Pickup**, cliquez sur **aucune fonction** -> **EnergyHubBase** -> **ResetAnimation**.
    * Sous **sur l’Action de sélection élective**, cliquez sur **aucune fonction** -> **EnergyHubBase** -> **OnSelect**.

![Appuyez sur à la Place avec son et Action](images/holograms220-taptoplace.png)

### <a name="part-2---sound-occlusion"></a>2ème partie-Occlusion audio

#### <a name="key-concepts"></a>Concepts clés

* Son, comme la lumière, permettre être bloqué.

Un exemple classique est une salle de concert. Lorsqu’un écouteur est permanent en dehors de la salle et la porte est fermée, les sons de musique muffled. Il est également généralement une réduction de volume. Lorsque la porte est ouverte, la gamme complète du son est entendue à du volume réel. Sons de haute fréquence sont absorbées généralement plus de basses fréquences.

#### <a name="instructions"></a>Instructions

* Dans le **hiérarchie** volet, développez **HologramCollection** et sélectionnez **P0LY**.
* Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Audio émetteur**.

La classe de l’émetteur de l’Audio fournit les fonctionnalités suivantes :

* Restaure toutes les modifications sur le volume de la **AudioSource**.
* Effectue un **Physics.RaycastNonAlloc** à partir de la position de l’utilisateur dans la direction de la **GameObject** auquel le **AudioEmitter** est attaché.

Optimiser les performances, la méthode RaycastNonAlloc permet de limiter les allocations, ainsi que le nombre de résultats retournés.

* Pour chaque **IAudioInfluencer** rencontré, appelle le **ApplyEffect** (méthode).
* Pour chaque précédente **IAudioInfluencer** appel de ne plus s’est produite, autrement dit le **RemoveEffect** (méthode).

Notez que AudioEmitter met à jour sur les échelles de temps humain, par opposition à sur une trame par trame. Pour cela, car l’homme généralement ne se déplace pas assez rapide pour l’effet de mettre à jour plus fréquemment que tous les trimestres ou d’une demie seconde. Hologrammes ce teleport rapidement d’un emplacement vers un autre peut interrompre l’illusion.

* Dans le **hiérarchie** volet, développez **HologramCollection**.
* Développez **EnergyHub** et sélectionnez **BlobOutside**.
* Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Audio OCCLUSION**.
* Dans **Audio OCCLUSION**, affectez la valeur **fréquence de coupure** à **1500**.

Ce paramètre limite les fréquences AudioSource à 1 500 Hz et versions antérieures.

* Définissez **Volume passthrough** à **0.9**.

Ce paramètre réduit le volume de la AudioSource à 90 % de son niveau actuel.

Audio OCCLUSION implémente IAudioInfluencer à :

* Appliquer un effet d’occlusion à l’aide un **AudioLowPassFilter** qui est attaché à la **AudioSource** managé acheter le **AudioEmitter**.
* S’applique à atténuation de volume à la AudioSource.
* Désactive l’effet en définissant une fréquence de coupure neutre et de la désactivation du filtre.

La fréquence utilisée comme neutre est 22 kHz (22000 Hz). Cette fréquence a été choisie car elles sont au-dessus de la fréquence maximale nominale pouvant être entendu l’oreille humaine, cette aucun impact notable rendre le son.

* Dans le **hiérarchie** panneau, sélectionnez **SpatialMapping**.
* Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **Audio OCCLUSION**.
* Dans **Audio OCCLUSION**, affectez la valeur **fréquence de coupure** à **750**.

Lorsque plusieurs occluders se trouvent dans le chemin d’accès entre l’utilisateur et le **AudioEmitter**, la fréquence de la plus basse est appliquée au filtre.

* Définissez **Volume passthrough** à **0,75**.

Lorsque plusieurs occluders se trouvent dans le chemin d’accès entre l’utilisateur et le **AudioEmitter**, le volume passthrough est appliqué en feu.

* Dans le **hiérarchie** panneau, sélectionnez **gestionnaires**.
* Dans le **inspecteur** volet, développez **Gestionnaire d’entrée vocale**.
* Dans **Gestionnaire d’entrée vocale**, développez **frais accédez**.
* Modification **aucune fonction** à **PolyActions.GoCharge**.

![mot clé : Accédez de frais](images/gocharge.png)

* Développez **ici**.
* Modification **aucune fonction** à **PolyActions.ComeBack**.

![mot clé : Viens ici](images/comehere.png)

#### <a name="build-and-deploy"></a>Générer et déployer

* Comme précédemment, générez le projet dans Unity et déployés dans Visual Studio.

Une fois que l’application est déployée :

* Par exemple *« Accédez frais »* avoir P0LY Entrez le Hub d’énergie.

Notez le changement dans le son. Cela doit sembler des et un peu plus calme. Si vous êtes en mesure de vous positionner avec un mur ou un autre objet entre vous et le Hub de l’énergie, vous devriez remarquer un muffling supplémentaire du son en raison de l’occlusion par le monde réel.

* Par exemple *« Sont fournis ici »* avoir P0LY laisser le Hub d’énergie et se positionner devant vous.

Notez que l’occlusion audio est supprimée une fois que P0LY quitte le Hub d’énergie. Si vous êtes toujours occlusion d’Audition, P0LY peuvent être bloqués par le monde réel. Essayez de déplacer pour vous assurer une délimitation nette à P0LY.

### <a name="part-3---room-models"></a>Partie 3 : modèles de la salle

#### <a name="key-concepts"></a>Concepts clés

* La taille de l’espace fournit des files d’attente subliminales qui contribuent à la localisation d’un son.
* Modèles de salle sont définies par-**AudioSource**.
* Le [MixedRealityToolkit pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity) fournit du code pour la définition du modèle de la salle.
* Pour des expériences de réalité mixte, sélectionnez le modèle d’espace qui convient le mieux à l’espace du monde réel.

Si vous créez un scénario de réalité virtuelle, sélectionnez le modèle d’espace qui convient le mieux à l’environnement virtuel.

## <a name="chapter-4---sound-design"></a>Chapitre 4 - sonorisation

### <a name="objectives"></a>Objectifs

* Comprendre les considérations relatives à la conception audio efficace.
* Découvrez des techniques et des instructions mixtes.

### <a name="part-1---sound-and-experience-design"></a>Partie 1 : conception de l’expérience et de son

Cette section décrit la bonne clé et de considérations de conception d’expérience et de recommandations.

#### <a name="normalize-all-sounds"></a>Normaliser toutes les sons

Cela évite la nécessité d’un code cas spécial régler les niveaux de volume par son, qui peut prendre du temps et limite la possibilité de mettre à jour facilement des fichiers audio.

#### <a name="design-for-an-untethered-experience"></a>Conception pour une expérience librement

HoloLens est un ordinateur entièrement contenu, librement HOLOGRAPHIQUE. Vos utilisateurs peuvent et utilisera vos expériences lors du déplacement. Veillez à tester votre combinaison audio en parcourant autour.

#### <a name="emit-sound-from-logical-locations-on-your-holograms"></a>Émettre le signal sonore à partir d’emplacements logiques sur votre hologrammes

Dans le monde réel, un chien ne pas écorce de sa fin et les voix d’un humain ne provient pas de son pieds. Évitez d’avoir que votre sons émettent à partir de parties inattendues de votre hologrammes.

Pour hologrammes petits, il est raisonnable d’avoir son émission à partir du centre de la géométrie.

#### <a name="familiar-sounds-are-most-localizable"></a>Sons familiers sont plus localisables

La voix humaine et la musique sont très faciles à localiser. Si quelqu'un appelle votre nom, vous êtes en mesure de déterminer très précisément à partir de quel sens provient de la voix et de l’éloignement. Sons courts et non connus sont plus difficiles à localiser.

#### <a name="be-cognizant-of-user-expectations"></a>Être informé des attentes des utilisateurs

Expérience de la vie joue un rôle dans notre capacité à identifier l’emplacement d’un son. Il s’agit d’une seule raison pour laquelle la voix humaine particulièrement facile à localiser. Il est important de connaître votre appris attentes des utilisateurs lorsque vous placez votre sons.

Par exemple, lorsqu’une personne entend une chanson bird ils généralement recherchent, comme oiseaux ont tendance à être au-dessus de la ligne de vue (flottantes ou dans une arborescence). Il n’est pas rare pour un utilisateur à activer dans la direction correcte d’un son, mais Regarder dans la mauvaise direction verticale et devenir confus ou frustré lorsqu’ils ne peuvent pas trouver l’hologramme.

#### <a name="avoid-hidden-emitters"></a>Éviter les émetteurs masqués

Dans le monde réel, si nous entendre un son, nous pouvons identifier généralement l’objet qui émet le son. Ceci est également valable dans vos expériences. Il peut être très déconcertante pour les utilisateurs et émet un son, de savoir où le son provient et pourra consulter un objet.

Il existe quelques exceptions à cette recommandation. Par exemple, des sons ambiantes comme crickets dans un champ ne sont pas nécessairement visibles. Expérience de la vie nous donne vous êtes familiarisé avec la source de ces sons sans la nécessité pour l’afficher.

### <a name="part-2---sound-mixing"></a>Partie 2 - mixage

#### <a name="target-your-mix-for-70-volume-on-the-hololens"></a>Cibler votre combinaison de volume de 70 % sur le HoloLens

Expériences de réalité mixtes autoriser hologrammes être affichés dans le monde réel. Ils doivent également autoriser sons du monde réel à entendre. Une cible de 70 % volume permet à l’utilisateur d’entendre le monde autour d’elles, ainsi que le son de votre expérience.

#### <a name="hololens-at-100-volume-should-drown-out-external-sounds"></a>HoloLens à 100 % de volume vous noyer doit les sons externes

Un niveau de volume de 100 % équivaut à une expérience de réalité virtuelle. Visuellement, l’utilisateur est transféré vers un monde différent. Les mêmes valable façon audible.

#### <a name="use-the-unity-audiomixer-to-adjust-categories-of-sounds"></a>Utiliser le AudioMixer Unity pour ajuster les catégories de sons

Lorsque vous concevez votre combinaison, il est souvent utile de créer des catégories de sons et ont la possibilité d’augmenter ou diminuer leur volume en tant qu’unité. Cela conserve les niveaux relatifs de chaque signal sonore lors de l’activation rapides et faciles des modifications à la combinaison générale. Incluent des catégories courantes ; effets sonores, ambiance, montages audio et musique de fond.

#### <a name="mix-sounds-based-on-the-users-gaze"></a>Combiner des sons selon le regard de l’utilisateur

Il peut souvent être utile d’en modifier la combinaison de sonore dans votre expérience selon où un utilisateur est (ou n’est pas) la recherche. Une utilisation courante de cette technique sont afin de réduire le niveau de volume pour hologrammes qui se trouvent en dehors de la trame HOLOGRAPHIQUE pour faciliter le travail de l’utilisateur pour vous concentrer sur les informations devant eux. Une autre utilisation consiste à augmenter le volume d’un son pour attirer l’attention de l’utilisateur à un événement important.

#### <a name="building-your-mix"></a>Création de votre combinaison

Lorsque vous générez votre combinaison, il est recommandé de démarrer avec audio d’arrière-plan de votre expérience et ajouter des couches en fonction de l’importance. Souvent, cela entraîne dans chaque couche en cours plus bruyant que le précédent.

Imaginer votre combinaison comme un entonnoir inversé, avec le moins important (et généralement plus calmes sons) en bas, il est recommandé de structurer votre combinaison similaire au diagramme suivant.

![Structure de mixage audio](images/soundlevels.png)

Montages audio sont un scénario intéressant. Basé sur l’expérience que vous créez, vous pouvez avoir un son stéréo (non localisé) ou spatialize votre montages audio. Deux Microsoft a publié des expériences illustrer d’excellents exemples de chaque scénario.

[HoloTour](http://www.microsoft.com/store/p/holotour/9nblggh5pj87) utilise une voix stéréo sur. Lorsque le Narrateur est décrivant l’emplacement en cours de visualisation, le son est cohérent et ne varie pas en position de l’utilisateur. Ainsi, le Narrateur décrire la scène sans prise de sons spatialized de l’environnement.

[Fragments](https://www.microsoft.com/store/p/fragments/9nblggh5ggm8) utilise une voix spatialized sur sous la forme d’un détective. Voix de sa est utilisé pour aider à attirer l’attention de l’utilisateur à un indice important comme si un homme réel a été dans la salle. Cela permet une encore plu judicieux d’immersion dans l’expérience de résolution le mystère.

### <a name="part-3--performance"></a>Partie 3 - performances

#### <a name="cpu-usage"></a>Utilisation du processeur

Lorsque vous utilisez Spatial son, 10-12 émetteurs consomme environ 12 % de l’UC.

#### <a name="stream-long-audio-files"></a>Fichiers audio long Stream

Données audio peuvent être volumineuses, en particulier à des taux d’échantillonnage (kHz 44,1 et 48) courants. Une règle générale est que les fichiers audio plus de 5 à 10 secondes doivent être diffusé en continu afin de réduire l’utilisation mémoire des applications.

Dans Unity, vous pouvez marquer un fichier audio pour la diffusion en continu dans les paramètres d’importation du fichier.

![Paramètres d’importation audio](images/audioimportsettings.png)

## <a name="chapter-5---special-effects"></a>Chapitre 5 - effets spéciaux

### <a name="objectives"></a>Objectifs

* Ajout de profondeur à « Magic Windows ».
* Placer l’utilisateur dans le monde virtuel.

### <a name="magic-windows"></a>Magic Windows

#### <a name="key-concepts"></a>Concepts clés

* Création de vues dans un monde masqué, est visuellement attrayante.
* Améliorer réalisme en ajoutant des effets audio lorsqu’un hologramme ou l’utilisateur est presque le monde masqué.

#### <a name="instructions"></a>Instructions

* Dans le **hiérarchie** volet, développez **HologramCollection** et sélectionnez **Underworld**.
* Développez **Underworld** et sélectionnez **VoiceSource**.
* Dans le **inspecteur** du panneau, cliquez sur **ajouter un composant** et ajoutez **effet de voix utilisateur**.

Un **AudioSource** composant sera ajouté à **VoiceSource**.

* Dans **AudioSource**, affectez la valeur **sortie** à **UserVoice (Mixer)**.
* Vérifier le **Spatialize** case à cocher.
* Faites glisser le **Blend Spatial** curseur jusqu’au **3D**, ou entrez **1** dans la zone d’édition.
* Développez **paramètres audio 3D**.
* Définissez **Doppler niveau** à **0**.
* Dans **effet de voix utilisateur**, affectez la valeur **objet Parent** à la **Underworld** à partir de la scène.
* Définissez **Max Distance** à **1**.

Paramètre **Max Distance** indique **effet de voix utilisateur** comment fermer l’utilisateur doit être l’objet parent avant l’effet est activé.

* Dans **effet de voix utilisateur**, développez **chaleureusement Robert paramètres**.
* Définissez **profondeur** à **0.1**.
* Définissez **appuyez sur 1 Volume**, **appuyez sur le Volume 2** et **appuyez sur le Volume 3** à **0.8**.
* Définissez **d’origine son Volume** à **0,5**.

Les paramètres précédents configurent les paramètres de l’unité **AudioChorusFilter** permettant d’ajouter la richesse de voix de l’utilisateur.

* Dans **effet de voix utilisateur**, développez **Echo paramètres**.
* Définissez **délai** à **300**
* Définissez **Decay, Ratio** à **0.2**.
* Définissez **d’origine son Volume** à **0**.

Les paramètres précédents configurent les paramètres de l’unité **AudioEchoFilter** utilisée pour provoquer la voix de l’utilisateur à renvoyer.

Le script de l’effet de voix utilisateur est chargé de :

* Mesure de la distance entre l’utilisateur et le **GameObject** auquel le script est joint.
* Déterminer si l’utilisateur est accessible sur le **GameObject**.

L’utilisateur doit être accessible sur le GameObject, quelle que soit la distance, pour l’effet doit être activé.

* Application et la configuration un **AudioChorusFilter** et un **AudioEchoFilter** à la **AudioSource**.
* La désactivation de l’effet en désactivant les filtres.

Effet de voix utilisateur utilise le composant de sélecteur de Stream Mic, à partir de la [MixedRealityToolkit pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity), pour sélectionner le flux de voix de haute qualité et de la router système audio d’Unity.

* Dans le **hiérarchie** panneau, sélectionnez **gestionnaires**.
* Dans le **inspecteur** volet, développez **Gestionnaire d’entrée vocale**.
* Dans **Gestionnaire d’entrée vocale**, développez **Underworld afficher**.
* Modification **aucune fonction** à **UnderworldBase.OnEnable**.

![mot clé : Afficher Underworld](images/showunderworld.png)

* Développez **masquer Underworld**.
* Modification **aucune fonction** à **UnderworldBase.OnDisable**.

![mot clé : Masquer Underworld](images/hideunderworld.png)

#### <a name="build-and-deploy"></a>Générer et déployer

* Comme précédemment, générez le projet dans Unity et déployés dans Visual Studio.

Une fois que l’application est déployée :

* Sont confrontés à une surface (mur, floor, table) et le say *« Underworld afficher »*.

L’underworld s’affichera et tous les autres hologrammes seront masquées. Si vous ne voyez pas l’underworld, vérifiez que vous êtes confronté à une surface du monde réel.

* Approche à moins de 1 mètre l’hologramme underworld et commencer à parler.

Il existe désormais des effets audio appliqués à votre voix !

* Activer en dehors de l’underworld et notez comment l’effet n’est plus appliqué.
* Par exemple *« Masquer Underworld »* pour masquer l’underworld.

L’underworld est masqué et les hologrammes auparavant masqués réapparaît.

## <a name="the-end"></a>La fin

Félicitations ! Vous avez maintenant terminé **220 Spatial MR : Son spatial**.

Écoutez le monde et faites vivre vos expériences avec son !
