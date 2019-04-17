---
title: Persistance dans Unity
description: Persistance permet aux utilisateurs d’épingler hologrammes individuels ou un espace de travail, où qu’ils veulent et puis recherchez il où qu’elles attendent de plusieurs utilise de votre application.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: HoloLens, persistance, Unity
ms.openlocfilehash: b6a67e52b3a5ce724a90eb1a479c5eda74b0c4cb
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597116"
---
# <a name="persistence-in-unity"></a><span data-ttu-id="2af44-104">Persistance dans Unity</span><span class="sxs-lookup"><span data-stu-id="2af44-104">Persistence in Unity</span></span>

<span data-ttu-id="2af44-105">**Namespace :** *UnityEngine.XR.WSA.Persistence*</span><span class="sxs-lookup"><span data-stu-id="2af44-105">**Namespace:** *UnityEngine.XR.WSA.Persistence*</span></span><br>
<span data-ttu-id="2af44-106">**Classe :** *WorldAnchorStore*</span><span class="sxs-lookup"><span data-stu-id="2af44-106">**Class:** *WorldAnchorStore*</span></span>

<span data-ttu-id="2af44-107">Le WorldAnchorStore est essentiel à la création d’expériences HOLOGRAPHIQUE où hologrammes restent dans les positions du monde réel spécifique entre les instances de l’application.</span><span class="sxs-lookup"><span data-stu-id="2af44-107">The WorldAnchorStore is the key to creating holographic experiences where holograms stay in specific real world positions across instances of the application.</span></span> <span data-ttu-id="2af44-108">Vous pouvez ainsi vos utilisateurs épinglent hologrammes individuels ou un espace de travail, où qu’ils le souhaitent il et ensuite les retrouver ultérieurement où qu’elles attendent sur nombreuses utilisations de votre application.</span><span class="sxs-lookup"><span data-stu-id="2af44-108">This lets your users pin individual holograms or a workspace wherever they want it, and then find it later where they expect over many uses of your app.</span></span>

## <a name="how-to-persist-holograms-across-sessions"></a><span data-ttu-id="2af44-109">Comment conserver hologrammes entre les sessions</span><span class="sxs-lookup"><span data-stu-id="2af44-109">How to persist holograms across sessions</span></span>

<span data-ttu-id="2af44-110">Le WorldAnchorStore permettent de conserver l’emplacement de WorldAnchor entre les sessions.</span><span class="sxs-lookup"><span data-stu-id="2af44-110">The WorldAnchorStore will allow you to persist the location of WorldAnchor's across sessions.</span></span> <span data-ttu-id="2af44-111">Pour conserver réellement hologrammes entre les sessions, vous devrez effectuer séparément le suivi de votre GameObjects qui utilisent un point d’ancrage du monde particulier.</span><span class="sxs-lookup"><span data-stu-id="2af44-111">To actually persist holograms across sessions, you will need to separately keep track of your GameObjects that use a particular world anchor.</span></span> <span data-ttu-id="2af44-112">Il est souvent judicieux pour créer une racine GameObject avec un point d’ancrage du monde et avoir des enfants hologrammes ancrée par celui-ci avec un décalage de position local.</span><span class="sxs-lookup"><span data-stu-id="2af44-112">It often makes sense to create a GameObject root with a world anchor and have children holograms anchored by it with a local position offset.</span></span>

<span data-ttu-id="2af44-113">Pour charger hologrammes provenant des sessions précédentes :</span><span class="sxs-lookup"><span data-stu-id="2af44-113">To load holograms from previous sessions:</span></span>
1. <span data-ttu-id="2af44-114">Obtenir le WorldAnchorStore</span><span class="sxs-lookup"><span data-stu-id="2af44-114">Get the WorldAnchorStore</span></span>
2. <span data-ttu-id="2af44-115">Charger des données d’application sur le point d’ancrage du monde qui vous donne l’id de l’ancrage du monde</span><span class="sxs-lookup"><span data-stu-id="2af44-115">Load app data relating to the world anchor which gives you the id of the world anchor</span></span>
3. <span data-ttu-id="2af44-116">Charger un point d’ancrage du monde entier à partir de son id</span><span class="sxs-lookup"><span data-stu-id="2af44-116">Load a world anchor from its id</span></span>

