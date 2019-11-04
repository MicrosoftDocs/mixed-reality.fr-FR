---
title: Envoi d’une application au Microsoft Store
description: Cet article propose des conseils sur la soumission de vos applications de réalité mixte au Microsoft Store, y compris comment empaqueter et tester votre application, ainsi que des conseils pour transmettre la certification et faciliter la découverte de votre application dans le Windows Store.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: application, UWP, envoyer, envoi, filtres, métadonnées, configuration système requise, Mots clés, wack, certification, package, AppX, merchandising
ms.openlocfilehash: 63377239498319e84666ba0dbdbe36ce626901c5
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437437"
---
# <a name="submitting-an-app-to-the-microsoft-store"></a>Envoi d’une application au Microsoft Store

[HoloLens](hololens-hardware-details.md) et le PC Windows 10 qui alimentent votre [casque immersif](immersive-headset-hardware-details.md) s’exécutent plateforme Windows universelle applications. Que vous soumettez une application qui prend en charge HoloLens ou PC (ou les deux), vous soumettez votre application au Microsoft Store via l' [espace partenaires](https://partner.microsoft.com/dashboard).

Si vous n’avez pas encore de compte de développeur d’espace partenaires, vous pouvez vous [inscrire dès aujourd’hui](https://developer.microsoft.com/store/register).

## <a name="packaging-a-mixed-reality-app"></a>Empaquetage d’une application de réalité mixte

### <a name="prepare-image-assets-included-in-the-appx"></a>Préparer les ressources d’image incluses dans le AppX

Les outils de génération AppX requièrent plusieurs ressources d’image pour générer votre application dans un package AppX à envoyer au magasin. Vous pouvez en savoir plus sur [les instructions relatives aux ressources de vignettes et d’icônes](https://msdn.microsoft.com/library/windows/apps/mt412102.aspx) sur MSDN.

| Élément multimédia requis | Mise à l’échelle recommandée | Format d’image | Où cela s’affiche-t-il ? | 
|----------|----------|----------|------------------|
| Logo carré 71 x 71 | Indéfini |  PNG | N/A | 
| Logo carré 150 x 150 | 150 x 150 (échelle de 100%) ou 225x225 (échelle de 150%) | PNG | Démarrer les codes confidentiels et toutes les applications (si 310 x 310 n’est pas fourni), stocker les suggestions de recherche, la page de liste des boutiques, Store Browse, Store Search | 
|  Logo 310 étendu |  Indéfini  |  PNG  |  N/A | 
|  Logo de la boutique |  75x75 (échelle de 150%)  |  PNG  |  Espace partenaires, application de rapport, rédiger un avis, ma bibliothèque | 
|  Écran de démarrage |  930x450 (échelle de 150%)  |  PNG  |  lanceur d’applications 2D (ardoise) | 

HoloLens peut également tirer parti des ressources recommandées.

| Ressources recommandées | Mise à l’échelle recommandée | Où cela s’affiche-t-il ? | 
|----------|----------|----------|
|  Logo carré 310 x 310 |  310 x 310 (échelle de 150%) |  Démarrer les épingles et toutes les applications | 

### <a name="live-tile-requirements"></a>Exigences relatives aux vignettes dynamiques

Le menu Démarrer sur HoloLens utilise l’image de vignette carrée la plus grande incluse.

Vous pouvez constater que certaines applications publiées par Microsoft disposent d’un lanceur en 3D pour leur application. Les développeurs peuvent ajouter un lanceur 3D pour leur application à l’aide de [ces instructions](implementing-3d-app-launchers.md).

### <a name="specifying-target-and-minimum-version-of-windows"></a>Spécification de la version cible et minimale de Windows

Si votre application de réalité mixte comprend des fonctionnalités spécifiques à une certaine version de Windows, il est important de spécifier les versions de plateforme minimale et cible que votre application Windows universelle prendra en charge.

**Cela est particulièrement vrai pour les applications ciblant des [casques immersifs Windows Mixed Reality](immersive-headset-hardware-details.md), qui nécessitent au moins la mise à jour de Windows 10 automne Creators (10,0 ; Build 16299) pour fonctionner correctement.**

Vous serez invité à définir la version cible et la version minimale de Windows lorsque vous créerez un projet Windows universel dans Visual Studio. Vous pouvez également modifier ce paramètre pour un projet existant dans le menu « projet », puis « < les propriétés de > de votre nom d’application » en bas du menu déroulant.

![définir les versions de plateforme minimale et cible dans Visual Studio 2019](images/visual-studio-min-version-500px.png)<br>
Définir les versions de plateforme minimale et cible dans Visual Studio

### <a name="specifying-target-device-families"></a>Spécification des familles d’appareils cibles

Les applications Windows Mixed Reality (à la fois pour [HoloLens](hololens-hardware-details.md) et les [casques immersifs](immersive-headset-hardware-details.md)) font partie du plateforme Windows universelle. par conséquent, tout package d’application avec une [famille d’appareils cibles](https://msdn.microsoft.com/library/windows/apps/dn986903.aspx) « Windows. Universal » est en mesure de s’exécuter sur HoloLens ou PC Windows 10 avec des casques immersifs. Cela dit, si vous ne spécifiez pas de famille d’appareils cibles dans votre manifeste d’application, vous pouvez ouvrir par inadvertance votre application sur des appareils Windows 10 inattendus. Suivez les étapes ci-dessous pour spécifier la famille d’appareils Windows 10 prévue, puis [double-Vérifiez que les familles d’appareils appropriées sont sélectionnées lorsque vous téléchargez votre package d’application dans l’espace partenaires pour le soumettre au Store.](submitting-an-app-to-the-microsoft-store.md#submitting-your-mixed-reality-app-to-the-store)

Pour définir ce champ dans Visual Studio, cliquez avec le bouton droit sur package. appxmanifest, sélectionnez Afficher le code, puis recherchez le champ nom du TargetDeviceFamily. Par défaut, il peut se présenter comme suit :

```
<Dependencies>
   <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10586.0" />
</Dependencies>
```

Si votre application est créée pour **hololens**, vous pouvez vous assurer qu’elle est installée uniquement sur hololens en spécifiant une famille d’appareils cibles « Windows. holographique ». 

```
<Dependencies>
   <TargetDeviceFamily Name="Windows.Holographic" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10586.0" />
</Dependencies>
```

Si votre application est créée pour des **casques immersif Windows Mixed Reality**, vous pouvez vous assurer qu’elle est installée uniquement sur les PC Windows 10 avec la mise à jour Windows 10 automne Creators (nécessaire pour Windows Mixed Reality) en spécifiant une famille d’appareils cibles « Windows. Desktop» et MinVersion de « 10.0.16299.0 ».

```
<Dependencies>
   <TargetDeviceFamily Name="Windows.Desktop" MinVersion="10.0.16299.0" MaxVersionTested="10.0.16299.0" />
</Dependencies>
```

Enfin, si votre application est destinée à s’exécuter à la fois sur les **casques Windows HoloLens et Windows Mixed realing**, vous pouvez vous assurer que l’application est uniquement disponible pour ces deux familles d’appareils et garantir que chaque cible correspond à la version minimale correcte de Windows. y compris une ligne pour chaque famille d’appareils cibles avec son MinVersion respectif.

```
<Dependencies>
   <TargetDeviceFamily Name="Windows.Desktop" MinVersion="10.0.16299.0" MaxVersionTested="10.0.16299.0" />
   <TargetDeviceFamily Name="Windows.Holographic" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10586.0" />
</Dependencies>
```

Vous pouvez en savoir plus sur le ciblage des familles d’appareils en lisant la [documentation TARGETDEVICEFAMILY UWP](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-targetdevicefamily).

### <a name="associate-app-with-the-store"></a>Associer l’application au Windows Store

Dans le menu projet de votre solution Visual Studio, choisissez « Store > associer l’application au Store ». Si vous procédez ainsi, vous pouvez tester les scénarios d’achat et de notification dans votre application. Lorsque vous associez votre application au Windows Store, ces valeurs sont téléchargées dans le fichier manifeste de l’application du projet en cours sur votre ordinateur local :
* Nom complet du package
* Nom du package
* ID de l’éditeur
* Nom complet de l’éditeur
* Version

Si vous remplacez le fichier Package. appxmanifest par défaut en créant un fichier. xml personnalisé pour le manifeste, vous ne pouvez pas associer votre application au Windows Store. Si vous essayez d’associer un fichier manifeste personnalisé à la Banque, un message d’erreur s’affiche.

### <a name="creating-an-upload-package"></a>Création d’un package de téléchargement

Suivez les instructions dans [empaquetage d’applications Windows universelles pour Windows 10](https://msdn.microsoft.com/library/hh454036.aspx#Anchor_2).

La dernière étape de la création d’un package de téléchargement consiste à valider le package à l’aide du [Kit de certification des applications Windows](#windows-app-certification-kit).

Si vous souhaitez ajouter un package spécifiquement pour HoloLens à un produit existant disponible sur d’autres familles d’appareils Windows 10, vous devez également savoir [Comment les numéros de version peuvent avoir un impact sur les packages livrés à des clients spécifiques](https://msdn.microsoft.com/library/windows/apps/mt188602.aspx), et [mode de distribution des packages sur différents systèmes d’exploitation](https://msdn.microsoft.com/library/windows/apps/mt188601.aspx).

L’aide générale est que le package du numéro de version le plus élevé applicable à un appareil est celui distribué par le magasin.

S’il existe un package Windows. Universal et un package Windows. holographique et que le package Windows. Universal a un numéro de version supérieur, un utilisateur HoloLens télécharge le package Windows. Universal version plus élevé au lieu de Windows. holographique Packages. Il existe plusieurs solutions à ce problème :
1. Vérifiez que vos packages spécifiques à la plateforme, tels que Windows. holographique, ont toujours un numéro de version plus élevé que vos packages agnostiques de plateforme, tels que Windows. Universal
2. N’Empaquetez pas d’applications sous Windows. Universal si vous avez également des packages spécifiques à la plateforme. Empaquetez plutôt le package Windows. Universal pour les plateformes spécifiques pour lesquelles vous souhaitez qu’il soit disponible

>[!NOTE]
> Vous pouvez déclarer un package unique pour qu’il s’applique à plusieurs familles d’appareils cibles.

3. Créez un package Windows. Universal unique qui fonctionne sur toutes les plateformes. La prise en charge de ce n’est pas très bonne pour l’instant. les solutions ci-dessus sont donc recommandées.

## <a name="testing-your-app"></a>Test de votre application

### <a name="windows-app-certification-kit"></a>Kit de certification des applications Windows

Lorsque vous créez des packages d’application à envoyer à l’espace partenaires à l’aide de Visual Studio, l’assistant créer des packages d’application vous invite à exécuter le kit de certification des applications Windows sur les packages créés. Pour avoir un processus de soumission fluide au magasin, il est préférable de vérifier que les tests du [Kit de certification des applications Windows sont effectués](https://msdn.microsoft.com/library/windows/apps/jj657973.aspx) sur votre application sur votre ordinateur local avant de les soumettre au Windows Store. L’exécution du kit de certification des applications Windows sur un HoloLens distant n’est pas prise en charge actuellement.

### <a name="run-on-all-targeted-device-families"></a>Exécuter sur toutes les familles d’appareils ciblées

La plateforme Windows universelle vous permet de créer une application unique qui s’exécute sur toutes les familles d’appareils Windows 10. Toutefois, cela ne garantit pas que les applications Windows universelles fonctionnent uniquement sur toutes les familles d’appareils. Avant de choisir de rendre votre application disponible sur HoloLens ou sur toute autre famille d’appareils cibles Windows 10, il est important que vous [testiez l’application](testing-your-app-on-hololens.md) sur chacune de ces familles d’appareils pour garantir une bonne expérience.

## <a name="submitting-your-mixed-reality-app-to-the-store"></a>Envoi de votre application de réalité mixte au Store

Si vous soumettez une application de réalité mixte basée sur un projet Unity, consultez d’abord cette [vidéo](https://channel9.msdn.com/Blogs/One-Dev-Minute/How-to-publish-your-Unity-game-as-a-UWP-app) .

En général, la soumission d’une application Windows Mixed Reality qui fonctionne sur HoloLens et/ou des casques immersifs revient à envoyer une application UWP au Microsoft Store. Une fois que vous avez [créé votre application en réservant son nom](https://docs.microsoft.com/windows/uwp/publish/create-your-app-by-reserving-a-name), vous devez suivre la [liste de contrôle de soumission UWP](https://docs.microsoft.com/windows/uwp/publish/app-submissions).

L’une des premières choses à faire est de [Sélectionner une catégorie et une sous-catégorie](https://docs.microsoft.com/windows/uwp/publish/category-and-subcategory-table) pour votre expérience de réalité mixte. Il est important de **choisir la catégorie la plus précise pour votre** application afin que nous puissions faire de votre application dans les catégories de magasins appropriées et vous assurer qu’elle s’affiche à l’aide des requêtes de recherche pertinentes. **Le fait de répertorier votre titre de VR en tant que jeu n’entraîne pas une meilleure exposition pour votre application** et peut l’empêcher de s’afficher dans des catégories qui sont plus adaptées et moins encombrées.

Toutefois, il existe quatre domaines clés dans le processus de soumission où vous souhaiterez effectuer des sélections spécifiques à la réalité mixte :
1. Dans la section **[déclarations de produit](submitting-an-app-to-the-microsoft-store.md#mixed-reality-product-declarations)** , sous [Propriétés](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties).
2. Dans la section **[System Requirements](submitting-an-app-to-the-microsoft-store.md#mixed-reality-system-requirements)** sous [Properties (propriétés](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties)).
3. Dans la section disponibilité de la **[famille d’appareils](submitting-an-app-to-the-microsoft-store.md#device-family-availability)** , sous [packages](https://docs.microsoft.com/windows/uwp/publish/upload-app-packages).
4. Dans plusieurs champs de la **[page de liste des boutiques](submitting-an-app-to-the-microsoft-store.md#store-listing-page)** .

### <a name="mixed-reality-product-declarations"></a>Déclarations de produit de réalité mixte

Sur la page **[Propriétés](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties)** du processus d’envoi de l’application, vous trouverez plusieurs options relatives à la réalité mixte dans la section **[déclarations de produit](https://docs.microsoft.com/windows/uwp/publish/app-declarations)** .

![les déclarations de produit de réalité mixte](images/product-declarations-900px.png)<br>
Déclarations de produit de réalité mixte

Tout d’abord, vous voudrez identifier les types d’appareils pour lesquels votre application offre une expérience de réalité mixte. Cela garantit que votre application est incluse dans les collections de réalité mixte de Windows dans le magasin et qu’elle est exposée aux utilisateurs qui parcourent le magasin après avoir connecté un casque immersif (ou lorsque vous parcourez le magasin sur HoloLens).

En regard de « cette expérience a été conçue pour Windows Mixed Reality sur : »
* Cochez la case **PC** uniquement si votre application offre une expérience VR lorsqu’un casque immersif est connecté au PC de l’utilisateur. Vous devez cocher cette case si votre application est conçue exclusivement pour s’exécuter sur un casque immersif ou s’il s’agit d’un jeu/application PC standard qui offre un mode de réalité mixte et/ou du contenu bonus quand un casque est connecté.
* Vérifiez la zone **HoloLens** uniquement si votre application offre une expérience holographique lorsqu’elle est exécutée sur HoloLens.
* Cochez **les deux** cases si votre application offre une expérience de réalité mixte sur les deux types d’appareils, comme l' [application « Project Island](mixed-reality-250.md) » de la réalité mixte, à partir de la build 2017.

Si vous avez sélectionné « PC » ci-dessus, vous devez définir la « configuration de la réalité mixte » (niveau d’activité). Cela s’applique uniquement aux expériences de réalité mixte qui s’exécutent sur des PC connectés à des casques immersifs, car les applications de réalité mixte sur HoloLens sont à l’échelle mondiale et l’utilisateur ne définit pas de limite lors de l’installation.
* Choisissez **assis + debout** si votre application est conçue dans le but que l’utilisateur reste à une position (un exemple serait un jeu dans lequel vous êtes assis dans un cockpit d’un avion).
* Choisissez **toutes les expériences** si votre application est conçue avec l’intention pour l’utilisateur de se déplacer dans les limites qu’il a définies lors de l’installation (un exemple peut être un jeu dans lequel vous allez effectuer des étapes et envisagez d’effectuer des attaques).

### <a name="mixed-reality-system-requirements"></a>Configuration système requise pour la réalité mixte

Sur la page **[Propriétés](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties)** du processus d’envoi de l’application, vous trouverez plusieurs options relatives à la réalité mixte dans la section **[Configuration système requise](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties#system-requirements)** .

![Configuration système requise](images/system-reqs-800px.png)<br>
Configuration requise

Dans cette section, vous allez identifier le matériel minimal (obligatoire) et le matériel recommandé (facultatif) pour votre application de réalité mixte.

**Matériel d’entrée :**

Utilisez les cases à cocher pour indiquer aux clients potentiels si votre application prend en charge les contrôleurs de mouvement du **microphone** (pour les [entrées vocales](voice-input.md)), du **[contrôleur Xbox ou du boîtier de commande](hardware-accessories.md#bluetooth-gamepads)** et/ou de **[Windows Mixed Reality](motion-controllers.md)** . Ces informations seront exposées dans la page de détails du produit de votre application dans le Store et vous aideront à faire figurer votre application dans les collections d’applications/jeux appropriées (par exemple, une collection peut exister pour tous les jeux qui prennent en charge les contrôleurs de mouvement).

Veillez à sélectionner des cases à cocher pour « matériel minimum » ou « matériel recommandé » pour les types d’entrée. 

Exemple : 
* Si votre jeu nécessite des contrôleurs de mouvement, mais accepte les entrées vocales via le microphone, activez la case à cocher « matériel minimal » en regard de « contrôleurs de mouvement Windows Mixed Reality », mais la case à cocher « matériel recommandé » en regard de « microphone ». 
* Si votre jeu peut être lu avec un contrôleur/boîtier de commande Xbox, vous pouvez activer la case à cocher « matériel minimal » en regard de « contrôleur Xbox ou boîtier d’emballage », puis activer la case à cocher « matériel recommandé » en regard de « mouvement de réalité mixte Windows ». comme les contrôleurs de mouvement, les contrôleurs de mouvement offriront probablement un pas à pas détaillé dans l’expérience du boîtier.

**Casque immersif Windows Mixed Reality :**

Le fait d’indiquer si un casque immersif est nécessaire pour utiliser votre application ou est facultatif, est essentiel à la satisfaction des clients et à l’éducation.

Si votre application ne peut être utilisée *qu'* avec un casque immersif, activez la case à cocher « matériel minimal » en regard de « casque Windows mixte en réalité ». Elle sera exposée dans la page des détails du produit de votre application dans le Store sous la forme d’un avertissement au-dessus du bouton d’achat, de sorte que les clients ne pensent pas qu’ils achètent une application qui fonctionnera sur leur ordinateur comme une application de bureau traditionnelle.

Si votre application s’exécute sur le bureau comme une application PC traditionnelle, mais offre une expérience VR quand un casque immersif est connecté (que le contenu complet de votre application soit disponible ou seulement une partie), cochez la case « matériel recommandé » en regard de « Windows Mixed Reality ». casque immersif». Aucun avertissement ne sera présenté au-dessus du bouton acheter sur la page de détails du produit de votre application si votre application fonctionne comme une application de bureau traditionnelle sans un casque immersif connecté.

**Spécifications du PC :**

Si vous souhaitez que votre application atteigne autant que possible les utilisateurs du casque immersif Windows Mixed Reality, vous souhaiterez [cibler](understanding-performance-for-mixed-reality.md) les spécifications du PC pour les PC [Windows Mixed Reality avec des graphiques intégrés](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines).

Que votre application de réalité mixte cible la configuration minimale requise pour le PC Windows Mixed Reality ou qu’elle nécessite une configuration de PC spécifique (comme le GPU dédié d’un [ultra PC Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)), vous devez l’indiquer avec les spécifications de PC appropriées dans colonne « matériel minimal ».

Si votre application de réalité mixte est conçue pour offrir de meilleures performances ou si vous avez des graphiques de résolution supérieure, sur une configuration de PC ou une carte graphique particulière, vous devez indiquer cela avec les spécifications de PC appropriées dans la colonne « matériel recommandé ».

Cela s’applique uniquement si votre application de réalité mixte utilise un casque immersif connecté à un PC. Si votre application de réalité mixte s’exécute uniquement sur HoloLens, vous n’avez pas besoin d’indiquer les spécifications du PC, car HoloLens n’a qu’une seule configuration matérielle.

### <a name="device-family-availability"></a>Disponibilité de la famille d’appareils

Si vous avez [empaqueté votre application correctement](https://docs.microsoft.com/windows/uwp/publish/app-package-requirements) dans Visual Studio, son chargement dans la page packages du processus d’envoi d’application doit générer une table identifiant les familles de périphériques pour lesquelles votre application sera disponible.

Tableau de disponibilité des familles d’appareils ![](images/device-family-table-900px.png)<br>
Tableau de disponibilité des familles d’appareils

Si votre application de réalité mixte fonctionne sur des casques immersifs, au moins « Windows 10 Desktop » doit être sélectionné dans le tableau. Si votre application de réalité mixte fonctionne sur HoloLens, vous devez sélectionner au moins « Windows 10 holographique ». Si votre application s’exécute sur les deux types de casque Windows Mixed Reality, tels que l' [application « îlot de projet » de la réalité mixte](mixed-reality-250.md), « Windows 10 Desktop » et « Windows 10 holographique » doivent être sélectionnés.

>[!TIP]
>De nombreux développeurs peuvent rencontrer des erreurs lors du chargement du package de leur application liée à des incompatibilités entre le manifeste du package et les informations de votre compte d’application/éditeur dans l’espace partenaires. Vous pouvez souvent éviter ces erreurs en vous connectant à Visual Studio avec le même compte que celui associé à votre compte de développeur Windows (celui que vous utilisez pour vous connecter à l’espace partenaires). Si vous utilisez le même compte, vous pouvez associer votre application à son identité dans le Microsoft Store avant de l’empaqueter.

![associer votre application au Microsoft Store](images/associate-your-app-700px.png)<br>
Associer votre application à l’Microsoft Store dans Visual Studio

### <a name="store-listing-page"></a>Page de la liste des boutiques

Sur la page [Store Listing](https://docs.microsoft.com/windows/uwp/publish/create-app-store-listings) du processus d’envoi d’applications, vous pouvez ajouter des informations utiles sur votre application de réalité mixte à plusieurs endroits.

>[!IMPORTANT]
>Pour vous assurer que votre application est correctement catégorisée par le Store et rendue détectable par les clients Windows Mixed Reality, vous devez ajouter **« Windows Mixed Reality »** comme l’un de vos « termes de recherche » pour l’application (vous pouvez rechercher des termes de recherche en développant les « champs partagés » section).

![ajouter Windows Mixed Reality pour rechercher des termes](images/search-terms-800px.png)<br>
Ajouter « Windows Mixed Reality » aux termes de la recherche

## <a name="offering-a-free-trial-for-your-game-or-app"></a>Offre d’essai gratuit pour votre jeu ou votre application

De nombreux consommateurs n’auront aucune expérience de la réalité virtuelle avant d’acheter un casque immersif Windows Mixed Reality. Ils peuvent ne pas savoir ce qui se passe des jeux intenses et peuvent ne pas être familiarisés avec leur propre seuil de confort dans les expériences immersifs. De nombreux clients peuvent également essayer un casque immersif Windows Mixed Reality sur des PC qui ne sont pas dotés de badges [Windows Mixed Reality PC](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines). En raison de ces considérations, nous vous recommandons vivement de proposer une [version d’évaluation gratuite](https://docs.microsoft.com/windows/uwp/publish/set-app-pricing-and-availability#free-trial) pour votre application ou votre jeu de réalité mixte payant.

## <a name="see-also"></a>Articles associés
* [Réalité mixte](mixed-reality.md)
* [Vue d’ensemble du développement](development.md)
* [Vues d’applications](app-views.md)
* [Comprendre les performances de la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations en matière de performances pour Unity](performance-recommendations-for-unity.md)
* [Test de votre application dans HoloLens](testing-your-app-on-hololens.md)
* [Instructions de compatibilité matérielle PC minimale pour Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)
