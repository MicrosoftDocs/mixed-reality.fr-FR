---
title: Activer le placement des modèles 3D dans la page d’hébergement
description: Comment placer des modèles 3D à partir de votre site Web ou de votre application dans la page d’hébergement de Windows Mixed Reality
author: thmignon
ms.author: thmignon
ms.date: 05/04/2018
ms.topic: article
keywords: 3D, modèle, place à la terre, lieu, monde, modélisation, Hébergement de la réalité mixte, Web, application
ms.openlocfilehash: 954086b79e3614e1b75ceb7560f9fc87435530fa
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829735"
---
# <a name="enable-placement-of-3d-models-in-the-mixed-reality-home"></a>Activer le placement des modèles 3D dans la réalité mixte

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de la [mise à jour 2018 de Windows 10 avril](release-notes-april-2018.md). Les versions antérieures de Windows ne sont pas compatibles avec cette fonctionnalité.

La [base de la réalité Windows Mixed](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs se trouvent avant de lancer des applications. Dans certains scénarios, les applications 2D (comme l’application hologrammes) permettent de placer des modèles 3D directement dans l’espace de la réalité mixte en tant que décorations ou pour une inspection supplémentaire en 3D complet. Le *protocole Add Model* vous permet d’envoyer un modèle 3D à partir de votre site Web ou application directement dans la page d’hébergement Windows Mixed Reality, où il sera conservé comme les lanceurs d' [applications 3D](3d-app-launcher-design-guidance.md), les applications 2D et les hologrammes. 

Par exemple, si vous développez une application qui couvre un catalogue de mobilier en 3D pour la conception d’un espace, vous pouvez utiliser le *protocole ajouter un modèle* pour permettre aux utilisateurs de placer ces modèles de mobilier 3D à partir du catalogue. Une fois placés dans le monde, les utilisateurs peuvent déplacer, redimensionner et supprimer ces modèles 3D comme d’autres hologrammes de la famille. Cet article fournit une vue d’ensemble de l’implémentation du *protocole Add Model* pour vous permettre de commencer à permettre aux utilisateurs de décorer leur monde avec des objets 3D à partir de votre application ou du Web.

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
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Ajouter un protocole de modèle</td>
        <td>✔️</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="overview"></a>Vue d'ensemble

Il existe 2 étapes pour activer le placement des modèles 3D dans la page d’hébergement de la réalité mixte de Windows:
1. [Vérifiez que votre modèle 3D est compatible avec la page d’hébergement Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md).
2. Implémentez le *protocole Add Model* dans votre application ou votre page Web (cet article).

## <a name="implementing-the-add-model-protocol"></a>Implémentation du *protocole Add Model*

Une fois que vous disposez d’un [modèle 3D compatible](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md), vous pouvez implémenter le *protocole Add Model* en activant l’URI suivant à partir d’une page Web ou d’une application:

```
ms-mixedreality:addmodel?uri=<Path to a .glb 3D model either local or remote>
```

Si l’URI pointe vers une ressource distante, il est automatiquement téléchargé et placé dans la page d’hébergement. Les ressources locales seront copiées dans le dossier des données d’application de la réalité mixte avant d’être placées dans la page d’hébergement. Nous vous recommandons de concevoir votre expérience afin de prendre en compte les scénarios dans lesquels l’utilisateur peut exécuter une version antérieure de Windows qui ne prend pas en charge cette fonctionnalité en masquant le bouton ou en le désactivant si possible. 

### <a name="invoking-the-add-model-protocol-from-a-universal-windows-platform-app"></a>Appel du *protocole Add Model* à partir d’une application plateforme Windows universelle:

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

### <a name="invoking-the-add-model-protocol-from-a-webpage"></a>Appel du *protocole Add Model* à partir d’une page Web:

```html
<a class="btn btn-default" href="ms-mixedreality:addModel?uri=sample.glb"> Place 3D Model </a>
```

## <a name="considerations-for-immersive-vr-headsets"></a>Considérations relatives aux casques immersifs (VR)

* Pour les casques immersifs, le portail de réalité mixte n’a pas besoin d’être en cours d’exécution avant d’appeler le *protocole Add Model*. Dans ce cas, le *protocole Add Model* lance le portail de réalité mixte et place l’objet directement là où le casque regarde une fois que vous arrivez dans la zone d’hébergement de la réalité mixte. 
* Quand vous appelez le *protocole Add Model* à partir du bureau avec le portail de réalité mixte déjà en cours d’exécution, assurez-vous que le casque est «éveillé». Si ce n’est pas le cas, le positionnement échoue. 

## <a name="see-also"></a>Voir aussi

* [Création de modèles 3D à utiliser dans la page d’hébergement Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [Exploration de la page d’accueil Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)
