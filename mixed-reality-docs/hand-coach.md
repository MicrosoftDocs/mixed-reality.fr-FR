---
title: Guide de conception de MRTK main
description: mains en 3D qui sont déclenchées lorsque le système ne détecte pas les mains de l’utilisateur pour aider à les assister.
author: grayclee
ms.author: glee
ms.date: 09/25/2019
ms.topic: article
keywords: Windows Mixed Reality, conception, coach, casque immersif, MRTK, mains, main
ms.openlocfilehash: dc04f8f77548b226a822576befd60be107f4d3fb
ms.sourcegitcommit: 87aca9c2b73b0e83cb70a46443dcdb08c3621005
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/17/2020
ms.locfileid: "77373520"
---
# <a name="hand-coach-design-guidance"></a><span data-ttu-id="d269a-104">Conseils de conception pour les autocars manuels</span><span class="sxs-lookup"><span data-stu-id="d269a-104">Hand coach design guidance</span></span>

<span data-ttu-id="d269a-105">La main est un modèle de mains en 3D qui est déclenché lorsque le système ne détecte pas les mains de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d269a-105">Hand Coach is 3D modeled hands that are triggered when the system does not detect the user’s hands.</span></span> <span data-ttu-id="d269a-106">Elle est implémentée en tant que composant « d’apprentissage » qui aide à guider l’utilisateur lorsque le mouvement n’a pas été enseigné.</span><span class="sxs-lookup"><span data-stu-id="d269a-106">This is implemented as a “teaching” component that helps guide the user when the gesture has not been taught.</span></span> <span data-ttu-id="d269a-107">Si les utilisateurs n’ont pas effectué le mouvement spécifié pour un point, les mains sont en boucle avec un délai.</span><span class="sxs-lookup"><span data-stu-id="d269a-107">If users have not done the specified gesture for a period, the hands will loop with a delay.</span></span> <span data-ttu-id="d269a-108">L’entraîneur peut être utilisé pour représenter un bouton ou un hologramme.</span><span class="sxs-lookup"><span data-stu-id="d269a-108">The Hand coach could be used to represent pressing a button or picking up a hologram.</span></span>  


<span data-ttu-id="d269a-109">![exemple : main](images/HandCoach/MRTK_handCoach.jpg)</span><span class="sxs-lookup"><span data-stu-id="d269a-109">![Example: Hand coach](images/HandCoach/MRTK_handCoach.jpg)</span></span><br>
<span data-ttu-id="d269a-110">*Exemple HandCoach à partir de MRTK*</span><span class="sxs-lookup"><span data-stu-id="d269a-110">*HandCoach Example from MRTK*</span></span>

## <a name="hand-coach-provided"></a><span data-ttu-id="d269a-111">Autocar fourni</span><span class="sxs-lookup"><span data-stu-id="d269a-111">Hand coach provided</span></span>

<span data-ttu-id="d269a-112">Le modèle d’interaction actuel représente un large éventail de contrôles de mouvement, tels que le défilement, l’amplitude de sélection et le TAP.</span><span class="sxs-lookup"><span data-stu-id="d269a-112">The current interaction model represents a wide variety of gesture controls such as scrolling, far select, and near tap.</span></span> <span data-ttu-id="d269a-113">Vous trouverez ci-dessous une liste complète des gestes existants disponibles dans<a href="https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets"> MRTK</a>:</span><span class="sxs-lookup"><span data-stu-id="d269a-113">Below is a full list of existing hand gestures provided in<a href="https://github.com/microsoft/MixedRealityToolkit-Unity/tree/mrtk_release/Assets"> MRTK</a>:</span></span>

