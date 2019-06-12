---
title: Permettre le placement des modèles 3D dans la page d’accueil
description: Comment placer des modèles 3D à partir de votre site Web ou une application dans Windows Mixed Reality domestique
author: thmignon
ms.author: thmignon
ms.date: 05/04/2018
ms.topic: article
keywords: 3D, modèle, sur place à domicile, sur place, monde, modélisation, réalité mixte domestique, web, application
ms.openlocfilehash: 954086b79e3614e1b75ceb7560f9fc87435530fa
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829735"
---
# <a name="enable-placement-of-3d-models-in-the-mixed-reality-home"></a>Permettre le placement des modèles 3D dans la réalité mixte domestique

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de la [mettre à jour du 10 avril 2018 Windows](release-notes-april-2018.md). Les versions antérieures de Windows ne sont pas compatibles avec cette fonctionnalité.

Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs arrivent avant de lancer des applications. Dans certains scénarios, les applications 2D (par exemple, l’application hologrammes) permettent le placement des modèles 3D directement dans la page d’accueil réalité mixte comme des ornements, ou pour une nouvelle inspection entièrement en 3D. Le *ajouter modèle protocole* vous permet d’envoyer un modèle 3D à partir de votre site Web ou une application directement dans la réalité mixte Windows domestique, où il est conservé comme [lanceurs d’applications 3D](3d-app-launcher-design-guidance.md), applications 2D et hologrammes. 

Par exemple, si vous développez une application qui fait apparaître un catalogue de mobilier 3D pour la conception d’un espace, vous pouvez utiliser la *ajouter modèle protocole* pour permettre aux utilisateurs de placer ces modèles de mobilier 3D à partir du catalogue. Une fois placés dans le monde, les utilisateurs peuvent déplacer, redimensionner et supprimer ces modèles 3D à l’instar des autres hologrammes dans la page d’accueil. Cet article fournit une vue d’ensemble de l’implémentation de la *ajouter modèle protocole* afin que vous pouvez démarrer permettant aux utilisateurs de décorer la vie avec des objets 3D à partir de votre application ou le web.

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Ajouter le protocole de modèle</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="overview"></a>Vue d'ensemble

Il existe 2 étapes de permettre à l’emplacement des modèles 3D dans Windows Mixed Reality domestique :
1. [Vérifiez que votre modèle 3D est compatible avec Windows Mixed Reality accueil](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md).
2. Implémentez le *ajouter le protocole de modèle* dans votre application ou d’une page Web (cet article).

## <a name="implementing-the-add-model-protocol"></a>Mise en œuvre le *ajouter le protocole de modèle*

Une fois que vous avez un [modèle 3D compatible](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md), vous pouvez implémenter la *ajouter modèle protocole* en activant l’URI suivant d’une page Web ou d’application :

```
ms-mixedreality:addmodel?uri=<Path to a .glb 3D model either local or remote>
```

Si l’URI pointe vers une ressource distante, puis il est automatiquement téléchargé et placé dans la page d’accueil. Ressources locales seront copiés au dossier de données de la page d’accueil réalité mixte application avant d’être placé dans la page d’accueil. Nous vous recommandons de conception de votre expérience compte pour les scénarios où l’utilisateur peut exécuter une version antérieure de Windows qui ne prennent pas en charge cette fonctionnalité en masquant le bouton ou de la désactivation de la mesure du possible. 

### <a name="invoking-the-add-model-protocol-from-a-universal-windows-platform-app"></a>Appel de la *ajouter modèle protocole* à partir d’une application de plateforme Windows universelle :

```C#
private async void launchURI_Click(object sender, RoutedEventArgs e)
{
   // Define the add model URI
   var uriAddModel = new Uri(@"ms-mixedreality:addModel?uri=sample.glb");

   // Launch the URI to invoke the placement
   var success = await Windows.System.Launcher.LaunchUriAsync(uriAddModel);

   if (success)
   {
      // URI launched
   }
   else
   {
      // URI launch failed
   }
}
```

### <a name="invoking-the-add-model-protocol-from-a-webpage"></a>Appel de la *ajouter modèle protocole* à partir d’une page Web :

```html
<a class="btn btn-default" href="ms-mixedreality:addModel?uri=sample.glb"> Place 3D Model </a>
```

## <a name="considerations-for-immersive-vr-headsets"></a>Considérations pour des casques IMMERSIFS (VR)

* Pour des casques IMMERSIFS (VR), le portail de réalité mixte ne devra pas être en cours d’exécution avant d’appeler le *ajouter le protocole de modèle*. Dans ce cas, le *ajouter modèle protocole* lance le portail de réalité mixte et placer l’objet directement où le casque recherche une fois que vous arrivez dans la réalité mixte domestique. 
* Lors de l’appel le *ajouter modèle protocole* à partir du bureau avec le portail de réalité mixte déjà en cours d’exécution, vérifiez que le casque est « éveillé ». Si ce n’est pas le cas, le placement ne réussira pas. 

## <a name="see-also"></a>Voir aussi

* [Création de modèles 3D pour une utilisation dans la page d’accueil Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [Exploration de la page d’accueil Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)
