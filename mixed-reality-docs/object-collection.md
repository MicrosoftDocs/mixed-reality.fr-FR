---
title: Collection d’objets
description: La collection d’objets est un contrôle de disposition qui vous permet de disposer un tableau d’objets dans une forme à trois dimensions prédéfinie.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, contrôles, conception
ms.openlocfilehash: 7c3bbd82ec909b5a2e3c81f122366be564934f4d
ms.sourcegitcommit: c6b59f532a9c5818d9b25c355a174a231f5fa943
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66813892"
---
# <a name="object-collection"></a><span data-ttu-id="1fcf9-104">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="1fcf9-104">Object collection</span></span>

<span data-ttu-id="1fcf9-105">La collection d’objets est un contrôle de disposition qui vous permet de disposer un tableau d’objets dans une forme à trois dimensions prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-105">Object collection is a layout control which helps you lay out an array of objects in a predefined three-dimensional shape.</span></span> <span data-ttu-id="1fcf9-106">Il prend en charge divers styles de surface: **plan, cylindre, sphère** et **radial**.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-106">It supports various surface styles - **plane, cylinder, sphere** and **radial**.</span></span> <span data-ttu-id="1fcf9-107">Vous pouvez ajuster le rayon et la taille des objets, ainsi que l’espace entre eux.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-107">You can adjust the radius and size of the objects and the space between them.</span></span> <span data-ttu-id="1fcf9-108">La collection d’objets prend en charge n’importe quel objet d’Unity, à la fois 2D et 3D.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-108">Object collection supports any object from Unity - both 2D and 3D.</span></span> <span data-ttu-id="1fcf9-109">Dans la **[boîte à outils de la réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html)** , nous avons créé un script Unity et des exemples qui vous aideront à créer une collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-109">In the **[Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html)**, we have created Unity script and examples that will help you create an object collection.</span></span>

<span data-ttu-id="1fcf9-110">![Collection d’objets utilisée dans la table périodique de l’application d’éléments](images/640px-objectcollection-hero-640px.jpg)</span><span class="sxs-lookup"><span data-stu-id="1fcf9-110">![Object collection used in the Periodic Table of the Elements app](images/640px-objectcollection-hero-640px.jpg)</span></span><br>
<span data-ttu-id="1fcf9-111">*Exemples d’utilisation de la collection d’objets*</span><span class="sxs-lookup"><span data-stu-id="1fcf9-111">*Examples of using object collection*</span></span>

## <a name="object-collection-examples"></a><span data-ttu-id="1fcf9-112">Exemples de collection d’objets</span><span class="sxs-lookup"><span data-stu-id="1fcf9-112">Object collection examples</span></span>

<span data-ttu-id="1fcf9-113">[La table périodique des éléments](periodic-table-of-the-elements.md) est un exemple d’application qui illustre le fonctionnement de la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-113">[Periodic Table of the Elements](periodic-table-of-the-elements.md) is a sample app that demonstrates how Object collection works.</span></span> <span data-ttu-id="1fcf9-114">Elle utilise la collection d’objets pour disposer les zones d’éléments chimiques 3D dans différentes formes.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-114">It uses Object collection to lay out 3D chemical element boxes in different shapes.</span></span>

<span data-ttu-id="1fcf9-115">![Exemples de collection d’objets affichés dans la table periode de l’application Elements](images/periodictable-collections-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="1fcf9-115">![Object collection examples shown in the Periodic Table of the Elements app](images/periodictable-collections-1000px.jpg)</span></span><br>
<span data-ttu-id="1fcf9-116">*Exemples de collection d’objets affichés dans la table periode de l’exemple d’application d’éléments*</span><span class="sxs-lookup"><span data-stu-id="1fcf9-116">*Object collection examples shown in the Periodic Table of the Elements sample app*</span></span>

### <a name="3d-objects"></a><span data-ttu-id="1fcf9-117">objets 3D</span><span class="sxs-lookup"><span data-stu-id="1fcf9-117">3D objects</span></span>

<span data-ttu-id="1fcf9-118">Vous pouvez utiliser la collection d’objets pour disposer les objets 3D importés.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-118">You can use Object collection to lay out imported 3D objects.</span></span> <span data-ttu-id="1fcf9-119">L’exemple ci-dessous montre un plan et une disposition cylindrique de certains objets de chaise 3D.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-119">The example below shows a plane and a cylinder layout of some 3D chair objects.</span></span>

<span data-ttu-id="1fcf9-120">![Exemples de dispositions planes et cylindriques d’objets 3D](images/objectcollection-3dobjects-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="1fcf9-120">![Examples of plane and cylindrical layouts of 3D objects](images/objectcollection-3dobjects-1000px.jpg)</span></span><br>
<span data-ttu-id="1fcf9-121">*Exemples de dispositions planes et cylindriques d’objets 3D*</span><span class="sxs-lookup"><span data-stu-id="1fcf9-121">*Examples of plane and cylindrical layouts of 3D objects*</span></span>

### <a name="2d-objects"></a><span data-ttu-id="1fcf9-122">objets 2D</span><span class="sxs-lookup"><span data-stu-id="1fcf9-122">2D objects</span></span>

<span data-ttu-id="1fcf9-123">Vous pouvez également utiliser des images 2D avec la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-123">You can also use 2D images with Object collection.</span></span> <span data-ttu-id="1fcf9-124">Les exemples ci-dessous montrent comment les images 2D peuvent être affichées dans une grille.</span><span class="sxs-lookup"><span data-stu-id="1fcf9-124">The examples below demonstrate how 2D images can be displayed in a grid.</span></span>

![Exemple d’images 2D avec la collection d’objets](images/640px-layout-3dobjects-3.jpg)

<span data-ttu-id="1fcf9-126">![Exemple d’images 2D avec la collection d’objets](images/640px-layout-2dimages.jpg)</span><span class="sxs-lookup"><span data-stu-id="1fcf9-126">![An example of 2D images with Object collection](images/640px-layout-2dimages.jpg)</span></span><br>
<span data-ttu-id="1fcf9-127">*Exemples d’utilisation de la collection d’objets avec des images 2D*</span><span class="sxs-lookup"><span data-stu-id="1fcf9-127">*Examples of using object collection with 2D images*</span></span>

## <a name="see-also"></a><span data-ttu-id="1fcf9-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1fcf9-128">See also</span></span>
* [<span data-ttu-id="1fcf9-129">Scripts et prefabs pour la collection d’objets dans le Toolkit de réalité mixte sur GitHub</span><span class="sxs-lookup"><span data-stu-id="1fcf9-129">Scripts and prefabs for Object collection in the Mixed Reality Toolkit on GitHub</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_ObjectCollection.md)
* [<span data-ttu-id="1fcf9-130">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="1fcf9-130">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="1fcf9-131">Cadre englobant</span><span class="sxs-lookup"><span data-stu-id="1fcf9-131">Bounding Box</span></span>](app-bar-and-bounding-box.md)
