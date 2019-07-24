---
title: Implémenter des lanceurs d’applications en 3D (applications UWP)
description: Comment créer des programmes de lancement et des logos d’applications en 3D pour des applications et des jeux UWP Windows Mixed Reality (distribués via le Microsoft Store), à la fois sur des casques HoloLens et immersif (VR).
author: thmignon
ms.author: thmignon
ms.date: 07/12/2018
ms.topic: article
keywords: 3D, logo, icône, modélisation, lanceur, lanceur 3D, vignette, cube dynamique, lien profond, secondarytile, vignette secondaire, UWP
ms.openlocfilehash: 4a8d4a696ff6ef19d7332b20580f1f5ee67bf045
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63516743"
---
# <a name="implement-3d-app-launchers-uwp-apps"></a>Implémenter des lanceurs d’applications en 3D (applications UWP)

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de la mise à jour 2017 automne Creators (RS3) pour les casques immersifs et est prise en charge par HoloLens avec la mise à jour 2018 d’avril de Windows 10. Assurez-vous que votre application cible une version du SDK Windows supérieure ou égale à 10.0.16299 sur les casques immersifs et 10.0.17125 sur HoloLens. Vous trouverez les SDK Windows les plus récentes [ici](https://developer.microsoft.com/windows/downloads/windows-10-sdk).

La [base de la réalité Windows Mixed](navigating-the-windows-mixed-reality-home.md) est le point de départ où les utilisateurs se trouvent avant de lancer des applications. Lors de la création d’une application UWP pour Windows Mixed Reality, par défaut, les applications sont lancées en tant qu’ardoise 2D avec le logo de leur application. Lors du développement d’expériences pour Windows Mixed Reality, un lanceur 3D peut éventuellement être défini pour remplacer le lanceur 2D par défaut de votre application. En général, les lanceurs 3D sont recommandés pour lancer des applications immersifs qui utilisent les utilisateurs hors de Windows Mixed Reality, tandis que le lanceur 2D par défaut est préféré quand l’application est activée sur place. Vous pouvez également créer un [lien profond en 3D (secondaryTile)](#3d-deep-links-secondarytiles) en tant que lanceur en 3D pour le contenu d’une application UWP 2D.

>[!VIDEO https://www.youtube.com/embed/TxIslHsEXno]

## <a name="3d-app-launcher-creation-process"></a>processus de création du lanceur d’applications 3D

La création d’un lanceur d’applications 3D comporte trois étapes:
1. [Conception et concept](3d-app-launcher-design-guidance.md)
2. [Modélisation et exportation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. Intégration dans votre application (cet article)

les ressources 3D à utiliser comme lanceurs pour votre application doivent être créées à l’aide des [instructions de création Windows Mixed realisation](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) pour garantir la compatibilité. Les ressources qui ne satisfont pas à cette spécification de création ne seront pas affichées dans la page d’hébergement de la réalité mixte Windows.

## <a name="configuring-the-3d-launcher"></a>Configuration du lanceur 3D

Lorsque vous créez un projet dans Visual Studio, cela a pour effet de créer une vignette par défaut simple qui affiche le nom et le logo de votre application. Pour remplacer cette représentation 2D par un modèle 3D personnalisé, modifiez le manifeste d’application de votre application de manière à inclure l’élément «MixedRealityModel» dans le cadre de votre définition de vignette par défaut. Pour revenir au lanceur 2D, supprimez simplement la définition MixedRealityModel du manifeste.

### <a name="xml"></a>XML

Tout d’abord, recherchez le manifeste du package d’application dans votre projet actuel. Par défaut, le manifeste sera nommé Package. appxmanifest. Si vous utilisez Visual Studio, cliquez avec le bouton droit sur le manifeste dans votre afficheur de solution, puis sélectionnez **afficher la source** pour ouvrir le fichier XML à modifier. 

En haut du manifeste, ajoutez le schéma uap5 et incluez-le en tant qu’espace de noms pouvant être ignoré:

```xml
<Package xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2" 
         xmlns:uap5="http://schemas.microsoft.com/appx/manifest/uap/windows10/5"
         IgnorableNamespaces="uap uap2 uap5 mp"
         xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10">
```

Spécifiez ensuite la valeur «MixedRealityModel» dans la vignette par défaut de votre application:

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

Les éléments MixedRealityModel acceptent un chemin d’accès de fichier pointant vers une ressource 3D stockée dans votre package d’application. Actuellement, seuls les modèles 3D fournis à l’aide du format de fichier. GLB et créés par rapport aux [instructions de création de ressources 3D Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md) sont pris en charge. Les ressources doivent être stockées dans le package d’application et l’animation n’est pas prise en charge actuellement. Si le paramètre «Path» est laissé vide, Windows affiche la ardoise 2D au lieu du lanceur 3D. **Remarque:** la ressource. GLB doit être marquée comme «contenu» dans vos paramètres de génération avant de générer et d’exécuter votre application.


![Sélectionnez le. GLB dans votre Explorateur de solutions et utilisez la section Propriétés pour le marquer comme «contenu» dans les paramètres de génération.](images/buildsetting-content-300px.png)<br>
*Sélectionnez le. GLB dans votre Explorateur de solutions et utilisez la section Propriétés pour le marquer comme «contenu» dans les paramètres de génération.*

### <a name="bounding-box"></a>Cadre englobant

Un cadre englobant peut être utilisé pour ajouter éventuellement une zone de mémoire tampon supplémentaire autour de l’objet. Le cadre englobant est spécifié à l’aide d’un point central et d’étendues qui indiquent la distance entre le centre du rectangle englobant et ses bords le long de chaque axe. Les unités du cadre englobant peuvent être mappées à 1 unité = 1 mètre. Si aucun cadre englobant n’est fourni, l’un d’eux est automatiquement ajusté à la maille de l’objet. Si le cadre englobant fourni est plus petit que le modèle, il sera redimensionné pour s’ajuster à la maille.

La prise en charge de l’attribut cadre englobant sera fournie avec la mise à jour Windows RS4 en tant que propriété sur l’élément MixedRealityModel. Pour définir un cadre englobant tout d’abord en haut du manifeste de l’application, ajoutez le schéma uap6 et incluez-le en tant qu’espaces de noms pouvant être ignorés:

```xml
<Package xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest" 
         xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10" 
         xmlns:uap2="http://schemas.microsoft.com/appx/manifest/uap/windows10/2" 
         xmlns:uap5="http://schemas.microsoft.com/appx/manifest/uap/windows10/5"
         xmlns:uap6="http://schemas.microsoft.com/appx/manifest/uap/windows10/6"
         IgnorableNamespaces="uap uap2 uap5 uap6 mp"
         xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10">
```
Ensuite, sur le MixedRealityModel, définissez la propriété SpatialBoundingBox pour définir le cadre englobant: 

```xml
        <uap:DefaultTile Wide310x150Logo="Assets\WideLogo.png" >
          <uap5:MixedRealityModel Path="Assets\My3DTile.glb">
              <uap6:SpatialBoundingBox  Center=”1,-2,3” Extents=”1,2,3” />
          </uap5:MixedRealityModel>
        </uap:DefaultTile>
```

### <a name="using-unity"></a>Utilisation d’Unity

Lorsque vous utilisez Unity, le projet doit être généré et ouvert dans Visual Studio pour que le manifeste d’application puisse être modifié. 

>[!NOTE]
>Le lanceur 3D doit être redéfini dans le manifeste lors de la génération et du déploiement d’une nouvelle solution Visual Studio à partir d’Unity.

## <a name="3d-deep-links-secondarytiles"></a>Liens Deep 3D (secondaryTiles)

> [!NOTE]
> Cette fonctionnalité a été ajoutée dans le cadre de la mise à jour de 2017 automne Creators Update (RS3) pour les casques immersifs (VR) et dans le cadre de la mise à jour du 2018 d’avril (RS4) pour HoloLens. Assurez-vous que votre application cible une version du SDK Windows supérieure ou égale à 10.0.16299 sur les casques immersifs (VR) et 10.0.17125 sur HoloLens. Vous trouverez les SDK Windows les plus récentes [ici](https://developer.microsoft.com/windows/downloads/windows-10-sdk).

>[!IMPORTANT]
>les liens secondaryTiles (3D Deep Links) fonctionnent uniquement avec les applications UWP 2D. Toutefois, vous pouvez créer un lanceur d' [applications en 3D](implementing-3d-app-launchers.md) pour lancer une application exclusive à partir de la page d’hébergement de Windows Mixed Reality.

Vos applications 2D peuvent être améliorées pour Windows Mixed Reality en ajoutant la possibilité de placer des modèles 3D à partir de votre application dans la [page d’accueil Windows Mixed Real](navigating-the-windows-mixed-reality-home.md) comme des liens détaillés vers le contenu de votre application 2D, comme des [vignettes secondaires 2D](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-secondary-tiles) sur le site de démarrage de Windows menus. Par exemple, vous pouvez créer des photosphères de 360 ° qui se lient directement à une application de visionneuse de photos 360 °, ou permettre aux utilisateurs de placer du contenu 3D à partir d’une collection de ressources qui ouvre une page de détails à propos de l’auteur. Il s’agit simplement de quelques façons d’étendre les fonctionnalités de votre application 2D avec du contenu 3D.

### <a name="creating-a-3d-secondarytile"></a>Création d’un «secondaryTile» 3D

Vous pouvez placer du contenu 3D à partir de votre application à l’aide de «secondaryTiles» en définissant un modèle de réalité mixte au moment de la création. Les modèles de réalité mixte sont créés en référençant une ressource 3D dans votre package d’application et en définissant éventuellement un cadre englobant. 

> [!NOTE]
> La création de «secondaryTiles» à partir d’une vue exclusive n’est pas prise en charge actuellement.

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

Un cadre englobant peut être utilisé pour ajouter une zone de mémoire tampon supplémentaire autour de l’objet. Le cadre englobant est spécifié à l’aide d’un point central et d’étendues qui indiquent la distance entre le centre du rectangle englobant et ses bords le long de chaque axe. Les unités du cadre englobant peuvent être mappées à 1 unité = 1 mètre. Si aucun cadre englobant n’est fourni, l’un d’eux est automatiquement ajusté à la maille de l’objet. Si le cadre englobant fourni est plus petit que le modèle, il sera redimensionné pour s’ajuster à la maille.

### <a name="activation-behavior"></a>Comportement d’activation

> [!NOTE]
> Ce composant sera pris en charge à partir de la mise à jour de Windows RS4. Assurez-vous que votre application cible une version du SDK Windows supérieure ou égale à 10.0.17125 si vous envisagez d’utiliser cette fonctionnalité

Vous pouvez définir le comportement d’activation d’un secondaryTile 3D afin de contrôler la manière dont il réagit lorsqu’un utilisateur le sélectionne. Cela peut être utilisé pour placer des objets 3D dans la zone de vie de la réalité mixte qui sont informatifs ou décoratifs Purley. Les types de comportement d’activation suivants sont pris en charge:
1. Par défaut : Quand un utilisateur sélectionne l’secondaryTile 3D, l’application est activée
2. None : Lorsque les utilisateurs sélectionnent l’secondaryTile 3D, rien ne se produit et l’application n’est pas activée.

### <a name="obtaining-and-updating-an-existing-secondarytile"></a>Obtention et mise à jour d’un «secondaryTile» existant

Les développeurs peuvent obtenir une liste de leurs vignettes secondaires existantes, y compris les propriétés qu’ils ont spécifiées précédemment. Ils peuvent également mettre à jour les propriétés en modifiant la valeur, puis en appelant UpdateAsync ().

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

### <a name="checking-that-the-user-is-in-windows-mixed-reality"></a>Vérification de la présence de l’utilisateur dans Windows Mixed Reality

les liens en profondeur 3D (secondaryTiles) peuvent être créés uniquement lorsque la vue est affichée dans un casque Windows Mixed Reality. Lorsque votre affichage n’est pas présenté dans un casque Windows Mixed Reality, nous vous recommandons de le gérer en masquant le point d’entrée ou en indiquant un message d’erreur. Vous pouvez vérifier cela en interrogeant [IsCurrentViewPresentedOnHolographic ()](https://docs.microsoft.com/uwp/api/windows.applicationmodel.preview.holographic.holographicapplicationpreview#Windows_ApplicationModel_Preview_Holographic_HolographicApplicationPreview_IsCurrentViewPresentedOnHolographicDisplay_).

## <a name="tile-notifications"></a>Notifications par vignette

Les notifications par vignette ne prennent pas actuellement en charge l’envoi d’une mise à jour avec une ressource 3D. Cela signifie que les développeurs ne seront pas en mesure d’effectuer les opérations suivantes:
* Notifications Push
* Interrogation périodique
* Notifications planifiées

Pour plus d’informations sur les autres fonctionnalités et attributs de vignettes et sur la façon dont ils sont utilisés pour les mosaïques 2D, consultez la [documentation vignettes pour les applications UWP](https://docs.microsoft.com/windows/uwp/controls-and-patterns/tiles-and-notifications-creating-tiles).

## <a name="see-also"></a>Voir aussi

* [Exemple de modèle de réalité mixte](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/MixedRealityModel) contenant un lanceur d’application 3D.
* [Guide de conception du lanceur d’applications 3D](3d-app-launcher-design-guidance.md)
* [Création de modèles 3D à utiliser dans la page d’hébergement Windows Mixed Reality](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [Implémentation de lanceurs d’applications en 3D (applications Win32)](implementing-3d-app-launchers-win32.md)
* [Exploration de la page d’accueil Windows Mixed Reality](navigating-the-windows-mixed-reality-home.md)