:::row:::
    :::column:::
       <span data-ttu-id="d269a-114">![exemple de près de Select](images/HandCoach/NearSelect.gif)</span><span class="sxs-lookup"><span data-stu-id="d269a-114">![Example of Near Select](images/HandCoach/NearSelect.gif)</span></span><br>
       <span data-ttu-id="d269a-115">**Exemple de près de Select-used montre comment sélectionner des boutons ou fermer des objets interactifs**</span><span class="sxs-lookup"><span data-stu-id="d269a-115">**Example of Near Select - Used show how to select buttons or close interactable objects**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="d269a-116">![exemple de pression d’air](images/HandCoach/AirTap.gif)</span><span class="sxs-lookup"><span data-stu-id="d269a-116">![Example of Air Tap](images/HandCoach/AirTap.gif)</span></span><br>
        <span data-ttu-id="d269a-117">**Exemple de robinet d’air-utilisé pour montrer comment sélectionner des objets éloignés**</span><span class="sxs-lookup"><span data-stu-id="d269a-117">**Example of Air Tap - Used to show how to select objects that are far away**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="d269a-118">![exemple de déplacement](images/HandCoach/Move.gif)</span><span class="sxs-lookup"><span data-stu-id="d269a-118">![Example of Move](images/HandCoach/Move.gif)</span></span><br>
       <span data-ttu-id="d269a-119">**Exemple de déplacement d’un objet dans l’espace utilisé pour montrer comment déplacer un hologramme dans l’espace**</span><span class="sxs-lookup"><span data-stu-id="d269a-119">**Example of Moving an object in space-Used to show how to move a hologram in space**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="d269a-120">![exemple de rotation](images/HandCoach/Rotate.gif)</span><span class="sxs-lookup"><span data-stu-id="d269a-120">![Example of Rotate](images/HandCoach/Rotate.gif)</span></span><br>
       <span data-ttu-id="d269a-121">**Exemple de Rotate-utilisé pour montrer comment faire pivoter des hologrammes ou des objets**</span><span class="sxs-lookup"><span data-stu-id="d269a-121">**Example of Rotate-Used to show how to rotate holograms or objects**</span></span><br>
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
       <span data-ttu-id="d269a-122">![exemple de](images/HandCoach/Scale.gif) de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="d269a-122">![Example of Scale](images/HandCoach/Scale.gif)</span></span><br>
       <span data-ttu-id="d269a-123">**Exemple de mise à l’échelle : utilisé pour montrer comment manipuler les hologrammes pour qu’ils soient plus grands ou plus petits**</span><span class="sxs-lookup"><span data-stu-id="d269a-123">**Example of Scale- Used to show how to manipulate holograms to be bigger or smaller**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="d269a-124">![exemple de](images/HandCoach/PalmUp.gif) de palmier</span><span class="sxs-lookup"><span data-stu-id="d269a-124">![Example of Palm Up](images/HandCoach/PalmUp.gif)</span></span><br>
        <span data-ttu-id="d269a-125">**Exemple de Palm up – utilisation suggérée pour afficher les menus de la main**</span><span class="sxs-lookup"><span data-stu-id="d269a-125">**Example of Palm up – Suggested use, to bring up hand menus**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="d269a-126">![exemple de HandFlip](images/HandCoach/HandFlip.gif)</span><span class="sxs-lookup"><span data-stu-id="d269a-126">![Example of HandFlip](images/HandCoach/HandFlip.gif)</span></span><br>
       <span data-ttu-id="d269a-127">**Tour de main : un autre moyen d’afficher des menus manuels**</span><span class="sxs-lookup"><span data-stu-id="d269a-127">**Exmaple of Hand Flip – Another way to bring up Hand Menus**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="d269a-128">![exemple de défilement](images/HandCoach/Scoll.gif)</span><span class="sxs-lookup"><span data-stu-id="d269a-128">![Example of Scroll](images/HandCoach/Scoll.gif)</span></span><br>
       <span data-ttu-id="d269a-129">**Exemple de défilement : utilisé pour faire défiler une liste ou un document long**</span><span class="sxs-lookup"><span data-stu-id="d269a-129">**Example of Scroll – Used for scrolling a list or a long document**</span></span><br>
    :::column-end:::
:::row-end:::

## <a name="design-concepts"></a><span data-ttu-id="d269a-130">Concepts de conception</span><span class="sxs-lookup"><span data-stu-id="d269a-130">Design concepts</span></span>

