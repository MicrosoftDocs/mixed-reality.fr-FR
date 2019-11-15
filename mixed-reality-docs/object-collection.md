---
title: Collection d’objets
description: La collection d’objets est un contrôle de disposition qui vous permet de disposer un tableau d’objets dans une forme à trois dimensions prédéfinie.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, contrôles, conception
ms.openlocfilehash: 98fec76558502658511faf3f18d623bfa5a49dc2
ms.sourcegitcommit: 781e47db2ca2f2c792c95e76ac309b44b3535555
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74106005"
---
# <a name="object-collection"></a><span data-ttu-id="4f937-104">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="4f937-104">Object collection</span></span>

![Collection d’objets utilisée dans la table périodique de l’application d’éléments](images/UX/UX_Hero_ObjectCollection.jpg)<br>


<span data-ttu-id="4f937-106">La collection d’objets est un contrôle de disposition qui vous permet de disposer un tableau d’objets dans une forme à trois dimensions prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="4f937-106">Object collection is a layout control which helps you lay out an array of objects in a predefined three-dimensional shape.</span></span> <span data-ttu-id="4f937-107">Il prend en charge divers styles de surface : **plan, cylindre, sphère** et **radial**.</span><span class="sxs-lookup"><span data-stu-id="4f937-107">It supports various surface styles - **plane, cylinder, sphere** and **radial**.</span></span> <span data-ttu-id="4f937-108">Vous pouvez ajuster le rayon et la taille des objets, ainsi que l’espace entre eux.</span><span class="sxs-lookup"><span data-stu-id="4f937-108">You can adjust the radius and size of the objects and the space between them.</span></span> <span data-ttu-id="4f937-109">La collection d’objets prend en charge n’importe quel objet d’Unity, à la fois 2D et 3D.</span><span class="sxs-lookup"><span data-stu-id="4f937-109">Object collection supports any object from Unity - both 2D and 3D.</span></span> <span data-ttu-id="4f937-110">Dans la **[boîte à outils de la réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html)** , nous avons créé un script Unity et des exemples qui vous aideront à créer une collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="4f937-110">In the **[Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html)**, we have created Unity script and examples that will help you create an object collection.</span></span>


## <a name="object-collection-examples"></a><span data-ttu-id="4f937-111">Exemples de collection d’objets</span><span class="sxs-lookup"><span data-stu-id="4f937-111">Object collection examples</span></span>

<span data-ttu-id="4f937-112">[La table périodique des éléments](periodic-table-of-the-elements.md) est un exemple d’application qui illustre le fonctionnement de la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="4f937-112">[Periodic Table of the Elements](periodic-table-of-the-elements.md) is a sample app that demonstrates how Object collection works.</span></span> <span data-ttu-id="4f937-113">Elle utilise la collection d’objets pour disposer les zones d’éléments chimiques 3D dans différentes formes.</span><span class="sxs-lookup"><span data-stu-id="4f937-113">It uses Object collection to lay out 3D chemical element boxes in different shapes.</span></span>

