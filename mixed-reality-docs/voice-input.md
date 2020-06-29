---
title: Entrée vocale
description: L’entrée vocale est une entrée de base pour HoloLens et les casques immersifs immersifs de Windows Mixed Reality. La voix peut être utilisée pour les commandes, la dictée, Cortana et bien plus encore.
author: hak0n
ms.author: hakons
ms.date: 10/03/2019
ms.topic: article
keywords: GGv, voix, Cortana, discours, entrée
ms.openlocfilehash: 37364e90aa1d8a7b607a99f4c9b830972f7f80b3
ms.sourcegitcommit: 5612e8bfb9c548eac42182702cec87b160efbbfe
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85441826"
---
# <a name="voice-input"></a><span data-ttu-id="5a835-105">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="5a835-105">Voice input</span></span>

![Entrée vocale](images/UX/UX_Hero_VoiceCommand.jpg)

<span data-ttu-id="5a835-107">La voix est l’un des principaux types d’entrée sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="5a835-107">Voice is one of the key forms of input on HoloLens.</span></span> <span data-ttu-id="5a835-108">Elle vous permet de directement commander un hologramme sans avoir à utiliser des gestes à la [main](gaze-and-commit.md#composite-gestures).</span><span class="sxs-lookup"><span data-stu-id="5a835-108">It allows you to directly command a hologram without having to use [hand gestures](gaze-and-commit.md#composite-gestures).</span></span> <span data-ttu-id="5a835-109">Une entrée vocale peut être un moyen naturel de communiquer votre intention.</span><span class="sxs-lookup"><span data-stu-id="5a835-109">Voice input can be a natural way to communicate your intent.</span></span> <span data-ttu-id="5a835-110">La voix est particulièrement intéressante pour traverser les interfaces complexes, car elle permet aux utilisateurs de couper les menus imbriqués avec une commande.</span><span class="sxs-lookup"><span data-stu-id="5a835-110">Voice is especially good at traversing complex interfaces, because it lets users cut through nested menus with one command.</span></span>

<span data-ttu-id="5a835-111">L’entrée vocale est alimentée par le [moteur](https://msdn.microsoft.com/library/windows/apps/mt185615.aspx) qui prend en charge la reconnaissance vocale dans toutes les autres _applications universelles Windows_.</span><span class="sxs-lookup"><span data-stu-id="5a835-111">Voice input is powered by the [same engine](https://msdn.microsoft.com/library/windows/apps/mt185615.aspx) that supports speech in all other _Universal Windows Apps_.</span></span> <span data-ttu-id="5a835-112">Sur HoloLens, la reconnaissance vocale fonctionne toujours dans la langue d’affichage Windows configurée dans paramètres.</span><span class="sxs-lookup"><span data-stu-id="5a835-112">On HoloLens, speech recognition will always function in the Windows display language configured in Settings.</span></span> 

<br>

## <a name="voice-and-gaze"></a><span data-ttu-id="5a835-113">Voix et regard</span><span class="sxs-lookup"><span data-stu-id="5a835-113">Voice and gaze</span></span>

<span data-ttu-id="5a835-114">Lorsque vous utilisez des commandes vocales (tête ou œil), le point de regard est généralement utilisé comme mécanisme de ciblage, que ce soit avec un curseur (« Select ») ou pour canaliser implicitement votre commande vers une application que vous examinez.</span><span class="sxs-lookup"><span data-stu-id="5a835-114">When using voice commands, (head or eye) gaze is typically used as the targeting mechanism, whether with a cursor ("select") or to implicitly channel your command to an application that you are looking at.</span></span> <span data-ttu-id="5a835-115">Pour ce faire, il n’est même pas nécessaire de faire apparaître un curseur pointant vers le regard _(« Regardez-le, dites-le »)_.</span><span class="sxs-lookup"><span data-stu-id="5a835-115">For this, it may not even be required to show any gaze cursor _("see it, say it")_.</span></span> <span data-ttu-id="5a835-116">Bien entendu, certaines commandes vocales ne nécessitent pas de cible, telles que « aller à démarrer » ou « Hey Cortana ».</span><span class="sxs-lookup"><span data-stu-id="5a835-116">Of course, some voice commands don't require a target at all, such as "go to start" or "Hey Cortana."</span></span>

<br>

<iframe width="940" height="530" src="https://www.youtube.com/embed/eHMkOpNUtR8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## <a name="device-support"></a><span data-ttu-id="5a835-117">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="5a835-117">Device support</span></span>

<table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="5a835-118"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="5a835-118"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="5a835-119"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="5a835-119"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
        <td><span data-ttu-id="5a835-120"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="5a835-120"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
        <td><span data-ttu-id="5a835-121"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="5a835-121"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="5a835-122">Entrée vocale</span><span class="sxs-lookup"><span data-stu-id="5a835-122">Voice input</span></span></td>
        <td><span data-ttu-id="5a835-123">✔️</span><span class="sxs-lookup"><span data-stu-id="5a835-123">✔️</span></span></td>
        <td><span data-ttu-id="5a835-124">✔️</span><span class="sxs-lookup"><span data-stu-id="5a835-124">✔️</span></span></td>
        <td><span data-ttu-id="5a835-125">✔️ (avec microphone)</span><span class="sxs-lookup"><span data-stu-id="5a835-125">✔️ (with microphone)</span></span></td>
    </tr>
</table>

## <a name="the-select-command"></a><span data-ttu-id="5a835-126">Commande « sélectionner »</span><span class="sxs-lookup"><span data-stu-id="5a835-126">The "select" command</span></span>

<span data-ttu-id="5a835-127">**HoloLens (1ère génération)**</span><span class="sxs-lookup"><span data-stu-id="5a835-127">**HoloLens (1st gen)**</span></span>

<span data-ttu-id="5a835-128">Même sans ajouter spécifiquement la prise en charge vocale à votre application, vos utilisateurs peuvent activer des hologrammes simplement en disant à la commande System Voice « Select ».</span><span class="sxs-lookup"><span data-stu-id="5a835-128">Even without specifically adding voice support to your app, your users can activate holograms simply by saying the system voice command "select".</span></span> <span data-ttu-id="5a835-129">Cela se comporte de la même façon qu’un [TAP Air](gaze-and-commit.md#composite-gestures) sur HoloLens, en appuyant sur le bouton de sélection sur l’interactiveur [hololens](https://docs.microsoft.com/hololens/hololens1-clicker)ou en appuyant sur le déclencheur sur un [contrôleur de mouvement Windows Mixed Reality](motion-controllers.md).</span><span class="sxs-lookup"><span data-stu-id="5a835-129">This behaves the same as an [air tap](gaze-and-commit.md#composite-gestures) on HoloLens, pressing the select button on the [HoloLens clicker](https://docs.microsoft.com/hololens/hololens1-clicker), or pressing the trigger on a [Windows Mixed Reality motion controller](motion-controllers.md).</span></span> <span data-ttu-id="5a835-130">Vous entendez un son et vous voyez une info-bulle avec « sélectionner » qui s’affiche comme confirmation.</span><span class="sxs-lookup"><span data-stu-id="5a835-130">You will hear a sound and see a tooltip with "select" appear as confirmation.</span></span> <span data-ttu-id="5a835-131">« SELECT » est activé par un algorithme de détection de mot-clé à faible consommation d’énergie. il est donc toujours disponible pour vous, à tout moment, avec un impact minimal sur la durée de vie de la batterie, même avec vos mains.</span><span class="sxs-lookup"><span data-stu-id="5a835-131">"Select" is enabled by a low power keyword detection algorithm so it is always available for you to say at any time with minimal battery life impact, even with your hands at your side.</span></span>

<br>

---

:::row:::
    :::column:::
        <span data-ttu-id="5a835-132">**HoloLens 2**</span><span class="sxs-lookup"><span data-stu-id="5a835-132">**HoloLens 2**</span></span><br><br>
        <span data-ttu-id="5a835-133">Pour utiliser la commande vocale « SELECT » dans HoloLens 2, vous devez d’abord afficher le curseur en regard à utiliser comme pointeur.</span><span class="sxs-lookup"><span data-stu-id="5a835-133">In order to use the "select" voice command in HoloLens 2, you first need to bring up the gaze cursor to use as a pointer.</span></span> <span data-ttu-id="5a835-134">La commande pour l’afficher est facile à mémoriser, par exemple « Select ».</span><span class="sxs-lookup"><span data-stu-id="5a835-134">The command to bring it up is easy to remember -- just say, "select".</span></span><br><br>
        <span data-ttu-id="5a835-135">Pour quitter le mode, il vous suffit de réutiliser vos mains, soit par air, en appuyant sur un bouton avec vos doigts, soit en utilisant le mouvement du système.</span><span class="sxs-lookup"><span data-stu-id="5a835-135">To exit the mode, simply use your hands again, either by air tapping, approaching a button with your fingers, or using the system gesture.</span></span><br>
        <br>
        <span data-ttu-id="5a835-136">*Image : dites « sélectionner » pour utiliser la commande vocale pour la sélection*</span><span class="sxs-lookup"><span data-stu-id="5a835-136">*Image: Say "select" to use the voice command for selection*</span></span>
    :::column-end:::
        :::column:::
       ![Un utilisateur peut indiquer « sélectionner » pour utiliser la commande vocale pour une sélection.](images/kma-voice-select-00170.jpg)<br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="hey-cortana"></a><span data-ttu-id="5a835-138">Bonjour Cortana</span><span class="sxs-lookup"><span data-stu-id="5a835-138">Hey Cortana</span></span>

<span data-ttu-id="5a835-139">Vous pouvez également indiquer « Hey Cortana » pour afficher Cortana à tout moment.</span><span class="sxs-lookup"><span data-stu-id="5a835-139">You can also say "Hey Cortana" to bring up Cortana at anytime.</span></span> <span data-ttu-id="5a835-140">Vous n’avez pas besoin d’attendre qu’il apparaisse pour continuer à poser votre question ou de lui donner une instruction. par exemple, essayez de dire « Bonjour Cortana, qu’est-ce que la météo ? »</span><span class="sxs-lookup"><span data-stu-id="5a835-140">You don't have to wait for her to appear to continue asking her your question or giving her an instruction - for example, try saying "Hey Cortana, what's the weather?"</span></span> <span data-ttu-id="5a835-141">comme une seule phrase.</span><span class="sxs-lookup"><span data-stu-id="5a835-141">as a single sentence.</span></span> <span data-ttu-id="5a835-142">Pour plus d’informations sur Cortana et ce que vous pouvez faire, demandez-lui simplement !</span><span class="sxs-lookup"><span data-stu-id="5a835-142">For more information about Cortana and what you can do, simply ask her!</span></span> <span data-ttu-id="5a835-143">Dites « Hey Cortana, que puis-je faire ? »</span><span class="sxs-lookup"><span data-stu-id="5a835-143">Say "Hey Cortana, what can I say?"</span></span> <span data-ttu-id="5a835-144">et elle extrait une liste de commandes de travail et suggérées.</span><span class="sxs-lookup"><span data-stu-id="5a835-144">and she'll pull up a list of working and suggested commands.</span></span> <span data-ttu-id="5a835-145">Si vous êtes déjà dans l’application Cortana, vous pouvez également cliquer sur le **?**</span><span class="sxs-lookup"><span data-stu-id="5a835-145">If you're already in the Cortana app you can also click the **?**</span></span> <span data-ttu-id="5a835-146">sur la barre latérale pour extraire le même menu.</span><span class="sxs-lookup"><span data-stu-id="5a835-146">icon on the sidebar to pull up this same menu.</span></span>

<span data-ttu-id="5a835-147">**Commandes spécifiques à HoloLens**</span><span class="sxs-lookup"><span data-stu-id="5a835-147">**HoloLens-specific commands**</span></span>
* <span data-ttu-id="5a835-148">Qu’est-ce que je dis ?</span><span class="sxs-lookup"><span data-stu-id="5a835-148">"What can I say?"</span></span>
* <span data-ttu-id="5a835-149">« Aller au début »-au lieu de [fleuri](system-gesture.md#bloom) pour accéder au [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu)</span><span class="sxs-lookup"><span data-stu-id="5a835-149">"Go to Start" - instead of [bloom](system-gesture.md#bloom) to get to [Start Menu](navigating-the-windows-mixed-reality-home.md#start-menu)</span></span>
* <span data-ttu-id="5a835-150">« Lancer <app> »</span><span class="sxs-lookup"><span data-stu-id="5a835-150">"Launch <app>"</span></span>
* <span data-ttu-id="5a835-151">« Déplacer <app> ici »</span><span class="sxs-lookup"><span data-stu-id="5a835-151">"Move <app> here"</span></span>
* <span data-ttu-id="5a835-152">« Prendre une photo »</span><span class="sxs-lookup"><span data-stu-id="5a835-152">"Take a picture"</span></span>
* <span data-ttu-id="5a835-153">« Démarrer l’enregistrement »</span><span class="sxs-lookup"><span data-stu-id="5a835-153">"Start recording"</span></span>
* <span data-ttu-id="5a835-154">« Arrêter l’enregistrement »</span><span class="sxs-lookup"><span data-stu-id="5a835-154">"Stop recording"</span></span>
* <span data-ttu-id="5a835-155">« Afficher le rayon de la main »</span><span class="sxs-lookup"><span data-stu-id="5a835-155">"Show hand ray"</span></span>
* <span data-ttu-id="5a835-156">« Masquer le rayon de la main »</span><span class="sxs-lookup"><span data-stu-id="5a835-156">"Hide hand ray"</span></span>
* <span data-ttu-id="5a835-157">« Augmenter la luminosité »</span><span class="sxs-lookup"><span data-stu-id="5a835-157">"Increase the brightness"</span></span>
* <span data-ttu-id="5a835-158">« Réduire la luminosité »</span><span class="sxs-lookup"><span data-stu-id="5a835-158">"Decrease the brightness"</span></span>
* <span data-ttu-id="5a835-159">« Augmenter le volume »</span><span class="sxs-lookup"><span data-stu-id="5a835-159">"Increase the volume"</span></span>
* <span data-ttu-id="5a835-160">« Réduire le volume »</span><span class="sxs-lookup"><span data-stu-id="5a835-160">"Decrease the volume"</span></span>
* <span data-ttu-id="5a835-161">« Muet » ou « muet »</span><span class="sxs-lookup"><span data-stu-id="5a835-161">"Mute" or "Unmute"</span></span>
* <span data-ttu-id="5a835-162">« Arrêter l’appareil »</span><span class="sxs-lookup"><span data-stu-id="5a835-162">"Shut down the device"</span></span>
* <span data-ttu-id="5a835-163">« Redémarrer l’appareil »</span><span class="sxs-lookup"><span data-stu-id="5a835-163">"Restart the device"</span></span>
* <span data-ttu-id="5a835-164">« Go to Sleep »</span><span class="sxs-lookup"><span data-stu-id="5a835-164">"Go to sleep"</span></span>
* <span data-ttu-id="5a835-165">« Quel est l’heure ? »</span><span class="sxs-lookup"><span data-stu-id="5a835-165">"What time is it?"</span></span>
* <span data-ttu-id="5a835-166">« Quelle batterie ai-je laissée ? »</span><span class="sxs-lookup"><span data-stu-id="5a835-166">"How much battery do I have left?"</span></span>



<br>

---

:::row:::
    :::column:::
        ## <a name="see-it-say-itbr"></a><span data-ttu-id="5a835-167">« Regardez-le, dites-le »</span><span class="sxs-lookup"><span data-stu-id="5a835-167">"See It, Say It"</span></span><br>
        <span data-ttu-id="5a835-168">HoloLens a un modèle de « voir », par exemple, le modèle d’entrée vocale, où les étiquettes sur les boutons indiquent aux utilisateurs les commandes vocales qu’ils peuvent également prononcer.</span><span class="sxs-lookup"><span data-stu-id="5a835-168">HoloLens has a "see it, say it" model for voice input, where labels on buttons tell users what voice commands they can say as well.</span></span> <span data-ttu-id="5a835-169">Par exemple, lors de la consultation d’une fenêtre d’application dans HoloLens (1re génération), un utilisateur peut prononcer la commande « Adjust » qui s’affiche dans la barre de l’application pour ajuster la position de l’application dans le monde.</span><span class="sxs-lookup"><span data-stu-id="5a835-169">For example, when looking at an app window in HoloLens (1st gen), a user can say the "Adjust" command which they see in the App bar to adjust the position of the app in the world.</span></span><br>
        <br>
        <span data-ttu-id="5a835-170">*Image : un utilisateur peut prononcer la commande « Adjust » qui s’affiche dans la barre de l’application pour ajuster la position de l’application*</span><span class="sxs-lookup"><span data-stu-id="5a835-170">*Image: A user can say the "Adjust" command which they see in the App bar to adjust the position of the app*</span></span>
    :::column-end:::
        :::column:::
        <span data-ttu-id="5a835-171">![space](images/spacer-20x582.png)</span><span class="sxs-lookup"><span data-stu-id="5a835-171">![space](images/spacer-20x582.png)</span></span><br>
        <span data-ttu-id="5a835-172">![Quand vous examinez une fenêtre d’application ou un hologramme, un utilisateur peut prononcer la commande « Adjust » qui s’affiche dans la barre de l’application pour ajuster la position de l’application dans le monde.](images/microphone-600px.png)</span><span class="sxs-lookup"><span data-stu-id="5a835-172">![When looking at an app window or hologram, a user can say the "Adjust" command which they see in the App bar to adjust the position of the app in the world](images/microphone-600px.png)</span></span><br>
    :::column-end:::
:::row-end:::


<br>



:::row:::
    :::column:::
        <span data-ttu-id="5a835-173">Lorsque les applications suivent cette règle, les utilisateurs peuvent facilement comprendre ce qu’il faut savoir pour contrôler le système.</span><span class="sxs-lookup"><span data-stu-id="5a835-173">When apps follow this rule, users can easily understand what to say to control the system.</span></span> <span data-ttu-id="5a835-174">Pour renforcer ce point, pendant que Gazing a un bouton dans HoloLens (1ère génération), vous verrez une info-bulle « de la voix » qui apparaît après une seconde si le bouton est activé pour la voix et affiche la commande pour dire à « appuyez ».</span><span class="sxs-lookup"><span data-stu-id="5a835-174">To reinforce this, while gazing at a button in HoloLens (1st gen), you will see a "voice dwell" tooltip that comes up after a second if the button is voice-enabled and displays the command to speak to "press" it.</span></span> <span data-ttu-id="5a835-175">Pour afficher les info-bulles vocales dans HoloLens 2, affichez le curseur vocal en disant « sélectionner » ou « que puis-je dire » (Voir l’image).</span><span class="sxs-lookup"><span data-stu-id="5a835-175">To reveal voice tooltips in HoloLens 2, show the voice cursor by saying "select" or "What can I say" (See image).</span></span> <br>
        <br>
        <span data-ttu-id="5a835-176">*Image : les commandes « voir » s’affichent sous les boutons*</span><span class="sxs-lookup"><span data-stu-id="5a835-176">*Image: "See it, say it" commands appear below the buttons*</span></span>
    :::column-end:::
        :::column:::
       ![Voyez-le, disons que les commandes s’affichent sous les boutons](images/voice-seeitsayit-600px.png)<br><br>
    :::column-end:::
:::row-end:::


<br>

---


## <a name="voice-commands-for-fast-hologram-manipulation"></a><span data-ttu-id="5a835-178">Commandes vocales pour une manipulation d’hologramme rapide</span><span class="sxs-lookup"><span data-stu-id="5a835-178">Voice commands for fast hologram manipulation</span></span>

<span data-ttu-id="5a835-179">Il existe un certain nombre de commandes vocales que vous pouvez prononcer Gazing sur un hologramme pour effectuer rapidement des tâches de manipulation.</span><span class="sxs-lookup"><span data-stu-id="5a835-179">There are a number of voice commands you can say while gazing at a hologram to quickly perform manipulation tasks.</span></span> <span data-ttu-id="5a835-180">Ces commandes vocales fonctionnent sur les fenêtres d’application, ainsi que sur les objets 3D que vous avez placés dans le monde.</span><span class="sxs-lookup"><span data-stu-id="5a835-180">These voice commands work on app windows as well as 3D objects you have placed in the world.</span></span>

<span data-ttu-id="5a835-181">**Commandes de manipulation d’hologramme**</span><span class="sxs-lookup"><span data-stu-id="5a835-181">**Hologram manipulation commands**</span></span>
* <span data-ttu-id="5a835-182">Me faire face</span><span class="sxs-lookup"><span data-stu-id="5a835-182">Face me</span></span>
* <span data-ttu-id="5a835-183">Plus grand | Enrichissement</span><span class="sxs-lookup"><span data-stu-id="5a835-183">Bigger | Enhance</span></span>
* <span data-ttu-id="5a835-184">Grande</span><span class="sxs-lookup"><span data-stu-id="5a835-184">Smaller</span></span>

<span data-ttu-id="5a835-185">Sur HoloLens 2, vous pouvez également créer des interactions plus naturelles en association avec un regard en œil qui fournit implicitement des informations contextuelles sur ce à quoi vous faites référence.</span><span class="sxs-lookup"><span data-stu-id="5a835-185">On HoloLens 2, you can also create more natural interactions in combination with eye-gaze which implicitly provides contextual information about what you are referring to.</span></span> <span data-ttu-id="5a835-186">Par exemple, vous pouvez simplement regarder un hologramme et indiquer « placer _ce_», puis passer à l’emplacement où vous souhaitez le placer et indiquer « sur _ce_point ».</span><span class="sxs-lookup"><span data-stu-id="5a835-186">For example, you could simply look at a hologram and say "put _this_" and then look over where you want to place it and say "over _here_".</span></span>
<span data-ttu-id="5a835-187">Ou bien, vous pouvez consulter un composant holographique sur une machine complexe et indiquer : « Donnez-moi plus d’informations à _ce_sujet ».</span><span class="sxs-lookup"><span data-stu-id="5a835-187">Or you could look at a holographic part on a complex machine and say: "give me more information about _this_".</span></span>



## <a name="discovering-voice-commands"></a><span data-ttu-id="5a835-188">Détection des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="5a835-188">Discovering voice commands</span></span>

<span data-ttu-id="5a835-189">Certaines commandes, telles que les commandes de manipulation rapide ci-dessus, peuvent être masquées.</span><span class="sxs-lookup"><span data-stu-id="5a835-189">Some commands, like the commands for fast manipulation above, can be hidden.</span></span> <span data-ttu-id="5a835-190">Pour en savoir plus sur les commandes que vous pouvez utiliser, pointez avec le regard sur un objet et dites « que puis-je prononcer ? ».</span><span class="sxs-lookup"><span data-stu-id="5a835-190">To learn about what commands you can use, gaze at an object and say, "what can I say?".</span></span> <span data-ttu-id="5a835-191">Une liste de commandes possibles s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5a835-191">A list of possible commands pops up.</span></span> <span data-ttu-id="5a835-192">Vous pouvez également utiliser le curseur point-tête pour rechercher et afficher les info-bulles vocales de chaque bouton devant vous.</span><span class="sxs-lookup"><span data-stu-id="5a835-192">You can also use the head gaze cursor to look around and reveal the voice tooltips for each button in front of you.</span></span> 

<span data-ttu-id="5a835-193">Si vous souhaitez obtenir la liste complète, dites « afficher toutes les commandes » à tout moment.</span><span class="sxs-lookup"><span data-stu-id="5a835-193">If you want a complete list, just say, "Show all commands" anytime.</span></span> 


## <a name="dictation"></a><span data-ttu-id="5a835-194">Dictation</span><span class="sxs-lookup"><span data-stu-id="5a835-194">Dictation</span></span>

<span data-ttu-id="5a835-195">Plutôt que de taper avec des [robinets](gaze-and-commit.md#composite-gestures), la dictée vocale peut être plus efficace pour entrer du texte dans une application.</span><span class="sxs-lookup"><span data-stu-id="5a835-195">Rather than typing with [air taps](gaze-and-commit.md#composite-gestures), voice dictation can be more efficient to enter text into an app.</span></span> <span data-ttu-id="5a835-196">Cela peut accélérer l’entrée avec moins d’efforts pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a835-196">This can greatly accelerate input with less effort for the user.</span></span>

<span data-ttu-id="5a835-197">![La dictée vocale commence en sélectionnant le bouton microphone](images/micbuttonfordictation.png)</span><span class="sxs-lookup"><span data-stu-id="5a835-197">![Voice dictation starts by selecting the microphone button](images/micbuttonfordictation.png)</span></span><br>
<span data-ttu-id="5a835-198">*La dictée vocale commence en sélectionnant le bouton microphone sur le clavier.*</span><span class="sxs-lookup"><span data-stu-id="5a835-198">*Voice dictation starts by selecting the microphone button on the keyboard*</span></span>

<span data-ttu-id="5a835-199">À chaque fois que le clavier holographique est actif, vous pouvez basculer en mode dictée au lieu de taper.</span><span class="sxs-lookup"><span data-stu-id="5a835-199">Any time the holographic keyboard is active, you can switch to dictation mode instead of typing.</span></span> <span data-ttu-id="5a835-200">Sélectionnez le microphone sur le côté de la zone d’entrée de texte pour commencer.</span><span class="sxs-lookup"><span data-stu-id="5a835-200">Select the microphone on the side of the text input box to get started.</span></span>


## <a name="adding-voice-commands-to-your-app"></a><span data-ttu-id="5a835-201">Ajout de commandes vocales à votre application</span><span class="sxs-lookup"><span data-stu-id="5a835-201">Adding voice commands to your app</span></span>

<span data-ttu-id="5a835-202">Il est recommandé d’ajouter des commandes vocales à toutes les expériences que vous créez.</span><span class="sxs-lookup"><span data-stu-id="5a835-202">Consider adding voice commands to any experience that you build.</span></span> <span data-ttu-id="5a835-203">La voix est un moyen puissant et pratique de contrôler le système et les applications.</span><span class="sxs-lookup"><span data-stu-id="5a835-203">Voice is a powerful and convenient way control the system and apps.</span></span> <span data-ttu-id="5a835-204">Étant donné le nombre de dialectes et d’accents qui peuvent être utilisés, il est important de bien choisir les mots clés de reconnaissance vocale, afin de garantir que les commandes de vos utilisateurs seront correctement interprétées.</span><span class="sxs-lookup"><span data-stu-id="5a835-204">Because users speak with a variety of dialects and accents, proper choice of speech keywords will make sure that your users' commands are interpreted unambiguously.</span></span>

### <a name="best-practices"></a><span data-ttu-id="5a835-205">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="5a835-205">Best practices</span></span>

<span data-ttu-id="5a835-206">Voici quelques bonnes pratiques qui faciliteront la reconnaissance vocale.</span><span class="sxs-lookup"><span data-stu-id="5a835-206">Below are some practices that will aid in smooth speech recognition.</span></span>
* <span data-ttu-id="5a835-207">**Utilisez des commandes concises** : dans la mesure du possible, choisissez des mots clés de deux syllabes minimum.</span><span class="sxs-lookup"><span data-stu-id="5a835-207">**Use concise commands** - When possible, choose keywords of two or more syllables.</span></span> <span data-ttu-id="5a835-208">Les mots d’une syllabe comprennent souvent des voyelles qui peuvent être prononcées différemment selon l’accent de la personne.</span><span class="sxs-lookup"><span data-stu-id="5a835-208">One-syllable words tend to use different vowel sounds when spoken by persons of different accents.</span></span> <span data-ttu-id="5a835-209">Exemple : « lire la vidéo » est préférable à « lire la vidéo actuellement sélectionnée »</span><span class="sxs-lookup"><span data-stu-id="5a835-209">Example: "Play video" is better than "Play the currently selected video"</span></span>
* <span data-ttu-id="5a835-210">**Utilisation d’un vocabulaire simple** -exemple : « afficher la note » est préférable à « afficher le résumé »</span><span class="sxs-lookup"><span data-stu-id="5a835-210">**Use simple vocabulary** - Example: "Show note" is better than "Show placard"</span></span>
* <span data-ttu-id="5a835-211">**Utilisez des commandes non définitives** : assurez-vous que les actions réalisables par les commandes de reconnaissance vocale peuvent être facilement annulées, en cas de déclenchement involontaire provoqué par une personne parlant près de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a835-211">**Make sure commands are non destructive** - Make sure any action that can be taken by a speech command is non destructive and can easily be undone in case another person speaking near the user accidentally triggers a command.</span></span>
* <span data-ttu-id="5a835-212">**Évitez les commandes avec des consonances similaires** : évitez d’enregistrer plusieurs commandes vocales ayant une consonance très similaire.</span><span class="sxs-lookup"><span data-stu-id="5a835-212">**Avoid similar sounding commands** - Avoid registering multiple speech commands that sound very similar.</span></span> <span data-ttu-id="5a835-213">Exemple : « afficher plus » et « afficher le magasin » peuvent être très similaires.</span><span class="sxs-lookup"><span data-stu-id="5a835-213">Example: "Show more" and "Show store" can be very similar sounding.</span></span>
* <span data-ttu-id="5a835-214">**Désinscrivez votre application lorsque vous ne l’utilisez pas** : lorsque l’état de votre application rend une commande de reconnaissance vocale non valide, désinscrivez l’application pour que les autres commandes ne soient pas confondues avec celle-ci.</span><span class="sxs-lookup"><span data-stu-id="5a835-214">**Unregister your app when not it use** - When your app is not in a state in which a particular speech command is valid, consider unregistering it so that other commands are not confused for that one.</span></span>
* <span data-ttu-id="5a835-215">**Testez les différents accents** : testez votre application avec des utilisateurs ayant différents accents.</span><span class="sxs-lookup"><span data-stu-id="5a835-215">**Test with different accents** - Test your app with users of different accents.</span></span>
* <span data-ttu-id="5a835-216">**Maintenez une certaine cohérence au sein des commandes vocales** : si la commande « Retour » permet de retourner à la page précédente, gardez ce comportement dans toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="5a835-216">**Maintain voice command consistency** - If "Go back" goes to the previous page, maintain this behavior in your applications.</span></span>
* <span data-ttu-id="5a835-217">**Évitez d’utiliser des commandes du système** : les commandes vocales suivantes sont réservées au système.</span><span class="sxs-lookup"><span data-stu-id="5a835-217">**Avoid using system commands** - The following voice commands are reserved for the system.</span></span> <span data-ttu-id="5a835-218">Elles ne doivent pas être utilisées par les applications.</span><span class="sxs-lookup"><span data-stu-id="5a835-218">These should not be used by applications.</span></span>
   * <span data-ttu-id="5a835-219">« Hey Cortana »</span><span class="sxs-lookup"><span data-stu-id="5a835-219">"Hey Cortana"</span></span>
   * <span data-ttu-id="5a835-220">« Sélectionner »</span><span class="sxs-lookup"><span data-stu-id="5a835-220">"Select"</span></span>
   * <span data-ttu-id="5a835-221">« Aller au début »</span><span class="sxs-lookup"><span data-stu-id="5a835-221">"Go to start"</span></span>

### <a name="advantages-of-voice-input"></a><span data-ttu-id="5a835-222">Avantages de l’entrée vocale</span><span class="sxs-lookup"><span data-stu-id="5a835-222">Advantages of voice input</span></span>

<span data-ttu-id="5a835-223">La voix est un moyen naturel de communiquer nos intentions.</span><span class="sxs-lookup"><span data-stu-id="5a835-223">Voice input is a natural way to communicate our intents.</span></span> <span data-ttu-id="5a835-224">La voix est particulièrement intéressante pour les **parcours** d’interface, car elle peut aider les utilisateurs à franchir plusieurs étapes d’une interface (un utilisateur peut indiquer « revenir en arrière » lors de la consultation d’une page Web, au lieu de devoir cliquer sur le bouton précédent de l’application).</span><span class="sxs-lookup"><span data-stu-id="5a835-224">Voice is especially good at interface **traversals** because it can help users cut through multiple steps of an interface (a user might say "go back" while looking at a webpage, instead of having to go up and hit the back button in the app).</span></span> <span data-ttu-id="5a835-225">Cette économie d’énergie a un **effet émotionnelle** puissant sur la perception de l’expérience de l’utilisateur et lui donne une petite quantité d’Superpower.</span><span class="sxs-lookup"><span data-stu-id="5a835-225">This small time saving has a powerful **emotional effect** on user’s perception of the experience and gives them a small amount superpower.</span></span> <span data-ttu-id="5a835-226">L’utilisation de la voix est également pratique lorsque nous avons les mains occupées ou que nous effectuons **plusieurs tâches en même temps**.</span><span class="sxs-lookup"><span data-stu-id="5a835-226">Using voice is also a convenient input method when we have our arms full or are **multi-tasking**.</span></span> <span data-ttu-id="5a835-227">Sur les appareils où la saisie sur un clavier est difficile, la **dictée vocale** peut être un moyen efficace d’entrer du texte.</span><span class="sxs-lookup"><span data-stu-id="5a835-227">On devices where typing on a keyboard is difficult, **voice dictation** can be an efficient alternative way to input text.</span></span> <span data-ttu-id="5a835-228">Enfin, dans certains cas, lorsque la **plage de précision** du point de vue et du mouvement est limitée, la voix peut aider à lever l’ambiguïté de l’intention de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a835-228">Lastly, in some cases when the **range of accuracy** for gaze and gesture are limited, voice can help to disambiguate the user's intent.</span></span> 

<span data-ttu-id="5a835-229">**Avantages de l’utilisation de la voix**</span><span class="sxs-lookup"><span data-stu-id="5a835-229">**How using voice can benefit the user**</span></span>
* <span data-ttu-id="5a835-230">Gain de temps : l’objectif final est donc plus facile à atteindre.</span><span class="sxs-lookup"><span data-stu-id="5a835-230">Reduces time - it should make the end goal more efficient.</span></span>
* <span data-ttu-id="5a835-231">Efforts moindres : l’exécution des tâches est plus fluide et ne demande pas d’efforts.</span><span class="sxs-lookup"><span data-stu-id="5a835-231">Minimizes effort - it should make tasks more fluid and effortless.</span></span>
* <span data-ttu-id="5a835-232">Réduction de la charge cognitive : les commandes vocales sont intuitives, et faciles à apprendre et à mémoriser.</span><span class="sxs-lookup"><span data-stu-id="5a835-232">Reduces cognitive load - it's intuitive, easy to learn, and remember.</span></span>
* <span data-ttu-id="5a835-233">Acceptation sociale : leur comportement s’inscrit facilement dans les normes sociétales.</span><span class="sxs-lookup"><span data-stu-id="5a835-233">It's socially acceptable - it should fit in with societal norms in terms of behavior.</span></span>
* <span data-ttu-id="5a835-234">Routine : l’utilisation de la voix peut facilement se transformer en habitude.</span><span class="sxs-lookup"><span data-stu-id="5a835-234">It's routine - voice can readily become a habitual behavior.</span></span>

### <a name="challenges-for-voice-input"></a><span data-ttu-id="5a835-235">Défis liés à l’entrée vocale</span><span class="sxs-lookup"><span data-stu-id="5a835-235">Challenges for voice input</span></span>

<span data-ttu-id="5a835-236">Bien que les entrées vocales soient intéressantes pour de nombreuses applications différentes, elles sont également confrontées à plusieurs défis.</span><span class="sxs-lookup"><span data-stu-id="5a835-236">While voice input is great for a lot of different applications, it also faces several challenges.</span></span> <span data-ttu-id="5a835-237">Le fait de comprendre les avantages et les défis liés aux entrées vocales permet aux développeurs d’applications de faire des choix plus intelligents quant à la façon et au moment d’utiliser les entrées vocales et à créer une expérience optimale pour leurs utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5a835-237">Understanding both the advantages and challenges for voice input enables app developers to make smarter choices for how and when to use voice input and to create a great experience for their users.</span></span>

<span data-ttu-id="5a835-238">**Entrée vocale pour le contrôle d’entrée continu** Le contrôle affiné est l’un d’eux.</span><span class="sxs-lookup"><span data-stu-id="5a835-238">**Voice input for continuous input control** Fine-grained control is one of them.</span></span> <span data-ttu-id="5a835-239">Par exemple, un utilisateur peut souhaiter modifier son volume dans son application musical.</span><span class="sxs-lookup"><span data-stu-id="5a835-239">For example, a user might want to change their volume in their music app.</span></span> <span data-ttu-id="5a835-240">Elle peut simplement indiquer « plus fort », mais il n’est pas clair que le système est censé créer le volume.</span><span class="sxs-lookup"><span data-stu-id="5a835-240">She can simply say "louder", but it's not clear how much louder the system is supposed to make the volume.</span></span> <span data-ttu-id="5a835-241">L’utilisateur peut par exemple : « en faire un peu plus fort », mais « un peu » est difficile à quantifier.</span><span class="sxs-lookup"><span data-stu-id="5a835-241">The user could say: "Make it a little louder", but "a little" is difficult to quantify.</span></span> <span data-ttu-id="5a835-242">Le déplacement ou la mise à l’échelle d’hologrammes avec la voix est tout aussi difficile.</span><span class="sxs-lookup"><span data-stu-id="5a835-242">Moving or scaling holograms with voice is similarly difficult.</span></span> 

<span data-ttu-id="5a835-243">**Fiabilité de la détection des entrées vocales** Bien que les systèmes d’entrée de voix soient plus performants et mieux, ils peuvent parfois entendre et interpréter une commande vocale de manière incorrecte.</span><span class="sxs-lookup"><span data-stu-id="5a835-243">**Reliability of voice input detection** While voice input systems become better and better, sometimes they may incorrectly hear and interpret a voice command.</span></span>
<span data-ttu-id="5a835-244">La clé consiste à résoudre ce problème dans votre application en fournissant des commentaires à l’utilisateur lorsque le système est à l’écoute et ce que le système a compris pour créer une clarté sur les problèmes potentiels en maîtrisant correctement l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a835-244">The key is to address this challenge in your application by providing feedback to the user when the system is listening and what the system understood to create clarity on potential issues in correctly understanding the user.</span></span>  

<span data-ttu-id="5a835-245">**Entrée vocale dans les espaces partagés** La voix ne peut pas être socialement acceptable dans les espaces que vous partagez avec d’autres personnes.</span><span class="sxs-lookup"><span data-stu-id="5a835-245">**Voice input in shared spaces** Voice may not be socially acceptable in spaces that you share with others.</span></span>
<span data-ttu-id="5a835-246">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="5a835-246">Here are a few examples:</span></span>
* <span data-ttu-id="5a835-247">Il se peut que l’utilisateur ne souhaite pas déranger les autres (par exemple, dans une bibliothèque silencieuse ou un bureau partagé)</span><span class="sxs-lookup"><span data-stu-id="5a835-247">The user may not want to disturb others (e.g., in a quiet library or shared office)</span></span>
* <span data-ttu-id="5a835-248">Il se peut que les utilisateurs ne soient pas contraints de parler à eux-mêmes en public,</span><span class="sxs-lookup"><span data-stu-id="5a835-248">Users may feel awkward being seen talking to themselves in public,</span></span>
* <span data-ttu-id="5a835-249">Un utilisateur peut paraître inconfortant de dicter un message personnel ou confidentiel (y compris des mots de passe), tandis que d’autres sont à l’écoute</span><span class="sxs-lookup"><span data-stu-id="5a835-249">A user may feel uncomfortable dictating a personal or confidential message (including passwords) while others are listening</span></span>

<span data-ttu-id="5a835-250">**Entrée vocale de mots uniques ou inconnus** Les problèmes d’entrée vocale se posent également lorsque les utilisateurs dictent des mots qui peuvent être inconnus du système, tels que des surnoms, certains mots d’argot ou abréviations.</span><span class="sxs-lookup"><span data-stu-id="5a835-250">**Voice input of unique or unknown words** Difficulties for voice input also come when users are dictating words that may be unknown to the system, such as nicknames, certain slang words or abbreviations.</span></span> 

<span data-ttu-id="5a835-251">**Apprentissage des commandes vocales** Tandis que l’objectif ultime est de naturellement communiquer avec votre système, les applications s’appuient souvent sur des commandes vocales prédéfinies spécifiques.</span><span class="sxs-lookup"><span data-stu-id="5a835-251">**Learning voice commands** While the ultimate goal is to naturally converse with your system, often times apps still rely on specific pre-defined voice commands.</span></span>
<span data-ttu-id="5a835-252">Un défi associé à un grand nombre de commandes vocales est de savoir comment les enseigner sans surcharger l’utilisateur et comment aider l’utilisateur à les conserver.</span><span class="sxs-lookup"><span data-stu-id="5a835-252">A challenge associated with a big set of voice commands is how to teach them without overloading the user and how to help the user to retain them.</span></span> 

<br>

---

### <a name="voice-feedback-states"></a><span data-ttu-id="5a835-253">Retours des commandes vocales</span><span class="sxs-lookup"><span data-stu-id="5a835-253">Voice feedback states</span></span>

<span data-ttu-id="5a835-254">Lorsque la voix est utilisée correctement, l’utilisateur **comprend ce qu’il peut dire et reçoit la confirmation** que le système a **bien compris sa commande**.</span><span class="sxs-lookup"><span data-stu-id="5a835-254">When Voice is applied properly, the user understands **what they can say and get clear feedback** the system **heard them correctly**.</span></span> <span data-ttu-id="5a835-255">Ce sont ces deux éléments qui donnent envie à l’utilisateur de choisir la voix comme méthode d’entrée principale.</span><span class="sxs-lookup"><span data-stu-id="5a835-255">These two signals make the user feel confident in using Voice as a primary input.</span></span> <span data-ttu-id="5a835-256">Voici un diagramme qui montre ce qui se passe au niveau du curseur lorsque l’entrée vocale est reconnue, et comment celle-ci est communiquée à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a835-256">Below is a diagram showing what happens to the cursor when voice input is recognized and how it communicates that to the user.</span></span>


:::row:::
    :::column:::
       <span data-ttu-id="5a835-257">![1. état normal du curseur](images/voicefeedbackstates-regular.jpg)</span><span class="sxs-lookup"><span data-stu-id="5a835-257">![1. Regular cursor state](images/voicefeedbackstates-regular.jpg)</span></span><br>
       <span data-ttu-id="5a835-258">**1. état normal du curseur**</span><span class="sxs-lookup"><span data-stu-id="5a835-258">**1. Regular cursor state**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="5a835-259">![2. communique les commentaires vocaux, puis disparaît](images/voicefeedbackstates-voice.jpg)</span><span class="sxs-lookup"><span data-stu-id="5a835-259">![2. Communicates voice feedback and then disappears](images/voicefeedbackstates-voice.jpg)</span></span><br>
        <span data-ttu-id="5a835-260">**2. communique les commentaires vocaux, puis disparaît**</span><span class="sxs-lookup"><span data-stu-id="5a835-260">**2. Communicates voice feedback and then disappears**</span></span><br>
    :::column-end:::
    :::column:::
       <span data-ttu-id="5a835-261">![1,3.</span><span class="sxs-lookup"><span data-stu-id="5a835-261">![\*3.</span></span> <span data-ttu-id="5a835-262">État de curseur normal](images/voicefeedbackstates-regular.jpg)</span><span class="sxs-lookup"><span data-stu-id="5a835-262">Regular cursor state](images/voicefeedbackstates-regular.jpg)</span></span><br>
       <span data-ttu-id="5a835-263">**3. retourne à l’état de curseur normal**</span><span class="sxs-lookup"><span data-stu-id="5a835-263">**3. Returns to regular cursor state**</span></span><br>
    :::column-end:::
:::row-end:::

<br>

---

<br>

## <a name="top-things-users-should-know-about-speech-in-mixed-reality"></a><span data-ttu-id="5a835-264">Points importants concernant la reconnaissance vocale dans la réalité mixte</span><span class="sxs-lookup"><span data-stu-id="5a835-264">Top things users should know about "speech" in mixed reality</span></span>
* <span data-ttu-id="5a835-265">Vous devez dire **« Sélectionner »** lorsque vous ciblez un bouton (vous pouvez l’utiliser n’importe où pour cliquer sur un bouton).</span><span class="sxs-lookup"><span data-stu-id="5a835-265">Say **"Select"** while targeting a button (you can use this anywhere to click a button).</span></span>
* <span data-ttu-id="5a835-266">Dans certaines applications, vous pouvez prononcer le **nom de l’étiquette d’un bouton de la barre d’application** pour exécuter une action.</span><span class="sxs-lookup"><span data-stu-id="5a835-266">You can say the **label name of an app bar button** in some apps to take an action.</span></span> <span data-ttu-id="5a835-267">Par exemple, lorsqu’il regarde une application, l’utilisateur peut prononcer la commande « Supprimer » pour supprimer cette application (cela vous évite d’avoir à la supprimer manuellement).</span><span class="sxs-lookup"><span data-stu-id="5a835-267">For example, while looking at an app, a user can say the command "Remove" to remove the app from the world (this saves time from having to click it with your hand).</span></span>
* <span data-ttu-id="5a835-268">Vous pouvez activer Cortana à l’aide de la commande **« Hey Cortana »**.</span><span class="sxs-lookup"><span data-stu-id="5a835-268">You can initiate Cortana listening by saying **"Hey Cortana."**</span></span> <span data-ttu-id="5a835-269">Vous pouvez lui poser des questions (« Hey Cortana, combien mesure la tour Eiffel ? »), lui demander d’ouvrir une application (« Hey Cortana, ouvre Netflix ») ou lui demander d’afficher le menu Démarrer (« Hey Cortana, ouvre le menu Démarrer »), et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="5a835-269">You can ask her questions ("Hey Cortana, how tall is the Eiffel tower"), tell her to open an app ("Hey Cortana, open Netflix"), or tell her to bring up the Start Menu ("Hey Cortana, take me home") and more.</span></span>

## <a name="common-questions-and-concerns-users-have-about-voice"></a><span data-ttu-id="5a835-270">Questions et inquiétudes fréquentes concernant la reconnaissance vocale</span><span class="sxs-lookup"><span data-stu-id="5a835-270">Common questions and concerns users have about voice</span></span>
* <span data-ttu-id="5a835-271">Que dois-je dire ?</span><span class="sxs-lookup"><span data-stu-id="5a835-271">What can I say?</span></span>
* <span data-ttu-id="5a835-272">Comment savoir si le système m’a bien entendu ?</span><span class="sxs-lookup"><span data-stu-id="5a835-272">How do I know the system heard me correctly?</span></span>
   * <span data-ttu-id="5a835-273">Le système ne comprend pas mes commandes vocales.</span><span class="sxs-lookup"><span data-stu-id="5a835-273">The system keeps getting my voice commands wrong.</span></span>
   * <span data-ttu-id="5a835-274">Il ne réagit pas quand je lui adresse une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="5a835-274">It doesn’t react when I give it a voice command.</span></span>
* <span data-ttu-id="5a835-275">Il réagit de façon inadaptée lorsque je lui adresse une commande vocale.</span><span class="sxs-lookup"><span data-stu-id="5a835-275">It reacts the wrong way when I give it a voice command.</span></span>
* <span data-ttu-id="5a835-276">Comment choisir l’application ou la commande d’application à laquelle adresser mes commandes vocales ?</span><span class="sxs-lookup"><span data-stu-id="5a835-276">How do I target my voice to a specific app or app command?</span></span>
* <span data-ttu-id="5a835-277">Puis-je utiliser la voix pour contrôler les éléments holographiques sur HoloLens ?</span><span class="sxs-lookup"><span data-stu-id="5a835-277">Can I use voice to command things out the holographic frame on HoloLens?</span></span>

## <a name="communication"></a><span data-ttu-id="5a835-278">Communication</span><span class="sxs-lookup"><span data-stu-id="5a835-278">Communication</span></span>

<span data-ttu-id="5a835-279">Pour les applications qui souhaitent tirer parti des options de traitement d’entrée audio personnalisées fournies par HoloLens, il est important de comprendre les différentes [catégories de flux audio](https://msdn.microsoft.com/library/windows/desktop/hh404178(v=vs.85).aspx) que votre application peut consommer.</span><span class="sxs-lookup"><span data-stu-id="5a835-279">For applications that want to take advantage of the customized audio input processing options provided by HoloLens, it is important to understand the various [audio stream categories](https://msdn.microsoft.com/library/windows/desktop/hh404178(v=vs.85).aspx) your app can consume.</span></span> <span data-ttu-id="5a835-280">Windows 10 prend en charge plusieurs catégories de flux et HoloLens utilise trois d’entre elles pour permettre un traitement personnalisé afin d’optimiser la qualité audio du microphone adaptée à la parole, à la communication et à d’autres qui peuvent être utilisées pour les scénarios de capture audio d’environnement ambiant (par exemple, « Camcorder »).</span><span class="sxs-lookup"><span data-stu-id="5a835-280">Windows 10 supports several different stream categories and HoloLens makes use of three of these to enable custom processing to optimize the microphone audio quality tailored for speech, communication and other which can be used for ambient environment audio capture (i.e. "camcorder") scenarios.</span></span>
* <span data-ttu-id="5a835-281">La catégorie de flux de AudioCategory_Communications est personnalisée pour les scénarios de qualité des appels et de narration et fournit au client un flux audio mono 16kHz 24bit de la voix de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a835-281">The AudioCategory_Communications stream category is customized for call quality and narration scenarios and provides the client with a 16kHz 24bit mono audio stream of the user's voice</span></span>
* <span data-ttu-id="5a835-282">La catégorie de flux de AudioCategory_Speech est personnalisée pour le moteur de reconnaissance de la parole HoloLens (Windows) et lui fournit un flux mono 16kHz 24bit de la voix de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a835-282">The AudioCategory_Speech stream category is customized for the HoloLens (Windows) speech engine and provides it with a 16kHz 24bit mono stream of the user's voice.</span></span> <span data-ttu-id="5a835-283">Cette catégorie peut être utilisée par les moteurs de reconnaissance vocale tiers si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5a835-283">This category can be used by 3rd party speech engines if needed.</span></span>
* <span data-ttu-id="5a835-284">La catégorie de flux de AudioCategory_Other est personnalisée pour l’enregistrement audio de l’environnement ambiant et fournit au client un flux audio stéréo de 48 bits.</span><span class="sxs-lookup"><span data-stu-id="5a835-284">The AudioCategory_Other stream category is customized for ambient environment audio recording and provides the client with a 48kHz 24 bit stereo audio stream.</span></span>

<span data-ttu-id="5a835-285">Tout ce traitement audio est l’accélération matérielle, ce qui signifie que les fonctionnalités se déchargent beaucoup moins d’énergie que si le même traitement a été effectué sur l’UC HoloLens.</span><span class="sxs-lookup"><span data-stu-id="5a835-285">All this audio processing is hardware accelerated which means the features drain a lot less power than if the same processing was done on the HoloLens CPU.</span></span> <span data-ttu-id="5a835-286">Évitez d’exécuter un autre traitement d’entrée audio sur le processeur pour maximiser la durée de vie de la batterie du système et tirer parti du traitement des entrées audio déchargées et intégrées.</span><span class="sxs-lookup"><span data-stu-id="5a835-286">Avoid running other audio input processing on the CPU to maximize system battery life and take advantage of the built in, offloaded audio input processing.</span></span>

## <a name="languages"></a><span data-ttu-id="5a835-287">Languages</span><span class="sxs-lookup"><span data-stu-id="5a835-287">Languages</span></span>

<span data-ttu-id="5a835-288">HoloLens 2 [prend en charge plusieurs langues](https://docs.microsoft.com/hololens/hololens2-language-support).</span><span class="sxs-lookup"><span data-stu-id="5a835-288">HoloLens 2 [supports multiple languages](https://docs.microsoft.com/hololens/hololens2-language-support).</span></span> <span data-ttu-id="5a835-289">N’oubliez pas que les commandes vocales s’exécutent toujours dans la langue d’affichage du système même si plusieurs claviers sont installés ou si les applications essaient de créer un module de reconnaissance vocale dans une autre langue.</span><span class="sxs-lookup"><span data-stu-id="5a835-289">Keep in mind that speech commands will always run in the system's display language even if multiple keyboards are installed or if apps attempt to create a speech recognizer in a different language.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5a835-290">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="5a835-290">Troubleshooting</span></span>

<span data-ttu-id="5a835-291">Si vous rencontrez des problèmes à l’aide de « SELECT » et de « Hey Cortana », essayez de passer à un espace plus silencieux, à l’extérieur de la source de bruit, ou en parlant plus fort.</span><span class="sxs-lookup"><span data-stu-id="5a835-291">If you're having any issues using "select" and "Hey Cortana", try moving to a quieter space, turning away from the source of noise, or by speaking louder.</span></span> <span data-ttu-id="5a835-292">À ce stade, toute la reconnaissance vocale sur HoloLens est réglée et optimisée spécifiquement pour les intervenants natifs de États-Unis anglais.</span><span class="sxs-lookup"><span data-stu-id="5a835-292">At this time, all speech recognition on HoloLens is tuned and optimized specifically to native speakers of United States English.</span></span>

<span data-ttu-id="5a835-293">Pour la version 2017 de Windows Mixed Reality Edition, la logique de gestion des points de terminaison audio fonctionnera correctement (éternellement) après la déconnexion et la réinitialisation du PC Desktop après la première connexion HMD.</span><span class="sxs-lookup"><span data-stu-id="5a835-293">For the Windows Mixed Reality Developer Edition release 2017, the audio endpoint management logic will work fine (forever) after logging out and back in to the PC desktop after the initial HMD connection.</span></span> <span data-ttu-id="5a835-294">Avant le premier événement de déconnexion/dans le cas de l’utilisation de WMR OOBE, l’utilisateur peut rencontrer différents problèmes de fonctionnalité audio, qu’il s’agisse d’aucun audio ou d’aucune commutation audio, en fonction de la configuration du système avant de connecter le HMD pour la première fois.</span><span class="sxs-lookup"><span data-stu-id="5a835-294">Prior to that first sign out/in event after going through WMR OOBE, the user could experience various audio functionality issues ranging from no audio to no audio switching depending on how the system was set up prior to connecting the HMD for the first time.</span></span>

<br>

---

## <a name="voice-input-in-mrtk-mixed-reality-toolkit-for-unity"></a><span data-ttu-id="5a835-295">Entrée vocale dans MRTK (ensemble d’outils de réalité mixte) pour Unity</span><span class="sxs-lookup"><span data-stu-id="5a835-295">Voice input in MRTK (Mixed Reality Toolkit) for Unity</span></span>
<span data-ttu-id="5a835-296">Avec **[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)**, vous pouvez facilement affecter une commande vocale à n’importe quel objet.</span><span class="sxs-lookup"><span data-stu-id="5a835-296">With **[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity)**, you can easily assign voice command on any objects.</span></span> <span data-ttu-id="5a835-297">Utilisez le **profil d’entrée vocale** de MRTK pour définir vos mots clés.</span><span class="sxs-lookup"><span data-stu-id="5a835-297">Use MRTK's **Speech Input Profile** to define your keywords.</span></span> <span data-ttu-id="5a835-298">En affectant le script **SpeechInputHandler** , vous pouvez faire en sorte qu’un objet réponde aux mots clés définis dans le profil d’entrée vocal.</span><span class="sxs-lookup"><span data-stu-id="5a835-298">By assigning **SpeechInputHandler** script, you can make any object respond to the keywords defined in the Speech Input Profile.</span></span> <span data-ttu-id="5a835-299">SpeechInputHandler fournit également une étiquette de confirmation vocale pour améliorer la confiance de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5a835-299">SpeechInputHandler also provides speech confirmation label to improve the user's confidence.</span></span>

* [<span data-ttu-id="5a835-300">Commande MRTK-Voice</span><span class="sxs-lookup"><span data-stu-id="5a835-300">MRTK - Voice command</span></span>](https://microsoft.github.io/MixedRealityToolkit-Unity/Documentation/Input/Speech.html)


---

## <a name="see-also"></a><span data-ttu-id="5a835-301">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5a835-301">See also</span></span>
* [<span data-ttu-id="5a835-302">Pointer et valider</span><span class="sxs-lookup"><span data-stu-id="5a835-302">Gaze and commit</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="5a835-303">Interactions instinctuelles</span><span class="sxs-lookup"><span data-stu-id="5a835-303">Instinctual interactions</span></span>](interaction-fundamentals.md)
* [<span data-ttu-id="5a835-304">Réalité mixte - Entrées - Cours 212 : Voix</span><span class="sxs-lookup"><span data-stu-id="5a835-304">MR Input 212: Voice</span></span>](holograms-212.md)
* [<span data-ttu-id="5a835-305">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="5a835-305">Voice input in DirectX</span></span>](voice-input-in-directx.md)
* [<span data-ttu-id="5a835-306">Entrée vocale dans Unity</span><span class="sxs-lookup"><span data-stu-id="5a835-306">Voice input in Unity</span></span>](voice-input-in-unity.md)
