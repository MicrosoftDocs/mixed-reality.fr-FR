---
title: Étude de cas - création d’une galaxie en réalité mixte
description: Avant que Microsoft HoloLens expédié, nous avons demandé notre communauté de développeurs quel type d’application il souhaite voir une équipe interne expérimentée à générer pour le nouvel appareil. Plus de 5 000 idées ont été partagées, et après une interrogation de Twitter 24 heures, le gagnant était une idée appelée « Explorer Galaxy. »
author: KarimLUCCIN
ms.author: kaluccin
ms.date: 03/21/2018
ms.topic: article
keywords: Explorateur de Galaxy, HoloLens, réalité mixte Windows, partager vos idées, étude de cas
ms.openlocfilehash: a478eaa35144a8ee0fbeaeb43cec4b9f901890ab
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597017"
---
# <a name="case-study---creating-a-galaxy-in-mixed-reality"></a><span data-ttu-id="f422f-105">Étude de cas - création d’une galaxie en réalité mixte</span><span class="sxs-lookup"><span data-stu-id="f422f-105">Case study - Creating a galaxy in mixed reality</span></span>

<span data-ttu-id="f422f-106">Avant que Microsoft HoloLens expédié, nous avons demandé notre communauté de développeurs quel type d’application il souhaite voir une équipe interne expérimentée à générer pour le nouvel appareil.</span><span class="sxs-lookup"><span data-stu-id="f422f-106">Before Microsoft HoloLens shipped, we asked our developer community what kind of app they'd like to see an experienced internal team build for the new device.</span></span> <span data-ttu-id="f422f-107">Plus de 5 000 idées ont été partagées, et après une interrogation de Twitter 24 heures, le gagnant était une idée appelée [Galaxy Explorer](galaxy-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="f422f-107">More than 5000 ideas were shared, and after a 24-hour Twitter poll, the winner was an idea called [Galaxy Explorer](galaxy-explorer.md).</span></span>

<span data-ttu-id="f422f-108">Andy Zibits, le responsable de la bibliothèque sur le projet et Karim Luccin, ingénieur de graphiques de l’équipe, parler de l’effort de collaboration entre art et d’ingénierie qui ont conduit à la création d’une représentation précise et interactive du galaxy lactée dans l’Explorateur de Galaxy.</span><span class="sxs-lookup"><span data-stu-id="f422f-108">Andy Zibits, the art lead on the project, and Karim Luccin, the team's graphics engineer, talk about the collaborative effort between art and engineering that led to the creation of an accurate, interactive representation of the Milky Way galaxy in Galaxy Explorer.</span></span>

## <a name="the-tech"></a><span data-ttu-id="f422f-109">Les technologies</span><span class="sxs-lookup"><span data-stu-id="f422f-109">The Tech</span></span>