<span data-ttu-id="2af44-117">Pour enregistrer les hologrammes pour les sessions ultérieures :</span><span class="sxs-lookup"><span data-stu-id="2af44-117">To save holograms for future sessions:</span></span>
1. <span data-ttu-id="2af44-118">Obtenir le WorldAnchorStore</span><span class="sxs-lookup"><span data-stu-id="2af44-118">Get the WorldAnchorStore</span></span>
2. <span data-ttu-id="2af44-119">Enregistrer un point d’ancrage du monde spécifiant un id</span><span class="sxs-lookup"><span data-stu-id="2af44-119">Save a world anchor specifying an id</span></span>
3. <span data-ttu-id="2af44-120">Enregistrer les données relatives à l’ancrage du monde avec un id d’application</span><span class="sxs-lookup"><span data-stu-id="2af44-120">Save app data relating to the world anchor along with an id</span></span>

### <a name="getting-the-worldanchorstore"></a><span data-ttu-id="2af44-121">Obtention de la WorldAnchorStore</span><span class="sxs-lookup"><span data-stu-id="2af44-121">Getting the WorldAnchorStore</span></span>

<span data-ttu-id="2af44-122">Nous souhaitons conserver une référence à la WorldAnchorStore autour donc nous savons que nous sommes prêts à exécuter une fois que nous souhaitons effectuer une opération.</span><span class="sxs-lookup"><span data-stu-id="2af44-122">We will want to keep a reference to the WorldAnchorStore around so we know we are ready to go when we want to perform an operation.</span></span> <span data-ttu-id="2af44-123">S’agissant d’un appel asynchrone, potentiellement dès le début, nous voulons appeler</span><span class="sxs-lookup"><span data-stu-id="2af44-123">Since this is an async call, potentially as soon as start up, we want to call</span></span>

```
WorldAnchorStore.GetAsync(StoreLoaded);
```

<span data-ttu-id="2af44-124">Dans ce cas, StoreLoaded est notre gestionnaire pour lorsque le WorldAnchorStore le chargement est terminé :</span><span class="sxs-lookup"><span data-stu-id="2af44-124">StoreLoaded in this case is our handler for when the WorldAnchorStore has completed loading:</span></span>

```
private void StoreLoaded(WorldAnchorStore store)
{
       this.store = store;
}
```

<span data-ttu-id="2af44-125">Nous disposons désormais d’une référence à la WorldAnchorStore que nous utiliserons pour enregistrer et charger les ancres monde spécifique.</span><span class="sxs-lookup"><span data-stu-id="2af44-125">We now have a reference to the WorldAnchorStore which we will use to save and load specific World Anchors.</span></span>

### <a name="saving-a-worldanchor"></a><span data-ttu-id="2af44-126">L’enregistrement d’un WorldAnchor</span><span class="sxs-lookup"><span data-stu-id="2af44-126">Saving a WorldAnchor</span></span>

<span data-ttu-id="2af44-127">Pour enregistrer, nous devons simplement nommer nous enregistrez et transmettez-le dans le WorldAnchor soulevées avant lorsque vous souhaitez enregistrer.</span><span class="sxs-lookup"><span data-stu-id="2af44-127">To save, we simply need to name what we are saving and pass it in the WorldAnchor we got before when we want to save.</span></span> <span data-ttu-id="2af44-128">Remarque : la tentative d’enregistrement de deux points d’ancrage à la même chaîne échoue (magasin. Enregistrer retournera la valeur false).</span><span class="sxs-lookup"><span data-stu-id="2af44-128">Note: trying to save two anchors to the same string will fail (store.Save will return false).</span></span> <span data-ttu-id="2af44-129">Vous devez supprimer l’enregistrement précédent avant d’enregistrer une nouvelle :</span><span class="sxs-lookup"><span data-stu-id="2af44-129">You need to Delete the previous save before saving the new one:</span></span>

```
private void SaveGame()
{
       // Save data about holograms positioned by this world anchor
       if (!this.savedRoot) // Only Save the root once
       {
              this.savedRoot = this.store.Save("rootGameObject", anchor);
              Assert(this.savedRoot);
       }
}
```

### <a name="loading-a-worldanchor"></a><span data-ttu-id="2af44-130">Le chargement d’un WorldAnchor</span><span class="sxs-lookup"><span data-stu-id="2af44-130">Loading a WorldAnchor</span></span>

<span data-ttu-id="2af44-131">Et à charger :</span><span class="sxs-lookup"><span data-stu-id="2af44-131">And to load:</span></span>

```
private void LoadGame()
{
       // Save data about holograms positioned by this world anchor
       this.savedRoot = this.store.Load("rootGameObject", rootGameObject);
       if (!this.savedRoot)
       {
              // We didn't actually have the game root saved! We have to re-place our objects or start over
       }
}
```

