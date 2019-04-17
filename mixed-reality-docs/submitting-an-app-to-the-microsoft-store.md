---
title: Soumission d’une application pour le Microsoft Store
description: Cet article propose des conseils sur l’envoi de vos applications de réalité mixte pour le Microsoft Store, y compris comment empaqueter et de tester votre application et les conseils de passer la certification et de faciliter la détectabilité de votre application dans le Store.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: application, uwp, envoyer, envoi, filtres, métadonnées, configuration système requise, mots clés, kit, certification, package, appx, merchandising
ms.openlocfilehash: 4eb69fbaa22f4864305f09d5e1bf1c1860a0d31f
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594571"
---
# <a name="submitting-an-app-to-the-microsoft-store"></a>Soumission d’une application pour le Microsoft Store

Les deux [HoloLens](hololens-hardware-details.md) et les PC Windows 10 mise sous tension votre [casque immersif](immersive-headset-hardware-details.md) exécuter des applications de plateforme Windows universelle. Si vous soumettez une application qui prend en charge de HoloLens ou PC (ou les deux), vous devez soumettre votre application pour le Microsoft Store via [partenaires](https://partner.microsoft.com/dashboard).

Si vous ne disposez pas d’un compte de développeur de partenaires, vous pouvez [Inscrivez-vous aujourd'hui](https://developer.microsoft.com/store/register).

## <a name="packaging-a-mixed-reality-app"></a>Empaquetage d’une application de réalité mixte

### <a name="prepare-image-assets-included-in-the-appx"></a>Préparer les composants inclus dans l’appx de l’image

Il existe plusieurs ressources d’image requis par l’application de création d’outils pour générer votre application dans un package appx envoyer vers le Store. Vous pouvez en savoir plus sur [les instructions pour les ressources en mosaïque et icône](https://msdn.microsoft.com/library/windows/apps/mt412102.aspx) sur MSDN.

| Ressource requise | Mise à l’échelle recommandée | Format d’image | Où s’affiche ? | 
|----------|----------|----------|------------------|
| Logo carré 71 x 71 | Indéfini |  PNG | N/A | 
| Logo carré 150 x 150 | 150 x 150 (mise à l’échelle 100 %) ou 225 x 225 (mise à l’échelle de 150 %) | PNG | Démarrer toutes les applications et les codes confidentiels (si 310 x 310 n’est fourni), Store les Suggestions de recherche, Page de liste de Store, Store Parcourir, recherche de Store | 
|  Rectangulaire 310 x 150 Logo |  Indéfini  |  PNG  |  N/A | 
|  Logo de Store |  75 x 75 (mise à l’échelle de 150 %)  |  PNG  |  Partenaires, d’application de rapport, rédiger une critique, ma bibliothèque | 
|  Écran de démarrage |  930 x 450 (mise à l’échelle de 150 %)  |  PNG  |  Lanceur d’applications 2D (séquence) | 

Il existe également certaines ressources recommandées qui HoloLens peut tirer parti de.

| Ressources recommandées | Mise à l’échelle recommandée | Où s’affiche ? | 
|----------|----------|----------|
|  Logo carré 310 x 310 |  310 x 310 (mise à l’échelle de 150 %) |  Toutes les applications et codes confidentiels de démarrage | 

### <a name="live-tile-requirements"></a>Exigences de vignette dynamiques

Le menu Démarrer sur HoloLens utilisera la plus grande image mosaïque carrée inclus.

Vous pouvez constater que certaines applications publiées par Microsoft ont un lanceur 3D pour leur application. Les développeurs peuvent ajouter un lanceur pour leur application à l’aide de 3D [ces instructions](implementing-3d-app-launchers.md).

### <a name="specifying-target-and-minimum-version-of-windows"></a>En spécifiant la cible et la version minimale de Windows

Si votre application de réalité mixte inclut des fonctionnalités qui sont spécifiques à une version spécifique de Windows, il est important de spécifier la cible et les versions de plateforme minimales qui prend en charge votre application Windows universelle.

**Cela est particulièrement vrai pour les applications ciblant [des casques IMMERSIFS Windows Mixed Reality](immersive-headset-hardware-details.md), qui requiert au moins le de Windows 10 Fall Creators Update (10.0 ; Build 16299) pour fonctionner correctement.**

Vous devrez définir la cible et la version minimale de Windows lorsque vous créez un nouveau projet Windows universel dans Visual Studio. Vous pouvez également modifier ce paramètre pour un projet existant dans le menu « Projet », puis « Propriétés de < nom de votre application > » en bas du menu déroulant.

![Valeur minimale et cibler des versions de plateforme dans Visual Studio 2017](images/visual-studio-min-version-500px.png)<br>
Valeur minimale et cibler des versions de plateforme dans Visual Studio

### <a name="specifying-target-device-families"></a>Spécification des familles de périphériques cibles

Applications de réalité mixte Windows (pour les deux [HoloLens](hololens-hardware-details.md) et [des casques IMMERSIFS](immersive-headset-hardware-details.md)) font partie de la plateforme Windows universelle, par conséquent, n’importe quel package d’application avec un [ciblent la famille de périphériques](https://msdn.microsoft.com/library/windows/apps/dn986903.aspx)de « Windows.Universal » est capable d’exécuter sur HoloLens ou des PC Windows 10 avec des casques IMMERSIFS. Cela étant dit, si vous ne spécifiez pas d’une famille de périphériques cible dans votre manifeste d’application vous pourrez par inadvertance ouvrir votre application jusqu'à des appareils Windows 10. Suivez les étapes ci-dessous pour spécifier la famille de périphériques Windows 10 souhaitée, puis [Vérifiez que les familles de périphériques corrects sont sélectionnés lorsque vous chargez votre package d’application dans le centre de partenaires à envoyer au Store.](submitting-an-app-to-the-microsoft-store.md#submitting-your-mixed-reality-app-to-the-store)

Pour définir ce champ dans Visual Studio, cliquez avec le bouton droit sur le Package.appxmanifest et sélectionnez « Afficher le Code », puis recherchez le champ de nom de TargetDeviceFamily. Par défaut, il peut se présenter comme suit :

```
<Dependencies>
   <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10586.0" />
</Dependencies>
```

Si votre application est créée pour **HoloLens**, puis vous pouvez vous assurer qu’il est installé uniquement sur HoloLens en spécifiant une famille de périphériques cible de « Windows.Holographic ». 

```
<Dependencies>
   <TargetDeviceFamily Name="Windows.Holographic" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10586.0" />
</Dependencies>
```

Si votre application est créée pour **des casques IMMERSIFS Windows Mixed Reality**, puis vous pouvez vous assurer qu’il est installé uniquement sur les PC Windows 10 avec la de Windows 10 Fall Creators Update (nécessaire pour la réalité mixte Windows) en spécifiant une cible famille de périphériques de « Windows.Desktop » et MinVersion de « 10.0.16299.0 ».

```
<Dependencies>
   <TargetDeviceFamily Name="Windows.Desktop" MinVersion="10.0.16299.0" MaxVersionTested="10.0.16299.0" />
</Dependencies>
```

Enfin, si votre application est destinée à s’exécuter sur les deux **HoloLens et Windows Mixed Reality des casques IMMERSIFS**, vous pouvez garantir l’application est uniquement accessible à ces deux familles et simultanément Vérifiez chaque cible correct version minimale de Windows en incluant une ligne pour chaque famille de périphériques cible avec son MinVersion respectif.

```
<Dependencies>
   <TargetDeviceFamily Name="Windows.Desktop" MinVersion="10.0.16299.0" MaxVersionTested="10.0.16299.0" />
   <TargetDeviceFamily Name="Windows.Holographic" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10586.0" />
</Dependencies>
```

Plus d’informations sur le ciblage des familles d’appareils en lisant le [documentation TargetDeviceFamily UWP](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-targetdevicefamily).

### <a name="associate-app-with-the-store"></a>Associer l’application avec le Store

Dans le menu projet dans votre solution Visual Studio, choisissez « Store > associer App avec le Store ». Si vous procédez ainsi, vous pouvez tester des scénarios d’achats et de notification dans votre application. Lorsque vous associez votre application du Store, ces valeurs sont téléchargées dans le fichier manifeste d’application pour le projet actuel sur votre ordinateur local :
* Nom complet du package
* Nom du package
* ID de l’éditeur
* Nom complet de serveur de publication
* Version

Si vous remplacez le fichier package.appxmanifest par défaut en créant un fichier .xml personnalisé pour le manifeste, vous ne pouvez pas associer votre application du Store. Si vous essayez d’associer un fichier manifeste personnalisé avec le Store, vous verrez un message d’erreur.

### <a name="creating-an-upload-package"></a>Création d’un package de téléchargement

Suivez les instructions fournies dans [applications Windows universelles Empaquetage pour Windows 10](https://msdn.microsoft.com/library/hh454036.aspx#Anchor_2).

La dernière étape de création d’un package de téléchargement est la validation du package à l’aide de la [Kit de Certification des applications Windows](#windows-app-certification-kit).

Si vous allez ajouter un package spécifiquement pour HoloLens à un produit existant qui est disponible sur les autres familles d’appareils Windows 10, vous devez également en savoir plus sur [comment les numéros de version peuvent avoir une incidence sur les packages sont remis à des clients spécifiques ](https://msdn.microsoft.com/library/windows/apps/mt188602.aspx), et [comment les packages sont distribués aux différents systèmes d’exploitation](https://msdn.microsoft.com/library/windows/apps/mt188601.aspx).

La recommandation générale est que le package numéro version le plus élevé qui s’applique à un appareil sera distribué par le Store.

S’il existe un package Windows.Universal et un package Windows.Holographic et le package Windows.Universal possède un numéro de version supérieur, un utilisateur de HoloLens télécharge le package de Windows.Universal numéro de version supérieur au lieu du Windows.Holographic package. Il existe plusieurs solutions à ce problème :
1. Vérifiez vos packages spécifiques de plateforme telles que Windows.Holographic ont toujours un numéro de version supérieur à vos packages agnostiques plateforme telles que Windows.Universal
2. Ne créez de package des applications comme Windows.Universal si vous disposez également de packages spécifiques de la plateforme - au lieu de cela dans un package du package Windows.Universal pour les plateformes spécifiques que vous le souhaitez disponible sur

>[!NOTE]
> Vous pouvez déclarer un seul package afin de s’appliquer à plusieurs familles d’appareils cible

3. Créer un package Windows.Universal unique qui fonctionne sur toutes les plateformes. Prise en charge pour ce n’est pas parfaite dès maintenant pour les solutions indiquées ci-dessus sont recommandées.

## <a name="testing-your-app"></a>Test de votre application

### <a name="windows-app-certification-kit"></a>Kit de certification des applications Windows

Lorsque vous créez des packages d’application à envoyer au centre de partenaires via Visual Studio, l’Assistant de créer des Packages d’application vous invitera à exécuter le Kit de Certification des applications Windows sur les packages qui sont créés. Afin d’avoir un processus de soumission smooth au Store, il est préférable de vérifier que le [teste de Kit de Certification des applications Windows](https://msdn.microsoft.com/library/windows/apps/jj657973.aspx) passer par rapport à votre application sur votre ordinateur local avant de les envoyer vers le Store. Le Kit de Certification des applications Windows en cours d’exécution sur un HoloLens à distance n’est pas pris en charge actuellement.

### <a name="run-on-all-targeted-device-families"></a>Exécuter sur toutes les familles de périphérique ciblé

La plateforme universelle Windows vous permet de créer une application unique qui s’exécute sur toutes les familles d’appareils Windows 10. Toutefois, il ne garantit pas que les applications Windows universelles fonctionnent sur toutes les familles d’appareils. Avant de décider de rendre votre application disponible sur HoloLens ou toute autre famille de périphériques de cible Windows 10, il est important que vous avez [tester l’application](testing-your-app-on-hololens.md) sur chacun de ces familles d’appareils pour garantir une bonne expérience.

## <a name="submitting-your-mixed-reality-app-to-the-store"></a>Soumission de votre application de réalité mixte vers le Store

Si vous soumettez une application de réalité mixte est basée sur un projet Unity, consultez ce [vidéo](https://channel9.msdn.com/Blogs/One-Dev-Minute/How-to-publish-your-Unity-game-as-a-UWP-app) première.

En règle générale, les application qui fonctionne sur HoloLens et/ou des casques IMMERSIFS soumettre une réalité mixte Windows s’apparente à envoyer n’importe quelle application UWP du Microsoft Store. Une fois que vous avez [créé votre application en réservant son nom](https://docs.microsoft.com/windows/uwp/publish/create-your-app-by-reserving-a-name), vous devez suivre les [liste de vérification de soumission UWP](https://docs.microsoft.com/windows/uwp/publish/app-submissions).

Une des premières choses que vous effectuerez est [sélectionner une catégorie et sous-catégorie](https://docs.microsoft.com/windows/uwp/publish/category-and-subcategory-table) pour votre expérience de réalité mixte. Il est important que vous avez **choisissez la catégorie la plus précise pour votre application** afin que nous pouvons commercialiser votre application dans les catégories de Store droit et vérifiez qu’il s’affiche à l’aide de requêtes de recherche pertinents. **Répertorier votre titre VR comme une partie n’entraînera une meilleure exposition de votre application,** et peut l’empêcher de s’afficher dans les catégories sont l’ajustement plus et moins encombré.

Toutefois, il existe quatre domaines clés dans le processus de soumission où vous souhaitez effectuer des sélections spécifiques à la réalité mixtes :
1. Dans le **[déclarations de produit](submitting-an-app-to-the-microsoft-store.md#mixed-reality-product-declarations)** section sous [propriétés](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties).
2. Dans le **[requise](submitting-an-app-to-the-microsoft-store.md#mixed-reality-system-requirements)** section sous [propriétés](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties).
3. Dans le **[disponibilité famille du périphérique](submitting-an-app-to-the-microsoft-store.md#device-family-availability)** section sous [Packages](https://docs.microsoft.com/windows/uwp/publish/upload-app-packages).
4. Dans plusieurs le **[page d’annonce Store](submitting-an-app-to-the-microsoft-store.md#store-listing-page)** champs.

### <a name="mixed-reality-product-declarations"></a>Déclarations de produit de réalité mixte

Sur le **[propriétés](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties)** page du processus de soumission d’application, vous trouverez plusieurs options relatives à la réalité mixte dans le **[déclarations de produit](https://docs.microsoft.com/windows/uwp/publish/app-declarations)** section.

![Déclarations de produit de réalité mixte](images/product-declarations-900px.png)<br>
Déclarations de produit de réalité mixte

Tout d’abord, vous voudrez identifier les types d’appareils pour lesquels votre application offre une expérience de réalité mixte. Cela garantit que votre application est incluse dans les collections de réalité mixte Windows dans le Store et qu’il est présenté aux utilisateurs qui parcourent le Store après avoir connecté un casque immersif (ou lorsque vous parcourez le Store sur HoloLens).

Regard » cette expérience est conçue pour la réalité mixte Windows sur : »
* Vérifier le **PC** zone uniquement si votre application offre une expérience de réalité virtuelle quand un casque immersif est connecté au PC de l’utilisateur. Vous devez cocher cette case si votre application est conçue exclusivement pour s’exécuter sur un casque immersif, ou si elle est un standard PC jeu ou une application qui offre un contenu de réalité mixte mode et/ou bonus lorsqu’un casque est connecté.
* Vérifier le **HoloLens** zone uniquement si votre application offre une expérience HOLOGRAPHIQUE lorsqu’il est exécuté sur HoloLens.
* Vérifiez **à la fois** zones si votre application offre une réalité mixte d’expérience sur les deux types d’appareils, comme le [Académie de réalité mixte « Îlot de projet » application](mixed-reality-250.md) à partir de la Build 2017.

Si vous avez sélectionné « PC » ci-dessus, vous voudrez définir des « setup de réalité mixte » (niveau d’activité). Cela s’applique uniquement à des expériences de réalité mixte qui s’exécutent sur des PC connectés à des casques IMMERSIFS, comme les applications de réalité mixte sur HoloLens sont à l’échelle mondiale et l’utilisateur ne définit pas une limite pendant l’installation.
* Choisissez **assis ! + debout** si votre application est conçue avec l’intention de l’utilisateur reste dans une position (un exemple serait un jeu où vous êtes assis dans un cockpit d’un avion).
* Choisissez **toutes les expériences** si votre application est conçue avec l’intention de l’utilisateur parcourt autour dans la limite, il ou elle définie pendant l’installation (un exemple peut être un jeu où vous côté-étape et canard pour éliminer les attaques).

### <a name="mixed-reality-system-requirements"></a>Réalité mixte requise

Sur le **[propriétés](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties)** page du processus de soumission d’application, vous trouverez plusieurs options relatives à la réalité mixte dans le **[requise](https://docs.microsoft.com/windows/uwp/publish/enter-app-properties#system-requirements)** section.

![Configuration système requise](images/system-reqs-800px.png)<br>
Configuration requise

Dans cette section, vous allez identifier () matérielle minimale et recommandée de matériel (facultatif) pour votre application de réalité mixte.

**Matériel d’entrée :**

Utilisez les cases à cocher pour indiquer les clients potentiels à si votre application prend en charge **microphone** (pour [entrée voix](voice-input.md)), **[Xbox contrôleur ou gamepad](hardware-accessories.md#bluetooth-gamepads)**, et/ou  **[contrôleurs de mouvement Windows Mixed Reality](motion-controllers.md)**. Ces informations seront visibles sur la page de détails de produit de votre application dans le Store et vous aide à votre application sont inclus dans les collections de l’application/jeu de votre choix (par exemple, une collection peut exister pour tous les jeux qui prennent en charge des contrôleurs de mouvement).

Être réfléchie sur la sélection des cases à cocher pour « matérielle » ou « matériel recommandé » pour les types d’entrée. 

Exemple : 
* Si votre jeu requiert des contrôleurs de mouvement, mais accepte l’entrée vocale via microphone, sélectionnez la case à cocher « matérielle » en regard de « Contrôleurs de mouvement Windows Mixed Reality », mais que la case à cocher « matériel recommandé » en regard de « Microphone ». 
* Si votre jeu peut être lu avec soit une Xbox contrôleur/gamepad ou mouvement contrôleurs, vous pouvez sélectionner la case à cocher « matérielle » en regard de « manette Xbox ou gamepad » et sélectionnez la case à cocher « matériel recommandé » en regard de « mouvement Windows Mixed Reality contrôleurs » en tant que contrôleurs de mouvement offrira probablement une licence de niveau supérieur dans l’expérience à partir du boîtier de commande.

**Casque immersif de réalité mixte Windows :**

Qui indique si un casque immersif est nécessaire pour utiliser votre application, ou qu’il est facultatif, est essentiel pour l’enseignement et la satisfaction des clients.

Si votre application peut *uniquement* être utilisé via un casque immersif, activez la case à cocher « matérielle » en regard de « Casque immersif Windows Mixed Reality ». Cela est visibles sur la page de détails de produit de votre application de Store en tant qu’avertissement au-dessus du bouton d’achat pour les clients ne pensent qu’ils vous achetez une application qui ne peut fonctionner sur leur PC comme une application de bureau traditionnelle.

Si votre application s’exécute sur le bureau, par exemple une application de PC traditionnel, mais offre une expérience de réalité virtuelle lorsqu’un casque immersif est connecté (si la totalité du contenu de votre application est disponible, ou uniquement une partie), sélectionnez la case à cocher « matériel recommandé » en regard de « Windows Mixed Reality casque immersif. » Aucun avertissement n’est visibles au-dessus du bouton de l’achat sur la page de détails du produit de votre application si vos fonctions d’application comme une application de bureau traditionnelle sans un casque immersive connecté.

**Spécifications de PC :**

Si vous souhaitez que votre application d’atteindre des utilisateurs de casque immersive de Windows Mixed Reality autant que possible, vous voudrez [cible](understanding-performance-for-mixed-reality.md) les spécifications de PC pour [PC de réalité mixte Windows avec les cartes graphiques intégrées](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines).

Si votre application de réalité mixte cible la configuration minimale requise le PC de réalité mixte Windows, ou nécessite une configuration de PC spécifique (telles que le GPU dédié d’un [Windows Mixed Reality Ultra PC](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines), vous devez indiquer qu’avec les informations pertinentes Spécifications de PC dans la colonne « matérielle ».

Si votre application de réalité mixte est conçue pour donner de meilleurs résultats, ou des graphiques de résolution plus élevée, sur une configuration particulière de PC ou une carte graphique, vous devez indiquer qui avec les spécifications de PC dans la colonne « matériel recommandé ».

Cela s’applique uniquement si votre application de réalité mixte utilise un casque immersif connecté à un PC. Si votre application de réalité mixte s’exécute uniquement sur HoloLens, vous n’aurez pas à indiquer les spécifications de PC comme HoloLens a uniquement une configuration matérielle.

### <a name="device-family-availability"></a>Disponibilité de la famille d’appareils

Si vous avez [empaqueté votre application correctement](https://docs.microsoft.com/windows/uwp/publish/app-package-requirements) dans Visual Studio, son téléchargement dans la page de Packages du processus de soumission d’application doit produire un tableau qui identifie votre application sera disponible pour les familles d’appareils.

![Table de disponibilité de famille d’appareils](images/device-family-table-900px.png)<br>
Table de disponibilité de famille d’appareils

Si votre application de réalité mixte fonctionne sur des casques IMMERSIFS, au moins « Windows 10 Desktop » doit être sélectionné dans la table. Si votre application de réalité mixte fonctionne sur HoloLens, au moins « Windows 10 HOLOGRAPHIQUE » doit être sélectionné. Si votre application s’exécute sur les deux types de casque Windows Mixed Reality, comme le [Académie de réalité mixte « Îlot de projet » application](mixed-reality-250.md), « Windows 10 Desktop » et « Windows 10 HOLOGRAPHIQUE » doivent être sélectionné.

>[!TIP]
>De nombreux développeurs rencontrez des erreurs lors du chargement de package de leur application lié à des incompatibilités entre le manifeste du package et les informations de votre compte / l’éditeur de l’application Centre de partenaires. Ces erreurs peuvent souvent être évitées en vous connectant à Visual Studio avec le même compte associé à votre compte de développeur Windows (celui qui vous permet de vous connecter au centre des partenaires). Si vous utilisez le même compte, vous serez en mesure d’associer votre application avec son identité dans le Microsoft Store avant que vous le package.

![Associez votre application avec le Microsoft Store](images/associate-your-app-700px.png)<br>
Associez votre application avec le Microsoft Store dans Visual Studio

### <a name="store-listing-page"></a>Page de liste de Store

Sur le [annonce de Store](https://docs.microsoft.com/windows/uwp/publish/create-app-store-listings) traiter de la page de la soumission de l’application, vous pouvez ajouter des informations utiles relatives à votre application de réalité mixte à plusieurs endroits.

>[!IMPORTANT]
>Pour vous assurer de votre application est correctement classée par le Store et les rendre détectable pour les clients Windows Mixed Reality, vous devez ajouter **« Windows Mixed Reality »** comme l’un de vos termes de recherche « » pour l’application (vous trouverez les termes de recherche en développant la « Partagées champs » section).

![Ajouter Windows Mixed Reality pour rechercher des termes du contrat](images/search-terms-800px.png)<br>
Ajouter « Windows Mixed Reality » pour rechercher des termes du contrat

## <a name="offering-a-free-trial-for-your-game-or-app"></a>Offre un essai gratuit pour votre jeu ou application

Nombreux consommateurs seront limitée à aucune expérience avec la réalité virtuelle avant d’acheter un casque immersif Windows Mixed Reality. Ils ne peuvent pas savoir à quoi s’attendre à partir des jeux et peut ne pas être familiarisés avec leur propre seuil de confort dans les expériences immersives. De nombreux clients peuvent également essayer un casque immersif Windows Mixed Reality sur les PC qui ne sont pas avec un badge comme [PC de réalité mixte Windows](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines). En raison de ces considérations, nous recommande fortement d’envisager offre un [version d’évaluation gratuite](https://docs.microsoft.com/windows/uwp/publish/set-app-pricing-and-availability#free-trial) pour votre application de réalité mixte payant ou d’un jeu.

## <a name="see-also"></a>Voir aussi
* [Réalité mixte](mixed-reality.md)
* [Vue d’ensemble du développement](development-overview.md)
* [Vues de l’application](app-views.md)
* [Comprendre les performances pour la réalité mixte](understanding-performance-for-mixed-reality.md)
* [Recommandations relatives aux performances pour Unity](performance-recommendations-for-unity.md)
* [Test de votre application sur HoloLens](testing-your-app-on-hololens.md)
* [Recommandations de compatibilité Windows Mixed Reality minimale PC matérielles](https://docs.microsoft.com/windows/mixed-reality/enthusiast-guide/windows-mixed-reality-minimum-pc-hardware-compatibility-guidelines)
