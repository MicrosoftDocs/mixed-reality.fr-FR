---
title: Implémenter des lanceurs d’applications 3D (applications UWP)
description: Comment créer des lanceurs d’applications 3D et les logos pour applications UWP de réalité mixte Windows et les jeux (distribués via le Microsoft Store), à la fois sur HoloLens et des casques IMMERSIFS (VR).
author: thmignon
ms.author: thmignon
ms.date: 07/12/2018
ms.topic: article
keywords: 3D, le logo, icône, modélisation, Lanceur, Lanceur 3D, vignette, cube en direct, lien profond, secondarytile, vignette secondaire, UWP
ms.openlocfilehash: 4a8d4a696ff6ef19d7332b20580f1f5ee67bf045
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597028"
---
# <a name="implement-3d-app-launchers-uwp-apps"></a>Implémenter des lanceurs d’applications 3D (applications UWP)

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de 2017 Fall Creators Update (RS3) pour des casques IMMERSIFS et est pris en charge par HoloLens avec les fenêtres de mettre à jour du 10 avril 2018. Assurez-vous que votre application cible une version du SDK Windows supérieur ou égal à 10.0.16299 sur des casques IMMERSIFS et 10.0.17125 sur HoloLens. Vous trouverez la dernière version du SDK de Windows [ici](https://developer.microsoft.com/windows/downloads/windows-10-sdk).

Le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs arrivent avant de lancer des applications. Lorsque vous créez une application UWP pour Windows Mixed Reality, par défaut, les applications sont lancées en tant qu’ardoises 2D avec le logo de leur application. Lorsque vous développez des expériences pour la réalité mixte Windows, un lanceur 3D peut éventuellement être défini pour remplacer le Lanceur 2D par défaut pour votre application. En règle générale, les lanceurs 3D sont recommandés pour le lancement des applications immersives qui acceptent les utilisateurs d’accéder à Windows Mixed Reality accueil tandis que le Lanceur 2D par défaut est préférable lorsque l’application est activée sur place. Vous pouvez également créer un [lien profond 3D (secondaryTile)](#3d-deep-links-secondarytiles) comme un lanceur 3D vers du contenu dans une application UWP 2D.

>[!VIDEO https://www.youtube.com/embed/TxIslHsEXno]

## <a name="3d-app-launcher-creation-process"></a>Processus de création de lanceur application 3D

Il existe 3 étapes à la création d’un lanceur d’applications 3D :
1. [Conception et concepting](3d-app-launcher-design-guidance.md)
2. [Modélisation et l’exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. L’intégration dans votre application (cet article)

Composants 3D à utiliser comme lanceurs pour votre application doivent être créés à l’aide de la [recommandations sur la programmation de Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) pour assurer la compatibilité. Actifs qui ne parviennent pas à répondre à cette spécification création seront affichera pas dans la réalité mixte Windows domestique.

## <a name="configuring-the-3d-launcher"></a>Configuration du Lanceur 3D

Lorsque vous créez un projet dans Visual Studio, cela a pour effet de créer une vignette par défaut simple qui affiche le nom et le logo de votre application. Pour remplacer cette 2D représentation avec un modèle 3D personnalisé modifier le manifeste d’application de votre application pour inclure l’élément « MixedRealityModel » dans le cadre de votre définition de la vignette par défaut. Pour revenir à la 2D Lanceur simplement supprimer la définition de MixedRealityModel à partir du manifeste.

### <a name="xml"></a>XML

Tout d’abord, recherchez le manifeste de package d’application dans votre projet actuel. Par défaut, le manifeste sera nommé Package.appxmanifest. Si vous utilisez Visual Studio, puis cliquez sur le manifeste dans l’Observateur de votre solution et sélectionnez **afficher la source** pour ouvrir le fichier xml pour la modification. 

En haut du manifeste, ajoutez le schéma uap5 et incluez-le comme un espace de noms peut être ignoré :

```xml
<Package xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2" 
         xmlns:uap5="http://schemas.microsoft.com/appx/manifest/uap/windows10/5"
         IgnorableNamespaces="uap uap2 uap5 mp"
         xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10">
```

Ensuite, spécifiez le « MixedRealityModel » dans la mosaïque par défaut de votre application :

```xml
<Applications>
    <Application Id="App"
      Executable="$targetnametoken$.exe"
      EntryPoint="ExampleApp.App">
      <uap:VisualElements
        DisplayName="ExampleApp"
        Square150x150Logo="Assets\Logo.png"
        Square44x44Logo="Assets\SmallLogo.png"
        Description="ExampleApp"
        BackgroundColor="#464646">
        <uap:DefaultTile Wide310x150Logo="Assets\WideLogo.png" >
          <uap5:MixedRealityModel Path="Assets\My3DTile.glb" />
        </uap:DefaultTile>
        <uap:SplashScreen Image="Assets\SplashScreen.png" />
      </uap:VisualElements>
    </Application>
</Applications>
```

Les éléments MixedRealityModel accepte un chemin d’accès qui pointe vers une ressource 3D stockée dans votre package d’application. Actuellement des modèles 3D uniquement remis en utilisant le format de fichier .glb et créé sur le [asset 3D de Windows Mixed Reality création instructions](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) sont pris en charge. Ressources doivent être stockées dans le package d’application et animation n’est pas pris en charge. Si le paramètre « Chemin » est vide, Windows affiche l’ardoise 2D au lieu du Lanceur 3D. **Remarque :** la ressource .glb doit être marquée comme « Contenu » dans vos paramètres de build avant de générer et exécuter votre application.


![Sélectionnez le .glb dans l’Explorateur de solutions et utiliser la section des propriétés pour marquer en tant que « Contenu » dans les paramètres de build](images/buildsetting-content-300px.png)<br>
*Sélectionnez le .glb dans l’Explorateur de solutions et utiliser la section des propriétés pour marquer en tant que « Contenu » dans les paramètres de build*

### <a name="bounding-box"></a>Cadre englobant

Un rectangle englobant peut être utilisé pour éventuellement ajouter une région de mémoire tampon supplémentaire autour de l’objet. La zone englobante est spécifiée à l’aide d’un point central et les extensions qui indiquent la distance entre le centre du rectangle englobant et ses bords chaque axe. Unités pour la zone englobante peuvent être mappées à 1 unité = 1 mètre. Si un rectangle englobant n’est pas fourni puis une sera être ajustée automatiquement à la maille de l’objet. Si la zone englobante fournie est plus petite que le modèle puis, il est redimensionné pour s’ajuster à la maille.

Prise en charge pour l’attribut de zone englobante proviendront avec la mise à jour Windows RS4 en tant que propriété sur l’élément MixedRealityModel. Pour définir un rectangle englobant de tout d’abord en haut de l’application manifeste ajouter le schéma uap6 et l’inclure en tant que des espaces de noms peut être ignoré :

```xml
<Package xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2" 
         xmlns:uap5="http://schemas.microsoft.com/appx/manifest/uap/windows10/5"
         xmlns:uap6="http://schemas.microsoft.com/appx/manifest/uap/windows10/6"
         IgnorableNamespaces="uap uap2 uap5 uap6 mp"
         xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10">
```
Ensuite, dans le MixedRealityModel définie la propriété SpatialBoundingBox pour définir la zone englobante : 

```xml
        <uap:DefaultTile Wide310x150Logo="Assets\WideLogo.png" >
          <uap5:MixedRealityModel Path="Assets\My3DTile.glb">
              <uap6:SpatialBoundingBox  Center=”1,-2,3” Extents=”1,2,3” />
          </uap5:MixedRealityModel>
        </uap:DefaultTile>
```

### <a name="using-unity"></a>À l’aide de Unity

Lorsque vous travaillez avec Unity, le projet doit être créé et ouvert dans Visual Studio avant de pouvoir modifier le manifeste d’application. 

>[!NOTE]
>Le Lanceur 3D doit être redéfini dans le manifeste pour créer et déployer une nouvelle solution Visual Studio à partir d’Unity.

## <a name="3d-deep-links-secondarytiles"></a>Profondeur 3D lie (secondaryTiles)

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de 2017 Fall Creators Update (RS3) pour des casques IMMERSIFS (VR) et dans le cadre de l’avril 2018 mise à jour (RS4) pour HoloLens. Assurez-vous que votre application cible une version du SDK Windows supérieur ou égal à 10.0.16299 sur des casques IMMERSIFS (VR) et 10.0.17125 sur HoloLens. Vous trouverez la dernière version du SDK de Windows [ici](https://developer.microsoft.com/windows/downloads/windows-10-sdk).

>[!IMPORTANT]
>Liens ciblés 3D (secondaryTiles) fonctionnent uniquement avec les applications UWP 2D. Vous pouvez, cependant, créer un [Lanceur d’applications 3D](implementing-3d-app-launchers.md) pour lancer une application exclusive à partir de Windows Mixed Reality domestique.

Vos applications 2D peuvent être améliorées pour la réalité mixte Windows en ajoutant la possibilité de placer des modèles 3D à partir de votre application dans le [Windows Mixed Reality accueil](navigating-the-windows-mixed-reality-home.md) en tant que liens ciblés vers du contenu dans votre application 2D, tout comme [secondaire 2D vignettes](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-secondary-tiles) dans le menu Démarrer de Windows. Par exemple, vous pouvez créer photospheres 360° lier directement dans une application de visionneuse de photos de 360°, ou permettent aux utilisateurs de placer du contenu 3D à partir d’une collection de ressources qui ouvre une page de détails à propos de l’auteur. Voici quelques façons d’étendre les fonctionnalités de votre application 2D avec du contenu 3D.

### <a name="creating-a-3d-secondarytile"></a>Création d’une « secondaryTile » 3D

Vous pouvez placer du contenu 3D à partir de votre application à l’aide de « secondaryTiles » en définissant un modèle de réalité mixte lors de la création. Modèles de réalité mixte sont créés en faisant référence à une ressource 3D dans votre package d’application et éventuellement définir un rectangle englobant. 

> [!NOTE]
> Création de « secondaryTiles » à partir de dans une vue exclusive n’est pas pris en charge actuellement.

```cs
using Windows.UI.StartScreen;
using Windows.Foundation.Numerics;
using Windows.Perception.Spatial;

// Initialize the tile
SecondaryTile tile = new SecondaryTile("myTileId")
{
    DisplayName = "My Tile",
    Arguments = "myArgs"
};

tile.VisualElements.Square150x150Logo = new Uri("ms-appx:///Assets/MyTile/Square150x150Logo.png");

//Assign 3D model (only ms-appx and ms-appdata are allowed)
TileMixedRealityModel model = tile.VisualElements.MixedRealityModel;
model.Uri = new Uri("ms-appx:///Assets/MyTile/MixedRealityModel.glb");
model.ActivationBehavior = TileMixedRealityModelActivationBehavior.Default;
model.BoundingBox = new SpatialBoundingBox
{
    Center = new Vector3 { X = 1, Y = 0, Z = 0 },
    Extents = new Vector3 { X = 3, Y = 5, Z = 4 }
};

// And place it
await tile.RequestCreateAsync();
```

### <a name="bounding-box"></a>Cadre englobant

Un rectangle englobant peut être utilisé pour ajouter une région de mémoire tampon supplémentaire autour de l’objet. La zone englobante est spécifiée à l’aide d’un point central et les extensions qui indiquent la distance entre le centre du rectangle englobant et ses bords chaque axe. Unités pour la zone englobante peuvent être mappées à 1 unité = 1 mètre. Si un rectangle englobant n’est pas fourni puis une sera être ajustée automatiquement à la maille de l’objet. Si la zone englobante fournie est plus petite que le modèle puis, il est redimensionné pour s’ajuster à la maille.

### <a name="activation-behavior"></a>Comportement d’activation

> [!NOTE]
> Cette fonctionnalité sera pris en charge à compter de la mise à jour Windows RS4. Assurez-vous que votre application cible une version du SDK Windows supérieure ou égale à 10.0.17125 si vous envisagez d’utiliser cette fonctionnalité

Vous pouvez définir le comportement d’activation pour une secondaryTile 3D contrôler comment il réagit lorsqu’un utilisateur le sélectionne. Cela permet de placer des objets 3D dans la réalité mixte domestique qui sont purley informative ou décoratif. Les types de comportement d’activation suivants sont pris en charge :
1. Default : Lorsqu’un utilisateur sélectionne la secondaryTile 3D l’application est activée
2. None : Lorsque l’utilisateur sélectionne la secondaryTile 3D, rien ne se produit et l’application n’est pas activé.

### <a name="obtaining-and-updating-an-existing-secondarytile"></a>Obtention et la mise à jour une instance existante de « secondaryTile »

Les développeurs peuvent obtenir une liste de leurs vignettes secondaires existantes, ce qui inclut les propriétés qui ont été spécifiées précédemment. Ils peuvent également mettre à jour les propriétés en modifiant la valeur, puis UpdateAsync().

```cs
// Grab the existing secondary tile
SecondaryTile tile = (await SecondaryTile.FindAllAsync()).First();

Uri updatedUri = new Uri("ms-appdata:///local/MixedRealityUpdated.glb");

// See if the model needs updating
if (!tile.VisualElements.MixedRealityModel.Uri.Equals(updatedUri))
{
    // Update it
    tile.VisualElements.MixedRealityModel.Uri = updatedUri;

    // And apply the changes
    await tile.UpdateAsync();
}
```

### <a name="checking-that-the-user-is-in-windows-mixed-reality"></a>Vérification que l’utilisateur est en réalité mixte Windows

Liens ciblés 3D (secondaryTiles) peuvent uniquement être créés alors que la vue est affichée dans un casque Windows Mixed Reality. Lorsque votre vue n’est pas en cours de présentation dans un casque Windows Mixed Reality, nous vous recommandons d’envisageable normalement en masquant le point d’entrée ou en affichant un message d’erreur. Vous pouvez le vérifier en interrogeant [IsCurrentViewPresentedOnHolographic()](https://docs.microsoft.com/uwp/api/windows.applicationmodel.preview.holographic.holographicapplicationpreview#Windows_ApplicationModel_Preview_Holographic_HolographicApplicationPreview_IsCurrentViewPresentedOnHolographicDisplay_).

## <a name="tile-notifications"></a>Notifications par vignette

Notifications de vignette ne gèrent pas actuellement envoyer une mise à jour avec la ressource de 3D. Cela signifie que les développeurs ne sera pas en mesure d’effectuer les opérations suivantes
* Notifications push
* Interrogation périodique
* Notifications planifiées

Pour plus d’informations sur les autres vignettes de fonctionnalités et d’attributs et comment ils sont utilisés pour les vignettes 2D font référence à la [vignettes pour documentation UWP Apps](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-creating-tiles).

## <a name="see-also"></a>Voir aussi

* [Exemple de modèle de réalité mixte](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) contenant un lanceur d’applications 3D.
* [Guide de conception du Lanceur d’application 3D](3d-app-launcher-design-guidance.md)
* [Création de modèles 3D pour une utilisation dans la page d’accueil Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [Implémentation des lanceurs d’applications 3D (applications Win32)](implementing-3d-app-launchers-win32.md)
* [Navigation dans Windows Mixed Reality domestique](navigating-the-windows-mixed-reality-home.md)