<span data-ttu-id="d269a-131">Pour Hololens2, nous avons conçu des interactions de handles basées sur les gestes instinctual et Natural main.</span><span class="sxs-lookup"><span data-stu-id="d269a-131">For Hololens2, we designed out hand interactions based on instinctual and natural hand gestures.</span></span> <span data-ttu-id="d269a-132">Nous pensons que ceux-ci sont intuitifs pour la plupart des utilisateurs et n’ont donc pas créé de moments d’apprentissage de mouvement dédiés.</span><span class="sxs-lookup"><span data-stu-id="d269a-132">We believe these to be intuitive to most users and thus did not create dedicated gesture learning moments.</span></span> <span data-ttu-id="d269a-133">Au lieu de cela, nous avons créé le coach pour aider les utilisateurs qui peuvent être bloqués ou qui ne sont pas familiarisés avec l’interaction avec les hologrammes en savoir plus sur ces gestes.</span><span class="sxs-lookup"><span data-stu-id="d269a-133">Instead, we created the hand coach to help users who might get stuck or are unfamiliar with interacting with holograms learn about these gestures.</span></span> <span data-ttu-id="d269a-134">Sans un moment d’apprentissage, nous avons pensé que les utilisateurs indiquent comment effectuer une action en montrant qu’il s’agit de la meilleure option.</span><span class="sxs-lookup"><span data-stu-id="d269a-134">Without a learning moment, we felt that showing users how to perform an action by demonstrating it would be the best option.</span></span> <span data-ttu-id="d269a-135">Dans nos études, nous avons découvert que les utilisateurs étaient en mesure de déterminer le geste, mais ont besoin d’un peu de conseils.</span><span class="sxs-lookup"><span data-stu-id="d269a-135">In our studies, we found that users were able to figure out the gesture but needed a little guidance.</span></span> <span data-ttu-id="d269a-136">Si nous détectons qu’un utilisateur n’interagit pas avec un objet pendant un certain laps de temps, un autocar manuel sera déclenché pour illustrer la main correcte et le positionnement des doigts.</span><span class="sxs-lookup"><span data-stu-id="d269a-136">If we detect that a user does not interact with an object for a period, a Hand Coach would be triggered demonstrating the correct hand and finger placement.</span></span> 

### <a name="intuitive"></a><span data-ttu-id="d269a-137">Peu</span><span class="sxs-lookup"><span data-stu-id="d269a-137">Intuitive</span></span>

<span data-ttu-id="d269a-138">Quand vous animez des mains, cela doit être évident et shoudn’t provoquer des confusions.</span><span class="sxs-lookup"><span data-stu-id="d269a-138">When animating hands, it should be obvious and shoudn't cause any confusion.</span></span> <span data-ttu-id="d269a-139">L’animation des mains est une représentation du geste que vous essayez de évoquer à l’utilisateur pour comprendre son rôle.</span><span class="sxs-lookup"><span data-stu-id="d269a-139">The animation of the hands is a representation of the gesture your trying to evoke to the user to understand it's purpose.</span></span> 

<span data-ttu-id="d269a-140">Par exemple, si vous souhaitez qu’un utilisateur appuie sur un bouton, une main appuyant sur un bouton est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="d269a-140">For example, if you wish a user to press a button, a hand pressing a button would be triggered.</span></span>

<span data-ttu-id="d269a-141">Exemple de ![: main près TAP](images/HandCoach/NearSelect_unity.gif)</span><span class="sxs-lookup"><span data-stu-id="d269a-141">![Example: Hand Coach Near Tap](images/HandCoach/NearSelect_unity.gif)</span></span><br>
<span data-ttu-id="d269a-142">*Autocar montrant un témoin proche d’une gemme*</span><span class="sxs-lookup"><span data-stu-id="d269a-142">*Hand Coach demonstrating Near Tapping a Gem*</span></span>  

### <a name="hand-scale"></a><span data-ttu-id="d269a-143">Mise à l’échelle manuelle</span><span class="sxs-lookup"><span data-stu-id="d269a-143">Hand scale</span></span>

<span data-ttu-id="d269a-144">Nous avons testé différentes tailles de main avec les menus de l’interface utilisateur et j’ai pensé que si la main était vraie, elle donnait une menaçant, mais si elle était trop petite, il était difficile de voir et de comprendre le geste.</span><span class="sxs-lookup"><span data-stu-id="d269a-144">We tested various hand sizes with the UI menus and felt that if the hands were true to size, it gave a menacing feeling but if they were too small then it was hard to see and understand the gesture.</span></span> 

