---
title: Collection d’objets
description: Collection d’objets est un contrôle de disposition qui vous permet de disposer d’un tableau d’objets dans une forme 3D prédéfinie.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, contrôles, conception
ms.openlocfilehash: 88ab0359d5083d43d5d6312ef1185f67ca0caa7d
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597089"
---
# <a name="object-collection"></a><span data-ttu-id="ccf85-104">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="ccf85-104">Object collection</span></span>

<span data-ttu-id="ccf85-105">Collection d’objets est un contrôle de disposition qui vous permet de disposer d’un tableau d’objets dans une forme 3D prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="ccf85-105">Object collection is a layout control which helps you lay out an array of objects in a predefined three-dimensional shape.</span></span> <span data-ttu-id="ccf85-106">Il prend en charge quatre différents styles surfaces - **plan, cylindre, sphère** et **à nuages de points**.</span><span class="sxs-lookup"><span data-stu-id="ccf85-106">It supports four different surface styles - **plane, cylinder, sphere** and **scatter**.</span></span> <span data-ttu-id="ccf85-107">Vous pouvez ajuster le rayon et la taille des objets et de l’espace entre eux.</span><span class="sxs-lookup"><span data-stu-id="ccf85-107">You can adjust the radius and size of the objects and the space between them.</span></span> <span data-ttu-id="ccf85-108">Collection d’objets prend en charge n’importe quel objet à partir d’Unity - 2D et 3D.</span><span class="sxs-lookup"><span data-stu-id="ccf85-108">Object collection supports any object from Unity - both 2D and 3D.</span></span> <span data-ttu-id="ccf85-109">Dans le  **[Toolkit de réalité mixte](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/UX/Readme/README_ObjectCollection.md)**, nous avons créé le script de Unity et [scène d’exemple](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/UX/Scenes/ObjectCollectionExample.unity) qui vous aideront à créer une collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="ccf85-109">In the **[Mixed Reality Toolkit](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/UX/Readme/README_ObjectCollection.md)**, we have created Unity script and [example scene](https://github.com/Microsoft/MixedRealityToolkit-Unity/blob/htk_release/Assets/HoloToolkit-Examples/UX/Scenes/ObjectCollectionExample.unity) that will help you create an object collection.</span></span>

<span data-ttu-id="ccf85-110">![Collection d’objets utilisée dans la Table périodique de l’application d’éléments](images/640px-objectcollection-hero-640px.jpg)</span><span class="sxs-lookup"><span data-stu-id="ccf85-110">![Object collection used in the Periodic Table of the Elements app](images/640px-objectcollection-hero-640px.jpg)</span></span><br>
<span data-ttu-id="ccf85-111">*Collection d’objets utilisée dans la Table périodique de l’exemple d’application éléments*</span><span class="sxs-lookup"><span data-stu-id="ccf85-111">*Object collection used in the Periodic Table of the Elements sample app*</span></span>

## <a name="object-collection-examples"></a><span data-ttu-id="ccf85-112">Exemples de collection d’objets</span><span class="sxs-lookup"><span data-stu-id="ccf85-112">Object collection examples</span></span>

<span data-ttu-id="ccf85-113">[Tableau périodique des éléments](periodic-table-of-the-elements.md) est un exemple d’application qui illustre le fonctionne de la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="ccf85-113">[Periodic Table of the Elements](periodic-table-of-the-elements.md) is a sample app that demonstrates how Object collection works.</span></span> <span data-ttu-id="ccf85-114">Il utilise la collection d’objets pour présenter des boîtes d’élément chimique 3D dans différentes formes.</span><span class="sxs-lookup"><span data-stu-id="ccf85-114">It uses Object collection to lay out 3D chemical element boxes in different shapes.</span></span>

<span data-ttu-id="ccf85-115">![Exemples de collection d’objet indiqués dans le tableau périodique de l’application d’éléments](images/periodictable-collections-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="ccf85-115">![Object collection examples shown in the Periodic Table of the Elements app](images/periodictable-collections-1000px.jpg)</span></span><br>
<span data-ttu-id="ccf85-116">*Exemples de collection d’objet indiqués dans le tableau périodique de l’exemple d’application éléments*</span><span class="sxs-lookup"><span data-stu-id="ccf85-116">*Object collection examples shown in the Periodic Table of the Elements sample app*</span></span>

### <a name="3d-objects"></a><span data-ttu-id="ccf85-117">Objets 3D</span><span class="sxs-lookup"><span data-stu-id="ccf85-117">3D objects</span></span>

<span data-ttu-id="ccf85-118">Vous pouvez utiliser la collection d’objets pour disposer les objets 3D importés.</span><span class="sxs-lookup"><span data-stu-id="ccf85-118">You can use Object collection to lay out imported 3D objects.</span></span> <span data-ttu-id="ccf85-119">L’exemple ci-dessous montre un plan et une disposition de cylindre de certains objets CHAISE 3D.</span><span class="sxs-lookup"><span data-stu-id="ccf85-119">The example below shows a plane and a cylinder layout of some 3D chair objects.</span></span>

<span data-ttu-id="ccf85-120">![Exemples de plan et cylindriques dispositions d’objets 3D](images/objectcollection-3dobjects-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="ccf85-120">![Examples of plane and cylindrical layouts of 3D objects](images/objectcollection-3dobjects-1000px.jpg)</span></span><br>
<span data-ttu-id="ccf85-121">*Exemples de plan et cylindriques dispositions d’objets 3D*</span><span class="sxs-lookup"><span data-stu-id="ccf85-121">*Examples of plane and cylindrical layouts of 3D objects*</span></span>

### <a name="2d-objects"></a><span data-ttu-id="ccf85-122">Objets 2D</span><span class="sxs-lookup"><span data-stu-id="ccf85-122">2D objects</span></span>

<span data-ttu-id="ccf85-123">Vous pouvez également utiliser des images 2D avec la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="ccf85-123">You can also use 2D images with Object collection.</span></span> <span data-ttu-id="ccf85-124">Les exemples suivants illustrent comment 2D images peuvent être affichés dans une grille.</span><span class="sxs-lookup"><span data-stu-id="ccf85-124">The examples below demonstrate how 2D images can be displayed in a grid.</span></span>

![Un exemple des images 2D avec la collection d’objets](images/640px-layout-3dobjects-3.jpg)

<span data-ttu-id="ccf85-126">![Un exemple des images 2D avec la collection d’objets](images/640px-layout-2dimages.jpg)</span><span class="sxs-lookup"><span data-stu-id="ccf85-126">![An example of 2D images with Object collection](images/640px-layout-2dimages.jpg)</span></span><br>
<span data-ttu-id="ccf85-127">*Exemples d’images 2D avec la collection d’objets*</span><span class="sxs-lookup"><span data-stu-id="ccf85-127">*Examples of 2D images with object collection*</span></span>

## <a name="see-also"></a><span data-ttu-id="ccf85-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ccf85-128">See also</span></span>
* [<span data-ttu-id="ccf85-129">Scripts et prefabs pour la collection d’objets dans la boîte à outils de réalité mixte sur GitHub</span><span class="sxs-lookup"><span data-stu-id="ccf85-129">Scripts and prefabs for Object collection in the Mixed Reality Toolkit on GitHub</span></span>](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Examples/UX)
* [<span data-ttu-id="ccf85-130">Objet sur</span><span class="sxs-lookup"><span data-stu-id="ccf85-130">Interactable object</span></span>](interactable-object.md)
