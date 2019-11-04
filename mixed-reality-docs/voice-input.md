---
title: Entrée vocale
description: L’entrée vocale est une entrée de base pour HoloLens et les casques immersifs immersifs de Windows Mixed Reality. La voix peut être utilisée pour les commandes, la dictée, Cortana et bien plus encore.
author: Hak0n
ms.author: hakons
ms.date: 10/03/2019
ms.topic: article
keywords: GGv, voix, Cortana, discours, entrée
ms.openlocfilehash: 1b0a57ad680b7f779201e99dea24bfe746820c44
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437149"
---
# <a name="voice-input"></a><span data-ttu-id="6fe84-105">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="6fe84-105">Voice input</span></span>

<span data-ttu-id="6fe84-106">La voix est l’un des principaux types d’entrée sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="6fe84-106">Voice is one of the key forms of input on HoloLens.</span></span> <span data-ttu-id="6fe84-107">Elle vous permet de directement commander un hologramme sans avoir à utiliser des gestes à la [main](gaze-and-commit.md#composite-gestures).</span><span class="sxs-lookup"><span data-stu-id="6fe84-107">It allows you to directly command a hologram without having to use [hand gestures](gaze-and-commit.md#composite-gestures).</span></span> <span data-ttu-id="6fe84-108">L’entrée vocale peut être un moyen naturel de communiquer votre intention.</span><span class="sxs-lookup"><span data-stu-id="6fe84-108">Voice input can be a natural way to communicate your intent.</span></span> <span data-ttu-id="6fe84-109">La voix est particulièrement intéressante pour traverser les interfaces complexes, car elle permet aux utilisateurs de couper les menus imbriqués avec une commande.</span><span class="sxs-lookup"><span data-stu-id="6fe84-109">Voice is especially good at traversing complex interfaces, because it lets users cut through nested menus with one command.</span></span>

<span data-ttu-id="6fe84-110">L’entrée vocale est alimentée par le [moteur](https://msdn.microsoft.com/library/windows/apps/mt185615.aspx) qui prend en charge la reconnaissance vocale dans toutes les autres _applications universelles Windows_.</span><span class="sxs-lookup"><span data-stu-id="6fe84-110">Voice input is powered by the [same engine](https://msdn.microsoft.com/library/windows/apps/mt185615.aspx) that supports speech in all other _Universal Windows Apps_.</span></span> <span data-ttu-id="6fe84-111">Sur HoloLens, la reconnaissance vocale fonctionne toujours dans la langue d’affichage Windows configurée dans paramètres.</span><span class="sxs-lookup"><span data-stu-id="6fe84-111">On HoloLens, speech recognition will always function in the Windows display language configured in Settings.</span></span> 

<br>

## <a name="voice-and-gaze"></a><span data-ttu-id="6fe84-112">Voix et regard</span><span class="sxs-lookup"><span data-stu-id="6fe84-112">Voice and gaze</span></span>

<span data-ttu-id="6fe84-113">Lorsque vous utilisez des commandes vocales (tête ou œil), le point de regard est généralement utilisé comme mécanisme de ciblage, que ce soit avec un curseur (« Select ») ou pour canaliser implicitement votre commande vers une application que vous examinez.</span><span class="sxs-lookup"><span data-stu-id="6fe84-113">When using voice commands, (head or eye) gaze is typically used as the targeting mechanism, whether with a cursor ("select") or to implicitly channel your command to an application that you are looking at.</span></span> <span data-ttu-id="6fe84-114">Pour ce faire, il n’est même pas nécessaire de faire apparaître un curseur pointant vers le regard _(« Regardez-le, dites-le »)_ .</span><span class="sxs-lookup"><span data-stu-id="6fe84-114">For this, it may not even be required to show any gaze cursor _("see it, say it")_.</span></span> <span data-ttu-id="6fe84-115">Bien entendu, certaines commandes vocales ne nécessitent pas de cible, telles que « aller à démarrer » ou « Hey Cortana ».</span><span class="sxs-lookup"><span data-stu-id="6fe84-115">Of course, some voice commands don't require a target at all, such as "go to start" or "Hey Cortana."</span></span>

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/eHMkOpNUtR8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## <a name="device-support"></a><span data-ttu-id="6fe84-116">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="6fe84-116">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="6fe84-117"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="6fe84-117"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="6fe84-118"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="6fe84-118"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="6fe84-119"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="6fe84-119"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="6fe84-120"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="6fe84-120"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="6fe84-121">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="6fe84-121">Voice input</span></span></td>
        <td><span data-ttu-id="6fe84-122">✔️</span><span class="sxs-lookup"><span data-stu-id="6fe84-122">✔️</span></span></td>
        <td><span data-ttu-id="6fe84-123">✔️</span><span class="sxs-lookup"><span data-stu-id="6fe84-123">✔️</span></span></td>
        <td><span data-ttu-id="6fe84-124">✔️ (avec microphone)</span><span class="sxs-lookup"><span data-stu-id="6fe84-124">✔️ (with microphone)</span></span></td>
    </tr>
</table>

## <a name="the-select-command"></a><span data-ttu-id="6fe84-125">Commande « sélectionner »</span><span class="sxs-lookup"><span data-stu-id="6fe84-125">The "select" command</span></span>

<span data-ttu-id="6fe84-126">**HoloLens (1re génération)**</span><span class="sxs-lookup"><span data-stu-id="6fe84-126">**HoloLens (1st gen)**</span></span>

<span data-ttu-id="6fe84-127">Même sans ajouter spécifiquement la prise en charge vocale à votre application, vos utilisateurs peuvent activer des hologrammes simplement en disant à la commande System Voice « Select ».</span><span class="sxs-lookup"><span data-stu-id="6fe84-127">Even without specifically adding voice support to your app, your users can activate holograms simply by saying the system voice command "select".</span></span> <span data-ttu-id="6fe84-128">Cela se comporte de la même façon qu’un [TAP Air](gaze-and-commit.md#composite-gestures) sur HoloLens, en appuyant sur le bouton de sélection sur l’interactiveur [hololens](hardware-accessories.md#hololens-clicker)ou en appuyant sur le déclencheur sur un [contrôleur de mouvement Windows Mixed Reality](motion-controllers.md).</span><span class="sxs-lookup"><span data-stu-id="6fe84-128">This behaves the same as an [air tap](gaze-and-commit.md#composite-gestures) on HoloLens, pressing the select button on the [HoloLens clicker](hardware-accessories.md#hololens-clicker), or pressing the trigger on a [Windows Mixed Reality motion controller](motion-controllers.md).</span></span> <span data-ttu-id="6fe84-129">Vous entendez un son et vous voyez une info-bulle avec « sélectionner » qui s’affiche comme confirmation.</span><span class="sxs-lookup"><span data-stu-id="6fe84-129">You will hear a sound and see a tooltip with "select" appear as confirmation.</span></span> <span data-ttu-id="6fe84-130">« SELECT » est activé par un algorithme de détection de mot-clé à faible consommation d’énergie. il est donc toujours disponible pour vous, à tout moment, avec un impact minimal sur la durée de vie de la batterie, même avec vos mains.</span><span class="sxs-lookup"><span data-stu-id="6fe84-130">"Select" is enabled by a low power keyword detection algorithm so it is always available for you to say at any time with minimal battery life impact, even with your hands at your side.</span></span>

<br>

---

:::row:::
    :::column:::
        <span data-ttu-id="6fe84-131">**HoloLens 2**</span><span class="sxs-lookup"><span data-stu-id="6fe84-131">**HoloLens 2**</span></span><br><br>
        <span data-ttu-id="6fe84-132">Pour utiliser la commande vocale « SELECT » dans HoloLens 2, vous devez d’abord afficher le curseur en regard à utiliser comme pointeur.</span><span class="sxs-lookup"><span data-stu-id="6fe84-132">In order to use the "select" voice command in HoloLens 2, you first need to bring up the gaze cursor to use as a pointer.</span></span> <span data-ttu-id="6fe84-133">La commande pour l’afficher est facile à mémoriser, par exemple « Select ».</span><span class="sxs-lookup"><span data-stu-id="6fe84-133">The command to bring it up is easy to remember -- just say, "select".</span></span><br><br>
        <span data-ttu-id="6fe84-134">Pour quitter le mode, il vous suffit de réutiliser vos mains, soit par air, en appuyant sur un bouton avec vos doigts, soit en utilisant le mouvement du système.</span><span class="sxs-lookup"><span data-stu-id="6fe84-134">To exit the mode, simply use your hands again, either by air tapping, approaching a button with your fingers, or using the system gesture.</span></span><br>
        <br>
        <span data-ttu-id="6fe84-135">*Image : dites « sélectionner » pour utiliser la commande vocale pour la sélection*</span><span class="sxs-lookup"><span data-stu-id="6fe84-135">*Image: Say "select" to use the voice command for selection*</span></span>
    :::column-end:::
        :::column:::
       ![Un utilisateur peut indiquer « sélectionner » pour utiliser la commande vocale pour une sélection.](images/kma-voice-select-00170.jpg)<br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="hey-cortana"></a><span data-ttu-id="6fe84-137">Hey Cortana</span><span class="sxs-lookup"><span data-stu-id="6fe84-137">Hey Cortana</span></span>

<span data-ttu-id="6fe84-138">Vous pouvez également indiquer « Hey Cortana » pour afficher Cortana à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6fe84-138">You can also say "Hey Cortana" to bring up Cortana at anytime.</span></span> <span data-ttu-id="6fe84-139">Vous n’avez pas besoin d’attendre qu’il apparaisse pour continuer à poser votre question ou de lui donner une instruction. par exemple, essayez de dire « Bonjour Cortana, qu’est-ce que la météo ? »</span><span class="sxs-lookup"><span data-stu-id="6fe84-139">You don't have to wait for her to appear to continue asking her your question or giving her an instruction - for example, try saying "Hey Cortana, what's the weather?"</span></span> <span data-ttu-id="6fe84-140">comme une seule phrase.</span><span class="sxs-lookup"><span data-stu-id="6fe84-140">as a single sentence.</span></span> <span data-ttu-id="6fe84-141">Pour plus d’informations sur Cortana et ce que vous pouvez faire, demandez-lui simplement !</span><span class="sxs-lookup"><span data-stu-id="6fe84-141">For more information about Cortana and what you can do, simply ask her!</span></span> <span data-ttu-id="6fe84-142">Dites « Hey Cortana, que puis-je faire ? »</span><span class="sxs-lookup"><span data-stu-id="6fe84-142">Say "Hey Cortana, what can I say?"</span></span> <span data-ttu-id="6fe84-143">et elle extrait une liste de commandes de travail et suggérées.</span><span class="sxs-lookup"><span data-stu-id="6fe84-143">and she'll pull up a list of working and suggested commands.</span></span> <span data-ttu-id="6fe84-144">Si vous êtes déjà dans l’application Cortana, vous pouvez également cliquer sur le **?**</span><span class="sxs-lookup"><span data-stu-id="6fe84-144">If you're already in the Cortana app you can also click the **?**</span></span> <span data-ttu-id="6fe84-145">sur la barre latérale pour extraire le même menu.</span><span class="sxs-lookup"><span data-stu-id="6fe84-145">icon on the sidebar to pull up this same menu.</span></span>

<span data-ttu-id="6fe84-146">**Commandes spécifiques à HoloLens**</span><span class="sxs-lookup"><span data-stu-id="6fe84-146">**HoloLens-specific commands**</span></span>
* <span data-ttu-id="6fe84-147">Qu’est-ce que je dis ?</span><span class="sxs-lookup"><span data-stu-id="6fe84-147">"What can I say?"</span></span>
* <span data-ttu-id="6fe84-148">« Aller au début »-au lieu de [fleuri](system-gesture.md#bloom) pour accéder au [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu)</span><span class="sxs-lookup"><span data-stu-id="6fe84-148">"Go to Start" - instead of [bloom](system-gesture.md#bloom) to get to [Start Menu](navigating-the-windows-mixed-reality-home.md#start-menu)</span></span>
* <span data-ttu-id="6fe84-149">« Launch <app>»</span><span class="sxs-lookup"><span data-stu-id="6fe84-149">"Launch <app>"</span></span>
* <span data-ttu-id="6fe84-150">« Déplacer <app> ici »</span><span class="sxs-lookup"><span data-stu-id="6fe84-150">"Move <app> here"</span></span>
* <span data-ttu-id="6fe84-151">« Prendre une photo »</span><span class="sxs-lookup"><span data-stu-id="6fe84-151">"Take a picture"</span></span>
* <span data-ttu-id="6fe84-152">« Démarrer l’enregistrement »</span><span class="sxs-lookup"><span data-stu-id="6fe84-152">"Start recording"</span></span>
* <span data-ttu-id="6fe84-153">« Arrêter l’enregistrement »</span><span class="sxs-lookup"><span data-stu-id="6fe84-153">"Stop recording"</span></span>
* <span data-ttu-id="6fe84-154">« Augmenter la luminosité »</span><span class="sxs-lookup"><span data-stu-id="6fe84-154">"Increase the brightness"</span></span>
* <span data-ttu-id="6fe84-155">« Réduire la luminosité »</span><span class="sxs-lookup"><span data-stu-id="6fe84-155">"Decrease the brightness"</span></span>
* <span data-ttu-id="6fe84-156">« Augmenter le volume »</span><span class="sxs-lookup"><span data-stu-id="6fe84-156">"Increase the volume"</span></span>
* <span data-ttu-id="6fe84-157">« Réduire le volume »</span><span class="sxs-lookup"><span data-stu-id="6fe84-157">"Decrease the volume"</span></span>
* <span data-ttu-id="6fe84-158">« Muet » ou « muet »</span><span class="sxs-lookup"><span data-stu-id="6fe84-158">"Mute" or "Unmute"</span></span>
* <span data-ttu-id="6fe84-159">« Arrêter l’appareil »</span><span class="sxs-lookup"><span data-stu-id="6fe84-159">"Shut down the device"</span></span>
* <span data-ttu-id="6fe84-160">« Redémarrer l’appareil »</span><span class="sxs-lookup"><span data-stu-id="6fe84-160">"Restart the device"</span></span>
* <span data-ttu-id="6fe84-161">« Go to Sleep »</span><span class="sxs-lookup"><span data-stu-id="6fe84-161">"Go to sleep"</span></span>
* <span data-ttu-id="6fe84-162">« Quel est l’heure ? »</span><span class="sxs-lookup"><span data-stu-id="6fe84-162">"What time is it?"</span></span>
* <span data-ttu-id="6fe84-163">« Quelle batterie ai-je laissée ? »</span><span class="sxs-lookup"><span data-stu-id="6fe84-163">"How much battery do I have left?"</span></span>



<br>

---

:::row:::
    :::column:::
        ## <a name="see-it-say-itbr"></a><span data-ttu-id="6fe84-164">« Regardez-le, dites-le »</span><span class="sxs-lookup"><span data-stu-id="6fe84-164">"See It, Say It"</span></span><br>
        <span data-ttu-id="6fe84-165">HoloLens a un modèle de « voir », par exemple, le modèle d’entrée vocale, où les étiquettes sur les boutons indiquent aux utilisateurs les commandes vocales qu’ils peuvent également prononcer.</span><span class="sxs-lookup"><span data-stu-id="6fe84-165">HoloLens has a "see it, say it" model for voice input, where labels on buttons tell users what voice commands they can say as well.</span></span> <span data-ttu-id="6fe84-166">Par exemple, lors de la consultation d’une fenêtre d’application dans HoloLens (1re génération), un utilisateur peut prononcer la commande « Adjust » qui s’affiche dans la barre de l’application pour ajuster la position de l’application dans le monde.</span><span class="sxs-lookup"><span data-stu-id="6fe84-166">For example, when looking at an app window in HoloLens (1st gen), a user can say the "Adjust" command which they see in the App bar to adjust the position of the app in the world.</span></span><br>
        <br>
        <span data-ttu-id="6fe84-167">*Image : un utilisateur peut prononcer la commande « Adjust » qui s’affiche dans la barre de l’application pour ajuster la position de l’application*</span><span class="sxs-lookup"><span data-stu-id="6fe84-167">*Image: A user can say the "Adjust" command which they see in the App bar to adjust the position of the app*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="6fe84-168">espace de ![](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="6fe84-168">![space](images/spacer-20x582.png)</span></span><br>
        <span data-ttu-id="6fe84-169">![lors de la consultation d’une fenêtre d’application ou d’un hologramme, un utilisateur peut prononcer la commande « Adjust » qui s’affiche dans la barre de l’application pour ajuster la position de l’application dans le monde](images/microphone-600px.png)</span><span class="sxs-lookup"><span data-stu-id="6fe84-169">![When looking at an app window or hologram, a user can say the "Adjust" command which they see in the App bar to adjust the position of the app in the world](images/microphone-600px.png)</span></span><br>
    :::column-end:::
:::row-end:::


<br>



:::row:::
    :::column:::
        <span data-ttu-id="6fe84-170">Lorsque les applications suivent cette règle, les utilisateurs peuvent facilement comprendre ce qu’il faut savoir pour contrôler le système.</span><span class="sxs-lookup"><span data-stu-id="6fe84-170">When apps follow this rule, users can easily understand what to say to control the system.</span></span> <span data-ttu-id="6fe84-171">Pour renforcer ce point, pendant que Gazing a un bouton dans HoloLens (1ère génération), vous verrez une info-bulle « de la voix » qui apparaît après une seconde si le bouton est activé pour la voix et affiche la commande pour dire à « appuyez ».</span><span class="sxs-lookup"><span data-stu-id="6fe84-171">To reinforce this, while gazing at a button in HoloLens (1st gen), you will see a "voice dwell" tooltip that comes up after a second if the button is voice-enabled and displays the command to speak to "press" it.</span></span> <span data-ttu-id="6fe84-172">Pour afficher les info-bulles vocales dans HoloLens 2, affichez le curseur vocal en disant « sélectionner » ou « que puis-je dire » (Voir l’image).</span><span class="sxs-lookup"><span data-stu-id="6fe84-172">To reveal voice tooltips in HoloLens 2, show the voice cursor by saying "select" or "What can I say" (See image).</span></span> <br>
        <br>
        <span data-ttu-id="6fe84-173">*Image : les commandes « voir » s’affichent sous les boutons*</span><span class="sxs-lookup"><span data-stu-id="6fe84-173">*Image: "See it, say it" commands appear below the buttons*</span></span>
    :::column-end:::
        :::column:::
       ![Voyez-le, disons que les commandes s’affichent sous les boutons](images/voice-seeitsayit-600px.png)<br><br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="voice-commands-for-fast-hologram-manipulation"></a><span data-ttu-id="6fe84-175">Commandes vocales pour une manipulation d’hologramme rapide</span><span class="sxs-lookup"><span data-stu-id="6fe84-175">Voice commands for fast hologram manipulation</span></span>

<span data-ttu-id="6fe84-176">Il existe un certain nombre de commandes vocales que vous pouvez prononcer Gazing sur un hologramme pour effectuer rapidement des tâches de manipulation.</span><span class="sxs-lookup"><span data-stu-id="6fe84-176">There are a number of voice commands you can say while gazing at a hologram to quickly perform manipulation tasks.</span></span> <span data-ttu-id="6fe84-177">Ces commandes vocales fonctionnent sur les fenêtres d’application, ainsi que sur les objets 3D que vous avez placés dans le monde.</span><span class="sxs-lookup"><span data-stu-id="6fe84-177">These voice commands work on app windows as well as 3D objects you have placed in the world.</span></span>

<span data-ttu-id="6fe84-178">**Commandes de manipulation d’hologramme**</span><span class="sxs-lookup"><span data-stu-id="6fe84-178">**Hologram manipulation commands**</span></span>
* <span data-ttu-id="6fe84-179">Me faire face</span><span class="sxs-lookup"><span data-stu-id="6fe84-179">Face me</span></span>
* <span data-ttu-id="6fe84-180">Plus grand | Enrichissement</span><span class="sxs-lookup"><span data-stu-id="6fe84-180">Bigger | Enhance</span></span>
* <span data-ttu-id="6fe84-181">Grande</span><span class="sxs-lookup"><span data-stu-id="6fe84-181">Smaller</span></span>

<span data-ttu-id="6fe84-182">Sur HoloLens 2, vous pouvez également créer des interactions plus naturelles en association avec un regard en œil qui fournit implicitement des informations contextuelles sur ce à quoi vous faites référence.</span><span class="sxs-lookup"><span data-stu-id="6fe84-182">On HoloLens 2, you can also create more natural interactions in combination with eye-gaze which implicitly provides contextual information about what you are referring to.</span></span> <span data-ttu-id="6fe84-183">Par exemple, vous pouvez simplement regarder un hologramme et indiquer « placer _ce_», puis passer à l’emplacement où vous souhaitez le placer et indiquer « sur _ce_point ».</span><span class="sxs-lookup"><span data-stu-id="6fe84-183">For example, you could simply look at a hologram and say "put _this_" and then look over where you want to place it and say "over _here_".</span></span>
<span data-ttu-id="6fe84-184">Ou bien, vous pouvez consulter un composant holographique sur une machine complexe et indiquer : « Donnez-moi plus d’informations à _ce_sujet ».</span><span class="sxs-lookup"><span data-stu-id="6fe84-184">Or you could look at a holographic part on a complex machine and say: "give me more information about _this_".</span></span>



## <a name="discovering-voice-commands"></a><span data-ttu-id="6fe84-185">Détection des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="6fe84-185">Discovering voice commands</span></span>

<span data-ttu-id="6fe84-186">Certaines commandes, telles que les commandes de manipulation rapide ci-dessus, peuvent être masquées.</span><span class="sxs-lookup"><span data-stu-id="6fe84-186">Some commands, like the commands for fast manipulation above, can be hidden.</span></span> <span data-ttu-id="6fe84-187">Pour en savoir plus sur les commandes que vous pouvez utiliser, pointez avec le regard sur un objet et dites « que puis-je prononcer ? ».</span><span class="sxs-lookup"><span data-stu-id="6fe84-187">To learn about what commands you can use, gaze at an object and say, "what can I say?".</span></span> <span data-ttu-id="6fe84-188">Une liste de commandes possibles s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6fe84-188">A list of possible commands pops up.</span></span> <span data-ttu-id="6fe84-189">Vous pouvez également utiliser le curseur point-tête pour rechercher et afficher les info-bulles vocales de chaque bouton devant vous.</span><span class="sxs-lookup"><span data-stu-id="6fe84-189">You can also use the head gaze cursor to look around and reveal the voice tooltips for each button in front of you.</span></span> 

<span data-ttu-id="6fe84-190">Si vous souhaitez obtenir la liste complète, dites « afficher toutes les commandes » à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6fe84-190">If you want a complete list, just say, "Show all commands" anytime.</span></span> 


## <a name="dictation"></a><span data-ttu-id="6fe84-191">Dictée</span><span class="sxs-lookup"><span data-stu-id="6fe84-191">Dictation</span></span>

<span data-ttu-id="6fe84-192">Plutôt que de taper avec des [robinets](gaze-and-commit.md#composite-gestures), la dictée vocale peut être plus efficace pour entrer du texte dans une application.</span><span class="sxs-lookup"><span data-stu-id="6fe84-192">Rather than typing with [air taps](gaze-and-commit.md#composite-gestures), voice dictation can be more efficient to enter text into an app.</span></span> <span data-ttu-id="6fe84-193">Cela peut accélérer l’entrée avec moins d’efforts pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fe84-193">This can greatly accelerate input with less effort for the user.</span></span>

<span data-ttu-id="6fe84-194">![la dictée vocale commence en sélectionnant le bouton microphone](images/micbuttonfordictation.png)</span><span class="sxs-lookup"><span data-stu-id="6fe84-194">![Voice dictation starts by selecting the microphone button](images/micbuttonfordictation.png)</span></span><br>
<span data-ttu-id="6fe84-195">*La dictée vocale commence en sélectionnant le bouton microphone sur le clavier.*</span><span class="sxs-lookup"><span data-stu-id="6fe84-195">*Voice dictation starts by selecting the microphone button on the keyboard*</span></span>

<span data-ttu-id="6fe84-196">À chaque fois que le clavier holographique est actif, vous pouvez basculer en mode dictée au lieu de taper.</span><span class="sxs-lookup"><span data-stu-id="6fe84-196">Any time the holographic keyboard is active, you can switch to dictation mode instead of typing.</span></span> <span data-ttu-id="6fe84-197">Sélectionnez le microphone sur le côté de la zone d’entrée de texte pour commencer.</span><span class="sxs-lookup"><span data-stu-id="6fe84-197">Select the microphone on the side of the text input box to get started.</span></span>


## <a name="adding-voice-commands-to-your-app"></a><span data-ttu-id="6fe84-198">Ajout de commandes vocales à votre application</span><span class="sxs-lookup"><span data-stu-id="6fe84-198">Adding voice commands to your app</span></span>

<span data-ttu-id="6fe84-199">Il est recommandé d’ajouter des commandes vocales à toutes les expériences que vous créez.</span><span class="sxs-lookup"><span data-stu-id="6fe84-199">Consider adding voice commands to any experience that you build.</span></span> <span data-ttu-id="6fe84-200">La voix est un moyen puissant et pratique de contrôler le système et les applications.</span><span class="sxs-lookup"><span data-stu-id="6fe84-200">Voice is a powerful and convenient way control the system and apps.</span></span> <span data-ttu-id="6fe84-201">Étant donné le nombre de dialectes et d’accents qui peuvent être utilisés, il est important de bien choisir les mots clés de reconnaissance vocale, afin de garantir que les commandes de vos utilisateurs seront correctement interprétées.</span><span class="sxs-lookup"><span data-stu-id="6fe84-201">Because users speak with a variety of dialects and accents, proper choice of speech keywords will make sure that your users' commands are interpreted unambiguously.</span></span>

### <a name="best-practices"></a><span data-ttu-id="6fe84-202">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="6fe84-202">Best practices</span></span>

<span data-ttu-id="6fe84-203">Voici quelques bonnes pratiques qui faciliteront la reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="6fe84-203">Below are some practices that will aid in smooth speech recognition.</span></span>
* <span data-ttu-id="6fe84-204">**Utilisez des commandes concises** : dans la mesure du possible, choisissez des mots clés de deux syllabes minimum.</span><span class="sxs-lookup"><span data-stu-id="6fe84-204">**Use concise commands** - When possible, choose keywords of two or more syllables.</span></span> <span data-ttu-id="6fe84-205">Les mots d’une syllabe comprennent souvent des voyelles qui peuvent être prononcées différemment selon l’accent de la personne.</span><span class="sxs-lookup"><span data-stu-id="6fe84-205">One-syllable words tend to use different vowel sounds when spoken by persons of different accents.</span></span> <span data-ttu-id="6fe84-206">Exemple : « lire la vidéo » est préférable à « lire la vidéo actuellement sélectionnée »</span><span class="sxs-lookup"><span data-stu-id="6fe84-206">Example: "Play video" is better than "Play the currently selected video"</span></span>
* <span data-ttu-id="6fe84-207">**Utilisation d’un vocabulaire simple** -exemple : « afficher la note » est préférable à « afficher le résumé »</span><span class="sxs-lookup"><span data-stu-id="6fe84-207">**Use simple vocabulary** - Example: "Show note" is better than "Show placard"</span></span>
* <span data-ttu-id="6fe84-208">**Utilisez des commandes non définitives** : assurez-vous que les actions réalisables par les commandes de reconnaissance vocale peuvent être facilement annulées, en cas de déclenchement involontaire provoqué par une personne parlant près de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fe84-208">**Make sure commands are non destructive** - Make sure any action that can be taken by a speech command is non destructive and can easily be undone in case another person speaking near the user accidentally triggers a command.</span></span>
* <span data-ttu-id="6fe84-209">**Évitez les commandes avec des consonances similaires** : évitez d’enregistrer plusieurs commandes vocales ayant une consonance très similaire.</span><span class="sxs-lookup"><span data-stu-id="6fe84-209">**Avoid similar sounding commands** - Avoid registering multiple speech commands that sound very similar.</span></span> <span data-ttu-id="6fe84-210">Exemple : « afficher plus » et « afficher le magasin » peuvent être très similaires.</span><span class="sxs-lookup"><span data-stu-id="6fe84-210">Example: "Show more" and "Show store" can be very similar sounding.</span></span>
* <span data-ttu-id="6fe84-211">**Désinscrivez votre application lorsque vous ne l’utilisez pas** : lorsque l’état de votre application rend une commande de reconnaissance vocale non valide, désinscrivez l’application pour que les autres commandes ne soient pas confondues avec celle-ci.</span><span class="sxs-lookup"><span data-stu-id="6fe84-211">**Unregister your app when not it use** - When your app is not in a state in which a particular speech command is valid, consider unregistering it so that other commands are not confused for that one.</span></span>
* <span data-ttu-id="6fe84-212">**Testez les différents accents** : testez votre application avec des utilisateurs ayant différents accents.</span><span class="sxs-lookup"><span data-stu-id="6fe84-212">**Test with different accents** - Test your app with users of different accents.</span></span>
* <span data-ttu-id="6fe84-213">**Maintenez une certaine cohérence au sein des commandes vocales** : si la commande « Retour » permet de retourner à la page précédente, gardez ce comportement dans toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="6fe84-213">**Maintain voice command consistency** - If "Go back" goes to the previous page, maintain this behavior in your applications.</span></span>
* <span data-ttu-id="6fe84-214">**Évitez d’utiliser des commandes du système** : les commandes vocales suivantes sont réservées au système.</span><span class="sxs-lookup"><span data-stu-id="6fe84-214">**Avoid using system commands** - The following voice commands are reserved for the system.</span></span> <span data-ttu-id="6fe84-215">Elles ne doivent pas être utilisées par les applications.</span><span class="sxs-lookup"><span data-stu-id="6fe84-215">These should not be used by applications.</span></span>
   * <span data-ttu-id="6fe84-216">« Hey Cortana »</span><span class="sxs-lookup"><span data-stu-id="6fe84-216">"Hey Cortana"</span></span>
   * <span data-ttu-id="6fe84-217">« Sélectionner »</span><span class="sxs-lookup"><span data-stu-id="6fe84-217">"Select"</span></span>
   * <span data-ttu-id="6fe84-218">« Aller au début »</span><span class="sxs-lookup"><span data-stu-id="6fe84-218">"Go to start"</span></span>

### <a name="advantages-of-voice-input"></a><span data-ttu-id="6fe84-219">Avantages de l’entrée vocale</span><span class="sxs-lookup"><span data-stu-id="6fe84-219">Advantages of voice input</span></span>

<span data-ttu-id="6fe84-220">La voix est un moyen naturel de communiquer nos intentions.</span><span class="sxs-lookup"><span data-stu-id="6fe84-220">Voice input is a natural way to communicate our intents.</span></span> <span data-ttu-id="6fe84-221">La voix est particulièrement intéressante pour les **parcours** d’interface, car elle peut aider les utilisateurs à franchir plusieurs étapes d’une interface (un utilisateur peut indiquer « revenir en arrière » lors de la consultation d’une page Web, au lieu de devoir cliquer sur le bouton précédent de l’application).</span><span class="sxs-lookup"><span data-stu-id="6fe84-221">Voice is especially good at interface **traversals** because it can help users cut through multiple steps of an interface (a user might say "go back" while looking at a webpage, instead of having to go up and hit the back button in the app).</span></span> <span data-ttu-id="6fe84-222">Cette économie d’énergie a un **effet émotionnelle** puissant sur la perception de l’expérience de l’utilisateur et lui donne une petite quantité d’Superpower.</span><span class="sxs-lookup"><span data-stu-id="6fe84-222">This small time saving has a powerful **emotional effect** on user’s perception of the experience and gives them a small amount superpower.</span></span> <span data-ttu-id="6fe84-223">L’utilisation de la voix est également pratique lorsque nous avons les mains occupées ou que nous effectuons **plusieurs tâches en même temps**.</span><span class="sxs-lookup"><span data-stu-id="6fe84-223">Using voice is also a convenient input method when we have our arms full or are **multi-tasking**.</span></span> <span data-ttu-id="6fe84-224">Sur les appareils où la saisie sur un clavier est difficile, la **dictée vocale** peut être un moyen efficace d’entrer du texte.</span><span class="sxs-lookup"><span data-stu-id="6fe84-224">On devices where typing on a keyboard is difficult, **voice dictation** can be an efficient alternative way to input text.</span></span> <span data-ttu-id="6fe84-225">Enfin, dans certains cas, lorsque la **plage de précision** du point de vue et du mouvement est limitée, la voix peut aider à lever l’ambiguïté de l’intention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fe84-225">Lastly, in some cases when the **range of accuracy** for gaze and gesture are limited, voice can help to disambiguate the user's intent.</span></span> 

<span data-ttu-id="6fe84-226">**Avantages de l’utilisation de la voix**</span><span class="sxs-lookup"><span data-stu-id="6fe84-226">**How using voice can benefit the user**</span></span>
* <span data-ttu-id="6fe84-227">Gain de temps : l’objectif final est donc plus facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="6fe84-227">Reduces time - it should make the end goal more efficient.</span></span>
* <span data-ttu-id="6fe84-228">Efforts moindres : l’exécution des tâches est plus fluide et ne demande pas d’efforts.</span><span class="sxs-lookup"><span data-stu-id="6fe84-228">Minimizes effort - it should make tasks more fluid and effortless.</span></span>
* <span data-ttu-id="6fe84-229">Réduction de la charge cognitive : les commandes vocales sont intuitives, et faciles à apprendre et à mémoriser.</span><span class="sxs-lookup"><span data-stu-id="6fe84-229">Reduces cognitive load - it's intuitive, easy to learn, and remember.</span></span>
* <span data-ttu-id="6fe84-230">Acceptation sociale : leur comportement s’inscrit facilement dans les normes sociétales.</span><span class="sxs-lookup"><span data-stu-id="6fe84-230">It's socially acceptable - it should fit in with societal norms in terms of behavior.</span></span>
* <span data-ttu-id="6fe84-231">Routine : l’utilisation de la voix peut facilement se transformer en habitude.</span><span class="sxs-lookup"><span data-stu-id="6fe84-231">It's routine - voice can readily become a habitual behavior.</span></span>

### <a name="challenges-for-voice-input"></a><span data-ttu-id="6fe84-232">Défis liés à l’entrée vocale</span><span class="sxs-lookup"><span data-stu-id="6fe84-232">Challenges for voice input</span></span>

<span data-ttu-id="6fe84-233">Bien que les entrées vocales soient intéressantes pour de nombreuses applications différentes, elles sont également confrontées à plusieurs défis.</span><span class="sxs-lookup"><span data-stu-id="6fe84-233">While voice input is great for a lot of different applications, it also faces several challenges.</span></span> <span data-ttu-id="6fe84-234">Le fait de comprendre les avantages et les défis liés aux entrées vocales permet aux développeurs d’applications de faire des choix plus intelligents quant à la façon et au moment d’utiliser les entrées vocales et à créer une expérience optimale pour leurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6fe84-234">Understanding both the advantages and challenges for voice input enables app developers to make smarter choices for how and when to use voice input and to create a great experience for their users.</span></span>

<span data-ttu-id="6fe84-235">**Entrée vocale pour le contrôle d’entrée continu** Le contrôle affiné est l’un d’eux.</span><span class="sxs-lookup"><span data-stu-id="6fe84-235">**Voice input for continuous input control** Fine-grained control is one of them.</span></span> <span data-ttu-id="6fe84-236">Par exemple, un utilisateur peut souhaiter modifier son volume dans son application musical.</span><span class="sxs-lookup"><span data-stu-id="6fe84-236">For example, a user might want to change their volume in their music app.</span></span> <span data-ttu-id="6fe84-237">Elle peut simplement indiquer « plus fort », mais il n’est pas clair que le système est censé créer le volume.</span><span class="sxs-lookup"><span data-stu-id="6fe84-237">She can simply say "louder", but it's not clear how much louder the system is supposed to make the volume.</span></span> <span data-ttu-id="6fe84-238">L’utilisateur peut par exemple : « en faire un peu plus fort », mais « un peu » est difficile à quantifier.</span><span class="sxs-lookup"><span data-stu-id="6fe84-238">The user could say: "Make it a little louder", but "a little" is difficult to quantify.</span></span> <span data-ttu-id="6fe84-239">Le déplacement ou la mise à l’échelle d’hologrammes avec la voix est tout aussi difficile.</span><span class="sxs-lookup"><span data-stu-id="6fe84-239">Moving or scaling holograms with voice is similarly difficult.</span></span> 

<span data-ttu-id="6fe84-240">**Fiabilité de la détection des entrées vocales** Bien que les systèmes d’entrée de voix soient plus performants et mieux, ils peuvent parfois entendre et interpréter une commande vocale de manière incorrecte.</span><span class="sxs-lookup"><span data-stu-id="6fe84-240">**Reliability of voice input detection** While voice input systems become better and better, sometimes they may incorrectly hear and interpret a voice command.</span></span>
<span data-ttu-id="6fe84-241">La clé consiste à résoudre ce problème dans votre application en fournissant des commentaires à l’utilisateur lorsque le système est à l’écoute et ce que le système a compris pour créer une clarté sur les problèmes potentiels en maîtrisant correctement l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fe84-241">The key is to address this challenge in your application by providing feedback to the user when the system is listening and what the system understood to create clarity on potential issues in correctly understanding the user.</span></span>  

<span data-ttu-id="6fe84-242">**Entrée vocale dans les espaces partagés** La voix ne peut pas être socialement acceptable dans les espaces que vous partagez avec d’autres personnes.</span><span class="sxs-lookup"><span data-stu-id="6fe84-242">**Voice input in shared spaces** Voice may not be socially acceptable in spaces that you share with others.</span></span>
<span data-ttu-id="6fe84-243">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="6fe84-243">Here are a few examples:</span></span>
* <span data-ttu-id="6fe84-244">Il se peut que l’utilisateur ne souhaite pas déranger les autres (par exemple, dans une bibliothèque silencieuse ou un bureau partagé)</span><span class="sxs-lookup"><span data-stu-id="6fe84-244">The user may not want to disturb others (e.g., in a quiet library or shared office)</span></span>
* <span data-ttu-id="6fe84-245">Il se peut que les utilisateurs ne soient pas contraints de parler à eux-mêmes en public,</span><span class="sxs-lookup"><span data-stu-id="6fe84-245">Users may feel awkward being seen talking to themselves in public,</span></span>
* <span data-ttu-id="6fe84-246">Un utilisateur peut paraître inconfortant de dicter un message personnel ou confidentiel (y compris des mots de passe), tandis que d’autres sont à l’écoute</span><span class="sxs-lookup"><span data-stu-id="6fe84-246">A user may feel uncomfortable dictating a personal or confidential message (including passwords) while others are listening</span></span>

<span data-ttu-id="6fe84-247">**Entrée vocale de mots uniques ou inconnus** Les problèmes d’entrée vocale se posent également lorsque les utilisateurs dictent des mots qui peuvent être inconnus du système, tels que des surnoms, certains mots d’argot ou abréviations.</span><span class="sxs-lookup"><span data-stu-id="6fe84-247">**Voice input of unique or unknown words** Difficulties for voice input also come when users are dictating words that may be unknown to the system, such as nicknames, certain slang words or abbreviations.</span></span> 

<span data-ttu-id="6fe84-248">**Apprentissage des commandes vocales** Tandis que l’objectif ultime est de naturellement communiquer avec votre système, les applications s’appuient souvent sur des commandes vocales prédéfinies spécifiques.</span><span class="sxs-lookup"><span data-stu-id="6fe84-248">**Learning voice commands** While the ultimate goal is to naturally converse with your system, often times apps still rely on specific pre-defined voice commands.</span></span>
<span data-ttu-id="6fe84-249">Un défi associé à un grand nombre de commandes vocales est de savoir comment les enseigner sans surcharger l’utilisateur et comment aider l’utilisateur à les conserver.</span><span class="sxs-lookup"><span data-stu-id="6fe84-249">A challenge associated with a big set of voice commands is how to teach them without overloading the user and how to help the user to retain them.</span></span> 

<br>

---

### <a name="voice-feedback-states"></a><span data-ttu-id="6fe84-250">Retours des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="6fe84-250">Voice feedback states</span></span>

<span data-ttu-id="6fe84-251">Lorsque la voix est utilisée correctement, l’utilisateur **comprend ce qu’il peut dire et reçoit la confirmation** que le système a **bien compris sa commande**.</span><span class="sxs-lookup"><span data-stu-id="6fe84-251">When Voice is applied properly, the user understands **what they can say and get clear feedback** the system **heard them correctly**.</span></span> <span data-ttu-id="6fe84-252">Ce sont ces deux éléments qui donnent envie à l’utilisateur de choisir la voix comme méthode d’entrée principale.</span><span class="sxs-lookup"><span data-stu-id="6fe84-252">These two signals make the user feel confident in using Voice as a primary input.</span></span> <span data-ttu-id="6fe84-253">Voici un diagramme qui montre ce qui se passe au niveau du curseur lorsque l’entrée vocale est reconnue, et comment celle-ci est communiquée à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fe84-253">Below is a diagram showing what happens to the cursor when voice input is recognized and how it communicates that to the user.</span></span>


:::row:::
    :::column:::
       <span data-ttu-id="6fe84-254">![1. État normal du curseur](images/voicefeedbackstates-regular.jpg)</span><span class="sxs-lookup"><span data-stu-id="6fe84-254">![1. Regular cursor state](images/voicefeedbackstates-regular.jpg)</span></span><br>
       <span data-ttu-id="6fe84-255">**1. état normal du curseur**</span><span class="sxs-lookup"><span data-stu-id="6fe84-255">**1. Regular cursor state**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="6fe84-256">![2. Communique les commentaires vocaux, puis disparaît](images/voicefeedbackstates-voice.jpg)</span><span class="sxs-lookup"><span data-stu-id="6fe84-256">![2. Communicates voice feedback and then disappears](images/voicefeedbackstates-voice.jpg)</span></span><br>
        <span data-ttu-id="6fe84-257">**2. communique les commentaires vocaux, puis disparaît**</span><span class="sxs-lookup"><span data-stu-id="6fe84-257">**2. Communicates voice feedback and then disappears**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="6fe84-258">![\* 3.</span><span class="sxs-lookup"><span data-stu-id="6fe84-258">![\*3.</span></span> <span data-ttu-id="6fe84-259">État normal du curseur](images/voicefeedbackstates-regular.jpg)</span><span class="sxs-lookup"><span data-stu-id="6fe84-259">Regular cursor state](images/voicefeedbackstates-regular.jpg)</span></span><br>
       <span data-ttu-id="6fe84-260">**3. retourne à l’état de curseur normal**</span><span class="sxs-lookup"><span data-stu-id="6fe84-260">**3. Returns to regular cursor state**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

<br>

## <a name="top-things-users-should-know-about-speech-in-mixed-reality"></a><span data-ttu-id="6fe84-261">Points importants concernant la reconnaissance vocale dans la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="6fe84-261">Top things users should know about "speech" in mixed reality</span></span>
* <span data-ttu-id="6fe84-262">Vous devez dire **« Sélectionner »** lorsque vous ciblez un bouton (vous pouvez l’utiliser n’importe où pour cliquer sur un bouton).</span><span class="sxs-lookup"><span data-stu-id="6fe84-262">Say **"Select"** while targeting a button (you can use this anywhere to click a button).</span></span>
* <span data-ttu-id="6fe84-263">Dans certaines applications, vous pouvez prononcer le **nom de l’étiquette d’un bouton de la barre d’application** pour exécuter une action.</span><span class="sxs-lookup"><span data-stu-id="6fe84-263">You can say the **label name of an app bar button** in some apps to take an action.</span></span> <span data-ttu-id="6fe84-264">Par exemple, lorsqu’il regarde une application, l’utilisateur peut prononcer la commande « Supprimer » pour supprimer cette application (cela vous évite d’avoir à la supprimer manuellement).</span><span class="sxs-lookup"><span data-stu-id="6fe84-264">For example, while looking at an app, a user can say the command "Remove" to remove the app from the world (this saves time from having to click it with your hand).</span></span>
* <span data-ttu-id="6fe84-265">Vous pouvez activer Cortana à l’aide de la commande **« Hey Cortana »** .</span><span class="sxs-lookup"><span data-stu-id="6fe84-265">You can initiate Cortana listening by saying **"Hey Cortana."**</span></span> <span data-ttu-id="6fe84-266">Vous pouvez lui poser des questions (« Hey Cortana, combien mesure la tour Eiffel ? »), lui demander d’ouvrir une application (« Hey Cortana, ouvre Netflix ») ou lui demander d’afficher le menu Démarrer (« Hey Cortana, ouvre le menu Démarrer »), et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="6fe84-266">You can ask her questions ("Hey Cortana, how tall is the Eiffel tower"), tell her to open an app ("Hey Cortana, open Netflix"), or tell her to bring up the Start Menu ("Hey Cortana, take me home") and more.</span></span>

## <a name="common-questions-and-concerns-users-have-about-voice"></a><span data-ttu-id="6fe84-267">Questions et inquiétudes fréquentes concernant la reconnaissance vocale</span><span class="sxs-lookup"><span data-stu-id="6fe84-267">Common questions and concerns users have about voice</span></span>
* <span data-ttu-id="6fe84-268">Que dois-je dire ?</span><span class="sxs-lookup"><span data-stu-id="6fe84-268">What can I say?</span></span>
* <span data-ttu-id="6fe84-269">Comment savoir si le système m’a bien entendu ?</span><span class="sxs-lookup"><span data-stu-id="6fe84-269">How do I know the system heard me correctly?</span></span>
   * <span data-ttu-id="6fe84-270">Le système ne comprend pas mes commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="6fe84-270">The system keeps getting my voice commands wrong.</span></span>
   * <span data-ttu-id="6fe84-271">Il ne réagit pas quand je lui adresse une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="6fe84-271">It doesn’t react when I give it a voice command.</span></span>
* <span data-ttu-id="6fe84-272">Il réagit de façon inadaptée lorsque je lui adresse une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="6fe84-272">It reacts the wrong way when I give it a voice command.</span></span>
* <span data-ttu-id="6fe84-273">Comment choisir l’application ou la commande d’application à laquelle adresser mes commandes vocales ?</span><span class="sxs-lookup"><span data-stu-id="6fe84-273">How do I target my voice to a specific app or app command?</span></span>
* <span data-ttu-id="6fe84-274">Puis-je utiliser la voix pour contrôler les éléments holographiques sur HoloLens ?</span><span class="sxs-lookup"><span data-stu-id="6fe84-274">Can I use voice to command things out the holographic frame on HoloLens?</span></span>

## <a name="communication"></a><span data-ttu-id="6fe84-275">Communication</span><span class="sxs-lookup"><span data-stu-id="6fe84-275">Communication</span></span>

<span data-ttu-id="6fe84-276">Pour les applications qui souhaitent tirer parti des options de traitement d’entrée audio personnalisées fournies par HoloLens, il est important de comprendre les différentes [catégories de flux audio](https://msdn.microsoft.com/library/windows/desktop/hh404178(v=vs.85).aspx) que votre application peut consommer.</span><span class="sxs-lookup"><span data-stu-id="6fe84-276">For applications that want to take advantage of the customized audio input processing options provided by HoloLens, it is important to understand the various [audio stream categories](https://msdn.microsoft.com/library/windows/desktop/hh404178(v=vs.85).aspx) your app can consume.</span></span> <span data-ttu-id="6fe84-277">Windows 10 prend en charge plusieurs catégories de flux et HoloLens en utilise trois pour permettre un traitement personnalisé afin d’optimiser la qualité audio du microphone adaptée à la parole, à la communication et à d’autres qui peuvent être utilisées pour l’audio de l’environnement ambiant. scénarios de capture (par exemple, « Camcorder »).</span><span class="sxs-lookup"><span data-stu-id="6fe84-277">Windows 10 supports several different stream categories and HoloLens makes use of three of these to enable custom processing to optimize the microphone audio quality tailored for speech, communication and other which can be used for ambient environment audio capture (i.e. "camcorder") scenarios.</span></span>
* <span data-ttu-id="6fe84-278">La catégorie de flux AudioCategory_Communications est personnalisée pour les scénarios de qualité des appels et de narration et fournit au client un flux audio mono 16kHz 24bit de la voix de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fe84-278">The AudioCategory_Communications stream category is customized for call quality and narration scenarios and provides the client with a 16kHz 24bit mono audio stream of the user's voice</span></span>
* <span data-ttu-id="6fe84-279">La catégorie de flux AudioCategory_Speech est personnalisée pour le moteur de reconnaissance de la parole HoloLens (Windows) et lui fournit un flux mono 16kHz 24bit de la voix de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fe84-279">The AudioCategory_Speech stream category is customized for the HoloLens (Windows) speech engine and provides it with a 16kHz 24bit mono stream of the user's voice.</span></span> <span data-ttu-id="6fe84-280">Cette catégorie peut être utilisée par les moteurs de reconnaissance vocale tiers si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6fe84-280">This category can be used by 3rd party speech engines if needed.</span></span>
* <span data-ttu-id="6fe84-281">La catégorie de flux AudioCategory_Other est personnalisée pour l’enregistrement audio de l’environnement ambiant et fournit au client un flux audio stéréo de 48 bits.</span><span class="sxs-lookup"><span data-stu-id="6fe84-281">The AudioCategory_Other stream category is customized for ambient environment audio recording and provides the client with a 48kHz 24 bit stereo audio stream.</span></span>

<span data-ttu-id="6fe84-282">Tout ce traitement audio est l’accélération matérielle, ce qui signifie que les fonctionnalités se déchargent beaucoup moins d’énergie que si le même traitement a été effectué sur l’UC HoloLens.</span><span class="sxs-lookup"><span data-stu-id="6fe84-282">All this audio processing is hardware accelerated which means the features drain a lot less power than if the same processing was done on the HoloLens CPU.</span></span> <span data-ttu-id="6fe84-283">Évitez d’exécuter un autre traitement d’entrée audio sur le processeur pour maximiser la durée de vie de la batterie du système et tirer parti du traitement des entrées audio déchargées et intégrées.</span><span class="sxs-lookup"><span data-stu-id="6fe84-283">Avoid running other audio input processing on the CPU to maximize system battery life and take advantage of the built in, offloaded audio input processing.</span></span>

## <a name="languages"></a><span data-ttu-id="6fe84-284">Langues</span><span class="sxs-lookup"><span data-stu-id="6fe84-284">Languages</span></span>

<span data-ttu-id="6fe84-285">HoloLens 2 prend également en charge des langues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6fe84-285">HoloLens 2 also supports additional languages.</span></span> <span data-ttu-id="6fe84-286">N’oubliez pas que les commandes vocales s’exécutent toujours dans la langue d’affichage du système même si plusieurs claviers sont installés ou si les applications essaient de créer un module de reconnaissance vocale dans une autre langue.</span><span class="sxs-lookup"><span data-stu-id="6fe84-286">Keep in mind that speech commands will always run in the system's display language even if multiple keyboards are installed or if apps attempt to create a speech recognizer in a different language.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6fe84-287">Dépannage</span><span class="sxs-lookup"><span data-stu-id="6fe84-287">Troubleshooting</span></span>

<span data-ttu-id="6fe84-288">Si vous rencontrez des problèmes à l’aide de « SELECT » et de « Hey Cortana », essayez de passer à un espace plus silencieux, à l’extérieur de la source de bruit, ou en parlant plus fort.</span><span class="sxs-lookup"><span data-stu-id="6fe84-288">If you're having any issues using "select" and "Hey Cortana", try moving to a quieter space, turning away from the source of noise, or by speaking louder.</span></span> <span data-ttu-id="6fe84-289">À ce stade, toute la reconnaissance vocale sur HoloLens est réglée et optimisée spécifiquement pour les intervenants natifs de États-Unis anglais.</span><span class="sxs-lookup"><span data-stu-id="6fe84-289">At this time, all speech recognition on HoloLens is tuned and optimized specifically to native speakers of United States English.</span></span>

<span data-ttu-id="6fe84-290">Pour la version 2017 de Windows Mixed Reality Edition, la logique de gestion des points de terminaison audio fonctionnera correctement (éternellement) après la déconnexion et la réinitialisation du PC Desktop après la première connexion HMD.</span><span class="sxs-lookup"><span data-stu-id="6fe84-290">For the Windows Mixed Reality Developer Edition release 2017, the audio endpoint management logic will work fine (forever) after logging out and back in to the PC desktop after the initial HMD connection.</span></span> <span data-ttu-id="6fe84-291">Avant le premier événement de déconnexion/dans le cas de l’utilisation de WMR OOBE, l’utilisateur peut rencontrer différents problèmes de fonctionnalité audio, qu’il s’agisse d’aucun audio ou d’aucune commutation audio, en fonction de la configuration du système avant de connecter le HMD pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="6fe84-291">Prior to that first sign out/in event after going through WMR OOBE, the user could experience various audio functionality issues ranging from no audio to no audio switching depending on how the system was set up prior to connecting the HMD for the first time.</span></span>

## <a name="see-also"></a><span data-ttu-id="6fe84-292">Articles associés</span><span class="sxs-lookup"><span data-stu-id="6fe84-292">See also</span></span>
* [<span data-ttu-id="6fe84-293">Point de regard et validation</span><span class="sxs-lookup"><span data-stu-id="6fe84-293">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="6fe84-294">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="6fe84-294">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="6fe84-295">Entrée MR 212 : voix</span><span class="sxs-lookup"><span data-stu-id="6fe84-295">MR Input 212: Voice</span></span>](holograms-212.md)
* [<span data-ttu-id="6fe84-296">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="6fe84-296">Voice input in DirectX</span></span>](voice-input-in-directx.md)
* [<span data-ttu-id="6fe84-297">Entrée vocale dans Unity</span><span class="sxs-lookup"><span data-stu-id="6fe84-297">Voice input in Unity</span></span>](voice-input-in-unity.md)
