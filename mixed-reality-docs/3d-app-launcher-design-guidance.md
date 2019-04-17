---
title: Guide de conception du Lanceur d’application 3D
description: Un lanceur d’applications 3D est un objet « physique » dans la maison de réalité mixte de l’utilisateur qu’ils peuvent sélectionner pour lancer une application.
author: thmignon
ms.author: thmignon
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, conception, de lanceur d’applications 3D immersif casque, live cube
ms.openlocfilehash: 47db5bffa121c0cc11d246dc749c464e5f187270
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593646"
---
# <a name="3d-app-launcher-design-guidance"></a><span data-ttu-id="99cd4-104">Guide de conception du Lanceur d’application 3D</span><span class="sxs-lookup"><span data-stu-id="99cd4-104">3D app launcher design guidance</span></span>

<span data-ttu-id="99cd4-105">Quand vous placez sur un casque (VR) immersif de Windows Mixed Reality, vous entrez Windows Mixed Reality domestique, affichée sous la forme d’une maison sur une falaise entouré d’eau et Montagnes (bien que vous puissiez [choisissez autres environnements et même créer vos propres](add-custom-home-environments.md)).</span><span class="sxs-lookup"><span data-stu-id="99cd4-105">When you put on a Windows Mixed Reality immersive (VR) headset, you enter the Windows Mixed Reality home, visualized as a house on a cliff surrounded by mountains and water (though you can [choose other environments and even create your own](add-custom-home-environments.md)).</span></span> <span data-ttu-id="99cd4-106">Dans l’espace de cette maison, un utilisateur est libre de réorganiser les objets 3D et les applications qui les intéressent tout comme ils le souhaitent.</span><span class="sxs-lookup"><span data-stu-id="99cd4-106">Within the space of this home, a user is free to arrange and organize the 3D objects and apps that they care about any way they want.</span></span> <span data-ttu-id="99cd4-107">Un **Lanceur d’applications 3D** est un objet « physique » dans l’utilisateur mixte de maison réalité qu’ils peuvent sélectionner pour lancer une application.</span><span class="sxs-lookup"><span data-stu-id="99cd4-107">A **3D app launcher** is a “physical” object in the user’s mixed reality house that they can select to launch an app.</span></span>