<span data-ttu-id="f422f-110">[Notre équipe](galaxy-explorer.md#meet-the-team) - constitués de deux concepteurs de trois développeurs, quatre artistes, un producteur et un testeur — avait six semaines pour générer une application entièrement fonctionnelle qui permettrait aux utilisateurs d’en savoir plus sur et explorez les vastness et la beauté de notre Galaxy lactée.</span><span class="sxs-lookup"><span data-stu-id="f422f-110">[Our team](galaxy-explorer.md#meet-the-team) - made up of two designers, three developers, four artists, a producer, and one tester — had six weeks to build a fully functional app which would allow people to learn about and explore the vastness and beauty of our Milky Way Galaxy.</span></span>

<span data-ttu-id="f422f-111">Nous souhaitons tirer pleinement parti de la possibilité d’effectuer le rendu des objets 3D directement dans votre espace de vie, donc nous avons décidé de créer un aspect réaliste galaxy où les personnes serait en mesure de zoomer fermer et voir les étoiles individuels, chacun sur leurs propres trajectoires de HoloLens .</span><span class="sxs-lookup"><span data-stu-id="f422f-111">We wanted to take full advantage of the ability of HoloLens to render 3D objects directly in your living space, so we decided we wanted to create a realistic looking galaxy where people would be able to zoom in close and see individual stars, each on their own trajectories.</span></span>

<span data-ttu-id="f422f-112">Dans la première semaine du développement, nous avons élaboré quelques objectifs pour notre le Galaxy lactée représentation : Il est nécessaire d’avoir une profondeur, de déplacement et la convivialité volumétrique — intégral d’étoiles qui permet de créer la forme du galaxy.</span><span class="sxs-lookup"><span data-stu-id="f422f-112">In the first week of development, we came up with a few goals for our representation of the Milky Way Galaxy: It needed to have depth, movement, and feel volumetric—full of stars that would help create the shape of the galaxy.</span></span>

<span data-ttu-id="f422f-113">Le problème avec la création d’un galaxy animée qui avait des milliards d’étoiles était que le nombre d’éléments uniques nécessitant la mise à jour serait trop volumineux par trame pour HoloLens animer à l’aide de l’UC.</span><span class="sxs-lookup"><span data-stu-id="f422f-113">The problem with creating an animated galaxy that had billions of stars was that the sheer number of single elements that need updating would be too big per frame for HoloLens to animate using the CPU.</span></span> <span data-ttu-id="f422f-114">Notre solution impliquait un mélange complexe de l’art et de science.</span><span class="sxs-lookup"><span data-stu-id="f422f-114">Our solution involved a complex mix of art and science.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="f422f-115">En arrière-plan</span><span class="sxs-lookup"><span data-stu-id="f422f-115">Behind the scenes</span></span>

<span data-ttu-id="f422f-116">Pour permettre aux utilisateurs d’Explorer les étoiles individuels, notre première étape a été de déterminer combien de particules nous aurions pu effectuer le rendu à la fois.</span><span class="sxs-lookup"><span data-stu-id="f422f-116">To allow people to explore individual stars, our first step was to figure out how many particles we could render at once.</span></span>

### <a name="rendering-particles"></a><span data-ttu-id="f422f-117">Particules de rendu</span><span class="sxs-lookup"><span data-stu-id="f422f-117">Rendering particles</span></span>

<span data-ttu-id="f422f-118">UC actuelles est très utiles pour le traitement des tâches en série et jusqu'à quelques tâches parallèles en une seule fois (en fonction du nombre de cœurs sont-ils), mais les GPU sont beaucoup plus efficaces pour traiter des milliers d’opérations en parallèle.</span><span class="sxs-lookup"><span data-stu-id="f422f-118">Current CPUs are great for processing serial tasks and up to a few parallel tasks at once (depending on how many cores they have), but GPUs are much more effective at processing thousands of operations in parallel.</span></span> <span data-ttu-id="f422f-119">Toutefois, car ils ne partagent généralement la même mémoire que l’UC, échange de données entre les UC <> GPU peut rapidement devenir un goulot d’étranglement.</span><span class="sxs-lookup"><span data-stu-id="f422f-119">However, because they don’t usually share the same memory as the CPU, exchanging data between CPU<>GPU can quickly become a bottleneck.</span></span> <span data-ttu-id="f422f-120">Notre solution était de rendre une galaxie sur le GPU, et il devait live complètement sur le GPU.</span><span class="sxs-lookup"><span data-stu-id="f422f-120">Our solution was to make a galaxy on the GPU, and it had to live completely on the GPU.</span></span>

<span data-ttu-id="f422f-121">Nous avons commencé à des tests de contrainte avec des milliers de particules de point dans différents modèles.</span><span class="sxs-lookup"><span data-stu-id="f422f-121">We started stress tests with thousands of point particles in various patterns.</span></span> <span data-ttu-id="f422f-122">Cela nous a permis d’obtenir le galaxy sur HoloLens pour voir ce qui a fonctionné et ce qui n’a pas.</span><span class="sxs-lookup"><span data-stu-id="f422f-122">This allowed us to get the galaxy on HoloLens to see what worked and what didn’t.</span></span>

### <a name="creating-the-position-of-the-stars"></a><span data-ttu-id="f422f-123">Création de la position des étoiles</span><span class="sxs-lookup"><span data-stu-id="f422f-123">Creating the position of the stars</span></span>

<span data-ttu-id="f422f-124">Un membre de notre équipe avait déjà écrit le C# code susceptible de générer étoiles à leur position initiale.</span><span class="sxs-lookup"><span data-stu-id="f422f-124">One of our team members had already written the C# code that would generate stars at their initial position.</span></span> <span data-ttu-id="f422f-125">Les étoiles se trouvent sur une ellipse et leur position pouvant être décrits par (**curveOffset**, **ellipseSize**, **élévation**) où **curveOffset**est l’angle de l’étoile le long de l’ellipse, **ellipseSize** est la dimension de l’ellipse le long de X et Z et l’élévation l’élévation appropriée de l’étoile dans le galaxy.</span><span class="sxs-lookup"><span data-stu-id="f422f-125">The stars are on an ellipse and their position can be described by (**curveOffset**, **ellipseSize**, **elevation**) where **curveOffset** is the angle of the star along the ellipse, **ellipseSize** is the dimension of the ellipse along X and Z, and elevation the proper elevation of the star within the galaxy.</span></span> <span data-ttu-id="f422f-126">Par conséquent, nous pouvons créer une mémoire tampon ([ComputeBuffer d’Unity](http://docs.unity3d.com/ScriptReference/ComputeBuffer.html)) qui serait initialisée avec chaque attribut en étoile et les envoyer sur le GPU où il serait live pour le reste de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="f422f-126">Thus, we can create a buffer ([Unity’s ComputeBuffer](http://docs.unity3d.com/ScriptReference/ComputeBuffer.html)) that would be initialized with each star attribute and send it on the GPU where it would live for the rest of the experience.</span></span> <span data-ttu-id="f422f-127">Pour dessiner cette mémoire tampon, nous utilisons [DrawProcedural d’Unity](http://docs.unity3d.com/ScriptReference/Graphics.DrawProcedural.html) qui permet d’exécuter un shader (code sur un GPU) sur un ensemble arbitraire de points sans avoir une maille réelle qui représente le galaxy :</span><span class="sxs-lookup"><span data-stu-id="f422f-127">To draw this buffer, we use [Unity’s DrawProcedural](http://docs.unity3d.com/ScriptReference/Graphics.DrawProcedural.html) which allows running a shader (code on a GPU) on an arbitrary set of points without having an actual mesh that represents the galaxy:</span></span>

<span data-ttu-id="f422f-128">**PROCESSEUR :**</span><span class="sxs-lookup"><span data-stu-id="f422f-128">**CPU:**</span></span>




```
GraphicsDrawProcedural(MeshTopology.Points, starCount, 1);
```

<span data-ttu-id="f422f-129">**GPU :**</span><span class="sxs-lookup"><span data-stu-id="f422f-129">**GPU:**</span></span>




```
v2g vert (uint index : SV_VertexID)
{

 // _Stars is the buffer we created that contains the initial state of the system
 StarDescriptor star = _Stars[index];
 …

}
```

<span data-ttu-id="f422f-130">Nous avons commencé avec des modèles circulaires brutes avec des milliers de particules.</span><span class="sxs-lookup"><span data-stu-id="f422f-130">We started with raw circular patterns with thousands of particles.</span></span> <span data-ttu-id="f422f-131">Cela nous a donné la preuve que nous devions nous aurions pu gérer plusieurs particules et l’exécuter à des vitesses de performante, mais nous n’avons pas satisfaits de la forme générale de la galaxy.</span><span class="sxs-lookup"><span data-stu-id="f422f-131">This gave us the proof we needed that we could manage many particles AND run it at performant speeds, but we weren’t satisfied with the overall shape of the galaxy.</span></span> <span data-ttu-id="f422f-132">Pour améliorer la forme, nous avons essayé de différents modèles et les systèmes de particules avec une rotation.</span><span class="sxs-lookup"><span data-stu-id="f422f-132">To improve the shape, we attempted various patterns and particle systems with rotation.</span></span> <span data-ttu-id="f422f-133">Celles-ci étaient initialement prometteurs, car le nombre de particules et performances restée cohérent, mais la forme est tombé en panne près du centre et les étoiles émettait vers l’extérieur qui n’était pas réaliste.</span><span class="sxs-lookup"><span data-stu-id="f422f-133">These were initially promising because the number of particles and performance stayed consistent, but the shape broke down near the center and the stars were emitting outwardly which wasn't realistic.</span></span> <span data-ttu-id="f422f-134">Nous avions besoin d’une émission qui nous permettrait de manipuler les temps et que les particules à déplacer dans la pratique, une boucle sans cesse plus étroite au centre du galaxy.</span><span class="sxs-lookup"><span data-stu-id="f422f-134">We needed an emission that would allow us to manipulate time and have the particles move realistically, looping ever closer to the center of the galaxy.</span></span>

![Nous avons essayé de différents modèles et les systèmes de particules de faire pivoter, comme celles-ci.](images/galaxy-patterns-500px.png)

<span data-ttu-id="f422f-136">Nous avons essayé de différents modèles et les systèmes de particules de faire pivoter, comme celles-ci.</span><span class="sxs-lookup"><span data-stu-id="f422f-136">We attempted various patterns and particle systems that rotated, like these.</span></span>

<span data-ttu-id="f422f-137">Notre équipe a fait des recherches sur la fonction de galaxies moyen et nous avons apporté un système de particules personnalisée spécifiquement pour le galaxy afin que nous pourrions passer les particules basés sur des points de suspension «[théorie sur les ondes de densité](https://en.wikipedia.org/wiki/Density_wave_theory), » qui theorizes qui les branches d’un Galaxy sont des zones de densité plus élevée, mais dans un flux constant, comme un embouteillage.</span><span class="sxs-lookup"><span data-stu-id="f422f-137">Our team did some research about the way galaxies function and we made a custom particle system specifically for the galaxy so that we could move the particles on ellipses based on "[density wave theory](https://en.wikipedia.org/wiki/Density_wave_theory)," which theorizes that the arms of a galaxy are areas of higher density but in constant flux, like a traffic jam.</span></span> <span data-ttu-id="f422f-138">Il semble stable et solide, mais les étoiles bougent vers et depuis les bras lorsqu’ils passent le long de leurs points de suspension respectifs.</span><span class="sxs-lookup"><span data-stu-id="f422f-138">It appears stable and solid, but the stars are actually moving in and out of the arms as they move along their respective ellipses.</span></span> <span data-ttu-id="f422f-139">Dans notre système, les particules existent jamais sur le processeur — nous générer les cartes et les orienter tous sur le GPU, par conséquent, l’ensemble du système est simplement initialState + temps nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f422f-139">In our system, the particles never exist on the CPU—we generate the cards and orient them all on the GPU, so the whole system is simply initial state + time.</span></span> <span data-ttu-id="f422f-140">Il s’est déroulée comme suit :</span><span class="sxs-lookup"><span data-stu-id="f422f-140">It progressed like this:</span></span>

![Progression de système de particules avec le rendu du GPU](images/spiral-galaxy-arms-500px.jpg)

<span data-ttu-id="f422f-142">Progression de système de particules avec le rendu du GPU</span><span class="sxs-lookup"><span data-stu-id="f422f-142">Progression of particle system with GPU rendering</span></span>


<span data-ttu-id="f422f-143">Une fois que suffisamment points de suspension sont ajoutés et sont définies pour faire pivoter, les galaxies ont commencé au formulaire « armes » où le déplacement des étoiles converger.</span><span class="sxs-lookup"><span data-stu-id="f422f-143">Once enough ellipses are added and are set to rotate, the galaxies began to form “arms” where the movement of stars converge.</span></span> <span data-ttu-id="f422f-144">L’espacement des étoiles sur chaque tracé elliptique ont été fournie à un caractère aléatoire, et chaque étoile a obtenu un peu de caractère aléatoire positionnel ajouté.</span><span class="sxs-lookup"><span data-stu-id="f422f-144">The spacing of the stars along each elliptical path was given some randomness, and each star got a bit of positional randomness added.</span></span> <span data-ttu-id="f422f-145">Cela créé une distribution qui recherchent beaucoup plus naturelle de la forme de mouvement et arm en étoile.</span><span class="sxs-lookup"><span data-stu-id="f422f-145">This created a much more natural looking distribution of star movement and arm shape.</span></span> <span data-ttu-id="f422f-146">Enfin, nous avons ajouté la possibilité de couleur de lecteur en fonction de distance à partir du centre.</span><span class="sxs-lookup"><span data-stu-id="f422f-146">Finally, we added the ability to drive color based on distance from center.</span></span>

### <a name="creating-the-motion-of-the-stars"></a><span data-ttu-id="f422f-147">Création le mouvement des étoiles</span><span class="sxs-lookup"><span data-stu-id="f422f-147">Creating the motion of the stars</span></span>

<span data-ttu-id="f422f-148">Pour animer le mouvement en étoile général, nous avions besoin pour ajouter un angle constant pour chaque trame et pour obtenir des étoiles déplacer le long de leurs points de suspension à une vitesse constante radiale.</span><span class="sxs-lookup"><span data-stu-id="f422f-148">To animate the general star motion, we needed to add a constant angle for each frame and to get stars moving along their ellipses at a constant radial velocity.</span></span> <span data-ttu-id="f422f-149">C’est la raison principale pour l’utilisation de **curveOffset**.</span><span class="sxs-lookup"><span data-stu-id="f422f-149">This is the primary reason for using **curveOffset**.</span></span> <span data-ttu-id="f422f-150">Ce n’est pas techniquement correct, comme les étoiles déplacera plus rapidement sur les côtés long des ellipses, mais le mouvement général senti bon.</span><span class="sxs-lookup"><span data-stu-id="f422f-150">This isn’t technically correct as stars will move faster along the long sides of the ellipses, but the general motion felt good.</span></span>

![Étoiles accélère la migration de l’arc long, plus lent sur les bords.](images/ellipse-movement.jpg)

<span data-ttu-id="f422f-152">Étoiles accélère la migration de l’arc long, plus lent sur les bords.</span><span class="sxs-lookup"><span data-stu-id="f422f-152">Stars move faster on the long arc, slower on the edges.</span></span>


<span data-ttu-id="f422f-153">Avec cela, chaque étoile est entièrement décrite par (**curveOffset**, **ellipseSize**, **élévation**, **âge**) où **âge** est une accumulation du temps total écoulé depuis la scène a été chargée.</span><span class="sxs-lookup"><span data-stu-id="f422f-153">With that, each star is fully described by (**curveOffset**, **ellipseSize**, **elevation**, **Age**) where **Age** is an accumulation of the total time that has passed since the scene was loaded.</span></span>




```
float3 ComputeStarPosition(StarDescriptor star)
{

  float curveOffset = star.curveOffset + Age;
  
  // this will be coded as a “sincos” on the hardware which will compute both sides
  float x = cos(curveOffset) * star.xRadii;
  float z = sin(curveOffset) * star.zRadii;
   
  return float3(x, star.elevation, z);
  
}
```

<span data-ttu-id="f422f-154">Cela a permis de générer des dizaines de milliers d’étoiles qu’une seule fois au début de l’application, puis nous animée un ensemble simples d’étoiles sur les courbes établis.</span><span class="sxs-lookup"><span data-stu-id="f422f-154">This allowed us to generate tens of thousands of stars once at the start of the application, then we animated a singled set of stars along the established curves.</span></span> <span data-ttu-id="f422f-155">Dans la mesure où tout est sur le GPU, le système peut animer tous les étoiles en parallèle sans coût à l’UC.</span><span class="sxs-lookup"><span data-stu-id="f422f-155">Since everything is on the GPU, the system can animate all the stars in parallel at no cost to the CPU.</span></span>

![Voici à quoi elle ressemble lorsque dessin quadrilatères blancs.](images/drawing-white-quads-300px.jpg)

<span data-ttu-id="f422f-157">Voici à quoi elle ressemble lorsque dessin quadrilatères blancs.</span><span class="sxs-lookup"><span data-stu-id="f422f-157">Here’s what it looks like when drawing white quads.</span></span>



<span data-ttu-id="f422f-158">Pour rendre chaque face quad l’appareil photo, nous avons utilisé un nuanceur de géométrie pour transformer chaque position en étoile à un rectangle 2D de l’écran qui contient notre texture en étoile.</span><span class="sxs-lookup"><span data-stu-id="f422f-158">To make each quad face the camera, we used a geometry shader to transform each star position to a 2D rectangle on the screen that will contain our star texture.</span></span>

![Diamants au lieu de quadrilatères.](images/drawing-white-quads-300px.jpg)

<span data-ttu-id="f422f-160">Diamants au lieu de quadrilatères.</span><span class="sxs-lookup"><span data-stu-id="f422f-160">Diamonds instead of quads.</span></span>


<span data-ttu-id="f422f-161">Étant donné que nous souhaitons limiter les superpositions (nombre de fois où un pixel est traité) autant que possible, nous paysage notre quadrilatères afin qu’ils auraient pas moins se chevauchent.</span><span class="sxs-lookup"><span data-stu-id="f422f-161">Because we wanted to limit the overdraw (number of times a pixel will be processed) as much as possible, we rotated our quads so that they would have less overlap.</span></span>

### <a name="adding-clouds"></a><span data-ttu-id="f422f-162">Ajout de clouds</span><span class="sxs-lookup"><span data-stu-id="f422f-162">Adding clouds</span></span>

<span data-ttu-id="f422f-163">Il existe de nombreuses façons d’obtenir un sentiment volumétrique avec particules — à partir de ray marching à l’intérieur d’un volume au dessin de particules autant que possible pour simuler un cloud.</span><span class="sxs-lookup"><span data-stu-id="f422f-163">There are many ways to get a volumetric feeling with particles—from ray marching inside of a volume to drawing as many particles as possible to simulate a cloud.</span></span> <span data-ttu-id="f422f-164">Ray en temps réel marching allait être trop coûteux et difficile d’auteur, donc nous avons tout d’abord tenté de création d’un système imposteur à l’aide d’une méthode pour les forêts de rendu dans les jeux, avec un grand nombre d’images 2D d’arbres accessible sur l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="f422f-164">Real-time ray marching was going to be too expensive and hard to author, so we first tried building an imposter system using a method for rendering forests in games—with a lot of 2D images of trees facing the camera.</span></span> <span data-ttu-id="f422f-165">Lorsque nous le faire dans un jeu, nous pouvons avoir les textures de rendu à partir d’un appareil photo qui pivote autour, enregistrez toutes ces images et lors de l’exécution pour chaque carte billboard des arborescences, sélectionnez l’image qui correspond à la direction de la vue.</span><span class="sxs-lookup"><span data-stu-id="f422f-165">When we do this in a game, we can have textures of trees rendered from a camera that rotates around, save all those images, and at runtime for each billboard card, select the image that matches the view direction.</span></span> <span data-ttu-id="f422f-166">Cela ne fonctionne pas aussi bien lorsque les images sont hologrammes.</span><span class="sxs-lookup"><span data-stu-id="f422f-166">This doesn't work as well when the images are holograms.</span></span> <span data-ttu-id="f422f-167">La différence entre l’oeil gauche et de l’oeil droit faire en sorte que nous avons besoin d’une plus grande résolution, sans quoi il recherche simplement à plat, un alias, ou répétitives.</span><span class="sxs-lookup"><span data-stu-id="f422f-167">The difference between the left eye and the right eye make it so that we need a much higher resolution, or else it just looks flat, aliased, or repetitive.</span></span>

<span data-ttu-id="f422f-168">Lors de notre deuxième tentative, nous avons essayé d’avoir des particules autant que possible.</span><span class="sxs-lookup"><span data-stu-id="f422f-168">On our second attempt, we tried having as many particles as possible.</span></span> <span data-ttu-id="f422f-169">Les meilleurs visuels ont été obtenus lorsque nous avons dessiné de particules feu et que vous les floue avant de les ajouter à la scène.</span><span class="sxs-lookup"><span data-stu-id="f422f-169">The best visuals were achieved when we additively drew particles and blurred them before adding them to the scene.</span></span> <span data-ttu-id="f422f-170">Les problèmes classiques de cette approche ont été liés à combien de particules nous pouvons dessiner en une seule fois et écran combien ils superficie tout en conservant 60 i/s.</span><span class="sxs-lookup"><span data-stu-id="f422f-170">The typical problems with that approach were related to how many particles we could draw at a single time and how much screen area they covered while still maintaining 60fps.</span></span> <span data-ttu-id="f422f-171">Flou de l’image obtenue pour obtenir ce cloud que vous vous sentez était généralement une opération très coûteuse.</span><span class="sxs-lookup"><span data-stu-id="f422f-171">Blurring the resulting image to get this cloud feeling was usually a very costly operation.</span></span>

![Sans la texture, c’est quoi ressemblerait les clouds avec une opacité de 2 %.](images/clouds-without-texture-300px.jpg)

<span data-ttu-id="f422f-173">Sans la texture, c’est quoi ressemblerait les clouds avec une opacité de 2 %.</span><span class="sxs-lookup"><span data-stu-id="f422f-173">Without texture, this is what the clouds would look like with 2% opacity.</span></span>



<span data-ttu-id="f422f-174">Additif en cours et avoir un grand nombre d'entre eux signifie que nous devrions plusieurs quadrilatères au-dessus des autres, ombrage à plusieurs reprises le même pixel.</span><span class="sxs-lookup"><span data-stu-id="f422f-174">Being additive and having a lot of them means that we would have several quads on top of each other, repeatedly shading the same pixel.</span></span> <span data-ttu-id="f422f-175">Dans le centre du galaxy, le même pixel a des centaines de quadrilatères superposées et cela a un coût considérable lorsque effectué plein écran.</span><span class="sxs-lookup"><span data-stu-id="f422f-175">In the center of the galaxy, the same pixel has hundreds of quads on top of each other and this had a huge cost when being done full screen.</span></span>

<span data-ttu-id="f422f-176">Effectuant des clouds de plein écran et essayez de les flou aurait été une mauvaise idée, par conséquent, au lieu de cela que nous avons décidé de laisser le matériel de faire le travail pour nous.</span><span class="sxs-lookup"><span data-stu-id="f422f-176">Doing full screen clouds and trying to blur them would have been a bad idea, so instead we decided to let the hardware do the work for us.</span></span>

### <a name="a-bit-of-context-first"></a><span data-ttu-id="f422f-177">Un bit du contexte tout d’abord</span><span class="sxs-lookup"><span data-stu-id="f422f-177">A bit of context first</span></span>

<span data-ttu-id="f422f-178">Lors de l’utilisation des textures dans un jeu de la taille de texture rarement correspond à la zone que nous souhaitons utiliser dans, mais nous pouvons utiliser différents types de filtrage pour obtenir la carte graphique pour interpoler la couleur que nous voulons des pixels de la texture de texture ([defiltragedeTexture<C3/>](https://msdn.microsoft.com/library/dn642451.aspx)).</span><span class="sxs-lookup"><span data-stu-id="f422f-178">When using textures in a game the texture size will rarely match the area we want to use it in, but we can use different kind of texture filtering to get the graphic card to interpolate the color we want from the pixels of the texture ([Texture Filtering](https://msdn.microsoft.com/library/dn642451.aspx)).</span></span> <span data-ttu-id="f422f-179">Le filtrage qui nous intéresse est [Filtrage bilinéaire](https://msdn.microsoft.com/library/windows/desktop/bb172357.aspx) qui calcule la valeur d’un pixel à l’aide de la 4 voisins les plus proches.</span><span class="sxs-lookup"><span data-stu-id="f422f-179">The filtering that interests us is [bilinear filtering](https://msdn.microsoft.com/library/windows/desktop/bb172357.aspx) which will compute the value of any pixel using the 4 nearest neighbors.</span></span>

![Original avant le filtrage](images/texture-1.png)

![Résultat après le filtrage](images/texture-2.png)

<span data-ttu-id="f422f-182">À l’aide de cette propriété, nous voyons que chaque fois que nous essayons de dessiner une texture dans une zone à deux reprises en tant que big, brouiller le résultat.</span><span class="sxs-lookup"><span data-stu-id="f422f-182">Using this property, we see that each time we try to draw a texture into an area twice as big, it blurs the result.</span></span>

<span data-ttu-id="f422f-183">Au lieu de rendu au mode plein écran et perdre ces millisecondes précieux, que nous pourrions passer sur autre chose, nous affichons vers une version minuscule de l’écran.</span><span class="sxs-lookup"><span data-stu-id="f422f-183">Instead of rendering to a full screen and losing those precious milliseconds we could be spending on something else, we render to a tiny version of the screen.</span></span> <span data-ttu-id="f422f-184">Ensuite, en copiant cette texture et en étirant selon un facteur de 2 plusieurs fois, nous obtenons en plein écran tout en atténuant le contenu dans le processus.</span><span class="sxs-lookup"><span data-stu-id="f422f-184">Then, by copying this texture and stretching it by a factor of 2 several times, we get back to full screen while blurring the content in the process.</span></span>

![x3 haut de gamme à pleine résolution.](images/galaxy-resolutions-300px.png)

<span data-ttu-id="f422f-186">x3 haut de gamme à pleine résolution.</span><span class="sxs-lookup"><span data-stu-id="f422f-186">x3 upscale back to full resolution.</span></span>



<span data-ttu-id="f422f-187">Cela a permis de récupérer la partie cloud avec uniquement une fraction du coût d’origine.</span><span class="sxs-lookup"><span data-stu-id="f422f-187">This allowed us to get the cloud part with only a fraction of the original cost.</span></span> <span data-ttu-id="f422f-188">Au lieu d’ajouter des clouds sur la résolution maximale, nous uniquement paint 1/64 pixels et simplement étirer la texture à pleine résolution.</span><span class="sxs-lookup"><span data-stu-id="f422f-188">Instead of adding clouds on the full resolution, we only paint 1/64th of the pixels and just stretch the texture back to full resolution.</span></span>

![Gauche, avec un haut de gamme parlent de 1/8 en pleine résolution ; et bien, avec 3 haut de gamme à l’aide de la puissance de 2.](images/stars-upscaled-300px.jpg)

<span data-ttu-id="f422f-190">Gauche, avec un haut de gamme parlent de 1/8 en pleine résolution ; et bien, avec 3 haut de gamme à l’aide de la puissance de 2.</span><span class="sxs-lookup"><span data-stu-id="f422f-190">Left, with an upscale from 1/8th to full resolution; and right, with 3 upscale using power of 2.</span></span>


<span data-ttu-id="f422f-191">Notez que de l’accès à partir de 1/64, la taille pour la version complète la taille d’un coup ressemblerait complètement différente, comme la carte graphique utiliseriez toujours 4 pixels à ombrer une zone plus grande dans notre programme d’installation et d’artefacts commencent à apparaître.</span><span class="sxs-lookup"><span data-stu-id="f422f-191">Note that trying to go from 1/64th of the size to the full size in one go would look completely different, as the graphic card would still use 4 pixels in our setup to shade a bigger area and artifacts start to appear.</span></span>

<span data-ttu-id="f422f-192">Ensuite, si nous ajoutons les étoiles pleine résolution avec cartes plus petites, nous obtenons le galaxy complète :</span><span class="sxs-lookup"><span data-stu-id="f422f-192">Then, if we add full resolution stars with smaller cards, we get the full galaxy:</span></span>

![Près de résultat final du rendu galaxy en utilisant les étoiles pleine résolution](images/full-galaxy-500px.png)

<span data-ttu-id="f422f-194">Une fois que nous avons sur la bonne voie avec la forme, nous avons ajouté une couche de clouds, permutée les points temporaires avec ceux que nous peints dans Photoshop et ajouté des couleurs supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f422f-194">Once we were on the right track with the shape, we added a layer of clouds, swapped out the temporary dots with ones we painted in Photoshop, and added some additional color.</span></span> <span data-ttu-id="f422f-195">Il en résultait une galaxie lactée notre art et ingénieurs les deux senti bons pour qu’il atteint ses objectifs en matière de profondeur, de volume et de mouvement, tout cela sans imposer de l’UC.</span><span class="sxs-lookup"><span data-stu-id="f422f-195">The result was a Milky Way Galaxy our art and engineering teams both felt good about and it met our goals of having depth, volume, and motion—all without taxing the CPU.</span></span>

![Notre Galaxy lactée finale en 3D.](images/final-galaxy-500px.jpg)

<span data-ttu-id="f422f-197">Notre Galaxy lactée finale en 3D.</span><span class="sxs-lookup"><span data-stu-id="f422f-197">Our final Milky Way Galaxy in 3D.</span></span>


### <a name="more-to-explore"></a><span data-ttu-id="f422f-198">Autres points à Explorer</span><span class="sxs-lookup"><span data-stu-id="f422f-198">More to explore</span></span>

<span data-ttu-id="f422f-199">Nous avons le code de l’application Explorateur de Galaxy open source et qu’il est disponible sur [GitHub](https://github.com/Microsoft/GalaxyExplorer) aux développeurs de créer.</span><span class="sxs-lookup"><span data-stu-id="f422f-199">We've open-sourced the code for the Galaxy Explorer app and made it available on [GitHub](https://github.com/Microsoft/GalaxyExplorer) for developers to build on.</span></span>

<span data-ttu-id="f422f-200">Vous souhaitez trouver plus d’informations sur le processus de développement pour Explorer de Galaxy ?</span><span class="sxs-lookup"><span data-stu-id="f422f-200">Interested in finding out more about the development process for Galaxy Explorer?</span></span> <span data-ttu-id="f422f-201">Découvrez toutes nos cours projet mises à jour sur le [chaîne YouTube de Microsoft HoloLens](https://www.youtube.com/playlist?list=PLZCHH_4VqpRj0Nl46J0LNRkMyBNU4knbL).</span><span class="sxs-lookup"><span data-stu-id="f422f-201">Check out all our past project updates on the [Microsoft HoloLens YouTube channel](https://www.youtube.com/playlist?list=PLZCHH_4VqpRj0Nl46J0LNRkMyBNU4knbL).</span></span>

## <a name="about-the-authors"></a><span data-ttu-id="f422f-202">À propos des auteurs</span><span class="sxs-lookup"><span data-stu-id="f422f-202">About the authors</span></span>

<table style="border:0">
<tr>
<td style="border:0" width="60px"> <img alt="Picture of Karim Luccin at his desk" width="60" height="60" src="images/karim-thumb.jpg" /></td>
<td style="border:0"><span data-ttu-id="f422f-203"><b>Karim Luccin</b> est un ingénieur logiciel et un passionné de fantaisie visuels.</span><span class="sxs-lookup"><span data-stu-id="f422f-203"><b>Karim Luccin</b> is a Software Engineer and fancy visuals enthusiast.</span></span> <span data-ttu-id="f422f-204">Il a été l’ingénieur de graphiques pour Explorer de Galaxy.</span><span class="sxs-lookup"><span data-stu-id="f422f-204">He was the Graphics Engineer for Galaxy Explorer.</span></span></td>
</tr>
<tr>
<td style="border:0" width="60px"> <img alt="Photo of art lead Andy Zibits" width="60" height="60" src="images/andy-avatar.png" /></td>
<td style="border:0"><span data-ttu-id="f422f-205"><b>Andy Zibits</b> est un Art Lead et espace passionné gérés de l’équipe de modélisation 3D pour Explorer de Galaxy et lutté pour encore plus de particules.</span><span class="sxs-lookup"><span data-stu-id="f422f-205"><b>Andy Zibits</b> is an Art Lead and space enthusiast who managed the 3D modeling team for Galaxy Explorer and fought for even more particles.</span></span></td>
</tr>
</table>


## <a name="see-also"></a><span data-ttu-id="f422f-206">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f422f-206">See also</span></span>
* [<span data-ttu-id="f422f-207">Explorer Galaxy sur GitHub</span><span class="sxs-lookup"><span data-stu-id="f422f-207">Galaxy Explorer on GitHub</span></span>](https://github.com/Microsoft/GalaxyExplorer)
* [<span data-ttu-id="f422f-208">Mises à jour de projet Galaxy Explorer sur YouTube</span><span class="sxs-lookup"><span data-stu-id="f422f-208">Galaxy Explorer project updates on YouTube</span></span>](https://www.youtube.com/playlist?list=PLZCHH_4VqpRj0Nl46J0LNRkMyBNU4knbL)