<span data-ttu-id="2af44-132">Nous pouvons en outre utiliser le magasin. Delete() pour supprimer un point d’ancrage que nous avons précédemment enregistré et store. Clear() supprimer toutes les données précédemment enregistrées.</span><span class="sxs-lookup"><span data-stu-id="2af44-132">We additionally can use store.Delete() to remove an anchor we previously saved and store.Clear() to remove all previously saved data.</span></span>

### <a name="enumerating-existing-anchors"></a><span data-ttu-id="2af44-133">Énumération des ancres existants</span><span class="sxs-lookup"><span data-stu-id="2af44-133">Enumerating Existing Anchors</span></span>

<span data-ttu-id="2af44-134">Pour découvrir les ancres précédemment stockés, appelez GetAllIds.</span><span class="sxs-lookup"><span data-stu-id="2af44-134">To discover previously stored anchors, call GetAllIds.</span></span>

```
string[] ids = this.store.GetAllIds();
for (int index = 0; index < ids.Length; index++)
{
        Debug.Log(ids[index]);
}
```

## <a name="persisting-holograms-for-multiple-devices"></a><span data-ttu-id="2af44-135">Hologrammes persistantes pour plusieurs appareils</span><span class="sxs-lookup"><span data-stu-id="2af44-135">Persisting holograms for multiple devices</span></span>

<span data-ttu-id="2af44-136">Vous pouvez utiliser <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">ancres Spatial Azure</a> pour créer un point d’ancrage cloud durable à partir d’un WorldAnchor local, lequel votre application peut ensuite localiser dans plusieurs HoloLens, appareils iOS et Android, même si ces appareils ne sont pas présents dans le même heure.</span><span class="sxs-lookup"><span data-stu-id="2af44-136">You can use <a href="https://docs.microsoft.com/azure/spatial-anchors/overview" target="_blank">Azure Spatial Anchors</a> to create a durable cloud anchor from a local WorldAnchor, which your app can then locate across multiple HoloLens, iOS and Android devices, even if those devices are not present together at the same time.</span></span>  <span data-ttu-id="2af44-137">Étant donné que les ancres cloud sont persistants, plusieurs périphériques au fil du temps peuvent chacun voir le contenu restitué par rapport à ce point d’ancrage dans le même emplacement physique.</span><span class="sxs-lookup"><span data-stu-id="2af44-137">Because cloud anchors are persistent, multiple devices over time can each see content rendered relative to that anchor in the same physical location.</span></span>

<span data-ttu-id="2af44-138">Pour commencer à créer des expériences partagées dans Unity, essayez les 5 minutes <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Démarrages rapides Azure Spatial ancres Unity</a>.</span><span class="sxs-lookup"><span data-stu-id="2af44-138">To get started building shared experiences in Unity, try out the 5-minute <a href="https://docs.microsoft.com/azure/spatial-anchors/unity-overview" target="_blank">Azure Spatial Anchors Unity quickstarts</a>.</span></span>

<span data-ttu-id="2af44-139">Une fois que vous êtes en cours d’exécution ancres spatiale d’Azure, vous pouvez ensuite <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">créer et localiser les points d’ancrage dans Unity</a>.</span><span class="sxs-lookup"><span data-stu-id="2af44-139">Once you're up and running with Azure Spatial Anchors, you can then <a href="https://docs.microsoft.com/azure/spatial-anchors/concepts/create-locate-anchors-unity" target="_blank">create and locate anchors in Unity</a>.</span></span>

## <a name="see-also"></a><span data-ttu-id="2af44-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2af44-140">See Also</span></span>
* [<span data-ttu-id="2af44-141">Persistance de l’ancre spatial</span><span class="sxs-lookup"><span data-stu-id="2af44-141">Spatial anchor persistence</span></span>](coordinate-systems.md#spatial-anchor-persistence)
* <span data-ttu-id="2af44-142"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Ancres Spatial Azure</a></span><span class="sxs-lookup"><span data-stu-id="2af44-142"><a href="https://docs.microsoft.com/azure/spatial-anchors" target="_blank">Azure Spatial Anchors</a></span></span>
* <span data-ttu-id="2af44-143"><a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Ancres Spatial Azure SDK pour Unity</a></span><span class="sxs-lookup"><span data-stu-id="2af44-143"><a href="https://docs.microsoft.com/dotnet/api/Microsoft.Azure.SpatialAnchors" target="_blank">Azure Spatial Anchors SDK for Unity</a></span></span>