<span data-ttu-id="99cd4-108">![Exemple : Lanceur d’applications 3D Bird flottante](images/20171016-151526-mixedreality1-1200px-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="99cd4-108">![Example: Floaty Bird 3D app launcher](images/20171016-151526-mixedreality1-1200px-1000px.jpg)</span></span><br>
<span data-ttu-id="99cd4-109">*Exemple de lanceur flottante application 3D d’imagerie Bird ' s (application fictive)*</span><span class="sxs-lookup"><span data-stu-id="99cd4-109">*Floaty Bird 3D app launcher example (fictional app)*</span></span>

## <a name="3d-app-launcher-creation-process"></a><span data-ttu-id="99cd4-110">Processus de création de lanceur application 3D</span><span class="sxs-lookup"><span data-stu-id="99cd4-110">3D app launcher creation process</span></span>

<span data-ttu-id="99cd4-111">Il existe 3 étapes à la création d’un lanceur d’applications 3D :</span><span class="sxs-lookup"><span data-stu-id="99cd4-111">There are 3 steps to creating a 3D app launcher:</span></span>
1. <span data-ttu-id="99cd4-112">Conception et concepting (cet article)</span><span class="sxs-lookup"><span data-stu-id="99cd4-112">Designing and concepting (this article)</span></span>
2. [<span data-ttu-id="99cd4-113">Modélisation et l’exportation</span><span class="sxs-lookup"><span data-stu-id="99cd4-113">Modeling and exporting</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
3. <span data-ttu-id="99cd4-114">Intégration dans votre application :</span><span class="sxs-lookup"><span data-stu-id="99cd4-114">Integrating it into your application:</span></span>
    * [<span data-ttu-id="99cd4-115">Applications UWP</span><span class="sxs-lookup"><span data-stu-id="99cd4-115">UWP apps</span></span>](implementing-3d-app-launchers.md)
    * [<span data-ttu-id="99cd4-116">Applications Win32</span><span class="sxs-lookup"><span data-stu-id="99cd4-116">Win32 apps</span></span>](implementing-3d-app-launchers-win32.md)

## <a name="design-concepts"></a><span data-ttu-id="99cd4-117">Principes de conception</span><span class="sxs-lookup"><span data-stu-id="99cd4-117">Design concepts</span></span>

### <a name="fantastic-yet-familiar"></a><span data-ttu-id="99cd4-118">Tout simplement fantastique encore familier</span><span class="sxs-lookup"><span data-stu-id="99cd4-118">Fantastic yet familiar</span></span>

<span data-ttu-id="99cd4-119">L’environnement Windows Mixed Reality dans que Lanceur d’applications se trouve est partie familière, partie fantastiques/sci-fi.</span><span class="sxs-lookup"><span data-stu-id="99cd4-119">The Windows Mixed Reality environment your app launcher lives in is part familiar, part fantastical/sci-fi.</span></span> <span data-ttu-id="99cd4-120">Les lanceurs meilleures suivent les règles de ce monde.</span><span class="sxs-lookup"><span data-stu-id="99cd4-120">The best launchers follow the rules of this world.</span></span> <span data-ttu-id="99cd4-121">Imaginez comment vous pouvez prendre un objet familière et représentatif de votre application, mais certaines des règles de réalité réelle de pliage.</span><span class="sxs-lookup"><span data-stu-id="99cd4-121">Think of how you can take a familiar, representative object from your app, but bend some of the rules of actual reality.</span></span> <span data-ttu-id="99cd4-122">Magic entraîne.</span><span class="sxs-lookup"><span data-stu-id="99cd4-122">Magic will result.</span></span>

### <a name="intuitive"></a><span data-ttu-id="99cd4-123">Intuitive</span><span class="sxs-lookup"><span data-stu-id="99cd4-123">Intuitive</span></span>

<span data-ttu-id="99cd4-124">Lorsque vous examinez le Lanceur d’applications, son objectif - pour lancer votre application - devrait être évident et ne devrait pas causer de toute confusion.</span><span class="sxs-lookup"><span data-stu-id="99cd4-124">When you look at your app launcher, its purpose - to launch your app - should be obvious and shouldn’t cause any confusion.</span></span> <span data-ttu-id="99cd4-125">Par exemple, n’oubliez pas que votre Lanceur est un évident suffisamment représentative de votre application qu’elle ne sont pas confondue pour un élément de décor dans le Cliff House.</span><span class="sxs-lookup"><span data-stu-id="99cd4-125">For example, be sure your launcher is an obvious-enough representative of your app that it won’t be confused for a piece of decor in the Cliff House.</span></span> <span data-ttu-id="99cd4-126">Lanceur d’applications doit inviter des personnes à tactile/sélectionner il.</span><span class="sxs-lookup"><span data-stu-id="99cd4-126">Your app launcher should invite people to touch/select it.</span></span>

<span data-ttu-id="99cd4-127">![Exemple : Lanceur d’applications 3D Remarque fraîche](images/20171016-152145-mixedreality1-1200px-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="99cd4-127">![Example: Fresh Note 3D app launcher](images/20171016-152145-mixedreality1-1200px-1000px.jpg)</span></span><br>
<span data-ttu-id="99cd4-128">*Exemple de Lanceur d’application 3D Remarque fraîche (application fictive)*</span><span class="sxs-lookup"><span data-stu-id="99cd4-128">*Fresh Note 3D app launcher example (fictional app)*</span></span>

### <a name="home-scale"></a><span data-ttu-id="99cd4-129">Accueil mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="99cd4-129">Home scale</span></span>

<span data-ttu-id="99cd4-130">Lanceurs d’applications 3D live dans le Cliff House et leur taille par défaut vous semblera logique avec les autres objets « physiques » dans l’espace.</span><span class="sxs-lookup"><span data-stu-id="99cd4-130">3D app launchers live in the Cliff House and their default size should make sense with the other “physical” objects in the space.</span></span> <span data-ttu-id="99cd4-131">Si vous placez votre Lanceur beside, par exemple, une usine de la maison ou certains meubles, cela vous à la maison, size-wise.</span><span class="sxs-lookup"><span data-stu-id="99cd4-131">If you place your launcher beside, say, a house plant or some furniture, it should feel at home, size-wise.</span></span> <span data-ttu-id="99cd4-132">Un bon point de départ consiste à voir à quoi il ressemble à 30 centimètres cubes, mais n’oubliez pas que les utilisateurs mettre à l’échelle vers le haut ou vers le bas s’ils le souhaitent.</span><span class="sxs-lookup"><span data-stu-id="99cd4-132">A good starting point is to see how it looks at 30 cubic centimeters, but remember that users can scale it up or down if they like.</span></span>

### <a name="own-able"></a><span data-ttu-id="99cd4-133">Peut être propriétaire</span><span class="sxs-lookup"><span data-stu-id="99cd4-133">Own-able</span></span>

<span data-ttu-id="99cd4-134">Le Lanceur d’applications doit sembler un objet, une personne serait ravie d’accueillir dans leur espace.</span><span class="sxs-lookup"><span data-stu-id="99cd4-134">The app launcher should feel like an object a person would be excited to have in their space.</span></span> <span data-ttu-id="99cd4-135">Ils amèneront être pratiquement entourant eux-mêmes avec ces éléments, donc le Lanceur doit s’apparentent à quelque chose l’idée de l’utilisateur a été suffisamment souhaitable pour débusquer et conserver à proximité.</span><span class="sxs-lookup"><span data-stu-id="99cd4-135">They’ll be virtually surrounding themselves with these things, so the launcher should feel like something the user thought was desirable enough to seek out and keep nearby.</span></span>

<span data-ttu-id="99cd4-136">![Exemple : Lanceur d’applications 3D de astro Warp](images/20171016-132936-mixedreality-1200px-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="99cd4-136">![Example: Astro Warp 3D app launcher](images/20171016-132936-mixedreality-1200px-1000px.jpg)</span></span><br>
<span data-ttu-id="99cd4-137">*Exemple de lanceur d’application 3D astro Warp (application fictive)*</span><span class="sxs-lookup"><span data-stu-id="99cd4-137">*Astro Warp 3D app launcher example (fictional app)*</span></span>

### <a name="recognizable"></a><span data-ttu-id="99cd4-138">Reconnaissable</span><span class="sxs-lookup"><span data-stu-id="99cd4-138">Recognizable</span></span>

<span data-ttu-id="99cd4-139">Le Lanceur d’applications 3D doit instantanément express « marque de votre application » aux personnes il.</span><span class="sxs-lookup"><span data-stu-id="99cd4-139">Your 3D app launcher should instantly express “your app’s brand” to people who see it.</span></span> <span data-ttu-id="99cd4-140">Si vous avez un caractère en étoile ou un objet en particulier identifiable dans votre application, nous vous recommandons de l’utiliser comme une grande partie de votre conception.</span><span class="sxs-lookup"><span data-stu-id="99cd4-140">If you have a star character or an especially identifiable object in your app, we recommend using that as a big part of your design.</span></span> <span data-ttu-id="99cd4-141">Dans un monde de réalité mixte, un objet sera susciter l’intérêt du plus à partir d’utilisateurs que simplement un logo autonome.</span><span class="sxs-lookup"><span data-stu-id="99cd4-141">In a mixed reality world, an object will draw more interest from users than just a logo alone.</span></span> <span data-ttu-id="99cd4-142">Objets reconnaissables communiquent marque rapidement et de manière claire.</span><span class="sxs-lookup"><span data-stu-id="99cd4-142">Recognizable objects communicate brand quickly and clearly.</span></span>

### <a name="volumetric"></a><span data-ttu-id="99cd4-143">Volumétriques</span><span class="sxs-lookup"><span data-stu-id="99cd4-143">Volumetric</span></span>

<span data-ttu-id="99cd4-144">Votre application mérite plus que placer votre logo sur un plan plat et appel de journée.</span><span class="sxs-lookup"><span data-stu-id="99cd4-144">Your app deserves more than just putting your logo on a flat plane and calling it a day.</span></span> <span data-ttu-id="99cd4-145">Votre Lanceur devriez vous sentir comme un objet physique, 3D et intéressant dans l’espace de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="99cd4-145">Your launcher should feel like an exciting, 3D, physical object in the user’s space.</span></span> <span data-ttu-id="99cd4-146">Une bonne approche est d’imaginer que votre application s’apprêtait à avoir une info-bulle dans jour de Thanksgiving YCbCr de le Macy.</span><span class="sxs-lookup"><span data-stu-id="99cd4-146">A good approach is to imagine your app was going to have a balloon in the Macy’s Thanksgiving Day Parade.</span></span> <span data-ttu-id="99cd4-147">Posez-vous, ce qui serait vraiment épater personnes tel qu’indiqué dans la rue ?</span><span class="sxs-lookup"><span data-stu-id="99cd4-147">Ask yourself, what would really wow people as it came down the street?</span></span> <span data-ttu-id="99cd4-148">Ce qui aurait l’aspect souhaité à partir de tous les angles d’affichage ?</span><span class="sxs-lookup"><span data-stu-id="99cd4-148">What would look great from all viewing angles?</span></span>


:::row:::
    :::column:::
        ![Logo only](images/20171016-140436-mixedreality-640px.jpg)
        *Logo only*
    :::column-end:::
    :::column:::
        ![More recognizable with a character](images/20171016-140557-mixedreality-640px.jpg)
        *More recognizable with a character*
    :::column-end:::
:::row-end:::


:::row:::
    :::column:::
        ![Flat approach, not surprisingly, feels flat](images/20171016-155101-mixedreality-640px.jpg)
        *Flat approach, not surprisingly, feels flat*
    :::column-end:::
    :::column:::
        ![Volumetric approach better showcases your app](images/20171016-161407-mixedreality-640px.jpg)
        *Volumetric approach better showcases your app*
    :::column-end:::
:::row-end:::


## <a name="tips-for-good-3d-models"></a><span data-ttu-id="99cd4-149">Conseils pour les bons modèles 3D</span><span class="sxs-lookup"><span data-stu-id="99cd4-149">Tips for good 3D models</span></span>

### <a name="best-practices"></a><span data-ttu-id="99cd4-150">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="99cd4-150">Best practices</span></span>
* <span data-ttu-id="99cd4-151">Lorsque vous planifiez des dimensions du Lanceur de votre application, viser à peu près d’un cube de 30 centimètres.</span><span class="sxs-lookup"><span data-stu-id="99cd4-151">When planning dimensions for your app launcher, shoot for roughly a 30cm cube.</span></span> <span data-ttu-id="99cd4-152">Par conséquent, 1 : rapport de taille de 1:1.</span><span class="sxs-lookup"><span data-stu-id="99cd4-152">So, a 1:1:1 size ratio.</span></span>
* <span data-ttu-id="99cd4-153">Modèles doivent être des polygones moins de 10 000.</span><span class="sxs-lookup"><span data-stu-id="99cd4-153">Models must be under 10,000 polygons.</span></span> [<span data-ttu-id="99cd4-154">En savoir plus sur les nombres de triangle et les niveaux de détails (degrés)</span><span class="sxs-lookup"><span data-stu-id="99cd4-154">Learn more about triangle counts and levels of details (LODs)</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#triangle-counts-and-levels-of-detail-lods)
* <span data-ttu-id="99cd4-155">Tester sur un casque immersif lorsque cela est possible.</span><span class="sxs-lookup"><span data-stu-id="99cd4-155">Test on an immersive headset when possible.</span></span>
* <span data-ttu-id="99cd4-156">Détails de la build dans la géométrie de votre modèle lorsque cela est possible, ne vous fiez textures pour les détails.</span><span class="sxs-lookup"><span data-stu-id="99cd4-156">Build details into your model’s geometry where possible – don’t rely on textures for detail.</span></span>
* <span data-ttu-id="99cd4-157">Construire une géométrie de « eau étroite » fermé.</span><span class="sxs-lookup"><span data-stu-id="99cd4-157">Build “water tight” closed geometry.</span></span> <span data-ttu-id="99cd4-158">Aucune faille qui n’est pas modélisés.</span><span class="sxs-lookup"><span data-stu-id="99cd4-158">No holes that are not modeled in.</span></span>
* <span data-ttu-id="99cd4-159">Utiliser des matériaux naturelles dans votre objet.</span><span class="sxs-lookup"><span data-stu-id="99cd4-159">Use natural materials in your object.</span></span> <span data-ttu-id="99cd4-160">Imaginez qu’il créant dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="99cd4-160">Imagine crafting it in the real world.</span></span>
* <span data-ttu-id="99cd4-161">Assurez-vous que votre modèle lit bien avec les dimensions et les distances différents.</span><span class="sxs-lookup"><span data-stu-id="99cd4-161">Make sure your model reads well at different distances and sizes.</span></span>
* <span data-ttu-id="99cd4-162">Lorsque votre modèle est prêt à commencer, lisez le [exportation des indications de ressources](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#asset-requirements-overview).</span><span class="sxs-lookup"><span data-stu-id="99cd4-162">When your model is ready to go, read the [exporting assets guidelines](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#asset-requirements-overview).</span></span>

<span data-ttu-id="99cd4-163">![Modèle avec des détails subtils dans la texture](images/20171013-143334-mixedreality-640px.jpg)</span><span class="sxs-lookup"><span data-stu-id="99cd4-163">![Model with subtle details in the texture](images/20171013-143334-mixedreality-640px.jpg)</span></span><br>
<span data-ttu-id="99cd4-164">*Modèle avec des détails subtils dans la texture*</span><span class="sxs-lookup"><span data-stu-id="99cd4-164">*Model with subtle details in the texture*</span></span>

### <a name="what-to-avoid"></a><span data-ttu-id="99cd4-165">Pratiques à éviter</span><span class="sxs-lookup"><span data-stu-id="99cd4-165">What to avoid</span></span>
* <span data-ttu-id="99cd4-166">N’utilisez pas les détails de contraste élevé ou modèles de petite taille, occupés et des textures.</span><span class="sxs-lookup"><span data-stu-id="99cd4-166">Don't use high-contrast details or small, busy patterns and textures.</span></span>
* <span data-ttu-id="99cd4-167">N’utilisez pas geometry mince : il ne fonctionne bien à distance et sera alias mal.</span><span class="sxs-lookup"><span data-stu-id="99cd4-167">Don't use thin geometry – it doesn’t work well at a distance and will alias badly.</span></span>
* <span data-ttu-id="99cd4-168">Ne laissez pas les parties de votre modèle étendre trop au-delà de 1 : rapport de taille de 1:1.</span><span class="sxs-lookup"><span data-stu-id="99cd4-168">Don't let parts of your model extend too much beyond the 1:1:1 size ratio.</span></span> <span data-ttu-id="99cd4-169">Il crée des problèmes de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="99cd4-169">It will create scaling problems.</span></span>

<span data-ttu-id="99cd4-170">![Éviter le contraste élevé, de petits modèles occupés](images/20171013-143603-mixedreality-640px.jpg)</span><span class="sxs-lookup"><span data-stu-id="99cd4-170">![Avoid high-contrast, small busy patterns](images/20171013-143603-mixedreality-640px.jpg)</span></span><br>
<span data-ttu-id="99cd4-171">*Éviter les modèles de contraste élevé, petite, occupés*</span><span class="sxs-lookup"><span data-stu-id="99cd4-171">*Avoid high-contrast, small, busy patterns*</span></span>

## <a name="how-to-handle-type"></a><span data-ttu-id="99cd4-172">Comment gérer le type</span><span class="sxs-lookup"><span data-stu-id="99cd4-172">How to handle type</span></span>

### <a name="best-practices"></a><span data-ttu-id="99cd4-173">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="99cd4-173">Best practices</span></span>
* <span data-ttu-id="99cd4-174">Nous vous recommandons de que votre type se compose d’environ 1/3 du Lanceur d’applications (ou plus).</span><span class="sxs-lookup"><span data-stu-id="99cd4-174">We recommend your type comprises about 1/3 of your app launcher (or more).</span></span> <span data-ttu-id="99cd4-175">Le type est la principale chose qui fournit aux personnes une idée votre Lanceur est, en fait, un lanceur afin qu’il est intéressant si elle est assez importante.</span><span class="sxs-lookup"><span data-stu-id="99cd4-175">Type is the main thing that gives people an idea that your launcher is, in fact, a launcher so it’s nice if it’s pretty substantial.</span></span>
* <span data-ttu-id="99cd4-176">Évitez de faire très large de type – essayez de conserver dans les limites des lanceurs d’applications des dimensions de base (plus ou moins).</span><span class="sxs-lookup"><span data-stu-id="99cd4-176">Avoid making type super wide – try to keep it within the confines of the app launchers core dimensions (more or less).</span></span>
* <span data-ttu-id="99cd4-177">Type plat, vous pouvez travailler, mais n’oubliez pas qu’il peut être difficile à afficher à partir de certains angles et dans certains environnements.</span><span class="sxs-lookup"><span data-stu-id="99cd4-177">Flat type can work, but be aware that it can be hard to view from certain angles and in certain environments.</span></span> <span data-ttu-id="99cd4-178">Vous pouvez envisager de placer un objet solid ou l’arrière-plan derrière lui pour aider à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="99cd4-178">You might consider putting it a solid object or backdrop behind it to help with this.</span></span>
* <span data-ttu-id="99cd4-179">Ajout de dimension à votre type semble intéressante en 3D.</span><span class="sxs-lookup"><span data-stu-id="99cd4-179">Adding dimension to your type feels nice in 3D.</span></span> <span data-ttu-id="99cd4-180">Les côtés du type d’ombrage une couleur différente, plus sombre peut faciliter la lisibilité.</span><span class="sxs-lookup"><span data-stu-id="99cd4-180">Shading the sides of the type a different, darker color can help with readability.</span></span>


:::row:::
    :::column:::
        ![Flat type without a backdrop can be hard to view from certain angles and in certain environments](images/flattype-640px.png)
        *Flat type without a backdrop can be hard to view from certain angles and in certain environments*
    :::column-end:::
    :::column:::
        ![Type with a built-in backdrop can work well](images/flattypeandbkg-640px.png)
        *Type with a built-in backdrop can work well*
    :::column-end:::
    :::column:::
        ![Extruded type can work well if you shade the sides](images/20171016-160221-mixedreality-640px.jpg)
        *Extruded type can work well if you shade the sides*
    :::column-end:::
:::row-end:::


<span data-ttu-id="99cd4-181">**Couleurs de type qui fonctionnent**</span><span class="sxs-lookup"><span data-stu-id="99cd4-181">**Type colors that work**</span></span>
* <span data-ttu-id="99cd4-182">Blanc</span><span class="sxs-lookup"><span data-stu-id="99cd4-182">White</span></span>
* <span data-ttu-id="99cd4-183">Noir</span><span class="sxs-lookup"><span data-stu-id="99cd4-183">Black</span></span>
* <span data-ttu-id="99cd4-184">Vif semi-structurées saturée</span><span class="sxs-lookup"><span data-stu-id="99cd4-184">Bright semi-saturated color</span></span>

<span data-ttu-id="99cd4-185">![Type des couleurs qui fonctionnent.](images/20171016-112111-mixedreality-640px.jpg)</span><span class="sxs-lookup"><span data-stu-id="99cd4-185">![Type colors that work.](images/20171016-112111-mixedreality-640px.jpg)</span></span><br>
<span data-ttu-id="99cd4-186">*Couleurs de type qui fonctionnent*</span><span class="sxs-lookup"><span data-stu-id="99cd4-186">*Type colors that work*</span></span>

### <a name="what-to-avoid"></a><span data-ttu-id="99cd4-187">Pratiques à éviter</span><span class="sxs-lookup"><span data-stu-id="99cd4-187">What to avoid</span></span>

<span data-ttu-id="99cd4-188">**Couleurs de type qui entraînent des problèmes**</span><span class="sxs-lookup"><span data-stu-id="99cd4-188">**Type colors that cause trouble**</span></span>
* <span data-ttu-id="99cd4-189">Demi-teintes</span><span class="sxs-lookup"><span data-stu-id="99cd4-189">Mid-tones</span></span>
* <span data-ttu-id="99cd4-190">Gris</span><span class="sxs-lookup"><span data-stu-id="99cd4-190">Gray</span></span>
* <span data-ttu-id="99cd4-191">Excessif saturation des couleurs ou couleurs désaturées</span><span class="sxs-lookup"><span data-stu-id="99cd4-191">Over-saturated colors or desaturated colors</span></span>

<span data-ttu-id="99cd4-192">![Type des couleurs qui entraînent des problèmes.](images/20171016-112246-mixedreality-640px.jpg)</span><span class="sxs-lookup"><span data-stu-id="99cd4-192">![Type colors that cause trouble.](images/20171016-112246-mixedreality-640px.jpg)</span></span><br>
<span data-ttu-id="99cd4-193">*Couleurs de type qui entraînent des problèmes*</span><span class="sxs-lookup"><span data-stu-id="99cd4-193">*Type colors that cause trouble*</span></span>

## <a name="lighting"></a><span data-ttu-id="99cd4-194">Éclairage</span><span class="sxs-lookup"><span data-stu-id="99cd4-194">Lighting</span></span>

<span data-ttu-id="99cd4-195">L’éclairage du Lanceur de votre application provient de l’environnement Cliff House.</span><span class="sxs-lookup"><span data-stu-id="99cd4-195">The lighting for your app launcher comes from the Cliff House environment.</span></span> <span data-ttu-id="99cd4-196">Veillez à tester votre Lanceur à plusieurs endroits de la maison afin qu’il vous semble correct dans la lumière et les ombres.</span><span class="sxs-lookup"><span data-stu-id="99cd4-196">Be sure to test your launcher in several places throughout the house so it looks good in both light and shadows.</span></span> <span data-ttu-id="99cd4-197">La bonne nouvelle, c’est, si vous avez suivi les conseils de conception dans ce document, votre Lanceur doit être assez bien établies pour la plupart des éclairage dans la Cliff House.</span><span class="sxs-lookup"><span data-stu-id="99cd4-197">The good news is, if you’ve followed the other design guidance in this document, your launcher should be in pretty good shape for most lighting in the Cliff House.</span></span>

<span data-ttu-id="99cd4-198">Bon pour tester la manière dont votre Lanceur apparence dans les différents voyants dans l’environnement est le Studio, la salle de média, n’importe où à l’extérieur et dans le Patio précédent (la zone concrète avec la pelouse).</span><span class="sxs-lookup"><span data-stu-id="99cd4-198">Good places to test how your launcher looks in the various lights in the environment are the Studio, the Media Room, anywhere outside and on the Back Patio (the concrete area with the lawn).</span></span> <span data-ttu-id="99cd4-199">Un autre bon test consiste à placer dans la moitié de lumière et la moitié de clichés instantanés et voir à quoi elle ressemble.</span><span class="sxs-lookup"><span data-stu-id="99cd4-199">Another good test is to put it in half light and half shadow and see what it looks like.</span></span>

<span data-ttu-id="99cd4-200">![Assurez-vous que votre Lanceur semble correct dans la lumière et les ombres.](images/20171013-145523-mixedreality-1200px-1000px.jpg)</span><span class="sxs-lookup"><span data-stu-id="99cd4-200">![Make sure your launcher looks good in both light and shadows.](images/20171013-145523-mixedreality-1200px-1000px.jpg)</span></span><br>
<span data-ttu-id="99cd4-201">*Assurez-vous que votre Lanceur semble correct dans la lumière et les ombres*</span><span class="sxs-lookup"><span data-stu-id="99cd4-201">*Make sure your launcher looks good in both light and shadows*</span></span>

## <a name="texturing"></a><span data-ttu-id="99cd4-202">Texture</span><span class="sxs-lookup"><span data-stu-id="99cd4-202">Texturing</span></span>

### <a name="authoring-your-textures"></a><span data-ttu-id="99cd4-203">Création de vos textures</span><span class="sxs-lookup"><span data-stu-id="99cd4-203">Authoring your textures</span></span>

<span data-ttu-id="99cd4-204">Le format de la fin de votre Lanceur d’applications 3D sera un fichier .glb, qui est effectué à l’aide du pipeline PBR (physiquement en fonction de rendu).</span><span class="sxs-lookup"><span data-stu-id="99cd4-204">The end format of your 3D app launcher will be a .glb file, which is made using the PBR (Physically Based Rendering) pipeline.</span></span> <span data-ttu-id="99cd4-205">Cela peut être un processus difficile, est maintenant temps d’employer un artiste technique si vous n’avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="99cd4-205">This can be a tricky process - now is a good time to employ a technical artist if you haven't already.</span></span> <span data-ttu-id="99cd4-206">Si vous êtes un courageux soi-même-er, prendre le temps de [effectuer des recherches et découvrez la terminologie PBR](http://wiki.polycount.com/wiki/PBR) et ce qui se passe sous le capot avant de commencer, vous éviterez les erreurs courantes.</span><span class="sxs-lookup"><span data-stu-id="99cd4-206">If you’re a brave DIY-er, taking the time to [research and learn PBR terminology](http://wiki.polycount.com/wiki/PBR) and what’s happening under the hood before you begin will help you avoid common mistakes.</span></span> 

<span data-ttu-id="99cd4-207">![Exemple : Application de Note de frais](images/pbr-freshnote1-640px-500px.png)</span><span class="sxs-lookup"><span data-stu-id="99cd4-207">![Example: Fresh Note app](images/pbr-freshnote1-640px-500px.png)</span></span><br>
<span data-ttu-id="99cd4-208">*Exemple de Lanceur d’application 3D Remarque fraîche (application fictive)*</span><span class="sxs-lookup"><span data-stu-id="99cd4-208">*Fresh Note 3D app launcher example (fictional app)*</span></span>

<span data-ttu-id="99cd4-209">**Outil de création recommandé**</span><span class="sxs-lookup"><span data-stu-id="99cd4-209">**Recommended authoring tool**</span></span>

<span data-ttu-id="99cd4-210">Nous vous recommandons d’utiliser [reproduire la mise en Substance](https://www.allegorithmic.com/products/substance-painter) par Allegorithmic pour créer votre fichier finale.</span><span class="sxs-lookup"><span data-stu-id="99cd4-210">We recommend using [Substance Painter](https://www.allegorithmic.com/products/substance-painter) by Allegorithmic to author your final file.</span></span> <span data-ttu-id="99cd4-211">Si vous n’êtes pas familiarisé avec la création de nuanceurs PBR en Substance, ici du peintre un [didacticiel](https://docs.allegorithmic.com/documentation/display/SPDOC/Tutorials).</span><span class="sxs-lookup"><span data-stu-id="99cd4-211">If you’re not familiar with authoring PBR shaders in Substance Painter, here’s a [tutorial](https://docs.allegorithmic.com/documentation/display/SPDOC/Tutorials).</span></span>

<span data-ttu-id="99cd4-212">(Vous pouvez également cliquer [3D-Coat](https://3dcoat.com/home/), [Quixel Suite 2](https://quixel.se/suite2/), ou [Marmoset Toolbag](https://www.marmoset.co/toolbag/) fonctionne également si vous êtes familiarisé avec un d’eux.)</span><span class="sxs-lookup"><span data-stu-id="99cd4-212">(Alternately [3D-Coat](https://3dcoat.com/home/), [Quixel Suite 2](https://quixel.se/suite2/), or [Marmoset Toolbag](https://www.marmoset.co/toolbag/) would also work if you’re more familiar with one of these.)</span></span>

### <a name="best-practices"></a><span data-ttu-id="99cd4-213">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="99cd4-213">Best practices</span></span>

* <span data-ttu-id="99cd4-214">Si votre objet de lanceur d’application a été créé pour PBR, il doit être relativement simple pour le convertir pour l’environnement Cliff House.</span><span class="sxs-lookup"><span data-stu-id="99cd4-214">If your app launcher object was authored for PBR, it should be pretty straightforward to convert it for the Cliff House environment.</span></span>
* <span data-ttu-id="99cd4-215">Notre nuanceur attend un flux de travail complète/irrégularité : nuanceur de PBR Unreal l’est une télécopie ferme.</span><span class="sxs-lookup"><span data-stu-id="99cd4-215">Our shader is expecting a Metal/Roughness work flow – The Unreal PBR shader is a close facsimile.</span></span>
* <span data-ttu-id="99cd4-216">Lorsque l’exportation de vos textures de conserver le [texture tailles recommandées](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#material-guidelines) à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="99cd4-216">When exporting your textures keep the [recommended texture sizes](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md#material-guidelines) in mind.</span></span>
* <span data-ttu-id="99cd4-217">Veillez à créer vos objets d’éclairage en temps réel, cela signifie que :</span><span class="sxs-lookup"><span data-stu-id="99cd4-217">Make sure to build your objects for real-time lighting — this means:</span></span>
    * <span data-ttu-id="99cd4-218">Éviter les ombres cuites – ou shadows peintes</span><span class="sxs-lookup"><span data-stu-id="99cd4-218">Avoid baked shadows – or painted shadows</span></span>
    * <span data-ttu-id="99cd4-219">Éviter la boulangerie d’éclairage dans les textures</span><span class="sxs-lookup"><span data-stu-id="99cd4-219">Avoid baked lighting in the textures</span></span>
    * <span data-ttu-id="99cd4-220">Utilisez une de l’objet material PBR création de packages pour obtenir les mappages de droit générés pour notre nuanceur de</span><span class="sxs-lookup"><span data-stu-id="99cd4-220">Use one of the PBR material authoring packages to get the right maps generated for our shader</span></span>

## <a name="see-also"></a><span data-ttu-id="99cd4-221">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="99cd4-221">See also</span></span>

* [<span data-ttu-id="99cd4-222">Créer des modèles 3D pour une utilisation dans la réalité mixte domestique</span><span class="sxs-lookup"><span data-stu-id="99cd4-222">Create 3D models for use in the mixed reality home</span></span>](creating-3d-models-for-use-in-the-windows-mixed-reality-home.md)
* [<span data-ttu-id="99cd4-223">Implémenter des lanceurs d’applications 3D (applications UWP)</span><span class="sxs-lookup"><span data-stu-id="99cd4-223">Implement 3D app launchers (UWP apps)</span></span>](implementing-3d-app-launchers.md)
* [<span data-ttu-id="99cd4-224">Implémenter des lanceurs d’applications 3D (applications Win32)</span><span class="sxs-lookup"><span data-stu-id="99cd4-224">Implement 3D app launchers (Win32 apps)</span></span>](implementing-3d-app-launchers-win32.md)
