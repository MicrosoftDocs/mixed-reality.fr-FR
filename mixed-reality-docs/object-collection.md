---
title: Collection d’objets
description: La collection d’objets est un contrôle de disposition qui vous permet de disposer un tableau d’objets dans une forme à trois dimensions prédéfinie.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, contrôles, conception
ms.openlocfilehash: 8f3629c6d9465383efc901ed784a3719cd6fdfb2
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438169"
---
# <a name="object-collection"></a><span data-ttu-id="5fd9f-104">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="5fd9f-104">Object collection</span></span>

![Collection d’objets utilisée dans la table périodique de l’application d’éléments](images/640px-objectcollection-hero-640px.jpg)<br>


<span data-ttu-id="5fd9f-106">La collection d’objets est un contrôle de disposition qui vous permet de disposer un tableau d’objets dans une forme à trois dimensions prédéfinie.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-106">Object collection is a layout control which helps you lay out an array of objects in a predefined three-dimensional shape.</span></span> <span data-ttu-id="5fd9f-107">Il prend en charge divers styles de surface : **plan, cylindre, sphère** et **radial**.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-107">It supports various surface styles - **plane, cylinder, sphere** and **radial**.</span></span> <span data-ttu-id="5fd9f-108">Vous pouvez ajuster le rayon et la taille des objets, ainsi que l’espace entre eux.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-108">You can adjust the radius and size of the objects and the space between them.</span></span> <span data-ttu-id="5fd9f-109">La collection d’objets prend en charge n’importe quel objet d’Unity, à la fois 2D et 3D.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-109">Object collection supports any object from Unity - both 2D and 3D.</span></span> <span data-ttu-id="5fd9f-110">Dans la **[boîte à outils de la réalité mixte](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html)** , nous avons créé un script Unity et des exemples qui vous aideront à créer une collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-110">In the **[Mixed Reality Toolkit](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/README_ObjectCollection.html)**, we have created Unity script and examples that will help you create an object collection.</span></span>


## <a name="object-collection-examples"></a><span data-ttu-id="5fd9f-111">Exemples de collection d’objets</span><span class="sxs-lookup"><span data-stu-id="5fd9f-111">Object collection examples</span></span>

<span data-ttu-id="5fd9f-112">[La table périodique des éléments](periodic-table-of-the-elements.md) est un exemple d’application qui illustre le fonctionnement de la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-112">[Periodic Table of the Elements](periodic-table-of-the-elements.md) is a sample app that demonstrates how Object collection works.</span></span> <span data-ttu-id="5fd9f-113">Elle utilise la collection d’objets pour disposer les zones d’éléments chimiques 3D dans différentes formes.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-113">It uses Object collection to lay out 3D chemical element boxes in different shapes.</span></span>

<span data-ttu-id="5fd9f-114">![exemples de collection d’objets affichés dans la table périodique des éléments de l’application](images/periodictable-collections-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="5fd9f-114">![Object collection examples shown in the Periodic Table of the Elements app](images/periodictable-collections-1000px.jpg)</span></span><br>
<span data-ttu-id="5fd9f-115">*Exemples de collection d’objets affichés dans la table periode de l’exemple d’application d’éléments*</span><span class="sxs-lookup"><span data-stu-id="5fd9f-115">*Object collection examples shown in the Periodic Table of the Elements sample app*</span></span>

### <a name="3d-objects"></a><span data-ttu-id="5fd9f-116">objets 3D</span><span class="sxs-lookup"><span data-stu-id="5fd9f-116">3D objects</span></span>

<span data-ttu-id="5fd9f-117">Vous pouvez utiliser la collection d’objets pour disposer les objets 3D importés.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-117">You can use Object collection to lay out imported 3D objects.</span></span> <span data-ttu-id="5fd9f-118">L’exemple ci-dessous montre un plan et une disposition cylindrique de certains objets de chaise 3D.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-118">The example below shows a plane and a cylinder layout of some 3D chair objects.</span></span>

<span data-ttu-id="5fd9f-119">![des exemples de dispositions planes et cylindriques d’objets 3D](images/objectcollection-3dobjects-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="5fd9f-119">![Examples of plane and cylindrical layouts of 3D objects](images/objectcollection-3dobjects-1000px.jpg)</span></span><br>
<span data-ttu-id="5fd9f-120">*Exemples de dispositions planes et cylindriques d’objets 3D*</span><span class="sxs-lookup"><span data-stu-id="5fd9f-120">*Examples of plane and cylindrical layouts of 3D objects*</span></span>

### <a name="2d-objects"></a><span data-ttu-id="5fd9f-121">objets 2D</span><span class="sxs-lookup"><span data-stu-id="5fd9f-121">2D objects</span></span>

<span data-ttu-id="5fd9f-122">Vous pouvez également utiliser des images 2D avec la collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-122">You can also use 2D images with Object collection.</span></span> <span data-ttu-id="5fd9f-123">Les exemples ci-dessous montrent comment les images 2D peuvent être affichées dans une grille.</span><span class="sxs-lookup"><span data-stu-id="5fd9f-123">The examples below demonstrate how 2D images can be displayed in a grid.</span></span>

![Exemple d’images 2D avec la collection d’objets](images/940px-layout-3dobjects-3.jpg)

<span data-ttu-id="5fd9f-125">![un exemple d’images 2D avec la collection d’objets](images/940px-layout-2dimages.jpg)</span><span class="sxs-lookup"><span data-stu-id="5fd9f-125">![An example of 2D images with Object collection](images/940px-layout-2dimages.jpg)</span></span><br>
<span data-ttu-id="5fd9f-126">*Exemples d’utilisation de la collection d’objets avec des images 2D*</span><span class="sxs-lookup"><span data-stu-id="5fd9f-126">*Examples of using object collection with 2D images*</span></span>

## <a name="see-also"></a><span data-ttu-id="5fd9f-127">Articles associés</span><span class="sxs-lookup"><span data-stu-id="5fd9f-127">See also</span></span>
* [<span data-ttu-id="5fd9f-128">Scripts et prefabs pour la collection d’objets dans le Toolkit de réalité mixte sur GitHub</span><span class="sxs-lookup"><span data-stu-id="5fd9f-128">Scripts and prefabs for Object collection in the Mixed Reality Toolkit on GitHub</span></span>](https://github.com/microsoft/MixedRealityToolkit-Unity/blob/mrtk_release/Documentation/README_ObjectCollection.md)
* [<span data-ttu-id="5fd9f-129">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="5fd9f-129">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="5fd9f-130">Cadre englobant</span><span class="sxs-lookup"><span data-stu-id="5fd9f-130">Bounding Box</span></span>](app-bar-and-bounding-box.md)