<span data-ttu-id="d269a-145">**Voix et mains**</span><span class="sxs-lookup"><span data-stu-id="d269a-145">**Voice over and hands**</span></span>

<span data-ttu-id="d269a-146">Ne vous attendez pas à ce que les utilisateurs puissent écouter un ensemble d’instructions via la voix et regarder différentes instructions via la main.</span><span class="sxs-lookup"><span data-stu-id="d269a-146">Don’t expect users can listen to one set of instructions via voice over and watch different instructions via Hand Coach.</span></span> <span data-ttu-id="d269a-147">Séquencez vos instructions pour aider les utilisateurs à se concentrer sur leur attention et à réduire la surcharge sensorielle.</span><span class="sxs-lookup"><span data-stu-id="d269a-147">Sequence your instructions to help users focus versus compete for their attention to reduce sensory overload.</span></span>


## <a name="can-i-create-my-own"></a><span data-ttu-id="d269a-148">Puis-je créer mon propre ?</span><span class="sxs-lookup"><span data-stu-id="d269a-148">Can I create my own?</span></span>

<span data-ttu-id="d269a-149">Oui.</span><span class="sxs-lookup"><span data-stu-id="d269a-149">Yes!</span></span> <span data-ttu-id="d269a-150">Nous vous encourageons à créer votre propre geste unique pour votre jeu et à contribuer à la communauté !</span><span class="sxs-lookup"><span data-stu-id="d269a-150">We encourage you to create your own unique gesture for your game and contribute back to the community!</span></span>
<span data-ttu-id="d269a-151">Nous avons fourni un fichier maya d’une main qui peut être utilisée pour votre application et qui peut être téléchargée ici : <a href="files/HandCoach_MRTK.zip">télécharger HandCoach_MRTK. zip</a></span><span class="sxs-lookup"><span data-stu-id="d269a-151">We have provided a Maya file of a Rigged hand that can be used for your app which can be downloaded here: <a href="files/HandCoach_MRTK.zip"> Download HandCoach_MRTK.zip</a></span></span>

<span data-ttu-id="d269a-152">![exemple de mains animées dans Maya](images/HandCoach/MayaSelect_Gif.gif)</span><span class="sxs-lookup"><span data-stu-id="d269a-152">![Example of Animated Hands in Maya](images/HandCoach/MayaSelect_Gif.gif)</span></span><br>
<span data-ttu-id="d269a-153">*Exemple de la main animée d’une boîte dans Maya*</span><span class="sxs-lookup"><span data-stu-id="d269a-153">*Example of animated Hand Poking a box in Maya*</span></span>


<span data-ttu-id="d269a-154">**Outil de création recommandé**</span><span class="sxs-lookup"><span data-stu-id="d269a-154">**Recommended authoring tool**</span></span>

