---
title: Tableau périodique des éléments
description: Tableau périodique des éléments est un exemple de l’open source d’application à partir mixte réalité conception Labs de Microsoft, où vous pouvez apprendre à disposer d’un tableau d’objets dans l’espace 3D avec différents types de surface à l’aide d’une collection d’objets.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, exemple d’application, contrôles
ms.openlocfilehash: ad95d2bcfd1b70d805adcceb36be0c6c29b838f0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596694"
---
# <a name="periodic-table-of-the-elements"></a><span data-ttu-id="bec23-104">Tableau périodique des éléments</span><span class="sxs-lookup"><span data-stu-id="bec23-104">Periodic Table of the Elements</span></span>

>[!NOTE]
><span data-ttu-id="bec23-105">Cet article présente un exemple exploratoire, nous avons créé dans le [laboratoires de conception de réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity), un emplacement où nous partageons nos connaissances acquises sur et des suggestions pour développement d’applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="bec23-105">This article discusses an exploratory sample we’ve created in the [Mixed Reality Design Labs](https://github.com/Microsoft/MRDesignLabs_Unity), a place where we share our learnings about and suggestions for mixed reality app development.</span></span> <span data-ttu-id="bec23-106">Nos articles relatifs à la conception et le code évoluera lors de nos nouvelles découvertes.</span><span class="sxs-lookup"><span data-stu-id="bec23-106">Our design-related articles and code will evolve as we make new discoveries.</span></span>

<span data-ttu-id="bec23-107">[Tableau périodique des éléments](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable) est un exemple de l’open source d’application à partir de laboratoires de conception réalité mixte de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bec23-107">[Periodic Table of the Elements](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable) is a open-source sample app from Microsoft's Mixed Reality Design Labs.</span></span> <span data-ttu-id="bec23-108">Avec ce projet, vous pouvez apprendre à disposer d’un tableau d’objets dans l’espace 3D avec différents types de surface à l’aide un  **[collection d’objets](object-collection.md)**.</span><span class="sxs-lookup"><span data-stu-id="bec23-108">With this project, you can learn how to lay out an array of objects in 3D space with various surface types using an **[Object collection](object-collection.md)**.</span></span> <span data-ttu-id="bec23-109">Découvrez également comment créer des objets sur qui répondent aux entrées standards à partir de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="bec23-109">Also learn how to create interactable objects that respond to standard inputs from HoloLens.</span></span> <span data-ttu-id="bec23-110">Vous pouvez utiliser les composants de ce projet pour créer vos propres mixte d’expérience d’application de réalité.</span><span class="sxs-lookup"><span data-stu-id="bec23-110">You can use this project's components to create your own mixed reality app experience.</span></span>

![Table des périodes de l’application d’éléments](images/640px-periodictable-hero.jpg)

## <a name="about-the-app"></a><span data-ttu-id="bec23-112">À propos de l’application</span><span class="sxs-lookup"><span data-stu-id="bec23-112">About the app</span></span>

<span data-ttu-id="bec23-113">Tableau périodique des éléments permet de visualiser les éléments sur les produits chimiques et chacune de leurs propriétés dans un espace 3D.</span><span class="sxs-lookup"><span data-stu-id="bec23-113">Periodic Table of the Elements visualizes the chemical elements and each of their properties in a 3D space.</span></span> <span data-ttu-id="bec23-114">Il intègre les interactions de base de HoloLens tels que des regards et air tap.</span><span class="sxs-lookup"><span data-stu-id="bec23-114">It incorporates the basic interactions of HoloLens such as gaze and air tap.</span></span> <span data-ttu-id="bec23-115">Les utilisateurs peuvent en savoir plus sur les éléments avec des modèles 3D animés.</span><span class="sxs-lookup"><span data-stu-id="bec23-115">Users can learn about the elements with animated 3D models.</span></span> <span data-ttu-id="bec23-116">Ils comprennent visuellement interpréteur de commandes d’un élément d’électrons et son noyau - composé de protons et neutrons.</span><span class="sxs-lookup"><span data-stu-id="bec23-116">They can visually understand an element's electron shell and its nucleus - which is composed of protons and neutrons.</span></span>

## <a name="background"></a><span data-ttu-id="bec23-117">Arrière-plan</span><span class="sxs-lookup"><span data-stu-id="bec23-117">Background</span></span>

<span data-ttu-id="bec23-118">Une fois que j’ai rencontré tout d’abord HoloLens, une application de tableau périodique était une idée, que je savais que je souhaitais faire des essais avec en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="bec23-118">After I first experienced HoloLens, a periodic table app was an idea I knew that I wanted to experiment with in mixed reality.</span></span> <span data-ttu-id="bec23-119">Étant donné que chaque élément a plusieurs points de données qui sont affichées en texte, j’ai pensé qu’il serait très sujet pour l’exploration de composition typographique dans un espace 3D.</span><span class="sxs-lookup"><span data-stu-id="bec23-119">Since each element has many data points that are displayed with text, I thought it would be great subject matter for exploring typographic composition in a 3D space.</span></span> <span data-ttu-id="bec23-120">La possibilité de visualiser le modèle de l’élément d’électrons était une autre partie intéressante de ce projet.</span><span class="sxs-lookup"><span data-stu-id="bec23-120">Being able to visualize the element's electron model was another interesting part of this project.</span></span>

## <a name="design"></a><span data-ttu-id="bec23-121">Concevoir</span><span class="sxs-lookup"><span data-stu-id="bec23-121">Design</span></span>

<span data-ttu-id="bec23-122">Pour l’affichage par défaut de la table périodique, j’ai imaginé boîtes à trois dimensions qui contient le modèle d’électrons de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="bec23-122">For the default view of the periodic table, I imagined three-dimensional boxes that would contain the electron model of each element.</span></span> <span data-ttu-id="bec23-123">La surface de chaque zone serait translucide afin que l’utilisateur peut obtenir une idée approximative du volume de l’élément.</span><span class="sxs-lookup"><span data-stu-id="bec23-123">The surface of each box would be translucent so that the user could get a rough idea of the element's volume.</span></span> <span data-ttu-id="bec23-124">Un appui sur regards et air, l’utilisateur peut ouvrir une vue détaillée de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="bec23-124">With gaze and air tap, the user could open up a detailed view of each element.</span></span> <span data-ttu-id="bec23-125">Pour rendre la transition entre la vue de table et affichage des détails sans heurts et naturelle, je me suis semblable à l’interaction physique d’une zone d’ouverture dans la vie réelle.</span><span class="sxs-lookup"><span data-stu-id="bec23-125">To make the transition between table view and detail view smooth and natural, I made it similar to the physical interaction of a box opening in real life.</span></span>

<span data-ttu-id="bec23-126">![Ébauche de projet de conception](images/640px-sketch20170406.jpg)</span><span class="sxs-lookup"><span data-stu-id="bec23-126">![Design sketch](images/640px-sketch20170406.jpg)</span></span><br>
<span data-ttu-id="bec23-127">*Conception des croquis*</span><span class="sxs-lookup"><span data-stu-id="bec23-127">*Design sketches*</span></span>

<span data-ttu-id="bec23-128">Dans la vue de détail, je voulais visualiser les informations de chaque élément avec le texte rendu impeccable et dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="bec23-128">In detail view, I wanted to visualize the information of each element with beautifully rendered text in 3D space.</span></span> <span data-ttu-id="bec23-129">Le modèle d’électrons 3D animés s’affiche dans la zone centrale et sont consultables sous différents angles.</span><span class="sxs-lookup"><span data-stu-id="bec23-129">The animated 3D electron model is displayed in the center area and can be viewed from different angles.</span></span>

![Interaction](images/640px-periodictable-interaction.jpg)

<span data-ttu-id="bec23-131">![Prototypes](images/640px-periodictable-prototypes.jpg)</span><span class="sxs-lookup"><span data-stu-id="bec23-131">![Prototypes](images/640px-periodictable-prototypes.jpg)</span></span><br>
<span data-ttu-id="bec23-132">*Prototypes d’interaction*</span><span class="sxs-lookup"><span data-stu-id="bec23-132">*Interaction prototypes*</span></span>

<span data-ttu-id="bec23-133">L’utilisateur peut modifier le type de surface par voie aérienne en appuyant sur les boutons en bas de la table, ils peuvent basculer entre un plan, cylindre, sphère et à nuages de points.</span><span class="sxs-lookup"><span data-stu-id="bec23-133">The user can change the surface type by air tapping the buttons on the bottom of the table - they can switch between plane, cylinder, sphere and scatter.</span></span>

## <a name="common-controls-and-patterns-used-in-this-app"></a><span data-ttu-id="bec23-134">Contrôles et modèles utilisés dans cette application courants</span><span class="sxs-lookup"><span data-stu-id="bec23-134">Common controls and patterns used in this app</span></span>

### <a name="interactable-object-button"></a><span data-ttu-id="bec23-135">Objet sur (bouton)</span><span class="sxs-lookup"><span data-stu-id="bec23-135">Interactable object (button)</span></span>

<span data-ttu-id="bec23-136">[Objet sur](interactable-object.md) est un objet qui peut répondre aux entrées de base HoloLens.</span><span class="sxs-lookup"><span data-stu-id="bec23-136">[Interactable object](interactable-object.md) is an object which can respond to basic HoloLens inputs.</span></span> <span data-ttu-id="bec23-137">Il est fourni en tant que préfabriqué/script que vous pouvez facilement appliquer à n’importe quel objet.</span><span class="sxs-lookup"><span data-stu-id="bec23-137">It is provided as a prefab/script which you can easily apply to any object.</span></span> <span data-ttu-id="bec23-138">Par exemple, vous pouvez rendre une tasse de café dans votre scène sur et répondre aux entrées telles que des regards, appui, les mouvements de navigation et de manipulation.</span><span class="sxs-lookup"><span data-stu-id="bec23-138">For example, you can make a coffee cup in your scene interactable and respond to inputs such as gaze, air tap, navigation and manipulation gestures.</span></span> [<span data-ttu-id="bec23-139">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="bec23-139">Learn more</span></span>](interactable-object.md)

![objet de nteractable](images/640px-periodictable-interactableobject.jpg)

### <a name="object-collection"></a><span data-ttu-id="bec23-141">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="bec23-141">Object collection</span></span>

<span data-ttu-id="bec23-142">[Collection d’objets](object-collection.md) est un objet qui permet de disposer de plusieurs objets dans différentes formes.</span><span class="sxs-lookup"><span data-stu-id="bec23-142">[Object collection](object-collection.md) is an object which helps you lay out multiple objects in various shapes.</span></span> <span data-ttu-id="bec23-143">Il prend en charge le plan, cylindre, sphère et à nuages de points.</span><span class="sxs-lookup"><span data-stu-id="bec23-143">It supports plane, cylinder, sphere and scatter.</span></span> <span data-ttu-id="bec23-144">Vous pouvez configurer des propriétés supplémentaires telles que le rayon, le nombre de lignes et l’espacement.</span><span class="sxs-lookup"><span data-stu-id="bec23-144">You can configure additional properties such as radius, number of rows and the spacing.</span></span> [<span data-ttu-id="bec23-145">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="bec23-145">Learn more</span></span>](object-collection.md)

![Collection d’objets](images/640px-periodictable-collections.jpg)

### <a name="fitbox"></a><span data-ttu-id="bec23-147">Fitbox</span><span class="sxs-lookup"><span data-stu-id="bec23-147">Fitbox</span></span>

<span data-ttu-id="bec23-148">Par défaut, hologrammes seront placés dans l’emplacement où l’utilisateur est gazing au moment où l’application est lancée.</span><span class="sxs-lookup"><span data-stu-id="bec23-148">By default, holograms will be placed in the location where the user is gazing at the moment the application is launched.</span></span> <span data-ttu-id="bec23-149">Cela entraîne parfois des résultats indésirables tels que hologrammes placées derrière un mur ou au milieu d’une table.</span><span class="sxs-lookup"><span data-stu-id="bec23-149">This sometimes leads to unwanted result such as holograms being placed behind a wall or in the middle of a table.</span></span> <span data-ttu-id="bec23-150">Un fitbox permet à un utilisateur à utiliser des regards pour déterminer l’emplacement où l’hologramme sera placé.</span><span class="sxs-lookup"><span data-stu-id="bec23-150">A fitbox allows a user to use gaze to determine the location where the hologram will be placed.</span></span> <span data-ttu-id="bec23-151">Il est effectué avec une texture d’image PNG simple qui peut être personnalisée facilement avec vos propres images ou des objets 3D.</span><span class="sxs-lookup"><span data-stu-id="bec23-151">It is made with a simple PNG image texture which can be easily customized with your own images or 3D objects.</span></span>

![Fitbox](images/450px-periodictable-fitbox.jpg)

## <a name="technical-details"></a><span data-ttu-id="bec23-153">Détails techniques</span><span class="sxs-lookup"><span data-stu-id="bec23-153">Technical details</span></span>

<span data-ttu-id="bec23-154">Vous pouvez trouver des scripts et prefabs pour la Table périodique de l’application d’éléments sur le [GitHub de laboratoires de conception réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable).</span><span class="sxs-lookup"><span data-stu-id="bec23-154">You can find scripts and prefabs for the Periodic Table of the Elements app on the [Mixed Reality Design Labs GitHub](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable).</span></span>

## <a name="application-examples"></a><span data-ttu-id="bec23-155">Exemples d’applications</span><span class="sxs-lookup"><span data-stu-id="bec23-155">Application examples</span></span>

<span data-ttu-id="bec23-156">Voici quelques idées pour ce que vous pouvez créer en exploitant les composants dans ce projet.</span><span class="sxs-lookup"><span data-stu-id="bec23-156">Here are some ideas for what you could create by leveraging the components in this project.</span></span>

### <a name="stock-data-visualization-app"></a><span data-ttu-id="bec23-157">Application de visualisation des données boursières</span><span class="sxs-lookup"><span data-stu-id="bec23-157">Stock data visualization app</span></span>

<span data-ttu-id="bec23-158">Que la Table périodique de l’exemple d’éléments, utilisez les mêmes contrôles et le modèle d’interaction, vous pouvez générer une application qui visualise les données boursières.</span><span class="sxs-lookup"><span data-stu-id="bec23-158">Using the same controls and interaction model as the Periodic Table of the Elements sample, you could build an app which visualizes stock market data.</span></span> <span data-ttu-id="bec23-159">Cet exemple utilise le contrôle de collection d’objets pour présenter les données de stock dans une forme sphérique.</span><span class="sxs-lookup"><span data-stu-id="bec23-159">This example uses the Object collection control to lay out stock data in a spherical shape.</span></span> <span data-ttu-id="bec23-160">Vous pouvez l’imaginer une vue de détail où des informations supplémentaires sur chaque action pouvant être affichées dans une façon intéressante.</span><span class="sxs-lookup"><span data-stu-id="bec23-160">You can imagine a detail view where additional information about each stock could be displayed in an interesting way.</span></span>

![Exemple d’application : Finance (1 sur 3)](images/640px-periodictable-applicationexamples-finance1.jpg)

![Exemple d’application : Finance (2 sur 3)](images/640px-periodictable-applicationexamples-finance2.jpg)

<span data-ttu-id="bec23-163">![Exemple d’application : Finance (3 sur 3)](images/640px-periodictable-applicationexamples-finance3.jpg)</span><span class="sxs-lookup"><span data-stu-id="bec23-163">![Application example: Finance (3 of 3)](images/640px-periodictable-applicationexamples-finance3.jpg)</span></span><br>
<span data-ttu-id="bec23-164">*Un exemple d’utilisation de la collection d’objets utilisée dans la Table périodique de l’exemple d’application éléments peut être dans une application de finance*</span><span class="sxs-lookup"><span data-stu-id="bec23-164">*An example of how the Object collection used in the Periodic Table of the Elements sample app could be used in a finance app*</span></span>

### <a name="sports-app"></a><span data-ttu-id="bec23-165">Application de sport</span><span class="sxs-lookup"><span data-stu-id="bec23-165">Sports app</span></span>

<span data-ttu-id="bec23-166">Il s’agit d’un exemple de visualisation des données de sports à l’aide de la collection d’objets et d’autres composants de la Table périodique de l’exemple d’application éléments.</span><span class="sxs-lookup"><span data-stu-id="bec23-166">This is an example of visualizing sports data using Object collection and other components from the Periodic Table of the Elements sample app.</span></span>

![Exemple d’application : Sports (1 sur 3)](images/640px-periodictable-applicationexamples-sports0.jpg)

![Exemple d’application : Sports (2 sur 3)](images/640px-periodictable-applicationexamples-sports1.jpg)

<span data-ttu-id="bec23-169">![Exemple d’application : Sports (3 sur 3)](images/640px-periodictable-applicationexamples-sports3.jpg)</span><span class="sxs-lookup"><span data-stu-id="bec23-169">![Application example: Sports (3 of 3)](images/640px-periodictable-applicationexamples-sports3.jpg)</span></span><br>
<span data-ttu-id="bec23-170">*Un exemple d’utilisation de la collection d’objets dans la Table périodique de l’appcould exemple éléments être utilisé dans une application de sports*</span><span class="sxs-lookup"><span data-stu-id="bec23-170">*An example of how the Object collection used in the Periodic Table of the Elements sample appcould be used in a sports app*</span></span>

## <a name="about-the-author"></a><span data-ttu-id="bec23-171">À propos de l’auteur</span><span class="sxs-lookup"><span data-stu-id="bec23-171">About the author</span></span>

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><span data-ttu-id="bec23-172"><b>Dong Yoon Park</b></span><span class="sxs-lookup"><span data-stu-id="bec23-172"><b>Dong Yoon Park</b></span></span><br><span data-ttu-id="bec23-173">Concepteur UX @Microsoft</span><span class="sxs-lookup"><span data-stu-id="bec23-173">UX Designer @Microsoft</span></span></td>
</tr>
</table>

## <a name="see-also"></a><span data-ttu-id="bec23-174">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="bec23-174">See also</span></span>

* [<span data-ttu-id="bec23-175">Objet sur</span><span class="sxs-lookup"><span data-stu-id="bec23-175">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="bec23-176">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="bec23-176">Object collection</span></span>](object-collection.md)
