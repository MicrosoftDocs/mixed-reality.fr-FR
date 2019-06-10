---
title: Collection d’objets
description: Collection d’objets est un contrôle de disposition qui vous permet de disposer d’un tableau d’objets dans une forme 3D prédéfinie.
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
# <a name="object-collection"></a><span data-ttu-id="19b07-104">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="19b07-104">Object collection</span></span>

<span data-ttu-id="19b07-105">Collection d’objets est un contrôle de disposition qui vous permet de disposer d’un tableau d’objets dans une forme 3D prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="19b07-105">Object collection is a layout control which helps you lay out an array of objects in a predefined three-dimensional shape.</span></span> <span data-ttu-id="19b07-106">Il prend en charge divers styles de surface - **plan, cylindre, sphère** et **radiale**.</span><span class="sxs-lookup"><span data-stu-id="19b07-106">It supports various surface styles - **plane, cylinder, sphere** and **radial**.</span></span> <span data-ttu-id="19b07-107">Vous pouvez ajuster le rayon et la taille des objets et de l’espace entre eux.</span><span class="sxs-lookup"><span data-stu-id="19b07-107">You can adjust the radius and size of the objects and the space between them.</span></span> <span data-ttu-id="19b07-108">Collection d’objets prend en charge n’importe quel objet à partir d’Unity - 2D et 3D.</span><span class="sxs-lookup"><span data-stu-id="19b07-108">Object collection supports any object from Unity - both 2D and 3D.</span></span> <span data-ttu-id="19b07-109">Dans le  **[Toolkit de réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html)** , nous avons créé le script de Unity et obtenir des exemples qui vous aideront à créent une collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="19b07-109">In the **[Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html)**, we have created Unity script and examples that will help you create an object collection.</span></span>

<span data-ttu-id="19b07-110">![Collection d’objets utilisée dans la Table périodique de l’application d’éléments](images/640px-objectcollection-hero-640px.jpg)</span><span class="sxs-lookup"><span data-stu-id="19b07-110">![Object collection used in the Periodic Table of the Elements app](images/640px-objectcollection-hero-640px.jpg)</span></span><br>
<span data-ttu-id="19b07-111">*Exemples d’utilisation de collection d’objets*</span><span class="sxs-lookup"><span data-stu-id="19b07-111">*Examples of using object collection*</span></span>

## <a name="object-collection-examples"></a><span data-ttu-id="19b07-112">Exemples de collection d’objets</span><span class="sxs-lookup"><span data-stu-id="19b07-112">Object collection examples</span></span>

<span data-ttu-id="19b07-113">[Tableau périodique des éléments](periodic-table-of-the-elements.md) est un exemple d’application qui illustre le fonctionne de la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="19b07-113">[Periodic Table of the Elements](periodic-table-of-the-elements.md) is a sample app that demonstrates how Object collection works.</span></span> <span data-ttu-id="19b07-114">Il utilise la collection d’objets pour présenter des boîtes d’élément chimique 3D dans différentes formes.</span><span class="sxs-lookup"><span data-stu-id="19b07-114">It uses Object collection to lay out 3D chemical element boxes in different shapes.</span></span>

<span data-ttu-id="19b07-115">![Exemples de collection d’objet indiqués dans le tableau périodique de l’application d’éléments](images/periodictable-collections-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="19b07-115">![Object collection examples shown in the Periodic Table of the Elements app](images/periodictable-collections-1000px.jpg)</span></span><br>
<span data-ttu-id="19b07-116">*Exemples de collection d’objet indiqués dans le tableau périodique de l’exemple d’application éléments*</span><span class="sxs-lookup"><span data-stu-id="19b07-116">*Object collection examples shown in the Periodic Table of the Elements sample app*</span></span>

### <a name="3d-objects"></a><span data-ttu-id="19b07-117">Objets 3D</span><span class="sxs-lookup"><span data-stu-id="19b07-117">3D objects</span></span>

<span data-ttu-id="19b07-118">Vous pouvez utiliser la collection d’objets pour disposer les objets 3D importés.</span><span class="sxs-lookup"><span data-stu-id="19b07-118">You can use Object collection to lay out imported 3D objects.</span></span> <span data-ttu-id="19b07-119">L’exemple ci-dessous montre un plan et une disposition de cylindre de certains objets CHAISE 3D.</span><span class="sxs-lookup"><span data-stu-id="19b07-119">The example below shows a plane and a cylinder layout of some 3D chair objects.</span></span>

<span data-ttu-id="19b07-120">![Exemples de plan et cylindriques dispositions d’objets 3D](images/objectcollection-3dobjects-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="19b07-120">![Examples of plane and cylindrical layouts of 3D objects](images/objectcollection-3dobjects-1000px.jpg)</span></span><br>
<span data-ttu-id="19b07-121">*Exemples de plan et cylindriques dispositions d’objets 3D*</span><span class="sxs-lookup"><span data-stu-id="19b07-121">*Examples of plane and cylindrical layouts of 3D objects*</span></span>

### <a name="2d-objects"></a><span data-ttu-id="19b07-122">Objets 2D</span><span class="sxs-lookup"><span data-stu-id="19b07-122">2D objects</span></span>

<span data-ttu-id="19b07-123">Vous pouvez également utiliser des images 2D avec la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="19b07-123">You can also use 2D images with Object collection.</span></span> <span data-ttu-id="19b07-124">Les exemples suivants illustrent comment 2D images peuvent être affichés dans une grille.</span><span class="sxs-lookup"><span data-stu-id="19b07-124">The examples below demonstrate how 2D images can be displayed in a grid.</span></span>

![Un exemple des images 2D avec la collection d’objets](images/640px-layout-3dobjects-3.jpg)

<span data-ttu-id="19b07-126">![Un exemple des images 2D avec la collection d’objets](images/640px-layout-2dimages.jpg)</span><span class="sxs-lookup"><span data-stu-id="19b07-126">![An example of 2D images with Object collection](images/640px-layout-2dimages.jpg)</span></span><br>
<span data-ttu-id="19b07-127">*Exemples de l’utilisation de la collection d’objets avec des images 2D*</span><span class="sxs-lookup"><span data-stu-id="19b07-127">*Examples of using object collection with 2D images*</span></span>

## <a name="see-also"></a><span data-ttu-id="19b07-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="19b07-128">See also</span></span>
* [<span data-ttu-id="19b07-129">Scripts et prefabs pour la collection d’objets dans la boîte à outils de réalité mixte sur GitHub</span><span class="sxs-lookup"><span data-stu-id="19b07-129">Scripts and prefabs for Object collection in the Mixed Reality Toolkit on GitHub</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_ObjectCollection.md)
* [<span data-ttu-id="19b07-130">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="19b07-130">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="19b07-131">Zone englobante</span><span class="sxs-lookup"><span data-stu-id="19b07-131">Bounding Box</span></span>](app-bar-and-bounding-box.md)