<span data-ttu-id="d269a-155">Parmi les artistes en 3D, beaucoup choisissent d’utiliser les [Maya de Autodesk qui peuvent lui-même utiliser HoloLens](https://www.youtube.com/watch?v=q0K3n0Gf8mA) pour transformer la façon dont les ressources sont créées.</span><span class="sxs-lookup"><span data-stu-id="d269a-155">Among 3D artists, many choose to use [Autodesk’s Maya which itself is able to use HoloLens](https://www.youtube.com/watch?v=q0K3n0Gf8mA) to transform the way assets are created.</span></span> <span data-ttu-id="d269a-156">Le fichier mains fourni est un fichier binaire Maya. il est donc recommandé d’utiliser Maya pour animer et exporter les mains.</span><span class="sxs-lookup"><span data-stu-id="d269a-156">The hands file provided is a Maya Binary File, so it is recommended to use Maya to animate and export the hands.</span></span> <span data-ttu-id="d269a-157">Si vous préférez utiliser un autre programme 3D, voici un <b>. FBX</b>: <a href="files/HandCoachMRTK_FBX.zip">Téléchargez HandCoachMRTK_FBX. zip</a> pour créer votre propre configuration de contrôleur.</span><span class="sxs-lookup"><span data-stu-id="d269a-157">If you prefer to use another 3D program, here is a <b>.FBX</b>: <a href="files/HandCoachMRTK_FBX.zip">           Download HandCoachMRTK_FBX.zip</a> to create your own controller setup.</span></span> 

<span data-ttu-id="d269a-158">Si vous utilisez le fichier. Maya téléchargeable fourni, il est recommandé de réduire les mains dans Unity à 0,6.</span><span class="sxs-lookup"><span data-stu-id="d269a-158">If using the downloadable maya Hand File provided, it is suggested to scale down the hands in unity to 0.6.</span></span>

<span data-ttu-id="d269a-159">Exemple de ![: une plate-forme de autocar dans Maya](images/HandCoach/MayaExample.png)</span><span class="sxs-lookup"><span data-stu-id="d269a-159">![Example: Hand Coach rig in Maya](images/HandCoach/MayaExample.png)</span></span><br>
<span data-ttu-id="d269a-160">*Mains*</span><span class="sxs-lookup"><span data-stu-id="d269a-160">*Rigged Hands*</span></span>

### <a name="technical-specs"></a><span data-ttu-id="d269a-161">Caractéristiques techniques</span><span class="sxs-lookup"><span data-stu-id="d269a-161">Technical Specs</span></span>

*   <span data-ttu-id="d269a-162">Deux fichiers droitier sont disponibles au format ASCII Maya</span><span class="sxs-lookup"><span data-stu-id="d269a-162">Two handed File is available in Maya Ascii format</span></span>
*    <span data-ttu-id="d269a-163">La partie droite et la main gauche sont disponibles au format binaire Maya</span><span class="sxs-lookup"><span data-stu-id="d269a-163">Right and Left Hand is available in Maya Binary format</span></span>
*   <span data-ttu-id="d269a-164">Définir votre fichier maya sur 24 ips</span><span class="sxs-lookup"><span data-stu-id="d269a-164">Set your Maya file to 24 FPS</span></span>
*   <span data-ttu-id="d269a-165">Dans le fichier, il y a une main gauche et une main droite qui peuvent être utilisées pour deux gestes droitiers ou à sens unique.</span><span class="sxs-lookup"><span data-stu-id="d269a-165">Within the file, there is a left and right hand which can be used for two handed or single-handed gestures.</span></span> <span data-ttu-id="d269a-166">La main droite est visible uniquement par défaut.</span><span class="sxs-lookup"><span data-stu-id="d269a-166">The right hand will only be visible by default.</span></span>
*   <span data-ttu-id="d269a-167">Il est recommandé de conserver une mémoire tampon d’environ 10 frames au début et à la fin pour les disparitions</span><span class="sxs-lookup"><span data-stu-id="d269a-167">It is suggested to leave a buffer of about 10 frames at the beginning and end for fades</span></span>
*   <span data-ttu-id="d269a-168">En cas d’animation d’un objet avec une cible spécifiée, il est recommandé d’animer une case par défaut ou une valeur null.</span><span class="sxs-lookup"><span data-stu-id="d269a-168">If animating a object with a specified target, its best practice to animate to a Default box or Null.</span></span>
*   <span data-ttu-id="d269a-169">Si la main anime un objet physique tel qu’une zone, il est recommandé de ne pas animer la translation dans Maya, mais d’en faire une animation dans Unity ou dans le code.</span><span class="sxs-lookup"><span data-stu-id="d269a-169">If the hand is animating a physical object such as a box, its best practice to not animate the translation in Maya but wait to animate it in Unity or in Code.</span></span>
*   <span data-ttu-id="d269a-170">L’animation visible doit être de 1,5 secondes pour que toutes les informations significatives soient transmises</span><span class="sxs-lookup"><span data-stu-id="d269a-170">Visible Animation should be 1.5 secs for any meaningful information to be conveyed</span></span>
*   <span data-ttu-id="d269a-171">Quand vous êtes satisfait de votre animation :</span><span class="sxs-lookup"><span data-stu-id="d269a-171">When you feel satisfied with your animation:</span></span>
    *   <span data-ttu-id="d269a-172">Sélectionner tous les joints et les images clés de cuisson</span><span class="sxs-lookup"><span data-stu-id="d269a-172">Select all joints and bake key frames</span></span>
    *   <span data-ttu-id="d269a-173">Supprimez les contrôleurs, sélectionnez les jointures et les maillages, puis exportez-les en tant que FBX</span><span class="sxs-lookup"><span data-stu-id="d269a-173">Delete the Controllers, Select the joints and mesh and export as an FBX</span></span>
    *  <span data-ttu-id="d269a-174">S’il existe plusieurs animations, vous pouvez utiliser l’exportateur de jeux intégré à Maya : https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2015/ENU/Maya/files/Game-Exporter-htm.html</span><span class="sxs-lookup"><span data-stu-id="d269a-174">If there are Multiple Animations, you can use Maya’s built in Game Exporter: https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2015/ENU/Maya/files/Game-Exporter-htm.html</span></span>

## <a name="exporting-from-maya"></a><span data-ttu-id="d269a-175">Exportation à partir de Maya</span><span class="sxs-lookup"><span data-stu-id="d269a-175">Exporting from Maya</span></span>

<span data-ttu-id="d269a-176">Une fois que vous êtes satisfait de votre animation</span><span class="sxs-lookup"><span data-stu-id="d269a-176">After you are satisfied with your animation</span></span>
* <span data-ttu-id="d269a-177">Sélectionner tous les jointures : sélectionnez > hiérarchie</span><span class="sxs-lookup"><span data-stu-id="d269a-177">Select all joints: Select > Hierarchy</span></span>

     ![Exemple : emplacement du menu](images/HandCoach/Hierarchy.png)<br>
* <span data-ttu-id="d269a-179">Intégrer votre animation : basculer vers l’animation > touche > animation de cuisson</span><span class="sxs-lookup"><span data-stu-id="d269a-179">Bake out your animation: Switch to Animation > Key > Bake Animation</span></span>

     ![Exemple : emplacement du menu](images/HandCoach/BakeAnimation.png)<br>
* <span data-ttu-id="d269a-181">Supprimer la plate-forme de contrôleur : > MainR_Grp ou MainL_Grp</span><span class="sxs-lookup"><span data-stu-id="d269a-181">Delete the Controller Rig: Outliner > MainR_Grp or MainL_Grp</span></span>

     ![Exemple : emplacement du menu](images/HandCoach/ControllerRig.png)<br>

* <span data-ttu-id="d269a-183">Exporter en tant que FBX : sélectionnez JNT + maille : fichier > Exporter la sélection (case d’option) > Exporter la sélection</span><span class="sxs-lookup"><span data-stu-id="d269a-183">Export as FBX: Select JNT + Mesh: File > Export Selection (option box) > Export Selection</span></span>

     ![Exemple : emplacement du menu](images/HandCoach/OptionBox.png)<br>

     ![Exemple : emplacement du menu](images/HandCoach/SelectionExport.png)<br>

     ![Exemple : emplacement du menu](images/HandCoach/FBXSelection.png)<br>


 <span data-ttu-id="d269a-187">Lorsque vous exportez en tant que FBX et que vous mettez sous Unity, mettez à l’échelle les mains jusqu’à 0,6.</span><span class="sxs-lookup"><span data-stu-id="d269a-187">When exporting as a FBX and brought into Unity, scale the hands down to 0.6.</span></span> <span data-ttu-id="d269a-188">Nous avons découvert que ce fut parfait pour l’affichage des mains.</span><span class="sxs-lookup"><span data-stu-id="d269a-188">We found that this was perfect balance for displaying the hands.</span></span> 

<span data-ttu-id="d269a-189">Exemple de ![: paramètres Unity](images/HandCoach/HandHintScale.png)</span><span class="sxs-lookup"><span data-stu-id="d269a-189">![Example: Unity Settings](images/HandCoach/HandHintScale.png)</span></span><br>
<span data-ttu-id="d269a-190">*Paramètres Unity pour HandCoach_R Prefab trouvés dans MRTK*</span><span class="sxs-lookup"><span data-stu-id="d269a-190">*Unity Settings for HandCoach_R prefab found in MRTK*</span></span>


## <a name="implementing-hands-into-your-unity-project"></a><span data-ttu-id="d269a-191">Implémentation des mains dans votre projet Unity</span><span class="sxs-lookup"><span data-stu-id="d269a-191">Implementing Hands into your Unity project</span></span>

### <a name="best-practices"></a><span data-ttu-id="d269a-192">Bonnes pratiques</span><span class="sxs-lookup"><span data-stu-id="d269a-192">Best practices</span></span>
*    <span data-ttu-id="d269a-193">Il est suggéré de réduire les mains d’Unity à 0,6</span><span class="sxs-lookup"><span data-stu-id="d269a-193">It is suggested to scale down the hands in unity to 0.6</span></span>
*   <span data-ttu-id="d269a-194">Les mains doivent être jouées deux fois et si elles ne sont pas terminées, puis en boucle jusqu’à ce que le geste soit terminé.</span><span class="sxs-lookup"><span data-stu-id="d269a-194">Hands should be played twice and if not completed then continuously looped until gesture is completed.</span></span> <span data-ttu-id="d269a-195">Les mains doivent être bouclées deux fois pour garantir que l’utilisateur avait le temps de s’inscrire et de voir le mouvement.</span><span class="sxs-lookup"><span data-stu-id="d269a-195">The hands should be looped twice to ensure the user had time to register and see the gesture.</span></span> <span data-ttu-id="d269a-196">Les mains doivent apparaître et disparaître entre les boucles.</span><span class="sxs-lookup"><span data-stu-id="d269a-196">The hands should fade in and out between loops.</span></span> 
 *  <span data-ttu-id="d269a-197">Si les mains de l’utilisateur sont visibles par les appareils photo HL2, mais que les utilisateurs n’effectuent pas l’interaction dont ils ont besoin, les mains s’affichent au bout de 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="d269a-197">If user’s hands are visible by HL2 cameras but users are not doing the interaction needed of them the hands will appear after 10 seconds.</span></span>
*   <span data-ttu-id="d269a-198">Si les mains de l’utilisateur ne sont pas visibles par les appareils photo HL2, les mains s’affichent au bout de 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="d269a-198">If user’s hands are NOT visible by HL2 cameras, the hands will appear after 5 seconds.</span></span>  
*   <span data-ttu-id="d269a-199">Si les mains de l’utilisateur sont visibles par les appareils photo HL2 au milieu de l’animation, l’animation se termine et disparaît en fondu.</span><span class="sxs-lookup"><span data-stu-id="d269a-199">If user’s hands are visibly tracked by HL2 cameras in the middle of the animation, the animation will complete and fade out.</span></span>
*   <span data-ttu-id="d269a-200">Si vous incluez la voix, nous suggérons qu’elle corresponde au geste de la main.</span><span class="sxs-lookup"><span data-stu-id="d269a-200">If you are including voice over, we suggest that it corresponds to the gesture of the hand.</span></span>
*   <span data-ttu-id="d269a-201">Si vous avez enseigné les mains au moins une fois, répétez uniquement le mouvement si son a détecté que l’utilisateur est bloqué.</span><span class="sxs-lookup"><span data-stu-id="d269a-201">If you have taught the hands at least once, only repeat the gesture if its detected that the user is stuck.</span></span>
*   <span data-ttu-id="d269a-202">Si les positions de doigt/main spécifiques sont critiques, assurez-vous que les utilisateurs peuvent voir clairement ces nuances dans l’animation.</span><span class="sxs-lookup"><span data-stu-id="d269a-202">If specific finger/hand positions are critical, ensure users can clearly see these nuances in the animation.</span></span> <span data-ttu-id="d269a-203">Essayez droite les mains pour que les parties les plus importantes soient clairement visibles.</span><span class="sxs-lookup"><span data-stu-id="d269a-203">Try angling the hands so the most important parts are clearly visible.</span></span> 
* <span data-ttu-id="d269a-204">Si vous constatez une distorsion des mains, vous devez accéder aux paramètres de qualité de Unity pour augmenter la quantité d’os.</span><span class="sxs-lookup"><span data-stu-id="d269a-204">If you notice distortion on the hands, you need to go to Unity's Quality settings increase the amount of bones.</span></span> 
 <span data-ttu-id="d269a-205">Accédez à modifier > paramètres du projet > qualité > autres > poids de la fusion.</span><span class="sxs-lookup"><span data-stu-id="d269a-205">Go to Unity's Edit > Project Settings > Quality > Other > Blend Weights.</span></span> <span data-ttu-id="d269a-206">Assurez-vous que « 4 segments » sont sélectionnés pour afficher des articulations lisses.</span><span class="sxs-lookup"><span data-stu-id="d269a-206">Make sure "4 bones" are selected to see Smooth Joints.</span></span> 

   ![Exemple : emplacement du menu](images/HandCoach/ProjectSettings.png)<br>





### <a name="what-to-avoid"></a><span data-ttu-id="d269a-208">Éléments à éviter</span><span class="sxs-lookup"><span data-stu-id="d269a-208">What to avoid</span></span>
* <span data-ttu-id="d269a-209">Mise à l’échelle des mains trop grandes</span><span class="sxs-lookup"><span data-stu-id="d269a-209">Scaling the Hands too large</span></span>
* <span data-ttu-id="d269a-210">le placement des mains trop près de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d269a-210">placing the Hands too close to the user</span></span>
* <span data-ttu-id="d269a-211">Les mains ne doivent être enseignées qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="d269a-211">Hands should only be taught once.</span></span> <span data-ttu-id="d269a-212">L’apprentissage peut entraîner des confusions et des opérations</span><span class="sxs-lookup"><span data-stu-id="d269a-212">Over teaching can cause confusion and messiness</span></span>
*   <span data-ttu-id="d269a-213">En le plaçant dans Unity, téléchargez la dernière version de MRTK ici : https://github.com/microsoft/MixedRealityToolkit-Unity</span><span class="sxs-lookup"><span data-stu-id="d269a-213">Bringing it into Unity, please download the latest MRTK  here: https://github.com/microsoft/MixedRealityToolkit-Unity</span></span>
    *   <span data-ttu-id="d269a-214">Matériel : Teaching_Hand2</span><span class="sxs-lookup"><span data-stu-id="d269a-214">Material: Teaching_Hand2</span></span>
    *   <span data-ttu-id="d269a-215">Scripts : consultez MRTK Guidelines for <a href= "https://github.com/MixedRealityToolkit-Unity/blob/'HandCoachUX'/Documentation/README_HandCoach.md">MRTK main coach</a></span><span class="sxs-lookup"><span data-stu-id="d269a-215">Scripts: Refer to MRTK guidelines for <a href= "https://github.com/MixedRealityToolkit-Unity/blob/'HandCoachUX'/Documentation/README_HandCoach.md"> MRTK hand Coach </a></span></span>
    *   <span data-ttu-id="d269a-216">Paramètre par projet</span><span class="sxs-lookup"><span data-stu-id="d269a-216">Per- project setting</span></span>
        *   <span data-ttu-id="d269a-217">Scène définie sur UWP : l’instruction se trouve dans le [projet configurer Unity](Configure-Unity-Project.md) pour Windows Mixed Reality</span><span class="sxs-lookup"><span data-stu-id="d269a-217">Scene set to UWP: Instruction can be found on the [Configure Unity Project](Configure-Unity-Project.md) for Windows Mixed Reality</span></span>

## <a name="see-also"></a><span data-ttu-id="d269a-218">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d269a-218">See also</span></span>
* [<span data-ttu-id="d269a-219">Interaction-notions de base</span><span class="sxs-lookup"><span data-stu-id="d269a-219">Interaction-fundamentals</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="d269a-220">Processus de création de ressources</span><span class="sxs-lookup"><span data-stu-id="d269a-220">Asset Creation Process</span></span>](asset-creation-process.md)
* [<span data-ttu-id="d269a-221">Mouvements</span><span class="sxs-lookup"><span data-stu-id="d269a-221">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="d269a-222">Installer les outils</span><span class="sxs-lookup"><span data-stu-id="d269a-222">Install the Tools</span></span>](install-the-tools.md)
* [<span data-ttu-id="d269a-223">Configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="d269a-223">Configure Unity Project</span></span>](Configure-Unity-Project.md)
* [<span data-ttu-id="d269a-224">Vue d’ensemble du développement Unity</span><span class="sxs-lookup"><span data-stu-id="d269a-224">Unity development overview</span></span>](unity-development-overview.md)
* [<span data-ttu-id="d269a-225">MRTK 101</span><span class="sxs-lookup"><span data-stu-id="d269a-225">MRTK 101</span></span>](mrtk-101.md)
