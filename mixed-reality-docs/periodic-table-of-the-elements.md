---
title: Tableau périodique des éléments
description: La table périodique des éléments est un exemple d’application open source des laboratoires de conception de la réalité mixte de Microsoft, où vous pouvez apprendre à disposer un tableau d’objets dans l’espace 3D avec différents types de surface à l’aide d’une collection d’objets.
author: cre8ivepark
ms.author: dongpark
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, exemple d’application, contrôles
ms.openlocfilehash: ad95d2bcfd1b70d805adcceb36be0c6c29b838f0
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63525367"
---
# <a name="periodic-table-of-the-elements"></a><span data-ttu-id="c2857-104">Tableau périodique des éléments</span><span class="sxs-lookup"><span data-stu-id="c2857-104">Periodic Table of the Elements</span></span>

>[!NOTE]
><span data-ttu-id="c2857-105">Cet article présente un exemple exploratoire que nous avons créé dans les [laboratoires de conception de réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity), un endroit où nous partageons nos connaissances et des suggestions concernant le développement d’applications de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="c2857-105">This article discusses an exploratory sample we’ve created in the [Mixed Reality Design Labs](https://github.com/Microsoft/MRDesignLabs_Unity), a place where we share our learnings about and suggestions for mixed reality app development.</span></span> <span data-ttu-id="c2857-106">Nos articles et code liés à la conception évoluent à mesure que nous effectuons de nouvelles découvertes.</span><span class="sxs-lookup"><span data-stu-id="c2857-106">Our design-related articles and code will evolve as we make new discoveries.</span></span>

<span data-ttu-id="c2857-107">[La table périodique des éléments](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable) est un exemple d’application open source des laboratoires de conception de la réalité mixte de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c2857-107">[Periodic Table of the Elements](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable) is a open-source sample app from Microsoft's Mixed Reality Design Labs.</span></span> <span data-ttu-id="c2857-108">Avec ce projet, vous pouvez apprendre à disposer un tableau d’objets dans l’espace 3D avec différents types de surface à l’aide d’une **[collection d’objets](object-collection.md)** .</span><span class="sxs-lookup"><span data-stu-id="c2857-108">With this project, you can learn how to lay out an array of objects in 3D space with various surface types using an **[Object collection](object-collection.md)**.</span></span> <span data-ttu-id="c2857-109">Découvrez également comment créer des objets interactifs qui répondent aux entrées standard de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="c2857-109">Also learn how to create interactable objects that respond to standard inputs from HoloLens.</span></span> <span data-ttu-id="c2857-110">Vous pouvez utiliser les composants de ce projet pour créer votre propre expérience d’application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="c2857-110">You can use this project's components to create your own mixed reality app experience.</span></span>

![Table period de l’application Elements](images/640px-periodictable-hero.jpg)

## <a name="about-the-app"></a><span data-ttu-id="c2857-112">À propos de l’application</span><span class="sxs-lookup"><span data-stu-id="c2857-112">About the app</span></span>

<span data-ttu-id="c2857-113">La table périodique des éléments visualise les éléments chimiques et chacune de leurs propriétés dans un espace 3D.</span><span class="sxs-lookup"><span data-stu-id="c2857-113">Periodic Table of the Elements visualizes the chemical elements and each of their properties in a 3D space.</span></span> <span data-ttu-id="c2857-114">Il intègre les interactions de base de HoloLens, telles que le toucher et l’air.</span><span class="sxs-lookup"><span data-stu-id="c2857-114">It incorporates the basic interactions of HoloLens such as gaze and air tap.</span></span> <span data-ttu-id="c2857-115">Les utilisateurs peuvent en savoir plus sur les éléments avec des modèles 3D animés.</span><span class="sxs-lookup"><span data-stu-id="c2857-115">Users can learn about the elements with animated 3D models.</span></span> <span data-ttu-id="c2857-116">Ils peuvent comprendre visuellement le shell électron d’un élément et son noyau, qui est composé de protons et de neutrons.</span><span class="sxs-lookup"><span data-stu-id="c2857-116">They can visually understand an element's electron shell and its nucleus - which is composed of protons and neutrons.</span></span>

## <a name="background"></a><span data-ttu-id="c2857-117">Présentation</span><span class="sxs-lookup"><span data-stu-id="c2857-117">Background</span></span>

<span data-ttu-id="c2857-118">Une fois que j’ai expérimenté le langage HoloLens, une application de table périodique était une idée que je souhaitais expérimenter en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="c2857-118">After I first experienced HoloLens, a periodic table app was an idea I knew that I wanted to experiment with in mixed reality.</span></span> <span data-ttu-id="c2857-119">Étant donné que chaque élément a de nombreux points de données qui s’affichent avec du texte, j’ai pensé qu’il serait intéressant d’explorer la composition typographique dans un espace 3D.</span><span class="sxs-lookup"><span data-stu-id="c2857-119">Since each element has many data points that are displayed with text, I thought it would be great subject matter for exploring typographic composition in a 3D space.</span></span> <span data-ttu-id="c2857-120">La possibilité de visualiser le modèle d’électrons de l’élément était une autre partie intéressante de ce projet.</span><span class="sxs-lookup"><span data-stu-id="c2857-120">Being able to visualize the element's electron model was another interesting part of this project.</span></span>

## <a name="design"></a><span data-ttu-id="c2857-121">Concevoir</span><span class="sxs-lookup"><span data-stu-id="c2857-121">Design</span></span>

<span data-ttu-id="c2857-122">Pour la vue par défaut de la table périodique, j’ai imaginé des cases tridimensionnelles qui contiennent le modèle d’électrons de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="c2857-122">For the default view of the periodic table, I imagined three-dimensional boxes that would contain the electron model of each element.</span></span> <span data-ttu-id="c2857-123">La surface de chaque zone est translucide afin que l’utilisateur puisse obtenir une idée approximative du volume de l’élément.</span><span class="sxs-lookup"><span data-stu-id="c2857-123">The surface of each box would be translucent so that the user could get a rough idea of the element's volume.</span></span> <span data-ttu-id="c2857-124">Lorsque vous appuyez sur le regard et l’air, l’utilisateur peut ouvrir une vue détaillée de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="c2857-124">With gaze and air tap, the user could open up a detailed view of each element.</span></span> <span data-ttu-id="c2857-125">Pour effectuer la transition entre la vue de table et l’affichage détaillé en douceur et en naturel, j’ai fait de la même façon que l’interaction physique d’une ouverture de Box dans la vie réelle.</span><span class="sxs-lookup"><span data-stu-id="c2857-125">To make the transition between table view and detail view smooth and natural, I made it similar to the physical interaction of a box opening in real life.</span></span>

<span data-ttu-id="c2857-126">![Concevoir l’esquisse](images/640px-sketch20170406.jpg)</span><span class="sxs-lookup"><span data-stu-id="c2857-126">![Design sketch](images/640px-sketch20170406.jpg)</span></span><br>
<span data-ttu-id="c2857-127">*Concevoir des croquis*</span><span class="sxs-lookup"><span data-stu-id="c2857-127">*Design sketches*</span></span>

<span data-ttu-id="c2857-128">En mode Détails, je voulais visualiser les informations de chaque élément avec un rendu impeccable du texte dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="c2857-128">In detail view, I wanted to visualize the information of each element with beautifully rendered text in 3D space.</span></span> <span data-ttu-id="c2857-129">Le modèle d’électrons 3D animé est affiché dans la zone centrale et peut être affiché à partir de différents angles.</span><span class="sxs-lookup"><span data-stu-id="c2857-129">The animated 3D electron model is displayed in the center area and can be viewed from different angles.</span></span>

![Interaction](images/640px-periodictable-interaction.jpg)

<span data-ttu-id="c2857-131">![Prototypes](images/640px-periodictable-prototypes.jpg)</span><span class="sxs-lookup"><span data-stu-id="c2857-131">![Prototypes](images/640px-periodictable-prototypes.jpg)</span></span><br>
<span data-ttu-id="c2857-132">*Prototypes d’interaction*</span><span class="sxs-lookup"><span data-stu-id="c2857-132">*Interaction prototypes*</span></span>

<span data-ttu-id="c2857-133">L’utilisateur peut modifier le type de surface par air en appuyant sur les boutons situés en bas du tableau: il peut basculer entre le plan, le cylindre, la sphère et le nuage de points.</span><span class="sxs-lookup"><span data-stu-id="c2857-133">The user can change the surface type by air tapping the buttons on the bottom of the table - they can switch between plane, cylinder, sphere and scatter.</span></span>

## <a name="common-controls-and-patterns-used-in-this-app"></a><span data-ttu-id="c2857-134">Contrôles et modèles communs utilisés dans cette application</span><span class="sxs-lookup"><span data-stu-id="c2857-134">Common controls and patterns used in this app</span></span>

### <a name="interactable-object-button"></a><span data-ttu-id="c2857-135">Objet interagiable (bouton)</span><span class="sxs-lookup"><span data-stu-id="c2857-135">Interactable object (button)</span></span>

<span data-ttu-id="c2857-136">L’objet pouvant être [interagi](interactable-object.md) est un objet qui peut répondre aux entrées HoloLens de base.</span><span class="sxs-lookup"><span data-stu-id="c2857-136">[Interactable object](interactable-object.md) is an object which can respond to basic HoloLens inputs.</span></span> <span data-ttu-id="c2857-137">Il est fourni en tant que Prefab/script que vous pouvez facilement appliquer à n’importe quel objet.</span><span class="sxs-lookup"><span data-stu-id="c2857-137">It is provided as a prefab/script which you can easily apply to any object.</span></span> <span data-ttu-id="c2857-138">Par exemple, vous pouvez faire en sorte qu’une tasse de café dans votre scène puisse être manipulée et répondre à des entrées telles que le pointage, le toucher en air, les mouvements de navigation et de manipulation.</span><span class="sxs-lookup"><span data-stu-id="c2857-138">For example, you can make a coffee cup in your scene interactable and respond to inputs such as gaze, air tap, navigation and manipulation gestures.</span></span> [<span data-ttu-id="c2857-139">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="c2857-139">Learn more</span></span>](interactable-object.md)

![objet nteractable](images/640px-periodictable-interactableobject.jpg)

### <a name="object-collection"></a><span data-ttu-id="c2857-141">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="c2857-141">Object collection</span></span>

<span data-ttu-id="c2857-142">La [collection d’objets](object-collection.md) est un objet qui vous permet de disposer plusieurs objets dans différentes formes.</span><span class="sxs-lookup"><span data-stu-id="c2857-142">[Object collection](object-collection.md) is an object which helps you lay out multiple objects in various shapes.</span></span> <span data-ttu-id="c2857-143">Il prend en charge les plans, les cylindres, les sphères et les nuages de points.</span><span class="sxs-lookup"><span data-stu-id="c2857-143">It supports plane, cylinder, sphere and scatter.</span></span> <span data-ttu-id="c2857-144">Vous pouvez configurer des propriétés supplémentaires telles que le rayon, le nombre de lignes et l’espacement.</span><span class="sxs-lookup"><span data-stu-id="c2857-144">You can configure additional properties such as radius, number of rows and the spacing.</span></span> [<span data-ttu-id="c2857-145">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="c2857-145">Learn more</span></span>](object-collection.md)

![Collection d’objets](images/640px-periodictable-collections.jpg)

### <a name="fitbox"></a><span data-ttu-id="c2857-147">Fitbox</span><span class="sxs-lookup"><span data-stu-id="c2857-147">Fitbox</span></span>

<span data-ttu-id="c2857-148">Par défaut, les hologrammes sont placés à l’emplacement où l’utilisateur est Gazing au moment où l’application est lancée.</span><span class="sxs-lookup"><span data-stu-id="c2857-148">By default, holograms will be placed in the location where the user is gazing at the moment the application is launched.</span></span> <span data-ttu-id="c2857-149">Cela entraîne parfois des résultats indésirables, tels que des hologrammes placés derrière un mur ou au milieu d’une table.</span><span class="sxs-lookup"><span data-stu-id="c2857-149">This sometimes leads to unwanted result such as holograms being placed behind a wall or in the middle of a table.</span></span> <span data-ttu-id="c2857-150">Un fitbox permet à un utilisateur d’utiliser du regard pour déterminer l’emplacement où l’hologramme sera placé.</span><span class="sxs-lookup"><span data-stu-id="c2857-150">A fitbox allows a user to use gaze to determine the location where the hologram will be placed.</span></span> <span data-ttu-id="c2857-151">Il est créé avec une texture d’image PNG simple qui peut être facilement personnalisée avec vos propres images ou objets 3D.</span><span class="sxs-lookup"><span data-stu-id="c2857-151">It is made with a simple PNG image texture which can be easily customized with your own images or 3D objects.</span></span>

![Fitbox](images/450px-periodictable-fitbox.jpg)

## <a name="technical-details"></a><span data-ttu-id="c2857-153">Détails techniques</span><span class="sxs-lookup"><span data-stu-id="c2857-153">Technical details</span></span>

<span data-ttu-id="c2857-154">Vous trouverez scripts and prefabs pour la table Periodic de l’application Elements sur le GitHub de conception de la [réalité mixte](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable).</span><span class="sxs-lookup"><span data-stu-id="c2857-154">You can find scripts and prefabs for the Periodic Table of the Elements app on the [Mixed Reality Design Labs GitHub](https://github.com/Microsoft/MRDesignLabs_Unity_PeriodicTable).</span></span>

## <a name="application-examples"></a><span data-ttu-id="c2857-155">Exemples d’applications</span><span class="sxs-lookup"><span data-stu-id="c2857-155">Application examples</span></span>

<span data-ttu-id="c2857-156">Voici quelques idées de ce que vous pouvez créer en tirant parti des composants de ce projet.</span><span class="sxs-lookup"><span data-stu-id="c2857-156">Here are some ideas for what you could create by leveraging the components in this project.</span></span>

### <a name="stock-data-visualization-app"></a><span data-ttu-id="c2857-157">Application de visualisation des données boursières</span><span class="sxs-lookup"><span data-stu-id="c2857-157">Stock data visualization app</span></span>

<span data-ttu-id="c2857-158">En utilisant les mêmes contrôles et le même modèle d’interaction que la table périodique de l’exemple d’éléments, vous pouvez créer une application qui visualise les données boursières.</span><span class="sxs-lookup"><span data-stu-id="c2857-158">Using the same controls and interaction model as the Periodic Table of the Elements sample, you could build an app which visualizes stock market data.</span></span> <span data-ttu-id="c2857-159">Cet exemple utilise le contrôle de collection d’objets pour présenter les données boursières dans une forme sphérique.</span><span class="sxs-lookup"><span data-stu-id="c2857-159">This example uses the Object collection control to lay out stock data in a spherical shape.</span></span> <span data-ttu-id="c2857-160">Vous pouvez imaginer un affichage détaillé où des informations supplémentaires sur chaque stock peuvent être affichées d’une manière intéressante.</span><span class="sxs-lookup"><span data-stu-id="c2857-160">You can imagine a detail view where additional information about each stock could be displayed in an interesting way.</span></span>

![Exemple d’application: Finance (1 sur 3)](images/640px-periodictable-applicationexamples-finance1.jpg)

![Exemple d’application: Finance (2 sur 3)](images/640px-periodictable-applicationexamples-finance2.jpg)

<span data-ttu-id="c2857-163">![Exemple d’application: Finance (3 sur 3)](images/640px-periodictable-applicationexamples-finance3.jpg)</span><span class="sxs-lookup"><span data-stu-id="c2857-163">![Application example: Finance (3 of 3)](images/640px-periodictable-applicationexamples-finance3.jpg)</span></span><br>
<span data-ttu-id="c2857-164">*Exemple de la façon dont la collection d’objets utilisée dans la table périodique de l’exemple d’application Elements peut être utilisée dans une application finance*</span><span class="sxs-lookup"><span data-stu-id="c2857-164">*An example of how the Object collection used in the Periodic Table of the Elements sample app could be used in a finance app*</span></span>

### <a name="sports-app"></a><span data-ttu-id="c2857-165">Application sportive</span><span class="sxs-lookup"><span data-stu-id="c2857-165">Sports app</span></span>

<span data-ttu-id="c2857-166">Voici un exemple de visualisation de données sportives à l’aide de la collection d’objets et d’autres composants de la table périodique de l’exemple d’application d’éléments.</span><span class="sxs-lookup"><span data-stu-id="c2857-166">This is an example of visualizing sports data using Object collection and other components from the Periodic Table of the Elements sample app.</span></span>

![Exemple d’application: Sports (1 sur 3)](images/640px-periodictable-applicationexamples-sports0.jpg)

![Exemple d’application: Sports (2 sur 3)](images/640px-periodictable-applicationexamples-sports1.jpg)

<span data-ttu-id="c2857-169">![Exemple d’application: Sports (3 sur 3)](images/640px-periodictable-applicationexamples-sports3.jpg)</span><span class="sxs-lookup"><span data-stu-id="c2857-169">![Application example: Sports (3 of 3)](images/640px-periodictable-applicationexamples-sports3.jpg)</span></span><br>
<span data-ttu-id="c2857-170">*Exemple de la façon dont la collection d’objets utilisée dans la table périodique de l’exemple d’éléments appcould doit être utilisée dans une application sportive*</span><span class="sxs-lookup"><span data-stu-id="c2857-170">*An example of how the Object collection used in the Periodic Table of the Elements sample appcould be used in a sports app*</span></span>

## <a name="about-the-author"></a><span data-ttu-id="c2857-171">À propos de l’auteur</span><span class="sxs-lookup"><span data-stu-id="c2857-171">About the author</span></span>

<table style="border-collapse:collapse" padding-left="0px">
<tr>
<td style="border-style: none" width="60px"><img alt="Picture of Dong Yoon Park" width="60" height="60" src="images/dongyoonpark.jpg"></td>
<td style="border-style: none"><span data-ttu-id="c2857-172"><b>Dong Yoon Park</b></span><span class="sxs-lookup"><span data-stu-id="c2857-172"><b>Dong Yoon Park</b></span></span><br><span data-ttu-id="c2857-173">Concepteur UX@Microsoft</span><span class="sxs-lookup"><span data-stu-id="c2857-173">UX Designer @Microsoft</span></span></td>
</tr>
</table>

## <a name="see-also"></a><span data-ttu-id="c2857-174">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c2857-174">See also</span></span>

* [<span data-ttu-id="c2857-175">Objet avec interaction possible</span><span class="sxs-lookup"><span data-stu-id="c2857-175">Interactable object</span></span>](interactable-object.md)
* [<span data-ttu-id="c2857-176">Collection d’objets</span><span class="sxs-lookup"><span data-stu-id="c2857-176">Object collection</span></span>](object-collection.md)
