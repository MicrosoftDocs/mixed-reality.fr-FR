---
title: Monsieur le son spatial 220-spatial
description: Suivez cette procédure pas à pas de codage à l’aide de Unity, Visual Studio et HoloLens pour apprendre les concepts de son spatial.
author: keveleigh
ms.author: kurtie
ms.date: 10/22/2019
ms.topic: article
keywords: holotoolkit, mixedrealitytoolkit, mixedrealitytoolkit-Unity, Academy, didacticiel, son spatial
ms.openlocfilehash: a3fc054927d73cf9ac21f831caa4ec23875977bd
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73434726"
---
>[!NOTE]
>Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.  Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.  Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.  Ils seront conservés pour continuer à travailler sur les appareils pris en charge. [Une nouvelle série de didacticiels](mrlearning-base.md) a été publiée pour HoloLens 2.

<br>

# <a name="mr-spatial-220-spatial-sound"></a>MR spatial 220 : son spatial

Le [son spatial](spatial-sound.md) passe par des hologrammes et leur donne la présence dans notre monde. Les hologrammes sont composés de la lumière et du son, et si vous perdez la vision de vos hologrammes, le son spatial peut vous aider à les trouver. Le son spatial n’est pas comme le son classique que vous entendez sur la radio, il s’agit d’un son positionné dans l’espace 3D. Avec un son spatial, vous pouvez faire en sorte que les hologrammes s’affichent derrière vous, en regard de vous ou même en tête. Dans ce cours, vous allez :

* Configurez votre environnement de développement pour utiliser le son spatial Microsoft.
* Utilisez le son spatial pour améliorer les interactions.
* Utilisez le son spatial conjointement avec le [mappage spatial](spatial-mapping.md).
* Comprendre la conception et la combinaison des meilleures pratiques.
* Utilisez le son pour améliorer les effets spéciaux et amener l’utilisateur dans le monde de la réalité mixte.

## <a name="device-support"></a>Périphériques pris en charge

<table>
<tr>
<th>Course</th><th style="width:150px"> <a href="hololens-hardware-details.md">HoloLens</a></th><th style="width:150px"> <a href="immersive-headset-hardware-details.md">Casques immersifs</a></th>
</tr><tr>
<td>MR spatial 220 : son spatial</td><td style="text-align: center;"> ✔️</td><td style="text-align: center;"> ✔️</td>
</tr>
</table>

## <a name="before-you-start"></a>Avant de commencer

### <a name="prerequisites"></a>Conditions préalables