<span data-ttu-id="4f937-114">![exemples de collection d’objets affichés dans la table périodique des éléments de l’application](images/periodictable-collections-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="4f937-114">![Object collection examples shown in the Periodic Table of the Elements app](images/periodictable-collections-1000px.jpg)</span></span><br>
<span data-ttu-id="4f937-115">*Exemples de collection d’objets affichés dans la table periode de l’exemple d’application d’éléments*</span><span class="sxs-lookup"><span data-stu-id="4f937-115">*Object collection examples shown in the Periodic Table of the Elements sample app*</span></span>

### <a name="3d-objects"></a><span data-ttu-id="4f937-116">objets 3D</span><span class="sxs-lookup"><span data-stu-id="4f937-116">3D objects</span></span>

<span data-ttu-id="4f937-117">Vous pouvez utiliser la collection d’objets pour disposer les objets 3D importés.</span><span class="sxs-lookup"><span data-stu-id="4f937-117">You can use Object collection to lay out imported 3D objects.</span></span> <span data-ttu-id="4f937-118">L’exemple ci-dessous montre un plan et une disposition cylindrique de certains objets de chaise 3D.</span><span class="sxs-lookup"><span data-stu-id="4f937-118">The example below shows a plane and a cylinder layout of some 3D chair objects.</span></span>

<span data-ttu-id="4f937-119">![des exemples de dispositions planes et cylindriques d’objets 3D](images/objectcollection-3dobjects-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="4f937-119">![Examples of plane and cylindrical layouts of 3D objects](images/objectcollection-3dobjects-1000px.jpg)</span></span><br>
<span data-ttu-id="4f937-120">*Exemples de dispositions planes et cylindriques d’objets 3D*</span><span class="sxs-lookup"><span data-stu-id="4f937-120">*Examples of plane and cylindrical layouts of 3D objects*</span></span>

### <a name="2d-objects"></a><span data-ttu-id="4f937-121">objets 2D</span><span class="sxs-lookup"><span data-stu-id="4f937-121">2D objects</span></span>

<span data-ttu-id="4f937-122">Vous pouvez également utiliser des images 2D avec la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="4f937-122">You can also use 2D images with Object collection.</span></span> <span data-ttu-id="4f937-123">Les exemples ci-dessous montrent comment les images 2D peuvent être affichées dans une grille.</span><span class="sxs-lookup"><span data-stu-id="4f937-123">The examples below demonstrate how 2D images can be displayed in a grid.</span></span>

![Exemple d’images 2D avec la collection d’objets](images/940px-layout-3dobjects-3.jpg)

<span data-ttu-id="4f937-125">![un exemple d’images 2D avec la collection d’objets](images/940px-layout-2dimages.jpg)</span><span class="sxs-lookup"><span data-stu-id="4f937-125">![An example of 2D images with Object collection](images/940px-layout-2dimages.jpg)</span></span><br>
<span data-ttu-id="4f937-126">*Exemples d’utilisation de la collection d’objets avec des images 2D*</span><span class="sxs-lookup"><span data-stu-id="4f937-126">*Examples of using object collection with 2D images*</span></span>

<br>

---

## <a name="object-collection-in-mrtkmixed-reality-toolkit-for-unity"></a><span data-ttu-id="4f937-127">Collection d’objets dans MRTK (Mixed Reality Toolkit) pour Unity</span><span class="sxs-lookup"><span data-stu-id="4f937-127">Object collection in MRTK(Mixed Reality Toolkit) for Unity</span></span>

* [<span data-ttu-id="4f937-128">MRTK-collection d’objets</span><span class="sxs-lookup"><span data-stu-id="4f937-128">MRTK - Object collection</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html)


<br>

---


## <a name="see-also"></a><span data-ttu-id="4f937-129">Articles associés</span><span class="sxs-lookup"><span data-stu-id="4f937-129">See also</span></span>

* [<span data-ttu-id="4f937-130">Curseurs</span><span class="sxs-lookup"><span data-stu-id="4f937-130">Cursors</span></span>](cursors.md)
* [<span data-ttu-id="4f937-131">Rayon de la main</span><span class="sxs-lookup"><span data-stu-id="4f937-131">Hand ray</span></span>](point-and-commit.md)
* [<span data-ttu-id="4f937-132">Button</span><span class="sxs-lookup"><span data-stu-id="4f937-132">Button</span></span>](button.md)
* [<span data-ttu-id="4f937-133">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="4f937-133">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="4f937-134">Rectangle englobant et barre de l’application</span><span class="sxs-lookup"><span data-stu-id="4f937-134">Bounding box and App bar</span></span>](app-bar-and-bounding-box.md)
* [<span data-ttu-id="4f937-135">Manoeuvr</span><span class="sxs-lookup"><span data-stu-id="4f937-135">Manipulation</span></span>](direct-manipulation.md)
* [<span data-ttu-id="4f937-136">Menu de la main</span><span class="sxs-lookup"><span data-stu-id="4f937-136">Hand menu</span></span>](hand-menu.md)
* [<span data-ttu-id="4f937-137">Menu proche</span><span class="sxs-lookup"><span data-stu-id="4f937-137">Near menu</span></span>](near-menu.md)
* [<span data-ttu-id="4f937-138">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="4f937-138">Object collection</span></span>](object-collection.md)
* [<span data-ttu-id="4f937-139">Commande vocale</span><span class="sxs-lookup"><span data-stu-id="4f937-139">Voice command</span></span>](voice-input.md)
* [<span data-ttu-id="4f937-140">Clavier</span><span class="sxs-lookup"><span data-stu-id="4f937-140">Keyboard</span></span>](keyboard.md)
* [<span data-ttu-id="4f937-141">Bulle</span><span class="sxs-lookup"><span data-stu-id="4f937-141">Tooltip</span></span>](tooltip.md)
* [<span data-ttu-id="4f937-142">Médias</span><span class="sxs-lookup"><span data-stu-id="4f937-142">Slate</span></span>](slate.md)
* [<span data-ttu-id="4f937-143">Curseur</span><span class="sxs-lookup"><span data-stu-id="4f937-143">Slider</span></span>](slider.md)
* [<span data-ttu-id="4f937-144">Billboarding et tag-along</span><span class="sxs-lookup"><span data-stu-id="4f937-144">Billboarding and tag-along</span></span>](billboarding-and-tag-along.md)
* [<span data-ttu-id="4f937-145">Affichage de la progression</span><span class="sxs-lookup"><span data-stu-id="4f937-145">Displaying progress</span></span>](progress.md)
* [<span data-ttu-id="4f937-146">Aimantation de surface</span><span class="sxs-lookup"><span data-stu-id="4f937-146">Surface magnetism</span></span>](surface-magnetism.md)