* Un PC Windows 10 configuré avec les [outils appropriés installés](install-the-tools.md).
* Certaines fonctionnalités C# de programmation de base.
* Vous devez avoir terminé les [notions de base de m. 101](holograms-101.md).
* Un appareil HoloLens [configuré pour le développement](using-visual-studio.md#enabling-developer-mode).

### <a name="project-files"></a>Fichiers projet

* Téléchargez les [fichiers](https://github.com/Microsoft/HolographicAcademy/archive/Holograms-220-SpatialSound.zip) requis par le projet. Requiert Unity 2017,2 ou une version ultérieure.
  * Si vous avez encore besoin de la prise en charge d’Unity 5,6, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.6-220.zip). Cette version n’est peut-être plus à jour.
  * Si vous avez encore besoin de la prise en charge d’Unity 5,5, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.5-220.zip). Cette version n’est peut-être plus à jour.
  * Si vous avez encore besoin de la prise en charge d’Unity 5,4, utilisez [cette version](https://github.com/Microsoft/HolographicAcademy/archive/v1.5.4-220.zip). Cette version n’est peut-être plus à jour.
* Désarchivez les fichiers sur votre bureau ou un autre emplacement facile à atteindre.

>[!NOTE]
>Si vous souhaitez examiner le code source avant le téléchargement, il est [disponible sur GitHub](https://github.com/Microsoft/HolographicAcademy/tree/Holograms-220-SpatialSound).

### <a name="errata-and-notes"></a>Errata et notes

* L’option « Activer Uniquement mon code » doit être désactivée (*décochée*) dans Visual Studio sous outils-> Options-> le débogage pour atteindre les points d’arrêt dans votre code.

## <a name="chapter-1---unity-setup"></a>Chapitre 1-Configuration Unity

### <a name="objectives"></a>Objectifs

* Modifiez la configuration du son de l’unité pour utiliser un son spatial Microsoft.
* Ajoutez du son 3D à un objet dans Unity.

### <a name="instructions"></a>Instructions

* Démarrez Unity.
* Sélectionnez **ouvrir**.
* Accédez à votre bureau et recherchez le dossier que vous avez précédemment désinstallé.
* Cliquez sur le dossier **Starting\Decibel** , puis appuyez sur le bouton **Sélectionner un dossier** .
* Attendez que le projet se charge dans Unity.
* Dans le panneau **projet** , ouvrez **Scenes\Decibel.Unity**.
* Dans le volet **hiérarchie** , développez **HologramCollection** , puis sélectionnez **P0LY**.
* Dans l’inspecteur, développez **audiosource** et Notez qu’il n’y a pas de case à cocher **spatialiser** .

Par défaut, Unity ne charge pas de plug-in Spatializer. Les étapes suivantes permettent d’activer le son spatial dans le projet.

* Dans le menu supérieur de Unity, accédez à **modifier > paramètres du projet > audio**.
* Recherchez la liste déroulante du **plug-in Spatializer** , puis sélectionnez **MS HRTF Spatializer**.
* Dans le volet **hiérarchie** , sélectionnez **HologramCollection > P0LY**.
* Dans le panneau **inspecteur** , recherchez le composant **audio source** .
* Cochez la case **spatialiser** .
* Faites glisser le curseur de **lissage spatial** jusqu’à la forme **3D**, ou entrez **1** dans la zone d’édition.

Nous allons maintenant générer le projet dans Unity et configurer la solution dans Visual Studio.

1. Dans Unity, sélectionnez **fichier > paramètres de build**.
2. Cliquez sur **Ajouter des scènes ouvertes** pour ajouter la scène.
3. Sélectionnez **plateforme Windows universelle** dans la liste **plateforme** , puis cliquez sur **basculer la plateforme**.
4. Si vous développez spécifiquement pour HoloLens, définissez **appareil cible** sur **hololens**. Dans le cas contraire, laissez-le sur **un appareil**.
5. Vérifiez que le **type de build** est défini sur **D3D** et que le **Kit de développement logiciel (SDK** ) est défini sur le **dernier installé** (qui doit être le SDK 16299 ou une version ultérieure).
6. Cliquez sur **Build**.
7. Créez un **dossier** nommé « App ».
8. Cliquez sur le dossier de l' **application** .
9. Appuyez sur **Sélectionner un dossier**.

Lorsque Unity est terminé, une fenêtre de l’Explorateur de fichiers s’affiche.

1. Ouvrez le dossier de l' **application** .
2. Ouvrez la **solution Visual Studio décibels**.

En cas de déploiement dans HoloLens :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x86**.
2. Cliquez sur la flèche déroulante en regard du bouton ordinateur local, puis sélectionnez **ordinateur distant**.
3. Entrez **l’adresse IP de votre appareil HoloLens** et définissez le mode d’authentification sur **universel (protocole non chiffré)** . Cliquez sur **Sélectionner**. Si vous ne connaissez pas l’adresse IP de votre appareil, accédez à **paramètres > réseau & Internet > options avancées**.
4. Dans la barre de menus supérieure, cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**. S’il s’agit de la première fois que vous déployez sur votre appareil, vous devrez le [coupler à Visual Studio](using-visual-studio.md#pairing-your-device).

En cas de déploiement sur un casque immersif :

1. À l’aide de la barre d’outils supérieure dans Visual Studio, remplacez la cible Debug par **Release** et de ARM par **x64**.
2. Assurez-vous que la cible de déploiement est définie sur **ordinateur local**.
3. Dans la barre de menus supérieure, cliquez sur **Déboguer-> exécuter sans débogage** ou appuyez sur **CTRL + F5**.

## <a name="chapter-2---spatial-sound-and-interaction"></a>Chapitre 2-sons spatiaux et interaction

### <a name="objectives"></a>Objectifs

* Améliorez le réalisme des hologrammes à l’aide du son.
* Dirigez le point de regard de l’utilisateur à l’aide du son.
* Fournir des commentaires de mouvement en utilisant le son.

### <a name="part-1---enhancing-realism"></a>Partie 1-amélioration du réalisme

#### <a name="key-concepts"></a>Concepts clés

* Spatialer les sons hologrammes.
* Les sources audio doivent être placées à un emplacement approprié sur l’hologramme.

L’emplacement approprié pour le son va dépendre de l’hologramme. Par exemple, si l’hologramme est un homme, la source du son doit être située près de la bouche et non pas des pieds.

#### <a name="instructions"></a>Instructions

Les instructions suivantes attachent un son spatial à un hologramme.

* Dans le volet **hiérarchie** , développez **HologramCollection** , puis sélectionnez **P0LY**.
* Dans le volet de l' **inspecteur** , dans le **audiosource**, cliquez sur le cercle en regard de **Audioclip** et sélectionnez **polypointer** dans la fenêtre contextuelle.
* Cliquez sur le cercle en regard de **sortie** et sélectionnez **SoundEffects** dans la fenêtre contextuelle.

Project décibel utilise un composant Unity **audiomixer** pour permettre l’ajustement des niveaux sonores pour les groupes de sons. En regroupant les sons de cette manière, le volume global peut être ajusté tout en conservant le volume relatif de chaque son.

* Dans le **audiosource**, développez **paramètres audio 3D**.
* Affectez au **niveau Doppler** la valeur **0**.

Le fait de définir le niveau Doppler sur zéro désactive les modifications du pas en raison du mouvement (de l’hologramme ou de l’utilisateur). Un exemple classique de Doppler est un véhicule à déplacement rapide. À mesure que la voiture approche un écouteur stationnaire, la hauteur du moteur augmente. Lorsqu’il passe l’écouteur, le pas à pas est inférieur à la distance.

### <a name="part-2---directing-the-users-gaze"></a>Partie 2 : diriger le regard de l’utilisateur

#### <a name="key-concepts"></a>Concepts clés

* Utilisez le son pour attirer l’attention sur des hologrammes importants.
* Les oreilles vous aident directement là où les yeux doivent ressembler.
* Le cerveau a des attentes apprises.

Un exemple de l’expérience acquise est que les oiseaux sont généralement au-dessus des têtes des êtres humains. Si un utilisateur entend un son oiseau, sa réaction initiale est de rechercher. Le fait de placer un oiseau au-dessous de l’utilisateur peut entraîner une direction correcte du son, mais ne parvient pas à trouver l’hologramme en raison de la nécessité d’effectuer des recherches.

#### <a name="instructions"></a>Instructions

Les instructions suivantes permettent à P0LY de se masquer derrière vous, afin que vous puissiez utiliser le son pour localiser l’hologramme.

* Dans le volet **hiérarchie** , sélectionnez **gestionnaires**.
* Dans le panneau **inspecteur** , recherchez **Gestionnaire d’entrée vocale**.
* Dans le **Gestionnaire d’entrée vocal**, développez **Go Hide**.
* **Ne modifiez aucune fonction** en **polyactions. GoHide**.

![Mot clé : go Hide](images/gohide.png)

### <a name="part-3---gesture-feedback"></a>Partie 3 : commentaires sur les mouvements

#### <a name="key-concepts"></a>Concepts clés

* Fournir à l’utilisateur une confirmation de mouvement positive à l’aide du son
* N’encombrez pas les sons trop bruyants de l’utilisateur
* Les sons subtils fonctionnent mieux : ne assombrissent pas l’expérience

#### <a name="instructions"></a>Instructions

* Dans le volet **hiérarchie** , développez **HologramCollection**.
* Développez **EnergyHub** et sélectionnez **base**.
* Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter un gestionnaire de sons de **geste**.
* Dans **Gestionnaire de sons de geste**, cliquez sur le cercle en regard de l' **élément de navigation démarré** et de la **navigation mise à jour** , puis sélectionnez **RotateClick** dans la fenêtre contextuelle pour les deux.
* Double-cliquez sur « GestureSoundHandler » pour charger dans Visual Studio.

Le gestionnaire de son geste effectue les tâches suivantes :

* Créez et configurez un **audiosource**.
* Placez le **audiosource** à l’emplacement du **gameobject**approprié.
* Lit le **Audioclip** associé au geste.

#### <a name="build-and-deploy"></a>Génération et déploiement

1. Dans Unity, sélectionnez **fichier > paramètres de build**.
2. Cliquez sur **Build**.
3. Cliquez sur le dossier de l' **application** .
4. Appuyez sur **Sélectionner un dossier**.

Vérifiez que la barre d’outils indique « version finale », « x86 » ou « x64 », et « périphérique distant ». Dans le cas contraire, il s’agit de l’instance de codage de Visual Studio. Vous devrez peut-être rouvrir la solution à partir du dossier de l’application.

* Si vous y êtes invité, rechargez les fichiers projet.
* Comme précédemment, déployez à partir de Visual Studio.

Une fois l’application déployée :

* Observez la façon dont le son change au fur et à mesure que vous vous déplacez autour de P0LY.
* Dites *« Go Hide »* pour faire en sorte que P0LY se déplace vers un emplacement derrière vous. Recherchez-le par le son.
* Pointez le regard de la base du hub d’énergie. Appuyez et faites glisser vers la gauche ou vers la droite pour faire pivoter l’hologramme et notez la façon dont le bruit de clic confirme le mouvement.

Remarque : il existe un volet de texte qui s’étiquette avec vous. Elle contient les commandes vocales disponibles que vous pouvez utiliser tout au long de ce cours.

## <a name="chapter-3---spatial-sound-and-spatial-mapping"></a>Chapitre 3-sons spatiaux et mappage spatial

### <a name="objectives"></a>Objectifs

* Confirmez l’interaction entre les hologrammes et le monde réel à l’aide du son.
* Occultait le son à l’aide du monde physique.

### <a name="part-1---physical-world-interaction"></a>Partie 1-interaction du monde physique

#### <a name="key-concepts"></a>Concepts clés

* En général, les objets physiques font l’objet d’un bruit lorsqu’ils rencontrent une surface ou un autre objet.
* Les sons doivent être contextuels dans l’expérience.

Par exemple, la définition d’une tasse sur une table doit rendre un son plus calme que la suppression d’un Boulder sur un morceau de métal.

#### <a name="instructions"></a>Instructions

* Dans le volet **hiérarchie** , développez **HologramCollection**.
* Développez **EnergyHub**, sélectionnez **base**.
* Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajoutez **TAP pour placer le son et l’action**.
* **Appuyez pour placer le son et l’action**:
  * Cochez **Placer le parent sur TAP**.
  * Définissez **son** emplacement sur **place**.
  * Définissez le **son de collecte** sur **Pick**.
  * Appuyez sur le signe + dans le coin inférieur droit, sous à la fois **action de collecte** et **action de placement**. Faites glisser EnergyHub à partir de la scène dans les champs **aucun (objet)** .
    * Sous **action de cueillette**, cliquez sur **aucune fonction** -> **EnergyHubBase** -> **ResetAnimation**.
    * Sous **action de placement**, cliquez sur **aucune fonction** -> **EnergyHubBase** -> **onselect**.

![Appuyez pour placer le son et l’action](images/holograms220-taptoplace.png)

### <a name="part-2---sound-occlusion"></a>Partie 2-occlusion sonore

#### <a name="key-concepts"></a>Concepts clés

* Un son, comme Light, peut être bloqués.

Un exemple classique est un hall de concert. Lorsqu’un écouteur se trouve en dehors du Hall et que la porte est fermée, la musique est atténuée. Il y a également généralement une réduction du volume. Lorsque la porte est ouverte, le spectre complet du son est audible sur le volume réel. Les sons à fréquence élevée sont généralement absorbés plus que les fréquences basses.

#### <a name="instructions"></a>Instructions

* Dans le volet **hiérarchie** , développez **HologramCollection** , puis sélectionnez **P0LY**.
* Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter un **émetteur audio**.

La classe d’émetteur audio fournit les fonctionnalités suivantes :

* Restaure toutes les modifications apportées au volume du **audiosource**.
* Exécute un **physique. RaycastNonAlloc** à partir de la position de l’utilisateur dans la direction du **gameobject** auquel le **AudioEmitter** est attaché.

La méthode RaycastNonAlloc est utilisée comme optimisation des performances pour limiter les allocations, ainsi que le nombre de résultats retournés.

* Pour chaque **IAudioInfluencer** rencontré, appelle la méthode **ApplyEffect** .
* Pour chaque **IAudioInfluencer** précédent qui n’est plus rencontré, appelez la méthode **RemoveEffect** .

Notez que AudioEmitter met à jour les échelles de temps humaines, par opposition à des mises à jour par image. Cela est dû au fait que les êtres humains ne se déplacent pas suffisamment rapidement pour que l’effet doive être mis à jour plus fréquemment que chaque trimestre ou moitié de seconde. Les hologrammes qui se téléportent rapidement d’un emplacement à un autre peuvent briser l’illusion.

* Dans le volet **hiérarchie** , développez **HologramCollection**.
* Développez **EnergyHub** , puis sélectionnez **BlobOutside**.
* Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter des **OCCLUDER audio**.
* Dans **OCCLUDER audio**, définissez la **fréquence de coupure** sur **1500**.

Ce paramètre limite les fréquences AudioSource à 1500 Hz et inférieures.

* Définissez **passage du volume** à **0,9**.

Ce paramètre réduit le volume du AudioSource à 90% de son niveau actuel.

L’audio OCCLUDER implémente IAudioInfluencer pour :

* Appliquez un effet d’occlusion à l’aide d’un **AudioLowPassFilter** qui est attaché à **audiosource** Managed buy the **AudioEmitter**.
* Applique l’atténuation du volume à AudioSource.
* Désactive l’effet en définissant une fréquence de coupure neutre et en désactivant le filtre.

La fréquence utilisée est neutre est 22 kHz (22000 Hz). Cette fréquence a été choisie car elle se trouve au-dessus de la fréquence maximale nominale pouvant être entendue par l’oreille humaine, ce qui n’a aucun impact perceptible sur le son.

* Dans le volet **hiérarchie** , sélectionnez **SpatialMapping**.
* Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter des **OCCLUDER audio**.
* Dans **OCCLUDER audio**, définissez la **fréquence de coupure** sur **750**.

Lorsque plusieurs Occluders se trouvent dans le chemin d’accès entre l’utilisateur et le **AudioEmitter**, la fréquence la plus faible est appliquée au filtre.

* Définissez **passage du volume** à **0,75**.

Lorsque plusieurs Occluders se trouvent dans le chemin d’accès entre l’utilisateur et le **AudioEmitter**, le transfert de volume est appliqué de façon additive.

* Dans le volet **hiérarchie** , sélectionnez **gestionnaires**.
* Dans le panneau **inspecteur** , développez **Gestionnaire d’entrée vocal**.
* Dans le **Gestionnaire d’entrée vocal**, développez **frais Go**.
* **Ne modifiez aucune fonction** en **polyactions. GoCharge**.

![Mot clé : facturation](images/gocharge.png)

* Développez-le **ici**.
* **Ne modifiez aucune fonction** en **polyactions. Comeback**.

![Mot clé : ici](images/comehere.png)

#### <a name="build-and-deploy"></a>Génération et déploiement

* Comme précédemment, générez le projet dans Unity et déployez-le dans Visual Studio.

Une fois l’application déployée :

* Dites *« Go Fact »* pour que P0LY entre dans le hub d’énergie.

Notez la modification du son. Le bruit doit être atténué et un peu plus calme. Si vous êtes en mesure de vous positionner avec un mur ou un autre objet entre vous et le hub d’énergie, vous remarquerez un Muffling supplémentaire du son en raison de l’occlusion par le monde réel.

* Dites *« venez ici »* pour que P0LY laisse le hub d’énergie et se positionne en face de vous.

Notez que l’occlusion sonore est supprimée une fois que P0LY a quitté le hub d’énergie. Si vous entendez encore des occlusions, P0LY peut être bloqués par le monde réel. Essayez de vous assurer que vous disposez d’une ligne de vue claire sur P0LY.

### <a name="part-3---room-models"></a>Partie 3-modèles Room

#### <a name="key-concepts"></a>Concepts clés

* La taille de l’espace fournit des files d’attente subliminal qui contribuent à la localisation du son.
* Les modèles de salle sont définis par**audiosource**.
* Le [MixedRealityToolkit pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity) fournit du code pour définir le modèle de salle.
* Pour les expériences de réalité mixte, sélectionnez le modèle de salle qui correspond le mieux à l’espace de monde réel.

Si vous créez un scénario de réalité virtuelle, sélectionnez le modèle de salle qui correspond le mieux à l’environnement virtuel.

## <a name="chapter-4---sound-design"></a>Chapitre 4-conception du son

### <a name="objectives"></a>Objectifs

* Comprendre les considérations relatives à la conception d’un son efficace.
* Apprenez à mélanger les techniques et les recommandations.

### <a name="part-1---sound-and-experience-design"></a>Partie 1 : conception du son et de l’expérience

Cette section décrit les considérations et les recommandations relatives à la conception du son et de l’expérience.

#### <a name="normalize-all-sounds"></a>Normaliser tous les sons

Cela évite d’avoir à utiliser un code de cas particulier pour ajuster les niveaux de volume par son, ce qui peut prendre du temps et limiter la possibilité de mettre à jour facilement des fichiers audio.

#### <a name="design-for-an-untethered-experience"></a>Conception pour une expérience non attachée

HoloLens est un ordinateur holographique entièrement contenu et non attaché. Vos utilisateurs peuvent et utiliseront vos expériences pendant le déplacement. Veillez à tester votre combinaison audio en vous.

#### <a name="emit-sound-from-logical-locations-on-your-holograms"></a>Émettre du son à partir d’emplacements logiques sur vos hologrammes

Dans le monde réel, un chien n’est pas à l’écorce de sa queue et la voix d’un homme ne provient pas de ses pieds. Évitez que vos sons émettent des parties inattendues de vos hologrammes.

Pour les petits hologrammes, il est raisonnable d’émettre un son à partir du centre de la géométrie.

#### <a name="familiar-sounds-are-most-localizable"></a>Les sons habituels sont plus localisables

La voix humaine et la musique sont très faciles à localiser. Si quelqu’un appelle votre nom, vous pouvez déterminer très précisément le sens de la voix et à quel moment. Les sons peu familiers sont plus difficiles à localiser.

#### <a name="be-cognizant-of-user-expectations"></a>Être Cognizant des attentes de l’utilisateur

L’expérience de vie joue un rôle dans notre capacité à identifier l’emplacement d’un son. C’est l’une des raisons pour lesquelles la voix humaine est particulièrement facile à localiser. Il est important de connaître les attentes de vos utilisateurs lors de la mise en place de vos sons.

Par exemple, quand quelqu’un entend un morceau d’oiseau, il recherche généralement des oiseaux au-dessus de la ligne de vue (volant ou dans une arborescence). Il n’est pas rare pour un utilisateur d’activer la direction correcte d’un son, mais de regarder dans une mauvaise direction verticale et de devenir confus ou frustré lorsqu’ils ne parviennent pas à trouver l’hologramme.

#### <a name="avoid-hidden-emitters"></a>Éviter les émetteurs masqués

Dans le monde réel, si nous entendons un son, nous pouvons généralement identifier l’objet qui émet le son. Cela doit également être vrai dans vos expériences. Il peut être très difficile pour les utilisateurs d’entendre un son, de savoir à quel endroit le son provient et de ne pas voir un objet.

Il existe quelques exceptions à cette règle. Par exemple, les sons ambiants tels que les crickets dans un champ n’ont pas besoin d’être visibles. L’expérience de vie nous permet de vous familiariser avec la source de ces sons sans avoir à le voir.

### <a name="part-2---sound-mixing"></a>Partie 2-mixage audio

#### <a name="target-your-mix-for-70-volume-on-the-hololens"></a>Ciblez votre combinaison pour 70% du volume sur le HoloLens

Les expériences de réalité mixte permettent de voir les hologrammes dans le monde réel. Ils doivent également permettre l’entendre des sons réels. Une cible de volume de 70% permet à l’utilisateur d’entendre le monde autour de lui et du son de votre expérience.

#### <a name="hololens-at-100-volume-should-drown-out-external-sounds"></a>HoloLens à 100% du volume doit être submergé de sons externes

Un niveau de volume de 100% est similaire à une expérience de réalité virtuelle. Visuellement, l’utilisateur est transporté vers un autre monde. Il en va de même de la même façon audible.

#### <a name="use-the-unity-audiomixer-to-adjust-categories-of-sounds"></a>Utiliser Unity AudioMixer pour ajuster les catégories de sons

Lors de la conception de votre combinaison, il est souvent utile de créer des catégories de son et d’augmenter ou de réduire leur volume en tant qu’unité. Cela permet de conserver les niveaux relatifs de chaque son tout en permettant de modifier rapidement et facilement la combinaison globale. Les catégories courantes incluent ; effets sonores, ambiance, voix et musique en arrière-plan.

#### <a name="mix-sounds-based-on-the-users-gaze"></a>Mélanger des sons en fonction du point de regard de l’utilisateur

Il peut souvent être utile de modifier la combinaison de sons dans votre expérience en fonction de l’endroit où un utilisateur est (ou n’est pas) à l’origine de la recherche. Une utilisation courante de cette technique consiste à réduire le volume des hologrammes qui se trouvent en dehors du cadre holographique pour permettre à l’utilisateur de se concentrer plus facilement sur les informations qu’il contient. Une autre utilisation consiste à augmenter le volume d’un son pour attirer l’attention de l’utilisateur sur un événement important.

#### <a name="building-your-mix"></a>Conception de votre combinaison

Lors de la création de votre combinaison, il est recommandé de commencer par l’audio d’arrière-plan de votre expérience et d’ajouter des couches en fonction de leur importance. Souvent, cela entraîne une couche plus forte que la précédente.

En imaginant votre combinaison comme un entonnoir inversé, avec les moins importants (et généralement les plus calmes) en bas, il est recommandé de structurer votre combinaison comme dans le diagramme suivant.

![Structure de combinaison de sons](images/soundlevels.png)

Les fonctionnalités vocales sont un scénario intéressant. En fonction de l’expérience que vous créez, vous souhaiterez peut-être avoir un son stéréo (non localisé) ou pour spatialer votre voix. Deux expériences Microsoft publiées illustrent des exemples excellents de chaque scénario.

[HoloTour](https://www.microsoft.com/store/p/holotour/9nblggh5pj87) utilise une voix stéréo. Lorsque le narrateur décrit l’emplacement affiché, le son est cohérent et ne varie pas en fonction de la position de l’utilisateur. Cela permet au narrateur de décrire la scène sans sortir des sons spatiaux de l’environnement.

Les [fragments](https://www.microsoft.com/store/p/fragments/9nblggh5ggm8) utilisent une voix spatiale sous la forme d’un détective. La voix du détective est utilisée pour attirer l’attention de l’utilisateur sur un indice important comme si un humain réel était dans la pièce. Cela permet un sens encore plus important de l’immersion dans l’expérience de résolution du mystère.

### <a name="part-3--performance"></a>Partie 3-performances

#### <a name="cpu-usage"></a>Utilisation du processeur

Lorsque vous utilisez un son spatial, 10-12 émetteurs consomment environ 12% du processeur.

#### <a name="stream-long-audio-files"></a>Diffuser des fichiers audio longs

Les données audio peuvent être volumineuses, en particulier aux taux d’échantillonnage courants (44,1 et 48 kHz). Une règle générale est que les fichiers audio d’une durée supérieure à 5-10 secondes doivent être diffusés en continu pour réduire l’utilisation de la mémoire de l’application.

Dans Unity, vous pouvez marquer un fichier audio pour la diffusion en continu dans les paramètres d’importation du fichier.

![Paramètres d’importation audio](images/audioimportsettings.png)

## <a name="chapter-5---special-effects"></a>Chapitre 5-effets spéciaux

### <a name="objectives"></a>Objectifs

* Ajoutez une profondeur à « Magic Windows ».
* Mettez l’utilisateur dans le monde virtuel.

### <a name="magic-windows"></a>Magic Windows

#### <a name="key-concepts"></a>Concepts clés

* La création d’affichages dans un monde masqué, est visuellement attrayante.
* Améliorez le réalisme en ajoutant des effets audio quand un hologramme ou l’utilisateur est proche du monde masqué.

#### <a name="instructions"></a>Instructions

* Dans le volet **hiérarchie** , développez **HologramCollection** , puis sélectionnez **subworld**.
* Développez le sous- **monde** et sélectionnez **VoiceSource**.
* Dans le panneau **inspecteur** , cliquez sur **Ajouter un composant** et ajouter un **effet utilisateur vocal**.

Un composant **audiosource** sera ajouté à **VoiceSource**.

* Dans **audiosource**, définissez **sortie** sur **UserVoice (Mixer)** .
* Cochez la case **spatialiser** .
* Faites glisser le curseur de **lissage spatial** jusqu’à la forme **3D**, ou entrez **1** dans la zone d’édition.
* Développez **paramètres audio 3D**.
* Affectez au **niveau Doppler** la valeur **0**.
* Dans l' **effet utilisateur vocal**, définissez l' **objet parent** sur le sous- **monde** à partir de la scène.
* Définissez **distance maximale** sur **1**.

La définition de la **distance maximale** indique à l' **utilisateur** qu’il doit être l’objet parent avant l’activation de l’effet.

* Dans **effet vocal**de l’utilisateur, développez **paramètres de chœur**.
* Définissez **profondeur** sur **0,1**.
* Définissez **Tap 1 volume**, **Appuyez sur 2 volume** , puis **sur 3 volumes** jusqu’à **0,8**.
* Définissez le **volume de son original** sur **0,5**.

Les paramètres précédents configurent les paramètres du **AudioChorusFilter** Unity utilisé pour ajouter la richesse à la voix de l’utilisateur.

* Dans l' **effet utilisateur vocal**, développez **paramètres Echo**.
* Définir le **délai** sur **300**
* Définissez le **taux d’atténuation** sur **0,2**.
* Définissez le **volume de son original** sur **0**.

Les paramètres précédents configurent les paramètres du **AudioEchoFilter** Unity utilisé pour faire écho à la voix de l’utilisateur.

Le script de l’effet utilisateur vocal est chargé des opérations suivantes :

* Mesure de la distance entre l’utilisateur et le **gameobject** auquel le script est attaché.
* Déterminer si l’utilisateur est confronté au **gameobject**.

L’utilisateur doit être orienté GameObject, quelle que soit la distance, pour que l’effet soit activé.

* Application et configuration d’un **AudioChorusFilter** et d’un **AudioEchoFilter** à **audiosource**.
* La désactivation de l’effet en désactivant les filtres.

L’effet User Voice utilise le composant sélecteur de flux MIC, à partir du [MixedRealityToolkit pour Unity](https://github.com/Microsoft/MixedRealityToolkit-Unity), pour sélectionner le flux vocal de haute qualité et l’acheminer dans le système audio Unity.

* Dans le volet **hiérarchie** , sélectionnez **gestionnaires**.
* Dans le panneau **inspecteur** , développez **Gestionnaire d’entrée vocal**.
* Dans le **Gestionnaire d’entrée vocal**, développez afficher le sous- **monde**.
* **Ne modifiez aucune fonction** en **UnderworldBase. OnEnable**.

![Mot clé : afficher le sous-monde](images/showunderworld.png)

* Développez masquer le sous- **monde**.
* **Ne modifiez aucune fonction** en **UnderworldBase. OnDisable**.

![Mot clé : masquer le sous-monde](images/hideunderworld.png)

#### <a name="build-and-deploy"></a>Génération et déploiement

* Comme précédemment, générez le projet dans Unity et déployez-le dans Visual Studio.

Une fois l’application déployée :

* Face à une surface (mur, plancher, table) et dites *« afficher le monde »* .

Le sous-monde s’affiche et tous les autres hologrammes sont masqués. Si vous ne voyez pas le sous-monde, assurez-vous que vous êtes face à une surface réaliste.

* Approche à l’intérieur d’un compteur de l’hologramme de la planète et commencer à parler.

Des effets audio sont désormais appliqués à votre voix.

* Quittez le sous-monde et notez la façon dont l’effet n’est plus appliqué.
* Dites *« masquer le monde »* pour masquer le sous-monde.

Le sous-monde est masqué et les hologrammes précédemment masqués réapparaissent.

## <a name="the-end"></a>La fin

Félicitations ! Vous avez maintenant terminé le **son spatial 220 : spatial**.

Écoutez l’univers et donnez vie à vos expériences !
